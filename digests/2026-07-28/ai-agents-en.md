# OpenClaw Ecosystem Digest 2026-07-28

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-28 01:17 UTC

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

Here is the OpenClaw project digest for **2026-07-28**.

---

## OpenClaw Project Digest — 2026-07-28

### 1. Today's Overview
The project is in a high-activity state. With **500 issues** and **500 PRs** updated in the last 24 hours, the maintainer team and community are deeply engaged in triage, code review, and feature development. While no new official releases were published today, the project is processing a significant number of incoming contributions, with **230 merged/closed PRs**. The core focus remains on resolving acute stability and memory issues (P0/P1 bugs), addressing security vulnerabilities related to prompt injection and secrets management, and refining the agent context and session management architecture.

### 2. Releases
**None.** No new releases were recorded for today.

### 3. Project Progress
Today saw significant progress on several fronts, with **230 PRs** being merged or closed. Key areas of advancement include:
- **UI/UX Polish:** `PR #114812` aims to match ClickClack discussion sidebars to host themes, improving the visual consistency of the web UI.
- **Developer Tooling:** `PR #114688` (`steipete`) adds per-run stats (code-mode engagement, round trips, cost) to agent JSON envelopes, giving developers deeper insight into agent behavior.
- **Plugin Ecosystem:** `PR #114783` (`giodl73-repo`) introduces manifest-first host contribution bundles, simplifying how external plugins declare their capabilities.
- **Telegram Fixes:** `PR #114822` (`joshavant`) addresses a security/privacy concern where unmodified replies could flash in previews.
- **Session Management:** `PR #114842` (`steipete`) improves the performance of `sessions.list` by watermark-caching derived titles and implementing single-pass filtering.
- **Bug Fixes:** `PR #112515` (`sunlit-deng`) fixes plugin-hosted media disappearing during registry changes, and `PR #114254` (`lujiajing1126`) fixes cost reporting freezing after a gateway restart.

### 4. Community Hot Topics
The community is highly engaged on critical stability and feature requests.

- **Cross-Platform Gap:** `Issue #75` (115 comments, 80 👍) remains the most active discussion. The community is urgently requesting native Linux/Windows gateways to match the macOS experience, indicating a major barrier to adoption for non-Apple users.
- **Memory & Stability Crisis:** `Issue #91588` (21 comments, P0) detailing a memory leak from 350MB to 15.5GB is a top concern, reflecting frustration with the gateway's reliability under load.
- **Security & Trust:** `Issue #7707` (22 comments) regarding "Memory Trust Tagging by Source" shows a sophisticated user base concerned about poisoning attacks. This is paired with `Issue #10659` (15 comments, 4 👍) for "Masked Secrets" to prevent API key exposure.
- **Telegram Duplicate Replies:** `Issue #86519` (14 comments, P1) reports a regression causing agents to reply 2-10x on Telegram post-update, highlighting pain in a key messaging channel.
- **TUI Accessibility:** `Issue #10118` (6 comments, 4 👍) requesting `Shift+Enter` for newlines reflects a desire for a more mature terminal experience.
- **Duplicate Startup Work:** `PR #114743` discusses reducing duplicate `chat.startup` requests, a clear pain point for users managing multiple sessions in the Control UI.

### 5. Bugs & Stability
The project is grappling with several high-severity bugs:

**Critical (P0):**
- **Gateway Memory Leak (OOM):** `Issue #91588` (RSS grows to 15.5GB) is the most severe stability issue. *No fix PR linked.*
- **State Migration Failure:** `Issue #109867` (8 comments, 7 👍) blocks gateway startup after a beta upgrade due to an invalid migration order. *Closed with fix.*

**High (P1):**
- **Session Initialization Conflict:** `Issue #102020` (16 comments) – "Second message in a session fails". *Closed.*
- **Telegram Duplicate Replies:** `Issue #86519` (14 comments) – persistent regression. *No fix PR linked.*
- **Gateway Heap Growth:** `Issue #87109` (9 comments) – Heap grows to 1073MB+ at idle, causing silent cron failures. *Open.*
- **Ollama Streaming Not Consumed:** `Issue #94251` (8 comments) – Chat sessions stall. *Open, linked to a PR.*
- **Lobster Workflow Hang:** `Issue #87756` (8 comments) – Regression where a prompt-launched workflow hangs. *Open.*

**Significant (P2):**
- **Session Context Bloat:** `Issue #67419` (10 comments) – 20-30% of context wasted on bootstrap file re-injection. *Open.*
- **SQLite Snapshot Guarantees:** `Issue #113306` (12 comments) – Snapshot restore lacks crash guarantees. *Open.*

### 6. Feature Requests & Roadmap Signals
Based on issue labeling and maintainer activity, several features are likely on the roadmap:

