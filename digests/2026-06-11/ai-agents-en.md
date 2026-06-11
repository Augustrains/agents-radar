# OpenClaw Ecosystem Digest 2026-06-11

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-11 02:14 UTC

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

# OpenClaw Project Digest — 2026-06-11

Generated from GitHub data: 500 updated issues, 500 updated PRs, 1 new release

---

## Today's Overview

OpenClaw shows **very high activity** with 500 issues and 500 pull requests updated in the last 24 hours, indicating a large and engaged community alongside significant maintainer throughput. Of the updated issues, **469 remain open/active** with only 31 closed, suggesting a heavy triage backlog despite active development. The PR pipeline shows **101 merged/closed** against 399 still open, reflecting steady integration work. A single new beta release (v2026.6.6-beta.1) shipped today with major security hardening. The project continues to grapple with systemic challenges around session state integrity, message delivery reliability, and multi-channel communication correctness, while community demand for security controls and configuration flexibility remains high.

---

## Releases

### v2026.6.6-beta.1 — OpenClaw 2026.6.6-beta.1

**Highlights:** Substantially tightened security boundaries across multiple attack surfaces:
- Transcript sandbox binds
- Host environment inheritance
- MCP stdio handling
- Codex HTTP access controls
- Native search policy enforcement
- Elevated sender checks
- Deleted-agent ACP bypass prevention
- Loopback tool restrictions
- Discord moderation hardening
- Teams group access controls

**Breaking changes:** Not explicitly detailed, but security boundary tightening may break existing configurations that relied on permissive defaults.

**Migration notes:** Users running self-hosted or exposed gateways should review their sandbox and host environment configurations after update.

[View Release](openclaw/openclaw)

---

## Project Progress

**101 PRs merged/closed today** — strong integration velocity. Key progress areas:

