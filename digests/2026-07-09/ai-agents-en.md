# OpenClaw Ecosystem Digest 2026-07-09

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-09 01:29 UTC

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

# OpenClaw Project Digest — July 9, 2026

## Today's Overview

OpenClaw shows extremely high activity with 500 issues and 500 PRs updated in the last 24 hours — indicating either a massive community-driven triage event or automated sweeper activity across the entire backlog. Only 41 of the updated issues (8.2%) were closed, suggesting maintenance is largely in review/assessment mode rather than resolution. The project has **no new releases** today. There are 417 open PRs and 83 merged/closed, reflecting a moderate throughput of ~17% merge/close rate. Priority remains on stability and security, with P1 diamond lobster issues (the highest severity rating) dominating the top of both issue and PR activity.

- Total open issues updated: 459; closed: 41
- Total open PRs updated: 417; merged/closed: 83
- New releases: 0

---

## Releases

No new releases were published today. The latest available version remains **OpenClaw 2026.6.x** (exact latest patch not specified from this data). Users should watch for the pending release that addresses the accumulation of P1 diamond-lobster bugs related to session-state corruption, message loss, and security vulnerabilities.

---

## Project Progress

Today's merged/closed PR count of 83 indicates solid forward progress. Key fixes and features that advanced include:

- **Memory/Snippet Truncation (#101946)** — Fix for invalid UTF-16 surrogate pairs in `memory-core` dreaming snippet truncation
- **Control UI Chat History (#102143)** — Increased chat history limit from 100 to 500 messages
- **Settings Deep Merging (#102333, #102330)** — Critical fixes for nested settings objects being incorrectly shallow-merged across scopes, causing silent field drops (especially for `retry.provider` config)
- **SSRF Loopback Allowance (#101991)** — Fix allowing loopback for hostnames already in the `allowedHostnames` trust list
- **WebChat Activity for iOS (#102309)** — UI fix showing chat activity after foreground refresh on iOS
- **Proxy Capture Oversized Responses (#101268)** — Guard against unbounded `arrayBuffer()` reads in proxy capture
- **Non-ClawHub Plugin Warnings (#102197)** — New install-time warning before installing plugins from sources outside ClawHub review (XL-sized PR affecting 18+ channels/extensions)
- **Multimodal Function Response Fix for Google/Gemini (#102327)** — Properly recognizing provider-prefixed Gemini 2.x model IDs
- **OpenAI Refusal Surface (#102334)** — Making chat-completions `refusal` field visible as text instead of silent empty response
- **Comfy Private Service Hostnames (#99065)** — Allowing Docker/Compose service hostnames in Comfy local workflows

---

## Community Hot Topics

### Most Active Issues (by comment count)

| Issue | Comments | 👍 | Status |
|-------|----------|---|--------|
| [#25592 — Text between tool calls leaks to messaging channels](https://github.com/openclaw/openclaw/issues/25592) | 35 | 1 | OPEN |
| [#44925 — Subagent completion silently lost — no retry/notification/auto-restart](https://github.com/openclaw/openclaw/issues/44925) | 21 | 1 | OPEN |
| [#48003 — Steer mode doesn't inject messages mid-turn](https://github.com/openclaw/openclaw/issues/48003) | 15 | 3 | OPEN |
| [#85333 — `openclaw doctor --fix` 4-5x slower (performance regression)](https://github.com/openclaw/openclaw/issues/85333) | 15 | 1 | OPEN |
| [#45740 — gh-issues skill: untrusted issue body injected into sub-agent prompt (security)](https://github.com/openclaw/openclaw/issues/45740) | 14 | 1 | OPEN |

### Underlying Community Needs

1. **Message Integrity & Channel Hygiene**: The #1 concern (35 comments on #25592) is that internal agent processing text is leaking to users. This is compounded by #44905 (Discord leaking tool-call traces) and #41744 (Feishu losing media). The community clearly demands clean, predictable message delivery.

2. **Session Stability & Orchestration Reliability**: Multiple top-voted issues center on sessions breaking silently — subagents lost (#44925), sessions hanging (#43661), and multi-agent orchestration causing config overwrites (#43367). Users running production deployments are hitting reliability walls.

3. **Security Sandbox Tightening**: Issue #45740 (untrusted GitHub issue body injection) and #39604 (request for private network access toggle) show a community actively hardening their deployments but needing better tooling controls.

### Most Active PRs

| PR | Comments | Status |
|----|----------|--------|
| [#102333 — deep-merge nested settings](https://github.com/openclaw/openclaw/pull/102333) | — | OPEN, needs proof |
| [#102331 — Google Meet session affinity](https://github.com/openclaw/openclaw/pull/102331) | — | OPEN, ready for maintainer |
| [#102202 — tasks.list re-sort performance fix](https://github.com/openclaw/openclaw/pull/102202) | — | OPEN, ready for maintainer |
| [#89041 — Discord WS 8.21.0 receiver limits](https://github.com/openclaw/openclaw/pull/89041) | — | OPEN, ready for maintainer (stale) |

---

## Bugs & Stability

### Critical (P0 — Release Blockers)

| Issue | Summary | Has Fix PR? |
|-------|---------|------------|
| [#43661 — Session hangs indefinitely on compaction timeout, causing duplicate message sends](https://github.com/openclaw/openclaw/issues/43661) | Session hang → repeated duplicate messages to user | No |
| [#48920 — Live Docs ahead of release](https://github.com/openclaw/openclaw/issues/48920) | Documentation references features not yet shipped in stable | No |

### High Severity (P1 — Diamond Lobster / Platinum Hermit)

1. [#25592 — Text between tool calls leaks to messaging channels](https://github.com/openclaw/openclaw/issues/25592) — **Core UX integrity issue** — No fix PR yet
2. [#44925 — Subagent completion silently lost](https://github.com/openclaw/openclaw/issues/44925) — Silent data loss in subagent orchestration — No fix PR yet
3. [#48003 — Steer mode fails to inject messages mid-turn](https://github.com/openclaw/openclaw/issues/48003) — Message routing broken — No fix PR yet
4. [#85333 — `openclaw doctor --fix` 4-5x slower regression](https://github.com/openclaw/openclaw/issues/85333) — Performance regression in core maintenance command — No fix PR yet
5. [#94228 — Anthropic thinking block signature invalid on long sessions](https://github.com/openclaw/openclaw/issues/94228) — Session permanently bricks — No fix PR yet
6. [#43367 — Multi-agent orchestration unstable](https://github.com/openclaw/openclaw/issues/43367) — Config overwrites, detached child work — No fix PR yet
7. [#39476 — A2A `sessions_send` causes duplicate messages](https://github.com/openclaw/openclaw/issues/39476) — Agent-to-agent messaging loop — No fix PR yet
8. [#41165 — Telegram DMs polluting main session](https://github.com/openclaw/openclaw/issues/41165) — Routing bug — No fix PR yet

### Regressions Reported Today

Several regressions were reported or remain active:
- [#85333](https://github.com/openclaw/openclaw/issues/85333) — `doctor --fix` performance regression (2026.5.19→5.20)
- [#38327](https://github.com/openclaw/openclaw/issues/38327) — "Cannot convert undefined or null to object" with Google Vertex (2026.3.2)
- [#38439](https://github.com/openclaw/openclaw/issues/38439) — Webchat avatar 404 (regression)
- [#45494](https://github.com/openclaw/openclaw/issues/45494) — Cron jobs silently time out instead of fast-failing on API errors

### New Bugs Reported Today (July 9)

| Issue | Summary | Severity |
|-------|---------|----------|
| [#99912](https://github.com/openclaw/openclaw/issues/99912) | Agent heartbeat routes to wrong agent's session | P1, diamond lobster |
| [PR #102325](https://github.com/openclaw/openclaw/pull/102325) _(closed)_ | Cron main-session wakes skipped as disabled without per-agent heartbeat config | P2 |

Several new fix PRs target open bugs — most notably #102331 (Google Meet wrong agent), #102329 (Anthropic image blocks crash on text-only models), and #102074 (reply session permanent wedge).

---

## Feature Requests & Roadmap Signals

### Top User-Requested Features (by 👍 count)

| Issue | Feature | 👍 | Priority |
|-------|---------|---|----------|
| [#39604](https://github.com/openclaw/openclaw/issues/39604) | `tools.web.fetch.allowPrivateNetwork` config key | 11 | P2 |
| [#42840](https://github.com/openclaw/openclaw/issues/42840) | MathJax/LaTeX rendering in Control UI | 9 | P2 |
| [#45608](https://github.com/openclaw/openclaw/issues/45608) | Pre-reset agentic memory flush (`/new`, daily reset) | 4 | P2 |
| [#42026](https://github.com/openclaw/openclaw/issues/42026) | Distributed Agent Runtime (separate control plane from compute) | 3 | P2 |
| [#45758](https://github.com/openclaw/openclaw/issues/45758) | YAML config file format support | 2 | P3 |

### Predictions for Next Release

Based on PR activity and severity velocity:

1. **Deep settings merge fix** — Two PRs (#102333 and #102330) both landed today for the same root cause; expect this merged within 48 hours
2. **Anthropic thinking block crash fix** — PR #102329 directly addresses the session-bricking bug (#94228); high likelihood of merge
3. **Non-ClawHub install warnings** — PR #102197 is in "ready for maintainer look" status; security-focused change likely to land
4. **Web_fetch range check fix** — PR #102335 fixes a subtle truncation-reporting bug; small change, high value

### Longer-term Roadmap Signals

- **RFC: Distributed Agent Runtime** (#42026) — Represents a significant architectural shift, separating control plane from agent compute. This would enable horizontal scaling and true multi-instance deployments.
- **Multi-Session Architecture** (#48874) — Proposed shared LLM layer with isolated sessions, indicating community interest in enterprise multi-tenant deployments.
- **Gateway lifecycle hooks** (#43454) — Users want event-driven automation (onSubagentComplete, onToolCallThreshold), pointing to CI/CD integration needs.

---

## User Feedback Summary

### Pain Points

1. **"Silent failures are the loudest complaints"** — Users consistently report that agent orchestration fails without notification. Subagent tasks are lost (#44925), cron jobs time out without alerting (#45494), and session compaction hangs silently (#43661). Operators cannot trust the system without external monitoring.

2. **"My agent talks to the wrong people"** — Cross-channel message routing continues to plague users. Telegram DMs land in main sessions (#41165), Discord leaks internal tool traces (#44905), and A2A calls produce duplicate messages (#39476). Users need strict message boundaries.

3. **"Everything is slow and growing"** — Performance regressions hit core tooling (`doctor --fix` at 4x slower, #85333), session files bloat unboundedly (#45718), and the Control UI paginates at only 100 messages (#102143). Users on production VPS are feeling the pain.

4. **"Configuration is fragile and opaque"** — Settings deep-merge bugs (#102318) silently drop config fields. Session-reset startup messages are hardcoded (#45501). YAML is requested (#45758). Users want configuration that behaves predictably.

### Use Cases

- **Multi-agent group chat** — Real-world usage of natural-language rule training across agents sharing the same model (#41366)
- **Production cron automation** — Users running scheduled agent tasks that silently fail on provider outages (#45494)
- **Browser automation at scale** — Extensive field testing across 9+ email providers highlights CSS selector gaps and broken file uploads (#44431)
- **Enterprise cost management** — Per-agent cost budgets (#42475) and archived session file tracking (#46252) show operators monitoring spend

### Satisfaction/Dissatisfaction

**Satisfaction signals:**
- 11 👍 on the private network access request (#39604) — users trust the security model but want granular opt-in
- 9 👍 on LaTeX rendering (#42840) — academic/scientific users are engaging deeply enough to request math support
- Multi-agent orchestration is being actively adopted despite friction

**Dissatisfaction signals:**
- Diamond lobster rating (highest severity) on 15+ open issues — users are filing extremely detailed, well-researched bug reports, indicating high engagement but also high frustration
- "Maturity: stable" tag on 10+ of top bugs — these aren't edge cases; they affect production deployments
- 3 people reporting the same memory management chaos (#43747) with inconsistent behavior across machines

---

## Backlog Watch

### Critical Items Needing Maintainer Attention

| Issue/PR | Status | Age | Why Important |
|----------|--------|-----|---------------|
| [#25592 — Text leaks to channels](https://github.com/openclaw/openclaw/issues/25592) | Needs security review, needs product decision | ~135 days | #1 by comment count; core UX poison |
| [#44925 — Subagent completion lost](https://github.com/openclaw/openclaw/issues/44925) | Needs maintainer review | ~118 days | Silent data loss pattern |
| [#45740 — gh-issues prompt injection](https://github.com/openclaw/openclaw/issues/45740) | Needs security review | ~117 days | Security vulnerability |
| [#22439 — Tiered bootstrap loading PR](https://github.com/openclaw/openclaw/pull/22439) | Ready for maintainer (stale) | ~138 days | Token efficiency for large workspaces |
| [#43661 — Session hangs on compaction timeout (P0)](https://github.com/openclaw/openclaw/issues/43661) | Needs product decision | ~119 days | Release-blocker severity |

### Oldest High-Severity Issues Still Open

- [#25592](https://github.com/openclaw/openclaw/issues/25592) — Created Feb 24, 2026 (135 days ago) — **Text between tool calls leaks**
- [#22439 PR](https://github.com/openclaw/openclaw/pull/22439) — Created Feb 21, 2026 (138 days ago) — **Tiered bootstrap loading** — stale with "ready for maintainer" label
- [#38327](https://github.com/openclaw/openclaw/issues/38327) — Created Mar 6, 2026 (125 days ago) — **Vertex/Gemini regression**

### Watch List

The `clawsweeper:needs-live-repro` label on several high-severity bugs (#85333, #94228, #39476, #44905, #38439, #41366, #42820) suggests these require real-time reproduction that maintainers have not been able to achieve. These may benefit from community reproduction efforts or better logging to capture root cause.

---

*This digest was generated from GitHub activity data for the OpenClaw project (github.com/openclaw/openclaw) as of 2026-07-09. Data reflects issues and PRs updated in the last 24 hours.*

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-07-09 | **Analyst:** AI Agent Open-Source Ecosystem Team

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing **intense, multi-front development** with at least 10 actively maintained projects. Activity is concentrated on three core challenges: **agent reliability** (session stability, message delivery, context integrity), **channel/plagorm expansion** (Discord, Telegram, Matrix, WeCom, QQ, Feishu, Slack, WhatsApp), and **security hardening** (token governance, plugin trust, private network controls). Projects are converging on WSAM plugin architectures and multi-agent orchestration patterns, but each differentiates through its primary interface (CLI/headless, WebUI/multi-channel, or mobile-first). The ecosystem is roughly divided between mature "reference" implementations (OpenClaw) with large community backlogs, and newer minimalist projects (PicoClaw, TinyClaw, Moltis) that prioritize simplicity but lack feature parity. Community health indicators are strong overall, though several projects show concerning backlogs of stale high-severity bugs that risk trust erosion.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | Issues Closed | PRs Updated (24h) | PRs Merged/Closed | New Release? | Health Score* |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500 | 41 (8.2%) | 500 | 83 (16.6%) | ❌ | 🟡 **Stable with backlogs** |
| **NanoBot** | 8 (7 closed) | 7 (87.5%) | 27 | 7 (25.9%) | ❌ | 🟢 **Responsive & healthy** |
| **Hermes Agent** | 50 | 7 (14%) | 50 | 8 (16%) | ✅ v0.18.2 | 🟡 **Active, data loss risk** |
| **PicoClaw** | 2 | 0 | 3 | 3 (100%) | ❌ | 🟢 **Steady, community-driven** |
| **NanoClaw** | 2 | 0 | 28 | 4 (14.3%) | ❌ | 🟢 **High velocity, queue bottleneck** |
| **NullClaw** | 0 | 0 | 0 | 0 | ❌ | ⚫ **Inactive** |
| **IronClaw** | 22 | 7 (31.8%) | 50 | 11 (22%) | ❌ | 🟡 **Intense dev, systemic failures** |
| **LobsterAI** | (moderate) | (high) | (high) | 10 | ❌ | 🟢 **Strong fix cycle** |
| **TinyClaw** | 0 | 0 | 1 | 1 (100%) | ❌ | 🟢 **Stable but quiet** |
| **Moltis** | 0 | 0 | 1 | 0 | ❌ | 🟡 **Minimal activity** |
| **CoPaw** | 38 | (many) | 47 | 15 (31.9%) | ✅ v2.0.0-beta.4 | 🟢 **High velocity, beta stabilization** |
| **ZeptoClaw** | 0 | 0 | 0 | 0 | ❌ | ⚫ **Inactive** |
| **ZeroClaw** | 50 | 10 (20%) | 50 | 16 (32%) | ❌ | 🟢 **High velocity, RFC-driven** |

*Health Score: 🟢 Green (active, responsive), 🟡 Yellow (active with concerns), 🔴 Red (critical issues), ⚫ Black (inactive).*

**Key Takeaways:**
- **Volume leaders:** OpenClaw, ZeroClaw, Hermes, IronClaw, CoPaw all show 50+ updated items daily.
- **Most responsive (highest close rate):** NanoBot (87.5% issues closed), TinyClaw (100% PRs merged).
- **Most backlogged:** OpenClaw (only 8.2% issues closed despite 500 updates) — likely a triage/tagging event.
- **Releasing today:** Hermes (v0.18.2 patch), CoPaw (v2.0.0-beta.4).

---

## 3. OpenClaw's Position

### Advantages vs. Peers
- **Scale of community engagement:** 500+ issues/PRs touched daily dwarfs every other project (nearest: Hermes/ZeroClaw at 50). OpenClaw is the de-facto reference implementation.
- **Feature breadth:** Handles 12+ messaging channels (Discord, Telegram, Feishu, Matrix, WeCom, QQ, Slack, WhatsApp, iMessage, etc.), multi-agent orchestration, cron, browser automation — unmatched coverage.
- **Security maturity:** Dedicated diamond-lobster severity classification (P1), security vulnerability reports actively triaged. Has a ClawHub plugin review system.
- **Enterprise adoption signals:** Distributed agent runtime RFC, per-agent cost budgets, archived session file tracking — features for operators, not hobbyists.

### Technical Approach Differences
- **Multi-session architecture** (RFC #48874) separates shared LLM layer from isolated sessions — an enterprise multi-tenant design that most peers lack.
- **Session compaction/coring** with graduated pressure relief (unlike CoPaw's context loss in scroll) — but the approach is still causing data loss bugs (#43661).
- **Language ecosystem:** TypeScript/Node.js (vs. Python for NanoBot, CoPaw; Rust for ZeroClaw; Go for IronClaw) — limits direct code sharing but benefits from JS ecosystem breadth.

### Community Size Comparison
- **OpenClaw:** ~100-200 daily active contributors (by PR/issue authorship). Largest ecosystem with ClawHub plugin store.
- **Tier 2 (10-50 daily contributors):** Hermes Agent, ZeroClaw, CoPaw, IronClaw.
- **Tier 3 (<10 daily contributors):** NanoBot, NanoClaw, PicoClaw, LobsterAI.
- **Tier 4 (<5 daily):** TinyClaw, Moltis, NullClaw, ZeptoClaw.

---

## 4. Shared Technical Focus Areas

| Focus Area | Affected Projects | Specific Need |
|---|---|---|
| **Session/Context Integrity** | OpenClaw, Hermes, IronClaw, CoPaw, ZeroClaw | Silent session compaction deletes data (#43661, #61145, #5838, #5860, #6034). Context overflow causes hallucination (#6517). Message delivery failure without error (#2985). |
| **Provider API Robustness** | OpenClaw, Hermes, IronClaw, ZeroClaw, CoPaw | Rate-limiting saturation (#5859). Model ID drift (Gemini misrouting #39047). Custom API failures (#6034). Thinking block signature invalidity (#94228). |
| **Channel/Plagorm Reliability** | OpenClaw, Hermes, PicoClaw, CoPaw, ZeroClaw | Feishu drops messages (#5757). QQ bot startup failure (#58646). Matrix auth breaks on upgrade (#5868). Telegram routing wrong agent (#41165). Discord leaks tool traces (#44905). |
| **Security Hardening** | OpenClaw, NanoBot, Hermes, ZeroClaw, TinyClaw, CoPaw | WebUI token issuance to unauthenticated callers (#4825). Untrusted content injection in sub-agents (#45740). `rm -rf ${HOME}` bypass (#5090). Workspace file protection missing `.ignore` (ZeroClaw #8424). |
| **Multi-Agent Orchestration** | OpenClaw, Hermes, NanoClaw, LobsterAI, CoPaw | Subagent completion silently lost (#44925). Config overwrites in multi-agent setups (#43367). Agent-to-agent messaging loops (#39476). Team delegation improvements (LobsterAI #2285). |
| **Desktop App Quality** | Hermes, ZeroClaw, CoPaw | macOS quit doesn't stop gateway (#61087). Chinese text truncated (#39534). App non-functional on fresh macOS install (#7527). Windows encoding bugs (#61211). |
| **Performance Regressions** | OpenClaw, Hermes, IronClaw | `doctor --fix` 4-5x slower (#85333). Cold-start skills bottleneck (#3356). Routines near-zero success rate due to "No thread attached" (#5836). |

**Emerging Pattern:** Context integrity is the **#1 cross-project pain point**. Three projects (OpenClaw, Hermes, IronClaw) have P0/P1 bugs for data loss during session compaction or cleanup. This is the ecosystem's most urgent shared engineering challenge.

---

## 5. Differentiation Analysis

| Project | Primary Interface | Target User | Architectural Distinction |
|---|---|---|---|
| **OpenClaw** | CLI + WebUI + all messaging channels | Power users, enterprise ops | Reference implementation. ClawHub plugin store. Deepest channel coverage. Largest community. |
| **NanoBot** | Python SDK + CLI | Developers integrating agents into workflows | Utility-focused (onboard, config refresh, Docker). Strongest maintainer responsiveness. |
| **Hermes Agent** | Desktop app + CLI + multi-channel | End-users, researchers | Desktop-first UX (macOS, Windows, Linux). Patch pipeline is fast. ACP/editor integration stalled. |
| **PicoClaw** | Embedded (NanoKVM) + webhooks | Hardware/IoT developers | Lightweight, deployment on edge devices. Grafana Alertmanager integration signals DevOps/observability use. |
| **NanoClaw** | CLI + Discord/WhatsApp/Slack | Teams, channel operators | Scheduled-tasks train (5-part initiative) for production cron replacement. Agent template system. |
| **IronClaw** | WebUI + extensions | Enterprise, managed platform | NEAR AI integration. Extension registry with WASM tools. SSO, admin panel, private installs. |
| **LobsterAI** | Cowork system + IM channels | Enterprise multi-agent deployments | Strong subagent collaboration flow. Scheduled tasks crisis from v4.1 boot-loop regression. |
| **TinyClaw** | Minimal headless | Security-conscious, minimalists | Very small codebase. Hardened channel auth. Update integrity checks. Unclear roadmap. |
| **Moltis** | Rust library/CLI | Rust developers building custom agents | Rust-based. Minimal activity; CalDAV integration suggests calendar/automation focus. |
| **CoPaw** | Console + TUI + Windows UIA | Chinese-speaking power users, desktop automators | Scroll context compression. DeepSeek/Qwen model optimization. Memory distillation plugin. |
| **ZeroClaw** | CLI + WebUI + all channels | Developers, multi-agent operators | WSAM plugin architecture (in RFC). Model-catalog fix for xAI/Groq/DeepSeek. ZeroCode tracker parity with Claude Code. |

**Key Differentiation Axes:**
- **Language:** Node.js (OpenClaw, NanoClaw) vs. Python (NanoBot, CoPaw, LobsterAI) vs. Rust (ZeroClaw, Moltis) vs. Go (IronClaw)
- **Deployment Model:** Cloud/container (NanoBot, IronClaw) vs. Edge (PicoClaw) vs. Desktop (Hermes) vs. Any (OpenClaw, ZeroClaw)
- **User Base:** English/global (ZeroClaw, Hermes) vs. Chinese-dominant (CoPaw, LobsterAI, NanoClaw)
- **Plugin Model:** ClawHub (OpenClaw) vs. WSAM-in-progress (ZeroClaw) vs. Compile-time (IronClaw) vs. SDK/tool-based (NanoBot)

---

## 6. Community Momentum & Maturity

### Tier 1: Rapidly Iterating (High Feature Velocity, Active Bug Fixing)
**OpenClaw, ZeroClaw, Hermes Agent, CoPaw, IronClaw**

- All have 50+ daily PR/issue updates.
- All are shipping new features weekly (TodoWrite tracker, Scheduled Tasks train, UIA computer-use, extension unification).
- **Risk:** High velocity creates review bottlenecks (ZeroClaw has 94 open PRs; IronClaw's 50 PRs show 1:5 close:open ratio).

### Tier 2: Stabilizing (Feature-Complete, Focused on Reliability)
**NanoBot, LobsterAI, PicoClaw, TinyClaw**

- NanoBot closed 87.5% of issues today — clear triage discipline.
- LobsterAI merged 10 PRs fixing systemic bugs (USER.md scope, IM scoping).
- PicoClaw and TinyClaw are low-activity but reliable; TinyClaw merged a major security audit (PR #44).
- **Risk:** Low activity may mean low adoption (TinyClaw) or stalled roadmap (Moltis).

### Tier 3: Quiet / Maintenance-Mode
**Moltis, NullClaw, ZeptoClaw, TinyClaw**

- Zero or near-zero activity. Moltis has one single PR addressing a CalDAV panic.
- **Risk:** These projects may be abandoned or preserving cycles for future resumption.

### Community Sentiment Summary
- **Trust erosion risks:** OpenClaw (135-day-old text leakage bug), Hermes (data loss bug with fix submitted but not merged), IronClaw (systemic routine failures).
- **Strong positive sentiment:** NanoBot (researcher found vulnerability → fix within 24h), LobsterAI (USER.md fix merged same day as report), CoPaw (beta.4 addresses top regression).

---

## 7. Trend Signals

### 1. Context Integrity is the #1 Reliability Challenge
Every major project has a "session compacted/cleaned/compressed my data" bug. The ecosystem lacks a safe, standard approach to context window management. **Value for developers:** Invest in defensive context validation before building new features. A shared "context integrity layer" could become a de-facto standard.

### 2. Multi-Agent Orchestration is Moving from "Experimental" to "Expected"
OpenClaw, LobsterAI, CoPaw, NanoClaw, and ZeroClaw all have features or RFCs for multi-agent teams, sub-agent delegation, or swarm collaboration. **Value for developers:** Building single-agent-only systems risks obsolescence. The ecosystem demands agent-to-agent communication, credential isolation, and handoff protocols.

### 3. Security Auditing is Becoming Community-Driven
NanoBot, ZeroClaw, Hermes, and TinyClaw all received security vulnerability reports from external researchers in the last 24 hours. Projects with quick fix cycles (NanoBot) gain trust; those with stale disclosures (ZeroClaw #6672, #8094) risk reputation damage. **Value for developers:** Proactive vulnerability disclosure programs and 24-hour response SLAs are becoming differentiators.

### 4. Cross-Platform Desktop is Fragile
Hermes, ZeroClaw, and CoPaw all have macOS/Windows-specific bugs blocking users. Desktop apps are treated as second-class citizens compared to CLI/web interfaces. **Value for developers:** Expecting users to tolerate broken desktop experiences is a competitive vulnerability. Electron/Tauri code paths need equal engineering investment to server/CLI code.

### 5. The Plugin/Extension Model is Converging on WASM
ZeroClaw's RFC #8850 (WSAM runtime plugins), IronClaw's extension registry, OpenClaw's ClawHub, and TinyClaw's security-hardened bundle system all point to a future where agent functionality is distributed as sandboxed, portable plugins. **Value for developers:** If building a new agent project, design for WSAM plugin loading from day one — JSON skill definitions are insufficient.

### 6. Chinese-Language Community is Driving Real-World Production Use
CoPaw, LobsterAI, and parts of ZeroClaw's community are reporting bugs from live enterprise deployments (Feishu, WeCom, QQ channels). The issues are not "what if" scenarios — users are running these agents 24/7 and reporting context loss, silent failures, and channel unreliability. **Value for developers:** Ignoring the Chinese-language user base means missing the most demanding, production-experienced segment of the ecosystem.

### 7. "Agent Doesn't Know Its Own Capabilities" is a UX Gap
ZeroClaw #5862 (agent unaware of cron) and OpenClaw's tool-discovery issues point to a fundamental missing feature: **agent capability self-reflection**. Users expect agents to proactively offer their own features. **Value for developers:** Building a tool registry that the agent can introspect and advertise to users is a high-leverage UX improvement.

---

*End of report. Generated from GitHub digest data for 2026-07-09.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-09

## 1. Today's Overview

NanoBot saw high activity today with 27 pull requests updated and 7 of 8 issues closed. The development team is heavily focused on fixing a cluster of **WebUI security vulnerabilities** discovered by security researchers, with three closely related advisories closed and corresponding fix PRs submitted. Beyond security, the team advanced several infrastructure improvements including MCP reconnect stability, shell process management, and dependency flexibility. One new enhancement request for non-interactive config refresh remains open and has a companion PR already submitted, suggesting it may land soon. Overall, the project is in a healthy, responsive state with maintainers actively triaging and addressing both security reports and feature requests.

## 2. Releases

**No new releases** — last release date is unknown. Several PRs that could form a minor release (security fixes, MCP stability improvements, config refresh) are in progress.

## 3. Project Progress

**7 PRs merged/closed today**, representing meaningful progress across multiple areas:

| Area | PR | Impact |
|------|-----|--------|
| **Security** | [#4849 fix(webui): gate bootstrap API token issuance](https://github.com/HKUDS/nanobot/pull/4849) | Critical fix: splits WebUI WebSocket tokens from REST API tokens, only returns API token after verifying `tokenIssueSecret` or static token |
| **Infrastructure** | [#4848 refactor(agent): extract turn hook assembly](https://github.com/HKUDS/nanobot/pull/4848) | Clean architecture improvement: moves per-turn hook assembly into dedicated module, adds focused tests |
| **Documentation** | [#4850 docs: improve search entry pages](https://github.com/HKUDS/nanobot/pull/4850) | Restructures README with search-oriented capability section, adds docs/guides entry pages |
| **Config** | [#4852 Feature: non-interactive config refresh](https://github.com/HKUDS/nanobot/pull/4852) | Adds `nanobot onboard --refresh` for automated config updates (addresses #4851) |
| **Chore** | [#4460 chore: bump to node 24](https://github.com/HKUDS/nanobot/pull/4460) | Dependency modernization |
| **Telegram** | [#12 feat: add vision support for Telegram](https://github.com/HKUDS/nanobot/pull/12) | Image recognition: base64-encodes Telegram images to LLM for multimodal support |
| **Bug** | [#4829 aiohttp missing in Slack deps](https://github.com/HKUDS/nanobot/pull/4829) | Fixes Slack plugin installation failure by adding `aiohttp` to slack dependencies |

## 4. Community Hot Topics

**Security advisories dominate today's discussion.** All three related WebUI vulnerability reports received rapid maintainer engagement:

- **[#4825 Security: Unauthenticated localhost callers can mint API tokens](https://github.com/HKUDS/nanobot/issues/4825)** (3 comments) — Reported by YLChen-007, describes how any local process can call `/webui/bootstrap` to get API tokens when no `tokenIssueSecret` or static `token` is configured. **Closed same day after fix in PR #4849.**

- **[#4827 Security: Embedded WebUI bootstrap issues bearer tokens to unauthenticated callers](https://github.com/HKUDS/nanobot/issues/4827)** (2 comments) — Companion issue to #4825 focusing on the embedded WebUI gateway. **Closed same day.**

- **[#4826 Security: WebUI bootstrap issues API-capable bearer tokens to localhost](https://github.com/HKUDS/nanobot/issues/4826)** (2 comments) — Third variant describing the same class of vulnerability. **Closed same day.**

The **most active open issue** is:

- **[#4851 Enhancement: non-interactive config refresh](https://github.com/HKUDS/nanobot/issues/4851)** (1 comment, new today) — User `alekwo` requests automated config updates without interactive prompts. A companion PR (#4852) was submitted and already merged, suggesting this will be delivered quickly.

**Underlying need**: Users want to deploy NanoBot in automated/containerized environments where manual configuration prompts are infeasible. Security researchers are actively auditing the project, and maintainers are responding quickly — a strong signal of project health.

## 5. Bugs & Stability

| Severity | Issue | Status | Summary |
|----------|-------|--------|---------|
| **Critical** | [#4825, #4827, #4826 - WebUI token leakage](https://github.com/HKUDS/nanobot/issues/4825) | **Closed** with fix | Any unauthenticated localhost process could mint API bearer tokens via `/webui/bootstrap`. Fix in PR #4849 splits token types and adds verification gate. |
| **High** | [#4829 aiohttp missing in Slack deps](https://github.com/HKUDS/nanobot/issues/4829) | **Closed** with fix | Slack plugin fails to install because `aiohttp` not listed in `pyproject.toml`. Quick fix merged. |
| **Medium** | [#2450 minimax-m2.7 fails on 2nd+ request](https://github.com/HKUDS/nanobot/issues/2450) | **Closed** (stale) | Cloud-hosted Ollama model breaks on subsequent requests with `Internal Server Error`. Marked as closed/stale. |
| **Medium** | [#2463 Architectural: prompt prefix mismatch](https://github.com/HKUDS/nanobot/issues/2463) | **Closed** (stale) | Persisted conversation history differs from actual prompt prefix sent to model. Closed as stale without resolution. |

**Open bug-fix PRs** that address stability issues:

- **[#4764 fix(mcp): isolate reconnect cancel scopes](https://github.com/HKUDS/nanobot/pull/4764)** — Prevents gateway crash when MCP HTTP stream expires. Still open with 2 reviewers.
- **[#4843 fix(mcp): defer stale stack cleanup during reconnect](https://github.com/HKUDS/nanobot/pull/4843)** — Companion to #4764, defers cleanup of stale async stacks to gateway shutdown.
- **[#4840 fix(shell): reap zombie processes](https://github.com/HKUDS/nanobot/pull/4840)** — Properly cleans up child processes on all exit paths (not just timeout/cancel).
- **[#4816 fix(runner): narrow BaseException catch](https://github.com/HKUDS/nanobot/pull/4816)** — Prevents catching `KeyboardInterrupt`, `SystemExit`, `MemoryError` in tool execution.

## 6. Feature Requests & Roadmap Signals

| Request | PR/Issue | Likelihood for Next Release |
|---------|----------|----------------------------|
| Non-interactive config refresh (`nanobot onboard --refresh`) | [#4851](https://github.com/HKUDS/nanobot/issues/4851) → [#4852 merged](https://github.com/HKUDS/nanobot/pull/4852) | **Very High** — Already merged |
| Dockerfile `NANOBOT_EXTRAS` arg for custom deps | [#4857 open](https://github.com/HKUDS/nanobot/pull/4857) | **High** — Small, non-breaking, solves containerization pain |
| Guided channel setup flows | [#4855 open](https://github.com/HKUDS/nanobot/pull/4855) | **Moderate** — Large PR with conflicts, needs resolution |
| RTK command rewriter for exec tool | [#4854 open](https://github.com/HKUDS/nanobot/pull/4854) | **Moderate** — New opt-in feature for exec security |
| `nano_timer` core tool | [#4853 open](https://github.com/HKUDS/nanobot/pull/4853) | **Moderate** — Small, dependency-free utility tool |
| Sustained goals gated behind runtime mode | [#4844 open](https://github.com/HKUDS/nanobot/pull/4844) | **Moderate** — Significant refactor with conflicts |
| Cron job model presets | [#4622 open](https://github.com/HKUDS/nanobot/pull/4622) | **Moderate** — User-requested (#4378), feature complete |
| File edit diff progress view in WebUI | [#4828 open](https://github.com/HKUDS/nanobot/pull/4828) | **Lower** — Nice UX improvement, priority p2 |
| Discord forwarded message preservation | [#2873 open](https://github.com/HKUDS/nanobot/pull/2873) | **Stale** — Open since April, needs maintainer review |

**Prediction**: The next release will likely include the security fixes (WebUI token gating), the non-interactive config refresh, Docker customization, and one or both MCP reconnect stability fixes.

## 7. User Feedback Summary

**Pain points expressed:**

- **Automated deployment friction**: User `alekwo` reports that `nanobot onboard` forces interactive prompts, making unattended config refreshes impossible in CI/CD. The fix (#4852) was merged same day — **strong maintainer responsiveness**.

- **Slack plugin broken**: User `alekwo` also reported missing `aiohttp` dependency in Slack extras, making the plugin unusable out of box. Fixed same day.

- **Security concerns**: Researcher YLChen-007 discovered that unauthenticated local processes could obtain full API access via the WebUI bootstrap endpoint. This is a **significant trust concern** for users running NanoBot on shared or multi-tenant systems. Rapid patching demonstrates the project takes security seriously.

- **Historical issues unresolved**: Issues #2463 (prompt prefix mismatch) and #2450 (Ollama Cloud regression) were closed as stale without resolution. Users who encountered these bugs may still be affected.

**Use cases driving development:**
1. **Containerized/automated deployments** (#4851, #4857)
2. **Multi-channel bot operation** — Feishu, Slack, Telegram vision, Discord
3. **Enterprise security posture** — Active security auditing
4. **Long-running autonomous agents** (#4844 sustained goals)

## 8. Backlog Watch

| Issue/PR | Age | Last Updated | Status | Concern |
|----------|-----|--------------|--------|---------|
| [#2463 Prompt prefix mismatch](https://github.com/HKUDS/nanobot/issues/2463) | 106 days | 2026-07-08 | **Closed/stale** | Architectural issue with conversation fidelity — closed without fix. Important for anyone relying on deterministic model responses. |
| [#2450 Minimax Ollama Cloud regression](https://github.com/HKUDS/nanobot/issues/2450) | 106 days | 2026-07-08 | **Closed/stale** | 2nd+ request fails with 500 error on cloud-hosted models. Stale-closed, may still be broken. |
| [#2873 Discord forwarded messages](https://github.com/HKUDS/nanobot/pull/2873) | 94 days | 2026-07-08 | **Open** | Bug fix for Discord integration — forwarded messages lose body text. Needs maintainer review. Badgerbees has provided regression tests. |
| [#4078 OpenAI-compat API unauthenticated](https://github.com/HKUDS/nanobot/issues/4078) | 40 days | 2026-07-08 | **Closed** | `/v1/chat/completions` accepts unauthenticated requests. Closed without visible fix — **potential gap** if the fix was applied elsewhere or not at all. |

**Recommendation**: The project should consider re-opening or documenting resolution for #2463 (prompt prefix accuracy) and #2450 (Ollama Cloud), as they represent real user-impacting issues that were allowed to go stale. The `long_task`/`complete_goal` tooling PR (#4844) and Discord fix (#2873) are both high-value contributions that deserve prompt review.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-07-09  
**Data Source:** GitHub (NousResearch/hermes-agent)

---

## 1. Today's Overview

Hermes Agent is experiencing **high-velocity development** with 50 issues and 50 PRs updated in the last 24 hours, suggesting a maturing but actively maintained project. A patch release (v0.18.2) was issued to fix a critical Docker build dependency for WhatsApp integration. The community is highly engaged, particularly around **gateway stability issues** (Matrix decryption, session hygiene, platform adapters) and **UX improvements** for the desktop and CLI interfaces. A significant number of bug reports involve platform-specific failures on Windows (file paths, Chinese character encoding) and message delivery reliability across multiple chat backends (Matrix, WeCom, QQ, IRC). The overall project health appears strong with rapid issue triage, but the volume of open issues (43 open, 7 closed today) and the presence of several P1 critical bugs indicate continuous operational challenges.

---

## 2. Releases

### v2026.7.7.2 – Hermes Agent v0.18.2 (Patch Release)

- **Date:** July 7, 2026
- **Type:** Same-day patch on v0.18.1

**Changes:**
- Fixed WhatsApp Baileys dependency by unpinning from a git commit and using the published `7.0.0-rc13` release.
- Resolves a Docker build failure for tagged releases.

**Breaking Changes:** None

**Migration Notes:** Users running Docker-based deployments should update to `v2026.7.7.2` to restore WhatsApp functionality. No configuration changes required.

---

## 3. Project Progress

### Merged/Closed PRs Today (8 total)

| PR # | Title | Status | Impact |
|------|-------|--------|--------|
| #52407 | fix: add default retention for cron output files to prevent disk fill | **Merged** | Prevents unbounded disk growth from cron job output logs. Addresses issue #52383. |
| #61087 | Desktop app does not stop gateway on quit (macOS) | **Closed** (PR merged prior) | User-facing fix for macOS gateway lifecycle. |
| #60955 | hermes-fallback-bug-report | **Closed** | Bug report; likely closed as duplicate or insufficient info. |
| #3356 | perf(ttft): eliminate cold-start skills frontmatter bottleneck | **Closed** | Performance improvement for first-token latency. |
| #28260 | custom_providers with self-signed HTTPS endpoints fail | **Closed** | SSL verification fix for custom provider HTTPS endpoints. |

**Key Feature Advances:**
- **Cron retention policy** (PR #52407) – automated pruning of old cron output files prevents disk exhaustion in long-running deployments.
- **Disk snapshot performance** (Issue #3356 closed) – cold-start skills parsing bottleneck addressed, improving Time-to-First-Token (TTFT).

---

## 4. Community Hot Topics

### Most Active Issues (by comments & reactions)

1. **[#39691 – Tool Output Compression via headroom-ai](https://github.com/NousResearch/hermes-agent/issues/39691)**  
   **9 comments, 12 👍**  
   *Need:* Community strongly supports a smarter compression system that compresses individual tool outputs rather than entire conversation windows. This is a high-value feature for reducing token costs and improving context retention.

2. **[#59224 – Classic CLI /resume hides non-CLI sessions](https://github.com/NousResearch/hermes-agent/issues/59224)**  
   **8 comments**  
   *Need:* Users running Hermes via Desktop app or WebUI cannot see their sessions in the CLI `/resume` listing, breaking cross-platform workflow continuity.

3. **[#39534 – Windows Desktop cuts off Chinese prompts](https://github.com/NousResearch/hermes-agent/issues/39534)**  
   **7 comments**  
   *Pain point:* Critical localization bug where Chinese characters are truncated in the Desktop GUI after a specific version update.

4. **[#58646 – QQ Bot adapter startup failure](https://github.com/NousResearch/hermes-agent/issues/58646)**  
   **7 comments**  
   *Urgency:* QQ adapter completely fails to connect due to an unexpected `is_reconnect` keyword argument – blocks all QQ integration.

5. **[#569 – Agent Client Protocol (ACP) Server Mode](https://github.com/NousResearch/hermes-agent/issues/569)**  
   **2 comments, 9 👍**  
   *Vision:* Long-standing feature request (since March) for running Hermes inside Zed, JetBrains, Neovim via open ACP standard. Strong community support but no recent maintainer response.

### Most Active PRs

1. **[#61002 – Teams: fix authenticated and channel attachments](https://github.com/NousResearch/hermes-agent/pull/61002)**  
   *New PR* – Fixes Microsoft Teams media ingestion, including inline images and RSC all-message delivery.

2. **[#61218 – Add compact matrix/matrix_admin tools](https://github.com/NousResearch/hermes-agent/pull/61218)**  
   *New PR* – Discord-parity tools for Matrix (reactions, history, admin functions).

3. **[#61204 – Strip `required: null` from tool schemas](https://github.com/NousResearch/hermes-agent/pull/61204)**  
   *New PR* – Fixes HTTP 400 errors with strict OpenAI-compatible backends due to invalid JSON Schema.

---

## 5. Bugs & Stability

### P1 (Critical) Bugs Reported Today

| Issue | Description | Status |
|-------|-------------|--------|
| [#61145](https://github.com/NousResearch/hermes-agent/issues/61145) | **Gateway session-hygiene auto-compress DELETEs transcript** instead of soft-archiving (silent data loss) | **Open; fix PR #61209 submitted** |
| [#61087](https://github.com/NousResearch/hermes-agent/issues/61087) | Desktop app does not stop gateway on quit (macOS) | **Closed (fixed)** |

### P2 (High) Bugs Reported Today

| Issue | Description | Fix PR Exists? |
|-------|-------------|----------------|
| [#61207](https://github.com/NousResearch/hermes-agent/issues/61207) | `/plan` command doesn't write a plan file anymore | ❌ No |
| [#61211](https://github.com/NousResearch/hermes-agent/issues/61211) | WeCom file upload fails with FileNotFoundError on Windows (Chinese filenames + MAX_PATH) | ✅ **PR #61214** |
| [#61212](https://github.com/NousResearch/hermes-agent/issues/61212) | Duplicate of #61211 | ❌ (duplicate) |
| [#61220](https://github.com/NousResearch/hermes-agent/issues/61220) | Session expiry finalization doesn't set `end_reason` – stale recovery reopens expired sessions | ❌ No |
| [#61048](https://github.com/NousResearch/hermes-agent/issues/61048) | Kanban worker ignores `fallback_providers` when primary provider is unresponsive | ❌ No |

### P3 (Moderate) Bugs Reported Today

| Issue | Description |
|-------|-------------|
| [#61191](https://github.com/NousResearch/hermes-agent/issues/61191) | Desktop Composer persists stale URL/file attachments across conversations (localStorage cache) |
| [#58619](https://github.com/NousResearch/hermes-agent/issues/58619) | Desktop spawns unbounded serve processes on reconnection – process leak |

### Stability Summary

- **Critical data loss** discovered in gateway session hygiene (P1) – fix already proposed (PR #61209).
- **Windows-specific encoding** bugs continue to plague the WeCom and Desktop platforms.
- Multiple **message delivery** issues across Matrix, QQ, and WeCom platforms suggest gateway connector maturity gaps.
- **Kanban worker** ignoring fallback providers (P2) is a reliability concern for production deployments relying on the cron/kanban system.

---

## 6. Feature Requests & Roadmap Signals

### High-Interest Features (likely in next minor release)

1. **[#39691 – Tool output compression (headroom-ai)](https://github.com/NousResearch/hermes-agent/issues/39691)** – 12 👍, very active. The community strongly wants granular compression instead of whole-context summarization. Likely candidate for v0.19 or v0.18.3.

2. **[#569 – ACP Server Mode](https://github.com/NousResearch/hermes-agent/issues/569)** – 9 👍, but no maintainer engagement since March. This would unlock Hermes in major IDEs (Zed, JetBrains, Neovim). **Risk:** staleness may frustrate community.

3. **[#23524 – Per-cron reasoning effort overrides](https://github.com/NousResearch/hermes-agent/issues/23524)** – Users want fine-grained control over model thinking level per cron job, not just global settings.

4. **[#53617 – Desktop: keep reasoning panel expanded](https://github.com/NousResearch/hermes-agent/issues/53617)** – Simple UX fix for users of thinking models (DeepSeek, etc.) who want to see ongoing reasoning.

5. **[#50718 – Session visibility & unread markers](https://github.com/NousResearch/hermes-agent/issues/50718)** – Desktop UX request for unread cues, needs-input indicators, and OS badges. Indicates Desktop app is becoming a primary interface.

### Speculative Roadmap Direction

Based on today's PR activity, the following areas appear to be in active development:
- **Matrix platform maturity** (#61218, #61206, #61210, #61219) – multiple PRs adding Discord-parity tools and fixing sync/reliability.
- **Profile routing & multi-provider management** (#61205, #54748) – PRs adding in-app routing controls and model routing tiers suggest a strategic push toward enterprise multi-provider setups.
- **Editor/IDE integration** – While ACP (#569) is stalled, the `hermes_cli` fix (PR #61215, #61208) and profile work hint at improved CLI-first workflows.

---

## 7. User Feedback Summary

### Real Pain Points (from issue descriptions & comments)

| Theme | Examples | Frequency |
|-------|----------|-----------|
| **Platform adapter fragility** | QQ bot won't connect (#58646), WeCom file upload fails on Windows (#61211), Matrix decryption breaks (#13891) | **High** – 4+ platform-specific bugs today |
| **Desktop app UX gaps** | Chinese text truncated (#39534), stale attachments stick (#61191), no session visibility cues (#50718), terminal commands truncated (#61193) | **High** – Desktop is a major pain point |
| **Silent failures & data loss** | Session hygiene deletes history (#61145), fallback activation silent (#35419), kanban ignores fallback providers (#61048) | **Critical** – Trust eroding for production use |
| **CLI inconsistency** | `/resume` hides Desktop sessions (#59224), `/plan` stopped working (#61207) | **Moderate** – Workflow breaks for power users |
| **Learning curve** | Feature discovery (#61205 – profile routing), documentation gaps (#39838 – `notification_sources` undocumented) | **Low** but persistent |

### Satisfaction Signals

- ✅ Patch releases land quickly (v0.18.2 same-day fix).
- ✅ Active maintainer responding – multiple PRs submitted by known contributors (nepenth, AlexFucuson9).
- ✅ Community is contributing features (free LLM provider profiles PR #58586, IRC Libera.Chat policy fix PR #61194).

### Dissatisfaction Signals

- ❌ Data loss bug (#61145) is a severe trust issue for users relying on long-running gateway sessions.
- ❌ Chinese language users face recurring encoding issues (#39534, #61211, #61212) – suggests an incomplete i18n testing process.
- ❌ The ACP Server Mode request (#569) has been open for 4+ months with no official response, despite strong community support.

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention (long-unanswered, high-impact)

| Issue | Age | Description | Priority Signal |
|-------|-----|-------------|-----------------|
| [#569](https://github.com/NousResearch/hermes-agent/issues/569) – ACP Server Mode | 4+ months (March 7) | Run Hermes in editors via Agent Client Protocol | **9 👍**, no maintainer response |
| [#5254](https://github.com/NousResearch/hermes-agent/issues/5254) – Tool calls repeating with LM-Studio | 3+ months (April 5) | Fragmented tool calls when using local models (Gemma4) | Still open, no fix PR |
| [#23524](https://github.com/NousResearch/hermes-agent/issues/23524) – Per-cron reasoning overrides | 2 months (May 11) | Cron jobs should support per-job `reasoning_effort` | 2 comments, stale |
| [#39047](https://github.com/NousResearch/hermes-agent/issues/39047) – Gemini model routed to wrong backend | 1+ month (June 4) | Auxiliary compression misroutes Gemini to Codex backend | 3 comments, no resolution |

### PRs Needing Review

| PR | Age | Scope | Risk |
|----|-----|-------|------|
| [#58586](https://github.com/NousResearch/hermes-agent/pull/58586) – Free LLM provider profiles | 4 days (July 5) | Groq/Mistral/Cerebras bundled profiles | Low – additive |
| [#54748](https://github.com/NousResearch/hermes-agent/pull/54748) – Model routing tiers | 10 days (June 29) | Config-driven provider/fallback routing | **High** – core architecture change |
| [#43780](https://github.com/NousResearch/hermes-agent/pull/43780) – Post-curator hook | 29 days (June 10) | Plugin hook after curator runs | **Stale** – needs maintainer attention |

### Summary for Maintainers

- **Critical action needed:** #61145 (data loss) fix PR #61209 should be reviewed and merged urgently.
- **Community trust issue:** #569 (ACP Server) needs at least a status comment after 4+ months of silence.
- **Windows/Chinese encoding bugs** are a recurring pattern – consider adding automated i18n test cases for non-ASCII filenames and rendering.
- **Stale PRs** #43780 (post-curator hook) and #54748 (model routing) are significant features that have gone un-reviewed for weeks, risking community contributor burnout.

---

## Project Health Indicators (Today)

| Metric | Value | Assessment |
|--------|-------|------------|
| Issues updated (24h) | 50 | High activity |
| Open issues | 43 | Stable (not growing too fast) |
| PRs updated (24h) | 50 | Very high development pace |
| Open PRs | 42 | High – good, but review capacity needed |
| P1 bugs | 1 (with fix submitted) | Under control |
| P2 bugs | 5+ (some with fixes) | Moderate concern |
| Community engagement | High (multiple feature requests + contributions) | Healthy |
| **Overall** | **Active, but data loss bug is a critical risk** | **🟡 Yellow – stable with one severe issue** |

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-09

## 1. Today's Overview
PicoClaw shows moderate activity today, with 2 open issues updated and 3 pull requests merged, but no new releases. The project is healthy, with a strong focus on infrastructure reliability (gateway fallback), integration expansion (Grafana Alertmanager channel), and provider completeness (vision support for Anthropic). However, a notable user-reported bug involving OpenAI GPT on the new NanoKVM platform suggests potential friction for edge-device deployments. Overall, maintenance velocity is steady, with community contributions driving channel and agent improvements.

## 2. Releases
No new releases were published. The latest available version remains unchanged; users should monitor the repository for the next tagged release.

## 3. Project Progress
Three pull requests were merged/closed today, all representing meaningful enhancements:

- **PR #2278** — [Gateway reliability] Implemented a fallback from loopback bind to wildcard bind with CIDR allowlist when loopback is unavailable. This improves startup robustness in environments like Docker or restricted networks. *(URL: https://github.com/sipeed/picoclaw/pull/2278)*

- **PR #2251** — [New channel] Added a `grafana_alertmanager` webhook input channel, enabling PicoClaw to receive and process Grafana alerts and trigger skills on alert arrival. This expands PicoClaw's observability integrations. *(URL: https://github.com/sipeed/picoclaw/pull/2251)*

- **PR #3234** — [Anthropic provider fix] Fixed `anthropic_messages` provider to embed image media (e.g., `load_image` outputs) into user messages so vision models (Claude) can actually see attachments. Previously images were silently dropped. *(URL: https://github.com/sipeed/picoclaw/pull/3234)*

## 4. Community Hot Topics
- **Issue #3195** (2 comments) — A user reports that OpenAI GPT fails on NanoKVM with default configuration. The issue has been open since June 30 and is gaining visibility. Underlying need: ensuring out-of-the-box compatibility with Sipeed's own hardware platform is critical for adoption. Link: https://github.com/sipeed/picoclaw/issues/3195

- **Issue #3201** (1 comment) — User requests streaming output support for the QQ channel. Only Telegram and WebSocket currently support real-time token streaming. This reflects a growing expectation for responsive, real-time chat experiences across all channel types. Link: https://github.com/sipeed/picoclaw/issues/3201

## 5. Bugs & Stability
| Severity | Issue | Description | Fix Exists? |
|----------|-------|-------------|-------------|
| High | #3195 | OpenAI GPT non-functional on NanoKVM with default config — full responses fail, potentially blocking core feature on official hardware | No open PR |
| Medium | (Fixed today) #3234 | Anthropic vision models couldn't see attached images (dropped silently) — now fixed by PR #3234 | ✅ Merged today |
| Low | #3201 (feature, not a crash) | QQ channel lacks streaming; users get full response only | No PR |

The NanoKVM bug (#3195) is the most critical open stability issue, as it directly impacts a key hardware integration. No fix PR exists yet.

## 6. Feature Requests & Roadmap Signals
- **Streaming for QQ channel (#3201)** — This aligns with the broader trend of real-time interaction. Expect a PR in the next 2–4 weeks as community interest grows.
- **Grafana Alertmanager channel (PR #2251, merged today)** — Signals growing interest in PicoClaw as an alert routing/agent tool for DevOps/observability stacks.
- **Gateway bind fallback (PR #2278, merged today)** — Indicates maintainers are focusing on edge-case reliability, which often precedes a stable release.

Prediction: The next minor release will likely include the Grafana channel, Anthropic vision fix, and gateway fallback — all merged since the last tag.

## 7. User Feedback Summary
- **Pain point (NanoKVM users)**: Issue #3195 reflects frustration that a highly promoted feature (OpenAI GPT on NanoKVM) fails out-of-the-box. The user specifically followed official docs, indicating a documentation-to-reality gap.
- **Pain point (QQ users)**: The request for streaming (#3201) suggests dissatisfaction with latency for QQ — users want parity with Telegram/WebSocket experiences.
- **Positive signal**: The Grafana webhook PR was authored by an external contributor (loafoe) and merged cleanly, showing the community is invested in extending PicoClaw's integration surface.
- **Configuration complexity**: The NanoKVM bug may stem from model list config issues or protocol mismatches; users need clearer debugging guidance or default presets.

## 8. Backlog Watch
- **Issue #3195** (created 2026-06-30, updated today) — No maintainer response or fix PR. This should be prioritized given it affects first-party hardware. Needs: reproduction by maintainers, configuration validation, or a hotfix. Link: https://github.com/sipeed/picoclaw/issues/3195

- **Issue #3201** (created 2026-07-01, updated today, stale label) — The `[stale]` label suggests it has not been formally prioritized. If QQ channels are important to the user base, this should be moved to an active milestone. Link: https://github.com/sipeed/picoclaw/issues/3201

- **No stale, unmerged PRs of significance** — The three PRs merged today were all handled promptly (one was created and merged the same day). Maintainer response time for PRs appears good.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest
**Date:** 2026-07-09 | **Generated by:** AI Analyst

---

## 1. Today's Overview

NanoClaw is experiencing a high-velocity development cycle today, with **28 pull requests updated in the last 24 hours**—a surge in activity. The project maintains strong momentum with core team members driving multiple feature trains, most notably the **scheduled-tasks initiative** (Part 1/6 and Part 2/5 landed or opened). No new releases were published. Two new issues were opened, and **4 PRs were merged/closed**, indicating steady progress toward trunk. The project health is strong, though the sheer volume of open PRs (24 open) signals a growing queue that may require focused review cycles in the coming days.

---

## 2. Releases

**No new releases in the last 24 hours.**

The last known release appears to be v2.1.17 (with a pending CHANGELOG expansion in PR #2798). No breaking changes or migration notes to report.

---

## 3. Project Progress

**Merged/Closed PRs (4 total):**

- **#2980** – `[CLOSED] ncl CLI: verb-level args, deep help, server-rendered human view` (Part 1/6 of scheduled-tasks train). *Merged.* Introduces strict argument validation, fix-carrying error messages, and server-rendered human views for all `ncl` CLI verbs. [GitHub](https://github.com/nanocoai/nanoclaw/pull/2980)

- **#2978** – `[CLOSED] ci: auto-label PRs from core team members` *Merged.* Adds an author allowlist to the `label-pr.yml` workflow so core-team PRs are automatically tagged. [GitHub](https://github.com/nanocoai/nanoclaw/pull/2978)

- **#1702** – `[CLOSED] fix: break for-await loop on result to prevent IPC message loss` *Closed.* A bug fix for IPC message loss in agent-runner loops, reported in April. [GitHub](https://github.com/nanocoai/nanoclaw/pull/1702)

- **#2981** – `[OPEN, but categorized as part of train] [core-team] Scheduled tasks: ncl tasks control plane, isolated sessions, script gate` *Opened as Part 2/5* — ships `ncl tasks` resource, cancel/pause/resume helpers, per-series isolated sessions, run history, and pre-task script gates. Supersedes #2947. [GitHub](https://github.com/nanocoai/nanoclaw/pull/2981)

**Key Features That Advanced:**
- Scheduled tasks infrastructure (2 of 5 parts now live)
- Per-group harness capability toggles (PR #2983) — cron/scheduling/agent-teams/workflow can be turned off by default
- CLI ergonomics overhaul (deep help, human views)
- Agent template setup wizard with first-agent stamping (PR #2909)
- Structured-skill-format credentials flow for Teams (PR #2958)

---

## 4. Community Hot Topics

**Most Active Issue (by recency, no comments yet):**
- **#2985** – `[OPEN] opencode provider: silent no-reply when the final text snapshot misses session.idle` — Reports a mysterious bug where the agent completes a long turn but delivers nothing to the user. No replies yet, but the silence is concerning. [GitHub](https://github.com/nanocoai/nanoclaw/issues/2985)

**Most Active Feature Request:**
- **#2984** – `[OPEN] feat: auto-rename Discord threads by topic` — User-facing quality-of-life feature for Discord adapter. No comments yet, but addresses a clear pain point for server operators. [GitHub](https://github.com/nanocoai/nanoclaw/issues/2984)

**Longest-Running Open Feature PR:**
- **#2742** – `[OPEN] feat(recipes): the PR Factory` — A published recipe for automated PR review, triage, and testing via Slack threads. 27 days open, still active with core-team label. [GitHub](https://github.com/nanocoai/nanoclaw/pull/2742)

**Underlying Needs Analysis:**
- The silent-no-reply bug (#2985) reveals a reliability gap in the opencode provider—users cannot trust long agentic turns to deliver responses. This could erode trust in production deployments.
- Discord thread auto-rename (#2984) speaks to the growing adoption of NanoClaw on busy Discord servers where discoverability of conversation threads is failing.
- The PR Factory (#2742) represents a demand for self-hosting the entire development workflow within NanoClaw, signaling a shift toward "dogfooding" the platform.

---

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Available? |
|----------|-------|-------------|----------------|
| **Critical** | #2985 | **opencode provider silent no-reply**: Agent completes turn but no message delivered; no error raised. Occurs on long agentic turns when `session.idle` is missing from the final text snapshot. | No PR yet |
| **High** | #2913 (PR) | **WhatsApp Cloud bridge instance key collision**: Bridge registered under generic `whatsapp` key, conflicting with native Baileys adapter. | Fixed by PR #2913 (open, core-team) |
| **Medium** | #2982 (PR) | **Claude tool allowlist drift**: `TOOL_ALLOWLIST` references five tools that don't exist on pinned CLI v2.1.197. | PR #2982 open with drift guard |
| **Medium** | #2878 (PR) | **Codex stale OpenAI secret**: `runCodexAuthStep()` treats any matching OneCLI secret as valid, even if revoked, causing silent failures mid-conversation. | PR #2878 open |

**Notable:** The silent-no-reply bug (#2985) is the highest-priority stability issue today. It has no fix PR yet and zero comments—maintainers should triage urgently. The WhatsApp Cloud fix (#2913) is ready for merge, as is the Codex stale-secret fix (#2878).

---

## 6. Feature Requests & Roadmap Signals

**User-Requested Features (via Issues):**
- **#2984** – Auto-rename Discord threads by topic (host-side `rename_thread` tool) — Low implementation risk, high user impact for Discord operators.

**Feature PRs Likely to Land in Next Release:**
1. **Scheduled tasks control plane** (#2981) — Part 2/5, already opened. Likely to merge quickly given the train approach.
2. **Per-group harness capability toggles** (#2983) — Disabling unused features by default improves stability and security. Clean, well-scoped.
3. **Agent template setup wizard** (#2909) — Part 2 of 2 for the template system. Ready for final review after template loader (#2890) landed.
4. **Instance-wide default agent provider** (#2906) — Simple config change that reduces operator toil.

**Roadmap Signals:**
- The **scheduled-tasks train** (5 parts) is the dominant feature stream. Parts 1 and 2 are now live or open. This suggests NanoClaw is building production-grade job scheduling akin to cron but with agent isolation.
- **Approvals with reject-with-reason** (#2941) is extending to OneCLI credential cards, indicating a push toward enterprise-grade approval workflows.
- The **PR Factory** (#2742) and **structured-skill-format** (#2958) signal a maturation toward modular, deterministic agent skill development.

---

## 7. User Feedback Summary

**Pain Points Reported:**
- **Silent delivery failures** in the opencode provider (#2985): Users cannot trust the agent to deliver answers on long turns—messages appear to be eaten silently. This is a breaking trust issue.
- **Discord thread name chaos** (#2984): Date-stamped thread names like "Thread 7/8/2026, 3:28 PM" make navigation impossible on busy servers.
- **WhatsApp Cloud setup confusion** (#2911, fixed by #2913): Instance key collision caused bridge misconfiguration; users had to debug internal registration conflicts.

**Satisfaction Signals:**
- Continued high engagement from core team members (6 distinct authors in today's PRs).
- The PR Factory (#2742) has been open for nearly a month with sustained activity, suggesting users are invested in the recipe system.
- Community-contributed fix PRs (e.g., #2979 from OowhitecatoO for dependency bump) show an active contributor base beyond the core team.

**Use Cases Evident:**
- **Multi-channel enterprise support** (Discord, WhatsApp, Slack, Teams) is central—users run agents across several chat platforms simultaneously.
- **Self-hosted CI/CD workflows** via the PR Factory recipe—users want NanoClaw to manage its own development process.
- **Scheduled and recurring tasks**—the five-part train signals demand for reliable, agent-driven cron replacements.

---

## 8. Backlog Watch

**Long-Unanswered Important Items Requiring Maintainer Attention:**

| Issue/PR | Age | Status | Concern |
|----------|-----|--------|---------|
| #2742 – PR Factory recipe | 28 days | Open, active | No merge activity; this large feature may need a dedicated review slot |
| #2798 – CHANGELOG expansion for v2.1.17 | 22 days | Open, core-team | Blocking release notes for an already-shipped version |
| #1702 – IPC message loss fix | 92 days (opened April 8) | **Closed today** | Resolved after 3 months; this pattern suggests deep-rooted issues may take too long to fix |
| #2770 – Codex file events + `file` ProviderEvent | 25 days | Open, core-team | Blocks image generation delivery; recent activity suggests it's not abandoned |

**Notable:** The **critical silent-no-reply bug** (#2985) was opened only today (2026-07-08) and has zero comments or assignee—it should be escalated to an on-call maintainer immediately.

**Maintainer Attention Needed:**
- The 24 open PRs represent a growing queue. Core team members (gabi-simons, omri-maya, Koshkoshinsk, glifocat) are the primary contributors—review bandwidth may be a bottleneck.
- The scheduled-tasks train requires careful merge ordering to avoid conflicts (PRs build on each other).

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-09

## 1. Today's Overview

The IronClaw project is in a period of intense active development. Issues and PRs updated in the last 24 hours are high (22 issues, 50 PRs), indicating strong team velocity. Activity is focused on two major fronts: an 8-PR stack (NEA-25) to unify the extension-surface architecture, and a suite of bug-bash P2 and P3 fixes addressing routine failures, UI inconsistencies, and integration errors. The daily failure taxonomy (#5859) reports that LLM provider rate-limiting is saturating benchmark runs, and a routine scheduler bug is causing systemic failures. No new releases were published today.

## 2. Releases

None

## 3. Project Progress

**Merged/closed PRs in the last 24h:** 11 of 50 updated PRs were merged or closed.

**Key advances that landed or are approaching merge:**
- **NEA-25 unified extension surfaces** (7‑PR stack by BenKurrek, PRs #5833–#5850): A comprehensive refactor to eliminate the legacy "kind"-based extension taxonomy. Slack is the validation case — `slack_bot` and `slack_personal` are retired into a single `slack` extension with both inbound/outbound surfaces.
- **Perf: Reduced API capacity pre-model latency** (PR #5857 by serrrfirat): Caches system skill filesystem descriptors to reduce overhead for concurrent API user flows.
- **Private tool/skill installs** (PRs #5525, #5780, #5499 by zetyquickly): SSO users can now privately install tools from the Extension Registry, and admins can install tools via ZIP upload — a direct answer to #5459.
- **WebUI streaming improvements** (PR #5821 by serrrfirat): Assistant text is now streamed through the Reborn/WebUI projection SSE path with live provider-level NEAR AI Chat SSE support.
- **WebUI workspace filesystem scoping** (PR #5831 by serrrfirat): Replaced fixed workspace browser views with caller-scoped mount resolvers for cross-user/cross-project isolation, plus regression tests.

## 4. Community Hot Topics

**Most active issues by comment count and reactions:**

- **#5702** [OPEN, bug_bash_P2] **GitHub issue search/create fails with HTTP 403** — 4 comments, 0 reactions. Users report that the GitHub integration returns "operation_failed" status despite correct configuration. *(Link: [#5702](https://github.com/nearai/ironclaw/issues/5702))*
- **#5705** [OPEN, bug_bash_P3] **Terminal icon has no disable option** — 2 comments, 0 reactions. Persistent UI element with no toggle for users who don't use the terminal. *(Link: [#5705](https://github.com/nearai/ironclaw/issues/5705))*
- **#5557** [OPEN, bug_bash_P3] **Logs deep link requires double click** — 2 comments, 0 reactions. Clicking a Logs link from a routine run opens an empty page on first attempt; second click loads correctly. *(Link: [#5557](https://github.com/nearai/ironclaw/issues/5557))*

**Analysis:** The low-reaction counts suggest these are early bug-bash findings rather than user-community outcries. The GitHub 403 error (#5702) is the highest-priority integration failure — it blocks any user who relies on the GitHub capability. The UI complaints (#5705, #5557) are irritants that erode confidence but are less critical.

**Most active PRs by comment count:** All 20 PRs in the table above had `undefined` comment counts, indicating zero or unreported comments. The PRs with the most developer activity are the NEA-25 stack (#5833–#5850) and the admin-tools/private-installs PRs (#5525, #5780, #5499), each with multiple authors and commit chains.

## 5. Bugs & Stability

**New bugs reported in the last 24h (7 total), ranked by severity:**

**P2 (High severity — blocks core workflows):**
1. **#5837** — Routine run "Open run" / "Logs" buttons are unclickable, preventing failure diagnosis. *(Link: [#5837](https://github.com/nearai/ironclaw/issues/5837))* **No fix PR yet.**
2. **#5838** — Run fails with "context compaction could not complete" after successful tool execution, wasting tool calls. *(Link: [#5838](https://github.com/nearai/ironclaw/issues/5838))* **No fix PR yet.**
3. **#5836** — Every scheduled routine run fails with "No thread attached" — 0% success rate, systemic scheduling issue. *(Link: [#5836](https://github.com/nearai/ironclaw/issues/5836))* **No fix PR yet.**
4. **#5834** — Agent incorrectly refuses to disconnect Slack; integration remains stuck. *(Link: [#5834](https://github.com/nearai/ironclaw/issues/5834))* **No fix PR yet.**

**P3 (Low severity — cosmetic or minor UX):**
5. **#5835** — "Jump to latest" button appears unnecessarily and is positioned too high, overlapping chat content. *(Link: [#5835](https://github.com/nearai/ironclaw/issues/5835))* **No fix PR yet.**
6. **#5820** — WebChat silently drops files beyond the 10-file cap without error message. *(Link: [#5820](https://github.com/nearai/ironclaw/issues/5820))* **No fix PR yet.**

**Aging bugs that remain open:**
- **#5702** (GitHub 403, P2, opened Jul 6) — no fix PR.
- **#5557** (Logs deep link, P3, opened Jul 2) — no fix PR.

**Closed issues (7):** Included #5787 (flaky Slack pairing test — root cause identified: tokio clock vs wall-clock TTL race), #5768 (i18n coverage on Reborn Projects page — completed), #5419 (no rename-automation option — likely closed via a separate fix), #3535 (timestamps bug — closed after verification). #5795 was a placeholder.

**Stability signal:** The daily failure taxonomy (#5859) calls out two major impediments to benchmark trust: 1) LLM provider rate-limiting making nearly every test call fail spuriously, and 2) a harness defect where a single flat token-bucket rate limiter is used across all test users instead of per-user quotas, causing false negatives.

## 6. Feature Requests & Roadmap Signals

**User-requested features visible in today's issues:**

- **#5820** — Raise the WebChat attachment file-count limit and surface overflow errors (instead of silently dropping). This came from real skill workflow usage. Likely a quick fix that could land in the next minor release.
- **#5856** — Admin panel: API-token re-issue for existing users is missing, plus a stale "Create Token" button from the old UI. Follow-up to #5779 (admin user-management). This blocks operational workflows and is likely to be addressed soon.
- **#5828, #5827, #5826** — A cleanup trilogy by italic-jinxin to remove legacy v1 test artifacts (test binaries, fixtures, stale docs). These are housekeeping items that reduce maintenance burden.

**Predictions for next version:**
- The NEA-25 extension-surface unification (PRs #5833–#5850) is an architectural refactor that will land in a single release, likely v0.33 or v0.34.
- Private tool installations (PRs #5525, #5499, #5780) are completing — these will give users and admins the ability to install WASM/skills without admin-only ZIP imports.
- WebUI streaming for assistant text (#5821) is a user-facing improvement that improves perceived responsiveness.

## 7. User Feedback Summary

**Real pain points (from bug-bash issues):**
- **Integration failures:** Users cannot reliably use GitHub issue search/create (HTTP 403) or disconnect Slack — both integrations are in a degraded state.
- **Routine reliability:** Scheduled routines have near-zero success rate (#5836) due to a systematic "No thread attached" bug. The "Open run" and "Logs" buttons being unclickable (#5837) means users cannot even diagnose why routines are failing.
- **UI friction:** The terminal icon is always visible with no disable option (#5705). The "Jump to latest" button overlaps chat content (#5835). Logs deep links require two clicks (#5557). These are small but cumulative irritants.
- **File handling:** Hitting the 10-file cap with silent overflow is a productivity blocker for users who attach multiple screenshots or documents (#5820).

**Satisfaction signals:**
- No user complaints about recent UI improvements (WebUI v2 is not being criticized in today's data).
- The daily failure taxonomy (#5859, #5788) is a sign of the team proactively measuring and reporting quality regressions.

## 8. Backlog Watch

**Issues needing maintainer attention (high signal, low recent activity):**

- **#5419** [CLOSED] No option to rename an automation — closed today, but worth verifying the fix is complete. *(Link: [#5419](https://github.com/nearai/ironclaw/issues/5419))*
- **#4108** [CLOSED] Nightly E2E failed — closed today but was open since May 27 (43 days). The failure was in "Full E2E / E2E (web-regressions)". Ensure the fix that closed this is robust. *(Link: [#4108](https://github.com/nearai/ironclaw/issues/4108))*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the project digest for **LobsterAI**, generated from GitHub activity on **2026-07-09**.

---

### LobsterAI Project Digest — 2026-07-09

### 1. Today's Overview
Project activity is **high**, driven by a significant batch of merged PRs addressing long-standing bugs and feature gaps. The core team closed 10 PRs in the last 24 hours, focusing on fixing a critical data-scoping bug regarding `USER.md` files and improving the subagent collaboration workflow. While no new releases were cut, the rapid closure of these issues signals a push toward a more stable release candidate. Community engagement is focused on two regressions: a boot-loop issue from version 4.1 and a recently introduced bug where agent-specific user profiles are overwritten.

### 2. Releases
**None.** No new releases were published in the last 24 hours.

### 3. Project Progress
Ten pull requests were merged or closed, indicating a strong maintenance and fix cycle.

**Key Advancements:**
- **Subagent Collaboration (PR #2285):** A major feature for delegated subagent collaboration was merged. This allows users to configure which Agents can be delegated to, syncing them as explicit allowlists and materializing delegated runs as child sessions.
- **Permission Prompt UX (PR #2296):** Minimizable permission prompts were added to the Cowork system, improving user flow when agents require confirmation.
- **Bug Fixes:**
    - **Agent `USER.md` Scope (PR #2295):** Fixed a critical bug where editing the "about you" section of one agent silently overwrote the same file in all other agents.
    - **IM Session Scoping (PR #2298):** Fixed IM channel session mappings to respect agent boundaries, preventing cross-agent conversation collisions.
    - **Memory Search (PR #2297):** Fixed a crash that occurred when embedding search was disabled by defaulting to local Full-Text Search (FTS).
    - **Multi-file Attachment (PR #1402) & i18n (PR #1403):** Fixed a bug where only the last file was kept during multi-select, and a missing translation key for "delete".
    - **Scheduled Task Channels (PR #1406):** Fixed a bug where the notification dropdown was empty if no IM platform was toggled on.

### 4. Community Hot Topics
The most active discussions revolve around **data collisions between agents** and a **critical startup failure**.

- **Issue #2293: `USER.md` Overwrite Bug (1 comment, HIGH priority):** This issue reports that modifying the "about you" section in one agent overwrites the same data in all other agents. This is a major privacy/session isolation concern for users running multiple distinct agents. A fix (PR #2295) was merged shortly after the issue was reported, which should resolve this in the next release.
    [GitHub Issue #2293](https://github.com/netease-youdao/LobsterAI/issues/2293)

- **Issue #1400: 4.1 Version Boot Loop (7 comments, CRITICAL):** A user reports that upgrading from version 3.30 to 4.1 causes an infinite restart loop, making the application completely unusable. The user also reports a secondary issue with custom LLM configurations (Qwen3.5-plus) failing due to the web-extractor dependency on web-search. This issue was closed as stale, suggesting the team may be working on a hotfix or considers it a specific environment issue, though the user’s feedback indicates high frustration.
    [GitHub Issue #1400](https://github.com/netease-youdao/LobsterAI/issues/1400)

### 5. Bugs & Stability
Two significant bugs are at the forefront, with one having an immediate fix.

- **HIGH: Agent `USER.md` Confusion (Issue #2293):** Editing an agent's "about you" section propagates changes to all agents. This breaks the fundamental use case of maintaining distinct agent personalities/instructions.
    - **Fix:** PR #2295 (merged) scopes the read/write of `USER.md` to the specific agent workspace.
- **CRITICAL: v4.1 Boot Loop (Issue #1400):** Upgrade from 3.30 to 4.1 results in an infinite restart loop, rendering the software inoperable. This is the most severe bug reported.
    - **Status:** Marked stale. No fix PR is explicitly linked, but the volume of activity suggests it is a known regression.
- **MEDIUM: OpenClaw Memory Search Crash (PR #2297):** The system crashed when embedding search was disabled. Fix merged.
- **LOW: IM Channel List Empty (PR #1406):** Notification dropdown for scheduled tasks was empty when no IM platforms were toggled. Fix merged.

### 6. Feature Requests & Roadmap Signals
- **Subagent Collaboration (PR #2285):** The merge of this feature confirms a roadmap focus on multi-agent orchestration and delegation, allowing complex workflows to be split across specialized agents.
- **Scheduled Task Enhancements (Stale PR #1347):** This open PR proposes adding Cron scheduling, agent selectors, and UX improvements to the scheduled task module. While stale, it represents a high-request feature for power users who want more control over automation.
- **TakoAPI Directory Listing (PR #2294):** A community contributor added a badge for the TakoAPI directory, indicating efforts to increase project discoverability within the AI agent ecosystem.

### 7. User Feedback Summary
- **Pain Point (High):** The v4.1 boot-loop issue (Issue #1400) is causing extreme dissatisfaction, with the user describing the software as "completely paralyzed" and leaving contact info for urgent assistance.
- **Pain Point (Medium):** The `USER.md` bug (Issue #2293) is breaking the user's workflow for managing multiple distinct agents. The user expressed confusion, asking, "I wonder if other users have encountered this problem," indicating a lack of awareness (until now) that it was a bug rather than intended behavior.
- **Satisfaction Signal:** A community contributor (oratis) proactively submitted a PR to list LobsterAI in the TakoAPI directory, suggesting a positive external perception of the project's value.

### 8. Backlog Watch
- **Stale Feature: Skills Management (PR #1346):** This PR has been open since April 2, 2026. It proposes a new "Skills" management feature. While now stale, it represents a significant feature request that has been waiting for maintainer review for over three months.
    [GitHub PR #1346](https://github.com/netease-youdao/LobsterAI/pull/1346)

- **Stale Feature: Scheduled Task Enhancements (PR #1347):** Same age as #1346. Introduces highly requested features (Cron, Agent selection). The backlog on feature reviews appears to be substantial.
    [GitHub PR #1347](https://github.com/netease-youdao/LobsterAI/pull/1347)

- **Stale Bug: Duplicate Scheduled Task Names (Issue #1348):** A low-severity request to add validation preventing duplicate names for scheduled tasks. Has been open since April 2 with no maintainer response.
    [GitHub Issue #1348](https://github.com/netease-youdao/LobsterAI/issues/1348)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

# TinyClaw Project Digest — 2026-07-09

## Today's Overview
Project activity is very low today, with zero new issues and one pull request closed in the last 24 hours. The single PR (#44) was merged after a five-month development cycle, representing a significant security hardening effort. No new releases were published. Overall, the project appears to be in a maintenance period with minimal community engagement.

## Releases
No new releases or version tags were detected. The last release remains unpublished as of this date.

## Project Progress
One pull request was closed/merged in the last 24 hours:
- **#44 [Harden channel auth, file safety, and update integrity]** (closed/merged 2026-07-08) — This PR completes a comprehensive security audit by enforcing sender allowlists across Telegram, Discord, WhatsApp, and queue processing; restricting outbound file handling; and hardening bundle update/install integrity. This is a major architectural improvement that closes multiple security gaps.
  - GitHub: [TinyAGI/tinyagi PR #44](https://github.com/TinyAGI/tinyagi/pull/44)

## Community Hot Topics
No issues or pull requests displayed significant discussion activity (comments: undefined for the only PR). The community has not raised concerns or questions in tracked channels. This could indicate low adoption or that all active discussion happens outside GitHub Issues/PRs.

## Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project appears stable with no open bug reports. The security hardening in PR #44 preemptively addresses potential integrity and authorization vulnerabilities.

## Feature Requests & Roadmap Signals
No user-submitted feature requests were recorded in the last 24 hours. Given the recent security focus, the next likely development steps may involve:
- Expanding platform support (e.g., Slack, Matrix)
- Adding multi-modal capabilities (voice/image processing)
- Improving developer documentation and onboarding
- Building an official plugin/extension marketplace

## User Feedback Summary
No explicit user feedback was captured in the last 24 hours. The absence of issues suggests either high satisfaction or low community engagement. The project may benefit from soliciting user feedback through surveys or community calls.

## Backlog Watch
No long-unanswered issues or pull requests were found in the tracked data. The project backlog appears clean, with the recently merged PR #44 being the only item resolved today. Maintainers may want to proactively open RFCs to gather community input on next priorities.

---
*Overall project health: Stable but quiet. The significant security hardening PR merged today is a positive quality signal, but the lack of community activity warrants monitoring.*

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-09

## Today's Overview
Moltis saw minimal activity in the last 24 hours, with no new issues opened or closed and no new releases published. A single open pull request (#1145) was updated, indicating that contributor attention is focused on a specific stability fix rather than broad feature work. The project appears to be in a low-activity maintenance phase, with developers likely working on longer-running tasks or addressing foundational quality concerns. Overall project health is stable but quiet, with no signs of regression or community distress.

## Releases
No new releases were published today. The latest available release remains the last official version; no migration notes or changelogs to report.

## Project Progress
- **No PRs merged or closed today.**  
  The only PR activity is #1145, which remains open. No features or fixes were officially integrated into the codebase in the last 24 hours.

## Community Hot Topics
- **#1145: `fix(caldav): avoid panic on non-ASCII datetime in normalise_datetime`** — [PR Link](https://github.com/moltis-org/moltis/pull/1145)  
  *Opened and updated on 2026-07-08*  
  This is the only active pull request and the sole item with recent updates. It addresses a panic bug in the CalDAV crate when parsing datetime strings from remote servers that contain non-ASCII digits. The author has proposed a guard that already exists for the DATE branch but is missing for the DATETIME branch. The underlying need here is reliability: users syncing with non-standard CalDAV servers (e.g., those returning localized or malformed date strings) are exposed to crashes. The PR has zero comments or reactions so far, suggesting limited community engagement but clear technical importance.

## Bugs & Stability
- **Critical: Panic on non-ASCII datetime in CalDAV**  
  **Issue:** `normalise_datetime` in `crates/caldav/src/ical.rs` crashes (panics) when a remote CalDAV server returns datetime values containing non-ASCII characters. The DATE branch protects against this with `raw.chars().all(|c| c.is_ascii_digit())`, but the DATETIME branch lacks equivalent validation.  
  **Severity:** High — this is a runtime panic that can break CalDAV sync entirely for affected users.  
  **Fix Status:** A fix is proposed in PR #1145, but it has not yet been reviewed or merged.  
  **Recommendation:** This should be prioritized for merge and release, as it blocks reliable operation with certain CalDAV providers.

No other bugs, crashes, or regressions were reported in the last 24 hours.

## Feature Requests & Roadmap Signals
No new feature requests were filed today. Based on the single active PR, the next version may include:
- Improved robustness in CalDAV datetime parsing, specifically non-ASCII handling.
- No other feature signals detected.

## User Feedback Summary
There is no new user feedback from issues or comments in the last 24 hours. The lack of user-reported issues may indicate that the current feature set is meeting user needs, or that the community is small and quiet. The absence of complaints also suggests no recent regressions from prior releases.

## Backlog Watch
- **PR #1145: CalDAV panic fix** — [PR Link](https://github.com/moltis-org/moltis/pull/1145)  
  *Status:* Open since 2026-07-08, no reviewer activity or maintainer response.  
  **Why it matters:** This fix prevents a crash on standard CalDAV sync operations with non-ASCII servers. If left unattended, users encountering this bug have no workaround. It is a small, focused patch that would benefit from prompt maintainer review and merge.

No other long-unanswered issues or PRs were identified in the current data window.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-09

## 1. Today's Overview

CoPaw shows **high development velocity** with 47 PRs and 38 issues updated in the last 24 hours, alongside a new **v2.0.0-beta.4** release. Activity is concentrated around the `scroll` context compression system, tool-call argument recovery, and security hardening — reflecting a project in active beta stabilization. The 32 open PRs (68%) suggest reviewers are bottlenecked, though 15 PRs were merged or closed today. The community is highly engaged, particularly Chinese-speaking users reporting regressions in v2.0.0-beta.3, with several multi-comment bug threads indicating real-world deployment friction. Maintainer response time to critical bugs appears strong, with most high-severity reports receiving fix PRs within 24 hours.

## 2. Releases

**v2.0.0-beta.4** was released today.

### Changes
- Version bump to `2.0.0b4` (@rayrayraykk)
- `scroll` fix: protect the active turn from eviction, add graduated pressure relief, and make recall failures unmistakable (@niceIrene)

### Breaking Changes
- None documented in this release

### Migration Notes
- No migration steps required; this is a patch-level beta release

## 3. Project Progress

**15 PRs merged/closed today.** Key advances:

### Merged/Closed PRs
- **#5792** (closed) — `fix(agents)`: stop dropping valid self-paired tool messages during sanitation (first-time contributor @Osamaali313)
- **#5864** (closed) — `fix(mcp)`: apply runtime approval level to MCP driver policy, auto-allow `ask` policy (@xiaoming-qxm)
- **#5846** (closed) — `[bug]` v2.00b3: approval popup still appears in "auto-execute mode" — root cause identified and fixed

### Features Advanced
- **#5869** (open, Under Review) — expose system commands (`/new`, `/history`, `/plan`, etc.) in slash autocomplete across Console and TUI (@Jun-yao-hub)
- **#4171** (open, Under Review) — new `memory-distill` tool plugin with title-diffing distillation engine (~92% noise reduction) (@wjt0321)
- **#5187** (open, Under Review) — Windows desktop GUI automation via UIA + Tauri Control Mode, enabling agent-driven desktop interaction (@jinglinpeng)

## 4. Community Hot Topics

### Most Active Issues

1. **#5757** [OPEN] — "[Bug]: 飞书信息不回复情况" (Feishu messages not replying)
   - *12 comments* | Author: @PhillWangdd
   - Root cause: v1.1.12.post2 Feishu channel accepts first message, then silently drops subsequent messages. Related to AgentScope Platform instance behavior.
   - 🔗 [Issue #5757](https://github.com/agentscope-ai/QwenPaw/issues/5757)

2. **#5846** [CLOSED] — "v2.00b3版本,在选择[关闭模式]下仍弹出审批弹窗" (Approval popup still appears in auto-execute mode)
   - *10 comments* | Author: @vipcys001-bot
   - **RESOLVED:** Fix included in beta.4 — critical for unattended automation workflows
   - 🔗 [Issue #5846](https://github.com/agentscope-ai/QwenPaw/issues/5846)

3. **#5171** [CLOSED] — "上下文压缩保留缺少按条数保留或排除人设文件" (Context compression destroys persona files, breaks tasks)
   - *9 comments* | Author: @MCQSJ
   - **RESOLVED:** Systemic issue where context compression zeroes out context when persona file tokens exceed threshold. No retention-by-count option.
   - 🔗 [Issue #5171](https://github.com/agentscope-ai/QwenPaw/issues/5171)

4. **#5860** [OPEN] — "2.0版本频繁出现对话进度丢失和无限循环" (Frequent context loss and infinite loops in v2.0)
   - *3 comments*| Author: @MCQSJ
   - New report: v2.0.0-beta.3 agent loses task context mid-conversation, answers old questions instead of current ones. **High severity** — core reasoning loop defect.
   - 🔗 [Issue #5860](https://github.com/agentscope-ai/QwenPaw/issues/5860)

### Underlying Needs
- **Reliability in unattended mode:** Users running automated workflows (cron, Feishu bots) demand zero-touch operation without silent failures
- **Context stability:** Compounding reports ( #5171, #5746, #5860 ) reveal deep concern about scroll compression corrupting active tasks — the #1 stability pain point
- **Cross-platform parity:** Matrix channel token auth broke after upgrade (#5868), Zalo channel PR (#5801) suggests demand for Southeast Asian messenger support

## 5. Bugs & Stability

### Critical (Active task corruption / Silent data loss)

| ID | Issue | Status | Severity | Fix PR Exists? |
|---|---|---|---|---|
| #5860 | v2.0 context loss + infinite loop (mid-conversation task switch) | **OPEN** | 🔴 HIGH | No |
| #5757 | Feishu channel silently drops messages after first reply | **OPEN** | 🔴 HIGH | No |
| #5846 | Approval popup still shows in "auto-execute" mode (v2.0b3) | **CLOSED** | 🔴 HIGH | Fix in beta.4 ✅ |
| #5868 | Matrix channel token auth fails after upgrade | **OPEN** | 🟠 MEDIUM | No |

### Moderate

| ID | Issue | Status | Severity | Fix PR Exists? |
|---|---|---|---|---|
| #5859 | opencode deepseek model fails when auto_memory_search injects messages without `reasoning_content` | **OPEN** | 🟠 MEDIUM | Workaround: disable auto_memory_search |
| #5863 | Coding session displays binary instead of images for .png/.jpeg files | **OPEN** | 🟠 MEDIUM | No |
| #5841 | PR submitted: recover whitespace-prefixed tool-call JSON arguments | **OPEN** | 🟡 LOW | PR #5841 ✅ |
| #5871 | PR submitted: anchor live turn in scroll eviction index to prevent false eviction | **OPEN** | 🟡 LOW | PR #5871 ✅ |

### Security
- **#5866** (PR, open) — Fix `rm -rf ${HOME}` bypass (#5090) by splitting detection and extraction logic before shlex tokenization
- **#5745** (PR, open) — Redact secrets in persisted dialog artifacts (first-time contributor)

## 6. Feature Requests & Roadmap Signals

### In Development / Under Review (likely v2.1)
- **Agent Team / Swarm Collaboration** (#5139, closed) — User request for native multi-agent team collaboration similar to WorkBuddy and JiuwenSwarm. High community interest (4 comments)
- **Memory Distillation Plugin** (#4171, Under Review) — Title-diffing distillation engine for ~92% noise reduction in daily notes consolidation
- **Computer Use: Windows UIA Automation** (#5187, Under Review) — Desktop GUI driving via UIA + Tauri Control Mode
- **Reranker for Memory Search** (#5692, Under Review) — Post-retrieval reranking stage on top of reme0.4 hybrid retrieval

### Community-Requested (not yet accepted)
- **System tray minimize on close** (#5312, closed) — Desktop app minimizes to tray instead of exiting
- **Task completion notification sounds** (#3302, #5852) — Sound alerts when tasks finish or await approval
- **Multiple command queueing** (#3302) — Queue new instructions while agent is busy
- **Zalo Bot channel** (#5801, open PR) — Vietnam's dominant messenger platform (100M+ users)

### Roadmap Prediction
Given the volume of context-compression bugs, **v2.0.0-beta.5** will likely focus on scroll system hardening — the current beta.4 changes plus #5871 (anchor live turn) and #5848 (handle un-headlined evicted spans). The swarm collaboration feature (#5139) is gaining traction and may appear in v2.1 planning.

## 7. User Feedback Summary

### Pain Points
1. **v2.0 regression:** "Frequent context loss and infinite loops" (@MCQSJ) — multiple users report v2.0 beta is less reliable than v1.x
2. **Silent failures:** Feishu/Matrix channels accept messages then drop them without error (@PhillWangdd, @zero9k)
3. **UI lag:** Console streaming output causes browser stutter until response completes (#5725)
4. **Plugin ecosystem issues:** Python 3.13 incompatibility (`imghdr` removed), packaging scripts broken (#5165, #5166)

### Satisfaction Signals
- Quick maintainer response to #5846 (approval popup regression) — **fixed within hours**
- Multiple first-time contributors submitting quality PRs (#5869, #5792, #5801) indicating a healthy onboarding experience
- Scroll compression system is getting dedicated attention with graduated pressure relief (beta.4) and seam banner anchoring (#5871)

### Use Cases
- **Unattended automation:** Cron agents, Feishu bots (dominant Chinese enterprise scenario)
- **Multi-agent setups:** Team collaboration, knowledge distillation
- **Desktop automation:** Computer-use feature (Windows UIA) for GUI-driven workflows
- **Long-running sessions:** Users leave agents running for hours; stability during extended conversations is critical

## 8. Backlog Watch

### Long-unanswered Issues Needing Maintainer Attention

| ID | Issue | Created | Last Updated | Days Open | Priority Signal |
|---|---|---|---|---|---|
| #5259 | Windows vector index not persisted; "rebuild on startup" must stay enabled | 2026-06-17 | 2026-07-08 | **22 days** | 🟠 4 comments, no maintainer response |
| #5379 | `Internal Server Error` on fresh Python installation | 2026-06-22 | 2026-07-08 | **17 days** | 🟠 8 comments, no fix |
| #5725 | Console streaming causes browser freeze until response completes | 2026-07-02 | 2026-07-08 | **7 days** | 🟡 5 comments, user provided detailed reproduction |
| #5784 | Frontend compression threshold shows wrong provider's value | 2026-07-05 | 2026-07-08 | **3 days** | 🟡 3 comments, root cause already identified in issue |

### Stale PRs Under Review (no update >7 days)

| PR # | Description | Created | Status | Age |
|---|---|---|---|---|
| #4171 | Memory distill plugin | 2026-05-10 | Under Review | **60 days** ⚠️ |
| #5187 | Windows UIA computer-use | 2026-06-14 | Under Review | **25 days** |
| #5692 | Reranker for memory search | 2026-07-01 | Under Review | **8 days** |

### Risk Note
Issue #5259 (Windows vector index persistence) has been open for **22 days** with no maintainer response — a Windows-specific regression that forces all Desktop users to rebuild memory indices on every restart. Combined with #5379 (fresh install crash, 17 days), these represent the longest-unaddressed critical bugs in the backlog.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-09

## Today's Overview

ZeroClaw shows **high development activity** with 50 issues and 50 PRs updated in the last 24 hours. Of these, 10 issues and 16 PRs were closed or merged, indicating a productive cycle of both bug fixing and feature integration. No new releases were published today. The project continues advancing toward its v0.8.3 milestone with major architectural RFCs progressing through community review and implementation, while several high-severity bugs remain under active investigation. The breadth of work spans core runtime stability, channel parity, security hardening, and the long-term WASM plugin infrastructure transition.

---

## Releases

No new releases today. The last published release information was not provided in this data window.

---

## Project Progress

**Merged/Closed PRs Today (16 total):** Notable completions include:

- **#8861** (closed) — `fix(providers): resolve alias credential for model-catalog so native /models is used` — Fixes the model dropdown showing no credentialed provider families (xAI/Grok, Groq, DeepSeek) in ZeroCode/gateway/CLI. *Author: tidux*
- **#8639** (closed) — `feat(zerocode): TodoWrite tracker for ZeroCode (RPC + ACP + durable persistence)` — A major feature implementing a live task tracker in the style of Claude Code/OpenCode, with a `TodoWrite` tool and full RPC/ACP pipeline. *Author: tidux*
- **#8795** (closed) — `fix(web): add Skills nav entry to left sidebar` — Adds the missing navigation link so users can reach the Skills page without typing the URL directly. *Author: xydt-juyaohui*
- **#7690** (closed) — `feat(provider): cover responses-wire option propagation` — Test coverage for non-default constructor and request options in the responses provider. *Author: Audacity88*
- **#7737** (closed) — `bug(channels): carry approval attribution without a global side channel` — Fixes a concurrency bug where concurrent approvals could overwrite side-channel state. *Author: Audacity88*
- **#8334** (closed) — `[Bug]: skills install/list/remove target data_dir, which no multi-agent runtime loads` — Fixes a S2-severity issue breaking the "pull a skill and use it" flow on multi-agent installs. *Author: JordanTheJet*
- **#8553** (closed) — `[Bug]: Agent cannot use environment variables as http_request secrets` — S1 blocker resolved: agents can now use process environment variables for authenticated HTTP requests. *Author: mgstoyanov*

**Features That Advanced:**
- The TodoWrite tracker (#8639) represents a significant UX improvement for ZeroCode users, bringing it closer to parity with Claude Code.
- The provider model-catalog fix (#8861) unblocks users of non-OpenAI API providers (xAI, Groq, DeepSeek) who were unable to select models in the dashboard.
- The web UI Skills navigation fix (#8795) addresses a discovered UX gap immediately after the Skills page was implemented.

---

## Community Hot Topics

**Most active issues (by comment count):**

1. **#5862** (13 comments) — `[Bug]: zeroclaw does not know it can add cron` — User reports the agent doesn't know it can use `zeroclaw cron` to schedule recurring tasks. This suggests a gap in the agent's tool awareness, where it fails to self-reference its own cron capability. *Author: PeterlitsZo*

2. **#6034** (7 comments) — `[Bug]: 单轮对话以及多轮对话会出现丢失 user message的现象` — Chinese-language report of user messages being lost in both single and multi-turn conversations when using a custom API provider. S1 severity (workflow blocked). *Author: lazy-hs*

3. **#8424** (7 comments) — `RFC: .ignore File Mechanism for Workspace File Protection` — Community design proposal for protecting sensitive workspace-internal files from AI agent access, extending beyond the current `forbidden_paths` mechanism. *Author: rakaarwaky*

4. **#6002** (5 comments) — `[Bug]: Not clearly addressed to the assistant` — Telegram channel integration issue where ZeroClaw fails to properly route messages addressed to the assistant, querying llama.cpp incorrectly. S1 severity. *Author: sikc231*

5. **#6672** (5 comments) — `[Bug]: reasoning_content not passed back in agentic tool-call loops with Xiaomi thinking mode` — S0 severity (data loss/security risk): `reasoning_content` from first LLM turn is not forwarded to subsequent turns when using Xiaomi's thinking mode models. *Author: babaksh*

6. **#8226** (5 comments) — `[Feature]: support per-agent custom environment variables configuration` — RFC for introducing `runtime_context` and `runtime_secrets` blocks to resolve identity and token multi-tenancy across process lanes and shared MCP instances. *Author: susyabashti*

7. **#8850** (4 comments) — `Move optional channels & tools from compile-time feature flags to runtime plugins` — A major architectural RFC proposing WASM-based runtime plugins to eliminate recompilation for adding channels/tools. *Author: JordanTheJet*

**Underlying Needs Analysis:** The most active threads reveal three core community concerns:
- **Agent self-awareness** (#5862): Users expect the agent to know about and proactively use its own built-in capabilities (cron, tools). This points to a need for better tool discovery/registration that the agent can introspect.
- **Provider/interop reliability** (#6034, #6002, #6672): Custom API providers and multi-turn scenarios are breaking in interoperable ways, indicating the provider abstraction layer needs hardening.
- **Security & multi-tenancy** (#8424, #8226): As ZeroClaw moves toward multi-agent deployments, workspace file protection and per-agent credential management are emerging as critical design requirements.

---

## Bugs & Stability

**S0 (Data Loss / Security Risk):**
- **#6672** — `reasoning_content not passed back in agentic tool-call loops` — Xiaomi thinking mode models lose reasoning data across turns. *Status: blocked, needs author action.*
- **#8094** — Anthropic provider added in Quickstart is unavailable in chat until reset. *Status: blocked, needs repro.*

**S1 (Workflow Blocked):**
- **#6034** — User messages lost in single/multi-turn conversations with custom API. *Status: accepted, needs author action.*
- **#7527** — macOS app not working (permissions detection fails, empty page, window disappears). *Status: blocked, no known fix PR yet.*
- **#8553** (now closed) — Agent couldn't use environment variables as `http_request` secrets. **Fix merged today via #8553 closure.**
- **#6002** — Telegram messages not clearly addressed to assistant. *Status: accepted.*

**S2 (Degraded Behavior):**
- **#6173** (closed) — `model_switch` tool does not persist across turns. *Fix was in progress.*

**Regression/Stability Fixes in Progress (open PRs):**
- **#8870** — `test(log): flush async writes in emit() so reinit_* tests see them` — Fixes red CI on two `zeroclaw-log` tests. *Author: perlowja*
- **#8867** — `fix(memory): wrap SqliteMemory embedder in Arc + flush before assert in log reinit test` — Fixes CI failure from combined PR interactions. *Author: singlerider*

**UTF-8 Safety:** PR #8873 addresses the recurring byte-limited UTF-8 truncation bug class tracked in #7828, auditing every runtime-reachable truncation path. This is a follow-up to the partial fix in #7455.

---

## Feature Requests & Roadmap Signals

**High-Impact RFCs Under Discussion/Implementation:**

1. **#8850** — `Move optional channels & tools from compile-time feature flags to runtime plugins` — This is the foundational architectural change for WASM plugins. *Author: JordanTheJet. Status: in-progress, accepted. Risk: high.*

2. **#8424** — `.ignore File Mechanism for Workspace File Protection` — Community-driven security enhancement for multi-agent deployments. *Author: rakaarwaky. Status: blocked.*

3. **#8603** — `RFC: OpenAI Chat Completions compatibility adapter` — Would allow OpenAI-compatible clients (Open WebUI, LobeChat) to connect directly to ZeroClaw. *Author: REL-mame. Status: accepted.*

4. **#7497** — `RFC: OCI-Compliant Container Registries as the Plugin Storage and Discovery Mechanism` — Replaces JSON index files with OCI registries for WASM plugin distribution. *Author: bheatwole. Status: blocked.*

5. **#7673** — `RFC: Native context compression as a provider pipeline decorator` — A `CompressionDecorator` to reduce token usage before forwarding requests. *Author: ConYel. Status: blocked.*

6. **#8132** — `RFC: Replace React/Vite web UI build with Rust→Wasm framework` — Eliminates Node.js from the build pipeline using Dioxus/Leptos/Yew. *Author: ConYel. Status: blocked.*

7. **#7543** — `Multi-session support in the gateway web chat UI` — Session sidebar with new/switch/rename/delete. *Author: NiuBlibing. Status: accepted.*

**Predictions for Next Version (v0.8.3 likely):**
- **TodoWrite tracker** (#8639) — Already merged, will ship in next release.
- **Provider model-catalog fix** (#8861) — Already merged, unblocks many provider users.
- **Skills nav fix** (#8795) — Already merged, minor UX improvement.
- **Permission/credential fixes** (#8553, #8334) — Both closed, stabilizing multi-agent workflows.
- **WASM plugin foundation** (#8850, #8863) — Early implementation PRs are stacking; the next release may include basic WASM channel plugin support as experimental.

---

## User Feedback Summary

**Real Pain Points Expressed:**

- **"Agent doesn't know its own capabilities"** (#5862): A user asked ZeroClaw to schedule a recurring task and the agent replied it lacked tools, despite `zeroclaw cron` existing. This indicates a user experience gap where tool registration works technically but the agent cannot introspect its own toolset.

- **"Messages lost in conversation"** (#6034): Chinese-language user reports of complete message loss, blocking their workflow. The error suggests custom API compatibility issues at the protocol level (400 Bad Request).

- **"macOS app doesn't work"** (#7527): A fresh install on macOS 15.7.7 produces a completely non-functional app — permissions not detected, blank page, app window disappears on restart. This is a critical onboarding blocker.

- **"Can't select Anthropic model after adding"** (#8094): The Quickstart flow adds models to the dashboard but they're not available in chat until a full reset — confusing new user experience.

- **"Android Termux setup failure"** (#7911): Precompiled binaries are misidentified as x86_64 Linux instead of aarch64, and compilation also fails. Android users are currently locked out.

- **"Context overflow causes hallucination"** (#6517): Long conversations fill the context window, causing the agent to drift off-topic or hallucinate. This is a fundamental limitation users are hitting in production.

**Satisfaction Signals:**
- The community is actively contributing RFCs and patches (multiple first-time and repeat contributors in today's data).
- The tracker issues (#8071 for v0.8.3, #7831 for Discord parity) show organized community coordination.
- The Skills nav fix (#8795) was reported as a UX gap and fixed the same day — responsive maintainer engagement.

---

## Backlog Watch

**Important Issues Needing Maintainer Attention:**

1. **#5862** (updated 2026-07-08, 13 comments) — `[Bug]: zeroclaw does not know it can add cron` — *Needs repro, blocked, stale candidate.* Despite being the most-commented issue on the board and a clear user-facing gap, it lacks a confirmed reproduction path and maintainer response.

2. **#6517** (updated 2026-07-08, 2 comments) — `[Bug]: Context Overflow Causes Hallucination / Topic Drift` — *Needs repro, stale candidate.* A critical user-reported quality issue with no active resolution path.

3. **#7527** (updated 2026-07-08, 1 comment) — `[Bug]: macos app not work` — S1 severity, macOS 15.7 support, zero maintainer comments. New macOS users are completely blocked.

4. **#7911** (updated 2026-07-08, 2 comments) — `[Support]: Android Termux Setup` — *Blocked, stale candidate.* No resolution for Android users, with the binary distribution issue unaddressed.

5. **#7215** (updated 2026-07-08, 0 maintainer comments) — `fix(quickstart): surface port field for webhook channel config` — Open since June 4 with no maintainer review. Blocks new users from completing webhook channel setup in the FTUE flow. *Author: chengzhichao-xydt*

6. **#8094** (updated 2026-07-08, 1 comment) — `[Bug]: Anthropic provider added in Quickstart is unavailable in chat until reset` — S0 severity (data loss/security risk) with no maintainer visibility.

**Stale PR Needing Review:**
- **#8173** (updated 2026-07-08) — `feat(gateway): in-app upgrade with auto-restart from the web dashboard` — A large feature implementing RFC #8170 end-to-end, with 0 maintainer comments since June 22. Risk: high, size: L, needs maintainer review.

---

*Digest generated from GitHub data for zeroclaw-labs/zeroclaw as of 2026-07-09.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*