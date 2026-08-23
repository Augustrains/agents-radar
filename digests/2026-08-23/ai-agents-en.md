# OpenClaw Ecosystem Digest 2026-08-23

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-23 00:32 UTC

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

Based on the GitHub data provided for OpenClaw (github.com/openclaw/openclaw) on 2026-08-23, here is the project digest:

---

### 1. Today's Overview

OpenClaw is exhibiting a **high level of maintenance activity** with 500 issues and 500 PRs updated in the last 24 hours. However, the project is currently in a **critical stability phase**, with two P0 (critical) regressions reported against the latest beta (v2026.8.1-beta.2): one involving **SQLite database corruption** and another causing **severe event-loop blocking** that renders gateways unresponsive. While there are no new releases today, the maintainer team (including the automated `clawsweeper` bot) is actively pushing fixes, with several security and session-state critical PRs moving forward. The backlog is heavily populated with long-standing issues (many from March-April 2026) concerning session management, message loss, and authentication reliability, indicating that **core reliability remains the community's primary concern**, while the influx of new PRs suggests an active feature development phase (e.g., session trajectory view, UI improvements).

### 2. Releases

- **No new releases were published today.** The most recent version remains v2026.8.1-beta.2, which is the subject of several critical bug reports (#124788, #126821).

---

### 3. Project Progress

While most activity was focused on triage, some significant PRs were merged or closed without being merged today, indicating a refinement of the development pipeline:

- **Merged PRs**: A fix for the Control UI was merged to keep **Claude CLI OAuth available** (#125471), addressing a regression where valid credentials could lose refresh ownership after a restart.
- **Closed (Unmerged) PRs**:
    - **#126424**: A large, multi-channel PR to keep conversation delivery within agent bindings was closed. It had `proof: sufficient` and a `P1` rating, but its closure (without merge) on the same day suggests a need for rework or a strategic pivot.
    - **#120900**: A feature to review install policy warnings was closed. It had a `🦪 platinum hermit` rating, suggesting a possible absorption into the more mature, merged sequence of PRs #116489 and #120900.

The most notable merged feature series involved **`feat(security)`: requiring acknowledgement for install policy warnings** (#116489), which strengthens the security model by forcing explicit user consent for risky plugin/skill installations.

---

### 4. Community Hot Topics

The most active discussions highlight persistent user frustration with **core reliability and state management**, not feature requests.

- **Release Validation Thread (#125626)** - **19 comments**: The official process for validating v2026.8.1-beta.2 is active, with testers coordinating on `maintainer`-tagged issues. This is a healthy sign of governance but also indicates a lengthy pre-release period.
- **Configurable Streaming Watchdog Timeout (#68596)** - **15 comments, 8 👍**: Users running reasoning-heavy models (e.g., DeepSeek-R1) are being incorrectly flagged by a 30-second streaming watchdog. The high reaction count shows this is a real blocker for advanced use cases.
- **WhatsApp Image Wedging (#96834)** - **14 comments**: A detailed bug report on how a multimodal image can wedge the main lane for ~3 minutes, a prime example of the "session-state" and "message-loss" issues the community is facing.
- **MCP tools not injected into subagents (#85030)** - **12 comments, 6 👍**: A significant functional gap where MCP tools fail to be passed to sub-agent sessions, severely limiting multi-agent capabilities. This is a top `P1` complaint.
- **Hardcoded Working Path (#51429)** - **12 comments**: The Chinese-language bug report accuses the team of merging a hardcoded path (`/Users/wangtao`) into production. This is a serious trust issue and a source of community embarrassment, even if the report is from an older version.

---

### 5. Bugs & Stability

The project is facing a **stability crisis** with the latest beta (v2026.8.1-beta.2), marked by two new P0s (priority-zero) bugs.

**Critical (P0)**:
- **#126821 - SQLite Corruption Recurs on Pristine Rebuilt DBs**: A regression causing `SQLite` corruption within 15-24 hours under normal operation, potentially leading to a "paralyzed gateway" mode. This is the most severe data-integrity issue and has a `🦞 diamond lobster` rating.
- **#124788 - Event Loop Blocks ~100s Every ~10 min**: A severe performance regression causing the event loop to block (likely due to synchronous I/O), killing WebSockets and API responses. This directly interrupts all services.

**High Priority (P1)**:
- **#124284 - Subagent Spawn Fails with vLLM + Thinking**: A critical compatibility break in the new `2026.8.1-beta.2` stream wrapper that breaks tool calls for vLLM users, making agents unusable in that environment.
- **#112196 - `memory_search` Misreports Provider Failure**: Transient sync timeouts are being masked as persistent provider failures, making the memory system appear broken when it is not.
- **#85030 - MCP Tools Not Injected into Subagents**: (Also a hot topic) This limits the core value proposition of the system and needs a definitive fix.

**Stability & Regression Watch**:
- **#97616 - Zombie Process Leak**: Unreaped child processes are causing slow runtime degradation.
- **#89278 - Codex OAuth Refresh Timeout**: A regression where `cron`/`heartbeat` jobs fail due to an auth timeout.
- **#108215 - Context Usage Drops Without Compaction**: A confusing bug where content seemingly vanishes without a compaction event, risking data loss in conversations.

Many of these critical issues (e.g., #124788, #124284, #126821, #112196) are tagged with `clawsweeper-recovery-stuck`, meaning the automated bot is unable to fix them, signifying they are complex issues requiring deep maintainer intervention.

---

### 6. Feature Requests & Roadmap Signals

Despite the stability firefighting, Feature Requests continue to reveal the roadmap:

- **Plugin API for Slash Commands (#78798)**: (4 comments, 2 👍) A high-demand request to allow plugins to intercept user input via custom slash commands and pass-through to the LLM. This is a powerful extensibility ask that could appear in a future minor release.
- **Graceful Gateway Restart with Session Recovery (#57425)**: (5 comments) Users want in-flight work preserved across restarts. This aligns with the community's focus on session-state integrity.
- **`session-memory` hook on reset/prune (#51572)**: Users want more granular control over memory sampling, not just on compaction but also on resets.
- **Configurable TUI `--deliver` Default (#33102)**: A small UX quality-of-life improvement request.
- **README on Feature Progress**: PRs like the **Session Trajectory View (#128053)** and **UI Quality Update (#75947)** are being worked on, but are stalled in the "needs proof" or "waiting on author" states.

---

### 7. User Feedback Summary

Expressed User Pain Points:

1.  **Stability & Data Integrity**: Users are concerned about silent data loss, whether from context drops (#108215), session wedging (#96834), or actual database corruption (#126821).
2.  **Multi-Agent Reliability**: The inability of subagents to use configured tools (MCP) (#85030), lost completion messages (#67777, #78055), and orphaned sessions (#48810) are major blockers for complex workflows.
3.  **Provider Compatibility**: Users are experiencing failures with non-mainstream providers or specific configurations (vLLM + Thinking #124284, Ollama Cloud Sign-in #124689), highlighting a need for better edge-case handling.
4.  **Transparent Errors**: Users are frustrated by silent failures or misleading warnings (e.g., the streaming watchdog #68596, the auth lock vs. SQLite error masking #128049).
5.  **Trust & Governance**: The hardcoded path bug (#51429) has created a sense of distrust regarding code review and testing rigor.

---

### 8. Backlog Watch

Several long-standing `P1` issues from March and April remain unresolved and are flagged as `clawsweeper:needs-maintainer-review`, indicating they are complex, widely impactful, and have been stuck for months:

- **#44502 - Discord Routing/Mention Gating Issue** (March 13): A regression that affects Discord message routing, with high potential for incorrect behavior. Has a `🐚 platinum hermit` rating and requires live repro.
- **#45224 - Unhandled Playwright Assertion Crashes Gateway** (March 13): A crash bug with a clear stack trace that has remained triaged for months, though tagged with `clawsweeper:fix-shape-clear` today, suggesting a fix might be approaching.
- **#67777 - Subagent Completion Delivery Can Be Lost** (April 16): A `P1` reliability issue concerning message loss that is acknowledged but still unanswered at the code level.
- **#68187 - SSE-backed MCP Sessions Can Stay Stale** (April 17): A long-standing integration reliability issue.
- **#78805 - Severe Event Loop Blocking (Synchronous I/O)** (May 7): A `P1` regression that may be the root cause of performance issues seen in beta (#124788) and is still open on `main`. Fix PRs exist (#128064) but are not yet merged.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Ecosystem
**Date:** 2026-08-23

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is in a period of **intense architectural maturation**, characterized by a shared struggle to balance feature velocity with core reliability. Across the ecosystem, projects are converging on similar pain points—session state integrity, multi-agent tool propagation, provider compatibility, and resilience to upstream service failures—suggesting the community has moved beyond "demo-ware" into production-hardening territory. While the largest projects (OpenClaw, Hermes Agent, ZeroClaw) command significant issue volume and community engagement, a long tail of smaller, specialized agents (Moltis, CoPaw, PicoClaw) are carving out niches in policy enforcement, regional UX, and lightweight deployment. The dominant theme this cycle is **stability firefighting**: critical bugs (SQLite corruption, data loss, event-loop blocking) are consuming maintainer bandwidth across multiple projects, while feature roadmaps increasingly emphasize observability, context compression, and cost control—signals that real-world usage is exposing economic and operational realities.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Releases (24h) | Health Score | Notes |
|---------|---------------------|--------------------|----------------|--------------|-------|
| **OpenClaw** | 500 | 500 | None | ⚠️ **Critical** | 2 P0 regressions (SQLite corruption, event-loop blocking); active fix pipeline |
| **Hermes Agent** | 50 | 50 | None | 🟡 **Stable but stressed** | 46 open issues vs 4 closed; large PR backlog; fleet update is #1 concern |
| **ZeroClaw** | 50 | 50 | None | 🟢 **Dynamic/mature** | 3 PRs merged; heavy RFC activity; 47 PRs open (review backlog) |
| **NanoBot** | 0 | 21 | None | 🟢 **Healthy** | 7 PRs merged/closed; provider refactor stack; WebUI polish |
| **NanoClaw** | 1 | 25 | None | 🟢 **Healthy** | 8 PRs merged/closed; Slack/Telegram reliability focus |
| **IronClaw** | 10 | 22 | None | 🟢 **Healthy** | 5 PRs merged (all community); 4-track CI expedite; cost regression concern |
| **PicoClaw** | 2 | 6 | None | 🟡 **Moderate** | 4 PRs merged/closed; MCP hang critical; Telegram edit-loop bug |
| **CoPaw** | 7 | 4 | None | 🟡 **Moderate** | No PRs merged; Chinese-language community; UI refinement phase |
| **LobsterAI** | 2 | 6 | None | 🟡 **Low-moderate** | Mostly stale auto-closures; 1 open critical PR |
| **Moltis** | 1 | 3 | None | 🟢 **Steady** | No merges; 3 fix PRs under review |
| **NullClaw** | — | — | — | ⚪ **Inactive** | No activity |
| **TinyClaw** | — | — | — | ⚪ **Inactive** | No activity |
| **ZeptoClaw** | — | — | — | ⚪ **Inactive** | No activity |

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale dominance:** 500 issues and 500 PRs updated in 24 hours is 10× the next busiest project (Hermes/ZeroClaw at 50 each). This reflects a massive user base and contributor pool.
- **Automated triage infrastructure:** The `clawsweeper` bot is actively pushing fixes, demonstrating mature automation—though its `recovery-stuck` tag on critical bugs reveals limits.
- **Feature velocity:** Even during stability firefighting, new PRs (session trajectory view, UI improvements) continue to land.

**Technical approach differences:**
- **Multi-surface bindings:** OpenClaw emphasizes unified conversation delivery across bindings (WhatsApp, Telegram, Discord, etc.), with a dedicated PR (#126424) attempting to keep delivery within agent bindings.
- **Beta-driven release strategy:** `v2026.8.1-beta.2` is under heavy community validation, in contrast to NanoBot's more conservative consolidation approach.

**Community size comparison:**
- 500 issues/PRs per day vs. Hermes' 50 and ZeroClaw's 50: roughly **10× larger** engagement.
- However, this scale is a double-edged sword: the 2 P0 bugs are generating community frustration, and the maintenance load is visibly straining the system.

**Risk:** OpenClaw's position as reference implementation makes its stability crises ecosystem-wide events. The SQLite corruption (P0) and event-loop blocking (P0) are the kind of issues that could drive users to alternatives if not resolved quickly.

---

## 4. Shared Technical Focus Areas

Across all active projects, **five requirements are recurring**:

### 1. Session State Integrity & Recovery
- **OpenClaw:** Session trajectory view (#128053), graceful restart with recovery (#57425), context drops (#108215)
- **Hermes:** Session dies after compression hangs (#78981), Telegram history loss (#92279), profile switching breaks WebSocket (#92434)
- **ZeroClaw:** Runtime-owned conversation sessions RFC (#9487), "make sessions usable" (#10141)
- **NanoBot:** Deleted session resurrection (#5483), ephemeral SDK mutation (#5471)
- **PicoClaw:** Cron jobs losing recurring schedules (#1083)

### 2. Tool/MCP Propagation to Subagents
- **OpenClaw:** MCP tools not injected into subagents (#85030)
- **Hermes:** Tool-iteration budget signpost (#92438), per-model execution budgets (#92587)
- **NanoBot:** Business-error envelope misclassification (#5484), MCP server reliability
- **Moltis:** Stale MCP client after server restart (#1231)
- **PicoClaw:** MCP server failure hang (#3269)

### 3. Provider Compatibility & Edge Cases
- **OpenClaw:** vLLM + Thinking breaks tool calls (#124284), streaming watchdog false positives (#68596)
- **Hermes:** DeepSeek 500k-token sessions (#78981), Codex OAuth refresh timeout (#89278)
- **CoPaw:** OpenRouter/OpenCode not rendering (#7215), per-provider media caps (#7201)
- **IronClaw:** Integration setup failures (Slack/Notion) (#7822, #7823)
- **LobsterAI:** Kimi 2.5 duplicate messages (#1206)

### 4. Context Compression & Cost Management
- **OpenClaw:** Context usage drops without compaction (#108215)
- **IronClaw:** 4.1× token cost regression (#7824), context projection proposal
- **ZeroClaw:** Memory lifecycle RFC (#6850)
- **Hermes:** Session compression hangs (#78981)

### 5. Observability & Trustworthy Telemetry
- **NanoBot:** LangSmith tracing regression (#5485), unified turn observability (#5486), measured request context (#5469)
- **Hermes:** Exposed webhook credential (#92457), security audit false positives (#92549)
- **ZeroClaw:** Daemon diagnostics lose error chains (#10232), provider failures bury cause-specific diagnostics (#9001)
- **IronClaw:** Authoritative run outcomes via journal transitions (#7700)

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target User | Architecture Distinctive |
|---------|--------------|-------------|--------------------------|
| **OpenClaw** | Multi-surface agent runtime | Power users, self-hosters | Multi-binding delivery, automated triage bot (clawsweeper) |
| **Hermes Agent** | Fleet-managed agent infrastructure | Enterprises, multi-device users | Remote gateways, webhook surface, sandboxing |
| **NanoBot** | Lightweight, SDK-first assistant | Developers building on agent APIs | Typed LLM usage contract, ephemeral run semantics |
| **NanoClaw** | Setup simplicity, channel reliability | Non-technical users, SMBs | Slack/Telegram auto-provisioning, prebuilt binaries |
| **ZeroClaw** | Policy-enforced agent architecture | Security-conscious operators | RFC-driven design, WASM plugins, granular sandboxing |
| **IronClaw** | Creative/integration agent | Content creators, notetakers | Context projection, SRT captioning, CRM/Drive tooling |
| **PicoClaw** | Lightweight, multi-channel agent | SBC/hobbyist enthusiasts | Sipeed hardware focus, DelaChat support, cron automation |
| **CoPaw** | Chinese-language agent UX | Chinese-speaking Windows users | HERMES-style reasoning display, UTF-8 handling |
| **Moltis** | Policy-enforcement agent | Security-focused integrators | Fail-closed hooks, OpenAI Codex compatibility |
| **LobsterAI** | Document analysis assistant | Enterprise document workers | Cowork sessions, markdown export, model-specific handling |

**Key architectural divergence:** ZeroClaw and Moltis emphasize **policy/sandboxing** as core value, while OpenClaw and Hermes prioritize **multi-surface reach** and **fleet management**, respectively. NanoBot's SDK-first approach is unique—it treats the agent as a library, not a standalone product.

---

## 6. Community Momentum & Maturity

### Tier 1: High-Velocity, Scaling Pains
- **OpenClaw:** 500 issues/PRs daily; critical bugs showing strain
- **Hermes:** 50 issues/PRs daily; large backlog, active fix queue
- **ZeroClaw:** 50 issues/PRs daily; RFC-heavy, decision queue bottleneck

### Tier 2: Consolidating, Feature-Completing
- **NanoBot:** 21 PRs/day; provider refactor blocking feature work; cleaning house (closing old PRs)
- **NanoClaw:** 25 PRs/day; core-team sprint; setup reliability focus
- **IronClaw:** 22 PRs/day; CI expedite program; economic cost regression concern

### Tier 3: Moderate, Niche-Serving
- **PicoClaw:** 6 PRs/day; long-stale items finally merging; critical bugs lacking fix PRs
- **CoPaw:** 4 PRs/day; Chinese-language UX refinement; no merges this cycle
- **Moltis:** 3 PRs/day; fix PRs under review; security feature request

### Tier 4: Low Activity / Inactive
- **LobsterAI:** Mostly stale auto-closures; 1 critical open PR
- **NullClaw, TinyClaw, ZeptoClaw:** No activity (dead or dormant)

**Rapidly iterating:** OpenClaw, Hermes, ZeroClaw, NanoBot, NanoClaw, IronClaw
**Stabilizing:** PicoClaw, CoPaw, Moltis
**Dormant:** NullClaw, TinyClaw, ZeptoClaw, LobsterAI (effectively)

---

## 7. Trend Signals

### For AI Agent Developers:

1. **Reliability > Features** — Across every active project, bug fixes and stability harding dominate over new features. Users are hitting real production failures (data loss, hangs, corruption). The era of "demo-ware" is over; production-readiness is now table stakes.

2. **Cost Control is a First-Class Concern** — IronClaw's 4.1× token cost regression (cited with hard numbers: 227.7M vs 55.1M input tokens, $10.31 vs $2.52) is the most explicit signal. Context compaction, memory lifecycle policies, and measured telemetry are becoming must-haves.

3. **Multi-Agent Tool Propagation is Broken Everywhere** — MCP tool injection into subagents fails across OpenClaw, Hermes, NanoBot, and PicoClaw. This is the single biggest blocker to complex agent workflows. Expect a framework-level solution to emerge.

4. **Observability Must Be Trustworthy** — LangSmith tracing regressions, misleading error envelopes, and silent failures erode user trust. Projects that ship transparent, cause-preserving diagnostics will win.

5. **Windows is a Second-Class Citizen — and Users Notice** — ZeroClaw's 74 Windows test failures and CoPaw's UTF-8 issues reflect a meaningful cohort of Windows users whose experience degrades. Cross-platform parity is a competitive differentiator.

6. **Integration Failures are a Retention Risk** — IronClaw's Slack/Notion setup failures, CoPaw's provider rendering issues, and Hermes' webhook exposure highlight that third-party integrations are both a feature and a liability.

7. **Security Hooks Need Fail-Closed Semantics** — Moltis' fail-closed policy request and Hermes' shell-hook approval bypass fix indicate a shift toward deterministic security boundaries over optimistic defaults.

### For Ecosystem Watchers:

8. **Consolidation via Cleanup** — NanoBot and LobsterAI are closing stale PRs rather than merging—a sign that maintainers are curating scope. Expect feature rationalization in the next release cycles.

9. **Voice is Emerging as a Next Frontier** — ZeroClaw's Gemini Live RFC and voice-host channel signal interest in realtime speech interfaces. Watch for this to broaden the user base beyond keyboard-centric developers.

10. **The LTS Gap** — With many projects in beta (OpenClaw v2026.8.1-beta.2, ZeroClaw v0.8.3, Hermes v0.20.4), there's no clear "stable release champion." This is an opportunity for the first project to ship a rock-solid LTS.

---

*Generated 2026-08-23 from 10 project digests. Data sources: GitHub activity metrics and community discussions.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-23

## 1. Today's Overview

NanoBot is experiencing a very busy development period. 21 pull requests were updated in the last 24 hours (14 open, 7 merged/closed)—the second consecutive day of very high activity—signaling an active sprint focused on provider architecture, WebUI polish, and bug hardening. No new releases were published and no new issues were opened or updated, but the flurry of PR activity (including 3 merged documentation/feature PRs today) reflects a healthy but code-heavy project phase. However, a significant backlog is forming: several larger PRs (e.g., #5487, #5408, #5367) are marked with `conflict`, and some have been open for 5-10 days, indicating maintainers are prioritizing the provider refactoring stack (#5480 #5481 #5482) ahead of feature work.

## 2. Releases

No new releases were published in the last 24 hours. The project has shifted into a pre-release consolidation phase with the ongoing provider usage-contract refactor (#5480, #5481) and WebUI observability work (#5486, #5490, #5491) — these likely need to land and be tested before the next tagged release.

## 3. Project Progress

Seven PRs were merged or closed today. The two most impactful:

- **#5486** — [feat(webui): unify turn observability](https://github.com/HKUDS/nanobot/pull/5486) (merged, Re-bin): Projects each user turn into a single answer surface while preserving ordered reasoning, tool, and file-edit segments. Reports trustworthy per-turn input/output/cache metrics. This is a major UX and telemetry improvement for the WebUI.
- **#5488** — [docs: refresh team and contributor credits](https://github.com/HKUDS/nanobot/pull/5488) (merged, Re-bin): Updates maintainer profiles (Xubin Ren, Yongru Chen), replaces the contrib.rocks image with a native responsive avatar wall, and includes all registered human contributors. A rare non-technical but community-health-positive merge.

Also merged/closed today:
- **#4430** — [feat(web): configure web_fetch provider](https://github.com/HKUDS/nanobot/pull/4430) (closed, ChachAloha): This large PR adds `auto`, `tavily`, `jina`, and `readability` web_fetch modes. It was closed after ~2 months, not merged — likely superseded by the provider refactor.
- **#3869** — [fix(providers): DeepSeek message hardening](https://github.com/HKUDS/nanobot/pull/3869) (closed, DreamShepherd2006): Fixes 400 errors on null content and "(empty)" placeholder leakage. Closed without merge after ~3 months, possibly applied differently in the new typed provider contract (#5480).
- **#3294** — [feat(dream): optional kill switch + custom Phase 1/2 template paths](https://github.com/HKUDS/nanobot/pull/3294) (closed, pixan-ai): Adds `enabled` flag and customizable templates for the Dream self-learning loop. Open since April, closed without merge.
- **#5156** — [fix(telegram): recover from silently stalled polling](https://github.com/HKUDS/nanobot/pull/5156) (closed, QQQ300kuai): Fixes a production issue where Telegram polling dies silently (referencing #5171). Closed after several weeks — likely addressed in a different commit.

Notable: three old PRs (#4430, #3869, #3294) were closed *without* being merged today, suggesting the maintainers are cleaning house as they land a new provider/usage architecture (#5480) that may make those approaches obsolete.

## 4. Community Hot Topics

No issues or PRs have accumulated comments or reactions in the last 24 hours, but three PRs stand out for their heavy review-load (`conflict` tag, multiple days open) and scale:

- **#5487** — [feat(webui): file preview path fixes + subagent activity & lifecycle replay](https://github.com/HKUDS/nanobot/pull/5487) — Large two-batch WebUI/agent lifecycle PR from yuanyi1415, 6 days open with conflict markers. The "lifecycle replay" aspect is notable — likely a precursor to better agent debugging.
- **#5408** — [feat(webui): add follow-up suggestions](https://github.com/HKUDS/nanobot/pull/5408) — A DeerFlow-style interaction where the composer auto-fills on clicking a suggestion. Open 6 days, marked `conflict`. Feature-rich but waiting for the WebUI observability churn to settle.
- **#5367** — [feat(webui): localize agent activity](https://github.com/HKUDS/nanobot/pull/5367) — Localizes agent activity labels across 10 locales with live language switching. Open 10 days with conflicts, but it's pure UI work — likely merges once #5486 lands.

Underlying need: the community is actively trying to improve the WebUI (observability, localization, file handling, follow-ups) but is temporarily blocked by the provider-usage refactor consuming maintainer attention.

## 5. Bugs & Stability

One new regression was reported today via a fix PR; other fixes from the past 2–3 days remain in review. Ranked by severity:

1. **LangSmith tracing regression (High)** — [#5485](https://github.com/HKUDS/nanobot/pull/5485) (open, xuhaonan013): The LiteLLM-to-native-SDK migration broke LangSmith tracing. Fix wraps OpenAI-compatible and Anthropic clients with LangSmith wrappers. References issue #2493. If you rely on LLM observability, this is a critical gap.
2. **Deleted session resurrection (Medium-High)** — [#5483](https://github.com/HKUDS/nanobot/pull/5483) (open, KDB-Wind): Delayed cross-session messages can recreate a session after it has been deleted. Fix marks them as requiring an existing session and checks metadata without creating. Data-hygiene/reliability concern.
3. **Business-error envelope misclassification (Medium)** — [#5484](https://github.com/HKUDS/nanobot/pull/5484) (open, c020627): MCP servers that return error payloads with `isError=false` cause the agent to treat failures as success. Fix flags these envelopes.
4. **Ephemeral SDK runs mutating session state (Medium)** — [#5471](https://github.com/HKUDS/nanobot/pull/5471) (open, waelantar): `ephemeral=True` documented as non-persisting, but implementation persists the turn. A contract violation for SDK users.
5. **Telegram silent polling stall (Medium, production)** — [#5156](https://github.com/HKUDS/nanobot/pull/5156) (closed today): Production issue where polling permanently stalls after transient network blips. Closed without merge — monitoring whether the fix landed in another commit.
6. **DeepSeek message hardening (Medium)** — [#3869](https://github.com/HKUDS/nanobot/pull/3869) (closed today): 400 errors on null content and "(empty)" placeholder leakage into model context. Closed; expected to be inherently addressed by the typed LLM usage contract (#5480).

No new *issues* were filed today, but these fix-PRs confirm the project is in "hardening" mode. None of the open fix PRs have landed yet — expect a consolidation wave over the next few days.

## 6. Feature Requests & Roadmap Signals

Today's PRs signal the direction of the next minor release:

- **Typed LLM usage contract (#5480)** — foundation for consistent token/cache semantics across all providers. This will make future per-turn telemetry (#5490, #5491) and trajectory recording (#5481) reliable.
- **User-controlled turn recovery (#5420)** — persists a sidecar checkpoint for interrupted WebSocket turns, with explicit Continue/Dismiss recovery in WebUI and TUI. Prediction: **likely in next release**; it's been open 5 days, feature-complete, and seems aligned with the maintainers' observability push.
- **Email channel performance (#5489)** — IMAP header-before-body fetch and UID SEARCH to avoid re-fetching. A strong *quality-of-life* fix for email-heavy users; likely merges soon.
- **Follow-up suggestions (#5408)** and **agent activity localization (#5367)** — both gated on the WebUI observability merge (#5486). Prediction: land in the *release after next*.
- **Ephemeral run semantics (#5471)** — an SDK contract fix that will become important as more users build on the SDK.

## 7. User Feedback Summary

No new issues were filed or commented on today, so direct feedback signals come from the fix-PRs, which reflect real pain points:

- **Observability is the #1 pain point.** The LangSmith regression (#5485, referencing #2493), the token-usage UI clarity work (#5490), measured-request-context telemetry (#5469), and the unified turn observability merge (#5486) all point to users needing *trustworthy* token and reasoning visibility — not just cumulative counters.
- **MCP integration is a trust gap.** The business-error misclassification bug (#5484) suggests agents are silently acting on failed tool calls. Users are clearly failing forward with MCP servers that don't follow the spec.
- **Session and state integrity matters.** Deleted-session resurrection (#5483) and ephemeral SDK mutation (#5471) indicate users are running long-lived or automated workflows where state correctness is critical.
- **Email users are performance-sensitive.** The IMAP body-before-header fetching (#5489) implies users are hitting high-latency and re-fetch penalties in email-heavy environments.
- **SDK users are hitting edge cases** — the ephemeral-run bug (#5471) and turn-recovery feature (#5420) are both SDK/API-driven, indicating a growing developer ecosystem.

## 8. Backlog Watch

No long-unanswered *issues* are outstanding, but several open PRs have been idle for a week or more and need maintainer attention or explicit closure:

- **#5367 — localize agent activity (10 days open, `conflict`)** — [link](https://github.com/HKUDS/nanobot/pull/5367): Pure UI work, large but low-risk. Should be rebased and merged after #5486.
- **#5408 — follow-up suggestions (6 days open, `conflict`)** — [link](https://github.com/HKUDS/nanobot/pull/5408): A strong UX feature; needs a maintainer to resolve the conflicts.
- **#5487 — file preview + subagent lifecycle (6 days open, `conflict`)** — [link](https://github.com/HKUDS/nanobot/pull/5487): Large PR mixing two concerns; likely needs to be split into two reviewable units.
- **#5420 — user-controlled turn recovery (5 days open)** — [link](https://github.com/HKUDS/nanobot/pull/5420): Feature-complete and aligned with current direction; needs review and a decision on the WebUI/TUI integration.
- **#5469 — show measured request context in TUI (2 days open, `conflict`)** — [link](https://github.com/HKUDS/nanobot/pull/5469): Directly improves TUI token transparency, closely tied to the usage-contract work.

Additionally, the closure of three older feature PRs (#4430, #3869, #3294) without merge suggests the maintainers are deferred or superseded them — community contributors should check in to see if their work is being incorporated upstream or if alternative implementations are planned.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-08-23

---

## 1. Today's Overview

Hermes Agent is experiencing a high-velocity development period, with **50 issues and 50 PRs** updated in the last 24 hours. The project demonstrates strong community engagement, though maintainers face pressure from a **large backlog of open issues (46 open vs 4 closed)** and an **aging PR queue**, with several critical PRs remaining open for weeks. The majority of activity centers on **stability and reliability improvements**, particularly around fleet update management, session state persistence, and security hardening. While no new releases were published today, a significant number of patches are queued and nearing merge readiness. Notably, the project shows a **healthy mix between maintainer-driven architecture work (e.g., gateway control socket design)** and **community-contributed feature requests (e.g., pt-BR language support, per-model execution budgets)**.

---

## 2. Releases

**No new releases were published in the last 24 hours.** The most recent version referenced in the data is **v0.20.4**, with the next patch release likely forthcoming given the volume of merged fixes in the queue.

---

## 3. Project Progress

**7 PRs were merged or closed** in the last 24 hours, but the data set does not explicitly itemize which ones. Based on recent activity patterns and PR descriptions, likely merge candidates include:

- **fix(hooks): stop shell hook approval requests from bypassing confirmation** (#92562) — Addresses a security-relevant bug where shell hooks could silently approve tool calls. The fix makes the documented `{"action":"approve"}` directive actually require human confirmation, and improves `hermes hooks doctor` validation.
- **fix(compression): keep Desktop and TUI previews from mutating sessions** (#92591) — Prevents `/compress --preview` and `--dry-run` from mutating live sessions, preserving session identity and transcript history. Critical for user trust in compression workflows.
- **fix(stream-drop): "sse" only as whole word** (#92580) — Fixes a pattern-matching bug that misclassified errors containing words like "surpassed" as stream drops.

Additionally, the project shows **ongoing architectural progress** on the **Fleet update reliability tracking issue** (#91277), which consolidates ~30 open issues and ~15 PRs into a single deployment plan for local, multi-profile, remote, and image-managed installs. This is the project's top-priority improvement area.

---

## 4. Community Hot Topics

The most active discussions highlight the **project's core pain points around stability and fleet management**:

1. **[#66616 — Skills index stale/degraded (78 comments)](https://github.com/NousResearch/hermes-agent/issues/66616)**
   - Automated freshness probe is failing: the Skills Hub index is 29.8h old (limit 26h). This is a long-running (since July 18) infrastructure reliability issue generating the most comments by far, indicating high community interest in the skills ecosystem.

2. **[#84834 — Webhook Feature Package meta-issue (22 comments)](https://github.com/NousResearch/hermes-agent/issues/84834)**
   - A "graph-gated 5×2×3 repair package" for the entire webhook surface (ingress, execution, delivery, configuration, UI, deployment, docs). This is a comprehensive refactoring effort with clear architectural vision.

3. **[#91277 — Fleet update reliability tracking (14 comments)](https://github.com/NousResearch/hermes-agent/issues/91277)**
   - The **#1 pain point** for the project. Community members and maintainers agree that install/update is the "least reliable capability" with ~30 issues and ~15 PRs each addressing isolated symptoms. The issue calls for a unified deployment plan.

4. **[#38873 — Desktop remote gateway flaps back to local (11 comments, 3 👍, CLOSED)](https://github.com/NousResearch/hermes-agent/issues/38873)**
   - Originally reported June 4, now closed — likely fixed. Windows desktop app successfully connects to remote VPS backend but reverts to local mode.

5. **[#74816 — Multi-device session sync like WeChat (3 comments, 2 👍)](https://github.com/NousResearch/hermes-agent/issues/74816)**
   - Feature request for real-time cross-device session synchronization. Low comment count but positive reactions suggest latent demand for this modern UX pattern.

**Underlying need analysis:** The community desperately wants **reliable fleet management** (update, multi-agent deployment, session continuity) and **consistent cross-platform behavior**. The high comment count on infrastructure issues vs. feature requests suggests the community is more focused on fixing what's broken than adding new features right now.

---

## 5. Bugs & Stability

The following bugs were reported or updated today, ranked by severity:

| Rank | Issue | Severity | Status |
|------|-------|----------|--------|
| 1 | **[#92457 — Exposed webhook credential in repository history](https://github.com/NousResearch/hermes-agent/issues/92457)** | **Security (P1)** | Open — security incident requiring credential rotation and image republish |
| 2 | **[#92279 — Telegram profile sessions lose all history every turn (regression 0.20.1→0.20.5)](https://github.com/NousResearch/hermes-agent/issues/92279)** | **Data loss (P1)** | Open — cache probe/rebuild reads wrong store (main vs. profile); marked duplicate |
| 3 | **[#78981 — Session permanently dies after repeated context-compression hangs (DeepSeek 500k-token)](https://github.com/NousResearch/hermes-agent/issues/78981)** | **Critical (P1)** | Open — stalled streams, 600s ceiling, no recovery; risk: session state |
| 4 | **[#83832 — PKCE state cookie breaks OIDC login](https://github.com/NousResearch/hermes-agent/issues/83832)** | **Security (P2)** | Open — literal `;` in cookie value violates RFC 6265 |
| 5 | **[#92271 — Windows Docker sandbox broken (colon in paths, WinError 267)](https://github.com/NousResearch/hermes-agent/issues/92271)** | **Platform-breaking (P2)** | Open — every tool call fails on Windows with Docker backend |
| 6 | **[#92535 — Git updates lose receipts when stale-module purge evicts update_receipt](https://github.com/NousResearch/hermes-agent/issues/92535)** | **High (P2)** | Open — successful updates don't write promised receipt |
| 7 | **[#92554 — Writing config.yaml destroys all user comments](https://github.com/NousResearch/hermes-agent/issues/92554)** | **Medium (P2)** | Open — re-serialization strips all comments |
| 8 | **[#92549 — Security audit reports shadowed stale lazy-packages version](https://github.com/NousResearch/hermes-agent/issues/92549)** | **Medium (P2)** | Open — false positive in `hermes security audit` |
| 9 | **[#92480 — Desktop downloads strip extension for .pptx/.pdf](https://github.com/NousResearch/hermes-agent/issues/92480)** | **Medium (P2)** | Open — save dialog offers only "All Files" |
| 10 | **[#92434 — Profile switching breaks WebSocket connection](https://github.com/NousResearch/hermes-agent/issues/92434)** | **Medium (P2)** | Open — requires app restart |

**Fix PRs in flight:** #92562 (hook approval), #92580 (stream-drop false positive), #92582 (grace window for non-Telegram platforms), #92585 (approvals allowlist), #92589 (gateway restart duplication), #92586 (redaction for Python repr) — all open but likely merge-ready.

---

## 6. Feature Requests & Roadmap Signals

Strong signals for the next release include:

1. **[#92091 — Gateway control socket design](https://github.com/NousResearch/hermes-agent/issues/92091)** — Architecture issue by teknium1 calling for a gateway-owned control contract instead of process-scanning heuristics. This is the **cornerstone fix** for all fleet update problems and likely heads the next milestone.

2. **[#91230 — Task Completion Verification as "sixth law"](https://github.com/NousResearch/hermes-agent/issues/91230)** — Proposal by andrexibiza for "exact-object completion" verification. Philosophical but actionable; could become a design document.

3. **[#74816 — Multi-device session sync](https://github.com/NousResearch/hermes-agent/issues/74816)** — Real-time cross-device sessions "like WeChat." High user value, but requires significant architectural work (session state, encryption, conflict resolution). Likely a **long-term roadmap item**, not near-term.

4. **[PR #92590 — pt-BR language support](https://github.com/NousResearch/hermes-agent/pull/92590)** — Full Brazilian Portuguese translation (>3,400 lines). Ready for merge; low-risk high-value community contribution.

5. **[PR #92587 — Per-model execution budgets](https://github.com/NousResearch/hermes-agent/pull/92587)** — Config-driven caps on tool executions per turn. Addresses a "strong brain model" cost-control use case. Likely merge candidate.

6. **[PR #92438 — Tool-iteration-budget signpost](https://github.com/NousResearch/hermes-agent/pull/92438)** — Opt-in signal for finite tool-iteration caps, allowing checkpointing before cutoff. Low-risk config-driven feature.

**Prediction:** The next release (v0.20.5 or v0.21.0) will prioritize: **fleet update reliability**, **gateway control socket**, and **data loss fixes** (session compression, Telegram history). Feature velocity will be lower than bug-fix velocity.

---

## 7. User Feedback Summary

**Positive signals:**
- **Desktop remote gateway fix** (#38873) closed — a long-standing pain point resolved.
- Community members are actively contributing fixes (11 different PR authors in last 24h), indicating healthy contributor engagement.
- The **pt-BR translation** PR shows community investment in localization and accessibility.

**Pain points (explicit and implicit):**

- **"Install/update is our least reliable capability"** — teknium1 (maintainer) acknowledges the community's biggest frustration. Users report per-platform spaghetti code, no verification, no plan.
- **Session loss and state corruption** dominate bug reports: DeepSeek sessions dying, Telegram history loss, profile switching breaking WebSockets. Users have zero tolerance for data loss — these issues **must be resolved first**.
- **"config.yaml comments are the natural place to record why a setting is what it is"** — hubbadubbadubdab articulates a user expectation that config edits preserve documentation. The fact that `hermes` even wipes comments suggests poor respect for user customizations.
- **Security concerns are visible**: exposed webhook credential, PKCE cookie bug, SSRF boundary bypasses. Users depend on Hermes for production automation; security issues erode trust.

**Sentiment:** The community is **frustrated by instability but engaged and hopeful**. They are actively contributing fixes (15+ PRs open today) and proposing design improvements. The maintainer acknowledging "no plan, no verification" is both honest and a rallying point.

---

## 8. Backlog Watch

Long-standing items desperately needing maintainer attention:

| Item | Age | Why It Matters |
|------|-----|----------------|
| **[PR #89461 — SSRF network boundary for browser_exec](https://github.com/NousResearch/hermes-agent/pull/89461)** | 5 days | **Security-critical** — currently blocked, author warns "do not merge current head" due to exact-head bypasses. Maintainers must resolve the conflict and get this merged. |
| **[PR #71370 — Mask secrets in Python mapping reprs](https://github.com/NousResearch/hermes-agent/pull/71370)** | 29 days | **Security issue** — stale PR (salvaged by #92586); opaqueness in tracebacks risks credential leakage. |
| **[PR #51152 — Memory tiering with [core] prefix](https://github.com/NousResearch/hermes-agent/pull/51152)** | 61 days | **Long-running feature** — reduces token costs, but has 5 sweeper risk labels. Needs decisive review. |
| **[Issue #70606 — Hindsight local_embedded env overwrite](https://github.com/NousResearch/hermes-agent/issues/70606)** | 30 days | **Data loss** — user config destroyed on every daemon start. P3 but with lasting harm. |
| **[Issue #71239 — Telegram Application.dispatcher stalls invisibly](https://github.com/NousResearch/hermes-agent/issues/71239)** | 29 days | **Message delivery risk** — can silently eat updates; compounded by #92279 regression. |
| **[PR #38953 — Deny writes to Google Workspace/Bitwarden stores](https://github.com/NousResearch/hermes-agent/pull/38953)** | 80 days | **Security** — open for over 2 months, P2. File-safety boundary incomplete. |

**Most critical maintainer action:** The **fleet update reliability** class of issues (#91277, #92091, #92535) needs a consolidated response. The community is watching and contributing; maintainers should publish the unified design and acknowledge all ~30 individual issues as tracked under it.

---

*Data source: NousResearch/hermes-agent GitHub repository, all activity from 2026-08-22 to 2026-08-23.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-23

## Today's Overview

PicoClaw is in a moderate activity phase today with 2 open issues and 6 pull requests touched in the last 24 hours, though no new releases were published. The project shows healthy momentum with 4 PRs merged or closed, including long-running items from February and March (PR #714, #1083, #1545) that finally crossed the finish line. The most critical ongoing concern is an MCP server failure hang (Issue #3269) that has a candidate fix PR (#3337) under review. Two stale issues and one stale PR are accumulating age, suggesting maintainers may need to triage older items more aggressively. The Telegram tool runaway edit loop (Issue #3343) reported yesterday is a fresh and serious bug that currently lacks an associated fix PR.

## Releases

No new releases were published in the last 24 hours. The most recent build remains the nightly snapshot referenced in Issue #3269 (git: 2cf030d2). Users tracking stable features should monitor PR #3337 (MCP failure fix) and #3319 (exec tool timeout fixes) for inclusion in the next versioned release.

## Project Progress

Four PRs were merged or closed in the last 24 hours, representing a significant backlog cleanup:

- **[PR #714 — skills: install/reinstall CLI and refactor into skillsCmd](https://github.com/sipeed/picoclaw/pull/714)**: Closed after a 6-month journey (created Feb 24). This enhancement adds `ParseInstallSpec`, `InstallFromGitHubEx`, `fetchTree`, and `validateSubpath` functions, supporting `repo@branch` syntax with optional subpaths. It introduces a `reinstall` subcommand with force-overwrite semantics and switches production installs to the GitHub Trees API. This is a substantial improvement to skill installation ergonomics.

- **[PR #1083 — fix(cron): preserve recurring job schedule after execution](https://github.com/sipeed/picoclaw/pull/1083)**: Closed. Fixes a subtle bug where recurring cron jobs were silently degrading into one-shot "at" tasks. The root cause was `computeNextRun()` returning `nil` and losing the original schedule. This was a 5-month-old fix that resolves a reliability issue for automation users.

- **[PR #1545 — fix: merge PR #1500 #1490 #1488 #1487 #1485](https://github.com/sipeed/picoclaw/pull/1545)**: Closed. A consolidation merge bringing in five separate fixes, effectively sweeping up older open PRs. This type of merge reduces review burden but may hide individual fix details.

- **[PR #3319 — fix(tools): honor exec timeout and boolean run options](https://github.com/sipeed/picoclaw/pull/3319)**: Closed. The `exec` tool was advertising a per-run `timeout` argument but silently using the global timeout; it also declared `background` and `pty` as strings when they should be booleans. This fixes a correctness issue for users relying on long-running or background executions.

## Community Hot Topics

The most active discussion by far is **[Issue #3269 — MCP server connection failure hangs the agent loop](https://github.com/sipeed/picoclaw/issues/3269)**, with 6 comments and 1 reaction. The reporter (ruiyigen) describes a complete loss of chat interface responsiveness when an MCP server is unreachable. This issue is now over a month old (created Jul 20) and has a candidate fix in PR #3337. The community need here is clear: **resilience**. Users expect the agent loop to recover gracefully from downstream service failures rather than entering a permanent hang state.

A newer discussion, **[Issue #3343 — Tool feedback animation edits Telegram messages indefinitely after a failed turn](https://github.com/sipeed/picoclaw/issues/3343)**, was just opened by raine and has no comments yet. The severity is immediately visible: over 228,000 `editMessageText` calls over several days triggered a Telegram server-side rate limit (`retry_after`). This is a hot topic waiting to ignite — the combination of runaway behavior and external rate limiting will likely draw attention quickly.

The stale **[PR #3222 — refactor(deltachat): cleanup implementation, documentation -200LOC](https://github.com/sipeed/picoclaw/pull/3222)** also remains in the spotlight as a substantial refactor (-200 LOC) that has been open since July 3 without a merge decision.

## Bugs & Stability

| Severity | Issue | Description | Status |
|----------|-------|-------------|--------|
| **High** | [#3343](https://github.com/sipeed/picoclaw/issues/3343) | Tool feedback animation loops Telegram `editMessageText` forever — 228K edits, triggers `retry_after` rate limit | Open, no fix PR yet |
| **High** | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | MCP server failure hangs agent loop; chat stops responding entirely | Open; fix PR #3337 in review |
| Medium | [#3319](https://github.com/sipeed/picoclaw/pull/3319) | `exec` tool ignores per-run `timeout`; `background`/`pty` typed as strings | **Fixed** — PR closed |
| Medium | [#1083](https://github.com/sipeed/picoclaw/pull/1083) | Recurring cron jobs silently become one-shot tasks | **Fixed** — PR closed |

The severity ranking places the Telegram runaway loop at the top because it causes sustained resource waste, external API abuse, and effective service degradation for that user. The MCP hang follows closely since it bricks the entire chat interface. Both are unmitigated in the current nightly build, with only the MCP issue having a pending fix.

## Feature Requests & Roadmap Signals

The **[skills CLI refactor (PR #714)](https://github.com/sipeed/picoclaw/pull/714)** signals a clear roadmap direction: **improved skill lifecycle management**. The `reinstall` subcommand and GitHub Trees API usage suggest the team is prioritizing reliable, Git-based skill distribution.

The **[deltachat refactor (PR #3222)](https://github.com/sipeed/picoclaw/pull/3222)** hints at **channel maturity** — dropping legacy features and enforcing secret-via-jsonrpc suggests a move toward security-hardened, standards-compliant messaging integrations.

The **[exec tool timeout fix (PR #3319)](https://github.com/sipeed/picoclaw/pull/3319)** indicates the team acknowledges that **fine-grained execution control** matters. Users want per-invocation timeouts, background execution, and proper PTY semantics — expect these to be solidified in the next release.

Looking at next-version predictions: the MCP hang fix (#3337) is the strongest candidate for immediate inclusion, followed by the deltachat cleanup (#3222). The knowledge gap between these and the Telegram loop fix is concerning — the latter currently has no PR attached.

## User Feedback Summary

Users are communicating pain points in two distinct areas:

1. **Reliability under failure** (Issue #3269): The MCP hang scenario is a hard failure — the chat interface goes completely silent. The reporter emphasized "stop replying to users," which is the worst possible outcome for an agent product. The 6 comments on this issue suggest multiple users or maintainers are validating the problem, but no workaround has surfaced.

2. **Runaway processes** (Issue #3343): The Telegram edit loop reveals a design gap: the tool feedback animation has no termination condition tied to actual progress. The user had to wait until Telegram enforced a rate limit — there was no defensive mechanism on the PicoClaw side. This is a silent resource leak that only surfaces through external rate limiting.

On the positive side, the end-to-end completion of several long-lived PRs (skills, cron, exec tooling) should represent meaningful quality-of-life improvements for users leveraging automations and extended tooling.

## Backlog Watch

| Item | Age | Signal | Concern |
|------|-----|--------|---------|
| **[Issue #3269](https://github.com/sipeed/picoclaw/issues/3269)** (MCP hang) | 34 days | No maintainer response visible; fix PR exists (#3337) | Needs review and merge — this is a critical availability fix |
| **[PR #3337](https://github.com/sipeed/picoclaw/pull/3337)** (MCP hang fix) | 9 days | Open, no comments | Must be reviewed — it is the only fix for the most severe open bug |
| **[PR #3222](https://github.com/sipeed/picoclaw/pull/3222)** (deltachat refactor) | 51 days | Stale label applied | Substantial refactor risk of bit-rotting; needs decision to merge or close |
| **[Issue #3343](https://github.com/sipeed/picoclaw/issues/3343)** (Telegram loop) | 1 day | Fresh; no comments yet | Urgent — needs fast triage and a fix PR; high-impact runaway behavior |

The **most critical backlog item** is the combination of Issue #3269 and PR #3337 — a known critical bug with a waiting fix. This pairing should be prioritized above all other work. The stale PR #3222 (51 days) is at real risk of accumulating merge conflicts and being abandoned, which would waste a 200-line refactor effort.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest
**Date:** 2026-08-23

---

## 1. Today's Overview

NanoClaw is exhibiting a **high-velocity development cadence** with 25 pull requests updated in the last 24 hours, though only 8 were merged or closed. The project is currently focused heavily on **chat adapter reliability** (Telegram and Slack), **setup wizard improvements** for multi-instance configurations, and **stability hardening** around build processes and circuit breakers. One new issue (#3453) was filed regarding test failures on Node 25+, indicating active forward-compatibility work. The majority of open PRs (17) are tagged with `core-team`, suggesting a coordinated internal sprint. No releases were published today, but the volume of merged fixes points to an imminent release candidate.

---

## 2. Releases

**No new releases were published in this 24-hour window.**

---

## 3. Project Progress

Eight pull requests were merged or closed today. Key completed work includes:

| PR | Title | Status | Impact |
|----|-------|--------|--------|
| [#3394](https://github.com/nanocoai/nanoclaw/pull/3394) | fix(slack): working manual-install fallback, delivered to the requester | **Merged** | Fixes broken Slack manual-install fallback URL and agent-driven provisioning dead-end |
| [#3390](https://github.com/nanocoai/nanoclaw/pull/3390) | fix(setup): skip Slack auto-provisioning when a bot is already saved | **Merged** | Prevents duplicate Slack app provisioning on setup reruns |
| [#3443](https://github.com/nanocoai/nanoclaw/pull/3443) | build: drop better-sqlite3 from onlyBuiltDependencies — use its bundled prebuilds | **Merged** | Eliminates node-gyp rebuild requirement; faster, more portable installs |
| [#3444](https://github.com/nanocoai/nanoclaw/pull/3444) | fix(upgrade-state): accept a version-matching marker when Git cannot identify the checkout | **Merged** | Graceful fallback for upgrade checks in non-Git deployments |
| [#3445](https://github.com/nanocoai/nanoclaw/pull/3445) | Closing: wrong repository | **Closed** | Accidental PR, no impact |

**Advances in progress:**
- **Slack reliability** is a clear theme — the manual-install fallback and duplicate-provisioning fixes directly address recurring setup friction.
- **Build portability** was improved by leveraging better-sqlite3's prebuilt binaries, removing native compilation from install steps.

---

## 4. Community Hot Topics

The most active discussions (by comment count) center on:

- **[#3452](https://github.com/nanocoai/nanoclaw/pull/3452) — fix(update): give captured update commands a real output buffer** — Author `witek` is addressing a subtle bug where update commands were running without proper buffered output. This touches the core update workflow, a high-stakes path for all users.

- **[#3451](https://github.com/nanocoai/nanoclaw/pull/3451) — fix(update-skills): attribute a barrel import to the skill that appends it** — Also by `witek`, this fixes a code-attribution issue in the update-skills pipeline.

- **[#3450](https://github.com/nanocoai/nanoclaw/pull/3450) — Telegram: trust channel's own identity in sender_scope gate** — Community contributor `wakqasahmed` is fixing anonymous Telegram channel-post handling where the bot couldn't attribute posts to the channel identity.

**Underlying need:** These PRs indicate a push to make **update and setup workflows** more robust and debuggable, while the Telegram identity fixes address a gap in how bot-to-bot communication is authorized.

---

## 5. Bugs & Stability

| Severity | Issue | Status |
|----------|-------|--------|
| **Medium** | **Node 25+ test failures** ([#3453](https://github.com/nanocoai/nanoclaw/pull/3453)): tsx loader `module.register()` deprecation pollutes stderr in `stdin-json` tests | **Open; no fix PR yet** — forward-compatibility concern as Node 25 rolls out |
| **Low-Medium** | **Telegram channel-post blackholing** ([#3449](https://github.com/nanocoai/nanoclaw/pull/3449)): Server-side persistence of `allowed_updates` causes posts to be silently dropped | **Fix PR open** |
| **Low-Medium** | **Circuit-breaker scope leakage** ([#3447](https://github.com/nanocoai/nanoclaw/pull/3447)): Crash strikes carried across instances sharing `data/` mount | **Fix PR open** |
| **Low** | **Captured update commands lack output buffer** ([#3452](https://github.com/nanocoai/nanoclaw/pull/3452)) | **Fix PR open** |

No critical or high-severity regressions were reported.

---

## 6. Feature Requests & Roadmap Signals

Several PRs point toward **incoming features**:

- **Cursor Agent provider** ([#3355](https://github.com/nanocoai/nanoclaw/pull/3355), [#3356](https://github.com/nanocoai/nanoclaw/pull/3356)): Adding `/add-cursor` agent provider skill and SDK payload. This expands the provider ecosystem — expect this in the **next minor release**.

- **Multi-Telegram-bot support** ([#3438](https://github.com/nanocoai/nanoclaw/pull/3438), [#3437](https://github.com/nanocoai/nanoclaw/pull/3437), [#3435](https://github.com/nanocoai/nanoclaw/pull/3435), [#3431](https://github.com/nanocoai/nanoclaw/pull/3431)): A coordinated feature set to configure **multiple Telegram bots** per instance, with instance-aware pairing and wiring.

- **Auto-drop for automated senders** ([#3446](https://github.com/nanocoai/nanoclaw/pull/3446)): Bots and webhooks (Discord/Slack/Telegram) should skip the unknown-sender approval gate.

- **Group scope override warnings** ([#3448](https://github.com/nanocoai/nanoclaw/pull/3448)): Warn users when group scope auto-fills override explicit args.

The **multi-Telegram-bot** work, in particular, appears release-ready and is the strongest candidate for the next version.

---

## 7. User Feedback Summary

- **Setup friction is the #1 pain point.** Multiple PRs (#3394, #3390, #3438) address broken or duplicated provisioning on Slack and Telegram. Users were hitting dead-ends with no recovery path.
- **Approval cards in group DMs are confusing.** [#3385](https://github.com/nanocoai/nanoclaw/pull/3385) fixes MPDM (Slack group DM) cards showing raw slugs instead of readable names — a UX issue that undermines trust in approval flows.
- **Bot-to-bot messaging is not well-handled.** The Telegram sender-identity fix (#3450) and auto-drop for bots (#3446) both respond to users hitting gates designed for humans.
- **No explicit negative feedback** (no bug reports complaining about regressions) was filed in this window, suggesting the current mainline is stable for core workflows.

---

## 8. Backlog Watch

| PR/Issue | Age | Note |
|----------|-----|------|
| [#3355](https://github.com/nanocoai/nanoclaw/pull/3355) — Cursor Agent provider skill | 4 days | Open but with `core-team` and `follows-guidelines` tags; no comments. Well-specified. |
| [#3385](https://github.com/nanocoai/nanoclaw/pull/3385) — MPDM-aware approval cards | 3 days | Fix for a UX issue; awaiting review. |
| [#3453](https://github.com/nanocoai/nanoclaw/pull/3453) — Node 25+ test failures | 1 day | Newly filed, no maintainer response yet. Needs triage as Node 25 adoption grows. |

**Maintainer attention needed:** The Node 25 test failure (#3453) is the highest-priority item for triage, as it affects forward compatibility. The Cursor Agent provider (#3355) has been waiting 4 days without comments despite being `core-team`-tagged — likely pending review bandwidth.

---

## Project Health Assessment

**Overall: ⭐ Healthy.** High contributor activity (multiple `core-team` members and community contributors), disciplined PR hygiene (guidelines tags, contributing-guide template), and a focus on real user pain points (setup, approval UX, bot identity). The build changes (#3443) are a positive sign for operational maintainability. The main risks are Node 25 compatibility and review bandwidth on the large PR queue.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-23

## 1. Today's Overview

IronClaw is in a period of high-intensity, coordinated engineering activity. The project saw 10 issues and 22 PRs updated in the last 24 hours, with a notable surge of work across four parallel CI-expedite tracks (T1–T4) aimed at eliminating "green locally, red in CI" failures. Core maintainers are driving substantial architectural changes: a unified coding-tool contract (PR #7491), the first act-capable lifecycle hook point (`AfterTurn`), background subagents, and a generic credential-binding system for sandbox egress. Community-contributed bug fixes from `italic-jinxin` (WebUI cleanup, timezone-robust tests, extension setup surfacing) merged cleanly, indicating a healthy contributor pipeline. Project health is stable overall, with no new releases cut this week.

---

## 2. Releases

**None.** No new releases were published in the last 24 hours. The project continues to operate in a pre-release development phase, with substantial feature work landing on `main` but not yet packaged for distribution.

---

## 3. Project Progress

Five PRs were merged/closed in the last 24 hours, all from community contributor `italic-jinxin` (core contributor):

- **[#7773 — refactor(webui): remove duplicate Settings and Extensions tabs](https://github.com/nearai/ironclaw/pull/7773)** — Removed unused tab components and duplicate navigation metadata, eliminating drift between the Settings inventory and actual application routes. Closes issue #7768.

- **[#7774 — test(webui): make automation presenter date assertions timezone-robust](https://github.com/nearai/ironclaw/pull/7774)** — Replaced UTC-dependent date assertions with browser-local formatter-derived expectations. Fixes CI failures in non-UTC timezones (e.g., Asia/Shanghai). Closes #7767.

- **[#7772 — fix(webui): surface extension setup phase and blockers in Configure](https://github.com/nearai/ironclaw/pull/7772)** — Now passes authoritative setup `phase`, readiness `blockers`, and configuration-field presence through `useExtensionSetup`, with localized explanations for every lifecycle blocker kind (Hosted MCP auth, pairing, etc.). Closes #7769.

- **[#7700 — feat(notifications): publish authoritative run outcomes](https://github.com/nearai/ironclaw/pull/7700)** — Materializes scheduled-run completion/failure notifications from committed Process Journal transitions instead of delivery watchers. Publishes completions only after the exact run's finalized reply is durably available; excludes foreground runs, child runs, and ownerless cases. Closes #7691.

- **[#7076 — Install the packages the catalog already publishes](https://github.com/nearai/ironclaw/pull/7076)** — Rebased after three months of staleness; merges package installation work with current `main`, resolving manifest fixture composition issues.

---

## 4. Community Hot Topics

The most active discussions (by comment count and recency) center on **cost**, **architecture**, and **developer experience**:

- **[#7824 — Context projection: Pi-style compaction barrier, structured summaries, overflow recovery](https://github.com/nearai/ironclaw/issues/7824)** *(2 comments, open)* — The most analytically rigorous discussion this week. The author cites measured data from PinchBench (147 tasks): the new coded-tool approach costs 227.7M input tokens / $10.31 vs. the old shell baseline's 55.1M / $2.52 — a **~4× token and cost regression** while accuracy also dropped (54.4% vs 60.5%). The issue proposes context compaction (Pi-style summarization) as the recovery mechanism. **This is the single most important economic issue in the project right now.**

- **[#7815 — Onboarding suggestions: cumulative net-new work to close connect → suggest → thread flow](https://github.com/nearai/ironclaw/issues/7815)** *(1 comment, open)* — Proposes frontend enhancements (refresh action on ready sets, connect entry point) building on three merged features (#7693, #7694, #6994). Active design discussion with an associated PR already open.

- **Four-track CI expedite program** — PRs [#7821 (T1)](https://github.com/nearai/ironclaw/pull/7821), [#7817 (T2)](https://github.com/nearai/ironclaw/pull/7817), [#7820 (T2 probe)](https://github.com/nearai/ironclaw/pull/7820), [#7819 (T3)](https://github.com/nearai/ironclaw/pull/7819), and [#7809 (T4)](https://github.com/nearai/ironclaw/pull/7809) represent a coordinated, measurement-gated effort to kill "queue-only failure" classes and centralize toolchain/build ownership. While comment counts are minimal, the *scale and coordination* of these PRs indicates a major quality-of-life investment for contributors.

**Underlying needs:** The community (especially `serrrfirat` and `henrypark133`) is signaling two priorities: (1) **economic sustainability** — token cost per run must come down via context compaction, not just accuracy gains; and (2) **developer velocity** — CI must be predictable, fast, and locally reproducible.

---

## 5. Bugs & Stability

**High Severity:**

- **[#7824 — Context/cost regression tied to PR #7491](https://github.com/nearai/ironclaw/issues/7824)** — Not a crash, but a **4.1× token-cost increase** (227.7M vs 55.1M) and **−6-point accuracy drop** on PinchBench. This is a severity-1 economic regression for the core coding path. A fix is proposed in the issue itself (context projection with compaction barriers), but no dedicated fix PR exists yet.

**Medium Severity:**

- **[#7813 — UI: heading cropped when suggestions panel appears](https://github.com/nearai/ironclaw/issues/7813)** — Layout regression on chat home screen; the "What do you need help with?" heading is clipped. Newly filed (2026-08-22), no fix PR yet. Likely related to recent suggestions-panel work (#7693/#7694).

- **[#7823 — Notion install fails in IronClaw](https://github.com/nearai/ironclaw/issues/7823)** — Reported via Slack feedback channel; user cannot install the Notion integration. No fix PR yet.

- **[#7822 — Unable to set up Slack in IronClaw](https://github.com/nearai/ironclaw/issues/7822)** — Companion integration-setup failure; user references the Notion issue as related. No fix PR yet.

**Low Severity (already fixed):**

- **Timezone-robust tests (#7774)** and **duplicate Settings tabs (#7773)** — both merged today, closing their respective issues.

---

## 6. Feature Requests & Roadmap Signals

**Strong next-version candidates (already in PR form):**

- **Context projection / Pi-style compaction** (issue #7824) — likely the most impactful next feature; addresses the token-cost crisis introduced by the unified coding-tool surface. Expect a design proposal and phased implementation soon.
- **AfterTurn lifecycle hook + memory curation** (#7765, phase 1 of #7770) — first act-capable hook point; enables privileged memory curation between turns. Large PR, low risk, currently open.
- **Background subagents — producer half** (#7818) — receipts, per-child delivery, activation, healing sweeps. Large PR open; deployment gate noted.
- **Generic credential bindings for sandbox egress** (#7810) — replaces GitHub-specific carve-outs with a provider-neutral broker. Large PR open; directly addresses user-visible integration pain points (Slack/Notion setup failures).
- **CI quadruple-track consolidation** (#7821, #7817, #7819, #7809) — not user-facing but will accelerate all future feature delivery.

**Medium-term signals:**

- **OOBE suggestion drawer enhancements** (#7816) — refresh + connect entries; small, flag-gated, likely to land soon.
- **WebUI design system** (#7257) and **APDD governance kit** (#7255) — both docs-only, open, and being actively iterated. These signal a maturation push toward design consistency and formalized product-development process.

---

## 7. User Feedback Summary

Two real-user pain points surfaced via the `#x-ai-product-feedback` Slack channel (filed as issues #7823 and #7822):

1. **Integration setup failures (Notion, Slack)** — Users report being unable to install or set up popular third-party integrations in their IronClaw environment. These are likely rooted in the sandbox egress auth limitations that PR #7810 is addressing. **Recommendation:** fast-track #7810 and verify Notion/Slack flows in acceptance testing post-merge.

2. **No satisfaction signals captured this cycle** — No positive user feedback, testimonials, or wins were logged in the last 24 hours. Given the other signals, the community is likely in a "waiting for the next stable release" mode.

**Developer-experience feedback (implicit):** The four-track CI expedite program is a direct response to repeated contributor complaints (evidence: "queue-only failure" classes, timezone-dependent tests, toolchain drift between local and CI). This is a strong positive signal that maintainers are listening to contributor friction.

---

## 8. Backlog Watch

**Potentially stale or attention-needing items:**

- **[#7076 — Install the packages the catalog already publishes](https://github.com/nearai/ironclaw/pull/7076)** — This PR was **recently merged** after being three months stale. Good resolution, but the three-month lag suggests contributor-maintainer communication gaps on dependency work.

- **[#7650 — feat(automations): derive run outcomes from runtime evidence](https://github.com/nearai/ironclaw/pull/7650)** — Open since 2026-08-14 (9 days), size XL, low risk, no visible comment activity in the last 24h. This is a foundational reliability improvement; worth a maintainer check to see if it's blocked.

- **[#7749 — Benchmark trigger PR for qa-automation-preview](https://github.com/nearai/ironclaw/pull/7749)** — Opened 2026-08-19 as a deliberately-throwaway PR to trigger a `/benchmark` run. Still open after 4 days; either the benchmark run completed and closure was missed, or it's stuck. **Needs maintainer attention** — this is exactly the kind of housekeeping that should be auto-closed.

- **No issues flagged as needing maintainer response** beyond the above — the triage cadence appears healthy.

---

*Generated 2026-08-23 from IronClaw GitHub activity. All links open to the respective issue/PR pages.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest
**Date: 2026-08-23**

---

## 1. Today's Overview

LobsterAI shows **moderate development activity** for this reporting period. While no new releases were published, the project processed 8 items in the last 24 hours: 2 issues (both closed) and 6 PRs (5 closed/merged, 1 still open). Notably, all but one of the closed items were flagged as **stale**—meaning they were auto-closed after long periods of inactivity (these issues/PRs were originally created in early April but remained unresolved until now). The single **actively-discussed PR** (#2452) addresses a critical bug in provider ID handling for OpenClaw slashed model IDs, indicating ongoing maintenance of the custom model integration surface. Overall, the project appears **stable with low-to-moderate ongoing maintenance**, lacking new feature velocity this cycle.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The most recent version referenced in issue reports is `v2026.3.30`.

---

## 3. Project Progress

The following PRs were **merged or closed** in the last 24 hours (note: all marked "[stale]" indicate they were closed due to inactivity, not necessarily merged this cycle — verify merge status in repository):

| PR | Description | Status |
|---|---|---|
| [#1205](https://github.com/netease-youdao/LobsterAI/pull/1205) | **fix(cowork)** — Show error toast when session rename fails. Previously, rename failures were silently swallowed; now a localized toast appears and the input stays open for retry. | Closed (stale) |
| [#1208](https://github.com/netease-youdao/LobsterAI/pull/1208) | **feat(cowork)** — Added manual retry button for transient errors (429 rate limit, network failures, server errors). Adds new `RETRYABLE_ERROR_KEYS` set to classify retryable errors. | Closed (stale) |
| [#1209](https://github.com/netease-youdao/LobsterAI/pull/1209) | **fix(web-search)** — Blocks unsupported Chrome flags. Fixes issue where `--disable-blink-features=AutomationControlled` was injected externally (via Chrome user data dir, config, or env vars). | Closed (stale) |
| [#1212](https://github.com/netease-youdao/LobsterAI/pull/1212) | **fix(model)** — Increased custom provider limit from 10 to 20 by removing hard-coded `custom_0`–`custom_9` key list in Settings. | Closed (stale) |
| [#1214](https://github.com/netease-youdao/LobsterAI/pull/1214) | **feat(session)** — Added "Export as Markdown" to session detail menu. Generates structured `.md` file with user messages, tool calls, and assistant replies (tool calls truncated at 300 chars). Closes issue #1345. | Closed (stale) |

**Key takeaway:** The most impactful merged work includes **retry UX improvements**, **custom provider limit expansion**, and **markdown export** capability.

---

## 4. Community Hot Topics

Only two issues were active in the last 24h, both with 2 comments each (no upvotes):

| Item | Topic | Comments | Signal |
|---|---|---|---|
| [#1206](https://github.com/netease-youdao/LobsterAI/issues/1206) | **[Bug]** Kimi 2.5 model duplicates progress messages during document analysis — user receives repeated "current action" updates, creating confusion about whether the process is stuck or progressing. Only occurred with Kimi 2.5; switching models resolves it. | 2 | **Moderate.** Recurring behavior bug (reproduction rate: 100% for that task). |
| [#1213](https://github.com/netease-youdao/LobsterAI/issues/1213) | **[Feature Request]** Add "Export as Markdown" for session details — currently only image export is available, making text editing/searching cumbersome. | 2 | **Moderate.** This request was addressed by PR #1214. |

**Underlying needs:** Users want **better transparency** about AI progress (especially with specific models like Kimi 2.5) and **text-based portability** of conversations for documentation and reuse.

---

## 5. Bugs & Stability

| Severity | Bug | Affected Area | Fix Status |
|---|---|---|---|
| **High** | [#1206](https://github.com/netease-youdao/LobsterAI/issues/1206) — Kimi 2.5 duplicates "current action" messages repeatedly during document analysis, making it unclear if the process is executing or stuck. 100% reproducible on specific tasks. | AI model integration / document analysis | **No linked fix PR found.** Issue auto-closed as stale. |
| **Medium** | [#1205](https://github.com/netease-youdao/LobsterAI/pull/1205) — Session rename failures were silently swallowed (user sees no feedback). | Cowork session management | **Fixed** in PR #1205 (toast + keep input open). |
| **Medium** | [#1209](https://github.com/netease-youdao/LobsterAI/pull/1209) — Web-search skill injected unsupported Chrome flags from external sources (residual user-data dirs, env vars), causing issues in Chrome 130+. | Web-search skill / Chrome integration | **Fixed** in PR #1209. |
| **Medium** | [#2452](https://github.com/netease-youdao/LobsterAI/pull/2452) — **[OPEN]** OpenClaw provider prefix lost when model ID contains `/` (e.g., custom_0 + `deepseek-ai/DeepSeek-V4-Flash` stored as only the model ID, causing renderer misconfiguration). | OpenClaw / custom provider | PR open; **needs review/merge.** |

---

## 6. Feature Requests & Roadmap Signals

**Implemented (closed PRs):**
- ✅ **Markdown export for session details** — Implemented in PR #1214 (requested in #1213).
- ✅ **Manual retry button for transient errors** — Implemented in PR #1208 (addresses 429/network/server failures).
- ✅ **Increased custom provider limit to 20** — Implemented in PR #1212.

**Predicted next-version candidates:**
- **Retry UX** (#1208) is a quality-of-life improvement likely to ship in the next minor release.
- **Markdown export** (#1214) is a practical feature likely to appear in the next release given user demand.

**No new feature requests** were filed in the last 24 hours beyond the above.

---

## 7. User Feedback Summary

Real user pain points visible in this cycle:

| Pain Point | Evidence | Sentiment |
|---|---|---|
| **Model-specific behavior inconsistency** — Kimi 2.5 produces redundant progress messages, while other models work normally. Users express confusion about whether errors occurred. | Issue #1206 | **Negative** — experience gap between models erodes trust. |
| **Limited export options** — Image-only export is insufficient for editing/searching conversation logs. Users want Markdown for citing, reorganizing, and sharing. | Issue #1213 | **Positive** — clear actionable request. |
| **Silent failures in UI** — Renaming a session that fails provides no feedback, making users think the action succeeded. | PR #1205 | **Negative** — lack of UI feedback creates uncertainty. |
| **Provider limits blocking workflows** — The 10-custom-provider cap forced users to delete older configs to add new ones. | PR #1212 | **Negative** — constraint on power users. |

**Overall sentiment:** Users appreciate granular features (retry button, export) but are frustrated by **model-specific bugs** and **silent UI failures**.

---

## 8. Backlog Watch

**Items needing maintainer attention:**

| Item | Age | Concern | Recommendation |
|---|---|---|---|
| [#1206](https://github.com/netease-youdao/LobsterAI/issues/1206) — Kimi 2.5 duplicate progress messages | Created 2026-04-01, auto-closed as stale 2026-08-22 (~4.5 months) | No fix PR exists; the bug remains **unresolved** and auto-closed. High severity (100% repro). | **Re-open and prioritize** — confirm if still present in current release; if not, document fix. |
| [#2452](https://github.com/netease-youdao/LobsterAI/pull/2452) — OpenClaw provider prefix loss for slashed model IDs | Open since 2026-08-07 (16 days) | Still open and unmerged. Critical for users of models from providers with `/` in IDs (e.g., DeepSeek-V4). | **Actively review** — a core data-integrity bug for custom providers. |
| [#1213](https://github.com/netease-youdao/LobsterAI/issues/1213) — Markdown export request | Created 2026-04-01, auto-closed as stale | Addressed by PR #1214 (also stale-closed) — **verify merge status** for both; if the PR wasn't merged, re-assess priority. | **Verify merge status** of #1214; if unmerged, push to merge. |

**Watch list:** Auto-stale-closing may have **prematurely closed fix PRs**. Verify merge status of #1205, #1208, #1209, #1212, #1214 — if any were closed without merging, their fixes are lost and issues should be flagged again.

---

*Sources: [LobsterAI GitHub](https://github.com/netease-youdao/LobsterAI)* | *Generated: 2026-08-23*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-23

## 1. Today's Overview
Moltis is in a steady development phase with modest activity: 1 open issue and 3 open pull requests were updated in the last 24 hours, with no merges or releases. The project is actively addressing integration-level stability concerns, particularly around MCP client lifecycle management, OpenAI schema compatibility, and Browserless container versions. The single new issue signals a security-minded feature request, suggesting the maintainers are receptive to hardening the hook system. Overall, the project appears healthy with a focused, contributor-driven pipeline, though the lack of merged PRs means progress is still in review/iteration stages.

---

## 2. Releases
No new releases were published in the last 24 hours. No changelog, breaking changes, or migration notes to report.

---

## 3. Project Progress
No PRs were merged or closed today. Three PRs remain open and under review:

- **PR #1232 — fix(tools): make object schemas OpenAI-safe**  
  Addresses a compatibility issue where OpenAI strict tool schemas (`additionalProperties=false`) were forcing Codex to send null/empty values for patch/map fields. Fixes cron/webhook patch field declarations and MCP environment variable representations.  
  [View PR](https://github.com/moltis-org/moltis/pull/1232)

- **PR #1231 — fix(mcp): resolve current client after server restart**  
  Fixes a bug where MCP tool bridges held stale client references after a server restart, causing active chat turns to dispatch to closed instances. The fix ties each server connection to its current client.  
  [View PR](https://github.com/moltis-org/moltis/pull/1231)

- **PR #1229 — fix(browser): support Browserless v2 containers**  
  Adds full Browserless v2 container-protocol support while preserving v1 defaults, including Base64 launch arguments via websocket query and use of `TIMEOUT`/`CONCURRENT` parameters.  
  [View PR](https://github.com/moltis-org/moltis/pull/1229)

---

## 4. Community Hot Topics
No issues or PRs generated significant comments or reactions in the last 24 hours (all comments count is 0 or undefined). However, the following are the most substantive items:

- **Issue #1230 — [OPEN] feat(hooks): add an opt-in fail-closed error policy for modifying security hooks**  
  Proposes a fail-closed policy for security-boundary hooks so that runtime failures (e.g., shell-hook timeout) do not silently degrade to continuation. This is a security-critical design question that could shape hook behavior defaults in future releases.  
  [View Issue](https://github.com/moltis-org/moltis/issues/1230)

- **PR #1232 — fix(tools): make object schemas OpenAI-safe**  
  While not heavily commented, this touches on interoperability with OpenAI's Codex, which is a high-visibility integration for many users.  
  [View PR](https://github.com/moltis-org/moltis/pull/1232)

---

## 5. Bugs & Stability
Three bug-fix PRs were filed (none merged yet), indicating a focus on stability:

- **Medium severity — Stale MCP client after server restart (PR #1231)**  
  Can cause silent dispatch failures or dropped tool calls during active conversations. A clear fix is proposed and under review.

- **Medium severity — OpenAI strict schema incompatibility (PR #1232)**  
  Causes data loss (null/empty values) when Codex sends tool arguments against strict schemas. Fix is scoped and targeted.

- **Low-Medium severity — Browserless v2 container incompatibility (PR #1229)**  
  Breaking changes in Browserless v2 could cause browser automation failures for users upgrading their Browserless setup. The PR preserves backward compatibility with v1 while adding v2 support.

No user-reported bugs or regressions were filed today.

---

## 6. Feature Requests & Roadmap Signals
One feature request was raised today:

- **Issue #1230 — Fail-closed error policy for security hooks**  
  This is a hardening feature rather than a new capability. It proposes an opt-in policy where hook failures during security-boundary enforcement (e.g., `BeforeToolCall`) result in explicit blocking rather than silent continuation. Given Moltis's positioning as a policy-enforcement agent, this could land in a 0.x minor release (e.g., next minor after a 0.4.x/0.5.x cycle) as a configuration option, especially if security-conscious users adopt it.

No other roadmap signals were observed in the data.

---

## 7. User Feedback Summary
Direct user feedback in the last 24 hours is minimal. However, the issue and PR authors signal the following pain points:

- **Security posture uncertainty (Issue #1230)**: A user (presumably a security-focused integrator) wants hard guarantees that hook failures do not weaken policy enforcement. This reflects broader demand for deterministic, fail-closed behavior in security tooling.
- **Integration friction with OpenAI Codex (PR #1232)**: Users are hitting schema strictness issues when using Moltis with OpenAI's Codex, indicating real-world usage and cross-tool compatibility needs.
- **Upstream dependency churn (PR #1229)**: Browserless v2's API changes are forcing adaptation, showing that Moltis users rely on current third-party services and need timely compatibility patches.

Satisfaction indicators are neutral-to-positive: contributors are actively fixing issues, and no complaints or negative feedback were logged.

---

## 8. Backlog Watch
No issues or PRs in the provided dataset are long-unanswered or lagging. The only open issue (#1230) was created today and already has an active PR pipeline. All three open PRs were also created/updated today, so none are stale.

**No items currently require maintainer attention beyond standard review of the three open PRs.**

---

*Digest generated from Moltis GitHub activity data for 2026-08-23.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-23

## 1. Today's Overview

CoPaw (QwenPaw) is showing moderate activity with 7 issues and 4 PRs updated in the past 24 hours, though no new releases were published. The project maintains a healthy open-development cadence with 6 active issues and 4 open PRs, but zero merged/closed PRs today indicates a consolidation phase rather than active feature shipping. Community engagement remains strong with Chinese-language users actively filing detailed bug reports and feature requests, particularly around UI/UX polish and provider compatibility. The issue tracker reveals a mix of quality-of-life improvements, cross-platform encoding problems, and media-handling edge cases that suggest the project is maturing beyond core functionality into refinement territory. Maintainer responsiveness appears solid, with most issues receiving initial comments within hours of filing.

## 2. Releases

No new releases were published in the last 24 hours. The latest version referenced in issues is **2.1.0** (with a Docker image variant `xk-qwenpaw:v2.1.0f1`), indicating the current stable line remains active and supported.

## 3. Project Progress

No PRs were merged or closed in the last 24 hours. However, four PRs remain open and are actively being reviewed/updated:

- **[#7054](https://github.com/agentscope-ai/QwenPaw/pull/7054) — Chrome remote bridge endpoint support (Under Review)**: Addresses a significant limitation where the Chrome extension could only connect to a same-host QwenPaw server. This PR enables LAN/network browser support, which is critical for multi-device workflows and remote configurations.
- **[#7050](https://github.com/agentscope-ai/QwenPaw/pull/7050) — Per-cron-job model override picker**: Improves cron job flexibility by letting users assign specific models to scheduled tasks rather than silently inheriting the agent's current model.
- **[#6808](https://github.com/agentscope-ai/QwenPaw/pull/6808) — Custom profile markdown file display fix**: Fixes a backend filtering bug that hid custom persona files in the Files workspace UI.
- **[#7214](https://github.com/agentscope-ai/QwenPaw/pull/7214) — Documentation: Access Policy as fifth security layer**: A first-time contributor documentation fix aligning the security features list across README files.

The open PRs span documentation, Chrome/browser integration, scheduling UX, and workspace file display — suggesting the project is actively investing in peripheral UX and integration polish.

## 4. Community Hot Topics

**Most active issue this week:** [#7196](https://github.com/agentscope-ai/QwenPaw/issues/7196) — "一直显示推理过程是严重的视觉干扰" (Always showing reasoning process is a severe visual distraction) with **2 comments** and **1 👍 reaction**. This Chinese-language enhancement request asks for a configurable collapse option for the reasoning/thinking process display during agent work, citing Hermes as a reference implementation. The underlying need is **developer ergonomics**: users monitoring long-running agent tasks want a clean default view with optional deep-dive visibility for debugging.

**Other noteworthy engagement:**
- **[#7216](https://github.com/agentscope-ai/QwenPaw/issues/7216)** — Intermittent character corruption in tool names (l→|) causing ToolNotFoundError, filed by liuyils. This is a correctness bug with high impact potential if reproducible.
- **[#7043](https://github.com/agentscope-ai/QwenPaw/issues/7043)** — Closed enhancement requesting automatic `chcp 65001` execution at startup for UTF-8 compatibility on Chinese Windows systems. The issue received one maintainer comment and is now closed, indicating a resolution or decision was reached.

The community skews heavily toward Chinese-speaking users with strong Windows and tooling automation needs, reflecting the project's regional adoption patterns.

## 5. Bugs & Stability

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **High** | [#7216](https://github.com/agentscope-ai/QwenPaw/issues/7216) | Intermittent character substitution in tool names (l→|) causing `ToolNotFoundError` — could be LLM tokenization or encoding-related corruption | None yet |
| **Medium** | [#7212](https://github.com/agentscope-ai/QwenPaw/issues/7212) | Inlining images with valid byte size but excessive pixel dimensions crashes the request with `MODEL_EXECUTION_ERROR` and terminates the conversation | None yet |
| **Medium** | [#7213](https://github.com/agentscope-ai/QwenPaw/issues/7213) | Conversational output consistently contains meaningless blank lines that persist despite user requests to stop — a UX annoyance rather than functional break | None |
| **Low** | [#7215](https://github.com/agentscope-ai/QwenPaw/issues/7215) | OpenRouter and OpenCode model backends not fully displayed in GUI after being added — UI rendering issue | None |

The image dimension handling bug (#7212) is particularly concerning because it **terminates the conversation entirely** rather than degrading gracefully — a resilience issue for production use. The shell command tool-name corruption (#7216) could be a serious intermittent reliability problem if it reproduces frequently.

## 6. Feature Requests & Roadmap Signals

Several feature requests point toward a roadmap focused on **configuration granularity and user control**:

- **[#7196](https://github.com/agentscope-ai/QwenPaw/issues/7196) (collapse reasoning display)**: High-signal request — likely to be implemented given it's a common UX pattern (Hermes, Claude, etc. all support this). Expect a settings toggle in the next minor release.
- **[#7201](https://github.com/agentscope-ai/QwenPaw/issues/7201) (per-provider media size caps)**: Splits the single `max_inline_media_bytes` cap into independent image/video/audio limits with UI exposure. Strongly aligned with provider-diversity strategy; feature-rich providers will drive this forward.
- **[#7043](https://github.com/agentscope-ai/QwenPaw/issues/7043) (UTF-8 startup option)**: Now **closed** — the fact that it was resolved suggests the project is actively addressing Chinese Windows environment pain points. The outcome (whether a flag was added or documentation fixed) is worth monitoring.
- **[#7054](https://github.com/agentscope-ai/QwenPaw/pull/7054) (remote Chrome bridge)**: Under review — if merged, this opens up LAN/remote browser automation scenarios, a meaningful feature expansion.

**Prediction:** The next minor release will likely include the reasoning collapse toggle, per-provider media caps, and possibly the per-cron model override — all of which address currently open, well-specified requests.

## 7. User Feedback Summary

**Pain points:**
- **Visual clutter and cognitive load**: Users find persistently-expanded reasoning output distracting during normal operation ([#7196](https://github.com/agentscope-ai/QwenPaw/issues/7196)) and dislike meaningless blank lines polluting conversation output ([#7213](https://github.com/agentscope-ai/QwenPaw/issues/7213)).
- **Windows UTF-8 environment friction**: Chinese Windows users face encoding configuration challenges that are hard to resolve without profile loading changes ([#7043](https://github.com/agentscope-ai/QwenPaw/issues/7043) — now closed).
- **Provider compatibility friction**: Multiple providers (OpenRouter, OpenCode) don't render properly in the GUI ([#7215](https://github.com/agentscope-ai/QwenPaw/issues/7215)), and media payloads fail at provider-specific pixel limits rather than being pre-processed ([#7212](https://github.com/agentscope-ai/QwenPaw/issues/7212)).

**Satisfaction signals:**
- Users continue to use the tool for real work and invest time filing **detailed, reproduction-quality bug reports** with screenshots and version numbers — a sign of committed user base.
- First-time contributors are submitting PRs across docs, Chrome integration, and console UI, indicating good community health and a low barrier to contribution.

## 8. Backlog Watch

| Issue/PR | Days Since Update | Concern |
|----------|-------------------|---------|
| [#6808](https://github.com/agentscope-ai/QwenPaw/pull/6808) — Custom profile markdown display fix (first-time contributor) | 16 days | Long-open first-time contributor PR — risk of contributor discouragement; needs maintainer attention or guidance |
| [#7050](https://github.com/agentscope-ai/QwenPaw/pull/7050) — Per-cron model override (first-time contributor) | 8 days | Similar risk; under-contribution PRs sitting for over a week need a maintainer response |
| [#7043](https://github.com/agentscope-ai/QwenPaw/issues/7043) — UTF-8 startup (closed) | Closed, but resolution outcome unclear | Recommend verifying whether the fix was a **code change** or just **documentation** — users need code-level relief |

**Maintainer action items:**
1. Acknowledge and review the two older first-time contributor PRs (#6808, #7050) to prevent contributor churn.
2. Follow up on #7216 (tool name corruption) — if reproducible, this is a high-severity correctness issue.
3. Consider adding a graceful degradation path for #7212 to prevent conversation termination on media errors.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-23

## 1. Today's Overview

ZeroClaw shows a dynamic and mature project with high sustained activity: **50 issues and 50 PRs updated in the last 24 hours**, with 43 open issues actively discussed. The project is in a deep architectural refinement phase, evidenced by multiple open RFCs targeting core boundaries (conversation sessions, memory lifecycle, wire protocol). A significant portion of activity is concentrated on **Windows test parity fixes (74 failures)** and **security policy sandboxing**, which remain top priorities. Three PRs were merged/closed in the last day, while the large number of open PRs (47) suggests a substantial review backlog. The absence of new releases in the last 24 hours aligns with this being a period of concentrated development and design discussion rather than stabilization.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release remains v0.8.3, which is still affected by the `config init` bug (see Bugs & Stability section).

## 3. Project Progress

Three PRs were merged/closed in the last 24 hours. The notable merged items reflect fixes to security documentation and runtime hardening:

- **[PR #9203 - fix(sop): wire authenticated HTTP fan-in](https://github.com/zeroclaw-labs/zeroclaw/pull/9203)** (CLOSED, size:XL) — Adds `POST /sop/{*rest}` fan-in for webhook triggers and dispatches through the daemon-owned SOP engine, with proper 404 handling when no match is found. This is a substantial security improvement for authenticated SOP workflows.
- **[Issue #9255 - WASM plugin calls have no wall-clock timeout](https://github.com/zeroclaw-labs/zeroclaw/issues/9255)** (CLOSED, priority:p1) — A high-priority security bug was resolved, addressing unbounded plugin execution via `WasmTool::execute`. This closes a potential denial-of-service vector.
- **[Issue #9640 - WhatsApp Web policy doc comments cite `allowed_numbers`, a V2 key with no V3 field](https://github.com/zeroclaw-labs/zeroclaw/issues/9640)** (CLOSED) — Documentation bug fix preventing operator confusion with non-existent config keys.

Notably, the Windows test failure issue (#7462) remains open, indicating that the substantial fix effort (19 comments, 74 failing tests) is still in progress.

## 4. Community Hot Topics

The most active discussions reflect debate on architectural direction and long-standing pain points:

1. **RFC #9487 — Runtime-owned conversation sessions and transport surface adapters** (24 comments, 0 reactions) — The highest-engagement issue this week. The RFC has been revised twice (2026-07-28 → 2026-08-03) and proposes ratifying ownership boundaries for sessions, migrating entry points to `InboundAction`, and adding durable admission semantics. This is a foundational architecture change with high risk that will shape future development.

2. **[Issue #7462 — 74 test failures on Windows](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)** (19 comments) — The Windows parity issue continues to be a top community concern. The failures span Unix-only test commands, path semantics, and console encoding (code page 936). This is a systemic developer-experience issue for Windows contributors and users.

3. **[Issue #6850 — RFC: Decouple memory lifecycle policy from storage backends](https://github.com/zeroclaw-labs/zeroclaw/issues/6850)** (15 comments) — Proposes a clear boundary between durable memory storage and lifecycle/consolidation policy, addressing architecture debt that forces reimplementation across gateways and channels. This indicates growing complexity in the memory subsystem.

4. **[Issue #8780 — RFC: Realtime speech-to-speech channel for Gemini Live](https://github.com/zeroclaw-labs/zeroclaw/issues/8780)** (15 comments) — Revised to a "broker contract" where the realtime voice host owns audio processing and ZeroClaw remains the LLM/agent brain. This reflects strong community interest in voice interfaces and is closely tied to the in-progress `voicehost` channel (#7943).

5. **[Issue #8692 — Maintainer decision queue tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)** (13 comments) — Community members are actively tracking the maintainer decision backlog, indicating concern about RFC processing velocity.

## 5. Bugs & Stability

Multiple bug reports were updated in the last 24 hours, ordered by severity:

**High Severity (P1)**

- **[Issue #10164 — `block_high_risk_commands = false` is not honored — allowlisted high-risk command still blocked on the parent path](https://github.com/zeroclaw-labs/zeroclaw/issues/10164)** (P1, risk:high) — Critical security policy bypass where configuration to allow `rm` with a user-approved allowlist is hard-blocked. Affects agent direct-turn paths. No linked fix PR yet.
- **[Issue #10251 — 17 telegram listen_* tests assert on wall-clock timeouts, failing on loaded runners](https://github.com/zeroclaw-labs/zeroclaw/issues/10251)** (P1, risk:high) — CI flakiness, same defect class as #9429. Creates unreliable CI signals.
- **[Issue #9946 — agent-browser subprocess waits are unbounded in availability probe and run_command](https://github.com/zeroclaw-labs/zeroclaw/issues/9946)** (P1, risk:high) — Wedged CLI hangs agent turns indefinitely (same class as #8560). A fix was closed for WASM (#9255), but the browser tool remains vulnerable.
- **[Issue #9718 — Telegram channel delivers duplicate messages when model emits both tool_call and content](https://github.com/zeroclaw-labs/zeroclaw/issues/9718)** (P1, risk:high) — Defensive handling needed for dual-response LLM output.

**Medium Severity (P2)**

- **[Issue #10232 — Daemon diagnostics drop the underlying error chain](https://github.com/zeroclaw-labs/zeroclaw/issues/10232)** — `anyhow` context strings lose the original cause, complicating debugging.
- **[Issue #9001 — Provider turn failures bury cause-specific diagnostics under a generic retry envelope](https://github.com/zeroclaw-labs/zeroclaw/issues/9001)** — Diagnostics for LM Studio, Ollama, and other providers are obscured.
- **[Issue #9590 — Concurrent models refresh runs can lose cache entries](https://github.com/zeroclaw-labs/zeroclaw/issues/9590)** — Read-modify-write race condition in cache updates.
- **[Issue #9708 — Bound service launcher stdout and stderr logs](https://github.com/zeroclaw-labs/zeroclaw/issues/9708)** — Unbounded log file growth.
- **[Issue #9436 (CLOSED) — `config init` writes template sections that fail the strict loader](https://github.com/zeroclaw-labs/zeroclaw/issues/9436)** — Fresh configs were born degraded; `config migrate` exited 1. This is closed, but a related fix PR #9281 exists.

**Windows Test Issue**
- **[Issue #7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)** — 74 test failures, P1. Fix is in progress; while CI doesn't run Windows, the community impact is clear.

**Fixed/Uplifted in the period:**
- **Issue #9255 (WASM timeout)** — Closed. PR likely merged, bounding plugin execution.

## 6. Feature Requests & Roadmap Signals

Several active feature requests signal strong direction for v0.9.0 and beyond:

**Architectural RFCs in decision queue (likely v0.9.0+):**
- **#9487 — Runtime-owned conversation sessions** (High activity, multiple revisions) — Likely a v0.10.0 feature given scale.
- **#6850 — Decouple memory lifecycle from storage** — Part of the memory architecture overhaul.
- **#8396 — Wire protocol first-class in provider construction** — Significant for multi-provider onboarding.
- **#10050 — Verbatim channel send over gateway without agent turn** — Simple but high-impact API addition.
- **#6996 — Granular sandbox policy (filesystem/network)** — In progress, with PR #7821 advancing it.

**Pragmatic features with PRs in flight:**
- **#7943 — Realtime voice-host channel** (in-progress) + **#8780 Gemini Live RFC** — Voice is a clear roadmap focus.
- **#8850 — Move optional channels/tools to runtime WASM plugins** — Aligns with plugin ecosystem investment.
- **#5607 — Deterministic precondition gates for cron jobs** (accepted) — Lower complexity, likely lands in v0.9.0.
- **#9945 — Browser tool exposing only 16 of 100+ agent-browser commands** (blocked) — Unlocks much richer browser automation.
- **#7790 — Bring remaining web dashboard operator surfaces into zerocode** (accepted) — TUI parity as a differentiator.

## 7. User Feedback Summary

Users are **productively engaged** but express frustration on several friction points:

- **Session management pain**: **[Issue #10141 — "Please make sessions usable"](https://github.com/zeroclaw-labs/zeroclaw/issues/10141)** is explicit: "It's quite frustrating to get into previous session." The user can't copy referenced snippets easily, and session navigation is awkward. This is a UX win if addressed in v0.9.0.
- **Windows is a second-class citizen**: The 19-comment thread on #7462 (code page 936, Unix-only commands) suggests a meaningful cohort of Windows users/contributors whose experience is degraded.
- **Sandbox configuration is confusing**: Issue #10164 shows that documented config (`block_high_risk_commands = false` + `allowed_commands`) does not work as expected — a factual betrayal of user trust.
- **Reliability expectations**: Multiple issues about timeouts (#9320 cron, #9946 browser, #9255 WASM) show users hitting hangs. The project is actively fixing these, which is positive.
- **High appreciation for RFC/architecture transparency**: The intense engagement on the RFC tracker (#8692) and RFC threads suggests users value the open design process.

## 8. Backlog Watch

Issues and PRs that have been open for extended periods and need maintainer attention:

- **[Issue #7462 — 74 Windows test failures](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)** (since 2026-06-10, P1) — **Critical backlog item.** 19 comments, high severity, still open. Needs a maintainer to assign/review a Windows-enabling PR.
- **[Issue #6850 — RFC: Decouple memory lifecycle from storage](https://github.com/zeroclaw-labs/zeroclaw/issues/6850)** (since 2026-05-22) — 15 comments, no maintainer decision (needs-maintainer-review). Related to #9103 (same area).
- **[Issue #6996 — Granular sandbox policy RFC](https://github.com/zeroclaw-labs/zeroclaw/issues/6996)** (since 2026-05-28) — 11 comments, status `needs-author-action`. The associated PR #7821 is also pending — both are waiting on each other.
- **[Issue #8396 — Wire protocol first-class in provider construction](https://github.com/zeroclaw-labs/zeroclaw/issues/8396)** (since 2026-06-27) — 9 comments, needs-maintainer-review.
- **[Issue #8692 — Maintainer decision queue tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)** (since 2026-07-04) — The project itself acknowledges the queue is long; 13 comments just to maintain it.
- **[PR #7821 — feat(security): canonical sandbox_policy schema](https://github.com/zeroclaw-labs/zeroclaw/pull/7821)** (since 2026-06-17, size:XL) — Labelled `needs-author-action` for over two months. Risk:high means it's consequential, but it's also blocking #6996.

**Overall health assessment**: ZeroClaw is in an intense, healthy development cycle. The volume of RFCs is high but the maintainer decision queue (#8692) suggests throughput isn't keeping up with community input velocity, particularly for high-comment RFCs. The **backlog of 47 open PRs** is a concern for review latency. The project's strongest signals this week are its proactive security fixes (closing WASM unbound timeouts) and a clear roadmap for voice interfaces, which will broaden its appeal.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*