| Area | Progress |
|------|----------|
| **CLI & Runner** | PR [#91974](openclaw/openclaw/pull/91974) scopes Claude CLI queue to live-session owner identity, enabling concurrent independent sessions on shared workspaces |
| **Web UI** | PR [#92063](openclaw/openclaw/pull/92063) fixes duplicate assistant groups during segmented streaming replies |
| **Web Fetch** | PR [#91950](openclaw/openclaw/pull/91950) sanitizes URL whitespace from LLM tool call arguments |
| **Git Updates** | PR [#91296](openclaw/openclaw/pull/91296) routes supervised git-source updates through detached handoff path |
| **Session Recovery** | PR [#79910](openclaw/openclaw/pull/79910) adds recovery from stale temp artifacts in session store |
| **Plugin Config** | PR [#90167](openclaw/openclaw/pull/90167) resolves environment variable placeholders in plugin configs at runtime |

---

## Community Hot Topics

### 🔥 Most Active Issues

| Issue | Comments | Type | Summary |
|-------|----------|------|---------|
| [#25592](openclaw/openclaw/issues/25592) — **Diamond Lobster** | 31 | Bug | Text between tool calls leaks to messaging channels (Slack, iMessage, etc.) — **UX emergency** |
| [#44925](openclaw/openclaw/issues/44925) — **Diamond Lobster** | 19 | Bug | Subagent completion silently lost — no retry, no notification, no auto-restart on timeout |
| [#88838](openclaw/openclaw/issues/88838) — **Diamond Lobster, P0** | 19 | Tracker | Track core session/transcript SQLite migration via accessor seam — **maintainer-driven initiative** |
| [#32473](openclaw/openclaw/issues/32473) — **Diamond Lobster** | 17 | Regression | Control UI requires device identity (HTTPS/localhost) — blocks VPS/Docker users |
| [#22438](openclaw/openclaw/issues/22438) — **Diamond Lobster** | 17 | Feature | Tiered bootstrap file loading to conserve token budget |
| [#22676](openclaw/openclaw/issues/22676) — **Diamond Lobster** | 17 | Bug | Signal daemon race condition on SIGUSR1 restart — orphaned processes |

### 🔥 Notable by Reactions

| Issue | 👍 | Summary |
|-------|----|---------|
| [#18160](openclaw/openclaw/issues/18160) — Direct Exec Mode for Cron Jobs | 10 | Strong demand for non-LLM cron job execution to reduce costs and latency |
| [#39604](openclaw/openclaw/issues/39604) — Private network access for web_fetch | 9 | Enterprise users need opt-in internal network access |
| [#79077](openclaw/openclaw/issues/79077) — Telegram guest bots + bot-to-bot | 7 | Community eager for new Telegram platform features |

**Analysis:** The top issues reveal a **core reliability crisis** — tool-call text leaking to public channels, subagent completions going missing, and session context confusion are undermining trust in the agent's ability to operate without human supervision. Users are demanding **deterministic guarantees** (hard enforcement hooks, append-only file modes, tiered bootstrap loading) over probabilistic LLM behavior.

---

## Bugs & Stability

### 🔴 Critical (P0–P1, Diamond Lobster)

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| [#88838](openclaw/openclaw/issues/88838) | **P0** | Core session/transcript SQLite migration tracking — foundational architecture issue | No (tracker issue) |
| [#25592](openclaw/openclaw/issues/25592) | **P1** | Tool-call text leaks to messaging channels — **security + UX** | No |
| [#44925](openclaw/openclaw/issues/44925) | **P1** | Subagent completion silently lost — **data loss** | No |
| [#22676](openclaw/openclaw/issues/22676) | **P1** | Signal daemon race condition — **crash loop + orphaned processes** | No |
| [#32296](openclaw/openclaw/issues/32296) | **P1** | Agent replies to previous message — **session context confusion** | No |
| [#31583](openclaw/openclaw/issues/31583) | **P1** | `exec` tool ignores `skills.entries.*.env` — **regression, security** | No |
| [#32473](openclaw/openclaw/issues/32473) | **P2** | Control UI requires HTTPS — **blocks Docker/VPS users** | No |
| [#29387](openclaw/openclaw/issues/29387) | **P1** | Bootstrap files in agentDir silently ignored | No |
| [#44905](openclaw/openclaw/issues/44905) | **P1** | Discord leaks internal tool-call traces (NO_REPLY, JSON args) — **security** | No |
| [#83184](openclaw/openclaw/issues/83184) | **P1** | Heartbeat-driven replies get stuck — **blocks subsequent heartbeats** | No |

### 🟠 Notable Regressions

| Issue | Description |
|-------|-------------|
| [#38327](openclaw/openclaw/issues/38327) | "Cannot convert undefined or null to object" in v2026.3.2 with Google Vertex/Gemini |
| [#40540](openclaw/openclaw/issues/40540) | `openclaw update` fails with EBUSY on Windows |
| [#38439](openclaw/openclaw/issues/38439) | Avatar endpoint returns 404 — broken in webchat UI |

### 🟡 Active Fix PRs

| PR | Fixes | Status |
|----|-------|--------|
| [#91057](openclaw/openclaw/pull/91057) | Stale gateway model-run session pruning | 👀 Ready for maintainer |
| [#91974](openclaw/openclaw/pull/91974) | Claude CLI queue scoping | 📣 Needs proof |
| [#92063](openclaw/openclaw/pull/92063) | Duplicate assistant groups in UI | Open |
| [#79799](openclaw/openclaw/pull/79799) | Session store recovery from temp artifacts | ⏳ Waiting on author |

**Key takeaway:** The bug landscape reveals **systemic reliability failures** in session management, message routing, and subagent orchestration. The volume of P1 security issues (tool-call leaks, Discord trace exposure, env variable inheritance) suggests the v2026.6.6 security tightening was necessary but may not have addressed the full surface area.

---

## Feature Requests & Roadmap Signals

### High-Community-Demand Features

| Issue | Support | Description | Likely Next Version? |
|-------|---------|-------------|---------------------|
| [#18160](openclaw/openclaw/issues/18160) — Direct Exec Mode for Cron Jobs | 10 👍 | Bypass LLM for simple cron commands — reduce cost, increase reliability | **Likely** — fixes critical UX pain |
| [#39604](openclaw/openclaw/issues/39604) — Private network access for web_fetch | 9 👍 | Opt-in `allowPrivateNetwork` config | **Likely** — low risk, high value |
| [#79077](openclaw/openclaw/issues/79077) — Telegram guest bots + bot-to-bot | 7 👍 | New Telegram platform features | **Possible** — external dependency |
| [#42840](openclaw/openclaw/issues/42840) — MathJax/LaTeX in Control UI | 6 👍 | Display mathematical formulas | **Possible** — UI enhancement |
| [#37634](openclaw/openclaw/issues/37634) — Keep isolated sandbox workspaces writable | 6 👍 | `workspaceAccess: "none"` should still allow writing | **Likely** — bug-like behavior |

### Strategic Roadmap Signals

1. **Multi-Agent Orchestration** (Issues [#35203](openclaw/openclaw/issues/35203), [#43367](openclaw/openclaw/issues/43367), [#22358](openclaw/openclaw/issues/22358)) — Capability profiling, shared blackboards, layered memory, and cost governance are being RFC'd. This is the **next frontier** for OpenClaw but remains unstable.

2. **Session/Transcript SQLite Migration** ([#88838](openclaw/openclaw/issues/88838)) — A **P0 maintainer-driven initiative** to replace JSON session storage with SQLite. This is foundational and will unblock many session-state bugs.

3. **Hard Enforcement Hooks** ([#13583](openclaw/openclaw/issues/13583), [#39979](openclaw/openclaw/issues/39979)) — Users increasingly want **mandatory tool-call gates** and **path-scoped RWX permissions** to move beyond soft prompt-based rules.

4. **Dynamic Model Discovery** ([#10687](openclaw/openclaw/issues/10687)) — Static model catalogs are insufficient for fast-moving providers (OpenRouter). This is a **medium-term priority**.

**Prediction:** The next minor release (v2026.6.x) will likely include Direct Exec Mode for cron jobs, private network opt-in for web_fetch, and the first PRs from the SQLite migration seam. The security tightening in v2026.6.6-beta.1 suggests a **security-focused release cycle**.

---

## User Feedback Summary

### Major Pain Points

1. **Message leakage** — Internal processing text reaching public channels is the #1 complaint. Users cannot trust the agent to operate autonomously.
2. **Silent failures** — Subagent completions, heartbeat replies, and cron jobs fail without notification. "It just stops working" is a recurring theme.
3. **Session confusion** — Agent replies to wrong messages, loses context, or gets stuck on old state. Multi-turn conversations degrade over time.
4. **Docker/VPS hostility** — HTTPS requirement for control UI blocks self-hosted users. Sandbox workspace mounts broken in Docker-outside-of-Docker setups.
5. **Windows-specific breakage** — `openclaw update` EBUSY, missing tool environment inheritance — Windows remains a second-class platform.

### Satisfaction Signals

- **Telegram support** is evolving rapidly with guest bot and bot-to-bot support requested
- **Plugin ecosystem** is maturing — memory-wiki, workboard, and active-memory plugins show real adoption
- **Security focus** in v2026.6.6-beta.1 is welcomed — users want tighter controls
- **Backup/restore utilities** ([#13616](openclaw/openclaw/issues/13616), [#40786](openclaw/openclaw/issues/40786)) show a mature user base concerned with disaster recovery

### Dissatisfaction Patterns

> "The agent promises follow-ups but doesn't start them" — [#58450](openclaw/openclaw/issues/58450)
> "I can't use the browser tool without a PhD in CSS selectors" — [#44431](openclaw/openclaw/issues/44431)
> "Setting up memory is never mentioned in onboarding, but it's the most important feature" — [#16670](openclaw/openclaw/issues/16670)

---

## Backlog Watch

### Long-Unanswered, High-Importance Issues

| Issue | Age | Maintainer Tags | Why It Matters |
|-------|-----|-----------------|----------------|
| [#88838](openclaw/openclaw/issues/88838) — SQLite migration tracker | 10 days | `maintainer` | P0 foundational architecture change — **actively tracked but no PRs yet** |
| [#10687](openclaw/openclaw/issues/10687) — Dynamic model discovery | 4 months | `maintainer`, `P2` | Blocks users from using fast-moving providers; upstream catalog is stale |
| [#13583](openclaw/openclaw/issues/13583) — Pre-response enforcement hooks | 4 months | `needs-maintainer-review` | Critical for high-stakes workflows (finance, security) |
| [#11665](openclaw/openclaw/issues/11665) — Webhook multi-turn support | 4 months | `needs-product-decision` | Documented feature that doesn't work — **misleading docs** |
| [#16670](openclaw/openclaw/issues/16670) — Memory setup in onboarding | 4 months | `needs-product-decision` | New users miss the most important feature |
| [#29387](openclaw/openclaw/issues/29387) — Bootstrap files in agentDir ignored | 3.5 months | `needs-maintainer-review`, `needs-product-decision` | Per-agent configuration is broken |
| [#41165](openclaw/openclaw/issues/41165) — Telegram DMs pollute main session | 3 months | `needs-product-decision` | Privacy violation — DMs should be isolated |

### PRs Needing Maintainer Review

| PR | Age | Merge Risk |
|----|-----|------------|
| [#91976](openclaw/openclaw/pull/91976) — Durable inter-tool commentary | 1 day | 🚨 compatibility, message-delivery |
| [#91057](openclaw/openclaw/pull/91057) — Stale session pruning | 4 days | 🚨 compatibility, session-state |
| [#87697](openclaw/openclaw/pull/87697) — Clear stale provider cooldowns | 14 days | 🚨 compatibility, auth-provider, session-state |
| [#80681](openclaw/openclaw/pull/80681) — Trajectory event byte cap override | 31 days | 🚨 compatibility |

**Critical observation:** 7 of the top 20 issues have been open for **3+ months** with `needs-product-decision` or `needs-maintainer-review` tags. This suggests a **product governance bottleneck** — maintainers are active on code but slow to make architectural decisions, leaving foundational issues (bootstrap file loading, webhook multi-turn, per-agent configuration) unresolved for months.

---

## Summary Assessment

**Project Health: 🟡 Yellow — High activity, but systemic instability**

OpenClaw has an **extraordinarily active community** and a development team shipping code daily, but the project is struggling with **reliability debt**. The top issues cluster around session state corruption, message delivery failures, and security boundaries — all symptoms of an architecture that evolved rapidly without sufficient investment in foundational guarantees.

The v2026.6.6-beta.1 security tightening is a positive signal, but users are clear: they need **deterministic behavior** (hard enforcement hooks, append-only file modes, proper error propagation), not just prompt engineering.

**What to watch:**
- The SQLite migration tracker ([#88838](openclaw/openclaw/issues/88838)) — success here could solve half the session-state bugs
- The product decision backlog — if maintainers don't resolve 3+ month-old architecture issues, community trust may erode
- Direct Exec Mode for cron jobs — if shipped, it signals the maintainers are listening to the #1 cost/reliability complaint

---

## Cross-Ecosystem Comparison

## Cross-Project Comparison Report — AI Agent Open-Source Ecosystem
**Date:** 2026-06-11

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing **unprecedented activity**, with seven major projects collectively processing over **1,700+ issues and 700+ pull requests** updated in the last 24 hours. The landscape is bifurcating between **general-purpose agent frameworks** (OpenClaw, Hermes Agent, ZeroClaw) and **vertically-integrated assistant experiences** (NanoBot, CoPaw, LobsterAI). A clear theme is the tension between **rapid feature velocity** and **systemic reliability debt** — several projects are shipping daily while accumulating critical bugs around session state, message delivery, and security boundaries. The ecosystem is also seeing a **shift toward multi-agent orchestration** (OpenClaw, ZeroClaw, PicoClaw) and **runtime architecture migration** (IronClaw, CoPaw) as foundational design decisions from 2025 are being revisited.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status | Health Score |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | v2026.6.6-beta.1 | 🟡 Yellow |
| **ZeroClaw** | 42 | 50 | Stable (no release today) | 🟡 Yellow |
| **CoPaw** | 36 | 49 | v1.1.11 stable | 🟢 Good |
| **Hermes Agent** | 50 | 50 | v0.16.0 (no release today) | 🟡 Yellow |
| **NanoBot** | 10 | 34 | v0.2.1 (v0.2.2 imminent) | 🟢 Very Good |
| **IronClaw** | 50 | 50 | v0.24.0 (crates.io), v0.27.0 (tagged) | 🟡 Yellow |
| **PicoClaw** | 5 | 15 | v0.2.9-nightly | 🟢 Healthy |
| **NanoClaw** | 2 | 12 | No release today | 🟢 Good |
| **LobsterAI** | 0 | 23 | v2026.6.10 | 🟢 Good |
| **Moltis** | 1 | 0 | No release today | 🟢 Quiet/Stable |
| **TinyClaw** | 0 | 0 | No activity | ⚪ Inactive |
| **ZeptoClaw** | 0 | 0 | No activity | ⚪ Inactive |
| **NullClaw** | 0 | 4 | No release today | 🟢 Clean |

**Key observations:**
- **OpenClaw dominates raw volume** (500 issues, 500 PRs) but carries significant reliability debt
- **CoPaw and NanoBot** show best health-to-velocity ratios — merging fixes within 24 hours
- **Hermes Agent and IronClaw** have high issue counts suggesting active community but potential triage bottlenecks
- **NullClaw and Moltis** are low-activity but clean — no technical debt accumulation
- **TinyClaw and ZeptoClaw** are effectively dormant

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale of community:** 500 issues/PRs updated daily dwarfs all competitors (next closest: Hermes/ZeroClaw at ~50 each). This indicates the largest developer mindshare and install base.
- **Feature surface breadth:** Multi-channel (Slack, Telegram, Discord, Teams), MCP integration, Codex HTTP, subagent orchestration — more completeness than any single competitor.
- **Plugin ecosystem maturity:** Reference implementation with tools like memory-wiki, workboard, active-memory showing real adoption.

**Technical approach differences:**
- **Security-first architecture:** v2026.6.6-beta.1 introduced substantial sandboxing, host environment inheritance controls, and loopback restrictions — more aggressive than peers. CoPaw and NanoBot have tool guards but fewer transport-layer controls.
- **Session state model:** JSON-based session store with planned SQLite migration — currently more fragile than NanoBot's session-scoped history or IronClaw's Reborn event-driven architecture.
- **Subagent model:** Deeply integrated but unreliable (silent failures, lost completions). ZeroClaw's RFC #7415 to unify turn engines suggests the entire ecosystem is struggling with this.

**Community size comparison:**
OpenClaw's engagement is likely **5-10x** the next largest project. However, this scale comes with downsides: 469 open issues, 399 open PRs, and a 31-closed/101-merged ratio suggests maintainers are overwhelmed compared to projects like NanoBot (10 issues, 34 PRs, 19 merged) which clear PRs more efficiently.

---

## 4. Shared Technical Focus Areas

| Requirement | Affected Projects | Specific Needs |
|---|---|---|
| **Message delivery reliability** | OpenClaw, Hermes Agent, PicoClaw, ZeroClaw | Tool-call text leaking to channels, duplicate messages, silent delivery failures |
| **Session state integrity** | OpenClaw, NanoBot, ZeroClaw, IronClaw | Context pollution between sessions, lost messages, stale artifacts |
| **Multi-agent/subagent orchestration** | OpenClaw, ZeroClaw, PicoClaw, NanoBot, CoPaw | Silent subagent failures, missing retry logic, no progress visibility |
| **Security boundary hardening** | OpenClaw, CoPaw, NanoClaw, ZeroClaw | SSRF bypasses, credential leaks, host network access control |
| **Provider/model configuration** | IronClaw, Hermes Agent, ZeroClaw, CoPaw | Broken fallback logic, credential pool mismanagement, empty responses |
| **Windows/macOS platform parity** | OpenClaw, CoPaw, LobsterAI, ZeroClaw | EBUSY updates, SSL cert failures, installer issues, path separator bugs |
| **Docker/VPS deployment** | OpenClaw, Hermes Agent, ZeroClaw, NanoClaw | HTTPS requirement for UIs, egress lockdown side effects, permission models |
| **Deterministic tool execution** | OpenClaw, NanoBot, CoPaw | Hard enforcement hooks, pre-response gating, append-only file modes |
| **CI/build pipeline stability** | CoPaw, ZeroClaw | SSL certificate corruption in builds, dependency regressions |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | CoPaw | ZeroClaw | IronClaw | Hermes Agent |
|---|---|---|---|---|---|---|
| **Primary user** | Advanced developers, self-hosters | Technical users, production schedulers | Chinese-speaking enterprise, Qwen users | Multi-cloud, multi-agent | NEAR AI ecosystem, Rust-centric | Desktop app users, Docker operators |
| **UI sophistication** | Web UI with Control, TUI | WebUI, Slack, Telegram | Tauri Desktop + Web | TUI-heavy | Reborn WebUI v2 (in progress) | Dashboard + Desktop |
| **Architecture** | Monolith + plugins | Modular Python | AgentScope-based | Runtime engine (Rust?) | Rust crate-based | Rust core + Python plugins |
| **Channel support** | ⭐ Broadest (Slack, Telegram, Discord, Teams, iMessage, SMS) | Slack, Telegram, Feishu | DingTalk, WeChat, Web | Telegram, Discord, WhatsApp | Slack, NEAR AI WebChat | Docker gateway, Telegram |
| **Model diversity** | Broad (OpenAI, Anthropic, Gemini, OpenRouter) | OpenAI, DeepSeek, local models | Qwen, DeepSeek, local | Qwen3.5, OpenAI, custom | NEAR AI, OpenAI, Anthropic | OpenAI, Kimi, Anthropic |
| **Enterprise readiness** | Medium (security tightening, plugin guard) | Low-Medium (fragile cron) | Medium-High (File Guard, Tool Guard, per-agent accounts) | Medium (config filtering, RFCs for plugin system) | Medium (MCP, auth-gate resume) | Low (Docker fragility, macOS instability) |
| **Release cadence** | Beta every ~2-3 days | Patch imminent (v0.2.2) | Stable releases, frequent patches | Between releases | Blocked (crates.io gap) | Post-v0.16.0, stabilization |
| **Language** | TypeScript/Node | Python | Python | Rust | Rust | Rust + Python |

**Key differentiation patterns:**
- **CoPaw** leads in Chinese-market enterprise features (DingTalk, WeChat, Qwen)
- **IronClaw** is architecturally most ambitious (Reborn migration, Rust crate ecosystem) but currently blocked on distribution
- **NanoBot** is the fastest-responding project — bugs fixed within 24 hours
- **ZeroClaw** is investing in future architecture (plugin system, turn engine unification) but shipping less now
- **OpenClaw** has the greatest breadth but the deepest reliability debt

---

## 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating (High risk/reward)**
- **OpenClaw** — Maximum activity, maximum reliability debt. Shipping features faster than stabilizing them.
- **ZeroClaw** — Heavy RFC activity, critical bug fixes in progress. Preparing for v0.8.x.
- **Hermes Agent** — High bug report volume, P1 fixes in progress. In "crunch mode" after v0.16.0.

**Tier 2: Stabilizing (Good velocity, improving quality)**
- **CoPaw** — v1.1.11 released, strong health score. AgentScope 2.0 migration on the horizon.
- **NanoBot** — Best PR-to-bug-fix ratio. v0.2.2 imminent with well-targeted fixes.
- **LobsterAI** — Consolidating after v2026.6.10. "Computer Use MVP" queued for next release.

**Tier 3: Maintenance Phase**
- **PicoClaw** — Moderate activity, focused on security patches and type safety.
- **NanoClaw** — Steady skill ecosystem growth, corporate PRs (microsoft/amplifier-app sibling).

**Tier 4: Quiet / Stalled**
- **NullClaw** — Low community engagement but clean maintenance.
- **Moltis** — Single bug report, no development activity.
- **TinyClaw, ZeptoClaw** — Dormant.

**Maturity signal:** CoPaw and NanoBot show the healthiest lifecycle — actively merging community PRs while maintaining low open issue counts. OpenClaw and ZeroClaw have the most ambitious roadmaps but risk community trust erosion if reliability doesn't improve.

---

## 7. Trend Signals

1. **From Prompt Engineering to Deterministic Guarantees:** Across OpenClaw, NanoBot, and CoPaw, users are demanding **hard enforcement hooks** and **append-only file modes** — not just instructions. The era of "prompt as contract" is ending.

2. **Multi-Agent Orchestration is the Next Frontier:** Every major project (OpenClaw, ZeroClaw, PicoClaw, NanoBot) has open RFCs or bugs about subagent reliability. The ecosystem knows multi-agent is the future but **no one has solved it yet** — all implementations are fragile.

3. **Security Boundaries are Table Stakes:** The v2026.6.6 beta security tightening at OpenClaw, SSRF fixes at PicoClaw, and File/Tool Guard at CoPaw all point to **production deployments demanding security**. This is no longer optional.

4. **Chinese-Language Community is a Major Force:** CoPaw, NanoBot (30%+ Chinese issues), and ZeroClaw all have substantial Chinese-speaking user bases. Features like DingTalk, WeChat, Qwen integration, and Xiaomi MiMo Token Plan are becoming important for ecosystem reach.

5. **Platform Fragmentation is Costly:** Windows-specific bugs (OpenClaw EBUSY, CoPaw SSL, LobsterAI installer), macOS instability (Hermes Agent kill signals), and Docker quirks are draining maintainer cycles. Projects that abstract platform differences (CoPaw's Tauri desktop) are winning user satisfaction.

6. **Distribution is a Bottleneck:** IronClaw's 37-day crate publishing gap, LobsterAI's recent release consolidation, and ZeroClaw's "full Docker image" demand all point to **distribution and onboarding friction** as limiting growth.

7. **Corporate Backing is Emerging:** Microsoft/amplifier-app sibling PRs in NanoClaw, NEAR AI backing IronClaw, and NetEase Youdao funding LobsterAI signal that enterprise-grade agents are becoming strategic. Expect more corporate contributions to open-source agent frameworks.

**Value for developers:** The ecosystem is converging on **session reliability, multi-agent orchestration, and security hardening** as universal requirements. Projects that solve these foundations first (NanoBot's session scoping, CoPaw's tool guards) are building competitive moats. The next 6-12 months will likely see a shakeout where projects with unsustainable technical debt (high open issues, low fix velocity) lose community trust to those balancing feature breadth with reliability.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date:** 2026-06-11  
**Analysis Period:** 2026-06-10 — 2026-06-11

---

## 1. Today's Overview

NanoBot v0.2.x shows **high community activity** with 10 issues and 34 PRs updated in the last 24 hours, signaling a project in active maintenance and development. There are **no new releases** today, but the volume of merged/closed PRs (19) indicates strong momentum toward a future patch release. The project is addressing **critical stability and usability bugs**, particularly around subagent workflows, context isolation, and model fallback behavior. Four open issues and 15 open PRs suggest ongoing work spanning the WebUI, Slack, Telegram, and core agent engine.

---

## 2. Releases

**No new releases** today. The latest available version remains **v0.2.1** (inferred from Issue #4287 referencing "nanobot v0.2.1"). Several fix PRs suggest a **v0.2.2 release may be imminent.**

---

## 3. Project Progress

**19 PRs merged or closed today**, indicating substantial forward movement. Key highlights:

### ✅ Merged/Closed Highlights

| PR | Summary | Impact |
|----|---------|--------|
| [#4272](https://github.com/HKUDS/nanobot/pull/4272) | Allow retry and fallback on stream stalled timeout | Fixes #4013 — major stability improvement for LLM streaming |
| [#4274](https://github.com/HKUDS/nanobot/pull/4274) | Scope prompt recent history by session | Closes #4259 — prevents cross-session context pollution |
| [#4273](https://github.com/HKUDS/nanobot/pull/4273) | Add `pathPrepend` config for `exec` tool | Closes #3934 — users can now prepend custom Python envs to `$PATH` |
| [#4275](https://github.com/HKUDS/nanobot/pull/4275) | Fail fast on invalid config files | Improves developer experience with immediate error feedback |
| [#4277](https://github.com/HKUDS/nanobot/pull/4277) | Lazy-load `lark_oapi` SDK for Feishu channel | Reduces startup overhead |
| [#4278](https://github.com/HKUDS/nanobot/pull/4278) | Segment transcript storage for WebUI | Prevents history loss when files exceed 8MB limit |
| [#4255](https://github.com/HKUDS/nanobot/pull/4255) | On-demand version check (no polling) | Implements community feedback to remove background PyPI requests |
| [#4281](https://github.com/HKUDS/nanobot/pull/4281) | Add SiliconFlow as transcription provider | Closes #4000 — expands ASR provider diversity |

### 🔄 Notable Still-Open PRs (likely to merge soon)
- [#4293](https://github.com/HKUDS/nanobot/pull/4293) — Fixes cron jobs with subagents (targets #4290)
- [#4288](https://github.com/HKUDS/nanobot/pull/4288) — Fixes empty model response fallback (targets #4287)
- [#4284](https://github.com/HKUDS/nanobot/pull/4284) — Skill activation from WebUI slash palette

---

## 4. Community Hot Topics

### Most Active Issues (by comments/reactions)

1. **[#4013](https://github.com/HKUDS/nanobot/issues/4013)** — *"Error calling LLM: stream stalled for more than 90 seconds"* (4 comments, CLOSED)  
   **Analysis:** User hit a hardcoded 90s timeout after upgrading from v0.1.5post2 to v0.2.0. The fix (#4272) was merged the same day, showing responsive maintainership. The user explicitly praised the v0.1.5 release, indicating high UX expectations.

2. **[#3934](https://github.com/HKUDS/nanobot/issues/3934)** — *"exec tool cannot pip install Python libraries"* (3 comments, CLOSED)  
   **Analysis:** Root cause: appended `$PATH` had lower priority than system Python. Fixed by adding `pathPrepend` config in #4273 — a clean, backward-compatible solution.

3. **[#4259](https://github.com/HKUDS/nanobot/issues/4259)** — *"history.jsonl cross-session context pollution"* (2 comments, CLOSED)  
   **Analysis:** A well-documented data flow analysis. The author traced the issue to `Consolidator.archive()` and `ContextBuilder.build_system_prompt()` lacking session isolation. Fixed by #4274 with a `session_key` approach.

### Hottest Open Discussion
- **[#4287](https://github.com/HKUDS/nanobot/issues/4287)** (1 comment) — DeepSeek returning empty choices not triggering fallback. This has an **open PR #4288** with a fix.

---

## 5. Bugs & Stability

### 🔴 High Severity (with fix in progress)

| Issue | Description | Fix PR |
|-------|-------------|--------|
| [#4290](https://github.com/HKUDS/nanobot/issues/4290) | Cron jobs end early when subagent spawned; main agent cannot process subagent reply | [#4293](https://github.com/HKUDS/nanobot/pull/4293) |
| [#4287](https://github.com/HKUDS/nanobot/issues/4287) | Empty model responses (DeepSeek peak hours) not triggering fallback | [#4288](https://github.com/HKUDS/nanobot/pull/4288) |
| [#4286](https://github.com/HKUDS/nanobot/issues/4286) | Missing "sustained goal" context; agent repeatedly reports error | No fix PR yet |

### 🟡 Medium Severity (addressed or in review)

| Issue | Description | Status |
|-------|-------------|--------|
| [#4261](https://github.com/HKUDS/nanobot/issues/4261) | GPT-5.x expects `max_completion_tokens` not `max_tokens` | CLOSED |
| [#4237](https://github.com/HKUDS/nanobot/issues/4237) | bwrap sandbox does not reset `$HOME`, breaking tool writes | CLOSED |
| [#4013](https://github.com/HKUDS/nanobot/issues/4013) | Stream stall timeout (no fallback) | Fixed in #4272 |

### 🟢 Low Severity / Minor

| Issue | Description | Status |
|-------|-------------|--------|
| [#4279](https://github.com/HKUDS/nanobot/issues/4279) | Subagent notifications should be aggregated to prevent hallucinations | OPEN — enhancement proposal |

---

## 6. Feature Requests & Roadmap Signals

### Features with High Likelihood for Next Release

1. **Model Presets for Subagents** ([#4291](https://github.com/HKUDS/nanobot/pull/4291))  
   Subagents can use a different model than the parent agent via `spawnPresets`. This is a significant architectural enhancement for multi-agent workflows.

2. **Slack: `groupRequireMention`** ([#4289](https://github.com/HKUDS/nanobot/pull/4289))  
   Allows Slack bots to require @mentions even in allowed channels — solves the "bot responds everywhere" problem.

3. **WebUI: Skill Activation via Slash** ([#4284](https://github.com/HKUDS/nanobot/pull/4284))  
   Users can now activate skills from the slash palette. Implements community wish from issue #2488.

4. **WebUI: File Manager in Settings** ([#4282](https://github.com/HKUDS/nanobot/pull/4282))  
   Users can browse and modify agent/SOUL config files from the WebUI — eliminates need for host login.

5. **Context Continuity Under Pressure** ([#4280](https://github.com/HKUDS/nanobot/pull/4280))  
   Persistence of short-term memory when context limits are hit — addresses long-standing memory loss complaints (#4044).

### Emerging Roadmap Signals
- **Subagent aggregation** ([#4279](https://github.com/HKUDS/nanobot/issues/4279)) — users want batched subagent results to reduce LLM hallucination risk
- **Sustained goal tracking** (#4286) — the "missing sustained goal" bug suggests users rely heavily on multi-turn goal persistence
- **Cron robustness** (#4290, #4285) — cron job reliability is a recurring theme, suggesting NanoBot is being used in production/scheduled workflows

---

## 7. User Feedback Summary

### Positive Signals
- **v0.1.5 praised:** User in #4013 called it "very good" and thanked the team
- **Fast fixes:** Several users had their bugs resolved within 24 hours (e.g., #4013 → #4272), indicating responsive development
- **Quality of bug reports:** Issues like #4259 show users are doing deep data flow analysis, indicating a technically savvy community

### Pain Points
- **Upgrade friction:** Moving from v0.1.5post2 to v0.2.0 broke streaming/timeout behavior (#4013) — suggests regression testing gaps
- **Empty responses without fallback:** DeepSeek peak-hour empty responses (#4287) block production use
- **Context pollution:** Multi-session history bleeding (#4259) undermines trust in agent memory
- **Environment isolation:** bwrap sandbox not resetting `$HOME` (#4237) and `pathPrepend` ordering (#3934) show configuration sharp edges
- **Chinese-language reports:** Several issues are in Chinese (#3934, #4259, #4290), pointing to a substantial Chinese-speaking user base

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Problem | Reason for Watch |
|-------|-----|---------|------------------|
| [#4286](https://github.com/HKUDS/nanobot/issues/4286) | 1 day | Missing "sustained goal" context with screenshot | **No fix PR or response yet** — user appears blocked |
| [#4279](https://github.com/HKUDS/nanobot/issues/4279) | 1 day | Subagent notification aggregation | Enhancement with clear design, no PR yet |
| [#4290](https://github.com/HKUDS/nanobot/issues/4290) | <1 day | Cron jobs ending early with subagents | Fix PR #4293 exists but still open — needs review |

### Older Items (potential neglect)
- **None identified** — all open issues are <2 days old, suggesting the project maintains a healthy response cadence

---

## Summary Assessment

**Project Health: 🌟 Very Good**  
NanoBot is in a productive development phase with high community engagement. The maintainers are merging fixes within 24 hours of bug reports, and the PR pipeline is clearing rapidly (19 of 34 PRs closed today). The most pressing issues (stream stalls, context pollution, fallback failures) have identified fixes. The addition of SiliconFlow transcription, subagent model presets, and WebUI file management signals expansion toward enterprise-grade features. The main risk is **regression velocity** — users hit new issues on upgrade, suggesting a need for more comprehensive pre-release testing in future releases.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for 2026-06-11.

---

## Hermes Agent Project Digest — 2026-06-11

### 1. Today's Overview
The project is experiencing a **very high volume of activity**, with 50 open issues and 50 open PRs updated in the last 24 hours, indicating a highly engaged community and a surge of bug reports following a recent release cycle. While no new releases were published today, the project is processing a substantial number of contributions, with 4 PRs merged/closed. However, the sheer volume of open items—particularly P1 and P2 bugs—suggests the maintainers are in a **crunch mode**, balancing critical stability fixes with a healthy stream of feature contributions. The backlog is growing, which may require prioritization triage.

### 2. Releases
**No new releases today.** The latest available version remains v0.16.0, referenced in several current bug reports.

### 3. Project Progress
Four pull requests were merged or closed today, primarily focusing on stability and data integrity:
- **#31531 [CLOSED]**: A critical P1 fix preventing silent data loss where the session database (`state.db`) could skip writing assistant responses after a scaffolding pop.
- **#43909 [OPEN]**: A new test contribution was opened (status unclear on merge).
- **#43863, #43864**: Two separate PRs from the same author addressed configuration wizards and a new standalone cron daemon mode, indicating active feature development alongside bug fixing.

### 4. Community Hot Topics
The most active discussions highlight major UX friction and critical data-loss scenarios:

- **#23402 [15 comments] — Docker Permissions Bug**: The most active issue this period. Users are struggling with permission issues specifically related to the `HERMES_UID` environment variable in Docker, which breaks the Dashboard chat feature. This is a major adoption blocker for users on Unraid and similar NAS platforms. [Link](https://github.com/NousResearch/hermes-agent/issues/23402)
- **#26689 [9 comments] — Accessibility (VoiceOver)**: A blind user has detailed a comprehensive list of blockers for screen-reader users on macOS. This is a strong signal from a passionate user who values the backend power but finds the UX inaccessible. [Link](https://github.com/NousResearch/hermes-agent/issues/26689)
- **#40239 [4 comments] — Portuguese (pt-BR) Localization**: A user is requesting full desktop app localization, noting that backend/TUI support already exists. This indicates a fragmented user experience between the desktop client and the CLI. [Link](https://github.com/NousResearch/hermes-agent/issues/40239)

### 5. Bugs & Stability
Today saw a significant number of **P1 and P2** bugs reported, indicating a "critical fix" period:

- **P1**:
    - **#24187 - SessionDB silent skip**: Message repair can cause the database to skip writing the current turn, leading to lost assistant replies. *Fix PR #43905 exists.* [Link](https://github.com/NousResearch/hermes-agent/issues/24187)
    - **#43842 - macOS plist kill**: A self-update from inside the gateway kills the CLI process before the bootstrap is complete, leaving the service unloaded and unreachable. [Link](https://github.com/NousResearch/hermes-agent/issues/43842)

- **P2**:
    - **#43475 - macOS `/restart` bricks gateway**: The restart command exits cleanly, but on `launchd` systems, this prevents the service from automatically restarting. [Link](https://github.com/NousResearch/hermes-agent/issues/43475)
    - **#43835 - Telegram double messages**: Users see a terminal/code block output followed by the text response, appearing as a duplicate message. [Link](https://github.com/NousResearch/hermes-agent/issues/43835)
    - **#43617 - Kimi provider broken**: The `kimi-coding` provider uses a wrong API endpoint, breaking all API calls including vision. [Link](https://github.com/NousResearch/hermes-agent/issues/43617)
    - **#43830 - WhatsApp groups broken**: Messages to migrated groups with LID addressing are silently dropped due to an outdated dependency. [Link](https://github.com/NousResearch/hermes-agent/issues/43830)
    - **#43747 - Credential pool false positive**: A working API account is incorrectly marked as rate-limited, requiring manual auth reset. [Link](https://github.com/NousResearch/hermes-agent/issues/43747)

### 6. Feature Requests & Roadmap Signals
- **High Likelihood (Next Release)**:
    - **Per-platform lifecycle messages (#43887)**: PR already exists; allows admins to customize gateway restart notifications per platform (Telegram, Slack, etc.).
    - **Standalone Cron Daemon (#43864)**: PR ready for merge; solves the issue of cron jobs not running on systems where the gateway is not active (e.g., Windows, headless).
    - **Simultaneous Local/Remote Backends (#37876)**: A long-standing request for the Desktop app that is seeing new traction.

- **Emerging Signals**:
    - **Accessibility (#26689)**: The detail in this request suggests a growing demand from assistive-technology users.
    - **Docker Reliability (#23402)**: The high activity on this issue indicates the Docker deployment path needs more robust testing and documentation.

### 7. User Feedback Summary
- **Pain Points**:
    - **Docker complexity**: The permission model (`HERMES_UID`) is unintuitive and breaks basic functionality (chat).
    - **macOS instability**: The `/restart` command and self-update logic are dangerous on `launchd`-managed services, effectively bricking the gateway.
    - **Desktop app inconsistency**: Users are frustrated that features like `hooks`, profile support, and localization work in CLI/TUI but not in the Desktop app.
    - **Memory pollution**: The Honcho memory module is generating duplicate facts and treating skill invocations as user speech, degrading the quality of long-term memory.
- **Satisfaction Signals**: The development of a native `OpenTUI` (#42922) and the new `hexis_appraisal` plugin (#43906) show that the community is actively building sophisticated, opt-in features that the maintainers are reviewing. The rapid merging of critical P1 fixes (#31531) shows maintainer responsiveness.

### 8. Backlog Watch
The following issues remain open and unanswered for extended periods, requiring maintainer triage or a clear status update:

- **#15296 [P3, Updated 2026-06-11] - Credential pool backoff**: Opened 2026-04-24. This feature request for exponential backoff on API exhaustion has sat for over a month with no official acknowledgment or rejection. *Likely being reviewed alongside the related bug #43747.* [Link](https://github.com/NousResearch/hermes-agent/issues/15296)
- **#3335 [OPEN, Created 2026-03-27] - Zulip integration**: This PR has been open for 2.5 months without merge or close. Zulip is a popular open-source alternative to Slack/Telegram; the lack of movement may be a missed opportunity for adoption. [Link](https://github.com/NousResearch/hermes-agent/pull/3335)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-11

## Today's Overview

PicoClaw shows moderate-high activity today with **5 issues** and **15 pull requests** updated in the last 24 hours, alongside a new **nightly release** (v0.2.9-nightly). The project is in a healthy maintenance phase, with several security and stability patches being actively merged. A notable SSRF vulnerability fix was closed, and multiple PRs address type-safety issues flagged by static analysis. Community engagement remains steady, with two new bug reports and one feature request opened today.

## Releases

- **nightly (v0.2.9-nightly.20260611.d955d5bb)**  
  Automated nightly build — unstable, use with caution.  
  No breaking changes or migration notes provided.  
  [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

## Project Progress

**6 PRs merged/closed today**, covering important fixes:

- **SSRF Protection Hardened** — [#3085](https://github.com/sipeed/picoclaw/pull/3085) (merged): Blocks `198.18.0.0/15` in SSRF guard, closing security advisory [#3077](https://github.com/sipeed/picoclaw/issues/3077).
- **Windows Path Separator Fix** — [#3089](https://github.com/sipeed/picoclaw/pull/3089) (merged): Fixes `list_dir` "invalid argument" error on Windows (issue [#2472](https://github.com/sipeed/picoclaw/issues/2472)).
- **Error Handling Improvements** — [#3043](https://github.com/sipeed/picoclaw/pull/3043) (merged): Adds proper error checks for `strconv.Atoi` and `json.Unmarshal` calls.
- **Web Search API Compatibility** — [#2951](https://github.com/sipeed/picoclaw/pull/2951) (merged): Switches to `function` type web search to avoid HTTP 400 errors on OpenAI endpoints.
- **Claude Opus 4-7 Temperature Fix** — [#2948](https://github.com/sipeed/picoclaw/pull/2948) (merged): Skips deprecated temperature parameter for claude-opus-4-7 models.
- **Debug Tracer Tool** — [#2945](https://github.com/sipeed/picoclaw/pull/2945) (merged): Adds standalone picoclaw-tracer UI for real-time LLM trace viewing.

**Still open (9 PRs)** include critical type-safety fixes across multiple packages, agent collaboration infrastructure, and web UI hardening.

## Community Hot Topics

- **Most active issue** — [#2472](https://github.com/sipeed/picoclaw/issues/2472) (stale, 5 comments, 👍1): Windows path separator bug in `list_dir`. Now resolved by PR [#3089](https://github.com/sipeed/picoclaw/pull/3089).
- **Security advisory** — [#3077](https://github.com/sipeed/picoclaw/issues/3077) (closed): SSRF bypass via `198.18.0.0/15` — resolved in PR [#3085](https://github.com/sipeed/picoclaw/pull/3085).
- **Duplicate message bug** — [#3094](https://github.com/sipeed/picoclaw/issues/3094) (new, 0 comments): Spawned subagent results causing duplicate push notifications. No fix PR yet — likely requires architectural change in message routing.

Underlying need: The `spawn` tool duplicate issue (#3094) reflects a growing demand for clear, noiseless multi-agent workflows, especially in chat platforms. The community is experiencing friction between raw subagent output and curated final responses.

## Bugs & Stability

*Ranked by severity:*

1. **Medium** — **Duplicate subagent messages** [#3094](https://github.com/sipeed/picoclaw/issues/3094)  
   *ForUser* field reused for both direct push and master agent summary. Causes spam in Telegram/Feishu. No fix PR yet.

2. **Low** — **Safari <16.4 panel breakage** [#3090](https://github.com/sipeed/picoclaw/issues/3090)  
   Panel login fails on older iOS Safari. Likely a frontend compatibility issue with CSS/JavaScript features.

3. **Low (fixed)** — **Windows path separator crash** [#2472](https://github.com/sipeed/picoclaw/issues/2472)  
   Fixed by [#3089](https://github.com/sipeed/picoclaw/pull/3089) (merged today).

4. **Low (fixed)** — **SSRF bypass** [#3077](https://github.com/sipeed/picoclaw/issues/3077)  
   Fixed by [#3085](https://github.com/sipeed/picoclaw/pull/3085) (merged today).

Additional fixes in open PRs: HTTP client type assertion panic [#3095](https://github.com/sipeed/picoclaw/pull/3095), native search type assertion [#3091](https://github.com/sipeed/picoclaw/pull/3091), skills install type safety [#3092](https://github.com/sipeed/picoclaw/pull/3092), lock store panic [#3053](https://github.com/sipeed/picoclaw/pull/3053).

## Feature Requests & Roadmap Signals

- **New messenger gateways** — [#3093](https://github.com/sipeed/picoclaw/issues/3093): User requests **SimpleX**, **Wire**, or **Tox** gateway support. Indicates demand for more privacy-centric, decentralized messaging backends.
- **Agent collaboration** — [#2937](https://github.com/sipeed/picoclaw/pull/2937) (open, stale): Internal agent collaboration bus with mailboxes and session threads. This large feature could land in v0.3.0 if merged.
- **Debug tracer** — [#2945](https://github.com/sipeed/picoclaw/pull/2945) (merged): New standalone trace viewer — likely to appear in next stable release.

**Prediction for next minor version (v0.3.0)**: Agent collaboration bus (#2937) if finalized, plus merged stability fixes. Gateway additions (SimpleX/Tox) are lower priority but could appear as experimental plugins.

## User Feedback Summary

- **Pain point**: Windows users blocked by path separator bug (#2472) — frustrating because it prevented file operations entirely. Fix is now merged.
- **Pain point**: Noisy multi-agent workflows (#3094) — duplicate messages confuse users and degrade chat experience.
- **Use case**: Operators deploying behind proxies need more granular access control (#3083) — launcher hardening PR suggests production deployments are increasing.
- **Satisfaction**: The `list_dir` fix and SSRF patch were well received (closed quickly with direct maintainer attention).
- **Dissatisfaction**: Safari iOS <16.4 users cannot access panel (#3090) — indicates mobile access is important but less tested.

## Backlog Watch

- **Stale, high-value** — [#2937](https://github.com/sipeed/picoclaw/pull/2937) (open since 2026-05-24): Agent collaboration bus PR. No activity in 18 days. If maintainers intend to merge, it needs review and conflict resolution. If abandoned, should be closed.
- **Stale bug** — [#2472](https://github.com/sipeed/picoclaw/issues/2472) (created 2026-04-10, open for 2 months) — now fixed by [#3089](https://github.com/sipeed/picoclaw/pull/3089), can be closed.
- **Open without maintainer response** — [#3093](https://github.com/sipeed/picoclaw/issues/3093) (SimpleX/Tox request, 0 comments) — no maintainer acknowledgment yet. Could benefit from a brief "wontfix" or "needs discussion" label.

---

*Generated for 2026-06-11. All links reference sipeed/picoclaw on GitHub.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-11

## Today's Overview

The NanoClaw project shows **high activity** today with 12 pull requests updated in the last 24 hours and 2 new open issues. Of the 12 PRs, 5 have been merged or closed, reflecting steady progress on both bug fixes and feature development. The project continues to advance its modular skill ecosystem, with contributions spanning container logging, guardrails, web search, and documentation improvements. Two security-related bugs surfaced today, both receiving prompt fix PRs.

## Releases

No new releases today.

---

## Project Progress

**Merged/Closed PRs (5):**

- [#2719 — Add uninstall.sh (per-copy uninstaller)](https://github.com/nanocoai/nanoclaw/pull/2719) — Merged 2026-06-10. Adds a standalone uninstall utility with dry-run, confirmation, and OneCLI agent cleanup. This operational skill improves lifecycle management for users running multiple NanoClaw copies.

- [#2721 — Docs: customizing intro, skills model, and skill guidelines](https://github.com/nanocoai/nanoclaw/pull/2721) — Merged 2026-06-10. Establishes three formal documentation layers (`docs/customizing.md`, skills model, skill guidelines) that define how users create and contribute skills, explicitly addressing the "merge fights on update" pain point.

- [#3 — Secure IPC with per-group namespaces](https://github.com/nanocoai/nanoclaw/pull/3) — Closed 2026-06-10. This long-standing PR (opened Feb 2026) implements per-group IPC directories with authorization enforcement, preventing privilege escalation between agent groups.

- [#2723 — Finance DD agent](https://github.com/nanocoai/nanoclaw/pull/2723) — Closed 2026-06-10. A utility skill for financial due diligence agents.

- [#2724 — Opened against wrong repo — disregard](https://github.com/nanocoai/nanoclaw/pull/2724) — Closed immediately as misdirected.

---

## Community Hot Topics

**Most Active Discussion:**

1. **[#1690 — Multi-runtime agent SDK abstraction](https://github.com/nanocoai/nanoclaw/issues/1690)** (6 comments, 👍3) — The highest-reacted open issue, ongoing since April. Proposes modular runtime backends (Claude Codex, local models) installable like channels (`/add-claude`, `/add-codex`). The 6 comments suggest active design discussion, though no maintainer response is visible in the available data. This is the community's clearest signal for multi-model support demand.

**Most Active New PRs:**

2. **[#2730 — fix: NANOCLAW_* flags never reach process.env under launchd/systemd](https://github.com/nanocoai/nanoclaw/pull/2730)** — Opened today, 0 comments yet, but directly addresses the root cause of today's most critical bug (Issue #2731).

3. **[#2727 — feat: persist agent container stdout+stderr to disk](https://github.com/nanocoai/nanoclaw/pull/2727)** — Opened yesterday, still open. A microsoft/amplifier-app sibling PR porting container log persistence to the main repo, indicating corporate interest in operational observability.

**Underlying Need Analysis:**
The persistent attention on #1690 reveals a community desire to break free from single-runtime vendor lock-in. Users want NanoClaw as a neutral orchestration layer, not tied to any one agent SDK. The 3-month lifespan with no maintainer engagement signals a potential gap between community demand and roadmap.

---

## Bugs & Stability

**Critical:**

- **[#2731 — Egress lockdown hijacks host.docker.internal](https://github.com/nanocoai/nanoclaw/issues/2731)** — Opened 2026-06-11, 0 comments. When `NANOCLAW_EGRESS_LOCKDOWN=true` is set, the egress lockdown gateway attaches to a network that blocks agents from reaching `host.docker.internal` (Ollama, local proxies). This breaks all host-local service access in egress-locked deployments — a complete denial-of-service for host-dependent agents. **Severity: Critical** (breaks production functionality with no workaround).

- **Fix PR Exists:** [#2730](https://github.com/nanocoai/nanoclaw/pull/2730) fixes the `.env` loading bug that prevents `NANOCLAW_EGRESS_LOCKDOWN` from being reliably set in non-Docker environments. However, Issue #2731 is a separate Docker-level network topology bug not yet addressed.

**High:**

- **[#2730 — .env flags never reach process.env under launchd/systemd](https://github.com/nanocoai/nanoclaw/pull/2730)** — Bug: `egress-lockdown.ts` gates on `process.env.NANOCLAW_EGRESS_LOCKDOWN` but nothing loads `.env` before that module. Affects all systemd/launchd deployments where flags are set via `.env` and `docs/SECURITY.md` instructs users to use that method. **Severity: High** (documented configuration method is non-functional).

**Medium:**

- **[#2728 — Telegram pairing with --intent wire-to never creates DB row](https://github.com/nanocoai/nanoclaw/pull/2728)** — Bug: Pairing with wire-to intent reports success but doesn't insert the `messaging_group_agents` row, so the wiring has no effect. **Severity: Medium** (feature partially broken, no crash).

- **[#2729 — Telegram skill doc has mismatched status-block names](https://github.com/nanocoai/nanoclaw/pull/2729)** — Documentation bug where the pairing walkthrough references status blocks that the setup step never emits, causing user confusion. **Severity: Low-Medium** (bad UX, but no functional breakage).

---

## Feature Requests & Roadmap Signals

**High-likelihood for next release:**

1. **Container log persistence** ([#2727](https://github.com/nanocoai/nanoclaw/pull/2727)) — Sibling PR from microsoft/amplifier-app, already tested. Capturing agent container stdout/stderr to disk is likely to merge given corporate backing and clear operational value.

2. **Per-agent-group guardrails** ([#2726](https://github.com/nanocoai/nanoclaw/pull/2726)) — Adds input/output guardrails (prompt injection blocking, credential leak detection) with quarantine audit trail. This addresses growing enterprise security requirements for multi-tenant agent deployments.

3. **Web search plus skill** ([#2725](https://github.com/nanocoai/nanoclaw/pull/2725)) — Multi-provider web search + extraction as a standalone CLI-based utility skill, no MCP dependency. Practical tool for agent information gathering.

4. **Tool-visibility live previews** ([#2211](https://github.com/nanocoai/nanoclaw/pull/2211)) — Open since May, now conforming to the skills model. Live tool-call previews in chat UX. This is a mature PR that could land soon after documentation alignment.

**Medium-likelihood:**

5. **Multi-runtime SDK abstraction** ([#1690](https://github.com/nanocoai/nanoclaw/issues/1690)) — Community-driven feature request. If maintainers prioritize, this could become a v0.5 milestone. Currently no roadmap commitment visible.

6. **Finance due diligence agent** ([#2723](https://github.com/nanocoai/nanoclaw/pull/2723)) — Closed but shows vertical-specific skill interest.

---

## User Feedback Summary

**Pain Points:**

1. **Configuration non-functional in production** — Users on launchd/systemd cannot reliably set operational flags via `.env` because no bootstrapping loads environment variables before module evaluation. This breaks documented setup flow for `NANOCLAW_EGRESS_LOCKDOWN`.

2. **Egress lockdown breaks host service access** — Setting `NANOCLAW_EGRESS_LOCKDOWN=true` for security unexpectedly kills all host-local service connectivity (Ollama, proxies), making the security feature self-defeating for common local AI configurations.

3. **Telegram pairing is buggy** — The wire-to intent appears to succeed but creates no DB wiring, and documentation references nonexistent status steps. Users following the documentation end up with broken integrations and no error messages.

**Satisfaction Signals:**

4. **Documentation improvements warmly received** — The merged docs PR (#2721) directly addresses the "merge fights on update" pain point that has been a long-standing frustration. The formalized skills contract is clearly aligned with how the community wants to contribute.

5. **Corporate interest in operational features** — The microsoft/amplifier-app sibling PR (#2727) suggests NanoClaw has enterprise adopters who value observability (container logging) and lifecycle tooling (uninstall script).

---

## Backlog Watch

**Issues Needing Maintainer Attention:**

- **[#1690 — Multi-runtime agent SDK abstraction](https://github.com/nanocoai/nanoclaw/issues/1690)** — Created 2026-04-07 (65 days old). 6 comments, 3 upvotes. The community's most-requested feature with no maintainer response visible. If left unanswered much longer, risks disengagement of contributors invested in this direction.

**PRs Needing Review:**

- **[#2211 — Tool-visibility skill](https://github.com/nanocoai/nanoclaw/pull/2211)** — Open since 2026-05-03 (39 days). Updated 2026-06-10. After being rebuilt to conform to the new skills model, this PR is ready for maintainer review. Longest-open feature PR without closure.

- **[#2727 — Container log persistence](https://github.com/nanocoai/nanoclaw/pull/2727)** — Open since 2026-06-10. Corporate-backed PR with clear value. Should be prioritized given the amplifier-app sibling already exists.

**Action Items:**
- Respond to Issue #1690 with roadmap position on multi-runtime support
- Block Issue #2731 on the egress lockdown bug for critical fix
- Review PR #2211 which has been waiting 39 days post-rebuild
- Land PR #2730 to fix the `.env` loading bug before it compounds with the egress lockdown issue

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-06-11**.

---

### NullClaw Project Digest – 2026-06-11

**1. Today's Overview**
The project shows low community interaction but moderate development activity, with four new open pull requests submitted in the last 24 hours and zero issues reported. No new releases were published, and there is no open issue backlog to manage, indicating a clean project state. The development focus is squarely on stability, configuration flexibility, and fixing edge-case bugs in the agent runner, gateway, and cron systems. While user feedback signals are absent today, the maintainer team is actively addressing technical debt and test reliability.

**2. Releases**
*No new releases were published today.*

**3. Project Progress**
No pull requests were merged or closed today. However, four new PRs were opened, signaling active development in the following areas:
- **Agent Runner stability**: PR [#951](https://github.com/nullclaw/nullclaw/pull/951) suppresses stderr initialization logs when an agent process fails, preventing noisy channel messages.
- **Configuration flexibility**: PR [#949](https://github.com/nullclaw/nullclaw/pull/949) makes the agent queue mode configurable via `config.json`, moving the `QueueMode` enum to `config_types.zig` for shared use.
- **Cron system reliability**: PR [#948](https://github.com/nullclaw/nullclaw/pull/948) fixes delivery attribution for cron agent commands, preserving metadata across subprocess spawns.
- **Gateway test cleanup**: PR [#950](https://github.com/nullclaw/nullclaw/pull/950) moves the port probe before memory allocations to prevent resource leaks when `gateway.run()` fails with `AddressInUse`.

**4. Community Hot Topics**
There are no issues or pull requests with comments or reactions today. The four open PRs have zero discussion activity, suggesting either prompt triage by maintainers or low community engagement on this cycle.

**5. Bugs & Stability**
No bugs were reported by users today. However, the opened PRs identify two internal stability improvements:
- **Medium severity – Gateway test leak**: PR [#950](https://github.com/nullclaw/nullclaw/pull/950) addresses a memory leak in test environments when a port is already in use. This is a development-time stability issue, not a production crash, but important for CI reliability.
- **Medium severity – Agent stderr noise**: PR [#951](https://github.com/nullclaw/nullclaw/pull/951) fixes a logic flaw where agent failure logs were posted to channels as responses. This could cause confusing messages in production chat threads.
- **Low severity – Cron attribution**: PR [#948](https://github.com/nullclaw/nullclaw/pull/948) fixes a missing metadata pass-through that could cause cron deliveries to appear unattributed.

**6. Feature Requests & Roadmap Signals**
No new feature requests were filed today. The PRs hint at internal roadmap priorities:
- **Configuration-driven behavior**: The move to make `queue_mode` configurable (PR [#949](https://github.com/nullclaw/nullclaw/pull/949)) suggests a push toward more user-accessible settings, likely to appear in the next minor release.
- **Reliability improvements**: The combined focus on agent output handling, gateway startup, and cron attribution indicates the team is polishing core infrastructure before a release candidate.

**7. User Feedback Summary**
No user feedback was recorded today. There are no issues, comments, or reactions to analyze.

**8. Backlog Watch**
There are no outstanding issues or pull requests awaiting maintainer attention. The open PRs were all created within the last 24 hours and are in early review state. The project’s backlog is effectively zero, indicating strong maintenance hygiene.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-11

## 1. Today's Overview

IronClaw is in a period of intense development activity, with 50 issues and 50 PRs updated in the last 24 hours, including 22 merged/closed PRs and 15 closed issues. The project is heavily focused on the **Reborn** architecture migration, which is now the dominant theme across all workstreams. The team is addressing a significant backlog of WebUI v2 usability issues, provider configuration bugs, and auth flow problems discovered during local testing. Activity is concentrated on stabilising the Reborn WebUI and operator experience, with particular attention to LLM provider configuration, OAuth credential flows, and the agent loop's gate-resume mechanism. No new releases were published today, and a notable long-standing issue (#3259) remains open regarding missing crate publishes.

## 2. Releases

No new releases were published in the last 24 hours. The project continues to be affected by the blocked publishing pipeline documented in Issue #3259, where crate versions 0.25.0 through 0.27.0 are tagged on GitHub but not available on crates.io, pinning downstream consumers to 0.24.0.

## 3. Project Progress

Eleven PRs were merged or closed today, representing substantial progress across several fronts:

- **Provider Configuration**: PR #4731 ([link](https://github.com/nearai/ironclaw/pull/4731)) fixes operator LLM provider configuration end-to-end — saving providers, model discovery, and Settings UI — closing Issue #4673 and addressing #4705 and #4697.

- **Auth-Gate Resume**: PR #4746 ([link](https://github.com/nearai/ironclaw/pull/4746)) adds auth-gate resume functionality so OAuth capability calls re-dispatch automatically after credential setup, fixing a bug where "next meeting" queries returned stale data.

- **Slack Integration**: PRs #4730 ([link](https://github.com/nearai/ironclaw/pull/4730)), #4739 ([link](https://github.com/nearai/ironclaw/pull/4739)) complete the personal Slack DM delivery pipeline and enable Slack for Railway QA deployments.

- **Error Classification**: PR #4743 ([link](https://github.com/nearai/ironclaw/pull/4743)) fixes NEAR context overflow classification so "prompt is too long" errors are correctly identified as `ContextLengthExceeded`.

- **Manual Token Credentials**: PR #4742 ([link](https://github.com/nearai/ironclaw/pull/4742)) fixes manual token runtime credential selection, allowing these credentials to satisfy runtime requests.

- **WebUI Approval Affordance**: PR #4717 ([link](https://github.com/nearai/ironclaw/pull/4717)) restores the "Always Allow" affordance for typed product-workflow approval gates in WebUI v2.

- **Refactoring**: PR #4745 ([link](https://github.com/nearai/ironclaw/pull/4745)) refactors the Automations panel facade to use TriggerRepository, removing capability dispatch from panel reads.

- **Documentation**: PR #4652 ([link](https://github.com/nearai/ironclaw/pull/4652)) documents the Reborn serve/WebUI testing flow with a launch script.

- **Content Overflow**: PR #4734 ([link](https://github.com/nearai/ironclaw/issues/4734)) resolved the issue of the agent avatar showing "IC" instead of an IronClaw icon.

## 4. Community Hot Topics

### Issue #3259 — "Publish 0.25.0–0.27.0 to crates.io" ([link](https://github.com/nearai/ironclaw/issues/3259))
- **14 comments**, open since May 5, 2026
- The highest-engagement issue by far. Downstream consumers cannot access tagged releases because crates.io only has v0.24.0. This blocks users dependent on the crates.io distribution channel and suggests an infrastructure or release-process bottleneck that is becoming a community pain point.

### Issue #3036 — "Configuration-as-Code for IronClaw Reborn" ([link](https://github.com/nearai/ironclaw/issues/3036))
- **6 comments**, 1 👍
- An epic request for declarative configuration of IronClaw via tenant blueprints and harnesses, addressing operator pain with mixing `.env`, settings JSON, and runtime flags. This signals desire for production-grade, reproducible deployment configurations.

### Issue #3283 — "Migrate OpenAI-compatible APIs onto Reborn" ([link](https://github.com/nearai/ironclaw/issues/3283))
- **3 comments**, closed
- Part of the larger Reborn migration effort, successfully completed. The community and contributors are actively working through the Reborn migration backlog.

## 5. Bugs & Stability

### High Severity

1. **NEAR AI provider configuration cannot be saved** (#4673, [link](https://github.com/nearai/ironclaw/issues/4673)) — The "Save" button fails silently after a successful test connection. **Fix in PR #4731** (merged today).

2. **Strict-mode provider null values rejected** (#4642, [link](https://github.com/nearai/ironclaw/issues/4642)) — Null-for-unset optionals from strict-mode LLM providers are rejected by capability-port validation, breaking most first-party tools. Closed with a fix.

3. **Conversation cannot use NEAR AI provider after setup** (#4703, [link](https://github.com/nearai/ironclaw/issues/4703)) — Despite successful test connection, the provider doesn't function in conversations. **Active, no linked fix yet.**

4. **Auth flow unrecoverable after failed sign-in** (#4706, [link](https://github.com/nearai/ironclaw/issues/4706)) — Both NEAR AI SSO and ChatGPT subscription fail to recover after cancelled or failed sign-ins.

### Medium Severity

5. **Unsent drafts lost on new conversation** (#4724, [link](https://github.com/nearai/ironclaw/issues/4724)) — Unsent messages are discarded when navigating away from the New Conversation page.

6. **Composer remains interactive during Working state** (#4725, [link](https://github.com/nearai/ironclaw/issues/4725)) — Hover/focus styling hints at interactivity when the composer is actually disabled.

7. **Login broken for local/desktop builds** (#4729, [link](https://github.com/nearai/ironclaw/issues/4729)) — `private.near.ai` rejects non-standard `frontend_callback` values, breaking local development auth.

8. **builtin.http approval loop on failure** (#4704, [link](https://github.com/nearai/ironclaw/issues/4704)) — After an `invalid_input` failure, the approval loop repeats without actionable error details.

9. **Opaque master key error** (#4741, [link](https://github.com/nearai/ironclaw/issues/4741)) — Corrupt secret master key produces an unactionable error message.

### Low Severity / UX

10. **No syntax highlighting in code blocks** (#4708, [link](https://github.com/nearai/ironclaw/issues/4708))
11. **Font size too small** (#4707, [link](https://github.com/nearai/ironclaw/issues/4707))
12. **Avatar missing user/assistant identity** (#4722, [link](https://github.com/nearai/ironclaw/issues/4722))
13. **Missing agent identity in avatar** (#4734, [link](https://github.com/nearai/ironclaw/issues/4734))

## 6. Feature Requests & Roadmap Signals

Several issues point toward features likely to appear in the next minor release:

- **Automated NEAR AI MCP enablement** (#4700, [link](https://github.com/nearai/ironclaw/issues/4700)) — When NEAR AI credentials are configured, the MCP integration should auto-enable without manual steps. This is a clear UX improvement likely to be prioritised.

- **Attachment support for WebChat v2** — PRs #4738 ([link](https://github.com/nearai/ironclaw/pull/4738)) and #4670 ([link](https://github.com/nearai/ironclaw/pull/4670)) are wiring file upload UX into the Reborn WebUI SPA, bridging inbound bytes into transcript attachment refs. This is a substantial feature addition in-flight.

- **Programmatic MCP server configuration** — PR #4735 ([link](https://github.com/nearai/ironclaw/pull/4735)) adds `headers` and `oauth` fields to `InstallExtensionRequest`, plus PATCH update support. This enables API-driven extension management.

- **Observability seams for external hosts** — PR #4588 ([link](https://github.com/nearai/ironclaw/pull/4588)) adds trajectory observer hooks and LLM provider injection for external benchmarking systems like `nearai-bench`.

- **Configuration-as-Code epic** (#3036, [link](https://github.com/nearai/ironclaw/issues/3036)) — A long-running epic for declarative configuration; likely a v0.28+ or v0.29+ target.

## 7. User Feedback Summary

The most prominent user pain points emerging this week centre on **WebUI v2 first-run experience** and **provider configuration reliability**. The extensive local testing findings documented in Issue #4692 ([link](https://github.com/nearai/ironclaw/issues/4692)) aggregate several concrete frustrations:

- **Silent failures** are a recurring theme — providers test successfully but fail to save, provider config errors yield generic "driver unavailable" messages instead of actionable diagnostics, and tool call failures loop without explanation.
- **Auth flow fragility** is the single largest source of user friction: broken SSO callback handling for local builds (#4729), unrecoverable states after failed sign-ins (#4706), and opaque "Invalid master key" errors (#4741) make initial setup punishing.
- **Information density** in the UI is low: the approval modal shows too little context for `builtin.http` tool requests (#4701), conversation messages lack user/assistant identities (#4722), and code blocks lack syntax highlighting (#4708).
- **Chat workflow interruptions** from external links navigating away from the conversation (#4733) and unsent drafts being lost (#4724) disrupt the core chat experience.

Satisfaction signals are more indirect — the team is rapidly shipping fixes (11 merged PRs today), suggesting responsive engagement with testers and early users.

## 8. Backlog Watch

| Item | Issue/PR | Age | Status | Notes |
|------|----------|-----|--------|-------|
| **Blocked crate publishing** | [#3259](https://github.com/nearai/ironclaw/issues/3259) | 37 days | Open, 14 comments | Downstream pinned to v0.24.0; no update from maintainers |
| **Configuration-as-Code epic** | [#3036](https://github.com/nearai/ironclaw/issues/3036) | 44 days | Open, 6 comments | No progress since creation; large surface area |
| **Release PR** | [#3708](https://github.com/nearai/ironclaw/pull/3708) | 26 days | Open | Chore release PR with breaking changes in `ironclaw_common` and `ironclaw_skills`; not yet merged despite potential downstream dependency fixes |
| **Tokio ecosystem dependency bumps** | [#4499](https://github.com/nearai/ironclaw/pull/4499) | 6 days | Open | 3 dependency updates pending merge |
| **Trace Commons onboarding** | [#4559](https://github.com/nearai/ironclaw/pull/4559) | 3 days | Open | Large feature PR for agent-driven Trace Commons invites |

The most critical backlog item remains **Issue #3259** — the crate publishing gap. Given that PR #3708 also exists to publish a new release containing breaking changes and fixes, the actual bottleneck appears to be in the release automation or maintainer approval process rather than code readiness. This deserves urgent attention as it blocks the entire crate-based downstream ecosystem.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for June 11, 2026.

---

### LobsterAI Project Digest: 2026-06-11

**1. Today's Overview**
The project experienced a burst of activity with 23 Pull Requests updated in the last 24 hours (3 open, 20 closed/merged) and a new release cut yesterday. The high number of recent merges indicates a focused effort to consolidate a stable release (`2026.6.8`), while the team is already preparing the next feature set with a prominent open PR for a "Computer Use MVP." A significant batch of older (stale) PRs were also closed, suggesting a cleanup of the backlog to prepare for this new development phase.

**2. Releases**
- **Version:** [LobsterAI 2026.6.10](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.10)
- **Release Date:** June 10, 2026
- **Key Changes:**
    - `feat(data-migration)`: Added user data backup and restore functionality.
    - `feat(auth)`: Introduced a local callback login flow.
    - `feat(settings)`: Surface OpenCla... (truncated in source data)
- **Breaking Changes / Migration Notes:** Not explicitly mentioned. The data backup and restore feature implies users can protect their configuration, but no mandatory migration steps were detailed.

**3. Project Progress**
Today saw the culmination of several feature streams. Key advancements include:
- **Data Migration & Backup:** Merged via [PR #2125](https://github.com/netease-youdao/LobsterAI/pull/2125) and bundled in release 2026.6.8 ([PR #2140](https://github.com/netease-youdao/LobsterAI/pull/2140)).
- **Task Notifications:** The task completion notification system was refined to restore the main window on task finish and handle macOS notification center clicks ([PR #2134](https://github.com/netease-youdao/LobsterAI/pull/2134)).
- **UI Polishing:** Code block styling was modernized with One Dark/Light themes, and model selector styling was refined ([PR #2139](https://github.com/netease-youdao/LobsterAI/pull/2139)).
- **Bug Fixes:** A critical fix for the Windows in-app update mechanism was merged ([PR #2141](https://github.com/netease-youdao/LobsterAI/pull/2141)).
- **Backlog Clearance:** A large number of older PRs (from April 2-7) were finally closed, including a fix for disabled skills being injected into prompts ([PR #1485](https://github.com/netease-youdao/LobsterAI/pull/1485), [PR #1501](https://github.com/netease-youdao/LobsterAI/pull/1501)) and a new session pruning feature to prevent context window overflows ([PR #1499](https://github.com/netease-youdao/LobsterAI/pull/1499)).

**4. Community Hot Topics**
- **Open PR #2143:** [feat: add computer use MVP](https://github.com/netease-youdao/LobsterAI/pull/2143)
    - **Analysis:** This is the most significant open PR, prepared for merge into a `release/2026.6.11` branch. It suggests the next major feature focus is enabling the AI to control the user's computer (a "Computer Use" or CUA-style feature). This is a high-impact, forward-looking feature that will likely generate significant discussion once its code is finalized.

**5. Bugs & Stability**
No new bugs or crashes were reported in the last 24 hours. However, several older fixes were recently merged, indicating past stability concerns have been resolved:
- **High Severity:** Fixed an issue where **disabled skills** were still being invoked in cowork chats ([PR #1485](https://github.com/netease-youdao/LobsterAI/pull/1485), [PR #1501](https://github.com/netease-youdao/LobsterAI/pull/1501)).
- **Medium Severity:** Fixed the **Windows in-app update** process ([PR #2141](https://github.com/netease-youdao/LobsterAI/pull/2141)).
- **Medium Severity:** Fixed the **NSIS destructive init** (installer issue) and redesigned the engine loading page for Windows ([PR #2142](https://github.com/netease-youdao/LobsterAI/pull/2142)).
- **Low Severity:** Fixed scheduled task notification channels not updating after an edit ([PR #1490](https://github.com/netease-youdao/LobsterAI/pull/1490)).

**6. Feature Requests & Roadmap Signals**
- **Near-Term (Likely next release):** The **Computer Use MVP** ([PR #2143](https://github.com/netease-youdao/LobsterAI/pull/2143)) is being prepared for a `release/2026.6.11` branch, strongly signaling it will be the headline feature of the next version.
- **On the Horizon:** The recently merged **session pruning** ([PR #1499](https://github.com/netease-youdao/LobsterAI/pull/1499)) indicates a focus on long-running session reliability, which is a prerequisite for more autonomous or "computer use" agents. The **Markdown editor for Agent guides** ([PR #1503](https://github.com/netease-youdao/LobsterAI/pull/1503)) suggests continued investment in user customization and configuration UX.

**7. User Feedback Summary**
While direct user comments are not present, the project's code changes offer a proxy for user pain points:
- **Pain: Disabled skills still working.** This was fixed ([PR #1485](https://github.com/netease-youdao/LobsterAI/pull/1485), [PR #1501](https://github.com/netease-youdao/LobsterAI/pull/1501)), showing users expect explicit configuration to be honored.
- **Pain: Changes not persisting.** A fix ensures that saving a skill list in the Agent settings immediately syncs to the current session ([PR #1505](https://github.com/netease-youdao/LobsterAI/pull/1505)).
- **Pain: Windows-specific issues.** The dedicated fixes for NSIS installer, Windows updates, and a "close button" behavior configuration ([PR #1497](https://github.com/netease-youdao/LobsterAI/pull/1497)) highlight a clear user desire for a polished, native-feeling Windows experience.
- **Pain: Long conversations breaking.** The new session pruning feature ([PR #1499](https://github.com/netease-youdao/LobsterAI/pull/1499)) directly addresses a critical user workflow failure.

**8. Backlog Watch**
- **[Open PR #1277 (dependabot):](https://github.com/netease-youdao/LobsterAI/pull/1277)** Bumping `electron` from 40.x to 42.x. This PR has been open since April 2, 2026. A major Electron version bump is a significant dependency update that requires rigorous testing. Its long-open status could be a potential risk for security or compatibility if not merged soon, but it was recently updated, suggesting maintainers are reviewing it.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-11

## Today's Overview
Project activity is very low today, with only one new issue opened and no pull requests or releases. The issue is a minor bug report regarding a provider configuration error, which suggests the project may be in a stable or quiet maintenance phase. No merged PRs or closed issues were recorded in the last 24 hours. Overall, the project shows minimal community engagement or development activity today. Maintainers may benefit from reviewing the open issue and engaging with the reporter.

## Releases
No new releases were published today. The latest release remains unchanged.

## Project Progress
No pull requests were merged or closed in the last 24 hours. No feature advancements, fixes, or code changes were recorded.

## Community Hot Topics
The only active item is:
- **[Issue #1114 – [Bug]: provider 'coqui' not configured](https://github.com/moltis-org/moltis/issues/1114)** (opened 2026-06-10, updated 2026-06-10, 0 comments, 0 reactions)  
  This is a new, unreviewed bug report with no community discussion yet. The underlying issue appears to be that the Coqui provider is missing or misconfigured, possibly due to recent changes in the TTS module or API key handling. No maintainer response has been recorded.

## Bugs & Stability
One bug was reported today, ranked as **minor**:
- **Issue #1114**: `provider 'coqui' not configured` – User reports that the Coqui text-to-speech provider is not recognized or configured, despite using the latest version. The reporter states they have searched existing issues and are using the latest version. No fix PR exists yet. Severity is low as this likely affects a specific feature (TTS) and may be configuration-related.

## Feature Requests & Roadmap Signals
No feature requests were submitted today. The bug report does not imply any new feature direction. The project roadmap remains unclear from today's activity.

## User Feedback Summary
Only one user interaction was recorded today. The reporter (vvuk) appears to be actively using Moltis and encountered a provider setup issue, indicating real-world use of the TTS/speech features. They have followed the bug reporting guidelines, suggesting a generally positive engagement attitude. No satisfaction or dissatisfaction signals beyond the bug report.

## Backlog Watch
No long-unanswered issues or PRs exist in today's data. The only open issue (#1114) is less than 24 hours old and does not yet require escalation. No items require immediate maintainer attention.

---

**Overall Assessment:** The project is in a low-activity state with only one minor bug report. No regression, crash, or high-severity issues are present. Community engagement is minimal, and no development push is visible. The project appears stable but may need renewed attention to sustain contributor momentum.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-11

## Today's Overview
CoPaw shows **high activity** today with **49 PRs and 36 Issues updated** in the last 24 hours, culminating in the **v1.1.11 release**. The project closed **17 issues** and merged/closed **30 PRs**, indicating strong maintenance velocity. The release cycle appears to have stabilized a **v1.1.11 stable** after a beta phase, with the team actively addressing SSL certificate regressions on Windows, DingTalk AI Card bugs, and session management issues. Community engagement remains robust, with Chinese-language users reporting several real-world deployment pain points. The project is also laying groundwork for significant architectural evolution — including an **AgentScope 2.0 migration** and a **Runtime 2.0 modular redesign**.

---

## Releases
**Two new releases** shipped:
- **v1.1.11** (stable) — Includes **Free Model OAuth** for zero-config free models with one-click authentication ([#5049](https://github.com/agentscope-ai/QwenPaw/pull/5049)) and **Xiaomi MiMo Token Plan** as a built-in provider ([#4722](https://github.com/agentscope-ai/QwenPaw/pull/4722)).
- **v1.1.11-beta.3** — Contains CI workflow cleanup ([#5056](https://github.com/agentscope-ai/QwenPaw/pull/5056)), **self-evolving skill creation** enhancement ([#4857](https://github.com/agentscope-ai/QwenPaw/pull/4857)), and additional skill improvements.

**Breaking changes**: None reported.
**Migration notes**: No special migration steps documented.

---

## Project Progress
Key merged/closed PRs from the last 24 hours:

**Bug Fixes & Stability**
- [#5082](https://github.com/agentscope-ai/QwenPaw/pull/5082) — Pin `aiohttp<=3.14.0` to fix Windows build SSL errors from aiohttp 3.14.1 regressions
- [#5083](https://github.com/agentscope-ai/QwenPaw/pull/5083) — Use `certifi` CA bundle for Windows build verification
- [#5084](https://github.com/agentscope-ai/QwenPaw/pull/5084) — Compile-check discord after conda-unpack for Windows packaging
- [#5079](https://github.com/agentscope-ai/QwenPaw/pull/5079) — Surface original API error reason in user-facing messages (was buried in temp JSON files)
- [#5081](https://github.com/agentscope-ai/QwenPaw/pull/5081) — Allow previewing files outside workspace in File Guard

**DingTalk Channel Fix**
- [#5061](https://github.com/agentscope-ai/QwenPaw/pull/5061) — Remove AI Card pre-creation to prevent sending empty cards when Agent output is empty

**Authentication**
- [#4858](https://github.com/agentscope-ai/QwenPaw/pull/4858) — Add agent-scoped Web Console accounts (per-agent credentials)

---

## Community Hot Topics
The following issues attracted the most community engagement (sorted by comment count):

1. **#4342** — [CLOSED] Local models + providers + tunnel + utils unit test coverage (Phase 5) — 11 comments. Backend test coverage milestone work wrapping up.

2. **#4727** — [OPEN] **[Breaking Change]** Migrate backend from AgentScope 1.x to AgentScope 2.0 — **8 comments, 2 👍**. This is a significant architectural upgrade that will affect the entire project stack. The community is watching closely as it will change APIs and runtime behavior.

3. **#4878** — [CLOSED] **[Bug]** WeChat push delivery failure for scheduled tasks — **7 comments**. Root cause identified in `channel.py` `to_handle_from_target` logic for WeChat integration.

4. **#5064** — [OPEN] **[Bug]** Agent-generated scheduled tasks fail to trigger and cannot be manually edited — **5 comments**. A usability-critical issue where AI-created timers are non-functional and uneditable.

5. **#4989** — [CLOSED] **[Bug]** v1.1.9/v1.1.10 no response with locally deployed Qwen 3.6-27B — **5 comments**. Model connection regression affecting users who upgraded from v1.1.5.post2.

**Underlying needs**: Community is pushing for **better reliability of agent-created artifacts** (scheduled tasks), **smoother model integration** (especially local/self-hosted models), and **cross-platform stability** as new OS releases (macOS 26.5, Windows updates) introduce breaking environmental changes.

---

## Bugs & Stability
High-severity bugs reported or active today:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **CRITICAL** | [#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086) | **OpenSSL 3.5 regression** blocks Desktop startup. Python 3.10 + OpenSSL 3.5.7 fails on DER certificate parsing, crashes backend before HTTP ready | [🔍 Open](https://github.com/agentscope-ai/QwenPaw/pull/5086) |
| **HIGH** | [#5082](https://github.com/agentscope-ai/QwenPaw/issues/5082) | aiohttp 3.14.1 module-level SSL context creation corrupts Windows builds | ✅ Merged: pin to ≤3.14.0 |
| **HIGH** | [#5052](https://github.com/agentscope-ai/QwenPaw/issues/5052) | **Tool call keyword argument regression**: after several rounds, all tools fail with `got an unexpected keyword argument 'arguments'` | 🔍 Open |
| **MEDIUM** | [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) | Agent-generated scheduled tasks not triggerable/editable | 🔍 Open |
| **MEDIUM** | [#5031](https://github.com/agentscope-ai/QwenPaw/issues/5031) | Skill slash invocation shows expanded SKILL.md content instead of clean output | 🔍 Open |
| **LOW** | [#4993](https://github.com/agentscope-ai/QwenPaw/issues/4993) | Image preview jitter when zoomed and dragged (macOS 26.5) | Closed (partial fix?) |

**Build stability**: Three PRs ([#5082](https://github.com/agentscope-ai/QwenPaw/issues/5082), [#5083](https://github.com/agentscope-ai/QwenPaw/issues/5083), [#5084](https://github.com/agentscope-ai/QwenPaw/issues/5084)) were dedicated to fixing Windows CI build failures from SSL certificate store corruption — indicating **environmental fragility** in the build pipeline that merits attention.

---

## Feature Requests & Roadmap Signals
New user-requested features surfaced today:

1. **#4992** — **[Feature]: Support independent visual model fallback** (4 comments, 1 👍). User wants a separate `visual_model` config so text-only LLMs (e.g., DeepSeek-v4-flash) can still process images via an auxiliary vision model. **Likelihood for next release**: Medium — solves a common user workflow gap.

2. **#5063** — **[Feature]: Integrate Headroom context compression** (2 comments). Proposes integrating an optional local-first compression layer claiming 60–95% token reduction. **Likelihood**: Low — requires careful evaluation of compression quality.

3. **#4887** — **[Feature]: Add custom endpoint support for DingTalk private deployment** (2 comments). Enterprise user needs private DingTalk API endpoints. **Likelihood**: Medium — aligns with enterprise roadmap.

4. **#4356** — **[Feature]: Finer granular control for File Guard and Tool Guard** (2 comments). User wants read-only access for some directories, whitelist support. **Likelihood**: Medium — complements existing security infrastructure.

**Predictions for v1.1.12**: The **independent visual model** configuration and **DingTalk private endpoints** have the most momentum and address clear user pain points.

---

## User Feedback Summary
Real user experiences captured from issues:

**Pain Points**:
- **Windows Tauri desktop performance degrades** with >3 sessions open (10-second switch delays) ([#5053](https://github.com/agentscope-ai/QwenPaw/issues/5053))
- **Mobile/phone browser access** to desktop control panel fails even with firewall disabled ([#4960](https://github.com/agentscope-ai/QwenPaw/issues/4960))
- **Long conversation history causes UI hangs** because entire session is re-fetched on every tab switch ([#4917](https://github.com/agentscope-ai/QwenPaw/issues/4917))
- **Sub-agent task invisibility**: `spraw_subagent` started tasks show no progress and incomplete history ([#4923](https://github.com/agentscope-ai/QwenPaw/issues/4923))
- **`write_file` output not streamed** in Web UI — long file generations appear as "loading" with no feedback ([#4865](https://github.com/agentscope-ai/QwenPaw/issues/4865))

**Satisfaction Signals**:
- Multiple closed bugs indicate **responsive maintainers** — WeChat push, local model regression, and shell command popup issues were addressed quickly.
- **DingTalk AI Card empty card bug** ([#5057](https://github.com/agentscope-ai/QwenPaw/issues/5057)) was fixed within 24 hours ([#5061](https://github.com/agentscope-ai/QwenPaw/pull/5061)).

**Common themes**: Users want **better streaming and real-time feedback** for long-running operations, **seamless cross-platform network access**, and **stability across OS updates**.

---

## Backlog Watch
Issues and PRs needing maintainer attention:

| Age | Issue/PR | Status | Concern |
|-----|----------|--------|---------|
| ~49 days | **#3751** — [ENH] System tray icon for Windows desktop | OPEN, 3 comments | Simple UX enhancement that would greatly improve desktop feel; no maintainer response |
| ~28 days | **#4356** — Finer File Guard control | OPEN, 2 comments | Reviewed but no progress; important for enterprise security |
| ~16 days | **#4727** — AgentScope 2.0 backend migration | OPEN, **Breaking Change**, 2👍 | Major architectural shift; community waiting for migration plan |
| ~9 days | **#4865** — write_file not streaming | OPEN, 2 comments | Clear UX pain point affecting all file-generating workflows |
| ~1 day | **#5088** — Governance & sandbox interface discussion | OPEN | **Interesting: two PRs exist** ([#5087](https://github.com/agentscope-ai/QwenPaw/issues/5087) closed, [#5088](https://github.com/agentscope-ai/QwenPaw/issues/5088) open) — suggests active but possibly stalled governance work |

**Watch items**: The **AgentScope 2.0 migration** (1.1.11 has a PR at [#5078](https://github.com/agentscope-ai/QwenPaw/issues/5078) titled "Runtime 2.0 modular architecture") could stall if not carefully coordinated. The **Desktop auto-updater PR** ([#4669](https://github.com/agentscope-ai/QwenPaw/issues/4669), open since May 25) would significantly improve user experience on Tauri desktop.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is your ZeroClaw project digest for June 11, 2026.

---

### ZeroClaw Project Digest - 2026-06-11

#### 1. Today's Overview
High velocity continues across the ZeroClaw project, with 42 issues and 50 pull requests updated in the last 24 hours. The maintainer team is executing aggressively on a bug-fix and stabilization sprint, particularly around the runtime, gateway, and provider stack. Seven new issues were opened today, primarily bug reports, while an equal number of fixes were landed or merged. The project remains in a heavy development phase with no new releases in the period, but significant architectural discussions (RFCs) and critical fixes are moving toward the upcoming v0.8.1 and v0.8.2 milestones.

#### 2. Releases
No new releases were published in the last 24 hours. The project appears to be stabilizing between releases, with the majority of current activity focused on merging fixes and preparing for the next package builds.

#### 3. Project Progress
Only one PR was closed today: **PR #7446**, which fixes a critical bug where `image_info` tool output failed to reach multimodal/vision models in most common scenarios. This was a high-risk, high-priority fix targeting the runtime and provider components.

Active PR momentum is focused on stability:
- **PR #7471** (open): Fixes config list filtering to use segment-boundary matching instead of simple string prefixes, preventing cross-contamination of agent settings in the TUI.
- **PR #7443** (open): A governance/housekeeping PR that updates CODEOWNERS to reflect departing and new maintainers.
- **PR #7464** (open): Changes the default MCP config so configured MCP servers are enabled by default, with an explicit disable flag for those who don't need it.

#### 4. Community Hot Topics
The most active community discussions this period:

- **#4710 - A Better LOGO for ZeroClaw (CLOSED)**
  - *Summary:* A feature request for a new logo design from contributor `mastwet`.
  - *Notes:* The most commented issue this period (20 comments, 2 👍). The discussion appears to have concluded with the issue being closed, suggesting a new visual identity has been settled on. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/4710)

- **#3642 - Provide a "full" Docker image (OPEN)**
  - *Summary:* A long-standing request for a feature-complete Docker image that includes all flags (e.g., WhatsApp), reducing the barrier for non-technical users.
  - *Notes:* High engagement (12 comments, 3 👍). This is a known pain point for new users and remains a priority P2 request. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/3642)

- **#6034 - Bug: Single/multi-turn conversations losing user messages (OPEN)**
  - *Summary:* A Chinese-language bug report where `custom:http` provider calls result in all providers failing with a 400 error.
  - *Notes:* This is classified as a P1, risk-high bug blocking user workflows. The error suggests a prompt formatting issue with specific backends (Qwen3.5-35B). [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6034)

#### 5. Bugs & Stability
New bug reports from today, ranked by severity:

- **S1 - Workflow Blocked:**
  - **#7470**: Delegate agentic mode rejects empty `risk_profile.allowed_tools`, preventing multi-agent setups from functioning. This is a critical block for agentic delegation patterns.
  - **#7263**: Subagents in ACP sessions don't inherit `cwd`, breaking workflows that rely on workspace context. A fix is likely still in progress.

- **S2 - Degraded Behavior:**
  - **#7436**: The `image_info` tool only works with absolute POSIX paths; relative paths silently fail. A fix was merged in **PR #7446** earlier today.
  - **#7469**: A minor TUI issue where the default editor is set to `vi`, which is not included in the container image.

- **S3 - Minor:**
  - **#7469** (listed above also covers the severity): A configuration mismatch between the default TUI setting and the container's available software.

#### 6. Feature Requests & Roadmap Signals
Two new feature requests and two major RFCs are shaping the future of ZeroClaw:

- **#7467** (new): Request for arrow-key navigation when editing strings in the TUI, improving the text-editing UX. Likely a small, quick-win feature for the next point release.
- **#7468** (new): Request to allow renaming aliases in the TUI (for agents, model providers, MCP servers). Given the upcoming TUI improvements, this is a strong candidate for inclusion in v0.8.1.
- **#7415** (RFC): "Unify the three agent turn engines" - A major architecture RFC proposing consolidation of `run_tool_call_loop`, `turn_streamed`, and `Agent::turn`. This could be a cornerstone for v0.8.1's stability improvements.
- **#7420** (RFC): "Native Dynamic-Library Plugin System" - An ambitious RFC detailing a move away from monolithic builds towards a WASM-based plugin architecture for v0.8.2. This signals a major shift in ZeroClaw's extensibility model.

#### 7. User Feedback Summary
Real user sentiment from this period indicates:

- **Configuration friction:** Users are hitting multiple configuration-related bugs, including missing port fields in the quickstart wizard (PR #7215) and config-list filtering issues (PR #7471). The onboarding experience still has rough edges.
- **Vision model pain points:** The `image_info` tool bug (fixed today) was causing significant frustration for users trying to work with multimodal models. The PR comments suggest another contributor actively tested and verified the fix, indicating a responsive maintainer cycle.
- **Containerization needs:** The persistent demand for a "full" Docker image (Issue #3642) shows that while ZeroClaw is powerful, its out-of-the-box experience for new or non-technical users is a barrier to adoption.

#### 8. Backlog Watch
The following issues remain open for a concerningly long time without sufficient maintainer action:

- **#3642 - Provide a "full" docker image (OPEN, since Mar 15)**
  - *Priority:* P2 | *Comments:* 12 | *Status:* Blocked/Accepted
  - *Notes:* One of the most popular feature requests. It has the "status:blocked" tag, but no clear path to resolution has been communicated. Active engagement and a status update would be appreciated by the community. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/3642)

- **#6165 - RFC: Prefer a lighter ZeroClaw core through external integrations (OPEN, since Apr 27)**
  - *Priority:* P2 | *Comments:* 4 | *Status:* Blocked/Accepted
  - *Notes:* This is a foundational architectural RFC that parallels the newer #7420 RFC. It suggests removing hard-coded integrations (Jira, GitHub CLI) in favor of skills or plugins. The RFC has been "blocked" for over a month without clear movement, despite being central to the project's future architecture. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*