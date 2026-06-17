# OpenClaw Ecosystem Digest 2026-06-17

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-17 02:29 UTC

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

Based on the provided GitHub data snapshot for OpenClaw, here is the project digest for June 17, 2026.

---

### OpenClaw Project Digest: 2026-06-17

#### 1. Today's Overview

OpenClaw is in a high-intensity development and maintenance phase, with a staggering **500 issues** and **500 pull requests** updated in the last 24 hours. This indicates a massive community and development effort, but also a significant volume of incoming problems. The project is currently dealing with a critical class of bugs related to **session state corruption, message loss, and race conditions**, particularly for users on messaging platforms like Telegram and Discord. While a new release is out (v2026.6.8), the core stability is being challenged by a high volume of regressions and concurrency bugs that suggest the system is struggling under its own complexity.

#### 2. Releases

**New Version:** `v2026.6.8`
- **Key Changes:** This minor release focuses on improving the reliability and formatting of channel delivery.
    - **Telegram:** Richer text rendering is now supported, including tables, lists, blockquotes, and intentional line breaks. Replies also support CLI-backed actions.
    - **WhatsApp:** Now correctly honors configured ACP bindings (Automatic Chat Persistence).
- **Migration Notes:** No breaking changes or explicit migration steps were mentioned. This appears to be a standard patch release.

#### 3. Project Progress

