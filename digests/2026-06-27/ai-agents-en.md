# OpenClaw Ecosystem Digest 2026-06-27

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-27 01:56 UTC

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

# OpenClaw Project Digest — 2026-06-27

## Today's Overview

OpenClaw is experiencing **extremely high activity**, with 500 issues and 500 PRs updated in the last 24 hours. The project maintains a large open issue backlog (473 open vs. 27 closed) and a significant open PR queue (448 open vs. 52 merged/closed). Development velocity is strong, with numerous fix PRs targeting stability, security, and provider compatibility. The project’s maintainer team is actively reviewing and merging contributions, though many issues carry `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision` labels, indicating a **growing bottleneck in triage and product decisions**. No new releases were published today.

## Releases

**None** — no new releases were published on 2026-06-27.

## Project Progress

### Merged/Closed PRs Today (52 total)

Notable closed PRs include:
- **#97128** *(closed)* — `fix(opencode-go): re-arm idle timer on block-boundary events to prevent false stalled-stream abort` — Addresses a streaming watchdog false-positive in the opencode-go provider.
- **#68936** *(closed)* — `Autofix: add PR review autofix pipeline + Windows daemon` — Adds automated PR review response pipeline and Windows background daemon.
- **#90184** *(closed)* — `fix(ui): rename chat sessions from the picker` — Adds inline session rename capability in the web UI sidebar.
- **#96004** *(closed)* — `fix(proxy): apply enhanced NO_PROXY matching to global undici dispatcher` — Fixes proxy bypass for internal plugin requests.

### Key Open PRs Advancing Today

- **#97140** — `fix(agent-core): ignore truncated tool calls` — Prevents partial/incomplete tool calls from executing when a model response is interrupted. Ready for maintainer review.
- **#97139** — `fix(openai-responses): bound SSE response reads via buildGuardedModelFetch` — Adds byte caps on OpenAI SSE streaming to prevent OOM. Ready for maintainer review.
- **#96883** — `Scope agent cron operations to the calling agent` — Security fix limiting cron tool access to the calling agent’s own jobs. Ready for maintainer review.
- **#97086** — `feat(mxc): add Windows MXC sandbox backend` — Adds Microsoft eXecution Container support for Windows sandboxing. Waiting on author.

## Community Hot Topics

### Most Active Issues

