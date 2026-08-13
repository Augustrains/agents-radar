# OpenClaw Ecosystem Digest 2026-08-13

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-13 00:54 UTC

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

Here is the structured OpenClaw project digest for 2026-08-13.

---

### 1. Today's Overview
OpenClaw demonstrates a very high maintenance velocity this week, with 500 issues and 500 PRs updated in the last 24 hours, indicating significant ongoing development and active community triage. The project maintains a high open-to-closed backlog ratio (roughly 4:1 for issues and 2:1 for PRs), suggesting the maintainers are prioritizing new work and fixes while facing a substantial volume of incoming reports. No new releases were published today, but a large number of "chore" and "fix" PRs are awaiting review, signaling a consolidation phase. A significant recurring theme among top issues is the reliability of subagent orchestration and message delivery, with multiple P1 bugs still open on these core systems.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Project Progress
Merged/Closed activity includes several high-priority fixes that are crucial for stability. Specifically, PR #122883 (fix(agents): repair extension fixtures for explicit ownership) was closed, addressing a CI failure and unblocking other PRs. The closure of issues like #57901 (Safeguard compaction ignores config) and #48579 (Compactions firing when mode is 'off') shows progress in refining the context management system. Active PRs, while not yet merged, signal development effort on fixing session-locking and delivery issues, including #122864 (fix(telegram): requeue aborted ingress claims) and #122850 (fix(matrix): keep streamed replies visible).

