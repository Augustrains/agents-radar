# OpenClaw Ecosystem Digest 2026-07-03

> Issues: 195 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-03 01:43 UTC

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

# OpenClaw Project Digest — 2026-07-03

## 1. Today's Overview

OpenClaw is in a high-activity maintenance cycle with 195 issues and 500 PRs updated in the last 24 hours. The project is actively triaging a significant bug backlog — 122 open issues remain, many tagged P1 and carrying the "diamond lobster" severity rating. A new beta release (v2026.7.1-beta.1) shipped today adding GPT-5.6 support and external harness attachment. Community engagement is strong, with 73 issues closed and 62 PRs merged/closed in the last day, though the 438 open PRs signal a growing review bottleneck. The overall picture is a mature, heavily used project grappling with reliability regressions across multiple channels and provider integrations.

**Activity Assessment:** Very high. The ratio of open PRs (438) to merged/closed (62) raises concern about review capacity. P1 bug density is elevated, particularly around session state, message loss, and auth-provider issues.

---

## 2. Releases

### Latest: v2026.7.1-beta.1

**Changes:**
- **OpenAI GPT-5.6 support:** OpenClaw now recognizes the GPT-5.6 model family across catalog, capability, and runtime selection paths. (#98333) — Thanks @steipete-oai
- **External harness attachment:** `openclaw attach` now launches an external harness against an existing Gateway session, enabling third-party tooling to interact with live agent sessions.

**⚠️ Migration Notes:**
- No breaking changes documented. Users on previous 2026.6.x releases should be able to upgrade directly (`npm install -g openclaw@latest`).
- GPT-5.6 model selection may require updating model configuration files if using explicit model IDs.

---

## 3. Project Progress

**Merged/Closed Today:** 62 PRs merged/closed

**Key Merged Fixes:**
- **#99296** — `refactor(shared): consolidate gateway and stateful runtime lazy loaders` — Reduces duplicated promise memoizers. Related to #98748.
- **#99276** — `fix(memory-wiki): source imports crash on unreadable pages` — Resolves page-read crashes during retry. Related to #98360.
- **#99294** — `fix(qa): stagger isolated worker startup` — Prevents CPU starvation on CI runners during parallel flow workers.
- **#99252** — Closed as superseded by #99253 (fabricated user turns — see Bugs section)

**Notable Closed Issues:**
- **#98672** — "Sessions breaking constantly" — Closed, suggesting a patch has been applied or identified as duplicate.
- **#91872** — "Android App v2026.5.25 node mode chat.send never reaches Gateway" — Closed, signaling resolution of a cross-version compatibility bug.
- **#99093** — "iOS Voice Wake crash reinstalling mic tap" — Fixed.
- **#99108** — "Render /session_recent as bullet rows with inline code in Telegram" — Closed as implemented.
- **#99120** — "OpenAI OAuth refresh false-green falls back to invalidated external credential" — Fix landed.

**Active PRs Nearing Merge:**
- **#98907** — `fix(telegram): distinguish and render streamed reasoning/commentary progress lanes` — Status "ready for maintainer look" with screenshot proof. This is the fix for the well-known Telegram progress rendering issue.
- **#95738** — `feat(signal): add target aliases` — Ready for maintainer review, addresses a long-standing usability gap for Signal users.
- **#99111** — `fix: recover Control UI bundle loading after gateway restart` — Ready for maintainer.

---

## 4. Community Hot Topics

### Most Active Issues (by comment count)

| Issue | Comments | 👍 | Summary |
|-------|----------|---|---------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) — **Text between tool calls leaks to messaging channels** | 33 | 1 | Agent internal processing output (error handling, acknowledgments) leaks to Slack/iMessage. P1, security-impacting, "diamond lobster" severity. |
| [#88312](https://github.com/openclaw/openclaw/issues/88312) — **Codex app-server turn-completion stall regression** | 19 | 5 | 2026.5.27 regression: multi-tool turns fail with "Codex stopped before confirming turn complete." Affects ChatGPT Plus subscribers. |
| [#92201](https://github.com/openclaw/openclaw/issues/92201) — **Embedded runner: streamed thinking signatures intermittently invalid on replay** | 18 | 1 | Anthropic thinking blocks with invalid signatures; recovery wrapper never fires due to generic error text. |
| [#73148](https://github.com/openclaw/openclaw/issues/73148) — **Image tool: opaque "Failed to optimize image" when sharp not installed** | 14 | 3 | Missing native dependency causes confusing errors and no fallback. |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) — **"Cannot convert undefined or null to object" with google-vertex/gemini** | 10 | 3 | 2026.3.2 regression affecting Google Vertex users. Still open since March. |

### Most Engaged Issues (by reactions)
- **#88312** (5 👍) — Codex turn stall regression — high user impact for ChatGPT Plus users
- **#98416** (5 👍) — v2026.6.11 published dist missing reentrancy guard — caused session initialization conflicts
- **#73148** (3 👍) — Image tool sharp dependency issue — affects many users with non-standard environments
- **#38327** (3 👍) — Google Vertex crash — long-running (since March) with no fix

**Underlying Needs Analysis:**
The community is most vocal about **reliability regressions** after version updates (Codex turns, Anthropic replays, OAuth refresh). There's an emerging theme of **cross-platform inconsistencies** — Telegram vs Discord rendering differences (PR #98907 addresses this), iOS vs Android bugs, and channel-specific behavior. Users express frustration with **opaque error messages** (#73148, #92201) that provide no action path. The #25592 "text leakage" issue represents a fundamental UX/security concern — internal agent processing should never be visible to end users.

---

## 5. Bugs & Stability

### New P1/Critical Bugs Reported Today

| Issue | Channel/Area | Severity | Summary | Fix PR Exists? |
|-------|-------------|----------|---------|----------------|
| [#99253](https://github.com/openclaw/openclaw/issues/99253) | Safety/Core | 🔴 **Critical** | Assistant self-inserted fabricated user turn and answered it as real input. Security concern. | No — new issue |
| [#99183](https://github.com/openclaw/openclaw/issues/99183) | Embedding workers | 🟠 High | Local embedding worker fork fails with ENOENT after Node upgrade — `fork()` inherits `execPath` of deleted binary. | No |
| [#98790](https://github.com/openclaw/openclaw/issues/98790) | Multi-agent | 🟠 High | Concurrent agent-to-agent turn forks session tree; Anthropic rejects "continue from message role: assistant" — permanent transcript poisoning. | No |
| [#99071](https://github.com/openclaw/openclaw/issues/99071) | Codex Apps | 🟠 High | Repeated plugin discovery causing excessive disk I/O during single request (opensnoop/atop confirmed). | No |
| [#98702](https://github.com/openclaw/openclaw/issues/98702) | OAuth/Auth | 🟡 Medium | Inherited OpenAI OAuth rejected at provider for built-in runtime on `openai-chatgpt-responses` transport while main succeeds. | No |

### Regressions Reported Today
- **#98614** — `sessions_spawn` missing scope `operator.write` — regression between v2026.6.1 and v2026.6.11
- **#99252** (closed, superseded by #99253) — Assistant response contained fabricated timestamped user transcript line

### Fixes Landed Today for Previously Reported Bugs
- **#99186** — Tool results with Cyrillic UTF-8 rendered as image attachment in webchat — Closed
- **#99093** — iOS Voice Wake crash reinstalling mic tap — Closed
- **#99120** — OpenAI OAuth refresh false-green falls back to invalidated credential — Closed

### Reliability Concerns
- **Anthropic/Rekognition:** Continuous cluster of issues around thinking signatures (##92201), replay failures after compaction (#98527 has an open fix PR)
- **Telegram streaming:** Multiple PRs in flight (#98907 merged, #90997 closed) addressing progress lane rendering and commentary handling
- **Codex/OpenAI OAuth:** Auth refresh and credential invalidation issues creating cascading failures (#98702, #91352)

---

## 6. Feature Requests & Roadmap Signals

### User-Requested Features (P2/P3, Open)

| Issue | Feature | Priority | Impact |
|-------|---------|----------|--------|
| [#35203](https://github.com/openclaw/openclaw/issues/35203) | Multi-Agent Collaboration Enhancement: Capability Profiling + Shared Blackboard + Layered Memory + Token Cost Governance | P2 | Session State, Security |
| [#32530](https://github.com/openclaw/openclaw/issues/32530) | Auto-discovery of agent configurations from external workspaces | P2 | Session State, Security |
| [#77165](https://github.com/openclaw/openclaw/issues/77165) | Auto-Generate Session Titles via AI Summarization | P3 | Session State |
| [#81084](https://github.com/openclaw/openclaw/issues/81084) | MSTeams channel-bound agents need opt-out from per-thread sessions | P2 | Session State |
| [#48080](https://github.com/openclaw/openclaw/issues/40880) | MEDIA_MAX_BYTES should be user-configurable (currently hardcoded 5MB) | P2 | Security, Message Loss |
| [#75947](https://github.com/openclaw/openclaw/issues/75947) | UI quality update based on UX scoring | P3 | Other |

### Predictions for Next Release (v2026.7.x)

**Likely inclusions:**
1. **Signal reply quotes** — PR #95718 (ready for maintainer) would add native Signal quote context preservation
2. **Signal target aliases** — PR #95738 would allow friendly names like `signal:me` instead of raw phone numbers
3. **Telegram progress lane fixes** — PR #98907 merged today, fixing the long-standing "indistinguishable reasoning and commentary" issue
4. **Control UI recovery** — PR #99111 would prevent the "Control UI did not start" dead state after gateway restart

**Longer-term roadmap signals:**
- The multi-agent enhancement RFC (#35203) has been open since March with 9 comments but no maintainer action — suggests it's considered important but not urgent
- The UI redesign request (#75947) at P3 indicates UX polish is on the radar but lower priority than reliability bug fixes
- Durable runtime wiring (#98719) is an XL PR in progress that could underpin session persistence improvements

---

## 7. User Feedback Summary

### Pain Points
- **"Sessions keep breaking after updates"** — Multiple users report upgrade-related regressions (#98672, #98416). The reentrancy guard fix (#98416) addresses one case, but the pattern of "worked before, now fails" is recurring.
- **"I can't tell what's wrong"** — Opaque error messages (#73148 — "Failed to optimize image" without mentioning `sharp`; #92201 — generic error text masking Anthropic signature issues) frustrate troubleshooting.
- **"Telegram/Discord behave differently"** — The community consistently demands parity across messaging channels (#98907, #90962). Telegram progress rendering is the most complained-about discrepancy.
- **"Multi-agent is unreliable"** — Subagent completion silently dropped (#92433), empty subagent lists (#75593), session tree corruption (#98790).
- **"Auth keeps breaking silently"** — OAuth refresh failures, stale credentials, opaque "authentication needed" states (#98046, #98702, #99120).

### Use Cases (Revealed by Bug Reports)
- **Multi-agent gateways:** Several enterprises running shared gateways with multiple agents, inter-agent traffic, and subagent spawning
- **Codex ChatGPT Plus integration:** Heavy use of Codex app-server for ChatGPT Plus subscribers — this is clearly a primary integration path
- **Cross-platform deployments:** Users running on macOS, Windows, Android, iOS with Tailscale, LAN, or SSH transport
- **International users:** Cyrillic UTF-8 rendering bugs (#99186), Chinese UI feedback (#99046 — iOS Private Access localization in Chinese)
- **Telegram power users:** The channel-specific PRs and issues suggest a substantial Telegram user base

### Satisfaction Indicators
- Rapid issue closure rate (73 closed today) suggests the team is responsive
- User gratitude through 👍 reactions on fix PRs and closed issues
- No "project abandonment" sentiment evident — users are engaged and reporting bugs constructively

### Dissatisfaction Indicators
- Frustration with "permanent" session corruption requiring transcript reset (#98790)
- Confusion about permission requirements on mobile (#99046, #98044, #98046)
- Concern about security boundaries (#99253 — fabricated turns; #25592 — text leakage)

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Status | Why It's Stuck |
|-------|-----|--------|----------------|
| [#38327](https://github.com/openclaw/openclaw/issues/38327) — Google Vertex crash "Cannot convert undefined or null to object" | Since 2026-03-06 (4 months) | `needs-live-repro` | Cannot reproduce consistently. Affects Google Vertex users — growing frustration. |
| [#73148](https://github.com/openclaw/openclaw/issues/73148) — Image tool sharp dependency | Since 2026-04-28 (2+ months) | `stale`, P1 | Tagged stale despite being P1. No fix PR exists. |
| [#35203](https://github.com/openclaw/openclaw/issues/35203) — Multi-Agent Collaboration RFC | Since 2026-03-05 (4 months) | `needs-product-decision` | Comprehensive proposal with no maintainer response. |
| [#32530](https://github.com/openclaw/openclaw/issues/32530) — Auto-discovery of agent configurations | Since 2026-03-03 (4 months) | `needs-maintainer-review`, `needs-product-decision` | No progress despite community interest. |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) — Text between tool calls leaks to channels | Since 2026-02-24 (4.5 months) | Complex, security-impacting | 33 comments, "diamond lobster" rating. Needs product decision. |
| [#11623](https://github.com/openclaw/openclaw/issues/11623) — Floating agent bubbles (Clawi) for macOS | Since 2026-02-08 (5 months) | P3, no action | Feature request with no traction. |

### PRs Stuck in Review

| PR | Age | Status | Blockers |
|----|-----|--------|----------|
| [#41892](https://github.com/openclaw/openclaw/issues/41892) — Control UI cron calendar timeline | Since 2026-03-10 (4 months) | `waiting on author` | Has screenshots but author has been slow to respond. |
| [#96134](https://github.com/openclaw/openclaw/issues/96134) — SSH transport security check fix | Since 2026-06-23 (10 days) | `waiting on author` | Addresses a remote Gateway SSH tunnel issue. |
| [#98990](https://github.com/openclaw/openclaw/issues/98990) — Bound template file cache | 1 day | `waiting on author` | Fresh but needs author adjustment. |

**Overall Backlog Health:** The project has a healthy number of open issues (122) but 438 open PRs indicates a significant review queue. The oldest open P1 issues (4+ months) with no fix traction are a concern — particularly #25592 (text leakage) and #38327 (Google Vertex crash). The `needs-product-decision` tag on several high-impact issues suggests the maintainer team is resource-constrained on product strategy, which may delay roadmap decisions on multi-agent enhancements.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report — 2026-07-03

## 1. Ecosystem Overview

The personal AI assistant open-source landscape continues to mature, with seven projects showing active development today and three dormant. The ecosystem is converging around common challenges: **multi-modal reliability**, **cross-platform channel consistency**, and **enterprise-grade security** (OAuth, credential isolation, secret management). A clear bifurcation is emerging between **general-purpose agent frameworks** (OpenClaw, NanoBot, IronClaw, ZeroClaw) and **specialized assistant implementations** (Hermes Agent, CoPaw, Moltis, PicoClaw, NanoClaw). The community is prioritizing **stability over novelty**, with bug fixes and reliability regressions dominating activity across all active projects. Notably, the GPT-5.6 model support landing in OpenClaw signals the ecosystem's rapid adaptation to frontier model releases.

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today? | Health Score |
|---------|---------------------|-------------------|----------------|--------------|
| **OpenClaw** | 195 | 500 | ✅ (v2026.7.1-beta.1) | 🟡 High activity, review bottleneck |
| **NanoBot** | 97 | 63 | ❌ No | 🟢 High velocity, systematic fix batch |
| **Hermes Agent** | 50 | 50 | ❌ No | 🟢 Healthy, steady throughput |
| **IronClaw** | 23 | 50 | ❌ No | 🟡 High momentum, growing bug debt |
| **ZeroClaw** | 37 | 50 | ❌ No | 🟢 Very high, architectural work |
| **CoPaw (QwenPaw)** | 50+ | 50 | ✅ (v2.0.0-beta.2) | 🟡 Intense dev, stability gaps |
| **PicoClaw** | 2 | 25 | ❌ No | 🟡 Moderate, dependency-driven |
| **NanoClaw** | 4 | 14 | ❌ No | 🟡 Moderate, targeted fixes |
| **Moltis** | 0 | 3 | ❌ No | 🟢 Quiet, focused maintenance |
| **LobsterAI** | 0 | 8 | ❌ No | 🟡 7/8 merged → high merge rate |
| **NullClaw** | 0 | 0 | ❌ No | ⚪ Dormant |
| **TinyClaw** | 0 | 0 | ❌ No | ⚪ Dormant |
| **ZeptoClaw** | 0 | 0 | ❌ No | ⚪ Dormant |

**Health Score Legend:** 🟢 Active/Healthy | 🟡 Moderate/Caution | 🔴 Critical | ⚪ Dormant

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Largest community by volume:** 195 issues + 500 PRs updated in 24h dwarfs all peers (next closest: NanoBot at 97/63). This indicates the largest user base and contribution pipeline.
- **Mature release cadence:** v2026.7.1-beta.1 shipped today with GPT-5.6 support—OpenClaw is consistently first to support new frontier models.
- **Robust cross-platform support:** Explicit issues and fixes across macOS, Windows, Android, iOS, Telegram, Discord, Signal, Slack, iMessage—broader than any competitor.
- **Established governance:** "diamond lobster" severity rating, systematic triage process, dedicated maintainer team.

**Technical Approach Differences:**
- OpenClaw uses a **Gateway → Runtime** architecture with session state management, whereas NanoBot and Hermes favor **monolithic agent processes**.
- OpenClaw's **multi-channel abstraction** is the most mature, with dedicated fix PRs for Telegram (#98907), Signal (#95738), and webchat rendering.
- The **438 open PRs** vs. 62 merged/closed today signals a **review bottleneck** that competitors (NanoBot: 63 PRs updated, 28 merged) do not face to the same degree.

**Community Size Comparison (Proxy: Activity Ratios):**
- OpenClaw: 438 open PRs → largest active contributor pool
- NanoBot: ~35 open PRs → smaller but high-impact contributions
- IronClaw: 29 open PRs → growing, new contributors joining
- ZeroClaw: ~31 open PRs → strong sustained throughput

## 4. Shared Technical Focus Areas

| Focus Area | Projects Affected | Specific Needs |
|------------|------------------|----------------|
| **OAuth/Auth Refresh Stability** | OpenClaw (#98702, #99120), NanoBot (#4632, #4669), IronClaw (#5502, #5576), Hermes (#23944) | False-green auth states, token refresh races, credential invalidation |
| **Multi-Platform Channel Consistency** | OpenClaw (#98907 Telegram vs Discord), NanoBot (#3344 DingTalk, #3166 Feishu), Hermes (#52914 QQBot), ZeroClaw (#8627 WhatsApp) | Progress rendering, file handling, thread support diverging across platforms |
| **Context/Session Persistence Reliability** | OpenClaw (#98672 sessions breaking), CoPaw (#5746 context compression), NanoBot (#4082 cron context reuse), IronClaw (#5527 session scope mismatch) | Session corruption, data leakage between contexts, compaction destroying active state |
| **Opaque Error Messages** | OpenClaw (#73148, #92201), IronClaw (#5552 "invalid result"), Hermes (#52914 infinite retry), ZeroClaw (#8631 silent SOP completion) | Errors without action paths, silent failures, generic text masking root causes |
| **Memory Leak & Resource Exhaustion** | CoPaw (#5720 memory leak on Windows), ZeroClaw (#5542 OOM in WSL2), OpenClaw (#99071 excessive disk I/O) | Unbounded memory growth, process crashes, configuration corruption |
| **Windows Compatibility** | CoPaw (#5720 memory leak), ZeroClaw (#7462 74 test failures), NanoBot (#4511, #4544), Hermes (#57434 install encoding) | Unix-only assumptions, shell inconsistencies, background mode failures |
| **Multi-Tenant Data Isolation** | IronClaw (#5460 memories visible to all), NanoBot (#2836 WhatsApp workspace), OpenClaw (#25592 text leakage) | Cross-user credential/memory leakage, missing role-based access |

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | IronClaw | Hermes Agent | CoPaw (QwenPaw) | ZeroClaw |
|-----------|----------|---------|----------|--------------|------------------|----------|
| **Target User** | Power users, multi-platform | Developer tooling, OSS enthusiasts | Enterprise teams, Slack-first | Desktop-first, individual | Chinese market, Feishu/QQ | CLI/SDK heavy, developer |
| **Architecture** | Gateway + Stateful Runtime | Monolithic agent | Reborn architecture (v1→v2 migration) | Desktop app + gateway | Monolithic + Tauri desktop | Rust core, daemon + RPC |
| **Primary Channels** | Telegram, Discord, Signal, Slack, iMessage, Webchat | DingTalk, Feishu, WeChat, Telegram | Slack (read/write) | Desktop, Telegram, QQ, Signal | Feishu, QQ, Discord | Git forge, WhatsApp, Web |
| **Unique Strength** | Multi-channel parity, fastest model support | Systematic bug sweeps, dream memory | Enterprise OAuth, tool management | Desktop UX, skills/MCP hub | v2.0.0 modern rewrite | SOP engine, wire protocol |
| **Primary Weakness** | PR review bottleneck (438 open) | Stale bugs (3+ months unfixed) | Nightly CI failing (38 days) | UI regressions | v2.0.0 stability gaps | OOM risk (S0, 84 days) |
| **Language** | TypeScript/Node.js | Python | Rust | Python | Python/TypeScript (Tauri) | Rust |
| **Community Language** | English dominant | Chinese + English | English | English | Chinese | English |

## 6. Community Momentum & Maturity

**Tier 1 — High Velocity / Rapid Iteration:**
- **OpenClaw** — Mature but straining under scale. Highest absolute activity, but 438 open PRs vs. 62 merged indicates review capacity is the bottleneck. Beta release ships today.
- **NanoBot** — Highest merge efficiency (28 merged of 63 updated). Systematic bug-sweep (PR #4648 addressing 13 issues) signals disciplined maintenance. No release today—likely building toward one.
- **IronClaw** — Very high feature velocity (Slack OAuth, tool management, design system). However, nightly CI failing for 38 days (#4108) is a **critical infrastructure concern** that undermines confidence.
- **ZeroClaw** — Strong throughput (19 PRs merged today). Architectural work (memory durability, wire protocol refactor) suggests long-term investment. OOM issue (#5542, 84 days open) is a durability red flag.

**Tier 2 — Moderate / Focused Maintenance:**
- **Hermes Agent** — Stable throughput (17 PRs merged). Steady but not breaking new ground. Desktop UX focus.
- **CoPaw (QwenPaw)** — Split between stable v1.1.12 and v2.0.0 beta. v2.0.0 shows promise but has blocker bugs (context compression, infinite loops) that must be resolved before GA.
- **PicoClaw** — Quiet, dependency-driven updates. Two new HIGH-severity bugs (#3203, #3206) with no fix yet—needs maintainer attention.
- **NanoClaw** — Small but focused. Template system and WhatsApp fixes show targeted investment.
- **Moltis** — Very quiet; one significant fix merged (WhatsApp LID addressing). Minimal community engagement.

**Tier 3 — Dormant:**
- **NullClaw, TinyClaw, ZeptoClaw** — No activity in 24h. Likely abandoned or in deep maintenance mode.

**Maturity Index (Subjective):**
1. OpenClaw (most mature, largest ecosystem)
2. Hermes Agent (stable desktop UX)
3. NanoBot (high-quality contributions, growing)
4. IronClaw (high potential, infrastructure risk)
5. ZeroClaw (strong architecture, critical bugs)
6. CoPaw (promising v2.0, pre-GA instability)
7. PicoClaw / NanoClaw / Moltis (niche, low activity)

## 7. Trend Signals

### Emerging Industry Trends from Community Feedback

1. **"Auth is the new bottleneck"** — Across 6+ projects, OAuth refresh races, stale credential detection, and token lifecycle management dominate bug reports. The community is demanding **silent, automatic auth recovery** (OpenClaw #99120, NanoBot #4684, IronClaw #5501). This suggests the agent-as-service model is straining traditional API key authentication.

2. **"Multi-platform is table stakes, not a differentiator"** — Users expect identical behavior across Telegram, Discord, Slack, WhatsApp, and web. Projects that fail at channel parity (OpenClaw's Telegram vs Discord rendering, NanoBot's DingTalk/Feishu gaps, Hermes' QQBot retry loops) face disproportionate user frustration. **Channel consistency is now a hygiene factor**, not a feature.

3. **"Agent-to-agent is the next frontier"** — Multi-agent session tree corruption (OpenClaw #98790), subagent silent drop (OpenClaw #92433), and inter-agent context poisoning (CoPaw #5746) reveal that **agent orchestration at scale is fundamentally broken**. The community is pushing beyond single-agent use cases into multi-agent workflows, and the tools aren't ready.

4. **"Observability debt is accumulating"** — Opaque errors, missing latency metrics (NanoBot #3257), silent failures (ZeroClaw #8631), and generic "invalid result" messages (IronClaw #5552) indicate that **agent monitoring and debugging infrastructure is lagging behind feature development**. Users want OpenTelemetry-grade observability, not "it worked before."

5. **"Memory is a trust issue"** — Data isolation failures (IronClaw #5460, NanoBot #4082), history compaction destroying active state (CoPaw #5746), and text leakage across channels (OpenClaw #25592) signal that **memory management is the #1 trust-eroding problem**. Users fear their data is leaking or being lost.

6. **"Enterprise features are emerging organically"** — RBAC for tools (IronClaw #5459), per-agent environment isolation (ZeroClaw #8226), audit-graded credentials, and SSO integration requests all point to **upward pressure from enterprise deployment**. These are no longer nice-to-haves for teams running agents in shared workspaces.

7. **"Windows remains an afterthought"** — Systematic test failures (ZeroClaw #7462), memory leaks (CoPaw #5720), shell inconsistencies (NanoBot #4544), and install encoding bugs (Hermes #57434) prove that **the ecosystem neglects Windows users**, who represent a significant underserved segment.

### Value for AI Agent Developers

- **Invest in auth infrastructure first** — Token refresh, credential isolation, and silent recovery are the most common failure points. They're unglamorous but block adoption.
- **Build channel abstraction early** — Every project that grew multi-platform support reactively now pays a compounding maintenance tax. Design a channel-agnostic message model from day one.
- **Memory must be durable, scoped, and auditable** — The community is moving from "agents that remember" to "agents that remember *correctly* and *privately*." Treat memory as a security boundary, not a storage optimization.
- **Observability is a feature, not an afterthought** — Users are building complex multi-agent pipelines. Without structured logs, span tracing, and error categorization, debugging is guesswork.
- **Plan for Windows from start** — The Windows user base is vocal and growing. Unix-only assumptions create a community of frustrated, second-class users.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-03

## Today's Overview

NanoBot is experiencing **intense development activity**, with **97 issues** and **63 pull requests** updated in the last 24 hours — marking a high-velocity period for the project. The open/active issue count (94) significantly exceeds closed issues (3), suggesting a growing backlog of reported problems alongside rapid PR throughput. A major coordinated fix batch was submitted by core contributor `hamb1y` today (PR #4648), targeting 13 validated bugs in a single focused PR, signaling a maintainer-led stabilization push. No new releases were cut today, indicating these changes are mid-flight toward a future release. The community is actively contributing both bug reports and feature implementations, with several high-priority PRs addressing security, crash, and compatibility issues.

## Releases

**No new releases today.** The last published release remains unknown; the project appears to be between release cycles with active development on `main`.

---

## Project Progress

**Merged/closed PRs today: 28** — a substantial number, indicating heavy review and merge activity.

### Key Fixes and Features Advancing Today

| PR | Title | Status | Description |
|----|-------|--------|-------------|
| [#4648](https://github.com/HKUDS/nanobot/pull/4648) | Fix validated issue batch | **CLOSED** (Merged) | A massive batch fix addressing 13 validated issues (#4078, #4076, #4075, #4072, #4068, #4064, #4061, #4058, #4055, #4604, #4378, #4544, #4136). This single PR represents a coordinated bug-sweep. |
| [#4666](https://github.com/HKUDS/nanobot/pull/4666) | fix(mcp): contain malformed tool results | OPEN | Fixes crash when MCP tool calls return errors/empty data (#4652). Wraps exceptions gracefully. |
| [#4687](https://github.com/HKUDS/nanobot/pull/4687) | fix(providers): update Anthropic default model | OPEN | Updates default model from `claude-sonnet-4-20250514` to `claude-sonnet-4-6` across codebase. |
| [#4671](https://github.com/HKUDS/nanobot/pull/4671) | fix: pin validated DNS for SSRF checks | OPEN | Security fix: returns validated resolved IPs from SSRF URL validation. |
| [#4685](https://github.com/HKUDS/nanobot/pull/4685) | fix: omit temperature for sonnet 5 | OPEN | Fixes 400 error with `claude-sonnet-5` where `temperature` parameter is rejected. |
| [#4686](https://github.com/HKUDS/nanobot/pull/4686) | feat: support canonical opencode provider | OPEN | Adds official OpenCode Zen provider support. |
| [#4669](https://github.com/HKUDS/nanobot/pull/4669) | fix: require API key for serve | OPEN | Security fix: requires API key before OpenAI-compatible API server starts (#4078). |
| [#4668](https://github.com/HKUDS/nanobot/pull/4668) | fix: enforce message outbound policy | OPEN | Authorization hook for `message` tool; fixes #4076 (outbound recipient authorization). |
| [#4667](https://github.com/HKUDS/nanobot/pull/4667) | fix: protect user skills from dream writes | OPEN | Adds `dream_managed: true` frontmatter guard before Dream can modify skills. |
| [#4673](https://github.com/HKUDS/nanobot/pull/4673) | fix(dream): ground memory audit records | OPEN | Ensures Dream consolidation audit records match actual git diff. |
| [#4684](https://github.com/HKUDS/nanobot/pull/4684) | fix(copilot): guard token refresh with asyncio.Lock | OPEN | Prevents race condition when Copilot access token expires. |
| [#4459](https://github.com/HKUDS/nanobot/pull/4459) | feat: add Mattermost channel support | OPEN | New channel integration for Mattermost via WebSocket + REST API. |
| [#4632](https://github.com/HKUDS/nanobot/pull/4632) | feat(providers): add Anthropic OAuth | OPEN | Enables Claude subscription users to use nanobot without API key. |
| [#4665](https://github.com/HKUDS/nanobot/pull/4665) | fix: preserve pending message runtime context | OPEN | Fixes #4064 — message context for mid-turn pending message injections. |
| [#4664](https://github.com/HKUDS/nanobot/pull/4664) | fix: protect dream history during compaction | OPEN | Fixes #4055 — preserves entries newer than Dream cursor during compaction. |
| [#4663](https://github.com/HKUDS/nanobot/pull/4663) | fix: quarantine invalid tool results | OPEN | Sanitizes missing/empty/duplicate tool result IDs before provider replay. |
| [#4662](https://github.com/HKUDS/nanobot/pull/4662) | fix: normalize text tool call markup | OPEN | Parses plain-text `<tool_call>` markup from OpenAI-compatible providers. |
| [#4661](https://github.com/HKUDS/nanobot/pull/4661) | fix: separate file edit progress ids | OPEN | Corrects file-edit event coalescing in WebUI. |
| [#4659](https://github.com/HKUDS/nanobot/pull/4659) | fix: isolate matrix stream buffers | OPEN | Fixes #4068 — Matrix stream buffer isolation for concurrent streams. |
| [#4670](https://github.com/HKUDS/nanobot/pull/4670) | refactor: make retention planning explicit | OPEN | Refactors session retention logic for clarity (#4136). |

---

## Community Hot Topics

### Most Active Issues (by comment count)

| Issue | Title | Comments | 👍 | Summary |
|-------|-------|----------|---|---------|
| [#4657](https://github.com/HKUDS/nanobot/issues/4657) | Nanobot Radar Finding | 5 | 0 | Tracking issue for 13 independently validated bugs that lack open PRs — project management artifact indicating systematic bug-dispatch |
| [#3344](https://github.com/HKUDS/nanobot/issues/3344) | DingTalk Group Can not Seed file | 5 | 0 | File uploads in DingTalk arrive as separate messages, bot can't associate them |
| [#4604](https://github.com/HKUDS/nanobot/issues/4604) | Anthropic OAuth | 5 | 0 | Feature request for Anthropic OAuth (now addressed by PR #4632) |
| [#4419](https://github.com/HKUDS/nanobot/issues/4419) | Automatic reasoning effort escalation | 5 | 0 | Request for dynamic `reasoningEffort` control across provider models |
| [#4253](https://github.com/HKUDS/nanobot/issues/4253) | Support overriding model per conversation | 5 | 0 | User wants per-conversation model switching |
| [#2231](https://github.com/HKUDS/nanobot/issues/2231) | Plugin system for agent extensibility | 5 | 0 | Long-standing feature request for plugin architecture like Copilot CLI |
| [#4010](https://github.com/HKUDS/nanobot/issues/4010) | TTS / voice output support | 3 | 2 | Voice loop is half-complete (STT in, no TTS out) — high community interest |
| [#3166](https://github.com/HKUDS/nanobot/issues/3166) | Feishu channel no progress notifications | 2 | 1 | Feather/Lark channel lacks progress display |
| [#3309](https://github.com/HKUDS/nanobot/issues/3309) | Per-chat group policy overrides | 2 | 1 | Telegram group policy needs per-group customization |
| [#4683](https://github.com/HKUDS/nanobot/issues/4683) | temperature parameter error for sonnet-5 | 2 | 1 | API 400 error with claude-sonnet-5 — now fixed by PR #4685 |

### Underlying Needs Analysis

1. **Channel interoperability pain**: Multiple issues across DingTalk (#3344), Feishu (#3166), Telegram (#3309), WhatsApp (#2836, #2837), and WeChat/WeCom (#3343) — users consistently struggle with channel-specific quirks. The DingTalk file-seeding issue alone has dragged since April.

2. **Provider compatibility friction**: Temperature parameter rejection for sonnet-5 (#4683), Ollama tool-calling broken (#2829), OpenAI text-format tool calls not parsed (#4061) — users hitting edge cases with non-OpenAI providers.

3. **Multi-tenancy and isolation**: WhatsApp workspace isolation (#2836), cron session context reuse (#4082), heartbeat isolation debate (#1899) — growing demand for proper tenant/session boundaries.

4. **Voice loop completion**: TTS feature request (#4010) received 2 👍 in a week, indicating strong but small-group interest for closing the STT→LLM→TTS loop.

---

## Bugs & Stability

### Critical & High Severity Bugs Reported or Active

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **Critical** | [#4652](https://github.com/HKUDS/nanobot/issues/4652) | MCP tool call exception causes process crash | PR #4666 open |
| **Critical** | [#4683](https://github.com/HKUDS/nanobot/issues/4683) | `temperature` parameter omitted for sonnet-5 causes 400 error | PR #4685 open |
| **Critical** | [#4082](https://github.com/HKUDS/nanobot/issues/4082) | Cron jobs reuse fixed session context across runs (data leakage) | No fix PR yet |
| **Critical** | [#4076](https://github.com/HKUDS/nanobot/issues/4076) | `message` tool lacks outbound recipient authorization | PR #4668 open |
| **Critical** | [#4061](https://github.com/HKUDS/nanobot/issues/4061) | OpenAI-compatible text-based tool calls not parsed | PR #4662 open |
| **Critical** | [#4078](https://github.com/HKUDS/nanobot/issues/4078) | OpenAI-compatible API server lacks API key enforcement | PR #4669 open |
| **Critical** | [#2829](https://github.com/HKUDS/nanobot/issues/2829) | Ollama tool calling broken with gemma4 model | No fix PR; stale since April |
| **High** | [#4511](https://github.com/HKUDS/nanobot/issues/4511) | Windows `--background` mode mismatch between PID file and actual process | No fix PR |
| **High** | [#4544](https://github.com/HKUDS/nanobot/issues/4544) | Windows `exec` tool uses inconsistent shell (cmd.exe vs PowerShell) | PR #4648 batch fix included |
| **High** | [#3626](https://github.com/HKUDS/nanobot/issues/3626) | Telegram long polling silently hangs | No fix PR; stale since May |
| **High** | [#3257](https://github.com/HKUDS/nanobot/issues/3257) | Voice pipeline latency metrics missing (35-60s delays) | No fix PR |
| **High** | [#4068](https://github.com/HKUDS/nanobot/issues/4068) | Matrix stream buffer isolation broken | PR #4659 open |
| **Medium** | [#4055](https://github.com/HKUDS/nanobot/issues/4055) | Dream history not protected during compaction | PR #4664 open |
| **Medium** | [#4058](https://github.com/HKUDS/nanobot/issues/4058) | Invalid/double tool result IDs leak into session history | PR #4663 open |
| **Medium** | [#4064](https://github.com/HKUDS/nanobot/issues/4064) | Pending message runtime context lost | PR #4665 open |
| **Medium** | [#4075](https://github.com/HKUDS/nanobot/issues/4075) | Dream can overwrite user skills without guard | PR #4667 open |

**Summary**: The project has a **significant bug density** with at least 7 critical-severity issues active today. The encouraging sign is that **most have open fix PRs** (often by the same reporter `hamb1y`), suggesting a systematic bug-sweep is in progress. However, several high-severity bugs (Ollama tool calling #2829, Telegram hang #3626, email handling #2954) remain unfixed for months.

---

## Feature Requests & Roadmap Signals

### Predictions for Next Release

| Feature | Issue/PR | Likelihood | Rationale |
|---------|----------|------------|-----------|
| **Anthropic OAuth** | [#4604](https://github.com/HKUDS/nanobot/issues/4604) / [#4632](https://github.com/HKUDS/nanobot/pull/4632) | **High** | PR already open, actively discussed; Claude users highly motivated |
| **Mattermost Channel** | [#4459](https://github.com/HKUDS/nanobot/pull/4459) | **Medium-High** | Feature-complete PR, new channel integration |
| **OpenCode Zen Provider** | [#4686](https://github.com/HKUDS/nanobot/pull/4686) | **High** | PR open, canonical provider addition |
| **Plugin System** | [#2231](https://github.com/HKUDS/nanobot/issues/2231) | **Medium** | Long-standing (March), but no PR yet — likely deferred |
| **TTS Voice Output** | [#4010](https://github.com/HKUDS/nanobot/issues/4010) | **Medium-Low** | Small call count (2 👍), no PR yet |
| **Per-conversation model override** | [#4253](https://github.com/HKUDS/nanobot/issues/4253) | **Medium** | No PR, but steady interest |
| **Reasoning effort escalation** | [#4419](https://github.com/HKUDS/nanobot/issues/4419) | **Medium** | Clearly described, leverages existing `reasoningEffort` config |
| **Embedding-based context compression** | [#2937](https://github.com/HKUDS/nanobot/issues/2937) | **Low** | No PR, complex feature, quiet since April |

### Roadmap Signals

The rapid bug-fix batch (PR #4648) combined with new channel/provider support (Mattermost, OpenCode, Anthropic OAuth) suggests the project is **preparing for a stabilization release** that adds a few high-value features while cleaning up long-standing technical debt. The "Nanobot Radar" tracking issue (#4657) explicitly flags 13 issues as "validated but unaddressed" — this systematic triage work signals maintainer investment in quality.

---

## User Feedback Summary

### Notable Pain Points

1. **Channel fragmentation**: Users consistently report breaking or inconsistent behavior across different messaging platforms — DingTalk file seeding (#3344), Feishu progress notifications (#3166), Telegram hangs (#3626), WhatsApp workspace isolation (#2836).

2. **Windows compatibility**: Two bugs (#4511, #4544) specifically target Windows users: background mode state inconsistency and inconsistent shell selection (`cmd.exe` vs PowerShell).

3. **Voice interaction latency**: User reporting 35-60 second round-trips for voice interactions (#3257) with no way to debug which stage (STT, LLM, TTS) is the bottleneck.

4. **Multi-tenant isolation**: Users express clear privacy/confidentiality concerns — WhatsApp chats sharing a single workspace (#2836), cron jobs leaking context across runs (#4082), heartbeat session isolation rationale unclear (#1899).

5. **Ollama/edge provider support**: Three-month-old issue (#2829) with tool calling broken on Ollama remains unfixed — frustration may be building among local-model users.

### Satisfaction Signals

- **Community responsiveness**: Many issues receive comments within hours, and PRs are filed quickly for reported bugs — the bug-fix batch (#4648) addresses 13 issues in one shot.
- **Feature progression**: Anthropic OAuth and Mattermost channel support are being actively built — users see their requests turning into code.
- **Security awareness**: SSRF fixes, API key enforcement, and outbound authorization controls show maintainers take security seriously.

### Dissatisfaction Signals

- **Stale bugs**: Ollama tool calling (#2829), Telegram hang (#3626), email handling (#2954) — all open 2+ months without fix PRs.
- **Chinese-language issue**: Issue #4511 is written in Chinese — the project may need to ensure non-English contributors feel equally supported.

---

## Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Problem | Why Urgent |
|-------|-----|---------|------------|
| [#2829](https://github.com/HKUDS/nanobot/issues/2829) | 3 months | Ollama tool calling broken | Blocks a major local-model user base |
| [#3626](https://github.com/HKUDS/nanobot/issues/3626) | 2 months | Telegram long polling hangs | Core channel reliability issue |
| [#2954](https://github.com/HKUDS/nanobot/issues/2954) | 3 months | Email checking/handling inconsistent | Feature advertised but broken |
| [#3257](https://github.com/HKUDS/nanobot/issues/3257) | 2.5 months | Voice latency blind spot | No metrics = no optimization path |
| [#4082](https://github.com/HKUDS/nanobot/issues/4082) | 5 weeks | Cron context reuse | Data leakage risk; no fix PR despite being "validated" (#4657) |
| [#3096](https://github.com/HKUDS/nanobot/issues/3096) | 2.5 months | Tool scheduling serializes parallel calls | Performance regression for tool-heavy agents |
| [#2937](https://github.com/HKUDS/nanobot/issues/2937) | 3 months | Embedding-based context compression | Improves token efficiency — no traction |
| [#3436](https://github.com/HKUDS/nanobot/issues/3436) | 2 months | Call external agent framework | User wants NanoBot as orchestrator — interesting architectural direction |
| [#3559](https://github.com/HKUDS/nanobot/issues/3559) | 2 months | WebSocket can't replace webhooks for proactive sends | Multi-tenant deployment blocker |

### Watch Items

- **Issue #4657** ("Nanobot Radar Finding") itself is a meta-tracking issue — watch for when the 13 "validated but unaddressed" bugs get resolved. Currently only ~5 have open PRs.
- **PR #4632** (Anthropic OAuth) and **PR #4459** (Mattermost) have high community interest but are not yet merged — their progress indicates release readiness.
- **PR #4648** closed today — the merge of this 13-fix batch signals that maintainers may cut a release soon.

---

*Generated from public GitHub data for [HKUDS/nanobot](https://github.com/HKUDS/nanobot). Data snapshot: 2026-07-03.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for July 3, 2026.

---

## Hermes Agent Project Digest: 2026-07-03

### 1. Today's Overview
Activity on the Hermes Agent project remains high, with 50 issues and 50 pull requests updated in the last 24 hours. The project is currently processing a high volume of incoming bug reports (42 open issues) and community contributions (33 open PRs), signaling a healthy but potentially strained development cycle. While there were no new releases today, the team merged or closed 17 PRs, focusing on stability, security hardening, and user experience improvements across the Desktop, CLI, and gateway components. A significant portion of the activity involves regressions and edge cases, suggesting the project is in a phase of rapid iteration following recent large feature merges.

### 2. Releases
- **None** reported in the last 24 hours.

### 3. Project Progress (Merged/Closed PRs)
The 17 merged/closed PRs today indicate strong progress in stabilizing the codebase:
- **Security & Stability:** PR #57436 hardens long-term memory against CJK injection and unattended writes. PR #57433 improves systemd service management by ignoring inactive user-manager defaults. PR #30666 adds a configurable reply prefix for the Signal gateway platform.
- **Desktop UX:** PR #57443 caps the overlay inner-page width for better readability. PR #57430 (and #57432) fixes a bug where assistant reasoning was rendered as multiple broken "Thought" fragments.
- **Bug Fixes:** PR #57445 resolves an HTTP 500 crash in the dashboard when using only `basic_auth`. PR #57251 closed a bug fix for `APIConnectionError` errors when using the MoA (Mixture of Agents) provider on streaming platforms like Telegram.

### 4. Community Hot Topics
- **High Interest / Votes:** **Issue #38602** (Desktop Client-Only Installation, 👍37) remains the most upvoted feature request, showing a strong desire for a thin-client architecture. **Issue #33940** (Proper LiteLLM support, 👍5) also has sustained interest.
- **Active Discussion:** **Issue #52914** (11 comments) details a critical QQBot gateway regression causing infinite retry loops, a clear pain point for QQ Bot users. **Issue #36934** (8 comments) discusses a complex interaction where the `/steer` command collides with injection defenses on high-resistance models, leading to false positives.
- **New Feature Activity:** PR #57441 (Desktop: Skills/MCP hub parity) and PR #56859 (new offline memory skill "mind") are highly active, representing direct community contributions that expand Hermes' capabilities.

### 5. Bugs & Stability
Bug reports continue to surface regressions and edge cases. A clear theme is the instability introduced by new features and platform integrations.

- **Critical/P1 (Reported Today):**
    - **Issue #56704** ([P2]): `computer_use` fails on Linux/WSL due to a `TypeError: int() argument must be a string`, crashing the capture feature. No fix PR linked yet.
    - **Issue #52470** ([P2]): Dashboard auto-restart silently fails due to environment variable inheritance, breaking webhook and QR onboarding flows. No fix PR linked yet.
    - **Issue #53049** ([P3]): Desktop app left menu enters a reload loop, consuming high CPU. This appears to be a regression from a recent update.
- **Moderate/P2 (Reported Today):**
    - **Issue #57405** ([P3]): Model selector in the Desktop app crashes with `'dict' object has no attribute 'lower'`.
    - **Issue #57381** ([P3]): `hermes-setup` fails on Python 3.14 due to the removal of `distutils.version`.
- **Active Fix PRs:** Several bugs reported earlier now have fix PRs in progress: PR #57437 fixes the Honcho client singleton timeout issue (#57347), and PR #57434 addresses Windows install encoding failures.

### 6. Feature Requests & Roadmap Signals
- **Likely Next Version:**
    - **Desktop Client-Only Mode (#38602):** The high number of upvotes and the fact that the current desktop behavior is described as "always bootstrapping" suggests a move towards a thin-client is a top community priority.
    - **Skills & MCP Hub in Desktop UI (#57441):** This PR brings CLI parity to the GUI, which is a major quality-of-life improvement likely to be merged soon, given it relies on existing backend endpoints.
- **Speculative / Future:**
    - **OAuth Broker (#23944):** A proposal for a generic OAuth credential source to handle rotating tokens is gaining support, indicating a need for better multi-process and enterprise auth support.
    - **Advanced Secrets Management (#3630, Phase 4):** This feature continues to be updated but lacks recent maintainer activity. It appears to be a long-term roadmap item.

### 7. User Feedback Summary
- **Pain Points:**
    - **Regressions:** Users are frustrated by recurring regressions, particularly in the QQBot gateway (#52914) and Desktop UI (#53049, #47368). The "Delete profile" bug (#47368) is a specific example where a user action appears to succeed but is silently ignored.
    - **Platform-Specific Issues:** Telegram users are experiencing duplicate messages (#53449) and missing thread support (#48811). The SQLite locking issue on NFS (#33485) indicates platform incompatibility for some deployments.
    - **Configuration Complexity:** Users report difficulties with model configuration (#57405, #25106, #8465), where CLI switches do not persist correctly or break the UI.
- **Satisfaction:**
    - There is clear appreciation for new features, such as the Vertex provider support (#56687) and the ability to control model temperature defaults (PR #57440), even when these features initially ship with UI gaps.
    - The community is active in contributing fixes and new skills (e.g., PR #56859, PR #57438), indicating a high level of engagement and satisfaction with the project’s extensibility.

### 8. Backlog Watch
These issues have seen little to no maintainer action despite being open for a significant time and having workarounds or fixes proposed.

- **Issue #13490** (Configurable TUI status bar): Open since April 21, this request for theming and layout customization has community support but no maintainer engagement.
- **Issue #9403** (Pricing overrides & sync CLI): This is a long-standing feature from an unimplemented Phase 4 of the pricing architecture, indicating a roadmap item that has stalled.
- **Issue #24782** (Subagent fallback model uses wrong base_url): Open since May 13, this is a nuanced bug in the core agent delegation logic that impacts tool-using agents, making its lack of a fix concerning for reliability.
- **Issue #33485** (Honcho memory causes SIGABRT on shutdown): A potentially serious process termination bug open since May 27 with no fix in sight.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-03

## Today's Overview
PicoClaw shows **moderate activity** driven largely by automated dependency updates, with **25 PRs** updated in the last 24 hours—14 merged/closed and 11 still open. Two new open issues were filed, both representing **stability risks**: a config migration regression (v2→v3) affecting fresh installs, and a silent Matrix sync loop death without reconnection logic. While no new releases were published, the volume of merged PRs—many from `dependabot` and several `[stale]` bug fixes—suggests active maintenance and **clearing of technical debt**. The project's health is stable but warrants attention to the two reported bugs, particularly the silent failure in Matrix sync.

## Releases
**None**  
No new releases were published in the last 24 hours. The latest known release remains **v0.2.9** (git 2992...).

## Project Progress
**14 PRs were merged/closed today**, reflecting progress on both infrastructure and bug fixes:

- **New Feature**: [#3063](https://github.com/sipeed/picoclaw/pull/3063) — DeltaChat gateway added (merged, closed).
- **Bug Fixes**:
  - [#3160](https://github.com/sipeed/picoclaw/pull/3160) — Rejects cross-site launcher setup requests (auth).
  - [#3161](https://github.com/sipeed/picoclaw/pull/3161) — Keeps deny patterns active for custom allow rules (exec).
  - [#3158](https://github.com/sipeed/picoclaw/pull/3158) — Added tests for sandbox FS Windows path handling.
- **Dependency Updates** (mostly merged today):
  - Go: AWS SDK v2 config, Mautrix, Anthropic SDK, golang.org/x/crypto, Copilot SDK, and more.
  - Frontend: ESLint, react-i18next, shadcn, TypeScript-ESLint, Vite React plugin.
- **Stale PRs Closed**: Several older PRs (#3100, #3103, #3104, #3177) were merged for re-validation or superseded by newer versions.

## Community Hot Topics
Active discussions remain **low** (0 comments on both open issues), but volume suggests the community is engaged through PRs rather than issues:

- [#3063](https://github.com/sipeed/picoclaw/pull/3063) — **DeltaChat gateway feature** (merged, earlier comments). Likely drew interest for multi-platform bridging.
- [#3165](https://github.com/sipeed/picoclaw/pull/3165) — **Seed XML tool call recovery** (open). Relevant for users of Volcengine Doubao/Seed AI, indicating demand for OpenAI-compatible tool-call custom formats.
- **Dependency bump PRs** generated the most noise, but no deep discussion.

The lack of comments on new Issues (#3203, #3206) may indicate users encountering bugs are **not yet verified or reproduced** by maintainers.

## Bugs & Stability
Two new issues reported today:

1. **[HIGH] Issue #3206** — [v2→v3 config migration fails](https://github.com/sipeed/picoclaw/issues/3206) with `unknown field(s): build_info, session.dm_scope`.   
   - Affects fresh installs of v0.2.9. Causes `picoclaw status` to fail.  
   - **No fix PR exists.** Maintainers should prioritize: new users cannot start.

2. **[HIGH] Issue #3203** — [Matrix sync loop has no reconnection logic](https://github.com/sipeed/picoclaw/issues/3203).  
   - Causes silent death of long-polling `/sync` after network disruption. Systemd `Restart=on-failure` does not trigger.  
   - **No fix PR exists.** Critical for Matrix channel reliability in production.

No regressions or crash reports from merged PRs.

## Feature Requests & Roadmap Signals
- **DeltaChat gateway** (PR #3063, merged) is now available—signals intention to support **federated/encrypted messaging** alongside Matrix.
- **Seed XML tool call recovery** (PR #3165) suggests preparation for **non-standard OpenAI-compatible providers** (e.g., Volcengine Doubao). Likely candidate for next release.
- **Copilot SDK bump** (PR#3207, #3177) from `v0.2.0` to `v1.0.x` indicates **GitHub Copilot integration may be maturing** toward stable use—possibly a planned feature for the next minor release.

## User Feedback Summary
- **Pain points**: 
  - Configuration migration failure blocks fresh installations (Issue #3206) — likely frustrating for new users.
  - Matrix channel unreliability (Issue #3203) — impacts users relying on Matrix bridging for persistent chat.
- **No explicit satisfaction signals** in the past 24h; no praise or thank-you comments on issues.
- **Indirect positive**: High number of dependency updates merging without conflict suggests a well-maintained CI and responsive maintainers.

## Backlog Watch
The following items deserve maintainer attention:

- **Issue #3206 (HIGH)** — v2→v3 config migration bug. No maintainer response yet; should be acknowledged and assigned.
- **Issue #3203 (HIGH)** — Matrix sync reconnection logic missing. No maintainer response yet.
- **PR #3165** — Fork/Seed XML tool call recovery: open 9 days without review. Relevant to users of non-standard LLM providers.
- **PR #3171** — LINE channel sync.Map type assertion panic fix: open 8 days without review. Low severity but clean code fix.
- **Leftover stale PRs**: #3160, #3161, #3158 were merged today → clearing backlog is ongoing. No extremely long-dormant items remain.

No unassigned issues or PRs older than 30 days were detected in the top 20.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the project digest for **NanoClaw** for **2026-07-03**, generated from the provided GitHub data.

---

## NanoClaw Project Digest — 2026-07-03

**Project Health:** 🟡 **Moderate Activity**

### 1. Today's Overview
NanoClaw saw moderate activity today, with a clear focus on bug fixing and infrastructure cleanup. While **no new releases** were cut, the project processed **4 open issues** and **14 pull requests** in the last 24 hours, indicating a healthy level of community and maintainer engagement. The most critical discussion revolves around two high-priority WhatsApp bugs—user ID divergence and adapter collisions—both of which already have dedicated fix PRs open. The maintainer team also appears to be consolidating work on two major feature areas: an **agent template system** (with 3 related PRs) and an **instance-wide default provider** configuration.

### 2. Releases
**No new releases** as of today's data. The latest release remains previous versions (none listed). Users should expect incremental improvements via the current open PRs before the next release tag.

### 3. Project Progress
**Merged/Closed PRs (2):**
- **#2890** – `feat(templates): local template loader, ncl --template, and docs` — *Merged.* This is part 1 of the agent templates feature, allowing users to stamp an agent group from a template via the `ncl groups create --template <ref>` command. This unblocks the setup wizard flow in #2909.
- **#2771** – `perf(container): configurable --shm-size (default 1g) + --init for agent containers` — *Merged.* Improves headless Chromium stability inside agent containers by setting a larger shared memory size (default 1GB) and adding the `--init` flag.

**Features & Fixes Advancing:**
- **Agent Templates (Part 2)** – PR #2909 (draft, stacked on #2890) adds a template setup flow in the wizard and first-agent stamping.
- **Codex Provider support for Templates** – PR #2908 extends the template system to work with the Codex provider, adding persona prepend and git-independent skill discovery.
- **Recurring Task Fix** – PR #2915 addresses a bug where recurring tasks would fork into duplicate occurrences.
- **WhatsApp Cloud Fixes** – PR #2913 and #2914 fix the adapter key collision (Issue #2911) and document the webhook migration.
- **Container Cleanup** – PRs #2822, #2823, #2824 remove stale global memory instructions and dead mounts, improving Docker container reliability.
- **Default Agent Provider** – PR #2906 adds an instance-wide `DEFAULT_AGENT_PROVIDER` config variable.

### 4. Community Hot Topics
- **#2916** – *hi* by atinganematin2-byte ([link](https://github.com/nanocoai/nanoclaw/issues/2916)) — A generic greeting issue with 1 comment. Likely a test or introductory post; no material content.
- **#2912** – *WhatsApp user ids diverge between Baileys and Cloud paths* by glifocat ([link](https://github.com/nanocoai/nanoclaw/issues/2912)) — **High engagement potential.** This bug describes a core identity problem where the same human gets two different handles depending on which WhatsApp path they join, breaking roles/membership. No fix PR yet, but it’s directly related to the adapter collision (#2911) which has a fix.
- **#2911** – *WhatsApp Cloud adapter collides with native WhatsApp in the adapter registry* by glifocat ([link](https://github.com/nanocoai/nanoclaw/issues/2911)) — **Priority: High.** A clear architectural bug where both WhatsApp bridges register under the same `whatsapp` key, causing silent disabling of one channel. Already has a fix PR (#2913) open and ready for review.
- **#2907** – *ape_claw_cli* by slotaibuddy-admin ([link](https://github.com/nanocoai/nanoclaw/issues/2907)) — No summary. Likely a feature request or placeholder for a CLI tool.

**Underlying Need:** The WhatsApp issues reflect a growing user demand for **multi-instance and multi-channel support**, where operators want to run both native Baileys and WhatsApp Cloud simultaneously without collisions. This is a common pain point in multi-tenant or mixed-infrastructure deployments.

### 5. Bugs & Stability
| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| #2911 | 🔴 **High** | WhatsApp Cloud adapter collides with native WhatsApp (same registry key) | PR #2913 (open) |
| #2912 | 🟡 **Medium** | WhatsApp user IDs diverge between Baileys and Cloud paths (roles break) | No dedicated fix yet; may be resolved by #2913 |
| #2915 (PR) | 🟡 **Medium** | Recurring tasks fork into duplicate occurrences | Fix PR #2915 (open, self-fixing) |
| #2916 | ⚪ **Low** | Non-informative greeting issue | No action needed |

**Analysis:** The two WhatsApp bugs are the biggest stability risks today. #2911 is a blocking bug—running both WhatsApp paths silently disables one. The fix in #2913 should resolve both #2911 and likely mitigate #2912 by ensuring distinct adapter keys.

### 6. Feature Requests & Roadmap Signals
- **Agent Templates (PR #2890, #2909, #2908)** — This is a **major roadmap signal**. The ability to stamp agent groups from predefined templates, especially with Codex provider support, suggests NanoClaw is moving toward a “one-click agent deployment” model. Expect this to land in the next release (likely v0.8 or v0.9).
- **Instance-Wide Default Provider (PR #2906)** — A small but impactful quality-of-life feature. Operators who manage many groups will soon be able to set a single `.env` variable instead of configuring each group. This is likely a high-demand feature for enterprise users.
- **Web-Search-Plus Skill (PR #2725)** — A standalone utility skill for multi-provider web search + URL extraction. Aims to reduce dependency on MCP and improve offline/self-contained capability. Still open after 3 weeks; may need final review.
- **WhatsApp Cloud Instance Key (PR #2913, #2914)** — The documentation and fix PRs indicate that **multi-instance channel support** is a near-term priority. Expect the next release to stabilize the WhatsApp Cloud integration.

**Prediction for next release:** The template system (parts 1 & 2) and the WhatsApp Cloud instance key fix are the most likely candidates for the upcoming version.

### 7. User Feedback Summary
- **Pain Points:**
    - *WhatsApp identity fragmentation* – Users running both Baileys and WhatsApp Cloud are frustrated that permissions don’t carry over. (Issue #2912)
    - *Adapter collisions* – Silent failure when installing two WhatsApp adapters. User glifocat explicitly reported they had to choose one path. (Issue #2911)
    - *Recurring task duplication* – Scheduled tasks spawning multiple copies, causing confusion and resource waste. (PR #2915)
- **Positive Signals:**
    - The template system (PR #2890) and default provider config (PR #2906) were well-received by contributors (amit-shafnir, Koshkoshinsk), indicating community alignment on operational improvements.
    - The container performance fix (#2771) for Chromium stability was merged, addressing a long-standing issue with browser-based agents.
- **Use Cases:** Multi-channel WhatsApp deployments (enterprise), recurring automation workflows (scheduling), and rapid provisioning of agent groups via templates (SaaS/ISV).

### 8. Backlog Watch
- **PR #2725** – `Add web-search-plus skill` (robbyczgw-cla) — Created **2026-06-10**, last updated **2026-07-02**. Open for 23 days. Needs a maintainer review. It’s a large feature PR and may require architectural sign-off.
- **PR #2689** – `fix(signal): DM platform ID consistency, isMention, and ask_question/approval delivery` (klingel) — Created **2026-06-04**, last updated **2026-07-02**. Open for 29 days. This is a critical Signal integration fix that has been sitting for nearly a month. If Signal is a supported path, this PR needs expedited review.
- **PRs #2822, #2823, #2824** (CutSnake01) — Created **2026-06-20**, still open after 13 days. These are small cleanup/fix PRs (stale mounts, seed prompt, CLAUDE.md file). Low risk, likely just awaiting a quick merge.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-03

## Today's Overview

IronClaw activity is **very high** today with substantial development velocity. 21 PRs were merged or closed, 50 PRs were updated overall, and 23 issues were touched. The project is clearly in an intense build-and-fix phase focused on the **Reborn** architecture, with major feature work landing in Slack OAuth integration, tool/credential management, and WebUI redesign. However, a significant number of QA-flagged bugs (many from `joe-rlo`'s systematic bug bash) and infrastructure issues around Exa search throttling, routine creation hangs, and vision model reliability signal that **stability is currently lagging behind feature velocity**. The most critical pattern: multiple Reborn coordinator-stage wiring gaps (checkpoint ports, skill activation paths) are being discovered through coverage testing, suggesting some architectural seams need hardening.

**Assessment: Project health is mixed — high momentum and feature output, but a growing bug backlog and several mid-severity regressions that could erode user trust if not addressed.**

---

## Releases

No new releases today. The last release candidate (PR #5311, still open) would have bumped `ironclaw` from 0.24.0 → 0.29.1 with breaking changes in `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0), but it has not yet merged.

---

## Project Progress

21 PRs merged or closed today. Key advancements:

### Major Feature Landings
- **#5502** (closed, XL): Slack personal (user-token) OAuth — browser Connect flow. Converts manual token paste to one-click OAuth. **New contributor** @sergeiest.
- **#5501** (closed, M): Fix OAuth token exchange leak-sanitization. Adds `execute_credential_exchange` egress path that skips response sanitization for internal credential exchanges.
- **#5573** (closed, M): Fix Exa MCP SSE initialize parsing — accepts raw JSON and SSE-wrapped JSON-RPC bodies, reconstructs multi-line SSE events. Directly addresses the Exa search failures in issue #5571.
- **#5548** (closed, M): C-TRACECAP + C-ATTACH coverage — turn-event sink and attachment read-port wiring for Reborn test harness.
- **#5547** (closed, M): PR-C2 Tier-2 coverage — skill/durable/errors (C-SKILL, C-DURABLE, C-ERRORS) seams.
- **#5559** (closed, L): Architecture sprawl checks added to pre-commit scripts.

### Documentation & Cleanup
- **#5569** (open, S): Marks `ironclaw_oauth` as v1-only, slated for deletion. This is a healthy sign of the v1 → Reborn migration completing.
- **#5567** (open, XL): Type/trait cleanup — 6 traits removed, 6 DTO clusters unified, -176 lines net.

### Still Open & Active
- **#5576** (open, XL): Slack personal OAuth + move credentials to UI setup. DB migration required. Likely a follow-up to #5502.
- **#5565** (open, XL): Onboarding/NUX demo — intent handoff, OAuth entry, chat-first workspace, mock-backed Vercel demo.
- **#5563** (open, XL): Design system tokens + /playground page.
- **#5280** (open, XL): Trace Commons — instance-wide enrollment, per-user profiles, trace inspection.

---

## Community Hot Topics

### Most Active Discussions

1. **#5522 — Reborn routine fails when task requires reading Slack DMs** (2 comments, QA-bug)
   - [Issue #5522](https://github.com/nearai/ironclaw/issues/5522)
   - Core complaint: Agent cannot read Slack DMs because no read capability exists; gets stuck in `capability_info` retry loop. This is a **feature gap masquerading as a bug** — the Slack integration only supports write (posting) but the agent is being asked to read. PRs #5502 and #5576 directly address this by adding Slack personal OAuth with read-capable tokens.

2. **#5459 — Configurable skills and tools** (2 comments)
   - [Issue #5459](https://github.com/nearai/ironclaw/issues/5459)
   - This is the umbrella feature for private vs. admin tool/skill installation. Underlying need: Enterprise/workspace users need role-based access control over extensions. The three PRs (#5499, #5513, #5525) all branch from this issue, showing it's getting significant engineering attention.

3. **#5460 — Memories visible to every user in workspace** (1 comment, QA)
   - [Issue #5460](https://github.com/nearai/ironclaw/issues/5460)
   - Reported by @zetyquickly: saved memories are not scoped to the user who created them. This is a **data isolation / multi-tenancy bug** that would be a compliance concern in any shared workspace deployment.

### Underlying Community Needs
The pattern across active threads is clear: **users need proper integration with external services (Slack read/write, Google SSO) and proper data isolation (memories, credentials) — the two pillars of collaborative team use.** The project is responding to the first (Slack OAuth is landing) but the second (memory scoping, credential isolation) appears to be a work-in-progress with no fix PRs yet.

---

## Bugs & Stability

### Critical/High Severity

1. **#5522 — Reborn routine fails on Slack DM reading** (P1-suggested, QA-bug)
   - Agent cannot read Slack DMs, enters retry loop. **No capability exists**, not a runtime regression. PRs #5502/#5576 add the missing OAuth flow. **Fix in progress.**

2. **#5571 — Web search fails on Railway QA (Exa IP throttling)** (CLOSED)
   - Exa MCP upstream throttling causes `invalid_output` that aborts entire turn, cascading across 5 test cases. **Fixed by PR #5573** (merged today) which fixes SSE parsing. Fix confirmed closed.

3. **#5572 — HookedLoopCheckpointPort doesn't forward checkpoint payload methods** (OPEN, no comments)
   - Any hooks-enabled coordinator turn fails at Checkpoint stage. This is a **wiring regression** in the hooks middleware — the `HookedLoopCheckpointPort` only overrides `checkpoint()` but not `stage_checkpoint_payload()` / `load_checkpoint_payload()`. **No fix PR yet.**

4. **#5552 — Run fails with generic "invalid result" after multiple tool failures** (P2)
   - No user-visible error details about which tool failed or why. UX regression: Activity section shows nothing useful. **No fix PR yet.**

### Medium Severity

5. **#5504 — Routine creation hangs without returning result** (P1)
   - Chat shows planning message then hangs indefinitely. Different from previous generic communication errors. **No fix PR yet.**

6. **#5508 — Slack delivery target not found despite active connection** (P2)
   - New routines can't find Slack targets that old routines use successfully. User is told to reconnect something already connected. **No fix PR yet.**

7. **#5558 — Vision model hallucinates image contents, accepts false corrections** (P2)
   - Model misidentifies objects, then accepts user's false correction without re-analyzing. This is concerning — suggests the vision pipeline has no re-verification step when user contradicts the model. **No fix PR yet.**

8. **#5551 — Automation posts intermediate progress messages to Slack instead of final result** (P2)
   - Internal execution steps leaked to Slack channel. UX regression: users get spammy intermediate messages instead of clean summaries. **No fix PR yet.**

### Lower Severity / Cosmetic

9. **#5555 — Terminal floating button overlaps chat composer** (P2, UI)
10. **#5554 — Mobile chat layout breaks with horizontal overflow** (P2, UI)
11. **#5553 — Approval notifications disappear instead of remaining in history** (P2)
12. **#5556 — Active chat remains highlighted in sidebar after navigating away** (P3, UI)
13. **#5557 — Logs deep link requires opening twice** (P3, UI)
14. **#5509 — Chat creation latency scales with accumulated history** (P2, performance)

### Infrastructure / Coverage

15. **#5527 — FilesystemSessionThreadService idempotency write/read scope mismatch** (OPEN)
    - `owner scope` write vs `system scope` read — early replay-before-policy is dead in production. Codegraph-verified. **No fix PR yet.**
16. **#5530 — Skill criteria-based auto-activation unreachable from TurnCoordinator** (CLOSED)
    - Dead code on the modern submit path. **Closed as known gap** — the feature path needs re-wiring rather than a bugfix.
17. **#5479 — Reborn one-runtime group harness: second thread fails** (CLOSED)
    - `driver_unavailable / unknown thread` — blocks E-MULTIUSER/C-MULTIUSER seams. Closed, but no fix PR reference.

---

## Feature Requests & Roadmap Signals

### Likely in Next Release

1. **Slack Personal OAuth** (PRs #5502, #5501, #5576) — The three-PR stack for Slack personal (user-token) OAuth is landing aggressively. This will likely ship in the next release and unblock #5522.
2. **Configurable Tools & Skills** (issue #5459, PRs #5499, #5513, #5525) — Private installs, admin UI for tenant-shared credentials, WASM tool install from zip. This is a multi-part feature that's actively landing.
3. **Design System Tokens + /playground** (PR #5563) — Achalvs is building a shared design token infrastructure. Likely to land soon given the WebUI redesign momentum.
4. **Onboarding/NUX** (PR #5565) — Intent-driven onboarding with mock backend. Strategic priority for new user conversion.

### Possible But Less Certain

5. **Trace Commons per-user enrollment** (PR #5280) — Still open since June 26, but large (XL) and has DB migration. Might be deferred for a later release.
6. **Stable OAuth auth-relay for PR previews** (issue #5570) — Requested by @zetyquickly to test Google SSO on ephemeral Railway deployments. Engineering-significant but blocking CI quality.
7. **Automations page redesign** (PR #5084) — Open since June 18, still active. Denser, more scannable layout for the Automations surface.

### Design Signal
The **/playground** PR (#5563) is interesting — a separate "playground" surface suggests IronClaw is thinking about developer experience and experimentation, not just production agent usage.

---

## User Feedback Summary

### Pain Points (from QA Bug Bash / Issues)

| Pain Point | Issue | Frequency/Likelihood of Impact |
|---|---|---|
| Routine creation hangs indefinitely with no feedback | #5504 | High — blocks core workflow |
| Slack delivery targets not found despite active connection | #5508 | High — new routine creation fails |
| Tool failures show generic "invalid result" with no details | #5552 | High — debugging impossible |
| Intermediate Slack spam instead of final results | #5551 | Medium — user-facing annoyance |
| Vision model hallucinates and accepts false corrections | #5558 | Medium — trust erosion |
| Mobile chat layout broken (horizontal overflow) | #5554 | Medium — mobile users affected |
| Chat creation gets slower with history accumulation | #5509 | Medium — degrades over time |
| Approval notifications vanish without trace | #5553 | Low but trust-eroding for automations |
| Memories visible to all workspace users | #5460 | High if multi-tenant deployment — data leak |

### Positive Signals
- The **Slack OAuth flow** (PRs #5502, #5576) directly addresses user frustration with manual token setup — a clear UX improvement.
- The **design system tokens** effort (#5563) suggests investment in UI consistency and future AI-ability to make small UI changes.
- Active bug bash by @joe-rlo (10+ issues filed today) shows systematic QA investment.
- **pinchbench** (65 non-passing tests analyzed in #5537) shows the benchmarking infrastructure is mature enough to measure regressions.

### Satisfaction Indicators
No explicit positive user feedback captured in this data window. The volume of bug reports suggests user dissatisfaction with reliability, but the feature velocity (Slack OAuth, tool management, UI redesign) may offset for early adopters.

---

## Backlog Watch

### Issues Needing Maintainer Attention

1. **#4108 — Nightly E2E failed** (OPEN since 2026-05-27)
   - [Issue #4108](https://github.com/nearai/ironclaw/issues/4108)
   - **38 days without resolution.** Nightly E2E has been failing for over a month with no root cause fix referenced. This is a **critical infrastructure signal** — if nightly CI is red, confidence in all changes is diminished. The most recent run (2026-07-02) also failed. This is the single most concerning item in the backlog.

2. **#5527 — FilesystemSessionThreadService idempotency scope mismatch** (OPEN since 2026-07-02)
   - Production bug confirmed via codegraph. Early replay-before-policy is dead in production. **No fix PR.** This could silently corrupt data in edge cases.

### Stale/Long-Open Items
- No other items older than ~2 months appear in this window. The project is generally responsive, with the E2E CI failure being the notable exception.

### Maintainer Capacity Assessment
The project has multiple active contributors (henrypark133, sergeiest, zetyquickly, joe-rlo, pranavraja99, achalvs, serrrfirat) and a CI bot. The addition of **new contributors** (@sergeiest, @achalvs) is healthy. However, the sheer volume of open issues (19 active, many P1/P2) plus 29 open PRs suggests **maintainer bandwidth may be stretched thin**, especially given the nightly E2E has been failing for 38 days without root-cause fix. Risk: regressions may accumulate faster than they can be triaged.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-03

## 1. Today's Overview
Project activity remains moderate with 5 open issues and 8 updated PRs in the last 24 hours. Notably, **7 of 8 PRs were merged or closed**, indicating strong forward momentum on fixes and optimizations. No new releases were published today. All 5 open issues are now marked stale (last updated 2026-04-02) and have received no maintainer response in over three months, raising concern about community responsiveness. The merge rate suggests active internal development, but long-neglected user reports signal a growing backlog of unresolved problems.

## 2. Releases
**None.** No new releases were published today. The latest release remains unknown.

## 3. Project Progress
Seven PRs were merged or closed today, demonstrating focused effort on engine reliability, UI polish, and bug fixes:

- **#2259** — `chore: optimize engine failure overlay` (area: renderer, openclaw, cowork) — Merged
- **#2258** — `fix(openclaw): stabilize DeepSeek prompt cache in long sessions` — Merged. Disables aggregate tool-result rewriting on the live prompt path to maintain byte-stable history for provider prefix caches, while retaining existing overflow protections.
- **#2257** — `feat(cowork): unify engine startup screen into one continuous splash` — Merged. Adds a static pre-React splash screen to eliminate spinner handoff between window show, renderer init, and engine startup.
- **#2255** — `fix/scheduled task none delivery` — Merged. Fixes a bug where switching a scheduled task's notification channel to "不通知" did not persist because the OpenClaw gateway `cron.update` patch-merged `delivery` and could not clear a previously set channel property.
- **#2254** — `chore: update main page image` — Merged
- **#2253** — `chore: update readme` — Merged
- **#2252** — `fix(settings): prevent white screen when deleting active custom model` — Merged. Fixes a race condition where deleting the currently selected custom provider caused a white screen because `confirmDeleteCustomProvider` awaited `configService.updateConfig` before switching away from the deleted key.

**Still open:** PR #2256 (fix for scheduled-task none-delivery and settings model-delete) — overlaps with #2255 and #2252 but remains unmerged.

## 4. Community Hot Topics
All 5 open issues have **zero new activity** since April 2, 2026. No issues or PRs today received more than 2 comments or significant reactions. This indicates low recent community engagement or that maintainers have not surfaced any hot discussions. The most notable:

- **#1354** — [stale] "让龙虾帮忙启动pageant后电脑蓝屏" — BSOD after launching Pageant via LobsterAI. 2 comments. [Issue link](https://github.com/netease-youdao/LobsterAI/issues/1354)
- **#1357** — [stale] "帮我开启pageant" claims it started Pageant but it did not — 1 comment. [Issue link](https://github.com/netease-youdao/LobsterAI/issues/1357)
- **#1358** — [stale] Scheduled task click has no interaction feedback — 1 comment. [Issue link](https://github.com/netease-youdao/LobsterAI/issues/1358)

**Underlying need:** Users are encountering unreliability in task execution feedback and stability issues (BSOD) when using Pageant integration, along with confusion about whether tasks are actually running. These indicate a need for better visual confirmation and more robust external tool integration.

## 5. Bugs & Stability
No new bugs were reported today. The five stale issues (all from April 2) remain unresolved:

| Issue | Severity | Summary | Fix PR Exists? |
|-------|----------|---------|----------------|
| #1354 | **Critical** | BSOD when launching Pageant via LobsterAI | No |
| #1357 | **High** | False positive: says Pageant started but it didn't | No |
| #1359 | **Medium** | Deleted tasks reappear after restart | No |
| #1360 | **Low** | No duplicate name validation when creating custom agents | No |
| #1358 | **Low** | No visual feedback when clicking scheduled tasks | No |

**Notable:** PR #2256 (still open) directly addresses the "scheduled-task none-delivery" bug and the "white screen on model delete" crash (already fixed via #2252 and #2255). No fix PRs exist for the BSOD or false-positive Pageant issues.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were made today. Signals from merged PRs indicate the following near-term priorities:
- **Engine startup UX improvement** (#2257) — continuous splash screen merging multiple init phases
- **DeepSeek prompt cache stability** (#2258) — ensuring long sessions remain performant and cache-friendly
- **Scheduled task notification channel fix** (#2255) — ensuring "do not notify" option actually works
- **Settings crash prevention** (#2252) — white screen on model deletion

**Prediction:** Next version will likely include the unified startup screen, DeepSeek cache improvements, and ongoing scheduled task reliability fixes. The stale Pageant BSOD and false-positive issues (#1354, #1357) are critical but have no visible progress; they may not land until a major stability release.

## 7. User Feedback Summary
User pain points expressed in stale issues:
- **Stability concerns:** BSOD after using Pageant feature (#1354)
- **False positives:** Claims "started" but actually did not (#1357)
- **Lack of feedback:** No visual indication whether a scheduled task is running (#1358)
- **Persistence bugs:** Deleted tasks re-appear after app restart (#1359)
- **Usability gap:** No duplicate name validation when creating agents (#1360)

**Satisfaction indicators:** Low — zero new community interactions in 3+ months on reported bugs, and all issues remain unaddressed. The lack of any recent user praise or feature requests suggests either a quiet user base or unresolved frustrations driving disengagement.

## 8. Backlog Watch
All 5 open issues are **stale** (last updated 2026-04-02) with no maintainer response. This backlog is critical:

- **#1354** — BSOD after Pageant launch (3 months stale) [Issue link](https://github.com/netease-youdao/LobsterAI/issues/1354)
- **#1357** — Pageant false "started" claim (3 months stale) [Issue link](https://github.com/netease-youdao/LobsterAI/issues/1357)
- **#1359** — Deleted tasks reappear (3 months stale) [Issue link](https://github.com/netease-youdao/LobsterAI/issues/1359)
- **#1360** — Duplicate agent name allowed (3 months stale) [Issue link](https://github.com/netease-youdao/LobsterAI/issues/1360)
- **#1358** — Scheduled task no feedback (3 months stale) [Issue link](https://github.com/netease-youdao/LobsterAI/issues/1358)

**Maintainer attention needed:** All five require triage, confirmation, or a response. The BSOD and task deletion bugs are most severe. PR #2256 (open) is a near-duplicate of two already-merged PRs and should be closed or consolidated.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-03

## Today's Overview
Moltis had a quiet day in terms of issue traffic, with zero new or updated issues in the last 24 hours. However, three pull requests received updates, including one significant merged fix and two new open PRs targeting WhatsApp reliability and provider extensibility. No new releases were published today. Overall, the project appears in a maintenance-and-extension phase, with focused improvements to WhatsApp integration and LLM provider support.

## Releases
No new releases were published today. The most recent release remains unavailable in this data window.

## Project Progress
One pull request was merged/closed today:

- **PR #1116 (CLOSED)** — `fix(whatsapp): deliver replies to @lid chats via PN JID rewrite`  
  **Author:** juanlotito | **Created:** 2026-06-12 | **Merged:** 2026-07-02  
  **Summary:** Fixed a critical bug where replies sent to privacy-enabled senders' `@lid` chats were silently dropped on WhatsApp. The agent would generate a reply visible in the web UI, but the outbound sender would never deliver it to the user, and no "Delivered" receipt was returned. The fix applies a JID rewrite via push notification (PN) to ensure replies reach users in LID-addressed conversations.  
  **Link:** https://github.com/moltis-org/moltis/pull/1116

This fix closes a significant reliability gap for WhatsApp messaging, particularly for users who have enabled privacy features.

## Community Hot Topics
Two new open PRs were submitted today, neither has comments yet, but both address meaningful gaps:

- **PR #1144 (OPEN)** — `feat(whatsapp): bump whatsapp-rust 0.5 -> 0.6 with LID-native addressing`  
  **Author:** juanlotito | **Updated:** 2026-07-02  
  **Summary:** Upgrades the WhatsApp Rust library from 0.5 to 0.6, pinning to a specific merge commit to enable LID (Lightweight Identifier) native addressing. Without this, inbound messages from WhatsApp users whose devices have migrated to LID addressing would be silently lost. The PR also includes a patch override via `[patch.crates-io]` for the fix merged in `oxidezap/whatsapp-rust#943`.  
  **Link:** https://github.com/moltis-org/moltis/pull/1144

- **PR #1143 (OPEN)** — `Add Requesty as an OpenAI-compatible provider`  
  **Author:** Thibaultjaigu | **Updated:** 2026-07-02  
  **Summary:** Adds Requesty (https://requesty.ai) as a table-driven OpenAI-compatible LLM provider, mirroring the existing OpenRouter wiring for consistency. This enables users to route requests through Requesty's API using `Authorization: Bearer $REQUESTY_API_KEY` at `https://router.requesty.ai/v1`.  
  **Link:** https://github.com/moltis-org/moltis/pull/1143

**Underlying need analysis:** Both PRs reflect the community's desire for broader connectivity — WhatsApp LID compatibility addresses a growing privacy requirement, while Requesty support expands LLM provider choice and reliability through an additional routing option.

## Bugs & Stability
No new bugs were reported in the last 24 hours. However, the recently merged PR #1116 fixed a high-severity WhatsApp delivery bug affecting `@lid` chats, which was likely causing silent message loss for users with privacy-enabled senders. This fix is now live in the codebase.

## Feature Requests & Roadmap Signals
No explicit feature requests were filed as issues today. However, the two open PRs signal likely roadmap directions:

- **WhatsApp LID-native addressing** (PR #1144) — Likely to be merged soon, as it directly follows the fix in PR #1116 and enables full compatibility with WhatsApp's evolving addressing scheme. Expect this in the next minor release.
- **Requesty provider support** (PR #1143) — A clean, low-risk addition following the established OpenRouter pattern. This is likely to land in the same release cycle or shortly after.

No speculative community requests were identifiable from today's data.

## User Feedback Summary
No direct user feedback (comments, reactions, or issue discussions) was recorded in the last 24 hours. The data does not indicate any new satisfaction or dissatisfaction signals.

## Backlog Watch
No long-unanswered issues or PRs were identified in today's data. Both open PRs are very recent (created July 2), and the only closed item was merged today. No stale issues await maintainer attention at this time.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the project digest for **CoPaw (QwenPaw)** on **2026-07-03**.

---

### 1. Today's Overview

CoPaw has entered a period of **intense active development**, driven by the **v2.0.0-beta.2** pre-release. Activity is very high, with a significant volume of merged PRs (27) and a large pipeline of open work (50 PRs updated in 24h). The community is actively stress-testing both the legacy v1.1.12 and the new v2.0.0 beta, uncovering critical bugs related to memory leaks, context management, and channel reliability. The large number of open issues (14) and community feature requests indicates the project is scaling in usage but facing growing pains in stability and UX. The v2.0.0 release appears to be on a fast track, but several blocker-level bugs remain.

### 2. Releases

- **v2.0.0-beta.2** was released.
    - **Status:** Early beta for QwenPaw 2.0.0.
    - **Warning:** Contains breaking changes and instability; not production-ready for general use.
    - **What's Changed:** The only noted change is `feat(cli): add cron up...` (implementation appears to have been truncated in the log data).
    - **Action:** N/A - This is a pre-release. Developers should test against this version but prepare for further breaking changes.

### 3. Project Progress

The last 24 hours show a healthy mix of feature advancement and critical bug fixes, with **27 PRs merged or closed**.

- **Security Hardening:** Multiple PRs were merged to address secret leakage. These include env var resolution for config, redaction of secrets in dialog logs and persistent artifacts, and adding rate limiting.
- **Context & Runtime Stability:** Critical fixes were merged for the v2.0.0 runtime, including preventing scroll context eviction from destroying active tasks and fixing the goal mode gate.
- **Platform & Frontend:** Improvements to the desktop build pipeline (Tauri switch) and the console UI (agent table readability) were merged.
- **Specific Fixes:**
    - **Merged:** ` feat(auth): enhance rate limiting` ([PR #5738](agentscope-ai/QwenPaw PR #5738))
    - **Merged:** `fix(context): don't crash compaction when summary exceeds schema maxLength` ([PR #5287](agentscope-ai/QwenPaw PR #5287))
    - **Merged:** `fix(loop): fix goal mode gate architecture` ([PR #5727](agentscope-ai/QwenPaw PR #5727))

### 4. Community Hot Topics

The community is most engaged around the **security and stability of their deployments**.

- **#5705 - Secret Security Enhancement:** ([Issue #5705](agentscope-ai/QwenPaw Issue #5705)) This is the most active feature request, detailing gaps in API key storage and log sanitization. The high engagement suggests a strong underlying need for enterprise-grade security, especially for users deploying in shared or containerized environments.
- **#5273 - v2.0.0 Tracking Issue:** ([Issue #5273](agentscope-ai/QwenPaw Issue #5273)) Serves as the primary hub for all v2.0.0 pre-release bugs. It has the most reactions (👍: 1) and is the central point of feedback for the new version, indicating significant developer interest.
- **#5720 - Memory Leak (v1.1.12):** ([Issue #5720](agentscope-ai/QwenPaw Issue #5720)) Reports a significant memory leak on Windows leading to process crashes and configuration corruption. This is a critical stability concern for production users.

### 5. Bugs & Stability

Stability remains a major theme, with several high-severity bugs reported in the last 24 hours.

- **Critical:**
    - **[Bug] #5720 - Memory Leak on v1.1.12.post2:** ([Issue #5720](agentscope-ai/QwenPaw Issue #5720)) Memory grows unboundedly until the process is killed, corrupting configuration data. **Status:** Open.
    - **[Bug] #5748 - Agent Hangs Forever (v2.0.0):** ([Issue #5748](agentscope-ai/QwenPaw Issue #5748)) Consumer thread blocks permanently on tool call failure, causing an endless typing indicator. **Status:** Fix PR [#5749](agentscope-ai/QwenPaw PR #5749) is open.
    - **[Bug] #5746 - Scroll Context Compression Folds Active Task (v2.0.0 beta):** ([Issue #5746](agentscope-ai/QwenPaw Issue #5746)) The context manager can "forget" the current task and reply to an old message. **Status:** Fix PR [#5747](agentscope-ai/QwenPaw PR #5747) is open.
    - **[Bug] #5717 - Malformed Tool-Call History Causes Infinite Loops (v2.0.0):** ([Issue #5717](agentscope-ai/QwenPaw Issue #5717)) A truncated tool call argument forces the model to repeat the previous step indefinitely. **Status:** Open.
- **High:**
    - **[Bug] #5701 - Page Freezes on Concurrent Access (v1.1.10):** ([Issue #5701](agentscope-ai/QwenPaw Issue #5701)) The console becomes unresponsive with multiple users/agents accessing the same agent. **Status:** Closed (fix likely merged).
    - **[Bug] #5709 - Feishu Bot Message Hard Drop:** ([Issue #5709](agentscope-ai/QwenPaw Issue #5709)) All messages from other bots are discarded, breaking multi-agent Feishu collaboration. **Status:** Closed (fix likely merged).

### 6. Feature Requests & Roadmap Signals

User requests are clearly pointing towards **automation, security, and developer experience (DX)**.

**Likely for Next Release (v2.0.0 stable / v1.2.0):**
- **Model Auto-Failover:** ([Issue #5718](agentscope-ai/QwenPaw Issue #5718)) Users want the agent to automatically switch to a backup model when the primary is rate-limited or down. A corresponding PR [#5597](agentscope-ai/QwenPaw PR #5597) is already open, making this a strong candidate.
- **Config Security with Env Vars:** ([Issue #5705](agentscope-ai/QwenPaw Issue #5705)) The request for env var substitution in config files and log sanitization is already addressed by merged PRs ([#5740](agentscope-ai/QwenPaw PR #5740), [#5741](agentscope-ai/QwenPaw PR #5741), [#5745](agentscope-ai/QwenPaw PR #5745)), so this will land soon.
- **Enhanced CLI Capabilities:** ([Issue #5737](agentscope-ai/QwenPaw Issue #5737)) There is demand for a richer CLI to support non-graphical, programmatic control, such as pre-installing skills. This is a strong signal for DX improvements.

**Longer Term / Speculative:**
- **Multi-Model Routing:** The auto-failover feature could evolve into intelligent model routing based on task complexity or cost.
- **Selectable Text in UI:** ([Issue #5712](agentscope-ai/QwenPaw Issue #5712)) A simple UX request for mouse-based text selection. A fix PR [#5739](agentscope-ai/QwenPaw PR #5739) is open, suggesting a quick resolution.

### 7. User Feedback Summary

- **Pain Points (Dissatisfaction):**
    - **Instability in v2.0.0 beta:** Users are reporting significant regressions, particularly with context management (scroll, anchor points) and runtime execution (infinite loops, hangs).
    - **Memory Leaks:** A major concern for production users on the stable v1.1.12 branch, causing data loss.
    - **Channel Integration Brokenness:** Feishu and QQ channel bugs are causing message loss and broken multi-agent workflows, which is a core use case for the platform.
    - **Performance:** Streaming output in the browser console causes significant lag, which is a poor user experience compared to competitors like DeepSeek.
- **Use Cases:**
    - **Multi-Agent Collaboration:** Users are heavily testing multi-agent scenarios across different channels (Feishu, QQ, Discord).
    - **Containerized / Remote Deployments:** Reports mention running QwenPaw in restricted containers and needing CLI-only management, pointing towards cloud/enterprise deployments.
    - **Cron Jobs & Automation:** The user who reported the context compression bug was using a `/heartbeat` cron job, highlighting the importance of long-running, unattended tasks.
- **Satisfaction:** Users are actively contributing fixes (many first-time contributors) and pushing for advanced features, which is a strong positive signal. The community is engaged, but the sheer volume of bug reports indicates they are hitting real walls.

### 8. Backlog Watch

- **#5273 - v2.0.0 Pre-release Bug Tracker:** ([Issue #5273](agentscope-ai/QwenPaw Issue #5273)) This is the primary watch item. Any maintainer action on this thread is critical to prevent bug reports from being fragmented.
- **#5720 - Memory Leak (v1.1.12):** ([Issue #5720](agentscope-ai/QwenPaw Issue #5720)) While a fix is not yet identified, this is a critical production blocker that likely requires immediate root cause analysis. The detailed analysis provided by the reporter should be prioritized.
- **#5717 - Tool Call Loop (v2.0.0):** ([Issue #5717](agentscope-ai/QwenPaw Issue #5717)) An open bug causing "endless repeated tool execution" in the new runtime. This is a show-stopper for the v2.0.0 GA release and needs maintainer attention.
- **#5708 - Feishu Interactive Card Parsing:** ([Issue #5708](agentscope-ai/QwenPaw Issue #5708)) An open bug where a core Feishu feature (interactive cards) is completely broken. This is likely a high-impact issue for Feishu users that has been open for some time.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-03

## Today's Overview

ZeroClaw continues at high velocity with **37 active issues** and **50 pull requests** updated in the last 24 hours, indicating a very active development cycle. No new releases were published today—the project remains in its pre-release iteration phase (latest tagged work references v0.8.3 and v0.9.0 targets). The maintainer team is processing a heavy inbound workload: 4 issues were closed and 19 PRs were merged/closed in the past day, suggesting sustained triage and merge throughput. The project is tackling significant architectural work—memory persistence, channel expansion, observability, and security hardening—while simultaneously fighting technical debt in CI, Windows compatibility, and tool surface gaps.

---

## Releases

**None.** No new releases were published today. The project is operating between tagged versions; documentation references v0.8.2 and v0.8.3, and a v0.9.0 tracker ([#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)) is actively accumulating breaking changes.

---

## Project Progress

**19 PRs merged or closed today.** Key advances include:

- **MCP tool visibility fixed in the dashboard:** PR [#8305](https://github.com/zeroclaw-labs/zeroclaw/pull/8305) (merged) surfaces MCP server tools through the gateway API to the web tools dashboard, resolving a user-reported gap where configured MCP tools were invisible in the UI even though the agent could use them.

- **Security auditing advances:** PR [#8547](https://github.com/zeroclaw-labs/zeroclaw/pull/8547) (merged) removes the `rag-pdf` feature and its `ttf-parser` dependency, clearing RUSTSEC-2026-0192. PR [#8574](https://github.com/zeroclaw-labs/zeroclaw/pull/8574) adds regression tests for zip bomb inflation guards.

- **Memory architecture:** PR [#8570](https://github.com/zeroclaw-labs/zeroclaw/pull/8570) (open) proposes a durable store seam for memory with dedup, budget, and policy-gating—"Epic A" of the persistent-memory path.

- **Channel expansion:** A stacked 3-PR series (PRs [#8609](https://github.com/zeroclaw-labs/zeroclaw/pull/8609), [#8611](https://github.com/zeroclaw-labs/zeroclaw/pull/8611), [#8618](https://github.com/zeroclaw-labs/zeroclaw/pull/8618)) adds a Git forge channel with GitHub and Gitea/Forgejo providers, plus SOP-ingress from channel events.

- **Skills fixes:** PR [#8335](https://github.com/zeroclaw-labs/zeroclaw/pull/8335) makes `skills install`/`list`/`remove` bundle-aware, fixing a broken workflow where skill commands targeted the wrong directory. PR [#8616](https://github.com/zeroclaw-labs/zeroclaw/pull/8616) restores the `always: true` frontmatter flag for skills.

- **Windows build:** PR [#8604](https://github.com/zeroclaw-labs/zeroclaw/pull/8604) statically links the MSVC CRT for Windows targets.

---

## Community Hot Topics

### Most Active Issues

1. **[#8193 — MCP tools missing from TUI sessions](https://github.com/zeroclaw-labs/zeroclaw/issues/8193)** (14 comments, S1 severity)
   - Two users report that MCP servers expose tools but the TUI doesn't receive them. Root cause appears to be a gateway/runtime synchronization gap. **Fix status:** PR [#8305](https://github.com/zeroclaw-labs/zeroclaw/pull/8305) (merged) addresses dashboard visibility, but the TUI gap persistence suggests more work needed.

2. **[#6808 — RFC: Work Lanes, Board Automation, Label Cleanup](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)** (13 comments)
   - A governance RFC for improving issue/PR routing and label hygiene. Label documentation PR [#8612](https://github.com/zeroclaw-labs/zeroclaw/pull/8612) and stale ramp PR [#8607](https://github.com/zeroclaw-labs/zeroclaw/pull/8607) appear to be rollout steps from this RFC.

3. **[#7462 — 74 test failures on Windows](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)** (7 comments, P1)
   - Windows users face systematic test suite failures due to Unix-only assumptions. A Windows build fix PR [#8604](https://github.com/zeroclaw-labs/zeroclaw/pull/8604) was opened today, suggesting the team is actively working on this.

4. **[#5542 — OOM kills in WSL2](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)** (6 comments, S0 severity—data loss/security risk)
   - The daemon is killed by OOM with very high memory consumption. Still open since April with no fresh fix PRs.

5. **[#8226 — Per-agent custom environment variables](https://github.com/zeroclaw-labs/zeroclaw/issues/8226)** (5 comments)
   - Feature request for multi-tenancy support with per-agent runtime contexts and masked secrets. Blocked on architecture decisions.

### Analysis

The community is consistently hitting two pain points: **MCP tool visibility** (tools exist but UIs don't show them) and **configuration model gaps** (skills/single-agent assumptions break in multi-agent deployments). The volume of RFC-driven governance work (labels, stale process, audit policy) suggests the project is scaling past its initial rapid-prototyping phase and needs process scaffolding.

---

## Bugs & Stability

### New Today (2026-07-02/03)

| Issue | Severity | Description | Status |
|-------|----------|-------------|--------|
| [#8631](https://github.com/zeroclaw-labs/zeroclaw/issues/8631) | S2 | Deterministic SOP steps marked "Completed" without executing when triggered headlessly | Open, no fix PR |
| [#8632](https://github.com/zeroclaw-labs/zeroclaw/issues/8632) | S1 | Source install with embedded-web fails because generated API client doesn't exist yet | Open, build blocker |
| [#8627](https://github.com/zeroclaw-labs/zeroclaw/issues/8627) | S1 | WhatsApp Web device linking broken by new passkey/companion-linking gate | Open, channel broken |
| [#8615](https://github.com/zeroclaw-labs/zeroclaw/issues/8615) | S2 | Compatible provider silently deletes content via unconditional `<think>` tag stripping | Open, content loss |

### Previously Reported (active)

| Issue | Severity | Description | Status |
|-------|----------|-------------|--------|
| [#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542) | S0 | Consecutive OOM in WSL2 (data loss risk) | Open since April |
| [#8193](https://github.com/zeroclaw-labs/zeroclaw/issues/8193) | S1 | MCP tools missing from TUI sessions | Fix PR merged, may need follow-up |
| [#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302) | P1 | Gemini 400 errors—wrong turn order in history | Open, no fix PR |
| [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | S2 | 74 Windows test failures | Build fix PR open [#8604](https://github.com/zeroclaw-labs/zeroclaw/pull/8604) |

**Notable:** Two S1 workflow-blocking bugs were filed today ([#8632](https://github.com/zeroclaw-labs/zeroclaw/issues/8632) and [#8627](https://github.com/zeroclaw-labs/zeroclaw/issues/8627)), both affecting installation and channel functionality. The OOM issue ([#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)) remains the highest-severity open bug at S0.

---

## Feature Requests & Roadmap Signals

### High-Impact Requests from Today

1. **[#8600 — Easy per-chat model switching for multi-model providers](https://github.com/zeroclaw-labs/zeroclaw/issues/8600)**
   - User migrating from moltis wants to switch between any model supported by a provider (e.g., all OpenRouter models). Currently no UI or command to enumerate or switch models mid-session. Likely v0.8.3 candidate.

2. **[#8602 — Enhanced file_read: line caps, charset detection, PDF, notebooks](https://github.com/zeroclaw-labs/zeroclaw/issues/8602)**
   - File read tool is fragile for non-trivial files. Proposes parity with Claude Code's Read tool. Tool-level change; could ship in a minor release.

3. **[#8626 — zerocode should validate against full daemon RPC spec](https://github.com/zeroclaw-labs/zeroclaw/issues/8626)**
   - Currently zerocode shadows the RPC registry with hand-typed constants. Proposes receiving and validating against the daemon's spec at connect. Architecture fix; likely v0.9.0.

4. **[#8550 / #8603 — OpenAI-compatible chat completions endpoint](https://github.com/zeroclaw-labs/zeroclaw/issues/8550)**
   - Duplicate-feeling requests (both from REL-mame) for an OpenAI-compatible REST endpoint so Open WebUI/LobeChat can connect. High-value integration request; visible on roadmap as RFC.

5. **[#8396 — Wire-Protocol-First Provider Model](https://github.com/zeroclaw-labs/zeroclaw/issues/8396)**
   - An RFC proposing `wire_api` as the primary organizing axis for providers, replacing the current provider-kind-based model. Architecture-breaking change; definitely v0.9.0 or later.

### Prediction for Next Release (v0.8.3)

From tracker [#8073](https://github.com/zeroclaw-labs/zeroclaw/issues/8073), v0.8.3 focuses on observability, CI, docs, and dependencies. Likely shipping: OTel content policy ([#8567](https://github.com/zeroclaw-labs/zeroclaw/pull/8567)), audit policy docs, skills install fixes, and the MCP dashboard fix.

---

## User Feedback Summary

- **Positive signals:** The Git forge channel series ([#8609](https://github.com/zeroclaw-labs/zeroclaw/pull/8609), [#8611](https://github.com/zeroclaw-labs/zeroclaw/pull/8611), [#8618](https://github.com/zeroclaw-labs/zeroclaw/pull/8618)) shows sophisticated Community + Provider expansion. The memory architecture PR (Epic A) is a major foundation for persistent state.

- **Pain points (user-reported):**
  - *"MCP tools exist but UIs don't show them"* (multiple users, issues [#8193](https://github.com/zeroclaw-labs/zeroclaw/issues/8193), [#8302](https://github.com/zeroclaw-labs/zeroclaw/issues/8302))
  - *"Can't install skills in multi-agent setups"* (issue [#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334), fixed in PR [#8335](https://github.com/zeroclaw-labs/zeroclaw/pull/8335))
  - *"Windows is broken out of the box"* (issue [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462), fix in progress)
  - *"Can't switch models mid-chat"* (issue [#8600](https://github.com/zeroclaw-labs/zeroclaw/issues/8600))
  - *"No OpenAI-compatible endpoint"* (issues [#8550](https://github.com/zeroclaw-labs/zeroclaw/issues/8550), [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603))

- **Satisfaction notes:** SOP engine praised as "a great concept" (issue [#8587](https://github.com/zeroclaw-labs/zeroclaw/issues/8587)), but documentation is insufficient—users want more examples and syntax detail.

---

## Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Days Since Last Update | Summary | Risk |
|-------|------------------------|---------|------|
| [#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542) | 84+ days | Consecutive OOM in WSL2 (S0) | Critical—data loss risk, no movement |
| [#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302) | 60+ days | Gemini 400 errors (P1) | Production blocker for Gemini users |
| [#6250](https://github.com/zeroclaw-labs/zeroclaw/issues/6250) | 62+ days | Auth middleware extraction (P1) | Security improvement, blocked on architecture |
| [#7946](https://github.com/zeroclaw-labs/zeroclaw/pull/7946) | 14+ days | Context window bar for TUI/CLI—needs author action | Feature PR stalled |
| [#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) | 1 day (closed) | `.ignore` file mechanism RFC—closed without merge | Closed despite 5 comments and user interest |

### PRs Stuck in Review

- **[#7946](https://github.com/zeroclaw-labs/zeroclaw/pull/7946)** — Context window bar: `needs-author-action` label, no movement from author eugeneb50 since 2026-06-18. High-value UX feature blocked on author response.

### Risk Signal

The OOM issue ([#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)) has been open for **84 days** at S0 (data loss/security risk) with 6 comments but no fix PR. This is concerning for a project that markets itself as a production-ready agent runtime. The Gemini 400 bug ([#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302)) has stalled for 60 days, potentially alienating Gemini provider users.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*