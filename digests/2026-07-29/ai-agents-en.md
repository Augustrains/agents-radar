# OpenClaw Ecosystem Digest 2026-07-29

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-29 01:19 UTC

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

# OpenClaw Project Digest — 2026-07-29

## Today's Overview

OpenClaw shows intense community engagement with 500 issues and 500 PRs updated in the last 24 hours, reflecting a highly active project in mid-beta development. With 231 open issues, 234 open PRs, and a new beta release (v2026.7.2-beta.5), the project is in a sustained phase of rapid iteration. The 266 merged/closed PRs against 234 open suggest a healthy cadence of fixes landing, though the volume of open items (especially P0/P1 bugs) indicates significant ongoing reliability work. Community attention remains concentrated on cross-platform desktop support, memory/state safety, and session stability.

## Releases

### v2026.7.2-beta.5 — 2026-07-28

This release focuses on **state safety and data recovery**, a critical area given recent session-corruption and data-loss reports:

- **Quarantine store** — Protects persisted data when the primary database is damaged, preventing cascading failures
- **Crash-recoverable SQLite snapshots** — Enables safe recovery after process crashes
- **Crash-durable filesystem publication** — Ensures file writes survive abrupt termination
- **Schema-upgrade data-loss rejection** — Blocks migrations that would destroy data, preventing silent corruption
- **Rollback-writer snapshot recovery** — Allows safe reversion after failed writes

**No breaking changes or migration notes were included.** This release directly addresses the class of crash-loop and session-corruption bugs seen in Issues #91588, #113434, and #78562.

---

## Project Progress — Merged/Closed PRs (266 total today)

