# OpenClaw Ecosystem Digest 2026-07-16

> Issues: 471 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-16 01:19 UTC

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

# OpenClaw Project Digest — 2026-07-16

## 1. Today's Overview

OpenClaw shows **intense development activity** with 471 issues and 500 PRs updated in the last 24 hours — placing this among the project's most active days on record. A new **v2026.7.2-beta.1** release shipped today, highlighting remote coding sessions, cloud worker support, and terminal-based session resumption. However, the release train faces **significant stability headwinds**: a cluster of P0 crash-loop bugs related to legacy state migration and gateway startup failures in v2026.7.1 dominate the issue tracker, with multiple users reporting upgrade breakage that `openclaw doctor --fix` cannot resolve. The community is both excited about new capabilities and frustrated by regression churn.

---

## 2. Releases

### v2026.7.2-beta.1 (released today)
[openclaw/openclaw v2026.7.2-beta.1](openclaw/openclaw Releases)

**Highlights:**
- **Remote coding sessions:** Run Control UI sessions on cloud workers; open Codex and Claude catalog sessions in terminals on their owning hosts; resume OpenCode and Pi sessions directly in a terminal.
- **Native automation and nodes:** Expanded node support (details truncated in source).

**Migration notes:** The release description was cut short in the source data. Given the severe migration bugs reported against v2026.7.1 (see Bugs & Stability section), **users on v2026.7.1 should test this beta carefully in non-production environments first** before upgrading production instances.

---

## 3. Project Progress

Today's closed/merged activity (173 PRs) includes:

