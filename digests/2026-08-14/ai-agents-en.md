# OpenClaw Ecosystem Digest 2026-08-14

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-14 00:54 UTC

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

# OpenClaw Project Digest — 2026-08-14

## 1. Today's Overview

OpenClaw is experiencing a period of intense community activity driven by a growing backlog of reliability issues around message delivery, subagent orchestration, and session-state integrity. With 500 issues and 500 PRs updated in the last 24 hours, the project shows clear signs of scaling pains typical of a rapidly adopted agent framework. Notably, **zero new releases** were published, leaving the maintainer team in catch-up mode as they review a wave of incoming fixes, including several contributing directly to long-standing bugs. The most prominent concerns converge on silent reply/session failures that erode user trust, while the UI continues to receive steady polish to keep pace with gateway feature growth.

## 2. Releases

*No new releases were published in the last 24 hours.*

The absence of new versions is notable, especially amid a growing number of issues and PRs marked as "needs-maintainer-review." This suggests the team is prioritizing stabilization and review over shipping new features, likely holding the branch for a consolidation release.

## 3. Project Progress

Today's merged/closed PRs skew toward internal tooling and hard bug fixes, indicating a strong push to stabilize the codebase after the recent feature-heavy period.

- **PR #123208** *(Closed, P1)* — **fix(gateway): models.list returns empty forever while chat works (owner binding-flag mismatch)**. Fixed a critical bug where the Control UI composer permanently displayed "No models available" and `models.list` returned empty arrays, which also caused CPU burn by rebuilding the model cache.
- **PR #123381** *(Closed)* — **fix(ui): create automations for selected agent in all-agents view**. Prevents an `AgentSelectionRequiredError` when switching page scope to "All agents" while a specific agent is selected.
- **PR #123392** *(Closed)* — **fix(ci): restore unique Codex test shard ownership**. Resolves a CI audit failure caused by a test file being registered in two Vitest shards.
- **PR #123400** *(Open)* — **fix(ci): restore Codex state test shard owner after merge drift**. CI hygiene continues as concurrent PRs caused ownership drift.
- **PR #123399** *(Open)* — **fix: install externalized configured plugins during upgrades**. Aims to prevent missing companion plugin installs when upgrading a packaged install.
- **PR #123397** *(Open)* — **fix(openai): unify server-side compaction gates and harden compaction recovery**. Fixes two disagreeing definitions of "server-side compaction is enabled," improving recovery paths.

## 4. Community Hot Topics

- **Issue #121058** — *Silent reply failures still recurring after #116277 closed — no queued reply payload* (92 comments). The most active issue demonstrates a systemic problem: the original fix was closed, but the monitoring cron continues to log new failures. **[Open Issue](https://openclaw/openclaw Issue #121058)**
- **Issue #7707** — *Feature Request: Memory Trust Tagging by Source* (48 comments). A prolific, long-running feature suggestion to tag memory by provenance to prevent "memory poisoning." The issue remains open, awaiting product decision. **[Open Issue](https://openclaw/openclaw Issue #7707)**
- **Issue #25592** — *Text between tool calls leaks to messaging channels* (48 comments). A UX-damaging bug where internal agent narration is broadcast to users, highlighting a need for better output-stream hygiene. **[Open Issue](https://openclaw/openclaw Issue #25592)**
- **Issue #91363** — *Isolated cron consistently fails with "LLM request failed"* (10 comments, 👍 6). A high-impact bug for automation users, indicating reliability gaps in the cron subsystem. **[Open Issue](https://openclaw/openclaw Issue #91363)**
- **Issue #16555** — *Add TTL/Expiry for Delivery Queue Messages* (6 comments). A feature request aligned with several "stale message delivery" bugs, suggesting it may be prioritized in the near term.

The common thread across today's top conversations is **"silent failure"** — the system needs to either reliably deliver a reply or fail in a way users can see and recover from, rather than dropping messages without notice.

## 5. Bugs & Stability

The following bugs are ranked by severity based on impact and community response. Notably, several have fix PRs open or in review.

