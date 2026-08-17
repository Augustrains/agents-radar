# OpenClaw Ecosystem Digest 2026-08-17

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-17 00:29 UTC

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

Based on the provided GitHub data snapshot for OpenClaw on 2026-08-17, here is the project digest.

---

# OpenClaw Project Digest — 2026-08-17

## 1. Today's Overview
OpenClaw is in a period of extremely high activity and substantial backlog pressure. The repository saw 500 issues and 500 PRs updated in the last 24 hours, indicating a very busy development and community engagement cycle. While there is a steady stream of merged PRs (82), the sheer volume of open issues (463) and PRs (418) suggests the maintainer team is stretched thin, with many items tagged `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision` waiting for input. The project is advancing on major architectural features like session permission modes and cloud worker profiles, but persistent, critical reliability bugs concerning message loss and session state continue to be the community's primary focus.

## 2. Releases
- **No new stable releases today.** The single latest release is a CI artifact: `pr-124528-profiles`, which contains CPU profiling data from a three-node gateway rig for the PR #124528 event-loop hotspot comparison. This is not a user-facing release.

## 3. Project Progress
The following PRs were merged or closed today, highlighting progress and fixes:

- **Improved Install Security:** PR #120900 (merged) allows admins to review and acknowledge install-policy warnings in the Control UI before proceeding, addressing security concerns.
- **Child Process Cleanup:** PR #120398 (merged) fixes a Linux-only issue where tool child processes were not terminated when their run hit the command timeout, preventing resource leaks.
- **Stuck-Session Recovery Fix:** PR #123877 (open) addresses a critical bug where stuck-session recovery could abort healthy model requests before a configured provider timeout, hindering slow/self-hosted models.
- **UI Polish:** PR #124939 (open) fixes a styling issue where all content on dashboard session cards was incorrectly underlined.
- **Developer Experience:** PR #123975 (open) fixes the `tsgo` typechecker hanging indefinitely when it wedges, instead of failing, which should improve CI and local dev workflows.
- **New Feature Advancements:** Large PRs are in the pipeline for adding cloud worker profiles and machine selection (#124864), keeping durable work visible and auto-archiving stale sessions (#124925), and introducing session permission modes (#124909), signaling upcoming major features.

## 4. Community Hot Topics
The most controversial and critical issues continue to be about silent failures and reliability. These topics draw the most engagement because they undermine user trust in the system's core function: delivering a response.

- **#121058 (CLOSED)**: **[P1] Silent reply failures still recurring after #116277 closed** (97 comments). This is the top issue by far, indicating that the problem of messages being generated but not delivered persists, causing significant user frustration and churn.
  [Link](https://github.com/openclaw/openclaw/issues/121058)
- **#44925 (OPEN)**: **[P1] Subagent completion silently lost — no retry, no notification, no auto-restart on timeout** (31 comments). Users are frustrated by the lack of resilience in subagent orchestration, where work is done but results are lost without any visible feedback.
  [Link](https://github.com/openclaw/openclaw/issues/44925)
- **#42475 (OPEN)**: **[P2] Per-agent cost budget enforcement at the gateway level** (26 comments). There is strong community interest in having built-in cost controls to prevent runaway spending, a key feature for production and business users.
  [Link](https://github.com/openclaw/openclaw/issues/42475)
- **#48003 (OPEN)**: **[P1] Steer mode does not inject messages mid-turn for main sessions** (21 comments). Users expect preemptive steering to work in real-time, but it only works between turns, leading to UX friction.
  [Link](https://github.com/openclaw/openclaw/issues/48003)

## 5. Bugs & Stability
Reliability and core session state integrity are the biggest concerns. Reported issues this period involve regressions, message loss, and process hygiene.

- **High Severity (P1) — Message Loss & Session State:**
    - **#87744**: Codex-backed Telegram turns time out repeatedly, never delivering final answers after 2026.5.27 update. [Link](https://github.com/openclaw/openclaw/issues/87744)
    - **#96834**: WhatsApp 1:1 image sends wedge the message lane for ~3 minutes, blocking processing (repro on 2026.6.10). [Link](https://github.com/openclaw/openclaw/issues/96834)
    - **#115908**: Session transcript projection can livelock under sustained writes, blocking the main thread and stalling *all* channel transports. This is a critical core bug. [Link](https://github.com/openclaw/openclaw/issues/115908)
    - **#53408**: `write`/`exec` tool parameters are silently dropped after long conversations, causing wrong output without error. [Link](https://github.com/openclaw/openclaw/issues/53408)

- **Medium Severity (P2) — Resource & Process Leaks:**
    - **#97616**: OpenClaw leaks unreaped hook/tool child processes, causing zombie accumulation and runtime degradation over time. [Link](https://github.com/openclaw/openclaw/issues/97616)
    - **#74378**: On Windows, CLI commands (`version`, `status`) remain alive as zombie `node.exe` processes after execution. [Link](https://github.com/openclaw/openclaw/issues/74378)

- **Fix PRs in Flight:**
    - PR #123877 aims to fix the stuck-session recovery bug (#121018) that aborts healthy requests.
    - PR #120398 fixes the child process leak (#120386).
    - PR #124858 (open) addresses a security issue where approved scripts could change before execution.

## 6. Feature Requests & Roadmap Signals
There are clear signals about upcoming features based on current PRs and long-standing requests.

- **Near-Term (Likely in next release, based on open PRs):**
    - **Session Permission Modes:** PR #124909 introduces permissions per session with worktree-scoped defaults, moving away from process-global config. This is a major feature for multi-tenant or shared environments. [Link](https://github.com/openclaw/openclaw/pull/124909)
    - **Cloud Worker Profiles:** PR #124864 adds cloud worker profiles and machine selection via the UI. [Link](https://github.com/openclaw/openclaw/pull/124864)
    - **Better CLI Guidance:** PRs #124892 and #124903 improve CLI error messages and fix inconsistent help text for `--json` flags.
- **Long-Standing, Actively Discussed:**
    - **Per-Agent Cost Budgets:** Issue #42475 discusses enforcing cost limits at the Gateway level, a high-demand feature to prevent runaway spend. [Link](https://github.com/openclaw/openclaw/issues/42475)
    - **Tiered Bootstrap Loading:** Issue #22438 addresses context window bloat by proposing a tiered file loading system for sessions to save tokens.
  [Link](https://github.com/openclaw/openclaw/issues/22438)

## 7. User Feedback Summary
- **Frustration with Silent Failures:** The overwhelming sentiment is frustration with the system's lack of resilience. Users are repeatedly reporting that messages are lost, subagent completions are dropped, and replies fail without any notification. This "failure without feedback" is a major pain point.
- **Demand for Control and Observability:** There is a clear need for more control mechanisms and better observability. This includes features like per-agent cost budgets (#42475) and audit trails explaining message delivery (#123709).
- **Satisfaction with Feature Velocity:** Despite the bugs, the project has a strong pipeline of new features (e.g., cloud profiles, session permissions), indicating a healthy roadmap and responsive feature development.

## 8. Backlog Watch
The following issues are important but appear stuck, showing a need for maintainer intervention.

- **#74586 (P1)**: AM embedded run aborts `memory_search` tool calls, classifying it as a timeout despite the model completing. Tagged `clawsweeper-recovery-stuck`.
  [Link](https://github.com/openclaw/openclaw/issues/74586)
- **#50093 (P1)**: WhatsApp backfill for missed messages after reconnection. A critical data-loss issue if the connection drops.
  [Link](https://github.com/openclaw/openclaw/issues/50093)
- **#38327 (P1)**: **"Cannot convert undefined or null to object"** regression in 2026.3.2 with `google-vertex/gemini-3.1-pro-preview`, blocking all agent responses. This is a critical user-facing bug.
  [Link](https://github.com/openclaw/openclaw/issues/38327)
- **#46786 (P1)**: **Security regression**: Enabling `tools.elevated.enabled: true` breaks exec routing logic, routing all `exec` calls to the host.
  [Link](https://github.com/openclaw/openclaw/issues/46786)
- **#87561 (P1)**: Define durable final fallback delivery semantics across channels. This is an architectural issue blocking many of the message-loss bug fixes.
  [Link](https://github.com/openclaw/openclaw/issues/87561)

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-17

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source landscape is experiencing a bifurcation between **scale-intensive core platforms** (OpenClaw, NanoBot, Hermes Agent) and **specialized or niche implementations** (PicoClaw, IronClaw, Moltis, CoPaw). The dominant themes across all projects are reliability (message loss, session state integrity), security hardening (SSRF, approval flows, secret management), and token economics (cost observability, consolidation, context management). A significant architectural shift toward **multi-session orchestration, cross-session context sharing, and agent-to-agent communication** is visible across NanoClaw, Hermes Agent, and ZeroClaw RFCs. The ecosystem is maturing from "single-channel chatbot" toward **durable, multi-channel, multi-agent infrastructure** with provider-neutral abstractions (connectors, memory backends, wire protocols). Community engagement remains high, but maintainer bandwidth is the critical bottleneck across nearly all projects, with PR backlogs accumulating at unsustainable rates.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score* | Primary State |
|---|---|---|---|---|---|
| **OpenClaw** | 500 updated (463 open) | 500 updated (418 open, 82 merged) | No new (CI artifact only) | **3.0/10** | Overwhelmed; critical reliability bugs |
| **NanoBot** | 15 updated (11 open) | 500 touched (499 open, 1 merged) | No new | **2.5/10** | Stagnant; PR conflict crisis |
| **Hermes Agent** | 50 updated | 50 updated | **v0.20.2** (2026.8.16) | **7.5/10** | High-velocity bug-fixing; responsive |
| **PicoClaw** | 3 updated | 5 updated (1 closed) | No new | **6.0/10** | Steady maintenance; security focus |
| **NanoClaw** | 1 (closed, mis-file) | 32 updated (13 merged) | No new | **8.0/10** | High-velocity internal iteration |
| **NullClaw** | — | — | — | N/A | Inactive |
| **IronClaw** | 1 active issue | 9 updated (2 merged) | No new | **6.5/10** | Maintenance & polish; deps accumulating |
| **LobsterAI** | 10 updated (3 closed) | 17 updated (6 merged) | No new | **7.0/10** | Security hardening & cleanup |
| **TinyClaw** | — | — | — | N/A | Inactive |
| **Moltis** | 3 bugs (2 open) | 17 updated (16 merged) | No new | **8.5/10** | Major feature completion; responsive |
| **CoPaw** | 9 updated (3 closed) | 9 updated (0 merged) | No new | **5.5/10** | External contributors awaiting review |
| **ZeroClaw** | 96 open items total | 4 merged | No new (0.8.4 rolling) | **7.5/10** | Architectural renovation; RFC-heavy |

*Health Score: Composite of responsiveness, merge velocity, bug severity, and backlog pressure (10 = excellent).

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**

- **Scale & Mindshare:** With 463 open issues and 418 open PRs, OpenClaw has the largest community engagement of any project in this ecosystem. It is clearly the **reference implementation** — other projects (Hermes Agent PR #88026 "ported from openclaw") explicitly borrow from it.
- **Feature Breadth:** Session permission modes, cloud worker profiles, and steer mode position it as the most feature-complete platform.
- **Active Security Improvements:** Install-policy warnings, child-process cleanup, and approved-script verification show security consciousness.

**Technical Approach Differences:**

- OpenClaw uses a **gateway-centric multi-channel architecture** with process-global config (currently being refactored to session-scoped permissions).
- Unlike Moltis (Rust, memory-backend pluggable) or ZeroClaw (RFC-driven, plugin egress policies), OpenClaw leans on a **Python/TypeScript monorepo** with a "clawsweeper" labeling system for triage.
- The project is **unapologetically feature-rich** — while ZeroClaw debates a "lighter core" (#6165), OpenClaw is adding cloud profiles and session permissions concurrently.

**Community Size Comparison:**

| Metric | OpenClaw | NanoBot | Hermes Agent | ZeroClaw |
|---|---|---|---|---|
| Open Issues | 463 | 11 | ~50 | ~96 (combined) |
| Open PRs | 418 | 499 | ~50 | ~50 |
| Comments on Top Issue | 97 | 15 | 45 | 23 |
| Merge Rate (24h) | 82 | 1 | 2 | 4 |

**Verdict:** OpenClaw's size is both its strength (ecosystem gravity) and weakness (maintainer bottleneck, critical P1 bugs persisting). It's the **default choice for scale**, but teams needing stability may prefer Hermes Agent or Moltis.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects (Evidence) | Specific Needs |
|---|---|---|
| **Message Delivery Reliability** | OpenClaw (#121058 silent failures, #87561 fallback semantics), NanoBot (#5377 consolidation data loss), NanoClaw (#3254 batch starvation) | Unified delivery semantics, retry with notification, audit trails |
| **Token & Cost Governance** | NanoBot (#5266 token burn, #5402 underestimation), OpenClaw (#42475 per-agent budgets), ZeroClaw (#10020 thinking policy) | Per-agent budgets, observability, consolidation correctness |
| **Security Hardening** | OpenClaw (#46786 exec routing, #124858 script tampering), NanoBot (#5305 exec allowlist bypass — fixed), PicoClaw (#3322-24 SSRF), Hermes Agent (#87722-26 gateway secret scope, MCP approval bypass), LobsterAI (#1831-33 log desensitization, IPC ACL, scheme whitelist), Moltis (#1180 zip extraction, #1179 pairing signatures), ZeroClaw (#9580 egress policy) | SSRF guards, approval flows, secret scoping, plugin egress policies |
| **Session & Context Management** | NanoClaw (#3257 cross-session fanout, #3256 detached_at), OpenClaw (#124925 auto-archive stale sessions), Moltis (#1182 main session deletion), CoPaw (#7065 history view) | Multi-session state, context isolation, lifecycle management |
| **Channel Parity & Connectors** | PicoClaw (Simplex, Telegram tables), NanoClaw (OpenMail email), Moltis (#1190 durable connectors: CalDAV, Gmail, Himalaya), LobsterAI (IM instances) | Provider-neutral connectors, native platform features, media handling |
| **Memory & Provenance** | Moltis (#1158 zvec backend), Hermes Agent (#84412 recall provenance), ZeroClaw (RFC #6954 provenance), NanoBot (#1205 KV cache) | Pluggable backends, auditability, provenance envelopes |
| **MCP & Tool Ecosystem** | PicoClaw (#3302 OAuth 2.1 MCP), NanoBot (#5251 MCP Apps UI), ZeroClaw (WASM plugin egress), OpenClaw (MCP tool save_document) | Modern auth, interactive UI, budget-visible schemas |
| **Developer Experience** | OpenClaw (#123975 tsgo hang), Moltis (#1194 macOS bash), IronClaw (Dependabot stack), CoPaw (first-time contributors) | CI stability, onboarding, contributor retention |

---

## 5. Differentiation Analysis

| Project | Primary Differentiator | Target User | Architecture |
|---|---|---|---|
| **OpenClaw** | Broadcast feature coverage; default reference | Enterprises, power users | Monorepo, gateway-centric |
| **NanoBot** | Stability within patch lines; interactive MCP Apps | Individual developers | Python, provider-agnostic |
| **Hermes Agent** | Frequent release cadence; strong bug-fix responsiveness | DevOps, multi-session operators | Python, multiplex-gateway |
| **PicoClaw** | Hardware/embedded focus (Sipeed) | IoT makers, hobbyists | Lightweight, Go/Rust |
| **NanoClaw** | Cross-session orchestration; internal hardening | Deployment-focused teams | Python, agent-group sessions |
| **IronClaw** | Automation & code-review assist (Near AI) | AI-assisted software teams | Rust, event-driven |
| **LobsterAI** | Desktop IM integration (NetEase) | Enterprise China market | Electron, IPC security |
| **Moltis** | Durability; connector-neutral design | Reliability-focused operators | Rust, memory-backend pluggable |
| **CoPaw** | Community-driven; first-time contributor pipeline | Researchers, multi-modal (video) | Python, agent controls |
| **ZeroClaw** | Architectural RFCs; edge egress control | Security-conscious mesh users | Rust, WASM plugins |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapidly Iterating (High Merge Velocity, Active Maintainers):**

- **Moltis** (8.5/10): 16 of 17 PRs merged; quick bug fixes; healthy contributor base.
- **NanoClaw** (8.0/10): 13 PRs merged; deep architectural work on session context and delivery invariants.
- **Hermes Agent** (7.5/10): Patch release (v0.20.2) rolling ~397 PRs; multiple P1 bugs opened and fix PRs filed within 24h.
- **ZeroClaw** (7.5/10): Major security PR merged; RFC process signals deliberate, governance-driven advancement.

**Tier 2 — Stabilizing (Moderate Velocity, Maintenance Focus):**

- **LobsterAI** (7.0/10): Security hardening series merged; stale item sweep indicates backlog cleanup.
- **PicoClaw** (6.0/10): Steady but slow; SSRF PRs awaiting review for 8 days.
- **IronClaw** (6.5/10): Dependency-focused; only 2 merges (both low-risk), feature PRs stalled.

**Tier 3 — Under Stress (High Volume, Low Throughput):**

- **OpenClaw** (3.0/10): 82 merges but 500+ items updated; P1 reliability bugs persist; maintainer stretch.
- **NanoBot** (2.5/10): 1 merge vs 499 open PRs; `[conflict]` crisis from February; needs structural intervention.
- **CoPaw** (5.5/10): 0 merges; 8 first-time contributor PRs awaiting review; contributor-retention risk.

**Inactive:** NullClaw, TinyClaw, ZeptoClaw (no activity in 24h).

---

## 7. Trend Signals

1. **From "Chatbot" to "Infrastructure":** The most active projects (Moltis, NanoClaw, ZeroClaw) treat agents as durable services with connectors, memory backends, and egress policies — not ephemeral chat responses.

2. **Multi-Agent Orchestration is the Next Frontier:** Cross-session context (NanoClaw #3257), internally-initiated agent turns (ZeroClaw #6954), ephemeral swarms (#10025), and subagent orchestration are emerging as core architecture challenges.

3. **Gateway Security Boundaries Are Not Yet Solved:** Hermes Agent's gateway secret-scope issues (#87722-26), NanoBot's exec bypass (#5305), and ZeroClaw's egress policy all point to a collective gap: **secure multi-tenant agent gateways**.

4. **Token Economics is the #1 User Trust Killer:** Users are reporting "millions of tokens burned invisibly" (NanoBot #5266) and "unexpected sub-agent costs" (ZeroClaw #10020). Projects that ship observability and enforcement will win production trust.

5. **Windows is a Second-Class Citizen:** Multiple Windows-specific failures across Hermes Agent (update hangs, Defender SIGTERM), LobsterAI (white icon), and OpenClaw (zombie node.exe) indicate cross-platform robustness is an unfinished journey.

6. **First-Time Contributor Experience is Fragile:** CoPaw's 8 unreviewed PRs and NanoClaw's long review times for external PRs (OpenMail waited 5 months) threaten the ecosystem's contributor pipeline.

7. **Interoperability via Wire Protocols is Being Demanded:** ZeroClaw's OpenAI-compatible RFC (#8603) and Hermes Agent's Devin ACP proposal (#88027) show users want to plug agents into existing toolchains (Open WebUI, LobeChat, Aider) rather than being locked in.

8. **Plugin/Extension Egress is a Security Frontier:** ZeroClaw's multi-PR egress policy rollout (#9580, #9137, #10046) and Moltis's security fixes suggest WASM/plugin sandboxing will be a differentiator.

---

## Concluding Recommendation

For decision-makers evaluating this ecosystem:

- **Choose OpenClaw** if you need maximum feature breadth and community support, and have the ops bandwidth to manage reliability issues.
- **Choose Hermes Agent or Moltis** for production stability, responsive maintainers, and durable architecture.
- **Monitor NanoBot** carefully — its token-management bugs and 499-PR backlog are red flags.
- **Watch ZeroClaw** — its RFC-driven, security-first approach may produce the most hardened, interoperable agent hub in 6-12 months.
- **NanoClaw** is the quiet winner for multi-session orchestration and deserves attention from teams building agent groups.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-17

---

## 1. Today's Overview

NanoBot shows a **high-activity but low-merge** day: **15 issues** were updated (11 open, 4 closed) and **500 PRs** were touched, yet only **1 PR** was merged/closed, leaving **499 open PRs** — a staggering backlog that signals maintainer bandwidth as the primary bottleneck. No new releases shipped this period. The community continues to surface **token-management bugs** (underestimation, consolidation truncation, excessive burn) and **architectural concerns** around prompt fidelity and security, suggesting the project is in a **stabilization phase** rather than a feature-expansion phase. The sheer volume of stale `[conflict]`-tagged PRs (many from February) indicates a **needs-rebase crisis** that may require maintainer triage or automated conflict resolution tooling.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The last release remains `0.1.4post5`, which was the subject of a regression report ([#2185](https://github.com/HKUDS/nanobot/issues/2185)) regarding Gemini 3 Flash Preview compatibility.

---

## 3. Project Progress

Only **1 PR was merged/closed** in the last 24 hours:

- **[#4329](https://github.com/HKUDS/nanobot/pull/4329) — [CLOSED] feat(cli): add native TypeScript terminal UI** — This is a notable recovery event: the original PR was *mistakenly marked merged* when its head briefly appeared on `main`, then `main` was restored. The replacement PR **[#5406](https://github.com/HKUDS/nanobot/pull/5406)** carries the same commit history plus terminal test fixes. This signals the maintainers are actively curating the CLI modernization path, even if the close was procedural rather than a true merge.

Additionally, **4 issues were closed**, including:
- **[#2185](https://github.com/HKUDS/nanobot/issues/2185) — Gemini regression** (still needs verification of fix)
- **[#5305](https://github.com/HKUDS/nanobot/issues/5305) — exec allowlist security bypass** — resolved
- **[#5275](https://github.com/HKUDS/nanobot/issues/5275) — Matrix thread context** — resolved
- **[#5373](https://github.com/HKUDS/nanobot/issues/5373) — Cron scheduler persistence crash** — resolved

No new features were merged in this window.

---

## 4. Community Hot Topics

The most active conversations reveal core pain points around **system prompt fidelity**, **token economics**, and **security**:

- **[#2463](https://github.com/HKUDS/nanobot/issues/2463) — Architectural: prompt prefix not preserved (15 comments)** — The most-discussed issue. User `ronny-rentner` argues that persisting conversation history in a form that differs from the exact prompt prefix sent to the model creates a fundamental conflict with OpenAI's provider semantics. This is a **deep architectural concern** that affects reproducibility, debugging, and cost optimization. Maintainers should treat this as a design-debt signal.

- **[#5266](https://github.com/HKUDS/nanobot/issues/5266) — Token consumption logging (14 comments)** — Users report burning **millions of tokens in 2 hours** with no visible activity. The ask is basic observability: "log when and which call produces which token consumption." This is a **high-value, low-effort** feature that would dramatically improve user trust.

- **[#2185](https://github.com/HKUDS/nanobot/issues/2185) — Gemini regression (9 comments)** — Users are frustrated by a silent breaking change between patch releases. The underlying need: **stable behavior within a patch line**.

- **[#4864](https://github.com/HKUDS/nanobot/issues/4864) — Endless loop on `complete_goal` (6 comments, 1 👍)** — Tool parameter serialization regression causing runaway loops. This is a **correctness bug**, not just a nuisance.

The **PR backlog** is dominated by `[conflict]`-tagged PRs (12 of the top 20), all from February, including:
- **[#1306](https://github.com/HKUDS/nanobot/pull/1306)** — Discord voice/audio support
- **[#1205](https://github.com/HKUDS/nanobot/pull/1205)** — KV cache reuse
- **[#1149](https://github.com/HKUDS/nanobot/pull/1149)** — PromptGuard injection detection
- **[#1128](https://github.com/HKUDS/nanobot/pull/1128)** — 163.com IMAP fix

These PRs represent **significant community work** that is effectively frozen due to merge conflicts.

---

## 5. Bugs & Stability

Ranked by severity:

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|-----------|
| **Critical** | [#5305](https://github.com/HKUDS/nanobot/issues/5305) | `exec.allowPatterns` allowlist bypass → chained shell command execution via API | **Closed** (fix verified) |
| **Critical** | [#5373](https://github.com/HKUDS/nanobot/issues/5373) | Cron scheduler **dies permanently** after a single persistence failure; no next tick is armed | **Closed** |
| **High** | [#4864](https://github.com/HKUDS/nanobot/issues/4864) | Endless loop in `<tool_call> <function=complete_goal>` due to gateway mis-parsing `recap` as bare string instead of JSON | Open; likely regression from recent tool param serialization |
| **High** | [#5402](https://github.com/HKUDS/nanobot/issues/5402) | Token consolidation never triggers — tiktoken **underestimates** actual token counts by API's measure | Open; no fix PR yet |
| **High** | [#5377](https://github.com/HKUDS/nanobot/issues/5377) | Consolidation truncates archive input but **advances past the full message batch** → permanent message loss | Open; no fix PR yet |
| **Medium** | [#5266](https://github.com/HKUDS/nanobot/issues/5266) | Excessive token burn with no logging — observability gap, not a crash but a **cost leak** | Open; enhancement request |

**Note:** Two of the three "High" bugs are in the **token consolidation subsystem**, which appears to be the **most fragile area** of the current codebase.

---

## 6. Feature Requests & Roadmap Signals

Strong roadmap signals from active requests:

- **[#5404](https://github.com/HKUDS/nanobot/issues/5404) — `disable-model-invocation` for skills** — Users want to make skills *user-only* (model cannot auto-invoke). Patterned after PI/Cursor/Claude Code. This is a **power-user governance feature** likely to land soon given its simplicity.

- **[#5251](https://github.com/HKUDS/nanobot/issues/5251) — MCP Apps host support in WebUI** — Treat MCP call results as interactive UI (via `io.modelcontextprotocol/ui`), not just text/images. This is a **forward-looking feature** aligned with the MCP roadmap; moderate complexity.

- **[#5298](https://github.com/HKUDS/nanobot/issues/5298) — Budget model-visible MCP schemas** — Reduce context cost for large MCP tool sets. A **practical performance feature** that pairs with the token-burn complaints.

- **[#5289](https://github.com/HKUDS/nanobot/issues/5289) — Telegram stickers + agent-initiated reactions** — Channel parity feature. Low complexity, high delight.

- **[#4467](https://github.com/HKUDS/nanobot/issues/4467) — Dream should *update* existing skills, not duplicate** — Users want **iterative skill evolution** rather than recreation per run. This has 1 👍 and reflects a workflow-integration desire.

- **[#5358](https://github.com/HKUDS/nanobot/pull/5358) — WebUI session collaboration via mentions** — Active PR, suggests **multi-session orchestration** is on the roadmap.

**Prediction:** The token-consolidation fixes (`#5377`, `#5402`) and the CLI TypeScript UI (`#5406`) are the most likely next merges. The `disable-model-invocation` skill feature (`#5404`) is a strong candidate for v0.1.5.

---

## 7. User Feedback Summary

**Pain Points:**
- **Token economics are unpredictable** — Users report millions of tokens burned invisibly (`#5266`) and consolidation logic that silently fails (`#5402`, `#5377`). Trust in cost control is low.
- **Prompt fidelity matters** — Users want exact reproducibility of what was sent to the model (`#2463`). This is an architectural trust issue.
- **Patch releases break things** — Silent regressions between `0.1.4` and `0.1.4post5` (`#2185`) erode confidence in semantic versioning.
- **Skills workflow friction** — Users maintain workspace skills long-term and want incremental updates, not duplicates (`#4467`).
- **Media accumulation** — Multiple PRs (`#1026`, `#1128`) address unbounded disk growth from media files and config key loss — long-standing operational annoyances.

**Satisfaction Indicators:**
- The Matrix thread-context issue was **closed**, indicating channel-parity work is progressing.
- The `exec` security bypass was fixed and closed — a **positive security response signal**.
- The Cron scheduler permanent-death bug was fixed — **resilience improving**.

**Overall sentiment:** Users are **engaged but cautious** — they appreciate the framework's breadth but are frustrated by stability gaps and lack of observability.

---

## 8. Backlog Watch

### Critical: Frozen PRs needing maintainer attention

These are **high-value, conflict-tagged PRs** awaiting rebase/merge. They represent significant community effort and are blocked only by maintenance bandwidth:

- **[#1306](https://github.com/HKUDS/nanobot/pull/1306)** — Discord voice/audio + TTS (Feb 28)
- **[#1205](https://github.com/HKUDS/nanobot/pull/1205)** — KV cache reuse (Feb 25)
- **[#1149](https://github.com/HKUDS/nanobot/pull/1149)** — PromptGuard injection defense (Feb 25)
- **[#1147](https://github.com/HKUDS/nanobot/pull/1147)** — Telegram group sender-name prefix (Feb 24)
- **[#1073](https://github.com/HKUDS/nanobot/pull/1073)** — Preserve unknown config keys (Feb 23) — addresses config data-loss bug
- **[#1072](https://github.com/HKUDS/nanobot/pull/1072)** — Catch `CancelledError` in tool execution (Feb 23) — **crash-prevention**
- **[#1066](https://github.com/HKUDS/nanobot/pull/1066)** — Release & Docker CI workflow (Feb 23)
- **[#1026](https://github.com/HKUDS/nanobot/pull/1026)** — Delete processed media files (Feb 23) — **disk growth fix**
- **[#1025](https://github.com/HKUDS/nanobot/pull/1025)** — Persist OAuth tokens + preserve unknown fields (Feb 23)
- **[#1024](https://github.com/HKUDS/nanobot/pull/1024)** — Subagent profiles with tools/skills (Feb 22)
- **[#1015](https://github.com/HKUDS/nanobot/pull/1015)** — Per-subagent model parameter (Feb 22)

### Long-unanswered Issues

- **[#2185](https://github.com/HKUDS/nanobot/issues/2185)** — Gemini regression (closed, but no fix PR linked — verify the fix is actually shipped)
- **[#2463](https://github.com/HKUDS/nanobot/issues/2463)** — Prompt-prefix fidelity (open since **March**; architectural, needs maintainer design decision)

### Recommendation

The **500-PR backlog with 499 open** is unsustainable. I recommend the maintainers:
1. **Batch-rebase** the ~20 `[conflict]` PRs from Feb–Mar or explicitly request rebases from authors.
2. **Auto-close stale PRs** (>90 days without activity) with a clear re-open path.
3. Prioritize merging the **crash-prevention** PRs (`#1072`, `#1026`, `#1073`) before new features.

---

*Digest generated from GitHub data as of 2026-08-17. All links point to original GitHub items for verification.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-08-17

---

## 1. Today's Overview

Hermes Agent (v0.20.2, released 2026.8.16) is in a period of high-intensity bug-fixing and feature development. Activity is elevated: 50 issues and 50 PRs were updated in the last 24 hours, with a patch release rolling up ~397 PRs. The project's health is characterized by strong momentum but notable strain—a significant cluster of new P1/P2 bugs appeared on August 16–17, particularly around Windows update flows, gateway security boundaries, and desktop stability. The maintainer team appears responsive, with multiple fix PRs already opened against the most critical issues, and several long-running PRs (including a per-job cron cap and streaming attribution fix) continue to receive attention.

---

## 2. Releases

**New release: v2026.8.16 — Hermes Agent v0.20.2** (2026-08-16)

This patch release rolls up **~397 PRs merged since v0.20.1** into a stable tagged release for downstream consumers (Docker images, hosted deployments, fresh installs). It primarily serves as a stabilization point; no breaking changes or migration notes were highlighted.

---

## 3. Project Progress

**Merged/Closed (2 PRs)** — note: none of the top-20 by comment count were merged today; the two merged/closed PRs are not in the detailed list.

**Notable PRs updated today (open, high-signal):**

| PR | Focus | Status Signal |
|---|---|---|
| [#45809](https://github.com/NousResearch/hermes-agent/pull/45809) | Per-job `max_turns` + wall-clock timeout caps for cron jobs | Long-running feature (since June 13), still open; addresses a real resource-exhaustion gap |
| [#74875](https://github.com/NousResearch/hermes-agent/pull/74875) | Attribute worker-thread failures to their session in logging | Fix for cross-session log attribution, open since July 30 |
| [#78819](https://github.com/NousResearch/hermes-agent/pull/78819) | Don't bump skill telemetry from curator's review fork | Prevents self-inflating skill usage stats; subtle but important data-integrity fix |
| [#68271](https://github.com/NousResearch/hermes-agent/pull/68271) | Route TUI skill secret prompts to the owning session | Fixes cross-session credential-prompt routing bug; security-adjacent |
| [#84412](https://github.com/NousResearch/hermes-agent/pull/84412) | Structured recall-provenance envelope (RecallItem) for memory | Tier B of a larger memory provenance effort; improves auditability |
| [#88026](https://github.com/NousResearch/hermes-agent/pull/88026) | `hermes logs -f` survives log rotation | Quality-of-life CLI fix, ported from openclaw |
| [#88028](https://github.com/NousResearch/hermes-agent/pull/88028) | `decline` option for unauthorized-DM behavior | New gateway policy option: one-time polite decline + 24h quiet |
| [#88030](https://github.com/NousResearch/hermes-agent/pull/88030) | OR-relaxed retry for `session_search` paraphrased recall | Improves recall quality for fuzzy queries |
| [#88024](https://github.com/NousResearch/hermes-agent/pull/88024) | Generative UI: agents render live inline UI via plugin directives | Notable feature: closes the gap between "agent builds a plugin" and "plugin shows up in chat" |
| [#88027](https://github.com/NousResearch/hermes-agent/pull/88027) | Expose Devin ACP as a first-class Hermes provider | New provider integration, requires maintainer decision |
| [#87712](https://github.com/NousResearch/hermes-agent/pull/87712) | New `vision_ocr` tool + OCR grounding for auxiliary vision path | Enables CPU-friendly OCR for text-only models |
| [#87711](https://github.com/NousResearch/hermes-agent/pull/87711) | Add Grok Imagine Image 2.0 to xAI image catalog | Feature addition + model-selection fix for editing |

---

## 4. Community Hot Topics

**Top by engagement:**

1. **[#66616 — Skills index stale/degraded](https://github.com/NousResearch/hermes-agent/issues/66616)** — **45 comments**. Automated freshness probe failing (index 29.8h old vs 26h limit). Long-running infrastructure-degradation issue; high community visibility because it affects `docs/skills` and the Skills Hub. Signals a need for better owner-less, "watchdog" alerting.

2. **[#53480 — Updater should guard against interrupting active Desktop sessions](https://github.com/NousResearch/hermes-agent/issues/53480)** — 5 comments. Feature request to block/defer updates while agents are actively working. Underlying need: user data-loss and workflow-interruption anxiety during self-updates.

3. **[#87818 — computer_use capture drops `question` param on auxiliary.vision path](https://github.com/NousResearch/hermes-agent/issues/87818)** — 4 comments. A specific bug with clear root-cause analysis.

4. **[#87027 — Ollama MCP tools: fabricated results, no real tool_calls](https://github.com/NousResearch/hermes-agent/issues/87027)** — **CLOSED** (4 comments). Major user-facing provider bug, now closed.

5. **[#87703 — Windows: hermes update hangs ~11 min on cua-driver](https://github.com/NousResearch/hermes-agent/issues/87703)** — 3 comments. Part of today's **Windows update cluster** (see Bugs section).

---

## 5. Bugs & Stability

Ranked by severity (P1 > P2 > P3):

| Severity | Issue | Summary | Fix PR? |
|---|---|---|---|
| **P1** | [#87694](https://github.com/NousResearch/hermes-agent/issues/87694) | `hermes update` autostash can create orphan commit → **breaks all subsequent updates** | Not yet |
| **P2** | [#87027](https://github.com/NousResearch/hermes-agent/issues/87027) | Ollama: agent fabricates MCP tool results, no real tool_calls (CLOSED) | — |
| **P2** | [#87724](https://github.com/NousResearch/hermes-agent/issues/87724) | `computer_use` mutations **fail open** in headless mode (no approval callback) — security boundary risk | Not yet |
| **P2** | [#87722](https://github.com/NousResearch/hermes-agent/issues/87722) | Secondary-profile cron delivery **escapes secret scope**, can use default-profile credentials — security risk | Not yet |
| **P2** | [#87726](https://github.com/NousResearch/hermes-agent/issues/87726) | MCP approval responses do not resolve authoritative gateway approvals — approval bypass | Not yet |
| **P2** | [#87856](https://github.com/NousResearch/hermes-agent/issues/87856) | `API_SERVER_ENABLED=false` has no effect — server starts anyway (always-on API key) | Not yet |
| **P2** | [#87857](https://github.com/NousResearch/hermes-agent/issues/87857) | Desktop renderer crash loop: "Duplicate key toolCallId in useResources" → blank window | Not yet |
| **P2** | [#87703](https://github.com/NousResearch/hermes-agent/issues/87703) | Windows: `hermes update` hangs ~11 min on invisible UAC prompt (cua-driver) | Not yet |
| **P2** | [#87772](https://github.com/NousResearch/hermes-agent/issues/87772) | Desktop update stalls 10–17 min on hung cua-driver; stuck "update finishing" marker | Not yet |
| **P2** | [#87697](https://github.com/NousResearch/hermes-agent/issues/87697) | Local LLM streams cancelled after ~1.5s (Ollama) — triggers `<unused49>` token loop | Not yet |
| **P2** | [#70233](https://github.com/NousResearch/hermes-agent/issues/70233) | `reasoning_details` from Groq leaks into next request → breaks non-reasoning models | Not yet |
| **P2** | [#87781](https://github.com/NousResearch/hermes-agent/issues/87781) | Memory approval replay fails on removal-only batches ("empty content") | Not yet |
| **P3** | [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | Skills index stale/degraded (watchdog-detectable) | Not yet |

**Notable clusters:**
- **Windows update/installer cluster** — #87703, #87772, plus related [#87828](https://github.com/NousResearch/hermes-agent/issues/87828) (health check SIGTERM due to Defender), all pointing to fragile cua-driver interaction on Windows.
- **Gateway security-boundary cluster** — #87722, #87723, #87726 (profile/cron secret escape, shared session DB, MCP approval bypass) suggest multiplex-gateway hardening is needed.
- **TTS double-play bug** — [#86601](https://github.com/NousResearch/hermes-agent/issues/86601) and duplicate [#87823](https://github.com/NousResearch/hermes-agent/issues/87823) both describe auto-TTS reading the same reply twice.

---

## 6. Feature Requests & Roadmap Signals

**Strong signals:**

- **Windows platform hardening** (multiple issues): Smart App Control detection (`os error 4551`, [#87789](https://github.com/NousResearch/hermes-agent/issues/87789)), update-flow guards ([#53480](https://github.com/NousResearch/hermes-agent/issues/53480)), installer timeouts — clearly a prioritized area.
- **Generative UI in chat** ([#88024](https://github.com/NousResearch/hermes-agent/pull/88024)): plugin-registered inline UI directives — would be a significant UX leap.
- **Devin ACP as a provider** ([#88027](https://github.com/NousResearch/hermes-agent/pull/88027)): new external-process provider; needs maintainer decision.
- **Session-title regeneration** ([#47803](https://github.com/NousResearch/hermes-agent/issues/47803)): LLM-based, multi-language titles with periodic refresh — community-voted (1 👍).
- **OCR tooling** ([#87712](https://github.com/NousResearch/hermes-agent/pull/87712)): dedicated `vision_ocr` tool with bounding boxes for CPU-class models.
- **`decline` mode for unauthorized DMs** ([#88028](https://github.com/NousResearch/hermes-agent/pull/88028)): privacy-preserving gateway behavior.

**Prediction for next release (v0.20.3 / v0.21):** Likely to include the Windows update-flow fixes (cua-driver timeout, Smart App Control detection), the gateway secret-scope fixes, and possibly the generative-UI or Devin-provider features if maintainers greenlight them.

---

## 7. User Feedback Summary

**Pain Points (explicit or inferred):**

- **Update anxiety**: "update didn't finish," invisible hangs, orphan commits, Smart App Control blocks producing opaque failures — users are losing confidence in a smooth update story.
- **Windows second-class experience**: Multiple windows-only issues (installer hangs, Defender behavior monitoring SIGTERM, health-check failures) reveal a gap between Linux/macOS polish and Windows robustness.
- **Local-model friction**: Ollama users report fabricated tool calls ([#87027](https://github.com/NousResearch/hermes-agent/issues/87027)) and stream cancellation ([#87697](https://github.com/NousResearch/hermes-agent/issues/87697)) — trust in local-provider support is eroding.
- **Security-conscious operators**: Gateway/multiplex profile isolation issues are being reported with detailed code evidence (tachyon-r) — power users are probing security boundaries and finding gaps.
- **Data-integrity concerns**: Orphan commits, session rows disappearing, skills index staleness — users value reliability of the underlying data store.

**Satisfaction signals:** Rapid issue closure (e.g., #87027 closed within 24h), active volunteer PR contributions (multiple first-time/community authors), and a detailed, well-documented release cadence.

---

## 8. Backlog Watch

Long-running items needing maintainer attention:

- **[#45809 — Per-job cron caps (max_turns/timeout)](https://github.com/NousResearch/hermes-agent/pull/45809)** — Open since **June 13** (65 days). Feature is well-scoped and addresses a real operational risk, yet has not been merged. Likely waiting for review bandwidth.
- **[#74875 — Attribute worker-thread failures to session](https://github.com/NousResearch/hermes-agent/pull/74875)** — Open since **July 30** (18 days). Fixes a debug-tooling promise; important for multi-session users.
- **[#27724 — BusyBox grep fallback for search tool](https://github.com/NousResearch/hermes-agent/pull/27724)** — Open since **May 18** (91 days). Simple compatibility fix (Alpine/embedded), long-stalled.
- **[#68271 — Route TUI skill secret prompts to owning session](https://github.com/NousResearch/hermes-agent/pull/68271)** — Open since **July 20** (28 days). Security-adjacent fix for cross-session credential leakage; should be prioritized.
- **[#78819 — Skill telemetry shouldn't count curator reads](https://github.com/NousResearch/hermes-agent/pull/78819)** — Open since **August 4** (13 days). Data-integrity fix with no downside.
- **[#66616 — Skills index freshness watchdog (issue)](https://github.com/NousResearch/hermes-agent/issues/66616)** — 45 comments, open a month; needs an owner or a watchdog-recovery path.

---

*Data source: GitHub — NousResearch/hermes-agent, data as of 2026-08-17.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-17

## 1. Today's Overview
PicoClaw shows moderate activity with 3 open issues and 5 pull requests updated in the past 24 hours, none of which were newly created today except one bug report (#3338). A single PR (#3193) was closed during this window, indicating only gradual progress toward merging contributions. The project is in a steady maintenance phase, with a clear focus on security hardening (SSRF protections across messaging channels), platform integration improvements, and feature parity enhancements. Notably, three open PRs by the same contributor (SashaMIT) targeting SSRF vulnerabilities across WeCom, Weixin, and other channels are approaching potential merge readiness, while the community continues to push for broader protocol support.

## 2. Releases
No new releases were published in the last 24 hours. The most recent version appears to be 0.3.x based on the bug report context.

## 3. Project Progress
- **Closed PR #3193**: "Added simplex channel type" — A new feature adding support for the Simplex messaging protocol, marking the only merge/closure today. The PR had been open since June 27 and was closed after approximately 7 weeks of review, suggesting it was either merged or rejected after a lengthy evaluation period.
- No other PRs were merged or closed in this window. The remaining open PRs (#3299, #3322, #3323, #3324) are all still under review, with the three SSRF hardening PRs by SashaMIT forming a coordinated security improvement series.

## 4. Community Hot Topics
- **[Issue #3302 — OAuth 2.1 for MCP servers](https://github.com/sipeed/picoclaw/issues/3302)** — 3 comments, created July 30. The community is requesting support for OAuth 2.1 authentication for MCP servers, building on an earlier request in issue #2546. This signals a growing need for modern, secure authentication standards in the MCP integration layer.
- **[Issue #3325 — Render Telegram tables with rich messages](https://github.com/sipeed/picoclaw/issues/3325)** — 1 comment, created August 9. Users want Telegram's native table UI (introduced in Bot API 10.1) instead of degraded Markdown tables. This reflects a desire for richer, platform-native message rendering.
- **[Issue #3338 — Slack media upload failure](https://github.com/sipeed/picoclaw/issues/3338)** — Newest issue, created today. Slack media uploads are completely broken due to a missing `FileSize` parameter in the upload configuration, causing every upload to fail with a "file size cannot be 0" error before any network call is made.

## 5. Bugs & Stability
- **[HIGH] Slack media uploads completely broken (#3338)](https://github.com/sipeed/picoclaw/issues/3338)** — Newly reported today. The `SendMedia` function omits the `FileSize` field when building `slack.UploadFileParameters`, causing the slack-go SDK to reject every upload. This is a regression-level bug that entirely blocks media sharing to Slack. No fix PR exists yet; the issue is open with zero comments.
- **[MEDIUM] SSRF vulnerabilities across multiple channels (PRs #3322, #3323, #3324)** — Not new bugs, but security concerns being actively patched. The PRs address SSRF vectors where malicious media URLs can reach loopback, link-local, or RFC1918 addresses through WeCom, Weixin, and other channels (QQ, Telegram, Discord, LINE, Slack). These are coordinated fixes using `CreateSafeHTTPClient` and `BlockPrivateTargets` hardening. While the fixes are not yet merged, the fact that they're being developed in parallel suggests the maintainers recognize the severity.

## 6. Feature Requests & Roadmap Signals
- **[OAuth 2.1 support for MCP servers (#3302)](https://github.com/sipeed/picoclaw/issues/3302)** — A follow-up to #2546, marking this as a long-standing request. User marked it as "Nice-to-Have," but given the growing adoption of OAuth 2.1 across the ecosystem, this could become a priority for the next minor release.
- **[Native Telegram table rendering (#3325)](https://github.com/sipeed/picoclaw/issues/3325)** — The Telegram Bot API 10.1 feature for native tables is new, and this request aligns with keeping PicoClaw's platform integrations up-to-date with the latest API capabilities.
- **[Exa web search provider (PR #3299)](https://github.com/sipeed/picoclaw/pull/3299)** — An open PR adding Exa as a native `tools.web` / `web_search` provider. If merged, it would expand the search capabilities beyond existing providers, suggesting work on broader tool ecosystem expansion.
- **Simplex channel (PR #3193)** — Either newly merged or closed today; if merged, this adds a privacy-focused messaging channel, broadening the platform support matrix.

## 7. User Feedback Summary
Community sentiment shows users actively pushing for both security improvements and feature richness:
- **Security awareness**: Users are contributing SSRF hardening fixes proactively, indicating a security-conscious contributor base that values safe defaults in network operations.
- **Integration pain points**: The Slack media upload bug (#3338) is a clear functional breakage, suggesting users rely heavily on media sharing across channels and expect it to work out-of-the-box.
- **Modern protocol adoption**: Requests for OAuth 2.1 and native Telegram tables show users expect PicoClaw to keep pace with evolving platform APIs and authentication standards rather than lagging behind.
- **Privacy focus**: The Simplex channel addition (wherever it landed) and the request for Exa search suggest a user base interested in privacy-respecting alternatives to mainstream services.

## 8. Backlog Watch
- **[PR #3299 — Exa web search provider](https://github.com/sipeed/picoclaw/pull/3299)** — Open since July 26 (3 weeks), with no comments listed. This feature addition appears stalled without reviewer feedback, which may frustrate the contributor and delay search capability expansion.
- **[Issue #3302 — OAuth 2.1 for MCP servers](https://github.com/sipeed/picoclaw/issues/3302)** — Open since July 30 with 3 comments but no maintainer response visible. As a follow-up to #2546, this has now been pending for months and needs at least a roadmap acknowledgment.
- **[PRs #3322, #3323, #3324 — SSRF hardening series](https://github.com/sipeed/picoclaw/pull/3322)** — All open since August 9 (8 days) and marked as stale. These security fixes should be prioritized for review and merge given the potential attack surface they address. The maintainers' attention here would materially improve the project's security posture.

*Note: The active 24-hour timeline showed no new releases, no merged PRs beyond #3193 (closure status unclear), and the project appears to be in a holding pattern where community contributions are accumulating without rapid maintainer response — a possible bottleneck worth monitoring.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-17

## 1. Today's Overview
NanoClaw maintained a **high-velocity development cadence** over the past 24 hours, with **32 PRs** updated (19 open, 13 closed/merged) and only **1 issue** registered (subsequently closed as a non-actionable error). Core-team activity dominated the merge pipeline, with 10+ PRs focused on **agent-group session management, channel adapter capabilities, and delivery-pipeline hardening**. Notably, no new releases were published, and the single issue was filed against the wrong repository — indicating **low user-facing bug noise** but **deep architectural iteration** happening internally.

## 2. Releases
**None.** No new versions were published in the reporting window.

## 3. Project Progress (Merged/Closed PRs)
**13 PRs were closed/merged**, with the following themes:

### Agent-to-Agent & Session Context
- **PR #3257** — Cross-session context fan-out: messages now echo into sibling sessions (`trigger=0` session-echo rows), DM sessions get backfilled, and a new `ncl sessions history` command was added. *(Open)*
- **PR #3265** — `CreateAgentOptions.suppressCreatedNotify` flag: suppresses only the success message while preserving error notifications for wrappers needing post-creation provisioning. *(Closed)*
- **PR #3262** — Chat SDK bridge DM-surface handling: app-context capture, DM-thread normalization, `dm-opened` hook (A8 + C4). *(Closed)*

### Core Delivery & Container Logic
- **PR #3284** — **Mid-turn streaming as the single content door**: providers that stream assistant text now never send content via the final result path; DB-backed echo suppression eliminates the need for persistent dedupe state. *(Closed)*
- **PR #3254** — Two-phase inbound batch selection: context rows (`trigger=0`) can no longer crowd out due task rows in the capped batch — previously a backlog could push the actual work item out, causing a wake with no deliverable work. *(Open)*
- **PR #3255** — Outbound delivery now resolves the sender's own channel row, not an arbitrary sibling instance, fixing multi-identity per-room scenarios. *(Open)*
- **PR #3256** — `messaging_groups.detached_at` column (migration 022): tracks when the bot is removed from platform conversations; delivery refuses sends into detached rooms. *(Open)*

### Channel & Adapter Layer
- **PR #3261** — Optional adapter capabilities: status-bearing `setTyping`, `setThreadTitle`, `setSuggestedPrompts`, with registry passthroughs. *(Closed)*
- **PR #3263** — `startChannelAdapter(key)`: hot-start a registered adapter post-boot, replaying the same four boot steps. *(Closed)*

### Permissions & Interception
- **PR #3260** — New `decline_notify` unknown-sender policy: polite decline + one-line owner FYI, no approval card interruption. *(Closed)*
- **PR #3266** — `registerChannelCardInterceptor` seam: modules can consume channel-registration approval escalation before a card is built. *(Closed)*

### Setup & Tooling
- **PR #3259** — Skill-apply heading-ordinal stripping, headless browser URL surfacing, and inherit-script extraction. *(Closed)*
- **PR #3278** — `save_document` MCP tool: persists Word/PDF attachments to agent group durable memory (Story 1.1 of the Document Memory epic). *(Closed)*
- **PR #3283** — Preserves Chat SDK hyperlink targets when platform display text is shortened/labeled differently; hidden deduplicated URLs from `links[]`. *(Closed)*
- **PR #1251** — **`/add-openmail` skill**: adds email via OpenMail as a channel (auto-respond) or tool+notify mode. *(Closed — long-running since March)*

## 4. Community Hot Topics
With only 1 issue (a mis-file) and no comments reported on the top PRs, community discussion activity was **minimal**. The most substantive PRs by author investment and architectural scope:

- **PR #3257** (Cross-session context) — Notably complex: fan-out, DM backfill, echo pruning. Indicates the maintainers are anticipating real-world multi-session agent deployments.
- **PR #3284** (Single delivery door) — Architectural invariant change; likely the most debated design internally given its complexity.
- **PR #1251** (OpenMail email) — Community-contributed (external author `armandokun`), was open since March and finally merged — suggests a **platform-expansion backlog** rather than core churn.
- **PR #3282** (Telegram pairing codes with spaces) — User-facing UX fix from a contributor; reflects real-world friction in the setup wizard.

**Underlying need:** The community is pushing toward **practical deployment durability** (email integration, attachment handling, multi-channel identity) while the core team focuses on **architectural hardening** (delivery invariants, context isolation).

## 5. Bugs & Stability
No new user-reported bugs in the last 24 hours. The only issue (#3271) was closed as a mis-file. However, **fix PRs** in flight include:

| Severity | Issue / Fix | Description |
|----------|-------------|-------------|
| **High** | PR #3254 (open) | **Batch selection starvation**: agenda task rows could be crowded out by newer context rows — the agent wakes but never processes the actual task. Fix is two-phase selection. |
| **Medium** | PR #3282 (open) | Telegram pairing code UX: pasted codes with spaces were rejected; now whitespace-collapsed. |
| **Medium** | PR #3281 (open) | `ncl tasks` blind to pre-2.1.54 legacy sessions for agent-scoped queries (fixes #3233). |
| **Medium** | PR #2752 (open, since June) | Inbound Discord attachments (both pasted text and images) never reach the agent with bytes/path — only a bare filename placeholder. |
| **Low** | PR #3280 (open) | `ncl groups config update` cannot unset a nullable scalar (`--model ""` stores empty string not `NULL`). |
| **Low** | PR #3255 (open) | Outbound delivery resolves arbitrary sibling channel row in multi-identity rooms — incorrect recipient resolution. |

## 6. Feature Requests & Roadmap Signals
No explicit user feature requests landed in the past 24 hours. However, **merged PRs signal roadmap direction**:

- **Document Memory epic (PR #3278)** — `save_document` MCP tool is Story 1.1; expect **Word/PDF fill-in editing and retrieval** in subsequent stories.
- **Cross-session context (PR #3257)** — Suggests a roadmap for **multi-session agent groups with shared memory**, likely leading to orchestration features.
- **OpenMail skill (PR #1251)** — Email channel capability is now available; expect **email-driven agent workflows** in community usage.
- **Detached conversation tracking (PR #3256)** — Sets groundwork for **rejoin/sync behavior for platform removals**.

**Prediction:** Next release likely includes the detached_at migration (022), cross-session echo logic, and the channel-adapter hot-start — all core-team items currently open and queued.

## 7. User Feedback Summary
Due to minimal issue/comment activity, direct user feedback is sparse. Signals from closed/fixed items:

- **Setup friction**: Telegram pairing code whitespace rejection (PR #3282) indicates user-facing wizard error handling needed polish.
- **Attachment usability**: Discord attachments being invisible to agents (PR #2752, open since June) is a **persistent pain point** — contributor-aged fix has not merged.
- **CLI edge cases**: `--model ""` not clearing config (PR #3280) suggests power users poke at nullable fields with empty flags.
- **Community contributions are healthy**: 32% of today's PRs originated from external contributors (`adas666`, `amit-shafnir`, `wakqasahmed`, `stumpjumper`, `Koshkoshinsk`, `chubbicorn245`), indicating a **engaged and technically capable user-base**.

## 8. Backlog Watch
Items requiring maintainer attention:

- **PR #2752 (open since June 12, 2026)** — Discord attachment staging. This is **the longest-open PR** in the window and addresses a **core platform integration gap**. Two months without merge suggests either blocking review or design disagreement.
- **PR #1251 (merged after ~5 months)** — OpenMail skill languished since March before merging this week; indicates **external PRs may face long review timelines**, a potential contributor-retention risk.
- **Issue #3233 (referenced by PR #3281)** — Legacy session blindness in `ncl tasks`; PR exists but is **open and unmerged**, linking a confirmed bug to an in-flight fix.
- **PR #3282, #3280, #3283** — Smaller contributor fixes awaiting merge; all authored within the last 48 hours, so no staleness yet — but should be tracked for review turnaround.

---

**Overall assessment:** NanoClaw is in a **hardening-and-protocol phase** — the core team is investing heavily in delivery invariants and multi-session state integrity, while community contributions focus on concrete platform gaps (email, Telegram UX, Discord attachments). The project's health is strong: no fresh regressions, a healthy external-contributor pipeline, and deliberate architectural evolution. The main risk is **review-queue latency** for community PRs, which could dampen contributor momentum if not addressed.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-17

## 1. Today's Overview
IronClaw is in a **steady maintenance and polish phase** with moderate activity. Nine PRs were updated in the last 24 hours, but **only two were closed/merged** — one a trivial config cleanup and one a routine dependency bump. The remaining seven open PRs are mostly Dependabot-driven dependency updates (Rust crates, GitHub Actions) that are accumulating, suggesting a **possible bottleneck in the review/merge cycle** for low-risk automation. The single active issue is a **well-scoped Slack UX enhancement** (unlinked-user onboarding) that already has an associated fix PR open — a sign of healthy issue-to-PR velocity. No new releases this period; the project appears to be consolidating prior feature work (automations, Slack integration) rather than shipping new versions.

## 2. Releases
No new releases were published in the last 24 hours. The project remains between release cycles; the most recent feature work (automation result suppression in PR #7651, Slack nudge fix in #7682) is still in review.

## 3. Project Progress
Two PRs were closed/merged today, both low-risk:

- **[#7683 — chore: remove retired IronLoop network settings](https://github.com/nearai/ironclaw/pull/7683)** *(closed, XS, core contributor)* — Removed obsolete `network_access` fields from trusted repo configuration while retaining existing Implement/Tester/Review/Resolve behaviors. A safety-focused cleanup that simplifies config surface.
- **[#7632 — chore(deps): bump the everything-else group with 4 updates](https://github.com/nearai/ironclaw/pull/7632)** *(closed, M, Dependabot)* — Bumped `base64`, `toml`, `rstest`, and `jsonschema` Rust dependencies. Note: the newer open PR **#7684** re-bumps two of these (base64 to 0.23.1, toml to 1.1.4), indicating the merge of #7632 may have been partial or superseded.

**Notable: no feature work merged today.** The substantive contributions (Slack fix #7682, automation suppression #7651) remain open, suggesting maintainers are prioritizing dependency hygiene over feature landing this cycle.

## 4. Community Hot Topics
- **[Slack unlinked-user connect message (Issue #7681)](https://github.com/nearai/ironclaw/issues/7681)** — The sole active issue, despite low engagement metrics (0 comments, 0 reactions), represents the **highest-signal UX concern**: in shared channels, onboarding nudges are public, and the manual round-trip has no context carry-over. The associated fix PR **#7682** explicitly addresses this with a private, one-click connect link.
- **[feat(automations): deterministic no-result suppression (PR #7651)](https://github.com/nearai/ironclaw/pull/7651)** — Large-scope (XL) feature, open for 3 days with no comments logged. It adds intent-based result delivery (suppress vs. deliver) for automations. The silence suggests either maintainer bandwidth issues or that the design needs more discussion before review.

**Analysis:** The project's "hot" items are not high-traffic discussions but rather **unreviewed substantive work**. The lack of comments on a large-scope feature PR is a risk signal — it may stall without maintainer attention.

## 5. Bugs & Stability
**No new bugs or regressions reported today.** The single open issue (#7681) is more UX/onboarding than a functional bug — the bot works, but the experience is public and clumsy. No crash reports, no security findings in the last 24h.

**Stability outlook:** Low risk. However, seven accumulated dependency-update PRs (base64, toml, tokio-tungstenite, wasm-tools, GitHub Actions) mean the project is **at risk of dependency drift** if not merged soon, particularly `tokio-tungstenite` (#7020, open 15 days) and the `actions` group (#7406, open 8 days, medium risk).

## 6. Feature Requests & Roadmap Signals
- **Private, one-click Slack onboarding (Issue #7681 + PR #7682):** Directly requested via the issue; PR delivers private DM nudge with embedded connect link. High probability of merging next cycle given the author also opened the fix.
- **Deterministic no-result suppression for automations (PR #7651):** Not a user request but a design improvement — derived `result_delivery` from user wording. If merged, it will change automation behavior subtly, likely shipped in the next minor release.
- **IronLoop config cleanup (PR #7683):** Already merged — signals ongoing internal infra modernization.

**Prediction for next release:** Slack onboarding fix (#7682) and the automation suppression feature (#7651) are the leading candidates. Dependency bumps are likely to batch-merge before that.

## 7. User Feedback Summary
The only concrete user pain point this period is from the Slack integration:
- **Pain point:** Onboarding an unlinked user in a shared channel **leaks the nudge publicly** and creates a **multi-step, context-free connection flow** ("what's the link to connect you?" dead-end). The reported thread ends with user confusion.
- **Desired outcome:** Private delivery and one-click action with context preserved.

There is **no negative feedback** on core agent behavior, performance, or reliability in this window. The absence of complaint may indicate satisfaction, but the **low comment count across all items** also suggests a quiet community or one that communicates off-GitHub.

## 8. Backlog Watch
Items accumulating with no maintainer response:
- **[PR #7020 — tokio-tungstenite 0.29 → 0.30 bump](https://github.com/nearai/ironclaw/pull/7020)** — Open **15 days**, low risk. Version 0.30 may contain breaking API changes (per changelog), so it should not be left to rot. Needs review or explicit closure.
- **[PR #7406 — GitHub Actions group bump](https://github.com/nearai/ironclaw/pull/7406)** — Open **8 days**, medium risk. Clangs with CI tooling; the `claude-code-action` bump in particular may alter agent eval behavior.
- **[PR #7651 — Deterministic no-result suppression](https://github.com/nearai/ironclaw/pull/7651)** — Open **3 days**, large scope, **zero comments** from maintainers or contributors. This is the highest-value PR needing design review; silence risks feature rot.
- **[PR #7262 — wasm group bump](https://github.com/nearai/ironclaw/pull/7262)** — Open **12 days**, low risk. Accumulating days without review.

**Maintainer action needed:** Batch-review the small dependency PRs (all are low-risk, Dependabot-driven) and prioritize a design pass on #7651 before it goes stale. The Slack fix (#7682) should move to merge once the dependent issue is triaged.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Based on the GitHub data provided for LobsterAI (github.com/netease-youdao/LobsterAI) for the period ending 2026-08-17, here is the project digest:

---

## LobsterAI Project Digest — 2026-08-17

### 1. Today's Overview

LobsterAI is showing a moderate level of activity with 10 issues and 17 PRs updated in the past 24 hours. A significant portion of this activity is driven by a large backlog of stale items being swept through, with 3 issues and 6 PRs being closed/merged. The most notable development is a wave of **security-focused PRs by `kayo5994`** (addressing log desensitization, IPC access control, and scheme whitelisting), indicating a strong focus on hardening the application. The community is also actively contributing, with several feature PRs (e.g., TTS for AI messages, Agent import/export) from multiple authors. The project health appears stable, with no new releases, but the backlog of stale items is a potential concern that maintainers are actively addressing.

### 2. Releases

No new releases were published in the last 24 hours.

### 3. Project Progress

Nine PRs were merged or closed, signaling significant progress in several areas. The most critical advancement is a **security hardening series** by `kayo5994`, which closed three major vulnerabilities:
- **PR #1831** ([link](https://github.com/netease-youdao/LobsterAI/pull/1831)): Desensitizes sensitive logs in the main process and IM modules (masking Bearer tokens, API keys, auth codes).
- **PR #1832** ([link](https://github.com/netease-youdao/LobsterAI/pull/1832)): Implements key-level access control for the `store:*` IPC channels to prevent unauthorized read/write of sensitive tokens.
- **PR #1833** ([link](https://github.com/netease-youdao/LobsterAI/pull/1833)): Adds a scheme whitelist for `shell.openExternal` to block dangerous protocols (e.g., `file://`, `javascript:`).

Other notable changes include:
- **PR #1690** ([link](https://github.com/netease-youdao/LobsterAI/pull/1690)): Adds a confirmation modal to prevent accidental deletion of IM instances.
- **PR #1691** ([link](https://github.com/netease-youdao/LobsterAI/pull/1691)): Introduces Agent template import/export functionality.
- **PR #1693** ([link](https://github.com/netease-youdao/LobsterAI/pull/1693)): Improves the model setup entry point and fixes a bug where draft input was lost when no model was configured.
- **PR #1715** ([link](https://github.com/netease-youdao/LobsterAI/pull/1715)): Fixes a critical bug where the OpenClaw service proxy was not including the `session_id` in requests.
- **PR #1835** ([link](https://github.com/netease-youdao/LobsterAI/pull/1835)): Removes duplicate error messages in the UI when `continueSession` fails.

### 4. Community Hot Topics

- **Issue #1797** ([link](https://github.com/netease-youdao/LobsterAI/issues/1797)): Request for a feature to delete individual conversations and batch delete invalid ones to keep context relevant. This is a closed issue with 1 reaction, suggesting a desired UX improvement for better context management.
- **Issue #1813** ([link](https://github.com/netease-youdao/LobsterAI/issues/1813)): Reports a failure when using the `DeepSeek V4` model, with an LLM request error about the schema or tool payload. This is a closed issue with 8 comments, indicating a troubleshooting thread that may signal a compatibility issue with a popular model.
- **Issue #1698** ([link](https://github.com/netease-youdao/LobsterAI/issues/1698)): A reproducible bug (100%) detailing a gateway port conflict and process race condition when installing "智企帝王蟹" while LobsterAI is running. This is an open issue with 3 comments and is a high-severity integration problem.
- **PR #1682** ([link](https://github.com/netease-youdao/LobsterAI/pull/1682)): A feature request to add text-to-speech (TTS) functionality for AI replies in the Cowork interface. It remains open, showing community interest in multi-modal feedback.

**Underlying Needs**: The community is focused on reliability (model compatibility, integration stability), privacy/security (token safety), and richer UX features (TTS, conversation management, Agent customization).

### 5. Bugs & Stability

Several bugs were reported, ranked by severity:

- **High Severity**: 
    - **Port Conflict & Process Race** ([Issue #1698](https://github.com/netease-youdao/LobsterAI/issues/1698)): A guaranteed crash/conflict when running alongside another NetEase product ("智企帝王蟹"), rendering the latter unusable. No fix PR is currently linked.
    - **Write Tool Always Fails** ([Issue #1796](https://github.com/netease-youdao/LobsterAI/issues/1796)): A user reports that Write/Edit tools fail persistently *for the last few days*, even after updating the app. This is a critical regression for core functionality, though it has been closed.
- **Medium Severity**:
    - **DeepSeek V4 Incompatibility** ([Issue #1813](https://github.com/netease-youdao/LobsterAI/issues/1813)): The LLM provider rejects the request schema or tool payload for DeepSeek V4. This indicates a potential issue with the tool-calling implementation for this specific model.
    - **Windows 11 Installation Issue** ([Issue #1714](https://github.com/netease-youdao/LobsterAI/issues/1714)): Users on Windows 11 often experience a white, non-functional icon during installation.
    - **Diff Display Broken** ([Issue #1783](https://github.com/netease-youdao/LobsterAI/issues/1783)): The user has located a specific bug in the `extractDiffFromToolInput` function that prevents the UI from showing diffs for file edits.
- **Low Severity**:
    - **Email Connection Incompatibility** ([Issue #1745](https://github.com/netease-youdao/LobsterAI/issues/1745)): The client does not support OAuth2 for Outlook, preventing users from connecting their accounts.

### 6. Feature Requests & Roadmap Signals

The community is actively suggesting new features and improvements, indicating the following potential directions for the roadmap:

- **Conversation Management** ([Issue #1797](https://github.com/netease-youdao/LobsterAI/issues/1797)): Users want the ability to delete or batch-delete conversations to better manage context, a high-demand feature.
- **Model Customization** ([Issue #1688](https://github.com/netease-youdao/LobsterAI/issues/1688)): There is a desire to dynamically adjust model parameters like `temperature` during a conversation.
- **Enhanced Agent Personalization** ([PR #1760](https://github.com/netease-youdao/LobsterAI/pull/1760)): While a PR for image avatars exists, it's still open, suggesting this feature is in progress and not yet released.
- **Accessibility & UX** ([PR #1682](https://github.com/netease-youdao/LobsterAI/pull/1682), [#1769](https://github.com/netease-youdao/LobsterAI/pull/1769), [#1770](https://github.com/netease-youdao/LobsterAI/pull/1770)): A cluster of PRs for UI/UX improvements, including TTS for messages, skeleton loading screens, and better empty states, indicates a continuous focus on polish.

### 7. User Feedback Summary

User sentiment appears mixed due to the backlog of issues, but the active development is a positive sign.

- **Pain Points**: Users are frustrated by functional regressions (Write tool failure) and integration issues (port conflicts). There is also clear dissatisfaction with the inability to connect to Outlook and the lack of basic conversation deletion. The need for a configuration confirmation for destructive actions (IM deletion) was also highlighted.
- **Use Cases**: The requests show a diverse set of use cases, from a personal assistant (TTS, context management) to a development tool (Agent import/export, diff viewing) and an enterprise communication hub (IM integration).
- **Satisfaction**: The rapid response to security vulnerabilities and the merging of features like Agent export suggest the team is responsive, which typically improves user confidence. However, the prolonged existence of stale issues might breed frustration.

### 8. Backlog Watch

Several issues and PRs have been open for a long time and may require maintainer attention.

- **Issue #1698** ([link](https://github.com/netease-youdao/LobsterAI/issues/1698)): The critical port conflict with "智企帝王蟹" has been open for **4 months** with no fix PR. This is a significant integration stability issue that could affect enterprise users.
- **Issue #1744** ([link](https://github.com/netease-youdao/LobsterAI/issues/1744)): A "Bug report" opened on 2026-04-19 with no usable information. It might be a user error or a failed upload; closing this could reduce noise.
- **PR #1765** ([link](https://github.com/netease-youdao/LobsterAI/pull/1765)): A Dependabot PR for `@headlessui/react` has been open for **4 months**. It's a major version bump and likely requires review and potential code changes. It's worth investigating if the breaking changes are manageable.
- **Issue #1714** ([link](https://github.com/netease-youdao/LobsterAI/issues/1714)): The Windows 11 icon issue has been open for several months, suggesting it might be a persistent problem on that platform without a simple fix.
- **PR #1682** ([link](https://github.com/netease-youdao/LobsterAI/pull/1682)): The TTS feature PR has been open for **4 months**. It's a self-contained feature and may just need a final review. If the maintainers are interested, this could be a low-effort, high-impact addition to the community.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-17

## 1. Today's Overview
Moltis saw a significant surge in merged activity over the past 24 hours, with 16 of 17 updated PRs closing or merging, indicating a major stabilization and feature-completion push. The project faces two immediate, merge-blocking issues on `main`: a compilation error in `moltis-gateway` (fixed by PR #1201) and a red CI Format gate due to files exceeding line limits (Issue #1202). Two new bugs were reported — a heartbeat scheduling violation and a newly identified design limitation on the main session — along with continued cleanup and dependency bumps. While no new releases were cut, the high PR throughput and quick bug-fix responses signal a healthy, actively maintained codebase.

## 2. Releases
None published in this period. Previous releases remain the latest published versions.

## 3. Project Progress
The 24-hour window is dominated by a substantial merge spree, highlighting several major feature areas and infrastructure fixes:

- **Major Feature: Durable Connectors (#1190, [closed](https://github.com/moltis-org/moltis/pull/1190))** — A foundational addition introducing provider-neutral connector persistence with atomic snapshots, scheduling, projections, bounded local full-text search, and read-only CalDAV, Gmail, Himalaya v2, and channel-history datasets. This significantly expands Moltis's integration capabilities.
- **Major Feature: zvec Memory Backend (#1158, [closed](https://github.com/moltis-org/moltis/pull/1158))** — A new experimental vector database memory backend (featuring `zvec` and `redb`), feature-gated behind a cargo feature, providing an alternative to the default memory implementation.
- **Major Feature: Slack Native Live Task Cards (#1195, [closed](https://github.com/moltis-org/moltis/pull/1195))** — Introduces channel-neutral tool lifecycle updates rendered as native Slack plan/task cards, protected by opaque per-run IDs and registered canonical tool names.
- **Feature: New Agent Support (#1204, [open](https://github.com/moltis-org/moltis/pull/1204))** — Adds MiniMax Code as an ACP agent (external-agent kind backed by `mcode acp`) with default executable detection and documentation. This is the only actively open PR today.
- **Feature: Channel Activity Log Visibility (#1093, [closed](https://github.com/moltis-org/moltis/pull/1093))** — Adds per-account, per-channel, and per-user `activity_log` visibility settings (`all`, `errors_only`, `off`) with a priority hierarchy that was long in review (created 6/3) and is now merged.
- **Feature: CalDAV Time Ranges (#1147, [closed](https://github.com/moltis-org/moltis/pull/1147))** — Properly honors `list_events` time ranges via RFC 4791 `calendar-query` REPORT requests, including UTC normalization and recurring event expansion.
- **Fix: Main Session Deletion (#1182, [closed](https://github.com/moltis-org/moltis/pull/1182))** — Resolves Issue #1132 by removing the guard that prevented deleting/archiving the "main" session (while keeping the active-channel restriction).
- **Fix: Gateway Compilation (#1201, [closed](https://github.com/moltis-org/moltis/pull/1201))** — A critical fix unblocking the build for `moltis-gateway` caused by a refactor in #1158.
- **Fix: Security Hardening (#1180, [closed](https://github.com/moltis-org/moltis/pull/1180))** — Closes two arbitrary-file-write bug classes via Zip extraction (`clawhub.rs`) and HuggingFace model path validation.
- **Fix: Security — Node Pairing Signatures (#1179, [closed](https://github.com/moltis-org/moltis/pull/1179))** — Binds node pairing verification to the server-issued pending request, preventing caller-supplied keys/challenges.

Additional fixes include vault recovery-phrase normalization (#1186), sandbox gogcli URL correction (#1191), wacrawl skill metadata updates (#1192), macOS bash 3.2 script compatibility (#1194), and a deterministic push fanout test (#1203).

## 4. Community Hot Topics
There is no single heavily debated thread; the project is resolving topics quickly through PRs. The most actively discussed (with comments or broad impact) items are:

- **"Main" Session Behavior — Issue [#1132](https://github.com/moltis-org/moltis/issues/1132)** (1 comment, now closed): The inability to delete/archive the main session. This is a user-facing restriction that was resolved in **PR #1182** (merged), which explicitly re-implemented the guard.
- **Gateway Compilation Break — Issue [#1202](https://github.com/moltis-org/moltis/issues/1202) & PR [#1201](https://github.com/moltis-org/moltis/pull/1201)**: An immediate build breakage that the community responded to with an immediate fix (merged within hours), paired with a separate CI gate issue for file size limits.

The community's activity today centers on **stability and infrastructure**, rather than debate over features.

## 5. Bugs & Stability
Daily bug report volume is low (3 closed, 2 open), and the maintainers have been responsive. Ranked by severity:

1.  **High — Gateway Compilation Break (PR #1201, [closed](https://github.com/moltis-org/moltis/pull/1201))**: A hard compile error on `main` (`start_background_tasks` not found) in `crates/gateway/src/server/init_memory.rs`. The fix was merged quickly. Also blocked the flaky test fix (#1203) from building in isolation.
2.  **Medium — Heartbeat Scheduling Ignored (Issue [#1205](https://github.com/moltis-org/moltis/issues/1205), [open](https://github.com/moltis-org/moltis/issues/1205))**: The heartbeat runs continuously, ignoring configured active hours. This is a behavioral regression/oversight, unresolved as of this digest. No fix PR is listed yet.
3.  **Low — Flaky Fanout Timeout Test (Issue [#1193](https://github.com/moltis-org/moltis/issues/1193), [closed](https://github.com/moltis-org/moltis/issues/1193))**: A CI test (`fanout_is_bounded_and_times_out_a_hung_endpoint`) was failing intermittently under full-suite load. Fixed by running on a paused clock (PR #1203).
4.  **Low — Format CI Gate Red (Issue [#1202](https://github.com/moltis-org/moltis/issues/1202), [open](https://github.com/moltis-org/moltis/issues/1202))**: `store.rs` (1799 lines) and `admin.rs` (1531 lines) exceed the 1500-line limit. A minor CI hygiene issue that will block merges until resolved.

Other resolved bugs this week from earlier reporting: Sandbox build failure (#1189, fixed in #1191), main session deletion bug (#1132, fixed in #1182).

## 6. Feature Requests & Roadmap Signals
The commits today signal a clear roadmap direction toward **durability and integration breadth**:

- **Provider-Neutral Connectors (#1190)**: This is the strongest signal. The introduction of durable calendar/channel/email connectors, with atomic snapshots and scheduling, suggests a major push toward making Moltis a reliable, long-running background service rather than a just-in-time assistant. Expect more connector types (e.g., Slack, Teams, more email providers) to be built on this foundation in the next versions.
- **Agent Ecosystem Expansion (#1204)**: MiniMax Code support is the first of likely many new named ACP agents. The "keep everything in sync" mention (config validation, UI fixtures, docs) indicates the framework is now mature enough for rapid agent additions.
- **Platform-Native UI (#1195)**: The Slack live task cards are an initial step toward reducing UI boilerplate for users. "Channel-neutral tool lifecycle updates" hints at a generic infrastructure that other platforms (Discord, Teams) can adopt.
- **Alternative Memory Backends (#1158)**: The zvec vector-database backend establishes a precedent for pluggable memory. However, it introduces a significant code size (`store.rs` at 1799 lines) that triggers the CI gate, suggesting this might need refactoring for size before broader adoption.

## 7. User Feedback Summary
Direct user inputs via issues are limited, but actionable; the community is reporting real edge cases, and maintainers are responding.

- **Pain Point (Resolved)**: "Main" session cannot be deleted/archived (#1132). A structural design limit that was removed in latest merge (#1182), allowing users full control over session lifecycle.
- **Pain Point (Active)**: Heartbeat ignores active-hours config (#1205). A configuration contract is being broken, causing unexpected background activity; this directly affects users who rely on "do not disturb" windows.
- **Pain Point (Tooling)**: CI gates block development on macOS (Immediate fix #1194; broader issue of path/script portability).
- **Security Consciousness**: Community members are proactively submitting security fixes (e.g., #1180 and #1179) before adopting Moltis, indicating a user base with high security expectations.

Overall, the signal is positive: bugs are fixed quickly, the contributor base is growing and engaged, and the latest merges directly address user-visible complaints.

## 8. Backlog Watch
No severe stagnation; however, a few items merit attention:

- **Open Feature PR — MiniMax Code Agent ([#1204](https://github.com/moltis-org/moltis/pull/1204))**: The only open PR, from a new contributor. It requires review and likely CI fixes (the branch is new). Timely review encourages further community contributions.
- **Issue #1202 — Line Limit Violations**: Though not a "long-term" stalled item, it is a merge-blocking CI gate that must be addressed (likely by refactoring `store.rs`/`admin.rs` or raising the limit) to keep the `main` branch healthy.
- **Issue #1205 — Heartbeat Config**: Currently unclaimed; it is a subtle behavioral bug that could require deeper investigation into the scheduling loop, but no PR exists yet.

No other community PRs have been waiting over a week without maintainer interaction; the project remains remarkably responsive.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-17

## 1. Today's Overview

CoPaw shows moderate activity over the past 24 hours: 9 issues and 9 PRs were updated, with 3 issues closed and no PRs merged. The project remains healthy overall — issues are being triaged and closed, and a significant influx of **first-time contributor** PRs (8 of 9) signals a growing external community. However, an unresolved crash bug (#7063) and a high-frequency runtime crash report (#7074) warrant attention. Notably, all open PRs are from external contributors awaiting review, suggesting maintainer bandwidth may be a constraint. No new releases were published today.

## 2. Releases

No new releases were published in the last 24 hours. The latest known version remains **v2.1.0** (referenced in recent issues), with no release-related activity to report.

## 3. Project Progress

**Merged/Closed PRs:** No PRs were merged or closed today. All 9 PRs remain open, with one (#6940) flagged as `ready-for-human-review`.

**Active PRs awaiting review (notable):**
- **#6302** (open since Jul 21) — Major refactor unifying provider discovery, model metadata, routing, and agent controls. This is the most substantial pending PR (17+ days open), suggesting either high complexity or reviewer bandwidth issues.
- **#6940** — Adds a native "DataPaw" app runtime and durable analysis workspace; includes screenshots and references an infra repo. Marked `ready-for-human-review` since Aug 12 — 5 days awaiting review.

**Fixes submitted (all by first-time contributor suantea, pending review):**
- **#7066** — Fix for OAuth2 rotating refresh_token not being persisted for remote MCP servers (fixes #7053)
- **#7069** — Fix for data-URL images not rendering in chat history on session reload (fixes #7051)
- **#7070** — Fix for `view_video` silently failing on OpenAI Responses API path (fixes #7059)
- **#7071** — Makes `view_video` inline cap configurable instead of hardcoded 2 MB (fixes #7060)
- **#7064** — Fixes `cron update --text` not syncing top-level text field (fixes #7048)

## 4. Community Hot Topics

**Most discussed items (3 comments each):**

- **[#7063 — Crash on every tool call](https://agentscope-ai/QwenPaw Issue #7063)** — *[CLOSED]* — A `TypeError` in `_execute_tool_call` where `async for` is used on a coroutine returned by `_acting()`. The bug was reported, discussed, and closed within 24 hours — the fastest resolution cycle today, suggesting good maintainer responsiveness to critical issues.

- **[#7003 — ViBo memory proposal for QwenPaw](https://agentscope-ai/QwenPaw Issue #7003)** — *[CLOSED]* — Proposal for a memory solution claiming "97.5% fewer tokens" via encrypted external memory. Referenced the project's 33,748 stars. Closed without adoption, but the underlying need (memory persistence across sessions) remains a community pain point.

- **[#6471 — Cron tasks misfire after event loop idle](https://agentscope-ai/QwenPaw Issue #6471)** — *[CLOSED]* — APScheduler `AsyncIOScheduler` not firing after long idle periods. Closed after ~3 weeks open. This is the oldest issue in today's batch.

**Analyzing community needs:** The ViBo proposals and #7003 show users are actively investing in memory solutions for agents — a signal that built-in memory/context management is a top feature gap. The cluster of `view_video` fixes (#7059, #7060, #7070, #7071) indicates real-world multimodal usage is hitting edge cases that need hardening.

## 5. Bugs & Stability

Ranked by severity:

**High:**
- **#7063 — Agent crashes on every tool call** (CLOSED) — `TypeError: 'async for' requires an object with __aiter__ method, got coroutine` in `_execute_tool_call`. Version v2.1.0. **Fix status:** Closed within 24h with 3 comments — likely a known issue with a workaround or quick fix.

- **#7074 — Frequent runtime crashes requiring page refresh** (OPEN) — High-frequency crashes reported; logs show session state loading from `session.py:454`. One comment; no fix PR yet identified.

**Medium:**
- **#7065 — Cannot view chat history after 7+ rounds** (OPEN) — Only last 3-4 messages visible; scrolling to top doesn't reveal earlier discussion. Related: **#7069** (PR fixing data-URL image rendering in history) may partially address this class of issue.

- **#6471 — Cron task misfire after idle** (CLOSED) — APScheduler `AsyncIOScheduler` not firing. Closed after 21 days; users on v2.0.1 affected.

## 6. Feature Requests & Roadmap Signals

**Requested features (with signals for next version):**

- **#7052 — `system_prompt` permission for plugin API** (OPEN) — Enterprise need: companies want to hide their internal system prompts from end users in session UI. Business-critical for plugin ecosystems.

- **#7062 — Per-agent/per-session `reasoning_effort` override** (OPEN) — Users want different thinking depths for different roles (quick Q&A vs deep research). This aligns with PR #6302's "agent model controls" theme, suggesting it may already be on the roadmap.

- **#7068 — File/script viewer support for C#, shader files (.shader, .gdshader, .hlsl)** (OPEN) — Game-dev workflow gap; low complexity request.

- **#7073 — Skill name deduplication** (OPEN) — Technical deep-dive PR to prevent duplicate loading of workspace and built-in skills. This is a PR-as-feature, indicating the contributor wants to fix it themselves.

- **#7003 — ViBo memory solution** (CLOSED) — External proposal not adopted, but memory persistence remains a repeated community request.

**Predictions for next version:** The `reasoning_effort` per-agent feature (#7062) has a strong chance of landing, as PR #6302 (provider/agent controls unification) seems designed to enable it. The plugin API `system_prompt` control (#7052) is likely for enterprise adoption.

## 7. User Feedback Summary

**Pain points:**
- **Cost of memory** — Users building agents report high costs from sending full memory with every request; ViBo proposer called it "costs a fortune" (#7003).
- **Chat history reliability** — Losing visibility of earlier messages after several rounds (#7065) and history mismatches between backend/frontend data handling.
- **Silent failures** — `view_video` showing "Video loaded" but never passing frames to the model (#7059); OAuth refresh tokens expiring silently (#7053).
- **Enterprise privacy** — Companies want to inject system prompts without exposing them to end users in the session UI (#7052).
- **Cron reliability** — Scheduled tasks misfiring after idle periods (#6471) undermines trust in automation.
- **Crash frequency** — One user reports crashes happening frequently enough to need page refresh each time (#7074).

**Satisfaction signals:** Fast turnaround on the critical crash (#7063 closed within 24h) is positive. The project's 33k+ stars are referenced by community members. First-time contributors are actively submitting PRs — a sign of project attractiveness — but their PRs sit unreviewed, which could discourage repeat contributions if maintainers don't engage soon.

## 8. Backlog Watch

**PRs needing maintainer attention (no comments/reviews visible):**

- **[#6302 — Provider/model system unification](https://agentscope-ai/QwenPaw PR #6302)** — *OPEN since Jul 21 (27 days)* — This is the project's most complex pending PR. Being unmerged for nearly a month could signal either substantial review workload or maintainer disagreement. Its themes (model routing, agent controls) overlap with user requests (#7062), making this a high-priority review.

- **[#6940 — DataPaw app runtime (ready-for-human-review)](https://agentscope-ai/QwenPaw PR #6940)** — *Waiting 5 days* — Marked "ready-for-human-review" with extensive screenshots. A significant feature addition that may be waiting on maintainer availability.

- **[#6471 — Cron misfire issue](https://agentscope-ai/QwenPaw Issue #6471)** — *Closed after 21 days* — While closed, the 21-day gap between creation (Jul 26) and update (Aug 16) suggests slow triage for some issues. Worth monitoring whether the APscheduler fix ships in a future release.

**Potential risk:** With 8 of 9 PRs from first-time contributors (all created Aug 16) waiting for review, there is a **contributor retention risk** — fast, engaged newcomers may lose momentum if responses don't come soon. Maintainer bandwidth appears to be the current bottleneck.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest
**Date: 2026-08-17**

---

## 1. Today's Overview

ZeroClaw is in a period of **intense architectural renovation**, with 96 open items across Issues and PRs showing extremely high contributor activity. The project is currently processing a significant wave of RFCs focused on core architecture: wire protocols for OpenAI-compatible clients, unified attachment handling, security posture definitions, and plugin egress policies. Notably, the maintainer decision queue ([#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)) is actively triaging the high-volume design discussions. While no new releases shipped in the last 24 hours, the recent 0.8.4 milestone is under rollout, and the development velocity suggests the next minor version will be substantial, potentially bringing native OpenAI-compatible API support, a hardened plugin egress policy, and tighter security controls.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

Four PRs were merged or closed, with no new releases. The closed/merged activity included:

- **[#9580 — fix(security): harden built-in HTTP egress on the shared network guard](https://github.com/zeroclaw-labs/zeroclaw/pull/9580)** (merged, size:XL, priority:p1): A major security hardening PR that **lays the foundation for the plugin egress policy** (ADR-013). Key changes include:
  - Rejecting all audited non-global IPv4/IPv6 addresses in built-in HTTP egress.
  - Moving shared network-classification primitives into `zeroclaw-infra::net_guard` for reuse by the plugin egress work.
  - Acting as the dependency base for two other open PRs ([#9137](https://github.com/zeroclaw-labs/zeroclaw/pull/9137), [#10046](https://github.com/zeroclaw-labs/zeroclaw/pull/10046)) which stack on its head.

- **[#9416 — docs(tools): document that AllToolsResult.tools is the pre-filter registry](https://github.com/zeroclaw-labs/zeroclaw/pull/9416)** (merged, size:XS): A small docs fix clearing up a subtle semantic distinction around the `AllToolsResult` field naming.

- **[#9953 — [Bug]: SOP step schema validation rejects a double-encoded output object](https://github.com/zeroclaw-labs/zeroclaw/issues/9953)** (closed): Bug in runtime/daemon where a double-encoded JSON string was rejected instead of unwrapped.

- **[#10013 — [Bug]: Edge TTS cancellation test can miss fake child startup under parallel load](https://github.com/zeroclaw-labs/zeroclaw/issues/10013)**: A follow-up test-fix was pushed, making the parallel test job stable.

This activity underscores that **security is the dominant theme**: the egress policy is a multi-stage rollout, and other security-focused PRs (knowledge graph attribution, attack surface reducers) continue to land.

---

## 4. Community Hot Topics

The most active discussions revolve around the most fundamental architectural decisions:

- **[#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)** (23 comments) — **Author: Audacity88**: A continuously revised roadmap/rfc tracker (Rev. 25). Signals a strong, governance-focused maintainer culture with a clear process for shepherding complex changes.

- **[#8603 — RFC: ZeroClaw Chat Completions profile](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)** (22 comments) — **Author: REL-mame**: A direct response to ecosystem demand. The need to speak the OpenAI protocol to integrate with Open WebUI, LobeChat, Aider, etc. demonstrates that **users want ZeroClaw to drop into existing toolchains** rather than being an island.

- **[#9488 — RFC: Unified attachment architecture for web chat and channels](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)** (17 comments) — **Author: NiuBlibing**: The need to unify how files/images/attachments flow through different channels (Telegram, Web, etc.) is a classic pain point as channels multiply.

- **[#6954 — RFC: Provenance, conversation binding, and reply contract for internally initiated agent turns](https://github.com/zeroclaw-labs/zeroclaw/issues/6954)** (14 comments) — **Author: mov-xound-glitch**: Deep design work on *when an agent calls another agent* (internally initiated) — who owns the conversation, how replies are routed. A major piece of agent-mesh architecture.

- **[#6971 — RFC: Security posture, credential boundaries, and universal ingress policy](https://github.com/zeroclaw-labs/zeroclaw/issues/6971)** (14 comments) — **Author: Audacity88**: A security "grand view" RFC attempting to unify all the security controls and make them inspectable.

- **[#8692 — [Tracker]: Maintainer decision queue for RFCs and design issues](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)** (13 comments) — The sheer volume of design discussion requires meta-organization. The bot-moderated queue itself is a hot topic, suggesting these decisions are not quick.

The underlying need: the community is **pushing for ZeroClaw to be a modular, secure, and interoperable hub** rather than a monolithic stack.

---

## 5. Bugs & Stability

Multiple high-severity (P1) bugs with acceptance status are under active investigation, indicating a strong QA culture.

- **S1 — Workflow blocked:**
  - [#10013 — [Bug]: Edge TTS cancellation test can miss fake child startup under parallel load](https://github.com/zeroclaw-labs/zeroclaw/issues/10013): Intermittent CI failure, but a follow-up fix appears to be in place.

- **S2 — Degraded behavior (High Risk):**
  - [#9655 — [Bug]: approval cards carry no position, so back-to-back cards from one message are indistinguishable before tapping](https://github.com/zeroclaw-labs/zeroclaw/issues/9655) — **Author: ZiBibro**: A UX/security issue where multiple pending approvals from the same message can't be told apart in the UI. Potential for mis-approval.
  - [#9811 — /health reports a channel healthy that has never connected](https://github.com/zeroclaw-labs/zeroclaw/issues/9811) — **Author: bryankwandou**: Reports wildly misleading health status for a Telegram channel with an invalid token. No fix PR visible.
  - [#9965 — [Task]: runtime-written executable test fixtures hit ETXTBSY under the parallel runtime gate](https://github.com/zeroclaw-labs/zeroclaw/issues/9965): A stubborn test flakiness issue.
  - [#10020 — [Bug]: Agentic independent delegates ignore the target thinking policy](https://github.com/zeroclaw-labs/zeroclaw/issues/10020) — **Author: vrurg**: Sub-agents don't respect the thinking budget, leading to unexpected costs/time.
  - [#10037 — [Bug]: POST /api/cron silently stores invalid session_target as isolated](https://github.com/zeroclaw-labs/zeroclaw/issues/10037) — **Author: zyw02**: API accepts invalid values instead of rejecting them, leading to silent misconfiguration.

**Fix availability:** PRs are associated with security-focused bugs. [#9580](https://github.com/zeroclaw-labs/zeroclaw/pull/9580) fixes the broad HTTP egress issue. No fix PRs yet exist for #9811, #10020, or #10037.

---

## 6. Feature Requests & Roadmap Signals

The RFC queue points directly at the features most likely to land in the next releases.

- **Likely in next minor (0.9.x):**
  - **OpenAI-compatible chat completions** ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)): High demand and a clear protocol. If ratified, it instantly makes ZeroClaw usable by a huge ecosystem.
  - **Unified attachment architecture** ([#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)): Blocking UX consistency across channels.
  - **Plugin egress policy** (PRs in staging): The multi-PR rollout ([#9584](https://github.com/zeroclaw-labs/zeroclaw/pull/9584), [#9582](https://github.com/zeroclaw-labs/zeroclaw/pull/9582), [#9137](https://github.com/zeroclaw-labs/zeroclaw/pull/9137)) is actively moving. This is a major security feature for WASM plugins.

- **Potential for 0.10+ (longer horizon):**
  - **Realtime speech-to-speech** ([#8780](https://github.com/zeroclaw-labs/zeroclaw/issues/8780)): A major feature that would position ZeroClaw in the voice space.
  - **Ephemeral agent swarms** ([#10025](https://github.com/zeroclaw-labs/zeroclaw/issues/10025)): A TUI for spinning up agent teams quickly. Shows a move toward advanced orchestration/scheduling.
  - **Staged product telemetry** ([#9621](https://github.com/zeroclaw-labs/zeroclaw/issues/9621)): For maintainers to make data-driven decisions — a clear sign of a maturing project.

---

## 7. User Feedback Summary

The discussions in the hot RFCs and user-reported bugs paint a clear picture of user sentiment:

- **Frustration with configuration files:** Several features (e.g., agent swarms [#10025](https://github.com/zeroclaw-labs/zeroclaw/issues/10025)) are requested because users find "config surgery" a barrier. The "no orchestrator" comment directly laments the need to manually wire agents via toml.
- **Integration desire:** The number of comments on the OpenAI-compat RFC and the "prefer a lighter core" RFC ([#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)) shows users want to bring their own tools. The "lighter core" discussion suggests the project may have feature-bloat perception.
- **Operational safety concerns:** Bugs like the approval cards ([#9655](https://github.com/zeroclaw-labs/zeroclaw/issues/9655)) and false health reports ([#9811](https://github.com/zeroclaw-labs/zeroclaw/issues/9811)) rub sourly with operators. The /health bug in particular can undermine trust in the system's monitoring.
- **Corporate/team use case:** The Telegram shared-group session improvement ([#9772](https://github.com/zeroclaw-labs/zeroclaw/pull/9772)) explicitly addresses multi-user collaboration pain in a shared channel. This is a clear B2B / team-collaboration signal.

---

## 8. Backlog Watch

There are several high-priority items wandering in the backlog that require maintainer eyes. The **maintainer decision queue tracker ([#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692))** is the central watch-list.

- **Long-pending RFCs (needs maintainer review):**
  - [#8396 — RFC: Make wire protocol first-class in provider construction and onboarding](https://github.com/zeroclaw-labs/zeroclaw/issues/8396) — 7 comments, filed 2026-06-27, still `needs-maintainer-review`. If #8603 (OpenAI profile) is ratified, this foundational RFC should be unblocked as it affects the same architectural layer.
  - [#6165 — RFC: Prefer a lighter ZeroClaw core through external integrations](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) — 14 comments, filed 2026-04-27, still under review. This will dictate the *future direction* of the project's footprint.

- **Stalled but Critical:**
  - [#7822 — RFC: WASM plugin lifecycle hook subscriptions](https://github.com/zeroclaw-labs/zeroclaw/issues/7822) — `needs-author-action`, stale since last author response. A minor author update is needed to keep it moving. A blocking issue for rich plugin ecosystems.

- **PRs requiring attention:**
  - **Dependency update pressure**: [#9808 — 46 dependency updates](https://github.com/zeroclaw-labs/zeroclaw/pull/9808) is a giant bump that can cause subtle breakage. Prioritize a dedicated CI run.
  - The **large PR stack** (e.g., [#9109](https://github.com/zeroclaw-labs/zeroclaw/pull/9109), [#9126](https://github.com/zeroclaw-labs/zeroclaw/pull/9126)) all list `needs-author-action` or `needs-maintainer-review`. With several sizable, high-risk PRs pending (size:XL), a maintainer-led focus sprint is needed to avoid a growing merge queue and stale branches.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*