| PR | Status | Description | Impact |
|---|---|---|---|
| [#108538](openclaw/openclaw PR #108538) | Merged | Tightened dead-code analysis for 15 extension workspaces, removing unused exports | Build quality |
| [#95400](openclaw/openclaw PR #95400) | Merged | Codex usage-limit payloads now properly classified for model fallback | Fixes model fallback chain (related to [#103734](openclaw/openclaw Issue #103734)) |
| [#108512](openclaw/openclaw PR #108512) | Merged | Zalo channel now uses timing-safe media token comparison | Security fix |
| [#107227](openclaw/openclaw Issue #107227) | Closed | Migration gate crash-loop bug accepted as closed | Bug acknowledged as fixed |
| [#103076](openclaw/openclaw Issue #103076) | Closed | Additional legacy migration sources blocking startup | Partial fix merged |

**Major feature PRs still open but advancing:**
- **Autonomous agent loop** ([#108206](openclaw/openclaw PR #108206)) — `feat(loop): implement autonomous agent loop with token budget guard` — Close #107423
- **Grouped Claw schema** ([#101328](openclaw/openclaw PR #101328)) — Read-only RFC 0016 slice for agent/workspace/packages ownership boundaries
- **Slack user identity sessions** ([#108522](openclaw/openclaw PR #108522)) — Enables dedicated member account DMs in Slack

---

## 4. Community Hot Topics

### Most Controversial: Platform Expansion Demand
- [#75](openclaw/openclaw Issue #75) — **Linux/Windows Clawdbot Apps** (113 comments, 81 👍)
  - *Status:* Open since Jan 2026, P2, needs product decision
  - *Analysis:* The single most commented-upon issue is a **7-month-old feature request** for desktop apps on non-Apple platforms. The fact that this still lacks a maintainer decision is a growing community pain point — users feel their platforms are second-class citizens.

### Most Critical: Gateway Crash-Loop Cluster (4 P0 bugs)
| Issue | Comments | Summary |
|---|---|---|
| [#107220](openclaw/openclaw Issue #107220) | 8 | Legacy memory sidecar `meta`/`chunks` conflicts are fatal while `files` auto-resolve |
| [#107227](openclaw/openclaw Issue #107227) (Closed) | 8 | `startup-migration gate is fatal` — `openclaw doctor` doesn't resolve crash-loop |
| [#107694](openclaw/openclaw Issue #107694) | 7 | Gateway fails to start on benign legacy migration skips |
| [#107727](openclaw/openclaw Issue #107727) (Closed) | 7 | Plugin install metadata conflict for codex/discord blocks gateway readiness |

*Underlying need:* The v2026.7.1 upgrade path is **brittle and user-hostile** — long-lived installs hit fatal startup failures with no documented recovery path.

### Model Fallback & Provider Issues
- [#85103](openclaw/openclaw Issue #85103) — Model fallback chain not triggered on provider-wide quota exhaustion (10 comments, P1)
- [#94518](openclaw/openclaw Issue #94518) — DeepSeek cache hit rate <10% after 6.x upgrade (9 comments, 10 👍)
- [#103734](openclaw/openclaw Issue #103734) (Closed) — Codex usage-limit surfaced as `promptError` instead of thrown — **fallback never fires**

*Underlying need:* Users running hybrid/multi-provider setups need **reliable fallback chains** that actually work — this has been a recurring pain for months.

---

## 5. Bugs & Stability

### P0 (Critical — Gateway Crash-Loop / Release Blockers)

| Issue | Summary | Has Fix PR? |
|---|---|---|
| [#107220](openclaw/openclaw Issue #107220) | `2026.7.1 gateway crash-loop: legacy memory sidecar conflicts fatal` | PR not yet linked in data |
| [#107694](openclaw/openclaw Issue #107694) | `Gateway fails to start due to strict startupMigrationWarnings guard` | Not yet |
| [#107727](openclaw/openclaw Issue #107727) (CLOSED) | Plugin install metadata conflict blocks gateway readiness | Closed, presumed fixed |
| [#107227](openclaw/openclaw Issue #107227) (CLOSED) | Startup migration gate fatal, doctor doesn't fix | Closed with fix |
| [#103076](openclaw/openclaw Issue #103076) (CLOSED) | Additional legacy-state migration sources block startup | Closed with fix |
| [#107330](openclaw/openclaw Issue #107330) | `OpenClaw Update 2026.7.1 Crash` on Windows 11 | Not yet |

### P1 (High — Data Loss / Session Corruption / Provider Failure)

| Issue | Summary | Impact |
|---|---|---|
| [#91009](openclaw/openclaw Issue #91009) | Codex PreToolUse hook spawns CPU-bound processes, stalls RPC | Crash-loop |
| [#107449](openclaw/openclaw Issue #107449) | `cron` tool JSON Schema incompatible with llama.cpp (pattern: `\S`) | Regression since prior working |
| [#106779](openclaw/openclaw Issue #106779) | `llama.cpp` provider fails with 400 on 2026.7.1 (MacBook Pro M5 Max) | Local inference broken |
| [#96834](openclaw/openclaw Issue #96834) | WhatsApp image wedges lane ~3min before processing | Multimodal UX broken |
| [#77012](openclaw/openclaw Issue #77012) | WebChat transcript overwritten every turn (regression) | Data loss |
| [#101763](openclaw/openclaw Issue #101763) | Hosted Molty: model selector doesn't persist (dot vs dash in model ID) | API compatibility |

### Recurring Theme: Legacy State Migration (v2026.7.1)
At least **5 distinct P0/P1 bugs** trace to the same root cause: the v2026.7.1 upgrade introduces a strict legacy-migration gate that treats benign conflicts as fatal, while `openclaw doctor --fix` cannot resolve them. This is the **most urgent stability issue** in the project right now.

---

## 6. Feature Requests & Roadmap Signals

### Likely for Next Release (v2026.7.x)
| Feature | Issue/PR | Reasoning |
|---|---|---|
| **Autonomous agent loop** | [#108206](openclaw/openclaw PR #108206) | Large PR under active review by maintainers; closes feature request [#107423] |
| **Iteration budget for agent safety** | [#97485](openclaw/openclaw PR #97485) | Production incident-driven safety feature |
| **Intelligent Multi-LLM Router** | [#107686](openclaw/openclaw Issue #107686) | Closed as feature request, P3, but high user demand for cost optimization |
| **Grouped Claw schema** | [#101328](openclaw/openclaw PR #101328) | RFC 0016 implementation advancing |

### Needs Product Decision (Stalled)

| Issue | Feature | Age | Blockers |
|---|---|---|---|
| [#75](openclaw/openclaw Issue #75) | Linux/Windows Clawdbot Apps | 7 months | No product decision; needs maintainer review |
| [#11665](openclaw/openclaw Issue #11665) | Multi-turn webhook sessions | 5 months | No product decision; linked PR open |
| [#82548](openclaw/openclaw Issue #82548) | AI safety & quality observability | 2 months | No product decision; security review needed |
| [#87660](openclaw/openclaw Issue #87660) | Lifecycle-aware LLM curation for MEMORY.md | ~7 weeks | No product decision |

### Predictions
The **autonomous loop** and **iteration budget** features are likely to land in v2026.7.2 or v2026.7.3, as both have active maintainer-driven PRs. The **multi-LLM router** may be deferred to v2026.8.x given its P3 priority. The **Linux/Windows Clawdbot Apps** request (#75) shows no signs of progress and risks becoming a community grievance.

---

## 7. User Feedback Summary

### Pain Points (High Severity)

1. **"Upgrade broke everything"** — Multiple users (liewjiajun, Marvinthebored, HankSU7889, smelike, scoutnj19) reported that **upgrading to v2026.7.1 caused gateway crash-loops** with no working repair path. User Marvinthebored: *"`openclaw doctor` doesn't resolve the conflict — gateway crash-loops with no documented remedy."*

2. **"Model fallback doesn't work"** — Users rickrvo, Maless88, xiep-dot report that fallback chains fail to trigger on provider quota exhaustion, usage limits, or OAuth failures. "The model fallback simply didn't fire."

3. **"Session state is fragile"** — Recurring `EmbeddedAttemptSessionTakeoverError` (jonah791, rickrvo, garnetlyx), WebChat transcript loss (#77012), and message delivery failures continue to undermine user trust.

4. **"Local models broken again"** — User delimir on M5 Max MacBook: "Fails: any local llama.cpp provider" with `400 Unable to generate parser for this template`. User Patt92 reports `cron` tool JSON Schema breaks llama.cpp.

5. **"Platform inequality"** — The **#75 issue** (113 comments, 81 👍) represents a simmering sentiment that macOS/iOS users get full support while Linux/Windows users are left waiting indefinitely.

### Satisfaction Signals
- **Remote coding sessions** in v2026.7.2-beta.1 are the most positively received new capability.
- Users appreciate the active fix pace: many closed bugs today indicate the team is responsive.
- The **refactor to narrow plugin SDK exports** ([#108440](openclaw/openclaw PR #108440)) signals attention to downstream developer experience.

---

## 8. Backlog Watch

### Long-Unanswered Critical Issues (No Maintainer Response in 30+ Days)

| Issue | Age | Priority | Summary | Concern |
|---|---|---|---|---|
| [#67915](openclaw/openclaw Issue #67915) | 90 days | P2 | "Local assistant attachments shown as 'Unavailable — Outside allowed folders' despite correct config" | User workflow blocked; linked PR open |
| [#75621](openclaw/openclaw Issue #75621) | 76 days | P1 | Gateway lazy-spawns duplicate stdio MCP children — memory + CPU leak | Closed stale, but no fix merged |
| [#77012](openclaw/openclaw Issue #77012) | 73 days | P1 | WebChat transcript overwritten every turn (regression) | Still open, needs live repro |
| [#83968](openclaw/openclaw Issue #83968) | 58 days | P1 | Gateway crashes on macOS with `assert(!this.paused)` — rollback required | Still open, needs maintainer review |
| [#77625](openclaw/openclaw Issue #77625) | 72 days | P2 | `reasoningDefault=stream` causes infinite reasoning recursion | Needs maintainer review + product decision |
| [#84783](openclaw/openclaw Issue #84783) | 56 days | P1 | Moonshot Discord runs spend ~30s in model-resolution before dispatch | Needs live repro |

### PRs Awaiting Maintainer Review (>30 days)

| PR | Age | Summary |
|---|---|---|
| [#89039](openclaw/openclaw PR #89039) | 45 days | `fix: prevent silent message loss from EmbeddedAttemptSessionTakeoverError` — Large, messy merge risks |
| [#97175](openclaw/openclaw PR #97175) | 19 days | `fix(context-engine): bound deferred turn maintenance with per-task timeout` — AI-assisted, ready for look |
| [#95289](openclaw/openclaw PR #95289) | 26 days | `fix: bound Codex Telegram turns fail after /codex bind on OAuth refresh` — Ready for maintainer look |

### Warning Signal
- **Issue #75** (Linux/Windows apps) has been open for **197 days** with 113 comments, 81 reactions, and **zero maintainer response beyond label assignments**. This gap between community demand and maintainer attention is the project's most prominent community-relations risk.

---

## Summary Assessment

| Dimension | Score | Notes |
|---|---|---|
| **Release velocity** | ⚡ Very High | 2 releases in 2 weeks (v2026.7.1 → v2026.7.2-beta.1) |
| **Stability** | 🔴 Critical | P0 crash-loop cluster on upgrade; multiple regression chains |
| **Community engagement** | 🟡 Active but strained | High bug report volume; growing platform inequality frustration |
| **Developer experience** | 🟢 Good | Plugin SDK refactoring, QA lab improvements, CI type fixes |
| **Backlog health** | 🟡 Warning | 5+ critical bugs stale >30 days; 3 high-severity PRs waiting on maintainer |

**Bottom line:** The project is shipping fast but bleeding stability. The v2026.7.1 upgrade path needs an **urgent patch release** focused on migration fixes. The autonomous loop and remote session features indicate strong product vision, but the regression churn is eroding user trust.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem
**Date:** 2026-07-16

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing **intense development velocity** across the board, with eight of eleven tracked projects showing significant activity in the last 24 hours. The landscape is bifurcating along two axes: **stability vs. bleeding-edge features** and **general-purpose agents vs. specialized toolchains**. OpenClaw, Hermes Agent, IronClaw, and ZeroClaw lead the pack in raw development throughput, each processing 40–500+ PR/issue updates daily, while smaller projects like Moltis and TinyClaw demonstrate focused, targeted iteration. A clear pattern emerges: projects that shipped major upgrades in the last 2–4 weeks (OpenClaw v2026.7.x, CoPaw 2.0, Hermes Agent v0.18.x) are now contending with **regression clusters and migration pain**, while those in consolidation phases (NanoBot, PicoClaw) are investing in security audits and test coverage. The ecosystem continues to converge on **multi-provider resilience**, **agentic autonomy**, and **cross-platform portability** as non-negotiable base requirements.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | PRs Merged/Closed (24h) | Release Status | Health Score |
|---------|----------------------|--------------------|--------------------------|----------------|--------------|
| **OpenClaw** | 471 | 500 | 173 | v2026.7.2-beta.1 (today) | 🟡 Active but unstable |
| **Hermes Agent** | 50 | 50 | 31 closed issues, 1 PR merged | v0.18.2 (stable) | 🟢 High stability |
| **NanoBot** | 24 | 26 | 11 | None | 🟢 Hardening phase |
| **IronClaw** | 23 | 38 | 13 | None (v0.29.x pending) | 🟡 High velocity |
| **ZeroClaw** | 38 | 50 | 12 | v0.8.x (CI blocked) | 🟡 Heavy PR pipeline |
| **CoPaw** | 50 | 43 | 22 | QwenPaw 2.0 (fresh release) | 🟡 Migration pains |
| **LobsterAI** | 6 | 17 | 11 | v2026.7.15 (today) | 🟢 Healthy |
| **NanoClaw** | 2 | 11 | 4 | None | 🟢 Moderate growth |
| **Moltis** | 0 | 6 | 6 | None | 🟢 Focused |
| **PicoClaw** | 3 | 1 | 0 | v0.3.1 (prior) | 🟡 Low maintainer activity |
| **TinyClaw** | 0 | 1 | 0 | None | 🟢 Stable but low engagement |
| **NullClaw** | 0 | 0 | 0 | None | ⚪ Inactive |
| **ZeptoClaw** | 0 | 0 | 0 | None | ⚪ Inactive |

**Key insight:** OpenClaw dominates raw volume (471 issues, 500 PRs) but has a **critical stability concern** — the only project with P0 crash-loop bugs and acknowledged upgrade breakage. IronClaw and ZeroClaw show comparable PR throughput but with better stability profiles.

---

## 3. OpenClaw's Position

### Advantages vs. Peers
- **Release velocity:** 2 releases in 2 weeks (v2026.7.1 → v2026.7.2-beta.1) — fastest cadence in the ecosystem.
- **Feature breadth:** Remote coding sessions, cloud workers, terminal session resumption — capabilities that only Hermes Agent (via Telegram/DM topics) and ZeroClaw (via gateway endpoint) partially match.
- **Community scale:** 113 comments on the Linux/Windows app request (#75) dwarfs comparable requests in any other project (IronClaw's Slack regressions: ~3–5 comments; CoPaw's Kylin OS request: 1 comment).
- **Developer experience investment:** Plugin SDK refactoring, dead-code analysis, CI type fixes — signals commitment to ecosystem builders.

### Technical Approach Differences
- **Architecture:** OpenClaw's "Claw" schema (RFC 0016) for agent/workspace/package boundaries is unique — no other project has formalized ownership domains at this level. ZeroClaw's closest equivalent (plugable security, principal isolation) is still in RFC stage.
- **Migration strategy:** OpenClaw's aggressive legacy state migration (the root cause of its crash-loop cluster) reflects a **cut-over** philosophy. Hermes Agent and NanoBot prefer **gradual deprecation** with backward compatibility — resulting in fewer upgrade incidents but slower adoption of new architectures.
- **Provider model:** OpenClaw's model fallback chain is sophisticated but broken in practice (see #85103, #103734). IronClaw's "unified generic extension runtime" takes a different approach — channel lifecycle state machines rather than linear fallback chains.

### Community Size Comparison
| Metric | OpenClaw | Next Largest (Hermes Agent) |
|--------|----------|------------------------------|
| Issue reactions on top request | 81 👍 (#75) | 5 👍 (#3326) |
| Comments on top request | 113 | 4 |
| P0 bugs open | 2 (after fixes) | 0 (both fixed today) |
| PRs waiting >30 days | 3 | 4–5 |
| External contributor PRs today | ~15% of merged | ~20–30% of merged |

OpenClaw's community is **larger and louder** — but the noise includes significant frustration. Hermes Agent's community is smaller but more satisfied (both P0 bugs fixed within 24 hours of reporting).

---

## 4. Shared Technical Focus Areas

The following requirements are emerging across **three or more projects**, indicating ecosystem-wide priorities:

| Focus Area | Projects | Specific Needs |
|------------|----------|----------------|
| **Multi-Provider Resilience** | OpenClaw (#85103), Hermes Agent (#63680), NanoClaw (#3057), ZeroClaw (#5600) | Fallback chains that work on quota exhaustion; graceful 400/5xx handling; per-agent failover |
| **Session Persistence & State** | OpenClaw (#77012), Hermes Agent (#63713), NanoBot (#4940), CoPaw (#6148) | No transcript/data loss on restart; memory compaction; context surviving crashes |
| **Channel Reliability** | IronClaw (#5877, #5943), Hermes Agent (#63911), LobsterAI (#1383), CoPaw (GBK encoding) | Telegram/DM message loss; Slack disconnect/reconnect; channel state machines |
| **Cross-Platform Desktop** | OpenClaw (#75), Hermes Agent (#63698, Windows), CoPaw (#6076, Windows 7), PicoClaw (#3260, ARM64) | Linux/ARM support; no console flash; consistent build targets |
| **Agent Autonomy & Safety** | OpenClaw (#108206), NanoBot (#4942), Hermes Agent (#37935), ZeroClaw (#8794) | Iteration budgets; approval gates; mid-task interruption handling |
| **Observability** | OpenClaw (#82548), Hermes Agent (#65272), ZeroClaw (#6641), NanoBot (audit findings) | OTel trace correlation; per-message timestamps; scriptable CLI output |

**Notable gap:** No project has shipped a reliable **multi-model routing** capability (e.g., route codegen to Codex, chat to Claude). Moltis's #574 is the only RFC on this topic, and it has been open for 3 months without maintainer response.

---

## 5. Differentiation Analysis

| Feature Focus | OpenClaw | Hermes Agent | IronClaw | ZeroClaw | CoPaw |
|---------------|----------|---------------|----------|----------|-------|
| **Primary use case** | Universal agent with remote coding | Desktop/TUI agent with Telegram focus | Enterprise agent with Slack/GitHub CI | Multi-user/multi-agent production | Chinese market agent (Qwen) |
| **Target user** | Power users, developers | Individual power users | Teams, QA, DevOps | Production operators | Enterprise, government |
| **Unique strength** | Cloud worker sessions, remote coding | Fast bug triage (P0s fixed same-day) | Channel lifecycle state machines | OIDC auth, plugable security | QwenPaw 2.0, memory system |
| **Weakness** | Upgrade instability, regression churn | Windows UX gaps, 49 open PRs | Slack reliability across 4 bug-bash waves | CI blocked for v0.8.x release | v2.0 migration pains |
| **Community language** | English (global) | English (global) | English (global) | English (global) | Chinese (primary) |
| **License** | Open source (OSI) | Open source | Open source | Open source | Open source |

**Architectural divergence:**
- **OpenClaw, ZeroClaw, NanoClaw** adopt **microservice/gateway patterns** — channels as pluggable, stateful services
- **Hermes Agent, TinyClaw** favor **monolithic desktop-first** — one binary, CLI + TUI
- **CoPaw** is the only project deeply tied to a **specific model family** (Qwen), though Moltis is building agnostic provider registries
- **LobsterAI** is the most **consumer-UI-focused** — blocking update overlays, settings card redesigns, ad concerns

---

## 6. Community Momentum & Maturity

### Activity Tiers

**Tier 1 — Rapidly Iterating (10+ PRs merged/day, release cadence <2 weeks)**
- **OpenClaw** — 173 merged PRs, beta release today. Momentum: 🟡 (fast but unstable)
- **CoPaw** — 22 merged PRs, fresh v2.0. Momentum: 🟡 (fast but migration pains)
- **IronClaw** — 13 merged PRs, v0.29.x imminent. Momentum: 🟢 (fast, stable, test-driven)

**Tier 2 — Stabilizing & Hardening (5–10 PRs merged/day, security/audit focus)**
- **ZeroClaw** — 12 merged PRs, CI-blocked release. Momentum: 🟢 (heavy but thoughtful)
- **LobsterAI** — 11 merged PRs, release today. Momentum: 🟢 (healthy, polished)
- **NanoBot** — 11 merged PRs, post-audit fixes. Momentum: 🟢 (disciplined)
- **Hermes Agent** — 1 merged PR but 31 issues closed. Momentum: 🟢 (responsive, test-driven)

**Tier 3 — Low Activity (0–5 PRs merged/day)**
- **NanoClaw** — 4 merged PRs. Momentum: 🟢 (steady but small team)
- **Moltis** — 6 merged PRs. Momentum: 🟢 (focused)
- **PicoClaw** — 0 merged PRs, 2 critical bugs open. Momentum: 🔴 (stalled)
- **TinyClaw** — 0 merged PRs. Momentum: 🟡 (low engagement)
- **NullClaw, ZeptoClaw** — Dead. Momentum: ⚪

### Maturity Indicators
- **Best upgrade experience:** Hermes Agent, NanoBot — backward-compatible, no reported crash-loops
- **Worst upgrade experience:** OpenClaw, CoPaw (v2.0) — migration gates causing fatal failures
- **Best community responsiveness:** Hermes Agent (P0s fixed same-day), NanoBot (post-audit within hours)
- **Worst community engagement:** OpenClaw (#75 unanswered for 197 days), PicoClaw (critical bugs with 0 comments)
- **Strongest test infrastructure:** IronClaw (4-lane parallel tier-2, fault-injection), Hermes Agent (waroffchange's test drive)

---

## 7. Trend Signals

### Industry Trends Extracted from Community Feedback

1. **"Shove the agent into production" demand** — Across OpenClaw, ZeroClaw, and NanoClaw, users are deploying agents in customer-facing or business-critical roles. This drives demand for:
   - **Session persistence** (no state loss on crash/upgrade)
   - **Multi-user isolation** (ZeroClaw's principal isolation, IronClaw's OAuth audit)
   - **Observability** (OTel tracing, turn-level correlation)
   - **Backup/export** (Hermes Agent's checkpoint export, IronClaw's dashboard backup)

2. **Local model renaissance, with friction** — The Llama.cpp/ollama ecosystem is growing, but:
   - OpenClaw (#106779), Hermes Agent (#63680), ZeroClaw (#5600) all report **model-specific bugs** (400 errors, tool definition gaps, thinking leak)
   - **Cache efficiency** is a pain point: DeepSeek cache <10% (OpenClaw #94518)
   - **Hardware diversity** is uneven: M5 Max MacBooks (OpenClaw), Raspberry Pi (PicoClaw), Colima/Lima (NanoClaw) all hit specific blockers

3. **Agent-to-agent protocols are the next frontier** — ZeroClaw's A2A discovery RFC (#7218) and CoPaw's multi-agent orchestration (#6136) signal that the ecosystem is moving beyond single-agent assistants toward **agent meshes**. Moltis's ACP agent auto-detection (PR #1149) is a concrete implementation.

4. **"App store" ecosystems are emerging but immature** — CoPaw's experimental PawApp SDK (#6150), Hermes Agent's plugin interface tracking (#64182), and OpenClaw's plugin refactoring (#108440) all point toward **third-party extension marketplaces**. None are production-ready — this is a 2027 opportunity.

5. **Platform inequality is a growing risk** — OpenClaw's #75 (Linux/Windows apps, 113 comments, 81 👍) and CoPaw's #6076 (Windows 7) and #6125 (Kylin OS) show that **ignoring non-macOS platforms creates community resentment**. Only IronClaw and ZeroClaw demonstrate cross-platform parity.

6. **Security is shifting from "nice to have" to "blocker"** — NanoBot's 42-finding audit, Hermes Agent's CVSS 6.5/7.0 delegation context issue (#37935), and ZeroClaw's OIDC auth RFC (#7141) indicate that **enterprise security requirements are migrating upstream into agent tooling**.

7. **The "fail-fast" vs. "fail-safe" debate is unresolved** — OpenClaw's aggressive migration gate (crash on benign conflict) represents a "fail-fast" approach. NanoBot and Hermes Agent's gradual deprecation is "fail-safe." The community is voting with bug reports: **fail-safe is winning** for production deployments.

### Value for AI Agent Developers

| If you're building... | Watch this project | For this insight |
|-----------------------|--------------------|-------------------|
| Production agent services | ZeroClaw, IronClaw | Multi-user auth, channel lifecycle, SSE streaming reliability |
| Desktop agent for developers | Hermes Agent | Fast bug triage, TUI/CLI focus, plugin architecture |
| Cross-platform consumer agent | LobsterAI | UI polish, update flows, model provider management |
| Multi-agent orchestration | CoPaw, Moltis | Agent templates, inter-agent protocols, memory sharing |
| Enterprise deployment | NanoBot, OpenClaw | Security audit patterns, migration strategies, backup/export |

**Key takeaway for technical decision-makers:** The ecosystem is converging on **reliability** as the differentiator. Feature velocity is table stakes — the projects that win production deployments will be those that can upgrade without breaking, handle transient failures gracefully, and provide clear observability into agent behavior. OpenClaw has the most ambitious feature roadmap but the worst stability track record. Hermes Agent and NanoBot demonstrate that you can fix bugs faster than you introduce them — a lesson OpenClaw's v2026.7.x team should study closely.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for 2026-07-16.

---

## NanoBot Project Digest – 2026-07-16

### 1. Today's Overview
NanoBot is in a period of intense **stabilization and hardening** following a comprehensive 42-finding security and correctness audit. Activity surged with 24 issues and 26 PRs updated in the last 24 hours, driven largely by the closure of 21 audit findings (mostly security bugs) by security researcher `hamb1y`. The project maintainers are actively merging fixes across channels, providers, and the core agent loop, while also advancing significant refactoring work to decouple channels and centralize configuration. While no new releases were cut today, the volume of merged PRs suggests a high-quality release may be imminent as the backlog of critical bugs is cleared.

### 2. Releases
**None.** No new releases were published today. The project appears to be consolidating bug fixes before a major release.

### 3. Project Progress
Today saw **11 PRs merged or closed**, reflecting a strong focus on fixing post-audit issues and other regressions:
- **Agent Stability:** `fix(agent): reprompt on hard context overflow` (#4925) and `fix(agent): scope project instructions and trim default prompt` (#4945) were both opened, with #4945 targeting scope trimming and performance.
- **Gateway Shutdown:** `fix(gateway): stop channels before draining tasks` (#4944) was closed, fixing a regression where the DingTalk Stream SDK could hang during shutdown.
- **Provider Fixes:** `fix(providers): honor Codex proxy config consistently` (#4943) was closed, and `fix: add Qwen thinking models to control reasoning content exposure` (#4946) addresses the Qwen thinking leak bug (#4934).
- **Refactoring:** `fix(webui): correct activity timer duration` (#4649) was closed, and `fix: include Feishu SDK in dev dependencies` (#4926) was merged to fix local development setup.
- **Feature (Triggers):** `feat(triggers): let agents manage session-local triggers` (#4942) was opened, introducing a new agent tool for session-scoped automation.
- **Security Bug Fixes:** Nine out of the 21 closed issues were direct fixes for the `hamb1y` audit findings, including fixes for `.strip()` crashes on multimodal messages (#4813), token budget spurious values, and session metadata fallbacks.

### 4. Community Hot Topics
The most active discussion centers on three critical issues/PRs:
- **#4924: Heartbeat failure with `unifiedSession` [OPEN]**
    - *Comments:* 4 | *Link:* [HKUDS/nanobot Issue #4924](https://github.com/HKUDS/nanobot/issues/4924)
    - *Analysis:* A user reports a functional bug where the heartbeat system breaks when a "unified" session is active but no other sessions exist. This indicates a missing edge-case in the unified session routing logic. A fix PR (#4928) was quickly opened to address this directly.
- **#4934: Qwen thinking content leak [OPEN]**
    - *Comments:* 1 | *Link:* [HKUDS/nanobot Issue #4934](https://github.com/HKUDS/nanobot/issues/4934)
    - *Analysis:* A common user-facing issue where reasoning tokens from Qwen models are returned as visible chat content instead of being stripped. This degrades UX significantly. A fix PR (#4946) was opened on the same day, showing high responsiveness.
- **#4779 Series: Security Findings [CLOSED]**
    - *Comments:* 2-4 each (multiple items) | *Link:* [HKUDS/nanobot Issue #4779](https://github.com/HKUDS/nanobot/issues/4779) (and related #4778, #4777, #4776)
    - *Analysis:* These 4 issues detail severe authorization bypasses (`process_direct`, system channel, `/stop`, `/restart`). The underlying need is for a robust, centralized authorization layer. The community (via `hamb1y`) is demanding security-by-design.

### 5. Bugs & Stability
Several bugs were reported or addressed today, ranked by severity:

- **HIGH:** `cli/commands.py:_pick_heartbeat_target_from_sessions` fails with `unifiedSession: true` (#4924). **Fix PR exists:** #4928.
- **HIGH:** Qwen models expose thinking/reasoning content (#4934). **Fix PR exists:** #4946.
- **HIGH:** `read_session_metadata()` lacks legacy filename fallback, causing WebUI `workspace_scope` loss (#4940). **Fix PR exists:** #4941.
- **MEDIUM:** Gateway shutdown regression with DingTalk stream SDK (#4944). **Fix PR exists:** #4944 (already closed).
- **LOW:** Feishu SDK missing from dev dependencies (#4926). **Fix PR exists:** #4926 (already closed).

The project is very actively firing fixes for these issues as they appear.

### 6. Feature Requests & Roadmap Signals
Today's activity signals a clear roadmap:
- **Deployment Improvements:** The new PR `feat: add one-click Deploy to Render support` (#4937) suggests a push towards easier, cloud-native hosting. This is likely for the next minor release.
- **Agent Autonomy (Triggers):** The new PR `feat(triggers): let agents manage session-local triggers` (#4942) signals a move toward persistent, agent-managed workflows (e.g., "remind me in 5 minutes"). This deepens the agent’s ability to run autonomously.
- **Channel Decoupling:** The ongoing refactors (e.g., #4908, #4918) point toward a "pluggable" channel architecture, making it easier for the community to build and maintain new channel integrations without forking core logic.

### 7. User Feedback Summary
Real user pain points are driving the current release cycle:
- **Security Concern:** The 42-finding audit reveals deep concern from the community (specifically power users like `hamb1y`) about authorization boundaries, session isolation, and the risk of DoS via `/restart`.
- **Multimodal Support:** The bug report about `.strip()` crashing on list-form content (#4800) highlights that users are actively sending multimodal messages (images, files), and the code is not handling them gracefully.
- **Model Compatibility:** The Qwen thinking leak (#4934) and the need for custom Bot API base URLs (#4919) show that users are deploying on non-standard infrastructure (self-hosted LLMs, custom Telegram proxies) and expect flexible tooling.
- **Session Persistence:** The metadata loss after restart (#4940) is a critical UX regression for users relying on the WebUI, highlighting the fragility of the file-naming convention.

### 8. Backlog Watch
No long-abandoned critical issues or PRs are currently languishing. The project maintainers have been highly responsive, even closing audit findings from over a month ago (e.g., #4082 from May 29). The following longer-running PRs are still open and require attention:
- **PR #4621:** `feat(memory): gate archive facts with provenance context` — A substantial memory architecture improvement from July 1. It is still open with no merge conflicts flagged, but has not been prioritized over bug fixes.
- **PR #4620:** `add heartbeat trigger command` — Also from July 1, this PR is a significant feature addition. It remains open, likely awaiting feedback from reviewers.
- **PR #4822:** `fix(webui): preserve automation source on streamed replies` — From July 7, this PR has a conflict flag, indicating it needs rebase or resolution before it can be merged.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-16

## 1. Today's Overview

Hermes Agent shows **high activity** with 50 issues and 50 PRs updated in the last 24 hours, though the vast majority (31 issues closed, 1 PR merged/closed) represent a **cleanup wave** rather than new feature work. The project closed **two P0 bugs** today (async session DB drops, system prompt persistence nullification)—both serious regressions that were actively harming users. Activity is dominated by a **sustained test-coverage drive** (7+ open test-only PRs from contributor `waroffchange`) and a **heavy backlog of open PRs** (49 open vs. 1 merged). No new releases were cut, suggesting the team is consolidating fixes before a version bump. The 19 open issues include several long-standing feature tracks (plugin interface, provider inventory) with no signs of near-term closure.

## 2. Releases

**No new releases in the last 24 hours.** The latest release remains v0.18.2.

## 3. Project Progress

Only **one PR merged/closed** in the last 24 hours:
- **[#53695] fix(desktop): refresh sidebar sessions on profile switch** — [PR link](https://github.com/NousResearch/hermes-agent/pull/53695). A desktop UI fix ensuring the sidebar session list refreshes when switching profiles.

**Key fixes that advanced** (closed issues, presumed merged or implemented on main):
- [#63712] **AsyncSessionDB methods silently dropped when called without await (P0)** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/63712). Lost writes and `RuntimeWarning` from missing `await` on `AsyncSessionDB.__getattr__`. **Fixed on main**.
- [#63713] **Session system_prompt persists as null after a turn (P0)** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/63713). Every turn rebuilt system prompt from scratch, permanently missing prefix cache. **Fixed on main**.
- [#63911] **Telegram DM topic mode: root-lobby gate swallows kanban wake events (P3)** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/63911). Early return when `thread_id` is empty/1 blocked message processing.
- [#63396] **Kanban goal_mode workers never enter the goal loop (P3)** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/63396). Dispatcher spawned `chat -q` (single-query) instead of goal-loop capable path.
- [#63506] **opencode-go: Qwen models fallback due to api_mode mismatch (P2)** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/63506). Called `/chat/completions` instead of `/messages`.
- [#63698] **Console windows flash despite windows_hide_console: true (P2)** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/63698). Windows terminal popups not suppressed.

## 4. Community Hot Topics

Most active discussion items:

1. **#64182 [OPEN] Tracking: Plugin Interface Expansion** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/64182)  
   *12 comments* — Root tracking issue for community-sourced plugin interface ideas from Discord. This is a major ongoing effort with many contributors having long-queued PRs. Indicates the project is formally organizing plugin ecosystem growth.

2. **#63911 [CLOSED] Telegram DM topic mode: root-lobby gate swallows messages** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/63911)  
   *5 comments* — Detailed bug with repro steps, involved gateway code, resolved after discussion.

3. **#23359 [OPEN] Provider/model inventory has no scriptable surface** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/23359)  
   *4 comments* — Tracks that five PRs reinvent the same functionality. Points to a **missing API abstraction** that is wasting contributor effort.

4. **#3326 [OPEN] feat(cli): add --output-format json flag** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/3326)  
   *5 👍, 2 comments* — Popular feature request from March 2026 still open. Strong user demand for programmatic/scriptable CLI output.

5. **#37935 [OPEN] fix(delegate-task): preserve approval context** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/37935)  
   *1 comment, security-rated CVSS 6.5/7.0* — Security issue with delegating tasks losing approval context. Community member provided thorough CVSS assessment.

**Underlying needs:** Users are demanding **scriptability** (JSON output, API surfaces), **plugin ecosystem expansion**, and **better Telegram/Discord integration**. The 4-comment issue #23359 is particularly telling—it indicates infrastructure gaps causing duplicated effort.

## 5. Bugs & Stability

**Critical (P0) — Fixed today:**
- [#63712] **AsyncSessionDB methods silently dropped without await** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/63712). Coroutine returned instead of awaited → lost database writes, `RuntimeWarning`. Fix on main.
- [#63713] **Session system_prompt persists as null → prefix cache misses permanently** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/63713). Every turn rebuilt prompt from scratch, negating cache benefits. Fix on main.

**High (P2) — Open:**
- [#65272] Per-message timestamps missing in TUI/Desktop — [Issue link](https://github.com/NousResearch/hermes-agent/issues/65272). No time data in message pipeline anywhere.
- [#46778] **Desktop pool backends orphaned on idle reap (PPID=1 dashboard leak)** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/46778). Electron desktop leaks Python dashboard processes per profile per idle-reap cycle; processes run indefinitely.
- [#64789] **Desktop prompt.submit can target stale runtime A when route points to B** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/64789). Race condition where three session identity pointers diverge. Existing drift guard (#54527) is insufficient.

**Medium (P2) — New today:**
- [#65034] **Dashboard Full Backup fails silently in v0.18.2** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/65034). CLI argument syntax mismatch causes backup to run indefinitely without producing output.

**New bug-fix PRs today:**
- [#65288] fix(gateway): stop truncate_message hanging on pathologically small max_length — [PR link](https://github.com/NousResearch/hermes-agent/pull/65288)
- [#65295] fix(kanban): reject event streams for removed boards — [PR link](https://github.com/NousResearch/hermes-agent/pull/65295)
- [#65294] fix(gemini): emit thoughtSignature sentinel for cross-provider/MoA tool calls — [PR link](https://github.com/NousResearch/hermes-agent/pull/65294)

## 6. Feature Requests & Roadmap Signals

**High-demand features** (from open issues and PRs):

- **Structured CLI output** (#3326, 5 👍) — `--output-format json` for CI pipelines. **Likely for next release** given the 5-thumbs-up and scriptability push.
- **Per-run metadata propagation to MCP tools** (#64890) — Allows MCP servers to correlate calls with specific user/run. Important for multi-tenant setups.
- **Checkpoint export/import** (#63748) — Cross-session context bridging, currently sessions cannot transfer tool outputs. Filed and closed as implemented, likely shipping.
- **Plugin Interface Expansion** (#64182) — Major community-driven effort, likely spans multiple releases.
- **Per-message timestamps** (#65272) — Simple UI enhancement with high community visibility.

**Prediction for v0.19.0:** JSON CLI output, MCP metadata propagation, and the Desktop session drift fix are the strongest candidates. The plugin interface expansion will likely remain as a tracking issue for multiple future releases.

## 7. User Feedback Summary

**Positive signals:**
- Active community proposing **themed plugin ideas** (#64182, Islamic features example in #63923)
- Contributor `waroffchange` is systematically adding test coverage (7+ PRs for pure helpers), indicating the codebase is stable enough for test-focused contributions.

**Pain points:**
- **Windows users** report persistent issues: `hermes update` broken by venv shim detection (#60239), console windows flashing despite config (#63698), GUI force-restart losing sessions (#63599).
- **Telegram integration** is fragile: 409 Conflict loops (#63724), root-lobby message swallowing (#63911), polling conflicts on macOS (#63387).
- **Desktop reliability** is weak: sessions disappearing after restart (#63516, #63599), orphaned processes (#46778), stale session pointers (#64789).
- **Custom provider/Ollama** tool definitions not transmitted (#63680) — blocks users trying local models.

**Satisfaction:** The rapid closure of P0 bugs today (both fixed on main) suggests the team is responsive to critical issues. However, the 49 open PRs vs. 1 merged indicates a **merging bottleneck** that may frustrate contributors.

## 8. Backlog Watch

**Long-unanswered high-importance items needing maintainer attention:**

- **#23359 [OPEN] Provider/model inventory has no scriptable surface** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/23359)  
  Created 2026-05-10 (68 days). 5 PRs reinvent the same wheel. **No maintainer response.** This is blocking progress and wasting contributor effort.

- **#3326 [OPEN] feat(cli): add --output-format json flag** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/3326)  
  Created 2026-03-27 (111 days). 5 👍, no assignee. Community demand is clear but unaddressed.

- **#37935 [OPEN] fix(delegate-task): preserve approval context** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/37935)  
  Created 2026-06-03 (43 days). Security issue (CVSS 6.5/7.0) with thorough community analysis. **No maintainer response** despite severity.

- **#46778 [OPEN] Desktop pool backends orphaned on idle reap (PPID=1 dashboard leak)** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/46778)  
  Created 2026-06-15 (31 days). Memory/resource leak impacting desktop users. No fix PR linked.

- **#65272 [OPEN] Per-message timestamps in TUI/Desktop** — [Issue link](https://github.com/NousResearch/hermes-agent/issues/65272)  
  Created today. Time-sensitive — this is a basic UX gap.

**Key concern:** Multiple open issues with security implications (#37935, #63650's blast-moderate risk) and community-blocking infrastructure gaps (#23359) lack maintainer engagement, which could erode contributor trust.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for **2026-07-16**.

---

## PicoClaw Project Digest: 2026-07-16

**Project:** github.com/sipeed/picoclaw
**Version tracked:** Latest commits (v0.3.1)

### 1. Today's Overview

Activity on the PicoClaw repository today was moderate, driven entirely by community-submitted bug reports and a lone documentation PR. While no new releases were cut, three stale issues from late June were closed automatically, suggesting maintainers may be cleaning the backlog. A significant spike in bug reports (two critical bugs filed on July 15) regarding Linux/ARM support and the tool hook system indicates recent `v0.3.1` changes may have introduced regressions. The single open PR is a minor text update, not a code fix, meaning the new bugs do not yet have dedicated resolution branches.

### 2. Releases

No new releases were published today.

### 3. Project Progress

- **Merged/Closed PRs:** 0 pull requests were merged or closed today.
- **Notable Open PRs:**
    - **#3222** (refactor: deltachat): This PR is still open after 13 days with no maintainer merge. It represents a solid code cleanup (-200 LOC) for the Delta Chat integration, including removing legacy features and hardcoded secrets.
    - **#3259** (Update PicoClaw description for parallelization): A minor documentation update that has received no comments or reactions since its filing.

### 4. Community Hot Topics

- **#3153 - [CLOSED] [BUG] Volcengine Doubao Seed tool calls leak as text** (4 comments)  
  *URL:* [Issue #3153](https://github.com/sipeed/picoclaw/issues/3153)  
  This was the most discussed issue in the dataset. A user reported that tool calls from the `doubao-seed-2.0-pro` model occasionally fail to execute, returning raw XML tags like `<seed:tool_call>` to the user instead. This is a reliability bug for users on the Volcengine provider. Labeled `[stale]` and closed, it is unclear if a fix has been merged or if the issue simply aged out due to inactivity.

- **#3196 / #3197 - [CLOSED] [BUG] Codex and Antygravity OAuth login not working** (2 comments each)  
  *URL:* [#3196](https://github.com/sipeed/picoclaw/issues/3196) | [#3197](https://github.com/sipeed/picoclaw/issues/3197)  
  Both filed by the same user regarding `v0.2.9`, these duplicates suggest a fundamental authentication failure for two specific providers (Codex, Antygravity). Now closed as stale, this signals a potential permanent support gap for those integrations.

### 5. Bugs & Stability

| Severity | Issue | Summary | Status |
| :--- | :--- | :--- | :--- |
| **Critical** | **#3260** | *Launcher missing for ARM64 (ARM) release*: A user on a Raspberry Pi 3B (Raspbian) cannot launch PicoClaw after downloading the official ARM64 build from picoclaw.io. The launcher binary appears to be missing or broken. | OPEN (0 comments, no fix PR) |
| **Critical** | **#3258** | *Process Hook `before_tool` modify not working*: The `decision` field in custom tool hooks is discarded, and arguments are misparsed due to a deserialization defect. This breaks the core promise of customizable tool behavior. | OPEN (0 comments, no fix PR) |
| **Low** | **#3153/3196/3197** | Various stale tool-call leaks and OAuth failures on older versions (v0.2.8/v0.2.9). | CLOSED / Stale |

**Analysis:** The two new critical bugs are concerning. The ARM64 launcher issue (#3260) blocks an entire hardware segment (Raspberry Pi). The `before_tool` hook deserialization bug (#3258) is a deep code defect that will require a careful JSON parsing fix. Neither has a corresponding Pull Request yet.

### 6. Feature Requests & Roadmap Signals

- **#3257 - [OPEN] Add stateless/no-history mode for gateway sessions**  
  *URL:* [Issue #3257](https://github.com/sipeed/picoclaw/issues/3257)  
  *User Request:* The user wants to use PicoClaw in `gateway` mode without persistent conversation history. Currently, in CLI mode they can use `--session` to create fresh conversations, but in gateway mode the session is static.  
  *Prediction:* This is a low-code, high-impact quality-of-life improvement. Given the user's clear API use-case, this is likely to land in the next minor release (0.3.2 or 0.4.0) as a `--stateless` flag.

### 7. User Feedback Summary

- **Pain Points:**
    - *Cross-platform fragmentation:* ARM64 Linux users are currently locked out of the latest release.
    - *Plugin fragility:* Hook/deserialization bugs are eroding trust in the extensibility layer.
    - *Provider inconsistency:* The closed issues suggest support for niche providers (Codex, Antygravity, Volcengine) is unstable or lacks regression testing.
- **Use Cases:** Users are clearly trying to run PicoClaw on low-power devices (Raspberry Pi) and integrate it into automated pipelines (gateway mode). The `before_tool` hook user is a power user attempting to rewrite tool calls via a Python script.

### 8. Backlog Watch

- **PR #3222 - refactor(deltachat): cleanup implementation, documentation**  
  *URL:* [PR #3222](https://github.com/sipeed/picoclaw/pull/3222)  
  **Status:** Open since 2026-07-03 (13 days).  
  **Action needed:** This is a healthy, -200 LOC cleanup of the Delta Chat integration. It removes legacy code and hardcoded secrets. The fact it has been ignored for nearly two weeks suggests either the maintainers are busy or the PR requires a review cycle. If unaddressed for another week, it may go stale and cause merge conflicts.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-16

## Today's Overview
NanoClaw saw **moderate-to-high activity** over the past 24 hours, with **11 PRs** updated (4 merged/closed, 7 open) and **2 issues** (1 open, 1 closed). No new releases were published. The project is in a **healthy development phase**, with contributions from both core-team members and external contributors. Key themes include **delivery reliability fixes**, **new agent provider integrations**, **memory system enhancements**, and **container runtime improvements**. The open issue count is relatively low, suggesting the maintainers are keeping up with bug reports, though one critical delivery-retry bug remains open with an accompanying fix PR.

## Releases
**None.** No new releases were published today.

## Project Progress
**Merged/Closed PRs (4 total):**
- **[PR #3056]** [closed] feat(opencode): add OpenCode as an agent provider — Adds OpenCode as a new provider, spawning an `opencode serve` subprocess with shared server lifecycle management per container. **External contributor: dtanikella**
- **[PR #3055]** [closed] feat: add deploy.sh for one-command redeploys — Provides a script for SSH-based redeploy with `git pull`, `pnpm install`, `pnpm build`, and service restart. **External contributor: dtanikella**
- **[PR #3013]** [closed, core-team] feat(codex): load shared memory on session start — Codex counterpart for provider-agnostic memory, using `SessionStart` command hook for startup/clear/compact. **Author: amit-shafnir**
- **[PR #3012]** [closed, core-team] feat(memory): add provider-agnostic persistent memory — Scaffolds a shared memory tree (`memory/index.md`, `memory/system/definition.md`) for every agent group, loaded at startup/clear/compact (excluding resume). **Author: amit-shafnir**

**Key features advanced today:**
- Provider-agnostic persistent memory system (core milestone)
- OpenCode provider integration (new provider option)
- Deployment automation tooling (deploy.sh)

## Community Hot Topics
- **[Issue #3058]** *Transient outbound-send failures permanently dropped after 3 fast retries* — **1 comment**, recently updated. The most technically significant open issue. Highlights a design flaw where transient network failures (429, 5xx, timeouts) are treated identically to permanent validation errors. This could cause silent message loss in production. [View issue](https://github.com/nanocoai/nanoclaw/issues/3058)
- **[Issue #3054]** *agent_message_policies rows can outlive their group/connection* — **0 comments** (closed). A database integrity issue where FK constraints block group deletion due to orphaned policy rows. Closed, likely with the lifecycle contract fix. [View issue](https://github.com/nanocoai/nanoclaw/issues/3054)
- **[PR #3059]** *fix(delivery): don't permanently drop transient send failures* — Fix PR for issue #3058, distinguishing transient from permanent failures. **0 comments** but directly addresses the most active open bug. [View PR](https://github.com/nanocoai/nanoclaw/pull/3059)

**Underlying needs:** Users are encountering silent message loss in distributed deployments where network blips are common. The community needs clear failure mode differentiation (transient vs permanent) to maintain delivery guarantees without requiring manual message recovery.

## Bugs & Stability

### High Severity
- **[Issue #3058]** *Transient outbound-send failures permanently dropped after 3 fast retries* (OPEN) — **Fix PR #3059 exists.** The `delivery.ts` module retries on ~1s polls and after 3 attempts calls `markDeliveryFailed()` permanently regardless of failure type. This means a brief 3-second network blip can permanently lose an agent's reply. The fix distinguishes transient (429/5xx/timeout – will requeue) from permanent (validation – mark failed). **Need:** Merge and release urgently for production environments.

### Medium Severity
- **[Issue #3054]** *agent_message_policies rows outlive group/connection* (CLOSED) — FK constraints prevented group deletion when policy rows existed. Resolved via the unified approval lifecycle contract fix (PR #3040).
- **[PR #3040]** [open] fix: unify approval holds behind one lifecycle contract — Addresses the underlying architectural issue that caused policy cleanup problems. In-progress core-team fix.

### Low Severity
- **[PR #3053]** [open] fix(agent-runner): stand down cleanly when idle — Containers linger until 30-min kill timeout because `processQuery` keeps SDK stream open. Fix adds idle-timeout cleanup. Performance/efficiency improvement rather than data loss.
- **[PR #3052]** [open] fix(container-runtime): resolve host gateway under Colima/Lima/Rancher Desktop — macOS VM-based runtimes missing `host.gateway` mapping that Docker Desktop provides automatically. Affects developers using alternative container runtimes.

## Feature Requests & Roadmap Signals
Based on today's PRs and issues, the following features are progressing toward next release:

1. **Provider-Agnostic Persistent Memory** — Both Codex and memory scaffolding PRs merged today. Likely to be a headline feature in the next release (v0.x.0). Enables cross-provider conversation memory sharing.

2. **Automatic Claude↔Codex Quota Fallback** — [PR #3057] adds per-agent-group automatic failover when Claude hits quota mid-turn, plus Telegram/WhatsApp channel adapters. Currently open; suggests multi-provider resilience is a priority.

3. **OpenCode Provider** — [PR #3056] merged today. New agent provider option for users who prefer or require OpenCode.

4. **Deployment Automation** — [PR #3055] merged. One-command redeploy script signals growing production use cases.

**Prediction for next version:** Memory system + quota fallback + delivery reliability fix. These three features address core operational pain points (message loss, provider availability, context continuity).

## User Feedback Summary
- **Pain point:** Silent message loss from transient network failures (Issue #3058). Users relying on NanoClaw for critical agent communications cannot tolerate permanent drops from brief blips. The fix PR suggests the community values delivery guarantees.
- **Pain point:** Container resource waste from idle sessions lingering for 30 minutes (PR #3053). Affects cost and cluster utilization for users running many agent sessions.
- **Pain point:** Inconsistent local development setup across container runtimes (PR #3052). macOS users with Colima/Lima/Rancher Desktop face connectivity issues that Docker Desktop users don't.
- **Satisfaction signal:** Active community with 4 merged PRs today from both core-team and external contributors. Low issue-to-PR ratio suggests responsive maintainers.

## Backlog Watch
- **[PR #2591]** *fix: namespace user IDs by channel-type prefix, not bare colon* — **Open since 2026-05-22 (55 days).** By external contributor mmahmed. Updated as recently as yesterday (2026-07-15) but no maintainer activity in over 7 weeks. This PR addresses channel ID collision risks; may need core-team review to avoid bitrot. [View PR](https://github.com/nanocoai/nanoclaw/pull/2591)
- **[PR #3051]** *fix(groups): preflight provider config before save* — **Open for 1 day** but by external contributor OtherVibes. Prevents invalid provider configurations from being saved. No comments yet; needs maintainer review to validate approach. [View PR](https://github.com/nanocoai/nanoclaw/pull/3051)

**Verdict:** The project shows strong momentum with active merging of major features (memory, providers, deployment). The oldest pending PR (#2591) at 55 days is a concern for community contributor retention—maintainers should prioritize its review. The bug #3058 with accompanying fix PR #3059 is the most pressing item to address for production reliability.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-16

## Today's Overview

The IronClaw project remains in high-velocity development, with 38 PRs and 23 issues updated in the last 24 hours — indicating intense focus on both bug fixing and architectural work. The team is actively addressing a cluster of Slack integration regressions that have persisted across multiple QA bug-bash waves, while simultaneously executing a major "Reborn" runtime refactor that includes retiring the v1 codebase. Release activity is paused (no new releases), and the project continues to invest heavily in tier-2 integration testing and fault-injection coverage to prevent regressions.

## Releases

**No new releases** in the last 24 hours. The last release channel activity remains at PR #5598 (chore: release) which proposes bumping `ironclaw` to v0.29.1 with breaking changes in `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0), but this PR has not been merged.

## Project Progress

### Merged/Closed PRs Today (13 total)
- [#6135](https://github.com/nearai/ironclaw/pull/6135) **[size: XL]** — fix(reborn): recover Slack host after OAuth activation — *Merged*
- [#6128](https://github.com/nearai/ironclaw/pull/6128) **[size: XL]** — fix(auth): audit + review blockers — scope ceiling, Notion refresh, fan-out retryability, removal/callback race — *Merged*
- [#6084](https://github.com/nearai/ironclaw/pull/6084) **[size: M]** — feat(webui): replace native confirmations with a shared modal — *Merged*
- [#6082](https://github.com/nearai/ironclaw/pull/6082) **[size: S]** — fix(webui-v2): render extension registry without enrichment delay — *Merged*
- [#6055](https://github.com/nearai/ironclaw/pull/6055) **[size: M]** — test(reborn): StaleSurface same-run refresh pin + extension-remove channel-cleanup integration coverage — *Merged*

### Key Advancements
- **OAuth lifecycle hygiene**: PR #6128 landed critical fixes for auth flow race conditions, including shared-vendor state isolation, Notion refresh token handling, and removal/callback race fixes — part of the "unified generic extension runtime" initiative.
- **Slack recovery**: PR #6135 fixed post-OAuth activation Slack host recovery, addressing what has been the project's #1 user-facing bug family.
- **UX polish**: The team replaced native `confirm()` dialogs with a shared Reborn modal system (PR #6084) and fixed the extension registry loading delay (PR #6082).

## Community Hot Topics

### Most Active Issues

1. [#6105](https://github.com/nearai/ironclaw/issues/6105) **[OPEN, Enhancement]** — "Extension/channel lifecycle state-machine test (install→connect→disconnect→reconnect→uninstall)" with 3 comments. *This is the project's most strategic issue this week — it directly addresses the persistent Slack regression problem. The author (ilblackdragon) has linked fixes from PRs #5851, #5898, #5953, #5957, #6054.*
   
2. [#3533](https://github.com/nearai/ironclaw/issues/3533) **[CLOSED]** — "Telegram in v 0.28.1 does not automatically setup from UI." *Though closed, this older P1 bug shows the long tail of channel setup issues.*

3. [#5834](https://github.com/nearai/ironclaw/issues/5834) **[OPEN, bug_bash_P2]** — "Slack disconnect request is incorrectly rejected by agent." *3 comments, still open — users cannot disconnect Slack through the agent.*

### Most Active PRs

1. [#6116](https://github.com/nearai/ironclaw/pull/6116) **[size: XL, OPEN]** — "Unified generic extension runtime + Option A honest state machine (reconcile main)" — *Massive reconciliation of 92 commits into the new architecture. This is the central architectural effort.*

2. [#6140](https://github.com/nearai/ironclaw/pull/6140) **[OPEN]** — "github.get_job_logs + SSRF-safe redirect egress + triage-CI QA scenario" — *New capability for GitHub CI triage, demonstrating continued platform expansion.*

3. [#5910](https://github.com/nearai/ironclaw/pull/5910) **[OPEN]** — "fix: hydrate approval gates on notification open" — *Long-running PR from ironloopai[bot] addressing approval gate delivery.*

### Underlying Needs
The community (and QA team) is most vocal about **Slack reliability** — disconnect/reconnect flows, DM delivery, and authentication state management. There is clear demand for **channel lifecycle stability** before new features can be safely shipped.

## Bugs & Stability

### Critical/P1 Bugs (OPEN)
| Issue | Description | Fix PR Exists? |
|-------|-------------|----------------|
| [#5877](https://github.com/nearai/ironclaw/issues/5877) | Slack notification delivered to wrong user | No |
| [#5943](https://github.com/nearai/ironclaw/issues/5943) | Slack DM action posts to current channel instead of DMs | No |
| [#5882](https://github.com/nearai/ironclaw/issues/5882) | Repeated Slack reconnect leaves auth flow broken | PR #6135 (merged) |
| [#6125](https://github.com/nearai/ironclaw/issues/6125) | User message rejected with "busy" error while routine runs | No |
| [#6126](https://github.com/nearai/ironclaw/issues/6126) | First message in new chat has no loading/streaming state | No |

### P2 Bugs (OPEN)
| Issue | Description |
|-------|-------------|
| [#5834](https://github.com/nearai/ironclaw/issues/5834) | Slack disconnect request incorrectly rejected by agent |
| [#5944](https://github.com/nearai/ironclaw/issues/5944) | Slack DM delivery silently fails but run reports success |
| [#6127](https://github.com/nearai/ironclaw/issues/6127) | Running routine displays "Previous run still in progress" on first execution |

### P3 Bugs (OPEN)
| Issue | Description |
|-------|-------------|
| [#6127](https://github.com/nearai/ironclaw/issues/6127) | Status display error for first routine execution |
| [#6126](https://github.com/nearai/ironclaw/issues/6126) | Missing loading state on first chat message |

### New Bugs Today (2026-07-16)
- [#6138](https://github.com/nearai/ironclaw/issues/6138) — Tier-2 harness can't express compound denied-gate + HTTP-egress-error scenario (found during fault-injection work)
- [#6137](https://github.com/nearai/ironclaw/issues/6137) — Mixed-batch gate resume never redispatches non-first gated call
- [#6136](https://github.com/nearai/ironclaw/issues/6136) — WebChatV2Event accepted/cancelled/failed variants are dead code

### Closed Bugs Today
- [#6052](https://github.com/nearai/ironclaw/issues/6052) — Extensions Registry slow loading (P3, fixed in PR #6082)
- [#6087](https://github.com/nearai/ironclaw/issues/6087) — Extension catalog load failures shown as empty state
- [#6044](https://github.com/nearai/ironclaw/issues/6044) — Enter key sometimes does not submit message (P2)
- [#5886](https://github.com/nearai/ironclaw/issues/5886) — Pending approval blocks subsequent automation runs (P2)
- [#5741](https://github.com/nearai/ironclaw/issues/5741) — builtin.http.save can fail with OutputTooLarge

## Feature Requests & Roadmap Signals

### User-Requested Features (via Issues)
1. **[#6118](https://github.com/nearai/ironclaw/issues/6118)** — Add per-user secrets management to Admin UI (OPEN, filed today)
2. **[#6117](https://github.com/nearai/ironclaw/issues/6117)** — Workspace UI should display localized region names and human-readable file sizes (OPEN, filed today)
3. **[#6105](https://github.com/nearai/ironclaw/issues/6105)** — Channel lifecycle state-machine test automation (Enhancement, in progress)

### Predictions for Next Version
Based on current activity, the next release (likely v0.29.x) will include:
- **Slack lifecycle stability** — post-OAuth recovery fix (PR #6135) and state-machine tests (PR #6113)
- **Reborn v1 retirement** — PR #6123 removes the legacy v1 runtime, suggesting a clean architecture split
- **Shared modal system** — Replacing native browser dialogs (already merged in PR #6084)
- **Github CI integration** — PR #6140 adds `github.get_job_logs` capability
- **OAuth flow fixes** — PKCE verifiers, supersede-on-start, expiry projections (PR #6130)

## User Feedback Summary

### Pain Points (High Confidence)
1. **Slack integration is the #1 pain point** — Users cannot reliably disconnect Slack (#5834), DMs are delivered to wrong channels (#5943) or fail silently (#5944), and reconnect attempts leave auth in broken state (#5882). QA reports this bug family regressed across **all four** recent bug-bash waves.
2. **Background routines lock users out** — Users are blocked from sending messages when routines run (#6125), creating a poor multitasking experience.
3. **Missing UI feedback** — New chat sessions show blank screens with no loading state (#6126), and extension catalog failures show empty lists indistinguishable from empty catalogs (closed #6087).

### Satisfaction Signals
- Quality of regression test infrastructure is improving (4-lane parallel tier-2 extension plan, fault-injection scenarios in PR #6134)
- Prompt bug fix turnaround for UX issues (Extension Registry loading time fixed within 2 days)

## Backlog Watch

### Stale Important Issues
| Issue | Age | Last Update | Status |
|-------|-----|-------------|--------|
| [#3533](https://github.com/nearai/ironclaw/issues/3533) — Telegram auto-setup from UI (P1) | 65 days | 2026-07-15 (closed) | Resolved |
| [#5598](https://github.com/nearai/ironclaw/pull/5598) — Release PR (chore: release) | 13 days | 2026-07-15 | Open, no merge in sight |

### PRs Needing Attention
- [#5910](https://github.com/nearai/ironclaw/pull/5910) — "fix: hydrate approval gates on notification open" — Open for 6 days, from `ironloopai[bot]`, marking this as a lower-priority automation-driven fix.
- [#6116](https://github.com/nearai/ironclaw/pull/6116) — The 92-commit unified extension runtime reconciliation is the largest open PR and has been parked in favor of smaller targeted fixes (PR #6128, #6130). This architectural work remains the most significant long-term risk/opportunity.

### Maintainer Attention Items
- **SSE wire-contract coverage**: PR #6133 adds round-trip tests for WebChatV2Event variants, but issue #6136 reveals three variants (`accepted`, `cancelled`, `failed`) are dead code — no production constructor exists. This implies either unused code that should be removed, or a gap between schema design and actual use.
- **Mixed-batch gate resume bug** (#6137): Critical for compound tool-call workflows — the non-first gated call is never redispatched after gate resolution.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-16

## 1. Today's Overview
LobsterAI saw a burst of activity, with 17 pull requests updated in 24 hours (11 merged or closed) and a new release (v2026.7.15) going out. The six issues updated were all closed stale items except one new open bug (#2342), indicating maintainers are making headway cleaning the backlog. Six open PRs remain, led by long-standing dependency bumps and a stale cowork fix. Overall, the project is in a healthy integration phase with a focused release cycle and active triage.

## 2. Releases
**New Version: [LobsterAI 2026.7.15](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.7.15)**  
*No breaking changes or migration notes announced.*

**What's Changed:**
- `feat: optimize file card` — improved file attachment display
- `feat(build): add opt-in Windows web installer target` — new Windows distribution option
- `feat(cowork): revamp homepage quick-action scenario` — redesigned Cowork homepage shortcuts

## 3. Project Progress
Eleven PRs were merged or closed today, reflecting a strong push across UI/UX, settings, and Cowork features:

- **[#2341](https://github.com/netease-youdao/LobsterAI/pull/2341) — Release/2026.7.13** — cut release branch (merged)
- **[#2340](https://github.com/netease-youdao/LobsterAI/pull/2340) — Revert "fix: fixed model not allowed"** — rollback of model restriction fix (merged)
- **[#2339](https://github.com/netease-youdao/LobsterAI/pull/2339) — fix(update): align update card header content** — improved responsive layout for narrow sidebars (merged)
- **[#2338](https://github.com/netease-youdao/LobsterAI/pull/2338) — feat(update): refine the blocking update overlay** — centered progress, scrollable release notes, error recovery (merged)
- **[#2337](https://github.com/netease-youdao/LobsterAI/pull/2337) — fix: fixed model not allowed** — model restriction fix (merged, then reverted)
- **[#2336](https://github.com/netease-youdao/LobsterAI/pull/2336) — feat(settings): group General settings into labeled cards** — reorganized settings into Basics/Notifications/Data & Privacy sections (merged)
- **[#2335](https://github.com/netease-youdao/LobsterAI/pull/2335) — fix: fixed content copy bug** — copy functionality fix (merged)
- **[#2334](https://github.com/netease-youdao/LobsterAI/pull/2334) — fix(cowork): restore IM session loading state** — prevented cron/desktop events from affecting loading state (merged)
- **[#2333](https://github.com/netease-youdao/LobsterAI/pull/2333) — feat(update): block app interactions during user-initiated updates** — lightweight overlay for downloads and installs (merged)
- **[#2332](https://github.com/netease-youdao/LobsterAI/pull/2332) — feat(providers): add GPT-5.6 and Grok 4.5 default models** — versioned model migration with dedup logic (merged)
- **[#1372](https://github.com/netease-youdao/LobsterAI/pull/1372) — 修复会话中多文件选择只保留最后一个文件的问题** — fixed multi-file attachment bug in Cowork input (merged, stale)

## 4. Community Hot Topics
Only one open issue shows recent community engagement:

- **[#2342](https://github.com/netease-youdao/LobsterAI/issues/2342) — 左下角广告可以彻底关闭吗** (1 comment, opened 2026-07-15)  
  *User reports an in-app ad appearing after updating to v2026.7.15, asking for a permanent disable option.*  
  **Analysis:** This is the only new issue today and appears to be a regression from the latest release. Users want a configuration setting, not just a close button.

*No PRs had exceptional comment activity in this window.*

## 5. Bugs & Stability

| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **High** | [#2342](https://github.com/netease-youdao/LobsterAI/issues/2342) — Unwanted bottom-left ad after update to v2026.7.15 | Open, reported today | None yet |
| **Medium** | [#1384](https://github.com/netease-youdao/LobsterAI/issues/1384) — Multi-file selection in chat only shows last file | Closed (stale) — fixed via [#1372](https://github.com/netease-youdao/LobsterAI/pull/1372) | Merged |
| **Medium** | [#1385](https://github.com/netease-youdao/LobsterAI/issues/1385) — WeChat bot: deleting session doesn't clear history on re-ask | Closed (stale) | No PR |
| **Low** | [#1383](https://github.com/netease-youdao/LobsterAI/issues/1383) — WeChat bot: duplicate messages not synced | Closed (stale) | No PR |
| **Low** | [#2335](https://github.com/netease-youdao/LobsterAI/pull/2335) — Content copy bug | Fixed today | Merged |

The ad regression (#2342) is the top stability concern. The long-standing multi-file selection bug in Cowork has finally been fixed.

## 6. Feature Requests & Roadmap Signals
- **Model support:** [#2332](https://github.com/netease-youdao/LobsterAI/pull/2332) added GPT-5.6 and Grok 4.5 — shows commitment to latest frontier models
- **UI/UX polish:** Multiple PRs (#2336, #2338, #2339) indicate focus on settings reorganization and update flow refinement
- **Windows installer:** [#2323](https://github.com/netease-youdao/LobsterAI/pull/2323) added opt-in Windows web installer — likely to appear in next stable release
- **Cowork homepage revamp:** Implied by the release notes — quick-action scenario redesign may appear in next version

**Predictions for next release:**
- The Cowork homepage quick-action redesign (already in 2026.7.15)
- Windows web installer as optional target
- Continued resolution of WeChat bot sync issues

## 7. User Feedback Summary
- **Dissatisfaction:** The ad regression (#2342) is a clear pain point — users find it intrusive and want a setting to permanently disable it
- **Feature requests:** WeChat bot users continue to request better session deduplication (#1383) and history cleanup on session deletion (#1385)
- **Satisfaction signals:** The long-standing multi-file attachment bug fix (#1384 → #1372) addresses a consistent user complaint in Cowork
- **UX concerns:** Users want logged export warnings to use a less alarming color (#1382 — red implies failure)

## 8. Backlog Watch
The following high-value items remain open and have not received maintainer attention in over 30 days:

- **[#1223](https://github.com/netease-youdao/LobsterAI/issues/1223)** — *(Not shown in 24h data but referenced via related issues)* — WeChat bot session history management appears unresolved
- **[#1322](https://github.com/netease-youdao/LobsterAI/pull/1322) — fix(cowork): true LRU eviction for LLM memory judge cache**  
  *Status:* Open since 2026-04-02 (labeled `stale`)  
  *Worth attention:* Critical performance fix for LLM memory cache that could affect Cowork reliability under load
- **[#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) — chore(deps-dev): bump the electron group**  
  *Status:* Open since 2026-04-02 (label: electron)  
  *Risk:* 3-month gap in Electron dependency updates may introduce unpatched vulnerabilities
- **[#2165](https://github.com/netease-youdao/LobsterAI/pull/2165) — bump actions/checkout from 4 to 6**  
  *Status:* Open since 2026-06-15 — should be reviewed soon for CI pipeline health

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

# TinyClaw Project Digest — 2026-07-16

## 1. Today's Overview
Project activity is very low today, with no new issues, releases, or merged work. A single open pull request (#295) was updated, addressing a logic bug in the CLI’s team leader removal flow. The absence of closed issues or PRs suggests a quiet maintenance period or that attention is focused on higher-priority work elsewhere. Overall project health appears stable but could benefit from increased community engagement.

## 2. Releases
**No new releases today.** The latest public release remains unchanged.

## 3. Project Progress
**No PRs were merged or closed today.** The only open PR is:

- **#295** — *fix(cli): print the "New leader" note after removing a team leader*  
  *Status:* Open (created & last updated 2026-07-15)  
  *Author:* Osamaali313  
  *Summary:* Fixes a logic bug in `teamRemoveAgent` where the condition to print the "New leader" note was always false because `team.leader_agent` was already updated to the new leader before the check. The fix ensures the note is printed only when leadership has actually changed.  
  [View PR #295](https://github.com/TinyAGI/tinyagi/pull/295)

## 4. Community Hot Topics
No issues or PRs have significant comment or reaction activity today. The only discussion item, PR #295, has zero comments and zero reactions, indicating low community engagement on this specific fix.

## 5. Bugs & Stability
One bug was identified via PR #295:

- **Logic bug in CLI team leader removal (Severity: Medium)**  
  *Description:* In `packages/cli/src/team.ts`, when the removed agent is the team leader, the code prompts for a replacement, sets the new leader, and then prints a "New leader" note — but the condition to print it is always false because the leader variable is already updated. As a result, the note is never shown to the user.  
  *Fix available:* Yes, proposed in open PR #295.

No other bugs, crashes, or regressions were reported today.

## 6. Feature Requests & Roadmap Signals
No feature requests or roadmap signals were observed today. The only activity is a minor quality-of-life fix. Based on project trajectory, next versions may continue focusing on CLI polish, team management, and agent lifecycle improvements.

## 7. User Feedback Summary
No user feedback was posted today. The lack of issues or comments may indicate that current users are either satisfied or encountering no blockers that compel them to report.

## 8. Backlog Watch
**No long-unanswered issues or PRs identified.** The project's issue tracker is clean with zero open issues. PR #295 is the only open item and was created just yesterday, so it does not yet qualify as backlog. Maintainers should monitor it for timely review to avoid stagnation.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for **2026-07-16**, based on the provided GitHub data.

---

### 1. Today's Overview
The Moltis project shows high development velocity today, with **6 pull requests merged/closed** in the last 24 hours, indicating a strong push toward stabilization and feature completeness. Activity is focused heavily on **provider model support** and **infrastructure fixes**, particularly around token expiry handling and context window management. No new releases were published today, suggesting the team is consolidating changes before a potential cut. Community engagement is moderate, with one open enhancement request awaiting maintainer feedback.

### 2. Releases
**None.** No new versions were cut in the last 24 hours.

### 3. Project Progress
Six PRs were merged/closed today, advancing several key areas:

- **New Provider Model Support:**
    - **PR #1151** (Closed, *octo-patch*): Added **MiniMax M3** to the provider registry while retaining the older M2.7 model. Includes metadata for context limits and image-input capabilities.
- **Token & Auth Fixes:**
    - **PR #1152** (Closed, *juanlotito*): Fixed a critical **10-day token expiry dead end** in the `openai-codex` provider by deriving expiry from the JWT `exp` claim instead of relying on a null `expires_at` field.
- **Context Window Logic:**
    - **PR #1150** (Closed, *penso*): Centralized context window values by deriving them from model capabilities, including parsing live metadata from GitHub Copilot and Codex dynamic providers.
- **ACP Agent Detection:**
    - **PR #1149** (Closed, *penso*): Added auto-detection for **ACP (Agent Communication Protocol)** external agents, supporting Copilot, Codex, Claude, Pi, Gemini, Augment, and others.
- **Infrastructure & Stability:**
    - **PR #1153** (Closed, *penso*): Added a fallback service manager for **containers without systemd** (e.g., Coder/devbox), improving usability in headless environments.
    - **PR #1148** (Closed, *dependabot[bot]*): Routine dependency bumps for `esbuild` and `vite` across UI and docs directories.

### 4. Community Hot Topics
- **[Issue #574] Model Routing Per Topic** (Open, [Link](https://github.com/moltis-org/moltis/issues/574))
    - *Author:* azharkov78 | *Comments:* 1 | *Reactions:* 1 👍
    - **Analysis:** This is the only active user-facing issue. The request is for intelligent routing of different conversation topics to different LLMs (e.g., routing code generation to a codex model and casual chat to a general model). This suggests a growing user need for **task-specific model selection** beyond simple fallback logic.

### 5. Bugs & Stability
No new bugs or regressions were reported in the last 24 hours. However, the following stability fix was merged today:

- **Critical Fix (Merged):** **PR #1152** fixes a high-severity bug where `openai-codex` sessions would **hard crash every ~10 days** due to missing token expiry logic, requiring manual re-login. This is now resolved.

### 6. Feature Requests & Roadmap Signals
- **Likely for Next Release:**
    - **Multi-Model Routing (Issue #574):** While the request is new, the merged work on **ACP agent auto-detection (PR #1149)** and the ongoing provider registry enhancements suggest the foundation for this feature is already being laid. It is a strong candidate for inclusion in the next minor version.
    - **MiniMax M3 Support (PR #1151):** Already merged, this will ship with the next release.
- **Speculative:**
    - **Containerized CLI (PR #1153):** The systemd-less service fallback hints at upcoming support for running Moltis as a long-lived agent inside ephemeral environments.

### 7. User Feedback Summary
- **Pain Points:**
    - **Token Expiry (Resolved):** Users relying on `openai-codex` were facing forced re-authentication every 10 days. This is now eliminated.
    - **Context Window Friction (Addressed):** The centralization of context window logic via PR #1150 suggests users were experiencing inconsistent behavior when switching between dynamic providers (Copilot/Codex).
- **Desired Usage:**
    - A user (Issue #574) wants a single agent that can dynamically select the best model for the topic at hand, indicating a desire for **unified multi-model orchestration**.

### 8. Backlog Watch
- **[Issue #574] Model Routing Per Topic** ([Link](https://github.com/moltis-org/moltis/issues/574))
    - *Status:* Open since 2026-04-06 (over 3 months) with no maintainer activity.
    - **Risk:** This is a significant feature request that has been largely ignored. While it has only 1 reaction, its age and lack of any comment from the team could signal either low priority or a lack of capacity. If the project intends to support multi-model orchestration, this issue needs a response or a "needs design" label.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the CoPaw project digest for 2026-07-16.

---

## CoPaw Project Digest — 2026-07-16

### 1. Today's Overview
Project activity is **very high**, with 50 Issues and 43 PRs updated in the last 24 hours. The community is heavily focused on the transition to **QwenPaw 2.0**, reporting significant regressions in memory (context retention) and stability, while also proposing new SDKs and channel features. The project maintainers are responsive, actively merging bug fixes and reviewing critical PRs for memory and rendering issues. No new releases were published today, indicating a period of intensive bug-fixing and stabilization.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Project Progress
The team merged/closed **22 PRs** today, demonstrating strong forward momentum. Key advancements include:
- **Memory & Context Fixes:** PR [#6153](https://github.com/agentscope-ai/CoPaw/pull/6153) enhances ReMe memory safeguards with file-size limits and dimension passing, directly addressing a backlog of memory bugs.
- **Console UI & UX:** PR [#6142](https://github.com/agentscope-ai/CoPaw/pull/6142) fixed the auto-memory interval validation, allowing users to set it to 0 to disable it. PR [#6139](https://github.com/agentscope-ai/CoPaw/pull/6139) fixed missing spaces/newlines in thinking blocks, and PR [#6137](https://github.com/agentscope-ai/CoPaw/pull/6137) merged twin fixes for thinking blocks and doom-loop prevention.
- **Channels & Backend:** PRs [#6159](https://github.com/agentscope-ai/CoPaw/pull/6159) and [#6140](https://github.com/agentscope-ai/CoPaw/pull/6140) refactored channel token usage and fixed GBK encoding issues in command execution, improving cross-platform reliability.
- **Website & CI:** PR [#6147](https://github.com/agentscope-ai/CoPaw/pull/6147) added blog view/like counts, a small but key community engagement feature. CI was updated (PR [#6143](https://github.com/agentscope-ai/CoPaw/pull/6143)) to support Supabase config.

### 4. Community Hot Topics
The community is vocal about two main themes: **migration pain to v2.0** and **advanced agent workflows**.

- **Memory Loss in v2.0:** Issue [#6148](https://github.com/agentscope-ai/CoPaw/issues/6148) ("失忆症很严重") with the `/compact` command is receiving rapid attention, with a fix PR [#6123](https://github.com/agentscope-ai/CoPaw/pull/6123) already open. This is the top concern for existing users.
- **Multi-Agent Orchestration:** Issue [#6136](https://github.com/agentscope-ai/CoPaw/issues/6136) highlights a real usability gap: leader agents struggle to autonomously invoke sub-agents. This points to a need for better inter-agent communication protocols.
- **Enterprise & Cross-Platform Needs:** Issue [#6125](https://github.com/agentscope-ai/CoPaw/issues/6125) requests support for the Chinese Kylin OS, and Issue [#6076](https://github.com/agentscope-ai/CoPaw/issues/6076) asks for non-Tauri builds for Windows 7, showing a strong demand from enterprise/government users.
- **New Plugin Features:** PR [#6157](https://github.com/agentscope-ai/CoPaw/pull/6157) introduces a new Chrome extension plugin, which has generated significant interest for enabling browser-based agent interactions.

### 5. Bugs & Stability
Stability remains a primary concern, with several high-severity bugs reported today, all related to the v2.0 release.

| Severity | Bug | Fix PR Exists? |
| :--- | :--- | :--- |
| **Critical** | **Memory Loss & Context Truncation:** Issue [#6148](https://github.com/agentscope-ai/CoPaw/issues/6148) reports severe amnesia after upgrade, with `/compact` failing. | Yes, PR [#6123](https://github.com/agentscope-ai/CoPaw/pull/6123) |
| **Critical** | **Memory Leak on Startup:** Issue [#6124](https://github.com/agentscope-ai/CoPaw/issues/6124) describes a 48GB+ memory leak from ReMe background loops on editable installs. | Yes, PR [#6153](https://github.com/agentscope-ai/CoPaw/pull/6153) |
| **High** | **Agent State Corruption:** Issue [#6141](https://github.com/agentscope-ai/CoPaw/issues/6141) shows that a `MODEL_EXECUTION_ERROR` after aborting a mission leaves the conversation permanently broken. | No |
| **Medium** | **v1.x to v2.0 Migration Bugs:** Issue [#6155](https://github.com/agentscope-ai/CoPaw/issues/6155) details two specific bugs: a missing embedding dimension mapping and auto-memory configuration issues on upgrade. | Yes, PRs [#6153](https://github.com/agentscope-ai/CoPaw/pull/6153) and [#6142](https://github.com/agentscope-ai/CoPaw/pull/6142) |
| **Medium** | **Model Doom Loop:** PR [#6138](https://github.com/agentscope-ai/CoPaw/pull/6138) fine-tunes repetition detection thresholds, a known issue where agents get stuck repeating actions. | Yes, PR [#6138](https://github.com/agentscope-ai/CoPaw/pull/6138) |

### 6. Feature Requests & Roadmap Signals
- **Agent Templates & Ease of Use:** The request for pre-built agent templates (Issue [#4259](https://github.com/agentscope-ai/CoPaw/issues/4259)) was closed, suggesting this is now being considered as a core feature for lowering the barrier to entry for non-technical users.
- **PawApp SDK & Ecosystem:** An experimental PR ([#6150](https://github.com/agentscope-ai/CoPaw/pull/6150)) introduces a **"PawApp SDK" and Kanban app**, signaling a potential shift toward an app/plugin ecosystem. While marked "[Do not merge]", it is a strong roadmapping signal.
- **Desktop UX Improvements:** Issue [#6083](https://github.com/agentscope-ai/CoPaw/issues/6083) requesting quick access to workspace output files is a clear sign that the user workflow on the desktop app needs refinement.
- **Per-Session Model Overrides:** PR [#5992](https://github.com/agentscope-ai/CoPaw/pull/5992) adds the ability to use different models in different conversations, a highly requested power-user feature.

### 7. User Feedback Summary
- **Pain Points (v2.0 Migration):** Users are experiencing significant frustration with the upgrade. The top complaint is "amnesia" (memory loss), making the agent unreliable. A user explicitly stated the `/compact` command appears to be "simply truncating by character count" rather than intelligently summarizing.
- **Satisfaction:** The willingness of users to file detailed bug reports (e.g., with hex dumps and debug packets) shows high engagement and a desire to see the project succeed.
- **Workflow Gaps:** Users are trying to use CoPaw for complex, real-world tasks (multi-agent planning, long-running missions) and finding that the agent struggles with context consistency and autonomous collaboration.
- **Use Cases:** Key use cases include enterprise knowledge management (knowledge bases), project management (multi-agent delegation), and coding assistance (LSP support requested).

### 8. Backlog Watch
- **Long-Standing Issues:** Several issues from April 2026 were updated today, indicating a backlog crop rotation.
    - Issue [#2911](https://github.com/agentscope-ai/CoPaw/issues/2911) (Windows client crashes after hours) is still closed without a clear resolution, implying it may have been a known issue with a silent fix or workaround.
    - Issue [#2930](https://github.com/agentscope-ai/CoPaw/issues/2930) (Tool parsing failures with local models) was recently closed, likely targeting the v2.0 release.
- **Pending Reviews:** PR [#6039](https://github.com/agentscope-ai/CoPaw/pull/6039) ("fix(mcp): resolve ${VAR} env references") is a critical fix for MCP authentication but still under review. It requires maintainer attention to unblock users migrating MCP configs.
- **API Logistics:** Issue [#6076](https://github.com/agentscope-ai/CoPaw/issues/6076) asks for a non-Tauri variant for Windows 7, a request that likely has no easy path forward given the project's architectural decisions. It may need an explicit response from maintainers.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-16

## Today's Overview
ZeroClaw shows **high sustained activity** with 38 issues and 50 PRs updated in the last 24 hours. The project is in an active development phase, with 18 open/active issues, 20 closed, and 38 open PRs versus 12 merged/closed — indicating a **heavy PR pipeline** that is currently stacked toward review and refinement. The maintainer team is processing significant RFC-driven architecture work (OIDC auth, pluggable security, A2A agent discovery) while addressing critical bugs (SSE streaming hangs, agent work interruption, tool-call normalization). No new releases today; the last release attempt (v0.8.3) hit CI timeouts.

## Releases
**No new releases today.** The latest release remains the v0.8.x series. A CI timeout fix PR (#9098) was merged today to increase the build matrix timeout from 40 to 90 minutes to unblock future release cuts.

## Project Progress
**12 PRs were merged/closed today** (out of 50 updated). Key advances:

- **[#9098](https://github.com/zeroclaw-labs/zeroclaw/pull/9098) (merged):** CI release build timeout raised to 90 minutes (unblocking future releases)
- **[#9090](https://github.com/zeroclaw-labs/zeroclaw/pull/9090) (merged):** Enforced tool-call pairing at one canonical chokepoint — fixes Anthropic/Bedrock provider rejections
- **[#9083](https://github.com/zeroclaw-labs/zeroclaw/pull/9083) (merged):** Context overflow trimming now respects model window, adds attribution to compactions
- **[#9070](https://github.com/zeroclaw-labs/zeroclaw/pull/9070) (merged):** Anthropic SSE parser now flushes open tool_use blocks at message_stop
- **[#9071](https://github.com/zeroclaw-labs/zeroclaw/pull/9071) (merged):** ACP session/new now logs agent init failures
- **[#9062](https://github.com/zeroclaw-labs/zeroclaw/pull/9062) (merged):** execute_pipeline sub-tools now gated by per-agent ToolAccessPolicy
- **[#9060](https://github.com/zeroclaw-labs/zeroclaw/pull/9060) (merged):** Malformed native tool-call arguments normalized across OpenAI-format providers
- **[#8901](https://github.com/zeroclaw-labs/zeroclaw/pull/8901) (merged):** Massive repo-wide comment bureaucracy strip + CI gate
- **[#8838](https://github.com/zeroclaw-labs/zeroclaw/pull/8838) (merged):** Idle-bound SSE streaming — prevents hanging on stalled local LLM backends
- **[#8845](https://github.com/zeroclaw-labs/zeroclaw/pull/8845) (merged):** Live sessions now rebuild when agents.<alias>.model_provider is edited
- **[#8754](https://github.com/zeroclaw-labs/zeroclaw/pull/8754) (merged):** Schema V4 breaking cut — removes retired channels, SaaS tools, skills cruft
- **[#8672](https://github.com/zeroclaw-labs/zeroclaw/pull/8672) (merged):** Multi-user auth providers, permission profiles, and principal isolation (RFC #7141)

## Community Hot Topics
### Most commented issues (last 24h):
- **[#5600](https://github.com/zeroclaw-labs/zeroclaw/issues/5600) (12 comments):** Use kimi-code provider in streaming chat triggers a 400 error — "thinking is enabled but reasoning_content is missing" — **open since April, risk:high, S1 blocked**
- **[#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) (7 comments, CLOSED):** OIDC authentication provider RFC — umbrella for pluggable auth, now fully delivered (see PR #8672 merged today)
- **[#7184](https://github.com/zeroclaw-labs/zeroclaw/issues/7184) (6 comments, CLOSED):** Move i18n translation files to git submodule — completed
- **[#6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641) (6 comments):** Turn-level OTel trace correlation — in progress, follow-up to #6009/#6190
- **[#7218](https://github.com/zeroclaw-labs/zeroclaw/issues/7218) (5 comments, CLOSED):** A2A agent discovery RFC (.well-known/agent-card.json) — groundwork for multi-agent interoperability
- **[#9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048) (4 comments):** Separate conversation history from agent-curated long-term memory — RFC, needs maintainer review

**Underlying need:** The community is pushing hard on **multi-user/multi-agent architecture** (OIDC auth, A2A discovery, principal isolation) and **observability/debugging** (OTel tracing, memory separation). The highest-urgency item (#5600) reflects frustration with streaming reliability from third-party providers — users want transparent error handling, not cryptic 400 errors.

### Most active PRs (by comments):
No PRs had comment data populated in the metadata, but the largest PRs by scope/labels include:
- **PR #8880** ([feat(sop): approval broker](https://github.com/zeroclaw-labs/zeroclaw/pull/8880)) — size XL, adds group membership and quorum approval
- **PR #8486** ([feat(gateway): OpenAI chat completions endpoint](https://github.com/zeroclaw-labs/zeroclaw/pull/8486)) — size XL, adds HTTP-api compatibility

## Bugs & Stability
### Critical bugs (S1 — workflow blocked):
1. **[#5600](https://github.com/zeroclaw-labs/zeroclaw/issues/5600)** — kimi-code provider streaming error: "reasoning_content missing" → 400 Bad Request. **Open since April, still not resolved.** No fix PR identified.
2. **[#8559](https://github.com/zeroclaw-labs/zeroclaw/issues/8559)** — Agents stop work when exiting web dashboard chat window. **Open, risk:high.** User workflow completely blocked.
3. **[#8794](https://github.com/zeroclaw-labs/zeroclaw/issues/8794)** — Stopping agent mid-work erases tool calls and thinking from context. **Open, risk:high.** Next message doesn't see prior work.

### Other bugs:
4. **[#9078](https://github.com/zeroclaw-labs/zeroclaw/issues/9078)** (new, today) — Serial transport desynchronized after non-matching response ID (S2 — degraded behavior). No fix PR yet.
5. **[#8560](https://github.com/zeroclaw-labs/zeroclaw/issues/8560)** (CLOSED) — browser_open hangs on headless hosts; unbounded subprocess wait. **Now fixed.**

**Fix PRs merged today:**
- **#8838** — Idle-bound SSE streaming (fixes stalls from local LLMs like llama.cpp, vLLM)
- **#9090** — Tool-call pairing enforcement (fixes Anthropic/Bedrock 400 errors)
- **#9060** — Tool-call argument normalization (fixes malformed JSON arguments across OpenAI-format providers)

## Feature Requests & Roadmap Signals
### Strongest requests from recent issues:
1. **Telegram webhook mode** ([#8046](https://github.com/zeroclaw-labs/zeroclaw/issues/8046)) — Optional webhook ingress alongside long-polling. **Likely for v0.9.x** given the gateway focus.
2. **ComfyUI/RunPod image generation provider** ([#6563](https://github.com/zeroclaw-labs/zeroclaw/issues/6563), [#7875](https://github.com/zeroclaw-labs/zeroclaw/issues/7875)) — Community wants shared media generation across the stack. **Likely v0.9.x; #6563 was closed, suggesting work underway.**
3. **Memory/history separation** ([#9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048)) — Clear RFC from Audacity88; strongly requested. **Could land in v0.9.x as part of the multi-user milestone.**
4. **ZeroCode session history clarity** ([#9047](https://github.com/zeroclaw-labs/zeroclaw/issues/9047)) — Users confused about Code vs Chat memory isolation. **Likely a documentation fix landing soon.**
5. **CI coverage for firmware protocol** ([#9079](https://github.com/zeroclaw-labs/zeroclaw/issues/9079)) — Hardware-focused user wants firmware tests in CI. **Minor, but signals growing hardware community.**

### Predictions for next version:
- **v0.9.x will be the "multi-user" and "security" release** — RFC #7141 (OIDC auth) and #7142 (pluggable security enforcement) are already implemented and merged.
- **SOP (Standard Operating Procedures) milestone** is tracking to 5/5 (#8288 → #8880 approval broker is open).
- **OpenAI Chat Completions endpoint** (#8486) would be a major gateway addition for ecosystem interoperability.

## User Feedback Summary
### Pain points voiced:
1. **Streaming reliability** (#5600) — Users hitting provider-specific errors with no clear resolution path. "Workflow blocked" severity.
2. **Agent work interruption** (#8559, #8794) — Exiting web UI or stopping agent mid-task loses context. Users want "set and forget" background execution.
3. **Learning curve for multi-agent** (#9048, #9047) — Users confused about memory isolation between Code and Chat interaction modes.
4. **Hardware/peripherals** (#9078) — Serial protocol desync makes peripherals unreliable (S2 severity, but important for robot/HW use cases).

### Satisfaction signals:
- **High PR velocity** — 50 PRs updated in 24 hours shows a responsive maintainer team.
- **RFC culture working** — Multiple complex RFCs (#7141, #7142, #7218, #6293) moved from proposal to implementation in weeks.
- **New contributor activity** — Users like Audacity88, Rhoahndur, metalmon filing substantive feature requests and bug reports.

### Use cases emerging:
- Multi-agent deployments needing per-principal isolation and A2A discovery
- Media generation (ComfyUI) as a first-class provider
- Background agent execution (don't stop when user exits chat)
- Hardware/peripheral integration (firmware protocol, serial transport)

## Backlog Watch
### Long-unanswered issues needing maintainer attention:
1. **[#5600](https://github.com/zeroclaw-labs/zeroclaw/issues/5600)** (kimi-code streaming error) — First opened 2026-04-10, still open, 12 comments, **p1, risk:high**. This is the oldest high-severity bug in the active set. Users are clearly frustrated.
2. **[#7875](https://github.com/zeroclaw-labs/zeroclaw/issues/7875)** (RunPod/ComfyUI provider) — 2026-06-17, only 1 comment from maintainer. Feature request with prior PR work that was pulled back for scoping. Needs a decision: accept for v0.9.x or defer.
3. **[#8559](https://github.com/zeroclaw-labs/zeroclaw/issues/8559)** (agents stop on web exit) — 2026-06-30, p1, 3 comments. User workflow completely broken but no fix PR visible yet.
4. **[#8794](https://github.com/zeroclaw-labs/zeroclaw/issues/8794)** (mid-work stop erases context) — 2026-07-07, p1. Related to #8559; these two bugs may share root cause in session lifecycle.

### PRs awaiting maintainer review (labeled `needs-author-action`):
- **#8486** (OpenAI endpoint, since June 29)
- **#7821** (Sandbox policy schema, since June 17)
- **#8571** (OAuth credential fallback fix, since July 1)
- **#7960** (pipeline tool policy gating, since June 19) — **Note: #7960 and #9062 appear to solve the same problem; #9062 was just merged. This PR may be superseded.**

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*