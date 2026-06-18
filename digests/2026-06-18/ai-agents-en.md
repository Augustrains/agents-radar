# OpenClaw Ecosystem Digest 2026-06-18

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-18 02:14 UTC

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

Here is the **OpenClaw Project Digest** for **2026-06-18**.

---

## 1. Today's Overview
The project remains in a state of **high maintenance activity** but with **concerning bug volume**. In the last 24 hours, 500 issues and 500 PRs were updated, though only 17 issues were closed (3.4%) and 52 PRs were merged/closed (10.4%). There are **zero new releases**, suggesting the team is deep in a stabilization cycle rather than shipping new versions. The backlog of **483 open/active issues** and **448 open PRs** indicates a significant review and resolution bottleneck. Security, session-state integrity, and message-loss bugs dominate the top-tier discussions.

## 2. Releases
**None.** No new releases were published in the last 24 hours.

## 3. Project Progress
In the last 24 hours, 52 PRs were merged or closed. Key progress includes:
- **Paginations fixes (Feishu/Lark):** PRs [#94161](https://github.com/openclaw/openclaw/pull/94161), [#94173](https://github.com/openclaw/openclaw/pull/94173), and [#94181](https://github.com/openclaw/openclaw/pull/94181) fixed pagination for bitable tables, document block listings, and message reactions. These were silent data-loss bugs for users with large Feishu workspaces.
- **Agent text delivery:** PR [#94327](https://github.com/openclaw/openclaw/pull/94327) (by wangmiao0668000666) added a fallback mechanism for subagent completion delivery when the requester session is inactive or locked.
- **Streaming integrity:** PR [#94247](https://github.com/openclaw/openclaw/pull/94247) fixed a `block-streamed delivery` bug where paragraph separators were lost across streamed chunks.
- **UI fixes:** PR [#94325](https://github.com/openclaw/openclaw/pull/94325) fixed a critical UI glitch where the raw config textarea was invisible after switching from Form mode. PR [#94361](https://github.com/openclaw/openclaw/pull/94361) added scroll-to behavior for cron run history.
- **WhatsApp observe-only:** PR [#94357](https://github.com/openclaw/openclaw/pull/94357) introduced `observe-only` message hooks for WhatsApp, allowing passive monitoring without auto-reply.
- **Provider externalization:** PR [#94350](https://github.com/openclaw/openclaw/pull/94350) externalized the GMI provider plugin, moving it to an official publishable package.

## 4. Community Hot Topics
The most active discussions reflect deep concerns about **security boundaries**, **session state**, and **agent reliability**.

- **#25592 – Text between tool calls leaks to messaging channels** (32 comments, Diamond Lobster) — [Issue Link](https://github.com/openclaw/openclaw/issues/25592)
  - **Analysis:** This is the single most discussed issue. Users are seeing internal agent processing output (error handling, narration) leaked to Slack/iMessage. The P1 security tag means the team is likely prioritizing a fix.

- **#88838 – Track core session/transcript SQLite migration via accessor seam** (30 comments, Diamond Lobster) — [Issue Link](https://github.com/openclaw/openclaw/issues/88838)
  - **Analysis:** A maintainer-driven discussion about breaking a massive session-store rewrite into small, reviewable PRs. This signals a major architectural shift that will affect reliability for weeks.

- **#9443 – Request: Prebuilt Android APK releases** (25 comments, Off-Meta Tidepool) — [Issue Link](https://github.com/openclaw/openclaw/issues/9443)
  - **Analysis:** A clear UX pain point: the Android companion app exists in source but requires compilation. Users are asking for basic CI/CD artifact delivery.

- **#68596 – Configurable streaming watchdog timeout threshold** (15 comments, 8 👍) — [Issue Link](https://github.com/openclaw/openclaw/issues/68596)
  - **Analysis:** Extended-reasoning models (DeepSeek-R1, kimi-k2.5) frequently trigger false-positive watchdog resets. The high reaction count (8 👍) suggests many users hitting this.

- **#39604 – `web_fetch` private network access config** (13 comments, 9 👍) — [Issue Link](https://github.com/openclaw/openclaw/issues/39604)
  - **Analysis:** Highest-reaction issue today. Users need to fetch from internal services (localhost, 10.x, 192.168.x) but are currently blocked. The strong demand suggests this will land soon.

## 5. Bugs & Stability
The bug landscape is dominated by **security regressions** and **crash-loop risks**.

**Critical (P0-P1, Security/Data Loss):**
- **#25592 – Text leak to channels** (P1, Security) — Active. See Hot Topics.
- **#62505 – Coding Agent never completes** (P1, Regression) — [Issue Link](https://github.com/openclaw/openclaw/issues/62505)
  - A regression between v2026.4.2 and now. Agent outputs "vague status updates" and nothing else. No fix PR linked.
- **#22676 – Signal daemon SIGUSR1 restart race condition** (P1, Crash-loop) — [Issue Link](https://github.com/openclaw/openclaw/issues/22676)
  - Orphaned processes + port conflicts on restart. Linked PR exists.
- **#10659 – Masked Secrets** (P1, Security) — [Issue Link](https://github.com/openclaw/openclaw/issues/10659)
  - Agents can see raw API keys stored in `.env`. No fix shipped.

**High (P1-P2, Session State / Auth):**
- **#29387 – Bootstrap files in agentDir silently ignored** (P1, Session-state) — [Issue Link](https://github.com/openclaw/openclaw/issues/29387)
  - Per-agent bootstrap files are completely ignored. Only workspace directory files load.
- **#31583 – `exec` tool ignores `skills.entries.*.env` variables** (P1, Regression) — [Issue Link](https://github.com/openclaw/openclaw/issues/31583)
  - Environment variables configured per-skill are not passed to subprocesses.
- **#32473 – Control UI HTTPS/localhost secure context requirement** (P2, Regression) — [Issue Link](https://github.com/openclaw/openclaw/issues/32473)
  - Users on VPS/Docker with Brave key hit this error with no clear resolution path.

**Fix PRs observed in the 24h window:**
- [#94311](https://github.com/openclaw/openclaw/pull/94311) fixes **auto-grant model override** loss (relates to #94289).
- [#94096](https://github.com/openclaw/openclaw/pull/94096) fixes **inverted date range** rejection in usage APIs.
- [#94247](https://github.com/openclaw/openclaw/pull/94247) fixes **paragraph separator loss** in block streaming.

## 6. Feature Requests & Roadmap Signals
Several high-demand features suggest what will ship in the next major release:

- **Masked Secrets (#10659, P1, Diamond Lobster):** Very likely to land soon. The security risk is rated critically, and the community is vocal.
- **Configurable streaming watchdog (#68596, 8 👍):** Likely to be added as a config key (`streaming.watchdogTimeout`) in a patch release for extended-reasoning model support.
- **`web_fetch` private network access (#39604, 9 👍):** Strongest community signal today. Likely to ship as `tools.web.fetch.allowPrivateNetwork`.
- **Slack Block Kit support (#12602, P2):** Not critical, but would unlock rich interactive responses (CRM cards, tables). Unlikely to be next release, but likely on the roadmap.
- **Filesystem sandboxing config (#7722, 7 👍):** Users want `allowedPaths`/`denyPaths` for file tools. Currently in design/review.
- **Multi-Agent Collaboration enhancement (#35203, RFC):** A comprehensive RFC covering capability profiling, shared blackboard, and token cost governance. This is a medium-to-long-term architecture play.

## 7. User Feedback Summary
**Real pain points expressed today:**
- "The Coding Agent just stopped working. It apologizes for being vague and does nothing." (#62505)
- "I can't get the Control UI to work on my VPS because of HTTPS requirements." (#32473)
- "I can't use `web_fetch` to talk to my own internal services." (#39604 – 9 upvotes)
- "I have to compile the Android app myself. Why is there no APK?" (#9443)
- "My agent's environment variables from the config are not being passed to scripts." (#31583)
- "I don't want my internal processing text sent to Slack." (#25592 – most commented issue)

**Positive signals:**
- The community is actively submitting high-quality, well-structured PRs (e.g., [#93567](https://github.com/openclaw/openclaw/pull/93567), [#94327](https://github.com/openclaw/openclaw/pull/94327)).
- Documentation is being actively improved (PRs [#93941](https://github.com/openclaw/openclaw/pull/93941), [#93942](https://github.com/openclaw/openclaw/pull/93942), [#94332](https://github.com/openclaw/openclaw/pull/94332)).
- External provider plugins are being formalized (GMI externalized via #94350), which indicates confidence in the plugin ecosystem.

## 8. Backlog Watch
Several important issues show signs of **maintainer neglect** or **stale status**:

- **#9443 – Prebuilt Android APK** (Created Feb 5, last updated Jun 18) — 25 comments, no assigned milestone. *Needs maintainer product decision.*
- **#6731 – Safe/unsafe ClawdBot (Rust rewrite)** (Created Feb 2) — An ambitious but vague request with no movement.
- **#50248 – Session cleanup prunes fresh cron sessions** (Created Mar 19, stale) — Data loss risk but no fix PR linked.
- **#45765 – `OPENCLAW_HOME` nested directory bug** (Created Mar 14, regression) — English-language reproduction, but the reporter (Chinese user max2055) is describing a real path resolution bug.
- **#37966 – `cacheRetention` ignored for LiteLLM-proxied Anthropic** (Created Mar 6, stale) — LiteLLM users getting no prompt caching despite paying for it.
- **#13616 – Backup/restore utility** (Created Feb 10) — No movement. Users managing production deployments lack a disaster recovery path.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided community digest summaries.

---

## Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem
**Date:** 2026-06-18

### 1. Ecosystem Overview

The open-source personal AI agent ecosystem is exhibiting a split between high-velocity, feature-rich "reference" projects (OpenClaw) and a wave of specialized forks and new entrants focused on specific deployment scenarios (e.g., lightweight hardware, desktop control, cloud-native). A clear trend is the community's demand for **stability and reliability** over raw feature addition, with several projects experiencing critical bugs related to context management, session state, and security boundaries. The landscape is maturing, with projects like OpenClaw and IronClaw addressing complex multi-agent orchestration and architectural rewrites, while others like NullClaw and TinyClaw cater to minimalist or niche hardware users. Security, particularly around agent prompt injection and data leakage to messaging channels, has become a top-tier concern across the board.

### 2. Activity Comparison

| Project | Issues (Updated/Total Open) | PRs (Updated/Merged) | Releases (Last 24h) | Health Signal |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 / 483 | 500 / 52 | None | 🟡 **Concerning** - High bug volume, severe backlog bottleneck. |
| **NanoBot** | 9 / ~7 | 18 / 18 | None | 🟢 **Healthy** - High velocity, good fix rate. |
| **Hermes Agent** | 50 / 45 | 50 / 7 | None | 🟢 **Healthy** - High activity, focused on Windows/cross-platform. |
| **PicoClaw** | 4 / ~2 | 10 / 6 | None | 🟢 **Good** - Steady progress with clear security focus. |
| **NanoClaw** | 5 / 4 | 19 / 3 | **2 (v2.1.0, v2.1.17)** | 🟡 **Stabilizing** - Breaking changes, rapid hotfixes. |
| **NullClaw** | 3 / 3 | 2 / 0 | None | 🟡 **Low Activity** - No merges, 2 new critical PRs awaiting review. |
| **IronClaw** | 49 / 26 | 50 / 17 | None | 🟢 **High Intensity** - "Reborn" architecture in rapid "fix and ship" mode. |
| **LobsterAI** | 0 / 0 | 13 / 13 | **1 (2026.6.15)** | 🟢 **Very Healthy** - Clean backlog, strong focus on polish. |
| **Moltis** | 2 / 2 | 1 / 0 | None | 🟡 **Idle** - Low activity, single feature PR. |
| **CoPaw** | 47 / ~24 | 50 / 32 | **2 (v1.1.12, v2.0.0a1)** | 🟡 **Volatile** - High feature velocity but significant stability issues. |
| **ZeptoClaw** | 0 | 0 | None | ⚪ **Inactive** - No activity in 24h. |
| **TinyClaw** | 0 | 0 | None | ⚪ **Inactive** - No activity in 24h. |

*(Note: "Health Signal" is an analyst assessment based on the 24-hour window. A single day of low activity does not indicate a project's overall health.)*

### 3. OpenClaw's Position

- **Advantages vs. Peers:** OpenClaw remains the clear **reference implementation** with the largest community (500 updated issues/PRs). It has the most extensive integration ecosystem (Slack, iMessage, WhatsApp, Feishu, etc.) and is the primary target for architectural improvements, such as the session SQLite migration (#88838). It is the "main trunk" from which many other projects (e.g., PicoClaw, NanoClaw) derive or are inspired.
- **Technical Approach Differences:** OpenClaw employs a monolithic, plugin-rich architecture. This contrasts with lighter forks like **NanoBot** (more streamlined, MCP-focused) and **IronClaw** (undergoing a "Reborn" WebUI rewrite). While powerful, this complexity is directly linked to its high bug volume and review bottleneck (483 open issues, 448 open PRs).
- **Community Size Comparison:** OpenClaw's community is an order of magnitude larger than all others. It sets the agenda for common problems (e.g., session state, security leaks). However, this scale creates a **maintenance debt** that other, more nimble projects are currently avoiding or solving in a more focused way.

### 4. Shared Technical Focus Areas

The following requirements are emerging as cross-project priorities, indicating industry-wide pain points:

| Focus Area | Projects Affected | Specific Community Needs |
| :--- | :--- | :--- |
| **Context/Session Management** | **OpenClaw**, **NanoClaw**, **CoPaw**, **ZeroClaw** | Process freezes on compaction (CoPaw #5218), silent data loss (OpenClaw #29387), lack of cron context (ZeroClaw #6105). |
| **Security & Leak Prevention** | **OpenClaw**, **NanoClaw**, **CoPaw** | Internal agent text leaking to chat channels (OpenClaw #25592), full RCE via prompt injection in cloud (CoPaw #5234), path traversal in file tools (NanoClaw #2799). |
| **Windows & Cross-Platform Stability** | **Hermes Agent**, **NanoClaw**, **ZeroClaw**, **CoPaw** | Build failures (Hermes #47917), 74 test failures (ZeroClaw #7462), installer bugs (CoPaw #5286), Docker backend path issues (Hermes #48168). |
| **Multi-Agent & Agent-to-Agent (A2A) Protocols** | **Hermes Agent**, **ZeroClaw**, **NanoClaw** | Community push for standardized inter-agent communication (Hermes #514), governance/per-message approvals (NanoClaw #2793), context sharing. |
| **Model Fallback & Watchdog Configuration** | **OpenClaw**, **NanoBot**, **Hermes Agent** | False watchdog resets for extended-reasoning models (OpenClaw #68596), need for configurable context window per fallback model (NanoBot #4389), empty model/provider fields (Hermes #48061). |

### 5. Differentiation Analysis

| Feature Focus | Project(s) | Target User / Use Case | Key Characteristic |
| :--- | :--- | :--- | :--- |
| **Maximum Extensibility / "Swiss Army Knife"** | **OpenClaw** | Developers, power users, multi-platform integrators. | Plugin ecosystem, wide protocol support, but complex. |
| **Desktop Computer-Use & WebUI Polish** | **IronClaw**, **LobsterAI** | Users needing a GUI-driven agent with screen control (IronClaw) or a polished Cowork mode (LobsterAI). | Focus on UX and real-time interaction, "Reborn" WebUI. |
| **Lightweight / Minimalist / Edge** | **Moltis**, **NullClaw**, **TinyClaw** | Users with resource-constrained hardware, headless servers, or specific, simple tasks. | Low activity, slow iteration, focused on stability. |
| **Cloud-Native & Managed Deployments** | **NanoClaw**, **CoPaw** | Teams deploying agents on fleets or in the cloud. | Docker/immutable VM support, upgrade state tracking, broader concerns about cloud security. |
| **China-Market & WeChat Integration** | **CoPaw**, **OpenClaw** | Users heavily reliant on Chinese messaging ecosystems (Feishu, XiaoYi). | Deep integrations with local platforms, dual WebSocket refactors for reliability. |

### 6. Community Momentum & Maturity

- **Tier 1: Rapidly Iterating / High Intensity**
    - **IronClaw, ZeroClaw, CoPaw, NanoBot**: These projects show a very high PR merge rate and are actively shipping new features or major architectural changes (IronClaw's "Reborn", CoPaw's AgentScope 2.0 migration). Stability is a secondary concern to velocity.
- **Tier 2: Stabilizing & Hardening**
    - **LobsterAI, PicoClaw, Hermes Agent**: These projects are focusing on bug fixes, security patches, and quality-of-life improvements. They are building trust through rapid issue resolution and a clean backlog (LobsterAI being the prime example).
- **Tier 3: Maintenance & Low Activity**
    - **NullClaw, Moltis, TinyClaw, ZeptoClaw**: These projects are either in a quiet period or have a small, dedicated maintainer base. Innovation is slow, but they serve niche users well.

### 7. Trend Signals

1.  **Reliability Over Features:** The most upvoted and commented issues across all projects are not about new features, but about **reliability**—context compaction freezes, session state loss, message leaks, and silent failures. Developers are being hired to fix integration, not add it.
2.  **The "Agentic Desktop" is a Major Battleground:** The high demand for desktop computer-use (ZeroClaw #6909) and polished WebUIs (IronClaw's Reborn) signals that the industry is moving beyond chat-based assistants towards agents that can directly interact with the user's operating system and native applications.
3.  **Security is an Ecosystem Risk:** From full RCE in cloud deployments (CoPaw) to silent text leaks to Slack (OpenClaw), security vulnerabilities are not isolated. A single major exploit in a popular project like OpenClaw could erode trust in the entire ecosystem. **Sandboxing, input/output validation, and credential management are no longer optional.**
4.  **Agent-to-Agent (A2A) is the Next Frontier:** The most-upvoted feature request in Hermes Agent (#514) and the active PRs in NanoClaw (#2793) indicate that the community is preparing for a future where multiple agents must collaborate. Standardization will be a key value driver for the project that leads on this.
5.  **Windows is a Second-Class Citizen No More:** The sheer volume of Windows-specific bugs (builds, installers, path handling, IME input) across Hermes Agent, NanoClaw, CoPaw, and ZeroClaw shows a significant, underserved, and vocal user base. Projects that invest in first-class Windows support will gain a significant market share.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for **2026-06-18**.

---

## NanoBot Project Digest – 2026-06-18

### 1. Today's Overview
NanoBot is experiencing a surge in development velocity, with 18 PRs merged/closed and 12 still open in the last 24 hours, signaling a healthy release cycle. Community engagement is high, with 9 issues updated, though only 2 were closed, indicating a growing backlog. The project is heavily focused on stability and polish, with numerous bug fixes targeting MCP servers, filesystem safety, WebUI, and provider compatibility. New feature requests continue to pour in, particularly around multi-instance management and improved onboarding, showing strong traction among less-technical users.

### 2. Releases
No new releases were published today. The last version remains unreported in this window.

### 3. Project Progress (Merged/Closed PRs)
18 PRs were merged or closed today, demonstrating significant advancement across multiple areas:
- **Provider & API Fixes**: `#4351` (Better Mistral support, fixed `reasoning_effort` values and `max_tokens` mapping), `#4356` (Sanitize Anthropic `tool_use`/`tool_result` IDs), `#4367` (Disable proxy for local endpoints like Ollama/vLLM, respecting env proxy for cloud).
- **WebUI & UX**: `#4283` (Corrected activity duration display in the WebUI), `#4347` (Fixed model preset switching in MyTool).
- **Feishu (Lark) Integration**: `#4381` (Recover failed Feishu streaming updates with retries), `#4354` (Send read receipts/blue ticks for WhatsApp messages).
- **Memory & Session**: `#4349` (Preserved user turns in replay-window history to prevent LLM context start in the middle of a turn).
- **Filesystem & Tools**: `#4053` (Kept read-only roots out of write paths for security), `#4202` (Clarified filesystem workspace write policy), `#4380` (Allowed git commands in workspace subdirectories).
- **Stability & Logging**: `#4385` (Logged primary model error before fallback to aid debugging), `#4386` (Silenced unroutable CLI progress noise).
- **Web Search**: `#4350` (Added Keenable as a built-in web search provider).

### 4. Community Hot Topics
- **#936 – Multi-Tenant Gateway (Feature Request)** – *1 comment, 0 👍* – This long-standing request (since Feb) was updated today. The user wants a single gateway to manage multiple agents to reduce container overhead. It signals a clear need for simpler scaling solutions.
- **#4376 – User-friendly Wizard (Enhancement)** – *1 comment, 1 👍* – The highest-liked open issue today. The author explicitly calls out that the current `--wizard` assumes too much technical knowledge, a direct pain point for new/non-technical users.
- **#4390 – Multi-instances for Normies (Enhancement)** – *0 comments* – A brand-new request echoing the frustration with multi-instance setup per the wiki. The user wants to *hide* UI settings and simplify configuration, suggesting a desire for a more opinionated, out-of-the-box experience.
- **#4303 – MCP Server Crash on Close (Bug Fix)** – *High activity* – This open PR addresses a critical runtime crash when MCP server sessions terminate. The discussion is centered on fixing an asyncio scope exit bug, showing the community is actively helping stabilize core infrastructure.

### 5. Bugs & Stability
| Severity | Issue / PR | Description | Fix Status |
| :--- | :--- | :--- | :--- |
| **Critical** | **#4360** (Closed) | Installer crashes in fresh Docker image with "end of file unexpected" | **Fixed** |
| **High** | **#4388** (Open) | WebUI: iOS Safari auto-zooms on input field click, causing UI breakage | **No fix PR yet** |
| **High** | **#4322** (Closed) | `NameError: 'session_key' is not defined` after merge – crashes agent startup | **Fixed** |
| **Medium** | **#4303** (Open) | MCP `streamableHttp` server crashes on reconnect with `RuntimeError` | **Fix PR #4303 open** |
| **Medium** | **#4381** (Closed) | Feishu streaming card updates fail silently, leaving blank cards | **Fixed in #4381** |
| **Low** | **#4386** (Closed) | Unroutable progress calls add noise to CLI logs for unknown channels | **Fixed in #4386** |

**Key takeaway**: The project is highly reactive to bugs, with multiple critical and high-severity issues closed within the same day. The iOS WebUI zoom issue (#4388) is the most visible remaining bug for mobile users.

### 6. Feature Requests & Roadmap Signals
- **Multi-Instance / Multi-Tenant Simplification**: Issues #936 (Multi-tenant gateway) and #4390 (Multi-instances for normies) both attack the same problem from different angles. **Prediction**: A "simplified multi-agent" mode, possibly controlled via a single YAML config, is likely in the next minor release (0.3.x or 0.2.2).
- **Per-Model `contextWindowTokens`**: Request #4389 asks for context window configuration per fallback model. This is a nuanced but critical feature for power users mixing models with different context limits (e.g., GPT-4 vs. a smaller local model). **Prediction**: Likely to be accepted and shipped within the next release cycle if a PR appears.
- **On-demand Heartbeat Trigger**: RFC #3437 wants a manual heartbeat trigger for debugging `HEARTBEAT.md` behavior without incurring execution costs. This signals that the advanced agentic features are becoming complex enough to need developer tooling. **Prediction**: Low priority but could land as a hidden CLI flag or a debug mode toggle.
- **Cron-Level Model/Preset Switching**: Request #4378 explores a workaround for scheduled model switching (e.g., cron job calling a script). **Prediction**: The maintainers may add a built-in `cron`-driven preset overrider, turning this workaround into a native feature.

### 7. User Feedback Summary
- **Positive**: Users are generally satisfied with the project's responsiveness to bugs. The quick fix for the Docker installer (#4360) and the MCP server crash (#4303) shows the team values stability.
- **Pain Points (High Volume)**:
    1.  **Onboarding Friction**: "Nanobot onboard --wizard assumes you know many technical details" (#4376) – Direct feedback that the initial setup is too complex.
    2.  **Multi-Agent Complexity**: "Running multiple agents requires separate gateway containers… increasing resource usage" (#936) and "1 machine, multi-instances… I want to be able to hide UI settings" (#4390) – Users want a simpler, resource-efficient way to run multiple agents.
    3.  **Mobile UX**: "In the latest code… clicking the input field still triggers page auto-zoom" (#4388) – A persistent UI issue on iOS Safari.
- **Satisfaction**: The community is actively contributing high-quality fixes (e.g., PR #4380 fixing git workspace subdirectory issues, PR #4354 adding WhatsApp read receipts), indicating a healthy, engaged contributor base.

### 8. Backlog Watch
- **🔴 Issue #3437 – RFC: On-demand heartbeat trigger** – *Updated 2026-06-17* – First updated April 25. This is a mature request with technical detail (Phase 1/Phase 2 separation) but has seen no maintainer response. It could block advanced debugging workflows.
- **🔴 Issue #936 – Multi-Tenant Gateway** – *Updated 2026-06-17* – First reported Feb 21. This is the longest-standing open feature request with real user demand. Maintainer triage or a comment on feasibility is overdue.
- **🔴 PR #4205 – Mailbox-backed subagent results** – *Updated 2026-06-17* – Open since June 5. A significant architectural change to subagent communication. It has not been merged or formally reviewed despite multiple updates to the branch. This needs maintainer attention to avoid stagnation.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-18

## Today's Overview

Hermes Agent shows a burst of high activity today, with 50 issues and 50 PRs updated in the last 24 hours. The project has 45 open active issues and 43 open PRs, indicating a healthy flow of community contributions and bug reports. No new releases were published today, but the development pipeline is busy with 7 merged/closed PRs. Cross-platform stability (Windows, macOS, Linux) remains a recurring theme, as does gateway and desktop build reliability.

## Releases

No new releases today. The latest available version remains v0.16.0 (2026-06-05).

## Project Progress

Seven PRs were merged or closed today:

- **#48147** `feat(relay): connector⇄gateway channel auth + signed-HTTP inbound receiver + enroll CLI` — A significant feature that authenticates the connector-to-gateway relay channel and adds the gateway's signed-HTTP inbound delivery receiver plus enrollment CLI.
- **#48149** `[Bug]: gh CLI authentication fails with 401/Blocked` — Closed after resolution.
- **#47477** `[Feature]: WhatsApp Group Sending with Hermes Skill (Termux)` — A community guide was merged.
- **#47967** `[Bug]: XML tool call syntax in external file content generates phantom tool calls` — Closed (needs-repro label previously applied).
- **#48084** `bug(desktop): electronDist path mismatch` — Closed as duplicate.
- **#48059** `[Bug]: macOS desktop build fails — electronDist does not exist` — Closed as duplicate.
- **#48084** duplicate resolution for `electronDist` path issue.

Additional open PRs that advanced include **#48168** and **#48157** (both fixing Windows Docker backend drive-letter path issues), **#48170** (stripping timestamp metadata from chat payloads), and **#48162** (fixing Chinese IME input display on Windows). The `was_auto_reset` flag fix for slash commands (**#48174**, **#48166**) also progressed.

## Community Hot Topics

1. **#514** — *[Feature]: A2A (Agent-to-Agent) Protocol Support*  
   **22 comments, 18 👍**  
   The most-discussed and most-upvoted issue. Community members are actively discussing inter-agent communication standards based on Google's A2A protocol. Underlying need: users want Hermes to interoperate with other agent frameworks through standardized discovery and communication, complementing MCP's tool focus.  
   [Issue Link](https://github.com/NousResearch/hermes-agent/issues/514)

2. **#47917** — *[Bug]: Desktop build fails after update — electronDist does not exist (cache invalidated)*  
   **8 comments, 1 👍**  
   High attention because multiple duplicate reports exist (#48084, #48059). The `electronDist` path resolution bug affects Windows, macOS, and Linux builds across different update paths.  
   [Issue Link](https://github.com/NousResearch/hermes-agent/issues/47917)

3. **#27555** — *[Bug]: vision fallback_chain silently broken — wrong kwargs in _resolve_single_provider*  
   **7 comments**  
   A critical bug in image processing fallback chains that causes silent failures. Community frustration stems from the silent nature — users don't know their vision features are degraded.  
   [Issue Link](https://github.com/NousResearch/hermes-agent/issues/27555)

4. **#46260** — *[Bug]: INSTALL DIDN'T FINISH — npm install exit code 1 on Windows 10*  
   **6 comments**  
   Windows installer reliability concerns, especially with npm lifecycle scripts.  
   [Issue Link](https://github.com/NousResearch/hermes-agent/issues/46260)

5. **#13072** — *[Feature]: CLI Auto-Queue Mode with Smart Interrupt and Crash Recovery*  
   **5 comments, 1 👍**  
   A long-standing feature request (since April) for improving CLI workflow with queuing and crash recovery.  
   [Issue Link](https://github.com/NousResearch/hermes-agent/issues/13072)

## Bugs & Stability

### P1 — Critical

- **#48061** — *Hermes Agent v0.16.0 still sends empty runtime model/provider on Linux pipx install* (Open)  
  Requests fail with `max_retries_exhausted` due to empty MODEL and PROVIDER fields. No fix PR linked yet.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/48061)

### P2 — High

- **#47917** — *Desktop build fails after update — electronDist does not exist* (Open)  
  Multiple duplicates reported today (#48059, #48084). Active fix discussions but no merged solution yet.
- **#46260** — *Windows installer fails at "desktop" stage — npm install exit code 1* (Open)
- **#48167** — *Gateway GUI start button doesn't work, but 'hermes gateway run' CLI works fine* (Open)  
  Windows-specific gateway GUI issue.
- **#48161** — *Chinese IME input not displayed until next keypress on Windows* (Open)  
  PR #48162 exists to fix this — `patch_stdout` VT mode toggle interference with IME composition.
- **#48150** — *Plain text gateway adapters swallow Markdown bullet lists and literal asterisks* (Open)  
  PR #48165 submitted to fix the `strip_markdown` regex.
- **#48133** — *Gateway timestamp strip fails on Windows multi-word timezone names* (Open)
- **#48055** — `/new` does not reset model to config default after session-only /model switch* (Open)
- **#48173** — *Mid-session model switch leaves stale Model/Provider in persisted system prompt* (Open)
- **#48172** — *macOS app-bundle Chrome is ignored by local tool availability check* (Open)
- **#27555** — *vision fallback_chain silently broken* (Open) — P1 severity noted in issue description.
- **#32497** — *Hermes unexpectedly modifies its own skills/system prompts* (Open)
- **#47006** — *Custom-endpoint onboarding wizard hard-fails on OpenAI-compatible endpoints without /v1/models* (Open)

### P3 — Moderate

- **#40692** — *Desktop Composer typing extremely laggy with long conversation history on macOS* (Open)
- **#48100** — *Windows installer fails with "Access Denied" on pythonw.exe during auto-update* (Open)
- **#48098** — *Desktop shows stale "Summarizing thread" status after compaction resumes* (Open)

### Closed Today

- **#47967** — XML tool call syntax bug (closed, needs-repro)
- **#48084**, **#48059** — electronDist duplicates (closed)
- **#48149** — gh CLI auth failure (closed)

## Feature Requests & Roadmap Signals

### High-Potential Features for Next Release

1. **A2A Protocol Support (#514)** — The most-upvoted feature request. Given strategic alignment with inter-agent standards and high community demand, this could be a v0.17 priority.

2. **CLI Auto-Queue Mode (#13072)** — Smart interrupt and crash recovery for CLI. The author (Apostol Apostolov) provided a detailed design draft. Likely candidate for inclusion.

3. **Kanban Board in Desktop (#48159)** — Already exists in CLI and web dashboard; extending to Electron app is incremental.

4. **System Tray Support (#48163)** — A PR was submitted today adding close-to-tray behavior on Windows/Linux.

5. **OpenAI Responses API text verbosity (#20203)** — Configuration support for `text.verbosity` parameter (low/medium/high). Small scope, tangible UX improvement.

6. **`hermes usage` CLI command (#21814)** — Expose token/quota information in CLI and as an agent tool.

### Other Notable Requests

- **Nous Portal credit balance CLI (#33376)** — Users want to check credits without leaving the terminal.
- **WhatsApp Group Sending (#47477)** — Community guide merged; official support may follow.
- **Frequent File Paths injection (#47885)** — PR submitted to reduce file-search iterations, improving efficiency.

## User Feedback Summary

### Pain Points

1. **Windows installation and build failures** dominate user frustration this week. Multiple duplicate reports about `electronDist` path issues, npm lifecycle failures, and "Access Denied" during auto-update point to a systematic Windows packaging problem.

2. **CLI input issues on Windows** — Chinese IME users face significant friction with input composition. The fix PR (#48162) suggests this is a known issue with `patch_stdout()`.

3. **Silent failures** — The vision fallback chain bug (#27555) and empty model/provider (#48061) both fail silently, eroding user trust in the system's reliability.

4. **Gateway usability** — GUI start button not working on Windows (#48167), stale status indicators, and Markdown stripping in plain-text adapters (#48150) create a fragmented gateway experience.

### Satisfaction Signals

- Community is actively contributing fixes and features — 7 PRs merged today.
- Detailed bug reports with system information and reproduction steps indicate invested user base.
- Feature requests like A2A protocol support show users see Hermes as a platform for inter-agent ecosystems.

## Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Status |
|-------|-----|--------|
| **#514** *A2A Protocol Support* | 3+ months (Mar 2026) | Highest community demand, no maintainer response yet |
| **#8359** *Docs/specs out of sync with ACP, pricing, Honcho, container CLI* | 2+ months (Apr 2026) | Documentation drift affecting developer experience |
| **#13072** *CLI Auto-Queue Mode* | 2 months (Apr 2026) | Detailed design draft, no maintainer engagement |
| **#27555** *Vision fallback_chain silently broken* | 1 month (May 2026) | P1-impact bug with no fix PR in sight |
| **#32497** *Hermes modifies own skills/system prompts* | 3+ weeks (May 2026) | Concerning agent autonomy issue |

### PRs Needing Review

- **#24158** — MCP array schema sanitization for Codex (May 12, 36 days open) — Fixes a cross-platform compatibility issue.
- **#36286** — MiniMax China-region OAuth provider (June 1, 17 days open) — Regional feature expansion.
- **#43277** — Respect exhausted cooldowns in codex pool fallback resolver (June 10, 8 days open) — Auth reliability fix.
- **#47885** — Frequent file paths injection (June 17, 1 day open) — Efficiency improvement, low risk.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the structured digest for the PicoClaw open-source AI assistant project.

---

# PicoClaw Project Digest – 2026-06-18

## Today's Overview
Activity remains robust, with 10 pull requests and 4 issues updated in the last 24 hours. The project merged 6 PRs, including critical security fixes and a high-impact Gemini model compatibility patch. No new releases were published today. Maintainer attention is split between stabilizing core features (spawn sub-agents, web search) and addressing community feature requests for additional messaging gateways.

## Releases
**No new releases** were tagged on this date. The last available release remains unchanged.

## Project Progress
Six pull requests were merged or closed today, advancing several areas:
- **Security – OneBot inbound fetch** (#3140): Merged a fix that blocks attacker-controlled `message[].data.url` fields from fetching private network addresses. The fix reuses existing HTTP guard logic from `web_fetch` and `media_url` handlers. (lc6464)
- **Gemini 3.5 Flash Support** (#3136): Closed the blocking issue for tool execution failures by setting both `camelCase` and `snake_case` `thought_signature` fields in the request body. This enables compatibility with Gemini 3.5 Flash’s Agentic reasoning schema. (ZOOWH)
- **Web Search – Sogou** (#3139): Fixed a parsing break caused by HTML structure changes on Sogou’s WAP search page. (SiYue-ZO)
- **Web UI – Session History** (#2990, stale): Merged a fix that restores full conversation history display, addressing a regression where only the last user message was visible. (yuxuan-7814)
- **Review Feature** (#3138): Merged a Korean-language PR (`리뷰기능 추가`) adding a review/rating feature to the project (exact scope TBD on translation).

## Community Hot Topics
- **#3088 – Use vodozemac instead of libolm** (Open, 2 👍): The most-upvoted open issue. User pbsds wants to replace the unmaintained and insecure `libolm` library with `vodozemac`, the official replacement. The proposed implementation makes `libolm` optional at compile time. This issue carries a **high priority** label and has one comment from a contributor.
- **#3142 – Fix spawn sub-turn duplicate messages** (Open): A current PR fixing a logic gap in `subturn.go` where both `ForLLM` and `ForUser` were set with identical content, causing duplicate push notifications.
- **#3093 – SimpleX / Tox gateway** (Open, stale): User Damian-o2 requests support for SimpleX or Tox messaging protocols, reflecting demand for decentralized chat backends.

## Bugs & Stability
- **[HIGH] Gemini 3.5 Flash tool execution failure** (CLOSED #3111): Tool calls to the new `gemini-3.5-flash` model resulted in a `400 Bad Request`. Root cause: the schema used `thoughtSignature` (camelCase) only, while Gemini 3.5 Flash requires `thought_signature` (snake_case). **Fixed in #3136**.
- **[MID] Spawn sub-agent duplicate message delivery** (OPEN #3142): When a spawn sub-agent completes, `subturn.go` sets both `ForLLM` and `ForUser` to the same content, triggering two independent push attempts. A fix PR is open and under review.
- **[LOW] Sogou web search parsing regression** (CLOSED #3139): HTML structure changes on Sogou’s WAP page broke result extraction. **Fixed**.
- **[CRITICAL] OneBot private network fetch vulnerability** (CLOSED #3070/#3140): A security advisory detailed that attacker-controlled media URLs could be fetched from the host’s private network. **Fixed and merged**.

## Feature Requests & Roadmap Signals
- **vodozemac migration** (#3088): High-priority request to replace `libolm`. Likely to land in the next minor release given the "high priority" label.
- **Decentralized messaging gateways** (#3093): Requests for SimpleX, Tox, or Wire gateways persist. The DeltaChat gateway PR (#3063) is still open, suggesting this is an active development track.
- **NEAR AI Cloud provider** (#2917, merged earlier): A new OpenAI-compatible provider for NEAR AI Cloud has been integrated, enabling TEE-capable model usage.

## User Feedback Summary
- **Pain Point – Gemini 3.5 Flash compatibility**: Users reported broken tool execution with the newest Gemini model. The fix was well-received and quickly merged.
- **Pain Point – Session history truncation**: Users could only see the last user message in long conversations. The fix (#2990) addresses this long-standing UX issue.
- **Satisfaction – Security responsiveness**: The OneBot vulnerability was reported, assigned an advisory, and fixed within 8 days. Community trust in maintainer responsiveness appears strong.
- **Dissatisfaction – libolm dependency**: Users are pushing for a migration away from an unmaintained crypto library, signaling impatience with technical debt.

## Backlog Watch
- **#3092 – fix(skills_install): version/force type assertion checks** (OPEN, stale, since 2026-06-10): This PR adds proper `ok` checks for type assertions in the skills installer. It has no comments and appears neglected. A silent failure risk for users running `force-reinstall` commands.
- **#3063 – DeltaChat gateway** (OPEN, since 2026-06-08): A large feature PR adding a full DeltaChat messaging gateway. Zero maintainer comments to date. This is a high-value contribution that risks becoming stale.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-18

## Today's Overview

NanoClaw posted **high activity** today with 19 pull requests updated (16 open, 3 merged/closed) and 5 issues updated (4 open, 1 closed). Two new releases (v2.1.17 and v2.1.0) shipped, both containing breaking changes requiring migration attention. The project is in a **stability sprint**: the majority of today's PRs are bug fixes, security patches, and documentation corrections, with a clear focus on hardening the delivery pipeline, CLI tooling, and credential management. Community contributions are strong, with several users submitting fixes for documentation gaps they encountered during setup.

## Releases

Two releases landed today:

### v2.1.17
- **Rollup release** covering all `package.json` bumps from v2.1.1 through v2.1.17
- **[BREAKING]** `@onecli-sh/sdk` 0.5.0 → 2.2.1 — requires a OneCLI server with the `/v1` API. Older servers will 404 every SDK call. The sanctioned gateway and CLI are now pinned.

### v2.1.0
- **Rollup release** covering v2.0.65 through v2.1.0
- **[BREAKING]** Startup now requires an upgrade marker file (`data/upgrade-state.json`). The host refuses to boot unless the file records that the install reached the current version through a sanctioned upgrade path.

**Migration note:** Deployments must upgrade their OneCLI server to a `/v1`-compatible version before updating the SDK. Immutable VM/fleet deployments should set `NANOCLAW_DISABLE_UPGRADE_TRIPWIRE=1` to bypass the new startup check (see PR #2780 below).

## Project Progress

Three pull requests were merged/closed today:

- **PR #2797** (merged) — [fix(delivery): isolate per-session failures so one bad session can't stall delivery for all](https://github.com/nanocoai/nanoclaw/pull/2797)  
  Fixes Issue #2796. The delivery loop now wraps each session in its own `try/catch` instead of a single global block, preventing a single `outbound.db` read failure from halting message delivery for all agents. **Critical stability improvement.**

- **PR #2794** (merged) — [fix(providers): restore env-var gateway auth for managed fleets](https://github.com/nanocoai/nanoclaw/pull/2794)  
  Managed-fleet agents (baked into immutable VM images) could no longer authenticate to the LLM after v2.1.17. Restores environment-variable-based gateway auth for these deployments.

- **PR #2780** (merged) — [feat(upgrade-state): env opt-out for the startup tripwire (managed fleets)](https://github.com/nanocoai/nanoclaw/pull/2780)  
  Adds `NANOCLAW_DISABLE_UPGRADE_TRIPWIRE=1` environment variable to allow immutable deployments to bypass the new v2.1.0 startup upgrade check.

## Community Hot Topics

- **[Issue #2796](https://github.com/nanocoai/nanoclaw/issues/2796) (CLOSED)** — "One unhealthy session stalls message delivery for all agents"  
  Reported by mashkovtsevlx, who also submitted the fix (PR #2797). This was the **highest-impact bug** reported today: a single session with a momentarily unreadable `outbound.db` would halt delivery for every agent until daemon restart. The issue had 1 comment and was fixed within the same day — excellent turnaround.

- **[PR #2799](https://github.com/nanocoai/nanoclaw/pull/2799)** — "fix(security): confine send_file reads to /workspace (CVE-2026-29611)"  
  A security vulnerability where `send_file` accepted absolute paths without canonicalization, allowing a prompt-injected or compromised agent to read any container-visible file (credentials, mounted files). Sturdy4days submitted this fix with a **CVE identifier** assigned (CVE-2026-29611). High interest from the security-conscious community.

- **[PR #2793](https://github.com/nanocoai/nanoclaw/pull/2793)** — "feat(agent-to-agent): per-message approval policies on connected agents"  
  A feature PR from moshe-nanoco adding an optional approval gate between connected agents. When enabled, messages from Agent A to Agent B are held for approval before delivery. Fully backward-compatible (no policy = free flow). This is likely to generate significant community discussion about multi-agent governance patterns.

## Bugs & Stability

| Severity | Issue | Status | Fix PR? |
|----------|-------|--------|---------|
| **Critical** | [Delivery stall on single session failure](https://github.com/nanocoai/nanoclaw/issues/2796) — all agents blocked | CLOSED | ✅ PR #2797 merged |
| **Critical** | [CVE-2026-29611: send_file path traversal](https://github.com/nanocoai/nanoclaw/pull/2799) — any container file readable by compromised agent | OPEN | ✅ PR #2799 open |
| **High** | [CLI `ncl messaging-groups create` always throws](https://github.com/nanocoai/nanoclaw/pull/2804) — NOT NULL constraint missing `instance` column | OPEN | ✅ PR #2804 open |
| **High** | [Socket client has no timeout or response-size cap](https://github.com/nanocoai/nanoclaw/pull/2802) — hangs forever on unresponsive host | OPEN | ✅ PR #2802 open |
| **Medium** | [CLI `ncl groups create` allows path traversal via `--folder`](https://github.com/nanocoai/nanoclaw/pull/2800) — CWE-22 | OPEN | ✅ PR #2800 open |
| **Medium** | [safeParseContent breaks on non-object JSON](https://github.com/nanocoai/nanoclaw/pull/2801) — primitives return undefined fields | OPEN | ✅ PR #2801 open |
| **Low** | [Setup token parsing fails under wrapped PTY](https://github.com/nanocoai/nanoclaw/pull/2805) | OPEN | ✅ PR #2805 open |

**Notable:** All bugs reported today already have fix PRs open, and the most critical (delivery stall) was fixed and merged same-day. Security vulnerabilities are receiving prompt attention with CVE tracking.

## Feature Requests & Roadmap Signals

- **Per-message approval policies** (PR #2793) — adds governance to agent-to-agent connections. Likely to land in v2.2.0 as a major capability for multi-agent deployments requiring compliance gates.

- **CLI dashboard skill** (PR #2795) — a read-only CLI-derived dashboard as a standalone utility skill. Indicates community demand for better observability tooling.

- **Atlas Cloud LLM backend** (PR #2717, open since 2026-06-09) — documentation-only addition adding a new OpenAI-compatible provider. Still open after 9 days, suggesting maintainers may be vetting the provider integration more carefully.

- **Imessage channel support** (PR #2792, Issue #2791) — documentation fixes for the `add-imessage` skill. Community interest in Apple ecosystem integration remains steady.

## User Feedback Summary

**Pain points surfaced today:**
1. **Setup documentation gaps** — Three separate issues from the same user (specterslient95-lgtm) found that setup guides (setup, init-onecli, migrate-nanoclaw, add-imessage) were incomplete or misleading, with missing `mkdir` steps, undeclared ports, and generic headings. This user filed both issues and fix PRs, showing engaged contributors but frustration with documentation quality.
2. **Managed fleet authentication** (PR #2794) — Fleet deployments broke entirely after v2.1.17 due to credential auth changes. Fixed within a day, but indicates insufficient testing of the immutable-deployment path.
3. **Delivery reliability** — The delivery stall bug (#2796) would silently halt all message delivery, likely causing confusion in production deployments where agents simply stopped responding.

**Satisfaction signals:**
- Rapid response to reported bugs (all issues today received fix PRs)
- Breaking changes in v2.1.17 and v2.1.0 have clear migration notes and env-var opt-outs for managed fleets
- Community contributors are actively submitting fixes rather than just filing complaints

## Backlog Watch

- **PR #2717** (open since 2026-06-09) — [docs: add Atlas Cloud as OpenAI-compatible LLM backend option](https://github.com/nanocoai/nanoclaw/pull/2717)  
  Awaiting maintainer review for 9 days. Low-risk documentation PR that appears stalled.

- **PR #2750** (open since 2026-06-12) — [fix: recover stale outbound.db journals after container kills](https://github.com/nanocoai/nanoclaw/pull/2750)  
  Fixes two related failure modes (#2516, #2640). Open for 6 days without comments — this is a blocking fix for container orchestration stability and should be prioritized.

- **No uncommented Issues or PRs** found that have been open for extended periods without maintainer attention — the project is keeping up well with community submissions.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is your **NullClaw Project Digest** for **2026-06-18**.

---

## NullClaw Project Digest: 2026-06-18

### 1. Today’s Overview
NullClaw is currently experiencing a **low-activity day** with no new releases and no merged pull requests. However, the development cycle shows active community contribution, with **2 open PRs** (both critical fixes) submitted within the last 24 hours. The issue tracker remains stable with **3 open bugs**, none of which were resolved today. The project's health is neutral: maintainers appear to be reviewing community-submitted fixes, but no internal commits or merges occurred today. The lack of closed issues suggests a bottleneck in review capacity.

### 2. Releases
**None.** No new versions were published in the last 24 hours.

### 3. Project Progress
**Merged/Closed PRs today:** **0**
**New PRs (both still open):**
- **[PR #961]** — *feat(memory): configurable auto-recall, recall_limit, max_context_bytes* (Author: valonmulolli | 2026-06-18)  
  This feature adds three configuration keys to control memory recall behavior, including the ability to disable memory enrichment entirely, limit how many memory entries are injected, and cap context byte usage. This is a meaningful performance optimization for users running on resource-constrained hardware or with large context windows.
- **[PR #960]** — *fix(cli): handle arrow keys in agent REPL* (Author: vernonstinebaker | 2026-06-17)  
  Fixes a long-standing CLI usability bug by implementing an allocation-free line editor with raw-mode input, enabling proper arrow key navigation, history, and cursor movement. Directly addresses Issue #865.

### 4. Community Hot Topics
The following issues and PRs are generating the most community attention:

- **[Issue #915]** — *[bug] Problem with scheduler unauthorized* (Updated 2026-06-17, 2 comments)  
  [Link](https://github.com/nullclaw/nullclaw/issues/915)  
  A user running NullClaw with an external Ollama host (RTX 3090, Qwen3.6:27b) reports that the scheduler entirely fails to work in both Telegram and CLI. The underlying need is for better documentation or error handling around LLM authorization and scheduling configuration, especially when models are hosted externally.

- **[Issue #865]** — *CLI shows ctrl characters for up/down/left/right keys* (Updated 2026-06-17, 2 comments)  
  [Link](https://github.com/nullclaw/nullclaw/issues/865)  
  This is a clear usability regression for CLI users. The corresponding fix PR #960 is already submitted and awaiting review—this is the most actionable community discussion today.

- **[Issue #861]** — *How to enable the Web UI on headless VPS server?* (Updated 2026-06-17, 1 comment)  
  [Link](https://github.com/nullclaw/nullclaw/issues/861)  
  A user explicitly expresses confusion over the README documentation for Web UI tunneling. This signals a documentation quality gap for non-expert users.

### 5. Bugs & Stability
**High Severity:**
- **[Issue #915]** — Scheduler unauthorized error on external Ollama models.  
  *Status:* Open, no fix PR. The scheduler is a core feature; this likely blocks Telegram users.

**Medium Severity:**
- **[Issue #865]** — CLI broken arrow key handling.  
  *Status:* Fix PR #960 is pending review. This is a serious UX bug for interactive terminal users.

**Low Severity:**
- **[Issue #861]** — Documentation clarity issue (Web UI setup). Not a software bug, but a support blocker.

### 6. Feature Requests & Roadmap Signals
The following feature requests suggest likely roadmap items:

- **[PR #961]** — Configurable memory recall (auto_recall, recall_limit, max_context_bytes)  
  This is the only active feature-enhancement PR. If merged, it will give advanced users fine-grained control over memory injection, which is critical for managing context windows on smaller models or with high-throughput workloads.

**Prediction:** Expect PR #961 to be merged in the next 1–2 weeks. Memory configurability is a low-risk, high-value enhancement that addresses user complaints about context overflow.

### 7. User Feedback Summary
- **Pain Points:**
  - CLI terminal handling is broken for basic navigation (Issue #865).
  - Scheduler fails silently when using an external Ollama host (Issue #915).
  - Web UI setup documentation is too jargon-heavy for non-experts (Issue #861).
- **Use Cases:**
  - Users are running NullClaw on headless VPS servers with remote LLM backends (Ollama).
  - Users are relying on the scheduler for automated task execution via Telegram/CLI.
- **Satisfaction:** Mixed. While the tool generally works for tool calling, core features like the scheduler and CLI editor are producing frustration. The community is actively contributing fixes, which is a positive signal.

### 8. Backlog Watch
The following items require maintainer attention due to age or lack of response:

- **[Issue #861]** — *How to enable the Web UI on headless VPS server?* (Created 2026-04-22, last updated 2026-06-17)  
  No maintainer response. This issue has been open for nearly two months with only one user comment. A documentation update or a simple step-by-step guide would resolve this.

- **[Issue #865]** — *CLI shows ctrl characters...* (Created 2026-04-23)  
  Even though a fix PR (#960) now exists, this bug has been open for nearly two months. The fix should be prioritized for merge.

**No PRs currently awaiting maintainer response beyond the two already open this week.**

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for **2026-06-18**.

---

## IronClaw Project Digest — 2026-06-18

### 1. Today's Overview

The project is in a high-intensity development cycle, driven by the "Reborn" architecture overhaul. Over the last 24 hours, **49 issues** were updated (26 active) and **50 PRs** were updated (33 open), indicating a very high level of contributor and maintainer engagement. The focus is split between stabilizing the new Reborn WebUI (fixing approval workflows, UI feedback, and automation states) and laying down future infrastructure (the "Projects" entity, Bedrock support, and new agent filesystem viewers). While no new releases were published, the sheer volume of merged PRs (17) suggests the team is in a rapid "fix and ship" mode, addressing both critical bugs (e.g., Slack OAuth security, automation loops) and long-requested features (agent file browser). The presence of multiple stacked PRs from core contributors (serrrfirat, ilblackdragon) points to significant architectural work being gated and merged sequentially.

### 2. Releases

**None.** No new releases were published in the last 24 hours. The last release, `v0.29.1`, was managed via PR #3708 which has now been closed.

### 3. Project Progress (Merged/Closed PRs)

The 17 merged/closed PRs represent significant progress in two major areas:

- **Reborn WebUI Polish & Bug Fixing:**
    - **PR #5035** (closed): A major UX win—tool arguments are now visible **live** while a tool is running, not just after completion. This closes a top feedback item (#4852).
    - **PR #4977** (closed): Fixes the approval-denial flow. Denied tool activities now remain visible and correctly ordered in the UI, resolving a core dogfooding complaint.
    - **PR #4983** (closed): Cleanup of the NEAR AI tool-message flattening compatibility path, simplifying the backend.
    - **PR #5004, #4980, #4988** (closed): Multiple UX fixes for the Automations dashboard, making failure states actionable and improving empty-state guidance.
- **Security & Core Infrastructure:**
    - **PR #5052** (closed): Live Slack OAuth path hardened to match the structural DM-parity of triggered runs (closes #5009). This is a security-focused fix.
    - **PR #5022, #5000** (closed): Key PRs in the "no-progress detection" redesign, adding `ContentDigest` plumbing for output-aware agent progress tracking.
    - **PR #5053** (closed): Fixes OAuth token refresh by removing a per-process cache that was causing expired tokens to be reused.

### 4. Community Hot Topics

The most active discussions revolve around **Reborn usability and architectural gaps**:

- **#4764 (Closed) - Approval Denial Feedback:** This issue (2 comments, reported by sunglow666) highlighted a critical UX failure: denying a shell command left the tool invocation silently pending. The closure of PR #4977 directly addresses this, making the denied state visible and consistent.
- **#5058 (Open) - Bedrock Incompatibility:** Reported 18 hours ago, this issue quickly gained a fix PR (#5059). It reveals a clear user need: running IronClaw with AWS Bedrock as a standalone binary. The problem was a simple feature flag mis-wiring, suggesting this is a common deployment pain point.
- **#5009 (Closed) - Slack OAuth Security:** This issue, raised during a code review, identified a structural security gap in the live Slack OAuth path compared to the triggered path. The swift closure by PR #5052 shows strong security responsiveness.

### 5. Bugs & Stability

The following bugs were reported or updated, ranked by severity:

- **High [Critical]:** **#5058** (Open): AWS Bedrock is unreachable from the standalone Reborn binary, and the Converse tool schema rejects valid combinators. **Fix exists: PR #5059 is open.**
- **High [Regression]:** **#5044** (Open): `NEARAI_MODEL=auto` is rejected by the cloud API with a HTTP 400, causing silent hangs. **Fix exists: PR #5045 is open** to resolve `auto` to a real model.
- **Medium [UI/UX]:** **#5007** (Open): Validation errors in the Skills page do not clear after required fields are filled.
- **Medium [Automation]:** **#5031** (Open): The Slack connect card can be invoked even when already connected, and is English-only.
- **Low [Security/Dependency]:** **#4824** (Open): `cargo-deny` CI is failing repo-wide due to new RUSTSEC advisories against postgres crates. This blocks all PRs until fixed.

### 6. Feature Requests & Roadmap Signals

The following issues signal near-term roadmap priorities:

- **"Reborn Projects" (Stack PRs #5015-#5019):** A massive 5-part stack introducing a first-class `Project` entity with roles, permissions, and a dedicated WebUI page. This is a foundational feature for multi-user collaboration. **Prediction:** These PRs are likely to merge into the next release (v0.30+), drastically changing the user management model.
- **Agent Filesystem Viewer (PR #5057):** A read-only viewer for the agent's memory and project directories. This addresses a long-standing user request for transparency into what the agent "sees."
- **Improved Engineering Productivity (#4878):** This meta-issue is driving the creation of an "Agent Task Service" (#5036). This is a shift towards dogfooding IronClaw as an AI-native engineering tool. **Prediction:** Expect internal CI/CD and code-review automation features to emerge from this initiative.

### 7. User Feedback Summary

The "User Feedback" is largely derived from the QA reports by **sunglow666**, who appears to be a dedicated tester. Pain points are heavily concentrated on the **Reborn WebUI**:

- **Dissatisfaction:** Users (testers) are frustrated by **silent failures**. The "Working" indicator stays on after the agent finishes (#4961), deleting a running conversation gives no feedback (#4823), and automation tool denials leave things hanging (#4986).
- **Dissatisfaction (Onboarding):** First-run onboarding blocks access to Extensions and Automations (#4793). New users are left confused about how to create automations (#4980).
- **Satisfaction:** The quick turnaround on issues like the denial feedback (#4977) and live tool arguments (#5035) suggests that the development team is highly responsive to tester feedback, which is a strong positive signal for project health.

### 8. Backlog Watch

The following items remain open or unresolved and may need maintainer attention:

- **#3729 (Open - since May 17):** **Failed `tool_install` calls are shown as successful after a page refresh.** This is a long-standing bug reporting stale UI state that misleads users. It has 1 comment but no assignee or active fix PR.
- **#4191 (Open - since May 28):** **WeCom Channel Validation Findings.** A deep validation report for the v0.29.0 WeChat Work (WeCom) integration has gone unanswered for three weeks, with 0 comments. While these are staging findings, the lack of follow-up could signal a deprioritization of this channel.
- **#4824 (Open - since June 12):** **`cargo-deny` CI failure.** This is a blocker for every new PR. While acknowledged, an open issue with no assigned fix for nearly a week is concerning for project stability.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-06-18**.

---

## LobsterAI Project Digest — 2026-06-18

### 1. Today's Overview
The project is in a **high-velocity stabilization and polish phase**, with 13 pull requests merged in the last 24 hours and zero open issues. A new release (2026.6.15) was published, delivering significant new features including Computer Use integration and real-time ASR voice input for the Cowork mode. The merge cluster is dominated by **fixes and refinements** to the Cowork session experience, particularly around streaming behavior, UI jank, and model selection. The activity level is **high**, with a clear focus on quality-of-life improvements and bug squashing rather than speculative new feature work.

### 2. Releases
**New Release: [LobsterAI 2026.6.15](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.15)**
- **What’s Changed:**
  - **Feature:** Added "Computer Use" capability (likely a remote desktop or screen control task agent mode).
  - **Feature:** Realtime ASR voice input for Cowork sessions.
  - **Improvement:** Post-compaction context continuity improvements for the Cowork agent (detailed in PR #2145).
- **Breaking Changes:** None indicated in the changelog.
- **Migration Notes:** No specific migration steps were published. Users should update via standard package channels.

### 3. Project Progress
*All 13 PRs merged today were closed (13/13 merged).* The work can be grouped into three themes:

- **Cowork Agent & UI Stability (9 PRs):**
  - **[#2174](https://github.com/netease-youdao/LobsterAI/pull/2174):** Fixed scroll-to-bottom positioning to align with the latest message height.
  - **[#2173](https://github.com/netease-youdao/LobsterAI/pull/2173):** User messages now render as plain text preserving line breaks.
  - **[#2171](https://github.com/netease-youdao/LobsterAI/pull/2171):** Reduced rail navigation jank in long sessions (disables smooth scrolling for long jumps).
  - **[#2162](https://github.com/netease-youdao/LobsterAI/pull/2162):** Preserved voice input cancel guard after a merge conflict resolution.
  - **[#2153](https://github.com/netease-youdao/LobsterAI/pull/2153):** Fixed model selection for same-name packaged vs. custom models.
  - **[#2154](https://github.com/netease-youdao/LobsterAI/pull/2154):** Show model metadata after manually stopping a stream.
  - **[#2147](https://github.com/netease-youdao/LobsterAI/pull/2147):** Prevented stopped startup turns from sending a chat.
  - **[#2145](https://github.com/netease-youdao/LobsterAI/pull/2145):** Improved post-compaction context continuity (core feature of the 2026.6.15 release).
  - **[#2149](https://github.com/netease-youdao/LobsterAI/pull/2149):** Raised OpenClaw gateway heap limit to prevent OOM crashes.

- **Infrastructure & Portal (2 PRs):**
  - **[#2144](https://github.com/netease-youdao/LobsterAI/pull/2144):** Updated portal fallback URLs to new domains.
  - **[#2172](https://github.com/netease-youdao/LobsterAI/pull/2172):** Added support for restoring HTML shares closed due to quota limits.

- **Docs & Chores (2 PRs):**
  - **[#2175](https://github.com/netease-youdao/LobsterAI/pull/2175):** Optimized the README.
  - **[#1463](https://github.com/netease-youdao/LobsterAI/pull/1463):** Fixed long modal titles (truncation + tooltip).

### 4. Community Hot Topics
No issues or PRs in the last 24 hours received notable comments or reactions. The discussion weight is concentrated in the **PR review process for Cowork fixes**, which are being handled rapidly internally. The absence of open community issues suggests the team is preemptively squashing bugs before they reach a wide user base.

### 5. Bugs & Stability
No new bugs were reported today. However, the PRs merged indicate proactive fixes for several critical stability issues:

- **High Severity:** **[PR #2149](https://github.com/netease-youdao/LobsterAI/pull/2149)** — Fixed OOM crashes in the OpenClaw gateway under long-running multi-channel workloads (heap limit raised).
- **High Severity:** **[PR #2147](https://github.com/netease-youdao/LobsterAI/pull/2147)** — Fixed a race condition where stopping a startup turn could result in an unwanted chat message being sent.
- **Medium Severity:** **[PR #2154](https://github.com/netease-youdao/LobsterAI/pull/2154)** — Fixed missing model metadata display after a user stops a streaming response.
- **Medium Severity:** **[PR #2171](https://github.com/netease-youdao/LobsterAI/pull/2171)** — Addressed UI jank and performance issues in very long sessions.

### 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. The roadmap signal is **strongly defined by the 2026.6.15 release**:
- **Computer Use:** Suggests future expansion into agent-driven desktop interaction.
- **Realtime ASR:** Indicates a move toward multimodal, low-latency voice interaction in the Cowork agent.

The next minor version (e.g., 2026.6.18) will likely focus on baking the stability fixes merged today into the released branch.

### 7. User Feedback Summary
No explicit user feedback via GitHub issues was recorded in the last 24 hours. However, the nature of the merged PRs implies implicit user pain points:
- **Pain Point:** Long sessions were becoming sluggish and visually janky (PR #2171, #2174).
- **Pain Point:** Stopping a streaming agent response was confusing (no metadata shown) or could cause unintended side effects (PR #2154, #2147).
- **Pain Point:** Multi-window/session management of voice input was fragile (PR #2162).

The team is responding to these issues with immediate fixes.

### 8. Backlog Watch
- **[PR #1463](https://github.com/netease-youdao/LobsterAI/pull/1463) (stale):** A fix for long modal titles was created on 2026-04-04 and **merged today** (2026-06-17), ending a 74-day stale period. This was the only long-latency item in the backlog.
- **Status:** The backlog is currently clean. No open issues or lingering PRs require maintainer attention.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for **2026-06-18**.

---

## Moltis Project Digest: 2026-06-18

**Overall Status:** Stable, low activity. The project is in a "maintenance and refinement" phase with no new releases. Focus is on addressing specific user-experience (UX) requests regarding output handling (TTS format, Markdown export) and infrastructure configuration (RPC timeouts).

### 1. Today's Overview
The Moltis project exhibited low activity over the past 24 hours, reflecting a stable development cycle with no new releases. Two enhancement issues remain open, indicating a community focus on improving output flexibility rather than fixing critical bugs. A single open pull request addressing a core infrastructure setting (WebUI RPC timeout) was updated, suggesting active work on configuration improvements. Overall, the project appears to be in a "quality of life" improvement phase, with maintainers responding to specific user requests.

### 2. Releases
No new releases were published in the last 24 hours. The project remains on its current stable track.

### 3. Project Progress
- **Open Pull Requests (1):**
    - **#1130 (feat: make webui rpc timeout configurable):** Authored by *khimaros*. This PR directly addresses a prior issue (#1127) by allowing users to configure the RPC timeout setting for the WebUI. This is a critical fix for users experiencing timeouts during long operations. *Note: This PR is open and has not been merged as of this digest.*

### 4. Community Hot Topics
The following issues are driving current discussion:

- **Issue #1126: Allow to configure the format of tts output**
    - **Link:** [Issue #1126](https://github.com/moltis-org/moltis/issues/1126)
    - **Analysis:** With 3 comments, this is the most discussed item. Users are seeking control over the specific output format of Text-to-Speech (TTS), likely indicating a desire for interoperability with different audio pipelines or file size constraints. The need for "format configuration" suggests the current implementation is rigid.

- **Issue #1131: Add copy + export as Markdown**
    - **Link:** [Issue #1131](https://github.com/moltis-org/moltis/issues/1131)
    - **Analysis:** This request for Markdown export points to a user workflow where Moltis outputs are shared in documentation, code review, or conversation logs. The lack of comments suggests this is a straightforward "nice-to-have" feature rather than a contentious debate.

### 5. Bugs & Stability
**No high-severity bugs or regressions** were reported in the last 24 hours. The only active technical fix is the open PR (#1130) related to a network timeout issue, which is a configuration enhancement rather than a crash.

### 6. Feature Requests & Roadmap Signals
- **High Likelihood (Next Release):**
    - **Configurable RPC Timeout (PR #1130):** This PR is already open and authored by a regular contributor. It is likely to be merged soon, as it fixes a clear infrastructure pain point.
    - **TTS Output Format (Issue #1126):** Given the moderate discussion and the project’s apparent focus on configurability, this is a strong candidate for the next minor release.
- **Medium Likelihood:**
    - **Markdown Export (Issue #1131):** A low-effort, high-utility feature. It may be bundled with a future release if a contributor picks it up.

### 7. User Feedback Summary
**Pain Points:**
- Users are encountering **lock-in** due to a fixed TTS output format, limiting integration with external tools.
- Users require the ability to **export conversation/data** in a standard, re-usable format (Markdown), indicating a workflow dependency on the project.
- The **WebUI RPC timeout** is a clear friction point for users performing long tasks, causing interruptions.

**Satisfaction:** No strong negative sentiment was detected. The requests are specific and constructive, suggesting users are actively invested in the project’s direction.

### 8. Backlog Watch
- **Issue #1127 (Implied by PR #1130):** While not in the "updated in 24h" list, this issue is the driver behind the current PR. It has likely been waiting for a fix and is now being addressed by PR #1130. Maintainers should ensure this linked issue is closed upon merge.
- **Actions for Maintainers:** Review PR #1130 for merge readiness. Acknowledging Issues #1126 and #1131 with a "triaged" label would improve community morale and signal prioritization.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-18

## Today's Overview

CoPaw is in a period of **high activity and rapid iteration**, with **47 issues** and **50 pull requests** updated in the last 24 hours — indicating strong community engagement and active development. The project shipped **two releases** today (`v1.1.12` and `v1.1.12-beta.2`), one of which is a major version bump to `2.0.0a1` for the AgentScope 2.0 migration, marking a significant architectural milestone. Maintenance velocity is high (32 merged/closed PRs vs. 18 open), but the issue tracker reveals **troubling stability concerns** — particularly around context compaction causing process freezes, and a critical security vulnerability (RCE via prompt injection) in cloud deployments. The **XiaoYi (Huawei Xiaoyi) channel** continues to be a persistent pain point, with multiple issues spanning protocol, connectivity, and routing problems.

---

## Releases

### v1.1.12 (Stable) — [Release Notes](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.12)
- **Console**: Models page overhaul — Provider aggregation, unified card UI, and layout redesign ([#5203](https://github.com/agentscope-ai/QwenPaw/pull/5203))
- **Console**: Simple mode with flat navigation and sorted session list by updated time ([#5222](https://github.com/agentscope-ai/QwenPaw/issues/5222) — PR reference to be confirmed)
- **Chore**: Version bump from `1.1.12b2` to `1.1.12`

### v1.1.12-beta.2 — [Release Notes](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.12-beta.2)
- **Performance**: Removed unnecessary deep copy operations in agent config ([#5240](https://github.com/agentscope-ai/QwenPaw/pull/5240))
- **Feature**: Console — add session filter by title ([#5178](https://github.com/agentscope-ai/QwenPaw/pull/5178))

### v2.0.0a1 (Alpha) — [PR #5281](https://github.com/agentscope-ai/QwenPaw/pull/5281)
- **Breaking Change**: Backend migration from AgentScope 1.x to AgentScope 2.0 — no migration guide yet provided; use at your own risk
- Version bumped from `1.1.10b1` to `2.0.0a1`

**Migration Note**: Users on `v1.1.11.post2` attempting in-place upgrade via `install.sh` may encounter a **script bug** (`PRERELEASE_ARGS[@]: unbound variable`) — see [Issue #5286](https://github.com/agentscope-ai/QwenPaw/issues/5286). A fix has been released as `v1.1.12.post1` via [PR #5288](https://github.com/agentscope-ai/QwenPaw/pull/5288).

---

## Project Progress

### Merged/Closed PRs Today (32 total)

**Core Stability & Bug Fixes**
- **Desktop plugin dependency crash fix** ([#5260](https://github.com/agentscope-ai/QwenPaw/pull/5260)) — Prevents Tauri desktop crash loops when third-party plugins require pip dependencies; routes frozen backend to correct pip binary
- **XiaoYi channel full refactor** ([#5274](https://github.com/agentscope-ai/QwenPaw/pull/5274)) — Dual WebSocket architecture (primary domain + backup IP), aligned with official `@ynhcj/xiaoyi-channel` plugin protocol
- **Backup resilience** ([#5041](https://github.com/agentscope-ai/QwenPaw/pull/5041)) — `add_agent_workspaces()` no longer fails the entire backup when a single file is unreadable (Windows-specific)
- **Session file path deduplication** ([#5026](https://github.com/agentscope-ai/QwenPaw/pull/5026)) — Fixes `submit_to_agent` failures where `{session_id}_{session_id}.json` was generated instead of `{user_id}_{session_id}.json`

**Features & Enhancements**
- **Desktop port configuration** ([#5272](https://github.com/agentscope-ai/QwenPaw/pull/5272)) — Users can now set a fixed backend port via environment variable
- **OpenClaw config migration CLI** ([#5276](https://github.com/agentscope-ai/QwenPaw/pull/5276)) — New `qwenpaw migrate openclaw` auto-detects `~/.openclaw` and imports agent configs

**Documentation**
- **Roadmap update** ([#5277](https://github.com/agentscope-ai/QwenPaw/pull/5277)) — Updated project roadmap

---

## Community Hot Topics

### Most Active Discussions

1. **[Issue #1911](https://github.com/agentscope-ai/QwenPaw/issues/1911) — XiaoYi channel: replies never delivered** (22 comments, **closed**)
   - *Analysis:* User reports that after adding the XiaoYi channel, messages are received by CoPaw but replies never appear in the Huawei XiaoYi client. This is the community's longest-running unresolved channel integration issue, and it has now been closed — likely resolved by today's dual-WebSocket refactor ([PR #5274](https://github.com/agentscope-ai/QwenPaw/pull/5274)).

2. **[Issue #5218](https://github.com/agentscope-ai/QwenPaw/issues/5218) — Sub-agent context compaction freezes QwenPaw process** (16 comments, **open**)
   - *Analysis:* **Critical stability bug** — when a sub-agent triggers context compaction, the entire process becomes unresponsive. Only manual restart recovers it. A fix PR ([#5287](https://github.com/agentscope-ai/QwenPaw/pull/5287)) has been opened by a first-time contributor to prevent crash when summary exceeds schema `maxLength`, but the freeze scenario may be separate.

3. **[Issue #5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) — Agent-created cron jobs fail to trigger** (12 comments, **open**)
   - *Analysis:* Agent-generated scheduled tasks display correctly but never execute. Users cannot manually edit these jobs. A related PR ([#5241](https://github.com/agentscope-ai/QwenPaw/pull/5241)) increases the default `misfire_grace_seconds` from 60 to 3600, which may mitigate the issue but doesn't fix the root cause.

4. **[Issue #4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) — AgentScope 2.0 migration** (11 comments, **open**, 2 👍)
   - *Analysis:* The community is actively discussing the breaking migration from AgentScope 1.x to 2.0. The alpha release (`v2.0.0a1`) was merged today. No migration guide yet — expect community concern about compatibility.

5. **[Issue #4808](https://github.com/agentscope-ai/QwenPaw/issues/4808) — Skill not found: `person_stat_skill`** (7 comments, **closed**)
   - *Analysis:* User's custom skill (`SKILL.md`) fails with "Agent not exists" error despite correct configuration. Likely a path/registration issue.

---

## Bugs & Stability

### High Severity

1. **🔴 Context compaction causes process freeze** ([#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218))
   - *Impact:* Sub-agent triggers compaction → entire QwenPaw process freezes → only manual restart recovers. **Fix PR** ([#5287](https://github.com/agentscope-ai/QwenPaw/pull/5287)) prevents crash on summary overflow, but freeze root cause may remain.

2. **🔴 Desktop (Tauri) crash loop on macOS ARM64** ([#5209](https://github.com/agentscope-ai/QwenPaw/issues/5209))
   - *Impact:* `qwenpaw-backend` crashes every ~1 minute with `EXC_BAD_ACCESS (SIGSEGV)` — desktop version unusable. **Fix PR** ([#5260](https://github.com/agentscope-ai/QwenPaw/pull/5260)) addresses plugin pip dependency installation in Tauri sidecar, which may resolve this.

3. **🔴 File download broken for non-text files** ([#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140))
   - *Impact:* `docx`, `pdf` downloads return HTTP 404; only plain-text works. Regression from `v1.1.11`. No fix PR identified yet.

4. **🔴 Execution deadlock/dead loop** ([#4967](https://github.com/agentscope-ai/QwenPaw/issues/4967), [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162))
   - *Impact:* Multiple users report conversation processing entering infinite loops with no recovery — requires manual restart.

### Medium Severity

5. **🟡 ChromaDB probe collection name fails** ([#5284](https://github.com/agentscope-ai/QwenPaw/issues/5284))
   - *Impact:* `_probe` collection name starts with underscore, violating ChromaDB naming rules → runtime probe always returns `False` → system falsely downgrades to local backend. **Fix PR** ([#5289](https://github.com/agentscope-ai/QwenPaw/pull/5289)) renames to `probe-test`.

6. **🟡 Windows vector index not persisted** ([#5259](https://github.com/agentscope-ai/QwenPaw/issues/5259))
   - *Impact:* `memory_search` returns empty after restart unless "Rebuild memory index on startup" is enabled. Windows-specific.

7. **🟡 MCP/ACP config not persisted to `agent.json`** ([#5266](https://github.com/agentscope-ai/QwenPaw/issues/5266))
   - *Impact:* API returns `201 Created` but GET returns empty list — configs silently lost.

### Low Severity

8. **🟢 Assistant message count mismatch** ([#5208](https://github.com/agentscope-ai/QwenPaw/issues/5208))
   - *Impact:* `reasoning` block type vs. `thinking` type causes warnings but no functional breakage.

9. **🟢 Install script `PRERELEASE_ARGS[@]` bug** ([#5286](https://github.com/agentscope-ai/QwenPaw/issues/5286))
   - *Impact:* `install.sh` upgrade fails with unbound variable error on macOS. **Fixed in** [PR #5288](https://github.com/agentscope-ai/QwenPaw/pull/5288).

### Critical Security Issue

10. **🔴 Prompt injection → full RCE in cloud deployment** ([#5234](https://github.com/agentscope-ai/QwenPaw/issues/5234), 2 comments)
    - *Impact:* Attackers can use crafted prompts to install monitoring probes (`komari-agent`) with shell access, potentially leading to container escape. **No fix PR identified yet.** This is a design-level concern for cloud deployments.

---

## Feature Requests & Roadmap Signals

### Likely to land in next release

| Request | Issue | Likelihood |
|---------|-------|------------|
| **Customizable column order in sessions page** | [#4770](https://github.com/agentscope-ai/QwenPaw/issues/4770) | **High** — PR [#4975](https://github.com/agentscope-ai/QwenPaw/pull/4975) already under review |
| **Agent avatar upload & display** | — | **High** — PR [#5263](https://github.com/agentscope-ai/QwenPaw/pull/5263) merged today |
| **Cron job update CLI** (`qwenpaw cron update`) | [#4939](https://github.com/agentscope-ai/QwenPaw/issues/4939) | **High** — PR [#5210](https://github.com/agentscope-ai/QwenPaw/pull/5210) open and under review |

### Under discussion / needs maintainer attention

| Request | Issue | Notes |
|---------|-------|-------|
| **AgentScope tracing integration** | [#4057](https://github.com/agentscope-ai/QwenPaw/issues/4057) | User wants `agentscope.init(tracing_url=...)` for Arize Phoenix monitoring. Needs maintainer input on architecture |
| **UI font scaling & file path hyperlinks** | [#4077](https://github.com/agentscope-ai/QwenPaw/issues/4077) | QoL enhancement for desktop UI |
| **Built-in skill persistence across upgrades** | [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) | Users must manually disable unwanted skills after every update — frustrating UX |

### Roadmap Signals

- **AgentScope 2.0 Migration** ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)): The `v2.0.0a1` alpha release is out. This is a **breaking change** — expect API incompatibilities. Community needs a migration guide.
- **OpenClaw migration** ([PR #5276](https://github.com/agentscope-ai/QwenPaw/pull/5276)): Indicates strategic intent to absorb users from competing AI agent platforms.

---

## User Feedback Summary

### Pain Points

| Theme | Evidence |
|-------|----------|
| **Context compaction is unreliable** | Multiple issues ([#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218), [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171)) report freezes, information loss, and task interruption |
| **File download broken** | [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) — regression in `v1.1.11`; non-text files return 404 |
| **XiaoYi channel unreliable** | [#1911](https://github.com/agentscope-ai/QwenPaw/issues/1911) (closed), [#3840](https://github.com/agentscope-ai/QwenPaw/issues/3840) — persistent protocol/connectivity issues |
| **Cron jobs not triggering** | [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) — agent-created scheduled tasks fail silently |
| **Desktop stability on macOS** | [#5209](https://github.com/agentscope-ai/QwenPaw/issues/5209) — crash loops make desktop version unusable on ARM Macs |
| **Windows memory_index not persisted** | [#5259](https://github.com/agentscope-ai/QwenPaw/issues/5259) — requires rebuild on every restart |

### Satisfaction Signals

- **Community contributors are active** — many first-time-contributor PRs today ([#5287](https://github.com/agentscope-ai/QwenPaw/pull/5287), [#5241](https://github.com/agentscope-ai/QwenPaw/pull/5241), [#5242](https://github.com/agentscope-ai/QwenPaw/pull/5242), [#5210](https://github.com/agentscope-ai/QwenPaw/pull/5210))
- **Positive reactivity** — most user-reported bugs get quick response; today alone 23 issues were closed
- **XiaoYi channel fix may resolve year-old pain point** — [#1911](https://github.com/agentscope-ai/QwenPaw/issues/1911) closed after 3 months

### Dissatisfaction Signals

- **Upgrade process is fragile** — [#5286](https://github.com/agentscope-ai/QwenPaw/issues/5286) shows `install.sh` can fail; [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) shows user configuration is lost on upgrade
- **AI agent loop/freeze issues unresolved** — [#4967](https://github.com/agentscope-ai/QwenPaw/issues/4967), [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) remain open with no clear root cause
- **Cloud security concern** — [#5234](https://github.com/agentscope-ai/QwenPaw/issues/5234) reveals potential RCE via prompt injection, which could erode trust in cloud deployments

---

## Backlog Watch

| Issue/PR | Age | Priority | Reason for Attention |
|----------|-----|----------|---------------------|
| [#5075](https://github.com/agentscope-ai/QwenPaw/issues/5075) "Add agent sharing via QR code" | 9 days | Medium | No maintainer comment, user showing frustration |
| [#4077](https://github.com/agentscope-ai/QwenPaw/issues/4077) "UI Font Scaling & File Link Support" | 43 days | Low | No maintainer response — user requested QoL feature |
| [#4057](https://github.com/agentscope-ai/QwenPaw/issues/4057) "AgentScope tracing initialization" | 43 days | Low-Medium | User needs tracing for production monitoring; no guidance on workaround |
| [#3804](https://github.com/agentscope-ai/QwenPaw/issues/3804) "Add support for custom model providers via API key only" | 53 days | Medium | Multiple users asking; no maintainer engagement |

### Critical Attention Needed

- **[#5234](https://github.com/agentscope-ai/QwenPaw/issues/5234) — Prompt injection leads to RCE in cloud**: No maintainer response yet. This is a **security vulnerability** that could have serious consequences for hosted deployments. Immediate triage and a security advisory are warranted.
- **[#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) — AgentScope 2.0 migration**: The alpha is out, but users need a clear migration guide, compatibility matrix, and rollback plan. Without it, early adopters risk breaking their setups.

---

**Overall Assessment**: CoPaw is shipping fast and has a vibrant contributor community, but **stability and reliability are the top concerns** — particularly around context compaction, desktop crashes, and scheduled task execution. The security implication in cloud deployments needs urgent attention. The project's strategic move to AgentScope 2.0 is a major milestone, but communication about migration paths must improve.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for June 18, 2026.

---

## ZeroClaw Project Digest: 2026-06-18

### 1. Today's Overview

ZeroClaw is in a period of **very high development velocity**, with 50 issues and 50 PRs updated in the last 24 hours, indicating a highly active and engaged team. The focus is split between hardening existing features (fixing regression bugs, improving Windows support, and securing the build pipeline) and building out the next major release’s architecture (agent renaming, WASM plugins, skills platform). A significant CI and security hardening push is evident, with multiple RFCs for supply-chain scanning, context compression, and desktop computer-use entering the discussion phase.

### 2. Releases

**No new releases** were published in the last 24 hours, though the high volume of PRs and RFCs suggests a stabilization push toward an upcoming v0.8.x or v0.9.0 milestone.

### 3. Project Progress (Merged/Closed PRs)

12 PRs were merged or closed today, including several from a stacked feature series:

- **Agent & Config Management:** A large 8-PR stack was merged, implementing a typed delete-with-cascade system and agent alias rename functionality. Key PRs in this series include:
    - `[CLOSED]` [#7842](https://zeroclaw-labs/zeroclaw/pull/7842) (feat(cli): agents/providers/channels CRUD + skill-bundle cascade)
    - `[CLOSED]` [#7841](https://zeroclaw-labs/zeroclaw/pull/7841) (feat(gateway): agent owned-state rename cascade)
    - `[CLOSED]` [#7840](https://zeroclaw-labs/zeroclaw/pull/7840) (feat(config): rename_with_cascade for aliased entries)
- **Stability & User Experience:** Several small fixes were merged to improve error messages and fix UI bugs.
    - `[CLOSED]` [#7684](https://zeroclaw-labs/zeroclaw/pull/7684) (fix(acp): surface history-pruner and turn-cancel as visible events)
    - `[CLOSED]` [#7856](https://zeroclaw-labs/zeroclaw/pull/7856) (fix(cli): add confirmation feedback after secret prompt input)
- **Bug Fixes:** A critical S1 regression was resolved.
    - `[CLOSED]` [#7563](https://zeroclaw-labs/zeroclaw/pull/7563) ([Bug]: canvas-store regression in WS chat/ACP sessions)

### 4. Community Hot Topics

The most active discussions centered on architectural enhancements and security hardening:

- **Desktop Computer-Use (Issue #6909):** The most-commented issue proposes adding screen capture and mouse/keyboard control, enabling ZeroClaw to operate as a true desktop agent. This suggests a desire to compete with the "computer-use" features of other major agents.
- **Context Compression (Issue #7673):** A proposal for a `CompressionDecorator` to compress LLM request payloads. The underlying need is managing the cost and latency of large context windows, a critical scaling concern for long-running agent sessions.
- **Supply-Chain Security (Issue #7675):** An RFC for a hardened CI pipeline with SBOM generation and provenance tracking. This indicates a proactive, enterprise-focused approach to security, going beyond just fixing runtime bugs.
- **Cron & Context Bugs (Issues #6954, #6105, #6055):** Active discussions about how scheduled tasks and Slack interactions handle agent context, revealing pain points where the agent’s memory of its own actions is lost or incomplete.

### 5. Bugs & Stability

Several S1 (workflow blocked) and S2 (degraded behavior) bugs were filed or updated today.

- **`[Bug]: agent rename can move owned state before config persistence`** ([Issue #7907](https://zeroclaw-labs/zeroclaw/issues/7907)) — **S1:** A race condition in the newly merged rename cascade function. A fix is likely being prepared. **No fix PR identified.**
- **`[Bug]: 74 test failures on Windows`** ([Issue #7462](https://zeroclaw-labs/zeroclaw/issues/7462)) — **S2:** A major cross-platform stability regression, highlighting a blind spot in CI. The team is actively addressing this with a new tracking issue for test coverage ([#7910](https://zeroclaw-labs/zeroclaw/issues/7910)) and a fix PR for the Windows self-update ([#7853](https://zeroclaw-labs/zeroclaw/pull/7853)).
- **`[Bug]: canvas-store regression in WS chat/ACP sessions`** ([Issue #7563](https://zeroclaw-labs/zeroclaw/issues/7563)) — **S1 (Resolved):** A critical regression was linked to a recent PR and has since been closed, indicating a rapid fix.
- **`[Bug]: Agent doesn't have context of the cron job it's run`** ([Issue #6105](https://zeroclaw-labs/zeroclaw/issues/6105)) — **S2 (Blocked):** This older, high-priority bug about cron context is now blocked, awaiting the architectural changes proposed in RFC #6954.
- **`[Bug]: channels/approval attribution without a global side channel`** ([Issue #7737](https://zeroclaw-labs/zeroclaw/issues/7737)) — **S2:** A concurrency bug where approvals can overwrite each other. Likely to be a focus for the v0.9.0 security milestone.

### 6. Feature Requests & Roadmap Signals

User requests and RFCs point toward a major focus on **agent autonomy and extensibility** for the next versions (v0.8.2 and v0.9.0).

- **Likely for v0.8.2 (Skills & WASM):**
    - **WASM Plugin Lifecycle Hooks** ([#7822](https://zeroclaw-labs/zeroclaw/issues/7822)): Allow plugins to react to agent lifecycle events, making the plugin system more powerful.
    - **llama.cpp Model Router** ([#7539](https://zeroclaw-labs/zeroclaw/issues/7539)): A highly requested feature for users running local models, enabling quick model switching.
    - **Date-Range Conditional Cron Schedules** ([#7887](https://zeroclaw-labs/zeroclaw/issues/7887)): A niche but powerful request for advanced job scheduling.
    - **RunPod/ComfyUI Image Gen Provider** ([#7875](https://zeroclaw-labs/zeroclaw/issues/7875)): Expanding the creative capabilities of the agent with a new backend.

- **Predicted for v0.9.0 (Auth & Security):**
    - **Zero-Downtime Config Reloads** ([#7897](https://zeroclaw-labs/zeroclaw/issues/7897)): A high-value feature for production deployments requiring no service interruption.
    - **Hardened CI Pipeline** ([#7675](https://zeroclaw-labs/zeroclaw/issues/7675)): An indicator of maturity and a stepping stone for enterprise adoption.
    - **Native Context Compression** ([#7673](https://zeroclaw-labs/zeroclaw/issues/7673)): A critical performance and cost optimization feature.

- **Further Out:**
    - **Desktop Computer-Use** ([#6909](https://zeroclaw-labs/zeroclaw/issues/6909)): A game-changing feature that would move ZeroClaw into a new category of agent capability.

### 7. User Feedback Summary

- **Pain Points:**
    - **Windows Support:** Multiple issues (confirmation of Windows update fix via [#7853](https://zeroclaw-labs/zeroclaw/pull/7853), 74 test failures in [#7462](https://zeroclaw-labs/zeroclaw/issues/7462)) show Windows users are a significant but underserved segment.
    - **Context & Memory Lapses:** Users report frustration when the agent “forgets” its own cron-triggered messages ([#6105](https://zeroclaw-labs/zeroclaw/issues/6105)) or lacks thread history in Slack ([#6055](https://zeroclaw-labs/zeroclaw/issues/6055)).
    - **Local Model Usability:** A request for a model router for `llamacpp` ([#7539](https://zeroclaw-labs/zeroclaw/issues/7539)) implies that switching between local models is currently cumbersome.
- **Desires:**
    - **Autonomous Desktop Control:** The most popular issue ([#6909](https://zeroclaw-labs/zeroclaw/issues/6909)) is a strong signal users want ZeroClaw to act as their digital assistant, not just a chat bot.
    - **Cost Visibility:** Users want to know when a cheaper/faster model was used due to fallback ([#7883](https://zeroclaw-labs/zeroclaw/issues/7883)), indicating a desire for fine-grained control over operational cost.
    - **Better Onboarding:** The issue to validate `config.toml` at startup ([#6416](https://zeroclaw-labs/zeroclaw/issues/6416)) suggests that initial configuration is a common stumbling block for new users.

### 8. Backlog Watch

- **`[Bug]: Agent doesn't have context of the cron job it's run`** ([Issue #6105](https://zeroclaw-labs/zeroclaw/issues/6105)) (Created: 2026-04-25): This high-priority cron bug has been **blocked for over a month**, awaiting the routing architecture changes from RFC #6954. This is a significant user-facing issue for anyone using scheduled tasks.
- **`feat(channel/mattermost): add optional WebSocket listener mode`** ([PR #7098](https://zeroclaw-labs/zeroclaw/pull/7098)) (Created: 2026-06-02): This PR has been open for over two weeks with a `needs-author-action` label. If the author does not respond, this valuable feature for Mattermost users could stall.
- **`[Bug]: 74 test failures on Windows`** ([Issue #7462](https://zeroclaw-labs/zeroclaw/issues/7462)) (Created: 2026-06-10): While progress is being made (new tracking issue #7910, fix PR #7853), the sheer scope of 74 failures means this will remain a critical concern for Windows users until a comprehensive solution is merged.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*