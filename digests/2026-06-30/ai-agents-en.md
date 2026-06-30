# OpenClaw Ecosystem Digest 2026-06-30

> Issues: 404 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-30 02:01 UTC

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

Here is the OpenClaw project digest for **2026-06-30**.

---

## OpenClaw Project Digest – 2026-06-30

### 1. Today's Overview

OpenClaw is experiencing a period of **very high community engagement** but **moderate development churn**. With **404 issues** and **500 PRs** updated in the last 24 hours, the project is drowning in activity, with a significant backlog of open work (340 open issues, 446 open PRs). The closure rate remains low relative to activity, suggesting a **formation of a bottleneck** in maintainer review and merge capacity. While community contributors are actively submitting fixes, the sheer volume of "clawsweeper:needs-maintainer-review" tags indicates that the core team is struggling to keep pace with triage. No new releases were published today.

### 2. Releases

**None.** No new versions of OpenClaw were released today.

### 3. Project Progress

Despite high open counts, several critical fixes were merged or closed today, indicating movement on high-priority bugs:

- **Merged/Closed PRs (54):** 
    - **Security & Stability:** Fixed unhandled `SyntaxError` crashes caused by malformed JSON responses in the **Slack relay** (`#97976`) and **Discord API** (`#97889`).
    - **TUI Fixes:** A fix for slash commands (`/status`, `/compact`) in Terminal UI local mode was merged (`#97288`), closing a long-standing bug where commands were treated as messages.
    - **Message Delivery:** A fix was merged to filter out short trailing acknowledgments (e.g., "OK", "Done") that follow tool sends, preventing confusing double-replies in chat interfaces (`#96763`).
    - **Telegram Compatibility:** A fix was closed to gracefully fall back to `sendMessage` when the newer `sendRichMessage` API is unsupported by the client (`#95626`).

### 4. Community Hot Topics

The most heated discussions and highest-demand items reveal deep concerns about **session reliability, silent failures, and cross-platform parity**.

- **🥇 #75: Linux/Windows Clawdbot Apps** (110 comments, 81 👍)
    - **Link:** `openclaw/openclaw Issue #75`
    - **Analysis:** This is the single most requested feature in the project history. Users on Windows and Linux feel like second-class citizens, lacking native desktop app parity with macOS and iOS. The sheer volume of engagement (open for over 6 months) signals severe user frustration and a direct threat to user acquisition on those platforms.
- **🥈 #79077: Support for Telegram Bot-to-Bot & Guest-Bot Modes** (8 comments, 8 👍)
    - **Link:** `openclaw/openclaw Issue #79077`
    - **Analysis:** The community is eager to leverage Telegram's new platform features (released May 7). The demand is for inter-agent communication and guest access, pointing to a desire for multi-user or network-of-agents use cases.
- **🥉 #94518: DeepSeek Cache Hit Rate <10% After Upgrade** (6 comments, 8 👍)
    - **Link:** `openclaw/openclaw Issue #94518`
    - **Analysis:** A high-impact regression causing severe cost increases for DeepSeek users. The "boundary-aware caching" feature introduced in a recent release appears to have broken prefix matching, destroying the primary value proposition (low cost) of running DeepSeek models.

### 5. Bugs & Stability

The project is facing severe stability issues, many related to session management and silent failures. Reported today (or updated today with high priority):

