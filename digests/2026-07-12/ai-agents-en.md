# OpenClaw Ecosystem Digest 2026-07-12

> Issues: 459 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-12 01:22 UTC

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

# OpenClaw Project Digest — 2026-07-12

## 1. Today's Overview

OpenClaw is experiencing **heavy development activity** with 459 issues and 500 PRs updated in the last 24 hours, and a balanced open/closed ratio (224 open active vs. 235 closed issues; 244 open vs. 256 merged/closed PRs). A new beta release `v2026.7.1-beta.5` shipped today, featuring conversational onboarding and AI-guided provider setup. The project is actively addressing **critical stability and performance regressions** including a P0 macOS relaunch issue, gateway memory leaks, and a P0 bug where all tool results return "(see attached image)" literal strings. The backlog shows strong community engagement with several long-standing feature requests (Linux/Windows desktop apps, memory security, secret masking) still awaiting product decisions.

## 2. Releases

**New Release: OpenClaw v2026.7.1-beta.5** (2026-07-12)
[GitHub Release](https://github.com/openclaw/openclaw/releases/tag/v2026.7.1-beta.5)

### Highlights
- **Conversational onboarding:** Crestodian now runs a real agent-loop setup across CLI, web install, and macOS app
- AI-guided provider setup with model-judged approvals bound to exact operations
- Masked credential prompts for security
- Deterministic fallback when no model is available

### Migration/Notes
- This is a beta release (2026.7.1-beta.5)
- Users upgrading from earlier 2026.6.x releases should check for [legacy state migration warnings](https://github.com/openclaw/openclaw/issues/90213) and run `openclaw doctor --fix` if needed

## 3. Project Progress

**256 PRs merged/closed in the last 24 hours.** Key merged PRs and their impact:

- **[#101618](https://github.com/openclaw/openclaw/pull/101618) (CLOSED):** Fixes `#100368` — marks undelivered `message_tool_only` finals in replay, ensuring durable behavior for direct and queued follow-up runs
- **[#103332](https://github.com/openclaw/openclaw/issues/103332) (CLOSED):** Regression fix for Codex/GPT-5.6 compatibility in pi runtime
- **[#86538](https://github.com/openclaw/openclaw/issues/86538) (CLOSED):** Session write-lock timeout blocking subagent delivery lanes — resolved
- **[#86572](https://github.com/openclaw/openclaw/issues/86572) (CLOSED):** ALS scope hoisting for `withOwnedSessionTranscriptWrites` to fix vanilla OpenClaw same-lane fence trips
- **[#88838](https://github.com/openclaw/openclaw/issues/88838) (CLOSED):** Track core session/transcript SQLite migration via accessor seam (Path 3 implementation PR #96625 merged)

## 4. Community Hot Topics

| Issue/PR | Comments | Reactions | Topic |
|----------|----------|-----------|-------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | 110 | 👍81 | Linux/Windows Clawdbot Apps |
| [#88838](https://github.com/openclaw/openclaw/issues/88838) | 37 | 👍3 | SQLite session migration |
| [#99241](https://github.com/openclaw/openclaw/issues/99241) | 21 | 👍2 | Tool outputs as unreadable image attachments |
| [#86538](https://github.com/openclaw/openclaw/issues/86538) | 19 | 👍1 | Session write-lock timeout |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | 17 | 👍0 | Memory trust tagging by source |

**Analysis:** The community is most engaged around:
1. **Cross-platform expansion** — Issue #75 (110 comments, 81 👍) shows strong demand for Linux/Windows desktop apps comparable to the macOS app
2. **Session reliability** — Multiple high-comment issues (#99241, #86538, #88838) reflect user frustration with session state corruption, message loss, and migration complexity
3. **Security concerns** — Issue #7707 (memory trust tagging), #10659 (masked secrets), and #7722 (filesystem sandboxing) show growing awareness of AI agent security risks

## 5. Bugs & Stability

### P0 (Critical)
- **[#104721](https://github.com/openclaw/openclaw/issues/104721)** — *All tool results return "(see attached image)" literal string instead of actual output.* Regression — completely broken, actual data replaced with placeholder. **No fix PR yet.**
- **[#104538](https://github.com/openclaw/openclaw/issues/104538) (implied)** — macOS launchd relaunch failure. **Fix PR: [#104637](https://github.com/openclaw/openclaw/pull/104637)** (P0, ready for maintainer)

### P1 (High)
- **[#99241](https://github.com/openclaw/openclaw/issues/99241)** — Tool outputs render as image attachments, unreadable to agent. Open since July 2.
- **[#91009](https://github.com/openclaw/openclaw/issues/91009)** — Codex PreToolUse hook relay spawns CPU-bound processes, stalls gateway RPC
- **[#86996](https://github.com/openclaw/openclaw/issues/86996)** — Active Memory + Codex path causes long latency, hook timeouts, gateway stalls
- **[#103917](https://github.com/openclaw/openclaw/issues/103917)** — Gateway crashes on `FsSafeError` when subagent workspace directory is deleted
- **[#104631](https://github.com/openclaw/openclaw/issues/104631)** — False-positive heap threshold diagnostics with custom `--max-old-space-size`. **Fix PR: [#104681](https://github.com/openclaw/openclaw/pull/104681)**

### P2 (Medium)
- **[#102175](https://github.com/openclaw/openclaw/issues/102175)** — Embedded prompt cache breaks across room-event, policy, and Responses boundaries (opened July 8, 16 comments)
- **[#104516](https://github.com/openclaw/openclaw/pull/104516)** — Zero-value `resetArchiveRetention` causes silent data loss (P0-tagged, needs proof)
- **[#104691](https://github.com/openclaw/openclaw/pull/104691)** — Teams proactive sends fail after conversation migration (P1, ready for maintainer)
- **[#104654](https://github.com/openclaw/openclaw/pull/104654)** — Stuck recovery must not abort replacement embedded runs (P1, ready for maintainer)

### Stability Pattern
Multiple reports point to **gateway memory leaks** and **session state corruption** as the most painful recurring issues. The "tool outputs as image attachments" bug (#99241/#104721) appears to be a critical regression requiring immediate attention.

## 6. Feature Requests & Roadmap Signals

### Likely for Next Version (v2026.7.x or v2026.8.x)
- **Plugin-ownership enforcement** — PR [#103534](https://github.com/openclaw/openclaw/pull/103534) adds cross-plugin session mutation protection (P1)
- **Web search SecretRef resolution** — Multiple PRs ([#104829](https://github.com/openclaw/openclaw/pull/104829), [#104667](https://github.com/openclaw/openclaw/pull/104667), [#104817](https://github.com/openclaw/openclaw/pull/104817), [#104672](https://github.com/openclaw/openclaw/pull/104672)) fixing credential resolution for Ollama, MiniMax, Exa, and Gemini
- **UI unification** — PR [#104834](https://github.com/openclaw/openclaw/pull/104834) folds Skills and Skill Workshop into a Plugins hub
- **macOS menu bar redesign** — PR [#104846](https://github.com/openclaw/openclaw/pull/104846) (P3, ready for maintainer)
- **Settings search improvement** — PR [#104675](https://github.com/openclaw/openclaw/pull/104675) enables search within Settings pages

### Community-Requested Features (Under Discussion)
- **[#75](https://github.com/openclaw/openclaw/issues/75):** Linux/Windows desktop apps (110 comments, 81 👍) — highest community demand
- **[#7707](https://github.com/openclaw/openclaw/issues/7707):** Memory trust tagging by source (17 comments) — security-critical
- **[#10659](https://github.com/openclaw/openclaw/issues/10659):** Masked secrets to prevent agent access to raw API keys (14 comments) — another security priority
- **[#7722](https://github.com/openclaw/openclaw/issues/7722):** Filesystem sandboxing configuration (10 comments, 4 👍)
- **[#42026](https://github.com/openclaw/openclaw/issues/42026):** Distributed agent runtime — separate control plane from agent compute (8 comments, 3 👍)
- **[#6615](https://github.com/openclaw/openclaw/issues/6615):** Denylist support for exec-approvals (8 comments, 7 👍)

## 7. User Feedback Summary

### Pain Points
- **Tool output corruption** — "This is completely broken — the actual data is being replaced with a placeholder string" (#104721)
- **Memory leaks** — Users report gateway growing from 389MB to 14.7GB over 4 days (#54155); heap growing to 1073MB+ at idle (#87109)
- **Session state fragility** — "A single agent's stalled session blocks the entire Gateway event loop" (#84903)
- **Onboarding failures** — "Clean install of new versions since 2026.5.xx is not possible" — take 5+ minutes (#76042)
- **Documentation/documentation mismatches** — "The docs for /hooks/agent state... However, this does not work as documented" (#11665)
- **Flaky browser automation** — "File upload/chooser flow is flaky and can misreport stale-click failures as browser control timeouts" (#38844)

### Use Cases Shared
- Multi-turn webhook conversations for automation pipelines (#11665)
- Slack Block Kit for CRM summaries and database query results (#12602)
- Streaming TTS for voice calls (#8355)
- Cost tracking for OpenRouter users (#9016)
- Batch API support for background cron jobs (#9865)

## 8. Backlog Watch

### Issues Needing Maintainer Attention (High Priority)
| Issue | Age | Comments | Priority | Status |
|-------|-----|----------|----------|--------|
| [#75](https://github.com/openclaw/openclaw/issues/75) — Linux/Windows apps | 6+ months | 110 | P2 | Needs product decision |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) — Memory trust tagging | 5+ months | 17 | P2 | Needs product decision & security review |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) — Filesystem sandboxing | 5+ months | 10 | P2 | Needs product decision & security review |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) — Masked secrets | 5+ months | 14 | P1 | Needs security review & product decision |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) — Exec-approval denylist | 5+ months | 8 | P2 | Needs security review |
| [#42026](https://github.com/openclaw/openclaw/issues/42026) — Distributed runtime RFC | 4+ months | 8 | P2 | Needs security review |

### PRs Stuck in Review
| PR | Age | Status | Issue |
|----|-----|--------|-------|
| [#79982](https://github.com/openclaw/openclaw/pull/79982) — `group:core` tool grouping | 2+ months | Waiting on author | Compatibility/security implications |
| [#83933](https://github.com/openclaw/openclaw/pull/83933) — Cron deleteAfterRun fix | 2+ months | Waiting on author | Sessions/conversation state edge cases |

### New Issues Without Fix PRs (Established Today)
- [#104721](https://github.com/openclaw/openclaw/issues/104721) — P0 tool output regression (no fix yet)
- [#104829](https://github.com/openclaw/openclaw/pull/104829) — Ollama web search secret refs (PR opened same day)
- [#104691](https://github.com/openclaw/openclaw/pull/104691) — Teams conversation migration (PR ready for maintainer)

---

**Project Health Assessment:** OpenClaw is in an active development phase with strong community engagement, but is struggling with **critical stability regressions** and a **growing backlog of security-related feature requests** that have been awaiting product decisions for 5+ months. The new beta release adds valuable onboarding improvements, but the P0 tool output corruption bug and recurring memory leaks undermine user trust. The team would benefit from prioritizing the security feature backlog (masked secrets, filesystem sandboxing, memory trust tagging) to address emerging AI agent security concerns.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided community digest summaries.

---

## Cross-Project Comparison Report: Personal AI Agent Ecosystem

**Date:** 2026-07-12
**Prepared for:** Technical Decision-Makers & Developers

### 1. Ecosystem Overview

The personal AI agent open-source ecosystem is experiencing a **polarized phase of rapid innovation versus critical stabilization**. Projects like OpenClaw, ZeroClaw, and NanoBot are pushing architectural boundaries with new features (goal-modes, WASM runtimes, persistent memory), while simultaneously struggling with **critical regressions in core reliability** (session state corruption, tool output corruption, and memory leaks). The community is actively contributing via security audits (NanoBot) and bug reports (CoPaw, Hermes Agent), but maintainer bandwidth appears strained, particularly in responding to critical platform gaps (Windows support, local MCP server support) and long-standing security feature requests (secret masking, filesystem sandboxing). The landscape is consolidating around a few key pain points: **local model performance, context budget management, and robust session handling**, which are emerging as the minimum viable requirements for production agent deployments.

### 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Release Status | Health Score* | Key Activity Theme |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 459 | 500 | **New beta** (v2026.7.1-beta.5) | ⚠️ Critical | Heavy dev + critical regressions (P0 tool output bug) |
| **NanoBot** | 22 | 26 | No new release | ⚠️ Medium | Security audit remediation (42 findings) |
| **Hermes Agent** | 50 | 50 | No new release | ⚠️ Critical | Bug-fix wave from community (P1 config corruption) |
| **ZeroClaw** | 50+ | 46 | No new release | ⚠️ Medium | High-velocity architecture (goal-mode, WASM) |
| **IronClaw** | 8 | 50 | No new release (PR open 9 days) | ⚠️ Critical | Platform gaps (Windows, security reporting, local MCP) |
| **CoPaw** | 23 | 7 | **v2.0.0** (post-release) | 🔴 **Critical** | Severe v2.0.0 regressions (sandbox, context, memory) |
| **NanoClaw** | 2 | 8 | No new release | ✅ Stable | Moderate dev on guard seam + scheduled tasks |
| **PicoClaw** | 0 | 3 | No new release | ✅ Stable | Low activity, one useful fork-sync PR merged |
| **NullClaw** | 2 | 0 | No new release | ⚠️ Low | Low activity, critical bug (Telegram idle timeout) |
| **LobsterAI** | 3 | 1 | No new release | ⚠️ Stale | All items stale (>3 months), one core feature broken |
| **Moltis** | 0 | 1 | No new release | ✅ Stable | Very low activity, one open bugfix PR |
| **TinyClaw** | 0 | 0 | N/A | ⚠️ Inactive | No activity |
| **ZeptoClaw** | 0 | 0 | N/A | ⚠️ Inactive | No activity |

*Health Score is a qualitative assessment based on bug severity, PR merge velocity, release recency, and community engagement.*

### 3. OpenClaw's Position

OpenClaw maintains a **dominant position** in terms of community size (459 issues, 500 PRs updated in 24h) and release cadence (new beta release today). Its key advantages include:
- **Feature Depth**: Pioneered conversational onboarding, AI-guided provider setup, and plugin-ownership enforcement.
- **Community Investment**: The largest user base demanding cross-platform apps (Issue #75: 110 comments, 81 👍) and security features (masked secrets, memory tagging).
- **Technical Approach**: Focus on deterministic fallback and a rich agent-loop setup differentiates it from competitors.

However, OpenClaw shares the same core vulnerability as its peers: **critical stability regressions** (P0 tool output bug, memory leaks) that undermine user trust. Its position is strong but precarious; the high velocity of new features must be matched by an equally aggressive stabilization effort to retain its community lead.

### 4. Shared Technical Focus Areas

The following requirements are emerging across **multiple projects**, indicating industry-wide gaps:

1.  **Local & Self-Hosted Model Performance (NanoBot, ZeroClaw, OpenClaw)**
    - *Need:* Efficient prompt caching, context budget that works out-of-the-box, and reliable streaming.
    - *Impact:* Directly affects usability on single-GPU setups; fundamental for on-premise deployments.

2.  **Session State Reliability & Recovery (OpenClaw, Hermes Agent, CoPaw, ZeroClaw)**
    - *Need:* Robust session write-locks, no silent message drops (WhatsApp, Telegram), recoverable session state after crashes, and no hallucinated user requests.
    - *Impact:* Essential for production-grade automation pipelines.

3.  **Security & Access Control (NanoBot, OpenClaw, Hermes Agent, IronClaw, ZeroClaw)**
    - *Need:* API key isolation, masking secrets from agents, filesystem sandboxing, approval gate bypass prevention for non-shell tools, and subprocess environment hygiene.
    - *Impact:* Blockers for enterprise adoption and multi-tenant deployments.

4.  **Cross-Platform Support (OpenClaw, IronClaw, CoPaw, NullClaw)**
    - *Need:* First-class Windows and Linux desktop apps, functional macOS packaging, and reliable operation on Windows (VS 2026, PowerShell).
    - *Impact:* Limits developer adoption to the macOS/Linux user base.

5.  **MCP (Model Context Protocol) Ecosystem Integration (Hermes Agent, IronClaw, NanoBot, ZeroClaw)**
    - *Need:* Reliable MCP server lifecycle management (no zombie processes), support for local (stdio/loopback) transports.
    - *Impact:* Critical for custom tool/plugin development workflows.

### 5. Differentiation Analysis

| Feature Focus | OpenClaw | NanoBot | Hermes Agent | ZeroClaw | IronClaw | CoPaw | Key Differentiator |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Target User** | Power users, massive community | Security-conscious devs | Enterprise / platform reliability | **Developers building agents** | NEAR AI ecosystem devs | Chinese-language users | ZeroClaw targets the "agent developer" use case most explicitly. |
| **Architectural Priority** | Rich plugin ecosystem, conversational UX | Security hardening | Reliability, approval gates | WASM runtime, goal-mode | Extension-runtime, attestation | Sandbox, memory | ZeroClaw is the most architecturally ambitious; NanoBot the most security-focused. |
| **Technical Stack** | Heavy ML inference focus | Python, rapid OSS | C++, platform-native | Rust, WebAssembly | Rust, NEAR protocol | Python, desktop-focus | Stack choice correlates with target user (Python for ease, Rust for performance/security). |
| **Key Weakness** | Stability regressions | Local model perf | Config corruption, context compaction | Context budget, tool availability | Platform gaps, no security channel | Post-release regressions | Each project has a critical single point of failure. |

### 6. Community Momentum & Maturity

**Tier 1: Rapid Iteration / High Risk (High velocity, critical regressions)**
- **OpenClaw**, **ZeroClaw**, **Hermes Agent**, **IronClaw**, **CoPaw**
    - These projects are pushing the most code and features but are also generating the most friction from regressions. CoPaw is in a particularly dangerous state post-v2.0.0. IronClaw is at risk of alienating new developers due to platform gaps.

**Tier 2: Focused Hardening (Medium velocity, high quality)**
- **NanoBot**, **NanoClaw**
    - NanoBot is successfully absorbing a large security audit. NanoClaw is advancing carefully on architectural improvements (guard seam, scheduled tasks). These projects are likely to produce the most stable next releases.

**Tier 3: Maintenance & Low Activity (Low velocity, stable)**
- **PicoClaw**, **NullClaw**, **Moltis**
    - These projects are operational but not attracting significant new contributions. NullClaw's critical Telegram bug remains unaddressed.

**Tier 4: Dormant / Inactive (No velocity)**
- **TinyClaw**, **ZeptoClaw**, **LobsterAI**
    - These projects show no recent code activity. LobsterAI is notable for having a ready-to-merge PR and a critical bug left unattended for 3+ months.

### 7. Trend Signals for AI Agent Developers

1.  **The "Out-of-the-Box" Obstacle**: The single most common pain point across projects is that **first-run experience is broken**. Context budgets exceed limits (ZeroClaw, OpenClaw), no model is available (OpenClaw), CLI commands don't match docs (NanoBot), and Windows support is non-functional (IronClaw). **Implication**: The market is not saturated; a project that nails a reliable, one-command setup on all platforms will capture significant adoption.

2.  **Security is Moving from "Nice-to-Have" to "Must-Have"**: The NanoBot security audit (42 findings) and the IronClaw security reporting gap signal that **vulnerability disclosure is a hygiene factor**. Projects without a `SECURITY.md` or private reporting channel are at risk of a public disclosure crisis. **Implication**: AI agent developers should treat security as a release-blocker, not a backlog item.

3.  **The Rise of the "Reasoning Model" Tax**: Multiple projects report issues specific to reasoning models (e.g., CoPaw infinite loops with Qwen3.7+, Hermes Agent context compaction fabricating history, OpenClaw/ZeroClaw tool-availability lies to reasoning models). **Implication**: Loop architectures designed for older models (GPT-4, Claude 3) are failing under new reasoning patterns. Rearchitecting for "fast-thinking (tool use) vs slow-thinking (reasoning)" is the next frontier.

4.  **Local AI is a First-Class Requirement, Not a Niche**: The demand for performance with local models (Ollama, 32GB VRAM) is no longer a corner case. It is the primary pain point for NanoBot and a growing concern for ZeroClaw. **Implication**: Projects that optimize for local inference (prompt caching, smaller context budgets, efficient streaming) will unlock the massive "self-hosted developer" market.

5.  **Automated Pipelines are the Unspoken Killer App**: User stories across projects (cron jobs, webhooks, Slack Block Kit, CRM summaries) reveal a clear pattern: **agents are being used as batch processing engines, not just chat interfaces**. The most requested features (scheduled tasks, queued messages, headless operation, notification channels) all point toward **background automation**. **Implication**: The next competitive moat will be a project's ability to function as a reliable, unattended cron-based agent runtime, not just a conversational chatbot.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-12

## 1. Today's Overview

NanoBot is in an **intense security and stability remediation phase**, with a comprehensive 42-finding audit driving the majority of recent activity. The project saw **22 issues updated** (19 open, 3 closed) and **26 PRs updated** (20 open, 6 merged/closed) in the last 24 hours, representing a **high level of community and contributor engagement**. A significant security audit by contributor `hamb1y` produced a wave of coordinated bug reports and corresponding fix PRs, suggesting the maintainer team is prioritizing hardening. No new releases were published, indicating the project is in a focused development cycle rather than a release stabilization phase. The community's central concern — performance degradation with local models — is gradually being addressed through architectural changes to prompt caching.

## 2. Releases

**No new releases** since the last digest. The project appears to be accumulating fixes and features for a future release.

## 3. Project Progress

**Merged/Closed PRs (6 total):**

- **[#4891 [merged]** `refactor(agent): make runtime context opt-in and prefix-stable`](https://github.com/HKUDS/nanobot/pull/4891) — A critical architectural improvement that stops injecting runtime context (time, channel info) into every user prompt by default, enabling better LLM cache utilization. This directly addresses the performance degradation reported in issues #2463 and #4867.
- **[#4844 [merged]** `refactor(agent): gate sustained goals behind explicit /goal`](https://github.com/HKUDS/nanobot/pull/4844) — Refactors the sustained-goal feature to require explicit user invocation, preventing background tasks from blocking user interaction.
- **[#4764 [merged]** `fix(mcp): isolate reconnect cancel scopes to prevent gateway crash`](https://github.com/HKUDS/nanobot/pull/4764) — Fixes a crash when MCP servers timeout and the reconnect path is triggered, resolving issue #4302.
- **[#4860 [closed]** No such command "onboard" or "webui"](https://github.com/HKUDS/nanobot/issues/4860) — Documentation/onboarding bug resolved.
- **[#4302 [closed]** Gateway crashes after MCP reconnect](https://github.com/HKUDS/nanobot/issues/4302) — Fixed by PR #4764.
- **[#4872 [closed]** Dream should only create git commits if productive](https://github.com/HKUDS/nanobot/issues/4872) — Quality-of-life improvement for the "Dream" memory consolidation feature.

## 4. Community Hot Topics

The most active discussions reveal a community deeply focused on **performance, security, and developer experience**:

1. **[#2463 [14 comments]** Architectural: prompt prefix not preserved](https://github.com/HKUDS/nanobot/issues/2463) — A foundational issue dating to March 2026, still actively discussed. The core problem: NanoBot's conversation history format differs from what's actually sent to LLMs, breaking prompt caching and causing 60-second delays with local models.

2. **[#4867 [4 comments]** Preserve exact prompt prefix to enable caching](https://github.com/HKUDS/nanobot/issues/4867) — A direct follow-up to #2463, reporting that the caching issue makes NanoBot "totally unusable with Ollama and 32 GB of VRAM." User frustration is palpable, with reports of 60-second overhead on every simple turn. The newly merged PR #4891 directly addresses this.

3. **[#4815 [audit summary]** 42 security/bug/refactor findings](https://github.com/HKUDS/nanobot/issues/4815) — A comprehensive code audit that has sparked rapid responses (7+ fix PRs submitted in 24 hours). The community is watching this closely as it sets the tone for NanoBot's security posture.

**Underlying needs**: The community wants NanoBot to be performant with local/self-hosted models, secure enough for production use, and reliable under multi-user deployment scenarios.

## 5. Bugs & Stability

**Critical severity — fix PRs exist:**

- **API key leaking between providers** ([#4784](https://github.com/HKUDS/nanobot/issues/4784)) — Provider API keys written to global `os.environ` can overwrite or leak between providers; subprocesses inherit all keys. Fix in PRs #4889, #4880.
- **CLI apps leak API keys to subprocesses** ([#4783](https://github.com/HKUDS/nanobot/issues/4783)) — Full environment passed to installed app subprocesses.

**High severity — fix PRs submitted:**

- **Read_file OOM on multi-GB files** ([#4785](https://github.com/HKUDS/nanobot/issues/4785)) — Entire file loaded before truncation.
- **Unbounded/asyncio.Queue memory exhaustion** ([#4780](https://github.com/HKUDS/nanobot/issues/4780)) — No backpressure in MessageBus.
- **WebSocket connection exhaustion** ([#4781](https://github.com/HKUDS/nanobot/issues/4781)) — No max_connections limit.
- **API rate limiting absent** ([#4782](https://github.com/HKUDS/nanobot/issues/4782)) — Zero throttling on /v1/chat/completions.
- **Authorization bypass via process_direct()** ([#4779](https://github.com/HKUDS/nanobot/issues/4779)) — 6+ callers bypass channel-level auth.
- **/stop command cancels other users' tasks** ([#4777](https://github.com/HKUDS/nanobot/issues/4777)) — Scoped to chat, not sender.
- **System channel bypasses all auth** ([#4778](https://github.com/HKUDS/nanobot/issues/4778)) — No allowlist on sender_id.

**Medium severity:**

- **Docker Compose disables container confinement** ([#4886](https://github.com/HKUDS/nanobot/issues/4886)) — SYS_ADMIN, AppArmor, and seccomp disabled.
- **CLI app registry is unsigned supply chain** ([#4885](https://github.com/HKUDS/nanobot/issues/4885)) — Remote registries control install commands.
- **WebFetch sends URLs to Jina** ([#4884](https://github.com/HKUDS/nanobot/issues/4884)) — Privacy concern with third-party service.
- **API session locks grow without bounds** ([#4883](https://github.com/HKUDS/nanobot/issues/4883)) — Fix submitted in PR #4890.
- **Dream reports empty files as modified** ([#4882](https://github.com/HKUDS/nanobot/issues/4882)) — False change detection.
- **Windows PowerShell output corruption** ([#4881](https://github.com/HKUDS/nanobot/issues/4881)) — UTF-8 decoding of UTF-16LE output.
- **Test setup: dev extra missing dependency** ([#4887](https://github.com/HKUDS/nanobot/issues/4887)) — Feishu tests fail without `lark-oapi`.

**Notable**: Every critical/high-severity issue has a corresponding fix PR already submitted by the same reporter or core contributors, indicating **rapid community-to-maintainer response**.

## 6. Feature Requests & Roadmap Signals

**Most likely for next release:**

1. **Prefix-stable prompt caching** (PR #4891 merged) — The top community pain point (60-second delays with Ollama) is being addressed by making system prompts cacheable. This is the single highest-impact feature for local model users.

2. **Session-bound model presets** ([PR #4866](https://github.com/HKUDS/nanobot/pull/4866)) — Per-session model selection, preserved across turns and subagents. Expected to merge soon.

3. **Guided WebUI setup flows** ([PR #4855](https://github.com/HKUDS/nanobot/pull/4855)) — Productized channel setup with validation and QR handoff. Indicates focus on onboarding experience.

4. **Workspace write serialization** ([PR #4888](https://github.com/HKUDS/nanobot/pull/4888)) — Prevents file corruption from concurrent sessions editing the same workspace.

5. **MCP ToolProvider refactoring** ([PR #4875](https://github.com/HKUDS/nanobot/pull/4875)) — Extracting MCP lifecycle into a dedicated provider for better maintainability.

**Predicted for next version**: The sustained-goal refactoring (PR #4844) and 42-finding audit fixes strongly suggest the next release will be a **security-and-stability-focused minor version** (likely 0.7.x) rather than a feature release.

## 7. User Feedback Summary

**Pain points (clearest signals):**

- **"Totally unusable with Ollama and 32 GB of VRAM"** (#4867) — The caching issue adds 60 seconds per turn, rendering local model usage impractical. This is the community's loudest complaint.
- **New user confusion**: "The commands mentioned on the website don't exist" (#4860) — Documentation and CLI command mismatches hurt first-run experience.
- **Windows compatibility**: PowerShell UTF-16 corruption (#4881) limits Windows adoption.
- **Developer experience**: Test setup is broken for contributors (#4887), discouraging external contributions.

**Satisfaction signals:**

- The audit author `hamb1y` is submitting both bug reports and fix PRs, indicating high contributor trust in the maintainer team's responsiveness.
- Multiple contributors (chengyongru, adabarbulescu, hamb1y) are actively involved in the security hardening effort, suggesting a healthy open-source community.
- The 42-finding audit (#4815) was met with rapid fix submissions, signaling that security concerns are taken seriously.

## 8. Backlog Watch

**Long-unanswered, high-priority items:**

- **[#2463** (created March 25, 2026)** Architectural: prompt prefix not preserved**](https://github.com/HKUDS/nanobot/issues/2463) — 14 comments, 4 months old. The root cause of the caching performance problem. Has now been addressed by PR #4891, which was merged today. This is effectively resolved.

- **[#4021** (created May 27, 2026)** fix(codex): dedup reasoning items before send**](https://github.com/HKUDS/nanobot/pull/4021) — 1.5 months open. Addresses duplicate-item errors in OpenAI Codex provider. Still open but has an AI-assisted PR ready.

- **[#4371** (created June 16, 2026)** fix(cache): add breakpoint before Recent History**](https://github.com/HKUDS/nanobot/pull/4371) — Another caching improvement PR, related to #2463. Potentially superseded by PR #4891 but still open with conflicts.

- **[#4145** (created June 1, 2026)** Weather Skill**](https://github.com/HKUDS/nanobot/pull/4145) — Feature PR, 1.5 months open with conflicts. New contributor's first PR, needs maintainer attention to resolve.

**Items needing maintainer attention:**

- The `hamb1y` security audit flood (8 issues, all created July 6-11) has generated 7+ fix PRs from multiple contributors. Coordination of merging order to avoid conflicts is critical.
- PR #4889 (authorize destructive priority commands) and PR #4880 (default restrict_to_workspace) both depend on each other conceptually — the maintainer should merge them together to avoid partial security fixes.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the project digest for **Hermes Agent** on **2026-07-12**.

---

## Hermes Agent Project Digest — 2026-07-12

### 1. Today's Overview
The Hermes Agent project is exhibiting **very high activity** today, with 50 Issues and 50 PRs updated in the last 24 hours. While no new releases were cut, the repository is processing a heavy inbound load of bug reports (many with `P1` and `P2` severity) covering critical agent runtime, desktop client, and platform integration failures. The PR queue is robust, with 49 open PRs actively addressing these defects, including several in the `sweeper:risk-session-state` and `sweeper:risk-platform-windows` categories. This suggests a **stabilization phase** following recent version introductions, likely v0.18.x, with the community acting as a rapid bug-finding layer.

### 2. Releases
- **New Releases:** None

### 3. Project Progress
Only **one** PR was merged or closed today (out of 50 total PRs updated). No details on the specific merge are available, but the bulk of the day's activity is focused on **open bug-fix submissions** rather than feature integration.

Key PRs submitted today include:
- **fix(update): refuse to reset away local commits** ([PR #62867](https://github.com/NousResearch/hermes-agent/pull/62867)) — Prevents `hermes update` from silently discarding local commits.
- **fix(tools): lazy-init SSH environment in vision_analyze** ([PR #62847](https://github.com/NousResearch/hermes-agent/pull/62847)) — Fixes a sandbox access failure for vision analysis under SSH backends.
- **feat(memory): per-chat/per-user/per-session memory scope isolation** ([PR #62841](https://github.com/NousResearch/hermes-agent/pull/62841)) — Adds configurable memory isolation between conversations.
- **fix(line): correct cache func for audio/video** ([PR #62848](https://github.com/NousResearch/hermes-agent/pull/62848)) — Fixes broken STT for LINE voice messages by routing non-image media correctly.

### 4. Community Hot Topics
The most active discussion threads reveal deep concerns about agent reliability and core architecture gaps:

- **#38240: Skills index is stale or degraded** ([Issue](https://github.com/NousResearch/hermes-agent/issues/38240)) — 21 comments. An automated freshness probe has been failing for over a month, indicating a chronic CI/CD pipeline issue with the skills hub generation. This is a systemic gap that affects all users relying on dynamically loaded skills.

- **#35357: Tirith approval gate bypass for non-shell tools** ([Issue](https://github.com/NousResearch/hermes-agent/issues/35357)) — 6 comments. A critical security concern: `send_message`, `write_file`, and MCP-connected tools bypass the human-in-the-loop approval system entirely. This is a fundamental architectural gap for enterprise deployment.

- **#32925: Integrate Microsoft SkillOpt** ([Issue](https://github.com/NousResearch/hermes-agent/issues/32925)) — 11 upvotes. Strong community interest in self-evolving agent skills, suggesting users want the agent to improve its own tooling through trajectory-driven optimization.

- **#62914: Unguarded `_emit_pending_fallback_notice()` crash** ([Issue](https://github.com/NousResearch/hermes-agent/issues/62914)) — 3 comments, filed today. A version skew bug crashes the entire API call on the fallback success path, blocking long-running sessions.

### 5. Bugs & Stability
**High Severity (P1/P2) Bugs Reported Today:**
- **#62914 (P2):** `AttributeError` on fallback success path crashes API calls due to version skew. (*Fix PR: None yet*)
- **#62723 (P1):** Config migration v30→v32 silently drops entire `platforms` sections in multi-profile setups, disabling integrations (e.g., Feishu) for 9 out of 10 profiles. (*Fix PR: None yet*)
- **#62557 (P1):** Hermes Desktop leaks bracketed-paste markers (`~[[200×200+`) into user messages, corrupting persisted chat history. (*Fix PR: None yet*)
- **#62365 (P1):** Context compaction fabricates user requests that were never made, injecting false history into conversations. (*Fix PR: None yet*)
- **#60385 (P2):** MCP server processes leak on reconnect, accumulating over hours. (*Status: Recently closed*)
- **#62904 (P3 - Internal Clock):** The LLM agent has no persistent internal clock, repeatedly failing to check the system date for time-relative tasks despite multiple attempted fixes. (*Fix PR: None yet*)

**Platform-Specific Risks:**
- Windows: Gateway pymalloc memory leak (#53995), Desktop infinite restart loop (#62884), CUA driver dies on Alt+Tab (#52951).
- macOS: Matrix gateway blocked due to unnecessary `python-olm` build (#62401).

### 6. Feature Requests & Roadmap Signals
- **#62927: `skills.always_preload` config option** — Users with custom model endpoints struggle to trigger `skill_view()` manually. Expect a config-based preload toggle in a minor release.
- **#62675: Add Context7 MCP to catalog** — The repository's own reference server is absent from the optional MCP catalog, forcing manual config. Likely an oversight that will be fixed soon.
- **#62916: Native OpenCode Go provider** — Request for a first-class provider in the GUI to avoid manual, unstable OpenAI-compatible endpoint configuration.
- **#62883: Edge TTS pitch control** — Simple feature request to expose the existing `pitch` parameter in config. Likely a quick win for the next patch.
- **Pricing Overrides (#9403):** Phase 4 of the pricing architecture (contract pricing, CLI sync) remains unimplemented, indicating a gap in enterprise readiness.

### 7. User Feedback Summary
User sentiment is mixed between **frustration with reliability** and **appreciation for the project's ambition**.

- **Pain Points:**
  - Context compaction inventing history (#62365) is a “hallucination of input” that undermines user trust in conversation integrity.
  - Silent config corruption during migration (#62723) causes invisible, hard-to-debug service outages.
  - Headless cron deployments cannot handle interactive approval gates (#62905), rendering automated workflows non-functional.
  - The lack of an internal clock (#62904) makes the agent unreliable for any time-sensitive task, a common complaint that feels “solved but not fixed.”

- **Positive Signals:**
  - Feature requests like SkillOpt (#32925) and memory scope isolation (PR #62841) show user engagement with advanced capabilities.
  - The community is actively submitting PRs (50 in 24h), indicating a healthy developer ecosystem despite the high bug count.

### 8. Backlog Watch
- **#38240 (Skills index stale, 21 comments, created 2026-06-03):** This automation issue has been unresolved for over a month and directly impacts the skills ecosystem. Maintainer action is required to fix the cron pipeline.
- **#35357 (Tirith HITL bypass, 6 comments, created 2026-05-30):** A security architecture gap that remains open for over six weeks. High priority for enterprise adoption.
- **#13126 (Slack TTS reply never sent, 2 comments, created 2026-04-20):** This long-standing bug has been open for nearly three months with no fix PR, suggesting a neglected platform adapter.
- **#32925 (SkillOpt integration, 11 upvotes, created 2026-05-27):** High community interest but no maintainer response or roadmap commitment yet.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest
**Date:** 2026-07-12

## Today's Overview
The project is in a low-activity phase today, with zero new issues or releases in the last 24 hours. However, three pull requests received updates, including one merged (PR #3249), indicating a moderate maintenance cadence. The merged PR brings a notable fork-sync feature for skill state management. The two remaining open PRs (one stale, one for refactoring) continue to receive attention but await further review. Overall, project health appears stable with steady, if not high-velocity, development.

## Releases
No new releases were published in the last 24 hours.

## Project Progress
One pull request was merged/closed today:

- **PR #3249** — *Skill enable/disable state + cron RunNow*  
  Author: m4n3z40 | Closed: 2026-07-11  
  [GitHub Link](https://github.com/sipeed/picoclaw/pull/3249)  
  **Summary:** This contribution syncs a fork-based feature from Ethos P6.6, adding skill toggle support in the UI and cron pause functionality. Skills can now be set to a `disabled` state in `workspace/skills/.skills-state.json`, leveraging automatic prompt cache invalidation. Disabled skills disappear from the `<skills>` context on the next turn without requiring a restart. This improves user control over active skill sets and cron scheduling.

The two remaining open PRs continue to advance:

- **PR #3225** (stale, updated 2026-07-11) — Support agent-specific runtime overrides  
  [GitHub Link](https://github.com/sipeed/picoclaw/pull/3225)

- **PR #3222** (updated 2026-07-11) — Refactor deltachat: cleanup implementation, documentation (-200 LOC)  
  [GitHub Link](https://github.com/sipeed/picoclaw/pull/3222)

## Community Hot Topics
No issues were updated or created in the last 24 hours. Among pull requests, interest remains primarily with maintainer activity. The most notable conversation (based on the summary and context of the PR) is:

- **PR #3225** — *Support agent-specific runtime overrides*  
  This persistent PR aims to allow per-agent configuration overrides (max_tokens, summarization thresholds, split_on_marker). The stale label and zero reactions suggest the community may be waiting for maintainer guidance or testing feedback, but the feature itself addresses a commonly requested need for flexible agent customization.

## Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. The only stability-related work appears in the merged PR #3249, which introduces a safer skill disablement mechanism that avoids restart requirements — a stability improvement for runtime skill management.

## Feature Requests & Roadmap Signals
While no explicit feature requests were filed today, two open PRs strongly indicate community-desired features:

1. **Per-agent runtime overrides (PR #3225)** — Allowing `max_tokens`, summarization thresholds, and other parameters to be set per agent entry. This is likely to be a candidate for the next release if testing and review progress.

2. **DeltaChat refactoring (PR #3222)** — Dropping legacy features, removing hardcoded relay lists, and adding proper `join_invite_link`/`show_invite_link` commands. This cleanup signals a push toward better protocol support and maintainability.

Predictions: The next version (if one is cut) will likely include agent overrides and the DeltaChat improvements, with skill toggle state from PR #3249 already merged.

## User Feedback Summary
No new user feedback surfaced in the reporting period. Based on the nature of the merged PR, there is an implied user need for **granular skill control** — the ability to enable/disable skills without restarting the agent — which PR #3249 addresses directly. The absence of bug reports or complaints suggests no major dissatisfaction at this time.

## Backlog Watch
The following item is flagged for maintainer attention due to inactivity or stale status:

- **PR #3225** — *Support agent-specific runtime overrides*  
  [GitHub Link](https://github.com/sipeed/picoclaw/pull/3225)  
  Stale since 2026-07-04 with no comments or reactions. This is a feature that would unlock significant flexibility for multi-agent deployments. A maintainer review or request for testing would help move it forward.

No open issues are currently unattended in the backlog.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-12

## 1. Today's Overview

NanoClaw shows moderate-high development activity today with 8 PRs updated and 2 new issues filed. The core team is progressing on two major architectural initiatives: the **guard seam** (privileged-action decision function) and **scheduled-tasks delivery unification**, with PRs #2986 and #2988 respectively active. Two critical bug fixes have been contributed: a stall watchdog for hung in-flight tools (PR #3019) and a rescue mechanism for undelivered unwrapped replies (PR #3020). Both open issues are fresh and currently unattended. No new releases were published. Overall project health appears stable with active development on both features and stability.

## 2. Releases

No new releases were published today. The most recent release remains unchanged.

## 3. Project Progress

Two PRs were closed/merged today:

- **#3018 (CLOSED) — RFC: temporal (incognito) sessions** — A vision-sharing RFC for throwaway, memory-free DM sessions. Closed as non-mergeable per `CONTRIBUTING.md` (features must be skills on `main`). Continued discussion expected in issues or a skill repo.
- **#3015 (CLOSED) — fix: preserve phase context in live progress** — Fixes a real E2E issue where Claude's first tool event could arrive before phase narration, causing orphaned "completed readings". Also addresses tool_result 60-character summaries being consumed by warnings, thus losing test pass counts. Now uses 1000-character sanitized summaries. 1267 tests pass.

**Active feature PRs still open:**

- **#2986 — Guard seam (phase 2)**: Every privileged action now passes through `guard()` (allow/hold/deny). Awaiting full review.
- **#2987 — `/add-audit` skill**: Opt-in local audit log for ncl surface. Rebased onto `feat/guard-seam`. Still open.
- **#2988 — One-door delivery for tasks**: `send_message` is the only path out of a task session, `to` is now required. Part 3/5 of scheduled-tasks train.
- **#3012 — Provider-agnostic persistent memory**: Adds shared memory tree across agent providers. Scaffolds memory index/definition per agent group.

## 4. Community Hot Topics

Both activity points today are fresh and have zero comments, so no discussion-heavy threads yet. However, the two open issues represent immediate user pain points:

- **#3016 — Rate limit logs as quota errors (even when allowed)** — Every `rate_limit_event` is logged as `[poll-loop] Error: Rate limit (retryable: false, quota)` even on successful turns. The user reports 82 instances in one week. This is a false-positive logging regression from PR #2965. Likely to attract attention soon.
  [GitHub Issue #3016](https://github.com/nanocoai/nanoclaw/issues/3016)

- **#3017 — Windows + VS 2026 + better-sqlite3 v11.10.0 compilation fails** — A platform-specific build blocker for Windows 11 users with Visual Studio 2026. Environment-constrained (Node v20/v24, Python 3.14.4). No resolution yet.
  [GitHub Issue #3017](https://github.com/nanocoai/nanoclaw/issues/3017)

## 5. Bugs & Stability

**High severity:**

- **#3017 — Windows compilation failure with VS 2026 + better-sqlite3 v11.10.0** — Full build blocker on modern Windows tooling. No workaround documented. No fix PR yet. Likely needs upstream dependency alignment or a build-script patch.
  [GitHub Issue #3017](https://github.com/nanocoai/nanoclaw/issues/3017)

**Medium severity:**

- **#3016 — False-positive quota error logging** — Every rate limit event (even allowed) logged as an error. Creates noise and potential alarm for subscription users. Regression from PR #2965. No fix PR yet.
  [GitHub Issue #3016](https://github.com/nanocoai/nanoclaw/issues/3016)

**Addressed today:**

- **#3019 (OPEN PR) — Stall watchdog for hung in-flight tools** — Fixes a real-world issue where the container was killed after 30 minutes of zero SDK activity (heartbeatAgeMs ≈ 1,800,000). The watchdog will detect and recover from hung tools before the absolute ceiling. Authored by Shufel83. Not yet merged.
  [GitHub PR #3019](https://github.com/nanocoai/nanoclaw/pull/3019)

- **#3020 (OPEN PR) — Rescue undelivered unwrapped replies after re-wrap nudge** — Fixes silent drops when the model omits `<message to>` wrapper after long tool chains. Also suppresses recap in these cases. Addresses #2369, #2393, and #2404. Not yet merged.
  [GitHub PR #3020](https://github.com/nanocoai/nanoclaw/pull/3020)

- **#3015 (CLOSED) — Phase context preservation** — Fixed race condition where first tool event could precede phase narration, and improved tool_result summaries to avoid losing test pass counts to warning text.
  [GitHub PR #3015](https://github.com/nanocoai/nanoclaw/issues/3015)

## 6. Feature Requests & Roadmap Signals

**Likely incoming (based on in-flight PRs):**

- **Persistent memory (#3012)**: Provider-agnostic persistent memory tree — appears in advanced review. Likely to land within 1-2 weeks.
- **Scheduled tasks delivery (#2988)**: One-door delivery (part 3/5). Once this train completes, scheduled tasks will have a unified delivery path.
- **Guard seam (#2986)**: Every privileged action goes through a single decision function. After merge, the security model will be centralized.
- **`/add-audit` skill (#2987)**: Opt-in local audit logging for ncl surface. Shows community demand for observability.

**RFC / vision signals:**

- **Temporal (incognito) sessions (#3018)**: Throwaway, memory-free DM sessions. Even though closed as non-mergeable RFC, the concept indicates interest in ephemeral, privacy-preserving interaction modes. Might appear as a skill or in a future minor release.

## 7. User Feedback Summary

**Pain points:**

- **Windows build failures**: VS 2026 + better-sqlite3 compilation blocks new Windows users (Issue #3017).
- **False-positive error logging**: Rate limit events logged as errors even when successful, causing confusion and alarm among subscription users (#3016). One user saw 82 occurrences in a week.
- **Undelivered replies after tool chains**: Silent drops when model omits wrapper after long tool chains (Addressed by PR #3020 but not yet merged).
- **Container kills from hung tools**: Real-world E2E issue where containers killed after 30 minutes of zero SDK activity (Addressed by PR #3019 but not yet merged).
- **Phase-context timing issue**: Claude's first tool event could arrive before phase narration, causing orphaned "completed readings" (Fixed in #3015, now merged).

**Satisfaction signals:**
- No direct positive feedback captured in today's issues/PRs.
- The number of open feature PRs from core team suggests sustained investment.

## 8. Backlog Watch

No long-unanswered issues or PRs were detected today. Both open issues are fresh (created 2026-07-11) and have zero comments — maintainers have not yet had time to respond. The PRs are all less than 3 days old and actively maintained. No items in the backlog exceed typical response windows.

**Items to monitor:**
- Issue #3016 (rate limit false positives) — regression from PR #2965; may need quick patch given the high annoyance factor.
- Issue #3017 (Windows build) — platform blocker affecting Windows 11 + VS 2026 users; may need build-script patch or dependency pinning.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-07-12**.

---

# NullClaw Project Digest
**Date:** 2026-07-12
**Source:** github.com/nullclaw/nullclaw

### 1. Today's Overview
NullClaw is currently in a **low-activity, maintenance-focused** phase. Over the past 24 hours, no new releases or pull requests have been merged, and the main repository has seen no code changes. The community is engaged in two open issues: a critical bug report regarding Telegram channel instability and a feature request for a new API provider. With zero merges and no new releases, the project appears to be in a period of triage or developer downtime, relying on existing stability to handle community concerns.

### 2. Releases
**None.** No new versions were released today.

### 3. Project Progress
**No pull requests** were updated, merged, or closed in the last 24 hours. There is no evidence of new features, bug fixes, or code changes being integrated into the main branch.

### 4. Community Hot Topics
Two issues are currently driving community discussion, though activity remains moderate.

- **#972 (Bug): Telegram channel stops responding after idle time**  
  *Author: i11010520 | Created: 2026-06-30 | Updated: 2026-07-11 | Comments: 3*  
  [View Issue](https://github.com/nullclaw/nullclaw/issues/972)  
  **Analysis:** This is the oldest ongoing issue and has the highest comment count. The user reports that the Telegram integration "dies" after a night of inactivity, although the backend (`nullclaw agent -m "ping"`) continues to work. The underlying need is **session persistence**: users need the Telegram bot to maintain long-lived connections without manual re-authentication or restart. This is a high-impact usability concern for anyone relying on NullClaw for hands-free daily operation.

- **#975 (Feature Request): Add `grok-cli` provider**  
  *Author: yanggf8 | Created: 2026-07-11 | Updated: 2026-07-11 | Comments: 1*  
  [View Issue](https://github.com/nullclaw/nullclaw/issues/975)  
  **Analysis:** The user requests a new provider that leverages the local `grok` CLI (a subscription-based chat interface). The rationale is to follow the same pattern used for `claude-cli`, `codex-cli`, and `gemini-cli`. This signals that the community is actively seeking **unmetered or subscription-based model access** through local CLI tools, likely to avoid API usage costs or rate limits.

### 5. Bugs & Stability
One active bug is reported, with medium-to-high severity due to its impact on primary user workflows.

- **#972: Telegram channel stops responding after idle time**  
  **Severity:** High (affects core communication channel, disrupts daily use)  
  **Status:** Open, no fix PR exists.  
  **Details:** The Telegram channel dies silently after hours of inactivity. The backend remains functional, suggesting a **connection timeout or session expiry** issue in the Telegram client adapter.  
  **Recommendation:** Priority attention required, as this undermines the reliability of one of NullClaw’s primary interfaces.

No crashes or regressions were reported in the last 24 hours.

### 6. Feature Requests & Roadmap Signals
The only feature request is **Issue #975** (Grok CLI provider).  
**Prediction:** Given that NullClaw already supports three similar CLI-based providers (`claude-cli`, `codex-cli`, `gemini-cli`), adding `grok-cli` is a low-effort, high-utility addition. It is likely to be accepted in the next minor release, as it aligns with the project’s existing architecture (`src/provider_probe.zig:43`) and addresses a clear user desire for low-cost AI access.

### 7. User Feedback Summary
- **Pain Points:** The Telegram idle disconnection (Issue #972) is the most prominent source of user dissatisfaction. Users find it frustrating that the backend is alive but the bot is unresponsive, requiring a full restart.
- **Use Cases:** The feature request for Grok CLI (Issue #975) highlights a user base that prefers running AI models through local CLI sessions (likely to avoid API fees) rather than using direct cloud APIs.
- **Satisfaction:** No positive feedback or closed issues indicate satisfied users; the mood is neutral with a slight tilt toward unmet needs.

### 8. Backlog Watch
- **Issue #972 (Telegram bug).**  
  *Created: 2026-06-30 | Last Updated: 2026-07-11*  
  **Status:** Open with 3 comments, no maintainer assignment.  
  **Watch reason:** This issue has been open for 12 days with no maintainer response or fix PR. It is the most critical item in the backlog. Continued silence from the team risks user churn from Telegram users and erodes trust in the project’s responsiveness. A maintainer comment or triage label is overdue.

No other long-unanswered or stalled items were identified.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-12

## 1. Today's Overview
IronClaw saw **high activity** over the past 24 hours with **50 pull requests updated** (15 merged/closed, 35 still open) and **8 issues updated** (7 open, 1 closed). The project had **no new releases**. The activity is dominated by the ongoing **extension-runtime train** (PR #5995, #5996 — phases P1/P2 of an 8-PR series) and a wave of **reliability/UX fixes** from `ironloopai[bot]` contributors (PRs #5906–#5914). Three critical **platform gaps** surfaced from user `Anubhav-Koul`: Windows incompatibility in the `local-dev-yolo` profile, an MCP transport dead-end for local servers, and the absence of a security reporting channel. A daily failure taxonomy (#5992) indicates that benchmark defects, not model quality, dominate current test failures.

---

## 2. Releases
**None.** No new releases were published in the last 24 hours. The open release PR #5598 (which would bump `ironclaw_common` to 0.5.0, `ironclaw_skills` to 0.4.0, and `ironclaw` to 0.29.1 with API breaking changes) remains unmerged and unlabeled as ready.

---

## 3. Project Progress
**15 PRs merged/closed** in the last 24 hours. Notable merged items:

### Merged/Closed
- **[#6003](https://github.com/nearai/ironclaw/pull/6003) [CLOSED]** — `ci: route workflows to ci-standard runner` — Infrastructure change replacing `ubuntu-latest-8-cores` with `ci-standard` runner label, improving pilot artifact build caching/error handling. Spans 18 scope tags; appears to be a major CI consolidation.
- **[#5997](https://github.com/nearai/ironclaw/pull/5997) [CLOSED]** — `test(e2e): address Emulate fixture review` — Follow-up fixes for the Emulate fixture suite (#5989), addressing automated review feedback from Gemini and CodeRabbit (defensive parsing, fixture token selection, Drive file ownership).
- **[#5951](https://github.com/nearai/ironclaw/pull/5951) [CLOSED]** — `fix(llm): recover near.ai streaming tool-call args with trailing content` — Fixes a bug where streaming tool calls from reasoning models (e.g. DeepSeek-V4-Flash) lost arguments if a stray token appeared after a complete arguments object. Author: `khorolets` (new contributor).
- **[#5969](https://github.com/nearai/ironclaw/issues/5969) [CLOSED]** — `[bug] GLM-5.2 not available in opencode default model list` — was resolved, though the fix commit is not linked in the issue data.

### Features and Fixes Advanced (Open PRs)
- **Extension-runtime train** progressing: **#5995 (P1)** — manifest v3, VendorId, recipes, resolved record; **#5996 (P2)** — adapters, ExtensionHost, tool-dispatch cutover.
- **Queued-message steering** [#5981](https://github.com/nearai/ironclaw/pull/5981) — allows messages to busy threads to be queued (not rejected), with WebUI visibility.
- **Responses API coverage** [#5991](https://github.com/nearai/ironclaw/pull/5991) — requiring full Responses API E2E test suite in PR CI.
- **Agent guidance Reborn-native** [#6001](https://github.com/nearai/ironclaw/pull/6001) — rewrote root AGENTS.md and `.claude/rules` to reflect Reborn architecture.
- **Google OAuth token refresh** [#6004](https://github.com/nearai/ironclaw/pull/6004) — infrastructure for canary sharding with per-run token refresh.
- **Scope-admin secrets** [#5934](https://github.com/nearai/ironclaw/pull/5934) — admin-provisioned secrets scoped to default agent.

---

## 4. Community Hot Topics
### Most Active Issues
| Issue | Author | Comments | Status | Topic |
|-------|--------|----------|--------|-------|
| [#5969](https://github.com/nearai/ironclaw/issues/5969) | sergeiest | 1 | CLOSED | GLM-5.2 model missing from opencode defaults |
| [#6000](https://github.com/nearai/ironclaw/issues/6000) | Anubhav-Koul | 0 | OPEN | No security reporting channel (no SECURITY.md, private reporting disabled) |
| [#5999](https://github.com/nearai/ironclaw/issues/5999) | Anubhav-Koul | 0 | OPEN | Windows: `local-dev-yolo` broken by POSIX path assumption |
| [#5998](https://github.com/nearai/ironclaw/issues/5998) | Anubhav-Koul | 0 | OPEN | No transport for local MCP server (stdio rejected, loopback HTTP denied) |
| [#5987](https://github.com/nearai/ironclaw/issues/5987) | sergeiest | 0 | OPEN | Request: easy local proxy for private inference with attestation |

### Analysis
The community's attention is **concentrated on platform limitations**: Windows support failure (#5999), local MCP development dead-end (#5998), and missing security infrastructure (#6000) — all from user `Anubhav-Koul`. These are **fundamental platform gaps** that block entire categories of developers from using IronClaw. A secondary cluster (#5969, #5987) reflects **configuration complexity pain** — users wanting simpler setup for local inference and model availability. Issue #6000 has **no maintainer response**, which is notable given its security severity.

### Most Active PRs
No PRs have visible comment counts above 1. The most complex PRs by size/scope are:
- [#5996](https://github.com/nearai/ironclaw/pull/5996) (XL, medium risk) — extension-runtime P2
- [#5995](https://github.com/nearai/ironclaw/pull/5995) (XL, low risk) — extension-runtime P1
- [#5981](https://github.com/nearai/ironclaw/pull/5981) (XL, low risk) — queued-message steering
- [#5965](https://github.com/nearai/ironclaw/pull/5965) (XL, low risk) — recoverable errors reach model via detail channel

---

## 5. Bugs & Stability
### Ranked by Severity

**CRITICAL** — Platform blockers:
1. **[#6000](https://github.com/nearai/ironclaw/issues/6000) — No security reporting channel** — User has a potential security finding in Reborn runtime but cannot report privately. No SECURITY.md, private vulnerability reporting disabled. **No fix PR.** *Severity: Critical.*
2. **[#5999](https://github.com/nearai/ironclaw/issues/5999) — `local-dev-yolo` broken on Windows** — Host filesystem paths cannot satisfy MountAlias POSIX requirement, making local development impossible on Windows. **No fix PR.** *Severity: Critical (platform-excluding).*
3. **[#5998](https://github.com/nearai/ironclaw/issues/5998) — No transport for local MCP server** — `stdio` rejected, `http://127.0.0.1` refused; local MCP servers completely unreachable. **No fix PR.** *Severity: High (blocks MCP development/testing).*

**HIGH** — Functional defects:
4. **[#5969](https://github.com/nearai/ironclaw/issues/5969) [CLOSED] — GLM-5.2 missing from opencode defaults** — Resolved, but indicates model availability gaps in default configurations.
5. **[#5968](https://github.com/nearai/ironclaw/issues/5968) — HTTP tool fails with third-party APIs without MCP** — Generic HTTP tool returns non-descriptive errors, no auth/egress support for non-MCP services (e.g. Attio). **No fix PR.** *Severity: Medium.*

**MEDIUM** — Reliability:
6. **[#5992](https://github.com/nearai/ironclaw/issues/5992) — Daily failure taxonomy 2026-07-11** — Clawbench run: 138 non-pass tests, ~77+ failures attributed to **benchmark defects** (not model quality). Signals test infrastructure quality issues.

**FIXES MERGED:**
- `fix(llm): recover near.ai streaming tool-call args with trailing content` ([#5951](https://github.com/nearai/ironclaw/pull/5951)) — Fixes tool-call argument loss with reasoning models.

---

## 6. Feature Requests & Roadmap Signals
### User-Requested Features
| Issue | Request | Likely Timeline |
|-------|---------|-----------------|
| [#5987](https://github.com/nearai/ironclaw/issues/5987) | Easy local proxy service for private inference (CVM attestation proxy) | **Unlikely next version** — large feature, no PR |
| [#5968](https://github.com/nearai/ironclaw/issues/5968) | HTTP tool support for third-party APIs without MCP (auth/egress) | **Possible mid-term** — gaps in generic HTTP tool affect many users |
| [#5998](https://github.com/nearai/ironclaw/issues/5998) | Local (on-device) MCP server transport support | **High priority** — blocks MCP development workflow |

### Internal Roadmap Signals
- **Extension-runtime train** (PRs #5995, #5996) is the most significant architectural work in progress — 8-PR series for extension manifest v3, adapters, and dispatch cutover.
- **Responses API** is being hardened: PR #5991 requires full test coverage; #5990 tracks remaining gaps (lifecycle safety, external-tool gaps).
- **Queued-message steering** ([#5981](https://github.com/nearai/ironclaw/pull/5981)) is a UX improvement for busy threads (queue instead of reject).
- **Recoverable errors to model** ([#5965](https://github.com/nearai/ironclaw/pull/5965)) — architectural change making errors visible to the model for better self-correction.

### Prediction
The **extension-runtime** and **Responses API hardening** will likely land in the next release (0.29.x or 0.30.x). The **Windows support gap** (#5999) and **local MCP transport** (#5998) are likely blockers for near-term developer adoption and may be addressed urgently given the severity of user reports.

---

## 7. User Feedback Summary
### Pain Points
- **Configuration complexity**: Users find NEAR AI attestation docs too complex (#5987), and models like GLM-5.2 require manual configuration in opencode (#5969).
- **Platform lock-out**: Windows users completely blocked from local development (#5999).
- **Missing developer infrastructure**: No local MCP server support (#5998), no security reporting channel (#6000).
- **Generic HTTP tool inadequate**: Cannot connect to third-party APIs without dedicated MCP integration (#5968).
- **Benchmark noise**: Daily failure taxonomy (#5992) suggests test infrastructure problems are wasting contributor time.

### Satisfaction Signals
- **Streaming tool-call fix merged** (#5951) — a specific user pain point with reasoning models losing arguments was addressed.
- **Active UX polish**: Multiple `ironloopai[bot]` PRs (#5906–5914) fixing UI issues with failure banners, tool activity visibility, chat history pagination, trigger creation display — indicates ongoing investment in user experience.
- **Recoverable errors now model-visible** (#5965) — architectural improvement that should help models self-correct rather than retrying blind.

### User Profile
The three issues from `Anubhav-Koul` (#5998, #5999, #6000) read as a **single developer's integration experience** — attempting to set up IronClaw Reborn on Windows with a local MCP server, then finding a security vulnerability. This mirrors a real-world "developer gets blocked at every turn" scenario.

---

## 8. Backlog Watch
### Issues Needing Maintainer Attention
| Issue | Age | Author | Problem |
|-------|-----|--------|---------|
| **[#6000](https://github.com/nearai/ironclaw/issues/6000)** | 1 day | Anubhav-Koul | **No response** — User has an unmitigated security finding in Reborn runtime. No SECURITY.md, private reporting disabled. **Critical.** |
| **[#5999](https://github.com/nearai/ironclaw/issues/5999)** | 1 day | Anubhav-Koul | Zero comments — Windows platform blocker. |
| **[#5998](https://github.com/nearai/ironclaw/issues/5998)** | 1 day | Anubhav-Koul | Zero comments — Local MCP server transport blocker. |
| **[#5987](https://github.com/nearai/ironclaw/issues/5987)** | 1 day | sergeiest | Zero comments — Feature request for local attestation proxy. |
| **[#5968](https://github.com/nearai/ironclaw/issues/5968)** | 2 days | sergeiest | Zero comments — HTTP tool gap with third-party APIs. |

### Long-Open PRs Needing Review
| PR | Age | Subject |
|----|-----|---------|
| **[#5598](https://github.com/nearai/ironclaw/pull/5598)** | **9 days** | Release PR (bumps 4 crates, breaking changes in 2) — still open, not labeled ready. |

### Assessment
The **new user onboarding experience** is fragile: `Anubhav-Koul` reported 3 separate platform/protocol/show-stoppers in a single day with **no maintainer responses on any**. This signals a **community response gap** for incoming developers. The **release PR has been open 9 days** without progression — the next tagged release is overdue. The **daily failure taxonomy** (#5992) being generated suggests the team is actively monitoring CI health, but the infrastructure issues (benchmark defects dominating failures) remain unresolved. **Security vulnerability disclosure** (#6000) is the most urgent item requiring immediate attention.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-07-12**, generated from the provided GitHub data.

---

# LobsterAI Project Digest — 2026-07-12

## 1. Today's Overview
The project is currently in a **low-activity maintenance phase**. There are **no new releases** today, and only **3 Issues and 1 PR** have been updated in the past 24 hours, none of which were closed or merged. All tracked work items remain **open** and have been marked as `stale`, indicating they have not received maintainer attention for several months. The most recent code update activity appears to have stalled since April 2026, suggesting the core team may be focusing on internal development or a larger upcoming release.

## 2. Releases
**None.** No new versions have been published. The most recent user-reported version is `v2026.4.1` (mentioned in Issue #1329).

## 3. Project Progress
**No PRs were merged or closed today.** The only open PR (#1327) remains unchanged and unmerged since April 2, 2026. This PR implements the "ToolUse batch expand/collapse" feature, which is directly linked to Issue #1326. Without maintainer review or merge, this feature has not advanced into the main codebase.

## 4. Community Hot Topics
The three most active (and only) updated Issues are all from early April 2026, with exactly **one comment each** and **zero reactions**. None have received recent engagement.

- **#1326 – ToolUse batch expand/collapse** ([Link](https://github.com/netease-youdao/LobsterAI/issues/1326))
  - *Author:* MaoQianTu | *Comments:* 1 | *Reactions:* 0
  - *Analysis:* This request targets UX friction in cowork sessions. The underlying need is reducing repetitive manual clicking when an AI response invokes multiple tool blocks. It implies users are frequently running multi-tool workflows.

- **#1330 – Error status red dot badge for session list** ([Link](https://github.com/netease-youdao/LobsterAI/issues/1330))
  - *Author:* MaoQianTu | *Comments:* 1 | *Reactions:* 0
  - *Analysis:* Users want immediate visual feedback for session failures. The lack of such indicators suggests debugging or monitoring workflows are currently cumbersome, particularly in high-volume session environments.

- **#1329 – Scheduled task notification channel empty** ([Link](https://github.com/netease-youdao/LobsterAI/issues/1329))
  - *Author:* gongfen0121 | *Comments:* 1 | *Reactions:* 0
  - *Analysis:* A clear functional bug. Users cannot configure notification channels for scheduled tasks, severely limiting the utility of the scheduler. This indicates a missing UI binding or an incomplete database migration.

## 5. Bugs & Stability
| Issue | Severity | Status | Fix PR Exists? | Description |
|-------|----------|--------|----------------|-------------|
| [#1329](https://github.com/netease-youdao/LobsterAI/issues/1329) – Scheduled task notification channel empty | **High** – Core feature broken (scheduler unusable) | Open / Stale | No | New scheduled tasks offer zero valid notification options; only "no notification" is selectable. |
| No crash or regression reports were filed today. | – | – | – | – |

**Assessment:** Only one bug was re-discussed today, but it is a **functional blocker** for users relying on the scheduler. With no fix PR attached and the issue stale since April, this is a growing risk for user retention.

## 6. Feature Requests & Roadmap Signals
Two actionable feature requests remain open, both authored by **MaoQianTu**:

1. **Batch expand/collapse for ToolUse blocks** ([#1326](https://github.com/netease-youdao/LobsterAI/issues/1326) / PR [#1327](https://github.com/netease-youdao/LobsterAI/pull/1327))
   - *Prediction:* Likely to land in the next version if the maintainers pick up the existing, ready-to-merge PR. High probability for `v2026.8.x`.

2. **Error status red dot badge in session list** ([#1330](https://github.com/netease-youdao/LobsterAI/issues/1330))
   - *Prediction:* Lower probability unless there is a broader UI polish pass. No PR exists yet.

These two features together suggest the community is pushing for **better real-time observability and multi-step AI interaction ergonomics**.

## 7. User Feedback Summary
- **Pain Points:**
  - Repeated clicking to expand/collapse multi-tool AI responses (Issue #1326).
  - Inability to spot errored sessions without manually opening each one (Issue #1330).
  - Scheduled tasks are functionally incomplete, limiting automation use cases (Issue #1329).

- **Satisfaction Signals:** Minimal positive feedback observed. The lack of reactions or follow-up comments may indicate user fatigue or a small active community base.

- **Implicit Need:** Users are using LobsterAI for **complex, multi-step AI workflows** and **automated scheduling**, but the UI is lagging behind these usage patterns in both feedback and reliability.

## 8. Backlog Watch
All tracked items are over **3 months old** and are officially `stale`. They require urgent maintainer attention:

| Item | Type | Age (Days) | Last Updated | Why Important |
|------|------|------------|--------------|---------------|
| [#1329](https://github.com/netease-youdao/LobsterAI/issues/1329) – Notification channel empty | Bug | 101 | 2026-07-11 | Blocks a core product feature (scheduler); likely a simple UI state bug. |
| [#1326](https://github.com/netease-youdao/LobsterAI/issues/1326) – ToolUse batch toggle | Feature | 101 | 2026-07-11 | Has a draft PR (#1327) attached, meaning work is already done — only review and merge are missing. |
| [#1330](https://github.com/netease-youdao/LobsterAI/issues/1330) – Error state badge | Feature | 101 | 2026-07-11 | Low implementation complexity but high user value for debugging. |
| [#1327](https://github.com/netease-youdao/LobsterAI/pull/1327) – PR for #1326 | PR | 101 | 2026-07-11 | Open, unmerged, uncommented by maintainers. Code changes are fully written. |

**Recommendation:** The project would benefit from a **stale-clearance sprint** to merge the ready PR and resolve at least the highest-severity bug (#1329) before the user base loses confidence in the scheduler feature.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest – 2026-07-12**

---

### 1. Today's Overview
Project activity was extremely light over the last 24 hours, with no new issues, no releases, and zero closed or merged pull requests. The sole event was a single open pull request submitted yesterday and updated today. This low activity suggests the team may be in a quiet maintenance cycle or preparing for a larger update. Overall project health appears stable but warrants closer observation for emerging blockers.

---

### 2. Releases
No new releases were published in the last 24 hours. The latest available release remains the previous version (no release data provided).

---

### 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The only open PR is:
- **#1147** [OPEN] `fix(caldav): honor time range in list_events via server-side calendar-query` – Author: thoscut  
  This PR addresses a functional bug in the CalDAV client where `start`/`end` parameters were bound but never used, causing every resource to be fetched regardless of the requested time range. The fix implements proper server-side calendar-query filtering. This represents an important correctness improvement but has not yet been merged.

---

### 4. Community Hot Topics
There are no highly active discussions today. The only open item, **PR #1147** ([link](https://github.com/moltis-org/moltis/pull/1147)), has zero comments and zero reactions, indicating it has not yet attracted community review or feedback. The underlying need is for proper CalDAV date-range filtering, which is critical for users relying on calendar event tools.

---

### 5. Bugs & Stability
One bug was reported and addressed via PR today:
- **CalDAV `list_events` ignoring time range** (severity: **High**) – The `_range` parameter was bound but never used, making `start`/`end` parameters ineffective. This contradicts documentation and could cause performance issues when fetching large calendars.  
  **Fix status:** PR #1147 exists but remains open and unmerged. No confirmation yet of testing or validation.

No crashes, regressions, or other bugs were reported in the last 24 hours.

---

### 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. The only actionable item is the bug fix in PR #1147, which is a correction rather than a new feature. No roadmap signals or user-requested features were observed. If the team is prioritizing CalDAV reliability, this fix could be part of a near-term patch release.

---

### 7. User Feedback Summary
No user feedback, pain points, or satisfaction signals were recorded in the last 24 hours. The absence of new issues may indicate either user satisfaction or low engagement. The open PR suggests at least one contributor identified a significant discrepancy between documentation and behavior, which could imply user frustration with that feature.

---

### 8. Backlog Watch
No older issues or PRs are flagged as needing maintainer attention in the provided data. However, **PR #1147** ([link](https://github.com/moltis-org/moltis/pull/1147)) is the only item requiring review and merge. It has been open for one day with no comments, so it is not yet backlogged, but prompt maintainer review would be prudent to validate the fix and address the functional gap.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-12

## 1. Today's Overview
CoPaw is currently in a **high-pressure stabilization phase** following the v2.0.0 release. The project has **23 open issues**, all created or updated in the last 24 hours, with **zero closed issues** — an unusually high open-to-closed ratio that signals a backlog in triage. Seven PRs were updated today: **4 merged/closed** (all fixing dark mode contrast) and **3 still open**. No new releases were published. The community is **actively reporting regressions across core subsystems** — sandbox, context compression, memory, session recovery, and channel integration — indicating the v2.0.0 release introduced widespread breakage that has not yet been addressed by maintainers.

## 2. Releases
**No new releases today.** The last known release is **v2.0.0**, which is the subject of most bug reports.

## 3. Project Progress
Four PRs were merged/closed today, all by contributor **Marlin-Phone**, all addressing the same issue:

| PR | Status | Description |
|---|---|---|
| [#5970](https://github.com/agentscope-ai/QwenPaw/pull/5970) | **Merged** | Fix dark mode text contrast for loop templates and chat history (Closes #5969) |
| [#5971](https://github.com/agentscope-ai/QwenPaw/pull/5971) | **Merged** | Same fix, iteration addressing Copilot review suggestions |
| [#5973](https://github.com/agentscope-ai/QwenPaw/pull/5973) | **Merged** | Same fix, refined CSS scoping |
| [#5974](https://github.com/agentscope-ai/QwenPaw/pull/5974) | **Merged** | Same fix, final version |

No other functional features advanced today. **The v2.0.0 regression wave remains unaddressed by maintainers.**

## 4. Community Hot Topics
The most active discussions reveal deep frustration with v2.0.0 regressions:

- **[#5951](https://github.com/agentscope-ai/QwenPaw/issues/5951) — Windows sandbox pwsh recursion explosion** (7 comments)  
  User reports that `execute_shell_command` triggers infinite pwsh window spawning, memory exhaustion, and no way to disable the sandbox. This is the **most severe bug** currently open. The author claims the sandbox initialization in v2.0.0 is fundamentally broken.

- **[#5788](https://github.com/agentscope-ai/QwenPaw/issues/5788) — Skills list stuck at 20 items** (4 comments)  
  Progressive rendering via `IntersectionObserver` fails when the page container has CSS overflow restrictions. A fix PR ([#5968](https://github.com/agentscope-ai/QwenPaw/pull/5968)) is open from first-time contributor **feng183043996**.

- **[#4124](https://github.com/agentscope-ai/QwenPaw/issues/4124) — OAuth login for OpenAI / Codex** (4 comments)  
  A long-standing feature request (since May 2026) for OAuth-based provider authentication. No maintainer response visible.

- **[#5961](https://github.com/agentscope-ai/QwenPaw/issues/5961) — v2.0.0 infinite write/delete loop with Qwen3.7+** (3 comments)  
  Agent repeatedly writes and deletes files without completing tasks. Suggests a feedback-loop bug in the agent loop logic for the new model version.

**Underlying need**: The community is **desperate for a v2.0.0 hotfix release**. Multiple issues describe the tool as "almost unusable" after upgrade.

## 5. Bugs & Stability
**Severity: Critical (6 issues)**

| Issue | Description | Severity | Fix PR? |
|---|---|---|---|
| [#5951](https://github.com/agentscope-ai/QwenPaw/issues/5951) | Windows sandbox pwsh recursion, memory 20GB cap, cannot disable | **Critical** — tool unusable | None |
| [#5960](https://github.com/agentscope-ai/QwenPaw/issues/5960) | Context compression splits tool_call/tool_result pairs → API 400 | **Critical** — breaks all long conversations | None |
| [#5962](https://github.com/agentscope-ai/QwenPaw/issues/5962) | WeChat channel orphaned tool_result after scroll eviction → 400 | **Critical** — all WeChat sessions fail | None |
| [#5972](https://github.com/agentscope-ai/QwenPaw/issues/5972) | heartbeat recovery loads stale session, tool messages orphaned → 400 | **Critical** — session recovery broken | None |
| [#5963](https://github.com/agentscope-ai/QwenPaw/issues/5963) | `execute_shell_command` hard-capped at 60s, ignore config | **High** — long commands silently fail | None |
| [#5961](https://github.com/agentscope-ai/QwenPaw/issues/5961) | v2.0.0 + Qwen3.7+ infinite write/delete loop | **High** — tasks never complete | None |
| [#5952](https://github.com/agentscope-ai/QwenPaw/issues/5952) | auto-memory fails: missing module `_scripts` | **High** — memory summarization broken | None |
| [#5965](https://github.com/agentscope-ai/QwenPaw/issues/5965) | PyInstaller backend missing `_scripts` submodule → Glob tool crashes | **High** — bundled Windows app broken | None |
| [#5967](https://github.com/agentscope-ai/QwenPaw/issues/5967) | Pydantic error on `parse_legacy_memory_state` after v2.0.0 upgrade | **High** — data incompatibility | None |
| [#5964](https://github.com/agentscope-ai/QwenPaw/issues/5964) | Chat list/conversation mapping lost after v2.0.0 upgrade | **High** — sessions inaccessible (500 error) | None |
| [#5956](https://github.com/agentscope-ai/QwenPaw/issues/5956) | DingTalk sessions with legacy file tool results fail to load (Pydantic error) | **High** — channel migration broken | None |
| [#5950](https://github.com/agentscope-ai/QwenPaw/issues/5950) | Chinese memory files trigger embedding 400 (char vs token truncation) | **Medium** — non-English users affected | None |
| [#5955](https://github.com/agentscope-ai/QwenPaw/issues/5955) | Skills UI: only 20 shown, disabled skills hidden (duplicate of #5788) | **Low** — UI only | [#5968](https://github.com/agentscope-ai/QwenPaw/pull/5968) |
| [#5969](https://github.com/agentscope-ai/QwenPaw/issues/5969) | Dark mode text contrast unreadable | **Low** — UI only | **Fixed** in 4 PRs |
| [#5977](https://github.com/agentscope-ai/QwenPaw/issues/5977) | Plugin HTTP routes lost after workspace hot-reload | **Medium** — plugin stability | None |

**Alarm**: **Six critical-severity regressions** with no maintainer fix PRs. The v2.0.0 release appears to have shipped with multiple fundamental flaws in context management, sandbox, and data migration.

## 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. Existing requests show **no maintainer engagement**:

- **[#4124](https://github.com/agentscope-ai/QwenPaw/issues/4124) — OAuth login for OpenAI/Codex** (open 65 days, no response)
- **[#5976](https://github.com/agentscope-ai/QwenPaw/issues/5976) — Separate control for channel tool-call parameters vs results** (new, 1 comment)  
  User wants tool-result truncation (show first/last N lines) to reduce channel noise. Low complexity — likely for next minor release.

**Prediction**: The next release (v2.0.1 or v2.1.0) will be a **stabilization-only hotfix** addressing the context compression bug (#5960) and the sandbox recursion (#5951). Feature development is frozen until regressions are resolved.

## 7. User Feedback Summary
**Strong dissatisfaction** with the v2.0.0 upgrade experience:

> *"升级到最新版 QwenPaw 桌面壳后，沙箱实现存在严重且无法关闭的问题，导致整个工具几乎不可用。"*  
> — After upgrading to latest QwenPaw desktop, the sandbox has a severe, uncloseable problem making the tool almost unusable. (#5951)

> *"搭配qwen3.7-plus模型使时，发现智能体总会反反复复的写入、删除、写入、删除，很长时间也不能完成一个简单任务！"*  
> — With qwen3.7-plus, the agent repeatedly writes, deletes, writes, deletes… a simple task never completes. (#5961)

> *"升级到 2.0.0 后之前的部分聊天会话在 Web UI 中打不开，点击后返回 500 错误。"*  
> — After upgrade, some chat sessions return 500 error when opened. (#5964)

> *"用户说升级到 2.0 后企业微信报错 '/Internal error'"*  
> — User says WeChat Work shows "/Internal error" after upgrading to 2.0. (#5957)

**Positive signal**: Multiple first-time contributors are submitting fixes (#5968, #5970–5975), indicating an **engaged OSS community** willing to help stabilize the release.

## 8. Backlog Watch
The following issues require **immediate maintainer attention** but show no activity:

| Issue | Age | Topic | Risk |
|---|---|---|---|
| [#5951](https://github.com/agentscope-ai/QwenPaw/issues/5951) | 2 days | Windows sandbox recursion (critical) | **High** — Windows users blocked |
| [#5960](https://github.com/agentscope-ai/QwenPaw/issues/5960) | 1 day | Context compression corrupts tool_call pairing | **High** — all long sessions broken |
| [#5952](https://github.com/agentscope-ai/QwenPaw/issues/5952) | 2 days | Missing `_scripts` module in auto-memory | **High** — memory broken after upgrade |
| [#4124](https://github.com/agentscope-ai/QwenPaw/issues/4124) | 65 days | OAuth authentication for providers | **Medium** — pending feature request |
| [#2664](https://github.com/agentscope-ai/QwenPaw/issues/2664) | 103 days | Intel Mac support | **Low** — unanswered question |

**Overall project health**: ⚠️ **Concerning**. v2.0.0 introduced multiple critical regressions in sandbox, context management, data migration, and channel integration. The community is actively reporting but maintainer response has been absent on all serious bugs today. The strong contributor activity on UI fixes is a positive sign, but **a hotfix release is urgently needed** to restore trust.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-12

## Today's Overview

ZeroClaw continues at high velocity with **50 open issues** and **46 open pull requests** updated in the last 24 hours, and **4 PRs merged/closed**. No new releases were published today. The project remains heavily focused on foundational architecture work—particularly around the **goal-mode implementation split** (tracker #8681), **WASM-first plugin runtime** (RFC #8135), and **persistent memory subsystem parity** (tracker #8891). Activity is dominated by large cross-cutting feature PRs, critical bug fixes for provider streaming and memory growth, and a significant surge in Quickstart onboarding improvements. The zero-code (#zerocode) and web gateway surfaces show intense development, with 6+ PRs targeting the Quickstart experience alone.

## Releases

**None.** No new releases were published in the last 24 hours.

## Project Progress

**Merged/Closed PRs (4):** Details were not enumerated in the data sample, but the project saw PR activity closing out documentation fixes and small bugfixes. Key advances visible from open PRs:

- **Inkbox native channel** (PR #8384) — a massive XL-sized PR adding email, SMS, voice, and iMessage channel support with Quickstart onboarding
- **SSE streaming idle timeout fix** (PR #8838) — an XL-sized fix bounding all SSE streaming paths with per-read idle timeouts, critical for local runtime stability
- **Gemini thought signature preservation** (PR #8935) — fixes multi-turn tool workflows where Gemini rejected follow-up requests due to missing `extra_content` in tool-call history
- **Hindsight memory backend** (PR #8992) — adds a new first-class external HTTP memory backend for delegated persistence and vectorization
- **Declarative skill auto-activation** (PR #8965) — skills can now self-activate on inbound channel messages via triggers, provider switches, and image-turn tool blocking
- **SOP channel gate prompts** (PR #8979) — deterministic SOP building blocks for approval-gated pipelines without live agent turns
- **Quickstart subscription auth modes** (PRs #8980, #8981) — inline CLI subscription auth for OpenAI/Anthropic, normalizing model-provider aliases

## Community Hot Topics

### Most Active Issues (by comment count)

1. **[#8681] [Tracker]: Goal mode implementation split stack** (9 comments)  
   [zeroclaw-labs/zeroclaw Issue #8681](zeroclaw-labs/zeroclaw Issue #8681)  
   *This tracker coordinates splitting the accepted goal-mode implementation into reviewable PRs. The community and maintainers are aligning on how to break a large feature into digestible, reviewable chunks.*

2. **[#8054] System prompt tool-availability should match per-turn effective tools across all entry points** (9 comments)  
   [zeroclaw-labs/zeroclaw Issue #8054](zeroclaw-labs/zeroclaw Issue #8054)  
   *A high-risk P1 bug where reasoning models receive "No tools are available" in the system prompt while native/MCP tools are present. The fix for the direct runtime path (#8053) is merged, but the same mismatch exists across WebSocket, gateway, multimodal, and /think entry points.*

3. **[#5808] Default 32k context budget is exceeded by system prompt + tool definitions on iteration 1** (8 comments)  
   [zeroclaw-labs/zeroclaw Issue #5808](zeroclaw-labs/zeroclaw Issue #5808)  
   *A workflow-blocking S1 bug where the very first LLM iteration exceeds the default 32k context budget by ~3.3x, causing perpetual preemptive trimming. This is a long-standing pain point (April 2026) that continues to frustrate users.*

### Most Active Pull Requests

- **PR #8384** (Inkbox channel) — XL-sized with heavy community engagement around onboarding
- **PR #8838** (SSE idle timeout) — XL-sized, addresses a critical local runtime stability issue
- **PR #8987** (capability-safe runtime defaults for Quickstart) — L-sized, recommended defaults for providers
- **PR #8979** (SOP channel gate prompts) — XL-sized, new deterministic pipeline capability

### Underlying Needs

The most active discussions reveal three core community demands: (1) **reliable local inference** with proper timeout handling, (2) **context budget that works out-of-the-box** without manual tuning, and (3) **consistent tool availability messaging** across all entry points and providers. The tool-availability issue (#8054) is a particularly sensitive pain point because it misleads reasoning models into refusing to use tools that are actually available.

## Bugs & Stability

### Critical (S1 — Workflow Blocked)

- **[#5808] Default 32k context budget exceeded on first iteration** — Perpetual preemptive trim, 8 comments, open since April 2026. [Issue #5808](zeroclaw-labs/zeroclaw Issue #5808)
- **[#8675] Malformed native tool-call arguments sent unvalidated to OpenAI-format providers** — Provider 400 error, empty reply, 1 comment. [Issue #8675](zeroclaw-labs/zeroclaw Issue #8675)

### High (S2 — Degraded Behavior)

- **[#8654] Skill-review fork panics with out-of-range slice → daemon SIGSEGV** — Crashes the entire agent process after tool-heavy turns. [Issue #8654](zeroclaw-labs/zeroclaw Issue #8654)
- **[#8731] Stdio-based MCP servers accumulating as zombie processes** — Sub-processes not cleanly reaped, accumulating under active daemon PIDs. [Issue #8731](zeroclaw-labs/zeroclaw Issue #8731)
- **[#8642] MCP/tool-schema cloning drives unbounded RSS growth** — Memory leak in the agent loop, split from OOM root-cause tracker #5542. [Issue #8642](zeroclaw-labs/zeroclaw Issue #8642)
- **[#6350] WhatsApp Web allowed-numbers bypassed for LID-based contacts** — Silent message drops, open since May 2026. [Issue #6350](zeroclaw-labs/zeroclaw Issue #6350)
- **[#8578] Daemon fails to terminate process on startup failure** — Leaves orphaned zerocode process. [Issue #8578](zeroclaw-labs/zeroclaw Issue #8578)

### Notable Fix PRs in Progress

- **PR #8838** (SSE idle timeout) — directly addresses the "provider 400 → empty reply" pattern from #8675
- **PR #8845** (rebuild live sessions on model_provider edits) — fixes a config refresh gap
- **PR #8751** (LocalWhisperConfig defaults) — fixes serde defaults that left fields at 0
- **PR #8759** (clipboard screenshot paste reliability) — fixes intermittent image drop on Wayland

### Risk Assessment

Six issues carry the `risk:high` label: #8654 (skill-review SIGSEGV), #8731 (zombie MCP processes), #8642 (unbounded RSS growth), #8054 (tool-availability mismatch), #5808 (context budget overflow), and #6350 (WhatsApp silent drops). The SIGSEGV and memory growth issues pose the most immediate risk to production deployments.

## Feature Requests & Roadmap Signals

### High-Signal Features (likely v0.8.3 or v0.9.0)

1. **Goal-mode implementation** (tracker #8681) — The largest coordinated effort, splitting an accepted implementation into reviewable PRs. Expect this to land in the next release.
2. **Persistent memory parity** (tracker #8891) — Active PR #8992 (Hindsight backend) and tracker #8891 indicate a multi-PR rollout targeting full parity with mature peer runtimes.
3. **WASM-first plugin runtime** (RFC #8135) — Multiple RFCs and trackers (#7314, #7822, #8135, #8187) show strong maintainer interest in making Wasm the default plugin runtime with signed, capability-declaring modules.
4. **Gateway Kanban board** (RFC #8832) — A user-requested feature for visualizing agent work, inspired by OpenClaw Workboard and Hermes Agent.
5. **Discord interaction-surface parity** (tracker #7831) — Embeds, typed slash options, components, and voice.
6. **Session TTL auto-truncation** (#8134) — Users operating through channels (Slack, Telegram) are explicitly asking for automatic stale session history truncation.

### Prediction

Based on tracker activity and the v0.8.3 milestone index (#7320), the **goal-mode implementation** and **persistent memory parity** are the most likely candidates for the next major release. The **WASM plugin runtime** RFCs suggest a longer-term architectural shift that may land in v0.9.0 rather than v0.8.3.

## User Feedback Summary

### Expressed Pain Points (from issue text and comments)

1. **"Out-of-the-box context budget doesn't work"** — Issue #5808: "The first LLM iteration already exceeds budget by ~3.3x." Users are forced to manually tune `max_context_tokens` before they can run their first conversation.
2. **"Tool availability lies to reasoning models"** — Issue #8054: The system prompt tells models "No tools are available" when tools are present, causing reasoning models to refuse tool use.
3. **"MCP subprocesses become zombies"** — Issue #8731: Daemon accumulates unreaped stdio-based MCP server processes, degrading system resources.
4. **"WhatsApp silently drops messages"** — Issue #6350: Allowed-numbers bypassed for LID-based contacts, messages dropped with no error surfaced. Users report invisible failure.
5. **"Provider errors give empty replies"** — Issue #8675: Malformed tool-call arguments cause provider 400 errors that result in silent empty replies.
6. **"Channels-full confusion"** — Issue #7952: Users who configure non-default channels find they're not included in the default prebuilt binary.
7. **"Can't disable cachePoint for Bedrock Nova 2 Lite"** — Issue #8720: A user explicitly asks for a config file mechanism to disable caching for a specific model.

### Satisfaction Signals

- **Quickstart improvements** (PRs #8987, #8980, #8981) show the community actively shaping onboarding
- **Inkbox channel** (PR #8384) was contributed by a community member (dimavrem22), suggesting enthusiasm for adding first-class channel support
- **Hindsight memory backend** (PR #8992) was also community-contributed (logical-and), indicating a healthy plugin/memory ecosystem

## Backlog Watch

### Issues Needing Maintainer Attention

1. **[#5808] Default 32k context budget exceeded** — Open since April 16, 2026 (nearly 3 months). This is an S1 blocker for new users, yet remains `status:in-progress` without a concrete fix PR. The community is frustrated by the lack of progress on a fundamental usability bug. → [Issue #5808](zeroclaw-labs/zeroclaw Issue #5808)

2. **[#6350] WhatsApp Web silent message drops** — Open since May 3, 2026 (over 2 months). Labeled P1 with `risk:high`, but has only 2 comments and no clear fix path visible. Users relying on WhatsApp channel face invisible data loss. → [Issue #6350](zeroclaw-labs/zeroclaw Issue #6350)

### PRs Needing Review

3. **[#8751] LocalWhisperConfig default fix** — `needs-author-action` since July 6, addressing a critical serde default bug. Awaiting author response. → [PR #8751](zeroclaw-labs/zeroclaw PR #8751)

4. **[#8759] Clipboard screenshot paste reliability** — `needs-author-action` since July 6, fixing a Wayland-specific clipboard bug in zerocode. → [PR #8759](zeroclaw-labs/zeroclaw PR #8759)

5. **[#8845] Live session rebuild on model_provider edits** — `needs-author-action` since July 8, fixing a config refresh gap that leaves live sessions stale. → [PR #8845](zeroclaw-labs/zeroclaw PR #8845)

### Risk Note

The combination of an unresolved S1 context-budget bug (3 months old) and a P1 WhatsApp silent-drop bug (2 months old) with no fix PRs in progress suggests maintainer bandwidth may be constrained. The project's high activity on new features (Inkbox channel, Hindsight memory, SOP pipelines) may be drawing attention away from these critical stability issues.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*