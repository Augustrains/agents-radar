# OpenClaw Ecosystem Digest 2026-07-13

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-13 01:23 UTC

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

# OpenClaw Project Digest — 2026-07-13

---

## 1. Today's Overview

Project activity remains **high**, with 500 issues and 500 pull requests updated in the last 24 hours (290 open/active issues, 265 open PRs). Two **P0 regressions** are currently open (#104721, #101290), both involving critical data integrity and message delivery failures. There are no new releases today. The community continues to engage actively on long-standing enhancement requests (e.g., Linux/Windows desktop apps with 110 comments), while maintainers are working through a substantial backlog of platform stability issues — particularly around memory leaks, SQLite corruption, and message loss in multi-channel environments. The `clawsweeper` triage bot has tagged numerous items as `needs-maintainer-review` and `needs-product-decision`, indicating some bottlenecks in the review pipeline.

---

## 2. Releases

**No new releases today.** The last release appears to be `2026.6.x`, with users reporting issues against version `2026.6.8`, `2026.6.6`, and `2026.6.11`.

---

## 3. Project Progress

**Today's merged/closed PRs (210 total closed/merged):** Key patterns observed in the top 30 PRs:

| PR | Author | Summary |
|----|--------|---------|
| [#97017](https://openclaw/openclaw/pull/97017) | ralf003 | **Large fix** — Zhipu `silentOverflow` misclassification + cron watchdog stage bug; closed with thorough provider-level fix |
| [#84937](https://openclaw/openclaw/pull/84937) | ximanuki | **New feature** — Minimal Discord `/ask` command with bundled Ask plugin |
| [#96237](https://openclaw/openclaw/pull/96237) | aqilaziz | Indonesian i18n for Control UI labels |
| [#96767](https://openclaw/openclaw/pull/96767) | dryftr | **Security** — Upgrade `actions/checkout v6 → v7` across 41 workflow files |
| [#94103](https://openclaw/openclaw/pull/94103) | fsdwen | Tailscale stale serve entry cleanup on gateway restart |
| [#93939](https://openclaw/openclaw/pull/93939) | davedavehong | Tailscale serve reset on gateway reconfiguration |
| [#92762](https://openclaw/openclaw/pull/92762) | 1052326311 | Fix missing `message_sending` hooks when `beforeDeliver` is configured |
| [#93505](https://openclaw/openclaw/pull/93505) | sunlit-deng | Support `baseURL` alias in memory embedding provider config |
| [#93243](https://openclaw/openclaw/pull/93243) | iloveleon19 | Mattermost thread history backfill after gateway restart |
| [#93977](https://openclaw/openclaw/pull/93977) | fsdwen | **Lazy fence** for foreground reply — defer creation to delivery time |
| [#93885](https://openclaw/openclaw/pull/93885) | Coder-Wangyankun | Skip Docker sandbox custom binds colliding with skill mounts |
| [#94914](https://openclaw/openclaw/pull/94914) | aniruddhaadak80 | Filter `models list` by configured providers in replace mode |
| [#103778](https://openclaw/openclaw/pull/103778) | yetval | Fix: gateway plugin reload metadata corruption (closed) |
| [#86217](https://openclaw/openclaw/pull/86217) | jguida941 | Closed iOS background location plist documentation gap |
| [#90404](https://openclaw/openclaw/pull/90404) | VanadisGithub | Fix ACPX TypeError — closed |

**Currently open high-impact PRs needing review:**
- [#105819](https://openclaw/openclaw/pull/105819) — Fix: reclaim phantom reply work (stuck sessions)
- [#103534](https://openclaw/openclaw/pull/103534) — Fix: Gateway plugin-ownership check for `sessions.patch`
- [#101276](https://openclaw/openclaw/pull/101276) — **Feature**: exec-approval denylist (fixes #6615, highly requested)
- [#105726](https://openclaw/openclaw/pull/105726) — Fix: AbortError on cancelled tool execution

---

## 4. Community Hot Topics

| Issue/PR | Comments | 👍 | Topic |
|----------|----------|----|-------|
| [#75](https://openclaw/openclaw/issues/75) | **110** | 81 | **Linux/Windows Clawdbot Apps** — most-discussed feature request, community strongly wants desktop parity with macOS |
| [#99241](https://openclaw/openclaw/issues/99241) | 22 | 2 | Tool output rendered as unreadable image attachments — **P1**, affects agent capability |
| [#91588](https://openclaw/openclaw/issues/91588) | 19 | 1 | **P0 memory leak** — Gateway RSS grows from 350MB → 15.5GB over days, OOMs |
| [#7707](https://openclaw/openclaw/issues/7707) | 16 | 0 | Memory trust tagging by source — security enhancement |
| [#10659](https://openclaw/openclaw/issues/10659) | 13 | 4 | Masked secrets system — strong community resonance (👍 4) |
| [#104721](https://openclaw/openclaw/issues/104721) | 12 | 1 | **P0 regression**: All tool results return `"(see attached image)"` literal |
| [#87744](https://openclaw/openclaw/issues/87744) | 12 | 3 | Codex-backed Telegram turns timeout on `2026.5.27` |
| [#101290](https://openclaw/openclaw/issues/101290) | 8 | 1 | **P0 regression**: CLI preflight corrupts live state DB |
| [#6615](https://openclaw/openclaw/issues/6615) | 7 | 7 | Denylist for exec-approvals — **most upvoted feature** (PR #101276 open) |
| [#10118](https://openclaw/openclaw/issues/10118) | 5 | 4 | Shift+Enter for TUI newlines |

**Analysis**: The Linux/Windows desktop app request (#75) remains the single most engaging conversation, with strong community desire for cross-platform parity. The memory leak (#91588) and the "(see attached image)" placeholder regression (#104721) represent the most urgent operational concerns — both directly impact agent reliability.

---

## 5. Bugs & Stability

### Critical (P0 / Platinum Hermit)

1. **[#104721](https://openclaw/openclaw/issues/104721) — Tool results return literal "(see attached image)" placeholder**  
   *Severity: P0, Regression* — All tool outputs (file reads, exec, etc.) return the literal string `"(see attached image)"` instead of actual data. Filed 2026-07-11, 12 comments. **No fix PR yet.** Related to #99241 (P1).

2. **[#101290](https://openclaw/openclaw/issues/101290) — CLI preflight corrupts live state DB**  
   *Severity: P0, Regression* — On 2026.6.6 macOS, `openclaw.sqlite` corrupted 4 times over 5 days during normal gateway operation. "Database disk image is malformed." Vanilla SQLite does not reproduce. **No fix PR yet.**

3. **[#91588](https://openclaw/openclaw/issues/91588) — Gateway memory leak (350MB → 15.5GB)**  
   *Severity: P0* — RSS grows continuously over 2-3 days, causing OOM kills and `launchd-handoff` restart cycles. Filed 2026-06-09, 19 comments. **No fix PR yet.**

### High Severity (P1 / Diamond Lobster)

4. **[#102020](https://openclaw/openclaw/issues/102020) — Second message fails with "reply session initialization conflicted"**  
   Cross-channel, position-dependent, affects Signal and Discord. Filed 2026-07-08. **No fix PR yet.** Related PR [#103562](https://openclaw/openclaw/pull/103562) open for Discord specifically.

5. **[#91009](https://openclaw/openclaw/issues/91009) — Codex hooks CPU-bound process spawning**  
   `openclaw-hooks` processes consume 100%+ CPU, stall gateway RPC. Has linked PR open.

6. **[#94939](https://openclaw/openclaw/issues/94939) — 6.x state migration leaves empty SQLite (0 bytes)**  
   Breaks proactive sends in MS Teams. Filed 2026-06-19. **No fix PR yet.**

7. **[#99947](https://openclaw/openclaw/issues/99947) — Codex harness mirrored-session-history read fails on failover**  
   Ephemeral/subagent sessions broken; one-shot cleanup retires shared client in-flight. Filed 2026-07-04. **No fix PR yet.**

8. **[#53408](https://openclaw/openclaw/issues/53408) — Write/exec tool parameters silently dropped after 15+ turns**  
   8 comments, filed 2026-03-24 — open for over 3 months.

### Notable Stable Regression

9. **[#87644](https://openclaw/openclaw/issues/87744) — Codex-backed Telegram turns repeatedly time out**  
   Filed 2026-05-28, still open — no fix merged.

**Availability concerns**: Two PRs (#93977, #94103) were closed as duplicates or not-planned, suggesting Tailscale/Tailscale-related fixes are being deferred or consolidated.

---

## 6. Feature Requests & Roadmap Signals

### High-Community-Interest Features

| Request | Issue | 👍 | Status |
|---------|-------|----|--------|
| **Exec-approval denylist** | [#6615](https://openclaw/openclaw/issues/6615) | **7** | Fix PR [#101276](https://openclaw/openclaw/pull/101276) **open** — likely next release |
| **Masked Secrets** (agent can't see API keys) | [#10659](https://openclaw/openclaw/issues/10659) | 4 | Triaged, `needs-maintainer-review` |
| **Shift+Enter for TUI newlines** | [#10118](https://openclaw/openclaw/issues/10118) | 4 | `needs-maintainer-review` |
| **Memory trust tagging by source** | [#7707](https://openclaw/openclaw/issues/7707) | 0 | `needs-product-decision` |
| **Filesystem sandboxing** | [#7722](https://openclaw/openclaw/issues/7722) | 4 | `needs-maintainer-review` |
| **Linux/Windows Clawdbot Apps** | [#75](https://openclaw/openclaw/issues/75) | **81** | Long-term roadmap; `needs-product-decision` |

### Features Likely in Next Version

1. **Exec-approval denylist** (#6615) — PR #101276 is active, well-reviewed, and addresses a clear community pain point.
2. **Gateway plugin-ownership enforcement** — PR #103534 closes a security gap in `sessions.patch`.
3. **AbortError on cancelled tool execution** — PR #105726 fixes a subtle agent-state inconsistency.
4. **Phantom reply work reclamation** — PR #105819 fixes stuck-session bugs across all channels.

### Features Pushed Back / Stalled

- **Linux/Windows desktop apps** (#75) — still `needs-product-decision`, no PR activity.
- **Dynamic model discovery** (#10687) — 9 comments, `needs-product-decision`, foundational but complex.
- **Webhook multi-turn sessions** (#11665) — `needs-maintainer-review`.
- **Private Mode for demos** (#7403) — `needs-product-decision`, niche use case.

---

## 7. User Feedback Summary

### Pain Points (Most Reported)

| Pain Point | Issues | Impact |
|------------|--------|--------|
| Agent can't read tool output (image placeholder) | #104721, #99241 | **Critical** — breaks agent reasoning |
| Repeated OOM crashes from memory leak | #91588 | **Critical** — service unavailable after 2-3 days |
| Messages silently dropped / session conflicts | #102020, #102400, #87744 | **High** — message loss, user frustration |
| SQLite corruption under normal use | #101290, #71689 | **Critical** — data loss, gateway restart cycles |
| Tool parameters silently dropped in long conversations | #53408 | **High** — undermines trust in long sessions |
| No Linux/Windows desktop apps | #75 | **High** — excludes Linux/Windows users from full feature set |
| API key security (agent can read secrets) | #10659 | **Medium** — security concern for production use |
| No exec-approval denylist | #6615 | **Medium** — forces allow-everything or constant prompting |

### Positive Signals

- Active community is submitting well-structured feature requests with clear use cases (e.g., #7707 memory trust, #7722 filesystem sandboxing).
- Contributors are actively submitting fixes — 210 PRs closed/merged in the last 24 hours, including meaningful architectural changes (refactoring pairing state to SQLite, consolidating retry scheduling).
- Indonesian localization contribution (#96237) shows growing international community.

### Notable Dissatisfaction Signals

- **P0 regressions** (#104721, #101290) suggest insufficient regression testing in the release pipeline.
- The "(see attached image)" placeholder bug (#104721) is a **UX blocker** that could permanently damage user trust — affected users cannot even read file contents.
- Multiple heartbeat-related regressions (#65161) were closed as stale without resolution, suggesting known issues are being aged out rather than fixed.

---

## 8. Backlog Watch

### Issues Stale Without Resolution (>3 months open, critical-severity)

| Issue | Age | Topic | Status |
|-------|-----|-------|--------|
| [#53408](https://openclaw/openclaw/issues/53408) | ~112 days | Tool parameters silently dropped after 15+ turns | `needs-live-repro` |
| [#39476](https://openclaw/openclaw/issues/39476) | ~127 days | A2A duplicate messages on `sessions_send` back-call | `needs-live-repro`, linked PR open |
| [#11665](https://openclaw/openclaw/issues/11665) | ~155 days | Webhook multi-turn session broken | `needs-maintainer-review` |
| [#7707](https://openclaw/openclaw/issues/7707) | ~161 days | Memory trust tagging | `needs-product-decision` |

### PRs Stuck in Review (Waiting on Maintainer)

| PR | Age | Topic | Risk |
|----|-----|-------|------|
| [#105819](https://openclaw/openclaw/pull/105819) | <1 day | Phantom reply work reclamation | **High** — fixes stuck sessions |
| [#103534](https://openclaw/openclaw/pull/103534) | 3 days | Gateway plugin-ownership check | **High** — security boundary fix |
| [#104027](https://openclaw/openclaw/pull/104027) | 2 days | Dependencies update (14 actions) | **Medium** — security updates |
| [#101276](https://openclaw/openclaw/pull/101276) | 6 days | Exec-approval denylist | **Medium** — requested by community |

### Items Needing Product Decision (Blocks Progress)

| Issue | Topic |
|-------|-------|
| [#75](https://openclaw/openclaw/issues/75) | Linux/Windows desktop apps — 110 comments, no decision |
| [#10687](https://openclaw/openclaw/issues/10687) | Dynamic model discovery — foundation for many other features |
| [#7722](https://openclaw/openclaw/issues/7722) | Filesystem sandboxing |
| [#7707](https://openclaw/openclaw/issues/7707) | Memory trust tagging |
| [#7403](https://openclaw/openclaw/issues/7403) | Private Mode for demos |

**Recommendation**: The two P0 regressions (#104721, #101290) should be escalated to immediate hotfix priority. The `needs-product-decision` backlog (especially #75 and #10687) are blocking significant community contributions and should be triaged by maintainers in the next 30 days.

---

*Generated from GitHub data for OpenClaw (openclaw/openclaw) — snapshot as of 2026-07-13T00:00:00Z*

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report.

---

### Cross-Project Ecosystem Report: Personal AI Assistant Landscape
**Date:** 2026-07-13

#### 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is currently defined by a tension between aggressive feature expansion and regressions in core reliability. Projects like OpenClaw, IronClaw, and ZeroClaw are in hyper-growth phases, shipping complex runtime overhauls and governance features (SOPs, memory subsystems, MCP stores) at the cost of regressions in message delivery, SQLite integrity, and token budget management. In contrast, smaller or specialized projects (NanoBot, PicoClaw, LobsterAI) are showing lower velocity but dealing with critical, unaddressed configuration fragility (e.g., Discord message drops, Android service crashes, multi-agent data overwrites). A dominant industry concern is **message integrity**: multiple projects face user-visible failures where tools return placeholders, session states are corrupted, or messages are silently dropped. The community is acutely sensitive to token waste, operational noise (false-positive logs), and the lack of robust multi-platform desktop support.

#### 2. Activity Comparison

| Project | Issues (Open/Active) | PRs (Open) | Release Today | Health Score (Subjective) |
|---|---|---|---|---|
| **OpenClaw** | 290 | 265 | None | **Strained** – High activity, but 2 P0 regressions |
| **NanoBot** | 4 | 6 | None | **Stable, Low** – Low volume, needs bug triage |
| **Hermes Agent** | 50 updated (34 closed) | 50 updated (0 merged) | None | **Mature** – Heavy grooming, but PR merge bottleneck |
| **PicoClaw** | 3 | 2 | None | **Stable** – Low volume, one critical reconnection bug |
| **NanoClaw** | 13 updated (3 open) | 13 updated (2 closed) | None | **Healthy** – Rapid fixes for regressions |
| **NullClaw** | 0 | 0 | None | **Idle / Clean** – Single batch merge, zero backlog |
| **IronClaw** | 50 updated (unclear) | 50 updated (25 merged) | None | **High Velocity** – Intense dev, red CI is main risk |
| **LobsterAI** | 1 | 2 updated (1 closed) | None | **Stagnant** – Critical bug unaddressed for 6 days |
| **CoPaw** | 21 updated | 10 updated (3 merged) | None | **Challenged** – Post-2.0.0 stability crisis |
| **ZeroClaw** | 33 (32 active) | 50 (47 open) | None | **Hyper-Active** – Major sprints, P1 bugs in play |
| **TinyClaw / Moltis / ZeptoClaw** | N/A | N/A | None | **Dormant** – No activity |

#### 3. OpenClaw's Position

- **Advantages vs. Peers:**
    - **Largest Community Scale:** With 500 issues and 265 open PRs, OpenClaw has the most active and diverse contributor base. It has the highest volume of external contributions, including multiple first-time contributor PRs.
    - **Broadest Platform Coverage:** It explicitly targets Linux/Windows desktop parity (the most commented request at 110 comments), addressing a critical demand that competitors like Hermes Agent and IronClaw have not fully met.
    - **Security Conscious:** OpenClaw has active PRs for exec-approval denylists (#101276) and masked secrets (#10659), signaling a proactive stance on enterprise-grade security.

- **Technical Approach Differences:**
    - OpenClaw uses a `clawsweeper` triage bot to manage its massive backlog, a strategy unique to its scale. In contrast, ZeroClaw relies on human-maintained trackers, and NullClaw operates with a zero-backlog model.
    - Its architecture appears to emphasize a plugin/gateway model (Tailscale, Discord `/ask` command), making it modular but also prone to regressions when gateway logic changes.

- **Community Size Comparison:**
    - OpenClaw's community is orders of magnitude larger than projects like LobsterAI (1 active issue) or PicoClaw (3 issues). It rivals IronClaw in activity but has a much higher volume of *open* work, suggesting its triage pipeline is a bottleneck.
    - Its user base is vocal about reliability: the "(see attached image)" placeholder bug (#104721) and the memory leak (#91588) are highly visible and damaging to trust.

#### 4. Shared Technical Focus Areas

A clear set of cross-project requirements is emerging, indicating the industry's baseline expectations for AI agents:

1.  **Message & Session Integrity:** This is the top universal pain point.
    - **OpenClaw:** Tool results returning placeholders (#104721), session conflicts.
    - **CoPaw:** `tool_call/tool_result` pairing broken by context compression (#5986).
    - **ZeroClaw:** Unbounded RSS growth from MCP cloning (#8642).
    - **NanoClaw:** Duplicate replies after re-wrap nudge (#3026).
    - **Hermes Agent:** Cross-tab message leaking in the desktop client (#59305).

2.  **Stable Multi-Platform Delivery:**
    - **Matrix reliability** is a shared failure mode: PicoClaw has a critical reconnection bug (#3203).
    - **Slack/Telegram/Discord** are common targets, with user frustration over inconsistent delivery (OpenClaw, Hermes Agent).
    - **Desktop parity** (Linux/Windows) is a top feature request across OpenClaw (#75) and Hermes Agent.

3.  **Token & Memory Efficiency:**
    - **Context Budget Overflow:** ZeroClaw's default 32K budget is exceeded by the system prompt alone (#5808).
    - **Prompt Caching:** NanoBot users report a 60-second delay per turn because exact prefixes aren't preserved (#4867, closed).
    - **Skill/SOP Optimization:** IronClaw's skill-listing optimization (#5977) and ZeroClaw's memory overhaul are direct responses.

4.  **Security Governance (Exec-Approval):**
    - OpenClaw has a popular request for an exec-approval denylist (#6615).
    - CoPaw users are frustrated by forced approval prompts on every shell execution on landlock-devoid kernels (#5984).
    - ZeroClaw is shipping HITL approval in its SOP milestone.

5.  **Operational Observability:**
    - **Noisy false positives**: NanoClaw's rate-limit mislogging (#3016) and LobsterAI's silent data overwrite (#2293) erode user trust in monitoring.
    - **CI Reliability**: IronClaw (70% red pushes, #6014) and ZeroClaw (OOM crashes) show that development infrastructure is a major blocker.

#### 5. Differentiation Analysis

| Project | Feature Focus | Target User | Technical Architecture |
|---|---|---|---|
| **OpenClaw** | Broadest platform support, | General power users, | Plugin/gateway model, |
| | security governance, | TUI/CLI advocates, | modular, community-driven |
| | desktop parity | multi-platform users | |
| **Hermes Agent** | Platform stability, | Enterprise users needing | Sweeper-driven, focus on |
| | bug triage, | multi-platform gateways | clearing backlogs, |
| | multi-platform gateway | (WeChat, QQ, Telegram) | robust CI/grooming |
| **IronClaw** | "Reborn" runtime overhaul, | Developers wanting | High-velocity feature train |
| | MCP integration, | SWE-bench competitive | (extension runtime, MCP), |
| | CI hardening | agents, Rust backend | aggressive CI fixes |
| **ZeroClaw** | SOP pipeline, memory | Advanced operators, | Major memory subsystem |
| | overhaul, WASM plugins, | automation workflow | rewrite, zero-code UX |
| | goal-mode | creators | |
| **CoPaw** | AgentScope ecosystem, | Users migrating to | Post-2.0.0 stability crisis, |
| | v2 migration, | AgentScope 2.0.0 | context management issues |
| | system prompt efficiency | | |
| **NanoBot** | Dream memory system, | Local model users, | Small feature set, |
| | WebUI, Ollama integration | resource-constrained | strong focus on Ollama |
| | | users | |
| **NullClaw** | Configuration hardening, | DevOps/operators | Single-batch maintainer |
| | operational correctness | running stable deployments | push, zero backlog |

#### 6. Community Momentum & Maturity

- **Tier 1: Hyper-Active / High Velocity**
    - **OpenClaw, IronClaw, ZeroClaw**: These three projects are iterating rapidly, shipping major architectural changes weekly. They are shaping the ecosystem's technical direction (governance, memory, runtime efficiency). Their biggest risk is that velocity outpaces stability, leading to the P0 regressions seen in OpenClaw and the red CI in IronClaw.

- **Tier 2: Maintenance & Stabilization**
    - **Hermes Agent, CoPaw, NanoClaw**: These projects are in a "fix the bugs" phase. Hermes is aggressively grooming a deep backlog; CoPaw is fighting post-major-release regressions; NanoClaw is rapidly closing regressions from recent nudge changes. They represent the more mature, reliable end of the spectrum.

- **Tier 3: Low Activity / Stalled**
    - **LobsterAI, NanoBot, PicoClaw, NullClaw**: LobsterAI and PicoClaw have unaddressed critical bugs, suggesting maintainer bandwidth issues. NanoBot has very low issue volume. NullClaw's zero-backlog state is either a sign of extreme efficiency or a pause in development.

- **Tier 4: Dormant**
    - **TinyClaw, Moltis, ZeptoClaw**: No observable activity, suggesting these may be experimental or low-priority projects.

#### 7. Trend Signals

1.  **Context Management is the #1 Reliability Frontier:** The most critical cross-project failure is the inability to preserve `tool_call`/`tool_result` pairings and session state during context truncation (CoPaw, OpenClaw, ZeroClaw). This is a fundamental architectural challenge that will define the next generation of agent frameworks.

2.  **From CLI/TUI to Services:** Users are demanding 24/7 operation. Failures like Matrix sync loops (PicoClaw), memory leaks (OpenClaw), and silent Android service crashes (PicoClaw) show that the ecosystem is maturing from a developer tool to an always-on service. Projects that neglect production reliability will lose trust.

3.  **Security Governance is a Core Feature, Not a Niche:** The demand for exec-approval denylists, masked secrets, and HITL approval is widespread. This signals a shift from "zero trust for agents" to "managed trust with user control." OpenClaw's denylist and ZeroClaw's SOP approval are leading this trend.

4.  **The "SWE-bench Gap" Drives Hardening:** IronClaw's explicit focus on closing the 30% vs 65% SWE-bench gap and the Reborn runtime highlights that agent developers are directly competing on coding benchmarks. This is driving investment in tool schema optimization, context compression, and error resilience.

5.  **Community Fatigue with False Positives:** Users across OpenClaw (monitoring noise), NanoClaw (rate-limit mislogging), and CoPaw (false approval prompts) are frustrated by systems that produce more noise than signal. The next wave of features will likely include user-configurable thresholds and audit trails to filter out benign events.

6.  **ARM and Container Deployments are Becoming Mainstream:** Requests for armhf Docker support (PicoClaw) and issues with landlock-devoid kernels on Raspberry Pi (CoPaw) confirm that agents are being deployed on edge hardware and containerized environments. This is a growth area for platform support.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-13

## Today's Overview
The NanoBot project shows moderate activity today with 4 issues and 6 pull requests updated in the last 24 hours. One issue was closed, and two PRs were merged/closed, indicating steady progress on bug fixes and feature work. Two critical `priority: p1` PRs are in the pipeline — one fixing a heartbeat execution regression introduced in v0.2.1 and another tightening remote WebUI access security — suggesting the team is actively addressing regressions from recent refactors. However, three open bugs reported yesterday remain unaddressed, and the project has no new releases today.

## Releases
No new releases were published today. The most recent release remains the current version available on the repository's releases page.

## Project Progress
Two PRs were merged/closed today:
- **[PR #4898 — merge](https://github.com/HKUDS/nanobot/pull/4898)** — A simple merge PR (author: Theembers), likely integrating branches or minor changes.
- **[PR #4892 — fix(webui): allow remote workspace access reduction](https://github.com/HKUDS/nanobot/pull/4892)** (closed, `priority: p1`) — A security-focused fix by Re-bin that allows remote WebUI sessions to reduce their access scope from Full Access to Default Permission without altering the workspace. This change limits project changes and access escalation to localhost and native clients, addressing a potential security vulnerability.

## Community Hot Topics
The most commented issue this period is:
- **[Issue #4867 [CLOSED] — Preserve exact prompt prefix to enable caching in Ollama and others](https://github.com/HKUDS/nanobot/issues/4867)** — Author: The-Markitecht, 4 comments. The reporter describes a severe usability problem: every turn with Ollama incurs an *extra 60 seconds* delay because Nanobot does not preserve exact prompt prefixes to enable model caching. The user states this makes the system *"totally unusable with Ollama and 32 GB of VRAM."* This was a follow-up to issue #2463 and has now been closed, suggesting a solution was either implemented or determined infeasible.

No issues or PRs in the current batch have reactions (👍 counts are all zero).

## Bugs & Stability
Three open bugs were reported yesterday, all currently without fix PRs:
1. **[Issue #4897 [OPEN] — Discord bot integration failure](https://github.com/HKUDS/nanobot/issues/4897)** — *Severity: Medium.* The bot comes online in Discord but receives no messages. Setup steps confirm the gateway runs and the bot appears online, yet message delivery fails. No comments or assignee yet.
2. **[Issue #4894 [OPEN] — `prune_dream_sessions()` fails to prune base64-encoded Dream session files](https://github.com/HKUDS/nanobot/issues/4894)** — *Severity: Medium.* After commit `cf2f5896`, session filenames switched to base64 encoding, but the pruning function still uses `dream_*.jsonl` glob patterns. This means legacy files may be pruned while new ones are not. A simple glob mismatch maintenance issue.
3. **[Issue #4893 [OPEN] — `/dream-log` and `/dream-restore` show non-Dream commits](https://github.com/HKUDS/nanobot/issues/4893)** — *Severity: Low-Medium.* The Dream timeline commands call `git.log()` without filtering for Dream-specific commits, causing unrelated workspace commits (backups, manual edits) to appear in output. This is confusing but not data-corrupting.

**Bug Fix PRs in progress (not yet merged):**
- **[PR #4896 [OPEN] — fix heartbeat execution regression](https://github.com/HKUDS/nanobot/pull/4896)** (`priority: p1`) — Addresses a regression from v0.2.1 where the heartbeat prompt was not updated after refactoring from a service to a cron job. Currently agents only listen/report instead of executing tasks.
- **[PR #4895 [OPEN] — fix transcription API key env placeholders](https://github.com/HKUDS/nanobot/pull/4895)** (`priority: p2`) — Resolves `${ENV_VAR}` placeholder resolution for transcription providers.

## Feature Requests & Roadmap Signals
The only enhancement-closed issue today, **[Issue #4867](https://github.com/HKUDS/nanobot/issues/4867)**, requests preserving exact prompt prefixes to enable caching with Ollama and other local model providers. Given the severity of the 60-second delay per turn, this is likely to be prioritized in the next release if not already addressed. The fact that it is now closed suggests a patch or guidance exists.

Two other feature-oriented PRs remain open but inactive:
- **[PR #4855 [OPEN] — feat(webui): add guided setup flows](https://github.com/HKUDS/nanobot/pull/4855)** — Adds channel setup wizards with validation, QR handoff, and Feishu assistant management. This is a substantial feature that may land in a future minor release.
- **[PR #4145 [OPEN] — fix: resolve #3958 — Weather Skill](https://github.com/HKUDS/nanobot/pull/4145)** — A long-open PR (since June 1) adding a weather skill example with tests. This has been in review for over six weeks.

## User Feedback Summary
Real user pain points visible today include:
- **Ollama performance crisis**: One user explicitly states NanoBot is *"totally unusable with Ollama and 32 GB of VRAM"* due to a 60-second per-turn overhead. This is the strongest negative feedback in the current data.
- **Discord integration failure**: User AustinCGomez successfully sets up the Discord bot (it appears online) but receives zero messages, indicating a non-obvious configuration or runtime bug.
- **Dream system confusion**: User groudas reports two related bugs (base64 filename mismatch, unfiltered commit logs) that degrade the user experience for the Dream memory system.

## Backlog Watch
- **[PR #4145 — Weather Skill fix](https://github.com/HKUDS/nanobot/pull/4145)** (created June 1, last updated July 12) — A 6-week-old PR awaiting maintainer review. No comments from maintainers. Risk of becoming stale.
- **[Issue #4867 — Ollama caching](https://github.com/HKUDS/nanobot/issues/4867)** has been closed, but the underlying problem's resolution status is unclear — users may need confirmation that a fix is in place.
- The three open bugs from July 12 (Issues #4897, #4894, #4893) have no assignees and no maintainer responses, suggesting a backlog gap in bug triage.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for **2026-07-13**.

---

## Hermes Agent Project Digest — 2026-07-13

### 1. Today's Overview
Project activity is **high**, driven entirely by issue triage and a deep backlog of open pull requests. 50 issues were updated in the last 24 hours, with a remarkable **34 closed** — indicating a heavy maintainer focus on clearing swept bugs and features. However, **no new releases** were published, and **zero PRs were merged or closed**, despite 50 PRs being updated. The delta between high issue closure rates and zero PR merges suggests that while sweeper/bot-driven issue grooming is efficient, manual merge review may be a bottleneck. The project remains in a **maintenance-heavy phase** with a focus on platform stability and bug fixes for gateway components.

### 2. Releases
**None.** No new versions of Hermes Agent were published today.

### 3. Project Progress
No pull requests were merged or closed today. However, the **34 closed issues** indicate that a significant volume of fix code has reached `main`, likely via sweeper automation. Key progress areas from closed issues include:
- **Cron jobs**: The "Cron doesn't work!" bug (#21867) was resolved via sweeper (`implemented-on-main`).
- **Gateway stability**: Several gateway bugs were closed, including fixes for port conflicts on systemd restarts (#21915), multi-platform WebSocket cascading disconnections (#21026), and a missed `/sessions` command handler (#21734).
- **Platform compatibility**: Fixes landed for QQ bot import failures outside the Hermes venv (#22153), WhatsApp bridge disablement in Docker (#21710), and MemOS memory provider process leaks (#20939).
- **CLI/TUI fixes**: The `hermes dashboard --tui` session-ended bug (#21801), the `@` autocomplete freeze in tmux (#21623), and the Python 3.9 crash from `X | None` type hints (#21798) were all resolved.

### 4. Community Hot Topics
The most active discussions revolve around **security, session reliability, and multi-platform stability**.

- **[Issue #12816 (PR)] feat(compressor): budget-capped summarizer input with progressive truncation** — This open PR has the highest blast radius of any item in the backlog. It addresses a core token waste issue where `/compress` costs excessive tokens. It is a **high-value, high-risk** change touching session state and caching.
- **[Issue #52951] Bug: cua-driver UIAccess helper process dies after window focus change** — A critical Windows desktop bug. User **2ndNatureAI** reports that Alt+Tabbing kills the computer-use driver entirely, blocking all automation for a session. This has high visibility (+0 reactions, but severe blocking impact).
- **[Issue #59305] Cross-tab message leaking in Desktop client** — User **ufq-yyy** reports that messages from one chat tab appear in another. This is a **high-severity UX bug** that corrupts conversation context and erodes trust in the desktop app.
- **[Issue #63469] Orchestrator trusts stale memory over canonical policy** — User **sene1337** describes a complex, long-running state corruption issue where the orchestrator's memory diverges from the profile config, causing multi-profile model routing to break. This signals a need for more robust state reconciliation logic.

### 5. Bugs & Stability
**High Severity:**
- **Windows Desktop: cua-driver crash on Alt+Tab** (#52951). Blocks all computer-use for a session. No fix PR linked yet; status is `OPEN` with `P2` priority.
- **Desktop Chat Tab Message Leak** (#59305). Cross-tab content mixing. Status `OPEN`, P2, `needs-repro`.
- **Orchestrator state corruption** (#63469). Stale memory vs. canonical config. Status `OPEN`, P3 — but with long-running implications for multi-profile users.

**Medium Severity (Fix PR Exists):**
- **Concurrent OAuth flows stomp on each other** (PR #22172). A shared module-level global (`_oauth_port`) causes two gateway sessions to conflict. Fix written by `amathxbt` but **not yet merged**.
- **MCP stderr silently discarded** (PR #22168). Log fallback to `/dev/null` is hidden at DEBUG level. Fix written by `amathxbt`, **not merged**.
- **URL-encoded path traversal bypass** (PR #22173). `validate_within_dir` misses encoded components. Security fix written, **not merged**.

**Low Severity / Resolved:**
- The cron job non-execution bug (#21867) and the `/sessions` command handler absence (#21734) were both closed via sweeper today.

### 6. Feature Requests & Roadmap Signals
Several user-requested features signal where Hermes is heading:

- **Topic-Aware Subagent Routing** (#21827, *closed*): The proposal to route tasks (coding, finance, chat) to the right model was closed as `not-planned` via sweeper. However, its existence suggests strong user demand for model specialization.
- **Claude Code / Team authentication as a Hermes provider** (#32392, *open*): User **vimox-shah-genea** requests support for `claude login` credentials. This is a high-value request for enterprise users who already have Anthropic accounts. **Prediction**: Likely to be implemented in the next major release if Anthropic standardizes the auth flow.
- **Per-channel personality and model routing** (#21637, *closed*): This feature, extending `channel_prompts`, was implemented via sweeper. It will likely appear in the next changelog.
- **Desktop Tirith approval dialog** (#38164 & #38173, *closed*): Users want a GUI popup for security approval in the desktop client. Closed today; expect it in a near-future release.

### 7. User Feedback Summary
- **Satisfaction**: Users appreciate the **breadth of platform support** (Discord, Slack, Telegram, WeChat, QQ). The fix for `hermes dashboard --tui` (#21801) was well-received (+3 👍).
- **Pain Points**:
    - **Timeout configuration**: User **juniperbevensee** highlights that hardcoded platform timeouts break local model workflows (#21525). This is a systemic issue for Ollama/vLLM users.
    - **Docker complexity**: Multiple issues (e.g., #21915 on systemd loops, #21710 on WhatsApp disablement) show that Docker + multi-platform gateway setups are fragile and require more robust health checks.
    - **Token cost management**: The demand for budget-capped summarizers (PR #12816) and smarter model routing (#21827) shows that users are **acutely sensitive to LLM token costs**.

### 8. Backlog Watch
These items require maintainer attention due to age, importance, or risk:

- **[PR #12816] Budget-capped summarizer (P2)** — Created 2026-04-20. 84 days open. **Highest blast radius** and highest value-add for heavy users. Needs a core maintainer review.
- **[PR #22200] fix(acp): pass fallback_providers to AIAgent (P2, blast-massive)** — Created 2026-05-09. Affects all ACP clients (VS Code, JetBrains). If merged, it fixes a silent failure path where fallback models never activate.
- **[Issue #21525] Hardcoded platform timeouts (P2)** — Created 2026-05-07. 3 👍 reactions. Closed as `not-planned`, but the underlying user need (configurable timeouts for local models) persists and may come back as a higher-priority feature request.
- **[PR #22186] fix: preserve Grubtech local gateway patches (P3, blast-massive)** — Created 2026-05-09. Despite its `blast-massive` label, this PR has seen no maintainer activity. It patches critical gateway logic (WhatsApp bridge, MIME maps) and may be blocking a specific deployment setup.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-13

## Today's Overview

PicoClaw shows steady but moderate activity today, with 5 issues updated and 2 PRs touched in the last 24 hours. Three issues remain open/active, while two were closed. No new releases were published. The project is addressing a mix of critical Matrix connectivity bugs, provider parsing edge cases, and platform-specific deployment requests, indicating active maintenance with room for improvement in release cadence.

## Releases

No new releases were published today. The most recent tagged version remains v0.2.9 (as referenced in Issue #3203).

## Project Progress

One pull request was merged/closed today:

- **#3190** (closed) — [fix(i18n): sync missing locale keys from en.json to bn-in and cs translations](https://github.com/sipeed/picoclaw/pull/3190) – Added missing translation keys `chat.dropImagesActive`, `chat.disableCodeWrap`, `chat.enableCodeWrap` for Bengali (India) and Czech locales. This is a minor localization improvement with no feature impact.

One pull request remains open:

- **#3251** (open) — [fix(providers): capture the prompt cache token usage in Anthropic providers](https://github.com/sipeed/picoclaw/pull/3251) – Adds cache token metrics tracking (`cache_creation_input_tokens`, `cache_read_input_tokens`) for both the Anthropic SDK and Anthropic Messages API providers. This is a monitoring/observability improvement that does not change behavior.

**Key observation:** No functional features or bug fix PRs were merged today. The only merge was a localization fix.

## Community Hot Topics

The most active issues by recent activity and reactions:

1. **#3203** (open, 👍1, 2 comments) — [Matrix sync loop has no reconnection logic — silent death after network/server disruption](https://github.com/sipeed/picoclaw/issues/3203)  
   *Reporter: weissfl* – Describes a critical reliability failure where the Matrix `/sync` long-polling loop dies silently after any network disruption or homeserver restart. Because the main process doesn't crash, systemd's `Restart=on-failure` never triggers. This is a significant operational risk for always-on deployments.

2. **#3182** (open, 3 comments) — [BUG: Android version — can't launch service](https://github.com/sipeed/picoclaw/issues/3182)  
   *Reporter: Monessem* – User reports inability to run PicoClaw as a service on Android despite granting full permissions. Includes a screenshot showing settings path cannot be changed. Has been open since June 26 with no maintainer response.

3. **#3252** (open, 0 comments) — [splitKnownProviderModel strips provider prefix when model ID contains known provider alias](https://github.com/sipeed/picoclaw/issues/3252)  
   *Reporter: v2up-32mb* – A parsing logic bug where model IDs containing substrings that match provider aliases (e.g., `"openai/gpt-4"` if "openai" is a provider prefix) have their prefix incorrectly stripped. This causes configuration failures for valid models.

**Underlying needs:** Users urgently want **operational reliability** (Matrix reconnection), **mobile platform support**, and **correct provider configuration parsing**. The Matrix issue (#3203) affects anyone using Matrix as a communication channel in production.

## Bugs & Stability

| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| 🔴 Critical | [#3203](https://github.com/sipeed/picoclaw/issues/3203) | Matrix sync loop dies silently after network/server disruption — no reconnection logic, process-health-unaware | No |
| 🟠 High | [#3252](https://github.com/sipeed/picoclaw/issues/3252) | `splitKnownProviderModel` incorrectly strips provider prefix when model ID contains a known provider alias | No |
| 🟡 Medium | [#3182](https://github.com/sipeed/picoclaw/issues/3182) | Android service won't launch — "Can't change path from settings" with full permissions granted | No |
| 🟢 Low | [#3194](https://github.com/sipeed/picoclaw/issues/3194) (closed) | "Received encrypted message but crypto is not enabled" — stale issue, closed today | N/A |

**No fix PRs exist for the critical or high-severity bugs.** The Matrix reconnection issue (#3203) is particularly concerning as it affects system reliability without triggering auto-restart mechanisms.

## Feature Requests & Roadmap Signals

One feature request was closed today:

- **#3250** (closed) — [添加对于armhf设备的docker compose支持 (Add Docker Compose support for armhf devices)](https://github.com/sipeed/picoclaw/issues/3250)  
  *Reporter: zhang090210* – Requested Docker Compose support for ARMv7 devices like the OneCloud/玩客云 and Raspberry Pi Zero. The user explicitly offered a proposed solution (modify Dockerfile/docker-compose.yaml for multi-arch). This was closed but **without a merge or comment from maintainers visible in the data**, suggesting either a quick close or a separate resolution path.

**Prediction:** Given the PR #3251 (Anthropic cache metrics) is open and small, it may land in the next patch release. The armhf Docker support (#3250) is a low-effort, high-value addition for the ARM community and could appear in v0.2.10 if maintainers pick it up.

## User Feedback Summary

**Pain points:**
- **Reliability failures** (#3203): Users running PicoClaw as a service experience silent Matrix channel death after network hiccups, requiring manual restart.
- **Mobile platform gaps** (#3182): Android users cannot run PicoClaw as a service, limiting mobile use cases.
- **Configuration parsing surprises** (#3252): Provider model IDs with embedded aliases cause silent misconfiguration.
- **Encryption confusion** (#3194, closed): Users receiving encrypted Matrix messages without crypto enabled—likely a configuration experience gap.

**Satisfaction indicators:**
- Low 👍 counts across all issues, which may indicate a small but active user base.
- The i18n PR (#3190) shows community contributors care about localization quality.

**Positive voice:** The Anthropic cache metrics PR (#3251) was requested by operators who want to verify prompt caching is working, indicating advanced users are monitoring performance.

## Backlog Watch

**Issues needing maintainer attention:**

1. [#3182](https://github.com/sipeed/picoclaw/issues/3182) – **Android service bug, open since 2026-06-26 (17 days)**. No maintainer comments despite 3 user comments. This is the oldest open issue in today's batch and affects a specific but growing platform.

2. [#3203](https://github.com/sipeed/picoclaw/issues/3203) – **Matrix reconnection failure, open since 2026-07-02 (11 days)**. One reaction, clear reproduction steps, and a significant reliability impact. The lack of a fix PR is a risk.

3. [#3252](https://github.com/sipeed/picoclaw/issues/3252) – **Provider parsing bug, filed today (2026-07-12)**. Fresh issue, zero comments — needs initial triage.

**Notable observation:** None of the open bugs have any `[stale]` label despite #3182 and #3203 being open for over a week. The project may benefit from a triage process or response SLA for user-reported issues.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-13

## Today's Overview
NanoClaw shows **elevated development activity** with 13 PRs updated in the last 24 hours, signaling a focused push on stability and user-facing governance. Three open issues were updated, including a critical silent failure (#3023) that was already closed by a fix PR (#3024). The project is actively addressing two systemic regressions introduced by recent nudging logic (#3016, #3026) and shipping approved maintainer features for operator controls and audit logging. No new releases were cut today.

## Releases
_No new releases published in the last 24 hours._

## Project Progress
Two PRs were merged or closed today:

- **#3024** (closed) — **fix(container): raise the agent SDK's 32000 output-token cap to the model's real ceiling**  
  Author: javexed  
  A critical fix for Issue #3023: Claude agents were silently capped at 32K output tokens because the `CLAUDE_CODE_MAX_OUTPUT_TOKENS` env var was never set. The fix raises the cap to match the underlying model's true limit.  
  [GitHub PR #3024](https://github.com/nanocoai/nanoclaw/pull/3024)

- **#2952** (closed) — **Skill: add OpenCode stack**  
  Author: javexed  
  An operational container skill that adds support for the OpenCode development stack.  
  [GitHub PR #2952](https://github.com/nanocoai/nanoclaw/pull/2952)

Additionally, high-impact open PRs receiving commits today include:
- **#3020** — Rescue undelivered unwrapped replies after re-wrap nudge (fixes message drops)  
- **#3025** — Alternative (open) PR raising the output-token cap to model ceiling  
- **#3027** — Relocate TMPDIR to prevent container poisoning from root-owned dirs  
- **#3028** — Avoid duplicate replies after `send_message`

## Community Hot Topics
**Most Active Issue:**
- **#3016 — Every rate_limit_event logged as a quota error** (1 comment, 0 👍)  
  Author: glifocat  
  A regression from PR #2965 causing all rate-limit events to be mislogged as quota errors, even on successful turns. Users report 82 false-positive logs in a week. This is a noisy but non-functional bug affecting operational monitoring.  
  [GitHub Issue #3016](https://github.com/nanocoai/nanoclaw/issues/3016)

**Notable PRs with Discussion:**
- **#3020** — Rescue undelivered unwrapped replies (fixes silent drops) — directly addresses persistent user pain around lost messages #2369 and #2393.  
- **#2986** — Guard seam: one decision function for every privileged action — a major architectural consolidation for security, still open after 4 days.

## Bugs & Stability
Bugs ranked by severity:

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **Critical** | #3023 | Claude agents silently capped at 32K output tokens; long turns die mid-generation | Fixed in #3024, alternative fix in #3025 (open) |
| **High** | #3026 | Re-wrap nudge duplicates replies after `send_message`; agent messages silently doubled | Fix in #3028 (open) |
| **High** | #3027 | Container fails to start (EISDIR error) when `/tmp/onecli-proxy-ca.pem` is a directory; agents go silent | Fix in #3027 (open) |
| **Medium** | #3016 | Rate-limit events mislogged as quota errors; 82 false-positive logs per week for one install | No fix PR yet |

- **#3027** is a particularly dangerous intermittent bug: when `/tmp/onecli-proxy-ca.pem` becomes a directory (e.g., from a failed container build), the agent host cannot spawn any new containers — channels like WhatsApp stop replying entirely. The fix relocates TMPDIR to avoid this race condition.

## Feature Requests & Roadmap Signals
No pure feature requests were filed today, but several open PRs signal the next roadmap priorities:

- **Subject-matter governance** — PR #3029 adds CLI `approve/reject` verbs for approvals, enabling operators to resolve pending actions directly. Likely for next minor release.
- **Scheduled task templates** — PR #3022 lets agent templates define recurring tasks (cron + prompt). High demand for reducing manual setup.
- **Audit logging** — PR #2987 introduces an opt-in local audit log for the CLI surface, designed as a skill. Likely to land behind a feature flag soon.
- **Harness capability toggles** — PR #2983 adds per-group configuration to disable built-in harness capabilities (cron, scheduling) in favor of NanoClaw equivalents. Expected in the next few releases.

## User Feedback Summary
Real pain points visible today:

- **Silent message drops** — Users report agents that "go silent" on WhatsApp (#3027 root cause) or produce duplicate replies (#3026). Both are regressions from recent nudge changes.
- **Operational noise** — False-positive quota error logs (#3016) are eroding trust in monitoring; users can't distinguish real quota warnings from benign events.
- **Token cap confusion** — A user (#3023) hit the undocumented 32K output cap while generating OpenSCAD files, receiving a non-obvious error message. The cap has no clear path to configuration.
- **Container bootstrap fragility** — The `/tmp` poisoning issue (#3027) silently breaks container startup without clear error reporting to end users.

Overall sentiment: frustration with regressions introduced by recent nudge/rewrap changes, but appreciation for rapid fixes (output cap fix closed same day as filed).

## Backlog Watch
Issues requiring maintainer attention:

- **#3016** (opened July 11, 2 days ago) — Rate-limit mislogging. No fix PR. A one-line logging fix could eliminate 80+ weekly false positives per install.  
  [GitHub Issue #3016](https://github.com/nanocoai/nanoclaw/issues/3016)

- **Several long-lived open PRs** face merge conflicts or staleness due to `feat/guard-seam` advancement:
  - **#2987** (audit skill, opened July 9) — explicitly rebased but base keeps moving  
  - **#2982** (tool allowlist drift guard, opened July 8) — no recent activity  
  - **#2986** (guard seam, opened July 9) — large architectural change, still accumulating commits

- **No issues older than 1 week** are currently unanswered, suggesting maintainer responsiveness is strong.

---

*Generated from NanoClaw GitHub activity on 2026-07-13.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-13

## 1. Today's Overview
Project activity today was focused entirely on cleanup of previously submitted work, with **4 pull requests merged in a single batch** and **no new issues, releases, or open PRs** reported. After a period of no visible movement since early June, this coordinated merge of fixes across the agent runner, gateway, configuration, and cron subsystems signals a deliberate maintenance push by the maintainers. The repository is currently in a **clean state**: zero open issues, zero open PRs, and no new releases cut today. This suggests the team may be preparing for a milestone release or performing pre-release stabilization.

## 2. Releases
**No new releases** were published today. The latest release remains unchanged from prior periods.

## 3. Project Progress
All **4 closed PRs today** were merged and represent focused bug fixes and minor feature enablement:

- **#951 — fix(agent_runner): suppress stderr initialization logs on agent failure**  
  *Author: vernonstinebaker* | [PR Link](https://github.com/nullclaw/nullclaw/pull/951)  
  Prevents initialization logs (memory plan, MCP server registration, channel startup) from being posted as agent responses when the child process exits with non-zero status. Stderr fallback is now only used on success, eliminating spurious noise in failure scenarios.

- **#950 — fix(gateway): move port probe before allocations to prevent test leak**  
  *Author: addadi* | [PR Link](https://github.com/nullclaw/nullclaw/pull/950)  
  Reorders `gateway.run()` startup so the port availability check occurs before expensive allocations (`Config`, `RuntimeProviderBundle`, `SessionManager`, tools). Fixes resource leaks in test environments when `AddressInUse` failures occur early.

- **#949 — fix: make queue_mode configurable from config.json**  
  *Author: vernonstinebaker* | [PR Link](https://github.com/nullclaw/nullclaw/pull/949)  
  Adds `agent.default_queue_mode` configuration field, allowing users to set the initial queue mode (e.g., `"latest"`) for new sessions via `config.json`. Refactors `QueueMode` enum into `config_types.zig` as the single source of truth.

- **#948 — fix cron agent delivery attribution**  
  *Author: DonPrus* | [PR Link](https://github.com/nullclaw/nullclaw/pull/948)  
  Passes cron delivery origin metadata into spawned `nullclaw agent` subprocesses so `agent_start` events are correctly attributed to the delivery channel/account. Preserves routing flags for `nullclaw cron once-agent` in both local storage and gateway `/cron/add` payloads.

## 4. Community Hot Topics
**No active community discussion** occurred today. The 4 merged PRs had **zero comments** and **zero reactions** each, indicating these were internal/maintainer-driven changes rather than community-driven requests. The repository's zero open issue/PR count suggests either a very active maintainer team that clears backlogs quickly, or a currently low-engagement community.

## 5. Bugs & Stability
**No new bugs, crashes, or regressions** were reported today. However, the merged PRs address three stability-related issues:

- **Medium severity**: Spurious initialization logs leaked as agent responses on failure (#951) — could cause confusing output in error scenarios. **Now fixed**.
- **Medium severity**: Resource leaks in test environments when gateway fails with `AddressInUse` (#950) — caused incomplete cleanup of allocated components. **Now fixed**.
- **Low severity**: Cron agent deliveries not properly attributed to originating channels (#948) — affected audit trails and routing integrity. **Now fixed**.

No fixes merged today were regressions; all address existing behavioral gaps.

## 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. However, PR #949 (configurable `queue_mode`) represents a **completed feature** that users likely requested: exposing previously internal queue behavior to configuration. Given the pattern of these merges, the team appears focused on **configuration hardening** and **operational correctness** (resource cleanup, error handling, attribution) rather than new capabilities. The next version is likely to include:

- Improved configuration surface area (queue_mode)
- Better error resilience in gateway startup
- Cleaner agent failure output behavior
- Enhanced cron delivery metadata support

## 7. User Feedback Summary
**No user feedback was recorded today.** The zero-comment nature of all merged PRs, combined with the absence of open issues, makes it difficult to gauge user sentiment. However, the nature of the fixes — initialization log leakage, resource leaks, configuration gaps — suggests these were pain points identified internally or reported through non-GitHub channels. The fixes prioritize **production stability** and **clean operation** over new features.

## 8. Backlog Watch
**The backlog is empty.** There are **zero open issues** and **zero open pull requests** across the entire repository as of today's data. This is an unusually clean state that may reflect:
- A deliberate triage/sweep by maintainers in preparation for a release
- A project in a phase between feature development cycles
- Possible archiving or reduced active development pace

No long-unanswered items require maintainer attention at this time.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-13

---

## 1. Today's Overview

IronClaw is in a period of **intense development activity**, with 50 pull requests updated in the last 24 hours and a 50/50 split between open and merged/closed work. The project's core team is executing on a major **"Reborn" runtime overhaul** — a multi-PR delivery train spanning extension runtime, MCP registration, agent loop resilience, and CI hardening. However, **CI stability remains a critical concern**: issue #6014 documents that ~70% of July `main` pushes have been red, driven by a combination of flaky non-hermetic tests and deterministic-but-static-catchable breakage. The maintainers are responding forcefully with a dedicated pre-push static check PR (#6022) and targeted test isolation fixes (#6023). No new releases were cut today, but the Reborn feature train appears close to landing.

---

## 2. Releases

**No new releases** in the last 24 hours.

---

## 3. Project Progress

**25 pull requests were merged or closed today.** Notable progress includes:

- **Extension Runtime (P5) — Delivery Coordinator** (#6012, open): Slack/Telegram outbound delivery wiring, fifth of eight runtime PRs. Green across workspace, integration, and both database backends.
- **Extension Runtime (P6) — Extraction Completion** (#6025, open, draft): Config/connect UI, frontend, CLI, and migrations for the extension runtime. Sixth PR in the train.
- **Per-User MCP Registration Store** (#5970, open): T1 of the MCP registration stack, rebuilt on `InstallationOwner` machinery. Supersedes #5916 with all prior review feedback incorporated.
- **Prompt-Cache Break Detection** (#5975, open): Detects when KV-cache collapses (82%→29% hit rate observed on long agentic turns) and stops doomed compaction loops. Stack 1/4 on issue #5959.
- **Read-Before-Edit Guardrails** (#5978, open): Rejects stale edits when files changed since the model read them. Stack 3/4 on the skill-listing PR.
- **Post-Edit Diagnostics** (#5979, open): Surfaces NEW diagnostics after each edit (baseline→diff, pydoc-parse, lint) to reduce collateral damage from agent edits.
- **Skill Listing Optimization** (#5977, open): Advertises skills as one-line listings; loads full bodies only on activation. Shrinks system prompt by ~7K tokens/call.
- **Reborn Loop Resilience** (#5959, open): Deep availability retries, iteration backstop, model-visible tool-failure reasons. Addresses the 30% vs 65% SWE-bench gap versus Hermes/OpenClaw.
- **CI Static Pre-Push Checks** (#6022, open): Adds `include_str!` path verification, Docker-COPY coverage, hermetic env guards. Implements issue #6018.
- **Unix Timestamp Support in builtin.time** (#6024, open): Accepts JSON numbers, fractional seconds, Slack timestamps — reduces agent arithmetic overhead.
- **Doctor Command Enhancement** (#6019, open): Adds LLM/provider credential readiness checks, optional `--live` probes.
- **Agent Loop Completion Nudge** (#6013, open): Makes interactive coding nudges tools-capable.

---

## 4. Community Hot Topics

The most active discussions center around **CI reliability and user onboarding friction**:

- **#6014 — "CI fragility: flaky non-hermetic tests abort the coverage matrix"** (OPEN, 0 comments, high severity context): Documents that ~70% of July pushes failed, with two "full-red waves" (Jun 29–Jul 3, Jul 8–11). This is the single biggest drag on project health and has spawned dedicated fix work (#6022, #6023). A daily failure taxonomy (#6011) provides systematic tracking.

- **#6015 — "build_runtime_input_production_* races on std::env"** (OPEN): Identifies a genuine test-isolation defect in the `all-features` coverage leg. A targeted fix (#6023) is already proposed. This is the only flaky-CI offender that is a real code defect rather than a timing-dependent test.

- **#6016 — "Slack trigger-delivery e2e tests time out"** (OPEN): The two most recent `main` failures (Jul 11) were caused by this. The fix is in #6020 (Q-10 Slack journey determinism PR).

- **#6017 — "DB concurrency contract tests flake"** (OPEN): Postgres delete/recreate race and libSQL concurrent writer tests time out under parallel load.

- **#2601 — "Feature Proposal: CLI / TUI for Managing Secrets"** (OPEN, 2 comments, created Apr 18): A long-standing user request about authentication friction. The author notes that "authentication patterns may drift over time" and that secrets management is "not well documented." No maintainer response visible yet — this is the oldest open feature request in the digest.

---

## 5. Bugs & Stability

**Severity: High**

- **[Q-10 Slack journeys non-deterministic]**: Issue #6016, fix in #6020. Slack e2e tests intermittently miss fired triggers. The fix adds model-visible Slack/outbound contract alignment and public-output redaction guards.
- **[Non-hermetic test races in coverage leg]**: Issue #6015, fix in #6023. 14 `build_runtime_input_production_*` tests flake together in `all-features` mode. Root cause: a missing serialization lock in the test harness.

**Severity: Medium**

- **[DB concurrency contract tests]**: Issue #6017. Postgres CAS delete-vs-recreate race and libSQL concurrent writer tests — timing-sensitive rather than deterministic.
- **[Image preview transparency during chat]**: Issue #5704 (CLOSED). UI bug: image thumbnails lose opacity while agent is generating. Already fixed.

**Severity: Low**

- **[GLM-5.2 inference hangs]**: Issue #6010 (CLOSED). Model hangs for minutes during opencode usage. Already fixed or workaround identified.
- **[GLM-5.2 not in default model list]**: Issue #6009 (CLOSED). Manual addition required. Already resolved.

**Structural Concern**: The CI failure taxonomy (#6011) reveals that clawbench analysis of run `e7457386` showed ~103 of 136 non-pass results are due to a benchmark provisioning defect, not model or harness quality. This suggests the benchmarking infrastructure itself has reliability issues that may confound performance comparisons.

---

## 6. Feature Requests & Roadmap Signals

**Strong roadmap signal — high likelihood of landing next cycle:**

- **Extension Runtime (P5 + P6)**: PRs #6012 and #6025 are actively in review. This is the largest feature landing in progress — Slack/Telegram outbound, config UI, frontend, CLI, and database migrations.
- **MCP Registration Store** (#5970): Per-user MCP registration is the foundation for the MCP ecosystem. Expect T2 (egress enforcement) and T3 (registration UI) to follow.
- **Prompt-Cache Break Detection** (#5975): This is a performance-critical optimization. Claude Code's KV-cache management is a competitive differentiator, and IronClaw is clearly closing this gap.

**Moderate roadmap signal:**

- **CI Hardening Suite** (#6018 → #6022): Static pre-push checks are likely to land within days given the severity of the CI situation.
- **Skill Listing Optimization** (#5977): Reducing prompt token overhead by ~7K tokens/call is a meaningful UX improvement for agent users.

**Lower likelihood but notable:**

- **CLI/TUI for Secrets Management** (#2601): This issue has been open since April with no maintainer activity. It may be deprioritized in favor of the extension runtime's configuration UI, which could absorb this need.

---

## 7. User Feedback Summary

**Identified pain points:**

1. **Authentication / Secrets management** (#2601): "Struggles with authentication for some services" and poor documentation on secrets management. The author explicitly acknowledges this may be "understandable" given drifting auth patterns, but the lack of a CLI/TUI for secrets is a friction point for new users.

2. **Inference reliability for interactive coding** (#6010, #6009): GLM-5.2 hangs "for minutes at a time" during opencode usage, making it "unusable for real-time interactive development." Additionally, the model isn't in the default opencode model list, requiring forking and manual addition — "significant effort and technical knowledge."

3. **UI polish** (#5704, closed): Image previews becoming transparent during chat processing. While fixed, this reflects ongoing UX surface area improvements.

**Satisfaction signals:** The pace of Reborn feature delivery (P5 and P6 drafted in consecutive days) and the aggressive CI stabilization work suggest the core team is responsive to the SWE-bench gap findings (30% vs 65%) and user feedback about runtime reliability.

---

## 8. Backlog Watch

| Issue/PR | Age | Status | Concern |
|----------|-----|--------|---------|
| **#2601 — CLI/TUI for Secrets** | Created Apr 18 (~87 days) | OPEN | Oldest open issue in digest. Two user comments, zero maintainer responses. |
| **#4032 — WASM dependency bumps** | Created May 25 (~49 days) | OPEN, needs merge | Dependabot PR with 2 updates (wit-component, wit-parser). Stale. |
| **#5114 — Tokio ecosystem bumps** | Created Jun 21 (~22 days) | OPEN, needs merge | Dependabot PR with 4 updates. Could block tokio-related work if left unmerged. |
| **#5664 — GitHub Actions bumps** | Created Jul 5 (~8 days) | OPEN, needs merge | 16 updates, including `actions/checkout` v4→v7 and `claude-code-action` v1.0.88→v1.0.171. Action updates are security-sensitive. |
| **#5926 — Everything-else deps bumps** | Created Jul 10 (~3 days) | CLOSED | Merged — good hygiene. |

**Notable**: The Dependabot PR backlog is accumulating. #4032 and #5114 are weeks old with no maintainer activity. Given that #5664 includes a major leap for `claude-code-action` (v1.0.88→v1.0.171) and `actions/checkout` (v4→v7), these bumps may have compatibility concerns requiring manual review. However, the project's focus on the Reborn feature train and CI stabilization likely explains the delayed dependency maintenance.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-13

## Today’s Overview

Project activity remains moderate, with 1 issue and 2 pull requests updated in the past 24 hours. The majority of traffic is focused on a lingering user-reported regression concerning multi-agent `USER.md` file overwriting (Issue #2293), which has collected 4 comments and is now a week old with no maintainer response. Two stale PRs (#1325 and #2065) received updates but neither has moved toward merge. No new releases were cut, and the project appears to be in a maintenance lull, with community patience potentially wearing thin around a clear data-loss bug. Overall project health is stable but warrants attention to the open bug and backlog clearance.

## Releases

No new releases were published on 2026-07-13 or in the preceding days. The latest available release remains from an earlier period.

## Project Progress

Two pull requests were updated but none were merged or closed as part of normal progress today:
- **[PR #2065 — CLOSED]** *fix(agent): 使用短 UUID 替代名称生成 Agent ID* — This PR was marked as closed. It addressed a data resurrection bug where re-creating an Agent with the same name reused old workspace files. The fix replaces name-derived IDs with short UUIDs. However, the PR notes that deletion of associated `cowork_sessions` is still not handled. The closing is notable — it may have been merged or abandoned, but no merge commit is visible in the daily data.
- **[PR #1325 — OPEN]** *feat(ui): 为新建对话图标按钮添加悬停提示* — This UI enhancement (adding tooltips to the new-chat button) remains open and appears idle since April 2026. It was last updated due to a stale bot or minor comment.

There were no feature-advancing merges in the last 24 hours.

## Community Hot Topics

**Most active issue:**
- **[Issue #2293 — OPEN] 重启后，多个agent下的USER.md被覆盖替换的BUG？** — [GitHub](netease-youdao/LobsterAI Issue #2293)  
  Author: yepcn | Created: 2026-07-07 | Updated: 2026-07-12 | Comments: 4  
  *Analysis:* This is the clear hot topic. The user describes a critical regression where modifying one Agent's `USER.md` (or "About You" settings) overwrites the same file for all other Agents. Worse, this behavior persists across restarts — the main Agent's `USER.md` replaces all others on launch. The issue has gone unanswered for 6 days, suggesting maintainer unavailability or lack of prioritization. Underlying need: multi-agent profile isolation is a core feature, and this break essentially makes multiple agents unusable.

**Most active PRs (both stale):**
- PR #1325 (0 comments, but long open) and PR #2065 (recently closed) — both have low community engagement but represent unaddressed work.

## Bugs & Stability

| Severity | Bug | Status | Fix PR? |
|----------|-----|--------|---------|
| **Critical** | Multi-agent USER.md overwrite on restart (Issue #2293) | Open, 6 days old, no maintainer response | None visible |
| Medium | Agent ID regeneration fixes data resurrection but leaves orphan sessions (PR #2065) | Closed — fix partially applied | PR #2065 (closed) |
| Low | Tooltip missing on new-conversation button (PR #1325) | Open, idle since April 2026 | PR #1325 (open) |

**Ranking rationale:** The USER.md overwrite bug is critical because it causes silent data loss/corruption across all agents. Users cannot maintain distinct agent personalities. No fix PR exists. The partial fix in PR #2065 is not directly related but highlights ongoing workspace cleanup problems.

## Feature Requests & Roadmap Signals

No new feature requests were filed in the last 24 hours. The community is currently focused on bug resolution rather than new feature requests. However, signals from the existing codebase and PRs suggest two areas of user demand:

1. **Improved multi-agent management** — The USER.md bug indicates users are actively using multiple agents with distinct identities. Formal support for per-agent file isolation and workspace cleanup is needed.
2. **UI polish for collapsed sidebar** — PR #1325 suggests users care about discoverability of UI actions when in a compact view. This tooltip enhancement is small but reflects broader UX maturity goals.

At this pace, the next minor release is likely to include the Agent UUID fix (PR #2065) and possibly the tooltip enhancement (PR #1325), but only if maintainers return to active triage.

## User Feedback Summary

**Pain points expressed:**
- Inability to maintain separate agent identities due to `USER.md` overwriting (Issue #2293). User explicitly states: *“这样就没法对不同agent建立不同的需求”* — “then it's impossible to set different requirements for different agents.”
- User reports the bug is a *regression from a recent update* — implying previous versions worked correctly. This erodes trust.
- Workaround attempts (manually editing `workspace-*` files while software is closed) fail because the software forcefully replaces all files on restart.

**Satisfaction signals:** No positive feedback was recorded in the last 24 hours.

**Overall sentiment:** Frustrated, with one vocal user documenting a clear workflow-blocking bug and receiving zero acknowledgement.

## Backlog Watch

| Item | Age | Maintainer Action Needed |
|------|-----|-------------------------|
| **Issue #2293** — Multi-agent USER.md overwrite | 6 days | **High priority** — Needs at minimum a triage response, workaround suggestion, or assignment. Currently a critical bug with zero response. |
| **PR #1325** — Tooltip enhancement | 3+ months | Low priority but needs a decision (merge, close, or request changes). Staleness suggests maintainer bandwidth issue. |
| **PR #2065** — Agent ID fix (partially closed) | 6 weeks | Clarify whether this was merged or closed without merge. If closed, why? The orphan session problem remains. |

**Most concerning:** Issue #2293 represents the highest-urgency backlog item. Its continued silence risks user churn and dissatisfaction on a core feature.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-13

## 1. Today's Overview
CoPaw experienced a **high-activity day** with 21 issues updated and 10 PRs updated in the last 24 hours, indicating sustained community engagement and active development. The project is dealing with **significant post-2.0.0 stability challenges**, particularly around context compression breaking tool_call/tool_result pairing, message serialization errors with OpenAI-compatible APIs, and v1→v2 compatibility regressions. A cluster of **3 PRs all targeting the same legacy `file` block type compatibility fix** suggests some coordination friction in the contributor pipeline, though the issue is now resolved. **No new releases** were published today, which is notable given the volume of critical bugs being reported.

## 2. Releases
**No new releases** today. The latest version remains **CoPaw v2.0.0** / AgentScope 2.0.4.

## 3. Project Progress
**3 PRs merged/closed today:**

- **#5987** (closed) — `fix(scroll): sanitize unpaired tool messages after context compression` by tadebao. Addresses the root cause of the 400 BadRequestError epidemic: orphan `tool_result` messages surviving context compression and confusing API formatters. *This is the most impactful fix merged today.*
- **#5988** (closed) — `fix(compat): handle legacy 'file' block type in _coerce_block` by Nioolek. Fixes v1→v2 deserialization for `file`-type tool results, which were silently failing.
- **#5990** (closed/NOT MERGED?) — Identical description to #5988 by the same author, likely a duplicate/retracted PR.

**Key feature advancement**: PR #5869 (`feat(console, tui): expose system commands in slash autocomplete across all UIs`) by Jun-yao-hub remains **open and under review** — this would significantly improve discoverability of daemon/control commands in both TUI and Web Console.

## 4. Community Hot Topics

| Issue/PR | Comments | Topic |
|----------|----------|-------|
| [#5996](https://github.com/agentscope-ai/QwenPaw/issues/5996) | **5 comments** | `MODEL_EXECUTION_ERROR` — `ToolResultBlock` serialized as orphan `role=tool` message without preceding `tool_calls` |
| [#5952](https://github.com/agentscope-ai/QwenPaw/issues/5952) | **4 comments** | Auto-memory fails: `No module named 'agentscope.tool._builtin._scripts'` |
| [#5986](https://github.com/agentscope-ai/QwenPaw/issues/5986) | **4 comments** | Context compression evicts tool_call/tool_result pairs → 400 error |
| [#5998](https://github.com/agentscope-ai/QwenPaw/pull/5998) | **2 comments** | Memory context inconsistency: Agent ignores user-confirmed plan |

**Underlying need analysis**: The **dominant theme** across the most active issues is **message integrity during context management**. Users are hitting API 400 errors because CoPaw's compression/eviction logic does not preserve the paired relationship between `tool_calls` (assistant) and `tool_result` (tool) messages. This is a **systemic architectural issue** in the message pipeline — it affects multiple formatters (OpenAI, DeepSeek), multiple trigger paths (context compression, background tools, legacy compat), and multiple UI entry points (console, Feishu). The clustering of comments across #5996, #5986, and #5985 suggests this is the #1 pain point for power users running long sessions.

## 5. Bugs & Stability

**Critical severity:**
- **#5996 / #6002** — `MODEL_EXECUTION_ERROR`: Assistant messages containing `ToolResultBlock` get serialized as orphan `role=tool` messages without preceding `tool_calls`, causing OpenAI API 400 errors. **Root cause**: `_hint.py:make_offload_hint_msg()` creates mixed-content assistant messages that break the OpenAI message protocol. **Fix status**: PR #5989 (by tadebao, open) provides multi-layer orphan defense. No fix merged yet.

- **#5986** — Context compression breaks `tool_call/tool_result` pairing → 400 BadRequestError. **Fix status**: PR #5987 (by tadebao, **closed/merged**) addresses the scroll path. Production users should upgrade.

**High severity:**
- **#5952** — Auto-memory completely broken in v2.0.0 desktop app: `No module named 'agentscope.tool._builtin._scripts'`. PyInstaller bundle missing `_glob_helper.py`. **Fix status**: PR #5997 (by wananing, open) includes AgentScope Glob helper in desktop bundle.
- **#5984 / #5982** — Shell execution demands approval every time even when governance is disabled. Landlock-devoid kernels (Raspberry Pi, containers) cannot permanently disable approval prompts. **Fix status**: No fix PR yet.
- **#5978** — `/compact` fails on Telegram sessions due to `:` being an invalid filesystem character in session IDs. **Fix status**: No fix PR yet.

**Medium severity:**
- **#5995** — Messages silently dropped when session is busy (no queue, no error logged). Feishu channel users lose messages under concurrency. **Fix status**: No fix PR yet.
- **#5998** — Agent memory context inconsistency: ignores user-confirmed plan and falls back to old erroneous data. UX trust issue.
- **#5985** — Combined trigger: `chat_with_agent` tool + context compression + DeepSeek V4 Pro → assistant message split into orphan `tool` messages.

**Low severity / Nuisance:**
- **#5983** — `qwenpaw doctor` always reports FAIL due to wrong health check URL (`/api/agent/health` vs `/api/version`). Simple config error.
- **#5981** — Model search field auto-filled with auth username rather than model names.

**Compatibility regressions (v1→v2):**
- **#5964** — Chat list mapping lost on upgrade to v2.0.0; sessions in DB but unreachable via UI (500 error).
- **#5980** — v2.0.0 Desktop missing SSH Offline and Profiles features (return 404).
- **#5993 / #5991 / #5990 / #5988** — Three PRs all fixing `file` block type in legacy deserialization; merged now.

## 6. Feature Requests & Roadmap Signals

**Most requested features:**
1. **#5999** — Cross-channel session handoff: Continue the same agent conversation across Console, Feishu, DingTalk seamlessly. *Predict next version: medium priority — requires session routing infrastructure.*
2. **#6001** — Skill pool auto-discovery for newly installed skills (currently broken). *Predict next version: high priority due to "completely broken" status.*
3. **#5994** — Governance policy customization: user wants to disable security checks entirely (AUTO mode hit for every operation). *Predict next version: likely addressed via config toggle.*
4. **#5992 (PR)** — Per-session model overrides (Settings > Models modal). *Under review, likely merged soon.*

**Feature gaps identified from user reports:**
- Skill system installation pipeline is broken for *all* new skills (not just some).
- No concurrency queue for incoming messages — silent dropping is a design gap.
- No per-session filesystem (Telegram `:` in session ID) — session IDs leak into filesystem paths.

## 7. User Feedback Summary

**Satisfaction signals:**
- Active community contributing **3 distinct first-time-contributor PRs** (#5993, #5869, #5987) — indicates engaged power-user base.
- Users are actively upgrading to v2.0.0 (desktop app users reporting v1→v2 upgrade experiences), suggesting the new version is desired despite regressions.

**Dissatisfaction signals:**
- **"completely broken"** (verbatim, in #6000) — skill system for new installations.
- **"非常浪费时间"** (very time-consuming) — security governance triggers on every operation.
- **"非常浪费时间和多次不必要的尝试和错误输出"** (very wasteful, repeated unnecessary attempts) — memory inconsistency causing agent to ignore user's explicit confirmation.
- **"critical for my workflow"** — SSH Offline and Profiles features returning 404 in v2.0.0 Desktop, users blocked from upgrading.

**Key pain points from real use cases:**
- **Travel planning scenario** (#5998): Agent creates itinerary, user corrects it, user confirms correction, agent ignores correction and uses old itinerary. This erodes user trust in agent reliability.
- **Container/edge deployment** (#5982, #5984): Governance prompts cannot be disabled on Raspberry Pi / ARM / Docker hosts — breaks automation.
- **Long sessions** (#5986): Power users with long-running conversations hit 400 errors during context compression, losing work.

## 8. Backlog Watch

**Issues needing maintainer attention:**
- **#5964** (2026-07-11, 2 comments) — v2.0.0 upgrade broke chat list mapping. No fix PR yet. Affects all users upgrading with existing chat history.
- **#5977** (2026-07-12, 1 comment) — Plugin HTTP routes lost after workspace hot-reload. PluginRegistry singleton incorrectly clears routes. Affects plugin developers.
- **#5979** (2026-07-12, 1 comment) — Electron CLI tool cannot run in Linux sandbox because real user mapped to root; `--no-sandbox` doesn't help. Blocks Obsidian CLI usage.
- **#5978** (2026-07-12, 1 comment) — `/compact` fails on Telegram sessions due to `:` character in session ID. Blocks memory compaction for Telegram users.
- **#5952** (2026-07-10, 4 comments) — Auto-memory completely broken on desktop. PR #5997 exists but not yet merged. High impact for desktop users relying on memory summarization.

**PRs needing review:**
- **#5869** (2026-07-08, "Under Review") — Slash autocomplete across all UIs. Significant UX improvement, pending review for 9 days.
- **#5791** (2026-07-05, "Under Review") — formatCompact rounding rollover fix. Minor but affects number display quality. Pending review for 8 days.
- **#5992** (2026-07-12) — Per-session model overrides. New feature, needs architectural review.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

**Project Digest: ZeroClaw**
**Date:** 2026-07-13
**Source:** GitHub (`zeroclaw-labs/zeroclaw`)

---

### 1. Today's Overview

ZeroClaw is in the midst of a major development sprint, with 33 updated issues (32 active) and 50 updated pull requests (47 open) in the last 24 hours. Activity is extremely high, driven by two major workstreams: the **SOP (Standard Operating Procedure) milestone** and a sweeping **memory subsystem overhaul**. A broad "v0.8.3 maintenance train" is also actively landing features, while several P1 severity bugs related to memory leaks, context budget overflows, and process crashes are under active remediation. No new releases were cut today.

### 2. Releases

None.

### 3. Project Progress

One PR was closed today, and three were merged/closed in the reporting window:
- **PR #8940 (CLOSED):** A small bugfix (`fix(zerocode): apply fill_style() to queue sidebar and session picker overlays`) fixing a visual regression in the ZeroCode theme was merged.
- **PR #9027 (MERGED):** A focused fix (`fix(sop): key AMQP dispatch idempotency on the message-id`) ensures that duplicate SOP runs are prevented when a single AMQP message matches multiple SOP definitions. This is a direct step toward the SOP 5/5 milestone.

Major features advancing via open PRs include:
- **Memory Overhaul:** A series of large, stacked PRs from author `Nillth` is reshaping the memory engine: adding a **gated rerank stage**, a **mandatory content-screening layer**, a **gated audit trail**, a **retrieval cache decorator**, and **typed memory classification**. These are foundational changes for performance and security.
- **SOP Milestone:** PRs #8848, #8880, and #8903 are a stacked sequence adding HITL (Human-in-the-Loop) approval, broker-based group membership/quorum, and channel delivery for approval requests.
- **WASM & Plugins:** PR #8661 is a proof-of-concept for running WASM plugins out-of-process via a sidecar. PR #8852 wires in the ability to run installed WASM channel plugins.
- **ZeroCode UX:** PR #8655 is a major refactor to consolidate the Code pane, rails, and prompt drafts.

### 4. Community Hot Topics

The most active discussions are centered on core architectural stability and feature delivery:

- **Issue #8681 (Tracker, 9 comments):** `[Tracker]: Goal mode implementation split stack`. This tracker coordinates the splitting of a massive, already-implemented `feat/goal-mode` branch into reviewable PRs. The high level of engagement reflects the complexity of this feature and the team's effort to ensure safe integration.
    - *Link:* [Issue #8681](https://github.com/zeroclaw-labs/zeroclaw/issues/8681)

- **Issue #5808 (P1 Bug, 8 comments):** `Default 32k context budget is exceeded...`. This is a long-standing, high-severity issue where the system prompt + tool definitions alone exceed the default context budget, causing a perpetual preemptive trim loop. The continued activity suggests finding a resolution is critical for user onboarding.
    - *Link:* [Issue #5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808)

- **Issue #6055 (Feature, 6 comments):** `Slack: hydrate thread context from conversations.replies...`. A feature request with consistent engagement, highlighting a key user need for seamless Slack integration where the agent can understand the history of a thread when first mentioned.
    - *Link:* [Issue #6055](https://github.com/zeroclaw-labs/zeroclaw/issues/6055)

### 5. Bugs & Stability

The project is actively fighting several high-risk stability bugs:

- **Issue #8654 (P1, High Risk):** `skill-review fork panics (out-of-range slice...)`. A critical crash bug where the background skill-review fork causes a SIGSEGV, taking down the entire agent pod. It is marked `in-progress`.
    - *Link:* [Issue #8654](https://github.com/zeroclaw-labs/zeroclaw/issues/8654)

- **Issue #8642 (P1, High Risk):** `MCP/tool-schema cloning drives unbounded RSS growth`. A memory leak bug, split from a larger OOM tracker, where MCP tool schema cloning causes unbounded memory growth in the agent loop. It is marked `accepted`.
    - *Link:* [Issue #8642](https://github.com/zeroclaw-labs/zeroclaw/issues/8642)

- **Issue #9016 (P2, New):** `OpenAI tool turns fail when Chat Completions rejects reasoning effort`. A workflow-blocking bug where sending a non-`none` reasoning effort with function tools causes an API failure. No fix PR is linked yet.
    - *Link:* [Issue #9016](https://github.com/zeroclaw-labs/zeroclaw/issues/9016)

- **Issue #9019 (P1, New):** `OpenAI Responses provider rejects vision-capable models...`. The new `responses` API provider hardcodes `vision = false`, blocking images from being sent. Marked as a P1 blocker.
    - *Link:* [Issue #9019](https://github.com/zeroclaw-labs/zeroclaw/issues/9019)

- **Issue #9017 (P2, New):** `--config-dir is ignored during CLI locale detection`. A degraded behavior bug where CLI help translation reads the wrong config directory.
    - *Link:* [Issue #9017](https://github.com/zeroclaw-labs/zeroclaw/issues/9017)

### 6. Feature Requests & Roadmap Signals

Several new feature requests hint at upcoming priorities:

- **Issue #9022 (New):** `Optional Slack Events API (HTTP Request URL) mode for scale-to-zero deploys`. This request is for a more scalable, event-driven Slack integration path. This is a clear signal for cloud-native deployment scenarios and is a likely candidate for a future release.
    - *Link:* [Issue #9022](https://github.com/zeroclaw-labs/zeroclaw/issues/9022)

- **Issue #9020 (New):** `Add session rewind and fork-from-message workflows to ZeroCode`. This addresses a core resiliency and usability gap in the ZeroCode interface. Given the project's focus on ZeroCode, this is highly likely to be prioritized in the v0.8.3 or v0.8.4 scope.
    - *Link:* [Issue #9020](https://github.com/zeroclaw-labs/zeroclaw/issues/9020)

- **Issue #9010 (Tracker):** `ZeroCode Consolidation & Hardening`. This official tracker signals that the team is moving from feature velocity into a stabilization and hardening phase for the ZeroCode surface. This is a strong roadmap signal.
    - *Link:* [Issue #9010](https://github.com/zeroclaw-labs/zeroclaw/issues/9010)

### 7. User Feedback Summary

User feedback this period highlights a tension between advanced features and baseline stability:

- **Pain Point (Critical):** Users are actively hitting P1 bugs that block workflows (context overflows, process crashes, failing API calls). This indicates that while the project is moving fast, stability in the default configuration is a clear source of dissatisfaction.
- **Pain Point (Usability):** The request for Slack thread history hydration (Issue #6055) and Telegram multi-message mode (Issue #8445) show users want more natural, rich integrations with existing communication tools.
- **Success Signal:** The active community engagement on complex architectural issues (e.g., goal-mode tracker, WASM plugins) suggests a developer user base that is engaged and invested in the project's long-term capabilities.
- **New User/Operator Friction:** The `--config-dir` bug (Issue #9017) and the "SOP documentation missing" report (Issue #7762) indicate friction for new operators trying to configure the system.

### 8. Backlog Watch

Several critical items with significant history require continued maintainer attention:

- **Issue #5808 (P1, Updated 2026-07-12):** The default context budget overflow bug. This has been open since April and is a fundamental onboarding blocker. While marked `in-progress`, its longevity is a concern.
    - *Link:* [Issue #5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808)

- **Issue #6074 (P2, Updated 2026-07-12):** `audit: track 153 commits lost in bulk revert`. This is a high-risk audit task to recover potentially 153 commits lost in a bulk rollback. The fact that this is still open after several months is a significant technical debt risk.
    - *Link:* [Issue #6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)

- **Issue #7762 (P2, Updated 2026-07-12):** `Cron documentation missing and need to run cronjobs with a specific model`. This issue has been open for a month with no action indicators. The lack of documentation for a core feature (cron) is a clear documentation gap.
    - *Link:* [Issue #7762](https://github.com/zeroclaw-labs/zeroclaw/issues/7762)

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*