# OpenClaw Ecosystem Digest 2026-06-06

> Issues: 319 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-06 08:20 UTC

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

# OpenClaw Project Digest — 2026-06-06

## Today's Overview

OpenClaw shows **elevated community activity** with 319 issues and 500 pull requests updated in the last 24 hours—a high-traffic period suggesting both active development and user engagement. The project maintains a **healthy merge rate** (90 closed/merged PRs vs 410 open), though the open-to-closed issue ratio (182 open vs 137 closed) indicates a growing backlog. A new **v2026.6.5-beta.1** release shipped today, primarily addressing chat delivery quality-of-life fixes. The most urgent signals cluster around the **2026.6.1 upgrade wave**, which has introduced several regressions in OpenAI/ChatGPT Responses transport, Matrix dispatch, and SQLite migration paths.

## Releases

**v2026.6.5-beta.1** ([openclaw 2026.6.5-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5-beta.1)) was released today. Key highlights:
- **QQBot fix**: Model reasoning/thinking scaffolding (`<thinking>` tags) is now stripped before native delivery, preventing internal thought leakage into channel replies (#89913, #90132). Thanks @openperf.
- **MCP tool results**: Now coerce `resource_link`, `resource`, `audio`, and malformed image content types.

No breaking changes or migration notes are documented for this release.

## Project Progress

Today **137 issues were closed** and **90 PRs were merged/closed**, signaling a productive development cycle. Notable merged/closed items include:

- **Closed:** [#67035](https://github.com/openclaw/openclaw/issues/67035) — Windows chat UI regression (input text swallowed, streamed replies invisible) — this high-severity P1 bug from April is now resolved.
- **Closed:** [#78016](https://github.com/openclaw/openclaw/issues/78016) — Voice messages to agent not working on Matrix.
- **Closed:** [#71992](https://github.com/openclaw/openclaw/issues/71992) — WebChat assistant reply duplication regression (2026.4.21).
- **Closed:** [#90072](https://github.com/openclaw/openclaw/issues/90072) — Cron state silently wiped during SQLite migration on upgrade to 2026.6.1.
- **Closed:** [#86811](https://github.com/openclaw/openclaw/issues/86811) — WebChat dashboard freeze during tool calls with no WebSocket auto-reconnect.

Infrastructure/feature PRs awaiting merge include [#78441](https://github.com/openclaw/openclaw/pull/78441) (forwarding `toolsAllow` from `sessions_spawn` to subagents) and [#89712](https://github.com/openclaw/openclaw/pull/89712) (scheduled shell-style cron jobs via Codex).

## Community Hot Topics

The most active discussions this week reveal concentrated user concern around **post-upgrade regressions** and **provider transport issues**:

| Issue/PR | Comments | Reactions | Topic |
|----------|----------|-----------|-------|
| [#22438](https://github.com/openclaw/openclaw/issues/22438) | 17 | 0 | Tiered bootstrap file loading for progressive context control |
| [#67035](https://github.com/openclaw/openclaw/issues/67035) **(CLOSED)** | 14 | 0 | Windows chat UI regression (resolved) |
| [#90083](https://github.com/openclaw/openclaw/issues/90083) | 13 | 3 | OpenAI ChatGPT Responses transport fails for GPT-5.4/5.5 on 2026.6.1 |
| [#76562](https://github.com/openclaw/openclaw/issues/76562) **(CLOSED)** | 13 | 5 | High CPU & extreme RPC latency after upgrade to 2026.4.29/5.2 |
| [#78308](https://github.com/openclaw/openclaw/issues/78308) | 12 | 1 | Channel-mediated approval for MCP tool calls (consent envelope) |

**Underlying needs**: Users strongly desire **upgrade stability**—multiple top-voted threads document regressions introduced by minor version bumps. The MCP consent envelope proposal (#78308) shows growing demand for **fine-grained security controls** as agents gain more powerful tool access.

## Bugs & Stability

**Critical regressions reported today (2026-06-05/06):**

| Bug | Severity | Status | Fix PR |
|-----|----------|--------|--------|
| [#90083](https://github.com/openclaw/openclaw/issues/90083) — ChatGPT Responses transport fails for GPT-5.4/5.5 on 2026.6.1 | **P1** | Open | None identified |
| [#90093](https://github.com/openclaw/openclaw/issues/90093) — Native replay sends encrypted reasoning, breaks next turn with `invalid_encrypted_content` | **P1** | Open | None identified |
| [#90325](https://github.com/openclaw/openclaw/issues/90325) — Matrix channel dispatch broken in v2026.6.1 (`TypeError: Cannot read properties of undefined (reading 'run')`) | **P1** | Open | None identified |
| [#90428](https://github.com/openclaw/openclaw/issues/90428) — `exec` tool triggers gateway SIGTERM restart on WSL2 with Node 24 | **P1** | Open | None identified |
| [#90711](https://github.com/openclaw/openclaw/issues/90711) — launchd plist hardcodes `StandardErrorPath` to `/dev/null`, hides all gateway stderr (5.28 regression) | **P2** | Open | None identified |
| [#90466](https://github.com/openclaw/openclaw/issues/90466) — memory-core dreaming uses `.jsonl.deleted.*` paths; writes fallback despite valid prose responses | **P2** | Open | None identified |

**Stability concerns**: Three of the top P1 bugs are **direct regressions from the 2026.6.1 release**, indicating a problematic upgrade path. The WSL2 crash (#90428) and Matrix dispatch breakage (#90325) suggest platform-specific testing gaps.

## Feature Requests & Roadmap Signals

**High-signal feature requests trending this week:**

- **Per-agent memory-wiki vault** ([#63829](https://github.com/openclaw/openclaw/issues/63829), 9 👍, 9 comments) — Isolation of knowledge wikis per agent in multi-agent setups. Near-term viability: **High** — PR [#79745](https://github.com/openclaw/openclaw/pull/79745) ("Memory/QMD: isolate mcporter sidecars per agent") already exists and addresses a related isolation pattern.
- **Tiered bootstrap file loading** ([#22438](https://github.com/openclaw/openclaw/issues/22438), 17 comments) — Progressive context control to reduce token waste on sub-agents and cron jobs. Near-term viability: **Medium** — design is complex but addresses a common pain point.
- **Channel-mediated MCP approval** ([#78308](https://github.com/openclaw/openclaw/issues/78308), 12 comments) — Consent envelope for MCP tool calls. Near-term viability: **High** — extends an existing security pattern (shell-exec approval pipeline).
- **Per-candidate retry count** ([#59413](https://github.com/openclaw/openclaw/issues/59413), 9 comments) — Model fallback improvements for pool-based providers. Near-term viability: **High** — narrow, well-scoped enhancement.

**Likely for next release (v2026.6.x):** The Signal note-to-self support PR ([#90709](https://github.com/openclaw/openclaw/pull/90709)) and Slack `ignoreOtherMentions` config ([#89846](https://github.com/openclaw/openclaw/pull/89846)) are in "ready for maintainer look" status and may land soon.

## User Feedback Summary

**Positive signals:**
- Community contributors are actively closing longstanding bugs (Windows UI regression, Matrix voice messages, WebChat duplication).
- The project shows strong open-source health with 500+ PRs updated in 24h and diverse external contributors (32 unique authors in the top 50 issues alone).

**Pain points:**
1. **Upgrade anxiety**: Multiple users reported silent data loss (#90072 — cron state wiped), regressions (#90083, #90325), and performance degradation (#76562) after point releases. One operator notes: *"Upgrading from 2026.5.28 to 2026.6.1 silently wiped 44 of 45 cron jobs during the SQLite migration. Only 1 job survived."*
2. **MCP/subagent tool injection gaps**: Power users report that MCP tools are not propagated to subagent sessions despite configuration, breaking complex multi-agent workflows (#85030).
3. **Context window cost management**: The 3,500-token fixed tool schema tax (#14785) and bootstrap file token waste (#22438) frustrate users with large workspaces.
4. **Channel integration fragility**: Feishu reactions API regression (#66406, closed), Matrix dispatch crash (#90325), and iMessage send wedging (#90850) suggest ongoing platform-specific quality issues.

## Backlog Watch

**Issues needing maintainer attention (open >30 days, no fix PR):**

| Issue | Created | Comments | Impact |
|-------|---------|----------|--------|
| [#57256](https://github.com/openclaw/openclaw/issues/57256) — `openclaw status --deep` falsely reports mem0 as unavailable | 2026-03-29 | 6 | Session-state |
| [#37446](https://github.com/openclaw/openclaw/issues/37446) — Sub-agent timeout recovery creates duplicate API posts | 2026-03-06 | 5 | Message-loss |
| [#43015](https://github.com/openclaw/openclaw/issues/43015) — `message.send` schema overexposes poll/components causing GPT auto-population breakages | 2026-03-11 | 7 | Message-loss |
| [#14785](https://github.com/openclaw/openclaw/issues/14785) — Reduce tool schema token overhead (~3,500 tok/session) | 2026-02-12 | 7 | Session-state |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) — Tiered bootstrap file loading | 2026-02-21 | 17 | Session-state |
| [#58730](https://github.com/openclaw/openclaw/issues/58730) — exec() sandbox isolation and tool permission model | 2026-04-01 | 5 | Security |

**Oldest open issue in top 50:** [#14785](https://github.com/openclaw/openclaw/issues/14785) (Feb 12, 2026) — tool schema token optimization, 115 days without resolution.

**PRs stalled on author/maintainer:**
- [#69270](https://github.com/openclaw/openclaw/pull/69270) — Session compaction invariants fix (last updated Apr 20, status: "needs proof")
- [#79745](https://github.com/openclaw/openclaw/pull/79745) — Memory/QMD mcporter isolation per agent (last updated May 9, status: "waiting on author")

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report.

---

### Cross-Project Ecosystem Report — 2026-06-06

#### 1. Ecosystem Overview

The open-source personal AI agent ecosystem is characterized by intense, rapid iteration and a clear split between "core reference" platforms and specialized derivatives. While the ecosystem is maturing—evidenced by structured RFC processes, formal security models, and production-grade release cycles—it is currently navigating a period of painful post-upgrade regressions. A dominant trend is the community's demand for **operational stability** and **fine-grained security controls** (e.g., MCP consent envelopes, approval gates) as agents are trusted with more powerful tool access. Architecturally, the ecosystem is consolidating around **multi-provider**, **multi-channel**, and **multi-instance** deployment models, with a strong signal that users are moving from experimental use toward critical, automated workflows.

#### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release? | Health Score | Key Signal |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 319 | 500 | Yes (v2026.6.5-beta.1) | ★★★★☆ | High traffic, problematic upgrade wave (v2026.6.1) |
| **Hermes Agent** | 50 | 50 | Yes (v0.16.0) | ★★★★☆ | Post-major-release stabilization |
| **IronClaw** | 12 | 50 | No | ★★★★☆ | High refactor velocity (Reborn), blocked release |
| **ZeroClaw** | 50 | 50 | No | ★★★★☆ | Intense RFC-driven development, v0.9.0 roadmap |
| **NanoBot** | 8 | 19 | No | ★★★★☆ | Healthy feature-acceleration, team responsive |
| **CoPaw** | 17 | 12 | No | ★★★☆☆ | High community engagement, fix pipeline robust |
| **PicoClaw** | 2 | 21 | Yes (Nightly) | ★★★☆☆ | Stability-focused, strong fix velocity |
| **LobsterAI** | 0 | 9 | Yes (v2026.6.5) | ★★★☆☆ | Good release cadence, user-reported bugs aging |
| **NanoClaw** | 0 | 8 | No | ★★☆☆☆ | Consolidation phase, PRs stalling |
| **Moltis** | 4 | 5 | No | ★★★☆☆ | Responsive team, low community engagement |
| **NullClaw** | 0 | 1 | No | ★★☆☆☆ | Stagnant, single PR for new provider |
| **ZeptoClaw** | 2 | 1 | No | ★★☆☆☆ | Measured, maintainer-driven optimization |
| **TinyClaw** | 0 | 0 | No | ★☆☆☆☆ | No activity |

#### 3. OpenClaw's Position

OpenClaw is the clear **center of gravity** in the ecosystem by volume (319 issues, 500 PRs in 24h), dwarfing all other projects. Its primary advantage is breadth and community size, acting as the "reference implementation" that sets standards for provider integration and channel connectivity. However, this position comes with a significant cost: **upgrade fragility**. The v2026.6.1 release introduced multiple high-severity regressions (ChatGPT transport, Matrix dispatch, SQLite migration), eroding user trust and generating "upgrade anxiety"—a pain point less visible in smaller projects like NanoBot or PicoClaw, which are more narrowly scoped and easier to stabilize.

**Technical Approach:** OpenClaw's architecture is a large monorepo, leading to complex interdependencies between its many transports and data stores. In contrast, projects like ZeroClaw are proactively defining new architectures (e.g., pluggable security providers, WASM plugins) to manage this complexity from the ground up, while IronClaw is undertaking a massive "Reborn" refactor to decouple its components. OpenClaw's advantage in raw feature velocity is countered by a growing technical debt burden that its derivatives (like PicoClaw) are actively patching.

#### 4. Shared Technical Focus Areas

Several requirements are emerging independently across multiple projects, indicating strong market demand:

- **Fine-Grained Security & Approval Workflows:**
    - *OpenClaw*: MCP consent envelope (#78308), exec sandbox (#58730)
    - *IronClaw*: Approval gate refinement (#4386, #4390), WeCom approval bug (#4502)
    - *CoPaw*: `WriteFileOverwriteGuardian` (#4026)
    - *ZeroClaw*: Air-gapped mode (#6293), pluggable security provider (#7142), shell command confirmation (implicit in RFCs)

- **Multi-Instance & Context Isolation:**
    - *OpenClaw*: Per-agent memory wiki (#63829), agent isolation through sessions
    - *NanoBot*: Agent collaboration message bus (#3992)
    - *ZeroClaw*: A2A agent discovery (#7218)
    - *IronClaw*: Channel identity decoupling (#2551, though this is PicoClaw, the pattern is similar)

- **Provider Fallback & Resilience:**
    - *OpenClaw*: Per-candidate retry count (#59413)
    - *Hermes Agent*: Multiple OAuth fallback (#933)
    - *NanoClaw*: Poll-loop retry for 5xx errors (#2692)
    - *PicoClaw*: Fallback chain fix for expired contexts (#2905)

- **Desktop/Web UI Polish & Portability:**
    - *Hermes Agent*: v0.16.0 "Surface Release" (new Desktop UI)
    - *NanoBot*: Desktop WebUI polish (#4195)
    - *CoPaw*: Session sidebar reordering (#4971), mobile browser access (#4960)
    - *LobsterAI*: Modal data loss bugs (#1468-#1470)

- **Memory & Context Management:**
    - *OpenClaw*: Tiered bootstrap file loading (#22438), tool schema token overhead (#14785)
    - *NanoBot*: Long-term memory inference reinforcement (#4212)
    - *PicoClaw*: `/context` fix for clarity (#2985)
    - *CoPaw*: `/compact` model input length bug (#4937), context compression persistence (#4661)

#### 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | IronClaw | ZeroClaw | NanoBot |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Primary Focus** | Ubiquitous connectivity & feature breadth | Desktop-first experience | Enterprise architecture (Reborn) | Secure, modular framework | Lightweight, fast iteration |
| **Target User** | Power users, self-hosters | Desktop users, multi-instance | Enterprise teams, Slack/WeCom users | Security-conscious developers | Developers, SDK embedders |
| **Architecture Approach** | Large monorepo, rapid feature additions | "Ship and fix" cycle | Major refactor (Reborn) to decouple | RFC-driven, pluggable traits (WASM) | Modular SDK, community contributions |
| **Community Style** | Massive, diverse but facing churn | Engaged, rapid feedback | Structured, maintainer-driven | Governance-oriented, formal RFC process | Responsive, welcoming to newcomers |
| **Key Weakness** | Upgrade regression risk | Non-standard environment fragility | Stalled release pipeline | Configuration complexity, Windows UX | PR review bottlenecks |

#### 6. Community Momentum & Maturity

- **Tier 1: High-Velocity Iteration (Active Development, Post-Release Stabilization)**
    - **OpenClaw, Hermes Agent, IronClaw, ZeroClaw**: These projects are experiencing the highest throughput of issues and PRs. They are either recovering from a major release (Hermes, OpenClaw) or deep into a foundational refactor (IronClaw, ZeroClaw). This tier is where the most architectural risk and innovation is concentrated.

- **Tier 2: Healthy Feature-Acceleration (Stable Core, Adding Features)**
    - **NanoBot, PicoClaw, CoPaw, LobsterAI**: These projects show a strong, consistent cadence of merging fixes and features. They have a stable core with fewer regressions than Tier 1. Community engagement is high, and the maintainer teams are responsive.

- **Tier 3: Consolidation or Stalling (Low Activity, Blocked Items)**
    - **NanoClaw, NullClaw, ZeptoClaw, TinyClaw**: These projects show low activity or are stalled. NanoClaw and NullClaw have open PRs that are not being merged, indicating a potential bottleneck. ZeptoClaw is maintainer-optimizing with low community engagement, while TinyClaw is dormant.

#### 7. Trend Signals for AI Agent Developers

1.  **Operational Stability Over New Features**: The strongest signal from the community is a cry for stability. Users are actively frustrated by silent data loss during upgrades (OpenClaw #90072), broken transport protocols after minor version bumps (OpenClaw #90083), and unexpected costs from implicit API key detection (Hermes Agent #32524). **Developers should prioritize robust migration paths, comprehensive E2E testing before release, and clear communication of breaking changes.**

2.  **The Security Moat is the Next Battleground**: The proliferation of RFCs for MCP consent, approval gates, air-gapped modes, and sandbox execution indicates that agents are moving beyond "chat toys" to become autonomous workers. **Implementing secure tool execution, credential management, and audit trails is no longer optional—it is a prerequisite for production deployment.**

3.  **The Rise of the Edge Device**: Projects like ZeptoClaw (binary-size gates for aarch64 at 7MB) and the focus on WASM plugins in ZeroClaw signal a push toward deployment on low-resource, local-first devices (robots, Raspberry Pis, Apple Silicon). **Developers targeting the edge should optimize for binary size, memory footprint, and offline capability.**

4.  **Multi-Agent is the New Single-Agent**: The focus on agent collaboration (NanoBot #3992), work lanes (ZeroClaw #6808), and per-agent memory isolation (OpenClaw #63829) confirms that the ecosystem is shifting from single, monolithic agents to swarms of specialized subagents. **Building for inter-agent communication, shared context, and partitioned responsibility is a key architectural choice.**

5.  **Channel Integration is a Source of Fragility**: From Matrix dispatch crashes (OpenClaw #90325) to WeCom approval loops (IronClaw #4502) to Signal DM drops (NanoClaw #2694), channel-specific bugs are a major source of user frustration. **A robust channel abstraction layer with comprehensive testing across platforms is critical for maintaining user trust.**

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-06

## 1. Today's Overview
NanoBot saw a surge of activity with **19 PRs** and **8 Issues** updated in the last 24 hours, signaling a healthy development pace. Three PRs were merged/closed, including a critical SDK fix for MCP connection teardown. Community contributions are strong, with 7 new PRs opened today from external developers adding features like Exa search integration, DingTalk group allowlisting, and fork-from-here WebUI functionality. The project has no new release today, but the volume of merges suggests a release may be imminent. Overall, the project is in a robust maintenance and feature-acceleration phase.

## 2. Releases
**No new releases today.** The latest release remains nanobot v0.1.4.post6. However, with 3 PRs merged and a desktop surface PR (#4195) nearing completion, a new version may arrive within days.

## 3. Project Progress
**3 PRs merged/closed today:**

- **`#4216` — fix(sdk): close MCP connections from Nanobot facade** (closed/merged)  
  Critical fix for Issue #4211 where SDK usage with stdio MCP servers caused `RuntimeError: Attempted to exit cancel scope in a different task` at shutdown.  
  [GitHub](https://github.com/HKUDS/nanobot/pull/4216)

- **`#4210` — Fix desktop restart token and replay gaps** (closed/merged)  
  Addresses WebUI bootstrap token refresh after native engine restart, WebSocket transcript persistence for replay, and desktop notifications for streamed replies.  
  [GitHub](https://github.com/HKUDS/nanobot/pull/4210)

- **`#3968` — feat(command): add /skill slash command to list enabled skills** (closed/merged)  
  Resolves Issue #3959 where disabled skills were incorrectly listed. Adds a `/skill` built-in command showing only enabled skills (name + description).  
  [GitHub](https://github.com/HKUDS/nanobot/pull/3968)

**Features advanced (open PRs with recent updates):**
- **Desktop WebUI polish** (#4195) — First open desktop surface with file preview, skills, and automation APIs  
- **Extra query support for OpenAI providers** (#4217) — Enables Azure-style `?api-version=` params  
- **Exa web search provider** (#4213) — New search backend integration  
- **Agent collaboration message bus** (#3992) — Cross-instance agent communication  
- **DingTalk group allowlisting** (#4206) — `group_allow_from` config support

## 4. Community Hot Topics

**Most active Issues:**

1. **`#2573` — Github Copilot login failure** (4 comments, 9 👍)  
   *Closed today* — `Authorization header is badly formatted` error after switching from litellm to openai library. High community interest (9 reactions).  
   [GitHub](https://github.com/HKUDS/nanobot/issues/2573)

2. **`#3959` — /skill command lists disabled skills** (4 comments)  
   *Closed today* — Fixed by PR #3968 which now properly filters disabled skills.  
   [GitHub](https://github.com/HKUDS/nanobot/issues/3959)

3. **`#4212` — History reinforcement of unconfirmed inferences** (0 comments, new)  
   Deep design discussion about long-term memory consolidator potentially reinforcing unverified LLM inferences as facts.  
   [GitHub](https://github.com/HKUDS/nanobot/issues/4212)

**Underlying needs:** The Copilot login issue (#2573) reveals the complexity of OAuth integration changes, while the memory inference problem (#4212) shows advanced users thinking about long-term factual integrity in agent memory systems — a sophisticated architectural concern.

## 5. Bugs & Stability

**High Severity:**

- **`#4211` — SDK leaves stdio MCP open → `exit cancel scope` RuntimeError**  
  *Fix PR #4216 merged today.* SDK embedding with stdio MCP servers crashed at shutdown. This is now resolved.  
  [GitHub](https://github.com/HKUDS/nanobot/issues/4211)

**Medium Severity:**

- **`#4203` — `find_legal_message_start` discards all messages after orphan tool result**  
  *Fix PR #4215 open.* When user message is followed by an orphan tool result, `retained[start:]` becomes empty, dropping entire conversation. PR changes to drop only the orphan result.  
  [GitHub](https://github.com/HKUDS/nanobot/issues/4203)

- **`#1946` — Matrix test error on `main`**  
  *Open since March 2026.* Integration test failure with no clear resolution path. Low recent activity.  
  [GitHub](https://github.com/HKUDS/nanobot/issues/1946)

**Low Severity:**

- **`#3959` — /skill command lists disabled skills** (now fixed via #3968)

**Regressions:** The Copilot login issue (#2573) was identified as a regression from switching providers, now closed.

## 6. Feature Requests & Roadmap Signals

**Likely incoming (PRs with high merge readiness):**

- **Extra query for OpenAI providers** (#4204/#4217) — High demand for Azure-style gateways. PR #4217 opened today, likely to merge quickly.  
- **Exa web search** (#4213) — New search provider, first-time contributor, well-structured PR.  
- **DingTalk group allowlist** (#4206) — Enterprise chat platform feature, clean implementation with tests.

**Predictions for next release (v0.1.5):**
- Desktop WebUI polish (#4195)
- Agent collaboration bus (#3992)
- Extra query support (#4217)
- Exa search provider (#4213)
- Multiple SDK/MCP stability fixes

**Long-term signals:**

- **`#4212` — Memory inference reinforcement prevention** suggests growing sophistication around long-term memory architecture  
- **`#4202` — Filesystem workspace write policy clarification** indicates tightening of security boundaries  
- **`#4190` — Tool call validation strictness** shows hardening of core agent execution

## 7. User Feedback Summary

**Pain points:**
- **Copilot OAuth failures** (#2573) — Users frustrated by authentication regression after library switch
- **Disabled skills still visible** (#3959) — Configuration not respected, now fixed
- **SDK crashes at shutdown** (#4211) — Embedding nanobot in custom apps was broken for MCP users
- **Conversation truncation** (#4203) — Rare edge case but catastrophic when hit

**Use cases revealed:**
- **Enterprise gateway integration** (#4204) — Azure OpenAI and similar gateways with query-param requirements
- **Voice/image chat** (#4132) — Custom image generation providers like Agnes AI
- **Multi-instance agents** (#3992) — Users want independent agents collaborating
- **Custom search providers** (#4213) — Demand for niche search engines beyond Google/Bing

**Satisfaction signals:** The rapid merging of user-reported bugs (3 closed today) indicates a responsive maintainer team. Multiple first-time contributors (erikmackinnon, bymle, lmzopq) suggest good onboarding experience.

## 8. Backlog Watch

**Critical long-unanswered items needing maintainer attention:**

1. **`#1946` — Matrix test error on `main`** (opened 2026-03-13, 0 maintainer responses)  
   Core integration test is broken on main branch. Low activity but blocks CI confidence for Matrix channel.  
   [GitHub](https://github.com/HKUDS/nanobot/issues/1946)

2. **`#1408` — Add unit-test workflow with coverage gate** (PR opened 2026-03-02)  
   Still open after 3 months. Would significantly improve CI quality, but reviews stalled.  
   [GitHub](https://github.com/HKUDS/nanobot/pull/1408)

3. **`#1284` — Add CI workflow with quality checks** (PR opened 2026-02-27)  
   Similar to #1408, competing PR for CI pipeline. Hasn't received maintainer feedback in months.  
   [GitHub](https://github.com/HKUDS/nanobot/pull/1284)

4. **`#3538` — Gateway start/stop/restart commands** (PR opened 2026-04-29)  
   Adds CLI commands for gateway lifecycle management. No comments from maintainers.  
   [GitHub](https://github.com/HKUDS/nanobot/pull/3538)

**Assessment:** The competing CI PRs (#1284 vs #1408) suggest duplicated effort that maintainers should consolidate. The Matrix test failure (#1946) has been silently broken for nearly 3 months, which may reflect lower priority of the Matrix integration.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for June 6, 2026.

---

## Hermes Agent Project Digest — 2026-06-06

### 1. Today's Overview
Hermes Agent is in a period of extremely high-velocity development following the release of v0.16.0 ("The Surface Release") yesterday. The project saw 50 issues and 50 PRs updated in the last 24 hours, indicating a highly engaged community and an active core team. Activity is heavily focused on stabilizing the new desktop application, fixing regressions in gateway integrations (Matrix, Discord, WeCom), and resolving infrastructure bugs on non-standard platforms like Termux/Android and containerized environments. The surge in new issues (many from today) suggests broad adoption is generating rapid feedback, while the concurrent rapid-fire PRs demonstrate a strong "ship and fix" cycle.

### 2. Releases
**New Release:** [v0.16.0 (v2026.6.5) — The Surface Release](https://github.com/NousResearch/hermes-agent/releases/tag/v2026.6.5)
This is a massive release (874 commits, 542 merged PRs, 399 issues closed) representing a significant milestone for Hermes, likely introducing the new Desktop client and Dashboard TUI as first-class interfaces. The high number of closed issues (including 2 P0 and 62 P1) suggests this release tackled major technical debt and stability problems. No explicit breaking changes or migration notes were provided in the summary snippet, but the sheer scale implies users upgrading from v0.15.2 should review the full changelog.

### 3. Project Progress
Four PRs were merged or closed today. The standout merged PR is a long-standing feature request:
- **[PR #11506 (Closed)](https://github.com/NousResearch/hermes-agent/pull/11506):** Adds support for custom profile alias names in `hermes profile list/show`. This allows users with complex wrapper setups to see human-readable names (e.g., "qiaobusi") instead of raw profile names.
- **[PR #40293 (Closed)](https://github.com/NousResearch/hermes-agent/issues/40293):** A feature request for a persistent right-side TUI dashboard was closed, likely deprecated in favor of the new v0.16.0 Dashboard TUI.
- **[Issue #40277 (Closed)](https://github.com/NousResearch/hermes-agent/issues/40277):** A critical bug regarding `fallback_model` as a list returning an empty chain was fixed, likely by a commit today.

### 4. Community Hot Topics
- **[Issue #10221: `/skills` is unknown](https://github.com/NousResearch/hermes-agent/issues/10221)** (7 comments): A long-standing CLI bug where the `/skills` command is not recognized. Despite being closed today, the high comment count suggests it was a persistent frustration for users new to the CLI.
- **[Issue #30399: Matrix gateway fails from Docker](https://github.com/NousResearch/hermes-agent/issues/30399)** (5 comments): A clear documentation/build issue where a required dependency (`mautrix[encryption]`) is missing from the Docker image. This is a blocker for anyone trying to use Matrix in a containerized setup.
- **[Issue #933: Support multiple OAuth tokens with automatic fallback](https://github.com/NousResearch/hermes-agent/issues/933)** (5 comments): A feature request with high support (3 👍). Users with multiple Codex accounts want automatic failover between tokens to manage rate limits and separate work/personal accounts.

**Underlying Need:** The community is aggressively pushing Hermes into production-like and multi-account/network environments. The demand for reliable fallback behavior (OAuth, provider routing, failover) is a clear signal that users trust Hermes enough to automate critical workflows, and they need resilience.

### 5. Bugs & Stability
Several bugs reported today are critical or high-severity:
- **P1 - [Issue #27564: Gateway interrupts `clarify` replies](https://github.com/NousResearch/hermes-agent/issues/27564):** Gateway unconditionally discards user text input during a clarify prompt, treating the answer as an interrupt. **A fix PR exists: [PR #40359](https://github.com/NousResearch/hermes-agent/pull/40359).**
- **P1 - [Issue #32524: Gateway silently uses cloud API keys from environment](https://github.com/NousResearch/hermes-agent/issues/32524):** A serious security/cost concern. The gateway auto-picks up `ANTHROPIC_API_KEY` without warning, leading to ~$80 in unexpected charges. No explicit fix PR yet, but this is likely a high priority.
- **P2 - [Issue #40324: Webhook CLI shows "platform not enabled"](https://github.com/NousResearch/hermes-agent/issues/40324):** A CLI bug where `webhook list`/`subscribe` commands fail even when the gateway confirms the webhook is connected.
- **P2 - [Issue #40328: `hermes update` fails in Termux/PRoot environments](https://github.com/NousResearch/hermes-agent/issues/40328):** Two distinct errors prevent updates on Android's Termux. **A fix PR exists: [PR #40377](https://github.com/NousResearch/hermes-agent/pull/40377).**
- **New Regressions:** Issues [#40368 (Docker DooD paths)](https://github.com/NousResearch/hermes-agent/issues/40368) and [#40369 (TUI auto-refresh jitter)](https://github.com/NousResearch/hermes-agent/issues/40369) are fresh bugs from the v0.16.0 release.

### 6. Feature Requests & Roadmap Signals
- **Next Likely Release (v0.16.1+):** The volume of bugs reported today, especially P1 gateway and P2 CLI issues, strongly suggests the next release will be a stability patch. Features like the [Android app](https://github.com/NousResearch/hermes-agent/issues/40327) and [Russian locale](https://github.com/NousResearch/hermes-agent/issues/40347) are low-effort, high-impact additions that could easily be included.
- **Mid-Term Features:**
    - **Remote Desktop Client:** [Issue #37663](https://github.com/NousResearch/hermes-agent/issues/37663) and [Issue #36970](https://github.com/NousResearch/hermes-agent/issues/36970) both request first-class support for connecting the desktop app to an existing remote Hermes instance. This is a highly demanded capability for power users.
    - **Profile Sync:** [PR #39343](https://github.com/NousResearch/hermes-agent/pull/39343) proposes `hermes sync` for backing up profiles to a personal git repo. This aligns with the need for portability and disaster recovery.
    - **Persistent TUI Dashboard:** [Issue #40294](https://github.com/NousResearch/hermes-agent/issues/40294) requests a right-side panel for system metrics, which is a direct UX inspiration from OpenCode.

### 7. User Feedback Summary
- **Pain Points:** The most intense pain points revolve around **stability in non-standard environments** (Termux, Docker, Docker-outside-of-Docker, Unraid) and **surprising behavior** (unexpected API costs when env vars are set, CLI commands failing despite successful setup). Users are clearly pushing Hermes into edge-case deployments.
- **Dissatisfaction:** There is frustration with **false starts** in the desktop client onboarding (cannot connect to existing remote instances) and the **"babysitting" feeling** from tool-call limits ([Issue #6997](https://github.com/NousResearch/hermes-agent/issues/6997)).
- **Satisfaction:** The rapid pace of fixes and community engagement (e.g., a user submitting the Russian locale installer [Issue #40347](https://github.com/NousResearch/hermes-agent/issues/40347)) indicates a strong, invested user base that believes in the project's trajectory.

### 8. Backlog Watch
- **[Issue #15973: WeCom cannot receive files](https://github.com/NousResearch/hermes-agent/issues/15973) (Updated Apr 26, 2026):** A P2 bug for WeCom file reception that the reporter claims was supposedly "repaired" but still persists. A new PR [#40372](https://github.com/NousResearch/hermes-agent/pull/40372) today attempts to fix a related WeCom file download issue, which may resolve this.
- **[Issue #35184: Symlinked skills invisible to `skill_manage`](https://github.com/NousResearch/hermes-agent/issues/35184) (Updated May 30, 2026):** A subtle but annoying bug where `Path.rglob` doesn't follow symlinks, breaking skill management for users who use symlinks for organization. No active PR.
- **[Issue #6997: What is tool-call limit?](https://github.com/NousResearch/hermes-agent/issues/6997) (Updated Apr 10, 2026):** A user question that has devolved into a support ticket. The absence of a clear "can't finish task" documentation or a configurable limit is causing user frustration. This points to a documentation gap.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-06

## Today's Overview

PicoClaw shows strong development velocity with 21 PRs updated in the last 24 hours (19 merged/closed), matching one of the busier days in recent weeks. A new nightly build `v0.2.9-nightly.20260606.89ee8f1b` was released, though marked as potentially unstable. Core infrastructure fixes dominated the day's merged work—goroutine leaks during reload, OneBot group messaging routing, type assertion panics, and context display clarity. Two new open issues emerged, including a Windows QQ channel connection failure, while a long-standing skill-creator documentation gap (Issue #652, open since February) remains unresolved. Overall, this is a high-velocity, stability-focused period for the project.

## Releases

**New: Nightly Build v0.2.9-nightly.20260606.89ee8f1b**
- Automated nightly build from `main` branch, may be unstable
- No migration notes or breaking changes documented
- **Full Changelog**: https://github.com/sipeed/picoclaw/compare/v0.2.9...main

No stable patch releases today.

## Project Progress

19 PRs were merged/closed in the last 24 hours, reflecting substantial infrastructure hardening:

**Core Engine Fixes:**
- [#3014](https://github.com/sipeed/picoclaw/pull/3014) — Fix goroutine leak in `Manager.Reload()`: dispatch tasks now properly cancel old goroutine contexts on channel reload; nil-guard for `ts.agent` on concurrent shutdown
- [#2985](https://github.com/sipeed/picoclaw/pull/2985) — `/context` command now shows both `SummarizeAtTokens` and `CompressAtTokens`, resolving confusion reported in Issue #2968
- [#3009](https://github.com/sipeed/picoclaw/pull/3009) — OneBot group reply routing fixed: inbound `ChatID` now uses `group:` prefix so replies use `send_group_msg` instead of `send_private_msg`
- [#3010](https://github.com/sipeed/picoclaw/pull/3010) — Added `ok` checks for type assertions in `toChannelHashes` to prevent panics from unexpected JSON config values

**Tooling & Security:**
- [#2965](https://github.com/sipeed/picoclaw/pull/2965) — Workspace guard no longer misreads scheme-less URLs (e.g., `curl -s "wttr.in/Beijing"`) as absolute paths
- [#2900](https://github.com/sipeed/picoclaw/pull/2900) — Added CSRF protection, path traversal validation (`filepath.Clean` + `isWithinDir`), and security headers to web backend

**Documentation:**
- [#3013](https://github.com/sipeed/picoclaw/pull/3013) — Removed references to missing `init_skill.py` and `package_skill.py` from skill-creator SKILL.md

**Dependencies:**
- 5 automated dependency bumps merged (react 19.2.6, shadcn 4.8.0, TanStack Router 1.170.6, React Query 5.100.11, Tabler Icons 3.44.0, go.mau.fi/util 0.9.9)

**SiYue-ZO's stale batch (all merged):**
- [#2913](https://github.com/sipeed/picoclaw/pull/2913) — JSONL session index: fixed hot-path cloning and TTL refresh semantics
- [#2907](https://github.com/sipeed/picoclaw/pull/2907) — JSONL store: fixed metadata drift after crashes (consistency between `.jsonl` and `.meta.json`)
- [#2905](https://github.com/sipeed/picoclaw/pull/2905) — Fallback chain: expired contexts now stop chain immediately instead of trying later candidates
- [#2908](https://github.com/sipeed/picoclaw/pull/2908) — Web UI: restored provider logo fallbacks on models page after backend-catalog refactor
- [#2915](https://github.com/sipeed/picoclaw/pull/2915) — Added `CommonModels` for MiMo provider (`mimo-v2.5` multimodal, `mimo-v2.5-pro` text-only)

**Still open large PR:**
- [#2551](https://github.com/sipeed/picoclaw/pull/2551) — Major refactor to decouple channel names from provider types (open since April 16)

## Community Hot Topics

**Most commented Issue:**
- [#3015](https://github.com/sipeed/picoclaw/issues/3015) — ❗ **NEW**: QQ channel connection failure on Windows after release build. Token retrieval timeout from `bots.qq.com`. Pico channel works fine. 0 comments yet, but reports a fresh regression in the Windows build.

**Most reacted Issue (continued):**
- [#2968](https://github.com/sipeed/picoclaw/issues/2968) — `/context` showing only compression threshold (now **resolved** in PR #2985 merged today). User satisfaction likely increased with the fix clarifying both thresholds.

**Long-running open Issue with continued updates:**
- [#652](https://github.com/sipeed/picoclaw/issues/652) — Skill-creator audit task (open since Feb 22). Updated yesterday; PR #3013 addressed documentation references, but the core validation still tracked as incomplete.

**Underlying need:** Users want **transparency** in memory management (thresholds), **reliable channel connectivity** across platforms (QQ, Windows), and **working documentation** for skill creation workflows.

## Bugs & Stability

| Severity | Issue | Status | Notes |
|----------|-------|--------|-------|
| 🔴 High | [#3015](https://github.com/sipeed/picoclaw/issues/3015) — QQ channel fails on Windows | **Open, 0 comments** | Token retrieval timeout on `picoclaw gateway`; Pico channel works. No fix PR yet. |
| 🟡 Medium | [#3002](https://github.com/sipeed/picoclaw/issues/3002) — OneBot group reply uses `send_private_msg` | **Closed** | **Fixed** in PR [#3009](https://github.com/sipeed/picoclaw/pull/3009) (merged today) |
| 🟡 Medium | #2968 — `/context` shows only compression threshold | **Closed** | **Fixed** in PR [#2985](https://github.com/sipeed/picoclaw/pull/2985) (merged today) |
| 🟢 Low | #3010 — Panic risk from unchecked type assertions | **Closed** | **Fixed** in PR [#3010](https://github.com/sipeed/picoclaw/pull/3010) (merged today) |
| 🟢 Low | #3014 — Goroutine leak on reload | **Closed** | **Fixed** in PR [#3014](https://github.com/sipeed/picoclaw/pull/3014) (merged today) |

**Key stability improvements merged today:** Crash consistency in JSONL storage (PR #2907), context deadline handling in fallback chains (PR #2905), and web security hardening (PR #2900).

## Feature Requests & Roadmap Signals

**Likely for next release:**
- **Image compression pipeline** — PR [#2964](https://github.com/sipeed/picoclaw/pull/2964) (still open) adds configurable multi-level inbound image compression before building model payloads, reducing token waste for vision providers. High value for MiniMax/MiMo users.
- **Channel identity decoupling** — PR [#2551](https://github.com/sipeed/picoclaw/pull/2551) (open since April) would allow multiple instances of the same channel provider. If merged, enables setups like two distinct QQ bots or multiple Matrix homeservers.

**User requests visible in new issues:**
- [#3015](https://github.com/sipeed/picoclaw/issues/3015) implies demand for **reliable Windows builds** and QQ channel support, likely from Chinese users on the platform.
- The Cluster WebUI logo fix (PR #2908) shows users care about UI polish and provider recognition.

**Predictions:** Image compression (PR #2964) has strong community value and may be merged next week. The QQ Windows regression (Issue #3015) is blocking for Windows users and will likely be prioritized.

## User Feedback Summary

**Positive signals:**
- Fix for #2968 (clearer `/context` output) directly addresses user confusion—the `SummarizeAtTokens` display was explicitly requested
- Workspace guard URL handling fix (PR #2965) resolves an actual workflow blocker for `curl` users under `restrict_to_workspace`
- OneBot group reply fix (PR #3009) restores expected behavior for Chinese QQ/NapCat users

**Pain points:**
- **Windows QQ connectivity** (#3015) is a **new regression** in the release build—critical for Chinese users
- **Skill-creator documentation** (#652) has been broken for 3.5 months; PR #3013 only patches documentation, not the underlying missing scripts
- **Nightly-only fixes** — several important fixes are in nightly builds only, meaning stable users on v0.2.9 may still experience issues with token budget display and OneBot routing (though these fixes are fresh and may appear in next stable)

## Backlog Watch

| Item | Age | Priority |
|------|-----|----------|
| [#652](https://github.com/sipeed/picoclaw/issues/652) — Skill-creator audit | 104 days | 🟡 **Medium** — Documentation patched today but scripts still missing. New users creating skills hit dead end. |
| [#2551](https://github.com/sipeed/picoclaw/pull/2551) — Channel identity refactor | 51 days | 🟢 **Low** — Large, risky refactor with no recent activity. Needs maintainer review before it accumulates more merge conflicts. |
| [#2964](https://github.com/sipeed/picoclaw/pull/2964) — Image compression | 9 days | 🟢 **Low** — Fresh PR, no comments from maintainers yet. Staleness risk. |
| [#3015](https://github.com/sipeed/picoclaw/issues/3015) — QQ on Windows | <1 day | 🔴 **High** — Brand new regression. Needs immediate triage. |

**Maintainer attention needed:** The QQ Windows regression (#3015) is the most urgent item. The skill-creator issue (#652), though old, is still blocking self-service workflows and should be addressed in full (not just documentation). The image compression PR (#2964) is a community contribution that should receive maintainer feedback soon to avoid becoming stale.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**Project Digest: NanoClaw**
**Date:** 2026-06-06

---

### 1. Today's Overview
NanoClaw shows moderate activity today, driven entirely by a backlog of **8 open Pull Requests** updated within the last 24 hours, though none were merged or closed. There were **zero new issues** created or updated, and **no new releases** were published. The project appears to be in a consolidation phase, with maintainers actively pushing fixes and features toward completion but not yet integrating them into the main branch. The lack of fresh bug reports or community issues suggests a stable user base, but the stalled state of several weeks-old PRs may indicate a bottleneck in review or merge capacity.

---

### 2. Releases
**None.** No new versions or tags were released today.

---

### 3. Project Progress
**Merged/Closed PRs Today:** 0

**Open PRs Updated Today (no merge activity):**
- **PR #2694** – [Fix] Signal adapter: set `isMention`/`isGroup` on inbound DMs to prevent silent dropping of direct messages.
- **PR #2693** – [Skill] Added `/add-google-contacts-tool` as a sibling to existing Gmail/GCal tools (MCP server bundle).
- **PR #2531** – [Fix] Poll-loop: suppress duplicate text when `send_message` fires mid-turn.
- **PR #2184** – [Fix] Poll-loop: retry immediately on stale session instead of delivering error to user.
- **PR #2230** – [Fix] Container runner: map host user via `keep-id` for rootless Podman.
- **PR #2349** – [Fix] Mount security: tolerate allowlist entries missing a path field.
- **PR #2208** – [Feat] MCP: support HTTP and SSE MCP server transports.
- **PR #2692** – [Fix] Poll-loop: retry transient 5xx API errors, notify on exhaustion (author: ddaniels).

*Assessment:* The backlog is dominated by `fix(poll-loop)` and infrastructure fixes (container, security, transport). No features were landed today.

---

### 4. Community Hot Topics
**Most Active Items (by comments/reactions):** None of the open PRs or issues have recorded comments or reactions today. All have `0` comments and `👍: 0`.

**Analysis:** The absence of community engagement on these PRs suggests either:
- The changes are low-level and uncontentious (e.g., Signal adapter fix, mount security).
- Community awareness or review capacity is low.
- The discussion may be happening off-GitHub (e.g., Discord, internal chats).

Notable PRs that address visible user pain points:
- **PR #2694** (Signal DMs dropped) – likely a high-impact fix for Signal users.
- **PR #2692** (5xx retry exhaustion) – directly addresses user-visible error spam.

---

### 5. Bugs & Stability
**New Bugs Reported Today:** 0

**Active Fix PRs (not merged):**
| Severity | Bug Description | Fix PR | Status |
|----------|----------------|--------|--------|
| High | Signal inbound DMs silently dropped (missing `isMention`/`isGroup`) | #2694 | Open |
| Medium | Duplicate text output when `send_message` fires mid-turn | #2531 | Open (since May 18) |
| Medium | Stale session errors delivered as user-visible messages | #2184 | Open (since May 2) |
| Medium | 5xx API errors (e.g., 529 Overloaded) shown to user instead of retry | #2692 | Open (since Jun 5) |
| Low | Container runner breaks under rootless Podman (uid mapping) | #2230 | Open (since May 3) |
| Low | Crash/mount failure if allowlist entry lacks `path` field | #2349 | Open (since May 8) |

*Note:* No bug reports were filed today, but multiple fixes for known bugs remain unmerged.

---

### 6. Feature Requests & Roadmap Signals
**New Feature Requests Today:** 0

**Roadmap Signals from Open PRs:**
- **PR #2693** – `/add-google-contacts-tool`: Indicates continued investment in the Google Workspace tool suite (Gmail, GCal, now Contacts). Likely to land soon.
- **PR #2208** – HTTP and SSE MCP server transports: A significant architecture expansion, enabling MCP servers beyond stdio. This could unlock remote/cloud-hosted MCP skills. Wait time: 33 days (opened May 3).

**Prediction for Next Release:**
- The `/add-google-contacts-tool` (PR #2693) is small and self-contained — likely to be merged next.
- The Signal DM fix (PR #2694) is a clear bug that affects core functionality — high priority.
- The MCP transport expansion (PR #2208) may be deferred due to its scope and review time.

---

### 7. User Feedback Summary
**Direct Feedback (Issues/Comments):** None recorded today.

**Inferred Pain Points from Open PRs:**
- **Signal users:** Inbound DMs are being silently dropped (PR #2694). This is a critical UX failure for anyone using Signal as a chat channel.
- **All users:** Transient API errors (5xx) and stale sessions cause confusing error messages instead of graceful retry (PRs #2184, #2692).
- **Self-hosters:** Running NanoClaw in containers (especially rootless Podman) may fail due to missing UID mapping (PR #2230).

**Satisfaction Signal:** The lack of new bug reports suggests the current release is stable for most users. The main friction is with edge cases around connectivity and container deployment.

---

### 8. Backlog Watch
**Long-unanswered Issues/PRs Needing Maintainer Attention:**

| Item | Age (days) | Type | Summary | Risk |
|------|------------|------|---------|------|
| PR #2184 | 35 | Fix | Stale session retry | User-visible error spam, low complexity fix |
| PR #2230 | 34 | Fix | Rootless Podman UID mapping | Blocks container users on modern Podman |
| PR #2208 | 34 | Feature | HTTP/SSE MCP transport | Large architectural addition, potential merge conflicts |
| PR #2349 | 29 | Fix | Mount allowlist path handling | Hardening fix for security/edge cases |
| PR #2531 | 19 | Fix | Duplicate text suppression | Annoying but non-critical UX glitch |

**Recommendation:** PR #2184 and PR #2694 are the most critical to merge first due to their direct impact on message delivery and user experience. The older infrastructure PRs (#2230, #2208) should be reviewed for mergeability or closed with guidance.

---

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-06-06**.

---

## NullClaw Project Digest – 2026-06-06

### 1. Today's Overview
The NullClaw project is currently in a **low-activity** state. Only a single Pull Request was updated in the last 24 hours, and there are zero closed issues or merged PRs. This indicates a period of slow progress or maintainer focus. However, the open PR represents an important new feature (provider integration) that has the potential to significantly expand the user base. With no new releases and no reported bugs, the project is stable but stagnant.

### 2. Releases
There are no new releases to report for this date. The latest stable release remains the previous version (none documented in the current data window).

### 3. Project Progress
- **Merged/Closed PRs today:** 0
- **Advanced Features:** No features were merged or fixed in the last 24 hours. The only activity is an open PR (see below).

### 4. Community Hot Topics
The sole active item is the most (and only) discussed topic today:

- **PR #947 (Open): feat(providers): add Evolink as an OpenAI-compatible provider**
  - **Author:** EvoLinkAI
  - **Link:** [PR #947](https://github.com/nullclaw/nullclaw/pull/947)
  - **Analysis:** This PR is submitted by the provider itself (EvoLinkAI), suggesting a **vendor-driven integration**. The underlying need is clear: users want access to a multi-model gateway (GPT-5, Gemini, DeepSeek, etc.) through a single, OpenAI-compatible endpoint. This would reduce the need for users to manage multiple API keys or configurations. The lack of community comments (0 👍) suggests limited awareness or testing so far, but the feature is strategically valuable for platform reach.

### 5. Bugs & Stability
**No bugs, crashes, or regressions were reported in the last 24 hours.** The project is currently stable with no known stability issues.

- **Severity:** None
- **Status:** No fix PRs required.

### 6. Feature Requests & Roadmap Signals
- **Active Feature Request (in review):** Adding **Evolink** as a provider (PR #947).
- **Prediction for next version:** Based on this PR, the next minor release will likely include **Expanded LLM Provider Support**. If merged, users will gain access to GPT-5, Gemini, DeepSeek, Doubao, and MiniMax models through a single endpoint. This is a clear roadmap signal that the project is moving toward becoming an **aggregator of multi-model gateways**, not just individual providers.

### 7. User Feedback Summary
- **Real Pain Points:** No direct user complaints were recorded today.
- **Use Cases:** The introduction of Evolink targets power users who need unified access to multiple cutting-edge models without managing separate subscriptions.
- **Satisfaction/Dissatisfaction:** Neutral. The absence of bug reports or support requests suggests current users are not experiencing friction, but the lack of activity also indicates low engagement or user growth.

### 8. Backlog Watch
**No long-unanswered issues or PRs** exist in the current data window. The total issue count is 0, meaning the backlog is clean. The single open PR (#947) is new (created yesterday) and does not yet require maintainer intervention beyond standard review.

- **Watched Items:** None.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-06

## Today's Overview

IronClaw continues its intense development cadence focused on the "Reborn" architecture overhaul. The project recorded 50 PRs updated in the last 24 hours (26 open, 24 merged/closed) and 12 issues updated (9 active, 3 closed). Activity remains concentrated on three fronts: the hook framework production activation (now fully merged), the ProductWorkflow architectural split into submit/read/subscribe doors (with PR #4506 merging), and Slack/WeCom channel support improvements. Nightly E2E tests continue to show instability (#4108), but the core development velocity is very high, with multiple XL-sized PRs advancing Reborn-state features.

## Releases

No new releases were published today. The last release cycle produced `ironclaw` v0.29.1 (per issue metadata) with breaking changes in `ironclaw_common` (0.4.2→0.5.0) and `ironclaw_skills` (0.3.0→0.4.0). The next release appears imminent—PR #3708 (open, 21 days old) is the release automation PR advancing toward a v0.29+ milestone.

## Project Progress

24 PRs were merged or closed today, representing substantial Reborn milestone progress:

- **Hook Framework Production Activation (Complete)**: The 4-PR hook activation series from zmanian fully merged: #3938 (HOOKS_ENABLED flag), #3936 (LibSqlPredicateStateBackend), #3937 (cross-backend parity suite), #3951 (third-party hook activation). These deliver the long-awaited hook execution framework behind a default-OFF flag.

- **CI Infrastructure Split**: PR #4513 (henrypark133, merged) splits legacy and Reborn CI scopes, adding a `Tests (Reborn)` workflow that triggers only on Reborn-scoped changes—addressing a pain point where every change triggered the full test matrix.

- **Architecture Simplification**: PR #4506 (danielwpz, open) splits `ProductWorkflow` into three effect-boundary doors (`submit_inbound`, `read_projection`, `subscribe_to_streams`), a prerequisite for OpenAI-compatible API wiring.

- **Approval Gate Refinements**: Two PRs from serrrfirat merged (#4386, #4390) extracting the approval-gating authorizer into reusable profile-aware boundaries, moving local-dev specific logic behind runtime profile policies.

- **Docs Accuracy**: PR #4302 (thisisjoshford, merged) reconciles all crate AGENTS.md maps to current Reborn code—a community contributor landing a docs-only fix.

## Community Hot Topics

**Issue #4311 — "Reborn model gateway collapses budget governance failures into context-overflow recovery"** (by henrypark133, 2 comments) — This architectural concern identifies a critical domain error: non-context budget governance failures (rate limits, cost caps) are being misclassified as context-overflow errors. This could mask real budget issues and complicate debugging. The issue remains open with high architectural impact.

**Issue #4502 — "WeCom group chat approval reply does not work"** (by sunglow666, 1 comment) — A concrete production blocker for WeCom channel users. Reply with `y`/`yes`/`always` to tool approval prompts is ignored, causing infinite approval loops. This is a functional regression in v0.29.1.

**Issue #4488 — "Split ProductWorkflow into explicit submit/read/subscribe doors"** (by danielwpz, 2 comments) — Parent of PR #4506. This architectural refactor blocks the OpenAI-compatible API roadmap (blocks #4459) and affects at least 7 related issues. It represents a foundational design decision being actively debated.

**PR #3708 — "chore: release"** (by ironclaw-ci[bot], 21 days open) — The release automation PR has been pending for three weeks. Its gating likely blocks the rollout of the hook framework and other Reborn features to production.

## Bugs & Stability

| Severity | Issue | Description | Status |
|----------|-------|-------------|--------|
| Critical | #4502 | WeCom group chat approval reply not working—infinite loop | Open, no fix PR |
| High | #4108 | Nightly E2E schema/sandbox failures persist (10 days) | Open, recurring |
| High | #4512 | Concurrent sandbox `job_semaphore` never acquired—dead code | Open, likely latent bug |
| Medium | #4500 | Channel onboarding written to wrong conversation (WeCom + Telegram) | Open |
| Medium | #4191 | WeCom channel validation: multiple issues found (staging) | Open |
| Low | #4505 | WeCom group title not distinguishable in Web UI sidebar | Open |

The nightly E2E failure (#4108) is concerning—it has been failing since May 27 with schema-related errors and no fix PR identified. The sandbox semaphore bug (#4512, reported today) is a latent concurrency issue where a synchronization primitive is never acquired, meaning it provides no actual protection.

## Feature Requests & Roadmap Signals

Several features appear to be targeting the **next minor release** (v0.30+):

1. **OpenAI-Compatible API** (PR #4459) — A new `ironclaw_reborn_openai_compat` crate for Chat Completions/Responses API ingress. This work is blocked on #4488 architecture decisions but would enable external LLM routing.

2. **Slack Channel Routing** (PRs #4510, #4509, both open) — Adds dynamic product-workflow channel route stores and subject routing. This would allow the Reborn Slack host to route messages by channel ID rather than installation-level fallback.

3. **Reborn CLI Docker Image** (PR #4504, open) — Adds a dedicated Dockerfile for standalone Reborn WebUI/Slack service with Railway PORT support.

4. **Slack AI Streaming** (Issue #4491) — Requests proper streaming for Slack responses rather than the current "thinking..." placeholder approach.

5. **IronHub Port to Reborn** (PR #4479, open) — Signed catalog with Ed25519 verification, artifact downloads, and sha256 checks for third-party skills/tools.

## User Feedback Summary

**Primary Pain Points (via sunglow666's WeCom validation, #4191):**
- Group/private DM conversations merge incorrectly (fixed in #4194, closed today)
- Approval flow broken in group chat (#4502, critical)
- Unpaired user visibility unclear (#4198, closed)
- Onboarding events written to wrong conversations (#4500)
- Indistinguishable group titles in sidebar (#4505)

**User Workflow Satisfaction:**
- ✅ Core text messaging, pairing/reconnect, markdown/emoji/multilingual support working well
- ❌ Approval interaction flow unreliable in production
- ❌ Channel onboarding UX confusing (wrong conversation destination)

The WeCom validation issues come from a single power user (sunglow666) deeply testing v0.29.1 staging, suggesting focused enterprise WeChat support development.

## Backlog Watch

| Item | Age | Status | Concern |
|------|-----|--------|---------|
| #4108 — Nightly E2E failure | 10 days | Open, no fix | CI health; if unresolved, blocks reliable testing |
| #3708 — Release automation PR | 21 days | Open | Gating the next release; all features pending this |
| #4002 — Dependabot actions upgrade (16 updates) | 13 days | Open | Growing security risk; multiple GitHub Action version jumps (checkout 4.3→6.0, etc.) |
| #4191 — WeCom staging validation findings | 9 days | Open | Multiple known bugs from user testing without all fixes deployed |
| #4311 — Budget governance error misclassification | 5 days | Open | Architectural bug affecting error handling across all LLM interactions |

**Maintainer attention needed:**
- The release automation (#3708) has been stalled for three weeks—its completion would unblock critical user-facing features.
- The nightly E2E failure (#4108) has no associated fix PR despite being open since May 27. This should be a priority for CI health.
- The Dependabot PR (#4002) updates GitHub Actions from early 2024 to mid-2026 versions—not merging this risks accumulating security CVEs in the CI pipeline.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-06-06**, generated from the provided GitHub data.

---

# LobsterAI Project Digest – 2026-06-06

## 1. Today's Overview
LobsterAI shows a high level of **maintenance and feature velocity** today, with 9 PRs merged/closed and a new point release (2026.6.5) published. The project is actively refining the **cowork** and **artifacts** experiences, while also improving platform-specific stability (macOS microphone permissions, Windows update scripts). The issue queue remains static with 5 open items, all stale and lacking recent maintainer responses, indicating a potential backlog in user-facing bug triage. Overall, the project appears healthy with a strong commit rhythm, though community-reported bugs are aging without resolution.

## 2. Releases
**New Release: [LobsterAI 2026.6.5](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.5)** (June 5, 2026)
- **Key Changes:**
  - `feat(cowork): improve channel session sync and cleanup` – Enhances session state management for the cowork feature.
  - `feat(shortcuts): overhaul keyboard shortcuts with expanded actions and improved UX` – A major rework of the shortcut system, likely adding new actions and better usability.
- **Breaking Changes:** None explicitly noted.
- **Migration Notes:** No specific migration steps required.

## 3. Project Progress (Merged/Closed PRs Today)
All 9 PRs updated in the last 24h were **merged or closed**. The majority came from the **2026.6.4 release cycle** (June 5), with one PR [#1529](https://github.com/netease-youdao/LobsterAI/pull/1529) and [#1530](https://github.com/netease-youdao/LobsterAI/pull/1530) from April finally being closed (likely as part of a cleanup).

**Key Feature Advances (from release 2026.6.4):**
- **Cowork & UX:** Added authenticated voice input (ASR) ([PR#2119](https://github.com/netease-youdao/LobsterAI/pull/2119)), improved clipboard copy fallback chain ([PR#2118](https://github.com/netease-youdao/LobsterAI/pull/2118)), and enhanced error UX with free-quota warnings and empty-state guides ([PR#2116](https://github.com/netease-youdao/LobsterAI/pull/2116)).
- **IM Reliability:** Fixed IM reply assembly to only use current-turn messages ([PR#2115](https://github.com/netease-youdao/LobsterAI/pull/2115)).
- **Artifacts:** Enhanced file previews, expanded panel UX, and fixed Office/PDF zoom issues ([PR#2114](https://github.com/netease-youdao/LobsterAI/pull/2114)).
- **Platform/Stability:** Added macOS microphone permission request ([PR#2113](https://github.com/netease-youdao/LobsterAI/pull/2113)); preserved user-deleted provider models after migration ([PR#2117](https://github.com/netease-youdao/LobsterAI/pull/2117)).
- **Scheduled Tasks:** Added agent selection when creating scheduled tasks in multi-agent setups ([PR#1530](https://github.com/netease-youdao/LobsterAI/pull/1530)).
- **Batch Export:** Added export-to-JSON feature for selected cowork sessions ([PR#1529](https://github.com/netease-youdao/LobsterAI/pull/1529)).

## 4. Community Hot Topics
- **Issue #1495 – "无缘无故中断进程" (Unexpected process interruption)**  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1495) | 👍: 1 | Comments: 1  
  User reports recurring process crashes with no clear trigger. This is the highest-reacted issue today and suggests a potential stability concern that may be linked to model timeouts or resource exhaustion. No maintainer response yet.

- **Issue #1496 – "任务显示完成，但是没有返回" (Task shows complete but no return)**  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1496) | Comments: 2  
  A user reports a specific UI bug where tasks appear completed but produce no output. This could be a session cache or streaming bug related to the cowork feature.

- **Issue #1468, #1469, #1470 – Batch of "Unsaved changes" UX bugs**  
  [Links](https://github.com/netease-youdao/LobsterAI/issues/1468) | Comments: 1 each  
  Three related issues filed by the same user (MaoQianTu) highlight a systemic UX gap: Agent creation modals, settings panels, and MCP server config modals all lack unsaved-change confirmation dialogs. This is a significant quality-of-life concern for power users.

## 5. Bugs & Stability
- **Medium Severity:** *Unexpected process interruption* ([#1495](https://github.com/netease-youdao/LobsterAI/issues/1495)) – User reports spontaneous crashes. No fix PR identified.
- **Medium Severity:** *Task completion without return* ([#1496](https://github.com/netease-youdao/LobsterAI/issues/1496)) – Could be a session/streaming bug. No fix PR identified.
- **Low-Medium (UX) Severity:** *Data loss on modal close* ([#1468](https://github.com/netease-youdao/LobsterAI/issues/1468), [#1469](https://github.com/netease-youdao/LobsterAI/issues/1469), [#1470](https://github.com/netease-youdao/LobsterAI/issues/1470)) – Three related bugs showing silent data loss when closing forms. No fix PRs identified. These were filed in April and remain unaddressed.

## 6. Feature Requests & Roadmap Signals
- **Multi-Agent Task Assignment** – The merge of PR [#1530](https://github.com/netease-youdao/LobsterAI/pull/1530) (scheduled task agent selection) suggests the team is investing in **multi-agent workflow orchestration**. This may be a precursor to broader multi-agent management features.
- **Batch Data Portability** – PR [#1529](https://github.com/netease-youdao/LobsterAI/pull/1529) (batch session export to JSON) indicates a growing need for **data export/portability** from the cowork feature. Future versions may add import functionality or extended export formats.
- **Voice Input (ASR) Maturation** – The authenticated ASR voice input merged in 2026.6.4 ([PR#2119](https://github.com/netease-youdao/LobsterAI/pull/2119)) signals a push toward voice-first interaction in cowork. Expect further refinements to voice UX and platform permission handling.

## 7. User Feedback Summary
- **Pain Points:**
  - Recurring crashes and task completion failures (issues #1495, #1496) are causing frustration and workflow interruptions.
  - Silent data loss when editing agents, settings, or MCP configurations is a repeated complaint, highlighting a **critical UX miss** in modal design.
- **Use Cases:**
  - Users are heavily utilizing the **cowork** and **scheduled task** features, with demand for agent-specific management.
  - Power users (e.g., MaoQianTu) are systematically testing edge cases, indicating deep engagement with the tool.
- **Satisfaction/Dissatisfaction:**
  - No explicit positive feedback in this snapshot. The community appears engaged but is **waiting for maintainer responses** on stale, high-impact bugs.

## 8. Backlog Watch
The following items are **stale** (created April 4-7) with no recent maintainer activity and should be prioritized:

1. **[Issue #1468](https://github.com/netease-youdao/LobsterAI/issues/1468)** – Agent create modal data loss (2 months stale)
2. **[Issue #1469](https://github.com/netease-youdao/LobsterAI/issues/1469)** – Agent settings panel data loss (2 months stale)
3. **[Issue #1470](https://github.com/netease-youdao/LobsterAI/issues/1470)** – MCP server config modal data loss (2 months stale)
4. **[Issue #1495](https://github.com/netease-youdao/LobsterAI/issues/1495)** – Unexpected process interruption (2 months stale, highest reaction)
5. **[Issue #1496](https://github.com/netease-youdao/LobsterAI/issues/1496)** – Task completed but no output (2 months stale)

These issues represent **the longest-unaddressed user pain points** and are likely eroding user trust. A maintainer response or fix commit for any of these would significantly improve project health perception.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-06

## Today's Overview
The project shows moderate activity with 4 issues and 5 PRs updated in the last 24 hours. Three new bug reports and one feature request were filed, all by the same contributor (IlyaBizyaev), indicating active community engagement. One critical bug regarding Telegram streaming was fixed and merged. No new releases were published today. Overall project health appears stable, with the maintainer team responding promptly to bug reports.

## Releases
No new releases were published today. The latest available version remains unchanged.

## Project Progress
One pull request was merged today:
- **[PR #1099] Separate Telegram progress stream from final replies** (closed/merged) – Fixes issue #1097 where Telegram edit-in-place streaming incorrectly mixed intermediate progress output into the final reply. The solution treats streaming updates as temporary progress messages, deletes them upon completion, and delivers the final reply separately.

Three new open PRs were submitted:
- **PR #1106** – Adds opt-in Podman sandbox escape hatches for host socket passthrough and privileged nested Podman, plus improved rootless Podman diagnostics.
- **PR #1105** – Fixes Docker sandbox filesystem tool fallback when the gateway process cannot access host mounts.
- **PR #1104** – Allows replacing preferred models in provider configurations, including clearing all preferences with an empty selection.

One earlier PR remains open and under review:
- **PR #1089** – Caps persisted tool results before session history rehydration.

## Community Hot Topics
The most active item by comments is the now-closed bug report:
- **[Issue #1097] Telegram edit-in-place streaming mixes intermediate output into final reply** (1 comment, now closed) – This bug was resolved by PR #1099, demonstrating responsive maintainer engagement with reported issues. [GitHub Link](https://github.com/moltis-org/moltis/issues/1097)

All other issues and PRs currently have 0 comments and 0 reactions, suggesting either early-stage review or lower community engagement on these topics.

## Bugs & Stability
Three bug reports were filed today (all by IlyaBizyaev), ranked by potential impact:

**Medium Severity:**
- **[Issue #1109] Update banner does not account for Docker installs** – Docker users may see incorrect update notifications or miss updates entirely. No fix PR yet. [GitHub Link](https://github.com/moltis-org/moltis/issues/1109)

**Low Severity:**
- **[Issue #1108] Session list in web UI shows times but not dates for past-day sessions** – Annoying but non-critical UI limitation affecting session navigation. No fix PR yet. [GitHub Link](https://github.com/moltis-org/moltis/issues/1108)

**Previously Reported (now fixed):**
- **[Issue #1097] Telegram streaming bug** – Resolved by PR #1099, which was merged today.

Two sandbox-related PRs (#1105 and #1106) address potential stability issues in Docker and Podman environments, though no related bugs were reported today.

## Feature Requests & Roadmap Signals
One feature request was filed today:
- **[Issue #1107] Multiline text input in mobile web UI** – User requests proper multiline support for chat input on mobile devices, likely to improve usability for typing longer messages. [GitHub Link](https://github.com/moltis-org/moltis/issues/1107)

Given the focused nature of this request and its relatively low implementation complexity, this feature could appear in the next minor release if prioritized.

Additionally, PR #1104 (preferred model management) and PR #1106 (Podman support) suggest ongoing infrastructure improvements that may be part of the upcoming roadmap.

## User Feedback Summary
- **User IlyaBizyaev** provided three reports today, indicating active use of both Docker deployment and web UI. The reports suggest:
  - Positive: User is actively using the latest version and filing structured bug reports with preflight checklists.
  - Pain points: Docker installation experience (update banner issue), web UI session history usability, and mobile input limitations.
  - No negative sentiment or dissatisfaction expressed.

- **User s-salamatov** contributed both the Telegram bug report and its fix, demonstrating developer-user engagement with the platform.

## Backlog Watch
No critical long-unanswered issues were identified today. All open issues are less than 2 days old:
- Issues #1107, #1108, #1109 were created on 2026-06-05.
- PRs #1104, #1105, #1106 were created or updated on 2026-06-05.
- PR #1089 (2026-06-01) remains open with no comments, awaiting maintainer review or community discussion. This PR caps persisted tool results on rehydration and may require attention.

**Recommendation:** PR #1089 should be reviewed in the coming days to avoid accumulating review debt.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the project digest for **CoPaw** based on data from **2026-06-06**.

---

## CoPaw Project Digest – 2026-06-06

### 1. Today’s Overview
CoPaw is showing **high community engagement**, with **17 issues** and **12 PRs** updated in the last 24 hours. Activity is heavily concentrated on **bug fixes and infrastructure** for the Yuanbao channel (protobuf/streaming issues) and **UI/UX enhancements** for the Console frontend. The project is in a **stable maintenance and polish phase**, with no new releases today, but a significant number of fix PRs are actively being merged or reviewed. The `main` branch is seeing a healthy cadence of contributions from first-time contributors, indicating a welcoming contribution environment.

### 2. Releases
**No new releases** were detected in the last 24 hours. The latest reported version in issues is **v1.1.10**.

### 3. Project Progress
Several PRs were **merged or closed** today, indicating active development:

- **PR #4972 (Merged):** Enabled LaTeX math formula rendering in Markdown. This fixes issue #4756, adding support for scientific/technical users.
- **PR #4026 (Merged):** Implemented a security feature (`WriteFileOverwriteGuardian`) to prevent `write_file` from silently overwriting non-empty files.
- **PR #4765 (Merged):** UI polish: Centered the shield icon and adjusted column widths in the security rule table.
- **PR #4766 (Merged):** Fixed a scrollbar flickering bug on hover in the Environment Variables page.

### 4. Community Hot Topics
The most active discussions reflect **core user frustrations with default settings and configuration complexity**:

- **Issue #4937 (Bug, 5 comments):** The `/compact` command ignores the user-configured model `max_input_length` and defaults to 128K. *Link: [Issue #4937](https://github.com/agentscope-ai/QwenPaw/issues/4937)*
- **Issue #4770 (Feature Request, 5 comments):** Users want to reorder columns in the left session panel to move "update time" to a visible position. *Link: [Issue #4770](https://github.com/agentscope-ai/QwenPaw/issues/4770)*
- **Issue #4705 (Bug, 4 comments):** Mission Mode Phase 2 gets stuck in an infinite loop, even after the agent explicitly requests user input, causing excessive token usage. *Link: [Issue #4705](https://github.com/agentscope-ai/QwenPaw/issues/4705)*

**Underlying Need:** Users are asking for **more intuitive defaults and better control** over workflows (session management, model compression, task automation). The pattern suggests users want the tool to "get out of the way" and match their specific hardware and workflow constraints.

### 5. Bugs & Stability
Multiple bugs were reported and fix PRs were opened in parallel, showing a **strong triage-to-fix pipeline**:

**High Severity:**
- **Yuanbao Channel Bugs (Issues #4976-#4980):** A cluster of 5 issues filed by the same user reveals a **fragile integration with the Yuanbao channel**: missing proto files in the pip wheel, protobuf version incompatibility, missing `connectId` field, streaming replies being dropped, and `SendC2CMessage` failing. *Links: [4976](https://github.com/agentscope-ai/QwenPaw/issues/4976), [4978](https://github.com/agentscope-ai/QwenPaw/issues/4978), [4979](https://github.com/agentscope-ai/QwenPaw/issues/4979), [4980](https://github.com/agentscope-ai/QwenPaw/issues/4980)*
    - **Fix PRs already open:** PR #4983 (connectId), PR #4982 (streaming fix).
- **Issue #4962:** DeepSeek API replies are being incorrectly folded into the "thinking" bubble, requiring user expansion to see the final answer.
- **Issue #4832:** Windows `cmd.exe` window flashes when executing shell commands, creating a poor desktop UX.

**Medium/Low:**
- **Issue #4661 (Closed):** Context compression defaults not persisting after upgrade from v1.1.7 → v1.1.8post1.
- **Issue #4960:** Users cannot access the console from mobile browsers on the same LAN, even after adding host whitelist rules.

### 6. Feature Requests & Roadmap Signals
Clear user demand is emerging for **better session management and visual identification**:

- **Session Management (#4971):** A dedicated session sidebar for one-click switching (instead of two clicks). This is the most concrete, repeated request.
- **Agent Avatars (#4974):** Support for uploading or URL-based avatars per agent, displayed in management lists and chat windows. Predicts a "persona polish" push.
- **Cron Script Execution (#4963):** Ability to run raw shell scripts in cron tasks without routing through the AI agent. Signals a shift toward treating CoPaw as a **home-automation orchestration hub** rather than just a chat interface.

**Roadmap Prediction:** The next version (v1.1.11) is likely to focus on **Yuanbao channel reliability** (fixing the current cluster of bugs) and **UI customization** (reorderable session columns, agent avatars).

### 7. User Feedback Summary
- **Satisfaction:** International and Chinese-language users are actively contributing first-time PRs (e.g., #4973, #4975, #4765), indicating a healthy, trusting community.
- **Pain Points:**
    - **Configuration Complexity:** Model context compression config is described as confusing and "not taking effect" (#4661, #4937).
    - **New User Onboarding:** Questions about packaging methods (#4754) and LAN access (#4960) suggest documentation gaps for local/extended deployment.
    - **Desktop Experience:** The Windows cmd flash (#4832) and session switching friction (#4971) degrade the daily user experience.
- **Use Cases:** Users are deploying CoPaw for **mission-driven automation** (Phase 2 loops, cron tasks) and **multi-protocol messaging** (Feishu, Yuanbao, Web Console).

### 8. Backlog Watch
No critical long-standing issues were identified in this snapshot. However, the following items may require maintainer attention:

- **Issue #4744 (Open, 2 comments):** Question about macOS Tauri support for Intel chips. Unanswered for 9 days. *Link: [Issue #4744](https://github.com/agentscope-ai/QwenPaw/issues/4744)*
- **Issue #4832 (Open, 2 comments):** The Windows `cmd.exe` flash bug has a clear root cause identified by the user, but no PR is open yet.
- **PR #4900 (Open):** Decouples plugin loader from agent startup but has had no recent comments. This may be a blocker for Tauri/PyInstaller frozen builds and could benefit from a maintainer review.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-06-06

## 1. Today's Overview

The ZeptoClaw project shows focused, maintenance-heavy activity with two binary-size related issues and one open PR spanning the last six days. No new releases were made today, and the open PR #611 has been under review since June 1, indicating deliberate progress on CI infrastructure. The project is actively tightening its binary-size gates, moving from post-mortem checks toward PR-blocking enforcement. The community engagement remains low (0 reactions, minimal comments), suggesting a single maintainer or small team operating at a measured pace. Overall health appears stable, with strategic attention on cross-platform binary size optimization for edge/robot deployment targets.

## 2. Releases

- **No new releases as of 2026-06-06.**

## 3. Project Progress

- **No PRs were merged or closed today.** The only open PR is:
  - **#611 [OPEN] – chore(ci): promote binary-size to PR gate at 7.5MB**  
    *(Created: 2026-06-01, Updated: 2026-06-06)*  
    [GitHub Link](https://github.com/qhkm/zeptoclaw/pull/611)  
    **Summary:** This PR turns the existing `binary-size` job (which measures stripped release binaries) into a PR-time gate—removing the `if:` guard so it runs on every PR, and lowering the threshold from 11MB (current x86_64 size) to 7.5MB. It is directly related to the active issue #629, which argues for a stricter 7MB aarch64 gate.

## 4. Community Hot Topics

**Most Active Issues:**

1. **#612 [CLOSED] – chore(perf): audit ~800KB binary-size drift since 6.2MB low water mark, tighten gate to 7MB**  
   *(1 comment, updated today)*  
   [GitHub Link](https://github.com/qhkm/zeptoclaw/issues/612)  
   **Analysis:** This issue tracks the binary-size regression from a previously recorded 6.2MB low-water mark to the current 6.98MB. The underlying need is maintaining the "6MB fits on a robot" strategic moat—driving the project to audit bloat and set a hard 7MB gate for aarch64 targets.

2. **#629 [OPEN] – chore(ci): add aarch64 binary-size gate at 7MB (the actual robot moat)**  
   *(0 comments, created today)*  
   [GitHub Link](https://github.com/qhkm/zeptoclaw/issues/629)  
   **Analysis:** This issue explicitly calls out that the 11MB x86_64 gate from PR #611 is not the "strategic moat"—the true target is aarch64 at 7MB. It reflects a clear prioritization of embedded/edge deployment (Pi, Jetson, Apple Silicon) over desktop x86_64.

**Observation:** Both issues and the open PR form a single coherent effort to tighten binary-size enforcement. Zero user reactions/comments suggest this is a maintainer-driven optimization, not user-requested.

## 5. Bugs & Stability

- **No bugs, crashes, or regressions reported today.**  
  The project is in a proactive optimization phase (binary size), not a reactive bug-fixing phase.

## 6. Feature Requests & Roadmap Signals

**User-Requested Features:** None detected in today's data.

**Roadmap Signals (from Issues/PRs):**
- **Binary-size gate enforcement for aarch64 at 7MB** (Issue #629) — likely the next PR after #611 lands.
- **Binary-size regression audit** (Issue #612, closed) — suggests the 800KB drift has been addressed or acknowledged.
- **Prediction:** Next minor version will likely include:
  - PR-time binary-size gate for both x86_64 (11MB) and aarch64 (7MB)
  - Potential code changes to reduce binary size below 7MB for aarch64 targets

## 7. User Feedback Summary

- **No user feedback or pain points expressed in today's data.**  
  The issues and PR are purely maintainer-authored (`qhkm`), with zero external contributors or reactions. This suggests either an early-stage project, or a small/private team with limited community engagement.

## 8. Backlog Watch

**Items Needing Maintainer Attention:**

- **PR #611 [OPEN] – chore(ci): promote binary-size to PR gate at 7.5MB**  
  *(No activity since 2026-06-01; updated only today)*  
  [GitHub Link](https://github.com/qhkm/zeptoclaw/pull/611)  
  **Status:** The PR has been open for 5 days without review/merge. Issue #629 directly contradicts its threshold (7.5MB vs 7MB), which may explain the delay—maintainers may be aligning on the correct aarch64 gate.

**Takeaway:** The remaining open issue (#629) and open PR (#611) are in direct tension over the binary-size threshold. Resolution likely requires either amending PR #611 or merging it as-is and following up with Issue #629 in a subsequent PR. No stale items (uncommented >30 days) were identified.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for **2026-06-06**.

---

## ZeroClaw Project Digest — 2026-06-06

### 1. Today's Overview
The project is in an **intense development cycle** with extremely high community engagement. Over the last 24 hours, **50 Issues and 50 PRs** were updated, indicating a project operating at scale. There is a clear focus on **security, observability, and multi-agent architecture**, driven by several ambitious RFCs and tracking issues. The closing rate (7 Issues, 4 PRs) suggests that maintainers are actively processing work, but the large number of open items (43 Issues, 46 PRs) points to a significant backlog that is being addressed methodically, primarily through governance-oriented RFCs.

### 2. Releases
**No new releases** in the last 24 hours. The last official milestone referenced is **v0.9.0**, with several high-priority tracking issues (like OIDC Authentication and pluggable security providers) targeting that version.

### 3. Project Progress
**4 PRs were merged/closed today (2026-06-06):**
- **`PR #7283`**: Merged "two-level pane cursor, agent-picker mouse, registry-driven config help" for the `zerocode` TUI—improving navigation and user experience.
- **Bugs Fixed**: Two significant bug-fix PRs landed:
  - `PR #7245`: Fixed a critical runtime bug where `read_skill` could not load **plugin-bundled** or **bounded** skills.
  - `PR #7238`: Fixed a channel logic error where `strip_old_tool_context` was trimming context at the wrong boundary, potentially losing data from new sessions.
- **Infrastructure**: `PR #7176` was updated, focusing on container build pipeline improvements (musl static linking) to make the StageX build more reliable.

### 4. Community Hot Topics
The community is deeply engaged in high-level architectural decisions and advanced feature planning.

- **#6808: RFC: Work Lanes & Board Automation** (9 comments) — A governance RFC aiming to simplify maintainer workflows through automated PR routing. This signals a maturing project that is scaling its contributor base and needs process efficiency.
- **#6969: RFC: Unified Output Routing Model** (7 comments) — The most popular user-facing feature request. A recent migrant from Letta is driving a conversation about "per-peer modality preference" (controlling how/where replies go, e.g., morning briefings). This addresses a clear gap between ZeroClaw's current functionality and user expectations from other agent systems.
- **#5601: OAuth for Multiple Chinese Providers** (6 comments, 1 👍) — A feature request for native login support for Ollama Cloud, Zhipu, Moonshot, and MiniMax. This indicates a strong **Asian market user base** seeking friction-free authentication.
- **#7141: OIDC Authentication Provider Support** (4 comments) — A high-priority (P1) tracking issue for v0.9.0. This is linked to enterprise security requirements and is likely the most "saleable" feature in the current roadmap.

### 5. Bugs & Stability
Two new bug-fix PRs were merged today, but the focus remains on **systemic stability** via new mechanisms rather than firefighting.

- **High-Risk Bugs (with fixes):**
    - **`PR #7245`** (fixes `read_skill`): A bug causing plugin-bundled skills to be invisible during execution. Severity: High. **Fix: Merged.**
    - **`PR #7238`** (fixes channel context trimming): A logic error that could strip tool context from short sessions. Severity: Medium/High. **Fix: Merged.**
- **Open & Unresolved (High Severity):**
    - **#7059 (P1):** A bug tracking the "default provider" credential fallback in the channel orchestrator, which conflicts with the new V3 schema. This is being actively worked.
    - **#6074 (P2):** A long-running audit to recover **153 commits** that were lost in a bulk revert. This is a significant data recovery effort that has been in progress for over a month.
- **Security Incidents:** No crashes or data-loss bugs reported today, but the project is proactively building defenses against them via several RFCs (air-gap mode, shell command confirmation, process memory limits).

### 6. Feature Requests & Roadmap Signals
The roadmap for **v0.9.0** is clearly crystallizing around **Security & Architecture**.

- **Lock for v0.9.0:**
    - **OIDC Auth (#7141):** Pluggable enterprise authentication.
    - **Pluggable Security Provider (#7142):** Exposing the security enforcement layer behind a trait.
    - **Air-Gapped Mode (#6293):** Running the agent offline with a companion daemon.
- **Strong Candidates for Next Release (v0.10?):**
    - **A2A Agent Discovery (#7218):** Defining a `/.well-known/agent-card.json` for multi-agent interoperability.
    - **Per-Model Capability Config (#7100):** Allowing users to set `vision` and `context_window` per model, enabling better UI and context budgeting.
    - **Unified Output Routing (#6969):** The "Letta-like" per-channel modality preference, which is a high priority (P2).
- **Ecosystem Growth:**
    - A massive batch of **new WASM plugins** was proposed today (Mistral OCR, AssemblyAI, Deepgram, OCR.space, Recraft, Ideogram, Stability, ElevenLabs) via PRs #7288-#7296. These are "Tier B" plugins, indicating a push to make ZeroClaw a **universal media-processing agent**.

### 7. User Feedback Summary
User sentiment is a mix of **high enthusiasm for the vision** and **friction from breaking changes/complexity**.

- **Pain Points:**
    - **Loss of legacy behavior (#6969):** A user migrating from Letta explicitly stated a feature they relied on ("output routing") is "gone." This is a common theme for users of competing agent frameworks.
    - **Configuration confusion:** Users are struggling with provider setup (`#6120` - OpenAI Codex prompts for wrong key) and config validation (`#6416` - quickstart should warn about incompatibilities).
    - **Windows experience (#7089):** A user is frustrated with `cmd.exe` as the default shell host on Windows, suggesting the project is still maturing its cross-platform support.
- **Satisfaction:**
    - The rapid influx of new plugin PRs (from the same contributor) suggests the WASM plugin system is well-received and easy to target.
    - The RFC process (#6808) shows a community that is engaged and wants to help shape the project's direction, a sign of a healthy open-source ecosystem.

### 8. Backlog Watch
Several important items remain stale or blocked, requiring maintainer intervention:

- **#5601 (P2, blocked):** OAuth support for Chinese providers. Blocked for nearly 2 months. This is a community blocker for a significant user segment.
- **#6715 (P3, blocked):** Cleaning up 200+ stale branches. A simple housekeeping task that hasn't been addressed in 3 weeks.
- **#6293 (P2, blocked):** The Air-gapped execution mode RFC. Blocked for over a month. This is a key architectural feature of the v0.9.0 vision.
- **#6279 (P2, blocked):** Improving release triage criteria. Blocked for a month, despite being a process improvement that could accelerate releases.
- **#5842 (P2, stale):** Evaluating `extra_args` validation for security-affecting CLI flags. This has been sitting open for over a month with no activity, despite being a security concern.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*