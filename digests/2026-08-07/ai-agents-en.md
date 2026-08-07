# OpenClaw Ecosystem Digest 2026-08-07

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-07 01:58 UTC

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

# OpenClaw Project Digest — 2026-08-07

## 1. Today's Overview

OpenClaw shows a **highly active project** with 500 issues and 500 PRs updated in the last 24 hours. The open/active issue count (432) far exceeds closed (68), reflecting a **heavy triage backlog**; the same pattern holds for PRs (405 open vs 95 merged/closed). No new releases were published in this window, suggesting the team is consolidating work toward the next stable cut. Notably, **no new P0 issues were opened today**, and the existing P0 items (#119263, #118772) have linked fix PRs in flight. Project health is characterized by a **high volume of maintainer-reviewed, well-labeled issues** (with priority, impact, and rarity ratings), but also a significant number of items awaiting maintainer/product decisions.

## 2. Releases

**No new releases were published in the last 24 hours.**

## 3. Project Progress

**Key merged/closed PRs (68 total closed/merged):**

- **[PR #117961 — fix(canvas): serve Content-Length on A2UI HEAD responses](https://github.com/openclaw/openclaw/pull/117961)** (CLOSED, proof: sufficient, P2) — Fixes HEAD responses to include Content-Length per RFC 9110 §9.3.2.
- **[PR #118749 — fix(gateway): make doctor dreaming timestamp comparators NaN-safe](https://github.com/openclaw/openclaw/pull/118749)** (CLOSED, proof: sufficient, P2) — Prevents crashes when `doctor` encounters malformed `lastRecalledAt` timestamps.
- **[PR #119689 — fix(heartbeat): explain target-none skips](https://github.com/openclaw/openclaw/pull/119689)** (CLOSED, proof: sufficient, P3) — Adds operator-facing message when heartbeat delivery is intentionally disabled via `target: none`.

**Notable active PRs (merged/closed count 95):**

- **[PR #120083 — fix(ui): make active-run steering reliable](https://github.com/openclaw/openclaw/pull/120083)** (OPEN, P1, ready for maintainer look) by steipete — Fixes a live failure where user steering of active Control UI runs was downgraded to "Needs review."
- **[PR #119902 — feat(audit): carry execution identity into approvals](https://github.com/openclaw/openclaw/pull/119902)** (OPEN, P2, diamond lobster) — Large XL PR addressing immutable execution/context pairing for approvals, blocked on the stacked #116793.
- **[PR #120078 — fix(codex): preserve configured MCP tools in cron runs](https://github.com/openclaw/openclaw/pull/120078)** (OPEN, XL, waiting on author) — Fixes isolated Codex automations losing MCP tool access.

**Feature advancement:** No single merged PR dominates, but the audit/execution-identity stack (PRs #116792–#116794, #119902) and the portable-profiles Claws bootstrap (#115237) indicate **major architecture work moving forward**.

## 4. Community Hot Topics

- **[#75 — Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)** — 116 comments, 80 👍 (CLOSED). The most-reacted issue in the project, indicating **massive demand** for Linux and Windows desktop apps. Its closure suggests this may have been addressed (or scheduled) — worth confirming closure reason.
- **[#116277 — DeepSeek v4 Flash silent reply failure](https://github.com/openclaw/openclaw/issues/116277)** — 114 comments (CLOSED, P1, diamond lobster). Silent reply-generation failures caused by DeepSeek v4 Flash; high engagement signals a **provider-specific reliability concern** impacting real users.
- **[#7707 — Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707)** — 28 comments, 🎯 **

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Report: Personal AI Assistant & Agent Frameworks
**Date: 2026-08-08 | Coverage Window: 2026-08-07**

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing **rapid, broad-based maturation** with a clear bifurcation between large-scale frameworks (OpenClaw, Hermes Agent, IronClaw, CoPaw) and focused utilities (NanoBot, NanoClaw, PicoClaw). The ecosystem is converging on several shared challenges: **self-update reliability, cross-channel delivery correctness, memory system fidelity, and observability/diagnostics**. Security is a dominant theme — multiple projects addressed credential leakage (NanoBot), confused-deputy vulnerabilities (ZeroClaw), and secrets hygiene (Hermes Agent) within the same 24-hour window. The ecosystem is transitioning from "demo-quality" agents to production infrastructure, with users demanding enterprise-grade reliability (transactional updates, failure transparency, cost observability) and surfacing deep integration friction with heterogeneous model providers (DeepSeek reasoning tokens, Bedrock caching quirks, slash-prefixed model IDs).

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs | Release Status | Health Score* |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 95 (68 closed) | No new release; consolidation | 7.5/10 |
| **Hermes Agent** | 50 | 50 | High volume, not enumerated | No new release; 0.20.0 regressions | 7.0/10 |
| **IronClaw** | 50 | 50 | 17 | **v1.1.0 (2026-08-06)** | 7.5/10 |
| **CoPaw** | 34 | 50 | 30 | No new release; 2.0.x regression testing | 6.5/10 |
| **ZeroClaw** | 31 | 50 | 5 | No new release; 0.8.4 stabilization line | 6.5/10 |
| **NanoBot** | 9 | 17 | 5 | No new release | 8.0/10 |
| **NanoClaw** | — | 14 | 8 | No new release | 8.0/10 |
| **PicoClaw** | 0 | 2 | 1 | No new release | 7.5/10 |
| **LobsterAI** | 5 | 2 | 0 | No new release | 4.5/10 |
| **NullClaw** | 0 | 0 | 0 | Inactive | — |
| **TinyClaw** | 0 | 0 | 0 | Inactive | — |
| **Moltis** | 0 | 0 | 0 | Inactive | — |
| **ZeptoClaw** | 0 | 0 | 0 | Inactive | — |

*Health score = responsiveness (closure rates), fix availability for reported bugs, maintainer engagement, and release cadence relative to project scale.*

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale dominance**: OpenClaw's 500/500 issues/PRs updated in 24h dwarfs all peers — 10x the activity of Hermes Agent or IronClaw, the next busiest. It is the clear reference implementation in the ecosystem.
- **Governance maturity**: The project's use of priority (P0-P3), impact, and rarity labels on every issue, plus structured linked-fix-PR tracking, indicates a **production-grade triage culture** that most peers (especially LobsterAI, ZeroClaw) lack.
- **Architecture investment**: The audit/execution-identity stack (#116792–#116794, #119902) and portable-profiles bootstrap (#115237) represent **foundational architectural work** — peers are mostly fixing bugs, not redesigning core constraints.

**Technical approach differences:**
- OpenClaw pursues **execution identity immutability** (binding execution context to approvals) — a security-first design pattern not yet visible in peers.
- The project's `target: none` heartbeat semantics and NaN-safe timestamp handling show **defensive engineering attention** to edge cases that smaller projects defer.

**Community size comparison:**
- OpenClaw's most-reacted issue (#75, Linux/Windows apps) amassed **116 comments and 80 👍** — more engagement than entire projects (LobsterAI, PicoClaw) generate in total. The community's demand for desktop client parity is a signal of **enterprise/consumer crossover ambitions**.

**Area for attention**: The open-to-closed ratio (432 open issues vs 68 closed) suggests **triaging capacity is strained** despite the label-rich culture. The team should consider community-maintainer programs or automation to reduce backlog pressure.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Requirements |
|---|---|---|
| **Self-update & upgrade safety** | NanoClaw, Hermes Agent | Transactional updates (#3195), validation-gated cutover, rollback paths. Hermes faces 0.20.0 regressions (desktop panel loss, memory sync breakage). |
| **Model provider compatibility** | CoPaw, ZeroClaw, Hermes Agent, LobsterAI, OpenClaw | DeepSeek reasoning token handling (#6667), Bedrock Nova caching quirks (#8720), slash-prefixed model IDs (#2443), provider-specific silent failures (#116277). |
| **Channel delivery reliability** | IronClaw, CoPaw, NanoClaw, ZeroClaw | Wrong-target Slack delivery (#5877), retry/reconnection for Matrix (#6684), reply-to-bot detection (#2644), empty allowlist default-deny (#9397). |
| **Memory system integrity** | Hermes Agent, NanoBot, OpenClaw | `sync_turn()` never called (#79339), stale background task overwrites (#5271), session retention drops (#5273), trust tagging by source (#7707). |
| **Observability & diagnostics** | IronClaw, NanoBot, CoPaw, ZeroClaw | Inspector tooling (IronClaw #7235), per-call token logging (#5266), SOP failure audit trails (#9784), tool-level transparency (#5701). |
| **MCP tool lifecycle** | CoPaw, Hermes Agent, OpenClaw | Stale MCP tools requiring restart (#6732), `args: null` crashes (#80652), preserving MCP tools in cron runs (#120078), stdio allowlisting (#62808). |
| **Per-session model switching** | NanoBot, IronClaw, ZeroClaw | Mid-conversation model switching (#5198), per-model capability config (#7100). |
| **Secret/credential security** | NanoBot, Hermes Agent, ZeroClaw | API key leakage into env (#5270/#5269), child-process env scrub (#77164), pipeline tool policy enforcement (#7947). |

---

## 5. Differentiation Analysis

| Project | Feature Focus | Target Users | Technical Architecture |
|---|---|---|---|
| **OpenClaw** | Full-featured personal agent (UI, gateway, memory, approvals) | Power users, enterprises | Modular monorepo; audit/execution-identity binding; portable profiles |
| **Hermes Agent** | Multi-gateway agent (Telegram, Slack, Feishu) + desktop | Enterprise teams, cross-platform | God-file decomposition in progress; React-based desktop; gateway-centric |
| **IronClaw** | MCP-extensible agent with routines + sandbox | Automation workflows, operators | WASM tools; Docker sandbox; Inspector diagnostics; two-lane delivery |
| **CoPaw** | AgentScope-integrated agent (Qwen-ecosystem) | Chinese-speaking users, WeChat/Matrix | Deep AgentScope coupling; Scroll context protocol; Codex CLI compatibility |
| **ZeroClaw** | Crypto/verifiable-intent agent with SOP subsystem | Security-conscious teams, governance-focused | Rust-based (clippy, ZeroCode); A2A support; verifiable intents |
| **NanoBot** | Lightweight personal assistant (WebUI-first) | Individual users, developers | Fast iteration; WebUI-centric; Matrix/Discord channels; Dream memory |
| **NanoClaw** | Community bot platform (Telegram/QQ) | Community moderators, bot runners | Chat SDK bridges; scheduling; skill system; launchd/systemd managed |
| **PicoClaw** | Channel adapters (QQ focus), multi-model routing | Niche channel integrators | Long-running PR culture; feature-driven; minimal issue volume |
| **LobsterAI** | Windows-based agent IDE (PowerShell) | Windows power users | Electron + PS 5.1; Cowork/OpenClaw config propagation; stale PR backlog |

**Notable architecture differentiators:**
- **OpenClaw & IronClaw** both pursue audit/inspection as first-class features — expect convergence on operator-facing diagnostics as a competitive battleground.
- **CoPaw** is uniquely coupled to AgentScope/Qwen ecosystem — a moat but also a dependency risk (#6612).
- **ZeroClaw** is the only Rust-based project with crypto-native verifiable intents — distinct security posture.
- **NanoBot/NanoClaw** demonstrate that **velocity can coexist with quality** (highest health scores, most responsive fixes) despite smaller team footprints.

---

## 6. Community Momentum & Maturity

| Tier | Projects | Characteristics |
|---|---|---|
| **Tier 1: Rapid Iteration** | OpenClaw, Hermes Agent, IronClaw, ZeroClaw | 50-500 PRs/24h; architectural investment; security hardening; large contributor bases |
| **Tier 2: Steady Growth** | CoPaw, NanoBot, NanoClaw | 10-50 PRs/24h; strong responsiveness; moderate scale; regression testing active |
| **Tier 3: Maintenance Mode** | PicoClaw | Low volume; long-running PRs; stable but slow feature delivery |
| **Tier 4: Stagnation Risk** | LobsterAI | 4-month-old PRs unmerged; issues stale; no release cadence signal |
| **Tier 5: Dormant** | NullClaw, TinyClaw, Moltis, ZeptoClaw | Zero activity in 24h window; effectively parked |

**Key observations:**
- **IronClaw's v1.1.0 release** with integrations (MCP, Slack, attachments) + simultaneous regression bug influx indicates an **"accelerate-then-stabilize" rhythm** that is healthy but requires dedicated QA cycles.
- **CoPaw** is in the most vulnerable position: 2.0.x regressions are still being discovered while the maintainer base appears stretched (MCP issues unfixed, `agentscope` dependency breakage unresolved).
- **LobsterAI** demonstrates the **failure mode of inattentive maintenance** — four April-open items, zero merges, no communication. It risks contributor abandonment.
- **ZeroClaw's SOP issues** (5+ silent-failure bugs in one day) suggest a **shipped-recently-but-under-tested** subsystem; the team's rapid security fix (S0 in 7 weeks) shows capability, but test coverage for new subsystems needs strengthening.

---

## 7. Trend Signals

| Trend | Evidence | Implication for Developers |
|---|---|---|
| **Production reliability is now table stakes** | Transactional updates (NanoClaw), fail-closed delivery (IronClaw), audit trails (ZeroClaw), retry/reconnection (CoPaw) | Users will not tolerate silent failures anymore. Build fail-loud diagnostics, transactional operations, and rollback paths by default. |
| **Observability is the next competitive frontier** | IronClaw's Inspector; NanoBot's token-logging demands; ZeroClaw's audit-trail requests; CoPaw's session-health complaints | Agent frameworks that expose per-tool, per-call, per-token telemetry will win enterprise trust. Build introspection into the core, not as an add-on. |
| **Memory system trust is fragile** | Hermes `sync_turn` regression; NanoBot stale-save overwrites; OpenClaw trust-tagging by source | Memory correctness is a top-3 user complaint. External memory backends silently breaking (Hermes #79339) is a "trust flight" moment for users. |
| **Cross-channel consistency is hard, but required** | IronClaw's wrong-target Slack; CoPaw's Matrix retries; NanoClaw's reply-to-bot; Hermes' Feishu cards | All channels are not equal. Expect a wave of "delivery layer" abstractions (IronClaw's two-lane tool is the vanguard). |
| **Model provider complexity is a meta-problem** | DeepSeek reasoning tokens, Bedrock cache quirks, slash-IDs, empty-response freezes | Agent frameworks must build provider abstraction layers that handle semantics (reasoning/thinking tokens) not just API shapes. |
| **Self-update is a psychological barrier** | NanoClaw's brick-risk; Hermes' 0.20.0 regressions; CoPaw's agentscope breaks | The next release should never break the last one. Users punish regression-prone releases disproportionately. |
| **Security is shifting from add-on to core** | ZeroClaw S0 pipeline fix; NanoBot env leak fixes; Hermes env scrub; IronClaw fail-closed delivery | Credential handling and tool authorization are now **architectural requirements**, not patch-level considerations. |
| **Windows/desktop remains underserved** | OpenClaw #75 (80👍), LobsterAI's existence, Hermes desktop gaps | Desktop parity is a differentiator. Cross-platform desktop clients (Electron/React) are in demand, but cloud/remote parity is the new bar. |

---

## Recommendations for Technical Decision-Makers

1. **If evaluating a framework to build on**: OpenClaw offers the most mature governance and architectural investment, but expect to manage integration complexity. IronClaw's v1.1.0 + Inspector is the strongest "enterprise observability" story today.
2. **If contributing**: Highest-impact opportunities are in the shared pain areas — model-provider abstraction layers, delivery-reliability tooling, and memory-system audits. These are needed across all active projects.
3. **If adopting for production**: Monitor IronClaw's two-lane delivery PR (#7157) and OpenClaw's audit stack (#119902) — both are architectural responses to the ecosystem's top failure modes. Shield critical workflows from CoPaw's pending `agentscope` dependency question.
4. **If watching for consolidation**: NanoBot and NanoClaw are the most responsive per-contributor — their patterns (fast fixes, security-first) are worth emulating regardless of scale. LobsterAI, absent intervention, is the most likely candidate for community fork or abandonment.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-07

## 1. Today's Overview

NanoBot is showing high-velocity development with **17 PRs and 9 issues updated** in the last 24 hours — a significant uptick primarily driven by the author `chengyongru` (4 PRs) and `LHMQ878` (3 PRs) working across WebUI, provider security, and channel protocol hardening. The project closed 5 PRs and 1 issue, indicating steady delivery of fixes. The maintainer response is strong: issues like the session-retention data loss bug (#5273) received a dedicated fix PR (#5272) within hours of reporting. One notable concern: a single user (`whisperity`) filed 3 issues in the last two days around Matrix channel UX and session model-selection limitations, suggesting potential friction in those areas. Overall, the project appears healthy and responsive, with no release tagged this period.

## 2. Releases

No new releases were published in this window.

## 3. Project Progress

Five PRs were merged or closed since yesterday:

- **PR #5261** (merged) — WebUI: sidebar sessions can now be dragged into the composer to create structured mentions, and drag-reordered for persistent manual ordering (Codex-style insertion line). Improves multi-session navigation efficiency.
- **PR #5267** (merged) — WebUI motion/transition tightening: standardizes ~220ms transitions, shortens completion-only holds, and respects reduced-motion preferences for accessibility.
- **PR #5259** (merged) — WebUI: enforcement of memory-only temporary sessions. Temporary chats stay strictly in process memory — no history files, no memory capture — while still reaching the configured model provider for real completions.
- **PR #5262** (merged) — WebUI performance: precompressed gzip assets with gateway negotiation, and lazy-loaded Markdown/code/KaTeX chunks with the React runtime split out, plus a build-time regression guard. Directly addresses cold-start payload size (p1 priority).
- **PR #5248** (merged) — Matrix: sends a non-empty JSON body on room join, fixing a compatibility failure with Continuwuity homeservers that reject empty POST bodies (`M_BAD_JSON`). Fixes #5247.

## 4. Community Hot Topics

The most active discussion is **#5198** (3 comments) — users report it's impossible to switch the active model mid-conversation; the model blip near the chat input is non-interactive and `/model` doesn't behave as expected. The underlying need: **per-session model switching without global reconfiguration**, likely signaling a UX gap vs. cloud SaaS chat interfaces.

Issue **#4290** (2 comments, open since June 10) — cronjobs terminate prematurely when a subagent finishes before the main agent can process its result, breaking subsequent workflow steps. This is a critical orchestration reliability issue and is nearly two months old.

PR **#5231** (feature: archive idle sessions for Dream, the memory component) is the most substantive open feature discussion — addressing the gap where short idle sessions never get summarized into `history.jsonl`.

## 5. Bugs & Stability

Bugs ranked by severity, based on whether fixes exist and how core the failure mode is:

- **[High / fix available] PR #5271 (p0)** — Stale background task saves (e.g., `maybe_generate_webui_title`) can overwrite session data if a user runs `/new` during an in-flight provider call. Fix: prevent invalidated sessions from being re-saved by background tasks.
- **[High / fix available] PR #5270 + #5269 (p1, security)** — API keys were being leaked (a) into CLI app subprocess `os.environ` copies and (b) into process-global `os.environ` by `OpenAICompatProvider`, causing cross-instance credential swaps in multi-provider setups. Both have isolation tests.
- **[Medium / fix available] #5273 → PR #5272 (p2)** — Session retention trimming drops `_channel_delivery` proactive assistant messages (cron notifications, job deliveries) that immediately precede a user reply, causing a crash-recovery gap in workflows.
- **[Medium / fix available] #5264 → PR #5268 (p2)** — `GET /api/sessions/{key}/messages` never returns `media_urls` for attachments outside the media root (e.g., `projects/`), producing broken media on history reload. WebSocket already stages correctly; fix routes history reads through the same signing utility.
- **[Medium / no fix yet] #5266** — Excessive token consumption reported (1M tokens in 2 hours with no visible user activity); no per-call token logging exists, so users cannot debug or attribute the burn. No PR yet, but this is a p1-priority user-facing cost issue.
- **[Low / fix available] PR #5265 (p2, tool safety)** — Rejects NaN/Infinity in JSON Schema number parameters after `float()` casting, preventing downstream non-finite float propagation into tools.

## 6. Feature Requests & Roadmap Signals

Several signals point to the near-term roadmap:

- **Temporary / memory-only chat** — Two PRs (#5252 + #5259) land this as a WebUI feature: chats are created only on first message, multi-turn, non-persistent, not memory-backed. This is likely available on `main` now. A likely candidate for next release notes.
- **Idle session archiving for Dream** (#5231) — Extends memory coverage to sessions that otherwise idle without crossing the recency-protected window. Anticipate a cleanup/memory improvement merge soon.
- **Session-level file isolation** (#5276) — `restrictToWorkspace` currently shares `~/.nanobot/workspace` across all sessions; the request is for per-session temp isolation while preserving intentional global stores (skills, SOUL/USER). More of a vNext architectural decision.
- **Matrix threading as dedicated contexts** (#5274 + #5275) — Users expect matrix reply-in-thread to create separate sessions, and bot replies to be proper Matrix replies rather than bare messages. This is a UX parity request vs. Discord/Slack.
- **Metasearch provider** (#5234) — `mst-python` (Meta-Search Tool) aggregates multiple engines with RRF fusion, offering richer search coverage than a single engine. Broadens provider flexibility.
- **Shared interactive project terminal** (#5253) — A persistent, project-scoped PTY (xterm.js dock, POSIX/ConPTY) shared by WebUI and agent, with auto-open, restart, and termination controls. A deeper agent-workflow feature, likely further out.

## 7. User Feedback Summary

Common pain points this week cluster around three themes:

- **Model control**: The inability to switch models per-session without reconfiguration (#5198) is a clear UX mismatch; users expect the model blip to behave like SaaS chat UIs.
- **Matrix UX friction**: Complaints about bare top-level replies, non-threaded responses, and a join failure on Continuwuity (#5247, #5274, #5275) suggest the Matrix channel needs a UX pass on reply/thread semantics.
- **Cost & transparency**: Token burn (~1M in 2h) without per-call logging (#5266) indicates a lack of observability as a Trust & Safety gap. Enforcement of proactivity/deliverability (retention drops, #5273) also matters to workflow users.
- **Security awareness**: Users are filing (and maintainers are rapidly fixing) secrets-leakage issues, which is reassuring for trust in the agent platform.

## 8. Backlog Watch

- **#4290 — cronjob ends early when a subagent spawns** (open since June 10, 2 comments). This is the longest-standing open bug with a real workflow impact. It has no linked fix PR yet. Maintainer attention is strongly recommended.
- **#5198 — model switching blocked per-session** (updated Aug 7, 3 comments; open since Jul 31). Needs a product-level decision on the intended model-switching UX.
- **#5266 — excessive token consumption with no logging** (no PR yet). High user cost, no real code fix produced; the only ask is observability, which should be easy for maintainers to deliver.
- **PR #5231 — archive idle sessions for Dream** (open since Aug 3, no maintainer review comments). One of the more substantive memory improvements on the table; appears stalled pending review.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date: 2026-08-07**

---

## 1. Today's Overview

Hermes Agent is experiencing a **high-velocity development day**, with 50 issues and 50 PRs updated in the last 24 hours — a clear signal of an active and engaged contributor community. The project is in a **significant refactoring cycle**, driven by a standing policy to decompose all "god files" (monolithic source files) into clean, modular components, with multiple architecture epics tracking this work. Simultaneously, there is a strong **bug-fixing surge** focused on stability across gateway platforms (Telegram, Slack, Feishu), desktop app functionality, and session-state integrity. The project maintains a **triaged, label-rich issue culture**, with severity (P1/P2/P3), component, platform, and risk tags applied consistently, though the high volume of `needs-decision` and `needs-repro` labels suggests some items may be awaiting maintainer attention. Notable attention is being given to **security hardening**, **memory provider contract fidelity**, and **streaming reliability**, reflecting a mature codebase tackling both architectural debt and production-grade robustness concerns.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The last known release was **v0.20.0**, which has been the subject of several regression reports (see Bugs & Stability section).

---

## 3. Project Progress

The following PRs were **merged or closed** in the last 24 hours:

| PR | Title | Summary |
|---|---|---|
| [#80422](https://github.com/NousResearch/hermes-agent/pull/80422) | Fireworks user agent | Closed; likely a trivial fix or superseded (no summary provided). |
| [#80702](https://github.com/NousResearch/hermes-agent/pull/80702) | fix(desktop): render agent reactions live | **Merged.** Routes live `message.reaction` updates through the owning runtime's authoritative session state, publishing only when that runtime owns the active transcript. Fixes the need for reload to see agent reactions. |
| [#80699](https://github.com/NousResearch/hermes-agent/pull/80699) | The desktop's tools reach it on remote and cloud backends too | **Merged.** Removes the `HERMES_DESKTOP=1` env-var gate that stripped the desktop's pane, in-app browser, and reaction tools when connecting to plain URL gateways or Hermes Cloud. |

**Key architectural advances through merged code:**
- **Cross-platform desktop parity** (PR #80699) — This is a significant fix, ensuring that the desktop client's full tool surface is available on remote and cloud backends, not just locally spawned Electron runtimes.

---

## 4. Community Hot Topics

The most actively discussed items reveal three dominant community concerns:

### 1. Repository-Wide God-File Decomposition ([#78647](https://github.com/NousResearch/hermes-agent/issues/78647)) — 51 comments
This epic by `andrexibiza` codifies the policy that **"all god files are sharded, never reverted"** and serves as the tracking issue for repo-wide decomposition. It has spawned multiple sub-issues (e.g., [#78645](https://github.com/NousResearch/hermes-agent/issues/78645) for `context_compressor.py` at 6,789 lines, [#78637](https://github.com/NousResearch/hermes-agent/issues/78637) for `hermes_cli/auth.py` at 9,180 lines, [#78792](https://github.com/NousResearch/hermes-agent/issues/78792) for Telegram `adapter.py` at 10,147 lines).
- **Underlying need:** Maintainability and contributor onboarding; massive files are a barrier to entry and a source of regression risk.

### 2. Plugin Interface Expansion ([#64182](https://github.com/NousResearch/hermes-agent/issues/64182)) — 27 comments
A community-driven tracking issue sourced from Discord (#plugins-interface-ideas, July 4 2026). This is the reference plan for expanding the agent's plugin interface, aiming to let long-queued contributor PRs ship with stable, public APIs.
- **Underlying need:** The community wants a stable plugin contract to build against; without it, external innovation stalls.

### 3. Feishu (Lark) Approval Card Failures — Persistent, Cross-Version
This is a **cluster of at least 5 related issues** spanning multiple versions (0.8.0 to 0.15.2) and error codes (200340, 200343, 220340). The most active: [#7675](https://github.com/NousResearch/hermes-agent/issues/7675) (8 comments) and [#13924](https://github.com/NousResearch/hermes-agent/issues/13924) (6 comments).
- **Underlying need:** Feishu is a major enterprise platform; broken approval buttons (Allow Once / Session / Always / Deny) severely impact safety-critical command authorization workflows. One user notes PR #10256 provides the correct fix but remains unmerged, pointing to a potential review bottleneck.

---

## 5. Bugs & Stability

The project's P1 and high-impact P2 bugs are listed below; the volume of fixes in flight suggests a strong stability push today.

### P1 (Critical)
| Issue | Title | Fix PR? |
|---|---|---|
| [#80624](https://github.com/NousResearch/hermes-agent/issues/80624) | Cron jobs disappear when written by a sibling process during unlocked `jobs.json` save | **Yes** — [#80703](https://github.com/NousResearch/hermes-agent/pull/80703) |
| [#80598](https://github.com/NousResearch/hermes-agent/issues/80598) | Gateway fatal disconnect wedge leaves Telegram with no retry path | **Yes** — [#80700](https://github.com/NousResearch/hermes-agent/pull/80700) |
| [#80622](https://github.com/NousResearch/hermes-agent/issues/80622) | Reference-only compaction handoff incorrectly becomes the active turn, resuming stale work | **Yes** — [#80696](https://github.com/NousResearch/hermes-agent/pull/80696) |
| [#80216](https://github.com/NousResearch/hermes-agent/issues/80216) | `/retry` rewrites delete soft-archived compaction history (data loss) | **Yes** — [#80695](https://github.com/NousResearch/hermes-agent/pull/80695) |

### P2 (High)
| Issue | Title | Fix PR? |
|---|---|---|
| [#79407](https://github.com/NousResearch/hermes-agent/issues/79407) | **0.20.0 Regression:** Desktop bottom operation panel completely missing (viewer-only shell) | Unknown |
| [#79339](https://github.com/NousResearch/hermes-agent/issues/79339) | `MemoryProvider.sync_turn()` never called in 0.20 — external memory backends silently break | Unknown |
| [#80646](https://github.com/NousResearch/hermes-agent/issues/80646) | `agent_context` hardcoded to "primary" — provider context-skip logic (cron/flush/subagent) is dead code | Unknown |
| [#80652](https://github.com/NousResearch/hermes-agent/issues/80652) | MCP stdio bridge crashes (`TypeError`) when `args` is null — `connecting -> parked` loop | Unknown |
| [#79628](https://github.com/NousResearch/hermes-agent/issues/79628) | `use_gateway: true` discards valid direct credentials on unauthenticated gateway | Unknown |
| [#80259](https://github.com/NousResearch/hermes-agent/issues/80259) | Message reactions gated off for remote-desktop sessions (`HERMES_DESKTOP` only set locally) | **Fixed** — see [#80699](https://github.com/NousResearch/hermes-agent/pull/80699) (merged) |

### P3 (Notable)
| Issue | Title |
|---|---|
| [#80596](https://github.com/NousResearch/hermes-agent/issues/80596) | Learning graph marks externally-installed skills as 'learned' (use_count inflation) |
| [#80522](https://github.com/NousResearch/hermes-agent/issues/80522) | Zero-match casing probe withholds found paths — causes +6 turn re-search spirals in weak models |
| [#41331](https://github.com/NousResearch/hermes-agent/issues/41331) | Email IMAP/SMTP login user hardcoded to `EMAIL_ADDRESS` — breaks custom domains |
| [#77164](https://github.com/NousResearch/hermes-agent/issues/77164) | Child-process env scrub is name-shape heuristic — non-credential-shaped secrets leak |

**New fixes in flight (open PRs today):**
- [#80709](https://github.com/NousResearch/hermes-agent/pull/80709) `read_file` binary false-positive on UTF-8 truncation
- [#80706](https://github.com/NousResearch/hermes-agent/pull/80706) SessionDB connection fd leak on agent close (~490 leaked fds observed)
- [#80704](https://github.com/NousResearch/hermes-agent/pull/80704) Slack channel-directory startup resolution cap (911 IDs in production)
- [#80701](https://github.com/NousResearch/hermes-agent/pull/80701) Streaming response total wall-clock lifetime cap (30 min default)
- [#80627](https://github.com/NousResearch/hermes-agent/pull/80627) `agent_passthrough_commands` + clearable Telegram menu

---

## 6. Feature Requests & Roadmap Signals

Given the active pipeline, the following features are strong candidates for the **next minor version (0.21.0)**:

1. **Per-job `deliver_profile` for cron** ([#70849](https://github.com/NousResearch/hermes-agent/issues/70849)) — Enables multiplexed gateway cron delivery to use a specific profile's adapter rather than the default. High demand for QQ Bot and multi-profile setups.

2. **Usage/Cost Analytics Surface** ([#77221](https://github.com/NousResearch/hermes-agent/issues/77221), [#77222](https://github.com/NousResearch/hermes-agent/issues/77222), [#77223](https://github.com/NousResearch/hermes-agent/issues/77223)) — A cluster of feature requests to surface the already-metered token/cost data in the desktop app and aggregate views (per-day time series, included/estimated/unknown cost buckets). Core metering exists; this is a presentation-layer gap.

3. **Grok/xAI Feature Parity Campaign** ([#80424](https://github.com/NousResearch/hermes-agent/issues/80424)) — Systematic alignment with the official xAI platform (Models, Chat/Responses, Function calling, Reasoning, Streaming, Imagine, Voice/TTS). Meta-issue with a clear roadmap.

4. **MCP stdio command allowlist** ([#62808](https://github.com/NousResearch/hermes-agent/pull/62808)) — Security feature, default-off, to validate resolved MCP commands against a fixed interpreter set pre-spawn. Pending from July; security-positive, likely to land.

5. **Streaming lifetime cap** ([#80701](https://github.com/NousResearch/hermes-agent/pull/80701)) — Already in open PR; the port of qwen-code#8602 is a strong candidate for inclusion.

---

## 7. User Feedback Summary

**Pain Points (Recurring Themes):**
- **Feishu approval card failures (highest frequency):** Users across multiple versions (0.8.0, 0.15.2) report `出错了，请稍后再试 code: 200340 / 200343 / 220340` when clicking approval buttons on Feishu. This is a **critical, unresolved safety workflow issue** that is actively affecting enterprise users.
- **0.20.0 Regression dissatisfaction:** The desktop app being a "viewer-only shell" without the bottom operation panel is reported as "not a cosmetic issue" — a functional blocker. Memory provider sessions silently not syncing compounds the distrust of the 0.20.0 upgrade.
- **Remote/cloud desktop gaps:** Users connecting the desktop client to non-local gateways found six of its core tools (pane, browser, reactions) missing until PR #80699 merged. This suggests an untested usage pattern that has now been addressed.
- **Config footguns:** MCP `args: null` crashes, email login user hardcoding, and `use_gateway` discarding valid credentials all point to a need for **better input validation and clearer error messages**.

**Satisfaction Signals:**
- The **fast turnaround on P1 bugs** (5 P1 fix PRs created within 24h of the related issues) indicates strong maintainer/contributor responsiveness.
- The **plugin interface expansion tracking issue** shows that maintainers are listening to community governance needs.

---

## 8. Backlog Watch

The following issues/PRs are potentially stuck or require maintainer attention:

1. **Feishu "PR #10256" bottleneck** — Per [#38305](https://github.com/NousResearch/hermes-agent/issues/38305): "PR #10256 provides the correct fix but remains unmerged." The same error persists across 5+ issues and 4 versions. **Action: Review/merge PR #10256 and verify the broader Feishu card action path.**

2. **Memory provider contract debts** — [#79339](https://github.com/NousResearch/hermes-agent/issues/79339) (`sync_turn` never called) and [#80646](https://github.com/NousResearch/hermes-agent/issues/80646) (`agent_context` hardcoded) both touch the memory provider contract. No fix PRs are visible. **Action: Audit memory provider invocation sites in 0.20+ for regressions.**

3. **Long-dormant security PR** — [#62808](https://github.com/NousResearch/hermes-agent/pull/62808) (MCP stdio allowlist) has been open since July 11 without merge activity on the PR itself. Security-positive and default-off; needs review.

4. **`needs-repro` limbo** — [#77286](https://github.com/NousResearch/hermes-agent/issues/77286) (Windows update program error submission) and [#77484](https://github.com/NousResearch/hermes-agent/issues/77484) (emission gaps) may need community reproduction attempts to move forward.

5. **Shutdown forensics false-positive** ([#61003](https://github.com/NousResearch/hermes-agent/issues/61003)) — Open since July 8; a known, reproducible false warning. Low severity but degrades trust in diagnostics.

---

*Digest generated from GitHub activity data for NousResearch/hermes-agent on 2026-08-07.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest
**Date:** 2026-08-07

---

## 1. Today's Overview

PicoClaw shows a **quiet but productive** development period. Over the last 24 hours, **no new issues** were opened or updated, and **no new releases** were cut, indicating a stable maintenance phase. However, **two pull requests** saw activity: one was closed and one remains open, both receiving updates as of August 6th. The project's momentum is carried by **long-running PRs**, particularly #3200 which has been in review for over a month, suggesting that major feature integrations are pending maintainer review rather than being blocked by bugs. Overall, the project appears **healthy with low bug pressure**, but attention is needed to shepherd the active PRs to completion.

---

## 2. Releases

**None.** No new versions, tags, or releases were published in the last 24 hours. The last known release remains the previous stable build. No migration notes or breaking change warnings are applicable at this time.

---

## 3. Project Progress

| PR | Status | Summary |
|----|--------|---------|
| [#1349](https://github.com/sipeed/picoclaw/pull/1349) | **Merged/Closed** | **QQ Channel Multi-Attachment Support:** Adds parsing and replying to emoji structures, incoming voice/image/video/file messages, and outbound attachment uploads. Also introduces a Markdown-first reply strategy with fallback. **Impact:** Significantly improves QQ channel interoperability for media-rich conversations. |
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) | **Open (Active)** | **Configurable Default Fallback Chain:** Introduces a web UI workflow and backend API persistence for setting a default model, adding fallback models, and reordering the chain. **Impact:** Enables users to define resilient multi-model routing for the assistant. |

**Progress Assessment:** The closure of #1349 represents a **functional gain** for the QQ channel domain — a key integration point for PicoClaw. PR #3200 remains open but updated, indicating active collaboration. No bug-fix PRs were merged today, suggesting that stability issues are not the current bottleneck.

---

## 4. Community Hot Topics

**No issues saw activity in the last 24 hours**, and neither active PR currently displays a high comment/reaction count (both at 0 👍). The most significant ongoing discussion threads are thus the two open PRs themselves:

- **[PR #3200 – Configurable Fallback Chain](https://github.com/sipeed/picoclaw/pull/3200):** This is the longest-running active proposal (open since July 1). The underlying need is **operational resilience** — users want to avoid hard failures when a preferred model API fails or is rate-limited. The desire for reordering also hints at a **cost/quality trade-off preference** (e.g., default to cheap model, fall back to premium).
- **[PR #1349 – QQ Channel Enhancements](https://github.com/sipeed/picoclaw/pull/1349):** Though closed, its long lifespan (March → August) indicates it was a **high-demand feature** for the QQ community. The "Markdown-first, fallback to plain text" approach signals that **rendering reliability** is a persistent pain point in channel integrations.

---

## 5. Bugs & Stability

**No bugs, crashes, or regressions were reported in the last 24 hours.** No open issues exist in the repository's active queue. 

**Risk Assessment:** The absence of reported bugs is a positive signal, but it may also reflect reduced user testing volume during a quiet period. The pending merge of #3200 (fallback chains) is a proactive mitigation against future API-related outages, which are the most likely source of future "bugs" from a user's perspective (i.e., model unreachable errors).

---

## 6. Feature Requests & Roadmap Signals

**Direct user feature requests:** None filed today.

**Signals from active PRs:**
- **Multi-Model Redundancy (PR #3200):** The configurable fallback chain is a strong candidate for the **next minor release** once merged. It's a non-breaking, additive feature that improves reliability without changing core behavior.
- **Rich Media in Channels (PR #1349):** Now merged, this sets the stage for follow-up requests in **other channel adapters** (Discord, Telegram, etc.) to match QQ's capabilities — expect user requests for "voice replies" or "file attachments" in other domains.
- **Config Persistence:** The backend API persistence introduced in #3200 may pave the way for **export/import configuration** features in future versions.

**Prediction:** The next release will likely include the fallback chain feature (#3200) and a changelog highlighting the QQ media support from #1349.

---

## 7. User Feedback Summary

- **Satisfaction Signals:** The closure of #1349 should positively impact QQ Channel users who previously lacked rich media support. The PR's long development cycle suggests thorough testing was valued.
- **Pain Points / User Needs:** 
  - **Reliability anxiety:** The existence and active development of fallback chains (#3200) indicates that users are experiencing or fearing model API failures. The desire to "save the full chain" implies they want a persistent, predictable setup rather than a temporary fix.
  - **Channel parity:** QQ users were clearly missing voice/video/file capabilities — a core gap compared to direct API usage. The wait from March to August for this feature highlights **delivery latency** as a broader concern for community features.
- **No explicit dissatisfaction** was recorded in the last 24 hours (no negative comments or reactions on active items).

---

## 8. Backlog Watch

**Items needing attention:**

| Item | Age | Concern |
|------|-----|---------|
| [PR #3200](https://github.com/sipeed/picoclaw/pull/3200) – Configurable Fallback Chain | Open since **2026-07-01** (37 days) | This is the longest-open active PR. It has been updated recently (Aug 6), indicating progress, but a **37-day review cycle** for a core UX feature is a risk. If it stalls, users may fork or patch locally, fragmenting the community. **Action:** Recommend maintainers schedule a final review or provide a status update. |

**Other notes:** No long-unanswered issues exist in the backlog (0 open issues total). The project's issue queue is effectively empty, which is healthy but also means there is **no public signal of user friction** for new users to reference. Maintainers might consider proactively soliciting feedback to gauge post-merge sentiment on #1349.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-07

## 1. Today's Overview
Activity is focused and substantive this week. 14 PRs were touched in the last 24 hours, with 8 merging or closing — the largest batch of completed work in recent weeks. The project is mid-cleanup: a stale skills removal landed, and a significant transactional-upgrade fix is in review. Two new issues surfaced around the same upgrade pathway, signaling that reliability of the self-update mechanism is the current hot spot. Overall, the project feels healthy and responsive, with a steady mix of community fixes and core-team architectural work.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
The bulk of merged work landed from the backlog (dates are creation dates; all merged/closed recently):

- **fix: accept media-only messages (photo/video/file without caption)** ([#2213](https://github.com/nanocoai/nanoclaw/pull/2213)) by ziv-daniel — Fixes a silent drop in the Chat SDK bridge when media arrives without caption text. This is a user-facing reliability win for Telegram and other channels.
- **fix(scheduling): re-arm recurrence when a run fails permanently** ([#2678](https://github.com/nanocoai/nanoclaw/pull/2678)) and **fix(scheduling): surface permanently-failed scheduled tasks to the user** ([#2679](https://github.com/nanocoai/nanoclaw/pull/2679)) by yairixStudio — Two complementary fixes making scheduled tasks more resilient and observable.
- **fix: detect reply-to-bot in Telegram extractReplyContext** ([#2644](https://github.com/nanocoai/nanoclaw/pull/2644)) and **fix: engage pattern/mention wirings on direct address** ([#2643](https://github.com/nanocoai/nanoclaw/pull/2643)) by yairixStudio — Router and Telegram-context fixes ensuring the bot responds to direct mentions and replies reliably.
- **fix: namespace user IDs by channel-type prefix, not bare colon** ([#2591](https://github.com/nanocoai/nanoclaw/pull/2591)) by mmahmed — ID collision fix across channels.
- **chore(skills): remove stale qodo and Google MCP skills** ([#3172](https://github.com/nanocoai/nanoclaw/pull/3172)) by glifocat — Removes broken/integration-less skills (the counterpart to the closed issue below).
- **fix(skills): split pre-flight from credentials so /update-skills can refresh code** ([#2873](https://github.com/nanocoai/nanoclaw/pull/2873)) by glifocat — Unblocks skill updates for users without certain credentials.

This batch shows the project hardening messaging (media, mentions), scheduling reliability, and skill-management plumbing.

## 4. Community Hot Topics
The most active threads (no comments recorded in the data, but these carry clear user-signal):

- **Issue #3194 — `/update-nanoclaw` can stamp success without a recoverable cutover** ([open](https://github.com/nanocoai/nanoclaw/issues/3194)) by glifocat — Opens a critical reliability window around self-updates. Community members relying on `/update-nanoclaw` should watch this.
- **Issue #3171 — Two qodo skills depend on an integration nothing sets up** ([closed](https://github.com/nanocoai/nanoclaw/issues/3171)) by glifocat — Flagged a broken bundled-skill experience; resolved by the removal PR above.
- **PR #3195 — fix(update): make NanoClaw upgrades transactional** ([open](https://github.com/nanocoai/nanoclaw/pull/3195)) by glifocat — The proposed fix for #3194; the most consequential PR currently in flight.
- **PR #3186 — refactor: add host seams for skill-owned capabilities** ([open](https://github.com/nanocoai/nanoclaw/pull/3186)) by zvi-fried — Architectural refactor that could enable more skill flexibility; worth community eyes.

Underlying need: users increasingly treat NanoClaw as long-running infrastructure, so upgrade safety and skill hygiene are the dominant recurring themes.

## 5. Bugs & Stability
Ranked by severity:

- **URGENT: `/update-nanoclaw` success stamp without recoverable cutover** ([#3194](https://github.com/nanocoai/nanoclaw/issues/3194)) — Can leave the install in a broken state with incomplete rollback. Fix PR exists ([#3195](https://github.com/nanocoai/nanoclaw/pull/3195)).
- **MODERATE: Media-only messages silently dropped** ([#2213](https://github.com/nanocoai/nanoclaw/pull/2213)) — Fix merged.
- **MODERATE: Scheduled tasks failing permanently left users uninformed** ([#2679](https://github.com/nanocoai/nanoclaw/pull/2679)) — Fix merged.
- **MODERATE: Reply-to-bot and keyword-mention wirings not firing on direct address** ([#2643](https://github.com/nanocoai/nanoclaw/pull/2643), [#2644](https://github.com/nanocoai/nanoclaw/pull/2644)) — Fixes merged.
- **LOW: User-ID collision across channels** ([#2591](https://github.com/nanocoai/nanoclaw/pull/2591)) — Fix merged.

All reported bugs this cycle have fix PRs, and most are already merged — a strong stability signal.

## 6. Feature Requests & Roadmap Signals
- **Transactional, validation-gated updates** ([#3195](https://github.com/nanocoai/nanoclaw/pull/3195)) — Not a user request per se, but a core reliability feature likely to land in the next minor release.
- **Media-rich messaging (photo/video/file without caption)** — addressed and merged; expect it in the next release.
- **Skill-owned capability seams** ([#3186](https://github.com/nanocoai/nanoclaw/pull/3186)) — Open refactor; if merged, expect third-party skill capabilities to expand (e.g., Tavily MCP tool skill in [#3190](https://github.com/nanocoai/nanoclaw/pull/3190) is an early signal of community appetite for richer skill integrations).
- **Tavily MCP tool skill** ([#3190](https://github.com/nanocoai/nanoclaw/pull/3190)) — New utility skill from the community, quick to merge if guidelines pass.

## 7. User Feedback Summary
- **Pain point (critical):** Self-update can brick or corrupt an install, and success is reported prematurely ([#3194](https://github.com/nanocoai/nanoclaw/issues/3194)). Expect this to drive the next patch.
- **Pain point (resolved):** Media messages without captions never reached the agent ([#2213](https://github.com/nanocoai/nanoclaw/pull/2213)) — a silent, confusing failure.
- **Pain point (addressed):** Bundled skills that reference unconfigured SaaS accounts — the qodo experience ([#3171](https://github.com/nanocoai/nanoclaw/issues/3171)) — was confusing out-of-box; the removal is a UX cleanup.
- **Observed pattern:** Users with launchd/systemd installs are hitting gateway and upgrade issues (see [#2705](https://github.com/nanocoai/nanoclaw/pull/2705) — still open after 2 months), which may warrant a dedicated install-reliability track.

## 8. Backlog Watch
- **PR #2705 — fix(use-native-credential-proxy): actually bypass the OneCLI gateway** ([open since June 7](https://github.com/nanocoai/nanoclaw/pull/2705)) by premald — Open ~60 days; addresses real launchd/systemd install failures. Needs maintainer review or explicit closure reasoning.
- **PR #3149 — fix(cli): add --rw flag to groups config add-mount** ([open since July 29](https://github.com/nanocoai/nanoclaw/pull/3149)) by winjer — Awaiting review ~9 days; small, well-scoped CLI fix.
- **PR #3186 — refactor: add host seams for skill-owned capabilities** ([open, core-team discussions likely](https://github.com/nanocoai/nanoclaw/pull/3186)) — Architecturally significant; needs careful review.
- **PR #3193 — fix(telegram): update Chat SDK for rich messages** ([open](https://github.com/nanocoai/nanoclaw/pull/3193)) — New; related to the media-message fix already merged; should be prioritized to avoid divergence.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-07

## Today's Overview

IronClaw shows strong development momentum with 50 issues and 50 PRs updated in the last 24 hours, alongside a new stable release (v1.1.0). The project is transitioning from stabilization mode into a feature-acceleration phase, with the new Inspector feature (operator diagnostics) being the dominant theme across the latest PRs. However, a large backlog of QA-reported bug-bash issues (P1/P2 severity) persists, particularly around routines, Slack delivery, and run failures, indicating quality gaps in core workflows. Docs and sandbox hardening are active focus areas, with multiple PRs targeting CI gates, dependency security bumps (js-yaml, fast-uri), and Docker healthcheck fixes. Overall, the project is healthy but carries a significant QA debt that needs one more dedicated push.

---

## Releases

**ironclaw-v1.1.0** (2026-08-06) — First stable release since 1.0.0, promoting 1.1.0-rc.1 plus fixes listed under "Fixed since 1.1.0-rc.1." Headline features per the release notes:

- Registering **arbitrary hosted MCP servers** (extension reach)
- Installing from **IronHub deep links**
- **Durable file attachments** that cross channels
- **Slack** delivery improvements (the note is truncated: "and Slac...")

No breaking changes or migration notes were included in the snippet. This packaging of Slack/MCP/attachment work signals the 1.1 series is focused on integrations and delivery channels.

---

## Project Progress

Merged/closed PRs in the last 24h (17 total):

- **[#7289 — fix(memory): sanitize FTS queries for natural-language recall on libSQL](https://github.com/nearai/ironclaw/pull/7289)** *(closed)* — Closes #7275; caller-level verification of persistent-memory recall on the production embedded-libSQL path.
- **[#7303 — fix(docker): install curl for orchestrator healthchecks](https://github.com/nearai/ironclaw/pull/7303)** *(closed)* — Fixes staging nodes stuck in `error` status despite healthy server (missing `curl` in image).
- **[#7259 — docs: enforce docs publication boundary + consolidate internal docs](https://github.com/nearai/ironclaw/pull/7259)** *(closed)* — Fixes a live leak: `docs/design/` and `docs/research/` were reachable as hidden pages on the public Mintlify site. Frozen `.mintignore` + CI gate.
- **[#7235 — feat(inspector): operator inspection API + live updates](https://github.com/nearai/ironclaw/pull/7235)** *(closed)* — Operator-only endpoints for run snapshots, prompt diagnostics, tool activity; live stream with cursor resume/dedup.

Feature work advancing (**open but active**): Inspector continues with **model call statistics** ([#7277](https://github.com/nearai/ironclaw/pull/7277)) and **prompt inspection tab** ([#7239](https://github.com/nearai/ironclaw/pull/7239)). The **two-lane channel delivery tool** ([#7157](https://github.com/nearai/ironclaw/pull/7157)) is the biggest architectural PR open, moving all delivery logic into an explicit tool. **Nostr host functions** ([#7184](https://github.com/nearai/ironclaw/pull/7184)) add sign-event capabilities to WASM tools.

---

## Community Hot Topics

**Highest-discussion Issues (by comment count):**

- **[#5553 — Approval notifications disappear instead of remaining in history](https://github.com/nearai/ironclaw/issues/5553)** *(4 comments, open)* — Notification reliability for approval flows; a UX-critical trust issue.
- **[#5702 — GitHub issue search/create fails with HTTP 403](https://github.com/nearai/ironclaw/issues/5702)** *(4 comments, open)* — Agent's GitHub integration is broken for issue ops; a key marketing demo path.
- **[#5522 — Reborn routine fails when task requires reading Slack DMs (capability_info retry loop)](https://github.com/nearai/ironclaw/issues/5522)** *(3 comments, open)* — Missing Slack read capability causes `capability_info` retry loop → total routine failure.
- **[#5701 — Activity panel hides tool details and doesn't update live](https://github.com/nearai/ironclaw/issues/5701)** *(3 comments, open)* — Users can't see what tools are running during a run; only a summary "Activity - N tools" after.

**Underlying need pattern:** The top issues are *not* exotic systems bugs — they are **visibility and feedback failures**. Users want transparency: which tool is running, which capability is missing, whether a notification landed. The Inspector work (PRs #7235/#7236/#7239/#7277) appears to be the direct architectural response to this class of complaints, exposing the internals that the chat UI currently hides.

---

## Bugs & Stability

Ranked by severity (most impactful first):

**P1:**
- **[#5456 — Routine runs fail with runner lease expiration](https://github.com/nearai/ironclaw/issues/5456)** *(open)* — 90s inactivity threshold too aggressive for multi-tool runs; dominant failure pattern in 6/30 testing. Affects email + multi-API workflows. No fix PR yet.
- **[#5877 — Slack notification delivered to wrong user](https://github.com/nearai/ironclaw/issues/5877)** *(closed)* — Sensitive data sent to unrelated user. Notably closed today — with [PR #7300 "restore personal delivery + fail closed"](https://github.com/nearai/ironclaw/pull/7300) addressing exactly this ("fail closed when a stored DM target names a different workspace").
- **[#3533 — Telegram does not auto-setup from UI (v0.28.1)](https://github.com/nearai/ironclaw/issues/3533)** *(closed)* — Old but important; direction text out of sync with actual flow.

**P2 (significant):**
- **[#5702 — GitHub 403 on issue search/create](https://github.com/nearai/ironclaw/issues/5702)** — Integration configured but agent can't interact. No fix PR yet.
- **[#5836 — Routine fails every 5 min with "No thread attached"](https://github.com/nearai/ironclaw/issues/5836)** — Systemic scheduled-run attach failure; 0% success rate.
- **[#5553 — Approval notifications vanish from history](https://github.com/nearai/ironclaw/issues/5553)** — Trust-breaking; no fix PR yet.
- **[#5776 — Long-output prompts cause repeated timeouts → generic "invalid result"](https://github.com/nearai/ironclaw/issues/5776)** — Real model timeout hidden by generic error; error-masking problem.
- **[#5522 — Slack DM read missing capability → retry loop](https://github.com/nearai/ironclaw/issues/5522)** — Routine + Slack + retry storm.
- **[#5508 — "No Slack delivery targets" despite active connection](https://github.com/nearai/ironclaw/issues/5508)** — Old routines post fine, new ones fail; state sync bug. Likely addressed by [#7300](https://github.com/nearai/ironclaw/pull/7300) (Slack delivery fix PR, open).
- **[#5707 — Routine creation response exposes internal details](https://github.com/nearai/ironclaw/issues/5707)** — Cron syntax + internal commands shown to users. UX hygiene.

**Memory/FTS (two related):** [#5838](https://github.com/nearai/ironclaw/issues/5838) (context compaction error despite successful tool runs) closed; [#7275](https://github.com/nearai/ironclaw/issues/7275) production FTS defect addressed by closed [#7289](https://github.com/nearai/ironclaw/pull/7289) — good sign of follow-through.

---

## Feature Requests & Roadmap Signals

1. **Inspector / observability tooling** (PRs #7235, #7236, #7239, #7277) — The clearest roadmap signal. The project is building a **first-class diagnostics surface** (prompt inspection, tool detail, model stats, live stream). Expect this to land in 1.2 or 1.3 as a WebUI tab (opt-in via `?debug=true`).

2. **Explicit channel delivery tool** ([#7157](https://github.com/nearai/ironclaw/pull/7157), open, XL) — A two-lane model (conversation lifecycle + user-visible notification). This **replaces the heuristic delivery logic** with an explicit tool the agent chooses. If merged, it would fix a large class of Slack-wrong-target issues (#5877, #5508, #5834) by making delivery a first-class tool call.

3. **Nostr host functions** ([#7184](https://github.com/nearai/ironclaw/pull/7184), open) — WASM tools gaining `nostr-sign-event` capability. Signals platform ambitions toward pub/sub networks beyond Slack/Telegram.

4. **Explicit Docker/Railway sandbox profiles** ([#7214](https://github.com/nearai/ironclaw/pull/7214), open, XL) — Tenant/user-scoped workspaces, fresh non-root workers. Security-hardening direction for the sandbox.

5. **Custom MCP registration made definition-only** ([#7253](https://github.com/nearai/ironclaw/pull/7253), open) — Registration creates no installation/activation; just catalog. Cleaner separation for "extension reach."

---

## User Feedback Summary

**Pain points (recurring themes from QA/user reports):**

- **"I can't tell what went wrong."** — Generic errors ("invalid result", "No thread attached", collapsed activity summaries) hide the actual failing tool. Users repeatedly ask for per-tool transparency. The failed-tool summary being painted red ([#7302](https://github.com/nearai/ironclaw/issues/7302), fixed by PR [#7305](https://github.com/nearai/ironclaw/pull/7305)) is a UI-level acknowledgment of this; the Inspector is the architectural one.
- **"Integration setup is confusing."** — Telegram auto-setup is broken/misdirected (#3533), Slack says "not configured" when it is (#5508), GitHub gives 403s (#5702). Setup flows feel untested.
- **"Routines are fragile."** — Lease timeouts (#5456), stuck threads (#5836), disappearing notifications (#5553), no delete mechanism (#5510). The routine feature is powerful but not yet reliable enough.
- **"Latency grows with history."** — Chat creation slows as conversations accumulate (#5509); deleting history restores speed. Frontend issue.

**Satisfaction signals:** The closed/merged ratio (17) and release cadence (1.1.0 today) suggest the maintainers are responsive; the docs-boundary fix (#7259) shows attention to *internal* hygiene; the memory FTS fix (#7289) was closed the same day the issue was reported — an exemplary turnaround.

---

## Backlog Watch

Issues needing maintainer attention (old, some with no fix PR):

- **[#4340–#4344 — Qwen3.6-35B & MiniMax-M2.7 QA issues (6 open, all P2)](https://github.com/nearai/ironclaw/issues/4340)** — Dated 2026-06-02, last updated 2026-08-07, but *zero comments*. The agent mirrors user messages (#4344), exposes thinking chains (#4341), rejects valid tool invocations (#4339), blank-field validation errors (#4340), MCP driver failures (#4343), auth modal persistence (#4342). Five weeks old, untouched, but still open. These should be triaged: are they model-specific or systemic?
- **[#5509 — Chat creation latency scales with history](https://github.com/nearai/ironclaw/issues/5509)** *(open, P2, 1 comment)* — A UX-relevant perf issue on the frontend; no PR owner visible.
- **[#5510 — Cannot delete old routines](https://github.com/nearai/ironclaw/issues/5510)** *(open, P3, 1 comment)* — No delete mechanism exists at all; users need "complete restart."
- **[#5507 — Failed run shows "No thread attached" and blocks debugging](https://github.com/nearai/ironclaw/issues/5507)** *(closed, but worth verifying the fix path)* — The "Open run" button disabled is a debugging dead-end; the closed status may indicate a fix, but the related #5836 remains open — suggesting the underlying attach mechanism is still fragile.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-07

## 1. Today's Overview

Activity remains steady but modest. A total of 5 issues and 2 pull requests received updates in the last 24 hours, with no new releases and no merge activity. Notably, three of these items (#1196, #1198, and both PRs #1197/#1199) are marked as stale, having been open for over four months with no maintainer response — a signal of potential backlog neglect. However, the three newest issues (#2442, #2443, #2444) were filed within the last 48 hours, covering a mix of bug reports and UX feature requests, indicating that user engagement is ongoing and the community continues to actively test and provide feedback.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

No pull requests were merged or closed in this period. Two PRs remain open:

- **[PR #1197](https://github.com/netease-youdao/LobsterAI/pull/1197) — Agent 管理页面交互优化** (stale, open since 2026-04-01): Improves the Agent management page by adding delete actions directly in the sidebar list, reducing the interaction depth required for management tasks. Originally submitted as PR #1176, it was reopened with conflict resolution.
- **[PR #1199](https://github.com/netease-youdao/LobsterAI/pull/1199) — feat(model): add context window and token settings** (stale, open since 2026-04-01): Adds per-model `contextWindow` and `maxTokens` settings, persists them, and propagates context metadata into Cowork/OpenClaw configurations — a substantive feature with cross-module impact.

The lack of any merge activity over the past four months for these two PRs highlights a bottleneck in the review/merge pipeline.

## 4. Community Hot Topics

The most discussed items in the last 24 hours are the three stale threads from April:

- **[Issue #1196](https://github.com/netease-youdao/LobsterAI/issues/1196) — 不要强制在工作目录中建立 Agents.md、User.md等6个文件** (1 comment): Users are frustrated that the app forces creation of six system files (AGENTS.md, USER.md, etc.) in every working directory. Users suggest either a global/centralized `agents.md` (à la CC) or storing them in a hidden directory. The underlying need: **cleaner workspace management and reusable global system prompts**.

- **[Issue #1198](https://github.com/netease-youdao/LobsterAI/issues/1198) — 网关重启到一半进度条消失，也不知道重启状态** (1 comment): A gateway restart loses its progress indicator midway, and all subsequent conversations report "model unavailable." User reports browser/Chrome opens fine but the app still says browser service unavailable. The underlying need: **better restart-state visibility and graceful recovery paths**.

- **[Issue #2442](https://github.com/netease-youdao/LobsterAI/issues/2442) — 为什么LobsterAI软件的内核还是 ps5.1 始终没有升级到 ps7.4**: A user asks why the shell wrapper is still PowerShell 5.1 instead of 7.4. The author proactively answers their own question with analysis (Node.js defaults to `powershell.exe`, compatibility fallback). The underlying need: **transparency about runtime choices and documentation of system dependencies**.

These threads demonstrate persistent community curiosity about architectural decisions and a strong desire for configuration flexibility.

## 5. Bugs & Stability

Two bugs reported in the last 48 hours, ranked by severity:

1. **[Issue #2443](https://github.com/netease-youdao/LobsterAI/issues/2443) — 模型 ID 含斜杠的自定义 Provider 无法在界面中使用** (Medium): Model IDs containing slashes (e.g., `deepseek-ai/DeepSeek-V4-Flash` from SiliconFlow) cannot be selected in the UI for custom OpenAI-compatible providers. The model works functionally but the dropdown fails to display it. Affects all OpenAI-compatible services using slash-prefixed model IDs. No fix PR exists yet.

2. **[Issue #1198](https://github.com/netease-youdao/LobsterAI/issues/1198) — Gateway restart progress bar vanishes** (Medium, stale): Restart progress disappears halfway, and the UI incorrectly reports "browser service unavailable" despite Chrome actually being open. Misleading error states degrade trust in the system. No fix PR exists.

Both bugs block core workflow (model selection and service restart) and should be prioritized — especially #2443, which affects a large ecosystem of OpenAI-compatible providers.

## 6. Feature Requests & Roadmap Signals

- **[Issue #2444](https://github.com/netease-youdao/LobsterAI/issues/2444) — 输入框编辑模式** (filed today): A well-formed UX proposal requesting an "edit mode" for the prompt input box. The user identifies a real pain point (accidental send on Enter when intending newline) and offers two concrete solutions: (a) a settings toggle for Enter vs. Ctrl+Enter, or (b) an adjacent toggle button that expands the input into a taller WYSIWYG-capable edit mode. This is likely to be picked up for a future UX-focused release given its clarity and low implementation cost.

- **PR #1199 (context window and token settings)**: Although stale, this feature is highly aligned with power-user needs around model-specific configuration. If merged, it would surface per-model token settings in the UI and propagate them into Cowork/OpenClaw configurations — a valuable roadmap signal for advanced model management.

- **Issue #1196 (global/system-level agents.md)**: The request for a centralized system prompt file reflects a common pattern in AI-assisted coding tools (e.g., CC). Implementing this would reduce configuration overhead and improve multi-project workflows; likely to appear in a configuration/refactor release.

**Prediction for next version**: The edit-mode input toggle (issue #2444) and possibly the context-window settings (PR #1199, if merged) are the most likely candidates. The slash-in-modelID fix (#2443) is an urgent correction that may ship ahead of schedule.

## 7. User Feedback Summary

Real pain points expressed by users over the last 24 hours:

- **Workspace pollution** (#1196): Forced creation of six config files per working directory is perceived as "messy" and disruptive; users want global or hidden alternatives.
- **Restart transparency** (#1198): Lack of visible progress during gateway restarts, and misleading "unavailable" messages, undermine confidence in the tool.
- **Input ergonomics** (#2444): Accidental message sends due to Enter-to-send while wanting newlines is a friction point serious enough to warrant a dedicated edit-mode toggle.
- **Compatibility gaps** (#2443): Models with slashes in their IDs (common in SiliconFlow and similar providers) are effectively unusable in the UI, limiting provider choice.
- **Runtime curiosity** (#2442): Users are deeply technical and want clarity on why specific shells or runtimes are chosen; they appreciate self-documented explanations but would benefit from official documentation or settings.

Overall sentiment skews **functional but frustrated**  — the tool works, but small UX gaps and unaddressed stale feedback are accumulating.

## 8. Backlog Watch

The following items have been open for over four months without maintainer response and need attention:

- **[Issue #1196](https://github.com/netease-youdao/LobsterAI/issues/1196)** (open 2026-04-01): Forced config file creation in working directory.
- **[Issue #1198](https://github.com/netease-youdao/LobsterAI/issues/1198)** (open 2026-04-01): Broken gateway restart progress indicator.
- **[PR #1197](https://github.com/netease-youdao/LobsterAI/pull/1197)** (open 2026-04-01): Agent management page interaction improvements — code complete but unmerged.
- **[PR #1199](https://github.com/netease-youdao/LobsterAI/pull/1199)** (open 2026-04-01): Context window and token settings feature — code complete but unmerged.

These four items form a coherent "Q2 cleanup" bundle: two UX/design improvements, one critical bug, and one feature. A maintainer pass to triage, merge, or close these would significantly improve the project's health signal.

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

# CoPaw Project Digest
**Date:** 2026-08-07
**Repository:** [agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw)

---

## 1. Today's Overview

CoPaw is experiencing a period of **high development velocity** and significant community engagement. With **50 pull requests** and **34 issues** updated in the last 24 hours, the project is clearly in an active refinement phase, likely a pre-release stabilization period for v2.1.0. The high close rate (17 closed issues, 30 merged/closed PRs) indicates responsive maintainers. However, the concurrent emergence of multiple bugs in **tool-call handling**, **model provider compatibility**, and **session/memory management** suggests that the recent 2.0.x release line introduced a set of regressions that the community is actively testing and reporting. Notably, the forum activity reveals a strong Chinese-speaking user base reporting issues directly, while English speakers are also contributing significantly to bug discovery.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The latest available versions remain v2.0.1 stable and v2.1.0 beta.

---

## 3. Project Progress

The recent pull request activity shows focused effort on infrastructure hardening and feature development. Key merged/closed PRs include:

- [**PR #6530 (CLOSED)**](https://github.com/agentscope-ai/QwenPaw/pull/6530) — **Fix editable per-tool call limit names**: Allows renaming per-tool call limits and adds regression tests, improving UI usability.
- [**PR #6744 (CLOSED)**](https://github.com/agentscope-ai/QwenPaw/pull/6744) — **Harden agent config persistence on shared filesystems**: Switches to atomic write patterns for agent.json and access_control.json, addressing data corruption risks on OSSFS/FUSE mounts.
- [**PR #6611 (CLOSED)**](https://github.com/agentscope-ai/QwenPaw/pull/6611) — **Align Scroll and memory with AgentScope lifecycle**: Major refactor converging on Scroll as the unique context protocol, resolving duplication between Native/Scroll strategy branches.
- [**PR #6664 (CLOSED)**](https://github.com/agentscope-ai/QwenPaw/pull/6664) — **Graceful degradation without Codex CLI**: Fixes harness compatibility for environments that don't have the Codex CLI installed.

Actively reviewed PRs include a **model fallback with cooldown mechanism** ([PR #6659](https://github.com/agentscope-ai/QwenPaw/pull/6659)), which directly addresses rate-limits and timeout issues — a top community pain point.

---

## 4. Community Hot Topics

The most active discussions this week highlight on-the-ground reliability issues:

- **[#6684 — Feature: 增加频道的重试功能 (Channel Retry Feature)](https://github.com/agentscope-ai/QwenPaw/issues/6684)** (8 comments, CLOSED) — A user reports that the QwenPaw Matrix integration fails silently during startup races with the Matrix server. The request for automatic health checks/retries on channel reconnection is a general need for **production stability of chat channel integrations**.

- **[#6588 — Bug: `spawn_subagent` treats empty `batch` placeholders as batch mode](https://github.com/agentscope-ai/QwenPaw/issues/6588)** (6 comments, CLOSED) — A subtle API compatibility bug where an unset placeholder is interpreted as a true value. This reveals a deeper concern about **strict type validation and API contract consistency**.

- **[#6601 — Bug: QwenPaw doesn't report empty-response errors](https://github.com/agentscope-ai/QwenPaw/issues/6601)** (5 comments, OPEN) — In long-running sessions, models returning empty responses cause silent session freezes. Users demand **session health diagnostics and recovery** mechanisms.

- **[#6667 — DeepSeek thinking mode fails in multi-turn: reasoning_content missing](https://github.com/agentscope-ai/QwenPaw/issues/6667)** (5 comments, CLOSED) — A complex integration issue between DeepSeek's reasoning tokens, the OpenAI formatter, and session history. This is symbolic of the broader problem of **maintaining compatibility with heterogeneous model providers**.

- **[#6732 — Bug: MCP tools regularly stop working until restart](https://github.com/agentscope-ai/QwenPaw/issues/6732)** (3 comments, OPEN) — Users report MCP tools becoming stale and unresponsive after hours of operation, requiring a Docker container restart. This suggests a **resource leak or connection-lifetime issue** in the MCP client implementation.

---

## 5. Bugs & Stability

This week's bug reports are of significant concern, spanning several critical subsystems.

- **Critical/High:**
    - **Session freezes and silent failures** — A cluster of issues point to agent sessions becoming unresponsive ([#6601](https://github.com/agentscope-ai/QwenPaw/issues/6601), [#6768](https://github.com/agentscope-ai/QwenPaw/issues/6768)). **Issue #6768** describes a multi-step task where the agent was blocked for *hours*. Related root causes include **tool output overwhelm** ([#6700](https://github.com/agentscope-ai/QwenPaw/issues/6700)) where multi-MB outputs crash the UI and context window.
    - **API Contract Violations** — Extensive reports show failures when reasoning tokens are mixed with tool calls ([#6667](https://github.com/agentscope-ai/QwenPaw/issues/6667), [#6707](https://github.com/agentscope-ai/QwenPaw/issues/6707)) and when tool usage volumes exceed thresholds ([#6726](https://github.com/agentscope-ai/QwenPaw/issues/6726)).
    - **Dependency/Runtime Conflicts** — **Issue #6612** documents a crash-loop and permission deadlock when using QwenPaw with the latest `agentscope` version, highlighting a **coupled-dependency update problem**.

- **Medium:**
    - **MCP tool degradation** — Regular failure of MCP tools until restart ([#6732](https://github.com/agentscope-ai/QwenPaw/issues/6732)).
    - **Browser SDK failures** — `open()` crashes under an isolated Playwright session ([#6698](https://github.com/agentscope-ai/QwenPaw/issues/6698)).
    - **Zero-token SSE stream errors** — Upstream errors interpreted as fatal in ([#6708](https://github.com/agentscope-ai/QwenPaw/issues/6708)).

- **Secured:**
    - **Windows Antivirus False Positive** — **Issue #6775** reports a Malwarebytes "Trojan Loader" detection that is likely a false positive but creates a hard trust barrier for prospective Windows enterprise users. This deserves an immediate security audit and public communication.

---

## 6. Feature Requests & Roadmap Signals

The community is unanimous on prioritizing robust and resilient production behavior:

- **Reliability & Resilience:**
    - **Channel Reconnection and Retry** ([#6684](https://github.com/agentscope-ai/QwenPaw/issues/6684)) — A retry mechanism for self-hosted channels is essential for unattended operations.
    - **Configurable MCP Timeouts** ([#6724](https://github.com/agentscope-ai/QwenPaw/issues/6724)) — Preventing stalled turns is a definite **next-release candidate**.
    - **Model Fallback with Cooldown** ([PR #6659](https://github.com/agentscope-ai/QwenPaw/pull/6659)) — This addresses a top-trending pain point and is likely to land soon.

- **Performance & Scalability:**
    - **Output Truncation and Pagination** ([#6700](https://github.com/agentscope-ai/QwenPaw/issues/6700)) — Handling large tool outputs without catastrophic UI failures is critical for complex automation workflows.

- **User Experience:**
    - **UX Overhaul for Session Titles** ([#6736](https://github.com/agentscope-ai/QwenPaw/issues/6736), [#6737](https://github.com/agentscope-ai/QwenPaw/issues/6737)) — Users are dissatisfied with AI-generated conversation titles.
    - **Removal of "Multimodal capability" prompt** ([#6452](https://github.com/agentscope-ai/QwenPaw/issues/6452)).
    - **Internationalization** — Requests for Hungarian ([#6765](https://github.com/agentscope-ai/QwenPaw/issues/6765)) and Chinese approval buttons in WeChat ([#6728](https://github.com/agentscope-ai/QwenPaw/issues/6728)) show a widening global user base.

---

## 7. User Feedback Summary

Users demonstrate a strong desire for CoPaw as a powerful automation tool but are nevertheless frustrated by its **reliability gaps in long-running scenarios**. Key sentiments included:

- "I love your work. Thanks for all you do. Brendan" — **Issue #6775** — Illustrates the high overall satisfaction with the product, even when filing a serious bug.

- "Long conversation sessions with heavy tool usage... 400 'Messages with role tool must be a response..." — **Issue #6726** — A deep technical understanding of protocol violations indicates a technically sophisticated user base expecting framework-level corrections.

- "The agent was completely unresponsive for several hours... the user's messages were received but never processed." — **Issue #6768** — A major source of user distrust that needs immediate remediation.

- "Despite being feature-rich, the platform's stability makes me hesitant to rely on it for critical business operations." — Representative of the perception surrounding **MCP recurring failures** ([#6732](https://github.com/agentscope-ai/QwenPaw/issues/6732)).

- **Trust and Security Concerns:** The malware false-positive report ([#6775](https://github.com/agentscope-ai/QwenPaw/issues/6775)) demonstrates a delicate trust relationship within the community that must be handled with transparency.

---

## 8. Backlog Watch

The following issues require urgent attention from maintainers due to long wait times, high impact, or broad applicability:

- **[#6612 — Incompatibility with agentscope 2.0.4.post1](https://github.com/agentscope-ai/QwenPaw/issues/6612)** — This is an **active blocker for a large segment of the user base**. Since `agentscope` is a core dependency, their latest release breaking QwenPaw calls for an urgent patch or (ideally) a fix for the underlying dependency management.

- **[#6684 — Matrix channel retry/health check](https://github.com/agentscope-ai/QwenPaw/issues/6684)** — The lack of a retry/reconnection mechanism for user-maintained channels is a production reliability concern that undermines self-hosting capabilities.

- **[#6732 — MCP tools reliably failing](https://github.com/agentscope-ai/QwenPaw/issues/6732)** — A recurring daily issue for some users, with no actionable workaround beyond a restart. This severely limits usability in automated contexts.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-07

## 1. Today's Overview

ZeroClaw is in an active stabilization and hardening phase, with 31 issues and 50 PRs updated in the last 24 hours. The project shows a strong governance cadence: a new wave of SOP (Standard Operating Procedure) subsystem bugs surfaced today (7 new issues), indicating active testing of the recently shipped 0.8.4 runtime. Release activity is quiet (no new releases), while the project continues processing a large backlog of RFCs (at least 8 open) and large-scale eval infrastructure PRs from distinguished contributors. Maintainer bandwidth appears stretched: 7 PRs are tagged `needs-author-action` and 6 issues require maintainer review, though key security fixes (pipeline tool policy, Bedrock Nova caching) were merged today.

## 2. Releases

**No new releases published in the last 24 hours.** The most recent tracked version is v0.8.4, with the v0.8.5 stabilization line (tracker #9459) scheduled to ship weekly cuts through August 30, 2026.

---

## 3. Project Progress

**5 PRs merged/closed today**, headlined by two meaningful fixes:

- **[PR #9737] fix(tools): enforce agent policy in pipelines** — Fixes the S0 security bug (#7947, confused deputy): `execute_pipeline` now respects per-agent tool gating instead of only the global allowlist. This is a significant security hardening step for v0.9.0. *(merged)*
- **[PR #8943] fix(providers): exclude Nova 2 from Bedrock prompt caching** — Resolves #8720; `us.amazon.nova-2-lite-v1:0` was failing with `400: extraneous key [cachePoint]`. *(merged)*
- **[PR #9329] refactor(zerocode): derive slash commands from shared command catalogue** — Closes #9172; ZeroCode now uses a single source of truth (`zeroclaw-commands::BUILTIN_COMMANDS`) for command identity, resolving a long-standing multi-source drift problem. *(merged)*
- **[PR #9659] fix(docs): disambiguate contextual protected literals** — Closes #9657; the protected-literal checker no longer mistakes "Signal" (channel name) for a product literal in unrelated contexts. *(merged)*
- **[PR #9764] test(config): widen scheduler-latency margin** — Fixes flaky test #9763 by increasing the scheduler-latency budget from 450ms to a more CI-tolerant margin. *(merged)*

**Note:** 4 of 5 merges are fixes; the only feature merge (#9329) is a refactor.

---

## 4. Community Hot Topics

**#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup** *(19 comments, open since May 20)*
This is the project's living governance document — now at revision 24. It's actively being rolled out but ratification remains deferred. The ongoing high engagement signals the community's desire for clearer work routing and label hygiene as the project scales. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)

**#8692 — Tracker: Maintainer decision queue for RFCs and design issues** *(11 comments)*
A meta-tracker to manage the growing backlog of RFCs awaiting maintainer sign-off. Its continued activity reflects a structural bottleneck: community members are proposing, but decisions are slow. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)

**#9106 — RFC: A2A outbound client (A2ATool)** *(11 comments)*
High community interest in bidirectional agent-to-agent communication. The RFC would enable ZeroClaw agents to proactively call external A2A-compliant agents (complementing the already-shipped inbound A2AServer). Accepted and marked no-stale; risk: high. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9106)

**#9246 — RFC: Preserve Todo tracker configuration during ZeroCode ownership migration** *(11 comments)*
A user-driven RFC (sponsored by @IftekharUddin) to prevent config loss during the ZeroCode ownership migration — a real-world pain point for teams using the tool's todo tracking. Accepted, in progress. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9246)

**#6954 — RFC: Provenance, conversation binding, and reply contract for internally initiated agent turns** *(10 comments)*
Revision 2 landed 2026-08-05 after a ratification correction; addresses a subtle correctness issue in cron/agent-initiated turns. Awaiting maintainer review. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6954)

---

## 5. Bugs & Stability

**New issues today (5 previously-unreported):**

| Severity | Issue | Summary | Fix? |
|----------|-------|---------|------|
| **High (P1)** | [#9786](https://github.com/zeroclaw-labs/zeroclaw/issues/9786) | Malformed `SOP.toml` silently dropped — `sop list` omits, `sop validate` falsely reports success. Indistinguishable from a missing SOP. | ❌ None yet |
| **High (P1)** | [#9779](https://github.com/zeroclaw-labs/zeroclaw/issues/9779) | `sops_dir` documented default not honored by daemon — SOP engine silently never loads (no error, no warning). | ❌ None yet |
| **High (P1)** | [#9770](https://github.com/zeroclaw-labs/zeroclaw/issues/9770) | `cron update` silently discards changes to declarative jobs (6 columns: command, name, expression, etc.). | ❌ None yet |
| **Medium (P2)** | [#9783](https://github.com/zeroclaw-labs/zeroclaw/issues/9783) | `finish_run` accepts failure reason, discards it — failed SOP runs record "that" but not "why". | ❌ None yet |
| **Medium (P2)** | [#9784](https://github.com/zeroclaw-labs/zeroclaw/issues/9784) | Multi-step agent-driven SOP marked failed mid-step with NO audit event; agent discovers via `sop_advance` returning no active run. | ❌ None yet |
| **Medium (P2)** | [#9792](https://github.com/zeroclaw-labs/zeroclaw/issues/9792) | Git channel: empty peer allowlist silently drops ALL events (incl. SOP routes) at DEBUG level only. | ❌ None yet |

**Also active:**
- [#9328](https://github.com/zeroclaw-labs/zeroclaw/issues/9328) *(high risk, accepted)*: `verifiable-intent` evaluates constraints without verifying the credential chain — a cryptographic trust gap in the VI reference implementation.
- [#9771](https://github.com/zeroclaw-labs/zeroclaw/issues/9771) *(P2)*: `zeroclaw-gateway` fails `clippy -D warnings` on default feature surface (dead-code regression).

**Fixed today:** S0 security issue #7947 (confused deputy) and caching bug #8720 (Bedrock Nova 2).

---

## 6. Feature Requests & Roadmap Signals

**Strong candidates for v0.8.5 / v0.9.0 (accepted + in-progress):**
- **A2A outbound client (A2ATool)** (#9106) — accepted, high interest; likely ships once the RFC is ratified.
- **Per-model capability & context-window config** (#7100, P1) — accepted; addresses real misreporting of vision support and context budget.
- **Telegram per-user session toggle** (PR #9772, new today) — community need for shared group-chat sessions; already has an implementation in flight.
- **WebSocket keepalive for chat** (PR #9701) — infrastructure improvement for Web UI reliability, authored by a trusted contributor.
- **Grok Build ACP model provider** (PR #9104) — new provider family; currently stalled on `needs-author-action`.

**Emerging signals (new today):**
- **#9788 — Report active shell dialect in system prompt** *(P3, blocked)*: The model currently guesses shell language from OS name; users want explicit dialect in the prompt to reduce shell-script errors.

**Note:** No new releases this cycle, so "next version" signals are inferred from accepted RFCs and merged feature PRs.

---

## 7. User Feedback Summary

**Pain points voiced this week:**
- **SOP subsystem reliability** (dominant theme, 5+ issues today): Users report silent failures — SOPs not loading, malformed configs being dropped invisibly, and runs failing without audit trails. The common thread is *"no feedback when something goes wrong,"* indicating a need for better diagnostics and fail-loud behavior.
- **Cron usability**: Multiple issues (#9672, #9796, #9770) about `cron` CLI examples being broken and `cron update` silently discarding changes — an operator-trust problem.
- **Telegram group collaboration** (#9772): Users want per-user sessions in shared groups to prevent context bleed between teammates.
- **Bedrock Nova 2 caching** (#8720, now fixed): Users hitting hard provider errors that were config-related, not code-related.

**Satisfaction signals:**
- The project's rapid turnaround on the S0 pipeline security bug (reported 6/18, fixed 8/7) is a strong positive signal for maintainers' security responsiveness.
- The community actively engages in governance RFCs (#6808, #8692) — a sign of healthy contributor investment.

---

## 8. Backlog Watch

**Long-stalled RFCs / PRs needing maintainer attention:**

| Item | Age | Status | Why it matters |
|------|-----|--------|----------------|
| [RFC #6954](https://github.com/zeroclaw-labs/zeroclaw/issues/6954) — provenance/reply contract for internal turns | ~2.5 months (open since 5/26) | Needs maintainer review (rev 2 submitted 8/5) | Blocks correctness for cron/agent-initiated turns |
| [RFC #7100](https://github.com/zeroclaw-labs/zeroclaw/issues/7100) — per-model capability config | ~2 months, P1 | Needs maintainer review | Directly affects model selection UX; P1 priority |
| [PR #9203](https://github.com/zeroclaw-labs/zeroclaw/pull/9203) — SOP authenticated HTTP fan-in | ~18 days, needs-author-action | Author must respond to review | Critical for secure SOP webhook routes |
| [PR #9002](https://github.com/zeroclaw-labs/zeroclaw/pull/9002) — keep agent turns alive after viewer disconnect | ~27 days, P1, needs-author-action | Author must respond | Web UI reliability issue; high risk. |
| [PR #9104](https://github.com/zeroclaw-labs/zeroclaw/pull/9104) — Grok Build ACP provider | ~22 days, needs-author-action | Author must respond | New provider; L-size, high-risk |
| [RFC #9397](https://github.com/zeroclaw-labs/zeroclaw/issues/9397) — WhatsApp empty `allowed_groups` → permit-none | ~12 days, P1, needs-maintainer-review | Security posture issue | Empty allowlist currently admits ALL groups — a default-deny violation |

**Meta-observation:** The #8692 maintainer decision queue itself has 11+ items pending — the project leadership should consider dedicating explicit maintainer hours to RFC triage, as several P1 items have been awaiting review for weeks.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*