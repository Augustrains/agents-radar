# OpenClaw Ecosystem Digest 2026-07-21

> Issues: 353 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-21 01:20 UTC

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

Here is the OpenClaw project digest for **2026-07-21**.

---

## OpenClaw Project Digest: 2026-07-21

### 1. Today's Overview
The OpenClaw project shows **very high activity** today, with 353 issues and 500 pull requests updated in the last 24 hours. While no new releases were cut, the project is in a heavy bug-fixing and feature-development cycle. However, a **critical stability concern** is the high volume of open PRs (388) versus merged/closed (112), suggesting a potential bottleneck in maintainer review and merge capacity. The community is highly engaged, but the project may be experiencing a build-up of work-in-progress.

### 2. Releases
**No new releases were published today.** The latest available version appears to be `2026.7.1`, as referenced in recent bug reports.

### 3. Project Progress
Today, **112 pull requests were merged or closed**. Key areas of advancement include:
- **Stability & Reliability:** A fix was merged to prevent gateway startup failures on slow hosts by increasing the model runtime build timeout to 120s ([#111983](https://github.com/openclaw/openclaw/pull/111983)).
- **Plugin & Extension Fixes:** A fix was merged to prevent plugin-managed shell commands from leaving orphaned child processes after a timeout ([#111602](https://github.com/openclaw/openclaw/pull/111602)).
- **UI & Diagnostics:** Work advanced on paginating chat history in the Web UI ([#111941](https://github.com/openclaw/openclaw/pull/111941)) and enabling OTel diagnostics for one-shot agent runs ([#100845](https://github.com/openclaw/openclaw/pull/100845)).
- **Channel Parity:** A fix ensures that Zalo outbound messages are properly sanitized to remove internal tool traces, matching the behavior of other messaging channels ([#101431](https://github.com/openclaw/openclaw/pull/101431)).

### 4. Community Hot Topics
The following items are generating the most discussion and engagement this week:

- **Tool Output Image Collapse (Issue #99241):** Users report that tool outputs (especially ANSI-heavy) are being rendered as unreadable "attached images," breaking the agent's ability to read its own results. This is a *Platinum Hermit* severity issue, indicating deep systemic impact on session state and message flow.
    - [Issue: #99241](https://github.com/openclaw/openclaw/issues/99241) (23 comments)
- **Codex Turn-Completion Stall (Issue #88312 - CLOSED):** A major regression in the Codex app-server causing agents to stall before completing turns was heavily debated. The root cause, a regression from a previous fix, appears to have been resolved, but the volume of discussion highlights the fragility of the Codex backend integration.
    - [Issue: #88312](https://github.com/openclaw/openclaw/issues/88312) (22 comments)
- **Memory Trust & Security (Issue #7707):** A feature request to tag memory by trust source (user vs. web) to prevent "memory poisoning" continues to be a high-priority topic, reflecting a growing community concern around security in agent workflows.
    - [Issue: #7707](https://github.com/openclaw/openclaw/issues/7707) (19 comments)

### 5. Bugs & Stability
Several high-severity (P1) bugs are active, creating a "perfect storm" of session and message-loss risks:

| Issue | Summary | Severity | Fix PR Exists? |
| :--- | :--- | :--- | :--- |
| [#87744](https://github.com/openclaw/openclaw/issues/87744) | Codex-backed Telegram turns repeatedly timeout after 2026.5.27 update. | P1 - Message Loss / Crash Loop | No |
| [#108238](https://github.com/openclaw/openclaw/issues/108238) | [Chinese community] Session context incorrectly counts cached reads into total tokens, triggering false compaction errors. | P1 - Session State | No |
| [#102006](https://github.com/openclaw/openclaw/issues/102006) | Aborting one `exec` tool call wedges all subsequent `exec` calls in the same session. | P1 - Session State / Crash Loop | No |
| [#101349](https://github.com/openclaw/openclaw/issues/101349) | Agent-created cron jobs inherit an overly restrictive `toolsAllow` list, causing backend (Claude-CLI) to refuse to run them. | P1 - Auth Provider / UX | No |
| [#109017](https://github.com/openclaw/openclaw/issues/109017) | Anthropic provider disappears from the model picker and new models (Fable 5) are never discovered from the static catalog. | P1 - Auth Provider / UX | No |

**Key Observation:** The absence of fix PRs for many critical P1 regressions (e.g., the exec tool wedge, Telegram timeouts, cron `toolsAllow`) suggests these are still under investigation or awaiting maintainer review.

### 6. Feature Requests & Roadmap Signals
The following features, driven by user demand, are likely candidates for upcoming versions:

- **Antigravity CLI (agy) Support (Issue #84527):** With Google deprecating the Gemini CLI, there is strong community demand (+11 reactions) to support the new `agy` CLI backend. This is a **high-probability** candidate for the next minor release to prevent breakage for Google model users.
    - [Issue: #84527](https://github.com/openclaw/openclaw/issues/84527)
- **Skill Permission Manifests (Issue #12219):** In response to security incidents (credential stealers), users are calling for a standard `skill.yaml` manifest to declare permissions before installation. This aligns with increasing community focus on security and is a **medium-probability** roadmap item.
    - [Issue: #12219](https://github.com/openclaw/openclaw/issues/12219)
- **Claude Bridge (PR #86655):** A large PR is waiting to be merged to add a first-class Claude CLI harness extension. Given the community's reliance on Anthropic models, this is a **high-probability** feature for the next release.
    - [PR: #86655](https://github.com/openclaw/openclaw/pull/86655)
- **Cursored SQLite Transcript API (Issue #79904 - CLOSED):** The community's need for a robust, programmatic way to read session transcripts has been addressed with a new cursor API, suggesting a focus on improving companion tooling and integrations.
    - [Issue: #79904](https://github.com/openclaw/openclaw/issues/79904)

### 7. User Feedback Summary
- **Pain Point #1: Session Reliability on Codex.** Users are deeply frustrated by recurring timeouts and "turn-completed" stalls, which render the Codex backend effectively unusable for critical, multi-step tasks. This is the single largest source of dissatisfaction.
- **Pain Point #2: Context Compaction Loops.** The agent getting stuck in infinite "compacting" loops, especially in tool-heavy sessions, is a major UX failure. Users feel the agent is "broken" and must manually reset it.
- **Pain Point #3: Security Anxiety.** There is a clear undercurrent of concern about security, specifically regarding credential leaks (via `exec` and API keys) and memory poisoning (via untrusted web content). The community is actively requesting more granular controls.

### 8. Backlog Watch
The following "stale" but critical issues have been open for months and need maintainer attention:

- **Agent "False Promise" (Issue #58450):** The agent can end a turn by promising "I'll check and follow up" without actually starting a task. This is a deceptive UX bug that has been open since March 31.
    - [Issue: #58450](https://github.com/openclaw/openclaw/issues/58450) (P2, Last Updated: 2026-07-20)
- **Sub-Agent Announce Suppression (Issue #8299):** Users want a simple config toggle to disable post-announce summaries from sub-agents without relying on a finicky `ANNOUNCE_SKIP` model command. This request has been open since Feb 3.
    - [Issue: #8299](https://github.com/openclaw/openclaw/issues/8299) (P2, Last Updated: 2026-07-21)
- **Heartbeat Swallowing Replies (Issue #64810):** In Telegram topics, asynchronous system events can interrupt and permanently hide a user's reply. This critical stability bug has been open since April 11.
    - [Issue: #64810](https://github.com/openclaw/openclaw/issues/64810) (P1, Last Updated: 2026-07-20)

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report generated from the provided digests.

---

## Cross-Project Comparison Report: Personal AI Agent Ecosystem (2026-07-21)

### 1. Ecosystem Overview

The open-source personal AI agent ecosystem is undergoing a **rapid maturation phase**, characterized by a split between projects executing large-scale architectural overhauls and those focused on iterative stability and bug fixing. A dominant theme is the **convergence on tool-use reliability, session state integrity, and multi-channel support** (Telegram, Matrix, WhatsApp, etc.). Security is emerging as a top-tier community concern, with projects like NanoClaw and NanoBot facing explicit pressure to harden credential storage and permission models. The landscape is highly active, with several projects—including OpenClaw and IronClaw—showing extremely high PR volumes, but also significant maintenance bottlenecks and post-release regressions.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status (24h) | Health Score | Key Signal |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 353 | 500 | Stable (last: 2026.7.1) | ⚠️ **Critical** | Massive PR backlog (388 open); P1 regressions piling up with no fix PRs |
| **NanoBot** | 6 | 30 | Stable (last: unspecified) | ✅ **High** | High merge velocity (11 closed); responsive to user pain points (Ollama caching) |
| **Hermes Agent** | 50 | 50 | **New release** (v0.19.0) | ⚠️ **Elevated Risk** | Post-release regressions (session state, desktop); high community engagement |
| **PicoClaw** | 11 | 10 | Stable (last: v0.3.1) | ✅ **Good** | Balanced bug/feature mix; responsive maintainers |
| **NanoClaw** | 6 | 20 | Stable (no new release) | ✅ **Good** | Strong focus on security hardening (roles, approvals) |
| **NullClaw** | 0 | 1 | Stable (no new release) | 🟢 **Low Activity** | Maintenance lull; single stale dep bump PR |
| **IronClaw** | 43 | 50 | **Pre-RC** (0.9.x) | ⚠️ **High Risk/High Reward** | Massive "Tier-B" legacy deletion; post-merge breakage patched immediately |
| **LobsterAI** | 0 | 15 | Stable (no new release) | ✅ **Good** | High merge rate (66%); focused on Cowork/UI polish |
| **CoPaw** | 30 | 42 | Stable (last: v2.0.0) | ⚠️ **Moderate Risk** | Large PR backlog; community reports critical reasoning bugs |
| **ZeroClaw** | 39 | 50 | Stable (no new release) | ✅ **High** | Intense coordinated feature delivery (eval, SOP, memory); 13 PRs merged |
| **TinyClaw, Moltis, ZeptoClaw** | 0 | 0 | - | 🟢 **Inactive** | No activity in 24 hours |

### 3. OpenClaw's Position

- **Advantages vs. Peers:** OpenClaw has the largest community engagement (353 issues, 500 PRs) and is the de-facto "core reference" project. It boasts the broadest channel support, including specific fixes for Zalo and Telegram.
- **Technical Approach Differences:** OpenClaw's architecture relies on a heavy "Codex" backend, which is currently a major source of user dissatisfaction. In contrast, IronClaw is aggressively simplifying its architecture by deleting a legacy v1 monolith, while NanoBot focuses on a lightweight, channel-first design.
- **Community Size vs. Health:** OpenClaw's massive scale is a double-edged sword. The 388 open PRs indicate a significant maintainer bottleneck. More critical P1 bugs (e.g., exec tool wedge, Codex timeouts) lack fix PRs compared to peers. **OpenClaw is the most dominant project by volume but is currently the most fragile from a stability perspective.**

### 4. Shared Technical Focus Areas

The following requirements are emerging across multiple projects, indicating ecosystem-wide pain points:

- **Session State Reliability & Cross-Platform Context:**
    - *Projects:* OpenClaw, Hermes Agent, NanoBot, IronClaw, CoPaw
    - *Specific Needs:* Solving session duplication (Hermes #68196), context compaction loops (OpenClaw #108238), cross-platform session bridging (Hermes #4335), and preventing "false promise" turn endings (OpenClaw #58450).
- **Agent Loop/Stall Detection & Recovery:**
    - *Projects:* OpenClaw, CoPaw, PicoClaw
    - *Specific Needs:* Preventing agents from getting stuck in "doom loops" or infinite polling (CoPaw #4873), handling MCP server failure hangs (PicoClaw #3269), and providing a way to interrupt runaway agents.
- **Security & Authorization Hardening:**
    - *Projects:* OpenClaw, NanoClaw, NanoBot
    - *Specific Needs:* Preventing accidental global admin grants (NanoClaw #3097), requiring environment variables over plaintext API keys (NanoBot #4803), and adding skill permission manifests (OpenClaw #12219).
- **Model Provider & Backend Resilience:**
    - *Projects:* OpenClaw, PicoClaw, ZeroClaw
    - *Specific Needs:* Fixing Antigravity provider regressions (PicoClaw #3274), handling provider timeouts without crash loops (ZeroClaw #9206), and ensuring compatibility with new models (OpenClaw #109017).
- **Process Reliability & Infrastructure:**
    - *Projects:* OpenClaw, LobsterAI, IronClaw
    - *Specific Needs:* Preventing orphaned child processes after timeout (OpenClaw #111602), silent Windows updates (LobsterAI #2368), and preventing stream replay loops (IronClaw #6352).

### 5. Differentiation Analysis

| Feature Focus | Leading Project(s) | Key Differentiator |
| :--- | :--- | :--- |
| **Massive Community / Reference Implementation** | OpenClaw | Largest scale, but currently burdened by its own success (PR bottleneck) |
| **Stability & Speed (After Refactor)** | IronClaw | Aggressively cutting legacy code for a more disciplined, "Reborn" stack |
| **Multi-Agent / Subagent Lifecycle** | NanoBot, CoPaw | NanoBot unified the subagent turn lifecycle (#4993); CoPaw is working on multi-mode agents. |
| **Enterprise / Deterministic Workflows** | ZeroClaw | Pioneering SOP (Standard Operating Procedure) control plane for approval-gated pipelines. |
| **Security-Centric Architecture** | NanoClaw | Most explicit focus on role-based access control and privilege prevention in admin CLI. |
| **Mobile / Asian Market Channels** | NanoBot, PicoClaw | Strong support for QQ, WeChat, Feishu, LINE, and ongoing work on Chinese cloud providers (DashScope). |
| **Hardware & Model Optimization** | PicoClaw | Focuses on Alibaba Cloud (DashScope), Antigravity providers, and rolling cache breakpoints for cost optimization. |
| **Desktop / UI Polish** | LobsterAI, Hermes Agent | LobsterAI refining Cowork (IM) experience; Hermes working on desktop avatars and sidebar UI. |

### 6. Community Momentum & Maturity

- **Tier 1: Rapidly Iterating (High Risk/High Reward):** These projects are undergoing massive changes and have high community engagement but also significant stability risks.
    - **IronClaw:** In the final stages of a complete architecture rewrite. The highest risk/reward profile.
    - **ZeroClaw:** Shipping multiple foundational features (Eval, SOP, Memory) in parallel. Very high forward momentum.
    - **OpenClaw:** The largest ecosystem but is struggling with PR review capacity and critical bug resolution.

- **Tier 2: Stable & Iterative (Healthy Maturation):** These projects have a stable core and are focusing on user-facing fixes, security, and feature polish.
    - **NanoBot:** High merge velocity with a clear focus on resolving user pain points (e.g., Ollama caching). Healthy state.
    - **PicoClaw:** Balanced bug/feature cycle with responsive maintainers, albeit with a small PR backlog.
    - **NanoClaw:** Strong focus on security hardening, indicating a mature understanding of admin/enterprise concerns.
    - **LobsterAI:** Highly efficient merge rate, focused on UI/UX polish.

- **Tier 3: Stabilizing from a New Release:**
    - **Hermes Agent:** Just released v0.19.0 and is quickly addressing post-release regressions. High community engagement but in "firefighting" mode.

- **Tier 4: Maintenance Lull:**
    - **NullClaw:** No feature development or bug resolution, indicating a project in a low-activity state.

- **Tier 5: Inactive:**
    - **TinyClaw, Moltis, ZeptoClaw:** No observable activity.

### 7. Trend Signals

1.  **The "Session State" Integrity Crisis:** The single biggest pain point across all active projects is the fragility of agent session state. Users are reporting lost context, duplicated messages, stalled turns, and silent failures. This signals that the current state management models (e.g., rotating compression, SQLite duplication) are not keeping up with the demands of long-running, tool-heavy agentic sessions.

2.  **Security is No Longer an Afterthought:** The community is moving from "make it work" to "make it safe." The simultaneous appearance of security-related issues across NanoClaw (role grants), NanoBot (plaintext keys), OpenClaw (memory poisoning), and IronClaw (auto-auth) marks a clear ecosystem-wide shift. **AI agent developers must prioritize permission manifests and credential lifecycle management.**

3.  **The "MCP Hang" Anti-Pattern:** A critical failure mode is emerging where a single failing tool or provider (e.g., MCP server, nvidia-smi, web fetch) can deadlock the entire agent. This highlights the need for robust timeouts, circuit breakers, and graceful degradation in tool-calling layers.

4.  **Convergence on Evaluation (Eval) as a Core Feature:** ZeroClaw's aggressive development of a full `zeroclaw eval` harness (regression suites, pass@k stats, LLM-judge graders) is a leading indicator. The ecosystem is maturing from "script children" to needing systematic ways to measure and improve agent performance.

5.  **Demand for Deterministic Pipelines (SOP):** ZeroClaw's "Standard Operating Procedure" feature represents a new category of demand: users want to create approval-gated, repeatable agent workflows. This blends the line between "agent developer" and "business process automation," suggesting a move towards enterprise adoption.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-21

## Today's Overview
NanoBot shows **very high development activity** today, with 30 pull requests updated in the last 24 hours and 11 merged/closed. The project is actively shipping fixes for multiple channel-specific bugs (QQ, Telegram, Feishu), advancing the subagent lifecycle refactor, and responding to community deployment requests. Six issues were updated (3 closed), with the milestone-worthy #5000 proposal for multi-agent collaboration receiving maintainer attention. The project is in a **healthy, fast-moving maintenance and feature iteration phase** with no new releases today.

## Releases
No new releases were published in the last 24 hours. The latest available version remains unchanged.

## Project Progress
**11 PRs merged/closed today**, representing substantial forward motion:

- **Core Agent Refactor (merged):** [#4993](https://github.com/HKUDS/nanobot/pull/4993) — Unified internal turn lifecycle for subagents, eliminating the duplicate mini-loop in `_process_system_message`. This is a foundational refactor enabling more reliable late subagent delivery.

- **Channel Bug Fixes (merged):**
  - [#4768](https://github.com/HKUDS/nanobot/pull/4768) — Added exponential backoff to QQ channel WebSocket reconnection, fixing the excessive error logging on network failure.
  - [#4981](https://github.com/HKUDS/nanobot/pull/4981) — Fixed Telegram markdown split infinite loop when `max_len <= 0`.
  - [#4982](https://github.com/HKUDS/nanobot/pull/4982) — Fixed Feishu fallback text chunk infinite loop under same condition.
  - [#5008](https://github.com/HKUDS/nanobot/pull/5008) — Fixed multimodal image merging where consecutive user turns dropped all but the last image.

- **Deployment & Documentation (merged):**
  - [#4937](https://github.com/HKUDS/nanobot/pull/4937) — Added one-click Render Blueprint deployment (gateway + WebUI).
  - [#4998](https://github.com/HKUDS/nanobot/pull/4998) — Added Ollama prompt-cache diagnostics guide to improve local model performance.

## Community Hot Topics

1. **[#4867](https://github.com/HKUDS/nanobot/issues/4867) — Preserve prompt prefix for Ollama caching (CLOSED)**  
   *15 comments, 0 reactions* — This user reported that NanoBot adds **60 seconds per turn** with Ollama due to broken prompt caching. The underlying need is acute: Ollama users with 32 GB VRAM find the project "totally unusable." The issue was closed, likely addressed by #4998's caching diagnostics guide.

2. **[#5000](https://github.com/HKUDS/nanobot/issues/5000) — Multi-agent collaboration proposal (OPEN)**  
   *1 comment* — A detailed proposal to evolve subagents from "background task delegation" to a true multi-agent system with persistent identities, shared task state, and agent-to-agent communication. This is the project's 5000th issue—a milestone that signals community interest in advanced multi-agent architectures.

3. **[#4988](https://github.com/HKUDS/nanobot/pull/4988) — Keep background turns silent when model ends empty (OPEN)**  
   *Active discussion* — Addresses the UX inconsistency where cron/local trigger turns produce unwanted "I couldn't produce a final answer" messages. Community wants silent completion for automation, with error reporting only on actual failures.

## Bugs & Stability

| Severity | Issue | Fix PR | Summary |
|----------|-------|--------|---------|
| **High** | [#4803](https://github.com/HKUDS/nanobot/issues/4803) | [#5010](https://github.com/HKUDS/nanobot/pull/5010) | API keys stored as plaintext in config.json — `repr=False` doesn't protect `model_dump()`. Fix PR adds documentation recommending env-var references. |
| **High** | [#4867](https://github.com/HKUDS/nanobot/issues/4867) | Closed | 60-second delay per turn with Ollama due to broken prompt caching. Addressed via caching guide. |
| **Medium** | [#4767](https://github.com/HKUDS/nanobot/issues/4767) | [#4768](https://github.com/HKUDS/nanobot/pull/4768) (merged) | QQ channel WebSocket reconnect loop flooding logs on DNS failure. Fixed with exponential backoff. |
| **Medium** | [#4982](https://github.com/HKUDS/nanobot/pull/4982) | Merged | Feishu infinite loop in `_fallback_text_chunks` when `limit <= 0`. |
| **Medium** | [#4981](https://github.com/HKUDS/nanobot/pull/4981) | Merged | Telegram infinite loop in `_split_telegram_markdown` when `max_len <= 0`. |
| **Low** | [#5004](https://github.com/HKUDS/nanobot/pull/5004) | Open | Session directory `fsync` fails on unsupported filesystems (EINVAL). Simple tolerance fix proposed. |

**Active regressions in flight:** PRs [#4954](https://github.com/HKUDS/nanobot/pull/4954), [#4992](https://github.com/HKUDS/nanobot/pull/4992), and [#4928](https://github.com/HKUDS/nanobot/pull/4928) address WebUI subagent visibility bugs and heartbeat routing issues introduced by the new unified session system.

## Feature Requests & Roadmap Signals

**Likely for next release:**

1. **Multi-agent collaboration (#5000)** — The detailed proposal and maintainer engagement suggest this architectural evolution is being seriously considered for a future milestone.

2. **Dokploy one-click deploy (#1503, #5007)** — PR [#5007](https://github.com/HKUDS/nanobot/pull/5007) is open with a complete template; likely to merge soon, fulfilling a 4-month-old feature request from March 2026.

3. **Guarded tool gateway (#5006)** — PR [#5006](https://github.com/HKUDS/nanobot/pull/5006) adds an opt-in `ToolGateway` protocol for channel plugins, addressing security and isolation needs.

4. **Telegram custom Bot API (#4919)** — PR [#4919](https://github.com/HKUDS/nanobot/pull/4919) supports self-hosted Bot API servers, opening enterprise deployment scenarios.

**Speculative next-version features:** Feishu "listen" mode for context-only group ingest ([#5009](https://github.com/HKUDS/nanobot/pull/5009)), scoped temp directory cleanup ([#5005](https://github.com/HKUDS/nanobot/pull/5005)), and env-var-based secret management ([#5010](https://github.com/HKUDS/nanobot/pull/5010)).

## User Feedback Summary

**Pain Points:**
- Ollama performance is **critically bad** — 60 seconds per turn with local models on 32 GB VRAM (#4867). Users find this "totally unusable."
- API key security is a **real concern** — plaintext storage in config.json despite `repr=False` suggests a mismatch between developer intent and implementation (#4803).
- Infinite loops in channel message splitting (Telegram, Feishu) cause hard hangs (#4981, #4982).

**Satisfaction Signals:**
- The community is actively contributing deployment templates (Render, Dokploy) and detailed architectural proposals (multi-agent collaboration), indicating high engagement.
- Merge velocity is strong: 11 PRs closed in 24 hours, including critical channel stability fixes.
- The prompt caching diagnostics guide (#4998) directly addresses the #1 user complaint about Ollama.

## Backlog Watch

1. **[#1503](https://github.com/HKUDS/nanobot/issues/1503) — Dokploy template (OPEN, 138 days)**  
   *Last updated 2026-07-20* — 4 months old, but PR [#5007](https://github.com/HKUDS/nanobot/pull/5007) now provides an implementation. This is effectively resolved; the PR needs review and merge.

2. **[#4803](https://github.com/HKUDS/nanobot/issues/4803) — Plaintext API keys (OPEN, 15 days)**  
   *Security vulnerability* — While a documentation PR exists ([#5010](https://github.com/HKUDS/nanobot/pull/5010)), the underlying code issue (missing `exclude=True` on secret fields) remains unaddressed. A code-level fix should be prioritized over documentation-only remediation.

3. **No other critically stalled issues** — The project maintains good response times to new issues and PRs.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-21

## Today's Overview

Hermes Agent v0.19.0 "The Quicksilver Release" shipped yesterday, marking a major milestone with ~2,245 commits, ~1,065 merged PRs, and ~3,300 issues closed since v0.18.0, with contributions from over 450 community members. Activity remains extremely high, with 50 issues and 50 PRs updated in the last 24 hours, indicating a healthy and responsive development cycle. However, the volume of bug reports—particularly around session state and desktop stability—suggests the new release has introduced several regressions that the team is actively addressing. A notable cluster of P1 and P2 severity bugs around session duplication, cost tracking, and desktop UI responsiveness indicates ongoing stability work post-release.

## Releases

**Hermes Agent v0.19.0 (v2026.7.20) — The Quicksilver Release** was released on July 20, 2026.

Key highlights from the release:
- **Scale:** ~2,245 commits, ~1,065 merged PRs, ~300,000 insertions, ~36,000 deletions across ~2,465 files
- **Community:** 450+ community contributors, ~3,300 issues closed since v0.18.0
- The release tagline "Hermes is the mess" may hint at acknowledged internal complexity

No breaking changes or migration notes were explicitly detailed in the release description. Given the volume of recent bug reports (particularly around session state rehydration and cron job authentication), users should review the v0.19.0 changelog thoroughly before upgrading production instances.

## Project Progress

In the last 24 hours, 8 PRs were merged or closed, covering several important fixes:

- **`#68305` (CLOSED)** — Auto-formatting fix for JS lint issues, merged automatically
- **`#68309` (CLOSED)** — Fix(kanban): Aligned review handoff contract between Athena and H-Omar components (#67652 merged first)
- **`#68288` (CLOSED)** — **Critical:** Fixed duplicate transcript rows on cold Desktop resume with rotating compression (addresses #68196)
- **`#68301` (CLOSED)** — Native session bridging feature request closed as duplicate (path already underway)
- **`#68299` (CLOSED)** — Duplicate session entry in sidebar bug closed as duplicate
- **`#67817` (CLOSED)** — Telegram HTTPXRequest read-only attribute bug (needs-repro, closed without merge)
- **`#66611` (CLOSED)** — Desktop "Already up to date" overlay close button unresponsive (UX bug)
- **`#46511` (CLOSED)** — Cron job credential pool exhaustion fix merged to main

Open PRs with significant progress include:
- **`#68069`** — Desktop message avatars with editable names and images (feature, UX enhancement)
- **`#68293`** — Drill into project folders before listing sessions (desktop UI)
- **`#68303`** — Deduplicate aliased profile databases (desktop backend)
- **`#68304`** — Named delegation routes for model/reasoning routing (new feature)
- **`#68306`** — Widget-app SDK for TUI (new developer API)
- **`#68308`** — Fix reasoning token inclusion in cost estimation (important pricing fix)

## Community Hot Topics

### Most Active Issues (by comment count)

1. **#67600** — [BUG] Desktop session sidebar empty for `default` profile only (9 comments)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/67600  
   *Analysis:* High engagement on a P2 desktop bug affecting the default profile. Users report backend serves data correctly but sidebar rendering fails—likely a frontend session routing issue. The 9 comments suggest community members are actively debugging and sharing workarounds.

2. **#4335** — Feature Request: Cross-platform session context sharing (CLI ↔ Telegram) (7 comments, 2 👍)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/4335  
   *Analysis:* Long-standing request (March 2026) for unified session context across platforms. Community desire for seamless multi-platform experience is strong. This aligns with #68301 (closed as duplicate), suggesting the team is working on it.

3. **#2788** — [BUG] Cron jobs never run or fail silently (6 comments)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/2788  
   *Analysis:* Persistent cron reliability issue. Users report jobs created but never executing or recording errors. Long-lived issue (March) suggesting this remains a pain point.

4. **#66868** — [BUG] Cron job primary model call fails 401 (5 comments)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/66868  
   *Analysis:* Auth credential collapse in cron scheduler—provider drops to "custom" outside runtime session. Related to #33333/#34651 fixes but not fully resolved.

5. **#67762** — [BUG] `agent.session_estimated_cost_usd` resets to $0 on gateway restart (5 comments)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/67762  
   *Analysis:* Session cost tracking fails on restart—blocker for any billing display feature. Community concerned about silent undercounting.

### Most Active PRs (by comment count)

- `#68069` — Desktop message avatars (feature, open, 0 comments but active commits)
- `#68303` — Profile database deduplication (bug fix, open, technical discussion expected)
- `#68308` — Reasoning token cost estimation fix (bug fix, open, pricing-critical)

## Bugs & Stability

### Critical (P0)

- **#67194 (CLOSED)** — Windows installer impossible to run (`Hermes-Setup.exe` fails). Marked duplicate but unresolved for the Windows user. Severity: blocker for Windows adoption.

### High Severity (P1-P2)

1. **#68196** — **Cold Desktop resume duplicates persisted transcript** (P1)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/68196  
   *Fix PR:* #68288 (merged)  
   *Issue:* On first turn after cold resume, rotating compression appends entire already-persisted transcript to parent session a second time. Durable SQLite duplication.

2. **#68302** — **Sidebar session click has no effect while Skills & Tools is active** (P3)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/68302  
   *Issue:* UI dead zone—clicking sessions in sidebar does nothing when middle panel shows Skills & Tools.

3. **#68244** — **Update process breaks agent when user declines "Restore local changes"** (P2)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/68244  
   *Issue:* Choosing "no" during update restore prompt leaves system broken with no recovery path.

4. **#67762** — **Session cost estimation resets to $0 on restart** (P2)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/67762  
   *Issue:* `agent.session_estimated_cost_usd` not rehydrated from SQLite. Undercounting costs.

5. **#68261** — **TUI skill credential prompts routed to wrong session** (P2)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/68261  
   *Issue:* Process-global callback captures secret for wrong session when multiple sessions share a gateway.

6. **#61573** — **Desktop: message queued in busy session delivered to unrelated idle session** (P2)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/61573  
   *Issue:* User messages land in wrong threads—privacy and correctness risk.

7. **#29866** — **brew upgrade breaks certifi (TLS failures on all platforms)** (P1)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/29866  
   *Issue:* Homebrew upgrade pipeline missing CA bundle in venv. Blocks Feishu, Telegram, WeChat.

8. **#2228** — **System error messages injected with wrong role (appear as user)** (P2)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/2228  
   *Issue:* Dynamic role assignment can make system errors look like user messages.

### Medium Severity (P3)

- **#55369** — Union integer|string tool args drop leading zeros ("007" → 7)  
- **#55551** — Groq STT ignores language parameter for non-English audio  
- **#57626** — Skill library update injected into child delegate sessions  
- **#7135** — Hindsight local daemon fails on macOS Apple Silicon (MPS path issue)  
- **#59626** — `dashboard --status` falsely reports running servers  
- **#68287** — Desktop selection context menu missing Read Aloud/Translate (fix PR open)

### Fix PRs in Progress

| Bug Issue | Fix PR | Status |
|-----------|--------|--------|
| #68196 (transcript duplicate) | #68288 | **MERGED** |
| #68150 (message preservation E2E) | #68150 | Open, P3 |
| #68069 (desktop avatars) | #68069 | Open, P3 |
| #68287 (context menu) | #68287 | Open |
| #67817 (Telegram HTTPX) | No fix PR | Closed needs-repro |

## Feature Requests & Roadmap Signals

### Likely for Next Release (v0.20.0)

1. **Cross-platform session bridging** — Multiple issues (#4335, #68301) requesting unified session context across CLI, Telegram, Desktop. The duplicate closure of #68301 suggests the team has this in development. Probability: **High**.

2. **Session archive/compress CLI** — #41075 requests `hermes sessions archive` and `hermes sessions compress` for safe storage management. With v0.19.0's compression work, this may be a natural next step. Probability: **Medium-High**.

3. **Named delegation routes** — PR #68304 adds operator-defined routes for `delegate_task` (provider, model, reasoning level by task purpose). This is a significant architectural addition. Probability: **High** (PR already submitted).

4. **MCP Server Management CLI** — #690 (long-standing, 4 comments) requests interactive MCP tool discovery and selective loading. Probability: **Medium** (3 months old, no PR yet).

### Community-Requested Features (No PR Yet)

- **Widget-app SDK** — PR #68306 introduces a new TUI widget framework. Likely to ship in v0.20.
- **Desktop avatar customization** — PR #68069 adds editable names/images. UX improvement, likely to merge.

## User Feedback Summary

### Pain Points (High Signal)

1. **Session state reliability** — Users consistently report session-related bugs: empty sidebars (#67600), duplicate entries (#68299), context routing failures (#61573), and credential prompt misrouting (#68261). This is the #1 category of dissatisfaction post-v0.19.0.

2. **Update/recovery fragility** — Multiple users (#68244, #29866) report that update processes can leave the system in an unrecoverable state. The brew upgrade certifi breakage (#29866) is particularly widespread, affecting all platforms.

3. **Cron job unreliability** — Issues #2788 and #66868 indicate cron jobs fail silently or with 401 auth errors, recurring since March. Users report creating jobs but finding no execution trace.

4. **Cost tracking opacity** — #67762 (cost reset on restart) and #68308 (reasoning tokens excluded) show users are concerned about accurate billing transparency.

5. **macOS/Apple Silicon compatibility** — #7135 (Hindsight daemon timeout), #2975 (WhatsApp Node.js PATH issue) show platform-specific friction for Apple Silicon users.

### Positive Signals

- The release of v0.19.0 with 450+ contributors demonstrates strong community engagement and contribution velocity.
- Many bugs have active fix PRs (especially session state issues), indicating responsive maintainers.
- Feature requests like cross-platform session bridging and named delegation routes show a community actively shaping the product's roadmap.

## Backlog Watch

### Critical Unresolved Issues (30+ days old, high impact)

1. **#2788** — [BUG] Cron jobs never run or fail silently (created 2026-03-24, 6 comments, P2)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/2788  
   *Status:* No fix PR in over 4 months. Cron reliability is foundational—this should be prioritized.

2. **#4335** — Feature Request: Cross-platform session context sharing (created 2026-03-31, 7 comments, 2 👍)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/4335  
   *Status:* Long-standing request with no implementation. Recent duplicate closure (#68301) suggests internal work, but no public PR yet.

3. **#690** — MCP Server Management CLI (created 2026-03-08, 4 comments)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/690  
   *Status:* Oldest issue in the top-30, no PR. MCP tool support is a core differentiator—lack of management CLI limits power users.

4. **#2228** — System error messages injected with wrong role (created 2026-03-20, 3 comments, P2)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/2228  
   *Status:* 4 months old, no fix PR. This is a data integrity bug that could confuse models.

5. **#3944** — Slack gateway integration fails (created 2026-03-30, 5 comments)  
   *URL:* https://github.com/NousResearch/hermes-agent/issues/3944  
   *Status:* 4 months unresolved. Slack integration is a common enterprise use case.

### PRs Awaiting Maintainer Attention

- **#47278** — Add `ProviderProfile.build_client` for custom model provider clients (created 2026-06-16, sweeper:risk-compatibility)  
  *URL:* https://github.com/NousResearch/hermes-agent/pull/47278  
  *Status:* Open for 35 days, labeled with broad blast radius. Architectural proposal with high impact—needs maintainer decision.

- **#61511** — Matrix always-visible tool activity list pane (created 2026-07-09, sweeper:risk-message-delivery)  
  *URL:* https://github.com/NousResearch/hermes-agent/pull/61511  
  *Status:* Open for 12 days, multiple Matrix PRs from same author (#61206, #61218, #61219) all awaiting review.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-21

## 1. Today's Overview

PicoClaw shows **high development activity** with 11 issues and 10 PRs updated in the last 24 hours, indicating a healthy and responsive project. The issue tracker has a **balanced mix** of bug reports (7 open/active, 4 closed) and feature work, with several regressions emerging from the latest `main` branch commits. Notably, **two separate Antigravity provider bugs** were filed within hours of each other — one a code regression, the other an upstream Google policy change — suggesting recent provider refactoring may have introduced instability. On the positive side, the community contributed **three significant feature PRs** (Japanese localization, DashScope TTS, and model name updates) that are advancing the platform's capabilities. However, a **critical agent-loop hanging bug** related to MCP server failures remains open without a fix PR yet.

## 2. Releases

**No new releases** in the last 24 hours. The latest tagged release remains `v0.3.1`. Users building from source on `main` (@85dcfcca) are currently experiencing regressions reported in issues #3274 and #3275.

## 3. Project Progress

### Merged/Closed PRs Today (5 total)

| PR | Description | Status |
|---|---|---|
| [#3277](https://github.com/sipeed/picoclaw/pull/3277) | **fix(tools):** deferred-tool visibility heal + sliding TTL + SSE tool-call index fix — prevents silent tool removal on restart/TTL expiry | ✅ Merged |
| [#3192](https://github.com/sipeed/picoclaw/pull/3192) | **chore:** bump goreleaser base images from alpine:3.21 to 3.23 | ✅ Merged |
| [#3191](https://github.com/sipeed/picoclaw/pull/3191) | **chore:** remove duplicate `build/` entry in `.gitignore` | ✅ Merged |
| [#276](https://github.com/sipeed/picoclaw/pull/276) | **docs:** improve README clarity and branding consistency | ✅ Merged |
| [#277](https://github.com/sipeed/picoclaw/pull/277) | **feat:** update `make deps` logic to prevent frequent dependency version updates | ✅ Merged |

### Key Advances
- **Tool system stabilization**: PR #3277 fixes a critical issue where deferred MCP tools would silently disappear on restart or TTL expiry, causing model hallucination. This is essential for multi-session agent reliability.
- **Documentation and build cleanup**: Two chore PRs and a documentation PR merged, showing ongoing maintenance hygiene.
- **Dependency version control**: PR #277 improves the build system to avoid automatic dependency bumps, which should reduce supply-chain churn.

## 4. Community Hot Topics

| Issue/PR | Comments | Reactions | Topic |
|---|---|---|---|
| [#3182](https://github.com/sipeed/picoclaw/issues/3182) | 4 | 0 | **Android version startup failure** — user cannot launch service despite full permissions; path settings non-functional |
| [#3203](https://github.com/sipeed/picoclaw/issues/3203) | 3 | 👍1 | **Matrix sync reconnection** — silent death after network disruption, systemd doesn't restart because main process stays alive |
| [#3231](https://github.com/sipeed/picoclaw/issues/3231) | 2 | 0 | **SearXNG basic auth support** — cannot use URL-based auth, needs request header support |
| [#3229](https://github.com/sipeed/picoclaw/issues/3229) | 2 | 0 | **Rolling cache breakpoints** for Anthropic conversational caches — advanced optimization proposal |
| [#3274](https://github.com/sipeed/picoclaw/issues/3274) | 1 | 0 | **Antigravity regression** on `main` — immediate attention needed |

**Underlying needs**: Users are demanding **provider diversity** (Android, Matrix, SearXNG, Antigravity) and **operational reliability** (reconnection logic, silent failure detection). The Anthropic caching proposal (#3229) signals advanced users pushing for cost optimization at scale.

## 5. Bugs & Stability

### Critical Severity
- **[#3269](https://github.com/sipeed/picoclaw/issues/3269) — MCP server failure hangs agent loop** (OPEN, no fix PR): If any MCP server connection fails, the entire agent loop hangs, freezing chat interface. This is a **user-facing denial-of-service** bug. No fix exists yet.

### High Severity
- **[#3274](https://github.com/sipeed/picoclaw/issues/3274) — Antigravity provider regression on `main`** (OPEN, 1 comment): Freshly built from source `85dcfcca` returns `INVALID_ARGUMENT` — `tool_schema_transform "simple"` no longer sufficient. **Regression from v0.3.1**. Likely introduced by recent provider refactoring.
- **[#3278](https://github.com/sipeed/picoclaw/issues/3278) — Google blocks Antigravity OAuth login** (OPEN, 0 comments): Google's OAuth policy enforcement prevents login entirely. **External blocker** — requires changes to the OAuth consent screen configuration or app verification.
- **[#3203](https://github.com/sipeed/picoclaw/issues/3203) — Matrix sync reconnection failure** (OPEN, stale): Network disruption kills sync permanently. Main process stays alive, so systemd auto-restart doesn't trigger. **Silent data loss** for Matrix users.

### Medium Severity
- **[#3275](https://github.com/sipeed/picoclaw/issues/3275) — `model_list` loses `api_keys` on config rewrite** (CLOSED): Config entries corrupted after Launcher WebUI operations. Already closed, but implication is config management instability.
- **[#3182](https://github.com/sipeed/picoclaw/issues/3182) — Android service launch failure** (OPEN, 22 days old): Oldest open bug; unreproducible by maintainers, unresponsive author.

### Fixed Today
- **PR [#3277](https://github.com/sipeed/picoclaw/pull/3277)** merged: Fixes deferred tool visibility and SSE tool-call index, solving a class of "phantom tool" bugs.

## 6. Feature Requests & Roadmap Signals

### Likely for Next Release
| Feature | Issue/PR | Rationale |
|---|---|---|
| **Japanese WebUI localization** | [#3272](https://github.com/sipeed/picoclaw/issues/3272) / [#3273](https://github.com/sipeed/picoclaw/pull/3273) | Complete 968-line translation PR already submitted; docs already have Japanese translation |
| **DashScope TTS + WeChat audio** | [#3270](https://github.com/sipeed/picoclaw/pull/3270) | Full provider implementation PR, adds TTS and WeChat integration |
| **Model name updates for 9 providers** | [#3271](https://github.com/sipeed/picoclaw/pull/3271) | Refreshes default model list to 2026-07 latest (e.g., GPT-5.6 variants, Claude 4 Opus) |

### Possible Near-Term
- **Externally-managed gateway detection for Launcher** [#3276](https://github.com/sipeed/picoclaw/issues/3276): User requesting systemd-friendly Launcher behavior — important for headless/server deployments.
- **Anthropic rolling cache breakpoints** [#3229](https://github.com/sipeed/picoclaw/issues/3229): Advanced cost optimization — likely waiting on maintainer capacity.
- **SearXNG basic auth header support** [#3231](https://github.com/sipeed/picoclaw/issues/3231): Small change, high value for self-hosted search setups.

## 7. User Feedback Summary

### Pain Points
1. **Agent-loop hangs from MCP failures** (#3269) — most critical user-facing issue: complete UI lockup with no error recovery.
2. **Antigravity provider broken** on latest `main` (#3274, #3278) — two separate issues blocking a significant provider for users building from source.
3. **Silent Matrix sync death** (#3203) — undermines trust in persistent channel connectivity.
4. **Android app unusable** (#3182) — oldest open bug, though low community engagement suggests limited Android user base.

### Use Cases Revealed
- **Headless server deployments** (#3276): Launcher-as-systemd, not wanting browser-based controls.
- **Chinese ecosystem integration** (#3270): DashScope (Alibaba Cloud) TTS + WeChat audio sending — clear China-market demand.
- **Japanese language community** (#3272/#3273): Active contributor investing in full 968-line translation.
- **Cost-optimized agentic workflows** (#3229): Users running long, multi-turn conversations want Anthropic prompt caching at scale.

### Satisfaction Signals
- **High-quality PRs from community**: honbou submitted both the Japanese localization PR and three detailed bug reports — indicates engaged power-user.
- **Rapid bug closure**: Issues #3230, #3231, #3229, #3275 all closed within 24 hours of being opened or updated, showing maintainer responsiveness.

## 8. Backlog Watch

### Issues Needing Maintainer Attention
| Issue | Age | Status | Why Concern |
|---|---|---|---|
| [#3182](https://github.com/sipeed/picoclaw/issues/3182) — Android launch failure | 24 days | OPEN, 4 comments | Oldest open bug; user provided screenshots but maintainers can't reproduce; needs closer or repro request |
| [#3203](https://github.com/sipeed/picoclaw/issues/3203) — Matrix sync reconnection | 18 days | OPEN, stale, 👍1 | Stale for 18 days with 1 upvote — silent failure mode is dangerous; systemd users cannot mitigate |
| [#3269](https://github.com/sipeed/picoclaw/issues/3269) — MCP hang | <24h | OPEN, 0 comments | Critical severity but no maintainer response yet since filed today |

### PRs Waiting for Review
| PR | Age | Status | Impact |
|---|---|---|---|
| [#3254](https://github.com/sipeed/picoclaw/pull/3254) — fix model resolution | 7 days | OPEN, stale | Fixes incorrect model selection with aliases — medium severity, no recent activity |
| [#3251](https://github.com/sipeed/picoclaw/pull/3251) — Anthropic cache token capture | 8 days | OPEN | Improves observability for operators — no response from maintainers |
| [#3271](https://github.com/sipeed/picoclaw/pull/3271) — model name updates | <24h | OPEN | Fresh PR, needs review |
| [#3270](https://github.com/sipeed/picoclaw/pull/3270) — DashScope TTS + WeChat | <24h | OPEN | Fresh PR, needs review |
| [#3273](https://github.com/sipeed/picoclaw/pull/3273) — Japanese localization | <24h | OPEN | Fresh PR, needs review |

### Summary
The project is **actively maintained** with strong community contributions, but the **Antigravity regressions** (#3274, #3278) and the **MCP hang bug** (#3269) represent the most urgent blockers. The backlog of un-reviewed PRs (5 total, ranging from 1–8 days old) suggests the maintainer team may be bandwidth-constrained, especially given the high issue volume today.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the NanoClaw project digest for **2026-07-21**.

---

## NanoClaw Project Digest — 2026-07-21

### 1. Today's Overview
The project saw a surge in maintenance activity over the past 24 hours, with **20 pull requests** updated and **6 new issues** filed. A significant portion of this activity involves critical security and stability fixes, including a coordinated series of patches addressing the role and approval system and the WhatsApp Cloud bridge. Six PRs were merged or closed, indicating strong core-team throughput on bug fixes. However, the lack of a new release suggests these fixes are still being staged for a future version.

### 2. Releases
**None.** No new releases were published in the last 24 hours.

### 3. Project Progress
Six pull requests were merged or closed today, reflecting focused progress on infrastructure and bug fixes:

- **Container Image & Infrastructure:**
    - **[#3110 (CLOSED)](https://github.com/nanocoai/nanoclaw/pull/3110):** Bakes the `caldav-mcp` server into the base agent image, enabling calendaring features without runtime installs.
    - **[#1110 (CLOSED)](https://github.com/nanocoai/nanoclaw/pull/1110):** Fixes container-runtime tests to align with actual implementation details (bind mounts, system status commands).
- **WhatsApp Cloud Fixes:**
    - **[#3108 (CLOSED)](https://github.com/nanocoai/nanoclaw/pull/3108):** Patches the Chat SDK bridge to rehydrate inbound attachments when adapters lack `fetchData`, fixing attachment handling for voice notes.
    - **[#3107 (CLOSED)](https://github.com/nanocoai/nanoclaw/pull/3107):** Companion documentation and adoption module for the WhatsApp Cloud instance re-key fix.
    - **[#3087 (CLOSED)](https://github.com/nanocoai/nanoclaw/pull/3087):** Engages mention-mode wirings for typed @-mentions in WhatsApp groups.
- **Telegram Pin Fix:**
    - **[#2642 (CLOSED)](https://github.com/nanocoai/nanoclaw/pull/2642):** Pins the Telegram adapter version to resolve a peer-dependency conflict with the Chat SDK.

### 4. Community Hot Topics
The highest-engagement items revolve around **security hardening of the admin CLI** and **extending the platform to new geographies**:

- **Security & Authorization (High Traffic):** A user (k-fls) filed a series of four interlinked issues (#3097, #3098, #3099, #3100) detailing flaws in `ncl roles` and approval routing. These received no comments yet but are critical in nature. Corresponding fix PRs (#3101, #3102, #3103, #3104) were opened immediately, suggesting these are high-priority for the core team.
- **LINE Channel Support:** Issue **[#3096](https://github.com/nanocoai/nanoclaw/issues/3096)** (1 comment) proposes adding LINE as a communication channel, addressing a gap for users in Japan, Taiwan, and Thailand. The related skill PR **[#2918](https://github.com/nanocoai/nanoclaw/pull/2918)** remains open, signaling strong community interest in Asian market expansion.
- **Voice Transcription:** PR **[#2459](https://github.com/nanocoai/nanoclaw/pull/2459)** (on-device whisper.cpp transcription) continues to receive updates, indicating sustained interest in local AI processing without cloud dependencies.

### 5. Bugs & Stability
Several bugs were reported today, sorted by severity. Fix PRs are already in progress for all critical items.

- **Critical: Accidental Global Admin Grant (Issue [#3097](https://github.com/nanocoai/nanoclaw/issues/3097)):** Running `ncl roles grant --role admin` without the `--group` flag silently grants global admin. **Fix:** PR [#3101](https://github.com/nanocoai/nanoclaw/pull/3101) requires explicit `--scope`.
- **Critical: Last Owner Revocable (Issue [#3100](https://github.com/nanocoai/nanoclaw/issues/3100)):** Revoking the sole `owner` leaves the system with no root of trust. **Fix:** PR [#3104](https://github.com/nanocoai/nanoclaw/pull/3104) blocks this action.
- **High: Self-Approval & Privilege Inversion (Issue [#3099](https://github.com/nanocoai/nanoclaw/issues/3099)):** Role-change approvals can be routed to the target user, or require a lower-privileged user's approval. **Fix:** PR [#3103](https://github.com/nanocoai/nanoclaw/pull/3103) enforces privilege-proportional routing.
- **Medium: Opaque Approval Cards (Issue [#3098](https://github.com/nanocoai/nanoclaw/issues/3098)):** Approval cards show raw command lines instead of human-readable effects. **Fix:** PR [#3102](https://github.com/nanocoai/nanoclaw/pull/3102) renders structured cards.
- **Medium: WhatsApp Cloud Stranded Rows (Bug [#3105](https://github.com/nanocoai/nanoclaw/issues/3105)):** Upgrading existing WhatsApp installs silently drops messages due to missing migration. **Fix:** PR #3106 addresses the row adoption logic.

### 6. Feature Requests & Roadmap Signals
Platform expansion and documentation localization are the key signals from today's activity:

- **New Channel: LINE Official Account:** Issue [#3096](https://github.com/nanocoai/nanoclaw/issues/3096) and PR [#2918](https://github.com/nanocoai/nanoclaw/pull/2918) propose adding the dominant Asian messenger. Given the README's RFS process and the presence of a Traditional Chinese README (PR [#2950](https://github.com/nanocoai/nanoclaw/pull/2950)), this is a strong candidate for the next minor release.
- **New Channel: Dial (SMS + AI Voice):** PRs [#3041](https://github.com/nanocoai/nanoclaw/pull/3041) and [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) add a voice and SMS adapter. This signals a push into phone-based interactions and the "runChannelSkill" model.
- **Local Voice Transcription:** PR [#2459](https://github.com/nanocoai/nanoclaw/pull/2459) (whisper.cpp) continues to advance, predicting an eventual "no cloud required" transcription feature in the SDK.

### 7. User Feedback Summary
User feedback today is split between **platform adaptability** and **administrative safety**:

- **Satisfaction (Feature Gaps):** Users are actively contributing new channel adapters (LINE, Dial) because existing coverage doesn't meet their local market needs (Japan, Thailand). The RFS process is being used as intended.
- **Pain Points (Administrative Safety):** User k-fls has surfaced a significant trust model flaw—the role/approval system allows accidental privilege escalation and self-approval of destructive actions. The swift pairing of issues and fix PRs indicates the core team values this feedback highly.
- **Pain Points (Upgrade Experience):** User glifocat reported that upgrading a WhatsApp bridge silently breaks the installation (Issue [#3105](https://github.com/nanocoai/nanoclaw/issues/3105)), causing a silent failure. This highlights a regression in the upgrade/`update-skills` pipeline.

### 8. Backlog Watch
The following items remain open for extended periods and may require maintainer attention:

- **PR [#2459](https://github.com/nanocoai/nanoclaw/pull/2459)** (whisper.cpp voice transcription) — Open since **2026-05-13** (2+ months). It has been updated recently but lacks a clear path to merge. This is a popular feature (local AI) that is stalling.
- **PR [#2918](https://github.com/nanocoai/nanoclaw/pull/2918)** (LINE channel) — Open since **2026-07-03**. It is a large feature skill that has received updates but may need core-team review for architectural alignment.
- **PR [#3044](https://github.com/nanocoai/nanoclaw/pull/3044)** (Inbound attachment fix) — Open since **2026-07-14** (7 days). While PR #3108 was merged for a similar issue, this PR targets a deeper fix for `fetchData` loss at the bridge level and remains unresolved.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**NullClaw Project Digest — 2026-07-21**

**1. Today's Overview**
The NullClaw project shows minimal activity over the last 24 hours. No new issues were created or updated, and no new releases were published. Activity is limited to a single open pull request (#956) that updates the base Docker image from Alpine 3.23 to 3.24, which remains unmerged after over a month. Overall, the project appears to be in a low-activity or maintenance-lull phase, with no feature development or bug-fix signals visible on this date.

**2. Releases**
No new releases were published in the last 24 hours.

**3. Project Progress**
No pull requests were merged or closed today. The only PR updated (#956) remains open and has not advanced toward merge.

**4. Community Hot Topics**
The single active pull request is the primary point of community attention:
- **[#956 [OPEN] ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group](https://github.com/nullclaw/nullclaw/pull/956)** — Submitted by dependabot[bot] on 2026-06-15, last updated 2026-07-20. This automated dependency update has zero reactions and zero comments. **Underlying need:** This PR reflects the need to keep the base Docker image current for security patches and compatibility. The lack of engagement may indicate maintainer bandwidth constraints or pending review of automated updates.

**5. Bugs & Stability**
No bugs, crashes, or stability issues were reported in the last 24 hours. The project’s issue tracker currently shows zero open items, suggesting either a clean state or that issues are being resolved outside the visible window.

**6. Feature Requests & Roadmap Signals**
No user-submitted feature requests were observed in the last 24 hours. With zero new issues or PRs beyond the automated dependency bump, there are no clear signals for upcoming features. The next version’s direction remains uncertain from this data snapshot.

**7. User Feedback Summary**
No new user feedback (comments, reactions, or pain points) was recorded in the last 24 hours. The absence of activity suggests either a satisfied user base or low community engagement at this time.

**8. Backlog Watch**
The single open PR (#956) has been pending for 36 days without maintainer action or community discussion. While not a critical item, its prolonged open status may indicate a review bottleneck or a need to configure auto-merge for low-risk dependency updates. No other long-unanswered items exist in the current tracker.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for July 21, 2026.

---

## IronClaw Project Digest: 2026-07-21

### 1. Today's Overview

The project is in an **extremely high-velocity state**, dominated by the final stages of a massive architectural overhaul. Activity is at a peak, with 43 issues and 50 PRs updated in the last 24 hours. The core team is executing a "Tier-B" cleanup, which involves deleting the legacy v1 monolith (`src/`) and repointing all production infrastructure to the new "Reborn" stack. This has resulted in the highest-risk PR of the week being merged (#6375), leading to some immediate post-merge breakage that was quickly patched (#6379). The project is stabilizing from this major transition, with a focus on fixing regressions and preparing the first Release Candidate for the new architecture.

### 2. Releases

**None.** No new releases were created today.

### 3. Project Progress

A significant number of PRs were merged or closed today, indicating rapid execution on the core roadmap.

- **Tier-B / Legacy Deletion (Highest Impact):** The most significant change is the merge of [#6375](https://github.com/nearai/ironclaw/pull/6375) (ilblackdragon), which deletes the entire legacy v1 monolith (`src/`) and switches production deploys to the "Reborn" stack. This was a massive PR touching nearly every scope.
- **Post-Merge Stabilization:** A critical fix, [#6379](https://github.com/nearai/ironclaw/pull/6379) (ilblackdragon), was quickly merged to repair the build (`main` went red) because CI workflows still referenced parts of the now-deleted legacy code. This was a high-priority, high-urgency fix.
- **Architecture Simplification (Refactoring):**
    - [#6374](https://github.com/nearai/ironclaw/pull/6374) (ilblackdragon) eliminated a large "shadow store" module (`local_trigger_access`), cleaning up the deployment configuration model per the new architecture document.
    - [#6377](https://github.com/nearai/ironclaw/pull/6377) and [#6378](https://github.com/nearai/ironclaw/pull/6378) (ilblackdragon) removed dead code and feature flags from the `ironclaw_runner` crate, further simplifying the codebase.
- **Stability & UX Fixes:**
    - [#6337](https://github.com/nearai/ironclaw/pull/6337) (serrrfirat) was merged to improve stream management: keeping healthy streams alive and preventing partial text from being treated as a successful answer.
    - Three user-facing bugs were closed: [#6178](https://github.com/nearai/ironclaw/issues/6178) (Automation error banner), [#6179](https://github.com/nearai/ironclaw/issues/6179) (Settings import), and [#6335](https://github.com/nearai/ironclaw/issues/6335) (Capability remediation text).
- **Release Prep:** [#6370](https://github.com/nearai/ironclaw/pull/6370) (henrypark133) prepared the changelog for the upcoming `ironclaw-v1.0.0-rc.1` release.

### 4. Community Hot Topics

The most active discussions are driven by the core team and bug bash participants, focusing on the final steps of the major refactor and critical stability issues.

- **[#6263](https://github.com/nearai/ironclaw/issues/6263) - Final store consolidation (9 comments):** The most discussed issue. It details the final debt item in retiring a legacy `InMemoryTurnStateStore`. This is a highly technical, internal refactoring task that is the last major piece of a long-running cleanup.
- **[#6274](https://github.com/nearai/ironclaw/issues/6274) - Finish DeploymentConfig (4 comments):** This issue tracks the completion of the new `DeploymentConfig`, the central piece of the new architecture. It is directly linked to multiple open PRs (#6387) and is the primary driver of the current refactoring wave.
- **[#6190](https://github.com/nearai/ironclaw/issues/6190) & [#6189](https://github.com/nearai/ironclaw/issues/6189) - Confusing error handling (4 comments each):** These `bug_bash_P2` issues highlight a common UX pain point: conflicting and misleading error messages during and after failed streaming requests. This suggests the error handling layer needs consolidation to present a single, clear root cause to the user.
- **[#6369](https://github.com/nearai/ironclaw/issues/6369) - Legacy deletion gaps (3 comments):** A direct follow-up to the massive #6375 PR, this issue documents the known capability gaps left after deleting the legacy codebase, signaling a clear "known unknowns" approach to the transition.

### 5. Bugs & Stability

A large batch of `bug_bash_P2` issues was opened today, indicating a focused quality assurance phase. Several are regressions stemming from the ongoing architectural changes.

- **Critical (P1):**
    - **[#6360](https://github.com/nearai/ironclaw/issues/6360) - No navigation back in provider onboarding:** A basic UX flow that locks the user, requiring a full cancel.
    - **[#6348](https://github.com/nearai/ironclaw/issues/6348) - Gmail extension auto-authorizes after reinstall:** A significant security and privacy violation where user consent is bypassed.

- **High (P2 - Bug Bash):**
    - **[#6351](https://github.com/nearai/ironclaw/issues/6351) - Checkpoint unreachable errors:** Multi-tool runs are failing due to infrastructure issues with the checkpoint system.
    - **[#6350](https://github.com/nearai/ironclaw/issues/6350) - Assistant switches language:** A confusing model behavior bug that degrades user trust.
    - **[#6352](https://github.com/nearai/ironclaw/issues/6352) - Stream replay loop:** A UI regression where leaving and returning to a chat causes streamed chunks to replay in a loop.
    - **[#6349](https://github.com/nearai/ironclaw/issues/6349) - Telegram chat history corruption:** Cross-platform chat rendering is broken, leading to a fragmented and unusable UI.
    - **[#6353](https://github.com/nearai/ironclaw/issues/6353) - Long messages truncated:** A basic display bug where large responses are cut off without a way to view the full content.

**No fix PRs yet exist for the bugs opened today.**

### 6. Feature Requests & Roadmap Signals

New issues today are less about user requests and more about finishing the core "Reborn" platform features to fill gaps left by the legacy deletion.

- **Platform Features (Reborn-native):** Several issues track the creation of Reborn-native replacements for legacy features:
    - **[#6320](https://github.com/nearai/ironclaw/issues/6320) - IronHub extension install flow:** Creating a new system for discovering and installing extensions.
    - **[#6325](https://github.com/nearai/ironclaw/issues/6325) - Thread-scoped MCP sessions:** Better isolation and configuration for Model Context Protocol.
    - **[#6324](https://github.com/nearai/ironclaw/issues/6324) - WebUI workspace redesign:** A chat-first UX overhaul for the new platform.
- **In-Chat Commands (Backlog):** [#6384](https://github.com/nearai/ironclaw/issues/6384) prioritizes the gap between legacy and new in-chat command coverage, indicating this will be a major focus for the next version.
- **Policy & Security:** [#6371](https://github.com/nearai/ironclaw/issues/6371) opens a discussion to narrow the hook framework, signaling a move towards a simpler, more centralized authorization model.

**Prediction:** The completion of `DeploymentConfig` (#6274) and the in-chat command backlog (#6384) are the strongest signals for what will land in the next major version (1.0.0-rc.1).

### 7. User Feedback Summary

The "bug bash" issues, filed by `joe-rlo` and `italic-jinxin`, represent the most direct user pain points after recent changes.

- **Pain Points:**
    - **Confusing Error States:** Multiple conflicting error banners (#6190) and "ghost" errors on successful operations (#6189) erode user confidence.
    - **Broken Cross-Platform Sync:** Telegram chats rendered incorrectly in the WebUI (#6349) breaks a core workflow for users who switch devices.
    - **Data & Privacy Violations:** The Gmail extension auto-authorizing (#6348) is a major trust-breaking bug.
    - **Basic UX Failures:** The inability to navigate back during onboarding (#6360) and truncated messages (#6353) point to a lack of polish in recent UI changes.
- **Satisfaction/Dissatisfaction:** The high volume of merged PRs shows the team is extremely responsive. However, the sheer number of regressions (P2 bugs) suggests the rapid pace of architectural change is creating a rough UX for end-users in the short term.

### 8. Backlog Watch

- **[#2277](https://github.com/nearai/ironclaw/issues/2277) - ACP-backed child thread backends (Opened: April 10, 2026):** This feature request for delegating work to external coding agents (like Codex) has been open for over 3 months. It has 2 comments and a 👍, indicating community interest. It is a complex feature and may be deprioritized while the core platform is stabilized.
- **[#5664](https://github.com/nearai/ironclaw/pull/5664) - chore(deps): bump the actions group (Opened: July 5, 2026):** This dependency update PR has been open for over two weeks. While low risk, stale dependency PRs can be a sign of maintainer bandwidth being fully occupied by feature work. It currently blocks 16 updates.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the project digest for **LobsterAI** based on data from **2026-07-21**.

---

## LobsterAI Project Digest – July 21, 2026

### 1. Today's Overview
LobsterAI saw a highly productive day with **15 PRs updated** in the last 24 hours, resulting in **10 merged/closed** contributions. While there were no new releases or open issues created, the team focused heavily on polishing the **Cowork (IM) experience**, stabilizing the **Windows build pipeline**, and introducing a new **browser multi-annotation feature**. The high merge rate (66%) indicates strong momentum and efficient code review. Three stale dependency bump PRs remain open, suggesting a stable core that is undergoing controlled modernization.

### 2. Releases
**None.** No new releases were published today.

### 3. Project Progress
The following features and fixes were advanced or completed today:

- **Cowork & Browser Annotations:** PR [#2366](https://github.com/netease-youdao/LobsterAI/pull/2366) (merged) introduced support for multiple browser annotations, including a new browser comment protocol, screenshot asset storage IPC, and structured annotation context in Cowork message metadata.
- **Windows Build & Update:** PR [#2368](https://github.com/netease-youdao/LobsterAI/pull/2368) (open) aims to install Windows updates silently via NSIS. PR [#2367](https://github.com/netease-youdao/LobsterAI/pull/2367) (merged) added explicit channel entry points for Windows dist builds to prevent environment variable leakage.
- **AI Skin Creation:** PR [#2361](https://github.com/netease-youdao/LobsterAI/pull/2361) (merged) improved the AI skin creation flow with a persistent entry in Appearance settings and first-use onboarding.
- **OpenClaw Config Hot-Reload:** PR [#2365](https://github.com/netease-youdao/LobsterAI/pull/2365) (merged) fixed configuration hot-reload to use RPC acknowledgment instead of file polling.

### 4. Community Hot Topics
There were no highly active community discussions (zero comments/reactions on today’s items). The most notable long-lived open PRs are automated dependency bumps:

- **Dependency Updates (Stale):** PRs [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) (Electron 40→43), [#1282](https://github.com/netease-youdao/LobsterAI/pull/1282) (Headless UI), [#1283](https://github.com/netease-youdao/LobsterAI/pull/1283) (React 18→19), and [#1284](https://github.com/netease-youdao/LobsterAI/pull/1284) (Syntax highlighter) remain open after 3+ months. These indicate the project is cautious about major framework upgrades, likely due to breaking changes in React 19 or Electron 43.

### 5. Bugs & Stability
No new bugs (crashes, regressions) were reported today. However, several stability fixes were merged:

- **Cowork Scroll Jumps (Medium):** PR [#2364](https://github.com/netease-youdao/LobsterAI/pull/2364) (merged) fixed scroll jumps during session refresh by scoping events by session ID.
- **IM Message Flicker (Medium):** PR [#2363](https://github.com/netease-youdao/LobsterAI/pull/2363) (merged) resolved periodic flickering in IM messages by improving window reconciliation.
- **Auth Callback Loss (Medium):** PR [#2360](https://github.com/netease-youdao/LobsterAI/pull/2360) (merged) preserved local callback servers across login retries, preventing auth failure loops.
- **Cron UI Bug (Low):** PR [#2362](https://github.com/netease-youdao/LobsterAI/pull/2362) (merged) fixed a minor cron UI display bug.

### 6. Feature Requests & Roadmap Signals
Today’s activity signals the following roadmap priorities:

- **Silent Windows Updates (Next):** PR [#2368](https://github.com/netease-youdao/LobsterAI/pull/2368) (open) indicates the team is preparing a seamless update experience for Windows users, likely targeting the next minor release.
- **Browser Annotation Ecosystem:** The merged multi-annotation support (#2366) suggests LobsterAI is deepening its "cowork" functionality to allow rich, screenshot-based feedback directly within the built-in browser.
- **AI Skin Designer Kit:** With #2361 merged, the AI skin creation workflow is now a persistent, first-class feature. Expect improvements to the prompting framework or result sharing in upcoming releases.

### 7. User Feedback Summary
No explicit user feedback (comments, reactions) was recorded in today’s data. The absence of open issues suggests either low user engagement or a healthy state where bugs are filed as PRs quickly. The fixes for scroll jumps and flicker (#2364, #2363) likely address latent user pain points in the Cowork chat interface.

### 8. Backlog Watch
The following items require maintainer attention:

- **Major Dependency Bumps (Critical):** PRs [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277), [#1282](https://github.com/netease-youdao/LobsterAI/pull/1282), [#1283](https://github.com/netease-youdao/LobsterAI/pull/1283), and [#1284](https://github.com/netease-youdao/LobsterAI/pull/1284) are stale for over 110 days. The Electron 43 and React 19 bumps carry breaking changes that need careful testing and may block other modernizations.
- **POPO Connectivity Validation (Resolved but Relevant):** PR [#1349](https://github.com/netease-youdao/LobsterAI/pull/1349) (merged 3 months ago) fixed a fake API validation bug. If any new POPO-related issues arise (e.g., credential lifecycle), this fix’s pattern is a reference.

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

# CoPaw Project Digest — 2026-07-21

## 1. Today's Overview

CoPaw shows **very high activity** with 30 issues and 42 PRs updated in the last 24 hours, indicating a rapidly evolving project. The majority of issues remain open (22 of 30), and most PRs are still under review (32 of 42), suggesting the maintainer team is actively processing a large backlog. No new releases were published today, but the high PR throughput (10 merged/closed) points to steady progress toward a future release. The community is heavily engaged, particularly around reasoning bugs, tool call behavior, and feature requests for UI/UX improvements.

## 2. Releases

**None.** No new releases were published in the last 24 hours. The latest available versions remain v2.0.0.post3 (released earlier) and v1.1.12.postx for the older stable line.

## 3. Project Progress

**10 PRs were merged or closed today**, reflecting substantive progress:

- **#6210 [CLOSED]** — `refactor: make the default loop an agent mode` — A significant refactor that turns the ordinary ReAct loop into a first-class `DefaultMode`, moving gate ownership out of `AgentBuilder` and `CommandHandler`. This improves lifecycle management and paves the way for multi-mode agents.

- **#6150 [CLOSED]** — `feat(pawapp): add pawapp sdk and kanban app` — Introduces a new plugin SDK (`pawapp`) and an example `agent-kanban` app, expanding the plugin ecosystem.

- **#6235 [CLOSED]** — `feat(memory): enhance ReMe Light index maintenance stability and chunking` — Major memory subsystem improvements: moves index rebuild to explicit maintenance, adds console/API controls, upgrades `reme-ai` to 0.4.1.3 with self-repair, concurrent write protection, and Markdown chunking.

- **#5922 [CLOSED]** — `feat(observability): track user/session/version on langfuse traces` — Adds user/session/version metadata to Langfuse observability traces for better debugging.

- **#5961, #5958, #5959, #6246, #6250, #6255, #6101, #6264** — Eight bugs and questions closed, including crash fixes (`_saved_tool_refs` OSError), sandbox fallback behavior, and a refactor of conversation reset lifecycle.

**Key features that advanced but remain open:**
- Unified browser system (#6276) — one SDK for any backend browser control
- Chrome extension plugin with native messaging bridge (#6157)
- Per-session model overrides (#5992)
- Windows desktop GUI automation with UIA (#5187)
- AIOnly provider integration (#6271)
- Background tool call offload refactor (#6151)

## 4. Community Hot Topics

**Most active issue:**
- **#6257** — *[Bug]: Multiple tool calls produce identical thinking output* (13 comments) — This bug is generating significant discussion. When an agent executes multiple tool calls in a single turn, each call's thinking block contains the exact same content instead of independent reasoning. This is a core reasoning pipeline issue.

**Other highly discussed items:**
- **#5961** — *v2.0.0版本循环执行的问题* (8 comments, CLOSED) — Agent repeatedly writes/deletes in a loop with qwen3.7-plus model, causing task stagnation.
- **#4873** — *同时开两个subagent会导致主agent无限快速轮询* (5 comments) — Two subagents cause rapid polling loops that can't be interrupted from Feishu.
- **#6242** — *Console embedding dimensions setting not sent to OpenAI-compatible APIs* (3 comments) — Configuration gap for ReMe Light memory.

**Underlying needs:** The community is struggling with **reasoning consistency** across multiple tool calls, **agent loop detection** (both doom loops and infinite polling), and **configuration completeness** for advanced features like memory dimensions. There's also strong demand for **Chinese-language documentation and support** as many issues are filed in Chinese.

## 5. Bugs & Stability

**High Severity:**

| Bug | Issue | Description | Status | Fix PR? |
|-----|-------|-------------|--------|---------|
| **Identical thinking across tool calls** | #6257 | Multiple tool calls in one turn share same thinking text, breaking multi-step reasoning | OPEN | No direct fix yet |
| **Reasoning relay corrupts thinking blocks** | #6282 | AgentScope 2 multi-ReAct iterations copy first thinking block to all segments | OPEN | PR #6280 (fix aligns reasoning with tool segments) |
| **Desktop hangs on nvidia-smi stall** | #6197 | Frozen binary hangs indefinitely if nvidia-smi hangs | OPEN | No fix |
| **Loop execution with qwen3.7-plus** | #5961 | Agent repeatedly writes/deletes, never completing tasks | CLOSED | Fixed in v2.0.0 |

**Medium Severity:**
- **#6241** — Agent outputs identical text across consecutive turns + `memory_search` enters infinite loop (no mechanism to stop repeated calls)
- **#6239** — Windows PATH concatenation drops `;` separator, breaking npm globals for child processes
- **#6242** — `use_dimensions` not exposed for ReMe Light embedding dimensions → Console settings silently ignored
- **#6197** — Desktop Tauri build hangs on Windows if `nvidia-smi` blocks indefinitely

**Low Severity / Configuration:**
- #6258 — OpenAI max output token setting not honored
- #6249 — TUI stuck in "warming" state from source
- #6261 — Offline code mode can't preview files (requires online resources)
- #6252 — Ctrl+/- zoom doesn't work in Linux Desktop mode
- #5688 — CSS prefix mismatch (`ant-` vs `qwenpaw-`) likely causing style breakage

## 6. Feature Requests & Roadmap Signals

**High-likelihood for next release (based on active PRs and maintainer engagement):**

| Feature | Issue/PR | Likelihood | Rationale |
|---------|----------|------------|-----------|
| **AIOnly model provider** | #6268 / PR #6271 | **Very High** | PR open, author offering contribution, maintainers tagged |
| **Session grouping/folders** | #6287 | **High** | Long-standing UX pain point, clear value |
| **User-editable agent mode** | PR #6270 | **High** | Active PR from core contributor rayrayraykk |
| **Unified browser system** | PR #6276 / #6157 | **High** | Large feature, multiple PRs, maintainers reviewing |
| **ask_user_question tool (HITL)** | #6274 | **Medium** | Well-specified, solves real approval workflow gaps |
| **Per-session model overrides** | PR #5992 | **Medium** | Active but hasn't merged; may need refinement |
| **Windows desktop GUI automation** | PR #5187 | **Medium** | Large feature, still open after a month |
| **Built-in tool description customization** | #6286 | **Medium** | Clear token savings appeal (8-10k tokens/request) |

**Lower-likelihood but notable:**
- Mobile web console adaptation (#6281)
- Auto-attach current timestamp to context (#6283)
- Minimize to system tray (#6264, CLOSED — may reconsider)
- Collapsible thinking/tool blocks in UI (#6260)

## 7. User Feedback Summary

**Satisfaction signals:**
- Users are actively contributing new providers (AIOnly, #6268) and apps (QwenPaw Creator, PR #6284), indicating strong developer engagement.
- The plugin ecosystem is growing, with the new `pawapp` SDK giving users clear extension paths.

**Pain points:**
- **Reasoning & loop issues dominate:** Multiple users report agents getting stuck in repetitive cycles, identical thinking outputs, and inability to escape loops — this is the #1 cluster of user dissatisfaction (#6257, #5961, #4873, #6241).
- **Configuration gaps frustrate power users:** `use_dimensions` not exposed (#6242), sandbox fallback hardcoded (#6250), max tokens not honored (#6258) — users want finer-grained control.
- **Desktop/mobile experience needs polish:** Linux zoom broken (#6252), Windows PATH issues (#6239), mobile web adaptation lacking (#6281), file preview broken offline (#6261).
- **Memory system confusion:** Two overlapping memory systems (MEMORY.md + Dream digests) confuse users (#6222) — clearer documentation is needed.
- **UI clutter:** Users want thinking and tool calls collapsible (#6260) — the current UI buries results under process output.

**Language/accessibility note:** Roughly 40% of issues are filed in Chinese, with many asking about Chinese cloud providers (Alibaba Bailian, qwen models). The project's bilingual community is healthy but may benefit from more formalized translation of core documentation.

## 8. Backlog Watch

**Issues needing maintainer attention (older, unanswered, or high-impact):**

| Issue | Age | Summary | Concern |
|-------|-----|---------|---------|
| **#4873** | 49 days | Two subagents cause infinite polling, Feishu interruption broken | **Critical UX bug**, no resolution in sight. User reports inability to interrupt runaway loops. |
| **#5688** | 20 days | CSS prefix mismatch `ant-` vs `qwenpaw-` | Likely affects UI rendering across the frontend. No maintainer response. |
| **#5187** | 37 days | Windows desktop GUI automation PR | Large feature PR sitting open; users may be waiting for this to land or be rejected. |
| **#5992** | 9 days | Per-session model overrides PR | First-time contributor PR with no maintainer comments yet. Risk of abandonment. |
| **#6041** | 8 days | Read-only tools exempt from doom loop detection | Addresses a false-positive loop detection bug. PR exists but no maintainer review. |
| **#6151** | 6 days | Background tool call offload refactor | Complex refactor; no maintainer comment yet. |

**Actionable recommendation:** Issue #4873 (subagent infinite polling) is the most critical backlog item — it blocks a core multi-agent workflow and has been unanswered for 49 days. PR #5992 (per-session model overrides) from a first-time contributor should receive at least a courtesy check to encourage continued contribution.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-21

## Today's Overview

ZeroClaw is experiencing a burst of coordinated engineering activity, with **50 PRs and 39 issues updated in the last 24 hours**, signaling an intense development cycle driven by multiple parallel feature tracks. The project is shipping several foundational capabilities—an **agent evaluation harness**, **SOP (Standard Operating Procedure) ingress and control-plane features**, and **memory subsystem consolidation**—all of which are landing as multi-PR rollouts tracked by milestone epics. While no new releases were published today, the volume of merged work suggests a release candidate may be approaching. The community remains highly engaged, with seven new issues opened today ranging from critical S0 workspace resolution bugs in cron jobs to UI polish items in ZeroCode.

## Releases

No new releases were published today.

## Project Progress

Thirteen PRs were merged or closed in the last 24 hours. Key accomplishments include:

- **Provider stability**: [#8931](https://github.com/zeroclaw-labs/zeroclaw/pull/8931) (merged) fixes malformed tool-call arguments causing HTTP 400 errors on OpenRouter and compatible providers, addressing the critical bug reported in #8675.
- **Eval harness foundation**: Four PRs from contributor IftekharUddin landed the initial regression suite seed ([#9225](https://github.com/zeroclaw-labs/zeroclaw/pull/9225)), comparable run receipts and failure transcript dumps ([#9220](https://github.com/zeroclaw-labs/zeroclaw/pull/9220)), JUnit XML reporting format ([#9223](https://github.com/zeroclaw-labs/zeroclaw/pull/9223)), and repeated live runs with pass@k/pass^k statistics ([#9224](https://github.com/zeroclaw-labs/zeroclaw/pull/9224)).
- **SOP ingress wiring**: [#9203](https://github.com/zeroclaw-labs/zeroclaw/pull/9203) and [#9205](https://github.com/zeroclaw-labs/zeroclaw/pull/9205) wire authenticated HTTP fan-in for SOP endpoints and centralize fan-in ingress adapters, advancing the SOP milestone tracker (#8288).
- **Runtime safety**: [#9201](https://github.com/zeroclaw-labs/zeroclaw/pull/9201) prevents shared iteration budget underflow (TOCTOU race), addressing #9192.
- **Telegram channel reliability**: [#8955](https://github.com/zeroclaw-labs/zeroclaw/pull/8955) (merged) fixes batch media group attachment handling for Telegram.
- **Bug fixes closed**: Serial transport desynchronization (#9078), ZeroCode code-block copy issues (#8664 and #8644), terminal background inheritance (#8765), transcript mouse selection (#8944), and comment hygiene gate failures (#9216, closed by merges).

## Community Hot Topics

- **[RFC: Work Lanes, Board Automation, and Label Cleanup (#6808)](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)** — 14 comments, 0 👍  
  Status: Accepted, rollout in progress. This governance RFC proposes restructuring work lanes and automating board management to reduce manual maintainer overhead. It touches every contributor and is a signal that the project is maturing its contribution processes.

- **[74 test failures on Windows (#7462)](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)** — 10 comments, 0 👍  
  Open for over a month, this bug highlights that CI only runs on Linux. The community is blocked on a critical cross-platform gap, and the issue tracks S2-degraded behavior with path semantics and console encoding on Windows.

- **[A2A Protocol Support (#3566)](https://github.com/zeroclaw-labs/zeroclaw/issues/3566)** — 9 comments, 7 👍  
  The most-upvoted open feature request. Users clearly want native Agent-to-Agent protocol support for inter-instance and external agent communication, which aligns with the v0.9.0 auth/security/gateway tracker (#7432).

- **[Agent Evaluation Harness (#7065)](https://github.com/zeroclaw-labs/zeroclaw/issues/7065)** — 4 comments, 0 👍  
  Mother of today's eval PRs. Four follow-up issues were filed today (#9226–#9228) requesting dashboard/trend tracking, LLM-judge calibration tooling, and memory seeding for eval sandboxes. This is currently the most active feature area.

- **[Persistent Memory Tracker (#8891)](https://github.com/zeroclaw-labs/zeroclaw/issues/8891)** — 6 comments, 0 👍  
  Tracks 18 open items (3 issues, 15 PRs) to bring cross-session memory to parity with peer runtimes. PR #8899 landed config validation and migration reindex hooks today.

## Bugs & Stability

**Critical (S0 — data loss / security risk):**
- **[Cron agent jobs intermittently resolve workspace_dir to `/` (#9206)](https://github.com/zeroclaw-labs/zeroclaw/issues/9206)** — Opened today. Intermittent data-loss/security risk when natural-language cron jobs execute with the wrong workspace root. No fix PR open yet.

**Severity 1 (S1 — workflow blocked):**
- **[Landlock sandbox locks zeroclaw itself into landlock (#9204)](https://github.com/zeroclaw-labs/zeroclaw/issues/9204)** — Opened today. Prior issue #5153. Causes SQLite memory access and other failures. No fix PR open.
- **[web_fetch returns garbage for compressed responses (#9207)](https://github.com/zeroclaw-labs/zeroclaw/issues/9207)** — Opened today. gzip/brotli/deflate responses return binary garbage that agents cannot parse. No fix PR open.
- **[shared_budget TOCTOU can wrap AtomicUsize; SopEngine::finish_run unwrap panics (#9192)](https://github.com/zeroclaw-labs/zeroclaw/issues/9192)** — Fix PR [#9201](https://github.com/zeroclaw-labs/zeroclaw/pull/9201) is open and addressing the atomic underflow path.
- **[Malformed tool-call arguments sent to OpenRouter providers (#8675)](https://github.com/zeroclaw-labs/zeroclaw/issues/8675)** — Fix PR [#8931](https://github.com/zeroclaw-labs/zeroclaw/pull/8931) was merged today, closing this issue.

**Severity 2 (S2 — degraded behavior):**
- **[History trimming occurs silently with pruning disabled (#8837)](https://github.com/zeroclaw-labs/zeroclaw/issues/8837)** — Closed today (resolved).
- **[74 test failures on Windows (#7462)](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)** — Remains open with no fix PR.
- **[Serial transport desynchronization after non-matching response ID (#9078)](https://github.com/zeroclaw-labs/zeroclaw/issues/9078)** — Closed today.
- **[SOP HTTP fan-in documented but not wired (#6685)](https://github.com/zeroclaw-labs/zeroclaw/issues/6685)** — PRs [#9203](https://github.com/zeroclaw-labs/zeroclaw/pull/9203) and [#9205](https://github.com/zeroclaw-labs/zeroclaw/pull/9205) are open and addressing this.

**Severity 3 (S3 — minor):**
- **[`zeroclaw desktop` uses dead download URL and does not detect installed AppImage (#9202)](https://github.com/zeroclaw-labs/zeroclaw/issues/9202)** — Opened today.
- **[Discord typing indicator stuck after daemon reload (#9198)](https://github.com/zeroclaw-labs/zeroclaw/issues/9198)** — Opened today.

## Feature Requests & Roadmap Signals

**Likely in next release (v0.9.x or imminent):**

1. **Agent Evaluation Harness** — The `zeroclaw eval` subsystem is landing rapidly: regression suites, JUnit reports, pass@k statistics, LLM-judge graders, baseline comparison, and receipt dumps. Four PRs merged today and three follow-up issues filed (#9226–#9228). This is the most active feature track and ripe for a roadmap milestone.

2. **SOP Ingress and Control Plane** — The daemon-owned SOP control plane tracker (#8288) is advancing toward "5/5" capability. Today saw wiring of authenticated HTTP fan-in and centralized ingress adapters. SOP is on track to reach parity with its design specification.

3. **OpenAI-Compatible Gateway** — PR [#8486](https://github.com/zeroclaw-labs/zeroclaw/pull/8486) (OpenAI chat completions endpoint, XL size) remains open with 5 comments and is tagged as blocking #8550, #8603, and #6850. This would enable LangChain, Continue.dev, Aider, and OpenAI SDK compatibility.

4. **Persistent Memory Consolidation** — Tracker #8891 has 15 open PRs. Config validation landed today. Full parity with mature peer runtimes is the goal.

**Emerging signals:**
- **A2A Protocol Support (#3566)** — 7 upvotes, tied to the v0.9.0 auth/security/gateway milestone. High community demand.
- **Skill installation security** — PR [#9084](https://github.com/zeroclaw-labs/zeroclaw/pull/9084) (screen, receipt, verify, and sandbox-gate skill installs, XL size) addresses supply-chain security for third-party skills from ClawHub/Git registries.
- **Embedded context / deliver_file for ACP (#9178)** — One comment, but opens resource-blob and delivery capabilities for the Agent Communication Protocol.

## User Feedback Summary

**Pain points (explicit and implicit from bugs):**

- **Cross-platform frustration**: Windows users report 74 test failures (#7462) that CI doesn't catch, and ZeroCode fails to start without manually setting `ZEROCLAW_SOCKET` (#9117, closed). The project's Linux-only CI is a known gap.
- **Silent context loss**: A user reported that history trimming occurs even with pruning disabled, causing the agent to "suddenly lose context without explanation" (#8837, closed). This eroded trust in long sessions.
- **Web fetch broken for modern sites**: Compressed responses return garbage (#9207), breaking agents' ability to browse or scrape the web. This is a regression in a core tool.
- **Desktop installation friction**: The `zeroclaw desktop` command point to a dead download URL and doesn't detect an existing AppImage (#9202), creating a poor onboarding experience.
- **Discord integration glitches**: The typing indicator gets permanently stuck after a daemon reload (#9198), which is confusing for channel users.

**Satisfaction signals:**
- The community is actively filing follow-up issues for the eval harness (three filed today by IftekharUddin), indicating genuine enthusiasm for the feature.
- Seven upvotes on the A2A protocol feature suggest strong demand for multi-agent interoperability.
- Multiple closed bugs today (serial transport, ZeroCode UI issues) show responsive maintainers.

**Use case insights:**
- Enterprise users appear interested in SOP-based deterministic pipelines for approval-gated workflows (PR #8979).
- The Telegram media group fix (#8955) indicates real-world use of photo/document sharing in chat interfaces.
- Cron job execution with agent-style prompts (#9206) suggests users are leveraging ZeroClaw for scheduled, autonomous decision-making.

## Backlog Watch

Issues and PRs that have gone unanswered or lack maintainer attention:

1. **[#6685 — SOP HTTP fan-in documented but not wired](https://github.com/zeroclaw-labs/zeroclaw/issues/6685)** — Open since May 15 (2+ months). Advertised in docs but never implemented. **Mitigation**: PRs [#9203](https://github.com/zeroclaw-labs/zeroclaw/pull/9203) and [#9205](https://github.com/zeroclaw-labs/zeroclaw/pull/9205) are now open as of today.

2. **[#7462 — 74 test failures on Windows](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)** — Open since June 10 (41 days). No PR or assignee. If maintainers consider Windows a tier-1 platform, this needs an owner.

3. **[#3566 — A2A Protocol Support](https://github.com/zeroclaw-labs/zeroclaw/issues/3566)** — Open since March 15 (4+ months). 7 upvotes, tied to v0.9.0 tracker (#7432) but no dedicated PR or milestone commitment visible.

4. **[#9202 — `zeroclaw desktop` dead download URL + AppImage detection](https://github.com/zeroclaw-labs/zeroclaw/issues/9202)** — Filed today. Should be a quick win for UX improvement; no response yet.

5. **[#9204 — Landlock sandbox locks zeroclaw itself](https://github.com/zeroclaw-labs/zeroclaw/issues/9204)** — Filed today. Pre-existing issue #5153 was never resolved; this is a regression that blocks security sandbox functionality. No response yet.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*