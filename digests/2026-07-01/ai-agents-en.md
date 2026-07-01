# OpenClaw Ecosystem Digest 2026-07-01

> Issues: 285 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-01 02:07 UTC

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

# OpenClaw Project Digest — 2026-07-01

## 1. Today's Overview

OpenClaw shows **sustained high activity** with 285 issues and 500 PRs updated in the last 24 hours, indicating a large, actively maintained open-source AI agent ecosystem. The project's maintainers are processing a substantial volume of contributions, with **84 merged/closed PRs** today. A new patch release (v2026.6.11) shipped, specifically targeting "rough edges" around reliability — misplaced replies, stuck sends, reconnects, and model setup failures. However, the high number of open PRs (416) and the prevalence of `needs-maintainer-review` labels across both issues and PRs suggest the team is **operating near or beyond capacity**, with significant backlog pressure.

## 2. Releases

**New release: v2026.6.11 (openclaw 2026.6.11)**

- **Focus**: Reliability polish — fixing "rough edges that make OpenClaw feel less dependable"
- **Key fixes included**:
  - Misplaced replies
  - Stuck message sends
  - Reconnection issues
  - Model setup failures
  - Safer admin defaults
- **Breaking changes**: None indicated
- **Migration notes**: Standard patch release; users can `npm install -g openclaw@latest`

