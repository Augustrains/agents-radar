# OpenClaw Ecosystem Digest 2026-08-03

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-03 01:25 UTC

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

Based on the provided GitHub data for OpenClaw, here is the project digest for 2026-08-03.

---

# OpenClaw Project Digest - 2026-08-03

## 1. Today's Overview

OpenClaw's development activity remains exceptionally high, with a massive volume of 500 Issues and 500 PRs updated in the last 24 hours. The project is in a heavy maintenance and bug-fixing phase, with a significant focus on stability, session-state integrity, and message-delivery reliability, as evidenced by the clustering of `P1` bugs and `diamond lobster` ratings. A new beta release, `v2026.7.2-beta.7`, has been published, highlighting substantial work on state safety and crash recovery. While the influx of issues is high, the volume of activity from both human maintainers and automated `clawsweeper[bot]` indicates a rapid response cycle to address these concerns in the upcoming stable release.

## 2. Releases

- **v2026.7.2-beta.7** ([Link](https://github.com/openclaw/openclaw/releases))
  - **Highlights:**
    - **State safety and recovery:** This is a major theme of this release. It introduces a quarantine store to protect persisted data from primary-database damage, crash-recoverable SQLite snapshots, crash-durable filesystem publication, and schema-upgrade data-loss rejection. A rollback-writer snapshot recovery mechanism has also been implemented.
  - **Potential Migration Notes:** Due to the extensive changes to state persistence and database handling, users should carefully review the upgrade process. Pay special attention to any schema migration warnings, as the new version is designed to reject data-loss scenarios.

## 3. Project Progress

The last 24 hours saw a high number of PRs being merged or closed (160). The most prominent areas of advancement and fixes include:

- **UI/UX Fixes:** Merging a PR to keep the web chat's Send and Stop buttons responsive on mobile, resolving a significant user friction point ([PR #116104](https://github.com/openclaw/openclaw/pull/116104)).
- **Reliability & Bug Fixes:** A critical fix was merged to properly skip invalid location messages in the LINE channel, preventing potential API crashes ([PR #118064](https://github.com/openclaw/openclaw/pull/118064)).
- **Automated Maintenance:** A significant number of fixes are being generated and pushed by `clawsweeper[bot]`, addressing issues like preserving CLI side-question mode for commitments ([PR #118339](https://github.com/openclaw/openclaw/pull/118339)) and fixing Google embedding provider aliases (`google` -> `gemini`) for memory search ([PR #117976](https://github.com/openclaw/openclaw/pull/117976)).
- **Core Agent Behavior:** New PRs have been opened to address critical agent behavior, such as restoring channel replies after a failed final tool call ([PR #118344](https://github.com/openclaw/openclaw/pull/118344)) and surfacing `sessions_yield` waiting status to users to avoid silent parent turns ([PR #117509](https://github.com/openclaw/openclaw/pull/117509)).

## 4. Community Hot Topics

The most active discussions highlight major pain points around reliability, silence, and state management.

- **#116277: DeepSeek v4 Flash silent reply failure** (88 comments) - This is by far the most active thread. Users are reporting that the model silently fails to generate replies and posts a generic fallback message in Telegram. The underlying need is for better error detection, retry mechanisms, and transparency when a model fails. [Link](https://github.com/openclaw/openclaw/issues/116277)
- **#116201: Realtime voice work can retain unbounded provider and consult state** (50 comments) - This issue discusses memory leaks and unbounded resource retention in real-time voice sessions. It suggests a need for hard ownership bounds and better cleanup to prevent stalls and excessive memory usage. [Link](https://github.com/openclaw/openclaw/issues/116201)
- **#115326: Crash-loop breaker suppresses Discord/WhatsApp permanently** (26 comments) - A high-impact bug where the crash-loop breaker permanently disables channels and the documented recovery path fails. This is a critical reliability issue causing complete communication loss. [Link](https://github.com/openclaw/openclaw/issues/115326)
- **#117956: claude-cli backend metered Anthropic API usage despite scrub** (10 comments) - A serious privacy/security concern where OpenClaw's `claude-cli` backend billed ~13.7M tokens to a user's Anthropic account despite attempts to scrub the API key. This is a major trust-breaking issue. [Link](https://github.com/openclaw/openclaw/issues/117956)

## 5. Bugs & Stability

This is the dominant theme of the digest. Several `P1` and `diamond lobster`-rated bugs are active, with a particular focus on session state, message loss, and crash loops.

- **Critical (Crash/Loop):**
    - **#117956: `claude-cli` backend leaked API usage** - Highest severity due to the financial and security implications. No fix PR is currently linked. [Link](https://github.com/openclaw/openclaw/issues/117956)
    - **#115326: Crash-loop breaker permanently suppresses Discord/WhatsApp** - Causes total channel outage. Closed, with fix likely in the new `v2026.7.2-beta.7` quarantine store work. [Link](https://github.com/openclaw/openclaw/issues/115326)
    - **#115424: Gateway V8 heap OOM during main-session turn, causing a 7-core-dump loop** - A severe crash that cascades into a loop. No fix PR is currently linked. [Link](https://github.com/openclaw/openclaw/issues/115424)
    - **#115908: Session transcript projection livelock blocking the main thread** - Can stall all channels for tens of seconds. No fix PR is currently linked. [Link](https://github.com/openclaw/openclaw/issues/115908)

- **High (Message Loss / State):**
    - **#116277: DeepSeek v4 Flash silent reply failure** - Active and heavily discussed. No fix PR is currently linked. [Link](https://github.com/openclaw/openclaw/issues/116277)
    - **#115700: `chat.send` rejected with "thread switched branches"** - Persistent rejection requires workaround. A linked PR exists to fix this. [Link](https://github.com/openclaw/openclaw/issues/115700)
    - **#116010: All persistent sessions capped at 128k context** - Ignores model capabilities, severely limiting sessions. A linked PR exists. [Link](https://github.com/openclaw/openclaw/issues/116010)
    - **#115037: Synthetic "No response requested." triggers downgrade to fallback model** - Silently serves users with a worse model. No fix PR is currently linked. [Link](https://github.com/openclaw/openclaw/issues/115037)

- **Fix PRs in progress:** New PRs are actively being submitted for these issues, including for restoring replies after failed tool calls ([#118344](https://github.com/openclaw/openclaw/pull/118344)), fixing Slack presence polling hangs ([#117478](https://github.com/openclaw/openclaw/pull/117478)), and preserving context-window-limited responses from Claude ([#117748](https://github.com/openclaw/openclaw/pull/117748)).

## 6. Feature Requests & Roadmap Signals

Several feature requests point toward improving user control, observability, and platform parity.

- **SDK Stabilization:** The continuous discussion around improving and stabilizing the `@openclaw/sdk` for external app clients ([SDK Issue #74704](https://github.com/openclaw/openclaw/issues/74704), [ACP fixes](https://github.com/openclaw/openclaw/issues/52249)) is a strong signal that the project is maturing its developer platform.
- **Enhanced Observability:** The desire for better tracing context fields in plugin hooks ([Issue #50291](https://github.com/openclaw/openclaw/issues/50291)) and surfacing resolved provider names ([Issue #51441](https://github.com/openclaw/openclaw/issues/51441)) suggests a push for more profound debugging and management capabilities.
- **Platform Parity & Control:** Requests for multi-bot support for Microsoft Teams ([Issue #71058](https://github.com/openclaw/openclaw/issues/71058)), and OpenAI Realtime (speech-to-speech) in Talk Mode ([Issue #71195](https://github.com/openclaw/openclaw/issues/71195)) show a desire for feature parity across channels.
- **User Configurability:** A significant number of requests are for making existing behaviors configurable, such as upload size limits ([Issue #71142](https://github.com/openclaw/openclaw/issues/71142)), persistent task-status surfaces ([Issue #52640](https://github.com/openclaw/openclaw/issues/52640)), and always-visible tools via `alwaysVisibleTools` ([PR #118335](https://github.com/openclaw/openclaw/pull/118335)).

## 7. User Feedback Summary

The overall sentiment appears to be a mix of frustration and high engagement. Key trends include:

- **High Frustration with Reliability:** The most common pain points are silent message failures, crashes, and message loss, which directly impact users' ability to rely on the agent for daily tasks. The lengthy, complex issues with detailed logs show users are deeply invested in diagnosing these problems but are clearly affected by them.
- **Concern Over Unexpected Costs:** The `claude-cli` billing issue ([#117956](https://github.com/openclaw/openclaw/issues/117956)) is a major source of dissatisfaction, stemming from a breakdown of trust and unexpected financial impact.
- **Value in Community & Automation:** The rapid response and fixes from `clawsweeper[bot]` suggest that the project's automation is effectively addressing some issues, but they also generate a large volume of PRs that require maintainer review, potentially creating a bottleneck.
- **Desire for Clarity and Control:** Users are requesting clearer error messages, better sorting in the UI, and more control over configuration, indicating a desire for a more mature, polished, and predictable product.

## 8. Backlog Watch

Several critical, long-standing issues remain open and require maintainer attention, often flagged with `clawsweeper:needs-maintainer-review` and `needs-product-decision`.

- **#67777: Subagent completion delivery can be lost** - Open since April, this core reliability issue continues to be a source of session-state and message-loss problems. [Link](https://github.com/openclaw/openclaw/issues/67777)
- **#47975: Subagent sessions persist after completion, main session becomes unresponsive** - Open since March, this is a major session-management bug that has not been resolved. [Link](https://github.com/openclaw/openclaw/issues/47975)
- **#47910: feat: provider fallback by failure class** - This long-running PR from March addresses a key architectural limitation in how providers are treated. It’s marked as `P1` and `diamond lobster`, indicating high importance, but still needs a maintainer decision. [Link](https://github.com/openclaw/openclaw/issues/47910)
- **#48786: Feishu: replied/quoted message mentions show as raw `@_user_N` placeholders** - This bug has been open since March and continues to degrade the experience for Feishu users. [Link](https://github.com/openclaw/openclaw/issues/48786)
- **#53408: Write/exec tool parameters silently dropped after long conversations** - A serious `P1` bug affecting agent autonomy, open since March and still awaiting a maintainer decision. [Link](https://github.com/openclaw/openclaw/issues/53408)

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-03

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is characterized by **intense reliability-focused development**, with the most active projects (OpenClaw, Hermes Agent, ZeroClaw) processing 50+ issues and PRs daily. A dominant theme across all projects is the tension between **feature velocity and production stability** — projects are investing heavily in session-state integrity, message-delivery reliability, and crash recovery, indicating a maturation from experimental toys to dependable daily-use tools. Security hardening is emerging as a critical differentiator, with projects like IronClaw and ZeroClaw actively addressing SSRF vectors, sandbox escapes, and credential leakage. The ecosystem is also converging on **standard API compatibility** (OpenAI Chat Completions profiles, MCP server support) as a key integration strategy, while multi-channel support (Telegram, Discord, Slack, Teams, Signal) has become table stakes rather than a differentiator.

---

## 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Release Status | Health Score (1-10) |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | v2026.7.2-beta.7 (new) | 7/10 — High activity, critical bugs being addressed |
| **Hermes Agent** | 50 | 50 | v2026.7.20 (stable, no new) | 7/10 — Healthy balance, security focus |
| **ZeroClaw** | 50 | 50 | v0.8.4 (new) | 7/10 — Active RFCs, security hardening |
| **IronClaw** | 7 | 26 | Release PR pending (breaking) | 8/10 — Excellent fix-per-issue velocity |
| **NanoClaw** | 1 | 10 | No new (pipeline fix merged) | 7/10 — Healthy, growing review queue |
| **PicoClaw** | 3 | 9 | No new (v0.3.1 latest) | 6/10 — Moderate, stale PRs concern |
| **NanoBot** | 0 | 9 | No new | 7/10 — Clean bill of health, PR queue active |
| **LobsterAI** | 3 | 6 | No new (2026.3.26 latest) | 4/10 — Stale backlog, no maintainer response |
| **CoPaw** | 2 | 3 | No new (QwenPaw 2.0.1) | 6/10 — Active fixes, no merges today |
| **Moltis** | 0 | 1 | No new | 7/10 — Quiet, feature development phase |
| **NullClaw** | 0 | 0 | — | N/A (no activity) |
| **TinyClaw** | 0 | 0 | — | N/A (no activity) |
| **ZeptoClaw** | 0 | 0 | — | N/A (no activity) |

---

## 3. OpenClaw's Position

**Advantages:**
- **Reliability engineering maturity:** OpenClaw is the only project with a dedicated quarantine store, crash-recoverable SQLite snapshots, and rollback-writer recovery — a level of state-safety investment unmatched by peers. The `clawsweeper[bot]` automation pipeline provides rapid fix generation and triage, giving it a **5-10x faster issue-to-fix cycle** than competitors.
- **Massive community engagement:** With 500 issues/PRs daily, OpenClaw has 10x the activity of its nearest competitor (Hermes Agent), indicating the largest developer and user base.
- **Provider breadth:** The beta release addresses a wide range of provider issues (DeepSeek, Gemini, Claude CLI, Google embeddings), showing commitment to multi-provider reliability.

**Technical Approach Differences:**
- OpenClaw uses an **automated bot-driven fix pipeline** (`clawsweeper[bot]`) — unique among peers, enabling parallel bug-fixing at scale.
- Focus on **session-state integrity as a core architectural principle** rather than treating it as an add-on.

**Community Size Comparison:**
| Metric | OpenClaw | Hermes Agent | ZeroClaw | NanoBot |
|---|---|---|---|---|
| Daily Issues | 500 | 50 | 50 | 0 |
| Daily PRs | 500 | 50 | 50 | 9 |
| Top Issue Comments | 88 (#116277) | 10 (#4335) | 17 (#6808) | N/A |

**Vulnerability:** The sheer volume of activity (500 issues daily) risks maintainer burnout and review bottlenecks. The `claude-cli` billing leak (#117956) is a **trust-breaking event** that competitors can exploit.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|---|---|---|
| **Session state integrity & continuity** | OpenClaw, Hermes Agent, NanoClaw, IronClaw | Cross-platform session sync, session data loss prevention, context persistence across devices |
| **Message delivery reliability** | OpenClaw, Hermes Agent, NanoClaw, IronClaw | Silent failures, duplicate sends, crash-loop suppression, delivery retry mechanisms |
| **Provider compatibility & fallback** | OpenClaw, NanoBot, Hermes Agent, ZeroClaw | Graceful fallback on API errors, provider-agnostic error handling, standardized API profiles |
| **Security hardening** | OpenClaw, ZeroClaw, IronClaw | Secret redaction, sandbox escapes, SSRF protection, credential management |
| **Docker/container deployment** | NanoClaw, ZeroClaw | SQLite lock contention, filesystem compatibility (VirtioFS), containerized stability |
| **Network-aware API design** | CoPaw, NanoClaw | Pagination, compression, payload size reduction for slow connections |
| **Cross-session search & linking** | NanoBot, Hermes Agent | Navigable chat history, cross-conversation context retrieval |
| **MCP server support** | Moltis, NanoClaw, CoPaw | Remote MCP servers, managed repository bundles, tool name validation |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target Users | Architecture |
|---|---|---|---|
| **OpenClaw** | Mass-market multi-channel assistant with heavy automation | General users, power users | Monolithic core with plugin ecosystem, bot-driven fixes |
| **Hermes Agent** | Desktop-first agent with strong UX | Desktop users, Windows-centric | Desktop GUI + gateway/session infrastructure |
| **ZeroClaw** | Security-hardened runtime with governance RFCs | Enterprise, security-sensitive | Modular runtime with sandbox isolation, RFC-driven governance |
| **IronClaw** | Delivery reliability & network security | Distribution/automation platforms | Rust-based Reborn architecture, durable delivery |
| **NanoBot** | WebUI-focused assistant | Developers, self-hosters | Lightweight Python, plugin system |
| **NanoClaw** | Multi-channel adapter breadth | Channel integrators | Adapter-based, Docker-first |
| **PicoClaw** | Lightweight embedded agent | Edge/IoT, resource-constrained | Minimal core, provider presets |
| **LobsterAI** | Enterprise IM integration | Chinese enterprise (DingTalk, Feishu) | IM-focused, cowork features |
| **CoPaw** | Qwen-powered assistant | Chinese AI users, MCP integrators | QwenPaw base, MCP compatibility |
| **Moltis** | MCP server management | MCP ecosystem builders | Git-driven MCP repository bundles |

---

## 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating (Active daily, high velocity)**
- **OpenClaw** — Highest activity; automation-driven rapid fixes; beta releases weekly. Risk: quality control under volume.
- **Hermes Agent** — Strong balance of features and fixes; security-focused contributors; desktop momentum.
- **ZeroClaw** — High RFC activity signals architectural evolution; v0.8.4 stabilizes while v0.9.0 takes shape.
- **IronClaw** — Excellent fix-per-issue velocity; QA-driven development; deeply technical.

**Tier 2: Healthy Maintenance/Growth**
- **NanoBot** — Zero open issues but active PRs; clean codebase; predictable release cycle.
- **NanoClaw** — Moderate activity; channel expansion; growing review queue.
- **PicoClaw** — Moderate; security hardening and provider expansion; review bottleneck evident.
- **CoPaw** — Reactive maintenance; strong report-fix pipeline.

**Tier 3: Low/Stabilizing**
- **LobsterAI** — 4+ months of stale items; no maintainer response; at risk of contributor attrition.
- **Moltis** — Feature development phase; minimal community engagement; maintainer-driven.

**Tier 4: Dormant**
- NullClaw, TinyClaw, ZeptoClaw — No activity; likely abandoned or in hibernation.

---

## 7. Trend Signals

1. **Reliability is the new feature:** Across OpenClaw, Hermes Agent, and IronClaw, the dominant theme is session-state integrity, message-delivery guarantees, and crash recovery. Users increasingly treat AI agents as mission-critical infrastructure, not toys.

2. **Security is a differentiator:** Projects investing in security (ZeroClaw's sandbox, IronClaw's SSRF protection, OpenClaw's credential redaction) are attracting security-conscious contributors and enterprise evaluations. The OpenClaw `claude-cli` billing leak is a cautionary tale — trust is fragile.

3. **API compatibility is the integration path:** RFCs for OpenAI Chat Completions profiles (ZeroClaw) and MCP server support (Moltis, NanoClaw, CoPaw) signal that agents must interop with the broader AI ecosystem rather than being walled gardens.

4. **Cross-platform continuity is a top unmet demand:** Users want seamless session state across CLI, desktop, and messaging channels (Hermes Agent's #4335 cluster with 22+ comments). No project has solved this yet — the first to do so wins multi-device power users.

5. **Provider fallback is a source of trust:** Silent failures (DeepSeek in OpenClaw, HTTP 400s in NanoBot) destroy user trust. Projects that implement deterministic, transparent fallback mechanisms will build stronger user loyalty.

6. **Automated maintenance is double-edged:** OpenClaw's `clawsweeper[bot]` enables scale but risks review bottlenecks. Projects must balance automation with human judgment.

7. **Network-aware design is neglected but critical:** CoPaw's MB-level payloads causing 30s timeouts highlight that many projects assume localhost or high-bandwidth deployment. Expect more projects to adopt pagination and compression as standard.

8. **Governance is emerging as a concern:** ZeroClaw's RFC-driven governance and Hermes Agent's duplicate-issue cluster (5+ issues on the same feature) suggest projects need better mechanisms for consolidating community demand and maintaining contributor momentum.

---

**Bottom Line:** The ecosystem is consolidating around reliability and security, with OpenClaw leading in scale and velocity but facing trust challenges. IronClaw's QA-driven approach and ZeroClaw's governance structure are models worth emulating. For developers, the highest-value opportunities lie in solving cross-platform session continuity, transparent provider fallback, and network-aware API design — all areas with demonstrated, unmet user demand.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for 2026-08-03.

---

# NanoBot Project Digest — 2026-08-03

## 1. Today's Overview

A productive wave of **pull request activity** (9 PRs updated) suggests a focused push on developer-experience layers, provider compatibility, and backend robustness. While there are **no new releases** and **zero open issues**, the volume of pending PRs indicates maintenance and hardening are the current priorities. The absence of new issue reports is a positive health signal, suggesting the project is not experiencing an influx of external bug reports. The PR queue is heavily concentrated on fixes (5 out of 9 PRs are bug fixes) with a mix of performance and feature work.

## 2. Releases

**No new releases** were published in the last 24 hours. The most recent release remains the previous stable version. Users tracking specific bug fixes (e.g., the provider issues in PRs #5214 and #5216) will need to wait for the next release cycle or build from `main`.

## 3. Project Progress

Today saw **1 closed PR**:
- **[[CLOSED] fix(codex): dedup reasoning items before send, retry on duplicate-item 400](https://github.com/HKUDS/nanobot/pull/4021)** (merged). This long-running PR (opened May 27) was finally merged, resolving [#3633](https://github.com/HKUDS/nanobot/issues/3633). It fixes the `openai_codex_provider` which was intermittently causing multi-turn conversation failures (HTTP 400 `Duplicate item found`). The fix includes a pre-send deduplication pass and a retry mechanism on duplicate-item errors.

Additionally, **1 new issue was closed** during this period, though its association with a specific PR merge is not confirmed.

## 4. Community Hot Topics

The most active areas of contribution are emerging from the PR queue, though none have traction via comments or reactions yet (all show `undefined`). The key thematic clusters are:

- **Provider Reliability (Gemini & OpenAI):** Two PRs address fatal API incompatibilities.
  - [PR #5216: fix(image): send Gemini Flash hints via `generationConfig.imageConfig`](https://github.com/HKUDS/nanobot/pull/5216) addresses a hard failure (HTTP 400) for all Gemini Flash image models.
  - [PR #5214: fix(providers): fall back to chat completions on serde body rejections](https://github.com/HKUDS/nanobot/pull/5214) prevents terminal failures when the OpenAI Responses API rejects the request body.
- **Cross-Session UX:**
  - [PR #5211: feat(session): add cross-session search and mentions](https://github.com/HKUDS/nanobot/pull/5211) introduced by `Re-bin` is a significant feature addition that allows the WebUI to link and search across different chats.

**Analysis:** The underlying need is clear: users are hitting hard walls with multiple model providers, and there is a desire to move beyond single-session isolation. The lack of comments on these PRs suggests they may be recently opened and awaiting maintainer review.

## 5. Bugs & Stability

Several bugs were addressed in the last 24 hours, with fix PRs already existing for all of them. They are ranked by severity (P1 = High, P2 = Medium):

1.  **Gateway Shutdown Hang (P1):** [PR #5215](https://github.com/HKUDS/nanobot/pull/5215) fixes a critical issue where stopping the gateway during an active exec session or MCP subprocess leads to `asyncio` teardown noise and can stall the shutdown process entirely.
2.  **Provider Fatal Errors (P1):** [PR #5214](https://github.com/HKUDS/nanobot/pull/5214) fixes a terminal failure for all conversations routed through the OpenAI Responses API when the endpoint rejects the request body.
3.  **Image Model Incompatibility (P2):** [PR #5216](https://github.com/HKUDS/nanobot/pull/5216) fixes a `HTTP 400 INVALID_ARGUMENT` error that bricks all Gemini Flash image generation models.
4.  **Plugin Installation Failure (P2):** [PR #5213](https://github.com/HKUDS/nanobot/pull/5213) fixes plugin commands (e.g., `nanobot plugins enable feishu`) failing in `uv`-based environments where `pip` is missing.
5.  **Duplicate Item Errors (Fixed):** The merge of [PR #4021](https://github.com/HKUDS/nanobot/pull/4021) resolves the `400 Duplicate item found` issue in the Codex provider.

## 6. Feature Requests & Roadmap Signals

While no new feature requests were filed as issues, the PR queue provides strong signals for the upcoming roadmap:

- **Enhanced Session Management:** The [PR #5211](https://github.com/HKUDS/nanobot/pull/5211) feature for cross-session search and mentions is likely to be a highlight in the next minor release, potentially paving the way for more complex agent interactions.
- **New Provider Support:** [PR #5212](https://github.com/HKUDS/nanobot/pull/5212) adds documentation and guidance for **MiniMax music generation**, indicating ongoing expansion of the provider ecosystem, specifically into audio generation.
- **Performance Optimizations:** [PR #5194](https://github.com/HKUDS/nanobot/pull/5194) targets WebUI performance by caching session lists, suggesting a focus on scaling for users with many threads.

**Prediction:** The next release will likely include the session search feature and the MiniMax expansion, alongside the stable backlog of provider fixes.

## 7. User Feedback Summary

Based on the PRs submitted, user pain points are centered on **production reliability**:

- Users are frustrated by **fatal, non-recoverable errors** (HTTP 400s) that break specific workflows, such as image generation with Gemini Flash and multi-turn conversations with OpenAI Codex.
- Users face **installation friction**, specifically in modern Python environments managed by `uv` where `pip` is not present.
- The push for **cross-session linking** (PR #5211) suggests users want a more connected and navigable chat history, rather than isolated silos.

The overall sentiment is constructive, with users actively contributing solutions (fixes) rather than just reporting issues.

## 8. Backlog Watch

The following open PRs have been updated recently and may require maintainer attention or review to avoid stalling:

- **[PR #5152](https://github.com/HKUDS/nanobot/pull/5152)**: A fix for subagent partial completion results, open since July 28. This is a regression fix and should be prioritized for review to prevent further issues.
- **[PR #5194](https://github.com/HKUDS/nanobot/pull/5194)**: A WebUI performance enhancement, open since July 31. It involves a complex change regarding "workspace-scope snapshots" and might need a thorough review from a core maintainer.
- **[PR #5211](https://github.com/HKUDS/nanobot/pull/5211)**: The larger feature PR for cross-session search. While new, it changes core session management and will likely need a detailed design review.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-08-03

---

## 1. Today's Overview

Hermes Agent is showing **very high activity**, with exactly 50 issues and 50 PRs updated in the last 24 hours. The project health is characterized by a **healthy balance of incoming bug reports and active fixes** — particularly on the Desktop app and gateway/session infrastructure. Several **security-related issues** were filed today (`#77162`, `#77164`, `#77165`) by a single contributor, indicating focused security hardening work. The stale backlog is a growing concern: the top 30 issues by comment count include items spanning from June to August, with issues like **#44846 (cross-channel awareness)** and **#56439 (session provenance)** aging for weeks without resolution. Notably, a *duplicate* cluster on cross-platform/session continuity (#4335, #49730, #62780, #44846, #74816) is now the **dominant community pain point**. No new releases were published today; the most recent version remains **v2026.7.20**.

---

## 2. Releases

**None.** No new releases were published in the last 24 hours. The latest available version remains **v2026.7.20** (referenced in issue #73381).

---

## 3. Project Progress

Nine PRs were closed/merged today. Key advances:

- **[PR #77180 — fix(env): config.yaml terminal.\* keys win over stale .env]** (CLOSED, P2) — Prevents stale `.env` `TERMINAL_ENV` values from overriding explicit `config.yaml` terminal settings mid-session; salvages a prior abandoned PR.
- **[PR #77159 — feat(models): add four Gemini models to OpenRouter curated list]** (CLOSED, P3) — Adds `google/gemini-3.5-flash`, `-lite`, and two others to the curated picker for BYOK users.
- **WS reconnect race (RAH-05/RAH-06) — [PR #77205] and [PR #77206]** (CLOSED, P2) — Fixed the WebSocket disconnect/reconnect TOCTOU race in `_close_sessions_for_transport()` that was never merged to main; the regression test was split into a follow-up PR.
- **Plugin lifecycle — [PR #62960]** (OPEN, P3) — Fixes bundled Chronos plugin failing to load via the general `PluginContext` (missing `register_cron_scheduler`), redirects it to its dedicated discovery path.
- **Deferred plugin discovery — [PR #77213]** (OPEN, P3) — Prevents circular-imports during registration from permanently disabling plugins by deferring discovery until `gateway.run`.

Other merged fixes include **[PR #77218]** (strip inline comments from unquoted `.env` values), **[PR #77214]** (drop unused `m.content` from search result rows), **[PR #77203]** (drop five retired/non-tool-capable OpenRouter IDs), and **[PR #77118]** (Buzz adapter native document upload).

---

## 4. Community Hot Topics

These issues are drawing the most attention, either by comments or reactions:

- **[Issue #4335 — Feature: Cross-platform session context sharing (CLI ↔ Telegram)**](https://github.com/NousResearch/hermes-agent/issues/4335) — **10 comments, 3 👍.** *"I had a long conversation on Telegram but the CLI agent knows nothing about it."* The most-commented issue; part of the larger cross-platform continuity cluster.
- **[Issue #75655 — Managed-runtime provisioning always fails**](https://github.com/NousResearch/hermes-agent/issues/75655) — **8 comments.** `uv sync` receives both `--locked` and `--no-config`, which are mutually exclusive; the failure is misattributed to a smoke-test failure and cannot self-heal. A **strong engineering-burden signal** for the installation path.
- **[Issue #53374 — Desktop GUI creates new session after Windows sleep**](https://github.com/NousResearch/hermes-agent/issues/53374) — **6 comments, 1 👍.** WebSocket disconnect on sleep causes the GUI to create a fresh session on reconnect, losing session context. Directly tied to the reconnection race fixed in PRs #77205/#77206.
- **[Issue #70647 — `-z/--oneshot` pipes silently ignored]** — **6 comments.** Docs claim "Intended for scripts / pipes" but stdin is never read. A **P2 design gap** for automation users.
- **[Issue #69161 — Collapse thinking/reasoning blocks by default]** — **5 comments, 2 👍.** Desktop UI scrolls/jumps while streaming the reasoning block; a UX annoyance with clear community support.
- **[Issue #49730 — Cross-platform conversation continuity]** — **4 comments, 1 👍.** A near-duplicate of #4335; confirms this is the **dominant user demand**.

---

## 5. Bugs & Stability

Ranked by severity *reported today*:

| Severity | Issue | Summary | Fix Status |
|---|---|---|---|
| **P2 — Session data loss** | **[#74133 — Queued messages leak across sessions (Desktop)**](https://github.com/NousResearch/hermes-agent/issues/74133) | Switching session tabs auto-sends pending input into the *wrong* session; causes cross-contamination. | No fix PR yet; related to pending-session logic. |
| **P2 — Functional regression** | **[#74278 — Auth login ignores X-Forwarded-Prefix**](https://github.com/NousResearch/hermes-agent/issues/74278) | Sign-in breaks behind path-prefix reverse proxies; hardcoded root-absolute paths. | No fix PR. |
| **P2 — Delivery failure** | **[#74001 — Update error every time since 2026/07/29**](https://github.com/NousResearch/hermes-agent/issues/74001) | Desktop update fails after the recent update; screenshots attached. | Marked `needs-repro`; no fix PR yet. |
| **P2 — Delivery correctness** | **[#76767 — Desktop replies to Telegram never delivered**](https://github.com/NousResearch/hermes-agent/issues/76767) | Replies bound to Telegram session are not created as delivery obligations; conversations silently lost. | No fix PR. |
| **P2 — State corruption** | **[#73401 — `_apply_managed_env()` crash on PermissionError**](https://github.com/NousResearch/hermes-agent/issues/73401) | Startup crash contradicts its own fail-open contract. | No fix PR. |
| **P2 — Incorrect behavior** | **[#73032 — Discord auto-thread duplicates**](https://github.com/NousResearch/hermes-agent/issues/73032) | Single message creates two threads + duplicate replies. | `needs-repro`. |
| **P1 (Security)** | **[#77162, #77164, #77165 — Secret redaction gaps**](https://github.com/NousResearch/hermes-agent/issues/77162) | Applied-secrets snapshot values leak into provider egress paths, child-process env, and tool results. | Three focused security PRs needed; no fix PRs yet filed for these. |

**Post-2026/07/29 update regressions** (issues #74001, #73381) are a **recurring pattern** on Windows, specifically around the managed-venv upgrade path — worth immediate maintainer attention. Fix PRs exist only for the WS reconnect cluster (#77205/#77206); most other P2s are unaddressed.

---

## 6. Feature Requests & Roadmap Signals

The loudest signals, in priority order:

1. **Cross-platform/session continuity (highest demand)** — Issues #4335, #49730, #62780, #44846, #74816 all demand shared, real-time syncable sessions across CLI/Desktop/Telegram/Discord. This is the **most-requested feature set** with 22+ total comments.
2. **Auto-launch Desktop at login (Windows)** — [#76897](https://github.com/NousResearch/hermes-agent/issues/76897), **PR #77025 already implements it** — likely to land in the next release.
3. **Collapse thinking/reasoning blocks by default** — [#69161](https://github.com/NousResearch/hermes-agent/issues/69161), 2 👍; a simple UX toggle that could ship quickly.
4. **Full German localization** — [#77197](https://github.com/NousResearch/hermes-agent/issues/77197) (filed and closed today — likely asked and answered quickly).
5. **More Gemini models in OpenRouter picker** — [#76732](https://github.com/NousResearch/hermes-agent/issues/76732); **PR #77159** (merged) addresses this.

**Prediction:** The next minor version (v2026.8.x) will likely include *Launch at login* (PR #77025) and the OpenRouter Gemini additions (PR #77159). The cross-session context sharing (largest demand) still lacks a maintained implementation plan and will be a **multi-PR effort**.

---

## 7. User Feedback Summary

- **Top recurring pain point — session isolation across interfaces.** Users describe: *"I had a long conversation on Telegram but the CLI agent knows nothing about it"* (#49730), *"The same logical thread... separate session each time"* (#62780), *"No notion of one conversation"* (#4335). This is a **critical usability gap** for multi-device power users.
- **Windows installation/update failures dominate stability complaints.** Issues #73381 (venv + `cryptography` + file locking) and #74001 (update error after 07/29) show **persistent Windows-specific regression risk** around the managed-venv provisioning path.
- **Desktop UX momentum is strong.** Positive signals: users are requesting quality-of-life features (collapse thinking blocks, scroll preservation, message delete/quote/auto-scroll — #73296), signaling **product maturity and daily-driver usage**. The volume of niche UX requests suggests the Desktop app is *already trusted as primary interface*.
- **Security-conscious contributors are active.** The `andrexibiza` cluster of security issues (#77162–#77165) indicates an engaged security community probing egress redaction paths — a healthy sign for the project's security posture.

---

## 8. Backlog Watch

High-value items requiring maintainer attention, ranked by age and importance:

- **[#44846 — Cross-channel session awareness](https://github.com/NousResearch/hermes-agent/issues/44846)** — created **2026-06-12**, 1 comment, 2 👍. Oldest active cross-platform request; outdated vs. the newer #4335. Needs triage/closure decision.
- **[#32887 — gateway_state.json heartbeat missing](https://github.com/NousResearch/hermes-agent/issues/32887)** — created **2026-05-27**, 3 comments. Idle gateways falsely marked down in cross-container WebUI; **stale for ~10 weeks**.
- **[#56439 — gateway /resume overwrites sessions.source](https://github.com/NousResearch/hermes-agent/issues/56439)** — created **2026-07-01**, 3 comments, 1 👍. Destroys session provenance; **untouched for a month**.
- **[#60852 — Deduplicate session system prompt snapshots](https://github.com/NousResearch/hermes-agent/issues/60852)** — PR open since **2026-07-08**, P2 perf improvement. Long-unmerged; risks conflicts with the session-state sweeper work.
- **[#62960 — Chronos plugin loading fix](https://github.com/NousResearch/hermes-agent/issues/62960)** — PR open since **2026-07-12**. Small P3 fix; drags maintenance burden.

**Maintainer recommendation:** The session-continuity cluster (#4335, #49730, #62780, #44846) should be consolidated into a **single canonical roadmap issue** with a clear architectural direction, otherwise the community demand appears unaddressed for months.

---

*Source: github.com/NousResearch/hermes-agent — data as of 2026-08-03.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-03

## 1. Today's Overview
PicoClaw shows moderate activity with 3 issues and 9 PRs updated in the last 24 hours, reflecting a steady but not frantic pace. The project maintains a healthy mix of community-driven feature work, bug fixes, and security-hardening efforts. Notably, one critical user-facing bug (silent tool failure loops) has both a reported issue and a dedicated fix PR in progress. Three PRs were merged or closed today, including a Taiwanese localization effort and an automated PR experiment. The presence of several items marked `[stale]` after just 7–8 days suggests maintainer bandwidth could be a constraint.

## 2. Releases
No new releases were published in this window. The most recent reference is PicoClaw v0.3.1 (`2cf030d`), mentioned in a bug report from July 25. Community members are actively contributing features (Exa search provider, AI Router preset) that likely target a future minor release.

## 3. Project Progress
Three PRs were merged or closed today:

- **[#3313](https://github.com/sipeed/picoclaw/pull/3313) [Merged] — Fix: agent not able to execute shell command added to `customAllowPatterns`** — This is a substantive bug fix by `j-v`. The issue was that default deny patterns always took precedence in `guardCommand`, preventing users' explicit allow-patterns (e.g., `git push`) from working. The PR corrects the precedence logic so `customAllowPatterns` function as intended. This addresses a real workflow blocker for users extending the agent's shell capabilities.

- **[#3310](https://github.com/sipeed/picoclaw/pull/3310) [Closed] — Feat/auto pr** — An experimental PR submitted by an automated bot (`picoclanker did this`). No human-authored description; this appears to be a user testing an auto-PR workflow, not a substantive contribution.

- **[#3261](https://github.com/sipeed/picoclaw/pull/3261) [Closed] — Add zh-TW locale and Traditional Chinese translations** — Merged after 18 days in review. Adds Taiwanese terminology across the WebUI and documentation, extending the project's localization coverage.

On the PR front, an important note: `j-v` opened **[#3314](https://github.com/sipeed/picoclaw/pull/3314)** as what appears to be a direct follow-up to the merged fix #3313 (same title, same author) — possibly a re-attempt if the first merge was incomplete or rebased.

## 4. Community Hot Topics
The most active discussion today:

- **[Issue #3298 — Add AI Router as an OpenAI-compatible provider preset](https://github.com/sipeed/picoclaw/issues/3298)** — The author (maintainer of AI Router) discloses affiliation and proposes a named provider preset. While PicoClaw can already connect via the generic `openai` provider with a custom `api_base`, users can't select a named preset in the UI. This is a quality-of-life request that reduces setup friction for a popular routing service. One comment, no reactions.

- **[Issue #3294 — `/list models` only shows current model instead of all configured models](https://github.com/sipeed/picoclaw/issues/3294)** — A user with multiple models in `model_list` expects `/list models` to show all configured options, but only the active model/provider is displayed. This is a command semantics mismatch — the behavior doesn't match the documented description.

Both issues have exactly one comment and zero reactions, indicating focused attention rather than broad community engagement. The tool-failure loop issue ([#3311](https://github.com/sipeed/picoclaw/issues/3311)) hasn't yet drawn comments, but the associated PR is the project's most technically substantive recent work.

## 5. Bugs & Stability
One new bug reported today, ranked by severity:

**High — Silent repeated tool failure loops with no user response** ([Issue #3311](https://github.com/sipeed/picoclaw/issues/3311))
- **Reported by:** `lucapette`
- **Impact:** A turn can spin silently for minutes (up to `max_tool_iterations`) when a tool returns the same error every call. In production over Telegram, a user asking for a `git` command never got a reply. This is a user-facing reliability failure.
- **Fix available:** PR [#3312](https://github.com/sipeed/picoclaw/pull/3312) is open, implementing early turn termination on repeated identical tool failures. Not yet merged.

**Medium — `customAllowPatterns` precedence bug** (reported earlier, fixed today)
- Merged via [#3313](https://github.com/sipeed/picoclaw/pull/3313). Users adding commands like `git push` to their exec allow list were still blocked because default deny patterns took precedence. Root cause: logic inversion in `guardCommand`.

**Medium — `/list models` semantic mismatch** ([Issue #3294](https://github.com/sipeed/picoclaw/issues/3294))
- Not a crash, but misleading UX. Command description says "Configured models," yet only the current one is displayed. No fix PR open yet.

**Low — `SplitMessage` hang on oversized fence headers** (mentioned in PR [#3295](https://github.com/sipeed/picoclaw/pull/3295))
- Open PR from July 26; the issue was identified during review, not as a fresh bug report. The fix adds a fallback raw split to ensure progress.

## 6. Feature Requests & Roadmap Signals
Several features are in flight:

- **Native Exa web search provider** ([PR #3299](https://github.com/sipeed/picoclaw/pull/3299)) — Adds Exa's `/search` API as a first-class `web_search` provider. Supporting rationale per the PR: the existing generic approach doesn't expose Exa's `type: "auto"` and range filters properly. This signals interest in expanding provider coverage beyond the usual suspects.

- **AI Router provider preset** ([Issue #3298](https://github.com/sipeed/picoclaw/issues/3298)) — A named provider preset for AI Router to make setup one-click. The contributor is the service maintainer, which increases the probability of a merged implementation. It's a small, well-scoped addition.

- **Security hardening for remote prompts and exec boundaries** ([PR #3297](https://github.com/sipeed/picoclaw/pull/3297)) — Normative security work: moving remote sender/chat metadata out of provider system instructions, defaulting remote exec to disabled, and enforcing origin policy at execution time. Includes a config schema migration to v4.

- **i18n expansion** — Czech code wrap labels ([PR #3296](https://github.com/sipeed/picoclaw/pull/3296)) and completed zh-TW ([PR #3261](https://github.com/sipeed/picoclaw/pull/3261)) show consistent community investment in localization.

Predictions for next release: the tool failure early-termination fix (#3312) is likely to land first given its severity. The Exa provider (#3299) and security hardening (#3297) are both substantive and likely for the next minor version. The stale items may need maintainer nudge (see Backlog Watch).

## 7. User Feedback Summary
Real pain points from today's data:

- **Silent agent failure** — The tool-loop bug (#3311) is the most serious: users ask for something, the agent silently loops for minutes, and no answer arrives. Likely causes cited include `git` without credentials or shell safety guard blocks. This destroys trust in the agent.
- **Shell allow list confusion** — `customAllowPatterns` not honoring explicit user configuration was a deployment-blocking bug for the reporter (#3313). When documented tests pass but production behavior fails, users can spend significant time debugging configuration before realizing it's a software bug.
- **List command UX mismatch** — The `/list models` complaint is minor but symptomatic of interface expectations vs. implementation drift.
- **Provider setup friction** — Users want first-class provider presets (AI Router) rather than manually constructing `api_base` URLs, even when the generic path works.

Community sentiment appears constructive overall — issues are well-formatted, contributors are submitting fix PRs alongside bug reports, and localization contributors are actively expanding reach.

## 8. Backlog Watch
Items that need maintainer attention:

- **[PR #3297 — fix(security): harden remote prompt and exec boundaries](https://github.com/sipeed/picoclaw/pull/3297)** — Open for 8 days, none of which have seen maintainer comment. This is security-relevant and includes a config migration (schema v4). Stale labeling suggests maintainers haven't yet triaged it.

- **[PR #3296 — i18n: complete Czech code wrap labels](https://github.com/sipeed/picoclaw/pull/3296)** — 8 days open, no reviewer assignee. i18n PRs are usually low-risk and quick to review; stagnation discourages future contribution.

- **[PR #3295 — fix(channels): prevent `SplitMessage` hang on oversized fence headers](https://github.com/sipeed/picoclaw/pull/3295)** — 8 days open. Includes regression coverage, suggesting a well-prepared contribution that could use maintainer sign-off.

- **[PR #3299 — Add native Exa web search provider](https://github.com/sipeed/picoclaw/pull/3299)** — 8 days open, no comments from the maintainer. As a new provider integration, this needs architectural review.

The cluster of five stale items from July 26–27 (two issues, three PRs plus #3296) suggests a review backlog that began building about a week ago. If the maintainer team has limited bandwidth, a triage pass prioritizing security (#3297), bug fixes (#3295), and provider additions (#3299) would keep momentum healthy.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-03

## Today's Overview
NanoClaw is in a **moderate-to-high activity** phase, with 10 PRs updated in the last 24 hours (7 open, 3 closed/merged) but only 1 new issue opened. The project shows a healthy mix of new feature development (Dial channel integration, remote MCP servers), targeted bug fixes (Docker/SQLite lock contention, Teams file support), and housekeeping (removing deprecated skills, release pipeline hardening). The staleness of several PRs (some open since May–July) suggests a potential review bottleneck, though the core team continues to merge fixes. No new releases were published today, but a release-pipeline fix (retry post-publish readback) was merged, indicating an imminent release cycle. Overall, the project is **healthy but has a growing review queue** that warrants attention.

## Releases
**No new releases were published in the last 24 hours.** Given the merge of PR #3176 (fix release retry logic), a release is likely imminent, though no tag or changelog is available yet.

---

## Project Progress
Three PRs were closed/merged in the last 24 hours:

1. **[#3176 — fix(release): retry post-publish readback](https://github.com/nanocoai/nanoclaw/pull/3176)** *(merged)* — Core-team fix that adds retry logic to post-publish readback steps in the release pipeline, reducing flaky release failures.

2. **[#301 — feat(skill): enhance add-telegram skill with Markdown rendering, file downloads, and Linux/Docker guidance](https://github.com/nanocoai/nanoclaw/pull/301)** *(closed, was blocked since Feb)* — Completes a long-pending Telegram skill enhancement (HTML/plain-text fallback for Markdown, file download support, typing-indicator pattern docs). Marked as "pending closure" — likely an abandoned PR that was finally cleaned up.

3. **[#2626 — fix(signal): replace silent restartService failure with explicit error](https://github.com/nanocoai/nanoclaw/pull/2626)** *(closed; closes #2583)* — Fixes a subtle Signal channel bug where `launchctl kickstart -k` failed silently (when a prior `unload` ran), confusing users during setup. Now surfaces explicit errors.

**Feature advancement:** The open Dial channel PRs (#3041, #3050) continue to be updated, suggesting active iteration on the new SMS + AI voice channel adapter.

---

## Community Hot Topics
1. **[Issue #3177 — Session database lock contention on Docker cross-mount filesystems](https://github.com/nanocoai/nanoclaw/issues/3177)** *(opened by DawoudIO)* — 29,000+ readonly errors reported. This is the **single most critical user-facing problem** today. Although it has 0 comments, the severity and reproducibility make it the top pain point. Root cause: SQLite DELETE journal mode doesn't propagate across Docker VirtioFS mounts.

2. **[PR #3090 — fix(templates): prepend all top-level context Markdown](https://github.com/nanocoai/nanoclaw/pull/3090)** *(core-team, open since Jul 19)* — Continued updates suggest active discussion/review. Affects how context is injected into agent prompts — a core behavioral change.

3. **[PR #3092 — feat: support remote Streamable HTTP MCP servers](https://github.com/nanocoai/nanoclaw/pull/3092)** *(core-team, open since Jul 19)* — Also actively updated. This is a **high-demand architectural feature** (remote MCP servers over HTTP) that many users have been requesting for production deployments.

4. **[PR #2625 — fix(teams): set supportsFiles: true in Teams manifest](https://github.com/nanocoai/nanoclaw/pull/2625)** *(open since May 27)* — A long-stale fix for silent file-delivery drops in Teams (closes #2461). Its continued lifespans despite being a confirmed bug fix is concerning.

---

## Bugs & Stability
1. **Critical — SQLite lock contention under Docker (Issue #3177)** — 29,000+ readonly errors on `inbound.db`/`outbound.db` when deployed via Docker cross-mount on macOS/Linux. Root cause identified: VirtioFS + SQLite DELETE journal mode conflict. **No fix PR exists yet.** This is the #1 stability issue and likely a blocker for containerized production deployments.

2. **Medium — Silent Teams file-delivery failures (PR #2625)** — `supportsFiles: false` hardcoded in the manifest, causing bidirectional file-send failures in personal chats. **Fix PR open for 68 days** without merge.

3. **Medium — Silent Signal restart failures (PR #2626, merged)** — Resolved today; `restartService` silently no-oped after `unload`. Explicit error handling now in place.

4. **Low — Command-gate denial write-path corruption (PR #3175)** — `writeOutboundDirect()` violated the single-writer rule by having the host write directly into container-owned `outbound.db`. Open PR proposes routing through the delivery adapter. This is a correctness/architecture fix but has been open only 1 day.

---

## Feature Requests & Roadmap Signals
- **Dial channel (SMS + AI voice calls)** — PRs #3041 (channel adapter) and #3050 (channel picker + wizard/skills) are the largest feature effort in progress. The sustained updates over 3 weeks suggest this is the **next flagship integration**, likely in the upcoming release.
- **Remote Streamable HTTP MCP servers (PR #3092)** — Enables MCP servers outside the local process. Strong signal for multi-machine/cloud deployments; likely to land within the next 1–2 versions.
- **Top-level context Markdown prepending (PR #3090)** — A subtle but impactful change to how context is assembled in templates; could be a precursor to configurable prompt architecture.

---

## User Feedback Summary
- **Pain point: Docker deployments are fragile.** Issue #3177 (29K readonly errors) is a systemic problem on macOS/Linux Docker hosts. Users running containers with bind mounts experience intermittent delivery failures — this erodes trust in the "works everywhere" promise.
- **Pain point: Silent failures frustrate setup.** The Signal restart fix (#2626) and Teams file support (#2625) both address scenarios where the system silently stops working — a pattern users dislike because debugging requires deep log diving.
- **Positive signal: Channel ecosystem expansion.** Active PRs for Dial (voice/SMS) and Telegram skill improvements show the community is building a genuine multi-channel platform, not just a chat tool.
- **Frustration indicator:** The 68-day-old Teams fix (#2625) with a clear root cause and user impact (#2461) remains unmerged — suggesting either maintainer bandwidth constraints or unstated concerns.

---

## Backlog Watch
These items need maintainer attention:

1. **PR #2625 — Teams `supportsFiles: true`** ([link](https://github.com/nanocoai/nanoclaw/pull/2625)) — Open 68 days, closes a real bug (#2461, file delivery drops). Simple one-line manifest + doc change. **Highest priority for review.**

2. **Issue #3177 — Docker SQLite lock contention** ([link](https://github.com/nanocoai/nanoclaw/issues/3177)) — Critical, no fix PR yet. Needs a maintainer response/acknowledgment and a proposed migration path (e.g., WAL mode, volume-based storage for DBs).

3. **PR #301 — Telegram skill enhancement** ([link](https://github.com/nanocoai/nanoclaw/pull/301)) — Closed as "pending closure" after 5 months. The underlying work (Markdown, file downloads) is valuable; consider reassigning or cherry-picking parts into a fresh PR.

4. **PR #2626 — Signal explicit error fix** ([link](https://github.com/nanocoai/nanoclaw/pull/2626)) — Already merged today; **no action needed**, included for context.

5. **PR #3090 / #3092 — Template + MCP changes** — Both open ~15 days with core-team labels. These are architectural changes and should not be rushed, but they need either review updates or a status comment to keep momentum.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-03

## 1. Today's Overview

IronClaw is in a period of intense stabilization and hardening, with a clear focus on the Reborn architecture's delivery and network security layers. The project saw 7 issues updated in the last 24 hours (6 open) and 26 PRs updated, with 11 merged/closed — a high-velocity day dominated by QA findings and rapid response fixes. The QA team (primarily `theredspoon`) filed five detailed bug reports covering durable delivery race conditions, SSRF protection gaps, and coordinator concurrency issues, and maintainers already closed matching fix PRs for two of them (#7028, #7029). A significant refactoring effort consolidating the Wave 2 port-inversion stack (#7018) was merged, marking continued architectural de-coupling of product-facing contracts. The overall project health appears robust: bugs are being found systematically, fixed immediately with deterministic regression tests, and the release train (#5598) continues to move forward. Dependency updates and CI efficiency improvements round out a mature, well-governed development cycle.

## 2. Releases

No new releases were published today. The most recent release candidate PR (#5598, still open) proposes the next version bump:
- `ironclaw_common`: 0.4.2 → 0.5.0 (⚠ API breaking changes)
- `ironclaw_safety`: 0.2.2 → 0.2.3 (✓ API compatible)
- `ironclaw_skills`: 0.3.0 → 0.4.0 (⚠ API breaking changes)

This release PR remains open with no comments indicating a merge blocker, though it was updated today, suggesting the release train is being kept aligned with `main`.

## 3. Project Progress

**Merged/Closed PRs today (11 total), key items:**

- **Wave 2 port-inversion consolidation (#7018, closed)** — XL-sized refactor merging four fully-reviewed PRs (#7000, #7003, #7004, #7005) into one stack onto `main`. This completes significant contract de-coupling, notably inverting `ironclaw_operator`'s product-facing ports, splitting `ironclaw_extension_manager` out of `extension_host`, and resolving the `ProductSurfaceFailure` linchpin across 19 production files.

- **Durable delivery fix (#7029, closed)** — Restores the `Prepared → Sending` compare-and-swap as the sole authority for vendor-egress ownership, addressing the QA-reported #7025 (concurrent coordinators sending duplicate deliveries). Includes `DuplicateSuppressed` return semantics and removes the process-local `in_flight` authority.

- **Terminal status preservation fix (#7028, closed)** — Replaces the unconditional status write in interrupted-delivery recovery with a guarded `Sending → Unknown` transition, directly addressing QA issue #7017. Includes a deterministic coordinator-level regression test.

- **CI improvements (#7013, #6952, #7007, all closed)** — Restored the original 90% changed-line coverage floor; implemented deterministic affected-area scoping for Reborn PR tests (running full transitive workspace consumer closures); and added Slack alerting for live-canary merge queue failures.

**Open but active large PRs:**
- #5981 (Reborn queued-message steering, XL) — still open after weeks of review, with turn-boundary races fixed and end-to-end journey tests added.

## 4. Community Hot Topics

The most active discussion centers on the **delivery-race and network-security QA cluster** filed by `theredspoon`:

- **#7025 — Concurrent coordinators can both send the same durable delivery attempt** — Critical domain bug with direct architectural implications. Analyzes how `in_flight` authority and CAS failures interact across coordinator instances. [Link](https://github.com/nearai/ironclaw/issues/7025)
- **#7017 — Interrupted-delivery recovery can overwrite a concurrent Delivered status** — Paired with #7025; QA verified the fix in #7028 reverifies cleanly. [Link](https://github.com/nearai/ironclaw/issues/7017)
- **#7016 — Ambient proxy env vars bypass DNS-rebinding protection in ReqwestNetworkTransport** — Security-focused finding; the fix PR #7027 (disable ambient proxy discovery) is already up. [Link](https://github.com/nearai/ironclaw/issues/7016)
- **#7030 — Host-mediated egress ignoring ambient proxy variables in operator diagnostics** — Companion to #7016, focused on `doctor` diagnostics accuracy. [Link](https://github.com/nearai/ironclaw/issues/7030)

The underlying need is clear: IronClaw's Reborn network transport and outbound delivery engine are being held to extremely high correctness and security standards, with QA and maintainers collaborating on deterministic, test-covered fixes.

## 5. Bugs & Stability

Ranked by severity:

**High — Delivery correctness races:**
1. **#7025 (Concurrent coordinators duplicate sends)** — Same delivery attempt sent twice; likely caused by losing `Prepared→Sending` CAS claims replaying without `DuplicateSuppressed`. *Fix PR #7029 already merged.* [Issue](https://github.com/nearai/ironclaw/issues/7025) | [PR](https://github.com/nearai/ironclaw/pull/7029)
2. **#7017 (Recovery overwrites Delivered status)** — Data-integrity risk where a `Delivered` terminal state can be clobbered back to `Unknown`. *Fix PR #7028 already merged.* [Issue](https://github.com/nearai/ironclaw/issues/7017) | [PR](https://github.com/nearai/ironclaw/pull/7028)
3. **#7031 (Failed lazy-delivery recovery not retried within coordinator lifetime)** — Lower data-integrity risk but a resilience gap; no fix PR yet. [Link](https://github.com/nearai/ironclaw/issues/7031)

**Medium — Security/SSRF:**
4. **#7016 (Ambient proxy bypasses DNS-rebinding protection)** — SSRF vector via `reqwest` system-proxy discovery. *Fix PR #7027 open, not yet merged.* [Issue](https://github.com/nearai/ironclaw/issues/7016) | [PR](https://github.com/nearai/ironclaw/pull/7027)

**Medium — Migration bug (already fixed):**
5. **Legacy loop checkpoint startup failure** — `ironclaw serve` crashed on startup for stores with legacy loop checkpoints (`no checkpoint-state payload`); join was on mismatched columns. *Fixed in PR #7026.* [PR](https://github.com/nearai/ironclaw/pull/7026)

**Low:**
6. **#7030 (diagnostics ignore ambient proxy vars)** — Operator visibility gap; no fix PR yet. [Link](https://github.com/nearai/ironclaw/issues/7030)
7. **#7015 (Staking page UI bug, closed)** — User-reported UI defect with no repro steps; closed without fix (likely insufficient info).

## 6. Feature Requests & Roadmap Signals

- **Time-awareness without prompt-cache churn (#7012)** — Filed by `ilblackdragon`, this is a well-articulated design proposal for append-only rollover context and duration evidence. It extends PR #7001's cache-boundary fix (moving runtime context out of the leading system block) into a broader temporal contract. This smells like a deliberate design-stage feature that may land as a structured RFC or implementation in the near future — very likely a candidate for the next minor release. [Link](https://github.com/nearai/ironclaw/issues/7012)

- **Hosted MCP auth resilience (#7024, open)** — Enhancing structured credential setup for metadata-less hosted MCP `401` responses with actionable, provider-neutral guidance. Ongoing work by core contributor `henrypark133`. [Link](https://github.com/nearai/ironclaw/pull/7024)

- **CI/canary observability (merged)** — Slack alerting on merge-queue failures (#7007) signals operational maturity and a focus on velocity with safety.

## 7. User Feedback Summary

- **UI bug on Staking page (#7015, closed):** A user reported a UI defect but provided no screenshot, description, or repro steps. Closed as-is — and a signal that the product feedback loop may need guardrails (e.g., requiring evidence) to avoid low-value triage overhead. No satisfaction/dissatisfaction score available.

- **QA-driven feedback (most of today's volume):** The substantive feedback is coming from the internal QA harness, which is highly constructive — each finding includes commit hashes, repro steps, and proposed bounds. This indicates strong engineering culture and fast feedback loops, but it also means external user feedback is relatively quiet this week.

## 8. Backlog Watch

- **PR #5981 — Reborn queued-message steering (XL, open since Jul 11):** The longest-running open PR. Forward-ported and fixed for turn-boundary races, but has been sitting for three weeks. Likely waiting on a maintainer review pass — may be a merge bottleneck for Reborn scope. [Link](https://github.com/nearai/ironclaw/pull/5981)

- **PR #5598 — Release (open since Jul 3):** The release PR with breaking changes (`ironclaw_common`, `ironclaw_skills`) has been open for a month. It was touched today, but no merge. If breaking changes are going out, the team should coordinate timing carefully — this could be blocked by the QA findings currently being fixed.

- **Issues #7030/#7031 (filed today, no fix PR yet):** Operator diagnostics gap and delivery-retry gap; these are new but should be triaged soon to avoid piling onto an already-hot topic area (outbound reliability).

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-03

## 1. Today's Overview

LobsterAI shows a **quiet but active** development period, with 6 PRs and 3 issues touched in the last 24 hours, though none were opened or merged today. All activity represents older work (dated ~April 2026) receiving final comments, stale-marking, or closure — suggesting the project is in a **stabilization and cleanup phase** rather than a rapid-development sprint. The absence of new releases, new issues, or fresh PRs for over four months points to a **mature project with an active maintenance backlog**, where dependabot PRs (concurrently, tailwindcss) and UX/perf improvements are being reviewed but not yet merged. The project remains healthy — no critical new bugs and no community escalations — but momentum has slowed considerably, and the growing stale-marker count could warrant maintainer attention to triage or close lingering items.

## 2. Releases

**No new releases** were published in the last 24 hours, and none are pending or documented in the data. The last referenced version in the issues is **2026.3.26** (from Issue #1217). There are two stalled dependency-update PRs (#1285, #1286) that could potentially be batched into a future maintenance release, but no release timeline is currently visible.

## 3. Project Progress

No PRs were merged or closed today. The two closed items in the last 24 hours were **stale issue closures** (#1287, #1289), not code merges. The **four open PRs** represent the project's most substantial in-flight work, all awaiting review/merge:

- **[#1215 — fix(im): always rebuild chat handler on setConfig](https://github.com/netease-youdao/LobsterAI/pull/1215)** — Critical fix for platform-specific config saves (DingTalk, Telegram) not triggering chat handler updates, meaning `systemPrompt` and other settings changes were silently ignored.
- **[#1218 — fix(定时任务): 重构任务列表排序规则](https://github.com/netease-youdao/LobsterAI/pull/1218)** — Replaces the current random UUID-based sorting of scheduled tasks with a sensible, creation-time-based order.
- **[#1219 — perf(cowork): 消除无效重渲染](https://github.com/netease-youdao/LobsterAI/pull/1219)** — Adds `React.memo` and consolidates multiple `useSelector` calls to eliminate unnecessary re-renders in cowork session lists/details.
- **[#1220 — perf(cowork): 消除 N+1 查询](https://github.com/netease-youdao/LobsterAI/pull/1220)** — Optimizes `recentChats()` and `conversationSearch()` to batch message queries per session instead of executing N+1 individual queries.

These PRs address **real, tangible user pain points** (correctness, usability, and performance) and would meaningfully improve the product if merged. Their extended time in-review may indicate a bottleneck in reviewer availability.

## 4. Community Hot Topics

No issues or PRs saw new comments or reactions in the last 24 hours, and all existing engagement is low (0-2 comments). The most discussed items historically are:

- **[#1287 — IM机器人popo连通性测试Bug](https://github.com/netease-youdao/LobsterAI/issues/1287)** (2 comments, now closed as stale) — Users can pass connectivity tests with entirely fake credentials (`appkey`, `appsecret`, `aes key` all set to "1"). This is a **validation-gap bug** that undermines trust in the IM integration setup wizard. Notably, the issue was closed as **stale without an identified fix**, which could disappoint affected users.

- **[#1289 — 长代码块折叠/展开功能](https://github.com/netease-youdao/LobsterAI/issues/1289)** (2 comments, now closed as stale) — Users have been requesting collapsible long code blocks for months. The proposal is well-formed (auto-collapse between 15-200 lines, with existing limit mechanisms already at 200 lines). Its stale-closure is a **missed opportunity** — the feature was fully scoped and ready for implementation.

## 5. Bugs & Stability

**No new bugs were reported in the last 24 hours.** However, the stale-closure of two historically reported issues leaves the following unresolved (ranked by user impact):

1. **[#1217 — 偶发启动网关，影响正常使用](https://github.com/netease-youdao/LobsterAI/issues/1217)** (OPEN) — **Most severe.** Users experience spontaneous gateway restarts 3-5 times per day on Windows 10, causing active interruptions. The issue includes logs and a specific version (2026.3.26), making it actionable — but it has been **open and stale for ~4 months with only 1 comment and no maintainer response**. This is the project's most significant open stability concern.

2. **[#1287 — 连通性测试伪造凭据可过](https://github.com/netease-youdao/LobsterAI/issues/1287)** (CLOSED as stale) — The connectivity test passes with fake credentials, misleading users into thinking integration setup succeeded. Closed without a fix.

No fix PRs exist for either issue.

## 6. Feature Requests & Roadmap Signals

**No new feature requests** were filed today. The only significant pending feature request is:

- **[#1289 — 长代码块折叠/展开](https://github.com/netease-youdao/LobsterAI/issues/1289)** — Closed as stale despite being fully specified. Given the detailed requirements already captured (auto-fold over 15 lines, configurable limits, expand/collapse mechanics), this could be picked up by any contributor or fast-tracked by maintainers for a **next minor release**. The codebase already has the infrastructure (`CODE_BLOCK_LINE_LIMIT`, `CODE_BLOCK_CHAR_LIMIT`), meaning the implementation cost is low.

**Roadmap signal:** The broader trend in open PRs (#1215, #1218, #1219, #1220) shows the team's focus on **hardening existing features** (IM integration, scheduled tasks, cowork performance) rather than shipping new features. If these PRs merge, they will likely be bundled into a "stability and performance" release.

## 7. User Feedback Summary

User feedback in the dataset is sparse but consistent across two themes:

- **Interruptions are the top concern** — The spontaneous gateway restart bug (#1217) is the only issue that directly disrupts active daily use, and it remains unanswered for months. Users shared logs and specifics but got no response.
- **UX polish gaps exist but are tolerated** — The long-code-block readability request (#1289) indicates users routinely encounter large AI outputs that are hard to navigate. This is a common complaint across AI-assisted chat UIs.
- **Setup validation needs strengthening** — The popo connectivity test passing with fake credentials (#1287) signals users want trustworthy setup diagnostics, and may have spent time configuring broken integrations based on misleading "success" results.

Overall, users are reporting **practical, real-world issues** (instability, readability, validation), but the lack of maintainer responses on any of them may increase dissatisfaction.

## 8. Backlog Watch

The following items have gone **over 4 months without meaningful maintainer response** and are at risk of user attrition:

1. **[#1217 — 偶发启动网关](https://github.com/netease-youdao/LobsterAI/issues/1217)** — OPEN, stale, 0 comments from maintainers. This is the **highest-priority unresolved bug** in the project. Needs immediate triage or user engagement.

2. **[#1289 — 长代码块折叠](https://github.com/netease-youdao/LobsterAI/issues/1289)** — CLOSED as stale with an actionable, well-specified feature. Reopening or implementing this would be a quick win.

3. **[#1287 — 连通性测试漏洞](https://github.com/netease-youdao/LobsterAI/issues/1287)** — CLOSED as stale with no fix. The underlying validation bug remains unaddressed.

4. **Open PR stalemate** — PRs #1215, #1218, #1219, #1220 have been open for ~4 months. They represent completed work with clear value. **Review-bottleneck** is the likely cause; batching a review session for these would unblock multiple improvements at once.

5. **Dependency PRs** — #1285 (concurrently) and #1286 (tailwindcss) were closed without merging, likely auto-closed by staleness. Long-term dependency drift may be accumulating; a single "deps: update all" PR could consolidate this.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the project digest for **Moltis** for **2026-08-03**:

---

### 1. Today's Overview
Moltis is in a **low-activity, development-focused** phase. With zero issues updated in the last 24 hours, the community discussion is currently quiet, indicating that most users are not encountering blockers. The sole activity is a **newly opened Pull Request** (#1183) focused on expanding the MCP (Model Context Protocol) server management capabilities. This suggests the project is currently prioritizing infrastructure and feature expansion over bug-fixing or release stabilization. The project health appears stable, with no incoming bug reports threatening the current codebase.

### 2. Releases
**None.** There are no new releases available for this period. The project is currently in a build-up phase towards the next version.

### 3. Project Progress
**No PRs were merged or closed today.** 
However, a significant feature is in the pipeline for review:
- **[PR #1183 [OPEN] feat(mcp): add managed repository bundles](https://github.com/moltis-org/moltis/pull/1183)**: This Pull Request proposes a major enhancement to MCP server management. It introduces managed Git repository bundles that will allow users to discover, preview, install, update, and remove MCP servers directly from Git repositories. The feature includes support for **HTTPS credentials** and **SSH transport**, as well as integration with the **vault lifecycle** for secret management.

### 4. Community Hot Topics
**No active discussions.** The only open PR (#1183) currently has no comments or reactions from the community. The lack of chatter suggests that the maintainers are likely driving this feature independently, or the community is waiting to review the final implementation before providing feedback.

### 5. Bugs & Stability
**No new bugs, crashes, or regressions were reported today.** The project is currently in a stable state regarding user-facing issues. The primary risk to stability lies within the complexity of the open PR (#1183), which touches on authentication (SSH/HTTPS) and database migrations—areas that typically carry a risk of introducing regressions if not thoroughly reviewed.

### 6. Feature Requests & Roadmap Signals
The direction of the project is clearly signaled by **[PR #1183](https://github.com/moltis-org/moltis/pull/1183)**. The addition of "managed repository bundles" indicates a strong roadmap focus on **ecosystem extensibility**. By enabling users to import MCP servers directly from Git repositories, Moltis is moving toward a more decentralized plugin/registry model. **Prediction**: This feature is likely to be the headline of the next minor version release, alongside the specified "CLI/RPC/web UI workflows" and corresponding database migrations to support the new configuration types.

### 7. User Feedback Summary
**No direct user feedback was collected in the last 24 hours.** With zero comments on the open PR and no issues, there is no new data on user satisfaction or pain points. The project is operating in a "maintainer-driven" phase right now.

### 8. Backlog Watch
**No long-unanswered issues or PRs require attention.** The repository currently has a clean slate regarding unanswered community input. The only item that needs maintainer attention is the **review of PR #1183** to ensure it moves forward efficiently, particularly checking the security implications of supporting **SSH transports** and **Git credentials** for MCP servers.

---

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-03

## 1. Today’s Overview
CoPaw is in a stable but busy state. No new releases were published, and no PRs were merged or closed within the last 24 hours, indicating that the project is in a consolidation phase rather than one of active shipping. However, the incoming signal is strongly positive: the two newest open issues, both reported by the same user, are directly paired with two open fix PRs from an active contributor (BlackBox-Labs), showing a healthy report-fix pipeline. Both issues target a concrete, user-facing performance problem — MB-level API payloads causing 30-second frontend timeouts on slow networks — which is a sign of real-world usage at scale. A third PR addresses a separate MCP integration bug. Overall, the community is engaged, the core maintainers are not absent, and the project is moving forward despite zero merge activity today.

## 2. Releases
There were no new releases published in the last 24 hours. The latest public version remains **QwenPaw 2.0.1 (pip)**, which is the version referenced in the newly filed bug reports.

---

## 3. Project Progress
No PRs were merged or closed in the last 24 hours. However, the following pull requests are open and actively updated, indicating either in-review status or recent revisions (all updated on 2026-08-02):

- **[#6634] fix(skills): exclude full content from skill list endpoints to fix slow network timeouts** — *by BlackBox-Labs*
  Directly addresses Issue #6633. The root cause: `SkillSpec` model extends a base class that includes full SKILL.md content in list responses, making them MB-level. The fix removes full content from list endpoints.
  > Link: [agentscope-ai/QwenPaw PR #6634](https://github.com/agentscope-ai/QwenPaw/pull/6634)

- **[#6636] fix(chats): add pagination to chat history and enable GZip compression** — *by BlackBox-Labs*
  Targets Issue #6635 (rest of the problem). Introducing pagination to `GET /api/chats/{chat_id}` and enabling GZip compression, which directly addresses the 30s timeout on long conversation histories.
  > Link: [agentscope-ai/QwenPaw PR #6636](https://github.com/agentscope-ai/QwenPaw/pull/6636)

- **[#6561] fix(mcp): ensure exposed tool names start with a letter** — *by axelray-dev*
  This PR fixes a compatibility bug where MCP servers with display namespaces starting with a non-letter (e.g., `-MCP__...`) produce invalid tool names that strict OpenAI-compatible providers (Kimi/Moonshot) reject with `invalid_function_name`.
  > Link: [agentscope-ai/QwenPaw PR #6561](https://github.com/agentscope-ai/QwenPaw/pull/6561)

Even without merges, the fact that #6634 and #6636 were created on the same day as their corresponding issues and are already linked as fixes shows strong ownership of the codebase and rapid triage.

---

## 4. Community Hot Topics
The two most active items are the bug report + fix pairs, which dominate today's conversation:

**#6635: “[Bug]: Console pages fail to load on slow networks”** *(1 comment)*
- Reporter: Moonlit-Pages — Reported on 2026-08-02
- > [Issue #6635](https://github.com/agentscope-ai/QwenPaw/issues/6635)
- Analysis: This is a systemic performance issue affecting multiple console views simultaneously, not just a single page. The fact that the reporter mentions “several console views” failing suggests that the underlying concern — over-fetching or no pagination — is a design-level issue relevant to many parts of the app. User expectation is clear: the console should work on real-world networks, not just on localhost or high-bandwidth connections. This is a reliability/trust issue.

**#6633: “[Bug]: Skills / Skill Pool pages fail to load on slow networks”** *(1 comment)*
- Reporter: Moonlit-Pages — Reported on 2026-08-02
- > [Issue #6633](https://github.com/agentscope-ai/QwenPaw/issues/6633)
- Analysis: The same reporter also reported this focused issue on the Skills/Skill Pool pages, which shows that `GET /api/skills` returns unnecessary embedded content. The commenter count is low early on, but the existence of two open PRs touching exactly these endpoints within 24 hours of report means this is the hottest topic in the project right now.

Together, these two issues are the “hot core” of the engine this week: real users on networks with latency, blocked by an API design that doesn't consider payload size.

---

## 5. Bugs & Stability
Ranked by severity:

1. **Critical — Full chat history in one response, no pagination or compression** ([#6635](https://github.com/agentscope-ai/QwenPaw/issues/6635))
    - Console pages fail to load on slow networks when fetching long chat histories exceeding 1 MB in a single API call, combined with a fixed 30-second frontend timeout. This results in a complete UI failure, leaving the user unable to access their chats.
    - **Fix available:** PR [#6636](https://github.com/agentscope-ai/QwenPaw/pull/6636) (pagination + GZip) — open.

2. **High — Skill list endpoints embed full SKILL.md content** ([#6633](https://github.com/agentscope-ai/QwenPaw/issues/6633))
    - MB-level payload for list endpoints (both `GET /api/skills` and `GET /api/skills/workspaces`). Correlates exactly with which workspaces have many or heavy skills, making entire pages fail on limited bandwidth.
    - **Fix available:** PR [#6634](https://github.com/agentscope-ai/QwenPaw/pull/6634) — open.

3. **Medium — MCP tool name incompatibility with strict OpenAI-compatible providers** ([PR #6561](https://github.com/agentscope-ai/QwenPaw/pull/6561))
    - Not a direct user-reported bug but blocks adoption with Kimi/Moonshot. The fix is ready in the open PR; it needs review and merge. This is not fatal but will cause complete request rejection for a subset of users.

Even though two of these are similar in nature, they are independent code paths, so both fixes a required. The maintainers have already received good PRs, so the next bottleneck is review time and merge.

---

## 6. Feature Requests & Roadmap Signals
There are no explicit “new feature” requests in the repo today. However, the user reports (and the fixes attached to them) are strong signals about **two key roadmap directions**:

1. **Network-aware API design (planned feature implied)** — Having to fix pagination and compression per-endpoint on-demand instead of as a global default suggests that API design currently favors simplicity over performance for large data. It is likely that pagination, compression, and partial responses will become a standard pattern across endpoints in the next minor release (`2.1.x`) — for skills, chat history, and possibly other workspace data.

2. **Robustness on heterogeneous environments** — The user explicitly mentions “slow networks” — a clearly realistic use case. Expect more such fixes for other endpoints (e.g., usage stats, long logs) if similar patterns exist. A comprehensive “overview” endpoint that lists only metadata and fetches content lazily might be the architectural next step.

Prediction: The next release (likely 2.1.0, given two functional fixes plus the earlier MCP fix) will include both of these fixes merged, and might apply the same treatment to other list endpoints even if not yet reported.

---

## 7. User Feedback Summary
The clearest user feedback comes from reporter **Moonlit-Pages** (two correlated issues). Pain points:

- **“Too large to load”** — MB-level API payloads are simply too large for the target deployment context of users on low-bandwidth or unstable connections. This is not about a feature gap but about basic usability.
- **Silent failure of complete views** — The console sections are not degraded gracefully; they fail to load entirely due to the 30-second timeout. The user is effectively blocked from using basic features.
- **Varied root causes** — The user distinguishes between workspace-specific payloads (#6633) and chat-specific payloads (#6635), which means they were debugging this across different views and narrowed down the exact endpoints — notable technical effort from a user, so definitely part of a professional or power-user base.

Satisfaction level is hard to judge positively, but the team’s response (two PRs on the same day) should be reassuring. No negative sentiment towards maintainers was expressed in the texts; frustration is directed at the software's behavior, not at the team.

---

## 8. Backlog Watch
- **No clearly “old” issues from today** (the two are from 2026-08-02, aimed at fix PRs already).
- **PR #6561 (MCP fix)** — updated 2026-08-02, originally created 2026-07-29. Still open after 5 days. This is not extreme, but it is the only item here that has been waiting without a clear associated active issue to push it forward. The fix is ready; it lacks the “urgency” of the other two. It deserves prompt review to avoid accumulation of test surface. It is the **top candidate for maintainer attention** today — it sits unmerged even as contributors push new fixes stacked on top.
  > Watch: [PR #6561](https://github.com/agentscope-ai/QwenPaw/pull/6561)

- In the long run, the maintainers should monitor the two new “slow network” fixes (#6634 and #6636) for merge conflicts since both touch the area of large payloads but on different modules. No conflicts are visible yet, but both are on the same codebase era and might overlap in utility files (e.g., for compression). A coordinated merge or a follow-up to unify the approach would reduce tech debt.

---

**Summary:**  
CoPaw is in a generally healthy state: no crisis, but the community has raised a real scaling pain point that is being addressed quickly by active contributors. The biggest risk is the unmerged MCP PR #6561, which otherwise could become stale. Everything else looks on track for a strong patch release in the coming days.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Based on the GitHub data for ZeroClaw (github.com/zeroclaw-labs/zeroclaw) for 2026-08-03, here is the project digest:

---

### 1. Today's Overview

ZeroClaw is in a period of high activity and significant architectural evolution, marked by a flurry of RFCs (Requests for Comments) and critical bug fixes. The project is currently processing a large volume of work, with 50 issues and 50 PRs updated in the last 24 hours, indicating a very active development cycle. The release of **v0.8.4** stabilizes the codebase, while the ongoing focus is on hardening security boundaries, improving reliability across various channels and providers, and expanding the runtime's core capabilities. A major theme is the proposal of several high-impact RFCs that could reshape the architecture, suggesting the project is preparing for a substantial version 0.9.0. The community is highly engaged in governance and design discussions, though a significant backlog of PRs is awaiting maintainer attention.

### 2. Releases

**v0.8.4** was released as a maintenance and hardening version. This release spans **262 commits** from **49 contributors** and focuses on:
- Expanding the memory and SOP (Standard Operating Procedure) control planes.
- Improving provider and channel reliability.
- Strengthening sandbox and credential boundaries.
- Reworking the desktop and release pipeline.

This is a stability-focused release with no major new features, likely serving as a solid foundation for the more ambitious changes proposed in the current RFCs.

### 3. Project Progress

Today saw the closure of several key PRs, resolving critical bugs and regressions:
- **Security Fix:** PR [#9401](https://github.com/zeroclaw-labs/zeroclaw/pull/9401) was merged, fixing a critical security issue where the shell's current working directory was not preserved through the macOS Seatbelt sandbox, and improving the security of the `sandbox-exec` binary resolution.
- **Performance Fix:** PR [#8937](https://github.com/zeroclaw-labs/zeroclaw/pull/8937) was closed, addressing issue [#8936](https://github.com/zeroclaw-labs/zeroclaw/issues/8936) by changing the `loop_detector` to stream-hash tool arguments instead of deep-cloning the entire JSON tree on every tool call, eliminating a major performance bottleneck in hot paths.
- **Provider Refactor:** PR [#9400](https://github.com/zeroclaw-labs/zeroclaw/pull/9400) was closed, which refactored and shared the duplicated OAuth-refresh retry logic across OpenAI, Gemini, Email, and xAI providers.
- **Channel Fix:** PR [#9038](https://github.com/zeroclaw-labs/zeroclaw/pull/9038) was closed, fixing the Lark channel's `send_message_url` to correctly infer the `receive_id_type` from the recipient ID prefix, rather than hardcoding it.
- **CI Fix:** PRs addressing CI issues like the duplicated rustdoc theme flag ([#8847](https://github.com/zeroclaw-labs/zeroclaw/issues/8847)) were closed, improving build pipeline stability.

### 4. Community Hot Topics

The most active discussions are centered on the project's future architecture and governance:
- **RFC: Work Lanes, Board Automation, and Label Cleanup ([#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808))** - With 17 comments, this is a long-running governance RFC aiming to streamline maintainer workflows through automation and label hygiene, indicating a desire for project scalability.
- **RFC: ZeroClaw Chat Completions profile ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603))** - With 14 comments, this is a high-demand feature to expose agent capabilities through the standard OpenAI Chat Completions API, which would greatly enhance compatibility with the broader AI ecosystem.
- **RFC: Prefer a lighter ZeroClaw core through external integrations ([#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165))** - With 10 comments, this proposes offloading "long-tail" integrations to MCP servers or plugins to keep the core lean, a key architectural decision for maintainability.
- **RFC: Goal mode for bounded autonomous session work ([#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303))** - With 9 comments, this proposes a new first-class mode for pursuing a single user objective until completion, indicating a push towards more autonomous and durable agent behavior.

### 5. Bugs & Stability

Today's reports show a strong focus on resolving high-severity bugs, especially security concerns:
- **S0 - Security Risk:** Issue [#9675](https://github.com/zeroclaw-labs/zeroclaw/issues/9675) reports that the response cache can bypass before-LLM hooks and omit request identity, a critical vulnerability under opt-in response-cache configurations. This is actively accepted and a high priority.
- **S2 - Degraded Behavior:** Issues [#9676](https://github.com/zeroclaw-labs/zeroclaw/issues/9676) and [#9690](https://github.com/zeroclaw-labs/zeroclaw/issues/9690) highlight that the `all-features` Docker variant has been unbuildable since early July due to a Rust toolchain mismatch. A fix PR [#9691](https://github.com/zeroclaw-labs/zeroclaw/pull/9691) has been opened.
- **S3 - Minor Issues:** Issue [#9672](https://github.com/zeroclaw-labs/zeroclaw/issues/9672) documents that all three `cron add` examples in the CLI help are broken, pointing to a need for better testing of CLI documentation.

### 6. Feature Requests & Roadmap Signals

The project is clearly planning for significant expansion, based on the high volume of RFCs:
- **External API Compatibility:** The RFC for a "Chat Completions profile" ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)) is a strong signal towards making ZeroClaw a drop-in replacement for OpenAI-based backends.
- **Autonomous Operation:** The RFC for "Goal mode" ([#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)) indicates a move towards more autonomous and bounded agentic workflows.
- **Architectural Refactoring:** Multiple RFCs ([#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141), [#9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487), [#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)) propose shifting to a runtime-owned session model with pluggable authentication and a unified attachment architecture, suggesting a major refactor is on the horizon, likely for v0.9.0.
- **Governance and Process:** The active RFCs on voting windows ([#9496](https://github.com/zeroclaw-labs/zeroclaw/issues/9496)) and decision queues ([#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)) show the project is maturing its governance to handle increased community contributions.

### 7. User Feedback Summary

The main pain points and use cases driving development include:
- **Reliability and Stability:** Users are facing bugs like broken CLI examples ([#9672](https://github.com/zeroclaw-labs/zeroclaw/issues/9672)), failed daemon startup ([#8578](https://github.com/zeroclaw-labs/zeroclaw/issues/8578)), and channel-specific issues in Telegram and WeChat, where PRs are actively addressing message sync and command limits.
- **Security and Trust:** There is a strong community focus on security hardening, with contributions on sandbox escapes ([#9401](https://github.com/zeroclaw-labs/zeroclaw/issues/9401)), shell policy hardening ([#9678](https://github.com/zeroclaw-labs/zeroclaw/issues/9678)), and credential management. This indicates a user base deploying ZeroClaw in sensitive environments.
- **Desire for Ecosystem Integration:** The high demand for a Chat Completions-compatible API ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)) shows users want to leverage ZeroClaw with existing tools like Open WebUI and LangChain.

### 8. Backlog Watch

Several important items are awaiting maintainer action:
- **PRs Needing Author Action:** A large number of high-priority PRs are blocked on the author, including `fix(sop): drive cron-started headless runs` ([#9494](https://github.com/zeroclaw-labs/zeroclaw/pull/9494)), `feat(runtime): anchor context compaction to model window ratio` ([#9535](https://github.com/zeroclaw-labs/zeroclaw/pull/9535)), and `fix(wechat): persist sync cursor only after inbound batch is enqueued` ([#9313](https://github.com/zeroclaw-labs/zeroclaw/pull/9313)). These need revision to be merged.
- **Stalled Security PRs:** `fix(channels/telegram): skip unauthorized handler for non-mentioned group messages with mention_only` ([#9634](https://github.com/zeroclaw-labs/zeroclaw/pull/9634)) and `fix(config): warn on risky Codex CLI extra args` ([#9548](https://github.com/zeroclaw-labs/zeroclaw/pull/9548)) are high-risk security improvements that are also blocked on the author.
- **Long-Running Governance Items:** The "Maintainer decision queue" ([#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)) is a tracker for the many pending RFCs, including the canonical "Chat Completions profile" ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)) and the "Pluggable inbound authentication" ([#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)), which require maintainer decisions to move forward.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*