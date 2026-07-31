# OpenClaw Ecosystem Digest 2026-07-31

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-31 01:26 UTC

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

Based on the provided GitHub data for OpenClaw (openclaw/openclaw) for 2026-07-31, here is the project digest:

---

## 1. Today's Overview

The OpenClaw project shows a high level of activity, with 500 issues and 500 PRs updated in the last 24 hours. The vast majority of issues remain open (484/500), and the project's maintainers and ClawSweeper bot are actively managing a large, long tail of feature requests and bug reports, many of which have been open for over five months. Notably, there are zero new releases today, and the focus is clearly on stabilizing the codebase through merged fixes and addressing critical reliability and security concerns. The most urgent conversations are around severe memory leaks, session-state corruption, and security boundary issues.

## 2. Releases

None. No new releases were published on 2026-07-31.

## 3. Project Progress

Today's PR activity, while heavily reliant on automated bots, shows progress in several key areas. The community and maintainers are focusing on targeted bug fixes and architectural improvements.

- **Key Merged Fixes & Feature Advancements:**
    - **Session State Reliability:** `fix(session): defer flushPendingToolResults by one event-loop tick` (#97646) aims to fix a race condition causing missing tool results in session history. `feat(session-lock): opt-in diagnostics for embedded session fence takeovers` (#102203) adds observability for session integrity issues.
    - **Provider & Model Handling:** Multiple PRs target provider schema fixes, including `fix(doctor): migrate legacy google provider config to current catalog schema (#102138)` (#102163), `fix(google): repair legacy provider catalog config` (#102170), and `fix(openai): repair stale doctor route pins` (#102180). These address upgrade-path breakages for Google and OpenAI models.
    - **Gateway & Tooling Reliability:** `fix(setup): improve local model onboarding` (#116606) and `fix(google): stop offering unsupported CLI setup` (#116611) improve the setup experience, while `fix(ci): settle custodian mobile layout assertions` (#116613) addresses a CI flake.
    - **Expression and Tool Fixes:** PRs like `fix(security): ignore string-literal contents in code-safety env/exfil rules (#82469)` (#102278) and `fix(edit): preserve original bytes outside fuzzy-match replacement span` (#116600) are aimed at reducing false positives and preserving data integrity.

## 4. Community Hot Topics

The most discussed issues reveal a community deeply concerned with reliability, security, and the core agentic experience (state management, memory, and communication).

- **Critical Session State Loss:** Issue #25592 "Text between tool calls leaks to messaging channels" (38 comments, 🦞 diamond lobster) is the most discussed topic. The community is concerned about internal processing output being shown to users, causing confusion and revealing internal logic.
- **Major Memory Leak:** Issue #91588 "Critical: Gateway Memory Leak" (22 comments, P0, 🐚 platinum hermit) is a top-priority issue causing OOM crashes, indicating significant operational instability for large users.
- **Permanent Channel Suppression:** Issue #115326 "Crash-loop breaker suppresses Discord/WhatsApp permanently" (20 comments, P1) highlights a severe regression where documented recovery methods fail, leaving channels permanently disabled.
- **Config and Bootstrap Frustration:** Issues like #22438 "Tiered bootstrap file loading" (17 comments) and #29387 "Bootstrap files in agentDir are silently ignored" (14 comments, 🦞 diamond lobster) show a strong desire for better multi-agent session management and control over token usage and context.
- **New High-Severity Issue:** Issue #116201 "Realtime voice work can retain unbounded provider and consult state" (7 comments, P1) is a newly reported bug flagged as a `maintainer` concern, indicating potential memory/resource issues in voice sessions.

## 5. Bugs & Stability

Multiple high-severity bugs are actively being triaged, with a strong emphasis on session state, data integrity, and security.

- **P0 (Critical):**
    - #91588 **Critical: Gateway Memory Leak** — RSS grows to 15.5GB causing OOM crashes. No fix PR linked.
    - #48920 **Live Docs are ahead of release** — Documentation references features not in the stable version, causing user confusion and misconfiguration.
- **P1 (High):**
    - #115326 **Crash-loop breaker suppresses Discord/WhatsApp permanently** — Documented recovery fails with WebSocket 1006. This is a blocker for some users.
    - #53540 **Embedded runner "Network connection lost"** — Large tool calls exceed timeouts, breaking sessions.
    - #72015 **active-memory blocks replies and QMD boot initialization can overload gateway** — Reliability issues with the official plugin.
    - #51396 **clearUnboundScopes strips operator scopes unconditionally** — Regression breaking backend clients.
    - #102175, #29387, #99586, #116201 are all high-priority bugs related to security, session state, and runtime stability.
- **Fix PRs in Progress:** There are open PRs attempting to address these, e.g., #97646 for tool-result races, #102173 for hidden pre-tool text, and #116591 for node invoke deadlines, but many remain in review/needs-proof states.

## 6. Feature Requests & Roadmap Signals

The community is calling for more advanced control, governance, and extensibility, signaling a move towards enterprise-grade features.

- **Context and Memory Management:** Issues like #22438 (Tiered bootstrap file loading) and #96675 (Owner-signed responsibility gates) suggest a push for more granular, user-controlled context and memory, with an emphasis on reducing token wastage and increasing trust. These are strong candidates for future versions.
- **Cost Control and Governance:** #42475 "Per-agent cost budget enforcement" (#42475) and #35203 (Token Cost Governance) indicate a need for administrative controls over agent spending.
- **Model and Provider Flexibility:** #114335 (stop model catalog warning loop) and #102180 (repair stale doctor route pins) show an ongoing effort to make provider configuration robust and flexible, especially around local models like Ollama (see #116584).
- **Ecosystem Development:** Issue #50090 "Community Skill Development & ClawHub" (#50090, 15 comments) is a significant, long-running request to grow the ecosystem. The need for more hooks (like `#22358` Post-subagent completion hook) and richer UI integrations (#33413 Slack tool-level progress) will likely drive upcoming features.

## 7. User Feedback Summary

Users are expressing significant frustration around reliability and configuration complexity, but also showing strong enthusiasm for the product's potential.

- **Pain Points:**
    - **Unreliable Messaging Channels:** The leak of internal text (#25592) and permanent channel suppression (#115326) are severe UX issues.
    - **Complex and Silent Configuration Failures:** Issues like silent config drops (#51396), hardcoded paths (#51429), and ignored bootstrap files (#29387) highlight a lack of configurability and confusing troubleshooting.
    - **Safety and Data Integrity:** The report of cron sessions delivering hallucinated output (#49876) and the write tool lacking append mode (#40001, leading to data loss) raise significant trust and safety concerns.
- **Positive Signals:**
    - The enthusiasm for features like Telegram Business support (#20786, 6 👍) and per-agent dreaming (`#67413`, 5 👍) shows users are actively trying to leverage OpenClaw in complex, real-world scenarios.
    - A user requesting `announceTarget` (#27445, 5 👍) highlights a desire for more sophisticated, stateful multi-agent workflows.

## 8. Backlog Watch

Many issues and PRs have been stagnant for months, awaiting maintainer review or product decisions, creating a potential bottleneck.

- **Long-Open Issues (Created Feb-Mar 2026, still open with strong ratings):**
    - #25592 (Feb 24) **Text between tool calls leaks** — Top comment count, still no firm fix.
    - #22438 (Feb 21) **Tiered bootstrap file loading** — High-value feature request persisting for 5 months.
    - #29387 (Feb 28) **Bootstrap files in agentDir silently ignored** — A critical bug, still open.
    - #41744 (Mar 10) **Feishu: read image tool result loses media** — Data loss bug, still open.
    - #51396 (Mar 21) **clearUnboundScopes strips operator scopes** — Security regression, still open.
- **PRs Awaiting Maintainer Action:** Many PRs with the status `👀 ready for maintainer look` (e.g., #102180, #102278, #102204) have been sitting for weeks. The `clawsweeper:no-new-fix-pr` label on these issues indicates the bot has not generated a fix, leaving the ball in the maintainers' court. These require triage and a product decision to progress.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-07-31

---

## 1. Ecosystem Overview

The open-source personal AI assistant landscape is in a **rapid maturation phase**, characterized by intense stabilization efforts across all major projects. The ecosystem is converging on several core priorities: **session-state reliability, multi-channel message integrity, security hardening, and provider interoperability**. Projects are transitioning from feature-velocity mode to production-hardening mode, with notable investments in memory isolation, subprocess security, and cross-channel consistency. The community is actively demanding enterprise-grade features—cost governance, multi-tenant isolation, audit trails, and OpenAI-compatible APIs—while maintaining a strong ethos of local-first, privacy-preserving operation. Competition is intensifying as projects differentiate on architectural philosophy (monolithic vs. microservice), target user base (developer-centric vs. consumer-facing), and deployment footprint (full-desktop vs. lightweight-edge).

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Merged/Closed (24h) | Release Status | Health Score |
|---------|-------------|-----------|---------------------|----------------|--------------|
| **OpenClaw** | 500 updated (484 open) | 500 updated | ~15 merged | None | ⭐⭐⭐⭐ (High activity, but backlog-heavy) |
| **NanoBot** | 7 updated (5 open) | 50 updated | 33 merged | None | ⭐⭐⭐⭐⭐ (High throughput, clean pipeline) |
| **Hermes Agent** | 50 updated (50 open) | 50 updated | 3 merged | **v0.19.1** (2026-07-30) | ⭐⭐⭐⭐ (Release cadence, active triage) |
| **PicoClaw** | 7 updated | 17 updated | 5 merged | None | ⭐⭐⭐⭐ (Stable, steady development) |
| **NanoClaw** | — | 19 updated | 7 merged | None | ⭐⭐⭐⭐ (Intense hardening, but community PRs stall) |
| **NullClaw** | — | — | — | — | ⭐ (Inactive) |
| **IronClaw** | 40 updated | 29 open | 3 merged | None (release PR pending 28d) | ⭐⭐⭐⭐ (High architecture investment, UX gaps) |
| **LobsterAI** | 0 new | 10 updated | 7 merged | **2026.7.29** | ⭐⭐⭐⭐⭐ (Healthy, consumer-focused) |
| **TinyClaw** | — | — | — | — | ⭐ (Inactive) |
| **Moltis** | 2 new | 4 updated | 1 merged | None | ⭐⭐⭐⭐ (Lean, responsive, security-aware) |
| **CoPaw** | 25 updated | 50 updated | 26 merged | None (v2.0.1 latest) | ⭐⭐⭐⭐ (High momentum, critical bugs) |
| **ZeptoClaw** | 0 | 1 open | 0 | None | ⭐⭐⭐ (Quiet, maintenance-focused) |
| **ZeroClaw** | 15 open | 50 open | 0 | None | ⭐⭐⭐ (Consolidation phase, security focus) |

---

## 3. OpenClaw's Position

### Advantages vs. Peers
- **Community scale:** With 500 issues/PRs updated in 24h, OpenClaw has the largest community in the ecosystem—an order of magnitude beyond competitors (CoPaw, Hermes at ~50 each).
- **Ecosystem gravity:** The volume of community-contributed feature requests, plugin ideas (ClawHub), and multi-agent workflows demonstrates a self-sustaining innovation engine.
- **Bot-assisted maintenance:** ClawSweeper bot automation enables triage at a scale no other project approaches, keeping the backlog moving despite its size.
- **Feature depth:** Micro-optimizations (session locking, provider schema repair, token cost governance) show sophisticated, long-tail development rarely seen in peers.

### Technical Approach Differences
- **Modular gateway/monolith architecture:** OpenClaw emphasizes a unified gateway pattern with fine-grained session control, while peers like NanoBot favor microservice isolation and CoPaw favors an integrated desktop-plus-cloud model.
- **State management sophistication:** The `session-lock` diagnostics and `flushPendingToolResults` race fixes demonstrate a deep architectural investment in deterministic state management.

### Community Size Comparison
| Project | Scale Indicator |
|---------|----------------|
| **OpenClaw** | 500+ issues/PRs daily |
| **CoPaw** | 50 PRs, 25 issues daily |
| **Hermes Agent** | 50 issues, 50 PRs daily |
| **NanoBot** | 50 PRs, 7 issues daily |
| **ZeroClaw** | 15 issues, 50 PRs daily |
| **Others** | <10 daily |

**OpenClaw's community size is ~10x the nearest competitor**, creating both a strength (innovation diversity) and a weakness (maintainer bottleneck—484 open issues).

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|------------|----------|----------------|
| **Session-State Reliability** | OpenClaw, NanoBot, Hermes, CoPaw, IronClaw | Race conditions, state corruption, session-store pollution, background-run isolation |
| **Channel Message Integrity** | OpenClaw, NanoBot, Hermes, PicoClaw, ZeroClaw | Long-message handling (IRC), audio/video support (WhatsApp), reaction/edit fixes, cross-channel consistency |
| **Memory Isolation & Multi-Tenant Security** | IronClaw, Hermes, LobsterAI, Moltis | Cross-user memory leakage, profile isolation, per-account scoping, vault auth bypass |
| **Subprocess Security** | OpenClaw, ZeptoClaw, Hermes, CoPaw | Environment variable leakage, shell command output truncation, sandbox cleanup |
| **Provider Interoperability** | OpenClaw, NanoBot, CoPaw, ZeroClaw, PicoClaw | Model catalog fixes, OpenAI-compatible APIs, custom gateways, multi-provider fallback chains |
| **Cost Governance** | OpenClaw, Hermes, CoPaw | Per-agent budgets, token estimation accuracy, cost-aware routing |
| **Observability & Instrumentation** | Moltis, NanoClaw, IronClaw, OpenClaw | OTel export, conversation correlation, token/reasoning traceability |
| **MCP Server OAuth Support** | PicoClaw, OpenClaw, CoPaw | OAuth 2.1+PKCE for MCP servers, non-technical user onboarding |

---

## 5. Differentiation Analysis

| Project | Architecture Philosophy | Target User | Unique Differentiation |
|---------|------------------------|-------------|------------------------|
| **OpenClaw** | Monolithic gateway with micro-agent sessions | Power users, flexibility-focused | Largest ecosystem, ClawHub, session-locking sophistication, deep provider repair |
| **NanoBot** | Microservice-oriented, clean PR pipeline | Developers, channel-heavy users | SQLite migration, Responses API reasoning-state preservation, extremely clean CI |
| **Hermes Agent** | Enterprise-ready, multi-profile desktop+cloud | Enterprises, cross-platform teams | Native desktop apps (Windows/macOS), profile isolation, skill self-improvement loop, active release train |
| **PicoClaw** | Lightweight multi-channel gateway | IRC/DingTalk/DeltaChat/WeChat communities | Unusual channel breadth, Bedrock prompt caching, process hook flexibility |
| **NanoClaw** | Container-native, delegated runner architecture | DevOps/self-hosting enthusiasts | Image signing/attestation, opencode compatibility, hardened supply chain |
| **IronClaw** | Target-crate architecture (modular refactor) | Near/AI ecosystem, security-conscious | Skill reliability epics, error-recoverability contract, multi-user isolation focus |
| **LobsterAI** | Consumer desktop app, productivity-plugin | Consumer desktop users | Cowork side-chat, daily check-in gamification, polished Windows/macOS UX, NetEase/Youdao backing |
| **Moltis** | Minimalist multi-channel, security-forward | Early adopters, small teams | Privileged-tool operator gating, per-account operator lists, lean footprint |
| **CoPaw** | Full-featured desktop+cloud, AgentScope integration | Power users, AgentScope platform users | Native GUI automation (computer-use), Creator plugin, mission mode, aggressive community onboarding |
| **ZeptoClaw** | Lightweight, minimal dependencies | Developers, edge devices | Subprocess secrets scrubbing, process-tree reaping, ultra-low footprint |
| **ZeroClaw** | Rust-based, RPC-focused | Rust ecosystem, performance-critical | Rust performance + memory safety, OpenAI-compatible endpoint RFC, Gemini Live realtime channel |

---

## 6. Community Momentum & Maturity

### Tier 1: Rapid Iteration (high velocity)
| Project | Signal |
|---------|--------|
| **OpenClaw** | Massive daily activity, constant bot-assisted triage, deep feature long-tail |
| **CoPaw** | 26 merges in 24h, active first-time contributors, responsive maintainers |
| **NanoBot** | 33 merges in 24h, clean CI pipeline, SQLite migration momentum |

### Tier 2: Steady Development (consistent, focused)
| Project | Signal |
|---------|--------|
| **Hermes Agent** | Weekly release cadence, enterprise feature alignment, moderate community engagement |
| **LobsterAI** | High merge rate, consumer UX polish, no issue backlog—very healthy |
| **Moltis** | Lean and responsive, fast security-response culture |
| **PicoClaw** | Steady multi-channel development, multiple feature PRs in flight |

### Tier 3: Consolidation Phase (refining, not shipping)
| Project | Signal |
|---------|--------|
| **IronClaw** | Heavy architecture investment, user-facing UX gaps, release train pending |
| **ZeroClaw** | Zero merges in 24h, RFC-crunching phase, security hardening focus |
| **NanoClaw** | Internal hardening priority, community PRs stalled 2-4 months |

### Tier 4: Maintenance Mode / Inactive
| Project | Signal |
|---------|--------|
| **ZeptoClaw** | 1 open PR, no community activity, maintenance-lite |
| **NullClaw / TinyClaw** | No activity in 24h | 

**Momentum verdict:** OpenClaw, CoPaw, and NanoBot are racing forward; Hermes and LobsterAI are shipping steadily; IronClaw and ZeroClaw need to balance architecture with user-facing fixes before launch windows close.

---

## 7. Trend Signals

1. **Deterministic agent behavior is the new frontier.** The error-recoverability epic (IronClaw), tool-loop fixes (NanoBot, OpenClaw), and session-state guarantees (OpenClaw, Hermes) all point to developers demanding agents that fail predictably and recover autonomously.

2. **Security is becoming non-negotiable.** Cross-user memory leak (IronClaw), vault auth bypass (Moltis), webhook authentication (ZeroClaw), subprocess secret scrubbing (ZeptoClaw) — every major project has at least one security-critical finding. Expect security audits to become part of release gates.

3. **MCP OAuth 2.x is a hidden bottleneck.** PicoClaw and OpenClaw receive duplicate requests for non-technical MCP setup. This is table-stakes for enterprise SaaS integrations.

4. **OpenAI-compatible endpoints are the interoperability lingua franca.** ZeroClaw's RFC (and similar asks across NanoBot, CoPaw) signals that every agent tool needs to speak the OpenAI protocol to plug into existing ecosystems (Open WebUI, LobeChat).

5. **Memory architecture is being disaggregated.** The conversation-history vs. long-term-memory separation debate (ZeroClaw #9048, Hermes #31584) shows memory is becoming a first-class, swappable component rather than a hidden system.

6. **Channel completeness is a moat.** WhatsApp audio, IRC long-message, Telegram inline buttons, Slack Block Kit — every channel needs identical fidelity. Projects that fail here (NanoBot, OpenClaw, Hermes all have channel bugs) will lose daily-active users to more consistent alternatives.

7. **Cost governance is climbing the priority ladder.** Per-agent budgets (OpenClaw #42475), token estimator accuracy (Hermes #75102), cost-aware routing (PicoClaw fallback chains) — the community cares about money and wants transparent controls.

8. **Agent self-improvement needs guardrails.** Hermes #72269 (failed tasks encoded as validated skills) is a warning: autonomous skill-learning systems require confidence thresholds and human-in-the-loop verification.

9. **Local-first is still a differentiator.** Termux timezone support (NanoBot), compact `local_small` runtime profiles (ZeroClaw #5287), Ollama onboarding (OpenClaw #116584) — edge-device and local-model compatibility win user trust in privacy-sensitive contexts.

10. **Multi-tenancy isolation is immature.** Cross-user memory leaks (IronClaw), profile .env pollution (Hermes), account-state leakage (LobsterAI) — all projects need to harden multi-account isolation as enterprise adoption grows.

---

*Report generated from public GitHub community digest data, 2026-07-31.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-31

## 1. Today's Overview

NanoBot is in a highly active development phase, with 50 PRs updated in the last 24 hours (33 merged/closed, 17 open) and 7 issues updated (5 open, 2 closed). There are no new releases today, but the maintainers are pushing a substantial stabilization effort—multiple merged PRs target regressions in session locks, exec buffer bounds, CI speed, and pairing reliability. The project also shows major architectural momentum, with a significant merge that adopts OpenAI's Responses API reasoning-state preservation, plus an open PR to migrate session storage from JSONL to SQLite. However, seven open bugs—including a silent Telegram polling stall and a WhatsApp audio failure—indicate that reliability across channels remains the top concern. No new features were released, and the project is squarely in a "fix and harden" phase.

## 2. Releases

No new NanoBot releases were published in the last 24 hours. The most recent release was prior to this digest window. Users on older versions may want to track the `main` branch, as several critical bug fixes (noted below) have landed since the last tag.

## 3. Project Progress

The 33 merged/closed PRs today represent a significant round of fixes and improvements, centered on reliability and provider compatibility:

- **[`finish_reason='length'` recovery (#5136)](https://github.com/HKUDS/nanobot/pull/5136)** — Closes a tricky bug where blank content in long tool-call responses was misrouted to generic retries instead of length recovery.
- **[Responses API reasoning state (#5172)](https://github.com/HKUDS/nanobot/pull/5172)** — Merged support for preserving OpenAI's opaque Responses output-item chain (encrypted reasoning) and compacting context. A notable provider-level advancement.
- **[CI stabilization (#5145)](https://github.com/HKUDS/nanobot/pull/5145)** — Reworks a flaky timeout test and batches dependency installs for faster, more reliable pipelines.
- **[Session lock lifecycle fixes (#5151)](https://github.com/HKUDS/nanobot/pull/5151)** — Releases idle session locks to avoid unbounded memory growth.
- **[Bounded exec output (#5150)](https://github.com/HKUDS/nanobot/pull/5150)** — Adds fixed head/tail budget for buffered stdout/stderr, preventing OOM on verbose subprocess output.
- **[Pairing resilience (#5147)](https://github.com/HKUDS/nanobot/pull/5147)** — Ensures transient `pairing.json` read failures don't wipe approved user lists.

Open PRs to watch include the **SQLite session migration (#5173)**, **Quick Chat WebUI (#5184)**, and **Termux timezone support (#5189)**.

## 4. Community Hot Topics

- **[Issue #5149: "no audio?" (WhatsApp)](https://github.com/HKUDS/nanobot/issues/5149)** — 3 comments. A user reports that NanoBot can receive but cannot send audio files on WhatsApp. The most-commented issue today suggests channel-specific media handling gaps.
- **[Issue #5185: "Nanobot returning tool calls code in responses"](https://github.com/HKUDS/nanobot/issues/5185)** — 1 comment. A sudden regression where tool-call code appears in user-facing responses. This is a high-impact usability issue that may be related to recent provider changes.
- **[Issue #4791: DoS via missing channel rate limiting](https://github.com/HKUDS/nanobot/issues/4791)** — 1 comment; now closed. After 24 days, this security-relevant issue was closed, though no specific fix PR is visible today.

The main underlying needs here are: smooth multimedia handling, trust in model output integrity, and hardening against abuse.

## 5. Bugs & Stability

Ranked by severity:

1. **[Silent Telegram polling stall (#5171)](https://github.com/HKUDS/nanobot/issues/5171)** — Critical: Bot stops receiving messages indefinitely after network blips, with no log output. A targeted fix is being worked on in [PR #5156](https://github.com/HKUDS/nanobot/pull/5156) (open, in review).
2. **[Tool-call code leak in responses (#5185)](https://github.com/HKUDS/nanobot/issues/5185)** — High user impact; unclear root cause (no reproduction steps yet). No fix PR posted as of this digest.
3. **[Termux incompatibility (#5187)](https://github.com/HKUDS/nanobot/issues/5187)** — App fails to start on minimal Linux hosts due to missing timezone data. Open [PR #5189](https://github.com/HKUDS/nanobot/pull/5189) adds `tzdata` fallback; likely to merge soon.
4. **[No WhatsApp audio output (#5149)](https://github.com/HKUDS/nanobot/issues/5149)** — Medium severity channel bug with logs indicating ffmpeg warnings.
5. **[Generic completion loops for GPT on cron tasks (#3106)](https://github.com/HKUDS/nanobot/issues/3106)** — Reported months ago, still open.

## 6. Feature Requests & Roadmap Signals

The open PRs reveal strong signals for upcoming features:

- **SQLite-backed session storage (#5173)** — A major internal shift toward transactional persistence, with JSONL kept only as an import/backup format. Expect a faster and more robust web UI.
- **Quick Chat & Temporary Chat (#5181, #5184)** — WebUI improvements for persistent quick conversations and purely in-memory context. Good UX signals.
- **Custom Bot API gateways for Telegram (#4919)** — Self-hosting and enterprise use-case expansion.
- **Subagent model presets (#4291)** — Power users will be able to assign distinct LLMs to subagents via `spawn`.
- **`isolated_session` config for heartbeat (#4551)** — Fixes shared-session collisions.

Prediction: The three `p1`-priority fixes (Termux timezone, cron state preservation, agent `length` recovery) are likely to be merged within days. The SQLite migration could land in the next major version if the maintainers push through the risk of the JSONL import path.

## 7. User Feedback Summary

- **Reliability anxiety**: Users are hitting chained failures—silent stalls, timeout loops, lost approvals—which erodes trust despite the project's fast iteration.
- **Channel completeness**: WhatsApp audio and Telegram polling gaps are concrete complaints from daily users.
- **Model/provider sensitivity**: Users report varying behavior (e.g., GPT vs. GLM on cron tasks), suggesting that provider abstraction still leaks model-specific quirks.
- **Environment limitations**: Termux use-case highlights demand for running NanoBot on limited devices/off-the-shelf hardware.

## 8. Backlog Watch

These issues have been open for a while and deserve attention:

- **[Issue #3106: GPT tool-loop on scheduled tasks](https://github.com/HKUDS/nanobot/issues/3106)** — Open since April, no linked PR. Likely a provider heuristics problem; arguably a candidate for a `p0` regression fix.
- **[PR #4819: WeakValueDictionary race in consolidation locks](https://github.com/HKUDS/nanobot/pull/4819)** — Open since July 6, tagged `conflict`, no maintainer response visible. Suggest manual review or close/refresh.
- **[PR #4551: isolated_session for heartbeat](https://github.com/HKUDS/nanobot/pull/4551)** — Open since June 26, tagged `conflict`, not yet updated. A valid feature with no maintainer reply.
- **[Issue #4791: DoS risk via message floods](https://github.com/HKUDS/nanobot/issues/4791)** — Marked closed today, but the original fix plan was not merged in this digest. If you rely on rate limiting, verify the closing commit actually provides protection.

---

*Data window: 2026-07-30 to 2026-07-31. Digest compiled from public GitHub project activity.*


</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-31

## 1. Today's Overview

Hermes Agent is showing **extremely high activity** today, with 50 issues and 50 PRs updated in the last 24 hours. The project just cut its first stable patch release since v0.19.0, rolling up ~1,000+ PRs into **v0.19.1 (v2026.7.30)** for downstream consumers. The community is highly engaged: 10 issues and 5 PRs were created today, with several high-priority (P1/P2) bugs reported from real-world deployments. A notable cluster of activity centers on **session-state hygiene** — background agent runs polluting user-visible session lists, pin-sync races, and profile isolation issues across desktop/gateway boundaries. Security also features prominently, with a PR fixing cloud API key leakage to config-overridden private URLs and another patching vulnerable dependencies. The project shows a healthy balance of community bug reports, maintainer-driven fixes, and active feature development.

---

## 2. Releases

### v2026.7.30 — Hermes Agent v0.19.1 (patch)

**Release Date:** July 30, 2026

**Type:** Patch release — rolls up ~1,000+ PRs merged since v0.19.0 into a stable tagged release for Docker images, hosted deployments, and fresh installs.

**Details:**
- No breaking changes expected; this is a stabilization rollup.
- No migration notes provided beyond standard patch-upgrade guidance.
- Signals the project is keeping a **regular release cadence** (weekly/monthly tagged releases) for enterprise/downstream consumers.

---

## 3. Project Progress

**Merged/Closed PRs today: 3**

- **[#75105 — fix(mcp): recover cached server after terminal OAuth startup failure](https://github.com/NousResearch/hermes-agent/pull/75105)** *(merged)* — Fixes a stale MCP server cache after terminal OAuth failures by evicting dead lifecycle entries and allowing fresh discovery. Tagged `sweeper:implemented-on-main`, meaning the fix is live.

- **[#75113 — Retracted](https://github.com/NousResearch/hermes-agent/pull/75113)** *(closed)* — Windows platform fix retracted by author.

- **[#75037 — fix(sec): patch vulnerable deps + add publication-age floors and npm script allow-list](https://github.com/NousResearch/hermes-agent/pull/75037)** *(closed/merged area)* — Large supply-chain sweep: bumped Python deps (`Pillow`, `mcp`, `pygments`, `pynacl` and more) to fixed versions, and added structural guardrails (publication-age floors for new dependencies, npm script allow-listing) to prevent repeat drift.

**Other high-signal PRs still open (notable progress):**

- **[#75110 — fix(desktop): preserve URLs in Markdown code](https://github.com/NousResearch/hermes-agent/pull/75110)** — Prevents desktop composer from converting URLs inside code blocks into `@url:` chips.
- **[#75102 — fix(agent): stop double-counting api_content in token estimator](https://github.com/NousResearch/hermes-agent/pull/75102)** — Cost-accuracy fix: `api_content` is a substitute for `content`, not additive; affects usage metrics and potentially billing.
- **[#75112 — fix(desktop): adopt saved primary profile before gateway boot](https://github.com/NousResearch/hermes-agent/pull/75112)** — Fixes cold-boot race where the renderer connects the gateway before reading the persisted profile, breaking profile isolation.
- **[#75101 — fix(cron): route execution ledger to the active profile home](https://github.com/NousResearch/hermes-agent/pull/75101)** — Fixes cron execution DB ignoring `multiplex_profiles` scoping.
- **[#75103 — fix(kanban): throttle repeated same-reason respawn_guarded events](https://github.com/NousResearch/hermes-agent/pull/75103)** — Stops event-log spam (~1/min per tick) for cards held by persistent guards (e.g., `active_pr`).

---

## 4. Community Hot Topics

The most active threads reveal a community deeply concerned with **session-state reliability, cross-platform stability, and agent autonomy safety**.

1. **[#31584 — Memory-context as background not authoritative (10 comments)](https://github.com/NousResearch/hermes-agent/issues/31584)** — Long-running debate (since May) on whether memory-context should be treated as system context rather than user message content. Linked to prompt-injection threat surfaces. *High value for all users, unresolved for 2+ months.*

2. **[#37968 — Cron: isolate gateway approvals from environment pollution (8 comments)](https://github.com/NousResearch/hermes-agent/issues/37968)** — CVSS 7.0 (High) security issue: cron-scheduled jobs inheriting polluted environment variables in gateway approval flows. Needs a maintainer decision (`needs-decision` label).

3. **[#74942 — Desktop updater false-positive "another instance" (5 comments, 2 👍)](https://github.com/NousResearch/hermes-agent/issues/74942)** — **P1 bug**: updater detects its own PID as another instance, blocking updates. Impacts all Windows desktop users. Reported just yesterday; high urgency.

4. **[#67347 — Guided picker for Subagent Model/Provider (5 comments)](https://github.com/NousResearch/hermes-agent/issues/67347)** — Users find bare free-text fields for `delegation.model`/`provider` confusing; want a guided picker in Desktop + Dashboard. UX improvement signal.

5. **[#72269 — Review writes failures up as validated skills (4 comments)](https://github.com/NousResearch/hermes-agent/issues/72269)** — Self-improvement loop can encode failed tasks as "confident skills." *Safety concern for autonomous agents*; flagging priority P2.

6. **[#33485 — Honcho hybrid memory SIGABRT on CLI shutdown (4 comments)](https://github.com/NousResearch/hermes-agent/issues/33485)** — Intermittent CPython abort (exit 134) during teardown; same class as #43186. Impacts Mac/Linux users with hybrid memory enabled.

**Most-reacted:** P1 desktop updater issue (2 👍) and the Web TUI blank-space issue [#53413](https://github.com/NousResearch/hermes-agent/issues/53413) (1 👍).

---

## 5. Bugs & Stability

Ranked by severity (P1 = critical/blocking, P2 = high, P3 = normal):

| Severity | Issue | Description | Status |
|----------|-------|-------------|--------|
| **P1** | [#74942](https://github.com/NousResearch/hermes-agent/issues/74942) | Desktop updater false-positive PID check — blocks updates on Windows | No fix PR yet |
| **P2** | [#62935](https://github.com/NousResearch/hermes-agent/issues/62935) | `microsoft-teams-apps` import side-effect loads foreign `.env` — breaks profile secret isolation | Needs decision |
| **P2** | [#62401](https://github.com/NousResearch/hermes-agent/issues/62401) | Matrix gateway on macOS arm64 blocked — unneeded `python-olm` build (E2EE off) | No fix PR |
| **P2** | [#45563](https://github.com/NousResearch/hermes-agent/issues/45563) | `patch`/`write_file` silently refuses config edits instead of routing to approvals | No fix PR |
| **P2** | [#31987](https://github.com/NousResearch/hermes-agent/issues/31987) | MCP HTTP transport anyio RuntimeError → reconnect failure loop | No fix PR |
| **P2** | [#32827](https://github.com/NousResearch/hermes-agent/issues/32827) | `same_tool_failure_warning` doesn't auto-block → unbounded retry-loop cost | No fix PR |
| **P2** | [#51944](https://github.com/NousResearch/hermes-agent/issues/51944) | Invalid tool name `multi_tool_use.parallel` → persistent fallback to secondary model | No fix PR |
| **P2** | [#53413](https://github.com/NousResearch/hermes-agent/issues/53413) | Web TUI Dashboard blank whitespace after long conversations | No fix PR |
| **P3** | [#74570](https://github.com/NousResearch/hermes-agent/issues/74570) | Desktop pin/unpin reverted by `pullRemotePins` race | No fix PR |
| **P3** | [#33485](https://github.com/NousResearch/hermes-agent/issues/33485) | Honcho hybrid memory SIGABRT (exit 134) on CLI shutdown | No fix PR |
| **P3** | [#43186](https://github.com/NousResearch/hermes-agent/issues/43186) | Concurrent `hermes chat -q` subprocesses → SIGABRT on exit | No fix PR |
| **P3** | [#41805](https://github.com/NousResearch/hermes-agent/issues/41805) | Kanban hard usage-limit failures → dispatcher re-spawns indefinitely | No fix PR |

**Fixes in flight (PRs open):**
- [#75105](https://github.com/NousResearch/hermes-agent/pull/75105) (merged) — MCP cache recovery after OAuth failure
- [#75102](https://github.com/NousResearch/hermes-agent/pull/75102) — Token estimator double-count fix
- [#75101](https://github.com/NousResearch/hermes-agent/pull/75101) — Cron ledger profile scoping
- [#75103](https://github.com/NousResearch/hermes-agent/pull/75103) — Kanban event-log throttle

**Notable:** No closed issues today — all 50 updated issues remain open. The P1 Windows updater bug is the most critical open item.

---

## 6. Feature Requests & Roadmap Signals

**Strong signals (repeat requests / high relevance):**

- **Subagent Model/Provider Guided Picker** [#67347](https://github.com/NousResearch/hermes-agent/issues/67347) — UX gap, repeated sentiment that free-text config fields are hostile. Likely in next minor (v0.20).
- **Session hygiene for background runs** [#39372](https://github.com/NousResearch/hermes-agent/issues/39372) — Background/integration agent runs polluting user-visible session lists (Desktop, Dashboard, CLI, Cron). Echoed in issue #31584 and several sweeper tags. This is the **most consistent theme this week** — likely a roadmap focus.
- **Semantic / per-message skill retrieval** [#34823](https://github.com/NousResearch/hermes-agent/issues/34823) — Full skill index ~800 tokens/call; semantic retrieval exists but only matches first message. Cost-saving + quality win; flag as likely next-version candidate.
- **Cron metadata passthrough** [#26004](https://github.com/NousResearch/hermes-agent/issues/26004) — Pass `job_id`/`response_id` to platform adapters for better observability. Low-cost, high-value; plausible for v0.19.2/v0.20.
- **Honcho memory pruning controls** [#33436](https://github.com/NousResearch/hermes-agent/issues/33436) — Observation pruning for long-running agents. Growing interest; probably near-term.
- **Config descriptions in UI** [#45119](https://github.com/NousResearch/hermes-agent/issues/45119) — Field descriptions shown in Web Dashboard. Minor UX polish.
- **Custom model entry in `/model` picker** [#33653](https://github.com/NousResearch/hermes-agent/issues/33653) — Consistency gap between CLI and in-session picker.

**Prediction:** Next minor release (v0.20) will likely include session-store hygiene (background run isolation), subagent picker UX, and the MCP HTTP auth feature ([#43633](https://github.com/NousResearch/hermes-agent/pull/43633)) currently in review.

---

## 7. User Feedback Summary

**Pain points (recurring, evidence-based):**

1. **Session-store pollution** — Users report that cron jobs and integration runs create visible sessions in Desktop/Dashboard, confusing history (issues #39372, #31584). This is the **#1 filed concern** this week.
2. **Windows desktop update failures** — P1 bug blocking updates (false PID check) is a hard blocker for Windows users.
3. **Profile isolation leaks** — Foreign `.env` loading and non-scoped cron ledgers suggest multi-profile support has rough edges; some users report secret isolation concerns.
4. **Model fallback correctness** — Invalid tool names (e.g., `multi_tool_use.parallel`) causing silent fallback to secondary models is a **cost and behavior concern** for power users.
5. **Noisy/confusing failure modes** — Crash-style SIGABRTs (exit 134) on shutdown; Kanban respawn loops; usage-limit crashes — all described as *"collapse into crash symptoms."*
6. **Self-improvement unreliability** — The skill-review loop writing failed tasks up as "validated skills" is flagged by a user as a **dangerous trust issue** for autonomous agents.

**Positive signals:**
- Duplicate PRs (e.g., #75120 vs #23434, #72295) suggest **contributors actively watch each other's work** — a healthy maintainer culture.
- Users submitting *"written by my agent"* issues (e.g., #31584, #33436) — indicates organic adoption of Hermes for real workloads; also a subtle signal that agent auth/attribution needs work.
- Only 1 duplicate + 1 retracted PR today — relatively clean contribution pipeline for this volume.

---

## 8. Backlog Watch

Issues/PRs open for a long time without maintainer response — **needs attention:**

| Item | Age | Signals |
|------|-----|---------|
| [#26004 — Cron metadata passthrough](https://github.com/NousResearch/hermes-agent/issues/26004) | 78 days (May 14) | Feature request, 2 comments, still open — likely a small, clear win. |
| [#27804 — Email gateway: subject-based session isolation](https://github.com/NousResearch/hermes-agent/issues/27804) | 74 days (May 18) | 5 comments, P3, explicit user complaint (interrupting tasks on subject change). Still unresolved. |
| [#31584 — Memory-context authority](https://github.com/NousResearch/hermes-agent/issues/31584) | 68 days (May 24) | 10 comments — a big debate; needs a **maintainer decision** to close or implement. |
| [#29667 — WeCom ercode 846609 disconnects](https://github.com/NousResearch/hermes-agent/issues/29667) | 71 days (May 21) | Silent delivery failures; tagged with `sweeper:risk-message-delivery`; unresolved. |
| [#31987 — MCP anyio RuntimeError](https://github.com/NousResearch/hermes-agent/issues/31987) | 67 days (May 25) | P2, clear repro, no fix PR — likely worth a maintainer push. |
| [#33436 — Honcho pruning controls](https://github.com/NousResearch/hermes-agent/issues/33436) | 65 days (May 27) | Feature request with agent-authored issue—low cost, repeated user interest. |
| PR [#43633 — `hermes mcp serve` with auth](https://github.com/NousResearch/hermes-agent/pull/43633) | 51 days (Jun 10) | Feature PR, 0 comments, still open — needs reviewer to move forward. |
| PR [#23434 — BlueBubbles target resolution](https://github.com/NousResearch/hermes-agent/pull/23434) | 82 days (May 10) | Superseded by #75120 (today) — but has sat **unreviewed for 2.5 months**; a maintainer should close/merge explicitly. |

**Recommended focus:** The P1 Windows updater bug, the session-store pollution cluster, and the long-stale PRs (#43633, #23434) deserve immediate maintainer attention. The `needs-decision` tags on #37968, #39372, #62935 also indicate process stalls — decisions are overdue.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-31

## 1. Today's Overview

PicoClaw is in a **moderately active** state with 7 issues and 17 PRs touched in the last 24 hours. A significant portion of PR activity is automated dependency bumps (10 of 17), while the remaining 7 represent substantive feature work and bug fixes. The project shows **healthy ongoing development** across multiple channels (IRC, DingTalk, DeltaChat, WeChat), with notable interest in OAuth 2.x support for MCP servers (two duplicate feature requests). Three issues were closed today, indicating maintainers are actively triaging. No new releases this period. **Overall health: stable, with steady feature development and community engagement.**

---

## 2. Releases

No new releases in this period. The last known version remains 0.3.1 (referenced in issue #3258).

---

## 3. Project Progress

**Merged/Closed PRs (5):**

| PR | Description | Significance |
|---|---|---|
| [#3262](https://github.com/sipeed/picoclaw/pull/3262) | **build(deps):** bump actions/setup-go from 6 to 7 | CI tooling update |
| [#3263](https://github.com/sipeed/picoclaw/pull/3263) | **build(deps):** bump actions/setup-node from 6 to 7 | CI tooling update |
| [#3288](https://github.com/sipeed/picoclaw/pull/3288) | **build(deps):** bump aws-sdk-go-v2/service/bedrockruntime to 1.56.0 | AWS Bedrock runtime update |
| [#3290](https://github.com/sipeed/picoclaw/pull/3290) | **build(deps):** bump aws-sdk-go-v2/config to 1.32.31 | AWS SDK config update |
| [#3163](https://github.com/sipeed/picoclaw/pull/3163) | **feat(bedrock):** leverage Converse prompt caching via cache points | **Significant**: AWS Bedrock prompt caching reduces API costs (reads at ~0.1× input, writes at ~1.25×) — impactful for production users on Bedrock |

**Closed Issues (3):**
- [#2546](https://github.com/sipeed/picoclaw/issues/2546) — OAuth 2.1 + PKCE for MCP servers (closed; as feature request accepted)
- [#3257](https://github.com/sipeed/picoclaw/issues/3257) — Stateless/no-history mode for gateway sessions
- [#3258](https://github.com/sipeed/picoclaw/issues/3258) — Process Hook before_tool bug

---

## 4. Community Hot Topics

### Most Active Discussions

1. **[#2546 — OAuth 2.1 + PKCE for MCP servers](https://github.com/sipeed/picoclaw/issues/2546)** (6 comments, closed)
   - **Demand signal:** Strong. A duplicate request [#3302](https://github.com/sipeed/picoclaw/issues/3302) was filed today, showing continued community need.
   - **Underlying need:** Non-technical users want to add OAuth-protected MCP servers via a simple URL paste — cloud VM friendly, no shell/Node.js required.

2. **[#3287 — Better support for long messages in IRC](https://github.com/sipeed/picoclaw/issues/3287)** (2 comments, open)
   - **Underlying need:** IRCv3 messages split at 512 bytes are treated as separate messages, breaking conversational context. Users want cohesive multi-part message handling.

3. **[#3257 — Stateless/no-history mode for gateway sessions](https://github.com/sipeed/picoclaw/issues/3257)** (2 comments, closed)
   - **Underlying need:** Gateway mode lacks the `--session` control that CLI mode has, forcing stateful sessions for users needing ephemeral conversations.

### PR Activity Highlights
- **[#3270 — DashScope TTS provider + WeChat audio](https://github.com/sipeed/picoclaw/pull/3270)** — Adds Alibaba Cloud TTS and WeChat audio file sending; expands multimodal capabilities.
- **[#3200 — Configurable default fallback model chain](https://github.com/sipeed/picoclaw/pull/3200)** — Users want control over model fallback ordering via web UI; addresses resilience concerns.

---

## 5. Bugs & Stability

**Active bug reports (ranked by severity):**

| Severity | Issue | Status | Fix PR? |
|---|---|---|---|
| 🔴 **High** | [#3258](https://github.com/sipeed/picoclaw/issues/3258) — Process Hook `before_tool` modify broken: **decision field discarded, args misparsed** due to deserialization defect. Breaks core hooking functionality for tool modification workflows. | **Closed** (fix likely merged) | ✅ Issue closed 07-30 |
| 🟡 **Medium** | [#3279](https://github.com/sipeed/picoclaw/pull/3279) — Tool-call format leaking into LLM user messages via seahorse's `partsToReadableContent` — causes model confusion; related to a known bug class. | Open PR | ✅ Fix proposed in PR |
| 🟢 **Low** | [#3308](https://github.com/sipeed/picoclaw/issues/3308) — Code review findings: concurrency hazards, goroutine leaks, memory optimizations in SeaHorse/Channel Manager/Hooks. No immediate crash reports, but architectural concerns raised. | Open, 0 comments | ❌ None yet |

**Notable:** No critical new regressions reported today. The #3258 hook bug is resolved, which was the most impactful stability issue in recent days.

---

## 6. Feature Requests & Roadmap Signals

**New submissions (today):**

| Request | Issue | Likelihood for next release |
|---|---|---|
| **Session list/switch command for Telegram (other chat channels)** | [#3307](https://github.com/sipeed/picoclaw/issues/3307) — Users want `/sessions`-style commands mirroring the Web UI's session management. Medium effort; high value for Telegram power users. | 🟡 **Likely** — complements existing session work |
| **OAuth 2.1 for MCP servers** (duplicate of #2546) | [#3302](https://github.com/sipeed/picoclaw/issues/3302) — Same request as #2546, suggesting demand is real and unmet. | 🟢 **Very likely** — #2546 was closed, indicating acceptance into roadmap |

**Active feature PRs likely to merge soon:**
- **[#3200 — Fallback model chain configuration](https://github.com/sipeed/picoclaw/pull/3200)** — Web UI + backend persistence; near-complete.
- **[#3271 — Default model names refresh to 2026-07 latest](https://github.com/sipeed/picoclaw/pull/3271)** — Needed to keep pace with provider model updates (OpenAI GPT-5.6 series, Anthropic, etc.).
- **[#3222 — DeltaChat cleanup, -200 LOC](https://github.com/sipeed/picoclaw/pull/3222)** — Simplification and docs improvement; long-open (since 07-03) but low risk.

**Trendsignal:** The IRC long-message request ([#3287](https://github.com/sipeed/picoclaw/issues/3287)) plus DingTalk/WeChat/DashScope PRs indicate a **channel-experience polish push** — making each integration more robust rather than adding new channels.

---

## 7. User Feedback Summary

**Pain points expressed:**

1. **Hook system fragility** — User (Shiniese) reported the `before_tool` hook silently failing; decision field discarded and args misparsed. Frustration implied by "not working" in title. Fix is now closed, but this eroded trust in hook reliability.

2. **Gateway mode lacks session control** — User (lisiying) wants stateless mode; works around by using different `--session` values in CLI but can't do the same in gateway. This is a **usability gap between interfaces**.

3. **Multi-protocol message handling inconsistency** — IRC long messages broken (512-byte split); Telegram picture messages on DingTalk needed workaround PRs. Users expect consistent message fidelity across channels.

4. **MCP OAuth barrier for non-technical users** — Two separate users (rameshnetsys, sunboy0523) independently filed for the same feature, indicating repeated friction in real deployments.

**Satisfaction indicators:**
- The OAuth issue closed suggests maintainers acknowledge and may implement it.
- No bug reports expressing "this is broken beyond use" — issues are specific and actionable.
- Dependabot PRs closing quickly (e.g., #3288→#3290 superseding pattern) shows CI pipeline is responsive.

---

## 8. Backlog Watch

**Items needing maintainer attention:**

| Item | Age | Why it matters |
|---|---|---|
| [#3222 — DeltaChat refactor PR](https://github.com/sipeed/picoclaw/pull/3222) | Open since **07-03** | Clean 200-LOC reduction; no comments from maintainers. Risk of bit-rot as code diverges; needs review or explicit deferral. |
| [#3200 — Fallback model chain PR](https://github.com/sipeed/picoclaw/pull/3200) | Open since **07-01** | Major UX feature (fallback model configuration). Long review time may frustrate contributor lc6464. |
| [#3291 — Copilot SDK bump 0.2.0→1.0.8](https://github.com/sipeed/picoclaw/pull/3291) | Open since **07-23** | **Major version jump** (8 minor versions). Needs testing for breaking API changes; close or merge soon. |
| [#3287 — IRC long messages](https://github.com/sipeed/picoclaw/issues/3287) | Opened **07-22** | 2 comments, 0 maintainer response. Community identified a real gap; triage needed. |
| [#3308 — Concurrency/leak code review findings](https://github.com/sipeed/picoclaw/issues/3308) | Opened **07-30** (today) | Zero comments. The submission details goroutine leaks and memory issues — should at least get a maintainer acknowledgment to validate effort. |

**Stale label concern:** Multiple items are marked `[stale]` by bot (e.g., #3289, #3279 PRs), which may auto-close if maintainers don't respond soon — particularly risky for the seahorse fix ([#3279](https://github.com/sipeed/picoclaw/pull/3279)) which addresses a real bug class.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest
**Date:** 2026-07-31

---

## 1. Today's Overview

NanoClaw is in a period of **high-intensity stabilization and hardening**, with 19 PRs updated in the last 24 hours and 7 merges/closures signaling strong maintainer throughput. The project's focus has clearly pivoted toward production reliability: fixing container orchestration bugs, tightening image security, and repairing broken message-handling paths. A significant cluster of work centers on the **agent-runner** and **container-runner** subsystems, indicating real-world deployment feedback is driving the roadmap. However, a concerning pattern of **registry branch drift** (Issue #3155) and several long-stalled community PRs suggest the maintainer team may be prioritizing internal hardening over community feature integration. Overall, the project is **actively healthy**, with a clear emphasis on DevOps maturity (image signing, attestation verification, supply-chain security) rather than new feature velocity.

---

## 2. Releases

**No new releases were published on 2026-07-31.** The project is between release cycles, with the current activity concentrated on master-branch fixes and image re-pinning (see PR #3160) that will likely land in the next minor or patch release. The re-pinning work suggests a hardened image baseline (`hardened-2026-07-30`) is being prepared for a future tagged release.

---

## 3. Project Progress

Seven PRs were merged/closed today, spanning infrastructure, documentation, and bug fixes:

- **PR #3160** *(closed, merged)* – **Agent image re-pinned to `hardened-2026-07-30`** ([link](https://github.com/nanocoai/nanoclaw/pull/3160)). Significant supply-chain improvement: reduced from 18 layers (781 MB) to 8 layers (611 MB), with the largest layer at 27% vs. previous 39%, improving pull gating. **[core-team, merged]**
- **PR #3159** *(closed, merged)* – **Vercel CLI moved to opt-in** ([link](https://github.com/nanocoai/nanoclaw/pull/3159)). Removes baked-in deployment CLI from every agent image, reducing credential surface area by default. **[core-team, merged]**
- **PR #3122** *(closed, merged)* – **opencode compatibility + custom-endpoint transport + memory parity** ([link](https://github.com/nanocoai/nanoclaw/pull/3122)). Major fix cluster for the OpenCode integration, enabling custom endpoint transport and achieving memory parity. **[follows-guidelines, core-team]**
- **PR #2682** *(closed, merged)* – **update-skills now skips v1-only skill branches** ([link](https://github.com/nanocoai/nanoclaw/pull/2682)). Migration tooling fix to avoid breaking v2 compatibility during skill updates.
- **PR #3014** *(closed, merged)* – **`hasIdenticalSend` bound to turn-in-flight** ([link](https://github.com/nanocoai/nanoclaw/pull/3014)). Reliability fix for the agent-runner to prevent cross-turn send deduplication errors. **[follows-guidelines]**
- **PR #3152** *(closed, merged)* – **Architecture docs linked from README** ([link](https://github.com/nanocoai/nanoclaw/pull/3152)). Documentation discoverability improvement.
- **PR #2476** *(closed, likely not merged)* – **`Feat/restart no nanoclaw`** ([link](https://github.com/nanocoai/nanoclaw/pull/2476)). Inactive for ~2.5 months then closed on 07-30; likely rejected or superseded (unclear from data).

---

## 4. Community Hot Topics

- **Issue #3153 – *Message ID suffix bug causing add_reaction/edit_message failures*** ([link](https://github.com/nanocoai/nanoclaw/issues/3153)) – *1 comment*. The single most operationally-impactful issue today: **all inbound message interactions (`add_reaction`, `edit_message`) fail** because the agent-group suffix is not stripped from platform message IDs before the platform API call. On Slack, this manifests as `message_not_found` followed by 3× retries and eventual failure. This is a **core-path bug** affecting any user who wants agents to react or edit inbound messages, and it is the #1 pain point being discussed. *Author: TO-maschenborn.*
- **Issue #3155 – *Registry branches drifted from main; providers fail own install gates*** ([link](https://github.com/nanocoai/nanoclaw/issues/3155)) – *0 comments (but serious)*. A maintainer-level integrity report: the `providers` registry branch has drifted from `main` (at `0b034342`) such that `/add-codex` fails its own typecheck. This points to a **CI/CD pipeline gap** — branch drift is not being caught automatically. *Author: glifocat.*

The most attention is on the **registry drift** issue (from a core contributor) and the **inbound message reaction failure** (from a platform user), together signaling that while the codebase is advancing, **integration consistency and classic message-path reliability are the current weak points**.

---

## 5. Bugs & Stability

*Ranked by severity:*

1. **CRITICAL – Inbound message reactions/edits always fail (Issue #3153)**
   - *Impact:* All `add_reaction` and `edit_message` calls fail on inbound messages (Slack: `message_not_found`), 3× retry, then `failed`. This is a persistent, user-facing functional regression in a core capability.
   - *Fix status:* **None currently.** No PR linked. This is the most visible stability gap in production.

2. **HIGH – Registry branch drift breaks skill installs (Issue #3155)**
   - *Impact:* `/add-codex` cannot install/typecheck on `main` at `0b034342`, because `providers` payloads at `f2b75837` reference a stale baseline. Out-of-the-box operator workflows are broken.
   - *Fix status:* **None.** No PR linked; requires maintainer intervention to re-sync or gate registry updates.

3. **MEDIUM – Orphan containers causing duplicate group spawns (PR #3119, open)**
   - *Impact:* Untracked orphan containers can accumulate (observed: **3 concurrent containers per agent group** on a 5-day uptime host with `*/15` schedule triggers), polling the same session DB.
   - *Fix status:* **PR #3119 open** ([link](https://github.com/nanocoai/nanoclaw/pull/3119)) — reconciliation logic proposed, pending review/merge.

4. **LOW/MEDIUM – MCP server unavailability not reported (PR #3124, open)**
   - *Impact:* When MCP servers are down, the system fails silently instead of reporting.
   - *Fix status:* **PR #3124 open** ([link](https://github.com/nanocoai/nanoclaw/pull/3124)).

5. **LOW – Dangling symlinks break template skill materialization (PR #3157, open)**
   - *Impact:* `materializeTemplateSkills` follows symlinks into container paths (`/app/skills/<name>`) that don't exist at the host level, causing failures.
   - *Fix status:* **PR #3157 open** ([link](https://github.com/nanocoai/nanoclaw/pull/3157)).

---

## 6. Feature Requests & Roadmap Signals

**In-flight (high confidence for next release):**
- **Scheduled task current-time injection (PR #3154, open)** ([link](https://github.com/nanocoai/nanoclaw/pull/3154)) – Gives scheduled tasks the effective run time (`process_after`) rather than creation time, plus a `current_time` field. This is a **directly user-requested operational improvement** for cron-style agents.
- **Structured channel attachments (PR #3156, open)** ([link](https://github.com/nanocoai/nanoclaw/pull/3156)) – Carries channel attachments to providers as structured parts; would fix a long-standing limitation in provider interoperability.
- **Image publisher identity pinning + per-arch attestations (PR #3158, open)** ([link](https://github.com/nanocoai/nanoclaw/pull/3158)) – Fixes a gap where signature verification was skipped because the `AGENT_IMAGE_SIGNER_IDENTITY` variable didn't exist. **Critical for enabling auto-merge gates.**

**Long-stalled community features (low confidence, need maintainer attention):**
- **GitHub polling mode (PR #2301)** – NAT/firewall-friendly polling integration, open since May 6.
- **Free/Whisper voice transcription skill (PR #2317)** – Local free voice transcription, open since May 7.
- **Paws4Claws AWS credential proxy integration (PR #2634)** – Open since May 28.
- **Pre-commit hooks (PR #2537)** – Contributor experience improvement, open since May 18.

---

## 7. User Feedback Summary

- **Pain: Inbound message reactions are fundamentally broken.** The reporter of Issue #3153 is a real user on a real deployment, and this is a guaranteed failure on every inbound message. This is the single loudest signal today: **reaction/edit workflows are a launch-blocker for anyone wanting agents that respond to user interactions.**
- **Pain: Registry drift means `/add-codex` fails its own quality gate.** This is a developer/operator experience issue — the "batteries included" promise is not holding because the registry branches are not kept in lockstep with main.
- **Pain (ongoing): Several long-open community PRs (voice transcription, GitHub polling, pre-commit hooks) have been waiting for review for 2–3 months.** The community is *contributing* but the maintainer loop is slow on non-core items. This may lead to contributor churn.
- **Satisfaction signal:** The number of `[follows-guidelines]`-labelled PRs from external contributors (e.g., #3122, #3014, #2476) shows the contribution process is working, and the project's guidelines are being followed — a healthy sign for community sustainability.

---

## 8. Backlog Watch

*Items needing maintainer attention, sorted by staleness:*

1. **PR #2301 – GitHub polling mode (open since 2026-05-06)** ([link](https://github.com/nanocoai/nanoclaw/pull/2301)) – ~86 days. Inactivity may kill this. Valuable for NAT/firewall users.
2. **PR #2317 – Free voice transcription skill (open since 2026-05-07)** ([link](https://github.com/nanocoai/nanoclaw/pull/2317)) – ~85 days. Local/open-source transcription is a high-demand feature.
3. **PR #2537 – Pre-commit hooks (open since 2026-05-18)** ([link](https://github.com/nanocoai/nanoclaw/pull/2537)) – ~74 days. Quality-of-life for future contributors.
4. **PR #2634 – Paws4Claws AWS creds (open since 2026-05-28)** ([link](https://github.com/nanocoai/nanoclaw/pull/2634)) – ~64 days. Security-relevant for AWS-heavy deployments.
5. **PR #2685 – Signal docs (open since 2026-06-04)** ([link](https://github.com/nanocoai/nanoclaw/pull/2685)) – ~57 days. Docs-only; should be low-risk to merge.
6. **PR #3155 – Registry drift (issue, zero comments)** ([link](https://github.com/nanocoai/nanoclaw/issues/3155)) – If not addressed, will continue to break `/add-*` skills for every user pulling from main.

**Recommendation:** Maintainers should triage the 4-month-old community PRs (either merge or explicitly close with guidance) and prioritize a fix for the message-ID suffix bug (Issue #3153), as it is the most damaging to the core product experience.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-31

## 1. Today's Overview

IronClaw is in a period of intense, multi-track development. With 40 active issues and 29 open pull requests updated in the last 24 hours, the project shows very high activity, driven by three major workstreams: the **target crate architecture refactor** (epic #3773 with 9 new sub-issues filed today), the **skill reliability epic** (#6565) with two new large fixes, and an emerging focus on **security/correctness** concerns identified through user feedback. The volume of new issues filed today (including 8 architecture workstream tickets and 2 new user-reported bugs) suggests the team is actively executing a structured, wave-based refactoring plan. Notably, no new releases were cut, indicating the project is in a build-up phase where significant refactoring is being merged but not yet shipped.

---

## 2. Releases

**No new releases today.** The last release PR (#5598) has been open since July 3rd and would bump `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0), both with breaking API changes. This pending release appears to be waiting for the current large refactoring waves to complete before cutting a new version, given the scale of changes in flight.

---

## 3. Project Progress

Three PRs were merged/closed today (21 total closed in the last 24h across all PRs), the most significant being:

- **[#6934 — refactor(host_api): de-wildcard the contract prelude (WS0)](https://github.com/nearai/ironclaw/pull/6934)** (closed, XL, core): First completed item of the target-architecture program. Removed the flat `pub use <mod>::*;` prelude in `ironclaw_host_api` (45 modules), forcing every consumer to import through module paths. This is behavior-free refactoring that enforces architectural clarity.

- **[#6931 — feat(slack): native /ironclaw slash commands (PR-3 of command train)](https://github.com/nearai/ironclaw/pull/6931)** (closed, XL, core): Final PR of the product command-train, adding native Slack slash command support after role gating (#6873) and the WebUI palette (#6891).

- **[#6874 — chore(deps): bump everything-else group (34 upd...ides)](https://github.com/nearai/ironclaw/pull/6874)** (closed): Routine dependency refresh; superseded by the open #6932.

**Key open PRs advancing features:**
- [#6937](https://github.com/nearai/ironclaw/pull/6937) + [#6938](https://github.com/nearai/ironclaw/pull/6938) (both L-sized, core): The skill reliability epic's two halves — word-boundary keyword matching with measured activation thresholds, and refusing activation with explicit explanations.
- [#6935](https://github.com/nearai/ironclaw/pull/6935) (M, core): Fixes for libSQL cancelled-transaction recovery and conversation-history migration races.
- [#6936](https://github.com/nearai/ironclaw/pull/6936) (XS, core): Architecture baselines + shrink-only exception ratchet (WS0) — the measurement infrastructure before code moves.

---

## 4. Community Hot Topics

The most active issue this period is the **error-recoverability endgame epic**, a top priority for the broader model reliability agenda, per author serrrfirat suggesting a focused, deliverable near-term program:

- **[#6284 — [EPIC] Error-recoverability endgame — the model recovers from 100% of the errors it sees](https://github.com/nearai/ironclaw/issues/6284)** — 15 comments. The contract requires: (a) run survives, (b) model sees, (c) cause+fix visible, (d) model gets a turn to act, (e) no non-success reported. This is the first of four epic-scale issues by serrrfirat in the last 10 days (all authored 7/19-7/23), suggesting a rolling strategic agenda.

- **[#6524 — Epic: Hermetic capability and journey testing platform](https://github.com/nearai/ironclaw/issues/6524)** — 4 comments. Poses the basic question: "Does every supported capability and critical user journey have deterministic, meaningful coverage?"

**Notable for being silent:** The target-architecture epic [#3773](https://github.com/nearai/ironclaw/issues/3773) (opened 5/19) had 0 comments this period, yet generated 9 new issues today ([#6919](https://github.com/nearai/ironclaw/issues/6919) through [#6927](https://github.com/nearai/ironclaw/issues/6927)) and 2 PRs. This is an artifact of the bot-driven pattern, but the teamwork is visible: BenKurrek filed all 9 workstream issues in a single batch with detailed acceptance criteria.

---

## 5. Bugs & Stability

Ranked by severity:

**High — Security/Privacy:**
- **[#6900 — Shared-channel default subject binding collapses all users into the operator's memory namespace (cross-user memory leak)](https://github.com/nearai/ironclaw/issues/6900)** (suggested_P0, security, opened today). When an unrouted shared conversation (e.g., shared Slack channel) is processed, traffic binds to the operator's identity for memory operations. Fails closed or per-actor binding required. No fix PR yet — this is a **P0 security issue** with serious cross-tenant data-leak implications.

- **[#6866 — Same home directory shared across all users; workspaces visible to others](https://github.com/nearai/ironclaw/issues/6866)** (security, user-reported). All users see all workspaces. Requires isolated home dirs per user. Open 3 days, no fix.

**High — Functional breaks:**
- **[#6752 — Instance deletion fails, "Loading your agents..." stuck on re-login](https://github.com/nearai/ironclaw/issues/6752)** (v1-launch-checklist, 1 comment). User cannot delete an instance and gets stuck. On the launch checklist — likely release-blocking.

**Medium — Broken features:**
- **[#6940 — IronHub skill CTA returns 404 across all skills](https://github.com/nearai/ironclaw/issues/6940)** (p2, opened today). Every skill's CTA button links to a 404. Related PR #6933 (ironhub install verification) may address the underlying catalog identity issue.

- **[#6834 — Slack setup fails in IronClaw (near.foundation account)](https://github.com/nearai/ironclaw/issues/6834)** (p2, 1 comment). Extension left unusable after failed setup. Contrast with #6931 landing native slash commands — the Slack surface is actively being developed.

**Low — UI/UX bugs (all filed today by italic-jinxin):**
- [#6916](https://github.com/nearai/ironclaw/issues/6916) — Markdown files render as plain text in preview modal.
- [#6915](https://github.com/nearai/ironclaw/issues/6915) — Workspace file links don't open the referenced file.
- [#6903](https://github.com/nearai/ironclaw/issues/6903) / [#6904](https://github.com/nearai/ironclaw/issues/6904) — Admin users list and Logs page cannot load beyond the first page (pagination bug: `next_cursor` exposed but never used).
- [#6902](https://github.com/nearai/ironclaw/issues/6902) — Projects page displays fabricated metrics (`$0.00 spend`, `0 pending gates`) as real data.

---

## 6. Feature Requests & Roadmap Signals

**Strong signals for next version:**

1. **Migration tool for legacy agents** — [#6939](https://github.com/nearai/ironclaw/issues/6939) (feature, p2, opened today): Users of legacy Hermes/Openclaw face high switching costs with no way to port setup/config/memory. This is a classic adoption-barrier feature; given the project's Reborn branding, this feels like a "reborn migration" tool that could be a launch-moment differentiator.

2. **Keyless release signing** — [#6905](https://github.com/nearai/ironclaw/issues/6905) (opened today): Community maintainer (Packager for Arch Linux AUR) requests cosign keyless signing for verification. Small effort, high trust value for packaged distros.

3. **Skill reliability (epic #6565)** is actively being built (#6937, #6938, #6745 all open). This is a "make what exists work" epic — more of a correctness/quality push than a feature launch.

4. **Error recoverability (epic #6284)** — While not producing visible PRs this period, the 100% error-recovery contract is a deep architectural commitment that will shape many future model-loop changes.

5. **Architecture refactor (epic #3773)** — 10-workstream wave program. The 9 issues filed today ([#6919](https://github.com/nearai/ironclaw/issues/6919)–[#6927](https://github.com/nearai/ironclaw/issues/6927)) are all foundation-setting: the team is keeping the refactor from breaking behavior. Expect a multi-week effort with no user-visible features during the wave.

---

## 7. User Feedback Summary

**Pain points (from x-ai product feedback channel):**

- **Cross-user visibility/privacy is broken** — Reported twice in 3 days (#6866, #6900): users can see each other's workspaces; shared-channel traffic writes to the operator's memory. For a multi-user agent platform, this is the #1 trust-breaking bug.
- **High switching cost for legacy users** (#6939): users of Hermes/Openclaw "resist starting over." This is a retention risk for the Reborn effort — users want a path, not a reset.
- **Broken core flows** — Instance deletion (#6752), Slack setup (#6834), IronHub CTA (#6940): three different first-class integrations in unusable states.
- **UI trust erosion** — Fabricated metrics on Projects page (#6902) and broken file links (#6915) make the product feel unfinished to evaluators walking through it.

**Satisfaction signals:**
- The **command train** (WebUI palette + Slack slash commands, now merged) directly addresses power-user workflows and appears to be a response to earlier feedback.
- **Durable cross-channel attachments** (PR #6364) and **hosted MCP server registration** (PR #6930) are listed as open XL PRs — these are high-value enterprise features that users are likely requesting through support channels.

---

## 8. Backlog Watch

**Long-open items needing attention:**

- **[#6752 — Instance deletion fails (v1-launch-checklist)](https://github.com/nearai/ironclaw/issues/6752)** — Opened 7/28, 1 comment. Tagged v1-launch-checklist, meaning it blocks launch. No PR and no update in 2 days. **Release-blocking.**

- **[#6565 — Epic: Reliable Skill Discovery, Routing, and Activation](https://github.com/nearai/ironclaw/issues/6565)** — Opened 7/23, 1 comment, but 3 PRs attached (#6937, #6938, #6745). The comment is the author's own self-correction, which is healthy.

- **[#5598 — chore: release](https://github.com/nearai/ironclaw/pull/5598)** — Open since 7/3 (28 days). Contains breaking changes to `ironclaw_common` and `ironclaw_skills`. Long-running release train with no version shipped — external users (like the Arch Linux packager in #6905) are waiting on it.

- **[#4636 — Add standalone SSO session and multi-user isolation E2E coverage](https://github.com/nearai/ironclaw/issues/4636)** — Opened 6/9, closed today. This was a test-coverage issue for the exact bug class that #6900 just revealed. **The bug was found one day after the test was closed** — the E2E coverage wasn't hermetic enough to catch the real-world case. Worth reopening to add the shared-channel scenario.

- **[#3773 — Epic: Land the IronClaw Target Crate Architecture](https://github.com/nearai/ironclaw/issues/3773)** — Opened 5/19 (73 days). Active, well-underway, but the age and scope (10 workstreams) suggest it will be a multi-quarter effort. Not a concern, but worth tracking as the project's defining internal program.

**Quiet concern:** dependabot PRs [#5664](https://github.com/nearai/ironclaw/pull/5664) (actions group, open 26 days) and [#6428](https://github.com/nearai/ironclaw/pull/6428) (tokio ecosystem, open 10 days) sit unmerged while a newer parallel PR [#6932](https://github.com/nearai/ironclaw/pull/6932) (everything-else, 34 updates) was filed today. The dependency-updating process appears to be accumulating, possibly waiting for the release train.

---

## Overall Health Assessment

IronClaw is **architecturally healthy** — the team is investing in structural refactoring (target architecture, de-wildcarding) before feature acceleration, which is a sign of long-term intent. However, **user-facing stability is the weak spot**: three separate first-class integrations (Slack, IronHub, instance lifecycle) are broken per user reports, and the P0 memory-isolation leak (#6900) suggests the multi-user model wasn't fully hardened before the Reborn push. The gap between the ambitious internal refactoring work (9 issues filed in one batch) and the low-priority user feedback bug fixes is notable — a **launch-blocker (instance deletion) has gone unsolved for 3 days** while the team works on internal architecture. For a project near v1 launch, prioritizing the user-facing breakages while continuing the refactor wave would balance health signals.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-31

## 1. Today's Overview

LobsterAI is in a high-velocity development phase, with 10 pull requests updated in the last 24 hours and a fresh release shipped on July 29th. The project shows strong momentum, particularly around the cowork collaboration features, enterprise account isolation, and native activity experiences. The majority of PRs (8) were merged or closed, indicating a healthy review-to-merge pipeline, while 2 stale PRs from early April remain open. No new issues were filed or updated in this window, suggesting the community is currently more focused on consuming and testing new features rather than reporting problems.

## 2. Releases

### LobsterAI 2026.7.29 — Released July 29, 2026

The latest release brings several notable improvements:

- **Selected Text Tags in Side Chat**: The cowork side chat now supports tagging selected text, enhancing the contextual editing experience.
- **Kimi K3 Model Support**: New model integration expands the range of available AI backends.
- **Harden Session Lifecycle & Token Refresh**: Auth improvements to prevent session drops and token expiration issues.

**Migration Notes**: No breaking changes were announced in the release notes. The session lifecycle hardening may require users to re-authenticate once after upgrading.

**Link**: [Release 2026.7.29](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.7.29)

## 3. Project Progress

Seven PRs were merged or closed today, spanning several functional areas:

### Cowork Collaboration (3 PRs)
- **[PR #2397](https://github.com/netease-youdao/LobsterAI/pull/2397)**: Added an isolated `/btw` side chat panel — an editable floating window for selected assistant text, with drag/resize/stop/follow-up capabilities. Execution history is kept separate from the main conversation and routed through the OpenClaw utility stream.
- **[PR #2406](https://github.com/netease-youdao/LobsterAI/pull/2406)**: Improved side chat input handling — accumulates selected text excerpts while the panel is open, and removed product-level question length limits while retaining transport safety checks.
- **[PR #2405](https://github.com/netease-youdao/LobsterAI/pull/2405)** (in release): Added selected text tags to the side chat.

### Enterprise & Account Isolation (1 PR)
- **[PR #2409](https://github.com/netease-youdao/LobsterAI/pull/2409)**: Isolated auth, media, queued follow-up, sharing, and deployment state per account. Prevents stale async responses from leaking into newly signed-in accounts, and enforces enterprise entitlements with improved rollback/cleanup.

### Native Activity Features (2 PRs)
- **[PR #2408](https://github.com/netease-youdao/LobsterAI/pull/2408)**: Added a server-driven native daily check-in experience in the desktop sidebar and account menu, allowing signed-out users to trigger login flow and authenticated users to claim daily credit rewards without exposing tokens to the renderer.
- **[PR #2411](https://github.com/netease-youdao/LobsterAI/pull/2411)**: Unified sidebar carousel for daily check-in activities and image banners, with dismissal and reopen support.

### Windows Stability & UI Polish (3 PRs)
- **[PR #2412](https://github.com/netease-youdao/LobsterAI/pull/2412)**: Fixed NSIS installer to re-kill survivor processes on every poll round, catching processes that outlive the observation window.
- **[PR #2410](https://github.com/netease-youdao/LobsterAI/pull/2410)**: Aligned Sites page layout width/spacing/search styling with Skills and MCP management views.
- **[PR #2389](https://github.com/netease-youdao/LobsterAI/pull/2389)**: Fixed email attachment path traversal vulnerability with sanitization and directory boundary enforcement, plus cross-platform security tests.

## 4. Community Hot Topics

The most active PRs today center on the **cowork side chat** feature and **daily check-in activity**, both authored by core maintainers (`liuzhq1986`, `btc69m979y-dotcom`), indicating that these are product-driven initiatives rather than community-led.

**Analysis of underlying needs**:
- **PR #2397** (`/btw` side chat) and **PR #2406** (input handling) together reveal a strong push to make the assistant interaction more fluid — users want to reference and refine specific text segments without losing context in the main conversation.
- **PR #2408 + #2411** (daily check-in) signal a move toward user retention/gamification in the desktop app, a typical lifecycle step for mature productivity tools.

**Community-led signals**: The two 3-month-old stale PRs (see Backlog Watch) remain the only community contributions among open PRs, and neither has received maintainer comments.

## 5. Bugs & Stability

Two stability/security issues were addressed today:

| Severity | Issue | Fix PR | Status |
|----------|-------|--------|--------|
| **High (Security)** | Email attachment path traversal — malicious filenames could escape the download directory | [PR #2389](https://github.com/netease-youdao/LobsterAI/pull/2389) — filenames sanitized, directory boundaries enforced, cross-platform tests added | ✅ Merged |
| **Medium (Windows)** | NSIS installer could leave survivor processes alive when teardown outruns the polling window | [PR #2412](https://github.com/netease-youdao/LobsterAI/pull/2412) — Stop-Process now reissued each poll round with per-process logging | ✅ Merged |

**No new bugs, crashes, or regressions were reported via issues in the last 24 hours.**

## 6. Feature Requests & Roadmap Signals

Based on today's merged PRs, the following features appear to be on the roadmap:

1. **Account-Scoped Enterprise States** (PR #2409) — Multi-account isolation suggests enterprise multi-tenancy is being actively hardened. Expect more enterprise entitlement enforcement in upcoming releases.
2. **Native Gamification/Retention** (PR #2408, #2411) — Daily check-in rewards and banner carousels suggest a user-growth initiative. This will likely expand to more activity types (streaks, achievements).
3. **Incremental Text Interaction** (PR #2397, #2406) — The `/btw` side chat is a foundation for richer context-aware assistant interactions. Follow-up features may include multi-segment references, inline diff previews, or batch operations on selected text.
4. **Model Expansion** — Kimi K3 support (PR #2381) indicates continued investment in multi-provider model compatibility.

## 7. User Feedback Summary

With **zero new issues** in the last 24 hours, direct user feedback via issue tracker is minimal. However, indirect signals from PR descriptions highlight:

- **Pain point addressed**: Selected-text context loss when switching between assistant conversations → solved via isolated side chat with accumulated excerpts.
- **Pain point addressed**: Session/token expiration interrupting workflow → hardened auth lifecycle in release 2026.7.29.
- **UX consistency gap**: Sites page didn't match the styling of Skills/MCP → now aligned.
- **Security concern**: Attachment path traversal in email skill → fixed and tested.

The lack of complaint-driven issues suggests the current user base is generally satisfied or is primarily engaged in testing new features (as evidenced by the dense PR activity).

## 8. Backlog Watch

Two PRs from April 1, 2026 have been open for **4 months** without maintainer action:

1. **[PR #1228](https://github.com/netease-youdao/LobsterAI/pull/1228)** — *feat(cowork): 新增会话「标记为未读」功能* (Mark sessions as unread)
   - Adds "Mark as Unread" to session detail menu, context menu, Redux slice, and i18n.
   - **Why it matters**: Directly aligned with the current cowork collaboration push (PR #2397, #2406, #2405). The maintainers are rebuilding cowork UX in this area, and this stale contribution could be cherry-picked or adapted.

2. **[PR #1231](https://github.com/netease-youdao/LobsterAI/pull/1231)** — *fix(agent): AgentCreateModal 支持 Escape 键关闭，并在重新打开时重置表单*
   - Fixes missing Escape-key behavior and residual form data on reopen.
   - **Why it matters**: Addresses a UX consistency bug that the project clearly values (other modals already have this). Low-risk fix, likely mergeable as-is.

**Recommendation**: Maintainers should evaluate both PRs against the current cowork/agent refactoring or explicitly close them with guidance, to avoid accumulating stale contributions that may discourage community contributors.

---

*Digest generated from [LobsterAI GitHub data](https://github.com/netease-youdao/LobsterAI) for 2026-07-31.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-31

## 1. Today's Overview

Moltis shows a healthy, focused development cadence with 4 PRs updated and 2 new issues filed in the last 24 hours. The project is actively consolidating its channel infrastructure, with work spanning Slack reliability (reactions, reconnects, Block Kit), Telegram interactivity (inline buttons requested), and security hardening (privileged tool gating). Notably, #1170 successfully separates access from operator privilege — a meaningful security boundary improvement. While no new releases shipped this cycle, the merged Slack PR (#1166) indicates feature-complete work that will likely land in the next release. The issue tracker remains lean (2 open items), suggesting maintainers are responsive and the backlog is manageable.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release activity predates this digest window; the community should watch for an upcoming release that will likely incorporate the merged Slack improvements (#1166) and the security fix for operator privilege (#1170).

## 3. Project Progress

One PR was merged/closed in the last 24 hours:

- **[#1166 [MERGED] feat(slack): per-message acknowledgment reactions, phases, reconnect supervision, and Block Kit](https://github.com/moltis-org/moltis/pull/1166)** — This substantial PR builds on earlier acknowledgment-reaction work (#1165) to make the Slack reaction lifecycle safe under queueing, cancellation, retries, callback bursts, and delivery failures. It adds phase tracking, reconnect supervision, and Block Kit support. Since Slack bots lack typing indicators, this provides users with a critical visual receipt/progress signal.

Two additional PRs remain open and are actively being updated:

- **[#1174: Add instrumentation and feedback collection infrastructure](https://github.com/moltis-org/moltis/pull/1174)** — Adds backend-neutral agent instrumentation with Langfuse v4 export, OTLP backends, and end-user reaction feedback. Includes streaming/non-streaming parity and cache-aware token usage.
- **[#1170: gate /sh and privileged tools behind a per-account operators list](https://github.com/moltis-org/moltis/pull/1170)** — Security hardening that separates access from privilege; actively updated today.

## 4. Community Hot Topics

No issues or PRs currently show significant comment activity (all have 0 comments, 0 reactions). However, the following items represent the most actively worked-on topics:

- **[PR #1174: Instrumentation & feedback infrastructure](https://github.com/moltis-org/moltis/pull/1174)** — Open for 4 days, updated today. This is the most substantial open PR and signals a major investment in observability and user-feedback loops.
- **[PR #1170: Privileged tools / operators list](https://github.com/moltis-org/moltis/pull/1170)** — Open for 5 days, updated today. Security boundary enforcement is clearly a priority.
- **[PR #1176: Markdown copy and session export](https://github.com/moltis-org/moltis/pull/1176)** — New PR (1 day old) adding user-requested export functionality for the web client.

**Underlying need analysis**: The community is pushing for (a) production-grade observability (instrumentation), (b) stronger multi-tenant security controls, and (c) better data portability (Markdown export). These are hallmarks of a project transitioning from early adoption to enterprise-ready maturity.

## 5. Bugs & Stability

One bug was reported in the last 24 hours:

- **[#1177 [OPEN] [Bug]: Vault Unlock/Recovery Endpoints Missing Authentication (CWE-306)](https://github.com/moltis-org/moltis/issues/1177)** — **Severity: Critical.** This is an authentication bypass vulnerability on vault unlock/recovery endpoints. Missing authentication on credential-recovery endpoints could allow unauthorized vault access. Given the concurrent security PR (#1170) addressing privileged tool boundaries, the maintainers appear to be actively hardening security. **No fix PR exists yet for this specific issue** — community should track this closely.

No crashes, regressions, or other stability issues were reported today.

## 6. Feature Requests & Roadmap Signals

One new feature request was filed:

- **[#1178 [OPEN] [Feature]: Let agents send Telegram inline buttons and receive structured callback responses](https://github.com/moltis-org/moltis/issues/1178)** — Users want agents to create interactive Telegram inline-button interfaces with structured callback handling.

Predictions for next release:
- **Telegram inline buttons** are a natural extension of the recently merged Slack Block Kit work (#1166). The channel-interactivity pattern is already established, making this a likely next feature.
- **Instrumentation & feedback (#1174)** will likely land soon — it's the most mature open PR and aligns with the project's observability trajectory.
- **Vault auth fix** will probably be prioritized as a hotfix given its critical severity.

## 7. User Feedback Summary

User activity today reflects two clear themes:

1. **Security-consciousness**: The vault vulnerability report (#1177) demonstrates that users are actively security-testing the platform and care about credential safety. The style of the report (CWE reference, preflight checklist completed) suggests an experienced security practitioner in the community.

2. **Feature maturation**: The Telegram inline-button request (#1178) shows users want to build richer, more interactive agent experiences beyond text-based chat. Combined with the Markdown export PR (#1176), there's a clear demand for both richer input (interactive controls) and richer output (portable data).

No explicit dissatisfaction or negative sentiment was expressed in today's activity. The project appears to be meeting user expectations in terms of responsiveness and feature velocity.

## 8. Backlog Watch

**Needs immediate attention:**

- **[Issue #1177: Vault Unlock/Recovery auth bypass (CWE-306)](https://github.com/moltis-org/moltis/issues/1177)** — Critical security vulnerability; should be triaged and assigned immediately.

**Watching:**

- **[PR #1170](https://github.com/moltis-org/moltis/pull/1170)** and **[PR #1174](https://github.com/moltis-org/moltis/pull/1174)** have been open for 5 and 4 days respectively, both updated today — actively progressing, no maintainer action needed beyond continued review.
- **[PR #1176: Markdown copy/export](https://github.com/moltis-org/moltis/pull/1176)** is new (1 day) and awaiting maintainer review. Low-risk, user-visible improvement.

No stale issues (>30 days without response) were detected in the current backlog.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest
**Date:** 2026-07-31

---

## 1. Today's Overview

CoPaw (QwenPaw) is in a period of intense stabilization and polish following the v2.0 release. The project shows **high activity** with 25 issues and 50 PRs updated in the last 24 hours, reflecting an active community and responsive maintainers. The majority of activity centers on **bug fixes** (50% of closed PRs) and **UX enhancements**, with significant attention on MCP server reliability, shell command handling, and desktop application polish. The influx of first-time contributors (4+ in the PR list) suggests growing community interest, though the CI infrastructure bug blocking fork PRs (#6563, now closed) may have temporarily dampened external contributions. Overall, the project appears **healthy and responsive**, with maintainers actively reviewing and merging PRs (26 merged/closed in 24h), though no new releases were published today.

## 2. Releases

No new releases were published in the last 24 hours. The latest stable version remains **v2.0.1**, which has been the subject of many of the bug reports seen in this digest. Users are reporting issues directly attributable to the v2.0 architectural changes, most notably a ~2s overhead per reply (#6307) and MCP session recovery problems (#6524), suggesting a **v2.0.2 patch release is likely imminent** given the number of merged fixes awaiting release.

## 3. Project Progress

**26 PRs were merged or closed in the last 24 hours**, indicating strong momentum. Key advancements include:

- **[MERGE] feat(computer-use): native desktop GUI automation** ([PR #6424](https://github.com/agentscope-ai/QwenPaw/pull/6424)) — Large feature adding macOS/Windows desktop control via accessibility-first + Tauri control mode, now merged.
- **[MERGE] fix(matrix): probe vodozemac E2EE backend** ([PR #6486](https://github.com/agentscope-ai/QwenPaw/pull/6486)) — Fixes Matrix E2EE encryption (issue #6476) by supporting modern `vodozemac` backend on Python 3.12.
- **[MERGE] feat(governance): sandbox-unavailable fallback configurable** ([PR #6256](https://github.com/agentscope-ai/QwenPaw/pull/6256)) — Gives operators control over fallback behavior when sandbox is unavailable (issue #6250).
- **[MERGE] feat(creator): checkpoints, home redesign, media recovery** ([PR #6556](https://github.com/agentscope-ai/QwenPaw/pull/6556)) — Major Creator plugin iteration with creation checkpoints, media recovery, and export/import.
- **[MERGE] Multi-bug fix: /mission TypeError, approval inheritance, CI** ([PR #6562](https://github.com/agentscope-ai/QwenPaw/pull/6562)) — BlackBox-Labs (first-time contributor) fixed issues #6533, #6506, and #60.
- **[MERGE] fix(sandbox): cleanup handling** ([PR #6582](https://github.com/agentscope-ai/QwenPaw/pull/6582)) — Tool sandbox cleanup fixes.
- **[MERGE] fix(ci): ensure changes detected in reload()** ([PR #6584](https://github.com/agentscope-ai/QwenPaw/pull/6584)) — CI reliability improvement.

**Still open and under review** (highlights):

- **feat: unify provider discovery, model metadata, routing** ([PR #6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)) — Large architectural PR consolidating 7 model-provider pain points.
- **feat(console): configurable theme/skin module** ([PR #6312](https://github.com/agentscope-ai/QwenPaw/pull/6312)) — Draft implementation of Task 1 from #2291.

## 4. Community Hot Topics

**Most Active Issues (by comments):**

1. **[Performance] ~2s fixed overhead per reply in v2.0** ([#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307)) — 7 comments. Users are measuring direct regressions from v1.x; this is a critical adoption blocker.

2. **[MCP] Backend restart breaks auto-recovery** ([#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524)) — 5 comments. Stale `mcp-session-id` reuse after server restart; fix PR #6586 now open.

3. **[CI] 'Real behavior proof' workflow blocks all fork PRs** ([#6563](https://github.com/agentscope-ai/QwenPaw/issues/6563)) — 4 comments, **now closed** (fixed). The community was frustrated as this blocked all external contributions.

4. **[API] Connection test failure on AgentScope Platform** ([#6464](https://github.com/agentscope-ai/QwenPaw/issues/6464)) — 3 comments, **closed**. Deployment-specific issue with model connectivity.

**Analysis:** The community is primarily facing **v2.0 migration pains** (performance regression, MCP behavior changes) and **deployment friction** (AgentScope Platform). The swift closures of #6563 using Fix PRs indicate maintainers are actively engaging with community pain points.

## 5. Bugs & Stability

**Ranked by severity (reported in last 24h, unless noted):**

| Severity | Bug | Issue | Fix PR Status |
|----------|-----|-------|---------------|
| 🔴 **Critical** | `execute_shell_command` truncates >30KB output, sometimes with Internal error | [#6512](https://github.com/agentscope-ai/QwenPaw/issues/6512) | No fix PR yet |
| 🔴 **Critical** | `execute_shell_command` large output freezes UI entirely | [#6589](https://github.com/agentscope-ai/QwenPaw/issues/6589) | No fix PR yet |
| 🟠 **High** | `spawn_subagent` single-task mode unusable — `batch` incorrectly required | [#6588](https://github.com/agentscope-ai/QwenPaw/issues/6588) | No fix PR yet |
| 🟠 **High** | `execute_shell_command` folds newlines into spaces, breaking multi-line commands | [#6565](https://github.com/agentscope-ai/QwenPaw/issues/6565) | No fix PR yet |
| 🟠 **High** | ~2s fixed overhead per reply (v2.0 regression) | [#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307) | Under investigation |
| 🟡 **Medium** | MCP session recovery after backend restart | [#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524) | Fix PR #6586 open |
| 🟡 **Medium** | MCP tool names starting with `-` rejected by strict LLM APIs | [#6557](https://github.com/agentscope-ai/QwenPaw/issues/6557) | Fix PR #6561 open |
| 🟡 **Medium** | Dream/memory compression misses early-session events | [#6555](https://github.com/agentscope-ai/QwenPaw/issues/6555) | Under discussion |
| 🟢 **Low** | Session fork chaos — no parent-child grouping | [#6559](https://github.com/agentscope-ai/QwenPaw/issues/6559) | No fix PR yet |
| 🟢 **Low** | `dispatch.mode: "final"` not honored for cron jobs | [#6578](https://github.com/agentscope-ai/QwenPaw/issues/6578) | **Closed** (fixed) |

**Notable:** The `execute_shell_command` family of bugs (#6512, #6589, #6565) forms a **critical cluster** affecting power users — the primary use case for CoPaw. Fixes here should be prioritized.

## 6. Feature Requests & Roadmap Signals

**Most requested features (by signal strength):**

1. **Workflow / Strong logic enforcement** ([#6571](https://github.com/agentscope-ai/QwenPaw/issues/6571)) — Users need deterministic permission-based workflows (e.g., query employee ID → check permissions → execute/deny). Current skill system insufficient for security-critical logic.

2. **Global shortcut quick-input popup** ([#6568](https://github.com/agentscope-ai/QwenPaw/issues/6568)) — macOS `Option+Space`-style floating mini input (like Raycast/豆包). User verified current Tauri code already has hooks; likely a **v2.1 candidate**.

3. **Session / chat UX overhaul** ([#6558](https://github.com/agentscope-ai/QwenPaw/issues/6558), [#6560](https://github.com/agentscope-ai/QwenPaw/issues/6560), [#6408](https://github.com/agentscope-ai/QwenPaw/issues/6408)) — Copy, undo (removed), session hierarchy (retrieval). Cherry Studio-style undo command (#6408) closed — possibly implemented?

4. **Configurable display preferences** — Multi-line file lists (#6583), character-count toggle (#6585), app name simplification (#6587). All small UI polish items likely **landing in v2.0.2**.

5. **Desktop GUI automation** ([PR #6424](https://github.com/agentscope-ai/QwenPaw/pull/6424) — merged) — Computer-use tool is now merged; expect community tutorials/demos soon.

**Predictions for next release (v2.0.2):** Fixes for `execute_shell_command` truncation/freezing, MCP tool name sanitization, MCP session recovery, and UI polish items. **v2.1/3.0:** Session tree view, workflow engine, global hotkey input.

## 7. User Feedback Summary

**Positive signals:**

- Community members are actively contributing first-time PRs (BlackBox-Labs, JOJOCrazy123, WilShi, niuda-kok, mohitdebian) — indicates approachable codebase and welcoming maintainers.
- Users testing advanced features (Computer Use, Creator plugin, Mission mode) suggest strong product-market fit for power users.
- "非常不错的项目" ("very nice project") — direct praise in #6585.

**Pain points (ranked by frequency/severity):**

1. **Shell command reliability is the #1 complaint** — output truncation (#6512), UI freeze (#6589), newline handling (#6565). Affects the core agent experience.
2. **MCP integration friction** — session recovery (#6524), strict LLM API rejections (#6557). MCP is a key integration surface.
3. **Session/context management chaos** — unwanted forks (#6559), lost messages on switch (#6558), no way to undo (#6408). Users feel loss of control.
4. **v2.0 performance regression** (#6307) — though this is a single issue, 2s overhead affects every interaction.
5. **Polished UX details** — monitor permission popups (#6452), app naming (#6587), character counter flashing (#6585), truncated file names (#6583). Indicates users care about the 10% finishing touches.

**Satisfaction assessment:** Users are **engaged but impatient**. They want CoPaw to be a daily-driver tool; current bugs in critical paths (shell, MCP) force workarounds. Maintainers are responding quickly (7 issues closed today), which should yield improved sentiment after v2.0.2.

## 8. Backlog Watch

**Issues/PRs needing maintainer attention:**

1. **[#6307] Performance: 2s overhead per reply** — Created 2026-07-21, 10 days old. Critical regression, 7 comments, no resolution yet. This is the **top priority item** on this list.

2. **[#6302] PR: Unify provider discovery, model metadata, routing** — Open since 2026-07-21 without review comments. Large architectural change; being ignored may stall all provider-related improvements.

3. **[#6559] Session forking chaos** — Open since 2026-07-29, 2 comments only. Significant UX concern with no maintainer response — scheduling to act before user growth makes migration harder.

4. **[#6312] PR: Configurable theme/skin (draft)** — Open since 2026-07-21. No maintainer feedback on direction/scope; first-time contributor may lose momentum.

5. **[#6531] PR: Add `models` field to ACP `new_session`** — Open since 2026-07-28, marked Under Review. Important for external ACP clients (Multica, OpenCode, Zed). Unreviewed for 3 days — risk of ecosystem staleness.

6. **[#6512] execute_shell_command output truncation** — Open since 2026-07-28, 2 comments. Critical bug with no fix PR yet. Maintainers should **communicate acknowledgement**.

7. **[#6588] spawn_subagent schema `batch` bug** — Open since 2026-07-30. Blocks single-agent async usage; likely small fix, should be quick to resolve.

---

*Data sourced from GitHub (agentscope-ai/CoPaw) on 2026-07-31. Metrics based on 25 issues and 50 PRs updated in the last 24 hours.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-07-31

## 1. Today's Overview
ZeptoClaw is in a quiet but focused period: no new issues or releases in the last 24 hours, and no merges or closures on the PR front. The single open pull request, #645, is a substantive runtime hardening effort by the maintainer that has seen recent activity (updated yesterday) but has not yet been merged. This suggests active but deliberate development, likely awaiting review or additional testing. Overall, the project appears stable with low community churn and a maintenance-focused trajectory.

## 2. Releases
No new releases were published in the last 24 hours. The most recent release information is not available in this data window; users should monitor the [releases page](https://github.com/qhkm/zeptoclaw/releases) for upcoming version announcements.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The sole open PR, [#645](https://github.com/qhkm/zeptoclaw/pull/645), represents the project's current forward momentum. Authored by maintainer `qhkm`, it targets two critical runtime issues:
- **Secret scrubbing:** Ensures subprocess shell commands no longer inherit ZeptoClaw's full process environment, preventing provider keys and unrelated credentials from leaking into model-authored commands.
- **Process tree reaping:** Fixes timeout handling where `Command::output()` futures were dropped without consistently terminating and reaping descendant processes, which could leave orphans (especially in Docker containers).

These are foundational security and lifecycle improvements that, once merged, will strengthen the runtime's isolation guarantees.

## 4. Community Hot Topics
There is minimal community activity today: zero issues and one PR with no comments or reactions. PR [#645](https://github.com/qhkm/zeptoclaw/pull/645) is the single topic of note. While it lacks direct engagement metrics, its subject matter—credential leakage and zombie process cleanup—signals an underlying need for **secure subprocess execution** and **deterministic resource cleanup** in AI-agent runtimes. These are common pain points in the broader agent tooling ecosystem, where model-authored commands often run with excessive privileges or leave system resources in inconsistent states.

## 5. Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. The stability concerns addressed by PR [#645](https://github.com/qhkm/zeptoclaw/pull/645) are pre-emptive fixes rather than responses to filed bug reports:
- **High severity (potential):** Unauthorized credential exposure via inherited environment variables in subprocesses. No user-facing exploit has been reported, but the risk is significant if model-authored commands can access provider keys.
- **Medium severity (potential):** Orphaned process trees after runtime timeouts, which could accumulate system load or interfere with subsequent commands.

Both are addressed by the open PR, indicating proactive maintainer response to likely edge cases.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed in the last 24 hours. However, PR [#645](https://github.com/qhkm/zeptoclaw/pull/645) hints at the roadmap direction: **hardening the execution sandbox**. Anticipated next-version improvements may include:
- Configurable environment allowlisting/denylisting for subprocesses.
- More granular timeout and process-group management (e.g., `SIGKILL` fallbacks, cgroup integration).
- Optional Docker-specific cleanup hooks for long-running containers.

These are sensible extensions of the current fix and align with best practices for secure agent runtimes.

## 7. User Feedback Summary
There is no direct user feedback in the last 24 hours (no issues, comments, or reactions). The absence of filed complaints is mildly positive, but it also limits insight into user satisfaction. The maintainer's proactive work on secret scrubbing and process reaping suggests awareness of operational pain points, even if users have not formally voiced them. For the broader community, the lack of issues may indicate a stable feature set or a small user base; more signal is needed to assess satisfaction trends.

## 8. Backlog Watch
No long-unanswered issues or PRs are in the backlog. The single open PR, [#645](https://github.com/qhkm/zeptoclaw/pull/645), has been open for 8 days (since 2026-07-23) with its last update yesterday. Given its importance to runtime security and stability, maintainer attention should focus on completing the review and merging this PR promptly to avoid stagnation. No other items require triage.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest
**Digest Date:** 2026-07-31

---

## 1. Today's Overview

ZeroClaw is in a period of intense development activity, with a high volume of open work items. The project currently shows **15 open issues** and **50 open pull requests** updated in the last 24 hours, indicating a very active community and maintainer pipeline. However, with **zero PRs merged or closed** in this period, the project appears to be in a consolidation phase, focusing on refining and reviewing existing proposals rather than landing new code. Notably, there is a significant cluster of high-severity security bugs reported today (see Bugs & Stability), signaling a critical focus on hardening the gateway and sandbox components. The maintainers are actively engaged with a backlog of high-priority RFCs, suggesting a strategic planning phase for substantial architectural feature additions.

## 2. Releases

No new releases were published in the last 24 hours. There are no release notes, breaking changes, or migration guides to report for this digest period.

## 3. Project Progress

No pull requests were merged or closed in the last 24 hours. The project is not advancing new code into the `master` branch during this period. However, significant work is in progress across a wide front, as evidenced by active PRs:

- **Security Hardening:** Multiple PRs are addressing critical security findings reported today, including fixes for webhook verification and command allowlist matching.
- **Architecture RFCs:** A large number of "RFC" labeled issues are under active discussion for major features like OpenAI compatibility and memory separation, indicating the roadmap is being actively shaped.
- **Eval & Tooling:** A series of PRs from contributor `IftekharUddin` are advancing the evaluation framework, including run-history receipts (#9248) and regression test seeding (#9225), working to stabilize the testing pipeline.
- **Core Features:** Large-scale PRs like #8688 (trusted goal tools) and #9126 (plugin config validation) are in progress but require author attention, indicating the project is managing a heavy PR load.

## 4. Community Hot Topics

The most active discussions are centered on architectural design and high-impact enhancements:

- **[RFC: Separate conversation history from agent-curated long-term memory (#9048)](https://github.com/zeroclaw-labs/zeroclaw/issues/9048)** - With 12 comments, this is the most discussed issue. The community is heavily debating the core architecture of how ZeroClaw handles memory, indicating a strong need for clearer separation between ephemeral session context and durable, curated knowledge. This is a foundational change that will likely have widespread implications.
- **[RFC: OpenAI Chat Completions compatibility adapter (#8603)](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) & [Feature: Add OpenAI-compatible chat completions endpoint (#8550)](https://github.com/zeroclaw-labs/zeroclaw/issues/8550)** - These two related issues (7 and 5 comments respectively) highlight a very strong community demand for interoperability. Users want to connect standard OpenAI-compatible clients (like Open WebUI, LobeChat) directly to ZeroClaw without building custom adapters.
- **[[Feature]: define a compact local_small runtime profile (#5287)](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)** - With 7 comments and 2 👍 reactions, this shows a solid user base interested in a streamlined, low-resource local-first mode, emphasizing the project's commitment to local model support.

## 5. Bugs & Stability

Today saw the report of several serious bugs, primarily security-focused, all with corresponding fix PRs opened by the same reporter:

- **[S0 - Critical: Gateway webhook handlers do not fail closed (#9565)](https://github.com/zeroclaw-labs/zeroclaw/issues/9565)** - This is a severe data loss/security risk where WhatsApp Cloud, Linq, and WATI webhook handlers dispatch attacker-controllable messages without authentication. A fix PR ([#9569](https://github.com/zeroclaw-labs/zeroclaw/pull/9569)) has been opened to make these handlers fail closed when verification is not possible.
- **[S2 - High: Uppercase allowed_commands entries never match on Unix (#9566)](https://github.com/zeroclaw-labs/zeroclaw/issues/9566)** - This is a regression causing a silent denial of service for commands defined with uppercase characters. The fix PR ([#9568](https://github.com/zeroclaw-labs/zeroclaw/pull/9568)) addresses case-insensitive matching for the allowlist.
- **[S3 - Minor: cargo test --doc fails with duplicated rustdoc theme flag (#8847)](https://github.com/zeroclaw-labs/zeroclaw/issues/8847)** - A CI stability issue where `cargo test --doc` fails under Rust 1.96, blocking the CI pipeline.

## 6. Feature Requests & Roadmap Signals

The active RFCs provide strong signals for the upcoming roadmap:

- **External API Compatibility:** The two OpenAI-compatible endpoint requests (#8603, #8550) are clearly a major priority. Given their age and "in-progress" status, it is likely a version of this will land soon, opening ZeroClaw to a massive ecosystem of tools.
- **Memory Architecture Overhaul:** The RFC for separating conversation history from long-term memory (#9048) is a high-priority, high-risk architectural change. This is a foundational improvement likely destined for a major release (e.g., v0.9.0) rather than a minor patch.
- **New Interaction Modalities:** The [RFC for a Gemini Live realtime speech channel (#8780)](https://github.com/zeroclaw-labs/zeroclaw/issues/8780) points towards future voice-first interfaces.
- **Advanced Model Orchestration:** The [Mixture-of-Agents provider (#8568)](https://github.com/zeroclaw-labs/zeroclaw/issues/8568) signals a move towards more complex, AI-driven model routing for improved quality on hard tasks.

## 7. User Feedback Summary

- **Pain Point (Interoperability):** The repeated requests for an OpenAI-compatible API are the clearest signal of user pain. It is a significant barrier to entry for users invested in existing AI client ecosystems.
- **Pain Point (Local-First UX):** Issue #5287 and #7951 reveal users want more control over local vs. cloud model usage, with a desire for a more compact, efficient local runtime mode.
- **Satisfaction (Active Community):** The high volume of activity and detailed RFCs suggest a healthy and engaged community, though the significant number of PRs needing `needs-author-action` could indicate some friction in the contribution process.
- **UI Feedback:** A support request ([#9562](https://github.com/zeroclaw-labs/zeroclaw/issues/9562)) highlights a basic UX annoyance where auto-scroll in WebChat prevents reading history during streaming.

## 8. Backlog Watch

Several important issues are waiting for maintainer review or have not received updates, requiring attention:

- **[RFC: Add cross-turn conversation correlation to OTel export (#8933)](https://github.com/zeroclaw-labs/zeroclaw/issues/8933)** - Open since July 10th, this high-priority observability RFC is tagged `needs-maintainer-review`.
- **[RFC: Realtime speech-to-speech channel for Gemini Live (#8780)](https://github.com/zeroclaw-labs/zeroclaw/issues/8780)** - This high-priority RFC has been open since July 6th without maintainer sign-off, despite being a significant potential feature.
- **[PR: fix(providers): remove unconditional strip_think_tags from compatible provider (#8927)](https://github.com/zeroclaw-labs/zeroclaw/pull/8927)** - This bug-fix PR created on July 10th is tagged `needs-maintainer-review` and has been waiting for over three weeks for a maintainer to act.
- **[Bug: cargo test --doc fails with duplicated rustdoc theme flag (#8847)](https://github.com/zeroclaw-labs/zeroclaw/issues/8847)** - While tagged `in-progress`, this CI issue has been open since July 8th, and a broken CI state for over three weeks is a significant stability concern for contributors.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*