[Full release notes](https://docs.openclaw.ai/releases/2026.6.11)

## 3. Project Progress

**84 PRs merged/closed today.** Notable merged/closed items include:

- **PR #68936** (CLOSED) — `Autofix: add PR review autofix pipeline + Windows daemon` — adds automated review comment resolution using Claude Agent SDK, plus a Windows background daemon for gateway supervision
- **Issue #84674** (CLOSED) — Fix for Telegram isolated ingress spool remaining blocked by stale `.processing` claim after gateway recreate
- **Issue #84256** (CLOSED) — Fix for `openclaw plugins update --all` downgrading manually-updated npm plugins
- **Issue #96125** (CLOSED) — Fix for wiki_apply & wiki_lint YAML parsing errors (regression fix)
- **Issue #98297** (CLOSED) — Fix for iOS app silently rejecting QR setup codes with LAN `ws://` URLs
- **Issue #97970** (CLOSED) — Fix for `openclaw update` auto-completing `gateway.bind` as `lan` conflicting with `auth.mode: none`
- **Issue #89589** (CLOSED) — Fix for state directory permissions being relaxed to 0775 by update-check JSON writes
- **Issue #97935** (CLOSED) — Fix for skill_workshop proposal index being session-scoped (proposals invisible across sessions)

Significant open PRs moving forward:
- **PR #98224** (ready for maintainer look) — Fixes stray punctuation before `NO_REPLY` silent-reply token detection
- **PR #87917** (ready for maintainer look) — Fixes `sessions --json` dropping subagent lineage metadata
- **PR #98326** (ready for maintainer look) — Fixes CI runtime artifacts missing resources
- **PR #98328** (OPEN) — Fixes CLI session history rendering all user messages as hardcoded `User:` label

## 4. Community Hot Topics

### Most Active Issues (by comment count)

1. **#9443** — [OPEN] **Request: Prebuilt Android APK releases** (26 comments, 3 👍)
   - *Needs analysis*: Users want precompiled APK downloads in GitHub releases. The Android companion app source code exists but requires compilation, creating a **significant barrier for non-developer users** wanting mobile deployment.
   - [GitHub](https://github.com/openclaw/openclaw/issues/9443)

2. **#48003** — [OPEN] **Steer mode does not inject messages mid-turn for main sessions** (14 comments, 3 👍)
   - *Needs analysis*: Diamond-ranked session-state bug. `messages.queue.mode: "steer"` fails to inject user messages into active running turns — core mechanism for real-time interaction patterns.
   - [GitHub](https://github.com/openclaw/openclaw/issues/48003)

3. **#84516** — [OPEN] **Codex app-server: long agent replies silently truncated at ~1000-1100 chars** (11 comments, 2 👍)
   - *Needs analysis*: Critical P1 bug affecting Codex/OAuth agent users. Silent truncation with no error signal (`stop=null, aborted=false`) — model appears to complete but content is lost.
   - [GitHub](https://github.com/openclaw/openclaw/issues/84516)

4. **#84583** — [OPEN] **cron announce delivery triggers EmbeddedAttemptSessionTakeoverError** (9 comments, 3 👍)
   - *Needs analysis*: Cron job delivery conflicts with active user chat sessions, causing takeover errors.
   - [GitHub](https://github.com/openclaw/openclaw/issues/84583)

5. **#94228** — [OPEN] **Native Anthropic path: replaying historical thinking blocks bricks long tool-use threads** (9 comments, 2 👍)
   - *Needs analysis*: Anthropic provider sessions brick permanently with `Invalid signature in thinking block` — blocks entire thread on legacy thinking blocks.
   - [GitHub](https://github.com/openclaw/openclaw/issues/94228)

### Most Active PRs (by discussion)

- **PR #97106** — `fix(exec): distinguish one-shot from ask=always in approval prompt` — addresses misleading approval policy messaging when shell redirection is present
- **PR #98134** — `fix: clear timeout timer in Tailscale binary probe Promise.race` — part of a broader resource leak fix series
- **PR #95644** — `feat(cli): add --file option to image generate command` — enabling CLI workflows for image-conditioned generation
- **PR #98328** — `fix(cli-runner): use sender metadata in CLI session history user labels` — improving group chat participant distinguishability
- **PR #98329** — `fix(feishu): route image/file replies through the same withdrawn-target fallback as text/card` — addressing media reply loss

## 5. Bugs & Stability

### Critical / P0

- **#84882** — [OPEN, P0] **memory-core Dreaming silently deletes daily memory files** (memory/YYYY-MM-DD.md)
  - *Severity*: **Data loss**. The `normalized recall artifacts` pipeline step silently deletes memory files.
  - *Status*: Open; linked PR exists; needs maintainer review and product decision
  - [GitHub](https://github.com/openclaw/openclaw/issues/84882)

### High Severity (P1 — Session State / Message Loss / Crash Loop)

- **#98239** — `/pair qr` can change `gateway.bind` and break Tailscale Serve webchat (6 comments)
  - *Impact*: Security + session state — QR-based pairing alters gateway bindings
  - [GitHub](https://github.com/openclaw/openclaw/issues/98239)

- **#96704** — Managed browser cookies never persist to disk (login sessions lost on restart) — refile of #15645 (6 comments)
  - *Impact*: Data loss + session state — cookies in-memory only
  - [GitHub](https://github.com/openclaw/openclaw/issues/96704)

- **#92433** — Subagent completion silently dropped when announce steers into requester run ending early (6 comments)
  - *Impact*: Message loss
  - [GitHub](https://github.com/openclaw/openclaw/issues/92433)

- **#98311** — [NEW] Feishu image/file replies lose media on withdrawn/recalled reply targets (3 comments)
  - *Impact*: Message loss — text replies survive but media replies silently fail
  - [**Fix PR exists**: #98329](https://github.com/openclaw/openclaw/pull/98329)
  - [GitHub](https://github.com/openclaw/openclaw/issues/98311)

- **#84569** — WhatsApp session stalls on long model_call (incomplete turn, reply never delivered) (6 comments)
  - *Impact*: Session state + message loss
  - [GitHub](https://github.com/openclaw/openclaw/issues/84569)

- **#98244** — [NEW] OpenAI Responses API streaming: 120-second timeout after successful completion (3 comments)
  - *Impact*: Performance — streaming continues iterating after `response.completed` event
  - [GitHub](https://github.com/openclaw/openclaw/issues/98244)

### Noteworthy Regressions

- **#96125** (CLOSED) — wiki_apply & wiki_lint YAML parsing regression — **fixed today**
- **#84536** — Preemptive context overflow silently kills embedded sessions without user notification
- **#84516** — Codex app-server long replies truncated at ~1000 chars — confirmed on 2026.6.x releases

## 6. Feature Requests & Roadmap Signals

### Likely for Next Release

1. **Prebuilt Android APK releases** (#9443) — High demand (26 comments, 3 👍). Priority tier "P2" but user-visible barrier. **Prediction**: Likely addressed in a minor release within 1-2 cycles as it's a straightforward packaging issue.

2. **CLI `--file` option for image generate** (PR #95644) — Already implemented, awaiting review. **Prediction**: Will merge in v2026.6.12 or v2026.7.x.

3. **Multiple Azure/Teams bots on single Gateway** (#71058) — Enterprise deployment capability, P2, product decision needed. **Prediction**: Medium-term roadmap item (v2026.Q3).

4. **Signed marketplace feed config** (PR #98316) — New signed mode for marketplace feed verification with Ed25519 keys. Active PR under review. **Prediction**: May land in v2026.7.x.

### Emerging Signals

- **Slack per-thread context customization** (#97341) — New P3 enhancement for threaded conversation isolation. Indicates growing Slack enterprise adoption.
- **DingTalk external channel catalog** (PR #81736) — Chinese enterprise platform integration. Signals expansion into Asian enterprise markets.
- **UI i18n localization** (PR #82514) — Phase 1 Settings toolbar localization complete for 18 locales. Indicates internationalization push.
- **Discord canvas-first Activities support** (PR #65205) — Long-standing XL-sized PR for Discord gaming/integration features.

## 7. User Feedback Summary

### Pain Points Expressed

1. **Mobile deployment friction** — Prebuilt Android APK demand high; iOS QR setup rejects LAN `ws://` URLs (#98297, just fixed). Users want "download and run" without compilation.

2. **Silent failures erode trust** — Multiple reports of messages silently dropped (#84516, #92433, #84569), memory files silently deleted (#84882), and sessions killed without notification (#84536). **Most consistent thread in feedback**: "OpenClaw does something without telling me."

3. **Update-induced breakage** — `openclaw update` auto-completing `gateway.bind` as `lan` causing conflict with `auth.mode: none` (#97970, just fixed). Users express frustration that updates introduce unexpected configuration changes.

4. **Plugin management confusion** — `plugins update --all` downgrading manually updated plugins (#84256, just fixed). Users want "update to latest" semantics.

5. **Event loop saturation / startup hangs** — Multiple reports (#84771, #84983, #84610) of gateway becoming unresponsive for 28-64 seconds during startup or cron job execution.

6. **Provider-specific reliability issues** — xAI/Grok "could not decrypt encrypted_content" errors tripping circuit breakers (#97925), Google Vertex AI key rotation not working (#97314), DeepSeek V4 cost display showing ¥0.00 (#97054).

### Satisfaction Signals

- **Quick fix turnaround**: Several bugs reported within the last 24-48 hours already have fix PRs (e.g., #98311 → PR #98329, #98297 closed same day)
- **Proactive fix release**: v2026.6.11 explicitly addresses "rough edges that make OpenClaw feel less dependable" — maintains show they hear user frustration
- **Documentation improvements**: PR #98318 adds missing Matrix streaming config docs, PR #98326 fixes build artifact completeness

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Priority | Why Stuck |
|-------|-----|----------|-----------|
| [#71058](https://github.com/openclaw/openclaw/issues/71058) — Multiple Azure/Teams bots | 68 days | P2 | Needs product decision |
| [#58775](https://github.com/openclaw/openclaw/issues/58775) — Google Vertex provider merged into Google transport path | 91 days | P2 | Needs live reproduction; linked PR open |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) — "Cannot convert undefined or null to object" with google-vertex/gemini | 117 days | P1 (regression) | Needs live reproduction + product decision |
| [#81594](https://github.com/openclaw/openclaw/issues/81594) — Text /steer targets slash lane instead of direct lane | 47 days | P2 | Stale; linked PR open |
| [#81099](https://github.com/openclaw/openclaw/issues/81099) — claude-cli backend AskUserQuestion tool never returns result | 49 days | P1 (stale) | Source reproduction available but stale |
| [#77093](https://github.com/openclaw/openclaw/issues/77093) — Gmail Pub/Sub webhooks not processing in Docker + Tailscale Funnel | 57 days | P2 (regression, stale) | Needs live reproduction |

### PRs Needing Maintainer Review

| PR | Age | Size | Risk | Notes |
|----|-----|------|------|-------|
| [#67080](https://github.com/openclaw/openclaw/pull/67080) — Narrow gateway route loads from manifests | 77 days | L | 🚨 compatibility, security, availability | Waiting on author after extended period |
| [#65205](https://github.com/openclaw/openclaw/pull/65205) — Discord Activities support | 80 days | XL | 🚨 compatibility, security, availability | Waiting on author |
| [#82514](https://github.com/openclaw/openclaw/pull/82514) — UI i18n Settings toolbar localization | 46 days | XL | 🚨 automation | Ready for maintainer look (proof supplied) |
| [#95622](https://github.com/openclaw/openclaw/pull/95622) — WhatsApp QA scenario hardening | 9 days | XL | 🚨 automation, message-delivery | In "ready for maintainer look" stage |
| [#73724](https://github.com/openclaw/openclaw/pull/73724) — Avoid false local gateway unreachable on probe timeout | 64 days | XL | 🚨 compatibility, security | Has automerge label but pending human review |

### Assessment

The **backlog pressure is significant**. Several P1 bugs (some with diamond/platinum ratings) have been open for 2-4 months, and numerous PRs with "ready for maintainer look" status remain unreviewed for weeks. The `needs-product-decision` label appears on **12 of the top 50 issues**, suggesting a **product strategy bottleneck** for feature-level decisions. The team appears to prioritize recently filed P1 crashes/hangs over older stability issues, though the current fix velocity (84 closed PRs today) is healthy.

---

## Cross-Ecosystem Comparison

Here is a cross-project comparison report of the open-source personal AI assistant ecosystem based on the provided community digest summaries.

---

## Cross-Project Comparison Report: AI Agent Ecosystem

**Date:** 2026-07-01
**Prepared for:** Technical decision-makers and developers

---

### 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem is currently characterized by a **high-velocity, stability-focused iteration cycle** across all major projects. A clear industry consensus has emerged around three core priorities: **runtime reliability** (fixing silent failures and data loss), **channel expansion** (Discord, WeChat, Telegram, and enterprise messaging), and **agent memory management** (retrieval, consolidation, and contextual overflow prevention). The ecosystem is bifurcating between **all-in-one monorepos** (OpenClaw, Hermes Agent) and **lightweight modular frameworks** (NanoBot, PicoClaw), with the former bearing significant technical debt from rapid scaling. Crucially, **security vulnerabilities** (DNS rebinding, symlink escapes, SSRF) are being surfaced across projects, indicating that the security posture of these locally-hosted agents warrants immediate developer attention.

---

### 2. Activity Comparison

| Project | Issues (Updated/Closed) | PRs (Updated/Merged) | Release Today | Ecosystem Health Score |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 285 / High | 500 / 84 merged | ✅ v2026.6.11 | 🟡 High capacity, significant backlog |
| **NanoBot** | 12 / 7 closed | 66 / 34 merged | ❌ | 🟢 High velocity, healthy |
| **Hermes Agent** | 50 / 15 closed | 50 / 15 merged | ❌ | 🟢 High activity, stability mode |
| **NanoClaw** | N/A | 14 / 10 merged | ❌ | 🟢 Strong, multi-contributor |
| **CoPaw** | 23 / 7 closed | 50 / 21 merged | ❌ | 🟢 High velocity, pre-release |
| **ZeroClaw** | 50 / 4 closed | 50 / 4 merged | ❌ | 🟡 Heavy RFC phase, implementation lag |
| **IronClaw** | 22 / - | 50 / 25 merged | ❌ | 🟢 High-intensity engineering |
| **PicoClaw** | 6 / - | 7 / 3 merged | ✅ Nightly (unstable) | 🟡 Stable, some new bugs |
| **NullClaw** | 2 / - | 4 / 4 merged | ❌ | 🟢 Small, responsive |
| **LobsterAI** | - / - | 14 / 14 merged | ✅ v2026.6.30 | 🟢 Very high, fix-driven |
| **Moltis** | 0 / 0 | 3 / 2 merged | ❌ | 🔴 Maintenance-only |
| **TinyClaw** | No activity | No activity | ❌ | ⚪ Inactive |
| **ZeptoClaw** | No activity | No activity | ❌ | ⚪ Inactive |

---

### 3. OpenClaw's Position

**Advantages:**
- **Largest community & feature surface**: With 285 issues and 500 PRs touched in 24 hours, OpenClaw has the most extensive ecosystem, including advanced features (Codex/OAuth, steer mode, Tailscale Serve) that competitors lack.
- **Proactive reliability release**: The v2026.6.11 patch explicitly addressed user trust ("rough edges that make OpenClaw feel less dependable"), demonstrating responsive maintainership.
- **Enterprise-grade feature set**: Tailscale integration, multiple Azure bots, and gateway supervision (Windows daemon) target self-hosted power users and small teams.

**Disadvantages:**
- **Operational capacity risk**: The `needs-maintainer-review` label on numerous issues and PRs, combined with a 416 open PR backlog, suggests the team is bottlenecked.
- **Silent failure reputation**: Multiple reports of data loss (memory files, truncated messages) without user notification is the most consistent pain point, eroding trust despite the fix velocity.
- **Higher complexity burden**: Compared to NanoBot's "lightweight codebase" praise, OpenClaw's monorepo density creates a steeper learning curve for contributors and users alike.

**Technical Approach:** OpenClaw is an **opinionated, all-in-one agent runtime** with built-in gateway servers, plugin registries, and multi-protocol transport (Matrix, Tailscale, QR pair). This contrasts with NanoBot’s modular Python framework and NanoClaw’s security-hardened container approach.

---

### 4. Shared Technical Focus Areas

The following requirements are emerging across **three or more** projects, indicating industry-wide priorities:

| Requirement | OpenClaw | NanoBot | Hermes | CoPaw | NanoClaw | IronClaw | ZeroClaw |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Tool Execution Reliability** | ✅ (context overflow, parallel tools) | ✅ (emergency truncation) | ✅ (tool ID corruption) | ✅ (loop detection) | | | ✅ (MCP visibility) |
| **Session State Integrity** | ✅ (subagent lineage, session takeover) | ✅ (dream memory deletion) | ✅ (session isolation, key collisions) | ✅ (cancel envelope) | | ✅ (turn-state CAS) | ✅ (provider priority) |
| **Configuration Hygiene** | ✅ (update auto-complete bug) | | | ✅ (governance OFF mode) | | | ✅ (channel doctor false positives) |
| **Cron / Scheduled Tasks** | ✅ (cron delivery takeover) | ✅ (heartbeat channel delivery) | ✅ (cron context drift) | ✅ (heartbeat timeout) | | ✅ (runner lease expiration) | ✅ (per-job memory flag) |
| **Channel / Adapter Parity** | ✅ (Telegram, Discord, Feishu) | ✅ (WhatsApp, Signal) | ✅ (Mattermost, Telegram) | ✅ (DingTalk, WeChat, Feishu) | ✅ (Discord, WeChat, Signal) | | ✅ (Git forge, Telegram) |
| **Security Hardening** | ✅ (SSRF guard bypass fixed) | ❌ (DNS rebinding open) | | ✅ (bubblewrap sandbox) | ✅ (symlink escape fixed) | ✅ (Dependabot bumps) | ✅ (plugin permission model) |
| **Memory & Context Engineering** | ✅ (daily memory deletion bug) | ✅ (eager consolidation, Dream) | | ✅ (reranker, two-stage retrieval) | | ✅ (tool disclosure) | ✅ (SQLite degradation fixed) |
| **Mobile & Desktop Deploy** | ✅ (Android APK request, iOS QR fix) | ✅ (nssm / Windows service) | ✅ (Windows stability overhaul) | ✅ (Linux AppImage request) | | | ✅ (Rust→Wasm UI discussion) |

**Notable gap:** **Cross-project observability** (OpenTelemetry, robust logging) is only surfaced in IronClaw and ZeroClaw, while others struggle with generic error messages (`invalid_input`) or silent failures.

---

### 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | CoPaw | NanoClaw | IronClaw |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Primary User** | Power user / self-hoster | Python developer | Asia-Pacific enterprise | Security-conscious dev | NEAR ecosystem / production |
| **Architecture** | Monorepo, Node.js/TS agent | Lightweight Python framework | Python, Qwen ecosystem | Rust core, container-first | Rust, CI-heavy, Reborn backend |
| **Security Posture** | Reactive (fixes after reports) | Vulnerable (open DNS rebinding) | Proactive (bubblewrap, governance) | Proactive (container sandbox, symlink fix) | Moderate (dependency bumps) |
| **Channel Strategy** | Broad (Telegram, Discord, Feishu, WhatsApp, iMessage) | Narrow (WhatsApp, Signal, Telegram) | Focused (DingTalk, WeChat, Feishu) | Expanding (Discord, WeChat, Matrix) | Internal (Slack, Telegram) |
| **Automation Depth** | Cron, steer mode, subagents | Heartbeat tasks, A2A delegation | Cron, loop engineering | Cron, scheduled news | Routines, CAS contention |
| **Market Focus** | Global, developer-first | Developer & ML/scientific | China enterprise | Security-conscious OSS | NEAR AI cloud ecosystem |
| **Innovation Signal** | Tailscale Serve, Codex OAuth | A2A multi-agent, per-session model presets | Memory reranker, gate architecture | Document rendering sandbox, E2EE Matrix | Progressive tool disclosure, Trace Commons |

**Key insight:** NanoBot is positioning as the **easy-to-understand, Python-native alternative** to OpenClaw's complexity, explicitly praised by users for its lighter codebase. CoPaw is carving out the **China enterprise** niche with deep DingTalk/WeChat/Feishu integration. NanoClaw is the **security-first option** with the most aggressive container isolation and sandboxing.

---

### 6. Community Momentum & Maturity

| Tier | Project | Characteristics |
| :--- | :--- | :--- |
| **T1: Rapid Iteration** | OpenClaw, NanoBot, CoPaw, IronClaw | High PR merge velocity, frequent releases, large community, active bug tracking. OpenClaw is the largest but showing capacity strain. |
| **T2: Steady Growth** | Hermes Agent, NanoClaw | Strong contributor base, focused on stabilization. Hermes is closing old bugs rapidly. NanoClaw is in a feature-acceleration phase. |
| **T3: Stable Maintenance** | PicoClaw, NullClaw, LobsterAI | Smaller teams, responsive but lower volume. PicoClaw has new bugs raising concerns. NullClaw shows zero open PRs—efficient but quiet. |
| **T4: Inactive / Dormant** | Moltis, TinyClaw, ZeptoClaw | No meaningful development. Moltis is dependency-only. TinyClaw and ZeptoClaw have zero activity. |

**Maturity signal:** All T1 projects are currently **prioritizing reliability over new features**. OpenClaw released a "rough edges" patch. CoPaw and IronClaw are closing bugs from pre-release cycles. This suggests the ecosystem is maturing from "move fast" to "build trust."

---

### 7. Trend Signals

*Extracted from community feedback across projects, with value for AI agent developers.*

1.  **"Silent failures erode trust faster than bugs."** The #1 pain point across OpenClaw, Hermes, and NanoClaw is data loss without notification (memory files, truncated messages, invisible tools). **Developer takeaway**: When in doubt, log and notify. Failures should be visible errors, not silent omissions.

2.  **Multi-agent (A2A) is the next architecture wave.** NanoBot’s A2A delegation (PR #4571) and OpenClaw’s subagent lineage work point to a future where agents spawn child agents for specific tasks. **Developer takeaway**: Design agent loops with delegation primitives now; expect demand for depth guards and context isolation.

3.  **Self-hosted agents need enterprise-grade security.** DNS rebinding (NanoBot), symlink escapes (NanoClaw), and SSRF bypasses (OpenClaw) are being discovered in the wild. **Developer takeaway**: SSRF validation, sandboxing (bubblewrap/container), and permission models are table stakes. Security is not optional for locally-hosted infrastructure.

4.  **Channel reliability is the top engagement driver.** Feishu long messages, WhatsApp media drops, iMessage disconnects, and Telegram silent crashes dominate bug reports. **Developer takeaway**: A multi-platform agent is only as good as its weakest adapter. Invest in adapter resilience with retry, reconnection, and deduplication logic.

5.  **Cost optimization is emerging as a core feature.** NanoBot's context compression (PR #4581), IronClaw's progressive tool disclosure (PR #5149), and CoPaw's memory reranker all target token budget reduction. **Developer takeaway**: Models are expensive; tools that reduce token consumption (smart retrieval, tool pruning, context dedup) will be key differentiators.

6.  **Per-session and per-cron model overrides are becoming standard.** Users want cheap models for heartbeat tasks and expensive models for coding. This pattern appears in NanoBot, CoPaw, and ZeroClaw. **Developer takeaway**: Configuration should support granular model selection, not just a global default.

7.  **Windows and mobile deployment are pain points for all.** From Windows crash loops (Hermes) to Android APK requests (OpenClaw) to nssm service bugs (NanoBot), desktop/mobile parity is consistently underinvested relative to server-side features. **Developer takeaway**: The "always-on local agent" use case is real but underserved. Targeting Windows and Android is a strong competitive moat.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-01

## 1. Today's Overview

The NanoBot project is in a period of **very high activity**, with 66 pull requests updated in the last 24 hours (34 merged/closed) and 12 issues updated (7 closed). This is a substantially higher-than-average day, indicating either a planned release cycle or a coordinated community contribution wave. No formal releases were cut today, though the sheer volume of merged PRs suggests a significant feature batch may be imminent. The project's maintainers and core contributors are deeply engaged across memory consolidation, agent reliability, WhatsApp integration, and configuration hygiene. The overall health signal is strong, with rapid issue closure and responsive PR reviews.

**Key metric**: 34 PRs merged/closed in 24h, 7 issues closed — indicates disciplined merge velocity.

---

## 2. Releases

**No releases published for 2026-07-01.** The last release remains the latest published version on PyPI/Docker. Given the high merge volume, a new release may be imminent; watch for a tagged release in the coming days as these changes stabilize.

---

## 3. Project Progress

The following significant PRs were merged/closed today, representing real advances:

### Agent & Exec Improvements
- **[#4608]** `fix(agent): add emergency tool result truncation to prevent context overflow` — PR by alazycat, adds a safety valve when multiple tools in one turn produce large results that would exceed context window budget. **Critical for agent reliability** when models perform parallel searches or other data-heavy tool calls.
- **[#4610]** `refactor(tools): use structured tool error results` — Merged refactor to introduce `ToolResult` as a structured contract for failure, replacing brittle string-prefix checks (`result.startswith("Error")`) across the codebase.

### CLI/Setup improvements
- **[#4573]** `fix(cli): allow oauth login to be/set main provider` — Makes OAuth providers (GitHub, Google, etc.) settable as the main provider directly from `nanobot provider login`, solving a long-standing UX pain point where users didn't know their OAuth provider wasn't activated by default.

### WebUI
- **[#4609]** `fix(webui): keep idle compaction out of session recency` — Prevents AutoCompact from incorrectly updating session `updated_at`, which was causing sessions to appear "recent" even when idle. Fixes a confusing WebUI sorting bug.

### Network & Security
- **No security-related merges today**, but note Issue [#4611] (DNS rebinding TOCTOU) is still **open** without a fix PR.

---

## 4. Community Hot Topics

### Most Active Issues
| Issue | Title | Comments | Reactions | Status |
|-------|-------|----------|-----------|--------|
| [#4418](https://github.com/HKUDS/nanobot/issues/4418) | Feature: Heartbeat tasks deliver results to correct channel | 4 | — | **CLOSED** ✅ |
| [#4604](https://github.com/HKUDS/nanobot/issues/4604) | Anthropic OAuth | 2 | — | OPEN |
| [#4513](https://github.com/HKUDS/nanobot/issues/4513) | nssm Windows service /restart bug | 2 | — | CLOSED ✅ |
| [#1023](https://github.com/HKUDS/nanobot/issues/1023) | Provider login tokens not persisted (4 months old!) | 1 | 2 👍 | CLOSED ✅ |

### Most Active PRs
| PR | Title | Comments | Status |
|----|-------|----------|--------|
| [#4534](https://github.com/HKUDS/nanobot/pull/4534) | Agent reliability, verification, exec services | — | OPEN |
| [#4554](https://github.com/HKUDS/nanobot/pull/4554) | Dream duplicate skill write guard | — | OPEN |
| [#4581](https://github.com/HKUDS/nanobot/pull/4581) | Context usage optimization | — | OPEN |

### Analysis of Underlying Needs
The **most active topics** cluster around three themes:

1. **Heartbeat & Cron reliability** ([#4418], [#4437], [#4549], [#4551]) — Users are increasingly relying on scheduled/automated agent behavior (heartbeat tasks). The need for channel-aware delivery and model overrides for heartbeat tasks shows a maturing use case: NanoBot is being used as a **persistent infrastructure component**, not just a chat tool.

2. **Windows & service integration** ([#4513], [#4547]) — A persistent pain point. The `/restart` command breaks under nssm/Win32 because `os.execv` doesn't work. The community wants first-class Windows service support.

3. **OAuth & Copilot Enterprise** ([#4604], [#4220]) — Enterprise users are asking for Copilot for Business / GHE support and more flexible auth flows. This signals enterprise adoption interest.

---

## 5. Bugs & Stability

### High Severity Bugs (today)

| Issue | Description | Severity | Fix PR? |
|-------|-------------|----------|---------|
| [#4611](https://github.com/HKUDS/nanobot/issues/4611) | **DNS rebinding TOCTOU in SSRF validation** — `validate_url_target` doesn't pin the resolved IP, allowing a DNS rebinding attack after validation. | **CRITICAL** — Security vulnerability | **No** — No fix PR exists yet |
| [#4595](https://github.com/HKUDS/nanobot/issues/4595) | `apply_final_call_ids` overwrites correct tool_call IDs for non-file-edit tools, causing **permanent session poisoning** — incorrect IDs propagate into the session history | **HIGH** — Affects all tool types, corrupts history | No (closed without fix, appears to be fixed in PR stack elsewhere) |
| [#4599](https://github.com/HKUDS/nanobot/issues/4599) | Linux install script **immediately crashes** at TUI with no user interaction | **HIGH** — Blocks installation from script | No (rapidly closed as crash) |
| [#4580](https://github.com/HKUDS/nanobot/issues/4580) | Subprocess exec uses default path, not conda environments | **MEDIUM** — Feature gap for scientific/ML users | No |

### Note: Issue [#4611] (DNS rebinding) is the most concerning — it's a security vulnerability that bypasses SSRF IP validation by swapping DNS answers between validation and connection. This deserves immediate maintainer attention.

---

## 6. Feature Requests & Roadmap Signals

### User-Requested Features (today)
| Issue | Feature | Likely for Next Version? |
|-------|---------|--------------------------|
| [#4604](https://github.com/HKUDS/nanobot/issues/4604) | Anthropic OAuth support | **Prediction: YES** — Auth new provider, lower effort |
| [#4612](https://github.com/HKUDS/nanobot/issues/4612) | OpenAI Response API support (non-chat-compatible endpoint) | **Prediction: Possibly** — Niche, but OpenAI diversity |
| [#4605](https://github.com/HKUDS/nanobot/issues/4605) | External script → agent action trigger | **Prediction: YES** — Aligns with heartbeat/infra direction |
| [#4603](https://github.com/HKUDS/nanobot/issues/4603) | Stop mutating tool_call.id for WebUI file-edit correlation | **Prediction: YES** — This was a bug-by-design, already being refactored |

### Roadmap Signals from PRs
- **A2A (Agent-to-Agent delegation)** — [#4571](https://github.com/HKUDS/nanobot/pull/4571) adds native A2A peer delegation with depth guards. This is a **significant architecture signal** — NanoBot is moving toward multi-agent collaboration.
- **Per-session model presets** — Multiple PRs ([#4555], [#4556], [#4416]) add per-session, per-cron, and per-Dream model overrides. This is a major flexibility improvement that allows users to say "use cheap model for heartbeat, expensive model for coding."
- **Context cost optimization** — [#4581](https://github.com/HKUDS/nanobot/pull/4581) and [#4608] both explicitly target reducing token consumption. **Cost reduction is emerging as a core theme** for the project.

---

## 7. User Feedback Summary

### Pain Points (expressed today)
- **Windows + nssm**: "After /restart, service shows stopped but nanobot is actually running" — user reporting confusing behavior ([#4513])
- **Install script usability**: "TUI crashes before I even press anything" — user frustrated that the default install path is broken ([#4599])
- **OAuth setup ambiguity**: "Hard to know that oauth provider wasn't set by default, wasted my time" — setup flow still has UX debt ([#4573] context)
- **Provider token persistence**: "Running docker restart drops all stored provider tokens" — Docker users losing auth state on restart ([#1023], finally closed!)

### Satisfaction Signals
- **Praise for codebase quality**: "Compared to OpenClaw, the lightweight codebase makes it easy to read and understand the source, which I really appreciate" — explicit positive comparison to competitor ([#4605])
- **Rapid issue closure**: 7 of 12 issues updated were **closed**, including the 4-month-old [#1023] token persistence bug — users are seeing their reports resolved

### Use Cases Emerging
1. **Email classification agent** — [#4605] user sets up Gmail skill with CLI automation
2. **Headless/infra agent** — Multiple users wanting scheduled/heartbeat tasks (cron)
3. **Enterprise deployment** — OAuth, Copilot Enterprise, nssm service mode

---

## 8. Backlog Watch

### High-Priority Items Needing Maintainer Attention

| Item | Age | Problem |
|------|-----|---------|
| [#4611](https://github.com/HKUDS/nanobot/issues/4611) — SSRF DNS rebinding | **Created today** | **Security vulnerability**, no fix PR exists yet. The issue author demonstrates the TOCTOU race. This is the single most urgent open item. |
| [#4534](https://github.com/HKUDS/nanobot/pull/4534) — Agent reliability layer | **5 days old** | Large PR adding verification, exec services, Codex integration. Has no comments from maintainers. Risk of staleness given its scope. |
| [#4402](https://github.com/HKUDS/nanobot/pull/4402) — Eager memory consolidation | **12 days old** | No maintainer review. Important for memory system maturity. |
| [#4580](https://github.com/HKUDS/nanobot/issues/4580) — conda environment for exec | **2 days old** | Closed quickly, but the solution is unclear. Scientific/ML users need proper virtualenv support for code execution. |
| [#4603](https://github.com/HKUDS/nanobot/issues/4603) — Mutating `tool_call.id` | **Created today** | Raised as a refactor request — points to a design issue where a WebUI convenience caused protocol-level side effects. |

### Long-Standing (30+ days)
- None notable today — the project is closing issues rapidly.

---

**Summary Verdict**: NanoBot is in a **high-velocity, healthy development phase**. The team is merging aggressively, closing old bugs, and the community is actively contributing structured, high-quality PRs. The main risks are: (1) the unaddressed DNS rebinding vulnerability, and (2) the potential for the memory/heartbeat PR stack to grow stale without reviewer attention. The architecture is clearly evolving toward multi-agent (A2A), cost-optimized, infrastructure-grade deployments — this is a projects core maintainers appear to actively endorse.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-07-01

---

## 1. Today's Overview

Hermes Agent remains highly active with 50 issues and 50 PRs updated in the last 24 hours, signaling strong community engagement and rapid development velocity. Of the updated issues, 15 were closed (30%) and 35 remain open, while PR activity shows 15 merged/closed against 35 open proposals. The project released no new versions today, but a substantial wave of stability-focused PRs landed, particularly around Windows runtime hardening, session isolation fixes, and logging deadlocks. The community is surfacing a significant number of bug reports around provider compatibility (OpenAI Codex, Kimi K2.5, Cline) and gateway platform issues (Telegram polling crashes, desktop session profile loss), indicating both broad adoption and growing pains at scale.

---

## 2. Releases

No new releases today.

---

## 3. Project Progress

Despite zero releases, 15 PRs were merged or closed today, representing meaningful progress on several fronts:

- **Windows Stability Overhaul**: Multiple PRs targeted Windows-specific crashes — [#56013](https://github.com/NousResearch/hermes-agent/pull/56013) (logging freeze fix), [#56001](https://github.com/NousResearch/hermes-agent/pull/56001) (log lock contention mitigation via `RotatingFileHandler`), and [#56012](https://github.com/NousResearch/hermes-agent/pull/56012) (UTF-8/CP866 terminal decoding and concurrent-log-handler lock tolerance).

- **Desktop Session Isolation**: PR [#55980](https://github.com/NousResearch/hermes-agent/pull/55980) (closed) hardened desktop session isolation by preventing internal compaction todos from appearing as user turns, preserving compression bindings, and adding doctor checks.

- **Internal Todo Snapshots Cleanup**: PR [#55998](https://github.com/NousResearch/hermes-agent/pull/55998) refactored post-compression todo snapshots from fake `user` turns to `system` replay hints, fixing a source of confusion in session replay.

- **MoA (Mixture of Agents) Refactor**: PR [#55991](https://github.com/NousResearch/hermes-agent/pull/55991) unified slot provider-identity logic into a single chokepoint, improving maintainability of multi-provider orchestration.

- **Delegation System**: PR [#56010](https://github.com/NousResearch/hermes-agent/pull/56010) added config-backed persona presets for subagents, enabling reusable child-local prompts and runtime defaults.

- **Scheduled CRON Fixes**: PR [#56007](https://github.com/NousResearch/hermes-agent/pull/56007) anchored WhatsApp cron replies to the correct session brief, fixing context drift in automated messaging.

- **Photon & Webhook Fixes**: PR [#56006](https://github.com/NousResearch/hermes-agent/pull/56006) made Photon (iMessage) send/reaction state durable across restarts; PR [#56000](https://github.com/NousResearch/hermes-agent/pull/56000) suppressed spurious `[SILENT]` webhook responses.

---

## 4. Community Hot Topics

**Most Active Issues (by comment count):**

1. **[#33932](https://github.com/NousResearch/hermes-agent/issues/33932)** (12 comments) — **OpenAI Codex crash with `NoneType` error**. This closed bug report shows the community's frustration with OpenAI Codex provider reliability. The `HTTP None` error pattern is a critical blocker for users on `gpt-5.5` models.

2. **[#27430](https://github.com/NousResearch/hermes-agent/issues/27430)** (7 comments) — **`hermes update` fails with `NODE_ENV=production`**. A deployment pain point where npm's devDependency omission breaks web UI builds. Affects Docker/VPS users.

3. **[#40347](https://github.com/NousResearch/hermes-agent/issues/40347)** (6 comments) — **Russian locale request for Desktop app**. Strong community interest in localization; user `warment` even provided a working installer.

4. **[#27455](https://github.com/NousResearch/hermes-agent/issues/27455)** (6 comments) — **"Custom runtime does not implement sessions.patch" over SSH tunnel**. Affects remote gateway connections from Desktop, blocking remote agent usage.

5. **[#29299](https://github.com/NousResearch/hermes-agent/issues/29299)** (5 comments, 1 👍) — **HTTPS OAuth callback URL support needed**. Enterprise users need HTTPS redirect URIs for Salesforce/MCP OAuth flows.

**Active PRs with community interest:**

- **[#47755](https://github.com/NousResearch/hermes-agent/pull/47755)** — Configurable OAuth redirect_uri for MCP flows. Directly addresses the HTTPS callback need from issue #29299.

- **[#54230](https://github.com/NousResearch/hermes-agent/pull/54230)** — Mattermost live-thinking bubble, a frequently requested UX parity feature.

- **[#54229](https://github.com/NousResearch/hermes-agent/pull/54229)** — Extends session continuity fix to Mattermost DM channels, addressing a significant context-loss bug.

**Underlying Needs:** The community is consistently asking for:
- Better provider resilience (OpenAI Codex, Cline, Kimi)
- Enterprise-grade OAuth/authentication (HTTPS callbacks, refresh token management)
- Platform feature parity (Discord reactions, Mattermost live-thinking, Russian locale)
- Deployment reliability (Docker/NODE_ENV, Windows stability)

---

## 5. Bugs & Stability

### Critical/High Severity (P1)

| Issue | Description | Fix PR? |
|-------|-------------|---------|
| [#55925](https://github.com/NousResearch/hermes-agent/issues/55925) | Failing bg-review thread kills Telegram polling coroutine, causing agent to stop responding on Telegram | In progress (self-healing merged in #55921, root cause pending) |
| [#54919](https://github.com/NousResearch/hermes-agent/issues/54919) | Windows: `hermes` command fails with "uv trampoline failed to spawn Python child process" — likely a PATH/Python installation issue | None yet |
| [#55647](https://github.com/NousResearch/hermes-agent/issues/55647) (CLOSED) | skill_manage patches hallucinate existing skill content because review fork writes without read-before-write | Fixed in PR #55647 |
| [#19776](https://github.com/NousResearch/hermes-agent/issues/19776) (CLOSED) | Discord gateway connect timeout too short when slash command sync >30s | Fixed |
| [#27455](https://github.com/NousResearch/hermes-agent/issues/27455) (CLOSED) | SSH tunnel sessions.patch crash on Desktop | Fixed |

### Medium Severity (P2)

| Issue | Description | Fix PR? |
|-------|-------------|---------|
| [#55815](https://github.com/NousResearch/hermes-agent/issues/55815) | Cline provider incorrectly appends `/models` to base URL | None yet |
| [#55902](https://github.com/NousResearch/hermes-agent/issues/55902) | Kimi K2.5 HTTP 400: `messages[N].timestamp` not permitted | None yet — provider-specific sanitization needed |
| [#36239](https://github.com/NousResearch/hermes-agent/issues/36239) | `handle_max_iterations` uses soft user-role stop prompt instead of hard `tool_choice=none` stop | None yet |
| [#41517](https://github.com/NousResearch/hermes-agent/issues/41517) | Desktop/Dashboard chat worker loses selected profile, falls back to default | PR #55980 addresses session isolation |
| [#55985](https://github.com/NousResearch/hermes-agent/issues/55985) | Dashboard logout crashes container via `NotImplementedError` in `BasicAuthProvider` | None yet — container enters restart loop |
| [#50170](https://github.com/NousResearch/hermes-agent/issues/50170) | MCP tools silently absent in new sessions after keepalive failure — no warning to user | None yet |
| [#55761](https://github.com/NousResearch/hermes-agent/issues/55761) | Telegram: duplicate identical messages on text-only turns (stream preview + final send) | None yet |
| [#55658](https://github.com/NousResearch/hermes-agent/issues/55658) | Desktop: cannot start after update | Needs reproduction |

### Low Severity (P3)

| Issue | Description | Fix PR? |
|-------|-------------|---------|
| [#55416](https://github.com/NousResearch/hermes-agent/issues/55416) | Photon iMessage: persistent RST_STREAM code 2 on free shared line | None yet |
| [#33415](https://github.com/NousResearch/hermes-agent/issues/33415) | OpenAI OAuth returns TypeError on all gpt-5.x models — fallback never activates | None yet |
| [#55735](https://github.com/NousResearch/hermes-agent/issues/55735) (CLOSED) | Deprecated `rcedit@5.0.2` in desktop devDependencies | Closed as duplicate |

**Key Observation:** The Windows stability fixes landing today (PRs #56013, #56001, #56012) target a cluster of Windows-specific lock contention and encoding issues that have likely been causing hangs and crashes for Windows users.

---

## 6. Feature Requests & Roadmap Signals

### Top Community-Requested Features

1. **HTTPS OAuth Callback URL** ([#29299](https://github.com/NousResearch/hermes-agent/issues/29299), 5 comments, 1 👍) — Enterprise MCP integration requires HTTPS redirect URIs. PR [#47755](https://github.com/NousResearch/hermes-agent/pull/47755) is actively implementing configurable `redirect_uri` for MCP OAuth flows.

2. **Discord Reaction Support** ([#29026](https://github.com/NousResearch/hermes-agent/issues/29026), 1 comment) — Users want emoji reactions as quick feedback signals for confirmations.

3. **Generic OAuth Broker Credential Source** ([#23944](https://github.com/NousResearch/hermes-agent/issues/23944), 1 comment, 2 👍) — Solving refresh token rotation conflicts when Hermes runs across multiple runtimes.

4. **Longer/Configurable Backoff for HTTP 503/529 Overload** ([#55540](https://github.com/NousResearch/hermes-agent/issues/55540), 1 comment) — Production users hitting GLM-5.2 endpoints need smarter retry logic for provider overload.

5. **Auto-summarize Conversation History** ([#55961](https://github.com/NousResearch/hermes-agent/issues/55961), 1 comment) — Token consumption optimization for long conversations, similar to ChatGPT's summarization feature.

6. **Russian Locale** ([#40347](https://github.com/NousResearch/hermes-agent/issues/40347), 6 comments) — Community member already built a working installer.

7. **Multiple HERMES_WRITE_SAFE_ROOT Directories** ([#49535](https://github.com/NousResearch/hermes-agent/issues/49535), 1 comment) — Docker deployments with multiple bind mounts need multiple safe write roots.

8. **Local Model Setup Skill** ([#523](https://github.com/NousResearch/hermes-agent/issues/523), 3 comments, 3 👍) — Community guide for Ollama, llama.cpp, and vLLM configuration, inspired by Liquid AI's LocalCowork.

### Predictions for Next Version (0.14.x → 0.15.0)

Based on PR activity and issue velocity, the next release is likely to include:
- **Configurable MCP OAuth redirect_uri** (PR #47755 — nearing readiness)
- **Improved session isolation for Desktop** (PR #55980, #55998 — merged today)
- **Mattermost live-thinking bubble** (PR #54230 — opt-in feature)
- **Mattermost DM session continuity fix** (PR #54229)
- **Delegation persona presets** (PR #56010)

---

## 7. User Feedback Summary

### Pain Points (Dissatisfaction Signals)

1. **OpenAI Codex reliability crisis** — Two active bug reports ([#33932](https://github.com/NousResearch/hermes-agent/issues/33932), [#33415](https://github.com/NousResearch/hermes-agent/issues/33415)) show `gpt-5.x` models are effectively unusable via Codex. Users report `TypeError` and `NoneType` errors with no fallback activation.

2. **Provider fragmentation** — Users hitting integration-specific bugs with Cline ([#55815](https://github.com/NousResearch/hermes-agent/issues/55815)), Kimi K2.5 ([#55902](https://github.com/NousResearch/hermes-agent/issues/55902)), OpenRouter ([#56002](https://github.com/NousResearch/hermes-agent/pull/56002)), and Anthropic-compatible proxies ([#11906](https://github.com/NousResearch/hermes-agent/issues/11906)). The sheer diversity of providers is a strength but creates a long tail of integration issues.

3. **Windows deployment fragility** — Multiple reports ([#54919](https://github.com/NousResearch/hermes-agent/issues/54919), [#55658](https://github.com/NousResearch/hermes-agent/issues/55658), #55953) indicate Windows users face crashes on launch, post-update failures, and log-induced freezes. Today's stability PRs suggest maintainers are aware and acting.

4. **Session identity confusion** — Users report profile mismatch ([#41517](https://github.com/NousResearch/hermes-agent/issues/41517)) and session key collisions ([#12099](https://github.com/NousResearch/hermes-agent/issues/12099)) when using multiple profiles or platforms.

5. **Silent failures** — MCP tools silently absent after keepalive failure ([#50170](https://github.com/NousResearch/hermes-agent/issues/50170)) and silent `[SILENT]` responses ([#56000](https://github.com/NousResearch/hermes-agent/pull/56000)) erode user trust.

### Satisfaction Signals

- **Active community contributions**: Multiple external contributors submitting PRs (alexandersemenov27, wernerhp, LeonSGP43, konsisumer) indicates a healthy open-source ecosystem.
- **Rapid response to Telegram polling crash**: Issue #55925 was opened 2026-06-30, and a fix PR was already in progress, demonstrating quick iteration on critical platform issues.

---

## 8. Backlog Watch

Issues and PRs needing maintainer attention:

| Item | Age | Why It Matters |
|------|-----|----------------|
| [#523](https://github.com/NousResearch/hermes-agent/issues/523) — Local Model Setup Skill | Opened 2026-03-06 (117 days) | 3 👍, high community interest in local deployment; no maintainer response |
| [#23944](https://github.com/NousResearch/hermes-agent/issues/23944) — Generic OAuth Broker | Opened 2026-05-11 (51 days) | 2 👍, critical for multi-runtime deployments; no PR or progress |
| [#12099](https://github.com/NousResearch/hermes-agent/issues/12099) — `build_session_key()` hardcodes `agent:main` | Opened 2026-04-18 (74 days) | Breaks multi-profile isolation; closed without fix? Needs re-evaluation |
| [#29026](https://github.com/NousResearch/hermes-agent/issues/29026) — Discord Reaction Support | Opened 2026-05-20 (42 days) | Simple parity feature with high potential for community contribution |
| [#33415](https://github.com/NousResearch/hermes-agent/issues/33415) — OpenAI OAuth TypeError (duplicate of #33932?) | Opened 2026-05-27 (35 days) | Still open; users reporting same class of error but labeled as duplicate of closed #33932 — may need re-assessment |
| [#36239](https://github.com/NousResearch/hermes-agent/issues/36239) — Soft vs hard stop on max iterations | Opened 2026-06-01 (30 days) | Affects agent reliability; no PR yet |
| [#50170](https://github.com/NousResearch/hermes-agent/issues/50170) — MCP tools silently absent | Opened 2026-06-21 (10 days) | Zero-warning failure mode for MCP integration — high impact |
| [#55416](https://github.com/NousResearch/hermes-agent/issues/55416) — Photon iMessage persistent disconnect | Opened 2026-06-30 (1 day) | New, but affects a paid integrated service (iMessage) |
| [#55815](https://github.com/NousResearch/hermes-agent/issues/55815) — Cline provider base URL corruption | Opened 2026-06-30 (1 day) | Fresh bug, high impact for Cline users |

**Notable**: The `sweeper:risk-session-state` label appears on nearly every session-related issue, suggesting session state management is a systemic area of technical debt. The project is actively investing here (see PRs #55980, #55998, #56009), which is a healthy signal.

---

**Overall Health Assessment**: Hermes Agent is in a phase of rapid community growth with corresponding stability challenges. The project's strength lies in its diverse provider ecosystem and active maintainer response to critical bugs (especially Windows and platform-specific issues). The main risks are: (1) the OpenAI Codex provider effectively being broken for gpt-5.x models, (2) provider integration fragmentation creating a long tail of compatibility bugs, and (3) session state complexity causing emergent failures across Desktop, Telegram, and multi-profile setups. The aggressive PR throughput today indicates the team is prioritizing stability over new features, which is a prudent strategy.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-01

## Today's Overview

PicoClaw shows high activity today with 6 issues updated and 7 PRs touched in the last 24 hours, alongside a fresh nightly release. The project is in a healthy development cycle with three PRs merged/closed and one new build pushed. However, a cluster of newly filed bugs on 2026-06-30 (4 issues) raises stability concerns, particularly around connectivity with local endpoints and KVM deployments. Community contributions continue to flow, with features like Android ADB tooling and DeltaChat gateway still under review.

## Releases

**nightly (v0.3.1-nightly.20260701.2cf030d2)**

A new automated nightly build was published today. This is an unstable pre-release build intended for testing, with the full changelog available at [v0.3.1…main](https://github.com/sipeed/picoclaw/compare/v0.3.1...main). No stable version bump occurred. Users are advised to use with caution in non-production environments.

## Project Progress

Three PRs were merged or closed today:

- **[PR #3198](https://github.com/sipeed/picoclaw/pull/3198) (merged)** – *fix(providers): surface friendly auth error messages* by lc6464. Improves error handling when API keys or provider permissions fail, adding structured HTTPError types and clearer user-facing guidance.
- **[PR #3131](https://github.com/sipeed/picoclaw/pull/3131) (closed)** – *fix(registry): add ok checks for tool schema type assertions* by chengzhichao-xydt. Adds safety checks for type assertions in the tools registry, preventing crashes from malformed schema maps.
- **[PR #3143](https://github.com/sipeed/picoclaw/pull/3143) (closed)** – *fix(web): block private IPv4 embeds in ISATAP literals* by lc6464. Fixes a SSRF guard bypass in `web_fetch` by detecting ISATAP IPv6 literals embedding private/loopback addresses (issue #3074).

Today’s merged work focused entirely on reliability: better error messages, safer type handling, and security hardening.

## Community Hot Topics

- **[Issue #3153](https://github.com/sipeed/picoclaw/issues/3153)** – [BUG] Volcengine Doubao Seed tool calls leak as raw `<seed:tool_call>` text (2 comments). This 8-day-old bug persists, affecting users of `doubao-seed-2.0-pro` where tool invocations are returned as unexecuted XML text. The issue remains open without a fix PR.

- **[Issue #3159](https://github.com/sipeed/picoclaw/issues/3159)** – [BUG] Frequent task repetition (1 comment). A user reports that when asking sequential questions about different countries, the AI repeats the prior task before answering the new one. This suggests a session context management issue.

- **[PR #3063](https://github.com/sipeed/picoclaw/pull/3063)** – *feat: add deltachat gateway* (open 23 days). This feature PR for a decentralized messaging gateway continues to see updates, indicating maintainer interest in expanding communication channels beyond standard web/API interfaces.

The underlying need across these threads is for **reliable tool execution** and **session correctness** — users expect predictable behavior when chaining tasks.

## Bugs & Stability

Four new bugs were reported on 2026-06-30:

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#3199](https://github.com/sipeed/picoclaw/issues/3199) (closed) | **High** | Custom model provider cannot connect to `http://127.0.0.1` OpenAI-compatible endpoint. Works in other clients — suggests a localhost handling bug. | Closed without resolution (possible duplicate or config issue) |
| [#3195](https://github.com/sipeed/picoclaw/issues/3195) | **High** | OpenAI GPT fails on NanoKVM with default config. New feature in NanoKVM 2.4.0; all interactions return errors. | None |
| [#3196](https://github.com/sipeed/picoclaw/issues/3196) | **Medium** | Codex and AntiGravity OAuth login not working (v0.2.9). | None |
| [#3197](https://github.com/sipeed/picoclaw/issues/3197) | **Medium** | Same OAuth issue as #3196 — likely duplicate. | None |

Additionally, the open issue #3153 (Volcengine tool call leak) remains a **critical** concern for users of that provider. No fix PR currently exists.

## Feature Requests & Roadmap Signals

No new feature requests were filed today. The following open PRs signal likely roadmap directions:

- **[PR #3157](https://github.com/sipeed/picoclaw/pull/3157)** – Android ADB remote operations tool (open 9 days). Adds device control via ADB — taps, swipes, screenshots. Predictable for inclusion in next minor release if testing completes.
- **[PR #3118](https://github.com/sipeed/picoclaw/pull/3118)** – Remote Pico WebSocket mode for agent (open 19 days). Enables remote agent execution via WebSocket. Likely candidate for v0.3.2.
- **[PR #3063](https://github.com/sipeed/picoclaw/pull/3063)** – DeltaChat gateway (open 23 days). Decentralized messaging integration. Slower review pace suggests this may target v0.4.0.

**Prediction**: The next stable release (v0.3.1 or v0.3.2) will likely include the provider auth error fix (#3198) and tool schema safety (#3131), plus possibly the ADB tool (#3157) if reviewed soon.

## User Feedback Summary

**Pain points** evident from today’s issues:
- **Connectivity friction**: Localhost endpoints (issue #3199) and KVM deployments (#3195) failing out of the box — both are common self-hosted setups.
- **OAuth fragility**: Two users reported Codex/AntiGravity login failures (#3196, #3197), suggesting a regression in v0.2.9.
- **Tool execution reliability**: Task repetition (#3159) and tool call leaks (#3153) erode trust in agentic behavior.

**Satisfaction signals**: The merged PRs (#3198, #3131, #3143) address real user pain points around auth errors, crashes, and SSRF vulnerabilities — demonstrating responsive maintainership. The 3 merged/closed PRs today vs. 4 new bugs keeps the project in a net-positive stability trend.

## Backlog Watch

| Item | Age | Status | Concern |
|------|-----|--------|---------|
| [Issue #3153](https://github.com/sipeed/picoclaw/issues/3153) – Volcengine tool call leak | 9 days | Open, no fix PR | High impact for affected users; no triage response visible |
| [PR #3063](https://github.com/sipeed/picoclaw/pull/3063) – DeltaChat gateway | 23 days | Open, no recent review | Maintainer attention needed to avoid feature drift |
| [PR #3118](https://github.com/sipeed/picoclaw/pull/3118) – Remote WebSocket agent | 19 days | Open, stale updates | Needs review to unblock agent remote usage |
| [Issue #3159](https://github.com/sipeed/picoclaw/issues/3159) – Task repetition | 8 days | Stale, 0 maintainer comments | User reported in Chinese; possible language barrier slowing response |

**Action recommended**: Maintainers should triage issue #3153 (Volcengine leak) and engage on PR #3063 to prevent community contributions from becoming stale. The NanoKVM issue (#3195) represents a potential deployment blocker for new users adopting the v2.4.0 feature.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**NanoClaw Project Digest — 2026-07-01**

---

### 1. Today's Overview

NanoClaw shows very high development velocity today, with 14 pull requests updated in the last 24 hours—10 of which were merged or closed. The project addressed critical security vulnerabilities, expanded channel adapter support (Discord, WeChat, Signal resilience), and introduced a new document rendering sandbox. One moderately severe open issue regarding WhatsApp silent media drops remains, with a fix PR already submitted. Overall, the project is in a strong maintenance and feature-acceleration phase.

---

### 2. Releases

No new releases were published today. The latest release remains unchanged.

---

### 3. Project Progress

**10 Pull Requests merged/closed today:**

- **#2884 [merged]** — `feat(discord): add Discord channel adapter + fix Gateway approval-button routing`. Adds a native Discord adapter via the Chat SDK bridge and fixes a DM-context approval routing bug.  
- **#2889 [merged]** — `feat: daily-news-agent for Andy group + WeChat channel`. Introduces a daily-news agent with RSS/HN fetching and LLM digest generation, plus a WeChat channel adapter.  
- **#2893 [merged]** — `feat(render): host-mediated document rendering via ephemeral container`. Adds a `render_document` MCP tool that isolates Quarto/LaTeX/Chromium rendering in a per-session ephemeral container for security.  
- **#2891 [merged]** — `feat(channels): add optional resolveChannelName to ChannelAdapter interface`. Fixes TypeScript build failures for Slack and Telegram adapters referencing the method.  
- **#2895 [merged]** — `fix(whatsapp): recover inbound media download via reuploadRequest`. Fixes the WhatsApp adapter’s silent failure on CDN fetch errors.  
- **#2875 [merged]** — `[follows-guidelines] Deploy/coolify`. Adds deployment skill for Coolify.  
- **#2874 [merged]** — `fix(signal): survive signal-cli boot flaps instead of crash-looping`. Stabilizes the Signal adapter against transient startup failures.  
- **#2885 [merged]** — `fix(setup): offer Slack Socket Mode in the guided setup flow`. Ensures Slack Socket Mode is available in the `setup:auto` flow on `main`.  
- **#2018 [merged]** — `fix(channels): resolve clicker user from interaction.user in DM-context approvals`. Fixes a 3-month-old bug where DM approval buttons would fail to identify the user.  
- **#2880 [merged]** — `fix(security): contain inbox symlink escapes in attachment writes (#2828)`. Closes a critical CWE-59 symlink-follow vulnerability via host-side checks and a safer temp-file approach.

**Remaining open PRs (4):**  
- **#2896** — Follow-up fix for WhatsApp media-failure note regression  
- **#2844** — Native persistent E2EE Matrix adapter (in progress)  
- **#2892** — Telegram thread support (one-line capability flag)  
- **#2890** — Agent template loader and setup flow (feature-branch, active development)

---

### 4. Community Hot Topics

1. **#2828** [CLOSED, 2 👍] — Security: Symlink-follow in inbox attachment forwarding.  
   *Need:* Critical security concern around compromised/prompt-injected agents escaping container sandboxes. The community quickly acknowledged severity; the fix PR (#2880) was merged within 48 hours.

2. **#2896** [OPEN, 0 comments, 0 👍] — Follow-up fix for WhatsApp media-failure note regression.  
   *Need:* A review of the merged #2895 surfaced a regression where `appendMediaFailureNote` was applied before the pending-question handler, breaking the approval path. This shows active peer-review culture and rapid patch iteration.

3. **#2844** [OPEN, 0 comments, 0 👍] — Native persistent E2EE Matrix adapter.  
   *Need:* Replacing WASM crypto with Rust bindings to address cross-platform build failures and latency issues. This is a high-effort, long-duration PR attracting attention from Matrix users.

*Observation:* The community is heavily focused on security boundaries (container isolation, symlink containment) and channel reliability (WhatsApp, Matrix, Signal). Fewer feature requests than bug/stability fixes today.

---

### 5. Bugs & Stability

| # | Issue | Severity | Status | Fix PR |
|---|-------|----------|--------|--------|
| #2894 | WhatsApp adapter: inbound media silently dropped when direct CDN fetch fails | **Medium** — Data loss, silent failure | OPEN | ✅ #2895 (merged) |
| #2896 | WhatsApp: regression in media-failure note on approval path | **Low/Medium** — Breaks approval UX if triggered | OPEN | #2896 (open) |
| #2874 | Signal adapter crash-looping on boot flaps | **Medium** — Adapter unavailable | CLOSED | #2874 (merged) |

No new regressions reported beyond the WhatsApp one. The previously open security issue (#2828) has been resolved.

---

### 6. Feature Requests & Roadmap Signals

Based on merged/open PRs and community activity:

- **Channel expansion is a clear roadmap priority:** Discord (#2884), WeChat (#2889), and native Matrix E2EE (#2844) all advanced this week.
- **Document rendering** (#2893) was shipped as a security-hardened MCP tool — likely to be expanded to support more formats.
- **Agent templates** (#2890) are a new abstraction under active development, suggesting the project is moving toward reusable, composable agent groups.
- **Signal reliability** (#2874) and **Slack Socket Mode parity** (#2885) indicate infrastructure hardening is ongoing.

*Prediction:* Next minor release will likely include Discord, WeChat, document rendering, and agent templates. Telegram thread support (#2892) and the WhatsApp media regression fix (#2896) are trivial merges and could land within days.

---

### 7. User Feedback Summary

- **Positive signals:**  
  - Rapid security response (symlink fix merged in <48 hours)  
  - TDD-driven daily-news agent (#2889) was developed with 33 vitest cases  
  - Guided setup flow for Slack Socket Mode shows attention to UX

- **Pain points:**  
  - WhatsApp media reliability: users report silent attachment loss when CDN fails (#2894, #2895)  
  - Matrix performance: cross-platform WASM crypto is reportedly slow and fragile (#2844)  
  - Documentation gaps: agent templates (#2890) come with docs, but some users may find the setup flow still complex

- **Satisfaction indicators:**  
  - High merge rate (10/14 PRs closed)  
  - Multiple external contributors active today (echarrod, rudgalvis, avri-schneider, wangzx5521-wq, thisdotrob, amit-shafnir)

---

### 8. Backlog Watch

| # | Issue/PR | Age | Status | Notes |
|---|----------|-----|--------|-------|
| #2018 | fix(channels): DM-context approval user resolution | 66 days | ✅ **Merged today** | Finally resolved after 2 months |
| #2844 | feat(matrix): native persistent E2EE adapter | 7 days | OPEN | Longest-open active PR; maintainer avri-schneider is actively pushing commits |
| #2828 | Security: symlink-follow in inbox | 10 days | ✅ **Closed today** | Resolved with #2880 |

**No items currently at risk of abandonment.** The oldest PR (#2844) is actively maintained. No unaddressed user issues are languishing without maintainer attention.

---

**Project Health: 🟢 Strong** — High velocity, active multi-contributor community, rapid security fixes, and steady feature development. Only minor stability regressions remain open, with fixes in progress.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-01

## 1. Today's Overview
NullClaw shows a steady maintenance day with **2 open issues** and **4 pull requests merged/closed** in the last 24 hours. All PR activity comes from contributor **yanggf8**, indicating continued community-driven development despite no new release today. The project has **zero open PRs**, suggesting the maintainers are actively reviewing and integrating contributions. Activity is moderate but focused on bug fixes and cron subsystem improvements. No security incidents or critical regressions were recorded.

## 2. Releases
**No new releases** today. The latest tagged version remains **v2026.4.17** (referenced in Issue #868). Users relying on recent fixes in PRs #641, #643, #645, and #783 will need to build from source or wait for the next release cycle.

## 3. Project Progress
All 4 pull requests were **merged/closed** today:
- **PR #641** — Fix GLM/ZhipuAI thinking mode and native tool_calls (resolves response loops caused by GLM servers defaulting to thinking mode). Critical fix for users of Chinese LLM providers.
- **PR #643** — Allow agent cron jobs to omit `command` field in `cron.json`. Previously, agent jobs with `"command": null` were silently skipped on reload, causing all agent cron jobs to disappear after gateway restart.
- **PR #645** — Add `--account` flag to `cron add-agent` CLI, enabling full delivery routing (e.g., specifying Telegram bot account) from the command line without manual JSON editing.
- **PR #783** — Major cron subsystem enhancement: DB-backed scheduler with run history, cron subagent engine, JSON CLI output, per-job timezone offsets, delivery routing, and security hardening.

## 4. Community Hot Topics
**Most active issue:**  
- [#868 — `zig build` fails on Android/Termux (aarch64) with AccessDenied](https://github.com/nullclaw/nullclaw/issues/868)  
  *5 comments, open since April 23, 2026*  
  Users on Android (Termux) with aarch64 architecture cannot build NullClaw from source due to a Zig linker permission error (`linkat`). The issue has been open for over 2 months with no fix PR, suggesting it may be a Zig toolchain compatibility problem rather than a NullClaw bug. This is a pain point for mobile/edge deployment users.

**No issues/PRs with significant reactions today.** The project appears to have a small but engaged user base.

## 5. Bugs & Stability
**High severity:**
- **#868 — Android/Termux build failure (aarch64)** — Blocks all builds on ARM64 Android. Workaround: use prebuilt binaries or cross-compile. No fix PR exists.
- **#972 — Telegram channel stops responding after idle time** — Critical for users relying on Telegram as a delivery channel. Symptoms: NullClaw agent still responds to `ping` but Telegram channel goes silent after overnight idle. No comments yet, no fix PR. Likely a connection keepalive or reconnection logic issue.

**Medium severity:**
- **PR #643 resolved** a silent data loss bug where agent cron jobs with `null` command fields were discarded on gateway restart.

## 6. Feature Requests & Roadmap Signals
**Recent improvements suggest upcoming focus areas:**
- **Cron subsystem maturity** (PR #783): DB-backed scheduling, run history, JSON output, per-job TZ — indicates the project is moving toward enterprise-grade scheduled automation.
- **Provider diversity**: PR #641's GLM/ZhipuAI fixes show continued support for Chinese LLM providers alongside mainstream APIs.
- **CLI usability**: PR #645's `--account` flag reflects a pattern of making configuration less JSON-editing-dependent.

**Predicted next version features:** Guided cron setup wizard, Telegram channel reconnection health checks, and possibly ARM64 official prebuilt binaries.

## 7. User Feedback Summary
**Pain points:**
- Android/Termux users cannot build from source (Issue #868) — affects mobile automation use cases.
- Telegram channel users experience silent failures after idle periods (Issue #972) — erodes trust in channel reliability.
- **Positive signal**: The 4 merged PRs today directly address user-reported issues (agent cron jobs disappearing, missing CLI flags, GLM provider loops), showing responsive development.

**Satisfaction indicators:** No negative comments or frustration expressed in recent issues. Users filing bugs are providing detailed environment info and logs.

## 8. Backlog Watch
**Long-standing issue needing maintainer attention:**
- **#868 — Android/Termux build failure** (open 69 days, 5 comments) — Requires investigation: is this a NullClaw code issue or Zig Android toolchain problem? A maintainer response acknowledging the issue and suggesting workarounds (e.g., recommending cross-compilation or releasing prebuilt ARM64 binaries) would reduce user frustration.

**No unanswered PRs** — all open PRs were merged today, indicating healthy review velocity.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-01

## Today's Overview

IronClaw is in a period of **high-intensity engineering**, with 50 PRs and 22 issues updated in the last 24 hours—indicating a committed team working across stability, coverage, and infrastructure. The project has **25 open PRs and 25 merged/closed PRs**, demonstrating a balanced pipeline of new work and resolved items. No new releases were cut today, suggesting the team is consolidating fixes and features ahead of a planned release. The activity is heavily concentrated on the **Reborn** backend rewrite, CI infrastructure improvements, and addressing **persistence-layer bugs** that impact production reliability. While no critical security issues are present, several **stability regressions** around runner lease expiration and CAS contention are receiving focused attention.

## Releases

**No new releases today.** The last release remains `ibsql-prod` (as referenced in QA issues). The absence of releases alongside 25 merged PRs suggests an upcoming release candidate may be imminent.

## Project Progress

**25 PRs were merged or closed today**, reflecting significant forward momentum:

### Core Infrastructure & CI
- **PR #5430** (open, XL) adds `cargo-llvm-cov` integration-tier coverage for the Reborn backend (T0-COV roadmap task), providing per-PR informational coverage signals
- **PR #5432** (closed, M) adds dedicated low-contention CI jobs for Reborn group tests, addressing flaky test infrastructure
- **PR #5465** (closed, M) collapses the Reborn group harness to one runtime + scope-routed gateway, fixing ~1.4–5% flakiness under CPU contention
- **PR #5448** (open, XL) unblocks main-only checks by removing generated WebUI v2 bundles from source control and adding a Code Style guard

### Reborn Backend Features & Testing
- **PR #5433** (open, XS) adds `extension_activate` int-tier scenario (T0-EXTACT coverage gap)
- **PR #5431** (closed, S) re-enables `spawn_subagent` surface + un-ignores spawn e2e tests (T0-SPAWN)
- **PR #5434** (open, XS) adds `memory_search`/`memory_tree` int-tier scenarios (T0-MEMQ)
- **PR #5440** (open, M) introduces six test-harness seam constructors unlocking Tier-2 integration coverage
- **PR #5149** (open, XL) implements progressive tool disclosure (flag-gated, default off) to cut per-call prompt size from ~25.8k tokens

### Fixes & Performance
- **PR #5404** (open, L) fixes chat composer clearing after send in WebUI
- **PR #5338** (open, XL) surfaces real failure details instead of generic `invalid_input` in Reborn WebUI
- **PR #5471** (open, M) writes finalized assistant reply via one-shot append path, eliminating two-write sequence
- **PR #5475** (open, M) replaces unmaintained `serde_yml` with `serde_norway`, resolving two Dependabot alerts

### Dependencies & Security
- **PR #5473** (open, XS) bumps `ws` to 8.21.0 in docs/architecture-video
- **PR #5474** (open, XS) bumps `rand` to 0.8.6 in channels-src/wechat
- **PR #3706** (closed, XL) bumps postcss, @remotion/cli, @remotion/tailwind-v4

## Community Hot Topics

### Most Active Issues

1. **Issue #5420** — "Routine delivery target is a global per-user default, not per-routine"  
   *Comments: 1 | Opened 2026-06-29*  
   A user reports that setting Slack delivery for one routine reroutes *all* routines to Slack. This undermines the core automation workflow and has implications for user trust in per-routine configuration.  
   *Link: [nearai/ironclaw Issue #5420](https://github.com/nearai/ironclaw/issues/5420)*

2. **Issue #5426** — "[QA] Cannot create a routine: system drive is not available"  
   *Comments: 1 | Opened 2026-06-29*  
   A routine creation blocker in hosted-staging environment. The "system drive is not available" error suggests a backend resource provisioning issue.  
   *Link: [nearai/ironclaw Issue #5426](https://github.com/nearai/ironclaw/issues/5426)*

3. **Issue #5476** — "[QA] Reborn runs fail with 'could not start agent runtime' / 'runner lease expired'"  
   *Comments: 0 | Opened 2026-07-01*  
   High-severity stability issue affecting Reborn chat execution under CAS contention + model latency.  
   *Link: [nearai/ironclaw Issue #5476](https://github.com/nearai/ironclaw/issues/5476)*

### Most Active Pull Requests

1. **PR #5149** — "Context management — progressive tool disclosure" (XL, open since 2026-06-23)  
   *High engagement on a feature that addresses token-bloat and model timeout issues by shipping only relevant tools per call.*  
   *Link: [nearai/ironclaw PR #5149](https://github.com/nearai/ironclaw/pull/5149)*

2. **PR #5280** — "Trace Commons: instance-wide enrollment, per-user profiles, and trace inspection" (XL, open since 2026-06-26)  
   *A massive cross-cutting feature touching nearly every scope. Includes a DB migration.*  
   *Link: [nearai/ironclaw PR #5280](https://github.com/nearai/ironclaw/pull/5280)*

3. **PR #5430** — "ci(reborn): add cargo-llvm-cov integration-tier coverage job" (XL, open)  
   *Drives the T0-COV roadmap item—community interest in CI reliability and coverage signals.*  
   *Link: [nearai/ironclaw PR #5430](https://github.com/nearai/ironclaw/pull/5430)*

### Underlying Needs
The community is signaling **three primary needs**: (1) Reliable automation/routine workflows that respect per-routine configuration, (2) Transparent error messages instead of opaque failure tokens, and (3) Stable execution under load, particularly around runner leases and model gateway contention.

## Bugs & Stability

### Critical Severity
1. **Issue #5456** — Routine runs fail with runner lease expiration (bug_bash_P1)  
   *The 90-second inactivity threshold is too aggressive for multi-tool routines involving model inference and external API calls. Dominant failure pattern during 6/30 testing.*  
   *Link: [nearai/ironclaw Issue #5456](https://github.com/nearai/ironclaw/issues/5456)*  
   *Related: Issue #5476 (same root cause)*

2. **Issue #5476** — Reborn runs fail with "could not start agent runtime" / "runner lease expired" under turn-state CAS contention + model latency  
   *QA-reported, affects Reborn chat in railway-staging.*  
   *Link: [nearai/ironclaw Issue #5476](https://github.com/nearai/ironclaw/issues/5476)*

### High Severity
3. **Issue #5420** — Routine delivery target is global, not per-routine  
   *PR #5338 may improve error surfacing, but no fix PR exists for the routing bug itself.*  
   *Link: [nearai/ironclaw Issue #5420](https://github.com/nearai/ironclaw/issues/5420)*

4. **Issue #5460** — Memories in WebUI workspace visible to every user in the workspace  
   *Privacy/data isolation vulnerability—users can see other users' saved memories.*  
   *Link: [nearai/ironclaw Issue #5460](https://github.com/nearai/ironclaw/issues/5460)*

5. **Issue #5466** — Parallel same-tenant turn-runs vs FilesystemTurnStateStore CAS / libsql backend (~10% failure)  
   *Concurrency regression surfaced during PR #5465 development.*  
   *Link: [nearai/ironclaw Issue #5466](https://github.com/nearai/ironclaw/issues/5466)*

### Medium Severity
6. **Issue #5457** — Logs page remains empty and never loads log entries (bug_bash_P2)  
   *Blocks debugging routine failures.*  
   *Link: [nearai/ironclaw Issue #5457](https://github.com/nearai/ironclaw/issues/5457)*

7. **Issue #5458** — Double header displayed on Logs page (bug_bash_P3)  
   *UI rendering bug on the Logs page.*  
   *Link: [nearai/ironclaw Issue #5458](https://github.com/nearai/ironclaw/issues/5458)*

8. **Issue #5429** — Web Search requires a NEAR AI Cloud API token  
   *Friction for multi-tenant/production setups.*  
   *Link: [nearai/ironclaw Issue #5429](https://github.com/nearai/ironclaw/issues/5429)*

9. **Issue #5428** — Harden mock-MCP test egress layer (F1–F3 deferred from #5427)  
   *Test-scaffolding defects that could mask real failures.*  
   *Link: [nearai/ironclaw Issue #5428](https://github.com/nearai/ironclaw/issues/5428)*

### Fix PRs in Flight
- **PR #5338** (open) targets the error surfacing issue (#5289) that may help diagnose the CAS/lease failures
- **PR #5234** (closed today) fixed the per-record lock convoy anti-pattern that contributed to the 2026-06-24 runtime wedge
- **PR #5471** (open) optimizes the finalized reply write path, potentially reducing CAS contention

## Feature Requests & Roadmap Signals

### User-Requested Features
1. **Issue #5443** — Header notifications for newly triggered automation tasks  
   *Users want real-time awareness of automation results without manually checking the Automations page.*  
   *Link: [nearai/ironclaw Issue #5443](https://github.com/nearai/ironclaw/issues/5443)*  
   *PR #5441 (open) already implements approval notifications—likely to ship soon.*

2. **Issue #5459** — Configurable skills and tools  
   *Admins need to install WASM tools/skills that become available to workspace users, with per-user privacy controls.*  
   *Link: [nearai/ironclaw Issue #5459](https://github.com/nearai/ironclaw/issues/5459)*

### Predictions for Next Version
- **Progressive tool disclosure (#5149)** is likely to land next, as it directly addresses production timeout issues
- **Header notifications (#5441)** will likely merge as an immediate UX improvement
- **Trace Commons (#5280)** is a heavy lift but gaining traction as a major observability feature
- **CAS contention fixes** (#5234, #5468, #5469, #5470) are critical for production stability and will likely be prioritized

## User Feedback Summary

### Pain Points
1. **Routine reliability**: Users experience recurring failures due to runner lease expiration (Issue #5456) and global routing instead of per-routine delivery (Issue #5420)
2. **Debugging difficulty**: Empty Logs pages (Issue #5457) and generic error messages like `invalid_input` (PR #5338, Issue #5289) make troubleshooting impossible
3. **Workspace data isolation**: Shared memories across workspace users (Issue #5460) violates basic privacy expectations
4. **Onboarding friction**: System drive unavailability (Issue #5426) and required API tokens (Issue #5429) create barriers to adoption

### Satisfaction Signals
- The team's aggressive response to CI flakiness (PR #5432, #5465) shows commitment to developer experience
- Progressive tool disclosure (PR #5149) directly addresses token-bloat complaints
- The number of closed PRs (25) indicates fast iteration on reported issues

## Backlog Watch

### Long-Unanswered Issues Needing Maintainer Attention
1. **Issue #4108** — "Nightly E2E failed" (opened 2026-05-27, last updated 2026-06-30)  
   *Nightly E2E has been failing for over a month. While this is likely flaky CI infrastructure, the lack of dedicated attention is concerning.*  
   *Link: [nearai/ironclaw Issue #4108](https://github.com/nearai/ironclaw/issues/4108)*

### Stale PRs
2. **PR #5280** — "Trace Commons" (open since 2026-06-26)  
   *A massive PR touching almost every scope. Its breadth may be causing review bottlenecks.*  
   *Link: [nearai/ironclaw PR #5280](https://github.com/nearai/ironclaw/pull/5280)*

3. **PR #5149** — "Progressive tool disclosure" (open since 2026-06-23)  
   *Critical performance fix waiting for review/merge. Could unblock other work.*  
   *Link: [nearai/ironclaw PR #5149](https://github.com/nearai/ironclaw/pull/5149)*

### Watch Items
- **Issue #5437** — "Daily ironclaw failure taxonomy — 2026-06-30" indicates a batch of 146 non-pass tasks in pinchbench all failing with "Model deepseek/..." HTTP 400 errors, suggesting an upstream model gateway issue that may require cross-team coordination.
- The **per-key mutex maps** (Issue #5468) and **serial CAS writes** (Issue #5470) represent architectural debt that PR #5234 began addressing but leaves several stores unconverted.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is a structured project digest for LobsterAI based on the GitHub data provided.

---

## LobsterAI Project Digest: 2026-07-01

### 1. Today's Overview
Project activity was **very high** on June 30, driven by the release of version `2026.6.30`. The team merged **14 Pull Requests**, focusing heavily on fixes for the Cowork and OpenClaw flows, UI polish for conversation rails, and the addition of diagnostic logging. While 6 issues remain open, the rapid pace of PR closures suggests a strong focus on stabilization and addressing regressions. This high velocity, coupled with a new release, indicates the project is in an active development cycle.

### 2. Releases
- **Version:** [LobsterAI 2026.6.30](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.30)
- **Key Changes:** This release bundles several significant improvements and fixes:
    - **Diagnostics:** Added enhanced logging for Cowork and OpenClaw flows for easier troubleshooting.
    - **Analytics:** Added unified usage reporting across multiple areas (settings, agents, MCP, etc.) and removed potentially sensitive "prompt intent" fields from analytics payloads.
    - **OpenClaw Fixes:** Resolved a fallback issue for catalog max token limits.
    - **Scheduled Tasks:** Fixed a gateway initialization issue that caused the task list/history to appear empty on startup.
- **No breaking changes or migration notes were released.**

### 3. Project Progress
- **Cowork UI & UX (Major Focus):** Multiple PRs targeted the Cowork interface. Changes included fixing prompt toolbar overlap when resizing artifacts ([#2235](https://github.com/netease-youdao/LobsterAI/pull/2235)), improving the conversation rail with cleaned-up tooltip previews ([#2222](https://github.com/netease-youdao/LobsterAI/pull/2222), [#2223](https://github.com/netease-youdao/LobsterAI/pull/2223), [#2218](https://github.com/netease-youdao/LobsterAI/pull/2218)), and restoring these fixes after an accidental revert ([#2225](https://github.com/netease-youdao/LobsterAI/pull/2225), [#2226](https://github.com/netease-youdao/LobsterAI/pull/2226)).
- **AI Agent Execution:** A significant fix was merged to ensure child agents in `cron` and parallel flows can properly drive the parent agent to completion ([#2234](https://github.com/netease-youdao/LobsterAI/pull/2234)).
- **Notifications:** A feature enabling system notifications when a session completes or errors while the app is in the background was merged ([#1428](https://github.com/netease-youdao/LobsterAI/pull/1428)).
- **Stability & Configuration:** Model edit UI was optimized ([#2236](https://github.com/netease-youdao/LobsterAI/pull/2236)), and a fix prevents duplicate skills from being added via local upload ([#1427](https://github.com/netease-youdao/LobsterAI/pull/1427) - closed, though the associated issue is linked).

### 4. Community Hot Topics
While recent activity is dominated by core team work, a few historical issues show user interest. There were **no comments** on recent major PRs from the community.

- **Issue #1382:** [Suggestion to change red warning text color](https://github.com/netease-youdao/LobsterAI/issues/1382) (2 comments). This is a low-severity UI suggestion, but it highlights user consideration of standard UX conventions (red = error).
- **Issue #1426 & #1427:** [Bugs related to uploading local skills](https://github.com/netease-youdao/LobsterAI/issues/1426) (2 comments each). Users reported a lack of success feedback and the ability to create duplicate skills. The associated fix PR was closed recently, but the issues remain open.
- **Issue #1381:** [Request for scheduled task results in a single session](https://github.com/netease-youdao/LobsterAI/issues/1381) (1 comment). A feature request indicating users want a cleaner, less cluttered experience for recurring tasks.

**Underlying Need:** Users are signaling a need for more polished UX feedback (color coding, success confirmations) and better session management for automated tasks and WeChat integration.

### 5. Bugs & Stability
A critical performance issue was reported, alongside several older UI bugs.

| Severity | Issue # | Symptom | Fix PRs & Notes |
| :--- | :--- | :--- | :--- |
| **High** | [#2230](https://github.com/netease-youdao/LobsterAI/issues/2230) | **Same model is drastically slower in LobsterAI than in CodeBuddy** (25 min vs 2m24s). Token consumption is also 1000x higher (60M vs 67K). | **No fix PR yet.** This is a severe performance regression requiring immediate investigation. |
| **Medium** | [#1384](https://github.com/netease-youdao/LobsterAI/issues/1384) | Selecting multiple files in a session only shows the last one. | A fix PR exists but is still **open** ([#1372](https://github.com/netease-youdao/LobsterAI/pull/1372)). |
| Medium | [#1426](https://github.com/netease-youdao/LobsterAI/issues/1426) | No success feedback when adding a skill via upload. | Likely resolved by fix for duplicate skills. |
| Medium | [#1427](https://github.com/netease-youdao/LobsterAI/issues/1427) | Local upload allows adding duplicate skills. | A fix PR was closed ([#1427](https://github.com/netease-youdao/LobsterAI/pull/1427)), suggesting a fix is in the release. |
| Low | [#1383](https://github.com/netease-youdao/LobsterAI/issues/1383) | Duplicate WeChat messages are not synced to the desktop client. | **No fix PR yet.** |
| Low | [#1385](https://github.com/netease-youdao/LobsterAI/issues/1385) | Deleting a WeChat session task doesn't clear history for future messages in the same conversation. | **No fix PR yet.** |

### 6. Feature Requests & Roadmap Signals
- **Scheduled Tasks in Single Session (Issue #1381):** Users want `cron` job results to accumulate in one conversation window rather than spawning new ones. This aligns with the ongoing fixes for the conversation rail, suggesting a focus on session management.
- **System Notifications (PR #1428):** This feature, now merged, directly responds to the need for background task awareness, a key UX gap compared to tools like Cursor.
- **Deeper Diagnostics (PR #2229):** The addition of diagnostic logging indicates a proactive move to improve debuggability for the complex Cowork and OpenClaw systems, likely in response to harder-to-find issues like [#2230](https://github.com/netease-youdao/LobsterAI/issues/2230).

**Prediction:** The next version will likely contain the fix for the critical performance regression ([#2230](https://github.com/netease-youdao/LobsterAI/issues/2230)) and the ongoing fix for multiple file uploads ([#1372](https://github.com/netease-youdao/LobsterAI/pull/1372)). The long-standing request for unified scheduled task sessions ([#1381](https://github.com/netease-youdao/LobsterAI/issues/1381)) is a strong candidate for a future minor release.

### 7. User Feedback Summary
- **Satisfaction:** Users are actively testing integrations (WeChat, scheduled tasks) and reporting specific issues. The existence of a "suggestion" for UI colors indicates a level of comfort with the platform to request improvements.
- **Pain Points:**
    - **Performance:** Issue [#2230](https://github.com/netease-youdao/LobsterAI/issues/2230) is a stark pain point. The user is comparing directly to a competitor and finding LobsterAI orders of magnitude slower and more expensive.
    - **Inconsistent UI Feedback:** Several bugs (uploading files, adding skills, duplicate WeChat messages) lack clear visual confirmation or behavior, leading to user confusion.
    - **WeChat Integration:** The integration is functional but has several edge-case bugs that interrupt the user flow.

### 8. Backlog Watch
- **Critical: Issue #1384 (Multi-file upload) & PR #1372:** A user-facing bug from April has a fix PR that remains **open and stale**. This long wait on a seemingly straightforward fix is a red flag for project maintainability.
- **Important: Issue #1383 & #1385 (WeChat sync/history bugs):** These WeChat integration issues have been open since April with no activity from maintainers. As a core integration, these need triage.
- **Watch: Issue #1381 (Scheduled task session management):** This feature request has been open for three months. It represents a meaningful UX improvement that could serve as a strong signal for the project's responsiveness to user needs.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for **2026-07-01**, based on the provided GitHub data.

---

## Moltis Project Digest – 2026-07-01

### 1. Today's Overview
The Moltis repository shows **low activity** over the reporting period. There were **zero new issues** created or updated in the last 24 hours, and no new releases were published. Project momentum is centered entirely on dependency maintenance, with **3 pull requests** updated in the last day. Two of these PRs were closed/merged, indicating the development team is successfully keeping the build dependencies up to date, but there is no evidence of new feature work, bug fixes, or community discussion moving forward today.

### 2. Releases
**None.** There are no new releases to report for this period.

### 3. Project Progress
Two pull requests were closed or merged in the last 24 hours, both related to automated dependency updates:
- **[PR #1134]** – chore(deps): bump the npm_and_yarn group across 2 directories with 2 updates. Updated `astro` (6.3.3 → 6.4.8) in `/docs` and `undici` in `/website`.
- **[PR #1121]** – chore(deps-dev): bump `esbuild` from 0.25.12 to 0.28.1 in `/crates/web/ui`.

Both PRs were authored by `dependabot[bot]`, reflecting routine maintenance rather than deliberate feature advancement or functional fixes.

### 4. Community Hot Topics
There are currently **no issues or PRs with significant community engagement**. All three PRs observed have **0 comments and 0 reactions** (👍). The only open PR is:
- **[PR #1141]** – An open dependency update bumping `esbuild` and `vite` across three directories. It remains unmerged with zero discussion.

**Analysis:** The lack of community interaction suggests either a quiet development phase or that the project currently has no active user base raising concerns or feature requests.

### 5. Bugs & Stability
**No bugs, crashes, or regressions were reported** in the last 24 hours. There are no open issues classified as bugs, and no fix-related PRs are present. The project appears stable from a code health perspective, though this may also reflect low testing or reporting activity.

### 6. Feature Requests & Roadmap Signals
**No feature requests were submitted** during this period. The roadmap signals are absent; all activity is confined to dependency bumps. No predictions can be made for the next version based on current data.

### 7. User Feedback Summary
There is **no user feedback** captured in the form of issues, comments, or reactions during this reporting window. It is not possible to assess user satisfaction, pain points, or use cases from the available data.

### 8. Backlog Watch
There are **no long-unanswered items** to flag. The open PR [#1141] is only 1 day old (created 2026-06-30) and requires maintainer review/merging. No other stalled or ignored issues or PRs were identified.

---

**Project Health Assessment:** Quiet and stable. Moltis is in a maintenance-only phase with no feature development, bug reports, or community engagement visible in the last 24 hours. This low activity may indicate a pause in development or a mature product phase.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest
**Date:** 2026-07-01  
**Generated from:** GitHub data snapshot (agentscope-ai/CoPaw)

---

## 1. Today's Overview

CoPaw shows **high development velocity** with 50 PRs updated in the last 24 hours (29 open, 21 merged/closed) and 23 Issues updated (16 open, 7 closed). The project is actively addressing **v2.0.0 pre-release bugs** (#5273 tracking issue remains open) while shipping significant new features including **memory search reranker support**, **loop detection/gate architecture**, and **Linux sandbox improvements**. No new releases were published today, but the pipeline is rich with merged feature PRs targeting both the upcoming v2.0.0 release and current v1.1.12.x maintenance. The community is engaged, with 6 first-time contributors submitting PRs this period—a strong signal of healthy project adoption.

---

## 2. Releases

**No new releases today.** The latest release remains at the version noted in Issues (v1.1.12.post2 / v2.0.0b2). The high volume of pre-release bug fixes and v2.0.0-alpha tracking suggests a stable release is being prepared.

---

## 3. Project Progress

21 PRs were merged or closed in the last 24 hours. Key advancements:

### Security & Governance (Major)
- **PR #5310** (merged) — `feat(sandbox): add bubblewrap Linux sandbox with mount namespace isolation` — Adds `bwrap` as preferred Linux sandbox, providing mount-namespace filesystem isolation with invisible deny_paths, minimal /dev, and synthetic /proc. This is a **critical security enhancement** for Linux deployments.
- **PR #5301** (merged) — `refactor(governance): merge ToolGuard detectors into Policy engine` — Consolidates security policy infrastructure.
- **PR #5623** (merged) — `fix(governance): OFF mode still triggers tool approval` — Fixes bug where "OFF" mode in Web UI still showed approval prompts; root cause was `approval_level` vs `execution_level` mismatch.

### Memory & Search
- **PR #5647** (merged) — `feat(memory): add reranker config panel to memory settings` — UI for enabling/disabling reranker with API credentials and model config.
- **PR #5648** (merged) — `feat(memory): add configurable reranker for memory search` — Backend support for external rerank API (e.g. SiliconFlow) to re-rank hybrid search results.
- **PR #5669** (new, open) — `feat(memory): add qwen3-rerank to memory search` — Wraps ReMe's hybrid search with DashScope `qwen3-rerank` (addresses #5588).

### Documentation & Infrastructure
- **PR #5621** (merged) — `docs(security): add Sandbox section to security documentation` — Comprehensive coverage of OS kernel-level isolation, Tool Guard/File Guard relationship, and platform-specific sandboxes.
- **PR #5666** (merged) — `fix(docs): fix channel-related feature descriptions`.
- **PR #5662** (merged) — `fix(ci): modify channel name in the pr template`.
- **PR #5653** (new, under review) — `docs(website): add Architecture page (en + zh)`.

### TUI & Console
- **PR #5673** (new) — `feat(tui): add live context-usage bar to the status bar` — Shows context fill level and proximity to auto-compaction.
- **PR #5671** (new) — `fix(tui): support CJK / IME input (bump textual to >=8.2.8)` — Fixes raw escape sequence leak when typing Chinese/Japanese/Korean.
- **PR #5674** (new) — `fix(runtime): ensure cancel_envelope is yielded when task is cancelled` — Fixes frontend stuck in "processing" after cancel.

### Loop Engineering (New Feature)
- **PR #5665** (new) — `feat: Loop Engineering — Composable Gate Architecture & Frontend Settings` — Introduces composable gate-based loop detection system with frontend settings UI. This is a **significant new capability** for preventing agent loops (addresses #5657).

### Plugin Ecosystem
- **PR #5661** (new) — `feat: filter plugin market and CDN catalog by QwenPaw version compatibility` — Server-side filtering of official plugin catalog based on `qwenpaw_version` / `min_version` / `max_version`.

### First-Time Contributors
- **PR #5677** — `Load skill metadata into system prompt` (fixes #5676).
- **PR #5675** — `feat(console): remove hardcoded 10k input character limit` (fixes #5670).
- **PR #5669** — `feat(memory): add qwen3-rerank to memory search` (closes #5588).
- **PR #5310** — bubblewrap sandbox (merged).
- **PR #5301** — ToolGuard refactor (merged).
- **PR #5675** — Input limit removal.

---

## 4. Community Hot Topics

### Most Discussed Issues

| Issue | Comments | Summary |
|-------|----------|---------|
| [#5401](https://github.com/agentscope-ai/QwenPaw/issues/5401) (CLOSED) | 6 | Console crash with large tool-use history; root cause: `type: "data"` content blocks not handled |
| [#5630](https://github.com/agentscope-ai/QwenPaw/issues/5630) (OPEN) | 6 | Request: custom BaseURL for Telegram channel — reflects demand for network flexibility |
| [#5403](https://github.com/agentscope-ai/QwenPaw/issues/5403) (OPEN) | 5 | Browser autofill hijacks search input on Model Configuration page — UX annoyance |
| [#5588](https://github.com/agentscope-ai/QwenPaw/issues/5588) (OPEN) | 4 | Memory search needs dedicated reranker for two-stage retrieval — **now addressed by PR #5647 + #5648** |
| [#5561](https://github.com/agentscope-ai/QwenPaw/issues/5561) (OPEN) | 4 | Feishu bot fails on long messages; sends as file instead |
| [#5573](https://github.com/agentscope-ai/QwenPaw/issues/5573) (CLOSED) | 4 | DeepSeek V4 thinking mode: two 400 errors — `reasoning_content` missing and null type in tool schema |
| [#5550](https://github.com/agentscope-ai/QwenPaw/issues/5550) (CLOSED) | 4 | Remote SSH plugin: dependency install loop + old backend process residue |

### Most Active PRs (by engagement)

| PR | Comments | Summary |
|----|----------|---------|
| [#5677](https://github.com/agentscope-ai/QwenPaw/pull/5677) (OPEN) | New | First-time contributor: load skill metadata into system prompt |
| [#5675](https://github.com/agentscope-ai/QwenPaw/pull/5675) (OPEN) | New | First-time contributor: remove 10k input limit |
| [#5674](https://github.com/agentscope-ai/QwenPaw/pull/5674) (OPEN) | New | Fix cancel envelope propagation |
| [#5665](https://github.com/agentscope-ai/QwenPaw/pull/5665) (OPEN) | New | Loop engineering gate architecture |

### Underlying Needs
- **Two-stage retrieval** for memory (#5588) was the highest-demand feature this cycle, now **actively being implemented** across two PRs (#5647, #5648, #5669).
- **Channel reliability** (Feishu long message, DingTalk streaming speed, WeCom file handling) remains a consistent pain point.
- **Chinese-language community** is extremely active (~80% of issues in Chinese), suggesting strong adoption in Asia-Pacific markets.

---

## 5. Bugs & Stability

### Critical Bugs (New Today)

| Issue | Severity | Description | Fix Status |
|-------|----------|-------------|------------|
| [#5676](https://github.com/agentscope-ai/QwenPaw/issues/5676) | **Medium** | Available skills not listed in system prompt — agents can't discover tools they should use | **Fixed** → PR #5677 |
| [#5674](https://github.com/agentscope-ai/QwenPaw/issues/5674) | **High** | Cancel envelope not yielded on task cancellation — frontend stuck in "processing" state | **Fixed** → PR #5674 |
| [#5658](https://github.com/agentscope-ai/QwenPaw/issues/5658) | **Medium** | Cannot connect to 9router-proxied models — persistent 400 error | Open, no fix PR |
| [#5587](https://github.com/agentscope-ai/QwenPaw/issues/5587) | **Medium** | Qwen-Image Tool installation error on v1.1.12.post2 | Open |

### Recent Critical Bugs (Last Week)

| Issue | Severity | Description | Status |
|-------|----------|-------------|--------|
| [#5401](https://github.com/agentscope-ai/QwenPaw/issues/5401) | **Critical** | Console crash with large tool-use history (frontend white screen) | **CLOSED** |
| [#5573](https://github.com/agentscope-ai/QwenPaw/issues/5573) | **High** | DeepSeek V4 400 errors on non-official endpoints | **CLOSED** |
| [#5550](https://github.com/agentscope-ai/QwenPaw/issues/5550) | **High** | Remote SSH plugin: dependency loop + process residue | **CLOSED** |
| [#5539](https://github.com/agentscope-ai/QwenPaw/issues/5539) | **Medium** | Heartbeat task cancelled by 120s hardcoded timeout | **CLOSED** |
| [#5623](https://github.com/agentscope-ai/QwenPaw/issues/5623) | **High** | OFF mode still triggers tool approval (governance bypass) | **FIXED** → PR #5623 |

### Regression Watch
- **PR #5672** (`fix(scroll): strip ⟦…⟧ headline in HTTP history path`) addresses a scroll/context glitch surfaced as noisy logs and UI artifact.

### Summary
The team is closing bugs rapidly—7 issues closed today, most within 2-5 days of creation. The v2.0.0 tracking issue (#5273) suggests active regression hunting. The **cancel envelope bug** (#5674) and **skill metadata omission** (#5676) are the only new bugs appearing today, both with immediate fix PRs.

---

## 6. Feature Requests & Roadmap Signals

### High-Confidence Upcoming Features (PRs exist)

| Feature | Issue | PR(s) | Status |
|---------|-------|-------|--------|
| Memory search reranker (two-stage retrieval) | [#5588](https://github.com/agentscope-ai/QwenPaw/issues/5588) | [#5647](https://github.com/agentscope-ai/QwenPaw/pull/5647), [#5648](https://github.com/agentscope-ai/QwenPaw/pull/5648), [#5669](https://github.com/agentscope-ai/QwenPaw/pull/5669) | Merged + new |
| Loop detection / gate architecture | [#5657](https://github.com/agentscope-ai/QwenPaw/issues/5657) | [#5665](https://github.com/agentscope-ai/QwenPaw/pull/5665) | Open PR |
| Remove 10k character input limit | [#5670](https://github.com/agentscope-ai/QwenPaw/issues/5670) | [#5675](https://github.com/agentscope-ai/QwenPaw/pull/5675) | Open PR |
| Linux AppImage desktop build | [#5668](https://github.com/agentscope-ai/QwenPaw/issues/5668) | None yet | Open issue |
| Workspace file browser in chat | [#5667](https://github.com/agentscope-ai/QwenPaw/issues/5667) | None yet | Open issue |
| Custom Telegram BaseURL | [#5630](https://github.com/agentscope-ai/QwenPaw/issues/5630) | None yet | Open issue |
| Per-cron-job model override | [#5638](https://github.com/agentscope-ai/QwenPaw/issues/5638) | None yet | Open issue |

### Predictions for Next Release
1. **Memory reranker** is almost certain for v2.0.0 — three associated PRs merged or open.
2. **Loop detection** (gate architecture) is a strong candidate given the PR existence and user pain (#5657).
3. **Input limit removal** (#5675) is a trivial PR and likely to be merged quickly.
4. **Linux AppImage** (#5668) would fill a major platform gap.
5. **Skill metadata loading** (#5677) is a quick UX win for beginners.

### Lower Priority (No PRs Yet)
- Custom Telegram BaseURL (#5630)
- Media-only bypass debounce toggle (#5663)
- Feishu/WeCom/DingTalk reliability improvements (multiple issues)
- Workspace file browser (#5667)

---

## 7. User Feedback Summary

### Pain Points

| Category | Specific Feedback | Prevalence |
|----------|------------------|------------|
| **Channel reliability** | Feishu bot drops long messages (#5561), DingTalk streaming too slow (#5603), WeCom file handling broken (#5554), cron notifications non-suppressible (#5566) | **High** (4+ issues this week) |
| **Large context handling** | Frontend crashes with large tool-use history (#5401), 10k character input limit too restrictive (#5670) | **Medium-High** |
| **Model compatibility** | DeepSeek V4 400 errors (#5573), 9router proxy failures (#5658) | **Medium** |
| **Cron/automation** | Heartbeat hardcoded 120s timeout (#5539), cron silent execution impossible (#5566), per-job model override missing (#5638) | **Medium** |
| **UI/UX** | Browser autofill hijacking (#5403), CJK IME input broken in TUI (#5671, now fixed) | **Low-Medium** |
| **Plugin/installation** | Remote SSH plugin dependency loop (#5550), Qwen-Image Tool install error (#5587) | **Low** |

### Satisfaction Signals
- **First-time contributors**: 6 in this cycle alone — strong sign of onboarding success.
- **Quick fix turnaround**: Most bugs closed within 2-5 days of reporting.
- **v2.0.0 pre-release tracking**: Active community participation in regression testing (#5273).

### User Profiles (Inferred from Issues)
- **Enterprise users**: Heavy DingTalk/Feishu/WeCom integrators (multiple issues from same authors like `tecgic`).
- **Power users**: Running cron jobs, custom models, complex automations (#5566, #5539, #5638).
- **Chinese-language users**: ~80% of issues in Chinese; strong demand for CJK support and China-hosted model providers.
- **macOS/Linux developers**: Desktop app users (#5550), TUI users (#5671), Linux AppImage request (#5668).

---

## 8. Backlog Watch

### Issues Requiring Maintainer Attention

| Issue | Age | Priority | Reason |
|-------|-----|----------|--------|
| [#5273](https://github.com/agentscope-ai/QwenPaw/issues/5273) | 14 days | **Critical** | v2.0.0 pre-release bug tracker; needs consolidating and closing as GA approaches |
| [#5403](https://github.com/agentscope-ai/QwenPaw/issues/5403) | 8 days | **Medium** | Browser autofill hijacking — annoying UX bug, no fix PR yet |
| [#5561](https://github.com/agentscope-ai/QwenPaw/issues/5561) | 5 days | **Medium-High** | Feishu long message failure — no PR, affects enterprise users |
| [#5566](https://github.com/agentscope-ai/QwenPaw/issues/5566) | 5 days | **Medium** | Cron silent execution impossible + `channels send` unreachable — no PR |
| [#5587](https://github.com/agentscope-ai/QwenPaw/issues/5587) | 3 days | **Medium** | Qwen-Image Tool install error — no PR |
| [#5603](https://github.com/agentscope-ai/QwenPaw/issues/5603) | 2 days | **Medium** | DingTalk card streaming too slow — no PR |
| [#5616](https://github.com/agentscope-ai/QwenPaw/issues/5616) | 2 days | **Low** | Automation tasks terminating without intervention — insufficient details |
| [#5658](https://github.com/agentscope-ai/QwenPaw/issues/5658) | 1 day | **Medium** | 9router proxy 400 errors — persistent issue across versions, no PR |
| [#5630](https://github.com/agentscope-ai/QwenPaw/issues/5630) | 2 days | **Low-Medium** | Custom Telegram BaseURL — feature request, no PR |
| [#5668](https://github.com/agentscope-ai/QwenPaw/issues/5668) | 1 day | **Low-Medium** | Linux AppImage build — platform expansion, no PR but good first issue |

### PRs Needing Review

| PR | Age | Priority | Note |
|----|-----|----------|------|
| [#5665](https://github.com/agentscope-ai/QwenPaw/pull/5665) | 1 day | **High** | Loop engineering — large new feature, needs architectural review |
| [#5673](https://github.com/agentscope-ai/QwenPaw/pull/5673) | 1 day | **Medium** | TUI context-usage bar — UX enhancement |
| [#5671](https://github.com/agentscope-ai/QwenPaw/pull/5671) | 1 day | **High** | CJK/IME input fix — directly impacts Chinese users |
| [#5669](https://github.com/agentscope-ai/QwenPaw/pull/5669) | 1 day | **Medium** | qwen3-rerank integration — complements merged reranker PRs |
| [#5675](https://github.com/agentscope-ai/QwenPaw/pull/5675) | 1 day | **Low** | Remove 10k input limit — trivial, quick win |
| [#5677](https://github.com/agentscope-ai/QwenPaw/pull/5677) | 1 day | **Medium** | Load skill metadata — fixes #5676, beginner-friendly |

### Maintainer Alert
- **DingTalk/Feishu/WeCom reliability** (#5561, #5566, #5603, #5554) forms a **cluster of related channel issues** that may indicate a systemic problem rather than individual bugs. A consolidated investigation would be valuable.
- **v2.0.0 pre-release (#5273)** has comments indicating active regression tracking; maintainers should ensure all sub-issues are addressed before GA release.

---

*Digest generated from GitHub data snapshot on 2026-07-01 from [agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw).*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-01

## Today's Overview

ZeroClaw shows **high activity** today with 50 updated issues and 50 updated PRs in the last 24 hours, though only 4 issues and 4 PRs reached closure. The project remains firmly in a **heavy RFC-driven development phase**, with governance proposals covering plugin architecture, provider models, and channel host bindings dominating discussion. The backlog of accepted RFCs awaiting implementation continues to grow, while several S1-severity bugs (Telegram configuration, MCP tool visibility) remain open across multiple release cycles. The v0.8.3 release cycle is actively tracked across three tracker issues, indicating sustained development momentum toward a coordinated release.

## Releases

**None** — No new releases were published in the last 24 hours. The latest release remains v0.8.1, with v0.8.3 development tracked but unreleased.

## Project Progress

**4 PRs / Issues closed today:**
- **#8386 (Closed)** — *Bug: SQLite default memory backend doesn't prompt for embedding model, hybrid search degrades to keyword-only* — A configuration inconsistency affecting new users. Fix shipped.
- **#6943 (Closed)** — *RFC: Replace Extism with direct wasmtime component model host* — Accepted governance RFC now closed after approval.
- **#7816 (Closed)** — *Feature: Pluggable skill registries* — Accepted and closed, pending implementation.
- One additional issue closed (unlisted in top 30).

**PRs advanced (top by recency):**
- **#8551** — *feat(plugins): channel host bindings* — Major plugin infrastructure PR adding WASI HTTP, inbound queue, and config jail support for WASM-based channel plugins.
- **#8504** — *feat(channels): add Git forge channel with SOP ingress* — New channel type for GitHub polling, issue/PR lifecycle, and Standard Operating Procedure discovery.
- **#8486** — *feat(gateway): add OpenAI chat completions endpoint* — OpenAI-compatible HTTP endpoint for IDE tooling (Continue.dev, Aider) and LangChain integration.
- **#8547** — *fix(audit): remove rag-pdf feature to clear RUSTSEC-2026-0192* — Security vulnerability fix by removing the ttf-parser dependency path.

## Community Hot Topics

**Most active issues (by comments):**

1. **#6808** (13 comments) — *RFC: Work Lanes, Board Automation, and Label Cleanup* — Governance overhaul for routing work across the project. Audacity88's sustained multi-week effort to standardize labels and automation. Still active after 41 days — indicates ongoing negotiation about project workflow norms.

2. **#8193** (6 comments) — *bug(zerocode): MCP tools/tool_search missing from TUI sessions while gateway sees them* — S1 severity bug blocking MCP tool discovery in TUI. Two users confirmed in discussion #8045. High urgency as it undermines the core MCP integration value proposition.

3. **#5542** (6 comments) — *Consecutive OOM in WSL2* — S0 severity data-loss bug persisting since April 2026. Long-standing memory management issue in the daemon process, with 8+ GB RSS before OOM kill.

4. **#8226** (4 comments) — *Feature: per-agent custom environment variables* — Request for `runtime_context` and `runtime_secrets` blocks to support multi-tenancy across identity, parameter, and token separation for shared MCP instances.

5. **#8462** (3 comments, updated today) — *RFC: Runtime Policy for OTel LLM and Tool Content* — Fresh RFC on observability content filtering, split from umbrella structured-observability RFC #7232. Privacy-preserving OTel data handling for GenAI workloads.

**Notable newcomer:** **#8563** (0 comments, filed yesterday) — *Bug: SOPs not available through web dashboard* — S1 severity blocking configured Standard Operating Procedures from reaching agents in web UI sessions.

## Bugs & Stability

**S0 - Data Loss / Security Risk:**
- **#5542** — Consecutive OOM kills in WSL2 (since April 2026, no fix PR visible). Runtime daemon consuming >8GB RSS.

**S1 - Workflow Blocked:**
- **#8193** — MCP tools invisible in TUI sessions (since June 22). Core functionality gap for MCP-reliant users.
- **#8505** — Telegram channel cannot be configured (since June 29). `zeroclaw channels doctor` falsely reports unconfigured channels. Related to channel config validation.
- **#8563** — SOPs not available through web dashboard (filed June 30). Newly reported, no resolution in progress.
- **#8094** — Anthropic provider added in Quickstart unavailable until reset (since June 21). Registration lifecycle bug.

**S2 - Degraded Behavior:**
- **#8386** (Closed) — SQLite default memory backend silently degrades hybrid search. Fix shipped.
- **#5269** — Installation documentation missing for `cargo binstall zeroclaw` (since April 4). Continued user friction.

## Feature Requests & Roadmap Signals

**Likely candidates for v0.8.3 (based on tracker activity):**
- **#8360** — Provider and native-tool message serialization improvements
- **#8071** — Runtime execution, agent loop, tools, and skills stability
- **#8073** — Observability, CI, docs, dependencies, and release support
- **#7882** — `await_sessions` for delegate tool (background task orchestration)
- **#8397** — Per-cron-job `uses_memory` flag exposure in CLI and tools

**Architectural shifts gaining momentum:**
- **#8396** — Wire-Protocol-First Provider Model (Make `wire_api` primary axis) — Could fundamentally restructure provider configuration if accepted.
- **#8398** — Plugin permission, config, and secrets model — Addressing plugin security gaps from two prior permission model iterations.
- **#8424** — `.ignore` file mechanism for workspace file protection — User-driven security request for sensitive file access control.
- **#8132** — Replace React/Vite UI with Rust→Wasm framework (Dioxus/Leptos/Yew) — Elimination of Node.js from build/runtime.
- **#8043** — Retire standalone `aardvark-sys` crate, fold into `zeroclaw-hardware` — Cleanup of crate organizational debt.

**New quality-of-life features entering pipeline:**
- **#8445** — Telegram multi-message mode (one message per agent turn, not concatenated)
- **#8251** — Surface relationship memory as user-facing workflows
- **#8453** — Clean up dead `write_lock` code in logging crate

## User Feedback Summary

**Emerging pain points from recent issues:**
1. **MCP tool visibility gap** (#8193) — Users in #8045 report MCP servers connect and expose tools, but TUI doesn't receive them. This undermines the 0.8.x MCP value proposition that was a major selling point.
2. **Channel configuration fragility** (#8505) — Quickstart channel setup works for CLI but fails for Telegram. User confusion when `zeroclaw channels doctor` gives false negatives. Another user cited similar Discord configuration issues.
3. **Zero-config onboarding letdown** (#8386, closed) — SQLite default silently degrades search quality when no embedding model is configured. New users get a worse experience than they expect from the default.
4. **SOP workflow invisible in web UI** (#8563) — Users following the StageHand example find that configured SOPs don't reach agents through the web dashboard, breaking the intended agent behavior pattern.
5. **Provider lifecycle bugs** (#8094) — Anthropic provider added via Quickstart is "ghost" until a full runtime reset, breaking the first-impression onboarding flow.
6. **Cross-channel TOTP gating** (#3767) — Long-standing request (since March 2026) for 2FA enforcement on destructive commands across all channels. Security-conscious operators are blocked from using shell tools safely in Telegram/Discord/Matrix.

**Satisfaction signals:** Continued high community contribution volume, with multiple new contributors filing RFCs (ConYel, bheatwole, Taswen, rakaarwaky) and submitting PRs (77382104, REL-mame, wangmiao0668000666). The Matrix streaming draft (#8443) and Git forge channel (#8504) indicate active community investment in channel diversity.

## Backlog Watch

**High-severity issues lacking maintainer response or fix:**
- **#5542** (OOM in WSL2, filed Apr 9, 2026) — S0 data-loss severity, 6 comments, labeled `needs-repro`, no fix PR. **83 days open** without resolution.
- **#3767** (Cross-channel TOTP gate, filed Mar 17, 2026) — P1 security feature, 3 comments, accepted but no implementation PR. **106 days open**.
- **#8094** (Anthropic provider ghost after Quickstart, filed Jun 21) — S0 severity label but `needs-repro` and `needs-author-action` blocking triage. **10 days open.**

**Critical RFCs awaiting maintainer review:**
- **#8396** (Wire-protocol-first provider model, filed Jun 27) — P2, `needs-maintainer-review`
- **#8398** (Plugin permission/config/secrets, filed Jun 27) — P2, `needs-maintainer-review`
- **#8424** (.ignore file mechanism, filed Jun 28) — P2, `needs-author-action`
- **#7952** (Publish full-channel prebuilt assets, filed Jun 19) — P2, `needs-maintainer-review`

**PRs needing attention:**
- **#8486** (OpenAI chat completions endpoint) — Marked `needs-author-action`, stalled despite being one of the most visible feature gaps for IDE/ecosystem integration.
- **#8094** — Anthropic provider bug PR not yet filed; the issue has no linked implementation.

**Concern:** Three P2/P3 RFCs filed within 48 hours (June 27–28) addressing provider architecture, plugin security, and file protection all carry `needs-maintainer-review` status, indicating maintainer bandwidth may be stretched across the active release cycle work.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*