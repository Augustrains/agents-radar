# OpenClaw Ecosystem Digest 2026-08-01

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-01 01:27 UTC

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

Based on the GitHub data for OpenClaw (github.com/openclaw/openclaw) on 2026-08-01, here is the project digest:

---

### 1. Today's Overview

OpenClaw shows a very high level of activity with 500 issues and 500 PRs updated in the last 24 hours, indicating a heavily used and actively developed project. The majority of new work is focused on bug fixing and stabilization, with a significant number of issues still open and awaiting triage or review (443/500 open). No new releases were published today. The most discussed topics center on a critical, systemic problem: **message loss and delivery failures across multiple channels**. This suggests the team is currently in a "hardening" phase, addressing regressions and reliability issues rather than shipping new features.

### 2. Releases

No new releases were published today (2026-08-01).

### 3. Project Progress

While no PRs were merged or closed, 133 PRs were updated and closed today. The PRs indicate significant ongoing work toward codebase consolidation and improved system resilience. Key areas of progress appear to be:

- **Refactoring Initiatives**: A series of large refactors by contributor `steipete` are in progress, aiming to consolidate "messaging delivery," "session and channel regression fixtures," "plugin descriptors," "slash command ownership," and "turn lifecycle state ownership." These PRs (#114464, #114459, #117146, #117143, #117145) seem focused on reducing duplication and improving test coverage, which is a sign of a maturing codebase.
- **Channel-Specific Reliability Fixes**:
    - **Matrix**: A PR (#110568) aims to fix message loss by journaling inbound events before advancing sync tokens, and another (#117008) focuses on recovering durable sends after response loss.
    - **Slack**: A fix (#117135) is proposed to preserve durable retries for thread-history failures.
    - **Telegram**: A PR (#116149) fixes an issue where inline buttons ignored configured chat-kind limits.
- **Performance and Core Logic**:
    - A performance PR (#115138) proposes memory-mapping SQLite reads to prevent event-loop blocking.
    - A fix (#117072) aims to preserve approved exec continuation output, addressing a long-standing bug.
    - A security-related PR (#116957) seeks to redact sensitive authentication parameters (e.g., `x-api-key`, `sig`) from URLs and logs.

### 4. Community Hot Topics

The most active issues reflect major user pain points around session reliability and security.

- **Session State & Security (Security)**: [#10659 - Feature Request: Masked Secrets - Prevent Agent from Accessing Raw API Keys](https://github.com/openclaw/openclaw/issues/10659) (15 comments, 4 👍). Users are deeply concerned about security and want to prevent the agent from accessing raw secrets to mitigate prompt injection risks. This is a top-priority request with a `needs-security-review` label.
- **Message Loss & Duplicate Delivery (Stability)**: [#86519 - Agent repeats identical replies 2-10x on Telegram after 5.20 update](https://github.com/openclaw/openclaw/issues/86519) (13 comments, 1 👍). A P1 regression causing duplicate replies is severely impacting Telegram users. The umbrella issue [#69208 - Umbrella: duplicate transcript, replay, and context assembly across channels](https://github.com/openclaw/openclaw/issues/69208) (12 comments) highlights that this is a broader systemic problem affecting all channels.
- **Session State & Crash Loops (Stability)**: [#115908 - Session transcript projection reconcile can livelock under sustained writes](https://github.com/openclaw/openclaw/issues/115908) (11 comments). This critical P1 issue can block the main Node.js thread, stalling all channel transports.
- **Session State & Message Loss (Stability)**: [#114137 - Visible channel turns intermittently dispatch with no queued reply payloads](https://github.com/openclaw/openclaw/issues/114137) (11 comments). A P1 regression where final replies are persisted but never delivered.
- **Core Bug (Bizarre/User Trust)**: [#51429 - [Bug]: 看起来有人把工作路径hardcode进代码里而且居然被合并发布了](https://github.com/openclaw/openclaw/issues/51429) (13 comments). An alarming report of an apparent developer's hardcoded working path being merged into production, creating incorrect directories for users. This undermines user trust in the project's quality control.

### 5. Bugs & Stability

The project is facing several P0/P1 stability issues, primarily around session state and message delivery.

- **P0 - Startup Migration Block** ([#112395](https://github.com/openclaw/openclaw/issues/112395)): A regression where upgrading from 6.11 to 7.1 leaves the gateway blocked, unable to start. Labeled as a `ux-release-blocker`. No fix PR is linked.
- **P0 - Persistent Provider Cooldown** ([#70903](https://github.com/openclaw/openclaw/issues/70903)): An auth-provider issue where a cooldown persists across restarts, blocking users "for hours" even after a billing issue is resolved. Also a `ux-release-blocker`.
- **P1 - Session Livelock & Event Loop Blocking** ([#115908](https://github.com/openclaw/openclaw/issues/115908)): A core reliability issue causing a crash-loop for the entire gateway. No fix PR is linked.
- **P1 - Widespread Message Loss** ([#114137](https://github.com/openclaw/openclaw/issues/114137), [#85251](https://github.com/openclaw/openclaw/issues/85251), [#109490](https://github.com/openclaw/openclaw/issues/109490)): Multiple issues across different channels (Signal, Codex, Telegram) report the same core issue: the agent generates a reply, persists it, but fails to deliver it. This is the most critical and widespread problem.
- **P1 - Duplicate Replies Regression** ([#86519](https://github.com/openclaw/openclaw/issues/86519)): A confirmed regression in Telegram causing duplicate messages. A related fix for an all-channel duplicate write issue was closed today ( [#116409](https://github.com/openclaw/openclaw/issues/116409) ).

While many fixes are in flight (e.g., #116486, #117008, #117135), many critical issues still lack a linked fix PR, though they are often waiting on maintainer or product decisions.

### 6. Feature Requests & Roadmap Signals

Several feature requests with high user engagement signal a desire for a more polished, secure, and scalable product.

- **Security Enhancements**: High demand for a "masked secrets" system (#10659) and per-agent tool settings (#37584) to enhance security and multi-agent management. These are strong candidates for future releases.
- **SDK Stabilization**: A request to expose a stable Plugin SDK surface (#81913) suggests the project is preparing for a larger third-party ecosystem. This indicates a roadmap focus on extensibility.
- **Model Flexibility**: Requests for fully dynamic model discovery (#10687) and per-model usage logging (#13219) point to a desire for more control over and insight into model provider options and costs.
- **Multi-Agent & Browser Isolation**: A request for per-agent isolated browser instances with proxy support (#37487) indicates a push towards supporting more complex, parallel workflows that require strict separation.

These requests, particularly around security and extensibility, are likely strong candidates for the next version.

### 7. User Feedback Summary

User sentiment seems to be a mix of frustration with stability and enthusiasm for the project's potential.

- **Frustration**: The most dominant pain point is **message loss and unreliability**, particularly in Telegram and Slack. Users are also frustrated by the "hardcoded path" bug and a regression causing duplicate replies.
- **Security Concerns**: The high upvote count on the "Masked Secrets" issue indicates users are actively thinking about security and want a more robust system to protect their credentials from accidental leaks and prompt injection.
- **Enthusiasm for Features**: Users are requesting advanced features like dynamic model discovery, per-agent browser isolation, and a stable plugin SDK, showing they are pushing the platform to its limits and envisioning advanced use cases.

### 8. Backlog Watch

These important issues require maintainer attention and have been open for a significant or critical duration:

- **P0: Persistent file-based provider cooldown** ([#70903](https://github.com/openclaw/openclaw/issues/70903)): Open since April 24, this issue is a `ux-release-blocker` and shows a lack of responsiveness to a critical business-user-facing bug. It's marked `needs-maintainer-review`.
- **P0: Startup migration preflight blocks gateway** ([#112395](https://github.com/openclaw/openclaw/issues/112395)): Open since July 21, this blocks upgrades entirely and is also a `ux-release-blocker`. It has a linked PR but is still open, suggesting the fix may not be ready or merged.
- **P1: Core session management issues**: Issues like [#115908](https://github.com/openclaw/openclaw/issues/115908) (livelock), [#85251](https://github.com/openclaw/openclaw/issues/85251) (wedged Codex turns), and [#114211](https://github.com/openclaw/openclaw/issues/114211) (Matrix loops) are core stability problems that have been open for days to weeks, highlighting the backlog of critical bugs that are pending review or product decisions.
- **Stale Issues**: Many P1/P2 issues are marked as `stale` (e.g., [#53540](https://github.com/openclaw/openclaw/issues/53540), [#48238](https://github.com/openclaw/openclaw/issues/48238), [#47979](https://github.com/openclaw/openclaw/issues/47979)), indicating they might have lost priority.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Report: Personal AI Assistant & Agent Frameworks
**Date:** 2026-08-01 | **Prepared by:** Senior Analyst

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is currently in a **maturation and hardening phase**, characterized by distinct trajectories: while the largest projects (OpenClaw, IronClaw, ZeroClaw) are consolidating architectures and fixing systemic reliability issues, mid-tier projects (NanoBot, CoPaw, NanoClaw) are shipping rapid feature iterations with responsive maintainers. A **critical cross-cutting theme** dominates all major projects: **message delivery reliability and session-state integrity** — OpenClaw, Hermes Agent, and CoPaw all report P0/P1 bugs in this domain, indicating foundational infrastructure challenges that transcend individual implementations. Meanwhile, a **security hardening wave** is sweeping the ecosystem: NanoClaw, ZeroClaw, and Moltis each shipped or prepared security-critical fixes (secret redaction, fail-closed webhooks, signature verification). The market is also bifurcating between **Docker-centric architectures** (NanoClaw) and **runtime-agnostic designs** (IronClaw, ZeroClaw), with multi-user isolation emerging as a universal concern.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | PRs Merged/Closed | Releases | Health Score (1-10) |
|---------|----------------------|--------------------|--------------------|----------|---------------------|
| **OpenClaw** (openclaw) | 500 | 500 | 0 merged / 133 closed | None | 5.5 — High volume, stability crises |
| **IronClaw** (nearai) | 31 | 50 | 32 merged | None | 7.5 — Healthy velocity, focused refactor |
| **ZeroClaw** (zeroclaw-labs) | 50 | 50 | 0 merged (all open) | None | 5.0 — Heavy RFC backlog, decision bottleneck |
| **Hermes Agent** (nousresearch) | 50 | 50 | 0 merged / 0 closed | None | 5.0 — High activity, no PRs landing |
| **CoPaw** (agentscope-ai) | 20 | 43 | 13 merged | None | 7.0 — Strong contributor pipeline |
| **LobsterAI** (netease-youdao) | 4 (closed) | 12 | 11 merged | None | 7.5 — Stable, polished releases |
| **NanoBot** (HKUDS) | 4 | 16 | 6 merged | None | 8.0 — Excellent turnaround, responsive |
| **NanoClaw** (qwibitai) | 8 | 9 | 3 merged | None | 7.5 — Steady, security-focused |
| **Moltis** (moltis-org) | 2 | 6 | 2 merged | None | 7.0 — Feature-forward, security PRs pending |
| **PicoClaw** (sipeed) | 2 | 3 | 0 merged | None | 6.5 — Quiet but active contributions |
| **NullClaw** (nullclaw) | 0 | 1 | 0 merged | None | 7.0 — Stable, minimal debt |
| **TinyClaw** (TinyAGI) | 0 | 0 | 0 | None | N/A — No activity |
| **ZeptoClaw** (qhkm) | 0 | 0 | 0 | None | N/A — No activity |

---

## 3. OpenClaw's Position

**Advantages vs Peers:**
- **Reference implementation status**: With 500 issues + 500 PRs updated daily, OpenClaw is the ecosystem's most-used platform, likely the direct or indirect codebase ancestor of multiple peers (NanoClaw, PicoClaw, ZeroClaw naming/architecture echoes).
- **Massive community**: The scale of community engagement (bug reports like #86519 with real user impact) indicates production usage across Telegram, Slack, Matrix, Signal — a breadth no other project matches.
- **Active refactoring toward reliability**: The `steipete` branch of PRs (#114464, #114459, etc.) demonstrates architectural consolidation (plugin descriptors, turn lifecycle state ownership) that will pay dividends once the stability crisis resolves.

**Technical Approach Differences:**
- OpenClaw's **channel-first design** (30+ channel adapters) puts it in a different class than NanoBot (WeChat/Slack-focused), PicoClaw (IRC/DeltaChat/Simplex), or NanoClaw (Telegram/iMessage/Dial). This breadth creates unique systemic challenges — the umbrella issue #69208 (duplicate transcript, replay, context assembly across channels) has no equivalent in narrower projects.
- **SQLite-mapped / memory-mapped I/O** (PR #115138) and **journalling inbound events** (PR #110568) represent a deliberate investment in data integrity patterns.

**Community Size Comparison:**
OpenClaw's issue/PR volume exceeds **all other projects combined by ~10x**. IronClaw (50 PRs) and ZeroClaw (50 issues/PRs) are the closest competitors in engagement, but remain significantly smaller. OpenClaw's community is also **more diverse linguistically** (Chinese-language issue #51429, global user base), reinforcing its position as the ecosystem's central hub.

---

## 4. Shared Technical Focus Areas

The following requirements emerged independently across multiple projects — they represent **market consensus priorities** for developers building on this ecosystem:

| Requirement | Projects | Specific Signals |
|-------------|----------|------------------|
| **Session/message delivery integrity** | OpenClaw, Hermes, CoPaw, IronClaw | OpenClaw #114137 (message loss P1); Hermes #72776 (workspace hijack P1); CoPaw #6601 (empty responses); IronClaw #6900 (memory leak P0) |
| **Security hardening / secret management** | OpenClaw, ZeroClaw, NanoClaw, Moltis | OpenClaw #10659 (masked secrets); ZeroClaw #9569 (fail-closed webhooks); NanoClaw #3161 (log redaction); Moltis #1179/#1180 (signature verification, path hardening) |
| **Multi-user isolation** | OpenClaw, IronClaw, ZeroClaw | IronClaw #6866 (shared home dir), #6778 (MCP catalog exposure); ZeroClaw #9487 (runtime as session owner); OpenClaw #10659 (agent credential isolation) |
| **Provider/model flexibility** | OpenClaw, NanoBot, ZeroClaw, LobsterAI | NanoBot #5197 (DeepSeek Responses API); ZeroClaw #8550 (OpenAI-compatible endpoint); LobsterAI #2413/#2415 (DeepSeek prefix cache optimization); NullClaw #981 (grok-cli provider) |
| **Container/runtime portability** | IronClaw, NanoClaw, ZeroClaw | NanoClaw #1184 (K8s), #1732 (native mode); ZeroClaw #9487 (runtime as central owner); IronClaw "Reborn" refactor |
| **Observability & tracing** | ZeroClaw, IronClaw, LobsterAI | ZeroClaw #8933 (cross-turn correlation); IronClaw #6524 (hermetic testing); LobsterAI #2413 (cache hit rate monitoring) |
| **Agent-to-agent workflows** | ZeroClaw, CoPaw, LobsterAI | ZeroClaw #9106 (A2A outbound client); CoPaw #6602 (subagent task tracking); LobsterAI #2234 (cron descendant finalization) |
| **Memory/context management** | OpenClaw, Hermes, CoPaw, ZeroClaw | OpenClaw #69208 (context assembly); Hermes #52261 (compress/reset loop); CoPaw #6601 (context overflow silent failure); ZeroClaw #9048 (separate history from memory) |

---

## 5. Differentiation Analysis

| Project | Core Focus | Target Users | Architectural Distinction |
|---------|-----------|--------------|--------------------------|
| **OpenClaw** | Universal multi-channel gateway | Developers, creators, teams | 30+ channels, plugin SDK roadmap (#81913), massive community |
| **IronClaw** | Enterprise-grade agent runtime | Serious developers, multi-user deployments | Contract extraction (clean interfaces), deterministic testing (#6524), security isolation |
| **ZeroClaw** | Secure, extensible agent with RFC-driven governance | Security-conscious power users | Runtime as central owner, fail-closed security, DAG-planning tools |
| **Hermes Agent** | Local-first, cross-platform desktop agent | Individual users on desktop (Win/mac/Linux) | Desktop Tauri app, local MLX inference support, profile routing |
| **NanoBot** | Lightweight channel-focused agent | WeChat/Slack/Telegram users | JSONL→SQLite migration, session management, WebUI |
| **CoPaw** | Chinese-market, chat-centric agent | East Asian users (Heavy Feishu/WeChat/QQ) | AgentScope integration, workspace access, Desktop app |
| **NanoClaw** | Minimalist Docker-first agent | Privacy-focused individuals, self-hosters | Container isolation default, runtime-agnostic roadmap |
| **LobsterAI** | OpenClaw-adjacent dashboard + agent | Teams seeking polished UI + agent runtime | Cowork dashboard, agent orchestration, release-pinned cadence |
| **PicoClaw** | Multi-protocol, maker/hobbyist agent | IRC/DeltaChat/Simplex communities | Lightweight, protocol expansion focus |
| **Moltis** | Human-AI collaboration platforms | Nostr/self-hosted communities | NIP-29 group chat, vector memory backends |
| **NullClaw** | Minimal, CLI-driven provider shim | Power users with local CLIs | Spawn-per-request provider pattern |

---

## 6. Community Momentum & Maturity

### Tier 1 — Massively active, stabilizing (mature but under strain)
- **OpenClaw**: Highest raw engagement; team is in "hardening sprint" — consolidating refactors and channel reliability fixes will determine next release readiness. **Risk**: Review bottleneck (443/500 issues open) could erode contributor confidence.
- **IronClaw**: **Fastest-moving healthy project** — 32 PRs merged in 24h, Wave 1 of architectural refactor landing cleanly. Clearly executing against a roadmap (#6284 error-recoverability epic) with high maintainer responsiveness. **Rapidly iterating, not just fixing.**

### Tier 2 — Actively shipping (accelerating)
- **CoPaw**: Strong contributor pipeline, 13 PRs merged/closed, first-time contributors landing fixes. **Rapidly iterating.**
- **NanoBot**: Excellent turnaround (all critical bugs fixed within 24h); SQLite migration merged today. **On a roll.**
- **NanoClaw**: Steady architectural work (container abstraction) + security hardening. **Healthy momentum.**
- **LobsterAI**: Batch-merging polished UI/UX improvements; monthly release cadence observed. **Stabilizing with polish.**

### Tier 3 — Moderate/quiet (steady but not sprinting)
- **ZeroClaw**: High RFC volume but **decision bottleneck** — many proposals pending maintainer review since June. Risk of community attrition if RFC backlog isn't cleared.
- **Hermes Agent**: High submission volume but **zero PRs landed in 24h** — concerning review bottleneck for long-lived PRs (#62944, #71686).
- **Moltis**: Feature-forward (Markdown export, NIP-29) but critical security PRs (#1170, #1179, #1180) pending — needs faster security review turnaround.
- **PicoClaw**: Quiet; feature PRs (Simplex, fallback chains) waiting 4-5 weeks for review — **review lag risk**.
- **NullClaw**: Stable, minimal; single provider PR awaiting review.

### Tier 4 — Dormant
- **TinyClaw**, **ZeptoClaw**: No activity — likely stalled or on extended pause.

---

## 7. Trend Signals

### Signal 1: "Reliability is the new feature"
Across OpenClaw (message loss), Hermes (session corruption), CoPaw (silent failures), and IronClaw (memory leak), **session-state integrity** is the #1 blocker reported by real users. Projects investing in structural fixes (OpenClaw's journalling, NanoBot's SQLite migration, IronClaw's contract extraction) are positioning themselves for long-term trust advantage. **For developers:** prioritize durable message delivery and transactional session state over new channel features in your next iteration.

### Signal 2: "Security is becoming a competitive advantage"
NanoClaw, ZeroClaw, and Moltis shipped security-critical fixes in a single cycle. The community's demand for **masked secrets** (OpenClaw #10659), **fail-closed webhooks** (ZeroClaw #9569), and **verification of pairing signatures** (Moltis #1179) reflects a market where prompt-injection attacks and credential leaks are real, painful events. **For developers:** treat secret isolation and signature verification as non-negotiable launch requirements, not future hardening items.

### Signal 3: "Multi-user isolation is the next multi-tenant frontier"
IronClaw (#6866 shared home dir, #6778 MCP catalog exposure), OpenClaw (agent credential isolation), and ZeroClaw (#9487 runtime as session owner) independently wrestle with the same problem: **how to safely isolate state in an agent that spans multiple channels/users**. **For developers:** design for multi-tenant isolation from day one — retrofitting it later (as all these projects are doing) is costly.

### Signal 4: "Model provider flexibility is table stakes"
From DeepSeek Responses API (NanoBot) to grok-cli (NullClaw) to MiniMax/StepFun backends (Hermes), **users want to bring their own model**. LobsterAI's cache-hit optimization (#2413) reveals that cost is a driving factor. **For developers:** abstract model I/O (provider-agnostic interfaces) and optimize for token efficiency — cache-stable prompts are a differentiator.

### Signal 5: "Container abstraction is required, not optional"
NanoClaw's Kubernetes/native mode push and IronClaw's runtime-agnostic contract extraction both respond to the same reality: **Docker is not universal**. Users need to run agents on laptops without Docker, inside managed K8s, and on Apple Silicon microVMs. **For developers:** support at least one non-Docker execution path (native, microVM, or remote) or risk a shrinking addressable market.

### Signal 6: "Observability and deterministic testing are maturing"
ZeroClaw's OTel/Langfuse integration (#8933) and IronClaw's hermetic testing epic (#6524) signal that the ecosystem is moving beyond "does it work?" to "can we trust it works, and why?" **For developers:** invest in structured logs, trace correlation IDs, and deterministic replay tests — they are becoming table stakes for production deployments.

### Signal 7: "Agent-to-agent and goal-oriented autonomy is the horizon"
ZeroClaw's A2A outbound client (#9106), CoPaw's subagent lifecycle management (#6602), and LobsterAI's cron descendant finalization (#2234) all point toward **orchestrated multi-agent workflows** as the next capability layer. **For developers:** design skills and tools to be callable by other agents, not just interactive sessions.

---

**Bottom line for technical decision-makers:** The ecosystem is consolidating around three axes — **reliability**, **security**, and **portability**. Projects that land structural fixes (IronClaw, NanoBot) are racing ahead; projects stuck in review bottlenecks (OpenClaw fixes pending, Hermes zero-merge day, ZeroClaw RFC backlog) risk community defection to more responsive alternatives. Select your foundation based on **merge velocity**, **security posture**, and **multi-user isolation maturity** — not just feature breadth.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date:** 2026-08-01

---

## 1. Today's Overview

NanoBot is exhibiting **high-velocity development activity** with 16 PRs updated in the last 24 hours (10 open, 6 merged/closed) and 4 issues updated (2 open, 2 closed). The project shows strong maintainer engagement, with rapid triage and fixes landing for critical issues such as the WeChat channel session recovery and Termux configuration failure. A major architectural milestone — migrating session storage from JSONL to SQLite — was merged today, alongside a steady stream of quality-of-life fixes across the WebUI, Slack channel, and CLI. No new releases were published, but the volume of merged patches suggests an imminent release candidate. Overall, project health appears **robust**, with an active contributor base and responsive issue management.

---

## 2. Releases

**No new releases published today.**

---

## 3. Project Progress

**Major Merged PRs:**

- **[#5173 — feat(session): migrate session storage from JSONL to SQLite**](https://github.com/HKUDS/nanobot/pull/5173) *(merged)* — A significant architectural change making `sessions.db` the sole runtime session store. Transactions migrate canonical `<workspace>/sessions/*.jsonl` files on first startup, with JSONL retained as rollback backups. This improves performance and integrity for session management.

- **[#5189 — fix(config): install timezone data on all platforms**](https://github.com/HKUDS/nanobot/pull/5189) *(merged)* — Resolves the Termux issue (#5187) by installing `tzdata` as a fallback on all platforms, including minimal Linux hosts without a system timezone database.

- **[#5192 — fix(slack): scope channel thread openers to their own session**](https://github.com/HKUDS/nanobot/pull/5192) *(merged)* — Fixes a bug where top-level channel messages opening a Slack thread shared a channel-wide session, causing unrelated threads to see each other's opening turns.

- **[#5193 — fix(webui): preserve user scroll ownership near tail**](https://github.com/HKUDS/nanobot/pull/5193) *(merged)* — Improves WebUI thread scroll UX by keeping camera ownership with the user when scrolling near the bottom, preventing jarring auto-scroll behavior.

- **[#5196 — fix(weixin): recover refreshed state after session expiry**](https://github.com/HKUDS/nanobot/pull/5196) *(merged)* — Fixes bug #5195: reloads persisted Weixin state after a session pause when `account.json` has been refreshed, preventing permanent silent failure.

- **[#4223 — fix(weixin): reload session state after pause expiry**](https://github.com/HKUDS/nanobot/pull/4223) *(merged)* — An older PR (from June) resolved in parallel with #5196, fixing the same root cause: `_poll_once()` not reloading state after pause, leading to a death loop on expired tokens.

**Notable Open PRs (in progress):**
- [#5197](https://github.com/HKUDS/nanobot/pull/5197) — DeepSeek Responses API support (new provider feature)
- [#5194](https://github.com/HKUDS/nanobot/pull/5194) — WebUI JSONL session list performance optimization
- [#5200](https://github.com/HKUDS/nanobot/pull/5200) — Preserve exec `wait_for` targets across response truncation
- [#5201](https://github.com/HKUDS/nanobot/pull/5201) — Tolerate malformed persisted session summaries

---

## 4. Community Hot Topics

- **[Issue #5195 — WeChat QR re-scan overwrites token (2 comments)**](https://github.com/HKUDS/nanobot/issues/5195)
  The most active issue today, highlighting a painful UX problem: re-scanning a QR code in the WebUI to re-login WeChat results in an immediate session-expired error and a 60-minute forced pause. This bug affects real users relying on the WeChat channel for daily operations. **Fixed by PRs #5196 and #4223** (both merged).

- **[Issue #5198 — Cannot change models in a session without reconfiguring**](https://github.com/HKUDS/nanobot/issues/5198)
  A user expresses frustration that the model blip near the chat input is non-interactive and the `/model` command appears non-functional. This reflects a usability gap compared to commercial Cloud AI interfaces. No fix PR yet; likely a candidate for the next release.

- **PR #5184 — Quick Chat and Temporary Chat (WebUI feature)** — Active interest in improving the WebUI conversational experience with persistent quick-access and ephemeral temporary chat modes, indicating a demand for more flexible interaction patterns.

---

## 5. Bugs & Stability

| Severity | Issue | Status | Notes |
|----------|-------|--------|-------|
| **High** | [#5195 — WeChat QR re-scan session expiry loop](https://github.com/HKUDS/nanobot/issues/5195) | Closed | Fixed by #5196 & #4223. Caused 60-min service pauses; permanent silent failure without fix. |
| **Medium** | [#5187 — Termux failure: timezone validation error](https://github.com/HKUDS/nanobot/issues/5187) | Closed | Fixed by #5189 (`tzdata` fallback on all platforms). Blocks NanoBot on minimal Linux environments. |
| **Medium** | [#5190 — MIME type "text/plain" blocks JS module loading](https://github.com/HKUDS/nanobot/issues/5190) | Open | Windows-specific registry issue. Fix PR #5191 open — registers correct MIME types for static assets on Windows. |
| **Low** | [#5198 — Model switching in session not working](https://github.com/HKUDS/nanobot/issues/5198) | Open | Usability discrepancy; no PR yet. |

All high-severity bugs have been addressed within 24 hours, demonstrating excellent turnaround.

---

## 6. Feature Requests & Roadmap Signals

- **DeepSeek Responses API support** ([PR #5197](https://github.com/HKUDS/nanobot/pull/5197)) — Routing the `deepseek-v4-flash` model through DeepSeek's native Responses API while keeping others on Chat Completions. Signals continued investment in multi-provider support.

- **Quick Chat & Temporary Chat in WebUI** ([PR #5184](https://github.com/HKUDS/nanobot/pull/5184)) — Persistent quick-access chat plus opt-in ephemeral temporary chat with in-memory history. Reflects user desire for more WebUI flexibility.

- **Interactive model switching** (implied by Issue #5198) — Users expect the same click-to-switch-model behavior as cloud SaaS tools. Likely to be addressed soon given the visibility of the issue.

- **Session export/import/search commands** ([PR #1565](https://github.com/HKUDS/nanobot/pull/1565)) — Long-pending (since March) but still open; would enhance data portability.

**Predictions for next release:** DeepSeek Responses API support, WebUI Quick Chat/Temporary Chat, and MIME type fix for Windows are strong candidates based on merge readiness and active maintainer attention.

---

## 7. User Feedback Summary

- **Pain Point — WeChat stability:** Users depend on the WeChat channel heavily; the session expiry death-loop (#5195) caused 60-minute service interruptions, described as "permanent silent" failure without manual intervention. Root cause is now fixed.

- **Pain Point — Model selection UX:** A user explicitly compared NanoBot unfavorably to commercial Cloud AI UIs, noting the inability to switch models mid-session. Feedback emphasizes that the `/model` command and blip UI are not discoverable or functional enough.

- **Pain Point — Environment portability:** The Termux issue (#5187) reflects broader demand for NanoBot to run on resource-constrained or non-standard environments. The maintainer fix (#5189) included the user's request for broader platform coverage.

- **Pain Point — Windows asset serving:** The MIME type issue (#5190) is platform-specific but blocks the entire frontend from loading, effectively rendering the WebUI unusable on affected Windows setups.

Overall sentiment leans **positive**: critical bugs are acknowledged and fixed quickly (often same-day), but users expect more polish in everyday interactions (model switching, scroll handling).

---

## 8. Backlog Watch

- **[PR #1656 — String validation None handling](https://github.com/HKUDS/nanobot/pull/1656)** — Open since **March 7, 2026**, flagged with `conflict`. Addresses a TypeError on `None` values in string schema validation. Needs conflict resolution and maintainer review.

- **[PR #1565 — Session export/import/search/stats](https://github.com/HKUDS/nanobot/pull/1565)** — Open since **March 5, 2026**, flagged with `conflict`. A comprehensive feature that would significantly improve data management. Requires rebase and maintainer assessment.

- **[PR #1319 — Skill status command](https://github.com/HKUDS/nanobot/pull/1319)** — Open since **February 28, 2026**, flagged with `conflict`. Diagnostic CLI command to help users identify skill misconfigurations. This would greatly improve the ClawHub skill installation experience.

- **Issue #5198 — Model switching** — Only 1 day old but trending; should be prioritized before it becomes stale.

These long-standing PRs all carry `conflict` flags, suggesting they need maintainer attention to resolve merge conflicts and integrate valuable functionality that has been waiting for up to 5 months.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-08-01

---

## 1. Today's Overview

Hermes Agent is showing **high activity with moderate engagement depth**. 50 issues and 50 PRs were updated in the last 24 hours, with 4 issues closed and **zero PRs merged or closed** — a potential bottleneck indicating review capacity may be strained despite the high submission volume. The issue tracker is dominated by **bug reports (approximately 60%)** versus feature requests, with a notable cluster of fresh bugs filed on July 31–August 1, 2026 targeting session-state integrity, profile routing, and Desktop application stability. While 46 open issues were touched, the most-engaged threads (12 and 6 comments) are long-standing architectural or high-severity items, suggesting community energy is focused on a few persistent problems rather than broadly distributed. The PR queue shows substantial technical debt: several large, long-lived PRs (e.g., #62944, #71686) remain open for weeks, and the top PRs span critical fixes for state corruption, security boundary leaks, and memory leaks. The presence of multiple PRs with overlapping fixes for similar session-state risks suggests possible duplication of effort. No maintainer responses were recorded in the data, which is a concern given the volume of issues, especially those flagged as P1.

---

## 2. Releases

**No new releases published in the last 24 hours.** The most recent update mentioned in issues is v0.19.1 (referenced as causing a regression where local patches were wiped during autostash — see #75763).

---

## 3. Project Progress

**No PRs were merged or closed in the last 24 hours.** All 50 updated PRs remain open. This is a significant signal: despite a healthy pipeline of fixes and features, nothing is landing, which could indicate a maintainer review bottleneck. Key fixes waiting in the queue include:

- **[#73639](https://github.com/NousResearch/hermes-agent/pull/73639)** — Fix FTS UPDATE triggers causing disk I/O saturation and wedged gateways during session status updates.
- **[#75765](https://github.com/NousResearch/hermes-agent/pull/75765)** — Replace faulty inline regex for stripping thinking blocks from max-iterations summaries, fixing leaked XML in open models (GLM).
- **[#75763](https://github.com/NousResearch/hermes-agent/pull/75763)** — Reapply four local fixes (writer-connection race, cursor invalidation, handoff/compression reads) that the 0.19.1 autostash dropped from user installs; adds regression tests.
- **[#75760](https://github.com/NousResearch/hermes-agent/pull/75760)** — Bound and persist large tool results consistently across execution paths to prevent provider 400s.
- **[#75758](https://github.com/NousResearch/hermes-agent/pull/75758)** — Refactor: extract per-provider credential refresh into a mixin to simplify the 6,790-line `AIAgent` class.
- **[#75764](https://github.com/NousResearch/hermes-agent/pull/75764)** — Add MiniMax image-01 and StepFun step-image-edit-2 image generation backends.
- **[#75759](https://github.com/NousResearch/hermes-agent/pull/75759)** — Enable prompt_toolkit mouse support via new `display.mouse_support` config (default True).

---

## 4. Community Hot Topics

The most active discussions reveal deep operational concerns:

1. **[#64231 — Hook lifecycle-event catalog & taxonomy (12 comments)](https://github.com/NousResearch/hermes-agent/issues/64231)** — Maintainer (teknium1) proposes a systematic triage of a dozen pending observer-hook PRs against a formal lifecycle-event taxonomy, rather than merging ad-hoc `VALID_HOOKS` additions. This indicates a maintainer desire to impose architectural order on plugin extensibility, and signals that the plugin API surface area is a strategic focus.

2. **[#52261 — Local MLX/oMLX resource 400s misclassified as context_overflow (6 comments)](https://github.com/NousResearch/hermes-agent/issues/52261)** — A serious correctness bug: when OOM or resource errors from local inference are confused with context overflow, the agent enters a destructive compress/reset loop, corrupting session state. This is a P2 with a `sweeper:risk-session-state` label and is central to the reliability of local inference.

3. **[#72776 — Session workspace hijacked to unrelated git repo (5 comments)](https://github.com/NousResearch/hermes-agent/issues/72776)** — A P1 Desktop/CLI bug where a non-git workspace gets re-parented to a git directory it merely touches, breaking session isolation and prompting destructive resets.

4. **[#75737 — Per-subagent toolset restriction in delegate_task (4 comments)](https://github.com/NousResearch/hermes-agent/issues/75737)** — A feature request that was opened *and closed* on the same day (Aug 1). It highlights real token-bloat pain: subagents loading 21 toolsets for simple web research. The rapid closure (likely duplicate) may disappoint users hitting this issue.

5. **[#20717 — Dynamic Context Pruning (4 comments, 2 👍)](https://github.com/NousResearch/hermes-agent/issues/20717)** — A long-standing feature request (May 6) proposing proactive model-driven context management instead of the current reactive buffer-then-compress approach. It remains open with support.

---

## 5. Bugs & Stability

**P1 (highest):**
- **[#72776 — Session workspace hijacked to unrelated git repo](https://github.com/NousResearch/hermes-agent/issues/72776)** — Session state isolation breach on Windows; can trigger destructive reset loops. No fix PR yet.

**P2 (high severity):**
- **[#75598 — Issues with updates; conflicting multiple gateways/profiles](https://github.com/NousResearch/hermes-agent/issues/75598)** — After roughly a week of stability, updates began destabilizing the program with conflicting gateway instances across profiles. Platform: Windows.
- **[#75278 — Tauri updater handoff fails on macOS (PID mismatch)](https://github.com/NousResearch/hermes-agent/issues/75278)** — Perpetual "Hermes is still running" failure loop due to `HERMES_UPDATE_HANDOFF_PID` mismatch between Rust updater and Python update child.
- **[#75535 — /status shows configured default provider, not active fallback](https://github.com/NousResearch/hermes-agent/issues/75535)** — Misleading status/billing when on a fallback route; impacts cost visibility.
- **[#75684 — Multiplex /memory and /skills use default profile home, not routed profile](https://github.com/NousResearch/hermes-agent/issues/75684)** — Memory/skills write-approval surface disagrees with agent tools.
- **[#75756 — Desktop "Edit failed" / session not found on message rewind](https://github.com/NousResearch/hermes-agent/issues/75756)** — Urgent P2 (and user-flagged as "P1 / urgent"): editing an earlier message and resubmitting errors out; no rewind-and-rerun for the transcript.
- **[#73629 — Desktop Sessions list continuous flicker while scrolling (Win11)](https://github.com/NousResearch/hermes-agent/issues/73629)** — UI regression specific to Windows 11 (not Windows 10).
- **[#74169 — CLI crash on startup with voice.record_key alt combos](https://github.com/NousResearch/hermes-agent/issues/74169)** — `prompt_toolkit` rejects `a-v` key format.
- **[#75724 — Pre-update backup aborts on non-SQLite .db files](https://github.com/NousResearch/hermes-agent/issues/75724)** — Windows: `sqlite3.backup()` fails on unrelated `.db` cache files, aborting the entire pre-update backup.
- **[#75725 — MiniMax-M3 interleaved thinking stops after first tool-call turn](https://github.com/NousResearch/hermes-agent/issues/75725)** — Turn 2+ loses chain-of-thought.
- **[#75727 — New desktop sessions use localStorage-sticky model instead of profile default (closed as duplicate)](https://github.com/NousResearch/hermes-agent/issues/75727)** — 4 comments; closed.
- **[#75731 — Desktop: @file attachment rendered twice after history hydration](https://github.com/NousResearch/hermes-agent/issues/75731)** — Message display duplication.

**P3 (moderate):**
- **[#75708 — mem0 plugin ignores gateway_session_key for user_id scoping](https://github.com/NousResearch/hermes-agent/issues/75708)** — Privacy/scoping issue on API server path.
- **[#75694 / #75695 — "hermes made computer not work anymore"](https://github.com/NousResearch/hermes-agent/issues/75694)** — A bad `chown /home/ubuntu` during sftp setup broke hermes and the dashboard; user requested a failsafe. Pair of related issues.

**Fix PRs exist for:** session-state FTS triggers (#73639), cua-driver envelope normalization (#73007), xAI Invalid PNG recovery (#69104), wake-word `pypinyin` missing dependency (#74733), and memory leaks (#62934).

---

## 6. Feature Requests & Roadmap Signals

Strong signals for next-version priorities:

- **Plugin lifecycle standardization (#64231)** — Maintainer-driven; likely to land as a formal hooks taxonomy and triage of the pending PR cluster.
- **Per-subagent toolset restriction (#75737)** — High demand (token bloat), but closed as duplicate. The underlying need is real; watch for a consolidated issue.
- **Multiple simultaneous memory providers (#70390, PR)** — A long-lived PR (since Jul 23) with active revision history; likely to land soon.
- **Single gateway, multiple agents (#62944, #71686)** — Large stacked PRs (author jethac) that have been open for weeks; represents a major architectural feature push that is close to merge-ready.
- **Provider expansion — Gemini Vertex API key (#70663), MiniMax/StepFun image backends (#75764)** — Indicates focus on widening model/image support.
- **Dynamic Context Pruning (#20717)** — A recurring theme in user feedback; model-driven context management is a plausible roadmap item but lacks a clear owner.
- **Desktop UX polish — collapse thinking blocks (#69161), disable drag-chat (#70422)** — Smaller but high-visibility wins; likely candidates for next minor release.
- **CLI/Desktop input — mouse support (#75759)** — Minor feature, low risk, already PR-ready.

**Prediction:** The next version will likely include per-agent toolset restrictions, vertex API key auth, and the state-layer fixes. The "multiple agents per gateway" feature remains promising but has been waiting for a merge decision for over two weeks.

---

## 7. User Feedback Summary

- **Pain point: Update reliability is a top user concern.** Users report that updates (especially 0.19.1) are actively damaging configurations (patches dropped — #75763, backups aborting — #75724, updater handoff failures — #75278). Trust in the update channel is eroding; regression tests in the fix PRs are a positive step toward restoration.
- **Pain point: Session-state corruption is crippling for real users.** The P1 workspace-hijack bug (#72776), the local-inference compress/reset loop (#52261), and edit-rewind failures (#75756) all cause destructive data loss or workflow interruption. These are the most damaging experiences reported this period.
- **Positive signals:** Rapid issue closure on duplicate feature requests (#75737) and a focused bug (#75727) shows triage is moving, though with high volume (50 issues updated), response latencies are still long (e.g., #64231 from Jul 14).
- **Community engagement style:** The user base is technical, with detailed root-cause analyses (e.g., #75278, #74169, #75724). Many reports exceed the abstraction level of plain bug reports, effectively contributing early diagnostics to maintainers — a sign of a mature and invested community.
- **Gaps in feedback:** No positive feedback was recorded in this window. The dataset is entirely problem-focused (which is typical for issue trackers), but the absence of merged PRs or any appreciation/comments reinforce the perception that project health may be overshadowed by bug volume.

---

## 8. Backlog Watch

**Long-unanswered items needing maintainer attention:**

1. **[#7484 — Session fixation via predictable session ID derivation (P2, security, Apr 11, 3 comments)](https://github.com/NousResearch/hermes-agent/issues/7484)** — Over 3 months old, no maintainer reply. Security issue in the API server; deterministic SHA256 session IDs are trivially guessable.
2. **[#66084 — `_tui_need_npm_install()` compares against monorepo lockfile, not workspace (Jul 17, 3 comments)](https://github.com/NousResearch/hermes-agent/issues/66084)** — Causes npm reinstall on every dashboard start; flagged as duplicate but no resolution.
3. **[#43800 — Honcho plugin ignores endpoint.baseUrl in config, routes to production (Jun 10, 3 comments)](https://github.com/NousResearch/hermes-agent/issues/43800)** — A privacy/config bug in the memory plugin; unfixed for nearly 2 months.
4. **[#19128 — Add qwen3.6-flash, deepseek-v4-flash/pro to Alibaba provider (May 3, 4 comments)](https://github.com/NousResearch/hermes-agent/issues/19128)** — Simple model-list addition; stale since late May with no triage.
5. **[#64662 — llm_execution middleware cannot intentionally block provider execution (Jul 14, 2 comments)](https://github.com/NousResearch/hermes-agent/issues/64662)** — Plugin-facing capability gap; needs-decision label.
6. **[#71375 — Browser tab management (list, switch, close, auto-follow) (Jul 25, 2 comments)](https://github.com/NousResearch/hermes-agent/issues/71375)** — A UX feature request without response, despite being popular in the agent-browser space.
7. **[#62944 / #71686 — Single gateway multi-agent stack (Jul 12 / Jul 26, no comments)](https://github.com/NousResearch/hermes-agent/pull/62944)** — The biggest feature PRs by scope and complexity. Zero maintainer interaction in 20 days signals a serious review bottleneck that could become a community attrition risk, especially since the 0.19.1 update incidents increased urgency for other fixes.

---

*Digest generated from 50 issues and 50 PRs updated between 2026-07-31 and 2026-08-01 (UTC).*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-01

## 1. Today's Overview

PicoClaw is in a steady development phase with moderate activity across issues and pull requests. Over the last 24 hours, 2 issues were updated (both open) and 3 pull requests received updates (all open, none merged), indicating ongoing community contribution but a quiet period for direct merges. No new releases were published this cycle. The project continues to attract feature-driven contributions—particularly around channel protocol support (DeltaChat refactor, Simplex addition) and AI model configuration flexibility—while addressing user-facing quality concerns like CPU usage and messaging robustness. Overall, the project shows healthy community engagement with clear roadmaps toward protocol expansion and UX refinement.

## 2. Releases

No new releases were published during this period. The most recent version referenced in community reports is PicoClaw 0.3.1.

## 3. Project Progress

No pull requests were merged or closed within the last 24 hours. However, three open PRs remain active, representing significant feature development in flight:

- **#3222 (DeltaChat refactor):** A substantial cleanup reducing code by ~200 lines, dropping legacy features, removing hardcoded relay lists in favor of official references, and replacing password-based email config with JSON-RPC secrets. Also renames `invite_link` → `join_invite_link` and adds `show_invite_link`.
- **#3193 (Simplex channel support):** Adds a new channel type for Simplex messaging, expanding PicoClaw's multi-protocol reach.
- **#3200 (Configurable fallback chain):** Introduces a dedicated workflow on the models page, allowing users to set default models, add fallbacks, reorder, and persist via the backend API.

## 4. Community Hot Topics

The most active discussions this cycle are centered on usability and performance:

- **[Issue #3292 — High CPU when input focused (2 comments):](https://github.com/sipeed/picoclaw/issues/3292)** Reported by a Debian/Firefox user on web UI; likely related to cursor blink or re-render loops. Marked stale, but with 1 comment beyond the author, it remains a friction point for desktop web users.
- **[Issue #3287 — Long message support in IRC (2 comments):](https://github.com/sipeed/picoclaw/issues/3287)** Addresses the 512-byte IRC limit where clients split long messages with newlines, confusing PicoClaw's parser. The request is to treat IRCv3 long messages as a single cohesive unit—important for users migrating from IRC with longer-form content.
- **[PR #3200 — Fallback chain (no comments):](https://github.com/sipeed/picoclaw/pull/3200)** While comment-free, this PR targets AI model reliability—a natural next step given the diverse, often flaky model landscape users navigate.

**Underlying needs:** Users are pushing toward production-grade multi-protocol messaging (IRC, DeltaChat, Simplex), better web UI performance, and resilient model configurations that fail over gracefully—reflecting a maturing user base relying on PicoClaw as a daily driver.

## 5. Bugs & Stability

One bug was reported/updated in the last 24 hours:

- **[Issue #3292 — High CPU usage when input box focused (Severity: Medium):](https://github.com/sipeed/picoclaw/issues/3292)** Affects the web chat interface in Firefox on Linux. Users experience sustained high CPU usage when the input is selected, which degrades overall system responsiveness. No fix PR currently linked. The "stale" label suggests maintainers may deprioritize without further reproducer details.

No crashes or regressions were reported this cycle.

## 6. Feature Requests & Roadmap Signals

- **[IRC long-message handling (Issue #3287):](https://github.com/sipeed/picoclaw/issues/3287)** Explicitly requests that IRCv3 long messages be recognized as single messages despite client-side splitting. Given IRC's fundamental limits, this is a compatibility enhancement—likely to be picked up for the next milestone as multi-channel robustness is a recurring theme.
- **[Configurable model fallback chain (PR #3200):](https://github.com/sipeed/picoclaw/pull/3200)** Already implemented as a PR; if merged, a strong candidate for the next release. This directly addresses user pain around model availability and rate limits.
- **[Simplex support (PR #3193):](https://github.com/sipeed/picoclaw/pull/3193)** Adds a new channel type; likely to be merged and shipped pending review.

These signals indicate the next version will likely focus on protocol expansion (Simplex, refined DeltaChat) and AI resilience (fallback chains, long-message awareness).

## 7. User Feedback Summary

Users are pushing PicoClaw to feel more polished in real-world messaging scenarios:

- **Pain point — Messaging fidelity:** IRC users with long outputs (code blocks, logs) want the bot to interpret them correctly as one message, not fragmented lines.
- **Pain point — Resource usage:** Web UI input focus burning CPU is a blocker for lightweight/laptop usage, implying a need for smoother front-end rendering.
- **Positive signal — Expanding protocols:** The addition of Simplex and DeltaChat improvements shows users want PicoClaw as a universal bridge. The DeltaChat refactor (dropping legacy, enforcing secrets via JSON-RPC) reflects a push toward security-forward credentials handling.

Overall sentiment skews constructive: issues are well-specified with environment details, and PRs are clean, scope-contained contributions.

## 8. Backlog Watch

- **[PR #3193 — Simplex channel type (open since 2026-06-27):](https://github.com/sipeed/picoclaw/pull/3193)** Stalled for ~5 weeks without review. Given its breadth (new channel type), it may require maintainer input on architecture compliance (e.g., JSON-RPC patterns); deserves attention to prevent drift.
- **[PR #3222 — DeltaChat cleanup (open since 2026-07-03):](https://github.com/sipeed/picoclaw/pull/3222)** Substantial refactor pending review for ~4 weeks. Given its -200 LOC and behavior changes (invite link renaming), it needs a maintainer to sanity-check API breakage and merge timing.
- **[Issue #3292 — High CPU bug (open since 2026-07-24, marked stale):](https://github.com/sipeed/picoclaw/issues/3292)** If confirmed, this affects all web users; consider un-staling and requesting a minimal reproducer (e.g., does it happen with an empty input?).

None of these block critical paths, but extended open time increases merge conflict risk and community perception of stalled momentum.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-01

## 1. Today's Overview

NanoClaw is in a **strong, high-output development phase**: 8 issues and 9 PRs were updated in the last 24 hours, with 3 PRs closed/merged and zero open bug reports marked as unaddressed. The core team is actively landing **security hardening** (log redaction, release path fix) and pushing forward the **container-runtime abstraction roadmap** (Apple Container, Kubernetes, native mode), which remains the single most debated architectural topic. Community engagement is moderate — top issues draw 1-3 comments — but signal quality is high: contributors are filing detailed, reproducible bug reports with attack scenarios and environment specifics. The maintainers appear responsive, though a few long-standing questions (#1184, #1225) have gone weeks without a definitive answer from the team.

## 2. Releases

**No new releases published in the last 24 hours.** The most recent release path (v2.1.54) was the subject of a merged fix today — see Project Progress below — indicating the next release is likely being prepared or was just restored.

## 3. Project Progress

Three PRs were closed/merged today, reflecting a mix of operational fix and feature advancement:

- **[#3163 — fix(release): restore the v2.1.54 release path](https://github.com/qwibitai/nanoclaw/pull/3163)** (closed, core-team). A previously broken release pipeline was repaired — a critical housekeeping fix that unblocks future versioning.

- **[#3076 — feat(imessage): unified local+hosted adapter targeting spectrum-ts v11](https://github.com/qwibitai/nanoclaw/pull/3076)** (closed, feature skill). The iMessage integration consolidated into a unified adapter covering both local and hosted modes — a meaningful step toward making the channel story more coherent (and likely a prerequisite for the newer hosted iMessage PR, #3164).

- **[#1678 — docs(skills): update voice transcription skills for Telegram + Linux](https://github.com/qwibitai/nanoclaw/pull/1678)** (closed, docs). Documentation for `use-local-whisper` expanded beyond WhatsApp to Telegram and Linux — reducing friction for users on those platforms.

**Open PRs of note:** [#3161 — redact secrets from host structured logs](https://github.com/qwibitai/nanoclaw/pull/3161) is a security fix that addresses a real credential-leak vector; it is fresh (opened today) and has no comments yet, suggesting it is awaiting review.

## 4. Community Hot Topics

- **[#1184 — Challenges deploying NanoClaw in restricted K8s environments (Sealos)](https://github.com/qwibitai/nanoclaw/issues/1184)** — 1 👍, 3 comments. The oldest active thread. JachinShen praises the minimalist design but hits practical walls running in managed K8s. This is the highest-signal signal for the **container-runtime portability demand** that also drives #2354 and #1732.

- **[#2588 — skill/apple-container branch is substantially out of sync with mainline](https://github.com/qwibitai/nanoclaw/issues/2588)** — 1 comment. A user tried the documented `/convert-to-apple-container` skill and it failed immediately due to branch drift. This is both a **documentation** and a **maintenance** issue: it erodes trust in the official skill path and indicates the Apple Container story is not yet production-ready.

- **[#1732 — feat: native runner mode — bypass Docker for host-tool access](https://github.com/qwibitai/nanoclaw/issues/1732)** — 3 comments. Strongly framed use cases (tmux, headed browsers, macOS APIs) that Docker isolation blocks. No 👍 yet, but the issue list and the open PR #2809 show the team is already pursuing the Apple Container path as a partial answer.

- **[#3164 — Hosted iMessage (Photon): supersede #2999 with a working registration flow](https://github.com/qwibitai/nanoclaw/pull/3164)** — opened today, core-team. New feature PR explicitly superseding an older approach; currently uncommented but likely to draw review attention.

**Underlying needs:** The community is asking for **runtime flexibility** (Docker is not universal) and **host integration** (Docker is not sufficient). The team is responding by abstracting the runtime, but the pace of that work is creating documentation/branch drift that users are hitting.

## 5. Bugs & Stability

**High severity:**

- **[#3162 — Telegram pairing permanently broken if boot-time getMe fails](https://github.com/qwibitai/nanoclaw/issues/3162)** (open, new today). A single transient HTTP failure at boot permanently breaks pairing for the process lifetime, with no user-facing error. This is a silent availability bug in a core channel — it deserves priority triage. *No fix PR exists yet.*

**Medium severity:**

- **[#2923 — ask_user_question card can be defaced by forged click before origin authz](https://github.com/qwibitai/nanoclaw/issues/2923)** (open, from July 4). Display-integrity spoofing. Note: open PR **[#2651 — validate pending question response origin](https://github.com/qwibitai/nanoclaw/pull/2651)** exists and directly addresses this class of issue — it is still open and unmerged, so the fix is in progress but not shipped.

- **[#2589 — host.docker.internal doesn't resolve inside Apple Container microVM](https://github.com/qwibitai/nanoclaw/issues/2589)** (open, from May 22). Environment-specific networking bug that blocks the Apple Container path for users behind proxies.

**Low severity:**

- **[#2588 — apple-container branch out of sync with mainline](https://github.com/qwibitai/nanoclaw/issues/2588)** — operational/maintenance bug; immediate failure of a documented skill.

**Security hygiene improvement:** **[#3161 — redact secrets from host structured logs](https://github.com/qwibitai/nanoclaw/pull/3161)** (open, new) fixes verbatim credential serialization into `nanoclaw.log` — a worthwhile fix that should be reviewed and merged quickly.

## 6. Feature Requests & Roadmap Signals

Strong roadmap signals, in order of momentum:

1. **Container runtime abstraction** (highest). [#2354 (Kubernetes runtime)](https://github.com/qwibitai/nanoclaw/issues/2354), [#1732 (native runner)](https://github.com/qwibitai/nanoclaw/issues/1732), and open PR [#2809 (Apple Container)](https://github.com/qwibitai/nanoclaw/pull/2809) all push the same direction: `CONTAINER_RUNTIME` as an env-gated switch with `docker` as the byte-identical default. **Prediction:** this lands in the next minor release, with Apple Container support first; Kubernetes support is likely to follow as a separate PR.

2. **Channel expansion.** The iMessage adapter consolidation (#3076) plus the new hosted iMessage PR (#3164) and the Dial channel PR ([#3041 — SMS + AI voice calls](https://github.com/qwibitai/nanoclaw/pull/3041)) show the team is actively broadening channel coverage. **Prediction:** at least one of these merges within two release cycles.

3. **Security posture hardening.** Beyond the origin-auth fix (#2651) and log redaction (#3161), the open docs PR [#2954 — security reporting and triage policy](https://github.com/qwibitai/nanoclaw/pull/2954) signals the project is formalizing its security process — a good sign for enterprise adoption.

## 7. User Feedback Summary

- **Positive sentiment:** JachinShen (#1184) explicitly praises the "minimalist approach" and "lightweight, secure alternative to the more bloated agent frameworks" — a clear demonstration of product-market fit for the core design philosophy. Users value the security-by-default container isolation even while asking for escape hatches.

- **Pain points:**
  - **Docker dependency is the #1 friction point.** Two open questions (#1184, #1225) are effectively the same ask: "Can I run this without Docker?" — from Windows, Linux, and restricted K8s environments.
  - **Apple Container path is immature.** #2588 and #2589 both show users following official docs and hitting broken/unsupported behavior — a reliability gap that damages trust in the feature.
  - **Channel reliability matters.** The Telegram pairing bug (#3162) is silently destructive; the fact that it's a boot-time, whole-lifetime failure makes it particularly frustrating.

## 8. Backlog Watch

- **[#1184 — Restricted K8s (Sealos) deployment](https://github.com/qwibitai/nanoclaw/issues/1184)** — open since **March 17** (4.5 months). 3 comments, 1 👍. The team has not provided a direct answer; the issue is effectively parked pending the container-runtime work. A formal "we hear you, roadmap item X" from a maintainer would reduce community uncertainty.

- **[#1225 — Run it without Docker](https://github.com/qwibitai/nanoclaw/issues/1225)** — open since **March 18** (4.5 months). 2 comments, no maintainer response visible. FAQ-level question that deserves a documented answer even if the feature isn't ready.

- **[#2651 — Origin validation for ask_user_question](https://github.com/qwibitai/nanoclaw/pull/2651)** — open since May 30, directly fixes the security issue in #2923 (reported July 4). It has been waiting over two months for merge; given the security context, this warrants accelerated review.

- **[#2954 — Security reporting and triage policy](https://github.com/qwibitai/nanoclaw/pull/2954)** — open since July 4, no comments. A docs-only PR that codifies process; low-risk, high-value, and should be quick to merge.

---

**Overall health assessment:** NanoClaw is shipping steadily, with a clear architectural direction (runtime-agnostic containers) and active security improvements. The main risks are **backlog debt on long-open community questions** (#1184, #1225) and **the Apple Container feature being documented before it is stable** (#2588). Addressing those two items would materially improve community satisfaction.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-08-01

## 1. Today's Overview

NullClaw is currently in a **low-activity maintenance phase**: no issues were updated in the last 24 hours and no new releases were published. The project shows **one open pull request** (`#981`) that has been actively discussed over the past two days since its creation on 2026-07-29, indicating moderate review momentum in the provider-ecosystem area. There are **zero open or active issues**, which suggests either a well-stabilized core or a low volume of user traffic entering the tracker. Overall, the project appears **stable with light development activity**, focused on incremental expansion of provider integrations rather than core fixes or feature breakthroughs.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release history shows no version bumps within this digest window. No breaking changes or migration notes to report.

## 3. Project Progress

**No merged or closed PRs** occurred in the last 24 hours. The only active PR (`#981`) is still under review:

- **[#981 — feat(provider): add grok-cli provider for xAI Grok CLI](https://github.com/nullclaw/nullclaw/pull/981)** (open, created 2026-07-29)
  - Adds a new optional CLI-based provider that delegates to the local `grok` CLI.
  - Follows the established `spawn-per-request` pattern already used by `codex-cli`, `gemini-cli`, and `claude-cli` providers.
  - This is a **pattern-following extension** rather than a novel architectural change, which reduces review risk and likely speeds up merge once approved.

## 4. Community Hot Topics

The single active item is the **only** community conversation right now:

- **[#981 — feat(provider): add grok-cli provider for xAI Grok CLI](https://github.com/nullclaw/nullclaw/pull/981)** (open, 0 comments, 0 reactions)
  - **Underlying need:** Users deploying xAI's Grok models appear to want first-class support within NullClaw without waiting for an API-native integration. The `grok-cli` provider builds on an established pattern, suggesting demand for **rapid adoption of new model providers** via lightweight CLI shims rather than heavyweight API wrappers.
  - The lack of comments/reactions could indicate either low visibility or that the PR is waiting for maintainer review before broader community engagement.

## 5. Bugs & Stability

**No bugs, crashes, or regressions** were reported in the last 24 hours (zero open/active issues). No stability concerns to rank or address in this window.

## 6. Feature Requests & Roadmap Signals

No user-submitted feature requests are present in the current issue tracker. The signal for future direction comes from the open PR:

- **Provider ecosystem expansion** (`#981`): The pattern of adding CLI-based providers (`codex-cli`, `gemini-cli`, `claude-cli`, now `grok-cli`) strongly suggests that **the next release may include the `grok-cli` provider** if the PR is merged cleanly.
- **Likely near-term roadmap:** Additional CLI-based providers for emerging model vendors (e.g., other xAI or Mistral tools) could be expected, given the established, repeatable integration pattern.

## 7. User Feedback Summary

With zero issues and one PR, direct user feedback is minimal this window. Observable signals include:

- **Pain points:** None reported.
- **Use cases:** The `grok-cli` PR indicates real usage of xAI Grok CLI in local/agent environments, and a desire for NullClaw to interoperate with locally installed model CLIs.
- **Satisfaction:** The absence of bug reports or complaints suggests a generally satisfied user base, though it may also reflect low visibility of the issue tracker. The community appears to prefer **submitting PRs over filing issues**, indicating a technically engaged user base that self-resolves and contributes directly.

## 8. Backlog Watch

No items meet the criteria for backlog watch at this time:

- **No long-unanswered issues** exist (tracker is empty).
- **PR #981** (open since 2026-07-29, updated 2026-07-31) is the only open PR and is **not yet stale** — it has been active within the last day and is awaiting maintainer review. This PR represents the main pending action item for maintainers.

---

**Overall health assessment:** Stable, quiet, and clean. The project shows no accrued technical debt in its tracker, no unaddressed user pain, and a small but productive contribution pipeline. The primary watch item for maintainers is the review and merge decision on PR `#981`, which carries the current momentum for the provider roadmap.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-01

## 1. Today's Overview

IronClaw is in a period of significant architectural restructuring ("Reborn" initiative) alongside steady bug-fix velocity. Activity remains high: 31 issues and 50 PRs were updated in the last 24 hours, with 8 issues closed and 32 PRs merged. The project is executing Wave 1 of its target architecture (contract extraction and dependency narrowing), with a stacked PR sequence (#6975→#6977→#6980→#6981→#6982) representing the core refactoring effort. A serious cross-user memory leak (P0) and a freshly discovered CI structural failure are the most urgent stability concerns. The maintainer team is actively responding to community feedback, with multiple new feature requests filed in the past 48 hours.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release remains the open PR #5598, which proposes `ironclaw_common` 0.4.2→0.5.0 and `ironclaw_skills` 0.3.0→0.4.0, both with API breaking changes (still unmerged).

## 3. Project Progress

The Wave 1 architecture refactor made substantial progress with several stacked PRs:

- **#6977 (CLOSED)** — Extracted `ironclaw_extension_contracts` from `ironclaw_host_api` and closed dual import paths (WS1.3).
- **#6975 (CLOSED)** — Extracted `ironclaw_loop_contracts` and flipped the agent loop onto it (WS1.2).
- **#6967 (CLOSED)** — Completed turn vocabulary in host_api and retired turns shims (WS1.1).
- **#6979 (CLOSED)** — Reconciled target-architecture docs with the hosted MCP registration (#6930), docs-only change (+27/−11 across 5 files).
- **#6930 (CLOSED)** — Registered hosted MCP servers with tenant-runtime lifecycle integration (large: 153 files, +15k/−1.8k).
- **#6932 (CLOSED)** — Bulk dependency bump (34 updates) across the everything-else group.
- **#4022, #3942, #3952 (CLOSED)** — Older PRs merged this period: HTTP error recoverability fix, PilotAllowlist enum refactor, and TOCTOU-hardening of the filesystem backend via openat2.

Still open and pending review: **#6980** (WS1.4 — product contracts extraction), **#6981** (WS1.5 — sealed evidence minting), **#6982** (WS1.6/1.7 — common narrowing).

## 4. Community Hot Topics

The most active discussions reveal where users and maintainers are focusing attention:

- **[#6284 — Error-Recoverability Endgame Epic](https://github.com/nearai/ironclaw/issues/6284)** (15 comments) — The most-discussed issue. A comprehensive contract for error recovery: every mid-run error must survive, be seen by the model, carry cause + remedy, and give the model a turn to act. This is a foundational reliability epic.

- **[#6963 — Path-Keyed CI Gates](https://github.com/nearai/ironclaw/issues/6963)** (5 comments) — Filed as a review-followup, tracking 8 defects where CI/dev gates resolve scope from the literal flat crate tree. The "checklist row is weak tracking" complaint signals friction with how the team records multi-defect findings.

- **[#6524 — Hermetic Capability/Journey Testing Epic](https://github.com/nearai/ironclaw/issues/6524)** (4 comments) — The project's answer to "does everything have deterministic test coverage?" A long-running epic (since July 22) that keeps attracting attention.

- **WebUI feedback cluster** — Multiple issues from `italic-jinxin` (#6903, #6904, #6909, #6910) about pagination and shared components. These were all addressed quickly (3 of 4 closed), showing responsive maintainers.

The recurring theme: users and maintainers alike care deeply about **making the agent reliably recoverable** (#6284), **deterministic test coverage** (#6524), and **terminology/UX consistency** (#6971, #6854).

## 5. Bugs & Stability

Ranked by severity:

### Critical / P0
- **[#6900 — Shared-channel default subject binding collapses all users into the operator's memory namespace](https://github.com/nearai/ironclaw/issues/6900)** — Cross-user memory leak in shared conversations. Suggest P0. This is a security isolation failure and should be triaged for immediate fix.
- **[#6897 — Model gateway catch-all retries deterministic LLM errors for ~7 minutes](https://github.com/nearai/ironclaw/issues/6897)** — Suggested P0, and it's **CLOSED** — the regression appeared fixed, but verify the resolution shipped.

### High / P1
- **[#6866 — Same home directory shared across all users; workspaces visible](https://github.com/nearai/ironclaw/issues/6866)** — Reported 3 days ago, still open. Privacy concern with multi-user deployments.
- **[#6778 — Hosted-MCP discovered catalogs published per extension id, not installation](https://github.com/nearai/ironclaw/issues/6778)** — Cross-user metadata exposure on multi-principal servers. Open 4 days.

### Moderate / P2
- **[#6940 — IronHub skill CTA returns 404](https://github.com/nearai/ironclaw/issues/6940)** — User-facing breakage on every skill page.
- **[#6972 — New account email auth not working](https://github.com/nearai/ironclaw/issues/6972)** — Fresh account creation fails to authenticate.
- **[#6902 — Projects page displays fabricated metrics](https://github.com/nearai/ironclaw/issues/6902)** — UI shows `$0.00 spend`, `0 pending gates`, etc. that the backend never provided. **A fix PR exists: #6906** (open).
- **[#6947 — classify-test-scope.sh mis-buckets ironclaw_product](https://github.com/nearai/ironclaw/issues/6947)** — Pre-existing CI misclassification, not introduced by recent work.
- **[#6974 — libSQL thread_store_writes pathology](https://github.com/nearai/ironclaw/issues/6974)** — Tool-heavy stress cases at p95 37–135s, far over the 2.5s budget. A fix attempt exists in **#6973** (open).

### Infrastructure / CI
- **[#6978 — reborn-tests.yml workflow_dispatch structurally fails roll-up](https://github.com/nearai/ironclaw/issues/6978)** — `critical-mutation` is skipped on manual dispatch but the roll-up gate disallows it — a clean run with zero real failures still goes red. Proven from workflow source.

## 6. Feature Requests & Roadmap Signals

Several user-requested features are strong candidates for upcoming releases:

- **[#6939 — Migration tool for legacy agent setup](https://github.com/nearai/ironclaw/issues/6939)** — Port setup/config/memory from Hermes/Openclaw to IronClaw. High switching-cost barrier; likely to gain traction.
- **[#6938 — Skill selection moves to the model (PR)](https://github.com/nearai/ironclaw/pull/6938)** — "The model chooses the skill, not a keyword scorer." This aligns with the #6941 epic and could land soon.
- **[#6971 — Clarify "Tools" vs "Extensions" terminology](https://github.com/nearai/ironclaw/issues/6971)** — Product-language consistency question; likely a docs + UI renaming workstream.
- **[#6983 — Add `hub` alias for `ironhub` CLI subcommand](https://github.com/nearai/ironclaw/issues/6983)** — Small, low-risk, user-requested convenience.
- **[#6854 — Rebrand "Reborn" → "Ironclaw 1.0" in extensions page](https://github.com/nearai/ironclaw/issues/6854)** — External messaging consistency. Simple fix, reported 3 days ago.

## 7. User Feedback Summary

- **Positive signaling:** The WebUI bugs reported by `italic-jinxin` were closed quickly (pagination, shared components, confirm dialogs), indicating the team responds well to concrete reproduction steps.
- **Switching-cost friction:** #6939 captures real user resistance to migration (Hermes/Openclaw → IronClaw) without a porting path.
- **Identity/privacy concerns are recurring:** #6900 (memory leak), #6866 (home dir sharing), #6778 (MCP catalog exposure). Users are actively testing multi-user isolation and finding real gaps.
- **Documentation accuracy:** Users and maintainers both flag cases where docs claim behavior that isn't regression-tested (#6945, #6962). The team is correcting and tracking gaps.

## 8. Backlog Watch

Issues that have gone >48 hours without maintainer response or action:

- **[#6866 — Shared home directory (P2, security-tagged)](https://github.com/nearai/ironclaw/issues/6866)** — Open since July 29, no comments beyond the report. Privacy-critical.
- **[#6854 — "Reborn" branding on extensions page](https://github.com/nearai/ironclaw/issues/6854)** — Open since July 29, one comment (the report itself).
- **[#6778 — Hosted-MCP cross-user metadata exposure](https://github.com/nearai/ironclaw/issues/6778)** — Open since July 28, one comment. Security-adjacent; deserves a triage tag.

Long-dormant items worth attention:

- **[#5598 — Release PR (`chore: release`)](https://github.com/nearai/ironclaw/pull/5598)** — Open since July 3, with breaking changes in `ironclaw_common` and `ironclaw_skills`. 29 days with no merge — this blocks downstream consumers from the new API surface.

---

**Overall assessment:** IronClaw is a healthy, fast-moving project with clear architectural direction and responsive maintainers. The Wave 1 contract-extraction sequence is well-coordinated and mostly landing clean. The main risks are (a) the unmerged release PR from July 3, (b) three multi-user isolation bugs still open, and (c) a structural CI failure on `workflow_dispatch` that could produce false red signals during the refactor wave. Community engagement is strong, and the feedback loop from user reports to fixes is impressively short.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Based on the GitHub data from LobsterAI (netease-youdao/LobsterAI), here is the project digest for **2026-08-01**.

---

## LobsterAI Project Digest — 2026-08-01

### 1. Today's Overview
LobsterAI shows **moderate to high activity** over the last 24 hours, with **12 PRs updated** (11 merged/closed, 1 still open) and **4 issues closed** (all marked stale). No new releases were published today. The primary focus was improving **stability in the OpenClaw and Cowork agent runtime**, particularly around prompt caching, tool protocol hygiene, and the dashboard UI. A significant fix was merged to address a critical performance regression related to DeepSeek's prefix cache hit rate in long sessions. The project remains in a **stable phase**, with a clear push toward refining agent orchestration internals and improving the user interface of the companion dashboard.

### 2. Releases
**No new releases** were published in the last 24 hours. The most recent release appears to be `2026.7.31` (referenced by PR #2416), suggesting a monthly release cadence.

---

### 3. Project Progress
Today saw the merging of several key fixes and feature implementations aimed at improving both the **core agent engine (OpenClaw)** and the **user-facing dashboard (Cowork)**.

**Core Agent & Performance**
- **[#2413]** `fix(openclaw): keep live prompt tool-result history byte-stable across turns` & **[#2415]** `fix(openclaw): drop aggregate cap in live tool-result projection`: These two merged PRs are the day's biggest wins. They fix a critical regression where the prompt builder re-applied a char cap on every request, rewriting already-cached history and collapsing **DeepSeek's prefix cache hit rate from ~100% to ~57%** in long sessions. The fix ensures stable prefixes, restoring performance.
- **[#2234]** `fix(openclaw): cron yield descendant finalization` (Open): A requested fix is being prepared to handle finalization for cron-scheduled jobs that yield to descendant agents. It aims to ensure parent agents resume correctly after children complete, covering parallel and serial child scenarios.
- **[#2414]** `fix(cowork): prevent BTW tool protocol leakage`: Merged to sanitize provider tool-call markup in side-chat results, preventing internal protocol details from leaking into the user-facing chat. It also ensures stable guidance when a side question requires tools.

**Dashboard / UI & UX**
- **[#2417]** `fix(sites): add copy success feedback`: Improves UX by providing clear visual feedback when copying site URLs and share codes, reusing the existing conversation copy interaction.
- **[#2416]** `Release/2026.7.31`: A release-prep PR for the monthly cycle, containing docs, main, and openclaw updates.

**Historical/Older PRs Merged (previously stale)**
The batch of "stale" PRs merged today represents important user-requested enhancements that have finally been integrated. 
- **[#1315]** `功能增强：支持拖拽调整侧边栏宽度`: Implements draggable sidebar width adjustment (180px-480px range).
- **[#1318]** `功能增强：侧边栏按钮显示键盘快捷键 kbd 提示`: Displays keyboard shortcut hints (e.g., `Ctrl+N`) in the sidebar, with platform-aware symbol rendering (⌘ on macOS).
- **[#1320]** `功能增强：会话列表添加骨架屏加载状态`: Implements a skeleton loading screen for the session list, addressing the flicker of a "No Sessions" empty state during app initialization.
- **[#1321]** `fix(settings): dismiss overlays when switching settings tabs`: Fixes a UI bug where the memory editor or connection-test modals could block the settings screen after navigating between tabs.

---

### 4. Community Hot Topics
Current open discussions are limited, with the most active items being the now-merged feature requests. 

- **Feature: Sidebar Customization & Responsiveness** (`#1314`, `#1311`): These issues (now closed) highlighted a trend in user pain points around the dashboard UI. Users want more control over their workspace, such as adjustable sidebar widths to see more session titles, and better handling of long text in tables (e.g., hover to see full content, not just truncated text).
- **Feature: UI Discovery & Usability** (`#1317`): Users found features (like keyboard shortcuts) hard to discover, pointing to a need for better in-app guidance. 

These three issues (`#1314`, `#1317`, `#1319`) are related to improving the usability of the `Cowork` dashboard and were all submitted by user **MaoQianTu**, who also authored the corresponding merged PRs.

---

### 5. Bugs & Stability
Several bugs were addressed today, with the most severe being a **critical performance regression**.

1.  **[HIGH] DeepSeek Cache Hit Rate Collapse**:
    - **Issue:** Live prompt projection was rewriting history and breaking prefix cache stability, dropping hit rates from ~100% to ~57% in long sessions.
    - **Fix:** **Merged** in PRs `#2413` and `#2415`. This was a high-priority fix that rolled a significant amount of output token cost back by restoring byte-stable history.
2.  **[MEDIUM] BTW Tool Protocol Leakage**:
    - **Issue:** Internal `BTW` protocol markup from provider tool calls could leak into the rendered UI through side-chat results.
    - **Fix:** **Merged** in PR `#2414`, which sanitizes the markup.
3.  **[MEDIUM] Settings Modal Overlay Bug**:
    - **Issue:** The memory editor or connection-test modals could be left mounted and blocking the UI when switching settings tabs.
    - **Fix:** Merged in older PR `#1321` (now closed).
4.  **[LOW] Copy Site URL/Share Code Feedback**:
    - **Issue:** No visual feedback when copying site URLs, causing confusion.
    - **Fix:** Merged in PR `#2417`.
5.  **[LOW] "No Sessions" Flash on Startup**:
    - **Issue:** On app startup, the session list briefly displayed "No history" before loading actual data, potentially alarming users.
    - **Fix:** Merged in older PR `#1320` (now closed) by adding a skeleton loading state.

---

### 6. Feature Requests & Roadmap Signals
The issues and PRs merged today signal several clear roadmap items that have now been completed. Looking ahead, the next version of LobsterAI will likely include:

- **Enhanced Dashboard Usability:** The batch of merged "stale" PRs (`#1315`, `#1318`, `#1320`) brings much-needed polish to the `Cowork` dashboard. Expect to see **draggable sidebars**, **keyboard shortcut hints**, and **skeleton loading states** in the next release.
- **Improved Agent Orchestration:** The pending PR `#2234` for `cron yield descendant finalization` indicates a focus on making complex agent workflows (like parallel and serial sub-agents) more robust and reliable. This is likely to be a target fix for the next release.
- **Customizable Data Display:** The closed issue `#1311` requests better table rendering, specifically adding hover-to-see-full-text for long content. This is a user-visible feature that could be picked up in a future UI sprint.

---

### 7. User Feedback Summary
- **Pain Points:**
    - Users find the interface rigid and hard to read, specifically citing the fixed sidebar width for clipping long titles and the lack of context for truncated table content.
    - New users struggle to discover existing features (keyboard shortcuts), indicating a need for more intuitive design or onboarding hints.
- **Core Needs:**
    - **Performance & Stability:** The high-priority fixes for DeepSeek caching and prompt stability show users rely heavily on the tool being fast and efficient, especially for long-running sessions.
    - **Efficiency:** Users want to customize their workspace and understand how to use the tool more effectively.
- **Satisfaction (Indirect):**
    - The community is actively submitting detailed feature requests with proposed solutions and even implementing them via PRs (as seen with MaoQianTu's contributions), demonstrating a healthy and engaged user base that is proactively contributing to the project’s development.

---

### 8. Backlog Watch
These items require further attention from maintainers or are worth monitoring:

- **[OPEN] PR #2234** `fix(openclaw): cron yield descendant finalization` by `btc69m979y-dotcom` | Created: June 30, 2026. This is the only open PR and has been updated recently. While it has no comments or reactions, it targets a critical area of the agent runtime (cron scheduling finalization) and has been pending for a month. It is worth watching to ensure it gets proper review and testing.
- **[Potential Regression Watch]:** Keep an eye on any subsequent issues related to DeepSeek token usage or prompt caching after the fixes in `#2413` and `#2415` are released, to confirm the fix is stable in production.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for **2026-08-01**:

---

## Moltis Project Digest — 2026-08-01

### 1. Today's Overview
Moltis saw moderate activity today, with 2 issues and 6 PRs updated in the last 24 hours. The project is in a **healthy, security-conscious phase**, with two open security-hardening PRs (#1179, #1180) and a critical privileges-gating PR (#1170) awaiting review. Notably, two previously closed items were resolved this cycle: the Markdown copy/export feature request (#1131) and its implementing PR (#1176), which shipped successfully. A new bug report involving GPT-5.6 Luna (#1181) was filed but has received no initial triage or comments yet. No new releases were published.

### 2. Releases
No new releases were published in the last 24 hours. The most recent activity is concentrated in PRs and issues.

### 3. Project Progress
Two PRs were merged/closed today:
- **PR #1176** ([link](https://github.com/moltis-org/moltis/pull/1176)) — **feat(web): add Markdown copy and session export**, merged. This implements requested functionality for preserving raw Markdown in copied replies and a full session-level "Save as Markdown" action.
- **PR #1168** ([link](https://github.com/moltis-org/moltis/pull/1168)) — **feat(nostr): add NIP-29 group chat support for Buzz channels**, closed/merged. This expands the `moltis-nostr` connector to support Block's Buzz workspace via NIP-29 group chat over authenticated NIP-42 connections.

### 4. Community Hot Topics
- **Issue #1131** ([link](https://github.com/moltis-org/moltis/issues/1131)) — "Add copy + export as Markdown," received 1 👍 and was closed today, indicating strong community desire for better data portability, which has now been addressed by PR #1176.
- **PR #1158** ([link](https://github.com/moltis-org/moltis/pull/1158)) — "feat(memory): add zvec vector database memory backend," remains a popular experimental PR, suggesting interest in pluggable memory backends beyond the default.
- There are no issues or PRs with unusually high comment counts today; the community is focused on incremental feature and stability work.

### 5. Bugs & Stability
One new bug was reported today, plus two open security PRs:
- **[HIGH] Issue #1181** ([link](https://github.com/moltis-org/moltis/issues/1181)) — "Issue with GPT 5.6 Luna," filed by `ndrewtl` with no comments yet. No fix PR exists yet; requires triage.
- **[CRITICAL] PR #1170** ([link](https://github.com/moltis-org/moltis/pull/1170)) — "fix(channels): gate /sh and privileged tools behind per-account operators list." Separates access from privilege to stop allowlisted users from reaching host tools; essential security boundary fix, still open.
- **[CRITICAL] PR #1179** ([link](https://github.com/moltis-org/moltis/pull/1179)) — "fix(gateway): verify node pairing signatures." Binds pairing verification to server-issued requests to prevent callers from forging keys/challenges; still open.
- **[CRITICAL] PR #1180** ([link](https://github.com/moltis-org/moltis/pull/1180)) — "fix(security): harden model and zip paths." Prevents arbitrary file write outside intended dirs from malicious zips or HuggingFace repos, which could lead to code execution; still open.

### 6. Feature Requests & Roadmap Signals
- **Markdown copy/export** (Issue #1131) is now shipped, signaling improved UX for users who need portability across tools.
- **Nostr/Buzz group chat support** (PR #1168) is merged, indicating a roadmap trend toward interoperable, self-hosted, human-AI collaboration platforms.
- The continued interest in **alternative memory backends** (PR #1158, zvec/redb) suggests a future direction toward modular, performant, local-first vector storage. This could land in the next minor release if it passes review.

### 7. User Feedback Summary
- Users are actively **privacy- and security-conscious**, as evidenced by contributor `tsauvajon`'s explicit statement: *"I'd like to use Moltis, but I've got a couple of security fixes I'd like to get in before doing so."* This signals that security gaps are a **blocking concern** for adoption among technical users.
- The community shows strong interest in **data portability** (Markdown export) and **collaboration with humans inside existing platforms** (Buzz/Nostr).
- The new GPT-5.6 Luna bug report (no comments yet) may be anecdotal, but it highlights that the project is actively used with cutting-edge external models.

### 8. Backlog Watch
The following items need maintainer attention:
- **PR #1179** ([link](https://github.com/moltis-org/moltis/pull/1179)) — Critical security fix, open since 2026-07-31, unaddressed. Security PRs should take priority given the explicit blocker reported by the community.
- **PR #1170** ([link](https://github.com/moltis-org/moltis/pull/1170)) — Critical privileged-tools gating, open since 2026-07-26, no maintainer response.
- **PR #1180** ([link](https://github.com/moltis-org/moltis/pull/1180)) — Critical arbitrary-file-write fix, open since 2026-07-31.
- **Issue #1181** ([link](https://github.com/moltis-org/moltis/issues/1181)) — New bug with no triage or confirmation, filed 2026-07-31.

*Moltis appears to be in a solid, feature-forward development phase; the key risk this week is the accumulation of high-severity security PRs awaiting review.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest
**Date:** 2026-08-01

---

## 1. Today's Overview

CoPaw (QwenPaw) is in an active development phase with 20 issues and 43 PRs updated in the last 24 hours, indicating a high-velocity community-driven project. The project is currently addressing a backlog of stability issues, particularly around shell command execution (UI freezes, timeouts, large outputs), session data integrity, and memory/context management. A notable cluster of first-time contributors are submitting fixes for critical bugs (#6520 agent.json corruption, #6608 shell hanging, #6588 subagent schema), suggesting an accessible codebase and responsive maintainers. The release channel is quiet (no new versions), with ongoing work concentrated on the 2.0.1 bug-fix cycle. Overall, the project appears healthy with strong community engagement, though the volume of open issues (14) suggests a need for more maintainer bandwidth to keep pace.

---

## 2. Releases

No new releases were published in the last 24 hours. The project is currently on version 2.0.1 (Desktop), with users reporting compatibility issues with `agentscope==2.0.4.post1` (see [Issue #6612](https://github.com/agentscope-ai/QwenPaw/issues/6612)).

---

## 3. Project Progress

**Merged/Closed PRs (13 total):** The project saw several key fixes land today:

- **Audio transcription restored:** [PR #6573](https://github.com/agentscope-ai/QwenPaw/pull/6573) fixes silent audio transcription failures for Feishu and other channel messages after the AgentScope 2.0 migration (closes [Issue #6544](https://github.com/agentscope-ai/QwenPaw/issues/6544)).
- **Session integrity preserved:** [PR #6602](https://github.com/agentscope-ai/QwenPaw/pull/6602) fixes multiple chat session data integrity issues (#6558) by preserving in-flight streams across mode switches and reconnecting via a shared per-agent TaskTracker.
- **Memory compression fixed:** Two related PRs closed — [PR #6564](https://github.com/agentscope-ai/QwenPaw/pull/6564) and [PR #6592](https://github.com/agentscope-ai/QwenPaw/pull/6592) — both addressing the "Dream" process missing early-session events (Issue #6555).
- **File read fix:** [PR #6606](https://github.com/agentscope-ai/QwenPaw/pull/6606) accepts numeric string line ranges in the `read_file` tool.
- **Memory documentation:** [PR #6604](https://github.com/agentscope-ai/QwenPaw/pull/6604) clarifies how ReMe is used as a self-evolving, file-native personal knowledge base.

**Active PRs worth noting:** [PR #6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) (unifying provider discovery and model metadata) remains open and is a substantial architectural change. [PR #6611](https://github.com/agentscope-ai/QwenPaw/pull/6611) aligns Scroll context and memory with the AgentScope lifecycle, which could reduce the class of memory-related bugs being seen.

---

## 4. Community Hot Topics

1. **[Issue #6537](https://github.com/agentscope-ai/QwenPaw/issues/6537) "Skill tags disappear on restart"** (10 comments, open) — This regression of #3270 is generating significant discussion. Users report that tags saved correctly via API are lost on startup manifest reconciliation. This is a data-persistence bug that likely affects a core workflow (skill management).

2. **[Issue #6601](https://github.com/agentscope-ai/QwenPaw/issues/6601) "QwenPaw 不报空响应错误"** (5 comments, open) — Users report that long sessions approaching the context window limit cause silent empty responses with no error reporting. This is described as a framework-level issue and is causing complete loss of response in long conversations.

3. **[Issue #6563](https://github.com/agentscope-ai/QwenPaw/issues/6563) "CI bug: 'Real behavior proof' workflow blocks all fork PRs"** (5 comments, closed) — A critical contributor-experience issue: the CI workflow fails on every fork PR due to a GitHub token permissions issue, blocking all external contributions. This was closed, but the underlying friction for first-time contributors is a concern.

4. **[Issue #6083](https://github.com/agentscope-ai/QwenPaw/issues/6083) "Desktop 窗口增加工作区产出物快捷访问按钮"** (4 comments, open) — Users want a one-click way to access workspace output files (reports, CSVs, images) from the Desktop window, avoiding manual navigation to `~/.qwenpaw/workspaces/` directories. This has been open since July 14 and has broad appeal for non-technical users.

5. **[Issue #6588](https://github.com/agentscope-ai/QwenPaw/issues/6588) "`spawn_subagent` single-task mode unusable"** (4 comments, open) — A schema validation bug makes single-task subagent spawns fail. A fix PR ([#6609](https://github.com/agentscope-ai/QwenPaw/pull/6609)) is already open.

**Underlying needs:** Users are primarily seeking reliability (persistence, no silent failures) and usability (fewer clicks, better result presentation). The volume of Chinese-language issues suggests a strong East Asian user base with specific UX expectations.

---

## 5. Bugs & Stability

**Ranked by severity:**

1. **HIGH: Shell command execution hangs/UI freezes** — [Issue #6608](https://github.com/agentscope-ai/QwenPaw/issues/6608) documents a 1.5-hour Feishu session block caused by a long-running shell command bypassing timeouts, with orphan subprocesses on cancel. [Issue #6589](https://github.com/agentscope-ai/QwenPaw/issues/6589) reports UI freezes from massive `execute_shell_command` output. **Fix PRs exist:** [#6610](https://github.com/agentscope-ai/QwenPaw/pull/6610) and [#6615](https://github.com/agentscope-ai/QwenPaw/pull/6615).

2. **HIGH: Empty responses with no error in long sessions** — [Issue #6601](https://github.com/agentscope-ai/QwenPaw/issues/6601) causes complete loss of response as context window fills. Framework-level issue with no open fix PR yet.

3. **MEDIUM-HIGH: AgentScope 2.0.4.post1 incompatibility** — [Issue #6612](https://github.com/agentscope-ai/QwenPaw/issues/6612) causes proactive crashes and tool-permission deadlock. **Fix PR open:** [#6615](https://github.com/agentscope-ai/QwenPaw/pull/6615).

4. **MEDIUM: Official shell output truncation** — [Issue #6512](https://github.com/agentscope-ai/QwenPaw/issues/6512) reports >30KB outputs being truncated with possible `Internal error`. No direct fix PR yet.

5. **MEDIUM: `agent.json` systematic corruption** — [Issue #6520](https://github.com/agentscope-ai/QwenPaw/issues/6520) shows BOM, missing quotes, and double-encoding across ~20+ fields on Windows. **Fix PR open:** [#6528](https://github.com/agentscope-ai/QwenPaw/pull/6528).

6. **MEDIUM: WeChat cron silent failure** — [Issue #6614](https://github.com/agentscope-ai/QwenPaw/issues/6614) shows tasks reporting success but never delivering (ret=-2 context_token expiry), burning ~44M tokens in retries.

7. **MEDIUM: Skill tags lost on restart** — [Issue #6537](https://github.com/agentscope-ai/QwenPaw/issues/6537), a regression, has the most comments but no fix PR yet.

8. **LOW: Feishu audio transcription** — [Issue #6544](https://github.com/agentscope-ai/QwenPaw/issues/6544) silently fails; **fix PR #6573 already merged.**

---

## 6. Feature Requests & Roadmap Signals

**Strong signals (multiple comments, clear user demand):**

1. **Workspace output quick access in Desktop** ([#6083](https://github.com/agentscope-ai/QwenPaw/issues/6083)) — Likely to land soon given desktop UX improvements are active (see PR #6607 for a global-hotkey quick-input window).

2. **Collapsible reasoning/tool-call display** ([#6260](https://github.com/agentscope-ai/QwenPaw/issues/6260)) — Users want results front-and-center with process details collapsed. This is a common UX pattern in competing agents.

3. **Storage cleanup / maintenance page** ([#6593](https://github.com/agentscope-ai/QwenPaw/issues/6593)) — Auto-memory and tool calls accumulate data with no way to selectively clean. Requested as a global, not per-agent, feature.

4. **Bundled Python runtime** ([#6160](https://github.com/agentscope-ai/QwenPaw/issues/6160)) — Desktop app should not depend on system Python. Surfaces in environments without Python.

5. **Streaming/large-output handling for shell commands** ([#6512](https://github.com/agentscope-ai/QwenPaw/issues/6512)) — Auto-write to file or support streaming reads; pairs with the UI-freeze bug #6589.

6. **Global hotkey quick-input window** ([#6607](https://github.com/agentscope-ai/QwenPaw/pull/6607)) — Already implemented as a PR, likely for next release.

**Prediction for next version:** Bundled Python runtime, collapsible results, and large-output handling are likely candidates. The Scroll/AgentScope lifecycle refactor ([PR #6611](https://github.com/agentscope-ai/QwenPaw/pull/6611)) also signals a focus on memory reliability.

---

## 7. User Feedback Summary

**Pain points:**
- **Silent failures are the top frustration**: cron jobs show "success" but don't deliver ([#6614](https://github.com/agentscope-ai/QwenPaw/issues/6614)); shell commands hang with no timeout ([#6608](https://github.com/agentscope-ai/QwenPaw/issues/6608)); empty responses are un-reported ([#6601](https://github.com/agentscope-ai/QwenPaw/issues/6601)); audio transcription fails silently ([#6544](https://github.com/agentscope-ai/QwenPaw/issues/6544)).
- **Windows-specific data corruption** ([#6520](https://github.com/agentscope-ai/QwenPaw/issues/6520)) is destructive — users lose entire agent configurations.
- **UI/UX friction**: Input box obstructed in Desktop ([#6549](https://github.com/agentscope-ai/QwenPaw/issues/6549)), results buried under process output ([#6260](https://github.com/agentscope-ai/QwenPaw/issues/6260)), no quick file access ([#6083](https://github.com/agentscope-ai/QwenPaw/issues/6083)).
- **Session integrity**: messages lost or re-rendered when switching modes/sessions ([#6558](https://github.com/agentscope-ai/QwenPaw/issues/6558)) is a trust-breaking bug.

**Satisfaction indicators:**
- Active first-time contributor PRs suggest a welcoming community.
- Quick turnaround on some bugs (audio transcription, session integrity) shows responsiveness.
- Users are actively requesting enhancements (NVIDIA NIM support, global hotkey), indicating they see the product as worth investing in.

**Use cases observed:**
- Financial analysis (stock reports, data migrations with TeslaMate)
- Feishu/WeChat/QQ channel integrations in production settings
- Non-technical users running analysis scripts that produce large outputs

---

## 8. Backlog Watch

**Issues needing maintainer attention (open >3 days without fix PR):**

1. **[Issue #6537](https://github.com/agentscope-ai/QwenPaw/issues/6537)** — Skill tags disappearing on restart (10 comments, open 4 days). High engagement, no fix yet. Regression of a previously fixed issue (#3270).

2. **[Issue #6601](https://github.com/agentscope-ai/QwenPaw/issues/6601)** — Empty responses not reported in long sessions (open 1 day, but framework-level). No fix PR; affects model-agnostic long-context reliability.

3. **[Issue #6512](https://github.com/agentscope-ai/QwenPaw/issues/6512)** — Large shell output truncation (open 4 days). Related to two other open shell issues; a consolidated fix would be valuable.

4. **[Issue #6160](https://github.com/agentscope-ai/QwenPaw/issues/6160)** — Bundled Python runtime request (open 16 days, 4 comments). Common request, no response from maintainers visible.

5. **[Issue #6083](https://github.com/agentscope-ai/QwenPaw/issues/6083)** — Workspace output quick access (open 18 days, 4 comments). Popular request aligned with the desktop hotkey PR; maintainers may want to bundle.

**PRs needing review:**

1. **[PR #6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)** — Provider discovery/metadata unification (open 11 days, no comments from maintainers). Large architectural change that touches many modules; needs dedicated review time.

2. **[PR #6203](https://github.com/agentscope-ai/QwenPaw/pull/6203)** — Windows tasklist probe hardening (open 16 days, under review). Smaller fix with clear value on Windows.

3. **[PR #6543](https://github.com/agentscope-ai/QwenPaw/pull/6543)** — OneBot/QQ text and media handling (open 3 days, under review). Important for the QQ channel users.

**Contributor-experience watch:** The CI fork-PR block ([#6563](https://github.com/agentscope-ai/QwenPaw/issues/6563), now closed) should be verified as fully resolved, as several new first-time-contributor PRs are now arriving — a healthy sign if CI friction doesn't chase them away.

---

*Data source: GitHub API snapshot for agentscope-ai/CoPaw, 2026-08-01 00:00 UTC. All issue/PR links point to the public repository.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Based on the GitHub data for ZeroClaw provided on 2026-08-01 (covering activity from the last 24 hours), here is a structured project digest:

---

### 1. Today's Overview

ZeroClaw is in a period of high architectural activity, dominated by a significant backlog of RFCs (Requests for Comments) that are awaiting maintainer review. The project is actively processing a large volume of issues (50 updated) and pull requests (50 updated), but no new releases were published in the last 24 hours. The core focus is on hardening the system's security posture, redesigning the runtime to become the central owner of session execution, and unifying the tooling and channel landscape. While there is considerable community engagement, a large portion of contributors are blocked on `needs-maintainer-review` or `needs-author-action` labels, indicating a critical bottleneck in the decision-making process. The project is in a "design and RFC" phase rather than a "feature rollout" phase, with many high-risk, high-complexity proposals pending.

### 2. Releases

No new releases were published in the last 24 hours.

---

### 3. Project Progress

The activity in the last 24 hours was focused primarily on bug fixes and incremental improvements rather than major features, as most features are still in the RFC stage. Key updates include:

- **Configuration & Security Fixes:**
    - **PR #9548** (Open): Added a non-blocking warning for risky Codex CLI extra arguments that could weaken sandbox boundaries.
    - **PR #9433** (Open): Enforced tool allowlists in the config validation logic (`ensure_no_escalation_beyond`), fixing a security gap where `allowed_tools`/`excluded_tools` were ignored.
    - **PR #9354** (Closed): Addressed a configuration misperception by adding a warning when WhatsApp Web chat policies are set but cannot take effect due to mode restrictions.
    - **PR #9569** (Open): Fixed a critical security vulnerability (priority: p0) where WhatsApp Cloud and Linq webhooks would process messages without signature verification if a secret wasn't configured, failing open instead of closed.
- **Agent & Runtime Stability:**
    - **PR #9576** (Open): Fixed a multimodal processing bug where the system trimmed entire messages to reduce image count, rather than dropping individual images, which was overly aggressive.
    - **PR #9561** (Open): Removed filename labels from the rendered personality prompt to save tokens and provide cleaner context to the LLM.
    - **PR #8996** (Open): Addressed the preservation of running goals across daemon reloads to prevent session interruption.
- **Tooling & Plugin :**
    - **PR #9554** (Open): Added a new `DagPlanExecuteTool` allowing agents to plan and execute tasks in a DAG (Directed Acyclic Graph) structure, supporting both sequential and parallel execution.
- **Bug Fixes:**
    - **PR #9292** (Open): Fixed a UI bug in the ZeroCode session picker where the scroll offset was lost during mouse hit-testing.
    - **PR #9477** (Open): Improved tool-call parser recovery to handle invocations wrapped in `<tools>` tags, specifically for the Qwen2.5-Coder model.

---

### 4. Community Hot Topics

The most active discussions highlight deep architectural concerns and a desire for more robust controls.

- **RFC: Separate conversation history from long-term memory** ([Issue #9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048)) - **14 comments**
    - **Analysis:** The community is actively debating the lifecycle of data. The current implementation mixes short-term session context with long-term curated memory, and this RFC seeks to define cleaner boundaries. This suggests a push towards more sophisticated memory management and user control over what is retained.

- **RFC: Abstract a `KeySource` trait for master-key material** ([Issue #9127](https://github.com/zeroclaw-labs/zeroclaw/issues/9127)) - **11 comments**
    - **Analysis:** This discussion on security architecture focuses on how master keys are sourced and managed across different deployment forms. It indicates a need for greater flexibility and security compliance, moving beyond hardcoded secrets to integrate with external Key Management Systems (KMS) or environment-specific sources.

- **RFC: Add cross-turn conversation correlation to OTel export** ([Issue #8933](https://github.com/zeroclaw-labs/zeroclaw/issues/8933)) - **9 comments**
    - **Analysis:** With the addition of a Langfuse observer (PR #9556), the community is focused on deep observability. The need to tag telemetry with a `conversation.id` shows a desire to trace the entire lifecycle of a user interaction across multiple turns, enabling better debugging, analysis, and product insight.

- **RFC: Computer-use support for desktop screen interaction** ([Issue #6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)) - **7 comments**
    - **Analysis:** There is clear demand for ZeroClaw to perform beyond chat and APIs, moving into direct desktop automation. The high risk associated with this feature indicates significant concern around security and control, making it a highly requested but slowly progressing capability.

- **RFC: A2A outbound client** ([Issue #9106](https://github.com/zeroclaw-labs/zeroclaw/issues/9106)) - **8 comments**
    - **Analysis:** This topic focuses on enabling ZeroClaw to proactively call other A2A-compliant agents from other platforms. It's a push towards more complex, collaborative, agent-to-agent workflows, positioning ZeroClaw as a central orchestrator rather than a standalone assistant.

---

### 5. Bugs & Stability

The project addressed several significant stability and security issues in the last 24 hours, with a notable focus on fail-closed security.

- **Critical (P0):** 
    - [**PR #9569**](https://github.com/zeroclaw-labs/zeroclaw/pull/9569): Fixed a fail-open vulnerability where WhatsApp Cloud and Linq webhooks skipped signature verification if no secret was configured. This was a high-priority fix to prevent unauthorized message processing.
- **High (P1):**
    - [**Issue #8973**](https://github.com/zeroclaw-labs/zeroclaw/issues/8973): **CLOSED** - Landlock sandbox was blocking `sh` from accessing `/dev/null`, breaking the shell tool on Fedora. This fix is crucial for security-hardened users.
    - [**PR #9576**](https://github.com/zeroclaw-labs/zeroclaw/pull/9576): Fixed overly aggressive multimodal image trimming to resolve issues with message formatting and content loss.
    - [**Issue #8519**](https://github.com/zeroclaw-labs/zeroclaw/issues/8519): Continues to track the reconciliation of cargo-audit/deny ignore lists and remediation of `wasmtime-wasi` CVEs.
- **Medium (P2):**
    - [**Issue #9546**](https://github.com/zeroclaw-labs/zeroclaw/issues/9546): Reported a flaky test in the updater that depends on the host installation state, causing CI failures in certain dev environments.
    - [**PR #9321**](https://github.com/zeroclaw-labs/zeroclaw/pull/9321): Fixed a bug where unauthorized users sending media (not just text) on Telegram were not receiving the "unauthorized notice," leading to silent failures.

---

### 6. Feature Requests & Roadmap Signals

The feature roadmap is heavily oriented toward architectural overhaul and extensibility, with a strong security undercurrent.

- **Runtime as Central Owner:** [Issue #9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) proposes `zeroclaw-runtime` as the single owner of conversation sessions, reducing the role of WebSocket, Web dashboard, and channels to adapters. This signals a move toward a more stable and consistent core.
- **Unified Plugin System:** [Issue #6489](https://github.com/zeroclaw-labs/zeroclaw/issues/6489) calls for collapsing Integrations and Plugins into a single "everything is a plugin" catalog. This would simplify the contributor experience and unify how all capabilities are accessed.
- **Goal-Oriented Autonomy:** [Issue #8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) requests a "Goal mode" for bounded autonomous work, aiming to allow the agent to work towards a single objective without continuous prompting. This is a significant step up in agentic capabilities and could be a major release feature.
- **Enhanced Security & Control:** [Issue #7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) asks for granular confirmation tiers for shell commands, indicating a move beyond simple y/n approvals to more nuanced allow/ask/deny policies.
- **AI-Assisted Workflows:** [Issue #9330](https://github.com/zeroclaw-labs/zeroclaw/issues/9330) proposes AI-assisted PR pre-review, signaling that the project itself is looking to leverage AI to speed up its development workflow.

**Prediction:** The acceptance and implementation of [Issue #9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) (Runtime ownership) and [Issue #9103](https://github.com/zeroclaw-labs/zeroclaw/issues/9103) (Separate memory storage from connectors) would form the foundation for v0.9, as they are the most foundational and widely referenced architectural goals.

---

### 7. User Feedback Summary

User activity in the issues and PRs reveals several key pain points and preferences:

- **Frustration with Security Overhead:** Users like `perillamint` are reporting bugs where the security sandbox (Landlock) breaks core functionality (shell access to `/dev/null`). While the security is valued, these bugs cause significant friction and degrade the user experience.
- **Desire for Security Granularity:** Requests like [Issue #7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) (confirmation tiers for shell commands) show that users desire more control and nuance in the security policies. A blanket allow/deny approach is insufficient; they want to be prompted based on the "riskiness" of the command.
- **Compatibility with Existing Tools:** The push for the OpenAI-compatible endpoint ([Issue #8550](https://github.com/zeroclaw-labs/zeroclaw/issues/8550)) shows a strong desire for ZeroClaw to integrate with the wider ecosystem of clients (Open WebUI, LobeChat) rather than being locked into its own interfaces.
- **Concern for Efficiency:** The PR to remove filename labels from prompts ([PR #9561](https://github.com/zeroclaw-labs/zeroclaw/pull/9561)) reflects a community concern for token efficiency and reducing "noise" sent to the LLM.

---

### 8. Backlog Watch

The project is dealing with a significant bottleneck in the review process. A large number of high-priority, high-risk RFCs are awaiting maintainer decision.

- **Maintainer Decision Queue:** [Issue #8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) is itself a tracker for these unanswered RFCs. Without maintainer action on these, the community's design work cannot progress.
- **Security Review Backlog:** Several critical RFCs from June (e.g., [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) Shell policy, [#6971](https://github.com/zeroclaw-labs/zeroclaw/issues/6971) Security UX) remain open with a `needs-maintainer-review` label, posing a risk to the project's security evolution.
- **Observability Backlog:** RFCs for structured observability ([#7232](https://github.com/zeroclaw-labs/zeroclaw/issues/7232)) and cross-turn correlation ([#8933](https://github.com/zeroclaw-labs/zeroclaw/issues/8933)) are also waiting in the queue, delaying the project's monitoring and debugging capabilities.
- **"Won't Fix" Decisions:** Many PRs are also labeled with `needs-author-action` (e.g., [#8996](https://github.com/zeroclaw-labs/zeroclaw/pull/8996), [#9548](https://github.com/zeroclaw-labs/zeroclaw/pull/9548)), indicating that while the maintainers have reviewed them, the original authors need to respond to feedback. This could either lead to a quick convergence or stalled contributions if not addressed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*