In the last 24 hours, **117 PRs** were merged or closed, indicating active churn and fix deployment. Key areas of advancement include:
- **Filesystem Security:** A major PR (#60981) on Filesystem Access Control (PathGuard) is open and ready for review, aiming to dramatically tighten security for agent file tools.
- **Channel Stability:** Significant PRs are in the pipeline to fix message delivery races and data loss during gateway restarts (e.g., PR #46303 to drain buffers before restart, PR #92712 to clear stale "busy" session states).
- **Cross-Platform Support:** The long-standing request for a native Linux app (#75) has a PR (#59859) in progress. Another PR (#68936) attempts to add a full CI/CD autofix pipeline and a Windows daemon.
- **Configuration Streamlining:** A large PR (#93265) aims to simplify the initial onboarding experience using agent-assisted configuration.

#### 4. Community Hot Topics

The most active discussions reveal deep user frustration with the core chat agent's reliability and transparency.

- **Issue #75 - Cross-Platform Desktop Apps ([Link](openclaw/openclaw Issue #75)):** *109 comments, 79 👍*
    - **Analysis:** This is the most popular and active issue. The core need is parity. Users on Windows and Linux feel like second-class citizens compared to macOS users. The frustration is not just about missing features, but about the lack of a first-class, stable desktop experience for managing and interacting with their agents.

- **Issue #88838 - Session/Transcript Migration ([Link](openclaw/openclaw Issue #88838)):** *30 comments*
    - **Analysis:** This is a highly technical "maintainer" issue. The proposal to break the massive SQLite migration into smaller, reviewable PRs indicates that the current state of session management is fragile, and a large rewrite is seen as a high-risk endeavor that requires careful piece-by-piece integration.

- **Issue #44925 - Silent Subagent Failure ([Link](openclaw/openclaw Issue #44925)):** *19 comments*
    - **Analysis:** Users are deeply frustrated by a "silent failure" mode. Their agents (subagents) are completing tasks, but the results are being thrown away due to timeouts or race conditions, without any error message to the user. This "ghost work" problem undermines trust in the system's ability to perform multi-step tasks.

- **Issue #68596 - Configurable Streaming Watchdog ([Link](openclaw/openclaw Issue #68596)):** *14 comments, 8 👍*
    - **Analysis:** Users of advanced reasoning models (like DeepSeek-R1) hit a hardcoded 30-second watchdog timer, causing sessions to be reset even though the model is simply "thinking." This shows a mismatch between the project's infrastructure and the capabilities of newer, more powerful models.

#### 5. Bugs & Stability

The stability of the core agent experience is heavily compromised by a set of deep, interconnected bugs.

- **Critical (P0):**
    - **#88838 P0 - Session/Transcript SQLite Migration ([Link](openclaw/openclaw Issue #88838)):** The core data storage mechanism is seen as a critical risk, requiring careful surgery.

- **High Severity (P1):**
    - **#62505 - Coding Agent Regression ([Link](openclaw/openclaw Issue #62505)):** A critical regression where the coding agent "never completes anything." *No fix PR found.*
    - **#44925 - Silent Subagent Loss ([Link](openclaw/openclaw Issue #44925)):** Systematically losing subagent results. *No fix PR found.*
    - **#22676 - Signal Daemon Race Condition ([Link](openclaw/openclaw Issue #22676)):** A race condition during restarts orphans processes and causes `send` failures. *No fix PR found.*
    - **#43296 - Session Context Confusion ([Link](openclaw/openclaw Issue #32296)):** Agent replies to the wrong message. *This issue is marked closed.*
    - **Main Theme:** The #1 source of bugs is **concurrency and race conditions** around session state, message queues, and agent orchestration, leading to message loss and crashes. Many of these are regressions from recent versions.

- **Performance Degradation (P2):**
    - **#54155 - Gateway Memory Leak ([Link](openclaw/openclaw Issue #54155)):** A major leak growing from 389MB to 14.7GB over 4 days.
    - **#67419 - Context Bloat ([Link](openclaw/openclaw Issue #67419)):** Bootstrap files (MEMORY.md, etc.) waste 20-30% of the context window, reducing model effectiveness.

#### 6. Feature Requests & Roadmap Signals

User requests are shifting from basic functionality towards more mature, enterprise-like controls and customization.

- **High Demand & Likely in Next Version:**
    - **Per-Agent Memory Wikis (#63829):** Users want isolated knowledge bases for different agents in a multi-agent setup. *High demand (9 👍).*
    - **Configurable Streaming Watchdog (#68596):** A direct response to model evolution. *High demand (8 👍).*
    - **Private Network Access (Tool: fetch) (#39604):** A critical feature for users integrating agents with internal networks (localhost, 192.168.x). *High demand (9 👍).*
    - **Sensitive Data Redaction (#64046):** Security-conscious users want their API keys and other secrets masked in logs and the UI. *Moderate demand.*

- **Longer-Term Signals:**
    - **Persistent Task Status (#52640):** A first-class status indicator for long-running tasks, moving beyond simple typing indicators.
    - **Context Provenance (#54373):** Adding metadata to injected context so the agent knows where information came from (e.g., "freshly read" vs. "session start"). This shows a need for more intelligent context management.

#### 7. User Feedback Summary

- **Major Pain Points:**
    - **Silent Failures:** This is the #1 source of dissatisfaction. Users report agents that appear to respond but don't (e.g., message loss, completions not returned).
    - **Regression Instability:** Frequent updates ("it worked in version X") are breaking core features, creating a sense of fragility.
    - **Cross-Platform Incompleteness:** A strong sense of being left behind among non-macOS users.
    - **Complex Configuration:** The depth of bugs related to `config.patch` and `SIGUSR1` suggests that the hot-reload configuration process is fragile and a source of many outages.

- **Positive Signals:**
    - Users are highly engaged, attempting complex workflows (multi-agent orchestration, cron jobs.
    - The community is contributing a very high volume of PRs to fix the identified issues.

#### 8. Backlog Watch

Several critical issues with "needs-maintainer-review" or "needs-product-decision" labels have been open for a long time, creating a bottleneck.

- **Issue #75 (Linux/Windows Apps):** Open for 5.5 months, with 109 comments and 79 👍. While there is a PR (#59859), the issue itself is still open and in a needy state.
- **Issue #11665 (Webhook Multi-turn Support):** Open for 4 months. A documented feature is fundamentally broken. The lack of resolution creates a negative trust signal.
- **Issue #40001 (Write Tool Append Mode):** Open for 3 months. A basic I/O function is missing, causing data loss for users relying on cron jobs.
- **Issue #75538 (Accessibility - Screen Reader):** Open for 2 months. This is a barrier to entry for a specific user group and has been labeled "needs-live-repro," but no progress seems apparent.

**Conclusion:** OpenClaw is a vibrant but intensely volatile project. It is attracting massive usage and contributions, but its current health is poor due to a plague of regressions and race conditions in its core session and message routing logic. The community is providing an enormous amount of feedback and code to fix these issues, but the maintainers appear to be bottlenecked on triage and decision-making. The next version needs to focus more on **stabilization** rather than feature expansion to retain user trust.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided daily digests.

---

## Cross-Project Ecosystem Report: 2026-06-17

### 1. Ecosystem Overview

The open-source personal AI agent landscape on June 17, 2026, is characterized by a phase of intense, post-release consolidation, particularly for projects built on the Claw architecture. After a period of rapid feature expansion, the community is now contending with significant stability regressions, silent failures, and concurrency bugs that undermine user trust in core agentic workflows (multi-step tasks, session management, and cross-platform reliability). A clear divide is emerging between flagship, high-velocity projects (OpenClaw, ZeroClaw) that are processing hundreds of issues daily, and a tier of more focused or niche tools (TinyClaw, ZeptoClaw) with minimal activity. Across the board, shared pain points around long-context degradation, installer fragility, and documentation quality signal that the ecosystem is maturing beyond its early adoption phase and is now under pressure to deliver production-grade reliability and enterprise-level controls to retain its user base.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today | Health Assessment |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | v2026.6.8 | Poor – High volume, critical regressions, race conditions, maintainer bottleneck |
| **ZeroClaw** | 49 | 50 | None | Fair – High activity, fixing regressions (v0.8.0), documentation gap |
| **Hermes Agent** | 50+ | 50+ | None | Fair – High maintenance churn, good PR responsiveness, multi-platform bugs |
| **CoPaw (QwenPaw)** | 43 | 39 | v1.1.12-beta.1 | Fair – High activity, critical SIGSEGV crashes, long-context freeze |
| **NanoBot** | 9 | 24 | None | Good – Strong PR throughput, backlog clearing, minor installer issues |
| **IronClaw** | 50 | 50 | None | Fair – High-velocity sprint, UX friction in new WebUI, automation reliability |
| **PicoClaw** | 15 | 15 | Nightly build (v0.3.0) | Fair – High PR merge rate, but 12 stale security advisories |
| **NanoClaw** | 6 | 5 | None | Good – Healthy maintenance, quick bug fix turnaround, compliance concern |
| **LobsterAI** | 1 | 4 | None | Good – Steady incremental progress, but stale bugs (2+ months) |
| **Moltis** | 4 | 2 | None | Good – Responsive triage, quiet but focused |
| **NullClaw** | 2 | 3 | None | Fair – Low activity, long-running feature PR uncommented |
| **TinyClaw** | 0 | 1 | None | Stable but idle – Low engagement, single Windows fix pending |
| **ZeptoClaw** | 0 | 1 | None | Stable but idle – Only a Dependabot PR |

### 3. OpenClaw's Position

OpenClaw remains the undisputed **reference implementation** and the most active project by an order of magnitude, with 500 issues and 500 PRs updated in a single day. However, this volume is a double-edged sword.

- **Advantages:** Largest community, most extensive feature set, and the deepest integration ecosystem (Telegram, Discord, WhatsApp, CLI). It defines the architectural standard for other Claw-based projects.
- **Disadvantages:** Its health is currently poor. The massive number of issues is not a sign of health but of a system struggling under its own complexity. It is plagued by a "plague of regressions" and race conditions in core session/message routing logic, leading to severe silent failure problems and eroded user trust.
- **Technical Approach Difference:** OpenClaw's approach of building a single, monolithic agent with broad platform support is creating a maintenance nightmare. In contrast, **ZeroClaw** is differentiating by leveraging a Rust-based runtime (praised for lower resource usage) and an extensible tool ecosystem, while **CoPaw** is more focused on long-context management and integrating compression techniques.
- **Community Size Comparison:** OpenClaw's community is the largest and most vocal, but also the most frustrated. The 109-comment issue on cross-platform apps (#75) and the 79-upvote demand for a fix highlight a massive, engaged user base that is not getting its core needs met.

### 4. Shared Technical Focus Areas

A strong signal emerges: the ecosystem is desperately working on the same set of fundamental runtime problems.

- **Long-Context Degradation & Session Stability:**
    - **OpenClaw:** Session state corruption, context bloat (MEMORY.md wasting 20-30% window), silent subagent loss.
    - **CoPaw (QwenPaw):** Process freezes during context compaction, Long Conversation Freeze, requests for Headroom compression integration.
    - **NanoBot:** History injection issues even with Dream disabled.
    - **ZeroClaw:** Resumed sessions reopen with blank transcripts.
- **Installation & Environment Friction:**
    - **NanoBot:** PEP 668 issue on macOS, Debian Docker installer failure.
    - **NanoClaw:** Silent budget exhaustion turns.
    - **Hermes Agent:** Windows installer `python.exe` lock bug.
- **Multi-Provider & API Compatibility:**
    - **PicoClaw:** Empty LLM response retry logic.
    - **ZeroClaw:** MCP tools unavailable on specific providers (OpenAI/Anthropic).
    - **CoPaw:** Gemini API 400 errors, MiniMax XML format incompatibility.
    - **NullClaw:** Ollama integration returns truncated answers.
- **Security & Authorization Sandboxing:**
    - **PicoClaw:** Batch of 12 stale security advisories (SSRF, CSRF, privilege escalation).
    - **OpenClaw:** PathGuard filesystem access PR in review.
    - **ZeroClaw:** Hardened CI pipeline and signed attestations RFC.

### 5. Differentiation Analysis

| Project | Core Focus / Target User | Key Differentiator |
|---|---|---|
| **OpenClaw** | General-purpose, multi-platform user | The most comprehensive feature set, massive community, but struggling with monolithic complexity |
| **ZeroClaw** | Performance-conscious, light-weight deployment | **Rust-based runtime** for lower resource usage; prebuilt binaries are a key feature (currently broken) |
| **CoPaw (QwenPaw)** | Power users with long, complex sessions | Aggressive focus on **long-context management** (Headroom compression, auto-compaction) and i18n support |
| **NanoBot** | Easy setup, Docker-first deployment | Strong **installer reliability** and quick bug-fix turnaround; good for new users |
| **IronClaw** | Enterprise / Automation | Focus on **Engine V2**, multi-route execution, and a new **Reborn WebUI** for automations |
| **PicoClaw** | Telegram / Mobile-first | Narrow, strong integration with Telegram forum topics; adding security and WebUI improvements |
| **NanoClaw** | Lightweight, API-first | **Budget controls** and quick fixes; compliance anxiety around Anthropic credential proxy is a unique concern |
| **Hermes Agent** | Enterprise multi-channel communication | Strong support for **WeCom, Feishu, Matrix** in China market; good community-to-maintainer feedback loop |

### 6. Community Momentum & Maturity

- **Tier 1: High-Velocity Iteration (Struggling with Scale)**
    - **OpenClaw**, **ZeroClaw**, **IronClaw**: Processing 50-500 items daily. These are "first-movers" and feature-rich, but their high PR churn is masking deep stability issues. They are in a "firefighting" mode, reacting to post-release regressions. Their maturity is **high in scope, low in stability**.
- **Tier 2: Healthy Pre-Release / Feature Stabilization**
    - **CoPaw (QwenPaw)**: High activity but focused on a specific tight set of bugs (SIGSEGV, context freeze). The release of a beta patch shows disciplined release management. Maturity is **moderate**.
    - **NanoBot**, **NanoClaw**, **Moltis**: Lower volume but higher merge rates and clear focus. These projects are in a **healthy maintenance and incremental improvement phase**. Maturity is **high** relative to their scope.
- **Tier 3: Low Activity / Niche or Stalled**
    - **NullClaw**, **LobsterAI**, **TinyClaw**, **ZeptoClaw**: Low engagement. These projects may be mature codebases (ZeptoClaw), focused on a specific niche (TinyClaw), or simply lack community momentum. They are **stable but idle**.

### 7. Trend Signals

- **From "It Works" to "It Works Reliably":** The #1 feedback across all major projects is no longer about missing features, but about **silent failures, data loss, and trust**. Users want their agents to *not* lose messages, *not* get stuck in loops, and *not* corrupt their session state. The next competitive battleground is runtime reliability, not novel tools.
- **The "Configuration Complexity Ceiling":** Across OpenClaw, ZeroClaw, and Hermes Agent, users are hitting a wall with raw config files. There is a strong demand for **GUI-based configuration** (managing providers, API keys, profiles) that removes the need to edit TOML/YAML/JSON. The push towards ZeroCode (ZeroClaw) and Desktop apps (OpenClaw) is a direct response to this.
- **Rise of Specialized Runtimes:** The success of **ZeroClaw** (Rust) hints at a future where the "core agent OS" is decoupled from the Python ecosystem to solve resource and stability problems. The "Claw" architecture is splitting into lighter, language-optimized variants.
- **The "Long-Context Wall" is Real:** Users of advanced reasoning models (DeepSeek-R1, etc.) are consistently hitting hardcoded timeouts (OpenClaw's watchdog) or performance bugs (CoPaw's freeze). This creates an urgent need for smarter context window management, compression, and out-of-band thinking support.
- **Enterprise Governance is Emerging:** IronClaw's focus on **automation approvals, run threads, SSO auth, and Engine V2 multi-route execution** shows that enterprise deployment use-cases (auditability, reliability, security) are becoming a key driver, even in open-source projects.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-17

## Today's Overview
NanoBot is showing high activity with 9 issues updated and 24 pull requests updated in the last 24 hours. A strong 6 of 9 issues were closed, and 14 of 24 PRs were merged or closed, indicating the maintainers are actively clearing the backlog. The project has no new releases today, but the sustained PR throughput (especially bug fixes and infrastructure improvements) points to healthy engineering velocity. Community engagement remains solid, with several first-time contributors submitting meaningful patches around installer reliability, proxy handling, and provider compatibility.

## Releases
No new releases were published today.

## Project Progress
**14 PRs were merged or closed today**, advancing several areas:

- **WebUI Automation Management** (#4330, closed) — Adds a first-class automations section in the WebUI with filtering, sorting, editing, running, pausing/resuming, and deleting user-created automations, while keeping system jobs read-only. This is a significant feature delivery.
- **Installer & Environment Fixes** — Multiple merged PRs improve install reliability:
  - macOS PEP 668 fix (#4368) — avoids system-wide pip installs on externally-managed Python, preferring venv, uv, pipx.
  - Curl installer docs switch to pipe pattern (#4365) — fixes Dockerfile and script embedding issues.
- **Default Behavior Changes**:
  - Idle auto-compact enabled by default (#4370) — `idleCompactAfterMinutes` now defaults to 15 minutes instead of 0 (disabled).
  - Empty Dream runs now return a recoverable explanation (#4369) instead of an opaque failure.
- **Context & Provider Fixes**:
  - Recent-history digest capped by tokens, not characters (#4352) — prevents silent truncation of CJK and code-heavy system prompts.
  - Stream idle timeout centralized and validated (#4363) — fixes crashes from malformed `NANOBOT_STREAM_IDLE_TIMEOUT_S`.
  - Empty-response retry no longer duplicates user turns (#4358, closes #4079).
  - Kimi K2.7 model thinking support added (#4361).
  - WebUI dev-server LAN connectivity fixed (#4364).
  - `.gitignore` exclusion for bridge Node modules (#4355).

## Community Hot Topics
- **Issue #4360** (closed, 9 comments) — *"end of file unexpected" during installer*. A fresh Debian 13 Docker container fails with a pip syntax error. The discussion was likely resolved or supplemented by the simultaneous macOS installer fixes.
- **PR #4350** (open) — *Add Keenable search provider*. A new built-in web search option alongside DuckDuckGo/Brave/Tavily/etc. This PR has no comments but is the only feature addition PR open today, suggesting maintainer interest in expanding search provider support.
- **PR #4356** (open) — *Sanitize Anthropic tool IDs*. Addresses 400 errors from tool IDs containing pipes/dots from other providers or multi-turn sessions. A high-impact reliability fix for multi-provider setups.
- **Issue #4375** (open, new today) — *Git commands blocked by workspace security policy* in subdirectories. No comments yet, but represents a workflow blocker for users relying on Nanobot's Git tooling.

## Bugs & Stability

| Severity | Issue | Summary | Fix PR Exists? |
|----------|-------|---------|----------------|
| **High** | #4375 | Git commands blocked by workspace security guard in subdirectories | No |
| **High** | #4366 (closed) | Local model servers need proxy setting; HTTP_PROXY breaks localhost connections | Yes: #4367 (open) |
| **Medium** | #4374 | WebUI project workspaces: SOUL.md/USER.md read from project but written to default workspace | No |
| **Medium** | #4242 (open) | Disabling dream.enabled still injects all chat history into system prompt via Recent History | No |
| **Fixed** | #4360 | *"end of file unexpected"* during installer on Debian 13 | Explicit fix PR unclear, but #4368 and #4365 address installer robustness |
| **Fixed** | #4286 | Missing *"sustained goal"* context bug (closed, 1 comment) | Yes (closed) |
| **Fixed** | #4065 | Invalid `NANOBOT_STREAM_IDLE_TIMEOUT_S` crashes streaming | Yes: #4363 (merged) |
| **Fixed** | #4079 | API empty-response retry duplicates user turns | Yes: #4358 (merged) |

## Feature Requests & Roadmap Signals
- **New Search Provider: Keenable** (#4350) — A research-driven search engine company submitted a PR to become a built-in provider. If merged, it signals the project's openness to third-party search integrations.
- **Anthropic Tool ID Sanitization** (#4356) — While a bug fix, the need for cross-provider message format sanitization is a growing feature area as multi-model deployments expand.
- **Kimi K2.7 Thinking Support** (#4361, merged) — Shows active vendor-specific model support is a priority, likely continuing with more Chinese-model integrations.
- **Project Workspace Asymmetry** (#4374) — The SOUL.md/USER.md read/write mismatch may drive a follow-up PR to centralize workspace file paths, potentially in the next minor release.

**Prediction for next release**: Keenable search provider, Anthropic tool ID fix, and the WebUI automation management view are strong candidates for the next tagged version.

## User Feedback Summary
- **Pain point: Installer fragility** — Two separate installer issues (#4360 Debian, #4368 macOS) and a concurrent docs fix (#4365) suggest installation remains the top friction point for new users. The maintainers are actively addressing this with improved fallback logic.
- **Pain point: Proxy handling** — #4366 (closed) and its fix PR #4367 highlight that users behind corporate proxies or running local model servers are hitting silent failures. The community contributed a fix for ignoring proxies on local endpoints.
- **Pain point: Dream/History confusion** — #4242 and #4369 (merged) indicate users are confused about how Dream runs interact with auto-compact and history injection. The new explanatory messages in #4369 should reduce support queries.
- **Satisfaction signal**: Keenable submitted a self-promotional integration PR (#4362) without being asked, suggesting the project's A2A/MCP compatibility is attracting external tool developers.

## Backlog Watch
- **PR #3662** (open since May 6) — *Avoid network loads during token estimation*. A 42-day-old enhancement PR that would improve offline/resource-constrained environments. Has no comments and no recent activity. This may need a maintainer review or can be closed if deprioritized.
- **PR #4053** (open since May 29, 19 days) — *Keep read-only roots out of write paths*. A security-focused filesystem enhancement with regression tests. Updated yesterday but still unmerged. Given it modifies core tool permissions, it likely requires careful review.
- **Issue #4242** (open since June 8) — *Dream disabled still injects history*. One comment, no PR linked. This is a nuanced bug affecting users who explicitly disable Dream but still see history bloat. Maintainers may need trace-level debugging to reproduce.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for June 17, 2026.

---

## Hermes Agent Project Digest: 2026-06-17

### 1. Today's Overview

The Hermes Agent project is in a highly active maintenance and feature-development phase, processing over 50 Issues and 50 PRs in the last 24 hours. While no new releases were cut today, the community is driving significant stability improvements through a high volume of pull requests targeting bug fixes across a wide range of platform adapters (WhatsApp, Telegram, WeCom, Feishu). Key areas of focus include resolving persistent "zombie connection" bugs on messaging platforms, improving the reliability of the new TUI and Desktop interfaces, and addressing critical user feedback around multi-tenancy and enterprise deployment. The volume of activity suggests a strong focus on quality-of-life fixes ahead of a potential upcoming stable release.

### 2. Releases

**None.** No new releases were published today.

### 3. Project Progress

Several significant PRs were merged or advanced today, indicating active progress in specific areas:

- **Deployment Fixes:** **PR #47555** (P1) addresses a critical crash-loop issue in the supervised Docker gateway by using `--replace` to take over stale container holders.
- **UI/UX Polish:** **PR #45992** (Merged) fixes the Desktop model selector not updating when switching profiles. **PR #47558** improves the Desktop UI by prevalidating reserved profile names, preventing confusing raw IPC errors.
- **Platform Reliability:** **PR #47562** fixes the Feishu adapter to correctly extract table data from interactive cards for reply context. **PR #47567** resolves a critical sync issue for the Matrix adapter.
- **Core Fixes:** **PR #47144** (Merged) improves container detection to support containerd and cgroup v2, a key fix for Kubernetes deployments.

### 4. Community Hot Topics

The community is driving several high-value discussions and feature requests:

- **Multi-Tenant Memory Isolation (Issue #34352):** This remains the most active discussion (7 comments) driven by **NimbleCoAI**. The user presents a compelling case for Hermes to lead in "multiplayer agentic AI" and details a production fix for memory isolation. A dedicated PR (#47552) was submitted today to address this, suggesting strong community-engineering overlap and high maintainer attention.
- **Slack Markdown Support (Issue #8552):** With 9 👍 reactions, this feature request for Block Kit support to enable markdown tables is a clear pain point for Slack users. It remains open with 7 comments, indicating a high-demand feature that is still awaiting implementation.
- **Model Provider Picker (Issue #12655 & #10011):** Two related feature requests (7 & 3 comments respectively) highlight a desire for more control over the `/model` picker—filtering providers and auto-discovering models from custom API gateways. This points to a growing need for enterprise/advanced user configuration.
- **Claude Max/Pro Billing Bug (Issue #40014):** A critical user experience bug where OAuth credentials still hit pay-per-token endpoints instead of using subscription quotas, burning through credits. This is a potential financial drain for users and likely a high-priority item.

### 5. Bugs & Stability

Yesterday saw a significant number of new bug reports, many with corresponding fix PRs already submitted, indicating high responsiveness from the team.

- **P1 (Critical):**
    - **SysOps Incident (#47000):** A serious state-drift incident where all 23 lifecycle scheduler jobs were disabled by a specific personality profile (P12). Currently in a "watching" status.
    - **MCP Gateway Crash (#47134):** The `/reload-mcp` command can crash the entire gateway by sending `SIGTERM` to its own process group. **PR #47551** fixes a related bug (oversized screenshots causing 400 errors).
- **P2 (High):**
    - **WeCom Zombie Connection (#47564):** The adapter does not trigger a reconnection upon receiving a specific error code (846609), leading to a 57-79 second dead window.
    - **Telegram Typing Indicator Stuck (#47539):** The "typing..." indicator can persist forever (30+ minutes) after a session ends due to an orphaned async task.
    - **Desktop App Crash on Photo Send (#47498):** Sending a photo causes a "Maximum call stack size exceeded" crash in the Electron app, leading to a crash loop on restart.
    - **Windows Installer Bug (#47557):** The PowerShell installer fails to recreate the venv because it doesn't kill lingering `python.exe` processes that hold locks on `.pyd` files.
- **P3 (Medium):**
    - **Desktop Link Preview (#47500):** Hovering over links can trigger custom Windows protocol handlers (e.g., `bitbrowser://`), opening unwanted apps.

### 6. Feature Requests & Roadmap Signals

- **Memory Isolation for Multi-Tenancy (#34352, PR #47552):** A highly anticipated feature with a fix already submitted. Likely to land in the next version.
- **UI Scaling & Zoom (#47499):** User requested zoom controls for the Desktop app, a high-need feature for high-DPI displays and accessibility.
- **Dedicated Providers Settings Section (#39020):** Users want a proper GUI for managing API keys and enabling/disabling providers, moving away from raw config files.
- **Quick Workspace Switcher (#38849):** Users want to switch between profiles from the Desktop status bar without using the CLI.
- **Channel-Scoped Memory Context ID (#47552):** The proposed solution to the multi-tenancy problem introduces a `context_id` parameter, which could be a foundational building block for more advanced memory management.

### 7. User Feedback Summary

- **Strong Satisfaction with Community-Dev Interaction:** The submission of PR #47552 to address Issue #34352 shows a highly effective feedback loop where a user's production-grade fix is directly upstreamed, indicating strong project health.
- **Frustration with Platform-Specific Quirks:** A recurring theme is "zombie" connections and silent failures on niche platforms (WeCom, QQ Bot, Matrix), causing long periods of unreliability for users on these channels.
- **Financial Pain from Billing Bugs:** Issue #40014 (Claude Max billing) represents a real financial cost to users, causing significant dissatisfaction and a sense of being overcharged due to a routing error.
- **Need for Better UX:** Requests for UI scaling (#47499), a providers settings section (#39020), and a profile switcher (#38849) reflect a user base that is moving beyond CLI-only usage and demanding a more polished, desktop-native experience.

### 8. Backlog Watch

- **Issue #8552 (Slack Block Kit - 9 👍):** A high-demand feature for Slack users that has been open since April 2026 with no sign of an assigned implementer.
- **Issue #19821 (QQ Bot Zombie Connection - P2):** This long-standing bug (opened May 4) describing a fatal "silent death" of the WebSocket connection remains open without a fix PR, suggesting the QQ Bot integration may be under-resourced.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-17

## Today's Overview
PicoClaw is experiencing a high-velocity development day with 15 issues updated and 15 PRs processed in the last 24 hours. A new nightly build (v0.3.0-nightly.20260617) has been released. Activity is dominated by two waves: a security audit disclosure batch of 12 issues filed on June 9, all now marked as `stale`, and a surge of merged bug-fix PRs addressing Telegram forum topics, panic recovery, and LLM response handling. The project shows strong maintainer responsiveness with 12 PRs merged/closed today, though the stale security issues remain open without visible resolution patches.

## Releases
**Nightly Build v0.3.0-nightly.20260617** released today.

- Auto-generated nightly, marked as potentially unstable.
- Full changelog: https://github.com/sipeed/picoclaw/compare/v0.3.0...main
- No breaking changes or migration notes provided.

## Project Progress
**12 PRs merged/closed today**, indicating strong engineering throughput:

**New Features:**
- [#3137](https://github.com/sipeed/picoclaw/pull/3137) — `tools.cron.command_allowed_remotes` config to restrict remote cron command execution to selected channels.
- [#3120](https://github.com/sipeed/picoclaw/pull/3120) — `RegisterChannelSettings` hook enabling out-of-tree channel registration without forking PicoClaw.

**Bug Fixes:**
- [#3135](https://github.com/sipeed/picoclaw/pull/3135) — Telegram forum topic reply fix: `InboundContext.ChatID` now uses compositeChatID, aligning with `StartTyping` behavior.
- [#3132](https://github.com/sipeed/picoclaw/pull/3132) — Panic recovery added to core-path goroutines to prevent single-goroutine crashes from killing the process.
- [#3127](https://github.com/sipeed/picoclaw/pull/3127) — Explicitly ignore `Close()` errors on directory file descriptors to suppress benign linter warnings.
- [#3129](https://github.com/sipeed/picoclaw/pull/3129) — Explicitly ignore `file.Close()` error in TTS write error path.
- [#3130](https://github.com/sipeed/picoclaw/pull/3130) — `json.Marshal` errors in seahorse grep/expand tools now return descriptive `ErrorResult` instead of silently failing.
- [#2990](https://github.com/sipeed/picoclaw/pull/2990) — Web UI now shows full session history instead of only the last user message.
- [#2988](https://github.com/sipeed/picoclaw/pull/2988) — `/context` command now respects `summarize_token_percent` config instead of always showing 76800 tokens.
- [#2987](https://github.com/sipeed/picoclaw/pull/2987) — `tool_calls` messages no longer dropped during active streaming sessions.
- [#2983](https://github.com/sipeed/picoclaw/pull/2983) — Retry logic added for empty LLM responses from OpenAI-compatible providers.

## Community Hot Topics
**Most Active Issue:**
- [#2404](https://github.com/sipeed/picoclaw/issues/2404) — **Feature: streaming HTTP requests** (12 comments, 1 👍). User requests `"streaming": true` config support for LLM backends. Open since April 7, now stale. This is the longest-running active feature request with significant community interest.

**Security Advisory Batch:**
Twelve security issues filed June 9 by YLChen-007, each with 1 comment (maintainer acknowledgment). All remain open. Key reports include:
- [#3082](https://github.com/sipeed/picoclaw/issues/3082) — Feishu reply-context bypasses `allow_from` for parent messages.
- [#3081](https://github.com/sipeed/picoclaw/issues/3081) — Approval hook `cwd` symlink race allows `exec` in unapproved directory.
- [#3071](https://github.com/sipeed/picoclaw/issues/3071) — Authenticated WebSocket clients can trigger unauthorized `/reload`.

These collectively signal a systematic security review of channel authorization and execution sandboxing.

## Bugs & Stability
**Ranked by severity:**

1. **HIGH** — [#3081](https://github.com/sipeed/picoclaw/issues/3081) Approval hook `cwd` symlink race (privilege escalation via `exec`). No fix PR.
2. **HIGH** — [#3078](https://github.com/sipeed/picoclaw/issues/3078) SSRF bypass via HTTP proxy in `web_fetch`. No fix PR.
3. **HIGH** — [#3072](https://github.com/sipeed/picoclaw/issues/3072) CSRF in launcher first-run password setup allows local takeover. No fix PR.
4. **MEDIUM** — [#3110](https://github.com/sipeed/picoclaw/issues/3110) Telegram forum topic replies default to `#General`. **FIXED** in [#3135](https://github.com/sipeed/picoclaw/pull/3135) (merged today).
5. **MEDIUM** — [#3134](https://github.com/sipeed/picoclaw/issues/3134) `su -c 'echo OK'` fails with "No daemon is currently running". **CLOSED** today.
6. **LOW** — [#2987](https://github.com/sipeed/picoclaw/pull/2987) `tool_calls` dropped during streaming. **FIXED** (merged June 16).
7. **LOW** — [#2983](https://github.com/sipeed/picoclaw/pull/2983) Empty LLM response not retried. **FIXED** (merged June 16).

## Feature Requests & Roadmap Signals
- **[#2404](https://github.com/sipeed/picoclaw/issues/2404)** — **Streaming HTTP config** (`"streaming": true`). Core UX improvement for LLM backends. Despite being open since April and stale, it has strong community support. Likely candidate for v0.3.1 given the nightly build cadence.
- **[#3120](https://github.com/sipeed/picoclaw/pull/3120)** — Out-of-tree channel registration (merged today). This is an architectural extension enabling third-party channel plugins, signaling intent to grow the ecosystem.
- **[#3137](https://github.com/sipeed/picoclaw/pull/3137)** — Remote cron command restrictions (merged today). Enhances security posture for cron-triggered operations.

**Prediction:** Streaming support and channel plugin SDK are plausible next major features, potentially in v0.3.0 stable or v0.3.1.

## User Feedback Summary
**Pain Points:**
- **Telegram Forum Topic Confusion** — [#3110](https://github.com/sipeed/picoclaw/issues/3110) demonstrates real user frustration: typing indicator works in correct topic but message lands in `#General`. Fixed today.
- **Session History Visibility** — Users could only see the last message in multi-turn conversations via Web UI. Fixed in [#2990](https://github.com/sipeed/picoclaw/pull/2990).
- **`su -c` Shell Invocation** — [#3134](https://github.com/sipeed/picoclaw/issues/3134) user discovered that standard Linux shell patterns fail, indicating gaps in agent command execution.

**Satisfaction Signals:**
- High PR merge rate (12/15 today) suggests responsive maintainers.
- Security disclosure by YLChen-007 (12 issues) indicates external security researchers actively auditing, a sign of project maturity.

**Dissatisfaction Signals:**
- 12 stale security issues (filed June 9) have only 1 comment each (likely maintainer acknowledgment), with no fix progress visible. Users may perceive delayed response to critical vulnerabilities.

## Backlog Watch
**Critical:**
- **12 stale security advisories** (issues #[3068](https://github.com/sipeed/picoclaw/issues/3068)–#[3082](https://github.com/sipeed/picoclaw/issues/3082)), all filed June 9, all unaddressed. These cover SSRF, CSRF, privilege escalation, authorization bypass, and replay attacks. Maintainer attention urgently needed.

**Long-unanswered:**
- **[#2404](https://github.com/sipeed/picoclaw/issues/2404)** — Streaming HTTP feature request, open since April 7, stale. 12 comments, community engagement. No roadmap commitment visible.
- **[#3078](https://github.com/sipeed/picoclaw/issues/3078)** — SSRF via proxy in `web_fetch`, one of the more exploitable security issues, no triage update beyond initial comment.

**Open PRs pending review:**
- [#3116](https://github.com/sipeed/picoclaw/pull/3116) — `turn.done` lifecycle signaling fix (open since June 12, last updated June 16).
- [#3115](https://github.com/sipeed/picoclaw/pull/3115) — Fix inline data URL handling in session history (open since June 12).
- [#3136](https://github.com/sipeed/picoclaw/pull/3136) — Gemini API `thought_signature` snake_case support (opened today).

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-17

## Today's Overview

The NanoClaw project shows **moderate activity** with 5 PRs processed (4 closed/merged) and 6 issues updated in the last 24 hours. The project is in a **healthy maintenance and iteration phase**, with two critical bugs receiving fix PRs that were merged today. A notable community concern about API compliance (Anthropic's credential proxy policy) remains open and unresolved. No new releases were published today, indicating the team is consolidating fixes before a potential next version.

## Releases

**None** — No new releases were published today.

## Project Progress

Three meaningful fixes were merged/closed today:

- **#2759** (Closed) — **Budget/billing error delivery fix**: PR by `assapin` resolves the silent drop of budget-exhausted LLM turns (#2751). Agent-runner now delivers billing errors as user-visible messages instead of dropping them silently.
- **#2782** (Closed) — **Tailscale-Docker routing self-healing**: PR by `0xemc` fixes a long-standing issue where Tailscale's exit-node reconnections would flush ip rules, breaking container networking. The fix replaces a boot-only systemd unit with a more robust approach.
- **#2069** (Closed) — **Skill/webchat v1**: A feature skill PR by `javexed` has been merged after more than a month of development, adding webchat channel support.

One feature PR remains open:

- **#2780** (Open) — Adds `NANOCLAW_DISABLE_UPGRADE_TRIPWIRE=1` env var for managed fleets that bake NanoClaw into immutable images.

Documentation improvements also continued with **#2775** (Closed), clarifying the OneCLI gateway upgrade process in changelogs.

## Community Hot Topics

**Most Active Discussion:**
- **[Issue #1669](https://github.com/nanocoai/nanoclaw/issues/1669)** — *"Does Credential Proxy implementation risk Anthropic account bans?"* (1 comment, open since April 2026) — Despite only one comment, this is the longest-standing open debate. The user questions whether the Credential Proxy's OAuth reverse-proxy architecture violates Anthropic's ToS. **Underlying need**: The community is concerned about long-term sustainability and compliance risks. If Anthropic enforces its anti-fraud checks, users could lose API access. This may be blocking some enterprise adoptions.

**Other Active Issues:**
- **[Issue #2779](https://github.com/nanocoai/nanoclaw/issues/2779)** — Slack @handle mangling in URLs (1 comment, opened yesterday) — A user-discovered bug where agent-generated URLs containing `@` in paths get broken by Slack's mention detection. This is a quality-of-life issue for agents that share links to HackMD, Mastodon, or Medium profiles.

## Bugs & Stability

**High Severity:**
- **[Issue #2779](https://github.com/nanocoai/nanoclaw/issues/2779)** — *Slack: @handles inside URLs get mangled* — Agent-generated links break in Slack. **Severity: Medium-High** (functionality loss, but limited to Slack channel output). No fix PR yet.
- **[Issue #2784](https://github.com/nanocoai/nanoclaw/issues/2784)** — *container-runner staleness check misses ipc-mcp-stdio.ts changes* — The session source sync uses only `index.ts` as a staleness signal, so users editing `ipc-mcp-stdio.ts` won't trigger re-sync. **Severity: Medium** (silent code staleness, hard to debug). No fix PR yet.

**Low/Resolved:**
- **[Issue #2751](https://github.com/nanocoai/nanoclaw/issues/2751)** — *Budget-exhausted turns silently dropped* — **HIGH severity** but now **resolved** by PR #2759 (merged today). Users previously received no reply when token budgets were exhausted.

## Feature Requests & Roadmap Signals

**Likely Next Version Inclusions:**
- **[Issue #2780](https://github.com/nanocoai/nanoclaw/pull/2780)** — *NANOCLAW_DISABLE_UPGRADE_TRIPWIRE env var* — Open PR, likely to merge. Targets managed fleet operators who need deterministic startup behavior.
- **[Issue #2781](https://github.com/nanocoai/nanoclaw/issues/2781)** — *NANOCLAW_NATIVE_CREDENTIALS support* — User-requested bypass for OneCLI authentication in sandbox environments. No PR yet, but a clear use case from distributors.

**Documentation & Policy:**
- **[Issue #2783](https://github.com/nanocoai/nanoclaw/issues/2783)** — *docs/SECURITY.md describes retired v1 trust model* — The canonical security doc is outdated, referencing a non-existent skill. This is a **documentation liability** that could confuse new adopters evaluating security posture.

## User Feedback Summary

**Expressed Pain Points:**
1. **Silent failure on budget exhaustion** (#2751) — Users reported agents becoming unresponsive with no error feedback. **Now fixed**.
2. **Slack integration quality** (#2779) — URL mangling disrupts real workflows when agents share links in Slack channels.
3. **API compliance anxiety** (#1669) — Ongoing concern about Anthropic's anti-proxy policies affecting the Credential Proxy feature, a key differentiator.

**Expressed Satisfaction:**
- The quick turnaround on the budget-exhaustion fix (#2751 → #2759, 4 days) shows **responsive maintenance**, which users appreciate.
- The Tailscale routing fix (#2782) addresses a "silent failure" that was likely affecting self-hosted users.

**Use Case Signals:**
- **Enterprise/deployment operators** are pressing for environment-based configuration opt-outs (#2780, #2781) rather than hardcoded behaviors.
- **Self-hosted community** values reliability fixes (Tailscale routing, budget errors) over new features.

## Backlog Watch

**Critical Long-Standing Issue:**
- **[Issue #1669](https://github.com/nanocoai/nanoclaw/issues/1669)** — *Credential Proxy & Anthropic bans* — **Opened April 6, 2026 (72 days ago)**. Despite being the most consequential open issue (touches on project viability), it has only 1 comment and no maintainer response. The project should either (a) issue a formal security/policy analysis, or (b) document the risk and mitigation strategy in the README. Failure to address this could deter adoption.

**Stale PRs Needing Attention:**
- No stale PRs identified — the project appears to process PRs within days. This is a **healthy signal** for maintainer responsiveness.

**Documentation Drift:**
- **[Issue #2783](https://github.com/nanocoai/nanoclaw/issues/2783)** — *Outdated SECURITY.md* — Not critical but erodes trust; flagged as needing correction before next release.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-17

## 1. Today's Overview
NullClaw has seen low activity over the past 24 hours, with 2 open issues updated and 3 pull requests updated but none merged or closed. No new releases were published. Activity is concentrated around bug fixes for local model integration (Ollama) and scheduler tool access, along with ongoing work on Teams authentication and a long-running cron subagent feature. The absence of any merged PRs or closed issues suggests a consolidation or review phase, with maintainers focusing on open patches rather than pushing new changes.

## 2. Releases
_No new releases were published in the last 24 hours. The latest version remains v2026.4.17 (referenced in issue #839)._

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The three open PRs are:

- **#959** `fix(cron): persist paired token for scheduler tool access` — Aims to resolve issue #839 by persisting bearer tokens from `/pair` to the config directory, encrypted at rest using ChaCha20-Poly1305. This directly addresses the "bit has no access to scheduler" bug.
- **#958** `fix(teams): accept lowercase serviceurl JWT claim and raise JWKS fetch cap` — Fixes a 403 error during Bot Framework connector-token validation for MS Teams, caused by case sensitivity in the `serviceUrl` claim and a low JWKS fetch limit.
- **#783** `feat(cron): cron subagent, run history, JSON output, security hardening` — A long-running feature PR (since April 7) for a full cron subagent engine with DB-backed scheduling, multiple job types, timezone support, and JSON CLI output.

## 4. Community Hot Topics
All three active items are relatively quiet, with no more than 2 comments each. The two most discussed items are:

- **[#952: Local model using ollama returns incomplete answers](https://github.com/nullclaw/nullclaw/issues/952)** (2 comments, created Jun 11) — User reports that the agent produces truncated sentences using Gemma via Ollama. This is a usability blocker for local model users and the most recently discussed issue.
- **[#839: bug: bit has no access to scheduler !?](https://github.com/nullclaw/nullclaw/issues/839)** (1 comment, created Apr 18) — Scheduler tool access denied error in v2026.4.17. Although old, it has attracted a dedicated fix PR (#959) that is now under review.

## 5. Bugs & Stability
Two bugs are currently open and updated in the last 24 hours:

- **High severity: Issue #952** — Ollama integration returns incomplete answers with Gemma models, preventing coherent agent responses. No fix PR exists yet; reproduction with full steps (screenshot) is provided. This should be prioritized for local deployment users.
- **Medium severity: Issue #839** — Scheduler tool access denied ("bit has no access to scheduler") in the latest release. A fix is in progress via PR #959, which persists paired tokens for cron/schedule functionality. The fix is still open and unmerged.

No crashes or regressions were reported in the last 24 hours. Both bugs are pre-existing.

## 6. Feature Requests & Roadmap Signals
No new feature requests surfaced today. The most notable long-term feature signal is:

- **PR #783** (cron subagent) — This substantial feature has been open since April 7 and has received zero comments. It adds a full cron subagent engine, DB-backed history, JSON output, and security hardening. Its quiet state and lack of reviewer attention suggest it may be large or controversial; it could signal upcoming scheduling capabilities for enterprise users.

Teams authentication improvements (PR #958) are a tactical fix, not a new feature.

## 7. User Feedback Summary
From the two active issues, user feedback highlights:

- **Local model frustration (Issue #952):** Users running models like Gemma via Ollama encounter incomplete responses, indicating integration gaps with local inference setups. The user provided a detailed screenshot, showing they attempted standard usage but hit a truncation or parsing issue.
- **Permission configuration confusion (Issue #839):** A user encountered a "bit has no access to scheduler" error, likely related to token/pairing configuration. The error message alone is unhelpful for troubleshooting, and the user has not received a direct reply other than the PR referencing the issue. This reflects a need for clearer error messages or documentation around scheduler access.

No expressions of satisfaction or positive feedback were captured today.

## 8. Backlog Watch
Two items require maintainer attention:

- **[Issue #839: Scheduler access bug](https://github.com/nullclaw/nullclaw/issues/839)** — Created Apr 18, last updated Jun 16. While PR #959 exists to fix it, the issue itself has only 1 comment (the original report). The user has not received any direct response. Acknowledgment or testing assistance request would improve community engagement.
- **[PR #783: Cron subagent feature](https://github.com/nullclaw/nullclaw/pull/783)** — Open since Apr 7 with zero comments. No maintainer has reviewed or requested changes. This large PR risks becoming stale; a status update or decision (merge vs. close vs. revise) would clarify roadmap direction.

No other long-unanswered critical issues are present in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-17

## Today's Overview

IronClaw shows elevated development activity with 50 issues and 50 PRs updated in the last 24 hours, indicating a high-velocity sprint cycle. The project is in a **intensive stabilization and feature-completion phase** for the Reborn WebUI and Engine V2, with 20 issues closed and 15 PRs merged/closed today. A significant cluster of UX refinement issues (automations dashboard, skills page, approval dialogs) and critical bug fixes (SSO automation failures, approval-gate denial loops) dominate the active queue. No new releases were published today; the team appears focused on landing a substantial batch of fixes before the next tag.

## Releases

No new releases were published in the last 24 hours.

## Project Progress

**Merged/Closed PRs (15 total, selected highlights):**

- **[#4902](https://github.com/nearai/ironclaw/pull/4902) [merged]** — `feat(openai-compat): vision support for inline images` — Step 4 of the attachments epic (#4644). Inline base64 `image_url` content parts on `POST /v1/chat/completions` now reach a vision-capable model. This unblocks multimodal use cases for API consumers.

- **[#4858](https://github.com/nearai/ironclaw/pull/4858) [merged]** — `fix(reborn): show sanitized command details` — Fixes #4852 by surfacing `builtin.shell` command details in approval dialogs and Activity history (previously showed only generic `Capability: builtin.shell`). A direct response to dogfooding feedback.

- **[#4954](https://github.com/nearai/ironclaw/pull/4954) [merged]** — `fix(reborn): surface approval-gate denial to model instead of cancelling the run` — Previously, denying an approval-gated capability cancelled the entire run. Now the model receives feedback that the user declined, allowing re-planning instead of infinite re-block loops.

- **[#4995](https://github.com/nearai/ironclaw/pull/4995) [merged]** — `feat(bench): forward NEARAI_API_KEY so /benchmark reborn runs use NEAR cloud` — Infrastructure change routing benchmark agent runs to NEAR AI cloud instead of OpenRouter.

**Key feature advancements visible from merged work:**
- OpenAI-compat vision support (inline images) is now functional
- Approval gate denial now surfaces to the model rather than cancelling runs
- Shell command details are visible in approval/activity views
- Content-digest plumbing for output-aware progress (PR #5000, stacked but progressing)
- Slack OAuth URL now gated on verified personal DM (#4953, open but advanced)

## Community Hot Topics

**Most Active Issues:**

1. **[#2721](https://github.com/nearai/ironclaw/issues/2721)** — `Engine V2 quality: Milestone 0 + multi-route execution` (3 comments, closed) — The parent epic for Engine V2 quality improvements has been evaluated and closed. This milestone targeted reducing over-reliance on the single CodeAct/orchestrator path. The closure signals completion of the evaluation phase.

2. **[#4942](https://github.com/nearai/ironclaw/issues/4942)** — `[Reborn WebUI] Tool calls failed won't appear until the re-fetch/reload` (2 comments, open) — A blocking UX issue where failed Google Suite tool calls (especially Drive operations) are invisible until manual page refresh. Users report this as a critical workflow disruption.

3. **[#4986](https://github.com/nearai/ironclaw/issues/4986)** — `[Reborn] Recurring automation can become permanently blocked waiting for tool approval` (1 comment, open) — An automation that requires `builtin.http` can get stuck in RUNNING state indefinitely when waiting for user approval that the user never sees. This represents a serious reliability concern for unattended automations.

**Most Active PRs:**

- **[#5003](https://github.com/nearai/ironclaw/pull/5003)** — `fix(reborn): recover stranded local-dev SSO automations + surface fire-failure reason` — Direct fix for the Railway SSO automation breakage (#4992). Labelled XL size, regular contributor.

- **[#5001](https://github.com/nearai/ironclaw/pull/5001)** — `fix(safety): relax provider-output validation to stop give-up loops (B+C+D)` — Addresses the top two recommended fixes from the PinchBench failure taxonomy. Directly tackles model "give-up" loops by relaxing provider output validation.

- **[#5000](https://github.com/nearai/ironclaw/pull/5000)** — `feat(agent-loop): content-digest plumbing for output-aware progress (PR2)` — Second PR in the no-progress redesign stack. Adds inert plumbing for content digest tracking, a prerequisite for smarter loop detection.

**Underlying Needs:** Community energy is concentrated around **automation reliability** (blocked runs, invisible failures, approval loops) and **Engine V2 quality** (reducing unnecessary code execution, better finalization). The volume of UX issues from internal dogfooding suggests the team is actively stress-testing before a broader rollout.

## Bugs & Stability

**Critical (run-blocking or data-loss):**

- **[#4986](https://github.com/nearai/ironclaw/issues/4986)** — `[Reborn] Recurring automation can become permanently blocked waiting for tool approval` — **Severity: Critical**. Automations that require tool approval (e.g., `builtin.http`) get stuck in RUNNING state with no visible thread for the user to act on. No fix PR linked yet. The associated run thread is invisible (#4987, same submitter).

- **[#4992](https://github.com/nearai/ironclaw/issues/4992)** — `[Reborn] Local-dev SSO access mismatch can make Railway automations fail before run/thread creation` — **Severity: High**. Railway-hosted Reborn instances create scheduled automations but fires fail before any run is attached. **Fix PR [#5003](https://github.com/nearai/ironclaw/pull/5003) exists** and was submitted today.

**High (workflow-breaking):**

- **[#4942](https://github.com/nearai/ironclaw/issues/4942)** — `[Reborn WebUI] Tool calls failed won't appear until re-fetch/reload` — Users cannot see failed GSuite tool calls without manual refresh. No fix PR linked.

- **[#4991](https://github.com/nearai/ironclaw/issues/4991)** — `WASM google-drive auth failures dead-end as operation_failed without refresh-retry` — Expired OAuth tokens cause a generic `operation_failed` instead of triggering an `AuthRequired` gate. No retry mechanism. No fix PR linked.

- **[#4981](https://github.com/nearai/ironclaw/issues/4981)** — `[Reborn] Dashboard status badges are confusing` — Status badges (MUTED, SIGNAL, INFO, SUCCESS) on automation dashboard appear unrelated to actual automation states. This is confusing for users trying to understand system health.

- **[#5004](https://github.com/nearai/ironclaw/issues/5004)** — `[Reborn] Automations Failure summary card is not actionable` — Shows failure count but no way to identify which automation, which run, when, or why it failed.

**Medium (UX degradation):**

- **[#4988](https://github.com/nearai/ironclaw/issues/4988)** — `[Reborn] Recent runs visualization is difficult to understand` — Execution history shown as colored dots with no legend or explanation.
- **[#5007](https://github.com/nearai/ironclaw/issues/5007)** — `[Reborn] Skills validation error does not clear after required fields are filled` — Form validation UX bug.
- **[#4977](https://github.com/nearai/ironclaw/issues/4977)** — `[Reborn WebUI] Approval-deny tool activity should stay visible and ordered` — Denied approvals remain displayed as `RUN` until refresh.
- **[#4972](https://github.com/nearai/ironclaw/issues/4972)** — `[Reborn] "New" button's font size is larger than others` — Minor UI inconsistency.
- **[#5006](https://github.com/nearai/ironclaw/issues/5006)** — `Skills Findings 06/15-06/21` — QA note: no search/filter on skills page, metadata formatting issues.

**Known fix PRs in flight:**
- [#5003](https://github.com/nearai/ironclaw/pull/5003) addresses #4992 (SSO automation failure)
- [#5001](https://github.com/nearai/ironclaw/pull/5001) addresses provider-output validation loops
- [#4998](https://github.com/nearai/ironclaw/pull/4998) surfaces approval after auth resume
- [#4953](https://github.com/nearai/ironclaw/pull/4953) gates triggered Slack OAuth URL on verified DM

## Feature Requests & Roadmap Signals

**Strong signals for next release:**

1. **Preview Deployments for PRs** ([#4881](https://github.com/nearai/ironclaw/issues/4881)) — Request for Vercel-like preview deployments to validate changes via clickable links. Parented under #4878. Likely to be implemented as CI infrastructure work accelerates.

2. **Engine V2 Quality Milestone 0 Complete** ([#2721](https://github.com/nearai/ironclaw/issues/2721), closed) — The multi-route execution design has been evaluated. Expect the "larger architecture track" decision from the team soon. If the go/no-go from [#2725](https://github.com/nearai/ironclaw/issues/2725) was positive, a significant architecture refactor may be imminent.

3. **LLM Usage Persistence for Engine V2** ([#4985](https://github.com/nearai/ironclaw/issues/4985)) — `GET /api/admin/usage` returns empty on Engine V2 deployments. Required for billing/admin visibility. Likely to land soon as admin tooling matures.

4. **NEAR AI Tool-Message Flattening Removal** ([#4983](https://github.com/nearai/ironclaw/issues/4983)) — Request to remove compatibility path that flattens OpenAI multi-turn tool history. Indicates confidence in NEAR AI cloud provider capability.

5. **WASM Google Drive Extraction Beyond 1 MB** ([#4999](https://github.com/nearai/ironclaw/issues/4999)) — After landing host-side text extraction (#4997), the 1 MB cap is the next bottleneck. Expect a follow-up PR for streaming/chunked extraction.

**Prediction:** The next release will likely include: SSO automation fix (#4992/#5003), provider-output validation relaxation (#5001), approval-after-auth-resume (#4998), OpenAI-compat vision (#4902), and the beginning of Engine V2 architecture work. The Reborn automations UX overhaul (visibility, management, failure explanation) appears to be a major focus area.

## User Feedback Summary

**Pain Points (multiple reports):**

- **Automation management is opaque** — Users cannot find which automation failed, why it failed, or manage automations (pause/resume/edit/delete) from the dashboard (#5004, #5005, #4981, #4980). The dashboard shows status badges that users find confusing and unrelated to real state.

- **Tool approval visibility is broken** — Failed tool calls are invisible until page refresh (#4942). Approval-denied actions remain displayed as "RUN" (#4977). Automation approval threads are hidden from conversation lists (#4987), making it impossible for users to approve pending actions on recurring automations (#4986).

- **OAuth/auth state is unreliable** — Google Calendar authorization is not reused across conversations (#4913). WASM Google Drive auth failures dead-end without refresh-retry (#4991). SSO access mismatches kill Railway automations silently (#4992).

- **Onboarding is minimal** — Empty automations page has no guidance on how to create automations (#4980). Dashboard status badges have no tooltips or explanations (#4981). Skills page has no search or filter for hundreds of system skills (#5006).

**Use Cases Exercised:**
- Local IronClaw Reborn dogfooding as a daily driver agent (#4879, #4692)
- Google Suite integration (Drive file extraction, Calendar, Strategy doc access via #4942)
- Scheduled GitHub monitoring automations (#4986)
- Railway-hosted Reborn with SSO (#4992)
- Slack-triggered automations with OAuth challenge (#4953)

**Satisfaction Signals:** The rapid closure of 20 issues and 15 PRs in 24 hours indicates the team is responsive to dogfooding feedback. Fixes for approval-gate denial (#4954), shell command visibility (#4858), and OAuth URL security (#4953) directly address user-reported issues.

**Dissatisfaction Signals:** The volume of UX issues (11 issues from a single QA cycle in 3 days) suggests the Reborn WebUI is still rough around the edges. Automation reliability issues (#4986, #4992) are blockers for any unattended use case.

## Backlog Watch

**Long-unanswered/Stale Issues:**

- **[#2721](https://github.com/nearai/ironclaw/issues/2721)** — Engine V2 quality epic — Now **closed** after 58 days. Decision on next architecture track is pending. This should be monitored for the go/no-go outcome from #2725.

- **[#2725](https://github.com/nearai/ironclaw/issues/2725)** — Milestone 0 evaluation — **Closed** alongside #2721. Acceptance criteria required an explicit go/no-go decision. The outcome is not documented in the issue body — this may need a follow-up decision post.

- **[#3890](https://github.com/nearai/ironclaw/pull/3890)** — Add Reborn multi-tenant isolation contract tests — Open since **May 22 (26 days)**. Core contributor, XS size, low risk. Multiple reviewers may be waiting for related infrastructure.

- **[#3947](https://github.com/nearai/ironclaw/pull/3947)** — Add Reborn event and scheduling parity coverage — Open since **May 23 (25 days)**. Core contributor, XS size, low risk. Similar to #3890 — these test-only PRs may be blocked on CI or reviewer bandwidth.

- **[#4518](https://github.com/nearai/ironclaw/pull/4518)** — Add Reborn extension lifecycle e2e coverage — Open since **June 6 (11 days)**. Core contributor, XS size. Extension tests may be waiting on extension system stabilization.

**Items needing maintainer attention:**

- **[#4692](https://github.com/nearai/ironclaw/issues/4692)** — Dogfooding findings (June 8-14) — Open, 0 comments from maintainers. This was the prior week's QA cycle; some reported issues may have been addressed but not linked.
- The **Engine V2 architecture decision** from #2725 — The issue is closed but the decision outcome isn't public. A follow-up communication or architecture RFC would help the community understand the roadmap direction.
- **[#4983](https://github.com/nearai/ironclaw/issues/4983)** — Remove NEAR AI tool-message flattening — No assignee or milestone. This could be a breaking change that needs planning for downstream consumers.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-17

## 1. Today's Overview
Activity is moderate, with **4 pull requests updated in the last 24 hours**, of which **3 were merged/closed** and **1 remains open**. A single open issue is active but stale (2+ months old). **No new releases are published today**, and there is no evidence of an upcoming major version. The project shows steady incremental progress focused on the Cowork module (task search, scroll UX) and Artifacts (preview cards, browser integration). However, the presence of an unresolved stale bug around shortcut validation (#1425) and the failed `scheduledTasks` fix (#1424) suggest some areas of technical debt remain.

## 2. Releases
**No new releases today.** The most recent referenced version in issue data is **LobsterAI v2026.4.1**. Users are encouraged to review the [Releases page](https://github.com/netease-youdao/LobsterAI/releases) for prior updates.

## 3. Project Progress
Three PRs were merged today, all authored by the core team:

| PR | Summary | Area |
|----|---------|------|
| [#2170](https://github.com/netease-youdao/LobsterAI/pull/2170) | **fix(cowork): search tasks from database** — Implements SQLite-backed search for Cowork tasks instead of filtering preloaded recent sessions. Preserves existing session list behavior (sidebar, pagination, shortcut slots) when no search query is provided. | Cowork, Main, Docs, Renderer |
| [#2169](https://github.com/netease-youdao/LobsterAI/pull/2169) | **feat(artifacts): 优化预览卡片与浏览器预览体验** — Unifies preview card styles, file-type display, dark-mode hover effects, and multi-file folding. Adds hover subtitle for HTML cards ("Open in Lobster Browser"). Refines browser open menu, external browser count limits, and deduplication logic. | Artifacts, Renderer, Docs, Main, Cowork |
| [#2168](https://github.com/netease-youdao/LobsterAI/pull/2168) | **feat(cowork): add scroll-to-bottom control** — Adds a compact floating button for cowork conversations with smooth scrolling, wheel passthrough, i18n labels, and click diagnostics. | Renderer, Cowork |

**Key advancement:**
- Cowork search moves from in-memory filtering to proper SQLite-backed querying, improving scalability and correctness when many sessions exist.

## 4. Community Hot Topics

| Issue/PR | Type | Comments | Status | Link |
|----------|------|----------|--------|------|
| #1425 — 快捷键重复无校验 | Issue (stale) | 1 comment | Open | [View](https://github.com/netease-youdao/LobsterAI/issues/1425) |
| #1424 — fix(scheduledTasks): Stop IPC handler returns `{ success: true }` but does nothing | PR (stale) | 0 comments | Open | [View](https://github.com/netease-youdao/LobsterAI/pull/1424) |

**Analysis**: Both items are over 2 months old with no maintainer response. #1425 reveals a UX gap — users can save duplicate keyboard shortcuts without validation, which undermines customisation reliability. #1424 describes a serious but silent bug where the "Stop" IPC handler for scheduled tasks reports success while tasks keep running. These low-activity items signal either low maintainer bandwidth or prioritization of feature work over bug fixes.

## 5. Bugs & Stability

No new bugs were filed in the last 24 hours. The following previously-reported issues remain unaddressed:

| Severity | Issue | Description | Status | Fix PR? |
|----------|-------|-------------|--------|---------|
| **Medium** | [#1425](https://github.com/netease-youdao/LobsterAI/issues/1425) | Shortcut duplicate validation missing — users can save conflicting keybindings without warning. | Open (stale, 74 days) | No |
| **High** | [#1424](https://github.com/netease-youdao/LobsterAI/pull/1424) | `scheduledTasks` Stop IPC handler is a no-op that always returns success; users are misled into thinking tasks have stopped when they continue running. This PR is itself the fix but has not been merged. | Open PR (74 days) | PR #1424 exists but unmerged |

**Recommendation**: PR #1424 should be prioritized for review and merge as it addresses a functional integrity issue that could lead to unexpected behavior in production.

## 6. Feature Requests & Roadmap Signals

- **Cowork task search from database** (PR #2170, merged): Indicates the team is investing in Cowork ergonomics — searching *all* tasks rather than just recent sessions — suggesting this feature will be more robust in the next release.
- **Artifacts preview experience** (PR #2169, merged): Improved preview cards, multilingual titles, and refined browser open behavior point toward richer cross-application sharing.
- **Scroll-to-bottom usability** (PR #2168, merged): A small but clear UX improvement for long Cowork conversations, likely user-requested.

**Prediction**: The next release (likely v2026.7.x) will include Cowork full-database search, enhanced artifact previews, and scroll controls. No breaking changes are foreseen.

## 7. User Feedback Summary

Little direct feedback from the community was captured in the last 24h. However, the un-addressed #1425 suggests a user pain point: configuring keyboard shortcuts without validation leads to frustration and reduced trust in the settings UI. The lack of error feedback in scheduled tasks (reported via #1424) may impact users relying on automation, especially those who stop tasks only to find them still active.

**Satisfaction signal**: Merged quality-of-life features (better search, scroll-to-bottom) show the team is listening to workflow friction.

## 8. Backlog Watch

Items requiring maintainer attention, all stale and uncommented for over 2 months:

| Issue | Age | Priority | Description |
|-------|-----|----------|-------------|
| [#1425](https://github.com/netease-youdao/LobsterAI/issues/1425) | 74 days | Medium | Shortcut duplicate validation missing |
| [#1424](https://github.com/netease-youdao/LobsterAI/pull/1424) | 74 days | High | Fix PR for silent scheduled task "Stop" failure — unmerged |

Both are critical for correctness and user trust. If combined monthly active users of LobsterAI exceed 1,000, these bugs affect a non-trivial portion of the user base. **Action required**: Engage on PR #1424 and triage issue #1425 into a milestone.

---

*Digest generated on 2026-06-17 from GitHub data.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

# TinyClaw Project Digest — 2026-06-17

## Today's Overview
The TinyClaw project shows very low activity in the last 24 hours, with zero new issues, zero releases, and only one open pull request updated. The single PR (#281) addresses Windows cross-platform compatibility for the CLI, indicating ongoing but narrow-scope maintenance. No merged work or resolved issues were recorded today, suggesting the project may be in a quiet phase or awaiting review cycles. Overall project health appears stable but with minimal forward momentum.

## Releases
None — no new releases were published in the last 24 hours.

## Project Progress
No pull requests were merged or closed today. The only PR activity is an open fix:

- **[#281 [OPEN] fix: Windows cross-platform support in CLI](https://github.com/TinyAGI/tinyagi/pull/281)** — Author: mperkins0155. Created and updated on 2026-06-16. This PR targets three Windows-specific bugs that prevent the `tinyagi` CLI from running natively on Windows (non-WSL), including a critical `MODULE_NOT_FOUND` error caused by doubled drive letters in path resolution. No comments or reactions yet. This remains unmerged.

## Community Hot Topics
There are no highly active discussions today. The only open PR (#281) has zero comments and zero reactions, indicating either low community engagement or recent introduction. No issues were updated or commented on in the last 24 hours.

## Bugs & Stability
One bug report is addressed through the open PR #281, ranked as **high severity** (prevents the CLI from running on Windows):

1. **Doubled drive letter → `MODULE_NOT_FOUND`** (PR #281): On Windows, `new URL('.', import.meta.url).pathname` returns `/C:/Users/...`, which when passed to `path.resolve` creates a malformed path like `C:C:\...`, causing Node to fail module resolution.
2. **(Implied) Two additional Windows-only bugs** mentioned in the PR summary but not detailed individually.

**Status:** No fix has been merged; the PR awaits review.

## Feature Requests & Roadmap Signals
No feature requests were submitted or discussed in the last 24 hours. The single active PR is a bug fix, not a new feature. No roadmap signals are discernible from current data.

## User Feedback Summary
No user feedback, comments, or reactions were recorded in the last 24 hours. The lack of engagement could indicate either satisfied users or limited awareness. The PR #281 suggests an untapped Windows user base that may face installation friction.

## Backlog Watch
No long-unanswered issues or PRs were identified today. The only open item (PR #281) is recent (June 16) and has not yet received maintainer attention. It should be monitored for timely review to avoid drift.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest — 2026-06-17**

**1. Today's Overview**
Moltis shows moderate daily activity with four issues updated in the last 24 hours and two open pull requests progressing. One bug was closed quickly today, suggesting responsive maintainer triage. No new releases were cut, but development focus is on configurability and live-mode stability. The project maintains a healthy balance between feature requests and bug reports, all filed by a single repeat contributor (khimaros), indicating an engaged power-user community.

**2. Releases**
*None.* No new releases were published on or before this digest date.

**3. Project Progress**
No pull requests were merged or closed in the last 24 hours. Two open PRs continue with recent updates:
- **#1124** (Add context command support for chat turns) – Allows injecting runtime-generated context before each chat turn. Updated Jun 16.
- **#1125** (Support model and effort selection for external agents) – Adds per-agent model/effort configuration and UI support. Updated Jun 16.

Both are authored by **gptme-thomas** and represent significant config-layer enhancements that remain under review.

**4. Community Hot Topics**
Only one issue generated discussion in the period:
- **#1126** (Feature: allow to configure format of TTS output) – 2 comments, opened Jun 16. The author wants to control output format (e.g., WAV vs MP3, sample rate). This suggests growing usage in audio-pipeline deployments where file format matters for downstream processing.  
  [GitHub Issue #1126](https://github.com/moltis-org/moltis/issues/1126)

No other issues or PRs attracted comments or reactions today.

**5. Bugs & Stability**
Two bugs were reported; one was promptly closed:
- **#1128 [Closed]** – Transcription errors with self-hosted whisper.cpp. Fixed/closed within hours of creation. Low severity at this point.  
  [GitHub Issue #1128](https://github.com/moltis-org/moltis/issues/1128)
- **#1129 [Open]** – Lack of echo cancellation causes agent to retrigger itself in live mode. **High severity** – this directly impacts real-time voice interaction usability. No associated fix PR yet.  
  [GitHub Issue #1129](https://github.com/moltis-org/moltis/issues/1129)

**6. Feature Requests & Roadmap Signals**
Three feature/enhancement requests emerged today, all from user **khimaros**:
- **#1126** – TTS output format configuration (likely to land within 1–2 releases given existing audio modularity)
- **#1127** – RPC timeout configuration (essential for production reliability; high priority signal)
- Context command support (#1124) and external agent model/effort selection (#1125) are already in PRs, so these are likely next-version candidates.

The pattern suggests the community is pushing Moltis toward production-grade configurability and resilience.

**7. User Feedback Summary**
- **Pain Points:** Lack of echo cancellation in live mode (#1129) degrades the voice-agent experience; transcription errors with self-hosted whisper.cpp (#1128) show friction in offline/self-hosted setups.
- **Use Cases:** Real-time voice interaction, self-hosted speech pipelines, and automated chat turn injection.
- **Satisfaction:** The rapid closure of #1128 indicates responsive maintainers, which likely contributes to user satisfaction. However, the echo cancellation bug is unresolved and could cause frustration for live-mode adopters.

**8. Backlog Watch**
No long-unanswered issues or PRs are currently visible. The oldest open items updated in the last 24h are from Jun 15–17, so the project maintainers are keeping up with recent traffic. No flagged items require urgent maintainer attention beyond normal review cadence.

*End of digest.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the structured project digest for **CoPaw (QwenPaw)** based on the GitHub data for **2026-06-17**.

---

## CoPaw Project Digest — 2026-06-17

### 1. Today's Overview
The QwenPaw project remains highly active, with 43 issues and 39 PRs updated in the last 24 hours, alongside the release of a new beta patch. Activity is dominated by the community reporting critical stability bugs (SIGSEGV crashes, process freezes) and maintainers pushing fixes, particularly for the Desktop (Tauri) client and memory subsystems. The release of **v1.1.12-beta.1** focuses on security hardening and CI reliability. The community is also highly engaged in feature development, with multiple first-time contributors submitting translations, UI improvements, and new context compression integrations. Overall, the project is in a **high-velocity maintenance and feature-absorption phase**.

### 2. Releases
- **New Version:** `v1.1.12-beta.1`
- **Key Changes:**
    - **Security:** `fix(security): isolate keychain master key per install` — Improves credential isolation across different QwenPaw installations.
    - **Desktop (Tauri):** `fix(desktop): harden Tauri Windows CI against crates.io fetch failures` — Increases build reliability for Windows users.
    - **Refactoring:** `refactor(cons...` (truncated in data, likely a significant code refactor).
- **Breaking Changes:** None explicitly noted in the changelog. This is classified as a beta release.
- **Migration Notes:** Users are advised to upgrade via `uv tool install qwenpaw==1.1.12-beta.1` or the relevant package manager.

### 3. Project Progress
Today saw 21 PRs merged or closed. Notable advancements include:
- **Internationalization (i18n):** Merged PR [#5175](https://github.com/agentscope-ai/QwenPaw/pull/5175) adding **Vietnamese (vi)** interface language support.
- **Desktop UI/UX:** Merged PR [#5222](https://github.com/agentscope-ai/QwenPaw/pull/5222) adding a "simple mode" with a flat navigation bar and sorted session lists.
- **Console Enhancements:**
    - Merged PR [#5178](https://github.com/agentscope-ai/QwenPaw/pull/5178) adding session filtering by title.
    - Merged PR [#5248](https://github.com/agentscope-ai/QwenPaw/pull/5248) adding OSC 8 hyperlink support for clickable links in the terminal.
- **Performance & Bug Fixes:**
    - Merged PR [#5240](https://github.com/agentscope-ai/QwenPaw/pull/5240) removing deep copies in agent config caching to reduce memory usage and improve load times.
    - Merged PR [#5226](https://github.com/agentscope-ai/QwenPaw/pull/5226) fixing Gemini API 400 errors caused by invalid tool schemas.
    - Merged PR [#5201](https://github.com/agentscope-ai/QwenPaw/pull/5201) adding integration tests for cron execution and tool APIs.

### 4. Community Hot Topics
The most engaging discussions revolve around **core stability and long-context degradation**:
- **[Issue #5218](https://github.com/agentscope-ai/QwenPaw/issues/5218):** **Process Freeze on Context Compaction** (14 comments). Sub-agent context compression causing the entire app to freeze, requiring manual restart. This is the hottest issue, with a related fix PR [#5242](https://github.com/agentscope-ai/QwenPaw/pull/5242) submitted to add timeout protection.
- **[Issue #5063](https://github.com/agentscope-ai/QwenPaw/issues/5063):** **Integrate Headroom Compression** (6 comments). A feature request to use the local-first Headroom SDK to reduce token consumption by 60-95%. A corresponding PR [#5244](https://github.com/agentscope-ai/QwenPaw/pull/5244) was opened today.
- **[Issue #4625](https://github.com/agentscope-ai/QwenPaw/issues/4625):** **MiniMax-M2.5 XML Incompatibility** (6 comments). The model returns thinking steps as XML, breaking tool execution.
- **[Issue #5161](https://github.com/agentscope-ai/QwenPaw/issues/5161):** **Long Conversation Freeze** (5 comments). Users report QwenPaw stops responding entirely after long dialogues.

**Underlying Need:** There is a clear and urgent user demand for **robust long-context management**. Users are hitting stability limits on both the client (freezes) and API (token waste), indicating the current context compaction and memory systems are a major bottleneck.

### 5. Bugs & Stability
Stability is the dominant theme today, with several critical and high-severity bugs reported.

- **Critical:**
    - **[Issue #5209](https://github.com/agentscope-ai/QwenPaw/issues/5209):** **macOS SIGSEGV Crash Loop (Tauri Desktop).** Process crashes every minute on Apple Silicon. **Fix in progress:** PR [#5238](https://github.com/agentscope-ai/QwenPaw/pull/5238) is open to repair Tauri plugin startup.
    - **[Issue #5243](https://github.com/agentscope-ai/QwenPaw/issues/5243):** **ChromaDB SIGSEGV Crash.** 48 crashes in 2 days, traced to null pointer in Rust bindings during memory operations. **Fix in progress:** PR [#5246](https://github.com/agentscope-ai/QwenPaw/pull/5246) proposes a configuration-based workaround (disabling vector operations).
    - **[Issue #5218](https://github.com/agentscope-ai/QwenPaw/issues/5218):** **Process Freeze on Context Compaction.** **Fix in progress:** PR [#5242](https://github.com/agentscope-ai/QwenPaw/pull/5242).

- **High:**
    - **[Issue #5253](https://github.com/agentscope-ai/QwenPaw/issues/5253):** **Custom Channel Listener Dies After Save.** Requires re-saving the channel config to restart listening.
    - **[Issue #5235](https://github.com/agentscope-ai/QwenPaw/issues/5235):** **Cron Tasks Not Executing.** Tasks remain in "pending" state past their scheduled time.
    - **[Issue #5206](https://github.com/agentscope-ai/QwenPaw/issues/5206):** **Agent Config Cache Pollution.** `load_agent_config()` returns references, not copies, causing user settings to be silently overwritten. **Fix included** in merged PR [#5240](https://github.com/agentscope-ai/QwenPaw/pull/5240).

- **Medium/Low:**
    - **[Issue #5208](https://github.com/agentscope-ai/QwenPaw/issues/5208):** Message count mismatch with "reasoning" block types.
    - **[Issue #5207](https://github.com/agentscope-ai/QwenPaw/issues/5207):** Inconsistent path resolution between `read_file` and `execute_shell_command`.
    - **[Issue #5214](https://github.com/agentscope-ai/QwenPaw/issues/5214):** DingTalk Stream channel silently fails after system sleep.

### 6. Feature Requests & Roadmap Signals
The community is pushing QwenPaw towards more **autonomous, efficient, and enterprise-friendly operation**.
- **Agent Self-Evolution ([#5205](https://github.com/agentscope-ai/QwenPaw/issues/5205)):** A request for agents to learn from mistakes and auto-correct behavior, not just read static rules. High potential for v1.2.
- **Headroom Compression ([#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063)):** A concrete PR [#5244](https://github.com/agentscope-ai/QwenPaw/pull/5244) has been submitted. Likely to be merged in an upcoming minor release as an optional backend.
- **Silent Cron Mode ([#5251](https://github.com/agentscope-ai/QwenPaw/pull/5251)):** A PR to prevent cron agent output from flooding the user's main chat. This addresses a major UX flaw for automation users.
- **DataPaw Plugin ([#4622](https://github.com/agentscope-ai/QwenPaw/issues/4622)):** An ambitious data-analysis plugin with 12 BI skills remains under review, signaling a push into analytical use cases.
- **WeCom Image+Text Support ([#5217](https://github.com/agentscope-ai/QwenPaw/issues/5217)):** Request to support combined image+text messages for enterprise WeChat (WeCom).

**Prediction for next version (v1.1.13 / v1.2.0):**
The fixes for the **Tauri crash loop**, **ChromaDB crashes**, and **context compaction freezes** will almost certainly be hot-patched. The **Headroom integration** and **Silent Cron mode** are strong candidates for inclusion.

### 7. User Feedback Summary
- **Major Pain Points:**
    1.  **Instability/Lockups:** Users on macOS and Docker are experiencing frequent crashes (SIGSEGV) and process freezes, making the app unusable for long sessions.
    2.  **Context Management Failure:** Long conversations degrade to a halt. "QwenPaw stops responding after long conversation" is repeated by multiple users.
    3.  **Channel Reliability:** Channels (DingTalk, WeCom) fail silently after network interruptions or system sleep, requiring manual restarts.
    4.  **Configuration Corruption:** Users are frustrated by config files being corrupted silently (e.g., `loop_config.json`, `agent.json`).
    5.  **Windows File Path Issues:** Duplicated session IDs in filenames cause Windows MAX_PATH errors.

- **Satisfaction Signals:**
    - High engagement from first-time contributors (3 PRs today) indicates a welcoming community and high enthusiasm.
    - Users express appreciation for the HelloFeishu CardKit channel integration, despite noting performance issues.
    - Feature requests are well-structured and constructive, suggesting the user base is technically sophisticated and invested in the project's direction.

### 8. Backlog Watch
- **[Issue #4193](https://github.com/agentscope-ai/QwenPaw/issues/4193):** (1.1.6 upgrade lost `gtp-img` plugin) — Closed today, but the underlying issue of plugin discovery after upgrades is a recurring concern.
- **[Issue #4622](https://github.com/agentscope-ai/QwenPaw/pull/4622):** **DataPaw Plugin** — This PR has been open for nearly a month (since May 22). It is a large feature and is labeled "Under Review." It requires maintainer attention to either merge or provide feedback.
- **[Issue #5088](https://github.com/agentscope-ai/QwenPaw/pull/5088):** **Governance & Sandbox Interface** — A "Breaking Change" PR that has been open for a week with no comments. This defines the future of plugin security and needs community/maintainer discussion.
- **[Issue #5158](https://github.com/agentscope-ai/QwenPaw/pull/5158):** **User Input Queue** — Open for 5 days with no comments. This could be a highly valuable feature for managing concurrent user interactions.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest – 2026-06-17

## Today's Overview
The ZeptoClaw project maintained a low-activity profile on this date, with no new issues, releases, or merged PRs recorded in the last 24 hours. The sole activity was a single open pull request (#630) from Dependabot, performing a routine Docker base image update for Debian. This indicates a period of relative stability, with no active bug reports or feature development visible in the immediate pipeline. Project pulse appears steady but quiet, with no signs of critical maintenance or user engagement events.

## Releases
No new releases were published today. The latest release remains unchanged from prior dates.

## Project Progress
No pull requests were merged or closed today. There is no feature advancement, bug fix, or code merge to report from the last 24 hours.

## Community Hot Topics
The only active item drawing attention today is a routine dependency update:
- **[#630 – chore(deps): bump debian from `b6e2a15` to `4e401d9`](https://github.com/qhkm/zeptoclaw/pull/630)** (Open, by dependabot[bot])
  - **Created/Updated:** 2026-06-16 → 2026-06-16
  - **Comments:** 0 | **Reactions:** 0
  - This is an automated Dependabot PR updating the base Debian image tag in the Dockerfile from `trixie-slim` revision `b6e2a15` to `4e401d9`. It carries a compatibility score badge. No community discussion has occurred, and the PR is still open awaiting review or merge.

No other issues or PRs generated activity. There are no hot topics or user discussions to analyze further.

## Bugs & Stability
No bugs, crashes, regressions, or stability concerns were reported in the last 24 hours. The zero-issue count across all statuses (open/active/closed) confirms the absence of any defect reporting. No fix PRs exist for today.

## Feature Requests & Roadmap Signals
No feature requests or roadmap signals were submitted today. The lack of feature-related issues or discussion makes it impossible to predict content for the next version beyond routine maintenance.

## User Feedback Summary
No user feedback, pain points, use cases, or satisfaction/dissatisfaction signals were captured in the last 24 hours. The project’s community channels (GitHub Issues) show zero user engagement for this period.

## Backlog Watch
There are no long-unanswered issues or PRs requiring maintainer attention. The only open item (#630, Dependabot Docker update) is routine and not considered urgent or backlogged. The maintainer may wish to review and merge #630 at their earliest convenience to keep the Docker base image current.

---

**Assessment:** Project health is stable but idle. The absence of issues, PR merges, and community discussion suggests either a mature codebase with low ongoing maintenance needs, or a temporary lull in development activity. No immediate risks or bottlenecks are apparent.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-17

## 1. Today's Overview

ZeroClaw is in a high-activity phase with 49 issues and 50 pull requests updated in the last 24 hours, indicating a very active development cycle as the project stabilizes after the v0.8.0 release. The community is reporting significant regressions in prebuilt binaries (missing Slack/Discord features), gaps in documentation for new users, and several runtime tool-looping bugs that suggest the 0.8.x line is still maturing. The maintainer team is responding quickly — 11 issues were closed and 21 PRs were merged/closed today, including fixes for cron session targeting, CLI UTF-8 handling, Telegram API base URLs, and IRC mention parsing. No new releases were cut today.

## 2. Releases

No new releases today. The project remains on v0.8.0, with v0.8.1 integration work tracked in issue #6970 and v0.8.3 MCP dashboard work tracked in #7320.

## 3. Project Progress

**21 PRs were merged or closed today**, reflecting strong momentum across multiple subsystems:

- **Runtime fixes**: `session_target=main` cron jobs now correctly reuse the main session (PR #7731 by Pick-cat); heartbeat history query returns empty for zero-limit requests (PR #7721 by Alix-007); anti-narration system prompt now respects `show_tool_calls` config (PR #7722 by dwc1997)
- **Channel fixes**: Telegram channel now supports custom `api_base_url` with validation (PR #7697 by Alix-007, closes #6807); IRC mention detection now uses token boundaries instead of substring matching (PR #7710); `/clear` command added to Telegram for memory reset (PR #7671); CLI channel fixes UTF-8 backspace handling for CJK characters (PR #7672, closes #6995)
- **CLI/Diagnostics**: `zeroclaw status` output routed through Fluent i18n (PR #7499 by silas-qiao); `models list` and `doctor` commands now show configured models plus `--check` flag (PR #7450 by Nillth)
- **Configuration**: Legacy typed scalar strings now trimmed before validation (PR #7714 by Alix-007); 8 end-to-end tests added for config comment writer (PR #7766 by Pick-cat)
- **Docs/Infrastructure**: Generated reference docs synced with current CLI commands (PR #7711); squash-merge skill extended with CI checks (PR #7752)

## 4. Community Hot Topics

The most active discussions today center on governance, infrastructure hardening, and critical runtime issues:

- **[#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)** (11 comments) — Audacity88's governance RFC proposing automated issue routing, now in accepted rollout status. This is the project's attempt to scale its triage process as activity explodes post-0.8.0.
- **[#6856 — [Bug]: show_tool_calls is missing from [channel]](https://github.com/zeroclaw-labs/zeroclaw/issues/6856)** (5 comments, now closed) — A configuration regression in schema v3 that hid tool call details from channel responses. The fix (PR #7722) was merged today.
- **[#6970 — v0.8.1 integration/channel/provider/tool queue and history](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)** (3 comments) — Operational tracker for the next minor release, suggesting the team is prioritizing integration stability over new features.
- **[#7759 — Decouple gateway WebSocket lifetime from agent turn lifecycle](https://github.com/zeroclaw-labs/zeroclaw/issues/7759)** (2 comments, priority p1) — A request to support background turns and reconnection, indicating real-world deployment pain with the current WebSocket architecture.
- **[#7756 — Native/MCP tools unavailable on OpenAI Responses/reasoning and Anthropic turns](https://github.com/zeroclaw-labs/zeroclaw/issues/7756)** (1 comment, priority p1) — A critical workflow-blocking bug where MCP tools aren't passed to the model depending on provider, suggesting a provider abstraction gap in v0.8.0.

**Underlying need**: The community is stretching ZeroClaw's multi-provider architecture in ways the v0.8.0 release didn't anticipate — MCP tool routing per provider, WebSocket resilience, and configuration UX are emerging as pain points from real deployments.

## 5. Bugs & Stability

**Today's new bug reports (ranked by severity):**

| Severity | Issue | Status |
|----------|-------|--------|
| **S1 (workflow blocked)** | [#7787](https://github.com/zeroclaw-labs/zeroclaw/issues/7787) — Prebuilt v0.8.0 binaries ship without Slack/Discord features (regression from 0.7.x) | Open, no fix PR |
| **S1 (workflow blocked)** | [#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756) — MCP tools unavailable on OpenAI/Anthropic turns | Open, no fix PR |
| **S1 (workflow blocked)** | [#7804](https://github.com/zeroclaw-labs/zeroclaw/issues/7804) — Code history can send non-alternating Anthropic messages (provider 400) | Open, no fix PR |
| **S2 (degraded behavior)** | [#7815](https://github.com/zeroclaw-labs/zeroclaw/issues/7815) — ZeroCode Config doesn't show which config source is being edited | Open, no fix PR |
| **S2 (degraded behavior)** | [#7809](https://github.com/zeroclaw-labs/zeroclaw/issues/7809) — Channel turns ignore runtime-profile strict/parallel tool flags | Open, no fix PR |
| **S2 (degraded behavior)** | [#7820](https://github.com/zeroclaw-labs/zeroclaw/issues/7820) — Zeroclaw repeats identical shell approval loops before bounding | Open, no fix PR |
| **S2 (degraded behavior)** | [#7799](https://github.com/zeroclaw-labs/zeroclaw/issues/7799) — Resumed Code sessions reopen with blank transcript | Open, no fix PR |
| **S2 (degraded behavior)** | [#7810](https://github.com/zeroclaw-labs/zeroclaw/issues/7810) — git_operations gives no recovery hint outside a repository | Open, no fix PR |
| **S2 (degraded behavior)** | [#7800](https://github.com/zeroclaw-labs/zeroclaw/issues/7800) — ZeroCode keybindings misleading on macOS | Open, no fix PR |
| **S3 (minor)** | [#7805](https://github.com/zeroclaw-labs/zeroclaw/issues/7805) — Cancelled turns show queue-paused hint with empty queue | Open, no fix PR |

**Fixed today**: The Slack/Discord regression (#7787) has a related discussion but no fixing PR yet. The `show_tool_calls` bug (#6856) was fixed via PR #7722. The Telegram API endpoint issue (#6807) was fixed via PR #7697. The UTF-8 backspace bug (#6995) was fixed via PR #7672. The cron session_target bug (#6648) was fixed via PR #7731.

**Worst regression**: [#7787](https://github.com/zeroclaw-labs/zeroclaw/issues/7787) — prebuilt v0.8.0 binaries shipped without Slack/Discord channel features that worked in v0.7.x. This is a build configuration regression that blocks all Slack/Discord users who download binaries rather than building from source.

## 6. Feature Requests & Roadmap Signals

**Likely for v0.8.1** (tracked in #6970):
- **Per-agent opt-in Dream Mode** (issue #7794, PR #7797 by JordanTheJet) — Currently in-progress with a large PR implementing `[agents.<alias>.dream_mode]` config block, query surfaces, and chat `/dream` command. This is the most advanced feature actively merging.
- **Expose session ID to shell tools** (PR #7813 by RyanHoldren) — Adds `ZEROCLAW_SESSION_ID` env var to shell tool executions, a small but impactful improvement for users scripting tool behavior.
- **Gateway WebSocket decoupling** (issue #7759) — Priority p1, with demonstrated demand from production users needing background turns and reconnection.

**Pipeline signals**:
- [#7762](https://github.com/zeroclaw-labs/zeroclaw/issues/7762) — Request for cron documentation and per-cron model selection (cheap models for low-priority tasks). This reflects a maturing user base optimizing operational costs.
- [#7795](https://github.com/zeroclaw-labs/zeroclaw/issues/7795) — Telegram `static_voice_peers` caches config data on channel handle, violating single-source-of-truth. A design debt issue the maintainer team will likely refactor soon.

**Emerging roadmap theme**: The v0.8.3 tracker (#7320) signals that MCP dashboard, web surfaces, and plugin management are the next major horizon after the current integration stabilization push.

## 7. User Feedback Summary

**Positive signals**:
- Multi-provider support is being actively tested — users are running Slack-connected coding agents with shell tools (#7143, now closed/fixed), Telegram custom API endpoints (#6807, now fixed), and various model backends including GLM-5.1 (#6643) and Ollama.
- The Rust-based runtime is praised as "much lighter on resources than many other agent systems" (#7143) — this is a key differentiator worth highlighting.

**Pain points**:
- **Documentation crisis**: Issue #7758 titled "It doesn't matter how good the code is if the documentation is crap" (S1 severity, now closed but the underlying problem remains) and #7762 (cron docs missing) reflect a systemic documentation gap. The quickstart guide is reportedly insufficient to write a working config file.
- **Prebuilt binary regression**: Slack/Discord users who don't build from source are blocked on v0.8.0 (#7787), creating a trust issue with the release pipeline.
- **Tool looping**: Two separate users report agents getting stuck in tool-call loops — #7143 (shell discovery commands, fixed) and #7820 (identical shell approval loops, open today). This pattern suggests a flaw in tool iteration bounding or result deduplication.
- **ZeroCode UX friction**: Multiple bugs filed by Audacity88 today (#7800, #7803, #7805, #7814, #7815) suggest the TUI config/chat interface, while ambitious, has rough edges that frustrate power users.

## 8. Backlog Watch

**Long-standing important issues needing maintainer attention:**

- **[#5266 — No pairing code shown when running gateway start on alternate port](https://github.com/zeroclaw-labs/zeroclaw/issues/5266)** (created Apr 3, 2 comments, priority p1) — Open for 75 days. A security/onboarding issue that blocks users who test on non-default ports. The fix should be straightforward (print the pairing code), but it's been sitting with no assignee.
- **[#6643 — Thoughts merge into final message using GLM-5.1](https://github.com/zeroclaw-labs/zeroclaw/issues/6643)** (created May 13, 1 comment, priority p2) — Open for 35 days. A provider-specific regression where model thought content leaks into responses. The user explicitly requested re-opening after issue #5285 was closed, suggesting the fix was incomplete.
- **[#7675 — RFC: Hardened CI pipeline](https://github.com/zeroclaw-labs/zeroclaw/issues/7675)** (created Jun 15, 2 comments, needs-maintainer-review) — A detailed RFC for supply-chain security scanning, signed attestations, and SBOM generation. Given the prebuilt binary regression (#7787) today, this infrastructure work may gain urgency.

**PRs that stalled**:
- No PRs appear to have been open for more than 5 days without activity or closure — the maintainer team is keeping the merge queue moving quickly, suggesting good responsiveness despite the documentation gap.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*