# OpenClaw Ecosystem Digest 2026-07-23

> Issues: 431 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-23 01:26 UTC

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

# OpenClaw Project Digest — 2026-07-23

## Today's Overview

OpenClaw shows extremely high development activity today with 431 issues and 500 PRs updated in the last 24 hours, signaling a very active and rapidly evolving project. The ratio of open/active issues (281) to closed (150) suggests the maintainer team is making steady progress on a large backlog, though 301 open PRs versus 199 merged/closed indicates a significant review queue. No new releases were published today, but the volume of PR activity—particularly around release tooling, localization infrastructure, and channel plugin refactoring—suggests the project is preparing for a forthcoming release cycle. The overall health is robust, with sustained community engagement and clear maintainer investment in both bug fixes and architectural improvements.

## Releases

No new releases were published on 2026-07-23.

## Project Progress

Today's merged and closed PRs demonstrate several areas of meaningful progress:

- **Release workflow improvements**: PR #112822 (closed) isolates extended-stable Docker aliases to prevent accidental tag promotions, and PR #112831 addresses changelog attribution guard requirements for the release pipeline
- **Channel plugin fixes**: PR #112807 (closed) keeps Lark/Feishu Drive comments working through identity outages; PR #95313 (closed) fixes Slack channel-id reads for name-allowlisted channels; PR #102340 (closed) honors configured Slack App Home commands
- **UI and infrastructure refactoring**: PR #112817 (closed) moves sidebar attention ownership into a reactive controller for the Control UI; PR #112802 (closed) shrinks a 9,898-line database-first legacy-store guard architecture
- **TUI and CLI improvements**: PR #109535 (closed) and PR #109537 (closed) add timeouts to Codex CLI binary lookup and DNS admin subprocess probes, preventing indefinite blocking during initialization
- **New feature contributions**: PR #112828 (open) adds Control UI discovery and lifecycle for ClawHub search, add/update/remove preview methods, and consent management; PR #112811 (open) enables multiple Microsoft Teams bot accounts per gateway instance

## Community Hot Topics

