# OpenClaw Ecosystem Digest 2026-08-24

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-24 00:31 UTC

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

# OpenClaw Project Digest — 2026-08-24

## 1. Today's Overview

OpenClaw shows a high-velocity development cycle with 500 issues and 500 PRs updated in the last 24 hours, though this includes a considerable backlog: only 44 issues (8.8%) and 96 PRs (19.2%) were closed or merged during this window. The project is in active beta validation (v2026.8.1-beta.2), with a **P0 SQLite corruption issue** (#126821) and a **P0 totalTokens inflation bug** (#125333) both confirmed on the beta, though neither is formally marked as a beta release blocker. A significant **P0 iOS app regression** (#108520) breaking Talk Mode and chat remains open with the "ux-release-blocker" tag, indicating a potential mobile release hold. Merged PRs today focused on security (install policy acknowledge flow, transcript credential contract opt-out), gateway delivery fidelity, and UI reliability (session roster refresh storms, terminal message handling). Maintainer bandwidth appears strained, with a substantial number of issues tagged `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision`, and many PRs waiting on author or maintainer review.

## 2. Releases

**No new releases were published in the last 24 hours.** The last known release is `v2026.8.1-beta.2`, currently undergoing release validation via issue #125626. No migration notes or breaking-change announcements are available for a new version.

## 3. Project Progress

The 96 merged/closed PRs indicate steady progress across several fronts. Notable completed work (based on PR titles and labels):

- **Security & Policy:** [#116489](https://github.com/openclaw/openclaw/pull/116489) (merged) requires explicit acknowledgement for install policy warnings, closing a security boundary gap. [#128077](https://github.com/openclaw/openclaw/pull/128077) (open) lets operators opt out of the transcript credential contract. [#120900](https://github.com/openclaw/openclaw/pull/120900) (merged) adds UI for reviewing install policy warnings.
- **Gateway & Delivery:** [#126424](https://github.com/openclaw/openclaw/pull/126424) (merged) fixes conversation delivery scoping within agent bindings, addressing a multi-agent message-routing problem. [#128423](https://github.com/openclaw/openclaw/pull/128423) (merged) preserves mixed-media failure receipts, ensuring silent attachment failures are surfaced.
- **UI/UX:** [#123535](https://github.com/openclaw/openclaw/pull/123535) (open) addresses session catalog refresh storms in the Control UI. [#128397](https://github.com/openclaw/openclaw/pull/128397) (open) fixes terminal messages from reloading the session roster. [#128115](https://github.com/openclaw/openclaw/pull/128115) (open) adds collapsible Workboard columns.
- **Config & Secrets:** [#123209](https://github.com/openclaw/openclaw/pull/123209) (open) fixes channel schema ownership after a `preferOver` replacement. [#128318](https://github.com/openclaw/openclaw/pull/128318) (open) isolates manifest-owned credential failures so one bad plugin doesn't take down the gateway.
- **Model/Commands:** [#125471](https://github.com/openclaw/openclaw/pull/125471) (merged) keeps Claude CLI OAuth available in the Control UI after gateway restarts. [#128116](https://github.com/openclaw/openclaw/pull/128116) (open) fixes auth probe fallback selection skipping retired catalog rows.
- **Tooling:** [#123975](https://github.com/openclaw/openclaw/pull/123975) (merged) cleans up `tsgo` process trees on timeout or signal, addressing a classic zombie-process hygiene issue.

Several fixes target long-standing issues from this digest's "Bugs" section, including memory search timeouts ([#128244](https://github.com/openclaw/openclaw/pull/128244)) and Unicode boot reply suppression ([#110641](https://github.com/openclaw/openclaw/pull/110641)).

## 4. Community Hot Topics

The most active discussions reveal three core themes: **release reliability, message-delivery correctness, and infrastructure resilience.**

- **Release Validation v2026.8.1-beta.2** ([#125626](https://github.com/openclaw/openclaw/issues/125626)) — 18 comments. The formal validation process for the current beta, indicating the team is actively preparing for a stable release. This is the single most commented item.

- **Windows vitest teardown EBUSY error** ([#119796](https://github.com/openclaw/openclaw/issues/119796)) — 15 comments, *closed*. A Windows-specific test infrastructure failure where the agent state SQLite handle wasn't released. Closed, suggesting a fix is in place.

- **DeepSeek cron agent stalls** ([#121953](https://github.com/openclaw/openclaw/issues/121953)) — 13 comments. A provider-specific workaround is needed: the `[cron:<jobId> <name>]` prefix causes DeepSeek's API to deprioritize requests. This highlights the growing importance of provider-agnostic message formatting.

- **Client-delegated message tool interruption** ([#109490](https://github.com/openclaw/openclaw/issues/109490)) — 12 comments, *closed as duplicate*. A turn-interruption bug where promised work from a progress message never executed. Closed as duplicate, indicating the issue is tracked elsewhere.

- **A2A sessions_send duplicate messages** ([#39476](https://github.com/openclaw/openclaw/issues/39476)) — 12 comments. A core architectural issue with the A2A protocol where bidirectional `sessions_send` calls create duplicate channel messages. Long-running (since March) but critical for inter-agent workflows.

- **Codex OAuth refresh timeout** ([#89278](https://github.com/openclaw/openclaw/issues/89278)) — 10 comments, 2 👍. A regression where auth refresh succeeds but cron/heartbeat fail within a 10-second timeout. High user pain as it breaks scheduled automation.

The volume of discussion around message-delivery issues (Slack, Telegram, WhatsApp) and session-state consistency suggests these are the most impactful user-facing problems right now.

## 5. Bugs & Stability

**P0 (Critical / Release-Blocking Potential):**

| Issue | Description | Impact | Fix PR? |
|-------|-------------|--------|---------|
| [#126821](https://github.com/openclaw/openclaw/issues/126821) | SQLite corruption recurs on pristine DBs within 15-24h (WSL2, 2026.8.1-beta.2), incl. "paralyzed gateway" mode | Data loss, crash-loop | **No PR linked** — **Critical** |
| [#108520](https://github.com/openclaw/openclaw/issues/108520) | iOS app update breaks Talk Mode and chat (gateway connects, but no functionality) | UX release blocker | **No PR linked** — **Critical** |
| [#125333](https://github.com/openclaw/openclaw/issues/125333) | `totalTokens` inflation persists on beta.2; #123065 fix incomplete (`api === "cli"` only) | Session-state, data-loss | **No PR linked** — **Critical** |

**P1 (Major regressions):**

- **Session/Message Loss Clusters:** [#112668](https://github.com/openclaw/openclaw/issues/112668) (sessions_yield timeout drops subagent announce), [#111358](https://github.com/openclaw/openclaw/issues/111358) (sessions_send misdelivers as webchat), [#102380](https://github.com/openclaw/openclaw/issues/102380) (Slack button interaction uses heartbeat wake instead of reply turn). These all point to systemic fragility in the inter-session communication layer.
- **Delivery Failures:** Telegram stuck in `send_attempt_started` and lost on restart ([#126246](https://github.com/openclaw/openclaw/issues/126246)), WhatsApp blank bubbles on expired quote cache ([#127948](https://github.com/openclaw/openclaw/issues/127948)), QQBot slash commands unresponsive ([#125838](https://github.com/openclaw/openclaw/issues/125838)).
- **Context Management:** [#111857](https://github.com/openclaw/openclaw/issues/111857) — CLI budget reopens full compacted JSONL, inflating prompt estimates and causing repeated compactions. [#108215](https://github.com/openclaw/openclaw/issues/108215) — context usage drops from 57% to 13% without compaction, indicating a potential state-loss bug.
- **Process/Resource Leaks:** [#97616](https://github.com/openclaw/openclaw/issues/97616) — un-reaped hook/tool child processes causing zombie accumulation. [#91144](https://github.com/openclaw/openclaw/issues/91144) — Windows Scheduled Task gateway doesn't stay running.

**P2 (Moderate):**
- [#121046](https://github.com/openclaw/openclaw/issues/121046) — temporalDecay fails on dated files in `memory/dreaming/` subdirectories.
- [#116010](https://github.com/openclaw/openclaw/issues/116010) — All persistent sessions capped at 128k context regardless of model.
- [#78493](https://github.com/openclaw/openclaw/issues/78493) — `sudo openclaw update` creates mixed ownership; later `doctor` overwrites config.

**Good News:**
- Old P1 bugs are being resolved: [#109490](https://github.com/openclaw/openclaw/issues/109490) (codex turn interruption) closed as duplicate; [#112246](https://github.com/openclaw/openclaw/issues/112246) (session-key tombstone bricking GPT sessions) fixed; [#111969](https://github.com/openclaw/openclaw/issues/111969) (foreground reply fence unbounded wait) fixed; [#79451](https://github.com/openclaw/openclaw/issues/79451) (tools.deny not enforced) is *closed as stale*, which is concerning unless the fix landed elsewhere.

## 6. Feature Requests & Roadmap Signals

Requests indicate a focus on **operational control, deeper integration, and UX polish.**

- **Testing & Verification:** `/models test-fallback` command ([#6599](https://github.com/openclaw/openclaw/issues/6599)) — a clear ops feature to validate fallback chains without real failures. High value; likely candidate given community demand.
- **Documentation:** Kubernetes deployment ([#91455](https://github.com/openclaw/openclaw/issues/91455)) and explicit SecretRef `provider: "default"` docs ([#121083](https://github.com/openclaw/openclaw/issues/121083)). "Good first issue" type PRs, likely in next version.
- **Security & Scoping:** Per-agent MCP server scoping ([#72591](https://github.com/openclaw/openclaw/issues/72591)) — a major resource optimization (120 processes → fewer) and security improvement. This has long legs and is a strong candidate for a future major release.
- **i18n:** Slash command description translations ([#79458](https://github.com/openclaw/openclaw/issues/79458)) — specific to Chinese-speaking users, suggests a growing international community.
- **Global pre-routing interception** ([#109353](https://github.com/openclaw/openclaw/issues/109353)) — a powerful plugin API enhancement, closed as duplicate, so the core ask is tracked elsewhere.
- **UI Redesign:** UX scoring-based quality update ([#75947](https://github.com/openclaw/openclaw/issues/75947)) — a broad ask that will likely be addressed incrementally (e.g., the collapsible Workboard columns from PR #128115).

**Prediction:** The next version will likely include the install policy acknowledgement flows (both CLI and UI), the gateway delivery-scoping fix, and foundational work on session-state and message-delivery reliability (multiple P1s have linked PRs). MCP per-agent scoping and the `sessions_send` synchronous wait option ([#115400](https://github.com/openclaw/openclaw/issues/115400)) are strong "next major" features.

## 7. User Feedback Summary

- **Pain Point: Message Delivery Fragility** — Highest volume of complaints. Issues range across channels (Telegram, WhatsApp, Slack, QQBot, Discord) with replies generated but not delivered, stuck states, and blank bubbles. The underlying need is **guaranteed, durable, cross-platform message delivery**, especially for long-running or multi-agent turns.
- **Pain Point: Session-State Mysteries** — Several issues report unexpected context drops ([#108215](https://github.com/openclaw/openclaw/issues/108215)) and inflation ([#125333](https://github.com/openclaw/openclaw/issues/125333)), plus session-key binding drift ([#101672](https://github.com/openclaw/openclaw/issues/101672)). Users need **predictable, transparent, and stable session memory behavior**.
- **Pain Point: A2A Complexity** — The `sessions_send`/`sessions_yield`/`sessions_spawn` pattern is powerful but confusing and error-prone (duplicate messages, silent webchat delivery, missing transcripts, no sync wait). Users clearly want a **robust, well-documented multi-agent orchestration primitive**.
- **Satisfaction Signals:** The community is highly engaged and technical (agents filing issues on behalf of users, e.g., #124911). The release-validation process indicates a rigorous engineering culture.
- **Provider Pain:** DeepSeek deprioritization ([#121953](https://github.com/openclaw/openclaw/issues/121953)) and Codex OAuth timeout ([#89278](https://github.com/openclaw/openclaw/issues/89278)) show users are on multiple backends and expect uniform behavior. The "off-meta" issue ratings suggest the team is aware of these long-tail concerns.

## 8. Backlog Watch

These items are long-running, important, and appear to lack a clear path to resolution:

- **A2A `sessions_send` duplicate messages** ([#39476](https://github.com/openclaw/openclaw/issues/39476), open since March 2026, 12 comments) — A core architectural issue. No linked PR. The `dedupe:parent` label may indicate it's a tracking issue, but its longevity is concerning.

- **Codex app-server mid-turn client close** ([#86214](https://github.com/openclaw/openclaw/issues/86214), open since May 24, 8 comments) — `needs-maintainer-review`, `needs-product-decision`, `needs-info`. Untriaged for 3 months.

- **`sudo openclaw update` ownership mess** ([#78493](https://github.com/openclaw/openclaw/issues/78493), open since May 6, 6 comments) — `needs-maintainer-review`, `needs-product-decision`, `needs-live-repro`. A confusing mix of requests; needs a decisive call on supported update paths.

- **`tools.deny` not enforced for claude-cli backend** ([#79451](https://github.com/openclaw/openclaw/issues/79451)) — **Closed as stale** despite being a security issue. This is a red flag. The `needs-security-review` tag and the description clearly indicate a security boundary violation. If this was closed without a fix, it needs urgent reopening. **This is the most important item in this section.**

- **Native Windows CLI Scheduled Task failure** ([#91144](https://github.com/openclaw/openclaw/issues/91144), open since June 7, 7 comments) — `source-repro`, `linked-pr-open`. The linked PR seems to be in progress, so this may be resolved soon.

- **Remote Windows node no `node_exec` surface** ([#106203](https://github.com/openclaw/openclaw/issues/106203), open since July 13) — `not-repro-on-main`. Needs a clear repro or a decision to close.

- **Compaction `reserveTokensFloor` ignores model context** ([#124911](https://github.com/openclaw/openclaw/issues/124911), filed by Scott Hanselman's agent) — A well-analyzed P2 that points to a clear code improvement. `needs-maintainer-review` and `needs-product-decision`; this could be a quick win.

---

**Overall Project Health Assessment:** OpenClaw is in a **high-activity, pre-stable-release** state. The large open issue count (456 open) and substantial P1/P0 backlog are typical for a project this scale pre-release. The core risks are the **critical, unresolved P0s** (SQLite corruption, iOS breakage, totalTokens inflation) and the **un-addressed security regression** (tools.deny). The team is shipping fixes quickly, but the sheer volume of session-state and message-delivery bugs suggests a structural weakness in that layer that may need a dedicated refactor (similar to the SQLite storage rework that introduced some of these regressions). Positive signals include a healthy release-validation process and a very active, technically sophisticated community.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date: 2026-08-24 | Coverage: 12 Projects**

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is in a **high-velocity pre-stable maturation phase**, characterized by intense bug-fixing, security hardening, and architectural refactoring across major projects. Key themes dominating the ecosystem: **session-state reliability** (context drops, message delivery failures, SQLite corruption), **provider-agnostic behavior** (OAuth refresh, fallback chains, message formatting quirks), and **multi-agent orchestration primitives** (sessions_send/yield/spawn, A2A protocol). The ecosystem is bifurcating: flagship projects (OpenClaw, Hermes Agent, ZeroClaw) are shipping large-scale infrastructure changes with extensive RFC processes, while mid-tier projects (NanoBot, IronClaw, PicoClaw) are executing focused technical debt reduction and targeted security fixes. Newer entrants (TinyClaw, ZeptoClaw) show no activity, suggesting consolidation or abandonment. An emergent pattern is the **automated triage of user feedback into actionable GitHub issues** (IronClaw, Hermes Agent), indicating a shift toward data-driven product development. **No project shipped a stable release in the last 24 hours**, — all are in active beta or maintenance validation.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score | Notes |
|---|---|---|---|---|---|
| **OpenClaw** | 500 updated | 96 merged/closed | v2026.8.1-beta.2 (validation) | **7/10** | High activity but 3 unresolved P0s; security regression (tools.deny) closed as stale |
| **Hermes Agent** | 50 updated / 18 closed | 50 updated | v0.20.5 | **7/10** | P1 update-destroy bug; tool-result loss cluster; good triage speed |
| **NanoBot** | 2 (1 closed, 1 new) | 19 (5 merged) | No release | **8/10** | Clean, maintainer-driven; fast bug-to-fix cycle; config unification incoming |
| **ZeroClaw** | 50 updated / 12 closed | 50 updated / 5 closed | v0.8.4 Alpine | **7/10** | RFC-heavy governance; merge bottleneck; filesystem listener bug fixed |
| **IronClaw** | 9 updated | 23 updated / 5 merged | v1.4.0 milestone (in progress) | **7/10** | CI-expedite program (T1-T4); sandbox epic advancing; extension install regression |
| **PicoClaw** | 2 closed (stale) | 7 (5 merged) | No release | **8/10** | Maintenance/consolidation; SSRF fixes across all channels; WhatsApp unblocked |
| **NanoClaw** | 6 updated | 50 (20 merged) | v2.3.0 imminent | **7/10** | Stacked PR chains; macOS-specific stability issues; hardened install breakage |
| **CoPaw** | 6 updated (3 new) | 8 merged + 7 open | No release | **7/10** | Memory leak (20.7GB) high severity; task-replay bug; strong skill-system progress |
| **Moltis** | 3 updated | 6 open (0 merged) | No release | **6/10** | Fix pipeline active; 6-month-old TLS/WebSocket bug (critical) unaddressed |
| **LobsterAI** | 4 closed (all stale) | 3 merged | No release | **7/10** | Cleanup day; security issue (model key leak) closed without visible fix |
| **NullClaw** | 1 (new) | 0 | No release | **6/10** | Single but serious MCP stdio deadlock issue |
| **TinyClaw** | 0 | 0 | No release | **5/10** | Inactive |
| **ZeptoClaw** | 0 | 0 | No release | **5/10** | Inactive |

**Health Score Legend:** 10=Excellent, 8-9=Good, 6-7=Moderate (needs attention), 5=Concerning

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**

- **Dominant Community Scale**: 500 issues/PRs updated in 24h vs. 50 for nearest competitors (Hermes Agent, ZeroClaw). The community is 10x more active, providing a massive feedback loop and contributor pipeline.
- **Release Process Rigor**: Formal validation process (v2026.8.1-beta.2) with dedicated issues is the most mature testing methodology in the ecosystem.
- **Architecture Breadth**: A2A protocol, multi-agent bindings, and the `sessions_send/yield/spawn` orchestration pattern are more advanced than peers (only ZeroClaw's RFC process approaches this).
- **Security Boundary Development**: Shipment of install-policy acknowledgement flows and transcript credential opt-out signals strong security posture awareness.

**Technical Approach Differences:**

- **Heavy on agent/process lifecycle management**: `sessions_*` APIs, gateway delivery scoping, and subagent lifecycle management are more deeply integrated than in peers.
- **SQLite-backed storage** (now subject to P0s) — NanoBot uses local SQLite too, but OpenClaw has a larger surface area and more complex failure modes.
- **UI-heavy operational console** (Control UI, Workboard) — contrasts with NanoBot/CoPaw's lighter WebUI/TUI approaches.

**Community Size Comparison:**

| Metric | OpenClaw | Hermes Agent | NanoBot | ZeroClaw |
|---|---|---|---|---|
| Issues active | 456 | ~50-100 (est.) | ~10 | ~50-100 (est.) |
| Community engagement (comments/24h) | >100 | >30 | <5 | >30 |
| Maintainer bandwidth | Strained (large `clawsweeper` backlog) | Responsive (hourly PR closures) | Healthy (small, focused queue) | Bottleneck (RFC decision queue #8692) |

**Bottom Line:** OpenClaw is the ecosystem's "mainline" project with the most users, the most advanced multi-agent features, and the greatest architectural complexity. Its current risk is **reliability** — the three unresolved P0s and the `tools.deny` security regression could erode user trust if not addressed by stable release.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging independently across multiple projects (indicating ecosystem-wide industry needs):

| Focus Area | Projects (Specific) | Specific Need |
|---|---|---|
| **Message Delivery Durability** | OpenClaw (#126246 Telegram stuck, #127948 WhatsApp blank), NanoClaw (#3457 UNIQUE-constraint), Moltis (#1224 Slack shared channel), PicoClaw (#3320 WhatsApp 405) | Guaranteed, persistent message delivery with retries; idempotency for duplicate messages |
| **Session-State Stability** | OpenClaw (#125333 totalTokens inflation), Hermes Agent (#91276 session-not-found cluster, #93251 tool-result loss), CoPaw (#7217 task replay after stop), NanoBot (turn recovery PR) | Predictable, transparent session memory; no data loss across restarts; instrumented context transparency |
| **MCP Client Lifecycle & Security** | OpenClaw (#72591 per-agent scoping), NullClaw (#991 MCP deadlock), Moltis (#1231 MCP client dispatch), PicoClaw (#3302 OAuth 2.1 MCP) | Configurable timeouts, lock-free concurrent connections, scope-aware permissions, modern auth |
| **Update Reliability** | OpenClaw (#78493 ownership mess), Hermes Agent (#83529 update destroys CLI, #91115 macOS keychain), NanoClaw (#3498 update fails macOS, #3496 hardened install breakage) | Non-destructive, well-tested update paths; cross-platform consistency |
| **Context/Compaction Correctness** | OpenClaw (#108215 context drops, #111857 CLI budget reopens), Hermes Agent (compression refinements), NanoClaw (context window settings) | Predictable context management; accurate token accounting; no surprise compaction |
| **Security Regression Prevention** | OpenClaw (#79451 tools.deny closed stale), PicoClaw (SSRF fixes #3322-3324), LobsterAI (#1202 model key leak), Moltis (#1230 fail-closed hooks) | Prompt-injection resistance; denial-of-service protection; secure default configs |
| **Provider Uniformity** | OpenClaw (#121953 DeepSeek cron stalls, #89278 Codex OAuth), CoPaw (#7218 long-inference timeout mismatch), IronClaw (provider extension/auth issues) | Consistent behavior regardless of backend; documented per-provider quirks; proper timeout handling |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target Users | Architectural Approach | Distinct Identifier |
|---|---|---|---|---|
| **OpenClaw** | Multi-agent orchestration, heavyweight infra | Power users, developers, teams needing complex workflows | Rich A2A protocol, `sessions_*` APIs, SQLite storage, UI-heavy Control | Language-agnostic agent fabric |
| **Hermes Agent** | Stabilization, Bot Mode, desktop-first | End users on desktop (Electron), bot developers | Lifecycle guards, profile-aware gateway, desktop TUI | The "reliable daily driver" |
| **ZeroClaw** | RFC-driven architectural evolution, governance | Organizations needing formal change control | WASM plugin architecture (RFC), Rust-based, strict RFC process | The "governed enterprise agent" |
| **NanoBot** | Lightweight, developer-friendly, UX polish | Developers and small teams; lightweight self-hosters | Multi-provider (OpenAI, Codex, Linear), WebUI + TUI, active PR culture | The "clean and fast prototype" |
| **IronClaw** | Sandboxing, egress control, extensions | Security-conscious enterprises, Rust community | Persistent per-user sandboxes, proxy-mediated credentials, Rust/Wasm | The "secure multi-tenant sandbox" |
| **PicoClaw** | Security hardening, channel breadth | Users needing many messaging channels | Focused SSRF protection, native WhatsApp, Channel-agnostic HTTP clients | The "channel robustness specialist" |
| **NanoClaw** | Chat SDK integration, installation reliability | Developers embedding chat into products | Chat SDK 4.32.0 lockstep, typed indicator lifetime, image repinning | The "SDK-first embedder" |
| **CoPaw** | Skill system, agent lifecycle management | Users of the Qwen ecosystem | Dynamic skill loading, auto-title-sync, context-window tracking | The "skill-centric agent" |
| **Moltis** | Memory subsystem, connector reliability | Users needing robust local memory | Embeddings bounds, MCP lifecycle fixes, WhatsApp document ingestion | The "memory-safe agent" |
| **LobsterAI** | NIM/NetEase integration, UI/UX | Chinese-speaking users, NetEase ecosystem | Model settings, agent management UI, NIM-specific fixes | The "NIM-native agent" |
| **NullClaw** | Lightweight, homelab-friendly | Homelab operators (Proxmox) | Minimal daemon, MCP bridges, low resource usage | The "self-hosted tinkerer's agent" |

---

## 6. Community Momentum & Maturity

**Tier 1 — High-Velocity Iteration (Active development, multiple fronts):**

- **OpenClaw** — Shipment machine; 500+ issues/PRs daily, beta validation, but P0 risk could stall release.
- **Hermes Agent** — Rapid fix cycle; closing clusters efficiently. Desktop + Bot Mode is a growth vector.
- **ZeroClaw** — High RFC activity, but merge bottleneck creates a "brainstorming > shipping" dynamic.
- **NanoClaw** — Core-team sprint; high PR throughput with stacked chains. macOS issues are a near-term risk.
- **CoPaw** — Strong contributor onboarding (multiple first-time contributors merged). Feature velocity high but stability concern (#7222 memory) could negate gains.

**Tier 2 — Stabilizing / Consolidating (Focused but slower):**

- **NanoBot** — Small, maintainer-led, low community noise. Focused on config unification and provider fixes. Healthy with low churn.
- **IronClaw** — CI-expedite program (T1-T4) suggests heavy internal process work; extension install regression is a user-facing concern.
- **PicoClaw** — Stale-issue cleanup + security hardening; appears to be in a pre-release stabilization phase.
- **Moltis** — Fix pipeline is active but the underlying TLS/WebSocket issue is a 6-month gap that undermines reliability narrative.
- **LobsterAI** — Maintenance mode this cycle; security issue (#1202) closure without a fix is a negative signal.

**Tier 3 — Inactive (No Activity in 24h):**

- **TinyClaw** — No signals.
- **ZeptoClaw** — No signals.

**Momentum vs. Stability:** Most projects favor iteration speed over wait-and-fix discipline. Only NanoBot and PicoClaw demonstrate a conservative, "fix-then-ship" cadence.

---

## 7. Trend Signals

1. **Cross-Platform Reliability is a Top Priority (Strong Signal)** — Multiple P1 bugs across OpenClaw (Telegram, WhatsApp, Slack), PicoClaw (WhatsApp), and Moltis (Slack) show that **guaranteed message delivery is the #1 pain point**. Agent frameworks must treat each channel as a first-class citizen with durable retries, idempotent sends, and typed failure notifications.

2. **MCP is Becoming the Universal Integration Layer — with Concurrency Issues** — NullClaw (#991) and Moltis (#1231) are hitting lock contention and stale client dispatch during MCP server restarts. The ecosystem needs a **standardized MCP client lifecycle** with configurable timeouts, shared/read-only modes, and robust reconnection semantics.

3. **Security is Shifting from "Policy" to "Enforcement"** — The OpenClaw `tools.deny` regression and LobsterAI model-key leak show that **tool-level access control is not the default**. Expect a wave of "secure-by-default" hardening in the next release cycle (fail-closed hooks in Moltis #1230, sandboxing in IronClaw #7810).

4. **Context Management is a "Killer Feature" Gap** — The frequency of `totalTokens` inflation, compaction loops, and silent drops (OpenClaw, Hermes Agent, CoPaw) indicates that **accurately predicting and exposing context usage** is a frontier problem. Most frameworks are still opaque to users; the winning framework will ship a **developer-visible context debugger**.

5. **Update Mechanisms are an Emerging Trust Boundary** — The cluster of "update destroyed my setup" bugs (Hermes #83529, NanoClaw #3498, OpenClaw #78493) suggests that **self-update routines are consistently under-tested**. Reliable updates (atomic swaps, rollback, Windows/macOS specifics) are becoming a table-stakes feature.

6. **Automated Feedback Triage is the Next Productivity Lever** — IronClaw's automated pipeline converting Slack feedback into GitHub issues, and Hermes Agent's aggressive duplicate closure, signal that **data-driven issue triage** is emerging as a practice. This reduces maintainer cognitive load and ensures user pain points are tracked.

7. **Provider Uniformity is a Growing Demand** — Users on DeepSeek, Codex, and OAuth-heavy providers are hitting framework-level quirks (OpenClaw #121953, CoPaw #7218). Frameworks that **abstract away provider differences** (via a common message/normative layer) will win over operating on multiple backends.

---

**Final Takeaway:** This ecosystem is maturing from "what can agents do?" to "how do we make agents not fail?" The next release cycle will likely be defined by reliability improvements (durable delivery, stable context, tool-trust boundaries) rather than new agent capabilities. Developers selecting a framework for production should weight **delivery guarantees, update safety, and MCP concurrency resilience** over feature richness, as these are proven pain points across all major projects today.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date: 2026-08-24**

---

## 1. Today's Overview

NanoBot shows robust development activity over the last 24 hours with 19 pull requests updated (14 open, 5 closed/merged) and 2 issues (1 closed, 1 new). The project maintains a steady pulse with significant work converging around provider layer refactoring, WebUI fixes, and configuration experience improvements. The 4:1 PR-to-issue ratio indicates a healthy, maintainer-driven development cadence with contributors actively self-organizing around stability and UX. Notably, multiple PRs share overlapping concerns (configuration contracts, agent loop lifecycle), suggesting active coordination. No new releases were published in this window.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

Five pull requests were closed/merged, advancing several key areas:

- **[PR #5420 – Turn Recovery (merged)]** – Adds user-controlled turn recovery for interrupted WebSocket sessions: persists a narrow sidecar checkpoint, exposes explicit **Continue/Dismiss** actions in WebUI and TUI (no auto-resume), and restores final answers without re-invoking the model. This is a meaningful reliability feature for long agentic turns. *(closed 2026-08-23)*

- **[PR #5491 – WebUI Reasoning Shell Fix (merged)]** – Fixes a rendering/information-architecture bug where assistant answer text was being placed inside the reasoning/activity shell. Now merges answer slices into one clean final message while keeping reasoning/tool activity separate, preserving fork boundaries and media-only answers. *(closed 2026-08-23)*

- **[PR #5492 – Process Identity Naming (merged)]** – Names Python CLI processes by role (`nanobot-agent`, `nanobot-webui`, `nanobot-gateway`) and renames the Bun child to `nanobot-tui`. Improves process monitoring and debugging for operators. *(closed 2026-08-23)*

- **[PR #5445 – Docker OAuth Persistence (merged)]** – Fixes a critical Docker issue: OAuth client data now persists to the mounted instance directory (instead of ephemeral XDG paths) and remains writable after dropping to the non-root user. Directly addresses the previously reported login bug. *(closed 2026-08-23)*

- **[PR #5475 – Dead Code Removal (merged)]** – Removes zero-consumer helpers, unread state, ineffective config fields, and the unused `websocket-client` dependency; narrows exports to used symbols. Reduces surface area and maintenance burden. *(closed 2026-08-23)*

---

## 4. Community Hot Topics

Notably, all PRs and issues in this window have **zero reactions** and minimal comment activity, indicating a development-led rather than community-discussion-led cycle. The two issues with comments stand out:

- **[Issue #5444 – OpenAI OAuth Login Failure (2 comments, closed)](https://github.com/HKUDS/nanobot/issues/5444)** – The most-discussed item. User `Bennett-Yang` reported failing to complete OAuth login in Docker. **Fixed** by the merged PR #5445. A clean bug-report → fix cycle; the two comments likely reflect triage/diagnosis discussion.

- **[Issue #5493 – File Preview Enhancement (new, 0 comments)](https://github.com/HKUDS/nanobot/issues/5493)** – Requests native preview for HTML, .txt, and .md documents via a secure `iframe` + `srcdoc` approach. No maintainer response yet; this is a fresh feature request with a concrete proposal.

**Analysis:** The bug report demonstrates that issue reports are actionable and lead directly to fixes. The preview request reflects a growing user base relying on NanoBot channels for document workflows. Both signals show a project where maintainers respond quickly.

---

## 5. Bugs & Stability

Two issues/PRs address stability concerns, ranked by severity:

**High Severity:**
- **[Issue #5444 – OAuth login failure in Docker (closed)](https://github.com/HKUDS/nanobot/issues/5444)** – Authentication pipeline broken for containerized deployments. **Resolved** via PR #5445 (OAuth client data persistence).

**Medium Severity (fixes in flight):**

- **[PR #5500 – TLS context reuse for Codex provider](https://github.com/HKUDS/nanobot/pull/5500)** – Root cause: a 10-second unresponsiveness traced to constructing a fresh TLS context on every request (performance regression). Fix caches verified/fallback contexts per provider instance. *Open, not yet merged.*

- **[PR #5496 – Timeout gap for no-tools model requests](https://github.com/HKUDS/nanobot/pull/5496)** – `AgentRunner` only guarded `_request_model()` with wall-clock timeouts; no-tools fallback paths (malformed-call recovery, etc.) called the provider directly without protection, risking stalled turns. *Open, not yet merged.*

**Low Severity:**
- **[PR #5499 – Empty session persistence in TUI](https://github.com/HKUDS/nanobot/pull/5499)** – Opening the TUI in a new folder could save empty/abandoned sessions; fix keeps metadata transient until the first real message.

---

## 6. Feature Requests & Roadmap Signals

The strongest signal is **configuration experience unification** across two stacked PRs aimed at the next minor release:

- **[PR #5497 – Shared complete config editor contract](https://github.com/HKUDS/nanobot/pull/5497)** – A transport-neutral, full-schema editor contract with secret-safe handling and explicit replacement/clearing. Shared with existing WebUI storage.
- **[PR #5498 – Unified onboarding in Agent TUI](https://github.com/HKUDS/nanobot/pull/5498)** – Layers a schema-driven `/config` surface onto the Agent OpenTUI with searchable advanced settings, plus preserved onboarding flow.

Additional signals:

- **[PR #5495 – Native Linear agent channel](https://github.com/HKUDS/nanobot/pull/5495)** – Adds OAuth + PKCE, webhooks (deduplicated SQLite queue), and a WebUI setup flow. Indicates expansion beyond chat platforms into project-management tooling.
- **[Issue #5493 – Document preview (html/txt/md)](https://github.com/HKUDS/nanobot/issues/5493)** – User-supplied solution (iframe + srcdoc) aligns with existing sandboxing patterns; high likelihood of implementation.
- **[PR #5388 – Budget MCP tool schemas](https://github.com/HKUDS/nanobot/pull/5388)** – Opt-in byte budget for model-visible MCP schemas; addresses context-window efficiency for agent loops.

**Prediction:** Next feature release will likely ship the unified configuration editor (both PRs), the Linear channel, and potentially a first pass at document preview.

---

## 7. User Feedback Summary

Only two direct user signals this window:

- **Pain point (resolved):** Docker-based OAuth login was broken, blocking all authenticated workflows. User reported symptoms clearly; fix landed same week. High satisfaction expected given speed of resolution.
- **Feature desire (open):** A user wants native preview for HTML/txt/md documents, citing convenience. They also proposed a concrete secure implementation, suggesting technical confidence in the platform.

**Underlying themes:** Users are running NanoBot in production-like Docker deployments and are pushing it toward richer document and project-management workflows. The proposed solution quality suggests an experienced developer audience comfortable proposing architecture-level changes.

Overall, there is no visible dissatisfaction; activity is quiet but constructive.

---

## 8. Backlog Watch

Items requiring maintainer attention due to age or staleness:

- **[PR #5152 – Subagent partial completion results (open since 2026-07-28)](https://github.com/HKUDS/nanobot/pull/5152)** – 27 days without merge. Addresses a correctness issue: sibling tasks still running when a subagent announces results. Could block or confuse agent workflows. Needs review/decision.

- **[PR #5385 – Matrix Element SAS request flow (open since 2026-08-13)](https://github.com/HKUDS/nanobot/pull/5385)** – Adds modern Element verification flow support. Not merged; may be waiting on cryptographic review or test coverage.

- **[PR #5386 – MCP Apps result metadata (open since 2026-08-13)](https://github.com/HKUDS/nanobot/pull/5386)** – Preserves structured app result data separately from model text. Complex change; likely needs design review on how rich results interact with the agent loop.

- **[PR #5388 – MCP schema budget (open since 2026-08-13)](https://github.com/HKUDS/nanobot/pull/5388)** – Opt-in feature; non-urgent but adds configuration surface. Should be aligned with the new unified config contract (PRs #5497/#5498) before merging.

**Note:** These PRs are feature-rich but not directly blocking; the project’s remaining backlog appears well-triaged.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-24

**Source:** github.com/nousresearch/hermes-agent | **Data:** Issues/PRs updated Aug 23–24, 2026

---

## 1. Today's Overview

Hermes Agent is in a period of intensive stabilization. While no new releases shipped, 50 issues and 50 PRs were updated in the last 24 hours—a very high activity level. The project is currently dominated by two distinct workstreams: a sprawling bug-fix effort around session state and gateway lifecycle management (particularly for Bot Mode and multi-profile setups), and a series of quality-of-life fixes targeting the CLI, desktop app, and sandboxing backends. The open-to-closed issue ratio (32:18) is healthy, indicating maintainers are triaging and closing duplicates and confirmed fixes while new reports continue to flow in. Notably, the most recently filed issues (Aug 24) are receiving attention within hours, suggesting good maintainer responsiveness.

## 2. Releases

No new releases were published in the last 24 hours. The latest known version remains v0.20.5 (2026.8.19) with the desktop bundle at 0.17.0, as referenced in several issue reports.

## 3. Project Progress

While 49 PRs remain open, the following high-impact fixes were merged or reached closure today:

- **Session state cluster (the #91276 cluster):** PR #93361 consolidates a major fix for the "session-not-found" storm. It ensures desktop sessions survive gateway restarts, sleep/wake cycles, and WebSocket drops, and prevents the reap-storm bug where sessions would be stranded or aggressively reaped (8 salvaged fixes from the cluster).
- **Cron lifecycle guard hardening:** A series of PRs and issues focused on `lifecycle_guard.py`, which blocks cron jobs from restarting/stopping the Hermes gateway. Multiple false-positive bugs (prose in referenced data files #92372, absolute paths #86010, multi-line python #85557) were closed, alongside gaps like a missing `launchd bootout` verb #80260 and a `hermes -p <profile> gateway stop` bypass #78028.
- **Multi-profile / Bot Mode reliability:** PR #93369 addresses stranded bot sessions in the default store on profile resume, and #93361 routs RPCs to the correct session owner. PRs #93372 and #93373 fix desktop group disbanding leaving stale "0 bots" roster rows.
- **Infrastructure and security:** PR #93374 prevents `hermes backup` from failing on the gateway Unix socket (introduced by #92447). PR #93033 (open) makes `hermes update` exit non-zero when the upstream pull fails—currently it reports a successful no-op with exit 0.

## 4. Community Hot Topics

The most active items (by comment count) reveal deep, systemic pain points:

- **#66616 — Skills index stale/degraded (84 comments, open since Jul 18):** An automated freshness probe reports the Skills Hub index is consistently behind schedule (29.8h old vs. a 26h limit). This is a long-running source of frustration—essentially a watchdog that keeps firing without a durable fix. The underlying need is reliable, up-to-date documentation infrastructure.

- **#83529 — `hermes update` destroys hermes (9 comments, P1):** A catastrophic update failure on Debian Trixie where the CLI became non-functional after an update. This is the highest-severity user-facing bug today and is critical to resolve for user trust.

- **#91115 — macOS keychain prompt after update (7 comments, P2):** A subtle Electron/safeStorage bug where ad-hoc re-signing of the desktop app after every update invalidates the keychain ACL, causing repeated password prompts. Users want a frictionless update cycle.

- **#93091 — Bot Mode reliability program (7 comments, P3):** A feature request cluster covering typed failure reasons, envelope TTL, attention badges, and retry policies. This signals that Bot Mode is a strategic focus with real multi-bot coordination gaps.

- **#64392 — Duplicate skill names handled inconsistently (6 comments, P2):** `skills list`, the system prompt builder, and `skill_view` all interpret duplicate skill names differently. This is a latent correctness bug that can confuse both users and the model.

**Underlying needs:** Users demand a CLI that cannot self-destruct (update reliability), a desktop experience that respects platform security (keychain), and an agent that can reliably coordinate itself across sessions, skills, and platforms without silent failures.

## 5. Bugs & Stability

Ranked by severity as reported today:

| Severity (P1) | Bug | Fix PR? |
|---|---|---|
| P1 | **#83529 — `hermes update` destroys hermes** (Debian Trixie, CLI broken post-update) | No PR linked yet |
| P1 | **#93251 — Parallel tool batch of ≥4 calls loses ALL results** ('Result unavailable' for every call; batch of 1–3 works) | No PR linked yet |
| P2 | **#93345 — Desktop Bot Mode: remote group deletion leaves 0-bot roster row** (sessions layer dirty) | #93372, #93373 (open) |
| P2 | **#93349 — Gateway service identity collides across HERMES_HOME roots** (launchd/systemd name collision) | No PR linked yet |
| P2 | **#93087 — Malformed SQLite schema escapes WAL-reset probe** (persistence silently disabled) | Closed (fix verified) |
| P2 | **#55626 — mnemosyne_recall/cronjob list return [Result unavailable]** (persistent tool-result drop) | Closed (duplicate of #63000) |
| P2 | **#63000 — Composite tool_call ids (`call_xxx\|fc_yyy`) drop results** (OpenAI-compatible bridges) | Closed (fixed) |
| P3 | **#93364 — npm audit: nanoid <3.3.18 DoS vuln blocked by peer-dep conflict** | No PR linked yet |
| P3 | **#93263 — Config keys silently dropped by normalization** (umbrella: 14 issues, 6-PR swarm) | Multiple PRs in flight |

**Notable:** The "tool results dropped" class (#93251, #55626, #63000) is a recurring, high-severity failure mode. #63000 was closed today, but #93251 is a fresh P1 in the same family, suggesting the fix may be incomplete.

## 6. Feature Requests & Roadmap Signals

- **Bot Mode reliability program (#93091):** Types for failure reasons, event TTL, attention badges, and leader-routed group rooms. Given the concurrent fix PRs (#93369, #93372, #93373), Bot Mode is clearly an active investment area and these reliability features may land within one or two releases.

- **Lifecycle deletion for completed ephemeral agent sessions (#93341):** Request to auto-prune child sessions after results are delivered. This fits the broader session-hygiene theme and may be picked up by the sweeper for `risk-session-state`.

- **Expose cron run history over HTTP (#93365, PR open):** Likely to land next version—it's already implemented and waiting review.

- **Model description in selection tab (#93360):** A small UX ask with no controversy; probable quick win.

- **Cron failure lifecycle hook (#82353, PR #82901 open):** Add `cron_job_failed` event for reactive consumers. Strong fit with the automation-focused sweeper.

**Prediction:** The next minor release (v0.21.0) will likely include the Bot Mode session fixes (#93361, #93369), the cron lifecycle hook, and the update-failure exit code fix (#93033), alongside the ongoing compression and lifecycle-guard refinements.

## 7. User Feedback Summary

- **Pain: Update anxiety.** Two distinct reports (#83529, #91115) describe post-update breakage (CLI self-destruct and keychain prompts). Users on Debian and macOS are being burned by the update path, which is a trust-critical surface.
- **Pain: Silent configuration failures.** The config-key normalization bug (#93263-umbrella) and Langfuse placeholder keys (#92984) show users' settings are being silently ignored, wasting time and eroding confidence.
- **Pain: Tool-result loss.** The "Result unavailable" reports (#93251, #55626) describe the agent losing its own work—a fundamentally trust-breaking experience.
- **Satisfaction:** The rapid closing of duplicate issues and the speed of fix PRs (e.g., #93373, #93372 for #93345) suggest the maintainers are responsive and the sweeper system is working.
- **Frustration:** The skills index watchdog (#66616) has been "degraded" for over a month with 84 comments—a documentation-quality measurement that is itself degrading. This is an internal tooling annoyance that should be prioritized.

## 8. Backlog Watch

These items are older or have been open for a while and require maintainer attention:

- **#66616 — Skills index is stale (84 comments, open since Jul 18):** Long-running and extremely noisy. Needs either a real fix or a re-scoped threshold, not just more watchdog alerts.
- **#89964 — Lifecycle guard bypass via indirect execution (systemd-run, at, setsid):** Open since Aug 19. The guard is a security boundary (preventing gateway self-restarts via cron) and the issue correctly identifies that per-vector argv branches are incomplete. The suggested unified self-target check is the right direction and should be scoped.
- **#93364 and #91931 — Vulnerable transitive dependencies (nanoid, Python deps):** Both are open with no fix PR. #91931 has been open since Aug 22 and is security-relevant.
- **#64392 — Duplicate skill names inconsistent (open since Jul 14):** A long-standing correctness issue with unclear ownership across `skills list`, the prompt builder, and `skill_view`. Needs a decision on canonical handling.
- **#85388 — DeepSeek peak/off-peak pricing (open since Aug 13):** High user impact for cost tracking; the date for the new rate card is 2026-08-16, which has already passed. This PR is time-sensitive and should be prioritized.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Based on the GitHub data for PicoClaw (github.com/sipeed/picoclaw) on 2026-08-24, here is the project digest:

---

# PicoClaw Project Digest — 2026-08-24

## 1. Today's Overview
PicoClaw saw a moderate level of activity today, with 2 issues and 7 PRs updated. Notably, all 2 issues were closed (both stale), and 5 PRs were merged or closed, indicating a cleanup of older items. No new releases were published, and no new issues were opened today, suggesting the project might be in a maintenance and consolidation phase. The active work is focused on security hardening (SSRF fixes), performance optimization (prefix caching), and dependency updates, alongside a couple of new feature experiments.

## 2. Releases
**None.** There were no new releases published in the last 24 hours. Projects relying on the latest fixes will need to track commits on the main branch until the next official tag.

## 3. Project Progress
The project saw 5 PRs merged/closed, reflecting strong progress on stability and security:

- **fix(channels): block private targets on inbound media downloads (#3322)** — This is a significant security fix. It extends SSRF protection (already used in the OneBot channel) to QQ, Telegram, Discord, LINE, and Slack, preventing crafted media URLs from reaching loopback or private network hosts.
- **fix(weixin): use CreateSafeHTTPClient for media downloads (#3324)** & **fix(wecom): use CreateSafeHTTPClient for media downloads (#3323)** — These are sibling fixes to #3322, applying the same secure HTTP client logic to the Weixin and WeCom channels.
- **fix(agent): move dynamic context after history to preserve prefix caching (#3321)** — A performance optimization. Moving the dynamic context block after the conversation history keeps the prefix cache valid, improving performance and reducing token costs for repeated requests.
- **fix(deps): bump whatsmeow to unblock WhatsApp "client outdated (405)" (#3320)** — A critical dependency bump that unblocks the native WhatsApp channel, fixing a connectivity issue where the socket was being dropped and not reconnecting.

## 4. Community Hot Topics
While no new issues were created today, the most notable activity is around the closed items that previously generated discussion:

- **#3302 Support OAuth 2.1 for MCP servers** — (4 comments) — Despite being closed as stale, this feature request targets modernizing MCP server authentication. The desire for OAuth 2.1 indicates a push for more secure, standardized auth flows, aligning with broader industry trends.
- **#3325 Render Telegram tables with rich messages** — (2 comments) — Closed as stale, this request focuses on improving visual quality in Telegram by using native table UIs instead of plain text. This highlights a user desire for better rendering fidelity across messaging platforms.
- **PR #3344 Add Build Remote Agent phone pairing (gbr/1)** — This open PR is a new experimental feature that allows a phone to pair with and spectate the desktop agent, expanding remote use cases for PicoClaw.

## 5. Bugs & Stability
Several significant bugs were addressed today, all tied to fixes merged:

- **High: SSRF vulnerabilities (via media downloads)** — PicoClaw could be used as an SSRF proxy if users/admins were able to trick it into downloading media from malicious URLs. The fixes in PRs #3322, #3323, and #3324 close this vector across all major channels (QQ, WeCom, Weixin, Telegram, Discord, LINE, Slack).
- **High: WhatsApp "client outdated (405)" crash** — The native WhatsApp channel was non-functional due to a pinned dependency issue. Fixed by the dependency bump in PR #3320.
- **Medium: Weixin/WeCom media redirection** — These channels specifically lacked secure URL validation, allowing redirects to internal hosts. Addressed by the same SSRF fixes.

## 6. Feature Requests & Roadmap Signals
Despite the stale-issue cleanup, there are signals for future development:

- **OAuth 2.1 Support for MCP (#3302)** — While closed, it aligns with the roadmap item #2546. If #2546 progresses, we can expect this to be revisited in upcoming versions.
- **Build Remote Agent Phone Pairing (#3344)** — This is a new, open PR. It broadens PicoClaw’s use case to mobile spectators, which is a strong candidate for inclusion in the next minor version if it passes review.

## 7. User Feedback Summary
User sentiment is mixed, with high satisfaction around the rapid fixing of blocking bugs (like WhatsApp) and the proactive security hardening. The completion of several "stale" issues suggests maintainers are actively managing the backlog, which is good for project health. However, the closure of feature requests like Telegram table rendering (#3325) may cause some user dissatisfaction, as it signals a pass on visual polish in favor of core stability and security. Users relying on the native WhatsApp channel will be pleased to see resolution.

## 8. Backlog Watch
- **PR #3222 refactor(deltachat): cleanup implementation, documentation -200LOC** — Open since 2026-07-03, this PR has been updated recently but remains open. It aims to significantly clean up the DeltaChat implementation, dropping legacy features and simplifying the codebase. Maintainers should review this to prevent it from going stale, as the refactor could consolidate the codebase and reduce maintenance burden.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-24

## 1. Today's Overview

NanoClaw is in an active maintenance and stabilization phase with a surge in activity. While no new releases were cut today, the repository saw 50 PRs updated in the last 24 hours (20 merged/closed) and 6 issues updated, indicating a strong core-team push. The primary narrative is a coordinated effort to ship critical fixes for chat SDK integration, a new v2.3.0 release line, and targeted bug fixes. A significant architectural pattern this sprint is the use of **stacked PR chains** on `main` (e.g., [#3490] → [#3491] → [#3492]), including "twin" PRs on registry branches (`channels`, `providers`) for channel payloads that cannot be stacked on the canonical branch. The project appears to be under direct core-team control, with community contributions focused on new provider integrations and documentation.

## 2. Releases

No new releases were published in the last 24 hours. One PR, [#3495](https://nanocoai/nanoclaw PR #3495) (closed), prepares **v2.3.0** by bumping `package.json` and carrying curated release notes, indicating a release is imminent.

## 3. Project Progress

The recent activity shows a targeted effort to resolve installation and dependency issues:

- **v2.3.0 Release Preparation**: PR [#3495](https://nanocoai/nanoclaw PR #3495) closed, staging the next version release.
- **Hardened Image Repin (Stopgap)**: PR [#3496](https://nanocoai/nanoclaw PR #3496) closed. This is a stopgap fix for broken new hardened installs since 2026-08-21 by repinning the image to `hardened-2026-08-23`, allowing operators to get a patched image immediately.
- **Chat SDK 4.32.0 Bump and Lockstep**: PRs [#3466](https://nanocoai/nanoclaw PR #3466) and its registry twin (channels) [#3465](https://nanocoai/nanoclaw PR #3465) closed. These bump the chat core to 4.32.0 and pin every Chat SDK channel skill to it, ensuring lockstep updates.
- **Typing Indicator Lifetime**: PR [#3467](https://nanocoai/nanoclaw PR #3467) and its channels twin [#3468](https://nanocoai/nanoclaw PR #3468) closed. This introduces the ability for a channel adapter to declare its typing-indicator lifetime.
- **pnpm minimumReleaseAge Gate**: PRs [#3469](https://nanocoai/nanoclaw PR #3469) closed, with open stacked twins [#3492](https://nanocoai/nanoclaw PR #3492) and registry twins ([#3471](https://nanocoai/nanoclaw PR #3471), [#3470](https://nanocoai/nanoclaw PR #3470)) to hoist the gate out of the `pnpm:` key and turn it on.

## 4. Community Hot Topics

The most active discussions concern installation stability and bug fixes:

- **Severity: High — Claim-Stuck Watchdog Bug ([#3455](https://nanocoai/nanoclaw Issue #3455))**: This issue details a critical bug where the `host-sweep` watchdog kills legitimately busy turns because the heartbeat isn't touched between claim and first SDK event. It permanently blocks replies with no self-recovery, marking it as "high" impact alongside a fix PR referencing the root-caused logic.
- **Critical Install Breakage ([#3496](https://nanocoai/nanoclaw PR #3496))**: This closed PR marks the `dev.nanoclaw.agent-runner-lock-sha256` label comparison failure causing dead setups. Gets operators patched quickly via repinning.
- **Feature Requests for New Providers**: Signals from the community center on expanding provider support:
  - **Build Remote Agent phone pairing** ([#3494](https://nanocoai/nanoclaw PR #3494), open)
  - **MindsHub provider guide** ([#3493](https://nanocoai/nanoclaw PR #3493), open)
  - **Cursor Agent SDK payload + /add-cursor skill** ([#3355](https://nanocoai/nanoclaw PR #3355), [#3356](https://nanocoai/nanoclaw PR #3356), open)

## 5. Bugs & Stability

Several critical bugs are being reported and addressed:

- **High — Claim-Stuck Watchdog Bug ([#3455](https://nanocoai/nanoclaw Issue #3455))**: This issue details a high-severity bug where the `host-sweep` watchdog kills legitimately busy turns because the heartbeat isn't touched between claim and first SDK event. It permanently blocks replies with no self-recovery, marking it as "high" impact alongside a fix PR in progress.
- **High — Discord Approval/Ask-Question Broken ([#3456](https://nanocoai/nanoclaw Issue #3456))**: Redundant `value` param in the `chat-sdk-bridge` corrupts Discord custom IDs, causing silent rejects and duplicate resends. This issue is closed, indicating a fix has been merged.
- **High — Hardened Install Breakage ([#3496](https://nanocoai/nanoclaw PR #3496))**: This closed PR addresses a critical breakage on new hardened installs since 2026-08-21 by comparing image labels with `path.resolve()` where a realpath is needed. The stopgap fix repins the image.
- **High — update-nanoclaw Controller Fails on macOS ([#3498](https://nanocoai/nanoclaw Issue #3498))**: This issue details a high-severity bug where `update-nanoclaw` exits 0 without running on macOS due to symlinked tmpdir defeating the entrypoint guard and `hasSafeStatePaths`. The update controller's use of `path.resolve()` vs. realpath causes both comparisons to fail, making the documented invocation a no-op.
- **High — better-sqlite3 Segfault on macOS ([#3497](https://nanocoai/nanoclaw Issue #3497))**: This issue reports that `better-sqlite3@13.0.3` segfaults on Node 22 releases older than 22.14.0, leaving no working database layer and preventing `pnpm test` from completing. The declared floor is `>=22`, so an affected Node passes every check.
- **Medium — UNIQUE-Constraint Crash on Retried Delivery ([#3457](https://nanocoai/nanoclaw Issue #3457))**: `insertMessage()` uses a plain `INSERT` that crashes on retried delivery with the same message id, contributing to duplicate-message symptoms. Likely a fast-follow fix for the app.

## 6. Feature Requests & Roadmap Signals

- **New Provider Integrations**: The roadmap clearly includes expanding beyond standard channels. Active PRs for **Build Remote Agent** ([#3494](https://nanocoai/nanoclaw PR #3494)) and **Cursor Agent SDK** ([#3355](https://nanocoai/nanoclaw PR #3355), [#3356](https://nanocoai/nanoclaw PR #3356)) suggest an aggressive push to support more agent providers.
- **Documentation and Guides**: A pull request to add **MindsHub provider guide** and setup skill ([#3493](https://nanocoai/nanoclaw PR #3493)) indicates a focus on easing onboarding for new server providers.
- **Typing Indicators**: The merged PR for declaring typing-indicator lifetime ([#3467](https://nanocoai/nanoclaw PR #3467), [#3468](https://nanocoai/nanoclaw PR #3468)) hints at a future roadmap item to standardize the UX for typing indicators across all channels. This sets the architecture for future per-channel customization.

## 7. User Feedback Summary

- **Pain Point — Stability on macOS**: Two of today's issues ([#3497](https://nanocoai/nanoclaw Issue #3497), [#3498](https://nanocoai/nanoclaw Issue #3498)) highlight macOS-specific stability problems, from native module segfaults caused by too-low a Node version floor to symlinked tmpdir paths breaking update flows. There is a clear user expectation that `update-nanoclaw` and setup scripts work reliably on macOS out-of-the-box.
- **Pain Point — Broken Install Experience**: The hardened install breakage ([#3496](https://nanocoai/nanoclaw PR #3496)) demonstrates a direct user-facing failure: operators on new hardened images experienced dead setups. The quick repin response mitigates the issue, but the root-causing of the SHA label comparison error is pending.
- **Pain Point — Critical Reply Blocking**: The claim-stuck watchdog issue ([#3455](https://nanocoai/nanoclaw Issue #3455)) shows user-facing frustration with permanently blocked replies for a session, with no self-recovery. The impact of the `host-sweep` logic is a high-priority area for the community.
- **Pain Point — Discord Approval Flows**: Users hitting the Discord approval/ask_question card bug ([#3456](https://nanocoai/nanoclaw Issue #3456)) would experience silent rejection, duplicate resends, and an overall broken UX. The swift closure of this issue signals a clear priority on core action flows.

## 8. Backlog Watch

Several PRs and Issues have been open for an extended period without a clear path to merge:

- **Long-Standing Bug** — **`fix(signal): forward image/file attachments through a mounted inbox`** ([#3142](https://nanocoai/nanoclaw PR #3142)): Open since **July 27**. This is a critical bug affecting all non-image, non-audio attachments for Signal users. The fix is blocked by the container not reading from the mounted path. Because it touches security and container paths, it might be pending design review.
- **Long-Standing Enhancement** — **`feat(add-github): polling mode, git access question, safe OneCLI secret merge`** ([#2301](https://nanocoai/nanoclaw PR #2301)): Open since **May 6**. This is a large PR with a long summary covering a polling mode, webhook security warning, and safe secret merge. Despite being a major capability, it has been open for 3+ months. The size and scope might require it to be split into smaller, reviewable changes.
- **Long-Standing DevExperience** — **`ci: add pre-commit hooks (prettier, eslint, typecheck, vitest)`** ([#2537](https://nanocoai/nanoclaw PR #2537)): Open since **May 18**. This PR is ready and adds missing DX improvements. It has been open for over 3 months, possibly deprioritized by core-team stacked PR work. If maintainers want to improve contribution efficiency, this could be a quick win to merge.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

## NullClaw Project Digest — 2026-08-24

### 1. Today's Overview
NullClaw project status is **low activity with a notable stability concern**. Over the last 24 hours, there was 1 open/active issue, 0 merged or closed PRs, and no new releases. The single issue (#991) describes a **serious hang scenario** involving stdio MCP servers and a lock held by the gateway service — this is the primary focus of maintainer attention today. Overall, the project appears to be in a normal maintenance phase, but the reported deadlock potential in a core integration path warrants prioritization.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Project Progress
No pull requests were merged or closed in the last 24 hours. No new features, fixes, or refactoring advanced through the PR pipeline today.

### 4. Community Hot Topics
**Issue #991 — [OPEN] MCP stdio calls can hang indefinitely behind the Proxmox launcher lock**  
- Author: **locke1979** | Created: 2026-08-23 | Updated: 2026-08-23 | Comments: 2 | 👍: 0  
- Link: [NullClaw Issue #991](https://github.com/nullclaw/nullclaw/issues/991)  

This is the only active discussion today. It describes a race condition/deadlock where a standalone `nullclaw agent` invocation blocks indefinitely because the stdio MCP server is already owned by the long-lived gateway process (tested with a 148-tool Proxmox MCP bridge). The underlying need, though not explicitly stated, suggests that **users expect concurrent/parallel MCP server access** from gateway processes and ephemeral agents, and they need a lock negotiation or timeout mechanism rather than an indefinite block. Given 2 comments already, there is engaged discussion.

### 5. Bugs & Stability
| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **High** | [#991](https://github.com/nullclaw/nullclaw/issues/991) | Stdio MCP server calls hang indefinitely when the MCP server is already owned by the gateway (lock contention). Reproduced deterministically in Proxmox CT 151 with NullClaw 2026.8.22. | None currently open. |

**Analysis:** This is rated **High** not because of data loss, but because a hang of indefinite duration in a core execution path represents a **process-level deadlock** — an operator may need to manually kill the process. The problem likely stems from lock acquisition without a timeout. Since the reporter provided a clean reproduction (read-only Proxmox bridge, 148 tools), maintainers should be able to isolate this quickly.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed in the last 24 hours. However, a likely **roadmap signal** from issue #991 is: **"MCP server lock timeout & concurrency control"** — i.e., the ability to configure a lock-wait timeout, or to support shared/read-only MCP connections across multiple agents simultaneously. This hints at a broader need for **better process lifecycle management** for MCP bridges (daemonization, lock files, or socket-based sharing). Expect a fix or configuration option in the next patch release (likely `2026.8.23+`).

### 7. User Feedback Summary
**Pain point:** The single report today from **locke1979** highlights a real operational frustration: a user attempting to run a one-off `nullclaw agent` command while the gateway service is active can get a **silent, permanent hang**. This is especially problematic in homelab environments (Proxmox CT) where systemd services are long-running. The user went to the trouble of supplying a full environment description and reproduction steps, indicating they want a quick triage. No positive or negative satisfaction signals were otherwise present today.

### 8. Backlog Watch
No long-standing unanswered issues or stale PRs were updated today. With only 1 active issue in the queue, the backlog appears healthy and maintainers can focus entirely on triaging #991. **Recommendation:** Maintainers should engage with #991 as soon as possible — assign a fix target (e.g., adding a timeout to the launcher lock acquisition) and acknowledge the reporter to prevent frustration.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-24

## 1. Today's Overview

IronClaw is in a period of intense, coordinated infrastructure hardening. Activity is very high: 9 issues and 23 PRs were updated in the last 24 hours, with zero new releases. The core team (henrypark133, serrrfirat, sergeiest) is executing a four-lane CI-expedite program (T1–T4) aimed at eliminating "green locally, red in CI" drift; several large PRs in this program are open for review. Concurrently, the team is landing major architectural features—persistent per-user sandboxes with a managed egress proxy (PR #7810), and grounded suggestion generation (PR #7833)—while a newly surfaced product-feedback triage pipeline produced three bug reports about extension installation failures (Notion, Gmail, Slack), signaling a possible integration/auth regression. The project is healthy in terms of contributor throughput, but the CI rewrite and user-reported integration failures are the two key risk areas to monitor.

## 2. Releases

No new releases were published in the last 24 hours. The most recent tagged release remains the `v1.4.0` milestone toward which the Epic (#7732) is targeted.

---

## 3. Project Progress

**Merged/Closed PRs (5 total):**

- **[#7730 — chore(deps): bump the everything-else group with 6 updates](https://github.com/nearai/ironclaw/pull/7730)** (Merged) — Routine Rust dependency updates (uuid, base64, toml, etc.).
- **[#7406 — chore(deps): bump the actions group with 4 updates](https://github.com/nearai/ironclaw/pull/7406)** (Merged) — CI action updates: anthropics/claude-code-action, setup-node, rust-cache, docker/login-action.
- **[#7262 — chore(deps): bump the wasm group with 2 updates](https://github.com/nearai/ironclaw/pull/7262)** (Merged) — Wasm toolchain updates (wit-component, wit-parser).
- Two additional PRs closed without merge (throwaway CI probe branches [#7839](https://github.com/nearai/ironclaw/pull/7839) and [#7838](https://github.com/nearai/ironclaw/pull/7838) were created explicitly to exercise the new `nextest` CI pipeline and are marked "do not merge").

**Major features advanced (open, under review or active):**

- **Sandbox & egress security (plateau):** [PR #7810](https://github.com/nearai/ironclaw/pull/7810) is the centerpiece of the persistent-sandbox Epic. It completes the per-user sandbox runtime with manifest-declared, proxy-mediated credential bindings. The `gh` CLI is the first consumer: the command sees a placeholder, and only the `iron-proxy` sidecar injects the real `GH_TOKEN`, scoped to specific API endpoints. Risk: low. Size: XL.
- **Grounded suggestions:** [PR #7833](https://github.com/nearai/ironclaw/pull/7833) closes #7812. Suggestion generation now uses the user's read-only, no-approval tools, producing cards grounded in real connected data (e.g., reading Gmail) instead of a hardcoded allowlist. This significantly improves suggestion relevance.
- **Subagent background mode:** [PR #7818](https://github.com/nearai/ironclaw/pull/7818) lands slices 2b+2c of the background-subagent feature (receipt-based spawning, per-child delivery, activation, and healing sweeps). This turns the previously inert surface (#7788) into a functional producer path. A deployment gate is flagged in the PR.
- **IronHub agent link from WebUI:** [PR #7516](https://github.com/nearai/ironclaw/pull/7516) adds an operator surface to complete an IronHub agent link from the Extensions page; [PR #7826](https://github.com/nearai/ironclaw/pull/7826) fixes four catalog-install failure modes that block hub-published packages.

---

## 4. Community Hot Topics

- **Epic: Persistent per-user sandbox (Issue #7732)** — 9 comments. This is the most-discussed item, tying together the iron-proxy architecture (#7810), egress auth (#7825), and the deferral of loop executors. It is the architectural backbone for the v1.4.0 milestone, with implications for security, isolation, and multi-tenancy.
- **Onboarding suggestions permissions (Issue #7812)** — 3 comments. Discusses the tradeoff between grounding suggestions in user data vs. respecting user-level tool permissions. The fix (PR #7833) is already in review, adopting a conservative read-only, no-approval approach.
- **Slack product-feedback triage (#7832, #7827)** — The automated triage (created and updated in the same window) is generating sub-issues for actionable feedback. This is an emergent, automated "voice of the customer" flow; the underlying need is to make product feedback trackable and actionable in the repo.

---

## 5. Bugs & Stability

The highest-signal issue is a potential **integration/auth regression for third-party extensions**:

1. **Gmail auth popup immediately disappears (Issue #7829)** — Users report the OAuth popup closes within ~1 second during setup from the web UI. Severity: **High** (blocks a common integration, suggests a frontend/iframe/popup issue). No fix PR yet → likely needs maintainer attention.
2. **Notion extension fails to install (Issue #7830)** — Installation error on the IronClaw side. Severity: **High** (blocks integration). No fix identified.
3. **Slack setup blocked for NEAR Foundation accounts (Issue #7828)** — Possibly tenant- or account-specific; may overlap with #7829. Severity: **Medium-High**.
4. **PR #7826** — Identifies and fixes four catalog-install failure modes: unnecessary `capabilities.json` sidecar, egress budget applied to response instead of request, and schema-ref mismatches ("standard:" vs published). This directly addresses the class of bug reported in #7830/#7828, so a fix path exists and is under review.

These three user reports, triaged from the same Slack window, suggest a coordinated investigation into extension install/auth is warranted. The auth popup issue (#7829) may also be related to the proxy work in #7810 if any sandbox changes affected webview/iframe behavior.

---

## 6. Feature Requests & Roadmap Signals

- **Persistent per-user sandbox** is the flagship roadmap item (#7732), explicitly targeting v1.4.0. The egress-auth design (#7825) is its companion, retiring the GitHub-specific carve-out in favor of a generic host credential broker. Expect this to land in the next minor release.
- **Superuser-level tool permissions for suggestion generation** (#7812) is effectively a roadmap add; the PR is already written, so it will likely appear in v1.4.0 as well.
- **Tool advertisement filtered by availability** (#7836) — a correctness improvement to the tooling surface: models should only see tools that can actually execute (installed + activated + credential-ready + authorized). This prevents "doomed calls" and aligns with PinchBench findings. Expected in a near-term patch.
- **Background subagents (2b/2c)** — approaching full functionality; the next milestone is likely "healing sweeps" stabilization and, later, "loop executors," which are explicitly deferred per #7732.

---

## 7. User Feedback Summary

The automated triage pipeline brought in three distinct user pain points, all in the extension/integration setup path:

- **Gmail setup broken in web UI** — "window popup appears (I assume its to authenticate my google account) but it stays for like 1 seconds and goes away." Clear sign of a frontend auth-routing bug.
- **Notion install fails** — "Notion tool doesn't want to install in my IronClaw." Vague but reproducible enough to file.
- **Slack blocked** — "not being able to set up Slack in my alejo.escriva@near.foundation IronClaw." Account- or tenant-specific.

Satisfaction concern: three consecutive integration failures is a pattern, not a coincidence. The team will want to prioritize a general fix for extension install/auth flows; the root cause may be shared (PR #7826 points at the catalog-install path).

No positive feedback items were captured in this window; the triage process is new and may under-sample praise.

---

## 8. Backlog Watch

- **Issue #7829 (Gmail auth popup)** and **#7830 (Notion install)** — high-severity user-facing bugs, no fix PR linked yet. These should be triaged with urgency given the team is already active in this space.
- **Issue #7825 (Sandbox egress auth)** — no comments since creation; it's a design proposal referencing #7810. Needs review to ensure the generic credential broker lands with the sandbox work.
- **Issue #7836 (Tool advertisement filtering)** — zero comments; straightforward scoped improvement. Awaiting a champion.
- **PR #7837 and #7834 (dependency bumps, 11 and 4 updates)** — routine but large; Dependabot PRs have been merging consistently, so these are likely to be handled soon. The `actions/setup-node` bump from `4.0.2` to `7.0.0` in #7835 is a major-version jump worth reviewing for breaking changes in CI behavior.
- **PR #7255 (APDD governance kit evaluation)** — open since 2026-08-05 with no merged decision; flagged as a governance process item that may need maintainer attention to close the loop.
- **PR #7516 (WebUI IronHub link)** — open since 2026-08-12; a new contributor (neo-sky) with an XL-size PR. Might benefit from a maintainer pass to keep momentum and avoid drop-off.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-24

## 1. Today's Overview

Project activity was moderate, with 4 issues and 3 PRs updated in the last 24 hours—all items were closed or merged, leaving zero open items in the current batch. Notably, all updated items were flagged as **stale**, indicating these are older threads (created April 1) that are being swept through a cleanup cycle rather than representing fresh community interaction. No new releases were published during this period. The closure of 7 items in a single day suggests active maintenance and backlog hygiene, though the complete absence of newly created issues or PRs points to a lull in new feature development and community bug discovery.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

All three PRs updated today were closed/merged, and each addresses a distinct area of improvement:

- **[#1197 — Agent 管理页面交互优化](https://github.com/netease-youdao/LobsterAI/pull/1197)** — UI/UX improvement to the Agent management page. The PR reduces the interaction depth for deleting agents (previously required entering a detail panel) and improves the sidebar. This is a re-attempt of an earlier PR (#1176) that had merge conflicts with the main branch — resolved and now merged.

- **[#1199 — feat(model): add context window and token settings](https://github.com/netease-youdao/LobsterAI/pull/1199)** — Adds per-model `contextWindow` and `maxTokens` settings in the Settings panel. These fields are persisted, exported, and surfaced in the model list. The settings propagate into direct chat requests and into Cowork/OpenClaw config generation. This is a meaningful capability expansion for power users managing multiple models.

- **[#1201 — [Bug] NIM 超大群消息中 teamTypeNum 硬编码错误](https://github.com/netease-youdao/LobsterAI/pull/1201)** — One-line fix for a hardcoded enum mismatch in `nimGateway.ts` (line 917). The code swapped `team` and `p2p` type numbers, causing group name lookup failures for @-mention messages in NIM super-groups and normal groups. The fix aligns the code with the SDK enum definitions already documented in the file's header comments.

## 4. Community Hot Topics

All four issues updated today are stale threads with 2 comments each and no reactions, indicating they have been resolved and are being closed out. The issues cover distinct areas of user interest:

- **[#1196 — Working directory file clutter](https://github.com/netease-youdao/LobsterAI/issues/1196)**: User frustration with forced creation of 6 system files (AGENTS.md, USER.md, etc.) in every working directory. Suggests a global/shared configuration location or hidden directory approach. Reflects a desire for less invasive workspace management.

- **[#1198 — Gateway restart UI feedback](https://github.com/netease-youdao/LobsterAI/issues/1198)**: Progress bar disappears mid-restart, leaving users without status visibility. Also raises an inconsistency where Chrome opens successfully but the browser service is still reported unavailable.

- **[#1200 — NIM group naming bug](https://github.com/netease-youdao/LobsterAI/issues/1200)**: Same root cause as PR #1201 above — hardcoded enum values break group name resolution for super-group messages.

- **[#1202 — Model key leak through agent](https://github.com/netease-youdao/LobsterAI/issues/1202)**: Security concern where the agent reveals sensitive model key configuration details when prompted. User expects the agent to refuse such disclosures; instead, it leaks file paths, environment variable names, and related key information.

## 5. Bugs & Stability

| Severity | Issue | Status | Notes |
|----------|-------|--------|-------|
| 🔴 **High** | [Security/Privacy: Agent leaks model key info](https://github.com/netease-youdao/LobsterAI/issues/1202) | **No fix PR found** | Agent responds to prompts with sensitive key configuration details (file paths, env var names, key values). This is an AI agent product, so prompt-injection-resistant guardrails should be a core priority. |
| 🟡 **Medium** | [NIM group name resolution broken](https://github.com/netease-youdao/LobsterAI/issues/1200) | **Fixed in [#1201](https://github.com/netease-youdao/LobsterAI/pull/1201)** | Hardcoded enum values swapped between `team` and `p2p` types; one-line fix merged. Affects @-mentions in both super-groups and normal groups. |
| 🟡 **Low** | [Gateway restart UI progress bar loss](https://github.com/netease-youdao/LobsterAI/issues/1198) | **No fix PR found** | UX flaw during restart: progress indicator disappears, and stale "service unavailable" messages persist even when Chrome/browser is actually available. |

## 6. Feature Requests & Roadmap Signals

Two signals in today's batch point toward ongoing UX and capability improvements:

- **Per-model token/context configuration** ([#1199 — merged](https://github.com/netease-youdao/LobsterAI/pull/1199)): Users now have granular control over context window and max tokens per model, with proper propagation into Cowork/OpenClaw configs. Expect further iteration in this area, especially around surfacing these settings in more places and supporting model presets.

- **Workspace filesystem hygiene** ([#1196](https://github.com/netease-youdao/LobsterAI/issues/1196)): Users strongly dislike the forced creation of 6 system files in every working directory. Expect a global config file approach (similar to how some tools centralize `.agents.md`), or moving these files to a hidden directory. This is a high-likelihood candidate for the next minor release given the clear user sentiment.

- **Agent management UX** ([#1197 — merged](https://github.com/netease-youdao/LobsterAI/pull/1197)): The streamlined deletion flow and sidebar improvements reduce friction in the Agent management page; further refinements may follow based on adoption.

## 7. User Feedback Summary

Common themes from this batch of issues:

- **Workspace pollution**: Users want LobsterAI to be less intrusive in their file system. The forced file creation pattern is described as "messy" (太乱了) — users want a global/shared config location instead.
- **Security expectations**: Users expect agents to guard sensitive configuration data by default. The fact that an agent willingly reveals key paths and environment variable names is seen as a violation of trust.
- **Operational visibility**: Users need clearer status during gateway restarts and better consistency between reported service state and actual state (e.g., browser service being "unavailable" when it is actually open).
- **Chat accuracy**: Incorrect group name resolution in NIM integration undermines trust in the agent's ability to handle large-group messaging reliably (though this is now fixed).

## 8. Backlog Watch

- **[Issue #1202 — Model key leak via agent](https://github.com/netease-youdao/LobsterAI/issues/1202)**: Closed as stale, but this is a security-sensitive issue with no visible fix. High priority for maintainers to reopen if not truly resolved — recommend verifying the fix isn't just a documentation change and that actual prompt-level guardrails were added.

- **[Issue #1198 — Gateway restart UX](https://github.com/netease-youdao/LobsterAI/issues/1198)**: Closed as stale; the described UX gap remains unresolved. If the fix was folded into a larger refactor, it would help the community to reference the commit or PR that addressed it.

- **No clearly unaddressed long-running items** remain in this batch — all issues and PRs were closed or merged, which is a sign of healthy triage.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for **2026-08-24**.

---

# Moltis Project Digest: 2026-08-24

## 1. Today's Overview
The project is in a **high-velocity bug-fixing and hardening phase**. While no new releases were cut today, the maintainers are actively processing a significant queue of pull requests (6 open, 0 merged) focused on memory bounds, MCP client lifecycle, and bundled skill integrity. Issue activity is moderate (3 updates), with the older TLS/WebSocket bug (#245) drawing renewed attention. The overall health appears strong, with a clear focus on stabilizing the runtime (memory, TLS, MCP) and connector reliability (Slack, WhatsApp) rather than shipping new headline features.

## 2. Releases
No new versions were published in the last 24 hours. There are no release notes, breaking changes, or migration details to report for this period.

## 3. Project Progress
There were **no merged or closed PRs** in the last 24 hours; however, a significant feature issue (#1230) regarding fail-closed security hooks was closed. The focus remains on active PRs addressing specific technical debt and bugs:

- **Local Memory Safety (PR #1236, #1235)**: These PRs address critical stability and configuration consistency issues in the memory subsystem. PR #1236 bounds embedding encoder batches to prevent process crashes, while PR #1235 normalizes backend config values.
- **MCP Client Lifecycle (PR #1231)**: This fix ensures that after an MCP server restart, the tool bridge correctly resolves the new client, preventing dispatches through closed instances.
- **Bundled Skills (PR #1234)**: This addresses a bug where recursive bundled sidecar files (like `quick_validate.py`) were listed but reported as "not found," which is essential for packaging integrity.
- **Scheduled Outputs (PR #1226)**: This adds logic to deliver scheduled/cron outputs back to the originating chat, improving the conversational context for automated tasks.

## 4. Community Hot Topics
The most active discussion is centered on a **long-standing, critical bug**:

- **TLS/ALPN & WebSocket Breakage (Issue #245)** — [Link](https://github.com/moltis-org/moltis/issues/245)
    - **Activity**: 2 comments, updated 2026-08-23. This issue has been open since February but has recent activity.
    - **Analysis**: This is a high-priority interoperability issue. Users are experiencing silent failures where fresh browser sessions negotiate `h2` (HTTP/2) via ALPN, breaking WebSocket upgrades. The underlying need is for robust protocol negotiation (prioritizing `http/1.1` for WS) to ensure seamless connectivity across all user environments.

## 5. Bugs & Stability
One new user-reported bug surfaced, while two fixes are in the pipeline for critical stability issues.

1.  **Memory Process Crash (PR #1236)** — **Critical**: Local embeddings can terminate the entire process if a chunk exceeds 512 tokens. This is a severe stability issue. **Status**: Fix PR is open (#1236).
2.  **Shared Slack Channel Tool Failure (Issue #1224)** — [Link](https://github.com/moltis-org/moltis/issues/1224) — **High**: Tools stop functioning in shared Slack channels. This is a direct blocker for multi-workspace collaboration. **Status**: No linked PR yet; awaiting maintainer triage.
3.  **TLS/ALPN WebSocket Failure (Issue #245)** — **High**: Silent connectivity failure on page refresh/new tabs. **Status**: No linked PR yet; needs long-term fix.
4.  **MCP Client Dispatch (PR #1231)** — **Medium**: Active chat turns dispatched through closed clients after a server restart. **Status**: Fix PR is open (#1231).

## 6. Feature Requests & Roadmap Signals
The PRs and closed issues signal the roadmap focus for the next release:

- **Security Hardening**: The closing of issue #1230 (fail-closed policy for hooks) suggests the next version will include more robust security boundaries, making `fail-closed` an opt-in policy for critical infrastructure hooks.
- **Extended Connector Capabilities**: PR #1233 is a strong signal for **WhatsApp document ingestion**. This moves Moltis from metadata-only to actual file availability, enabling agents to process PDFs, images, etc., directly from WhatsApp. This is likely to be a headline feature in the upcoming release.
- **Better Automation Context**: PR #1226 (deliver to originating chat) indicates work on making scheduled outputs context-aware, enhancing the UX of cron jobs and automated reporting.

## 7. User Feedback Summary
- **Pain Point — Setup/Configuration Consistency**: Users have reported issues with config names (e.g., `sqlite` vs `builtin`), which creates friction during setup. PR #1235 directly addresses this confusion.
- **Pain Point — Critical Instability**: The crash on embedding is a frustrating experience for users experimenting with local memory models, as an over-length prompt can kill the entire session.
- **Pain Point — Integration Reliability**: The Slack shared-channel bug is a real-world use case failure for team collaboration, highlighting a need for more robust permission handling in multi-tenant scenarios.
- **Use Case Demand — Document Analysis**: The demand for WhatsApp document ingestion (PR #1233) shows that users want to leverage Moltis as a primary data analysis tool, not just a chat assistant.

## 8. Backlog Watch
- **Issue #245 (TLS/ALPN & WebSocket)** — [Link](https://github.com/moltis-org/moltis/issues/245): This is the most critical **long-standing issue** (open since Feb 2026). It has remained unaddressed for six months despite being a severe connectivity bug. This needs immediate maintainer attention to root-cause the ALPN negotiation.
- **Issue #1224 (Slack Shared Channels)** — [Link](https://github.com/moltis-org/moltis/issues/1224): While newer, this issue impacts a core use case and has **zero comments** from the maintainer team. It should be triaged quickly to assess impact and provide a workaround while a fix is developed.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-24

## 1. Today's Overview

CoPaw (QwenPaw) is in an active development phase with 8 PRs merged/closed and 7 PRs still open in the last 24 hours. The merged work clustered around two major feature areas — the **skill system** (dynamic loading, auto-unload, auto-title-sync) and **bug fixes** across CLI message construction, Windows process liveness probes, and token usage caching. Meanwhile, 5 open issues were touched today, dominated by two significant **stability concerns**: a runtime memory leak growing to 20.7 GB after two days of continuous use, and a plugin workspace-scoped registration loss on agent reload. The repo is healthy: the active contributors (Ferrum360 with 4 merged PRs, Yigtwxx with 3) show a strong pipeline of vetted contributions landing, but the emerging memory-leak report warrants close attention.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

The following PRs were **merged or closed** today. Highlights include a substantial skill-system overhaul and several targeted bug fixes:

- **feat(skill-system): dynamic skill loading + auto-unload + frontmatter fix** — [PR #7031](https://github.com/agentscope-ai/QwenPaw/pull/7031), [PR #7033](https://github.com/agentscope-ai/QwenPaw/pull/7033) (closed; duplicates) — Adds minimal runtime infrastructure for dynamic skill lifecycle: idle skills are unloaded and frontmatter/lazy-skill path bugs are fixed.
- **feat(auto-title-sync): auto-memory linked chat title refresh + observability** — [PR #7030](https://github.com/agentscope-ai/QwenPaw/pull/7030), [PR #7032](https://github.com/agentscope-ai/QwenPaw/pull/7032), [PR #7027](https://github.com/agentscope-ai/QwenPaw/pull/7027) (closed) — Chat titles now refresh as auto-memory entries evolve, plus observability and cleanup of backup files.
- **fix(token_usage): don't persist an unseeded cache on shutdown** — [PR #6220](https://github.com/agentscope-ai/QwenPaw/pull/6220) — Prevents writing an empty `TokenUsageBuffer` disk cache on shutdown when it was never seeded from disk.
- **fix(utils): bound and hide the Windows tasklist liveness probe** — [PR #6203](https://github.com/agentscope-ai/QwenPaw/pull/6203) — Adds a missing timeout and hides the console window for `tasklist` subprocess calls on Windows.
- **fix(cli): build a valid user message for the headless task command** — [PR #6616](https://github.com/agentscope-ai/QwenPaw/pull/6616) — Fixes `qwenpaw task` silently never running a task: `Msg.content` must be a `list[ContentBlock]` per pinned `agentscope==2.0.4.post1`, but a raw `str` was being passed.

## 4. Community Hot Topics

- **Memory leak to 20.7 GB after 2-day runtime** — [Issue #7222](https://github.com/agentscope-ai/QwenPaw/issues/7222) (2 comments) — The most severe and attention-grabbing report of the week. The user provides a precise reproduction window (2026-08-21 start → 23:00 on 08-23) and distinguishes it from the known startup leak (#9). This is a runtime accumulation, gradual growth to 20.7 GB, with heavy document workloads. No linked fix PR yet.
- **reload_agent() drops plugin workspace-scoped registrations** — [Issue #7221](https://github.com/agentscope-ai/QwenPaw/issues/7221) (3 comments, most-commented) — Any config change triggering zero-downtime reload loses plugin runtime hooks, modes, and slash commands. The adjacent open PR [PR #7183](https://github.com/agentscope-ai/QwenPaw/pull/7183) ("workspace-scoped always-on loading") may partially address this space, but is scoped to skills, not the reload path.
- **Aider CLI integration request (RU)** — [Issue #7224](https://github.com/agentscope-ai/QwenPaw/issues/7224) — A Russian-speaking user asks how to wire Aider CLI (`aider-chat`) as a managed agent. Reflects demand for bringing external CLI coding tools into the QwenPaw agent orchestration model.
- **Incomplete chunked read errors on long inferences** — [Issue #7218](https://github.com/agentscope-ai/QwenPaw/issues/7218) — User on Windows 10 v2.1.0 reports `peer closed connection without sending complete message body` on long text/reasoning. They also note their model provider sees QwenPaw exit at 130–140 s while the provider's timeout is 180 s — implying a client-side timeout or proxy behavior inside QwenPaw.

## 5. Bugs & Stability

| Issue | Severity | Description | Has Fix PR? |
|---|---|---|---|
| [#7222](https://github.com/agentscope-ai/QwenPaw/issues/7222) | **High** | Unbounded runtime memory growth: 20.7 GB after 2 days of continuous backend use with heavy document workloads; drags down the whole machine. | **No** |
| [#7217](https://github.com/agentscope-ai/QwenPaw/issues/7217) | **High** | Stopping a task/conversation mid-way causes the next conversation to replay the previous one entirely (including its thinking), regardless of the new question. Suggests stale context/state not cleared on stop. | **No** |
| [#7218](https://github.com/agentscope-ai/QwenPaw/issues/7218) | **Medium** | Recurring `peer closed connection without sending complete message body` on long inferences; user suspects a QwenPaw-side timeout (exit ~130–140 s vs provider 180 s). | **No** |
| [#7221](https://github.com/agentscope-ai/QwenPaw/issues/7221) | **Medium** | `reload_agent()` silently drops plugin workspace-scoped registrations (runtime hooks, modes, slash commands) after any zero-downtime config change. | **No** (PR #7183 partially related) |

## 6. Feature Requests & Roadmap Signals

- **Aider CLI as a first-class agent** — [Issue #7224](https://github.com/agentscope-ai/QwenPaw/issues/7224): Explicit request to connect an external CLI agent (Aider) to QwenPaw's orchestration. Suggests roadmap appetite for "agent-of-agents" integrations where QwenPaw managers external coding tools.
- **Session-scoped multi project directories** — [PR #6976](https://github.com/agentscope-ai/QwenPaw/pull/6976) (open) — Binds a chat to an ordered list of project directories (primary + additional), with relative paths and `cwd` resolving from the primary. Likely to land next.
- **Workspace-scoped always-on skills** — [PR #7183](https://github.com/agentscope-ai/QwenPaw/pull/7183) (open) — Preloads full instructions for enabled always-on skills before the model's first decision; complements the dynamic skill lifecycle work merged today.
- **All-agent LLM & tool-call trend chart** — [PR #7219](https://github.com/agentscope-ai/QwenPaw/pull/7219) (open) — Extends Token Usage view with an all-agent LLM & tool-call trend, matching Agent Statistics counting rules.
- **Exclude reasoning from generated titles** — [PR #7187](https://github.com/agentscope-ai/QwenPaw/pull/7187) (open) — Prevents thinking content from leaking into auto-generated chat titles (fixes #6979).

## 7. User Feedback Summary

Today's feedback skews **negative on stability**, **positive on feature velocity**. The memory leak report (#7222) is the starkest signal: "process memory from a few hundred MB at start grows continuously to 20.7 GB, eventually slowing down the whole machine" — a production-blocking issue for long-running heads. The task-replay bug (#7217) is equally alarming from a UX standpoint: "after stopping a task, the next conversation follows the previous one completely (including its thinking), no matter what is asked." Users are also hitting rough edges in the integration surface: timeout behavior on long inferences (#7218), plugin scope loss on reload (#7221), and lack of documentation for wiring external CLIs (#7224). On the other side, multiple first-time contributors had PRs merged or moved forward (#6203, #6616, #7223, #7220, #7066, #7187) — a sign the onboarding path is healthy and the maintainers are responsive.

## 8. Backlog Watch

- **Issue #7222 — Memory growth to 20.7 GB**: Highest severity item with no linked fix PR and no maintainer comment visible. The user has a clear repro timeline; this needs a maintainer response and a triage assignment.
- **Issue #7217 — Replay-previous-conversation after stop**: Potentially the most user-visible bug of the week, yet no maintainer reply or activity beyond the author's report. The behavior (carrying over prior thinking) suggests a context-buffer lifecycle bug in stop paths.
- **PR #7066 — Persist rotated refresh_token for OAuth2 auth-code providers** (open since 08-16, updated today): Marked "Under Review" but no merge. Closes a real bug for remote MCP servers using rotating refresh tokens (XMind). Could use attention to avoid token invalidation loops.
- **PR #7207 / #7219 / #7220 / #7223**: All first-time contributor PRs updated today but still waiting on review; PR #7220 (reject oversized image dimensions) closes a concrete freeze/crash bug (#7212) and deserves fast-track review.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-24

## 1. Today's Overview

ZeroClaw is in a period of intense architectural RFC activity and stabilization. Activity remains very high with 50 issues and 50 PRs updated in the last 24 hours, though no new releases were published. The project's core focus is on hardening the runtime, refining the channel/gateway architecture, and establishing governance processes for RFC decision-making. Only 12 issues and 5 PRs were closed/merged in the period, suggesting a bottleneck in merge throughput that may be linked to the high volume of open RFCs awaiting maintainer decision. The maintainer decision queue tracker (#8692) indicates a deliberate, slower path toward ratification of major architectural changes.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release remains the one referenced in PR #10217's reproduction note (v0.8.4 Alpine), which is relevant to a filesystem listener bug but does not appear to be the current version.

## 3. Project Progress

**Merged/Closed PRs (5 total — only the top item by comments shown below).** The most significant closed item is a high-urgency bug fix.

- **#10217 (CLOSED, risk:high, size:S)** — `fix(channels): make the filesystem listener cancellation-aware` (JordanTheJet). This directly resolves issue #9666 by replacing a blocking `std::sync::mpsc::Receiver::recv()` in the async filesystem watcher loop, which was parking Tokio workers and preventing clean supervisor shutdown/reload. This confirms issue #9666 as fixed.

In addition to this fix, the repository is seeing a wave of well-scoped PRs targeting cron, security, and provider reliability, several of which remain open (see Section 8).

## 4. Community Hot Topics

The community's attention is concentrated on large, high-risk RFCs demanding architectural decisions.

- **#9487 — RFC: Runtime-owned conversation sessions and transport surface adapters** (25 comments, needs-author-action) — Most active issue by comment count. It has been revised twice (July 28 → Aug 3) and ratifies ownership boundaries across multiple trackers (#9488/#9600). The scale of cross-referencing indicates a fundamental restructuring of how sessions and the API surface interact.
- **#9488 — RFC: Unified attachment architecture** (19 comments, needs-author-action) — A closely related sibling to #9487, proposing a unified approach across web chat and channels. High-level interest is shown by intense revision and cross-linking.
- **#6850 — RFC: Decouple memory lifecycle policy from storage backends** (17 comments, needs-author-action) — A long-running proposal (since May 22) generating ongoing discussion about the boundary between `Memory` trait backends and lifecycle/consolidation policies.
- **#8780 — RFC: Realtime speech-to-speech channel (Gemini Live)** (17 comments, rewritten v2 in August) — Pivoted the proposal to a broker contract, indicating active design iteration.
- **#8692 — Maintainer decision queue for RFCs (Tracker)** (13 comments) — The central coordination point for the backlog of RFCs awaiting maintainer approval; it is a key health indicator for this project.

## 5. Bugs & Stability

Several notable bugs were reported or addressed in the last 24 hours.

- **#10272 (NEW, Bug, parallel test correlation)** — A nondeterministic failure in `zeroclaw-providers` Hailo-Ollama integration tests, where parallel tests capture an event from another test. Severity is medium; a fix likely involves test isolation patterns (e.g., per-test output directories).
- **#9666 (CLOSED, severity S2)** — Filesystem listener cancellation bug (see PR #10217 merge). Fix now confirmed.
- **#6105 (OPEN, status:blocked)** — Cron agent context bug: the agent has no reference to the cron job message that triggered it. Blocked and waiting on runtime changes.
- **#10258 (OPEN PR)** — Fixes a cron update bug where `--command` patches on agent jobs write an unused column and may run shell-policy validation on prompt text.
- **#10253 (OPEN PR)** — Fixes a security policy resolution issue in cron jobs, preventing a double `SecurityPolicy` resolution with a different scope.

No severe regressions were reported in the last 24 hours; the most notable fixes are in cron runtime and filesystem listener behavior.

## 6. Feature Requests & Roadmap Signals

The backlog is dominated by new channel integrations and infrastructure, rather than user-facing agent features. Notable signals:

- **Channel expansion continues**: Requested channels include Twilio SMS (#6427), Zulip (#6437), Rocket.Chat (#6435), Mastodon (#6423), Lemmy (#6441), and a Slack Events API mode (#9022) for scale-to-zero deployments. All are accepted and marked `status:accepted` except the Slack mode.
- **Plugin/WASM infrastructure is a clear priority**: RFC #9810 (Agent Plugins 1.0 skill and MCP package loading) and RFC #10076 (comprehensive WASM plugin architecture) are strong signals for an "everything is a plugin" future. These align with the policy and sandboxing RFCs (#8424, #6996).
- **Governance is solidifying**: A new PR (#10288) defines deferred RFC vote cycles, ensuring the RFC process handles quorum failures predictably.

Given the high volume of accepted feature issues (`status:accepted`) and the steady pipeline, a next release is likely to include at least one of the new channels (Mastodon, Rocket.Chat, or Zulip), along with the security and memory fixes.

## 7. User Feedback Summary

Users are heavily focused on security posture and operational reliability. Expressed pain points:

- **Robust access control**: Users want workspace-relative forbidden paths (`.zeroclawignore`) (#8424), granular sandboxing (#6996), and protection against sensitive file leakage.
- **Operational scalability**: Users want Slack Events API support for scale-to-zero (#9022) and are frustrated with token-bound auto-pairing for ACP bridges (#6754).
- **Workflow context**: A recurring pain point is that the agent lacks context for the cron job it is running (#6105), breaking automations.

Visibility into the UI is also a concern, with a large RFC (#8132) proposing a rewrite of the React/Vite web UI in Rust→Wasm to eliminate Node.js from the build and runtime.

## 8. Backlog Watch

**Open, long-running RFCs and features that require maintainer review:**

- **#6850 — Memory lifecycle policy** (17 comments, created May 22) — High-traffic RFC with no maintainer response beyond `needs-author-action`; overdue for a maintainer decision.
- **#6996 — Granular sandbox policy** (11 comments, created May 28) — Accepted concept but still `needs-maintainer-review`; marked `in-progress` yet appears stalled.
- **#9109 — Native Hailo-Ollama support PR** (size:XL, created Jul 17) — A large provider-specific feature PR with label `needs-author-action`; tied to the filed bug #10272, suggesting test fixes are required before merge.
- **#9447 / #9999 — Anthropic / OpenAI-compatible terminal-response classification PRs** — Stacked PRs from trusted contributors, with #9999 `status:blocked` waiting for #9447 to land first. This stack is a critical provider-reliability improvement and deserves priority to avoid bit-rot.

The main bottleneck is the maintainer decision queue (#8692). With 13+ RFCs in various states of `needs-maintainer-review` or `needs-author-action`, the project health is good in terms of contributor activity but at risk of RFC sprawl and staleness if the queue is not actively drained.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*