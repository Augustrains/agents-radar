# OpenClaw Ecosystem Digest 2026-08-26

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-26 00:32 UTC

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
**Date:** 2026-08-26

---

## 1. Today's Overview

OpenClaw is in a high-intensity stabilization period, with 500 issues and 500 PRs updated in the last 24 hours. The project shows strong engagement with 437 open/active issues being actively triaged and 244 PRs merged/closed in the same window. Activity is concentrated on the **2026.8.1 beta cycle**, with **13 P0/P1 bugs** filed in the last week, including a critical SQLite corruption regression (#126821) and multiple message-loss defects in delivery pipelines. The maintainer team is actively labeling and reviewing issues (`clawsweeper:needs-maintainer-review` on ~30 items), indicating a well-organized triage process. No new releases landed today, suggesting the team is consolidating fixes for the next beta release rather than shipping new features.

---

## 2. Releases

**No new releases published today.** The current beta remains [v2026.8.1-beta.3](https://github.com/openclaw/openclaw/releases/tag/v2026.8.1-beta.3), with monitoring issue [#125626](https://github.com/openclaw/openclaw/issues/125626) tracking feedback and blocking issues for GA. Field reports from beta.7 (#128067) indicate six reliability defect classes are being tracked, suggesting a beta.4 or release candidate may land soon.

---

## 3. Project Progress

**63 issues closed** and **244 PRs merged/closed** in the last 24 hours. Notable merged/closed PRs:

- **[#129638](https://github.com/openclaw/openclaw/pull/129638)** `[CLOSED]` — **Session catalog isolation fix** (S-size): Prevents process-user HOME session catalog entries from leaking into named/relocated state profiles.
- **[#129626](https://github.com/openclaw/openclaw/pull/129626)** `[CLOSED]` — **Schema v10 cleanup**: Retires six dead shared-state tables (`agent_model_catalogs`, `android_notification_recent_packages`, `command_log_entries`, etc.), simplifying the state database.
- **[#120176](https://github.com/openclaw/openclaw/pull/120176)** `[CLOSED]` — **iOS voice permission sharing refactor** (S-size): Shares voice permission support across iOS surfaces.
- **[#125471](https://github.com/openclaw/openclaw/pull/125471)` `[CLOSED]` — **Claude CLI OAuth preservation**: Ensures refresh ownership survives Gateway restarts, fixing a broken OAuth flow.
- **[#129371](https://github.com/openclaw/openclaw/pull/129371)** `[CLOSED]` — **Automation attribution fix**: Agent-created automations now correctly appear under the creating session.

**Notable open progress:**
- **[#129707](https://github.com/openclaw/openclaw/pull/129707)** — **Control UI composer redesign** (XL-size): Unified slash command and skill invocation sheets, rebased onto main.
- **[#127076](https://github.com/openclaw/openclaw/pull/127076)** — **Chat transcript attachment structure** (XL-size, +2,435/-536): Adds dedicated rendering, lifecycle, and ownership for file attachments in chat.
- **[#128371](https://github.com/openclaw/openclaw/pull/128371)** `[CLOSED]` — **Release validation bypass for beta.3**: Authorizes focused beta evidence to unblock the frozen candidate.

---

## 4. Community Hot Topics

| Issue/PR | Comments | Topic | Analysis |
|----------|----------|-------|----------|
| [#125626](https://github.com/openclaw/openclaw/issues/125626) | 18 | OpenClaw 2026.8.1 beta feedback | Beta blocker tracking; community reporting regressions |
| [#80319](https://github.com/openclaw/openclaw/issues/80319) | 17 | QA tool-defaults suite conflates Codex-native tools | Architecture question: how Codex tools map to OpenClaw's dynamic parity layer |
| [#79902](https://github.com/openclaw/openclaw/issues/79902) | 14 | SQLite transcript/session seams for companion apps | Demand for programmatic access to session state |
| [#67777](https://github.com/openclaw/openclaw/issues/67777) | 13 | Subagent completion delivery lost on timeout/drain | **P1 reliability bug** — new architecture needed for subagent acknowledgements |
| [#114612](https://github.com/openclaw/openclaw/issues/114612) | 9 | SQLite unbounded growth (memory tables) | Production disk-fill concern; needs retention policy |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | 9 | Zombie process accumulation from hooks/tools | Long-running gateway degradation issue |
| [#67413](https://github.com/openclaw/openclaw/issues/67413) | 9 (👍 5) | Per-agent dreaming configuration | Memory spikes; most-upvoted feature request in active set |
| [#92633](https://github.com/openclaw/openclaw/issues/92633) | 9 | `memory_search corpus=all` times out | Slow regression; severity P1 |
| [#45758](https://github.com/openclaw/openclaw/issues/45758) | 9 | YAML config file support | Recurring user preference for YAML over JSON5 |

**Underlying needs:** The top issues reveal three themes: (1) **reliability under production load** (message loss, zombies, SQLite growth), (2) **better observability/control** (session state access, per-agent config), and (3) **configuration ergonomics** (YAML, model validation).

---

## 5. Bugs & Stability

**Critical (P0/P1) — 6 new/updated today:**

| Issue | Severity | Description | Fix Status |
|-------|----------|-------------|------------|
| [#126821](https://github.com/openclaw/openclaw/issues/126821) | **P0** | SQLite corruption recurs on pristine DBs every 15–24h (5 events/5 days) — "paralyzed gateway" mode | No fix PR; beta blocker candidate |
| [#128067](https://github.com/openclaw/openclaw/issues/128067) | **P1** | beta.7 field report: 6 reliability defect classes (persistence, delivery, restart-recovery) | No fix PR; broad stabilization needed |
| [#127710](https://github.com/openclaw/openclaw/issues/127710) | **P1** | Prepared-model-runtime fails closed on fingerprint drift — permanently wedges gateway; owner-commit race drops messages | No fix PR |
| [#127948](https://github.com/openclaw/openclaw/issues/127948) | **P1** | WhatsApp group replies render as BLANK bubbles when quote cache expired | Linked PR open |
| [#126246](https://github.com/openclaw/openclaw/issues/126246) | **P1** | Telegram durable outbound deliveries stuck in `send_attempt_started`, lost on restart | No fix PR |
| [#126900](https://github.com/openclaw/openclaw/issues/126900) | **P1** | `maxActiveTranscriptBytes` loops compaction forever, channel wedges | Linked PR open |
| [#126631](https://github.com/openclaw/openclaw/issues/126631) | **P1** | Sandbox skills bind-mount root-owned `/workspace/.openclaw` — locks out uid 1000 | Linked PR open |
| [#125570](https://github.com/openclaw/openclaw/issues/125570) | **P1** | Skill Workshop update overwrites live skill description, breaks routing | No fix PR |

**Pre-existing P1s with active scrutiny:**
- [#67777](https://github.com/openclaw/openclaw/issues/67777) — Subagent completion delivery loss (direct-announce timeout/drain/orphan)
- [#97616](https://github.com/openclaw/openclaw/issues/97616) — Zombie process leak from hook/tool execution
- [#92633](https://github.com/openclaw/openclaw/issues/92633) — `memory_search corpus=all` timeout (fix proposed in #129706 for Ollama variant)

**Trends:** 2026.8.1-beta is showing concentrated **delivery reliability** (Telegram, WhatsApp, Buzz, WebSocket) and **state persistence** (SQLite, session) defects. The team is actively prioritizing these with `clawsweeper:source-repro` and `clawsweeper:linked-pr-open` labels.

---

## 6. Feature Requests & Roadmap Signals

**High-demand requests likely to land in 2026.9.x:**

1. **[#67413](https://github.com/openclaw/openclaw/issues/67413)** — **Per-agent dreaming configuration** (👍 5): OOM prevention via staggered memory dreaming. Strong production need.
2. **[#26037](https://github.com/openclaw/openclaw/issues/26037)** — **Ali Bailian coding plan support** (thinking/reasoning): China-market LLM provider parity.
3. **[#51441](https://github.com/openclaw/openclaw/issues/51441)** — **Expose resolved backend model in session_status**: LiteLLM routing transparency.
4. **[#79902](https://github.com/openclaw/openclaw/issues/79902)** — **SQLite transcript/session seams**: Companion-app programmatic access (diamond-lobster rated).
5. **[#954/9016](https://github.com/openclaw/openclaw/issues/9016)** — **OpenRouter cost exposure**: Per-message cost tracking for agents.

**Recent PRs signaling roadmap direction:**
- **[#129670](https://github.com/openclaw/openclaw/pull/129670)** — **Credential vault for agent-requested API keys**: User can hand keys to the agent without exposing them in transcript. Security-conscious feature, likely to land.
- **[#112811](https://github.com/openclaw/openclaw/pull/112811)** — **Multi-bot Microsoft Teams support**: Enterprise multi-agent scenario.
- **[#129649](https://github.com/openclaw/openclaw/pull/129649)** — **Fix broken SSH tunnel commands for discovered gateways**: Developer-experience polish.

**Early signals:** Accessibility (TUI emoji toggle, VoiceOver chat history) and YAML config (#45758) remain niche but persistent requests.

---

## 7. User Feedback Summary

**Satisfaction themes:**
- **Positive reaction** to usage display placement near model selector (#95601): VoiceOver user appreciates keyboard-reachable UX improvements.
- **Gratitude** for accessibility-focused changes in v2026.6.9, with continued requests (VoiceOver chat history).

**Primary pain points from field reports:**

1. **Message loss is the #1 killer.** 5+ distinct P1 issues today across Telegram, WhatsApp, Buzz, and subagent delivery. Users running production multi-agent gateways are losing visible replies with no logs explaining why.
2. **SQLite instability erodes trust.** The P0 recurring corruption (#126821) and unbounded growth (#114612) are the most alarming findings — users rebuilding pristine DBs report corruption within 15–24 hours.
3. **Context/memory limits impact actually using agents.** `memory_search corpus=all` timing out (#92633) and dreaming OOM (#67413) make long-term memory effectively unusable for some 25-agent production deployments.
4. **Configuration foot-guns:** Unvalidated model names (#39811), session status values misleading agents (#64103), and silent reply suppression ignoring policy (#119401) indicate the runtime needs defensive input validation.

**Feedback quality:** Users provide detailed logs, reproduction steps, and 3-week field evidence (as in #128067). The maintainer team responds with precise labels and linked PRs, suggesting a responsive loop.

---

## 8. Backlog Watch

**Long-standing items needing maintainer attention:**

| Issue | Age | Priority | Reason for Watch |
|-------|-----|----------|------------------|
| [#16670](https://github.com/openclaw/openclaw/issues/16670) | ~6 months | P2 | Onboarding wizard omits mandatory Memory/Embedding setup. New users hit invisible `memory_search` failures. |
| [#39811](https://github.com/openclaw/openclaw/issues/39811) | ~6 months | P2 | Unvalidated model names silently misconfigure. Easy fix; shipping now prevents support load. |
| [#56217](https://github.com/openclaw/openclaw/issues/56217) | ~5 months | P1 | 1Password secret-provider crash-loop exhausts rate limits. Linked PR open but old. |
| [#80178](https://github.com/openclaw/openclaw/issues/80178) | ~3.5 months | P1 | CLI auth epoch invalidates sessions on storage flip — identity unchanged. Diamond-lobster rated. |
| [#45758](https://github.com/openclaw/openclaw/issues/45758) | ~5 months | P3 | YAML config support. Low urgency but high visibility. |
| [#119401](https://github.com/openclaw/openclaw/issues/119401) | ~3 weeks | P1 | `NO_REPLY` suppression ignores `silentReply` policy on small models — behavior regression. |

**Risk flags:**
- **#126821 (P0)** has no fix PR after 6 days — should be elevated to beta-blocker status if not already.
- **#128067** consolidates 9 defect classes from beta.7; needs a single tracking issue with sub-issues to prevent splintering.
- **#79902** (SQLite seams) remains open for 109 days despite being foundational for companion app ecosystem growth.

---

*Generated 2026-08-26 from openclaw/openclaw GitHub data.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem
**Date:** 2026-08-26

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is in a **high-intensity stabilization and hardening phase**, with the dominant players (OpenClaw, ZeroClaw, CoPaw, NanoBot, Hermes Agent) all converging on reliability improvements, security hardening, and delivery-pipeline fixes rather than new feature velocity. Across projects, recurring themes include **message-delivery reliability** (Telegram/WhatsApp/Slack failures), **state-persistence integrity** (SQLite corruption, memory leaks), **sandbox isolation security**, and **MCP (Model Context Protocol) ecosystem maturation**. A clear architectural split is emerging: Rust-based implementations (OpenClaw, ZeroClaw, NullClaw, IronClaw) are prioritizing security boundaries and performance, while Python/TypeScript-based projects (CoPaw, NanoBot, LobsterAI) focus on UX polish and channel integrations. The ecosystem is also witnessing a **push toward distributed/edge compute** (PicoClaw #3345, NullClaw #994, ZeroClaw #10360), signaling a possible next-wave shift from single-device assistants to household/enterprise mesh topologies.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score (1-10) | Notes |
|---------|-------------|-----------|----------------|---------------------|-------|
| **OpenClaw** | 500 updated / 437 open | 500 updated / 244 merged | No new; v2026.8.1-beta.3 | **6.5** | High-intensity stabilization; 13 P0/P1 bugs in week; critical SQLite P0 unresolved |
| **NanoBot** | 5 new / 5 open | 24 updated / 14 merged | No new; between versions | **8.0** | Strong fix pipeline; all P1s addressed; excellent contributor feedback loop |
| **Hermes Agent** | 50 updated / 40 open | 50 updated / 14 merged | No new; v0.20.5 (Aug 19) | **6.0** | Desktop instability; macOS permission resets; xAI provider broken; high community engagement |
| **PicoClaw** | 4 updated / 0 new | 1 updated / 0 merged | No new; 0.3.1 | **4.5** | Stagnant; critical MCP hang unresolved (37 days); stale backlog |
| **NanoClaw** | 5 new / 5 open | 50 updated / 16 merged | No new; imminent RC | **8.5** | High velocity; strong merge rate; setup-ecosystem focus; skills-layer robustness issues |
| **NullClaw** | 1 updated / 0 new | 0 | No new | **5.0** | Low activity; sole focus on edge mesh RFC; no code changes |
| **IronClaw** | 39 updated | 24 updated / 11 merged | No new; v1.4.0 imminent | **7.5** | CI expedite track delivering; design-system completion; 3:1 open:closed ratio |
| **LobsterAI** | 1 open | 9 merged | 2 releases this week (2026.8.21, 2026.8.25) | **8.0** | Settled user base; feature-focused; low community friction |
| **TinyClaw** | 0 | 0 | — | **3.0** | Inactive |
| **Moltis** | 2 updated | 5 updated / 1 merged | No new | **6.5** | Active sandbox expansion (Coder/K8s); quick bug turnaround |
| **CoPaw** | 84 combined | 29 merged | **v2.1.1-beta.3** (Aug 25) | **7.0** | High volume; Windows stability issues; strong test coverage increases |
| **ZeptoClaw** | 0 | 0 | — | **3.0** | Inactive |
| **ZeroClaw** | 50 updated / 38 open | 50 updated / 1 merged | No new; v0.9.0 milestone | **7.5** | Security-first culture; RFC governance robust; S0 cron-scope bug open |

---

## 3. OpenClaw's Position

**Advantages vs Peers:**
- **Scale of community engagement**: 500 issues/PRs updated in 24h — 10x larger than any competitor (ZeroClaw and CoPaw are closest at ~50-84).
- **Maturity of triage**: `clawsweeper:` label taxonomy (source-repro, linked-pr-open, needs-maintainer-review) demonstrates a world-class issue-management operation.
- **Architecture**: The dynamic parity layer for Codex tools and multi-channel gateway (Telegram, WhatsApp, Buzz, WebSocket) is more extensive than any peer.

**Technical Approach Differences:**
- OpenClaw uses a **schema-versioned state database** (currently v10) with active table retirement — a more disciplined approach than NanoBot's session-store or CoPaw's SQLite-backed store.
- Its **agent-dreaming configuration** (per-agent, #67413) is unique — no other project has an equivalent memory-staggering mechanism.

**Community Size Comparison:**
- OpenClaw's issue volume (500/24h) dwarfs NanoBot (5), Hermes (50), and IronClaw (39). This suggests either a significantly larger user base or a more vocal one.
- However, this scale brings a cost: OpenClaw has the **highest severity-bug burden** (P0 SQLite corruption, 5+ P1 delivery issues) and a beta cycle that has been stuck at beta.3 for weeks. NanoBot's clean, quick fix pipeline (P1s within 24h) is a model OpenClaw could learn from.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging independently across multiple projects:

| Requirement | Projects (Specific Evidence) |
|-------------|-------------------------------|
| **MCP reliability & recovery** | CoPaw (#6524 — session not auto-recovering); Hermes (#94859 — stdio MCP fails post-restart); PicoClaw (#3269 — MCP hang bricks agent); NanoBot (#5535 — MCP readiness retry); ZeroClaw (#10346 — MCP-registry caching) |
| **Sandbox/isolation security hardening** | ZeroClaw (#9947 — cron agent scoping; #9872 — bounded delegate filesystem); NanoBot (#5536 — restricted shell bypass); OpenClaw (#126631 — root-owned /workspace bind-mount); IronClaw (#7732 — persistent sandbox epic) |
| **Message-delivery reliability** | OpenClaw (5+ P1s across Telegram/WhatsApp/Buzz); CoPaw (#7258 — WeChat thinking display); Hermes (#94435 — Slack duplicate/clobbered messages); NanoBot (#5516 — Telegram streaming/rich conflict) |
| **SQLite/state-persistence integrity** | OpenClaw (#126821 — corruption, #114612 — unbounded growth); Hermes (#79005 — profile swap corrupts state.db); ZeroClaw (memory storage RFC #9103) |
| **Programmatic/API access to state** | OpenClaw (#79902 — SQLite seams for companion apps); NanoBot (session management tool); ZeroClaw (#8396 — wire protocol first-class) |
| **Edge/distributed compute** | PicoClaw (#3345 — worker mode); NullClaw (#994 — household edge mesh); ZeroClaw (#10360 — opt-in edge mesh); NanoClaw (#3538 — isolated edge workers) |
| **Setup/provisioning automation** | NanoClaw (structured setup driver PR bundle #3485-3487); OpenClaw (#16670 — onboarding wizard gap); IronClaw (OOBE suggestion drawer #7816) |
| **Thinking/reasoning display controls** | CoPaw (#7196, #7258 — collapsible/hide thinking); ZeroClaw (#8999 — streamed turns misread as payloads) |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target Users | Technical Architecture | Unique Differentiator |
|---------|---------------|--------------|------------------------|----------------------|
| **OpenClaw** | Multi-channel gateway reliability | Power users, self-hosters | Rust, schema-versioned SQLite, dynamic Codex parity layer | Largest ecosystem; most channels; most complex state model |
| **ZeroClaw** | Security & governance | Enterprise, multi-agent deployments | Rust, RFC-driven governance, sandbox-first | Strict security boundaries; formal RFC process; S0-aware culture |
| **CoPaw** | UX polish & feature breadth | General consumers, Chinese market | Python/TypeScript hybrid, Tauri desktop | Fast release cadence; broad model catalog; community-driven UX |
| **NanoBot** | Developer experience & reliability | Developers, MCP-heavy workflows | TypeScript/Node, MCP-native | Clean P1 fix pipeline; fast turnaround; strong contributor onboarding |
| **Hermes Agent** | Desktop application & multi-gateway | Desktop-centric users, macOS/Windows | Desktop app + gateway architecture | Desktop UI focus; salvage-PR workflow; multi-gateway session routing |
| **IronClaw** | Infrastructure & CI maturity | Cloud/railway deployers | Rust, CI-expedite, design-system program | CI convergence; persistent sandbox epic; notification-center durability |
| **LobsterAI** | Artifact/library management | Content creators, Chinese market | Electron, library-centric | Monetization signals (plan catalog, analytics); settled user base |
| **NanoClaw** | Setup automation & skill robustness | Ops/automation users | Container-isolated agents | Structured setup driver; skill-layer diagnostics; OpenCode/Codex deduplication |
| **Moltis** | Remote sandbox expansion | Enterprise, regulated industries | Rust (implied), sandbox backends | Kubernetes/Coder backend push; VM-level isolation support |
| **PicoClaw** | Edge/low-resource compute | Sipeed board owners | Lightweight, RISC-V friendly | Edge-worker proposals; lowest footprint philosophy |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapidly Iterating (Merging 15+ PRs/24h):**
- **NanoClaw** (16 merged) — highest velocity-to-issue ratio; clean PR lifecycle (3-5 days open typical).
- **NanoBot** (14 merged) — best fix-to-report turnaround; all P1s resolved within reporting window.
- **OpenClaw** (244 merged/closed) — massive scale, but merge-through-close suggests heavy churn; beta stuck.
- **CoPaw** (29 merged) — sustained momentum with 2 releases/week; test coverage increasing.

**Tier 2 — Moderate/Consolidating (5-15 merged/24h):**
- **IronClaw** (11 merged) — CI infra wins; design-system completion; awaiting v1.4.0.
- **Hermes Agent** (14 merged) — Desktop stabilization effort; salvage-PR pattern effective but reactive.
- **ZeroClaw** (1 merged) — Low merge count but high RFC activity; governance-heavy phase.
- **LobsterAI** (9 merged) — Feature-focused; 2 releases this week; settled user base.

**Tier 3 — Stabilizing/Stagnating (0-5 merged/24h):**
- **Moltis** (1 merged) — Advanced sandbox work in progress; low issue volume suggests niche adoption.
- **PicoClaw** (0 merged) — Stale backlog; critical MCP bug unattended for 37 days — **at risk of contributor flight**.
- **NullClaw** (0 merged) — Architectural pause; edge-mesh proposal may re-energize or fail to launch.
- **TinyClaw / ZeptoClaw** — Inactive; effectively dormant.

---

## 7. Trend Signals

**For AI Agent Developers:**

1. **Reliability is the #1 differentiator.** Across every active project, message loss, state corruption, and delivery failures are the top complaints. NanoBot's fast-fix culture and IronClaw's CI-expedite track show that **engineering discipline wins user trust** faster than feature velocity.

2. **MCP is becoming the default tool-interop standard — but the middleware is immature.** Every project with MCP support has open reliability bugs (session recovery, restart handling, large-result context overflow). Developers building on MCP should invest in **connection lifecycle management** as a core competency.

3. **Security is shifting from feature to prerequisite.** ZeroClaw's S0 cron-scope bug, NanoBot's restricted-shell bypass, and OpenClaw's root-owned bind-mount all point to **sandbox isolation as the next frontier**. Expect security audit demand to rise as agents gain more autonomous capabilities.

4. **Edge/distributed compute is the emerging architectural wave.** Three independent proposals (PicoClaw, NullClaw, ZeroClaw) within 24 hours signal genuine demand for **household/enterprise mesh topologies** — pooling idle devices into trusted compute grids. Watch for a first-mover implementation in late 2026/early 2027.

5. **Setup and provisioning are the new UX battleground.** NanoClaw's structured setup driver (IaC-style), IronClaw's OOBE suggestion drawer, and OpenClaw's onboarding wizard gap all point to **"getting started" as a competitive differentiator**. Agent frameworks are increasingly being deployed in automated/DevOps contexts, not just interactive chat.

6. **Thinking/reasoning visibility controls are platform-specific.** CoPaw's split community (show vs. hide thinking traces) and ZeroClaw's streamed-turn misclassification both reveal that **reasoning display is a UX decision requiring per-channel and per-model granularity**.

7. **Provider catalog maintenance is a silent operational cost.** CoPaw (Aliyun/Kimi refresh), Hermes (xAI reserved-name rejection), and OpenClaw (model fingerprint drift) all show that **model-provider compatibility is a moving target requiring dedicated tooling**.

8. **Windows remainsthemost fragile deployment target.** CoPaw (installer locks, memory leaks), Hermes (update hangs, permission resets), and OpenClaw (WhatsApp/Telegram channel issues) all report disproportionate Windows-specific failures. **Cross-platform CI and packaging investment is a strategic gap** for most projects.

---

*Report compiled from GitHub activity data for 2026-08-26 across 13 projects in the AI agent / personal assistant open-source ecosystem.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date:** 2026-08-26

---

## 1. Today's Overview

NanoBot is experiencing a **high-velocity development cycle**, with 24 pull requests updated in the last 24 hours (14 merged/closed, 10 open) and 5 issues reported in the same period—all still open. The project shows a **strong issue-to-fix pipeline**: multiple bugs reported today already have dedicated PRs addressing them (e.g., #5532 / #5536, #5527 / #5528). The Telegram rich-message streaming issue (#5516) has a candidate fix (#5531), and the Codex prompt cache routing (#5540) and `find_files` performance (#5533) issues were closed with fixes. No new releases were cut today, indicating a **consolidation phase** between version bumps, with the team prioritizing bug fixes, performance improvements, and UI polish across TUI, WebUI, and Telegram channels.

---

## 2. Releases

**No new releases published in the last 24 hours.**

---

## 3. Project Progress

**14 PRs merged/closed today**, representing significant stability and UX improvements:

**Core Agent & Tools:**
- **#5525** — Demand-driven document retrieval: `grep` now returns bounded snippets with 5-line context; PDF/DOCX/XLSX/PPTX searched incrementally with stable locators, bypassing the 200K attachment-preview cap
- **#5533** — `find_files` scans kept responsive via worker-thread execution and budgeted `os.scandir` traversal
- **#5540** — Codex prompt cache routing stabilized by propagating a session identity through provider call context; fallback/image-retry paths included
- **#5529** — Background subagents now only waited for at turn exit, keeping routine drains non-blocking (single 300s deadline)

**TUI/WebUI:**
- **#5534** — TUI autocomplete for `$skill-name` references with filtered picker, arrow navigation, and caret-aware insertion
- **#5538** — Composer action hint clarified: "Enter send now · Tab send next" replaces vague "Steer this turn…"
- **#5530** — Short transcripts and composer kept top-aligned in tall terminal panes; sticky scrolling preserved on overflow

**Telegram Channel:**
- **#5541** — Group messages now prefixed with sender display name (name → username → numeric ID fallback); private chats unchanged

**Infrastructure:**
- **#5526** — Session management tool renamed to `exec_session` with `until_exit`/`timeout_ms` controls; legacy `write_stdin` migrated

**Still open (needing review/merge):**
- **#5531** (fixes #5516): Streaming preview upgraded to rich in place at stream end—direct fix for the Telegram rich-message/streaming incompatibility
- **#5535**: Gateway retries MCP readiness before turns; ensures recovered tools registered before per-session snapshots
- **#5536** (p1): ExecTool fails closed when restricted shell lacks a sandbox—addresses symlink/expansion escape vectors (fixes #4072)
- **#5537**: Persistent session-scoped `focus` value in the `my` tool
- **#5528** (fixes #5527): Projects generated titles onto per-chat sessions under `unifiedSession`

---

## 4. Community Hot Topics

**Most active discussions (by comments/reactions):**

1. **[#5505 — AnySearch as web search provider](https://github.com/HKUDS/nanobot/issues/5505)** (3 comments)
   - Team behind AnySearch seeks to integrate their unified real-time search tool via API/MCP/Skill methods. Represents **interest in expanding provider ecosystem** with key-optional, anonymous-quota options.
   
2. **[#5532 — Missing `mask_session_key` import in autocompact.py](https://github.com/HKUDS/nanobot/issues/5532)** (1 comment)
   - Crash during a complex Chinese-language user query involving resource cleanup and memory clearing. Points to **edge-case handling in multi-step agent loops**.

3. **[#5516 — Telegram rich messages never render with streaming](https://github.com/HKUDS/nanobot/issues/5516)** (1 comment)
   - Detailed analysis of mutually-exclusive `rich_messages` and `streaming` modes; suggests Bot API 10.1–10.3 drafts as solution. **Fix PR #5531 exists and is open.**

4. **[#5527 — WebUI titles stay "Untitled" with unifiedSession](https://github.com/HKUDS/nanobot/issues/5527)** (0 comments)
   - Root cause identified: title generation on shared `unified:default` session never reaches per-chat `websocket:<id>` sessions. **Fix PR #5528 is open.**

**Underlying need pattern:** Users are pushing for **richer integration options** (search providers, MCP reliability) and **visible progress feedback** (titles, notifications, retry status) rather than raw model capabilities—a sign of **agent framework maturity**.

---

## 5. Bugs & Stability

**Ranked by severity:**

| Severity | Issue | Status | Fix PR |
|----------|-------|--------|--------|
| **P1 (High)** | [#5536 — Restricted shell lacks sandbox](https://github.com/HKUDS/nanobot/pull/5536): `restrict_to_workspace` can be bypassed via symlinks/command substitution | Fix PR open | #5536 |
| **P2 (Medium)** | [#5532 — Missing `mask_session_key` import crashes autocompact](https://github.com/HKUDS/nanobot/issues/5532) on complex user queries | Open, no fix PR yet | — |
| **P2 (Medium)** | [#5516 — Telegram rich messages broken with streaming](https://github.com/HKUDS/nanobot/issues/5516) | Fix PR open | #5531 |
| **P2 (Medium)** | [#5527 — WebUI titles stuck at "Untitled" under unifiedSession](https://github.com/HKUDS/nanobot/issues/5527) | Fix PR open | #5528 |

**Already fixed today:**
- **#5540** — Codex prompt cache routing (session identity based)
- **#5533** — `find_files` responsiveness (worker + budgeted traversal)
- **#5541** — Telegram group sender attribution
- **#5529** — Background subagent blocking behavior

**Assessment:** No crashes or regressions remain unfixed at P1 level. The #5532 import error is the only P2 without a linked fix; expected to be resolved quickly given its straightforward nature.

---

## 6. Feature Requests & Roadmap Signals

**Requested this week:**
- **#5524 — WebUI notification sound** when agent turn completes (default off, Settings toggle)
- **#5505 — AnySearch provider** with anonymous quota option (PR planned by submitter)

**Recently merged features pointing to roadmap direction:**

- **Skill & session management maturity** (#5534 autocomplete, #5537 focus persistence) → NanoBot is **doubling down on multi-session workflows** and skill discoverability
- **Demand-driven document retrieval** (#5525) → Moving beyond "load everything" to **lazy, targeted access** to complex document formats
- **Streaming with rich rendering** (#5531) → **Cross-channel UX parity** is a clear priority (Telegram streaming + rich messages)

**Prediction for next minor release:**
1. Telegram rich-message fix (#5531) — user-facing, directly addresses #5516
2. MCP readiness retry (#5535) — improves reliability for MCP-heavy deployments
3. Security hardening (#5536) — fail-closed sandbox; includes regression tests
4. WebUI title fix under `unifiedSession` (#5528) — small UX win, likely to slip in

---

## 7. User Feedback Summary

**Pain points expressed:**

1. **Telegram integration demands** (Issue #5516): A user with detailed Bot API knowledge submitted a thorough technical analysis of why rich messages fail with streaming—demonstrating **high technical competence in the user base** and expectation that platform-specific features should work together seamlessly.

2. **Multi-session confusion** (Issue #5527): The `unifiedSession` feature creates a **disconnect between backend state and UI presentation**—titles the system generates never appear where users look. This is a **UX consistency issue** affecting perceived polish.

3. **Workflow feedback gap** (Issue #5524): Users waiting for long agent turns (tool calls, shell commands) want **audible completion signals**; otherwise they must stare at the screen. Common in "agent as worker" usage patterns.

4. **Provider diversification** (Issue #5505): Third-party teams are **proactively seeking integration** with NanoBot—a **strong sign of ecosystem health**. The anonymous-quota option indicates interest in **lower-friction onboarding** for search providers.

**Satisfaction signals:**
- Quick turnaround on multiple P2 fixes (e.g., #5533, #5540 closed within a day of being reported)
- Active regression-test coverage added in most merged PRs

---

## 8. Backlog Watch

**PRs needing maintainer attention:**

1. **[#5234 — MST metasearch provider (P1, conflict)](https://github.com/HKUDS/nanobot/pull/5234)** — Open since Aug 3, marked with merge conflicts. Integrates Meta-Search Tool (DuckDuckGo, Google, Brave, Bing via RRF fusion). **Over 3 weeks without resolution**; the conflict label suggests codebase drift. Deserves either conflict resolution help or explicit design feedback.

2. **[#5389 — Drag-and-drop session organization (P2, conflict)](https://github.com/HKUDS/nanobot/pull/5389)** — Open since Aug 14. Full feature implementation (reordering, grouping, group creation via drag). Also marked with conflicts; the pane-based layout refactor likely caused the drift.

3. **[#5152 — Subagent partial completion results](https://github.com/HKUDS/nanobot/pull/5152)** — Open since Jul 28 (nearly a month). Fixes an ambiguity where the model may infer unfinished results as final. Marked as regression and conflict. **Longest-standing open PR**, affecting core agent behavior—should be prioritized.

**Pattern:** All three backlog items involve **merge conflicts from recent UI/layout refactors** (#5519 compact header, pane-based sessions). The maintainers should consider a **dedicated conflict-resolution pass** to unblock this queue, especially for #5152 which touches agent correctness.

---

*Data compiled from: HKUDS/nanobot GitHub repository — 2026-08-26*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Based on the GitHub data for Hermes Agent (github.com/nousresearch/hermes-agent) on 2026-08-26, here is the project digest:

---

## Hermes Agent Project Digest | 2026-08-26

### 1. Today's Overview
The Hermes Agent project is in a dynamic phase with 50 issues and 50 pull requests updated in the last 24 hours, indicating very high community engagement and active development. The open issue count (40) is high relative to closed items (10), suggesting the maintainers are managing a substantial backlog of reported bugs and feature requests. The PR pipeline is active, with 36 PRs still open and a significant number of new contributors submitting fixes and features, though no new releases were published today. A dominant theme in recent activity is the stability of the Desktop application and its multi-gateway architecture, alongside a series of "salvage" PRs that resurrect and adapt previously stalled fixes to the current codebase. Overall, the project shows high velocity, with a strong emphasis on community contributions, but faces challenges in addressing a large volume of nuanced bugs.

### 2. Releases
No new releases were published in the reporting period (2026-08-26). The most recent release, based on issue data, appears to be Hermes v0.20.5 (from 2026-08-19).

### 3. Project Progress
Today saw 14 PRs closed or merged, with a notable effort focused on stabilizing the Desktop application. Key advances include:

- **Desktop UI/UX Hardening:** Several PRs merged to improve the Desktop experience, including `fix(desktop): keep Routines controls visible in narrow panes (#95136)` to fix layout issues in the cron jobs panel, and `feat(desktop): add Chat Width setting in Appearance (#95134)` to offer users more control over the chat layout.
- **Bug Fixes (Salvage PRs):** A series of "salvage" PRs by contributor `teknium1` (which cherry-pick and adapt fixes from other authors) were merged, addressing key stability issues:
    - `fix(desktop): Bots roster no longer stalls behind a live profile's write lock (#95126)`
    - `macOS terminal permissions no longer reset on every Python patch update (#95131)`
    - `fix(bootstrap): stale checkouts can no longer deadlock the in-app updater (#95069)`
    - `Windows auto-update refreshes cua-driver again — unattended-safe, hangs fail in seconds (#95129)`
- **Gateway Stability:** A major focus was on fixing multi-gateway issues in the Desktop app. PRs like `fix(desktop): secondary gateways publish only live sockets and survive prune/mode-switch (#95082)` and `fix(desktop): gateway switches, primary reuse, and session routing hold exact route identity (#95080)` were merged, addressing critical connection and session routing bugs.
- **Core Fixes:** One PR addressing a core logic bug was also closed, covering a fix for `fix(relay): drain active turns before popping session scope on shutdown (#95130)`. Another merged PR addressed a security boundary, `fix(tools): route config credential-file mounts through the master-store deny-list (#84286)`.
- **Feature Growth:** The largest new feature pushed towards completion is `feat(webapp): serve Desktop renderer in browsers (#93508)`, which aims to allow the Desktop app to be used in a web browser. Another notable feature added today is `feat(gateway): expose active provider in runtime footer (#95135)`.

### 4. Community Hot Topics
The most significant community discussions and interest have centered on a few core problems:

1.  **Skills Index Watchdog Failure:** The most active issue by far, `#66616`, is an automated watchdog flagging that the "[skills-index-watchdog] Skills index is stale or degraded". With 97 comments, this seems to be a persistent and ongoing problem that the community is actively discussing and troubleshooting.
2.  **macOS Permission Resets:** The issue "[Bug]: macOS Full Disk Access (Files & Folders) revoked after every Hermes Desktop update" (`#52010`) continues to attract attention. With 21 comments, this is a major user pain point, even though a fix for a related issue (terminal permissions) was salvaged and merged today. The dissatisfaction stems from having to repeatedly re-grant permissions after each update.
3.  **xAI Provider Incompatibility:** A newly filed bug, "xAI rejects requests: function name tool_search is reserved for the native server-side tool" (`#95003`), has quickly gained attention with 7 👍 reactions and 9 comments. This is a high-impact issue that makes the Grok provider unusable and has an active community following it.
4.  **Architecture Proposal for Systemic Defects:** A fascinating discussion is unfolding in issue `#95028`, titled "[Architecture] Hermes Authority Execution Layer — the twelve issues are one defect, and the architecture that fixes it". This extensive proposal suggests many open bugs are actually one systemic issue, and the 9 comments indicate deep technical engagement from the community.

### 5. Bugs & Stability
The array of new and ongoing bugs reported today highlights several areas of fragility:

- **Critical (P1):** The most severe report is `#94906`, "[Bug]: Windows: native stdio MCP client discovers tools but every call fails with 'subprocess has exited'". This P1 bug completely breaks MCP functionality on Windows.
- **High (P2):** Multiple P2 bugs were reported, causing major disruptions:
    - **xAI Incompatibility:** `#95003` makes an entire provider unusable.
    - **Multi-Gateway Session Leaks:** `#93937` reports a "session not found" error when switching gateways in the Desktop app.
    - **Environmental Variable Pollution:** `#95078` reports a bug where a nested Hermes process inherits a stale `TERMINAL_CWD` instead of its explicit working directory.
    - **Intermittent MCP Failures:** `#94859` notes that multiple stdio MCP servers intermittently fail after a gateway restart.
    - **Provider Fallback Failure:** `#95054` reports that fallback entries configured for `provider: ollama` silently resolve to `(None, None)`, breaking redundancy.
    - **Slack Streaming Duplicates:** `#94435` and a closed duplicate `#93617` report issues with Slack native streaming causing duplicate or clobbered messages during concurrent turns.
- **Medium (P3):** Includes the `skills-index-watchdog` failing (`#66616`), Desktop profile swap corrupting `state.db` (`#79005`), and UI bugs like the TUI lowercasing Shift-letter input (`#90663`).
- **Closed with Fixes:** Many P2 bugs were closed after fixes were applied or salvaged, including the Desktop CRONJOBS pane being stuck (`#94516`, `#94483`), Windows update hanging on cua-driver (`#87703`), and the macOS launchd job being deregistered after update (`#74973`).

### 6. Feature Requests & Roadmap Signals
User-submitted features indicate a strong desire for more power and configurability in the tool:

- **Verified Local Cold Archive:** `#91005` (with corresponding PR `#94428`) proposes a feature to create a "verified local cold archive" for soft-archived sessions. This signals a need for a true and secure local backup solution.
- **Remote Backend Probe Toggle:** PR `#72423` adds an opt-out switch for the live remote-backend environment probe, hinting at user concerns over prompt-building process overhead or privacy.
- **Shared Visible Browser Control:** The proposal for a "Chrome Extension backend for shared visible browser control" (`#84000`) is a request for a more interactive browser tool that can share state with other applications.
- **Adaptive Explanation Policy:** Issue `#93382` is a feature request to adapt how Hermes explains its output, indicating a desire for more customizable interaction patterns.
- **Web Accessibility:** The large PR `#93508` to bring the full Desktop renderer to the web (`hermes webapp`) continues to progress, earmarking a major upcoming capability.

### 7. User Feedback Summary
The general sentiment is a mix of frustration with recurring stability issues and high enthusiasm for the project's potential.

- **High Dissatisfaction:** There is clear frustration over update-related regressions, particularly on macOS, where permissions are revoked (`#52010`) and system services are left in a broken state (`#74973`). The Windows update hanging issue (`#87703`) also points to serious reliability problems with the update process.
- **Deep Technical Engagement:** Users are not just reporting bugs; they are deeply engaged in diagnosing root causes and proposing architectural solutions, as seen in `#95028` and `#95003`. This suggests a sophisticated and committed user base.
- **Desire for Control:** There is a clear desire for more customization and control over the interface and behavior, demonstrated by requests like the "Chat Width" setting (merged as `#95134`) and the "Remote Backend Probe Toggle" (PR `#72423`).

### 8. Backlog Watch
Several important issues and PRs remain open and likely require maintainer attention:

- **Critical MCP Bug:** The P1 Windows MCP issue `#94906` is tagged as a `duplicate`, but its original is unclear. Maintainers should ensure the root cause is tracked and a fix is scheduled.
- **High-Impact Provider Bug:** The xAI incompatibility (`#95003`) has significant community support (7 👍) and renders a provider unusable. This would seem to warrant immediate attention.
- **Long-Standing Inactive Issue:** The `skills-index-watchdog` (`#66616`) has been open for over a month with 97 comments. As an automated system, its continued failure suggests a technical debt that needs resolution.
- **Persistent Permission Issue:** Despite several fixes, the broader issue of macOS permissions resetting after updates (tracker `#52010`) remains a point of friction. The community will likely watch to see if the salvage fix for terminal permissions (`#95131`) resolves the full class of problems.
- **Open Architecture Decision:** The i18n PR for pt-BR support (`#92590`) is a large community-driven contribution. With its "needs-decision" label, it may require maintainers to establish a clear policy on supporting community-submitted translations.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-26

## 1. Today's Overview

PicoClaw's activity is **moderate with a clear maintenance focus**. Four issues and one pull request were updated in the last 24 hours, though **none were newly created today** — the most recent issue (#3345) was opened yesterday. The project is currently processing a backlog of bug reports, with **zero merged/closed PRs today**, meaning no fixes landed this cycle. Notably, two of the four updated issues are marked as `[stale]`, suggesting the maintainers may be doing backlog triage. The single open PR (#3340) directly addresses one of the most impactful reported bugs (Slack media uploads), signaling that contributor-driven fixes are in flight but not yet merged. No new releases were published, consistent with a stabilization period.

## 2. Releases

**No new releases** were published in the last 24 hours. The project appears to be between releases, with the latest known version referenced in issue reports being **PicoClaw 0.3.1** and nightly builds. Users are actively testing nightlies, as evidenced by issue #3269 referencing a specific nightly commit.

## 3. Project Progress

**No PRs were merged or closed** in the last 24 hours. The only updated PR is:

- **[#3340 — fix(slack): set FileSize on media upload params](https://github.com/sipeed/picoclaw/pull/3340)** (Open, stale): A contributor-submitted fix for the Slack media upload bug (#3338). The PR corrects `SendMedia` to populate `FileSize` in `slack.UploadFileParameters`, addressing the `file.upload.v2: file size cannot be 0` rejection. This fix is authored by the same reporter of issue #3338 (octavioturra), showing active contributor engagement, though it has not yet received maintainer review or merge.

## 4. Community Hot Topics

The most actively discussed items (by comment count) reveal a mix of UX pain points and system reliability concerns:

1. **[#3281 — Web UI chat input very laggy with long history](https://github.com/sipeed/picoclaw/issues/3281)** — 7 comments, 1 👍
   - **Underlying need**: Users expect responsive chat input even with extensive conversation history. The lag likely stems from inefficient DOM handling or re-rendering of long message lists. This affects daily UX for heavy users.

2. **[#3269 — MCP server connection failure hangs the agent loop](https://github.com/sipeed/picoclaw/issues/3269)** — 7 comments, 1 👍
   - **Underlying need**: Robust error handling in agent orchestration. A single failed MCP connection should not deadlock the entire chat interface. This is a **critical reliability concern** for users integrating MCP tools.

3. **[#3338 — Slack does not attach image media content](https://github.com/sipeed/picoclaw/issues/3338)** — 2 comments
   - **Underlying need**: Functional Slack integration is table stakes for productivity-focused users. The single PR (#3340) addresses this, but the issue remains open pending review.

4. **[#3345 — Proposal: lightweight PicoClaw worker mode](https://github.com/sipeed/picoclaw/issues/3345)** — 0 comments (new, not yet discussed)
   - **Underlying need**: Distributed/edge-deployable agent workers on low-resource hardware. This signals growing interest in PicoClaw as a lightweight orchestrator rather than a PC-centric assistant.

## 5. Bugs & Stability

Three open bugs were active in the last 24 hours, ranked by severity:

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **Critical** | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | MCP server connection failure hangs agent loop → chat stops replying entirely | No fix PR |
| **High** | [#3281](https://github.com/sipeed/picoclaw/issues/3281) | Web UI input lag with long history — degraded but functional | No fix PR |
| **Medium** | [#3338](https://github.com/sipeed/picoclaw/issues/3338) | Slack media uploads fail with "file size cannot be 0" | Fix PR [#3340](https://github.com/sipeed/picoclaw/pull/3340) open |

**Assessment**: The MCP hang (#3269) is the most dangerous — it renders the assistant completely unresponsive. The Slack issue has a pending contributor fix, but two of three active bugs lack any fix in progress.

## 6. Feature Requests & Roadmap Signals

One notable feature proposal is active:

- **[#3345 — Lightweight PicoClaw worker mode for household edge compute](https://github.com/sipeed/picoclaw/issues/3345)** (kvnloo): Proposes adapting PicoClaw to run as lightweight worker nodes on low-cost boards (RISC-V/ARM/MIPS, Raspberry Pis, old phones) with only 10–20 MB memory available. Architecturally, this suggests a **distributed agent topology** where one powerful PC acts as coordinator and resource-constrained devices serve as workers.

**Prediction**: This aligns with PicoClaw's target platform (Sipeed boards are RISC-V-centric), making it a plausible **roadmap candidate for the next major version** — though it would require significant architectural work (smaller memory footprint, network-aware task distribution). It will likely generate discussion once maintainers respond.

## 7. User Feedback Summary

Real user pain points from active issues:

- **Performance degradation over time**: Users report the Web UI becomes unresponsive in long sessions (#3281), indicating performance testing gaps for sustained usage.
- **Single point of failure**: The MCP hang (#3269) means one failing tool connection can brick the entire conversation — users need **graceful degradation and timeout handling**.
- **Integration correctness**: Slack media failing with a confusing "size cannot be 0" error (#3338) suggests insufficient edge-case testing in integration adapters.
- **Resource-conscious users**: The new edge-compute proposal (#3345) reflects a user base interested in **maximizing value from cheap, low-power hardware** — a departure from cloud-centric AI assistants.

**Satisfaction signals**: The presence of contributor-submitted PRs (octavioturra in #3340) shows community confidence in the project's architecture and willingness to invest time in fixes.

## 8. Backlog Watch

Items needing maintainer attention:

- **[#3340 (PR)](https://github.com/sipeed/picoclaw/pull/3340)** — Marked `[stale]` but is a **direct fix for an identified bug**. Maintainers should review and merge promptly to clear the Slack issue.
- **[#3269](https://github.com/sipeed/picoclaw/issues/3269)** — Open for 37 days with 7 comments and no maintainer response. This is the **most severe bug** and should be prioritized for triage and assignment.
- **[#3281](https://github.com/sipeed/picoclaw/issues/3281)** — Open for 36 days, stale-tagged. A UX-critical issue with no fix in flight; may need a maintainer to reproduce and scope.

---

**Overall**: PicoClaw is in a **stable-but-stagnant phase** — no releases, no merges, but active community reporting. The main risk is the unattended MCP hang bug (#3269) and stale backlog items. Positive signals: contributor momentum on fixes and new feature ideation for edge deployments.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-26

## Today's Overview

NanoClaw saw a high-velocity development day with **50 PRs updated** in the last 24 hours (34 open, 16 merged/closed) and **5 new issues** filed, all still open. The [core-team] label dominates the PR activity, indicating active maintainer engagement across Slack integration, setup hardening, and agent-runner reliability. The issue tracker reveals a cluster of **skill-layer robustness concerns** — shell quoting vulnerabilities, symlink sync failures, and update-time adapter conflicts — all reported by the same contributor (glifocat), suggesting systematic testing of the skills framework. Notably, **zero new releases** shipped today, despite substantial merged work, meaning the project is likely accumulating changes for a larger release. The overall health signal is strong: maintainers are merging actively, no critical regressions have surfaced, and the roadmap shows clear investment in structured automation protocols.

## Releases

**No new releases** were published in the last 24 hours. The most recent release remains unspecified in the available data; substantial merged work (composer refactoring, Slack handoffs, setup protocol framing) has not yet been tagged, suggesting an imminent release candidate is being assembled.

## Project Progress

Sixteen PRs were merged or closed today, covering substantial architectural and reliability improvements:

- **Unified document composition** — PR [#3536](https://github.com/nanocoai/nanoclaw/pull/3536) (merged) inlines every instruction source into a single project document, fixing a Claude Code security-gate issue where `@` imports resolving outside the working directory required (and often got denied) approval. Agents now reliably receive capability instructions.
- **Codex composer deduplication** — Two related PRs ([#3537](https://github.com/nanocoai/nanoclaw/pull/3537), [#3539](https://github.com/nanocoai/nanoclaw/pull/3539)) merged, removing Codex's duplicated composer in favor of trunk's shared implementation. This fixes drift where `cli_scope: disabled` groups were handed incorrect manuals and bringsCodex's project-document generation in line with OpenCode's.
- **OpenCode workspace fix** — PR [#3540](https://github.com/nanocoai/nanoclaw/pull/3540) merged, ensuring OpenCode agents run in the actual agent workspace rather than the sibling `/workspace/group` directory, so project-document walks can resolve correctly.
- **Explicit Slack room handoffs** — PR [#3544](https://github.com/nanocoai/nanoclaw/pull/3544) merged (with follow-up [#3545](https://github.com/nanocoai/nanoclaw/pull/3545) still open), adding an explicit handoff tool for one or multiple agents, resolving real bot mentions host-side with validation for self/unknown/duplicate/outsider/raw inputs, and stopping room-creation from auto-mentioning everyone.
- **Mnemon setup correction** — PR [#2656](https://github.com/nanocoai/nanoclaw/pull/2656) merged after a long lifecycle, moving `mnemon setup` from `entrypoint.sh` (which the host overrides) to `main()` in `container/index.ts`, finally making mnemonic hooks register correctly.
- **Scheduled-task error routing** — PR [#3311](https://github.com/nanocoai/nanoclaw/pull/3311) (open) fixes a bug where scheduled-task errors were written with copied routing fields that don't exist on task batches, causing misdelivery. The fix routes errors to the operator directly.

Several setup-ecosystem PRs remain open but are actively iterating (see Feature Requests below).

## Community Hot Topics

The most active discussions cluster around **setup automation** and **skill-layer robustness**:

- **Structured setup driver protocol** ([#3485](https://github.com/nanocoai/nanoclaw/pull/3485)) — This PR, plus its companions [#3484](https://github.com/nanocoai/nanoclaw/pull/3484) (keep auth secrets out of argv), [#3486](https://github.com/nanocoai/nanoclaw/pull/3486) (expose preseed catalog), [#3487](https://github.com/nanocoai/nanoclaw/pull/3487) (timezone preseed), represent a major push to make NanoClaw setup scriptable. The underlying need: operators want to provision NanoClaw programmatically (IaC-style) without scrapping ANSI-rendered terminal output. This is a strong roadmap signal.
- **Agent-scope prompt blindness** ([#3525](https://github.com/nanocoai/nanoclaw/pull/3525)) — A wizard step using `nc:run effect:step` could print but not ask, so "which agents may use Dial" couldn't echo user input. The fix is minimal and the author explicitly dropped unrelated changes per maintainer request, showing good contributor-maintainer collaboration.
- **Isolated container edge workers** ([#3538](https://github.com/nanocoai/nanoclaw/issues/3538)) — A feature proposal suggesting NanoClaw's isolated containers could be deployed across users' existing idle PCs/NAS/home servers instead of requiring new GPU/cloud purchases. No comments yet, but it taps into edge-computing and cost-saving motivations.
- **Durable host integration** ([#3528](https://github.com/nanocoai/nanoclaw/pull/3528)) — A substantial PR adding lease-id claimants, restart-overlap protection, and an incarnation gate, built on a zero-conflict convergence of three sibling lines proven at 425/425 tests. This addresses multi-host concurrency and crash-consistency.

## Bugs & Stability

Five new issues were filed today, all reporting concrete reliability problems in the skills layer. The cluster is significant — all from one reporter (glifocat) — but each is independently actionable:

1. **High — Unquoted shell interpolation with metacharacter validation bypass** ([#3543](https://github.com/nanocoai/nanoclaw/issues/3543)): The `add-dial` skill substitutes `{{owner_email}}` unquoted into bash, so apostrophe-containing emails break sign-in and shell metacharacters pass validation. This is both a functional break (edge-case emails fail) and a **potential injection vector**. The fix belongs in SKILL.md line 196/203 and 117/124 of the two affected skills. *No fix PR exists yet.*
2. **High — Per-session skill copies block spawn-time symlink sync** ([#3535](https://github.com/nanocoai/nanoclaw/issues/3535)): `add-vercel` instructs operators to rsync real skill copies into every session directory, which then prevents the spawn-time symlink synchronization from working and pins groups to stale skill versions. Diligence in following setup instructions creates a maintenance trap. *No fix PR yet.*
3. **Medium — Update-time skill refresh overwrites/breaks local adapters** ([#3529](https://github.com/nanocoai/nanoclaw/issues/3529)): `update-nanoclaw`'s refresh assumes every channel import in `src/channels/index.ts` came from a skill, so custom/local adapters either block the update (validation failure) or get overwritten. The reporter's own adapter broke the update process. *No fix PR yet.*
4. **Medium — Per-agent tool scoping misses future agents** ([#3532](https://github.com/nanocoai/nanoclaw/issues/3532)): The `add-dial-tool` scoping (via OneCLI rules) only covered groups that existed at configuration time; agents created later inherit the tool by default, violating the "only chosen agents" intent. *No fix PR yet.*
5. **Stability fix candidates already merged/PR'd today** — The OpenCode workspace fix (#3540, merged) and the scheduled-task error routing (#3311, open) both address crash/misroute conditions.

## Feature Requests & Roadmap Signals

- **Structured setup driver (nanoclaw.driver.v1)** — The four-PR bundle ([#3485](https://github.com/nanocoai/nanoclaw/pull/3485), plus #3484, #3486, #3487) strongly signals that **programmatic/automated provisioning** is next on the roadmap. Expect a future release where setup is a first-class API, not a TUI-only flow.
- **Local web chat channel** ([#3298](https://github.com/nanocoai/nanoclaw/pull/3298)) — An open feature PR for a local web chat so fresh installs can be tested/demoed without external accounts (bot tokens, QR scans). High value for onboarding friction; likely to land in an upcoming release.
- **Isolated edge workers** ([#3538](https://github.com/nanocoai/nanoclaw/issues/3538)) — Early-stage proposal, no comments yet, but aligns with the project's container-isolation philosophy. Watch for community interest before predicting inclusion.
- **Host health introspection** ([#3482](https://github.com/nanocoai/nanoclaw/pull/3482)) — A single read-only call to answer "is this install up and what's in it" addresses observability gaps. Likely companions to the setup-driver work.

## User Feedback Summary

- **Skill documentation creates footguns**: The string of glifocat-reported issues (#3543, #3535, #3529) shares a theme — skills that instruct manual operations (rsync into sessions, unquoted interpolation) produce subtle breakage that is hard to diagnose. This points to a need for **skills that operate on the actual store/symlink layer** rather than duplicating files.
- **Scoping semantics trip users**: Two issues (#3532, plus the #3525 PR) show users expect scoping rules to be **live and future-proof**, not snapshots at configuration time.
- **Update path fragility**: The update-nanoclaw refresh issue (#3529) will erode trust if custom adapters are common. The reporter's "no opt-out" framing suggests users want a **choose-what-to-keep** flow.
- **Setup is a barrier**: Three of the top recent PRs (#3485, #3486, #3487) are authored by amit-shafnir, a core-team member, indicating maintainer-side acknowledgment that the wizard-only setup is a friction point for automation-oriented users.
- **Positive collaboration signal**: The #3525 author explicitly dropped unrequested changes per maintainer direction, demonstrating a healthy, guideline-driven contribution culture.

## Backlog Watch

- **PR #2431 — Conditional thread policy for Slack adapter** (open since 2026-05-12, 106 days): Adds `shouldUseThreadsFor(platformId)` so DM channels can be non-threaded while channels remain threaded. Last updated today, but the PR has been open for over three months — a maintainer decision or explicit deferral note would help contributors.
- **PR #2656 — mnemon setup fix** (open 84 days, merged today): Resolved after a long wait; not a current concern.
- **PR #3298 — Local web chat** (open since 2026-08-17, 9 days): Core-team labeled, substantial feature; no comments data available — needs a review pulse.
- **Issue #3543 — Shell-quoting injection risk**: Highest-severity new report with no fix PR yet; worth prioritization given the security-adjacent framing.

---

*Data window: 2026-08-25 to 2026-08-26. Metrics: 50 PRs updated (16 merged/closed), 5 new issues, 0 releases.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-08-26**:

---

### 1. Today's Overview
NullClaw is currently in a **low-activity maintenance phase**. Over the past 24 hours, the project saw only **1 issue update** (with no new pull requests or releases), indicating that core development has stalled or is in review. The single active discussion, Issue #994, is a high-level architectural proposal regarding edge mesh networking, suggesting that the community is focused on future scalability rather than immediate bug fixes. While the lack of PR velocity might seem quiet, the depth of the open proposal points to a project with strong existing primitives being considered for ambitious expansions.

### 2. Releases
**None.** There were no new releases published in the last 24 hours. Users should remain on the current stable version.

### 3. Project Progress
**None.** There were no merged or closed pull requests today. No code changes or bug fixes were introduced to the main branch in this reporting period.

### 4. Community Hot Topics
- **[#994 [OPEN] Household edge mesh using RuntimeAdapter workers and signed receipts](https://github.com/nullclaw/nullclaw/issues/994)** (Author: kvnloo)
  - **Activity:** Currently the only active issue, with 0 comments but high strategic importance.
  - **Analysis:** The author proposes utilizing NullClaw's existing "unusually good primitives"—specifically the `RuntimeAdapter` and `Peripheral` vtables, Docker/WASM containers, and hardware discovery—to create a "household edge mesh." This would allow operators to pool idle PCs and laptops into a local computing grid with signed receipts for trust. This signals a desire to pivot NullClaw from a single-device assistant to a **distributed personal cloud infrastructure**.

### 5. Bugs & Stability
**No bugs, crashes, or regression reports** were filed in the last 24 hours. The project appears to be currently stable on the `main` branch, with no new stability threats introduced.

### 6. Feature Requests & Roadmap Signals
The primary roadmap signal today comes from Issue #994. The request suggests a future version of NullClaw might include:
- **Distributed Compute:** A native mesh networking layer for running tasks across multiple household devices.
- **Trust & Verification:** Integration of signed receipts or cryptographic proof-of-work for executed tasks.
- **Resource Aggregation:** Automatic discovery and pooling of idle hardware via the existing `RuntimeAdapter` architecture.

**Prediction:** While this is a complex feature, NullClaw's strict size goals and modular runtime make this a plausible "v0.6" or "v0.7" milestone, likely developed as an opt-in adapter rather than a core rewriting of the runtime.

### 7. User Feedback Summary
- **Positive Sentiment:** The proposal text itself (written by a user) implicitly praises the project's architecture, calling the existing primitives "unusually good"—a strong signal of developer satisfaction with the codebase's design cleanliness and flexibility.
- **Use Case:** The underlying demand is for **autonomy and self-hosting**. Users want to break free from centralized cloud dependencies by creating their own trusted local networks.
- **Pain Point:** The request implies a current limitation: **lack of multi-node coordination**. Users currently must deploy NullClaw per-device, but want a single cohesive "household" control plane across heterogeneous hardware (PCs, laptops, ARM devices).

### 8. Backlog Watch
There are **no long-unanswered "stale" issues** currently requiring maintainer intervention; the only open item was created yesterday. However, maintainers should prioritize responding to **Issue #994** to acknowledge the proposal and set expectations. Given the lack of recent merged PRs, the community may be waiting for maintainer feedback on this architectural direction to gauge whether they should invest time in prototyping the mesh layer.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest
**2026-08-26**

---

## 1. Today's Overview

IronClaw is in a period of **intense convergence activity** — the project saw 39 issues and 24 PRs updated in the last 24 hours, with a strong **3:1 open-to-merged ratio** on issues suggesting active triage and reproduction work. The design-system program (Phases 1–5) is advancing through its final waves, while a broad **notification-center hardening** push (7 related issues) and a **CI expedite track** (T2–T4) are both accelerating. The most critical signal today is a cluster of **performance and correctness bugs discovered via real-world triage** (Telegram device-link failure, stuck log retrieval, 123-second runaway agent loops, and a 14.3-second inference-waste issue) that point to a mature codebase surfacing systemic issues under production load. No new releases were published in this window, indicating the project is consolidating before a v1.4.0 milestone.

---

## 2. Releases

**No new releases published in the last 24 hours.** The most recent release activity remains tied to the upcoming **v1.4.0 milestone**, which encompasses the persistent sandbox epic ([#7732](https://github.com/nearai/ironclaw/issues/7732)) and design-system Phases 2–3 ([#7781](https://github.com/nearai/ironclaw/issues/7781)).

---

## 3. Project Progress

**11 PRs merged/closed** in the last 24 hours, with several notable advances:

| PR | Description | Significance |
|---|---|---|
| [#7817](https://github.com/nearai/ironclaw/pull/7817) | **nextest pipeline (T2)** — Closes #7799. Cuts `Tests (Reborn)` wall clock and provides full-failure signal | CI expedite track delivering measurable infra gains |
| [#7818](https://github.com/nearai/ironclaw/pull/7818) | **Background subagents slices 2b+2c** — receipt spawns, per-child delivery, activation, healing sweeps | Major feature landing (producer half of R2) |
| [#7846](https://github.com/nearai/ironclaw/pull/7846) | **Retire legacy approval fallback** — durable inbox becomes exclusive source for notification rows | End-to-end notification-center migration complete |
| [#7809](https://github.com/nearai/ironclaw/pull/7809) | **Canonical preflight (T4)** — one gate list, worktree-safe hooks, self-printing REPRO | CI gate convergence |
| [#7819](https://github.com/nearai/ironclaw/pull/7819) | **PR/queue check convergence (T3)** — planner drift guard, default-features clippy | Closes #7800; eliminates "queue-only failure" classes |
| [#7861](https://github.com/nearai/ironclaw/pull/7861) | **Restore device-link guidance** on install/activate paths | Fixes Telegram setup regression |
| [#7820](https://github.com/nearai/ironclaw/pull/7820) | **Scope-isolation suite consolidation probe** — measurement-gated follow-up to T2 | Data-driven test strategy |
| [#7816](https://github.com/nearai/ironclaw/pull/7816) | **OOBE suggestion drawer** — refresh and connect entries | Onboarding flow completion (frontend half of #7815) |
| [#7894](https://github.com/nearai/ironclaw/pull/7894) | **Reduce required scope checkout transfer** — partial-clone filter, depth-1 checkouts | CI optimization |

**Design-system epics progressed:** Phase 1 ([#7038](https://github.com/nearai/ironclaw/issues/7038)) closed; Phases 2–3 ([#7781](https://github.com/nearai/ironclaw/issues/7781)) and 4–5 ([#7782](https://github.com/nearai/ironclaw/issues/7782)) remain active with the foundation PR ([#7831](https://github.com/nearai/ironclaw/pull/7831)) adding a Chromatic visual-regression lane.

---

## 4. Community Hot Topics

**Most discussed Issue this window:**

- **[#7732 — Persistent per-user sandbox (epic, v1.4.0, roadmap)](https://github.com/nearai/ironclaw/issues/7732)** — 9 comments, 0 👍. The project's largest open epic: persistent sandbox with iron-proxy, deferring loop executors. This is the architectural backbone for v1.4.0.

**Design-system epic family (3 epics, 2 merged threads):**
- [#7038](https://github.com/nearai/ironclaw/issues/7038) (closed), [#7781](https://github.com/nearai/ironclaw/issues/7781), [#7782](https://github.com/nearai/ironclaw/issues/7782) — collectively 6 comments. The re-scoping story is clear: Phase 1 delivered, Phases 2–3 in-flight with the Chromatic foundation, Phases 4–5 queued.

**Theme: notification-center evolution.** A burst of 8 issues ([#7871](https://github.com/nearai/ironclaw/issues/7871) through [#7880](https://github.com/nearai/ironclaw/issues/7880)) from the same author signals a coordinated hardening sprint rather than community demand.

**Underlying needs:** The most-commented items are all **infrastructure and experience epics** (sandbox persistence, design system, notification durability) — indicating an operator/enterprise-focused user base more concerned with reliability and polish than feature sprawl, plus a **Slack-channel roadmap** ([#4625](https://github.com/nearai/ironclaw/issues/4625), 1 comment) that keeps recurring.

---

## 5. Bugs & Stability

**Ranked by severity:**

| Severity | Issue | Description | Fix Status |
|---|---|---|---|
| 🔴 **High** | [#7862](https://github.com/nearai/ironclaw/issues/7862) | **Telegram device-link fails** with generic error when `telegram_api_id`/`api_hash` unconfigured | Companion fix [#7861](https://github.com/nearai/ironclaw/pull/7861) merged for install/activate path; deeper lookup-path issue remains in [#7887](https://github.com/nearai/ironclaw/issues/7887) |
| 🔴 **High** | [#7892](https://github.com/nearai/ironclaw/issues/7892) | **Agent loop stuck 15x on same tool, 123s runtime** — no terminating guard, 4 distinct calls repeated | Open; risk: medium; no fix PR yet |
| 🟠 **Medium** | [#7888](https://github.com/nearai/ironclaw/issues/7888) | **Log retrieval hangs indefinitely** on multiple instances | Open; user-reported with multi-instance confirmation |
| 🟠 **Medium** | [#7891](https://github.com/nearai/ironclaw/issues/7891) | **49 KB of raw MIME pushed to prompt** — 14.3s inference waste on two emails; 19.2s of a 19.7s turn | Open; performance bug with clear repro |
| 🟡 **Low** | [#7853](https://github.com/nearai/ironclaw/issues/7853) | **Telegram personal-account linking** missing tool (root cause of #7862 symptom) | [#7861](https://github.com/nearai/ironclaw/pull/7861) provides partial fix; #7887 splits remaining work |

**Notable PR addressing stuck-related issue:** [#7884](https://github.com/nearai/ironclaw/pull/7884) — **wall-clock occupancy cap** on interactive turns (10-minute bound) to prevent infinite holds on the one-active-run lock; honest queued-busy copy. Open, awaiting review.

---

## 6. Feature Requests & Roadmap Signals

**Strong v1.4.0 candidates:**

| Request | Issue | Why it's likely |
|---|---|---|
| **Remote edge workers** (RFC) | [#7889](https://github.com/nearai/ironclaw/issues/7889) | RFC status + "already supports local workers, Docker sandbox, WASM" — natural extension |
| **Personality editor in Settings** (agent.md) | [#7895](https://github.com/nearai/ironclaw/issues/7895) | User-reported pain point; small surface addition; ships with design-system work |
| **Voice-to-text in composer** | [#7867](https://github.com/nearai/ironclaw/issues/7867) | Explicitly scoped as an epic; channel parity argument (Slack/Telegram have it) |
| **Slack-to-console bridge + rich interactive UX** | [#7871](https://github.com/nearai/ironclaw/issues/7871) | New epic (created yesterday); aligns with long-running Slack channel work [#4625](https://github.com/nearai/ironclaw/issues/4625) |
| **Per-automation lessons file** | [#7893](https://github.com/nearai/ironclaw/issues/7893) | Clean architectural fit with memory systems; solves recurring operational learning loss |

**Design-system remaining work**: Phases 2–3 (DESIGN.md governance, theme reskin) and 4–5 (agentic interactions, IA) are roadmap-committed — high confidence of landing in v1.4.0.

**Prediction:** The **notification-center expansion** (8 issues from italic-jinxin) and **design-system completion** are the two most likely candidates for v1.4.0 inclusion, given the density of coordinated PRs and Epic tracking. The **Slack + voice** features may slip to v1.5.

---

## 7. User Feedback Summary

**Most direct user pain signal:** [#7895](https://github.com/nearai/ironclaw/issues/7895) — "me trying to set up personality with ironclaw" — a user struggling with agent personality configuration, explicitly requesting a Settings UI section. This is a **discoverability + UX gap**.

**Operational failures users are reporting on production instances (Railway):**
- Telegram bot setup works, but personal-account linking fails with an **unhelpful generic error** ([#7862](https://github.com/nearai/ironclaw/issues/7862)) — users cannot self-diagnose.
- Log retrieval **hangs indefinitely** across two separate instances ([#7888](https://github.com/nearai/ironclaw/issues/7888)) — blocking observability.
- Model agents **get stuck in loops** (79s/86s/123s runs repeating the same 4 tool calls) ([#7892](https://github.com/nearai/ironclaw/issues/7892)) — a reliability concern for automation trust.

**Satisfaction signals:** The notification-center migration (legacy fallback removed, durable inbox exclusive) suggests users received the inbox positively, and the rapid CI convergence ([#7817](https://github.com/nearai/ironclaw/pull/7817), [#7819](https://github.com/nearai/ironclaw/pull/7819)) indicates **responsive maintainer velocity** that users will likely view favorably.

---

## 8. Backlog Watch

| Item | Age | Status | Why it matters |
|---|---|---|---|
| **[#4625 — Slack channel-routed agents](https://github.com/nearai/ironclaw/issues/4625)** | 78 days (created 2026-06-09) | Open; 1 comment; roadmap-tagged | Long-standing core channel ask; only 1 comment suggests maintainer attention is thin relative to its roadmap prominence; new [#7871](https://github.com/nearai/ironclaw/issues/7871) may supersede/absorb it |
| **[#7491 — omp core-tool contract + engines](https://github.com/nearai/ironclaw/pull/7491)** | 15 days open | Size: XL, risk: medium; 6 exact tool names (`read`, `write`, `edit`, `glob`, `grep`, `bash`) | Large architectural PR without visible reviewer action in last 24h — may be stuck on review capacity |
| **[#7516 — IronHub agent-link operator surface](https://github.com/nearai/ironclaw/pull/7516)** | 14 days open | New contributor (neo-sky); Size: XL | Long-open newcomer PR needs maintainer attention to avoid contributor churn |
| **[#7732 — Persistent per-user sandbox epic](https://github.com/nearai/ironclaw/issues/7732)** | 8 days | 9 comments; most-active thread | Largest v1.4.0 dependency; activity is steady (updated yesterday) but no PRs yet attached — watch for stalled progression |

**Risk signal:** Two XL-sized PRs ([#7491](https://github.com/nearai/ironclaw/pull/7491), [#7516](https://github.com/nearai/ironclaw/pull/7516)) have been open 14–15 days without closing — combined with the flood of new issues today, maintainer bandwidth may be the constraint clearing the backlog.

---

### Project Health Summary

**Positive:** High merge velocity (11 PRs, including 4 CI-infrastructure wins), coordinated epic management, strong bug triage (issues promoted to PRs within hours), and a healthy new-contributor pipeline.

**Concerning:** A hot cluster of **user-facing reliability bugs** (log hangs, Telegram linking, agent loops) on production Railway instances suggests the v1.4.0 hardening pass is needed sooner rather than later. The 3:1 open-to-closed issue ratio at a 24-hour snapshot may reflect either active discovery (healthy) or undersized triage (unhealthy) — the prompt closure of #7799 and #7038 suggests the former.

**Watch items for next digest:** Whether [#7892](https://github.com/nearai/ironclaw/issues/7892) (agent loop guard) and [#7888](https://github.com/nearai/ironclaw/issues/7888) (log hang) receive fix-PR assignments within 48 hours — speed here is the strongest health indicator for this project.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-26

## 1. Today's Overview

LobsterAI is in an active release and feature-development cycle. Two releases shipped this week (2026.8.21 and 2026.8.25), and the project saw 9 PRs merged/closed and 2 releases cut in the last 24 hours, indicating strong, sustained maintainer momentum. The feature focus is clearly on the "library/artifacts" domain (local artifact lifecycle, preview, analytics) and the settings/renderer layer (plan model catalog, UI polish). Community engagement is currently low—with only 1 open issue (a WeChat group capacity request) and no bug reports—suggesting a settled user base with no immediate stability concerns. One long-open feature PR (`Session Fork`) and one dependency-bump PR remain in the backlog.

## 2. Releases

Two new releases were cut this week:

- **LobsterAI 2026.8.25** (released 2026-08-25)
  - `feat: library` — new library feature merge.
  - `feat(library):` enhanced cross-platform thumbnails and local artifact lifecycle management.
  - `feat(library):` optimized local artifact preview and interaction experience.
- **LobsterAI 2026.8.21** (released 2026-08-21)
  - `feat(dsh):` added usage analytics for enable toggle and workbench open.
  - `feat:` updated dsh to 0.1.1-rc.1.
  - `refactor(dsh):` moved usage analytics logic (details truncated in data).

No breaking changes or migration notes were flagged in either release.

## 3. Project Progress

Nine PRs were merged/closed in the last 24 hours. The most notable feature work:

- **[PR #2535](https://github.com/netease-youdao/LobsterAI/pull/2535) `feat(settings): add plan model catalog`** (closed) — Adds a plan model catalog to settings UI.
- **[PR #2530](https://github.com/netease-youdao/LobsterAI/pull/2530) `feat(settings): add plan model catalog`** (closed) — Companion implementation: adds a "plan model" tab above custom model settings, loads pricing catalog (text/image/video), renders categorized model cards with sticky controls, and adds lightweight diagnostics.
- **[PR #2529](https://github.com/netease-youdao/LobsterAI/pull/2529) `feat(analytics): 完善资料库埋点与发布转化归因`** (closed) — Adds library exposure, filter, search, preview, favorite, and refresh analytics events. Uses bucketed data (not raw content) for search analytics. Adds 7-day last-touch attribution from publish CTA to paid subscription state, with retry on failure and cleanup on logout. Also removes the standalone website entry, consolidating site management into the library.
- **[PR #2531](https://github.com/netease-youdao/LobsterAI/pull/2531) `fix(library): 修复本地产物后台刷新闪烁`** (closed) — Splits first-load, background-refresh, and pagination states to avoid full-page skeleton flicker; merges history backfill and file watcher events; adds batch artifact query API for targeted updates; in-place merge of new/changed/invalid artifacts while preserving filter/pagination/scroll; removes affected artifact IDs on task delete; adds comprehensive tests.
- **[PR #2533](https://github.com/netease-youdao/LobsterAI/pull/2533) `fix(artifacts): 区分网页与本地服务的预览展示`** (closed) — Distinguishes HTML pages from local services in preview UI (different icons, labels, and behavior), adds HTM file mapping and i18n text, updates design docs.

Also merged: **[PR #2532](https://github.com/netease-youdao/LobsterAI/pull/2532)** (fade out login promo tip after 5s, clean up timers), and release PR **[#2534](https://github.com/netease-youdao/LobsterAI/pull/2534)** for 2026.8.20. Two stale CI dependency bumps ([#1275](https://github.com/netease-youdao/LobsterAI/pull/1275), [#1276](https://github.com/netease-youdao/LobsterAI/pull/1276)) were closed.

## 4. Community Hot Topics

Activity is very low on the community front this cycle:

- **[Issue #2536](https://github.com/netease-youdao/LobsterAI/issues/2536): "微信群已满人" (WeChat group is full)** — 1 comment. Created/updated 2026-08-25. Community member requests another WeChat group as the current one is at capacity. This signals healthy community growth and a desire for more direct support channels. Underlying need: **community scaling and official communication channels**.

No PRs attracted meaningful discussion (comments/reactions data was not captured for most, and counts are at 0).

## 5. Bugs & Stability

No new bug reports were filed in the last 24 hours (0 issues closed, 1 open issue is a community request, not a bug). However, two stability-related fixes were merged:

- **[PR #2531](https://github.com/netease-youdao/LobsterAI/pull/2531)**: Fixed library background-refresh flicker (skeleton flash on pagination/refresh) — a user-visible UI regression fix.
- **[PR #2532](https://github.com/netease-youdao/LobsterAI/pull/2532)**: Fixed timer leak / unhandled promo timer on auth state change.

Neither has a severity tag, but the flicker fix addresses a likely common UX annoyance in the library view.

## 6. Feature Requests & Roadmap Signals

- **Plan model catalog / pricing UI** ([#2535](https://github.com/netease-youdao/LobsterAI/pull/2535), [#2530](https://github.com/netease-youdao/LobsterAI/pull/2530)): This work was merged, so the next release will likely expose a new pricing/model selection surface in settings. This is a strong signal LobsterAI is building toward monetization/plan differentiation.
- **Library analytics & conversion attribution** ([#2529](https://github.com/netease-youdao/LobsterAI/pull/2529)): Instrumented library interactions and paid-subscription attribution — roadmap signal for **trial-to-paid conversion optimization**.
- **Standalone website entry removed, consolidated into library**: Suggests a deliberate UX simplification, possibly ahead of a larger information-architecture revamp.
- **[PR #1159: `feat(cowork): add session fork`](https://github.com/netease-youdao/LobsterAI/pull/1159)** (open since 2026-03-31, still open): a long-pending feature enabling users to fork/snapshot cowork sessions from the detail view. It's a well-specified PR but has sat untouched for ~5 months — upcoming priority likely depends on backlog triage.

Prediction: the next minor release will include the plan model catalog, the new analytics events, and the artifact preview distinction fixes (all merged and likely part of the 2026.8.20/25 releases). The session fork feature is a candidate for the next feature milestone if maintainers pick it up.

## 7. User Feedback Summary

- **Positive signal**: The only user-originated issue is a request for an additional WeChat group ([#2536](https://github.com/netease-youdao/LobsterAI/issues/2536)) — indicating a growing, engaged user community, potentially in the Chinese market.
- **UX pain point (fixed)**: Library background-refresh flicker was a visible annoyance; fixed in [#2531](https://github.com/netease-youdao/LobsterAI/pull/2531).
- **No dissatisfaction signals** in the current cycle (no bug reports, no negative comments).

Overall user sentiment appears neutral-to-positive, with no reported blocking issues.

## 8. Backlog Watch

- **[PR #1159: `feat(cowork): add session fork`](https://github.com/netease-youdao/LobsterAI/pull/1159)** — Open since 2026-03-31 (5 months). A substantial, well-scoped feature that has not received maintainer attention. Needs review/decision: merge, request changes, or close.
- **[PR #1277: `chore(deps-dev): bump the electron group (electron 40 → 43)`](https://github.com/netease-youdao/LobsterAI/pull/1277)** — Open since 2026-04-02. A routine dependency bump, but it has been pending for ~5 months; likely has merge conflicts by now. Worth triaging to keep the dependency tree current.
- **[Issue #2536](https://github.com/netease-youdao/LobsterAI/issues/2536) "WeChat group is full"** — should be addressed quickly (create a new group or update links) to avoid community friction.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for 2026-08-26.

---

# Moltis Project Digest: 2026-08-26

## 1. Today's Overview
Moltis is in a high-velocity development phase, with 5 pull requests updated in the last 24 hours (4 open, 1 merged) and only 2 issues updated. Activity is heavily weighted toward feature development and integration fixes rather than bug triage, indicating a project in active expansion. The current focus is on expanding remote and cloud-based sandboxing backends (Coder, Kubernetes), while also hardening tool integration compatibility (Brave, Fastmail, OpenAI schemas). Maintenance velocity is high, with critical fixes being merged within 24 hours of being opened. No new releases were published today, suggesting the project is accumulating changes for a future patch or minor release.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
- **Merged:** PR [#1243](https://github.com/moltis-org/moltis/pull/1243) fix(cron): preserve delivered channel context — Fixes follow-up questions losing context when a scheduled message is delivered to WhatsApp or other channels. Cron execution remains isolated, but the final delivered text is appended as an assistant message, ensuring conversation continuity.
- **Advanced:** PR [#1199](https://github.com/moltis-org/moltis/pull/1199) Add Coder remote workspace sandbox support — This long-running PR (open since 8/15) is progressing. It creates ephemeral workspaces via the REST API and executes commands over reconnecting PTY WebSockets, with support for templates, presets, TTLs, and automatic backend selection.
- **Advanced:** PR [#1232](https://github.com/moltis-org/moltis/pull/1232) fix(tools): make object schemas OpenAI-safe — Fixes issues where OpenAI's strict tool schemas forced Codex to send null/empty values for webhook patch fields and MCP environment variables.

## 4. Community Hot Topics
- **[Issue #1118 Open] Kubernetes-native sandbox backend** ([Link](https://github.com/moltis-org/moltis/issues/1118)) — The most active item with 2 comments and 1 reaction. This is a major feature proposal for spawning ephemeral Kubernetes pods with `runtimeClassName` support for VM-level isolation (Kata Containers, gVisor). The project has a related open PR ([#1199](https://github.com/moltis-org/moltis/pull/1199) for Coder), indicating a clear strategic push toward remote and containerized sandboxing options.

## 5. Bugs & Stability
- **[Medium—Fixed]** Issue [#1224](https://github.com/moltis-org/moltis/issues/1224) "[Bug]: Tools stop working in shared Slack channels" was closed. The issue was reported on 8/21 and closed on 8/25, demonstrating a quick turnaround. No linked fix PR is visible in the current data, suggesting the resolution may have been config/documentation-based or fixed in a separate commit.
- **[Related Fix]** PR [#1243](https://github.com/moltis-org/moltis/pull/1243) addresses a related context-loss bug in scheduled messages across channels (WhatsApp), reinforcing that multi-channel message routing is an area seeing active bug-fix work.

## 6. Feature Requests & Roadmap Signals
The dominant roadmap signal is **expanding sandbox backend options** beyond local execution:
- **Kubernetes backend** ([#1118](https://github.com/moltis-org/moltis/issues/1118)): This is a significant request for enterprise/cloud-native deployments, specifically supporting VM-level isolation runtimes like Kata/gVisor.
- **Coder remote workspaces** (PR [#1199](https://github.com/moltis-org/moltis/pull/1199)): A direct implementation of remote workspace execution.

Given both are active concurrently, the next minor version of Moltis will likely include a suite of advanced sandboxing backends (Kubernetes + Coder), positioning the tool as a serious option for secure, distributed agent execution. The OpenAPI tool schema fixes ([#1232](https://github.com/moltis-org/moltis/pull/1232)) and Brave parameter validation ([#1245](https://github.com/moltis-org/moltis/pull/1245)) suggest a parallel focus on strict compliance with external platform requirements.

## 7. User Feedback Summary
- **Enterprise Need:** The Kubernetes feature request ([#1118](https://github.com/moltis-org/moltis/issues/1118)) signals demand from users who need to run agents in production with strict isolation policies, likely in regulated environments (finance, healthcare).
- **Third-Party Integration Friction:** Users are actively hitting walls with specific platform constraints (OpenAI strict schemas, Brave search localization, Fastmail OAuth scopes). The project is responding quickly with targeted fixes (PRs [#1232](https://github.com/moltis-org/moltis/pull/1232), [#1245](https://github.com/moltis-org/moltis/pull/1245), [#1244](https://github.com/moltis-org/moltis/pull/1244)), indicating a healthy feedback loop with the community.
- **Cross-Channel UX:** The cron/WhatsApp context fix ([#1243](https://github.com/moltis-org/moltis/pull/1243)) addresses user pain around fragmented conversations when agents send scheduled messages to other channels.

## 8. Backlog Watch
- **[Issue #1118](https://github.com/moltis-org/moltis/issues/1118) (Open since 6/12):** The Kubernetes sandbox feature request remains the oldest and highest-signal open item. However, it is actively referenced by ongoing PRs, so it is not ignored. Maintainers should consider formalizing this as a roadmap item with a target milestone.
- **PR [#1199](https://github.com/moltis-org/moltis/pull/1199) (Open since 8/15):** This large PR for the Coder backend has been open for 10 days. While it is being updated, the length and complexity of the diff may require a dedicated review window to avoid stalling. It is currently the longest-pending feature PR.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-26

## Today's Overview

CoPaw (QwenPaw) is showing high development velocity with 84 combined issue/PR updates in the last 24 hours, including 1 new release, 14 closed issues, and 29 merged/closed PRs. The project released **v2.1.1-beta.3** with a dependency pin and documentation fixes, indicating ongoing stabilization of the 2.1.1 beta line. Community engagement is strong, particularly around Windows-specific bugs (memory leaks, installer issues), MCP session resilience, and UX quality-of-life improvements. Notable contributions include a security fix for master key file permissions and a substantial test coverage increase (+5.02pp). The project maintains a healthy mix of bug fixes, feature work, and infrastructure improvements, though several long-standing PRs remain open without maintainer review.

## Releases

**[v2.1.1-beta.3](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.1.1-beta.3)** — Released 2026-08-25

Changes:
- chore(console): pin @agentscope-ai/chat to 1.1.72 (via #7257)
- docs(loop-engineering): fix PluginAPI casing to PluginApi (via #7269)
- test(integration): expand integration test coverage (truncated in data)

**Migration Notes:** None required. This is a minor beta refinement release focused on dependency stabilization and documentation consistency. No breaking changes or migration steps identified.

## Project Progress

**Security Fix:** [#7119](https://github.com/agentscope-ai/QwenPaw/pull/7119) — `fix(security): create the master key file with owner-only permissions` (open, by Yigtwxx). Fixes a contract violation where the Fernet master key file was not created with `0o600` permissions as documented. Critical for credential security.

**Session Thinking Modes:** [#7163](https://github.com/agentscope-ai/QwenPaw/pull/7163) — `feat: refine session thinking and model management` (open, by zhaozhuang521). Adds session-level thinking modes (Off/Low/Medium/High) with cross-device sync via Chat Metadata, applied with higher priority than agent-level settings.

**Provider Catalog Refresh:** [#7277](https://github.com/agentscope-ai/QwenPaw/pull/7277) — `fix(providers): refresh Aliyun and Kimi model catalogs` (open, by wangfei010313). Removes retired Kimi model IDs, adds newly available models, and drops unsupported Aliyun Coding Plan IDs.

**CI Improvements:** [#7293](https://github.com/agentscope-ai/QwenPaw/pull/7293) — `feat(ci): split tests.yml integration tests into three parallel shards (p0/p1/p2)` (open, by yutai78786). Reduces CI wall-clock time by parallelizing integration test execution.

**Test Coverage Boost:** [#7292](https://github.com/agentscope-ai/QwenPaw/pull/7292) — `test(coverage): add 19 unit test files (+5.02pp coverage)` (open, by yutai78786). Adds 1,148 tests, raising backend unit coverage from 58.04% to 63.06%, plus fixes `/root` classification in `safety_checks.py`.

**Media Handling:** [#7294](https://github.com/agentscope-ai/QwenPaw/pull/7294) — `feat(media): add opt-in image resizing by pixel limit` (open, by qbc2016). Adds `QWENPAW_MAX_IMAGE_PIXELS` env-controlled resizing to prevent provider pixel-limit errors.

**Chat Payload Rejection:** [#7299](https://github.com/agentscope-ai/QwenPaw/pull/7299) — `fix(console): reject conflicting chat payloads` (open, first-time contributor chrischen-coder). Fixes silent payload acknowledgment when a second POST arrives for an active run.

**Channel Contract Portability:** [#7264](https://github.com/agentscope-ai/QwenPaw/pull/7264) — `fix(channels): make contract checks portable and complete` (open, by kaiwangleo). Fixes UnicodeDecodeError on Windows and extends coverage to `SIPChannel` implementations.

**AgentScope Bump:** [#7276](https://github.com/agentscope-ai/QwenPaw/pull/7276) — `chore(deps): bumping version of agentscope to 2.0.7` (closed/merged, by qbc2016).

**QwenPaw Data Packaging:** [#7190](https://github.com/agentscope-ai/QwenPaw/pull/7190) — `feat(qwenpaw-data): PyPI runtime path, docker-compose one-shot demo, and env inheritance fix` (open, by cyruszhang). Makes qwenpaw-data installable via `pip install qwenpaw[qwenpaw-data]` with seeded GAAP demo stack.

**Creator 1.1.1:** [#7274](https://github.com/agentscope-ai/QwenPaw/pull/7274) — `feat(creator) 1.1.1: live website and desktop operation` (open, by xuanrui-L). Adds take recording, Bailian Wan3 video, and APE-benchmark review operators.

**Closed/merged older PRs today:** [#2773](https://github.com/agentscope-ai/QwenPaw/pull/2773) (self-evolution skill), [#5414](https://github.com/agentscope-ai/QwenPaw/pull/5414) (decouple skill SOP/judgement rules), [#1228](https://github.com/agentscope-ai/QwenPaw/pull/1228) (read_media tool), [#1525](https://github.com/agentscope-ai/QwenPaw/pull/1525) (cron isolation), [#4881](https://github.com/agentscope-ai/QwenPaw/pull/4881) (MiniMax M3), [#2304](https://github.com/agentscope-ai/QwenPaw/pull/2304) (404 models.list handling), [#1552](https://github.com/agentscope-ai/QwenPaw/pull/1552) (default_headers for custom providers).

## Community Hot Topics

**[#338 — Webhook feature request](https://github.com/agentscope-ai/QwenPaw/issues/338)** (9 comments, open since March) — User requests webhook integration to send messages to CoPaw and receive callbacks via a polling key. This long-running thread (6 months) shows sustained demand for async/interop integration patterns.

**[#7258 — WeChat channel "show thinking" setting ineffective](https://github.com/agentscope-ai/QwenPaw/issues/7258)** (6 comments, by rerbin) — Setting to hide thinking process in WeChat channel is ignored; thinking output still displayed. Reported on v2.1 web. Impacts users who find reasoning traces noisy in chat channels.

**[#6524 — MCP session not auto-recovering after backend restart](https://github.com/agentscope-ai/QwenPaw/issues/6524)** (6 comments, by ruijie-shilu) — With `streamable_http`, after MCP server restart, QwenPaw reuses stale `mcp-session-id`, causing tool query failures until manual `list mcp`. This is a significant reliability gap for remote MCP usage.

**[#7261 — Runaway SSE serialization loop after agent-to-agent run](https://github.com/agentscope-ai/QwenPaw/issues/7261)** (4 comments, closed) — v2.1.1b2 enters infinite SSE loop causing 100% CPU, unbounded memory, unresponsive server. Closed as resolved, but represents a serious stability concern.

**[#6810 — Windows installer fails with locked files](https://github.com/agentscope-ai/QwenPaw/issues/6810)** (5 comments, by 0959linger) — NSIS installer throws "cannot write file" errors because NM host lock files prevent overwrite. Recommends terminating processes before install/update.

## Bugs & Stability

**P0 — Critical**

1. **[#7261 — SSE serialization runaway loop](https://github.com/agentscope-ai/QwenPaw/issues/7261)** (closed) — Infinite SSE loop after agent-to-agent run; 100% CPU, unbounded memory, server unresponsive. Fix verified in 2.1.1b2 timeframe. Monitor for regressions.

2. **[#5720 — Memory leak in v1.1.12.post2](https://github.com/agentscope-ai/QwenPaw/issues/5720)** (closed) — Memory grows ~5.5MB/min from 150MB to 580MB within 64 min; async task leak + unclosed HTTP sessions leading to corrupted config on kill. Closed; verify fix holds in 2.x builds.

3. **[#7285 — Long-conversation performance degradation causing system lockup](https://github.com/agentscope-ai/QwenPaw/issues/7285)** (closed) — v2.1.1b2 web UI: after 1-2 min self-generation, entire computer becomes unresponsive (2s per frame). Task manager also stuck with no high resource usage. Closed — likely related to #7261 SSE issue; needs release verification.

**P1 — High**

4. **[#7259 — Rapid memory growth stuck in "Thinking" on Windows](https://github.com/agentscope-ai/QwenPaw/issues/7259)** (open, help wanted) — `qwenpaw-backend.exe` memory increases rapidly when stuck in "Thinking" with SiliconFlow or other providers. Help-wanted call for reproductions — maintainers actively investigating.

5. **[#7298 — OpenSSL 3.0.x TLS stack in Tauri desktop bundle](https://github.com/agentscope-ai/QwenPaw/issues/7298)** (open, by LUOSENGWA) — Python 3.11 runtime ships OpenSSL 3.0.x; carrier middleboxes reset handshakes for self-hosted HTTPS. Suggests bumping desktop CI to Python 3.13.

6. **[#7296 — OpenAI Responses multi-turn 400 "reasoning item not found"](https://github.com/agentscope-ai/QwenPaw/issues/7296)** (open, by huajiao1998) — Multi-turn with stateless upstreams (OpenCode Zen/Go Muse Spark) fails on 2nd turn with `Referenced reasoning item 'rs_...' not found or has expired`. No workaround documented.

**P2 — Medium**

7. **[#6524 — MCP session recovery](https://github.com/agentscope-ai/QwenPaw/issues/6524)** (open) — No auto-recovery after backend restart; manual `list mcp` required. Likely needs client-side session invalidation/retry.

8. **[#7218 — Peer closed connection (incomplete chunked read)](https://github.com/agentscope-ai/QwenPaw/issues/7218)** (open) — Frequent on long texts/thinking with custom models; user reports client disconnects at 130-140s while provider waits 180s. Insufficient timeout configurability.

9. **[#7288 — MCP large results bypass compaction](https://github.com/agentscope-ai/QwenPaw/issues/7288)** (open) — Large MCP responses in active turns can overflow model context, bypassing scroll compaction. Relevant for enterprise analytics workloads.

**P3 — Low / Edge Cases**

10. [#7129](https://github.com/agentscope-ai/QwenPaw/issues/7129) (closed) — Console drop-frames in long sessions + streaming; WPR-traced to Chrome rendering main thread block.
11. [7228](https://github.com/agentscope-ai/QwenPaw/issues/7228) (closed) — App Market UI shows "Install" on installed apps.
12. [7282](https://github.com/agentscope-ai/QwenPaw/issues/7282) (open) — Markdown lists render with excessive vertical spacing.
13. [7256](https://github.com/agentscope-ai/QwenPaw/issues/7256) (closed) — "App" renamed to "Market" in sidebar, community prefers original naming.
14. [7297](https://github.com/agentscope-ai/QwenPaw/issues/7297) (open) — QQ channel restart loses last conversation memory.

## Feature Requests & Roadmap Signals

**High likelihood for next release:**

- **[#338 — Webhook/async callback API](https://github.com/agentscope-ai/QwenPaw/issues/338)** — Long-standing (6 months) external integration request with 9 comments. Suggests growing need for headless/API-first usage patterns.

- **[#7196 — Collapsible reasoning process display](https://github.com/agentscope-ai/QwenPaw/issues/7196)** (closed with 👍) — Default-collapse option for thinking output, citing hermes/OAI convention. Aligns with #7258 (WeChat thinking display) — both point to reasoning visibility controls as a UX priority.

- **[#7182 — Workspace-scoped Skill preload policy](https://github.com/agentscope-ai/QwenPaw/issues/7182)** (open, by wuyak) — `on_demand` vs `preload` skills per workspace to avoid first-turn tool discovery overhead. Directly improves latency and token efficiency.

- **[#7279 — Popup selection for model choices](https://github.com/agentscope-ai/QwenPaw/issues/7279)** (closed) — Replace input-based option selection with clickable popups (hermes-style). UX improvement with clear precedent.

**Medium likelihood:**

- **[#7013 — Unified tool panel with Web preview + interactive terminal](https://github.com/agentscope-ai/QwenPaw/issues/7013)** (closed) — Comprehensive "workbench" for agent development: file preview, diff view, web service preview, terminal.

- **[#7263 — Task-completion indicator](https://github.com/agentscope-ai/QwenPaw/issues/7263)** (closed) — Bottom bar activity tab turns orange when background tasks finish.

- **[#7280 — Auto-clear completed background tasks](https://github.com/agentscope-ai/QwenPaw/issues/7280)** (open) — Configurable auto-cleanup for finished tasks.

- **[#7287 — Zero-intrusion "skin gateway"](https://github.com/agentscope-ai/QwenPaw/issues/7287)** (open) — AI-agent-authored theming proposal; interesting signal for extensibility demand but low priority vs functional issues.

## User Feedback Summary

**Pain Points:**

1. **Windows stability issues dominate** — Installer lock failures (#6810), memory leaks (#5720), stuck "Thinking" states (#7259). Windows users experience a disproportionate share of critical reliability bugs.

2. **MCP reliability is a recurring gap** — Session recovery (#6524), large-result context overflow (#7288). Power users with remote/enterprise MCP setups are hitting infrastructure-level friction.

3. **Long-session performance** — 100% CPU loops (#7261), browser drop-frame (#7129), system-wide lockup (#7285). The 2.1.x beta series has had meaningful performance regressions that erode user trust.

4. **The thinking-reasoning display controversy** — Users are split: some want it always visible, others find it distracting noise (#7196). WeChat channel users want it fully suppressed (#7258). The current default is too prominent for many workflows.

5. **Timeout/chunking defaults don't match custom models** — #7218 shows mismatch between QwenPaw's disconnect timing and upstream providers' expectations. Users want configurable timeouts.

**Satisfaction Signals:**

- Users actively citing hermes as UX benchmark (#7196, #7279) — they believe QwenPaw can/should match premium UX.
- Non-Chinese-language issues appearing (#7288, #7296, #7298) — growing international adoption.
- Community self-organizing help-wanted participation (#7259) — healthy contributor ecosystem.
- Named-pipe level detail in bug reports (#7129 with WPR traces) — sophisticated user base providing quality diagnostics.

## Backlog Watch

**PRs awaiting maintainer action (open 2-5 months):**

1. **[#2773 — Self-evolution skill (self-improving agent engine)](https://github.com/agentscope-ai/QwenPaw/pull/2773)** — Open since April 1 (147 days). Substantial feature: automatic error capture, pattern detection, LLM-based root-cause analysis. No maintainer engagement visible.

2. **[#5414 — Decouple skill SOP and judgement rules](https://github.com/agentscope-ai/QwenPaw/pull/5414)** — Open since June 23 (63 days). Changes skill architecture significantly: rules.json independent from SKILL.md, with conversation + frontend editing. Architecture-impacting; needs design review.

3. **[#4881 — MiniMax M3 flagship model](https://github.com/agentscope-ai/QwenPaw/pull/4881)** — Open since June 1 (85 days). Simple catalog addition for a flagship model. Low risk, should be mergeable.

4. **[#1552 — default_headers support for custom providers](https://github.com/agentscope-ai/QwenPaw/pull/1552)** — Open since March 16 (162 days). Custom headers for OpenAI-compatible providers (auth, User-Agent). High practical value; unclear why pending.

5. **[#2304 — Treat 404 from models.list as success](https://github.com/agentscope-ai/QwenPaw/pull/2304)** — Open since March 25 (154 days). One-line compatibility fix for MiniMax Anthropic-compatible endpoints. Regression-risk minimal.

6. **[#1228 — read_media tool](https://github.com/agentscope-ai/QwenPaw/pull/1228)** — Open since March 11 (168 days). Image/video/audio processing with compression. Broad utility; stalled despite first-time contributor.

**Notable issues needing attention:**

7. **[#6524 — MCP auto-recovery](https://github.com/agentscope-ai/QwenPaw/issues/6524)** — Open 29 days with clear repro and no maintainer response. Affects remote MCP reliability.

8. **[#7288 — Large MCP context bypass](https://github.com/agentscope-ai/QwenPaw/issues/7288)** — Only 1 day old but identifies an architectural gap (context compaction bypass) for enterprise workloads.

---

*Digest generated 2026-08-26 from GitHub data. Data reflects the 24-hour window ending 2026-08-25T23:59:59Z.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-26

## Today's Overview

ZeroClaw is in a highly active development phase, with a heavy focus on security hardening, runtime architecture refinement, and RFC-driven governance. The repo shows 50 issues and 50 PRs updated in the last 24 hours, with a healthy mix of open/active work (38 open issues, 49 open PRs) and a modest number of closures (12 issues, 1 PR). The development cadence is strong, with several high-risk, security-critical PRs (credential cache hardening, skill HTTP egress bounding, symlink race prevention) landing in review. The project is clearly approaching a major release, evidenced by the v0.9.0 milestone tracker (#7432) and the high volume of RFCs and architecture-level discussions, though no new official release was cut in this period. A governance framework is actively managing the decision queue, and the community is engaged around security boundaries and architectural improvements.

## Releases

No new releases were published in the last 24 hours.

## Project Progress

One PR was merged/closed in the last 24 hours:

- **[#10042 (CLOSED) bug(ci): MSRV system dependency installation can consume job timeout](https://github.com/zeroclaw-labs/zeroclaw/issues/10042)** — [Audacity88] — A CI bug fix ensuring the MSRV (Minimum Supported Rust Version) job no longer hits the 20-minute timeout during system dependency installation, which blocked the MSRV Cargo check from completing.

Additionally, several issues were closed, indicating completed feature work or accepted fixes:

- **[#9663 (CLOSED) fix(channels): bind Voice Wake to the agent transcription provider](https://github.com/zeroclaw-labs/zeroclaw/issues/9663)** — [Audacity88] — Resolves Voice Wake transcription using the owning agent's configured provider, instead of incorrectly passing the channel alias as a provider key.
- **[#10257 (CLOSED) [Bug]: cron update --command writes unused column on agent jobs](https://github.com/zeroclaw-labs/zeroclaw/issues/10257)** — [zyw02] — A degraded behavior fix (S2) where the CLI flag wrote an unused column, now remapped correctly on agent jobs.
- **[#10271 (CLOSED) chore(util): consolidate crate-local floor_char_boundary copies onto std](https://github.com/zeroclaw-labs/zeroclaw/issues/10271)** — [JordanTheJet] — A mandated refactor consolidating three crate-local UTF-8 truncation helpers onto the stabilized `str::floor_char_boundary`, following the project's internal audit.
- **[#10058 (CLOSED) [Bug]: ZeroCode file explorer search mode ignores row and page navigation](https://github.com/zeroclaw-labs/zeroclaw/issues/10058)** — [Audacity88] — A good-first-issue bug (S2) fixing arrow-key navigation in ZeroCode's file explorer search mode.
- **[#8999 (CLOSED) [Bug]: ZeroCode streamed user turns look like log/API payloads to small local models](https://github.com/zeroclaw-labs/zeroclaw/issues/8999)** — [Audacity88] — A high-risk bug (S2) where streamed user turns were misread as protocol/log data by small local models like Ollama's llama3.2, fixed to present as ordinary conversation.
- **[#9769 (CLOSED) [Task]: make the withheld-capability notice visible when log persistence is disabled](https://github.com/zeroclaw-labs/zeroclaw/issues/9769)** — [AngryPacifist] — Resolved the gap where the `vi_verify` capability notice was delivered only via persisted runtime traces, invisible under `log_persistence = "none"`.

Note: The single closed PR was a CI fix, and these closed issues indicate completed fixes or accepted follow-ups that are being resolved ahead of the next release.

## Community Hot Topics

### Most Active Issues (by comment count)

- **[#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup (24 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)** — [Audacity88] — A governance RFC that has been ratified and is in rollout. It focuses on making work routing easier without adding manual maintainer overhead, indicating a strong push to streamline contributor workflows and automation.
- **[#8692 — [Tracker]: Maintainer decision queue for RFCs and design issues (14 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)** — [Audacity88] — This tracker is the active decision queue for RFCs, design issues, and release-policy questions. Its high activity signals a period of intense architectural deliberation and community input.
- **[#9103 — RFC: separate authoritative memory storage from optional enrichment connectors (14 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/9103)** — [yanchenko] — A high-risk RFC revised by maintainers after a Core REVISE vote. The proposal to decouple the memory backend from a single serialized provider is a major architectural direction with significant community engagement.
- **[#8396 — RFC: Make wire protocol first-class in provider construction and onboarding (12 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/8396)** — [Taswen] — A high-risk architectural RFC aiming to make wire protocols a first-class concern in provider onboarding, reflecting a community desire for a cleaner, more standard provider model.
- **[#9965 — [Task]: harden runtime-written executable test fixtures under the parallel runtime gate (9 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/9965)** — [AngryPacifist] — A test-hardening task addressing flaky or unsafe test fixtures when running under the parallel runtime gate. This is a stability-focused issue with community input on root causes.

### Most Active PRs (by comment count)

- **[#10370 — fix(providers): harden Copilot credential cache](https://github.com/zeroclaw-labs/zeroclaw/pull/10370)** — [Audacity88] — A high-risk security fix (do-not-merge until review) to remove a predictable, username-derived temp file in the Copilot credential cache. This likely improves security for a widely-used provider.
- **[#10372 — feat(dev): add deterministic dependency footprint reports](https://github.com/zeroclaw-labs/zeroclaw/pull/10372)** — [Audacity88] — Adds reproducible Cargo feature/package reports across build profiles, a developer-experience and CI improvement.
- **[#9527 — ci(rust): bump routine toolchains and builders to 1.98.0](https://github.com/zeroclaw-labs/zeroclaw/pull/9527)** — [NiuBlibing] — Routine toolchain bump, keeping the supported source floor at 1.96.0 while moving builds to 1.98.0, addressing CI stability.
- **[#10369 — feat(runtime)!: bound skill HTTP egress](https://github.com/zeroclaw-labs/zeroclaw/pull/10369)** — [Audacity88] — A high-risk, breaking-change PR that enforces strict security on skill-defined HTTP tools: validating URLs one-time only, pinning approved addresses, disabling proxies/redirects, and bounding response text to 1 MiB. This is a significant security-forward feature.
- **[#10368 — test(runtime): stabilize stale local IPC cleanup test](https://github.com/zeroclaw-labs/zeroclaw/pull/10368)** — [Audacity88] — A low-risk test stabilizer fixing a flaky IPC cleanup test, ensuring it waits for the socket to be observably stale.

**Underlying Need Analysis:** The community is deeply focused on security hardening and architectural clarity. The high engagement on RFCs (wire protocol, memory storage separation) indicates a need for stable, well-documented extension points. The activity on work-lane automation (#6808) and the maintainer decision queue (#8692) shows a demand for transparent and efficient project governance, especially as ZeroClaw scales its contributor base.

## Bugs & Stability

The following bugs were reported or updated in the last 24 hours, ranked by severity:

1.  **S0 — Data Loss / Security Risk**
    - **[#9947 — [Bug]: cron tools are not scoped to the owning agent (open)](https://github.com/zeroclaw-labs/zeroclaw/issues/9947)** — [wromansky] — Any agent can read, trigger, modify, or delete another agent's cron jobs by ID on multi-agent installs. **Fix PR:** None open on this yet; high-priority (p1).

2.  **S1 — Workflow Blocked (High)**
    - **[#10357 — [Bug]: Tool execution error path discards the detailed error body (open)](https://github.com/zeroclaw-labs/zeroclaw/issues/10357)** — [joalvaradon] — Agents only receive a bare "HTTP 400" without the detailed error body, blocking debugging. **Fix PR:** [#10364](https://github.com/zeroclaw-labs/zeroclaw/pull/10364) is open to keep detailed tool output when a short error is also set.

3.  **S2 — Degraded Behavior (Medium-High)**
    - **[#9872 — [Bug]: Bounded delegate target resolves filesystem to delegator's workspace instead of own workspace (open)](https://github.com/zeroclaw-labs/zeroclaw/issues/9872)** — [rawlink] — Sandbox boundary is bypassed when a delegated agent's filesystem operations write to the delegator's workspace.
    - **[#10306 — [Task]: gate web/ TypeScript in required CI, and stop bare tsc from printing 75 misleading errors (open)](https://github.com/zeroclaw-labs/zeroclaw/issues/10306)** — [JordanTheJet] — Current build tooling is misleading and CI lacks a required web typecheck gate. **Fix Status:** New issue, no PR yet.
    - **[#10297 — [Feature]: Refresh agent tool registries after structural config changes (open)](https://github.com/zeroclaw-labs/zeroclaw/issues/10297)** — [Audacity88] — Enabling/disabling built-in tools requires a daemon restart, degrading operator experience.

4.  **Stability/Test Fixes (Lower Risk)**
    - **[#10368 test(runtime): stabilize stale local IPC cleanup test](https://github.com/zeroclaw-labs/zeroclaw/pull/10368)** — [Audacity88] — Fixes a flaky test.
    - **[#10042 bug(ci): MSRV system dependency installation can consume job timeout (CLOSED)](https://github.com/zeroclaw-labs/zeroclaw/issues/10042)** — CI timeout issue, now resolved.

**Infrastructure Security PRs:** Over the last 24 hours, several high-risk security fixes are in review: [#10370](https://github.com/zeroclaw-labs/zeroclaw/pull/10370) (Copilot credential cache hardening), [#10369](https://github.com/zeroclaw-labs/zeroclaw/pull/10369) (skill HTTP egress bounding), and [#10367](https://github.com/zeroclaw-labs/zeroclaw/pull/10367) (symlink race prevention in skill installs).

## Feature Requests & Roadmap Signals

Several notable features are being requested or are in active development, indicating strong roadmap signals for the next versions (0.9.0, 1.0):

- **Security & Sandbox Hardening:**
    - [**[#9947] Cron job scoping to owning agent (open, high-priority)**](https://github.com/zeroclaw-labs/zeroclaw/issues/9947) — This is a critical multi-tenant security fix that is a must-have for any production or multi-agent use case, strongly likely to be in the next release.
    - [**[#9872] Bounded delegate filesystem isolation (open, high-priority)**](https://github.com/zeroclaw-labs/zeroclaw/issues/9872) — Directly addresses sandbox boundary correctness.

- **Architecture & Provider Model:**
    - [**[#8396] RFC: Make wire protocol first-class (open, RFC)](https://github.com/zeroclaw-labs/zeroclaw/issues/8396)** — A major RFC that would reshape how providers are constructed.
    - [**[#9103] RFC: Separate authoritative memory storage from optional enrichment connectors (open, RFC)**](https://github.com/zeroclaw-labs/zeroclaw/issues/9103) — A high-risk architectural shift that is under maintainer review.

- **Runtime & Operator Experience:**
    - [**[#9206 CLOSED] Agent cron workspace_dir resolution (closed)**](https://github.com/zeroclaw-labs/zeroclaw/issues/9206) — This S0 data-loss/security risk was fixed, addressing a critical operator pain point.
    - [**[#10297] Refresh agent tool registries after config change (open)**](https://github.com/zeroclaw-labs/zeroclaw/issues/10297) — A key usability feature that eliminates daemon restarts, likely for an upcoming minor/major release.

- **Platform & Integration:**
    - [**[#10306] Gate web/ TypeScript in required CI (open)**](https://github.com/zeroclaw-labs/zeroclaw/issues/10306) — A clear CI stability improvement.
    - [**[#10356] Add AnySearch web search provider (PR open)**](https://github.com/zeroclaw-labs/zeroclaw/pull/10356) — Expanding tool ecosystem, a strong sign of growth.

- **New RFCs (Likely future roadmap):**
    - [**[#10360] RFC: Opt-in household edge mesh with pull workers and signed receipts (open, new)**](https://github.com/zeroclaw-labs/zeroclaw/issues/10360) — A major feature proposal pushing toward distributed local setups.
    - [**[#10346] RFC: Gateway and channels don't share the heartbeat worker's MCP-registry-caching pattern (open, new)**](https://github.com/zeroclaw-labs/zeroclaw/issues/10346) — A performance/architecture improvement to prevent triple-spawning MCP servers on boot.

**Prediction:** The next version (0.9.x) will likely focus heavily on security boundaries (cron scoping, delegate filesystem isolation), the results of the active RFCs (wire protocol, memory storage separation), and will likely include the new "household edge mesh" (if accepted) as an opt-in feature in a later 1.0 beta.

## User Feedback Summary

- **Pain Points (Positive Sign of Maturity):** Users are hitting real production-level issues, which is a good sign for a mature tool. Key complaints include:
    - **Security Boundaries:** The S0 cron scoping issue [#9947](https://github.com/zeroclaw-labs/zeroclaw/issues/9947) is a major data-loss/security risk for multi-agent deployments.
    - **Sandbox Isolation:** Bounded delegate filesystem resolving to the wrong workspace [#9872](https://github.com/zeroclaw-labs/zeroclaw/issues/9872) shows operators are deploying delegation and expecting strict isolation.
    - **Debuggability:** The tool error path discarding detailed error bodies [#10357](https://github.com/zeroclaw-labs/zeroclaw/issues/10357) is directly hindering user ability to debug agent workflows.
- **Use Cases:** The active discussions around "household edge mesh" [#10360](https://github.com/zeroclaw-labs/zeroclaw/issues/10360) and local models [#8999](https://github.com/zeroclaw-labs/zeroclaw/issues/8999) highlight strong use cases for, respectively: multi-device personal on-premise AI infrastructure, and running ZeroClaw with local Ollama models for privacy and cost. The work on the Git channel inclusion in Docker images [#10138](https://github.com/zeroclaw-labs/zeroclaw/issues/10138) and Mattermost approvals [#10358](https://github.com/zeroclaw-labs/zeroclaw/pull/10358) underscores a demand for broader downstream integration.
- **Satisfaction:** The community is deeply engaged and sticking around, evidenced by many returning contributors ([Audacity88](https://github.com/zeroclaw-labs/zeroclaw), [NiuBlibing](https://github.com/zeroclaw-labs/zeroclaw), [JordanTheJet](https://github.com/zeroclaw-labs/zeroclaw)) who are very active in filing and fixing issues. The structured governance RFC process indicates a healthy, organized, and engaged user base that cares about the long-term direction of the project.

## Backlog Watch

The following important items have been open for a while or are at high risk of blocking progress. They need maintainer attention or community input:

- **[#9206 — [Bug]: agent cron runs intermittently resolve workspace_dir to / (CLOSED today)](https://github.com/zeroclaw-labs/zeroclaw/issues/9206)** — Good example of a critical issue being resolved; no longer a watch item.
- Long-running RFCs and Trackers:
    - **[#8692 — [Tracker]: Maintainer decision queue for RFCs and design issues (open since Jul 4)](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)** — The decision queue is actively being used, which is good, but items inside may be waiting on maintainer decisions. Keep an eye on this tracker to ensure RFCs aren't stalled.
    - **[#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup (open since May 20)](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)** — This governance RFC has been ratified but is still in "rollout in progress". The project should ensure the automation is landing as planned.
- High-Risk Security PRs Awaiting Review:
    - **[#10370 — fix(providers): harden Copilot credential cache (PR open, do-not-merge)**](https://github.com/zeroclaw-labs/zeroclaw/pull/10370) — High-risk credential-persistence change; needs independent maintainer review after Windows CI passes.
    - **[#10142 — feat(zerorelay): secure transport with blind relay and native mTLS enrollment (PR open, needs-author-action)**](https://github.com/zeroclaw-labs/zeroclaw/pull/10142) — A large, high-risk security feature (supersedes #9080) that needs significant review and author action.
- Needs-Maintainer-Review Items:
    - **[#9103 — RFC: separate authoritative memory storage from optional enrichment connectors (open, RFC)**](https://github.com/zeroclaw-labs/zeroclaw/issues/9103) — High-risk architectural RFC, flagged `needs-maintainer-review`. This needs a clear decision to unblock the memory-storage roadmap.
    - **[#8396 — RFC: Make wire protocol first-class in provider construction (open, RFC)**](https://github.com/zeroclaw-labs/zeroclaw/issues/8396) — High-risk RFC, flagged `needs-maintainer-review`. Needs explicit acceptance/rejection to guide provider development.

Overall, the project is in very healthy shape with a strong security-first culture, robust community engagement, and clear roadmap signals. The main risks are ensuring the high-volume RFC process doesn't stall and that the S0-grade security bugs in multi-agent scoping are prioritized and resolved promptly.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*