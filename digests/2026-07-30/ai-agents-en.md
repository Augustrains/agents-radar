# OpenClaw Ecosystem Digest 2026-07-30

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-30 01:13 UTC

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

# OpenClaw Project Digest — 2026-07-30

## Today's Overview

OpenClaw is in a **high-activity maintenance phase** with significant stability and reliability concerns. The project shows **500 issues and 500 PRs updated in the last 24 hours**, with 444 open/active issues and 407 open PRs — indicating a large backlog of ongoing work. No new releases were published today. The project continues to address **critical stability bugs** across multiple subsystems including session management, memory indexing, subagent orchestration, and provider connectivity. A cluster of **P1 "diamond lobster" severity issues** around the Codex integration, OAuth refresh failures, and gateway event-loop stalls dominates the attention.

## Releases

**No new releases** were published today or in the recent window. The issue tracker references versions `2026.6.x` through `2026.7.1` as current, with multiple regressions reported between point releases (e.g., `2026.5.27 → 2026.5.28`).

---

## Project Progress

**Today's merged/closed PRs: 93** (out of 500 updated). Notable closures:

- **#116078** *(closed)* — `improve(ui): guide optional channel setup after model setup` — First-run UX gap fix, guides users through optional channel configuration
- **#107565** *(closed)* — `fix(voice-call): reject malformed Telnyx timestamps` — Security fix for voice webhook timestamp verification
- **#90621** *(stale, open)* — `chore(codeowners): gate heartbeat template and repair changes` — Process improvement adding CODEOWNERS gates
- **#116086** *(open, waiting on author)* — `fix(ui): clarify model setup and deduplicate active routes` — Addresses model configuration confusion
- **#116155** *(open)* — `fix(discord): preserve webhook timeout errors on stalled responses` — Improves error reporting for Discord delivery

The **#107565** voice-call security fix is the most significant merged change — it prevents acceptance of malformed timestamps in Telnyx webhook verification.

---

## Community Hot Topics

### Most Active Issues (by comment count)