### Stability & Infrastructure
- **[#115460]** — `refactor(code-mode): unify safe OpenAI tool filtering` — Standardizes tool-declaration parsing across streaming and non-streaming paths, reducing inconsistency risk
- **[#115459]** — `refactor(code-mode): prepare MCP namespaces once per run` — Eliminates redundant namespace builds, improves performance, prevents inherited-object-property exploits in untrusted MCP schemas
- **[#115467]** — `fix(ollama): preserve selected model capabilities during onboarding` — Prevents loss of vision/thinking support when models appear late in catalog enumeration

### Platform Compatibility
- **[#115453]** *(open)* — `fix(whatsapp): resolve WA Web version from web.whatsapp.com` — Prevents 405 handshake rejections by fetching live WhatsApp Web versions instead of relying solely on pinned Baileys lists

### Tooling & Config
- **[#105402]** *(closed)* — `fix(config): respect agent directory filesystem case` — Fixes false collision detection on case-sensitive volumes (macOS, Windows)
- **[#115461]** *(closed)* — `refactor(chat): remove duplicate session projection paths` — Eliminates inconsistency between browser and terminal session views

---

## Community Hot Topics

### Most Active Issues by Comments

| Issue | Comments | Description |
|-------|----------|-------------|
| [#75 — Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 115 💬 👍80 | **Longest-running community request.** Users want parity with macOS/iOS/Android desktop apps. High engagement over 7 months suggests this is the #1 community expectation. |
| [#7707 — Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707) | 22 💬 | Requests memory-poisoning prevention by tagging entries with source trust level—a security/UX crossover issue |
| [#91588 — Gateway Memory Leak — RSS grows 350MB→15.5GB](https://github.com/openclaw/openclaw/issues/91588) | 20 💬 | **P0 crash-loop bug.** Process OOM-killed after 2-3 days. Affects all Gateway users. No fix PR linked. |
| [#96857 — Text outputs degrade to “(see attached image)”](https://github.com/openclaw/openclaw/issues/96857) | 15 💬 (closed) | Tool text outputs replaced with image placeholders, making agent blind to command output — UX-critical regression |
| [#10659 — Masked Secrets System](https://github.com/openclaw/openclaw/issues/10659) | 14 💬 | API key protection against prompt injection — mirrors #7707's security theme |

### Underlying Community Needs

Across the top issues, three patterns emerge:
1. **Cross-platform desktop parity** — The #75 megathread (115 comments) shows significant demand for Windows/Linux native clients matching macOS/iOS capabilities
2. **Security-by-design** — Multiple issues (#7707, #10659, #7722) independently propose sandboxing, secret masking, and filesystem access controls, indicating community awareness of prompt-injection and data-leakage vectors
3. **Memory management anxiety** — The P0 memory leak (#91588) and repeated compaction/overflow issues (#78562, #98790) show users are hitting hard limits in real-world use

---

## Bugs & Stability

### Critical (P0) — Active, No Fix PR

| Issue | Summary | Impact |
|-------|---------|--------|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | **Gateway memory leak**: RSS 350MB→15.5GB in 2-3 days → OOM crash → `launchd-handoff` restart cycles | Crashes entire Gateway; all channels affected |

### High Severity (P1) — Active

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#115326](https://github.com/openclaw/openclaw/issues/115326) | Crash-loop breaker permanently suppresses Discord/WhatsApp; `channels.start` fails with WebSocket 1006 | No |
| [#114137](https://github.com/openclaw/openclaw/issues/114137) | Visible channel turns dispatch with no reply payloads—text persisted in transcript, never delivered | No |
| [#113434](https://github.com/openclaw/openclaw/issues/113434) | Codex `sessions.reset` reuses retired session ID; RAM exhaustion crash on catalog scans | No |
| [#102268](https://github.com/openclaw/openclaw/issues/102268) | Silent empty tool results in Sonnet 5 sessions after large tool results—persisted but invisible to agent | No |
| [#98435](https://github.com/openclaw/openclaw/issues/98435) | MCP loopback transport fails to auto-reconnect after gateway restart — `recovered=1` is misleading | No |

### Regressions Reported Today

| Issue | Version | Summary |
|-------|---------|---------|
| [#115326](https://github.com/openclaw/openclaw/issues/115326) | 2026.7.x | Discord/WhatsApp permanently suppressed (crash-loop breaker) |
| [#115001](https://github.com/openclaw/openclaw/issues/115001) | 2026.7.x | Hybrid memory search returns spurious 1.0 similarity scores via FTS `LIKE`-fallback |

### Recently Closed/Resolved
- **[#108075](https://github.com/openclaw/openclaw/issues/108075)** — LLM request schema rejection (2026.7.1 regression) — **Closed**
- **[#96857](https://github.com/openclaw/openclaw/issues/96857)** — Text→image placeholder degradation — **Closed**
- **[#111519](https://github.com/openclaw/openclaw/issues/111519)** — Telegram DM reply fallback (2026.7.2-beta.3 regression) — **Closed**

---

## Feature Requests & Roadmap Signals

### High-Community-Interest Requests

| Issue | Request | Votes | Likely Next Version? |
|-------|---------|-------|---------------------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows desktop apps | 👍80 | Unlikely in next beta (requires native UI work) |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked secrets for API key protection | 👍4 | Possible — aligns with security focus in v2026.7.2-beta.5 |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | Memory trust tagging by source | 👍0 | Possible — complements quarantine store pattern |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) | Denylist support for exec-approvals | 👍8 | Likely — complements existing allowlist |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) | Filesystem sandboxing config | 👍4 | Possible — part of broader security hardening |

### Predicted for v2026.7.x Stable
- **Security layer enhancements** — Given the v2026.7.2-beta.5 emphasis on data safety, expect proposals for secret masking (#10659) and filesystem sandboxing (#7722) to advance
- **Memory leak fix** — #91588 is P0 and generating user pressure; a fix PR should appear soon
- **Session stability improvements** — The compaction/overflow issues (#78562, #98790, #100982) are long-standing and likely targeted

---

## User Feedback Summary

### Pain Points
1. **Memory leaks degrading reliability** — Users report the Gateway becoming unusable after 2-3 days (#91588), forcing manual restarts
2. **Session transcript corruption** — Multiple reports of sessions being silently reset (#106403), overwritten (#77012), or permanently poisoned (#98790)
3. **Missing desktop clients** — The #75 thread (115 comments) expresses sustained demand; users are running workarounds with Telegram/CLI but want native apps
4. **Crash-recovery documentation fails** — The documented `channels.start` recovery path doesn't work (WebSocket 1006), leaving users without recourse (#115326)

### Satisfaction Signals
- **Positive sentiment** in #73537 ("genuinely become part of our daily workflow") and #75 ("thank you for OpenClaw")
- **Engagement is high** — 500 issues and 500 PRs updated in 24h suggests active, invested community
- **Beta being tested in production** — Users like petercheng, robingutsche, and EthanSK are running preview builds in real environments, indicating trust in the project's direction

### Use Cases Mentioned
- Family/business assistant with Telegram integration, automations, cron jobs, Home Assistant control (#73537)
- Multi-agent setups with inter-agent traffic (#98790, #8299)
- Code mode for development workflows
- Azure Foundry/OpenAI deployments for enterprise users (#87325)

---

## Backlog Watch — Items Needing Maintainer Attention

### Long-Unanswered / Stalled

| Issue | Days Open | Priority | Why Stalled |
|-------|-----------|----------|-------------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | 209 | P2 | Cross-platform desktop apps — large scope, no maintainer commitment |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | 176 | P2 | Needs security review + product decision |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | 172 | P1 | Needs security review + product decision |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) | 176 | P2 | Needs security review + product decision |
| [#8299](https://github.com/openclaw/openclaw/issues/8299) | 176 | P2 | Needs product decision — sub-agent announce suppression |
| [#9986](https://github.com/openclaw/openclaw/issues/9986) | 173 | P2 | Context-exceeded fallback — long-standing gap |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) | 172 | P2 | Dynamic model discovery — tagged `maintainer` but no action |

All stalled items carry the `clawsweeper:needs-product-decision` or `clawsweeper:needs-maintainer-review` labels. The consistent pattern is **security-review bottleneck** and **product-decision queue** — six of eight stalled items require one or both.

### PRs Awaiting Maintainer Review
- **[#97175](https://github.com/openclaw/openclaw/pull/97175)** — P1 fix: context-engine deferred turn maintenance timeout — ⏳ waiting on author
- **[#89040](https://github.com/openclaw/openclaw/pull/89040)** — P1 fix: event-loop stalls during `embedded_run` bootstrap — ⏳ waiting on author
- **[#115275](https://github.com/openclaw/openclaw/pull/115275)** — P1 fix: prevent invalid Code Mode exec calls on small models — needs review
- **[#114598](https://github.com/openclaw/openclaw/pull/114598)** — P1 fix: slide run budget deadline on progress activity — 📣 needs proof

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report.

---

### Cross-Project Comparison Report: Personal AI Assistant Ecosystem
**Date:** 2026-07-29

### 1. Ecosystem Overview
The open-source personal AI agent ecosystem is in a phase of rapid, high-velocity iteration, driven by a collective push toward production reliability, security hardening, and multi-platform interoperability. Projects are moving beyond basic chat capabilities to address enterprise-grade concerns: data persistence, state management, secret handling, and deterministic error recovery. A clear divergence is emerging between "thick" monolithic reference implementations (OpenClaw, IronClaw) and "thin" modular frameworks (NanoBot, ZeroClaw), each targeting different developer personas and deployment scales. Community engagement is exceptionally high, with several projects processing hundreds of issues and pull requests daily, signaling a vibrant and invested user base that is actively shaping roadmaps.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status | Health Score | Notes |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | v2026.7.2-beta.5 | Moderate (High activity, P0 bugs open) | Sustained rapid iteration; reliability work |
| **Hermes Agent** | 50 | 50 | No new release | Good | Steady, balanced merge cadence |
| **IronClaw** | 50 | 50 | No new release (1.0.0) | Good | Major feature push, epics closing |
| **CoPaw** | 18 | 50 | No new release (2.1.0b1) | Good | Very high contribution velocity |
| **NanoBot** | 7 | 37 | No new release | Good | Focused on hardening and CI |
| **ZeroClaw** | 49 | 50 | No new release | Moderate | Intense activity, high-risk item load |
| **LobsterAI** | 5 | 6 | No new release | Moderate | Windows-focused stability sprint |
| **Moltis** | 1 | 8 | No new release | Excellent | Clean backlog, proactive security |
| **PicoClaw** | 4 | 10 | No new release | Moderate | Maintainer bandwidth constrained |
| **NanoClaw** | 0 | 11 | No new release | Good | Focused bug-fix sprint |
| **ZeptoClaw** | 0 | 2 | Unknown | Sleepy | Only automated dependency bumps |
| **TinyClaw** | 0 | 0 | Unknown | No Activity | No data |
| **NullClaw** | 0 | 0 | Unknown | No Activity | No data |

### 3. OpenClaw's Position
**Advantages:** OpenClaw boasts the largest community by a wide margin, with over 500 daily issue/PR updates, representing an order of magnitude more engagement than its next-closest peer (IronClaw at 50). This scale provides unparalleled community feedback, a vast library of bug reports, and a large contributor base. Its recent beta release (v2026.7.2-beta.5) with a focus on state safety and data recovery is a direct response to critical crash-loop bugs, demonstrating a responsive maintainer team.

**Technical Approach:** OpenClaw functions as a "thick reference" monolith—a single, comprehensive codebase for a full-featured agent. This contrasts with the "thin" architectural experiments of ZeroClaw (moving to WASM runtime plugins) and the more modular, embeddable platforms like CoPaw and Moltis.

**Community Size:** OpenClaw's community is the largest in the ecosystem. While this drives innovation and rapid bug discovery, it also generates a significant volume of open issues (231) and PRs (234), creating a substantial maintenance burden and a more chaotic development environment than smaller, more curated projects.

### 4. Shared Technical Focus Areas
Several critical requirements are emerging independently across multiple projects, signaling fundamental industry needs:

- **Security & Secret Management:**
    - *OpenClaw:* Masked Secrets (#10659), Memory Trust Tagging (#7707)
    - *IronClaw:* Permissions fix for MCP auth failures (#6835)
    - *ZeroClaw:* `KeySource` trait RFC (#9127), credential migration fixes
    - *Hermes Agent:* Fixed command injection risk via `shell=True`
    - *Moltis:* Closed access control gap for privileged tools (#1170)
- **Memory & State Safety:**
    - *OpenClaw:* Crash-recoverable snapshots, quarantine store for data corruption
    - *NanoBot:* Session consolidation drops media paths (#5118), LLM finish reason misfouting
    - *CoPaw:* Agent/Sub-Agent isolation to prevent memory leaks between contexts (#6461)
    - *ZeroClaw:* Config flush overwrites concurrent writes (#9284)
- **Multi-Agent / Interoperability:**
    - *NanoBot:* Multi-Agent Collaboration Proposal (#5000)
    - *Moltis:* ACP agent exposure over stdio (#1169)
    - *CoPaw:* Sub-Agent isolation to prevent data sharing between bots (#6509)
    - *Hermes Agent:* Buzz messaging integration for team workflows (#68871)
- **Reliability & Error Recovery:**
    - *OpenClaw:* P0 memory leak (#91588), session corruption fixes
    - *IronClaw:* Error-recoverability epic (#6284) with five explicit sub-conditions
    - *ZeroClaw:* Signal/voice call crashloop fix (#6724), flaky test mutex poisoning
    - *CoPaw:* MCP reconnection failure (#6524)

### 5. Differentiation Analysis

| Feature Area | Project Focus | Target User |
|---|---|---|
| **Thick Monolith** | OpenClaw, IronClaw | Full-featured, deploy-and-forget for enthusiasts and small teams |
| **Modular / Embeddable** | NanoBot, ZeptoClaw | Developers who want to integrate a chat engine into their own app |
| **Enterprise/Infrastructure** | ZeroClaw (WASM plugins, KeySource trait) | Ops teams needing a secure, extensible platform |
| **Multi-Agent Orchestration** | Moltis (ACP), Hermes Agent (Buzz) | Users building collaborative agent networks |
| **Platform-Specific Use** | LobsterAI (Windows), CoPaw (Multi-platform, Chinese ecosystem) | Users in specific OS/regional ecosystems |
| **Edge / Embedded** | PicoClaw, NanoClaw, TinyClaw | Resource-constrained or single-purpose deployments |

### 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating (High Risk/High Stability)**
- **OpenClaw:** The highest velocity, but also the highest number of open bugs and regressions (P0 memory leak, crash-loop bugs). It is both the most feature-rich and the most chaotic.
- **IronClaw:** A well-organized, major feature push (Hermetic testing, error-recoverability). High maturity with a structured epic-based development model.

**Tier 2: High Velocity, Stabilizing**
- **ZeroClaw:** Very high activity with a clear architectural vision (plugins-first). Has a structured risk and maintainer-decision backlog, indicating self-awareness of its own scaling challenges.
- **CoPaw:** Very high community contribution rate. Community is actively pushing for security and isolation features, a sign of maturing use cases.

**Tier 3: Clean Linear Progress**
- **Hermes Agent:** Healthy, balanced PR cadence with strong maintainer oversight consolidating contributor work. Fewer regressions, but slower feature velocity.
- **NanoBot:** Focused, high-quality bug fixes. The project is in a hardening phase.
- **Moltis:** Excellent health with no open bugs and proactive security fixes. A model for lean, disciplined development.

**Tier 4: Maintenance/Low Activity**
- **LobsterAI:** Windows-focused stability work. Moderate activity with a clear niche.
- **PicoClaw:** Active but maintainer-constrained, with several long-open PRs.
- **NanoClaw:** Occasional bug-fix sprints.
- **ZeptoClaw:** Dormant, only automated dependency updates.

### 7. Trend Signals
Key industry trends extracted from community feedback, offering value for AI agent developers:

1.  **From "Chatbot" to "Multi-Tenant Agent Platform":** The highest-voted and most-discussed issues across projects (CoPaw’s Agent Isolation, OpenClaw’s missed Linux/Windows apps) show users are no longer building single-purpose assistants. They are deploying agents in multi-context, multi-user production environments where data isolation and access control are non-negotiable.

2.  **Security is the Next UX Battlefield:** The simultaneous emergence of `KeySource` traits (ZeroClaw), masked secrets (OpenClaw), and access control fixes (Moltis, IronClaw) signals that naive API-key-in-a-text-file management is a dead end. The ecosystem is rushing to standardize secret storage, credential rotation, and prompt-injection defense.

3.  **The Push for Deterministic Reliability:** The high engagement on IronClaw’s error-recoverability contract and the systematic approach to memory/state safety (OpenClaw’s quarantine store, NanoBot’s session consolidation fixes) demonstrates a market demand for agents that don't silently fail or lose state. "Fail open" is no longer acceptable; "recover automatically" is becoming table stakes.

4.  **Interoperability is the New Platform Lock-in:** The flurry of activity around ACP (Moltis), Buzz (Hermes Agent), and multi-agent proposals (NanoBot, CoPaw) suggests that the next major differentiator won't be a single agent's intelligence, but its ability to cooperate with other agents and human tools. The winning platform will be the one that best integrates into a broader ecosystem, not the one that tries to replace it.

5.  **The Rise of the Thick Client's Nightmare:** The core challenge for monoliths like OpenClaw (500 daily updates) is a scaling problem. The volume of data itself becomes a liability. The maintenance burden of a single, massive codebase may prove unsustainable compared to more modular, plugin-based architectures. The industry trend is towards **architectural modularity** (ZeroClaw’s WASM plugins, Moltis’s ACP) to escape the monolith's inherent complexity.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for 2026-07-29.

---

## NanoBot Project Digest
**Date:** 2026-07-29
**Source:** github.com/HKUDS/nanobot

### 1. Today's Overview
The NanoBot project is experiencing a period of **very high activity**, driven primarily by the core team. While there are no new releases, **37 pull requests were updated in the last 24 hours**, with 18 merged or closed, indicating a significant push to resolve bugs and land features. Concurrently, 7 issues were updated, with the quality of bug reports being notably high—often including root cause analysis. The overall project health appears strong, with a clear focus on hardening the codebase against edge cases and improving the developer and user experience through extensive testing.

### 2. Releases
**None.** No new versions of NanoBot were released today.

### 3. Project Progress
Today saw 18 PRs merged/closed, focusing on stability, CI, and user interface polish.
- **CI/CD Stability (#5145, #5144):** Two PRs were merged to stabilize the CI pipeline. This involved replacing a timing-dependent test with a more reliable handshake and fixing a bug where concurrent base-branch updates could cause incorrect path detection in PR scoping.
- **WebUI Polish (#5142, #5143):** The user interface received attention with a fix for thread navigation (opening to the latest message) and smoother animations for the reasoning/tool activity drawer.
- **Diagnostics & Recovery (#5110):** A significant feature was merged to add actionable startup diagnostics. The `nanobot status` command now performs offline checks for environment variables, model resolution, and provider setup, and provides redacted field-level errors for malformed configuration files.

### 4. Community Hot Topics
The community discussion is currently focused on the architecture and future evolution of the agent system.
- **Issue #5000: Multi-Agent Collaboration Proposal** (5 comments)
  - *Link:* HKUDS/nanobot Issue #5000
  - *Analysis:* This is the most structurally significant proposal. It argues the current "subagent" system is too simple (task delegation) and suggests moving toward persistent agents with shared state. This signals a user desire for more complex, collaborative workflows.

### 5. Bugs & Stability
A significant number of bugs were reported and fixed today, with a focus on data integrity and edge-case handling. **Severity is ranked High (data loss) to Medium (UI/UX).**

- **[HIGH] Session Consolidation Drops Media Paths (Issue #5118, PR #5120, #5139):**
    - *Issue:* When a session is archived, the absolute file path for uploaded media (e.g., images) is dropped if it’s stored in the `media[]` field but not in the message text. This makes the file unrecoverable after archiving.
    - *Status:* Two fix PRs are open (#5120, #5139) to resolve this critical data-loss bug.
- **[HIGH] LLM Finish Reason Misfouting (Issue #5133):**
    - *Issue:* When an LLM response finishes due to a length limit but also contains tool calls, the system incorrectly treats it as an empty response instead of triggering a length-recovery strategy.
    - *Status:* Report is open with no linked fix PR yet.
- **[MEDIUM] Null `approved` Map Crashes Pairing (PR #5155):**
    - *Fix:* Merged a patch to handle a `null` value for the `approved` map in pairing store, preventing a crash when checking a channel's approval status.
- **[MEDIUM] Non-Standard Timestamps Crash Memory Archiving (PR #5153):**
    - *Fix:* Merged a patch to handle non-string timestamps or missing `role` fields in archived messages, preventing a crash during session history consolidation.
- **[MEDIUM] Exec Session Output Unbounded (PR #5150):**
    - *Fix:* Merged a fix to bound the output buffer for executed commands, preventing potential memory issues from runaway output.
- **[LOW] WebUI Token Usage Page Crashes (PR #5146):**
    - *Fix:* Merged a fix to handle malformed day keys in token usage data, which would otherwise crash the entire settings page.

### 6. Feature Requests & Roadmap Signals
The development trajectory is clear: **hardening the existing system** is the priority.
- **The multi-agent proposal (#5000)** is the strongest signal for future direction, but it is in the proposal phase and likely won't ship in the next point release.
- **New platform support (PR #5115):** A PR adding a LINE Messaging API channel is open, signaling continued expansion of communication backends.
- **Image-Aware Model Presets (PR #5148):** An open PR to add model presets that are aware of image-input support indicates a push to better handle multimodal models.
- **Unified Extension Platform (PR #5098):** An open PR introduces a native Python extension system to fill capability gaps not covered by skills or MCP, suggesting a long-term move toward greater modularity.

### 7. User Feedback Summary
- **Pain Point: High Token Consumption (Issue #1332):** A long-standing issue from February was closed today. The user reported extremely high token usage (5000+ input tokens just for "hello"). The issue was closed as stale, but it highlights a recurring user concern about cost and efficiency.
- **Pain Point: Audio Messages (Issue #5149):** A new user reports that NanoBot does not *send* audio messages on WhatsApp, despite being able to receive them. This points to an incomplete feature in the WhatsApp channel implementation.

### 8. Backlog Watch
- **Issue #1332 (Token Consumption):** Recently closed as stale. This is a common user complaint across many LLM projects. While closed, maintainers should be aware it represents a latent usability issue that could resurface.

**No new critical issues requiring immediate maintainer attention were identified in the open backlog today.** The team is actively working through the new, high-quality bug reports.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-29

## Today's Overview

Hermes Agent shows high activity with 50 issues and 50 PRs updated in the last 24 hours, indicating a healthy, actively maintained project. The community is engaged, with 40 open/active issues and 10 closed, while the PR pipeline shows a balanced 25 open vs. 25 merged/closed, reflecting steady feature integration and bugfix throughput. Notably, maintainers appear to be consolidating contributor work — several PRs today salvage or supersede earlier contributions, suggesting a deliberate effort to land clean, reviewed changes over broad swarms. The project has not published a new release today.

## Releases

No new releases were published on 2026-07-29. The last release remains the current stable version, with ongoing work likely targeting the next minor or patch release.

## Project Progress

25 pull requests were merged or closed today. Key improvements include:

- **Desktop UI Overhaul**: [PR #73561](https://github.com/NousResearch/hermes-agent/pull/73561) adds a dedicated "Photon" section in the Desktop messaging sidebar for iMessage sessions, salvaging a 4-PR swarm into a clean fix.
- **Performance: FTS Write Lock Fix**: [PR #73579](https://github.com/NousResearch/hermes-agent/pull/73579) (and related #65554) bounds routine full-text search maintenance, preventing `database is locked` errors that killed turns every 1,000 writes. This addresses a painful production issue.
- **Gemini Default Model Sweep**: [PR #73570](https://github.com/NousResearch/hermes-agent/pull/73570) updates all hardcoded Gemini defaults to `gemini-3.6-flash`, fixing issue #32360 and accounting for Google's deprecation of `gemini-2.5-flash`.
- **Photon Bugfix Wave**: [PR #73560](https://github.com/NousResearch/hermes-agent/pull/73560) bundles four fixes for iMessage — U+FFFC ghost messages, streaming tofu artifacts, API envelope parsing, and test isolation.
- **Duplicate Fix Consolidation**: Three PRs from contributor JonthanaHanh closed duplicates for issues around model normalization double-namespacing ([#72464](https://github.com/NousResearch/hermes-agent/pull/72464)), dict-vs-object response crashes ([#72459](https://github.com/NousResearch/hermes-agent/pull/72459)), and JSON NO_REPLY envelope handling ([#73034](https://github.com/NousResearch/hermes-agent/pull/73034)).

Several PRs remain open pending review or needs-decision labels, including Mattermost parity ([#17606](https://github.com/NousResearch/hermes-agent/pull/17606)), QQBot media delivery ([#40457](https://github.com/NousResearch/hermes-agent/pull/40457)), and the TrustBoost PII sanitizer skill ([#17472](https://github.com/NousResearch/hermes-agent/pull/17472)).

## Community Hot Topics

- **Buzz Messaging Integration** ([Issue #68871](https://github.com/NousResearch/hermes-agent/issues/68871), closed, 18 comments, 16 👍): This was the most active feature request today, proposing integration with Block's open-source "Buzz" workspace for human-agent team messaging. Already closed, suggesting maintainers evaluated and either accepted or deferred quickly.

- **Gemini Tool Schema Compatibility** ([Issue #71804](https://github.com/NousResearch/hermes-agent/issues/71804), open, 3 comments): A critical bug where Gemini models reject tool schemas because array parameters lack `items` fields, causing HTTP 400 errors before generation. This affects all users with Gemini-based providers.

- **Desktop Profile WebSocket Bug** ([Issue #71527](https://github.com/NousResearch/hermes-agent/issues/71527), open, 6 comments): Desktop fails to pass the active profile as a query parameter to the WebSocket connection, breaking multi-profile setups. Affects users managing multiple agent personas.

- **CI Auto-Fix Robot** ([PR #73753](https://github.com/NousResearch/hermes-agent/pull/73753), closed): The `hermes-seaeye[bot]` automated a lint/formatting fix — a sign the project is investing in automated quality enforcement.

The Buzz integration and Gemini schema issues reflect the community's desire for broader platform interoperability and provider compatibility, respectively.

## Bugs & Stability

**Critical/High Severity (P2, active bugs):**

| Issue | Summary | Status |
|-------|---------|--------|
| [#71804](https://github.com/NousResearch/hermes-agent/issues/71804) | Gemini rejects tool schemas with missing `items` field — HTTP 400 before generation | Open, no fix PR yet |
| [#71527](https://github.com/NousResearch/hermes-agent/issues/71527) | Desktop doesn't pass `?profile=` to WebSocket, breaking multi-profile setups | Open |
| [#71453](https://github.com/NousResearch/hermes-agent/issues/71453) | `hermes chat -q` still kills children on exit, missed by #66617's sync fallback | Open |
| [#69107](https://github.com/NousResearch/hermes-agent/issues/69107) | TUI session state stale when another client writes to same session | Open |
| [#66587](https://github.com/NousResearch/hermes-agent/issues/66587) | Gemini HTTP 400: missing `thought_signature` in functionCall | Open |
| [#62975](https://github.com/NousResearch/hermes-agent/issues/62975) | Node sidecar NPM error on Podman install | Open |
| [#24159](https://github.com/NousResearch/hermes-agent/issues/24159) | Codex Responses API soft failures bypass credential pool rotation | Open |
| [#18421](https://github.com/NousResearch/hermes-agent/issues/18421) | `/goal` judge false positive when file write silently fails | Open |
| [#18470](https://github.com/NousResearch/hermes-agent/issues/18470) | Custom OpenAI providers lose `temperature` and `parallel_tool_calls` fields | Open |
| [#17575](https://github.com/NousResearch/hermes-agent/issues/17575) | Docker/container: `HERMES_INTERACTIVE=1` triggers sudo prompts in cron | Open |
| [#17576](https://github.com/NousResearch/hermes-agent/issues/17576) | Docker: gateway restart race conditions from bash watcher | Open |
| [#17157](https://github.com/NousResearch/hermes-agent/issues/17157) | Discord slash command sync times out recreating unchanged commands | Open |
| [#14324](https://github.com/NousResearch/hermes-agent/issues/14324) | QQBot image attachments with `content_type=file` never reach vision pipeline | Open |

**Closed today:**
- [#49253](https://github.com/NousResearch/hermes-agent/issues/49253) — Photon iMessage bold markdown corrupts Unicode (fixed via PR #73560)
- [#49793](https://github.com/NousResearch/hermes-agent/issues/49793) — Photon iMessage streaming cursor tofu artifact (fixed via PR #73560)
- [#2743](https://github.com/NousResearch/hermes-agent/issues/2743) — Command injection risk via `shell=True` in subprocess calls (security fix)
- [#50081](https://github.com/NousResearch/hermes-agent/issues/50081) — `_run_command_tts` hard timeout truncation

The Gemini schema bug (#71804) and the desktop profile WebSocket bug (#71527) stand out as the most impactful open issues without fix PRs.

## Feature Requests & Roadmap Signals

**High-interest features under discussion:**

- **Buzz Messaging Integration** ([#68871](https://github.com/NousResearch/hermes-agent/issues/68871)) — Already closed, but the 16 👍 indicates strong demand for team workspace integration.
- **Hetzner AI Inference Provider** ([#73423](https://github.com/NousResearch/hermes-agent/issues/73423), open, 2 comments) — User request for an additional OpenAI-compatible provider endpoint.
- **ACP Registry Registration** ([#47435](https://github.com/NousResearch/hermes-agent/issues/47435), open, 3 comments) — Register Hermes so Zed/JetBrains/VS Code can discover it natively.
- **Parallel Task Execution** ([#1468](https://github.com/NousResearch/hermes-agent/issues/1468), open, 4 comments) — Third option beyond "interrupt" or "queue" for concurrent user requests.
- **Plugin Hook for Message Transformation** ([#20307](https://github.com/NousResearch/hermes-agent/issues/20307), open, 2 comments) — Plugin authors need a `transform_api_message` hook.
- **YAML Schema for Config** ([#17266](https://github.com/NousResearch/hermes-agent/issues/17266), open, 1 comment, 4 👍) — Editor autocompletion for `config.yaml` via JSON schema.
- **Expandable Tool Calls in TUI** ([#16636](https://github.com/NousResearch/hermes-agent/issues/16636), open, 2 comments) — Users want to inspect full tool call context/results in-terminal.
- **Context-Aware Skills Budget** ([#10164](https://github.com/NousResearch/hermes-agent/issues/10164), open, 4 comments) — System prompt budget management to prevent context overflow.

**Predictions for next version:**
- The Buzz integration, if accepted, could land as a gateway adapter or plugin.
- ACP Registry registration is a low-effort, high-visibility change that would improve IDE adoption.
- The YAML schema for config is highly requested (4 👍 with few comments), and could be a quick win for maintainers.

## User Feedback Summary

**Positive signals:**
- The project is shipping fixes for high-friction bugs (FTS write lock, Gemini defaults, Photon iMessage artifacts).
- Automation (CI auto-fix bot, stale PR handling) shows investment in contributor experience.

**Pain points expressed:**
- **Docker reliability**: Multiple Docker-specific bugs remain open (#17575, #17576, #62975), indicating container deployments are fragile.
- **Gemini compatibility**: Two open bugs (#71804, #66587) and the model default sweep suggest Google's Gemini API is a persistent source of friction.
- **Multi-client state staleness**: Issue #69107 describes a real user experience problem where the TUI doesn't reflect writes from other clients — a usability blocker for power users running both TUI and web UI.
- **Configuration difficulty**: Feature request #17266 (YAML schema) echoes frustration with manual config editing.
- **Goal evaluation unreliability**: Issue #18421 reports `/goal` judging based on agent claims rather than verified evidence — undermines trust in the autonomy feature.

**Dissatisfaction areas:**
- Custom OpenAI provider support is broken in the field (#18470) — temperature and tool call parameters silently drop.
- QQBot image handling (#14324) and Discord slash command perf (#17157) indicate platform-specific polish is uneven.

## Backlog Watch

**Long-unanswered issues needing maintainer attention:**

| Issue | Age | Summary | Risk |
|-------|-----|---------|------|
| [#8465](https://github.com/NousResearch/hermes-agent/issues/8465) | ~109 days | Proper LiteLLM support — context size detection broken | Unaddressed, 7 👍 |
| [#1468](https://github.com/NousResearch/hermes-agent/issues/1468) | ~136 days | Parallel task execution — fundamental UX feature | Unanswered, 4 comments |
| [#10164](https://github.com/NousResearch/hermes-agent/issues/10164) | ~105 days | Context-aware skills budget — prevents context overflow crashes | Needs decision |
| [#16233](https://github.com/NousResearch/hermes-agent/issues/16233) | ~94 days | Add `topic` + `days` params to web search tool | Unanswered, 1 comment |
| [#17266](https://github.com/NousResearch/hermes-agent/issues/17266) | ~91 days | YAML schema for config-language-server | 4 👍, 1 comment |
| [#18422](https://github.com/NousResearch/hermes-agent/issues/18422) | ~90 days | MEDIA delivery support for plugin platforms via adapter | 1 comment |

**PRs pending review or decision:**
- [#17472](https://github.com/NousResearch/hermes-agent/pull/17472) — TrustBoost PII sanitizer skill (open since April 29, 2026)
- [#17606](https://github.com/NousResearch/hermes-agent/pull/17606) — Mattermost configurable prefix and reactions (open since April 29, 2026)
- [#40457](https://github.com/NousResearch/hermes-agent/pull/40457) — QQBot MEDIA delivery (open since June 6, 2026)
- [#45922](https://github.com/NousResearch/hermes-agent/pull/45922) — Anthropic partial-stream recovery (open since June 14, 2026)

The LiteLLM context size issue (#8465) is particularly notable: it has 7 👍 and has been open for over 3 months, suggesting a real gap in provider configuration that affects many self-hosted users. The Mattermost and QQBot PRs have been pending since late April and early June respectively, risking contributor attrition if not reviewed soon.

---

*Generated from GitHub data as of 2026-07-29 23:59 UTC. Data includes 50 issues and 50 PRs updated in the last 24 hours.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-29

## Today's Overview
The PicoClaw project shows **moderate activity** with 4 issues updated in the last 24 hours (1 open, 3 closed) and 10 pull requests updated (7 still open, 3 merged/closed). No new releases were published. Community contributions remain steady, with several infrastructure improvements and provider-specific fixes landing. Seven long-standing PRs remain open, suggesting maintainer bandwidth may be constrained.

## Releases
**None.** No new releases were published today.

## Project Progress
Three pull requests were merged or closed in the last 24 hours:
- **#3256 (Closed, merged)** — `fix(feishu): send audio and video with native message types` (Author: AaronZ345). Feishu channel now correctly sends audio/video as native playable messages instead of generic downloadable files.
- **#3254 (Closed, merged)** — `fix(agent): prefer verbatim model matches over provider-alias splits when resolving refs` (Author: fabdelgado). Fixes model resolution where earlier `model_list` entries could incorrectly win via provider-alias splitting over exact model string matches.
- **#3228 (Closed, merged)** — `fix(anthropic-messages): send SystemParts as system blocks with cache_control` (Author: AayushGupta16). Enables Anthropic prompt caching on the `anthropic_messages` provider by preserving per-block `cache_control` markers.

Also closed without merge:
- **#3300 (Closed)** — Bug report about `read_file` tool missing causing deadlock in conversations.

## Community Hot Topics
The most engaging discussions this update period:

1. **#3088** [CLOSED] — `[Feature] use vodozemac instead of libolm` (10 comments, 2 👍) — Community-driven request to replace the unmaintained `libolm` cryptographic library with its official replacement `vodozemac`. Strong interest, but the issue was closed without indication of implementation.

2. **#3182** [OPEN] — `[BUG] Android version` (5 comments) — User reports inability to launch the PicoClaw service on Android despite full permissions. Cannot change path from settings. No fix PR linked; issue remains open and stale.

3. **#3255** [CLOSED] — `[BUG] DingTalk chat list preview shows fixed "PicoClaw" instead of message content` (2 comments) — UI bug affecting chat list previews on the DingTalk channel. Closed, suggesting resolution or workaround.

**Underlying needs:** Users are requesting security modernization (vodozemac), mobile platform support improvements, and local language (Chinese) platform integration reliability (DingTalk, Feishu).

## Bugs & Stability
**High Severity:**
- **#3300** — `工具集缺失 read_file 导致每次对话死锁` (Missing `read_file` tool causes deadlock in conversations). Closed same day with 0 comments — suggests it was a duplicate, documentation issue, or quickly resolved. Without merge history visible, this could be a latent bug. **No fix PR identified.**

**Medium Severity:**
- **#3182** — Android service launch failure. No PR linked, no resolution. Platform-breaking for Android users.
- **#3255** — DingTalk chat list preview bug. Closed; likely fixed.

**Low Severity / In Progress:**
- **#2251** (stale but referenced in PR descriptions) — Tool-call format leakage into summaries. PR #3279 (open) aims to fix a related `seahorse` variant.

## Feature Requests & Roadmap Signals
New feature requests/implementations visible:
- **#3299** [OPEN] — `Add native Exa web search provider` (Author: kesku). Adds a new web search backend, expanding search provider diversity. Likely to merge next version.
- **#3200** [OPEN] — `feat(models): add configurable default fallback chain` (Author: lc6464). Enhances model fallback configurability via Web UI. Backend + frontend change; likely mid-term.
- **#1951** [OPEN, stale since March] — `chore: move installation scripts from docs repo to here` (Author: lc6464). Infrastructure improvement — consolidating documentation. Low priority but important for new users.
- **#3088** (closed) — Vodozemac replacement for libolm. Despite closure, security concerns may re-emerge.

**Prediction:** The Exa search provider (#3299) and model fallback chain (#3200) are strong candidates for the next release. The vodozemac migration may reappear as a prioritized issue.

## User Feedback Summary
**Positive signals:**
- Active Chinese-language community (DingTalk, Feishu, Chinese bug reports) indicates growing adoption in East Asian markets.
- Community contributors are submitting high-quality, structural fixes (Anthropic caching, model resolution, audio/video media types).

**Pain points:**
- **Android support (#3182)** is a recurring blocker for mobile users.
- **Tool availability (#3300)** — users want `read_file` to be available as a standard tool, not just through fixed-file injection.
- **OAuth login flow (#3280)** — broken on headless/remote setups; authorization codes get burned on failure.
- **Anthropic caching (#3251, #3228)** — operators cannot see cache metrics, making cost optimization difficult.

**Satisfaction indicators:** Users are actively contributing code (10 PRs in 24h), indicating high engagement and a healthy contributor community.

## Backlog Watch
Long-unanswered items requiring maintainer attention:

1. **#1951** [OPEN since 2026-03-24] — Installation scripts migration. Stale for **4 months**. Minimal code complexity but blocks documentation consolidation.

2. **#3182** [OPEN since 2026-06-26] — Android launch failure. **No fix PR exists, no maintainer response visible.** Critical for mobile users.

3. **#3280** [OPEN since 2026-07-21] — OAuth login fix. Authored with four root causes identified. Stale after ~7 days. High impact for remote/headless deployments.

4. **#3251** [OPEN since 2026-07-12] — Anthropic cache token capture. Technically important for cost transparency. Two related PRs (#3251, #3228) — one merged, one awaiting review.

5. **#3279** [OPEN since 2026-07-21] — Seahorse tool-call format leak. Related to established bug pattern; merging would close multiple discussions.

**Severity ranking for maintainer attention:**
1. **#3182** (Android — breaking for mobile users, no response)
2. **#3280** (OAuth — blocks headless auth, four bugs identified)
3. **#3251** (Anthropic cache — cost visibility, blocking operator adoption)
4. **#1951** (Install scripts — low urgency, 4-month stale)
5. **#3279** (Seahorse leak — moderate, has PR ready)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-29

## Today's Overview
NanoClaw showed elevated development activity today with 11 pull requests updated in the last 24 hours, though no new releases or fresh issues were filed. The core team appears to be on a focused bug-fix sprint, with seven open PRs addressing stability, configuration, and database consistency issues, while four closed PRs represent completed work. The project maintains a strong contributor pulse with multiple first-time contributors and experienced core members shipping fixes in parallel. Overall project health is good, with the community actively patching regressions rather than discovering new feature gaps.

## Releases
No new releases were published today. The latest available version remains the one associated with the previous release cycle.

## Project Progress
Four pull requests were merged or closed today, representing concrete improvements to the codebase:

- **#3060** — `fix(container): add --init to agent container spawn args` (merged). This closes a known production gap where zombie processes accumulated because agent containers lacked PID 1 reaping. The fix also corrects documentation in `docs/build-and-runtime.md` that incorrectly claimed the gap was already handled.
- **#2197** — `fix(update-nanoclaw): guard merge state` (merged). Prevents `/update-nanoclaw` from silently producing single-parent commits instead of real merges when run on customized forks. This is a critical fix for users maintaining long-lived forks.
- **#1136** — `feat(update-nanoclaw): add auto-merge audit and container smoke test` (merged). Adds two safety steps that catch silent code drops during upstream merges, triggered by a real incident where git auto-merge deleted code without conflict markers.
- **#1255** — `feat: add MiniMax OAuth as model provider` (closed, not merged). This long-running PR (from March 2026) was closed without merging. It added device-code OAuth flow with PKCE S256 for MiniMax's Coding Plan as an alternative to Anthropic API keys.

## Community Hot Topics
No issues were updated today, so the most active discussions are concentrated around open pull requests:

- **#3057** — `Dual-engine quota fallback: Claude→Codex overflow, handoff recaps, proactive quota warning` ([PR #3057](https://github.com/nanocoai/nanoclaw/pull/3057)). This feature branch has been battle-tested in production since July 6 on a live WhatsApp deployment. It addresses the fundamental pain point of Claude API quota exhaustion by automatically falling back to Codex, with handoff summaries and proactive warnings. It's the most substantial feature under review, with deep architectural implications for multi-provider support.

- **#3143** — `Preserve resolved approval card content` ([PR #3143](https://github.com/nanocoai/nanoclaw/pull/3143)). Addresses UI state persistence where resolved approval cards lost their title and request details after resolution. Underlying need: operators need to audit past approvals even after cards are resolved.

- **#3144** — `feat(webhook): configurable bind address via WEBHOOK_HOST` ([PR #3144](https://github.com/nanocoai/nanoclaw/pull/3144)). Hardcoded `0.0.0.0` bind exposed webhook servers on all interfaces, a security concern for deployments that want to restrict listening. Community is asking for basic network security hygiene.

## Bugs & Stability
Three bugs were addressed today, all with fix PRs submitted:

- **High severity: Zombie process accumulation in agent containers** — Fixed by PR #3060 (merged). Agent containers lacked `--init`, causing PID 1 to not reap zombie child processes. Could lead to resource exhaustion in long-running deployments. ✅ Fix merged.

- **Medium severity: Silent single-parent commits during upstream merges** — Fixed by PR #2197 (merged). Custom forks running `/update-nanoclaw` could silently lose merge history integrity. ✅ Fix merged.

- **Medium severity: WEBHOOK_PORT not honoring .env** — Addressed by PR #3148 (open). Environment variable `WEBHOOK_PORT` was not following NanoClaw's normal configuration precedence, meaning `.env` values were ignored unless the variable was also set in the process environment. Workaround existed (set as real env var), but violated user expectations. ⏳ Fix submitted.

- **Low severity: Rotten dev scripts** — Addressed by PR #3146 (open). Two dev scripts (`test-v2-host.ts` and another) had drifted from the current architecture and would crash before completing. Only affects developers running test scripts. ⏳ Fix submitted.

- **Low severity: Missing channel destinations in existing wirings** — Addressed by PR #3145 (open). Database migration gap where messaging-group wirings created before the destinations feature lacked channel destination records. ⏳ Fix submitted.

- **Low severity: Lost approval card content on resolution** — Addressed by PR #3143 (open). Resolved cards lost their title and request details, making post-resolution audits impossible. ⏳ Fix submitted.

## Feature Requests & Roadmap Signals
No new feature requests were filed today, but several themes emerge from the active PRs:

- **Multi-model provider fallback** (PR #3057) — This is the strongest roadmap signal. Production-tested Claude→Codex quota fallback with handoff recaps suggests NanoClaw is moving toward a resilient multi-provider architecture. This could appear in the next stable release.
- **Configurable webhook security** (PR #3144, PR #3148) — Two PRs targeting webhook server configurability (bind address and port) indicate growing enterprise deployment requirements. Likely to land together.
- **Database migration hygiene** (PR #3145) — A migration to backfill missing channel destinations signals that database schema evolution is maturing. Expect more migration-rigor features.

## User Feedback Summary
While no direct user comments or reactions were recorded, the PR descriptions reveal concrete pain points:

- **Configuration surprise**: Users expected `WEBHOOK_PORT` from `.env` to work without also setting it as a system environment variable. The fix restores the standard precedence that users reasonably assumed.
- **Fork maintenance friction**: Two PRs (#2197, #1136) address fork users' struggles with silent merge failures and code drops. These users are sophisticated operators who customize their deployments, and they've been burned by git auto-merge.
- **Production quota anxiety**: PR #3057 was built from a live WhatsApp deployment, indicating real production users hit Claude API quota limits frequently enough that automatic fallback became a must-have feature.
- **Terminal workflow auditability**: PR #3143's fix for resolved card content suggests users rely on approval cards as audit trails, not just transient interaction points.

## Backlog Watch
No long-stale issues or PRs currently require maintainer attention. The oldest open pull request among those updated today is #3057 (created July 15), which is actively reviewed. All other open PRs were created on July 27–28. The project's issue tracker is clean, with no orphaned bug reports or unanswered feature requests. Maintainer response times appear healthy.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-29

## Today's Overview

IronClaw shows high-velocity development with **50 issues and 50 PRs updated in the last 24 hours**, signaling a major feature push. The project closed **16 issues** and **15 PRs** today, with core contributors driving large refactors across the Reborn stack, messaging framework, and sandbox security layer. Activity centers on the **Hermetic capability testing epic (#6524)** and the **error-recoverability endgame (#6284)**, both nearing completion. No new releases were cut today; the project remains on `ironclaw 1.0.0` with a pending release PR (#5598) that has been open since July 3.

## Releases

- **No new releases today.** The last published version remains `ironclaw 1.0.0`. A release PR (#5598) has been open since July 3 and would bump `ironclaw_common` (0.4.2 → 0.5.0, breaking) and `ironclaw_skills` (0.3.0 → 0.4.0, breaking), but appears stalled.

## Project Progress

**15 PRs merged/closed today.** Key advances:

| PR | Title | Impact |
|---|---|---|
| [#6816](https://github.com/nearai/ironclaw/pull/6816) | Centralize ingress and scope manifest commands | Fixes channel auth/approval with fail-closed `[channel] commands` manifest allowlist |
| [#6696](https://github.com/nearai/ironclaw/pull/6696) | Collapse lifecycle state into row-native process journal | DB migration making `ironclaw_processes` the lifecycle authority |
| [#6729](https://github.com/nearai/ironclaw/pull/6729) | Normalize extension installation persistence | Installation state now in durable lifecycle records, closes #6481 epic workstream |

**Feature completions on epic #6524 (Hermetic testing platform):**
- WS4: [#6823](https://github.com/nearai/ironclaw/pull/6823) — Gate persistence backends on inventory coverage
- WS6: [#6825](https://github.com/nearai/ironclaw/pull/6825) — Cross fault profiles with failure fates
- WS8: [#6828](https://github.com/nearai/ironclaw/pull/6828) — Gate generic extension webhook ingress

**Feature completions on epic #6284 (Error recoverability):**
- WS1: [#6824](https://github.com/nearai/ironclaw/pull/6824) — Stop retrying model-stage failures that cannot succeed
- WS5: [#6826](https://github.com/nearai/ironclaw/pull/6826) — Stop reading rate limits as auth failures
- WS9: [#6832](https://github.com/nearai/ironclaw/pull/6832) — Bound recovery per RUN, not just per stage

## Community Hot Topics

| Issue/PR | Engagement | Signal |
|---|---|---|
| [#6284](https://github.com/nearai/ironclaw/issues/6284) — Error-recoverability epic | 15 comments, open 10 days | **Highest-engagement item.** Community deeply invested in this contract (model recovers from 100% of errors it sees); design has five explicit sub-conditions (a–e). |
| [#6524](https://github.com/nearai/ironclaw/issues/6524) — Hermetic capability testing | 3 comments | Underlying need: deterministic, mechanically-answerable coverage questions for every supported capability. |
| [#6820](https://github.com/nearai/ironclaw/issues/6820) — IronHub unsigned catalog URL | 2 comments | Trust-boundary issue: agent fetches unsigned URLs when discovery disappoints — filed separately as security-relevant. |

**Analysis:** The community is signaling a strong preference for **deterministic reliability guarantees**. Both #6284 and #6524 address the same root need: "can I trust the system to work without manual babysitting?" The high engagement on #6284 (15 comments) suggests the error-recoverability contract is considered a make-or-break design decision.

## Bugs & Stability

**P1 Bugs (active today):**

| Issue | Description | Severity | Fix PR? |
|---|---|---|---|
| [#6835](https://github.com/nearai/ironclaw/issues/6835) | MCP auth failures never raise a re-auth gate (classified as Client, not AuthRequired) | **Critical** — silent misclassification leaves users permanently locked out | No fix PR yet |
| [#6805](https://github.com/nearai/ironclaw/issues/6805) | Railway instance returns `service_unavailable` ~every 30 min | **High** — affects all functions intermittently | No fix PR, but related to [#6815](https://github.com/nearai/ironclaw/issues/6815) (turn-state store latch degraded forever) |
| [#6815](https://github.com/nearai/ironclaw/issues/6815) | Turn-state store latches degraded forever after one write-behind flush failure | **High** — requires restart to recover | No fix PR yet |
| [#6834](https://github.com/nearai/ironclaw/issues/6834) | Slack setup fails in IronClaw (near.foundation account) | **High** — blocks Slack integration onboarding | No fix PR yet |

**P2 Bugs:**

| Issue | Description |
|---|---|
| [#6833](https://github.com/nearai/ironclaw/issues/6833) | Notion tool fails to install in IronClaw |
| [#6806](https://github.com/nearai/ironclaw/issues/6806) | Automations don't show in web chat (must navigate to automations page) |
| [#6814](https://github.com/nearai/ironclaw/issues/6814) | Third-party skills trip prompt content denylist on 1.0.0 ("API key" in description kills every run) |

**Notable regression:**
- [#6826](https://github.com/nearai/ironclaw/pull/6826) fixes a **live bug** where rate-limit error strings containing `401` or `403` triggered misclassification as auth failures — meaning retryable rate limits burned retry budget and escalated incorrectly.

## Feature Requests & Roadmap Signals

| Request | Source | Likely Version |
|---|---|---|
| [#6806](https://github.com/nearai/ironclaw/issues/6806) — Automations visible in web chat | User feedback (bug_bash) | Next patch |
| [#6837](https://github.com/nearai/ironclaw/issues/6837) — Info-level logging for growth/usage stats | Contributor | Under consideration — zero `info!` calls in `ironclaw_analytics` |
| [#6810](https://github.com/nearai/ironclaw/issues/6810) — Progressive tool disclosure as default | Epic #6284 scope | Post-1.0.0 |

**Prediction:** The next release (likely 1.1.x or 2.0.0-alpha given pending breaking changes) will include **Hermetic testing platform integration** (#6524) and the **standardized messaging framework** (#6831). The error-recoverability contract (#6284) is the highest-priority design item and likely gates the next major version.

## User Feedback Summary

**Pain points reported:**
1. **Integration reliability:** Both Slack (#6834) and Notion (#6833) setup fail in user instances. The Slack issue affects `near.foundation` accounts specifically, suggesting a tenant-scoped configuration problem.
2. **Visibility gaps:** Automations run silently — users must manually navigate away from chat to see results (#6806).
3. **Service instability:** The Railway QA instance returns `service_unavailable` every ~30 minutes (#6805), affecting all functionality.
4. **Skill execution blocked:** Third-party skills containing "API key" in their description fail universally on 1.0.0 (#6814) — a regression from the certified-skill exemption in #5258.

**Satisfaction signals:** None reported today. The bug_bash findings suggest the QA preview is catching real issues before they reach production users.

## Backlog Watch

**Long-stale items needing maintainer attention:**

| Item | Age | Issue |
|---|---|---|
| [#5598](https://github.com/nearai/ironclaw/pull/5598) — Release PR | 26 days open | Blocked? Contains breaking changes in `ironclaw_common` and `ironclaw_skills`. No response from maintainers since July 3. |
| [#5659](https://github.com/nearai/ironclaw/pull/5659) — Tool-disclosure security surface fix | 24 days open | Contains three production-impacting fixes for tool-disclosure leak vectors. Marked for Reborn stack. |

**Emerging risk:** The turn-state store latch issue (#6815) that required a 30-minute manual restart on the QA deploy indicates a **reliability debt** in the persistence layer. With #6524 WS4 now gating persistence backends on inventory coverage, this may get systematic testing soon, but the live service behavior warrants an urgent fix.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the project digest for **LobsterAI** on **2026-07-29**.

---

# LobsterAI Project Digest — 2026-07-29

## 1. Today's Overview
LobsterAI saw a high-velocity day focused on **Windows installer stability** and **runtime safety**. **6 pull requests were merged/closed** (driven primarily by contributor `fisherdaddy`), addressing a critical installer rollback bug, a false-positive token-burn guard, and a new `/btw` side-chat feature. However, **5 open issues** surfaced, including a new installation-blocking bug and a silent failure for `exec` tool shell commands. Community engagement remains moderate, with several stale issues receiving activity after months of silence.

## 2. Releases
**No new releases** were published today.

## 3. Project Progress
Six PRs were merged/closed today, pushing the project forward on both stability and new features:

- **#2402** [CLOSED] — `fix(update): reject Windows installer redirects instead of trusting response.url`
  - Improves update reliability by validating Windows installer redirects.
- **#2400** [CLOSED] — `fix(openclaw): enforce runtime/config safety-contract gate to stop false-stop token burn`
  - Prevents the OpenClaw runtime from running without LobsterAI’s managed safety policy, avoiding wasted tokens.
- **#2399** [CLOSED] — `feat(renderer): hide sites nav entry outside test mode`
  - UI polish: hides an unfinished navigation entry during production use.
- **#2398** [CLOSED] — `fix(installer): drive Skills backup outcome from helper exit codes`
  - Fixes a Windows installer bug where a trailing CRLF caused the backup step to misread `exit 0` as a success, leading to a spurious "backup missing" state.
- **#2397** [CLOSED] — `feat(cowork): add isolated /btw side chat`
  - Adds a draggable, resizable floating side-chat panel for selected assistant text. Keeps `/btw` execution history isolated from the main conversation via the OpenClaw utility stream path.
- **#2394** [CLOSED] — `Fix/windows install manual overwrite blocked`
  - Fixes a Windows installer issue where a manual overwrite was blocked during update.

## 4. Community Hot Topics
No issues or PRs today generated high comment/reaction counts. Notable discussions include:

- **#2401** — *"skill技能"* (1 comment)
  - User asks whether LobsterAI's PDF/Docs/PPTX/XLSX skills use Anthropic's official implementations and whether those skills can be used commercially. This signals growing user concern about **licensing and third-party dependency compliance**.

- **#2396** — *"[Bug] exec 工具的默认 shell wrapper = Windows PowerShell 5.1"* (0 comments, new)
  - Reports that the `exec` tool defaults to PowerShell 5.1, causing Linux commands and inline scripts with special characters to fail silently. Unanswered as of publish.

## 5. Bugs & Stability
Two new bugs were reported today, ranked by severity:

| Severity | Issue | Summary | Fix PR |
|----------|-------|---------|--------|
| **Critical** | #2395 | **Installer blocks update**: "The LobsterAI update stopped because user skills could not be backed up." The previous installation is not replaced, leaving the user stuck. | #2398 (merged) addresses the backup logic; user error persists if the fix doesn't apply retroactively. |
| **High** | #2396 | `exec` tool silently fails on Windows when the target command requires a different shell wrapper (e.g., `grep`, `node -e`). Full session logs are available but AI behavior is broken. | No fix PR yet. |

Additionally, #1236 (plugin ID mismatch warning) and #2071 (scheduled task creation error) received updates after being stale for months, but remain **unresolved** and **unassigned**.

## 6. Feature Requests & Roadmap Signals
- **#2397** (merged today) — `/btw` isolated side chat is a clear enterprise/team collaboration signal. Expect it to appear in the next minor release.
- **#2401** — The commercial-use question about Anthropic skills may prompt a **licensing FAQ update** or a **skill attribution change** in the next release.
- **#2399** (merged) — Hiding the "sites" nav entry suggests an experimental multi-agent or site-browsing feature being developed internally, likely for a future beta.

## 7. User Feedback Summary
- **Installation frustration**: User `1yuyin1` (#2395) reports a complete installation block. PowerShell helper exit code handling (merged in #2398) directly addresses this class of failure.
- **Cross-platform CLI pain**: User `woxinsj` (#2396) describes advanced usage (PowerShell 7 + `node -e` + `grep`) that breaks due to Shell wrapper defaults. This is a **power-user dissatisfaction** signal.
- **Skill licensing concern**: User `whz1106` (#2401) raises a commercial-use compliance question, indicating that LobsterAI may need to clarify its dependency licenses for enterprise adopters.

## 8. Backlog Watch
Two **stale issues** and one **stale PR** remain open without maintainer assignment:

- **Issue #1236** (created 2026-04-01) — *[bug]插件 ID 不匹配警告* — Plugin ID mismatch warning on every gateway restart. Received a comment today but still no maintainer response or fix. **High-priority**: configuration noise erodes user trust.
- **Issue #2071** (created 2026-05-28) — *创建定时任务错误* — Scheduled task creation fails. No comments from maintainers. Given it's a core feature (task scheduling), this is a **medium-high concern**.
- **PR #1233** (created 2026-04-01) — *feat(model): 为模型提供商添加官网链接和 API Key 获取引导* — Adds official website links and API key guidance for model providers. No maintainer review in 4 months. **Low risk but high community value**: this is a quality-of-life improvement that would reduce user onboarding friction.

**Maintainer call to action**: #1236 (plugin ID mismatch) and #2396 (exec shell swallowing) are the most actionable high-severity items. The installer fix (#2398) was merged today, but a follow-up test to confirm #2395 is resolved would close the loop.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-29

## Today's Overview
Project activity today is **moderately high**, with 8 pull requests updated in the last 24 hours (6 open, 2 merged/closed) and 1 closed bug issue. The maintainer team, led by **penso**, is actively pushing three major feature branches: ACP agent exposure over stdio, comprehensive instrumentation and feedback infrastructure, and PWA notification reliability. The single bug issue (archiving cron sessions) was closed via a fix PR merged yesterday. No new releases were cut today, but the extensive PR activity signals that a significant feature release may be imminent.

## Releases
**No new releases today.** The latest published release remains unchanged. Given the volume of merged features in recent days (ACP selection, Slack Block Kit, instrumentation), a versioned release is likely soon.

## Project Progress
**Merged/Closed PRs (2):**
- **[#1172]** `fix(web): hide archived cron sessions by default` (merged) — Resolves the bug reported in #1111 by applying the existing archived-session preference to the Cron tab. Includes Playwright regression tests. (https://github.com/moltis-org/moltis/pull/1172)
- **[#1171]** `Move ACP selection into the chat model picker` (merged) — Integrates installed ACP clients directly into the composer model selector, removing the historical header-based ACP selector and redundant "Built-in LLM agent" option. Preserves per-session binding and reasoning controls. (https://github.com/moltis-org/moltis/pull/1171)

**Still Open:**
- **#1166** — Slack per-message acknowledgment reactions with phase feedback and Block Kit rendering (https://github.com/moltis-org/moltis/pull/1166)
- **#1170** — Privileged tool gating via per-account operators list, closing a security gap where channel senders could reach host tools (https://github.com/moltis-org/moltis/pull/1170)
- **#1169** — Expose Moltis as an ACP agent over stdio (https://github.com/moltis-org/moltis/pull/1169)
- **#1174** — Full instrumentation and feedback collection infrastructure (Langfuse v4, OTLP, reaction feedback) (https://github.com/moltis-org/moltis/pull/1174)
- **#1173** — PWA push notification reliability improvements (https://github.com/moltis-org/moltis/pull/1173)
- **#1175** — Terminal-Bench chat runner for benchmarking (https://github.com/moltis-org/moltis/pull/1175)

## Community Hot Topics
The most active discussion centers on the **instrumentation PR (#1174)**, authored by penso, which has been updated continuously since July 27. This PR touches on agent observability, Langfuse integration, and end-user reaction feedback — a topic with strong community interest given the lack of comment activity (undefined comments in data). The **ACP over stdio PR (#1169)** and **Terminal-Bench runner (#1175)** are also receiving sustained attention, indicating growing interest in programmatic agent access and benchmarking.

## Bugs & Stability
**One bug was resolved today:** Issue #1111 (`[Bug]: Archiving a cron session has no visible effect`) was closed via PR #1172, which hides archived cron sessions by default. **Severity: Medium** — this was a UX bug where the archive action appeared to do nothing because the archived sessions were not visually filtered in the Cron tab. A Playwright regression test was added to prevent recurrence.

**No new bugs were reported in the last 24 hours.** The fix PR #1170 (privileged tool gating) addresses a **security/latent bug** where channel senders with access allowlist membership could reach host commands — a high-severity issue that was proactively fixed before exploitation.

## Feature Requests & Roadmap Signals
Strong roadmap signals include:
- **ACP (Agent Communication Protocol) integration:** PR #1169 exposes Moltis as an ACP agent over stdio, and PR #1171 (merged) integrates ACP clients into the model selector. This suggests a **multi-agent ecosystem** is a core 2026 focus.
- **Observability infrastructure:** PR #1174 adds Langfuse v4 export, OTLP backends, and reaction feedback — likely leading to a **first-class observability dashboard** in the next release.
- **Slack UX improvements:** PR #1166 brings per-message reactions and Block Kit support, indicating investment in **enterprise Slack integrations**.
- **Performance benchmarking:** PR #1175 adds a Terminal-Bench chat runner, suggesting **performance regression testing** is becoming part of CI/QA.

Likely next-version features: ACP stdio mode, instrumentation dashboard, PWA reliability, and operator-based access control.

## User Feedback Summary
**No direct user feedback** (comments, reactions) was recorded in the last 24 hours on issues or PRs. However, the pattern of activity implies:
- **Pain point addressed:** Cron session archiving was confusing users (issue #1111). The fix improves UX clarity.
- **Unmet need (implicit):** The Slack reaction PR (#1166) directly responds to the fact that Slack bots cannot show typing indicators — users needed visible acknowledgment that their message was received.
- **Security concern (implicit):** PR #1170 closes a privilege escalation path. The lack of a public bug report suggests this was caught internally or reported privately.

## Backlog Watch
- **Issue #1111** is now closed, so no backlog concerns from that quarter.
- **No long-unanswered issues** are visible in the current data set. All 8 PRs have recent updates (within 24-48 hours), indicating active maintainer attention.
- **No stale issues or PRs** requiring maintainer action were identified.

**Overall health:** Excellent. The project is in an active development sprint with strong contributor velocity, zero open bugs, and proactive security fixes. The ACP and instrumentation features suggest a shift toward enterprise-grade observability and multi-agent interoperability.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Based on the GitHub data for CoPaw (agentscope-ai/CoPaw) as of 2026-07-29, here is the project digest.

---

## CoPaw Project Digest: 2026-07-29

### 1. Today's Overview
Project activity is **very high**, with 50 PRs and 18 Issues updated in the last 24 hours. The community is actively contributing both bug fixes and significant features, while the maintainers appear to be working through a stabilization phase following the 2.0.1 release and the recent 2.1.0b1 pre-release. A key theme emerging today is **isolation and security**, with multiple user reports and feature requests regarding agent data separation and session boundaries. The influx of bug reports related to reliability (MCP reconnection, config corruption) and developer experience (installer issues) suggests the project is balancing rapid iteration with hardening core stability.

### 2. Releases
**None.** No new releases were published in the last 24 hours. The latest available versions remain 2.0.1 and the 2.1.0b1 beta.

### 3. Project Progress
Today, **10 PRs were merged or closed**. Notable advances and fixes include:
- **Video Support Fix:** PR #6495 (`fix(video): deliver video data to models...`) was merged, closing issue #6474. This resolves a critical bug where the `view_video` tool reported success but the video data was silently dropped before reaching the LLM.
- **Plugin Compatibility:** PR #6497 (`fix(plugins): remove implicit max version derivation...`) from a first-time contributor was merged, fixing an issue where legacy plugins were silently disabled on 2.0+.
- **NoCode/Sole User Auth:** PR #6538 (`Feat/nocobase sole user authority`) from a first-time contributor was merged, adding a dedicated authority mode for single-user deployments.
- **Qubit Coverage Gate:** PR #6489 (`test(drivers): add Driver unit tests...`) was merged, enforcing a coverage floor for the Driver subsystem to prevent future regressions.

### 4. Community Hot Topics
The most active discussions center on **data isolation and security**:
- **#6461 [OPEN] - Agent Isolation Request:** [Link](agentscope-ai/QwenPaw Issue #6461) (👍: 2, Comments: 2). A user reports a serious privacy vulnerability: two agents bound to different QQ bots could read each other's memories and settings. The user requests a "complete isolation" toggle. This is the most "liked" issue today.
- **#6509 [OPEN] - Sub-Agent Isolation:** [Link](agentscope-ai/QwenPaw Issue #6509) (Comments: 2). Another user describes a related problem where Sub Agents can call each other and share session resources (files), leading to data leaks between different conversations.
- **#6520 [OPEN] - `agent.json` Corruption:** [Link](agentscope-ai/QwenPaw Issue #6520) (Comments: 2). A high-severity report detailing systematic corruption of the `agent.json` file on Windows (BOM, missing quotes), causing complete system failure. PRs #6528 and #6529 are open to fix this.
- **PR #6424 - Desktop GUI Automation:** [Link](agentscope-ai/QwenPaw PR #6424). This large feature PR (opened July 24) adding native desktop GUI automation for Windows and macOS continues to be updated, indicating it is a high-priority feature in the works.

The underlying need is clear: users are pushing QwenPaw into multi-tenant and multi-context production scenarios, and the current architecture's lack of strict agent isolation is a major pain point.

### 5. Bugs & Stability
Several significant bugs were reported today, ranked by severity:

- **Critical:** `agent.json` corruption (Issues #6520) is a system-killing bug on Windows, with a potential root cause in file write handling. Fix PRs #6528 are open.
- **High:**
    - **MCP Reconnection Failure (#6524):** MCP clients fail to recover after a server restart without manual intervention. This breaks the core reliability of the MCP tool integration.
    - **Windows Installer Infinite Loop (#6534):** The NSIS installer falsely detects itself as "still running," preventing installation. This is a blocker for new Windows users.
    - **Mission Mode Runtime Error (#6533):** A `TypeError` is thrown for any `/mission` command due to a missing keyword argument in a monkey-patch. Fix PR #6535 is open.
- **Medium:**
    - Skill Tags Disappear on Restart (#6537): A regression of a previous fix (#3270).
    - ACP `new_session` Response Missing Models (#6529): Hinders external client discovery. Fix PR #6531 is open.
    - Session Approval Level Not Inherited by Sub-Agents (#6506).
    - Chinese Path URL Encoding (#6510), causing file-not-found errors in Feishu (Lark) channels.

### 6. Feature Requests & Roadmap Signals
User-requested features today point towards **enterprise readiness and robust automation**:

- **Agent/Sub-Agent Isolation (#6461, #6509):** This is the strongest signal. It's likely that the next minor release (2.1.0) will include a feature for "strict agent isolation" to address these data leaks.
- **Streaming/Large Output for Shell Commands (#6514, #6513, #6512):** Multiple users (feng183043996) reported that `execute_shell_command` truncates outputs >30k characters, causing broken workflows.
- **MCP Reconnection Robustness (#6524):** The need for seamless recovery of MCP connections without manual commands is a clear signal for a more stateful and resilient integration layer.

Given the community pressure and security implications, **Agent Isolation** is the most likely candidate for the next feature milestone.

### 7. User Feedback Summary
- **Pain Points:** The dominant user pain point is **data privacy and lack of isolation**. Users are frustrated that agents can "see" each other's memories and settings, describing it as "unreasonable" and a "privacy leak." Stability issues like the Windows installer bug and config corruption create a high barrier to entry and frustration.
- **Use Cases:** Users are deploying QwenPaw in production-like scenarios: multi-role service (single-chat bot vs. group chat helper), multi-context file analysis, and external system integration via MCP.
- **Satisfaction/Dissatisfaction:** While engagement is high, the tone of many bug reports and feature requests reflects **dissatisfaction with current stability and isolation logic**, particularly for advanced use cases. The fact that multiple users reported the same `agent.json` corruption issue (though from different angles) indicates a systemic weakness. The fast response from the team (e.g., PRs opened for issues #6520, #6533 on the same day) is a positive signal.

### 8. Backlog Watch
- **PR #6151: Refactor Background Tool Calls:** [Link](agentscope-ai/QwenPaw PR #6151) (Opened July 15). A significant refactor of the background tool call mechanism. It has been open for two weeks with ongoing updates, suggesting it is large and complex. Its state should be monitored.
- **PR #6237 & #6267: Scroll History Improvements:** [Link](agentscope-ai/QwenPaw PR #6237) & [Link](agentscope-ai/QwenPaw PR #6267) (Opened July 17 & 20). Two long-running PRs related to improving the "Scroll" memory/history recall tool. These have been active for over a week and may be key to future agent memory performance.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

**ZeptoClaw Project Digest – 2026-07-29**

**1. Today's Overview**
Project activity is minimal today with no new issues, releases, or open/closed issue movement in the last 24 hours. The sole action is ongoing dependency management: one pull request (#613) was closed (merged), and a new PR (#649) was opened to bump the Docker base Rust image. Overall project velocity appears low, as the last human-authored feature or fix PR cannot be identified from today’s data. The project remains stable, with maintenance focused entirely on automated dependency updates.

**2. Releases**
No new releases were published today. The latest release date is unknown; no release data was provided.

**3. Project Progress**
- **PR #613** (closed, merged): Dependabot bumped the Rust Docker image from `1.95-slim-trixie` to `1.96-slim-trixie`. This is a routine security/build dependency update with no functional changes.  
  GitHub: [qhkm/zeptoclaw PR #613](https://github.com/qhkm/zeptoclaw/pull/613)

- **PR #649** (open): Proposes bumping the Rust Docker image from `1.95-slim-trixie` to `1.97-slim-trixie`, skipping version 1.96. This is the only open PR.  
  GitHub: [qhkm/zeptoclaw PR #649](https://github.com/qhkm/zeptoclaw/pull/649)

No feature work, bug fixes, or user-facing changes were merged today.

**4. Community Hot Topics**
No issues or PRs received comments or reactions in the last 24 hours. The only active PR (#649) has zero comments and zero thumbs-up. Community engagement is currently nil.

**5. Bugs & Stability**
No new bugs, crashes, or regressions were reported in the last 24 hours. No stability issues are flagged in the data.

**6. Feature Requests & Roadmap Signals**
No feature requests were raised today. The only signals are technical: automated dependency bumps indicate a focus on keeping the Docker build environment updated. There is no evidence of planned user-facing features or roadmap changes.

**7. User Feedback Summary**
No user feedback (comments, reactions, or issue descriptions) was recorded today. Pain points, use cases, or satisfaction levels cannot be inferred from this sample.

**8. Backlog Watch**
No long-unanswered issues or PRs were identified. The only open PR (#649) was created yesterday (2026-07-28) and has not yet received human maintainer review. No stale or abandoned items are present in today’s data.  
GitHub: [qhkm/zeptoclaw PR #649](https://github.com/qhkm/zeptoclaw/pull/649)

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for 2026-07-29.

---

## ZeroClaw Project Digest
**Date:** 2026-07-29

### 1. Today's Overview
ZeroClaw is in an exceptionally high-velocity development cycle. The repository shows intense activity with 49 Issues and 50 PRs updated in the last 24 hours. A significant portion of this activity is focused on security (secret management, credential handling), platform stability (CI fixes, crash prevention), and architecture (moving to runtime plugins). The project is currently managing a heavy load of high-risk ("risk:high") items, indicating a focus on hardening the codebase. While no new releases were cut today, the volume of accepted and in-progress patches suggests a major release candidate is being assembled.

### 2. Releases
**None.** No new releases were published in the last 24 hours.

### 3. Project Progress
The following PRs were **merged or closed** today, representing tangible progress:
- **Runtime Stability:** A fix for a flaky assertion that poisoned a global mutex during runtime tests ([#9357](https://zeroclaw-labs/zeroclaw Issue #9357)).
- **Authentication:** A critical fix for a breaking change where the `auth profile store` failed to load due to a missing data-field migration (`model_provider` vs `provider`) ([#9474](https://zeroclaw-labs/zeroclaw Issue #9474)).
- **Plugin System:** A fix for vendored `wit/v0` drift that caused silent plugin registration failures ([#9380](https://zeroclaw-labs/zeroclaw Issue #9380)).
- **Housekeeping:** A task to retire a dormant cron test module that was bloating the test suite ([#9471](https://zeroclaw-labs/zeroclaw Issue #9471)).

### 4. Community Hot Topics
The most active discussions revolve around **security architecture and runtime extensions**:
- **[#9127](https://zeroclaw-labs/zeroclaw Issue #9127) - RFC: Abstract a `KeySource` trait (8 comments):** This is a core design discussion on how ZeroClaw classifies and manages master-key material. The community is deeply engaged in defining a clean abstraction for "where does a key come from?" (filesystem, HSM, env var), indicating a push towards enterprise-grade secret management.
- **[#6157](https://zeroclaw-labs/zeroclaw Issue #6157) - Nextcloud Talk Bot API Bug (6 comments):** A persistent bug where the bot uses the wrong API endpoint. The long thread suggests the fix is non-trivial or has been deferred, despite being known for months.
- **[#9357](https://zeroclaw-labs/zeroclaw Issue #9357) - Flaky Runtime Test & Poisened Mutex (6 comments):** High heat on this bug because it is blocking the CI pipeline for all developers. The discussion centers on test isolation and Rust's global state.
- **[#8654](https://zeroclaw-labs/zeroclaw Issue #8654) - Skill-Review Fork Panic / SIGSEGV (5 comments):** A runtime crash that kills the entire agent process. Discussions are analyzing how a background skill-review fork can panic and take down the main daemon, suggesting a need for more robust process isolation.

### 5. Bugs & Stability
Several high-severity bugs were reported today:
- **Critical (P1):**
    - **[#9492](https://zeroclaw-labs/zeroclaw Issue #9492) - `auth refresh` dead-ends:** An external client (Codex CLI) can rotate the OAuth refresh token, leaving ZeroClaw with a stale token and no recovery path. **Status: Open, no fix PR yet.**
    - **[#9465](https://zeroclaw-labs/zeroclaw Issue #9465) - Telegram channel pre-check fails silently:** When the reply-intent pre-check declines a message, the bot adds a reaction but sends no text, making it look broken to users. **Status: In Progress.**
- **High (P2):**
    - **[#9486](https://zeroclaw-labs/zeroclaw Issue #9486) - High-entropy detector incorrectly redacts Solana addresses:** The `high_entropy_tokens=false` config is ignored on the channel path, blocking legitimate crypto transactions. **Status: Accepted.**
    - **[#9462](https://zeroclaw-labs/zeroclaw Issue #9462) - Plugin unit tests never execute in CI:** A significant CI gap where tests behind a feature flag are never run, risking broken WASM plugin support. **Status: Accepted.**

Existing Bugs with New Fix PRs:
- **[#9284](https://zeroclaw-labs/zeroclaw Issue #9284) - Config flush overwrites concurrent writes:** **PR [#9519](https://zeroclaw-labs/zeroclaw PR #9519)** is now open to serialize config writes and prevent data loss.
- **[#6724](https://zeroclaw-labs/zeroclaw Issue #6724) - Signal/Voice Call crashloop:** **PR [#9524](https://zeroclaw-labs/zeroclaw PR #9524)** addresses this by skipping channels with empty credentials at startup.

### 6. Feature Requests & Roadmap Signals
The project is clearly pivoting towards a **plugins-first architecture**.
- **Runtime Plugins ([#8850](https://zeroclaw-labs/zeroclaw Issue #8850)):** The ambitious plan to move optional channels/tools from compile-time features to WASM plugins is active. This will be a defining feature of the next major release, reducing binary size and enabling extension without recompilation.
- **Unified Attachment Architecture ([#9488](https://zeroclaw-labs/zeroclaw Issue #9488)):** A proposal to standardize how file attachments are handled across web chat and all channels. This is likely a prerequisite for the next version's rich-media capabilities.
- **Runtime-Owned Sessions ([#9487](https://zeroclaw-labs/zeroclaw Issue #9487)):** A major architectural RFC proposing that the **runtime** become the sole owner of sessions, with channels becoming "thin" transport adapters. This would standardize how the dashboard, WebSocket, and ACP adapters interact.
- **MCP Image Content ([#9521](https://zeroclaw-labs/zeroclaw Issue #9521)):** Users are requesting MCP tools to return image data into the vision pipeline, hinting at a future where ZeroClaw can natively handle image-based tools.

### 7. User Feedback Summary
Real user pain points are evident in the bug reports:
- **Frustration with Silent Failures:** Users on Telegram are reporting that the agent appears "broken" when a message is silently ignored rather than acknowledged (Issue [#9465](https://zeroclaw-labs/zeroclaw Issue #9465)).
- **Loss of Functionality:** A user with a Solana MCP server is blocked from using core crypto wallet features because of incorrect redaction logic on the Telegram channel (Issue [#9486](https://zeroclaw-labs/zeroclaw Issue #9486)).
- **Authentication Blockers:** Users are experiencing blocked workflows where simply running `auth` commands fails due to a broken migration path (Issue [#9474](https://zeroclaw-labs/zeroclaw Issue #9474)).
- **Satisfaction Signals:** The volume of RFCs from the community (e.g., [#9487](https://zeroclaw-labs/zeroclaw Issue #9487), [#9488](https://zeroclaw-labs/zeroclaw Issue #9488)) suggests high engagement from power users who are actively shaping the architecture of the next major version.

### 8. Backlog Watch
The following high-priority items have been open for a significant time and require maintainer decision or action:
- **[#6724](https://zeroclaw-labs/zeroclaw Issue #6724) - Signal/Voice Channel Crashloop (Open since May 16):** A P3 bug that can crashloop the supervisor. While a PR exists ([#9524](https://zeroclaw-labs/zeroclaw PR #9524)), it has been open for over two months.
- **[#6157](https://zeroclaw-labs/zeroclaw Issue #6157) - Nextcloud Talk API Bug (Open since April 27):** A P2 bug with an accepted status but no merged fix.
- **[#7904](https://zeroclaw-labs/zeroclaw Issue #7904) - SKILL.md frontmatter broken (Open since June 17):** A feature regression where skills cannot force-inject their prompts. A fix PR ([#9520](https://zeroclaw-labs/zeroclaw PR #9520)) was just opened, but the delay signals a potential blind spot in skill management testing.
- **[#8692](https://zeroclaw-labs/zeroclaw Issue #8692) - Maintainer Decision Queue Tracker:** This meta-issue itself is a signal that the project is struggling to keep up with the volume of design decisions, indicating a need for more maintainer bandwidth or a streamlined RFC process.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*