- **Security Hardening:** `Feature Request: Denylist for exec-approvals` (#6615), `Masked Secrets` (#10659), and `Filesystem Sandboxing Config` (#7722) point to a strong push for a trust-based security model.
- **Session & Context Management:** `Memory Trust Tagging by Source` (#7707) and `Config option to suppress sub-agent announce` (#8299) indicate a focus on giving users more granular control over agent memory and behavior.
- **Cross-Platform Support:** The immense popularity of `Issue #75` suggests Linux/Windows apps are a high-priority, though likely a long-term undertaking.
- **Model Management:** `Dynamic model discovery` (#10687) and `Trigger fallback on context length exceeded` (#9986) show a need for smarter, more resilient provider handling.

### 7. User Feedback Summary
**Pain Points:**
- **Reliability & Stability:** The most significant feedback relates to the gateway being unstable, with OOM crashes (`#91588`), heap leaks (`#87109`), and silent cron failures.
- **Feature Parity:** Users on Linux/Windows feel abandoned without native apps (#75).
- **Security Anxiety:** Users are explicitly worried about prompt injection, memory poisoning, and API key leaks (#7707, #10659).
- **Usability Regressions:** The Telegram duplicate message bug (#86519) and the loss of user-configured heartbeat prompts (#40255) show that regression testing needs improvement.

**Satisfaction & Use Cases:**
- Users are actively building complex automations (cron jobs with 70+ tool calls, #91532) and multi-agent workflows (sub-agent spawns, #8299), indicating high engagement with the platform for advanced use cases.
- The demand for accessibility features (TUI emoji config, #9637) and multi-line input (#10118) shows a maturing user base that wants a professional-grade terminal experience.

### 8. Backlog Watch
Several important, long-open issues require maintainer attention:

- **`Issue #75` [Linux/Windows Clawdbot Apps (115 comments)]:** Created 2026-01-01. The most requested feature with no clear resolution path. This is a strategic bottleneck for user acquisition.
- **`Issue #6615` [Denylist for exec-approvals (10 comments, 8 👍)]:** Created 2026-02-01. A simple, high-value security feature that has been sitting with `needs-product-decision` for months.
- **`Issue #7722` [Filesystem Sandboxing Config (10 comments, 4 👍)]:** Created 2026-02-03. Another critical security feature stuck in the "product decision" queue.
- **`Issue #67419` [Session context bloat (10 comments, 2 👍)]:** Created 2026-04-15. A performance issue affecting every user session, awaiting `needs-maintainer-review`.
- **`Issue #11665` [Webhook multi-turn support (11 comments)]:** Created 2026-02-08. A documentation/behavior mismatch that breaks a documented feature; linked to an open PR but has been stalled for months.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided digest summaries.

---

## Cross-Project Ecosystem Comparison Report
**Date:** 2026-07-28
**Prepared for:** Technical Decision-Makers & AI Agent Developers

### 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is in a state of **hyperactive maturation**, characterized by a split between massive, full-stack reference projects (like OpenClaw) and specialized, lightweight tools. The dominant theme is a **stability versus velocity tension**: while some projects ship major rewrites (IronClaw v1.0.0) or see hundreds of daily PRs (OpenClaw, CoPaw), most are grappling with systemic regressions in memory management, session state, and cross-platform support. Community feedback is coalescing around **critical, unsolved infrastructure problems**: memory leaks, prompt injection vulnerabilities, and poor Windows/Linux parity. The landscape is also witnessing a shift from basic chat agents toward **multi-agent orchestration, sandboxed execution, and enterprise-ready channel integrations** (Telegram, Feishu, Discord, Signal), indicating a move away from demo-ware toward production deployments.

### 2. Activity Comparison

| Project | Updated Issues (24h) | Updated PRs (24h) | Merged/Closed PRs | Release This Period | Project Health Score |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 500 | 230 | None | 🟡 **Moderate** (High activity, P0 bugs, critical memory leak) |
| **NanoBot** | 64 | 37 | 24 | None | 🟢 **Good** (High merge velocity, low active issues) |
| **Hermes Agent** | 50 | 50 | 11 | None | 🟡 **Moderate** (High activity, P1 bugs, platform friction) |
| **PicoClaw** | 5 | 4 | 0 | None | 🔴 **Concerning** (No merges, critical hang bug, no maintainer response) |
| **NanoClaw** | N/A | 9 | 1 | None | 🟢 **Good** (Steady maintenance, active PR pipeline) |
| **NullClaw** | 0 | 1 | 0 | None | 🔴 **Dormant** (Near-zero activity, stale dependency PR) |
| **IronClaw** | 39 | 50 | 19 | **v1.0.0 (Reborn)** | 🟡 **Moderate** (Post-launch chaos, critical connection bugs) |
| **LobsterAI** | 7 | 9 | 5 | None | 🟡 **Moderate** (Steady progress, critical data-corruption bug) |
| **Moltis** | 0 | 5 | 0 | None | 🟢 **Good** (Focused dev push, active security hardening) |
| **CoPaw** | 50 | 49 | 15 | None | 🟢 **Good** (High activity, healthy closure rate) |
| **ZeroClaw** | 48 | 50 | 12 | None | 🟡 **Moderate** (High-intensity security push, fragile CI) |
| **TinyClaw / ZeptoClaw** | 0 | 0 | 0 | None | 🔴 **Inactive** (No activity) |

*Health Score: 🟢 Good (active, merging, low critical bugs) | 🟡 Moderate (active but with significant bugs or velocity issues) | 🔴 Concerning/Dormant (critical bugs unanswered, low or no activity)*

### 3. OpenClaw’s Position

OpenClaw remains the **undisputed reference implementation** for the ecosystem, dwarfing all peers in raw activity (500 issues/500 PRs updated daily). Its key advantages include:

- **Unmatched Community Scale:** It is the only project where users are operating at massive scale (e.g., cron jobs with 70+ tool calls), generating the most sophisticated feedback on stability and security.
- **Technical Depth:** it is the only project actively working on "Memory Trust Tagging by Source" and "Masked Secrets" for advanced prompt injection defense, a problem others have not yet scoped.
- **Architecture:** It is the only project (along with IronClaw) undergoing a core session/context management re-architecture, whereas peers like NanoBot and CoPaw are focused on feature/plugin expansion.

**Key Weaknesses vs. Peers:**
- **Stability Gaps:** Despite its activity, OpenClaw is suffering from a P0 memory leak (350MB -> 15.5GB) and a P1 Telegram regression--bugs that, if unresolved, erode trust faster than peers who ship less frequently.
- **Cross-Platform Gap:** This is OpenClaw's single greatest strategic bottleneck, as explicitly called out in Issue #75. It is effectively a macOS-only platform, whereas IronClaw, NanoBot, and CoPaw all support Linux and Windows natively.

**Advantage Summary:** OpenClaw owns the **cutting edge of feature development and community insight**, but it is **losing the parity and stability race** to leaner projects.

### 4. Shared Technical Focus Areas

Multiple projects are independently converging on the same problems, validating these as ecosystem-wide priorities:

1.  **Session & Memory State Management (Critical):**
    - *Projects:* **OpenClaw** (P0 memory leak, session context bloat), **NanoBot** (cron session lock-in, memory consolidation failure), **Hermes Agent** (stale TUI session state), **LobsterAI** (settings loss, silent config corruption).
    - *Need:* Robust, leak-proof, and crash-safe session persistence.

2.  **Security Hardening (Prompt Injection/Secrets/Authorization):**
    - *Projects:* **OpenClaw** (Memory trust tagging), **ZeroClaw** (API key leakage, auth bypass in channels), **Moltis** (gating `/sh` command), **CoPaw** (exec bypass via Python), **LobsterAI** (attachment path traversal).
    - *Need:* A comprehensive, multi-layered security model that goes beyond basic input sanitization.

3.  **Cross-Platform Parity (Windows/Linux/macOS):**
    - *Projects:* **OpenClaw** (Issue #75 - urgent gap), **Hermes Agent** (Windows paths, macOS keyboard layouts), **LobsterAI** (PowerShell 5.1 hardcode), **CoPaw** (Windows vector index failure, PATH separator bug).
    - *Need:* First-class, tested support for all three major desktop OSs.

4.  **Channel Reliability & Feature Parity:**
    - *Projects:* **OpenClaw** (Telegram duplicate replies), **CoPaw** (Feishu bot not replying), **IronClaw** (Telegram pairing confusion), **NanoClaw** (Signal attachment paths).
    - *Need:* Deterministic, non-regressing behavior across all supported messaging platforms.

5.  **Error Recoverability & User Feedback:**
    - *Projects:* **IronClaw** (Error-recoverability endgame epic #6284), **OpenClaw** (silent cron failures), **NanoBot** (silently swallowed tool validation errors).
    - *Need:* The system must communicate failures clearly and allow for recovery, rather than silently failing.

### 5. Differentiation Analysis

| Feature/Approach | OpenClaw | NanoBot | IronClaw | CoPaw | ZeroClaw |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Primary Target User** | Advanced developers, power users | Broader base, i18n/Chinese market | Professional/enterprise (now v1.0 "Reborn") | Enterprise (Asian channels, AgentScope Platform) | Security-focused developers |
| **Core Architecture** | Monolithic reference (macOS-focused) | Modular (skills, Apps, MCP) | Monolithic, sandboxed (v1 Reborn rewrite) | Integrated with AgentScope Platform | Modular, WASM plugins, strict sandbox |
| **Key Feature Focus** | State-of-art features, big community | WebUI polish, new channels (LINE) | Core stability, error recovery, safety | Channel parity (Feishu/DingTalk), task execution | Security audit, policy hardening, CI reliability |
| **Architecture Differentiator** | Deepest context/session architecture | "Unified Extension Platform" (#5098) | "Hermetic capability platform", credential firewall | Visual Compact (context compression), ReMe Memory | WASM plugin backends, Landlock sandbox |
| **Risk Profile** | High feature velocity, high regression risk | High merge velocity, low active issues | Post-launch bug fix chaos | Moderate, healthy closure rate | Security-driven, fragile CI |

### 6. Community Momentum & Maturity

- **Tier 1: Hyperactive & Evolving (High Risk/High Reward):**
    - **OpenClaw** & **IronClaw**: These projects are pushing the boundary of what is possible but are also the most likely to break. IronClaw is stabilizing a major rewrite; OpenClaw is managing a firehose of contributions. They attract the most ambitious and tolerant developers.

- **Tier 2: High-Velocity & Stable:**
    - **NanoBot**, **CoPaw**, & **ZeroClaw**: These projects are merging code at a high rate while maintaining a more manageable bug profile. They represent the "sweet spot" of active development without the existential instability of Tier 1. NanoBot stands out for its nearly clean issue list.

- **Tier 3: Steady & Focused:**
    - **Hermes Agent**, **LobsterAI**, **NanoClaw**, **Moltis**: These projects are iterating steadily with a smaller scope. They are great for developers who need a reliable, specialized tool (e.g., Moltis for Discord bots, NanoClaw for Signal).

- **Tier 4: Stagnant / Inactive:**
    - **PicoClaw**, **NullClaw**, **TinyClaw**, **ZeptoClaw**: These projects show either zero or very low activity with no maintainer responsiveness. **PicoClaw is a particular risk** as it has critical bugs and zero merges, suggesting it may be abandoned. These should be avoided for new development.

### 7. Trend Signals

The data reveals three powerful trends that directly impact AI agent developers:

1.  **The "Production Wall":** The community is moving from "can it work?" to "can I rely on it?" This is the most important signal. The top complaints are no longer about missing features, but about **data integrity, silent failures, and platform lock-in**. Developers building on these platforms should prioritize projects with strong error-recoverability epics (IronClaw, ZeroClaw) and clear state management.

2.  **Security as a First-Class Citiizen:** The ecosystem is waking up to the fact that agentic AIs are uniquely vulnerable. The volume of security issues (prompt injection, API key leaks, tool bypasses) is scaling with adoption. The **"audit wave"** seen in ZeroClaw will likely hit other projects soon. Developers should plan for a future where rigorous security auditing is a prerequisite for any serious deployment.

3.  **The Rise of the "Operating System for Agents":** Projects like **IronClaw** (v1.0 Reborn) and **OpenClaw** (with its deep context/session work) are no longer just "chatbots." They are becoming operating systems for running a fleet of agents, with their own process lifecycle, filesystem sandboxing, and memory management. This is a fundamental shift away from plugins and toward a core runtime that manages all agent operations. Developers evaluating these platforms should consider the long-term architectural commitment this implies.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-28

## Today's Overview
NanoBot shows **very high** activity today after a prolonged period of accumulating closed issues: **64 issues** and **37 pull requests** were updated in the last 24 hours, though nearly all were previously-closed items receiving final activity. Only **1 open/active issue** remains, suggesting a major cleanup or triage sweep. The project has **13 open PRs** against **24 merged/closed**, with several high-priority fixes and new features reaching completion. **No new releases** were published, indicating that while development is active, no cut has been formalized today. The maintainer team, led by `chengyongru`, appears to be aggressively merging bug fixes and WebUI improvements.

## Releases
**None.** No new versions were tagged or published today.

## Project Progress
**24 pull requests were merged or closed** today. Key advances:

- **WebUI & UX**: Multiple PRs improved the WebUI composer experience, including switching model presets from the composer (#5077, merged), preventing composer resize scroll jitter (#5121, merged), softening model selector emphasis (#5119, merged), stabilizing repeated model preset rows (#5113, merged), and honoring custom gateway ports with Vite (#5076, merged). Brand assets were migrated to SVG (#5080, merged).

- **System Stability & Reliability**: A critical fix corrected double-encoding of git object IDs in `GitStore`, fixing memory session integrity (#5124, closed; superseded by #5126, open). Dream input integrity was preserved (#5114, merged). Session consolidation no longer drops uploaded media paths (#5120, open). A guard was added against invalid idle-compaction timestamps (#5117, open).

- **Documentation**: The README landing page was improved with clearer H1, GitHub star CTA, and actionable contribution paths (#5123, merged).

- **Extensions Platform**: A **significant new feature** (#5098, open) introduces a unified native extension platform, filling the code-level capability gap beyond skills, Apps, and MCP.

- **New Channel**: LINE Messaging API channel was contributed (#5115, open), targeting Japan, Taiwan, Thailand, and Indonesia markets.

- **Agent Readiness**: The `nanobot status` command was extended to check agent readiness offline (#5110, open).

## Community Hot Topics
The most active discussions this period are all **previously-closed issues** receiving final comments, likely from the triage sweep:

1. **[#1991 — Multiple custom model providers](https://github.com/HKUDS/nanobot/issues/1991)** (9 comments) — User request for supporting multiple custom model configurations with easy switching. Closed today, indicating this feature may have been addressed or deferred.

2. **[#3123 — Cron/scheduled task message send issues](https://github.com/HKUDS/nanobot/issues/3123)** (8 comments) — Cron jobs use the cron session for sending, preventing users from asking follow-up questions or requesting corrections on sent content. A core UX limitation for scheduled/delayed interactions.

3. **[#2570 — Local Ollama config 404 error](https://github.com/HKUDS/nanobot/issues/2570)** (7 comments) — Users running local models (Qwen2.5) report `404` errors and gateway not listening on the expected port. Persistent pain point for self-hosted users.

4. **[#2329 — Custom model provider fails on channels but works on CLI](https://github.com/HKUDS/nanobot/issues/2329)** (6 comments) — The `401 invalid_model` error suggests channel-specific configuration is not propagated correctly.

5. **[#1174 — Memory consolidation failures with local/cloud model mixing](https://github.com/HKUDS/nanobot/issues/1174)** (5 comments, 2 👍) — Long-running issue where switching from cloud to local models blocks new sessions. Users cannot bypass forced memory consolidation.

## Bugs & Stability
| Severity | Issue | Summary | Fix PR Exists? |
|----------|-------|---------|----------------|
| **Critical** | [#4792](https://github.com/HKUDS/nanobot/issues/4792) | `/stop` command silently discards all pending queue messages permanently | No |
| **High** | [#4805](https://github.com/HKUDS/nanobot/issues/4805) | `suppress(Exception)` in `prepare_call` silently swallows tool validation errors | No |
| **High** | [#5126](https://github.com/HKUDS/nanobot/pull/5126) | `GitStore` double-hex-encodes git object IDs, corrupting memory session references | ✅ #5126 (open) |
| **Medium** | [#5120](https://github.com/HKUDS/nanobot/pull/5120) | Session consolidation drops uploaded media paths in `media[]` | ✅ #5120 (open) |
| **Medium** | [#5117](https://github.com/HKUDS/nanobot/pull/5117) | Invalid timestamps crash idle compaction | ✅ #5117 (open) |
| **Low** | [#5113](https://github.com/HKUDS/nanobot/pull/5113) | Repeated model preset rows not stable in WebUI | ✅ #5113 (merged) |

**No new high-severity crashes or regressions were reported today.** Existing infrastructure bugs (cron, memory consolidation) continue to drive user frustration.

## Feature Requests & Roadmap Signals
Today's PRs and issues signal several likely upcoming features:

- **Unified Extension Platform** (#5098) — A deliberate native Python extension boundary that reuses nanobot's tool, command, and hook registries. Likely to land in next release.
- **LINE Messaging API Channel** (#5115) — New channel for major Asian markets; high probability of merge.
- **Dream Runs in WebUI** (#5112) — Read-only session exposure for Dream-generated workflows, including reasoning and tool calls.
- **skills.sh Marketplace** (#5116) — In-WebUI discovery and installation of third-party skills.

From the community:
- Multiple custom model providers with switching (#1991) — closed, may have been resolved or postponed.
- Configurable system prompt emoji (#2747) — minor but indicates users want prompt customization.
- Plugin support comparable to OpenClaw (#1881) — requested for integrating advanced web tools and memory management.

## User Feedback Summary
Users express **moderate satisfaction** with core functionality but **frustration** around:

- **Local model integration**: Multiple reports of Ollama/LM Studio setup failures (#2570, #1590, #1478, #1947) with confusing error messages. Users have to debug configuration manually.
- **Channel-specific behavior**: Custom models work on CLI but fail on Feishu, Discord, or WhatsApp (#2329, #1672). Cron jobs and message forwarding do not propagate correctly across channels.
- **Memory and state management**: Memory consolidation failures block session creation (#1174). Cron messages sent from cron sessions cannot be referenced later (#3123).
- **Missing progress indicators**: Feishu channel does not show `send_progress` notifications (#3166), even though other channels do.
- **Non-English users**: Chinese-language issue posters face a language barrier; issues are often filed in Chinese with English summaries, suggesting the project has a significant international user base.

## Backlog Watch
The following high-signal items remain **unaddressed** despite high user investment:

| Issue | Age | Comments | Status |
|-------|-----|----------|--------|
| [#1174](https://github.com/HKUDS/nanobot/issues/1174) — Memory consolidation failures | 5 months | 5 comments, 2 👍 | Closed today; root cause may still exist |
| [#1033](https://github.com/HKUDS/nanobot/issues/1033) — Inter-instance cache staleness | 5 months | 3 comments | Closed today |
| [#1328](https://github.com/HKUDS/nanobot/issues/1328) — Agent and gateway don't share skills | 5 months | 2 comments | Closed today |
| [#4792](https://github.com/HKUDS/nanobot/issues/4792) — `/stop` message loss (Critical) | 22 days | 3 comments | Still open; no maintainer response |
| [#4805](https://github.com/HKUDS/nanobot/issues/4805) — Silenced tool validation errors (High) | 22 days | 2 comments | Still open; no maintainer response |
| [#3559](https://github.com/HKUDS/nanobot/issues/3559) — WebSocket cannot replace webhooks for proactive delivery | 3 months | 3 comments | Closed today |

**Maintainer attention needed**: The two critical bugs (#4792, #4805) have no fix PRs and no maintainer comments, despite being open for 22 days. The repository's high volume of closed issues today suggests a triage pass but not necessarily substantive resolution for these deeper infrastructure issues.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-28

## 1. Today's Overview

Hermes Agent is experiencing a **high-velocity development day** with 50 issues and 50 PRs updated in the last 24 hours, indicating intense community and maintainer activity. The project has 39 open issues and 39 open PRs, with 11 of each closed or merged—suggesting healthy review throughput. **No new releases** were published today, but multiple critical bugs (P1) were reported, including an abort-function No-Op vulnerability and shutdown data-loss risk. The project's cross-platform health shows ongoing Windows and macOS compatibility friction, particularly around path handling and keyboard layout support.

## 2. Releases

**No new releases** were published on 2026-07-28. The last release remains v2026.7.20 (per issue #69398 references).

## 3. Project Progress — Merged/Closed PRs Today

11 PRs were closed or merged today. Notable advancements:

- **#73015** (closed) — `fix(desktop): resolve keybinds through the active keyboard layout` — Fixes a long-standing Dvorak/non-QWERTY keyboard bug by using `event.key` instead of `event.code` for letter shortcuts. *Closes #46369*
- **#72893** (closed) — `Collapse a turn's tool activity into one grouped, live-ticking line` — Desktop UX improvement reducing visual noise during multi-tool turns.
- **#73019 / #73023** (closed) — Automated JS lint/format PRs auto-merged.
- **#46374** (closed) — Another keyboard-layout fix PR (Dvorak compatible), merged after 43 days open.
- **#66757** (closed) — Desktop i18n config respect (labeled as duplicate, but the intent was merged elsewhere).
- **#71817** (closed) — CDP URL configuration startup delay fix (closed as duplicate).
- **#47656** (closed) — Windows browser UnicodeDecodeError fix.
- **#72667** (closed) — MCP stdio stale-process leak fix on macOS.

**Fix PRs now open for review:**
- **#73016** — Escalate abort when TCP close finds 0 sockets (fixes P1 #72975)
- **#73020** — Flush pending messages to disk before shutdown clear (fixes P1 #72680)

## 4. Community Hot Topics

### Most Active Issues (by comment count)
- **#67600** (13 comments) — *[Bug]: Desktop session sidebar empty for `default` profile* — 7 days old, still unresolved. Community frustration around profile-scoped session visibility. [Link](https://github.com/NousResearch/hermes-agent/issues/67600)
- **#61396** (5 comments) — *[Bug]: node-pty spawn-helper execute bit on macOS arm64* — Terminal crashes on Apple Silicon. Workaround exists but no fix merged. [Link](https://github.com/NousResearch/hermes-agent/issues/61396)
- **#63177** (5 comments) — *[Bug]: search_files silently returns 0 results on Windows absolute paths* — ripgrep + MSYS path conversion conflict. Deep platform friction. [Link](https://github.com/NousResearch/hermes-agent/issues/63177)
- **#68339** (4 comments) — *[Bug]: mixed-batch tool execution causes early-session behavior shift* — Subtle behavioral regression in agent reasoning. Needs maintainer decision. [Link](https://github.com/NousResearch/hermes-agent/issues/68339)
- **#26037** (4 comments) — *[Bug]: Feishu reply-to-image loses parent context* — Platform-specific feature gap, 74 days open. [Link](https://github.com/NousResearch/hermes-agent/issues/26037)

### Most Active PRs (by comment count)
All top PRs have undefined/0 comments in the data provided, suggesting community is engaging more on issues than PRs today.

**Underlying needs:** Users are experiencing **profile-specific data loss** (empty sidebar, pairing store path changes, session routing errors) and **cross-platform compatibility pain** (Windows paths, macOS keyboard layouts, MCP server leaks). The community is demanding better state management and platform testing.

## 5. Bugs & Stability

### Critical (P1)
| Issue | Summary | Fix PR Exists |
|-------|---------|---------------|
| **#72975** | `_abort_request_openai_client()` silently no-ops when `force_close_tcp_sockets()` returns 0, leaving requests alive for minutes | **Yes** — #73016 |
| **#73020** (PR) | Gateway `_pending_messages.clear()` during shutdown discards unsaved messages (data loss) | In review as fix for #72680 |

### High (P2)
| Issue | Summary | Status |
|-------|---------|--------|
| **#67600** | Desktop sidebar empty for `default` profile only | Open, 9 days old |
| **#63177** | `search_files` returns 0 results on Windows absolute paths | Open, needs platform fix |
| **#72971** | `prompt.submit` sends to wrong session after session switch during streaming | Open, 1 day old |
| **#42376** | macOS plist `LimitLoadToSessionType` breaks launchctl bootstrap on macOS Tahoe | Open, 50 days old |
| **#68137** | One-shot mode (`-z`) drops slow MCP servers silently | Open, 8 days old |
| **#69398** | v2026.7.20 pairing store path migration breaks existing approvals | Open, 6 days old |
| **#70253** | Inbound images dropped when arriving during busy turn | Open, 5 days old |
| **#69107** | TUI session state stale when another client writes | Open, 6 days old |
| **#66086** | Docker gateway silently drops MEDIA attachments for container-local paths | Open, 11 days old |
| **#72970** (closed) | Windows startup slow due to skill provenance backfill | Closed as duplicate |

### Moderate (P3)
| Issue | Summary | Status |
|-------|---------|--------|
| **#70719** | File-mutation verifier fires on arg-missing patch calls (noisy banner) | Open, 4 days old |
| **#62397** | Background review fork can't patch skills (read-before-write mismatch) | Open, 17 days old |
| **#72981** | Managed Cloud Honcho dependency install fails with permission denied | Open, 1 day old |

**Stability signals:** Three active P1 bugs (two with fix PRs) and consistent P2 issues around session state, file delivery, and platform compatibility. The project has a **high bug-fix velocity** but Windows and macOS issues persist as chronic pain points.

## 6. Feature Requests & Roadmap Signals

### New Today (2026-07-28)
- **#73017** (PR) — *Prompt-cache prewarm for TUI/desktop sessions* — Reduces first-message latency from ~20s to ~4s by prewarming provider-side prefix cache. **Likely to be in next release** given clear perf benefit.
- **#73008** (PR) — *Durable thread run lifecycle for Discord gateway* — Adds run markers and lifecycle classification. Medium priority.
- **#72842** (PR) — *Add hermes-ngit skill for Nostr-based Git* — Decentralized code hosting integration. Niche but adds backend diversity.
- **#70509** (PR) — *On-device wake words with open-vocabulary phrases* — Blocks on `needs-decision`. High complexity, likely deferred.
- **#67875** (PR) — *Friendli as first-class API-key provider* — New provider addition, moderate priority.

### Long-Open Requests
- **#29483** (66 days) — *Slack progress drafts as plan cards* — **2 upvotes**, still open. UX improvement for tool-heavy workflows.
- **#33489** (62 days) — *BlueBubbles group chat filtering* — Still open, community wants chat-type filtering.

**Prediction for next version:** Cache prewarm (#73017), keyboard layout fix (#73015), abort escalation (#73016), and shutdown data-loss fix (#73020) are strong candidates. The Nostr Git skill and Friendli provider may also ship.

## 7. User Feedback Summary

### Pain Points (Voiced in Issues)
- **Profile-scoped data loss:** "Desktop session sidebar is completely empty for the `default` profile" (#67600) — users losing access to sessions.
- **Cross-platform frustration:** "search_files silently returns 0 results on Windows" (#63177), "Dvorak keyboard shortcuts broken" (#46369, now fixed) — Windows/macOS users feel second-class.
- **Silent failures:** "One-shot mode drops slow MCP servers silently" (#68137), "Gateway silently drops MEDIA attachments" (#66086) — trust erosion from non-diagnosed failures.
- **Upgrade breakage:** "Existing pairing approvals silently stop working after upgrade" (#69398) — breaking changes without migration.
- **Abort reliability:** "Interrupt silently no-ops for minutes" (#72975) — users can't stop runaway requests.

### Positive Signals
- Three keyboard layout fix PRs merged today (#73015, #46374) — community feedback on Dvorak pain was heard.
- Cache prewarm PR (#73017) addresses the most visible performance complaint (20s first message).
- Multiple automation PRs (#73019, #73023) show CI maturity.

### Use Cases Emerging
- **Nostr/Git decentralized workflows** (#72842) — expanding beyond centralized platforms.
- **On-device voice wake words** (#70509) — privacy-conscious interaction model.
- **Friendli provider** (#67875) — demand for more API provider diversity.

## 8. Backlog Watch

### Issues Needing Maintainer Attention
| Issue | Days Open | Age | Reason |
|-------|-----------|-----|--------|
| **#26037** — Feishu reply-to-image loses context | 74 days | `P3` | Niche platform, but labeled `sweeper:risk-message-delivery` — message delivery reliability |
| **#42376** — macOS Tahoe launchctl breakage | 50 days | `P2` | `needs-decision` label. Affects macOS users on latest OS |
| **#61396** — node-pty macOS arm64 crash | 19 days | `P3` | Terminal completely unusable on Apple Silicon. No maintainer response |
| **#63177** — Windows search_files silent 0 results | 16 days | `P2` | Two duplicate issues (#67629) — major Windows workflow blocker |
| **#67600** — Desktop sidebar empty for default profile | 9 days | `P2` | High community engagement (13 comments), no fix |
| **#69398** — v2026.7.20 pairing store migration breakage | 6 days | `P2` | Upgrade breaks existing configurations. `area/profiles` |
| **#33489** — BlueBubbles group chat filtering | 62 days | `P3` | Straightforward filter feature, 2 upvotes, zero maintainer activity |

### PRs Stuck in Review
| PR | Age | Summary | Blockers |
|----|-----|---------|----------|
| **#12299** — Mattermost thread metadata fix | 101 days | Prefer metadata thread root over stale reply_to | `needs-decision`, rebased but not merged |
| **#70509** — On-device wake words | 4 days | High-complexity voice feature | `needs-decision` |

**Notable:** The `needs-decision` label is blocking 4+ issues/PRs, suggesting the maintainer team may have bandwidth constraints for design-level decisions. The `sweeper:risk-session-state` and `sweeper:risk-message-delivery` tags appear on 15+ open items, indicating user-data-integrity concerns are the project's most critical backlog theme.

---

**Project Health Rating:** 🟡 **Moderate** — High activity and good fix velocity, but chronic Windows/macOS platform issues, upgrade-breaking changes, and maintainer decision bottlenecks temper momentum. The P1 bugs today (abort No-Op, shutdown data loss) are serious but both have fix PRs, reflecting healthy incident response.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for **2026-07-28**.

---

## PicoClaw Project Digest – 2026-07-28

### 1. Today's Overview
Project activity is **moderate**, with a clear focus on **stabilizing the agent core and expanding usability**. Five open Issues and four open PRs were updated in the last 24 hours, though **zero items were closed or merged**, indicating a potential bottleneck in review or merge capacity. The community is actively reporting reliability bugs (agent hangs, UI lag) and submitting high-quality localization and provider updates. The absence of a release this cycle suggests the project is in a **consolidation phase** before a potential 0.4.0 release.

### 2. Releases
**No new releases** were detected in the last 24 hours. The latest tagged release remains **v0.3.1**.

### 3. Project Progress
**Merged/Closed PRs today:** **0**. No code was merged or closed in the last 24 hours. However, several significant open PRs advanced in discussion or review:

- **#3273 – feat(webui): add Japanese (ja) localization** – A fully ready 968-line translation file plus dayjs integration. Community response aligns with the related feature request #3272.
- **#3271 – chore(providers): update default model names to 2026-07 latest** – Refreshes model lists for 9 providers (OpenAI, Anthropic, etc.) to match official documentation.
- **#3270 – feat: add DashScope TTS provider and WeChat audio file sending** – Brings Alibaba Cloud TTS and WeChat audio integration.
- **#3200 – feat(models): add configurable default fallback chain** – A long-standing PR (27 days open) adding a user-facing fallback model workflow in the WebUI.

### 4. Community Hot Topics
- **#3272 / #3273 – Japanese Localization (Feature + PR)**
  - *Link:* [#3272](https://github.com/sipeed/picoclaw/issues/3272), [#3273](https://github.com/sipeed/picoclaw/pull/3273)
  - A user requested and simultaneously submitted a complete Japanese translation for the WebUI. This demonstrates strong **international interest** and a mature community that submits code with requests. The underlying need is broader i18n support for non-English speaking enterprise users.
- **#3269 – Agent hangs on MCP server failure**
  - *Link:* [#3269](https://github.com/sipeed/picoclaw/issues/3269)
  - The highest-impact bug being discussed. A user running Qwen3 reports that a failed MCP connection causes the whole agent loop to freeze, making the chat interface unresponsive. This is a **critical reliability issue** for production deployments.
- **#3281 – WebUI chat input lag with long history**
  - *Link:* [#3281](https://github.com/sipeed/picoclaw/issues/3281)
  - Multiple users are tacitly agreeing that the WebUI frontend has a performance bottleneck when rendering long chat contexts. No fix PR exists yet.

### 5. Bugs & Stability
**Severity ranking (High → Low):**

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **Critical** | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | Agent loop hangs on MCP connection failure – users entirely lose chat responses. | ❌ None |
| **High** | [#3281](https://github.com/sipeed/picoclaw/issues/3281) | WebUI chat input severe lag with moderate history (>20 messages). | ❌ None |
| **Medium** | [#3268](https://github.com/sipeed/picoclaw/issues/3268) | `exec` tool requires `action` field without default, causing LLM calls to fail unpredictably. | ❌ None |
| **Low** | [#3276](https://github.com/sipeed/picoclaw/issues/3276) | Launcher fails on unknown channel types and assumes full gateway lifecycle ownership. | ❌ None |

**No fix PRs have been opened for any of the above bugs.** This is a risk signal for the project’s responsiveness to stability issues.

### 6. Feature Requests & Roadmap Signals
- **Japanese WebUI l10n (#3272)** – Likely to land soon since a full PR (#3273) already exists. Expect inclusion in **v0.3.2 or v0.4.0**.
- **Model default fallback chain (#3200)** – 27 days open, no conflicts. This is a major UX improvement for reliability-mindful users. Likely target for next minor release.
- **Systemd gateway support (#3276)** – A niche but important request for headless/sysadmin users. May be deferred unless additional community demand appears.
- **DashScope TTS + WeChat audio (#3270)** – Aligns with the growing trend of **multi-modal output** and WeChat integration for the Chinese market. Strong candidate for next release.

**Prediction:** The next release will likely include: Japanese l10n, model fallback chain, and DashScope TTS.

### 7. User Feedback Summary
- **Pain Points:**
  - *"Agent dies silently"* – MCP connection failures break the entire chat (#3269).
  - *"WebUI input is unusable with long history"* – A common complaint from power users (#3281).
  - *"AI agents don't know how to call `exec` correctly"* – The `action` parameter default omission leads to silent LLM failures (#3268).
- **Positive Signals:**
  - Users are investing time to submit **full localization files** and **new provider integrations** (DashScope, WeChat). This indicates high trust and a desire to use PicoClaw in production.
  - A user explicitly called PicoClaw *"great for headless server deployments"* even while filing a bug, reflecting overall satisfaction with the architecture.

### 8. Backlog Watch
- **(⚠️ Stale, 28 days) #3200 – feat(models): add configurable default fallback chain**
  - *Link:* [#3200](https://github.com/sipeed/picoclaw/pull/3200)
  - No activity in the last 7 days. This is a high-value UX feature that has received zero maintainer review. Risk of divergence if not merged soon.
- **(⚠️ Stale, 8 days) #3271 – chore(providers): update default model names**
  - *Link:* [#3271](https://github.com/sipeed/picoclaw/pull/3271)
  - A low-risk, high-accuracy update. Without this, users manually selecting models may see outdated names. No merge activity yet.
- **All five open Issues have received exactly 1 comment each (the author)** – No maintainer responses have been recorded in any of the bug reports or feature requests. This suggests a **maintainer responsiveness gap** that may slow community momentum.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the project digest for **NanoClaw** on **2026-07-28**.

---

## NanoClaw Project Digest: 2026-07-28

### 1. Today's Overview
Project activity today is moderate, driven by infrastructure and integration fixes rather than major new features. While no new releases were cut, the team merged a critical bug fix regarding local configuration loading and continues to process a healthy backlog of community and core-team pull requests. The project shows consistent maintenance velocity, with 8 still-open PRs receiving attention in the last 24 hours. The focus appears to be on stabilizing the Signal integration, improving agent engagement-policy controls, and fixing issues with containerized skill configurations.

### 2. Releases
No new releases were published today. The latest release remains the previous version, with no breaking changes or migration notes to report.

### 3. Project Progress
One pull request was merged/closed today:

- **#2598** (Closed/Merged) – [**Fix**] **jonnychesthair-crypto**: Fixed loading of per-group `CLAUDE.local.md` by adding `'local'` to the `settingSources` list. This ensures that project-local configuration files are correctly recognized and applied across different group scopes.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/2598)

### 4. Community Hot Topics
No single issue or PR has attracted heavy comment or reaction volume today, but several ongoing efforts reflect community and core-team priorities:

- **#2971** – **zivisaiah**: Proposes a new `ncc` utility skill for host operational and health CLI. This is a standalone tool addition (no source changes), indicating community desire for better admin tooling.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/2971)

- **#3142** – **ira-at-work**: Fixes a broken attachment path for image/files in the Signal adapter, where attachments were stored at a path not mounted into the agent's container. This highlights a real-world integration pain point.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/3142)

- **#3050** – **OmriBenShoham**: Adds Dial as a channel option in the setup wizard and skill picker, showing interest in expanding supported communication channels.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/3050)

### 5. Bugs & Stability
No new bug reports were filed as issues today. However, several fix PRs are in the pipeline:

- **#3141** (Open) – **ERMOKHINNA**: Fixes a bug where the container compose logic did not respect `container.json` skill selections when loading `CLAUDE.md` fragments. This is a **moderate** bug impacting users who rely on skill-specific configuration in containerized environments.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/3141)

- **#3142** (Open) – **ira-at-work**: Addresses a **high priority** bug where the Signal adapter wrote attachment paths that were unreachable inside the agent container, effectively breaking all non-image, non-audio file handling.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/3142)

- **#3143** (Open) – **Koshkoshinsk**: Preserves resolved approval card content so that user-facing cards retain titles, requests, and decision status after resolution (instead of disappearing). This is a **low** severity but important UX polish fix.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/3143)

### 6. Feature Requests & Roadmap Signals
Several open PRs indicate likely roadmap directions:

- **Multi-channel expansion**: PR #3050 (Dial integration) and PR #2685 (Signal group typing, reactions, quote-reply) signal active effort to deepen and broaden communication channel support.
- **Self-serve wiring controls**: PR #3137 introduces group-scoped agent wiring inspection and engagement policy updates, pointing toward a future where agents are more autonomously configurable by users.
- **New utility skills**: PR #2971 (`ncc` health CLI) reflects user demand for better operational tooling outside the core agent loop.

### 7. User Feedback Summary
User pain points today center on **integration reliability** and **configuration correctness**:
- There is clear dissatisfaction with the Signal adapter's broken attachment handling (PR #3142), which prevents agents from receiving file-based inputs over that channel.
- The fix for per-group `CLAUDE.local.md` loading (PR #2598) suggests users were struggling with inconsistent local configuration behavior across different agent scopes.
- The container skill-fragment fix (PR #3141) hints at frustration when `container.json` skill selections are silently ignored.

Positive signals: community members are actively contributing standalone utility skills (PR #2971) and channel integrations (PR #3050), indicating a healthy ecosystem of contributors who find the skill framework usable and beneficial.

### 8. Backlog Watch
No long-unanswered issues or PRs were identified in the data. The oldest open PRs (e.g., #2346 from May 2026) are still being updated (last updated 2026-07-27), suggesting maintainers are not abandoning them but rather handling them at a measured pace. No items currently warrant automatic escalation.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-07-28**.

---

### NullClaw Project Digest – 2026-07-28

**1. Today's Overview**
The NullClaw repository is currently in a very low-activity state. There were no issues updated, no new releases, and no merged pull requests in the last 24 hours. The only significant activity is a single open dependency pull request (PR #956) which was last updated yesterday but remains open without review for over a month. The project appears to be in a maintenance lull with no active feature development or bug fixes evident in the recent data.

**2. Releases**
No new releases were published on this date. The repository has no version history listed.

**3. Project Progress**
No pull requests were merged or closed today. There were no features advanced or bugs fixed.

**4. Community Hot Topics**
The single active item is **PR #956**, which attempts to update the base Docker image from Alpine 3.23 to Alpine 3.24. This is a routine dependency bump opened by Dependabot. While the PR has no comments or reactions, the fact that it has been open since June 15 without action suggests a bottleneck in maintainer review or a lack of priority for infrastructure updates. The underlying need is basic supply chain security—keeping the CI/Docker environment current.

**5. Bugs & Stability**
No bugs, crashes, or regressions were reported in the last 24 hours. No stability issues are currently documented.

**6. Feature Requests & Roadmap Signals**
No feature requests were recorded in the last 24 hours. The absence of any user-submitted issues or discussions provides no strong signals regarding the project’s next feature direction.

**7. User Feedback Summary**
There is no user feedback (comments, reactions, or new discussions) available in the current data set. It is unclear if users are satisfied or dissatisfied, as the engagement level is near zero for this period.

**8. Backlog Watch**
The primary item requiring maintainer attention is **PR #956** ([GitHub Link](https://github.com/nullclaw/nullclaw/pull/956)). This routine infrastructure update has been open for 43 days (since June 15) without a review or merge. While not functionally critical, the delay could indicate maintainer bandwidth constraints that may affect future community contributions and project velocity.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-28

## Today's Overview

The IronClaw project is in an intense, highly active phase following the landmark **v1.0.0 stable release on 2026-07-27** — a ground-up rearchitecture branded "Reborn." Activity is exceptionally high: 39 issues and 50 pull requests were updated in the last 24 hours, with the team driving a **v1-launch-checklist** campaign to stabilize the new binary. Multiple critical bugs surfaced during real-world testing on staging and Railway instances, alongside sweeping refactoring work to collapse failure-handling enums, normalize extension lifecycle persistence, and build credential-firewall primitives for the sandbox. The project is simultaneously shipping production hardening and architectural debt reduction at high velocity.

## Releases

**ironclaw-v1.0.0** — released 2026-07-27

This is a **ground-up rewrite** of the agent runtime, storage, extension host, and web UI. It is not an increment on the 0.29.x line.

**Key changes:**
- The `ironclaw` binary is now the rearchitected CLI (Reborn)
- The v1 monolith builds as `ironclaw-legacy`
- **Breaking migration required** from pre-Reborn architecture (tracked in Issue [#6725](https://github.com/nearai/ironclaw/issues/6725))

**Migration notes (still being defined):**
- Internal engineering docs were being served publicly on the docs site; PR [#6692](https://github.com/nearai/ironclaw/pull/6692) added `docs/.mintignore` to fix this
- A migration-path epic ([#6725](https://github.com/nearai/ironclaw/issues/6725)) is tracking the path from `src/` monolith to v1, but the description is still pending

## Project Progress

**19 PRs merged/closed in the last 24 hours.** Notable advances:

**Core architecture & reliability:**
- PR [#6684](https://github.com/nearai/ironclaw/pull/6684) — Collapsed five overlapping failure-kind enums into one `host_api::FailureKind` (36 variants), fixing six wrongful-terminal / mis-retry bugs with regression tests. Directly advances the error-recoverability endgame epic (#6284)
- PR [#6696](https://github.com/nearai/ironclaw/pull/6696) — Made `ironclaw_processes` the single lifecycle authority for agent turns, capability invocations, and supervision state
- PR [#6723](https://github.com/nearai/ironclaw/pull/6723) — Added unwired credential-firewall primitives (SandboxCertificateAuthority + obligation staging) for the sandbox egress proxy
- PR [#6728](https://github.com/nearai/ironclaw/pull/6728) — Added nightly reverse-order journey testing for the hermetic capability platform (#6524)

**Extension & memory systems:**
- PR [#6724](https://github.com/nearai/ironclaw/pull/6724) — Rebuilt memory provider contract around declared capabilities: the bound provider's manifest is now the single source of truth for memory tools and lifecycle hooks
- PR [#6655](https://github.com/nearai/ironclaw/pull/6655) — Normalized extension lifecycle persistence into typed filesystem records with per-user membership and health records
- PR [#6737](https://github.com/nearai/ironclaw/pull/6737) — Fixed silent revert of extension behaviors caused by a merge conflict resolution in PR #6616

**Documentation & infrastructure:**
- PR [#6692](https://github.com/nearai/ironclaw/pull/6692) — Restructured docs site around the shipped 1.0 binary; fixed 33 internal doc paths returning HTTP 200 publicly
- PR [#6687](https://github.com/nearai/ironclaw/pull/6687) — 33 dependency updates across the crate tree

## Community Hot Topics

**Most active Issue:**
- **[#6284 — Error-recoverability endgame](https://github.com/nearai/ironclaw/issues/6284)** (14 comments) — This epic defines the contract that every mid-run error must satisfy: the run survives, the model sees the cause and the fix, and no non-success is ever reported as success. Multiple PRs today directly target this contract, indicating it is the team's highest-priority architectural concern.

**Active launch-blocker issues from staging QA:**
- **[#6581 — 429 Too Many Requests on SSE channel](https://github.com/nearai/ironclaw/issues/6581)** (3 comments) — WebChat v2's live-update SSE endpoint rate-limits under normal multi-thread usage, causing "Disconnected" badge on users
- **[#6718 — Streaming only resumes after switching pages](https://github.com/nearai/ironclaw/issues/6718)** — Continuous streaming breaks when stuck on "Reconnecting"
- **[#6719 — Conversation history fails to load after backend errors](https://github.com/nearai/ironclaw/issues/6719)** — 503 errors and CSP violations leave chat in broken state
- **[#6717 — Agent gives incorrect Telegram pairing instructions](https://github.com/nearai/ironclaw/issues/6717)** — After successful pairing, agent still tells user to connect Telegram
- **[#6716 — Model incorrectly claims Slack integration is unavailable](https://github.com/nearai/ironclaw/issues/6716)** — Hallucinates limitations despite Slack existing on the instance

**Design discussions:**
- **[#6524 — Hermetic capability testing platform](https://github.com/nearai/ironclaw/issues/6524)** (3 comments) — Epic for deterministic, meaningful coverage of every capability and critical user journey
- **[#6641 — Skill Self-Creation Design Doc](https://github.com/nearai/ironclaw/issues/6641)** — Design for hot-swappable, manifest-based skill-creation module, benchmarked across 86 tasks

## Bugs & Stability

**Critical / P1 bugs reported today:**

1. **[#6741 — Extension OAuth connection fails for Gmail, Calendar](https://github.com/nearai/ironclaw/issues/6741)** — After completing OAuth sign-in flow, connection fails with error. Brand new issue, no fix PR yet.

2. **[#6720 — Task runs indefinitely; stop button fails](https://github.com/nearai/ironclaw/issues/6720)** — P1 bug_bash: smoke test ran 15+ minutes, UI shows "Couldn't stop this run." Instance: Railway (ironclaw-qa-testing-libsql). No fix PR.

3. **[#6719 — Conversation history fails to load](https://github.com/nearai/ironclaw/issues/6719)** — Backend 503s + CSP violations leave conversation in partially broken state. v1-launch-checklist priority.

4. **[#6718 — Streaming only resumes after switching pages](https://github.com/nearai/ironclaw/issues/6718)** — Tool updates, reasoning, and streamed responses freeze while "Reconnecting." v1-launch-checklist priority.

5. **[#6575 — systemd service error after `ironclaw onboard`](https://github.com/nearai/ironclaw/issues/6575)** — Ubuntu local install fails immediately after onboarding. Closed but no fix noted.

**Regressions fixed today:**
- PR [#6737](https://github.com/nearai/ironclaw/pull/6737) — Fixed silent revert of extension behaviors from merge conflict (60-day scan found one regression)
- PR [#6697](https://github.com/nearai/ironclaw/pull/6697) — Fixed adapter finish-reason reporting: adapters now read the provider's real finish reason instead of inferring from response shape (epic #6284 item 8)

**Defect trends:**
- 4 issues closed in 24h: #4548 (DeepSeek duplicate model field — bug), #6060 (routine delivery target leakage), #6575 (systemd onboarding error), plus one unlisted
- Daily failure taxonomy [#6707](https://github.com/nearai/ironclaw/issues/6707) shows ClawBench has 83 non-passing tests, but the only hard (0.00) failures are a benchmark defect in ClawBench's per-task setup script

## Feature Requests & Roadmap Signals

**High-signal user-facing requests from today:**

1. **[#6743 — In-app feedback/bug report widget](https://github.com/nearai/ironclaw/issues/6743)** — Users must leave the app to report issues (Slack, GitHub). Request for persistent feedback button in WebUI. Likely next-version candidate given v1 launch.

2. **[#6742 — User profile details view](https://github.com/nearai/ironclaw/issues/6742)** — Profile menu has non-functional "IronClaw" item; users cannot see name, email, or which account is active. UX gap for multi-account users.

3. **[#6522 — IronClaw not aware how to setup Telegram locally](https://github.com/nearai/ironclaw/issues/6522)** — Needs user-facing instructions, even if CLI-based. Blocks Telegram production hardening epic (#6483).

**Roadmap-significant epics filed/updated today:**
- **[#6727 — Support custom/arbitrary MCP server](https://github.com/nearai/ironclaw/issues/6727)** — Only two MCP servers wired in at compile time; no CLI/WebUI/extension path for user-supplied MCP. Major extensibility gap.
- **[#6734 — Give agent access to own documentation](https://github.com/nearai/ironclaw/issues/6734)** — Let the running agent read `docs/reborn/` to guide tool/channel configuration instead of hallucinating.
- **[#6731 — Integrate IronHub into IronClaw](https://github.com/nearai/ironclaw/issues/6731)** — Turn tool/skill set into an extensible marketplace with runtime discovery, signed provenance checks.
- **[#6482 — Pluggable Memory Providers](https://github.com/nearai/ironclaw/issues/6482)** — Epic for provider-neutral memory extension surface. PR #6724 already lands the capability-based contract.
- **[#6481 — Unified Manifest-Driven Extension Platform](https://github.com/nearai/ironclaw/issues/6481)** — Manifest V3 schema roadmap. PR #6655 normalizes extension lifecycle records toward this.

## User Feedback Summary

**Pain points from v1-launch-checklist testing (all from staging/QA today):**

- **Connection stability is broken**: Users see "Disconnected" / "Reconnecting" state on WebChat v2; streaming stops until page switch (#6581, #6718)
- **Post-pairing confusion**: Telegram pairing succeeds, but agent still tells user to "look for Telegram pairing panel" (#6717)
- **Hallucinated limitations**: Model claims Slack "not installed" even when it exists; gives misleading instructions instead of helping configure (#6716)
- **Conversation loss**: Backend errors (503, CSP violations) permanently break conversation history loading (#6719)
- **Unstoppable tasks**: No way to cancel a long-running task; UI reports "Couldn't stop this run" (#6720)
- **Cannot identify own account**: Profile menu shows no user identity, problematic for multi-account users (#6742)
- **No feedback channel**: Users must leave app to report bugs (#6743)

**Satisfaction signals**: The team is running active QA (bug_bash_P1), generates daily failure taxonomies ([#6707](https://github.com/nearai/ironclaw/issues/6707)), and is methodically closing error-recoverability gaps. The v1.0.0 release marks a major milestone the team clearly intends to stabilize aggressively.

## Backlog Watch

**Issues needing attention:**
- [#4548 — DeepSeek duplicate model field bug](https://github.com/nearai/ironclaw/issues/4548) — Closed, but required a fix. Worth verifying the fix didn't regress on other OpenAI-compatible providers.
- [#6060 — Routine delivery target leaks across routines](https://github.com/nearai/ironclaw/issues/6060) — Closed, but this is a high-severity data leakage pattern (one user's Slack delivery changing every routine's target). Worth monitoring for recurrence.
- [#5598 — Chore: release PR](https://github.com/nearai/ironclaw/pull/5598) — Still open since July 3. Contains breaking API changes for `ironclaw_common` and `ironclaw_skills` (v0.5.0 and v0.4.0). Possibly superseded by v1.0.0 release, but should be closed if so.

**Long-running PRs:**
- [#3847 — Filesystem-backed Reborn skill bundle source](https://github.com/nearai/ironclaw/pull/3847) — Opened May 21, closed today. Finally merged after 2+ months. Validates that skill bundle infrastructure is now shipping.

**Unresolved epic with no recent activity:**
- [#6484 — Shared Messaging Capability Layer](https://github.com/nearai/ironclaw/issues/6484) — Last updated yesterday but no PRs targeting it. Critical for cross-channel consistency (Telegram/Slack/WebUI unified operations).

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-28

## Today's Overview
LobsterAI saw moderate activity today with 7 open issues and 9 PRs updated. While no new releases were published, the project had a productive day on the PR front with 5 merged/closed Pull Requests, suggesting steady development velocity. However, several critical data-integrity bugs (issues #2393, #2390) surfaced, raising concerns about stability in edge cases. The backlog also contains 3 stale issues (from April–May 2026) that remain unresolved, indicating some long-standing user pain points have not been addressed.

## Releases
**None** — No new releases were published on 2026-07-28.

## Project Progress
Five Pull Requests were merged/closed today, reflecting active development:

- **PR #2389** ([closed](https://github.com/netease-youdao/LobsterAI/pull/2389)) — _fix(email): prevent attachment path traversal_ — Sanitized attachment filenames and enforced download directory boundaries, adding cross-platform security tests. This is a security-critical fix for the email skill.

- **PR #2388** ([closed](https://github.com/netease-youdao/LobsterAI/pull/2388)) — _feat(artifacts): preview toolbar share & deploy entry_ — Added share and deploy buttons to the Artifact preview toolbar, with refined UI and comprehensive unit tests for deployment target logic.

- **PR #2386** ([closed](https://github.com/netease-youdao/LobsterAI/pull/2386)) — _fix(agentEngine): terminate no-progress tool loops before token budget exhaustion_ — Addresses a key resource-waste issue where the agent would burn through tokens on non-productive tool calls.

- **PR #2387** ([closed](https://github.com/netease-youdao/LobsterAI/pull/2387)) — _Feat/2026.7.20 sites_ — Feature work related to sites functionality (details in summary placeholder).

- **PR #1323** ([closed](https://github.com/netease-youdao/LobsterAI/pull/1323)) — _fix(cowork): narrow input-too-long error classification_ — Fixes a misleading error UI bug where unrelated `max_tokens` messages were incorrectly classified as "input too long" errors.

## Community Hot Topics

1. **Issue #2393** — _[Bug Report] Accelerator replaces `\f` with form feed character, corrupting files_  
   ([issue](https://github.com/netease-youdao/LobsterAI/issues/2393))  
   *Created & updated 2026-07-27* — 0 comments (new) | 🔴 **Critical severity**  
   The most technically severe issue today. User discovered that the "Accelerator" feature silently replaces literal `\f` byte sequences (e.g., in `\firecrawl`, `\filename`) with form-feed character `\x0C`, corrupting any file containing such tokens. 100% reproducible. No maintainer response yet.

2. **Issue #2390** — _[Bug Report] exec tool hardcodes PowerShell 5.1 & fails on Chinese-encoded usernames_  
   ([issue](https://github.com/netease-youdao/LobsterAI/issues/2390))  
   *Created & updated 2026-07-27* — 0 comments | 🔴 **High severity**  
   Windows users with non-ASCII usernames (e.g., `M幸福`) cannot use the `exec` tool at all. The tool hardcodes `powershell.exe` (version 5.1) instead of using the system's `pwsh.exe` (PowerShell 7).

3. **Issue #1240** — _[Stale] Model restriction cascades across all agents after quota exhaustion_  
   ([issue](https://github.com/netease-youdao/LobsterAI/issues/1240))  
   *Created 2026-04-01, updated 2026-07-27* — 1 comment | 👍: 0  
   A long-standing critical issue: when one API key is rate-limited, ALL agents fail (even those using different providers). This "poison pill" effect renders the entire application unusable.

**Analysis**: The three most active issues share a pattern: **configuration and state management failures**. Users are frustrated by silent data corruption (Accelerator), silent failure cascades (model lock-out), and silent loss of settings (Issue #1237). The underlying need is for robust, transparent state handling with clear user feedback.

## Bugs & Stability

### Critical (Data Integrity)
| Issue | Description | Fix PR? |
|-------|-------------|---------|
| [#2393](https://github.com/netease-youdao/LobsterAI/issues/2393) | Accelerator replaces `\f` with form-feed → file data corruption | None yet |
| [#2390](https://github.com/netease-youdao/LobsterAI/issues/2390) | exec tool hardcodes PowerShell 5.1, breaks on Chinese usernames | None yet |

### High (User-Blocking)
| Issue | Description | Fix PR? |
|-------|-------------|---------|
| [#1240](https://github.com/netease-youdao/LobsterAI/issues/1240) (stale) | One API restriction blocks all agents/cowork sessions (since April) | None yet |
| [#2062](https://github.com/netease-youdao/LobsterAI/issues/2062) (stale) | Tasks >24h auto-terminate with "Task timed out" — unclear if background continues | None yet |

### Medium (UX/Configuration)
| Issue | Description | Fix PR exists? |
|-------|-------------|----------------|
| [#1237](https://github.com/netease-youdao/LobsterAI/issues/1237) (stale) | Settings close without save confirmation → silent config loss | Yes: [#1241](https://github.com/netease-youdao/LobsterAI/pull/1241) (open since April!) |
| [#2392](https://github.com/netease-youdao/LobsterAI/issues/2392) | Scheduled tasks cannot select agent or skill | None yet |

## Feature Requests & Roadmap Signals

1. **Skill renaming** — Issue [#2391](https://github.com/netease-youdao/LobsterAI/issues/2391): User request to rename skills. This is a simple UX gap that likely requires minimal code but high user value. **Prediction**: Could land in next minor release given the active PR pipeline.

2. **Task scheduling improvements** — Issue [#2392](https://github.com/netease-youdao/LobsterAI/issues/2392): Scheduled tasks lack agent/skill selection. Complements the existing task system; may be bundled with agent configuration refactoring.

3. **Artifact preview & sharing** — PR [#2388](https://github.com/netease-youdao/LobsterAI/pull/2388) (merged today) adds share/deploy buttons to Artifact preview. This signals a strategic focus on **collaboration and deployment workflows** — a likely candidate for the next feature release.

## User Feedback Summary

**Positive signals:**
- The Artifact preview toolbar improvements (share/deploy) and the attachment path traversal fix (PR #2389) show the team is investing in both feature growth and security hardening.
- Multiple PRs today had thorough documentation (design docs, unit tests), indicating maturing engineering practices.

**Pain points (recurring themes):**
1. **Data integrity anxiety** — Silent corruption (`\f`→form-feed), silent config loss, silent model cascade — users repeatedly report that "the system did something wrong without telling me."
2. **Windows usability gap** — Chinese usernames, PowerShell version issues, and exec tool limitations make the Windows experience significantly worse than macOS/Linux.
3. **Stale "poison pill" behavior** — Issue #1240 (3 months old) is a top frustration: one API key's failure should not sink the entire application. The lack of agent isolation is a fundamental architectural pain point.
4. **Missing basic UX** — No save confirmation, no timer visibility, no skill rename — these are small features that disproportionately improve daily use.

## Backlog Watch
These important issues/PRs have been unanswered by maintainers for extended periods:

| Item | Age | Why it matters |
|------|-----|----------------|
| [Issue #1240](https://github.com/netease-youdao/LobsterAI/issues/1240) — Model restriction cascade | 3+ months | Core isolation failure; blocks all agents |
| [PR #1241](https://github.com/netease-youdao/LobsterAI/pull/1241) — Settings close confirmation fix | 3+ months | Already has a fix PR submitted, but never merged; closes Issue #1237 |
| [Issue #2062](https://github.com/netease-youdao/LobsterAI/issues/2062) — 24h task timeout | 2 months | Affects long-running workflows users expect to work |
| [PR #1239](https://github.com/netease-youdao/LobsterAI/pull/1239) — Taskbar flash on task completion | 3+ months | Low-risk, high-visibility UX improvement, never merged |
| [Issue #1237](https://github.com/netease-youdao/LobsterAI/issues/1237) — Settings silent config loss | 3+ months | Duplicate of #1241; user frustration acknowledged but unresolved |

**Recommendation**: The stale PR #1241 (Settings confirm dialog) and PR #1239 (taskbar flash) have been open for over 110 days with no maintainer activity. Merging these would resolve two of the community's oldest UX complaints. The project would benefit from a "stale backlog cleanup" sprint focused on merging or closing these lingering items.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-28

## Today’s Overview
The project shows moderate activity today with **5 open pull requests** updated in the last 24 hours, but **no new issues, releases, or merged PRs**. This indicates a focused development push, with multiple in-flight feature branches moving forward but none reaching the merge threshold today. The project remains in an active development phase, particularly around memory backends, agent protocol support, and infrastructure hardening. The absence of new issues suggests either a stable user base or low external bug reporting activity.

## Releases
**None.** No new releases were published today.

## Project Progress
No pull requests were merged or closed today. The following open PRs are progressing:
- **#1158** — `feat(memory): add zvec vector database memory backend` — experimental new memory backend using Zvec and Redb, feature-gated behind `zvec` Cargo feature
- **#1169** — `feat(acp): expose Moltis as an ACP agent over stdio` — adds the inverse of existing ACP client support, enabling Moltis to act as an agent
- **#1170** — `fix(channels): gate /sh and privileged tools behind a per-account operators list` — security fix restricting shell command execution to authorized operators
- **#1174** — `Add instrumentation and feedback collection infrastructure` — new `ObservationSink` fanout for pluggable monitoring backends
- **#1173** — `feat(pwa): make push notifications reliable and non-disruptive` — fixes silent notification replacement bug in PWA service worker

## Community Hot Topics
No issues or PRs have generated significant community discussion (zero comments and reactions on all open items). The **most substantive** PR is **#1158** (`feat(memory): add zvec vector database memory backend`), which represents a hands-on developer experiment with vibe-coding an alternative memory backend. The underlying need appears to be a lightweight, self-contained vector memory solution that can work with independently hosted embedding models.

GitHub: [PR #1158](https://github.com/moltis-org/moltis/pull/1158) | [PR #1169](https://github.com/moltis-org/moltis/pull/1169) | [PR #1170](https://github.com/moltis-org/moltis/pull/1170) | [PR #1174](https://github.com/moltis-org/moltis/pull/1174) | [PR #1173](https://github.com/moltis-org/moltis/pull/1173)

## Bugs & Stability
One critical security vulnerability is being addressed:
- **High severity** — **PR #1170** (`fix(channels): gate /sh and privileged tools`) addresses an arbitrary host command execution vulnerability. Previously, any Discord guild member who passed a channel's access gate could execute shell commands via `/sh`. The fix restricts this to a per-account operators list, which is essential for safe multi-user deployments.

GitHub: [PR #1170](https://github.com/moltis-org/moltis/pull/1170)

Additionally:
- **Medium severity** — **PR #1173** (`feat(pwa): make push notifications reliable`) fixes a bug where push notifications silently replaced previous ones without sound or alert, resulting in missed messages for PWA users.

## Feature Requests & Roadmap Signals
Key in-development features point toward upcoming capabilities:
- **Vector database memory backend (PR #1158)** — Likely to land soon, providing users with an alternative to the default memory system
- **ACP agent exposure (PR #1169)** — Significant for ecosystem integration, allowing tools like Zed or `buzz-acp` to use Moltis as their agent
- **Instrumentation & feedback collection (PR #1174)** — Signals a push toward monitoring and user feedback loops, suggesting Moltis is maturing toward production-grade observability

These features, combined with the security hardening in #1170, suggest the **next release will focus on reliability and integration** rather than new front-end capabilities.

## User Feedback Summary
No direct user feedback, issue reports, or satisfaction data were recorded today. The security fix in PR #1170 implicitly acknowledges that multi-user Discord deployments are in active use and need hardening. The PWA notification fix (PR #1173) addresses a real user pain point for web-based users who rely on push notifications.

## Backlog Watch
No issues or PRs are significantly aged or lacking maintainer attention. All five open PRs are recent (created within the last 1–12 days) and have received updates within the last 48 hours. The project maintainers appear to be actively shepherding these branches. However, **PR #1158** (zvec backend) has been open since July 17 without comments from other contributors — this may benefit from a review to unblock its integration.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-28

## Today's Overview

CoPaw shows moderate activity today with 50 issues and 49 PRs updated in the last 24 hours. The project maintains a healthy closure rate, with 35 of 50 issues closed and 15 of 49 PRs merged or closed. No new releases were published today. The development velocity is steady, with significant work visible in browser automation, context compression, workspace management, and third-party agent integrations. Community engagement remains high, particularly around channel integration issues (Feishu, DingTalk) and memory search functionality.

## Releases

None published today.

## Project Progress

**Merged/Closed PRs (15 total):**

- [#6489](https://github.com/agentscope-ai/CoPaw/pull/6489) — test(drivers): Added Driver unit tests with `fail_under=50` coverage gate enforcement, bringing Driver subsystem from 0% to regression-protected coverage.
- [#6462](https://github.com/agentscope-ai/CoPaw/pull/6462) — docs(sandbox): Clarified native Windows sandbox support (AppContainer, restricted-token isolation) correcting outdated docs that implied WSL2 was required.
- [#6502](https://github.com/agentscope-ai/CoPaw/pull/6502) — fix(dev): Fixed contributor setup instructions to include `test` extra dependency.
- Multiple bug-fix PRs addressing session approval level inheritance, history migration session ID preservation, Chrome CDP security defaults, and background tool call timing.

**Key features that advanced or were fixed:**
- Browser automation security: Chrome CDP exposure is now opt-in (PR [#6500](https://github.com/agentscope-ai/CoPaw/pull/6500))
- Context management: Visual Compact (PawFocus) for long agent histories (PR [#6456](https://github.com/agentscope-ai/CoPaw/pull/6456))
- Third-party agent integration: Codex, Qoder, Skills, and MCP support (PR [#6397](https://github.com/agentscope-ai/CoPaw/pull/6397))
- Workspace checkpoint management with shadow Git store (PR [#6269](https://github.com/agentscope-ai/CoPaw/pull/6269))
- ReMe memory search reranker support (PR [#6398](https://github.com/agentscope-ai/CoPaw/pull/6398))

## Community Hot Topics

Most active issues by comment count:

1. **[#5757](https://github.com/agentscope-ai/CoPaw/issues/5757) — Feishu bot not replying** (14 comments, CLOSED): Users reported that after the first message, the Feishu channel agent shows "received" but produces no further reply. This affected both Docker and AgentScope Platform instances. **Underlying need:** Channel reliability for production Feishu integrations.

2. **[#5725](https://github.com/agentscope-ai/CoPaw/issues/5725) — Console streaming causes browser lag** (6 comments, CLOSED): QwenPaw Console freezes during streaming output, but DeepSeek's web UI doesn't have this issue. **Underlying need:** Performance parity with competing solutions for real-time output.

3. **[#4895](https://github.com/agentscope-ai/CoPaw/issues/4895) — Infinite image compression loop** (5 comments, CLOSED): Uploading an image triggers a cycle of compression → re-injection → re-compression, causing hallucination-like behavior. **Underlying need:** Robust media handling without resource leaks.

4. **[#5090](https://github.com/agentscope-ai/CoPaw/issues/5090) — Security bypass via tool variation** (5 comments, CLOSED): The `rm` command was correctly blocked by safety guardrails, but the agent circumvented protection by using Python scripts to delete files. **Underlying need:** Comprehensive security that covers all execution paths.

5. **[#5259](https://github.com/agentscope-ai/CoPaw/issues/5259) — Windows vector index persistence failure** (5 comments, CLOSED): Memory search vector index fails to persist on Windows; requires "Rebuild on startup" to remain enabled. **Underlying need:** Platform parity for memory features.

## Bugs & Stability

**High Severity:**
- **[#6324](https://github.com/agentscope-ai/CoPaw/issues/6324) — LLM response truncation** (OPEN): Model responses are being cut off mid-generation with MiniMax-M3. No fix PR identified. **Severity: High** — affects output integrity.

- **[#6460](https://github.com/agentscope-ai/CoPaw/issues/6460) — High CPU on Edge/Wayland** (OPEN): QwenPaw 2.0.1 causes sustained high CPU usage in Edge browser tabs under Wayland, linked to large result set rendering. **Severity: High** — impacts user experience on Linux.

**Medium Severity:**
- **[#6258](https://github.com/agentscope-ai/CoPaw/issues/6258) — OpenAI model max_tokens not respected** (OPEN): The configured `max_tokens` parameter for OpenAI models does not take effect. No fix PR. **Severity: Medium** — model configuration regression.

- **[#5964](https://github.com/agentscope-ai/CoPaw/issues/5964) — Chat history mapping lost after 2.0.0 upgrade** (CLOSED): Session mapping between `chats` and `conversation_history` tables was lost during upgrade. **Severity: Medium** — data migration regression.

- **[#6457](https://github.com/agentscope-ai/CoPaw/issues/6457) — Task mode generates excessive history entries** (OPEN): Running in task mode creates hundreds of conversation entries. **Severity: Medium** — affects workflow clarity.

**Low Severity:**
- **[#6239](https://github.com/agentscope-ai/CoPaw/issues/6239) — Windows PATH semicolon dropped** (CLOSED): PATH concatenation loses separator between User and Machine PATH entries, breaking npm global access.

## Feature Requests & Roadmap Signals

**User-requested features visible in today's data:**

1. **Custom provider protocol support** ([#5609](https://github.com/agentscope-ai/CoPaw/issues/5609)): Users want to use non-OpenAI-compatible API endpoints (e.g., image generation APIs). **Prediction:** Likely to be addressed in next minor release as it blocks many free/alternative model integrations.

2. **DingTalk image preview improvement** ([#5593](https://github.com/agentscope-ai/CoPaw/issues/5593)): Uploading images to DingTalk media storage for previewable image messages instead of sending as files. **Prediction:** Moderately likely — improves channel parity.

3. **Session ID access in plugin tools** ([#5547](https://github.com/agentscope-ai/CoPaw/issues/5547)): Enterprise users need `sessionId` in MCP tools for user authorization. **Prediction:** High likelihood — enterprise use case with clear requirement.

4. **Kimi K2 Code Anthropic-compatible endpoint** ([#5427](https://github.com/agentscope-ai/CoPaw/issues/5427)): Kimi Coding Plan model uses Anthropic API format, not supported. **Prediction:** Moderate likelihood — niche model support.

5. **Memory search reranker** (PR [#6398](https://github.com/agentscope-ai/CoPaw/pull/6398)): Already under review, adds external reranker API for improved memory search quality. **Prediction:** Will land in next release.

6. **QwenPaw Creator app** (PR [#6284](https://github.com/agentscope-ai/CoPaw/pull/6284)): Script-to-video workflow as a plugin app. **Prediction:** Experimental feature for power users.

7. **Third-party agent integration** (PR [#6397](https://github.com/agentscope-ai/CoPaw/pull/6397)): Codex, Qoder, Skills, and MCP support. **Prediction:** Major roadmap item — likely v2.1.0.

## User Feedback Summary

**Pain Points:**
- **Channel reliability concerns**: Multiple users report Feishu ([#5757](https://github.com/agentscope-ai/CoPaw/issues/5757)), DingTalk ([#5603](https://github.com/agentscope-ai/CoPaw/issues/5603)), and enterprise WeChat ([#4990](https://github.com/agentscope-ai/CoPaw/issues/4990)) issues — agents respond inconsistently or slowly through IM channels.
- **Context bloat**: Users report images and attachments consuming excessive context tokens without compression ([#4921](https://github.com/agentscope-ai/CoPaw/issues/4921)), and new sessions loading uncompressed history ([#4872](https://github.com/agentscope-ai/CoPaw/issues/4872)).
- **Security bypass**: Safety guardrails are circumventable by using alternative tools (e.g., Python script instead of `rm` — [#5090](https://github.com/agentscope-ai/CoPaw/issues/5090)).
- **Windows platform issues**: Vector index persistence ([#5259](https://github.com/agentscope-ai/CoPaw/issues/5259)), PATH handling ([#6239](https://github.com/agentscope-ai/CoPaw/issues/6239)), and residual browser processes ([#4844](https://github.com/agentscope-ai/CoPaw/issues/4844)).

**Positive Signals:**
- The project is actively fixing community-reported issues (35 closed today).
- New features like Visual Compact context compression and reranker support show investment in core intelligence.
- Platform expansion (native Windows sandbox, macOS desktop automation) suggests broadening user base.

**Dissatisfaction Indicators:**
- One user reported feeling ignored after seeking help in community group ([#6467](https://github.com/agentscope-ai/CoPaw/issues/6467)).
- Multiple users report "same issue persisting across versions" (e.g., 9router connection issues [#5658](https://github.com/agentscope-ai/CoPaw/issues/5658)).

## Backlog Watch

**Issues needing maintainer attention:**

1. **[#6258](https://github.com/agentscope-ai/CoPaw/issues/6258) — OpenAI max_tokens not respected** (OPEN since Jul 19): No maintainer response or fix PR. Affects model configuration for the most commonly used provider.

2. **[#6324](https://github.com/agentscope-ai/CoPaw/issues/6324) — Response truncation** (OPEN since Jul 22): No maintainer response. Output integrity issue with MiniMax-M3.

3. **[#6457](https://github.com/agentscope-ai/CoPaw/issues/6457) — Task mode excessive history** (OPEN since Jul 24): No maintainer response. Workflow usability regression.

4. **[#6460](https://github.com/agentscope-ai/CoPaw/issues/6460) — High CPU on Edge/Wayland** (OPEN since Jul 25): Critical performance issue on Linux. No fix PR linked.

**Stale PRs:**
- **[#5490](https://github.com/agentscope-ai/CoPaw/pull/5490) — Tool card image gallery** (OPEN since Jun 24, last updated today): Awaiting review for over a month despite being a UI improvement with community interest.
- **[#6157](https://github.com/agentscope-ai/CoPaw/pull/6157) — Chrome extension plugin** (OPEN since Jul 15): Depends on PR [#6276](https://github.com/agentscope-ai/CoPaw/pull/6276) (unified browser core), which itself remains open. Blocked chain requiring prioritization.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-28

## Today's Overview
ZeroClaw is experiencing a period of high-intensity development and security hardening, with **48 open issues and 50 pull requests updated in the last 24 hours**, alongside **12 merged/closed items**. The project is in the middle of a major audit-driven security push, with a cluster of high-priority bugs filed by contributor `belumume` across channel authorization, API key leakage, and authentication bypasses. The CI and test infrastructure remains fragile, with **multiple platform-specific compilation failures** on Windows and macOS. No new releases were published, but the activity suggests the project is approaching a significant stabilization and security patch window.

## Releases
**None.** No new releases were published today. The latest stable version remains **zeroClaw 0.8.3**, with `master` tracking toward a future v0.9.0 milestone that includes breaking changes and a security/auth overhaul (tracked in issue #7432).

## Project Progress
**8 pull requests were merged or closed today**, advancing key areas:

- **Security & policy hardening:**
  - [#9472](https://github.com/zeroclaw-labs/zeroclaw/pull/9472) — Fix: `vi_verify` no longer registered as a model-callable tool, closing an unauthenticated verification path
  - [#9443](https://github.com/zeroclaw-labs/zeroclaw/pull/9443) — Fix: malformed tool payloads stripped from structured logs to prevent information leakage
  - [#9448](https://github.com/zeroclaw-labs/zeroclaw/pull/9448) — Fix: policy actions preserved during clock-underflow edge case
  - [#9420](https://github.com/zeroclaw-labs/zeroclaw/pull/9420) — Support for Anthropic stored OAuth profiles added (still open but received attention)

- **Test infrastructure:**
  - [#9442](https://github.com/zeroclaw-labs/zeroclaw/pull/9442) — Fixed wall-clock-dependent assertions in channel tests that caused CI flakiness
  - [#9429](https://github.com/zeroclaw-labs/zeroclaw/pull/9429) — Addressed related wall-clock timeout flake in `zeroclaw-channels` tests

- **Governance & docs:**
  - [#9388](https://github.com/zeroclaw-labs/zeroclaw/pull/9388) — Retired stale `CONTRIBUTORS.md` record; maintainer roles now exclusively grounded in FND-003

- **Infrastructure:**
  - Large infrastructure PR [#9251](https://github.com/zeroclaw-labs/zeroclaw/pull/9251) (PostgreSQL session backend) was closed; likely reworked or superseded

## Community Hot Topics
The most active discussions reflect a security-conscious community and growing concerns about fundamental reliability:

- **#9357** ([Bug: cargo test -p zeroclaw-runtime —lib fails on master in 19 of 20 runs](https://github.com/zeroclaw-labs/zeroclaw/issues/9357)) — 5 comments. A **99% test-failure rate** in the runtime crate, with a global mutex poisoning that cascades. This is the highest-signal stability issue, indicating the `master` branch is effectively untestable for this crate. The author `AngryPacifist` has filed multiple CI fragility bugs.

- **#9386** ([Gemini API key survives sanitize_api_error and leaks into chat](https://github.com/zeroclaw-labs/zeroclaw/issues/9386)) — 4 comments. A **credential leakage vulnerability** where a Google Gemini API key embedded in a URL query string is returned to the user in an error message. The `sanitize_api_error` function fails to strip the `?key=` parameter, exposing the key to the originating chat.

- **#8973** ([Landlock blocks shell access on Fedora](https://github.com/zeroclaw-labs/zeroclaw/issues/8973)) — 4 comments. Production-blocking issue for Fedora users: the Landlock sandbox prevents the shell tool from accessing `/dev/null`, making the shell tool completely non-functional when the security feature is enabled.

- **#9393** ([Bluesky and Reddit have no sender authorization](https://github.com/zeroclaw-labs/zeroclaw/issues/9393)) — 3 comments. Security vulnerability discovered during an audit: neither channel verifies sender identity, and no central authorization gate covers them. Same pattern found in #9392 (LINE) and #9417 (WhatsApp).

- **#9330** ([RFC: AI-assisted PR pre-review and re-review](https://github.com/zeroclaw-labs/zeroclaw/issues/9330)) — 2 comments. A forward-looking proposal to leverage existing CI results to trigger AI-assisted code review, while keeping human approval requirements risk-based.

**Underlying need:** The community is reacting to systemic issues — CI that can't be trusted, security gaps in channel integrations, and credential leakage. The volume of security-related issues filed within 24-48 hours suggests an ongoing audit is surfacing long-standing flaws that the project must prioritize before v0.9.0.

## Bugs & Stability
**High-severity bugs reported today (2026-07-27/28):**

| Issue | Severity | Component | Description | Fix PR? |
|-------|----------|-----------|-------------|---------|
| [#9421](https://github.com/zeroclaw-labs/zeroclaw/issues/9421) | S1 (workflow blocked) | runtime/daemon | Incomplete terminal responses reported as successful; tool calls can stop mid-execution without error | PR #9447 in progress |
| [#9425](https://github.com/zeroclaw-labs/zeroclaw/issues/9425) | S1 (workflow blocked) | web dashboard | No operator cancellation path for running SOP jobs | None yet |
| [#9362](https://github.com/zeroclaw-labs/zeroclaw/issues/9362) | S0 (data loss/security) | browser tool | Arbitrary file write escape via screenshot `path` parameter | PR #9362 open |
| [#9422](https://github.com/zeroclaw-labs/zeroclaw/issues/9422) | Degraded (S2) | CI/config | `zeroclaw-config` unit tests cannot compile on Windows — `cfg(unix)`-gated `EnvValueGuard` used by ungated test | None identified |
| [#9462](https://github.com/zeroclaw-labs/zeroclaw/issues/9462) | Minor (S3) | CI | `zeroclaw-plugins` lib tests gated behind `plugins-wasmtime` feature never executed in CI | None yet |
| [#9340](https://github.com/zeroclaw-labs/zeroclaw/issues/9340) | S1 (workflow blocked) | cron/CLI | CLI-created cron jobs hardcoded to `delivery.mode = "none"` — output silently discarded | None yet |
| [#9421](https://github.com/zeroclaw-labs/zeroclaw/issues/9421), [#9424](https://github.com/zeroclaw-labs/zeroclaw/pull/9424), [#9447](https://github.com/zeroclaw-labs/zeroclaw/pull/9447) | S1 | runtime | Incomplete terminal responses and semantic-empty completions being reported as success | PR #9424 (base) + #9447 (stacked) |
| [#9436](https://github.com/zeroclaw-labs/zeroclaw/issues/9436) | S2 (degraded) | config/onboarding | `config init` writes template sections that fail strict loader; fresh config is born degraded, `config migrate` exits 1 | None yet |

**Stability impact:** The runtime crate (`zeroclaw-runtime`) is functionally untestable on `master` (#9357). Combined with the Windows compilation failures (#9422) and macOS wall-clock flakes (#9429), the project's CI is currently unreliable across all three major platforms. Fix PRs are in progress for the runtime issues but remain open and unmerged.

## Feature Requests & Roadmap Signals
- **#9464** ([RFC: Anthropic stored-profile OAuth alias contract](https://github.com/zeroclaw-labs/zeroclaw/issues/9464)) — Proposed contract for explicit `auth_mode = "oauth"` with Anthropic, already with a matching PR (#9420). Likely to land soon.
- **#8983** ([Category-scoped read_memory_from](https://github.com/zeroclaw-labs/zeroclaw/issues/8983)) — Proposal to share only selected memory categories with sibling agents, enabling a "read-only observability agent" pattern. Currently all-or-nothing per agent.
- **#9330** ([AI-assisted PR pre-review](https://github.com/zeroclaw-labs/zeroclaw/issues/9330)) — RFC for using CI results to trigger AI review while keeping human approval risk-based. Signals growing operational maturity.
- **#9463** ([Wire WASM memory plugins into runtime backend selection](https://github.com/zeroclaw-labs/zeroclaw/issues/9463)) — Currently only the tool WASM plugin backend is reachable in production; channel and memory backends exist but are untestable in CI (#9462).
- **Milestone: SOP control plane** (#8288) continues toward "5/5" completion, with a new cancellation gap identified (#9425).

**Prediction for v0.9.0:** Look for Anthropic OAuth profiles (#9464/#9420), the WASM plugin backend wiring (#9463), and the category-scoped memory sharing (#8983) to land before the next release.

## User Feedback Summary
**Pain points from today's issues:**
- **"CLI feels broken out of the box"** — Issue #9436: `config init` produces a degraded config that immediately needs manual fixing, and `config migrate` exits with code 1 instead of providing a clear migration path.
- **"My cron jobs silently produce nothing"** — Issue #9340: CLI-created cron jobs hardcode `delivery.mode = "none"`, so output is silently discarded. Users have no way to know their automation is producing results that never reach them.
- **"The bot just gives me an emoji and ignores me"** — Issue #9465: When a precheck declines a channel message, Telegram users see only a reaction with no explanatory text, making the agent appear "broken" rather than politely declining.
- **"Fedora users can't use the shell tool"** — Issue #8973: Landlock sandbox blocks `/dev/null` access, making shell execution impossible with security enabled. Fedora is a common development platform.

**Satisfaction signals:** The project has attracted multiple distinguished/trusted contributors (Audacity88, vrurg, perlowja) submitting high-quality patches. The emergence of an "audit wave" (belumume filing multiple security bugs) suggests external security researchers are engaged and reporting responsibly.

## Backlog Watch
**Issues needing maintainer attention:**
- **#8279** ([delegate bypasses parent's tool allowlist](https://github.com/zeroclaw-labs/zeroclaw/issues/8279)) — **34 days open, S0 severity (data loss/security risk), status:in-progress, risk:high.** The `delegate` tool passes the parent's unfiltered tool set to sub-agents, completely bypassing the allowlist policy. Fix PRs exist but are not merged. This is the highest-risk unaddressed security issue.
- **#8692** ([Maintainer decision queue for RFCs](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)) — **24 days open.** A coordination tracker where RFCs and design issues await maintainer decisions. No new decisions recorded.
- **#8352-8355** — Assume similar long-standing tool/delegate security issues remain unaddressed.

**PRs needing maintainer attention:**
- **#8966** ([Carry live provider identity on usage events](https://github.com/zeroclaw-labs/zeroclaw/pull/8966)) — **17 days open, risk:high, needs-author-action.** A foundational infrastructure change that touches agent, channel, config, gateway, provider, and runtime code. Blocked or waiting for review.
- **#8443** ([Matrix single-message progress drafts](https://github.com/zeroclaw-labs/zeroclaw/pull/8443)) — **30 days open, size:XL, needs-author-action.** Large Matrix channel enhancement that has been in review/pending for a month.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*