- **[CRITICAL] Session Write-Lock Timeouts (#86538):** Open issue classified as `🦞 diamond lobster`. Subagent delivery lanes are being blocked by write-lock timeouts, leading to undiagnosed delivery failures. No immediate fix PR.
- **[CRITICAL] Empty-Error-Retry Blocked (#97877):** Filed today. Transient 5xx errors after tool use become terminal failures because the retry logic is blocked by a `hadPotentialSideEffects` guard. **Fix exists** (`#97966`).
- **[HIGH] DeepSeek Cache Hit Rate Collapse (#94518):** Regression causing 10x cost increases for DeepSeek users. No fix PR.
- **[HIGH] Web UI Response Delivery Delayed (#83532):** Users on Safari must manually refresh the page to see assistant responses. Represents a significant UX failure for the web interface.
- **[MEDIUM] CDP Auth Failure (#97972):** Fix submitted today for browser CDP authentication failing with percent-encoded credentials. **Fix exists** (`#97972`).
- **[MEDIUM] Unhandled JSON.parse Crashes (#97973, #97978):** Multiple fixes submitted today to wrap `JSON.parse` calls in try/catch blocks across Matrix, Slack, and Discord integrations, preventing crashes on malformed responses. **Fixes exist**.

### 6. Feature Requests & Roadmap Signals

Based on the "enhancement" tagged issues and community demand, the following features are likely candidates for the next minor release:

- **High Likelihood (Roadmap/MVP):**
    - **Phase 5 JSONL Session-Replay Harness (#80176):** Part of the Codex×Pi parity project, this testing infrastructure is critical for quality assurance.
    - **Skill Author Setup Hooks (#80213):** A clear UX gap for skill developers.
    - **Plugin SDK for Installed Skill Workflows (#81913):** Essential for the plugin ecosystem to mature.
- **Medium Likelihood (Based on Demand):**
    - **i18n for Slash Command Descriptions (#79458):** A low-friction feature that would improve accessibility for non-English users.
    - **Linear Persistent Workspace Mode for Blind Users (#82450):** A targeted accessibility feature with strong user advocacy.
- **Speculative:**
    - **Telegram Bot-to-Bot / Guest-Bot support (#79077):** Given the demand, a POC might appear in a beta channel, but full support is complex.

### 7. User Feedback Summary

- **Pain Points:**
    - **Silent Failures:** The community is deeply frustrated by "silent drops" where Telegram messages, Discord replies, or sub-agent outputs vanish without logs or error messages. (e.g., #80520, #80700, #77642).
    - **Regression Anxiety:** Multiple reports highlight that recent updates (e.g., 2026.5.7, 2026.5.12) introduce regressions in core features like Discord replies, Gmail sending, and model provider discovery. Users fear upgrading (#81484, #81934, #94518).
    - **Latency Asymmetry:** Non-default agents incur a 10-17 second startup latency overhead compared to the main agent, making multi-agent setups feel sluggish (#80607).
- **Positive Use Cases:**
    - One blind user (#82450) describes OpenClaw as "one of the most powerful AI work interfaces I have ever used," citing daily workflows for video production, browsing, and social media.
    - Users are actively building custom plugin providers (#95500) and skill ecosystems (#80213, #81913), demonstrating a strong desire for extensibility.

### 8. Backlog Watch

Several important items have been languishing for weeks or months without maintainer action.

- **#75: Linux/Windows Clawdbot Apps**: Open since January 1, 2026. The most-upvoted issue in the project. The `help wanted` label is appropriate, but the lack of a clear roadmap commitment is a growing risk.
- **#12581: Session Prune Lifecycle Event (PR):** Open since February 9, 2026. The `stale` label is present, and it awaits author updates. This feature is critical for observability.
- **#81061: `before_route_inbound_message` Hook:** Open since May 12, 2026. Marked `stale` but has a linked open PR. This is a fundamental architectural feature for channel bridging.
- **#82450: Linear Workspace Mode for Blind Users (Accessibility):** Open since May 16, 2026. No maintainer response beyond labeling. This is a critical accessibility gap.
- **#81960: Multi-Provider Onboarding:** Open since May 14, 2026. A significant UX friction point for new users, yet no maintainer has engaged.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Data Snapshot: 2026-06-30**

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing an explosive growth phase, characterized by high community engagement, rapid iteration cycles, and a pronounced bottleneck in maintainer review capacity. Projects are converging on a shared architectural pattern—multi-channel chat backends, plugin/skill ecosystems, and model provider abstraction—while diverging in target use cases from developer productivity to enterprise automation. A clear "quality vs. velocity" tension is emerging: the most active projects (OpenClaw, Hermes Agent, IronClaw) are drowning in PR backlogs (400-500 open items) yet still shipping critical fixes daily, while smaller projects (NanoBot, ZeroClaw) maintain healthier review ratios by limiting scope. Security hardening, cost optimization (caching, token reduction), and cross-platform reliability are the dominant themes across all active projects.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Open Issues | Open PRs | Release Today | Health Signal |
|---------|---------------------|-------------------|-------------|----------|---------------|---------------|
| **OpenClaw** | 404 | 500 | 340 | 446 | ❌ | **Overloaded** — drowning in activity, low closure rate |
| **Hermes Agent** | 50 | 50 | 46 | 43 | ❌ | **High churn** — heavy development phase, no release |
| **IronClaw** | 14 | 50 | — | 31 | ❌ | **Intense stabilization** — 19 merges, QA-driven |
| **CoPaw** | 29 | 50 | 20 | 32 | ❌ | **High activity** — post-beta release push |
| **ZeroClaw** | 50 | 40 | 50 | 40 | ❌ | **Sprint mode** — v0.8.3 hardening |
| **LobsterAI** | 11 | 40 | — | — | ✅ v2026.6.29 | **Release-driven** — 39 merges, stabilization focus |
| **NanoBot** | 7 | 33 | — | 23 | ❌ | **Healthy pipeline** — good merge/review ratio |
| **NanoClaw** | 1 | 7 | — | 5 | ❌ | **Converging** — feature PRs approaching merge |
| **PicoClaw** | 3 | 3 | — | 3 | ❌ | **Low activity** — stalled PRs, maintainer bottleneck |
| **NullClaw** | 1 | 4 | — | 3 | ❌ | **Steady but small** — single contributor momentum |
| **TinyClaw** | 0 | 0 | — | — | ❌ | **Inactive** |
| **Moltis** | 0 | 0 | — | — | ❌ | **Inactive** |
| **ZeptoClaw** | 0 | 0 | — | — | ❌ | **Inactive** |

---

## 3. OpenClaw's Position

**Advantages:**
- **Largest community by orders of magnitude** — 404 issues and 500 PRs updated in 24 hours is 8x the nearest competitor (Hermes Agent). This creates a massive contributor pipeline.
- **Most complete multi-channel support** — Telegram, Discord, Slack, Matrix, and a native desktop (macOS/Clawdbot) with active community demand for Linux/Windows ports (#75 — 110 comments, 81 👍).
- **Deepest platform integration** — Support for Slack relay, Discord API, Telegram rich messages, and browser CDP authentication indicates the most mature channel abstraction layer.
- **Highest user satisfaction ceiling** — A blind user describes it as "one of the most powerful AI work interfaces I have ever used," signaling strong accessibility and power-user adoption.

**Technical Approach Differences:**
- OpenClaw uses a **session-based architecture** with write-lock timeouts (#86538) and subagent delivery lanes — more complex than NanoBot's simpler agent loop but enabling richer multi-agent workflows.
- The project's "clawsweeper" labeling system for PR triage is more structured than competitors, but the sheer volume overwhelms it.

**Community Size Comparison:**
- OpenClaw's 404 issues/500 PRs in 24h dwarfs IronClaw (14/50), CoPaw (29/50), and ZeroClaw (50/40). However, this size is a double-edged sword: 446 open PRs with a "needs-maintainer-review" bottleneck means contributors face long wait times.
- The #75 Linux/Windows app request (110 comments, 81 👍) is the most-liked open issue across *all* projects in this digest, highlighting a critical platform gap.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging independently across multiple projects:

| Requirement | Affected Projects | Specific Signals |
|-------------|-------------------|------------------|
| **Model cost optimization** | OpenClaw, NanoBot, CoPaw, ZeroClaw | OpenClaw #94518 (DeepSeek cache <10%); NanoBot PRs #4581/#4588 (token reduction); CoPaw #3891 (prefix cache optimization); ZeroClaw #8327 (image markers inflating tokens) |
| **Session reliability & persistence** | OpenClaw, Hermes Agent, LobsterAI, CoPaw | OpenClaw #86538 (write-lock timeouts); Hermes Agent #20591 (stale credential pool); LobsterAI #1388 (email config timeout); CoPaw #5579 (conversation loss on crash) |
| **Multi-agent orchestration** | OpenClaw, NanoBot, Hermes Agent, ZeroClaw | OpenClaw #79077 (Telegram bot-to-bot); NanoBot #4291 (subagent model presets); Hermes Agent #5257 (generalized ACP client); ZeroClaw #7218 (A2A agent discovery) |
| **Security & credential hardening** | OpenClaw, Hermes Agent, NanoClaw, ZeroClaw | OpenClaw #97972 (CDP auth fix); Hermes Agent #55352 (credential redaction); NanoClaw #2880 (symlink escape); ZeroClaw #7497 (WASM plugin security) |
| **Cross-platform parity** | OpenClaw, Hermes Agent, NullClaw | OpenClaw #75 (Linux/Windows apps); Hermes Agent #32207 (Windows/WSL freeze); NullClaw #972 (Telegram idle disconnect) |
| **Plugin/Skill extensibility** | OpenClaw, NanoBot, ZeroClaw | OpenClaw #81913 (Plugin SDK); NanoBot #4554 (Dream skill duplication guard); ZeroClaw #8135 (WASM plugin runtime) |
| **Streaming stability** | NanoBot, NullClaw, CoPaw | NanoBot #4595 (tool_call ID corruption); NullClaw #971 (native tool calls during streaming); CoPaw #5573 (stream reasoning errors) |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | IronClaw | CoPaw | ZeroClaw |
|-----------|----------|---------|--------------|----------|-------|----------|
| **Target user** | Power users, multi-platform | Lightweight CLI users | Enterprise, multi-agent | Rust ecosystem, QA-heavy | Chinese market, channels | WASM plugins, desktop |
| **Primary language** | TypeScript/Node.js | Python → Node.js hybrid | TypeScript | Rust | TypeScript | TypeScript + WASM |
| **Architecture** | Session-based, subagents | Simple agent loop | ACP client/server | Reborn (Rust rewrite) | Runtime v2 | WASM plugin runtime |
| **Channel focus** | All major platforms | CLI + webhooks | Slack, Telegram, Discord | Browser + Slack | Feishu, DingTalk, WeChat | Telegram + desktop |
| **Deployment model** | Desktop app + server | `curl \| bash` | Dashboard + CLI | Self-hosted, staging | On-premise, cloud | Desktop + server |
| **Plugin ecosystem** | Skill ecosystem | Dream memory consolidation | Trial skill (autonomous gate) | MCP catalog | AgentScope 2.0 | WASM plugins |
| **Key innovation** | Phase 5 session replay | Streaming token reduction | Graphnosis encrypted memory | Progressive tool disclosure | Mission Mode integration | OCI registry distribution |

**OpenClaw vs. Peers:**
- **vs. NanoBot:** OpenClaw is far more feature-rich but much heavier; NanoBot's "ultra-lightweight" claim (#660) targets users who find OpenClaw bloated.
- **vs. Hermes Agent:** Hermes focuses on enterprise ACP orchestration, while OpenClaw is consumer-first; Hermes has better maintainer responsiveness (50 PRs vs 500, but better merge ratio).
- **vs. IronClaw:** IronClaw is Rust-based and QA-obsessed (daily failure taxonomy); OpenClaw is faster-moving but less stable.
- **vs. CoPaw:** CoPaw is China-focused (Feishu, DingTalk) with a release-driven cadence; OpenClaw is global but triage-bottlenecked.

---

## 6. Community Momentum & Maturity

**Tier 1: High Velocity, High Risk (Rapid Iteration)**
- **OpenClaw** — Exponential contributor growth but maintainer bottleneck; 500 PRs/day with 446 open. Risk: burnout, quality regression.
- **Hermes Agent** — 50 PRs/day, strong security focus, 7 merged today. Risk: Windows/macOS stability gaps.
- **IronClaw** — 19 merged today, daily QA taxonomy, Reborn architecture transition. Risk: breaking changes percolating.

**Tier 2: Controlled Growth (Stabilizing)**
- **CoPaw** — Post-beta release, 18 PRs merged today, active channel fixes. Maturity: high, with clear release cycle.
- **ZeroClaw** — Sprint toward v0.8.3, 40 open PRs, WASM plugin strategy. Maturity: medium, architectural changes ongoing.
- **NanoBot** — Good review ratio (10 merged/33 open), security hardening. Maturity: medium-high, but installer reliability issues.

**Tier 3: Low Activity / Stalled**
- **LobsterAI** — Release-driven but stale bugs (87 days old), low community engagement.
- **PicoClaw** — 3 open PRs, all stalled >7 days, maintainer bandwidth likely limited.
- **NullClaw** — Single contributor momentum, Telegram reliability issue unaddressed.

**Inactive:** TinyClaw, Moltis, ZeptoClaw — no activity in 24h+.

---

## 7. Trend Signals

**1. Cost Optimization is the #1 UX Priority**
Across OpenClaw (#94518 — DeepSeek cache collapse), NanoBot (#4581/#4588 — token reduction), and CoPaw (#3891 — prefix cache optimization), users are hitting API cost ceilings. The "cheap model" value proposition is being eroded by caching regressions. **Signal:** Projects that solve prompt caching and token efficiency will win cost-sensitive users.

**2. Multi-Agent Orchestration is Becoming Table Stakes**
Hermes Agent (#5257 — generalized ACP client), ZeroClaw (#7218 — A2A agent discovery), and OpenClaw (#79077 — bot-to-bot Telegram) all point to a future where agents must interoperate. **Signal:** A "TCP/IP for agents" standard is emerging; first-mover advantage for projects that ship inter-agent protocols.

**3. Security Hardening is Accelerating**
Hermes Agent merged 7 security PRs today (credential redaction, WebSocket limits, control character stripping). NanoClaw fixed a CWE-59 symlink escape. ZeroClaw proposed OCI registry distribution with cosign. **Signal:** Enterprise adoption is driving security investment; projects without security audits will be filtered out.

**4. Plugin Ecosystems are Maturing Beyond Simple Skills**
OpenClaw's Plugin SDK (#81913), ZeroClaw's WASM plugin runtime (#8135), and IronClaw's MCP catalog point to a shift from single-file skills to full plugin architectures. **Signal:** Plugin discoverability and security (WASM sandboxing, OCI registries) will differentiate projects.

**5. Cross-Platform Parity is a Competitive Battleground**
OpenClaw's #75 (Linux/Windows apps, 81 👍) and Hermes Agent's macOS update unreliability (#46076) show that desktop parity is a major acquisition blocker. **Signal:** Projects that ship native apps for all three platforms (or excellent web UIs) will capture users locked out by platform gaps.

**6. The "Silent Failure" Epidemic**
Multiple projects have bugs where errors are swallowed or delivery fails without notification (OpenClaw #80520, Hermes Agent #20591, ZeroClaw #8505). **Signal:** Users demand observability; logging, error propagation, and session replay (OpenClaw Phase 5) are emerging as must-haves.

**7. Reasoning Model Compatibility is Fragile**
ZeroClaw #7756 (tools blocked on reasoning models), OpenClaw #94518 (cache collapse on DeepSeek), and CoPaw #5573 (stream reasoning errors) indicate that the newest LLM models are breaking standard agent patterns. **Signal:** Projects that maintain backwards compatibility with reasoning models while supporting tool calling will be preferred.

---

**Bottom Line for Developers:** OpenClaw offers the richest ecosystem but the worst review latency. NanoBot and ZeroClaw offer better contributor experiences with narrower scope. IronClaw is the project to watch for enterprise-grade quality assurance. The shared pain points—cost, reliability, cross-platform support—are opportunities for targeted contributions that will be welcomed across the ecosystem.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the **NanoBot Project Digest** for **2026-06-30**.

---

## NanoBot Project Digest: 2026-06-30

### 1. Today's Overview
The NanoBot project is experiencing **high activity** today, with 33 Pull Requests updated in the last 24 hours and 7 Issues updated. The project remains in a rapid development phase, focusing heavily on **security hardening, context optimization, and infrastructure maturity**. There were no new releases today, but the project is seeing a surge in community contributions addressing edge cases in the execution engine, streaming logic, and provider configuration. The maintainers appear responsive, with 10 PRs merged/closed against 23 remaining open, suggesting a healthy review pipeline.

### 2. Releases
**None.** No new versions were published today.

### 3. Project Progress
10 PRs were merged or closed today, signaling solid advancement across several key areas:
- **Webhook Infrastructure**: PR #4502 ("Add gateway webhook triggers") was closed/merged, establishing a dedicated webhook ingestion layer for external event-driven workflows.
- **Streaming Stability**: PR #4596 (fix for non-file-edit tool ID corruption) was opened and is likely being fast-tracked due to the critical nature of Issue #4595.
- **Performance & Cost**: Two related PRs (#4581, #4588) advanced, focusing on aggressive input-token reduction through command-output compaction and subagent announcer pruning. These are high-value toward reducing API costs.
- **Sandbox Security**: PR #4577 added regression tests for bwrap (bubblewrap) sandbox mounts, validating workspace isolation.
- **Configuration Resilience**: PR #4583 addressed a crash bug where null config sections caused migration failures during load.

### 4. Community Hot Topics
- **Issue #660 (CLOSED)** – *"Project claims to be 'ultra-lightweight' but includes bloated Node.js dependency"* – **15 comments, 5 👍**
  - **Analysis**: This remains the most emotionally charged discussion in recent history. The user contends that requiring Node.js alongside Python contradicts the "ultra-lightweight" promise. The community likely debated the necessity of bundling a Node runtime vs. making it optional. Since this is closed, maintainers likely addressed it (possibly by documenting the dependency or making it optional).
  - [GitHub Issue #660](https://github.com/HKUDS/nanobot/issues/660)

- **PR #4596 (OPEN)** – *"fix(streaming): skip non-file-edit tools in apply_final_call_ids to prevent id corruption"* – **Critical fix**
  - **Analysis**: This PR directly addresses the highest-severity live bug (#4595). The high number of tool call ID corruptions suggests this has been a persistent pain point for users running parallel tool calls.
  - [GitHub PR #4596](https://github.com/HKUDS/nanobot/pull/4596)

- **PR #4554 (OPEN)** – *"fix(memory): block Dream from creating duplicate skills via write guard"* – **High interest**
  - **Analysis**: "Dream" is NanoBot's memory-consolidation agent. Users are experiencing skill directory bloat where Dream creates near-identical skill files. The community is pushing for guardrails that prevent duplication while retaining flexibility.
  - [GitHub PR #4554](https://github.com/HKUDS/nanobot/pull/4554)

- **PR #4591 (OPEN)** – *"Add session-bound local triggers"* – **New workflow paradigm**
  - **Analysis**: This introduces a `/trigger` command for external events delivered via local filesystem queue. This signals a move toward NanoBot as a programmable automation agent, not just a chat interface.
  - [GitHub PR #4591](https://github.com/HKUDS/nanobot/pull/4591)

### 5. Bugs & Stability
| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **Critical** | [#4595](https://github.com/HKUDS/nanobot/issues/4595) | `apply_final_call_ids` overwrites correct tool_call IDs for non-file-edit tools, causing permanent session poisoning where every subsequent API call fails. | ✅ [#4596](https://github.com/HKUDS/nanobot/pull/4596) |
| **High** | [#4599](https://github.com/HKUDS/nanobot/issues/4599) | Linux install script crashes silently at the TUI screen before user interaction. | ❌ None yet |
| **High** | [#4592](https://github.com/HKUDS/nanobot/issues/4592) | `restrictToWorkspace` security guard fails to detect absolute paths following `=` (e.g., `--output=/etc/passwd`), allowing container escapes. | ✅ [#4594](https://github.com/HKUDS/nanobot/pull/4594) |
| **Medium** | [#4222](https://github.com/HKUDS/nanobot/issues/4222) | `max_messages` truncation and `microcompact` continuously invalidate prompt/prefix caching, defeating performance optimizations. | ❌ Open |

**Assessment**: The tool_call ID corruption bug (#4595) is the most active crisis today, with a fix PR already submitted. The path security bypass (#4592) is a significant vulnerability but already has a fix pending.

### 6. Feature Requests & Roadmap Signals
| Request | Issue/PR | Likely Next Version? |
|---------|----------|----------------------|
| **Automatic reasoning effort escalation** | [#4419](https://github.com/HKUDS/nanobot/issues/4419) | **Likely** – This is a low-effort, high-value feature. Since `reasoningEffort` config already exists, escalating it per-task is a natural progression. |
| **GitHub Copilot Enterprise/GHE support** | [#4598](https://github.com/HKUDS/nanobot/pull/4598) | **Highly Likely** – The PR is already open with CI green. This is targeted for enterprise adoption. |
| **Provider-scoped proxy config** | [#4578](https://github.com/HKUDS/nanobot/pull/4578) | **Highly Likely** – enterprise feature for air-gapped environments. |
| **Subagent configurable model presets** | [#4291](https://github.com/HKUDS/nanobot/pull/4291) | **Likely** – This has been open for 19 days and addresses a core flexibility gap. |
| **Markdown session export** | [#4587](https://github.com/HKUDS/nanobot/pull/4587) | **Likely** – low complexity, high user satisfaction delta. |

**Prediction**: The next minor release will likely include: GHE provider support, proxy configuration, reasoning effort escalation, and the markdown export feature.

### 7. User Feedback Summary
- **Pain Point – Installer Reliability**: Issue #4599 (TUI crash during install) and the ongoing discussion around Node.js bloat (#660) indicate that **first-run experience is a weak point**. Users expect a frictionless `curl | bash` pipeline, but encountering a crash or unexpected dependency requirements causes immediate frustration.
- **Pain Point – Context Cost**: Multiple PRs (#4581, #4588) from user `hamb1y` focus on reducing input tokens. The urgency here suggests that **users are hitting API cost ceilings** with high-turn conversations, especially when tool outputs are verbose.
- **Satisfaction – Streaming & Session Stability**: The community is actively testing parallel tool calls and persistent sessions, and is fast to report regressions. This indicates **high engagement from power users** who depend on NanoBot for production workflows.
- **Use Case – Security-Conscious Enterprises**: The flurry of PRs around proxy config, sandbox mounts, and workspace containment suggests a growing **enterprise adoption wave** where users require air-gapped, auditable deployments.

### 8. Backlog Watch
| Issue/PR | Last Updated | Status | Reason for Concern |
|----------|--------------|--------|---------------------|
| [#660](https://github.com/HKUDS/nanobot/issues/660) | 2026-06-29 | **CLOSED** | Although closed, this was a high-reaction issue about the "ultra-lightweight" claim. If the closure didn't include documentation changes or an optional dependency flag, expect re-opening. |
| [#4222](https://github.com/HKUDS/nanobot/issues/4222) | 2026-06-29 | Open | **Stale bug** – 24 days since creation, no fix PR. Prompt caching is core to performance. If left unaddressed, heavy users will experience degraded latency. |
| [#4291](https://github.com/HKUDS/nanobot/pull/4291) | 2026-06-29 | Open | **Stale PR** – 19 days. This adds significant flexibility for subagent model configuration. Lack of review may indicate maintainer bandwidth constraints. |
| [#4293](https://github.com/HKUDS/nanobot/pull/4293) | 2026-06-29 | Open | **Stale PR** – 19 days. Fixes subagent result injection in cron jobs. If cron users are blocked on this, it is a silent backlog item. |

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-30

## Today's Overview

Hermes Agent shows **very high activity** on June 30, 2026, with 50 issues and 50 PRs updated in the last 24 hours. The open-to-closed ratio is heavily skewed toward open items (46 open issues, 43 open PRs), indicating a surge of community contributions and bug reports. A cluster of PRs today addresses **security hardening** (credential redaction, WebSocket size limits, control character stripping) and **platform fixes** (Windows encoding, SSH tunnel persistence). No new releases were published today, suggesting the project is in a heavy development phase between version bumps.

## Releases

**None.** No new releases were published today. The last known version mentioned in issues is `0.17.0`, with references to `0.16.0` and `0.14`/`0.15` in bug reports. The absence of a release despite high PR merge activity suggests a release may be imminent.

## Project Progress

**7 PRs were merged or closed today**, though the digest data does not enumerate which ones specifically. Notable PRs that remain open but reflect significant forward progress include:

- **#55340** — Fix Slack inbound user mentions and bot identity grounding (human-readable mentions, self-identification)
- **#55344** — Support confidential OIDC clients with `client_secret` for self-hosted dashboard auth
- **#51197** — Add Graphnosis as a local encrypted memory provider + MCP catalog entry
- **#12794** — Per-subagent model/provider overrides for `delegate_task` + model observability plugin
- **#55334** — New `trial` optional skill that gates autonomous agent outputs with independent judging

A **major security fix** batch landed across multiple PRs: credential redaction in debug logging (#55352), WebSocket 16 MiB message size limit (#55345), control character stripping from saved credentials (#55336), and forced UTF-8 encoding for all subprocess calls (#55339).

## Community Hot Topics

The most active discussions this period:

1. **#5257** — *"Generalized ACP client for multi-agent CLI orchestration"* (13 comments, 18 👍)  
   [Link](https://github.com/NousResearch/hermes-agent/issues/5257)  
   **Need:** The community wants Hermes to orchestrate *any* ACP-compatible coding agent (Claude Code, Copilot, etc.), not just its own. This is a major architectural expansion from server-only to peer orchestrator.

2. **#27282** — *"Gateway exits mid-turn with stdin EOF on macOS TUI"* (10 comments)  
   [Link](https://github.com/NousResearch/hermes-agent/issues/27282)  
   **Need:** A persistent macOS TUI stability bug affecting session continuity. Users need reliable terminal interactions without unexpected gateway exits.

3. **#17565** — *"Configurable Temperature Parameter"* (5 comments, 6 👍)  
   [Link](https://github.com/NousResearch/hermes-agent/issues/17565)  
   **Need:** Users report severe hallucinations because temperature is hardcoded. This is a fundamental UX gap — the most basic LLM inference parameter isn't user-configurable.

4. **#50775** — *"Visual Ghosting on Telegram macOS Client"* (1 comment, 4 👍)  
   [Link](https://github.com/NousResearch/hermes-agent/issues/50775)  
   **Need:** Visual artifacts in streamed Telegram responses since v0.17.0. High reaction count suggests widespread impact on Telegram users.

5. **#24039** — *"Auxiliary fallback chain should reuse fallback_providers"* (3 comments, 2 👍)  
   [Link](https://github.com/NousResearch/hermes-agent/issues/24039)  
   **Need:** Users want a single, unified fallback provider configuration instead of two parallel systems that don't coordinate.

## Bugs & Stability

**High severity (P1):**
- **#20591** — Credential pool reads stale `os.environ` instead of fresh `.env`; code doesn't match documented behavior. Security boundary risk. No fix PR identified yet. [Link](https://github.com/NousResearch/hermes-agent/issues/20591)

**Medium severity (P2) — with fix PRs available:**
- **#55314** — Tool-argument coercion rounds large Discord/Telegram IDs through float, corrupting values. [Link](https://github.com/NousResearch/hermes-agent/issues/55314)
- **#55309** — Lone surrogate characters in model replies crash Telegram delivery. [Link](https://github.com/NousResearch/hermes-agent/issues/55309)
- **#55305** — SQLite WAL corruption on ZFS with multiple connections, causing session-breaking errors. [Link](https://github.com/NousResearch/hermes-agent/issues/55305)
- **#55130** — Dashboard returns HTTP 500 when basic auth is the only provider. [Link](https://github.com/NousResearch/hermes-agent/issues/55130)
- **#55265** — Cron delivery to private chat forum-topics lands in General instead of correct topic. [Link](https://github.com/NousResearch/hermes-agent/issues/55265)

**Medium severity (P2) — no fix PR identified:**
- **#32207** — `/clear` command freezes terminal on Windows/WSL. [Link](https://github.com/NousResearch/hermes-agent/issues/32207)
- **#49242** — Windows WhatsApp gateway doesn't prefer Hermes-managed Node/npm. [Link](https://github.com/NousResearch/hermes-agent/issues/49242)
- **#32626** — SSH Tunnel connection settings not persisted across restarts. [Link](https://github.com/NousResearch/hermes-agent/issues/32626)
- **#16693** — Discord VC TTS plays but user hears nothing (no green ring). [Link](https://github.com/NousResearch/hermes-agent/issues/16693)
- **#51560** — `fallback_providers` as JSON string silently empties the fallback chain. [Link](https://github.com/NousResearch/hermes-agent/issues/51560)
- **#55268** (Closed) — MoA aggregator returns HTTP 404 on unrecognized host (duplicate). [Link](https://github.com/NousResearch/hermes-agent/issues/55268)

**Today's fix PRs (new):**
- #55352 — Credential redaction in debug logging
- #55345 — WebSocket message size limit (16 MiB)
- #55339 — Explicit UTF-8 encoding for all subprocess calls
- #55336 — Strip control chars from saved env credentials
- #55338 — Fix browser type with real input events
- #55340 — Fix Slack inbound mention parsing
- #55343 — Fix TUI voice transcript re-queue race
- #55346 — Fix stale session IDs in gateway logging
- #55333 — Bridge session context into subprocess env
- #55337 — Fix Windows git binary path resolution
- #55351 — Bound LINE reply/push error body reads
- #55348 — Bound Teams standalone error body reads

## Feature Requests & Roadmap Signals

**Strong next-release candidates:**
- **Generalized ACP client (#5257)** — Multi-agent orchestration across different coding agent types. Likely in next major release given 18 👍 and architectural significance.
- **Configurable temperature (#17565)** — Basic user-facing LLM parameter. The high number of hallucination complaints makes this urgent.
- **Graphnosis memory provider (#51197)** — Already implemented in an open PR. Likely incoming.
- **Per-subagent model overrides (#12794)** — Long-running PR (since April) with substantial code. May need rebase but represents a major delegation capability.
- **Chat width setting (#55287)** — Simple UI customization for Desktop app. Likely quick to merge.

**User-requested additions:**
- **DeepSeek provider in Desktop (#38065)** — Missing provider option in UI despite being available in CLI.
- **`compress_context` command (#31684)** — Context window management feature with patches attached.
- **Trial skill for autonomous agents (#55334)** — Novel quality gate that could reshape agent reliability guarantees.
- **Confidential OIDC client support (#55344)** — Already implemented in open PR, likely to merge.

## User Feedback Summary

**Satisfaction signals:**
- Active contributor community with 50+ PRs/day, suggesting strong developer engagement
- Users building complex integrations (BlueBubbles, Discord VC, Telegram cron, Feishu, Teams)
- Community contributed a full crypto module gift (#55230, though flagged as invalid)

**Pain points:**
- **Windows stability remains the #1 theme** — `/clear` freezes (#32207), Node/npm path issues (#49242), git binary path problems (#55337), subprocess encoding crashes (#53428)
- **Telegram delivery reliability** — Multiple P2 bugs: cron topic routing (#55265), ghosting (#50775), surrogate crashes (#55309), broken tables (#53632)
- **macOS update unreliability** — Desktop in-app updates don't apply or relaunch (#46076)
- **Configuration complexity** — Dual fallback systems (#24039), temperature not configurable (#17565), JSON string vs YAML confusion (#51560)
- **Provider compatibility gaps** — DeepSeek missing from Desktop (#38065), reasoning_effort silently dropped for custom/zai (#55276), ACP sessions with `provider="custom"` fail (#13489)

## Backlog Watch

**Issues needing maintainer attention:**
- **#20591** (P1, 26 days old) — Credential pool stale `os.environ` bug. Security boundary risk with zero fix PRs. Test documents correct behavior but code doesn't match — this should be urgent. [Link](https://github.com/NousResearch/hermes-agent/issues/20591)
- **#17565** (P3, 62 days old) — Configurable temperature. 6 👍, oldest feature request still open. [Link](https://github.com/NousResearch/hermes-agent/issues/17565)
- **#12794** (P3, 71 days old) — Per-subagent model overrides + observability plugin. Huge PR with detailed implementation. [Link](https://github.com/NousResearch/hermes-agent/pull/12794)
- **#5257** (P3, 86 days old) — Generalized ACP client. Most-liked open issue (18 👍) with no release commit. [Link](https://github.com/NousResearch/hermes-agent/issues/5257)
- **#16693** (P2, 64 days old) — Discord VC TTS silent playback. Unresolved for over two months. [Link](https://github.com/NousResearch/hermes-agent/issues/16693)
- **#13489** (No priority label, 70 days old) — ACP sessions with `provider="custom"` fail. [Link](https://github.com/NousResearch/hermes-agent/issues/13489)

**PRs needing review:**
- **#51197** (7 days old) — Graphnosis memory provider. Large feature PR. [Link](https://github.com/NousResearch/hermes-agent/pull/51197)
- **#52570** (5 days old) — CI timing reports. Infrastructure improvement. [Link](https://github.com/NousResearch/hermes-agent/pull/52570)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is your structured PicoClaw project digest for **2026-06-30**.

---

# PicoClaw Project Digest – June 30, 2026

## 1. Today's Overview
The project is in a steady but low-activity phase. Over the last 24 hours, 3 issues were touched, splitting between one closure (a Safari bug) and two active bugs regarding tool-calling. Three pull requests remain open, all of which involve significant new features (a Delta Chat gateway, AWS Bedrock prompt caching, and per-turn token usage tracking). No new releases were cut, indicating a potential pipeline bottleneck. The staleness of several high-value PRs and issues suggests maintainer bandwidth may be stretched.

## 2. Releases
**None** – No new releases were published as of this digest.

## 3. Project Progress
- **No PRs were merged or closed** in the last 24 hours. All three open PRs remain in review.
- Active open PRs (highlights):
  - **#3063** (Delta Chat gateway) – still unmerged after 22 days.
  - **#3163** (AWS Bedrock prompt caching) – 7 days open, maintains good momentum.
  - **#3156** (Per-turn token usage via Pico channel) – 8 days open, waiting for review.

## 4. Community Hot Topics
- **Feature Request: More Messaging Gateways** – Issue **#3093** (👍1, 4 comments) asks for integration of SimpleX, Tox, and Wire. The user explicitly needs gateway support beyond the current set. This is a strong signal for expanding protocol support.
- **Volcengine Tool-Call Leak** – Issue **#3153** (2 comments) describes a critical UX bug where tool calls are returned as raw `<seed:tool_call>` text. This has received recent attention and is the most active bug report today.
- **Safari Compatibility** – Issue **#3090** (3 comments, now closed) was resolved. The panel did not work on iOS < 16.4, but the closure suggests a fix was merged or deferred.

## 5. Bugs & Stability
- **[HIGH] Volcengine Doubao Tool-Call Leak (Issue #3153)** – A regression where tool calls from `doubao-seed-2.0-pro` are emitted as raw XML text instead of being executed. This makes the assistant unusable for tool-dependent workflows. **No associated fix PR exists.**
- **[LOW] Safari on iOS < 16.4 Panel (Issue #3090)** – Now closed. Fixed or determined out of scope. Low overall impact for modern iOS users.

## 6. Feature Requests & Roadmap Signals
- **Messaging Gateway Expansion (Issue #3093)** – User requests SimpleX, Tox, and Wire. With PR **#3063** (Delta Chat gateway) already open, it's likely the project is building a gateway abstraction layer. Expect SimpleX or Tox gateway support in the next 1–2 releases.
- **Prompt Caching & Cost Tracking (PRs #3163, #3156)** – Both PRs aim to improve LLM cost efficiency and observability. These are enterprise-friendly features that align with PicoClaw's positioning as a production-ready AI assistant.
- **No roadmap document was referenced** in this data, but the consistent pattern of gateway and LLM platform optimization suggests these are the project's current strategic priorities.

## 7. User Feedback Summary
- **Satisfaction driver:** Users are actively requesting and contributing new gateway integrations (Delta Chat, SimpleX, Tox), indicating the extensibility model is appreciated.
- **Pain point (tool reliability):** The Volcengine tool-call leak (Issue #3153) is a clear source of dissatisfaction—users expect tool execution to be transparent.
- **Pain point (platform compatibility):** Safari on older iOS was a blocker, though it appears to be resolved. Mobile support remains an area of sensitivity for the community.

## 8. Backlog Watch
- **PR #3063 – Delta Chat Gateway** (22 days open, no review from maintainers) – A fully featured PR with new functionality and documentation. If maintainer review is not coming, this risks becoming stale.
- **Issue #3093 – SimpleX / Tox Gateway Request** (20 days, 1 reaction, 4 comments) – No maintainer response. This and PR #3063 together represent a gateway expansion roadmap that may be blocked.
- **PR #3156 – Per-turn Token Usage** (8 days open, no comments from maintainers) – A straightforward feature that would improve transparency for power users; silence suggests triage capacity is limited.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-30

## Today's Overview
Activity is **elevated** today, with 7 pull requests and 1 issue updated in the last 24 hours, signaling a busy development cycle. The project appears to be at the tail end of a push to unify multiple chat channel adapters (Discord, Slack Socket Mode) under a single Chat SDK bridge, while also fixing several stability and security regressions. A critical open bug (#2888) where Discord drops image/file attachments is the top concern, affecting users who rely on visual inputs. No releases were published today, but the number of merged/closed PRs (2) and open PRs (5) suggests a release may be imminent once the current batch of channel-adapter PRs lands.

## Releases
**No new releases** in the last 24 hours. Users and contributors are working from the last published version.

## Project Progress
Two PRs were **merged/closed** today, representing both a feature and a fix:

- **#2883 [CLOSED] feat: voice-notify v3 意图分流 + kill-switch** (*tier2tech-tian*): A significant upgrade to the voice notification system, now categorizing summaries into 5 intent types (action/silent/navigate/tech_status/notify). Code blocks and long tables are skipped, and a runtime kill-switch (`VOICE_SUMMARY_VERSION=off`) has been added. 38/38 tests passed.  
  [PR #2883](https://github.com/nanocoai/nanoclaw/pull/2883)

- **#2882 [CLOSED] fix(ncl): default messaging-groups create instance to channel_type** (*omri-maya*): Fixes a `NOT NULL` constraint violation when using `ncl messaging-groups create`, caused by the `instance` column being missing from the generic CRUD column list.  
  [PR #2882](https://github.com/nanocoai/nanoclaw/pull/2882)

## Community Hot Topics
The most active items today:

- **#2888 [OPEN] Discord (and likely other url-only chat-sdk adapters) drop image/file attachments** (*eagansilverpathmarketing*) — 1 comment, opened today. This is the only open issue and is generating interest due to its functional severity: agents see only filenames, not content. The root cause is pinpointed to `messageToInbound` in the Chat SDK bridge.  
  [Issue #2888](https://github.com/nanocoai/nanoclaw/issues/2888)

- **#2884 [OPEN] feat(discord): add Discord channel adapter + fix Gateway approval-button routing** (*rudgalvis*) — 5 open PRs, this one is likely the most anticipated as it adds full Discord support via the Chat SDK bridge. It also fixes a bug where approval-card buttons were not routing correctly.  
  [PR #2884](https://github.com/nanocoai/nanoclaw/pull/2884)

The underlying need is clear: users are adopting NanoClaw on **multiple chat platforms**, and the project is racing to provide a unified adapter experience. The Discord issue (#2888) and PR (#2884) are complementary — once #2884 lands, #2888 becomes the top blocker for a fully functional Discord integration.

## Bugs & Stability
| Severity | Bug | PR Fix Exists? | Notes |
|----------|-----|----------------|-------|
| **Critical** | #2888 — Discord drops image/file attachments; agent only sees filename/type metadata | No fix PR yet | Root cause identified in `chat-sdk-bridge.ts`; Telegram works fine. Affects all URL-only adapters. |
| **Medium** | #2886 — New agents created via channel registration inherit the wrong provider (Claude instead of user's configured provider), causing 401 errors on single-provider installs | PR #2886 (open) | Fix exists but not merged; workaround available by manually setting provider. |
| **Medium** | #2880 — Symlink escape in attachment writes (CWE-59) allows compromised agent to write arbitrary host files via session directory symlinks | PR #2880 (open) | Security fix for both inbound file-write paths. Important for multi-tenant deployments. |
| **Low** | #2882 — `ncl messaging-groups create` fails with `NOT NULL` constraint (instance column) | PR #2882 (merged today) | Already fixed. |

## Feature Requests & Roadmap Signals
The current PR queue strongly signals that **multi-platform chat support** is the top roadmap priority. Specifically:

- **Native Discord adapter** (PR #2884) — expected to land soon, enabling Discord as a first-class channel alongside Telegram and Slack.
- **Slack Socket Mode in setup** (PR #2885) — currently only webhook-based setup is available; this PR would add Socket Mode option during `setup:auto`.
- **Dashboard with OpenCode support** (PR #2871) — a new dashboard pusher that sends state snapshots to a `@nanoco/nanoclaw-dashboard` server every 60 seconds. This could signal a planned hosted dashboard product or observability feature.
- **Voice notify v3** (PR #2883, already merged) — indicates ongoing investment in voice/notification UX, with intent-based routing and user-controlled kill-switch.

Prediction for next release: **Discord adapter + Slack Socket Mode setup + attachment fix (#2888)** will likely ship together in a minor version bump.

## User Feedback Summary
- **Pain point — Attachment handling:** A user-s-reported issue (#2888) highlights that Discord users cannot share images/screenshots/files with agents. This is a core functionality gap that prevents visual tasks (code review, UI screenshots, document analysis). The user explicitly notes Telegram works fine, which may drive users to prefer Telegram over Discord.
- **Pain point — Provider configuration:** Users on single-provider installs (e.g., only OpenAI) get 401 errors when new agents are created via channel registration, because the system defaults to Claude. PR #2886 addresses this directly.
- **Satisfaction indicator:** The voice-notify v3 feature was well-tested (38/38 tests) and received three rounds of review before merge, suggesting a careful, quality-focused community.
- **Security awareness:** The symlink escape fix (PR #2880) shows that users running multi-agent or shared-host setups are concerned about container security. The fix was requested via issue #2828, indicating proactive community reporting.

## Backlog Watch
- **#2871 [OPEN] feat(dashboard): add dashboard pusher with OpenCode support** (*grantland*) — Created 2026-06-27, no comments yet. This is a significant feature addition with no maintainer feedback or discussion. It may need review and decision on whether it aligns with project direction.  
  [PR #2871](https://github.com/nanocoai/nanoclaw/pull/2871)

- **#2880 [OPEN] fix(security): contain inbox symlink escapes in attachment writes** (*johnmathews*) — Created 2026-06-28, updated 2026-06-29. This is a security fix with no comments, despite addressing a CWE-59 vulnerability. It should be prioritized for review given the security implications.  
  [PR #2880](https://github.com/nanocoai/nanoclaw/pull/2880)

No long-unanswered issues or PRs beyond 48 hours old that require maintainer attention. The project appears to be well-maintained with active triage.

---

**Overall Project Health:** 🟢 **Good** — Activity is high, the team is reactive to bugs (especially security), and major feature work (Discord, Slack, dashboard) is converging. The #2888 attachment bug is the top risk for user satisfaction on Discord, but the root cause is known and a fix is likely imminent.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-30

## Today's Overview
Project activity is moderate with 4 PRs updated and 1 open issue reported today. The community contribution momentum remains healthy, with two related PRs targeting REPL improvements and a significant streaming tool-call feature under review. No new releases were published, and the single open bug report points to a potentially critical Telegram channel responsiveness issue. Overall, the project shows steady feature development and community engagement, though the lack of maintainer responses on the reported bug may cause user concern.

## Releases
No new releases were published on this date.

## Project Progress
One PR was merged or closed today:
- **PR #960** (Closed; author: vernonstinebaker) – [fix(cli): handle arrow keys in agent REPL](https://github.com/nullclaw/nullclaw/pull/960). This PR adds a small allocation-free line editor for the interactive `nullclaw agent` REPL, enabling POSIX raw-mode input for TTY sessions so arrow keys, history navigation, cursor movement, backspace/delete, Home/End, and common word-left/right sequences are handled instead of printed as control characters. This closes a longstanding UX pain point for CLI users.

Two new open PRs from the same author are pending review:
- **PR #971** (Open) – [feat(streaming): native tool calls during SSE streaming](https://github.com/nullclaw/nullclaw/pull/971). Decouples native tool-call support from the streaming path, allowing providers that support native tools during streaming to emit them. Previously the agent loop disabled native tools whenever a stream callback was attached, forcing tools into a prompt-injection format.
- **PR #970** (Open) – [fix(cli): handle arrow keys in agent REPL](https://github.com/nullclaw/nullclaw/pull/970). Appears to be a new iteration of the same fix as PR #960, with identical summary.

One dependency update PR remains open:
- **PR #956** (Open; author: dependabot[bot]) – [ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group](https://github.com/nullclaw/nullclaw/pull/956).

## Community Hot Topics
**Most active issue:**
- **Issue #972** (Open; created 2026-06-30) – [[bug] telegram channel stop respond after some idle time](https://github.com/nullclaw/nullclaw/issues/972). Author: i11010520. The user reports that the Telegram channel stops responding after overnight idle periods, while `nullclaw` backend processes appear to work normally. No comments or reactions yet. This issue is brand new but represents a critical user-facing feature degradation. The underlying need is for reliable continuous operation of the Telegram integration without requiring manual restart or intervention, especially for users running the agent as a long-lived service.

**Most active PRs:**
- **PR #971** – *feat(streaming): native tool calls during SSE streaming* – No comments listed in data, but represents a significant feature enhancement that addresses a known limitation in streaming provider compatibility.
- **PR #970 / PR #960** – The duplicate PRs for CLI arrow key handling suggest this feature received focused attention from the same contributor, indicating high community interest in improving the interactive REPL experience.

## Bugs & Stability
**High severity:**
- **Issue #972** – [Telegram channel stops responding after idle time](https://github.com/nullclaw/nullclaw/issues/972). The reporter states the channel "die[s] away at next morning after working well last day." The backend agent process (`nullclaw agent -m "ping"`) responds normally, suggesting a specific integration-level bug (e.g., session timeout, WebSocket disconnection, or Telegram API reconnection logic). No fix PR exists yet. This is likely a stability regression affecting production Telegram deployments.

No other bugs, crashes, or regressions were reported today. No fix PRs are associated with this issue at this time.

## Feature Requests & Roadmap Signals
The open PRs signal two clear roadmap directions:
1. **Streaming native tool calls (PR #971)** – This is a significant architectural improvement that enables better compatibility with LLM providers that support native tool calling during streaming responses. This feature will likely be included in the next release, as it resolves a known limitation.
2. **REPL usability (PR #970)** – The repeated fix for arrow key handling suggests CLI power users are a key segment. This small but impactful UX improvement is likely to be merged soon.

The dependabot PR for Alpine 3.24 bump (PR #956) indicates ongoing container maintenance.

## User Feedback Summary
The single issue today highlights a recurring user pain point: **reliability of long-running agent integrations**. The user reports that the Telegram channel works "well" during the day but fails after idle overnight periods. The fact that the backend agent responds normally to `ping` suggests the user has confidence in the core agent's stability but is experiencing frustration with channel-specific reconnection or session management. No explicit satisfaction or dissatisfaction cues are available, but the silence on the issue (0 comments) may indicate either lack of maintainer attention or that the reporter is awaiting initial triage.

## Backlog Watch
- **PR #956** (Open since 2026-06-15) – [ci(deps): bump alpine from 3.23 to 3.24](https://github.com/nullclaw/nullclaw/pull/956). This dependency update has been open for 15 days without merge or rejection. While low-severity, long-open dependency PRs can accumulate risk and should be periodically reviewed.
- **Issue #972** (Created today) – While not backlogged, this issue requires prompt maintainer attention to assess and triage the reported Telegram channel failure before user frustration escalates.

No other long-unanswered issues or PRs are evident from the current data window.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-30

## 1. Today's Overview

IronClaw (IronClaw Reborn) is in an intense development and stabilization phase, with **50 PRs** (31 open, 19 merged/closed) and **14 issues** updated in the last 24 hours. The project is undergoing a major architecture transition ("Reborn") alongside active QA testing. Activity is very high, with core contributors landing integration test frameworks, porting WebUI coverage, and addressing a large batch of QA-discovered bugs. A comprehensive daily failure taxonomy (#5411) and multiple P1/P2 bugs indicate the Reborn release is still maturing, though the team is responding rapidly with fix PRs.

## 2. Releases

**No new releases today.** The last release candidate (PR #5311, still open) proposes breaking changes across multiple crates:
- `ironclaw_common`: 0.4.2 → **0.5.0** (⚠ API breaking)
- `ironclaw_skills`: 0.3.0 → **0.4.0** (⚠ API breaking)
- `ironclaw`: 0.24.0 → **0.29.1**

These breaking changes are not yet merged/live.

## 3. Project Progress (Merged/Closed PRs Today — 19 items)

**Test Infrastructure & Coverage**
- **PR #5402** (closed, L, core) — Landed shared-persistence integration tests for approvals, auth, memory, secrets, extensions — major expansion of in-process Reborn test framework ([link](https://github.com/nearai/ironclaw/pull/5402))
- **PR #5427** (open, XS, core) — Extracted mock-MCP scaffolding into `harness_mcp.rs` as first step of Wave 0 backend coverage roadmap ([link](https://github.com/nearai/ironclaw/pull/5427))

**WebUI v2 Fixes**
- **PR #5414** (closed, M) — Fixed log entry text not being selectable/copyable in webui v2 Logs page ([link](https://github.com/nearai/ironclaw/pull/5414))

**QA & CI Tooling**
- **PR #5406** (closed, XL) — Hardcoded QA sheet prompts into live QA runner, removed harness GitHub latest-release prefetch ([link](https://github.com/nearai/ironclaw/pull/5406))
- **PR #5422** (closed, M) — Fixed `/canary` PR target validation to accept same-repo PR numbers ([link](https://github.com/nearai/ironclaw/pull/5422))
- **PR #5423** (closed, M) — Accepted routine wording variants in QA 7C text gates ([link](https://github.com/nearai/ironclaw/pull/5423))
- **PR #5424** (open, M) — Link failed Reborn QA cases to debug artifacts ([link](https://github.com/nearai/ironclaw/pull/5424))

**Coverage Porting (Codex)**
- **PR #5372** (closed, XL) — Ported browser coverage for approval gates, auth gates, rendering safety, tool execution visibility ([link](https://github.com/nearai/ironclaw/pull/5372))
- **PR #5371** (closed, XL) — Ported browser coverage for chat core, attachments, history, SSE behavior ([link](https://github.com/nearai/ironclaw/pull/5371))

**Design & Architecture**
- **PR #5425** (closed, XS) — Design proposal for multi-user RBAC convergence, "reuse what we have, add no new scope" ([link](https://github.com/nearai/ironclaw/pull/5425))

**Dependency Updates**
- **PR #5050** (closed, S) — `react-router` bump from 7.9.1 to 7.15.1 in webui v2 frontend ([link](https://github.com/nearai/ironclaw/pull/5050))

**Closed Issues**
- **#5413** — "Reborn inline OAuth refresh swallows non-applied refresh silently — make it fail loudly" — fix merged ([link](https://github.com/nearai/ironclaw/issues/5413))
- **#5196** — "[Reborn] 'Ask each time' tool permission may fail with authorization error" — closed ([link](https://github.com/nearai/ironclaw/issues/5196))
- **#5412** — "webui v2: log entry text is not selectable / copyable" — fixed in PR #5414 ([link](https://github.com/nearai/ironclaw/issues/5412))
- **#4776** — "Add global Always Allow setting for eligible tools" — closed ([link](https://github.com/nearai/ironclaw/issues/4776))

## 4. Community Hot Topics

### Most Active Issues
- **#5411** — "Daily ironclaw failure taxonomy — 2026-06-29" — Critical diagnostic report: out of 161 pinchbench tasks, only 50 passed (111 non-pass); dominant failures from rate-limiting (nearai/ironclaw), agent self-correction loops, and forced-approval dialog processing ([link](https://github.com/nearai/ironclaw/issues/5411))
- **#5421** — "[bug, scope: channel/web] Web search under ironclaw-reborn: not zero-config by default" — Blocks zero-config user experience for web search capability ([link](https://github.com/nearai/ironclaw/issues/5421))
- **#5420** — "[bug, scope: channel/web] Routine delivery target is a global per-user default, not per-routine" — Core automation feature broken — setting one routine to Slack reroutes ALL routines ([link](https://github.com/nearai/ironclaw/issues/5420))
- **#5415** — "[bug_bash_P1] Multi-tool Google Sheets workflow fails with protocol violation" — P1 severity, consistent failure on 18-25 call workflows ([link](https://github.com/nearai/ironclaw/issues/5415))

### Most Active PRs
- **#5149** — "Context management — progressive tool disclosure" — 91 tool schemas + system prompt + history pushing ~25.8k tokens per call; PR cuts this significantly to reduce latency/timeouts ([link](https://github.com/nearai/ironclaw/pull/5149))
- **#5311** — "chore: release" — Version bump with breaking changes across multiple crates, still open awaiting merge ([link](https://github.com/nearai/ironclaw/pull/5311))
- **#5362** — "[codex] Harden Slack pairing activation flows" — Addresses UX and reliability issues in Slack account pairing ([link](https://github.com/nearai/ironclaw/pull/5362))

### Underlying Needs
The community/QA team is systematically uncovering integration-quality gaps in the Reborn architecture: OAuth refresh failures, incorrect tool authorization, per-routine vs global settings, and protocol violations with complex Google Sheets workflows. The daily taxonomy (#5411) underscores systemic rate-limiting and agent loop issues that are the top priority for performance tuning.

## 5. Bugs & Stability

### P1 (Critical)
- **#5415** — "Multi-tool Google Sheets workflow fails with protocol violation" → Consistent failure on 18-25 call workflows; **no fix PR yet** ([link](https://github.com/nearai/ironclaw/issues/5415))

### P2 (High)
- **#5417** — "Wrong skill activated for Hacker News search" → Agent activates "tech-debt-tracker" instead of web search; **no fix PR yet** ([link](https://github.com/nearai/ironclaw/issues/5417))
- **#5416** — "Incorrect Google connection state causes contradictory authentication flow" → Agent contradicts itself on Gmail connection status; **no fix PR yet** ([link](https://github.com/nearai/ironclaw/issues/5416))
- **#5420** — "Routine delivery target is global, not per-routine" → Core automation feature broken; **no fix PR yet** ([link](https://github.com/nearai/ironclaw/issues/5420))

### P3 (Medium)
- **#5418** — "Conversation messages appear in wrong order after tool activity" → UI rendering bug; **no fix PR yet** ([link](https://github.com/nearai/ironclaw/issues/5418))
- **#5419** — "No option to rename an automation" → Missing UX feature; **no fix PR yet** ([link](https://github.com/nearai/ironclaw/issues/5419))

### Other
- **#5426** (unprioritized) — "Cannot create a routine: system drive is not available" → Blocks routine creation on hosted-staging; **no fix PR yet** ([link](https://github.com/nearai/ironclaw/issues/5426))
- **#5421** (scope: channel/web) — "Web search not zero-config under Reborn" → UX regression; **no fix PR yet** ([link](https://github.com/nearai/ironclaw/issues/5421))
- **#4108** (long-standing) — "Nightly E2E failed" → Ongoing CI instability since May 27 ([link](https://github.com/nearai/ironclaw/issues/4108))

**Notable:** 5 bug-bash issues (#5415-#5419) were all opened on the same day (2026-06-29) by `joe-rlo`, indicating an intensive QA session. Only #5412 (log selection) has an associated fix PR (#5414) that was merged. The remaining QA issues have no attached fix PRs yet.

## 6. Feature Requests & Roadmap Signals

### Likely in Next Release
- **Progressive Tool Disclosure** (PR #5149) — Cuts ~25.8k token prompt overhead by not shipping all 91 tool schemas every call; flag-gated, default off, but high-value for latency reduction ([link](https://github.com/nearai/ironclaw/pull/5149))
- **Multi-User RBAC Convergence** (PR #5425) — Design proposal to reuse existing authorization infrastructure rather than adding new layers ([link](https://github.com/nearai/ironclaw/pull/5425))
- **Slack Pairing Flow Hardening** (PR #5362) — Better error handling, expired code handling, thread isolation ([link](https://github.com/nearai/ironclaw/pull/5362))

### Moderate Likelihood
- **Channel Pairing Flows** (PR #5373) — Generic channel proof-code pairing alongside Slack ([link](https://github.com/nearai/ironclaw/pull/5373))
- **Capability Policy E2E** (PR #5394) — Addressing multi-user capability policy from issue #5385 ([link](https://github.com/nearai/ironclaw/pull/5394))
- **Storage Stress Harness** (PR #5313) — Filesystem-backed resource governor stress testing ([link](https://github.com/nearai/ironclaw/pull/5313))

### Lower Likelihood
- **Always Allow for Eligible Tools** (Issue #4776, now closed) — User-facing setting may ship in upcoming release ([link](https://github.com/nearai/ironclaw/issues/4776))
- **Automation Renaming** (Issue #5419) — Explicit user request, but no implementation started ([link](https://github.com/nearai/ironclaw/issues/5419))

## 7. User Feedback Summary

**Pain Points (from QA and real-world usage):**
- **Multi-tool workflows fail consistently** (#5415) — Complex Google Sheets sequences with 18-25 calls hit protocol violations; real productivity workflow is blocked
- **Routine delivery is unconfigurable** (#5420) — Setting per-routine delivery target is impossible; users cannot have different routines deliver to different channels
- **Misleading authentication state** (#5416) — Agent incorrectly claims Gmail is connected, then contradicts itself — confusing for non-technical users
- **Wrong skill selection** (#5417) — "Search Hacker News" activates "tech-debt-tracker" skill; undermines trust in agent's understanding
- **No automation rename** (#5419) — Auto-generated names are too long/truncated, users cannot fix them
- **OAuth refresh failures** (#5413, closed) — Silent failures made debugging extremely difficult; now fixed to fail loudly
- **"Ask Each Time" permission breaks** (#5196, closed) — Approval dialog appears but tool fails with authorization error, then asks for approval again — duplicate, broken flow

**Satisfaction Signals:**
- The team's **rapid response** to bugs is notable — #5412 (log selection) had a fix PR within hours; #5413 (OAuth refresh) was closed same day
- The **daily failure taxonomy** (#5411) demonstrates systematic, data-driven quality management
- **Coverage porting** (PRs #5371, #5372, #5376) shows commitment to maintaining E2E quality as the architecture transitions

## 8. Backlog Watch

### Critical Attention Needed
- **#4108** — "Nightly E2E failed" — **Open for 34 days** since May 27; multiple CI failures with no substantive updates. This is the longest-standing unresolved issue and suggests a chronic CI stability problem ([link](https://github.com/nearai/ironclaw/issues/4108))

### Important Open PRs Awaiting Merge/Review
- **#5311** — "chore: release" — Breaking changes across multiple crates (ironclaw_common 0.4.2→0.5.0, ironclaw_skills 0.3.0→0.4.0, ironclaw 0.24.0→0.29.1) — **Open for 4 days** without merge, may block other work ([link](https://github.com/nearai/ironclaw/pull/5311))
- **#5149** — "Context management — progressive tool disclosure" — Per-call latency fix; **open for 7 days**, still awaiting review or merge. Given the severity of timeout issues in production, this deserves prioritization ([link](https://github.com/nearai/ironclaw/pull/5149))
- **#3706** — "chore(deps): bump postcss, @remotion/cli and @remotion/tailwind-v4" — **Open for 45 days** — This long-standing dependency update PR has been blocked for a month and a half, which could indicate CI/tooling friction or lack of reviewer bandwidth for dependency updates ([link](https://github.com/nearai/ironclaw/pull/3706))

### QA Bug Fixes Without Pending PRs
The following **bug-bash issues from 2026-06-29 have no fix PRs yet**, and the QA results were filed just yesterday. They should see action within the next 1-2 days:
- **#5415** (P1 - Google Sheets workflow)
- **#5416** (P2 - Authentication flow)
- **#5417** (P2 - Wrong skill selection)
- **#5418** (P3 - Message ordering)
- **#5419** (P3 - No rename option)
- **#5420** (P2 - Routine delivery)
- **#5421** (P2 - Web search zero-config)
- **#5426** (Critical - System drive not available)

---

*Project health assessment: High activity, rapid bug response, but significant quality gaps in Reborn features. The daily failure taxonomy and intensive QA session indicate the team is investing heavily in stability ahead of a major release.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the structured project digest for LobsterAI based on the provided GitHub data for 2026-06-29 (data as of end-of-day).

---

**Project Digest: LobsterAI (github.com/netease-youdao/LobsterAI)**
**Date:** 2026-06-30 (Data Snapshot: 2026-06-29)

### 1. Today's Overview

The project saw very high activity on June 29, 2026, driven by a significant release cycle. With 40 PRs updated (39 closed/merged) and a new version cut, the team focused heavily on stabilization and integration fixes for the OpenClaw and Cowork subsystems. While community issue volume remained moderate (11 updated), user feedback highlighted persistent concerns around token consumption and subscription policies. The overall project health appears robust, with a strong emphasis on patching regressions and improving runtime reliability ahead of the monthly release.

### 2. Releases

- **New Version:** `LobsterAI 2026.6.29` (Released 2026-06-29)
- **Key Changes:**
    - **Permissions & Routing:** Route plugin approvals through permissions (`btc69m979y-dotcom`).
    - **UI Fixes (Cowork):** Cleaned navigation rail previews and re-applied conversation rail fixes after a reversion accident (`liuzhq1986`).
    - **Stability (OpenClaw):** Preserved user turn cache stability and kept agent bootstrap workspaces separate from task working directories.
    - **History Sync:** Fixed follow-up history preservation for cron runs.
- **Breaking Changes:** None documented in the release notes.
- **Migration Notes:** Users running OpenClaw agents should update to this release to prevent identity/persona file corruption (bootstrap files now correctly load from agent workspace instead of project directory).

### 3. Project Progress

The team merged 39 PRs today, focusing on the following advancements:
- **OpenClaw Integration (Majority of work):**
    - **Plugin Support:** Pre-installed QQ and Discord channel plugins; compiled NIM plugin runtime entries; supported upgraded IM plugin installs (DingTalk, Lark, WeCom).
    - **Cron & Scheduling:** Migrated legacy cron storage on startup; synced cron run sessions; clarified scheduled-task startup states.
    - **Auth & Routing:** Routed OpenAI OAuth to the correct ChatGPT responses provider.
- **Cowork UI Polish:**
    - Fixed and reverted conversation rail tooltip alignment and preview cleanup.
- **Dependencies:**
    - Dependency bumps for the Electron group (Electron 42.5.0) remain open as a long-running chore.

### 4. Community Hot Topics

The top 3 active threads by comment count (all had 2 comments) reveal a pattern of usability friction:

1.  **#2079 - [OPEN] Execution window freeze at scroll top** (Created: 2026-05-30)
    - **Link:** [Issue #2079](https://github.com/netease-youdao/LobsterAI/issues/2079)
    - **Analysis:** A reproducible UI freeze bug that has been open for a month. The user reports it specifically on the v2026.5.27 release. This is a high-friction UX issue that lowers the quality of life for heavy users of the execution interface.

2.  **#2131 - [OPEN] Support for Hermes Agent?** (Created: 2026-06-09)
    - **Link:** [Issue #2131](https://github.com/netease-youdao/LobsterAI/issues/2131)
    - **Analysis:** A community inquiry about supporting the "Hermes Agent" framework. This signals interest in multi-agent orchestration or specialized agent runtimes. The lack of a roadmap response suggests the team is either evaluating it or prioritizing other backends.

3.  **#2121 - [OPEN] Suspected bug: repeated text consuming tokens** (Created: 2026-06-07)
    - **Link:** [Issue #2121](https://github.com/netease-youdao/LobsterAI/issues/2121)
    - **Analysis:** A user attached a screenshot showing repeated output text, suspecting token waste. This is a direct concern about cost-efficiency, which is critical for user retention in a platform where users pay per token/credit.

### 5. Bugs & Stability

**High Severity:**
- **#2079 - Execution window freeze (Open, 30 days old):** UI freeze when scrolling to top. No fix PR linked. *Impact: High, Reproducible.*
- **#2121 - Suspected token waste via repeated output (Open, 22 days old):** User report of LLM repeating output lines. *Impact: High (Cost + Usability).*
- **#1388 - Email config test timeout (Open, 87 days old):** "Test Connectivity" button hangs indefinitely, even after restart. *Impact: High, Blocks workflow automation.*

**Medium Severity:**
- **#1386 - Share screenshot incomplete for long conversations (Open, 87 days old):** Content truncated in shared image. *Impact: Medium, UX polish.*
- **#1390 - Scheduled task update unresponsive (Open, 87 days old):** Intermittent bug where editing a cron task does nothing on click. *Impact: Medium, Reliability.*
- **#1389 - Language mismatch in dropdowns (Open, 87 days old):** English UI shows Chinese text for specific options. *Impact: Low, i18n polish.*

**Low Severity (Closed today):**
- **#1434, #1435 - Minor UI typos and input overflow:** Closed as stale. *Impact: Low.*

### 6. Feature Requests & Roadmap Signals

- **Task Queueing (Issue #2120):** A user specifically requested a "workbuddy"-style pre-input queue for Claw tasks to improve continuous execution. Given the team’s heavy focus on Claw reliability in this release, a task queue feature may appear in a near-future minor release (v2026.7.x).
- **Hermes Agent Support (Issue #2131):** While only a question, "Hermes Agent" compatibility would signal expanding beyond the current OpenClaw ecosystem. Unlikely for the next release unless announced.
- **UI Layout Refinements (Issue #2120):** A request to change the skills tab from 2-column to 3-column on 2560x1600 screens. This is a low-effort CSS change that could be quickly shipped in a patch.
- **Increased Timeout for Long Scripts (Issue #2120):** User requesting longer single-task runtime for monitoring scripts. This suggests a need for configurable timeout settings in the Claw agent.

### 7. User Feedback Summary

- **Satisfaction:** Mixed. The release cycle is active and fixes are coming (e.g., the PR volume indicates the team is addressing core issues), but users are frustrated by long-standing bugs.
- **Pain Points:**
    - **Token/Resource Waste:** Users (#2121) are actively worried about hidden costs from LLM loops.
    - **Subscription Policy:** User (#2081) expressed strong anger ("来搞笑的吧???") regarding monthly subscription credits being reset without warning. *This is a critical retention signal.*
    - **Reliability:** Users report that the tool "pretends to be stable" but can't handle long background scripts (issues with `terminated` status).

### 8. Backlog Watch

Several critical issues have been "stale" for nearly 3 months (since April 3) and still have no response or fix PR. These are high-priority items that require maintainer attention:

- **Issue #1388 - [OPEN] Email test connectivity hangs:** 87 days, 1 comment, no maintainer reply. [Link](https://github.com/netease-youdao/LobsterAI/issues/1388)
- **Issue #1386 - [OPEN] Share screenshot truncated:** 87 days, 1 comment, no maintainer reply. [Link](https://github.com/netease-youdao/LobsterAI/issues/1386)
- **Issue #1390 - [OPEN] Scheduled task update fails to update:** 87 days, 1 comment. [Link](https://github.com/netease-youdao/LobsterAI/issues/1390)
- **PR #1277 - [OPEN] Dependabot chore (Electron bump):** 88 days old. While low priority, stalling a security/dependency upgrade for 3 months is a risk vector. [Link](https://github.com/netease-youdao/LobsterAI/pull/1277)

**Recommendation:** The maintainer team should triage the "stale" label. Long-duration bugs with no feedback or resolution signal either resource constraints or a triage bottleneck.

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

Here is the CoPaw project digest for **2026-06-30**, based on the provided GitHub data.

---

## CoPaw Project Digest — 2026-06-30

### 1. Today's Overview
The project is in a period of very high activity, with **29 issues** and **50 pull requests** updated in the last 24 hours. This indicates a significant development push, possibly driven by the recent **v2.0.0-beta.1 release**. Activity is heavily concentrated on frontend bug fixes (tool card display counts), integration with the new AgentScope 2.0 architecture, and addressing regressions in areas like channel notifications and model compatibility. While closed/merged items are plentiful (9 issues, 18 PRs), the backlog of open items (20 issues, 32 PRs) suggests the team is actively tackling a large queue of both bug reports and feature work.

### 2. Releases
**No new releases were published today.** The latest release remains **v2.0.0-beta.1** (from 2026-06-26), which is still undergoing installation verification (see Issue #5571).

### 3. Project Progress
A significant number of fixes and features were merged or closed today, reflecting a heavy focus on stabilization:

- **Bug Fixes:**
    - **Tool Card Display:** PRs #5628 and #5632 provide two independent fixes for the critical bug where search/read tool result cards always showed a count of "1" (Issue #5624). PR #5628 normalizes the count from display text.
    - **Governance/Tool Approval:** PR #5601 fixed a regression where tool approval notifications were not being sent to IM channels (Feishu, WeChat, etc.).
    - **Schema Compatibility:** Issue #5543 (null type in function declaration schema) was closed, resolving a blocker for some third-party model providers.
- **Architecture & Refactoring:**
    - **Mission Mode:** PR #5442, which integrates the legacy Mission Mode with the new Runtime v2 architecture, continues to be refined (still open).
    - **AgentScope 2.0 Cleanup:** PR #5634 gracefully drops a test case for the now-removed `/plan` command, aligning with the AgentScope 2.0 migration.
- **Documentation:**
    - PR #5614 updated the context management documentation.
    - PR #5631 added documentation for frame scroll and episodic memory.
    - PR #5621 added a comprehensive Sandbox section to the security documentation.

### 4. Community Hot Topics
The community's focus is clearly split between performance optimization and stability concerns.

- **DeepSeek Prefix Cache Optimization (Issue #3891, 5 comments, 1 👍):** This long-standing issue about low prefix cache hit rates (~95%) remains a hot topic. The community is acutely aware of the **4x-10x cost difference** between cache hits and misses on the DeepSeek platform, and this is seen as a major optimization opportunity.
    - [View Issue](https://github.com/agentscope-ai/QwenPaw/issues/3891)

- **Subagent & Parent Coordination (Issue #4873, 3 comments):** The bug report about running two subagents causing a rapid, unbreakable polling loop is receiving developer attention, with a dedicated fix PR (#5633) opened today. This is a critical workflow issue for users employing subagents.
    - [View Issue](https://github.com/agentscope-ai/QwenPaw/issues/4873)

- **Tool Card Display Bug (Issue #5624, 3 comments):** This is the most actively bug-fixed issue of the day, with two separate PRs submitted. The immediate developer response highlights its high impact on user experience.
    - [View Issue](https://github.com/agentscope-ai/QwenPaw/issues/5624)

### 5. Bugs & Stability
A wide range of bugs were reported, with several having active fix PRs.

- **Critical (Fix PR Exists):**
    - **Tool Card Count (Issue #5624):** Glob search and read file cards show a constant count of "1". **Fix PRs:** #5628, #5632.
    - **Subagent Poll Loop (Issue #4873):** Multi-subagent tasks cause infinite rapid polling, unbreakable from Feishu. **Fix PR:** #5633.
    - **Governance "OFF" Mode Failure (PR #5623):** Even when the "Tool Execution Security" is set to OFF, approvals are still triggered. This is a direct regression. **Fix PR:** #5623 (open).
- **High:**
    - **DeepSeek V4 400 Errors (Issue #5573):** Users on non-official DeepSeek endpoints face two distinct 400 errors related to stream reasoning content and null schema types. **Status:** No dedicated fix PR.
    - **Conversation Loss on Crash (Issue #5579):** Dialogue history is completely lost during abnormal interruptions (e.g., host reboot, service crash). **Status:** No dedicated fix PR.
- **Medium:**
    - **Excessive API Logging (Issue #5591):** UOS users report terminal spam from a polling inbox API endpoint.
    - **Qwen-Image Tool Install Error (Issue #5587):** Core tool fails to install. **Status:** No dedicated fix PR.

### 6. Feature Requests & Roadmap Signals
The community is requesting features that improve resilience, usability, and channel parity.

- **High Likelihood for Next Release:**
    - **Model Auto-Fallback / Degradation (Issue #5572, #5527):** This is the single strongest signal for new features. Users are demanding automatic fallback to a backup model when the primary model is overloaded, fails, or is rate-limited. This is a top-3 pain point.
    - **DingTalk Channel Improvements (Issue #5603, #5593):** Usability requests for the DingTalk channel are also strong. These include fixing slow streaming output and enabling previewable image messages.
- **Notable Signals:**
    - **Conversation Checkpointing (Issue #5579):** This is a more specific request for a "save-state" mechanism to prevent data loss.
    - **Context Strategy Selector (PR #5629):** The PR to expose the context strategy in the UI suggests this feature is already in development and will appear soon.
    - **Vision Fallback for Text-Only Models (Issue #5615):** A user request for automatic image-to-text conversion, mirroring a feature seen in other projects like "qclaw / codex".

### 7. User Feedback Summary
- **Pain Points:**
    - **High Cost / Inefficiency:** DeepSeek prefix caching is seen as a major cost-saving opportunity, but the current ~95% hit rate is considered low. (Issue #3891)
    - **Lack of Resilience:** Users are frustrated by single points of failure. If a model goes down or is rate-limited, the entire task fails. (Issue #5572)
    - **Data Loss:** The irreversible loss of conversation context on service crash is a critical stability and trust issue. (Issue #5579)
    - **Performance Regressions:** Users are reporting increased lag in the latest versions (Issue #5555) and poor streaming performance on specific channels like DingTalk (Issue #5603).
- **Use Cases:**
    - Users are active in deploying agents via channels like Feishu and DingTalk for long-running, complex tasks (e.g., data report generation).
    - There is strong interest in using subagents for parallel processing, but this workflow is currently unstable.

### 8. Backlog Watch
While the project is highly active, a few important issues have gone relatively quiet.

- **Issue #3891 (DeepSeek Cache):** With 5 comments and a 👍, it's been open since April. The lack of recent movement on the fix itself, despite its high cost impact, is noteworthy.
    - [View Issue](https://github.com/agentscope-ai/QwenPaw/issues/3891)

- **PR #5296 (ADBPG Memory REST-only):** This PR, open since June 18, makes a significant change by removing direct SQL support for a memory backend. It is still open with no recent activity.
    - [View PR](https://github.com/agentscope-ai/QwenPaw/pull/5296)

- **Issue #5584 (Ascend-vLLM Connection):** A user reports that custom vLLM models on Ascend hardware no longer connect since version 1.1.7. This platform-specific regression has received no maintainer response and has no fix PR.
    - [View Issue](https://github.com/agentscope-ai/QwenPaw/issues/5584)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the structured digest for ZeroClaw on 2026-06-30.

---

## ZeroClaw Project Digest: 2026-06-30

### 1. Today's Overview
ZeroClaw is in a **high-velocity development sprint** (likely v0.8.3), with 50 active issues and 40 open PRs updated in the last 24 hours. Activity is heavily focused on **tool reliability, provider compatibility, and the WASM plugin runtime**. The project is resolving several S1 (workflow-blocked) critical bugs simultaneously, including a major fix for anonymous tool-call serialization on OpenAI-compatible providers. While no new releases were cut today, the sheer volume of merged "fix" PRs suggests a point release (v0.8.3) is being hardened.

### 2. Releases
**None.** No new releases were made on this date.

### 3. Project Progress (Merged/Closed)
Several critical fixes and significant features advanced to completion today, primarily in the **provider, channel, and CI** domains:

- **Provider Fix (High Impact):** PRs [#8510](https://github.com/zeroclaw-labs/zeroclaw/pull/8510) and [#8512](https://github.com/zeroclaw-labs/zeroclaw/pull/8512) were closed/merged, fixing a bug where empty `tool_calls` content caused 400 errors on strict OpenAI-compatible backends (e.g., OpenRouter, Copilot).
- **Channel Fix:** PR [#8469](https://github.com/zeroclaw-labs/zeroclaw/pull/8469) closed, adding i18n translations for the chat toolbar across 5 languages.
- **Test Coverage:** PR [#8458](https://github.com/zeroclaw-labs/zeroclaw/pull/8458) added unit tests for the `RecordingObserver` token accumulation logic.
- **Documentation:** PR [#8484](https://github.com/zeroclaw-labs/zeroclaw/pull/8484) added documentation for scoped labels, improving project governance transparency.
- **Bug Triage:** Issue [#8328](https://github.com/zeroclaw-labs/zeroclaw/issues/8328) (Nvidia GPU detection failing on WSL2) was closed, indicating a resolution for a serious hardware compatibility regression.

### 4. Community Hot Topics
The most active discussions reveal deep engagement with the **core agent loop and security architecture**:

- **System Prompt Tool Consistency (Highest Engagement):** Issue [#8054](https://github.com/zeroclaw-labs/zeroclaw/issues/8054) (9 comments) details a pervasive bug where the system prompt tells the model "no tools are available" even when tools are registered, affecting the gateway, WebSocket, and multimodal entry points. This is a critical UX and reliability issue.
- **"No Reply" Channel Behavior:** Issue [#8410](https://github.com/zeroclaw-labs/zeroclaw/issues/8410) (3 comments) addresses a user pain point where conditional agent tasks (e.g., "silent if no new email") still send a visible response. The discussion indicates a need for a first-class `NO_REPLY` outcome in the runtime.
- **WASM Plugin Security:** Issue [#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497) (3 comments) advocates for using OCI registries for plugin distribution, implementing supply-chain security (cosign) and multi-arch support—a sign of growing production requirements.

### 5. Bugs & Stability
The project is actively fighting a cluster of **S1 (workflow blocked)** and **S2 (degraded behavior)** bugs.

- **[S1 - Workflow Blocked] Tool Unavailability on Reasoning Models (Critical):** Issue [#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756) (High Priority) reports that native/MCP tools are not passed to OpenAI and Anthropic reasoning models. This effectively breaks agent tooling for the most advanced models. PR [#8053](https://github.com/zeroclaw-labs/zeroclaw/pull/8053) is the referenced fix.
- **[S1 - Workflow Blocked] Telegram Channel Configuration:** Issue [#8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505) (High Priority) reports that the Telegram channel cannot be configured via quickstart, breaking a primary chat interface. **No fix PR is currently attached.**
- **[S2 - Degraded Behavior] Translation Leak Data Loss:** Issue [#8312](https://github.com/zeroclaw-labs/zeroclaw/issues/8312) (High Priority) describes a data-loss bug where stale translation entries re-ship leaked text. A fix is marked as "in-progress".
- **[S2 - Degraded Behavior] Skills Install Broken for Multi-Agent:** Issue [#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334) (High Priority) reports that `skills install` targets the wrong directory, breaking the primary skill installation flow on multi-agent setups. Fix is "in-progress".
- **[S2 - Degraded Behavior] IMAGE Markers Inflate Token Count:** Issue [#8327](https://github.com/zeroclaw-labs/zeroclaw/issues/8327) (Medium Risk) was closed today, meaning the fix for base64 images being sent as plain text has been resolved.

### 6. Feature Requests & Roadmap Signals
Several RFPs and trackers indicate the roadmap for **v0.8.3 and beyond**.

- **"Must-Have" for v0.8.3:** Feature [#6557](https://github.com/zeroclaw-labs/zeroclaw/issues/6557) (Runtime Model Switching) is accepted with medium risk. Trackers for the WASM plugin program ([#7314](https://github.com/zeroclaw-labs/zeroclaw/issues/7314)), runtime execution ([#8071](https://github.com/zeroclaw-labs/zeroclaw/issues/8071)), and provider serialization ([#8360](https://github.com/zeroclaw-labs/zeroclaw/issues/8360)) are all active with `status:accepted`.
- **Desktop Computer-Use:** RFC [#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) (Computer-use for desktop) is a highly ambitious feature requested by the community, allowing agents to control the mouse/keyboard. This is a **high-risk, high-reward** feature likely for a later major release.
- **A2A Agent Discovery:** RFC [#7218](https://github.com/zeroclaw-labs/zeroclaw/issues/7218) proposes a `.well-known/agent-card.json` standard for multi-agent interoperability. This suggests the project is preparing for a federated agent ecosystem.
- **No-Reply Primitive:** Issue [#8410](https://github.com/zeroclaw-labs/zeroclaw/issues/8410) (channel tasks) has strong user demand. It is likely to be implemented soon to quiet noisy agents.

### 7. User Feedback Summary
Real user pain points are surfacing through verified bug reports:

- **Pain Point (Configuration):** Users report the Telegram channel is "impossible" to configure ([#8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505)). The bot works in CLI but not on Telegram, creating a broken onboarding experience.
- **Pain Point (Tooling):** Users are frustrated by misleading keybindings on macOS ([#7800](https://github.com/zeroclaw-labs/zeroclaw/issues/7800)). The ZeroCode UI advertises actions that are unreachable.
- **Pain Point (Reliability):** The "no tools available" bug ([#8054](https://github.com/zeroclaw-labs/zeroclaw/issues/8054)) is severely impacting trust in the agent's ability to execute tasks.
- **Satisfaction Signal:** The high volume of "fix" PRs being closed (e.g., [#8327](https://github.com/zeroclaw-labs/zeroclaw/issues/8327) on image markers) shows the maintainers are responsive to community-reported regressions.

### 8. Backlog Watch
Several important items are waiting for maintainer review or require author action:

- **RFC: In-App Upgrade:** [#8170](https://github.com/zeroclaw-labs/zeroclaw/issues/8170) (with implementation PR [#8173](https://github.com/zeroclaw-labs/zeroclaw/pull/8173)) is a high-impact feature for self-hosted users but is blocked by the `needs-maintainer-review` label.
- **WASM Plugin RFC:** [#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135) (Wasm-first plugin runtime) is a significant architectural change that has been open for over a week and requires maintainer sign-off.
- **CI Security Split:** Issues [#8056](https://github.com/zeroclaw-labs/zeroclaw/issues/8056) and [#8057](https://github.com/zeroclaw-labs/zeroclaw/issues/8057) (PR gate vs. scheduled security jobs) are split from a larger security audit and have PRs in draft; they are critical for hardening the CI pipeline.
- **Cron/Heartbeat Noise:** Issue [#2128](https://github.com/zeroclaw-labs/zeroclaw/issues/2128) (Cron sends `NO_REPLY` text) has been open for over 4 months. While a discussion is active, it remains unassigned.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*