| Severity | Issue | Summary | Fix PR? |
| :--- | :--- | :--- | :--- |
| **Critical** | [#121058](https://openclaw/openclaw Issue #121058) | Silent reply failures still recurring after #116277 closed — no queued reply payload; monitoring cron continues to log new occurrences. | No |
| **High** | [#44925](https://openclaw/openclaw Issue #44925) | Subagent completion silently lost — no retry, no notification, no auto-restart on timeout. | No |
| **High** | [#67777](https://openclaw/openclaw Issue #67777) | Subagent completion delivery can be lost on direct-announce timeout, drain, or orphan prune. | No |
| **High** | [#91363](https://openclaw/openclaw Issue #91363) | Isolated cron consistently fails with "LLM request failed" / timed out; model requests never reach provider. | No |
| **High** | [#121953](https://openclaw/openclaw Issue #121953) | Cron agent turn stalls on DeepSeek because the `[cron:...]` prefix is deprioritized by the API edge. | No |
| **Medium** | [#123073](https://openclaw/openclaw Issue #123073) | Dev-channel update fails with `EUNSUPPORTEDPROTOCOL` due to `workspace:*` deps (pnpm-only). | No |
| **Medium** | [#105342](https://openclaw/openclaw Issue #105342) | *(Closed)* All exec command outputs rendered as images on Telegram, not text; fixed. | Yes |
| **Medium** | [#121605](https://openclaw/openclaw Issue #121605) | *(Closed)* After model fallback, assistant reply produced but never delivered to channel. | Yes |

There is a clear trend of **message-delivery assurance** as a systemic weak point across subagent orchestration, cron, and fallback paths. The high volume of these issues suggests a need for a more robust, unified delivery queue with retry guarantees.

## 6. Feature Requests & Roadmap Signals

- **Memory Trust Tagging by Source** ([#7707](https://openclaw/openclaw Issue #7707)) — A "diamond lobster"-rated issue that has been open for six months with 48 comments. The need to prevent memory poisoning is likely to be addressed in a future security-focused release.
- **Delivery Queue TTL/Expiry** ([#16555](https://openclaw/openclaw Issue #16555)) — The recent surge in delivery-related bugs makes this a strong candidate for inclusion in an upcoming reliability patch, as it provides a straightforward remedy for stale/duplicate messages.
- **Built-in Pace-Aware Rate Limiting** ([#45771](https://openclaw/openclaw Issue #45771)) — As more users run autonomous agents, this feature to prevent API rate-limit burn will become increasingly critical.
- **YAML Config Support** ([#45758](https://openclaw/openclaw Issue #45758)) — A user-experience enhancer that lowers the barrier for adoption among DevOps-centric users; may land as a minor priority (P3) feature.
- **Self-Hosted STT/TTS in Webchat** ([#45508](https://openclaw/openclaw Issue #45508)) — A privacy-sensitive feature request, currently P2, with 2 👍. This could move up if the maintainers prioritize native voice setups.

The maintainer team appears to be focusing on **reliability bugs** before **new features**, but the persistent demand for roadmap items like memory trust and rate limiting will likely inform the next big feature push and help stem the flow of new bug reports.

## 7. User Feedback Summary

Real user pain points remain consistent and indicate a rough edge around reliability and UX.

- **Unreliable Reply Delivery**: The most common pain point is the **"silent reply failure"** recurring across many scenarios (subagents, cron, fallback models). Users express significant frustration that their conversations just stall with no error or retry, making the agent seem broken.
- **Session Pollution**: Users (e.g., in [#41165](https://openclaw/openclaw Issue #41165)) are frustrated by messages from direct channels (Telegram) landing in the main session, polluting the global session state, a problem that persists despite prior fixes.
- **Configuration Complexity**: Persistent issues with `sudo openclaw update` creating mixed file ownership ([#78493](https://openclaw/openclaw Issue #78493)) and the inability to configure certain defaults (e.g., `--deliver`, [#33102](https://openclaw/openclaw Issue #33102), `session.resetPrompt`, [#45501](https://openclaw/openclaw Issue #45501)) frustrate advanced users.
- **Memory Management Confusion**: Users report that memory is managed inconsistently across installations (e.g., chunking vs. not, [#43747](https://openclaw/openclaw Issue #43747)), leading to confusion and unpredictable agent behavior.

While the user base is deeply technical and often provides detailed bug reports with repro scripts, the recurring nature of the delivery bugs indicates that **reliability is the biggest source of user dissatisfaction**.

## 8. Backlog Watch

- **Issue #7707** — *Memory Trust Tagging by Source* (since Feb 2026, 48 comments). The `clawsweeper:needs-maintainer-review` label is overdue for a decision. This feature would significantly improve security posture. **[Watch](https://openclaw/openclaw Issue #7707)**
- **Issue #25592** — *Text between tool calls leaks to messaging channels* (since Feb 2026, 48 comments). A long-standing UX bug that is likely affecting many users; awaiting maintainer review. **[Watch](https://openclaw/openclaw Issue #25592)**
- **Issue #44925** — *Subagent completion silently lost* (since Mar 2026, 27 comments). The repeated emergence of subagent delivery bugs suggests the core architecture is not robust; a maintainer review is critical. **[Watch](https://openclaw/openclaw Issue #44925)**
- **Issue #45758** — *YAML config support* (since Mar 2026, 8 comments). A low-priority but often-requested feature that continues to gather interest (👍 2). **[Watch](https://openclaw/openclaw Issue #45758)**

*Note: The label system (`clawsweeper:no-new-fix-pr` etc.) suggests an automated issue-management bot is present, but these issues remain in the queue waiting for human maintainers to pick them up.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report
**AI Agent & Personal Assistant Open-Source Ecosystem — 2026-08-14**

---

## 1. Ecosystem Overview

The open-source AI agent landscape is undergoing a **reliability-focused maturation phase**, with top-tier projects prioritizing delivery assurance, session-state integrity, and security hardening over raw feature velocity. Message-delivery guarantees, subagent orchestration robustness, and memory management trust emerge as cross-cutting concerns across all active projects. Concurrently, a significant architectural shift toward **pluggable agent loops and provider-agnostic harnesses** is underway (IronClaw, ZeroClaw), signaling movement from monolithic agent frameworks toward composable kernels. The ecosystem is bifurcating into **general-purpose assistants** (OpenClaw, CoPaw, NanoBot) and **infrastructure/platform plays** (IronClaw, ZeroClaw), with community expectations increasingly focused on production-grade reliability, security boundaries, and operational transparency.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score* | Primary Focus |
|:--------|:---:|:---:|:---:|:---:|:---|
| **OpenClaw** | 500 | 500 | No release; consolidation pending | ⚠️ Fair | Reliability stabilization |
| **CoPaw** | 42 | 50 | **v2.1.0** (OS Shell) | 🟡 Stable w/ flags | Feature expansion + security |
| **IronClaw** | 50 | 50 | **v1.2.0** (stable) | ✅ Strong | Architectural rework (pluggable loops) |
| **ZeroClaw** | 50 | 50 | None; targeting v0.9.0 | ✅ Strong | RFC-driven design + security |
| **Hermes Agent** | 50 | 50 | **v0.20.1** (patch) | 🟡 Stable w/ flags | Bug fixes + webhook overhaul |
| **NanoBot** | 12 | 31 | None | ⚠️ Fair-to-positive | Crash-resilience data fixes |
| **NanoClaw** | — | 19 (13 merged) | **v2.2.0** | ✅ Strong | CI security-gated pipeline |
| **LobsterAI** | 0 | 6 merged | None | 🟡 Moderate | UI/UX consolidation |
| **Moltis** | 1 | 4 open | None | 🟡 Moderate | Connector durability (CalDAV, channels) |
| **PicoClaw** | 0 | 9 (8 Dependabot) | None (last: 0.3.1) | ⚠️ Moderate | Dependency hygiene; stagnant features |
| **NullClaw** | — | — | — | ⚪ Inactive | — |
| **TinyClaw** | — | — | — | ⚪ Inactive | — |
| **ZeptoClaw** | — | — | — | ⚪ Inactive | — |

*\*Health score is a composite of velocity, maintainer responsiveness, fix turnaround, and community sentiment.*

---

## 3. OpenClaw's Position

**Advantages over peers:**
- **Largest community scale**: 500/500 issues/PRs updated in 24h dwarfs all peers, indicating the widest adoption and most active contributor base.
- **Ecosystem centrality**: Multiple projects (Moltis, LobsterAI) explicitly track upstream OpenClaw changes, positioning it as a reference implementation for the broader agent framework ecosystem.
- **Subagent orchestration maturity**: Despite delivery bugs, OpenClaw's subagent architecture is the most mature in the ecosystem, with peers (NanoBot, CoPaw) still addressing basic session isolation.

**Technical approach differences:**
- **Gateway-centric delivery**: OpenClaw's messaging-gateway architecture is more channel-first than IronClaw's kernel model or NanoBot's consolidation-driven approach.
- **Configuration complexity**: YAML/TOML-driven configurability is more extensive than CoPaw's UI-first approach, attracting DevOps-savvy users but creating ergonomic friction.

**Community size comparison:**
- OpenClaw's issue volume is **10× the next-most-active projects** (IronClaw, ZeroClaw, Hermes at 50), confirming dominant mindshare. However, the **maintainer-to-issue ratio is the ecosystem's worst**, with 500 issues updated and zero releases shipped, creating a backlog bottleneck that could erode its leadership position if left unaddressed.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|:---|:---|:---|
| **Delivery assurance/retry** | OpenClaw, Hermes, CoPaw, NanoBot | Silent reply failures, subagent completion loss, cron job death, fallback delivery gaps |
| **Session-state integrity** | OpenClaw, Hermes, NanoBot, CoPaw | History corruption, session pollution from direct channels, context compression visibility, lost streamed answers |
| **Memory trust & governance** | OpenClaw, ZeroClaw, LobsterAI, NanoBot | Memory poisoning prevention, lifecycle policy decoupling from storage, schema-validated consolidation |
| **Security boundaries (auth/permissions)** | OpenClaw, ZeroClaw, CoPaw, NanoClaw | Pairing lockout flaws, plugin permission gaps, unauthenticated API exposure, shell command confirmation tiers |
| **Cron/automation reliability** | OpenClaw, NanoBot, Hermes, IronClaw | Silent cron death, timezone handling, per-run session isolation, dead-model pinning |
| **Supply-chain/CI security** | NanoClaw, ZeroClaw, IronClaw | Signature-verified image promotion, dependency hygiene, CodeQL false-positive suppression |
| **MCP ecosystem integration** | NanoBot, IronClaw, PicoClaw, CoPaw | Schema budget management, plugin MCP working-directory support, metadata passthrough, connector durability |
| **Cross-platform hardening** | Hermes, CoPaw, NanoBot, Moltis | Windows GBK encoding crashes, macOS bash 3.2 compatibility, path mangling in Docker |

---

## 5. Differentiation Analysis

| Differentiator | OpenClaw | IronClaw | ZeroClaw | CoPaw | NanoBot | Hermes |
|:---|:---|:---|:---|:---|:---|:---|
| **Primary target user** | Individual power users | Enterprise/cloud operators | Production/security-conscious teams | Chinese-market prosumers | Local-first developers | CLI/TUI-first developers |
| **Core architecture** | Channel-gateway + subagents | Kernel with pluggable harnesses | Runtime-owned sessions + RFC governance | Desktop app + OS Shell | WebUI + consolidation | Session/agent loop + skills |
| **Key differentiator** | **Scale & ecosystem centrality** | **Pluggable loop extensibility** | **RFC-driven design rigor** | **OS Shell UX + China integration** | **Fast-fix responsiveness** | **Streaming/first-principles stability** |
| **Deployment model** | Self-hosted (CLI/gateway) | Cloud-first, containerized | Self-hosted, infrastructure-grade | Desktop app + server | Local-first, WebUI | Docker/hosted, TUI desktop |
| **Language/stack** | TypeScript/Node.js | Go/Rust (Postgres) | Rust-heavy | Python-based | TypeScript/Node.js | TypeScript/Node.js (TUI) |
| **Security posture** | Reactive (fixing bugs) | Proactive (harness boundaries) | **Most rigorous** (RFC security cluster) | **Weakest** (open security reports) | Reactive (fast fixes) | Reactive (security PRs) |

---

## 6. Community Momentum & Maturity

### Tier 1: High-velocity, feature-forward (releasing regularly)
- **IronClaw** — Released v1.2.0, executing Reborn epic with 50/50 issue/PR volume; strong maintainer triage, clear roadmap.
- **CoPaw** — Released v2.1.0 (OS Shell); massive feature velocity (19 merged PRs) but security reports temper confidence.
- **NanoClaw** — Released v2.2.0; supply-chain-gated CI shows process maturity beyond its size.

### Tier 2: Stabilizing after growth (consolidation releases)
- **OpenClaw** — Zero releases while processing 1000 items; clearly in catch-up mode. Community trust eroding from recurring silent failures.
- **Hermes Agent** — Patch release (v0.20.1) with 656 accumulated PRs; webhook epic indicates strategic repositioning.

### Tier 3: Steady-state maintenance
- **NanoBot** — Rapid fix turnaround on critical data-loss bugs, but smaller absolute scale.
- **ZeroClaw** — Process-heavy RFC phase; high-quality design work but few shipped features.
- **LobsterAI** — UI consolidation; minimal issue traffic suggests maturing product.

### Tier 4: Stagnant or dependency-only
- **PicoClaw** — Only Dependabot PRs; unaddressed Web UI performance bug (24+ days) is a health concern.
- **Moltis** — Small but focused; connector PR signals upcoming feature velocity.
- **NullClaw, TinyClaw, ZeptoClaw** — Inactive; likely dormant or integrated into parent projects.

---

## 7. Trend Signals

### Signal 1: Reliability is the new differentiator
Recurring silent failures (OpenClaw #121058, NanoBot #5373, CoPaw #6921, Hermes #62142) indicate users are increasingly intolerant of **unpredictable agent behavior**. Across projects, the common pattern is the need for **delivery guarantees, visible failure modes, and automatic retry**. Value for developers: build **assertive failure handling** and **observable state transitions** into agent frameworks — silent drops are the #1 trust destroyer.

### Signal 2: Security is moving from afterthought to gate
ZeroClaw's RFC cluster (pairing lockout, shell command policies, credential-chain verification), NanoClaw's signature-gated CI, and CoPaw's unauthenticated-API reports collectively signal that **agent permissions and supply-chain integrity** are becoming P0 concerns. The **plugin permission model** (CoPaw #6916: silent cron creation) is emerging as a systemic gap. Value: expect **permission tiering** (allow/ask/deny) and **verifiable image promotion** to become standard features.

### Signal 3: Memory trust and provenance are unsolved
OpenClaw's six-month-old feature request for memory trust tagging (#7707) and ZeroClaw's memory lifecycle decoupling RFC (#6850) point to a **critical gap in agent memory management**. As agents persist more context, users demand: source-level trust grading, storage-backend-independent lifecycle policies, and schema-validated consolidation. Value: a **provenance-aware memory layer** is a strong differentiation opportunity.

### Signal 4: Provider fragmentation is a developer tax
DeepSeek failures (OpenClaw, Hermes), Alibaba Cloud billing support (CoPaw), QwenCloud paths (NanoBot), and broken fallback routing (Hermes cron) show **provider-specific friction is a universal pain**. Projects are converging on catalog-driven provider models with capability-aware routing (CoPaw #6302, ZeroClaw #9631). Value: invest in **provider abstraction layers** with graceful degradation and per-provider capability detection.

### Signal 5: MacOS/Windows parity is a hidden growth lever
Moltis (bash 3.2), Hermes (GBK encoding), CoPaw (Windows TUI startup crash), NanoBot (WinError 5), and PicoClaw (Web UI lag) reveal that **cross-platform robustness is under-invested**. With developer Macs and enterprise Windows, projects that solve these friction points early will win adoption in mixed-OS organizations.

### Signal 6: The "agent kernel" concept is gaining traction
IronClaw's Pluggable Agent Loops epic and ZeroClaw's runtime-owned sessions both suggest the ecosystem is moving toward **separating the agent loop from the framework**. This mirrors containerization history: the framework becomes a thin orchestrator, with external harnesses (Claude Code, codex, pi) plugged into a kernel that enforces policies and boundaries. Value: architectures that support **bring-your-own-loop** will outlast monoliths.

### Signal 7: China-market projects are a parallel ecosystem
CoPaw's Chinese-language bug reports, LobsterAI's Chinese documentation, and QwenCloud/DeepSeek integration focus signal that **China-specific UX and provider support** (Alibaba Bailian, WeChat, OneBot media) is a distinct market with high engagement but different security/compliance baselines. Developers targeting global markets should **separate channel adapters from core agent logic** to accommodate regional requirements.

---

### Bottom Line for Technical Decision-Makers

Choose **OpenClaw** for ecosystem reach and community despite reliability debt; **IronClaw** for production-grade kernel architecture with future-proof extensibility; **ZeroClaw** for security-rigorous, RFC-governed deployments; **CoPaw** for feature-rich desktop UX with strong China-market integration. Invest in **delivery guarantees, memory provenance, and pluggable harness support** — these three differentiators are consistently underserved across all active projects.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-14

## 1. Today's Overview
NanoBot showed **high activity** over the last 24 hours, with 12 issues and 31 pull requests updated. The project is in a **rapid bug-fix and feature-integration phase**, with multiple open PRs addressing session persistence, cron scheduler resilience, MCP schema budgeting, and WebUI collaboration. **No new releases** were published. The most significant cluster of work targets **data-loss and crash-resilience bugs** in session management, cron, and consolidation, alongside **feature-forward PRs** for Telegram stickers, MCP Apps metadata, and Matrix SAS verification.

## 2. Releases
No new releases in the last 24 hours. The most recent stable release remains the prior version; users tracking the above fixes should monitor the `main` branch or upcoming tags.

## 3. Project Progress
Nine PRs were **merged or closed** today (all with linked fixes):

- **[#5374](https://github.com/HKUDS/nanobot/pull/5374) / [#5375](https://github.com/HKUDS/nanobot/pull/5375) [CLOSED]**: `fix(cron): keep scheduler alive when job-store persistence fails` — address the silent cron-death bug from issue #5373. (Two attempts; the later one at #5376 remains open and is discussed below.)
- **[#5381](https://github.com/HKUDS/nanobot/pull/5381) [CLOSED]**: `feat(webui): add native workspace folder picker` — native macOS/Windows/Linux folder selection for loopback-bound, local WebUI sessions.
- **[#5384](https://github.com/HKUDS/nanobot/pull/5384) [CLOSED]**: `fix(webui): restore transcript-only session history` — re-enables sidebar discovery and deletion of transcript-only sessions without lossy reconstruction.
- **[#5306](https://github.com/HKUDS/nanobot/issues/5306) [CLOSED]**: Security advisory — `exec.allowPatterns` shell-chain bypass; closed, indicating a fix has been merged.
- **[#4556](https://github.com/HKUDS/nanobot/pull/4556) [CLOSED]**: `feat(dream): wire up model_override for Dream consolidation` (fixes #4029).
- **[#4550](https://github.com/HKUDS/nanobot/pull/4550) [CLOSED]**: `fix(cron): use per-run session key to prevent context sharing across cron runs` (fixes #4082).

**Key advances:** cron scheduler reliability, WebUI local UX, session history recovery, consolidated-config wiring, and a security fix for the `exec` tool.

## 4. Community Hot Topics
The most active discussions (defined by open issues with comments) centered on:

- **[#5373 Cron scheduler dies permanently after a single job-store persistence failure](https://github.com/HKUDS/nanobot/issues/5373)** — high severity bug, actively fixed in PR [#5376](https://github.com/HKUDS/nanobot/pull/5376).
- **[#5298 Proposal: budget model-visible MCP schemas for large tool sets](https://github.com/HKUDS/nanobot/issues/5298)** — addresses context-window cost of many MCP tools; a direct implementation PR [#5388](https://github.com/HKUDS/nanobot/pull/5388) was opened today.
- **[#4841 Matrix bot device 'untrusted' in Element](https://github.com/HKUDS/nanobot/issues/4841)** — long-standing E2EE usability issue with a proposed SAS-flow fix in PR [#5385](https://github.com/HKUDS/nanobot/pull/5385).
- **[#5289 Telegram sticker support & agent-initiated reactions](https://github.com/HKUDS/nanobot/issues/5289)** — feature request now with an open implementation PR [#5387](https://github.com/HKUDS/nanobot/pull/5387).
- **[#5251 MCP Apps host support in WebUI](https://github.com/HKUDS/nanobot/issues/5251)** — feature request with a partial fix in PR [#5386](https://github.com/HKUDS/nanobot/pull/5386), preserving MCP Apps metadata.

**Underlying needs:** Users are pushing for (a) tighter integration with the broader MCP ecosystem (schemas, apps, metadata), (b) richer channel UX (Telegram stickers, Matrix E2EE verification), and (c) robustness guarantees for unattended cron execution.

## 5. Bugs & Stability
Ranked by severity:

1. **Critical — Data loss in session archival/consolidation (NEW)**:
   - [#5378](https://github.com/HKUDS/nanobot/issues/5378): `file-cap archive failure mutates the session before persistence` — in-memory overflow discarded even when archive fails; PR [#5380](https://github.com/HKUDS/nanobot/pull/5380) restores prior state.
   - [#5377](https://github.com/HKUDS/nanobot/issues/5377): `consolidation truncates archive input but advances past the full message batch` — lossy truncation loses message suffixes; PR [#5379](https://github.com/HKUDS/nanobot/pull/5379) replaces truncation with lossless bounded chunks.

2. **High — Cron scheduler permanent death (NEW)**:
   - [#5373](https://github.com/HKUDS/nanobot/issues/5373): single persistence error kills timer. Fix PR [#5376](https://github.com/HKUDS/nanobot/pull/5376) is open.

3. **Medium — WebUI turn lifecycle (NEW)**:
   - [#5368](https://github.com/HKUDS/nanobot/issues/5368): copy/fork actions visible while agent turn still running; PR [#5357](https://github.com/HKUDS/nanobot/pull/5357) cancels active turns before session deletion.

4. **Medium — Windows session save crash (NEW)**:
   - PR [#5382](https://github.com/HKUDS/nanobot/pull/5382) fixes `JsonlSessionStore.save()` crashes on transient `[WinError 5]` PermissionError in heartbeat cron.

5. **Low — Test determinism**:
   - [#5348](https://github.com/HKUDS/nanobot/issues/5348)/[#5349](https://github.com/HKUDS/nanobot/pull/5349): settings API tests fail in a 5-hour UTC window due to missing `timezone_name`.

## 6. Feature Requests & Roadmap Signals
Strong signals from today’s issues and PRs:

- **MCP budget management** ([#5298](https://github.com/HKUDS/nanobot/issues/5298), PR [#5388](https://github.com/HKUDS/nanobot/pull/5388)) is likely to land in the next minor release — a highly requested control for token-heavy MCP deployments.
- **MCP Apps metadata passthrough** (PR [#5386](https://github.com/HKUDS/nanobot/pull/5386)) and **Telegram sticker replies** (PR [#5387](https://github.com/HKUDS/nanobot/pull/5387)) were both implemented today and are likely candidates for the next release.
- **Matrix SAS cross-signing** (PR [#5385](https://github.com/HKUDS/nanobot/pull/5385)) resolves a long-standing trust warning; expected soon.
- **Session collaboration via mentions** (PR [#5358](https://github.com/HKUDS/nanobot/pull/5358)) may indicate a move toward multi-user/multi-session workflows in the WebUI; watch for continued iteration.
- **QwenCloud as a separate provider path** ([#5350](https://github.com/HKUDS/nanobot/issues/5350)) reflects demand from international users; a backward-compatible addition is plausible.
- **WebUI i18n for agent activity text** ([#5366](https://github.com/HKUDS/nanobot/issues/5366)) is a small, low-risk enhancement likely to be picked up.

## 7. User Feedback Summary
- **Pain points:** Data-loss bugs in session archival ([#5378](https://github.com/HKUDS/nanobot/issues/5378), [#5377](https://github.com/HKUDS/nanobot/issues/5377)); cron jobs silently dying ([#5373](https://github.com/HKUDS/nanobot/issues/5373)); Windows transient crashes ([#5382](https://github.com/HKUDS/nanobot/pull/5382)); un-trusted Matrix devices breaking E2EE workflow trust ([#4841](https://github.com/HKUDS/nanobot/issues/4841)).
- **Use cases driving change:** local WebUI users with large file workspaces (folder picker [#5381](https://github.com/HKUDS/nanobot/pull/5381)); operators running many MCP tools (schema budget); channel-first users (Telegram stickers).
- **Satisfaction indicators:** Fast turnaround is a positive signal — critical session bugs reported today already have open or closed fix PRs. Community proposals (ViBo memory integration, [#5372](https://github.com/HKUDS/nanobot/issues/5372)) reflect an engaged external ecosystem, though this is primarily promotional.

## 8. Backlog Watch
Items that have received activity today but remain open and may need maintainer attention:

- **[#4841 Matrix untrusted-device (cross-signing/SAS)](https://github.com/HKUDS/nanobot/issues/4841)** — open **38 days**, no maintainer response despite a complex root-cause analysis; a fix PR (#5385) is now open, but the issue itself lacks maintainer triage.
- **[#5251 MCP Apps host support in WebUI](https://github.com/HKUDS/nanobot/issues/5251)** — open **9 days**, with users asking how to route app metadata; PR #5386 only preserves metadata, not full UI hosting. Likely needs broader design discussion.
- **[#4549 heartbeat model_override](https://github.com/HKUDS/nanobot/pull/4549)** and **[#4551 heartbeat isolated_session](https://github.com/HKUDS/nanobot/pull/4551)** — open **49 days**; both were updated today due to conflicts. These are long-pending feature PRs needing conflict resolution and merge decisions.
- **[#5372 ViBo memory integration proposal](https://github.com/HKUDS/nanobot/issues/5372)** — promotional, but could be a signal for multi-session memory demand; no maintainer response yet.

---
*Digest generated from GitHub API data for the 24h window ending 2026-08-14. All links are permanent and resolve to the public repository.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-14

## 1. Today's Overview

Hermes Agent is in a highly active development and maintenance cycle, with 50 issues and 50 PRs updated in the last 24 hours. The project released patch version v0.20.1 (v2026.8.13), which rolls up ~656 merged PRs since v0.20.0 into a stable tag for downstream consumers. Activity is heavily concentrated on bug fixes and stability hardening, with a notable cluster of security-focused PRs addressing skill governance, profile exports, credential leaks, and execution-trust boundaries. The community is actively contributing, with many PRs opened by external developers, and the maintainers appear to be working through a backlog of P1/P2 issues affecting core workflows like TUI sessions, webhooks, and cron jobs.

## 2. Releases

**v2026.8.13 — Hermes Agent v0.20.1** ([Release Link](https://github.com/NousResearch/hermes-agent/releases/tag/v2026.8.13))

- **Type:** Patch release
- **Content:** Rolls up ~656 PRs merged since v0.20.0 into a stable tagged release
- **Target audience:** Docker images, hosted deployments, and anyone installing from the latest tag
- **Breaking changes:** None indicated (patch release)
- **Migration notes:** None provided; stable tag recommended for downstream consumers

## 3. Project Progress

**Merged/Closed PRs (4 total):**

- **#85710** [CLOSED] — `fix(cron): reuse secret cache and clarify home delivery` — Reuses process-cached external secret-source snapshots for cron runs, continues reloading local `.env`, suppresses misleading "delivery target lost thread" warnings. **Key improvement:** reduces unnecessary secret-source refresh churn on every cron fire.

- **#85707** [CLOSED] — `fix(cache): establish typed tool-schema boundary before planned_tools[-1]` — Normalizes list elements to the tool-schema type before applying cache_control marker decoration, preventing type-related errors in the native tool-cache path in `agent/prompt_caching.py`.

- **#81639** [CLOSED] — `[Bug]: _canonicalize_api_tool_calls mutates stored history on repair path` — This P0 bug fix addresses a serious session-state corruption issue where unrepairable tool calls were substituted with `{}` and written through to persisted history, permanently leaving sessions stuck in reasoning-only responses.

- **#85705** [CLOSED] — `Opened in wrong repository` — Invalid issue, closed without action.

**Notable open PRs advancing features/fixes (with strong velocity):**

- **#85727** — `fix(gateway): skip home prompt for unsupported plugins` — Improves plugin compatibility by not advertising /sethome to platforms without cron delivery support.
- **#85728** — `fix(honcho): surface backend failures from search_context/get_peer_card/get_session_context` — Surfaces genuine backend errors instead of silently returning empty strings.
- **#85725** — `feat(skills): autocomplete plugin skill commands` — New feature enabling qualified interactive slash commands for plugin skills with TUI/CLI autocomplete.
- **#85723** — `docs(website): add Japanese locale` — Adds `ja-JP` Docusaurus locale with English fallback.
- **#85722** — `fix(tools): route browser snapshot storage through symlink-safe writer` — Security hardening for cache writes.
- **#85724** — `fix(streaming): treat OpenCode Go cost-only terminal chunk as finish_reason stop` — Prevents false truncation detection for OpenCode Go streams.
- **#85726** — `fix(kanban): fire on_kanban_task_updated from edit_completed_task_result` — Wires task-mutation observer into all user-facing task-field editors.
- **#85721** — `fix(state): fall back to billing_provider in session_gateway_runtime` — Improves CLI resume reliability by checking billing provider as fallback.

## 4. Community Hot Topics

**Most active Issues (by comment count):**

1. **#66616** (25 comments) — `[skills-index-watchdog] Skills index is stale or degraded` — Automated freshness probe degraded; Skills Hub index 29.8h old (limit 26h). This signals a CI/CD reliability issue affecting documentation/skills discoverability.

2. **#84834** (16 comments) — `Webhook Revolution — graph-gated repair campaign (meta-issue)` — EPIC for a 5×2×3 repair campaign covering the entire Hermes webhook surface: ingress, execution, delivery, config, management UI, deployment, docs. This represents a major cross-cutting initiative the community is rallying around.

3. **#69592** (12 comments) — `[Bug]: /sessions and /models overlays invisible with ambient widget dock` — P1 TUI issue breaking core workflows (session resume, model switching) for users with ambient widgets (quota gauges). Day 13 since broken; affects documented TUI dock pattern.

4. **#83390** (9 comments, 2 👍) — `Auxiliary title_generation fails on DeepSeek: HTTP 400` — Provider-specific incompatibility with response_format; impacts auto title generation when routed to DeepSeek.

5. **#4438** (8 comments) — `[Feature]: Rich Spreadsheet Skill (xlsx/csv)` — Community request for structured spreadsheet handling abstraction instead of raw Python library improvisation.

**Analysis:** The webhook repair campaign (#84834) is the dominant community-driven initiative, indicating broad dissatisfaction with webhook robustness. The skills index staleness (#66616) and TUI overlay bug (#69592) are persistent quality issues affecting core UX.

## 5. Bugs & Stability

**Highest severity (P0/P1):**

- **#81639** [P0, CLOSED] — `_canonicalize_api_tool_calls mutates stored history` — Sessions permanently stuck; **fix was merged today** (see project progress).
- **#69592** [P1, OPEN] — TUI overlays invisible with ambient widget dock — Critical UX break affecting session resume and model switching; **no fix PR identified today**.
- **#62142** [P1, OPEN] — `fix(tui): verification-stop can discard streamed final answers and cron reports` — Agent streams substantive answer, then loses it from durable transcript; **no fix PR observed**.

**P2 bugs reported today (Aug 13-14):**

- **#85614** — Slack peer bot IDs ignored by final bot authorization — Security boundary issue; **no fix PR yet**.
- **#85693** — `computer_use` tool not exposed in Desktop sessions — **no fix PR yet**.
- **#85706** — OpenAI-wire cache writes lost at accounting boundary — **no fix PR yet**.
- **#85658** — Interrupted command adopts another session's working directory — **no fix PR yet**.
- **#85622** — External memory provider suppresses built-in MEMORY.md/USER.md injection — contradicts documented contract; **no fix PR yet**.
- **#85406** — Windows host + Docker: `vision_analyze` fails with POSIX/backslash path mangling — **no fix PR yet**.
- **#83851** — Chinese Windows: GBK encoding kills gateway — **no fix PR yet**.
- **#85104** — Desktop duplicate assistant message rendering (frontend-only) — **no fix PR yet**.
- **#85215** — Cron jobs pin to dead model, ignore fallback_providers — **no fix PR yet**.

**Security-related PRs active (P3):**

- **#81939** — Fail-closed protected skill governance (AP-003)
- **#35601** — Prevent credential leaks and SQLite data loss in profile exports
- **#83787** — Block execution-trusting writes from messaging platforms
- **#85722** — Symlink-safe browser snapshot writer

## 6. Feature Requests & Roadmap Signals

**Strong signals (community-backed, likely candidates for next minor release):**

1. **Webhook Revolution (#84834)** — Massive EPIC; expect incremental PRs landing over coming weeks.
2. **Rich Spreadsheet Skill (#4438)** — Structured xlsx/csv abstraction; moderate interest, long-standing (since April).
3. **Credential pool TTL configurability (#33049)** — Small, well-scoped config enhancement; high value for multi-provider users.
4. **Plugin skill autocomplete (#85725)** — In-progress PR; likely to land soon.
5. **Memory provider proposal (#85418)** — Local-first, zero-dependency memory benchmarked against Honcho; needs-decision label suggests maintainer review pending.
6. **Telegram drop_pending_updates opt-out (#84317)** — Config flexibility for cold-boot behavior; small, clean feature.
7. **Signal adapter completeness (#39043)** — Quote/reply, edit, remote-delete, read receipts; has 3 👍, building community support.
8. **Expose session async delegations over HTTP (#81806)** — API server feature for /v1/runs orchestrators; active PR.

**Prediction:** The webhook repair campaign and plugin skill autocomplete are most likely to ship in the next version. The spreadsheet skill and credential pool TTL are strong candidates for a v0.21 minor release.

## 7. User Feedback Summary

**Pain points (recurring themes):**

- **Session state fragility:** Users report lost streamed answers, adopted working directories, invisible overlays, and corrupted session history — eroding trust in core conversation persistence.
- **Cross-platform gaps:** Windows-specific bugs (GBK encoding crash, path mangling in vision_analyze, sync_back file loss) indicate a lag in Windows hardening.
- **Provider compatibility friction:** DeepSeek title generation failure, missing OpenAI-wire cache writes, and provider-specific streaming quirks (OpenCode Go) show ongoing integration complexity.
- **Silent failures:** External memory provider suppressing built-in memory, cron jobs failing silently for days on dead models, and backend errors collapsing to empty strings are frustrating users who can't tell if something went wrong.
- **Desktop app inconsistencies:** Duplicate message rendering, stale app bundles after update, caret loss during streaming, and missing tools (computer_use) suggest the Desktop client is still maturing.

**Positive signals:**

- Credit for the Chrome DevTools fix (#52954) acknowledged by 2ndNatureAI in their memory provider proposal (#85418).
- Active external contributors (vinsew, pierrenode, JoaoMarcos44, etc.) repeatedly submitting quality PRs — a sign of a healthy contributor ecosystem.
- The large volume of P2/P3 community-submitted bugs indicates users are actively testing and reporting.

## 8. Backlog Watch

**Long-unanswered items needing maintainer attention:**

- **#69592** [P1, since 2026-07-22] — TUI overlay bug, 12 comments, **day 14+**, critical core workflow broken; needs prioritization or explicit triage.
- **#4438** [P3, since 2026-04-01] — Spreadsheet skill request; 4+ months old, no maintainer response visible.
- **#35838** [P2, CLOSED as duplicate] — Provider info blocking when models.dev unreachable; closed but root fix unclear.
- **#62142** [P1, since 2026-07-10] — Streaming final answer loss; categorized with `fix(tui)` label, but no fix PR visible in this window.
- **#33049** [P3, since 2026-05-27] — Credential pool TTL configurability; 1 👍, 3 comments, no maintainer response.
- **#39043** [P3, since 2026-06-04] — Signal adapter completeness; 3 👍, no maintainer response.
- **#52339** [P2, since 2026-06-25] — Desktop stale app bundle after terminal update; 6 comments, no fix PR observed.
- **#65085** [P2, since 2026-07-15] — Telegram group observe attribution breaks admin gating; 3 comments, no fix PR observed.
- **#64866** [P2, since 2026-07-15] — WeCom websocket backoff fix PR by vinsew; open for a month, may need review.

**Risk watch:** The P1 items (#69592, #62142) affect core session workflows. If left unresolved, they may erode user confidence in the TUI/Desktop experience, especially as the project gains broader adoption. The webhook EPIC (#84834) appears to be a strategic response to an accumulating quagmire of webhook-related reliability issues — its outcome deserves close monitoring.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-14

## 1. Today's Overview

PicoClaw is in a **moderate-to-high activity phase** today, with 3 issues and 9 pull requests updated in the last 24 hours. The project shows a healthy dependency-maintenance cadence with 8 Dependabot-driven PRs, though it's notable that **none of the open feature requests have been acknowledged by maintainers yet**. The issue tracker reflects a stable core user base actively requesting Web UI performance improvements, broader ASR model support, and more flexible subagent tooling. No new releases were published, and no issues or PRs were closed by maintainers today—all 3 closed PRs were previously stale Dependabot updates superseded by newer versions. Overall, the project is progressing steadily but could benefit from more explicit maintainer engagement with community feature requests.

## 2. Releases

No new releases were published in the last 24 hours. The last known version remains **PicoClaw 0.3.1**.

## 3. Project Progress

All three merged/closed PRs today were **Dependabot dependency updates** that were closed as stale (superseded by newer versions) rather than merged:

- **[#3304 (CLOSED)](https://github.com/sipeed/picoclaw/pull/3304)** — `anthropic-sdk-go` 1.55.1 → 1.61.0 (closed as stale, superseded by #3334 targeting 1.62.0)
- **[#3305 (CLOSED)](https://github.com/sipeed/picoclaw/pull/3305)** — AWS `bedrockruntime` 1.53.3 → 1.56.2 (closed as stale, superseded by #3336 targeting 1.57.1)
- **[#3306 (CLOSED)](https://github.com/sipeed/picoclaw/pull/3306)** — AWS `config` 1.32.25 → 1.32.33 (closed as stale, superseded by #3335 targeting 1.32.35)

**No feature work or bug fixes were merged today.** All six open PRs are also Dependabot updates (AWS SDK, Anthropic SDK, and Matrix `mautrix` library), indicating the maintainer team is prioritizing dependency hygiene via bots rather than manual merges.

## 4. Community Hot Topics

The most active discussion this week centers on a single issue:

**[#3281 — Web UI chat input is very laggy with long history](https://github.com/sipeed/picoclaw/issues/3281)** (5 comments, 1 👍)
- Reported by `xpader` on 2026-07-21, still open and actively updated (2026-08-13)
- Users report severe input lag in the Web UI when session history grows beyond a modest length
- **One upvote suggests this may be underreported** — users might be tolerating the issue or using alternative clients (CLI, Matrix)
- The 5 comments indicate meaningful community discussion around scope and potential causes

This is the only issue attracting real community engagement, suggesting the Web UI performance is a **primary pain point** for active PicoClaw users right now.

## 5. Bugs & Stability

**One active bug** is currently tracked:

**[#3281 — Web UI input lag with long history](https://github.com/sipeed/picoclaw/issues/3281)** — **Severity: Medium-High**
- Reproducible: input box becomes noticeably laggy as session history accumulates
- Impact: Degrades the primary interactive experience for Web UI users
- **No fix PR exists** — maintainers have not publicly responded or linked a fix attempt
- Given the issue's age (3+ weeks) and continued activity, this appears to be a **persistent, acknowledged-but-unaddressed** performance problem

No crashes, regressions, or other stability issues were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals

Two new feature requests were filed today — both technically grounded and likely to be **serious roadmap candidates**:

**[#3331 — Support any `/audio/transcriptions`-compatible model](https://github.com/sipeed/picoclaw/issues/3331)** by `stanislavvv`
- Current implementation hard-codes only `*-whisper-*` model patterns in `asr.go`, excluding newer/faster transcription models
- Proposes a `whisper-transcription: true` config flag to force the whisper code path regardless of model name
- **Solves a real compatibility gap** — likely to resonate as OpenAI-compatible ASR models proliferate
- **Prediction:** Moderate-to-high chance of landing in next minor release if maintainers prioritize model flexibility

**[#3330 — Dynamic model override in delegate/spawn/subagent tools](https://github.com/sipeed/picoclaw/issues/3330)** by `v2up-32mb`
- Currently, `delegate` uses the target agent's model, `spawn` uses `defaultModel` — no runtime override
- Requests call-time model specification, enabling cost/quality routing per invocation
- **Power-user feature** for multi-model workflows (e.g., cheap model for summarization, premium for generation)
- **Prediction:** Lower priority than #3331, but a natural extension for advanced orchestration; could appear in a 0.4.x release

**No release roadmap is publicly visible**, making exact version prediction difficult.

## 7. User Feedback Summary

**Pain Points:**
- **Web UI latency** (#3281): Users explicitly describe the input lag as "very laggy," indicating a notable degradation in the core Web experience. The issue being open for 3+ weeks without a fix may suggest growing user frustration.
- **ASR model lock-in** (#3331): The complaint that `*-whisper-*` matching is "too old and slow" reflects user demand for modern, faster transcription models — likely tied to real-world latency/cost concerns.

**Use Cases:**
- **Multi-model orchestration** (#3330): Users want fine-grained control over which models power subagent operations, suggesting advanced, possibly production-oriented usage patterns.
- **Web-centric interaction**: The presence of Web UI–specific bugs suggests a significant portion of the community uses PicoClaw via browser rather than CLI-only.

**Satisfaction Signals:**
- Community is actively filing detailed, well-structured feature requests — a sign of engaged users who see long-term value in the project
- Lack of maintainer replies on new issues (0 comments on both #3330 and #3331) may be a **communication gap** worth monitoring

## 8. Backlog Watch

Items needing maintainer attention:

**[#3281 — Web UI input lag](https://github.com/sipeed/picoclaw/issues/3281)** — **CRITICAL WATCH**
- Open since 2026-07-21 (24 days), 5 comments, 1 👍
- **No maintainer response, no linked PR** — longest-standing open bug with no visible progress
- The silence here is the project's biggest health concern this week

**[#3318 — Broken `pnpm-lock.yaml` fix (PR)](https://github.com/sipeed/picoclaw/pull/3318)** — **MODERATE WATCH**
- Open since 2026-08-05 (9 days), tagged `stale`
- Fixes a real blocker for Web frontend builds (duplicate YAML mapping key preventing `pnpm install`)
- **Maintainers should review/merge this**, as it unblocks frontend development and CI pipelines

**Pattern to watch:** All three stale PRs closed today were superseded by newer Dependabot versions — this is healthy automation, but it means maintainers are benefiting from bot-driven updates rather than actively reviewing dependency changes. Long-term, this could leave subtle breaking changes undetected if Dependabot merges fail to receive human review.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-14

## 1. Today's Overview

NanoClaw saw a **wave of core-team engineering around release v2.2.0**, with 19 PRs updated in the past 24 hours—13 merged/closed and 6 still open. The central theme is the **hardening and finalization of the agent image promotion pipeline** (verify → approve → auto-merge), driven by the `[core-team]` group, alongside the landing of a long-awaited template-to-Plugins migration. A steady stream of community-contributed fixes—Telegram pairing CSPRNG, unknown-slash-command handling, and DB migrations—also merged. With the v2.2.0 release cut, the focus is now on security-gated CI, plugin MCP working-directory support, and a live open issue about unbounded approval cards from bot senders. Overall, this is a **high-velocity, release-stabilization day** with a clear emphasis on supply-chain security and process automation.

## 2. Releases

**v2.2.0** was cut (PR #3237).

- **Headline change:** `ncl groups create --template <ref>` now performs an **in-place plugin update** if the group already carries a template's plugin, instead of spawning a duplicate agent.
- **Dry-run mode:** The command prints a plan of every plugin-owned surface (plugin files, skills, MCP servers, etc.) before making changes.
- **No breaking changes or migration notes** were included in the release summary; this appears to be an additive release centered on the template/plugin experience.

## 3. Project Progress

**Merged/closed PRs (13 total) — notable items:**

- **[#3241 — ci: let a verified signature be the approving review (closed)**](https://github.com/nanocoai/nanoclaw/pull/3241): Publisher signature now gate the final human-approval step on pin bumps. **Off by default** (`AGENT_IMAGE_AUTO_APPROVE=true` activates it; otherwise it reports a plan and stops).
- **[#3240 — ci: open the agent-image bump PR from a dispatch (closed)**](https://github.com/nanocoai/nanoclaw/pull/3240): An AWS worker promotes a verified image and fires a `repository_dispatch` that opens the `versions.json` PR. The split isolates ECR/promotion credentials from the publisher identity.
- **[#3238 — ci: let verify-agent-image run on every PR so it can gate (closed)**](https://github.com/nanocoai/nanoclaw/pull/3238): Removed the `paths: [versions.json]` filter that made the verify job advisory forever—now it runs on every PR and can be required.
- **[#3158 — verify-agent-image: pin the publisher identity, and check attestations per arch (closed)**](https://github.com/nanocoai/nanoclaw/pull/3158): Fixes a fatal flaw: the gate read two variables (`AGENT_IMAGE_SIGNER_IDENTITY`/`_ISSUER`) that never existed, so signature verification was skipped every run.
- **[#3236 — versions: repin the agent image to hardened-2026-08-13 (closed)**](https://github.com/nanocoai/nanoclaw/pull/3236): Size delta is tiny (+44KB) but the image now carries NanoClaw's **own content**, not just an upstream base refresh.
- **[#3220 — feat!: agent templates become Agent Plugins 1.0.0 directories (merged)**](https://github.com/nanocoai/nanoclaw/pull/3220): The engine-level format migration. Includes stamp-time symlink/caps/secret hardening.
- **[#2909 — feat(setup): template setup flow in the wizard and first-agent stamping (merged)**](https://github.com/nanocoai/nanoclaw/pull/2909): The second half of the template work—wizard flow and first-agent stamping (stacked on #3220).
- **[#3231 — feat(codex,opencode): honor plugin MCP cwd in both provider config writers (merged)**](https://github.com/nanocoai/nanoclaw/pull/3231): Registry-payload half of plugin MCP working-directory support; Codex TOML writer puts cwd above the `[.env]` header.
- **[#3229 — fix(telegram): generate pairing codes with a CSPRNG, not Math.random() (merged)**](https://github.com/nanocoai/nanoclaw/pull/3229): Security fix—switched to `crypto.randomInt` and widened the code space.

**Community fixes merged:** [#3145 (DB backfill migration for destinations)](https://github.com/nanocoai/nanoclaw/pull/3145), [#2624 (per-server disabledTools in McpServerConfig)](https://github.com/nanocoai/nanoclaw/pull/2624), [#3230 (docs fix: stale mirror references)](https://github.com/nanocoai/nanoclaw/pull/3230). **Note:** The "merged" status is inferred from the closed label; not explicitly confirmed for every item.

## 4. Community Hot Topics

- **[#3235 — Unknown-sender approval: webhook/bot senders generate unbounded approval cards (OPEN, 0 comments)**](https://github.com/nanocoai/nanoclaw/issues/3235): The only new open issue today. The author describes **infinite approval-card spam** when a webhook hits a group with `unknown_sender_policy = 'request_approval'`—denial doesn't persist and the card can't be sensibly approved. This is a design gap: the approval flow can't distinguish a human from a bot sender.
- **[#3234 — Template-stamped agent groups get a bare UUID (CLOSED, 1 comment)**](https://github.com/nanocoai/nanoclaw/issues/3234): Fixed quickly. The `--template` path emitted a bare `randomUUID()` instead of `ag-<uuid>`, which the OneCLI `ensureAgent` rejects. Community's feedback loop with the core team is tight here.
- **[#3242 / #3239 — DO NOT MERGE live-fire tests (both open/closed drafts)**](https://github.com/nanocoai/nanoclaw/pull/3242): Sham PRs used to exercise the full signature-approval chain end-to-end. Not a signal of instability—just process engineering.

The underlying need is **operations maturity**: users want predictable handling of automated senders and are probing the trust boundaries of the new approval/auto-merge machinery.

## 5. Bugs & Stability

Ranked by severity:

1. **[High] [#3235 — Unbounded approval cards for webhook/bot senders (OPEN)**](https://github.com/nanocoai/nanoclaw/issues/3235): An active reliability issue. No fix PR yet. The approval UI itself can be spammed, and denials are non-persistent.
2. **[Medium] [#3234 — Bare UUID for template-stamped groups (CLOSED)**](https://github.com/nanocoai/nanoclaw/issues/3234): Functional bug with an external compatibility break. **Fixed** (closed within a day).
3. **[Low] [#3229 — Telegram pairing codes via Math.random() (merged)**](https://github.com/nanocoai/nanoclaw/pull/3229): Predictable RNG for pairing codes is a security concern. **Fixed** in v2.2.0 with CSPRNG (`crypto.randomInt`).
4. **[Low] [#3230 — Docs pointing at retired data/env mirror (merged)**](https://github.com/nanocoai/nanoclaw/pull/3230): README rot. Fixed.

No regressions reported today.

## 6. Feature Requests & Roadmap Signals

- **Plugin MCP working-directory support** ([#3231](https://github.com/nanocoai/nanoclaw/pull/3231), #3220): landed on trunk for Codex and OpenCode config writers. Expect the same for more provider configs.
- **Stdin JSON mode** ([#3218 — OPEN: `feat(cli): accept bounded JSON from stdin`](https://github.com/nanocoai/nanoclaw/pull/3218)): A generic, bounded way to pass structured arguments to `ncl`—likely stays a candidate for an upcoming minor release.
- **Hindsight memory integration** ([#2420 — OPEN: `/add-hindsight` skill with bundled MCP wrapper](https://github.com/nanocoai/nanoclaw/pull/2420)): Quietly waiting for a review since May. The bundled MCP wrapper suggests the team is serious about long-term memory.

## 7. User Feedback Summary

- **Pain point:** Approval fatigue. The two most-discussed items today (#3234, #3235) are both about the approval/template layer confusing operators and the system's inability to distinguish humans from bots.
- **Positive signal:** The contributor experience is good—fixes like #3234 and #3229 were closed within a day of creation. The `verify-agent-image` chain got real fixes (identity pinning, path filtering removal) that make the gate actually enforceable.
- **Inferred satisfaction:** The "DO NOT MERGE" smoke tests (#3239, #3242) and the rapid closure of #3238 suggest the team trusts the new CI enough to run live-fire exercises—a sign of healthy process confidence.

## 8. Backlog Watch

- **[#2420 — /add-hindsight: MCP wrapper for Hindsight memory (OPEN since 2026-05-11, no maintainer comments)**](https://github.com/nanocoai/nanoclaw/pull/2420): Three months old, feature-complete-looking, no feedback. May need a maintainer triage.
- **[#2346 — fix(formatter): treat unknown slash commands as normal chat (OPEN since 2026-05-08)**](https://github.com/nanocoai/nanoclaw/pull/2346): A sensible behavior fix for silently-dropped messages. Stale without maintainer input.
- **[#3218 — stdin JSON mode (OPEN since 2026-08-09, no comments)**](https://github.com/nanocoai/nanoclaw/pull/3218): Fresh, but silent. After the v2.2.0 release, this is a good candidate for the next cycle.


</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-14

## 1. Today's Overview

IronClaw is in an intense period of architectural re-cutting and performance optimization. The project's activity is exceptionally high, with 50 issues and 50 PRs updated in the last 24 hours, driven by a major push on the "Pluggable agent loops" epic (#7482) as well as a coordinated campaign to reduce write amplification in the Postgres-backed filesystem substrate. This work is bookended by the stable release of **ironclaw v1.2.0** yesterday, which promoted an RC candidate after validation. The project is also in the middle of a recent surge of community bug reports (~8 new issues filed in the last 24 hours), and maintainers are regularly triaging and closing them. The team appears to be executing a well-structured phase-0 roll-out of the new harness/executor architecture, marked by several closed implementation issues. The overall signal is that of a project in heavy, coordinated engineering motion: stable release out, core architectural rework underway, and performance work targeting the database hot path.

## 2. Releases

- **ironclaw-v1.2.0** — Promoted to stable from `1.2.0-rc.3` via PR #7625 on 2026-08-13. This release consolidates fixes validated across RC2 and RC3. Notably, it includes a fix where the runtime container image now installs `curl`, allowing in-container HTTP healthchecks to execute. The changelog consolidates all RC1–RC3 entries under the stable heading. No breaking changes or migration notes were mentioned in the release summary.

## 3. Project Progress

Looking at closed/merged PRs, the project had a productive day focused on stabilization, performance, and tooling.

- **Release Promotion** — PR #7625 (merged) formally promoted `1.2.0-rc.3` to stable `1.2.0`.
- **Live Canary Fixes** — Two merged PRs from BenKurrek target the "Live Canary" CI pipeline: PR #7579 (merged) fixes slack connect failures in QA lanes, and PR #7590 (merged) aligns the bundled-skill marker owner with the runtime mint, fixing verification narration. Both were validated by the first runs after merging.
- **Document Tooling** — PR #7376 (merged) extended the reference gate in CI to scan the `docs/` surface, covering Mintlify pages, the Chinese locale mirror, and the internal contract corpus. This is part of a "doc-truth" initiative to pin documentation claims to actual behavior.
- **Loop Heuristics** — PR #7531 (merged) changed repeated-call detection in the loop to be advisory-only, replacing a sliding-window heuristic with a simpler three-consecutive-call check to avoid false positives.
- **Extensions** — PR #7581 (merged) fixes extension state refresh after OAuth discovery, rehydrating tools on restart while preserving policy across upgrades.
- **Performance Suite** — Several performance PRs were opened (not merged) by serrrfirat: #7631 (coalescing event sink), #7629 (reduce trigger writes), #7630 (measurement tooling for Postgres writes), and #7628 (remove heartbeat journal churn).

## 4. Community Hot Topics

The most commented issue by far is **#7482 ("Epic: Pluggable agent loops")**, opened by serrrfirat, which has 6 comments. This is the centerpiece epic that describes IronClaw becoming a **kernel** — offloading the agent loop and tool code to external harnesses (e.g., Claude Code) while keeping scheduling, capability controls, and egress boundaries in the kernel. The binding decisions made in this epic's comments are driving the entire current roadmap (**#7621, #7622, #7623**, and a series of closed WS-issues).

Second is **#6257** (PDF MIME-type generation bug), which is closed but still draws attention, and **#2117** ("ironclaw-bridge"), an older open enhancement requesting a file/MCP bridge daemon for cloud-hosted deployments.

The underlying need across these hot topics is a clear one: users and maintainers want IronClaw to support *any* agent loop (not just its own native one) while maintaining strict security boundaries, and to allow users to connect their own local workflows and files to cloud deployments.

## 5. Bugs & Stability

Several new bugs surfaced in the last 24 hours, and it was a mixed day for stability, highlighted by the stable release promotion.

- **Severity: High — Custom MCP auth-flow hang (#7626, OPEN)** — Filed yesterday by sergeiest. A user reported that IronClaw hangs when connecting to a custom MCP requiring browser/email verification. The harness appears to freeze while waiting for the OAuth callback. No fix PR exists yet; this is an active issue.
- **Severity: High — Invalid credential acceptance for GitHub extension (#7627, OPEN)** — A user entered "1" as credentials and the GitHub extension showed as "connected" even though it then fails authentication. This represents a confusing and potentially misleading UX bug. No fix PR yet.
- **Severity: High (Upstream) — NEAR AI Cloud Sonnet-5 500 errors (#7589, CLOSED)** — Reported by a user as a 3-day outage on the NEAR AI Cloud API (Sonnet-5). It references `nearai/cloud-api#920` as the root cause, and it was closed quickly by triage.
- **Severity: Medium — Memory not reliably recalled (#7185, OPEN)** — Open since Aug 4, still reporting that context from one conversation is not reliably available in later ones.
- **Severity: Low/Medium — PDF MIME-type error (#6257, CLOSED)** — Closed but was a core bug in the document generation pipeline.

## 6. Feature Requests & Roadmap Signals

The roadmap is very clearly driven by the **Pluggable agent loops** epic (#7482). The platform is explicitly moving toward a "kernel" model:

1. **Pluggable Agent Loops & Harnesses** — The release of issues **#7611–#7623** (HarnessDriver contract, executor, adapters for Claude Code/pi/codex, pinned images, workspace mounts) signals a major shift: IronClaw will soon support running external agent harnesses as first-class citizens, containerized and sandboxed.
2. **ACP (Agent Communication Protocol) Support** — Tied closely to the above, PR #7513 adds an `acp serve` command for `--stdio` transport, enabling external tools like GitHub Copilot CLI to connect.
3. **Local file/MCP bridge (ironclaw-bridge)** — Issue #2117 continues to seek implementation for laptop-to-cloud resource connectivity.

These signals suggest that the next release or two will likely introduce the phase-0 harness support (Claude Code, pi, codex), native ACP serve, and possibly the file/MCP bridge.

## 7. User Feedback Summary

User feedback across the issues fielded in the last day points to a few recurring themes:

- **Auth flows are a weak spot**: Two of the most recent bugs (#7626, #7627) involve authentication flows that either hang (custom MCP OAuth with email/browser verification) or misleadingly report a success state despite invalid credentials (GitHub extension).
- **Users want clear version visibility**: In #7580, a user in `#x-ai-product-feedback` asked how to view the IronClaw Reborn version from the web UI, suggesting that versioning is not visible in the interface—a UX discovery gap.
- **Memory/recall remains a pain point**: The "Memory not reliably recalled" issue (#7185) is still open, caused by multiple testers in the 2026-07-23 IronClaw Champions weekly check-in.
- **Cloud API reliability concerns**: The Sonnet-5 500 error report (#7589) indicates that external API failures directly impact the user experience, and were promptly escalated.

Overall, users seem engaged, actively testing, and filing bugs at a steady clip, but auth flows and memory/recall reliability are the two big friction points.

## 8. Backlog Watch

- **#2117 — "ironclaw-bridge" (OPEN, April 7)** — This remains the most sought-after feature on the backlog, with a small but concentrated call for local cloud file/MCP bridge capabilities. It has 2 comments and one heavy 👍.
- **#7185 — Memory reliability (OPEN, Aug 4)** — This issue has been open for 10 days and is still awaiting either a diagnosis or a fix assignment. It is central to user trust.
- **PR #7184 — Nostr host functions for WASM tools (OPEN, Aug 4)** — This is an XL, low-risk PR from a new contributor. It is now 10 days old and hasn't received any visible review comments or merges. Given the maintainers' focus on the reborn epic and release stabilization, this may need some reviewer attention to provide timely feedback to the community.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-14

## 1. Today's Overview

LobsterAI development remains steady, driven almost entirely by UI refactoring and feature polish in the renderer layer. Today's activity shows a strong engineering focus on unifying visual paradigms across skills, MCP connectors, and kits, alongside consolidating cowork/management flows — a sign of deliberate product-design alignment. Six pull requests were merged/closed today, indicating a healthy throughput, while 5 remain open for review. Notably, no new releases were published, and there are zero issues opened in the last 24 hours, suggesting the project is in a build-and-stabilize phase (not an exploratory/discovery phase). The persistent backlog of stale test-coverage PRs remains a point of concern.

## 2. Releases

No new releases were published for LobsterAI on 2026-08-14. There are no release notes, breaking changes, or migration steps to report. — **No actionable items.**

## 3. Project Progress

Six pull requests were merged or closed today, all merged on 2026-08-13 and tracked on 08-14. They cluster around two themes: UI refactoring and targeted bug fixes.

**UI & Experience Consolidation (Merged: 4 PRs)**
- **#2488** — [refactor(cowork): rework cowork BTM (Background Task Management?) and management UI](https://github.com/netease-youdao/LobsterAI/pull/2488). Overhauls the cowork management interface alongside the broader UI refactor.
- **#2487** — [refactor(skills): merge skills and MCP views into a unified "skills-and-connectors" view](https://github.com/netease-youdao/LobsterAI/pull/2487). Simplifies navigation by merging two previously separate management areas into a single view.
- **#2486** — [refactor(mcp): unify MCP card/detail UI with kits and skills styling](https://github.com/netease-youdao/LobsterAI/pull/2486). Extracts shared `CardOverflowMenu` (renamed from `SkillCardMenu`) and `managementTypography` utilities. Introduces `McpCard` / `McpDetailModal` components.
- **#2485** — [feat(activity): support evergreen daily check-in](https://github.com/netease-youdao/LobsterAI/pull/2485). Converts the one-off check-in activity (from #2408) into an "evergreen" permanent feature, including auto-refresh and improved account menu integration.

**Bug Fixes (Merged: 1 PR, Closed: 1 PR)**
- **#1232 (Merged)** — [fix(scheduledTask): repair first-execution result not pushed to UI](https://github.com/netease-youdao/LobsterAI/pull/1232). Fixes a logic bug in `cronJobService.ts` where `pollOnce()` compared `previousRunAtMs > 0`; on first run this value was `0`, causing the UI to miss the first execution event entirely.
- **#2484 (Closed)** — `Feat/enterprise edition`. This PR was closed without a clear merge status; it may have been closed in favor of a different implementation or due to incompleteness (its description includes unfilled template boilerplate).

## 4. Community Hot Topics

The only updated issue today is **#1162** ([Open] — [为 openclawMemoryFile 和 openclawLocalTimeContextPrompt 补充 Vitest 单元测试](https://github.com/netease-youdao/LobsterAI/issues/1162)), which has 1 comment. This issue (and its companion PR #1165) targets two core modules that have zero test coverage — a legitimate and important concern for maintainability, given the memory file module is critical to OpenClaw's core function. The low engagement (0 reactions, 1 comment) suggests this is a technical-debt issue acknowledged by the team but lacking in community urgency. It's worth monitoring to upstream.

## 5. Bugs & Stability

The merged PR **#1232** ([scheduledTask first-execution result not pushed](https://github.com/netease-youdao/LobsterAI/pull/1232)) addresses a **Medium severity** bug: users missed the first run result of any scheduled task, requiring a second run to see output. This is a regression-risk fix that landed cleanly today.

Beyond that, two Open PRs highlight latent quality/stability risks:
- **#1166** (Open, stale) — [fix(agent): prevent duplicate custom agent names](https://github.com/netease-youdao/LobsterAI/pull/1166). A UX bug allowing duplicate custom agent names in the list is now ambiguous. **Low severity but annoyingly persistent** — the fix exists but has not been merged.
- **#1165** (Open, stale) — [75 Vitest tests for openclawMemoryFile and openclawLocalTimeContextPrompt](https://github.com/netease-youdao/LobsterAI/pull/1165). This PR adds critical tests around memory parsing and local time prompt generation — both previously untested. It's explicitly linked to Issue #1162.

While #1232 is good news, the stagnation of #1166 (merged in April) remains an unresolved stabilization issue.

## 6. Feature Requests & Roadmap Signals

Today's merged PRs hint at an upcoming product roadmap focused on:
- **Unified connector & skills management** (#2487, #2486) — The product is moving toward a single management view for "skills-and-connectors," which will likely become a core navigation model in the next UI release.
- **Enterprise edition** (#2484) — The presence of a (now closed) "Feat/enterprise edition" PR suggests this is a planned or ongoing track; today's close might reflect an internal pivot, not an abandonment. The "evergreen daily check-in" (#2485) aligns with an enterprise/engagement suite.
- **Evergreen activities** (#2485) — A signal that gamification/engagement activities are becoming permanent, not one-off campaigns.

Looking at **Open PRs** for forward-looking demand:
- **#2483** (Open) — [fix(openclaw): key skill entries by frontmatter name](https://github.com/netease-youdao/LobsterAI/pull/2483). Fixes a real bug where UI toggles were silently ineffective due to a name/directory mismatch in skills. Likely to be merged soon as it touches core OpenClaw skill management.

**Prediction for v-next:** The next release will likely ship the unified "skills-and-connectors" management view (layout/UX overhaul), the evergreen check-in, and a fix for OpenClaw skill entries (from #2483). The enterprise edition might be a long-running branch.

## 7. User Feedback Summary

Real user pain points visible from today's data:
- **Silent UI failures**: The duplicate-agent-name bug (#1166) — creating agents with existing names leads to ambiguous lists and manual clean-up. Users had to find the original entry manually.
- **First-run uncertainty**: The scheduled task first-run bug (#1232) meant users couldn't trust the first execution result, an unsettling experience for automation users.
- **Cron "Run Now" UX gap**: Open PR #1163 (open, stale) details that clicking "Run Now" on a scheduled task yields no feedback, implying users often double-click due to a lack of confirmation. This is a direct pain point for power users relying on manual trigger control.
- **Skill name vs. path mismatch**: #2483 indicates that users toggling skills in the UI were seeing their changes ignored silently — a high-frustration bug for users configuring OpenClaw skills.

Overall, the community is mature and technical, reporting nuanced bugs (timing, name/path mapping). The response tempo from maintainers (fixing #1232 today) is reassuring.

## 8. Backlog Watch

Several stale and important PRs/Issues have been awaiting maintainer attention for over 4 months (all created around 2026-03-31). These are blocking test coverage and quality improvements:

- **#1165** (Open, stale since March 31) — [PR: 75 Vitest tests for memory & local time prompt](https://github.com/netease-youdao/LobsterAI/pull/1165) — Critical for destabilizing core memory modules; still no merge.
- **#1162** (Open, stale) — [Issue requesting the above test coverage](https://github.com/netease-youdao/LobsterAI/issues/1162) — High-priority tech-debt issue, no closure in sight.
- **#1156** (Open, stale) — [PR: Add Vitest tests for commandSafety and coworkMemoryJudge](https://github.com/netease-youdao/LobsterAI/pull/1156) — These are security-sensitive modules (dangerous command detection, memory quality gate). The absence of tests is a latent risk; the PR addresses it but remains idle.
- **#1166** (Open, stale) — [PR: Prevent duplicate custom agent names](https://github.com/netease-youdao/LobsterAI/pull/1166) — Small, user-visible fix pending for 4+ months.
- **#1163** (Open, stale) — [PR: Improve "Run Now" feedback for scheduled tasks with optimistic updates and Gateway sync](https://github.com/netease-youdao/LobsterAI/pull/1163) — Substantial UX/progress; yet unmerged.

All five signals indicate a **stale-review problem** in the project: maintainers are merging quickly, but reviewing/rebasing older quality/security-focused PRs is lagging. This is the project's primary process risk. **Recommendation:** The maintainers should prioritize merging or explicitly closing #1156, #1163, #1165, and #1166 within the next release cycle.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest
**Date:** 2026-08-14

---

## 1. Today's Overview

Moltis is in a steady state of active maintenance and incremental feature development. The project saw **4 open Pull Requests** (all pending review/merge) and **1 open Issue** reported in the last 24 hours, with no new releases published. The activity indicates a focused effort on bug fixes related to tooling portability (macOS compatibility) and external dependency migrations, alongside a substantial feature PR for durable connectors. While no code was merged today, the PR pipeline is healthy and the team is actively addressing technical debt, particularly around third-party tool repo reorganizations and test reliability.

---

## 2. Releases

No new versions were published during this reporting window.

---

## 3. Project Progress

No PRs were merged or closed in the last 24 hours. However, one significant PR remains open and represents notable upcoming progress:

- **[PR #1190: Add durable CalDAV and channel history connectors](https://github.com/moltis-org/moltis/pull/1190)** — This large feature PR adds provider-neutral connector persistence, atomic snapshots, scheduling, projections, and bounded local full-text search. It also introduces read-only CalDAV datasets and reusable Slack, Discord, Matrix, and Microsoft Teams message-history datasets without requiring channel credential copying. This is the most substantial work in the pipeline and signals a major expansion of Moltis's data ingestion capabilities.

---

## 4. Community Hot Topics

The most active discussions revolve around **environment portability and dependency management**, driven by recent changes in the upstream `openclaw` project:

- **[Issue #1193: Flaky test: push fanout timeout assertion races under full-suite load](https://github.com/moltis-org/moltis/issues/1193)** — While only reported today, the flaky test indicates potential concurrency bugs in the gateway's push/fanout logic that could manifest in production under high load.
- **[PR #1194: fix(scripts): guard empty bash array expansions for macOS bash 3.2](https://github.com/moltis-org/moltis/pull/1194)** — Active fix to resolve a hard crash in the `local-validate-full` recipe on macOS, caused by unbound variable errors in bash 3.2 when no PR number is provided.
- **[PR #1191: fix(sandbox): point gogcli module path at the openclaw org](https://github.com/moltis-org/moltis/pull/1191)** and **[PR #1192: fix(skills): point wacrawl install metadata at the openclaw org](https://github.com/moltis-org/moltis/pull/1192)** — Both address broken `go install` falls for `gogcli` and `wacrawl` respectively, caused by the upstream repositories being renamed into the `openclaw` organization.

These PRs highlight an underlying need for developers using Moltis on macOS to have a smooth local development experience, and a broader need to track upstream third-party dependency moves to prevent broken builds.

---

## 5. Bugs & Stability

One bug was reported today, ranked by severity:

**Medium Severity — Flaky Test Under Load:**
- **[Issue #1193: Flaky test: push fanout timeout assertion races under full-suite load](https://github.com/moltis-org/moltis/issues/1193)** — The `fanout_is_bounded_and_times_out_a_hung_endpoint` test in `moltis-gateway` fails intermittently (2 of 3 full-suite runs) on a 10-core macOS machine. The failure occurs only when the full workspace suite runs, suggesting a race condition or timing issue in the push/fanout service that may be exacerbated by parallel test execution. **No fix PR exists yet.**

Additionally, two **build-breaking bugs** were fixed via open PRs (see Section 6):
- **Critical (Build):** `moltis sandbox build` fails on all pre-built images due to a broken `go install` for `gogcli` ([PR #1191](https://github.com/moltis-org/moltis/pull/1191)).
- **High (Tooling):** The `just local-validate-full` command crashes on macOS due to a bash array expansion error ([PR #1194](https://github.com/moltis-org/moltis/pull/1194)).

---

## 6. Feature Requests & Roadmap Signals

The open PR for durable connectors ([PR #1190](https://github.com/moltis-org/moltis/pull/1190)) is the clearest roadmap signal. Adding CalDAV support and channel history connectors for Slack, Discord, Matrix, and Teams represents a major step toward making Moltis a more complete data orchestration platform. Given the size and detail of this PR, it is a strong candidate for inclusion in the next minor or major version.

No direct user-submitted feature requests were raised in the last 24 hours beyond the code changes in the PR pipeline.

---

## 7. User Feedback Summary

While no direct user comments were captured in this window, the bug reports and PRs paint a clear picture of the user base's pain points:

- **macOS Developers Are Active:** The macOS-specific bash 3.2 crash ([Issue #1193](https://github.com/moltis-org/moltis/issues/1193), [PR #1194](https://github.com/moltis-org/moltis/pull/1194)) shows a strong contingent of macOS users running full validation suites locally. The flaky test on an "otherwise idle 10-core macOS machine" suggests that users with powerful hardware may still encounter frustrating CI-like failures locally.
- **Broken Developer Experience (DX):** The broken `gogcli` and `wacrawl` installs ([PR #1191](https://github.com/moltis-org/moltis/pull/1191), [PR #1192](https://github.com/moltis-org/moltis/pull/1192)) block core workflows like `sandbox build` and skill installation. Users expect dependency resolution to "just work" and could be frustrated by failures stemming from third-party repo renames.
- **High Interest in Historical Data:** The substantial feature work in [PR #1190](https://github.com/moltis-org/moltis/pull/1190) suggests strong internal or community demand for persistent, searchable channel history, a common need for compliance, auditing, or analytics use cases.

---

## 8. Backlog Watch

- **[PR #1190: Add durable CalDAV and channel history connectors](https://github.com/moltis-org/moltis/pull/1190)** — Opened on 2026-08-11, this large PR has been open for 3 days without updates. Given its size, it likely needs careful review. The lack of comments may indicate the maintainers are reviewing privately or it could be at risk of being overtaken by other changes. This is the single most important item needing maintainer attention for feature velocity.

- **[Issue #1193: Flaky test: push fanout timeout assertion races](https://github.com/moltis-org/moltis/issues/1193)** — Only open for a day, but flaky tests can quickly erode trust in the test suite and hide real regressions. A maintainer should triage this early to confirm the test isn't masking a genuine concurrency issue in the gateway's timeout logic.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-14

## 1. Today's Overview

CoPaw (QwenPaw) demonstrates strong momentum with **42 issues** and **50 PRs** updated in the last 24 hours, alongside the release of **v2.1.0** — a significant milestone introducing the QwenPaw OS Shell with windowed app management. Community engagement is high, particularly around Chinese-language bug reports and feature requests, indicating a substantial user base in the Chinese market. However, the project faces **serious security concerns** with multiple reports of unauthenticated API exposure and plugin permission gaps. The development team shows strong velocity, processing a mix of bug fixes, feature enhancements (memory dashboards, channel isolation for Matrix, media localization for OneBot), and architectural improvements across providers and session management.

## 2. Releases

### v2.1.0 (Latest)
**Highlights:**
- **QwenPaw OS Shell**: Open apps in movable, resizable windows with a launcher, taskbar, notifications, and saved layouts ([PR #6645](https://github.com/agentscope-ai/QwenPaw/pull/6645))
- Installed and marketplace apps now share one unified catalog across the App Center and OS Shell

**Notable changes:**
- This is the release branch; several fixes from earlier betas are included (see below)

### v2.1.0-beta.5
- **fix(chats)**: Handle dict-like model responses ([PR #6816](https://github.com/agentscope-ai/QwenPaw/pull/6816))
- **fix(memory)**: Simplify long-term memory guidance ([PR #6942](https://github.com/agentscope-ai/QwenPaw/pull/6942))
- **docs(website)**: Fix Files workspace documentation

**Migration Notes:** Users upgrading from 2.0.x should be aware of the new OS Shell architecture. The unified app catalog may require re-indexing installed apps.

---

## 3. Project Progress

**Merged/Closed PRs (19 total):**

| Area | PR | Description |
|------|-----|-------------|
| **Mission Mode** | [#6652](https://github.com/agentscope-ai/QwenPaw/pull/6652) | Enforce `max_iterations` server-side in MissionGate — fixes infinite sub-agent dispatch issue |
| **Chat History** | [#6636](https://github.com/agentscope-ai/QwenPaw/pull/6636) | Added pagination and GZip compression to chat history — fixes 30s timeouts on long chats |
| **Channel Dependencies** | [#6387](https://github.com/agentscope-ai/QwenPaw/pull/6387) | Install optional channel dependencies on demand instead of bundling |
| **Memory (Auto-Dream)** | [#6884](https://github.com/agentscope-ai/QwenPaw/pull/6884) | Make Auto-Dream integration resilient to malformed LLM output |
| **Release Notes** | [#6989](https://github.com/agentscope-ai/QwenPaw/pull/6989) | Updated release notes for v2.1.0 |

**Open PRs Advancing Key Features:**
- **Provider unification** ([#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)): Catalog-driven provider model system with capability-aware routing and fallback support
- **OneBot media localization** ([#6715](https://github.com/agentscope-ai/QwenPaw/pull/6715)): Localize inbound images/audio/video/files before agent processing
- **Matrix per-sender isolation** ([#7001](https://github.com/agentscope-ai/QwenPaw/pull/7001)): Fix session/memory sharing within group rooms
- **PawPort import flow** ([#6960](https://github.com/agentscope-ai/QwenPaw/pull/6960)): Import from Codex and Qoder (instructions, skills, plugins, etc.)
- **Session-scoped multi-project directories** ([#6976](https://github.com/agentscope-ai/QwenPaw/pull/6976))

---

## 4. Community Hot Topics

### 🔥 Most Active Discussions

1. **[#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921) — Agent stops without notice (6 comments)**
   - Multi-step tasks halt silently after planning (e.g., "Let me do all three.") with no visible output — requires user prompt "continue" to resume.
   - **Signal:** Core reliability issue affecting task autonomy; likely a model output parsing/streaming problem.

2. **[#6973](https://github.com/agentscope-ai/QwenPaw/issues/6973) — Alibaba Cloud Bailian token plan support (5 comments)**
   - Users want to use Alibaba Cloud's token-based pricing with QwenPaw Creator.
   - **Signal:** Demand for flexible billing options with Chinese cloud providers.

3. **[#6811](https://github.com/agentscope-ai/QwenPaw/issues/6811) — OpenAI Responses continuation summary bugs (5 comments)**
   - `disable_thinking` ignored during scroll-triggered summaries; 60s cancellation misreported as malformed output. **Closed.**
   - **Signal:** Background continuation summaries can block the main conversation — serious UX issue.

4. **[#6853](https://github.com/agentscope-ai/QwenPaw/issues/6853) — prompts.py contradicts actual memory behavior (5 comments)**
   - `prompts.py` claims dream process syncs to MEMORY.md, but this was never implemented. **Closed.**
   - **Signal:** Documentation/prompt accuracy issues causing user confusion about memory features.

5. **[#6992/#6993](https://github.com/agentscope-ai/QwenPaw/issues/6992) — Critical security: exposed port, unauthenticated APIs (3+ comments)**
   - Security report claiming 0.0.0.0:8088 exposure, unauthenticated plugin installation API with arbitrary command execution, SSH backdoor persistence. Duplicate issues filed. One closed as invalid.
   - **Signal:** Potential major security concern — needs maintainer verification immediately.

6. **[#6847](https://github.com/agentscope-ai/QwenPaw/issues/6847) — Antivirus kills QwenPaw (4 comments)**
   - Same task+model, QwenPaw gets killed by antivirus; WorkBuddy doesn't.
   - **Signal:** Possible false-positive detection patterns or suspicious execution behavior.

---

## 5. Bugs & Stability

### Severity: 🔴 Critical
| Issue | Description | Status |
|-------|-------------|--------|
| [#6992/#6993](https://github.com/agentscope-ai/QwenPaw/issues/6992) | **Security**: Port 8088 exposed on 0.0.0.0, unauthenticated plugin install API, arbitrary command execution, SSH backdoor persistence | One closed as invalid; needs maintainer review |
| [#6916](https://github.com/agentscope-ai/QwenPaw/issues/6916) | **Security**: Plugins can silently create cron jobs and inject user-visible messages without approval | Closed |
| [#6768](https://github.com/agentscope-ai/QwenPaw/issues/6768) | Agent enters infinite loop after multi-step task; session blocked for hours | Closed |

### Severity: 🟠 High
| Issue | Description | Status |
|-------|-------------|--------|
| [#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921) | Agent stops silently mid-task, requires "continue" prompt | Open |
| [#6951](https://github.com/agentscope-ai/QwenPaw/issues/6951) | After scroll compact, pre-compaction chat transcript invisible in UI; only internal eviction index shown | Open |
| [#6966](https://github.com/agentscope-ai/QwenPaw/issues/6966) | Telegram `/new` doesn't rotate session ID; context fills indefinitely | Open |
| [#7007](https://github.com/agentscope-ai/QwenPaw/issues/7007) | Windows Desktop TUI fails: packaged executable rejects `-m qwenpaw acp` → "transport: Connection closed" (v2.1.0) | Open |
| [#6955](https://github.com/agentscope-ai/QwenPaw/issues/6955) | Intermittent startup crash/exit on Windows (pip install, v2.0.1) | Open |
| [#7008](https://github.com/agentscope-ai/QwenPaw/issues/7008) | Anthropic model falsely flags "sensitive images" in long history (61+ messages), interrupting session | Open |

### Severity: 🟡 Medium
| Issue | Description | Status |
|-------|-------------|--------|
| [#7005](https://github.com/agentscope-ai/QwenPaw/issues/7005) | Enabling Shabox prevents UV writing to `~/.cache/uv` | Open |
| [#6883](https://github.com/agentscope-ai/QwenPaw/issues/6883) | Daily page groups notes in subfolders under wrong dates | Closed |
| [#6047](https://github.com/agentscope-ai/QwenPaw/issues/6047) | New chat reopens old session after upgrade; stale ordering and missing session index sync | Closed |

**Fix PRs in progress:**
- [#6998](https://github.com/agentscope-ai/QwenPaw/pull/6998): Prevent semaphore leaks from unconsumed LLM streams
- [#6975](https://github.com/agentscope-ai/QwenPaw/pull/6975): Reset context-usage ring after `/compact`

---

## 6. Feature Requests & Roadmap Signals

### High Signal (likelihood of landing in next release: High)

1. **Agent import from other tools (PawPort)** — [#6960](https://github.com/agentscope-ai/QwenPaw/pull/6960)
   - Import instructions, settings, skills, plugins, projects, and recent work from Codex and Qoder. First PR already open.
   - **Prediction:** Likely in v2.2.0 given active PR.

2. **Session-scoped multi-project directories** — [#6976](https://github.com/agentscope-ai/QwenPaw/pull/6976)
   - Bind chats to ordered list of project directories; first entry primary.
   - **Prediction:** In review; possible v2.1.x patch or v2.2.0.

3. **QWENPAW_CHANNEL env variable** — [#6995](https://github.com/agentscope-ai/QwenPaw/issues/6995)
   - Inject current channel into shell subprocess environment so scripts know the source channel.
   - **Prediction:** Small change; likely to land quickly.

4. **Embeddable chat without sidebar/header + API key in URL** — [#6970](https://github.com/agentscope-ai/QwenPaw/issues/6970)
   - Request for embeddable chat sub-page, session list filtering by date/sessionId.
   - **Prediction:** Possible but requires frontend/API work; medium-term.

### Medium Signal

5. **Server-side agent proxy client** — [#7002](https://github.com/agentscope-ai/QwenPaw/issues/7002)
   - Lightweight desktop proxy client for server-deployed QwenPaw with desktop control capabilities.
   - **Prediction:** Architectural change; not immediate.

6. **Alibaba Cloud Bailian token plan support** — [#6973](https://github.com/agentscope-ai/QwenPaw/issues/6973)
   - **Prediction:** Likely given China market share; billing integration work needed.

7. **Toggle to disable character-stream counter in chat** — [#6585](https://github.com/agentscope-ai/QwenPaw/issues/6585)
   - Closed; likely implemented or declined.

### Security-Driven Roadmap Items

8. **Plugin permission model overhaul** — [#6916](https://github.com/agentscope-ai/QwenPaw/issues/6916)
   - Silent cron creation and message injection without approval.
   - **Prediction:** Needs urgent attention; may drive permission UI redesign.

---

## 7. User Feedback Summary

### Pain Points
- **Silent task abandonment** ([#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921)): Agent plans next steps but stops without executing — users must manually say "continue." Highly disruptive for automation use cases.
- **Context compression breaks transcript visibility** ([#6951](https://github.com/agentscope-ai/QwenPaw/issues/6951)): Compressed history becomes invisible in UI, showing only internal eviction indices — violates user expectation of complete chat record.
- **Antivirus interference** ([#6847](https://github.com/agentscope-ai/QwenPaw/issues/6847)): QwenPaw process killed by security software during tasks; not seen with competitors.
- **Memory feature inconsistencies** ([#6853](https://github.com/agentscope-ai/QwenPaw/issues/6853)): Prompts promise MEMORY.md sync that doesn't happen — erodes trust in memory capabilities.

### Use Cases Observed
- **Financial data processing**: Multi-step tasks importing/verifying payment records ([#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921))
- **Group chat collaboration**: Matrix channel used with shared rooms ([#7001](https://github.com/agentscope-ai/QwenPaw/pull/7001))
- **Video production**: Long conversations with image history for story/video context ([#7008](https://github.com/agentscope-ai/QwenPaw/issues/7008))

### Satisfaction Signals
- **High engagement**: 33,748 stars on GitHub noted by community members
- **Active feature requests**: Users actively propose enhancements and alternative workflows
- **Mixed sentiment**: Enthusiasm for capabilities tempered by reliability and security concerns

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Why It Matters |
|-------|-----|----------------|
| [#6847](https://github.com/agentscope-ai/QwenPaw/issues/6847) — Antivirus kills QwenPaw | ~5 days | Serious adoption blocker; competitor comparison suggests behavioral fix possible |
| [#6955](https://github.com/agentscope-ai/QwenPaw/issues/6955) — Windows startup crash (v2.0.1, pip) | ~2 days | Affects pip-install users specifically; regression likely |
| [#7008](https://github.com/agentscope-ai/QwenPaw/issues/7008) — Anthropic false-sensitive-image rejection | ~1 day | Long-history sessions break; needs retry/fallback logic |
| [#6966](https://github.com/agentscope-ai/QwenPaw/issues/6966) — Telegram `/new` doesn't rotate session ID | ~1 day | State leak across "new" conversations; memory pollution |

### PRs Awaiting Review

| PR | Age | Why It Matters |
|-----|-----|----------------|
| [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) — Provider discovery unification | ~24 days | Large architectural change; blocking other provider-related work |
| [#6715](https://github.com/agentscope-ai/QwenPaw/pull/6715) — OneBot media localization | ~9 days | Addresses maintainer feedback; channels features stalled |
| [#6823](https://github.com/agentscope-ai/QwenPaw/pull/6823) — Capability templates for custom providers | ~6 days | Small but valuable; improves custom provider UX |

### Security Incident Watch
- **Two duplicate security reports** ([#6992](https://github.com/agentscope-ai/QwenPaw/issues/6992), [#6993](https://github.com/agentscope-ai/QwenPaw/issues/6993)) filed within 24h — one marked invalid, one open. The incident report PDF (sanitized) describes a full compromise chain. Needs immediate maintainer triage to confirm or deny.

---

**Project Health Assessment:** 🟡 **Stable with caution flags.** High development velocity with regular releases and active community engagement, but security reports and silent-failure bugs need priority attention to maintain trust. The v2.1.0 OS Shell release represents a major capability expansion that could attract new users — but only if stability concerns (antivirus compat, silent stops, context compression bugs) are addressed quickly.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-14

## 1. Today's Overview

ZeroClaw is in a period of high architectural activity, with 50 issues and 50 PRs updated in the last 24 hours. The project is deep into RFC-driven design work and security hardening, with major proposals around session persistence ownership (#9600), SOP permission contracts (#9598), and runtime-owned conversation sessions (#9487) all active. The maintainer decision queue (#8692) is processing a heavy load of RFCs, suggesting a deliberate, process-heavy approach to the v0.9.0 milestone. A significant number of high-severity bug fixes were merged, including critical security fixes for gateway pairing authentication (#9389), dashboard asset containment (#9969), and session queue eviction (#9674). The repository shows strong engagement from a set of repeat contributors (Audacity88, NiuBlibing, JordanTheJet, Project516), indicating a healthy, sustained contributor base.

## 2. Releases

No new releases were published in the last 24 hours. The project appears to be in an active development cycle targeting v0.9.0, with multiple RFCs and trackers explicitly referencing that milestone (e.g., #7432, #9598).

## 3. Project Progress

**Merged/Closed PRs (9 total)** — Key items that advanced the codebase:

- **[#9969] fix(gateway): contain filesystem dashboard assets** — High-priority security fix (P1) from Audacity88. Canonicalizes filesystem-backed dashboard asset paths, prevents symlink escapes, and rejects paths outside the configured distribution root. This closes a potential arbitrary-file-read vulnerability.
- **[#9674] fix(infra): preserve session queue serialization during eviction** — High-priority (P1) fix from Audacity88. Registers session requests while the session-slot map is locked, preventing idle eviction from removing a selected slot before its pending count is visible. Uses an RAII guard for tracking.
- **[#9932] ci(codeql): drop rust/hard-coded-cryptographic-value** — CI hygiene fix from JordanTheJet. Suppresses a CodeQL query producing 27 false-positive "critical" alerts, all inside `cfg(test)`.
- **[#9709] fix(tts): clean up Edge TTS temp output on every error path** — Bug fix for temp file leakage on error paths in the Edge TTS provider.
- **[#9705] fix(config): allow config set on existing hyphenated cron aliases (#9652)** — Fixes a regression where `zeroclaw config set` rejected cron aliases containing hyphens.
- **[#9980] ci(docker): sticky-disk layer cache for PR image builds on Blacksmith** — CI infrastructure improvement for Docker layer caching on Blacksmith runners.
- **[#9984] rust-cache useblacksmith path validation** — Temporary validation-only PR for the Blacksmith cache path, closed as intended.
- **[#9639] docs(architecture): document provider routing lifecycle** — Source-grounded documentation of provider routing, retry, fallback, and cooldown behavior.
- **[#8546] fix(cli): localize status fragments** — Routes remaining CLI status fragments through the i18n Fluent layer.

**Security fixes across the board**: The pairing lockout fix (#9389), dashboard asset containment (#9969), and Zhipu credential handling (#9968, still open) represent a concerted security hardening push.

## 4. Community Hot Topics

The most active discussions reveal a project wrestling with architectural boundaries and security policy:

- **[#8303] RFC: Goal mode v1 — bounded foreground Matrix work** (20 comments) — The most-discussed issue. Proposes a durable mechanism for pursuing bounded user objectives across multiple agent turns. Revision history shows scope-splitting into smaller deliverables. The high number of comments suggests this is a contentious or carefully-scrutinized design.
- **[#7155] RFC: Per-execution confirmation tier for high-risk shell commands** (18 comments) — Claude Code-style allow/ask/deny command policy. Revision 3 narrowed scope per maintainer review; still needs maintainer review. This is a user-facing security UX feature with broad implications.
- **[#8692] Maintainer decision queue tracker** (13 comments) — The central coordination surface for RFC acceptance/rejection/deferral. Its activity signals the project's process health.
- **[#6850] RFC: Decouple memory lifecycle policy from storage backends** (12 comments) — Architectural separation of memory lifecycle governance from backend storage.
- **[#9328] verifiable-intent evaluates constraints without verifying credential chain** (12 comments) — Security bug in the `vi_verify` constraint evaluation.
- **[#9487] RFC: Runtime-owned conversation sessions and transport surface adapters** (11 comments) — Coordinates with #9600; proposes moving session ownership to the runtime layer.

**Underlying needs**: These discussions reveal a project actively decomposing monolith features into well-owned contracts, with heavy emphasis on security boundaries, permission models, and clear ownership of cross-cutting concerns (sessions, memory, tool policy). The community is pushing for production-grade reliability (bounded fallback, verified credential chains, confirmation tiers) over raw feature velocity.

## 5. Bugs & Stability

**High severity (P1):**

- **[#9389] (CLOSED) unauthenticated POST /api/pair keys its lockout on an attacker-supplied header** — Security vulnerability: the pairing endpoint's lockout mechanism trusts an attacker-controlled header. **Fix: merged (PR #9969 contains the fix; #9389 itself closed).**
- **[#9328] verifiable-intent evaluates constraints without verifying the credential chain** — `vi_verify`'s `evaluate_constraints` does not cryptographically verify the chain before evaluating L2 constraints. **Open; PR #9942 (still open) addresses the related config surface issue, not the core verification bug.**
- **[#9929] headless SOP step turns given session path but never persisted** — Runtime bug: headless SOP turns build session paths but never write them to the session store. **Open; P1, accepted, blocked.**

**Medium severity (P2):**

- **[#9951] (CLOSED) WeChat channel code and 51 lib unit tests never compile in CI** — Feature-gated module excluded from all CI feature sets; CI never exercises the code. **Closed; likely fixed.**
- **[#9366] (CLOSED) WhatsApp Web accepts approval_timeout_secs and never reads it** — Config option silently ignored. **Closed.**
- **[#9710] (CLOSED) macOS desktop screenshot temp files leak on early return paths** — S3 cleanup issue. **Closed.**
- **[#9706] (CLOSED) Edge TTS temp output cleanup on error paths** — S3 cleanup issue. **Closed.**

**Trend**: The majority of bugs are being fixed quickly. Security bugs are being treated as P1 with rapid turnaround. The S3 cleanup fixes (temp file leaks) show good attention to operational hygiene.

## 6. Feature Requests & Roadmap Signals

The RFC and feature tracker activity strongly signals the v0.9.0 roadmap focus:

**High likelihood for v0.9.0:**

- **#7155 — Shell command policy (allow/ask/deny)**: Advanced revision, maintainer-scoped, likely to land as a core permission feature.
- **#9487/#9600 — Runtime-owned sessions**: A tracker (#9600) explicitly owns ordering/ownership for session persistence; this is near-certain for v0.9.0.
- **#9598 — SOP capability permission contract**: Target explicitly set as v0.9.0.
- **#7432 — v0.9.0 auth/security/gateway tracker**: Central coordination for breaking changes.

**Emerging features:**

- **#9810 — Agent Plugins 1.0 standard support** (`plugin.json` + `skills/` + `mcp.json`): Loading vendor-neutral community plugins. This is a significant ecosystem play.
- **#9945 — Browser tool expansion**: 16 of 100+ agent-browser commands exposed; iframes, dialogs, tabs, form controls reachable. Blocked/accepted.
- **#9887 — Downscale oversized images instead of dropping**: Multimodal limits currently hard-reject; proposed downscale + `0` to disable. Accepted/blocked.
- **#9895 — Provider-grouped Telegram /model picker**: UX improvement for mobile command use. Accepted.
- **#9880 — Typed peer policy instead of `Vec<String>` grammar**: Replacing string-encoded grants/denies with typed policy.
- **#9631 — Stable session_id to OpenRouter for prompt caching**: Cost reduction feature for a popular provider.
- **#5907 — Opt-in LSP support for ZeroCode**: Long-standing request (April) for language-server-backed code generation.
- **#6998 — Schema-validated memory consolidation**: Replacing prompt/parse-based JSON with schema validation.

**Predictions**: The security/permission cluster (#7155, #9598, #9880) plus the session-ownership work (#9487/#9600) will define v0.9.0's headline changes. The Agent Plugins support (#9810) has "next major feature" potential given its ecosystem reach.

## 7. User Feedback Summary

- **Pain point — Configuration drift**: Multiple issues (#7929, #9705, #9707) show users struggling with inconsistent config handling across surfaces (slash commands declared separately, bare vs. dotted provider aliases, hyphenated cron aliases). This suggests the config system's ergonomics are a recurring frustration.
- **Pain point — Silent failures**: #9366 (WhatsApp timeout never read), #9929 (headless SOP sessions not persisted), and #9942 (vi_verify withheld with no log sink) all describe features that accept settings or report success without actually functioning. Users are hitting "config accepted but ignored" behavior.
- **Pain point — Cost awareness**: #9631 (OpenRouter prompt caching) highlights real user cost sensitivity; a single conversation spawning dozens of LLM requests with repeated system prompts is expensive.
- **Pain point — Mobile UX**: #9895 (Telegram /model picker) reflects the difficulty of using text-based commands on mobile.
- **Positive signal — CI reliability work**: Multiple CI PRs (#9985, #9962, #9980, #9932) show contributors investing in build speed and correctness, which benefits all users.
- **Security-conscious community**: The volume of security-focused issues and PRs (pairing auth, dashboard containment, Zhipu JWT handling, verifiable-intent) from multiple independent contributors suggests an active, security-minded user base.

## 8. Backlog Watch

**Issues needing maintainer attention:**

- **[#5907] Opt-in LSP support for ZeroCode** (created 2026-04-19, P2, needs-author-action) — 4 months old, 6 comments, high risk. A significant feature request that has stalled awaiting author updates.
- **[#6850] RFC: Decouple memory lifecycle policy from storage backends** (created 2026-05-22, P2, needs-author-action) — 12 comments, active discussion but author needs to respond.
- **[#7155] Shell command policy RFC** (created 2026-06-03, P1, needs-maintainer-review) — 18 comments, revision 3 submitted 2026-08-05; has been through multiple revisions, needs a maintainer decision.
- **[#7943]** (not in top-30 list, but pattern suggests similar age) — check for other pre-June RFCs awaiting review.

**Blocked items that are accepted but not progressing:**

- **[#9945] Browser tool expansion** — Blocked/accepted; no clear owner or next step visible.
- **[#9887] Image downscaling** — Blocked/accepted; multimodal limits improvement is waiting on something.
- **[#9598] SOP permission contract** — Blocked; revision 3 submitted, needs review.

**Stale-candidate watch:**

- **[#8546] fix(cli): localize status fragments** — Closed (good), but it was flagged stale-candidate before merging.
- **[#9707] fix(config): migrate bare vision_model_provider** — Open since 2026-08-03 with needs-author-action; risk of going stale.

**Recommendation**: The maintainer decision queue (#8692) is the right mechanism, but #7155 (P1, 18 comments, 2+ months old) and #5907 (4 months old) are the two items most needing a decision — either acceptance, deferral with a clear rationale, or closure.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*