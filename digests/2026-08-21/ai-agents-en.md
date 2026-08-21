# OpenClaw Ecosystem Digest 2026-08-21

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-21 00:32 UTC

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

# OpenClaw Project Digest
**Date: 2026-08-21**

---

## 1. Today's Overview

OpenClaw shows sustained high activity with 500 issues and 500 PRs updated in the last 24 hours, though no new releases were published. The project is in a heavy stabilization and hardening phase, with a significant portion of today's merged/closed work (151 PRs) focused on bug fixes across gateway reliability, memory management, session state integrity, and UI polish. The backlog shows a concerning accumulation of older, high-severity issues (P0/P1) that remain open with linked but unmerged fix PRs, suggesting a bottleneck in the maintainer review process. Community engagement remains strong, with several issues receiving double-digit comment counts and meaningful upvotes, indicating an active and vocal user base. Overall, the project is healthy but navigating a complex period of balancing new feature development (e.g., realtime Talk support, UI improvements) against a substantial debt of stability fixes.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

The project saw 151 PRs merged or closed today. Notable advancements and fixes include:

- **[#126897] fix(gateway): preserve incognito session visibility** — Fixes inconsistent incognito-session visibility for non-admin Gateway users when a session is selected through aliases, routes, or task identifiers.
- **[#116489] feat(security): require acknowledgement for install policy warnings** — Introduction of a `security.installPolicy` `warn` return, requiring operators to acknowledge and review suspicious plugin/skill installs.
- **[#120900] feat(ui): review install policy warnings** — Companion UI feature for the CLI security acknowledgement, allowing admins to review and continue plugin installs from the Control UI (merged/closed today).
- **[#125471] fix(models): keep Claude CLI OAuth available in Control UI** — Resolves a case where valid Claude CLI OAuth could lose refresh ownership after a Gateway restart due to legacy auth profile entries.
- **[#126489] fix(memory): preserve provenance across dreaming** — Fixes a security-relevant issue where restricted/tainted session content could lose its requester provenance during memory capture and dreaming.
- **[#126786] fix(status): reconcile degraded secret diagnostics** — Improves correctness of `openclaw status` output regarding degraded secret owners and missing diagnostics.
- **[#126611] fix: custom reasoning models truncate tool-call JSON at default 8192 maxTokens** — Addresses truncation issues for custom `openai-completions` providers with reasoning models.

---

## 4. Community Hot Topics

The most active discussions highlight deep user concerns around cost, reliability, and provider-specific issues:

- **[#42475] [Feature]: Per-agent cost budget enforcement at the gateway level** (23 comments) — Users are seeking native, gateway-level enforcement of per-agent cost budgets (daily/monthly caps) to prevent runaway spend without external monitoring. This indicates a strong need for built-in cost governance and observability.
- **[#48788] feat: centralized filename encoding utility for multi-encoding Content-Disposition handling** (20 comments) — A user proposes an architectural fix for handling multiple filename encodings (Shift-JIS, EUC-KR, GB18030) across all channel adapters, following a prior fix for Feishu. The discussion centers on proper design over one-off patches.
- **[#125626] Release validation: v2026.8.1-beta.2** (17 comments) — The validation thread for the latest beta release is active, with testers using the worksheet to validate the upgrade path. This is a critical checkpoint for release stability.
- **[#108435] [P0] update to openclaw 2026.7.1: gateway fails to start** (14 comments) — A critical regression where the gateway fails to start with systemd, ollama, and manual launch methods. This is a release-blocking issue with high community engagement.
- **[#38327] [P1] "Cannot convert undefined or null to object" with google-vertex/gemini-3.1-pro-preview** (14 comments) — A regression in 2026.3.2 affecting Google Vertex AI users; any message causes the embedded agent to fail.

---

## 5. Bugs & Stability

Multiple stability issues were reported or remain active today, ranked by severity:

**Critical (P0):**
- **[#108435] Gateway fails to start after update to 2026.7.1** (crash-loop, regression) — The gateway fails to start across systemd, ollama, and manual launch. No fix PR linked. [Link](https://github.com/openclaw/openclaw/issues/108435)
- **[#48920] Live Docs are ahead of release** (ux-release-blocker) — The live docs feature `IsolatedSessions` is not in the latest stable release (2026.3.13), causing configuration errors. [Link](https://github.com/openclaw/openclaw/issues/48920)
- **[#119270] File tools strip a leading @ from destination paths** (data-loss, bulk-filed) — `write`, `edit`, and `apply_patch` can silently operate on the wrong file when a path contains a leading `@`, potentially overwriting or deleting unintended files. This is a dangerous data-loss bug. [Link](https://github.com/openclaw/openclaw/issues/119270)

**High (P1):**
- **[#126246] Telegram durable outbound deliveries stuck in send_attempt_started, lost on restart** (message-loss) — Newly reported; agent runs complete but replies are not delivered, and recovery on restart fails. [Link](https://github.com/openclaw/openclaw/issues/126246)
- **[#123273] Image attachments fail for named (non-default) agents** (message-loss) — A clear version-specific regression where only named agents reject image attachments. [Link](https://github.com/openclaw/openclaw/issues/123273)
- **[#125431] Codex restricted tool policy silently disables workspace AGENTS.md** (security, session-state) — A silent behavior change that can alter agent behavior. A fix PR exists: [#126891](https://github.com/openclaw/openclaw/pull/126891).
- **[#124284] Subagent spawn fails with vLLM openai-completions + thinking** (other) — Regression introduced in v2026.8.1-beta.2 due to a new stream wrapper interfering with vLLM. [Link](https://github.com/openclaw/openclaw/issues/124284)
- **[#92241] Gateway holds stale module import paths after update/rollback** (message-loss) — Inbound messages are silently dropped (`ERR_MODULE_NOT_FOUND`) after a version rollback. [Link](https://github.com/openclaw/openclaw/issues/92241)
- **[#114234] Usage-cost refresh lock is never releasable after restart reusing owner PID** (session-state) — Permanently freezes the cache in container environments. [Link](https://github.com/openclaw/openclaw/issues/114234)

**Moderate (P2):**
- **[#51976] Active-memory blocks replies and can overload multi-agent gateways** is covered by issue [#72015](https://github.com/openclaw/openclaw/issues/72015) (reliability, P1).
- **[#74378] CLI commands remain alive as node.exe processes on Windows** (other). [Link](https://github.com/openclaw/openclaw/issues/74378)
- **[#97616] Leaks unreaped hook/tool child processes causing zombie accumulation** (crash-loop). [Link](https://github.com/openclaw/openclaw/issues/97616)

---

## 6. Feature Requests & Roadmap Signals

Several feature requests signal strong user demand for capabilities likely to appear in upcoming versions:

- **[#42475] Per-agent cost budget enforcement** — The high comment count and use case suggest this is a top priority for operators. Expect gateway-level cost controls in an upcoming release. [Link](https://github.com/openclaw/openclaw/issues/42475)
- **[#125068] Session hovercards in the Control UI sidebar** (PR open) — This feature is already being implemented and shows a clear roadmap investment in UI/UX improvements. [Link](https://github.com/openclaw/openclaw/pull/125068)
- **[#68920] HTTP /v1/chat/completions TTFB reduction (lightContext/voice mode)** — The 10-15 second TTFB is a major blocker for real-time voice agents. This is a critical performance feature request with a clear use case. [Link](https://github.com/openclaw/openclaw/issues/68920)
- **[#45501] Configurable session startup message** — A small but impactful quality-of-life feature request to let users customize the startup prompt after `/new` or `/reset`. [Link](https://github.com/openclaw/openclaw/issues/45501)
- **[#71142] Configurable upload size limit for Control UI** — Simple but highly requested; likely to be a quick win in a future patch. [Link](https://github.com/openclaw/openclaw/issues/71142)

---

## 7. User Feedback Summary

User feedback in the last 24 hours reveals several recurring pain points:

- **Provider Integration Friction:** Significant frustration around specific providers. The Google Antigravity ban issue ([#44134](https://github.com/openclaw/openclaw/issues/44134)) is a serious case where tool schema reloading triggered a false-positive anti-abuse ban. DeepSeek V4 Flash incomplete turns ([#88657](https://github.com/openclaw/openclaw/issues/88657)) and Claude CLI OAuth refresh dead-ends ([#83598](https://github.com/openclaw/openclaw/issues/83598)) further indicate a need for more robust provider-specific handling.
- **Silent Failures & Data Integrity:** Issues like the file tool `@` stripping ([#119270](https://github.com/openclaw/openclaw/issues/119270)), memory `index metadata is missing` ([#90361](https://github.com/openclaw/openclaw/issues/90361)), and silent message drops ([#124284](https://github.com/openclaw/openclaw/issues/124284)) cause distrust and lost work. Users are deeply concerned about these silent failures that don't produce clear errors.
- **Upgrade/Rollback Reliability:** Multiple issues ([#108435](https://github.com/openclaw/openclaw/issues/108435), [#92241](https://github.com/openclaw/openclaw/issues/92241), [#90378](https://github.com/openclaw/openclaw/issues/90378)) highlight that upgrades and rollbacks are not smooth. Silent migrations (e.g., cron store JSON to SQLite) and stale module paths are creating downtime and confusion.
- **Cross-Platform Consistency:** Windows-specific issues (process leaks [#74378](https://github.com/openclaw/openclaw/issues/74378), vitest teardown EBUSY [#119796](https://github.com/openclaw/openclaw/issues/119796)) and macOS issues (NVM node warning [#60612](https://github.com/openclaw/openclaw/issues/60612)) show users expect equal polish across all supported platforms.
- **Positive Signals:** Users are actively building and testing with the beta ([#125626](https://github.com/openclaw/openclaw/issues/125626)), indicating a strong community willing to validate releases. Several users have also contributed high-quality, well-researched issue reports with root cause analyses, demonstrating a sophisticated user base.

---

## 8. Backlog Watch

Several long-standing, important issues and PRs require maintainer attention:

- **[#53747] [P1] Memory management is in chaos** (created 2026-03-12) — A regression issue with varying memory behavior across users, still awaiting maintainer decision/patch. This has been open for 5 months with 11 comments. [Link](https://github.com/openclaw/openclaw/issues/43747)
- **[#72015] [P1] Active-memory blocks replies and QMD boot initialization overload** (created 2026-04-26) — A serious reliability issue with the official `active-memory` plugin, still open with a linked PR. [Link](https://github.com/openclaw/openclaw/issues/72015)
- **[#49728] [P0] [Bug]: Live Docs are ahead of release** (created 2026-03-17) — A release-blocking doc-vs-code drift that has been open for 5 months, indicating a process gap in keeping docs in sync with releases. [Link](https://github.com/openclaw/openclaw/issues/48920)
- **[#126246] [P1] Newly reported Telegram durable outbound delivery loss** — Needs immediate triage and reproduction. [Link](https://github.com/openclaw/openclaw/issues/126246)
- **PRs Stuck in Review:** Several PRs with `proof: sufficient` are still `status: 👀 ready for maintainer look`, including **[#126489] fix(memory): preserve provenance across dreaming** and **[#126887] fix(release): isolate plugin security scanning**. These appear to be high-value, well-tested changes that need maintainer time to merge.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-21 | **Scope:** 12 Projects in the Personal AI Assistant / Agent Space

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is experiencing **high-velocity maturation**, with leading projects prioritizing stability hardening and security remediation over new feature velocity. The ecosystem has bifurcated into two distinct camps: **full-featured gateway/platform projects** (OpenClaw, Hermes Agent, ZeroClaw) focusing on production-grade reliability, and **specialized/lightweight alternatives** (NanoBot, PicoClaw, NanoClaw) optimizing for specific niches like enterprise cloud providers and embedded environments. Cross-cutting themes include: per-agent cost governance, Windows platform parity, provider resilience (especially around streaming and OAuth), and architectural shifts toward plugin-based extensibility and persistent sandboxes. Community engagement remains strong across all projects, with sophisticated users filing precise, root-caused bug reports and contributing high-quality fixes.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed (24h) | Release Status | Health Score* |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 151 | No new release; beta validation active | ⭐⭐⭐⭐ (0.80) |
| **NanoBot** | 5 | 29 | 12 | No new release; pre-RC | ⭐⭐⭐⭐ (0.75) |
| **Hermes Agent** | 50 | 50 | 10 | No new release; consolidation phase | ⭐⭐⭐⭐ (0.78) |
| **PicoClaw** | 3 | 8 | 3 | No new release; v0.3.1 latest | ⭐⭐⭐ (0.65) |
| **NanoClaw** | 3 | 50 | 15 | No new release; RC being assembled | ⭐⭐⭐⭐ (0.72) |
| **NullClaw** | — | — | — | No activity | — |
| **IronClaw** | 22 | 35 | 7 | No new release; v1.4.0 milestones | ⭐⭐⭐⭐ (0.76) |
| **LobsterAI** | 2 | 7 | 6 | No new release | ⭐⭐⭐ (0.62) |
| **TinyClaw** | — | — | — | No activity | — |
| **Moltis** | 1 | 8 | 4 | **20260820.01** published | ⭐⭐⭐⭐ (0.82) |
| **CoPaw** | 28 | 50 | 28 | **v2.1.1-beta.1** published | ⭐⭐⭐⭐⭐ (0.85) |
| **ZeroClaw** | 50 | 50 | 2 | No new release; heavy RFC phase | ⭐⭐⭐ (0.60) |
| **ZeptoClaw** | — | — | — | No activity | — |

*\*Health Score = composite of merge efficiency, issue response time, backlog severity, and community engagement. Scale 0–1.*

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**

| Dimension | OpenClaw Advantage | Peer Comparison |
|---|---|---|
| **Scale & Community** | 500 issues + 500 PRs in 24h — 10–100x higher than peers | CoPaw (28/50) and ZeroClaw (50/50) are closest; most others are <10 |
| **Maturity** | 151 PRs merged/closed in 24h — clear stabilization focus | Only CoPaw (28) approaches this throughput |
| **Feature Depth** | Real-time Talk support, incognito sessions, policy acknowledgment workflows | Only ZeroClaw's realtime RFC shows comparable ambition |
| **Ecosystem Gravity** | Attracts high-quality, root-caused bug reports with linked fix PRs | Hermes Agent and IronClaw show similar depth but less volume |

**Technical Approach Differences:**

- **Gateway architecture:** OpenClaw treats the gateway as a first-class, multi-user, role-aware component (incognito visibility, policy acknowledgments). Most peers (NanoBot, PicoClaw) have simpler single-user gateway models.
- **Security posture:** OpenClaw's `security.installPolicy` `warn` return and provenance preservation across memory capture represent a more enterprise-ready security model than most peers.
- **Provider breadth:** OpenClaw's provider-agnostic design handles Claude CLI OAuth, custom `openai-completions` providers, and reasoning-model quirks — peers like Hermes Agent (OpenAI-specific tokens) are narrower.

**Community Size Comparison (by activity signal):**

| Tier | Projects |
|---|---|
| **5,000+ daily interactions** | OpenClaw (1,000 issues/PRs touched) |
| **500–1,000 daily interactions** | CoPaw (78), ZeroClaw (100), Hermes Agent (100) |
| **<100 daily interactions** | NanoBot (34), IronClaw (57), Moltis (9), PicoClaw (11), LobsterAI (9), NanoClaw (53) |

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|---|---|---|
| **Windows Platform Parity** | OpenClaw (#74378), Hermes Agent (#91079), Moltis (#468), CoPaw (#6974) | Process leaks, destructive updates, shell hook compatibility, VPN interference |
| **Provider Resilience & OAuth** | OpenClaw (#125471), NanoBot (#5444, #5454), Hermes Agent (#65346, #91164) | Docker OAuth redirect, streaming retry on `server_error`, token refresh persists, deprecated cache parameters |
| **Per-Agent Cost Governance** | OpenClaw (#42475), CoPaw (#6436), NanoClaw (#3270) | Gateway-level budgets, model routing, token usage telemetry |
| **Memory & Context Integrity** | OpenClaw (#53747, #126489), NanoBot (#5379), CoPaw (#7168), ZeroClaw (#6850) | Provenance preservation, history.db ballooning, lifecycle decoupling, consolidation correctness |
| **Upgrade/Rollback Reliability** | OpenClaw (#108435), Hermes Agent (#86443), ZeroClaw (#9578) | Transactional updates, stale module paths, doc-vs-code drift, stale-candidate false-closures |
| **Plugin/Extensibility Architecture** | OpenClaw (install policy), ZeroClaw (WASM plugins), CoPaw (marketplace unification), NanoClaw (skill audit) | Runtime ownership, scoped secrets, coherent config seams, "everything is a plugin" |
| **Real-Time/Voice Interaction** | OpenClaw (#68920), ZeroClaw (#8780), CoPaw (#7163) | TTFB reduction, speech-to-speech channels, session-level thinking modes |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target Users | Architecture Differentiator |
|---|---|---|---|
| **OpenClaw** | Full-featured gateway, multi-channel, enterprise-ready | Operators, power users, teams | Multi-user gateway, rich UI/CLI, provider-agnostic |
| **NanoBot** | Lightweight Python agent, broad provider coverage | Developers, automated pipelines | Python-first (agnostic), ChannelManager, TUI |
| **Hermes Agent** | Desktop-first companion, deep OpenAI/Anthropic support | Individual power users, macOS/Windows | Desktop client, session persistence, cron attestation |
| **PicoClaw** | Embedded/edge agent, Go-based | IoT, resource-constrained | Go implementation, Anthropic-native protocol, multi-agent Blackboard |
| **NanoClaw** | Community-skill-driven assistant | Channel integrators, multi-install users | 12+ community skills, skill audit culture, install-slug scoping |
| **IronClaw** | Enterprise agent platform, Rust-based | Enterprises, multi-user teams | Rust core, per-user persistent sandbox, agent lifecycle hooks, design system |
| **LobsterAI** | Chinese-market desktop companion | Chinese-speaking users | OpenClaw engine overlay, WeChat-integrated, file preview |
| **Moltis** | Security-hardened communication agent | Production WhatsApp users, security-literate | CWE-306 fixes, calver releases, configurable tool ceilings |
| **CoPaw** | Qwen-ecosystem agent, full console | Qwen users, Chinese market | QwenPaw Hub (self-hosted multi-user), session-level thinking modes |
| **ZeroClaw** | Architecture-forward multi-agent platform | Early adopters, architects | WASM plugin architecture, RFC-driven development, granular sandbox policy |

---

## 6. Community Momentum & Maturity

| Tier | Projects | Characterization |
|---|---|---|
| **Rapid Iteration (RC-forming)** | OpenClaw, CoPaw, NanoClaw | High merge rates, beta validation active, stacked feature PRs awaiting merge; risk of review-backlog accumulation |
| **Stabilization Phase** | Hermes Agent, IronClaw | Bug-fix concentrated, no releases cut; consolidating large fix bodies before stable releases |
| **Steady-State Maintenance** | NanoBot, Moltis, PicoClaw, LobsterAI | Moderate throughput, security hardening, slow-but-steady feature delivery; Moltis most efficient per-interaction |
| **Stalled / Inactive** | NullClaw, TinyClaw, ZeptoClaw | No 24h activity — likely unmaintained or in hibernation |
| **Architecture-Heavy (Releases Gated)** | ZeroClaw | High activity but 48/50 PRs open — RFC decisions block progress; long-term payoff likely |

---

## 7. Trend Signals for AI Agent Developers

1. **Governance Is the New Frontier:** OpenClaw (#42475) and CoPaw (#6436) both show users demanding **per-agent cost budgets and model routing**. Agent developers should build cost-observability into every layer — not just SDKs but also platform-gateway enforcement.

2. **Windows-Is-Back:** A cluster of Windows-specific bugs (OpenClaw #74378, Hermes #86443, Moltis #468) shows significant desktop-agent adoption on Windows. Cross-platform CI and transactional updaters are **table stakes**, not nice-to-haves.

3. **Streaming Reliability > Raw Speed:** NanoBot (#5454) and OpenClaw (#126611) both reveal nuanced streaming failure modes (mid-stream retries, token truncation). Solutions that don't handle edge-case streaming will lose trust in automated pipelines.

4. **The Plugin Wars Have Begun:** ZeroClaw's WASM plugins, CoPaw's marketplace unification, and NanoClaw's skill audit all point toward **pluggable everything** as the architectural ideal. Developers should avoid hard-coding channels/providers; design for seam-based extensibility.

5. **Persistence Is a Feature:** The persistent sandbox (IronClaw), durable outbound deliveries (OpenClaw), and execution attestation (Hermes) signal a shift from stateless tool-calling toward **stateful, auditable agent workflows** — critical for enterprise adoption.

6. **Context Is the New P0:** Memory provenance (OpenClaw #126489), history.db explosion (CoPaw #7168), and memory lifecycle decoupling (ZeroClaw #6850) all point to context management as the **#1 reliability risk** for long-running agents. Expect memory infrastructure to become a competitive battleground.

7. **Real-Time Voice Is on the Horizon:** OpenClaw, ZeroClaw, and CoPaw all have realtime/voice initiatives. The 10–15s TTFB problem (OpenClaw #68920) is the universal blocker — solving it will unlock voice-first agent experiences.

8. **Community Quality Is Rising:** A consistent pattern of sophisticated bug reports (root-caused, with fix PRs) across OpenClaw, Hermes, and CoPaw indicates the user base is increasingly **developer-grade**. Founders should invest in public roadmaps and RFC processes to harness this energy productively.

---

*Report compiled from 12 project community digests dated 2026-08-21.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-21

## 1. Today's Overview

NanoBot is in a period of high development velocity with 29 PRs updated in the last 24 hours, including 12 merged or closed and 17 still open. Issue activity is moderate (5 updated) with 3 open bugs and 2 closed items. No new releases were published today, but the volume of merged work signals a feature-rich cycle approaching a release candidate. Notable focus areas include provider reliability, channel-level error handling (Matrix, Slack, Telegram), agent lifecycle management, and WebUI polish. The project appears healthy with strong contributor engagement across multiple domains, although several long-running PRs carry `conflict` labels indicating merge friction.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

**12 PRs were merged or closed today.** Key completed work includes:

- **[#5452 — feat(tui): print resume command on exit](https://github.com/HKUDS/nanobot/pull/5452)** *(merged)* — Adds a ready-to-run `nanobot agent --session websocket:<id>` command when the TUI exits, a quality-of-life improvement for session resumption. Includes renderer tests and Windows/POSIX smoke coverage.
- **[#5240 — refactor(webui): unify floating controls](https://github.com/HKUDS/nanobot/pull/5240)** *(merged)* — Centralizes floating-surface styling and standardizes Menu, Popover, and Combobox semantics in the WebUI, reducing visual inconsistency.
- **[#1203 — fix(cli): workaround 'Event loop is closed' on linux](https://github.com/HKUDS/nanobot/pull/1203)** *(closed)* — A workaround for the recurring `RuntimeError: Event loop is closed` on Linux (Python 3.11) shutdown.
- **[#5447 — Paid security-scan MCP integration](https://github.com/HKUDS/nanobot/issues/5447)** *(closed)* — This request was closed, indicating the maintainers declined or the author withdrew the paid MCP/x402 Solana integration.
- **[#5425 — Support legacy socks:// proxy URLs](https://github.com/HKUDS/nanobot/issues/5425)** *(closed)* — Bug closed, likely fixed by existing provider proxy resolution logic.

**Open PRs showing meaningful advancement today:**

- **[#5455 — fix(provider): retry Codex server_error](https://github.com/HKUDS/nanobot/pull/5455)** — Adds `"server_error"` to transient-error markers; directly addresses open bug #5454.
- **[#5457 — fix(channels): scope dispatcher exception boundary](https://github.com/HKUDS/nanobot/pull/5457)** — Prevents a single outbound message failure from killing the entire background dispatch task.
- **[#5387 — feat(telegram): support reusable sticker replies](https://github.com/HKUDS/nanobot/pull/5387)** — Advanced with new commits, exposing sticker metadata and reply routing.
- **[#5431 / #5430 — agent background task fixes](https://github.com/HKUDS/nanobot/pull/5431)** — Two complementary fixes from `yu-xin-c`: proper failure logging and memory/leak cleanup for task groups.

## 4. Community Hot Topics

The most active discussions this cycle are primarily **bug reports around reliability**, not feature debates:

- **[#5454 — Streaming retry: mid-stream `server_error` skips retry](https://github.com/HKUDS/nanobot/issues/5454)** *(new, open)* — A precise bug report: Codex `response.failed` events do not trigger the transient-error retry once content has streamed. A fix PR (#5455) was opened the same day, indicating fast maintainer attention.
- **[#5444 — Failed OpenAI OAuth login in Docker](https://github.com/HKUDS/nanobot/issues/5444)** *(open, 1 comment)* — A user cannot complete OAuth flow inside Docker — redirect URL localhost mapping fails. This is a blocker for containerized deployments.
- **[#5459 — Native Google Vertex AI provider for Claude](https://github.com/HKUDS/nanobot/issues/5459)** *(new, open)* — Feature request with a clear rationale: Vertex AI is increasingly the standard enterprise path for Claude models. No comments yet, but high adoption potential.
- **[#5425 — `socks://` proxy alias unsupported](https://github.com/HKUDS/nanobot/issues/5425)** — Closed after resolution, but the underlying need for broad proxy-URL compatibility remains relevant for self-hosted users.

**Underlying needs:** Users want (a) enterprise-grade model access (Vertex AI), (b) bulletproof Docker operation, and (c) resilient streaming behavior under transient provider failures.

## 5. Bugs & Stability

Ranked by severity:

1. **HIGH — [#5444: OAuth login fails in Docker](https://github.com/HKUDS/nanobot/issues/5444)** — Blocks full NanoBot usage for Docker-based deployments. No fix PR yet. Needs maintainer response.
2. **MEDIUM — [#5454: Streaming mid-stream `server_error` skips retry](https://github.com/HKUDS/nanobot/issues/5454)** — Causes silent failed turns in Codex streaming. **Fix PR #5455 exists and targets the pre-stream case; a follow-up may be needed for the mid-stream case.**
3. **MEDIUM — [#5457 (PR): Dispatcher exception kills outbound delivery](https://github.com/HKUDS/nanobot/pull/5457)** — An unexpected error while processing one outbound message stops all future messages until process restart. Fix PR is open.
4. **LOW — [#5458 (PR): Matrix error logs missing context](https://github.com/HKUDS/nanobot/pull/5458)** — Loguru format mismatch (`%s` vs `{}`) hides filenames/room IDs/chat IDs in three Matrix failure paths, hampering diagnostics.
5. **LOW — [#5425: `socks://` proxy alias unsupported](https://github.com/HKUDS/nanobot/issues/5425)** — Closed; users must use `socks5://` explicitly, a minor configuration friction.

**Other stability PRs open (not yet merged):** Slack file-download redirect validation (#5414), provider fallback policy on raised exceptions (#5413), gateway log flushing (#5412), WebUI discarded-chat race (#5339), MCP OAuth credential preservation (#5338).

## 6. Feature Requests & Roadmap Signals

Two strong roadmap signals this cycle:

1. **[#5459 — Native Google Vertex AI provider](https://github.com/HKUDS/nanobot/issues/5459)** — This is the most strategically significant request. NanoBot already supports Bedrock, Copilot, and xAI; Vertex AI is the missing enterprise cloud piece. Given the project's pattern of rapid provider adoption (SenseNova PR also open), **a Vertex AI provider is plausible in the next minor release (v0.4 or v0.5)** — likely via the OpenAI-compatible endpoint first, with a native implementation later.
2. **[#5453 — SenseNova (商汤日日新) provider (PR open)](https://github.com/HKUDS/nanobot/pull/5453)** — Adds SenseNova models (`sensenova-6.8-flash-lite`, `deepseek-v4-flash`, `glm-5.2`). This signals the project's continued expansion into Chinese LLM ecosystems, complementing its existing global provider coverage.
3. **[#5387 — Telegram reusable sticker replies (PR open)](https://github.com/HKUDS/nanobot/pull/5387)** — Adds sticker awareness to the Telegram channel, closing a UX gap for a common chat pattern.

## 7. User Feedback Summary

- **Docker pain is real and recurrent** (#5444). OAuth redirect-URL handling in containers is a common failure across self-hosted AI tools; NanoBot users expect it to "just work."
- **Reliability under provider instability is the #1 technical pain point** (#5454, #5413, #5457). Users depend on NanoBot in automated pipelines; silent mid-stream failures and background-task deaths undermine trust in unattended operation.
- **Enterprise cloud provider demand is rising** (#5459). The request explicitly frames Vertex AI as the standard for Anthropic models at scale.
- **Proxy compatibility (socks://)** remains a friction point for users behind corporate or legacy networking — even closed, it indicates the user base runs in heterogeneous network environments.
- **Positive signal:** the TUI resume-command feature (#5452) was merged quickly, and users continue to submit polished, well-scoped PRs (Matrix logging fix, provider retries), suggesting a contributor-friendly project culture.

## 8. Backlog Watch

Items needing maintainer attention:

1. **[#5179 — Migrate MCP integration to SDK v2 (priority: p1, conflict)](https://github.com/HKUDS/nanobot/pull/5179)** — Open since 2026-07-30 (3+ weeks), flagged with a merge conflict and labeled priority p1. This is a large, strategic refactor with a competing draft (#5180). The longer it lingers, the more likely stacked MCP-related PRs (#5338) will accumulate merge friction. Maintainers should resolve the conflict or declare a decision between #5179 and #5180.
2. **[#5180 — Minimal MCP SDK v2 migration (draft, conflict)](https://github.com/HKUDS/nanobot/pull/5180)** — The evaluation branch for the SDK v2 migration. It exists to inform a decision that has not yet been made public. Needs a maintainer verdict.
3. **[#5379 — fix(memory): preserve full consolidation input (conflict)](https://github.com/HKUDS/nanobot/pull/5379)** — Open for 8 days with a conflict label. Memory consolidation correctness is important for long-running agent sessions; a stalled fix risks data loss in edge cases.
4. **[#5338 — fix(mcp): preserve credentials when OAuth store read fails](https://github.com/HKUDS/nanobot/pull/5338)** — Open 9+ days; security-adjacent correctness fix (credential overwrite risk). This one should be prioritized for review.
5. **[#5444 — OAuth login fails in Docker](https://github.com/HKUDS/nanobot/issues/5444)** — High-severity bug with no maintainer response yet. First response should be acknowledgment and triage within 24 hours given its user impact.

**Overall health assessment:** NanoBot is a well-maintained project with a responsive contributor base. The volume of quality PRs across channels, providers, and infrastructure suggests strong community health. The main risks are the MCP SDK migration decision and the accumulation of `conflict`-flagged PRs. A release in the coming weeks incorporating today's merged features (TUI resume, WebUI controls, ChannelManager fix) would lock in this progress.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for 2026-08-21.

---

# Hermes Agent Project Digest - 2026-08-21

## 1. Today's Overview

Hermes Agent is in a **high-velocity stabilization phase**, with maintainers and community contributors focused heavily on the reliability of the Windows Desktop client, session state persistence, and provider-level compatibility. The project is extremely active, with exactly **50 issues** and **50 PRs** updated in the last 24 hours, indicating a strong, healthy community and responsive maintainers. While there are no new releases today, the sheer volume of activity centers on resolving a cluster of P0/P1 bugs reported by users, particularly around the update/install process. The lack of new releases suggests the team is consolidating a large body of fixes before a significant stable release.

## 2. Releases

No new releases were published for this date.

## 3. Project Progress

While no PRs were merged today, ten issues/PRs were closed, signaling the resolution of several community-submitted fixes. Key activity includes the closure of a duplicate PR for the Kanban blocked status bug and the closure of a PR addressing a provider context-window mismatch for the `zai` provider.

Several open PRs are making significant progress, indicating features and fixes on the horizon:

- **Windows Desktop Stability:** PR #91079 (`fix(desktop): make Windows package rebuild transactional and self-healing`) is a major effort to address the destructive update bugs reported in #44225 and #90829. This is a high-priority fix aiming to prevent data loss and bricked applications.
- **Core Agent Fixes:** PRs #90734 (`fix(state): unlocked reads on the shared SessionDB writer connection...`) and #85065 (`fix(state): retry 'returned NULL without setting an exception'...`) are targeting the P1 session persistence failures, directly addressing the `state.db` corruption reports.
- **User Experience:** PR #91160 (`fix(desktop): preserve commas while editing list settings`) and PR #91172 (`fix(desktop): stabilize external-store runtime adapter`) are focused on fixing UI glitches. PR #91181 (`fix(agent): streamed refusals no longer vanish into empty-response retries`) improves error handling for model refusals.
- **New Features:** PR #91174 (`feat(cron): add execution and delivery attestation`) introduces provable execution logs for cron jobs, a significant feature for trust and debugging. PR #90973 (`feat(gateway): let identity plugins authorize resolved users`) is an architectural improvement for security boundaries.

## 4. Community Hot Topics

The most active discussions highlight critical reliability and scalability concerns:

- **[#66616 Skills index is stale or degraded (degraded)](https://github.com/NousResearch/hermes-agent/issues/66616)**: With 66 comments, this automated freshness probe failure is the hottest topic. The index is 29.8 hours old, indicating a broken or flaky CI/CD pipeline for documentation. The user interest here is for a reliable documentation and skills hub, and the underlying need is for operational robustness in the project's own infrastructure.

- **[#87093 Debian installation broken](https://github.com/NousResearch/hermes-agent/issues/87093)**: With 14 comments, this P1 issue details a complete installation failure on Debian. The community is actively discussing workarounds, and the underlying need is for a bulletproof `curl | bash` install process across all major Linux distributions.

- **[#75801 OpenCode Go gpt-5.6-luna omits finish_reason](https://github.com/NousResearch/hermes-agent/issues/75801)**: This 7-comment issue details a tricky bug where a model's clean stream end is misinterpreted as a network failure, leading to artificial retries and a confusing user experience. The community is interested in robust handling of non-standard model behaviors.

- **[#90971 apply_anthropic_cache_control is not idempotent](https://github.com/NousResearch/hermes-agent/issues/90971)**: A P0 bug that initially worried about prompt-caching failures. The community self-investigated and corrected the report, proving the original overflow scenarios were unreachable. This is a great example of the community and maintainers working together to disprove false positives and focus on the real issue.

## 5. Bugs & Stability

This is the dominant topic today, with several high-severity issues surfacing.

**P0 (Critical):**
- **[#90971: Anthropic Cache Control issue](https://github.com/NousResearch/hermes-agent/issues/90971)**: Initially reported as a P0, but proven to be a non-issue for the described scenarios. The community is still analyzing the edges.
- **[#91164: gpt-5.6 prompt_cache_retention causes 400 invalid_parameter](https://github.com/NousResearch/hermes-agent/issues/91164)**: A real P0 where turns die due to a deprecated prompt-caching parameter for OpenAI's gpt-5.6 family. This requires a migration to `prompt_cache_options.ttl`.

**P1 (High):**
- **[#85079: `returned NULL without setting an exception` on WAL append](https://github.com/NousResearch/hermes-agent/issues/85079)**: Causes hard-fail turns under concurrent writes. A fix PR (#85065) is open.
- **[#86443: `hermes update` deletes Desktop app after failed rebuild](https://github.com/NousResearch/hermes-agent/issues/86443)**: A destructive bug on Windows that leaves no `Hermes.exe` after a failed update. PR #91079 aims to fix this.
- **[#89293: Repeated state.db corruption](https://github.com/NousResearch/hermes-agent/issues/89293)**: A user reports 3 incidents in 8 days of `state.db` corruption, pointing to a systemic lock-storm and SQLite journal-mode issue. PR #90734 targets the root cause.
- **[#90734: Unlocked reads on shared SessionDB writer connection](https://github.com/NousResearch/hermes-agent/pull/90734)**: This open PR directly fixes a concurrency bug that destroys live turns.

**P2 (Medium):**
- Multiple Windows-specific issues around the build/update process, including **#90134** (blockmap.js issue), **#90237** (breaks Windows Snap/FancyZones), **#90829** (fail-closed gate on rebuild), and **#90906** (Python not updating). These are all disruptive for Windows users, and PR #91079 is the central fix.

## 6. Feature Requests & Roadmap Signals

Despite the bug-fixing focus, new features are being requested and developed.

- **Feature: Cron Job Attestation (PR #91174)**: This is a strong signal of the roadmap's direction toward enterprise-grade reliability. By providing "execution and delivery attestation," Hermes is adding provable, auditable logs for automated tasks, which is crucial for trust in agentic workflows.
- **Feature: Indefinite Peer Timeouts for A2A (PR #91171)**: This small fix addresses a real need for agent-to-agent communication, allowing for long-running peer tasks without arbitrary socket timeouts.
- **Feature: Preview Pane for Remote Backends (Issue #91149)**: Users want local dev servers routed through the harness when connected to a remote/SSH backend. This is a UX enhancement for desktop users.
- **Feature: Spanish (es) Locale (PR #91173)**: The community is actively extending the desktop app to non-English users. The PR was closed as a duplicate, suggesting there may be a larger localization effort in progress.

## 7. User Feedback Summary

The user feedback today is a mix of frustration from critical stability issues and appreciation for the project's overall capability.

- **High Frustration with Windows Updates:** The cluster of bugs around `hermes update` destroying the Desktop app is the primary pain point. Users like `ameniki` (#86443) are left with a completely broken installation. The demand for a transactional, self-healing update process is loud and clear.
- **Frustration with Installation and Setup:** Users are hitting walls even before they can use the agent. The Debian install failure (#87093), the stall on downloading Chrome (#90932), and the npm incompatibility on Windows are major barriers to entry.
- **Deep Trust in Advanced Features:** The fact that a user relies on Hermes for a 6TB data migration (#90929) shows a high level of trust and indicates the tool is used for serious, long-running tasks. This also means the "entire environment just spun down" bug is catastrophic for them.
- **Validator, Not Just User:** The community is highly technical and engaged. The self-correction of the P0 Anthropic bug (#90971) by multiple users is a strong sign of a healthy, collaborative ecosystem.

## 8. Backlog Watch

These items are long-standing and require maintainer attention:

- **[Issue #32678: GCP Vertex AI connection fails with 404 (2026-05-26)](https://github.com/NousResearch/hermes-agent/issues/32678)**: This is almost three months old with no recent maintainer activity. The bug blocks a major cloud provider integration, which could impact enterprise adoption.
- **[Issue #65346: OpenAI Codex OAuth token repeatedly invalidated (2026-07-16)](https://github.com/NousResearch/hermes-agent/issues/65346)**: This month-old P2 issue causes users to lose access to their paid OpenAI Codex provider every few days. The intermittent nature and lack of a definitive fix are concerning.
- **[PR #68499: fix(delegation): separate lifecycle from task outcome (2026-07-21)](https://github.com/NousResearch/hermes-agent/pull/68499)**: This month-old PR is a significant architectural fix for how delegated tasks are reported. It has multiple `sweeper` labels indicating it is considered a risk area. The fact that it is still open after a month, despite its importance, suggests it may be a complex review or blocked on other dependencies.
- **[Issue #66616: Skills index is stale or degraded (2026-07-18)](https://github.com/NousResearch/hermes-agent/issues/66616)**: While heavily commented, the final step to fix the broken automation pipeline appears to be lacking. This internal infrastructure problem degrades the user experience on the docs site.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-21

## Today's Overview

PicoClaw is showing moderate activity with 3 open issues and 8 PRs updated in the last 24 hours. The project is in a **steady-state maintenance phase**, with no new releases, a mix of dependency bumps (4 dependabot PRs), and 3 closed PRs advancing protocol support and multi-agent capabilities. Community engagement is focused on two areas: **performance degradation in the Web UI with long chat histories** (#3281, the most-discussed issue with 6 comments) and **extensibility of ASR and subagent tooling** (#3331, #3330). Notably, two long-running feature PRs — the Anthropic native Messages API protocol (#1158) and the multi-agent collaboration framework (#423) — were merged, signaling meaningful architectural progress despite the quiet release calendar. The stale label on several items suggests maintainer bandwidth may be a constraint.

## Releases

No new releases were published in the last 24 hours. The latest version remains **PicoClaw v0.3.1** (referenced in issue #3281).

## Project Progress

Three PRs were merged/closed in the last 24 hours:

- **[#1158 — feat: add anthropic-messages protocol for native Anthropic API format](https://github.com/sipeed/picoclaw/pull/1158)** *(merged)* — This is a significant compatibility addition. It introduces a new `anthropic-messages` protocol prefix that supports the Anthropic native Messages API format (`/v1/messages` endpoint). This resolves issue #269, enabling PicoClaw to work with Anthropic-compatible proxy services that *only* support the native API format (not the OpenAI-compatible format). This broadens PicoClaw's provider ecosystem considerably.
- **[#423 — feat: base multi-agent collaboration framework & shared context](https://github.com/sipeed/picoclaw/pull/423)** *(merged)* — A foundational advancement: a thread-safe **Blackboard** for shared context pooling across agents, plus agent handoff and discovery tools. This builds on previously merged PRs #213 (provider protocol refactor) and #131 (model fallback chain + multi-agent routing). This solidifies PicoClaw's multi-agent architecture as a core feature.
- **[#3318 — fix(web): repair unparseable pnpm-lock.yaml](https://github.com/sipeed/picoclaw/pull/3318)** *(merged)* — A maintenance fix resolving a duplicated YAML mapping key (`semver@7.8.5` listed twice under `packages:` and `snapshots:`) that was breaking pnpm lockfile parsing in the web frontend. This unblocks web development workflow.

## Community Hot Topics

- **[#3281 — [BUG] Web UI chat input is very laggy when history is a little long](https://github.com/sipeed/picoclaw/issues/3281)** — **Most active issue** (6 comments, 1👍, stale). Users report significant input lag in the Web UI as chat history grows within a single session. This is the highest-signal usability complaint currently tracked. Underlying need: **performance optimization for the chat frontend** — likely re-rendering of long DOM histories or inefficient state updates.
- **[#3331 — Feature: Use any models with /audio/transcriptions endpoint](https://github.com/sipeed/picoclaw/issues/3331)** — Users want to use modern ASR models (e.g., newer non-whisper or faster whisper variants) instead of being locked to the legacy `*-whisper-*` pattern. Suggests a model-config flag (e.g., `whisper-transcription: true`) to explicitly force the whisper path. Underlying need: **flexibility and performance in ASR model selection**.
- **[#3330 — Feature: Support dynamic model override in delegate/spawn/subagent tools](https://github.com/sipeed/picoclaw/issues/3330)** — Users want to select a model *at call time* for `delegate`, `spawn`, and `subagent` tools, rather than being constrained to static per-agent configuration. Underlying need: **runtime flexibility for heterogeneous model routing**, particularly for cost/quality trade-offs per task.

*Commentary:* The merging of #423 (multi-agent framework) makes #3330 (dynamic model override within subagents) a natural, highly-relevant follow-up. Expect this to gain traction.

## Bugs & Stability

*One bug reported, moderate severity:*

1. **[#3281 — Web UI input lag with long chat history](https://github.com/sipeed/picoclaw/issues/3281)** — **Medium severity (UX)**: The core user-facing interface degrades noticeably in long sessions. Reproduced with PicoClaw v0.3.1 on Go 1.25.11. **No fix PR exists yet.** The stale label indicates it has not seen maintainer action in 30 days. Given the age, this is a **persistent pain point** that should be prioritized.

No crashes, data loss issues, or regressions were reported in the last 24 hours.

## Feature Requests & Roadmap Signals

*Three clear signals from the community:*

1. **ASR model flexibility (#3331)** — Removing the strict `*-whisper-*` model-name pattern for `/audio/transcriptions` endpoints. Probability of inclusion in next minor release: **High** — it is a small, well-scoped config change.
2. **Dynamic model override for subagent tooling (#3330)** — Making `delegate`/`spawn`/`subagent` accept a model parameter at runtime. Probability for next minor release: **Medium-High** — directly complements the just-merged multi-agent framework (#423).
3. **Anthropic-native API compatibility (#1158, already merged)** — While merged, watch for related ecosystem requests (e.g., supporting other native vendor formats like Gemini's `generateContent` or Bedrock's Converse API). The dependabot PRs for `aws-sdk-go-v2/service/bedrockruntime` (#3336) suggest **Bedrock integration remains actively maintained**.

## User Feedback Summary

- **Pain points**: The primary user complaint (by engagement) is the **Web UI performance degradation** — this will generate churn if unaddressed. Secondary friction: **restrictive ASR model naming** and **inflexible subagent model routing**. These two are moderate-loss annoyances for power users.
- **Use cases revealed**: Users are actively routing through **Anthropic-compatible proxies** (hence #1158's importance), leveraging **multi-agent workflows** with heterogeneous models, and using **voice/audio interactions** (ASR — likely voice chat use cases).
- **Satisfaction signals**: The merging of #1158 and #423 addresses long-standing feature gaps (tracking back to #269 and the multi-agent work), which is a positive signal for users awaiting these capabilities. There are no explicit negative UX complaints about core stability.

## Backlog Watch

*Items needing maintainer attention:*

- **[#3281 — Web UI lag (30 days old, stale, 6 comments)](https://github.com/sipeed/picoclaw/issues/3281)** — **High priority**: The most-commented issue; an active, persistent UX degradation. Maintainers should triage and ideally assign this to a frontend-focused contributor.
- **[#3331 — ASR model flexibility](https://github.com/sipeed/picoclaw/issues/3331)** & **[#3330 — Dynamic subagent models](https://github.com/sipeed/picoclaw/issues/3330)** — Both only 8 days old but already flagged stale; they originate from engaged power users. Respond to these with feasibility comments to keep momentum.
- **Dependency bot PRs (#3332–#3336)** — 5 dependabot PRs updated in the last 24h, all stamped stale. These cover Bedrock runtime, AWS config, Anthropic SDK, and Mautrix. Routine, but left unmerged they can accrue security debt; recommend a regular merge cadence.
- **Watch item**: **PR #423** (recently merged multi-agent framework) is marked as a *base* framework (WIP label on the original PR). Expect follow-up issues/PRs for agent discovery robustness, context pool memory management, and handoff error handling. Mentally prioritize these.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-21

## 1. Today's Overview

NanoClaw is in a period of **high-velocity stabilization and skill-hardening**. While issue volume remains modest (3 updated in 24h; 2 open), pull request activity is intense — **50 PRs updated, with 15 merged/closed** against core-channel infrastructure. The project is clearly executing a coordinated audit of its 12+ community skills (Slack, Dashboard, Ollama, macOS statusbar, etc.), fixing systemic bugs related to multi-install pathing, dead configuration surfaces, and container scoping. Two intertwined bugs in the router's `mention-sticky` engagement logic and WhatsApp attachment mounting are open and represent the most visible user-facing issues. No new releases were cut today; the project appears to be consolidating a large batch of fixes for a future stable release.

## 2. Releases

**No new releases** were published in the last 24 hours. The flurry of merged fixes — especially the "audit" series of PRs (e.g., #3414–#3420) — strongly suggests a **release candidate is being assembled**, likely gated on the open router bug (#3369) and the skill payload compatibility fix (#3401).

## 3. Project Progress

A **systematic skill audit** is the dominant theme. Core-team member **gavrielc** landed a stacked series of fixes (15 PRs closed today), each auditing a specific community skill for real-world viability:

- **[Closed] #3421** — Docs/setup: announce one-click Slack agents (stacked on the `/add-slack` flip).
- **[Closed] #1311** — Feature: create new session (long-dormant PR finally merged).
- **[Closed] PRs #3414–#3420** — Fixes for `add-clidash`, `add-atomic-chat-tool`, `add-ollama-tool`, `add-dashboard`, `add-tavily-tool`, `add-anydoc`, and `add-macos-statusbar`. Key patterns corrected:
    - **Install-scoped `ncl`** — bare `ncl` calls now resolve to the correct install's DB/groups via `install-slug`, fixing multi-install conflicts.
    - **Per-group MCP config seams** — tools like Ollama and Atomic Chat previously read dead `process.env` values; config now lives in the per-group `container_configs` seam.
    - **Self-defeating UIs** — `add-clidash` was fanning out ~29 concurrent `bin/ncl` refreshes with a 10s timeout; now capped and payload-tested (tests grew 87→102).
    - **Honest smoke tests** — `add-tavily-tool` silently no-oped without running containers; now surfaces a real signal.

**Provider support is expanding**: PRs #3355 and #3356 (open) add a Cursor Agent SDK payload and `/add-cursor` setup skill, indicating marketplace-style provider growth beyond OpenAI/Anthropic.

## 4. Community Hot Topics

The most active discussions center on **engagement-mode semantics and channel attachment routing**:

- **[Issue #2715 — Inbound WhatsApp media unreachable](https://github.com/nanocoai/nanoclaw/issues/2715)** — Files save to an unmounted `DATA_DIR/attachments` dir; the agent gets a phantom `/workspace/attachments/...` path. This is a **critical, long-running bug (opened June 8)** with only 1 comment — it silently blocks a whole class of WhatsApp use-cases (document/audio QA). A fix PR (#3401) keeps skill payloads compatible with main, but the underlying mount issue may not be fully resolved.
- **[Issue #3369 — `mention-sticky` engages without mention](https://github.com/nanocoai/nanoclaw/issues/3369)** — `engage_mode: 'mention-sticky'` + `ignored_message_policy: 'accumulate'` causes the agent to start replying in threads where it was never mentioned. This is a **fresh, fundamental routing semantics bug** (opened Aug 20). A fix PR [#3422](https://github.com/nanocoai/nanoclaw/pull/3422) is already up, confirming the root cause is that "accumulate" creates the session row that becomes the subscription — the PR title literally reads "mention-sticky subscribes on a mention, not on a session".

The **PR review conversation** around #3422 and the audit series is where the real technical depth is; the issues section is comparatively quiet (0–1 comments each).

## 5. Bugs & Stability

Ranked by severity:

1. **[High] Issue #2715 — WhatsApp attachments unreachable** (open since June). Agent cannot see any inbound media files (images/docs/audio) due to a mount mismatch. Blocker for media-capable WhatsApp agents. Fix PR #3401 addresses payload compatibility but not explicitly the mount; **needs maintainer verification**.
2. **[High] Issue #3369 — `mention-sticky` phantom engagement** (open 1 day). At-worst produces spammy, unsolicited agent replies; at-best violates documented 'silent context' semantics. Fix PR #3422 is up — likely fast-tracked.
3. **[Medium] Issue #2606 — `engage_mode: 'always'` silently drops messages** (now closed). Root-caused to `evaluateEngage()` missing a switch case for `always`; dropped with `no_agent_engaged`. Closed today — presumably via the router refactor happening with #3422.
4. **[Medium] Malformed cron strings** — PR #3247 addresses `handleRecurrence` re-erroring every sweep tick instead of retiring the bad cron row. Prevents log-spam and repeated failed scheduling.
5. **[Medium] Node 22 / Matrix adapter** — PR #3403 fixes extensionless ESM imports failing under Node 22 by committing a pnpm patch (refresh-safe reapplication). A sign of ongoing Node 22 compatibility work.

## 6. Feature Requests & Roadmap Signals

- **[Cursor Agent SDK] — PRs #3355 & #3356 (open, core-team).** Provider-agnostic agent integration is clearly a roadmap item. Adding Cursor as a first-class provider signals the project's intent to be the "polyglot provider" layer.
- **[One-click Slack agents] — PR #3421 (closed).** The docs/announcement layer went in; the setup flip (#3404) is the underlying feature. This makes nano-to-production Slack agents consumer-grade.
- **[Token usage visibility] — PR #3270 (open, "Feat/ncl token usage").** User-facing cost telemetry is a recurring unmet need for any agent-infra project.
- **[`add-why` skill] — PR #3189 (open).** Lets users ask "why did the agent do that" — a lightweight agent-explainability/session-debugging tool. Interesting signal for observability as a community-driven feature.

Prediction: the next minor release likely bundles the entire audit series (#3414–3420) + the router engagement fix (#3422) + the Cursor provider PRs if they merge in time.

## 7. User Feedback Summary

- **Pain: Silent attachment failures (WhatsApp).** Users configure agents expecting media intake; they get empty `/workspace/attachments` paths. The silence (1 comment on a 2-month-old issue) suggests users are either avoiding WhatsApp or hitting it and silently giving up.
- **Pain: Engagement semantics are surprising.** The `mention-sticky` bug (#3369) shows that documented "silent context" is actually "active subscription" — a trust-breaking surprise for a chat-product whose core value is predictable behavior.
- **Satisfaction: Rapid core-team responsiveness.** The 24h fix for #3369 and the depth of the skill audit (config seams, dead envs, honest tests) signals the maintainers are actively quality-gating community skills — good for long-term trust.
- **Pain (PR-level): Multi-install confusion.** Multiple fixes reference "which checkout the global shim points at" and "reads install A's DB" — power users running multiple NanoClaw installs on one host are hitting cross-wiring bugs. The install-slug refactor is the response.

## 8. Backlog Watch

- **[Issue #2715 — WhatsApp media mounts](https://github.com/nanocoai/nanoclaw/issues/2715)** — Open **73 days**, 1 comment, no explicit fix linked. This is the project's oldest unresolved functional bug. The path fix is conceptually simple (bind-mount the host dir or change the path handed to the agent); it needs a maintainer to triage it against PR #3401.
- **[PR #3247 — Retire malformed cron strings](https://github.com/nanocoai/nanoclaw/pull/3247)** — Open 7 days, authored by a contributor (not core-team). A well-scoped stability fix that's untriaged; risks rotting without a maintainer review.
- **[PR #3270 — `ncl token usage`](https://github.com/nanocoai/nanoclaw/pull/3270)** — Open 5 days, feature-flagged; waiting on maintainer direction (the PR has no core-team label).
- **[PR #3189 — `add-why` skill](https://github.com/nanocoai/nanoclaw/pull/3189)** — Open 16 days, unlabeled; a quality-of-life debug skill that could serve the "explainable agent" narrative but needs a champion.

**Health verdict**: The project is **healthy but mid-migration**. Core-team throughput is exceptional, but the open issue-to-fix PR ratio (2 open issues with only 1 linked fix) and the 2-month-old WhatsApp bug are the weak points. If the router fix (#3422) and the audit series land cleanly, the next release should materially reduce the "it works in theory" gap across all major channels.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for 2026-08-21.

---

## IronClaw Project Digest: 2026-08-21

### 1. Today's Overview
IronClaw is in a high-velocity phase with significant architectural restructuring and feature delivery. Activity in the last 24 hours is intense, with 22 issues and 35 PRs updated. The project is pushing forward on major initiatives including a persistent per-user sandbox (#7732), the first phase of an agent lifecycle hook system (#7770), and a multi-phase WebUI design system overhaul (#7038). While no new releases were cut, the merge queue saw substantial cleanup, including merging the "run-now" automation feature (#7193) and consolidating seven subagent design docs into one canonical README (#7763). Notably, Rust 1.98's stable release caused a CI-wide lint cascade that was promptly fixed by two PRs, highlighting the team's responsiveness to toolchain drift.

### 2. Releases
No new releases were published in the last 24 hours. The project appears to be between release cycles, with active development focused on `v1.4.0` milestones (referenced in epics #7732 and #7781).

### 3. Project Progress
The merge queue was active, clearing out key features and fixes.

- **Automations "Run-Now" Shipped:** Issue #7193 (Closed) advanced the automation surface. PR [#7729](https://github.com/nearai/ironclaw/pull/7729) (Merged) added an atomic manual-fire path, wiring it through the capability, product service, WebUI API, and UI. This fulfills a major product gap where automations could only be scheduled.
- **Subagent Documentation Consolidation:** PR [#7763](https://github.com/nearai/ironclaw/pull/7763) (Merged) consolidated seven contradictory design docs (7,000+ lines) into a single canonical README, netting a **−9,713 line** reduction. This is a significant win for maintainability.
- **Suggestion Generation Fix:** PR [#7786](https://github.com/nearai/ironclaw/pull/7786) (Closed) unblocked suggestion generation on OpenAI models, which was completely broken by a `uniqueItems` schema property. It also cleaned up dead allowlist IDs and gated cards.
- **CI Lint Cascade Resolved:** Two PRs ([#7777](https://github.com/nearai/ironclaw/pull/7777), [#7778](https://github.com/nearai/ironclaw/pull/7778)) were merged to clear the clippy lint cascade from Rust 1.98, unbreaking the "Check all-target lints" step and the merge queue.
- **Slack Deployment UX:** PR [#7738](https://github.com/nearai/ironclaw/pull/7738) (Merged) added per-field help text to the Slack deployment configuration card.
- **Login UX Adjustment:** PR [#7304](https://github.com/nearai/ironclaw/pull/7304) (Merged) flips the WebChat login card to place OAuth provider buttons above the gateway token form.

### 4. Community Hot Topics
- **[Epic #7732: Persistent per-user sandbox with iron-proxy](https://github.com/nearai/ironclaw/issues/7732)** (8 comments): This is the most active item. The community is deeply engaged with the architectural shift toward a persistent sandbox. The conversation revolves around the limitations of the current ephemeral Docker container-per-command model and the desire for a persistent user computer.
- **[Epic #7770: Hook the agent lifecycle](https://github.com/nearai/ironclaw/issues/7770)** (3 comments): This epic is generating significant design discussion around introducing plugin-like seams for agent lifecycle events. The first PR ([#7765](https://github.com/nearai/ironclaw/pull/7765)) is already sparking follow-up issues (#7780, #7775), showing the team is iterating quickly on the initial design.
- **[Issue #7783: LLM timeout policy flaw](https://github.com/nearai/ironclaw/issues/7783)** (1 comment): This is a critical bug report that highlights a fundamental flaw in the non-streaming finalization path where stalled provider requests can trigger cascading timeouts and kill runs. It is a hot topic due to its potential impact on reliability.

### 5. Bugs & Stability
- **Critical - LLM Timeout Cascades:** [Issue #7783](https://github.com/nearai/ironclaw/issues/7783) details a serious flaw where a stalled provider request in structured-output finalization can't be measured for TTFT and the retry budget doesn't fit the deadline, causing run failures.
- **High - Memory Write Race Condition:** [Issue #7776](https://github.com/nearai/ironclaw/issues/7776) reports that `memory.write` with `append: false` can silently overwrite concurrent writes because the CAS only protects against torn writes, not full-document rewrite races.
- **High - OpenAI Suggestion Generation SEV:** The `uniqueItems` schema bug (fixed in [PR #7786](https://github.com/nearai/ironclaw/pull/7786)) was treated as a SEV (Severity 1) because it broke all OpenAI-backed suggestion generation. The fix is ready and cherry-pickable.
- **Medium - CI Red on Main:** The Rust 1.98 clippy lint cascade broke the CI on `main`. This was treated as a merge-queue blocker and fixed by PRs [#7777](https://github.com/nearai/ironclaw/pull/7777) and [#7778](https://github.com/nearai/ironclaw/pull/7778).
- **Medium - Persistent Test Flakiness:** [Issue #7767](https://github.com/nearai/ironclaw/issues/7767) and its corresponding fix PR [#7774](https://github.com/nearai/ironclaw/pull/7774) address a long-standing issue where Automation presenter tests fail due to timezone dependencies (e.g., in `Asia/Shanghai`).
- **Low - Hosted MCP OAuth Failure:** [Issue #7308](https://github.com/nearai/ironclaw/issues/7308) (Closed) was resolved after investigation, but highlights the fragility of hosted MCP OAuth registration.

### 6. Feature Requests & Roadmap Signals
The roadmap is clearly defined by several epics targeting `v1.4.0`:

- **Design System (Phases 2-5):** With Phase 1 progressing via [PR #7750](https://github.com/nearai/ironclaw/pull/7750), the scope is now split between Epics [#7781](https://github.com/nearai/ironclaw/issues/7781) (Phases 2-3: governance and reskin) and [#7782](https://github.com/nearai/ironclaw/issues/7782) (Phases 4-5: agentic interactions and IA). These are strong signals for a major UI overhaul in the coming releases.
- **Persistent Sandbox & Proxy:** The groundwork for the persistent sandbox epic (#7732) is being laid in [PR #7779](https://github.com/nearai/ironclaw/pull/7779), routing egress through a per-user proxy. The community is pushing for a more persistent, computer-like environment for agents.
- **Agent Lifecycle Hooks:** The `AfterTurn` hook ([PR #7765](https://github.com/nearai/ironclaw/pull/7765)) is the first of a phased lifecycle hook system (#7770). Follow-up requests for `BeforeTurn`, compaction, and tool-result seams (#7780, #7775) are already in the backlog, indicating this is a high-priority area for the next iterations.

### 7. User Feedback Summary
- **Satisfaction:** High confidence in the team's ability to ship complex features is evidenced by the rapid merging of the automations "run-now" feature and the Wasm tooling stack.
- **Developer Pain Points:**
    - **High:** The lack of an "on-demand" trigger for automations was a major issue, now resolved (#7193).
    - **Medium:** The UI configuration for OAuth extensions is flawed. [Issue #7769](https://github.com/nearai/ironclaw/issues/7769) reports that the Configure modal incorrectly indicates that no configuration is required because it discards setup blockers.
    - **Low:** Users want more guidance in configuration UIs, as shown by the addition of help text to the Slack deployment card (PR #7738).

### 8. Backlog Watch
- **[Issue #7038: Design System Phase 1 - Storybook](https://github.com/nearai/ironclaw/issues/7038)**: This epic has been open since the beginning of August. While the associated PR #7750 is active, the overall design-system program is sprawling and has already been re-scoped twice. Maintainers should watch for scope creep.
- **[Issue #7771: Daily failure taxonomy](https://github.com/nearai/ironclaw/issues/7771)**: This is a recurring process issue. While not a code bug, it serves as a crucial data source for the team, showing the overwhelming majority of benchmark failures are genuine model-quality errors rather than code regressions. It's a signal of where the team's focus might need to be long-term.
- **[PR #7749: Test trigger for /benchmark](https://github.com/nearai/ironclaw/pull/7749)**: This is a "meta" PR to re-trigger a benchmark. While not a product change, it indicates an ongoing need to validate the `qa-automation-preview` agent performance, which is critical for release confidence.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest
**Digest Date: 2026-08-21** | **Data Source: github.com/netease-youdao/LobsterAI**

---

## 1. Today's Overview

LobsterAI shows a steady maintenance cadence with 7 PRs touched in the last 24 hours, of which 6 have been closed or merged and 1 remains open. No new releases were published in this window. The project is processing a backlog of PRs from early April 2026, reflecting a batch of feature work and bug fixes moving through the pipeline. Two issues remain open, both flagged as stale with no recent maintainer activity since August 20. Overall, the project appears healthy in terms of code integration velocity, though stale issues and PRs indicate a need for better triage responsiveness.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent release information is not available in this data window.

---

## 3. Project Progress

Six PRs were closed/merged or otherwise resolved in the last 24 hours. Notably, several address meaningful UX gaps and build stability:

- **[PR #1545 — fix(agent): sync activeSkillIds immediately when updating current agent's skills](https://github.com/netease-youdao/LobsterAI/pull/1545)** (closed) — Fixes a bug (issue #1502) where saving skill changes in the Agent settings panel did not immediately update the Active Skill Badges in the current conversation. The root cause was a Redux state desync (`skillIds` updated but `activeSkillIds` not synced). Fixes a frustrating UX where users had to switch agents and back to see changes.
- **[PR #1546 — feat(engine-overlay): 引擎启动超时后显示取消启动和查看日志按钮](https://github.com/netease-youdao/LobsterAI/pull/1546)** (closed) — Adds escape-hatch buttons ("Cancel Startup" and "View Logs") to the EngineStartupOverlay after 30 seconds of startup. Previously users had to wait for a 5-minute hard timeout with no interactivity if OpenClaw engine startup hung due to network or cache issues.
- **[PR #1553 — feat(cowork): Write 工具文件卡片及分屏预览面板](https://github.com/netease-youdao/LobsterAI/pull/1553)** (closed) — Implements inline file cards for Write tool calls with file metadata and actions (open, reveal in Finder/Explorer, copy path, preview), plus a drag-resizable right-side FilePreviewPanel (320–900px) supporting Markdown, HTML sandbox iframes, SVG, images, and syntax highlighting. Addresses issue #1552.
- **[PR #1555 — fix: npm run dist:mac:x64打包失败](https://github.com/netease-youdao/LobsterAI/pull/1555)** (closed) — Fixes macOS x64 packaging failure caused by `sha256sum` not being supported on macOS; adds `shasum` compatibility in `build-openclaw-runtime.sh`.
- **[PR #1557 — feat(settings): 设置面板侧栏支持搜索筛选分类](https://github.com/netease-youdao/LobsterAI/pull/1557)** (closed) — Adds a search box to the settings sidebar for filtering tabs (General, Engine, Model, IM, Email, Memory, Agent, Shortcuts, About). Supports AND matching with NFKC normalization and auto-switches to first visible tab if the current one is filtered out.
- **[PR #1560 — fix: 修复Agent编辑后点击原Agent无法切换回聊天界面的问题](https://github.com/netease-youdao/LobsterAI/pull/1560)** (closed) — Fixes a navigation bug where clicking the currently selected Agent after editing it did not switch back to its chat interface; root cause was an early return in `SidebarAgentList.handleSwitch` when `agentId === currentAgentId`.

**Still open:**
- **[PR #1547 — fix(scheduledTask): 修复定时任务通知渠道选择后无法改回"不通知"的问题](https://github.com/netease-youdao/LobsterAI/pull/1547)** — Fixes a form bug in scheduled task editing where changing notification channel back to "Do Not Notify" was not persisted properly. The fix involves two code sections with inconsistent design from commit `61cfe60`. Minimal change: +2 lines in `TaskForm.tsx`.

---

## 4. Community Hot Topics

The most active discussions in the last 24 hours revolve around feature requests and documentation issues:

- **[Issue #1556 — doc bug: IM机器人配置指南404](https://github.com/netease-youdao/LobsterAI/issues/1556)** (2 comments, open since April 2026) — A user reports a 404 on the official IM bot configuration guide link. This is a straightforward documentation accessibility problem that has gone unresolved for over 4 months. The sustained interest suggests documentation quality is a recurring pain point for the user community.

- **[Issue #1552 — feat: AI产物 Markdown 预览及文件卡片支持](https://github.com/netease-youdao/LobsterAI/issues/1552)** (1 comment) — This feature request was **already addressed** by PR #1553 (closed), which implements the FileCard + preview panel. This demonstrates good responsiveness to user-driven feature requests.

Both issues carry a `[stale]` label, indicating they have aged significantly without resolution — though in the case of #1552, a corresponding PR has since landed.

---

## 5. Bugs & Stability

| Severity | Issue/PR | Description | Status |
|----------|----------|-------------|--------|
| **Medium** | [PR #1560](https://github.com/netease-youdao/LobsterAI/pull/1560) | After editing an Agent, clicking the same selected Agent doesn't return to its chat view — navigation dead-end | Fix merged (closed) |
| **Medium** | [PR #1545](https://github.com/netease-youdao/LobsterAI/pull/1545) | Active Skill Badges don't update immediately after saving skill changes; requires agent switch to see effect | Fix merged (closed) |
| **Medium** | [PR #1547](https://github.com/netease-youdao/LobsterAI/pull/1547) | Scheduled task notification channel can't be changed back to "No Notification" — persists prior IM channel selection | Fix open, awaiting merge |
| **Low** | [PR #1555](https://github.com/netease-youdao/LobsterAI/pull/1555) | macOS x64 packaging fails due to `sha256sum` unsupported on macOS | Fix merged (closed) |
| **Low** | [Issue #1556](https://github.com/netease-youdao/LobsterAI/issues/1556) | Documentation 404 on IM bot configuration guide | Open, unresolved for 4+ months |

No critical crashes or data-loss bugs were reported in this window.

---

## 6. Feature Requests & Roadmap Signals

Two notable feature requests have surfaced from the community:

- **[Issue #1552 — AI产物 Markdown 预览及文件卡片支持](https://github.com/netease-youdao/LobsterAI/issues/1552)** — Users want to preview AI-generated files (especially Markdown/HTML/code) directly in the app without cluttering chat with full file contents. **Already shipped via PR #1553**, which goes further with a resizable split-pane preview supporting syntax highlighting and sandboxed HTML rendering. This is a strong signal that the team is aligned with user needs around AI output ergonomics.

- **[PR #1557 — Settings panel search filtering](https://github.com/netease-youdao/LobsterAI/pull/1557)** — Community PR adding search to the settings sidebar. This improvements hints at growing complexity in the app (9+ settings tabs) — a product maturity marker. Likely to be included in the next minor release given it's already closed/merged.

- **[PR #1546 — Engine startup timeout escape hatch](https://github.com/netease-youdao/LobsterAI/pull/1546)** — Adds cancellation and log access options after 30s of engine startup. This is a robustness improvement that addresses user frustration with unresponsive startup screens.

**Prediction:** The next release is likely to include the FileCard/PreviewPanel feature, settings search, and the engine startup recovery UX — all three were merged in this batch and represent cohesive UX improvements.

---

## 7. User Feedback Summary

**Pain points expressed:**
- **Documentation accessibility**: The 404 on the IM configuration guide (Issue #1556) suggests docs are not thoroughly maintained or validated. The 4-month unresolved status may erode user trust.
- **State-sync frustration**: The skill badge delay (PR #1545/#1502) and the Agent-switch navigation bug (PR #1560) both point to UI state management issues that break user workflows with unexpected behavior.
- **Notification configuration inflexibility**: The scheduled task notification bug (PR #1547) prevents users from reverting a channel choice — a small but annoying data-integrity issue.
- **File preview friction** (Issue #1552): Users previously had to either ask the Agent to paste file contents into chat (wasting tokens/space) or manually switch to the file manager — a clear UX gap that has now been closed.

**Satisfaction signals:**
- The feature request (#1552) was addressed by a comprehensive PR (#1553), showing team responsiveness to well-articulated user needs.
- Multiple community contributors (stone333, gongzhi-netease, liulingfeng, kayo5994, flowell, noransu) submitted fixes and features — a healthy sign of an engaged external developer community.

---

## 8. Backlog Watch

Items requiring maintainer attention:

- **[Issue #1556 — doc bug: IM机器人配置指南404](https://github.com/netease-youdao/LobsterAI/issues/1556)** — Open since **2026-04-08** (over 4 months), flagged stale, with 2 comments and zero reactions. A trivial documentation fix that has been ignored for too long. **High priority for triage** — it's low-effort and blocks users from accessing critical configuration docs.

- **[PR #1547 — fix(scheduledTask): 通知渠道无法改回"不通知"](https://github.com/netease-youdao/LobsterAI/pull/1547)** — Open since **2026-04-07** (over 4 months), no comments from maintainers. This is a small, well-scoped fix (+2 lines) for a concrete bug. The lack of review/merge attention suggests possible maintainer bandwidth issues or PR triage gaps.

Both items are in the "stale" category and have waited 4+ months for resolution or acknowledgment — worth a maintainer pass to either close, accept, or provide guidance.

---

*Digest generated from LobsterAI GitHub data for 2026-08-21*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-21

## 1. Today's Overview

Moltis shows moderate activity this cycle with 1 issue and 8 pull requests updated in the last 24 hours. The project is in a steady state of maintenance and security hardening—4 PRs were merged/closed and 4 remain open. Notable focus areas include WhatsApp channel improvements, security fixes (vault authentication, sandbox image validation, supply chain pinning), and Windows compatibility. A new release `20260820.01` was published. The issue tracker is remarkably clean with just 1 issue updated (now closed), suggesting healthy triage discipline.

## 2. Releases

**`20260820.01`** (released 2026-08-20) — No detailed changelog or release notes were provided in the available data. The version numbering suggests a calendar-based scheme (YYYYMMDD.N). Given the cluster of security and WhatsApp-related PRs merged around this date, this release likely contains fixes for vault endpoint authentication, WhatsApp push-name handling, reply addressing, and the configurable tool-ceiling for untrusted turns.

_No breaking changes or migration notes were published in the data available._

## 3. Project Progress

Four PRs were merged/closed in this window:

- **[#1216 — fix(httpd): require authentication for vault unlock and recovery](https://github.com/moltis-org/moltis/pull/1216)** (merged, by penso): Fixes CWE-306 by adding `AuthSession` extractor to vault unlock/recovery endpoints. Previously the `/api/auth/` prefix allowlist bypassed `auth_gate`, permitting unauthenticated brute-force attacks.

- **[#1217 — fix(whatsapp): treat a reply to the bot as addressing it](https://github.com/moltis-org/moltis/pull/1217)** (merged, by vikng-dev): Fixes dropped messages in group chats with `mention_mode = "mention"`. WhatsApp replies land in `ContextInfo` differently than `@` mentions; both are now treated as addressing the bot.

- **[#1218 — fix(whatsapp): stop hardcoding the push name to "Moltis"](https://github.com/moltis-org/moltis/pull/1218)** (merged, by vikng-dev): The hardcoded push name caused bots configured with custom names (e.g., "Ada") to appear as "Moltis" in group chats for users without the number saved.

- **[#1219 — fix(channels): make the untrusted-turn tool ceiling configurable](https://github.com/moltis-org/moltis/pull/1219)** (merged, by vikng-dev): Addresses over-restriction from #1170—hardcoded deny-all policies removed three public-audience tools and made tool policy layers 4/5 unreachable in shared channels.

## 4. Community Hot Topics

**Activity is notably low** — no issues or PRs show comments or reactions beyond the baseline (all show `0` 👍). The most "active" items are the merged security and WhatsApp fixes:

- **[#1177 — Vault Unlock/Recovery Endpoints Missing Authentication (CWE-306)](https://github.com/moltis-org/moltis/issues/1177)** (closed, 0 comments): Security vulnerability reported by Practice100101. It was fixed and closed via PR #1216 within 3 weeks—impressive turnaround. The low comment count suggests reporter provided a clear, actionable report.

**Analysis:** The community's underlying needs center on: (1) **Security hardening**—vault endpoints, sandbox image validation, and supply chain attacks were all addressed this cycle, suggesting security-minded users are actively auditing Moltis; (2) **WhatsApp reliability**—push-name identity and mention/reply semantics matter for production deployments; (3) **Windows support**—the long-running PR #468 for `cmd.exe` in shell hooks (open since March) indicates Windows users are an underserved but persistent constituency.

## 5. Bugs & Stability

One bug was active in this window, ranked by severity:

- **Critical — [Issue #1177: Vault Unlock/Recovery Missing Authentication (CWE-306)](https://github.com/moltis-org/moltis/issues/1177)** (CLOSED): Any unauthenticated remote caller could brute-force vault unlock/recovery endpoints. **Fix delivered** via [PR #1216](https://github.com/moltis-org/moltis/pull/1216), merged the same day as the digest. This was a serious vulnerability (CWE-306: Missing Authentication for Critical Function) with clear brute-force implications.

**Related open PRs for ongoing hardening:**
- **[#1222 — validate sandbox image requests](https://github.com/moltis-org/moltis/pull/1222)**: Image reference and package-name validation before container/Dockerfile use; restricts operations to operator admins.
- **[#1221 — pin Snyk Agent Scan](https://github.com/moltis-org/moltis/pull/1221)**: Pins the `uvx` Snyk Agent Scan to 0.5.17 to prevent supply chain attacks; removes standalone `mcp-scan` fallback.

## 6. Feature Requests & Roadmap Signals

No explicit user feature requests were filed in this window. However, the merged PRs signal **implicit roadmap directions**:

- **Configurable security posture** — [#1219](https://github.com/moltis-org/moltis/pull/1219) making tool ceilings configurable suggests a trend toward more granular security controls (following the #1170 over-correction). Expect more configurability in tool policies per channel/audience.

- **WhatsApp channel maturity** — With push-name, reply-addressing, and Markdown rendering (PR #1220) fixes, WhatsApp is becoming a first-class channel. Model-generated Markdown → WhatsApp-native markup conversion in [#1220](https://github.com/moltis-org/moltis/pull/1220) fills a real gap for the **most common messaging use case** (LLM output formatting).

- **Windows compatibility** — [#468](https://github.com/moltis-org/moltis/pull/468) (open since March for `cmd.exe` hook support) is still pending. If merged, it would finally make shell hooks work on Windows without shims.

**Prediction for next release:** The three open PRs ([#1222](https://github.com/moltis-org/moltis/pull/1222), [#1221](https://github.com/moltis-org/moltis/pull/1221), [#1220](https://github.com/moltis-org/moltis/pull/1220) created 2026-08-20) are likely candidates for the next point release, plus [#468](https://github.com/moltis-org/moltis/pull/468) if a maintainer reviews it soon.

## 7. User Feedback Summary

Direct user feedback is sparse (no comments/reactions on issues or PRs in this window), but signals can be inferred from contributor behavior and the issue report:

- **Security-conscious deployments** (Practice100101, Issue #1177): The reporter filed a precise CWE-306 bug with a preflight checklist—indicating a security-literate user base running Moltis in exposed environments.

- **WhatsApp production users** (vikng-dev's PRs): The fixes for push-name, reply-addressing, and Markdown rendering address real-world pain points: bots mislabeled in group chats, dropped replies, and ugly raw-Markdown messages in WhatsApp. These are "this is broken in production" fixes.

- **Windows users** (jmikedupont2, PR #468): Long-standing pain point with shell hooks failing on Windows because `sh -c` isn't available. The PR author tested on Windows 10 with v0.9.10 and confirmed CI passes. The 5-month wait for review is a potential dissatisfaction point.

- **Alternative personalities** (PR #1218): Bots configured with custom names (e.g., "Ada") were mislabeled as "Moltis" in group chats—a subtle but confusing identity bug for branded deployments.

## 8. Backlog Watch

- **[PR #468 — fix(plugins): use cmd.exe on Windows for shell hooks](https://github.com/moltis-org/moltis/pull/468)** (open since **2026-03-23**, ~5 months): A straightforward fix with Windows 10 testing and passing CI. This is the longest-pending PR. It needs maintainer review/merge. Windows users are blocked on shell-hook functionality.

**No long-unanswered issues** are evident—the single bug (CWE-306) was triaged and fixed within 3 weeks. Inactive issues appear to be pruned or quickly closed, indicating strong issue hygiene.

---

**Overall health assessment:** Moltis is in good health—security was proactively hardened, the WhatsApp channel received meaningful user-facing fixes, the release cadence is consistent (daily via calver), and issue responsiveness is fast (Critical bug → fix in 21 days). The main organizational risk is the 5-month-old Windows PR awaiting review, which may indicate a maintainer bottleneck or lower priority for the Windows platform.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-21

## 1. Today's Overview

CoPaw (QwenPaw) is demonstrating a **healthy, high-velocity development cadence** with 28 issues and 50 PRs updated in the last 24 hours, including a new beta release (v2.1.1-beta.1). The project shows strong community engagement with 13 closed issues and 28 merged/closed PRs, indicating an efficient maintainer workflow. A significant portion of activity centers on **stability fixes** (timeouts, network resilience, file corruption handling) and **infrastructure improvements** (concurrent driver initialization, marketplace unification, skill system enhancements). The project's dual focus is evidenced by roughly equal activity on both **user-facing console features** and **backend/core reliability** work. Release duty verification for the v2.1.1-beta.1 is underway, signaling organized release management practices. Overall, the project appears well-maintained with active triage, though some long-standing issues (e.g., #6921, #6436) remain open and merit attention.

## 2. Releases

**v2.1.1-beta.1** (Beta, published 2026-08-20) — [Release page](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.1.1-beta.1)

Changes included:
- **Console improvement:** Editor tab overflow navigation enhancement by @rayrayraykk ([PR #6983](https://github.com/agentscope-ai/QwenPaw/pull/6983))
- **Providers fix:** Lowered rate limiter init log level to reduce noise by @rayrayraykk ([PR #6988](https://github.com/agentscope-ai/QwenPaw/pull/6988))
- Chore: release notes updates

**Migration notes:** This is a beta release with no breaking changes or migration steps indicated. Release duty verification issue [#7180](https://github.com/agentscope-ai/QwenPaw/issues/7180) is open with a 4-hour deadline for platform installation verification, indicating the project follows structured release validation.

## 3. Project Progress

**Notable merged/closed PRs in the last 24 hours:**

| PR | Description | Significance |
|---|---|---|
| [#7161](https://github.com/agentscope-ai/QwenPaw/pull/7161) | Add artifacts to assistant response card (console) | Enhances observability of tool outputs |
| [#6371](https://github.com/agentscope-ai/QwenPaw/pull/6371) | Fix file-handling: continue fallback after downloader timeout | Addresses resilience gap in download chain (wget→curl→urllib) |
| [#7135](https://github.com/agentscope-ai/QwenPaw/pull/7135) | Fix envs: preserve corrupt files and write atomically | Prevents silent env var loss on corruption |
| [#7174](https://github.com/agentscope-ai/QwenPaw/pull/7174) | perf(drivers): initialize persistent drivers concurrently | Reduces cold-start latency for workspace startup |
| [#6880](https://github.com/agentscope-ai/QwenPaw/pull/6880) | Unify apps, plugins, skills in marketplace | Consolidates three marketplace routes under `/market` |
| [#7166](https://github.com/agentscope-ai/QwenPaw/pull/7166) | Bundle qwenpawmail MCP as standalone sidecar | Improves packaging reliability for frozen builds |
| [#7073](https://github.com/agentscope-ai/QwenPaw/pull/7073) | Skill name deduplication (workspace vs built-in) | Prevents duplicate skill loading conflicts |

**Key advances:**
- **Memory systems**: Multiple PRs target memory improvements — `reme 0.4.1.8` update with configurable embedding health check timeout [PR #7133](https://github.com/agentscope-ai/QwenPaw/pull/7133), PowerContext pluggable memory backend [PR #7080](https://github.com/agentscope-ai/QwenPaw/pull/7080), and reranker UI config panel [PR #6399](https://github.com/agentscope-ai/QwenPaw/pull/6399)
- **Console performance**: Long chat session responsiveness work [PR #7176](https://github.com/agentscope-ai/QwenPaw/pull/7176) and free model listing restoration [PR #7175](https://github.com/agentscope-ai/QwenPaw/pull/7175)
- **New capabilities**: QwenPaw Hub (self-hosted multi-user control plane) [PR #7112](https://github.com/agentscope-ai/QwenPaw/pull/7112), session-level thinking modes (Off/Low/Medium/High) [PR #7163](https://github.com/agentscope-ai/QwenPaw/pull/7163), and dialogue-gated video dispatch for Creator [PR #7167](https://github.com/agentscope-ai/QwenPaw/pull/7167)

## 4. Community Hot Topics

1. **[Issue #6921](https://github.com/agentscope-ai/QwenPaw/issues/6921) (10 comments, Open)** — "Agent stops without notification after planning" — Users report the agent frequently halts mid-task after outputting planning statements (e.g., "Let me do all three") without visible indication. This appears to be the **most active issue** by comment count, suggesting a significant trust/usability problem with task completion perception.

2. **[Issue #7102](https://github.com/agentscope-ai/QwenPaw/issues/7102) (9 comments, Closed)** — "Freeze more than 10 minutes long" — User reported complete freeze with GLM 5.3, no token output for 10+ minutes. Closed, indicating resolution or escalation path.

3. **[Issue #6643](https://github.com/agentscope-ai/QwenPaw/issues/6643) (6 comments, Closed)** — "Task outputs should be organized per-task directories" — Users want artifacts organized by task rather than accumulating in a single `media` directory. This points to workspace organization as a real pain point.

4. **[PR #7112](https://github.com/agentscope-ai/QwenPaw/pull/7112) (Open)** — QwenPaw Hub self-hosted multi-user control plane — Significant architectural addition, likely to draw review attention and community interest for team deployments.

5. **[Issue #6436](https://github.com/agentscope-ai/QwenPaw/issues/6436) (4 comments, 1 👍, Open)** — Automatic model routing per message — Suggests routing each request to the most suitable model (small/local for simple turns, vision model for images, large for complex reasoning). This has roadmap-signal potential.

**Underlying needs:** The most active discussions reveal users care about **reliability of task completion** (halts without notification), **workspace organization**, and **performance under load**. These are production-readiness concerns from real-world usage rather than feature-novelty requests.

## 5. Bugs & Stability

### High Severity (with fix PRs or closed)
- **Freezing for 10+ minutes** — [Issue #7102](https://github.com/agentscope-ai/QwenPaw/issues/7102) (Closed): GLM 5.3 provider caused complete freezes with no output. Closed — likely addressed.
- **Streaming ReadError causing UNKNOWN_AGENT_ERROR** — [Issue #7162](https://github.com/agentscope-ai/QwenPaw/issues/7162) (Closed): `httpx.ReadError` during SSE streaming wasn't in `_get_httpx_retryable()`, causing task failures. Fix includes adding ReadError to retryable list.
- **Corrupt envs.json silently loses all env vars** — [Issue #7118](https://github.com/agentscope-ai/QwenPaw/issues/7118) (Closed) / [PR #7135](https://github.com/agentscope-ai/QwenPaw/pull/7135): Fixed with atomic writes and file preservation.

### Medium Severity (open)
- **Network interruption prevents auto-recovery** — [Issue #6932](https://github.com/agentscope-ai/QwenPaw/issues/6932) (Open): After transient network drops, all LLM requests fail with timeout errors until manual restart. Reproduced twice in one day. This is a **reliability gap for real-world use**.
- **history.db ballooning to 7.6GB** — [Issue #7168](https://github.com/agentscope-ai/QwenPaw/issues/7168) (Open): `recall_history` expand writes full tool outputs into conversation_history, causing unbounded growth. Critical for long-running agents.
- **Un-downloadable image link bricks session** — [Issue #7110](https://github.com/agentscope-ai/QwenPaw/issues/7110) (Closed): A single inaccessible image URL makes the entire conversation unusable; only `/clear` helps.
- **Embedding health check timeout hardcoded** — [Issue #7156](https://github.com/agentscope-ai/QwenPaw/issues/7156) (Open): 5s timeout hardcoded, always fails even when backend is warm — degrades across the board.
- **view_video inline-media cap hardcoded to 2MB** — [Issue #7060](https://github.com/agentscope-ai/QwenPaw/issues/7060) (Closed): Provider setting ignored; video over 2MB is replaced by placeholder text.

### Lower Severity (open/pr-related)
- **Assistant message end-time display wrong** — [Issue #6826](https://github.com/agentscope-ai/QwenPaw/issues/6826): UI shows seconds instead of 2min actual thinking time.

## 6. Feature Requests & Roadmap Signals

**Strong candidates for next releases:**

1. **Always-on workspace Skills for specialized agents** — [Issue #7182](https://github.com/agentscope-ai/QwenPaw/issues/7182) + [PR #7183](https://github.com/agentscope-ai/QwenPaw/pull/7183): PR already submitted with opt-in workspace-scoped mode preloading instructions into system prompt. Likely to land soon.

2. **Agent-level cross-session recall toggle** — [Issue #7184](https://github.com/agentscope-ai/QwenPaw/issues/7184): Configuration to control whether new sessions recall other sessions, with focused preservation of history options. Developer/user-proposed with clear config syntax.

3. **Qwen_Code as third-party agent harness** — [Issue #7181](https://github.com/agentscope-ai/QwenPaw/issues/7181): Support for users with limited network access; identified as better than ACP.

4. **Automatic model routing** — [Issue #6436](https://github.com/agentscope-ai/QwenPaw/issues/6436): 1 👍, growing interest in per-message model selection (small/large/vision).

5. **QQ bot scheduled messages** — [Issue #7159](https://github.com/agentscope-ai/QwenPaw/issues/7159): User request referencing official QQ capabilities (proactive push, timed tasks, message recall).

6. **DingTalk group context modes** — [Issue #7158](https://github.com/agentscope-ai/QwenPaw/issues/7158): Configurable isolation vs. shared context within group chats.

7. **Per-task output directories** — [Issue #6643](https://github.com/agentscope-ai/QwenPaw/issues/6643): Closed, likely implemented or planned.

## 7. User Feedback Summary

**Common pain points observed in this window:**

- **Task interruption without notification** — Multiple users reporting halts mid-run with no visible indicator ([#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921)); need to say "continue" to resume execution. This is the **top friction point** among active discussion.
- **Freezes with certain providers** ([#7102](https://github.com/agentscope-ai/QwenPaw/issues/7102)): LLM provider compatibility remains a trust issue.
- **Workspace organization**: Users find the single `media` directory for all outputs confusing; per-task directories desired ([#6643](https://github.com/agentscope-ai/QwenPaw/issues/6643)).
- **Chinese filename handling**: File references in prompts lose Chinese characters, harming readability for Chinese users ([#6453](https://github.com/agentscope-ai/QwenPaw/issues/6453)).
- **VPN compatibility**: Entire desktop client becomes unusable when using VPN ([#6974](https://github.com/agentscope-ai/QwenPaw/issues/6974)).
- **UI accessibility on mobile**: Users report platform web page is hard to use on phones — entry points placed below fold, risk of accidentally hitting "stop" ([#7177](https://github.com/agentscope-ai/QwenPaw/issues/7177)).

**Satisfaction signals:** Issue #7162, #7118, #6370 all demonstrate responsive maintainers addressing edge cases with targeted fixes. The completed release duty flow ([#7180](https://github.com/agentscope-ai/QwenPaw/issues/7180)) shows organizational maturity. The Hub PR ([#7112](https://github.com/agentscope-ai/QwenPaw/pull/7112)) suggests the team is actively building for multi-user enterprise scenarios.

## 8. Backlog Watch

**Issues needing maintainer attention:**

1. **[Issue #6921](https://github.com/agentscope-ai/QwenPaw/issues/6921)** (Open, 2026-08-12, 10 comments) — Agent halts in multi-step tasks without notifying the user. Age: ~9 days. High community interest, unresolved — **needs maintainer diagnosis**.

2. **[Issue #6436](https://github.com/agentscope-ai/QwenPaw/issues/6436)** (Open, 2026-07-24, 4 comments, 1 👍) — Automatic model routing request. Age: ~28 days. Underserved feature request with broad applicability.

3. **[Issue #6932](https://github.com/agentscope-ai/QwenPaw/issues/6932)** (Open, 2026-08-12, 3 comments) — Network interruption auto-recovery failure. Age: ~9 days. Reliability gap affecting production use. No PR referenced yet.

4. **[Issue #7168](https://github.com/agentscope-ai/QwenPaw/issues/7168)** (Open, 2026-08-20, 1 comment) — history.db exploding to 7.6GB via recall_history. Critical memory-management bug, **very recent, no PR yet** — requires urgent attention.

5. **[Issue #7156](https://github.com/agentscope-ai/QwenPaw/issues/7156)** (Open, 2026-08-20, 2 comments) — Hardcoded timeout on embedding health check. Configurable timeout PR exists as WIP ([PR #7133](https://github.com/agentscope-ai/QwenPaw/pull/7133)) but is marked WIP for reme 0.4.1.8.

6. **[Issue #7013](https://github.com/agentscope-ai/QwenPaw/issues/7013)** (Open, 2026-08-14, 3 comments) — Unified tool panel / Web service preview / interactive terminal for Chat. 7-day-old feature request with cross-component scope.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest
**Date:** 2026-08-21

---

## 1. Today's Overview

ZeroClaw is in a **high-velocity development phase**, with 50 issues and 50 PRs updated in the last 24 hours. The project is heavily focused on **architecture RFCs** (runtime ownership, WASM plugins, sandboxing) and **security-hardening PRs**, particularly around Git shell policy and risk-profile configuration. The maintainer decision queue ([#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)) is actively working through a backlog of high-priority RFCs, and there is clear momentum on the **"everything is a plugin"** WASM initiative, with multiple stacked PRs awaiting merge. While activity is extremely high, there are also **bottleneck signals**: 48 of 50 PRs remain open, and many carry the `needs-author-action` flag, suggesting that review bandwidth may be a limiting factor. No new releases were cut today, indicating that merging and stabilization are prioritized over shipping.

---

## 2. Releases

**No new releases were published in the last 24 hours.** The project is in a heavy pre-release integration phase, likely consolidating the significant RFC and security work before cutting the next version.

---

## 3. Project Progress

Two PRs were closed/merged in the last 24 hours:

- **[#9415 — docs(architecture): record execution-tree budget ownership](https://github.com/zeroclaw-labs/zeroclaw/pull/9415)** *(merged)* — Adds ADR-014, documenting execution-tree budget ownership. This is the second ADR in a stacked series (#9361 first), part of the project's broader effort to restore the ADR baseline and audit accepted RFC decision records ([#8691](https://github.com/zeroclaw-labs/zeroclaw/issues/8691)).

- **[#9578 — fix(config): honour a configured multimodal.max_images, and say when it is clamped](https://github.com/zeroclaw-labs/zeroclaw/pull/9578)** *(closed)* — Corrects a bug where `multimodal.max_images` was silently clamped to 16. The fix raises the sanity ceiling to 100 and now reports clamping explicitly instead of failing silently. The PR was tagged `stale-candidate`, indicating it may have been closed due to inactivity before merge, which is worth investigating.

**In-flight Feature Advancement:**
- **WASM Plugin Architecture** is the dominant theme. PRs [#10146](https://github.com/zeroclaw-labs/zeroclaw/pull/10146) (activate logical channel instances), [#9128](https://github.com/zeroclaw-labs/zeroclaw/pull/9128) (scoped tool secret service), and [#9129](https://github.com/zeroclaw-labs/zeroclaw/pull/9129) (coherent channel config services) are all open and progressing. These directly feed the RFC at [#10076](https://github.com/zeroclaw-labs/zeroclaw/issues/10076) and the tracker at [#8850](https://github.com/zeroclaw-labs/zeroclaw/issues/8850).

---

## 4. Community Hot Topics

The most active discussions are dominated by **architecture-level RFCs with security implications**:

- **[#9487 — RFC: Runtime-owned conversation sessions and transport surface adapters](https://github.com/zeroclaw-labs/zeroclaw/issues/9487)** *(22 comments)* — The most active issue. The RFC has gone through two revisions and is converging on an ownership boundary. It's a foundational architectural decision that will affect runtime, channels, and gateway—explaining the high engagement and `needs-maintainer-review` flag.

- **[#10118 — Rust anti-slop policy debt remediation tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/10118)** *(16 comments)* — A new tracker coordinating cleanup of 307 anti-slop candidates across 1,078 Rust files. This signals the project is prioritizing code-quality and maintainability, which is healthy for long-term sustainability.

- **[#6850 — RFC: Decouple memory lifecycle policy from storage backends](https://github.com/zeroclaw-labs/zeroclaw/issues/6850)** *(14 comments)* — Long-running RFC (created May 22) that continues to draw engagement. The community is clearly invested in the memory subsystem's architecture, which is a core differentiator for the project.

- **[#8780 — RFC: Realtime speech-to-speech channel for Gemini Live](https://github.com/zeroclaw-labs/zeroclaw/issues/8780)** *(14 comments)* — Revised to a broker contract in v2. The community want stateful real-time voice capabilities, not just stateless tool-calling.

**Underlying Need:** These threads reveal a community pushing for **production-grade, composable systems**—decoupled memory, realtime channels, plugin-based extensibility, and clean ownership boundaries. The engagement pattern suggests experienced users designing for enterprise-scale deployments.

---

## 5. Bugs & Stability

**High Severity:**
- **[#10068 — Interactive agent session caps context at 32,000 tokens, ignoring max_context_tokens = 131072](https://github.com/zeroclaw-labs/zeroclaw/issues/10068)** — S2 severity, `status:in-progress`. The runtime has a hard-coded 32k token cap that overrides configured limits. This is a critical user-facing bug affecting long-context use cases. Fix is in progress but no PR is linked yet.
- **[#10106 — Exact proxy selectors reject supported transcription services](https://github.com/zeroclaw-labs/zeroclaw/issues/10106)** — S2 severity, `status:in-progress`. Proxy-aware clients use service keys not recognized by the exact selector, breaking transcription via proxy for Groq, Deepgram, AssemblyAI, and Google.

**Medium Severity:**
- **[#10074 — SECURITY.md documents a removed CI job](https://github.com/zeroclaw-labs/zeroclaw/issues/10074)** — Documentation drift; container security checks are now convention, not enforced by CI. Risks future regressions.
- **[#9016 — OpenAI tool turns fail when Chat Completions rejects reasoning effort](https://github.com/zeroclaw-labs/zeroclaw/issues/9016)** — S1 severity, **closed yesterday**. This was resolved—likely via a provider fix.

**Fixed/Closed:**
- **[#10194 — PR reviewer publishes in-flight results after the PR merges](https://github.com/zeroclaw-labs/zeroclaw/issues/10194)** — Closed. CI tooling race condition.
- **[#10111 — Windows: Entry Point Not Found — TaskDialogIndirect](https://github.com/zeroclaw-labs/zeroclaw/issues/10111)** — Closed as duplicate. A known Windows installer issue.

**Fix PRs in flight for older bugs:**
- [#9748](https://github.com/zeroclaw-labs/zeroclaw/pull/9748) addresses stale provider refresh mutation (#9719)
- [#9746](https://github.com/zeroclaw-labs/zeroclaw/pull/9746) addresses session tool per-agent ownership scoping
- [#9745](https://github.com/zeroclaw-labs/zeroclaw/pull/9745) adds per-agent attribution to the knowledge graph
- [#9678](https://github.com/zeroclaw-labs/zeroclaw/pull/9678) and [#9635](https://github.com/zeroclaw-labs/zeroclaw/pull/9635) harden Git shell policy and risk classification
- [#9447](https://github.com/zeroclaw-labs/zeroclaw/pull/9447) classifies incomplete Anthropic terminal responses

---

## 6. Feature Requests & Roadmap Signals

Strong signals exist for the next release's direction:

**High-Priority In-Flight Features:**
- **WASM Plugin Architecture (likely next major feature):** RFCs [#10076](https://github.com/zeroclaw-labs/zeroclaw/issues/10076) and [#8398](https://github.com/zeroclaw-labs/zeroclaw/issues/8398), trackers [#8850](https://github.com/zeroclaw-labs/zeroclaw/issues/8850), and the corresponding PRs (#10146, #9128, #9129) all point to plugin-based extensibility shipping soon.

**Bundled Defaults Improvements** (from JordanTheJet, both accepted, likely in next patch):
- [#10168 — Enable the stall watchdog by default](https://github.com/zeroclaw-labs/zeroclaw/issues/10168) — Prevents hung turns by default.
- [#10166 — Default stream_mode to partial](https://github.com/zeroclaw-labs/zeroclaw/issues/10166) — Replies stream by default, massively improving perceived latency.

**New Capabilities:**
- **[#8780 — Realtime speech-to-speech channel (Gemini Live)](https://github.com/zeroclaw-labs/zeroclaw/issues/8780)** — Voice-first interaction is a clear roadmap item.
- **[#10025 — Ephemeral agent swarms with crush-style TUI](https://github.com/zeroclaw-labs/zeroclaw/issues/10025)** — Orchestrated multi-agent teams around a single goal.
- **[#10069 — Agent Portability](https://github.com/zeroclaw-labs/zeroclaw/issues/10069)** — Export/import agents across deployments.
- **[#4668 — MariaDB memory backend](https://github.com/zeroclaw-labs/zeroclaw/issues/4668)** — Enterprise database support; accepted and `no-stale`, a strong candidate for inclusion.

**Prediction:** The next release will likely emphasize **plugin architecture activation**, **default UX improvements** (streaming, stall watchdog), and **security hardening** for Git and shell policy. Features like swarms and speech-to-speech are likely 1–2 releases out.

---

## 7. User Feedback Summary

**Pain Points:**
- **Context limits are confusing and restrictive:** The 32k token cap ([#10068](https://github.com/zeroclaw-labs/zeroclaw/issues/10068)) shows users are hitting context limits that don't match their configuration expectations; this is a top priority to fix.
- **Deployment friction:** Windows users struggle with the installer ([#10111](https://github.com/zeroclaw-labs/zeroclaw/issues/10111)); users on MariaDB infrastructure feel excluded ([#4668](https://github.com/zeroclaw-labs/zeroclaw/issues/4668)).
- **Proxy configuration gaps:** Transcription services fail when used through proxies ([#10106](https://github.com/zeroclaw-labs/zeroclaw/issues/10106)), a blocker for enterprise users who rely on proxies.
- **Docs/CI drift:** The SECURITY.md inaccuracy ([#10074](https://github.com/zeroclaw-labs/zeroclaw/issues/10074)) erodes trust in documented enforcement mechanisms.

**Positive Signals:**
- The **rapid closure** of the Windows debug support issue and the CI race condition shows the maintainers are responsive.
- The active engagement on RFCs suggests a **healthy, expert community** that is co-designing the architecture.

---

## 8. Backlog Watch

Items that have been waiting for maintainer action (all have `needs-maintainer-review` or `needs-author-action` and are flagged as high-risk):

- **[#9487 — RFC: Runtime-owned conversation sessions](https://github.com/zeroclaw-labs/zeroclaw/issues/9487)** — 3+ weeks old, 22 comments, revision 2 submitted. This is the **highest-priority architectural decision pending**. The community has iterated; maintainers need to respond to revision 2.
- **[#8780 — RFC: Gemini Live speech-to-speech channel](https://github.com/zeroclaw-labs/zeroclaw/issues/8780)** — 6+ weeks old, rewritten to broker contract 5 days ago. Needs maintainer decision.
- **[#6850 — RFC: Decouple memory lifecycle policy](https://github.com/zeroclaw-labs/zeroclaw/issues/6850)** — **3 months old**, 14 comments, still `needs-maintainer-review`. This is the oldest unreviewed critical RFC.
- **[#6996 — RFC: Granular sandbox policy](https://github.com/zeroclaw-labs/zeroclaw/issues/6996)** — 2.5 months old, flagged `needs-author-action`. This is a security-critical architecture decision.
- **PR bottleneck:** 48 of 50 PRs are open. Particularly concerning are the **priority:p1** security PRs: [#9753](https://github.com/zeroclaw-labs/zeroclaw/pull/9753) (risk-profile allowed_tools fail-open), [#9678](https://github.com/zeroclaw-labs/zeroclaw/pull/9678) (Git shell policy), [#9637](https://github.com/zeroclaw-labs/zeroclaw/pull/9637) (CI exception guard). All carry `needs-author-action`, suggesting **authors, not reviewers, are the bottleneck**—these need maintainer nudges to unblock.
- **Stale-candidate risk:** [#9578](https://github.com/zeroclaw-labs/zeroclaw/pull/9578) was closed as a stale candidate just as it was being addressed—there may be a **process gap** where legitimate fixes are being closed due to multi-week review queues.

---

*This digest was generated from GitHub data pulled on 2026-08-21.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*