- **Merged/Closed PRs:**
    - [PR #122883](https://github.com/openclaw/openclaw/pull/122883): fix(agents): repair extension fixtures for explicit ownership
- **Key Open Fixes (Ready for Review):**
    - [PR #122831](https://github.com/openclaw/openclaw/pull/122831): fix(codex): keep sessionless mirror warnings out of onboarding

### 4. Community Hot Topics
The most engaged issues, with 45+ comments, are the longest-running open feature requests or bug reports. The conversation on [Issue #7707](https://github.com/openclaw/openclaw/issues/7707) about Memory Trust Tagging by Source (45 comments) shows a strong community interest in security posturing. The ongoing saga of [Issue #121058](https://github.com/openclaw/openclaw/issues/121058) regarding silent reply failures (91 comments) continues to dominate attention, although it was only created recently (2026-08-09). Activity in these threads often highlights a desire for greater transparency and control over the agent lifecycle.

### 5. Bugs & Stability
The most severe stability concerns remain focused on the subagent lifecycle and message delivery.

- **High Severity (P1):**
    - **Subagent/Message Loss:** A cluster of P1 issues remains open regarding subagent session management. [Issue #44925](https://github.com/openclaw/openclaw/issues/44925) (Subagent completions silently lost), [Issue #67777](https://github.com/openclaw/openclaw/issues/67777) (Subagent completion delivery lost), and [Issue #47975](https://github.com/openclaw/openclaw/issues/47975) (Subagent sessions persist, main session unresponsive) indicate a systemic problem with child-process lifecycle management. These have multiple linked PRs attempting fixes, but none are merged yet.
    - **Session Starvation:** [Issue #54488](https://github.com/openclaw/openclaw/issues/54488) (Session lane starvation) and [Issue #40611](https://github.com/openclaw/openclaw/issues/40611) (Heartbeat drift blocks Telegram) point to concurrency and scheduling flaws that effectively block arbitrary users from receiving replies.
- **Low/Medium Severity (P2/P3):**
    - Numerous P2 regressions were reported, including [Issue #111498](https://github.com/openclaw/openclaw/issues/111498) (Main agent blocked by workspace-state migration after auth recovery) and [Issue #115001](https://github.com/openclaw/openclaw/issues/115001) (Hybrid memory search returns spurious 1.0 scores).

### 6. Feature Requests & Roadmap Signals
Beyond bug fixes, the community is requesting quality-of-life improvements and new capabilities. Notable long-standing requests include:

- **Memory Trust & Security:** [Issue #7707](https://github.com/openclaw/openclaw/issues/7707) (Memory Trust Tagging) is a P2 with high engagement, suggesting it may be a candidate for a future security-focused release.
- **Configuration & UX:** Feature requests like [Issue #45758](https://github.com/openclaw/openclaw/issues/45758) (YAML support) and [Issue #45501](https://github.com/openclaw/openclaw/issues/45501) (configurable session reset prompt) remain open for months, indicating a backlog of community-desired ergonomics improvements.
- **Cost & Visibility:** [Issue #9016](https://github.com/openclaw/openclaw/issues/9016) (Expose OpenRouter usage cost) and [Issue #99583](https://github.com/openclaw/openclaw/issues/99583) (Session Auto-Titling) are signals for more advanced observability and session management features.

### 7. User Feedback Summary
User feedback this week is largely polarized by the severity of the bugs experienced. There is clear dissatisfaction and frustration (as evidenced by the 91 comments on the silent-reply failure issue) regarding **reliability and silent failures**, with users reporting lost work or unresponsive agents. Conversely, there is positive engagement on PRs for UI/UX improvements, such as [PR #122809](https://github.com/openclaw/openclaw/pull/122809) (fix(ui): model picker shifts), which shows the community testing and validating minor quality-of-life patches. The high number of `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision` labels on P1s suggests the community often identifies issues but feels blocked by the need for maintainer input to proceed.

### 8. Backlog Watch
Several long-standing P1 issues with associated PRs in "needs author" or "needs proof" status are at risk of stalling. They require maintainer attention to unblock.

- [Issue #43367](https://github.com/openclaw/openclaw/issues/43367) (Multi-agent orchestration is unstable) - P1, created 2026-03-11. This issue has a linked PR that is currently marked 'waiting on author'.
- [PR #90062](https://github.com/openclaw/openclaw/pull/90062) (fix(agent): infer agent from fresh session keys) - This PR fixes session-key parsing but has been open since 2026-06-03 and is currently in "needs proof" status.
- [PR #79405](https://github.com/openclaw/openclaw/pull/79405) (fix: harden subagent completion fallback delivery) - A critical fix for the P1 subagent-message-loss bugs, but open since 2026-05-08 with a 'waiting on author' label. This fix is high-risk if it remains stale while the issues it addresses (e.g., #44925) are still active.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date: 2026-08-13**

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is experiencing intense, convergent development across multiple projects, with a clear shift from single-agent chat interfaces toward multi-agent orchestration, plugin architectures, and cross-platform reliability. The ecosystem is bifurcating into two architectural camps: **fork-derived projects** (OpenClaw lineage: NanoClaw, PicoClaw, ZeptoClaw, TinyClaw, ZeroClaw, IronClaw) that inherit a common core and differentiate on channel integrations and deployment models, and **independent implementations** (NanoBot, Hermes Agent, CoPaw, LobsterAI) that are building distinctive agent frameworks from alternative foundations. Across all projects, subagent lifecycle reliability, silent message failures, memory/context management, and plugin extensibility have emerged as universal pain points, while token-cost optimization and cross-platform (Windows/macOS) support are becoming competitive differentiators. The ecosystem shows healthy community engagement (7 of 12 tracked projects active in the last 24 hours) but also reveals systemic challenges: maintainer review backlogs, long-stalled critical PRs, and recurring platform-specific regressions that suggest the space is maturing faster than its tooling.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs | Releases (24h) | Health Score |
|---------|---------------------|--------------------|--------------------|-----------------|--------------|
| **OpenClaw** | 500 | 500 | ~1 merged (high triage) | None | 7.5/10 |
| **Hermes Agent** | 50 | 50 | 2 | None | 7.0/10 |
| **ZeroClaw** | 50 | 50 | 14 | None | 8.0/10 |
| **NanoBot** | 8 | 36 | 17 | None | 8.5/10 |
| **CoPaw (QwenPaw)** | 29 | 42 | 15 | v2.1.0-beta.4 | 7.5/10 |
| **IronClaw** | 41 | 50 | 19 | v1.2.0-rc.2, rc.3 | 8.0/10 |
| **NanoClaw** | 4 | 10 | 0 (1 closed unmerged) | None | 6.5/10 |
| **PicoClaw** | 2 | 3 | 0 | None | 6.0/10 |
| **LobsterAI** | 6 | 8 | 7 | 2026.8.12 (in pipeline) | 7.0/10 |
| **NullClaw** | 0 | 0 | 0 | None | 4.0/10 |
| **TinyClaw** | 0 | 0 | 0 | None | 4.0/10 |
| **Moltis** | 0 | 0 | 0 | None | 4.0/10 |
| **ZeptoClaw** | 0 | 0 | 0 | None | 4.0/10 |

---

## 3. OpenClaw's Position

**Advantages:**

- **Scale dominance:** With 500+ issues and PRs updated daily, OpenClaw's community is 10-20x larger than its nearest competitor. This creates a virtuous cycle of faster bug identification, more contributing developers, and broader channel coverage.
- **Reference architecture status:** As the core reference implementation, OpenClaw defines the ecosystem's architectural patterns. Other projects (NanoClaw, PicoClaw, ZeroClaw) either fork its codebase or adopt its design patterns, effectively making it the "Linux kernel" of the personal AI assistant space.
- **Maintainer bandwidth:** Despite a 4:1 open-to-closed issue ratio, the project's large maintainer team can triage hundreds of items daily, preventing complete backlog paralysis.

**Technical Approach Differences:**

- **Language/stack:** Rust-based core with a CLI-first philosophy, whereas NanoBot uses a lightweight language-agnostic design and Hermes Agent leans on a Python ecosystem.
- **Extensibility:** OpenClaw emphasizes "claws" (extensions) and a modular agent architecture; Hermes Agent is pushing a more ambitious plugin API with versioned manifests, lifecycle event catalogs, and auxiliary model slots.
- **Sub-agent orchestration:** OpenClaw pioneered child-process subagent management but continues to struggle with systemic reliability issues (P1 bugs on message loss, session starvation) — an area where IronClaw's "Reborn" architecture and CoPaw's multi-agent session handling are innovating.

**Community Size Comparison:**

| Project | Community Signal |
|---------|-----------------|
| OpenClaw | Massive (500+ daily updates) |
| Hermes Agent | Large (50 daily updates, 18👍 on top issue) |
| ZeroClaw | Large (50 daily updates, 50% merge rate) |
| IronClaw | Moderate-Large (41 issues, 50 PRs daily) |
| CoPaw | Moderate-Large (29 issues, 42 PRs) |
| NanoBot | Moderate (36 PRs, 17 merged) |
| LobsterAI | Moderate (8 PRs, 7 merged) |
| NanoClaw / PicoClaw | Small but engaged |

---

## 4. Shared Technical Focus Areas

### 4.1 Subagent Orchestration & Reliability
- **OpenClaw:** P1 cluster — subagent completions silently lost (#44925, #67777), session lane starvation (#54488)
- **CoPaw:** Multi-subagent infinite loops (#6927), per-message shadow session creation (#6918)
- **IronClaw:** Telegram agent stuck after GIF (#7538), multi-agent session flow issues
- **NanoClaw:** PR #3316 fixing routed-agent context management
- **NanoBot:** Subagent transcript persistence (PR #5291)

### 4.2 Plugin Architecture Expansion
- **Hermes Agent:** Most aggressive push — 14+ coordinated issues/PRs for versioned plugin manifests, lifecycle events, discovery, and developer tooling (#64162–#64231, #84916–#84924)
- **NanoClaw:** Agent Plugins 1.0.0 format migration (PR #3220) with security hardening
- **OpenClaw:** "Claws" extension model, 500+ extension-related items
- **ZeroClaw:** Plugin-owned Kanban board RFC (#8832)
- **NanoBot:** Auto-discovery mechanism for agent hooks (#4878, merged)

### 4.3 Memory & Context Management
- **OpenClaw:** Memory Trust Tagging request (#7707), compaction fixes
- **CoPaw:** Memory pipeline documentation mismatch (#6853), scroll compression UI bug (#6951)
- **PicoClaw:** Routed-agent history/compression fix (PR #3316)
- **NanoClaw:** Context injection and cache-safe patterns
- **Hermes Agent:** Lazy tool schema loading (18👍, #6839) to reduce 3.5-5k token overhead

### 4.4 Cross-Platform (Windows/macOS) Reliability
- **ZeroClaw:** 74 Windows test failures (#7462), Windows CI expansion (#7461), PowerShell support (merged #9182)
- **CoPaw:** Windows crashes (#6955), idle freezes (#6780)
- **LobsterAI:** Windows plugin install EPERM fix (#2479), macOS icon fix (#2478)
- **OpenClaw:** Windows desktop gateway regressions in v0.20.0
- **Hermes Agent:** Termux/Android install break (#71331)

### 4.5 Token Cost Optimization
- **Hermes Agent:** Lazy tool schema loading (#6839, 18👍) — highest-upvoted issue this cycle
- **IronClaw:** Token estimator double-counting fix (#7485)
- **CoPaw:** Prefix cache optimization from unsorted tool schemas (#6952/PR #6953)
- **OpenClaw:** Configurable session reset, cost exposure requests (#9016)

### 4.6 Message Delivery & Channel Reliability
- **OpenClaw:** Silent reply failures (#121058, 91 comments), Telegram heartbeat drift, Matrix streaming issues
- **NanoBot:** Message repetition loops (#5327), Matrix reply threading
- **IronClaw:** Telegram webhook activation (#7535), sticker/GIF handling (#7538), message splitting (#7540)
- **NanoClaw:** Signal DM fixes (PR #2689), WhatsApp silent failures (PR #3086)

### 4.7 Security & Privacy
- **NanoBot:** ExecTool path-boundary hardening (3 PRs), Jina URL credential leak fix (#5258), session history relocation (#5279)
- **OpenClaw:** Memory Trust Tagging by source (#7707)
- **ZeroClaw:** SSRF gate improvement (#8713, waiting), release attestation consolidation (#9101)
- **Hermes Agent:** Secret-source plugin bootstrap fix (#64177)

---

## 5. Differentiation Analysis

| Project | Primary Distinction | Target User | Architecture |
|---------|--------------------|-------------|-------------|
| **OpenClaw** | Ecosystem reference; channel proliferation | Power users, self-hosters | Rust core, CLI-first, claw extensions |
| **Hermes Agent** | Plugin platform ambition | Developers building on agent platform | Plugin API v2, auxiliary model slots, stream hooks |
| **NanoBot** | Security-hardened lightweight agent | Security-conscious, Docker-first | Language-agnostic, minimal core, strong isolation |
| **ZeroClaw** | Developer workflow integration | CLI/TUI/ZeroCode users | Runtime + daemon model, PowerShell support, ZeroCode SOPs |
| **IronClaw** | Hosted/channel-first with NEAR integration | NEAR ecosystem, multi-channel ops | Cloud-native, "Reborn" architecture migration, IronHub registry |
| **CoPaw (QwenPaw)** | Qwen-specific optimization | Chinese-speaking users, Qwen models | Alibaba ecosystem, DataPaw native apps, MCP-first |
| **NanoClaw** | Security-hardened agent templates | Enterprise, template-driven | Agent Plugins 1.0.0, OneCLI, migration-focused |
| **PicoClaw** | Lightweight web UI assistant | Small deployments, Sipeed hardware ties | Simple architecture, web search providers |
| **LobsterAI** | Desktop GUI experience | Windows/macOS desktop users | Electron-based, visual editor, model-provider config |
| **Inactive (Null/Tiny/Moltis/Zepto)** | Low-maintenance forks | Hobbyists, niche users | OpenClaw-descendant, low development velocity |

---

## 6. Community Momentum & Maturity

### Tier 1: Rapidly Iterating (High Velocity, High Responsiveness)
- **NanoBot** (17 PRs merged/24h, 83% merge rate, security-focused)
- **IronClaw** (19 PRs merged/24h, RC releases shipping daily, QA bug-bash active)
- **ZeroClaw** (14 PRs merged/24h, 50% merge rate, tracked CI expansion)
- **CoPaw** (15 PRs merged/24h, daily beta patches, active Chinese community)

### Tier 2: Active Development (High Volume, Mixed Velocity)
- **OpenClaw** (Massive activity but 2:1 open:closed PR ratio, P1s stranded)
- **Hermes Agent** (High issue/PR volume, plugin push coordinated but review queue growing 48:2)
- **LobsterAI** (Strong merge discipline, quiet issue queue with aging bugs)

### Tier 3: Moderate Engagement
- **NanoClaw** (Active architecture work, no merges in 24h, long-stalled PRs)
- **PicoClaw** (Steady contributions, no merges, stale issue flags)

### Tier 4: Dormant
- **NullClaw, TinyClaw, Moltis, ZeptoClaw** (No activity in 24h)

---

## 7. Trend Signals

### 7.1 From Chatbots to Agent Platforms
The plugin architecture expansion across Hermes Agent (#84916–#84924), NanoClaw (#3220), and ZeroClaw (#8832) signals a shift: users no longer want a "chatbot with tools" — they want a **platform** where they can build, version, package, and share agent capabilities. Expect plugin registries and discovery to become table stakes.

### 7.2 Token Economy Becomes a Feature
With 18👍 for lazy tool loading (#6839) and multiple projects shipping token-estimator and prefix-cache fixes, **token efficiency is a headline feature**, not a backend concern. Local-model users and API-cost-conscious developers will choose platforms that minimize per-request overhead. Agent developers should expose cost/usage transparency as a first-class UI feature.

### 7.3 Silent Failures Are the Ultimate Anti-Product
Across OpenClaw (silent reply loss), CoPaw (silent task stops), and NanoClaw (silent WhatsApp drops), **failure transparency** is emerging as the most-cited user pain point (91 comments on #121058). Users would rather see an error than an unresponsive agent. Implement explicit failure surfacing, "still working" feedback, and reconnection/requeue mechanisms as core features.

### 7.4 Cross-Platform is a Retention Driver
ZeroClaw's 74 Windows test failures and CoPaw's Windows crash cluster show the community is increasingly expecting **production-grade desktop/Windows support**. Projects shipping macOS/Linux-only will see churn. This also extends to architecture: both ARM64 and x86_64 matter (Termux/Android, Raspberry Pi, Railway).

### 7.5 Security Audits by Users are Accelerating
NanoBot's ExecTool hardening (3 merged PRs) and Jina URL fix (#5258) came from external contributors — a sign that the community is **auditing rather than just using**. Projects that respond quickly to security findings will build trust; those that sit on SSRF fixes (ZeroClaw #8713, 40 days) risk damage.

### 7.6 Channel-First is the New Onboarding
IronClaw's "channel-first approach" epic (#7044) and the OOBE work (PR #6994) point to a shift: users no longer want to configure a web UI; they want to **open Telegram/Discord/Slack and start using the agent there**. Expect channel onboarding and webhook auto-configuration to be expected defaults.

### 7.7 Structured Execution Contracts
IronClaw's structured execution contracts for automations (PR #7548) and the growing demand for observability (ZeroClaw's SOP status icons) signal that **agent work is becoming more auditable and governed**. Users want to know what an agent is doing, why it stopped, and what it produced — and increasingly, they want that in a reviewable, contract-based format.

### 7.8 Qwen/Chinese-Ecosystem Growth
CoPaw's vibrant Chinese community (50% of issues) and QwenCloud provider requests (NanoClaw #3232) suggest the Qwen model family and Alibaba ecosystem are becoming a **first-class agent platform base**. Western developers should watch for cross-pollination opportunities.

---

## Summary for Decision-Makers

The ecosystem is consolidating around four core competencies: **reliable multi-agent orchestration, plugin extensibility, token efficiency, and cross-platform robustness**. OpenClaw leads in mindshare and scale but is vulnerable on reliability (P1 subagent loss) and review bandwidth. **NanoBot and IronClaw show the best merge discipline and responsiveness**; **Hermes Agent is the most ambitious on plugin architecture**; **CoPaw leads in Qwen/China-specific innovation**. Projects without activity (NullClaw, TinyClaw, Moltis, ZeptoClaw) are effectively maintenance-mode. For developers choosing a platform: prioritize **silent-failure handling and transparency** (few projects do this well), **token/usage visibility**, and **plugin/extension API stability** — these three factors dominate user-reported satisfaction across all projects this cycle.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-13

## 1. Today's Overview

NanoBot's development activity remains high, with 36 PRs updated in the last 24 hours (19 open, 17 merged/closed), alongside 8 issues (4 resolved, 4 active). A substantial cluster of security-focused fixes landed, particularly around `ExecTool` path-boundary enforcement, Jina reader URL handling, and Docker privilege-drop capabilities — reflecting ongoing hardening efforts. The community is actively contributing both feature work (DeepSeek V4 Pro Responses support, WebUI session collaboration) and reliability enhancements (Matrix reply threading, stale-session race-condition fixes). No new releases were published in this window, but the volume of merged work targeting p1 security and stability issues suggests a meaningful release may be imminent. Maintainer engagement appears strong, with several long-running PRs receiving recent activity and conflict-resolution updates.

## 2. Releases

No new releases were published during the reporting window. (No release notes, change logs, or migration guidance to summarize.)

## 3. Project Progress — Merged/Closed PRs

Seventeen PRs were merged or closed in the last 24 hours, showing a strong bias toward security and reliability fixes:

- **[#5320] fix(docker): restore capabilities for privilege drop** — Closed. Restores `cap_drop: ALL` while preserving three capabilities required for the root bootstrap path and enables `no-new-privileges` to prevent privilege regain. Hardens the Docker deployment path.
- **[#5329] fix(exec): guard bare and named-user home paths** — Closed. Fixes workspace-boundary bypasses in `ExecTool`'s path extraction for shell tilde expansion (`~`, `~/...`, `~user`), including nested cases like input redirects and assignment values. Directly addresses a security escalation vector.
- **[#5258] fix(web): keep credential-bearing URLs away from the remote Jina reader** — Closed. Prevents userinfo and token-style query parameters from being forwarded to `r.jina.ai`; inspects the redirect chain before allowing the original URL to be forwarded. This closes the privacy gap flagged in issue #4884.
- **[#5230] fix(gemini): preserve imported tool calls with signature fallback** — Closed. Fixes Gemini 3 rejection of replayed function-call steps when conversations are transferred from providers lacking Gemini signatures, improving cross-provider conversation portability.
- **[#5218] fix(tools): treat redirection and grouping delimiters in ExecTool path guard** — Closed. Broadens path extraction to cover redirection/grouping operators without breaking quoted paths — a continuation of the `ExecTool` security hardening.
- **[#5279] fix(session): store session history outside the agent workspace** — Closed. Moves session transcripts from `<workspace>/sessions/` to `<config-dir>/sessions/<workspace-id>/`, closing the reachability issue whereby workspace-scoped tools could read session history.
- **[#4878] feat(hooks): add auto-discovery mechanism for agent hooks** — Closed. Introduces hook registration via `pkgutil` scanning + `entry_points`, mirroring the channels/tools plugin model — a **long-running feature PR** (opened 2026-07-10) finally merged.

## 4. Community Hot Topics

- **[Issue #5327] [bug] Nanobot repeats multiple times the same message while reasoning** (11 comments, Closed). The most-discussed issue this window. Users report the agent looping on phrases like *“Good points, let me investigate the issue”* intermittently. High community engagement suggests this is a genuinely aggravating user-facing defect.
- **[Issue #4010] Feature proposal: text-to-speech / voice output support** (3 👍, 3 comments, still open since May). Continues to accumulate support. The author notes Nanobot has voice-in but not voice-out; closing this loop is seen as low-surface-area work given existing channel-side plumbing.
- **[PR #5291] [bug, documentation, fix, test] persist subagent conversation transcripts** (Open). Discussion history shows interest in auditability and debugging of subagent runs; the PR addresses the fact that subagent tool calls/reasoning currently vanish after completion.
- **[Issue #5295] [bug] deploy with docker compose failed: `/usr/local/bin/entrypoint.sh: Permission denied`** (5 comments, Closed). A deployment blocker, now resolved. Notably, the fix proceeded indirectly through the capability-restoration PR (#5320).

## 5. Bugs & Stability

Ranked by severity (High → Low), with fix status:

- **[P0 – Race condition] #5271 (PR): prevent stale background task saves from overwriting session data** — Open fix. Serializes `/new` with per-session compaction and rejects saves from invalidated/copied sessions. Prevents data-loss class bugs after session lifecycle events. **No issue filed; PR directly addresses the root cause.**
- **[P1 – Security] #5329 (PR): `ExecTool` tilde-expansion path bypass** — **Merged.** Multiple variants (`~username`, bare `~`, input redirection) escaped workspace boundaries. Fix landed in this window.
- **[P1 – Security] #5258 (PR): credential-bearing URLs forwarded to Jina** — **Merged.** Resolves #4884 (userinfo leaks to third-party reader).
- **[P1 – Deployment] #5320 (PR): Docker entrypoint permission denied** — **Merged.** Resolves #5295 (Compose fails at startup due to missing capabilities after `cap_drop: ALL`).
- **[P2 – Deterministic test failure] #5348 (Issue, open): token-usage tests fail in ~5hr/day window** — Root-caused: `record_token_usage()` assumes UTC while the settings payload reads the configured timezone. New issue, no fix PR yet.
- **[P2 – Privacy] #4884 (Issue, closed): WebFetch sends user URLs to Jina** — Closed via merged PR #5258.
- **[P2 – Functional] #5360 (PR, open): MCP tool-name collisions for fully non-ASCII names** — `"获取天气"` collapses to `"_"` causing silent collisions. Simple sanitizer fix proposed, not yet merged.

Additional closed issues this window: #5295 (Docker permission), #4858 (refactor MCP lifecycle out of `AgentLoop` — merged), #5327 (message repetition — closed without linked fix PR; worth watching for regression reports).

## 6. Feature Requests & Roadmap Signals

- **[#5350] QwenCloud provider path (new, open)** — Proposal to add a backward-compatible QwenCloud provider alongside existing DashScope support, motivated by international Qwen users. If maintainers act quickly, this may land in the next minor release.
- **[#4010] Text-to-speech / voice output (open since May, 3 👍)** — Steadily gaining support. The author argues that voice-in already exists and voice-out closes the conversational loop with minimal new surface area. A plausible near-term roadmap candidate.
- **[#5358] WebUI session collaboration via mentions (new, open)** — Server-owned `@name` handles for sessions, composer picker integration, and stable identity colors. Suggests the project is investing in multi-session, collaborative UI patterns.
- **[#5342] Apps discovery redesign (open, conflict)** — Redesigns the Apps view into Discover/Installed/All plus curated Featured batches backed by the nanobot.wiki registry with offline fallback. Forward-looking; needs conflict resolution.
- **[#5362] DeepSeek V4 Pro Responses support (merged)** — Confirms the provider roadmap: DeepSeek V4 Pro now routed through the native Responses API alongside V4 Flash. Expect the merged provider routes to appear in the next release.
- **[#5204] Declarative `ResponsesCapabilities` profile (open)** — Refactors Responses provider-name checks into a declarative capability profile covering routing, reasoning replay, compaction, API override, and Chat-fallback. Architecture-level work likely aimed at a 1.x stability milestone.

## 7. User Feedback Summary

- **Deployment friction:** Users hitting Docker Compose entrypoint permission errors (#5295) point to continued friction in the “official” deployment path. The fix (#5320) is merged but released only in a future version.
- **Intermittent message repetition (#5327):** Described as random and “while reasoning” — the phrasing suggests users are seeing the agent’s streamed reasoning tokens repeated, not the final answer. Closed without an explicit fix PR; may warrant a follow-up verification.
- **Voice output demand (#4010):** Users see voice as a natural completion of the existing voice-in pipeline, not a novel feature. The 3 👍 over ~3 months suggests moderate but not overwhelming demand.
- **Security/Privacy sensitivity:** The Jina URL-leak issue (#4884) and `ExecTool` path-boundary bugs (#5329, #5218) were both filed by external contributors, indicating the community is actively auditing the codebase for security. The prompt merges suggest maintainers treat these seriously.
- **Matrix parity requests (#5275):** Users are pushing for behavior parity across Slack/Discord/Matrix around thread-context semantics — “reply in thread” should form a dedicated context regardless of channel.

## 8. Backlog Watch

Items needing maintainer attention (open, unanswered, or unresolved for an extended period):

- **[#5275] Matrix thread-context request (open, 6 days, 1 comment)** — A behavior-parity feature request; no maintainer response yet despite a related PR (#5292) being open.
- **[#5271] P0 session race-condition fix (PR, 7 days, open)** — High severity, already scoped with a test plan; absent merge, it remains a lurking data-loss risk.
- **[#4329] Native TypeScript terminal UI (PR, 61 days, open, conflict)** — A major UX rework that has been open for two months with conflicts; is this blocked on architecture decisions or bandwidth?
- **[#5348] Timezone-related test failures (new, no comments)** — Deterministic, easy to reproduce, provides a clear window for fix; must be addressed before a release to keep CI green.
- **[#5204] Declarative provider capability refactor (12 days, open)** — Architectural cleanup with p1 priority; blocking follow-up provider work (e.g., #5362 depended on similar patterns).
- **[#4858] MCP lifecycle refactor (Closed)** — Issue is closed, but the PR that resolved it was not visible in this digest; worth confirming the merged state so downstream bugs don’t resurface.
- **[#5338] MCP OAuth store credential preservation (2 days, open)** — It is a relatively niche storage-corruption fix, but the risk of overwriting another server’s credentials is a real correctness threat.

---

*Digest generated from GitHub public data on 2026-08-13. All links are to HKUDS/nanobot issues and PRs.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date: 2026-08-13**

---

## 1. Today's Overview

Hermes Agent is experiencing a period of **intense development activity**, with 50 issues and 50 PRs updated in the last 24 hours. The project shows a healthy balance between feature development and bug fixing, though the ratio of open to closed items (36:14 for issues, 48:2 for PRs) indicates a **growing review queue that may need maintainer attention**. The most significant trend is the **large-scale plugin interface expansion** (#64162–#64231, PRs #84916–#84924), driven by contributor teknium1 — with 14 related issues and PRs appearing to represent a coordinated, multi-phase effort. Desktop and gateway stability remain the most **critical pain points**, with multiple P1 regressions reported. Notably, the issue tracker shows **no new releases** this cycle, despite the surge in activity.

---

## 2. Releases

**No new releases** were published in the last 24 hours (latest remains v0.20.0).

---

## 3. Project Progress

**2 PRs were merged/closed** in the last 24 hours (down from the high volume of open PRs). No merge details were shown for this period.

However, **14 closed issues** indicate progress in the following areas:

- **Plugin architecture expansion (major push):** A coordinated set of 7+ issues by teknium1 were closed (all updated 2026-08-12):
  - [#64162](https://github.com/NousResearch/hermes-agent/issues/64162) — Pluggable approval transport + gated approval policy
  - [#64167](https://github.com/NousResearch/hermes-agent/issues/64167) — Cache-safe context injection (system prompt sections + environment hints)
  - [#64174](https://github.com/NousResearch/hermes-agent/issues/64174) — Plugin LLM calls routed through auxiliary model slots (closes #44673)
  - [#64177](https://github.com/NousResearch/hermes-agent/issues/64177) — Secret-source plugins bootstrap fix
  - [#64179](https://github.com/NousResearch/hermes-agent/issues/64179) — Plugin API versioning, stability contract, compat test suite
  - [#64180](https://github.com/NousResearch/hermes-agent/issues/64180) — Research spike: Pi + OpenCode plugin architecture lessons
  - [#64227](https://github.com/NousResearch/hermes-agent/issues/64227) — Config & state bridge (ctx.get_config/set_config/state/cron)
  - [#64230](https://github.com/NousResearch/hermes-agent/issues/64230) — Developer tooling: scaffold, Plugin Doctor, test harness

- **Windows data-loss bug fixed:** [#57775](https://github.com/NousResearch/hermes-agent/issues/57775) — atomic_replace() drops writes on ERROR_SHARING_VIOLATION (closed)

- **Other closures:** [#64900](https://github.com/NousResearch/hermes-agent/issues/64900) (plugin send_message schema), [#44673](https://github.com/NousResearch/hermes-agent/issues/44673) (auxiliary slots), [#62294](https://github.com/NousResearch/hermes-agent/issues/62294) (desktop keyring), [#84623](https://github.com/NousResearch/hermes-agent/issues/84623) & [#84823](https://github.com/NousResearch/hermes-agent/issues/84823) (desktop duplicates)

The **plugin expansion work continues** with 8 new PRs opened today (see Community Hot Topics).

---

## 4. Community Hot Topics

**Most active/discussed items this cycle:**

| Issue/PR | Comments | 👍 | Topic |
|----------|----------|-----|-------|
| [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) | **39** | **18** | Lazy Tool Schema Loading — Two-Pass Injection to reduce 3.5–5k token overhead |
| [#64231](https://github.com/NousResearch/hermes-agent/issues/64231) | 24 | 0 | Plugin lifecycle-event catalog & hook taxonomy |
| [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | 19 | 0 | Skills index stale/degraded (automated probe) |
| [#83683](https://github.com/NousResearch/hermes-agent/issues/83683) | 9 | 0 | **P1** Desktop restart kills gateway (WeChat/QQ silent) |
| [#78069](https://github.com/NousResearch/hermes-agent/issues/78069) | 9 | 0 | **P1** Clarify tool response binding failure (hangs turn) |

**Analysis of underlying needs:**

- **Token cost consciousness is the #1 community concern.** The most-upvoted issue (18👍) is #6839 — full tool schemas are injected for every call regardless of need. This indicates users are hitting **significant usage-cost ceilings on local models**, and the ecosystem needs smarter, demand-driven tool injection. This is a strong candidate for near-term implementation.

- **Plugin architecture is a major nexus of interest.** 24 comments on the lifecycle-event catalog issue (#64231) plus the vast cluster of related plugin issues/PRs show the community is heavily invested in making Hermes a **first-class plugin platform**. The push appears coordinated (possibly a team effort or campaign), with a trail of dependencies (tracker #64182).

- **Desktop app reliability is a recurring theme.** The P1 gateway-kill regression (#83683) plus duplicate reports about desktop behavior (#84823, #84824, #84870, #84921) suggest the desktop app is a **growing but fragile surface area**.

---

## 5. Bugs & Stability

**Critical (P1) — active:**

1. **[#83683 — P1, OPEN](https://github.com/NousResearch/hermes-agent/issues/83683)** — **Desktop restart reaps live gateway but never relaunches it** (WeChat/QQ/Telegram go silent). Regression since v0.20.0. **No fix PR exists yet.**

2. **[#84824 — P1, OPEN (duplicate of above)](https://github.com/NousResearch/hermes-agent/issues/84824)** — Desktop serve boot reaps healthy detached gateway (SIGKILL, no clean shutdown). **Duplicate — no fix PR.**

3. **[#78069 — P1, OPEN](https://github.com/NousResearch/hermes-agent/issues/78069)** — **Clarify tool free-text response intermittently fails to bind** to pending call, hanging the turn indefinitely. Child issue [#82975](https://github.com/NousResearch/hermes-agent/issues/82975) (Telegram, P2) adds a second failure mode (profile-namespaced session keys). **No fix PR visible.**

**Moderate (P2) — active:**

4. **[#84871 — P2, OPEN](https://github.com/NousResearch/hermes-agent/issues/84871)** — Discord triggering-message context **leaks into stored user messages and session titles** (pollutes transcripts/exports).

5. **[#84870 — P2, OPEN](https://github.com/NousResearch/hermes-agent/issues/84870)** — Session list shows stale lineage ROOT instead of live tip after `/new` / reset.

6. **[#25065 — P2, OPEN](https://github.com/NousResearch/hermes-agent/issues/25065)** — `HASS_TOKEN` env force-enables Home Assistant gateway, overriding `config.yaml`.

7. **[#71331 — P2, OPEN](https://github.com/NousResearch/hermes-agent/issues/71331)** — Termux install fails when Python is 3.14+ (requires-python conflict).

**Stability note:** Two of the three P1 bugs are desktop/gateway regressions on Windows — a pattern suggesting the v0.20.0 desktop release may have introduced substantive lifecycle issues. Monitoring the resolution timeline of these is important.

---

## 6. Feature Requests & Roadmap Signals

**Strong signals from this cycle (likely for next release):**

| Feature | Issue | Why it matters |
|---------|-------|----------------|
| **Lazy/split tool schema loading** | [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) | 18👍 (highest this cycle); directly addresses token cost for local models |
| **Plugin discovery & search** | PR [#84919](https://github.com/NousResearch/hermes-agent/pull/84919) | `hermes plugins search/install` — community index; already implemented in PR |
| **Plugin manifest v2** (versioning, deps, pip seam) | PR [#84916](https://github.com/NousResearch/hermes-agent/pull/84916) | Upgrades plugin ecosystem to mature standard |
| **Session librarian skill** (prompt-driven session mgmt) | PR [#84917](https://github.com/NousResearch/hermes-agent/pull/84917) | New bundled skill for session find/summarize/rename/archive |
| **Streaming output observer hooks** | PR [#84924](https://github.com/NousResearch/hermes-agent/pull/84924) | Plugin visibility into live token stream |
| **Multi-gateway tabs in Desktop** | [#45779](https://github.com/NousResearch/hermes-agent/issues/45779) | 7👍; recurring desktop feature ask |
| **Xiaomi MiMo-V2.5 TTS/ASR** | [#46257](https://github.com/NousResearch/hermes-agent/issues/46257) | Native Chinese-language speech models; niche but concrete |

**Prediction:** The plugin expansion suite (PRs #84916–84924) appears ready and is likely to merge in the next 1–2 cycles. The lazy tool-loading issue has the most community support and is a natural cost-saving win — likely to be picked up soon.

---

## 7. User Feedback Summary

**Pain points (real user experiences):**

- **Token overhead is a real, costly problem.** Users running local models report 3,500–5,000 tokens per call are consumed by *all* tool schemas regardless of need (#6839). This suggests the current tool-injection model is **prohibitively expensive for local/self-hosted users**.

- **Desktop app is a reliability weak spot.** Users report messaging gateways going dark (WeChat, QQ, Telegram) after simple app restarts (#83683). Another user reports the desktop app kills a healthy detached gateway (Scheduled Task) on open (#84824). The desktop experience is **frustrating for multi-platform power users**.

- **Transcripts and session titles are being polluted.** Discord users see internal control wrappers ("Triggering message id:...") prepended to their own message text in exports (#84871). This undermines trust in exported data.

- **Session-lineage issues degrade the organizer experience.** After `/new`, the session list shows the old title/timestamp, not the live tip (#84870). This breaks workflows for long-running conversations.

- **Configuration overrides are not respected.** `HASS_TOKEN` env var takes precedence over explicit `config.yaml` settings (#25065). Users expect config file supremacy.

**Positive signals:** The plugin API expansion is being driven *by* active community contributors (teknium1, poisdahl, Diaspar4u, and employees like yingliang-zhang), indicating **engagement and a healthy contributor pipeline**.

---

## 8. Backlog Watch

**Issues/PRs needing maintainer attention (long-waiting, no response):**

| Issue/PR | Wait | Why it matters |
|----------|------|----------------|
| [#38275 — HAMP proposal](https://github.com/NousResearch/hermes-agent/issues/38275) | ~2.5 months (Jun 3) | Agent address system + async messaging + cryptographic identity. Ambitious vision, zero reactions — may need explicit roadmap deferral |
| [#71331 — Termux install break](https://github.com/NousResearch/hermes-agent/issues/71331) | ~19 days | Simple `install.sh` check bug; blocks Android/Termux users on Python 3.14+ |
| [#25065 — HASS_TOKEN override](https://github.com/NousResearch/hermes-agent/issues/25065) | **~3 months** (May 13) | Behavioral inconsistency between env and config; 2 comments only — unresolved |
| [#45779 — Multi-gateway Desktop tabs](https://github.com/NousResearch/hermes-agent/issues/45779) | ~2 months | 7👍 — substantial community interest, no maintainer response visible |
| **Plugin cluster PRs** (#84916–#84924) | New today | 7+ PRs opened in one day by the same contributor — **needs triage + consolidated review** to avoid a review queue backlog |

**Notable:** The 36 open *active* issues + 48 open PRs suggest the maintainer team may be **approaching review saturation**. The plugin cluster (14+ items all touching `hermes plugins` APIs) is the highest-risk item for **merge conflict cascades** without immediate maintainer coordination.

---

*Digest generated from GitHub activity data for 2026-08-13.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest
**Date: 2026-08-13**

---

## 1. Today's Overview

PicoClaw shows steady, moderate activity with 2 open issues and 3 open pull requests updated in the last 24 hours. No new releases were published, and no PRs were merged or closed during this period, suggesting a maintenance-focused phase rather than an aggressive feature push. Both open issues have been flagged as stale but have received updates within the last day, indicating they remain on the maintainers' radar. The PR queue contains three substantial improvements spanning agent context management, Telegram topic handling, and a new web search provider integration. Overall, the project appears healthy with active community contributions and reasonable maintainer engagement, though the lack of recent merges and releases may be a slight concern for velocity.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent known versions are **0.3.1** (referenced in issue reports) and a nightly build (`2cf030d2`). Users are advised to check the [releases page](https://github.com/sipeed/picoclaw/releases) for upcoming stable releases.

---

## 3. Project Progress

No PRs were merged or closed in the last 24 hours. However, three PRs remain open and actively updated:

- **[PR #3316](https://github.com/sipeed/picoclaw/pull/3316): fix: routed-agent context management not respecting history, summarization, compression, and seahorse bootstrap** — Fixes a bug where routed agents (e.g., Discord channel routing) did not persist session history or trigger auto-compaction. This is a significant bug fix that could improve long-session usability for multi-channel deployments.

- **[PR #3315](https://github.com/sipeed/picoclaw/pull/3315): Support topics in private bot chats** — Corrects Telegram topic handling for private chats with forum topic mode enabled, expanding PicoClaw's Telegram integration coverage.

- **[PR #3299](https://github.com/sipeed/picoclaw/pull/3299): Add native Exa web search provider** — Introduces Exa as a native `tools.web` / `web_search` provider with support for existing date range filters, adding to the project's extensibility for research use cases.

While none of these have merged yet, their continued updates suggest active development and review.

---

## 4. Community Hot Topics

Two issues are generating the most community engagement, both with 4 comments and 1 👍 reaction each:

- **[Issue #3281](https://github.com/sipeed/picoclaw/issues/3281): Web UI chat input is very laggy when history has a little bit long** — Users are reporting degraded input performance in the Web UI as conversation history grows. This is a UX-critical issue that negatively impacts daily usage for chat-heavy workflows. The core need here is performance optimization for long-context sessions, which is increasingly important as users push PicoClaw into longer, more complex conversations.

- **[Issue #3269](https://github.com/sipeed/picoclaw/issues/3269): If the MCP server connection fails, the agent loop will hang, causing the chat interface to stop replying** — MCP (Model Context Protocol) server failures cause the agent loop to hang, effectively freezing the chat interface. This is a reliability issue that undermines trust in the system, particularly for users who rely on external MCP tools. The community is signaling that failure handling and recovery mechanisms are critical for production use.

Both issues highlight a broader theme: **PicoClaw needs to be more robust at scale and in real-world deployments**, whether that means handling longer sessions or gracefully managing external service failures.

---

## 5. Bugs & Stability

Two bugs were actively discussed in the last 24 hours. Ranked by severity:

| Severity | Issue | Description | Fix PR |
|----------|-------|-------------|--------|
| **High** | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | MCP server connection failure causes agent loop to hang, freezing the entire chat interface. This is a system-level reliability bug that can completely block user interaction. | **No dedicated fix PR yet** |
| **Medium** | [#3281](https://github.com/sipeed/picoclaw/issues/3281) | Web UI input becomes laggy with moderately long chat history, degrading the user experience over extended sessions. | **No dedicated fix PR yet** |

Notably, neither bug has a linked fix PR at this time. PR #3316 addresses a similar context-management issue for routed agents, which may partially mitigate aspects of #3281, but the core problems remain unaddressed. These should be prioritized given their direct impact on usability and reliability.

---

## 6. Feature Requests & Roadmap Signals

- **Exa web search provider** ([PR #3299](https://github.com/sipeed/picoclaw/pull/3299)): The addition of a native Exa provider signals growing demand for better web search integration. This could be merged in the next minor release, broadening PicoClaw's research capabilities.

- **Private bot chat topic support** ([PR #3315](https://github.com/sipeed/picoclaw/pull/3315)): Telegram topic support for private chats is a niche but valuable integration enhancement. Likely to be included in the next patch release.

- **Improved routed-agent context management** ([PR #3316](https://github.com/sipeed/picoclaw/pull/3316)): This fix addresses memory management for routed agents, suggesting the maintainers are focused on making PicoClaw more viable for multi-channel, long-lived sessions.

**Prediction for next version:** The next release will likely include the Exa provider and Telegram topic fixes, along with the routed-agent context fix. Given current activity, a patch release (0.3.2 or 0.4.0) within the next 1-2 weeks is plausible.

---

## 7. User Feedback Summary

- **Web UI performance:** Users are comfortable with PicoClaw's Web UI for short sessions but experience noticeable lag with extended histories. This is a common pain point for chat-based AI assistants and directly affects user satisfaction for long-form work.

- **MCP reliability:** The MCP hang issue reflects a broader concern about external tool dependencies. Users want graceful degradation when third-party services fail, not complete system freezes. This suggests that resilience and error handling are top-of-mind for the community.

- **Multi-channel routing:** PR #3316 highlights that users are actively deploying PicoClaw across Discord channels and expecting full feature parity (memory, summarization, compression) regardless of the channel. This indicates real-world use cases that push the project beyond basic single-channel chat.

- **Positive signals:** Community members are actively submitting quality PRs and detailed bug reports with environment info, indicating a engaged and collaborative user/developer base.

---

## 8. Backlog Watch

The following items may need maintainer attention:

- **[Issue #3281](https://github.com/sipeed/picoclaw/issues/3281) and [Issue #3269](https://github.com/sipeed/picoclaw/issues/3269)**: Both are marked `[stale]` and have been open for over three weeks. The lag issue affects core UX and the MCP hang is a severe reliability bug. Neither has a linked fix PR, and these are the **most critical backlog items** — they should be prioritized or explicitly addressed.

- **[PR #3299](https://github.com/sipeed/picoclaw/pull/3299) (Exa provider)**: Open since July 26 without comments or review activity visible. This is a substantial feature contribution from the community that appears to be waiting for maintainer review. If approved, it would add real value to the project.

- **[PR #3315](https://github.com/sipeed/picoclaw/pull/3315) and [PR #3316](https://github.com/sipeed/picoclaw/pull/3316)**: Open since August 3, updated most recently on August 12. These appear to be under active review, but no merge has occurred yet. Maintainers should aim to close these out soon to keep PR momentum healthy.

**Overall health assessment:** PicoClaw remains a viable and actively developed project with a growing community, but the open bug backlog and unreviewed PRs suggest the maintainer team may be under-resourced. Clearing the critical bugs and reviewing the pending PRs would significantly improve project velocity and community trust.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-13

## Today's Overview

NanoClaw is in an active development cycle, with **4 open issues** and **10 pull requests** updated in the last 24 hours. The spotlight is on a **major architectural shift**: PR #3220, which converts agent templates into versioned "Agent Plugins 1.0.0" directories, is the most consequential change in flight, promising to improve security hardening and the overall plugin architecture. Six pull requests, including core-team features and community fixes, received updates, signaling strong ongoing collaboration. While there are **no new releases**, the volume of activity—particularly around the agent template plugin migration and its dependent setup wizard flow—shows this is a period of foundation-building rather than feature shipping. The community is also active in surfacing bugs identified in the recent 2.1.54 release, with two new issues already filed on migration and agent-group identification quirks.

## Releases

No new releases were published in the last 24 hours.

## Project Progress

While no PRs were **merged** in the last 24 hours (PR #3086 was closed but not merged), the most significant progress is on the **Agent Plugin 1.0.0 architecture** pushed by the core team. PR #3220 by `amit-shafnir` has seen recent activity and is the foundation for a two-part feature:

- **[PR #3220 — Agent Templates become Agent Plugins 1.0.0 directories](https://github.com/nanocoai/nanoclaw/PR/3220)**: This engine change is a bug-fix and a feature, introducing a format migration for templates with a focus on security hardening (stamp-time symlink/caps/secret hardening).
- **[PR #2909 — Setup wizard template flow and first-agent stamping](https://github.com/nanocoai/nanoclaw/PR/2909)**, explicitly stacked on #3220, is the second half. It adds a template flow to the setup wizard (14 setup-side files, +927/−52 lines).

These two PRs form a unified effort to fundamentally change how agents are instantiated from templates, moving from a simple mechanism to a more robust plugin architecture. Several other community-driven fixes are active but not merged:

- **[PR #3231 — Honor plugin MCP cwd in codex/opencode config writers](https://github.com/nanocoai/nanoclaw/PR/3231)** (core-team): Adds working-directory support to plugin MCP configurations, a new capability that will land on trunk with #3220.
- **[PR #3230 — Fix removal docs pointing at the retired data/env mirror](https://github.com/nanocoai/nanoclaw/PR/3230)**: A documentation fix correcting stale references.
- **[PR #3189 — add-why skill](https://github.com/nanocoai/nanoclaw/PR/3189)**: A new utility skill to explain what happened to a single message.

## Community Hot Topics

The most active discussions center on the **agent template plugin migration** and **integration fixes** that have been pending for a long time.

1.  **[Issue #2504 — `ncl status` command for lightweight operational health check](https://github.com/nanocoai/nanoclaw/Issue/2504)** (created 2026-05-15, 1 comment): Despite being three months old, this is the only issue with a comment today. It highlights a user need for a quick operational health signal for running instances, suggesting the existing `ncl sessions list` lacks health metadata and the `/add-dashboard` skill requires external dependencies. This is a recurring ask for better observability.

2.  **[PR #3220 — Agent Plugins 1.0.0 migration](https://github.com/nanocoai/nanoclaw/PR/3220)**: While it doesn't have many comments, its status as a core-team, breaking-change PR that is the base for other work (#2909, #3231) makes it the de-facto focal point. Its evolution is closely watched by contributors.

3.  **[PR #2689 — Signal DM fixes](https://github.com/nanocoai/nanoclaw/PR/2689)**: Updated today, this long-running PR (since June 4) addresses critical Silent Signal delivery issues (`isMention` flag, `signal:` prefix), fixing silent message drops. Its continued activity suggests maintainers are iterating on it, but its longevity also points to complexity.

4.  **[PR #2346 — Unknown slash commands as normal chat](https://github.com/nanocoai/nanoclaw/PR/2346)**: Also updated, this PR fixes a bug where unknown slash commands were mistakenly interpreted as Claude Code commands, causing responses to be dropped. Its long lifecycle (since May 8) indicates a challenging edge-case fix.

## Bugs & Stability

Three distinct stability issues surfaced today, ranging from a likely regression to a feature gap. No fix PRs are open for any of them yet.

- **[Issue #3233 (High) — Agent-scoped tasks blind to pre-2.1.54 recurring tasks](https://github.com/nanocoai/nanoclaw/Issue/3233)**: This is a **regression risk**. After migrating to v2.1.54, `ncl tasks list` inside agent containers returns "No tasks" and all task management commands fail, despite tasks firing on schedule. The root cause is identified as a missing migration for legacy task rows. This is a severe functional break for existing users upgrading, as it breaks agent self-management. It has been open for a day with no response.

- **[Issue #3234 (High) — Bare UUID for template-stamped agent groups](https://github.com/nanocoai/nanoclaw/Issue/3234)**: Creating an agent group from a template assigns a bare `randomUUID()` instead of the prefixed `ag-<uuid>`. This causes the OneCLI `ensureAgent` to reject the identifier at spawn, leading to failed agent launches. This is a clear bug in the template-creation path and will affect all users who use templates to create groups.

- **[PR #3086 (Medium) — WhatsApp silent failure on invalid recipient](https://github.com/nanocoai/nanoclaw/PR/3086)** (closed): Not a bug report, but a fix for one. The problem identified is that Baileys `sendMessage` returns a success key even for unregistered numbers, leading to "silent" message delivery failures with no user-facing error. The PR to validate recipients before sending was closed, which could indicate the fix is being reworked or was superseded.

## Feature Requests & Roadmap Signals

The roadmap is heavily influenced by the current architectural overhaul.

- **Agent Plugin Architecture (Nearsest Probability)**: The stacked PRs #3220, #2909, and #3231 signal that the next release (likely 3.0) will center around the Agent Plugin 1.0.0 format. Expect breaking changes for any custom agent template usage.

- **[Issue #3232 — QwenCloud provider skill](https://github.com/nanocoai/nanoclaw/Issue/3232)**: A user suggests adding a `/add-qwencloud` modular provider skill for Qwen models, following the established pattern of provider skills. Given the project's stated preference for keeping providers modular, this has a strong chance of being accepted, possibly in the next minor release.

- **Observability (Long-term)**: Issue #2504 requesting an `ncl status` command is a continuing signal for improved operational tooling. While not directly in flight, the need for health checks may be addressed in the future as the platform matures.

## User Feedback Summary

User activity reflects a mix of satisfaction with the project's direction and frustration with recent regressions.

- **Pain Point — Migration Breaks**: The #3233 issue is a significant pain point. An existing user reports that upgrading to 2.1.54 breaks core agent functionality (recurring task management). This causes immediate disruption to workflows and necessitates a migration fix.
- **Pain Point — Template Reliability**: Issue #3234 shows that the new template feature has an edge case that crashes agent group creation. This undermines trust in a newer feature.
- **Positive Signal — Contribution Quality**: The continued submission and refinement of guidelines-compliant PRs (like #3230, #3189, #3193) and the community's detailed bug reports with clear root-cause analysis demonstrate a healthy and engaged contributor base.

## Backlog Watch

The following items have been open for a concerning length of time and require maintainer attention to close out or communicate a path forward.

- **[PR #2346 — Treat unknown slash commands as normal chat](https://github.com/nanocoai/nanoclaw/PR/2346)** (Open since 2026-05-08): This fix addresses a "silent failure" bug where responses are dropped. It has been open for over three months, suggesting either a complex review or a paused decision on the best approach.

- **[PR #2689 — Signal DM platform fixes](https://github.com/nanocoai/nanoclaw/PR/2689)** (Open since 2026-06-04): More than two months without a merge for critical fixes to DM message dropping is a risk. Frequent updates indicate work is being done, but the timeline is long and the bug it fixes is severe for any Signal users.

- **[Issue #2504 — `ncl status` command request](https://github.com/nanocoai/nanoclaw/Issue/2504)** (Open since 2026-05-15): Three months old with only one comment, this feature request has not received an official response or roadmap acknowledgment from maintainers.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-13

## 1. Today's Overview

IronClaw is in a period of intense stabilization and feature expansion. Release candidates for v1.2.0 are shipping (rc.2 and rc.3) with critical runtime fixes, while a large QA bug-bash surfaced 19 new issues (many Telegram-specific) that are now driving rapid-fire fixes. The project shows strong momentum on two fronts: the ongoing "Reborn" architecture migration (context-window fixes, durable-storage refactors, and design-system work) and a push to expand core messaging capabilities across channels (Slack, Telegram). Notable activity includes 41 issues and 50 PRs updated in the last 24 hours, indicating a highly active development cadence. The open issue count (29 active) and the volume of P1/P2 QA bugs suggest the project is prioritizing stability for an upcoming stable release. Overall, the project appears healthy with rapid iteration, but the sheer volume of channel-specific bugs (especially Telegram) indicates the QA process is properly stress-testing real-world scenarios.

## 2. Releases

Two release candidates were published yesterday:

- **ironclaw-v1.2.0-rc.3** (1.2.0-rc.3) — **Fixed:** The runtime container image now installs `curl`, so in-container HTTP healthchecks can execute. Hosted orchestrators probe the worker with `curl -fsS http://localhost:3000/`; the image previously shipped no HTTP client, so the probe could never run and the container was never marked healthy. This is a critical fix for hosted deployments.
- **ironclaw-v1.2.0-rc.2** (1.2.0-rc.2) — **Fixed:** Windows first-start filesystem publication now uses native atomic rename semantics instead of hard links, and tolerates unsupported directory syncs. Release smoke runs also preserve the Windows account identity required to secure the standalone secrets key.

**Migration notes:** No breaking changes or migration notes provided. The container `curl` fix is important for anyone running hosted orchestrator healthchecks.

## 3. Project Progress

### Merged/Closed PRs (19 total)

**Stability & Release:**
- **PR #7560** [CLOSED] — `fix(release): retry the dist installer download` — Fixes flaky CI where the `x86_64-unknown-linux-musl` release leg failed 18 seconds in due to a network error downloading cargo-dist; adds retry logic.
- **PR #7427** [CLOSED] — `release: prepare 1.1.1-rc.1` — Backports urgent IronHub/custom MCP, WebUI, retrieval, runtime-credential, Slack, and Telegram fixes onto the 1.1 release line. Defaults the retained rc1 Slack/Telegram migration to skip legacy channel state safely; documents durable storage changes.

**Runtime & Container:**
- **PR #7555** [CLOSED] — `fix(docker): install curl so orchestrator healthchecks can run` — Forward-port of #7303 from `release/1.1.0-rc.1`. Fixes the runtime stage which ships no HTTP client (only `ca-certificates`, `postgresql-client`, `sqlite3` on `debian:bookworm-slim`), preventing healthcheck probes from succeeding.

**WebUI/Extensions:**
- **PR #7550** [CLOSED] — `feat(extensions): per-field help text on admin configuration forms + channel setup docs rewrite` — Manifest `[admin_configuration]` fields gain an optional `description` rendered as a hint under each input on the WebUI Admin → Configuration form. The Telegram manifest is the first consumer.

**Features:**
- **PR #5503** [CLOSED] — `[Experiment] Add compact Google extension capabilities` — Adds context-efficient capabilities (Gmail `fetch_message_summaries` for inbox triage, Google Calendar equivalents) without a new Google Workspace tool/package.
- **PR #6836** [CLOSED] — `feat(webui): @ironclaw/ui and workspace refactor` — Re-derives the WebUI design system as a workspace package `@ironclaw/ui` in reviewable layers; supersedes earlier PRs #5563/#6830.

**Issue Resolutions (12 closed):**
- **#7484** — `fix(loop): context window silently evicts the task` — fixed by pinning user messages, compacting on eviction, and revisiting the 128-message clamp.
- **#7485** — `fix(loop): token estimator double-counts ASCII` — unified the two inconsistent token estimators; the transcript one double-counted ASCII (2 chars/token instead of ~4).
- **#7407** — `Execute BatchPolicy::Parallel capability batches concurrently` — agent loop now actually runs parallel batches concurrently (bounded) with zero model-facing change.
- **#5508** — `[QA] Slack delivery target not found despite active Slack connection` — resolved; likely related to the Slack/Telegram migration skip default in #7427.
- **#6541** — `WebUI constantly reconnecting` — resolved.
- **#7383** — `chore(loop-host): track decomposition of tool_disclosure_port.rs` (4.4k lines) — tracking issue closed, likely after a decomposition PR landed.
- **#7302** — `[webui] Improve tool call UI when one of the calls failed` — resolved.

## 4. Community Hot Topics

The most active threads (by comment count, 3 comments each) reveal core infrastructure concerns:

1. **#7360** [OPEN] — *"Expand stress coverage across built-in and durable write paths"* (3 comments) — [Link](https://github.com/nearai/ironclaw/issues/7360). The nightly API-capacity workload exercises conversation persistence and concurrent reads, but the mock model never returns tool calls, so regressions in built-in capability writes land undetected. **Underlying need:** The stress harness must cover the full capability surface, including durable writes, to prevent silent regressions.

2. **#7407** [CLOSED] — *"Execute BatchPolicy::Parallel capability batches concurrently"* (3 comments) — [Link](https://github.com/nearai/ironclaw/issues/7407). The production capability port executes all batches sequentially despite the agent loop computing a parallel batch policy for multi-tool-call turns. **Underlying need:** Performance parity between what the loop plans and what the runtime executes; closed with the fix.

3. **#7554** [OPEN] — *"Custom MCP server add flow shows validation error"* (1 comment, from Slack) — [Link](https://github.com/nearai/ironclaw/issues/7554). **Underlying need:** Users expect a clear, actionable validation path when adding a custom MCP server; the current error is unhelpful ("red validation" with no guidance).

4. **#7517** [OPEN] — *"Cloud.near.ai: allow staking path for Google/GitHub sign-ins"* (1 comment) — [Link](https://github.com/nearai/ironclaw/issues/7517). **Underlying need:** Users with Google/GitHub sign-ins cannot stake for inference; the "Sign in with NEAR" option is only a login alternative, not an attachable wallet.

## 5. Bugs & Stability

A major QA bug-bash (19 new issues in the last 24h, many from the Railway testing instance) surfaced a cluster of Telegram-channel bugs. Ranked by severity:

### P1 (Critical — agent becomes unusable):

- **#7538** [OPEN] — *"Telegram agent becomes completely stuck after receiving GIF or sticker"* — [Link](https://github.com/nearai/ironclaw/issues/7538). After a GIF/sticker is sent, the session is entirely unresponsive; even text messages get no reply. **No fix PR yet.**
- **#7535** [OPEN] — *"Telegram webhook is not activated after saving bot configuration"* — [Link](https://github.com/nearai/ironclaw/issues/7535). Bot only works after a full redeploy; "Forbidden" errors and CrabStick traces during activation. **No fix PR yet.**
- **#7536** [OPEN] — *"Multi-user access flow is broken — additional users get 'Invalid secret' error"* — [Link](https://github.com/nearai/ironclaw/issues/7536). Users created from Admin UI receive an email/token but cannot open the UI. **No fix PR yet.**

### P2 (High — broken functionality):

- **#7541** — *"Agent cannot send generated files back as Telegram attachments"* — provides a local workspace path instead of a real attachment. [Link](https://github.com/nearai/ironclaw/issues/7541)
- **#7539** — *"Telegram user message appears after agent starts working — conversation flow looks out of order."* [Link](https://github.com/nearai/ironclaw/issues/7539)
- **#7540** — *"Long Telegram messages are split and partially missed"* — only first part processed; rest rejected with "still working on a previous message." [Link](https://github.com/nearai/ironclaw/issues/7540)
- **#7542** — *"Agent does not recognize that conversation is already in Telegram"* — offers to deliver to Telegram when already there. [Link](https://github.com/nearai/ironclaw/issues/7542)
- **#7543** — *"Telegram routine runs successfully but message is not delivered on first execution."* [Link](https://github.com/nearai/ironclaw/issues/7543)
- **#7544** — *"Agent exposes internal reasoning/planning instead of responding to user."* [Link](https://github.com/nearai/ironclaw/issues/7544)
- **#7545** — *"Agent incorrectly claims live crypto market data is unavailable"* despite having general HTTP capabilities. [Link](https://github.com/nearai/ironclaw/issues/7545)
- **#7451** — *"Telegram agent sometimes incorrectly asks for credentials"* — asks for API key even when not needed. [Link](https://github.com/nearai/ironclaw/issues/7451)
- **#7508** — *"GitHub MCP extension startup gives confusing endpoint verification prompt."* [Link](https://github.com/nearai/ironclaw/issues/7508)

### P3 / Other:

- **#7546** — *"Agent does not react to or acknowledge Telegram stickers."* [Link](https://github.com/nearai/ironclaw/issues/7546)
- **#7547** [v1-launch-checklist] — *"Instance upgrade fails during egress apply on agent staging"* — container image switches successfully but egress apply fails. [Link](https://github.com/nearai/ironclaw/issues/7547)
- **#7554** — *"Custom MCP server add flow shows validation error."* [Link](https://github.com/nearai/ironclaw/issues/7554)

**Positive signal:** The active PRs #7464 (Telegram linked-device auth) and #7515 (Slack core ops) may address several of these channel bugs. The container `curl` fix (#7555) and healthcheck issue are already released in rc.3.

## 6. Feature Requests & Roadmap Signals

Several features in flight strongly indicate v1.2/v1.3 scope:

- **Telegram linked-device authentication** (PR #7464, [link](https://github.com/nearai/ironclaw/pull/7464)) — real MTProto linked-device support with session custody and standard-op tools. This is likely to fix several of the P2 Telegram bugs and is a notable roadmap item for secure channel usage.
- **Generic per-request thinking/effort control** (#7537, [link](https://github.com/nearai/ironclaw/issues/7537)) — provider-native mapping (incl. DeepSeek `chat_template_kwargs`) for thinking/effort control. Triggered by DeepSeek V4 Flash checkout getting verbose; signals intent to support model-specific reasoning controls.
- **Structured execution contracts for automations** (PR #7548, [link](https://github.com/nearai/ironclaw/pull/7548)) — versioned contracts with goal, success criteria, output instructions, allowed capabilities, required skills. This formalizes the automation create flow.
- **Operator surface for IronHub agent link** (PR #7516, [link](https://github.com/nearai/ironclaw/pull/7516)) — brings IronHub registration to the WebUI Extensions page, ending CLI-only setup.
- **OOBE automation-tasks prototype** (PR #6994, [link](https://github.com/nearai/ironclaw/pull/6994)) — first-run onboarding carousel, inline cards, agent-mode pill; gated behind `oobe_suggestions` flag.
- **Railway sandbox workspace file bridge** (PR #7556, [link](https://github.com/nearai/ironclaw/pull/7556)) — `builtin.sandbox_workspace_copy` for copying files between runtime and Railway sandbox workspaces.
- **Design System (Storybook)** — Phase 1 (PR #7039) integrates Storybook; Phase 2 (PR #7043) adds DESIGN.md governance; Phase 3 scaffold for `@ironclaw/ui` (PR #7558). **Prediction:** The multi-user access fix (#7536) and Telegram attachment delivery (#7541) are near-term must-fixes likely targeted for v1.2.0 stable. The staking-path enhancement (#7517) is a likely v1.4.0 candidate.

## 7. User Feedback Summary

Recent Slack-sourced feedback (via issues) reveals consistent themes:

- **Configuration friction:** The custom MCP server flow (#7554) gives an unhelpful validation error; the Telegram webhook doesn't activate until a full redeploy (#7535). Users expect configuration changes to take effect immediately.
- **Channel awareness:** The agent frequently forgets it's already in Telegram (#7542) and offers to deliver there; it also exposes internal reasoning (#7544) instead of clean user-facing responses. These erode trust in the agent's understanding of context.
- **File delivery:** Users expect generated files to be sent as native Telegram attachments (#7541), not as workspace paths. This suggests a gap between the agent's file model and channel-native formats.
- **Onboarding:** The "channel-first approach" epic (#7044) was raised because "the WebUI opens to a blank slate" and users "don't know what to do with it." The OOBE work directly addresses this adoption friction.
- **Staking for non-NEAR logins (#7517):** Users with Google/GitHub sign-ins want a staking path without creating a separate NEAR wallet login.

## 8. Backlog Watch

- **#7538 (P1) — Telegram sticky on GIF/sticker** — [Link](https://github.com/nearai/ironclaw/issues/7538). No fix PR open; agent becomes fully unresponsive. Needs immediate maintainer attention.
- **#7535 (P1) — Telegram webhook not activating on save** — [Link](https://github.com/nearai/ironclaw/issues/7535). Requires full redeploy. High-impact for operators.
- **#7536 (P1) — Multi-user access "Invalid secret"** — [Link](https://github.com/nearai/ironclaw/issues/7536). Breaks a core multi-tenant workflow. No fix in flight.
- **#7537 (feature) — Generic thinking/effort control** — [Link](https://github.com/nearai/ironclaw/issues/7537). Opened 2026-08-12; no PR yet; will likely land in v1.3.0.
- **#7517 (enhancement) — Staking path for Google/GitHub sign-ins** — [Link](https://github.com/nearai/ironclaw/issues/7517). No PR. Low urgency but clear product gap.
- **#6993 — Backend wiring for OOBE automation-tasks** — [Link](https://github.com/nearai/ironclaw/issues/6993). Part of epic #7044; backend portion not yet started publicly. The frontend prototype (PR #6994) is open and large; coordination may be needed.
- **#7383 — tool_disclosure_port.rs decomposition (4.4k lines)** — Closed, but worth watching whether the file was actually decomposed or just tracked.
- **#7044 (epic) — Onboarding to channel-first approach** — [Link](https://github.com/nearai/ironclaw/issues/7044). Long-running epic; the OOBE PR (#6994) is still open and huge (XL size) — monitor for merge progress.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest
**Digest Date: 2026-08-13 | Data Window: Last 24 Hours**

---

## 1. Today's Overview

LobsterAI is in a **high-velocity release cycle**, with 8 PRs updated in the last 24 hours, 7 of which were merged or closed—indicating strong forward momentum. The project shipped its **2026.8.12 patch release** (PR #2480), bundling several fix-focused changes that address cross-platform compatibility issues (Windows file junctions, macOS icon handling). The issue tracker is notably quiet today, with **zero new issues filed**; however, all 6 updated issues carry the "stale" label, suggesting these are older threads receiving automated pings rather than fresh user engagement. In short: **strong code delivery cadence, but the community issue queue has gone quiet**, with several older user complaints left unanswered for months.

---

## 2. Releases

**No new releases** were published in the last 24 hours. However, the merged release branch **`Release/2026.8.12` ([PR #2480](https://github.com/netease-youdao/LobsterAI/pull/2480))** indicates a version bump to **2026.8.12** is in the pipeline. This hotfix release bundles at least three fixes (Windows plugin installation, macOS icon extraction, and model thinking-level persistence), and users should expect it to reach public channels shortly.

---

## 3. Project Progress

Today's merged PRs show a **multi-area sprint** across the renderer and main process layers:

- **[PR #2482](https://github.com/netease-youdao/LobsterAI/pull/2482)** — `feat: skills manager split mine builtin tabs`: Separates user-defined skills from built-in ones in the Skills Manager UI, improving navigation clarity.
- **[PR #2481](https://github.com/netease-youdao/LobsterAI/pull/2481)** — `feat(sidebar): move task search to header actions`: Replaces the labeled search entry with an icon-only action, with cross-platform (macOS/Windows) layout alignment and added regression coverage.
- **[PR #2479](https://github.com/netease-youdao/LobsterAI/pull/2479)** — `fix(plugins): preserve junctions during Windows install`: Fixes `EPERM` symlink failures on Windows by staging plugin installs on the same volume and atomically renaming into place—a meaningful stability win for Windows users.
- **[PR #2478](https://github.com/netease-youdao/LobsterAI/pull/2478)** — `fix(shell): avoid unsupported large file icon size on macOS/Windows`: Resolves an Electron API incompatibility where `'large'` icon size is unsupported on macOS.
- **[PR #2475](https://github.com/netease-youdao/LobsterAI/pull/2475)** — `fix(model-selector): give each model its own thinking level`: Fixes a bug where thinking-depth settings were global (setting model B would reset model A), now per-model state is persisted.

---

## 4. Community Hot Topics

The most active threads today are all **stale issues with limited recent comment activity**, but they reveal recurring user friction points:

- **[Issue #1179](https://github.com/netease-youdao/LobsterAI/issues/1179)** — "3.31版本强制沙箱怎么关？" (How to disable forced sandbox in 3.31?) — 2 comments. The user reports being unable to disable the sandbox as of version 3.31 and rolled back to 3.30. **This appears unresolved for ~5 months** and remains an open pain point around platform restrictions.

- **[Issue #1236](https://github.com/netease-youdao/LobsterAI/issues/1236)** — "插件 ID 不匹配警告" (Plugin ID mismatch warning) — 2 comments. A reproducible bug where the mcp-bridge plugin's entry key conflicts with the manifest ID, producing a persistent startup warning. Closed, but no linked fix PR was identified.

- **[Issue #2071](https://github.com/netease-youdao/LobsterAI/issues/2071)** — "创建定时任务错误" (Error creating scheduled task) — 2 comments. A bug report with screenshot attached for version 2026.5.27. **Might be related to the open PR #1181 that hides the OpenClaw main agent from the session list**, as that PR explicitly mentions internal heartbeat/cron routing.

- **[Issue #1173](https://github.com/netease-youdao/LobsterAI/issues/1173)** — "卸载之后程序还能运行？？" (Program still runs after uninstall?!) — 1 comment. User expresses serious concern (accusing the project of leaving a "backdoor") that the app keeps running and sending messages after Windows uninstall. This is a **trust-critical issue** that appears to be a process/daemon cleanup bug, but the emotional tone suggests the user may have already churned.

---

## 5. Bugs & Stability

Ranked by severity:

| Severity | Issue/PR | Description |
|----------|----------|-------------|
| **High** | [Issue #1173](https://github.com/netease-youdao/LobsterAI/issues/1173) | Post-uninstall process persistence: app continues running and sending messages after removal from Windows. **No fix PR identified.** This is the most severe issue — it erodes user trust and may indicate a missing uninstaller cleanup step (e.g., background daemon not terminated). |
| **Medium** | [Issue #1179](https://github.com/netease-youdao/LobsterAI/issues/1179) | Forced sandbox in v3.31 cannot be disabled; users are rolling back to 3.30. **No fix PR identified.** |
| **Medium** | [Issue #1180](https://github.com/netease-youdao/LobsterAI/issues/1180) | Modifying a self-built agent triggers repeated gateway restarts (v2026.3.31). **No fix PR identified.** |
| **Low** | [Issue #1236](https://github.com/netease-youdao/LobsterAI/issues/1236) | Startup config warning for plugin ID mismatch (mcp-bridge). Cosmetic but persistent. **No fix PR identified.** |
| **Fixed** | [PR #2479](https://github.com/netease-youdao/LobsterAI/pull/2479) | Windows plugin install `EPERM` symlink failures — resolved via atomic staging/rename. |
| **Fixed** | [PR #2478](https://github.com/netease-youdao/LobsterAI/pull/2478) | macOS app icon extraction crash/failure — resolved via platform-specific icon size selection. |

---

## 6. Feature Requests & Roadmap Signals

Two feature signals emerged from the stale queue:

- **[Issue #1174](https://github.com/netease-youdao/LobsterAI/issues/1174)** — "增加多个自定义模型提供商" (Support multiple custom model providers): A user requests the ability to maintain several custom model providers simultaneously, rather than replacing one with another. Given the project's **active model-selector work** (PR #2475 today), expanding provider configuration is a plausible near-term roadmap candidate.

- **[PR #1233](https://github.com/netease-youdao/LobsterAI/pull/1233)** — "为模型提供商添加官网链接和 API Key 获取引导" (Add official website link and API key guidance for model providers): This closed-but-merged PR adds clickable provider website links and "Get API Key" shortcuts plus i18n support. **Guidance suggests the team is doubling down on the model-provider experience**, which may pair well with the multiple-provider feature request above.

---

## 7. User Feedback Summary

- **Windows install/uninstall experience is a recurring sore spot**: Two separate issues (uninstall persistence [\#1173], forced sandbox [\#1179]) suggest platform-level restrictions annoy Windows users. The uninstall complaint also hints at **a trust deficit**—the user framing it as a possible "backdoor" is a red flag for churn.
- **Configuration friction**: The plugin ID mismatch warning [\#1236] appears in every startup log, and while cosmetic, it adds noise to a config-driven tool.
- **Gateway stability on agent edits** [\#1180]: Users expect self-service agent customization; hitting a restart loop is disruptive and blocks a core workflow.
- **Satisfaction signal**: The team's *fast iteration pace* on renderer UX (search placement, skills tab split, per-model thinking levels) implies active feature-driven development, which usually tracks positively with user adoption.

---

## 8. Backlog Watch

These items need maintainer attention and have received **no recent activity**:

1. **[Issue #1173](https://github.com/netease-youdao/LobsterAI/issues/1173)** (2026-03-31) — Uninstall persistence. **Urgent**: warrants an immediate binary check on the uninstaller to rule out actual daemon leaks, followed by a public explanation. Silent staleness could amplify user distrust.

2. **[Issue #1179](https://github.com/netease-youdao/LobsterAI/issues/1179)** (2026-03-31) — Forced sandbox blocking common use cases. Users are rolling back versions, which means **retention loss**; an official document or setting to disable sandbox (or explain the trade-off) would likely resolve this.

3. **[Issue #1180](https://github.com/netease-youdao/LobsterAI/issues/1180)** (2026-03-31) — Gateway restart loop on agent edit. This is a **crash-adjacent bug** in a core feature (agent customization) and has lingered for 4+ months.

4. **[PR #1181](https://github.com/netease-youdao/LobsterAI/pull/1181)** (2026-04-01) — Hide OpenClaw main agent sessions from the list; **still open after 4 months**. This is a UX clarity fix that may also unblock Issue #2071 (scheduled task errors). Why it hasn't been merged despite the small diff is unclear and worth a maintainer look.

---

**Bottom line**: LobsterAI is executing well on the engineering side (7 merged PRs in one day, including meaningful cross-platform fixes), but the **staleness of core bug reports (average ~4 months) and the uninstaller trust issue put the project's long-term retention at risk** if deliberately triaged. The model-provider feature cluster (multiple providers, API key guidance, thinking-level persistence) looks like the emerging product focus for the next iteration.

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

# CoPaw Project Digest — 2026-08-13

## 1. Today's Overview

CoPaw (QwenPaw) is in an active beta cycle, with the release of **v2.1.0-beta.4** alongside a high volume of bug reports and fixes — 29 issues and 42 PRs updated in the past 24 hours. The project shows a vibrant community, but also reveals significant stability concerns, particularly around Windows crashes (3+ reports), network resilience, and multi-agent orchestration reliability. The merge of 15 PRs (including critical fixes for memory guidance, channel configurators, and macOS Computer Use) indicates a maintainer team responding quickly to bug reports while pushing forward on feature development (TTS, DataPaw runtime). The density of Chinese-language issue reports (approximately 50%) reflects a strong user base in that region. Overall, the project is in a healthy but somewhat chaotic "crunch" phase leading into the v2.1.0 stable release, with releases coming roughly every 24 hours.

---

## 2. Releases

### v2.1.0-beta.4 (new)

**Release page:** https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.1.0-beta.4

**Changes:**
- **fix(files):** repair previews and dark mode styling (PR #6915)
- **fix(tools):** correct `read_file` tool description to improve agent comprehension (PR #6898)
- **chore:** version bump to 2.1.0b4

**Breaking Changes:** None indicated in release notes.

**Migration Notes:** Minimal — this is an incremental beta fix release; no config schema changes or data migrations announced.

---

## 3. Project Progress

**Merged/Closed PRs (15 total):**

**Stability Fixes:**
- **#6540** — fix(agents): sanitize tool messages before model calls (fixes orphaned tool results hitting providers) — merged by RerankerGuo
- **#6913** — fix(computer-use): improve macOS element activation (fixes transient menus and composite accessibility element handling) — merged by jinglinpeng
- **#6816** — fix(chats): handle dict-like model responses (fixes `KeyError: '__aiter__'` in auto-title generation, issue #6813) — merged by RerankerGuo

**Feature Work:**
- **#6937** — fix(creator): compose-gate scene auto-rereview, DAG production hardening, vendor runtime bootstrap, fail-closed plugin packaging (multi-part hardening for Creator pipeline) — merged by xuanrui-L

**Infrastructure/Docs:**
- **#6944** — chore: update release notes for v2.1.0 — closed by cuiyuebing

---

## 4. Community Hot Topics

**Highest Activity Issues:**

1. **#6853 — "prompts.py lies to agents: Dream writes to digest/ not MEMORY.md"** (5 comments)
   https://github.com/agentscope-ai/QwenPaw/issues/6853
   *Need:* A developer tracing the ReMe memory pipeline found a *documentation/implementation mismatch* — agents are told dream syncs to MEMORY.md, but it was never implemented. This drives a deeper need for **accurate memory system docs** and either implementing the claimed behavior or correcting the prompt.
   *Follow-up:* PR #6942 (fix(memory)) closes this issue by simplifying memory prompts.

2. **#6921 — "[Bug]: 经常在...输出后无提示就停止了，需要我说'继续'才会继续任务"** (5 comments)
   https://github.com/agentscope-ai/QwenPaw/issues/6921
   *Need:* Agents will stop mid-task after planning the next steps without any visual indication, requiring users to say "继续" (continue). **This is a major UX pain point** — the agent appears to be hitting some silent stop condition (possibly max steps, context cutoff, or output token limit) without surfacing an actionable message.

3. **#6928 — "历史消息+输入栏bug"** (4 comments)
   https://github.com/agentscope-ai/QwenPaw/issues/6928
   *Need:* History cannot scroll up for previous days' conversations; input field has a selection/editing bug that deletes trailing text. **This points to basic editor and transcript navigation issues** in the 2.1.0b3 web UI.

4. **#6839 — "MCP工具调用时，总是将像数字的字符串以数字格式传参"** (4 comments)
   https://github.com/agentscope-ai/QwenPaw/issues/6839
   *Need:* Models emit numeric-typed values for `type: string` tool args, causing validation failures with MCP tools. **Models need stricter type coercion or schema validation is too strict.** (Open PR #6936 addresses this.)

5. **#6780 — "2.0.1版，不使用时几十分钟后自己回卡死"** (4 comments)
   https://github.com/agentscope-ai/QwenPaw/issues/6780
   *Need:* System freezes after being idle for tens of minutes, requiring process kill/restart. **This is a notable reliability issue for the desktop app experience.**

**Most Active PR:**
- **#6940 — "feat(pawapp): add native DataPaw app runtime and durable analysis workspace"** (by cyruszhang, first-time contributor)
   https://github.com/agentscope-ai/QwenPaw/pull/6940
   *Signal:* A substantial new feature — treating DaaS-style data analysis as a "native app" (DataPaw) within QwenPaw, with its own infra repo. **This suggests a roadmap direction toward specialized app runtimes within the agent platform.**

---

## 5. Bugs & Stability

**Ranked by severity:**

**High: Windows Crashes and Freezes**
- **#6955** — Probabilistic startup errors and crashes on Windows 11 (v2.0.1, pip) — new 2026-08-12
  https://github.com/agentscope-ai/QwenPaw/issues/6955
  *No fix PR yet.*
- **#6919 (CLOSED)** — Frequent crashes with `console process/reply failed` traceback on Windows — closed 2026-08-12
  https://github.com/agentscope-ai/QwenPaw/issues/6919
- **#6780** — Idle freeze after ~30 minutes on Windows — still open, 4 comments
  https://github.com/agentscope-ai/QwenPaw/issues/6780

**High: Network Resilience**
- **#6932** — Network interruptions kill LLM connectivity; requires full process restart to recover (reproduced twice in one day) — 2026-08-12
  https://github.com/agentscope-ai/QwenPaw/issues/6932
  *This is a critical production reliability issue.* No fix PR yet.

**Medium: Agent Execution Reliability**
- **#6921** — Silent agent stoppage mid-task requiring user nudge ("继续") — 2.1beta2
  https://github.com/agentscope-ai/QwenPaw/issues/6921
- **#6927** — Multi-sub-agent tasks repeatedly enter infinite loops — 2.1beta3
  https://github.com/agentscope-ai/QwenPaw/issues/6927
- **#6918** — Inter-agent messages create a new agent session per message (shadow instances, duplicate data)
  https://github.com/agentscope-ai/QwenPaw/issues/6918

**Medium: Data Integrity**
- **#6926 (CLOSED)** — `sync.py` imports history under random AgentState UUID instead of real session_id → 18–50% rows orphaned, recall split/duplicated
  https://github.com/agentscope-ai/QwenPaw/issues/6926

**Low/Medium: Scroll Compression UI Bug**
- **#6951** — After `/compact` and re-entering a session, pre-compression history is invisible; UI only shows eviction index
  https://github.com/agentscope-ai/QwenPaw/issues/6951
  *Fix PR #6947 addresses the underlying deepseek message-pairing error, but maybe not the visibility issue.*

**Low: Time Display & Timezone**
- **#6826** — Chat history shows erroneous completion time for assistant messages (fix PR #6938 open)
  https://github.com/agentscope-ai/QwenPaw/issues/6826
- **#6948** — Console chat logs show UTC, ignoring `user_timezone` config
  https://github.com/agentscope-ai/QwenPaw/issues/6948

**Other notable:**
- **#6852 (CLOSED)** — Front-end renderer collapses long multi-line tool outputs into unreadable blob
  https://github.com/agentscope-ai/QwenPaw/issues/6852
- **#6872 (CLOSED)** — Legacy sessions with local-path media fail to load indefinitely
  https://github.com/agentscope-ai/QwenPaw/issues/6872

---

## 6. Feature Requests & Roadmap Signals

**Strongest signals for upcoming/potential versions:**

1. **Plugin channel configurators revert** — #6924 (question) and PR **#6943** ("feat(channels): support interactive configurators for plugin channels") — *likely in v2.1.0 stable.*
   https://github.com/agentscope-ai/QwenPaw/pull/6943

2. **Native apps ecosystem** — PR **#6940** introduces "DataPaw app runtime" with a durable analysis workspace, suggesting a first step toward an ecosystem of specialized agent apps.
   https://github.com/agentscope-ai/QwenPaw/pull/6940

3. **MiniMax TTS support** — PR **#6954** adds MiniMax text-to-speech to the SIP channel via HTTP, expanding channel media capabilities.
   https://github.com/agentscope-ai/QwenPaw/pull/6954

4. **Collapsed multi-agent sessions** — #6925 requests all agent-collaboration dialogs appear in one session window instead of spawning new sessions per message.
   https://github.com/agentscope-ai/QwenPaw/issues/6925

5. **Inbox delivery for agent messages** — #6917 requests a "fixed, non-scrolling" mechanism for agents to deliver structured reports to users, rather than rolling away in chat history.
   https://github.com/agentscope-ai/QwenPaw/issues/6917

6. **Context-aware file/CAS folders** — #6929 requests the ability to use folders as a conversation basis (like Codex/cursor) and drag file content into dialogs.

**Performance engineering:**
- **#6952 / PR #6953** — Prefix cache instability from unsorted tool schemas and interleaved `env_context` fields; fix sorts tool descriptors by name and splits env_context. **This is a meaningful cost/performance optimization for repeated turns.**

---

## 7. User Feedback Summary

**Common Pain Points:**

- **Silent task stall:** Multiple users report agents appear to "stop" mid-task without visible feedback and require manual "继续" nudges (#6921 in beta2; #6927 reports infinite loops in beta3). This is a top annoyance.
- **Windows instability:** Crash/freeze reports persist across 2.0.1 → 2.1.0b2 (#6919, #6955, #6780); these are severe enough to require full process restarts.
- **Transcript/history fidelity:** Users want to scroll back through complete histories, including post-compression (#6951, #6928); the current scroll system hides too much from the user.

**Feature Appreciation:**
- The Files workspace and memory features are being actively documented in user-facing blogs (PRs #6950, #6949), indicating the team's focus on making these complex features approachable.

**Community sentiment:** Users are actively testing beta versions and reporting issues with detailed logs (e.g., #6952, #6926 are extremely well-documented). This suggests a technically sophisticated user base engaging constructively with the alpha/beta process. The absence of "wishlist" churn shows that the current core value proposition (agent orchestration, memory, multi-modal tools) is landing well.

---

## 8. Backlog Watch

**Long-open PRs needing maintainer attention:**

1. **PR #5992 — "Add per-session model overrides"** (open since 2026-07-12, 5+ weeks, first-time contributor, Under Review)
   https://github.com/agentscope-ai/QwenPaw/pull/5992
   *Opt-in per-session model overrides for different LLMs across conversations. Broad community utility — worth scheduling for review.*

2. **PR #5869 — "expose system commands in slash autocomplete across all UIs"** (open since 2026-07-08, Under Review)
   https://github.com/agentscope-ai/QwenPaw/pull/5869
   *A UX polish that could simplify discovery of power features (`/plan`, `/dream`, etc.) — helps new users.*

3. **PR #6623 — "prevent final text loss when notifications race the prompt response"** (open since 2026-08-01, Under Review)
   https://github.com/agentscope-ai/QwenPaw/pull/6623
   *Addresses a tricky ACP race condition.* Continues to receive updates.

**Long-open issues that may be under-considered:**

- **#6780** (idle freeze, Windows) — 6 days old, still open. This is a top-3 UX blocker for Windows desktop users; the ideal time to get a fix before 2.1 stable.
- **#6839** (MCP string coercion) — Open PR #6936 addresses it; awaiting merge.
- **#6847** (antivirus/EDR kills QwenPaw) — 4 comments, open; no acknowledged fix likely if the root cause is behavioral (rapid file ops or unsigned binaries). Would be valuable to explicitly document recommended antivirus exclusions.

---

**Overall project health:** High-velocity, responsive maintainers (daily beta patches), active community, but stressed by Windows stability issues and memory/transcript-fidelity gaps. The influx of thoughtful feature requests suggests healthy experimentation in the user base. Watch that release cadence doesn't sacrifice regression management — the density of 2.0.x/2.1 beta bugs (esp. Windows-specific) warrants a "stabilization sprint" before 2.1 stable.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest
**Date:** 2026-08-13

---

## 1. Today's Overview

ZeroClaw is maintaining a **high level of activity**, with 50 issues and 50 PRs updated in the last 24 hours, indicating a healthy and busy development cycle. The project shows a strong balance between **bug fixes** (15 of the 50 issues are bug-labeled), **feature work** (24 enhancement-labeled), and **CI/infrastructure improvements** (CI/security-related items making up a notable chunk of both issue and PR traffic). The merge rate is solid: **14 of 50 PRs were merged or closed** in the last day, including several significant fixes (e.g., #9182 PowerShell support, #9720 response cache enforcement). Notably, the biggest pain point *continues* to be **cross-platform (Windows/macOS) test coverage and reliability**, with multiple open issues (#7462, #7461, #7910, #9398) and a tracked CI matrix expansion in progress. No new releases were published today, but the merging of several key fixes positions the project for a strong patch release soon.

---

## 2. Releases

**No new releases were published in the last 24 hours.** The latest available release remains **v0.8.3**.

---

## 3. Project Progress

The following PRs were **merged or closed** in the last 24 hours. The most impactful ones include:

| PR | Title | Summary | Impact |
|----|-------|---------|--------|
| [#9182](https://github.com/zeroclaw-labs/zeroclaw/pull/9182) | feat(runtime): support PowerShell as the native shell on Windows | Routes `powershell`/`pwsh` through `-NoProfile -NonInteractive -Command` on Windows, preserving `cmd.exe /C` as default. | **Significant:** Adds first-class Windows shell support, directly addressing a key cross-platform gap. |
| [#9720](https://github.com/zeroclaw-labs/zeroclaw/pull/9720) | fix(runtime): enforce response cache request boundaries | Applies modifying/cancelling hooks to an ephemeral final request before observers/providers see it; restricts local caching to deterministic requests. | **Critical fix:** Closes a possible correctness/security boundary issue in the response cache, flagged as `priority:p1` and `size:XL`. |
| [#8902](https://github.com/zeroclaw-labs/zeroclaw/pull/8902) | fix(runtime): route bidirectional JSON-RPC responses | Routes responses to the daemon's pending outbound caller, fixing ZeroCode ask-user and poll interactions. | **Bug fix:** Unblocks a key interactive workflow in ZeroCode. |
| [#9877](https://github.com/zeroclaw-labs/zeroclaw/pull/9877) | fix(cli): make cron scheduling help examples runnable | Corrects help text examples for `add-at`, `add-every`, and `once` commands. | **Docs/UX fix:** Closes issue #9796; makes CLI help actually usable. |
| [#9692](https://github.com/zeroclaw-labs/zeroclaw/pull/9692) | feat(zerocode): show live run-status icons on the SOP pane list | Adds status icons (🟢/🟡/🔵/🔴) driven by `sops/runs` polling. | **Feature:** Improves ZeroCode SOP visibility and closes task #9684. |
| [#9701](https://github.com/zeroclaw-labs/zeroclaw/pull/9701) | feat(gateway): keep chat WebSockets alive | Adds configurable `websocket_ping_interval_secs` to prevent idle disconnects. | **Feature:** Improves Web UI chat reliability. |
| [#9778](https://github.com/zeroclaw-labs/zeroclaw/pull/9778) | docs(foundations): reconcile revision histories | Backfills and corrects revision metadata across FND-001..FND-006. | **Docs:** Ensures foundation specifications are consistent. |

**Summary of merged work:** The most significant merged items focus on **Windows support** (#9182), **runtime correctness/security** (#9720), and **ZeroCode user experience** (#9692). Several `size:XL` PRs landed, showing the project is able to handle large, complex changes.

---

## 4. Community Hot Topics

These are the most actively discussed items (by comment count) in the last 24 hours, revealing areas of key community interest:

1. **[#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) — 74 test failures on Windows** (14 comments)
   - **Issue:** The test suite has 74 failures on Windows (11, Chinese locale, code page 936), highlighting Unix-only commands, path-handling, and console codec issues.
   - **Underlying Need:** The community *strongly* wants Windows to be a first-class platform. This is the single most-commented issue and is directly connected to the request to add Windows/macOS CI ([#7461](https://github.com/zeroclaw-labs/zeroclaw/issues/7461)).

2. **[#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) — Maintainer decision queue for RFCs and design issues** (13 comments)
   - **Issue:** A tracker for pending maintainer decisions on RFCs, design issues, and release policy questions.
   - **Underlying Need:** Community members are signaling a backlog of design questions that need a clear decision path. This is a project-health signal about maintainer bandwidth.

3. **[#8832](https://github.com/zeroclaw-labs/zeroclaw/issues/8832) — Plugin-owned Kanban board for agent work** (9 comments)
   - **Issue:** An RFC proposing an opt-in Kanban board as a plugin-owned domain for coordinating agent work.
   - **Underlying Need:** Users are exploring ways to manage and visualize multi-agent work directly inside the platform, extending ZeroClaw beyond a chat interface.

4. **[#9101](https://github.com/zeroclaw-labs/zeroclaw/issues/9101) — Consolidate release attestation mechanisms** (9 comments)
   - **Issue:** v0.8.3 shipped with three parallel signing mechanisms, creating redundancy and CI cost.
   - **Underlying Need:** Maintainers and contributors are pushing for simpler, cleaner supply-chain security practices—a sign of maturity.

5. **[#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) — Complete SearXNG configuration and web-search failure recovery** (6 comments)
   - **Issue:** Wants SearXNG support and better CAPTCHA/recovery handling for DuckDuckGo.
   - **Underlying Need:** Reliability of web search tools for autonomous agents remains a top concern for privacy-focused users.

---

## 5. Bugs & Stability

**Critical Issues (Severity S1 — workflow blocked):**

1. **[#9207](https://github.com/zeroclaw-labs/zeroclaw/issues/9207) — `web_fetch` returns garbage for compressed responses (gzip, brotli, deflate)** (`priority:p1`, `status:in-progress`)
   - **Impact:** The tool is completely unusable on sites that use standard compression, breaking many agent workflows.
   - **Fix:** Currently in progress; active work is underway (status:in-progress).

2. **[#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) — macOS desktop app can reopen blank or without a window** (`priority:p1`, `status:needs-repro`)
   - **Impact:** Blocks macOS users from using the app after restart.
   - **Status:** Blocked on a reproduction; needs more user/system details. This is an older issue [created 2026-06-12] and needs more attention to diagnose.

3. **[#9290](https://github.com/zeroclaw-labs/zeroclaw/issues/9290) — Windows desktop installer fails with missing TaskDialogIndirect** (`priority:p1`, `status:accepted`)
   - **Impact:** Blocks installation on Windows.
   - **Status:** Bug is accepted; no fix PR references it yet.

**Major Issues (Severity S2/S3 — degraded/minor):**

- **[#9198](https://github.com/zeroclaw-labs/zeroclaw/issues/9198) — Discord typing indicator stuck** (`S3`, `priority:p2`): After a daemon reload, the "typing" indicator stays on forever. Accepted, no fix PR yet.
- **[#9202](https://github.com/zeroclaw-labs/zeroclaw/issues/9202) — `zeroclaw desktop` uses a dead URL and doesn't detect installed AppImage** (`S3`, `priority:p2`): A UX issue; accepted, in-progress.
- **[#9796](https://github.com/zeroclaw-labs/zeroclaw/issues/9796) — Cron help prints invalid examples** (`S2`): **✅ Fixed** by PR #9877 (merged today).
- **[#9340](https://github.com/zeroclaw-labs/zeroclaw/issues/9340) — CLI-created cron jobs cannot deliver output** (`priority:p1`): **Closed today**, and the fix ([#9877](https://github.com/zeroclaw-labs/zeroclaw/pull/9877) corrects the related help text). The hardcoded `None` delivery issue was addressed separately.

**Cross-Platform Stability Themes:** The Windows test suite is failing significantly ([#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)), and CI only runs Linux today. While no new Windows-infra bugs were *reported today*, the 74 test failures serve as a "meta-bug" and a barrier to stability. Efforts are underway ([#7461](https://github.com/zeroclaw-labs/zeroclaw/issues/7461), [#7910](https://github.com/zeroclaw-labs/zeroclaw/issues/7910), and PR [#9398](https://github.com/zeroclaw-labs/zeroclaw/pull/9398) are open, with #9398 currently blocked) to bring Windows into CI.

---

## 6. Feature Requests & Roadmap Signals

**Hotly Requested Features (based on community activity):**

1. **True cross-platform CI** ([#7461](https://github.com/zeroclaw-labs/zeroclaw/issues/7461)): Run tests on Windows/macOS, not just Linux. This is the umbrella issue to fix #7462 and is likely to be included in the next upcoming release.

2. **Windows PowerShell support** ([#9182](https://github.com/zeroclaw-labs/zeroclaw/pull/9182), already merged): Will likely land in an imminent patch release and will be a major win for Windows users.

3. **Observability and agent reporting** — PR [#8337](https://github.com/zeroclaw-labs/zeroclaw/pull/8337) adds **herdr agent reporting integration** for CLI; it is a large, open PR waiting for review. This indicates that better agent state management will be a near-term roadmap item.

4. **ZeroCode contributor workflows** — RFC [#8078](https://github.com/zeroclaw-labs/zeroclaw/issues/8078) proposes a *local pre-submission gate* for contributors, enforcing CI standards locally before opening a PR. This suggests a focus on improving the contributor experience, which often precedes dev-tooling improvements.

5. **Self-service agent coordination** — The RFC for a **plugin-owned Kanban board** ([#8832](https://github.com/zeroclaw-labs/zeroclaw/issues/8832)) signals a demand for higher-level agent workflow management tools, but this is further out on the roadmap.

---

## 7. User Feedback Summary

**Pain Points:**

- **Windows platform is a second-class citizen:** The most visceral pain point is the 74 test failures on Windows ([#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)). Many pipeline and tooling components use Unix-only conventions, which becomes a huge road block for Windows-native developers.
- **Tooling reliability for autonomus agents:** The `web_fetch` compression bug ([#9207](https://github.com/zeroclaw-labs/zeroclaw/issues/9207)) and the slow progress on web search reliability ([#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316)) frustrate users trying to run autonomous workflows.
- **Desktop App difficulties:** Users are hitting installation/relaunch issues on both macOS ([#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527)) and Windows ([#9290](https://github.com/zeroclaw-labs/zeroclaw/issues/9290)), which harms the first-run experience and adoption.

**Unmet & Emerging Needs:**

- Users are increasingly interested in complex agent orchestration (e.g., Kanban boards [#8832](https://github.com/zeroclaw-labs/zeroclaw/issues/8832), execution-tree budgets [#9323](https://github.com/zeroclaw-labs/zeroclaw/issues/9323)), indicating a shift from single-agent loops to multi-agent/concurrent workflows.
- **Security and trust** remain at the forefront for users, with several open security-focused trackers (e.g., #9899 on removing an unmaintained advisory waiver, #9101 on consolidating attestations).

**Satisfaction Drivers:**

- A very active pull-request merge rate and the visibility of a "Maintainer decision queue" (#8692) suggests the community feels issues are being acknowledged and tackled, which is a positive health signal.

---

## 8. Backlog Watch

The following items have been open for a while and require maintainer attention:

1. **[#6653](https://github.com/zeroclaw-labs/zeroclaw/issues/6653) — Define host-architecture policy for emulated installs** (opened 2026-05-14)
   - **Status:** `needs-author-action` for 3 months. The user (Audacity88) needs to provide more context or propose a solution for a still-relevant edge case.

2. **[#5907](https://github.com/zeroclaw-labs/zeroclaw/issues/5907) — Opt-in LSP support for ZeroCode coding workflows** (opened 2026-04-19)
   - **Status:** `needs-author-action` for ~4 months. This is a high-impact feature request (LSP integration to improve code generation quality) that remains stalled while waiting for a contributor to take the lead on the RFC.

3. **[#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) — macOS desktop app blank window bug** (opened 2026-06-12)
   - **Status:** `needs-author-action` on a `priority:p1` issue for 2 months. The author needs to provide a repro or additional system information, but maintainers should consider whether the tooling to gather that info should be more proactive.

4. **[#7929](https://github.com/zeroclaw-labs/zeroclaw/issues/7929) — Unify slash-command registries across web UI, TUI, and runtime** (opened 2026-06-18)
   - **Status:** `needs-author-action` to refine scope.

5. **PR Waiting for Review: [#8713](https://github.com/zeroclaw-labs/zeroclaw/pull/8713) — add `allowed_private_hosts` opt-in to `file_download` SSRF gate** (opened 2026-07-04)
   - **Status:** `needs-author-action` on a `risk:high, size:XL` fix. This SSRF fix is security-relevant and large; it would benefit from a maintainer helping to unblock it to avoid merge conflicts and long drift from `master`.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*