1. **[#91009 — Codex PreToolUse native hook relay spawns CPU-bound processes](https://github.com/openclaw/openclaw/issues/91009)** (18 comments, 2 👍)
   - **Core Issue**: Codex app-server tool calls spawn multiple `openclaw-hooks` processes consuming 100%+ CPU each, stalling gateway RPC. Users see complete operational paralysis.
   - **Tags**: `P1`, `diamond lobster`, `impact:message-loss`, `impact:crash-loop`
   - **Age**: Opened 2026-06-06, still open

2. **[#86996 — Active Memory + Codex causes long response latency, hook timeouts, startup aborts](https://github.com/openclaw/openclaw/issues/86996)** (15 comments, 2 👍)
   - **Core Issue**: Complex interaction between Active Memory, lossless-claw, and Codex model causes entire agent to become unreliable for simple Telegram DMs.
   - **Tags**: `P1`, `diamond lobster`, `impact:message-loss`, `impact:auth-provider`, `impact:crash-loop`
   - **Age**: Opened 2026-05-26

3. **[#39476 — A2A sessions_send: target agent can call back causing duplicate messages](https://github.com/openclaw/openclaw/issues/39476)** (13 comments)
   - **Core Issue**: Inter-agent communication protocol flaw where `sessions_send` callbacks produce duplicate messages in the requester's channel.
   - **Tags**: `P1`, `platinum hermit`, `stale`, `impact:session-state`, `impact:message-loss`
   - **Age**: Opened 2026-03-08 (oldest active P1)

4. **[#90354 — Feature: Add bounded/validated append semantics for pre-compaction memory flush](https://github.com/openclaw/openclaw/issues/90354)** (11 comments)
   - **Core Issue**: Memory flush turns lack guardrails for append size, post-write validation, and silent failure handling — models can append oversized/noisy data.
   - **Tags**: `P2`, `diamond lobster`

5. **[#88657 — DeepSeek V4 Flash incomplete turn in 2026.5.27/28](https://github.com/openclaw/openclaw/issues/88657)** (10 comments)
   - **Core Issue**: Regression in specific releases where DeepSeek V4 Flash via OpenRouter produces zero-payload turns with no user-visible output.
   - **Tags**: `P2`, `platinum hermit`, `impact:message-loss`

### Most Active PRs

1. **[#115735 — fix(skills): honor Codex agents/openai.yaml invocation policy](https://github.com/openclaw/openclaw/pull/115735)** — Opened today, addresses Codex skill invocation alignment
2. **[#116143 — fix(channels): show tool lines under the progress status headline](https://github.com/openclaw/openclaw/pull/116143)** — Opened today, fixes Discord progress draft rendering
3. **[#114852 — feat(agents): rename scheduler strings to automations](https://github.com/openclaw/openclaw/pull/114852)** — Part of RFC 0026, renames "cron" to "automations" model-facing

### Underlying Needs Analysis

The community is experiencing **three systemic pain points**:
- **Codex/Anthropic integration fragility**: OAuth refresh failures (#86215, #89278), CPU-spawning hooks (#91009), mid-turn client closure (#86214) — the project's primary LLM integration is unstable
- **Subagent orchestration unreliability**: Silent completion drops (#92433, #89095), duplicate messages (#39476), announce suppression gaps (#8299, #90944)
- **Memory/search/session degradation**: Index corruption (#90042), unbounded growth (#89315), timeout masking (#112196), event-loop blocking (#112423)

---

## Bugs & Stability

### Critical Severity (P1/diamond lobster)

| Issue | Problem | Has Fix PR? |
|-------|---------|-------------|
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex PreToolUse hook spawns CPU-bound processes, stalls gateway | No |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) | Active Memory + Codex causes total unresponsiveness | No |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | Codex OAuth refresh succeeds but cron/heartbeat fail with 10s timeout | No |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth refresh failures wedge agent for hours | No |
| [#112423](https://github.com/openclaw/openclaw/issues/112423) | Large SQLite transcript cleanup blocks gateway event loop | No |
| [#87756](https://github.com/openclaw/openclaw/issues/87756) | Prompt-launched Lobster workflow hangs on nested /tools/invoke | No |
| [#92433](https://github.com/openclaw/openclaw/issues/92433) | Subagent completion silently dropped by announce steering | No |
| [#90944](https://github.com/openclaw/openclaw/issues/90944) | sessions_yield resume reply not delivered, wrong text sent | No |
| [#89315](https://github.com/openclaw/openclaw/issues/89315) | Gateway heap grows unbounded, killed by cgroup OOM | No |
| [#98976](https://github.com/openclaw/openclaw/issues/98976) | Provider refusals never trigger model fallback chain | No |
| [#111010](https://github.com/openclaw/openclaw/issues/111010) | Detached Codex subagents lose hook relay on parent release | No |
| [#90361](https://github.com/openclaw/openclaw/issues/90361) | Intermittent memory_search "index metadata is missing" | No |
| [#112196](https://github.com/openclaw/openclaw/issues/112196) | memory_search sync timeout masks as persistent provider failure | No |
| [#90042](https://github.com/openclaw/openclaw/issues/90042) | Gateway memory_search index stuck dirty after boot | No |
| [#89095](https://github.com/openclaw/openclaw/issues/89095) | Sub-agent run timeout silently drops completion event | No |

### Regressions Reported

- **#87756** (Prompt-launched Lobster workflow hangs vs curl-launched works) — regression
- **#89278** (Codex OAuth refresh succeeds but cron fails) — regression
- **#88707** (Regression 2026.5.27→5.28: Bedrock provider deregistration breaks all Bedrock calls)
- **#97616** (Zombie process accumulation from hook/tool children) — regression
- **#90711** (launchd plist hides all gateway stderr) — 5.28 regression
- **#105528** (exec/read tools silently return empty on Windows) — 2026.6.x regression

### Notable: No fix PRs exist for any P1/diamond lobster issues

This is concerning — the most critical stability issues have **no linked fix PRs** and are tagged `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision`, indicating they are stuck awaiting maintainer triage.

---

## Feature Requests & Roadmap Signals

### Active Feature Requests

| Issue | Request | Predicted Priority |
|-------|---------|-------------------|
| [#90354](https://github.com/openclaw/openclaw/issues/90354) | Bounded/validated append semantics for memory flush | **High** — addresses memory corruption risk |
| [#43454](https://github.com/openclaw/openclaw/issues/43454) | Gateway lifecycle hooks (onSubagentComplete, onToolCallThreshold) | Medium — closed but linked to ongoing subagent work |
| [#88154](https://github.com/openclaw/openclaw/issues/88154) | Slack Modal Support for structured input | Medium |
| [#13219](https://github.com/openclaw/openclaw/issues/13219) | Per-model usage logging for cost tracking | **High** — community demand for cost visibility |
| [#81061](https://github.com/openclaw/openclaw/issues/81061) | Pre-routing inbound message hook (before_route_inbound_message) | Medium |
| [#73537](https://github.com/openclaw/openclaw/issues/73537) | Production-readiness stability label on releases | **High** — user trust issue |
| [#8299](https://github.com/openclaw/openclaw/issues/8299) | Config option to suppress sub-agent announce | Medium |
| [#85461](https://github.com/openclaw/openclaw/issues/85461) | Capture image-generation provider usage metadata | Low-Medium |

### Likely Next Version Features

Based on PR activity and roadmap signals (RFC 0026 renaming in #114852):
- **"Cron" → "Automations" rename** (RFC 0026, Phase 1) — appears ready for merge
- **Plugin SDK deprecation metadata** (#90776) — groundwork for breaking changes
- **Model setup UX improvements** (#116086 closed, #116078 ready) — polishing the new UI

### Roadmap Uncertainty

The high volume of P1/diamond lobster stability bugs with no fix PRs suggests the **near-term roadmap is reactive** — the team is likely prioritizeing triage and hotfixes over new features. The 93 merged/closed PRs today are mostly fixes and refinements.

---

## User Feedback Summary

### Expressed Pain Points

1. **Reliability crisis**: Multiple users report agents becoming completely unresponsive, with no clear error messages. One user describes OpenClaw as "genuinely part of our daily workflow" (#73537) but is frustrated by lack of production-readiness signals.

2. **Upgrade breakage**: Users report point-release upgrades breaking critical functionality:
   - `2026.6.8 → 2026.6.9` corrupts email channel config (#95515)
   - `2026.5.27 → 2026.5.28` breaks Bedrock provider completely (#88707)
   - `2026.6.0 → 2026.6.1` loses progress on workarounds (#90711)
   - Windows users report exec/read tools silently failing (#105528)

3. **Debugging opacity**: Several issues highlight the difficulty of diagnosing failures:
   - Gateway stderr hidden by launchd plist (#90711)
   - memory_search timeout masked as provider failure (#112196)
   - Subagent timeouts produce zero notification (#89095)
   - Provider refusals give generic "LLM request failed" (#98976)

4. **Memory/complexity frustrations**: Users running "family and business assistant" deployments (#73537) report memory growth, OOM kills, and session database bloat blocking gateway responsiveness.

### Positive Signals
- **User #73537**: "It has genuinely become part of our daily workflow. Really appreciate the work you and the team put into this."
- **User #90361**: Includes a "locally hotfixed" workaround — engaged power user community.
- The 500 daily issue/PR updates show active community involvement despite frustration.

---

## Backlog Watch

### Critical Backlog Items (open >30 days, no fix PR, awaiting maintainer)

| Issue | Age | Status |
|-------|-----|--------|
| [#39476](https://github.com/openclaw/openclaw/issues/39476) — A2A sessions_send duplicate messages | 144 days | `stale`, `needs-live-repro` |
| [#8299](https://github.com/openclaw/openclaw/issues/8299) — Suppress sub-agent announce option | 178 days | `needs-maintainer-review`, `needs-product-decision` |
| [#11665](https://github.com/openclaw/openclaw/issues/11665) — Webhook session reuse doesn't work | 172 days | `CLOSED` but functionally unresolved |
| [#13219](https://github.com/openclaw/openclaw/issues/13219) — Per-model usage logging | 171 days | `needs-maintainer-review`, `needs-product-decision` |
| [#43454](https://github.com/openclaw/openclaw/issues/43454) — Gateway lifecycle hooks | 141 days | `CLOSED` with linked PR open |
| [#52526](https://github.com/openclaw/openclaw/issues/52526) — agent --json returns pre-hook text | 130 days | `stale`, `needs-maintainer-review` |
| [#69086](https://github.com/openclaw/openclaw/issues/69086) — attempt-execution session-history guard too broad | 102 days | `needs-maintainer-review`, `needs-product-decision` |
| [#81061](https://github.com/openclaw/openclaw/issues/81061) — Pre-routing inbound message hook | 79 days | `needs-product-decision` |
| [#86063](https://github.com/openclaw/openclaw/issues/86063) — Anthropic 1h cache invalidates every turn | 67 days | `needs-maintainer-review` |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) — Active Memory + Codex unresponsiveness | 65 days | `needs-maintainer-review`, `needs-product-decision` |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) — Codex OAuth wedges agent for hours | 67 days | `needs-maintainer-review`, `needs-product-decision` |
| [#87756](https://github.com/openclaw/openclaw/issues/87756) — Lobster workflow hangs on nested invoke | 63 days | `needs-maintainer-review`, `needs-product-decision` |
| [#88707](https://github.com/openclaw/openclaw/issues/88707) — Bedrock provider broken in 5.28 | 60 days | `needs-maintainer-review` |
| [#89095](https://github.com/openclaw/openclaw/issues/89095) — Sub-agent timeout no notification | 59 days | `needs-maintainer-review` |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) — Codex OAuth succeeds but cron fails | 58 days | `needs-maintainer-review`, `needs-product-decision` |
| [#90361](https://github.com/openclaw/openclaw/issues/90361) — memory_search index metadata missing | 56 days | `needs-maintainer-review` |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) — Codex hook CPU spawns | 54 days | `needs-maintainer-review`, `needs-product-decision` |
| [#92433](https://github.com/openclaw/openclaw/issues/92433) — Subagent completion dropped | 48 days | `needs-maintainer-review`, `needs-product-decision` |

**Observation**: 12+ of the most critical P1 bugs are awaiting maintainer review or product decision, with **zero linked fix PRs**. This pattern suggests either:
- The maintainer team is overloaded and cannot keep up with triage
- These bugs require architectural changes that haven't been prioritized
- The `clawsweeper` automation is correctly routing issues but fixes aren't materializing

### Stale PRs Needing Attention

- **#91408** (ACP bindings for Telegram DMs) — `waiting on author` since 2026-06-08
- **#90621** (CODEOWNERS gating) — stale, opened 2026-06-05
- **#90505** (Fix killed subagent task race) — stale, opened 2026-06-05
- **#90041** (Prevent message_tool_only from swallowing completions) — `waiting on author` since 2026-06-03
- **#90050** (Populate Langfuse trace-level input/output) — `waiting on author` since 2026-06-03
- **#112367** (GoogleChat/zalouser config key promotion) — `needs proof` since 2026-07-21

---

## Project Health Assessment

**Risk Level: HIGH** ⚠️

The project shows signs of **maintainer bottleneck**:
- 12+ P1/diamond lobster severity bugs unaddressed for 30-60+ days
- 407 open PRs with high merge-risk ratings (`🚨 compatibility`, `🚨 session-state`, `🚨 message-delivery`)
- Multiple regressions between recent point releases suggesting testing gaps
- No releases published in observation window

**Positive indicators**:
- High community engagement (500 daily updates, users contributing hotfixes)
- Some stability work is progressing (voice-call security fix merged, Discord progress improvements)
- Active RFC process (RFC 0026 scheduler rename moving forward)

**Recommended focus areas**:
1. **Reduce P1 bug count** — The 12+ unaddressed critical bugs are eroding user trust
2. **Improve release testing** — Multiple point-release regressions suggest insufficient testing
3. **Resolve Codex integration issues** — A disproportionate number of P1 bugs are Codex/OAuth related
4. **Clear the PR backlog** — 407 open PRs suggests review bottlenecks

---

## Cross-Ecosystem Comparison

**Cross-Project Ecosystem Comparison — 2026-07-30**

---

## 1. Ecosystem Overview

The personal AI agent open-source landscape is in a **high-velocity consolidation and hardening phase**, with leading projects simultaneously shipping ambitious architectural changes while struggling to contain regression debt from rapid release cycles. Activity across the eight tracked projects is **intense**: OpenClaw alone processed 500+ issues and PRs in 24 hours, while IronClaw merged 15 PRs and closed 30 issues in a single day. The ecosystem is polarizing between **reference implementations** (OpenClaw, ZeroClaw) bearing the burden of broad compatibility, and **specialized derivatives** (PicoClaw, NanoClaw, TinyClaw) optimizing for constrained or niche deployments. A shared pattern emerges: **memory architecture, inter-agent protocols, and provider integration stability** are the three axes where every project is actively investing or struggling.

---

## 2. Activity Comparison

| Project | Open Issues | Open PRs | Merged/Closed (24h) | Release (24h) | Health Signal |
|---|---|---|---|---|---|
| OpenClaw | 444 | 407 | 93 | None | ⚠️ High risk — critical P1 bugs, no fix PRs, maintainer bottleneck |
| IronClaw | ~20 (50 updated) | ~35 (50 updated) | 15 merged, 30 closed | None (release PR stalled 27d) | 🟢 Strong momentum — major refactors, coverage gates, security stack |
| NanoClaw | 2 active | ~4 open | 3 merged | None | 🟢 Healthy — rapid fixes, growing feature set |
| Hermes Agent | 43 | 45 | 5 merged | None | 🟡 Maintained — high issue load, moderate merge velocity |
| CoPaw | 21 | ~37 open | 13 merged | None | 🟡 Moderate-high — active fixing, v2.0.1 regressions |
| LobsterAI | 0 | 2 | 13 merged | None (2026.7.24 last) | 🟢 Strong — rapid fix cycle, clean tracker |
| NullClaw | 1 | 2 | 2 merged | None | 🟢 Light but healthy — targeted fixes |
| Moltis | 0 | 4 | 2 merged | None | 🟢 Active — observability and security hardening |
| PicoClaw | ~1 | 2 | 0 | None (v0.3.1) | 🟡 Low activity — sustained but slow |
| ZeroClaw | 39 | 6 merged | 6 closed | None | 🟡 High architectural ambition, maintainer queue under pressure |
| TinyClaw | — | — | — | — | 💤 No activity |
| ZeptoClaw | — | — | — | — | 💤 No activity |

---

## 3. OpenClaw's Position

**Advantages vs peers:**
- **Largest community:** 500 daily updates vs. 50 for IronClaw or ZeroClaw. User #73537 describes OpenClaw as "genuinely part of our daily workflow."
- **Broadest integration surface:** Supports Codex, Anthropic, OpenRouter, Bedrock, DeepSeek, Discord, Telegram, Slack, Telnyx — more providers and channels than any peer.
- **Most mature agent orchestration:** Subagent dispatch, A2A sessions, memory indexing, cron/automation — capabilities that derivatives (PicoClaw, NanoClaw) simplify from.

**Critical weakness:** The project is **dangerously overloaded**. 12+ P1 "diamond lobster" bugs have no fix PRs and are blocked on maintainer review for 30–60+ days. Multiple point-release regressions (5.27→5.28 broke Bedrock, 6.8→6.9 corrupted email config) erode trust. Codex/OAuth integration fragility accounts for a disproportionate share of critical bugs. In contrast, **IronClaw has no P0 without a fix path**, and **LobsterAI reverted a broken feature within 24 hours of identifying regressions**.

**Technical approach difference:** OpenClaw is a **monolithic reference implementation** — tries to support all possible configurations and integrations. IronClaw and ZeroClaw favor **modular architectures** (IronClaw's composition refactoring removed 9,421 lines; ZeroClaw's RFCs push toward runtime/channel separation). This modularity gives them better regression isolation.

---

## 4. Shared Technical Focus Areas

| Focus Area | Affected Projects | Specific Needs |
|---|---|---|
| **Memory architecture** | OpenClaw, ZeroClaw, NanoClaw, NullClaw | Index corruption (OpenClaw #90042, #90361), unbounded growth (OpenClaw #89315), configurable recall limits (NullClaw PR #979), session consolidation preserving media (NanoClaw PR #5157), memory/curated-memory separation (ZeroClaw RFC #9048) |
| **Provider integration reliability** | OpenClaw, Hermes Agent, IronClaw, CoPaw | Codex OAuth refresh failures (OpenClaw #86215, #89278), Gemini tool-calling 400s (IronClaw #6786, #6880), DeepSeek role injection bug (CoPaw #6541), OpenAI compatibility adapter demand (ZeroClaw #8603) |
| **Inter-agent communication** | OpenClaw, ZeroClaw, Moltis, NanoClaw | Duplicate messages in A2A sessions (OpenClaw #39476), outbound A2A client (ZeroClaw #9106), ACP protocol support (Moltis PR #1169, CoPaw #6531), multi-agent collaboration proposal (NanoClaw #5000) |
| **Scheduler/automation reliability** | OpenClaw, NullClaw, ZeroClaw, NanoClaw | Cron output silently discarded (ZeroClaw #9340), scheduler token not persisted (NullClaw #915), automations execute as interactive chats (IronClaw #6879), cron state inconsistency (NanoClaw #5163) |
| **WebUI and desktop UX** | OpenClaw, Hermes Agent, CoPaw, LobsterAI | Input occlusion, scroll jumps, session switching message loss, installers broken (CoPaw #6534), update detection false positives (Hermes Agent #74267), dark theme rendering issues |
| **Security hardening** | IronClaw, ZeroClaw, Moltis, CoPaw | Attested signing (IronClaw 8-PR stack), privileged tool gating (Moltis #1170), browser CDP opt-in (CoPaw #6500), prompt injection defenses (ZeroClaw #9542), E2EE probe for Python 3.12 (CoPaw #6486) |

---

## 5. Differentiation Analysis

| Axis | OpenClaw | IronClaw | ZeroClaw | CoPaw | LobsterAI |
|---|---|---|---|---|---|
| **Target user** | Daily-driver power users, multi-agent homes | Enterprise/QA-tolerant deployments | Workflow automation, crypto/Web3 | Chinese market, QQ/Feishu users, agent create | Desktop GUI users, side-chat cowork |
| **Primary backend** | Codex/Anthropic (fragile) | Gemini (broken on tools), Reborn stack | OpenAI-compatible (RFC), A2A protocol | Qwen, DeepSeek, MiniMax | Self-hosted, Electron-based |
| **Architecture** | Monolithic reference | Modular, composition-based | Runtime-channel separation (in RFC) | Plugin-based, cloud-enabled | Shim on OpenClaw core |
| **Release cadence** | Weekly point releases, regression-prone | RC-driven, stalled (27d) | Planned, consolidation phase | v2.0.1, fixing regressions | v2026.7.24, rapid fix cycle |
| **Key differentiator** | Broadest ecosystem | Testing infrastructure (WS9-12) | RFC-driven design | Chinese platform support | Desktop-first UX polish |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapidly iterating, high risk:** OpenClaw. Velocity is extreme but so is regression debt and maintainer bottleneck. The community is engaged but frustrated.

**Tier 2 — Strong momentum, managing risk:** IronClaw, ZeroClaw, NanoClaw. These projects are investing in architectural quality (coverage gates, RFC process, modular refactoring) and maintaining clean backlogs. IronClaw's 15 PRs merged + 30 issues closed in a day demonstrates disciplined throughput.

**Tier 3 — Stabilizing, polish phase:** Moltis, LobsterAI, NullClaw. Low issue counts, rapid fix cycles, focused feature additions (ACP protocol for Moltis, cowork polishing for LobsterAI). These are becoming reference implementations for specific integration patterns.

**Tier 4 — Low activity / dormant:** PicoClaw, TinyClaw, ZeptoClaw. PicoClaw has 1 active bug and no merged PRs today; TinyClaw and ZeptoClaw registered zero activity.

**Maturity signals:** IronClaw and ZeroClaw are investing most heavily in **quality infrastructure** — CI coverage gates, hermetic testing, RFC-based design decisions. OpenClaw and CoPaw are **feature-vulnerability cycles** — adding capabilities faster than the testing pipeline can validate.

---

## 7. Trend Signals

**1. Memory is the new bottleneck.** Four of eight active projects have critical memory issues — not just storage, but lifecycle management, indexed search reliability, and configurable recall. The community is moving beyond "does it remember?" to "how does it decide what to recall and when to forget?"

**2. Interoperability protocols are becoming table stakes.** Moltis merged ACP support, ZeroClaw is designing A2A outbound, NanoClaw added skill marketplaces, and OpenAI compatibility adapters are demanded across projects. The ecosystem is self-organizing around common protocols rather than monolithic lock-in.

**3. Provider diversity is a survival requirement.** Reliance on a single provider (OpenClaw on Codex, IronClaw on Gemini) creates acute fragility. Projects investing in fallback chains, quota-aware routing, and multi-provider parity (NanoClaw's Copilot request, ZeroClaw's Mixture-of-Agents RFC) are responding to community demand for resilience.

**4. Desktop UX is the differentiator for adoption.** The most upvoted community requests across projects are not AI capabilities but **UI polish**: Kanban boards (Hermes Agent), proper session management (CoPaw), stable Windows installers, and dark theme support. The technology is ready; the user experience is catching up.

**5. Chinese platform integration is an underserved market.** CoPaw's QQ/Feishu/DingTalk support and PicoClaw's DingTalk image PR signal a growing ecosystem gap that developers targeting Chinese users should prioritize.

**6. Security is moving from afterthought to architecture driver.** IronClaw's attested-signing stack, Moltis's operator gating, ZeroClaw's key-source abstraction, and CoPaw's CDP opt-in reflect a maturing ecosystem where trust and auditability are becoming competitive differentiators.

**Value for AI agent developers:** The most productive investment areas in Q3 2026 are (1) robust, configurable memory systems, (2) provider-agnostic fallback and quota management, (3) interoperable protocols (A2A, ACP, OpenAI-compatible APIs), and (4) deterministic testing infrastructure to prevent regression cycles. The projects that solve these will lead the next wave of adoption.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-30

## Today's Overview

NanoBot saw a high-activity day with 33 pull requests updated in the last 24 hours (19 merged/closed, 14 open) and 5 issues updated (3 active, 2 closed). The project remains in a strong maintenance and polish phase, with no new releases today. Activity was dominated by type-system modernization, WebUI reliability fixes, and memory/consolidation bug patches. The merge of BasedPyright strict type enforcement (PR #5158) marks a significant code quality milestone. No security advisories or blocking regressions were reported.

## Releases

No new releases were published today.

## Project Progress

19 PRs were merged or closed in the last 24 hours, reflecting substantial forward momentum:

**Type System & Code Quality**
- **PR #5158** (merged) — Enforced BasedPyright `strict` type checking across all 273 analyzed Python modules, a foundational improvement for maintainability and IDE support.

**WebUI Enhancements**
- **PR #5165** (merged) — Fixed false microphone silence errors that prevented valid voice input from being transcribed.
- **PR #5162** (merged) — Added optimistic message delivery status tracking (`sending`, `accepted`, `failed`) with correlated gateway error details.
- **PR #5116** (merged) — Added skill marketplaces (skills.sh + SkillHub) with trending lists, source filters, and install-history sparklines.

**Memory & Session Consolidation**
- **PR #5157** (merged) — Fixed media path preservation during session consolidation by sharing a unified media-breadcrumb renderer between live replay and archival.
- **PR #5160** (merged) — Fixed UTF-8 corruption in PowerShell 5.1 native pipeline input.

**Bug Fixes & Stability**
- **PR #5159** (closed) — Corresponding issue for the PowerShell 5.1 encoding bug.
- **PR #5118** (closed) — Media path drop during consolidation resolved.

## Community Hot Topics

**Most Active Discussions**

1. **Issue #5000 — Multi-agent collaboration proposal** (6 comments, open since Jul 20)  
   *[Link](https://github.com/HKUDS/nanobot/issues/5000)*  
   Proposes evolving subagent system toward persistent identities, shared task state, and true multi-agent coordination. This long-running discussion signals community appetite for advanced agent orchestration beyond simple task delegation.

2. **PR #5034 — Durable state-graph planning for /goal** (open since Jul 22, conflict-labeled)  
   *[Link](https://github.com/HKUDS/nanobot/pull/5034)*  
   A substantial feature PR adding structured execution plans with dependency tracking and recovery paths. Has been open for over a week with conflict markers, suggesting maintainers are weighing scope carefully.

3. **PR #5154 — Responses API parser safety** (open, priority p1)  
   *[Link](https://github.com/HKUDS/nanobot/pull/5154)*  
   Fixes a TypeError when SSE streams return primitive items. This touches a critical integration path for OpenAI-compatible providers.

**Underlying Needs:** The community is pushing for more sophisticated agent state management (Issue #5000, PR #5034) while also demanding reliability in provider integrations (PR #5154) and session handling (PR #5151, PR #5150).

## Bugs & Stability

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **P1** | #5118 (closed) | Session consolidation drops media paths → unrecoverable files | **Fixed** (PR #5157 merged) |
| **P1** | #5159 (closed) | PowerShell 5.1 UTF-8 pipeline corruption | **Fixed** (PR #5160 merged) |
| **P2** | #5163 (open) | Manual cron runs lose completion state on WebUI polling reload | No fix PR yet |

**Active Regressions with Fix PRs (non-merged)**
- PR #5154 (p1) — Primitive items crash in Responses API parser
- PR #5151 (p1) — Session lock leak retaining all keys indefinitely
- PR #5150 (p1) — Unbounded buffered session output in Exec tool
- PR #5166 (p1) — Goal permission ContextVar leak across async boundaries
- PR #5146 (p1) — Malformed token-usage day keys break all `/api/settings` requests

## Feature Requests & Roadmap Signals

| Feature | Request | Likelihood |
|---------|---------|------------|
| Multi-agent collaboration | Issue #5000 | Medium — long discussion, aligns with PR #5034 |
| Durable goal/state-graph planning | PR #5034 | Medium-High — active PR, but conflicts need resolution |
| Custom Telegram Bot API base URL | PR #4919 | High — required for self-hosted/enterprise deployments |
| Skill marketplace | PR #5116 (merged) | ✅ Already shipped in today's WebUI |

**Prediction:** The next release will likely include the skill marketplace (already merged), session lock management, and the output bounding fixes. The multi-agent proposal may be deferred to a 0.8-0.9 milestone.

## User Feedback Summary

**Pain Points Reported:**
- Voice input reliability: Microphone "silence" false positives preventing transcription (PR #5165 root cause)
- File loss after session consolidation: Absolute paths silently dropped (Issue #5118, now fixed)
- Cron state inconsistency: Completed jobs showing as "Failed" on WebUI reload (Issue #5163)
- Windows PowerShell compatibility: Non-ASCII input corruption on PS 5.1 (Issue #5159, now fixed)

**Satisfaction Signals:**
- The BasedPyright strict type checking merge (PR #5158) demonstrates strong commitment to code quality
- Three closed bugs in the media/session pipeline show responsive maintainer engagement

## Backlog Watch

| Item | Age | Status | Urgency |
|------|-----|--------|---------|
| **PR #4812** — Memory malformed role KeyError fix | 24 days open, conflict-labeled | Open | Medium — affects users with corrupted history |
| **PR #4919** — Custom Telegram Bot API URL | 16 days open, conflict-labeled | Open | Medium — blocking enterprise Telegram deployments |
| **PR #5094** — Canonical OpenRouter app URL | 4 days open, conflict-labeled | Open | Low — cosmetic/attribution fix |

**Notable:** Three open PRs carry conflict labels suggesting merge conflicts that need maintainer resolution. PR #4812 (memory malformed messages) is the longest-standing at 24 days and may affect users with corrupted history files.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-07-30

---

## Today's Overview

The Hermes Agent project is experiencing extremely high activity with 50 issues and 50 pull requests updated in the last 24 hours. The project maintains a healthy balance of incoming bug reports (43 open issues) and active development (45 open PRs), though only 5 PRs were merged or closed today, suggesting a stabilization period rather than a major feature push. The issue tracker shows significant community engagement with several long-running discussions exceeding 10 comments each, indicating sustained user investment in resolving platform-specific and configuration-related problems. Desktop compatibility, profile management, and provider credential handling remain the most active areas of community concern. No new releases were published today, with the latest stable version remaining v0.19.0 (2026.7.20).

**Project Health:** ⚠️ High activity with substantial bug load, moderate merge velocity.

---

## Releases

No new releases were published in the last 24 hours. The latest stable release remains Hermes Agent v0.19.0 (2026.7.20). Users tracking the `main` branch should prepare for significant changes to SQLite journal mode handling, credential pool logic, and desktop profile management based on committed PRs today.

---

## Project Progress

**Merged/Closed PRs Today (5 total):**

- **[#74485](https://github.com/nousresearch/hermes-agent/pull/74485)** – `fix(state): configurable journal_mode + WAL-refusal detection cluster` — Merged. This is a **critical stability fix** consolidating fixes for four separate issues (#68912, #57918, #46865, #55322). It makes `database.journal_mode` the canonical SQLite mode operator, detects WAL refusal across three platform shapes (raising, silent no-op, disk-I/O), and never live-downgrades existing WAL databases. This directly addresses the `state.db` corruption bug on macOS virtiofs ([#68545](https://github.com/nousresearch/hermes-agent/issues/68545)) and closes [#57820](https://github.com/nousresearch/hermes-agent/issues/57820).

- **[#74488](https://github.com/nousresearch/hermes-agent/pull/74488)** – `Feat/backend integration` — Closed as invalid.

- **[#74496](https://github.com/nousresearch/hermes-agent/pull/74496)** – `fix(prompt): apply root policy to named profiles` — Closed as duplicate (superseded by [#74502](https://github.com/nousresearch/hermes-agent/pull/74502)).

- **[#60197](https://github.com/nousresearch/hermes-agent/issues/60197)** – Bug: `RuntimeError: Event loop is closed during /exit` — Closed, indicating the MCP server shutdown race condition has been resolved.

- **[#67165](https://github.com/nousresearch/hermes-agent/issues/67165)** – Bug: `cua-driver macOS ScreenCaptureKit display_count=0` — Closed, likely resolved in a prior commit.

**Closed Issues Today (7 total):** Includes the critical `state.db` corruption fix, the Telegram pairing code display bug ([#46580](https://github.com/nousresearch/hermes-agent/issues/46580)), and the flaky PTY session test ([#73854](https://github.com/nousresearch/hermes-agent/issues/73854)).

---

## Community Hot Topics

### Most Active Issues (by Comments)

1. **[#71298](https://github.com/nousresearch/hermes-agent/issues/71298)** – *Bug: providers vs custom_providers dual storage causes CLI/GUI mismatch* (13 comments)
   - **Analysis:** This is a **high-impact configuration inconsistency** where two independent provider storage sections (`providers` vs `custom_providers`) in `config.yaml` are displayed differently between `hermes setup model` CLI and the Hermes Desktop GUI. Users are confused about which storage section takes precedence, and model versions get stuck in profiles. This represents a fundamental UX architecture issue that affects all users.

2. **[#69551](https://github.com/nousresearch/hermes-agent/issues/69551)** – *Desktop SSH remote mode broken with non-default profiles* (12 comments)
   - **Analysis:** A **profile-scoping bug** where token-path validation resolves against the profile-scoped `HERMES_HOME` while the client hardcodes `~/.hermes/desktop-ssh`. This breaks remote desktop access for any user with multiple profiles — a growing use case as Hermes expands its multi-profile capabilities.

3. **[#18715](https://github.com/nousresearch/hermes-agent/issues/18715)** – *Support remote Hermes agent with local tool execution* (12 comments, 👍22)
   - **Analysis:** The **second-most upvoted issue** (22 reactions). Users want to keep model execution on a powerful remote machine while running tools locally (e.g., for filesystem access or local APIs). This reflects a fundamental architecture request for split-agent topologies that is critical for enterprise adoption.

4. **[#41222](https://github.com/nousresearch/hermes-agent/issues/41222)** – *Feature Request: Integrate Kanban Board into Desktop App* (9 comments, 👍16)
   - **Analysis:** Strong community support (16 upvotes) for eliminating the friction of switching between CLI and Desktop for multi-agent Kanban workflows. This is a **clear roadmap signal** for desktop app enhancement.

### Most Active PRs (by Comments)

All PRs listed today show 0 comments, likely due to being very fresh (created within the last 24 hours). The most significant PRs with highest community interest based on context:

- **[#74485](https://github.com/nousresearch/hermes-agent/pull/74485)** – Journal mode fix (merged, critical)
- **[#74490](https://github.com/nousresearch/hermes-agent/pull/74490)** – Venv cleanup fix
- **[#74495](https://github.com/nousresearch/hermes-agent/pull/74495)** – Media resend fix for gateway

---

## Bugs & Stability

### Critical/P1 Bugs Reported Today

1. **[#74373](https://github.com/nousresearch/hermes-agent/issues/74373)** – `distribution_owned` does not constrain profile distribution copy/update payload (P1)
   - **Summary:** The `distribution_owned` manifest field is completely ignored by `_copy_dist_payload()`. All staged entries are copied unless they match a hardcoded `USER_OWNED_EXCLUDE` list. This allows distribution files to be overwritten and breaks profile isolation guarantees.
   - **Fix PR:** [#74498](https://github.com/nousresearch/hermes-agent/pull/74498) — Open.

2. **[#74456](https://github.com/nousresearch/hermes-agent/issues/74456)** – Hermes Agent installation fails in Termux (P2)
   - **Summary:** The installer script fails on Android Termux environments. A user reports the installation attempt produces errors with no clear resolution path.
   - **Fix PR:** None yet.

### Notable P2 Bugs

3. **[#74267](https://github.com/nousresearch/hermes-agent/issues/74267)** – Windows Desktop updater falsely detects running Hermes processes (P2)
   - **Summary:** The Windows updater aborts with "Another Hermes process is using this installation" even when all Python processes terminate correctly and no other Hermes instances are running. Persists across reboots.
   - **Fix PR:** [#74487](https://github.com/nousresearch/hermes-agent/pull/74487) — Open, addresses CRLF checkout issue for Windows.

4. **[#74462](https://github.com/nousresearch/hermes-agent/issues/74462)** – High cold start latency (16s for first chat, P3)
   - **Summary:** The first chat in each session takes 16 seconds to respond, far exceeding the expected 2-second cold start. Affects TUI mode.
   - **Fix PR:** None yet.

### Bug Clusters and Patterns

- **Desktop Profile Visibility Issues:** [#70679](https://github.com/nousresearch/hermes-agent/issues/70679) (profile switcher hidden in global remote mode), PR [#74500](https://github.com/nousresearch/hermes-agent/pull/74500) addresses this.
- **Database Corruption:** [#68545](https://github.com/nousresearch/hermes-agent/issues/68545) (state.db corruption on macOS virtiofs) — **Fixed** via [#74485](https://github.com/nousresearch/hermes-agent/pull/74485).
- **MCP Server Shutdown:** [#60197](https://github.com/nousresearch/hermes-agent/issues/60197) (`RuntimeError: Event loop is closed`) — **Closed**.
- **Media Attachment Delivery:** PR [#74495](https://github.com/nousresearch/hermes-agent/pull/74495) addresses silent media attachment failures.
- **Compression/Tool Loop Exhaustion:** [#72451](https://github.com/nousresearch/hermes-agent/issues/72451) (compression attempt budget exhaustion), PR [#74355](https://github.com/nousresearch/hermes-agent/pull/74355) in progress.

---

## Feature Requests & Roadmap Signals

### High-Priority Requests (by Upvotes)

1. **[#18715](https://github.com/nousresearch/hermes-agent/issues/18715)** – Remote agent with local tool execution (👍22) — This is a **major architectural request** indicating demand for split-agent topologies. Likely in roadmap within 1–2 releases given the strategic importance for enterprise hybrid deployments.

2. **[#41222](https://github.com/nousresearch/hermes-agent/issues/41222)** – Kanban board integration in desktop app (👍16) — Strong community interest in eliminating CLI friction for multi-agent workflows. Likely to be addressed in a future desktop update.

### Design Changes in Progress

- **[#71727](https://github.com/nousresearch/hermes-agent/issues/71727)** – Named delegation profiles: Prevents incoherent model/endpoint pairs by allowing named credential bundles for `delegate_task`. P3 priority.
- **[#70241](https://github.com/nousresearch/hermes-agent/issues/70241)** – `max_context_length` global ceiling: Survives model switches mid-session. P3, needs decision.
- **[#73886](https://github.com/nousresearch/hermes-agent/pull/73886)** – Multiple cron delivery targets for desktop: Replaces dropdown with checkbox group. Open PR.

### Predictions for Next Version (v0.20.0)

- Configurable `database.journal_mode` (already merged in #74485)
- Named delegation profiles (#71727 — P3, needs decision, but aligns with multi-profile growth)
- Desktop profile switcher fix for global remote mode (#74500 in progress)
- Root policy application to named profiles (#74502 in progress)

---

## User Feedback Summary

### Pain Points

- **Configuration Complexity:** Multiple users express confusion over dual provider storage (`providers` vs `custom_providers`), different behavior between CLI and GUI, and model version stuck in profiles (#71298).
- **Profile Isolation Failures:** The `distribution_owned` manifest bypass (#74373) undermines trust in Hermes' profile isolation model. Users expect declared ownership boundaries to be respected.
- **Desktop Remote Access:** SSH remote mode is broken with non-default profiles (#69551), and global remote mode hides the profile switcher (#70679). These regressions affect power users who rely on multi-profile remote setups.
- **Windows-Specific Issues:** The updater's false process detection (#74267) and CRLF checkout problems (#74487) create installation friction unique to Windows users. A user reports the issue persists even after full reboot.
- **SQLite Database Stability:** The `state.db` corruption issue on macOS virtiofs (#68545) caused significant concern, though it appears fixed in today's merged PR #74485.
- **Installation Failures:** Termux installation (#74456) is completely broken, limiting Hermes usage on Android/mobile environments.

### Satisfaction Signals

- The community remains highly engaged, with 22 upvotes on the remote agent feature request and 16 on Kanban integration — indicating strong desire for platform growth.
- Multiple users are actively contributing PRs, demonstrating high developer engagement.
- The closed bugs today (7) and merged PR (especially #74485) show maintainers are responsive to critical database stability issues.

---

## Backlog Watch

### Issues Needing Maintainer Attention

1. **[#7489](https://github.com/nousresearch/hermes-agent/issues/7489)** – *RPM-based pre-emptive throttling using x-ratelimit response headers* (Created: 2026-04-11, 6 comments)
   - **Age:** 111 days without resolution
   - **Status:** P3, no assigned milestone or PR
   - **Risk:** Provider rate limiting (429) causes expensive retry/failover loops. This feature would significantly improve reliability for heavy API users.

2. **[#18659](https://github.com/nousresearch/hermes-agent/issues/18659)** – *scan_skill_commands unconditionally clears _skill_commands* (Created: 2026-05-02, 5 comments)
   - **Age:** 90 days without resolution
   - **Status:** P2, needs-decision
   - **Risk:** On scan failure, all 90+ skill slash commands are silently lost with zero user-facing error. This is a fragile error-handling pattern that could cause subtle UX regressions.

3. **[#38359](https://github.com/nousresearch/hermes-agent/issues/38359)** – *TUI dark theme renders inline diff with light backgrounds* (Created: 2026-06-03, 2 comments)
   - **Age:** 57 days without resolution
   - **Status:** P3
   - **Risk:** Low severity but affects daily UX for terminal users who rely on dark themes.

4. **[#44799](https://github.com/nousresearch/hermes-agent/issues/44799)** – *Codex OAuth refresh chain not maintained during credential exhaustion* (Created: 2026-06-12, 5 comments)
   - **Age:** 49 days
   - **Status:** P2, sweeper:risk-security-boundary
   - **Risk:** During long cooldown windows (e.g., ChatGPT weekly quota), the refresh token expires silently, causing permanent credential loss. Requires user re-authentication.

### PRs Needing Review

- **[#51797](https://github.com/nousresearch/hermes-agent/pull/51797)** – *fix(cli): preserve one-shot isolation flags* (Created: 2026-06-24, P2)
  - **Age:** 37 days without review
  - **Summary:** Ensures `HERMES_IGNORE_USER_CONFIG=1` and other isolation flags are respected during startup discovery. Addresses a configuration leak that could affect CI/CD and sandboxed environments.
  - **Risk:** Moderate blast radius — isolation failures could leak user config into one-shot invocations.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-30

## Today's Overview
PicoClaw shows **low activity** over the past 24 hours, with only 1 issue updated, 2 pull requests (both still open), and no new releases. The single active issue reports a moderate regression in chat routing functionality, while the two open PRs — one for DingTalk image support and one for installation script migration — have seen recent maintainer attention but remain unmerged. Overall, the project appears stable but with a slowing pulse; no critical infrastructure changes have landed recently.

## Releases
**No new releases** since the last digest. The latest version remains **v0.3.1** (revision `2cf030d2`).

## Project Progress
- **No PRs were merged or closed** in the last 24 hours.
- Two PRs remain open and under review:
  - **#3283** — fix(dingtalk): support picture/image message inbound (stale, last updated 2026-07-29)
  - **#1951** — chore: move installation scripts from docs repo to here (type: enhancement, domain: build, last updated 2026-07-29)

No features or fixes advanced to the main branch today.

## Community Hot Topics
- **#3301 [BUG]** — `/clear` and session auto-compression don't work in chats routed to non-default agent via dispatch rules  
  URL: https://github.com/sipeed/picoclaw/issues/3301  
  Author: j-v (Raspberry Pi user, Discord/Telegram channels on DeepSeek via OpenCode Go).  
  This is the **only issue updated** in 24 hours. It has 0 comments and 0 reactions, but its content reveals a significant user pain point: session management breaks when custom dispatch rules are used. The lack of discussion suggests the community has not yet weighed in, but maintainers should prioritize reproducing this.

## Bugs & Stability

| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **High** | #3301 | `/clear` and session auto-compression fail for non-default agents routed via dispatch rules | No |
| Low | #3283 (PR) | DingTalk image inbound support — not a bug, but a feature gap | N/A |

**Key bug detail:** The `/clear` command and auto-compression not working in multi-agent dispatch scenarios is a **regression** that affects any user running custom dispatch rules. Since it involves session state management, it could lead to degraded user experience (memory leaks or stale context). No associated fix PR has been filed.

## Feature Requests & Roadmap Signals
- **#3283 (PR)** — DingTalk image message support: This is a **channel-specific enhancement** for the DingTalk platform. While it's a PR (not an issue), the addition of `downloadInboundPicture`, `getAccessToken`, and token caching infrastructure suggests a desire to make PicoClaw more capable in Chinese enterprise messaging. Likely candidate for **v0.3.2** if merged.
- **#1951 (PR)** — Move installation scripts from docs repo: This is a **maintainability improvement** that consolidates deployment documentation. Not user-facing, but signals a push to reduce fragmentation — could indicate a v0.4.0 preparation.

No brand-new feature requests were filed today.

## User Feedback Summary
- **Pain point (Raspberry Pi user j-v):** Session management is broken when using dispatch rules to route to non-default agents. This undermines one of PicoClaw's core differentiators: multi-agent dispatch. User reports clear frustration with the inability to reset context.
- **General observation:** The project lacks recent user feedback in issues. The low issue volume (only 1 in 24h) may indicate either high stability or low engagement. Given that the open issue references a functional regression, the latter is more likely.

## Backlog Watch
| Issue/PR | Status | Last Update | Maintainer Action Needed |
|----------|--------|-------------|--------------------------|
| **#1951** (PR) — Move installation scripts | Open, no activity since 2026-07-29 (but stale since March) | 2026-07-29 | Requires final review and merge; has waited >4 months |
| **#3283** (PR) — DingTalk image support | Open, marked `[stale]` | 2026-07-29 | Needs code review; token caching logic may have security implications |
| **#3301** (bug) — dispatch rule session bug | Open, uncommented | 2026-07-29 | Urgent: needs reproduction, triage, and assignee; no maintainer response yet |

**Longest-standing item:** PR #1951 (opened 2026-03-24, over 4 months stale). This continues to be a roadmap blocker if maintainers intend to clean up documentation repos before a larger release.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-30

## 1. Today's Overview
Project activity has returned to a strong cadence after a period of relative quiet, with **6 pull requests updated** and **3 merged/closed** in the last 24 hours. Two open issues remain active, reflecting both a maturing feature landscape and ongoing growing pains from Telegram's latest API bump. The steady stream of PR merges—particularly a long-dormant session routing fix (PR #2440, opened May 13) being closed today—signals that the maintainers are clearing technical debt while advancing core reliability. **Overall health: active with good momentum.**

## 2. Releases
No new releases today. The latest available release remains the one preceding the current development cycle; users building from source benefit from the hardened image fetch (PR #3150) and session routing improvements merged today.

## 3. Project Progress
Three pull requests were **merged or closed** in the last 24 hours:

- **[PR #3150]** — [core-team] Hardened agent image from registry (by gavrielc)  
  Adds a prebuilt, production-hardened agent container image sourced from Echo.ai, dramatically reducing `nanoclaw setup` time and attack surface. Building locally remains the default and only account-free path.  
  *Link:* https://github.com/qwibitai/nanoclaw/pull/3150

- **[PR #2440]** — fix(poll-loop) + feat(agent): Session routing fix and pre-compaction notification (by poisson-le; opened May 13, closed today)  
  Fixes a subtle bug where container restarts could misroute the first inbound message (an agent-type approval notification instead of a user message). Also adds a pre-compaction notification to the agent lifecycle.  
  *Link:* https://github.com/qwibitai/nanoclaw/pull/2440

- **[PR #2904]** — fix(slack): Reload thread history from platform on @mention (by gergokekesi)  
  Critical fix for Slack `engage_mode: 'mention'` wirings: previously, re-tagging the bot in a deep thread only delivered the single tagged message, leaving all human replies invisible. Now the bot fetches the full thread history.  
  *Link:* https://github.com/qwibitai/nanoclaw/pull/2904

## 4. Community Hot Topics
Two issues are drawing community attention:

- **🔥 Issue #1350** — "Add GitHub Copilot SDK as alternative AI backend" (by scottgl9, 8 👍, 3 comments)  
  The most popular open feature request. Users want Copilot models (GPT-4.1) alongside Claude. Given the 31% upvote ratio relative to total open issues, this is the #1 requested backend expansion.  
  *Link:* https://github.com/qwibitai/nanoclaw/issues/1350

- **⚡ Issue #3151** — "Telegram: Bot API 10.1 rich_message inbound arrives empty" (by jonnychesthair-crypto, opened yesterday)  
  Fresh, zero-comment bug report with a clear root-cause analysis referencing Bot API 10.1 (released June 11). Expect rapid maintainer response given the severity.  
  *Link:* https://github.com/qwibitai/nanoclaw/issues/3151

## 5. Bugs & Stability
**High severity** — one actively reported bug:

- **[Issue #3151]** — Telegram Bot API 10.1 `rich_message` payloads silently dropped (text + attachments go empty, no pipeline error). Impact: any user pasting formatted web content into Telegram loses all message content when using a NanoClaw agent.  
  *Severity:* **Critical** — silent data loss, wide Telegram user base affected. No fix PR in flight as of today.  
  *Link:* https://github.com/qwibitai/nanoclaw/issues/3151

**Medium severity** — fixed today:

- **[PR #2904]** — Slack thread history not fetched on re-@mention in `engage_mode: 'mention'` — **merged today**, fix live in main.  
  *Link:* https://github.com/qwibitai/nanoclaw/pull/2904

## 6. Feature Requests & Roadmap Signals
Three substantial features are under active development or discussion:

1. **Quota fallback engine (PR #3057)** — dual-engine support (Claude→Codex overflow), handoff recaps, proactive quota warnings. Battle-tested in production since July 6 on WhatsApp. Likely to merge in the next 1-2 weeks.  
   *Link:* https://github.com/qwibitai/nanoclaw/pull/3057

2. **GitHub Copilot SDK backend (Issue #1350)** — the most upvoted open feature. Predict inclusion in **v0.12** (Q3 2026) if maintainers prioritize multi-backend parity.

3. **CLI usability enhancement (PR #3149)** — adds `--rw` flag to `groups config add-mount` for read-write mounts. Small but addresses a common deployment friction point.

## 7. User Feedback Summary
- **Pain points:** Telegram Bot API 10.1 compatibility is the loudest current voice—users are losing messages with zero error feedback. Slack thread history not being loaded on @mention (now fixed) was another common frustration for `mention`-mode deployments.
- **Satisfaction:** The hardened image fetch (PR #3150) addresses a long-standing complaint about slow, error-prone local builds. The dual-engine fallback (PR #3057) is generating positive early buzz from production users.
- **Unmet need:** The 8-upvote on Issue #1350 (Copilot backend) reflects a clear desire for provider diversity beyond Anthropic.

## 8. Backlog Watch
No long-dormant issues with critical impact are currently unaddressed. The oldest open PR in today's batch (#2440, May 13) was **merged today**, indicating good backlog hygiene. PRs #3145 (db backfill migration, opened July 28), #3149 (CLI flag, July 29), and #3057 (quota fallback, July 15) remain open and should be monitored for merge cadence—especially #3057 as it touches production-critical quota logic.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**Project Digest: NullClaw — 2026-07-30**

**1. Today's Overview**  
NullClaw shows moderate development activity with 4 pull requests updated in the last 24 hours and 1 active issue. Two PRs were merged/closed, and two remain open, indicating steady progress on both feature implementation and bug fixes. No new releases were published today, but the repository has significant movement on critical memory and scheduler subsystems. The project appears healthy, with community contributions (notably from valonmulolli) driving core improvements.

**2. Releases**  
*None. No new versions were released in the last 24 hours.*

**3. Project Progress**  
Two pull requests were merged or closed today:

- **PR #981** (merged) — *feat(provider): add grok-cli provider for xAI Grok CLI*: Introduces a new CLI-based provider that delegates to the local `grok` CLI, following the same spawn-per-request pattern as the existing `codex-cli` provider. This expands NullClaw's model compatibility to xAI's Grok models. ([#981](https://github.com/nullclaw/nullclaw/pull/981))

- **PR #961** (closed, presumably superseded) — *feat(memory): add configurable auto-recall, recall_limit, max_context_bytes*: This older PR has been closed in favor of a newer iteration (#979) that carries the same feature set, signaling that the implementation was revised for a cleaner merge path.

**Key advancement**: The memory recall system is receiving important configurability — users will soon be able to disable automatic memory recall, limit the number of recalled entries (default 5), and cap total recall context size in bytes.

**4. Community Hot Topics**  
The most active item is **Issue #915** — *[bug] Problem with scheduler unauthorized* — which has accumulated 3 comments and 1 reaction since creation on 2026-05-15. The user reports that the scheduler tool fails to authenticate on Telegram/Chat integrations running under Ubuntu with an external Ollama host (Qwen3.6:27B on RTX 3090). The underlying issue appears to be a missing persistent token file that the cron/scheduler relies on for gateway authentication. A fix is already in progress via **PR #980**. ([#915](https://github.com/nullclaw/nullclaw/issues/915))

**5. Bugs & Stability**  
One active bug is reported today (updated yesterday):

- **Issue #915** — *Scheduler unauthorized*: **Severity: High** (blocks scheduled tasks). The scheduler cannot authenticate with the gateway because the paired token generated during `/pair` is stored only in memory and never written to disk. A dedicated fix PR (#980) exists and is currently open.

**No other bugs, crashes, or regressions were reported in the last 24 hours.**

**6. Feature Requests & Roadmap Signals**  
Two feature-oriented PRs signal likely upcoming capabilities:

- **PR #979** — *feat(memory): add configurable auto-recall, recall_limit, max_context_bytes*: This is the active incarnation of memory recall customization. Users will gain control over whether the agent automatically enriches conversations with past memories, and how much memory context is injected per request. Likely to land in the next release.

- **PR #981** (already merged) — *grok-cli provider*: This is now in the codebase and will ship with the next release, enabling xAI Grok CLI as a backend.

**Prediction for next release**: Memory recall configuration (auto_recall, recall_limit, max_context_bytes) plus the Grok CLI provider. The scheduler token persistence fix (PR #980) is also a strong candidate as it resolves a blocking bug.

**7. User Feedback Summary**  
**Pain points**:
- The scheduler is unusable for the reporter (scabros) due to the authentication token not being persisted to disk. The user mentions Telegram/Chat integration breaks entirely for scheduled tasks.
- No negative feedback received on current released features.

**Use cases represented**:
- Running NullClaw on Ubuntu with external Ollama hosts and local GPU (RTX 3090) for large models (Qwen3.6:27B).
- Use of scheduler tool within Telegram/Chat UI for automated task execution.

**Satisfaction signals**: None explicit, but the community is actively contributing fixes (valonmulolli) — a positive health signal.

**8. Backlog Watch**  
- **Issue #915** (created 2026-05-15, updated 2026-07-29) — *Scheduler unauthorized*: Has been open for over 2 months with no maintainer comment. A fix PR (#980) was submitted yesterday; this needs maintainer review and merge to resolve the long-standing bug.
- **PR #979** (created 2026-07-29) — Memory recall config: Should be reviewed and merged, as it supersedes the now-closed PR #961. No maintainer activity yet on this new version.

**No other issues or PRs appear abandoned or lacking maintainer attention at this time.**

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-30

---

## 1. Today's Overview

IronClaw remains in an intense, high-velocity development phase dominated by the **Reborn product-surface migration** and a sweeping **attested-signing feature stack** (8-part PR series). Activity is extremely high: 50 issues and 50 PRs updated in the last 24 hours, with 30 issues closed and 15 PRs merged. The project shows strong momentum toward production readiness, with major infrastructure work in composition refactoring, CI coverage enforcement, and signing/security hardening. However, several **critical QA bugs** (Gemini tool-calling failures, turn-state store degradation, automation pipeline defects) signal that stability work is actively catching up to feature velocity.

---

## 2. Releases

**No new releases today.** The last release attempt remains PR #5598 (`chore: release`), which has been open since July 3 and is still awaiting merge. That PR proposed breaking changes in `ironclaw_common` (0.4.2 → 0.5.0, due to added `Copy` impl) and `ironclaw_skills` (0.3.0 → 0.4.0). No migration notes have been published yet.

---

## 3. Project Progress

**15 PRs merged/closed today.** Key advances:

- **Composition refactoring (landmark):** PR #6691 (ilblackdragon) merged — reduced `ironclaw_reborn_composition` by **9,421 lines**, splitting monolithic factory/runtime code into focused assembly modules and deleting duplicate adapters. This is a significant structural cleanup.
- **WebUI streaming fix:** PR #6876 (serrrfirat, open) restores smooth streaming with `streamdown@2.5.0`, replacing a coarse 75ms coalescer with a 16ms snapshot window. Addresses a long-standing user experience pain point.
- **CI coverage gates (two PRs):** PR #6889 enforces WS11 coverage with 85.11% aggregate ratchet and numerator-backed floors for 15 critical crates. PR #6881 completes WS12 scaling, artifact, and coverage gate infrastructure.
- **Testing infrastructure:** PR #6884 adds WS10 regression promotion loop (production failures → scrubbed artifacts → regression fixes). PR #6886 completes WS9 generated state machines for seven-dimension equivalence testing.
- **Attested-signing stack (6 of 8 PRs open):** Groups 4–8 now all open (PRs #6769, #6809, #6811, #6813, #6818, #6822 by zmanian). These add multi-tenant isolation, trust registration, KMS ship-gate, Ledger clear-signing product (phase B/C), and attested gate resolve on capability-dispatch.
- **Channel migration:** Issue #3577 tracks v1-to-Reborn channel porting; Telegram port (#3581) is closed, with WASM-based ProductAdapter path progressing.
- **Process journal kernel moved:** Issue #6666 (ilblackdragon, closed) moved turn-run lifecycle representation into `ironclaw_processes`, proving neutral process-journal architecture.

---

## 4. Community Hot Topics

**Most engaged issues and PRs (by comment count):**

1. **#3031** (CLOSED, 7 comments) — *[EPIC] Reborn product surface migration* — The parent epic tracking the entire Reborn migration. High organizational importance; coordinates blocking compatibility gates (#3020) and final cutover readiness gates (#3022, #3032, #3039, #3067). URL: [Issue #3031](https://github.com/nearai/ironclaw/issues/3031)

2. **#6524** (OPEN, 4 comments) — *Epic: Hermetic capability and journey testing platform* — Addresses the structural gap in deterministic coverage for all capabilities and critical user journeys. Signals a push toward mechanical verification over manual testing. URL: [Issue #6524](https://github.com/nearai/ironclaw/issues/6524)

3. **#6786** (OPEN, 3 comments) — *[QA] provider_id="gemini" 400s on every tool call* — Active QA blocker; builtin tool schemas ship empty "type" to `functionDeclarations`. Urgent for Gemini provider users. URL: [Issue #6786](https://github.com/nearai/ironclaw/issues/6786)

4. **#3045, #3044** (both CLOSED, 3 comments each) — Runtime presets and local developer runtime profiles — Core Reborn ergonomics: enabling simple `ironclaw run --preset=...` without hand-wiring low-level grants. URL: [Issue #3045](https://github.com/nearai/ironclaw/issues/3045), [Issue #3044](https://github.com/nearai/ironclaw/issues/3044)

**Underlying needs:** The community (primarily core contributors) is driving three themes: (1) **developer experience** — making Reborn easy to operate and develop against; (2) **provider reliability** — especially Gemini integration which is actively breaking; (3) **verification discipline** — hermetic testing and coverage gates to prevent regressions.

---

## 5. Bugs & Stability

### Critical / P0

- **#6786** (OPEN) — *Gemini provider returns 400 on every tool call.* Empty `type` in `functionDeclarations` breaks all tool usage. **No fix PR yet.**  
  URL: [Issue #6786](https://github.com/nearai/ironclaw/issues/6786)

- **#6880** (OPEN) — *Gemini OAuth provider also returns 400s on tool calls.* Tool schemas bypass `shape_tool_schema` entirely. **No fix PR yet — likely related to #6786.**  
  URL: [Issue #6880](https://github.com/nearai/ironclaw/issues/6880)

- **#6815** (CLOSED) — *Turn-state store latches degraded forever after write-behind flush failure.* Required manual restart on QA deploy. **Fix PR unknown; issue closed.**  
  URL: [Issue #6815](https://github.com/nearai/ironclaw/issues/6815)

- **#6805** (CLOSED) — *Instance returns `service_unavailable` every ~30 min on Railway.* Affected all functions intermittently. **Fix PR unknown; issue closed.**  
  URL: [Issue #6805](https://github.com/nearai/ironclaw/issues/6805)

### High / P1

- **#6790** (OPEN) — *Restart during pending Codex device authorization blocks WebUI and hides recovery code.* Startup race condition. **No fix PR yet.**  
  URL: [Issue #6790](https://github.com/nearai/ironclaw/issues/6790)

- **#6879** (OPEN) — *Automation runs execute as plain interactive chat turns instead of unattended runs.* Structural pipeline defect, not model noise. **No fix PR yet.**  
  URL: [Issue #6879](https://github.com/nearai/ironclaw/issues/6879)

- **#6720** (CLOSED) — *Task runs indefinitely; stop button fails to cancel.* Smoke test ran 15+ minutes; UI shows "Couldn't stop this run." **Fix PR unknown; issue closed.**  
  URL: [Issue #6720](https://github.com/nearai/ironclaw/issues/6720)

### Medium / P2

- **#6348** (CLOSED) — *Gmail extension auto-authorized after reinstall without OAuth prompt.* Security concern — user consent bypassed. **Fix PR unknown; issue closed.**  
  URL: [Issue #6348](https://github.com/nearai/ironclaw/issues/6348)

- **#6806** (CLOSED) — *Automations output not shown in web chat — must navigate to automations page.* UX gap. **Fix PR unknown; issue closed.**  
  URL: [Issue #6806](https://github.com/nearai/ironclaw/issues/6806)

- **#5712** (CLOSED) — *tool_search discloses full capability catalog under narrowed CapabilityAllowSet.* Information disclosure via `ToolDisclosureCapabilityPort`. **Fix PR unknown; issue closed.**  
  URL: [Issue #5712](https://github.com/nearai/ironclaw/issues/5712)

### Test Infrastructure Issues

- **#6887** (OPEN) — *`ironclaw_reborn_composition` test suite intermittently red under parallelism.* Timeout contention, not code defect — but flaky CI is a reliability concern. **No fix PR yet.**  
  URL: [Issue #6887](https://github.com/nearai/ironclaw/issues/6887)

---

## 6. Feature Requests & Roadmap Signals

**Strong roadmap signals visible today:**

1. **Attested signing (8-part series, groups 4–8 open)** — A massive coordinated feature for Ledger clear-signing, multi-tenant isolation, KMS integration, and trust registration. Likely targeting **v1.0 release** given the ship-gate language in PR #6813.

2. **Hermetic testing platform (#6524)** — Epic for fully automated, deterministic coverage of every capability and journey. The WS9/WS10/WS11/WS12 CI PRs (#6881, #6884, #6886, #6889) are concrete implementations of this vision.

3. **WebUI workspace refactor (#6836)** — New contributor achalvs is building `@ironclaw/ui` as a proper workspace design system. Signals **WebUI maturing toward beta/GA**.

4. **TLS termination for sandbox egress (#6740)** — Security infrastructure for sandbox networking. Part of the W6 phase.

5. **Runtime presets (#3045, closed) + developer profiles (#3044, closed)** — Already implemented; expected in next release as core UX improvement.

**Prediction:** The next release (likely 1.0.0-rc.2 or similar) will include the composition refactoring, WebUI streaming fix, runtime presets, and possibly the first signed transaction flows. The Gemini provider bugs are **blockers** that must be fixed before any RC.

---

## 7. User Feedback Summary

**Real pain points surfaced:**

- **Gemini provider is broken** (#6786, #6880) — Users cannot make any tool calls. This likely affects anyone using Gemini as their LLM backend. No workaround documented.
- **Automations are unreliable** (#6879, #6806) — Runs execute as interactive chats; output hidden from main chat. Structural pipeline defect undermines the core "automation" use case.
- **Turn-state store can degrade permanently** (#6815) — Requires restart, no self-healing. Service reliability concern for self-hosters.
- **Gmail auto-authorization** (#6348) — Security UX failure: reinstalling extension silently re-grants access without OAuth. Undermines trust in consent model.
- **Flaky test suite** (#6887) — Intermittent timeouts in composition tests erode confidence in CI.

**Satisfaction signals:**

- **WebUI streaming fix** (#6876) — Directly addresses user experience complaints about choppy/interrupted output.
- **Composition refactoring** (#6691) — 9,421 lines removed suggests maintainability is improving, which benefits contributors.
- **Coverage gates** (#6889, #6881) — Community values deterministic quality assurance.

---

## 8. Backlog Watch

**Important issues/PRs needing attention:**

| Item | Days Open | Status | Concern |
|------|-----------|--------|---------|
| #5712 — `tool_search` capability disclosure | 24 days | CLOSED but fix unclear | Information disclosure vulnerability; verify the fix is complete |
| #5598 — Release PR | 27 days | OPEN, no merge | Blocking all versioned releases; breaking changes in `ironclaw_common` and `ironclaw_skills` must be resolved |
| #3964 — Attested signing PR4/10 (original) | 67 days | OPEN, rebased | 1,184 commits behind; risk of bitrot despite rebase |
| #3577 — v1 channel port tracking | 78 days | OPEN | Telegram port (#3581) is closed, but other legacy channels (Discord, Slack, WhatsApp) still need porting |
| #6887 — Flaky composition tests | 1 day | OPEN | New issue, but if unaddressed will cause CI noise |

**Longest-standing open issues (no recent update):**

- **#3577** (79 days) — Legacy channel porting tracker. Low activity suggests channels are deprioritized behind the Reborn kernel and signing work.
- **#3964** (67 days) — Original attested signing PR. Still alive after massive rebase; coordination with the new 8-part stack is unclear.

---

*Generated from IronClaw GitHub data on 2026-07-30. All links: https://github.com/nearai/ironclaw*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-30

## 1. Today's Overview
The project is in a **high-output stabilization phase** following the **2026.7.24 release** (PR #2407). In the last 24 hours, **13 pull requests were merged or closed**, with only **2 open PRs** remaining (a dependency bump and a stale bugfix). No new issues were opened, and no new releases were cut. The team is focusing on polishing the **cowork (side chat)** subsystem, fixing UI regressions, and reverting a problematic feature in the `openclaw` module. Overall project health is strong, with rapid issue resolution and active maintenance.

## 2. Releases
**No new releases today.** The most recent release is **2026.7.24** (PR #2407, merged yesterday), which bundles all fixes listed below.

## 3. Project Progress (Merged/Closed PRs Today)
The following 13 PRs were merged or closed in the last 24 hours:

### Cowork / Side Chat Improvements (4 PRs)
- **#2406** — `fix(cowork): improve side chat input handling`  
  Accumulates selected text excerpts while panel is open, removes product-level question length limit, retains bounded context and transport safety checks.
- **#2405** — `feat(cowork): add selected text tags to side chat`  
  New feature: selected text shown as removable side-chat context; supports direct sending, follow-up editing, with state safeguards and tests.
- **#2376** — `fix(cowork): render export modal above sidebar`  
  Fixes z-index stacking conflict by mounting export options modal via a body portal.
- **#2364** — `fix(cowork): prevent scroll jumps on session refresh`  
  Scopes refresh events by session ID and preserves loaded message history.

### Cowork Stability (2 PRs)
- **#2363** — `fix(cowork): prevent periodic IM message flicker`  
  Compares matching history windows during reconciliation; preserves older messages when repairing gateway tail mismatches.
- **#2346** — `fix(cowork): open email diagnostics in a new chat`  
  Prevents stale history or IM sessions from overriding new diagnostic chats.

### Authentication (1 PR)
- **#2360** — `fix(auth): preserve local callback across login retries`  
  Reuses active callback server for repeated and concurrent login attempts; adds safe lifecycle diagnostics and regression coverage.

### UI Polish (2 PRs)
- **#2355** — `fix(window): align Windows caption button hover colors`  
  Matches minimize/maximize hover states with sidebar using theme-aware surface colors.
- **#2347** — `chore(updater): reduce automatic update check interval`  
  Changed from 12 hours to 2 hours.

### OpenClaw Module (2 PRs)
- **#2404** — `Refactor/kimi k3 auto only compat`  
  Compatibility refactoring for Kimi K3 (auto-only mode).
- **#2403** — `revert(openclaw): remove run-safety-contract gate for no-progress token burn`  
  **Reverts** the Run Safety design from PR #2400 due to release-blocking issues (receipt identity keying, false-success followups, compaction runId handling, byte-accounting mismatches). DeepSeek cache probe spec updated accordingly.

### Cache & Scheduled Tasks (2 Stale PRs Closed)
- **#1322** — `fix(cowork): true LRU eviction for LLM memory judge cache`  
  Fixes documented-LRU-but-actually-Map-insertion-order eviction. Cache hits now re-order entries, preventing hot keys from being evicted first.
- **#1232** — `fix(scheduledTask): 定时任务首次执行结果不推送到 UI`  
  Fixes a long-standing bug where the first scheduled task execution never pushed results to the UI (Chinese description: scheduled task first-run result not pushed to UI).

## 4. Community Hot Topics
- **#1277 [OPEN]** — `chore(deps-dev): bump the electron group`  
  Bumps Electron from `40.2.1` to `43.2.0` and `electron-builder`. Minor activity; this is a routine dependency update.
- **#2403 [CLOSED]** — Revert of Run Safety feature. Generated significant review discussion (multiple release-blocking issues identified). The underlying need is maintaining **token economy correctness** without introducing regressions.
- **#1322 [CLOSED]** — LRU cache fix. Closed after 3+ months open; community/users likely impacted by stale cache eviction in cowork memory judge.

## 5. Bugs & Stability
| Severity | Bug / Issue | Fix Status |
|----------|-------------|------------|
| **High** | **Run Safety feature (PR #2400) introduced release-blocking bugs:** receipt identity keying, false-success followups, compaction runId handling, byte-accounting mismatches | **Reverted today** in PR #2403 |
| **Medium** | Periodic IM message flicker in cowork | Fixed in #2363 |
| **Medium** | Scroll jumps on session refresh in cowork | Fixed in #2364 |
| **Low** | Scheduled task first-execution results not pushed to UI | Fixed in #1232 (closed after 3 months) |
| **Low** | LLM memory judge cache not using true LRU eviction | Fixed in #1322 (closed after 3 months) |
| **Debug** | Windows caption button hover color mismatch | Fixed in #2355 |

No new bugs were reported today.

## 6. Feature Requests & Roadmap Signals
- **Selected text as removable context in side chat** (PR #2405) is now live. This directly enables richer multi-turn cowork interactions.
- **Refactoring for Kimi K3 auto-only compatibility** (PR #2404) suggests ongoing integration with the Kimi model ecosystem.
- **Run Safety revert** (#2403) signals that token burn/accounting features are still in design phase and not yet ready for release.
- **Electron upgrade to v43** (PR #1277) will bring security updates and new API support in the next release.

## 7. User Feedback Summary
No new user feedback or issues were filed in the last 24 hours. Based on the fixes:
- **Pain point addressed:** Cowork side chat input handling (text accumulation, length limits, context retention) — PR #2406/#2405
- **Pain point addressed:** Cowork export modal hidden behind sidebar — PR #2376
- **Pain point addressed:** Stale/missing first scheduled task execution output — PR #1232
- **Satisfaction signal:** Rapid fix cycle (multiple fixes per day) suggests the team is responsive to reported issues.

## 8. Backlog Watch
- **PR #1277 [OPEN]** — Electron dependency bump (updated 2026-07-29, still open). Unmerged for ~4 months. Risk: version drift, security patches not applied. Awaiting review/merge.
- **PR #1232 [CLOSED]** — Scheduled task bugfix closed today after 3+ months open. Resolution was long-overdue but finally addressed.
- **No Issues are open or backlogged** — the issue tracker currently has **0 open issues**, which is unusual. This may indicate issues are tracked elsewhere or community contribution is low.

**Maintainer attention needed:** PR #1277 (Electron v40→v43 upgrade) should be merged soon to keep dependencies current.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for **2026-07-30**.

---

## Moltis Project Digest – 2026-07-30

### 1. Today's Overview
The project remains active, with **zero new issues** but **five pull requests updated** in the last 24 hours. The maintainer team is focused on integrating production-grade **observability infrastructure** and **access control hardening**. Two PRs were merged/closed, signaling forward momentum on the PWA notification system and the ACP protocol adapter. No new releases were published today, but the dense feature work suggests a release candidate may be imminent.

### 2. Releases
**None.** No new releases were published.

### 3. Project Progress
Two PRs advanced to closure today, both merged:
- **#1173 [CLOSED] – feat(pwa): make push notifications reliable and non-disruptive**  
  *(Author: penso, merged)*  
  Delivers reliable, privacy-safe push notifications for the Progressive Web App. Key improvements: re-alerts for new messages in the same conversation without losing prior counts, generic privacy-safe titles, stripping of rich formatting, and cross-tab unread badge state.  
  [View PR #1173](https://github.com/moltis-org/moltis/pull/1173)

- **#1169 [CLOSED] – feat(acp): expose Moltis as an ACP agent over stdio**  
  *(Author: penso, merged)*  
  Implements the `moltis acp` command, exposing the entire agent as an Agent Communication Protocol (ACP) agent over stdio. Includes session isolation, bounded concurrency, prompt/history/output limits, and deterministic final-text reconciliation. This is a major step toward interoperable AI agent ecosystems.  
  [View PR #1169](https://github.com/moltis-org/moltis/pull/1169)

### 4. Community Hot Topics
The three open PRs are the primary focus of attention today. While none have received upvotes or comments yet, they represent the most active areas of development:

- **#1174 [OPEN] – Add instrumentation and feedback collection infrastructure**  
  *(Updated: 2026-07-30)*  
  A large infrastructure PR adding backend-neutral agent instrumentation, Langfuse v4 export support, OTLP backends, and end-user reaction feedback. This signals a strong push toward production observability and human-in-the-loop feedback.  
  [View PR #1174](https://github.com/moltis-org/moltis/pull/1174)

- **#1166 [OPEN] – feat(slack): per-message acknowledgment reactions, phases, reconnect supervision**  
  *(Updated: 2026-07-30)*  
  Extends the recent ack-reaction feature (#1165) with safety guarantees under queueing, cancellation, retries, callback bursts, and delivery failures.  
  [View PR #1166](https://github.com/moltis-org/moltis/pull/1166)

- **#1170 [OPEN] – fix(channels): gate /sh and privileged tools behind a per-account operators list**  
  *(Updated: 2026-07-30)*  
  Addresses a security gap where channel senders who passed the access allowlist could reach privileged commands/host tools. Introduces a separate per-account `operators` list to enforce privilege boundaries.  
  [View PR #1170](https://github.com/moltis-org/moltis/pull/1170)

### 5. Bugs & Stability
**No new bugs, crashes, or regressions were reported today.** The only security-related work is the proactive access-control hardening in PR #1170 (gate privileged tools behind an operator list), which is an active fix PR still open for review.

### 6. Feature Requests & Roadmap Signals
No explicit user feature requests were filed. However, the current development trajectory points to several expected next features:
- **Production observability** (PR #1174) – Likely to land in the next release, enabling Langfuse and OTLP backends.
- **ACP protocol support** (PR #1169, already merged) – Expected to be included in the next release, opening interoperability with other ACP agents.
- **Slack reliability upgrades** (PR #1166) – Per-message lifecycle and reconnect supervision for Slack bots.

### 7. User Feedback Summary
**No new user feedback was recorded today** (no issues, no comments on PRs, no reactions). The project appears to be in a development-heavy phase, with the maintainer (penso) driving all current activity. No pain points or satisfaction signals are available.

### 8. Backlog Watch
**No long-unanswered issues or PRs require maintainer attention.** The issue tracker is currently empty (0 open issues), and all four open PRs have been updated within the last 4 days. The project backlog is healthy and actively managed.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-30

## Today’s Overview
Project activity remains high with 25 issues and 50 PRs updated in the last 24 hours, though **no new release** was published. The open/active issue count of 21 indicates sustained bug triage pressure, while 13 PRs merged/closed signal steady forward progress. Community engagement is robust, particularly around UI/UX regressions (session integrity, input occlusion) and MCP connectivity reliability. Several repeat contributors (e.g. `RerankerGuo`, `axelray-dev`) are driving focused bug fix cycles, suggesting a maturing contributor base. Overall health is **moderate-high** — active fixing offsets pointed regressions in v2.0.1.

## Releases
**None** in this period. The last known release remains **QwenPaw v2.0.1**.

## Project Progress
**13 PRs closed/merged** in the last 24h, representing progress across multiple domains:

| Domain | PRs | Key Changes |
|--------|-----|-------------|
| Providers | #6479 (merged) | Sync MiniMax model baseline with official platform lineup |
| Token accounting | #6522 (open) | Preserve dirty flag on token usage flush failure — fix for #6374 |
| Mission mode | #6523 (open) | Quote-aware argument parsing for `/mission --verify` commands |
| MCP reliability | #6540 (open) | Last-mile tool‑message sanitizer before every model call (#6407 fix) |
| Queue management | #6539 (open) | Race condition fix in UnifiedQueueManager idle cleanup |
| MCP tool naming | #6561 (open) | Ensure exposed MCP tool names start with a letter (Kimi 400 fix) |
| ACP protocol | #6531 (open) | Add `models` field to `new_session` response (#6529 fix) |
| Matrix/encryption | #6486 (open) | Probe `vodozemac` E2EE backend for Python 3.12 support (#6476 fix) |
| CloudPaw mission | #6535 (open) | Accept `verification_instructions` kwarg in mission patch (#6533 root cause) |
| Browser security | #6500 (open) | Make unauthenticated local CDP exposure opt-in |
| Sandbox | #6383 (open) | Add unelevated sandbox for Windows |
| Computer use | #6424 (open) | Native desktop GUI automation (accessibility‑first + Tauri control) |
| Creator plugin | #6556 (open) | Checkpoints, home redesign, media recovery, export/import, bilingual guide |
| CI/test quality | #6102, #6103 (open) | Boundary meta‑test for #5813 failure modes; frontend coverage thresholds raised |

**Note:** Most day's work is still in open PRs — next few days will show how many merge.

## Community Hot Topics
| Issue/PR | Comments | Topic | Underlying Need |
|----------|----------|-------|-----------------|
| [#6537](https://github.com/agentscope-ai/QwenPaw/issues/6537) | 9 | Skill tags lost on restart (regression of #3270) | **Configuration persistence regression** — tags saved to disk but not reloaded on manifest reconciliation |
| [#6460](https://github.com/agentscope-ai/QwenPaw/issues/6460) | 4 | High CPU in single Edge+Wayland tab (large result set + WebSocket) | **Rendering pipeline CPU thrashing** — large session data + streaming pushes causing persistent high load |
| [#6542](https://github.com/agentscope-ai/QwenPaw/issues/6542) | 3 | Crash → total session history loss, suggest auto‑save | **Catastrophic data loss in crash** — users need real‑time checkpointing, not just JSONL logging |
| [#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524) | 3 | MCP session not auto‑recovered on server restart | **Resilience gap** — client sticks to stale `mcp-session-id` instead of re‑establishing connection |
| [#6056](https://github.com/agentscope-ai/QwenPaw/issues/6056) (closed) | 3 | Background offload kills subprocess immediately | **Process lifecycle bug** — timeout parameter from LLM silently ignored, subprocess killed prematurely |

**Pattern:** Users are experiencing **regression pain in v2.0.1** — persistence bugs (#6537), MCP session recovery (#6524), and silent data loss (#6542) all surfaced after the last release. The community strongly values deterministic, recoverable state.

## Bugs & Stability
### Critical severity
- **Skill tags disappear on restart** ([#6537](https://github.com/agentscope-ai/QwenPaw/issues/6537)) — v2.0.1 regression. Tags saved via API but lost during startup manifest reconciliation. **No fix PR yet.**
- **Session permanently blocked when shell command exceeds coordinator deadline** ([#6245](https://github.com/agentscope-ai/QwenPaw/issues/6245), closed) — regression from #6056 fix. All subsequent messages queue indefinitely until restart. *Assuming fix merged.*
- **NSIS installer infinite loop** ([#6534](https://github.com/agentscope-ai/QwenPaw/issues/6534)) — Windows installer matches itself as "still running" → install impossible. **No fix PR yet.**

### High severity
- **MCP backend restart → client not auto‑recovering** ([#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524)) — stale `mcp-session-id` blocks tool queries. **No dedicated fix PR yet.**
- **MCP tool names starting with `-` cause LLM API 400** ([#6557](https://github.com/agentscope-ai/QwenPaw/issues/6557)) — strict providers (Kimi) reject invalid function names. **Fix PR [#6561](https://github.com/agentscope-ai/QwenPaw/pull/6561) open.**
- **DeepSeek model error — `[context compressed]` uses role=user** ([#6541](https://github.com/agentscope-ai/QwenPaw/issues/6541)) — scroll strategy injects wrong role, causing API rejection. **No fix PR yet.**
- **CI blocks all fork PRs** ([#6563](https://github.com/agentscope-ai/QwenPaw/issues/6563)) — `real-behavior-proof.yml` fails on every fork PR. **No fix PR yet.**
- **`/mission` command TypeError** ([#6533](https://github.com/agentscope-ai/QwenPaw/issues/6533)) — CloudPaw patch missing `verification_instructions`. **Fix PR [#6535](https://github.com/agentscope-ai/QwenPaw/pull/6535) open.**

### Medium severity
- **Chinese path URL‑encoding in Feishu channels** ([#6510](https://github.com/agentscope-ai/QwenPaw/issues/6510)) — path construction bug. **No fix PR yet.**
- **ACP `new_session` response missing models field** ([#6529](https://github.com/agentscope-ai/QwenPaw/issues/6529)) — external clients can't discover models. **Fix PR [#6531](https://github.com/agentscope-ai/QwenPaw/pull/6531) open.**
- **MiniMax model lists outdated/drifted** ([#6479](https://github.com/agentscope-ai/QwenPaw/pull/6479), merged) — already fixed.
- **MiniMax context‑window metadata missing** ([#6554](https://github.com/agentscope-ai/QwenPaw/issues/6554)) — 1M‑token model falls back to 128k default. **Fix PR [#6554](https://github.com/agentscope-ai/QwenPaw/pull/6554) open.**

### Minor/UI
- **Input box occluded in Desktop App** (#6549, #6547) — cursor misplacement, scroll‑to‑see send button.
- **Audio messages silently fail transcription in Feishu** (#6544) — whisper_api config broken.
- **Dream/memory compression window bug** (#6555) — early‑session events lost if compressed before daily MD generation.

## Feature Requests & Roadmap Signals
| Request | Issue | Likely for Next Version |
|---------|-------|------------------------|
| **Auto‑save checkpointing** (#6542) — dialog crash recovery | [Link](https://github.com/agentscope-ai/QwenPaw/issues/6542) | **Highly likely** — data loss is critical pain point; expect a built‑in periodic checkpoint mechanism |
| **`notice_after_complete` tool** (#6475) — agent queues long task, replies to other user questions | [Link](https://github.com/agentscope-ai/QwenPaw/issues/6475) | **Possible** — aligns with agentscope's orchestration theme; could land as built‑in tool |
| **QQ channel streaming output** (#6421) — typed‑text effect | [Link](https://github.com/agentscope-ai/QwenPaw/issues/6421) | **Moderate** — existing channels already support streaming; QQ is a notable gap |
| **Chat session UX improvements** (#6560) — copy, undo, stop, mission mode, scrolling, context transfer | [Link](https://github.com/agentscope-ai/QwenPaw/issues/6560) | **Possible partial** — high user visibility; likely incremental rollouts |
| **Multiple session data integrity issues** (#6558) — messages lost on switch, instructions drift, re‑renders | [Link](https://github.com/agentscope-ai/QwenPaw/issues/6558) | **Highly likely** — core UI stability; blockers for daily use |
| **Unwanted session forking** (#6559) — no parent‑child grouping | [Link](https://github.com/agentscope-ai/QwenPaw/issues/6559) | **Possible** — tree‑style session list could appear as a console enhancement |

**Top candidate for v2.0.2:** Auto‑save checkpointing (#6542) and the DeepSeek context compression role bug (#6541), both critical severity with clear paths to fix.

## User Feedback Summary
**Satisfaction signals:**
- The **computer use** PR (#6424) and **Creator plugin** (#6556) represent ambitious feature additions that align with advanced user workflows (desktop automation, media‑rich creation).
- **Multiple first‑time contributors** (#6479, #6312, #6486, #6531, #6562) are successfully submitting PRs — a healthy onboarding signal.

**Dissatisfaction/pain points:**
- **v2.0.1 regressions are eroding trust** — users explicitly call out "regression of #3270" (#6537), "regression from #6056 fix" (#6245), and "was working before" patterns.
- **Silent data loss is the #1 emotional trigger** — "catastrophic", "不可恢复的丢失" (unrecoverable loss), "permanently blocked" appear in multiple reports.
- **Windows installer UX is broken** (#6534) — users cannot even install, a critical onboarding failure.
- **UI/UX confusion is loud** — "输入框被遮挡，发送按钮需要滚动" (input occluded, send button needs scrolling), cursor floating, messages disappearing on switch — these degrade daily experience even if not fatal.
- **Cross‑platform ecosystem gaps** — QQ streaming support, Feishu Chinese path handling, Wayland CPU issues show incomplete platform coverage.

**Underlying sentiment:** Users love QwenPaw's ambition but are **frustrated by the pace of regression fixes in v2.x**. The overall tone is constructive — users provide detailed reproduction steps and even offer workarounds — but patience may thin if the installer bug (#6534) and session data loss (#6542) aren't resolved in the next patch.

## Backlog Watch
| Item | Age | Priority | Reason for Watch |
|------|-----|----------|------------------|
| [#6537](https://github.com/agentscope-ai/QwenPaw/issues/6537) — Skill tags disappear on restart | 2 days | **Critical** | v2.0.1 regression affecting production use; 9 comments, no fix yet |
| [#6534](https://github.com/agentscope-ai/QwenPaw/issues/6534) — NSIS installer infinite loop | 2 days | **Critical** | Blocks all Windows installations |
| [#6563](https://github.com/agentscope-ai/QwenPaw/issues/6563) — CI blocks fork PRs | 1 day | **High** | Halts all external contributions; some improvement via #6535 patch |
| [#6460](https://github.com/agentscope-ai/QwenPaw/issues/6460) — High CPU in Edge+Wayland | 5 days | **High** | Persistent resource waste; may be hard to repro |
| [#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524) — MCP session not auto‑recovered | 2 days | **High** | MCP reliability gap; users report production impact |
| [#6440](https://github.com/agentscope-ai/QwenPaw/issues/6440) — Unknown (no link provided) | N/A | **Medium** | Not enough data; flag for maintainer review |
| [#6529](https://github.com/agentscope-ai/QwenPaw/issues/6529) — ACP missing models field | 2 days | **Medium** | Has open fix PR #6531 — needs review/merge |
| [#6541](https://github.com/agentscope-ai/QwenPaw/issues/6541) — DeepSeek context compression role | 1 day | **High** | Affects DeepSeek users; a single‑line fix likely |

**Maintainer attention needed:** #6534 (installer) and #6563 (CI fork block) are the two highest‑impact items requiring immediate maintainer intervention — one blocks all Windows users, the other blocks all external contributors. #6537 (skill tags) has the most community attention (9 comments) and needs a root‑cause fix.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-30

## Today's Overview

ZeroClaw is in an **intense phase of architectural expansion**, with 50 issues and 50 PRs updated in the last 24 hours reflecting a project moving from core stability toward major capability additions. The maintainer queue (tracker #8692) is under pressure with 39 active issues, many RFCs requiring decisions on foundational architecture changes. Activity is characterized by a **high concentration of RFC-driven design discussions** (6+ major RFCs active) and a healthy mix of bug fixes, with 11 issues closed and 6 PRs merged/closed yesterday. The project appears to be processing significant technical debt from rapid feature growth, particularly around memory separation, plugin architecture, and security hardening. **No new releases were cut today**, indicating the team may be consolidating before a planned release.

## Releases

**None.** No new releases in the last 24 hours.

## Project Progress

**Merged/closed PRs (6 total):**

- **#9542** (`docs(security): document untrusted review input`) — Security documentation for AI PR-review hardening, addressing prompt injection risks from untrusted GitHub content.
- **#9495** (`fix(channels): resolve aliases for one-off sends`) — Bug fix for `zeroclaw channel send` failing to resolve dotted alias identifiers.
- **#9469** (`fix(runtime): scope peer-agent turns to the recipient's cost context`) — Critical fix for peer-agent cost accounting where detached tasks lost their parent's cost context.
- **#9508** (`[Feature]: Harden AI PR-review skills against prompt injection`) — Security enhancement documentation.
- **#8810** (`[Bug]: Documentation is wrong - Telegram example`) — Documentation correction.
- **#7269** (`bug(docs): clean up docs build warning noise`) — Cleanup of rustdoc/mdBook build warnings.

**Key advances visible in open PRs:**
- The **goal controller system** (#8687, #8689) continues maturing, adding Rust-side goal admission, verifier completion gate, and channel `/goal` command support across Telegram, Matrix, WhatsApp.
- **SOP (Standard Operating Procedure) fan-in architecture** (#9203, #9205) is being wired with authenticated HTTP endpoints and centralized ingress adapters.
- **Telegram long-poll reliability** (#9314) is being hardened to prevent message loss on download failures.
- **Delegate tool fallback configuration** (#9544) is being fixed to honor provider routing/retry/fallback settings.

## Community Hot Topics

**Most active discussions (by comment count):**

1. **#9048** (11 comments) — *RFC: Separate conversation history from agent-curated long-term memory* — High interest in unpicking the memory architecture. Users and contributors recognize that mixing conversation logs with curated memory is causing lifecycle and performance issues. This RFC is foundational to many downstream features.

2. **#9127** (9 comments) — *RFC: Abstract a `KeySource` trait for master-key material* — Security-focused discussion on making credential encryption deployment-aware. The 93 secret-annotated fields and 59 credential-class fields need a pluggable key-source abstraction for different deployment scenarios (KMS, file, env).

3. **#4830** (7 comments, CLOSED) — *HMAC tool execution receipts for hallucination detection* — Closed proposal for cryptographic receipts on tool outputs, enabling runtime verification of output authenticity.

4. **#9106** (6 comments) — *RFC: A2A outbound client (A2ATool)* — Agent-to-Agent outbound calling is a major capability gap. Community wants ZeroClaw agents to proactively call external A2A-compliant agents, not just receive inbound connections.

5. **#8603** (6 comments) — *RFC: OpenAI Chat Completions compatibility adapter* — Strong demand for OpenAI API compatibility to enable integration with Open WebUI, LobeChat, and custom clients that speak the OpenAI protocol.

**Underlying needs:** The community is asking for **interoperability** (OpenAI API, A2A protocol), **architectural clarity** (memory separation, attachment handling), and **security hardening** (key management, prompt injection defenses).

## Bugs & Stability

**High-severity bugs reported today (ranked by risk):**

| Issue | Severity | Summary | Fix PR Exists? |
|-------|----------|---------|----------------|
| #9486 | S3 (minor) | **High-entropy detector redacts Solana wallet addresses** — `high_entropy_tokens=false` doesn't work on channel path | No |
| #9506 | S2 (degraded) | **Email channel cannot preserve CC recipients** — Cannot represent or forward CC lists; Reply All broken | No |
| #9340 | S1 (blocked) | **CLI-created cron jobs discard all output** — `delivery.mode` hardcoded to "none" | No |
| #9186 | S1 (blocked) | **MCP stdio: response ID mismatch, 30s hard timeout vs tool budget** — CLOSED, three interacting defects | Yes (closed) |
| #9462 | S3 (minor) | **Plugin unit tests never execute in CI** — Feature gate mismatch | No |

**Key stability concerns:**
- **MCP stdio timeout** (#9186) was the most critical bug recently (S1), now closed with fix — the 30s hard timeout conflicted with 180-600s tool budgets.
- **Cron output delivery** (#9340) remains a serious UX bug where all scheduled agent jobs silently discard results.
- **High-entropy detector over-sensitivity** (#9486) breaks legitimate use cases like sharing cryptocurrency wallet addresses.
- **Email channel limitations** (#9506) are a basic missing capability for email-based workflow automation.

## Feature Requests & Roadmap Signals

**Likely candidates for next release:**

1. **Memory architecture split** (#9048, #9103) — The RFCs are well-developed and address a recognized bottleneck. Separating conversation history from curated memory and making enrichment connectors (like Lucid) optional rather than backend-coupled would unblock many downstream improvements.

2. **OpenAI compatibility adapter** (#8603) — High community demand, already has an in-progress RFC. Would significantly expand ZeroClaw's integration ecosystem.

3. **A2A outbound client** (#9106) — Completes the Agent-to-Agent story (inbound already shipped in v0.8.2). Critical for multi-agent collaboration use cases.

4. **Runtime-owned conversation sessions** (#9487) — Makes runtime the sole owner of session lifecycle, turning channels into pure transport adapters. This is a major architectural cleanup that would improve consistency and security.

5. **Attachment architecture unification** (#9488) — Currently fragmented across web chat and channels. A unified system would reduce code duplication and edge cases.

**Longer-term signals:**
- **Realtime speech-to-speech** (#8780) for Gemini Live — experimental but indicates interest in multimodal channels.
- **Mixture-of-Agents provider** (#8568) — Virtual model provider that runs parallel model analysis before aggregation.
- **WASM plugin migration** (#8850) — Moving optional channels/tools from compile-time flags to runtime plugins is a multi-month effort already in progress.

## User Feedback Summary

**Pain points:**
- **Configuration complexity surfacing** — Users are hitting edge cases where defaults produce surprising behavior (context compression defaults to enabled but runtime ignores it, #9278; credential-less channel blocks crashloop, #6724).
- **Documentation accuracy issues** — Complaint about incorrect Telegram documentation (#8810, now fixed) suggests users are relying on docs for setup and finding gaps.
- **Missing basic communication features** — Email CC preservation (#9506) is a fundamental workflow blocker for business use.
- **Cron job invisibility** (#9340) — Users creating scheduled jobs have no visibility into whether they work (output silently discarded).

**Satisfaction indicators:**
- High engagement with RFC process — users actively contributing design discussions (NiuBlibing, IftekharUddin, JordanTheJet are regular contributors).
- Solana/crypto community engaging with MCP server integration (#9486), suggesting growing adoption in Web3 use cases.
- Multiple trusted/principal contributors (vrurg, JordanTheJet, IftekharUddin) consistently submitting high-quality PRs, indicating strong community health.

**Use cases visible from issues:**
- **Workflow automation** — cron jobs, SOP execution, email-based agents
- **Multi-agent systems** — A2A collaboration, peer-agent cost accounting
- **Crypto/blockchain** — Solana wallet interactions, high-entropy token handling
- **Enterprise integration** — OpenAI-compatible API, Slack/Telegram/WhatsApp channels

## Backlog Watch

**Issues/PRs needing maintainer attention:**

| Item | Days Since Update | Status | Why Concerning |
|------|-------------------|--------|----------------|
| #6724 | 1 day | Open, priority:p3, risk:high | **Empty credential channel crashloop** — accepted but still open for 75 days with only 4 comments. Risk-rated high but only p3 priority. Needs resolution or priority adjustment. |
| #8692 | 1 day | Open | **Maintainer decision queue tracker** — This is the tracker itself, listing 30+ RFCs awaiting decisions. The backlog of pending maintainer decisions is growing. |
| #8996 | 19 hours | Open, needs-author-action | **Goal preservation across daemon reload** — XL-sized PR with 27+ component labels from a trusted contributor. Critical for production reliability but stalled on author action. |
| #8850 | 1 day | Open | **WASM plugin migration tracker** — Multi-month architectural change with no recent merge activity. Risk of becoming stale if not actively driven. |
| #6864 | 1 day | Open, accepted | **Invert channels→runtime dependency** — Accepted since May 23 but still open. Layer inversion is fundamental to architecture health but has no active implementation PR. |

**Items now overdue (no activity > 7 days):**
*None flagged in the last 24h dataset.* However, the maintainer queue (#8692) has accumulated 30+ items, many older than the data window.

**Mitigating factor:** The high number of `needs-maintainer-review` and `needs-author-action` labels suggests the bottleneck is reviewer capacity, not contributor interest. The influx of large architectural RFCs (memory, plugins, runtime sessions) may be exceeding the maintainer team's bandwidth for thorough review.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*