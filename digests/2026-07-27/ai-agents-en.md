# OpenClaw Ecosystem Digest 2026-07-27

> Issues: 345 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-27 01:30 UTC

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

# OpenClaw Project Digest — 2026-07-27

## Today's Overview

OpenClaw is in a period of **very high activity**, with 345 issues and 500 PRs updated in the last 24 hours. The project maintains strong community engagement (247 open issues, 175 open PRs) but faces significant maintainer bandwidth pressure — the majority of top issues carry `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision` labels, indicating a bottleneck in triage and decision-making. No new releases were cut today, and the project shows a healthy closure rate with 98 issues and 325 PRs closed/merged. However, there are no signs of a near-term beta or stable release candidate. The volume of P1 bugs (session-state corruption, message loss, crash loops) suggests the project is deep in a stabilization and bug-fixing phase.

## Releases

**None.** No new releases were published today.

## Project Progress

325 PRs were closed or merged today. Notable changes that advanced:

- **Core infrastructure**: PR [#114219](https://github.com/openclaw/openclaw/pull/114219) (steipete) refactored abort-reason preservation for restart recovery — replaces fragile string matching with a structured code path.
- **UI fixes**: PR [#114223](https://github.com/openclaw/openclaw/pull/114223) (steipete) fixed the macOS tray icon drawing; PR [#114224](https://github.com/openclaw/openclaw/pull/114224) (steipete) improved cron failure detail in sidebar tooltip.
- **Provider consolidation**: PR [#114221](https://github.com/openclaw/openclaw/pull/114221) (steipete, closed) unified Anthropic and OpenAI admin usage reporting, eliminating duplicate credential cleanup and aggregation logic.
- **Codex compatibility**: PR [#107588](https://github.com/openclaw/openclaw/pull/107588) (VACInc, closed) fixed thinking and fast control presets being incorrectly stripped on Codex routes.
- **Telegram ingress**: PR [#114222](https://github.com/openclaw/openclaw/pull/114222) (backmeupplz, closed) preserved timeout diagnostics for Telegram durable-ingress handlers, helping recovery distinguish between timeouts and other aborts.
- **Dependency cleanup**: PR [#114218](https://github.com/openclaw/openclaw/pull/114218) (steipete) removed stale ownership-manifest entries for `glob` and `markdown-it`.

## Community Hot Topics

### Most Active Issues (by comment count)

1. **#75 — [ENHANCEMENT] Linux/Windows Clawdbot Apps** (115 comments, 👍80)  
   [Issue link](https://github.com/openclaw/openclaw/issues/75)  
   *User need:* The long-running request for desktop apps on non-Apple platforms remains the #1 community feature demand. Despite high engagement, it carries multiple `clawsweeper:needs-*` blockers (product-decision, security-review, maintainer-review).

2. **#99241 — Tool outputs render as unreadable image attachments** (24 comments, 👍2)  
   [Issue link](https://github.com/openclaw/openclaw/issues/99241)  
   *User need:* A critical P1 bug where ANSI-heavy tool outputs collapse into image placeholders that agents can't read — making LLM-driven workflows that rely on tool stdout effectively blind. No fix PR exists.

3. **#102020 — Second message fails with "reply session initialization conflicted"** (15 comments, 👍1)  
   [Issue link](https://github.com/openclaw/openclaw/issues/102020)  
   *User need:* A position-dependent, cross-channel bug that corrupts every second session turn. Still awaiting maintainer review and info.

4. **#86996 — Active Memory + Codex causes long latency, hook timeouts, startup aborts** (13 comments, 👍2)  
   [Issue link](https://github.com/openclaw/openclaw/issues/86996)  
   *User need:* A P1 diamond-lobster severity issue combining Active Memory, lossless-claw context engine, and Codex models. Multiple system health indicators degrade simultaneously.

5. **#86519 — Duplicate Telegram replies after 5.20 update** (12 comments, 👍1)  
   [Issue link](https://github.com/openclaw/openclaw/issues/86519)  
   *User need:* Regression causing 2-10x duplicate replies on Telegram. Partially mitigated by 5.22 update but not fully resolved.

### Most Active PRs

- **#114219 — refactor(ai): preserve abort reasons** (steipete) — Core restart recovery improvement, 0 comments but significant structural change.
- **#86655 — feat(claude): add claude-bridge app-server harness extension** (zeroaltitude) — The Claude parity PR, still open since May 25 with no maintainer decision despite being XL-sized with multiple merge risks.
- **#112000 — refactor(prompt): use plain inbound context labels** (jesse-merhi, closed) — Large prompt-security refactor, closed today after a week of review.

## Bugs & Stability

### P0/P1 Active Bugs (with high impact)

| Issue | Severity | Impact | Fix PR |
|-------|----------|--------|--------|
| [#112423](https://github.com/openclaw/openclaw/issues/112423) — Large SQLite transcript cleanup blocks gateway event loop | P1 | Session-state, event-loop stall | None |
| [#113315](https://github.com/openclaw/openclaw/issues/113315) — Telegram inbound update permanently lost after offset persistence | P1 | Message loss | None |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) — Active Memory + Codex → hook timeouts, crash loops | P1 | Message loss, auth-provider, crash-loop | None |
| [#92043](https://github.com/openclaw/openclaw/issues/92043) — 180s compaction timeout with no partial-progress reuse | P1 | Session-state, crash-loop | None |
| [#102020](https://github.com/openclaw/openclaw/issues/102020) — Second message "session initialization conflicted" | P1 | Session-state, message loss | None |
| [#90378](https://github.com/openclaw/openclaw/issues/90378) — Cron store migration to SQLite silently breaks jobs (P0) | **P0** | Session-state, data loss, message loss | Linked PR open |
| [#99241](https://github.com/openclaw/openclaw/issues/99241) — Tool outputs as unreadable image attachments | P1 | Session-state, message loss | None |
| [#86519](https://github.com/openclaw/openclaw/issues/86519) — Duplicate Telegram replies (regression, 5.20+) | P1 | Message loss | None |

### New or Updated Bugs (last 24h)

- **#113474** (CLOSED) — Gateway crash loop on Raspberry Pi 5 with repeated offline/online cycling. Resolved but underscores edge-case platform fragility.
- **#113315** (UPDATED) — Telegram inbound update permanently lost after offset persistence — a critical P1 with no ingress log, spool, or dispatch (maintainer needs more info).
- **#112423** (UPDATED) — Large SQLite transcript cleanup blocks the gateway event loop — ongoing P1 with no fix PR.
- **#106403** (UPDATED) — Terminal-main reconciliation gate silently resets healthy main session due to mtime race — P1 diamond lobster with source repro available.

### Critical Observations

- **8 of top 10 issues by comment count are P1 bugs.** This is an unusually high concentration of severity.
- **Session-state and message-loss** are the dominant impact categories, suggesting fundamental streaming/state-management issues.
- **No fix PR exists for any of the top P1 bugs.** Most have `clawsweeper:no-new-fix-pr` enforced, meaning the project is deliberately not accepting new fixes — possibly during a consolidation phase.

## Feature Requests & Roadmap Signals

### Most Requested Features (by reaction count)

| Issue | Feature | 👍 | Status |
|-------|---------|----|--------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows Clawdbot Apps | 80 | Needs product decision (since Jan 2026) |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) | Denylist support for exec-approvals | 8 | Needs product-decision, security-review |
| [#67413](https://github.com/openclaw/openclaw/issues/67413) | Per-agent dreaming configuration | 5 | Needs product-decision, linked PR open |
| [#42026](https://github.com/openclaw/openclaw/issues/42026) | Distributed Agent Runtime (control plane separation) | 3 | Stale since Mar 2026, needs decision |
| [#8892](https://github.com/openclaw/openclaw/issues/8892) | `--agent` flag for TUI | 3 | Needs product-decision & maintainer review |

### Likely Roadmap Candidates (next 1-2 releases)

- **Per-agent dreaming configuration** (#67413) has a linked PR and active shape-clear status — most likely to ship.
- **Exec-approval denylist** (#6615) has high demand and a linked PR but needs security review.
- **Skill Permission Manifest Standard** (#12219) aligns with recent security-conscious releases.
- **Isolated cron jobs per agent** (#26370) — a P1 enhancement that was closed but the underlying need (multi-tenant isolation) keeps resurfacing.

### Unlikely to ship soon

- **Linux/Windows desktop apps** (#75) — has sat since January 2026 with 115 comments and no PR. The `needs-product-decision` label suggests it's not a priority.
- **Distributed Agent Runtime** (#42026) — stale since March, no progress. Too architecturally invasive for current stabilization phase.

## User Feedback Summary

### Common Pain Points

1. **Session reliability is the #1 complaint.** Multiple P1 bugs cause sessions to wedge, duplicate messages, lose context, or silently drop replies. Users report this across Telegram, Discord, Signal, and WebChat channels.
2. **State corruption after upgrades.** Users migrating between minor versions (5.28→6.1, 5.20→5.22, 6.11→6.7.2-beta) experience silent state corruption — cron store migration, session reset, feature regressions.
3. **Codex/Ollama remote providers are unreliable.** Multiple issues describe streaming not being consumed (`model_call:started` never progresses), hooks starving, and recovery being unable to distinguish timeouts from real failures.
4. **Memory management is fragile.** Active Memory + Codex combinations cause cascading failures. Compaction timeouts don't reuse partial progress. Dreaming has no per-agent control.
5. **Plugin and tool boundary gaps.** Users want denylists, per-spawn tool restrictions, skill permission manifests, and proper HITL approval APIs — all of which are stuck awaiting product decisions.

### Positive Signals

- Active community with detailed bug reports including environment, reproduction steps, and logs.
- Maintainers (especially steipete) are actively refactoring core infrastructure — abort reasons, provider aggregation, state verifiers, memory embedding defaults.
- The project has a sophisticated labeling and severity system (`clawsweeper-*` labels, diamond/lobster/hermit ratings) that suggests good internal triage processes despite external bottlenecks.

### Frustration Indicators

- 5+ issues labeled `stale` that are also P1 — meaning critical bugs are aging out.
- The `clawsweeper:no-new-fix-pr` label appears on nearly every top issue, suggesting the project is refusing new fixes while dealing with existing PRs.
- Multiple users report "regression that worked before, now fails" — signs of inadequate regression testing on release candidates.

## Backlog Watch

### Long-unanswered Important Issues (stale or awaiting action >30 days)

| Issue | Age | Label | Concern |
|-------|-----|-------|---------|
| [#42026](https://github.com/openclaw/openclaw/issues/42026) — Distributed Agent Runtime | 130+ days | `stale`, P2 | Architectural RFC with no decision since March |
| [#85251](https://github.com/openclaw/openclaw/issues/85251) — Codex app-server goes silent mid-turn | 60+ days | `stale`, P1, `needs-live-repro` | High severity, no repro means it may never be fixed |
| [#86963](https://github.com/openclaw/openclaw/issues/86963) — Orphaned Codex thread wedges session permanently | 60+ days | `stale`, P1, `needs-live-repro` | Silent message dropping — deeply concerning |
| [#91892](https://github.com/openclaw/openclaw/issues/91892) — Cron jobs stall during AI model calls | 46+ days | `stale`, P1 | Cron reliability is core to the project's value proposition |
| [#94251](https://github.com/openclaw/openclaw/issues/94251) — Ollama streaming not consumed | 40+ days | P1 | Affects all local-model users; has linked PR but also needs live repro |

### PRs Needing Maintainer Attention (long-open, no decision)

| PR | Age | Size/Risk | Status |
|----|-----|-----------|--------|
| [#86655](https://github.com/openclaw/openclaw/pull/86655) — Claude bridge extension | 63 days | XL, 3 merge risks | Needs proof — the most consequential open PR |
| [#75299](https://github.com/openclaw/openclaw/pull/75299) — Starvation guard for priority queue | 88 days | S, 1 merge risk | Waiting on author since April |
| [#82950](https://github.com/openclaw/openclaw/pull/82950) — ReDoS guard for exec approval | 71 days | M, 2 merge risks | Waiting on author since May — security fix |
| [#97192](https://github.com/openclaw/openclaw/pull/97192) — Sandbox escape tests for skill loader | 30 days | M | Waiting on author — test-only PR |

**Backlash Risk:** The growing list of stale P1 bugs (particularly those causing silent message loss) combined with no-fix-PR policy and long-unanswered product-decisions may erode community trust. Several user reports indicate repeated regressions across minor version bumps, which suggests the project could benefit from a stabilization release with fewer features and more regression testing.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided digests.

---

### 1. Ecosystem Overview

The personal AI assistant and agent open-source landscape on July 27, 2026, is characterized by a **heavy focus on stability and security hardening** after a period of rapid feature growth. While projects like OpenClaw, Zeroclaw, and NanoBot are deep in bug-fixing and stabilization phases, others like Moltis and IronClaw are pushing significant architectural boundaries (bidirectional ACP, error-recoverability frameworks). The community's primary pain points center on session reliability, cross-platform parity (especially Windows/Linux), and managing the complexity of multi-provider and multi-channel integrations. Overall, the ecosystem is maturing from experimental features toward production-grade reliability.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status (24h) | Health Score & Key Signal |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 345 | 500 | No new release | **Moderate**. Very high activity but bottlenecked by maintainer review (`clawsweeper:needs-*` labels). Deep bug-fixing phase, with 8 of top 10 issues as P1 bugs. |
| **NanoBot** | 9 | 29 | No new release | **Strong**. High merge rate (76%), rapid fix turnaround for memory, MCP, and runtime issues. Active community contributing null-safe fixes. |
| **Hermes Agent** | 50 | 50 | No new release (v0.19.0 latest) | **Strong**. High-velocity maintenance with 16 PRs merged/closed. Major features landed (`/diff`, Desktop Artifacts) alongside critical patches (session pruning, skill registry, RCE fix). |
| **PicoClaw** | 4 | 7 | No new release | **Good**. Moderate activity, processing community contributions (security, new provider). One critical DoS bug with a fix in review. |
| **NanoClaw** | 2 | 9 | No new release | **Cautionary**. High-impact regression from a recent breaking change (silent reply drops). Other critical messaging reliability bugs with no fix. |
| **NullClaw** | 0 | 0 | No new release (v2026.5.29) | **Low**. Near-zero activity. A single, critical SIGSEGV bug on aarch64/Telegram remains unresolved for 11 days with no maintainer response. |
| **IronClaw** | 4 | 17 | No new release | **Strong**. Intense engineering push on error-recoverability framework. Core contributors actively closing large refactors; active mentorship of new contributors. |
| **LobsterAI** | 2 | 8 | No new release (v2026.4.1) | **Weak**. Very low activity, project appears under-maintained. Critical gateway restart bug open for 117 days with no response. 7 PRs stale since April. |
| **TinyClaw** | 0 | 0 | No new release | **Inactive**. No activity in the last 24 hours. |
| **Moltis** | 0 | 8 | No new release | **Moderate**. High feature velocity from core maintainers (zero community churn). No merged PRs, but 8 feature-heavy PRs are near merge-ready. No public bug reports. |
| **CoPaw** | 11 | 7 | No new release (v2.0.1 latest) | **Cautionary**. Moderate activity with zero PRs merged. Healthy community contributors but constrained maintainer bandwidth. Several critical/v2.0.1 regression bugs unfixed. |
| **Zeroclaw** | 50 | 48 | No new release (v0.8.4 RC in prep) | **Strong**. High-intensity development push for v0.8.4. Strong community contributions (security, channels). Active maintainer engagement with multiple focused patches. |

### 3. OpenClaw’s Position

OpenClaw remains the **largest and most active project** in the ecosystem by raw volume (345 issues, 500 PRs updated), but this scale poses significant challenges.

- **Advantages vs. Peers:** It has the most mature labeling, triage, and severity systems (e.g., `clawsweeper-*`, diamond/lobster/hermit ratings), suggesting robust internal processes. Key contributors like `steipete` are actively refactoring core infrastructure (abort reasons, provider aggregation). Feature breadth (Telegram, Discord, Signal, WebChat, Codex, Ollama) is a clear strength.
- **Technical Approach Differences:** OpenClaw’s architecture involves a modular "claw" pattern (memory, exec, skills) and a higher degree of abstraction, which, while powerful, leads to session-state and message-loss bugs that are its #1 user complaint. Its approach contrasts with Moltis' more focused, client-server ACP model or NanoBot's lightweight Python focus.
- **Community Size:** Its community is the largest and most vocal, providing detailed bug reports. However, the loudest feedback is frustration over repeated regressions and a growing backlog of stale P1 bugs, a dynamic less pronounced in smaller, higher-velocity projects like NanoBot.

**Verdict:** OpenClaw is the ecosystem's "operating system," but its stability phase is exposing the cost of its own complexity. Peers like IronClaw are methodically solving similar reliability problems with more focused architectural refactors.

### 4. Shared Technical Focus Areas

Emerging requirements that cut across multiple projects:

- **Session & Message Reliability (ALL):** Every major project (OpenClaw, NanoBot, Nanoclaw, Nullclaw, CoPaw) is dealing with some form of message loss, duplicate delivery, session corruption, or state-management bugs. This is the **single most critical shared pain point**.
- **Provider/Model Integration Parity & Robustness:** All projects are building toward multi-model support. Pain points include: streaming not being consumed (OpenClaw/Ollama), MCP schema rejection (NanoBot/Kimi), and API key security (Zeroclaw/Gemini). **Project-specific need: OpenClaw, PicoClaw, CoPaw**.
- **Security, Sandboxing, & Credential Management:** A strong theme across IronClaw, Zeroclaw, and Moltis. Concerns include: preventing arbitrary command execution (Moltis), Landlock sandbox fragility (Zeroclaw), SSRF prevention (Zeroclaw, NanoBot), and credential leaks/rotations (OpenClaw, Zeroclaw).
- **Windows/Linux Desktop Parity:** OpenClaw, Hermes, and Nanoclaw all have open issues for non-Apple desktop apps. **Project-specific need: OpenClaw** (Linux/Windows Clawdbot Apps), **Hermes** (GUI-only Desktop install), **CoPaw** (Windows PATH bug, Linux Sway support).
- **Performance on Low-Power Devices (Raspberry Pi):** Specifically mention in NanoBot and OpenClaw, indicating growing demand for edge deployment.
- **Human-in-the-Loop (HITL) & Approval Workflows:** Denylists for exec-approvals (OpenClaw), per-spawn tool restrictions (OpenClaw, Moltis), and `notice_after_complete` mechanisms (CoPaw) show a move toward safer, supervised automation.

### 5. Differentiation Analysis

| Feature / Focus | Project(s) Leading | Key Architectural Difference |
| :--- | :--- | :--- |
| **Error-Recoverability & Stability** | **IronClaw** | Methodically building a formal `FailureKind` vocabulary; every error is survivable. This is a more disciplined approach than the "stabilize through bug-fix" cycles in OpenClaw. |
| **Bidirectional ACP / Interop** | **Moltis** | Pushing beyond client-only ACP to become a full agent endpoint (e.g., for Buzz and Zed). This is a unique focus on agent-hosting infrastructure over feature breadth. |
| **Lightweight Python Focus** | **NanoBot** | Emphasizes rapid fix turnaround and ease of contribution, targeting developers who want a simpler stack. It contrasts with the Rust-heavy IronClaw/Zeroclaw. |
| **Desktop Artifacts & UX** | **Hermes Agent** | Landing Claude-style Desktop Artifacts and a long-awaited `/diff` command, focusing on developer experience and feature parity with hosted products. |
| **Modular "Claw" Architecture** | **OpenClaw** | Highest complexity and scale, but the most comprehensive feature set (Telegram, Discord, Signal, Codex, Active Memory). Its modularity is both a strength and a source of state-management bugs. |
| **Cross-Platform Desktop (non-Apple)** | **All major projects** | A clear gap in the ecosystem. No project has an official, stable Linux/Windows desktop app. |
| **Edge Deployment (RPi)** | **NanoBot, OpenClaw** | Special attention is being paid to CPU usage, compaction, and performance on low-power devices. |
| **Video/Media Pipelines** | **CoPaw** | Has a unique `view_video` feature and a "Creator" app for video generation, signaling a niche in creative and media production use cases. |

### 6. Community Momentum & Maturity

- **Tier 1: High Momentum / Actively Iterating**
    - **NanoBot:** Excellent fix-to-issue turnaround with strong community code ownership. Best health score.
    - **Hermes Agent:** High-velocity feature development and bug fixes with a receptive community. Strong.
    - **IronClaw:** Intense, focused engineering with a clear architectural roadmap. Strong.
    - **Zeroclaw:** High activity, clear release goals (v0.8.4), and strong maintainer engagement. Strong.
- **Tier 2: Moderate Momentum / Stabilizing**
    - **OpenClaw:** Very high activity but showing signs of "feverish" churn, with a mixed health score. Long-term strong, but currently stressed.
    - **Moltis:** High feature velocity from a core team, but zero community engagement. Unclear sustainability.
    - **PicoClaw:** Healthy community contribution pipeline but moderate overall velocity.
- **Tier 3: Cautionary / Low Momentum**
    - **Nanoclaw:** High-impact regression from a recent change is a red flag. Core messaging reliability is compromised.
    - **CoPaw:** Healthy community PRs are being submitted, but the zero-merge rate and critical v2.0.1 bugs are a concern.
    - **LobsterAI, NullClaw, TinyClaw, ZeptoClaw:** These projects show signs of being under-maintained, inactive, or critically broken. They are currently a risk for adopters.

### 7. Trend Signals

Observations valuable for AI agent developers evaluating the ecosystem:

- **"Stability is the new feature."** The market is saturated with experimental features. The winning projects will be those that can guarantee message delivery, session persistence, and error recovery. IronClaw's formal approach to this is a leading indicator.
- **Docker and Edge are the new "first-class" platforms.** The focus on Landlock, SSRF prevention, RPi CPU usage, and systemd integration shows the ecosystem is targeting production deployments, not just hobbyist setups. Security is a prerequisite for operationalization.
- **The "Chat Gateway" is commoditizing.** Providing Telegram, Discord, or WhatsApp integration is no longer a differentiator; it is table stakes. The new differentiators are **reliability of that connection** (no dropped or duplicate messages) and **security of that channel** (preventing arbitrary code execution).
- **Agent-to-Agent (A2A) communication is the next frontier.** Moltis's push for bidirectional ACP and OpenClaw's Distributed Agent Runtime request point to a future where the value is in agent orchestration, not just a single agent session. Developers should watch for standard protocols emerging.
- **User demand for self-service controls is rising.** HITL approval workflows, per-agent permissions, and denylists are becoming non-negotiable features for users moving from prototypes to real-world deployment.
- **Cross-platform neglect is a significant risk.** The lack of stable non-Apple desktop support (OpenClaw, Hermes) and specifically Windows parity (CoPaw, Zeroclaw) leaves a large market segment underserved and creates friction for enterprise adoption.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-27

## Today's Overview
The NanoBot project is in an **intense maintenance and stabilization phase** with 29 PRs and 9 Issues updated in the last 24 hours. Activity is concentrated on bug fixes (especially memory, MCP tool schema, and runtime context preservation) with a 76% merge/close rate (22 of 29 PRs merged or closed). The community-driven **unified extension platform** PR (#5098) signals a potential architectural shift ahead. Overall project health is strong, with rapid issue-to-fix turnaround observed across multiple critical stability problems.

## Releases
*No new releases today.* The latest release remains `nanobot-ai==0.2.2`, referenced in the length recovery issue (#5051).

## Project Progress
**22 PRs merged or closed today**, demonstrating high-velocity maintenance:

**Memory & Dream System (3 PRs):**
- [#5054](HKUDS/nanobot/pull/5054) — **Fix:** Progress past completed no-op Dream batches, preventing starvation of later history entries
- [#5099](HKUDS/nanobot/pull/5099) — **Fix:** Preserve unprocessed dream history entries newer than the cursor during compaction
- [#5087](HKUDS/nanobot/pull/5087) — **Fix:** Treat null `runHistory` as empty when loading triggers (cron edge case)

**Agent & Runtime (3 PRs):**
- [#5056](HKUDS/nanobot/pull/5056) — **Fix:** Preserve output across length recovery (accumulate contiguous segments)
- [#5084](HKUDS/nanobot/pull/5084) — **Fix:** Preserve pending message runtime context (sender/channel/chat metadata)
- [#5036](HKUDS/nanobot/pull/5036) — **Feat:** Make idle compaction scan interval configurable (30-40% CPU fix on Raspberry Pi)

**MCP & Provider (2 PRs):**
- [#5057](HKUDS/nanobot/pull/5057) — **Fix:** Normalize local schema refs in MCP tools (prevents Kimi/Moonshot rejection)
- [#5101](HKUDS/nanobot/pull/5101) — **Fix:** Honor provider proxy for URL downloads (image generation)

**Channels & Connectivity (4 PRs):**
- [#5069](HKUDS/nanobot/pull/5069) — **Fix:** Ignore confirmations after connect cancellation (WeChat/Feishu credential safety)
- [#4928](HKUDS/nanobot/pull/4928) — **Fix:** Route unified sessions to last channel via persisted metadata
- [#4446](HKUDS/nanobot/pull/4446) — **Feat:** DingTalk: gate private chats and mention sender in group replies
- [#5089](HKUDS/nanobot/pull/5089) — **Fix:** Tolerate null `multi_url` and list fields in Feishu card extract

**WebUI (2 PRs):**
- [#4603](HKUDS/nanobot/pull/4603) — **Refactor:** Stop mutating `tool_call.id` for WebUI file-edit progress correlation
- [#5100](HKUDS/nanobot/pull/5100) — **Fix:** Prevent long messages from widening mobile thread viewport

**Sandbox & Security (2 PRs):**
- [#4625](HKUDS/nanobot/pull/4625) — **Feat:** Allow extra bwrap bind roots (configurable tool directories)
- [#5095](HKUDS/nanobot/pull/5095) — **Fix:** Harden generated image URL downloads (SSRF protection, DNS pinning)

**Tooling & CLI (2 PRs):**
- [#4939](HKUDS/nanobot/pull/4939) — **Fix:** Support Codex OAuth in Quick Start CLI
- [#4656](HKUDS/nanobot/pull/4656) — **Fix:** Pass aspect ratio and size to Gemini Flash image models

## Community Hot Topics

### Most Active Issues

1. **#4924** [CLOSED] — `_pick_heartbeat_target_from_sessions` fails with unified session (*4 comments*)
   [HKUDS/nanobot/issues/4924](HKUDS/nanobot/issues/4924)
   *Root cause identified and fixed in #4928; community engaging on edge cases with empty session lists.*

2. **#1012** [OPEN] — Add subagent profiles with configurable tools and skills (*2 comments, 8 months old*)
   [HKUDS/nanobot/issues/1012](HKUDS/nanobot/issues/1012)
   *Persistent request for specialized agent types; no recent maintainer engagement. Underlying need: differentiate research, coding, and support agents with distinct tool sets.*

3. **#4792** [OPEN] — `/stop` silently discards pending queue messages (*2 comments*)
   [HKUDS/nanobot/issues/4792](HKUDS/nanobot/issues/4792)
   *Describes permanent message loss scenario; maintainer activity suggests potential fix in progress via #5084.*

### Most Active PRs

- **#5098** [OPEN] — Unified extension platform (*feature, enhancement, documentation*)
  [HKUDS/nanobot/pull/5098](HKUDS/nanobot/pull/5098)
  *Major architectural proposal — unified catalog, transactional lifecycle, multi-provider compatibility. Low comment count but high structural impact.*

- **#4301** [OPEN with conflict] — Cache skills loader entries and metadata
  [HKUDS/nanobot/pull/4301](HKUDS/nanobot/pull/4301)
  *Performance improvement with merge conflict blocking; repeated directory scans discussed as pain point since June.*

**Underlying community dynamics:** Users are optimizing for **performance** (Raspberry Pi CPU usage, skill loader caching) and **stability** (message loss, MCP schema rejection, Dream starvation). The subagent profiles request (#1012) indicates demand for architectural flexibility.

## Bugs & Stability

### Critical Severity

1. **Pending message loss** (#4792) — `/stop` command permanently discards queued messages; **fix PR #5084** addresses runtime context but not the re-publish gap described in the issue. *(OPEN, fix confirmed partial)*

2. **AgentRunner length recovery data loss** (#5051) — `final_content` only contains last continuation segment; earlier segments lost. **Fixed in PR #5056** (merged). *(CLOSED)*

### High Severity

3. **Dream batch starvation** (#5041) — Completed no-op Dream runs don't advance cursor; first batch selected repeatedly. **Fixed in PR #5054** (merged). *(CLOSED)*

4. **MCP tool schema rejection** (#5040) — Non-`#/$defs/` `$ref` disables entire model on Kimi/Moonshot. **Fixed in PR #5057** (merged). *(CLOSED)*

5. **Null pointer crashes** — Three PRs addressed null field handling: pairing maps (#5088), triggers history (#5087), Feishu card buttons (#5089). All merged today. *(CLOSED)*

### Medium Severity

6. **Unified session heartbeat failure** (#4924) — No sessions with unified session enabled breaks target selection. **Fixed in PR #4928** (merged). *(CLOSED)*

7. **Memory compaction destroying unprocessed dream history** — Addressed by PR #5099 *(OPEN, fix pending merge)*

8. **Mid-turn message context loss** (#4064) — Queued messages lack runtime identity metadata. **Fixed in PR #5084** (merged). *(CLOSED)*

9. **WebUI mobile viewport widening** (#5100) — Long unbroken Markdown breaks mobile layout. **Fix merged today.** *(CLOSED)*

## Feature Requests & Roadmap Signals

| Feature | Issue/PR | Status | Likely Version |
|---------|----------|--------|----------------|
| Subagent profiles with configurable tools | #1012 | Stale (8 months) | TBD — architectural change needed |
| Unified extension platform | #5098 | Open PR | v0.3+ — major new capability |
| Idle compaction configurable | #5036 | Merged | v0.2.3 |
| Codex OAuth in CLI | #4939 | Merged | v0.2.3 |
| DingTalk private chat gating | #4446 | Merged | v0.2.3 |
| Extra bwrap bind mounts | #4625 | Merged | v0.2.3 |

**Prediction for next minor release (v0.2.3):** The dense bug-fix velocity suggests a near-term patch release incorporating the 22 merged PRs from this period. The extension platform (#5098) would be a v0.3+ feature given its architectural scope.

## User Feedback Summary

**Pain Points (from Issues):**
- **Performance on low-power devices:** User `khmylov` reports 30-40% CPU usage on Raspberry Pi due to aggressive idle compaction (resolved in #5036)
- **Message integrity concerns:** User `hamb1y` reports permanent message loss with `/stop` (#4792) and context loss for mid-turn messages (#4064) — both addressed or in progress
- **Provider compatibility friction:** User `3L1AS` reports MCP tool schema rejection on Kimi/Moonshot (#5040) — fixed
- **Memory system confusion:** User `dajiaohuang` reports Dream starvation (#5041) — fixed; remains a complex subsystem

**User Behaviors Observed:**
- Three open-source contributors independently submitted null-safe fixes (#5087, #5088, #5089) within hours — strong community code ownership
- DingTalk operator (`lmzopq`) contributes enterprise-channel features with privacy controls
- Raspberry Pi deployment growing; performance tuning becoming community demand

**Satisfaction Indicators:**
- 22 PRs merged with zero re-opened issues — high fix quality
- Stale issue #1012 (subagent profiles) remains the longest-standing open request, suggesting maintainers are prioritizing stability over new architecture

## Backlog Watch

1. **[#1012](HKUDS/nanobot/issues/1012)** — Add subagent profiles (8 months open, 2 comments)
   *Maintainer attention needed: one of the oldest open feature requests. Community may perceive as deprioritized.*

2. **[#4301](HKUDS/nanobot/pull/4301)** — Cache skills loader entries (merge conflict, 46 days open)
   *Blocked performance improvement; could benefit from friction review by maintainers.*

3. **[#4792](HKUDS/nanobot/issues/4792)** — `/stop` message loss (21 days open, no fix PR)
   *Only critical-severity issue without a confirmed fix; partial progress in #5084 but gap remains.*

4. **[#5099](HKUDS/nanobot/pull/5099)** — Preserve unprocessed dream history (1 day open)
   *Newly opened; needs review and merge to prevent memory regression from earlier compaction fixes.*

---

*Digest generated 2026-07-27. Data source: GitHub API (HKUDS/nanobot).*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-27

## Today's Overview

The project sustained very high activity on 2026-07-27, with 50 issues and 50 PRs updated in the last 24 hours across a broad surface area. Maintenance velocity remains strong: 14 issues were closed, and 16 PRs were merged or closed, including a cluster of security patches, dependency fixes, and a major Desktop artifact feature. No new releases were cut today, though the project appears poised for a patch release given the volume of P0/P1 fixes landed. Key areas of focus included Anthropic proxy session affinity, session pruning correctness, skill registry integrity, and the ongoing campaign against SQLite WAL-reset vulnerabilities in the Docker image.

## Releases

No new releases today (as of 2026-07-27). The latest tagged version is v0.19.0 (v2026.7.20). Given the volume of P0/P1 fixes committed today, a patch release (v0.19.1) appears imminent.

## Project Progress

Sixteen PRs were merged or closed today. Notable advances:

- **📋 `/diff` Command Landed (finally):** After three prior attempts over four months (PRs #4839, #22703, #53527), salvage PR #72240 by @teknium1 unified `/diff` with staged/all/session modes across CLI, gateway, and TUI. Hermes now answers "what did you change this session?".
- **Desktop Artifacts (Claude-style):** PR #72345 introduces versioned cards, sandboxed live preview, and a right-rail viewer for generated content — a major feature gap vs. hosted competitors.
- **Anthropic Proxy Session Affinity:** PR #72369 preserves stable conversation affinity across tool loops, credential rotation, and provider fallback — addressing a critical caching and cost issue.
- **Dependency CVE Pins Updated:** PR #72362 moves `cryptography`, `starlette`, and `python-multipart` to current patched versions, fixing downgrade behavior on `hermes update`.

## Community Hot Topics

The following items generated significant discussion and reactions:

- **#68871 – Buzz Integration (15 comments, 13 👍)** — The most active open feature request. User @mwhuss proposes integrating Block's open-source Buzz workspace for human+agent messaging rooms. The high reaction count and comment volume suggest strong community demand for alternative messaging backends beyond Telegram/Matrix.

- **#62936 – Telegram Upload Timeout (7 comments)** — Long-standing bug report from @KShad10 where large media uploads (>15 MB) always time out because `HERMES_TELEGRAM_HTTP_WRITE_TIMEOUT` doesn't propagate to the PTB media `write_timeout`. Still open with no merged fix.

- **#72298 – Passwords Leaked in Telegram Chat (2 comments, 7 👍)** — A high-reaction security bug report from @facundopadilla where Hermes inadvertently shows passwords in Telegram chat output during skill execution. Marked `needs-repro` but the reaction count signals alarm.

- **#60783 – huggingface-hub Dependency Conflict (7 comments)** — Resolved a pin conflict where `lazy_deps` pinned `huggingface-hub==1.2.3` but `sentence-transformers` required `>=1.5.0`, breaking Hindsight local embeddings. Now closed.

## Bugs & Stability

**P0 (Critical):**
- **Session Pruning Data Loss (PR #72358)** — Auto-prune could delete recently-active conversations created long ago because the age check used `started_at` instead of `last_active_at`. Fix landed today.
- **Skill Registry Hijack (PR #72354)** — `hermes skills update` could silently replace an installed skill with a same-named skill from a different registry, causing data loss. Fix landed.
- **Anthropic Cache Breakpoint Loss (PR #72352, #72353)** — Two P0 fixes for prompt-cache breakpoints being dropped during ordered-replay and provider failover. Both landed.
- **Terminal RCE via Environment Injection (PR #72355)** — A newline in a Matrix display name could inject shell commands into terminal environment snapshots. P1 fix landed.

**P1 (High):**
- **Gateway Startup Mute (PR #72357)** — A single slow boot-resume turn could mute all channels indefinitely. Fix landed.
- **macOS uv Launcher Breakage (PR #72360)** — Stock macOS <13 missing `realpath` broke `hermes update`. Fix landed.
- **Compaction Summary Erasure (PR #72356)** — Turn compaction summaries erased from continuation history during gateway/ACP sessions. Fix landed.

**P2 (Medium):**
- **Telegram Model Picker Skips Keyless Providers (#33595)** — Closed today, fix merged.
- **Cron False Positives with Broken LINE Adapter (#51184)** — Still open, no assigned fix.
- **`hermes mcp add` Drops All But Last `--env` Flag (#37501)** — Still open.

**Docker/SQLite WAL-Reset Cluster:**
- Issues #70480 and #71851 both reported Docker images shipping SQLite 3.46.1 (vulnerable to WAL-reset corruption). Both closed, but #72093 notes that `hermes update` still prints a dead-end warning for users with managed runtimes. Fix PR #72363 partially addresses the provider dep healing but does not resolve the fundamental Docker image SQLite version.

## Feature Requests & Roadmap Signals

- **Buzz Messaging Integration (#68871, 13 👍)** — The strong reaction suggests this could be prioritized for a near-term release, especially as Block's Buzz fills a gap in self-hostable agent-human workspaces.
- **Shared Memory Pools for Sub-Agents (#377)** — Inspired by CAMEL-AI, this long-running request (created March 2026) asks for state sharing between delegated sub-agents. Still open with no maintainer response.
- **GUI-Only Desktop Installation (#50643, 3 👍)** — Users want to install only the Desktop GUI frontend connecting to a remote backend, without the full CLI/agent stack. No maintainer assignment.
- **Markitdown as Local Web Fetch Provider (#65179)** — A self-hosted, API-free alternative to hosted web_extract services. Still triaging.
- **Ctrl+F / Cmd+F in Desktop (#46169)** — Closed and merged; basic find UI now available.

Prediction: Buzz integration (#68871) and Shared Memory Pools (#377) are likely targets for the next minor release (v0.20.0), given community enthusiasm and alignment with the multi-agent orchestration roadmap.

## User Feedback Summary

**Pain Points:**
- **Database corruption anxiety:** Multiple users expressed frustration that the Docker image ships SQLite 3.46.1, which `hermes doctor` itself flags as WAL-reset vulnerable, with no straightforward workaround (#70480, #71851, #72093). The warning on every `hermes update` is a "dead-end" experience for users on managed runtimes.
- **Telegram media upload limits:** `#62936` documents a hard floor of ~15 MB without workaround, despite documented configuration options.
- **Configuration fragility:** Several users reported agent-led self-configuration corrupting credentials (#42727), and env sanitizer not removing `KEY=***` placeholders (#12651). These erode trust in autonomous configuration.
- **Cross-profile misdelivery:** Multiple reports (#56802, #70179) of kanban notifications delivered by the wrong Telegram bot when profiles share a board — fixed, but surfaced a systemic design issue in multi-gateway routing.

**Satisfaction Signals:**
- The `/diff` command was the most-requested workflow feature, finally landing after three prior attempts. Community reception appears positive.
- Desktop artifacts feature (#72345) directly addresses a long-standing feature gap vs. Anthropic's Claude Code and OpenAI's Codex.
- The CVE pin update (#72362) was a direct response to user-reported downgrade behavior, well-received.

## Backlog Watch

| Issue | Created | Last Updated | Status | Notes |
|-------|---------|--------------|--------|-------|
| **#377** Shared Memory Pools for Sub-Agents | 2026-03-04 | 2026-07-26 | OPEN | No maintainer response in 4+ months |
| **#3506** Durable Feedback Routing | 2026-03-28 | 2026-07-27 | OPEN | Comprehensive proposal from @kshitijk4poor, no assignment |
| **#12651** `.env` Sanitizer Fails to Remove Placeholders | 2026-04-19 | 2026-07-27 | OPEN | P2 bug, affects credential hygiene, no fix PR |
| **#51184** Cron False Positives with Broken LINE Adapter | 2026-06-23 | 2026-07-27 | OPEN | P2, impacts reliability for LINE users |
| **#9812** ACP Sessions Drop Provider Snapshot | 2026-04-14 | 2026-07-27 | OPEN | P2 session metadata loss, no PR |
| **#42727** Agent-Led Config Corruption | 2026-06-09 | 2026-07-27 | OPEN | P2 security-adjacent, high-impact if triggered |
| **#72298** Passwords Shown in Telegram Chat | 2026-07-26 | 2026-07-26 | OPEN (needs-repro) | High reaction count (7 👍), second-most-reacted open issue |

The oldest important item (#377, Shared Memory Pools) has been awaiting maintainer attention for nearly 5 months. While the volume of incoming work is high, this gap in multi-agent orchestration capability is becoming a competitive disadvantage vs. emerging frameworks.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-27

## 1. Today's Overview
PicoClaw shows moderate activity today, with 4 issues and 7 pull requests updated in the last 24 hours—most of which are still open. One issue was closed (a stale bug fix) and one PR was merged. There are no new releases today. The project is actively processing community contributions, including security hardening, a new web search provider integration, and critical bug fixes for message splitting hangs. A notable feature request for adding AI Router as a native provider was also filed today.

## 2. Releases
**No new releases today.** The latest release remains the previous version.

## 3. Project Progress
- **Merged/Closed PRs:** 1 PR was closed today — **PR #3248** ([sipeed/picoclaw PR #3248](https://github.com/sipeed/picoclaw/pull/3248)) "fix: bump Go to 1.25.12 to remediate stdlib vulnerabilities" — a stale bug fix that updates the Go toolchain to patch two standard library vulnerabilities (`GO-2026-5856` in `crypto/tls` and `GO-2026-4970` in `os`). This improves supply chain security.

- **Open PRs with recent updates:** 6 open PRs saw activity, including a new feature adding native Exa web search provider support ([PR #3299](https://github.com/sipeed/picoclaw/pull/3299)), a fix for SplitMessage hangs ([PR #3295](https://github.com/sipeed/picoclaw/pull/3295)), and security boundary hardening for remote prompts ([PR #3297](https://github.com/sipeed/picoclaw/pull/3297)).

## 4. Community Hot Topics
- **Most active issue:** **Issue #3265** ([sipeed/picoclaw Issue #3265](https://github.com/sipeed/picoclaw/issues/3265)) — Gateway startup fails with 'channel deltachat has unknown type deltachat' — users report the gateway fails to start even when deltachat is not configured. This has 1 comment and signals confusion around channel type validation during startup, potentially exposing a config parsing edge case.

- **Most commented issue:** **Issue #3252** ([sipeed/picoclaw Issue #3252](https://github.com/sipeed/picoclaw/issues/3252)) — `splitKnownProviderModel` strips provider prefix incorrectly when model ID contains a known provider alias. This bug was **closed** today after 2 comments, suggesting the fix was implemented and verified.

- **New feature request:** **Issue #3298** ([sipeed/picoclaw Issue #3298](https://github.com/sipeed/picoclaw/issues/3298)) — "Add AI Router as an OpenAI-compatible provider preset" — filed today by the AI Router maintainer. This reflects community desire for simplified multi-provider routing without manual `api_base` configuration.

## 5. Bugs & Stability
- **High severity:** **Issue #3264** ([sipeed/picoclaw Issue #3264](https://github.com/sipeed/picoclaw/issues/3264)) — `SplitMessage` hangs on an oversized fenced-code info string. This is a **potential denial-of-service** bug where the message splitter can loop forever. A fix PR (#3295) was submitted today by ErzerLP, implementing a bounded raw split fallback. **Fix availability: PR #3295 is open.**

- **Medium severity:** **Issue #3265** ([sipeed/picoclaw Issue #3265](https://github.com/sipeed/picoclaw/issues/3265)) — Gateway startup fails with unknown channel type error even when the channel is not configured. This could cause unexpected crashes on clean configurations. **No fix PR identified yet.**

- **Closed (fixed):** **Issue #3252** ([sipeed/picoclaw Issue #3252](https://github.com/sipeed/picoclaw/issues/3252)) — Provider prefix stripping bug in `splitKnownProviderModel`. **Closed today.**

## 6. Feature Requests & Roadmap Signals
- **#3298** ([sipeed/picoclaw Issue #3298](https://github.com/sipeed/picoclaw/issues/3298)) — "Add AI Router as an OpenAI-compatible provider preset" — Likely to be implemented in the next minor release given it's a small configuration addition (adding a preset) and comes from the provider maintainer.
- **#3299** ([sipeed/picoclaw PR #3299](https://github.com/sipeed/picoclaw/pull/3299)) — "Add native Exa web search provider" — This PR is already open and appears feature-complete. It adds `type: "auto"` search with date range filters. High probability of merging soon.
- **#3296** ([sipeed/picoclaw PR #3296](https://github.com/sipeed/picoclaw/pull/3296)) — "i18n: complete Czech code wrap labels" — A smaller localization improvement, likely to be accepted in the next patch release.

## 7. User Feedback Summary
- **Pain point (fix incoming):** Message splitting hangs when code fences have oversized info strings (Issue #3264). User `floze-the-genius` reported the exact reproduction case, and a fix is already in review.
- **Confusion:** Gateway startup failure with unknown channel type (Issue #3265) — user `Cipher208` expects the system to gracefully ignore unconfigured channels; the current strict validation surprises users.
- **Request for convenience:** Users want one-click integration with AI Router (Issue #3298), indicating a desire for simpler multi-provider setup without manual config tweaks.
- **Satisfaction (closed):** The provider prefix parsing bug (Issue #3252) was resolved, which should improve reliability for users with complex model IDs.

## 8. Backlog Watch
- **PR #3202** ([sipeed/picoclaw PR #3202](https://github.com/sipeed/picoclaw/pull/3202)) — "fix(routing): strip leading/trailing underscores in ID normalization" — Opened July 1, last updated July 26. This fix addresses a documented but unimplemented normalization rule. Stale for 25 days; may need maintainer review or nudging.
- **PR #3267** ([sipeed/picoclaw PR #3267](https://github.com/sipeed/picoclaw/pull/3267)) — "fix scope bug for refresh agy token" — Opened July 19, last updated July 26. Fixes an authentication scope bug for the Antigravity provider. No comments from maintainers yet; risk of going stale if not addressed soon.
- **Issue #3265** ([sipeed/picoclaw Issue #3265](https://github.com/sipeed/picoclaw/issues/3265)) — Gateway startup failure — no assignee, no PR linked. Could become a stale blocker if left unresolved.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-27

## Today's Overview

NanoClaw saw **moderate activity** over the past 24 hours, with 2 new issues filed and 9 pull requests receiving updates. The project shows a healthy **fix-heavy pulse**, with several core-team and community contributors addressing critical messaging reliability bugs. Two significant PRs were merged/closed, including a long-standing duplicate-reply fix and a per-agent-group timezone feature. No new releases were cut today, and two open issues with zero comments point to potentially underreported regressions following a recent breaking change. Overall, the project is in an **active stabilization phase** following the "explicit-destinations" migration.

## Releases

No new releases this period.

## Project Progress

**Merged/Closed PRs (2 items):**

- **`#3028`** — *fix: avoid duplicate replies after send_message* (merged, by ogarciarevett). This fix prevents the agent from emitting a second reply when `send_message` has already written a chat response to the triggering channel. A long-standing annoyance for users experiencing double-replies should now be resolved. [PR Link](https://github.com/nanocoai/nanoclaw/pull/3028)

- **`#3125`** — *feat: per-agent-group timezone override* (merged, by Koshkoshinsk, core-team). Adds an optional IANA timezone override per agent group via `ncl groups config update --timezone <IANA>`, with migration 020. Resolution logic chains: group override → install global. A new `resolveGroupTimezone` helper grounds the group's scheduling context. [PR Link](https://github.com/nanocoai/nanoclaw/pull/3125)

**Notable Open Progress:**
- **`#3126`** (core-team, glifocat) — *never deliver silence, never deliver `<internal>` thinking* — continues to advance with updates, targeting both agent-runner container delivery filtering. [PR Link](https://github.com/nanocoai/nanoclaw/pull/3126)

## Community Hot Topics

The most active areas of discussion revolve around **post-migration messaging reliability** and **channel integration expansion**:

- **`#3136`** — *`sendToDestination` stamps a foreign `in_reply_to` on outbound rows* (by JoshuaJFogg). Raises a subtle but critical bug in `poll-loop.ts`: the fallback `in_reply_to` logic can misroute messages when a destination has no inbound history, potentially breaking A2A return-path routing for new conversations. No comments yet, but the issue touches a core routing mechanism. [Issue Link](https://github.com/nanocoai/nanoclaw/issues/3136)

- **`#3050`** — *feat(setup): add Dial to the channel picker + wizard/skills* (by OmriBenShoham). A long-running feature PR (since July 14) that adds Dial as a new channel integration. Still open after 12 days with multiple updates, indicating active review or rework. The demand for new channel integrations remains high. [PR Link](https://github.com/nanocoai/nanoclaw/pull/3050)

- **`#3137`** — *Fix engagement consistency and expose self-serve wiring controls* (core-team, Koshkoshinsk). A significant PR touching warm-container follow-up suppression, agent wiring inspection, and engagement-policy updates. Its scope suggests the team is investing in **self-service operational controls**. [PR Link](https://github.com/nanocoai/nanoclaw/pull/3137)

## Bugs & Stability

**High Severity:**
- **`#3140`** — *Explicit-destinations migration: pre-existing wirings have no own-chat destination — all replies silently dropped* (by grtwrn). A **critical regression** affecting all users who updated across the explicit-destinations breaking change. Agent replies in long-standing chat groups are silently dropped with `Unknown destination` errors. No fix PR yet. Users should **not upgrade** without migration instructions. [Issue Link](https://github.com/nanocoai/nanoclaw/issues/3140)

**Medium-High Severity:**
- **`#3136`** — *`sendToDestination` stamps a foreign `in_reply_to` on outbound rows* (by JoshuaJFogg). Subverts A2A routing for destinations without inbound history. A fix PR is **not yet linked**, but this is likely triggered by the same explicit-destinations code path. [Issue Link](https://github.com/nanocoai/nanoclaw/issues/3136)

**Medium Severity:**
- **`#3135`** (PR) — *fix: mirror host-sent messages into the agent's context* (by brianjcohen). Fixes issue #3134 where approval cards, reject-reason prompts, and registration notices sent on the agent's behalf are invisible to the agent. This is a **user-visible transparency gap** — agents are unaware of their own outbound communications. Fix PR is open. [PR Link](https://github.com/nanocoai/nanoclaw/pull/3135)

**Lower Severity (fixes in progress):**
- **`#3126`** (PR, core-team) — Prevents delivery of silent messages and `<internal>` thinking blocks, cleaning up user-facing noise.
- **`#3139`** (PR, grtwrn) — *shared-number mode silences the owner* — stops blanket drop of `fromMe` messages in WhatsApp shared-number mode.

## Feature Requests & Roadmap Signals

- **Self-serve wiring controls** (`#3137`): Agents may soon inspect their own wirings and request approved engagement-policy updates without admin intervention. Signals an operational maturity push.
- **Dial channel integration** (`#3050`): Continued community interest in expanding channel support. Likely to land in next minor release.
- **Per-agent-group timezone** (`#3125`): Already merged — expected in next release.
- **Custom-endpoint transport + memory parity for Opencode** (`#3122`, core-team): Integration improvements for the Opencode protocol, suggesting expanded compatibility efforts.

**Prediction for next version (v0.x):** Focus will be on (1) fixing the explicit-destinations regression, (2) landing Dial channel support, and (3) shipping the agent-wiring introspection features.

## User Feedback Summary

**Pain Points (high frustration):**
- "All replies silently dropped after update" (`#3140`) — the **most impactful user-facing regression** currently open. Users who followed the breaking-change migration guide are left with non-functional agent groups. No workaround documented.
- Agents unaware of their own approval/rejection messages (`#3134` / `#3135 fix`) — users find it confusing that agents cannot see what they themselves sent. This erodes trust in multi-turn conversational workflows.
- WhatsApp shared-number mode owner silence (`#3139`) — owners being unable to receive their own messages is a **daily workflow blocker** for WhatsApp deployments.

**Satisfaction Signals:**
- The per-agent-group timezone feature (`#3125`) addresses a common request from users with geographically distributed agent groups.
- The duplicate-reply fix (`#3028`) closes a long-standing irritation, suggesting the team is responsive to quality-of-life bugs.

## Backlog Watch

- **`#3050`** (Dial channel PR, opened Jul 14, 13 days old) — While active, the 13-day review cycle may frustrate the contributor. Needs maintainer prioritization or explicit blockers communicated.
- **`#3140`** and **`#3136`** — Both **zero-comment issues** filed yesterday. The absence of maintainer acknowledgment or triage labels is concerning given their severity. Urgent attention required.
- **`#3122`** (Opencode compatibility PR, opened Jul 23, 4 days old) — Core-team authored, but no merge activity yet. If this blocks other Opencode-related changes, it may stall the integration roadmap.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-07-27**.

---

### 1. Today's Overview
The NullClaw project is currently in a **low-activity maintenance phase** with no new releases or merged pull requests in the last 24 hours. The primary signal is a single, critical open issue regarding a persistent crash bug in the Telegram gateway. While the project has no incoming feature work or merged changes today, the community is actively discussing a severe stability regression that prevents the Telegram integration from functioning. The project’s health appears stable in terms of code churn, but the unresolved nature of the SIGSEGV bug represents a high-risk point for users relying on the Telegram agent.

### 2. Releases
**None.** No new releases were published in the last 24 hours. The latest release remains **v2026.5.29**.

### 3. Project Progress
**No pull requests were merged or closed today.** There is no evidence of new features, bug fixes, or documentation improvements being integrated into the codebase in the last 24 hours.

### 4. Community Hot Topics
**Most Active Issue:**
- **[#976 [OPEN] SIGSEGV on every inbound Telegram message](https://github.com/nullclaw/nullclaw/issues/976)** (3 comments, 0 reactions)
  - *Description:* On aarch64 Linux, every inbound Telegram message causes a segfault due to an inbound worker thread spawned with a ~512 KB stack overflow. The process crash-loops as a `systemd` service, dropping all messages.
  - *Analysis:* This is the only active discussion thread in the repository. The user is experiencing a complete denial of service for the Telegram gateway. The core need is **reliability** and **platform compatibility** (aarch64). The issue appears to be a threading/memory configuration problem rather than a logic bug.

### 5. Bugs & Stability
- **Severity: Critical** – **Issue #976** – SIGSEGV on inbound Telegram messages.
  - **Impact:** Complete crash on every incoming message for aarch64 Linux users. The service is effectively non-functional.
  - **Context:** The user reports the issue occurs specifically on `v2026.5.29`. The root cause is identified as a stack overflow in an inbound worker thread (512 KB stack limit).
  - **Fix Status:** No associated pull request exists yet. No maintainer has confirmed a fix or workaround.

### 6. Feature Requests & Roadmap Signals
There are **no explicit feature requests** in the current data set. The community is entirely focused on a critical stability issue. The next version (if any) is likely to focus exclusively on:
- **Bug fix:** Resolving the SIGSEGV for aarch64 and potentially other architectures with small default thread stacks.
- **Configuration change:** Allowing user-configurable thread stack sizes to avoid similar overflows.

### 7. User Feedback Summary
- **Pain Point (Critical):** The Telegram gateway is completely broken on aarch64 Linux. The user is unable to receive any replies.
- **Use Case:** The user is running NullClaw as a `systemd` service (production-like environment).
- **Satisfaction:** The user is clearly frustrated by the crash-loop behavior, as every message kills the process and is permanently dropped. The lack of a recovery mechanism (e.g., message queue persistence) is a secondary pain point.

### 8. Backlog Watch
- **Issue #976** – This is the only open issue currently requiring immediate maintainer attention.
  - **Status:** No maintainer response has been recorded since the issue was created (2026-07-16). The issue is 11 days old with no triage or fix.
  - **Risk:** If a maintainer does not address this soon, aarch64 Telegram users will abandon the project. Given the severity, this issue should be escalated to a hotfix priority.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-27

---

## Today's Overview

IronClaw is in a period of intense engineering activity, with **17 pull requests updated in the last 24 hours** (6 merged/closed, 11 open) and **4 active issues** attracting focused discussion. The project's pulse is elevated, driven primarily by two major initiatives: a **unified error-recoverability framework** (epic #6284) and a **per-user hosted-MCP discovery feature** (P2b). Core contributors are closing out large refactors and structural ratcheting, while dependency updates across Rust crates, Wasm tooling, and GitHub Actions continue steadily. No new releases were cut today, but the volume of merged PRs suggests a release may be imminent. Overall project health is strong, with disciplined attention to breaking changes, regression testing, and dead-code elimination.

---

## Releases

**No new releases today.** The most recent release candidate remains PR #5598 (still open), which would cut `ironclaw_common` 0.5.0 and `ironclaw_skills` 0.4.0 with **API breaking changes** — see Backlog Watch below.

---

## Project Progress

### Merged/Closed PRs (6 total)

| PR | Title | Contributor | Significance |
|----|-------|-------------|--------------|
| [#6679](https://github.com/nearai/ironclaw/pull/6679) | Harden struct ratchet and remove dead Gemini API | ilblackdragon (core) | **High.** Addresses review findings from PR #6673; replaces line-oriented scanner with `syn` parsing for multi-line `cfg_attr` and `impl` headers; removes dead Gemini API code. Adds regression test coverage. |
| [#6677](https://github.com/nearai/ironclaw/pull/6677) | Compile-forced recoverability conformance matrix (§11.7 / #6284 item 7) | serrrfirat (core) | **High.** Adds `RecoverabilityClass` enum and exhaustive classifier for seven error enums — foundational work for the error-recoverability epic #6284. Superseded by #6684's more comprehensive collapse. |
| [#6365](https://github.com/nearai/ironclaw/pull/6365) | [reference] P2b: per-user hosted-MCP discovery (worker agents get per-hire connector tools) | kirikov (new) | **High.** Reference PR for porting the P2b feature from a fork branch. Replaced by cleaner rebase PR #6683. |
| [#6640](https://github.com/nearai/ironclaw/pull/6640) | build(deps): bump everything-else group with 31 updates | dependabot[bot] | **Routine.** Bulk dependency bump. |
| [#4032](https://github.com/nearai/ironclaw/pull/4032) | chore(deps): bump the wasm group with 2 updates (closed after 2 months open) | dependabot[bot] | **Routine.** Wasm dependency update finally closed. |
| [#5369](https://github.com/nearai/ironclaw/pull/5369) | fix(reborn): suppress Cranelift debug log floods | ogarciarevett (new) | **Low.** Logging fix — extends noise guard to Wasmtime/Cranelift compiler targets. |

### Key Feature Advances

1. **Error-Recoverability Consolidation (Epic #6284):** PR [#6684](https://github.com/nearai/ironclaw/pull/6684) (still open) collapses **five overlapping failure-kind enums** into a single 35-variant `FailureKind` with projection functions, and fixes **four wrongful-terminal bugs** exposed by the collapse, each with a red-verified regression test. This is the most significant single refactor of the week.

2. **Per-User MCP Discovery (P2b):** PR [#6683](https://github.com/nearai/ironclaw/pull/6683) (open) reimplements the feature cleanly on top of the post-#6116 main branch, with the capability path moved to a scope-free `ToolResolver` and `extension_host` extracted.

3. **Attested Signing Phase B:** PR [#6672](https://github.com/nearai/ironclaw/pull/6672) (open) introduces the *signed intent* — cryptographic attestation that an agent crafted exactly a transaction for exactly an approver — plus per-agent key lifecycle. Based on the Ledger revival design spec.

4. **Mutation Testing Infrastructure:** PR [#6681](https://github.com/nearai/ironclaw/pull/6681) (open) runs escape-history mutation targets but discovers the harness had a bug preventing output — the dispatcher thread was not polled. Fix in progress.

---

## Community Hot Topics

### Most Active Issue
**[#6284 — [EPIC] Error-recoverability endgame](https://github.com/nearai/ironclaw/issues/6284)** (8 comments, updated yesterday)
- *Author:* serrrfirat | *Created:* 2026-07-19
- *Underlying need:* A formal, verifiable contract that every mid-run error is survivable, visible to the model, actionable, and never reported as non-success to the user. This addresses a core reliability gap where agents silently fail or terminate without the model having a recovery opportunity.
- *Impact:* Foundational architecture issue — multiple PRs (#6677, #6684, #6681) are stacked on this epic. The five-error-enum collapse in #6684 fixed four actual bugs exposed by the conformance matrix.

### Most Updated PRs
**[#6687 — build(deps): bump everything-else group with 33 updates](https://github.com/nearai/ironclaw/pull/6687)** (dependabot, XL size)
- *Activity driver:* Bulk dependency maintenance — 31 package updates, low-risk but large file change footprint. Updated yesterday.

**[#6683 — P2b: per-user hosted-MCP discovery](https://github.com/nearai/ironclaw/pull/6683)** (kirikov, new contributor, XL size)
- *Activity driver:* A feature PR from a newer contributor, explicitly superseding a reference PR (#6365) after maintainer review feedback. Indicates active onboarding and collaborative refactoring.

**[#6684 — Refactor: one failure vocabulary](https://github.com/nearai/ironclaw/pull/6684)** (serrrfirat, core contributor, XL size)
- *Activity driver:* The real deliverable for the recoverability epic — collapses entire failure-kind system, +41 deletions, fixes 4 bugs. Stacked on #6677 (merged). This is the substantive engineering output of #6284.

### Analysis
The recoverability epic (#6284) is the project's primary structural concern — multiple PRs, core contributor focus, and the presence of a dedicated architecture doc (`docs/reborn/2026-07-17-architecture-...`) indicate a deliberate, methodical push to harden the agent runtime. The P2b MCP feature reflects ongoing investment in multi-agent/connector ecosystems.

---

## Bugs & Stability

### High Severity
1. **Four wrongful-terminal bugs found and fixed** via PR [#6684](https://github.com/nearai/ironclaw/pull/6684) — these were cases where the model's failure-kind vocabulary incorrectly categorized recoverable errors as terminal, causing runs to abort when they should have survived. Each has a red-verified regression test. **Fix merges pending.**

### Medium Severity
2. **Systemd unit file misconfiguration** — PR [#6652](https://github.com/nearai/ironclaw/pull/6652) (open) fixes a `Loaded: bad-setting` error after `ironclaw onboard` on Linux (issue #6575). `WorkingDirectory=` was incorrectly quoted as if it were an `ExecStart=` directive. **Fix PR exists, not yet merged.**

### Low Severity
3. **Cranelift debug log floods** — PR [#5369](https://github.com/nearai/ironclaw/pull/5369) (merged) suppresses noisy debug output from Wasmtime/Cranelift compiler targets when `IRONCLAW_REBORN_LOG=debug` is set. Already fixed.
4. **Mutation test harness bug** — Discovered in PR [#6681](https://github.com/nearai/ironclaw/pull/6681): the audit harness never produced its output because the dispatcher thread was not polled. **Fix PR exists, not yet merged.**
5. **DockerProcessSandboxBackend dead code** — Issue [#6686](https://github.com/nearai/ironclaw/issues/6686) identifies an entire `DockerProcessSandboxBackend` as dead (no production constructor, no test coverage, no call sites). Low risk but should be removed for hygiene.

### Stability Indicators
- The daily failure taxonomy ([#6682](https://github.com/nearai/ironclaw/issues/6682)) shows clawbench runs dominated by "genuine model-quality partial completions" — the agent produces valid, self-verifiable output but the evaluation considers it incomplete. This is a **benchmarking/measurement concern** rather than a runtime stability bug.
- No crashes or panics reported in the last 24 hours.
- The error-recoverability refactor is explicitly designed to make 100% of errors recoverable — this is the project's headline stability investment.

---

## Feature Requests & Roadmap Signals

### Explicitly in Progress
1. **Error-recoverability endgame (#6284)** — Nearing completion: the failure-kind enum collapse (#6684) will fully satisfy the recoverability contract. Expect it to land in the next major release.
2. **Per-user hosted-MCP discovery (P2b)** — PR #6683 refactors cleanly onto main. Likely to land soon; enables agent connectors per user/hire.
3. **Attested signing Phase B (#6672)** — Signed intents + per-agent key lifecycle. A feature milestone for the Ledger revival plan. Probably targets the release after next.

### Inferred from Merged/Active Work
4. **Struct ratchet hardening (#6679)** — Multi-line `cfg_attr` and `impl` header parsing suggests production-grade tooling for enforcing struct versioning contracts. Could become part of CI.
5. **Mutation testing pipeline** — PRs #6674, #6681 indicate investment in mutation/escape analysis for quality assurance. Early-stage but signals a growing testing culture.

### Predictions for Next Release
- The error-recoverability collapse (#6684) + recoverability conformance matrix (#6677) will land together — this is the headline feature.
- P2b MCP discovery (#6683) may also ship, depending on review velocity.
- Release PR #5598 (still open) will likely be merged to cut `ironclaw_common` 0.5.0 and `ironclaw_skills` 0.4.0 with breaking changes.
- DockerProcessSandboxBackend removal (#6686) will likely be a cleanup item in the same release.

---

## User Feedback Summary

### Pain Points (explicit or inferred)
- **Agent partial completions incorrectly scored as failures** — The daily failure taxonomy (#6682) shows the agent produces valid, self-verifiable output that the benchmark suite considers incomplete. This suggests a **gap in how the evaluation system handles partially correct multi-step reasoning**, not an agent quality problem per se. Users may see misleading failure rates.
- **Systemd unit file breaks after onboarding** — PR #6652 fixes a `Loaded: bad-setting` error. New Linux users running `ironclaw onboard` encounter a broken service — poor onboarding experience.
- **Debug log floods obscure useful output** — The Cranelift noise suppression fix (#5369) indicates that enabling debug logging produces overwhelming noise from Wasmtime internals. Intermediate users doing debugging face a high signal-to-noise problem.

### Satisfaction Indicators
- The project's disciplined approach to error-recoverability and structural hardening suggests a **maintainer team that values correctness and user trust**.
- New contributors (kirikov, ogarciarevett) are being onboarded with reference PRs and clean rebasing — the project has an effective mentorship pipeline.
- Daily failure taxonomy updates (#6682) demonstrate **operational transparency** — users can see exactly what the team is measuring and where the gaps lie.

---

## Backlog Watch

### High Priority (Needs Maintainer Attention)

1. **[PR #5598 — chore: release (open 24 days)](https://github.com/nearai/ironclaw/pull/5598)**
   - *Scope:* Release cutting `ironclaw_common` 0.5.0 and `ironclaw_skills` 0.4.0 with API breaking changes.
   - *Status:* Open since July 3, updated July 26. Breaking changes need review. This is blocking downstream consumers from accessing the new `Copy` impl on `EnvVar` and the `Display` impl on `SdkAgentData`.
   - *Why it matters:* Extended freeze on breaking-change release creates friction for ecosystem projects. The longer this sits, the more divergence accumulates.

2. **[PR #5664 — build(deps): bump the actions group with 16 updates (open 22 days)](https://github.com/nearai/ironclaw/pull/5664)**
   - *Scope:* CI/CD dependency updates including `actions/checkout` v4→v7, `claude-code-action` major version bumps, and 14 other Actions.
   - *Status:* Open since July 5. Updated July 26 but no maintainer review.
   - *Why it matters:* CI dependency rot can silently break automated workflows. The `actions/checkout` v4→v7 jump spans three major versions.

### Medium Priority

3. **[PR #6672 — feat(signing): signed intent + per-agent key lifecycle (open 2 days)](https://github.com/nearai/ironclaw/pull/6672)**
   - *Scope:* Major feature — Phase B of Ledger revival plan.
   - *Status:* Open since July 25, no comments. May still be under internal review. No immediate concern but should watch for stagnation.

4. **[PR #6681 — test(mutation): run escape-history targets (open 1 day)](https://github.com/nearai/ironclaw/pull/6681)**
   - *Scope:* Runs mutation audit targets, but the harness has a bug.
   - *Status:* Fresh PR; needs review of the harness fix itself. Low risk of neglect.

### Items Closed/Resolved This Period
- **PR #6679** (struct ratchet hardening) — merged. One less item in the backlog.
- **PR #6677** (recoverability conformance matrix) — merged, superseded by #6684.
- **PR #4032** (wasm deps) — closed after 62 days open. Example of dependabot PRs lingering.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-07-27**.

---

## LobsterAI Project Digest — 2026-07-27

### 1. Today's Overview
Activity on the LobsterAI repository remains **low**, with only 2 issues and 8 pull requests (PRs) updated in the last 24 hours. **No new releases** were published, indicating the project is in a maintenance or stabilization phase. The majority of activity involves **stale PRs** (7 out of 8 are still open and have not been touched since April 2026), suggesting a significant backlog in code review and merge processes. One critical bug regarding gateway instability (Issue #1243) remains open with no fix PR attached, signaling a potential stability risk for users on the 2026.4.1 build. Overall, the project appears to be **under-maintained** with a growing accumulation of unaddressed code and community feedback.

### 2. Releases
**None.** No new releases were created in the last 24 hours. The latest available version remains **2026.4.1** (released April 1, 2026).

### 3. Project Progress
Only **1 PR was closed/merged** today:
- **[PR #1325] feat(ui): Add hover tooltip for new conversation icon button** (Closed) — A small UI enhancement that adds a `title` attribute to the "New Conversation" icon button, improving discoverability when the sidebar is collapsed.

**No other PRs were merged.** The remaining 7 open PRs remain stalled, including significant features such as natural language scheduling (PR #1256) and gateway bundling optimizations (PR #1259), none of which have received maintainer feedback since April.

### 4. Community Hot Topics
The most active items (by comment count or reactions) reveal a focus on **Linux support** and **gateway stability**:

- **[Issue #273] [CLOSED] Request for Ubuntu Linux support** — Comment count: 2. User `billyoungs` requested Linux support 4 months ago. While now closed, the lack of any official roadmap for a Linux build is a clear gap.
- **[Issue #1243] [OPEN] Bug: qwen-portal-auth plugin causes frequent gateway restarts** — Comment count: 1. This is the most severe open bug (see Bugs & Stability section). Users are likely experiencing service disruption every 5-20 minutes.
- **[PR #1325] feat(ui): Add hover tooltip** — Closed today, this was a simple but welcomed fix for a common UX friction point.

**Underlying need:** Users are explicitly asking for **cross-platform support** (Linux) and **reliable core infrastructure** (gateway stability). The lack of progress on these fronts may be driving silent churn.

### 5. Bugs & Stability
**Severity: High**

- **Issue #1243: qwen-portal-auth plugin causes frequent gateway restarts** — **OPEN, no fix PR exists.**
    - **Impact:** Users report the gateway auto-restarts every 5-20 minutes, while a "AI engine is starting the gateway..." popup appears. This severely impacts all usage.
    - **Root Cause:** The `qwen-portal-auth` plugin configuration is being written in a loop, triggering an OpenClaw restart on every change.
    - **Urgency:** Critical. This bug affects all users on the 2026.4.1 release, regardless of which model they have configured. No maintainer response has been posted since the issue was opened on April 1, 2026.

**Severity: Medium**

- **PR #1247: Fix OpenClaw model switch recovery after provider limits** — A fix PR exists but is **stale** (no update since April). This addresses logic around model switching, which could lead to configuration mismatches.

**Severity: Low**

- **No new bugs reported in the last 24 hours.** The existing bug queue is old but unresolved.

### 6. Feature Requests & Roadmap Signals
**User-Requested Features (from open PRs/issues):**

1.  **Ubuntu/Linux Support (Issue #273)** — Request from March 2026. No official response from maintainers on plans. Likely not in next version.
2.  **Natural Language Scheduling (PR #1256)** — A user/contributor has built a complete feature for converting natural language descriptions into cron expressions. This is a high-value UX improvement. **Prediction:** Likely to be merged in the next release if maintainers review.
3.  **Unsaved Changes Confirmation (PR #1252 & PR #1258)** — Two PRs (by different authors) address the same problem: preventing data loss when cancelling task forms. **Prediction:** One of these PRs will likely be merged, as it is a common UX pain point.
4.  **Missing i18n keys (PR #1257)** — Simple localization fix for "edit" and "delete" buttons. Quick win.

**Roadmap Signal:** There is no official roadmap communication. The project appears to be relying on community contributions for feature development, with core maintainers not actively steering the feature direction.

### 7. User Feedback Summary
- **Satisfaction:** Low. The gateway restart bug (Issue #1243) is the loudest pain point. Users expressing satisfaction via reactions are absent in recent activity.
- **Pain Points:**
    - **Unstable core:** The recurring gateway restart issue undermines trust in the product.
    - **Lack of Linux support:** A persistent request that excludes a major user segment.
    - **UI friction:** Minor UX issues (missing tooltips, lack of unsaved-changes protection) are being reported but take months to fix.
- **Use Cases:** The project is being used for multi-agent AI orchestration (Cowork sessions), scheduled tasks, and MCP tool integration. Bugs in the session store and diff rendering (PR #1249) suggest users are actively trying to build complex workflows.

### 8. Backlog Watch
The following items are **high risk** due to age and lack of maintainer attention:

- **[Issue #1243] Gateway restart bug** — Open since April 1, 2026 (117 days). **No maintainer response.** This is the single most important item to unblock user trust.
- **[PR #1247] Fix OpenClaw model switch recovery** — Open since April 1, 2026. **Stale.** Directly affects model switching reliability.
- **[PR #1256] Natural language scheduling** — Open since April 1, 2026. **Stale.** A complete feature with potential high user impact; if not merged, it may be forked or abandoned.
- **[PR #1249] Fix DiffView rendering** — Open since April 1, 2026. **Stale.** A visual regression that prevents users from seeing code diffs in Cowork sessions—critical for developer users.
- **[PR #1259] Optimize gateway bundling** — Open since April 1, 2026. **Stale.** Addresses build failures for IM/channel SDKs, which may be blocking external contributions.

**Action Required:** Maintainers need to triage the stale PR queue (7 open) and provide a status update on the critical gateway bug (Issue #1243) to prevent further user attrition.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-07-27

## 1. Today's Overview
The Moltis project is in a period of **high feature velocity** with **zero new issues** and **no releases** in the last 24 hours, but **8 open pull requests** updated, all authored or co-authored by core maintainers. This signals a heavy **engineering push** rather than community churn — 6 of the 8 PRs are feature additions, 2 are critical fixes. The project is clearly preparing for a significant milestone release, likely featuring ACP agent-side support, a new memory backend (Zvec/Redb), and robust PWA/Slack/Nostr integrations. No community-reported bugs or support requests appeared today, indicating either a stable userbase or low public interaction.

## 2. Releases
**None** – no releases tagged in the last 24 hours.

## 3. Project Progress
**No PRs were merged or closed in the last 24 hours**, but the following high-impact open PRs are active and approaching merge-ready:

- **#1158** – New `zvec` vector database memory backend (vibe-coded, feature-gated) – a significant infrastructure addition to replace or supplement FAISS.
- **#1173** – PWA push notification reliability overhaul: fixes silent replacement of notifications (critical UX bug), adds `renotify`, and prevents duplicate notifications on session restore.
- **#1171** – Moves ACP client selection into the chat model picker, removing the old header selector – a major UX refactor for multi-provider workflows.
- **#1169** – Exposes Moltis itself as an ACP agent over stdio (bidirectional ACP support) – a **architectural milestone** enabling external harnesses (Zed, buzz-acp) to use Moltis as the agent.
- **#1166** – Slack integration enhancements: per-message reaction acknowledgments (replacing missing typing indicator), delivery failure handling, Block Kit support, and reconnect supervision.
- **#1168** – Adds NIP-29 group chat support for **Buzz** integration – Block's open-source Nostr relay for agent-human workspaces.
- **#1170** – **Critical security fix**: gates `sh` and privileged tools behind a per-account operators list, preventing arbitrary host command execution in group chats.

## 4. Community Hot Topics
With zero issues and no comments on today's PRs, there are **no community discussion threads** to highlight. The current activity is entirely **maintainer-driven**. The most significant PRs in terms of architectural impact are:

- **PR #1169** (ACP agent side) – Likely the most important technical shift, as it transforms Moltis from a pure ACP client into a full ACP endpoint.
- **PR #1158** (Zvec memory) – A novel experiment that could improve memory performance and reduce dependency on llama-cpp embeddings.

**Underlying needs**: These PRs collectively address **security hardening** (#1170), **reliability** (#1173, #1166), **interoperability** (#1169, #1168), and **performance** (#1158) – suggesting the team is preparing for larger-scale or multi-tenant deployments.

## 5. Bugs & Stability
**No new bugs were reported in issues today.** However, two PRs address existing stability/security defects:

| Severity | Bug | Fix PR | Status |
|----------|-----|--------|--------|
| 🔴 **Critical** | Arbitrary command execution: `/sh` was accessible to any group chat member without authorization | #1170 | Open, ready for review |
| 🟠 **High** | PWA push notifications silently replaced without sound/alert – chat messages lost | #1173 | Open, ready for review |
| 🟡 **Medium** | Slack bots lack typing indicator; acknowledgment reactions did not handle queueing/delivery failure correctly | #1166 | Open, ready for review |

No regressions were reported.

## 6. Feature Requests & Roadmap Signals
No feature requests were filed today. However, the open PRs strongly signal the following roadmap priorities:

- **Bidirectional ACP**: Moltis will soon function both as an ACP client and server, enabling integration with tools like Zed and Buzz.
- **Buzz/Nostr integration**: NIP-29 group chat support positions Moltis as a native agent for Nostr-based workspace tools.
- **Vector memory backend choice**: The Zvec/Redb experiment (#1158) may become an official alternative to FAISS, reducing deployment complexity.
- **PWA reliability as table stakes**: The team is investing in making the web app parity with native (reliable notifications, no silent failures).

**Prediction**: The next version (likely 0.7.x or similar) will include ACP agent mode, Slack Block Kit, Buzz group chat support, and the Zvec memory backend as an optional feature.

## 7. User Feedback Summary
There were **no user-submitted issues, comments, or reactions** in the last 24 hours. This likely reflects that Moltis is currently a **developer-tool-focused project** with a small, maintainer-heavy contributor base rather than a large consumer userbase. The absence of bug reports could indicate stability, but combined with zero issues, more likely indicates low community engagement or an early-stage product with few external users.

## 8. Backlog Watch
**No stale or unanswered important issues or PRs** exist in the last 24 hours. All 8 open PRs are recent (7–17 July) and actively maintained. However, it is worth noting:

- **PR #1158** (Zvec memory) was created on July 17 and has **no comments** – as an experimental feature, it may need reviewer attention or benchmarking data before merging.
- The project has **no open issues at all**, which is unusual. This may indicate that users are filing issues in another tracker (e.g., Discord) or that the project is in a pre-public-release phase.

**Recommendation**: Monitor #1158 for a call for performance comparisons against the existing memory backend before merging into a stable release.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-27

## Today's Overview
CoPaw (QwenPaw) on 2026-07-27 shows a moderate activity day with **11 issues** and **7 PRs** updated in the last 24 hours, but **zero new releases** and **no closed/merged items**. This signals a development cycle where the team is actively reviewing and discussing proposals rather than integrating changes. The majority of issues are bugs and questions, with one new feature request. The presence of three **first-time-contributor** PRs (#6481, #6479, #6477) indicates healthy community engagement, though the lack of any merged PRs today suggests maintainer bandwidth may be constrained. No releases were published today.

## Releases
**No new releases today.** The last known release remains v2.0.1 (Windows exe installer, referenced in multiple issues). Users continue to report bugs against this version.

## Project Progress
**Merged/closed PRs today: 0.** No PRs were merged or closed in the last 24 hours. This is a notable gap — the project has 7 open PRs accumulating, including two from first-time contributors (#6481, #6479), without any integrations happening today. The open PRs represent substantial feature work:

- **#6481** ([link](https://github.com/agentscope-ai/CoPaw/pull/6481)) — fix(crons): keepalive task for cron job misfires (addresses #6471)
- **#6387** ([link](https://github.com/agentscope-ai/CoPaw/pull/6387)) — feat(channels): on-demand installation and version repair
- **#6276** ([link](https://github.com/agentscope-ai/CoPaw/pull/6276)) — feat(browser): unified browser SDK with control/execution plane split
- **#6479** ([link](https://github.com/agentscope-ai/CoPaw/pull/6479)) — fix(providers): sync MiniMax model baseline
- **#6477** ([link](https://github.com/agentscope-ai/CoPaw/pull/6477)) — docs(faq): align zh/en sub-section headings
- **#6456** ([link](https://github.com/agentscope-ai/CoPaw/pull/6456)) — feat(context): Visual Compact (marked DO NOT MERGE)
- **#6284** ([link](https://github.com/agentscope-ai/CoPaw/pull/6284)) — feat(apps): qwenpaw-creator app plugin

## Community Hot Topics
The most active discussions by comment count reveal several pain points and user behaviors:

1. **#6470** ([link](https://github.com/agentscope-ai/CoPaw/issues/6470)) — **MCP driver ignoring transport config** (4 comments, 0 👍). The MCP driver hardcodes `sse_client` for transport, breaking servers configured for `streamable_http`. This is a core connectivity issue affecting multiple users' tool integrations. The reporter identified the root cause in `mcp_stateful_client.py` ~line 800.

2. **#6239** ([link](https://github.com/agentscope-ai/CoPaw/issues/6239)) — **Windows PATH concatenation drops semicolon** (3 comments, 0 👍). On Windows, when merging User and Machine PATH, the ';' separator is dropped between adjacent directories, causing child processes (npm, Node.js) to lose access to globally installed tools. This is a long-standing issue (opened July 18) and has substantial downstream impact for developers.

3. **#6473** ([link](https://github.com/agentscope-ai/CoPaw/issues/6473)) — **Plugin "Agent Kanban" fails to install** (2 comments, 0 👍). Users trying to install the official `agent-kanban@0.1.0` plugin from the App Center on Desktop 2.0.1 encounter `No module named 'qwenpaw.pawapp'`. This suggests a missing or renamed base module in the v2.0.1 release.

**Underlying needs**: Users are increasingly relying on MCP for tool integration (#6470), plugin ecosystem for workflow customization (#6473), and the system's ability to properly manage environment variables (#6239). The browser session high-CPU issue (#6460) and video delivery bug (#6474) indicate users are pushing the platform toward richer media and more complex agent interactions.

## Bugs & Stability
**Critical:**
- **#6470** — MCP driver hardcodes SSE transport, ignoring `streamable_http` config. Severity: **High** — breaks all MCP servers using Streamable HTTP. **No fix PR exists yet.**

**High:**
- **#6474** — `view_video` returns success but video DataBlock is silently dropped before reaching the LLM. Severity: **High** — makes video features completely non-functional despite appearing to work. **No fix PR exists.**
- **#6471** — Cron jobs misfire when event loop is idle (APScheduler AsyncIOScheduler not firing). Affects Linux/WSL2. Severity: **High** for automation-dependent users. **PR #6481** (first-time contributor) provides a fix with keepalive task.
- **#6476** — Matrix end-to-end encryption broken: `matrix-nio` + `vodozemac` fails due to missing `_cffi_backend`. Step-by-step manual fixes documented by user, suggesting an incomplete packaging dependency. **No fix PR.**

**Medium:**
- **#6473** — Plugin Agent Kanban fails with missing module `qwenpaw.pawapp`. Severity: **Medium** — affects specific plugin users on 2.0.1. **No fix PR.**
- **#6460** — High CPU in Edge+Wayland when viewing worklist with ComfyUI results. Severity: **Medium** — performance regression, specific to browser/display stack.
- **#6472** — JSON files not showing line numbers in Code mode after upgrading from 2.0.0 to 2.0.1. Severity: **Low** — UI regression, minor productivity impact.
- **#6239** — Windows PATH semicolon dropping (opened July 18). Severity: **Medium** — breaks npm/Node usage. **No fix PR.**

**Low:**
- **#6480** — `nohup`/`&` commands never return to idle (agent gets stuck). Severity: **Low** — behavioral issue with background processes.

## Feature Requests & Roadmap Signals
1. **#6475** ([link](https://github.com/agentscope-ai/CoPaw/issues/6475)) — `notice_after_complete` tool: Allow the agent to acknowledge long-running tasks, return to user for other questions, then push completion notification. This addresses a fundamental UX gap in async task handling and could be a high-value addition for v2.1.

2. **#6478** ([link](https://github.com/agentscope-ai/CoPaw/issues/6478)) — Traditional Chinese (繁體中文) localization. A user has already translated frontend and backend locally and is seeking permission to contribute. Evidence of international community engagement and desire for broader language support.

3. **PR #6387** ([link](https://github.com/agentscope-ai/CoPaw/pull/6387)) — On-demand installation and version repair for channels. This would improve plugin robustness and reduce dependency conflicts.

4. **PR #6276** ([link](https://github.com/agentscope-ai/CoPaw/pull/6276)) — Unified browser SDK with control/execution plane split. A major architectural improvement for browser automation.

5. **PR #6284** ([link](https://github.com/agentscope-ai/CoPaw/pull/6284)) — QwenPaw Creator app: script → assets → storyboard → video creation workflow plugin. Signals direction toward creative/media production use cases.

**Prediction for next version**: The `notice_after_complete` mechanism (#6475) and the browser unification (#6276) both address core UX and architectural gaps. The cron keepalive fix (#6481) is likely to land soon, and the MCP transport fix (#6470) is urgent.

## User Feedback Summary
**Satisfaction signals:**
- Users are actively exploring plugin ecosystem and MCP integration, suggesting growing trust in the platform's extensibility.
- Community contributors are appearing with PRs (three first-time contributors today).
- A user invested effort to translate the entire project to Traditional Chinese before even submitting (#6478).

**Pain points:**
- **v2.0.1 regression**: Multiple users report features working in 2.0.0 but broken in 2.0.1 (#6472 line numbers, possibly #6473 plugin installation).
- **Video handling broken**: The silent drop of video data (#6474) creates a support burden — users see "success" but get no results.
- **Windows environment management**: The PATH semicolon bug (#6239) echoes broader concerns about Windows as a first-class platform.
- **Plugin/dependency fragility**: Users encounter module-not-found errors (#6473) and incomplete library packaging (#6476), indicating QA gaps in the plugin/dependency pipeline.
- **MCP transport inflexibility**: Hardcoded transport choice shows the MCP integration is still maturing.

## Backlog Watch
**Unanswered issues needing maintainer attention (aged >1 day, no maintainer response):**
1. **#6239** ([link](https://github.com/agentscope-ai/CoPaw/issues/6239)) — Windows PATH semicolon bug. **Open for 9 days** (since July 18) with 3 user comments and no maintainer comment. A core Windows user experience bug affecting npm/Node.js workflows. Severity is Medium-High.

2. **#6460** ([link](https://github.com/agentscope-ai/CoPaw/issues/6460)) — Edge+Wayland high CPU bug. **Open for 2 days** (since July 25). No maintainer comment. Likely a rendering/WebSocket issue in the frontend.

3. **#6284** PR ([link](https://github.com/agentscope-ai/CoPaw/pull/6284)) — QwenPaw Creator app. **Open for 7 days** (since July 20), marked "Under Review" but no feedback. Could discourage the contributor.

**PRs that are stuck:**
- **#6276** ([link](https://github.com/agentscope-ai/CoPaw/pull/6276)) — Unified browser SDK. **Open for 7 days**, no comments. Represents significant architectural investment.
- **#6387** ([link](https://github.com/agentscope-ai/CoPaw/pull/6387)) — Channel installation/version repair. **Open for 4 days**, could address multiple plugin-related issues (#6473).

**Recommendation**: Prioritizing the MCP transport fix (#6470) and the Windows PATH fix (#6239) would resolve the highest-impact user-facing bugs. The cron keepalive PR (#6481) is small and ready for review, and merging it would demonstrate responsiveness to the community.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-27

## Today's Overview

ZeroClaw is in a high-intensity development cycle with **50 open issues and 48 open pull requests** updated in the last 24 hours, signaling a major push toward the v0.8.4 release. Two PRs were merged/closed today, including a Landlock sandbox fix that prevented ZeroClaw from locking itself. No new releases were cut today, but the release branch for v0.8.4 (PR #9376) is actively being prepared, encompassing crates.io publishing readiness and changelog assembly. The project continues to exhibit strong maintainer engagement, with multiple contributors submitting focused security and stability patches simultaneously.

## Releases

No new releases today. The v0.8.4 release candidate is in active preparation via PR #9376.

## Project Progress

**Merged/Closed PRs:**
- **PR #9233** (Merged): `fix(runtime/security): Prevent Landlock locks zeroclaw itself` — Fixed a critical bug where the Landlock sandbox's `restrict_self()` was called in the parent daemon process, locking the ZeroClaw daemon itself inside the sandbox after the first sandboxed shell command. This unblocks shell tool usage on Fedora (related to Issue #8973).
- One additional PR was closed (details not shown in top 20).

**Active Development Themes from Today's PRs (submitted in last 24h):**
- **Security fixes across multiple components**: PR #9410 (default command audit logging to disabled), PR #9401 (preserve shell cwd across sandbox wrappers), PR #9402 (avoid nesting Docker sandbox inside Docker runtime), PR #8826 (gate image_gen download URL against SSRF)
- **Provider authentication improvements**: PR #9420 (support stored OAuth profiles for Anthropic), PR #9419 (rotate live credentials after rate limits), PR #9400 (share OAuth refresh retry control flow)
- **Chat channel fixes**: PR #9382 (enforce WhatsApp Web chat policies under both modes), PR #9181 (send Nextcloud Talk replies via signed bot API), PR #9385 (implement request_approval for WhatsApp Web)
- **Runtime stability**: PR #9418 (multiplex stdio MCP calls without replaying unknown outcomes), PR #9403 (bound WASM exports by wall-clock deadline)
- **Documentation and governance**: PR #9388 (retire CONTRIBUTORS.md and ground maintainer roles), PR #9416 (document AllToolsResult.tools pre-filter registry)

## Community Hot Topics

**Most Active Issues (by comment count):**

- **[#7462] [Bug]: 74 test failures on Windows** (14 comments) — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)
  - Running the workspace test suite on Windows 11 yields 74 failing tests due to Unix-only test commands, path semantics, and console encoding issues. CI does not catch this because tests only run on Linux. User @NiuBlibing highlights a critical CI blind spot that affects Windows compatibility. Linked to Feature Request #7461 (add Windows/macOS CI).

- **[#9101] Consolidate release attestation mechanisms** (7 comments) — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9101)
  - v0.8.3 shipped with three parallel provenance/signing mechanisms (cosign, GitHub artifact attestations, SLSA), causing CI time redundancy and contributor confusion. Community member @JordanTheJet proposes reducing from 53 release assets to ~20 with one unified signing story.

- **[#5514] [Bug]: batch Telegram media groups into one multimodal turn** (6 comments) — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/5514)
  - Sending multiple images in Telegram causes the agent to perceive each as a separate request, generating redundant output messages. This has been open since April and is in progress but not yet resolved.

- **[#6157] [Bug]: Nextcloud Talk use correct bot message API** (6 comments) — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6157)
  - Nextcloud Talk response messages fail because the wrong bot message API endpoint is used. PR #9181 directly addresses this with the correct bot API endpoint and signed authentication.

**Most Active PRs (all submitted today):**
- **[#9376] chore(release): cut v0.8.4** — [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9376)
  - The v0.8.4 release preparation PR, making the workspace publishable to crates.io for the first time since the microkernel split. 18 crates to publish, 5 remain workspace-only.

**Underlying Needs Analysis:**
The community is strongly focused on three core needs: **(1)** Cross-platform reliability (Windows, macOS are underserved), **(2)** Authentication and credential management (OAuth support, API key security, rotation), and **(3)** Sandbox/security correctness (Landlock, Docker nesting, SSRF prevention).

## Bugs & Stability

**Critical (S1 - Workflow Blocked):**
- **#8559** — Agents stop when exiting the web dashboard chat window. PRs being discussed.
- **#8560** — `browser_open` hangs the agent turn indefinitely when window cannot be opened.
- **#7527** — macOS desktop app can reopen blank or without a window (blocked, needs reproducer).
- **#9085** — Nested runtime panic in `try_enable_pgvector` when pgvector is enabled.

**High/S2 - Degraded Behavior:**
- **#9386** (new today) — Gemini API key in request URL survives `sanitize_api_error` and is posted into chat. **PR fix needed.**
- **#8654** — Skill-review fork panics with out-of-range slice, causes SIGSEGV after tool-heavy turns.
- **#8973** — Landlock blocks shell access on Fedora (fix merged in PR #9233).
- **#8731** — Stdio-based MCP servers accumulate as zombie processes.

**Medium (S3 - Minor):**
- **#8810** — Telegram documentation is wrong/outdated.
- **#9046** — `models_cache.json` is read but never written.

**Fixes Available:**
- #8973 (Landlock on Fedora) — Fixed by PR #9233 ✅
- #6157 (Nextcloud Talk API) — Fix in PR #9181 (open)
- #6350 (WhatsApp allowed-numbers bypass) — Fix in PR #9382 (open)

## Feature Requests & Roadmap Signals

**User-Requested Enhancements:**
- **#8409** — Cron shell jobs should support raw stdout output (opt-in, 1 comment, status accepted).
- **#7099** — Route `zeroclaw status` output through CLI i18n layer.
- **#7461** — Run test suite on Windows and macOS in CI (not just Linux).

**Predictions for v0.8.4:**
Based on active PRs and the release branch, v0.8.4 will likely include:
- Unified release signing/attestation mechanism (reducing 53 assets)
- LLM provider credential rotation (rate-limit aware)
- Fixed Nextcloud Talk and WhatsApp Web channel implementations
- OAuth profile support for Anthropic
- Default command audit logging disabled (reverses v0.8.3 default)
- Sandbox improvements (Landlock, Bubblewrap, Docker nesting prevention)

## User Feedback Summary

**Pain Points:**
- Windows users face 74 test failures and cannot contribute safely (Issue #7462)
- macOS users experience blank/unresponsive desktop app (Issue #7527, needs reproduction)
- WhatsApp Web users on business mode find configured policies silently ignored (Issue #6350)
- Terminal/headless users cannot use `browser_open` without a display (Issue #8560)
- Android/Termux users get wrong binary architecture (Issue #7911)
- Chinese-language users (console code page 936) have unique path encoding failures (Issue #7462)

**Satisfaction Indicators:**
- Active community contributions across security (perillamint, wangmiao0668000666), channels (belumume), and providers (IftekharUddin, vrurg)
- High maintainer responsiveness — many accepted labels and in-progress statuses
- Structured governance work (PR #9388) shows project maturation

**Use Cases Expressed:**
- Production deployment with Docker on non-Linux hosts
- WhatsApp for business customer support automation
- CI/CD pipeline integration with cron jobs
- Multi-provider failover with API key rotation

## Backlog Watch

**Long-Open Issues Needing Attention:**
- **#5514** (Telegram media groups) — Open since April 8, 6 comments, P2, in-progress but no fix PR.
- **#6157** (Nextcloud Talk API) — Open since April 27, 6 comments, P2, PR #9181 open for 7 days.
- **#6350** (WhatsApp allowed-numbers bypass) — Open since May 3, 2 comments, P1, PR #9382 addresses this.
- **#7527** (macOS blank window) — Open since June 12, 2 comments, P1, blocked — needs a working reproducer from reporter.
- **#7462** (Windows test failures) — Open since June 10, 14 comments, P1, accepted but no fix PR yet.

**PRs Waiting for Author Action:**
- **#8337** (Herdr agent integration) — Needs author action since June 26.
- **#8826** (SSRF gate for image_gen) — Needs author action since July 8.
- **#9115** (Blacksmith CI runners) — Needs author action since July 17.
- **#9181** (Nextcloud Talk fix) — Needs author action since July 19.
- **#9382** (WhatsApp Web policy fix) — Needs author action since yesterday.

**Maintainer Attention Required:**
- **#9386** (Gemini API key leak) — Filed just today, P1, accepted, risk high. This is an active security vulnerability requiring prompt triage and fix.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*