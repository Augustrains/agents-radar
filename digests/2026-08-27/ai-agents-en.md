# OpenClaw Ecosystem Digest 2026-08-27

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-27 05:22 UTC

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

# OpenClaw Project Digest — 2026-08-27

## 1. Today's Overview

OpenClaw is showing extremely high activity, with **1,000 issues and PRs updated in the last 24 hours** (500 each). Of those, roughly **66% of issues remain open** (336) while **~42% of PRs were merged or closed** (211), indicating the maintainers are actively processing community contributions. No new releases were published today; the project is between **v2026.8.1-beta.3** and the next stable. The maintainer team (steipete, vincentkoc, jesse-merhi) is heavily engaged, authoring multiple large refactoring PRs while community bug reports continue to flood in, many tagged with maintainer-review labels and high-severity ratings. Priority-0 and Priority-1 issues related to message loss, data loss, and session-state integrity remain a central focus.

## 2. Releases

**No new releases were published in the last 24 hours.** The most recent beta remains **v2026.8.1-beta.3**, with the corresponding feedback issue (#125626) still open and actively collecting community input after 20 comments.

## 3. Project Progress

The maintainer team is executing on multiple large-scale refactors. Notable **merged/closed PRs (211 total)** include:

- **fix(models): keep Claude CLI OAuth available in Control UI** (#125471) — Fixes OAuth refresh ownership loss after Gateway restart, preventing stale auth profile entries from causing contradictory provider states.
- **fix(gateway): keep conversation delivery within agent bindings** (#126424) — Addresses multi-agent operators discovering delivery outside their agent binding scope, touched across 9 channel integrations (Discord, iMessage, Matrix, Mattermost, Slack, Telegram, Feishu).
- **feat(security): require acknowledgement for install policy warnings** (#116489) — Adds an interactive security gate where `security.installPolicy` can return `warn` for suspicious plugin/skill installs, requiring explicit operator confirmation.
- **feat(ui): review install policy warnings** (#120900) — Complementary Control UI flow enabling administrators to review and acknowledge install-policy warnings.
- **fix(release): authorize focused beta evidence** (#128371) — Resolves a beta.3 release blocker by allowing the release publisher to accept a focused validation manifest when only a subset of tests changed.

**Open, high-impact PRs in progress:**

- **refactor(state): consolidate wide rows, plugin index, workspace attestations, and shared auth singletons at schema v13** (#130466) — Large-scale storage layer cleanup removing stale redundant projections.
- **feat(browser): standalone extension relay daemon with native-host wake-up** (#128379) — Enables browser automation without a local Gateway serving the relay.
- **fix(telegram): prevent duplicate sends after delivery observer failures** (#130643) — Prevents duplicate replies if delivery bookkeeping throws errors post-acceptance.

## 4. Community Hot Topics

The most active issues reveal a strong focus on **delivery reliability and session-state integrity**:

- **#125626 — OpenClaw 2026.8.1 beta feedback** (20 comments) — The canonical beta feedback thread tracking release validation status and community-reported blockers.
- **#38327 — "Cannot convert undefined or null to object" with google-vertex/gemini-3.1-pro-preview** (14 comments, 3👍) — A high-severity regression dating to v2026.3.2 that remains unaddressed; users are still hitting this on the embedded agent path.
- **#53628 — ${XDG_CONFIG_HOME} not processed when installing a skill** (14 comments) — Environment variable interpolation bug in docker-based installs.
- **#43367 — Multi-agent orchestration is unstable** (13 comments) — Catalogues concurrent `agents add` config overwrites, session-lock failures, and detached child work — a P1 reliability cluster.
- **#87561 — Define durable final fallback delivery semantics across channels** (12 comments, maintainer-tagged) — Proposes a formal spec for what "delivered" means when channel delivery fails.
- **#113306 — SQLite snapshot restore lacks end-to-end crash and identity guarantees** (12 comments) — Data-loss risk flagged as P1.

**Most-reacted PRs:** #118750 (memory-core NaN-safe comparators), #77184 (plugin SDK type re-exports), #130205 (terminal receipt validation) — each receiving 1+ star reactions from the community.

## 5. Bugs & Stability

The issue tracker is heavily weighted toward **data-loss and message-loss regressions**, many with linked PRs but also many needing maintainer decisions:

**Critical (P0/P1, data-loss or message-loss):**

- **#48920 — Live Docs are ahead of release** (P0, 10 comments, 4👍) — Docs document `IsolatedSessions` not present in v2026.3.13; a UX release-blocker.
- **#113306 — SQLite snapshot restore lacks crash and identity guarantees** (P1, diamond lobster, 12 comments) — Can report success without durable parent-directory linking.
- **#83959 — Codex app-server startup retries exhaust before replacement server is ready** (P1, platinum hermit, 11 comments) — Crash-loop risk with the `codex` harness.
- **#94939 — 6.x migration leaves channel conversation-store SQLite empty** (P1, diamond lobster, 8 comments) — Orphans references, breaking proactive Microsoft Teams sends.
- **#92241 — Gateway holds stale module import paths after update/rollback** (P1, diamond lobster, 6 comments) — Inbound messages silently dropped (`ERR_MODULE_NOT_FOUND`).
- **#112259 — Visible inbound channel turn silently dropped** (P1, platinum hermit, 8 comments) — Zero-payload dispatch has no retry or dead-letter path.
- **#97616 — Zombie child processes leak (hooks/tools)** (P1, 9 comments) — Runtime degradation over time.
- **#114154 — bundle-mcp fails silently despite passing policy checks** (P1, 9 comments) — ToolSearch binding broken; no diagnostic output.

**High (P1, session-state):**

- **#43367 — Multi-agent concurrent config overwrites** (P1, 13 comments).
- **#71689 — Tasks registry restore fails on malformed SQLite** (P1, 6 comments).
- **#80498 — Premature/duplicate subagent completion announcements** (P1, 7 comments, 3👍).
- **#112248 — @openclaw/codex plugin fails to register (openSyncKeyedStore)** (P1, 6 comments).

**Active fix PRs:** #130537 (streamed function-name overwrite), #130643 (Telegram duplicate sends), #130701 (Codex stale resume conflicts), #129402 (Codex channel context preservation across hooks), #118750 (NaN-safe memory comparators), #93247 (idle state recovery).

## 6. Feature Requests & Roadmap Signals

The most-upvoted and most-discussed feature asks cluster around **agent self-awareness, memory architecture, and delivery durability**:

- **#60572 — Multi-Slot Memory Architecture** (8 comments, 3👍) — Multiple purpose-specific memory providers replacing the single-slot constraint.
- **#6757 — Agent-triggered context compaction** (8 comments, 2👍) — A self-compact tool allowing agents to manage their own context window.
- **#26037 — Ali Bailian coding plan support** (5 comments, 4👍) — Top-voted provider-extension request; high commercial demand signals.
- **#16555 — TTL/Expiry for Delivery Queue Messages** (8 comments) — Prevents stale outbound queue entries flooding channels on restart.
- **#40786 — .gitignore-like exclude patterns in backup CLI** (11 comments) — Security-adjacent UX improvement for backups.
- **#17840 — Reaction-triggered agent turns** (7 comments) — Interactive patterns (emoji-choice polling) via WhatsApp/Telegram reactions.
- **#20837 — Agent-aware communication channel** (5 comments) — Making the agent conscious of incoming message source.
- **#45415 — MEMORY.md size warning/limit enforcement** (5 comments, 1👍) — Data-preservation guard against silent truncation.
- **#71417 — Default --channel=last silently resumes most recent session** (5 comments) — Dangerous UX footgun; should be an explicit opt-in.

**Roadmap prediction:** The maintainer-tagged #87561 (durable final fallback delivery) and #113306 (snapshot guarantees) will likely define the next stable release's core stability story. The `security.installPolicy` `warn` path, already merged, will appear in the next release as a headline security feature.

## 7. User Feedback Summary

**What users are happy about:** The maintainers' rapid response to install-policy security feedback — two PRs (#116489, #120900) landed within weeks of the discussion — suggests good signal on security hardening. The active beta process (#125626) is generating visible product-decision involvement from maintainers.

**Pain points (recurring):**

- **Silent failures dominate:** Multiple top issues describe silent message drops (#112259, #92241), silent migration consequences (#94939, #90378), and silent session resumption (#71417). Users repeatedly express that a **failure that is quiet is worse than an explicit error**.
- **Non-deterministic multi-agent behavior:** #43367, #80498, #114154 show the same theme — concurrent agents stepping on each other's state, losing messages, or completing prematurely.
- **Migration trauma:** v5.x → v6.x and v6.x minor migrations continue to cause data loss or misconfiguration (cron store, conversation stores, tasks registry).
- **Provider-specific breakage:** The google-vertex bug (#38327) has been open for 5 months with 14 comments — a long-running dissatisfaction for a major cloud provider.
- **Process hygiene:** Zombie processes (#97616) and stale node.exe processes (#74378) reflect poor CLI lifecycle on Windows/macOS.

**Sentiment:** Frustrated but engaged. Users are filing detailed, well-structured repros with source-level investigation, which the maintainer tags (`clawsweeper:source-repro`) confirm are being triaged by automated sweeps.

## 8. Backlog Watch

Items needing maintainer attention or decision (tagged, long open, high severity):

- **#38327 — google-vertex/gemini crash** (P1, 14 comments, open since March 2026) — 5 months without a fix PR; currently tagged `needs-maintainer-review`.
- **#16555 — Delivery Queue TTL** (P1, 8 comments, open since February 2026) — Long-standing reliability gap; `needs-product-decision`.
- **#94939 — CS conversation store empty** (P1, 8 comments, open since June 2026) — Linked PR is open but the issue is still awaiting decision.
- **#83959 — Codex app-server startup exhaustion** (P1, 11 comments, open since May 2026) — Tagged `clawsweeper-recovery-stuck`.
- **#56692 — Group chat context blurring** (P2, platinum hermit, 8 comments, open since March 2026) — UX-affecting, tagged `recovery-stuck`.
- **#6747 — MEMORY.md truncation** (P3, 5 comments) — Low priority but data-loss risk; a quick win for trust.
- **#60772 — Multi-slot memory** (P3, 8 comments, 3👍) — High user enthusiasm, no maintainer acknowledgment beyond `needs-product-decision`.
- **#14747 — configurable lane-wait threshold** (P3, open since February) — Simple config knob, low-risk fix that could help many cron-heavy workloads.

**Backlog bias:** Many highest-signal issues (diamond/platinum lobster ratings) are blocked on `needs-product-decision` or `needs-maintainer-review`, suggesting the automation is working but **human capacity is the bottleneck**.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparative Analysis: Personal AI Assistant & Agent Ecosystem

**Date: 2026-08-27**

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is characterized by intense competition and rapid innovation, with projects at wildly different maturity stages—from the mature, high-volume OpenClaw and Hermes Agent to relatively quiet niche players like NullClaw and TinyClaw. Across the ecosystem, there is a strong convergence on core challenges: **delivery reliability, multi-agent state consistency, and context/window memory management**, with users consistently prioritizing silent-failure elimination over new features. Security hardening (SSRF, command injection, install-policy gates) and provider ecosystem resilience (OpenAI-family prompt caching, MCP OAuth quirks, TLS stacks) are emerging as table-stakes differentiators. Meanwhile, feature demand clusters around multi-slot memory architectures, realtime voice interaction, persistent sandboxes, and multi-tenant/governance controls, signaling a mature user base pushing beyond basic chat into production-grade autonomy.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Merged/Closed | Release Status | Health Score* |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 211 PRs / 336 issues open | Between v2026.8.1-beta.3 and next stable | **8.5/10** — High velocity, but P0/P1 data-loss bugs cluster |
| **Hermes Agent** | 50 | 50 | 9 PRs | v0.20.5 (no new) | **7/10** — Responsive, but critical MCP stdio regression widespread |
| **NanoBot** | 1 | 32 | 17 PRs | No new | **8/10** — Strong sprint, excellent merge rate, few issues |
| **IronClaw** | 27 | 50 | 48 PRs | **v1.4.0-rc.1** (new) | **8.5/10** — Pre-release stabilization, strong discipline |
| **CoPaw** | 33 | 45 | 28 PRs | **v2.2.0-beta.1** (new) | **8/10** — Hardening phase, critical Windows bug (no fix yet) |
| **ZeroClaw** | 26 | 50 | 3 PRs | v0.8.5 stabilization, v0.9.0 milestone | **7/10** — Healthy but maintainer bandwidth is bottleneck |
| **PicoClaw** | 7 | 5 | 3 PRs | v0.3.1 (no new) | **7/10** — Stable, slow burn-in of v0.3.1 |
| **NanoClaw** | 1 | 24 | 6 PRs | No new | **7.5/10** — Active contributor base, critical silent failure open |
| **LobsterAI** | 2 | 16 | 15 PRs | Imminent (release/2026.8.26) | **8.5/10** — Excellent polish cycle, calm bug surface |
| **Moltis** | 0 | 0 | 2 PRs | **20260826.01** (released) | **8/10** — Low but steady, clearing backlog |
| **NullClaw** | 1 | 0 | 0 | nullclaw 2025.5.29 (old) | **5/10** — Quiet, could be in RC phase or understaffed |
| **TinyClaw** | — | — | — | No activity | **N/A** |
| **ZeptoClaw** | — | — | — | No activity | **N/A** |

*Health score derived from merge velocity, regressions vs. fixes, maintainer responsiveness, and backlog cleanliness.

---

## 3. OpenClaw's Position

**Advantages:**
- **Scale of Community & Ecosystem:** With 500+ issues/PRs updated daily, OpenClaw dwarfs every competitor by an order of magnitude. This generates a robust feedback loop and a vast plugin/skill ecosystem that smaller projects cannot replicate.
- **Maintainer Engagement:** steipete, vincentkoc, and jesse-merhi are aggressively executing multi-file refactors and security features (e.g., install-policy `warn` gate landed within weeks), while other projects (ZeroClaw, NanoClaw) visibly struggle with maintainer review bottlenecks.
- **Proactive Reliability Investment:** The explicit focus on P0/P1 data-loss issues (snapshot restore guarantees, durable delivery fallback semantics) is more formalized than in peers, suggesting a maturing stability doctrine.
- **Security First-Mover:** Requiring explicit operator acknowledgment for install-policy warnings (#116489, #120900) sets a UX-and-security precedent that others (NanoClaw's command-injection fix, IronClaw's TOCTOU fixes) are only now reaching.

**Technical Approach Differences:**
- OpenClaw's approach to **channel integrations** is the most extensive (9+ integrations touched in a single delivery-scope PR), indicating a "cover-the-world" integration strategy versus IronClaw's more selective channel focus (Slack, Telegram) or NanoBot's TUI/WebUI-centric architecture.
- OpenClaw's **multi-agent orchestration** is a major architectural theme, whereas peers like Moltis focus on single-tenant model preference management.
- OpenClaw is **schema-heavy** (consolidating to schema v13, SQLite-backed snapshots), in contrast to NanoBot's Pythonic/Actor-model and IronClaw's Rust-based sandbox-heavy design.

**Community Size Comparison:**
- OpenClaw: Extremely large, high-velocity, formalized RFC/tracker processes, but with a human-capacity bottleneck on maintainer decisions.
- Hermes Agent, ZeroClaw: Large communities with strong contributor pipelines, but more vulnerable to decision stalls and duplicate issue reports.
- IronClaw, CoPaw: Mid-to-large communities with strong corporate backing (Near AI, agentscope-ai).
- NanoBot, NanoClaw, PicoClaw: Smaller but highly engaged contributor bases; NanoBot shows the healthiest contributor-to-maintainer ratio.
- Moltis, NullClaw, LobsterAI, TinyClaw, ZeptoClaw: Low-activity niches; NullClaw/TinyClaw/ZeptoClaw may be dormant or pre-release.

---

## 4. Shared Technical Focus Areas

| Requirement | Projects | Specific Need |
|---|---|---|
| **Eliminate Silent Failures** | OpenClaw (#112259, #92241), NanoClaw (#3568), CoPaw (#6921), Hermes (#94335) | Users consistently rank "quiet failure" as worse than a crash. Demand for explicit error paths, dead-letter queues, and retry visibility. |
| **Realtime / Voice Interaction** | ZeroClaw (#8780 Gemini Live), Hermes (#77111 RealtimeVoiceProvider, #95193), OpenClaw (Voice/Telegram voice notes) | Multiple RFCs and competing PRs for speech-to-speech and duplex voice. Need for a standard ABC/broker contract. |
| **Prompt & Context Cost Control** | IronClaw (#7891, #7921), CoPaw (#7335), OpenClaw (#38327, #71689) | Prompt bloat from unprojected payloads, prompt-cache collapse on OpenAI-family, context-window management across long sessions. |
| **Memory Architecture** | OpenClaw (#60572 multi-slot memory), CoPaw (#7252 OpenViking), IronClaw (memory-core comparators), NanoBot (usage tracking) | Users want purpose-specific memory providers beyond a single MEMORY.md / single-slot constraint. |
| **Persistent Sandbox / Workspace** | IronClaw (#7732 persistent per-user sandbox), CoPaw (#7194 workspace cancellation-safety), OpenClaw (SQLite snapshots) | Per-command or ephemeral containers are insufficient; need durable, per-tenant state. |
| **MCP Robustness** | Hermes (#94335 stdio liveness), Moltis (#1244 OAuth scopes), OpenClaw (#114154 bundle-mcp fails), ZeroClaw (#10394 MCP result storage) | Real-world integration quirks (stdio, OAuth, tool results) are dominating bug reports across all projects. |
| **Security Hardening** | OpenClaw (install-policy gates, OAuth), IronClaw (TOCTOU fixes, TLS seams), NanoClaw (#3550 command injection), ZeroClaw (#10070 SSRF) | SSRF, symlink races, command injection via shell substitution, and install-policy acknowledgments are converging priorities. |
| **Multi-Agent / Multi-Tenant Governance** | CoPaw (#7318 Hub multi-tenant), OpenClaw (#43367 orchestration stability), ZeroClaw (per-group MCP policy), LobsterAI (sharing/permissions) | Growing demand for RBAC, per-group tools, and stable concurrent-agent behavior. |
| **Multi-Channel Availability** | OpenClaw (9 integrations), PicoClaw (Telegram topics, Slack media), ZeroClaw (Microsoft Teams PR), IronClaw (Telegram/Slack bots) | Users expect deep chat-platform integration (Slack, Teams, Telegram, IRC) with rich media and topics. |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target User | Architectural Core | Key Differentiator |
|---|---|---|---|---|
| **OpenClaw** | The "everything" assistant | Power users, homelab, multi-agent ops | Node.js/TypeScript, schema-heavy SQLite, 9+ channels | Dominant ecosystem size and integration breadth |
| **Hermes Agent** | Desktop-centric, multi-gateway agent | Individual power users, cross-device | Python, MCP-heavy stdio tooling, Gateway/Desktop split | Strong desktop UX, telemetry, MCP depth |
| **NanoBot** | Engineering-mindset TUI/WebUI agent | Developers, CLI-first | Python, TUI (Bun/React), WebSocket sessions | Exceptional test discipline, contributor hygiene |
| **IronClaw** | Secure, sandboxed cloud agent | Enterprise/cloud, infrastructure-heavy | Rust, per-user sandboxes, proxy, MCP framework | Security/Sandbox rigor, performance measurement culture |
| **CoPaw** | Multi-agent hub & deployment | Teams, Chinese-market (WeChat), MCP/OpenAI | Python backend, QwenPaw Hub (multi-tenant), Windows desktop | Qwen integration, Windows installer focus, Hub governance |
| **ZeroClaw** | Async, event-driven assistant | Developers, Zed/TUI users | Rust, ZeroCode/ZeroRelay, Gemini Live RTC | Realtime voice + TUI + architecture RFC culture |
| **NanoClaw** | Lightweight, chat-platform native | Self-hosters, Mattermost/Matrix | Node.js, SQLite, Mattermost-first | Mattermost reliability, channel-specific polish |
| **PicoClaw** | Lightweight, home/edge deployment | Raspberry Pi, home automation | Go, IRC/Telegram/LINE/Slack focus | Low-resource friendliness, multi-channel bots |
| **LobsterAI** | Polished desktop/mobile AI client | Mainstream consumer, Chinese-market | Electron? (sidebar/UI focus), cloud library | UI polish, analytics, cloud sharing |
| **Moltis** | Provider-agnostic chat assistant | Privacy-focused, multi-MCP users | Python, LLM-agnostic, MCP discovery | Provider/model preference granularity, MCP OAuth |
| **NullClaw** | Minimalist CLI agent | CLI purists | Unknown (low activity) | Symlink support, dotfile integration |
| **TinyClaw / ZeptoClaw** | Inactive/niche | — | — | — |

---

## 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating (High-Velocity, Pre-Release)**
- **IronClaw** (v1.4.0-rc.1, 48 PRs merged in 24h) — Steroid release cycle, exceptionally disciplined.
- **CoPaw** (v2.2.0-beta.1, 28 PRs merged) — Multi-tenant Hub launch imminent; intense hardening.
- **OpenClaw** (500 PRs/24h, 211 merged) — Unmatched scale; the "moving bus" of the ecosystem.
- **LobsterAI** (15 PRs merged, release imminent) — Efficient, polish-focused sprint.

**Tier 2: Steady Shipment**
- **NanoBot** (17 PRs merged) — Excellent contributor cadence, low bug surface.
- **ZeroClaw** (3 merged, 47 open) — Large community, but maintainer review is the bottleneck.
- **Hermes Agent** (9 merged) — Responsive but wrestling with a mass-impacting MCP regression.
- **NanoClaw** (6 merged) — Active contributor base; core-team bandwidth varies.
- **PicoClaw** (3 merged) — Modest but healthy; v0.3.1 still burning-in.
- **Moltis** (2 merged) — Low volume, but clearing long-debt issues.

**Tier 3: Quiet / Stabilizing**
- **NullClaw** — Single issue, zero PRs. Possibly pre-release.
- **TinyClaw / ZeptoClaw** — No activity for 24h+. Watch for dormancy.

---

## 7. Trend Signals

1. **"Checkpointing" is the new must-have:** Across OpenClaw (snapshot restore), IronClaw (persistent sandboxes), and CoPaw (session reliability), the assumption of a long-lived, continuously-running process is giving way to **durable, restorable state** — crash-proof checkpoints and offline/online session migration are becoming core features.

2. **The "zero-silent-failure" doctrine is non-negotiable:** Reports from OpenClaw, NanoClaw, CoPaw, and IronClaw all converge on the same user complaint: **a quiet failure (dropped message, stuck UI, ignored command) is the fastest way to lose user trust.** LLM agents' non-deterministic behavior makes explicit, surfaced error paths the new competitive battleground.

3. **MCP is the de facto standard, but also the main point of failure:** MCP integration bugs (stdio liveness, OAuth scopes, tool-result envelopes, protocol version negotiation) are the most consistent cross-project bug category. Expect a wave of "MCP hardening" releases as projects move from "we support MCP" to "we support MCP reliably."

4. **Performance is measured in pennies, not seconds:** IronClaw (#7921 prompt-cache collapse), CoPaw (#7335 hit-rate observability), and OpenClaw (NaN-safe comparators) all signal a shift toward **cost-per-token and cache-hit-rate as first-class product metrics**, driven by users running high-volume, production-grade workloads.

5. **Realtime voice is the next frontier:** ZeroClaw's RFC for Gemini Live and Hermes' RealtimeVoiceProvider ABC are early signals that **speech-to-speech interaction is shifting from novelty to core roadmap**, likely driven by the latest frontier model capabilities.

6. **Security is now a feature, not a checklist:** Install-policy acknowledgment gates (OpenClaw), TOCTOU fixes (IronClaw), SSRF hardening (ZeroClaw), and command-injection patches (NanoClaw) indicate that **users are demanding auditable, secure-by-default agent behavior**—and are filing detailed security repros when they find gaps.

7. **Governance and multi-tenancy are mid-tier differentiators:** CoPaw's Hub, ZeroClaw's per-group MCP policies, and OpenClaw's multi-agent orchestration all point to a future where assistants are deployed **not as single-user toys, but as team infrastructure**.

---

*For AI agent developers, the actionable takeaways are: (1) prioritize explicit, surfaced errors over silent handling; (2) invest in durable, restorable session state; (3) treat MCP integration as a first-class engineering surface with dedicated testing; (4) measure and optimize cost-per-token; and (5) design for secure, multi-tenant deployment from day one.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date: 2026-08-27**

---

## 1. Today's Overview

NanoBot shows a very high activity day with 32 pull requests updated in the last 24 hours, of which 17 were merged or closed and 15 remain open. The project appears to be in a sustained development sprint, with a strong focus on agent lifecycle reliability, WebSocket stability, TUI/WebUI polish, and architectural refactoring. Only one issue was updated (a closed bug about `read_session` wildcard queries), which is notably low compared to PR volume—suggesting that most work is being driven by an active contributor group rather than user-reported problems. No new releases were published today. The consistently high merge rate (17 of 32 PRs) indicates a well-functioning review pipeline and healthy project momentum.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release information is not available in this data window.

---

## 3. Project Progress

### Merged/Closed PRs Today (Selected Highlights)

**Agent Core & Lifecycle**
- **[#5556](https://github.com/HKUDS/nanobot/pull/5556) — fix(agent): complete native reasoning lifecycle.** Closes provider-native reasoning before answer content, local tool execution, hosted tool events, stream recovery, and request completion. Keeps reasoning lifecycle state local to one provider request while preserving hook ownership of inline `<think>` parsing.
- **[#5555](https://github.com/HKUDS/nanobot/pull/5555) — refactor(agent): remove duplicate progress streaming path.** Removes the unused `AgentRunSpec.progress_callback` input and the runner's second provider-streaming state machine, consolidating reasoning, answer deltas, tool hints, and provider-hosted tool events onto the existing per-run hook path.
- **[#5546](https://github.com/HKUDS/nanobot/pull/5546) — refactor(agent): make run usage explicit.** Returns `AgentRunResult` from the agent loop boundary, removes the process-wide `AgentLoop._last_usage` side channel, and makes usage capture a per-run hook while `/status` reads session-scoped usage.

**TUI Improvements**
- **[#5557](https://github.com/HKUDS/nanobot/pull/5557) — perf(tui): skip redundant dependency installs.** Caches successful source-TUI dependency installs using a SHA-256 fingerprint of `tui/package.json` and `tui/bun.lock`; skips `bun install --frozen-lockfile` when the fingerprint matches.
- **[#5534](https://github.com/HKUDS/nanobot/pull/5534) — feat(tui): autocomplete skill references.** Enables `$skill-name` autocompletion in the TUI composer with a filtered picker, arrow navigation, Enter/Tab insertion, and caret-aware completion.
- **[#5538](https://github.com/HKUDS/nanobot/pull/5538) — refactor(tui): clarify active composer actions.** Replaces "Steer this turn…" with a responsive action hint: `Enter send now · Tab send next`.

**WebUI & Gateway**
- **[#5548](https://github.com/HKUDS/nanobot/pull/5548) — refactor(webui): isolate websocket application orchestration.** Moves reconnect hydration into `WebUISessionProjection` and `WebUIOutboundProjector`, routing semantic outbound runtime events and typed inbound envelopes through dedicated components.
- **[#5544](https://github.com/HKUDS/nanobot/pull/5544) — fix(gateway): recover degraded WebSocket listener.** Makes WebSocket running state and listening logs follow successful bind; supervises and rebinds recoverable listener failures with capped exponential backoff.
- **[#5543](https://github.com/HKUDS/nanobot/pull/5543) — fix(tui): surface chat connection failures.** Distinguishes quiet initial readiness, health-confirmed recovery, sustained unavailability, and unrecoverable service failure; queries the `/health` endpoint after connection failures.
- **[#5519](https://github.com/HKUDS/nanobot/pull/5519) — fix(webui): compact single-pane chat header.** Compresses header spacing, adds a model-settings entry to the model picker, and softens the composer boundary.

**Tools & Performance**
- **[#5533](https://github.com/HKUDS/nanobot/pull/5533) — fix(tools): keep find_files scans responsive.** Runs the complete scan in a worker, replaces repeated pathlib metadata calls with budgeted `os.scandir` traversal, and propagates cancellation.

**Usage & Telemetry**
- **[#5481](https://github.com/HKUDS/nanobot/pull/5481) — feat(usage): add unified provider usage backend.** Records one content-free usage row for every retry-managed provider attempt made by gateway-managed WebUI/TUI sessions.

**WebUI**
- **[#5491](https://github.com/HKUDS/nanobot/pull/5491) — fix(webui): keep answer text outside reasoning shell.** Preserves every assistant answer slice across answer → tool → answer turns; keeps explicit reasoning/tool activity inside the activity surface while merging answer slices into one final message.

---

## 4. Community Hot Topics

The most active items by discussion volume (comments/reactions data was sparse for this window, so activity is inferred from update recency, open/closed state, and scope):

- **[PR #5234](https://github.com/HKUDS/nanobot/pull/5234) — feat(agent): integrate mst-python as a metasearch provider** (OPEN, priority: p1). A long-running feature PR (since Aug 3) that adds Meta-Search Tool (mst) as a new web search provider, aggregating results from DuckDuckGo, Google, Brave, Bing with Reciprocal Rank Fusion (RRF). Its extended open period (25 days) with continued updates suggests it is a substantive, carefully-reviewed addition.

- **[PR #5553](https://github.com/HKUDS/nanobot/pull/5553) — fix(agent): hold goal continuation after a failed completion attempt** (OPEN, priority: p1, conflict flag). Aims to stop re-injecting goal-continue messages after a malformed completion attempt fails, preventing infinite continuation loops. The "conflict" flag suggests merge conflicts need resolving—this area needs maintainer attention.

- **[PR #5504](https://github.com/HKUDS/nanobot/pull/5504) — fix(ui): surface model retry status (NAN-34)** (OPEN, priority: p2, conflict). Wants to expose sanitized model retry lifecycle events to WebSocket clients with TUI/WebUI countdown rendering. Addresses a clear UX gap: users are currently blind to model retry attempts.

- **[PR #5364](https://github.com/HKUDS/nanobot/pull/5364) — feat(webui): add temporary side conversations** (OPEN, priority: p2, conflict). Would add `/side` to open transient side conversations beside the current WebUI topic with tab switching and parallel sending. This is a user-visible feature with broad appeal that has been open since Aug 13 and carries a conflict flag.

**Underlying needs:** The open PRs point to user demand for (1) better visibility into model behavior (retry status, failure surfacing), (2) more powerful search provider options, (3) multi-tasking via side conversations, and (4) robust sustained-goal behavior without runaway loops.

---

## 5. Bugs & Stability

Only one new issue was reported today, but merged fixes address several stability concerns:

| Severity | Issue/PR | Description | Status |
|----------|----------|-------------|--------|
| **Medium** | [#5550](https://github.com/HKUDS/nanobot/issues/5550) (CLOSED) | `read_session` tool returns empty history when models use wildcard queries (`"*"`, `".*"`, whitespace) for the optional filter | Closed; no comments—likely fixed by a related change |
| **High (fixed)** | [#5544](https://github.com/HKUDS/nanobot/pull/5544) (MERGED) | Degraded WebSocket listener could leave the gateway in a false "running" state; now supervised with capped exponential backoff | Fixed |
| **Medium (fixed)** | [#5553](https://github.com/HKUDS/nanobot/pull/5553) (OPEN) | Sustained goals can loop forever after a failed completion attempt—the runner re-injects goal-continue messages even when the completion failed | Fix proposed, needs merge |
| **Medium (fixed)** | [#5533](https://github.com/HKUDS/nanobot/pull/5533) (MERGED) | `find_files` scans could block the event loop; moved to worker thread with budgeted scandir traversal | Fixed |
| **Low (fixed)** | [#5491](https://github.com/HKUDS/nanobot/pull/5491) (MERGED) | WebUI rendered answer text inside the reasoning shell, mixing content boundaries | Fixed |

**Overall stability assessment:** The project is healthily responsive to bugs—several fixes landed within 1–2 days of issue reports. The WebSocket listener recovery fix and the goal-continuation fix are the most impactful stability changes today.

---

## 6. Feature Requests & Roadmap Signals

**Features merged/landed recently:**
- **Unified provider usage backend** ([#5481](https://github.com/HKUDS/nanobot/pull/5481)) — provides a single usage-recording path for gateway-managed sessions; likely groundwork for usage dashboards/billing.
- **TUI skill reference autocompletion** ([#5534](https://github.com/HKUDS/nanobot/pull/5534)) — improves TUI discoverability of skills.
- **TUI action hint clarity** ([#5538](https://github.com/HKUDS/nanobot/pull/5538)) — small UX polish.

**Features in flight (likely candidates for next version):**

1. **Metasearch provider (mst-python)** — [PR #5234](https://github.com/HKUDS/nanobot/pull/5234) is a priority-p1, feature-complete PR that has been iterating for ~3 weeks. Likely to be merged once review completes.
2. **WebUI side conversations** — [PR #5364](https://github.com/HKUDS/nanobot/pull/5364) is a substantial user-facing feature; the conflict flag needs resolving but the feature is likely desired.
3. **Model retry status surfacing** — [PR #5504](https://github.com/HKUDS/nanobot/pull/5504) addresses a clear UX gap (users don't know when models are retrying).
4. **Langfuse tracing for Codex** — [PR #5520](https://github.com/HKUDS/nanobot/pull/5520) would bring observability parity to the Codex provider.

**Roadmap signals:** The recent refactors (unified usage backend, explicit run usage, isolated WebSocket orchestration) suggest the project is preparing for a more mature multi-provider, multi-session architecture—possibly billing/usage dashboards, better observability, and more robust session management in the next minor release.

---

## 7. User Feedback Summary

- **Active community contribution:** All 15 open PRs are from community contributors (chengyongru, yonghuname, shakewingo, goodtiding5, akinolur, KDB-Wind, Re-bin, bingqilinweimaotai), showing strong external engagement.

- **Pain points being addressed:**
  - **Model retry invisibility** — users can't tell whether the model is retrying or stalled; addressed in [#5504](https://github.com/HKUDS/nanobot/pull/5504).
  - **Sustained goal loops** — a user-affecting bug where failed goal completions cause repeated continuation attempts; addressed in [#5553](https://github.com/HKUDS/nanobot/pull/5553).
  - **Wildcard session queries** ([#5550](https://github.com/HKUDS/nanobot/issues/5550)) — models calling `read_session` with `"*"` or whitespace queries get empty history, which can degrade multi-session context-aware conversations.
  - **WebUI/TUI organization** — users want compact layouts (fixed in [#5519](https://github.com/HKUDS/nanobot/pull/5519)), clear action hints (fixed in [#5538](https://github.com/HKUDS/nanobot/pull/5538)), and connection failure visibility (fixed in [#5543](https://github.com/HKUDS/nanobot/pull/5543)).

- **Satisfaction indicators:** Rapid merge cycle, community members filing PRs with detailed summaries and tests, and cross-contributor collaboration (chengyongru handling many refactors) all indicate a healthy, satisfied user/contributor base.

---

## 8. Backlog Watch

Items that have been open for extended periods without closure:

| Item | Age (days) | Priority | Status / Concern |
|------|-----------|----------|------------------|
| **[PR #5234](https://github.com/HKUDS/nanobot/pull/5234)** — mst-python metasearch provider | 24 days | p1 | Substantial feature; still open after 3+ weeks despite being p1. Needs maintainer review or explicit deferral. |
| **[PR #5364](https://github.com/HKUDS/nanobot/pull/5364)** — WebUI side conversations | 14 days | p2 | Conflict flag set; needs rebase/conflict resolution from maintainer or contributor. |
| **[PR #5257](https://github.com/HKUDS/nanobot/pull/5257)** — Bound sustained-goal continuation when idle | 22 days | p2 | Conflict flag; overlaps conceptually with [#5553](https://github.com/HKUDS/nanobot/pull/5553) which is newer but similar scope. Maintainers should consolidate these. |
| **[PR #5339](https://github.com/HKUDS/nanobot/pull/5339)** — Reject discarded temporary chat messages | 16 days | — | Conflict flag; security-adjacent fix for a race condition in temporary chat persistence. |
| **[PR #5520](https://github.com/HKUDS/nanobot/pull/5520)** — Langfuse tracing for Codex | 3 days | p2 | New; but involved (native SDK integration) and may need review waiting time. |
| **[PR #5504](https://github.com/HKUDS/nanobot/pull/5504)** — Surface model retry status | 3 days | p2 | Conflict flag set; likely needs rebase after recent refactors. |

**Maintainer attention needed:** Conflict-flagged PRs ([#5553](https://github.com/HKUDS/nanobot/pull/5553), [#5504](https://github.com/HKUDS/nanobot/pull/5504), [#5364](https://github.com/HKUDS/nanobot/pull/5364), [#5339](https://github.com/HKUDS/nanobot/pull/5339), [#5257](https://github.com/HKUDS/nanobot/pull/5257)) are accumulating; a rebase/merge pass would prevent contributor fatigue. The sustained-goal behavior has two overlapping PRs that should be reviewed together.

---

**Overall Health Assessment:** NanoBot is in a strong development phase with high throughput, active community contribution, and rapid bug-fix cycles. The main risks are (1) accumulating conflict-flagged PRs needing merge passes, and (2) the p1 metasearch PR remaining open for 3+ weeks despite priority status. No critical regressions or user-reported crashes appeared in this window.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-27

## 1. Today's Overview

Project activity is **high**, with 50 issues and 50 PRs updated in the last 24 hours. The maintenance campaign for desktop persistent multi-gateway connections (#94724) is reported complete with 27 PRs merged. However, a **critical, mass-impacting regression** is dominating attention: the `_stdio_children_dead()` inverted liveness check (#94335, #94637, #95165, #95150) is causing all stdio MCP tool calls to fail fast, with at least four duplicate reports. PRs are flowing steadily (9 merged/closed today), including a fresh wave of telemetry, session-state safety, and cross-gateway room features. Overall project health shows a responsive maintainer community, but the MCP regression and several Windows-specific desktop issues remain urgent open concerns.

## 2. Releases

No new releases published in the last 24 hours. The project remains at v0.20.5 per recent issue reports.

## 3. Project Progress

Today's merged/closed PRs (9 total) cover:

- **[#96098] Test-suite isolation standard** — Implements standardized test isolation per `TEST-ISOLATION.md` with import-time sandboxing.
- **[#96091] Token/cost usage metrics export** — Adds `hermes.*` metrics for model spend per user via OTLP, improving cross-tool observability.
- **[#95589] Windows desktop update hang fix (closed)** — The zombie-process update hang issue was resolved.

**Notable open PRs advancing features:**

- **[#96095]** `hermes serve` no longer loses in-memory sessions when killed mid-update (fixes reopened tracker #94724).
- **[#96097]** Prevents Telegram flood recovery from duplicating streamed final messages.
- **[#96092]** Prevents the empty-session sweep from deleting archived transcripts.
- **[#96088]** Security fix: Feishu privileged card clicks now authorized by operator, not group policy (fixes #96045).
- **[#96087]** Phase 1 admin/user tool-tier whitelist, salvaging RFC #20744.
- **[#95965 / #95966 / #95967]** Stacked drafts for cross-gateway RoomLink to keep Bot rooms running without Desktop.

## 4. Community Hot Topics

**Most active issues (by comments):**

- **[#94335 — _stdio_children_dead() inverted liveness check (13 comments)](https://github.com/NousResearch/hermes-agent/issues/94335)** — P1 bug breaking ALL stdio MCP calls. Root cause identified. This is the dominant community pain point right now.
- **[#93888 — Remote Gateway session restore failure (12 comments)](https://github.com/NousResearch/hermes-agent/issues/93888)** — Desktop sends local runtime ID to remote gateway; sessions permanently un-restorable.
- **[#94637 / #95165 / #95150 — Duplicate MCP stdio failures (10/2/2 comments)](https://github.com/NousResearch/hermes-agent/issues/94637)** — Same root cause as #94335, confirming wide impact across OSes.
- **[#94724 — Multi-gateway campaign tracker (8 comments)](https://github.com/NousResearch/hermes-agent/issues/94724)** — Campaign declared complete, but reopened for legacy-session migration and serve flush gap.
- **[#95589 — Windows update hang (8 comments)](https://github.com/NousResearch/hermes-agent/issues/95589)** — Now closed as fixed.

**Underlying needs:** The MCP regression cluster indicates heavy real-world reliance on stdio MCP servers; the fast-fail behavior makes many setups completely unusable. The multi-gateway session issues reveal growing multi-device/multi-backend usage patterns where state consistency is critical.

## 5. Bugs & Stability

**Critical (P1, active, wide impact):**

- **[#94335 (+3 duplicates)](https://github.com/NousResearch/hermes-agent/issues/94335) — MCP stdio fast-fail regression** — Inverted liveness check returns `True` (dead) for alive children; every stdio MCP call fails with "subprocess has exited." Introduced by #81995 fail-fast machinery. No fix PR yet — **top priority**.
- **[#93888 — Remote Gateway session restore broken](https://github.com/NousResearch/hermes-agent/issues/93888)** — Desktop sends local 8-char runtime ID to remote gateway; sessions permanently stuck on "Session not found." No fix PR identified.
- **[#94248 — Gateway SIGSEGV on delegate deadlines (macOS)](https://github.com/NousResearch/hermes-agent/issues/94248)** — 12 crash reports; crashes 17–72 ms after 600s delegate deadlines with Codex SSL reads.
- **[#95816 — Telegram gateway hangs at "Connecting" ](https://github.com/NousResearch/hermes-agent/issues/95816)** — v0.20.5; marked duplicate.

**High (P2):**

- **[#95589 — Windows update hang (closed)](https://github.com/NousResearch/hermes-agent/issues/95589)** — Resolved; zombie process after update no longer occurs.
- **[#95294 — Interrupted update leaves stale code forever](https://github.com/NousResearch/hermes-agent/issues/95294)** — Receipt records skew but nothing repairs it. Related fix in PR #96095 for session flush.
- **[#95188 — Deleted profile resurrects (Windows)](https://github.com/NousResearch/hermes-agent/issues/95188)** — Via stale `lastProfileByConnection` + cron-ticker shell.
- **[#95327 — In-flight turn killed by backend respawn](https://github.com/NousResearch/hermes-agent/issues/95327)** — 282 reaps, 213 respawns; bare "Operation interrupted" placeholder.
- **[#96073 — Auxiliary 503 never triggers provider fallback](https://github.com/NousResearch/hermes-agent/issues/96073)** — Vendor outage degrades task instead of switching.

**Fix PRs available:** #96095 (serve session flush), #96097 (Telegram duplicate finals), #96092 (archived transcript deletion), #96088 (Feishu auth boundary).

## 6. Feature Requests & Roadmap Signals

**Strong roadmap signals (multiple related items):**

- **[#5320 — Auto-scale memory_char_limit defaults](https://github.com/NousResearch/hermes-agent/issues/5320)** — Open since April; 8 comments, 2 upvotes. Curated memory limits too small; likely candidate for next release.
- **[#77111 — RealtimeVoiceProvider ABC](https://github.com/NousResearch/hermes-agent/issues/77111)** — Four competing duplex-voice PRs; maintainers may need to design an ABC + orchestrator per AGENTS.md.
- **[#49167 — Tool-level approval gating for MCP](https://github.com/NousResearch/hermes-agent/issues/49167)** — Extension of terminal approval to MCP tools; aligns with security-focused PR #96088.

**New feature PRs likely to land soon:**

- Telemetry: PR #95278 (opt-in metrics exporter) and #96091 (token/cost metrics) — telemetry infrastructure is maturing.
- Cross-gateway Bot rooms: PR #95965/66/67 stack — ambitious feature to run Bot groups without Desktop; needs-decision flagged.
- Mobile voice conversation (PR #95193) and Slack bounded history context (PR #96089).

## 7. User Feedback Summary

**Pain points:**

- **MCP reliability is the #1 complaint** — Multiple users report complete unusability of stdio MCP servers due to the fast-fail regression. One user (@cloudsthunder) notes direct spawn works fine, isolating the bug to the liveness check.
- **Windows desktop instability** — Update hangs, profile resurrection, in-flight turn kills, and runtime-not-ready states point to platform-specific process lifecycle issues.
- **Session/state consistency across gateways** — Users with multi-gateway setups face permanent session loss, stale code, and broken restores after sleep or interruption.

**Satisfaction signals:**

- Maintainers are responsive: the Windows update hang was closed within a day.
- The multi-gateway campaign completed with 27 PRs merged, showing sustainable feature delivery.
- The test-isolation standard (#96098) indicates strong engineering hygiene investment.

## 8. Backlog Watch

Long-unanswered or at-risk items needing maintainer attention:

- **[#5320 — memory_char_limit defaults (open since Apr 5, 9 comments)](https://github.com/NousResearch/hermes-agent/issues/5320)** — 4.5 months old; long-running sessions frequently hit limits. Low-effort, high-impact config change.
- **[#54945 — Mem0 OSS setup flags rejected by argparse (open since Jun 29)](https://github.com/NousResearch/hermes-agent/issues/54945)** — Documented feature blocked by CLI parsing; likely small fix.
- **[#86740 — computer-use doctor misleading on Wayland (open since Aug 15)](https://github.com/NousResearch/hermes-agent/issues/86740)** — Diagnostic misleads users about backend state; needs-repro tag but no response from maintainers in the thread.
- **[#77111 — RealtimeVoiceProvider ABC (open since Aug 2)](https://github.com/NousResearch/hermes-agent/issues/77111)** — Four competing PRs; without an architectural decision, merge pressure will grow.
- **[#94248 — Gateway SIGSEGV (open since Aug 24)](https://github.com/NousResearch/hermes-agent/issues/94248)** — 12 native crash reports; memory-safety issue in delegated workers on macOS; high severity, no PR yet.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-27

## 1. Today's Overview

The PicoClaw project is currently in a state of **moderate activity**, with 7 issues and 5 pull requests updated in the last 24 hours. Notably, the repo has a **healthy submission-to-resolution pipeline**: 3 PRs have been closed/merged (including a significant bug fix for routed-agent context management and a fix for Telegram topic support), while 2 remain open for review. The issue tracker shows a **balanced mix of technical bugs and feature requests**, including a touch of `[stale]` markers suggesting some items are aging. Most importantly, the project did not publish any new releases, indicating that the previous release (v0.31) is still stabilizing, with the latest issues still being reported against it.

## 2. Releases

**No new releases were published within the last 24 hours.** The most recent version remains v0.3.1, which serves as the baseline for the current batch of bug reports and testing.

## 3. Project Progress

Three pull requests were closed or merged over the past day:

- **[PR #3316:** fix: routed-agent context management not respecting history, summarization, compression](https://github.com/sipeed/picoclaw/issues/3316) – This is potentially the most impactful fix of the day. It addresses a critical bug where dispatch rules for routing agents to specific channels (e.g., Discord) caused the agent to have **zero memory** of previous messages and **disable auto-compaction**. This directly fixes Issue #3301 and significantly improves the usability of multi-agent, multi-channel setups.
- **[PR #3315:** Support topics in private bot chats](https://github.com/sipeed/picoclaw/issues/3315) – Enhances Telegram integration by recognizing topics in private bot chats (where `IsTopicMessage` is used instead of `Chat.IsForum`). This expands support for forum-mode private chats.
- **[PR #3314:** Fix customAllowPatterns not working](https://github.com/sipeed/picoclaw/issues/3314) – A security/config fix ensuring that `customAllowPatterns` (user-defined shell command allowlists) actually override default deny patterns. The fix addresses a bug where even explicitly allowed commands like `git push` were blocked due to rule precedence.

## 4. Community Hot Topics

The most engaged discussions involve user-experience and integration issues:

- **[Issue #3287:** "Better support long messages in IRC" (8 comments)](https://github.com/sipeed/picoclaw/issues/3287): While technically a feature request, the tone is more of a plea to handle a current limitation gracefully. Users want PicoClaw to treat multi-line/or super-512-byte IRC messages (split by IRC clients) as a single cohesive message for the LLM, rather than fragmented fragments. **Underlying need:** Better parsing and context assembly for open protocols with hard message length limits.

- **[Issue #3281:** "Web UI chat input is very laggy when history has a little bit long" (7 comments, 1 👍)](https://github.com/sipeed/picoclaw/issues/3281): This is a frontend performance complaint. Users are experiencing UI stutter that scales with chat history length. **Underlying need:** Optimized React frontend state handling or virtualization for long sessions; possibly moving from a "re-render everything" to a "virtualized list" approach.

## 5. Bugs & Stability

Bugs reported/updated in the last 24 hours, ranked by severity:

- **[High] Issue #3339:** Antigravity generation returns generic 429 despite valid OAuth scopes and successful model discovery (open). This is a frustrating integration failure where authentication works, but every generation request is blocked by a rate-limit error that appears to be a server-side or config registration issue, not a genuine quota limit. No fix PR exists yet.

- **[High] Issue #3338:** "Slack does not attach image media content" (open). A hard failure where media uploads always crash with `file.upload.v2: file size cannot be 0`. **Fix exists:** [PR #3340](https://github.com/sipeed/picoclaw/issues/3340) is open, setting `FileSize` on upload parameters. This is a clear "bug + immediate fix" pairing, but the PR has not been merged.

- **[Medium] Issue #3346:** "About RKLLM reply" (open, 0 comments). The reporter is experiencing abnormal responses from the RKLLM model on an ARM development board. The issue includes a screenshot, but lacks details. This appears to be a hardware/edge deployment issue.

- **[Low] Issue #3301:** `[stale]` A bug regarding session auto-compression and `/clear` not working with dispatch rules. **Fix exists:** Closed by PR #3316.

## 6. Feature Requests & Roadmap Signals

- **[Issue #3287:** Better support long messages in IRC](https://github.com/sipeed/picoclaw/issues/3287) – While marked `[stale]`, the proposal to treat split IRC messages as a single logical message is a solid, niche interoperability feature. However, given the clear multi-channel integrations focus of the project, a more generic "payload normalization" layer is likely. **Prediction:** Unlikely in the next minor release; may require a pluggable parsing architecture.

- **Slack media support (Issue #3338 + PR #3340)**: While this is currently a bug fix, the implication is that PicoClaw is expanding beyond text-based channels into rich media. This is a **strong signal** that image/video attachment handling will be a core feature in the next roadmap cycle.

Public roadmap signals are sparse; the active feature set is heavily focused on *stabilizing integrations* (Slack, LINE, Telegram, IRC, Antigravity) rather than new backend capabilities.

## 7. User Feedback Summary

- **Satisfaction:** Users are actively deploying PicoClaw in production-like settings (Raspberry Pi home setups, Discord channels with dispatch rules) and expect stable, long-running behavior.
- **Key Pain Points:**
    - **Memory and context loss** in multi-agent setups (Issue #3301) was a major sticking point for sophisticated users (now fixed).
    - **User-interface lag** (Issue #3281) on the Web UI is a significant UX detractor for heavy users.
    - **Integration friction:** Users experienced hard failures with specific providers (Slack uploads, Antigravity rate limits) despite correct configuration, which creates trust issues.
- **Overall sentiment:** Cautiously optimistic; the community appreciates rapid bug-fix turnaround (e.g., the quick PR for Slack), but the volume of 0.31-specific bugs suggests the release is still being "burned in."

## 8. Backlog Watch

These items have been updated recently but remain unresolved and require maintainer attention:

- **Issue #3281:** Web UI lag (updated Aug 26). Still open with no linked PR. As a UI performance issue, it requires deep frontend work, but it affects user satisfaction daily.

- **Issue #3339:** Antigravity generic 429 error (updated Aug 26). With only 2 comments and no maintainer response yet, this needs triage to confirm whether it's a code bug or a config documentation issue.

- **PR #3340 [Open]:** Fix for Slack media upload. Though it fixes a critical, dated bug (Issue #3338), it has been open since Aug 17 with no merge action. Maintainers should prioritize this, as the Slack channel is completely broken for media content in the current stable version.

- **PR #3329 [Open, stale]:** Fix for LINE webhook settings. While the underlying issue (#3328) is already closed, the PR itself remains unmerged. Marked `[stale]`, it will likely be auto-closed soon unless maintainers act.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-27

## 1. Today's Overview

NanoClaw shows strong, sustained development activity with **24 pull requests updated in the last 24 hours** — 18 open and 6 merged or closed — indicating a highly active contributor base and responsive maintainers. The vast majority of merged/fixes come from a single prolific contributor (Agi-Asi) addressing infrastructure reliability issues across setup scripts, container management, and CLI behavior, alongside smaller external community contributions. However, a **single severe open issue (#3568)** describes a critical bug where pending `system` rows can cause the agent to silently stop responding entirely, which warrants immediate attention. Community contributor PRs (#3550, #3549) fixing security and data-integrity issues remain open, suggesting a possible bottleneck in review throughput. No new releases were published today, and the overall project health appears solid despite the stability concern.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

Six PRs were merged or closed during this period, all centered on **Mattermost channel reliability** from core-team member glifocat:

- **[#3557 (merged) — fix(mattermost): improve initial setup and SiteURL handling](https://github.com/nanocoai/nanoclaw/pull/3557)** — This PR addresses common pain points in the initial Mattermost integration setup, particularly around SiteURL configuration which often causes connectivity failures.
- **[#3556 (merged) — fix(mattermost): recover card thread after restart](https://github.com/nanocoai/nanoclaw/pull/3556)** — Fixes a crash where interactive-card routing relied on an in-memory cache that was lost after a host restart, causing approval cards to become unresponsive. This is a significant stability improvement for production deployments using Mattermost approval workflows.

Additionally, 18 PRs remain open and await review, spanning fixes for infrastructure setup tooling, CLI behavior, and test hardening. Notably, 15 of these open PRs (from Agi-Asi) address a wide swath of operational reliability concerns, though the sheer volume suggests a possible review backlog.

## 4. Community Hot Topics

The most active item this cycle is a **critical bug report from a community user**:

- **[Issue #3568 — Pending system rows starve the inbound queue; agent silently stops responding](https://github.com/nanocoai/nanoclaw/issues/3568)** — With zero comments and one day old, this is the highest-severity item in the tracker. The report describes a scenario where an accumulation of pending `kind='system'` rows (default `maxMessagesPerPrompt` = 10) with lower sequence numbers than real traffic causes the agent to **completely ignore all inbound messages without any error**. This is a silent failure — the worst kind — and represents a critical reliability gap for production users.

- **[Issue #574 (closed, 3 comments) — containers lack jq](https://github.com/nanocoai/nanoclaw/issues/574)** — The project's containers lack `jq`, forcing users to fall back on `node -e` for parsing API responses, which introduces a potential **command injection attack surface**. The community has flagged this as a security-relevant enhancement, though it remains lower priority.

## 5. Bugs & Stability

Ranked by severity:

| Severity | Issue | Description |
|----------|-------|-------------|
| **Critical** | [#3568](https://github.com/nanocoai/nanoclaw/issues/3568) | **Agent silently stops responding** when pending system rows exceed the message threshold and starve the inbound queue. No error is raised, making the failure extremely difficult to detect. **No fix PR exists yet.** |
| **High** | [#3549 (PR)](https://github.com/nanocoai/nanoclaw/pull/3549) | **Infinite crash loop on message delivery retry** — a plain `INSERT INTO messages_in` throws `UNIQUE constraint failed` when a retried message id already exists; the caller treats this as a delivery failure and retries endlessly. The fix (using `INSERT OR IGNORE`) is in PR, but **not yet merged**. |
| **High** | [#3550 (PR)](https://github.com/nanocoai/nanoclaw/pull/3550) | **Command injection vulnerability via email substitution** — the email validation regex allows shell metacharacters (`;`, backticks, `$()`), and substitution is unquoted in `bash -c`. Also breaks onboarding for apostrophe-containing emails. Fix in PR, **not yet merged**. |
| **Medium** | [#3556 (closed)](https://github.com/nanocoai/nanoclaw/pull/3556) | Mattermost cards lost thread context after restart — **fixed and merged**. |
| **Medium** | [#3555 (PR)](https://github.com/nanocoai/nanoclaw/pull/3555) | **Node < 22.14 causes segfaults** with better-sqlite3 13 — setup now enforces a minimum Node version. PR open. |
| **Medium** | [#3563 (PR)](https://github.com/nanocoai/nanoclaw/pull/3563) | **signal-cli probes can deadlock** on the daemon's config lock — fix adds timeouts. PR open. |
| **Low/Medium** | [#3562 (PR)](https://github.com/nanocoai/nanoclaw/pull/3562) | **Non-interactive apt can hang** on `needrestart` prompt in Linux installers — fix pending. |

The cluster of setup/installer fixes (#3561–#3567) from Agi-Asi indicates that **fresh installation reliability is a known weak spot** being actively patched.

## 6. Feature Requests & Roadmap Signals

- **[#574 — Include `jq` in containers](https://github.com/nanocoai/nanoclaw/issues/574)** — This enhancement addresses both security (avoiding `node -e` eval attacks) and usability for API-response parsing. Given its security implications and low implementation cost, this is a strong candidate for the next release.

- **Dial channel documentation ([#3501 PR](https://github.com/nanocoai/nanoclaw/pull/3501))** — Makes the Dial integration discoverable in README and changelog. This signals that **Dial as a communication channel is now a shipped feature** and likely to be promoted in the next release notes.

- **Per-group MCP policy enforcement ([#3551, #3552 PRs)](https://github.com/nanocoai/nanoclaw/pull/3551)** — Enforcing MCP-only policy and gateway routing per group suggests a **move toward stricter, more granular governance controls**, likely aimed at enterprise deployment scenarios.

- **Group-scope auto-fill args documentation ([#3559 PR)](https://github.com/nanocoai/nanoclaw/pull/3559)** — Clarifying that auto-fill args are "locked" rather than "defaulted" hints at a subtle semantic shift in CLI configuration behavior that should be documented in the release notes.

## 7. User Feedback Summary

**Pain Points:**
- **Silent agent failures** (#3568) are the most alarming user-reported issue — the agent stops responding with no error, making it impossible to diagnose without deep log inspection.
- **Security vulnerabilities via insecure parsing** (#574) reflect a user base concerned about production safety when interacting with external APIs.
- **Setup/onboarding friction** continues to be a recurring theme — signal-cli deadlocks, launchd no-ops, `needrestart` hangs, and Node version requirements all add friction to new installations.

**Positive Signals:**
- The **sheer volume of the recent PR activity (24 in a day)** shows an active, engaged contributor ecosystem that is proactively identifying and fixing issues.
- Mattermost improvements (#3556, #3557) directly address reported usability/stability problems from the community.
- The **core-team (glifocat) and community (Agi-Asi, aniruddhaadak80, wildcard)** mix indicates a healthy balance of maintainer-driven work and external contribution.

**Overall Satisfaction:** Appears moderate-to-high — users are engaged enough to file detailed bug reports and submit fixes, though critical reliability bugs remain unresolved.

## 8. Backlog Watch

Items needing maintainer attention:

- **[#3568 — Critical silent agent failure](https://github.com/nanocoai/nanoclaw/issues/3568)** — Opened 2026-08-26, zero comments. This is the single most severe item in the tracker and needs immediate triage and a fix plan.
- **[#3550 — Command injection fix pending](https://github.com/nanocoai/nanoclaw/pull/3550)** — Security-relevant PR opened 2026-08-26 with no maintainer review. Should be prioritized given the injection vector.
- **[#3549 — Infinite crash-loop fix pending](https://github.com/nanocoai/nanoclaw/pull/3549)** — Data-integrity + crash-loop fix, open since 2026-08-26. Relates to message delivery reliability.
- **[#3551/#3552 — MCP policy enforcement PRs](https://github.com/nanocoai/nanoclaw/pull/3551)** — Open with no review; these configure remote MCP policy controls, likely part of an ongoing governance feature push.

The **Agi-Asi cluster of 15 open PRs** (e.g., #3553–#3567) is a bottleneck concern — if they remain unreviewed for weeks they will likely conflict as code changes. A dedicated review pass is recommended.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-08-27

## 1. Today's Overview
NullClaw's activity is at a low ebb today. The project saw **1 new/updated issue** and **0 Pull Requests** in the last 24 hours, with no releases or merges. The single open issue is a feature request regarding symlink support for skills, indicating that while the project is not actively shipping changes, it is still receiving user input. Overall project health appears stable but quiet; no regressions or bug reports were filed. The low operational tempo suggests the core team may be in a development or release-candidate phase.

## 2. Releases
**No new releases** were published within the reporting window. The most recent public version referenced in the issue is **`nullclaw 2025.5.29`**, which users are currently running. No migration notes or breaking changes to report.

## 3. Project Progress
**No Pull Requests were merged or closed** in the last 24 hours. Consequently, no features were advanced or fixes landed. The repository is static in terms of contribution throughput for this period.

## 4. Community Hot Topics
- **[#995 [OPEN] [enhancement] Support Skills Symlinks](https://github.com/nullclaw/nullclaw/issues/995)** — *Author: ivostoykov | Created: 2026-08-26 | Comments: 0 | 👍: 0*  
  Although the issue has no comments or reactions yet, it is the only recent activity and touches on a significant workflow concern for power users: the ability to symlink skill files/directories. The underlying need is to allow skills to be stored in one location (e.g., a dotfiles repo or a separate version-controlled folder) and referenced from the NullClaw skills directory without duplication. Empty engagement suggests the request is fresh and has not yet garnered community visibility.

## 5. Bugs & Stability
**No bugs, crashes, or regressions** were reported in the last 24 hours. The issue tracker shows zero stability-related reports for this window. The current build appears stable, with no known critical issues to escalate.

## 6. Feature Requests & Roadmap Signals
The sole feature request is **[#995: Support Skills Symlinks](https://github.com/nullclaw/nullclaw/issues/995)**. The request is straightforward and aligns with common open-source ecosystem practices (e.g., package managers and dotfile tools supporting symlinks). Given its simplicity and the clear user pain point (synchronization overhead and skill obsolescence management), this issue has a reasonable chance of being picked up in the next minor release (e.g., `2025.6.x`) if maintainers prioritize usability improvements. Prediction: **Low-to-moderate probability** of implementation in the next version, depending on maintainer bandwidth and whether it gains community traction.

## 7. User Feedback Summary
The single user report provides a clear signal on user expectations: users want **standard filesystem flexibility** (symlink support) within NullClaw. The motivation stated—*"Reduces synchronisation and feasibility of using obsolate skill"*—highlights two distinct pain points:  
- **Synchronization overhead**: duplicates consume storage and require manual sync.  
- **Skill lifecycle management**: users want to point to deprecated/obsolete skills without copying them into the main tree.  

This feedback indicates users are treating skills as modular, externally-managed components rather than immutable internals. No direct satisfaction/dissatisfaction metrics (stars, upvotes) are available.

## 8. Backlog Watch
No long-unanswered or stale issues requiring immediate maintainer attention were identified. The only open issue is from the last 24 hours, well within normal response expectations. The repository's backlog appears clean; however, with only one item in the window, it is worth monitoring whether **#995** receives a maintainer response within the next 48 hours—an absence of acknowledgment could indicate a maintainer availability bottleneck.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-27

## 1. Today's Overview

IronClaw is in an intensive pre-release stabilization phase for v1.4.0, with the first release candidate (`1.4.0-rc.1`) cut yesterday covering 81 commits since v1.3.0. Activity is exceptionally high: 27 issues updated and 50 PRs updated in the last 24 hours, with 48 PRs merged/closed versus only 2 still open — a healthy merge-to-open ratio suggesting strong execution velocity. The bulk of merged PRs are from a multi-week backlog of large, carefully-scoped changes (XL-sized PRs for filesystem security, TLS seams, agent-loop refactoring) that have now landed on `main`. Performance and context-window efficiency are emerging as the dominant themes, with two major performance bugs filed today (OpenAI-family prompt-cache collapse, unprojected MIME payloads) alongside a new PR introducing bounded JSON result views. The project shows strong engineering discipline: detailed performance measurements, root-cause analysis, and structured epics tracking roadmap phases.

## 2. Releases

**ironclaw-v1.4.0-rc.1** (2026-08-26) — [Release](https://github.com/nearai/ironclaw/releases/tag/ironclaw-v1.4.0-rc.1)

The first release candidate for v1.4.0, covering 81 commits since `ironclaw-v1.3.0`. Key addition:

- **Durable notification inbox**: runs now publish authoritative outcomes and actionable gates to a per-user inbox, surfaced through the WebUI notification center. This consolidates approvals and auth prompts into a single durable surface.

The cut commit ([PR #7926](https://github.com/nearai/ironclaw/pull/7926)) is a three-file change bumping `ironclaw_cli` from `1.2.0` to `1.4.0-rc.1`. This is a release candidate, so expect API/behavioral changes before final; teams should test notification-center flows and the new sandbox/container-supervised mode.

## 3. Project Progress

48 PRs merged/closed in the last 24 hours, representing substantial multi-week efforts landing on `main`:

**Security & Reliability (notable XL-sized PRs):**
- [PR #6817](https://github.com/nearai/ironclaw/pull/6817) — **Critical filesystem fix**: closes four TOCTOU containment escapes in the local backend via fd-rooted traversal. Pathname-check-then-syscall races are now eliminated.
- [PR #6740](https://github.com/nearai/ironclaw/pull/6740) — TLS termination seam for the sandbox egress proxy (phase 1), enabling HTTPS interception for sandboxed processes.
- [PR #6533](https://github.com/nearai/ironclaw/pull/6533) — Container-supervised mode for hosted deployments, fixing improper restart/apply paths and opaque `os error 2` failures.

**Agent Loop & Architecture:**
- [PR #6112](https://github.com/nearai/ironclaw/pull/6112) — Decomposed the canonical executor `execute()` in the agent loop, removing accumulated inline decision logic and deduplicating latency wrapping.
- [PR #6157](https://github.com/nearai/ironclaw/pull/6157) — Terminal UI (`ironclaw-reborn tui`, ratatui-based) + service install capability, both behind `webui-v2-beta`.

**MCP Framework:**
- Three MCP PRs landed: registration framework skeleton ([#5970](https://github.com/nearai/ironclaw/pull/5970)), user-facing hosted MCP registration/discovery ([#5918](https://github.com/nearai/ironclaw/pull/5918)), and egress boundary locking registered servers to host egress ([#5917](https://github.com/nearai/ironclaw/pull/5917)).

**Production Fixes:**
- [PR #5742](https://github.com/nearai/ironclaw/pull/5742) — Wired the memory prompt-context source (was fully implemented but never composed); pins the untrusted-memory injection-hardening envelope.
- [PR #5736](https://github.com/nearai/ironclaw/pull/5736) — Fixed dead local-dev synthetic retry path; retry-category coverage restored.
- [PR #5579](https://github.com/nearai/ironclaw/pull/5579) — Four OAuth wire-format bugs: `expires_in` string coercion, DCR error bodies, RFC 8414 optional registration endpoint, and callback query parsing.
- [PR #6096](https://github.com/nearai/ironclaw/pull/6096) — Serializes concurrent inbound-message writes per thread to fix out-of-order message persistence.

**New this morning:** [PR #7928](https://github.com/nearai/ironclaw/pull/7928) — Bounded, shallow JSON selection for durable tool-result reads (RFC 6901 pointers, collection limits, UTF-8 paging, continuation requests), directly addressing the "too many tools / giant results" failure mode.

## 4. Community Hot Topics

**Most active issues (by comments):**

1. **[#7732 — Epic: Persistent per-user sandbox with iron-proxy](https://github.com/nearai/ironclaw/issues/7732)** (10 comments) — The flagship architecture epic. Current Docker-per-command is too ephemeral; `/workspace` should persist per (tenant, user). This is the roadmap's centerpiece for v1.4.0's sandbox story.

2. **[#7891 — perf: unprojected capability payloads + blind 24 KiB head-slice cost 14.3s inference](https://github.com/nearai/ironclaw/issues/7891)** (5 comments) — Two Gmail API calls (274ms and 290ms) caused a **19.7-second turn** because 49,152 bytes of raw MIME headers were pushed into the prompt unasked, then re-read by the model. This is a scathing performance indictment and the most actionable issue this week.

3. **[#2117 — ironclaw-bridge: local file/MCP bridge daemon](https://github.com/nearai/ironclaw/issues/2117)** (3 comments, 1 👍) — Cloud-hosted deployments can't access local laptop files (Obsidian vaults, project dirs). Long-running request since April; the extension system may finally make this tractable.

4. **[#6369 — Epic: Tier B follow-up: gaps left by v1 (src/) retirement](https://github.com/nearai/ironclaw/issues/6369)** (3 comments) — Tracking capability gaps after the legacy monolith deletion.

**Underlying needs:** The community is pushing hard on (a) persistent, long-lived sandboxes vs. per-command containers, (b) making the model pay attention only to what it needs (prompt hygiene), and (c) bridging cloud-hosted IronClaw to local user resources. Performance-per-token is clearly becoming the #1 competitive differentiator.

## 5. Bugs & Stability

Ranked by severity:

**High — Prompt-cache collapse on OpenAI-family backends** ([#7921](https://github.com/nearai/ironclaw/issues/7921)) — No `prompt_cache_key` sent by OpenAI-family backends, causing measured cache-hit collapse from ~82% to ~29% past ~200 calls. Direct cost/latency impact on all non-Anthropic providers. No fix PR yet.

**High — Giant trajectories fail to download (HTTP 413)** ([#7918](https://github.com/nearai/ironclaw/issues/7918)) — "Content too large" blocks downloading examples with egregious tool-call counts. Blocks debugging the tool-loop exhaustion issue. No fix PR.

**Medium — Unprojected capability payloads bloat prompts** ([#7891](https://github.com/nearai/ironclaw/issues/7891)) — 49 KiB of raw MIME headers injected into a prompt unasked → 19.2s of wasted inference. This is a design flaw (no projection at capability boundary) rather than a crash. Related fix in-progress: [PR #7928](https://github.com/nearai/ironclaw/pull/7928) adds bounded JSON selection.

**Medium — Telegram removal returns 503 from WebChat extension endpoint** ([#7912](https://github.com/nearai/ironclaw/issues/7912)) — Reproducible in production; `POST /api/webchat/v2/extensions/telegram/...` fails when removing the channel.

**Low — [Closed] V2 read result + tool output parser before durable storage** ([#7917](https://github.com/nearai/ironclaw/issues/7917)) — Proposal closed; design being kicked off for agent implementation.

**Fixed this cycle:** Concurrent message writes out-of-order ([#6096](https://github.com/nearai/ironclaw/pull/6096) merged), memory prompt-context dead code ([#5742](https://github.com/nearai/ironclaw/pull/5742) merged), local-dev retry path dead code ([#5736](https://github.com/nearai/ironclaw/pull/5736) merged), four OAuth wire-format bugs ([#5579](https://github.com/nearai/ironclaw/pull/5579) merged).

## 6. Feature Requests & Roadmap Signals

**Strong signals for v1.4.0 final:**
- **Persistent per-user sandbox** ([#7732](https://github.com/nearai/ironclaw/issues/7732)) — The epic explicitly defers loop executors; expects `iron-proxy` for persistence. This is the headline architectural change.
- **Bounded selectable JSON result views** ([#7928](https://github.com/nearai/ironclaw/pull/7928), open) — Directly addresses the "too many tools" failure mode ([#7447](https://github.com/nearai/ironclaw/issues/7447)). Likely to merge before final.
- **Learned-skill extraction configuration in Inference settings** ([#7920](https://github.com/nearai/ironclaw/issues/7920)) — Currently gated by undocumented env var; making it a product surface.

**Signals for v1.5.0 (per issue labels):**
- **Personality (agent.md) editor in Settings UI** ([#7895](https://github.com/nearai/ironclaw/issues/7895)) — Users find setup difficult.
- **Telegram and Slack bot groups, personal vs. bot distinction** ([#7909](https://github.com/nearai/ironclaw/issues/7909)) and **Slack-to-console bridge** ([#7871](https://github.com/nearai/ironclaw/issues/7871)) — Rich interactive Slack UX with durable continuity into the console.
- **Context Management Optimisations epic** ([#7911](https://github.com/nearai/ironclaw/issues/7911)) — Broad, currently TBD scope.

**Watch:** the **Decision spike: persistent per-user sandboxed executor behind the trusted host kernel** ([#7903](https://github.com/nearai/ironclaw/issues/7903)) — risk: high. The current "host loop + sandboxed shell" split preserves authority but every new CLI requires plumbing. This might reshape the architecture for v1.5.

## 7. User Feedback Summary

- **Pain: Prompt bloat wastes money and time.** The Gmail/MIME issue ([#7891](https://github.com/nearai/ironclaw/issues/7891)) and the prompt-cache collapse ([#7921](https://github.com/nearai/ironclaw/issues/7921)) both reflect user complaints that turns take far longer than tool latency justifies. The team is clearly measuring this precisely and shipping fixes (bounded JSON views, cache keys).

- **Pain: Setup complexity.** A user literally reports "me trying to set up personality with ironclaw" as a frustrating experience ([#7895](https://github.com/nearai/ironclaw/issues/7895)). Learned-skill extraction is invisible without a documented env var ([#7920](https://github.com/nearai/ironclaw/issues/7920)). Expect more settings-surface work.

- **Pain: Cloud-hosted users can't reach local files.** The ironclaw-bridge request ([#2117](https://github.com/nearai/ironclaw/issues/2117)) has been open since April with only 1 👍, but it's a fundamental product gap for Obsidian-vault-style use cases.

- **Satisfaction signal:** Onboarding suggestions now run end-to-end on `main` ([#7815](https://github.com/nearai/ironclaw/issues/7815), closed) after three linked PRs — the connect → suggest → thread flow is working.

## 8. Backlog Watch

- **[#2117 — ironclaw-bridge](https://github.com/nearai/ironclaw/issues/2117)** (open since 2026-04-07, 3 comments) — Local file/MCP bridge for cloud deployments. High-value, zero maintainer response in months. The extension lifecycle work may now enable this; needs an owner.

- **[#6369 — Tier B gaps post-v1 retirement](https://github.com/nearai/ironclaw/issues/6369)** (open since 2026-07-20, 3 comments) — Epic tracking gaps left by deleting the legacy monolith. Hasn't moved; risks becoming permanently parked.

- **[#7447 — Agent fails after too many tools](https://github.com/nearai/ironclaw/issues/7447)** (open since 2026-08-10, 0 comments) — The fetch-retry-loop example (4 near-duplicate GitHub queries instead of paginating) is a textbook agent-loop failure. The new bounded JSON views help, but the loop-exhaustion behavior itself needs a targeted fix.

- **[#4625 — Slack channel-routed personal and team agents](https://github.com/nearai/ironclaw/issues/4625)** (open since 2026-06-09, 1 comment) — Phase 1 Slack-as-a-channel vs. later "agent acts as me" model. Labeled `suggested_P1` and `roadmap` but no recent activity; superseded in urgency by the richer Slack epic [#7871](https://github.com/nearai/ironclaw/issues/7871).

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-27

## 1. Today's Overview

LobsterAI is in a high-velocity release cycle, with 15 of 16 PRs closed today and an active release/2026.8.26 branch being prepared. The project shows a healthy, disciplined engineering cadence focused on polish: UI refinements (sidebar library icon redesign across 3 PRs), analytics instrumentation completion, and cloud sharing/file management features. Only 2 issues were touched in the last 24 hours, both open feature requests, indicating the community's attention is on enhancement rather than bug reporting. No new releases were published today, but the volume of merged PRs strongly suggests an imminent tag.

## 2. Releases

No new releases were published in the last 24 hours. The merged `Release/2026.8.26` branch (PR #2549) indicates the project team is preparing a build for release.

## 3. Project Progress

**15 PRs merged/closed today**, covering several significant areas:

**Cloud Library & Sharing — PR #2550** (`feat(library): 支持永久删除云端分享文件`, by liugang519): Adds permanent deletion of shared cloud files, with confirmation dialog, state conflict handling, server compatibility checks, and data calibration on failure. Also fixes duplicate deployment request triggers after account switching and popup close.

**Analytics Chain — PR #2555** (`feat(analytics): 完善发布与部署分析链路`, by liugang519): Instruments sharing, deployment, copy-link, and permission-update events, associating operations with outcomes, latency, and error categories. Adds async deployment end-state tracking and reliable reporting queue. Extends telemetry for library refresh, favorites, and publish popups.

**UI Polish — Multiple PRs (fisherdaddy, liuzhq1986):**
- Sidebar library icon redesign (3 PRs: #2540, #2542, #2544)
- Settings panel width update (#2548)
- Dark-mode fix for Zhipu icon (#2553)
- Login guide fixes (#2545, #2547) and reworked promo timing logic — sidebar login promo auto-hide is now paused until engine startup overlay clears (#2546)

**Account — PR #2539**: Added daily credit gift entry to user menu.

**Windows Installer — PR #2543**: Web installer timing diagnostics added.

**Stability Fix — PR #2551 (still open)**: App update state preservation for ready state — the only open PR at time of writing.

## 4. Community Hot Topics

Only 2 issues were updated in the last 24 hours, both with 1 comment each — neither has generated substantial discussion. The topics raised are:

1. **Issue #2554 — Synthorai as built-in provider** (cuihuan, created 2026-08-26): Requests adding Synthorai (an aggregator gateway supporting both OpenAI and Anthropic protocols) as a built-in service provider. User notes that the current Custom slot works but lacks default model lists, `switchableBaseUrls` for protocol switching, and proper base URL validation/guidance. This is the most actionable feature request among recent issues.

2. **Issue #2541 — Persian (Farsi) RTL text support** (hamidebrahimie-design, created 2026-08-26): Reports incorrect RTL rendering in chat — input box caret positioning and mixed-bidi handling issues, plus ZWNJ half-space rendering. UI/UX quality issue affecting a specific locale.

## 5. Bugs & Stability

No new bugs, crashes, or regressions were reported in the last 24 hours. The project is in a stable phase.

**Notable stability work merged today:**
- Deployment request duplication fix (PR #2550)
- Login guide timing and overlay logic fix (PR #2546)
- Sidebar library icon styling fixes for consistency

**Open stability concern:** PR #2551 (fix: app update preserve ready state) — ensures app update state is preserved through restarts; remains unmerged and warrants attention.

## 6. Feature Requests & Roadmap Signals

**Persian (Farsi) RTL support (Issue #2541)** — A legitimate usability gap affecting Persian-speaking users. Given the project actively addresses UX issues with quick turnaround (as seen in the login guide fixes), this has reasonable odds of being addressed soon, though RTL/bidi rendering is non-trivial and may require more planning.

**Synthorai as built-in provider (Issue #2554)** — Low-hanging fruit for onboarding users who want aggregator gateways. With OpenRouter already a first-class citizen, adding Synthorai follows a clear product pattern. This could land quickly given the team's focus on provider ecosystem polish (Zhipu dark-mode icon fix went in today).

**Analytics and monetization signals:** Merged PRs around daily credit gifts (#2539) and analytics instrumentation (#2555) suggest continued investment in user engagement and usage tracking — a roadmap signal for growth features.

## 7. User Feedback Summary

- **Pain point (provider onboarding):** Users want simplified setup for aggregator gateways like Synthorai — the Custom slot is functional but friction-heavy (manual model lists, no protocol switching, error-prone base URLs).
- **Pain point (i18n):** Persian text rendering is broken in core chat surfaces, affecting a specific but committed user base.
- **Positive signal:** Users are actively requesting feature parity, indicating engaged usage; the absence of bug reports suggests the 2026.8.26 release cycle has not surfaced regressions from the community yet.

## 8. Backlog Watch

- **PR #2551 (fix: app update preserve ready state)** — Open PR that ensures update readiness state isn't lost; important for reliability of the update flow. Needs review and merge.
- **Issue #2541 (Persian RTL)** and **Issue #2554 (Synthorai provider)** — Both fresh (created yesterday) and under consideration; neither has maintainer response yet. For a project this active, prompt note of triage would help manage community expectations.
- No long-dormant critical issues observed in the current window.

---

**Overall assessment:** LobsterAI is in excellent health — high merge velocity, focused scope discipline, a mix of feature, polish, and reliability work, and a calmanubug surface. The release pipeline for 2026.8.26 appears imminent.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-27

## Today's Overview
Moltis saw light but meaningful activity on 2026-08-27, with one issue closed and two pull requests merged within the last 24 hours. The project shipped release **20260826.01** on the previous day, continuing a steady cadence of incremental releases. Despite the low volume, the closed work addresses a long-standing user-reported bug from June and a freshly submitted Fastmail integration fix, indicating the maintainers are clearing backlog items. No new issues or PRs were opened today, suggesting a period of consolidation rather than expansion.

## Releases
**Release 20260826.01** (released 2026-08-26)

No release notes or changelog were provided in the available data, so detailed changes, breaking changes, or migration notes cannot be confirmed from this digest. The release follows the project's pattern of dated versioning (YYYYMMDD.NN) and appears to be a routine patch/minor release. Users should consult the [GitHub releases page](https://github.com/moltis-org/moltis/releases) for official details.

## Project Progress
Two pull requests were merged/closed today (both by contributor **penso**):

1. **[PR #1104 — fix(providers): allow replacing preferred models](https://github.com/moltis-org/moltis/pull/1104)** (merged): This closes long-standing issue [#1094](https://github.com/moltis-org/moltis/issues/1094) (reported June 3). The fix ensures that saved provider model preferences are preselected when opening the preferred-model dialog, and that saving replaces previous preferences (including clearing all preferences with an empty selection). It also added backend and Playwright regression coverage — a healthy sign for test-driven fixes.

2. **[PR #1244 — Fix Fastmail MCP OAuth scope registration](https://github.com/moltis-org/moltis/pull/1244)** (merged): Fixes the Model Context Protocol (MCP) OAuth discovery flow for Fastmail and similar providers. The fix prefers protected-resource scopes over the authorization server's broader catalog, includes selected scopes in RFC 7591 dynamic client registration, and adds a Fastmail-shaped regression test covering resource discovery, registration, and localhost redirect flows.

## Community Hot Topics
There were no issues or PRs with significant comment threads or reactions in the last 24 hours — both merged PRs had zero reactions and no comment data. The most notable community-driven item is the now-**closed** [Issue #1094](https://github.com/moltis-org/moltis/issues/1094) (De-Preferring Models, reported by **RokkuCode**), which sat open for nearly three months before being resolved today by PR #1104. The underlying need here was a UX/functional gap: users could set preferred models but could not remove or replace them, and the dialog did not reflect current selections. This suggests community interest in finer-grained model preference management.

## Bugs & Stability
One bug was resolved today:

- **[Issue #1094 — [Bug]: De-Preferring Models](https://github.com/moltis-org/moltis/issues/1094)** (severity: **medium-low**, closed): Users were unable to remove or replace preferred models in the provider settings dialog. This is a functional UX bug, not a crash or data-loss issue. The fix landed in **PR #1104** with regression tests, so the issue is fully resolved.

No new bugs were filed in the last 24 hours, and no crashes, regressions, or stability concerns were reported.

## Feature Requests & Roadmap Signals
No explicit feature requests were opened today. However, two signals from the merged work point toward ongoing roadmap themes:

1. **Model preference management** (PR #1104): The fix enables replacing/clearing preferred models — the community likely wants more granular control over model selection per provider. Future related work might include per-conversation model overrides or bulk preference management.

2. **MCP OAuth robustness** (PR #1244): The Fastmail-specific scope handling indicates the project is actively hardening its MCP integration against real-world provider quirks (resource-protected scopes, dynamic client registration). Expect continued MCP OAuth improvements, possibly generalizing to other providers with non-standard scope behavior.

## User Feedback Summary
The primary user pain point surfaced in this digest is the **inability to de-prefer models** — a workflow barrier for users who experiment with different models and want to retract a previous choice. The issue was reported as a bug (preflight checklist included, latest version confirmed), indicating the reporter was methodical and the problem was reproducible in the latest build. The fix's inclusion of regression tests suggests
afford that quality. There were no expressions of dissatisfaction or praise in comments; the low engagement overall (zero comments, zero reactions) suggests this is a niche functional issue rather than a widespread frustration.

## Backlog Watch
No long-unanswered issues or stale PRs were identified in the 24-hour window. The oldest item closed today (Issue #1094, filed 2026-06-03) was resolved in ~12 weeks, which is a reasonable turnaround. No open issues or PRs remain in the active set from today's data. Maintainers appear to be keeping the backlog under control, though tracking of older open issues beyond this window would be needed to confirm overall health.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-27

## 1. Today's Overview

CoPaw (QwenPaw) is in an active development phase, with the **v2.2.0-beta.1** release freshly cut and the codebase already moving toward **v2.2.0b2**. The project shows a healthy mix of feature advancement and stability work: 45 PRs were updated in the last 24 hours (28 merged/closed), signaling a high-velocity merge pipeline. On the issue tracker, 33 issues were updated (15 closed), suggesting issues are being triaged and resolved efficiently. However, the bug-to-feature ratio in new reports leans toward the **stability side**, particularly around the Windows installer, TLS stack, and desktop tooling regressions, indicating the v2.1.x series is undergoing hardening ahead of the 2.2.0 multi-tenant Hub launch. Overall, the project appears to be in a **release-candidate hardening phase** with a strong push on test coverage and infrastructure reliability.

---

## 2. Releases

**v2.2.0-beta.1** was released (dated within the last 24 hours).

Key changes from the release notes:
- **Docs**: Updated scroll context manager blog ([#7300](https://github.com/agentscope-ai/QwenPaw/pull/7300))
- **Providers**: Sanitized DashScope tool schemas for strict models ([#7284](https://github.com/agentscope-ai/QwenPaw/pull/7284))
- **Integration tests**: Targeted coverage improvements (truncated in notes)

**Migration/breaking notes:** No explicit breaking changes or migration instructions were announced in the release notes, but users on v2.1.1b2 or earlier Windows may want to note the upcoming NSIS installer fixes and the planned Python 3.13 / OpenSSL 3.5 TLS stack bump (see PRs below).

---

## 3. Project Progress

Multiple meaningful PRs were merged/closed in the last 24 hours, advancing both feature work and infrastructure:

**Infrastructure & CI:**
- **[#7293](https://github.com/agentscope-ai/QwenPaw/pull/7293)** — Split integration tests into three parallel shards (p0/p1/p2), significantly reducing CI turnaround time.
- **[#7326](https://github.com/agentscope-ai/QwenPaw/pull/7326)** — Split nightly E2E into three parallel shards with a **fail-closed** summary gate, fixing silent test passes.
- **[#7250](https://github.com/agentscope-ai/QwenPaw/pull/7250)** — Fixed the local test runner (`scripts/run_tests.py`) which was **silently skipping suites and reporting false successes** — a critical developer-experience fix.
- **[#7292](https://github.com/agentscope-ai/QwenPaw/pull/7292)** — Added 19 new unit test files (1,148 tests), lifting backend coverage from 58.04% to 63.06%. Also fixed a semantic bug in `safety_checks.py` regarding `/root` directory classification.
- **[#7325](https://github.com/agentscope-ai/QwenPaw/pull/7325)** — Expanded Console unit tests (+382 cases, +5.49pp statement coverage).
- **[#7327](https://github.com/agentscope-ai/QwenPaw/pull/7327)** — Added 23 new E2E test cases targeting highest-value uncovered product files.

**Runtime & Workspace:**
- **[#7194](https://github.com/agentscope-ai/QwenPaw/pull/7194)** — Made workspace startup/reload cleanup cancellation-safe, fixing a class of partial-state leaks.
- **[#7319](https://github.com/agentscope-ai/QwenPaw/pull/7319)** — Refactored Console to route background agent runs through the workspace TaskTracker, enabling proper status, stop, and reload ownership for background runs.

**Data/Integration:**
- **[#7190](https://github.com/agentscope-ai/QwenPaw/pull/7190)** — Made `qwenpaw-data` installable from PyPI, added docker-compose demo stack (Neo4j + PostgreSQL), and fixed env inheritance.

---

## 4. Community Hot Topics

The most active discussions reveal strong interest in the **multi-tenant Hub direction** and the **Windows install experience**:

1. **[#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921) — [OPEN] Agent stops mid-task without notice (11 comments)**  
   Users report the assistant frequently halts after stating a plan but never executes it, requiring a manual "继续" prompt. This is the **top pain point** on the tracker, indicating a reliability gap in agent task-continuation logic. The issue has been open since 2026-08-12 with no fix PR yet — needs maintainer attention.
   
2. **[#7318](https://github.com/agentscope-ai/QwenPaw/issues/7318) — [OPEN] QwenPaw Hub multi-tenant edition discussion (5 comments)**  
   An official discussion thread seeded by the team, gathering community input on the upcoming 2.2.0 Hub. References earlier multi-user requests ([#2324](https://github.com/agentscope-ai/QwenPaw/issues/2324)). This is a **strong product signal** that the team is actively building the multi-tenant path.
   
3. **[#6810](https://github.com/agentscope-ai/QwenPaw/issues/6810) — [CLOSED] Windows NSIS install/update blocker (5 comments)**  
   The NSIS uninstaller locking files was fixed (closed), but follow-up PRs exist to address edge cases not covered by the first fix.
   
4. **[#7258](https://github.com/agentscope-ai/QwenPaw/issues/7258) — [CLOSED] WeChat channel "show thinking process" toggle ineffective (6 comments)**  
   Closed, indicating a fix was landed or addressed.

**Underlying needs:** Users are pushing for (a) more reliable task completion without babysitting, (b) team/multi-user support, and (c) fewer Windows deployment friction points.

---

## 5. Bugs & Stability

Ranked by severity, with fix-PR status where applicable:

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **Critical** | [#7311](https://github.com/agentscope-ai/QwenPaw/issues/7311) | `v2.1.1b2` missing `_qwenpaw_remote_backend` module — **all tools broken** on Windows | No fix PR yet |
| **High** | [#7298](https://github.com/agentscope-ai/QwenPaw/issues/7298) | Desktop/Docker ship OpenSSL 3.0.x (Python 3.11) — carrier DPI resets TLS handshakes | **Fix PR:** [#7328](https://github.com/agentscope-ai/QwenPaw/pull/7328) bumps to Python 3.13 / OpenSSL 3.5.x |
| **High** | [#7296](https://github.com/agentscope-ai/QwenPaw/issues/7296) | OpenAI Responses multi-turn fails with 400 "Referenced reasoning item ... expired" on stateless upstreams | No fix PR yet |
| **Medium** | [#7324](https://github.com/agentscope-ai/QwenPaw/issues/7324) | Scheduled tasks miss inbox push notifications on success | No fix PR yet |
| **Medium** | [#7310](https://github.com/agentscope-ai/QwenPaw/issues/7310) | Software crash suspected from plugin conflict (datapaw plugin missing runtime) | Workaround: disable plugin |
| **Medium** | [#7212](https://github.com/agentscope-ai/QwenPaw/issues/7212) | Inlining oversized-pixel images crashes request instead of graceful degradation | Closed — likely fixed |
| **Medium** | [#7206](https://github.com/agentscope-ai/QwenPaw/issues/7206) | `/compact` fails with pydantic ValidationError when `compact_threshold_ratio == 0.9` (regression in 2.1.1b1) | Closed — fixed |
| **Low/UI** | [#7321](https://github.com/agentscope-ai/QwenPaw/issues/7321) | Tool call display stuck in "executing" state after forced stop | No fix PR yet |
| **Low/UI** | [#7306](https://github.com/agentscope-ai/QwenPaw/issues/7306) | Textarea focus jumps down a line on multi-line input | No fix PR yet |
| **Low/UI** | [#7282](https://github.com/agentscope-ai/QwenPaw/issues/7282) | Markdown lists render with excessive vertical spacing in Console | Closed — fixed |

**Health signal:** The majority of new bugs today are **UI/UX-level** rather than core logic failures, with the notable exception of [#7311](https://github.com/agentscope-ai/QwenPaw/issues/7311) (missing module) and [#7298](https://github.com/agentscope-ai/QwenPaw/issues/7298) (TLS). The NSIS installer fix from yesterday is being iteratively hardened via [#7323](https://github.com/agentscope-ai/QwenPaw/pull/7323) and [#7336](https://github.com/agentscope-ai/QwenPaw/pull/7336).

---

## 6. Feature Requests & Roadmap Signals

**Strong signals (likely in v2.2.0):**

1. **Multi-tenant Hub (v2.2.0)** — [#7318](https://github.com/agentscope-ai/QwenPaw/issues/7318) is an official roadmap thread; earlier requests [#5780](https://github.com/agentscope-ai/QwenPaw/issues/5780) and [#4702](https://github.com/agentscope-ai/QwenPaw/issues/4702) show years-long demand for RBAC/admin/multi-user. **This is the headline feature of the next release.**

2. **Chat scroll locking** — [#7339](https://github.com/agentscope-ai/QwenPaw/issues/7339) opened today; an immediate fix PR exists ([#7340](https://github.com/agentscope-ai/QwenPaw/pull/7340)). Likely lands in v2.2.0b2.

3. **MCP Streamable-HTTP dual-protocol client** — [#7330](https://github.com/agentscope-ai/QwenPaw/pull/7330) merges modern (2026-07-28) and legacy MCP protocols with fallback. Indicates ongoing MCP ecosystem investment.

**Moderate signals (candidates for next patch/minor):**

- **Prompt cache hit-rate observability** — [#7335](https://github.com/agentscope-ai/QwenPaw/issues/7335) opened today with documented 81.68% vs OpenCode's 96.02%, direct cost impact. Labels: `good first issue`.
- **Auto-clear completed background tasks** — [#7280](https://github.com/agentscope-ai/QwenPaw/issues/7280).
- **Model choice popup instead of text input** — [#7279](https://github.com/agentscope-ai/QwenPaw/issues/7279).
- **OpenViking-backed long-term memory** — [#7252](https://github.com/agentscope-ai/QwenPaw/issues/7252) — architecture pre-PR discussion.

---

## 7. User Feedback Summary

**Pain points (recurring):**

- **"Agent stalls mid-task"** is the most-upvoted complaint ([#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921), 11 comments). Users describe a pattern where the model says "Let me do X" then goes silent, requiring manual nudge. This degrades trust in autonomous execution.
  
- **Windows installer friction continues** despite fixes. [#6810](https://github.com/agentscope-ai/QwenPaw/issues/6810) details a nightmarish uninstall/install flow with NSIS file-lock errors. The PRs [#7323](https://github.com/agentscope-ai/QwenPaw/pull/7323) and [#7336](https://github.com/agentscope-ai/QwenPaw/pull/7336) show iterative fixing — but the **third iteration in 24h** suggests root-cause complexity remains.

- **Memory/context confusion in long sessions** ([#7193](https://github.com/agentscope-ai/QwenPaw/issues/7193)): Agent searched and pulled content from **another session** of the same agent, causing task derailment. This is a serious correctness issue for multi-session users.

- **Missing push notifications for scheduled task success** ([#7324](https://github.com/agentscope-ai/QwenPaw/issues/7324)) — reliability concern for automation workflows.

**Positive signals:**

- The team's **responsiveness** is notable: bugs filed on 08-25/08-26 are either closed or have PRs by 08-27 (e.g., [#7258](https://github.com/agentscope-ai/QwenPaw/issues/7258), [#7206](https://github.com/agentscope-ai/QwenPaw/issues/7206), [#7212](https://github.com/agentscope-ai/QwenPaw/issues/7212)).
- **Test coverage culture** is improving measurably (+5pp unit, +5.49pp console, 23 E2E cases) — visible response to community reliability concerns.
- Multi-tenant Hub is a **community-requested feature** finally landing — anticipation is high and positive.

---

## 8. Backlog Watch

Items that have been open for a while without clear resolution or maintainer response:

1. **[#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921) — Agent stops mid-task (open since 08-12, 11 comments, no fix PR).** This is the single most-commented issue on the tracker and is directly tied to core product trust metrics. **Needs a maintainer response / repro guidance.**

2. **[#7193](https://github.com/agentscope-ai/QwenPaw/issues/7193) — Cross-session memory contamination (open since 08-21, labeled need-info).** Silent data leakage between sessions is a correctness issue; no visible response yet.

3. **[#7298](https://github.com/agentscope-ai/QwenPaw/issues/7298) — OpenSSL 3.0.x TLS stack (open since 08-25).** Fix PR exists ([#7328](https://github.com/agentscope-ai/QwenPaw/pull/7328)) but is still **open** — bumping Python to 3.13 across 5 desktop workflows is a large surface-area change. Monitor merge progress.

4. **[#7296](https://github.com/agentscope-ai/QwenPaw/issues/7296) — OpenAI Responses multi-turn 400 error on stateless upstreams (open since 08-25).** Affects users via OpenCode Zen/Go Muse Spark. No fix PR yet.

5. **[#7229](https://github.com/agentscope-ai/QwenPaw/issues/7229) — Local test runner false-success (opened 08-24 causing silent test skipping).** Fix merged in [#7250](https://github.com/agentscope-ai/QwenPaw/pull/7250) — **confirm the fix is in the release cut**.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-27

## 1. Today's Overview

ZeroClaw is in a period of high architectural activity, with 26 issues and 50 PRs updated in the last 24 hours. The project is executing on several accepted RFCs, notably the Gemini Live realtime speech-to-speech broker channel (#8780) and session-scoped persistent prompt attachments (#9998), with dedicated implementation trackers (#10406, #10405) opened today. Security hardening remains a dominant theme, with multiple in-flight PRs addressing SSRF protection, symlink race conditions, and authenticated webhook ingress. The merge rate is modest (3 PRs closed/merged), but the large volume of open PRs (47) combined with the presence of a **maintainer decision queue tracker (#8692)** suggests maintainer bandwidth is a pacing factor. Overall, the project is healthy and shipping steady stabilization work alongside substantial new feature development.

## 2. Releases

No new releases were published in the last 24 hours. The **v0.8.5 stabilization line** (tracker #9459) is active through August 30, 2026, with weekly cuts shipping ready work; the **v0.9.0 milestone** (tracker #7432) continues accumulating breaking-change and auth/security work.

## 3. Project Progress

Three PRs were merged or closed in the last 24 hours:

- **#9725** — *fix(channels): clear delivery registry when reload removes all channels* — Closed (merged). Fixes bug #9591 where removing all channels via reload left a stale delivery registry, potentially causing messages to be routed to non-existent channels.
- **#10396** — *reasoning_content is replayed for every assistant message in history* — Closed. A bug fix in the OpenAI provider that prevented re-sending all historical reasoning content with each request.
- **#10235** — *[Docs]: update SECURITY.md distroless base to Debian 13* — Closed. Documentation update aligning SECURITY.md with the current container base image.

Most notably, the **session-scoped persistent prompt attachments** feature (#9998) saw its implementation PR (#10407) opened today by `vrurg`, adding SQLite-backed durable prompt attachments with approval-gated tools.

## 4. Community Hot Topics

- **#8780 — RFC: Realtime speech-to-speech channel for Gemini Live** (21 comments) — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/8780). The most-discussed item. The proposal has gone through two revisions, evolving into a broker contract. The demand for realtime voice interaction is significant; an implementation tracker (#10406) was opened today, signaling maintainer commitment. *Signal: high user interest in multimodal, low-latency interactions.*

- **#8692 — [Tracker]: Maintainer decision queue for RFCs and design issues** (14 comments) — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/8692). A meta-issue tracking pending maintainer decisions. Its activity reflects a community that is actively shepherding proposals through review. *Signal: the community values transparency in governance; a backlog of un-reviewd PRs (see #10346, #10366) suggests this queue may be overloaded.*

- **#9600 — [Tracker]: Session-persistence contract ownership and layer ordering** (13 comments) — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9600). Addresses a known architectural pain point: four independent workstreams touching the same persistence contract. Today's PR #10407 (prompt attachments) and #10380 (restore persisted ACP transcripts) both touch this area, highlighting the risk of merge conflicts and contract drift. *Signal: technical debt from parallel development; the community is aware and pushing for a clear owner.*

## 5. Bugs & Stability

Ranked by reported severity:

- **S1 — #10230: Daemon startup stack overflow during agent init** (*zerocode/tui*) — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/10230). A `quickstart` config apply can abort a Tokio worker with a stack overflow. Needs reproduction. **No fix PR yet.**
- **S0/S1 — #10379: Unable to cancel ongoing message in ZeroClaw Desktop** (*web dashboard*) — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/10379). Reported as S0 (data loss risk) with a disabled cancel button and no message-queueing. **No fix PR yet.**
- **S2 — #10186: Terminal fallback text bypasses live delivery seams** (*runtime/daemon*) — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/10186). Two paths return fallback strings outside the live delivery contract. **No fix PR yet.**
- **S2 — #10390: Entering an inactive Chat pane blocks ZeroCode navigation** — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/10390). **No fix PR yet.**
- **S2 — #10349: SOP pane loading blocks ZeroCode navigation** — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/10349). **No fix PR yet.**
- **P2 — #10394: MCP tool results stored as whole envelope, duplicating payloads** — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/10394). Newly reported.

Three bug-fix PRs are currently open, representing a backlog of high-risk fixes awaiting maintainer review: **#10367** (symlink race prevention), **#10236** (daemon capture log bounds), and **#10075** (live config threading).

## 6. Feature Requests & Roadmap Signals

- **#10400 — Configurable Telegram unauthorized-sender notice** — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/10400). A small, focused enhancement letting operators customize the notice and align it with the actual authorization path. Likely to ship in a near-term minor release given its scope.

- **#10298 — Make URLs clickable in ZeroCode transcripts** — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/10298). A UI/UX polish item, marked `in-progress`.

- **#9241 — Microsoft Teams channel** — [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9241). A large PR (size:XL) adding a Teams/Bot Framework channel remains open with no maintainer review yet.

- **#9222 — LLM-judge grader for eval** — [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9222). Diagnostic-first, deliberately off the gate until calibrated; will be a significant eval feature once proven.

**Prediction for v0.9.0:** Bounded by the v0.9.0 tracker (#7432), the most likely inclusions are: the authenticated webhook ingress refactor (already closed as #9587, likely merged), the ZeroRelay secure transport from **#10142**, the SSRF hardening for `file_download` (stacked PRs #10070/#10075/#10072), and the two newly-tracked implementations (#10406, #10405). The Gemini speech-to-speech channel is a stretched goal.

## 7. User Feedback Summary

- **High demand for realtime voice interaction.** The Gemini Live channel RFC (#8780) is the most-commented issue and has a dedicated implementation tracker; this is a top community-requested capability.

- **Desktop UX is a pain point.** Issue #10379 (cancel button broken, no message queue) was flagged at S0 severity by a user and demonstrates frustration with the Desktop workflow being interrupted.

- **Frustration with blocked navigation in ZeroCode.** Two reports (#10390, #10349) show that synchronous pane initialization makes the TUI temporarily unresponsive, degrading the interactive experience.

- **Active contributors are pushing for architectural clarity.** The tracker issues (#9600, #8692) and the many `needs-author-action` PRs (e.g., #8965, #10070) suggest contributors are ready to move faster but are waiting on author revisions or maintainer decisions.

## 8. Backlog Watch

Items that have been open and silent for a while, or are long-unanswered, needing maintainer attention:

- **#10070 — feat(tools): gate file_download against SSRF** — [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/10070). Open since 2026-08-18, marked `blocked` and `do-not-merge`. The first slice of SSRF hardening has been waiting for review; the stacked PRs #10075 and #10072 depend on it.

- **#8965 — feat(skills): declarative auto-activation with provider switch** — [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/8965). Open since 2026-07-11 (over a month), size XL, needs author action. Significant feature that has been restacked at least once; the author engagement may be waning.

- **#9222 — feat(eval): per-dimension LLM-judge grader** — [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9222). Open since 2026-07-20, size XL, needs author action. Important eval infrastructure, but stale.

- **#10346 — RFC: Gateway and channels heartbeat worker caching pattern** — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/10346). New, but addresses an acknowledged inefficiency (MCP servers spawn 3x on boot). Needs a maintainer verdict on the proposed design.

- **#10366 — RFC: Clarify PR review evidence and author-action boundaries** — [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/10366). Directly aims at reducing the `needs-author-action` backlog. With 47 open PRs, a clear policy here would likely unblock several stalled efforts.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*