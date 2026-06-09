# OpenClaw Ecosystem Digest 2026-06-09

> Issues: 500 | PRs: 470 | Projects covered: 13 | Generated: 2026-06-09 01:52 UTC

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

# OpenClaw Project Digest — 2026-06-09

## Today's Overview
OpenClaw shows **very high activity** with 500 issues and 470 PRs updated in the last 24 hours, 57 issues closed and 137 PRs merged/closed. Two new beta releases (v2026.6.5-beta.5 and v2026.6.5-beta.3) shipped, primarily addressing QQBot thinking-strip and MCP tool result coercion. The maintainer team is active across QA infrastructure, session handling, and provider compatibility fixes. However, a heavy backlog of 443 open issues — many tagged as stale with P1/P2 severity — indicates ongoing stability and feature-completeness challenges.

## Releases
**Two new releases today:**
- **v2026.6.5-beta.5** and **v2026.6.5-beta.3**: Both share identical highlights:
  - **QQBot**: Now strips model reasoning/thinking scaffolding (`<thinking>`) before native delivery, preventing raw content leaks into channel replies (#89913, #90132, thanks @openperf)
  - **MCP tool results**: Now coerce `resource_link`, `resource`, `audio`, malformed image, and future types for safer delivery

*No breaking changes or migration notes documented.*

## Project Progress
**137 PRs merged/closed today** — notable advances:
- **Session state & routing**: PR #90500 (ready for maintainer review) fixes stale session routes for removed providers, preventing routing through dead model providers.
- **Cron fixes**: PR #91380 (closed) lets isolated cron runs inherit default model fallbacks; PR #91548 fixes duplicate cron event text in heartbeat prompts (fixes #44922).
- **Developer experience**: PR #91551 adds explicit `replacePaths` contract for config array replacement; PR #91049 (ready for review) handles terminal chat send acknowledgements.
- **Infrastructure**: PR #91484 and #91502 add QA evidence normalization and Multipass channel-driver QA seam; PR #91547 fixes Docker store seed to use correct architecture packages.
- **Windows compatibility**: PR #91545 switches config-opening to supported `Start-Process -FilePath` parameter.

## Community Hot Topics
**Most active issues (by comments):**
1. **#48788** (18 comments) — Centralized filename encoding utility for multi-encoding Content-Disposition handling. Community wants a proper architectural fix beyond the current UTF-8-only solution for Feishu/Chinese filenames.
2. **#32473** (17 comments, 👍4) — Control UI requires HTTPS/localhost for device identity. Persistent pain point for self-hosted/VPS setups behind reverse proxies.
3. **#90083** (15 comments, 👍3) — OpenAI ChatGPT Responses transport fails with `invalid_provider_content_type` for gpt-5.4/5.5. Critical compatibility gap with latest OpenAI models.
4. **#50090** (15 comments) — Community Skill Development & ClawHub ecosystem. Users want better tooling for building and sharing skills, but gap between promise and practice is "wide."

**Underlying needs**: Users are demanding (a) better multi-encoding support for non-ASCII filenames, (b) reliable HTTPS/self-hosted workflows, (c) timely provider model support, and (d) a functioning skill marketplace.

## Bugs & Stability
**High-severity bugs reported/updated today:**

| Severity | Issue | Summary | Fix PR Exists? |
|----------|-------|---------|----------------|
| 🔴 P1 | #90083 | OpenAI gpt-5.4/5.5 Responses transport fails with `invalid_provider_content_type` | No |
| 🔴 P1 | #32296 | Agent replies to previous message (session context confusion) | No |
| 🔴 P1 | #48003 | Steer mode doesn't inject messages mid-turn for main sessions | No |
| 🔴 P1 | #43367 | Multi-agent orchestration: config overwrites, session-lock failures, detached child work | No |
| 🔴 P1 | #47975 | Subagent sessions persist after completion, main session unresponsive | No |
| 🔴 P1 | #51396 | `clearUnboundScopes` strips operator scopes for token-auth clients (regression) | No |
| 🔴 P1 | #45740 | gh-issues skill injects untrusted issue bodies into sub-agent prompts (security) | No |
| 🟡 P2 | #85888 | Cron jobs consistently fail with MiniMax 503 overload during early morning CST | No |

**Notable regressions**: #32473 (control UI HTTPS), #43747 (memory management "in chaos"), #44845 (Volcengine token usage shows 0), #52186 (ElevenLabs TTS ignored in favor of OpenAI).

## Feature Requests & Roadmap Signals
**Top user-requested features from today's data:**
1. **Per-skill model routing** (#43260) — `model` field in SKILL.md frontmatter for per-skill model selection. Likely next major feature given multi-agent orchestration focus.
2. **Skill priority configuration** (#50199) — Intelligent selection when multiple skills can handle same task.
3. **MathJax/LaTeX rendering** (#42840, 👍5) — For Control UI mathematical content display.
4. **YAML config support** (#45758) — Alternative to JSON5 config format.
5. **Per-agent cost budget enforcement** (#42475) — Gateway-level daily/monthly spend caps.

**Prediction**: Per-skill model routing (#43260) and per-agent cost budgets (#42475) are architecturally aligned with current multi-agent improvements and may appear in v2026.7.x.

## User Feedback Summary
**Pain points:**
- "Control UI requires device identity (use HTTPS or localhost secure context)" — blockers for VPS/homelab users without proper SSL (#32473)
- "Memory management is in chaos" — inconsistent behavior across users, with some experiencing endless chunking/embedding while others have no memory persistence (#43747)
- "Feishu streaming card: abnormal typewriter effect and content truncated to last character" — broken streaming UX for Chinese market (#88929)
- "Cron jobs consistently fail with MiniMax 503 overload during early morning" — timezone-dependent cron failures suggest scheduler/retry logic gaps (#85888)
- "Community Skill Development gap between promise and practice is wide" — frustration with skill ecosystem maturity (#50090)

**Satisfaction signals**: The two new releases and active PR flow indicate responsive maintainers; fixes for QQBot thinking leaks and MCP coercion show attention to polish.

## Backlog Watch
**Critical issues needing maintainer attention (P1/P2, stale, with no fix PR):**

| Issue | Age | Priority | Summary |
|-------|-----|----------|---------|
| #32473 | 98 days | P2 | Control UI HTTPS requirement blocking VPS users |
| #32296 | 99 days | P1 | Session context confusion (replies to wrong message) |
| #43367 | 90 days | P1 | Multi-agent orchestration instability |
| #45740 | 87 days | P1 | Security: untrusted issue body injection into sub-agent prompts |
| #49876 | 83 days | P1 | Cron sessions hallucinate instead of failing cleanly |
| #45031 | 88 days | P1 | Request for built-in security scanning for skill installation |
| #51363 | 80 days | P1 | Docker sandbox container name collision across instances |
| #47975 | 85 days | P1 | Subagent sessions persist, main session unresponsive |

**PRs waiting for maintainer review** (status: 👀 ready for maintainer look):
- **#91049** — Fix terminal chat send acknowledgements
- **#90500** — Fix stale session routes for removed providers
- **#91484** — Add QA evidence summary normalization
- **#91500** — Add QA scorecard taxonomy validation
- **#91502** — Add Multipass channel-driver QA seam

**Longest-open P1 bug**: #32296 (99 days) — "Agent replies to previous message instead of current message" — remains unfixed, a core UX reliability issue.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-06-09

---

## 1. Ecosystem Overview

The open-source personal AI assistant and agent ecosystem is experiencing a **divergent maturation phase**, where projects are simultaneously expanding capabilities (multi-agent orchestration, transcription, security) while struggling with **stability regressions and backlog accumulation**. The space is bifurcating into two architectural camps: **monolithic reference implementations** (OpenClaw, Hermes Agent) that prioritize feature breadth and ecosystem breadth, and **modular, lightweight alternatives** (NanoBot, PicoClaw, TinyClaw) that optimize for specific deployment scenarios (edge, embedded, enterprise isolation). A third emerging cluster—**enterprise-grade refactors** (IronClaw's Reborn v2, ZeroClaw's v0.9.0 security push)—signals a shift toward production-hardened multi-tenant architectures. Community feedback consistently demands **per-agent model routing, improved skill ecosystems, and better non-ASCII/Chinese character support**, reflecting the global and heterogeneous deployment reality.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release? | Bugs Fixed (24h) | Estimated Health Score |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 470 | ✅ 2 beta | 57 issues closed | ⚠️ Very active but high backlog (443 open) |
| **IronClaw** | 33 | 50 | ❌ | 25 PRs merged | ⚠️ High activity, in migration churn |
| **ZeroClaw** | 50 | 50 | ❌ | 12 PRs merged | ⚠️ Active, significant bugs (S0/S1) |
| **CoPaw** | 49 | 45 | ❌ | 23 PRs merged | ✅ Strong, focusing on plugins & enterprise |
| **NanoBot** | 8 | 37 | ❌ | 16 PRs merged | ✅ Very healthy, high merge rate |
| **PicoClaw** | 2* | 16 | ✅ 1 nightly | 9 PRs merged | ✅ Rapid iteration, small community |
| **LobsterAI** | 0 | 19 | ❌ | 18 PRs merged | ✅ Consolidation phase, all PRs clean |
| **NanoClaw** | 1 | 3 | ❌ | 2 PRs merged | ✅ Maintenance mode, clean backlog |
| **Hermes Agent** | 50 | 50 | ❌ | 3 PRs merged | ⚠️ Surge after v0.16.0 release, many bugs |
| **TinyClaw** | 0 | 1 | ❌ | 0 | ⚠️ Low activity, 1 open PR |
| **NullClaw** | 0 | 0 | ❌ | 0 | ❌ No activity |
| **Moltis** | 0 | 0 | ❌ | 0 | ❌ No activity |
| **ZeptoClaw** | 0 | 0 | ❌ | 0 | ❌ No activity |

**Note:** Health Score considers: merge rate, bug fix velocity, backlog ratio, and community engagement. PicoClaw and NanoClaw issue counts are +1 each (open issues); overall data is from their digest summaries.

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**

- **Scale leader**: With 500+ issues and 470 PRs in 24h, OpenClaw has the largest active community by 10x over the next closest (IronClaw, Hermes Agent at ~50 each). This generates faster bug discovery and feature proposals.
- **Ecosystem breadth**: Built-in QQBot thinking-strip fix, MCP tool result coercion, community skill development (#50090)—covers more channels and integrations than any competitor.
- **Core reference status**: As the "core reference" project, it sets architectural patterns (session routing, cron fixes, multi-agent orchestration) that downstream projects (PicoClaw, NanoClaw) adopt.

**Technical Approach Differences:**
- OpenClaw uses a **monolithic agent core** with plugin-based channel adapters; contrast NanoBot's microservices-style architecture and IronClaw's complete Reborn v2 backend rewrite.
- Heavier reliance on JSON5 config (vs. YAML in some peers), which generates community friction (#45758).

**Community Size Comparison:**
- Issues/PRs: OpenClaw (500/470) dwarfs all others
- Merges per day: ~137 PRs vs. IronClaw (25), CoPaw (23), NanoBot (16)
- Critical backlog: 443 open issues (many P1/P2, stale) vs. NanoBot's 2 open bugs—OpenClaw trades velocity for debt

---

## 4. Shared Technical Focus Areas

The following requirements emerge across **multiple projects simultaneously**, indicating ecosystem-wide priorities:

| Requirement | Projects Affected | Specific Needs |
|---|---|---|
| **Per-agent / per-skill model routing** | OpenClaw (#43260), NanoBot (#4253), Hermes Agent | Users want different models for different skills/tasks |
| **Improved skill/plugin marketplace** | OpenClaw (#50090), CoPaw (#5023), ZeroClaw | Community tooling for sharing skills is immature |
| **Non-ASCII / Chinese filename encoding** | OpenClaw (#48788), PicoClaw | Content-Disposition handling for multi-encoding |
| **HTTPS/reverse proxy support** | OpenClaw (#32473), Hermes Agent | Self-hosted deployments blocked without SSL |
| **Memory management stability** | OpenClaw (#43747), ZeroClaw (#5844), Hermes Agent | Inconsistent behavior, context corruption |
| **Telegram code block splitting** | NanoBot (#4250), ZeroClaw (#6701, fixed) | Fenced code blocks broken across split messages |
| **OIDC / SSO Authentication** | ZeroClaw (#7141), IronClaw | Production enterprise auth |
| **Multi-channel agent isolation** | ZeroClaw (#6487, fixed), Hermes Agent | Session collision across channel aliases |
| **Security: prompt injection, leak detection** | OpenClaw (#45740), NanoBot (#4242), ZeroClaw (#4832) | Prompt injection into sub-agents, token redaction false positives |
| **Desktop UI stability** | Hermes Agent (macOS, i18n), OpenClaw (Control UI) | UI regressions after major releases |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | IronClaw | ZeroClaw | CoPaw | PicoClaw |
|---|---|---|---|---|---|---|---|
| **Target User** | Generalists/power users | Edge/lightweight | Desktop/enterprise | Enterprise/cloud | Security-conscious | Chinese enterprise | RISC-V/embedded |
| **Architecture** | Monolithic core + plugins | Microservices | Monolithic desktop | Reborn v2 refactor | Modular security-first | AgentScope 2.0 | Minimal Go |
| **Deployment** | Self-hosted, Docker | Cross-platform binaries | Desktop (macOS/Win/Linux) | Multi-tenant cloud | Docker, WSL2 | WeChat/DingTalk/Feishu | RISC-V, ARM64 |
| **Strength** | Community size, channel breadth | Merge velocity, developer DX | Desktop UX, plugins | OpenAI-compatible API | Security architecture | Chinese enterprise localization | Embedded/low-resource |
| **Weakness** | Backlog accumulation, stale bugs | Small feature surface | Post-release regressions | Migration churn | Silent failures | Process management | Small community |
| **Key Differentiator** | Largest ecosystem, but debt-ridden | Fastest per-PR turnaround | Desktop-first, Codex competitor | Complete backend rewrite | Pluggable security providers | AgentScope 2.0 foundation | RISC-V support |

---

## 6. Community Momentum & Maturity

### Tier 1: Rapidly Iterating (High Activity, High Merge Rate)
- **OpenClaw**: 137 PRs merged today—unmatched volume, but 443 open issues suggest **fixing as fast as breaking**
- **NanoBot**: 16 PRs merged, balance of features (transcription) + fixes (symlink escapes)—healthiest ratio
- **CoPaw**: 23 merges, strong plugin ecosystem push
- **Hermes Agent**: 50 issues + 50 PRs updated—spike after v0.16.0 suggests **post-launch stabilization phase**

### Tier 2: Stable But Active (Controlled Merge Velocity)
- **IronClaw**: 25 PRs merged, focused on Reborn v2 migration (end-to-end feature branches)
- **ZeroClaw**: 12 PRs merged, fixing S0/S1 bugs (Matrix session, Telegram splitting, OOM)
- **LobsterAI**: 18 PRs merged—technically highest merge rate, but 0 new issues (consolidation, not bug discovery)

### Tier 3: Low Activity / Maintenance Mode
- **PicoClaw**: 9 merges but very small community (2 issues); healthy for its size
- **NanoClaw**: 2 merges, 1 bug report, security-focused (egress lockdown)
- **TinyClaw**: 0 merges, 0 issues, 1 open PR—**dormant but not dead**
- **NullClaw, Moltis, ZeptoClaw**: **Inactive** — no activity for 24+ hours

### Tier 4: Enterprise Backend Approaches
- **IronClaw** (Reborn v2) and **ZeroClaw** (v0.9.0) are both doing **major architectural rewrites**—their velocity is lower because scope is larger, but the roadmap signals suggest **long-term dominance potential** in enterprise/cloud segments.

---

## 7. Trend Signals for AI Agent Developers

1. **Per-instance model routing is the #1 unmet need**: Across OpenClaw (#43260), NanoBot (#4253), and Hermes Agent, users want to assign different models to different skills/conversations. This is the **next plateau** for agent flexibility.

2. **Security is moving from optional to mandatory**: ZeroClaw's OIDC (#7141) and per-execution shell confirmation (#7155), plus OpenClaw's injection fix (#45740) and NanoBot's symlink escape fix (#4221), show that **prompt injection, data leakage, and escape vulnerabilities** are now treated as P1/P0.

3. **Chinese/Asian market is a distinct ecosystem**: CoPaw and PicoClaw prioritize WeChat, DingTalk, Feishu, QQ, and RISC-V. Non-ASCII encoding (#48788) and Chinese ASR (Xiaomi MiMo) are recurring themes. Developers targeting Asia must consider **local channel support** and **multi-byte encoding** as first-class.

4. **Desktop AI assistants are converging**: Hermes Agent's desktop app, OpenClaw's Control UI, and ZeroClaw's web dashboard all aim for the same end-user experience. **Computer-use support** (ZeroClaw #6909) and **background task management** (Hermes Agent) are emerging as desktop differentiators.

5. **Multi-agent orchestration is moving beyond research**: OpenClaw (#43367), NanoBot (#3992, cross-instance message bus), and CoPaw (#4727, AgentScope 2.0 migration) are all investing in **multi-agent session management, delegation, and sub-agent lifecycle**. This is the infrastructure for **agent swarms and team-based automation**.

6. **Telegram is the universal channel—but it's fragile**: Almost every project reports Telegram-specific bugs (code splitting, prompt caching, LID issues). Telegram represents the largest common channel deployment, and its **message length limits, markdown handling, and session isolation** are the most frequently debugged surface.

7. **The skill/plugin economy is failing to deliver**: Despite two years of promises (OpenClaw's ClawHub, NanoBot's plugin system), users consistently report that **the gap between "promise and practice" is wide** (#50090). Early adopters want real marketplaces, not just plugin APIs. This is the **open-source ecosystem's biggest missed opportunity**.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-09

**Generated from:** [github.com/HKUDS/nanobot](https://github.com/HKUDS/nanobot)

---

## 1. Today's Overview

NanoBot is in a high-velocity development phase today, with 37 pull requests updated in the last 24 hours—16 of which were merged or closed—indicating strong maintainer throughput and community engagement. The 8 issues updated (4 open, 4 closed) show a healthy balance between bug discovery and resolution. No new releases were cut today, but the project is clearly refining its capabilities across transcription providers, security hardening, memory management, and WebUI features. The most notable architectural signal is the merging of the **agent collaboration cross-instance message bus** (PR #3992), suggesting the project is evolving from a single-agent assistant into a multi-agent orchestration platform.

---

## 2. Releases

**No new releases today.** No versions were published in the last 24 hours. Users remain on the latest available release.

---

## 3. Project Progress

**Merged/Closed PRs (16 total today)** — Key advancements include:

| PR | Title | Component |
|---|---|---|
| [#3992](https://github.com/HKUDS/nanobot/pull/3992) | feat(agent-collab) - enable cross agent messaging | Multi-agent messaging bus |
| [#4224](https://github.com/HKUDS/nanobot/pull/4224) | feat(transcription): add AssemblyAI as provider | Transcription |
| [#4175](https://github.com/HKUDS/nanobot/pull/4175) | feat(transcription): add Xiaomi MiMo ASR provider | Transcription (Chinese ASR) |
| [#4113](https://github.com/HKUDS/nanobot/pull/4113) | feat(transcription): configurable STT model + OpenRouter | Transcription model selection |
| [#4217](https://github.com/HKUDS/nanobot/pull/4217) | feat(providers): add extra_query config for OpenAI-compatible | Azure gateway compatibility |
| [#4232](https://github.com/HKUDS/nanobot/pull/4232) | feat(transcription): shared voice input support | Cross-channel transcription |
| [#4219](https://github.com/HKUDS/nanobot/pull/4219) | fix(session): drop orphan tool results before trimming | Session history stability |
| [#4221](https://github.com/HKUDS/nanobot/pull/4221) | fix(exec): block relative symlink workspace escapes | Security hardening |
| [#4235](https://github.com/HKUDS/nanobot/pull/4235) | feat(webui): show version in Settings Overview | UI improvement |

**Key theme:** Today's merges heavily focused on **transcription infrastructure** — adding three new providers (AssemblyAI, Xiaomi MiMo ASR, OpenRouter), making transcription a shared top-level capability instead of channel-specific, and enabling model selection. The **agent collaboration bus** (PR #3992) is a major architectural milestone that lays groundwork for multi-instance scenarios. Security fixes for symlink escapes (PR #4221) and orphan tool results (PR #4219) address real runtime stability and safety issues.

---

## 4. Community Hot Topics

| Issue/PR | Type | Engagement | Summary |
|---|---|---|---|
| [#4253](https://github.com/HKUDS/nanobot/issues/4253) | Enhancement | 1 comment, open | Override model per conversation — user wants to switch between fast OpenRouter and private LlamaCpp |
| [#4233](https://github.com/HKUDS/nanobot/issues/4233) | Enhancement/Good First Issue | 1 comment, open | Show NanoBot version in WebUI — now addressed by PR [#4255](https://github.com/HKUDS/nanobot/pull/4255) |
| [#4242](https://github.com/HKUDS/nanobot/issues/4242) | Bug report | 0 comments, open | Dream disabled still injects history into system prompt via Recent History |
| [#4250](https://github.com/HKUDS/nanobot/issues/4250) | Bug report | 0 comments, open | Telegram split_message breaks fenced code blocks — fix PR [#4257](https://github.com/HKUDS/nanobot/pull/4257) exists |
| [#4251](https://github.com/HKUDS/nanobot/issues/4251) | Feature Request (Chinese) | 1 comment, closed | Upload files/images for summarization — user wants multimodal file input in chat |

**Analysis:** The community is actively requesting **per-conversation model switching** (Issue #4253) — a pattern that aligns with the new multi-agent architecture. The **WebUI version badge** was a grassroots request (Issue #4233) that rapidly attracted a contributor (PR #4255), showing a responsive maintainer community. The **file upload for summarization** request (Issue #4251, in Chinese) signals demand for multimodal capabilities beyond text — though it was closed, likely because it overlaps with existing vision support.

---

## 5. Bugs & Stability

Ranked by potential impact:

| Severity | Issue | Description | Fix PR |
|---|---|---|---|
| **Critical** | [#4242](https://github.com/HKUDS/nanobot/issues/4242) | Dream disabled setting does not prevent history injection into system prompt — privacy concern | **None yet** — user reports `.dream_cursor` never advances when `dream.enabled=false`, causing `Recent History` to always inject full history |
| **High** | [#4250](https://github.com/HKUDS/nanobot/issues/4250) | Telegram fenced code blocks split across messages render broken HTML | ✅ PR [#4257](https://github.com/HKUDS/nanobot/pull/4257) (open, by axelray-dev) — makes `split_message` code-block-aware |
| **Medium** | [#4074](https://github.com/HKUDS/nanobot/issues/4074) | MCP HTTP/SSE attempts loopback before SSRF rejection — security bypass | **Closed** (#4074), not clear if fully resolved by merged PRs |
| **Medium** | [#4223](https://github.com/HKUDS/nanobot/pull/4223) | WeChat session token expiry leads to permanent silent dead loop (waiting for PR review/open) | PR [#4223](https://github.com/HKUDS/nanobot/pull/4223) (open) — fixes reload after pause expiry |

**Key observation:** The **dream cursor injection bug** (#4242) is the most concerning today — it suggests a user's entire chat history may leak into system prompts even when the user explicitly disabled dream functionality. This is both a privacy and a token-waste issue. No fix PR has been submitted yet. The **Telegram code-block splitting** (#4250) has an existing fix in review.

---

## 6. Feature Requests & Roadmap Signals

| Signal | Issue | Likelihood |
|---|---|---|
| **Per-conversation model override** | [#4253](https://github.com/HKUDS/nanobot/issues/4253) | **High** — aligns with agent collaboration architecture; easy to implement as config overlay |
| **File/image upload for summarization** | [#4251](https://github.com/HKUDS/nanobot/issues/4251) | **Medium** — may already be partially covered; likely needs UI polish |
| **WebUI version badge + update notifications** | [#4233](https://github.com/HKUDS/nanobot/issues/4233) | **Expected in next release** — PR [#4255](https://github.com/HKUDS/nanobot/pull/4255) is open and functional |
| **Azure gateway compatibility** | [#4204](https://github.com/HKUDS/nanobot/issues/4204) | **Already merged** via PR [#4217](https://github.com/HKUDS/nanobot/pull/4217) — `extra_query` support shipped |
| **Multi-agent cross-instance messaging** | [#3992](https://github.com/HKUDS/nanobot/pull/3992) | **Architecture milestone** — merged; further APIs and docs expected |
| **Context microcompaction gating** | [#4238](https://github.com/HKUDS/nanobot/pull/4238) | **In review** — promising optimization for token-efficient multi-turn conversations |

**Prediction:** The next NanoBot release will likely include:
- Version badge in WebUI (PR #4255)
- Multi-agent collaboration APIs (PR #3992)
- ContextGovernor for smart microcompaction (PR #4238)
- Shared transcription infrastructure (multiple PRs)
- Azure/AWS gateway `extra_query` support (PR #4217)

---

## 7. User Feedback Summary

**Pain Points Expressed:**
- Switching between public (OpenRouter) and private (LlamaCpp) models per conversation is not possible — user forced to choose one globally (#4253)
- Chinese users want to upload images/PDFs for AI analysis directly in the chat, not just via external tools (#4251)
- Dream mode cannot be cleanly disabled — history still leaks into the system prompt, wasting tokens and exposing data (#4242)
- Telegram users get broken code blocks when responses are long enough to be split (#4250)

**Satisfaction Signals:**
- Azure/extra_query support was requested (Issue #4204) and was quickly implemented and merged by axelray-dev (PR #4217) — demonstrates responsive maintainers
- Three transcription providers added in rapid succession (AssemblyAI, Xiaomi, OpenRouter) — users have real choice now
- The version badge feature was requested and immediately picked up by a contributor — community feels empowered

**Underlying Need:** Users increasingly want **fine-grained control** over which model handles which task (privacy, speed, capability), and they want **multimodal input** (files, images) as a first-class feature. Security and privacy awareness is high — the dream injection bug (#4242) could erode trust if unaddressed.

---

## 8. Backlog Watch

| Item | Type | Age | Status | Concern |
|---|---|---|---|---|
| [#4074](https://github.com/HKUDS/nanobot/issues/4074) | Security Bug | 10 days | Closed | MCP SSRF bypass; closed but verify fix is complete |
| [#4113](https://github.com/HKUDS/nanobot/pull/4113) | PR (transcription) | 9 days | **Closed** ✅ | Migrated to merged — no longer backlog |
| [#4170](https://github.com/HKUDS/nanobot/pull/4170) | PR (email IMAP) | 5 days | Open, low activity | Email post-actions for agent-managed mailboxes — valuable but quiet |
| [#4223](https://github.com/HKUDS/nanobot/pull/4223) | PR (WeChat fix) | 2 days | Open | WeChat session expiry dead loop — awaiting review/merge |
| [#4253](https://github.com/HKUDS/nanobot/issues/4253) | Feature Request | 1 day | Open | Per-conversation model override — high community interest, no PR yet |
| [#4242](https://github.com/HKUDS/nanobot/issues/4242) | Bug | 1 day | Open | Dream history leak — no fix PR, growing visibility risk |

**Maintainer Attention Needed:**
1. **Dream cursor bug** (#4242) — privacy-sensitive issue, needs triage and a fix path. Could become a community flashpoint if data leakage is confirmed widespread.
2. **WeChat session dead loop** (PR #4223) — simple fix, but blocks WeChat channel functionality for Chinese users.
3. **Email IMAP post-actions** (PR #4170) — valuable for enterprise/agent use cases, but has seen no activity for 5 days. May need maintainer nudge.

---

*Digest generated 2026-06-09 from public GitHub data. All links point to [HKUDS/nanobot](https://github.com/HKUDS/nanobot).*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for 2026-06-09.

---

## Hermes Agent Project Digest
**Date:** 2026-06-09
**Period:** 2026-06-08 – 2026-06-09
**Source:** GitHub (NousResearch/hermes-agent)

### 1. Today's Overview

The Hermes Agent project is currently in a **high-activity cycle**, likely following a recent major update (v0.16.0). In the last 24 hours, the community submitted **50 issues** and **50 pull requests**, indicating a surge in user testing and bug reporting against the latest release. While 4 issues and 3 PRs were closed/merged, the backlog of open items is growing, suggesting maintainers are focused on triaging critical bugs rather than clearing a high volume of tasks. The project is currently balancing the delivery of new features (e.g., background task improvements, desktop audio cues) with a significant influx of stability and configuration fixes (e.g., macOS deployment, credential handling).

### 2. Releases

**No new releases** were published in the last 24 hours. The latest version appears to be **Hermes v0.16.0 (2026.6.5)**, which is mentioned in several bug reports.

### 3. Project Progress

Despite a high volume of open work, a few key fixes and features advanced to closure or merge today:

- **Agent Fixes:** A critical fix for **parent context corruption** when using `delegate_task` (PR #42452, fix for #42449) was merged. This deep-copies the plugin context engine to prevent child agents from overwriting parent compression thresholds.
- **Desktop Stability:** Multiple PRs were opened to tackle desktop build and behavior issues, including fixes for **i18n TypeScript errors blocking the bootstrap installer** (PR #42511, closed) and the **macOS in-app updater** (PR #42482).
- **Security:** A **P1 security fix** for the Telegram adapter (PR #40916) is making progress, adding early authorization checks to prevent prompt injection via unauthorized messages.
- **Infrastructure:** A fix was merged to manage **macOS LaunchAgents** in the correct `gui` domain, preventing gateway restarts from detaching processes (PR #42508).

### 4. Community Hot Topics

The community is highly engaged with **gateway integration and stability**. The most active discussions include:

- **Docker and Gateway Deployment:** Issues [#34457](https://github.com/NousResearch/hermes-agent/issues/34457) (6 comments, 3 👍) and [#30399](https://github.com/NousResearch/hermes-agent/issues/30399) (6 comments, 3 👍) highlight pain points with Docker. The `s6-log` lock loop in multi-container setups and the inability to use the Matrix gateway from the Docker image are significant blockers for server administrators.
- **Security & UX Trade-offs:** A tension between tool visibility and security is a hot topic. Issue [#41955](https://github.com/NousResearch/hermes-agent/issues/41955) (2 👍) and [#41732](https://github.com/NousResearch/hermes-agent/issues/41732) (1 👍) report that terminal tool commands are being leaked as code blocks into messaging chats (WhatsApp, Telegram, Discord) after a recent update, creating noise and a security concern.
- **Missing Features:** Users are actively requesting features that impact daily workflow. Issue [#38357](https://github.com/NousResearch/hermes-agent/issues/38357) (3 comments, 1 👍) asks to show sessions from **all profiles** in the Desktop sidebar, a critical need for users managing multi-profile setups.

### 5. Bugs & Stability

The last 24 hours saw a spike in bug reports, many centered around regressions in the v0.16.0 desktop app and gateway integrations.

| Severity | Issue | Summary | Fix Status |
| :--- | :--- | :--- | :--- |
| **P1** | [#42449](https://github.com/NousResearch/hermes-agent/issues/42449) | `delegate_task` corrupts parent context via shared singleton. | **Fixed** (PR #42452) |
| **P2** | [#42405](https://github.com/NousResearch/hermes-agent/issues/42405) | Memory at capacity triggers a retry loop causing silent hangs. | **Open** |
| **P2** | [#42120](https://github.com/NousResearch/hermes-agent/issues/42120) | Desktop: Incomplete turn content lost when pressing Stop/Cancel. | **Open** |
| **P2** | [#42477](https://github.com/NousResearch/hermes-agent/issues/42477) | Cost tracking severely undercounts (Telegram sessions show zero tokens). | **Open** |
| **P2** | [#42306](https://github.com/NousResearch/hermes-agent/issues/42306) | Langfuse telemetry missing token counts and cost data. | **Closed** (as invalid/duplicate) |
| **P3** | [#42431](https://github.com/NousResearch/hermes-agent/issues/42431) | Desktop Files panel fails in remote mode (ENOENT on local FS). | **Open** |
| **P3** | [#42409](https://github.com/NousResearch/hermes-agent/issues/42409) | Desktop Artifacts timestamps render as Jan 1970 (epoch bug). | **Open** |
| **P3** | [#42401](https://github.com/NousResearch/hermes-agent/issues/42401) | Unsent prompts deleted when navigating to different app pages. | **Open** |

### 6. Feature Requests & Roadmap Signals

Based on the volume and sentiment of feature requests, the community is pushing for improvements in safety, configuration, and workflow support.

- **High Priority for Next Release:**
    1.  **Declarative Skill Safety Policy** ([#27997](https://github.com/NousResearch/hermes-agent/issues/27997)): A well-documented request for a centralized, enforced skill protection policy to prevent mishaps. This is a "quality of life" and safety win for power users.
    2.  **Configurable Sampling Parameters** ([#41988](https://github.com/NousResearch/hermes-agent/issues/41988)): Users running local models cannot set temperature/top_p/top_k, making the project less functional for this user segment.
    3.  **Session Isolation in Desktop** ([#38357](https://github.com/NousResearch/hermes-agent/issues/38357)): Showing all profile sessions is a logical UX extension for multi-profile users.
- **Longer-Term Signals:**
    - **WeCom Optimization** ([#38641](https://github.com/NousResearch/hermes-agent/issues/38641), [#16675](https://github.com/NousResearch/hermes-agent/issues/16675)): Requests for streaming support and message editing in the WeCom adapter suggest a growing enterprise / East Asian user base.
    - **Background Fork Write Scoping** ([#42388](https://github.com/NousResearch/hermes-agent/issues/42388)): A power user request to decouple a background review fork's write permissions from its triggers, indicating a desire for more granular agent autonomy controls.

### 7. User Feedback Summary

The feedback today paints a picture of **high engagement but significant friction** with the v0.16.0 release.

- **Pain Points:**
    - **"Flash and Disappear" Bug:** Users are frustrated by the desktop app flashing responses before they vanish ([#41898](https://github.com/NousResearch/hermes-agent/issues/41898)).
    - **Configuration Hell:** The inability to set default parameters for local models ([#41988](https://github.com/NousResearch/hermes-agent/issues/41988)) and the poor error messages from API key issues ([#42130](https://github.com/NousResearch/hermes-agent/issues/42130)) create a steep onboarding curve.
    - **Data Loss:** Issues like prompts being deleted on page navigation ([#42401](https://github.com/NousResearch/hermes-agent/issues/42401)) and session turn loss ([#42120](https://github.com/NousResearch/hermes-agent/issues/42120)) erode user trust.
- **Positive Signals:**
    - Despite bugs, users are actively deploying Hermes in complex multi-container stacks and enterprise scenarios (Matrix, WeCom, Telegram decision-making bots).
    - The community is quickly reporting and, in some cases, patching issues (e.g., the Photon SDk fix in PR #42498).

### 8. Backlog Watch

- **High: [#27997 - Declarative Skill Protection Policy](https://github.com/NousResearch/hermes-agent/issues/27997)**: This feature has 7 comments and has been open since May 18. No maintainer response or assignment is visible in the data. As a request to prevent a "high-severity gap," this warrants an update.
- **High: [#34457 - s6-log lock crash in Docker](https://github.com/NousResearch/hermes-agent/issues/34457)**: A critical Docker stability issue with 6 comments and 3 upvotes. This is a direct blocker for server-side users. No linked PRs or status updates are apparent.
- **Medium: [#40101 - mnemosyne-hermes Plugin Not Discovered](https://github.com/NousResearch/hermes-agent/issues/40101)**: An external plugin developer has submitted a detailed bug report about plugin discovery. Lack of maintainer response risks disincentivizing third-party contributions.
- **Medium: [#16675 - WeCom Optimization](https://github.com/NousResearch/hermes-agent/issues/16675)**: This request for basic WeCom functionality has been open since April 27 with only one comment. If the project wants to support WeCom, an initial response is overdue.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-09

## Today's Overview
PicoClaw shows **high development velocity** with **16 PRs updated in the last 24 hours**—the busiest day in recent memory. 9 PRs were merged or closed, indicating strong maintainer responsiveness. A new **nightly build (v0.2.9-nightly)** was released, though labeled potentially unstable. The repository has **2 open issues** showing active community involvement, with a notable RISC-V compatibility bug persisting for over 3 weeks. Overall, the project is in a **healthy, rapidly iterating phase** with a clear focus on defensive coding and cross-platform stability.

## Releases
**v0.2.9-nightly.20260609.46b29a0a** (Nightly Build)

- Automated build from latest `main` branch
- **No documented breaking changes or migration notes**
- Labeled as potentially unstable
- Full changelog: https://github.com/sipeed/picoclaw/compare/v0.2.9...main

## Project Progress — Merged/Closed PRs Today (9 items)

### Critical Bug Fixes
- **Telegram location handling** ([#3052](https://github.com/sipeed/picoclaw/pull/3052)) — Converts `message.location` payloads to text, fixing silent ignore of location pins
- **Health check fix** ([#3062](https://github.com/sipeed/picoclaw/pull/3062)) — Resolved "always returning not ready" bug affecting deployment monitoring

### Defensive Coding & Stability (Batch from contributor `chengzhichao-xydt`)
Six PRs addressing unchecked type assertions and error handling:
- **Type assertion safety** across `base.go` ([#3056](https://github.com/sipeed/picoclaw/pull/3056)), `webfetch.go` ([#3058](https://github.com/sipeed/picoclaw/pull/3058)), `subagent/spawn` tools ([#3057](https://github.com/sipeed/picoclaw/pull/3057)), `LINE channel` + `Evolution store` ([#3018](https://github.com/sipeed/picoclaw/pull/3018))
- **`os.Getwd` error handling** in `NewContextBuilder` ([#3055](https://github.com/sipeed/picoclaw/pull/3055))
- **Proper error wrapping (`%w`)** in channels and MCP ([#3051](https://github.com/sipeed/picoclaw/pull/3051))
- **Structured logging migration** replacing `log.Printf`/`fmt.Printf` ([#3050](https://github.com/sipeed/picoclaw/pull/3050))

### Outcome
9/16 PRs merged, all by contributors—demonstrating **strong community contribution pipeline** and maintainer review throughput.

## Community Hot Topics

### Most Active Issue: RISC-V .deb Failure ([#2887](https://github.com/sipeed/picoclaw/issues/2887))
- **9 comments** over 24 days
- **Open since May 17**—longest-running open issue
- **Underlying need**: Users deploying PicoClaw on RISC-V hardware (e.g., VisionFive, LicheePi) cannot use the `.deb` package for OpenAI models. The issue affects enterprise/embedded deployments where RISC-V is increasingly common.
- **Reactions**: 0 👍 — may be under-acknowledged despite severity

### Active PR Discussion: Health Check Fix ([#3062](https://github.com/sipeed/picoclaw/pull/3062))
- Quick merge (same day)—maintainers responsive to operational issues

### New PR: DeltaChat Gateway ([#3063](https://github.com/sipeed/picoclaw/pull/3063))
- **Open, feature PR** for adding DeltaChat integration
- Signals community interest in **decentralized/encrypted messaging channels**

## Bugs & Stability

### High Severity (Open)
| Bug | Issue | Impact |
|-----|-------|--------|
| **RISC-V .deb with OpenAI** | [#2887](https://github.com/sipeed/picoclaw/issues/2887) | Blocks all OpenAI model usage on RISC-V via .deb—unusable for affected users |
| **QQ Channel Windows failure** | [#3015](https://github.com/sipeed/picoclaw/issues/3015) | Token retrieval timeout on Windows, renders QQ channel unusable post-release build. **No fix PR exists** |

### Fixed Today
| Bug | Fix PR | Notes |
|-----|--------|-------|
| Telegram ignores locations | [#3052](https://github.com/sipeed/picoclaw/pull/3052) | Silent failure resolved—now converts to text |
| Health check false negative | [#3062](https://github.com/sipeed/picoclaw/pull/3062) | Operational monitoring blocker fixed |
| Panics from untyped assertions | 6 PRs ([#3056](https://github.com/sipeed/picoclaw/pull/3056), [#3057](https://github.com/sipeed/picoclaw/pull/3057), [#3058](https://github.com/sipeed/picoclaw/pull/3058), [#3018](https://github.com/sipeed/picoclaw/pull/3018), [#3055](https://github.com/sipeed/picoclaw/pull/3055), [#3051](https://github.com/sipeed/picoclaw/pull/3051)) | Prevented potential crashes in LINE, Evolution, subagent tools |

### Regressions
- None reported today

## Feature Requests & Roadmap Signals

### Likely Next Version (v0.3.0 or next nightly)
- **DeltaChat gateway** ([#3063](https://github.com/sipeed/picoclaw/pull/3063)) — Already submitted as PR; strong chance of inclusion
- **Windows child process flash fix** ([#3061](https://github.com/sipeed/picoclaw/pull/3061)) — Open PR addressing GUI launcher UX on Windows
- **Console flash suppression** across all Windows `exec.Command` sites

### User-Requested Features
- Better cross-platform support (driven by RISC-V bug)
- Enhanced channel diversity (DeltaChat interest)
- Windows stability (QQ channel and console flash issues)

## User Feedback Summary

### Pain Points
1. **RISC-V support gap** — `.deb` package for primary AI provider (OpenAI) non-functional; user must compile from source, which is challenging on RISC-V
2. **Windows QQ channel broken** — Release build regression for QQ messaging on Windows, critical for Asian market users
3. **Telegram location handling** — Silent ignore of location pins (now fixed) frustrated Telegram bot users

### Satisfaction Indicators
- **PR turnaround** — 9 PRs merged within 24 hours indicates responsive maintainers
- **New contributors active** — `chengzhichao-xydt` contributed 8 PRs in this digest alone
- **Structured logging adoption** shows project maturing its infrastructure

## Backlog Watch

### Critical Attention Needed
| Item | Issue | Age | Reason |
|------|-------|-----|--------|
| **RISC-V .deb + OpenAI** | [#2887](https://github.com/sipeed/picoclaw/issues/2887) | 24 days | Blocks RISC-V deployments; no assignee, no fix PR |
| **QQ Channel Windows** | [#3015](https://github.com/sipeed/picoclaw/issues/3015) | 4 days | Release-blocking regression for Windows users; no fix PR |

### Long-Running Open PR
| PR | Age | Status |
|----|-----|--------|
| **Agent loop reload & panic cleanup** ([#2904](https://github.com/sipeed/picoclaw/pull/2904)) | 21 days | Open, no recent maintainer activity |

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-09

## Today's Overview
NanoClaw shows moderate activity today with 3 pull requests and 1 open issue updated in the last 24 hours. The project is advancing security hardening, with two important PRs addressing egress lockdown and authentication vulnerabilities, both authored by different contributors suggesting healthy community involvement. No new releases were published today, and the single open issue indicates a concrete bug affecting WhatsApp media handling that blocks agent functionality. Overall, the project appears in a maintenance and security-focused phase rather than feature expansion.

## Releases
No new releases were published today. The latest release remains the previous version.

## Project Progress
Two pull requests were closed/merged today:

- **[#2713 — feat(security): egress lockdown (opt-in, off by default)](https://github.com/nanocoai/nanoclaw/pull/2713)** (merged/closed) — Adds opt-in egress lockdown by placing agent containers on a Docker `--internal` network. Agents can only reach the outside via a configured gateway proxy, significantly improving network security posture.

- **[#2712 — [follows-guidelines] pull request](https://github.com/nanocoai/nanoclaw/pull/2712)** (closed) — A guidelines-compliance PR, likely a test or documentation update.

Both merged PRs represent progress on the project's security infrastructure, particularly **#2713** which introduces an important enterprise-grade feature for controlling agent network access.

## Community Hot Topics
The most active thread today is:

- **[#2715 — Inbound WhatsApp media unreachable by agent](https://github.com/nanocoai/nanoclaw/issues/2715)** (open, 0 comments, 0 reactions) — A blocking bug where WhatsApp attachments are saved to an unmounted host directory, causing the agent to receive invalid paths inside its container. Despite zero comments, this issue represents a significant usability barrier for WhatsApp channel users. The silence suggests either the reporter hasn't received attention yet or the issue is straightforward to diagnose.

No other issues or PRs have received comments or reactions in the last 24 hours.

## Bugs & Stability
One high-severity bug was reported today:

- **#2715 — Inbound WhatsApp media unreachable** — **Severity: High**. Files save to `DATA_DIR/attachments` on the host, which is not mounted into the agent container. The agent receives a `/workspace/attachments/...` path that does not exist inside the container, preventing agents from accessing images, documents, or audio files sent via WhatsApp. No fix PR exists yet. This is a blocking issue for any v2 deployment using WhatsApp for file exchange.

**No other bugs, crashes, or regressions were reported today.**

## Feature Requests & Roadmap Signals
The only clear feature signal today is:

- **Egress lockdown (#2713)** — Though merged, this opt-in security feature signals a roadmap focus on enterprise-grade network isolation. It's likely to become default-on in a future release once battle-tested.

Based on the security PRs and the WhatsApp attachment bug, the next version will likely include:
- Fix for WhatsApp attachment mounting (#2715)
- Tighter default security posture (binding to `127.0.0.1`, crypto-random IDs)
- Possibly enabling egress lockdown by default after testing

## User Feedback Summary
The single user-reported issue (#2715) reveals a clear pain point:

- **Pain point**: WhatsApp file exchange is broken on v2 due to container path mismatches. Users expecting standard chatbot functionality (sending/receiving media) are blocked.
- **Use case**: WhatsApp-based customer service or document processing agents.
- **Satisfaction**: Presumably low for this user, as the issue prevents a core feature from working.

No positive or negative sentiment feedback was otherwise recorded today.

## Backlog Watch
No long-unanswered issues or PRs were identified in today's data. All items are from 2026-06-08 and have maintainer or contributor engagement (PRs #2713, #2714, and #2715 were all recently created and updated). The project's backlog appears clean with no stale items requiring maintainer attention.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-09

## Today's Overview

Project activity is **very high**, with 33 issues updated and 50 pull requests updated in the last 24 hours — nearly balanced between open and closed/merged items. The Reborn v2 migration remains the dominant theme, with significant progress on OpenAI-compatible API routing, auth parity, and workflow decomposition. No new releases were published today; the project appears to be in a rapid development phase between the **v0.29.1** release and the next cutover milestone. Security hardening and bug fixes are receiving equal attention alongside feature work.

## Releases

**None** — no new releases were published today. The last release remains `ironclaw v0.29.1` (from PR #3708).

---

## Project Progress

**25 PRs were merged/closed today**, advancing several major workstreams:

### Reborn v2 Core
- **PR #4572** (merged) — Replaced `researcher` subagent flavor with `planner`, producing structured plans; redesigned `spawn_subagent` schema
- **PR #4523** (merged) — Fixed system sentinel round-trip through `string_id` Deserialize for `TenantId`/`UserId`
- **PR #4528** (merged) — Added filesystem-backed product workflow idempotency ledger for Slack host-beta state persistence
- **PR #4546** (merged) — Routed Responses through `ProductWorkflow` with non-streaming create/retrieve/cancel support
- **PR #4488** (closed) — Split `ProductWorkflow` into explicit `submit/read/subscribe` doors

### OpenAI-Compatible API
- **PR #4442** (closed) — Added OpenAI-compatible API ingress contracts
- **PR #4443** (closed) — Added product refs (`chatcmpl-*`, `resp_*`) and idempotency keys
- **PR #4495** (open) — Routing non-streaming Chat Completions through `ProductWorkflow`
- **PR #4552** (open) — Translating projection streams to OpenAI SSE format

### Auth & Security
- **PR #4576** (merged) — Extended `ToolCall` with `arguments_parse_error` field (RC3/M9 Phase B)
- **PR #4580** (merged) — Added automation run history UI with persistent trigger repositories
- **PR #4581** (merged) — Scoped outbound delivery defaults with versioned preference writes
- **PR #4560** (closed) — Routed Trace Commons onboarding HTTP through host network-egress policy
- **PR #4583** (open) — `NormalizingProvider` Layer-3 decorator for finish_reason normalization

### Bug Fixes
- **PR #4578** (merged) — Fixed `google_calendar list_events` returning oldest instead of upcoming events
- **PR #4566** (merged) — Auto-detected Codex `client_version` to unlock newer models (e.g., GPT-5.5)
- **PR #4536** (closed) — Fixed OAuth Google/GitHub users unable to chat

---

## Community Hot Topics

### Most Active Issues

**1. Issue #3283 — OpenAI-compatible Chat & Responses APIs onto Reborn**
- 3 comments, parent epic
- URL: https://github.com/nearai/ironclaw/issues/3283
- *Need*: Users and integrators need OpenAI-compatible API surfaces on the Reborn platform. This is the foundational tracking issue for migrating `/v1/chat/completions` and Responses endpoints.

**2. Issue #4175 — Reborn ProductAuth production backend parity**
- 3 comments, 3 days old
- URL: https://github.com/nearai/ironclaw/issues/4175
- *Need*: Production auth safety for OAuth PKCE — high availability and refresh token lifecycle remain incomplete for multi-tenant deployment.

**3. Issue #3957 — Third-party hooks activation hardening**
- 2 comments, security-review-required tag
- URL: https://github.com/nearai/ironclaw/issues/3957
- *Need*: Security hardening for third-party hook activation before enabling in multi-tenant production — durable quarantine and audit tracing are needed.

**4. Issue #3026 — Reborn production wiring and cutover readiness**
- 2 comments, P0 epic
- URL: https://github.com/nearai/ironclaw/issues/3026
- *Need*: The production graph must be built, validated, and prevented from serving traffic when services are missing — this is the primary cutover blocker.

### Most Active Pull Requests

**1. PR #4580 — Automation run history UI** (XL, merged)
- URL: https://github.com/nearai/ironclaw/pull/4580
- *Need*: Users need visibility into automation trigger runs — this adds a full UI with metrics, filters, and detail panel.

**2. PR #4581 — Scoped outbound delivery defaults** (XL, merged)
- URL: https://github.com/nearai/ironclaw/pull/4581
- *Need*: Trigger delivery configuration needed scoping for shared vs. personal agent runs.

**3. PR #4186 — Codex local-dev approval gates** (XL, open)
- URL: https://github.com/nearai/ironclaw/pull/4186
- *Need*: Developers need local approval gates for effectful built-in capability calls while preserving local-dev speed.

---

## Bugs & Stability

### High Severity

**1. OAuth Google/GitHub users can't chat (Issue #4536)**
- **Severity**: Critical — blocks SSO users entirely
- **Status**: **CLOSED** (fix merged)
- URL: https://github.com/nearai/ironclaw/issues/4536

**2. Telegram creates new conversation after upgrade 0.28.2 → 0.29.1 (Issue #4556)**
- **Severity**: High — breaks conversation continuity
- **Status**: Open, no fix PR yet
- URL: https://github.com/nearai/ironclaw/issues/4556

**3. Hosted agents return 403 Forbidden while instance is RUNNING (Issue #4557)**
- **Severity**: High — production availability issue
- **Status**: Open, instances recovered automatically
- URL: https://github.com/nearai/ironclaw/issues/4557

### Medium Severity

**4. Chat completion request duplicates `model` field with tools (DeepSeek 400) (Issue #4548)**
- **Severity**: Medium — breaks DeepSeek tool usage
- **Status**: Open
- URL: https://github.com/nearai/ironclaw/issues/4548

**5. Codex hardcoded `client_version` hides newer models (Issue #4564)**
- **Severity**: Medium — GPT-5.5 and beyond invisible
- **Status**: **CLOSED** (fix in PR #4566, merged)
- URL: https://github.com/nearai/ironclaw/issues/4564

**6. `google_calendar list_events` returns oldest events (Issue #4577)**
- **Severity**: Medium — wrong default behavior
- **Status**: **CLOSED** (fix in PR #4578, merged)
- URL: https://github.com/nearai/ironclaw/issues/4577

**7. Incomplete i18n coverage and translator runtime crashes (Issue #4554)**
- **Severity**: Medium — UI usability issue
- **Status**: Open
- URL: https://github.com/nearai/ironclaw/issues/4554

### Low Severity

**8. WeCom channel validation findings (Issue #4191)**
- **Severity**: Low — staging-only issues found
- **Status**: Open
- URL: https://github.com/nearai/ironclaw/issues/4191

**9. Nightly E2E test failure (Issue #4108)**
- **Severity**: Low — CI reliability
- **Status**: Open, likely transient
- URL: https://github.com/nearai/ironclaw/issues/4108

---

## Feature Requests & Roadmap Signals

### Likely in Next Release (v0.30.0?)

1. **OpenAI-compatible API on Reborn** — Multiple PRs (#4495, #4546, #4552) are actively routing Chat Completions and Responses through `ProductWorkflow`. This is the highest-priority feature and likely to land soon.

2. **Self-serve secret setup (Issue #4545)** — New epic for user-generated tool secrets via Slack/web/Telegram without exposing values to LLMs. A strong candidate for the next release.

3. **Runtime service profiles (Issue #4543)** — Credential injection for generic HTTP and skill-declared services (Crisp, Stripe). Direct user demand from production.

4. **Reborn approvals parity (Issue #4539)** — Approve-once, deny, always-allow for tool calls. Direct V1 parity gap being closed.

5. **Reborn operator setup (Issue #4533)** — V1 replacement requires onboarding, config, diagnostics, and lifecycle management for operators.

6. **Reborn Postgres production storage (Issue #4551)** — Wiring production Postgres config for the `ironclaw-reborn` binary.

### Lower Probability

7. **Subagent durability (PR #4582)** — Doc-only spec for WU-B subagent compaction; likely deferred to v0.31.0.

---

## User Feedback Summary

### Pain Points

1. **Conversation loss on upgrade** — Telegram conversations restarting after upgrading from v0.28.2 to v0.29.1 (Issue #4556). This affects production users.

2. **Model availability regressions** — Codex GPT-5.5 being hidden by hardcoded `client_version` (Issue #4564). Users cannot access newer models.

3. **Calendar tool usability** — `list_events` returning years-old events instead of upcoming ones (Issue #4577). Breaks "what's my next meeting?" workflows.

4. **SSO login blocking chat** — OAuth users (Google/GitHub) redirected to `/welcome` instead of chat (Issue #4536). This was a *production blocker* that has been fixed.

5. **DeepSeek tool integration broken** — Duplicate `model` field causing 400 errors (Issue #4548). Blocks tool-using workflows on DeepSeek.

### Satisfaction Signals

- The **automation run history UI** (PR #4580) was delivered, addressing a clear user need for visibility.
- **Codex client_version auto-detection** (PR #4566) was fix-merged the same day it was reported.
- **Google Calendar timeMin default** (PR #4578) was fix-merged the same day.

### General Sentiment

The community is actively reporting bugs in the v0.29.x staging/production transition. The rapid fix turnaround (same-day for several issues) indicates a responsive team, but the volume of regressions suggests the Reborn migration is introducing churn. Security-focused users will appreciate the ongoing auth and hooks hardening work (#3957, #4175).

---

## Backlog Watch

### Long-Unanswered Important Issues

1. **Issue #3288 — Reborn capability lifecycle admin parity** (38 days old)
   - No maintainer response in 24h
   - URL: https://github.com/nearai/ironclaw/issues/3288
   - *Risk*: This is a P2 suggested item but blocks extension/skill/MCP lifecycle migration.

2. **Issue #4557 — Hosted agents 403 Forbidden** (1 day old)
   - No maintainer comment yet
   - URL: https://github.com/nearai/ironclaw/issues/4557
   - *Risk*: Production availability issue that recovered automatically — needs root cause analysis.

3. **Issue #4191 — WeCom channel validation findings** (11 days old)
   - No maintainer response
   - URL: https://github.com/nearai/ironclaw/issues/4191
   - *Risk*: Validation findings for a new channel; multiple issues flagged but no action yet.

### Stale PRs Needing Attention

4. **PR #3708 — Release automation** (24 days open)
   - Release automation PR that has been open since v0.29.1
   - URL: https://github.com/nearai/ironclaw/pull/3708
   - *Risk*: CI automation gap that may delay future releases.

5. **PR #4186 — Codex local-dev approval gates** (11 days open)
   - XL PR with medium risk, no recent activity
   - URL: https://github.com/nearai/ironclaw/pull/4186
   - *Risk*: Codex development workflow improvement that may be stuck on review capacity.

---

*Data sourced from nearai/ironclaw GitHub activity on 2026-06-08 to 2026-06-09 UTC.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-06-09**.

---

## LobsterAI Project Digest — 2026-06-09

### 1. Today's Overview
The project experienced a significant burst of activity on 2026-06-08, with **19 PRs updated** and **18 merged or closed**. This high closure rate indicates a productive maintenance and feature push, likely targeting a near-term release. No new releases were cut today, and the issue tracker saw zero new bug reports, suggesting that recent development efforts are focused on polishing existing features and refactoring infrastructure rather than addressing new user-facing defects. The team appears to be in a strong consolidation phase.

### 2. Releases
**None.** No new releases were published in the last 24 hours.

### 3. Project Progress
The 18 merged/closed PRs represent a substantial push on **data safety**, **authentication UX**, **settings visibility**, and **stability patches** for stale bugs.

- **Data Migration & Backup (High Priority):** Three PRs by `fisherdaddy` (#2125, #2126, #2128) introduce a full user data backup/restore service. The implementation archives data into tarballs, preserves runtime lock files (SingletonLock, Cookie, lockfile), and includes a rollback mechanism on failure. This directly addresses a critical risk of data loss during migrations.
- **Authentication Overhaul:** A trio of PRs from `liuzhq1986` (#2122, #2127, #2129) rework the login flow. Key changes include a new **localhost callback server** to avoid browser confirmation dialogs for desktop login, improved window focusing on Windows after login, and enhanced diagnostic logging for callback redirects.
- **User Settings & Visibility:** The `fisherdaddy` PR #2123 exposes the OpenClaw gateway URL in settings, adding a copyable address card with status badges. PR #1522 by `leedalei` adds a "Fetch model list" button to automate pulling available models from provider APIs.
- **Stale Bug Fixes:** Seven older PRs (stale) were finally merged, fixing issues ranging from silent IM notification failures (#1510) to log export timeouts (#1515) and GitHub Copilot token loss (#1517). This shows a strong commitment to clearing technical debt.

### 4. Community Hot Topics
- **PR #2126 — `fix(data-migration): restore data in place and preserve runtime locks`** (Author: `fisherdaddy`)
  - **Context:** No comments recorded, but the nature of the fix (preserving locks during restore) addresses a high-risk scenario where a failed restore could lock users out of the app. This is a core reliability concern.
- **PR #2129 — `chore(auth): add login callback diagnostics`** (Author: `liuzhq1986`)
  - **Context:** While minor in code, the addition of diagnostics for callback URL detection (overmind vs. fallback) addresses a long-standing pain point for Windows users where the login flow fails without clear error messages.
- **PR #1510 — `定时任务选择IM通知频道后未选会话即可提交，运行时通知静默失败`** (Author: `MaoQianTu`)
  - **Context:** A classic form validation gap. Users could create a scheduled task with no recipient selected, causing silent failures. The fix adds validation in `TaskForm.tsx` and error messages, solving a trust-breaking UX issue.

### 5. Bugs & Stability
- **Critical: Data Loss & Lock Conflicts (Fixed):** The data migration PRs (#2125, #2126, #2128) directly address a scenario where restore operations could **delete user data** or **clobber runtime locks**, causing app crashes. Fix PRs are merged.
- **High: Silent IM Notification Failures (Fixed):** PR #1510 fixed a bug where scheduled tasks with IM notifications would silently fail if no conversation was selected. This was a regression in task reliability.
- **High: Log Export Timeout (Fixed):** PR #1515 resolved a 30-second timeout during log export caused by inefficient DEFLATE compression (100MB+ log files). The fix likely switches to streaming or lower compression.
- **Medium: GitHub Copilot Token Loss (Fixed):** PR #1517 fixed a bug where closing the settings panel during OAuth polling would discard a successfully fetched token.
- **Low: Config Migration (Fixed):** PR #2117 fixed a bug where user-deleted provider models were restored on app restart after a migration, ensuring user customizations are preserved.

### 6. Feature Requests & Roadmap Signals
- **Data Portability is Live:** The new backup/restore feature (#2125) is a clear signal that LobsterAI is improving portability and disaster recovery, likely in preparation for cloud sync or multi-device support.
- **Dynamic Model List (#1522):** The "fetch model list from API" feature suggests the team anticipates a future where provider model lists change frequently, and manual config is no longer viable. This is a direct response to user friction with new model discovery.
- **Session Color Coding (#1526):** The addition of 7-color session labels in the cowork feature indicates growing user demand for visual organization tools. This is a strong indicator of mature usage patterns.
- **Local Auth Flow (#2122):** The new localhost callback server simplifies desktop login, a **blocker for some Windows users** on dev mode. This may be a stepping stone to a fully offline/E2E auth flow.
- **Prediction for Next Version:** I predict v1.2+ will include the backup/restore service, the local auth flow, dynamic model fetching, and the session color labeling feature.

### 7. User Feedback Summary
- **Pain Points Addressed:**
  - **Data Safety:** Users feared losing data during system migrations. The new backup/restore directly solves this.
  - **Login Friction:** Windows users reported issues with browser-based login callbacks. The local callback server and window-focus fixes directly resolve this.
  - **Model Management:** Users complained about manually adding new models (e.g., GLM-5.1). The "Fetch model list" button automates this.
  - **Silent Failures:** Users were frustrated by scheduled tasks failing silently and log exports timing out without explanation.
- **Satisfaction Drivers:**
  - **Visual Organization:** The session color coding (#1526) addresses a clear user need for visual hierarchy.
  - **Better Diagnostics:** The auth callback logging and improved connection error messages (#1524) increase user trust.

### 8. Backlog Watch
- **PR #1277 — `chore(deps-dev): bump the electron group...`** (Author: `dependabot[bot]`) **— OPEN (since 2026-04-02)**
  - **Status:** This dependency bump (Electron 40 -> 42) has been open for over two months. While it is a dev dependency update, major Electron version bumps often include breaking API changes or security fixes. This should be triaged to ensure it doesn't block future feature work or expose vulnerabilities.
- **No unanswered Issues:** The issue tracker shows zero open/active issues, which is healthy but may also indicate low community bug reporting volume.

---

**Project Health Assessment:** ✅ **Healthy**. The team is executing a clear roadmap focused on reliability (backup, auth logs) and user-friendliness (model fetching, visual cues). The high volume of merged PRs with low open defect count suggests a disciplined engineering process.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

**Project Digest: TinyClaw / TinyAGI**  
**Date: 2026-06-09**

---

### 1. Today's Overview
The project is in a low-activity phase with zero new issues and no releases in the last 24 hours. One pull request (#280) remains open, addressing a known installation pain point for native module dependencies. No merges or closures occurred, indicating a period of maintainer review or low contributor throughput. Overall project health appears stable but stagnant on the public surface.

---

### 2. Releases
None. No new versions were published or tagged in the last 24 hours. The latest release remains unavailable in this period.

---

### 3. Project Progress
No pull requests were merged or closed today. The sole PR, #280, is still open and under review.

- **PR #280 (Open)** – Fix(install): Add postinstall script to auto-rebuild better-sqlite3  
  *Author: dsy122* | [Link](https://github.com/TinyAGI/tinyagi/pull/280)  
  This PR introduces automation for a common, manual installation step. It addresses a recurring friction point for developers deploying TinyClaw in fresh environments.

---

### 4. Community Hot Topics
With zero issues and only one PR active, community activity is minimal. The single open PR (#280) has generated no comments or reactions yet, suggesting either low visibility or that the fix is self-explanatory. The underlying need is clear: users want a zero-config install experience.

---

### 5. Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. There are no open bug reports to track. The existing PR (#280) is preventive, fixing a compilation failure in `better-sqlite3` that occurs on fresh installations, making it a **medium-severity** installation stability issue. No fix PRs were merged today.

---

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were submitted today. The PR #280 points to a desire for smoother developer onboarding and environment portability. Future versions may include similar postinstall automation or Docker-based build helpers, though no roadmap signals are present in the data.

---

### 7. User Feedback Summary
There is no direct user feedback captured in issues or PR comments today. The existence of PR #280 indicates that users have encountered a real pain point: manual `npm rebuild` steps after installation. This suggests dissatisfaction with the current setup process. No positive or negative feedback was explicitly shared.

---

### 8. Backlog Watch
There are no open issues or PRs that have been left unanswered for extended periods. PR #280 was opened June 8 and remains uncommented by maintainers as of this digest. It does not yet represent a backlog risk, but attentive maintainers should review and respond soon to keep the contribution pipeline healthy.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Based on the provided GitHub data for `agentscope-ai/CoPaw` (referenced as `QwenPaw` throughout the data), here is the project digest for **2026-06-09**.

---

### 1. Today's Overview

The CoPaw project is experiencing **elevated development velocity** today, with 45 updated Pull Requests (22 open) and 49 updated Issues (28 open). Activity is concentrated on stabilizing the platform after a recent `v1.1.10` release, addressing specific MCP server lifecycle bugs, and building out the plugin ecosystem. A major backend migration to AgentScope 2.0 (#4727) is in the planning phase, signaling significant architectural changes ahead. While no new releases were cut today, the community is highly engaged, with a strong emphasis on improving stability for enterprise channels (WeChat, DingTalk, Feishu) and enhancing the core agent loop.

### 2. Releases

**No new releases** were recorded in the last 24 hours.

### 3. Project Progress (Merged/Closed PRs)

Today saw a significant number of PRs merged or closed (23), fixing critical bugs and laying groundwork for new features.

- **Plugin Ecosystem Expansion:** The `feat(console): Plugin extension infrastructure` (#4997) was closed, establishing a formal frontend registry for plugins. This is complemented by the **new `Plugin Market` tab** (#5023, open), which will allow users to browse community plugins from the AgentScope Platform.
- **Security & Stability Fixes**:
    - `fix(security): isolate keychain master key per install` (#5028) was merged, preventing secret conflicts on shared machines.
    - `fix(agents): prevent duplicated session_id in filename` (#5026) resolves a data integrity issue for inter-agent requests.
- **Core Functionality & UI:**
    - The `feat(acp): advertise commands, surface errors...` (#4949) was closed, significantly improving the Agent Client Protocol (ACP) for users of the terminal TUI (`paw`).
    - The `fix(install): restrict mlx-lm to Apple Silicon macOS` (#2771) was finally merged after a long review, preventing install failures on Intel Macs.
    - `fix(console): localize session and cron job controls` (#4286) was merged, improving internationalization for the web frontend.

### 4. Community Hot Topics

The community is deeply engaged in two major conversations: the architecture of the agent itself and the stability of enterprise messaging channels.

- **Architecture & Inspiration (Issue #5017 - OPEN):** This feature request, with **7 comments and 2 👍**, proposes adopting the "Learning Loop" design from the **Hermes Agent** project. The user specifically requests CoPaw to evolve beyond its current skill system (even if it’s not a fork of OpenClaw) to implement automatic skill creation and iteration from agent behavior.
    - *Analysis:* This signals a strong user desire for the framework to move from a "tool orchestrator" to a "self-improving agent". This is likely to be a top priority for the next major release roadmap.
- **MCP Process Accumulation & Cleanup (Issue #4834 - OPEN):** A bug report with **4 comments** details how MCP server processes accumulate on every restart, leading to performance degradation. This is a critical stability concern.
    - *Analysis:* A corresponding fix has already been submitted in PR #5014, which is currently open for review.

### 5. Bugs & Stability

Several stability bugs were reported and fixed today, ranked by severity:

- **Critical - Memory Compaction Crash (Issue #5019, CLOSED):** A bug causing the agent to crash with an `AttributeError` when performing memory compaction (triggered by memory limits). The root cause is an unexpected string type in the `as_msg_handler`. **Status: Resolved**.
- **Critical - Cross-User Chat Merging in DingTalk (PR #4932, OPEN):** A fix is proposed for a dangerous bug where messages from entirely different DingTalk users could be merged into a single conversation due to a collision in the `conversation_id` suffix. **Status: Fix under review.**
- **High - MCP Process Leak (Issue #4834, OPEN / PR #5014, OPEN):** MCP server subprocesses survive container restarts, leading to resource exhaustion. A fix has been proposed to kill the process group on shutdown. **Status: Fix under review.**
- **High - Agent Conversation Hangs with Alibaba Model (Issue #5003, OPEN):** A user reports the agent gets stuck indefinitely when using the `aliyun-coding-plan` with `qwen3.7-plus`. **Status: Unresolved, requires investigation.**
- **Medium - Frontend UI Jitter (Issue #4993, OPEN):** Image preview drag behavior is broken on MacOS. A known UI regression.

### 6. Feature Requests & Roadmap Signals

User feature requests point toward a more autonomous and flexible agent framework.

| Feature Request | Issue # | Likely Path to Next Version | Signal Strength |
| :--- | :--- | :--- | :--- |
| **"Learning Loop" / Self-Evolving Agent** | #5017 | **High** - The idea of skill creation is a natural evolution. | High (2 👍, 7 comments) |
| **Independent Visual Model Option** | #4992 | **Medium** - A useful workaround for text-only models. | Medium (1 👍, 3 comments) |
| **Self-Evolving Memory System** | #4994 | **Medium** - Complements Issue #5017; memory is a prerequisite for learning. | Medium (1 👍) |
| **Suppress final text after tool calls** | #4838 | **Low-Medium** - Niche use case for "silent" automation. | Low |
| **Goal Mode (Session-Scoped Objectives)** | #4443 | **High** - Already has an open PR. Likely to be merged soon. | Very High (Open PR) |

### 7. User Feedback Summary

- **Satisfaction:** Users consistently praise the project's **localization and out-of-box experience**, especially for Chinese users ("国内用起来特别舒服"). The plugin system is well-received, with one user contributing a full "DataPaw" data-analysis plugin (#4622).
- **Pain Points:**
    - **WeChat/Enterprise Messaging Instability:** The most frequent complaints relate to token expiry (ret=-2), silent failures, and inability to interrupt agent loops from chat apps like WeChat Work and Feishu.
    - **Process Management:** Users are frustrated by orphaned backend processes and accumulating MCP subprocesses, which degrade performance over time.
    - **Model API Compatibility:** Users are encountering specific issues with GPT-5.5 tool name validation and KimiCode thinking display, indicating a need for better model abstraction.

### 8. Backlog Watch

Several issues require immediate maintainer attention to prevent user abandonment or scaling issues.

- **Priority High: OneBot WebSocket Port Leak (#4926 - OPEN, 2 comments):** This issue, addressing a classic port-bind failure after reloads for the OneBot channel (used by QQ bots), has an open PR (#?) but needs review. It is a blocker for QQ bot reliability.
- **Priority High: MCP Process Accumulation (#4834 - OPEN, 4 comments):** Fix on the way (#5014), but needs rigorous testing as it involves process group management.
- **Priority Medium: Long-Standing Chat Entry Corruption (#4151 - CLOSED?):** While closed, the issue of orphaned chat entries after restarts is a persistent UX problem. The root cause (race condition in session persistence) may re-emerge.
- **Priority Medium: `loop_config.json` / `prd.json` Corruption (#4970 - OPEN):** A single corrupt JSON file can kill an entire agent session. This is a brittle design point for the "mission" system that needs a defensive handling fix (e.g., try/except with fallback to defaults).

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-09

## Today's Overview

ZeroClaw shows **high activity** with 50 issues and 50 PRs updated in the last 24 hours, indicating a healthy, fast-moving open-source project. The team closed only 2 issues and 12 PRs today, suggesting a heavy emphasis on active development and open review cycles rather than mass merges. There are **no new releases** today. The issue tracker reveals significant attention to **security architecture** (OIDC support, pluggable security providers, per-execution shell confirmation), **MCP tool parity** (filter bugs, resource/prompt support), and **channel-specific regressions** (Matrix session collision, WhatsApp LID handling, Telegram prompt caching). The community is actively submitting and reviewing PRs targeting the upcoming **v0.9.0** milestone.

## Releases

No new releases were published today.

## Project Progress

**12 PRs were closed/merged today**, including several that address longstanding bugs and regressions:

- **[PR #7388](https://github.com/zeroclaw-labs/zeroclaw/pull/7388) (merged)** — `fix(matrix): isolate session state per channel alias and repair key backup` — Closes the S1-severity multi-alias Matrix session clobber bug (#6487). This is a **breaking change** requiring manual session migration, as the state directory moves from a shared `<config_dir>/state/matrix/` to per-alias `<config_dir>/state/matrix/<alias>/`.

- **[PR #7403](https://github.com/zeroclaw-labs/zeroclaw/pull/7403) (merged)** — `fix(runtime): guard trim_history against orphan-cascade emptying all messages` — Prevents a scenario where conversation history trimming could delete all non-system messages.

- **[PR #6701](https://github.com/zeroclaw-labs/zeroclaw/pull/6701) (merged)** — `fix(telegram): preserve markdown fences when splitting messages` — Addresses the "Smart Truncation for Telegram" feature request (#6225), ensuring code blocks aren't broken across message splits.

- **[PR #6148](https://github.com/zeroclaw-labs/zeroclaw/pull/6148) (merged)** — `feat(hardware): smart-room ESP32 demo with Telegram + simulator` — A hackathon project delivering an end-to-end demo integrating Telegram, ZeroClaw, and an ESP32 smart-room controller.

Other notable open PRs advancing toward merge include work on **per-field MCP server editing** via the web dashboard (PR #7267), **AMQP inbound channel support** with mutual TLS for SOP workflows (PR #7369), **per-turn output routing** across channels (PR #7361), and **WASI plugin interface definitions** (PR #7060).

## Community Hot Topics

**Most active issues** (by comment count over the last 24h):

1. **[Issue #6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699) (7 comments)** — `tool_filter_groups is a no-op for real MCP tools` — Two distinct bugs: (a) prefix-check mismatch in the dispatch-time filter, (b) no integration with the deferred loading system. This blocks operators who rely on `tool_filter_groups` to restrict MCP tool surfaces, and has been open since May 16 with `priority:p1` status.

2. **[Issue #6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) (6 comments)** — `RFC: Computer-use support for desktop screen interaction and input control` — Users explicitly compare ZeroClaw to OpenAI Codex and openclaw/hermes' computer-use capabilities. This is a high-demand feature for desktop automation workflows.

3. **[Issue #5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) (5 comments)** — `[Bug]: Too much emphasis on memory` — Users report that in cron jobs especially, the system prompt gives too much priority to stored memories over the current instruction. Updated today with a new comment, suggesting ongoing frustration.

4. **[Issue #7184](https://github.com/zeroclaw-labs/zeroclaw/issues/7184) (5 comments)** — `RFC: Move translated .ftl and .po files into a git submodule` — A structural proposal to reduce repository churn from translation commits. Indicates growing internationalization workload.

5. **[Issue #4832](https://github.com/zeroclaw-labs/zeroclaw/issues/4832) (4 comments)** — `Add config option to disable LeakDetector high-entropy token redaction` — False positives on MD5 filenames, randomly generated media files. Users need an escape hatch for legitimate content.

**Underlying need analysis**: The community is pushing for **production-grade security controls** (pluggable security providers, OIDC, per-command confirmation tiers), **MCP maturity** (filtering, resources/prompts, proper deferred loading), and **better channel UX** (Telegram message splitting, Matrix multi-alias isolation, WhatsApp LID handling). The recurring theme is **configuration that actually works as documented** — the `tool_filter_groups` and `max_tool_iterations` bugs (issues #6699, #6877) undermine user trust in the config system.

## Bugs & Stability

**Critical bugs updated today (S0-S1):**

- **[Issue #4627](https://github.com/zeroclaw-labs/zeroclaw/issues/4627)** (S0 — data loss/security risk, 3 comments) — `file_write silently fails` — Files written by the agent are invisible on the host filesystem. **Fix PR #7129 exists** (still open), which guards against writing to ephemeral workspaces across all file tools.

- **[Issue #6487](https://github.com/zeroclaw-labs/zeroclaw/issues/6487)** (S1, 1 comment, **CLOSED**) — `Multi-alias Matrix instances share one session store` — **Fixed today by PR #7388**, though the fix is a breaking change requiring manual migration.

- **[Issue #5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)** (S0, 4 comments) — `consecutive OOM in WSL2` — The daemon is killed by the kernel OOM killer (total-vm > 17GB RSS > 8GB). Status is `in-progress` with `r:needs-repro` — no reproduction steps available yet.

- **[Issue #6434](https://github.com/zeroclaw-labs/zeroclaw/issues/6434)** (S1, 2 comments) — `Shell tool calls refused at [autonomy] level = "full"` — A fully permissive config still blocks shell tool execution. Status `in-progress` with `priority:p1`.

**High-severity bugs (S1-S2) updated today:**

- **[Issue #6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302)** — `Gemini 400 — assistant tool_call emitted as first non-system turn` — The history serializer violates Gemini's requirement that a conversation start with a user turn.

- **[Issue #6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361)** — `context_compression drops assistant(tool_calls) and tool(result) for OpenAI-compatible providers` — Causes tool loops and invalid message role errors for MiniMax and similar providers.

- **[Issue #6350](https://github.com/zeroclaw-labs/zeroclaw/issues/6350)** — `WhatsApp Web — allowed-numbers bypassed for LID-based contacts` — Messages are silently dropped with no operator-visible error, an invisible security bypass.

- **[Issue #6877](https://github.com/zeroclaw-labs/zeroclaw/issues/6877)** — `runtime_profiles.*.max_tool_iterations has no effect` — Must be set on `[agents.*]` instead, despite documentation. Confirmed by source inspection and empirical testing.

**Regression signals**: The **bulk revert of 153 commits** (issue #6074, `priority:p2`, `in-progress`) is being tracked for recovery — this is a latent source of regressions as features removed in that revert may need re-implementation.

## Feature Requests & Roadmap Signals

**High-priority features active today:**

- **[Issue #7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)** — `OIDC Authentication Provider support` — A tracking issue targeting **v0.9.0** with a pluggable authentication-provider interface. This is a security/architecture cross-cutting concern.

- **[Issue #7142](https://github.com/zeroclaw-labs/zeroclaw/issues/7142)** — `Pluggable security provider interface` — Also targeting **v0.9.0**, umbrella for exposing security enforcement, reporting, and incident response behind a single trait.

- **[Issue #7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)** — `RFC: Per-execution confirmation tier for high-risk shell commands` — A Claude Code-style allow/ask/deny pattern policy, filling a gap between today's binary allow-vs-deny for shell commands.

- **[Issue #6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)** — `RFC: Computer-use support for desktop screen interaction` — Screenshot capture + mouse/keyboard event control, matching OpenAI Codex capabilities.

- **[Issue #3767](https://github.com/zeroclaw-labs/zeroclaw/issues/3767)** — `Cross-channel TOTP gate for critical tool execution` — Extends OTP enforcement to all channels (Telegram, Discord, Matrix) with admin command gating.

**Prediction for next version (v0.9.0):** Based on tracking issues and PR activity, v0.9.0 will likely include **OIDC authentication**, **pluggable security provider interface**, **per-execution shell confirmation tiers**, **computer-use support** (screenshot + input control), and **MCP resource/prompt support** (issue #4467). The AMQP channel work and WASM plugin interface definitions also appear on track.

**Deferred/less likely:** The `tool_filter_groups` fix (#6699) may slip if the fix is complex; it requires fixing both the prefix-check mismatch and deferred loading integration. The i18n submodule proposal (#7184) is a process change, not a feature.

## User Feedback Summary

**Pain points (directly reported):**

- **Memory overemphasis** (issue #5844): "System prompt should be altered... to give less priority to memories and more to the current prompt." Users in cron jobs see degraded behavior.

- **Configuration doesn't work as documented**: Issues #6699 (`tool_filter_groups` no-op), #6877 (`max_tool_iterations` ignored), and #6434 (shell refused at `level = "full"`) all indicate **user trust erosion** in the config system. Each represents a case where documentation promises functionality that doesn't work.

- **Silent failures**: The file_write bug (#4627), WhatsApp allowed-numbers bypass (#6350), and the Matrix session clobbering (#6487) all cause **silent data loss or security bypasses** with no user-visible error.

- **Channel localization gaps**: "Some user-visible channel runtime replies are still hard-coded English strings even when ZeroClaw is configured with a non-English locale" (issue #6548). Non-English users get a mixed experience.

- **Prompt caching broken on Telegram**: "when chatting over CLI, prompt caching works as expected. when chatting over telegram, I am getting 'forcing full prompt re-processing'" (issue #6360). Users on Telegram pay higher LLM costs.

**Use cases reported:**

- Cron jobs for daily briefings (issue #5844)
- Desktop automation via computer-use (issue #6909)
- Smart-room/home automation with ESP32 + Telegram (PR #6148, PR #7363)
- SOP (Standard Operating Procedure) pipelines with AMQP (PR #7369)
- Multi-alias Matrix deployments (issue #6487, now fixed)
- Local-first small-model deployments (issue #5287)

**Satisfaction signals:** The community is actively contributing — the hardware demo, WASI plugin interface, and per-turn routing PRs show engaged developers building on the platform. The 4 reactions on issue #4467 (MCP resource/prompt support) and 2 reactions on #5287 (local-first mode) and #4879 (Gemini OAuth) indicate strong community desire for specific features.

## Backlog Watch

**Long-running open issues needing attention:**

- **[Issue #3767](https://github.com/zeroclaw-labs/zeroclaw/issues/3767)** — `Cross-channel TOTP gate` — Created March 17, still `in-progress` with `priority:p1`. 81 days old. This is a key security feature for multi-channel deployments.

- **[Issue #4467](https://github.com/zeroclaw-labs/zeroclaw/issues/4467)** — `MCP resource and prompt support` — Created March 24, still `in-progress` with 4 👍 reactions. 77 days old. MCP parity is a frequent ask; the bug #6699 shows the current MCP integration is incomplete.

- **[Issue #5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)** — `Local-First Mode for Small Models` — Created April 4, still `in-progress`. 66 days old. Important for the on-prem/self-hosted use case.

- **[Issue #6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)** — `Audit: track 153 commits lost in bulk revert` — Created April 24, still `in-progress`. 46 days old. A **risk to project stability** — until this is resolved, features and fixes from those 153 commits may need re-implementation.

- **[Issue #5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)** — `Consecutive OOM in WSL2` — Created April 9, `r:needs-repro` with no reproducer. 61 days old. S0 severity but blocked on reproduction — needs maintainer or community help narrowing down the trigger.

**PRs needing maintainer action:**

- **[PR #6973](https://github.com/zeroclaw-labs/zeroclaw/pull/6973)** — `fix(channels/whatsapp-web): pass LID JIDs unchanged` — Labeled `needs-author-action`, open since May 27. Fixes a S2-severity WhatsApp bug (#6350) that silently drops messages.

- **[PR #7369](https://github.com/zeroclaw-labs/zeroclaw/pull/7369)** — `feat(channels/sop): AMQP inbound channel with mutual TLS` — A large feature PR with no review comments yet after 1 day. May benefit from early maintainer feedback to avoid rework.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*