| Issue | Title | Comments | Reactions | Status |
|-------|-------|----------|-----------|--------|
| [#75](https://openclaw/openclaw/issue/75) | Linux/Windows Clawdbot Apps | **109** | 👍 **81** | Open, P2, needs product decision |
| [#9443](https://openclaw/openclaw/issue/9443) | Request: Prebuilt Android APK releases | 25 | 👍 2 | Open, P2 |
| [#77598](https://openclaw/openclaw/issue/77598) | Track live dev agent behavior and trajectory | 22 | 👍 1 | Open, P2, live observation |
| [#86538](https://openclaw/openclaw/issue/86538) | Session write-lock timeouts block subagent lanes | 16 | 👍 1 | Open, P1, linked PR |
| [#12602](https://openclaw/openclaw/issue/12602) | Slack Block Kit support for agent messages | 13 | — | Open, P2 |

### Analysis

The **most impactful community need** is **cross-platform client support**. Issue #75 (Linux/Windows Clawdbot Apps) has 109 comments and 81 reactions — the community urgently wants desktop clients beyond macOS/iOS/Android. This is a **major adoption barrier** for enterprise and Windows/Linux users.

**Subagent reliability** is the second major theme. Issues #86538, #75593, #77642, and #78055 all document subagent delivery failures, stale completions, and session state corruption — indicating **fundamental architectural pressure** in the subagent lifecycle system. The community’s reliance on multi-agent workflows is outpacing current stability guarantees.

## Bugs & Stability

### Critical (P1, Platinum/Diamond severity)

| Issue | Title | Impact | Fix Status |
|-------|-------|--------|------------|
| [#94228](https://openclaw/openclaw/issue/94228) | Native Anthropic: replaying `thinking` blocks bricks long tool-use threads | Session state, message loss, auth provider | Needs live repro |
| [#86538](https://openclaw/openclaw/issue/86538) | Session write-lock timeouts block subagent delivery lanes | Session state, message loss | **Linked PR open** |
| [#76042](https://openclaw/openclaw/issue/76042) | Clean install impossible since 2026.5.xx | Auth provider, crash loop | Needs maintainer review |
| [#77642](https://openclaw/openclaw/issue/77642) | [5.3 regression] Duplicate answers + "missing tool result" errors | Session state, message loss | Needs live repro |
| [#74484](https://openclaw/openclaw/issue/74484) | Gateway pairing scope deadlock | Security, auth provider | Needs live repro |
| [#74586](https://openclaw/openclaw/issue/74586) | AM embedded run aborts memory_search tool calls | Session state, auth provider | Needs live repro |
| [#76038](https://openclaw/openclaw/issue/76038) | Stuck Session Recovery double failure + slow preprocessing | Session state, crash loop | Needs live repro |

### High (P1-P2, Diamond)

| Issue | Title | Impact | Fix Status |
|-------|-------|--------|------------|
| [#75593](https://openclaw/openclaw/issue/75593) | Subagents list empty after spawn | Session state | **Linked PR open** |
| [#77930](https://openclaw/openclaw/issue/77930) | Discord channel not loaded (regression in 2026.5.4) | Message loss | **Linked PR open** |
| [#78055](https://openclaw/openclaw/issue/78055) | Subagent announce delivers stale output, inherits unrelated history | Session state, message loss | Needs maintainer review |
| [#77733](https://openclaw/openclaw/issue/77733) | Bare `/new`/`/reset` no longer triggers persona greeting | Session state, message loss | **Linked PR open** |
| [#75380](https://openclaw/openclaw/issue/75380) | `provider-payload.jsonl` and `cache-trace.jsonl` grow unbounded | Security, crash loop | **Linked PR open** |
| [#76171](https://openclaw/openclaw/issue/76171) | Stale worker process accumulation degrades responses | Crash loop | Needs maintainer review |
| [#43996](https://openclaw/openclaw/issue/43996) | Sandbox container exits immediately with no-new-privileges | Security, crash loop | Needs product decision |

### Regressions

Several regressions were introduced in version 2026.5.x, with **#77642, #77930, #77733, and #76042** all explicitly flagged as regressions. The main affected areas are:
- **Discord channel loading** (broken in beta.2/beta.3, fixed in beta.1)
- **Persona greeting on session reset** (broken since 5.3)
- **Duplicate answers and missing tool results** (since 5.2)
- **Clean installation failure** (since 2026.5.xx)

## Feature Requests & Roadmap Signals

### High-Community-Interest Features

| Issue | Feature | Comments/Reactions | Potential Version |
|-------|---------|-------------------|-------------------|
| [#75](https://openclaw/openclaw/issue/75) | Linux/Windows Clawdbot Apps | 109 comments, 81 👍 | Likely next major release |
| [#9443](https://openclaw/openclaw/issue/9443) | Prebuilt Android APK releases | 25 comments | Near-term |
| [#10659](https://openclaw/openclaw/issue/10659) | Masked Secrets (prevent agent access to raw API keys) | 13 comments, 4 👍 | Mid-term |
| [#12602](https://openclaw/openclaw/issue/12602) | Slack Block Kit support | 13 comments | Mid-term |
| [#78308](https://openclaw/openclaw/issue/78308) | Channel-mediated approval for MCP tool calls | 13 comments, 1 👍 | Near-term |
| [#6615](https://openclaw/openclaw/issue/6615) | Denylist support for exec-approvals | 7 comments, 7 👍 | Near-term |

### Likely Next-Release Features

Based on open PRs and community demand:
1. **MCP consent envelope** (#78308) — has clear design and strong alignment with existing shell-exec approval pipeline
2. **Exec-approval denylist** (#6615) — complements existing allowlist, high demand
3. **Memory trust tagging** (#7707) — addresses fundamental security concern about prompt injection via memory
4. **WhatsApp message delete** (#14344) — relatively contained feature with clear implementation path

## User Feedback Summary

### Pain Points

1. **Subagent reliability is the #1 frustration.** Users report empty subagent lists (#75593), stale completion delivery (#78055), duplicate answers (#77642), and write-lock timeouts (#86538). This affects users building multi-agent workflows — a core OpenClaw differentiator.

2. **Installation and onboarding friction.** Issues #76042 (clean install impossible since 5.xx) and #16670 (onboarding wizard missing memory setup) create significant barriers for new users. Multiple users report 5+ minute wait times for initial setup.

3. **Security concerns for production use.** Feature requests for masked secrets (#10659), filesystem sandboxing (#7722), capability-based permissions (#12678), and skill permission manifests (#12219) reveal **community anxiety** about running OpenClaw in sensitive environments.

4. **Cross-platform gaps.** The top-voted issue (#75, Linux/Windows clients) and Android APK request (#9443) show the community is hitting platform limits. This is likely suppressing enterprise adoption.

### Satisfaction Signals

- **High engagement with PRs** — 500 PRs updated in 24h indicates active contribution base
- **Detailed bug reports** — Users provide reproduction steps, regression matrices, and environment details, indicating invested, technical user base
- **Positive response to subagent concept** — Despite bugs, users are actively building multi-agent workflows and reporting issues, not abandoning the feature

## Backlog Watch

### Long-Unanswered Issues Needing Maintainer Attention

| Issue | Title | Age | Last Updated | Notes |
|-------|-------|-----|--------------|-------|
| [#77598](https://openclaw/openclaw/issue/77598) | Track live dev agent behavior and trajectory | **53 days** | 2026-06-26 | Maintainer issue, 22 comments, no decision |
| [#77700](https://openclaw/openclaw/issue/77700) | Tracking: Prepared runtime resolution migration | **53 days** | 2026-06-26 | Maintainer issue, no decision |
| [#74704](https://openclaw/openclaw/issue/74704) | SDK: stabilize app-client happy path | **58 days** | 2026-06-26 | Maintainer issue, no decision |
| [#33106](https://openclaw/openclaw/issue/33106) | Runtime trust verification via TrustChain | **115 days** | 2026-06-26 | **Closed as stale** — feature abandoned? |
| [#78297](https://openclaw/openclaw/issue/78297) | *(missing from top 50 but flagged)* | — | — | Possibly buried |

### Stale Issues Recently Closed

- **#33106** (Runtime trust verification via TrustChain) — Closed as stale after 115 days with 6 comments and no resolution. This represents a **significant community effort abandoned** without explanation.

### PRs Waiting on Author / Maintainer

- **#97077** — `fix(approval): distinguish policy vs non-persistable reason` — Waiting on author
- **#97086** — `feat(mxc): add Windows MXC sandbox backend` — Waiting on author (large PR, potentially blocked)
- **#90184** — `fix(ui): rename chat sessions from the picker` — Closed today after long wait
- **#14432** — `System prompt: add guidance for spawning background sub-agents` — Waiting on author since February

### Risk: Triage Bottleneck

A large fraction of P1/P2 issues carry the `clawsweeper:needs-product-decision` label, indicating **product direction decisions are a bottleneck** for resolving high-impact bugs and implementing requested features. This is particularly concerning for security-related issues (#10659, #78308, #12219, #12678) where delays increase exposure.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the June 27, 2026 community digest summaries.

---

## Cross-Project Comparison Report: AI Agent Open-Source Ecosystem

### 1. Ecosystem Overview

The personal AI assistant and agent open-source landscape is experiencing a period of intense, production-focused iteration. The ecosystem is bifurcating into two primary groups: large, feature-rich "reference" platforms (led by OpenClaw) and specialized, lightweight agents (like NanoBot and PicoClaw) targeting specific deployment niches. A dominant theme across all major projects is the struggle to stabilize **multi-agent (subagent) workflows**, which remain the primary source of critical bugs and user frustration. Concurrently, there is a strong, pan-project push toward **security hardening**, including supply-chain verification, policy-driven tool execution, and secret management, reflecting a maturation of the user base from hobbyists to enterprise operators. The ecosystem is healthy and highly active, but maintainer bandwidth for triage and product decisions is a growing bottleneck across the board.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release (24h) | Health Score (1-5) |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | No | 3 (High activity, severe triage bottleneck) |
| **NanoBot** | High (est.) | 44 | No | 4 (Very responsive, high velocity) |
| **Hermes Agent** | 50 | 50 | No | 3 (Busy, but slow-to-close pipeline) |
| **PicoClaw** | 5 | 22 | No | 4 (Focused sprint, high merge rate) |
| **NanoClaw** | 3 | 11 | No | 4 (Strong feature sprint, review bottleneck) |
| **NullClaw** | 1 | 0 | No | 2 (Low activity, critical build issue) |
| **IronClaw** | 30 | 50 | No | 4 (Intense stabilization phase) |
| **LobsterAI** | Low (est.) | 8 | **Yes (v2026.6.26)** | 4 (Healthy release cycle) |
| **CoPaw** | 29 | 50 | **Yes (v2.0.0-beta.1)** | 4 (Major migration, high momentum) |
| **ZeroClaw** | 50 | 50 | **Yes (v0.8.2)** | 5 (Excellent balance, P1 bug closure rate) |
| **Moltis** | 0 | 1 | No | 2 (Minimal activity) |
| **TinyClaw** | 0 | 0 | No | 1 (No activity) |
| **ZeptoClaw** | 0 | 0 | No | 1 (No activity) |

**Note:** Health Score is a qualitative assessment reflecting the balance of activity, responsiveness, and stability. Scores are based on data from this single day.

### 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale & Community:** OpenClaw's 500+ daily issues and PRs dwarf all other projects. It has the largest, most invested contributor base, evidenced by detailed bug reports and active participation across 100+ comment threads.
- **Architectural Breadth:** It is the only project attempting to serve as a universal "reference" core, covering a vast array of providers, clients, and subagent concepts. No other project has a comparable breadth of feature requests (desktop clients, security, Slack, etc.).
- **Feature Velocity:** Despite the triage bottleneck, the volume of merged PRs (52/day) for fixes and features indicates core development velocity is unmatched.

**Differences in Technical Approach:**
- OpenClaw functions as a **platform toolkit** (e.g., `buildGuardedModelFetch`, `clawsweeper` labels), whereas projects like NanoBot and Hermes Agent are more **integrated applications**. This makes OpenClaw more flexible but also introduces higher complexity and a greater need for maintainer triage.

**Community Size Comparison:**
OpenClaw's activity is an order of magnitude higher than the next most active projects (IronClaw, ZeroClaw, CoPaw at ~50 issues/PRs each). This confirms its position as the undisputed community heavyweight. However, this scale is also a vulnerability, as the project's `clawsweeper:needs-maintainer-review` bottleneck is the most severe in the ecosystem.

### 4. Shared Technical Focus Areas

Multiple projects are converging on identical technical pain points, indicating ecosystem-wide requirements:

- **Subagent/Multi-Agent Reliability (Critical):**
    - **OpenClaw:** Subagent delivery failures, session write-lock timeouts (#86538, #75593).
    - **LobsterAI:** Fixed frozen subagent progress in sidebar (PR #2207).
    - **PicoClaw:** Fixed duplicate messages from async sub-agents (#3094).
    - **IronClaw:** Feature focus on "Reborn" stack, which governs multi-agent and capability-policy systems.
    - **NanoBot:** Fixed `isolated_session` context leak for cron jobs (#4082).
    - **Need:** A deterministic, resilient subagent lifecycle manager is the highest ecosystem-wide priority.

- **Tool Execution & Policy Security:**
    - **NanoBot:** Multiple high-severity `exec.allowPatterns` bypasses discovered and fixed (#4514-4520).
    - **IronClaw:** Capability-policy system (epic #5261) in active development; current tool-approval UX is a major pain point.
    - **ZeroClaw:** Shell tool refused at full autonomy (#6434, fixed); `mcp_bundles` scoping was a silent no-op (#7733).
    - **Need:** A common, predictable, and auditable policy engine for tool execution is urgently required.

- **Cross-Platform & Channel Parity:**
    - **OpenClaw:** Community demand for Linux/Windows desktop clients (#75) and Android APK (#9443) is the #1 community hot topic.
    - **Hermes Agent:** Windows desktop flickering (#53342) and non-default profile session load failures (#44147).
    - **PicoClaw:** Android service launch failure (#3182); WhatsApp WebSocket timeout (#3178).
    - **CoPaw:** WeCom, Feishu, and DingTalk channel-specific bugs (file drops, @mentions).
    - **Need:** A consistent, reliable experience across all major platforms and messaging channels is a baseline expectation.

- **Memory & Context Management:**
    - **Hermes Agent:** Context compressor drops messages (#11585, fixed); Honcho memory leak (#40170).
    - **ZeroClaw:** Memory over-prioritization bug (#5844, fixed).
    - **PicoClaw:** "It gave itself amnesia" context loss (#3150).
    - **Need:** Robust, predictable context window management that survives summarization and tool calls.

### 5. Differentiation Analysis

| Feature | OpenClaw | NanoBot | Hermes Agent | ZeroClaw | CoPaw |
|---|---|---|---|---|---|
| **Primary Focus** | Universal agent platform | Lightweight, extensible personal assistant | Agent development & research | Enterprise agent interoperability | Enterprise channel integration |
| **Target User** | Developers, power users | Individual developers, hobbyists | Researchers, advanced developers | Enterprise ops, fleet managers | Enterprise ops (China market) |
| **Architecture** | Monolithic reference core | Python + Node.js (lightweight) | Python (AGPLv3) | Rust-based (high performance) | Python + AgentScope 2.0 |
| **Differentiator** | Largest community, broadest scope | "Plugins first" + security blitz | Strong research lineage, context management | A2A protocol, supply-chain security | WeCom/Feishu/DingTalk mastery |
| **Risk** | Triage bottleneck, complexity | "Ultra-lightweight" contradiction | Maintainer bandwidth, Windows UX | Security gaps in MCP isolation | v2.0 migration regressions |

### 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating & High Risk (Feature Additions)**
- **OpenClaw** - Despite its triage bottleneck, the sheer volume of activity keeps it in the lead. It is the ecosystem's "busiest city."
- **ZeroClaw** - Exhibits the best balance of high activity and high closure rate. The v0.8.2 release with A2A protocol signals a strong, strategic product vision.
- **CoPaw** - Very high momentum following a major migration (v2.0.0-beta.1). The risk is high due to breaking changes and channel-specific regressions, but the community is engaged and contributing.

**Tier 2: Stabilizing & Hardening**
- **IronClaw** - In a "intensive stabilization phase" for the Reborn stack. The focus on a capability-policy system indicates a shift from feature growth to production-grade security.
- **NanoBot** - Has a healthy, responsive team. The rapid security fixes and feature blitz (plugins, delegation) suggest a sprint toward a major stable release.
- **PicoClaw** - A "focused maintenance and quality assurance push." The systematic error-handling cleanup and SSRF fix show a mature codebase being hardened.

**Tier 3: Low Activity / Maintenance Mode**
- **Hermes Agent** - Active community but a "slow-to-close pipeline" and 70+ day unanswered questions suggest strained maintainer bandwidth.
- **NullClaw, TinyClaw, ZeptoClaw** - These show little to no activity, indicating either project dormancy, seasonal slowdowns, or a very small core team.

### 7. Trend Signals

1.  **The "Post-Experiment" Pivot:** The community is no longer interested in proof-of-concept agents. The demand is for **production reliability**: deterministic tool execution, secure secret handling, and resilient subagent workflows. Projects that fail to ship these will be quickly displaced.

2.  **Multi-Agent is the New Frontier (and the New Headache):** Every major project is wrestling with subagent reliability. The value proposition is clear (complex task decomposition), but the technical debt is piling up. The project that solves the subagent lifecycle problem (reliable spawning, context isolation, result collection) will gain a significant competitive advantage.

3.  **Security is a Non-Negotiable Feature:** *Not* a roadmap item. The volume of security bugs (bypasses, memory leaks, SSRF, MCP isolation failures) and the swift community responses signal that security is the #1 evaluation criterion for new users. The "move fast and break things" era for personal AI agents is definitively over.

4.  **Enterprise Tail Wagging the Dog:** Features like enterprise channel integration (CoPaw), supply-chain provenance (ZeroClaw), and SLSA compliance demonstrate that the most impactful users are not solo developers but **operators deploying fleets of agents in sensitive environments**. Their needs are driving the roadmap for the top-tier projects.

5.  **The Platform Trap:** OpenClaw's incredible community size is its greatest asset and its greatest liability. The massive triage bottleneck creates an opportunity for more focused, responsive projects (like NanoBot or ZeroClaw) to capture users who are tired of waiting for `clawsweeper:needs-product-decision` labels to be resolved. The ecosystem may see a fragmentation away from the single "reference core" model toward specialized, well-maintained alternatives.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for **2026-06-27**.

---

## NanoBot Project Digest — 2026-06-27

### 1. Today's Overview
The project is in a state of intense development, with a significant surge in pull request activity (44 PRs updated, 20+ new PRs opened in the last 24 hours). While no new releases were published, the volume of concurrent feature work, bug fixes, and security patches indicates a sprint towards a major version update. Community engagement is very high, driven by a coordinated security disclosure that surfaced multiple `exec` tool allowlist bypasses, alongside a long list of feature requests that are seeing active PRs. The overall health is excellent, showing a responsive maintainer team and a vibrant community.

### 2. Releases
No new releases were published on this date.

### 3. Project Progress
Six PRs were merged or closed in the last 24 hours, representing significant functional and security advancements:

- **Web Fetching:** **PR #4561** (Closed) adds optional support for [Crawl4AI](https://github.com/HKUDS/nanobot/pull/4561) as a web fetch extractor, providing a more reliable alternative to Jina.
- **Security Hardening:** Five high-priority security issues were resolved:
    - **PR #4562** (Open, fix pending merge): Validates each shell segment against `exec.allowPatterns` to fix a chained command bypass.
    - Several closed security advisories (Issues #4514, #4515, #4516, #4519, #4520) were reported and addressed, focusing on `exec` tool allowlist bypasses and MCP scope vulnerabilities.

### 4. Community Hot Topics
The most active threads reveal a community deeply engaged in shaping the project's architecture and security posture.

- **Security Overhaul (High Traffic):** The cluster of issues from user `YLChen-007` (#4514, #4515, #4516, #4519, #4520) detailing multiple `exec.allowPatterns` bypasses has been the dominant topic. The community (and maintainers) have been highly responsive, with fix PRs submitted concurrently.
- **Feature Implementation Blitz (High Volume):** While not all issues have high comment counts, a wave of new PRs from user `dajiaohuang` demonstrates the maintainers are directly addressing the most popular feature requests. This includes a new **plugin system** ([PR #4558](https://github.com/HKUDS/nanobot/pull/4558)), **external agent delegation** ([PR #4559](https://github.com/HKUDS/nanobot/pull/4559) resolving #3436 and #3024), and **per-conversation model overrides** ([PR #4555](https://github.com/HKUDS/nanobot/pull/4555) resolving #4253).
- **"Ultra-lightweight" Contradiction (Moderate Discussion):** Issue [#660](https://github.com/HKUDS/nanobot/issues/660) continues to simmer with 12 comments, highlighting a long-standing tension between the project's marketing and its actual dependency footprint (Python + Node.js). This remains a point of dissatisfaction for users seeking a truly minimal setup.

### 5. Bugs & Stability
Bug reports are being addressed with high velocity, with several fixes submitted on the same day the bugs were reported.

- **Critical - Security Bypasses (Fix Submitted):** The `exec.allowPatterns` bypass vulnerabilities (Issues #4514, #4515, #4516, #4520) are the most critical. Fix PR [#4562](https://github.com/HKUDS/nanobot/pull/4562) is open and addresses the core parsing issue.
- **High - Windows Process/Restart Issues (Fix Submitted):** Multiple Windows-specific bugs were reported:
    - **`/restart` with service managers (nssm):** Issue [#4513](https://github.com/HKUDS/nanobot/issues/4513) is fixed in [PR #4546](https://github.com/HKUDS/nanobot/pull/4546).
    - **Gateway PID file mismatch:** Issue [#4511](https://github.com/HKUDS/nanobot/issues/4511) is fixed in [PR #4547](https://github.com/HKUDS/nanobot/pull/4547).
    - **Inconsistent shell semantics (cmd vs PowerShell):** Issue [#4544](https://github.com/HKUDS/nanobot/issues/4544) is fixed in [PR #4545](https://github.com/HKUDS/nanobot/pull/4545).
- **Medium - Cron Job Context Leak (Fix Submitted):** Issue [#4082](https://github.com/HKUDS/nanobot/issues/4082) (cron jobs sharing session context across runs) is fixed in [PR #4550](https://github.com/HKUDS/nanobot/pull/4550).
- **Low - Telegram Web Rendering (Closed):** A visual-only bug with Telegram messages (Issue #4539) was quickly closed, likely resolved.

### 6. Feature Requests & Roadmap Signals
The current PR activity strongly signals the next version's feature set. The most likely incoming features are:

- **Plugin System:** [PR #4558](https://github.com/HKUDS/nanobot/pull/4558) implements a minimal plugin system, a top community request. **Prediction: Shipped in next release.**
- **External Agent Delegation:** [PR #4559](https://github.com/HKUDS/nanobot/pull/4559) adds an `agent_delegate` tool to call external CLI agents (Claude Code, Codex). **Prediction: Shipped in next release.**
- **Per-Conversation Model Override:** [PR #4555](https://github.com/HKUDS/nanobot/pull/4555) allows users to switch model presets per conversation. **Prediction: Shipped in next release.**
- **Reasoning Effort Escalation:** [PR #4552](https://github.com/HKUDS/nanobot/pull/4552) adds automatic reasoning effort escalation for complex tasks. **Prediction: Shipped in next release.**
- **TTS & Enhanced Heartbeat:** [PR #4560](https://github.com/HKUDS/nanobot/pull/4560) (TTS) and several PRs fixing config isolation for Heartbeat/Cron ([PR #4549](https://github.com/HKUDS/nanobot/pull/4549), [#4553](https://github.com/HKUDS/nanobot/pull/4553), [#4551](https://github.com/HKUDS/nanobot/pull/4551)) are also queued. **Prediction: High likelihood of inclusion.**

### 7. User Feedback Summary
Real user pain points are driving the current feature blitz.

- **Pain Point: Session/Context Management:** Users repeatedly request better control over which context a model uses. This is seen in requests for `isolated_session` for Heartbeat ([#1899](https://github.com/HKUDS/nanobot/issues/1899)), per-run cron sessions ([#4082](https://github.com/HKUDS/nanobot/issues/4082)), and fixed delivery channels ([#4418](https://github.com/HKUDS/nanobot/issues/4418)).
- **Pain Point: Inefficient Model Usage:** Users want to route specific tasks (like heartbeats or simple queries) to cheaper/faster models without manual config switching. Issues [#4253](https://github.com/HKUDS/nanobot/issues/4253), [#4029](https://github.com/HKUDS/nanobot/issues/4029), and [#4431](https://github.com/HKUDS/nanobot/issues/4431) all reflect this need for cost optimization.
- **Pain Point: Extensibility & Integration:** The requests for a plugin system ([#2231](https://github.com/HKUDS/nanobot/issues/2231)) and external agent delegation ([#3436](https://github.com/HKUDS/nanobot/issues/3436)) indicate a desire for NanoBot to function as a central hub, rather than a monolithic agent.
- **Satisfaction:** The rapid merging of PRs (e.g., Crawl4AI) and immediate response to security reports suggests high community trust in the maintainer team's responsiveness.

### 8. Backlog Watch
The following items have been open for an extended period without significant maintainer activity and represent potential technical debt or unmet community needs:

- **Issue #660: "Ultra-lightweight" Contradiction** (Updated 2026-06-26, Opened 2026-02-14): This long-standing issue about the Node.js dependency has high karma (5 👍) but no clear resolution plan. It represents a brand credibility risk.
- **Issue #2700: Crawl4AI Support** (Opened 2026-04-01): Despite now having a closed PR (#4561), the issue itself remained open for 3 months before action was taken. This tracks the long tail of feature requests.
- **Issue #1899: Heartbeat Session Isolation** (Opened 2026-03-11): While a fix PR ([#4551](https://github.com/HKUDS/nanobot/pull/4551)) now exists, this issue sat unaddressed for over 3 months, indicating a potential area where user workflows were silently broken.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-27

## Today's Overview

Hermes Agent saw elevated activity with **50 issues and 50 PRs updated in the last 24 hours**, though the majority remain open (35 issues, 47 PRs). Only **3 PRs were merged or closed** and **15 issues resolved**, suggesting a busy but slow-to-close pipeline. No new releases were published. The project shows signs of strain from sustained community growth, with multiple P1/P2 bugs receiving attention and a steady stream of feature requests indicating healthy but demanding user engagement. The backlog includes several long-standing infrastructure and UX issues that continue to generate discussion.

## Releases

No new releases were published in this period.

## Project Progress

Only **3 PRs were merged or closed** today:

- **#27974** (closed, not merged) — Added a TrustedRouter.com provider plugin using the OpenAI/OpenRouter-compatible endpoint, including CLI provider metadata and environment variable registration. Author: jperla
- **#53366** (open merge PR) — Restores local modifications stashed during a previous update, including `_estimate_tui_input_height()`, `home_mode config`, and async delegation cleanup. Author: onionlee21
- **#53363** (open, P2 bugfix) — Fixes the installer to recover from diverged managed updates when the local clone and `origin/main` have both advanced. Author: LeonSGP43

## Community Hot Topics

The most active discussions in the last 24 hours:

1. **#38240 — Skills index stale/degraded** (18 comments)  
   *An automated freshness probe has flagged the Skills Hub index as degraded for 24 days.* This is a long-running infrastructure concern that impacts all users relying on the skills documentation.  
   🔗 [NousResearch/hermes-agent Issue #38240](https://github.com/NousResearch/hermes-agent/issues/38240)

2. **#43564 — `hermes update` prunes `agent-browser` dependency** (8 comments, 2 👍)  
   *Users report that `hermes update` can silently remove the local browser dependency, breaking `hermes doctor` checks.* This is a critical UX issue for developers using browser automation.  
   🔗 [NousResearch/hermes-agent Issue #43564](https://github.com/NousResearch/hermes-agent/issues/43564)

3. **#44147 — Web dashboard fails for non-default profile sessions** (6 comments)  
   *The dashboard frontend requests messages without the owning `profile` parameter, making non-default sessions unreadable.*  
   🔗 [NousResearch/hermes-agent Issue #44147](https://github.com/NousResearch/hermes-agent/issues/44147)

4. **#31668 — Anthropic rate-limit/extra usage bug** (5 comments, 1 👍)  
   *Every API call fails with "Third-party apps now draw from your extra usage" — possibly a misconfiguration with new Anthropic billing tiers.*  
   🔗 [NousResearch/hermes-agent Issue #31668](https://github.com/NousResearch/hermes-agent/issues/31668)

5. **#44140 — Desktop GUI issues: auto-scroll, sidebar overlap, custom groups** (3 comments, 4 👍)  
   *A well-liked feature request for three core desktop UI improvements: chat auto-scrolling during streaming, right preview rail covering scrollbar, and custom session grouping.*  
   🔗 [NousResearch/hermes-agent Issue #44140](https://github.com/NousResearch/hermes-agent/issues/44140)

## Bugs & Stability

**Critical / P1 bugs reported or updated today:**

- **#40170 — Honcho memory recall leak** (P1, security)  
  *The customer-facing gateway leaks `<memory-context>` blocks containing recall data into API calls when using Honcho as a memory provider.* This is a data exposure risk.  
  🔗 [NousResearch/hermes-agent Issue #40170](https://github.com/NousResearch/hermes-agent/issues/40170)

- **#53342 — Windows desktop flickering black command prompt** (P2, UX-blocking)  
  *After upgrading on Windows 11, black terminal windows flash continuously, making the desktop client unusable.* Marked as duplicate but remains actively discussed.  
  🔗 [NousResearch/hermes-agent Issue #53342](https://github.com/NousResearch/hermes-agent/issues/53342)

- **#43564 — `hermes update` prunes `agent-browser`** (P2)  
  *Dependency silently removed during updates — see above.*

- **#53363 — Installer diverged update recovery** (P2, fix PR open)  
  *Managed installs can break when both local and remote have advanced. PR #53363 addresses this with divergence detection and reset fallback.*  
  🔗 [NousResearch/hermes-agent PR #53363](https://github.com/NousResearch/hermes-agent/pull/53363)

**Other severity bugs:**

- **#52289 — Local provider memory limit misclassification** (P2, fix PR open)  
  *oMLX/MLX memory guard failures are incorrectly classified as `context_overflow` instead of `overloaded`, leading to wrong user guidance. PR #52289 provides a fix.*  
  🔗 [NousResearch/hermes-agent PR #52289](https://github.com/NousResearch/hermes-agent/pull/52289)

- **#52843 — Remote file tool path corruption** (P2, fix PR open)  
  *Non-local terminal backends can canonicalize valid remote paths (e.g., `/home/...` → `/System/Volumes/Data/home/...`) causing `write_file` to report incorrect locations. PR #52843 preserves remote paths.*  
  🔗 [NousResearch/hermes-agent PR #52843](https://github.com/NousResearch/hermes-agent/pull/52843)

**Closed bugs with fixes validated:**

- **#11585 — Context compressor drops messages on summarization failure** (P1, closed)  
  *When `_generate_summary()` fails, the compressor deletes conversation turns and only keeps head + tail — losing the middle of conversations. Fix has been merged.*  
  🔗 [NousResearch/hermes-agent Issue #11585](https://github.com/NousResearch/hermes-agent/issues/11585)

- **#28093 — Context compaction drops user messages mid-conversation** (P1, closed)  
  *User messages sent during active processing are lost when compaction triggers on the agent's response turn. Fix confirmed.*  
  🔗 [NousResearch/hermes-agent Issue #28093](https://github.com/NousResearch/hermes-agent/issues/28093)

## Feature Requests & Roadmap Signals

**Most-liked and most-discussed feature requests:**

1. **#44140 — Desktop GUI improvements** (4 👍, 3 comments)  
   *Auto-scroll during streaming, sidebar overlap fix, custom session groups.* High demand for core UX polish.

2. **#53349 — `cwd-local soul.md` for per-directory agent identity** (2 comments)  
   *Allow per-directory `SOUL.md` files so agents have different personas depending on the project context. PR #53353 is open with an implementation.*  
   🔗 [NousResearch/hermes-agent Issue #53349](https://github.com/NousResearch/hermes-agent/issues/53349)

3. **#53341 — `!` prefix for direct shell passthrough** (1 comment)  
   *CLI users want a shorthand for bypassing the agent loop and executing shell commands directly (e.g., `!ls`, `!git status`).*  
   🔗 [NousResearch/hermes-agent Issue #53341](https://github.com/NousResearch/hermes-agent/issues/53341)

4. **#53320 — Add Vestige as a memory provider** (1 comment)  
   *Community-contributed plugin for an alternative memory backend, seeking official inclusion.*  
   🔗 [NousResearch/hermes-agent Issue #53320](https://github.com/NousResearch/hermes-agent/issues/53320)

5. **#52857 — CLI session browse sort by latest activity** (1 comment)  
   *Users want session pickers sorted by last activity, not creation time.*  
   🔗 [NousResearch/hermes-agent Issue #52857](https://github.com/NousResearch/hermes-agent/issues/52857)

**Predictions for next version:** The `cwd-local SOUL.md` feature (PR #53353) and the TrustedRouter provider addition (PR #27974, PR #53364) appear close to merging and are likely candidates for a near-term release. The CLI `!` shell passthrough is a low-risk, high-utility feature that could ship quickly.

## User Feedback Summary

**Pain points (high frequency):**

- **Context compaction losing messages** — Multiple bugs (closed) and lingering concerns about reliability of long sessions.
- **Platform-specific instability** — Windows desktop flickering (#53342), non-default profile session loading (#44147), Discord markdown rendering (#21168) — cross-platform parity remains a weakness.
- **Update/recovery failures** — `hermes update` prunes dependencies (#43564), Windows update loops (#38122), installer divergence (#53363) — the update mechanism is fragile.
- **Provider integration friction** — Anthropic billing tier confusion (#31668), Ollama reasoning model empty responses (#46131), local provider memory misclassification (#52289).

**Satisfaction signals:**

- Strong community contribution activity (50 open PRs, multiple feature PRs from first-time contributors)
- Vestige memory provider plugin (#53320) shows healthy plugin ecosystem development
- Repeated use of `hermes doctor` as a diagnostic tool indicates users value health checking

## Backlog Watch

**Long-unanswered issues needing maintainer attention:**

1. **#7269 — WhatsApp groups and `require_mention: true`** (3 comments, last updated 2026-06-27)  
   *Opened 2026-04-10 — 78 days ago. User asks whether bot-only responding to allowed users in WhatsApp groups is by design. No maintainer response.*  
   🔗 [NousResearch/hermes-agent Issue #7269](https://github.com/NousResearch/hermes-agent/issues/7269)

2. **#12020 — How to suppress `hermes.tool.progress` events** (5 comments, last updated 2026-06-26)  
   *Opened 2026-04-18 — 70 days ago. User requests a toggle to disable progress events that break OpenAI-compatible frontends. No decision or roadmapping from maintainers.*  
   🔗 [NousResearch/hermes-agent Issue #12020](https://github.com/NousResearch/hermes-agent/issues/12020)

3. **#4445 — Telegram Gateway: message chunking/splitting** (2 comments, last updated 2026-06-26)  
   *Opened 2026-04-01 — 87 days ago. Feature request for custom separator-based message splitting during streaming in Telegram. No maintainer engagement.*  
   🔗 [NousResearch/hermes-agent Issue #4445](https://github.com/NousResearch/hermes-agent/issues/4445)

4. **#20840 — Setup failure with dual RTX A6000 + vLLM** (1 comment, last updated 2026-06-27)  
   *Opened 2026-05-06 — 52 days ago. User with high-end hardware reports Hermes fills available context too quickly for Llama-3.1-70B. No diagnostic assistance from maintainers.*  
   🔗 [NousResearch/hermes-agent Issue #20840](https://github.com/NousResearch/hermes-agent/issues/20840)

5. **#39020 — Desktop: Dedicated Providers settings section** (2 comments, last updated 2026-06-26)  
   *Opened 2026-06-04 — 23 days ago. Feature request for per-provider API key management in the desktop GUI. Marked P3 with no assignee.*  
   🔗 [NousResearch/hermes-agent Issue #39020](https://github.com/NousResearch/hermes-agent/issues/39020)

**Verdict:** The project shows strong community momentum but strained maintainer bandwidth. Several P1 security and data-loss bugs were closed, which is positive, but the 70+ day unanswered questions suggest the team is prioritizing critical issues over feature requests and support questions. The 47 open PRs and 35 open issues represent a growing backlog that may need triage attention.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-27

## Today's Overview

PicoClaw is showing strong development momentum with 22 pull requests updated in the last 24 hours, of which 14 were merged or closed. This high PR activity—combined with 5 active issues—indicates a focused maintenance and quality assurance push. The project team appears to be in a sprint to resolve lint warnings, improve error handling hygiene, and patch critical connectivity bugs, particularly around WebSocket stability for messaging channels. No new releases were cut today, but the volume of merged fixes suggests a release may be imminent.

## Releases

No new releases were published today. The latest release remains the previously noted version.

## Project Progress

**14 PRs merged/closed today**, spanning several areas:

**Infrastructure & Dependency Updates (6 merged)**
- [`#3173`](https://github.com/sipeed/picoclaw/pull/3173) — Bump `modernc.org/sqlite` from 1.51.0 to 1.53.0
- [`#3174`](https://github.com/sipeed/picoclaw/pull/3174) — Bump `line/line-bot-sdk-go/v8` to 8.20.1
- [`#3175`](https://github.com/sipeed/picoclaw/pull/3175) — Bump `fyne.io/systray` to 1.12.2
- [`#3176`](https://github.com/sipeed/picoclaw/pull/3176) — Bump `mymmrac/telego` to 1.10.0 (Telegram Bot API v10)

**Security & Correctness Fixes (6 merged)**
- [`#3143`](https://github.com/sipeed/picoclaw/pull/3143) — Fix SSRF guard bypass via ISATAP IPv6 literals embedding private IPv4 addresses (high-severity web security fix)
- [`#3181`](https://github.com/sipeed/picoclaw/pull/3181) — Guard gateway startup info assertions against missing/malformed status data

**Error Handling Hygiene (6 merged)**
- [`#3183`](https://github.com/sipeed/picoclaw/pull/3183) through [`#3188`](https://github.com/sipeed/picoclaw/pull/3188) — A systematic cleanup of unhandled `resp.Body.Close()` and `json.Encode` errors across OneBot, WhatsApp, Pico channels, health server, updater, membench, and test utilities.

**Gateway Feature** — [`#3063`](https://github.com/sipeed/picoclaw/pull/3063) (adds Delta Chat gateway) remains open with ongoing work.

## Community Hot Topics

**🔴 #3094 — Duplicate messages from async sub-agents** *(Closed, 3 comments)*  
[Issue Link](https://github.com/sipeed/picoclaw/issues/3094)  
A long-standing bug where `spawn` tool results appeared both as raw sub-agent output and as formatted main-agent summary, causing double-posts on Telegram/Feishu. Now closed, implying a fix is in place.

**🟢 #3088 — Replace libolm with vodozemac** *(Open, 3 comments, 2 👍)*  
[Issue Link](https://github.com/sipeed/picoclaw/issues/3088)  
Community-driven security concern: libolm is unmaintained. Request to switch to vodozemac (official Matrix replacement library) with compile-time optionality. This has been open since June 9 and received maintainer discussion — a strong candidate for the roadmap.

**🟢 #3150 — "It gave itself amnesia"** *(Open, 3 comments)*  
[Issue Link](https://github.com/sipeed/picoclaw/issues/3150)  
An entertaining but concerning title describing a memory/context loss bug. The author reports the AI agent forgets context mid-conversation. Marked `stale` but only a week old — maintainers should re-evaluate.

**🟢 #3182 — Android version cannot launch** *(Open, 0 comments)*  
[Issue Link](https://github.com/sipeed/picoclaw/issues/3182)  
New report: the Android build fails to start a service, with the user unable to change path from settings. This may be a packaging or permission regression for the Android target.

**🟢 #3178 — WhatsApp WebSocket Timeout** *(Open, 0 comments)*  
[Issue Link](https://github.com/sipeed/picoclaw/issues/3178)  
WhatsApp channel connectivity issue: WebSocket connections timeout on Docker with Launchpad. This is particularly timely given [`#3179`](https://github.com/sipeed/picoclaw/pull/3179) (open PR to add reconnection logic for WhatsApp WebSocket drops).

## Bugs & Stability

| Severity | Issue | Status | Notes |
|----------|-------|--------|-------|
| **HIGH** | [#3178](https://github.com/sipeed/picoclaw/issues/3178) — WhatsApp WebSocket timeout | 🟢 Open | Fix PR [#3179](https://github.com/sipeed/picoclaw/pull/3179) adds reconnection logic and ping/pong keepalive |
| **HIGH** | [#3182](https://github.com/sipeed/picoclaw/issues/3182) — Android service launch failure | 🟢 Open | No fix PR yet; may be a packaging regression affecting Android users |
| **MEDIUM** | [#3150](https://github.com/sipeed/picoclaw/issues/3150) — Context loss / memory wipe | 🟢 Open, stale | Reported 8 days ago; lacks environment details for reproduction |
| **FIXED** | [#3094](https://github.com/sipeed/picoclaw/issues/3094) — Duplicate sub-agent messages | ✅ Closed | Fix appears merged |
| **FIXED** | [#3143](https://github.com/sipeed/picoclaw/issues/3143) — SSRF bypass via ISATAP | ✅ Merged | Critical web security vulnerability patched |

**Notable:** The systematic error-handling PRs (#3183–3188) indicate the team is cleaning up long-standing code quality debt that could mask runtime failures.

## Feature Requests & Roadmap Signals

**High Likelihood for Next Release:**
- **Delta Chat Gateway** ([#3063](https://github.com/sipeed/picoclaw/pull/3063)) — Open for 19 days, active. Adds a new messaging channel.
- **WhatsApp WebSocket Reconnection** ([#3179](https://github.com/sipeed/picoclaw/pull/3179)) — Directly addresses the WhatsApp timeout bug; maintainers are actively iterating.

**Medium-Term Signals:**
- **vodozemac Migration** ([#3088](https://github.com/sipeed/picoclaw/issues/3088)) — Community desire for modern crypto. The `help wanted, priority: high` labels suggest maintainers endorse this but need implementation help.
- **Copilot SDK v1.0.4 Upgrade** ([#3177](https://github.com/sipeed/picoclaw/pull/3177)) — Major version bump from 0.2.0 to 1.0.4, still open. May require API changes.

**Low Probability:** No new AI model integrations or major architecture changes signaled.

## User Feedback Summary

**Pain Points:**
- **WhatsApp reliability** (#3178): Users running on Docker/Launchpad are unable to maintain WebSocket connections — the most actionable complaint today.
- **Android usability** (#3182): Mobile users face a launch blocker that prevents service startup, suggesting insufficient testing on ARM/Android.
- **Sub-agent message spam** (#3094): Now resolved, but was frustrating for users relying on async delegation in chat channels.
- **Memory loss** (#3150): A single report of context corruption, but the colorful title suggests noticeable user frustration.

**Satisfaction Signals:**
- The rapid closure of 6 error-handling PRs suggests active maintenance that users appreciate.
- The ISATAP SSRF fix (#3143) shows the team is responsive to security research disclosures.

## Backlog Watch

**🔴 [#3088 — vodozemac migration](https://github.com/sipeed/picoclaw/issues/3088)**  
Open since June 9. While labeled `help wanted`, this is a security-critical dependency replacement. The unmaintained libolm dependency will only grow riskier over time. **Suggestion:** Prioritize for next minor release or explicitly call for community contributions.

**🟡 [#3063 — Delta Chat gateway](https://github.com/sipeed/picoclaw/pull/3063)**  
Open since June 8. A major new feature PR with no merge activity in 19 days. If maintainers are interested in Delta Chat support, this needs renewed attention to avoid bitrot.

**🟡 [#3150 — Memory/context loss](https://github.com/sipeed/picoclaw/issues/3150)**  
Marked `stale` despite being only 8 days old. If the environment details can be gathered from the reporter, this could reveal a deeper issue in context window management.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest
**Date:** 2026-06-27  
**Analysis Period:** 2026-06-26 – 2026-06-27

---

## Today's Overview

NanoClaw saw one of its most active development days in recent weeks, with **11 pull requests** updated in the last 24 hours—nearly all opened yesterday—and **3 issues** receiving attention. The project is in a clear **feature-and-fix sprint**, with multiple contributors landing improvements across WhatsApp group encryption, Signal debug cleanup, Discord attachment handling, v2 database migration fixes, and several new operational skills. The maintainer team appears highly engaged, with grantland authoring 5 PRs alone, though 9 of the 11 PRs remain open, suggesting a review backlog. No new releases were cut, but the volume of merged/fixed PRs points to an imminent release candidate.

---

## Releases

**None** – No new releases were published in the reporting period.

---

## Project Progress

### Merged/Closed PRs (2 items)
- **#2859** ([closed](https://github.com/nanocoai/nanoclaw/pull/2859)) – `fix(migrate-v2): don't SELECT is_main from v1 registered_groups`  
  *Author: cben0ist* – Critical fix for the v2 database migration. The migration previously queried the `is_main` column from the v1 `registered_groups` table, which didn't exist in older v1 installs (e.g. 1.1.0). This caused the migration to crash with `no such column: is_main`, preventing v2.db creation and cascading into sessions and tasks. This fix unblocks v2 adoption for users on legacy installations.

- **#2867** ([closed](https://github.com/nanocoai/nanoclaw/pull/2867)) – `test. finding`  
  *Author: Strke* – Minor/test PR (likely a CI validation or documentation update).

### Notable Open PRs Showing Active Progress
- **#2870** – WhatsApp group encryption fix (elancode) – critical for WhatsApp group functionality
- **#2866** – Telegram legacy markdown sanitizer removal (grantland) – modernization effort
- **#2865, #2864** – Stale session rotation fixes (grantland) – reliability for provider and opencode sessions
- **#2863** – `/setup-system-digest` and `/system-digest` skills (grantland) – new utility skills
- **#2862** – `/manage-agents` and `/manage-schedules` skills (grantland) – new operational skills
- **#2861** – MCP server env variable expansion (grantland) – infrastructure improvement
- **#2860** – Signal libsignal debug spam suppression (caburi00) – logging hygiene
- **#2752** – Discord attachment staging fix (chubbicorn245) – long-running PR for Discord usability

---

## Community Hot Topics

### Most Active Items

1. **Issue #2868** ([open](https://github.com/nanocoai/nanoclaw/issues/2868)) – `/update-skills` silent no-op for installed channels  
   *Creator: glifocat* | 0 comments but notable as the only open bug issue | *Signal:* Users expect `/update-skills` to refresh channel adapter code and dependencies, but it silently skips those steps. This undermines the v4.29 migration instructions telling users to "re-run `/add-<channel>`".

2. **PR #2870** ([open](https://github.com/nanocoai/nanoclaw/pull/2870)) – WhatsApp group encryption fix  
   *Author: elancode* | High activity (likely in review) | *Root cause identified:* `getNormalizedGroupMetadata()` is the sole provider for Baileys' `cachedGroupMetadata` socket hook, which Baileys uses for group encryption. The fix restores native participant addressing for groups.

3. **PR #2859** ([closed](https://github.com/nanocoai/nanoclaw/pull/2859)) – v2 migration fix  
   *Author: cben0ist* | Closed and merged | *Underlying need:* Users on older v1 installs who attempt v2 migration encounter a hard crash. This fix addresses a silent blocker for v1→v2 migration that could affect a significant portion of the userbase.

### Underlying Needs Analysis
The community is signaling two primary concerns: (1) **Migration reliability** – users upgrading from v1 to v2 face breaking issues that aren't gracefully handled, and (2) **Channel/skills management** – the `/update-skills` command doesn't actually update installed skills, creating confusion and manual workarounds. Both suggest a need for better upgrade paths and more transparent skill lifecycle management.

---

## Bugs & Stability

### High Severity

| Issue | Description | Status | Fix PR? |
|-------|-------------|--------|---------|
| **#2868** | `/update-skills` silent no-op for installed channels – pre-flight skips code/deps refresh | **OPEN** – unaddressed | No fix PR yet |
| **#2870** | WhatsApp group replies never appear – logged as delivered but invisible | OPEN – fix proposed | Yes – PR #2870 |
| **#1275** | Bot silent when added to new Telegram group – should auto-register prompts | **CLOSED** (was stale) | No fix identified initially; reopened? Unclear |

### Medium Severity
- **#2752** – Discord attachments (text + images) unreachable by agent – raw `[file: ...]` placeholder with no bytes (fix PR open since June 12)
- **#2865/#2864** – Stale provider/opencode sessions not rotating properly under certain conditions (fix PRs open)
- **#2860** – libsignal debug logging leaks session key material in console output (fix PR open)

### Low Severity
- **#2869** – Filed-in-error issue (closed)

### Stability Assessment
The WhatsApp group encryption issue is the most critical active bug – it renders group communication totally non-functional. The v2 migration fix (#2859) has been merged, which should stabilize upgrades. The stale session issues (#2865/#2864) could cause intermittent failures in production environments.

---

## Feature Requests & Roadmap Signals

### New Features in Active PRs (Likely for Next Release)
1. **System Digest Skills** ([PR #2863](https://github.com/nanocoai/nanoclaw/pull/2863)) – `/setup-system-digest` and `/system-digest` utility skills for automated status summaries
2. **Agent & Schedule Management** ([PR #2862](https://github.com/nanocoai/nanoclaw/pull/2862)) – `/manage-agents` and `/manage-schedules` operational skills for administrative control
3. **MCP Environment Variable Expansion** ([PR #2861](https://github.com/nanocoai/nanoclaw/pull/2861)) – `expand ${VAR_NAME}` refs in MCP server env at spawn time, enabling dynamic configuration

### User-Requested Features (Unresolved)
- **Auto-prompt on group join** ([#1275](https://github.com/nanocoai/nanoclaw/issues/1275)) – Users want the bot to proactively announce itself when added to new Telegram groups, rather than remaining silent. This issue is 3 months old and was closed, suggesting it may be deprioritized or considered out of scope. However, the user need—discoverability and onboarding clarity—remains valid.

### Prediction for Next Version
Based on the concentration of PRs from grantland (5 PRs) and the focus on skills management + session reliability, the next release (likely v4.30 or v5.0) will include:
- New `/setup-system-digest`, `/system-digest`, `/manage-agents`, `/manage-schedules` skills
- WhatsApp group encryption fix
- Telegram markdown sanitizer removal (simplifying the adapter)
- v2 migration stability (already merged)
- Signal debug logging cleanup

---

## User Feedback Summary

### Verified Pain Points
1. **WhatsApp groups broken** – "replies logged as delivered but never appeared in the group" – a fundamental communication failure for WhatsApp group users
2. **Discord attachments invisible to agent** – users pasting text or images see only placeholder tokens; the agent has no access to content
3. **`/update-skills` lies to users** – "Running `/update-skills` on an installed channel does not refresh that channel's adapter code or pinned dependency" – creates false confidence and wasted troubleshooting time
4. **V2 migration crashes** – users on older v1 installs hit a hard migration failure that prevents adoption of v2 features
5. **Signal debug spam** – log files fill with session key material, which is also a mild security concern

### Use Cases & Satisfaction
- **Telegram users** appear stable (no new Telegram-specific bugs reported beyond the old auto-prompt request)
- **WhatsApp group users** are likely frustrated – no working group communication
- **Developers upgrading from v1** – migration fix (#2859) is a welcome improvement, but the `/update-skills` bug (#2868) creates friction for the upgrade flow
- **Multi-platform administrators** – the new operational skills (system digest, agent/schedule management) signal a focus on making administration easier, which aligns with enterprise/deployment use cases

### Sentiment Overview
The project is clearly well-maintained given the high PR volume, but users experiencing WhatsApp group failures or v1→v2 migration crashes are likely at an impasse. The `/update-skills` issue (#2868) is particularly concerning because it makes the documented upgrade path unreliable.

---

## Backlog Watch

### Issues Needing Maintainer Attention
- **#2868** ([open](https://github.com/nanocoai/nanoclaw/issues/2868)) – `/update-skills` silent no-op bug  
  *0 comments, no maintainer response* – This is a clear regression that should be prioritized given it breaks a documented upgrade path.

- **#1275** ([closed](https://github.com/nanocoai/nanoclaw/issues/1275)) – Auto-prompt registration when added to new group  
  *Closed after 3 months with no resolution* – This feature request has steady user interest (no reactions listed, but the topic is recurring). If intentionally closed, a status update would help manage expectations.

### PRs Needing Review
- **#2752** ([open](https://github.com/nanocoai/nanoclaw/pull/2752)) – Discord attachment staging fix  
  *Open since June 12 (15 days)* – This is the longest-running open PR. Discord functionality impacts a significant user segment. The PR has not received maintainer comments despite being labeled as a fix.

- **#2860** ([open](https://github.com/nanocoai/nanoclaw/pull/2860)) – Signal debug spam suppression  
  *Small, low-risk change* – This could be merged quickly to clean up logs and mitigate a minor security concern.

### Maintainer Engagement Note
Grantland's high output (5 PRs filed in one day) suggests active development capacity, but the review bottleneck on 9 open PRs indicates that code review bandwidth may be the current constraint. The community would benefit from updated review timelines or merge criteria on these open PRs.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for June 27, 2026.

---

## NullClaw Project Digest – 2026-06-27

### 1. Today's Overview
The project is currently in a low-activity period, with no new releases or pull requests in the last 24 hours. There is one open issue, which has been updated recently but remains unresolved, indicating a bottleneck in the build pipeline for mobile environments. The lack of new contributions or merged code suggests maintainers may be in a planning or refactoring phase. While the project is stable on primary platforms, a critical platform-specific build failure on Android/Termux requires attention to prevent regressing mobile user support.

### 2. Releases
No new releases were published in the last 24 hours. The latest available release remains **v2026.4.17**. Users are advised to continue using this version until further notice.

### 3. Project Progress
No pull requests were merged or closed today. There is no advancement on feature development or bug fixes visible in the last 24 hours.

### 4. Community Hot Topics
The only active discussion revolves around a single, long-standing build issue:

- **[#868 [OPEN] [bug] zig build fails on Android/Termux (aarch64) with AccessDenied on options.zig linkat](https://github.com/nullclaw/nullclaw/issues/868)** (3 comments, last updated 2026-06-26)
  - **Analysis:** This issue is the sole point of community engagement. The user (NOTJuangamer10) is attempting to build NullClaw on an Android device using Termux with Zig 0.16.0. The failure occurs during the linking phase (`linkat` syscall), pointing to a potential permission model conflict between the Zig runtime and Termux’s restricted file system.
  - **Underlying need:** Users on Android/Linux environments (especially via Termux) need a seamless build experience. This bug signals that the build system does not yet handle filesystem access restrictions common on mobile/sandboxed Linux environments.

### 5. Bugs & Stability
- **Critical Bug:** Issue [#868](https://github.com/nullclaw/nullclaw/issues/868) — Build failure on Android (aarch64) due to `AccessDenied` on `linkat` during `zig build`.
  - **Severity:** High (blocks all Android builds from source).
  - **Status:** Open, no associated fix PR. The issue has been open since April 23, 2026, and was last updated by the community (not a maintainer) on June 26. No maintainer response is recorded.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the persistent nature of Issue #868 suggests that **improved cross-platform build support (especially for termux/aarch64)** is a hidden roadmap requirement. If unresolved, the next release may need to include a build-script patch or fallback linking mechanism to accommodate mobile filesystem permissions.

### 7. User Feedback Summary
- **Pain Points:** One user is actively blocked from building NullClaw on their daily driver (Android/Termux). The lack of maintainer response (since April) may indicate dissatisfaction with responsiveness on niche platforms.
- **Use Case:** Mobile/handheld usage of NullClaw is an emerging but unsupported use case. The user is attempting a standard `zig build -Doptimize=ReleaseSmall`, implying they want a lightweight, production-ready agent on Android.
- **Satisfaction:** No positive feedback is visible. The silence on this issue may lead to user attrition if not addressed.

### 8. Backlog Watch
- **[Issue #868](https://github.com/nullclaw/nullclaw/issues/868)** — This issue has been open for **65 days** without a maintainer response. It is the single most important item in the backlog. If the project aims to support mobile/ARM64 users, this requires a triage response (even if only to acknowledge the bug and provide a workaround). The delay risks driving away mobile contributors and users.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-27

## 1. Today's Overview
The IronClaw project shows **very high activity** with 30 issues and 50 PRs updated in the last 24 hours—one of the busiest recent days. The project appears to be in an **intensive development and stabilization phase**, particularly around the "Reborn" stack which is the focus of 11+ open issues and 5+ large PRs. A significant **capability-policy system** (epic #5261) is advancing through a stacked PR chain, while tool-approval UX bugs dominate the issue tracker. No new releases were cut today, suggesting the team is consolidating changes before a major version bump. The **code coverage CI remains red** due to test-harness issues (#5329), and a **security-deferred invariant** was surfaced in coverage gates (#5332).

---

## 2. Releases
**No new releases** today. The last automated release PR (#5311) proposes bumping `ironclaw` from 0.24.0 → 0.29.1 with two breaking changes (`ironclaw_common` 0.4.2→0.5.0, `ironclaw_skills` 0.3.0→0.4.0) but remains **open/unmerged**.

---

## 3. Project Progress
**15 PRs merged/closed today** (out of 50 updated). Key advances:

| PR | Description | Impact |
|---|---|---|
| [#5367] | Test LLM loop failure modes (retry on invalid model output) | Adds regression coverage for Reborn agent loop |
| [#5265] | Env-configurable turn-runner concurrency (0=unlimited) | Enables stress-testing libSQL backend |
| [#3890] | Reborn multi-tenant isolation contract tests | Foundation for production multi-tenancy |
| [#3767] | Lean host NoExposureGuard service | Adds text/JSON/HTTP leak detection safety |
| [#3766] | AuthorizedDispatchRequest seal for dispatch authority | Security hardening of capability dispatch |
| [#4934] | Dependency bump: js-yaml 4.1.1→4.2.0 | Docs architecture-video bump |

**Notable closed issues (5 total):** #5009 (Slack OAuth DM-parity), #5283 (tool approval persistence), #5197 (disabled tool behavior), #5227 (run failure message attachment), #5282 (Logs entry in composer).

---

## 4. Community Hot Topics
The most active discussions center on **tool approval UX and automation reliability**:

- **[Issue #5331]** (1 comment) — Tool-approval 'always' may not auto-approve the next same-tool call. A suspected **product bug in engine v2** with medium confidence, flagged by BenKurrek. The test `test_chat_reply_always_auto_approves_next_same_tool` shows the first "always" approval works, but the second same-tool call re-prompts. **Needs engine/approval owner confirm.**

- **[Issue #5283]** (2 comments, CLOSED) — "Approve & always allow" not persisted for `nearai.web_search`. Reproduced by sunglow666 on Reborn CI Preview. Fixed and closed rapidly, but highlights **persistence fragility** in tool permissions.

- **[Issue #5192]** (1 comment) — Denying a tool approval can still lead to additional tool approval requests. Sunglow666 reports a workflow where rejecting one tool still triggers new approval dialogs for unrelated tools. **Points to missing prompt/state reset after denial.**

- **[Issue #5196]** (1 comment) — "Ask each time" tool permission fails with authorization error and triggers **duplicate approval flow**. After approve, tool fails with `authorization` error and re-asks in chat.

**Underlying need:** Users require **deterministic, predictable tool approval behavior**—the current system has multiple failure modes (not persisting, not auto-approving, spawning duplicate dialogs, denying incorrectly). This is the #1 UX friction point.

---

## 5. Bugs & Stability

### Critical/Severe
| Issue | Summary | Status |
|---|---|---|
| [#5331] | Tool-approval 'always' may not auto-approve next same-tool call (engine v2) | OPEN, needs owner |
| [#5337] | Wasm-channel OAuth setup can't reach auth_url on first-time configure—**OAuth completely blocked** for fresh channels | OPEN, no workaround |
| [#5332] | `--all-features` coverage auto-enables forward-feature gates, exposing **deliberately-deferred security invariant** (memory isolation) | OPEN, structural gating bug |
| [#5289] | Run ends with generic "driver protocol error" after `builtin.json` `invalid_input`—**hides actual failure** | OPEN |
| [#5316] | Gmail extension discovery/install **inconsistent**—same prompt fails then succeeds without changes | OPEN |

### Medium
| Issue | Summary | Status |
|---|---|---|
| [#5323] | Automation creation fails because runner lease expires | OPEN |
| [#5322] | Automation creation times out before completion | OPEN |
| [#5302] | Pending approval in one conversation blocks sending in other conversations until refresh | OPEN |
| [#5319] | Automation created with UTC schedule without timezone confirmation—confusing Next Run display | OPEN |
| [#5333] | Composer keeps submitted message visible briefly after sending | OPEN |
| [#5330] | E2E skills-tab tests assert v2 SPA but harness serves legacy gateway (5 tests failing) | OPEN, test-harness issue |

### Lower Severity
| Issue | Summary | Status |
|---|---|---|
| [#5329] | E2E coverage: mock-LLM harness + stale-test failures (no product bugs, 10+ test-harness issues) | OPEN, test-only |
| [#5315] | Daily failure taxonomy—PinchBench near-pass, ClawBench 7.5/10 (flaky on large orchestrations) | OPEN, benchmark tracking |

**Fix PRs exist for:** #5365 (Retry button), #5366 (default auto-approve toggle), #5363 (Calendar event discovery). **No fix PRs yet** for the critical OAuth (#5337) or memory isolation (#5332) bugs.

---

## 6. Feature Requests & Roadmap Signals

### Strong Incoming Features (covered by open PRs)
| Feature | PR/Issue | Status | Likely next version? |
|---|---|---|---|
| **Capability-policy system** (epic #5261) | #5349, #5355, #5270, #5272 | 4 PR chain, all OPEN | **Yes**—this is the dominant theme |
| **"Always allow eligible tools" default ON** | #5366 (PR) | OPEN, risk=low | **Yes**—simple toggle flip |
| **Trace Commons: instance enrollment + per-user profiles** | #5280 (PR) | OPEN, size=XL | **Yes**—DB migration included |
| **Reborn WebUI v2 live QA canary** | #5354 (PR) | OPEN | **Yes**—CI infrastructure |
| **Remove WebUI chat connect shortcut** | #5362 (PR) | OPEN, size=XL | **Probable**—feature parity cleanup |
| **Wire non-Slack channel personal pairing** | #5368 (Issue) | OPEN, new today | **Next**—follow-up to #5362 |

### User-Requested Features (issues only)
| Issue | Request | Sentiment |
|---|---|---|
| [#5364] | Default "Always allow eligible tools" to ON | **Strong positive**—loopstring filed with fix PR #5366 |
| [#2355] | Persistent multi-identity Chrome + CDP browsing (epic) | Long-standing enhancement, dormant since April |
| [#5272] | REST-created local users for capability-policy testing | Development tooling, prerequisite for epic #5261 |

### Predictions for Next Release (likely `ironclaw 0.29.x`)
- Capability-policy engine + availability dimension + REST control plane
- Default auto-approve toggle ON
- Calendar event discovery fixes (PR #5363)
- Retry button fix (PR #5365)
- Dependency bumps including `ratatui 0.30` (PR #5361, fixes UB in `lru`)

---

## 7. User Feedback Summary
User **sunglow666** is the most active bug reporter (9 issues in 2 days), all on the Reborn WebUI v2. Key pain points:

1. **Tool approval confusion** — "always allow" not persisting (#5283), denial spawning more approvals (#5192), duplicate approval flows (#5196), approval blocking other conversations (#5302)
2. **Automation reliability** — timeouts (#5322), lease expiry (#5323), silent halt after planning (#5320), UTC schedule confusion (#5319)
3. **UX friction** — composer not clearing (#5333), Logs entry in composer (#5282), generic driver protocol errors (#5289), disabled tools invoking other tools (#5197)
4. **Extension inconsistency** — Gmail discovery failing then succeeding (#5316), OAuth setup blocked (#5337)

**Dissatisfaction signal:** Multiple issues describe the system "silently failing" or "hiding the actual error"—users cannot understand what went wrong or how to fix it. The generic "driver protocol error" (#5289) is a specific pain point.

**Satisfaction signal:** The near-pass on PinchBench (#5315) and ClawBench 7.5/10 suggest the agent loop itself is functional; the friction is in **tool configuration and approval UX**, not core capability.

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention
| Issue | Age | Reason |
|---|---|---|
| [#4108] | 31 days | **Nightly E2E continually failing** since May 27. Auto-filed by CI, last updated yesterday suggesting it's still red. No human response. |
| [#5331] | 1 day | **Engine v2 tool approval bug** — BenKurrek explicitly says "Needs engine/approval owner to confirm." Unresolved. |
| [#5337] | 1 day | **Fresh OAuth completely blocked** — wasm channels can never start OAuth flow. No workaround. |
| [#5332] | 1 day | **Deferred security invariant exposed** by coverage gates. Reborn/memory owner decision needed. |
| [#5274] | 2 days | **Runner-lease CAS loop migration** — security reviewer found filesystem guardrail violation. Needs follow-up PR. |

### Stale PRs of Concern
| PR | Age | Notes |
|---|---|---|
| [#5271] | 2 days | **47 dependency bumps** (rustls, refinery, etc.) — massive but stale. Security-relevant (GHSA-rhfx-m35p-ff5j mentioned in #5361). |
| [#5311] | 1 day | **Release PR** — blocked? All breaking changes, merges the 0.24→0.29 jump. Waiting on other PRs to land? |

### What's Missing
- **No triage labels** on many issues — `5350`, `5364`, `5330`, `5333` lack severity/priority tags
- **No assignee** on critical bug #5337 (wasm-channel OAuth blocked)
- **No maintainer response** on 31-day-old nightly E2E failure (#4108)
- **Dependabot PRs (#4934, #5271)** linger with no active merge path despite containing security fixes

---

*Generated 2026-06-27 from nearai/ironclaw GitHub activity. All links: Issue/PR numbers reference `github.com/nearai/ironclaw`.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-06-27**.

---

## LobsterAI Project Digest – June 27, 2026

### 1. Today's Overview
The project experienced a very high-activity day, with 8 pull requests merged (a significant spike from normal daily averages) and 1 new release published (v2026.6.26). Activity was primarily driven by infrastructure upgrades (OpenClaw runtime), fixes for the Cowork (multi-agent) system, and prompt engineering UI improvements. The community is engaging with a critical Bug Report regarding a desktop freeze during data backup. Overall, project health is robust, with maintainers rapidly closing issues and improving stability, though the new bug warrants immediate attention.

### 2. Releases
**New Version: [LobsterAI 2026.6.26](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.26)**

**Key Changes:**
- **Runtime Upgrade:** Upgraded the OpenClaw runtime from `v2026.4.14` to `v2026.6.1` (PR #2209).
- **New Feature:** Added "Plan Mode" workflow for the Cowork (collaborative agent) system (PR #2183).
- **Fix:** Patched the OpenClaw integration to support an upgraded instant messaging plugin.

**Breaking Changes & Migration Notes:** No breaking changes or migration steps were reported for this release. It is a drop-in upgrade.

### 3. Project Progress
Eight PRs were merged today, reflecting strong forward momentum across several areas:

- **Core & Cowork (Multi-Agent):**
    - **Runtime Upgrade:** Successful upgrade of the OpenClaw runtime to `v2026.6.1`, which includes associated plugin and build pipeline changes ([PR #2209](https://github.com/netease-youdao/LobsterAI/pull/2209)).
    - **Subagent Stability:** Fixed a significant bug where subagent progress (e.g., "5/5" steps) was incorrectly frozen or stale in the sidebar. Progress is now derived from local state rather than unreliable model-authored text. Also fixed the duration display for finished subagents ([PR #2207](https://github.com/netease-youdao/LobsterAI/pull/2207), [PR #2208](https://github.com/netease-youdao/LobsterAI/pull/2208)).

- **UI/UX & Rendering:**
    - **Mermaid Diagrams:** Two fixes prevent Mermaid-rendered error SVGs from "leaking" into the document and creating visual artifacts ([PR #2210](https://github.com/netease-youdao/LobsterAI/pull/2210), [PR #2213](https://github.com/netease-youdao/LobsterAI/pull/2213)).
    - **Skill Search:** Fixed a UX bug where the skill selection menu closed unintentionally when the user's focus was still in the search input ([PR #2212](https://github.com/netease-youdao/LobsterAI/pull/2212)).
    - **Legacy Skill Tooltip:** A long-dormant PR (from April) was revived and merged, adding a rich tooltip that shows the full skill description on hover ([PR #1459](https://github.com/netease-youdao/LobsterAI/pull/1459)).

### 4. Community Hot Topics
The community discussion is centered around the evolution of the project's agent architecture.

- **[Issue #1462 (Closed): Request for Per-Agent Model Binding and Group Mode](https://github.com/netease-youdao/LobsterAI/issues/1462)**
    - **Analysis:** This is the most significant community discussion to date regarding the future of the Cowork system. The user requests two features: 1) allowing each agent to use a different model, and 2) a "room" or "group" pattern with a manager agent that can delegate tasks. This was marked as stale and closed, but the explicit reference to "multi-agent collaboration" and the fact that PRs for Cowork stability were merged today suggests the maintainers are actively building the infrastructure for this request, even if the issue itself was closed.

### 5. Bugs & Stability
One high-severity bug was reported today.

- **[Issue #2214 (High Severity): Desktop "Data Backup" Causes Main Process Freeze](https://github.com/netease-youdao/LobsterAI/issues/2214)**
    - **Description:** The "Data Backup" feature in the settings causes a 100% reproducible freeze on Windows 11, requiring the user to force-kill the process. The user analysis points to a potential issue with how the Electron app handles large SQLite databases (71.6 MB) in WAL mode during the `backup()` API call.
    - **Status:** **No fix PR has been opened yet.** This is a critical stability issue that needs immediate maintainer attention.

### 6. Feature Requests & Roadmap Signals
- **Multi-Agent Orchestration:** The closed issue #1462, combined with today's merged PRs on Cowork subagent stability and the new "Plan Mode," strongly signals that the roadmap is moving toward a more formal multi-agent orchestration system. The next step is likely implementing per-agent model binding and a manager pattern.
- **Enhanced Artifact Handling:** The series of fixes for Mermaid diagram rendering suggest the team is focused on improving the reliability of the "Artifacts" feature (renderable content like charts and diagrams).

### 7. User Feedback Summary
- **Positive:** Users (like `orion0608`) express strong satisfaction with the current product, stating that "the interaction experience of Lobster AI is far better than that of its competitors."
- **Pain Points:**
    - **Stability:** The data backup freeze (Issue #2214) is a critical pain point that directly affects data safety for power users.
    - **Agent Flexibility:** There is a clear and articulate demand for more advanced multi-agent collaboration (per-agent models, manager/worker patterns). Users see this as the next logical evolution.
    - **Database Performance:** The reported crash hints that users with large databases (100k+ messages) are encountering edge cases in the app's I/O handling.

### 8. Backlog Watch
- **[Issue #1462 (Closed): Request for Multi-Agent Features](https://github.com/netease-youdao/LobsterAI/issues/1462)**
    - **Status:** Closed as stale, but its content is roadmap-relevant. The maintainers should consider either re-opening it or creating a new tracking issue linked to the upcoming Cowork features to keep the community informed.
- **[Issue #2214 (Open): Data Backup Freeze](https://github.com/netease-youdao/LobsterAI/issues/2214)**
    - **Status:** New, urgent, and unaddressed. This requires a quick response (acknowledgment) and a fix PR in the next 1-2 days to maintain user trust in the desktop client's reliability.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-27

## Today's Overview
The Moltis project saw minimal activity in the last 24 hours, with no new issues, releases, or merged pull requests. A single open pull request (#1135) was updated, proposing a feature for optional auto-screenshots after browser actions. The project currently has zero open or active issues, which may indicate either a mature, stable codebase or a temporary lull in community engagement. Overall, activity is very low today, with no changes to the codebase or new releases to report.

## Releases
*None*. No new versions were released in the last 24 hours.

## Project Progress
No pull requests were merged or closed today. The only activity was an update to an existing open PR.

## Community Hot Topics
- **PR #1135** (open): *browser: optional auto-screenshot after each action*  
  Author: resumeparseeval | Created: 2026-06-26 | Updated: 2026-06-26 | 0 comments | 0 reactions  
  [View PR](https://github.com/moltis-org/moltis/pull/1135)  
  This PR proposes capturing a screenshot automatically after each state-changing browser action and attaching it to the tool result. The underlying need appears to be improving the user experience for chat clients that require a per-step visual timeline. This is a feature enhancement targeting the browser module, likely driven by users who need better debugging or visual feedback during agent interactions.

## Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. No fix PRs are in progress.

## Feature Requests & Roadmap Signals
- **PR #1135** is effectively a feature request implemented as a pull request: auto-screenshots after browser actions. This suggests users or contributors want richer visual feedback from browser-based agent operations. If accepted, this feature could be expected in the next minor release, as it adds optional functionality without breaking existing behavior.

No other feature requests were recorded today.

## User Feedback Summary
With zero new issues and no merged PRs, there is no user feedback data to report from the last 24 hours. The lack of filed issues may indicate general user satisfaction or that users have not encountered blocking problems.

## Backlog Watch
No long-unanswered issues or PRs were identified. The only open PR (#1135) is less than 24 hours old and awaiting maintainer review. No items in the backlog currently require urgent attention.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-27

## 1. Today's Overview

CoPaw shows **very high activity** today with 29 issues and 50 PRs updated in the last 24 hours, signaling intense development momentum. The project has cut **v2.0.0-beta.1**, a major early beta release that migrates the underlying framework to AgentScope 2.0, though it carries breaking changes and instability warnings. Nine issues were closed and 24 PRs were merged/closed, reflecting a healthy merge velocity, while 20 open issues and 26 open PRs indicate sustained community contribution and ongoing development. The activity spike around channel integrations (WeCom, DingTalk, Feishu) and desktop reliability suggests the team is prioritizing production readiness ahead of a stable 2.0 release.

## 2. Releases

**v2.0.0-beta.1** was released today ([release page](https://github.com/agentscope-ai/CoPaw/releases/tag/v2.0.0-beta.1)).

- **⚠️ Breaking changes and instability expected** — early beta for developers and early adopters only; not recommended for production.
- **Key change**: `refactor: migrate agent` — the core agent framework has been migrated to AgentScope 2.0, which brings a completely rewritten memory manager (ReMe4) and significant architectural changes.
- **Installation note**: A release verification issue ([#5571](https://github.com/agentscope-ai/CoPaw/issues/5571)) is tracking platform installation checks.
- **No migration guide provided** in the release notes; existing users of v1.1.x should expect breaking changes in configuration, plugin APIs, and skill definitions.

## 3. Project Progress

Major work was merged or closed today across three key areas:

### AgentScope 2.0 Migration Cleanup
- **PR #5440** (merged, +4/-1493 lines): "Ponytail cleanup" fixing 3 post-merge bugs — `CancelledError` not being swallowed, Python 3.12 compatibility for `datetime.utcnow`, and a SQLite connection leak.
- **PR #5265** (merged): Graceful shutdown endpoint for desktop + Tauri lifecycle fix, resolving conflicts with AgentScope 2.0's rewritten memory manager.
- **PR #5153** (merged): Replicated Tauri instant-window startup optimization to the pywebview Windows client, reducing startup blank time from 10-30s.

### Feature Advances
- **PR #5297** (merged): Batch test and batch delete models in the provider management UI (`POST /{provider_id}/models/batch-test` and `POST /{provider_id}/models/batch-delete`).
- **PR #5436** (merged): Drag-and-drop file upload onto the chat sender area.
- **PR #5321** (open, under review): "Scroll" context management strategy — a retrieval-driven alternative to native compression that persists full conversation history to SQLite with on-demand recall.

### Desktop and Plugin Fixes
- **PR #5570** (open): Fixes plugin dependency install storms and orphaned backend processes (fixes #5550) — a critical memory leak on macOS desktop.
- **PR #5536** (open, under review): Kills orphaned Chrome renderer processes on browser stop (fixes #5520).
- **PR #5568** (open): Fixes all 5 official plugins failing to install on CoPaw 2.0 due to AgentScope 2.x breaking changes.

## 4. Community Hot Topics

### Most Active Issues
1. **#5262** — "[Bug]: 每次升级之后，被禁用的内置技能又会重新变回启用" *(12 comments, CLOSED)*  
   User frustration with built-in skills re-enabling after every upgrade. The fix was likely included in v2.0.0-beta.1's skill persistence changes.  
   [Link](https://github.com/agentscope-ai/CoPaw/issues/5262)

2. **#5379** — "[Bug]: 通过Python命令安装后启动，直接报错Internal Server Error" *(7 comments, OPEN)*  
   Fresh Python install fails with `get_remote_addr(transport)` error. A critical onboarding blocker affecting new users.  
   [Link](https://github.com/agentscope-ai/CoPaw/issues/5379)

3. **#5563** — "[Feature]: 建议优化多步骤回复的消息聚合" *(5 comments, OPEN)*  
   Strong user demand for message aggregation — agents sending 10+ fragmented message cards per task. Directly addressed by PR #5577 (open today).  
   [Link](https://github.com/agentscope-ai/CoPaw/issues/5563)

4. **#5480** — "[Bug]: Console 长消息排版错乱 — 切换选项卡后恢复" *(5 comments, CLOSED)*  
   CSS layout calculation bug causing Markdown rendering issues on long messages. Fixed via frontend re-render optimization.  
   [Link](https://github.com/agentscope-ai/CoPaw/issues/5480)

5. **#5550** — "Bug: Remote SSH 插件依赖安装循环 + 旧 backend 进程残留" *(4 comments, OPEN)*  
   Two compounding bugs causing `pip install` storms and memory exhaustion. PR #5570 opened to fix both.  
   [Link](https://github.com/agentscope-ai/CoPaw/issues/5550)

### Key Insight
The community is heavily focused on **stability after upgrade** (skills re-enabling, install crashes, layout bugs) and **channel integration quality** (WeCom file handling, DingTalk @mention support, Feishu long message delivery). User #tecgic is particularly active, filing 4 detailed feature requests and even creating a community skill to help others write better GitHub Issues ([#5567](https://github.com/agentscope-ai/CoPaw/issues/5567)).

## 5. Bugs & Stability

### High Severity
| Issue | Description | Fix Status |
|-------|------------|------------|
| **#5550** | Remote SSH plugin dependency install loop + orphaned backend processes (memory leak) | PR #5570 open |
| **#5520** | `browser_use stop()` leaves Chrome renderer processes running (memory leak, regression) | PR #5536 open |
| **#5379** | Fresh Python install → Internal Server Error on first launch | OPEN |
| **#5554** | WeCom file messages silently dropped after download | OPEN |
| **#5328** | DeepSeek agent gets stuck in thinking state, requires manual intervention | OPEN |

### Medium Severity
- **#5573** — DeepSeek V4 thinking mode fails on OpenAI-compatible endpoints with 400 errors (schema null type + missing `reasoning_content`). PR #5549 addresses the schema issue.
- **#5543** — `functionDeclaration` schema emitting `"type":"null"` blocks third-party model relays. PR #5549 fixes this.
- **#5539** — Heartbeat task hard-coded 120s timeout causes premature cancellation. PR #5557 makes timeout configurable (default 300s).
- **#5556** — Source install fails because `reme-ai 0.4.0.4` not on PyPI.
- **#5561** — Feishu bot fails to deliver long messages.

### Low Severity / UX
- **#5401** (CLOSED) — Console frontend crashes on sessions with large tool-use history.
- **#4865** — No streaming render for `write_file` tool calls, causing apparent UI freeze.
- **#5575** — Media-only messages require text to send in WeCom (PR #5575 adds configurable debounce).

## 6. Feature Requests & Roadmap Signals

### Likely to Ship in Next Release
1. **Message aggregation** ([#5563](https://github.com/agentscope-ai/CoPaw/issues/5563)) → PR #5577 adds opt-in `aggregate_message_replies` channel setting. *High confidence.*
2. **Heartbeat timeout configuration** ([#5539](https://github.com/agentscope-ai/CoPaw/issues/5539)) → PR #5557 adds `timeoutSeconds` field with 300s default. *Nearly merged.*
3. **No-text debounce toggle** ([#5554](https://github.com/agentscope-ai/CoPaw/issues/5554) / [#5558](https://github.com/agentscope-ai/CoPaw/issues/5558)) → PR #5575 adds `no_text_debounce_enabled` config. *High confidence.*
4. **DingTalk @mention support** ([#5564](https://github.com/agentscope-ai/CoPaw/issues/5564)) — In channels send CLI and API. *Medium confidence.*

### Community-Requested Features (Lower Priority)
- **Computer use support** ([#5551](https://github.com/agentscope-ai/CoPaw/issues/5551)) — Whether CoPaw plans to support computer-use agents. No maintainer response yet.
- **Automatic model fallback** ([#5572](https://github.com/agentscope-ai/CoPaw/issues/5572)) — Fallback when primary model quota exhausted or times out.
- **OpenAI Responses API support** ([#3993](https://github.com/agentscope-ai/CoPaw/issues/3993), CLOSED) — Rejected as out of scope for current architecture.
- **Silent cron execution** ([#5566](https://github.com/agentscope-ai/CoPaw/issues/5566)) — Agent can't run cron tasks without producing channel notifications.
- **Session ID exposure in plugin tools** ([#5547](https://github.com/agentscope-ai/CoPaw/issues/5547)) — Needed for multitenant auth in MCP tools.

### Roadmap Signal
The v2.0.0-beta.1 release and rapid AgentScope 2.0 cleanup (PR #5440, PR #5265) indicate the team is pushing hard toward a **stable 2.0 release**. The pattern of fix PRs opened the same day as bug reports (e.g., #5500 → #5570, #5520 → #5536, #5543 → #5549) suggests a responsive maintainer team prioritizing recent regressions.

## 7. User Feedback Summary

### Pain Points (Repeated Across Issues)
- **Upgrade friction**: Skills re-enable, configs break, fresh installs crash — multiple users report frustration with upgrade process reliability.
- **Channel reliability**: WeCom file handling broken, Feishu long messages lost, DingTalk lacks @mention — enterprise users clearly evaluating CoPaw as a production bot platform.
- **Agent thinking stalls**: DeepSeek users report agent "thinking" forever without action, requiring manual intervention — a specific model integration issue.
- **Visual feedback**: No streaming for file writes / long tool calls — users can't distinguish "still working" from "crashed".
- **Mac desktop memory**: Remote SSH plugin can trigger fork-bomb-like memory exhaustion on Apple Silicon.

### Positive Signals
- User #tecgic created a community skill to help others write proper GitHub Issues — shows investment in the project's health.
- Multiple first-time contributors submitting PRs (niceIrene, mynameyi, C1-BA-B1-F3) — healthy contributor pipeline.
- Users are deploying CoPaw in complex enterprise scenarios (CAD file parsing, PLM integration, multitenant auth) — indicates production trust despite beta status.

## 8. Backlog Watch

### Issues Needing Maintainer Attention
| Issue | Age | Problem | Why Urgent |
|-------|-----|---------|------------|
| **#5379** | 5 days | Python install → Internal Server Error | Blocks all new users installing via pip |
| **#5328** | 8 days | DeepSeek agent thinking stall | Affects DeepSeek users (growing user base) |
| **#4865** | 26 days | No streaming for write_file calls | UX regression; 2 thumbs-up from community |
| **#5554** | 1 day | WeCom file processing silently dropped | Enterprise WeCom users blocked |
| **#5547** | 1 day | No session ID in plugin tools | Blocks enterprise multitenant deployments |

### Key Risks
- **v2.0.0-beta.1 adoption cliff**: 5 official plugins confirmed broken on 2.0 (PR #5568). Without quick plugin fixes, early adopters will hit a wall.
- **Memory leak cascade**: Two separate memory leak issues (#5520 Chrome processes, #5550 SSH plugin) on macOS desktop — could erode user confidence in desktop client.
- **New contributor abandonment**: PR #5321 (scroll context manager) has been under review for 8 days with no maintainer comments — risk of first-time contributor frustration.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-27

## Today's Overview

ZeroClaw sees high development velocity today with **50 issues and 50 PRs updated** in the last 24 hours, alongside a new **v0.8.2 release**. The project maintains a healthy balance of 44 open/active issues and 39 open PRs, with 6 issues and 11 PRs resolved. Activity concentrates on **supply-chain security hardening** (SLSA provenance, SBOM generation, cosign signing), **runtime stability** for the release train toward v0.8.3, and a structured **GST extraction feature** being broken down into clean user-story issues by a new contributor. The release of v0.8.2 introduces agent-to-agent discovery and a richer skills system, signaling a strategic push toward interoperability.

---

## Releases

### v0.8.2 (Released 2026-06-26 or earlier, included in today’s data)
**Key additions:**
- **A2A agent discovery** — agent-to-agent interop via the A2A protocol, enabling agents to find and communicate with each other.
- **Richer skills system** — user-configured extra registries, typed slash-command options for better skill management.
- **Security posture sharpened** across plugins, channels, and the runtime.

**Breaking changes:** Not explicitly documented in the release notes shown. Migration guidance expected in the full changelog.

---

## Project Progress

### Closed/Merged PRs (11 resolved today, selected highlights):
- **[PR #8158](https://github.com/zeroclaw-labs/zeroclaw/pull/8158)** — Added CycloneDX SBOM generation for Rust and npm (Rust crate: `cargo-cyclonedx`, npm: `npm sbom`). A direct implementation of supply-chain security RFC #7675 Phase 2.
- **[PR #8146](https://github.com/zeroclaw-labs/zeroclaw/pull/8146)** — Fixed CLI one-shot runs losing telemetry and token totals on exit; ensures OTLP exporters flush before process termination.

### Resolved Issues (6 closed today, selected):
- **[Issue #5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844)** — Memory prioritization bug: system prompt gave excessive weight to memories over current prompt; now fixed.
- **[Issue #4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879)** — Gemini CLI OAuth failing after authentication (rate-limit error loop); resolved.
- **[Issue #6434](https://github.com/zeroclaw-labs/zeroclaw/issues/6434)** — Shell tool calls refused at `autonomy = "full"`; dispatch never reached runtime; fix applied.
- **[Issue #8047](https://github.com/zeroclaw-labs/zeroclaw/issues/8047)** — `ReadSkillTool` looked in wrong directory; skills now correctly found in agent workspace.

### Notable PRs still open (showing active development):
- **[PR #6893](https://github.com/zeroclaw-labs/zeroclaw/pull/6893)** — Multi-database session backends (Postgres, Oracle, MySQL, Db2) for fleet-wide session sharing.
- **[PR #8033](https://github.com/zeroclaw-labs/zeroclaw/pull/8033)** — Two-path onboard tree (LLM + deterministic), end-to-end over RPC and CLI.
- **[PR #8380](https://github.com/zeroclaw-labs/zeroclaw/pull/8380)** — Offline pricing catalog + cost/org RPC for air-gapped deployments, complementing live gateway pricing (#8233).

---

## Community Hot Topics

### Most Active Issues (by comment count):

1. **[RFC: Work Lanes, Board Automation, and Label Cleanup (#6808)](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)** — 11 comments. A governance RFC proposing work lanes to route issues without manual board maintenance. Accepted and in rollout. The high engagement reflects community desire for **structured project management automation**.

2. **[RFC: Supply chain signing — hardware PGP, hermetic builds, SLSA provenance (#8177)](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)** — 9 comments. Proposes hardware-backed PGP, multi-party quorum offline signing. High risk, blocked on maintainer review. Community is actively debating **security hardening for release artifacts**.

3. **[Bug: Too much emphasis on memory (#5844)](https://github.com/zeroclaw-labs/zeroclaw/issues/5844)** — 7 comments. Now closed and fixed. Users reported agents in cron jobs prioritizing old memories over fresh prompts. The fix here is **directly responsive to operational pain**.

4. **[Bug: Prompt Caching not working with Telegram (#6360)](https://github.com/zeroclaw-labs/zeroclaw/issues/6360)** — 4 comments, open. CLI caching works; Telegram forces full re-processing. Underlying need: **consistent performance across channels**.

5. **[Bug: Gemini CLI OAuth fails (#4879)](https://github.com/zeroclaw-labs/zeroclaw/issues/4879)** — 4 comments, now closed. User frustration with auth loop after success; resolution is a win for **provider onboarding UX**.

### Most Active PRs (today’s updates):
- **[PR #8336](https://github.com/zeroclaw-labs/zeroclaw/pull/8336)** — Nix build repair, adding hash updates to release process. **Community need:** Nix users blocked by broken builds.
- **[PR #8381](https://github.com/zeroclaw-labs/zeroclaw/pull/8381)** — Fixes unwrap panic in `hardware_memory_read` chip lookup. Small but important **stability fix**.

---

## Bugs & Stability

### Critical Bugs (Priority P1, Risk High):

| Issue | Summary | Status | Fix Available? |
|-------|---------|--------|----------------|
| [#6434](https://github.com/zeroclaw-labs/zeroclaw/issues/6434) | Shell tool refused at `autonomy = "full"` | **Closed/fixed** | ✅ |
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) | Gemini OAuth not working | **Closed/fixed** | ✅ |
| [#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) | Memory over-prioritization | **Closed/fixed** | ✅ |
| [#8312](https://github.com/zeroclaw-labs/zeroclaw/issues/8312) | `fill-translations leak-repair` leaves stale entries that re-ship leaked text via `write_po` | **Open** | No fix PR yet |
| [#7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733) | `mcp_bundles` parsed but never enforced — per-agent MCP scoping is a silent no-op | **Open** | **[PR #8370](https://github.com/zeroclaw-labs/zeroclaw/pull/8370)** — regression test for fix; production fix already landed on master |

### Degraded Behavior (P2, Risk Medium-High):
- **[#6360](https://github.com/zeroclaw-labs/zeroclaw/issues/6360)** — Telegram prompt caching broken; no fix PR yet.
- **[#7800](https://github.com/zeroclaw-labs/zeroclaw/issues/7800)** — ZeroCode keybindings misleading/unreachable on macOS.
- **[#8366](https://github.com/zeroclaw-labs/zeroclaw/issues/8366)** — Heartbeat engine reads `HEARTBEAT.md` from wrong directory.
- **[#8275](https://github.com/zeroclaw-labs/zeroclaw/issues/8275)** — Scoop manifest missing `zerocode.exe` shim (P3, minor).

**Overall stability trend:** Three high-impact bugs closed today signals the team is **actively reducing the P1 backlog**. Two open P1 bugs remain, but one (#7733) already has a production fix landed.

---

## Feature Requests & Roadmap Signals

### New Features Requested Today:
1. **[#8379](https://github.com/zeroclaw-labs/zeroclaw/issues/8379)** — Opt-in passive group context for WhatsApp Web: stores unaddressed group messages as context without triggering agent turns. **Likely for v0.8.4** given WhatsApp channel maturity.

2. **[#8378](https://github.com/zeroclaw-labs/zeroclaw/issues/8378) – #8372** — **GST extraction feature series** (7 issues from `arun-raze19`): A structured vertical feature for DMS (Dealer Management System) → GST-compliant document generation. Covers sales extraction, invoice generation, GSTR-1/3B return packs, validation, audit trails, and doc polish. **Likely for v0.8.4 or later** — appears to be a commercial/enterprise vertical.

3. **[#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)** — RFC: Goal mode for bounded autonomous session work (one user objective until completion/depletion). Accepted. **Likely for v0.8.3** — aligns with the runtime stability tracker.

### Roadmap Signals:
- **v0.8.3** tracked in **[#8071](https://github.com/zeroclaw-labs/zeroclaw/issues/8071)** — Focus on runtime, agent loop, tool execution, memory, daemon, cron, skills, execution stability.
- **Goal mode** (#8303) is an accepted RFC and may land in v0.8.3.
- **Multi-database session backends** (#6893) — large PR, still open, may land in v0.9.0.

---

## User Feedback Summary

### Real Pain Points (expressed in open issues):
- **Telegram users:** Prompt caching broken (#6360), reply-to-bot ignored in groups (#5866). Both signal **inconsistent channel parity**.
- **macOS users:** ZeroCode keybindings misleading/unreachable (#7800). Platform-specific UX friction.
- **Scoop users:** `zerocode.exe` missing from PATH (#8275). Minor but affects onboarding on Windows.
- **Gemini users:** OAuth rate-limit loop after successful auth (#4879, now fixed). **Provider integration quality** was a sore point, now resolved.
- **Memory system:** Over-prioritization of old memories (#5844, fixed) — users wanted **fresh context prioritization**.

### Positive Signals:
- The **GST extraction feature series** (#8372–#8379) from a contributor suggests **active enterprise use cases** driving feature development.
- The slow but steady progress on **supply-chain security** (SBOM, cosign, SLSA) indicates the project values **production-grade integrity**.

---

## Backlog Watch

### Issues Needing Maintainer Attention:

| Issue | Age | Status | Why It Matters |
|-------|-----|--------|----------------|
| [#7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733) (mcp_bundles not enforced) | 12 days (since 2026-06-15) | Accepted, production fix landed but still open as bug | **Security isolation silent no-op** — high risk, critical for multi-agent deployments |
| [#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) (Supply chain signing RFC) | 5 days | Blocked, needs-maintainer-review | **High-risk security RFC** with 9 comments; community invested |
| [#8309](https://github.com/zeroclaw-labs/zeroclaw/issues/8309) (SkillForge orphaned) | 2 days | Blocked, needs-maintainer-review | Orphaned feature from February 2026; needs decision (wire or remove) |
| [#8312](https://github.com/zeroclaw-labs/zeroclaw/issues/8312) (leak-repair stale entries) | 2 days | Open, no PR | **Data-loss path** — narrow trigger but affects translation tooling |
| [#6754](https://github.com/zeroclaw-labs/zeroclaw/issues/6754) (ACP bridge auto-pairing fragile) | 40 days | Accepted, no-stale | **Gateway bridge reliability** — operator workflow blocker |

### PRs Needing Review:
- **[PR #6893](https://github.com/zeroclaw-labs/zeroclaw/pull/6893)** — Multi-database session backends (34 days open, size:XL). Large but strategic for fleet deployments.
- **[PR #7361](https://github.com/zeroclaw-labs/zeroclaw/pull/7361)** — Per-turn output routing via `send_via` + voice delivery fixes (20 days open, size:XL). Spans many channels — coordination-heavy.

---

**Overall Assessment:** ZeroClaw’s health is **strong and accelerating**. The v0.8.2 release opens interoperability and skills fronts. Bug closure rate (3 P1s closed today) outpaces new high-severity reports. The GST feature series from a contributor and the active RFC discussion signal **growing enterprise adoption**. Key risk areas: **MCP scoping security gap** (#7733) is the highest-priority open issue despite the fix being landed; **SkillForge orphan** needs a maintainer decision to avoid dead code.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*