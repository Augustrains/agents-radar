# OpenClaw Ecosystem Digest 2026-07-18

> Issues: 403 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-18 01:14 UTC

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

# OpenClaw Project Digest — 2026-07-18

## 1. Today's Overview

OpenClaw sees **very high activity** with **403 issues** and **500 PRs** updated in the last 24 hours, signaling a project in rapid, continuous development. The **v2026.7.2-beta.2** release shipped today, introducing remote coding sessions, cloud worker Control UI sessions, and improved session resume across OpenCode, Pi, and Claude catalog sessions. While the release brings exciting new capabilities, the community reports **multiple P0/P1 regressions** from the **2026.7.1** release, particularly around Codex turn-completion stalls, Telegram session timeouts, and gateway startup failures. Maintainer bandwidth appears stretched, with **250 open issues** and **302 open PRs** awaiting review, including several critical bugs tagged with release-blocker labels.

---

## 2. Releases

### v2026.7.2-beta.2 — openclaw 2026.7.2-beta.2
**Released:** 2026-07-18

**Highlights:**
- **Remote coding sessions:** Run Control UI sessions on cloud workers; open Codex and Claude catalog sessions in terminals on their owning hosts; resume OpenCode and Pi sessions directly in a terminal. (#107670, #107086, #107200)
- **Native automation and nodes:** (details in release notes)

**No breaking changes or migration notes** were explicitly documented in the release.

---

## 3. Project Progress

In the last 24 hours, **198 PRs** were merged or closed; notable closures and fixes include:

| PR | Description | Status |
|----|-------------|--------|
| [#110289](https://github.com/openclaw/openclaw/pull/110289) | Speed up gateway async tests (Vitest polling interval fix) | **Merged** |
| [#110288](https://github.com/openclaw/openclaw/pull/110288) | Isolate model-call listener state in agents test | **Merged** |
| [#110291](https://github.com/openclaw/openclaw/pull/110291) | Isolate macOS sessions.send follow-up test from host state | **Merged** |
| [#110221](https://github.com/openclaw/openclaw/pull/110221) | Raise default session-store disk budget to 10 GiB (was 2 GiB) | **Closed** (merged) |
| [#106454](https://github.com/openclaw/openclaw/pull/106454) | Sanitize ClawRouter attribution headers to ByteString (fixes emoji/CJK crash) | **Closed** |

**Key feature advancement:**
- [#110269](https://github.com/openclaw/openclaw/pull/110269) **(OPEN):** Permanent OpenClaw presence — pinned sidebar entry and Settings dock (phase 6 of custodian onboarding redesign)

---

## 4. Community Hot Topics

### Most Active Issues (by comment count)

| Issue | Title | Comments | 👍 |
|-------|-------|----------|----|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows Clawdbot Apps | **114** | 81 |
| [#88312](https://github.com/openclaw/openclaw/issues/88312) | [Regression] Codex app-server turn-completion stall ("Codex stopped before confirming") | **20** | 5 |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | Memory Trust Tagging by Source | **18** | 0 |
| [#87744](https://github.com/openclaw/openclaw/issues/87744) | Codex-backed Telegram turns repeatedly time out | **16** | 3 |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked Secrets - Prevent Agent from Accessing Raw API Keys | **14** | 4 |

### Analysis

The **#1 community concern** (#75, 114 comments, 81 👍) remains the long-standing request for **Linux and Windows Clawdbot Apps**, mirroring existing macOS, iOS, and Android support. This has been open since January 2026 and is tagged with security, UX, and product-decision labels.

**Regression anxiety** dominates the top bugs, with **multiple P1 issues** all tracing back to the **2026.5.27 release** or **2026.7.1**: Codex turn stalls (#88312), Telegram timeouts (#87744), and session compaction bugs (#86684). These are tagged with `platinum hermit` severity, indicating senior maintainer attention required.

**Security-conscious users** are vocal: #7707 (memory trust tagging), #10659 (masked secrets), and #7722 (filesystem sandboxing) all reflect a community demanding better guardrails against prompt injection and data exfiltration.

---

## 5. Bugs & Stability

### Critical (P0) — Release Blockers

| Issue | Title | Status | Fix PR? |
|-------|-------|--------|---------|
| [#109867](https://github.com/openclaw/openclaw/issues/109867) | beta.2 state migration creates agent_id index before adding column — blocks gateway startup | **OPEN** | ❌ No fix PR linked |
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | 2026.7.1: gateway fails to start (systemd, ollama, manual launch) — regression | **OPEN** | ❌ No fix PR linked |
| [#101763](https://github.com/openclaw/openclaw/issues/101763) | Hosted Molty: model selector doesn't persist — API always receives dotted id `claude-opus-4.8` | **OPEN** | ❌ No fix PR linked |

### High (P1) — Open Issues

| Issue | Title | Fix PR? |
|-------|-------|---------|
| [#88312](https://github.com/openclaw/openclaw/issues/88312) | Codex app-server turn-completion stall (regression of #84076, fix #85107) | ❌ No new fix PR |
| [#87744](https://github.com/openclaw/openclaw/issues/87744) | Codex-backed Telegram turns time out waiting for turn/completed | ❌ No fix PR |
| [#107464](https://github.com/openclaw/openclaw/issues/107464) | Telegram message prematurely releases Codex turn in message_tool_only mode | ❌ No fix PR |
| [#107873](https://github.com/openclaw/openclaw/issues/107873) | Embedded prompt-lock session takeover aborts WebChat turns after tool failure | ❌ No fix PR |
| [#108344](https://github.com/openclaw/openclaw/issues/108344) | Session-store maintenance evicts in-flight cron sessions mid run-prep | ❌ **Closed** (unresolved?) |
| [#106231](https://github.com/openclaw/openclaw/issues/106231) | Loop detection blocks exec but does not terminate stuck agent run | ❌ No fix PR |
| [#110120](https://github.com/openclaw/openclaw/pull/110120) | active-memory: honor abortSignal during recall cleanup retry delays | ✅ **Fix PR open** |
| [#110216](https://github.com/openclaw/openclaw/pull/110216) | memory: recover from same-file legacy index divergence | ✅ **Fix PR open** (ready for maintainer) |

### Significant Regression Cluster

**2026.5.27/2026.7.1** introduced a wave of Codex-related session reliability bugs. Users report that multi-tool agent turns (Codex app-server, Telegram) stall with "Codex stopped before confirming the turn was complete" or timeout indefinitely. The root cause appears related to turn-completion handshake changes — #88312 explicitly notes this is a regression of #84076 (fixed by #85107), suggesting the fix may have been incomplete.

---

## 6. Feature Requests & Roadmap Signals

### Top Community Feature Requests (by engagement)

| Issue | Feature | Comments | 👍 | Priority |
|-------|---------|----------|----|----------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows Clawdbot Apps | 114 | 81 | P2 |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | Memory Trust Tagging by Source | 18 | 0 | P2 |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked Secrets (prevent agents from seeing raw API keys) | 14 | 4 | P1 |
| [#11665](https://github.com/openclaw/openclaw/issues/11665) | Webhook hook sessions: reuse existing session for multi-turn | 11 | 0 | P2 |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) | Fully dynamic model discovery (OpenRouter + beyond) | 10 | 3 | P2 |
| [#90916](https://github.com/openclaw/openclaw/issues/90916) | Topic-session families (one assistant, multiple context lanes) | 8 | 2 | P2 |

### Predictions for Next Release (v2026.7.x)

1. **Memory Trust Tagging** — High engagement, security-sensitive, multiple maintainer labels. Likely to see a design proposal soon.
2. **Masked Secrets** — Already P1 with a fix-shaped issue. Could land as a security hardening feature in the next beta.
3. **Dynamic Model Discovery** — OpenRouter's fast-moving catalog creates daily friction. PR #10687 mentions Pi's built-in catalog; this may be addressed by a plugin-side change.
4. **Session:end hook** — #10142 has a linked PR open and is straightforward; likely to ship soon.

### Lower-Priority But Notable

- **TUI accessibility** (#9637, #10118) — Screenreader users want emoji-free mode and Shift+Enter for multi-line input.
- **WhatsApp sticker support** (#7476) — Active Telegram/WhatsApp channel users requesting parity.
- **Plain text copy option** (#7909) — Small UX improvement, high daily-use impact.

---

## 7. User Feedback Summary

### Pain Points (Most Frequent)
- **Codex session reliability** is the #1 source of user frustration. Multiple reports describe agents doing work but never delivering results, leaving users with "Codex stopped before confirming" errors.
- **Telegram bot instability** — Duplicate messages (#96242), timeouts (#87744), and premature turn release (#107464) reduce trust in the Telegram channel.
- **Upgrade regressions** — Users report that upgrading across minor versions (2026.5.26→2026.5.27, 2026.6.8→2026.7.1) breaks previously working workflows. The 2026.7.1 gateway startup failure (#108435) left some deployments completely non-functional.
- **Plugin/core version drift** (#83337) — Upgrading core without upgrading plugins causes silent channel failures with no clear warning.

### Expressed Satisfaction
- **Remote coding sessions** in v2026.7.2-beta.2 are likely to be well-received — users have long requested the ability to run Control UI sessions on cloud workers.
- **Session-store disk budget increase** from 2 GiB to 10 GiB (#110221) addresses a common complaint about premature transcript eviction.
- **Quick Chat on Linux** (PR #110285) expands desktop platform parity, though the feature is still maturing.

### Underlying Themes
- **Trust & security** are emerging as major user concerns. Requests for masked secrets, memory trust tagging, and filesystem sandboxing reflect anxiety about prompt injection and agent safety.
- **Platform parity** remains unresolved — the 114-comment request for Linux/Windows Clawdbot Apps shows macOS users have a fundamentally better experience.
- **Documentation gaps** — Users filing bugs often note missing error messages, unclear migration paths, and undocumented configuration options.

---

## 8. Backlog Watch

### Long-Unanswered Important Issues (90+ days with maintainer attention needed)

| Issue | Created | Title | Last Updated | Needs |
|-------|---------|-------|--------------|-------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | 2026-01-01 | Linux/Windows Clawdbot Apps | 2026-07-18 | Product decision, security review, maintainer review |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | 2026-02-03 | Memory Trust Tagging by Source | 2026-07-18 | Product decision, security review |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | 2026-02-06 | Masked Secrets | 2026-07-18 | Product decision, security review |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) | 2026-02-03 | Filesystem Sandboxing Config | 2026-07-18 | Product decision, security review |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) | 2026-02-06 | Dynamic Model Discovery | 2026-07-18 | Live repro needed, product decision |
| [#51572](https://github.com/openclaw/openclaw/issues/51572) | 2026-03-21 | Fire session-memory hook on session reset/prune | 2026-07-17 | Product decision, security review |

### Stale P1 Issues (Needs Maintainer Prioritzation)

| Issue | Title | Stale Since |
|-------|-------|-------------|
| [#96242](https://github.com/openclaw/openclaw/issues/96242) | Multiple independent paths cause duplicate Telegram messages | 2026-06-24 (stale labeled) |
| [#72611](https://github.com/openclaw/openclaw/issues/72611) | Dreaming needs configurable session/cron exclusions | 2026-04-27 (stale labeled) |

### PRs Awaiting Maintainer Review (Critical Path)

| PR | Title | Status | 
|----|-------|--------|
| [#110216](https://github.com/openclaw/openclaw/pull/110216) | fix(memory): recover from same-file legacy index divergence (P1, ready for maintainer) | **Ready for maintainer look** |
| [#110291](https://github.com/openclaw/openclaw/pull/110291) | fix: isolate macOS sessions.send follow-up test | **Merged** |
| [#110256](https://github.com/openclaw/openclaw/pull/110256) | improve(mxc): document sandbox config options and flag network access as dangerous | **Ready for maintainer look** |
| [#109794](https://github.com/openclaw/openclaw/pull/109794) | fix(node-host): guard Claude CLI pipe errors | **Ready for maintainer look** |

### Blocked PRs

| PR | Title | Blocked By |
|----|-------|------------|
| [#110120](https://github.com/openclaw/openclaw/pull/110120) | fix(active-memory): honor abortSignal during recall cleanup | **Waiting on author** |
| [#110285](https://github.com/openclaw/openclaw/pull/110285) | feat(linux): Quick Chat agent switcher, avatars, per-agent routing | **Waiting on author** |
| [#110287](https://github.com/openclaw/openclaw/pull/110287) | refactor: delete unused agent-core session harness layer | **Waiting on author** |

---

## Project Health Summary

| Metric | Value | Assessment |
|--------|-------|------------|
| Open issues | 250 | High — maintainer throughput bottleneck |
| Open PRs | 302 | Very high — review queue growing |
| P0/P1 open bugs | ~15 | Concerning — multiple release blockers |
| Issues updated in last 24h | 403 | Very active community |
| PRs merged in last 24h | 198 | Strong delivery pipeline |
| Longest-open feature request | #75 (197 days) | Unaddressed platform gap |
| Regression cluster | 2026.5.27 / 2026.7.1 | Need urgent investigation |

**Bottom line:** OpenClaw is shipping rapidly with strong feature velocity (remote coding sessions, session budget increases, Linux Quick Chat), but the **regression debt** from the last two releases is accumulating. The Codex turn-completion reliability issues, Telegram channel failures, and gateway startup crashes are eroding user trust and generating high-volume support requests. Until the P0 gateway startup bug (#108435) and the P1 Codex session cluster (#88312, #87744, #107464) are resolved, the project risk is elevated.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-07-18 | **Coverage:** 12 open-source AI agent projects

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is experiencing a **rapid bifurcation** between mature, full-stack platforms (OpenClaw, CoPaw, ZeroClaw) and lean, specialized tools (NanoBot, PicoClaw, Moltis). A common pattern across projects is the shift from single-threaded chat interfaces toward **multi-agent orchestration**, **channel unification** (Telegram, Discord, WhatsApp, Matrix), and **production-grade security hardening**. The ecosystem is also converging on standardized agent communication protocols (A2A), supply-chain security (SLSA, OIDC), and sandboxed execution—reflecting enterprise adoption pressure. However, **regression debt** is accumulating: rapid release cycles across the top projects are producing a steady stream of P0/P1 bugs, particularly around Codex session reliability, gateway startup, and multimodal handling.

---

## 2. Activity Comparison

| Project | Open Issues | Open PRs | Recent Release | Activity Level | Health Assessment |
|---------|-------------|----------|----------------|----------------|-------------------|
| **OpenClaw** | 250 | 302 | v2026.7.2-beta.2 | Very High | 🟡 **Strained** – shipping fast, regression debt accumulating |
| **ZeroClaw** | ~50 (50 updated) | ~50 | None today | Very High | 🟢 **Healthy** – disciplined merging, security-focused |
| **CoPaw** | ~25 (25 updated) | ~42 (15 merged) | v2.0.0.post3 | Very High | 🟢 **Healthy** – high closure rate, Windows UX gap |
| **Hermes Agent** | 42 | 48 | None today | High | 🟡 **Strained** – heavy backlog, community hardening PRs unmerged |
| **NanoBot** | ~2 | ~11 (4 merged) | None today | Very High | 🟢 **Healthy** – bugs fixed same-day, maintainer responsive |
| **PicoClaw** | ~3 (4 updated) | ~12 (2 merged) | None (v0.2.9 latest) | Moderate | 🟢 **Stable** – low activity but well-maintained |
| **NanoClaw** | ~3 (4 updated) | ~15 (3 merged) | None (v2.x latest) | High | 🟡 **Moderate** – silent failures concern, few maintainer responses |
| **LobsterAI** | 2 | ~2 (13 merged) | 2026.7.16 | High | 🟢 **Strong** – 87% closure rate, feature-forward |
| **IronClaw** | ~50 (50 updated) | ~50 (26 merged) | None (v0.29.1 pending) | Very High | 🟢 **Healthy** – systematic refactoring, disciplined closures |
| **NullClaw** | 1 | 0 | v2026.5.29 | Minimal | 🔴 **Critical** – single critical bug (SIGSEGV) unaddressed |
| **Moltis** | ~1 (1 updated) | 2 (none merged) | 20260717.03 | Low | 🟢 **Stable** – minor patches, no regressions |
| **TinyClaw** | 0 | 0 | None | **None** | ⚪ **Dormant** |
| **ZeptoClaw** | 0 | 0 | None | Low | 🟢 **Stable** – maintenance only, backlog cleared |

---

## 3. OpenClaw's Position

**Advantages over peers:**
- **Scale:** 403 issues + 500 PRs updated in 24h dwarfs all other projects (next closest: ZeroClaw at ~50 each). Community engagement is 8-10x larger.
- **Feature velocity:** Remote coding sessions, cloud worker Control UI, and cross-session resume (OpenCode, Pi, Claude catalog) are capabilities no other project yet offers.
- **Platform breadth:** Supporting macOS, iOS, Android, Linux (Quick Chat in beta), and Telegram—versus Hermes Agent (macOS/Desktop only) or PicoClaw (channel-focused).

**Technical approach differences:**
- OpenClaw's architecture emphasizes **session resumption** and **worker delegation**—code sessions can migrate between terminal, cloud, and Control UI contexts. This contrasts with ZeroClaw's **Wasm-first plugin runtime** or IronClaw's **Reborn engine consolidation**.
- OpenClaw uses a **unified gateway** (ClawRouter) for all channels; PicoClaw and NanoClaw use per-channel adapters with less centralized routing.

**Community size comparison:**
- OpenClaw's top issue (#75, Linux/Windows Clawdbot Apps) has 114 comments and 81 👍—more engagement than any single issue in Hermes Agent (11 max), ZeroClaw (11 max), or CoPaw (7 max).
- However, OpenClaw's **maintainer bandwidth is severely strained** (250 open issues, 302 open PRs, 15+ P0/P1 bugs). ZeroClaw and CoPaw maintain better closure ratios despite smaller teams.

**Risk:** OpenClaw's growth is outpacing its ability to stabilize. The project is **the most innovative but also the most fragile**.

---

## 4. Shared Technical Focus Areas

| Requirement | Projects | Specific Needs |
|-------------|----------|----------------|
| **Channel unification** | OpenClaw, PicoClaw, NanoClaw, IronClaw, Hermes Agent | Telegram, Discord, WhatsApp, Matrix, QQ, Feishu parity across channels |
| **Multi-agent routing** | ZeroClaw, OpenClaw, CoPaw | Isolated agents per workspace, per-sender RBAC, A2A interop |
| **Security & secret management** | OpenClaw, ZeroClaw, PicoClaw, Hermes Agent | Masked secrets (#10659), memory trust tagging (#7707), OIDC, sandboxing |
| **Session reliability** | OpenClaw, Hermes Agent, NanoClaw, CoPaw | Codex turn stalls, Telegram timeouts, duplicate messages, silent drops |
| **Model provider flexibility** | NanoBot, Hermes Agent, Moltis, ZeroClaw | Dynamic model discovery (OpenRouter), per-call provider override, reasoning level selection |
| **Desktop/CLI UX** | OpenClaw, ZeroClaw, LobsterAI, CoPaw | TUI accessibility, emoji-free mode, Shift+Enter, status bar improvements |
| **Upgrade stability** | OpenClaw, CoPaw, Hermes Agent | v1→v2 migration scripts, regression testing, plugin/core version drift detection |
| **Security hardening** | ZeroClaw, OpenClaw, IronClaw | SLSA provenance, OIDC, sandbox policies, supply-chain signing |

**Notable gap:** No project has solved **upgrade regression testing** well. OpenClaw's 2026.7.1→2026.7.2 regression cluster, CoPaw's v1→v2 migration issues (#6155), and Hermes Agent's long-unresolved update pipeline bug (#3523) all point to a systemic weakness.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | CoPaw | Hermes Agent | NanoBot | PicoClaw |
|-----------|----------|----------|-------|---------------|---------|----------|
| **Target user** | Power users, multi-platform devs | Enterprise, multi-tenant ops | Chinese ecosystem, Windows users | Desktop-first, macOS devs | Lightweight, server users | Multi-channel bot operators |
| **Primary architecture** | Gateway + session-resume, cloud workers | Wasm plugins, OIDC, sandboxing | AgentScope protocol, MCP drivers | Hardened subprocess, CLI-first | Provider abstraction, WebUI | Channel adapters, streaming |
| **Release cadence** | Weekly betas (high risk) | Security-focused (v0.9.0) | Bi-weekly patches | Slow, stabilization | Daily bug-fix | Monthly |
| **Strengths** | Feature breadth, community size | Enterprise security, testing discipline | Ecosystem compatibility, Windows support | Robustness, community hardening | Provider support, rapid fixes | Channel parity, streaming |
| **Weaknesses** | Regression debt, maintainer bottleneck | macOS broken, PR author bottlenecks | Windows permission issues, internationalization | CLI exit codes, multimodal crashes | Less feature coverage | Low scaling activity |
| **Unique features** | Remote coding sessions, cloud worker UI | Wasm plugins, multi-agent routing, A2A | AgentScope integration, MCP ecosystem | Subprocess hardening initiative | Moonshot Kimi fast fixes, ModelScope | QQ streaming, WhatsApp presence |

**Key differentiation:** 
- **OpenClaw** is the **broadest** platform but **most brittle**.
- **ZeroClaw** is the **most architecturally ambitious** (Wasm, A2A, SLSA) but has **execution gaps** (macOS broken, PRs stalled).
- **CoPaw** is the **most ecosystem-connected** (AgentScope, MCP) but has **platform gaps** (Windows admin requirement).
- **Hermes Agent** is the **most community-hardened** but has **slow maintainer velocity**.
- **NanoBot** is the **fastest to respond** to provider changes but has **limited scope**.
- **PicoClaw** is the **best for multi-channel deployments** but has **low growth activity**.

---

## 6. Community Momentum & Maturity

### Tier 1: Rapid Iteration (high risk/reward)
- **OpenClaw** – 403 issues/500 PRs updated daily. Shipping weekly betas but accumulating regression debt. Community engagement is unmatched but maintainer burnout is a real risk.
- **CoPaw** – 25 issues/42 PRs updated daily. High closure rate (87% of PRs today). Growing international user base. Windows UX is the biggest friction point.
- **ZeroClaw** – 50 issues/50 PRs updated daily. Strong architectural vision. Blocked by "author-action bottleneck" on large PRs. macOS broken.

### Tier 2: Stabilization & Hardening (healthy maturation)
- **IronClaw** – 50 issues/50 PRs updated daily. Systematic refactoring toward v1.0. Disciplined closure (26 merged today). Most organized project in ecosystem.
- **LobsterAI** – 2 issues/15 PRs updated daily. 87% closure rate. Feature-forward (AI skins). UI polish focus. Stable, mature project.
- **Hermes Agent** – 42 issues/48 PRs. Heavy community hardening effort (subprocess timeout initiative). Slow maintainer merging is the bottleneck.

### Tier 3: Focused & Stable (low volatility)
- **NanoBot** – 2 issues/11 PRs. Rapid bug-fix turnaround (same-day). Provider compatibility focus. Healthy but narrow scope.
- **PicoClaw** – 3 issues/12 PRs. Moderate activity. Channel parity focus. No regressions. Well-maintained but not scaling quickly.

### Tier 4: Declining or Dormant
- **NullClaw** – 1 open issue (critical SIGSEGV, unaddressed for 2+ days). No PR activity. **Project is effectively stalled** with a blocking bug on aarch64.
- **Moltis** – 1 issue updated, 2 open PRs. Low activity. Minor patches only. Feature request (#574) has been open for 3+ months.
- **TinyClaw** – **Zero activity in last 24 hours.** Dormant.
- **ZeptoClaw** – Zero open issues/PRs. Maintenance-only (D5 gate-point data updates). Project may be in a pause or completion phase.

---

## 7. Trend Signals

### Signals for AI Agent Developers

**1. Security is now table stakes**
- ZeroClaw's SLSA/OIDC/sandbox RFCs, OpenClaw's masked secrets (#10659) and memory trust tagging (#7707), and PicoClaw's OAuth race fix (#3239) all point to **enterprise security becoming a must-have**—not a differentiator.
- **Action:** Prioritize secret management, sandboxed execution, and supply-chain signing in agent deployments.

**2. Multi-agent orchestration is converging**
- ZeroClaw (multi-agent routing, A2A), OpenClaw (session routing), CoPaw (AgentScope), and Moltis (ACP-only support) all signal that **single-agent chat is not the end state**. Developers should plan for multi-agent, multi-channel architectures.
- **Action:** Build agents with A2A/MCP compatibility and session isolation from day one.

**3. Reliability > novelty**
- OpenClaw's regression cluster (#88312, #87744, #108435) and Hermes Agent's CLI exit code bug (#62810) show that **user trust is eroding due to release velocity**. The most successful projects (IronClaw, CoPaw, NanoBot) prioritize stability over new features.
- **Action:** Invest in regression test suites, upgrade migration scripts, and canary releases.

**4. Channel unification is incomplete but essential**
- PicoClaw (QQ, WhatsApp), NanoClaw (Discord, Matrix), CoPaw (Feishu), and OpenClaw (Telegram, Codex) reveal that **users expect their agent to work everywhere**. Channel adapters are becoming a standard architectural component.
- **Action:** Design agents with a channel abstraction layer; do not hardcode to Telegram or Discord only.

**5. Provider abstraction is a core competency**
- NanoBot's Moonshot Kimi temperature fix (within hours), Hermes Agent's Gemini/OpenRouter bugs, and Moltis's ACP-only setup show that **API fragility is universal**. A robust provider abstraction layer is critical.
- **Action:** Implement provider-agnostic interfaces with graceful degradation and fallback strategies.

**6. Platform parity matters more than features**
- OpenClaw's #75 (Linux/Windows Clawdbot Apps, 114 comments, 81 👍) and ZeroClaw's broken macOS app (#7527) confirm that **platform gaps are the #1 user frustration**—more than missing features.
- **Action:** Ship core functionality on all three major platforms (Linux, macOS, Windows) before adding exotic capabilities.

**7. Community hardening is outpacing maintainer capacity**
- Hermes Agent's 24 unmerged subprocess-timeout PRs from user `x7peeps` and ZeroClaw's 8+ stalled large PRs signal that **community contributors are outpacing maintainers' ability to review**. This creates contributor churn and security risk.
- **Action:** Establish clear PR review SLAs, shepherd programs, and merge queues.

---

## Summary Table: Ecosystem Health

| Metric | Ecosystem Signal |
|--------|------------------|
| **Most active** | OpenClaw (403 issues, 500 PRs) |
| **Best stability:velocity ratio** | CoPaw (87% closure), IronClaw (52% closure) |
| **Highest community growth** | ZeroClaw (increasing English-language issues) |
| **Most fragile** | OpenClaw (15+ P0/P1, maintainer bottleneck) |
| **Most organized** | IronClaw (systematic refactoring toward v1.0) |
| **At risk of stalling** | NullClaw, TinyClaw, ZeptoClaw |
| **Best bug-response time** | NanoBot (hours) |
| **Blocked PRs (needs maintainer)** | Hermes Agent (24 PRs), ZeroClaw (8+ PRs) |
| **Emerging standard** | A2A protocol, MCP integration, SLSA provenance |

**Bottom line for developers:** Choose **OpenClaw** for maximum features and community; **ZeroClaw** for enterprise security and multi-tenant deployments; **CoPaw** for AgentScope/MCP ecosystem integration; **NanoBot** for lightweight server deployments. Expect **reliability investments** across all projects in Q3-Q4 2026 as the ecosystem matures beyond "move fast and break things."

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-18

## 1. Today's Overview

Development activity was **very high** today, with 11 PRs updated and 4 merged/closed, alongside 2 closed issues. The team focused heavily on provider compatibility fixes and new provider support, while the WebUI received significant UX polish. No new releases were cut today. The maintainer team appears actively engaged, with several critical Moonshot Kimi temperature bugs being identified, fixed, and iterated upon within hours. The project is in a healthy state with strong contributor momentum.

## 2. Releases

No new releases were published today.

## 3. Project Progress

**4 PRs merged/closed today across several domains:**

- **Provider fixes (Moonshot Kimi critical bugs):**
  - [#4962](https://github.com/HKUDS/nanobot/pull/4962) — Corrected Moonshot `kimi-k2.6` temperature override from 1.0 to the now-required 0.6 (fixing every request that was failing).
  - [#4967](https://github.com/HKUDS/nanobot/pull/4967) — Further refined the fix: stop sending temperature for `kimi-k2.5` and `kimi-k2.6` entirely, letting Moonshot select its fixed temperature based on thinking mode (1.0 for thinking, 0.6 for non-thinking).

- **Internationalization:**
  - [#4958](https://github.com/HKUDS/nanobot/pull/4958) — Improved zh-TW Traditional Chinese locale translation quality.

- **WebUI feature:**
  - [#4953](https://github.com/HKUDS/nanobot/pull/4953) — Added support for native folder picker bridges through WebUI bootstrap, enabling native host integration for file selection.

## 4. Community Hot Topics

**Most active item (4 comments):**
- [#4968](https://github.com/HKUDS/nanobot/issues/4968) — "Unbound cron jobs" enhancement: A user questions why NanoBot forbids creating unbound cron jobs, citing the code that immediately returns an error for unbound cron jobs. This touched on workflow flexibility and was closed, suggesting maintainers provided a rationale or solution.

**Other notable activity:** The Moonshot Kimi temperature bugs ([#4961](https://github.com/HKUDS/nanobot/issues/4961)) spawned two quick-fix PRs and a follow-up refinement, showing strong community and maintainer responsiveness to production-breaking issues.

**Underlying need:** Users are pushing for more flexibility in cron job creation (unbound) and encountering provider API changes that require rapid adaptation in the provider abstraction layer.

## 5. Bugs & Stability

**High severity (actively breaking: 2 bugs, both fixed today):**
1. **Moonshot `kimi-k2.6` temperature rejection (regression)** — API changed to require exactly 0.6, but NanoBot hardcoded 1.0. Every request failed. *Fix:* [#4962](https://github.com/HKUDS/nanobot/pull/4962) → Then refined in [#4967](https://github.com/HKUDS/nanobot/pull/4967) to omit temperature entirely for K2.5/K2.6. **Status: Resolved.**

**Medium severity:**
- No new regression reports. The fix in [#4925](https://github.com/HKUDS/nanobot/pull/4925) (still open) addresses hard context overflow errors with clearer user messages and proper stop reasoning — preventing silent failures during context overflow.

**Overall stability assessment:** Good. Two critical bugs hit and were fixed within hours. No outstanding critical bugs remain open.

## 6. Feature Requests & Roadmap Signals

**Active feature development (likely for next release):**
- **ModelScope provider support** ([#4965](https://github.com/HKUDS/nanobot/pull/4965), open) — Adding ModelScope as a built-in provider for open-source models (Qwen, DeepSeek, Kimi, GLM, etc.). This would significantly expand NanoBot's reach in the Chinese AI ecosystem.
- **Kimi K3 support** ([#4966](https://github.com/HKUDS/nanobot/pull/4966), open) — Native handling for Kimi K3's `reasoning_effort="max"` contract, indicating Moonshot's next-generation model is being integrated.
- **Channel architecture refactor** ([#4908](https://github.com/HKUDS/nanobot/pull/4908), open) — Making built-in channels self-contained packages with unified registration, removing central coupling — a major architectural improvement for third-party channel development.

**WebUI enhancements (already merged or open):**
- Agent output polish with live thinking surface and semantic action grouping ([#4963](https://github.com/HKUDS/nanobot/pull/4963))
- Live image generation settings hot-apply ([#4964](https://github.com/HKUDS/nanobot/pull/4964))
- One-click Render deploy support ([#4937](https://github.com/HKUDS/nanobot/pull/4937))

**Prediction:** Next release (likely v0.x.x) will include ModelScope provider, Kimi K3 support, and the channel refactor — representing major provider and architectural expansion.

## 7. User Feedback Summary

- **Pain point: Provider API fragility** — The Moonshot temperature change broke existing users without warning. Users expect the provider abstraction layer to handle such API shifts gracefully (e.g., by not hardcoding forced overrides).
- **Pain point: Cron job restrictions** — The "unbound cron jobs" issue indicates users want more flexible scheduling capabilities without being forced into bound job patterns.
- **Satisfaction indicators:** The rapid fix turnaround (~hours) on the Moonshot break shows users appreciate responsive maintainers. The zh-TW locale improvement shows attention to internationalization quality.
- **Use case expansion:** The ModelScope PR and Kimi K3 support suggest user demand for broader model provider choice, particularly in markets where ModelScope is prevalent.

## 8. Backlog Watch

**No long-unanswered issues or PRs identified** — all tracked issues and PRs have received attention within the last 24 hours. The maintainer team (Re-bin, chengyongru) is actively reviewing and engaging with open PRs.

**Items that may need maintainer attention soon:**
- [#4908](https://github.com/HKUDS/nanobot/pull/4908) (channel refactor, open since July 13) — Large architectural change that may require careful review.
- [#4965](https://github.com/HKUDS/nanobot/pull/4965) (ModelScope provider) — Tagged with `conflict`, may need merge conflict resolution.
- The unbound cron jobs feature request ([#4968](https://github.com/HKUDS/nanobot/issues/4968)) was closed, but the underlying desire for scheduling flexibility may resurface if the rationale is not documented.

---

**Project health:** Green. High contributor velocity, critical bugs fixed same-day, healthy mix of features and fixes, strong maintainer engagement.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-07-18

## Today's Overview

Hermes Agent is experiencing a period of intense community engagement and stabilization effort, with 50 issues and 50 PRs updated in the last 24 hours. The project shows strong open-source health with 42 open/active issues and 48 open PRs, though only 2 closed issues and 2 merged/closed PRs were recorded today, indicating a heavy triage and review backlog rather than rapid merging. The overwhelming theme of recent contributions is systematic robustness improvements, particularly adding timeouts and error handling to subprocess calls across the entire codebase, suggesting a concerted effort to address edge-case hangs and crashes that have been reported by the user community. No new releases were published today.

## Releases

No new releases were published on 2026-07-18. The latest release remains earlier versions.

## Project Progress

Only 2 PRs were merged or closed today. The closed items include:

- **[#66559](https://github.com/NousResearch/hermes-agent/issues/66559)** (CI-sensitive file review fails on every fork PR) — closed, likely resolved with a CI-pipeline fix for the `AUTOFIX_BOT_PAT` access issue.
- **[#66045](https://github.com/NousResearch/hermes-agent/issues/66045)** (Codex transport over-length `prompt_cache_key` causing silent fallback) — closed, indicating a fix was deployed.

The 48 open PRs show a strong pattern of defensive programming improvements contributed primarily by user `x7peeps`, who has submitted a wave of PRs adding `timeout`, `stdin=DEVNULL`, and `return_exceptions=True` parameters to `subprocess.run()` and `asyncio.gather()` calls across the CLI, agent, gateway, plugin, and tool subsystems (e.g., PRs [#62461](https://github.com/NousResearch/hermes-agent/pull/62461), [#62735](https://github.com/NousResearch/hermes-agent/pull/62735), [#63646](https://github.com/NousResearch/hermes-agent/pull/63646), [#64676](https://github.com/NousResearch/hermes-agent/pull/64676), etc.). This represents a massive community-driven hardening initiative.

## Community Hot Topics

The most active discussions indicate three key community pain points:

1. **CLI exit code regression** — Issue [#62810](https://github.com/NousResearch/hermes-agent/issues/62810) (5 comments): The CLI dispatcher drops integer exit statuses from command handlers, causing `set -e`, `&&` chaining, and CI automation to always see exit code `0`. This is a fundamental reliability issue for headless/automated usage.

2. **Infinite retry loop on vision turns** — Issue [#66267](https://github.com/NousResearch/hermes-agent/issues/66267) (5 comments, P1 priority): After image processing or context compaction, a bug causes an infinite retry loop that exhausts the API-call budget. The error involves `"expected string or bytes-like object"` on a content list, suggesting a serialization issue in multimodal message handling. This is the highest-priority open bug.

3. **Update pipeline regressions** — Issue [#3523](https://github.com/NousResearch/hermes-agent/issues/3523) (6 comments, oldest open issue in top set, created March 2026): The `hermes update` command lost git fetch progress output and creates unnecessary stashes on every run. Despite being open for nearly 4 months, this has not been resolved.

## Bugs & Stability

**Critical/P1 Severity:**
- **[#66267](https://github.com/NousResearch/hermes-agent/issues/66267)** — Multimodal content list crashes creating infinite retry loop exhausting API budget. No fix PR identified.

**High/P2 Severity (new today):**
- **[#66589](https://github.com/NousResearch/hermes-agent/issues/66589)** — Telegram startup notification race condition after planned restart, causing `send_path_degraded` failure. No fix PR yet.
- **[#66587](https://github.com/NousResearch/hermes-agent/issues/66587)** — Gemini provider HTTP 400: `Function call is missing thought_signature` in functionCall parts. No fix PR.
- **[#66572](https://github.com/NousResearch/hermes-agent/issues/66572)** — LM Studio initialization hardcodes context length to 64000 tokens, ignoring configured value. (Marked duplicate.)
- **[#66574](https://github.com/NousResearch/hermes-agent/issues/66574)** — Two Windows-specific issues: reasoning-field exhaustion not surfaced, and stale runtime state from Desktop process lifecycle. Requires repro and decision.
- **[#66544](https://github.com/NousResearch/hermes-agent/issues/66544)** — Custom-provider metadata probes ignore provider-scoped SSL CA settings. No fix PR.
- **[#66518](https://github.com/NousResearch/hermes-agent/issues/66518)** — WSL2 stdio MCP watchdog kills all healthy children due to `create_time` equality check breaking on clock drift. (Marked duplicate.)

**Medium/P3 Severity (new today):**
- **[#66541](https://github.com/NousResearch/hermes-agent/issues/66541)** — Kanban workers inherit dispatcher terminal settings instead of assignee profile configuration.
- **[#66543](https://github.com/NousResearch/hermes-agent/issues/66543)** — Custom providers do not map reasoning effort correctly to supported levels.

**Regression Watch:** The large wave of timeout/error-handling PRs (20+ PRs from user `x7peeps`) while not yet merged suggests the project is systematically addressing a pattern of subprocess hangs that have been plaguing the CLI, update flow, MCP installations, and gateway operations.

## Feature Requests & Roadmap Signals

Several feature requests emerged today, suggesting areas where the community sees gaps:

- **[#66621](https://github.com/NousResearch/hermes-agent/issues/66621)** — Custom icons for Desktop profiles (1 comment, 2026-07-18). Low complexity, likely for next minor Desktop release.
- **[#66536](https://github.com/NousResearch/hermes-agent/issues/66536)** — Per-call model/provider override for `delegate_task` (2 comments). This would enable multi-model delegation, a significant architectural enhancement.
- **[#9978](https://github.com/NousResearch/hermes-agent/issues/9978)** — Interactive card format for Feishu/Lark gateway messages (4 comments, opened April 2026). Desired for production deployments with multi-model routing.
- **[#50748](https://github.com/NousResearch/hermes-agent/issues/50748)** — Display token generation speed in Desktop app (1 comment). A usability enhancement for comparing model performance.
- **[#14859](https://github.com/NousResearch/hermes-agent/issues/14859)** — Show current session title in CLI/TUI status bar (2 comments). Small UI enhancement.
- **[#11442](https://github.com/NousResearch/hermes-agent/issues/11442)** — GitHub Copilot provider support for GitHub Enterprise Server (2 comments). Enterprise adoption blocker.

**Prediction:** The custom provider reasoning-effort mapping ([#66543](https://github.com/NousResearch/hermes-agent/issues/66543)) and per-call model override for delegation ([#66536](https://github.com/NousResearch/hermes-agent/issues/66536)) are architecturally significant and could appear in the next minor version (0.19.x), while UI features like custom icons ([#66621](https://github.com/NousResearch/hermes-agent/issues/66621)) and token speed display ([#50748](https://github.com/NousResearch/hermes-agent/issues/50748)) are likely for a Desktop-focused patch release.

## User Feedback Summary

**Pain Points (expressed directly or inferred from bug reports):**
- Users of automation/CI pipelines are frustrated by the CLI exit code bug ([#62810](https://github.com/NousResearch/hermes-agent/issues/62810)) breaking shell scripts and CI workflows with `set -e`.
- Vision/multimodal users are hitting a critical reliability wall with infinite retries exhausting API budgets ([#66267](https://github.com/NousResearch/hermes-agent/issues/66267)), effectively making image processing unusable in some configurations.
- Desktop users on Windows continue to face platform-specific issues: LM Studio integration failures ([#51448](https://github.com/NousResearch/hermes-agent/issues/51448)), MCP watchdog killing processes ([#66518](https://github.com/NousResearch/hermes-agent/issues/66518)), and stale runtime state ([#66574](https://github.com/NousResearch/hermes-agent/issues/66574)).
- Enterprise users are blocked by GHE Copilot support gap ([#11442](https://github.com/NousResearch/hermes-agent/issues/11442)) and the lack of Feishu interactive cards ([#9978](https://github.com/NousResearch/hermes-agent/issues/9978)).
- Security-conscious users have flagged that `uv.lock` pins vulnerable package versions, and pip fixes are transient ([#60841](https://github.com/NousResearch/hermes-agent/issues/60841)) — a concerning finding for production deployments.

**Satisfaction Signals:** The large volume of community-contributed hardening PRs (especially the `subprocess` timeout initiative) indicates a technically engaged user base that trusts the project's direction and is willing to invest in improving robustness. The lack of show-stopping complaints about core agent capabilities suggests the ML/agent functionality itself is generally working as expected.

## Backlog Watch

Several issues and PRs warrant maintainer attention due to age, severity, or strategic importance:

1. **[#3523](https://github.com/NousResearch/hermes-agent/issues/3523)** — *hermes update* regression. Created **2026-03-28** (nearly 4 months old), P2, needs-decision. This is one of the oldest open issues and affects the core update workflow for all users. Stale with 0 reactions suggests low community urgency but high functional impact.

2. **[#60841](https://github.com/NousResearch/hermes-agent/issues/60841)** — Vulnerable packages pinned in `uv.lock`. Security-related, P3. Has a maintainer-assigned `sweeper:risk-compatibility` label but no fix PR. For production deployments, unpatched CVEs in the lockfile are a governance blocker.

3. **[#33981](https://github.com/NousResearch/hermes-agent/issues/33981)** — RFC: Centralized Model/Provider Registry (2026-05-28). Closed, but the underlying architecture decision (centralized vs. distributed provider config) affects all future provider-related features.

4. **[#65907](https://github.com/NousResearch/hermes-agent/pull/65907)** — Gateway `asyncio.create_task` ref storage. Open, P2, needs-decision. This PR fixes potential task garbage collection in Python 3.12+ but requires architectural decision on background task management pattern.

5. **[#51448](https://github.com/NousResearch/hermes-agent/issues/51448)** — Windows Desktop + LM Studio fails (2026-06-23). P2, needs-repro, Windows-specific. With growing Windows Desktop usage, this platform gap needs resolution.

6. **[#62461](https://github.com/NousResearch/hermes-agent/pull/62461) through [#65963](https://github.com/NousResearch/hermes-agent/pull/65963)** — The 24 unmerged PRs from user `x7peeps` representing the subprocess timeout hardening initiative. These PRs (all P3, `sweeper:blast-contained` or `blast-moderate`) are low-risk individually but large in aggregate. Prioritizing and merging them in batches would significantly improve overall stability.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-18

## 1. Today's Overview
PicoClaw shows **moderate activity** with 4 issues and 12 PRs updated in the last 24 hours. The project has no new releases, but a steady stream of contributions focuses on **security hardening**, **performance optimization**, and **channel feature parity** (WhatsApp typing presence, QQ streaming). The open-to-closed ratio (3 open issues, 2 merged/closed PRs) indicates ongoing development with good review throughput. Community contributions are diverse, with multiple first-time and repeat contributors addressing both user-facing features and internal technical debt.

## 2. Releases
**No new releases** today (latest remains v0.2.9 / git 2992…). The absence of releases since last month (v0.3.1 mentioned in PR #3247 as having introduced `enableCodeWrap`/`disableCodeWrap` keys) suggests the current PR batch may be accumulating toward a v0.3.2 or v0.4.0 release.

## 3. Project Progress
**Merged/Closed PRs today (2 items):**
- [#3204 [CLOSED] fix(deps): restore Azure dependency freeze baseline](https://github.com/sipeed/picoclaw/pull/3204) — by **gezhengbin888**: Downgraded Azure SDK modules to frozen baseline versions (`azcore v1.21.1`, `azidentity v1.13.1`, MSAL v1.6.0) to align with downstream supply-chain checks. This is a **stability fix** for enterprise/infrastructure users.
- [#3180 [CLOSED] fix(cli): skip tool calls with invalid arguments](https://github.com/sipeed/picoclaw/pull/3180) — by **Alix-007**: Prevents CLI crashes when tool call arguments are malformed JSON; keeps valid tool calls from the same response. **Bug fix** for CLI reliability.

## 4. Community Hot Topics
- **[#3201 [OPEN] Support streaming output for QQ channel](https://github.com/sipeed/picoclaw/issues/3201)** (3 comments): User YsLtr requests token-by-token streaming for QQ channel, currently only available on Telegram and Pico WebSocket. **Underlying need**: Users on QQ (a major Chinese messaging platform) want real-time feedback during LLM response generation.
- **[#3206 [CLOSED] v2→v3 config migration fails with false 'unknown field(s): build_info, session.dm_scope'](https://github.com/sipeed/picoclaw/issues/3206)** (2 comments): Fresh installs on latest release encounter migration failure — **critical onboarding issue** resolved for those affected.
- **[#3239 [OPEN] OAuth refresh requests use incompatible provider semantics and can race](https://github.com/sipeed/picoclaw/issues/3239)** (1 comment) + **PR [#3241 [OPEN] fix(auth): make OAuth refresh provider-correct and concurrency-safe](https://github.com/sipeed/picoclaw/pull/3241)** (by As-tsaqib): Highlights a **systemic OAuth design flaw** affecting multiple providers (OpenAI JSON vs form-encoded, race conditions). Underlying need: enterprise-grade authentication reliability.

## 5. Bugs & Stability
| Severity | Issue | Status | Fix PR Exists? |
|----------|-------|--------|----------------|
| **High** | [#3206] v2→v3 config migration fails on fresh install (build_info, dm_scope) | **CLOSED** | Yes (PR #3204 indirectly addresses dependency)] |
| **High** | [#3239] OAuth refresh: incompatible provider semantics + race conditions | **OPEN** | Yes (PR #3241) |
| **Medium** | [#3246] MQTT TLS certificates disabled by default (`InsecureSkipVerify: true`) | **OPEN** | Yes (PR #3246) |
| **Low** | [#3202] Agent/Account ID normalization strips leading/trailing underscores incorrectly | **OPEN** | Yes (PR #3202) |

**Key finding**: The OAuth race condition (#3239) and MQTT TLS bypass (#3246) represent **security vulnerabilities** that could affect production deployments. Both have correction PRs pending review.

## 6. Feature Requests & Roadmap Signals
- **QQ channel streaming** (#3201) — Strong candidate for next release given it aligns with existing streaming architecture on other channels. User adoption signal: QQ is a major platform for Chinese users.
- **WhatsApp native typing presence** (#3240 + PR #3242 by As-tsaqib) — Already implemented in PR; likely included in next release. Addresses UX gap on WhatsApp.
- **Simplex channel type** (PR #3193 by dim) — New channel integration for decentralized messaging; signals expanding platform support.
- **Installation scripts migration** (PR #1951 by lc6464, open since March) — Long-lived PR to move docs-repo scripts into main repo; may see resolution if maintainers merge for v0.3.2.

**Prediction for next release**: WhatsApp typing presence (PR #3242), OAuth hardening (PR #3241), MQTT TLS fix (PR #3246), and QQ streaming (#3201 if implemented) are likely.

## 7. User Feedback Summary
- **Pain points**:
  - Config migration breaking fresh installs (#3206) — frustrated newer users.
  - No real-time feedback on WhatsApp (#3240) — “Users see no feedback between sending a message and receiving the bot reply.”
  - OAuth refresh failures (#3239) — impacts multi-provider setups with OpenAI and Google.
- **Use cases**:
  - Multi-channel deployment (QQ, WhatsApp, Telegram, WebSocket).
  - Enterprise/production environments requiring secure TLS and reliable auth.
- **Satisfaction signals**: Multiple contributors (corporatepiyush, As-tsaqib) actively fixing security/performance issues indicates healthy contributor trust.

## 8. Backlog Watch
| Item | Age | Status | Concern |
|------|-----|--------|---------|
| [PR #1951] Move installation scripts from docs repo to here | 116 days open | OPEN | Stale since March; no recent maintainer activity. Risk of documentation drift. |
| [PR #3193] Added simplex channel type | 21 days open | OPEN | No comments from maintainers; new channel integrations need guidance or merge decisions. |
| [PR #3202] fix(routing): ID normalization | 17 days open | OPEN | Addresses a documented-but-not-enforced contract; low urgency but adds correctness. |

**Maintainer attention needed**: PR #1951 (installation scripts) is critical for new-user experience and should be resolved before next release. PR #3193 (Simplex channel) requires architectural review to avoid future API instability.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-18

## Today's Overview

NanoClaw shows strong engineering velocity today, with **15 pull requests** updated in the last 24 hours (3 closed/merged, 12 open) and **4 issues** active (3 open, 1 closed). The project is deep in a stabilization and bug-fix cycle, with particular focus on session routing correctness, rate-limit handling, and Discord/Matrix channel reliability. No new releases were shipped today. The high PR volume and the security-focused fixes indicate a mature project actively hardening its production surfaces.

## Releases

**No new releases** were published today. The last tagged release remains the v2 series (commit 2d9375531b, dated 2026-06-06, referenced in issue #3075).

## Project Progress

**Merged/closed PRs today (3):**

- **#3063** (docs) — `docs(changelog): drop duplicated Unreleased bullets` by glifocat. Cleaned up CHANGELOG.md after a merge left four bullets duplicated in the `## [Unreleased]` block. ✅ Merged
- **#2952** — `[follows-guidelines] Skill/add opencode stack` by javexed. Added an operational/container skill for the OpenCode stack. ✅ Closed/merged (2026-07-17)
- **#2951** — `[follows-guidelines] fix(opencode): dedicated OPENCODE_BASE_URL, read from .env, NO_PROXY …` by javexed. Fixed OpenCode skill configuration. ✅ Closed/merged (2026-07-17)

**Key feature advances in open PRs:**
- **#2999** / **#3076** — iMessage unification: Two complementary PRs by underthestars-zhy and invisicat aiming to unify iMessage into a single channel with local and hosted backends. The newer PR (#3076 by invisicat, opened yesterday) targets spectrum-ts v11 and may supersede or merge with #2999.
- **#3073** — `Adoption Companion pack` by jliurner: A utility skill adding "Memory Receipts + Knowledge Inventory" tools.

## Community Hot Topics

### Most Active Discussions

- **#3071** (CLOSED) — **Discord bare URLs delivered as markdown literal**  
  *Author: statico-alt | 1 comment | [Link](https://github.com/nanocoai/nanoclaw/issues/3071)*  
  A cleanly reported bug where bare URLs (`https://spacemolt.com`) are sent as `[url](url)` and unclickable in Discord. The Chat SDK Discord adapter is appending markdown to plain URLs where none was intended. This was **closed** — likely hotfixed or a known-duplicate.

- **#3075** (OPEN) — **Silent log loss + inbound message duplicates after long uptime**  
  *Author: libellebilai-collab | 0 comments | [Link](https://github.com/nanocoai/nanoclaw/issues/3075)*  
  Two linked issues in WSL2/Matrix deployment: (1) logs silently stop recording after ~days of uptime, (2) inbound messages get duplicate-inserted into the DB. The user notes no systemd unit is installed. This is the highest-urgency open issue today — zero comments suggests maintainers haven't triaged it yet.

- **#3074** (OPEN) — **Claude provider + OpenRouter: turns silently dropped**  
  *Author: apelosi | 0 comments | [Link](https://github.com/nanocoai/nanoclaw/issues/3074)*  
  When `ANTHROPIC_BASE_URL` points to OpenRouter, some turns are silently dropped because the SDK result event is empty despite a valid model reply. Likely a streaming deserialization edge case specific to OpenRouter's response format.

### Underlying Needs

All three open issues point to the same pattern: **the project needs better error-surfacing for non-standard provider configurations and edge-case deployments**. Users are finding silent failures (logs, dropped turns, duplicate messages) that don't crash the agent but degrade reliability.

## Bugs & Stability

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| 🔴 **Critical** | #3075 | Silent log loss + message duplicates on Matrix after long uptime. Could cause data integrity issues in production deployments. | No |
| 🔴 **Critical** | #3074 | Turns silently dropped when using Claude provider with OpenRouter. Loss of user input without error. | No |
| 🟡 **High** | #3071 (CLOSED) | Discord URLs unclickable — delivery formatting issue. | Closed, likely fixed |
| 🟢 **Medium** | #3072 | Docs only document slash-command skill invocation (`/name`) but Codex uses `$name` and CLI doesn't support slash syntax. | No |

**Bug-fix PRs in flight today:**
- **#3077** (fix/claude) — Only abort on *rejected* `rate_limit_event`, not `allowed` telemetry. Fixes #3016 where health checks were falsely failing.
- **#3078** (fix/session) — Pin agent-shared session resolution to an anchor session, preventing multi-session forks after wiring changes.
- **#3079** (fix/agent-runner) — Gate mid-turn follow-up push on trigger=1, preventing warm containers from responding to background noise.
- **#3080** (fix/add-matrix) — Replace `node_modules` edit with proper pnpm patch for `matrix-js-sdk` ESM fix.
- **#3081** (fix/agent-runner) — Route per-turn results by turn generation, not entry-frozen routing.
- **#3082** (test/uninstall) — Skip chmod-based backup-failure test when running as root (false failure in containers).
- **#3065** (fix/security) — Authenticate loopback webhook to prevent action forgery (CVE-type fix, GHSA-h9g4-589h-68xv).

## Feature Requests & Roadmap Signals

1. **iMessage unification** — Two overlapping PRs (#2999, #3076) signal strong community interest in a single, clean iMessage channel. Likely lands in next minor release.
2. **Adoption Companion pack** — #3073 adds memory and knowledge-inventory tracking tools; signals user demand for onboarding/documentation helpers.
3. **OpenCode stack skill** (#2952 merged) — Indicates growing interest in running NanoClaw with non-Claude coding assistants (Codex, OpenCode).
4. **Documentation gap for skill invocation** (#3072) — Users actively need docs that cover all three coding harnesses (Claude Code `/name`, Codex `$name`, CLI).

## User Feedback Summary

### Pain Points
- **Silent failures** are the #1 frustration: logs disappear, turns get dropped, messages are duplicated — all without any error to the user (issues #3074, #3075)
- **Discord formatting** breaks UX: agents can't share plain URLs (#3071)
- **Documentation is Claude-Code-centric** — users of Codex or other harnesses find the docs misleading (#3072)
- **Rate-limit false positives** (#3077 fix context previously, #3016) cause service health checks to fail for users of API providers

### Use Cases
- **Long-running production agents** on Matrix/Discord (issue #3075 user running WSL2 + Docker + Matrix)
- **Multi-provider deployments** using OpenRouter as a Claude backend (issue #3074)
- **Agent-shared rooms** where multiple agents share a single channel (PR #3078 fix context)

## Backlog Watch

- **#3075** (OPEN, 0 comments) — No maintainer response yet on a critical stability bug. Needs triage.
- **#3074** (OPEN, 0 comments) — No maintainer response on the OpenRouter turn-drop issue.
- **#3072** (OPEN, 0 comments) — Documentation gap that affects Codex users, no response.
- **#2999** (OPEN since July 10) — iMessage unification PR by underthestars-zhy, 7 days without merge, now potentially competing with #3076 (newer iMessage PR by invisicat). Maintainer direction needed to avoid duplication.
- **#3065** (OPEN, security fix) — CWE-306 loopback webhook vulnerability fix from QuantumBreakz. Should be prioritized for security.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-18

## 1. Today's Overview

NullClaw shows minimal activity over the past 24 hours, with no new releases, pull requests, or merges. The project has one active issue (#976) reporting a critical crash bug that affects Telegram gateway functionality on aarch64 Linux. This crash-loop scenario represents a significant stability concern for users relying on the Telegram integration, as every inbound message causes a segmentation fault and message loss. The maintainers have not yet responded with a fix or workaround, indicating the issue is still under investigation or awaiting triage. Overall, the project appears in a low-activity maintenance phase with a pressing stability bug unresolved.

## 2. Releases

No new releases were published in the last 24 hours. The latest available release remains **v2026.5.29**, which is the version affected by the critical bug described below.

## 3. Project Progress

No pull requests were updated, merged, or closed in the last 24 hours. No feature development or bug-fix progress was visible.

## 4. Community Hot Topics

The single active issue is drawing community attention:

- **#976 [OPEN] SIGSEGV on every inbound Telegram message** — Author: wonhotoss | Updated: 2026-07-17 | Comments: 2  
  URL: nullclaw/nullclaw Issue #976  
  This issue reports a consistent crash on aarch64 Linux when processing any inbound Telegram message. The root cause is identified as an inbound worker thread spawned with an insufficient stack size (~512 KB). The user describes a crash-loop scenario under `systemd Restart=always`, with every message causing a segfault and being dropped before reply. The underlying need is for a reliable Telegram gateway that can handle typical message workloads without crashing, which is a core expectation for any messaging bot or assistant.

## 5. Bugs & Stability

| Issue | Severity | Description | Fix PR Exists? | Status |
|-------|----------|-------------|----------------|--------|
| #976 | **Critical** | SIGSEGV on every inbound Telegram message on aarch64 Linux; thread stack overflow (512 KB insufficient). Causes crash-loop under systemd, message loss, and complete gateway unavailability. | No | Open, unassigned |

This bug is the highest-priority stability issue currently facing the project. The crash is deterministic and affects all Telegram functionality on the affected architecture. Without a fix, users on aarch64 cannot practically use NullClaw's Telegram gateway. The fix likely involves either increasing the default thread stack size (e.g., to 2 MB) or making it configurable.

## 6. Feature Requests & Roadmap Signals

No new feature requests were filed in the last 24 hours. However, issue #976 implicitly signals a need for:
- Better architecture-specific testing, particularly for aarch64 and ARM platforms.
- Configurable thread stack sizes or more generous default stack allocations.
- Hardening of the gateway worker spawning logic to prevent stack overflows under normal message loads.

Given the severity, a hotfix release (v2026.5.30 or similar) addressing the stack size is likely the next deliverable, rather than new features.

## 7. User Feedback Summary

The only user signal is from the reporter of #976, who is experiencing a complete inability to use the Telegram gateway on aarch64 Linux. The pain point is severe: the product is effectively broken for their use case. The user provided a detailed reproduction case and root cause analysis (insufficient stack size), indicating technical sophistication and a desire to help resolve the issue. Satisfaction is clearly very low, but the constructive reporting suggests the user is invested in the project and expects a fix.

## 8. Backlog Watch

- **Issue #976** — Critical, open since 2026-07-16, updated 2026-07-17, with no maintainer response or assignment. This is the most urgent item requiring maintainer attention. The issue is well-documented with a clear root cause, and a fix (increasing thread stack size) is straightforward. Prolonged silence risks user churn and negative reputation for the project's stability on ARM/aarch64 platforms.

No other long-unanswered issues or PRs were identified in the current data window.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-18

## 1. Today's Overview

IronClaw is in a high-velocity refactoring and stabilization phase ahead of the v1.0 release, with 50 issues and 50 PRs updated in the last 24 hours. The project is actively converging its "Reborn" architecture (the next-generation engine) through systematic store consolidation (§4.3), naming cleanup (§4.4), and binary renaming (`ironclaw-reborn` → `ironclaw`). A significant security vulnerability was closed—removing unrestricted filesystem access via shell commands on multi-tenant instances. The team shows strong operational discipline, closing 24 issues and merging/merging 26 PRs in a single day, with maintainer activity dominated by architectural simplification work from core contributors ilblackdragon and henrypark133.

## 2. Releases

**No new releases today.** The last tracked release activity is PR #5598 (still open), which proposes:
- `ironclaw_common`: 0.4.2 → 0.5.0 (⚠ API breaking changes)
- `ironclaw_skills`: 0.3.0 → 0.4.0 (⚠ API breaking changes)
- `ironclaw`: 0.24.0 → 0.29.1

This pending release has been open since July 3, suggesting the team is holding it until the current refactoring wave settles.

## 3. Project Progress

Today's merged/closed PRs (26 total) show intense architectural cleanup:

### Core Architectural Simplification (§4.3 Store Consolidation)
- **PR #6210** (merged) — [`refactor(reborn): budget-gate store over RootFilesystem, delete InMemoryBudgetGateStore`](https://github.com/nearai/ironclaw/pull/6210) — Deleted a hand-written in-memory store, consolidated onto production `FilesystemBudgetGateStore`.
- **PR #6209** (merged) — [`refactor(reborn): rename LocalFilesystem -> DiskFilesystem`](https://github.com/nearai/ironclaw/pull/6209) — Bucket 2 of §4.4 naming cleanup, removing ambiguous "Local" deployment-mode naming from storage backend.
- **PR #6207** (merged) — [`refactor(reborn): rename LocalTraceSubmission* -> NodeTraceSubmission*`](https://github.com/nearai/ironclaw/pull/6207) — Bucket 3 rename clarifying these are this-node's records, not a deployment tier.
- **PR #6206** (merged) — [`refactor(reborn): rename LocalHostProcessPort -> HostProcessPort`](https://github.com/nearai/ironclaw/pull/6206) — Trust-boundary clarifying rename for process port type.

### Channel & Integration
- **PR #6159** (merged) — [`feat(reborn): telegram channel extension — admin bot setup, WebGeneratedCode pairing, DM entrypoint`](https://github.com/nearai/ironclaw/pull/6159) — Major Telegram channel support for Reborn, including admin bot, per-user pairing via WebGeneratedCode, DM ingress, and triggered delivery. Includes video demo.
- **PR #6140** (merged) — [`feat(reborn): github.get_job_logs + SSRF-safe redirect egress`](https://github.com/nearai/ironclaw/pull/6140) — New first-party GitHub CI triage capability for Reborn agents, with SSRF protection.
- **PR #6217** (merged) — [`fix(reborn): compile Telegram host in production image`](https://github.com/nearai/ironclaw/pull/6217) — Ensures Telegram host is built into Docker production image.

### Bug Fixes & CLI
- **PR #6211** (open) — [`fix(reborn-cli): disable channels/hooks/logs stubs, fix models feature-gate stub`](https://github.com/nearai/ironclaw/pull/6211) — Stubs that printed fake-success output now return explicit "not implemented yet" errors.
- **Issue #6170** (closed) — **Security fix:** Removed unrestricted filesystem access via shell for multi-tenant instances.

### Dependency Updates
- **PR #6186** (open) — Bumps tokio ecosystem (tokio 1.52.3→1.53.0, tokio-tungstenite, etc.)
- **PR #6196** (open) — Bumps dompurify from 3.2.3 to 3.4.11 (security-focused JS dependency)

## 4. Community Hot Topics

Most active items (by comment count, all closed today):

1. **[Issue #2767](https://github.com/nearai/ironclaw/issues/2767)** (7 comments) — Epic for separating engine v2 capability background from callable tool schemas. Epic-level design discussion around how the v2 bridge/orchestrator/LLM surfacing path should be restructured. This represents the core architectural thinking driving current refactoring.

2. **[Issue #2813](https://github.com/nearai/ironclaw/issues/2813)** (6 comments) — Adding typed assistant content model for final vs internal tool-use text in engine v2. Addresses the problem of `LlmResponse::ActionCalls` flattening text too aggressively.

3. **[Issues #2835, #2834, #2838](https://github.com/nearai/ironclaw/issues/2835) et al.** (3 comments each) — A multi-PR enhancement series for tool discovery, compact action cards, and regression coverage. These are well-planned, low-to-medium risk improvements to engine v2 prompting infrastructure.

**Analysis:** The community's underlying need is clear: IronClaw v2 needs richer, more structured tool-use prompting (separating background capabilities from callable schemas, adding discovery summaries, rendering compact action cards) to match parity with systems like Claude Code. The team is methodically addressing this through a multi-PR plan with explicit risk assessment per PR.

## 5. Bugs & Stability

### Critical
- **[Issue #6170](https://github.com/nearai/ironclaw/issues/6170) (CLOSED)** — **Security: Unrestricted filesystem access via shell on multi-tenant instances.** Users could execute `ls -all` unbounded to their workspace. Fixed in today's activity. **Severity: Critical** — immediate access to host filesystem in multi-tenant deployment.

### High
- **[Issue #6215](https://github.com/nearai/ironclaw/issues/6215) (OPEN)** — **Regression: Model cost table not rebuilt by LLM reload chokepoint** after PR #6174. The boot convergence change (`RebornLlmReloadAdapter::reload()`) broke re-initialization of the budget accountant. **Severity: High** — affects budget tracking for all LLM usage.
- **[Issue #5331](https://github.com/nearai/ironclaw/issues/5331) (CLOSED)** — **Tool-approval 'always' may not auto-approve next same-tool call.** First approval works; second fails. Medium confidence product bug affecting user workflow.

### Medium
- **[Issue #4278](https://github.com/nearai/ironclaw/issues/4278) (CLOSED)** — Potential performance issue: unbounded conversation growth in ENGINE_V2 causing context window exhaustion. All messages stored as single JSON blob in `memory_documents` table.
- **[Issue #3465](https://github.com/nearai/ironclaw/issues/3465) (CLOSED)** — ENGINE_V2 repeatedly calls `tool_info(schema)` during tool-use flows, especially around image generation.
- **[Issue #3464](https://github.com/nearai/ironclaw/issues/3464) (CLOSED)** — Failed tool calls render inconsistently in Gateway UI under ENGINE_V2.
- **[Issue #3618](https://github.com/nearai/ironclaw/issues/3618) (CLOSED)** — Debug panel stats stuck at 0 on engine v2 (only Tool Calls updates).
- **[Issue #3463](https://github.com/nearai/ironclaw/issues/3463) (CLOSED)** — Engine V2 generated images do not render correctly in Gateway UI.

## 6. Feature Requests & Roadmap Signals

### Likely in Next Release
1. **Telegram channel for Reborn** — PR #6159 (merged), PR #6217 (merged), tracked by Issue #5124 (closed). Telegram is now a production-supported channel for Reborn. **Prediction: Ships in v0.30+.**

2. **GitHub CI triage for Reborn agents** — PR #6140 (merged). First-party `github.get_job_logs` capability with SSRF-safe redirect. **Prediction: Ships in v0.30+.**

3. **Reborn onboarding CLI** — PR #6174 (open, XL size). Complete onboarding journey: keychain → model setup → login link → background service → browser. Makes Reborn usable standalone from source build.

### Under Active Development
4. **Binary rename** — PR #6185 (open, L size): `ironclaw-reborn` → `ironclaw`, legacy → `ironclaw-v1`. Issue #6201 tracks follow-up crate renames. Signals that v1.0 is approaching.

5. **Task attachment pipeline** — Issue #4644 (open). Universal attachments across all channels for Reborn. Currently dropped on Reborn; format support logic duplicated across 4+ call sites.

### In Design/Planning
6. **Engine v2 tool-use prompting overhaul** — Issues #2834-2838 (all closed). A series of enhancements: discovery-guided prompting, compact action cards, prompt hints metadata. Already merged/landed.

7. **Context budget broker** — Issue #2399 (closed). Framework for managing memory, skills, transcript, and action budgets.

## 7. User Feedback Summary

### Real Pain Points Addressed
- **Security**: Multi-tenant filesystem access via shell (Issue #6170, closed) — a critical vulnerability users could exploit on hosted instances.
- **Telegram channel support**: Requested via Issue #5124 — now merged with admin bot, pairing workflow, and DM support.
- **Tool approval flakiness**: Issue #5331 (closed) — "always" auto-approve not working consistently for same-tool calls.

### Unresolved User Pain Points
- **Engine v2 UI regressions**: Multiple bugs in Gateway UI (Issues #3463, #3464, #3465, #3618 — all closed) around image rendering, tool call display, and debug stats — users on engine v2 have degraded visual feedback.
- **Context window exhaustion**: Issue #4278 (closed) — the memory storage design stores entire conversation history as a single JSON blob, creating unbounded growth. This directly impacts real users with long sessions.
- **LLM usage tracking gap**: Issue #4822 (closed) — admin usage APIs don't track Engine V2 LLM calls, making per-user billing/auditing incomplete for Reborn users.
- **Failed tool calls rendering**: Issue #3464 — inconsistent failure state display confuses users about whether operations succeeded.

### Satisfaction Signals
- High velocity of issue closure (24 closed today) indicates responsive maintenance.
- Multiple engine v2 quality issues from May (Issues #3463-3465) are now closed, showing the team is systematically addressing the UI/UX regressions introduced by the engine v2 migration.
- The §4.3/4.4 refactoring series shows deep investment in code quality, which should reduce future bugs and improve maintainability.

## 8. Backlog Watch

### Important Open Issues Needing Attention
1. **[Issue #4644](https://github.com/nearai/ironclaw/issues/4644)** — Universal attachments for Reborn (open since June 9, ~6 weeks). Labeled `suggested_P1` and `reborn`. Attachments are silently dropped on Reborn; format logic duplicated across 4+ call sites. With Reborn becoming the default (PR #6185), this is a growing gap.

2. **[Issue #3577](https://github.com/nearai/ironclaw/issues/3577)** — Track v1 channel ports for Reborn (open since May 13, ~9 weeks). Labeled `suggested_P2`. The classification guide exists but channel porting progress is untracked.

3. **[Issue #5219](https://github.com/nearai/ironclaw/issues/5219)** — Harden activity identity invariants after gate lifecycle refactor (open since June 25, ~3 weeks). Follow-up from PR #5145, tagged as part of the gate lifecycle work.

### Stale/Non-Urgent
4. **[Issue #6198](https://github.com/nearai/ironclaw/issues/6198)** — The "Pre-v1 refactoring & legacy cleanup" epic (open since yesterday). This is the human-readable roadmap for all refactoring work before v1.0 release — actively managed, not stale.

### Risk Signal
The §4.3 store consolidation is aggressively deleting in-memory stores in favor of filesystem-based implementations. While this unifies the codebase, the `FROZEN_INMEMORY_STORES` list (noted in PR #6216) suggests some items are blocked on non-mechanical work — any missed case could introduce regressions in state persistence or test isolation.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-18

## 1. Today's Overview
LobsterAI shows strong and mature development velocity today, with **15 PRs updated in the last 24 hours**, of which **13 were merged or closed** — a healthy 87% closure rate. The project released version **2026.7.16** yesterday and appears to be preparing a **2026.7.17 release** (PR #2356 merged today). Only **2 issues remain open**, both from April, indicating the team has been actively clearing backlog. Activity is concentrated on UI polish, cowork stability improvements, and a major new **AI-generated skin experience** feature. The project remains in a feature-forward phase with disciplined maintenance.

## 2. Releases
**New Release: [LobsterAI 2026.7.16](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.7.16)** (published 2026-07-16)

**What's Changed:**
- `refactor(cowork)`: Extracted clipboard attachment file extraction into a testable helper (PR [#2343](https://github.com/netease-youdao/LobsterAI/pull/2343))
- `feat`: Added campaign final reward claim feature (commit `6eafb`)

**Breaking Changes:** None identified. The release is incremental with no migration notes required.

**Note:** A subsequent release branch `Release/2026.7.17` (PR [#2356](https://github.com/netease-youdao/LobsterAI/pull/2356)) was merged today, suggesting a follow-up release is imminent.

## 3. Project Progress
The following significant changes were merged in today's 13 closed PRs:

**New Features:**
- **[AI-Generated App Skin Experience](https://github.com/netease-youdao/LobsterAI/pull/2352)** (PR #2352): Adds a full AI-generated skin-pack workflow, reusable skin management (apply, restore, reapply, delete), light/dark appearance preference, and immersive skin presentation across sidebar, title bars, and conversations.
- **[Structured Run Failure Details](https://github.com/netease-youdao/LobsterAI/pull/2348)** (PR #2348): Adds `CoworkErrorDetail` structure visible in the assistant turn UI so users can expand technical details (provider, model, HTTP code, error type) on failed runs.
- **[Service Deployment Data Persistence](https://github.com/netease-youdao/LobsterAI/pull/2349)** (PR #2349): Implements persistence for service deployment configurations.

**Fixes & Improvements:**
- **[Artifact Panel Layout Stability](https://github.com/netease-youdao/LobsterAI/pull/2357)** (PR #2357): Prevents preview subtree rebuilds on panel toggle; syncs input area height to reduce flickering.
- **[OpenClaw Stale Chat Fix](https://github.com/netease-youdao/LobsterAI/pull/2354)** (PR #2354): Ignores stale chat errors after successful deferred final in OpenClaw.
- **[Windows Caption Alignment](https://github.com/netease-youdao/LobsterAI/pull/2355)** (PR #2355): Matches minimize/maximize hover colors with sidebar controls.
- **[Email Diagnostics in New Chat](https://github.com/netease-youdao/LobsterAI/pull/2346)** (PR #2346): Prevents stale history from overriding new email diagnostic chats.
- **[Update Check Interval](https://github.com/netease-youdao/LobsterAI/pull/2347)** (PR #2347): Reduced from 12h to 2h for faster notification of updates.
- **[NSIS Installer Fix](https://github.com/netease-youdao/LobsterAI/pull/2345)** (PR #2345): Localized download prompts and fixed progress bar overlap.

**Chores & Polish:**
- Main UI update (PR [#2353](https://github.com/netease-youdao/LobsterAI/pull/2353))
- Windows caption icon refinement (PR [#2351](https://github.com/netease-youdao/LobsterAI/pull/2351))
- Sidebar ad banner optimization (PR [#2350](https://github.com/netease-youdao/LobsterAI/pull/2350))

## 4. Community Hot Topics
All 7 issues updated today are **3+ months old** (created April 2) and were closed today as stale, indicating the community activity was lower on new discussions. However, the following items attracted attention:

| Issue | Comments | Summary |
|-------|----------|---------|
| [#1354](https://github.com/netease-youdao/LobsterAI/issues/1354) | 3 | BSOD when launching Pageant via LobsterAI |
| [#1357](https://github.com/netease-youdao/LobsterAI/issues/1357) | 2 | "Enable Pageant" reports success but doesn't start |
| [#1358](https://github.com/netease-youdao/LobsterAI/issues/1358) | 2 | Scheduled tasks show no interaction feedback |
| [#1359](https://github.com/netease-youdao/LobsterAI/issues/1359) | 2 | Deleted tasks reappear after restart |
| [#1360](https://github.com/netease-youdao/LobsterAI/issues/1360) | 2 | No duplicate name validation for custom agents |

**Underlying needs:** Users are expressing frustration around **reliability of system-level operations** (Pageant launching) and **UI feedback clarity** (task status, persistence). The common thread is a desire for transparent, predictable system interaction.

The two **still-open issues** — [#1311](https://github.com/netease-youdao/LobsterAI/issues/1311) (table rendering with raw tags + truncated text) and [#1314](https://github.com/netease-youdao/LobsterAI/issues/1314) (sidebar drag-to-resize) — both have open PRs ([#1315](https://github.com/netease-youdao/LobsterAI/pull/1315)) and represent long-standing UI quality-of-life requests.

Two open PRs remain: [#1308](https://github.com/netease-youdao/LobsterAI/pull/1308) (input draft isolation per agent) and [#1315](https://github.com/netease-youdao/LobsterAI/pull/1315) (sidebar resize), both from April 2.

## 5. Bugs & Stability
**No new bugs were reported today.** All 7 updated issues were closed as stale — none are from the last 24 hours. This is a positive signal for current stability.

**Historical high-severity bugs (all closed today):**
- **[CRITICAL] [#1354](https://github.com/netease-youdao/LobsterAI/issues/1354)** — BSOD when launching Pageant (stale)
- **[HIGH] [#1357](https://github.com/netease-youdao/LobsterAI/issues/1357)** — Pageant launch false positive (stale)
- **[MEDIUM] [#1359](https://github.com/netease-youdao/LobsterAI/issues/1359)** — Task deletion not persisted (stale)

**New fixes merged today** that improve stability:
- OpenClaw stale chat error ignore (PR [#2354](https://github.com/netease-youdao/LobsterAI/pull/2354))
- Artifact panel layout flicker fix (PR [#2357](https://github.com/netease-youdao/LobsterAI/pull/2357))
- NSIS installer progress bar overlap fix (PR [#2345](https://github.com/netease-youdao/LobsterAI/pull/2345))
- Email diagnostic session isolation (PR [#2346](https://github.com/netease-youdao/LobsterAI/pull/2346))

**No regressions** were identified.

## 6. Feature Requests & Roadmap Signals
**Likely for next version (based on merged PRs):**
1. **AI-Generated Skins** (PR [#2352](https://github.com/netease-youdao/LobsterAI/pull/2352)) — Almost certainly part of the upcoming 2026.7.17 release. This is a major visual customization feature.
2. **Service Deployment Persistence** (PR [#2349](https://github.com/netease-youdao/LobsterAI/pull/2349)) — Enables saving service deployment configurations across sessions.

**Pending user-requested features (open, with PR):**
3. **[Sidebar Drag-to-Resize](https://github.com/netease-youdao/LobsterAI/issues/1314)** (Issue #1314, PR [#1315](https://github.com/netease-youdao/LobsterAI/pull/1315)) — User-requested quality-of-life improvement, open since April. Could land in next minor release.
4. **[Input Draft Per-Agent](https://github.com/netease-youdao/LobsterAI/pull/1308)** (PR #1308) — For users managing multiple agents, prevents cross-contamination in input state. Also open since April.

**Roadmap signals:** The team appears to be investing in:
- **Visual customization** (skins, window controls, sidebar banners)
- **Reliability at scale** (persistence, error detail surfacing, update notifications)
- **Cowork/OpenClaw stability** (failure details, chat state management)

## 7. User Feedback Summary
**Pain Points (historical, now stale-closed):**
- **System automation reliability:** Users report Pageant launching crashes (BSOD) or false successes — critical for trust in system-level operations.
- **Task management confusion:** Deleted tasks reappearing after restart, scheduled tasks lacking visual feedback — undermines confidence in automation.
- **Agent creation UX:** No duplicate name validation for custom agents — minor but indicative of edge-case gaps.

**Positive Signal:** No new complaints were raised in the last 24 hours, and all 5 historical bugs were formally closed today, suggesting either resolution or acceptable workarounds.

**Satisfaction Indicator:** The project maintains stable output with multiple features and fixes per day, and the UI polish (skins, window controls, banners) suggests attention to user delight.

## 8. Backlog Watch
**Long-unanswered, still open:**

| Item | Type | Created | Last Updated | Days Stale | Risk |
|------|------|---------|--------------|------------|------|
| [#1311](https://github.com/netease-youdao/LobsterAI/issues/1311) — Table rendering with raw tags + truncated text hover | Issue | 2026-04-02 | 2026-07-17 | ~107 | MEDIUM — UI polish, may be deprioritized |
| [#1314](https://github.com/netease-youdao/LobsterAI/issues/1314) — Sidebar drag-to-resize | Issue | 2026-04-02 | 2026-07-17 | ~107 | LOW — has companion PR #1315 |
| [#1308](https://github.com/netease-youdao/LobsterAI/pull/1308) — Input draft per-agent | PR | 2026-04-02 | 2026-07-17 | ~107 | MEDIUM — functional improvement, no maintainer response |
| [#1315](https://github.com/netease-youdao/LobsterAI/pull/1315) — Sidebar resize implementation | PR | 2026-04-02 | 2026-07-17 | ~107 | LOW — pending review |

**All backlog items are UI/UX improvements**, not critical bugs. No maintainer action was taken on them today. Given the team's focus on releases and new features (skins, persistence), these may be addressed in a future UI-focused minor release.

**No security or high-severity items** are languishing in the backlog.

---

*Generated based on GitHub data from [netease-youdao/LobsterAI](https://github.com/netease-youdao/LobsterAI), snapshot date 2026-07-18.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-18

## 1. Today's Overview
Moltis shows low activity over the past 24 hours, with only 1 issue update and 2 pull requests opened—none merged or closed. Two new patch releases (20260717.02 and 20260717.03) were published, suggesting ongoing minor maintenance or hotfix work. The single active issue is an enhancement request from April that received a new comment today, while both open PRs are fresh, unmerged contributions. Overall project momentum appears moderate, with development focused on experimental backends and UI fixes rather than major milestones.

## 2. Releases
Two new releases were published today, both dated 2026-07-17:
- **20260717.02** — No changelog or migration notes provided in the data; likely a minor patch.
- **20260717.03** — Similarly undocumented; likely a subsequent hotfix or small feature release.

**No breaking changes or migration notes were reported.** Users should refer to the [releases page](https://github.com/moltis-org/moltis/releases) for exact commit logs.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. Two new open PRs were created:
- **PR #1158** ([link](https://github.com/moltis-org/moltis/pull/1158)): `feat(memory): add zvec vector database memory backend` — An experimental alternative memory backend using Zvec and redb, gated behind a cargo feature. This is described by the author as a "vibe-coded" setup, indicating exploratory development.
- **PR #1157** ([link](https://github.com/moltis-org/moltis/pull/1157)): `fix(web): support ACP-only chat setup` — Fixes the onboarding flow to recognize ACP-only configurations (no LLM models) as valid, improves agent selection in session pickers, and disables model controls when no LLM is configured.

Both PRs remain unmerged; no fixes or features were finalized today.

## 4. Community Hot Topics
The most active item is **Issue #574** ([link](https://github.com/moltis-org/moltis/issues/574)): **"[Feature]: Model Routing Per topic"** — Opened on 2026-04-06, updated today with 3 comments and 1 reaction. The feature request asks for the ability to route different conversation topics to different AI models, suggesting users want finer-grained control over model selection based on context. The underlying need is likely improved efficiency (e.g., using cheaper/smaller models for simple queries and more capable models for complex topics), as well as potential cost and latency optimization for multi-model setups.

No other issues or PRs had significant comments or reactions.

## 5. Bugs & Stability
No new bug reports, crashes, or regressions were filed in the last 24 hours. The only issue updated today is an enhancement request, not a defect. The project appears stable, with no urgent stability concerns reported.

## 6. Feature Requests & Roadmap Signals
- **Model Routing Per Topic** (Issue #574) — The sole feature request active today could align with Moltis’s emphasis on flexible AI agent orchestration. If implemented, it would allow dynamic model switching per conversation segment.
- **ACP-only setup support** (PR #1157) — Indicates the project is actively improving support for Agent Communication Protocol (ACP) agents without requiring an LLM, possibly expanding use cases for non-LLM agent integrations.
- **Zvec memory backend** (PR #1158) — An experimental vector database backend suggests interest in alternative memory stores, though this PR is currently a personal experiment and may not be prioritized for next release.

**Prediction**: The ACP-only fix (PR #1157) is small, low-risk, and likely to be merged in the next minor release. The model routing feature (Issue #574) is more complex and may appear in a future major/minor release if community interest grows.

## 7. User Feedback Summary
- **Positive signals**: The ACP-only fix (PR #1157) addresses a pain point for users who want to use external agents without an LLM backend, indicating satisfaction with the ACP ecosystem.
- **Requests**: The model routing feature suggests some users find the current all-or-nothing model assignment limiting and want granular control.
- **No explicit dissatisfaction** was expressed in the data; comments are neutral/constructive.

## 8. Backlog Watch
- **Issue #574** ([link](https://github.com/moltis-org/moltis/issues/574)) — Open since April 6, 2026 (over 3 months), with only 3 comments and 1 reaction. While not extremely high-traffic, the lack of maintainer response or assignment could indicate it is low priority or awaiting clearer specification. It may need a maintainer triage comment to confirm whether it is under consideration.

No other long-unanswered important items were identified in the data.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-18

Generated from GitHub data for **CoPaw** (github.com/agentscope-ai/CoPaw) — AI agent & personal assistant platform.

---

## 1. Today's Overview

CoPaw remains in a high-velocity development phase, with **42 PRs updated** (25 merged/closed) and **25 issues updated** (10 closed) in the last 24 hours. A patch release **v2.0.0.post3** shipped today, primarily addressing MCP driver credential migration and CI hardening. Community engagement is strong, with multiple bug reports around Windows permission elevation and MCP startup performance drawing maintainer attention. The project shows sustained maturity efforts: graceful shutdown, asset caching, and multi-agent startup bounding are all seeing fix PRs. There is a notable influx of feature requests from a single contributor (Hazemaan) proposing per-chat tool control, reasoning depth selection, and Hermes model support — signalling growing power-user expectations.

---

## 2. Releases

### v2.0.0.post3 (released 2026-07-17)

**What's Changed:**
- **fix(mcp):** Migrate `${VAR}` headers to env credential refs during driver migration ([PR #6091](https://github.com/agentscope-ai/QwenPaw/pull/6091))
- **refactor(ci):** Harden desktop workflows and drop legacy verify dead code ([PR #6098](https://github.com/agentscope-ai/QwenPaw/pull/6098))

**Migration Notes:**
No breaking changes. Users on v2.0.0.post2 can upgrade via `pip install --upgrade qwenpaw`. The MCP fix addresses a variable interpolation issue during driver migration — no manual action required.

**Verification:** A release-duty issue ([#6223](https://github.com/agentscope-ai/QwenPaw/issues/6223)) is tracking installation verification across platforms.

---

## 3. Project Progress

**Key PRs merged/closed today (highlights):**

| PR | Description | Status |
|----|-------------|--------|
| [#6234](https://github.com/agentscope-ai/QwenPaw/pull/6234) | fix: use absolute import in Tauri entry point (Windows sandbox) | Merged |
| [#6220](https://github.com/agentscope-ai/QwenPaw/pull/6220) | fix(token_usage): don't persist unseeded cache on shutdown | Merged |
| [#6218](https://github.com/agentscope-ai/QwenPaw/pull/6218) | fix(runtime): pass `model_slot_override` from HTTP request to model factory | Merged |
| [#6217](https://github.com/agentscope-ai/QwenPaw/pull/6217) | fix: treat unprobed multimodal as fail-open (prevent image stripping) | Merged |
| [#6204](https://github.com/agentscope-ai/QwenPaw/pull/6204) | fix(utils): drop redundant nvidia-smi probe in `get_vram_size_gb` | Merged |
| [#6198](https://github.com/agentscope-ai/QwenPaw/pull/6198) | feat: bound multi-agent startup and improve readiness UX | Merged |
| [#6170](https://github.com/agentscope-ai/QwenPaw/pull/6170) | fix(browser): add MAX_WAITTIME for browser use | Merged |
| [#6159](https://github.com/agentscope-ai/QwenPaw/pull/6159) | Refactor channel base (move turn usage settlement to BaseChannel) | Merged |

**Open but active PRs (progressing):**
- [#6237](https://github.com/agentscope-ai/QwenPaw/pull/6237) — feat(scroll): improve exchange and date-aware history recall
- [#6232](https://github.com/agentscope-ai/QwenPaw/pull/6232) — perf(console): cache and compress static assets
- [#6235](https://github.com/agentscope-ai/QwenPaw/pull/6235) — [WIP] feat(memory): add manual memory index rebuild for ReMe Light
- [#6225](https://github.com/agentscope-ai/QwenPaw/pull/6225) — fix(desktop): gracefully shut down backend sidecar

---

## 4. Community Hot Topics

### Most Active Issues

| Issue | Comments | Summary |
|-------|----------|---------|
| [#6161](https://github.com/agentscope-ai/QwenPaw/issues/6161) [CLOSED] | 7 | Windows update breaks normal-user startup — requires Admin |
| [#5995](https://github.com/agentscope-ai/QwenPaw/issues/5995) | 6 | Messages silently dropped when session is busy (Feishu channel) |
| [#6155](https://github.com/agentscope-ai/QwenPaw/issues/6155) | 5 | v1.x → v2.0 upgrade breaks: embedding mapping, auto-memo, system prompt |
| [#6221](https://github.com/agentscope-ai/QwenPaw/issues/6221) | 5 | Test notification bot (infrastructure) |
| [#5976](https://github.com/agentscope-ai/QwenPaw/issues/5976) | 4 | Feature request: separate control for tool call vs. result visibility |
| [#6193](https://github.com/agentscope-ai/QwenPaw/issues/6193) | 3 | MCP drivers start sequentially — 8× slowdown |

**Analysis:**
- **Windows permissions** dominate community pain: #6161 and #6169 both report forced admin requirements post-update. The v2.0.0.post3 release does not mention a fix for this — it remains a critical UX blocker for Windows users.
- **Message loss (#5995)** in busy sessions is a reliability issue affecting Feishu channel users — no fix PR visible yet.
- **MCP startup performance (#6193)** is generating strong interest; a fix via concurrent initialization is described but not yet addressed in merged PRs.
- **Feature requests** around channel tool-result truncation (#5976) and multi-config model IDs (#6231) reflect real usability friction for power users.

---

## 5. Bugs & Stability

### High Severity

1. **Windows: Normal users cannot start after update** — [#6161](https://github.com/agentscope-ai/QwenPaw/issues/6161) (CLOSED as invalid? needs verification) + [#6169](https://github.com/agentscope-ai/QwenPaw/issues/6169) (CLOSED as duplicate)
   - Impact: Blocks all Windows non-admin users. Workaround: Run as Administrator.
   - Fix status: Marked duplicate/closed. No fix PR identified. **⚠️ Recurrence risk high.**

2. **Message silently dropped on busy session** — [#5995](https://github.com/agentscope-ai/QwenPaw/issues/5995) (OPEN)
   - Impact: Data loss in Feishu/multi-step workflows. No queue mechanism.
   - Fix status: No linked PR. **Unresolved.**

3. **v1.x → v2.0 upgrade regression** — [#6155](https://github.com/agentscope-ai/QwenPaw/issues/6155) (OPEN)
   - Impact: Embedding mapping broken, auto-memo fails, system prompt changes break custom agents.
   - Fix status: Unresolved. No PR linked.

4. **MCP model crashes llama.cpp** — [#6201](https://github.com/agentscope-ai/QwenPaw/issues/6201) (CLOSED)
   - Diagnosis: PubMed MCP causes local model crash. Closed without visible fix.

### Medium Severity

5. **Desktop force-kills backend instead of graceful shutdown** — [#6219](https://github.com/agentscope-ai/QwenPaw/issues/6219) (OPEN)
   - **Fix PR exists:** [#6225](https://github.com/agentscope-ai/QwenPaw/pull/6225) — "gracefully shut down backend sidecar before exit" (OPEN)
   - Expected in next patch.

6. **Windows `file:///` media path corrupted on history replay** — [#5934](https://github.com/agentscope-ai/QwenPaw/issues/5934) (CLOSED)
   - Impact: Local media fails on Windows during conversation replay. Closed, fix assumed in v2.0.0.post3.

### Low Severity / Other

7. **Web UI not displaying channel messages** — [#6003](https://github.com/agentscope-ai/QwenPaw/issues/6003) (CLOSED)
8. **Desktop skill navigation progressive rendering broken** — [#6202](https://github.com/agentscope-ai/QwenPaw/issues/6202) (CLOSED as duplicate)

---

## 6. Feature Requests & Roadmap Signals

### New Today (most actionable)

| Issue | Proposal | Likelihood for Next Release |
|-------|----------|----------------------------|
| [#6231](https://github.com/agentscope-ai/QwenPaw/issues/6231) | Same model ID with different configs (e.g., thinking on/off) | Medium — config flexibility is highly requested |
| [#6229](https://github.com/agentscope-ai/QwenPaw/issues/6229) | Reasoning depth selection (Light/Medium/Deep/Auto) | Medium — intersects with model slot config work |
| [#6228](https://github.com/agentscope-ai/QwenPaw/issues/6228) | Per-chat internet search toggle | Medium-low — nice UX addition |
| [#6227](https://github.com/agentscope-ai/QwenPaw/issues/6227) | Per-chat MCP server & tool-level control | Medium — aligns with MCP scaling work |
| [#6230](https://github.com/agentscope-ai/QwenPaw/issues/6230) | Hermes model family support as secondary reasoning engine | Low — niche model support |
| [#6222](https://github.com/agentscope-ai/QwenPaw/issues/6222) | Clarify MEMORY.md vs Dream digest roles | Documentation — likely addressed soon |
| [#6205](https://github.com/agentscope-ai/QwenPaw/issues/6205) | Compress & cache console JS assets | **High — fix PR exists** [#6232](https://github.com/agentscope-ai/QwenPaw/pull/6232) (OPEN) |

### Earlier Requests Still Open

- [#5976](https://github.com/agentscope-ai/QwenPaw/issues/5976) — Separate tool call/result display in channels → **Fix PR exists** [#6233](https://github.com/agentscope-ai/QwenPaw/pull/6233) (OPEN)
- [#5919](https://github.com/agentscope-ai/QwenPaw/issues/5919) — Global runtime configuration — no PRs yet
- [#6162](https://github.com/agentscope-ai/QwenPaw/issues/6162) — Auto-read `max_input_length` from model API — closed as question

**Prediction:** The next minor release (v2.0.1 or v2.1.0) will likely include:
- Graceful desktop shutdown (#6225)
- Console asset caching/compression (#6232)
- Channel tool message display controls (#6233)
- Bounded multi-agent startup (#6198, already merged)
- Scroll history recall improvements (#6237)

---

## 7. User Feedback Summary

### Pain Points (recurring themes)

| Theme | Evidence | Severity |
|-------|----------|----------|
| **Windows admin requirement** | #6161, #6169, #6161 (7 comments) | **Critical** — blocks all non-admin users |
| **Upgrade regressions (1.x→2.0)** | #6155 (5 comments) | **High** — breaks embedding, auto-memo, system prompts |
| **Message loss on busy sessions** | #5995 (6 comments) | **High** — data loss in production use |
| **MCP startup slow** | #6193 (3 comments) | **Medium** — 8× slowdown with 8 MCPs |
| **Console slow on low bandwidth** | #6205 (3 comments) | **Medium** — UX friction for remote hosting |

### Satisfaction Signals

- **Competing requests for refinement** (per-chat controls, reasoning depth, model config flexibility) indicate users are actively *using* the platform at scale and want more granular control.
- Multiple first-time contributors ([Yigtwxx](https://github.com/Yigtwxx), [qbc2016](https://github.com/qbc2016)) submitted clean, accepted bug fixes — healthy community onboarding.

### English-Language Community Notes

Issues #5995, #6227–#6230 are in English, suggesting a growing international user base beyond Chinese-speaking users. The platform's English documentation and support responsiveness is indirectly being tested.

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Reason |
|-------|-----|--------|
| [#5995](https://github.com/agentscope-ai/QwenPaw/issues/5995) — Messages dropped when session busy | 5 days | High impact, no fix PR, no maintainer response since created |
| [#6155](https://github.com/agentscope-ai/QwenPaw/issues/6155) — v1.x→v2.0 upgrade regression | 2 days | Multiple regressions bundled, no maintainer confirmation of reproducibility |
| [#5919](https://github.com/agentscope-ai/QwenPaw/issues/5919) — Global runtime config | 7 days | Low activity, feature request from veteran user |
| [#5698](https://github.com/agentscope-ai/QwenPaw/pull/5698) — feat(tools): `run_tool_batch` for AgentScope 2.0 | **16 days** | Long-open PR with control-flow additions — may need review |
| [#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187) — Windows desktop GUI automation | **34 days** | Large feature PR (computer_use for Windows), possibly blocked by scope |

### Open PRs Needing Review

| PR | Age | Notes |
|----|-----|-------|
| [#6237](https://github.com/agentscope-ai/QwenPaw/pull/6237) — Scroll history recall | 0 days | Fresh, author: niceIrene |
| [#6235](https://github.com/agentscope-ai/QwenPaw/pull/6235) — Manual memory reindex | 0 days | WIP, author: jinliyl |
| [#6232](https://github.com/agentscope-ai/QwenPaw/pull/6232) — Console asset caching | 0 days | Fresh, author: fancyboi999 |
| [#6225](https://github.com/agentscope-ai/QwenPaw/pull/6225) — Graceful desktop shutdown | 0 days | **Critical fix** for #6219 |
| [#6210](https://github.com/agentscope-ai/QwenPaw/pull/6210) — Default loop as agent mode | 0 days | Major refactor — may need careful review |
| [#6151](https://github.com/agentscope-ai/QwenPaw/pull/6151) — Background tool call offload | 2 days | Dual-deadline architecture, fixes #6056 |
| [#5698](https://github.com/agentscope-ai/QwenPaw/pull/5698) — run_tool_batch AgentScope 2.0 | **16 days** | Stale, needs review |
| [#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187) — Windows computer_use | **34 days** | Longest open PR, likely complex |

---

*Generated from CoPaw GitHub data snapshot 2026-07-18. All links reference the `agentscope-ai/QwenPaw` repository.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

**ZeptoClaw Project Digest — 2026-07-18**

---

### 1. Today's Overview
The ZeptoClaw project saw a focused, low-activity day on 2026-07-18, with eight issues closed in the last 24 hours and no associated pull requests or new releases. All activity was concentrated on D5 gate-point metadata updates for security vulnerability analysis, reflecting a stable, maintenance-oriented workflow rather than active feature development. The closure rate is high relative to open activity, indicating efficient issue triage, though the absence of open PRs suggests the development cycle is currently in a consolidation phase.

---

### 2. Releases
No new releases were published today. The repository has no recent version tags or release artifacts.

---

### 3. Project Progress
No pull requests were merged or closed today. All project progress was captured via issue closures, which advanced the D5 gate-point data maintenance pipeline. The eight closed issues each performed targeted updates to CSV rows 34–38 of the `all-exist-vuls-d5-gate-point-type-missing-data-collect.csv` file, refreshing `d5_gate_points` and `d5_cross_component` fields for corresponding security issues (IDs: 263, 264, 268, 329, 466). This work is entirely analytical/non-code.

**Key items completed:**
- [#636 chore(analysis): update D5 gate data for Issue-zeptoclaw-263 row 34](https://github.com/qhkm/zeptoclaw/issues/636)
- [#637 chore(analysis): update D5 gate data for Issue-zeptoclaw-264 row 35](https://github.com/qhkm/zeptoclaw/issues/637)
- [#638 chore(analysis): update D5 gate data for Issue-zeptoclaw-268 row 36](https://github.com/qhkm/zeptoclaw/issues/638)
- [#639 chore(analysis): update D5 gate data for Issue-zeptoclaw-329 row 37](https://github.com/qhkm/zeptoclaw/issues/639)
- [#640 chore(analysis): update D5 gate data for Issue-zeptoclaw-466 row 38](https://github.com/qhkm/zeptoclaw/issues/640)

Three additional `llm-enhance` labeled issues (#641, #642, #643) performed the same type of metadata refresh with a more specific scope remark.

---

### 4. Community Hot Topics
No issues or PRs generated more than 1 comment or any reactions today. The most commented issues (all 1 comment each) were the eight D5 gate update tasks. This suggests the community is either highly aligned on the current workflow or engagement is limited to a small operational team. There were no open discussions, feature debates, or user interactions to highlight.

---

### 5. Bugs & Stability
No bugs, crashes, or regressions were reported today. The eight closed issues dealt exclusively with data completeness rather than defects. Stability appears maintained, with no new failure reports or instability indicators.

---

### 6. Feature Requests & Roadmap Signals
No feature requests were filed today. The lack of any open issues suggests the current focus is on internal data quality and metadata completeness rather than new functionality. The recurring pattern of D5 gate-point updates (five distinct rows processed in one batch) indicates the team is actively cleaning a known data gap. This could foreshadow future enhancements to how the LLM-enhance component uses this enriched data, potentially enabling more accurate vulnerability classification in an upcoming release.

---

### 7. User Feedback Summary
No direct user feedback was recorded today. The closed issues do not reference user pain points; they are all internal chore tasks from a single author (YLChen-007). Without forum posts, comments, or support tickets, user satisfaction or dissatisfaction cannot be assessed from this data set.

---

### 8. Backlog Watch
There are zero open issues and zero open PRs in the repository as of this digest. The backlog is effectively clear, with all tracked work having been completed or closed in the last 24 hours. No long-unanswered items require maintainer attention. This is an unusually clean state, which may indicate either a project pause or a milestone boundary.

--- 

*Digest generated 2026-07-18 from qhkm/zeptoclaw GitHub data.*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-18

## Today's Overview

The ZeroClaw project remains highly active with 50 GitHub issues and 50 pull requests updated in the last 24 hours. Of those, 7 issues were closed and 9 PRs were merged or closed, indicating steady but moderate throughput. No new releases were published today. The project continues to pursue an ambitious roadmap centered on **security hardening (SLSA provenance, OIDC, sandboxing)**, **multi-agent routing and A2A interoperability**, and **observability enhancements**. Several high-priority bugs remain in progress or blocked, particularly around macOS stability and subprocess hang behavior. Community engagement is healthy, with widely-discussed feature requests drawing cross-contributor attention.

## Releases

None.

## Project Progress

**9 PRs merged/closed today** (all closed items):

**Documentation improvements:**
- **[PR #9045]** docs(architecture): document generated docs and localization lifecycles  
- **[PR #8974]** docs(firmware): fix ESP32 hardware design link  
- **[PR #8742]** docs(sop): add no-toml syntax examples  

**Testing and CI hardening:**
- **[PR #9111]** test(commands): add unit tests for `normalize_command_name` edge cases  
- **[PR #8896]** ci(actions): narrow benchmark compile experiment to `agent_benchmarks` target  
- **[PR #8882]** test(api): cover escaped schema refs in properties  
- **[PR #8743]** test(config): cover LinkedIn Schema V4 removal scope  

**Bug fixes and features:**
- **[PR #8768]** fix(zerocode): expose channel root settings in TUI config type list  
- **[PR #8558]** feat(web): link skills to editor — adds Edit link for editable bundle skills in the Skills browser  
- **[PR #8426]** chore(web): allow `ZEROCLAW_GATEWAY_HOST` env override in Vite dev server  

## Community Hot Topics

1. **[ Issue #8177 — "RFC: Supply chain signing" (11 comments, 0 👍)**  
   https://github.com/zeroclaw-labs/zeroclaw/issues/8177  
   **Underlying need:** Users and maintainers are pushing for production-grade supply chain security. This RFC proposes **hardware-backed PGP, multi-party quorum, offline signing, and SLSA provenance** for container images and release binaries. The 11-comment thread suggests active technical debate on implementation details and timeline. Given the number of security-focused RFCs open simultaneously, this signals a coordinated push toward v0.9.0 as a "security release."

2. **[ Issue #5982 — "Per-sender RBAC for multi-tenant agent deployments" (10 comments, 0 👍)**  
   https://github.com/zeroclaw-labs/zeroclaw/issues/5982  
   **Underlying need:** Operators running ZeroClaw in shared environments need **role-based access control** to isolate customers, operators, and developers — with separate workspaces, tool sets, rate limits, and system prompts. The high comment count reflects real enterprise deployment pressure.

3. **[ Issue #3566 — "A2A (Agent-to-Agent) Protocol Support" (8 comments, 7 👍)**  
   https://github.com/zeroclaw-labs/zeroclaw/issues/3566  
   **Underlying need:** The most-liked open feature request asks for native A2A protocol support, enabling ZeroClaw agents to communicate with external agents (other ZeroClaw instances, NanoClaw, OpenClaw, or any A2A-compliant agent). The 7 reactions and sustained discussion indicate strong community interest in interoperability, especially with sibling projects.

4. **[ Issue #2767 — "Multi-Agent Routing" (6 comments, 9 👍)**  
   https://github.com/zeroclaw-labs/zeroclaw/issues/2767  
   **Underlying need:** Users want a single running Gateway to host **multiple isolated agents** with separate workspaces, agent directories, sessions, and channel accounts. This is the most-liked feature overall (9 👍), reflecting that multi-tenant and multi-purpose deployments are a top community priority.

## Bugs & Stability

**Critical/S1 severity (workflow blocked):**

1. **[Issue #8563 — "SOPs not available to agent through web dashboard chat session" (p1, accepted)**  
   https://github.com/zeroclaw-labs/zeroclaw/issues/8563  
   Agents cannot access shared SOP files (`shared/sops/...`). This blocks workflow functionality for users relying on SOP-based guidance. No fix PR identified.

2. **[Issue #8560 — "browser_open hangs the agent turn when launcher cannot open a window" (p1, in-progress)**  
   https://github.com/zeroclaw-labs/zeroclaw/issues/8560  
   On headless hosts or when browser launcher fails, `browser_open` causes indefinite hangs. Also affects robot-kit TTS and channels using ffmpeg. **Status is `in-progress`** — a fix is being worked.

3. **[Issue #7527 — "macOS app not working" (p1, blocked)**  
   https://github.com/zeroclaw-labs/zeroclaw/issues/7527  
   macOS 15.7.7 users report the Tauri desktop app cannot detect granted permissions, shows empty page, and disappears on restart. **Blocked** — no fix PR identified yet. This is a serious desktop experience gap.

**High severity (S2 - degraded):**

4. **[Issue #5628 — "Daemon service auto-starts on boot, causes port conflict" (p2, accepted)**  
   https://github.com/zeroclaw-labs/zeroclaw/issues/5628  
   Systemd service binds port 42617 on boot; manual `zeroclaw daemon` run fails with `Address already in use`. Known for months (accepted April 11), but no fix PR in sight.

5. **[Issue #5869 — "rumqttc v0.25.1 pins old rustls-webpki — RUSTSEC advisory cluster" (p1, blocked)**  
   https://github.com/zeroclaw-labs/zeroclaw/issues/5869  
   Four RUSTSEC advisories rooted in a single transitive dependency (`rumqttc v0.25.1`). **Blocked** — likely waiting on upstream MQTT client updates. This is a security blocker for production deployments.

## Feature Requests & Roadmap Signals

Several major features are converging toward what appears to be **v0.9.0**, themed as a **security and interoperability release**:

- **Pluggable OIDC authentication** (Issue #7141) — umbrella tracking issue, status `accepted`
- **Pluggable security enforcement provider** (Issue #7142) — companion to OIDC work
- **Air-gapped execution mode** (Issue #6293) — split architecture with offline agent container + online companion daemon, potentially for enterprise/classified use
- **Wasm-first plugin runtime** (Issue #8135) — default-on Wasm runtime with signed, capability-declaring plugin modules
- **Granular sandbox policy** (Issue #6996) — config-driven filesystem/network restrictions across Landlock, Bubblewrap, and Seatbelt backends
- **Multi-agent routing** (Issue #2767) — multiple isolated agents in one gateway
- **A2A protocol support** (Issue #3566) — inter-agent communication standard

**Prediction for next version (v0.9.0):** Given the density of `target v0.9.0` annotations on security RFCs and the `priority:p1` status of OIDC work, v0.9.0 will likely ship: **OIDC authentication provider**, **pluggable security enforcement**, and **granular sandbox policies**. A2A and multi-agent routing appear targeted for a subsequent release (v1.0.0).

## User Feedback Summary

**Pain points expressed in the last 24 hours:**

- **Documentation gaps:** Users report missing cron documentation (Issue #7762) and difficulty discovering capabilities through the agent itself (Issue #8367 — capability-aware documentation RFC).
- **Installation friction:** macOS desktop app is broken entirely (Issue #7527). Installation documentation is confusing — users ask for `cargo binstall` documentation (Issue #5269).
- **Tool limitations:** `file_read` cannot handle non-UTF-8 encodings (Issue #7521) — users working with Cyrillic, Latin-1, Shift-JIS files get garbage output. Cron jobs cannot be assigned to specific (cheaper) models (Issue #7762).
- **Configuration UX:** TUI edit string navigation is poor (no arrow keys, must retype everything — Issue #7467). Aliases cannot be renamed after creation (Issue #7468).
- **Interoperability desire:** Strong community demand for multi-agent routing (9 👍), A2A protocol (7 👍), and per-sender RBAC (10 comments) — users want to deploy ZeroClaw in multi-tenant, multi-agent, and cross-platform configurations.

**Satisfaction signals:**
- Active, multi-contributor engagement on high-profile RFCs (20+ unique commenters on the top issues)
- Maintainers responsive — @JordanTheJet and others are named successors for departing maintainer @singlerider (PR #9107), indicating project continuity is being actively managed
- Community members contributing test improvements (PR #9111, #8882) and documentation fixes (PR #8974) — signs of a healthy contributor base

## Backlog Watch

**Issues needing maintainer attention (stale, blocked, or long-unanswered):**

1. **[Issue #5869 — RUSTSEC advisory cluster in rumqttc](https://github.com/zeroclaw-labs/zeroclaw/issues/5869)**  
   Created Apr 18, **blocked**, 4 security advisories. No maintainer update in 90 days. This is a security vulnerability that should be escalated.

2. **[Issue #6293 — Air-gapped execution mode RFC](https://github.com/zeroclaw-labs/zeroclaw/issues/6293)**  
   Created May 3, **blocked + needs-author-action**. The original author hasn't responded to maintainer questions in ~75 days. If still desired, the project should reassign or close.

3. **[Issue #8984 — (not in top 30 but related)]**  
   Multiple PRs now carry `needs-author-action` labels: #8996, #8384, #8443, #8866, #8638, #8601. These large, complex PRs (many tagged `size:XL` or `size:L`) are stalled waiting for author responses. This "author-action bottleneck" is a **project health concern** — PRs over 1,000 lines can't merge without engagement.

4. **[Issue #7527 — macOS app broken](https://github.com/zeroclaw-labs/zeroclaw/issues/7527)**  
   Created Jun 12, **blocked**, no progress in over a month. For a project with a Tauri desktop app, this is a significant user experience gap that should be prioritized.

---

*Digest generated from ZeroClaw GitHub data (zeroclaw-labs/zeroclaw) — 2026-07-18*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*