**Most discussed issue**: [#75 - Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) remains the community's top priority with 115 comments and 80 reactions. The demand for desktop app parity across platforms (currently only macOS, iOS, and Android are supported) reflects a significant unmet need in the user base, particularly for enterprise and power users on Windows and Linux.

**Most requested security feature**: [#10659 - Masked Secrets](https://github.com/openclaw/openclaw/issues/10659) continues to garner strong support (15 comments, 4 reactions) for preventing agents from accessing raw API keys. The underlying need is for enterprise-grade secret management that allows API key *usage* without exposure to prompt injection or accidental leaks.

**Performance regression concern**: [#85333 - doctor --fix slow on 2026.5.20](https://github.com/openclaw/openclaw/issues/85333) (17 comments) documents a 4-5x performance regression that affects production VPS deployments. The community's investment in reproducing and analyzing this suggests high sensitivity to performance stability.

**Plugin ecosystem friction**: [#92516 - Containerized deploys can't use externalized channel plugins](https://github.com/openclaw/openclaw/issues/92516) reveals an architectural gap where channel plugins (unlike provider plugins) cannot be trusted when delivered via self-hosted containers, blocking enterprise deployment patterns.

## Bugs & Stability

**P0/Critical severity:**
- [#108435 - Gateway fails to start on 2026.7.1 update](https://github.com/openclaw/openclaw/issues/108435) (9 comments, regression) — gateway fails to start with systemd, ollama, or manual launch after update. No fix PR identified yet; marked as release blocker with `impact:crash-loop` and `impact:ux-release-blocker`.

**P1/High severity (open):**
- [#91009 - Codex PreToolUse hook relay spawns CPU-bound processes](https://github.com/openclaw/openclaw/issues/91009) (15 comments, regression) — spawns CPU-bound `openclaw-hooks` processes that stall gateway RPC. Linked PR open but no direct fix committed.
- [#92043 - 180s compaction timeout causes failure on legitimate long compactions](https://github.com/openclaw/openclaw/issues/92043) (12 comments) — no partial-progress reuse means long session compactions fail identically every turn. Fix PR is linked.
- [#108580 - Cron tool schema incompatible with llama.cpp grammar-constrained calling](https://github.com/openclaw/openclaw/issues/108580) (6 comments, regression on 2026.7.1) — blocks all chat requests for users on llama.cpp. Linked PR exists.
- [#90840 - Subagent raw output delivered to chat instead of parent summary](https://github.com/openclaw/openclaw/issues/90840) (7 comments, regression) — `sessions_spawn` mode="run" leaks child completion directly to chat.
- [#99773 - Hot reload drops include-defined models](https://github.com/openclaw/openclaw/issues/99773) (6 comments) — phantom "Unknown model" errors until restart after config hot reload.

**P2/Medium severity:**
- [#87318 - amazon-bedrock Haiku 4.5 inference profile ARN not supported](https://github.com/openclaw/openclaw/issues/87318) (10 comments) — modelId override ignored, falls back to direct Anthropic
- [#99840 - Accessibility: Screen readers announce every token during streaming](https://github.com/openclaw/openclaw/issues/65538) (7 comments) — aria-live="polite" causes continuous fragmented speech output
- [#94626 - LINE channel /status intermittently fails](https://github.com/openclaw/openclaw/issues/94626) (6 comments) — reply token expiry race condition

## Feature Requests & Roadmap Signals

**Strongest roadmap signal**: The localization infrastructure PRs (#112784, #112801, #111543) represent a major coordinated effort to add contributor ownership guides, catalog authoring, refresh loops, and surface disposition requirements. These are marked `maintainer`, `size: XL`, and reference RFC #42, indicating this is a planned, architecturally significant feature likely for the next major release.

**Likely for next minor release**: 
- [#13583 - Pre-response enforcement hooks (hard gates)](https://github.com/openclaw/openclaw/issues/13583) — mandatory tool-call/policy rules before agent responses. Multiple maintainer-review labels active.
- [#9912 - maxTurns/maxToolCalls config option](https://github.com/openclaw/openclaw/issues/9912) — limit agent iterations, strongly requested for models that ignore system prompt instructions.
- [#10142 - session:end internal hook event](https://github.com/openclaw/openclaw/issues/10142) — workflow orchestration integration with systems like Temporal.

**Longer-term signals**:
- #75 (Clawdbot Apps for Linux/Windows) — persistent top-voted feature, likely a major project milestone
- #38568 (Context window % in system prompt) — quality-of-life improvement for agent awareness
- #10659 (Masked Secrets) — foundational security architecture change

## User Feedback Summary

**Major pain points**: 
- Performance regressions are the most acutely felt issue, with users reporting 4-5x slowdowns in core CLI commands (#85333) and multi-hour agent session failures (#92043)
- Platform fragmentation continues to frustrate users — Linux and Windows users lack desktop app parity (#75)
- Enterprise deployment friction is rising: containerized self-hosted deploys cannot use external channel plugins (#92516), and production gateway stability issues (memory growth #87314, crash loops #76275, #83968) are recurring themes
- Configuration hot-reload failures (#99773) create persistent "phantom" errors that require full restarts, disrupting production workflows

**Satisfaction indicators**: 
- Strong community engagement with 115 comments on the top issue suggests an invested user base
- Multiple users contributing detailed reproduction steps, logs, and environment data demonstrates sophisticated, invested user base
- The rapid response to regressions (multiple PRs opened within hours/days of bug reports) suggests responsive maintainership that users appreciate

**Emerging use cases**: 
- Multi-channel scaling (Teams multi-bot support #112811, Slack App Home customization #102340)
- Voice/Talk interactions on iOS (#91007)
- Codex integration for enterprise agent workflows (#99947, #97911)
- Local inference adoption with llama.cpp (#108580, #87687) — multiple users pushing for vllm/llama.cpp compatibility

## Backlog Watch

**Issues needing maintainer attention**:

1. [#85333 - doctor --fix performance regression](https://github.com/openclaw/openclaw/issues/85333) (P1, stale since May 22) — marked `needs-maintainer-review` and `needs-live-repro` for 2 months. This is a P1 performance regression affecting production deployments with no fix PR.

2. [#85103 - Model fallback chain not triggered on quota exhaustion](https://github.com/openclaw/openclaw/issues/85103) (P1, closed but unresolved) — closed without resolution; fallback chain failures during provider quota exhaustion remain unaddressed.

3. [#41199 - Agent-to-Agent communication tool parameter conflicts](https://github.com/openclaw/openclaw/issues/41199) (P1, stale since March) — LLMs consistently add conflicting optional parameters, causing systematic tool execution failures. Marked `needs-live-repro` with linked PR but no movement in 4+ months.

4. [#39807 - Billing error 402 causes infinite retry death spiral](https://github.com/openclaw/openclaw/issues/39807) (P1, stale since March 8) — no backoff on billing errors burns API credits and makes agents unresponsive. Marked `needs-maintainer-review`.

5. [#65538 - Screen reader accessibility regression](https://github.com/openclaw/openclaw/issues/65538) (P1, since April 12) — aria-live="polite" causes continuous fragmented speech for NVDA users. No linked fix PR despite P1 severity.

6. [#87212 - System envelope footer leaked into Telegram outbound](https://github.com/openclaw/openclaw/issues/87212) (P1, since May 27) — internal separator text echoed verbatim as user-facing replies. Marked `needs-info` and `needs-security-review`; appears to be a sensitive data leak.

**PRs awaiting review**:
- [#111543 - localization contributor ownership guide](https://github.com/openclaw/openclaw/pull/111543) (XL, open 4 days) — foundational documentation for localization infrastructure, marked `needs proof`
- [#89040 - avoid event-loop stall during embedded_run](https://github.com/openclaw/openclaw/pull/89040) (XL, open 52 days) — addresses chronic message-loss issues causing 14-22 second stalls; P1, `ready for maintainer look`
- [#83933 - fix cron deleteAfterRun for manual runs](https://github.com/openclaw/openclaw/pull/83933) (XL, open 65 days) — manual runs consuming scheduled one-shot jobs; P1 but `needs proof` for 2+ months

---

## Cross-Ecosystem Comparison

## Cross-Project Ecosystem Comparison Report — 2026-07-23

### 1. Ecosystem Overview

The personal AI agent open-source landscape is in a **high-velocity expansion phase**, driven by convergence around multi-channel delivery, memory persistence, and enterprise-grade observability. Projects span a wide maturity gradient—from mature production systems like **OpenClaw** (431 daily issues, extensive plugin ecosystem) to incubation-stage tools like **NullClaw** (single Discord fix). A clear architectural split is emerging: monolithic gateway frameworks (OpenClaw, NanoBot) vs. modular, protocol-driven platforms (ZeroClaw, Moltis). The ecosystem is responding to three dominant user demands: **cross-platform desktop parity**, **production reliability (crash/compaction/OOM fixes)**, and **model/provider flexibility** (per-conversation routing, fallback chains). No single project dominates all axes; instead, specialized strengths are driving differentiation.

---

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Releases | Ecosystem Health Score* | Activity Tier |
|---|---|---|---|---|---|
| **OpenClaw** | 431 | 500 | None | ⚠️ High (review queue bottleneck) | Hyper-growth |
| **NanoBot** | 6 | 63 | None | ✅ High (high merge velocity) | Fast shipping |
| **Hermes Agent** | 50 | 50 | None | ✅ Moderate-high | Active |
| **CoPaw** | 31 | 50 | v2.0.0.post4 | ⚠️ Mixed (regressions offset new release) | High-change |
| **IronClaw** | 50 | 50 | None | ✅ High (pre-v1 polish) | Pre-launch sprint |
| **ZeroClaw** | 50 | 50 | None | ✅ Moderate-high | Sustained |
| **PicoClaw** | 4 | 5 | None | ⚠️ Low-medium (stale features) | Maintenance |
| **LobsterAI** | 1 | 5 | None | ✅ High (sprint clean-up) | Burst |
| **NanoClaw** | 1 | 3 | None | ✅ Stable-low | Quiet |
| **NullClaw** | 1 (closed) | 1 (merged) | None | ✅ Stable (single-fix day) | Maintenance |
| **Moltis** | 1 | 1 | None | 🟢 Stable | Low velocity |
| **TinyClaw** | 0 | 0 | None | 🟢 Inactive | Dormant |
| **ZeptoClaw** | 0 | 0 | None | 🟢 Inactive | Dormant |

*Health Score: Qualitative assessment considering merge velocity, regression rate, maintainer responsiveness, and issue resolution pace.

---

### 3. OpenClaw's Position

**Advantages:**
- **Largest community and contribution volume** — 431 issues + 500 PRs per day, far exceeding peers. The issue tracker serves as a de facto community feature forum.
- **Mature plugin ecosystem** — Separate channel plugins (Slack, Feishu, Teams) with externalized delivery. Multiple PRs extend plugin autonomy (Teams multi-bot, Slack App Home).
- **Self-hosted container deployment** — Docker/official images available, though containerized channel plugins have an open architectural gap (#92516).
- **Localization infrastructure** — Major investment in contributor guides, catalog refresh loops, and surface disposition (RFC #42), signaling internationalization readiness.

**Technical Approach Differences:**
- **Database-first store architecture** — OpenClaw uses a legacy-store guard based on 9,898 lines of database-first patterns (PR #112802), contrasting with ZeroClaw's `MemoryStrategy` trait abstraction and CoPaw's SQLite-as-source-of-truth approach.
- **Reactive vs. event-driven control** — OpenClaw is migrating to reactive controllers (sidebar attention, PR #112817), while ZeroClaw uses WebSocket daemon nodes with OTel spans.
- **Release pipeline complexity** — OpenClaw has intricate Docker alias isolation and changelog attribution guards; fewer peers have automated release tooling at this scale.

**Community Size Comparison:**
- OpenClaw's top issue (#75, 115 comments, 80 reactions) has more engagement than the *entire* monthly issue activity of PicoClaw, NullClaw, or Moltis.
- However, OpenClaw's 301 open PRs (vs. 199 merged) suggest a **maintainer bottleneck**—the review queue is ~1.5x the merge rate. NanoBot merges 63% of daily PRs; OpenClaw merges ~40%.

---

### 4. Shared Technical Focus Areas

| Focus Area | Involved Projects | Specific Needs |
|---|---|---|
| **Multi-agent orchestration** | NanoBot (#5000), OpenClaw (#41199), ZeroClaw (#7218) | Persistent agent identities, inter-agent negotiation, context handoff |
| **Enterprise authentication** | OpenClaw (#10659, masked secrets), ZeroClaw (#7141, OIDC), IronClaw (#6527, tenant security) | OIDC/SAML, secret masking, admin-managed access policies |
| **Production gateway reliability** | OpenClaw (#108435, crash-loop; #76275), CoPaw (#6376, process crash), PicoClaw (#3203, Matrix reconnection) | Supervisor crash recovery, silent-failure detection, zero-downtime restart |
| **Cross-platform desktop parity** | OpenClaw (#75, Linux/Windows apps), Hermes (#4335, multi-platform context), PicoClaw (#3257, stateless gateway) | Windows/Linux GUI clients, unified session store |
| **Model/provider flexibility** | CoPaw (#6318, per-conversation model), OpenClaw (#9912, maxTurns), ZeroClaw (#7100, per-model capability), Moltis (#574, topic-based routing) | Per-conversation model selection, fallback chains, provider-agnostic tools |
| **Memory & context management** | NanoBot (#5041, Dream cursor), OpenClaw (#92043, compaction timeouts), ZeroClaw (#6850, decoupled memory lifecycle), CoPaw (#6323, staged compaction) | Staged compaction, SQLite-based context stores, configurable expiry |
| **Observability & telemetry** | Hermes (#64536, OTLP export), ZeroClaw (#8752, OTel spans), IronClaw (#6284, error recoverability) | OpenTelemetry spans, turn-level trace correlation, model fallback visibility |

---

### 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | ZeroClaw | CoPaw | IronClaw | Others |
|---|---|---|---|---|---|---|---|
| **Target user** | Enterprise self-hoster, power user | Developer, lightweight deployer | AI researcher, multi-platform user | DevOps, daemon-oriented admin | Content creator, mini-program user | Pre-v1 early adopter | Niche / hobbyist |
| **Primary channel** | Gateway + plugins (Slack, Teams, Feishu) | Telegram, Feishu, Slack | CLI, Telegram, Discord | Daemon + WebSocket nodes (Matrix, WhatsApp) | Console + WeChat ecosystem | Web app + Telegram/Slack | Single-channel specialists |
| **Architecture style** | Monolithic gateway with plugin registry | Provider-agnostic core + per-channel adapters | Relay connector pattern | Daemon nodes + OTel instrumentation | Console-focused with scroll context | Web-first with hermetic testing | Minimal / micro |
| **Release maturity** | Pre-major (high churn) | Stable (frequent minor releases) | Active development | v0.9.0 candidate | v2.x with regression challenges | Pre-v1 (bug bash) | v0.x / single-fix |
| **Community style** | Large-scale bug-factory with maintainer bottleneck | High-velocity contributor acceptance | Feature-request heavy | RFC-driven architectural decisions | User-reported regression pressure | Sprint-style QA waves | Single-contributor / silent |

**Key Observation:**
- **OpenClaw** is the only project with a dedicated localization + plugin ecosystem at scale, but its maintainer bottleneck (301 open PRs) risks contributor burnout.
- **ZeroClaw** is the most architecturally deliberate—RFC processes, OTel observability, decoupled memory lifecycle—but has the highest barrier to contribution.
- **CoPaw** uniquely targets the Chinese market (WeChat, MiniMax, DashScope) and has the fastest release cadence among active projects (v2.0.0.post4 within days).
- **NanoBot** achieves the best "velocity vs. stability" balance (63% merge rate, 40 merged/closed PRs per day) with minimal regression drama.

---

### 6. Community Momentum & Maturity

**Tier 1 — Hyper-growth / Pre-launch Sprint:**
- **OpenClaw**: Insane volume but maintainer-limited. Momentum is strong; risk is fragmentation from unmerged PRs.
- **IronClaw**: Highest focus ratio (all activity points to v1 launch). Explicit bug_bash and v1-launch-checklist labels. Could ship v1.0.0 within weeks.

**Tier 2 — Active Development / Rapid Iteration:**
- **NanoBot**: Consistent high merge rate. Multi-bot Telegram, xAI Grok OAuth, and Dream cursor fix signals a strong next release.
- **ZeroClaw**: Sustained RFC-driven progress. Windows CI gap (#7462) and stale issue backlog are headwinds, but OIDC + Anthropic fallback work is production-oriented.
- **Hermes Agent**: High issue count (46 open) but low merge rate (6 merged). Risk of feature-request bloat without delivery.
- **CoPaw**: The fastest releaser (v2.0.0.post4 in days) but regressions are accumulating. v2.0 stability is the critical blocker.

**Tier 3 — Maintenance / Low Velocity:**
- **PicoClaw**: Stale features (Bedrock caching, DeltaChat refactor) and critical Matrix reconnection bug unfixed. Risk of community drift.
- **LobsterAI**: Sprint clean-up after long-dormant merges (skills management, cron builder). Likely moving back to maintenance.
- **NanoClaw**: Quiet but responsive. Low friction for contributors (3 open PRs).
- **Moltis**: Single feature request (#574) with no maintainer response. Low urgency.

**Tier 4 — Dormant:**
- **TinyClaw**: Zero activity.
- **ZeptoClaw**: Zero activity.
- **NullClaw**: Single-fix day; no feature pipeline.

---

### 7. Trend Signals

1. **Cross-platform desktop is the #1 unaddressed need**: OpenClaw (#75) has 115 comments for Linux/Windows apps. Hermes (#4335) wants CLI↔Telegram context sharing. PicoClaw (#3257) wants stateless gateway mode. The ecosystem is mobile/CLI-heavy; **desktop parity is the next competitive battleground**.

2. **Enterprise credential management is becoming table stakes**: OpenClaw (#10659, masked secrets), ZeroClaw (#7141, OIDC), and IronClaw (#6527, tenant security) all build enterprise auth. This signals a shift from "cool demo" to "production deployment" expectations. **Secrets isolation and SSO will differentiate viable vs. hobby projects** within 6 months.

3. **Memory context is the new "RAM" for agents**: CoPaw (staged compaction, #6323), ZeroClaw (decoupled memory lifecycle, #6850), NanoBot (Dream cursor, #5041) all wrestle with memory persistence. The trend is toward **SQLite-based stores with configurable compaction policies**. Projects that fail to solve "context loss without explanation" (#8837, ZeroClaw) will lose user trust.

4. **Error recoverability is a frustration sink**: IronClaw's #6284 epic and OpenClaw's #108435 crash-loop both address the same pain: agents that fail silently. Users want **observable, self-healing systems**—error visibility + model-triggered recovery. This is a UX design gap across all projects.

5. **Multi-provider flexibility is surface-level**: Almost every project claims "any LLM provider," but real friction surfaces in schema compatibility (CoPaw #6363, $ref crashes), fallback chains (OpenClaw #85103), and per-conversation routing (Moltis #574). **The next differentiator will be intelligent model routing**, not just provider configuration.

6. **Windows support is the forgotten platform**: ZeroClaw (#7462) reveals 74 test failures on Windows. OpenClaw (#75) has no desktop app at all. CoPaw (#6361) has broken Windows development scripts. **The ecosystem is Linux-first, leaving Windows enterprise users underserved**—a market opportunity for any project that invests.

7. **Community-driven PRs are accelerating feature velocity**: NanoBot's multi-bot Telegram (#5033) and ZeroClaw's Anthropic fallback chain (5 PRs by `IftekharUddin`) show that **peripheral contributors are designing major features**. Projects with clear RFC processes (ZeroClaw) and fast merge cycles (NanoBot) attract more external investment. OpenClaw's maintainer bottleneck risks losing this energy.

---

**Bottom line for technical decision-makers:** If you need **scale and plugin ecosystem** today, choose OpenClaw—but budget for maintainer delays. If you need **stability and rapid iteration**, NanoBot is the safest bet. For **architectural rigor and enterprise readiness**, ZeroClaw's RFC-driven approach will pay off in 6–12 months. For **Chinese market deployment**, CoPaw is the only option. **No project yet solves the cross-platform desktop + Windows gap**—that's a $10M greenfield opportunity.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here’s a structured project digest for **NanoBot** covering activity through **2026-07-23**.

---

## NanoBot Project Digest — 2026-07-23

### 1. Today’s Overview
NanoBot showed **very high development activity** today, driven primarily by a surge in pull request updates (63 total, 40 merged/closed). While there were no new releases, the project advanced significantly across multiple fronts: provider integration (xAI Grok OAuth, OAuth status warnings), channel fixes (Feishu, Slack, Telegram multi-bot), and core agent improvements (session-scoped presets, idle compaction). Bug-fix velocity was notable, with several small, targeted PRs addressing crash-causing edge cases in cron storage and channel pairing. Community engagement on issues was moderate, with 6 issues updated and a major architectural discussion (#5000) receiving ongoing comments.

### 2. Releases
**None.** No releases were published in the last 24 hours. The last tag remains at the previous stable version.

### 3. Project Progress
**40 pull requests were merged or closed** today, marking a high-velocity day for fixes and feature integrations. Notable advancements include:

- **Agent & Memory**  
  - **[#4866] feat(agent): make model presets session-scoped** (merged) — This major feature makes model preset selection per-session, persists only explicit overrides, and ensures a single `LLMRuntime` per turn for consistency across provider calls, tools, and compaction.  
  - **[#4988] fix(agent): keep background (cron / local trigger) turns silent** (open) — Prevents unwanted "I completed the tool steps but couldn't produce a final answer" messages in non-interactive contexts.

- **Providers & Channels**  
  - **[#5035] feat(providers): add xAI Grok OAuth** (open) — Adds native OAuth 2.0 + PKCE for xAI Grok subscriptions, capability-gated X Search, and proactive token refresh.  
  - **[#5009] feat(feishu): add groupPolicy listen** (open) — Allows Feishu group chats to accumulate context without LLM turns, replying only on `@mention`.  
  - **[#5033] feat(telegram): support multiple bot instances in WebUI** (open) — Enables multi-bot management with independent tokens, validation, and enable/disable controls.

- **Performance & UI**  
  - **[#5003] perf(webui): index conversation history in SQLite** (open) — Replaces runtime JSONL reads with indexed SQLite WAL, batching display writes on a dedicated thread.  
  - **[#5017] feat(webui): show the actual fallback model** (open) — Real-time composer badge updates during model fallback, with accessibility support.

- **Bug Fixes**  
  - **[#5044] fix(pairing): treat null approved channel lists as empty** (open) — Prevents crashes when `pairing.json` has `"telegram": null`.  
  - **[#5043] fix(cron): skip null runHistory elements** (open) — Avoids `TypeError` that quarantines the entire cron store.  
  - **[#5042] fix(cron): default null schedule** (open) — Falls back to `kind=every` instead of crashing.

### 4. Community Hot Topics
- **[#5000] [OPEN] Proposal: evolve subagent system toward multi-agent collaboration**  
  *Comments: 4 | Updated: 2026-07-22*  
  This issue is the most actively discussed feature request. The author argues the current subagent system is too simplistic (background task delegation without persistent identities, shared state, or inter-agent negotiation). The underlying need is for true multi-agent orchestration—agents that can debate, hand off tasks, and share evolving context. This could be a v2 milestone candidate.

- **[#4934] [CLOSED] Qwen models expose thinking/reasoning content**  
  *Comments: 2 | Updated: 2026-07-22*  
  A closed bug where Qwen models via DashScope displayed internal reasoning tokens in chat responses. The fix likely involved stripping `reasoning_content` fields before returning responses. Users relying on Qwen for production should verify this is resolved.

- **[#5041] [OPEN] Bug: completed no-op Dream batches starve later history**  
  *Comments: 0 | New: 2026-07-22*  
  A critical memory-system bug where a completed Dream run with no durable-memory diff fails to advance `.dream_cursor`, causing the same batch to be selected repeatedly and starving later history. Distinct from prior issue #4055.

### 5. Bugs & Stability

| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **Critical** | [#5041] Dream cursor not advancing | Stale batch selection starves memory history indefinitely | No |
| **High** | [#5040] MCP tool schema `$ref` disables Kimi/Moonshot | Non-`#/$defs/` JSON pointers crash strict providers | No |
| **High** | [#5042] null schedule crashes cron store | Null `schedule` fields quarantine sibling jobs | Yes ([#5042]) |
| **High** | [#5043] null runHistory crashes cron store | Null entries in `state.runHistory` raise `TypeError` | Yes ([#5043]) |
| **Medium** | [#5044] null channel lists crash pairing | `"telegram": null` raises `TypeError` on load | Yes ([#5044]) |
| **Medium** | [#5045] Slack: fenced markdown tables mangled | Code-fenced tables rewritten to key/value lines | Yes ([#5045]) |
| **Medium** | [#5046] Feishu: fenced markdown tables split | Tables inside code fences become real card `table` elements | Yes ([#5046]) |
| **Low** | [#4948] WebUI loses visibility on late subagent completion | System turn starts without WebUI lifecycle | No |

*Ranked: Critical (data loss/starvation), High (crash/store quarantine), Medium (incorrect output), Low (UI/UX degradation).*

### 6. Feature Requests & Roadmap Signals
- **Multi-agent evolution** ([#5000]) — The most ambitious request. If accepted, this would reshape the agent architecture toward persistent identities and inter-agent negotiation. Likely a v2 feature.
- **Parallel Search MCP preset** ([#5047]) — A lightweight, free search integration for users wanting web capabilities without API keys. High likelihood of inclusion in next release.
- **Idle compaction interval configurable** ([#5036]) — A user running NanoBot on Raspberry Pi flagged constant 30-40% CPU usage. Making the compaction scan interval configurable improves low-power/edge deployments. Likely to be merged quickly.
- **OAuth status and expiry warnings** ([#4689]) — Ongoing work to surface OAuth provider status in CLI, WebUI, and runtime. This addresses a common user pain point of silent token expiry.

**Prediction for next release:** Expect the xAI Grok integration ([#5035]), multi-bot Telegram support ([#5033]), and the cron/pairing crash fixes ([#5042], [#5043], [#5044]) to be included. The Dream cursor fix ([#5041]) is likely a hotfix candidate.

### 7. User Feedback Summary
- **Pain Point — MCP schema incompatibility with strict providers** ([#5040]): Users on Kimi/Moonshot are blocked when tools have non-standard `$ref` schemas. Feedback indicates frustration that one misconfigured tool can disable the entire model.
- **Pain Point — Dream memory starvation** ([#5041]): A clean no-op Dream run silently breaks future memory operations. Users relying on durable memory for long-term context are affected.
- **Pain Point — Media/workspace path conflicts in Feishu** ([#5028]): Chinese-speaking users report files uploaded via Feishu become inaccessible when workspace restrictions are enabled. The bug suggests a design tension between security boundary enforcement and cross-platform file access.
- **Satisfaction — Multi-bot Telegram support** ([#5033]): The PR received positive engagement, indicating real demand for managing multiple Telegram bots from a single WebUI.
- **Satisfaction — Fallback model visibility** ([#5017]): WebUI users wanted clear indication when a model falls back; this PR directly addresses that UX gap.

### 8. Backlog Watch
- **[#2584] [OPEN] Feature/xiaozhi support** — *Updated: 2026-07-23 | Created: 2026-03-28*  
  A 4-month-old PR adding ESP32 voice gateway support. Still open with no recent maintainer activity. This is a significant hardware integration that could broaden NanoBot’s use in IoT/voice scenarios.

- **[#4494] [OPEN] PWA support and mobile swipe gesture** — *Updated: 2026-07-22 | Created: 2026-06-24*  
  A mobile UX enhancement PR now open for ~1 month. No maintainer review yet. Good candidate for triage in the next maintainer cycle.

- **[#4689] [OPEN] OAuth status and expiry warnings** — *Updated: 2026-07-22 | Created: 2026-07-03*  
  A 20-day-old feature PR with no merged status. Important for providers with transient tokens; users are likely waiting on this.

- **[#4439] [OPEN] Feat(tools): add read-only search_history tool** — *Updated: 2026-07-22 | Created: 2026-06-21*  
  A one-month-old feature PR for memory recall. Not merged yet despite closing a linked issue. May need rebase or maintainer review.

---

*Generated 2026-07-23 | Data source: github.com/HKUDS/nanobot*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the project digest for **Hermes Agent**, generated from the provided GitHub data for **2026-07-23**.

---

# Hermes Agent Project Digest — 2026-07-23

## 1. Today's Overview
The project is experiencing a **high level of development and community activity**, with 50 Issues and 50 PRs updated in the last 24 hours. The majority of Issues (46) remain open, indicating an active triage and feature pipeline, while a modest 4 were closed. The PR queue is also heavily weighted toward open work (44 open vs. 6 merged/closed), suggesting a large volume of work-in-progress contributions. Although no new releases were published today, the project shows strong momentum in bug fixing, feature development, and infrastructure hardening, particularly around session state management, gateway reliability, and desktop application stability.

## 2. Releases
**None.** No new releases were recorded for this date. The latest available version remains `v2026.7.1-525-g1ea0bbbb0`, as referenced in Issue #63395.

## 3. Project Progress
Six PRs were merged or closed today, representing progress across several areas:
- **Desktop Session Behavior:** Two bugs were closed. **PR #69721** (`feat(relay): egress typing indicators through the connector`) was merged, adding "Hermes Agent is typing…" indicators to relay-fronted platforms (Slack, etc.) during processing.
- **Desktop UI Fixes:**
    - **#68302 [CLOSED]**: Fixed a bug where clicking a sidebar session had no effect while the "Skills & Tools" view was active.
    - **#68979 [CLOSED]**: Addressed a rendering issue in long threads where user messages would stack at the bottom after context compression.
- **Delegation Feature:** **#69694 [CLOSED]** (`feat(delegation): allow per-task model selection in delegate_task`) was merged, enabling users to assign different models to different sub-agents within a single batch task.
- **Active Fix PRs:** A new PR, **#69725** (`fix(desktop): preserve active correction on warm resume`), was opened to fix a desktop warm-resume race condition where submitted corrections were lost if the user switched sessions.

## 4. Community Hot Topics
The following Issues and PRs generated the most community discussion (comments and reactions), revealing key user needs:

- **[#4335] Cross-platform session context sharing (CLI ↔ Telegram)**
    - **Comments: 9 | 👍: 2**
    - [View Issue](https://github.com/NousResearch/hermes-agent/issues/4335)
    - **Analysis:** This is a long-standing feature request with high engagement. Users want a seamless experience across platforms (CLI, Telegram, Discord) where an agent's memory and conversational context are unified. The underlying need is for a **persistent, cross-channel user identity and session store**, which would represent a major architectural enhancement for the gateway.

- **[#66875] Desktop: Latest session does not switch after navigating to Plugins/Artifacts tab**
    - **Comments: 7 | 👍: 0**
    - [View Issue](https://github.com/NousResearch/hermes-agent/issues/66875)
    - **Analysis:** A high-frustration UX bug. Users expected a simple click on the most recent session to work, but a silent state conflict prevented the switch. This highlights the criticality of the session selection logic in the new desktop UI. A fix PR (**#66880**) is already open.

- **[#12238] Built-in Automatic Backup & Version Control for Agent Data**
    - **Comments: 5 | 👍: 19**
    - [View Issue](https://github.com/NousResearch/hermes-agent/issues/12238)
    - **Analysis:** The highest-reacted issue by a wide margin. Users are deeply concerned about losing their agent's learned state (memories, skills, history). This signals a strong desire for **data durability and rollback capabilities**, which is a core requirement for users who are investing time in "training" their personalized agent.

## 5. Bugs & Stability
Several critical and high-severity bugs were reported today or are under active discussion:

- **Critical (P0):**
    - **[#69704] [PR]**: `fix(agent): support stable cross-session prefix caching on Anthropic`. This major fix targets Anthropic prompt cache misses, which degrade performance and increase costs across sessions. A P0 label indicates it is the team's top priority.

- **High (P2):**
    - **[#69551]**: Desktop SSH remote mode breaks with non-default profiles. The client hardcodes a path to `~/.hermes/desktop-ssh`, but profile-scoped validation uses a different `HERMES_HOME`. This blocks a core remote-access feature for multi-profile users.
    - **[#69716] [PR]**: `fix(gateway): restore relay streaming and Slack command delivery`. This addresses a regression where Slack traffic through a relay lost streaming edits, thinking state, and command execution.

- **Medium (P3):**
    - **[#69660]**: Queued messages appear in thread history with a timer instead of a dedicated queue drawer, confusing users about their message status.
    - **[#47930]**: Windows Desktop active session arc-border animation is static, losing a key UX affordance that shows the agent is working.

**Note:** Multiple fix PRs exist for the most critical session-state issues (e.g., #69704, #69716, #66880), indicating a strong response from the development team.

## 6. Feature Requests & Roadmap Signals
User requests today point toward three major roadmap themes:

1.  **Advanced Delegation & Isolation:** **#69694 (Merged)** and **#66268 (Open)** signal a move toward more granular control over sub-agents, including per-task model selection and toolset isolation for security.
2.  **Observability & Diagnostics:** **#64536 [PR]** (`feat(monitoring): gateway health & diagnostics OTLP export`) and **#69717 [PR]** (`feat(cli): compare prompt size across profiles`) indicate a push for enterprise-grade monitoring and operator tooling. These are likely candidates for the next minor/major release.
3.  **Cross-Session & Cross-Platform Continuity:** The hot topic **#4335** demands a unified context. While complex to implement, its sustained engagement suggests it remains a high-value target for a future `v2026.8.x` or `v2026.9.x` release.

## 7. User Feedback Summary
- **Pain Points:**
    - **Session Management Confusion:** Users are frustrated by desktop bugs where session clicks don't work (#66875) and where thread rendering breaks after compression (#68979).
    - **Silent Failures:** The "Silent context-overflow" bug (#62708) is a major pain point—users receive no warning when the agent's context is blocked from compressing, leading to a broken agent with no explanation.
    - **Platform-Specific Issues:** macOS users report Homebrew shadowing (#45279), Windows users report file locking (#57775), and Dvorak keyboard users find shortcuts broken (#46369).
    - **Data Safety:** The high reaction count on #12238 shows users are anxious about losing their agent's "personality" and learned state.
- **Use Cases:**
    - **Power Users & Developers:** Running custom providers (#66329), using SSH remote mode (#69551), and performing PR reviews with parallel model sub-agents (#69694).
    - **Multi-Platform Users:** Wanting to start a conversation on Telegram and finish it on CLI (#4335).

## 8. Backlog Watch
The following items have **high feedback/impact** but lack recent maintainer action or a clear "needs-decision" resolution:

- **[#4335] Cross-platform session context sharing**
    - [View Issue](https://github.com/NousResearch/hermes-agent/issues/4335)
    - **Age:** Since 2026-03-31 (~4 months). Despite 9 comments and being labeled `needs-decision`, this foundational feature has no linked PR or milestone.

- **[#12238] Built-in Automatic Backup & Version Control**
    - [View Issue](https://github.com/NousResearch/hermes-agent/issues/12238)
    - **Age:** Since 2026-04-18 (~3 months). It is the highest-user-reaction issue (👍 19) but lacks a confirmed roadmap or maintainer comment.

- **[#21341] nixosModule `documents` option installs files to wrong paths**
    - [View Issue](https://github.com/NousResearch/hermes-agent/issues/21341)
    - **Age:** Since 2026-05-07 (~2.5 months). A persistent packaging bug for NixOS users that prevents correct loading of personality/memory files. This is a blocker for the NixOS community.

- **[#44845] Clarify prompts should be durable ID-addressable decisions, not short blocking timers**
    - [View Issue](https://github.com/NousResearch/hermes-agent/issues/44845)
    - **Age:** Since 2026-06-12 (~1.5 months). A core architecture discussion with a `needs-decision` label that has not seen recent maintainer input.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for 2026-07-23.

---

## PicoClaw Project Digest
**Date:** 2026-07-23
**Source:** github.com/sipeed/picoclaw

### 1. Today's Overview
Project activity is moderate, with 4 open issues and 5 pull requests receiving updates in the last 24 hours. The maintainers are actively merging documentation fixes and dependency updates (Go and x/text), indicating a focus on code hygiene and security compliance. However, three of the open PRs have gone stale, and the backlog contains two long-standing bugs that have not received maintainer attention in over a week. While no new releases were published, the community is surfacing specific integration bugs (Matrix, IRC, DingTalk) that suggest the project is scaling its channel support but encountering edge-case stability issues.

### 2. Releases
**No new releases today.** The latest version remains the tag associated with **v0.3.1** (referenced in Issue #3258). The backlog of several stale but significant features (e.g., Bedrock caching) suggests an upcoming minor release may be on the horizon.

### 3. Project Progress
One pull request was **merged/closed** today:

- **PR #3285 (Closed): [docs: remove picopaw](https://github.com/sipeed/picoclaw/pull/3285)** – A revert of a prior documentation change (#3096). This suggests a minor cleanup or correction in the project's docs/website files, likely removing a defunct reference to "picopaw."

No feature-level merges occurred today.

### 4. Community Hot Topics

- **#3203 [BUG] Matrix sync loop has no reconnection logic** – *5 comments, 2 👍*
  - **Link:** [Issue #3203](https://github.com/sipeed/picoclaw/issues/3203)
  - **Analysis:** This is the most active thread. The community is deeply concerned about a "silent death" scenario where the Matrix bridge fails after any network disruption. The core pain point is that the process remains alive, defeating systemd auto-restart. This indicates a critical reliability gap for users running PicoClaw in production with Matrix homeservers. The 5 comments suggest users are collaborating on workarounds but require an upstream fix.

- **#3222 [PR] refactor(deltachat): cleanup implementation** – *Stale (last updated 2026-07-22)*
  - **Link:** [PR #3222](https://github.com/sipeed/picoclaw/pull/3222)
  - **Analysis:** A significant -200 LOC cleanup of the DeltaChat integration. While stale, its update yesterday suggests it is still being reviewed. The refactor removes legacy features and hardcoded relay lists, signaling a drive for maintainability. Community users waiting for a stable DeltaChat bridge are likely following this.

- **#3287 [Feature] Better support long messages in IRC** – *0 comments but new (created 2026-07-22)*
  - **Link:** [Issue #3287](https://github.com/sipeed/picoclaw/issues/3287)
  - **Analysis:** A fresh feature request that highlights a fundamental protocol mismatch. IRC splits long messages, but PicoClaw currently treats each split part as a separate message. The need here is for message reassembly—a likely prerequisite for any serious IRC bridge user.

### 5. Bugs & Stability

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **Critical** | [#3203](https://github.com/sipeed/picoclaw/issues/3203) | Matrix `/sync` loop dies silently after network disruption; no reconnection logic; systemd restart fails. | No |
| **Medium** | [#3258](https://github.com/sipeed/picoclaw/issues/3258) | `before_tool` Process Hook bug: `decision` field discarded, args misparsed due to deserialization defect. | No |
| **Medium** | [#3286 (PR)](https://github.com/sipeed/picoclaw/pull/3286) | Go and `x/text` vulnerability fix via `govulncheck`. | ✅ PR is open and being reviewed |
| **Low** | [#3283 (PR)](https://github.com/sipeed/picoclaw/pull/3283) | DingTalk: missing support for inbound image/picture messages. | ✅ PR is open |

**Top Concern:** The Matrix reconnection bug (#3203) is the most severe unresolved stability issue. It breaks the core Matrix channel without any error reporting, leading to silent failures that are invisible to operators.

### 6. Feature Requests & Roadmap Signals

Several requests point toward a **v0.4.0** scope:

1. **Stateless/No-History Gateway Mode** ([#3257](https://github.com/sipeed/picoclaw/issues/3257)) – Users want ephemeral sessions in `picoclaw gateway` similar to the `--session` flag in CLI mode. The current derivation from channel/chat ID forces statefulness. **Likely in next version?** Yes—high user demand, clean feature scope.

2. **Bedrock Prompt Caching** ([PR #3163](https://github.com/sipeed/picoclaw/pull/3163)) – Though stale, this PR leverages AWS Converse API cache points for cost savings (~0.1x read pricing). **Likely in next version?** Low (stale), but valuable for AWS users.

3. **IRC Long Message Reassembly** ([#3287](https://github.com/sipeed/picoclaw/issues/3287)) – A protocol-level fix for IRCv3. **Likely in next version?** Possible, as it closes a basic usability gap.

### 7. User Feedback Summary

- **Pain Point #1 – Matrix reliability:** Users are experiencing production outages due to the missing reconnection logic (#3203). The workaround requires manually monitoring and restarting the agent.
- **Pain Point #2 – Gateway session control:** Users find the lack of stateless mode in `picoclaw gateway` restrictive for scripting and integration scenarios (#3257).
- **Pain Point #3 – IRC usability:** The project’s IRC channel support is cited as "unintelligent" due to the split-message issue (#3287), suggesting dissatisfaction with the current UX.
- **Satisfaction signal:** The community is actively contributing fixes (DingTalk images, Go vuln fix) and participating in PR reviews, indicating a healthy developer ecosystem despite the bugs.

### 8. Backlog Watch

The following items have gone **stale** (no maintainer activity in >7 days) but remain important:

- **Issue #3258 – `before_tool` hook bug** (last updated 2026-07-22) – Blocks users from customizing tool calls. A core hook functionality defect.
  - [Link](https://github.com/sipeed/picoclaw/issues/3258)
- **Issue #3257 – Stateless gateway mode** (last updated 2026-07-22) – High-demand feature request with no maintainer response.
  - [Link](https://github.com/sipeed/picoclaw/issues/3257)
- **PR #3163 – Bedrock prompt caching** (last updated 2026-07-22) – A significant feature PR that has been open for 30 days with no updates from maintainers.
  - [Link](https://github.com/sipeed/picoclaw/pull/3163)
- **PR #3222 – DeltaChat refactor** (last updated 2026-07-22) – -200LOC cleanup that reduces maintenance burden.
  - [Link](https://github.com/sipeed/picoclaw/pull/3222)

**Watch Item:** The Matrix sync loop bug (#3203) is not stale but has no fix PR yet. If it remains unaddressed for another week, it should be elevated to critical project risk status.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-23

## Today's Overview
Project activity is moderate with 3 pull requests updated and 1 open issue in the last 24 hours. No new releases were published. Community contributions continue across platform integration (Telegram rich messages, WhatsApp fixes) and utility skills (Waybar status indicator). The single security-related open issue (#3118) raises a documentation accuracy concern that may require maintainer clarification. Overall project health appears stable with steady contribution flow, though the absence of any merged PRs today suggests a lull in commit activity.

## Releases
No new releases today.

## Project Progress
No PRs were merged or closed in the last 24 hours. All 3 open PRs remain in review:

- **#3070** — *Fix WhatsApp sender identity divergence between Baileys and Cloud paths* — Addresses a bug where the same phone number maps to different user IDs depending on the channel path (native vs cloud). Remains open for 7 days.
- **#3117** — *feat(skill): add-omarchy-statusbar — Waybar status indicator for NanoClaw* — New utility skill for Linux desktop status monitoring. Follows guidelines and is in early review.
- **#2877** — *feat(telegram): native rich rendering via Bot API 10.1 sendRichMessage* — Long-standing feature PR (26 days) adding rich message format support. Still open and awaiting further review or testing.

## Community Hot Topics
- **[#3117](https://github.com/nanocoai/nanoclaw/pull/3117)** — *Waybar status indicator skill* (👍: 0) — One of two new skill submissions today, indicates growing interest in desktop integration and monitoring use cases.
- **[#2877](https://github.com/nanocoai/nanoclaw/pull/2877)** — *Telegram rich rendering* (👍: 0, open 26 days) — Despite low reaction count, this PR's longevity suggests it may be complex or blocked. Community need for native rich message rendering in Telegram is clear.
- **[#3070](https://github.com/nanocoai/nanoclaw/pull/3070)** — *WhatsApp identity divergence* (👍: 0) — Bug-fix PR addressing a core identifier consistency issue that could affect multi-channel deployments.

**Underlying needs**: Users are seeking (1) improved cross-platform message rendering, (2) consistent identity management across WhatsApp channel paths, and (3) desktop integration via utilities like Waybar.

## Bugs & Stability
One bug-related issue remains open, ranked *Medium severity*:

- **[#3070](https://github.com/nanocoai/nanoclaw/pull/3070)** — *WhatsApp sender identity divergence* — **Severity: Medium**. Bug causes different user IDs for same phone number depending on path (Baileys vs Cloud), potentially breaking message routing, history continuity, and per-agent policies. A fix PR exists and is under review.

No crash, regression, or production-blocking bugs were reported today.

## Feature Requests & Roadmap Signals
- **Skill ecosystem expansion**: Two new skill-focused PRs (#3117: Waybar status, #2877: Telegram rich messages) signal demand for broader desktop integration and richer messaging. Expect utility skills and channel improvements in next release.
- **Security documentation correction**: Issue [#3118](https://github.com/nanocoai/nanoclaw/issues/3118) requests clarification on credential isolation claims. This may not directly affect code but could impact adoption for organizations with strict security requirements.

**Prediction**: Next minor release may include the WhatsApp identity fix (#3070) and at least one of the pending skill PRs (#3117 or #2877) if reviews conclude favorably.

## User Feedback Summary
- **Pain point**: Inconsistent WhatsApp identity mapping between Baileys and Cloud paths (#3070) — a concrete integration bug affecting users running hybrid setups.
- **Use case**: Desktop monitoring via Waybar (#3117) — indicates interest in headless/desktop agent status visualization.
- **Documentation/trust concern**: Issue [#3118](https://github.com/nanocoai/nanoclaw/issues/3118) highlights a discrepancy between documented security claims and actual behavior for OAuth on self-hosted gateways. This is a potential trust issue for security-conscious adopters.

## Backlog Watch
No long-unanswered issues or PRs requiring immediate maintainer attention were identified. All open items have been updated within the last 7-26 days.

- **#2877** (*Telegram rich rendering*, open 26 days) is the longest-open PR but has been updated recently (2026-07-22), indicating it is not forgotten. Maintainers should prioritize a final review decision to avoid contributor frustration.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-23

## 1. Today's Overview
The NullClaw project saw low activity in the past 24 hours, with exactly one issue closed and one pull request merged. No new releases were cut, and there are no open issues or PRs currently awaiting action. The single closed issue describes a critical Discord gateway deafness bug (Issue #977), which was resolved by a merged PR that fixes a resource-constrained stack overflow problem. Overall, the project is in a maintenance and stability phase, with a focus on closing high-severity bugs rather than adding new features.

## 2. Releases
No new releases were published today. The most recent release remains unchanged.

## 3. Project Progress
One pull request was merged and closed today:

- **PR #978** — *discord: run typing thread on the heavy runtime stack*  
  Author: Tetraslam | [GitHub Link](https://github.com/nullclaw/nullclaw/pull/978)  
  This PR fixes a process-aborting crash caused by the Discord typing-indicator thread running on an insufficiently sized stack (512KB) while performing full HTTPS requests. The thread now uses the heavy runtime stack, preventing stack overflow from `std.crypto.tls` operations. This directly resolved the underlying cause of Issue #977.

## 4. Community Hot Topics
Only one discussion item saw community activity today:

- **Issue #977** — *Discord gateway goes permanently deaf after exactly one MESSAGE_CREATE*  
  Author: Tetraslam | Comments: 1 | [GitHub Link](https://github.com/nullclaw/nullclaw/issues/977)  
  This issue, filed and closed on the same day, describes a reproducible bug where the bot processes exactly one inbound message before becoming permanently deaf (heartbeats continue but no further events are dispatched). The single comment thread appears to confirm the fix via PR #978. Underlying need: reliable long-running Discord gateway event handling without silent failure.

## 5. Bugs & Stability
One critical stability bug was reported and resolved today:

- **Severity: Critical** — *Discord gateway permanent deafness after one MESSAGE_CREATE*  
  Issue #977 reported that the bot remains online (heartbeat OK) but silently discards all subsequent Discord events after processing one message. Root cause was a stack overflow in the typing-indicator thread causing undefined behavior.  
  **Fix exists:** Yes — PR #978 (merged) moves the thread to a larger stack.  
  No other crashes, regressions, or new bugs were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed or discussed today. The activity indicates the immediate roadmap focus is stability and reliability of the Discord gateway integration. Future versions may include:
- More robust thread/stack management for background tasks
- Possibly increased default stack sizes for network-bound coroutines

No user-requested features were visible in today's data.

## 7. User Feedback Summary
With only one closed issue and one merged PR, user feedback is minimal but telling:
- **Pain point:** A silent, non-obvious failure mode where the bot appears online but no longer responds to messages. This is highly disruptive for production bots.
- **Satisfaction:** The quick turnaround (issue to fix in <24 hours) suggests responsive maintainer support. No negative feedback was recorded.
- **Use case:** The bug affected all Discord-connected instances — any bot using the gateway integration was vulnerable.

## 8. Backlog Watch
No outstanding issues or PRs currently require maintainer attention. All items from the last 24 hours were either closed or merged. The active backlog appears clean.

---

*Disclaimer: This digest is based solely on GitHub activity from the past 24 hours and may not reflect broader community discussions or roadmap planning. All links point to https://github.com/nullclaw/nullclaw.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-23

## 1. Today's Overview

IronClaw shows **very high activity**, with 50 issues and 50 PRs updated in the last 24 hours, indicating a team working intensively toward a **v1 launch**. 36 issues remain open/active, while 23 PRs were merged or closed. The project is in a **stability and polish phase**, with several "v1-launch-checklist" and "bug_bash" tagged items surfacing real user-facing regressions, particularly around Telegram and Google OAuth. The v1 launch is imminent but blocked by critical channel delivery and configuration bugs. No new releases were cut today.

## 2. Releases

**None.** No new releases were created in the last 24 hours. The latest release remains from the `chore: release` PR #5598 (July 3, 2026), which contained breaking changes to `ironclaw_common` and `ironclaw_skills`.

## 3. Project Progress

**Merged/closed PRs today (23 total):** Significant architectural and testing progress was made:

- **ProductSurface routing** — PR #6441 (merged) named the `ProductSurface` boundary and PR #6444 (merged) refreshed the routing design docs. PR #6480 and #6536 (open) continue this migration.
- **Testing infrastructure** — PR #6535 (closed, merged) added a Slice 0 reference model for turn/run lifecycle oracles. PR #6528, #6525, #6526 (all open) add typed provider operation cases, mutable Emulate provider worlds, and provider capability coverage inventory.
- **Container deployment** — PR #6533 (open) fixes container-supervised mode for hosted Docker deployments, a verified live bug.
- **Extension stability** — PR #6520 (open) makes extension readiness and channel delivery generic.
- **Security foundation** — PR #6527 (open) adds admin-managed user security with private/tenant-managed content-access policies.

**Closed foundational retrospective issues (from `completed foundation` series):** #6519 (testing playbook), #6515 (operator config write plane), #6514 (generic extension runtime), #6513 (per-user extension lifecycle + OAuth), #6510 (unified web-gateway thread model), #6505 (Slack routing/delivery), #6499 (Telegram production image), #6498 (Telegram Reborn channel), #6495 (unified generic extension runtime), #6494 (manifest-driven extension ingress), #6493 (extension manifest registry), #6489 (host-managed memory retrieval).

## 4. Community Hot Topics

The most active discussions center on **error recoverability and system reliability**:

- **[#6284 — EPIC: error-recoverability endgame](https://github.com/nearai/ironclaw/issues/6284)** (4 comments) — Proposes a contract where every mid-run error must survive, be visible to the model, include cause and remedy, and give the model a turn to act. This is a high-level design goal for making the agent self-healing. PR #6530 and #6467 are implementing bounded warning turns and model error observations.

- **[#6105 — Extension/channel lifecycle state-machine test](https://github.com/nearai/ironclaw/issues/6105)** (3 comments) — Highlights that Slack lifecycle bugs have regressed across **four QA bug-bash waves** despite multiple fixes. This indicates a systemic testing gap, which the new Slice 0 reference model and hermetic testing platform (#6524) aim to close.

- **[#5459 — Configurable skills and tools](https://github.com/nearai/ironclaw/issues/5459)** (2 comments) — A long-standing request for admin vs. user installation of WASM tools and skills, with visibility controls. This is foundational to the tenant governance model being built in PR #6527.

## 5. Bugs & Stability

**High severity (P1):**

- **[#6475 — Telegram /pair command not recognized](https://github.com/nearai/ironclaw/issues/6475)** (bug_bash_P1) — Users are trapped in a pairing loop; the agent treats `/pair` as ordinary text. This blocks Telegram onboarding entirely. No fix PR identified yet.

- **[#6474 — Telegram delivery channel not configurable in Delivery Defaults](https://github.com/nearai/ironclaw/issues/6474)** (bug_bash_P1) — The Delivery Defaults page only offers "Web app only" with no way to select Telegram or Slack. This is a UX gap for external channel configuration.

**Medium severity (P2):**

- **[#6478 — Agent does not recognize connected Telegram, redirects to Slack](https://github.com/nearai/ironclaw/issues/6478)** (bug_bash_P2) — Even with Telegram connected, the agent tries to authorize Slack instead. This suggests channel routing/detection is broken.

- **[#6523 — Agent fails to create during onboarding if testing flag is set](https://github.com/nearai/ironclaw/issues/6523)** (v1-launch-checklist) — selecting "test build" flag causes deployment failure.

- **[#6534 — Google OAuth config can't be applied in hosted deployments](https://github.com/nearai/ironclaw/issues/6534)** — Operator can save config but it is not applied at runtime. PR #6531 (open) aims to fix this by resolving OAuth client credentials from tenant-scoped config at runtime.

**Low severity / infrastructure:**

- **[#6521 — ironclaw CLI not available on agent staging](https://github.com/nearai/ironclaw/issues/6521)** (closed) — CLI missing from staging SSH sessions.

## 6. Feature Requests & Roadmap Signals

**Features most likely to ship in the next release (v1.0.0):**

1. **Error recoverability** — #6284 epic + PRs #6530 and #6467 are implementing bounded pre-termination warnings and model error observations. This is a v1-blocker for "recover from 100% of errors."

2. **Hermetic testing platform** — #6524 epic aims to answer "does every capability have deterministic coverage?" This is essential for v1 release confidence given the history of regression.

3. **Attested signing / Ledger wallet support** — #6532 proposes blockchain transaction capability where the agent cannot move money unilaterally. This is a design-phase item, unlikely for v1 but a strong differentiator.

4. **Telegram as first-class channel** — The completed foundation PRs (#6499, #6498) show Telegram is production-ready, but bugs #6474/#6475/#6478 show it's not yet usable. Fixing these is a v1 launch blocker.

**Predictions for next version:** v1.0.0 will likely include error recovery, hermetic testing, Telegram channel fixes, and Google OAuth runtime application.

## 7. User Feedback Summary

**Major pain points:**

1. **Telegram pairing is broken** — Users cannot complete the pairing flow; the `/pair` command is not recognized, and the agent redirects to Slack instead. This is the top user-facing blocker.

2. **External channel configuration is missing** — The Delivery Defaults page has no option to configure Telegram or Slack, contradicting in-agent instructions that tell users to go there.

3. **Onboarding fails with test builds** — The "test build" flag during agent creation causes silent deployment failure (#6523).

4. **OAuth configuration is not applied** — Google integration cannot be configured in hosted deployments; saved config is ignored (#6534).

5. **No CLI on staging** — Operators cannot use CLI commands on agent-stg.near.ai (#6521, now closed but unresolved for users).

**Satisfaction signals:** The rapid closure of 14 foundational retrospective issues suggests the team is methodically tracking delivery history and building confidence in the architecture.

## 8. Backlog Watch

**Issues needing maintainer attention (long-open, high impact):**

- **[#1330 — Tool schema discovery: expose message routing and attachment semantics](https://github.com/nearai/ironclaw/issues/1330)** (created March 18, last updated July 22, 1 comment) — The `message` tool schema lacks clarity on routing defaults and attachment constraints. This has been open for 4 months and is tagged `on hold`. It directly affects the model's ability to use messaging tools correctly.

- **[#2246 — Unify extension model: MCP tools as single-tool extensions + provider dedup](https://github.com/nearai/ironclaw/issues/2246)** (created April 10, last updated July 22, 1 comment) — MCP servers flood the tool list and multiple providers have no deduplication. This is a significant UX and performance issue that has been open for 3+ months. While PR #6520 addresses generic extension readiness, the MCP unification specifically has no active PR.

- **[#1519 — Routine notifications lack context in user's chat thread](https://github.com/nearai/ironclaw/issues/1519)** (created March 21, last updated July 22, 1 comment) — Routine notifications are isolated to a dedicated conversation, missing the user's chat thread context. This has been open for 4 months with no resolution, affecting routine-notification user experience.

These three issues represent the longest-unaddressed architectural debt with direct user impact, and none have active PRs.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for July 23, 2026.

---

## LobsterAI Project Digest
**Date:** 2026-07-23
**Source:** github.com/netease-youdao/LobsterAI

### 1. Today's Overview
Project activity was high today, driven entirely by a concentrated effort to merge and close pull requests. Five PRs were closed or merged, while only one issue saw activity (a closed stale ticket). There were no new releases, indicating the team is focused on integrating recent development work rather than packaging a new version. The activity appears to be a sprint-style clean-up, addressing both recent bug fixes and long-dormant feature branches.

### 2. Releases
No new releases were published today. The project remains on its previous stable version.

### 3. Project Progress
All five updated PRs were successfully merged or closed today, signaling strong forward momentum. Key advancements include:

- **Windows Installer Security ([PR #2377](https://github.com/netease-youdao/LobsterAI/pull/2377)):** A feature was merged to harden the Windows update installer, improving platform security.
- **Co-work UI Fix ([PR #2376](https://github.com/netease-youdao/LobsterAI/pull/2376)):** A fix was merged for the co-work feature, ensuring the export modal renders correctly above the sidebar by using a body portal to avoid layout conflicts.
- **Stability Fix: OOM Crash Guard ([PR #2375](https://github.com/netease-youdao/LobsterAI/pull/2375)):** A critical stability fix was merged for the OpenClaw module to prevent out-of-memory (OOM) crashes caused by oversized transcripts. It blocks problematic turns, classifyes heap-OOM crashes, and prevents zombie reconnects.
- **Stale Feature Merges:** Two long-pending feature branches were finally closed:
    - **Skills Management ([PR #1346](https://github.com/netease-youdao/LobsterAI/pull/1346)):** A skills management feature was merged after a three-month delay.
    - **Scheduled Task Enhancement ([PR #1347](https://github.com/netease-youdao/LobsterAI/pull/1347)):** A major feature for the scheduled task module was merged, introducing custom Cron scheduling, an Agent/Model selector, and UX improvements (visual builder for cron expressions).

### 4. Community Hot Topics
The only active conversation today was on a closed issue, indicating the community was largely quiet while the team processed technical work.

- **[Issue #1348](https://github.com/netease-youdao/LobsterAI/issues/1348) (Closed): “定时任务名称重复没有校验” (No validation for duplicate scheduled task names):** This issue, created in April, was closed today as stale. It highlights a persistent user need for form validation. The lack of a fix suggests this was either deprioritized or will be addressed by the larger scheduled task overhaul merged today ([PR #1347](https://github.com/netease-youdao/LobsterAI/pull/1347)).

### 5. Bugs & Stability
One significant stability issue was addressed today:

- **High Severity: Heap Out-of-Memory Crashes in OpenClaw:** The fix in **[PR #2375](https://github.com/netease-youdao/LobsterAI/pull/2375)** directly targets a "critical" class of crash. The fix blocks oversized transcripts from causing OOM errors, classifies the crash type for better diagnostics, and prevents zombie reconnections after a restart. This is a major improvement for users managing large or complex workflow transcripts.

No other new bugs or regressions were reported in the last 24 hours.

### 6. Feature Requests & Roadmap Signals
The merging of two large, dormant PRs signals the team's intent to ship long-awaited features:

- **Custom Cron Scheduling:** The merged PR [#1347](https://github.com/netease-youdao/LobsterAI/pull/1347) confirms that a highly customizable scheduling system is now available. The inclusion of a visual builder and an Agent/Model selector suggests the roadmap for the scheduled task module is focused on power-user flexibility.
- **Skills Management:** The merge of PR [#1346](https://github.com/netease-youdao/LobsterAI/pull/1346) indicates that a formal skills management feature is now part of the main branch. This could be a foundational feature for allowing users to define and reuse agent behaviors.

These features are likely candidates for the next official release of LobsterAI.

### 7. User Feedback Summary
While direct user feedback was sparse today, the PRs address clear user pain points:

- **Pain Point (Stability):** Users experiencing crashes with long transcripts ("OOM crashes") should see an improvement with the fix in PR #2375.
- **Pain Point (Usability):** The demand for better form validation (e.g., duplicate task names, Issue #1348) remains a concern, though the new Cron scheduler may indirectly address some of these process issues.
- **Satisfaction Driver:** The long-awaited Skills Management and Custom Cron features are now merged, likely generating positive sentiment among users awaiting these capabilities.

### 8. Backlog Watch
The following items represent potentially important work that required maintainer action to close today:

- **[Issue #1348](https://github.com/netease-youdao/LobsterAI/issues/1348) (Closed/Stale):** This issue about duplicate task name validation was marked as stale and closed without a fix. While it is three months old, it remains a valid UI/UX concern. The community may re-open it if the newly merged scheduled task feature ([PR #1347](https://github.com/netease-youdao/LobsterAI/pull/1347)) does not include input validation.
- **[PR #1346](https://github.com/netease-youdao/LobsterAI/pull/1346) & [PR #1347](https://github.com/netease-youdao/LobsterAI/pull/1347) (Merged):** These were long-stalled (since April). Their closure is a positive sign of project maintenance, but it highlights that feature PRs can remain open for months. No other critical items remain in the active backlog from today's data.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-23

## Today's Overview
Project activity is light today, with only one new issue and one open PR updated in the last 24 hours. No new releases or merges occurred, suggesting a quiet maintenance or reflection period. The single active issue is a feature request with moderate community engagement (5 comments, 1 upvote), while the PR addresses a long-standing UI usability concern. Overall, Moltis appears stable but not currently under heavy development velocity.

## Releases
None, no new releases recorded.

## Project Progress
No pull requests were merged or closed today. The only PR activity is the open PR #1162, which remains unmerged. No features or bug fixes advanced beyond the PR creation stage.

## Community Hot Topics
- **#574 [Feature Request] Model Routing Per Topic** — *Open, created Apr 6, updated Jul 22*  
  *Comments: 5, 👍: 1*  
  [Issue Link](https://github.com/moltis-org/moltis/issues/574)  
  This is the most active discussion. The request proposes allowing users to assign different AI models to different conversation topics or domains (e.g., coding vs. creative writing). The underlying need is for more granular AI provider/LLM selection logic, reflecting a growing user desire to optimize cost, performance, and output style per use case without manually switching models each time.

- **#1162 [PR] fix(web): show dates for older sessions** — *Open, updated Jul 22*  
  [PR Link](https://github.com/moltis-org/moltis/pull/1162)  
  While low in comments, this PR addresses a long-standing user pain point: poor session browsing history. The fix adds proper date formatting for older conversations (yesterday, weekdays, calendar dates with year), which improves the UI for users with many saved sessions.

## Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. No stability-related issues were updated.

## Feature Requests & Roadmap Signals
The sole feature request this period is **#574: Model Routing Per Topic**. Given the moderate community interest and the growing ecosystem of diverse LLM providers, this feature may be prioritized for a future minor release (likely v1.x or early v2) to differentiate Moltis from simpler assistants. However, with no maintainer response recorded, it remains speculative.

## User Feedback Summary
No direct user feedback was captured in issues or comments today. However, the PR #1162 indirectly reflects user dissatisfaction with session history navigation, indicating that users with extensive conversation libraries want better temporal context (dates, “yesterday,” weekday labels) to quickly locate and resume specific sessions. This is a usability concern rather than a technical bug.

## Backlog Watch
**No items identified.** The oldest open issue (#574) has been active for 3.5 months but is not yet stale (updated just yesterday). All other issues and PRs are recent. No items appear to be abandoned or lacking maintainer attention. The project backlog is relatively clean.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-23

## 1. Today's Overview

CoPaw continues at a high level of activity, with 50 PRs and 31 Issues updated in the last 24 hours. The release of **v2.0.0.post4** addresses a key agent reasoning issue, but the project is simultaneously grappling with multiple regressions and quality concerns from the v2.0 transition. A significant contributor to these challenges is **patrick-andstar**, who filed 6 bug reports and submitted 8 PRs today—mostly first-time-contributor fixes—covering stability, governance, test infrastructure, and mission system hardening. While the community remains engaged with diverse feature requests, several user reports indicate that the v2.0.0.post3/post4 releases have introduced new stability problems, including process crashes and degraded responsiveness, which the maintainers will need to prioritize.

---

## 2. Releases

### **v2.0.0.post4** (New)
- **Changelog**: Optimized agent reasoning to mitigate redundant thinking loops and duplicate tool invocations.
- **Breaking Changes**: None documented.
- **Migration Notes**: No special steps required; follow standard pip upgrade (`pip install --upgrade qwenpaw`).

**Full Changelog**: https://github.com/agentscope-ai/CoPaw/compare/v2.0.0.post3...v2.0.0.post4

---

## 3. Project Progress

**Merged/Closed PRs (15 total):** Several critical fixes landed today:

| PR | Title | Status |
|---|---|---|
| [#6375](https://github.com/agentscope-ai/CoPaw/pull/6375) | fix(token-usage): retry token usage persistence | Closed |
| [#6359](https://github.com/agentscope-ai/CoPaw/pull/6359) | fix: change context injection role from system to user | Closed |

**Key Advances:**
- **Token usage reliability**: `TokenUsageBuffer` now retries on transient write failures, preventing silent data loss.
- **Context injection fix**: Persistent system-role injection mid-conversation is corrected to `user` role, fixing API compatibility with GLM/OpenAI providers.
- **Tool execution robustness**: A fix for markdown fences / XML tags in tool_call arguments (PR #6364) submitted to address #6363.
- **Console UI refinements**: PR #6357 rebalances approval dialog to prioritize "Just Once" over "Always Allow," addressing UI safety concerns (Issue #6354).

---

## 4. Community Hot Topics

### Most Active Issues

1. **[#5218](https://github.com/agentscope-ai/CoPaw/issues/5218) [CLOSED] — Sub-agent context compaction freezes QwenPaw** (18 comments)
   - **Analysis**: Root cause identified and fix merged in v2.0.0.post4. The issue involves context compression logic blocking the main process.

2. **[#6322](https://github.com/agentscope-ai/CoPaw/issues/6322) [CLOSED] — Platform domain redirects to ad pages on mobile networks** (8 comments)
   - **Analysis**: User reports ad redirects on mobile networks but not on wired connections. Likely ISP-level DNS hijacking rather than a product bug; closed without resolution.

3. **[#6314](https://github.com/agentscope-ai/CoPaw/issues/6314) [OPEN] — RemoteProtocolError: peer closed connection** (8 comments)
   - **Analysis**: Deep investigation using packet capture shows CoPaw process actively closing the connection to the LLM provider. Likely a timeout/health-check issue in the networking layer.

4. **[#6318](https://github.com/agentscope-ai/CoPaw/issues/6318) [OPEN] — Per-conversation model selection** (6 comments)
   - **Analysis**: Users want model flexibility per conversation rather than per-agent. Strong signal for multi-model workflows.

### Pull Request Activity
- **#6284** (35 comments, OPEN) — `qwenpaw-creator` app: a full script→assets→storyboard→video pipeline. High community interest.
- **#6323** (OPEN) — Staged compaction for Scroll context management. Redesign of long-context handling with SQLite as source of truth.

---

## 5. Bugs & Stability

### Critical

| Issue | Title | Severity | Fix PR |
|---|---|---|---|
| [#6376](https://github.com/agentscope-ai/CoPaw/issues/6376) | v2.0.0.post3/post4: loop feature crashes main process | **Critical** — User reports crash leads to complete process failure. | Not yet |
| [#6363](https://github.com/agentscope-ai/CoPaw/issues/6363) | tool_call arguments polluted with markdown/XML — breaks all tool execution | **Critical** — Affects GLM-5-Turbo and DeepSeek-V3 users. | [#6364](https://github.com/agentscope-ai/CoPaw/pull/6364) (open) |
| [#6324](https://github.com/agentscope-ai/CoPaw/issues/6324) | Model response truncated with MiniMax-M3 | **Critical** — Data loss in responses. | Not yet |

### High

| Issue | Title | Severity | Fix PR |
|---|---|---|---|
| [#6362](https://github.com/agentscope-ai/CoPaw/issues/6362) | MiniMax-M3: images not recognized (v2.0.0.post4) | **High** — Vision feature broken. | Not yet |
| [#6374](https://github.com/agentscope-ai/CoPaw/issues/6374) | Token usage persistence does not retry write failures | **High** — Silent data loss. | [#6375](https://github.com/agentscope-ai/CoPaw/pull/6375) (closed) |
| [#6372](https://github.com/agentscope-ai/CoPaw/issues/6372) | Idle cleanup removes newly recreated queue state | **High** — Race condition in channel message delivery. | [#6373](https://github.com/agentscope-ai/CoPaw/pull/6373) (open) |

### Medium

| Issue | Title |
|---|---|
| [#6358](https://github.com/agentscope-ai/CoPaw/issues/6358) | Context injection as role='system' causes ValueError on GLM/OpenAI APIs |
| [#6307](https://github.com/agentscope-ai/CoPaw/issues/6307) | v2.0 introduces ~2s fixed overhead per conversational reply |
| [#6370](https://github.com/agentscope-ai/CoPaw/issues/6370) | Downloader fallback broken after wget/curl timeout |
| [#6368](https://github.com/agentscope-ai/CoPaw/issues/6368) | Governance: audit_level=none still writes to SQLite |
| [#6361](https://github.com/agentscope-ai/CoPaw/issues/6361) | Console test scripts don't work on Windows |

### Regressions in v2.0.0.post3/post4
- Three separate reports of **process crashes and freezes** caused by the new loop/thinking functionality ([#6376](https://github.com/agentscope-ai/CoPaw/issues/6376), [#5218](https://github.com/agentscope-ai/CoPaw/issues/5218)).
- **~2s fixed overhead** per conversation turn not present in v1.x ([#6307](https://github.com/agentscope-ai/CoPaw/issues/6307)).

---

## 6. Feature Requests & Roadmap Signals

### High-Value Requests Likely in Next Release

- **[Per-conversation model selection](https://github.com/agentscope-ai/CoPaw/issues/6318)**: Multiple users want model flexibility per conversation rather than agent-level binding. Expected to land in v2.1 given community demand.
- **[Per-job model overrides for cron](https://github.com/agentscope-ai/CoPaw/issues/6316)**: PR [#6353](https://github.com/agentscope-ai/CoPaw/pull/6353) submitted today. Likely in v2.0.0.post5.
- **[Drag-and-drop file upload](https://github.com/agentscope-ai/CoPaw/issues/6297)**: Image, PDF, Office document support. High demand from enterprise users.

### Community-Driven Ideas

- [Docker hot-reload support](https://github.com/agentscope-ai/CoPaw/issues/6344) — Prevent container rebuild on every update (reference: AstrBot's approach).
- [Multi-user platform support](https://github.com/agentscope-ai/CoPaw/issues/6335) — Enterprise deployment with per-user accounts.
- [Explicit Node.js version specification](https://github.com/agentscope-ai/CoPaw/issues/6326) — For reproducible Console builds.

---

## 7. User Feedback Summary

### Pain Points (Dissatisfaction)

- **v2.0 stability concerns**: "Couldn't you test before release? Do some stress testing!" (Issue #6376) — multiple users report crashes from the new loop feature.
- **Performance regression**: "v2.0 introduces ~2s fixed overhead per reply" (Issue #6307) — user lululau provided detailed analysis.
- **MiniMax vision broken**: Two separate reports (#5135 from June, #6362 from today) confirm MiniMax-M3 vision still non-functional after v2.0.0.post4.
- **Model response truncation**: User fgdsfgfdsgdsfgsdfg reports data loss with MiniMax-M3 (Issue #6324).
- **Windows contributor friction**: Console test scripts fail out-of-the-box on Windows (Issue #6361).

### Use Cases Driving Requests

- **Enterprise contract review**: Drag-and-drop file upload requested for document analysis (Issue #6297).
- **Corporate agent platform**: Multi-user management with access control (Issue #6335).
- **Content creation**: The `qwenpaw-creator` app (PR #6284) points to video/media workflow ambitions.
- **Self-hosted reliability**: Docker hot-reload to retain installed tools across updates (Issue #6344).

### Positive Indicators

- Community is actively contributing **first-time patches** (8 by patrick-andstar today).
- The approval dialog UI fix (PR #6357) shows responsiveness to UX safety concerns.
- Release verification and rigor are improving (see automated release duty Issue #6338).

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Why Stalled |
|---|---|---|
| [#5135](https://github.com/agentscope-ai/CoPaw/issues/5135) — MiniMax-M3 vision broken (v1.1.11) | **42 days** | No fix despite two duplicate reports (#6362 filed today). Critical regression for MiniMax users. |
| [#6176](https://github.com/agentscope-ai/CoPaw/issues/6176) — CLI cron update resets runtime/metadata fields | **7 days** | Closed without resolution; may need re-opening. |

### PRs Awaiting Review

| PR | Title | Days Open |
|---|---|---|
| [#6284](https://github.com/agentscope-ai/CoPaw/pull/6284) | feat(apps): add qwenpaw-creator app | 2 days (35 comments) |
| [#6323](https://github.com/agentscope-ai/CoPaw/pull/6323) | feat(scroll): add staged compaction | 1 day — significant change |
| [#6311](https://github.com/agentscope-ai/CoPaw/pull/6311) | fix: share ToolGuard safety_checks and unregister on unload | 2 days |

### Recommendation

The MiniMax vision bug (#5135, #6362) and the v2.0 process crash issues (#6376) are likely to cause user churn if not addressed urgently. The maintainers should prioritize a **v2.0.0.post5** hotfix targeting the core loop stability regression and the MiniMax provider integration.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-23

## Today's Overview
ZeroClaw shows a **moderately high activity day** with 50 issues and 50 PRs updated in the last 24 hours, indicating sustained development momentum. The project currently has 40 open issues and 36 open pull requests, reflecting a healthy but sizable backlog. No new releases were published today. Critical infrastructure topics dominate: OIDC authentication, Windows platform support, and memory lifecycle architecture continue to drive the most active community discussions, while a growing cluster of PRs around Anthropic provider reliability signals a focused push toward production-grade stability.

## Releases
No new releases today.

## Project Progress
**14 PRs merged/closed** in the last 24 hours, representing advances across several subsystems:

- **Observability**: PR #8752 ([zeroclaw-labs/zeroclaw PR #8752](https://github.com/zeroclaw-labs/zeroclaw/pull/8752)) — *feat(obs): nest memory and RAG spans under the turn trace* — closes Issue #6641 by nesting `memory.*` and `rag.retrieve` OTel spans under the `gen_ai.agent.invoke` turn span. This completes the turn-level trace correlation feature for memory/RAG.

- **Reliability & Fault Tolerance**: PR #9070 ([zeroclaw-labs/zeroclaw PR #9070](https://github.com/zeroclaw-labs/zeroclaw/pull/9070)) — *fix(providers/anthropic): flush open tool_use block at message_stop* — fixes a streaming completion divergence in the Anthropic provider. PR #9169 ([zeroclaw-labs/zeroclaw PR #9169](https://github.com/zeroclaw-labs/zeroclaw/pull/9169)) — *fix(zerocode): time out stalled daemon initialization* — prevents blank terminals from unresponsive daemon connections.

- **Memory Backend Tuning**: PR #9105 ([zeroclaw-labs/zeroclaw PR #9105](https://github.com/zeroclaw-labs/zeroclaw/pull/9105)) — *fix(memory): allow Lucid ARM cold starts, make timeouts configurable* — raises default recall and store timeouts from sub-second to 3 seconds to accommodate AArch64 cold starts (~1.4-1.6 seconds).

- **CI & Release Infrastructure**: PR #9174 ([zeroclaw-labs/zeroclaw PR #9174](https://github.com/zeroclaw-labs/zeroclaw/pull/9174)) — *feat(release): add broad-channel measurement builds* — adds `dist-broad` feature selection for pre-release measurement. PR #8684 ([zeroclaw-labs/zeroclaw PR #8684](https://github.com/zeroclaw-labs/zeroclaw/pull/8684)) — *feat(runtime): surface model fallback notice on direct-turn surfaces* — records requested-vs-served provider/model for fallback transparency.

- **Firmware**: PR #8447 ([zeroclaw-labs/zeroclaw PR #8447](https://github.com/zeroclaw-labs/zeroclaw/pull/8447)) — *chore(firmware): share protocol parsing with ESP32* — standardizes protocol parsing across Pico, Nucleo, and ESP32 firmware.

## Community Hot Topics

### 💬 Most Active Discussions

1. **[Bug] 74 test failures on Windows (#7462)** — 11 comments
   - [zeroclaw-labs/zeroclaw Issue #7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)
   - *Key insight*: The community is surfacing a significant CI gap—the entire test suite is Linux-only, leaving Windows (especially Simplified Chinese locale with code page 936) as a blind spot. The 74 failures include Unix-only test commands, path semantics mismatches, and console encoding issues. This is acknowledged with `status:accepted`, `priority:p1`, and `risk:high`.

2. **[Feature] Turn-level OTel trace correlation (#6641)** — 8 comments (CLOSED)
   - [zeroclaw-labs/zeroclaw Issue #6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641)
   - *Key insight*: This was a highly collaborative feature spanning two prior issues and a PR (#8752 merged today). The community's engagement on observability signals strong interest in production-grade instrumentation.

3. **RFC: OIDC authentication provider support (#7141)** — 7 comments
   - [zeroclaw-labs/zeroclaw Issue #7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)
   - *Key insight*: This umbrella RFC for pluggable authentication is tracking toward v0.9.0, targeting enterprise/self-hosted deployments. The 7 comments reflect cross-cutting architectural discussion around security, config, daemon, and gateway.

4. **RFC: A2A agent discovery (#7218)** — 7 comments (CLOSED)
   - [zeroclaw-labs/zeroclaw Issue #7218](https://github.com/zeroclaw-labs/zeroclaw/issues/7218)
   - *Key insight*: Closed and accepted, this defines how multi-agent installations handle `/.well-known/agent-card.json` discovery, critical for interop with external agent systems.

### 🔄 Emerging PR Clusters
A notable **four-PR chain** by contributor `IftekharUddin` (PRs #9262, #9263, #9265, #9266, #9268) is systematically building Anthropic fallback capability: typed refusal errors → client-side fallback routing → server-side fallback opt-in → server-side fallback response detection → surfacing safeguard notices in channels. This represents a significant reliability investment.

## Bugs & Stability

### High Severity

- **[BUG] 74 test failures on Windows (#7462)** — `S2 - degraded behavior`
  - [zeroclaw-labs/zeroclaw Issue #7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)
  - *Status*: Open, accepted, `priority:p1`, `risk:high`. No fix PR yet. This is the highest-impact platform bug currently open.

- **[BUG] History trimming occurs silently with history pruning disabled (#8837)** — `S2 - degraded behavior`
  - [zeroclaw-labs/zeroclaw Issue #8837](https://github.com/zeroclaw-labs/zeroclaw/issues/8837) (CLOSED)
  - *Status*: Closed. Users reported mid-session context loss despite disabling history pruning. The fix was evidently deployed.

- **[BUG] Enabled Signal/Voice Call channel with empty credentials can crashloop the supervisor (#6724)** — `S3 - minor issue`
  - [zeroclaw-labs/zeroclaw Issue #6724](https://github.com/zeroclaw-labs/zeroclaw/issues/6724)
  - *Status*: Open, accepted, `priority:p3`, `risk:high`. Supervisor crashes every ~2 seconds when channel blocks are added with empty credentials.

### Medium Severity

- **[BUG] Channel runtime command replies bypass Fluent localization (#6548)** — `S3 - minor issue`
  - [zeroclaw-labs/zeroclaw Issue #6548](https://github.com/zeroclaw-labs/zeroclaw/issues/6548)
  - *Status*: Open, accepted. Hard-coded English strings appear when non-English locale is configured.

- **npm audit failed (#9235)** — Security vulnerability
  - [zeroclaw-labs/zeroclaw Issue #9235](https://github.com/zeroclaw-labs/zeroclaw/issues/9235)
  - *Status*: Updated today. 3 high/critical findings in `@redocly/openapi-core`.

- **Stale advisory ignores in dependency tree (#8781)** — Security
  - [zeroclaw-labs/zeroclaw PR #8781](https://github.com/zeroclaw-labs/zeroclaw/pull/8781)
  - *Status*: Open, needs author action. Removes 24 stale advisory ignores.

### Fix PRs in Progress
- PR #9197 ([zeroclaw-labs/zeroclaw PR #9197](https://github.com/zeroclaw-labs/zeroclaw/pull/9197)) — fixes channel supervisor restart loop during WhatsApp Web shutdown (fixes #9155)
- PR #9075 ([zeroclaw-labs/zeroclaw PR #9075](https://github.com/zeroclaw-labs/zeroclaw/pull/9075)) — fixes `models_cache.json` not being persisted after `zeroclaw models refresh`

## Feature Requests & Roadmap Signals

### Likely for v0.9.0 (based on RFC tracking and priority p1/p2 status)

1. **OIDC authentication provider support (#7141)** — `priority:p1`, tracked for v0.9.0. Enterprise-grade authentication plug-in.
2. **Per-model capability & context-window config (#7100)** — `priority:p1`. User-configurable vision/context window per model, wired into capability checks and UI indicators.
3. **Process-memory limits on shell/skill_tool subprocess execution (#6916)** — `priority:p1`. Prevents child process OOM in container environments.
4. **Agent evaluation harness (`zeroclaw eval`) (#7065)** — `priority:p2`, `status:in-progress`. Replay + live evaluation modes with pluggable graders.
5. **Decouple memory lifecycle policy from storage backends (#6850)** — `priority:p2`. `MemoryStrategy` trait for pluggable retrieval/consolidation.

### Community-Requested New Channel Integrations
- **Mastodon/ActivityPub (#6423)** — 2 comments, 1 👍. DM/mention/thread support.
- **Twilio SMS (#6427)** — 2 comments. Plain SMS for non-WhatsApp phones.
- **Rocket.Chat (#6435)** — 2 comments. Self-hosted Slack alternative.
- **Zulip (#6437)** — 2 comments. Stream/topic-threaded messaging.

### Architectural Signals
- **"Everything is a plugin" (#6489)** — CLOSED. Phased migration from separate Integrations to unified plugin catalog. Merged/closed, suggesting foundational work landed.
- **Zero-downtime config reload (#7897)** — `priority:p3`, `risk:high`. Scoped reload for security policy and channel config without full daemon restart.
- **Structured Observability Enhancement (#7232)** — `priority:p2`. Rich events, OTel trace correlation, bridge refactoring.

## User Feedback Summary

### Pain Points

1. **Windows CI blind spot** (#7462): A Chinese Windows 11 user experienced 74 test failures that CI doesn't catch. This is a real platform exclusion issue for non-Linux users.
2. **Unintended context loss** (#8837, now closed): A user reported "mid session suddenly loses its context without explanation"—critical for conversational AI reliability.
3. **Configuration friction**: Users report struggles with provider credential setup (#8925, Bedrock), channel credential validation (#6724, crashloops), and `models_cache.json` not persisting after recommended commands (#9075).
4. **Model switching confusion**: Issue #6557 (closed) addressed reconciling runtime model switching with provider structure—multiple command surfaces (`/models`, `/model`, `/config`) had inconsistent behavior.
5. **Observability gaps**: Users want channel attribution, agent aliases, and LLM input/output payloads in telemetry (#7232).

### Satisfaction Signals
- The observability work (#6641, PR #8752) completed with positive contributor engagement—contributor `alexandme` received explicit thanks from the maintainer.
- The Anthropic reliability chain (PRs #9262, #9263, #9265, #9266, #9268) demonstrates responsiveness to production deployment needs.
- The CI improvement work (#7108, `priority:p2`, `status:in-progress`) shows maintainers are investing in developer experience despite the open Windows gap.

## Backlog Watch

### Issues Needing Maintainer Attention

1. **Delete unneeded branches (#6715)** — `priority:p3`, 5 comments, open since May 16
   - [zeroclaw-labs/zeroclaw Issue #6715](https://github.com/zeroclaw-labs/zeroclaw/issues/6715)
   - *Status*: Accepted, no-stale, but no PR or assignment. 200+ stale branches pollute the repository.
   
2. **Validate config.toml in quickstart (#6416)** — `priority:p2`, 4 comments, open since May 6
   - [zeroclaw-labs/zeroclaw Issue #6416](https://github.com/zeroclaw-labs/zeroclaw/issues/6416)
   - *Status*: Accepted, no-stale. Would prevent users from hitting provider/setting incompatibilities at runtime. No PR yet.

3. **Real heartbeat tracking for daemon nodes (#6391)** — `priority:p2`, 6 comments, open since May 5
   - [zeroclaw-labs/zeroclaw Issue #6391](https://github.com/zeroclaw-labs/zeroclaw/issues/6391)
   - *Status*: Accepted, no-stale. Daemon nodes always show "Online" regardless of actual WebSocket liveness.

4. **`zeroclaw node add <url>` CLI (#6390)** — `priority:p2`, 4 comments, open since May 5
   - [zeroclaw-labs/zeroclaw Issue #6390](https://github.com/zeroclaw-labs/zeroclaw/issues/6390)
   - *Status*: Accepted, no-stale. No CLI path for daemon self-registration, despite dashboard having UI slots.

### Stale PRs Needing Action

1. **PR #9197 (fix channels restart loop)** — `needs-author-action`
   - [zeroclaw-labs/zeroclaw PR #9197](https://github.com/zeroclaw-labs/zeroclaw/pull/9197)
   - *Status*: Open since July 20, awaiting author response. Fixes a Ctrl+C crash-loop in WhatsApp Web channel.

2. **PR #9013 (refactor config!)** — `needs-author-action`, `risk:high`, `size:XL`
   - [zeroclaw-labs/zeroclaw PR #9013](https://github.com/zeroclaw-labs/zeroclaw/pull/9013)
   - *Status*: Open since July 12. Breaking change to TodoWrite display config—high impact, awaiting author.

3. **PR #9075 (fix doctor models cache)** — `needs-author-action`
   - [zeroclaw-labs/zeroclaw PR #9075](https://github.com/zeroclaw-labs/zeroclaw/pull/9075)
   - *Status*: Open since July 14. Fixes a dead-loop where recommended commands don't persist results.

---

*Digest generated 2026-07-23 from GitHub data (zeroclaw-labs/zeroclaw). Metrics: 50 issues updated, 50 PRs updated, 0 new releases.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*