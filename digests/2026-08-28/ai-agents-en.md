# OpenClaw Ecosystem Digest 2026-08-28

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-28 07:19 UTC

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

Based on the provided GitHub data for OpenClaw (github.com/openclaw/openclaw) on 2026-08-28, here is the structured project digest:

---

### 1. Today's Overview

OpenClaw exhibits a high-velocity development cycle with a "triage-then-fix" culture, as evidenced by extensive automation labels (e.g., `clawsweeper:*`, `issue-rating`) and a large volume of processed backlog. Activity is extremely high, with 500 issues and 500 PRs updated in the last 24 hours, though it's worth noting that these numbers represent the top of a very large list, likely showing a significant, perhaps overwhelming, influx of reports. The project maintains a healthy balance between bug fixing and feature development, with a strong focus on reliability for its multi-channel (Telegram, Slack, Teams, Discord) and multi-runtime (Codex, Claude, OpenAI) architecture. The presence of many open PRs "waiting on author" (e.g., #131575, #130993) suggests that while the community is highly engaged, maintainer bandwidth for review is a critical constraint.

### 2. Releases

No new releases were published for OpenClaw on 2026-08-28.

---

### 3. Project Progress

*(Based on closed/merged PRs and closed issues from the data)*

No PRs were explicitly listed with a "merged" status, but several were closed, indicating significant progress on stability and feature completeness.

- **Channel & Delivery Improvements:** PR #126424 (**fix(gateway): keep conversation delivery within agent bindings**) was closed. This large (XL) PR, tagged with high merge-risk for `message-delivery` and `security-boundary`, aimed to stop conversation tools from delivering messages outside their configured agent bindings, a crucial fix for multi-agent security and routing.
- **Control UI & Session Management:** PR #128995 (**feat: make full session actions available from chat header**) was closed, adding features like pinning, marking unread, and setting icons directly from the chat header. Additionally, PR #123535 (**fix(ui): avoid session catalog refresh storms**) was closed, resolving a performance issue causing redundant UI refreshes upon window focus.
- **Security & CLI Hardening:** PR #116489 (**feat(security): require acknowledgement for install policy warnings**) was closed, adding a new `warn` level for `security.installPolicy` that requires explicit operator acknowledgment before proceeding with risky installs. PR #128223 (**fix(cli): resolve alias targets from the write snapshot**) was also closed, fixing a bug in `openclaw models aliases add`.
- **Codex & Model Integration:** PR #125471 (**fix(models): keep Claude CLI OAuth available in Control UI**) was closed, addressing an issue where valid OAuth profiles could be misrepresented after a Gateway restart. PR #116489 also relates to the Codex integration by adding acknowledgement for security warnings.

---

### 4. Community Hot Topics

The most active discussions reveal deep concern around the **Codex runtime integration** and complex **session-state reliability**.

- **Issue #425 (Per-agent cost budget):** This top-commented issue (23 comments, 👍1) requests per-agent cost enforcement at the gateway level. The underlying need is that operators require **cost predictability and control** to prevent runaway spend, especially as they scale up agent usage.
- **Issue #125626 (2026.8.1 beta feedback):** With 22 comments, this is a release validation feedback thread. It serves as a central hub for reporting and triaging blockers and regressions specific to the current beta, indicating the community's active role in quality assurance.
- **Issue #91009 (Codex PreToolUse CPU-bound processes):** This **P0** issue (21 comments, 👍2) is a critical stability and resource leak report. Users are experiencing severe performance degradation (CPU saturation, RPC stalls) caused by the Codex native hook relay, indicating a deep integration flaw that can render a gateway unusable.
- **Issues #48003 (Steer mode injection) & #87744 (Codex Telegram timeouts):** Both are **diamond lobster**-rated reliability issues with ~20 comments each. #48003 shows that the `steer` mode, a key feature for mid-turn intervention, is broken, while #87744 highlights that Codex-backed Telegram turns fail silently without completing, causing a complete loss of response.

---

### 5. Bugs & Stability

The project is currently grappling with several severe stability bugs, primarily concentrated around the Codex runtime and session-state message loss.

- **P0 - Critical Resource Leak:** Issue #91009 (Codex PreToolUse CPU-bound processes) is a `crash-loop` and **P0** severity issue causing gateway RPC stalls. No fix PR is directly linked, though the `clawsweeper:linked-pr-open` label is absent.
- **P1 - High-Risk Bugs (No linked PRs):**
    - #87744 (Codex Telegram timeouts): Turns never complete, causing message loss. User 👍4.
    - #86215 (Codex OAuth refresh failures): Wedges agents for hours without clear alerting.
    - #100941 (WebSocket 1006 errors): Gateway drops concurrent tool-to-gateway connections under load, leading to a misleading "Gateway-crashed" error.
- **P1 - High-Risk Bugs (With Fix PRs):**
    - #106760 (Telegram pre-tool text erased): **Closed** - A fix was implemented and merged for this issue affecting multi-content-block responses.
    - #92057 (Gateway slow/timeouts under load): **Closed** - This was marked as `stale` and closed, suggesting the issue was either addressed elsewhere or deemed unreproducible, though it remains a concern.
- **P1 - Newer Regressions:**
    - #131150 (Slack DMs dropped after restart): A fresh bug reported today where `prepareSlackMessage` returns null post-gateway-restart, causing all Slack DMs to be silently dropped.

---

### 6. Feature Requests & Roadmap Signals

There are strong signals for expanding platform integrations and enhancing user-facing control surfaces.

- **Multi-Tenant/Identity Support:** Both Issue #71058 (Multiple Azure/Teams bots) and PR #112811 (feat(msteams): support multiple bot accounts) point toward a major roadmap item: **first-class support for multiple bot identities** per gateway. The open PR being in "ready for maintainer look" status suggests this is a high-priority, long-awaited feature that may land soon, though it carries high `compatibility` and `auth-provider` risks.
- **Richer UI & UX:** Several requests focus on making the TUI and Control UI more informative and less disruptive. Issues like #42840 (MathJax/LaTeX support), #44130 (TUI scroll-jump), and #51028 (sessions sorting by activity) are all aimed at either improving data presentation or fixing annoying UI behaviors.
- **Advanced Workflow & Governance:** Requests like #71712 (Agent-facing scheduling API with non-forgeable provenance) and #7338 (Agent Attestation Headers) signal a roadmap focused on **agent autonomy and security hardening**. These would formalize agent-to-agent communication and provide a foundation for a more complex agent ecosystem.
- **Platform-Specific Gaps:** PR #131592 (browser agent requests/emulate/snapshot) shows an intent to make browser control tooling more powerful and usable by agents, a key step for autonomous web tasks.

---

### 7. User Feedback Summary

- **Reliability on Codex Runtime is a Major Pain Point:** Multiple high-severity bugs (#91009, #87744, #86215) indicate that the Codex integration, while powerful, is seen as unstable in production, causing CPU spikes, silent timeouts, and OAuth wedges.
- **Desire for Greater Controller Runtime Control:** The top-voted and most-commented items demonstrate a clear need for **operational controls**: cost budgeting (#42475), persistent task-status (#52640), and clear provider-error surfacing (#51336).
- **Confusion Over Message Delivery & Session States:** Bugs like #131150 (Slack DMs dropped) and #69008 (Telegram group-bound sessions being session-only by default) highlight that users are frustrated by opaque delivery behavior and hard-to-predict session routing, especially in complex group/thread setups.
- **UI Polish Still Needed:** Issues like #44130 (TUI scroll-jump) and #124759 (iOS app lag) show that even with major features, everyday UI/UX friction and performance issues in clients remain a persistent source of dissatisfaction.

---

### 8. Backlog Watch

Several high-severity issues have been open for months and are blocked, seemingly awaiting a maintainer decision between a hack and a proper fix.

- **The "Platinum Hermit" Cluster:** Issues like #84393 (Codex base prompt injection), #90354 (Pre-compaction memory flush guardrails), and #92057 (Gateway slowness under load) are rated as high-impact `diamond lobster` or `platinum hermit` and have been open for several months. They are all tagged with `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision`, indicating they are stuck in a decision-making phase and represent a significant amount of unattended technical debt.
- **Long-Standing Feature Requests:** Issue #7338 (Agent Attestation Headers) and #41366 (Durable NL rule learning) have been open since early 2026 (Feb/Mar) and have received little-to-no visible progress. They touch on complex architectural changes (security & multi-agent state management), which likely requires a dedicated design phase.
- **In-Progress, High-Risk Fixes:** PR #131609 (fix(outbound): preserve delivery uncertainty) is explicitly marked as a draft and `review-required` by the author `steipete`, who is a maintainer. This PR is a direct response to an internal audit and is high-risk, touching on the core message-delivery layer. Its prolonged status signals a careful, necessary review process for a critical system component.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent & Personal Assistant Open-Source Ecosystem

**Date:** 2026-08-28

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is characterized by intense, concurrent development across multiple projects, with a clear shift from single-channel chat tools toward multi-platform, multi-runtime orchestration platforms. Projects are investing heavily in architectural consolidation—particularly around provider abstraction, persistent memory systems, and session-state reliability—while simultaneously addressing the operational realities of production deployments (cost control, security boundaries, and platform compatibility). The ecosystem shows a bifurcation between high-velocity, community-driven projects (OpenClaw, CoPaw/QwenPaw, NanoClaw) and more stability-focused, architecture-led efforts (IronClaw, ZeroClaw). Common pain points across all projects—channel adapter reliability, silent failure modes, and context-window management—indicate the field is maturing beyond prototypes into mission-critical infrastructure.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status (24h) | Health Score (1-10) | Notes |
|---------|---------------------|-------------------|----------------------|---------------------|-------|
| **OpenClaw** | 500 | 500 | None | 6.0 | Extremely high volume; maintainer review bottleneck; P0 Codex CPU bug |
| **Hermes Agent** | 50 | 50 | **v0.20.6** (Aug 27) | 7.0 | Healthy; ~525 PRs rolled into patch release; strong contributor ergonomics |
| **NanoBot** | 2 | 24 | None | 7.5 | Strong refactoring momentum; 9 PRs merged; stable trajectory |
| **PicoClaw** | 3 | 7 | None | 6.5 | Moderate maintenance; mostly dependency bumps; slow review cycle |
| **NanoClaw** | 11 | 50 | None | 6.0 | Major provider-contract refactor in flight; channel adapter bugs |
| **IronClaw** | 33 | 48 | None | 7.5 | High velocity; 31 PRs merged; memory system epic underway |
| **LobsterAI** | 7 | 13 | **2026.8.26** | 6.0 | Critical data-loss bug (#2561) needs immediate attention |
| **Moltis** | 0 | 2 | **20260827.01** | 7.0 | Quiet but healthy; security and API compatibility fixes |
| **CoPaw (QwenPaw)** | 31 | 50 | None (2.2.0 imminent) | 7.0 | Pre-release; 25 PRs merged; mobile client and Hub edition in progress |
| **ZeroClaw** | 29 | 50 | None (v0.8.5 freeze Aug 30) | 6.5 | Architecture RFC-heavy; PR contributor responsiveness is a bottleneck |
| **NullClaw** | 0 | 0 | None | — | No activity |
| **TinyClaw** | 0 | 0 | None | — | No activity |
| **ZeptoClaw** | 0 | 0 | None | — | No activity |

---

## 3. OpenClaw's Position

### Advantages vs. Peers

- **Massive community engagement**: 500 issues and 500 PRs updated in 24 hours dwarfs all competitors (next closest: 50 PRs). This indicates a significantly larger user base and contributor pool.
- **Multi-runtime support**: Native support for Codex, Claude, and OpenAI runtimes (plus browser agent tooling) is more extensive than any peer.
- **Automation infrastructure**: Sophisticated triage tooling (`clawsweeper:*` labels, issue-rating) suggests mature process management, though it may reflect an overloaded maintainer team.
- **Feature breadth**: Multi-bot identity support (PR #112811), per-agent cost budgets (#425), and security hardening (install policy warnings) demonstrate roadmap depth.

### Technical Approach Differences

| Dimension | OpenClaw | Peers |
|-----------|----------|-------|
| **Runtime strategy** | Multiple commercial AI runtimes unified under one gateway | Single-LLM or provider-agnostic with adapter pattern (NanoClaw, IronClaw) |
| **Channel focus** | Telegram, Slack, Teams, Discord simultaneously | Often 1–3 primary channels; CoPaw covers more but with less depth per channel |
| **Community model** | Broad, open contribution with heavy automation | More curated, maintainer-driven (IronClaw, ZeroClaw RFC process) |

### Community Size Comparison

OpenClaw is likely 10–20x larger than the median project in this ecosystem by raw activity. This creates a **quality-vs-quantity tension**: high issue/PR velocity demonstrates relevance but risks review bottlenecks, with several critical bugs (Codex P0 #91009, Codex Telegram timeouts #87744) lacking linked fixes. Competitors with smaller volumes (IronClaw, CoPaw) achieve faster bug-to-fix cycles on their most impactful issues.

---

## 4. Shared Technical Focus Areas

The following requirements emerged across multiple projects, indicating ecosystem-wide priorities:

| Requirement | Projects | Specific Needs |
|-------------|----------|----------------|
| **Memory Systems & Persistence** | IronClaw (#7276 epic, #7947-#7953), NanoBot (#5570, #5571, #5575), CoPaw (#7364), Hermes Agent (#84718, #33638), ZeroClaw (#6850) | Multi-turn memory reliability, durable cross-conversation recall, memory compaction without policy loss, pluggable memory backends |
| **Session & State Reliability** | OpenClaw (#131150, #100941), Hermes Agent (#93888), CoPaw (#7363), NanoClaw (#3568), ZeroClaw (#10408) | Session restore across restarts, serialized message processing, prevention of silent message drops, zero-downtime state reconciliation |
| **Cost Control & Visibility** | OpenClaw (#425), IronClaw (#7824), LobsterAI (#2562), CoPaw (#7316) | Per-agent/per-session budgets, token waste reduction, credit accounting clarity, cost-aware tool-output handling |
| **Provider Abstraction & Compatibility** | NanoClaw (#3581-#3592, #2136), CoPaw (#7337), ZeroClaw (#10329), Moltis (#1232), OpenClaw (#91009) | Multi-provider fallback, OpenAI/Anthropic schema compatibility, OAuth persistence, context-window overflow detection across wrappers |
| **Security Hardening** | OpenClaw (#7338, #116489), NanoBot (#5564), CoPaw (#7368, #7375), ZeroClaw (#10409, #9826), IronClaw (#1222 for Moltis variant) | Path-traversal prevention, file-guard enforcement, sandbox policy granularity, approval-flow integrity |
| **Channel Adapter Reliability** | OpenClaw (#131150), NanoClaw (#3456, #2888, #3575), CoPaw (#7370, #7302), ZeroClaw (#10237), Hermes Agent (#65522) | Discord/Telegram/WhatsApp/WeCom attachment handling, streaming consolidation, thread-scoped memory |

---

## 5. Differentiation Analysis

| Project | Core Differentiator | Target User | Primary Architecture |
|---------|---------------------|-------------|---------------------|
| **OpenClaw** | Multi-runtime (Codex/Claude/OpenAI) breadth; massive ecosystem; brand recognition | Developers/ops needing commercial AI runtime flexibility at scale | Gateway + adapters; tool-delivery semantics |
| **Hermes Agent** | Balanced stability + velocity; ~525 PRs/release; broad channel+desktop coverage | Production-first individual/team users; Desktop app users | Session+gateway model with multiplex profiles |
| **CoPaw (QwenPaw)** | **Multi-tenant Hub edition** + native mobile (Expo/React Native); strong Chinese ecosystem (DingTalk, WeCom, QQ); 2.2.0 imminent | Enterprise/team users in Asia; users needing full Chinese channel coverage | Agentscope-based; heavy on console/desktop |
| **NanoBot** | Explicit-memory-recall shift (#5571); provider fallback explicitness; clean refactoring cadence | Developers wanting lean, predictable agent runtime | Functional boundaries; tool-execution extraction; pluggable memory |
| **IronClaw** | **Persistent memory epic** (#7276); context projection; Reborn architecture migration | Ops-heavy users with Gmail/Slack workflows; cost-sensitive deployments | Producer boundaries; compaction barriers; SHA-256 memory CAS |
| **NanoClaw** | **Provider-contract refactor** (8 PRs); per-group model routing; Gemini/Cursor support | Users needing custom provider endpoints (LiteLLM, llama.cpp, vLLM) | Adapter-based; pnpm-managed; structured setup auth |
| **ZeroClaw** | **RFC-driven architecture** (session ownership, WASM plugins, granular sandbox); Rust runtime | Security-conscious developers; self-hosting communities | Rust; RFC process; WASM composability (v0.9+) |
| **LobsterAI** | Windows installer polish; library/resource management; cost accounting | Clipboard-centric power users; Windows-first environments | Desktop app; installer lifecycle; renderer UI |
| **Moltis** | Python-ecosystem orchestration; OpenAI/Codex strict-mode compatibility | Python developers; lightweight deployments | Minimal core; security-first operators |

---

## 6. Community Momentum & Maturity

### Tier 1: Rapid Iteration (High Release Cadence, Large Community)

- **OpenClaw** (500+500 daily updates, but quality-at-risk)
- **Hermes Agent** (50+50 daily, release yesterday; 525 PRs rolled up)

### Tier 2: Strong Momentum (Active, Focused)

- **CoPaw (QwenPaw)** — 31 issues + 50 PRs; 25 PRs merged today; 2.2.0 in final stages
- **IronClaw** — 33 issues + 48 PRs; 31 merged; memory epic well-scoped
- **NanoClaw** — 11 issues + 50 PRs; deep provider refactor; channel bugs acknowledged (but old PRs unmerged, risk of conflict)
- **ZeroClaw** — 29 issues + 50 PRs; RFC-heavy; v0.8.5 freeze approaching; contributor responsiveness bottleneck

### Tier 3: Steady Maintenance

- **NanoBot** — 2 issues + 24 PRs; 9 merged; architectural refactors landing
- **LobsterAI** — 7 issues + 13 PRs; installer polish; data-loss bug needs action
- **PicoClaw** — 3 issues + 7 PRs; mostly dependency bumps; slow review cycle
- **Moltis** — Quiet, 2 PRs merged; stable

### Tier 4: Dormant

- **NullClaw**, **TinyClaw**, **ZeptoClaw** — No activity in 24h.

---

## 7. Trend Signals

1. **Memory is the new battleground.** IronClaw, NanoBot, and ZeroClaw are all rearchitecting memory systems (explicit recall, pluggable backends, lifecycle/storage decoupling). By late 2026, agents without durable cross-conversation memory will be seen as incomplete.

2. **Silent failures are unacceptable.** Multiple projects report bugs where agents "look dead" (NanoClaw #3568, #3575), Slack/Telegram messages drop without logs (OpenClaw #131150), or context overflow is masked (ZeroClaw #10329). The ecosystem is converging on **observability-first** and **explicit error-surfacing** as table stakes.

3. **Cost control is no longer optional.** From per-agent budgets (OpenClaw #425) to 4x token-cost inflation from thread replay (IronClaw #7824) to credit-drain confusion (LobsterAI #2562), operators are demanding **cost predictability and visibility** as a first-class feature.

4. **Provider abstraction is undergoing its "striking distance" moment.** NanoClaw's 8-PR provider-contract refactor, OpenClaw's multi-runtime support, and Moltis's OpenAI-strict-mode fixes signal that projects are preparing for a **multi-provider, multi-model default** (Gemini, Cursor, local endpoints) rather than a single-LLM assumption.

5. **Security is moving up the stack.** Path traversal (NanoBot #5564), approval-flow corruption (NanoClaw #3456), file-guard bypasses (CoPaw #7362), and insecure temp-file permissions (ZeroClaw #10409) indicate that **agent security is no longer about the LLM** but about the platform's interaction boundaries — a necessary maturation for enterprise adoption.

6. **Channel diversity is a competitive moat.** CoPaw's Chinese market channels (DingTalk, WeCom, QQ), OpenClaw's four-platform breadth, and IronClaw's Slack/Gmail focus show that projects succeed by **deepening their chosen channel ecosystems** while maintaining a stable core.

7. **Architectural consolidation precedes feature expansion.** ZeroClaw's RFC queue (session ownership, WASM plugins, granular sandbox), NanoClaw's provider refactor, NanoBot's tool-execution boundary, and IronClaw's Reborn migration all point to **design-first development** as projects scale past their v1 prototypes. The next wave of feature releases (Gemini support, memory hubs, team editions) depends on these foundations landing successfully.

---

**Bottom line for decision-makers:** OpenClaw remains the ecosystem's strongest community play but faces quality-pressure at scale. For teams prioritizing stability and architecture, IronClaw and NanoBot offer excellent foundations. CoPaw/QwenPaw is the strongest non-English-market option. ZeroClaw is worth tracking for post-v0.9 composability. The ecosystem is healthy, but the delta between "chat wrapper" and "production infrastructure" is closing rapidly — and projects that fail to address memory, cost control, and silent failures will be left behind.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-28

## 1. Today's Overview
NanoBot saw moderate activity over the past 24 hours, with 2 open issues and 24 pull requests updated. Notably, 9 PRs were merged/closed, signaling strong forward momentum in the agent and memory subsystems. The bulk of merged work centers on architectural refactoring of the `AgentRunner`, memory archival, and provider fallback handling. The project appears healthy, with a clear thematic focus on improving context management, tool execution boundaries, and multi-turn memory behavior.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
Nine pull requests were merged/closed today, marking significant architectural progress:

- **[#5575 — refactor(memory): remove consolidation ratio](https://github.com/HKUDS/nanobot/pull/5575)** (merged): Removes the `consolidationRatio` configuration and ratio-driven archive loop, replacing it with a deterministic archival strategy that retains the latest eight messages. This simplifies memory behavior and makes it more predictable.
- **[#5572 — fix(agent): default request concurrency to unlimited](https://github.com/HKUDS/nanobot/pull/5572)** (merged, p1): Changes the default inbound request concurrency to unlimited when `NANOBOT_MAX_CONCURRENT_REQUESTS` is unset. Addresses WebUI stalls caused by overly conservative concurrency defaults.
- **[#5574 — refactor(providers): make fallback attempts explicit](https://github.com/HKUDS/nanobot/pull/5574)** (merged): Introduces an immutable `ProviderAttempt` and an explicit async route for resolving provider/model/transport/retry policy before execution, making fallback behavior explicit and testable.
- **[#5569 — refactor(agent): extract tool execution boundary](https://github.com/HKUDS/nanobot/pull/5569)** (merged): Moves tool-call preparation, execution, and error handling out of `AgentRunner` into a functional `nanobot.agent.tools.execution` boundary.
- **[#5565 — refactor(memory): decouple archival from provider state](https://github.com/HKUDS/nanobot/pull/5565)** (merged): Extracts `MemoryArchiver` to write the Memory ingestion journal without owning `SessionManager`, preserving provider continuation state across archival triggers.
- **[#4346 — fix(providers): mark stripped images as unviewable](https://github.com/HKUDS/nanobot/pull/4346)** (closed): Resolves a path-leak issue where stripped images could expose local file paths. Likely superseded or conflict-resolved after a long open period.

## 4. Community Hot Topics
While no PRs have high comment counts, the most discussed items reflect two deep user needs:

- **[#5567 — Feat: 飞书渠道应整合多轮回复为单条流式卡片消息](https://github.com/HKUDS/nanobot/issues/5567)** (2 comments): A Feishu (Lark) channel feature request. Users want a "one user message → one agent reply" mapping, consolidating streaming deltas, tool progress messages, and final responses into a single streaming card. **Underlying need**: cleaner channel UX and reduced message noise for enterprise chat platforms, likely relevant to other channels (Slack, Teams) as well.

- **[#5564 — fix(session): prevent path traversal in session file handling](https://github.com/HKUDS/nanobot/issues/5564)** (0 comments): Security issue opened by a bot (arena-ai-coding-agent) flagging that session IDs are used unsafely in file path construction. **Underlying need**: hardening against malicious input in a multi-tenant deployment context.

## 5. Bugs & Stability
Two bugs were reported in the last 24 hours:

| Severity | Issue | Status |
|----------|-------|--------|
| **High (Security)** | [#5564 — Path traversal in session file handling](https://github.com/HKUDS/nanobot/issues/5564) | No associated fix PR yet; likely requires validation of `session_id` before path construction in `nanobot/session/manager.py` |
| **Medium (UX)** | [#5567 — Feishu channel sends multiple messages per turn](https://github.com/HKUDS/nanobot/issues/5567) | Open feature/fix request; no linked PR |

Additionally, several previously reported bugs have fix PRs still open in the backlog (see Backlog Watch below), including Windows transient `PermissionError` crashes and delayed-message session recreation.

## 6. Feature Requests & Roadmap Signals
Several feature-significant PRs are open, suggesting likely roadmap items for upcoming versions:

- **[#5571 — feat(memory): require explicit recall by default](https://github.com/HKUDS/nanobot/pull/5571)** (p1): Switches memory from always-injected to explicit recall via a `recall_memory` tool, reducing prompt overhead. This is a notable architectural shift for context efficiency.
- **[#5570 — feat(memory): add pluggable recall backend](https://github.com/HKUDS/nanobot/pull/5570)** (p2): Defines a `MemoryBackend` interface, enabling future vector-store or external memory integrations. Next version may ship this as the foundation for memory extensibility.
- **[#5561 — feat(spawn): per-spawn model presets behind a spawnPresets allowlist](https://github.com/HKUDS/nanobot/pull/5561)** (p2): Resolves #4231; allows per-agent model selection, an alternative implementation of #4291.
- **[#5537 — feat(my): persist session focus across turns](https://github.com/HKUDS/nanobot/pull/5537)** (p2): Adds a durable session-scoped `focus` value, giving agents a short continuity cue across turns and restarts.
- **[#5573 — fix(mcp): refresh expired OAuth tokens automatically](https://github.com/HKUDS/nanobot/pull/5573)** (p2): Persists OAuth expiry/issuer metadata and refreshes automatically across gateway restarts.

## 7. User Feedback Summary
User feedback in the current window is sparse but informative:

- **Feishu channel UX dissatisfaction** (#5567): The reporter explicitly states that receiving *n* messages (tool hints, progress, final reply) for a single user message "is a poor experience" and requests a consolidated single-card streaming response. This is a clear quality-of-life pain point for production channel users.
- **Security-conscious automation** (#5564): The issue was auto-filed by a coding agent, reflecting the community's increasing use of AI-driven security auditing in CI workflows — a sign of a mature, security-aware contributor base.

## 8. Backlog Watch
Several PRs have been open for extended periods and require maintainer attention:

**Security/Stability:**
- [#5382 — fix(session): retry os.replace() on transient Windows PermissionError](https://github.com/HKUDS/nanobot/pull/5382) — Open since **2026-08-13** (15 days); confirmed crash in `gateway.log`; flagged with `conflict`.
- [#5483 — fix(session): prevent deleted sessions from being recreated by delayed messages](https://github.com/HKUDS/nanobot/pull/5483) — Open since **2026-08-22**; addresses a data-integrity edge case.

**MCP/Auth Credentials:**
- [#5338 — fix(mcp): preserve credentials when OAuth store read fails](https://github.com/HKUDS/nanobot/pull/5338) — Open since **2026-08-11** (17 days); critical for multi-server OAuth credential safety.
- [#5339 — fix(webui): reject discarded temporary chat messages](https://github.com/HKUDS/nanobot/pull/5339) — Open since **2026-08-11**; race condition in WebSocket chat persistence.

**Memory:**
- [#5379 — fix(memory): preserve full consolidation input](https://github.com/HKUDS/nanobot/pull/5379) — Open since **2026-08-13**; data-loss risk during consolidation; flagged `conflict`.

**Code Quality:**
- [#5396 — refactor: narrow file-level Pyright suppressions](https://github.com/HKUDS/nanobot/pull/5396) — Open since **2026-08-14**; low risk but may conflict with active refactoring in `nanobot/agent/tools/`.

---

**Project Health Summary**: NanoBot is in a strong refactoring phase, with maintainers actively merging architectural improvements in memory, tooling, and provider handling. The focus on explicit memory recall and pluggable backends signals a maturing agent runtime. The main concerns are the long-stalled Windows crash fix (#5382) and OAuth credential safety (#5338), both of which have been open for over two weeks and could benefit from prioritization.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-28

## 1. Today's Overview

Hermes Agent remains highly active with 50 issues and 50 PRs updated in the last 24 hours, indicating sustained development velocity. The project shipped patch release v0.20.6 (v2026.8.27) yesterday, rolling up ~525 merged PRs since the previous tag. Activity is dominated by bug fixes around session state management, context compression, and gateway/multiplex profile isolation, alongside several new feature contributions. Notable new submissions include a file-handoff capability for autonomous group chats, iOS WebKit dashboard tap fixes, and multiple compression-path hardening PRs. The open issue count is healthy at 49, with only 1 closed in the period, suggesting maintainers are prioritizing review throughput over issue triage.

---

## 2. Releases

### Hermes Agent v0.20.6 (v2026.8.27)

- **Release Date:** August 27, 2026
- **Type:** Patch release rolling up ~525 PRs since v0.20.5
- **Target consumers:** Docker images, hosted deployments, fresh installs

**Key notes:**
- This is a stability/tagging release — no breaking changes flagged in the release notes.
- Downstream consumers are advised to pull the updated tag for the cumulative fixes.
- Given the volume of merged PRs (~525), this release likely includes the session-state risk mitigations and compression fixes that have been recurring themes in the tracker.

---

## 3. Project Progress

**Merged/Closed PRs today (6 total):**

- **#96951** (closed) — Auto-fix formatting PR (bot-driven, routine).
- **#96634** (closed) — `fix(compression): retry a stalled summary on the fallback chain (#78981)` — addresses the long-standing stalled-compression gap (P1).
- **#96945** (closed, duplicate) — `perf(compression): add guarded fast summary lane` — superseded by #93634.
- **#93634** (closed) — `perf(compression): add guarded fast summary lane` — accepted version of the fast-lane compression route with bounded token/timeout controls and desktop compaction state reconciliation.

**Active PRs of note (open, high-signal):**

- **#93888** (bug, P1) — Fix for Desktop sending local runtime ID to Remote Gateway, breaking session restores. (Open, 14 comments.)
- **#65522** — Gateway media message queueing while sessions are busy (open since July, high-traffic area).
- **#83870** — Multiplex context files scoped by profile (fixes cross-profile `AGENTS.md` leakage).
- **#92526** — Cron delivery retains profile secret scope (multiplex credential-isolation gap).

---

## 4. Community Hot Topics

**1. Skills index watchdog (#66616)** — 110 comments, open since July 18, marked `degraded`.
- The Skills Hub index is consistently stale (29.8h old against a 26h limit).
- Root cause is in CI workflow scheduling/timing. This issue has massive community engagement likely because it affects docs discoverability and skill reliability for many users.
- **Link:** [Issue #66616](https://github.com/NousResearch/hermes-agent/issues/66616)

**2. Desktop ↔ Remote Gateway session restore failure (#93888)** — 14 comments, P1.
- Desktop sends an 8-char local runtime ID to a remote gateway, which cannot resolve it → “Restore failed — Session not found.”
- High severity: blocks all stored sessions on remote setups.
- **Link:** [Issue #93888](https://github.com/NousResearch/hermes-agent/issues/93888)

**3. Headroom-ai tool-output compression (#39691)** — 12 comments, 17 👍.
- Feature request to add tool-level output compression (not just conversation-level). Strong community desire for reducing token bloat from large tool outputs.
- **Link:** [Issue #39691](https://github.com/NousResearch/hermes-agent/issues/39691)

**4. RealtimeVoiceProvider ABC (#77111)** — 9 comments, 2 👍.
- RFC triggered by 4 competing duplex-voice PRs. Community calling for an interface design instead of sequential merges. Aligns with project’s own `AGENTS.md` guidance.
- **Link:** [Issue #77111](https://github.com/NousResearch/hermes-agent/issues/77111)

**5. Desktop macOS backend timeout (#60323)** — 11 comments, 1 👍.
- Desktop misses `HERMES_BACKEND_READY` even when logged, causing a 90-second boot timeout. Likely race-condition in the Electron bootstrap.
- **Link:** [Issue #60323](https://github.com/NousResearch/hermes-agent/issues/60323)

---

## 5. Bugs & Stability

| Severity | Issue | Description | Fix PR? |
|---|---|---|---|
| **P1** | [#93888](https://github.com/NousResearch/hermes-agent/issues/93888) | Desktop sends local runtime ID to Remote Gateway → session restore permanently fails | Not yet |
| **P1** | [#84718](https://github.com/NousResearch/hermes-agent/issues/84718) | Compaction drops skill policy and justifications but preserves todos — agent executes stale imperative | Not yet |
| **P1** | [#96775](https://github.com/NousResearch/hermes-agent/issues/96775) | Preflight compression stall re-enters same strategy after interrupt (no durable backoff) | In progress (PR #96949) |
| **P1** | [#60323](https://github.com/NousResearch/hermes-agent/issues/60323) | Desktop macOS backend timeout on `HERMES_BACKEND_READY` race | Not yet |
| **P2** | [#75130](https://github.com/NousResearch/hermes-agent/issues/75130) | Skill-proposal queue grows unbounded (357 in 8 days, 21% dead) | Not yet |
| **P2** | [#96877](https://github.com/NousResearch/hermes-agent/issues/96877) | MCP client sends unsupported `sampling.tools` capability breaking Zoho handshake | Not yet |
| **P2** | [#74798](https://github.com/NousResearch/hermes-agent/issues/74798) | Truncated tool args dropped when `finish_reason` set (no chunk recovery) | Not yet |
| **P2** | [#96800](https://github.com/NousResearch/hermes-agent/issues/96800) | Desktop UI sluggish on AMD RDNA4 + Wayland; Electron GPU flags not passable | Not yet |
| **P2** | [#83992](https://github.com/NousResearch/hermes-agent/issues/83992) | `DaemonThreadPoolExecutor` uses removed `_initializer`/`_initargs` on Python 3.14 | PR #90201 (dup) |
| **P2** | [#96924](https://github.com/NousResearch/hermes-agent/issues/96924) | Vision auxiliary runtime stays on stale provider after fallback restore | Not yet |

**New bug disclosures today** (lower-severity but note-worthy):
- [#96729](https://github.com/NousResearch/hermes-agent/issues/96729) — Real-profile browser launch leaves auth DBs `0644` and injects mock-keychain flags (security-adjacent).
- [#96918](https://github.com/NousResearch/hermes-agent/issues/96918) — Web dashboard session cards not tappable on iOS WebKit; fix PR #96952 submitted same day.
- [#96902](https://github.com/NousResearch/hermes-agent/issues/96902) — Copilot `grok-4.6` returns HTTP 400 (provider capability mismatch).

---

## 6. Feature Requests & Roadmap Signals

**High-traffic / high-likelihood features:**

1. **Tool-output compression (headroom-ai)** — [#39691](https://github.com/NousResearch/hermes-agent/issues/39691) — 17 👍. Strong signal; likely to land in a minor release if design converges with the existing compression refactors.
2. **Duplex-voice provider interface** — [#77111](https://github.com/NousResearch/hermes-agent/issues/77111) — actively debated; project’s own `AGENTS.md` pushes toward ABC design. Expect a merged abstraction soon.
3. **File handoff in autonomous group chats** — PR [#96919](https://github.com/NousResearch/hermes-agent/pull/96919) — new today, directly addresses a visible Bot-mode gap; likely to move quickly.
4. **WhatsApp `observe_unmentioned_group_messages`** — [#38710](https://github.com/NousResearch/hermes-agent/issues/38710) — 4 👍. Matches Telegram parity; moderate complexity, likely accepted.
5. **Polish language support** — [#96937](https://github.com/NousResearch/hermes-agent/issues/96937) — ready-made `pl.ts` (~3450 lines). Low effort, high goodwill; likely merged if maintainers confirm.
6. **China mirror/update channels** — [#96858](https://github.com/NousResearch/hermes-agent/issues/96858) and [#46839](https://github.com/NousResearch/hermes-agent/issues/46839) — repeated demand; longer-term infrastructure decision, may require org-level commitment.
7. **Project-scoped MEMORY.md** — [#33638](https://github.com/NousResearch/hermes-agent/issues/33638) — open since May; conceptually aligned with profile-scoping work (PR #83870), may get pulled in as part of that effort.

---

## 7. User Feedback Summary

**Recurring pain points:**

- **Session-state fragility** — Users on Desktop + Remote Gateway are hitting permanent restore failures (P1, #93888) and stale/deleted session IDs still cached in renderer (#79001). Trust in persistence is strained.
- **Compression policy destruction** — Multiple reports (#84718, #96775, #78981 family) that compression preserves the “what” but loses the “why” (policy, skill context). Users report agents blindly executing stale todos.
- **Cross-profile contamination** — Multiplex mode leaks context files or secrets across profiles (#83870, #92526); users running multi-tenant setups are exposed.
- **GPU/platform issues on Desktop** — AMD RDNA4/Wayland sluggishness (#96800), macOS boot timeouts (#60323); Electron wrapper needs better config passthrough.
- **Provider compatibility** — Zoho MCP handshake failure (#96877) and Copilot `grok-4.6` 400s (#96902) show integration surface still brittle.
- **Chinese users blocked by network** — Two active threads (#46839, #96858) asking for mirrors and fewer proxy assumptions during install.

**Positive signals:**
- The community is actively submitting complete, tested PRs (Polish locale, iOS tap fix, Feishu DM fix) — indicating good contribution ergonomics.
- The compression fast-lane PRs (#93634 merged) show maintainers are listening to performance complaints and shipping targeted improvements.

---

## 8. Backlog Watch

**Issues needing maintainer attention:**

- **#66616** (110 comments) — Skills index stale for weeks; high community engagement, no resolution. Could be turned into a fast-follow fix by adjusting cron timing.
- **#39691** (17 👍) — Headroom-ai tool compression; large community support, but no maintainer response. Likely a roadmap item but silence risks user frustration.
- **#77111** (9 comments) — Voice provider ABC; community is waiting for a design decision. This is an explicit `AGENTS.md`-triggered case; maintainers should acknowledge intent.
- **#60323** (11 comments) — macOS desktop boot timeout; P1 but no linked PR. Given how many users run macOS desktops, this deserves a fix or at least a workaround note.
- **#75130** — Skill-proposal queue unbounded growth; P2 but has config-corruption implications. Needs a triage decision on auto-approval limits.

**PRs waiting on review:**

- **#65522** — Gateway media queueing (open since July 16). Critical for media-heavy sessions; stale but non-trivial.
- **#90201** — Python 3.14 daemon pool fix (marked duplicate of #83992; both open). Should consolidate and merge.
- **#95278** — Telemetry exporter (opt-in). Feature-complete but low priority; needs a maintainer decision on privacy posture.

---

*Data source: GitHub (NousResearch/hermes-agent), captured 2026-08-28.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-28

## Today's Overview
PicoClaw showed steady activity over the last 24 hours with 10 total updates across issues and pull requests. Three issues saw updates (1 open, 2 closed via stale bot) and seven PRs were touched, with one new open PR (#3347) addressing web UI lag and six dependency bumps closed/merged. No new releases were published, but the project is actively maintaining its Go dependencies across AWS Bedrock, Anthropic, and Matrix (mautrix) SDKs. The single open feature request (#3287) on IRC long-message handling continues to gather community discussion, signaling sustained interest in IRCv3 improvements.

## Releases
No new releases were published during this period. The last release remains unavailable in this data window.

## Project Progress
Six PRs were closed/merged in the last 24 hours, though most were automated dependency bumps:
- **#3332** – Bump `aws-sdk-go-v2` from 1.42.0 to 1.43.4 *(dependencies)*
- **#3333** – Bump `maunium.net/go/mautrix` from 0.27.0 to 0.29.0 *(dependencies)*
- **#3334** – Bump `anthropics/anthropic-sdk-go` from 1.55.1 to 1.62.0 *(dependencies)*
- **#3335** – Bump `aws-sdk-go-v2/config` from 1.32.25 to 1.32.35 *(dependencies)*
- **#3336** – Bump `aws-sdk-go-v2/service/bedrockruntime` from 1.53.3 to 1.57.1 *(dependencies)*
- **#1555** – Merge of multiple open fixes from earlier PRs (#1390, #1389, #1383, #1381)

Notably, **#1555** consolidates previously submitted fixes from March, which may include long-pending bug fixes—worth reviewing what's actually inside. One new open PR **#3347** proposes a fix for laggy web interface with large chat text, and has been tested by the author on desktop and mobile (Brave).

## Community Hot Topics
The most active discussion this period is **Issue #3287** (`[OPEN] Better support long messages in IRC`), with 8 comments and counting. The author wants PicoClaw to treat IRCv3 messages split by the 512-byte limit as a single cohesive message rather than separate ones, as newlines currently break message boundaries. This is a legitimate protocol-level refinement that affects core IRC integration usability.

Other issues were closed as stale by the bot, with only 2 comments each—indicating low community engagement on those threads.

## Bugs & Stability
- **[Medium] Web UI lag with large chat text** — Addressed by open PR **#3347**. The author reports significant lag in the chat area when there's a lot of text; their fix ("analyzed and fixed by...") resolves it on both desktop and mobile browsers. Fix available but not yet merged.
- No crash-level or regression-level bugs were reported in this window. The stale-closed issues (#3330, #3331) were feature requests, not bugs.

## Feature Requests & Roadmap Signals
Three features are currently in discussion:
1. **IRCv3 long message handling** (#3287, open, 8 comments) — Treat split messages as one; high community interest, likely to be prioritized given the active discussion.
2. **Flexible `/audio/transcriptions` model support** (#3331, closed stale) — Wants to use any compatible model instead of only `*-whisper-*` models which are "too old and slow." Request was closed by stale bot, but may resurface as a real need.
3. **Dynamic model override in delegate/spawn/subagent tools** (#3330, closed stale) — Wants per-call model selection instead of static config. Also closed stale despite being a well-stated architectural improvement.

The latter two were closed due to inactivity, but both represent practical user needs. The largest signal is the IRC message-length issue, which addresses a core UX flaw for IRC users of PicoClaw.

## User Feedback Summary
- **Positive:** The author of PR #3347 successfully fixed the laggy web UI and validated it across devices—evidence that the UI team is responsive to performance issues.
- **Frustration:** The `/audio/transcriptions` limitation to only `*-whisper-*` models is seen as restrictive and outdated, with the user explicitly noting the models are "too old and slow."
- **Gap:** Users want more control over model selection at runtime (delegate/spawn tools), suggesting the current static model assignment is insufficient for complex workflows.
- **IRC users:** There's dissatisfaction with how PicoClaw handles long IRC messages that get split by the protocol's 512-byte limit—message fragmentation breaks conversational continuity.

## Backlog Watch
- **Issue #3287** (open, 8 comments, created 2026-07-22) — Over a month old, still awaiting maintainer response or implementation. This is the most active thread and holds clear product value for IRC users.
- **PR #3347** (open, 0 comments) — New fix for UI lag, tested and ready. Needs maintainer review within the next few days to avoid it going stale like previous PRs.
- **Issue #3330 and #3331** — Both closed as stale, but their underlying requests (dynamic model selection, flexible STT models) are legitimate and could be revisited as roadmap candidates. They may resurface if the community re-ups them.
- **PR #1555** (closed/merged) — Long-pending merge of four earlier PRs. The 5-month gap between creation (March) and close (August) suggests maintainers may be slow to review user-contributed fixes; monitor for regressions from this batch merge.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-28

---

## 1. Today's Overview

NanoClaw is in a period of intense feature development and structural refactoring. The project shows **very high activity**: 11 issues and 50 pull requests were updated in the last 24 hours, though only one issue was closed and four PRs were merged. The majority of open PRs are **large-scale provider-contract refactors** (opencode, codex, runtime, host, setup) submitted by core team members, indicating a significant architectural consolidation effort. Concurrently, a cluster of **channel-adapter bugs** (Discord, Telegram, WhatsApp) is putting pressure on reliability for real-world installs. No new releases or release candidates were cut this period.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Project Progress

**Merged/Closed (4 PRs)** — details not provided in the dataset, but the open PR list suggests areas of focus.

**Active architectural work (core-team, open):**

- **[#3594](https://github.com/nanocoai/nanoclaw/pull/3594) — fix(tasks): account errored task turns as FAILED runs instead of dropping them** — Resolves [#3223](https://github.com/nanocoai/nanoclaw/issues/3223); scheduled-task errors previously invisible.
- **[#3581–#3592 series](https://github.com/nanocoai/nanoclaw/pull/3581)** — Eight PRs by **zvi-fried** refactoring provider contracts: opencode ([#3588](https://github.com/nanocoai/nanoclaw/pull/3588)), codex ([#3584](https://github.com/nanocoai/nanoclaw/pull/3584)), runtime ([#3581](https://github.com/nanocoai/nanoclaw/pull/3581)), host ([#3585](https://github.com/nanocoai/nanoclaw/pull/3585)), setup ([#3586](https://github.com/nanocoai/nanoclaw/pull/3586)), plus tone/speed inference properties ([#3592](https://github.com/nanocoai/nanoclaw/pull/3592), [#3593](https://github.com/nanocoai/nanoclaw/pull/3593)).
- **[#3489](https://github.com/nanocoai/nanoclaw/pull/3489) — structured setup-driver authentication for Codex** — removes the human-at-terminal requirement for `codex login`.
- **[#3471](https://github.com/nanocoai/nanoclaw/pull/3471) — fix(pnpm): turn the minimumReleaseAge gate on (providers twin)** — fixes a config-key bug on the `providers` branch.
- **[#3463](https://github.com/nanocoai/nanoclaw/pull/3463) — opencode: fall back to `message.part.delta` text** — addresses a timing race where final snapshots missed (~78ms window).
- **[#2136](https://github.com/nanocoai/nanoclaw/pull/2136) — Google Gemini provider support** — long-running feature PR still open.

---

## 4. Community Hot Topics

**Most active issue: [#3456 — Discord approval card corruption](https://github.com/nanocoai/nanoclaw/issues/3456)** (5 comments, created 2026-08-23, updated 2026-08-27)
A redundant `value` param on Discord buttons corrupts `custom_id`, making every approval click resolve to the wrong option. **Severity: high** — breaks core ask_question/approval flows entirely on Discord.

**Other active threads (2 comments each):**
- [#2888 — Discord drops image/file attachments](https://github.com/nanocoai/nanoclaw/issues/2888) — agent only sees filename metadata, never content. Open for ~2 months, still unresolved.
- [#3572 — inbound attachments silently dropped (CLOSED)](https://github.com/nanocoai/nanoclaw/issues/3572) — closed, but appears to be a duplicate of #2888 rather than a fix; root cause described as adapter-vs-consumer contract mismatch (`url` vs `fetchData`).

**Underlying need:** The community is pushing hard on **production reliability across chat adapters**. Discord attachment handling, Telegram Markdown escaping, and WhatsApp image downscaling are the three most-repeated pain points. The provider refactor wave is internal; the *visible* pain is all channel-adapter related.

---

## 5. Bugs & Stability

Ranked by severity:

| # | Issue | Channel | Severity | Status |
|---|-------|---------|----------|--------|
| 1 | [#3456 — Discord approval button corruption](https://github.com/nanocoai/nanoclaw/issues/3456) | Discord | 🔴 Critical — approval flow unusable | Open, 5 comments |
| 2 | [#3568 — Pending system rows starve inbound queue](https://github.com/nanocoai/nanoclaw/issues/3568) | Core | 🔴 Agent silently stops responding | Open |
| 3 | [#2888 — Discord image/file attachments dropped](https://github.com/nanocoai/nanoclaw/issues/2888) | Discord | 🟠 High — open 2 months | Open |
| 4 | [#3575 — WhatsApp large images wedge session](https://github.com/nanocoai/nanoclaw/issues/3575) | WhatsApp | 🟠 High — agent dead until `/clear` | Open (fix PR likely needed) |
| 5 | [#3569 — Telegram odd-underscore URLs never deliver](https://github.com/nanocoai/nanoclaw/issues/3569) | Telegram | 🟠 High — pinned 3 versions behind upstream fix | Open |
| 6 | [#3576 — Rate-limit error flood, no backoff](https://github.com/nanocoai/nanoclaw/issues/3576) | Core | 🟡 Medium — UX spam | Open |

**Notable:** Several issues describe problems as *"agent looks dead"* or *"silently stops"* — the common theme is **silent failure modes** with no error surfaced to the user or operator. This is a systemic stability concern.

One directly-matching fix exists: [#3594](https://github.com/nanocoai/nanoclaw/pull/3594) fixes errored scheduled tasks being indistinguishable from successful no-op runs.

---

## 6. Feature Requests & Roadmap Signals

**From issues (likely near-term):**
- **#3577 — auto-wire sole eligible agent-group** — remove the manual "Choose an agent" picker when only one group exists. Small, high-impact UX improvement; likely in next minor release.
- **#3579 — prevent `nc:copy` lists from drifting** — registry skill recipe drift detection; a governance/maintenance feature, likely mid-term.

**From PRs (strong signals):**
- **Google Gemini provider** ([#2136](https://github.com/nanocoai/nanoclaw/pull/2136)) — flagship new-provider feature, open since April; may land once the provider-contract refactor settles.
- **Per-group model override** ([#2872](https://github.com/nanocoai/nanoclaw/pull/2872) opencode, [#1994](https://github.com/nanocoai/nanoclaw/pull/1994) codex) — a clear direction: **multi-model, per-group configuration** on a single install.
- **Custom OpenAI-compatible endpoints** ([#1995](https://github.com/nanocoai/nanoclaw/pull/1995), [#1994](https://github.com/nanocoai/nanoclaw/pull/1994)) — LiteLLM/llama.cpp/vLLM targeting; supports on-prem/local use cases.
- **Cursor Agent SDK payload** ([#3356](https://github.com/nanocoai/nanoclaw/pull/3356)) — another headline provider integration.

**Prediction:** The **provider-contract refactor** (8 PRs from zvi-fried + others) is the top roadmap item. Once merged, Gemini, Cursor, and per-group model routing become far easier to land. Watch for a **major provider-architecture release** within 2–4 weeks.

---

## 7. User Feedback Summary

**Pain points (ranked by frequency in issues):**

1. **Silent failures** — attachments dropped with no log, agent stops responding with no error, rate-limited turns flood errors with no dedup. Users report *"no error or warning is emitted anywhere"* (#3572) and *"the agent looks dead"* (#3575).
2. **Discord as a second-class citizen** — two critical Discord bugs (#3456, #2888) remain open; Web/Telegram are repeatedly cited as working correctly in contrast.
3. **Dependency pinning lag** — Telegram adapter pinned to 4.29.0 while upstream fixed the odd-underscore bug in 4.32.0; users are forced onto broken versions.
4. **Update process friction** — community-authored local adapters get overwritten by the update skill's auto-refresh with no opt-out (#3529); per-agent tool scoping doesn't apply to groups created later (#3532).

**Satisfaction indicators:** Long-lived PRs (since April) are still being actively updated, not abandoned. Core team is shipping consistently, and the community is writing detailed root-cause analyses — signs of an engaged, technically sophisticated user base.

---

## 8. Backlog Watch

**Long-standing issues needing maintainer attention:**

| # | Issue | Open since | Notes |
|---|-------|-----------|-------|
| [#2888](https://github.com/nanocoai/nanoclaw/issues/2888) | Discord attachments dropped | 2026-06-30 (~2 months) | High severity, duplicates closed #3572; needs a fix PR |
| [#3532](https://github.com/nanocoai/nanoclaw/issues/3532) | add-\*-tool scoping misses newer agents | 2026-08-25 | Design gap in skill scoping model |
| [#3529](https://github.com/nanocoai/nanoclaw/issues/3529) | update-nanoclaw overwrites local adapters | 2026-08-25 | No opt-out; destructive |

**Long-aged PRs still open (since April–June):**

| # | PR | Open since | Risk |
|---|-----|-----------|------|
| [#1995](https://github.com/nanocoai/nanoclaw/pull/1995) | opencode custom provider npm/no-auth + /add-local-llama | 2026-04-24 | May conflict with provider-contract refactor |
| [#1994](https://github.com/nanocoai/nanoclaw/pull/1994) | codex per-group custom endpoints | 2026-04-24 | Same |
| [#2878](https://github.com/nanocoai/nanoclaw/pull/2878) | codex stale-secret reconnect fix | 2026-06-28 | Auth reliability |
| [#2865](https://github.com/nanocoai/nanoclaw/pull/2865) | opencode stale-session rotation | 2026-06-26 | Steady-state reliability |
| [#2848](https://github.com/nanocoai/nanoclaw/pull/2848) | opencode cwd/.env fallback | 2026-06-24 | Config correctness |

**Watch item:** The 8-PR provider-refactor series (#3581–#3592) touches the same files as April–June opencode/codex PRs. Merge conflicts are likely; maintainers should prioritize sequencing or risk losing community contributions from TeeJS, grantland, and wakqasahmed.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-28

## 1. Today's Overview

IronClaw is in a high-velocity development phase, with 48 PRs and 33 issues updated in the past 24 hours, indicating strong momentum. The project is currently executing a major architectural push around persistent memory systems, with a coordinated series of issues and PRs (#7947–#7953) building out a shared learning router, memory admission policies, and multi-provider adapters. A parallel effort focuses on fixing critical performance issues in capability payload handling, with Issue #7891 highlighting a 14.3-second inference regression caused by unbounded MIME headers being injected into prompts. The project shows healthy closure rates (8 closed issues, 31 merged/closed PRs today) alongside an active roadmap with several high-risk decision spikes under discussion. CI reliability remains a concern, with nightly pipeline failures and ongoing infrastructure refactoring.

## 2. Releases

No new releases were published in this 24-hour window. The project continues to operate on the existing IronClaw 1.3.0 deployment (commit `70795c16ed0cec21eb8cba16d2dcf851d25dc83d`) per environment references in Issue #7856.

## 3. Project Progress

Today saw 31 merged/closed PRs and 8 closed issues, with several significant features landing:

- **Gmail semantic output** ([PR #7944](https://github.com/nearai/ironclaw/pull/7944)): Normalizes Gmail responses at the producer boundary, decoding base64url body data, preferring plain text, converting HTML to Markdown, and exposing semantic headers. This addresses the performance regression from Issue #7891 by ensuring only structured, curated content reaches the model.
- **Context compaction barrier** ([PR #7954](https://github.com/nearai/ironclaw/pull/7954)): Persists compaction outputs as cumulative context barriers, folding the newest durable barrier into subsequent summarization requests. This is a foundational piece for the ThreadService migration.
- **Slack broadcast mention fix** ([PR #7941](https://github.com/nearai/ironclaw/pull/7941)): Fixes a routing bug where "Also send to channel" replies with `subtype: "thread_broadcast"` were classified as `Ignore` events, breaking broadcast mentions.
- **Memory conflict detection** ([PR #7907](https://github.com/nearai/ironclaw/pull/7907)): Adds SHA-256 content hashing to `ironclaw.memory.read`/`write`, preventing silent data loss from stale full-document rewrites.
- **CI integration batching** ([PR #7943](https://github.com/nearai/ironclaw/pull/7943)): Compiles integration batches once across selected lanes, significantly reducing CI time.
- **GitHub content decoding** ([PR #7963](https://github.com/nearai/ironclaw/pull/7963)): Decodes GitHub Contents API base64 data at the producer boundary before model exposure.
- **Codebase knowledge graph refresh** ([PR #7966](https://github.com/nearai/ironclaw/pull/7966)): Automated nightly refresh of the committed codebase-memory bootstrap snapshot.

The closed Issue #3278 (MissionService integration with TurnCoordinator) is part of the ongoing Reborn architecture migration.

## 4. Community Hot Topics

1. **[Issue #7891 — Performance regression from unprojected capability payloads](https://github.com/nearai/ironclaw/issues/7891)** (10 comments) — The most active discussion today. Two Gmail calls (274ms, 290ms) cost 19.7 seconds due to 49,152 bytes of raw MIME headers being pushed into the prompt unasked. Users are closely watching this because it directly impacts latency and token costs. The fix ([PR #7944](https://github.com/nearai/ironclaw/pull/7944)) lands today, suggesting responsiveness to performance concerns.

2. **[Issue #7824 — Context projection: Pi-style compaction](https://github.com/nearai/ironclaw/issues/7824)** (4 comments) — References PinchBench results showing 227.7M input tokens ($10.31) versus 55.1M ($2.52) baseline, a 4x cost increase from thread replay. This is a systematic cost/quality tradeoff that the compaction barrier PR (#7954) begins to address.

3. **[Issue #6590 — Windows serve failure](https://github.com/nearai/ironclaw/issues/6590)** (3 comments) — Still open since July 23. Local dev fails on Windows because workspace root overlaps the default `/skills` root. This is a long-standing platform gap with no fix in sight.

4. **[Issue #7276 — Automatic promotion of conversation facts into durable memory](https://github.com/nearai/ironclaw/issues/7276)** (2 comments) — The parent epic coordinating the memory system work (Issues #7947–#7953). This is the most architecturally significant discussion, spanning memory admission, multi-provider support, and cross-conversation recall.

5. **[Issue #7903 — Persistent sandboxed executor decision spike](https://github.com/nearai/ironclaw/issues/7903)** (1 comment) — High-risk proposal to move the canonical agent loop into the Docker sandbox. Linked PR #7908 is open. This is a security-sensitive architectural decision.

## 5. Bugs & Stability

Ranked by severity:

1. **[HIGH] — Memory.write silent overwrites** ([Issue #7776](https://github.com/nearai/ironclaw/issues/7776), closed) — The read-modify-write CAS protected against torn writes but allowed stale full-document rewrites to silently clobber concurrent updates. Fixed via content hashing in PR #7907.

2. **[HIGH] — MCP tool catalog failure mode** ([PR #7964](https://github.com/nearai/ironclaw/pull/7964)) — A server that exceeds the resource ceiling publishes zero tools instead of truncating, silently dropping every tool already collected. This is especially dangerous because the failure is silent. Open PR applies the fix.

3. **[MEDIUM] — Unbounded performance regression** ([Issue #7891](https://github.com/nearai/ironclaw/issues/7891)) — Raw MIME headers pushed into prompts cost 14.3 seconds per turn. Mitigated by Gmail semantic output PR (#7944) and the HTML complexity gate issue (#7960).

4. **[MEDIUM] — Windows serve broken** ([Issue #6590](https://github.com/nearai/ironclaw/issues/6590)) — `ironclaw serve` fails outright on Windows due to workspace/skills root overlap. Open since July 23 with no fix.

5. **[LOW-MEDIUM] — MCP camelCase tool names silently skipped** ([Issue #7856](https://github.com/nearai/ironclaw/issues/7856)) — Discovery requires tool names to be directly usable as identifiers; camelCase names are dropped without notice.

6. **[LOW-MEDIUM] — Telegram pairing UX defects** ([Issue #7956](https://github.com/nearai/ironclaw/issues/7956), [Issue #7955](https://github.com/nearai/ironclaw/issues/7955)) — Unpaired senders get the command inventory instead of the pairing notice; personal-account linking shows a cryptic error when MTProto credentials are missing.

7. **[LOW] — CI nightly failures** ([Issue #7936](https://github.com/nearai/ironclaw/issues/7936)) — Playwright shard failures from stale landing-copy fixtures plus Postgres readiness gate flaking. Tracked but not yet fixed.

8. **[LOW] — Notification producer lifecycle** ([Issue #7876](https://github.com/nearai/ironclaw/issues/7876), closed) — Standardized deterministic IDs and best-effort publication; hardened by PRs #7899/#7900.

## 6. Feature Requests & Roadmap Signals

The roadmap signal is unambiguous: **persistent memory is the next major feature**. Issues #7647–#7953 form a cohesive, well-scoped epic:

- Shared learning router with bounded post-run proposals ([#7947](https://github.com/nearai/ironclaw/issues/7947))
- Stable memory commit/feedback/forget capabilities ([#7948](https://github.com/nearai/ironclaw/issues/7948))
- Deterministic admission with auto-or-approval promotion ([#7949](https://github.com/nearai/ironclaw/issues/7949))
- Native/mem0/Mnesis provider adapters ([#7950](https://github.com/nearai/ironclaw/issues/7950))
- Bounded active recall from provider memory ([#7951](https://github.com/nearai/ironclaw/issues/7951))
- Skill distillation routing ([#7952](https://github.com/nearai/ironclaw/issues/7952))
- Observability and evaluation gates ([#7953](https://github.com/nearai/ironclaw/issues/7953))

The parent epic [#7276](https://github.com/nearai/ironclaw/issues/7276) — automatically promoting conversation facts into durable cross-conversation memory — addresses the top user request from feedback in #7185. The shared review router PR (#7958) is the first implementation slice.

Other notable requests:

- **Voice-to-text in WebUI composer** ([#7867](https://github.com/nearai/ironclaw/issues/7867)) — The web UI is the only channel without voice input; Slack and Telegram already support it.
- **Automation lessons file** ([#7893](https://github.com/nearai/ironclaw/issues/7893), closed) — Per-automation lessons persisting operational knowledge between runs.
- **Streamed large artifact downloads** ([#7938](https://github.com/nearai/ironclaw/issues/7938)) — Blocked by fixed byte ceilings in the current assembly path.

These features likely land in the next minor release (1.4.0) alongside the MCP OAuth improvements ([#7940](https://github.com/nearai/ironclaw/issues/7940)) requesting CIMD support and the `resource` parameter.

## 7. User Feedback Summary

**Positive signals:** The weekly failure taxonomy in Issue #7937 indicates most officeqa failures are genuine model-quality errors on DeepSeek-V4-Flash, not infrastructure issues — suggesting the platform layer is stable. The GitHub producer improvements (decode content, PR #7965, tell the model scope) show responsiveness to model-visible quality issues.

**Pain points:**

- **Performance/cost on Gmail-heavy workflows** ([#7891](https://github.com/nearai/ironclaw/issues/7891)) — Users on email-heavy workflows are paying 4x token costs from full-thread replay. The compaction barrier and Gmail normalization directly address this.
- **Windows support is broken** ([#6590](https://github.com/nearai/ironclaw/issues/6590)) — A developer trying `ironclaw serve` on Windows cannot start. Open for 36 days.
- **MCP discovery failure mode** ([#7856](https://github.com/nearai/ironclaw/issues/7856)) — Tool names like `sendMessage` are silently skipped, which could make integrations appear as if they work but provide missing tools.
- **Telegram onboarding rough edges** ([#7955](https://github.com/nearai/ironclaw/issues/7955), [#7956](https://github.com/nearai/ironclaw/issues/7956)) — First-run experience is confusing when pairing is incomplete or configuration is missing.
- **Memory loss between conversations** ([#7276](https://github.com/nearai/ironclaw/issues/7276)) — Users expect facts from one conversation to persist to later ones. This is the single most valuable feature request currently in flight.

**Satisfaction:** The 31 merged PRs, including the Slack broadcast fix, Gmail performance work, and notification lifecycle hardening, indicate a proactive maintainer team. The failure taxonomy (Issue #7937) is a healthy practice for transparency.

## 8. Backlog Watch

- **[Issue #6590 — Windows serve failure](https://github.com/nearai/ironclaw/issues/6590)** (open 36 days, 3 comments) — A hard platform blocker with no fix or workaround in sight. Given the project targets developer tooling, Windows support should be prioritized.

- **[Issue #7856 — MCP camelCase tool discovery](https://github.com/nearai/ironclaw/issues/7856)** (open 4 days, 0 comments) — Reports a silent functional gap. The fix is trivial (normalize or explicitly reject camelCase names); the silence is the concern.

- **[Issue #7824 — Context projection](https://github.com/nearai/ironclaw/issues/7824)** (open 6 days, 4 comments) — References 4x token-cost inflation. While the compaction PR (#7954) landed, tracking issues call for a completed write pipeline (#7864). The performance concern remains live.

- **[Issue #7936 — Nightly CI failures](https://github.com/nearai/ironclaw/issues/7936)** (open 2 days, 0 comments) — Stale landing-copy fixtures and Postgres readiness gates have been failing nightly. The CI refactor PR (#7943) addresses some inventory issues but does not fix the stale fixtures.

- **[PR #7835 — Dependabot actions bump](https://github.com/nearai/ironclaw/pull/7835)** (open 5 days) — Includes `actions/setup-node` `4.0.2 → 7.0.0`, a major version jump that will require CI validation. Should be reviewed carefully before merge.

- **[Issue #5671 — LeakDetector rebuilt per JSON string](https://github.com/nearai/ironclaw/issues/5671)** (closed) — Performance issue closed today; confirms the maintainer team is systematically working through the performance backlog.

---

*Data as of 2026-08-28, sourced from the IronClaw GitHub repository (github.com/nearai/ironclaw).*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-28

## Today's Overview

LobsterAI saw a highly active development day on August 28, with 13 pull requests merged/closed and 7 issues updated, indicating a strong release-cycle push. One new release (2026.8.26) was published, primarily containing installer fixes for silent and web-first build scenarios. The majority of merged PRs today focused on renderer-side UI improvements, library thumbnail rendering, model list collapse features, and Windows installer hardening, suggesting a coordinated stabilization and polish phase. Two new open issues were filed today (both by the same user) concerning installer data-loss and unexpected credit drain — these are significant and warrant prompt maintainer attention. Overall project health appears solid with a regular release cadence and active contributor engagement, though the new data-loss report is a critical concern.

## Releases

**LobsterAI 2026.8.26** (published 2026-08-26) — This is a patch release focused on installer fixes:
- Fixed silent upload-first web builds support
- Removed banner display for dictbind silent package installations
- Additional unspecified installer-related fixes

Release URL: [v2026.8.26](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.8.26)

*Breaking changes:* None indicated. No migration notes were included for this release.

## Project Progress

**13 PRs merged/closed today** — no open PRs remaining at end of day. Highlights:

**Feature Development:**
- **#2568** ([feat: collapse more models and sync sidebar banner schedules](https://github.com/netease-youdao/LobsterAI/pull/2568)) — Merged `feat/more-models-collapse` into `release/2026.8.24`; groups optional models into a default-collapsed "More Models" section and adds server-synchronized sidebar banner scheduling with client-version gating, caching, and refresh recovery.
- **#2558** ([feat(auth): add rainbow animation to sidebar login CTA](https://github.com/netease-youdao/LobsterAI/pull/2558)) — Added rainbow border/glow animation to the logged-out sidebar login button with light/dark theme contrast preservation.

**Bugfixes & Stability:**
- **#2566** ([fix: win installer truncated payload hardening](https://github.com/netease-youdao/LobsterAI/pull/2566)) — Windows installer payload truncation protection.
- **#2551** ([fix: app update preserve ready state](https://github.com/netease-youdao/LobsterAI/pull/2551)) — App update flow now preserves ready state.
- **#2560** ([fix(installer): remove silent-install progress banner for all channels](https://github.com/netease-youdao/LobsterAI/pull/2560)) — `/S` silent installs now show zero installer-owned UI per contract; design spec and contract tests updated.
- **#2565** ([fix(library): optimize list query switching and reload states](https://github.com/netease-youdao/LobsterAI/pull/2565)) — Per-source snapshot tracking to prevent list flickering, stale query/cursor pollution, unified busy states, refresh progress indicators, and accessibility labels.
- **#2559** ([fix: library thumbnail rendering and publish resource management](https://github.com/netease-youdao/LobsterAI/pull/2559)) — Optimized grid image and PPTX first-slide thumbnail rendering with render-generation validation, frame-completion waits, blank detection and retry; subscription-based share/site deletion quota hints; improved share code display and durability warnings.
- **#2567 / #2563** ([Liuzhq/fix 2026.8.24](https://github.com/netease-youdao/LobsterAI/pull/2567) / [#2563](https://github.com/netease-youdao/LobsterAI/pull/2563)) — Renderer fixes for 2026.8.24 release branch.

**Test Coverage Enhancements:**
- **#1163** ([fix(定时任务): immediate-run feedback, optimistic updates, Gateway sync](https://github.com/netease-youdao/LobsterAI/pull/1163)) — Scheduled-task "Run Now" button now provides immediate visual feedback; IPC layer no longer blocks; state sync via optimistic updates instead of 15-sec polling wait.
- **#1165** ([add 75 Vitest unit tests for memory file and time-context prompt modules](https://github.com/netease-youdao/LobsterAI/pull/1165)) — Zero-coverage modules now fully tested (57 memory file + 18 time-context tests).
- **#1166** ([fix(agent): prevent duplicate custom agent names](https://github.com/netease-youdao/LobsterAI/pull/1166)) — Custom agent creation now validates against existing names to prevent ambiguity.

## Community Hot Topics

**Most active issue today:** [#2561 installer](https://github.com/netease-youdao/LobsterAI/issues/2561) (created 2026-08-27, 1 comment) — User reports that the upgrade process **"nukes and wipes entire projects folder"** if the installation directory contains the projects folder; user claims ~2000 credits lost. This likely references a destructive uninstall/upgrade flow that deletes the install root recursively. Newly filed, requires immediate attention. Note: this connects to the stale issue [#1173](https://github.com/netease-youdao/LobsterAI/issues/1173) about uninstall leaving the app running — together they suggest the installer/uninstaller lifecycle has real UX and safety problems.

**Second active issue:** [#2562 use the f words carefully drains 200 credits](https://github.com/netease-youdao/LobsterAI/issues/2562) — User claims the AI agent consumes ~200 credits per response when they use profanity, losing ~800 credits total. This is likely a misunderstanding of usage/OOM behavior, but indicates **cost visibility and control** are unclear to users — worth investigating whether profanity triggers unusual output-length or retry behavior.

**Stale but high-relevance:** [Issue #1179](https://github.com/netease-youdao/LobsterAI/issues/1179) — forced sandbox in v3.31, user unable to disable; reverted to 3.30. Now closed as stale, but the underlying **sandbox configurability** concern remains a governance topic for power users.

## Bugs & Stability

Ranked by severity:

**CRITICAL — Possible data loss during upgrade**: [#2561](https://github.com/netease-youdao/LobsterAI/issues/2561) — Upgrade wipes the entire projects folder if it resides inside the installation directory. User reports ~2000 credits lost. No fix PR exists yet; today's installer-focused PRs (#2566, #2560) do not explicitly address this scenario. *Special note: 2000 credits vs. 200 — worth verifying the actual cost model when projects are wiped.*

**HIGH — Explorer-mode stability**: [#1180](https://github.com/netease-youdao/LobsterAI/issues/1180) (closed as stale) — Modifying a custom agent (icon change) triggered repeated gateway restarts; deleting the agent resolved it. No associated fix PR was merged.

**MEDIUM — Uninstaller leaves process running**: [#1173](https://github.com/netease-youdao/LobsterAI/issues/1173) (closed as stale) — App remains functional after uninstall; user suspects malicious behavior, likely actually a background process not terminated by the uninstaller. Tied to broader installer lifecycle quality issues.

**MEDIUM — Text toggle regression**: [#2562](https://github.com/netease-youdao/LobsterAI/issues/2562) — 200 credits consumed per profanity-driven response cycle (800 total). Unclear if bug or user misunderstanding of cost model.

**LOW — Stale sandbox force-close**: [#1179](https://github.com/netease-youdao/LobsterAI/issues/1179) — Forced sandbox in 3.31 not user-disablable; closed as stale, no code change shipped.

## Feature Requests & Roadmap Signals

- **Multiple custom model providers** ([#1174](https://github.com/netease-youdao/LobsterAI/issues/1174), closed stale) — Users want to maintain several custom providers simultaneously, not just one. The PR [#2568](https://github.com/netease-youdao/LobsterAI/pull/2568) collapsing model lists hints that the model-management UI is being refined for scale; multi-provider support seems like a natural next step and likely to land within 1–2 releases.

- **Proactive share-file management** — PR [#2559](https://github.com/netease-youdao/LobsterAI/pull/2559) added subscription-based quota hints and deletion warnings for share files and sites. This suggests a broader library/resource lifecycle management initiative is in progress.

- **Login CTA engagement** ([#2558](https://github.com/netease-youdao/LobsterAI/pull/2558)) — Rainbow animation on the login button signals a push to increase authenticated conversion; expect more user-account-centric features (sync, quotas) soon.

- **Cost transparency** — Issue [#2562](https://github.com/netease-youdao/LobsterAI/issues/2562) highlights the need for per-session or per-call credit accounting and usage notifications; a cost dashboard or limits feature is plausible in the next roadmap cycle.

## User Feedback Summary

- **Positive**: The release cadence is fast and responsive to installer issues (three installer-focused PRs merged today alone). Users are adopting advanced library management features (thumbnails, sharing quotas), indicating product-market fit for work-oriented features.

- **Negative / Pain Points**:
  - **Data-loss risk** (Issue [#2561](https://github.com/netease-youdao/LobsterAI/issues/2561)): Installation-folder projects being wiped is a severe trust breaker; even one occurrence damages confidence.
  - **Forced sandboxing** (Issue [#1179](https://github.com/netease-youdao/LobsterAI/issues/1179)): power users, including corporate/enterprise users, want sandbox-control escape hatches.
  - **Uninstaller leaves processes running** (Issue [#1173](https://github.com/netease-youdao/LobsterAI/issues/1173)): triggers suspicion of hidden behavior; even if benign, hygiene must be fixed.
  - **Agent-name duplication** (fixed in [#1166](https://github.com/netease-youdao/LobsterAI/pull/1166)): real usability friction when managing multiple custom agents — this fix addresses a genuine pain point.
  - **Unclear cost/credit accounting** (Issue [#2562](https://github.com/netease-youdao/LobsterAI/issues/2562)): users are confused about what triggers credit consumption and how to monitor it.

## Backlog Watch

- **#1162/#1163/#1165** ([Issue](https://github.com/netease-youdao/LobsterAI/issues/1162) / [PR #1163](https://github.com/netease-youdao/LobsterAI/pull/1163) / [PR #1165](https://github.com/netease-youdao/LobsterAI/pull/1165)) — Test-coverage improvements and scheduled-task UI feedback fixes from March were **closed today as stale**, but the underlying test gaps may still exist in the newer codebase. These were merged long ago; fine to treat as resolved.

- **#1174** ([Issue](https://github.com/netease-youdao/LobsterAI/issues/1174)) — Multi-provider support, closed as stale without any code merge. Maintainers should proactively reopen or address in favor of the roadmap.

- **#1179 / #1180 / #1173** — Power-user and stability issues closed as stale without resolution; if these patterns resurface in newer versions (e.g., sandbox forces in 2026.8.x), they should be re-prioritized with new reproductions.

- **Action required**: Maintainers should immediately triage [#2561](https://github.com/netease-youdao/LobsterAI/issues/2561) (data loss), reproduce the project-folder wipe, and ship a defensive installer/upgrader fix that refuses deletion outside the application directory or moves projects outside the install tree. Also follow up on [#2562](https://github.com/netease-youdao/LobsterAI/issues/2562) to document or instrument credit accounting.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-28

## 1. Today's Overview

Moltis shows a quiet but productive period over the last 24 hours. No new issues were opened or updated today, while two Pull Requests were merged and closed. A new release (`20260827.01`) was published, indicating continued active maintenance of the project. The absence of open issues or commented-on PRs suggests the project is in a relatively stable and calm phase. Overall, project health appears solid, with recent work focused on security hardening and API-compatibility fixes.

---

## 2. Releases

**New Release: `20260827.01`** — published 2026-08-27

This is a patch-level release. No breaking changes or migration steps were explicitly announced. The release corresponds to the two merged PRs below, so it primarily includes security validation for sandbox image requests and OpenAI-safe tool schema improvements.

_Release link: [moltis-org/moltis/releases](https://github.com/moltis-org/moltis/releases)_

---

## 3. Project Progress

Two PRs were merged/closed in the last 24 hours:

| PR | Title | Author | Date Updated | Focus |
|----|-------|--------|-------------|-------|
| [#1222](https://github.com/moltis-org/moltis/pull/1222) | `fix(web): validate sandbox image requests` | **tsauvajon** | 2026-08-27 | Security hardening for container and image handling |
| [#1232](https://github.com/moltis-org/moltis/pull/1232) | `fix(tools): make object schemas OpenAI-safe` | **IlyaBizyaev** | 2026-08-27 | Tool schema compatibility with OpenAI's strict mode |

**Summary of advances:**
- **PR #1222** adds validation for image references and package names before container or Dockerfile use, restricting package checks and image builds to operator administrators. Full administrative access is preserved for password, passkey, and trusted loopback identities. This is a security hardening measure.
- **PR #1232** addresses a critical interoperability issue: OpenAI's strict tool schemas reject objects without `additionalProperties=false` declared. This fix declares webhook patch fields, represents MCP environment variables as fixed name/value entries, and ensures Codex-compatible behavior.

Both PRs were closed rather than merged, which is worth noting — project maintainers should confirm this is correct and intended.

---

## 4. Community Hot Topics

No issues or PRs had comments or reactions today (all items report 0 comments, 0 👍). **No active community discussion was observed in the last 24 hours.** The most recent substantial interaction was PR #1232 (created 2026-08-22, closed 2026-08-27), which took ~5 days to resolve. The underlying need was clear: users attempting to integrate Codex/OpenAI tooling with Moltis encountered schema validation failures, which indicates active usage of Moltis's tool-calling surface with major AI platforms.

---

## 5. Bugs & Stability

No new bugs were reported today. Two stability-related fixes were shipped in the last 24 hours:

| Severity | Issue | Status | Fix |
|----------|-------|--------|-----|
| **High** | Potential container/image creation by unauthorized users (security) | Fixed | PR [#1222](https://github.com/moltis-org/moltis/pull/1222) |
| **Medium** | Tool schema incompatibility with OpenAI strict mode (null/empty values instead of requested data) | Fixed | PR [#1232](https://github.com/moltis-org/moltis/pull/1232) |

No crashes, regressions, or unresolved stability issues were reported.

---

## 6. Feature Requests & Roadmap Signals

No explicit feature requests were filed today. However, the two merged PRs signal roadmap direction:

- **AI platform compatibility** is clearly a priority, given the OpenAI/Codex-oriented fix in PR #1232. Future versions will likely continue to improve compatibility across AI tool-calling standards (e.g., Anthropic, Gemini).
- **Security hardening** of operator-facing operations (image validation, package checks) suggests a broader security policy effort may be underway.

Predictions for next release (`20260828.x`):
1. Additional security validation for other resource types (e.g., networks, volumes).
2. Follow-up fixes to schema definitions for additional providers.

---

## 7. User Feedback Summary

With zero comments, reactions, or issue reports in the last 24 hours, direct user feedback data is unavailable. The primary signals come from the fixes merged today:

- Users of Codex/OpenAI integrations experienced data-loss-like behavior (null/empty values sent instead of requested data) — this was successfully addressed.
- The security hardening in #1222 was likely prompted by the maintainer's review rather than user reports, though it closed a potentially serious vulnerability surface for multi-tenant deployments.

**Overall sentiment:** Neutral-positive. No complaints, but no enthusiastic discussion either.

---

## 8. Backlog Watch

No long-unanswered issues or PRs were identified in the current data window.

- Both PRs that were active were closed within 5–7 days of creation, which is a healthy turnaround.
- No issues are currently open, indicating an efficiently triaged queue.

⚠️ **Note on PR closures:** Both PRs were closed without being merged. If this was not intentional (i.e., the changes were not incorporated), it may indicate abandoned contributions. Maintainers should verify that the fixes from [#1222](https://github.com/moltis-org/moltis/pull/1222) and [#1232](https://github.com/moltis-org/moltis/pull/1232) are present in the released version `20260827.01`.

---

*Digest generated automatically from GitHub activity data for moltis-org/moltis. Data window: 2026-08-27 → 2026-08-28.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-28

## 1. Today's Overview

CoPaw (QwenPaw) is in a period of intense development activity, with 31 issues and 50 PRs updated in the last 24 hours — roughly a 50/50 open/closed split on both fronts. The project is clearly approaching a **2.2.0 release milestone**, evidenced by the draft release notes PR (#7348), a new "QwenPaw Hub" multi-tenant edition announcement issue (#7318), and an early mobile client draft PR (#7378). The maintainer team (rayrayraykk, zhijianma, cuiyuebing, jinglinpeng) has been actively merging fixes and closing issues, particularly around security, task tracking, and streaming behavior. The project demonstrates healthy maintainer responsiveness, with several long-standing issues (e.g., #2814, #6083, #4865) finally being closed. Startup performance, TLS stack issues, and channel-level bugs remain the most persistent community pain points.

---

## 2. Releases

No new releases were published in the last 24 hours.

However, notable release-related signals:
- **PR #7348 (OPEN)** — "chore: the release notes for v2.2.0" by cuiyuebing is being prepared, indicating a **2.2.0 stable release is imminent** (currently on 2.2.0b1).
- The project is also preparing for **QwenPaw Hub (multi-tenant edition)** which is targeted for **2.2.0** per issue #7318.

---

## 3. Project Progress

**Merged/Closed PRs today (25 total, notable highlights):**

| PR | Description | Significance |
|----|-------------|--------------|
| [#7375](https://github.com/agentscope-ai/QwenPaw/pull/7375) | **fix(governance): enforce File Guard paths in active policy evaluation** (fixes #7362) | Critical security fix — File Guard settings were only enforced in legacy ToolGuardEngine, not the newer GovernancePolicy path. Now properly blocks protected paths like `.qwenpaw.secret`. |
| [#7368](https://github.com/agentscope-ai/QwenPaw/pull/7368) | **fix(security): keep file guard active in off mode** | Security hardening — standardizes "Tool Approval Mode" labels across EN/CN/JA/KR; ensures guard remains active even in "Off" mode. |
| [#7349](https://github.com/agentscope-ai/QwenPaw/pull/7349) | **feat(tools): propagate console stop cancellation to agent tools** | User-facing improvement — stopping a chat now properly cancels running tools and sub-agents, preserving `CancelledError` for clean interruption state. |
| [#7374](https://github.com/agentscope-ai/QwenPaw/pull/7374) | **feat(console): auto-fold assistant process messages** | UX enhancement — reasoning and tool-call steps are automatically grouped/folded during streaming, keeping user-facing text visible. |
| [#7309](https://github.com/agentscope-ai/QwenPaw/pull/7309) | **refactor(task-tracker): use structured events** | Infrastructure — replaces SSE parsing with JSON-compatible event snapshots, enabling cleaner event broadcast. |
| [#7337](https://github.com/agentscope-ai/QwenPaw/pull/7337) | **fix(providers): separate model output capabilities from request limits** | Correctness fix — prevents unknown model output capabilities from silently becoming request-level `max_tokens` limits. |
| [#7354](https://github.com/agentscope-ai/QwenPaw/pull/7354) | **fix(installer): clarify application data cleanup** | DX improvement — Windows NSIS uninstall cleanup option now clearly explained across 6 languages, addresses #7188. |
| [#7373](https://github.com/agentscope-ai/QwenPaw/pull/7373) | **chore(deps): bump agentscope to 2.0.7.post1** | Dependency update. |

**Open/In-progress PRs worth noting:**
- [#7378](https://github.com/agentscope-ai/QwenPaw/pull/7378) — **feat(mobile): QwenPaw native mobile experience** (Expo/React Native; DO NOT MERGE draft)
- [#7361](https://github.com/agentscope-ai/QwenPaw/pull/7361) — **feat(chats): paginate long chat history + virtualize transcript** (addresses freeze issue on large conversations)
- [#7351](https://github.com/agentscope-ai/QwenPaw/pull/7351) — **fix(console): route Agent source uploads** (fixes #7322 where uploads land in workspace root regardless of selected category)

---

## 4. Community Hot Topics

### [#7318 — QwenPaw Hub multi-tenant edition (10 comments, 1 👍)](https://github.com/agentscope-ai/QwenPaw/issues/7318)
The highest-engagement issue today. The community has been asking for team/multi-user support; the maintainers are now designing QwenPaw Hub for 2.2.0 and asking for feature input. Signals a major product direction shift from personal assistant to team platform.

### [#2814 — Multi-agent chat history empty for running callee agent (7 comments, CLOSED)](https://github.com/agentscope-ai/QwenPaw/issues/2814)
Long-standing bug (opened April 2026) finally closed. During multi-agent conversations, the callee agent's chat page showed empty history while streaming. The closure suggests a fix landed — relevant PR work around streaming/SSE events (#7309, #7374) may have addressed this.

### [#7298 — OpenSSL 3.0.x TLS stack in Desktop/Docker (7 comments)](https://github.com/agentscope-ai/QwenPaw/issues/7298)
Carrier networks reset TLS handshakes on the Python 3.11-era OpenSSL stack shipped in Tauri bundles and Docker images. Desktop users have no workaround. Related PR [#7372](https://github.com/agentscope-ai/QwenPaw/pull/7372) (unify packaged Python runtime source) appears to be the fix in flight.

### [#4770 — 左侧会话界面列顺序调整 (6 comments, CLOSED)](https://github.com/agentscope-ai/QwenPaw/issues/4770)
Users want column reordering in the left sidebar conversation view — specifically moving "update by time" to be left-visible and shoving ID/session ID to the right (or hiding them). Closed, indicating the UX improvement likely landed.

### [#6273 — Unify task tracking and same-session concurrency semantics (5 comments, CLOSED)](https://github.com/agentscope-ai/QwenPaw/issues/6273)
Bugs where task tracking and concurrency behave differently depending on execution entry point (some paths serialize work, some silently drop payloads). Closed in conjunction with PR #7309 and #7299.

---

## 5. Bugs & Stability

**Ranked by severity:**

### Critical
1. **[#7362 — 文件保护未生效 (File Guard not enforced) — CLOSED](https://github.com/agentscope-ai/QwenPaw/issues/7362)**
   - File Guard settings were ignored by the governance policy path; protected paths (e.g., `/etc/passwd`) were readable when they shouldn't have been.
   - **Fix:** [#7375](https://github.com/agentscope-ai/QwenPaw/pull/7375) merged — now enforced in active policy evaluation. Also [#7368](https://github.com/agentscope-ai/QwenPaw/pull/7368) keeps guard active in "Off" mode.

2. **[#7296 — OpenAI Responses multi-turn 400 on stateless upstreams — CLOSED](https://github.com/agentscope-ai/QwenPaw/issues/7296)**
   - Reasoning item references expire on stateless providers (OpenCode Zen/Go Muse Spark), breaking multi-turn conversations on 2nd turn. Fixed.

### High
3. **[#7363 — Synchronous calls freeze event loop, timeout never fires](https://github.com/agentscope-ai/QwenPaw/issues/7363)**
   - Windows Desktop becomes unresponsive for 118–135s at startup and ~126s when sending a message. Event loop is blocked by synchronous calls.

4. **[#7367 — Importing all 18 channel modules unconditionally (30–45s startup)](https://github.com/agentscope-ai/QwenPaw/issues/7367)**
   - Even with only `console` enabled, all channel SDKs are imported at startup; `lark_oapi` alone takes ~18.5s. Related to general startup slowness complaints (#7360, #7023).

5. **[#7364 — Zero-downtime reload reuses closed memory_manager](https://github.com/agentscope-ai/QwenPaw/issues/7364)**
   - After reload bursts, `memory_search` permanently breaks because a closed service is reused without calling `start()`.

6. **[#7370 — WeCom channel: base64 image → OSError Errno 36](https://github.com/agentscope-ai/QwenPaw/issues/7370)**
   - Sending a data-URI image results in "File name too long" crash, surfaced to users as generic "Internal error."

### Medium
7. **[#7360 — Desktop startup takes ~4 minutes (V2.2.0.b1)](https://github.com/agentscope-ai/QwenPaw/issues/7360)** — likely same root cause as #7367 + Playwright install (#7023).
8. **[#7312 — Windows Python hangs in execute_shell_command](https://github.com/agentscope-ai/QwenPaw/issues/7312)** — missing `stdin=DEVNULL` on inherited pipe.
9. **[#7377 — Agent Loop mode resets after task runs](https://github.com/agentscope-ai/QwenPaw/issues/7377)** — configuration not persisted across runs in v2.1.0 console.
10. **[#7302 — DingTalk channel sends empty messages when tool info hidden](https://github.com/agentscope-ai/QwenPaw/issues/7302)** — triggers unread badge in chat app.

### Confirmed fixed today (related to earlier reports)
- Silent message drops when agent busy — #5344 (CLOSED via PR #7299)
- Concurrent cron races with `share_session=true` — #4217 (CLOSED)
- Non-streaming `write_file` rendering in console — #4865 (CLOSED, likely the #7374 auto-fold fix)

---

## 6. Feature Requests & Roadmap Signals

### High Confidence for 2.2.0 (announced or in active PRs)
- **QwenPaw Hub (multi-tenant edition)** — #7318: team deployment, admin-managed skills. Community input being solicited.
- **Native Mobile Client** — PR #7378: Expo/React Nativefor Android & iOS; Chat, Agents, Community, Workbench surfaces.
- **Release notes preparation** — PR #7348 confirms 2.2.0 is in final stages.

### Likely in 2.2.0 or soon after
- **Per-session model overrides** — PR #5992 (open since July): one agent, different LLMs per conversation; opt-in.
- **Chat history pagination + virtualization** — PR #7361: tackles UI freeze on large conversations.
- **Agent source upload routing** — PR #7351: fix for files landing in wrong workspace directories.
- **Oversized tool result bounding** — PR #7331: truncate large single-line tool outputs, preserve full result as workspace artifact.

### Community suggestions gaining traction (potential future)
- **Tool result simplification** — #7316: LLM-driven tool to strip/fold useless tool outputs to optimize context window.
- **Browser Enter-key handling on mobile** — #7355: Enter should not submit on Android Chrome; move attachment icon for portrait mode.
- **Deploy version visibility** — #7366: show the upgradable version number on agentscope.io/deploy to avoid blind upgrades.
- **Workspace artifact quick-access in Desktop** — #6083 (CLOSED today): one-click access to generated files from the Desktop window (was addressed).

---

## 7. User Feedback Summary

### Recurring pain points
- **Startup latency** dominates complaints: #7360 (4 min), #7367 (30–45s), #7023 (60s Playwright install), #6380 (1.5h updates on HDD). Users want lazy-loading, skipped non-essential steps, and incremental updates.
- **Channel reliability issues**: DingTalk empty messages (#7302), QQ memory loss (#7297), WeCom image crash (#7370) — users are actively integrating QwenPaw with real messaging workflows and hitting rough edges.
- **File management confusion**: Uploads not routed to selected category (#7322), File Guard being bypassed (#7362), column ordering in session list (#4770).
- **Context window waste**: Users are aware of token waste on verbose tool outputs (#7316) — sophisticated user base thinking about optimization.

### Positive signals
- Long-standing bugs are being closed in batches (multi-agent history #2814, concurrency #6273, silent drops #5344, streaming #4865) — users are noticing the maintainers' responsiveness.
- Installer clarity fix (#7188 → #7354) shows attention to non-technical users on Windows.
- The community's multi-tenant request (#7318) is being actively answered with a Hub roadmap — strong maintainer-community alignment.

---

## 8. Backlog Watch

### Long-unanswered issues needing maintainer attention

1. **[#6380 — Update flow takes ~1.5 hours on HDD](https://github.com/agentscope-ai/QwenPaw/issues/6380)** — opened 2026-07-23, no maintainer response visible. High user impact for NAS users.

2. **[#7023 — Desktop blocks 60s on Playwright install at startup](https://github.com/agentscope-ai/QwenPaw/issues/7023)** — opened 2026-08-14; a related PR [#7057](https://github.com/agentscope-ai/QwenPaw/pull/7057) is open but focused on PATH, not the lazy-load issue.

3. **[#5992 — Per-session model overrides (PR)](https://github.com/agentscope-ai/QwenPaw/pull/5992)** — open since 2026-07-12, under review for over a month. Needs a decision (merge/shelve/close).

4. **[#6874 — MCP tool call timeout (PR)](https://github.com/agentscope-ai/QwenPaw/pull/6874)** — open since 2026-08-10, no recent maintainer activity despite being requested in #6724.

5. **[#7296 — Desktop/Docker OpenSSL 3.0.x TLS stack](https://github.com/agentscope-ai/QwenPaw/issues/7298)** — carrier-level TLS resets; PR #7372 exists but is brand new (not yet merged); monitor for follow-through.

### Overdue closures / decisions
- **[#7297 — QQ restart loses last conversation memory](https://github.com/agentscope-ai/QwenPaw/issues/7297)** — acknowledged but no visible fix PR; likely related to memory manager reload bugs (#7364).
- **#7316 — Tool output simplification design question** — good architectural discussion with potential as a future enhancement; no maintainer acknowledgment yet.

---

*Data sources: CoPaw GitHub repo (agentscope-ai/QwenPaw), issues and PRs updated between 2026-08-27 and 2026-08-28.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest
**Date:** 2026-08-28

---

## 1. Today's Overview

ZeroClaw is in a high-activity period with 29 issues and 50 PRs updated in the last 24 hours, reflecting a mature project in active stabilization. The v0.8.5 release line is in its final week (ending August 30), with maintainers actively working through a substantial RFC backlog (~15 open RFCs) covering architecture, security, and runtime concerns. The project shows a healthy mix of community contributions and maintainer-led work, with several "distinguished contributor" PRs active. However, there is a notable concern: the majority of open PRs are flagged with `needs-author-action` or `stale-candidate`, suggesting contributor responsiveness may be a bottleneck. The most significant architectural debates center on runtime session ownership (#9487), attachment architecture (#9488), and WASM plugin composability (#10076), indicating a platform-level evolution from a single-agent tool to a more composable, channel-agnostic runtime.

---

## 2. Releases

No new releases in the last 24 hours. The v0.8.5 stabilization line (tracked in [#9459](https://github.com/zeroclaw-labs/zeroclaw/issues/9459)) is scheduled to end August 30, 2026. Weekly cuts are shipping ready work without waiting for all milestone items.

---

## 3. Project Progress

**Merged/Closed PRs (2):**

- **[#10416](https://github.com/zeroclaw-labs/zeroclaw/pull/10416) — fix(runtime): detect context overflow through error causes** (merged, by jstar0): Improves `is_context_window_exceeded` to inspect the full `anyhow::Error` source chain instead of only the outer display string, fixing a bug where reliable provider wrappers were shadowing loop-level recovery paths (addresses #10329).
- **[#10413](https://github.com/zeroclaw-labs/zeroclaw/pull/10413) — test(channels): keep Telegram photo upload test offline** (merged, by ump45nose): Replaces real `api.telegram.org` request in test with local Wiremock endpoint, improving CI reliability.

**Closed Issues (3):**
- [#8720](https://github.com/zeroclaw-labs/zeroclaw/issues/8720) — Support request for disabling cachePoint for Bedrock Nova 2 Lite via config (resolved)
- [#10264](https://github.com/zeroclaw-labs/zeroclaw/issues/10264) — Make Quickstart CLI validation tests locale-independent (completed)
- [#10329](https://github.com/zeroclaw-labs/zeroclaw/issues/10329) — Resilient wrapper truncation shadows loop-level context overflow recovery (fixed by #10416)

**Notable Active PRs (not yet merged):**
- [#10380](https://github.com/zeroclaw-labs/zeroclaw/pull/10380) — Restore persisted ACP transcripts in ZeroCode (features directly addresses #10286)
- [#10411](https://github.com/zeroclaw-labs/zeroclaw/pull/10411) — Serialize same-session messages to prevent parallel runs (addresses #10408)
- [#10374](https://github.com/zeroclaw-labs/zeroclaw/pull/10374) — Keep ZeroCode input responsive during daemon reconnection

---

## 4. Community Hot Topics

The most active discussions are all centered on architecture and security:

1. **[#9487 — RFC: Runtime-owned conversation sessions and transport surface adapters](https://github.com/zeroclaw-labs/zeroclaw/issues/9487)** (27 comments): The most active topic. Debates ownership boundaries for session persistence across the runtime. Revision 2 (2026-08-03) ratifies ownership boundary with #9488/#9600. This is a foundational architecture decision affecting all channels.

2. **[#9488 — RFC: Unified attachment architecture for web chat and channels](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)** (21 comments): Now at Revision 9. Discusses how attachments should flow across different channels. Early-stage but already showing maintainer engagement.

3. **[#6850 — RFC: Decouple memory lifecycle policy from storage backends](https://github.com/zeroclaw-labs/zeroclaw/issues/6850)** (20 comments): Open since May 22, this RFC proposes a clearer boundary between durable memory storage and lifecycle policy. The long-duration discussion (3 months) suggests it touches core architectural boundaries.

4. **[#9600 — Tracker: Session-persistence contract ownership and layer ordering](https://github.com/zeroclaw-labs/zeroclaw/issues/9600)** (14 comments): Coordination tracker for four independent workstreams that touch the same persistence contract. Indicates ongoing complexity in the session management space.

5. **[#8692 — Tracker: Maintainer decision queue for RFCs and design issues](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)** (14 comments): Active tracking of the RFC decision queue — evidence that maintainers are working through the backlog systematically.

**Analysis:** The community/team is clearly focused on architectural consolidation: session ownership, attachment handling, and memory policy. These are foundational decisions that will shape ZeroClaw's next major version. The repeated revision histories (e.g., #9488 at Rev 9, #9487 at Rev 2) show the RFC process is alive and iterating.

---

## 5. Bugs & Stability

**Ranked by severity:**

***Priority P1 (workflow-blocking):***

- **[#10324](https://github.com/zeroclaw-labs/zeroclaw/issues/10324)** — [Bug]: cron manual trigger and run-history reads remain check-then-act across an agent rename. Filed at S2 severity but accepted as P1. Cross-agent boundary could allow a job to target the wrong agent. **No fix PR yet.**
- **[#10063](https://github.com/zeroclaw-labs/zeroclaw/issues/10063)** — [Bug]: Anthropic-backed compatible gateways reject image_url blocks inside tool results. S1 severity — a custom provider can fail when a tool returns an image. Accepted, no fix PR yet.

***Priority P2 (degraded behavior):***

- **[#10408](https://github.com/zeroclaw-labs/zeroclaw/issues/10408)** — Second message during active turn starts parallel run → duplicate work/reply. **Fix PR exists: #10411** (serialize same-session messages; status: needs-author-action).
- **[#10237](https://github.com/zeroclaw-labs/zeroclaw/issues/10237)** — Telegram reply-threads fragment conversation memory into per-thread buckets, losing multi-turn context. **No fix PR yet.**
- **[#10186](https://github.com/zeroclaw-labs/zeroclaw/issues/10186)** — Terminal fallback text bypasses live delivery seams (S2). **No fix PR yet.**
- **[#10329](https://github.com/zeroclaw-labs/zeroclaw/issues/10329)** — Resilient wrapper truncation shadows context-overflow recovery (closed today, fixed by #10416).
- **[#10286](https://github.com/zeroclaw-labs/zeroclaw/issues/10286)** — Restored ZeroCode transcripts omit persisted turns after history trimming. **Fix PR exists: #10380.**

***Priority P3 (minor):***

- **[#10326](https://github.com/zeroclaw-labs/zeroclaw/issues/10326)** — Reliable streaming errors report requested model instead of served pinned model. **Fix PR exists: #10415** (needs-author-action).

**Security Concern:**
- **[#10409](https://github.com/zeroclaw-labs/zeroclaw/issues/10409)** — PR (by arena-ai-coding-agent[bot]): Secure temp file handling with 0o600 permissions to prevent leaking voice messages/images on shared systems. Currently open, no comments.

---

## 6. Feature Requests & Roadmap Signals

**Strong Signals (accepted or in-progress):**

1. **[#6996 — RFC: Granular sandbox policy](https://github.com/zeroclaw-labs/zeroclaw/issues/6996)** (filesystem/network restrictions): In-progress, needs-maintainer-review. Next evolution of agent security after #7155 was accepted.

2. **[#6909 — RFC: Computer-use support for desktop screen interaction](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)**: Revision 2 (2026-08-24) integrates accepted #7155 confirmation boundary. Currently needs-maintainer-review. Likely a v0.9+ feature.

3. **[#9330 — RFC: AI-assisted PR pre-review and re-review](https://github.com/zeroclaw-labs/zeroclaw/issues/9330)**: Ratifying existing `pr-review-pilot` behavior as SOP. In-flight — could land in v0.8.6 or v0.9.

4. **[#10076 — RFC: Composable WASM plugin runtime architecture](https://github.com/zeroclaw-labs/zeroclaw/issues/10076)**: New (2026-08-18) but active. Extends the WASM plugin surface with typed extension points and replaceable providers. Architecturally significant; likely a v0.9+ item.

5. **[#10306 — Task: Gate web/ TypeScript in required CI](https://github.com/zeroclaw-labs/zeroclaw/issues/10306)** (accepted): Stop bare `tsc` from printing 75 misleading errors. PR #10399 (typecheck generated dashboard contract) exists.

**New Feature Requests (today):**

- **[#10419 — Stream agent-loop tokens from POST /webhook (SSE)](https://github.com/zeroclaw-labs/zeroclaw/issues/10419)**: New (created 2026-08-28) — hosted Path A workers need SSE streaming.
- **[#10421 — Paginate persisted ACP transcript restoration in ZeroCode](https://github.com/zeroclaw-labs/zeroclaw/issues/10421)**: New (2026-08-28), follows from #10380's full transcript restoration.

**Prediction:** The v0.8.5 line will likely include the Telegram model picker (#9997), Windows test measurement (#10350), and CI fixes. The session/serialization fixes (#10411, #10380) are likely near-term candidates given they fix accepted bugs. The broader RFCs (sessions, attachments, WASM composability) will likely become v0.9.0 items, given the v0.8.5 freeze date.

---

## 7. User Feedback Summary

**Pain points expressed:**

- **Bedrock config pain** (#8720): A user needed to disable caching for Bedrock Nova 2 Lite via config to avoid random errors — the config file wasn't sufficient for their use case. This is now closed, but indicates config flexibility concerns for cloud providers.
- **Context overflow hidden by wrapper** (#10329): Users see errors but the real cause (context overflow) is masked by the resilient provider wrapper — a debugging/visibility issue.
- **Parallel runs create duplicates** (#10408): A user reported that sending a second message during processing creates duplicate work — likely confusing chat behavior.
- **Telegram thread memory fragmentation** (#10237): Real usability issue where reply-threads break conversation continuity.
- **Tool result images fail** (#10063): A user's custom provider works for direct images but fails when tools return images — a compatibility gap.

**Signals of positive engagement:**
- Multiple "fix" PRs have been quickly filed for reported issues (e.g., #10411 for #10408, #10380 for #10286)
- The RFC process is actively used, with maintainers iterating on proposals
- Non-maintainer contributors (e.g., minato32, ump45nose, jstar0) are regularly submitting and getting PRs merged

---

## 8. Backlog Watch

**Long-stalled, high-importance items needing maintainer attention:**

1. **[#6850 — RFC: Decouple memory lifecycle policy from storage backends](https://github.com/zeroclaw-labs/zeroclaw/issues/6850)** (open since 2026-05-22, 20 comments): Active discussion but no clear decision. Core architectural issue; the "no-stale" flag is the only thing preventing silence.

2. **[#9826 — fix(cli): refuse to run when an agent's shell spawned the process](https://github.com/zeroclaw-labs/zeroclaw/pull/9826)** (by JordanTheJet, open 3 weeks): Security-critical fix — an agent invoking the CLI runs with operator privileges. Status: `needs-author-action` (contributor hasn't updated). This is a **high-risk security gap** that should be prioritized.

3. **[#9724 — fix(approval): always_ask survives Full autonomy](https://github.com/zeroclaw-labs/zeroclaw/pull/9724)** (by kckylechen1, open 3+ weeks): Security-relevant — `always_ask` config is dropped in Full-autonomy mode. Status: `stale-candidate` + `needs-author-action`. **This should be escalated.**

4. **[#9283 — fix(tools): decompress gzip/brotli/deflate web_fetch responses](https://github.com/zeroclaw-labs/zeroclaw/pull/9283)** (open since 2026-07-23): Functional bug — compressed web content returns unreadable bytes. Status: `stale-candidate`. Three weeks without action on a tool that's likely widely used.

5. **[#10064 — fix(channels/telegram): self-destruct approval cards](https://github.com/zeroclaw-labs/zeroclaw/pull/10064)** (open since 2026-08-17): UX/security: stale approval cards can be accidentally tapped. Status: `stale-candidate`.

**General observation:** The `stale-candidate` and `needs-author-action` labels on many PRs suggest either contributor disengagement or maintainer capacity constraints. Given the upcoming v0.8.5 deadline, maintainers may want to explicitly close or take over stalled PRs to clear the queue.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*