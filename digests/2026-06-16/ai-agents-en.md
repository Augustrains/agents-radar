# OpenClaw Ecosystem Digest 2026-06-16

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-16 02:32 UTC

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

Here is the OpenClaw project digest for June 16, 2026.

---

## OpenClaw Project Digest — 2026-06-16

### 1. Today's Overview
As of June 16, 2026, the OpenClaw project is experiencing **extremely high activity**, with 500 issues and 500 pull requests updated in the last 24 hours. This volume suggests a major push or hotfix cycle, likely tied to the recent `v2026.6.8-beta.2` release. While new features are advancing, the project remains heavily burdened by a significant backlog of **security-critical regressions and resource leaks** that demand maintainer and product decisions. Over 450 open/active issues indicate a high "noise floor" despite prolific PR generation.

### 2. Releases
**New Release: v2026.6.8-beta.2**
- **Highlights**: Significant improvements to Telegram and WhatsApp channel delivery. Telegram now supports structured rich text including tables, lists, expandable blockquotes, and preserved intentional line breaks. The release also features a prompt-preserving CLI backend delivery and safer rich-media handling.
- **Breaking Changes**: Not explicitly listed, but users should watch for changes in message formatting behavior and CLI output structure.
- **Migration Notes**: Users are encouraged to update their channel configurations to take full advantage of the new rich-text capabilities, especially for Telegram and WhatsApp integrations.

### 3. Project Progress
- **Merged/Closed PRs**: 82 PRs were merged or closed in the last 24 hours.
- **Key Fixes**:
    - **PR #93449**: Fixes Feishu channel message deduplication, preventing double-processing of private-chat texts.
    - **PR #93469**: Fixes agent session history repair that was stripping `partialJson` artifacts, which could corrupt tool call replay.
    - **PR #61151**: (Closed) An earlier attempt at the same `partialJson` fix was merged.
    - **PR #93463**: Adds logging for Codex app-server context compaction completion, improving observability.
    - **PR #93466**: Fixes a crash in the Feishu channel dispatch where `channelRuntime.inbound` was undefined after an upgrade.

### 4. Community Hot Topics
- **🦞 Linux/Windows Clawdbot Apps (Issue #75)**: With **109 comments** and **79 👍 reactions**, this is the most active community discussion. Users are demanding feature parity for desktop clients, indicating a strong desire for a unified cross-platform experience.
- **🦞 Text Between Tool Calls Leaks (Issue #25592)**: 32 comments. This P1 security and message-loss bug is a major pain point. Agents are leaking internal processing text (error handling, acknowledgements) to external channels, which is a significant UX and privacy concern.
- **🦞 Private Network Access Request (Issue #39604)**: While only 13 comments, it has **9 👍 reactions**. Users want an opt-in configuration (`tools.web.fetch.allowPrivateNetwork`) to allow agents to interact with internal services, a critical feature for enterprise deployment.
- **🐚 Session Context Confusion (Issue #32296)**: 15 comments. Users are reporting that the agent replies to the *previous* message instead of the *current* one, highlighting a deep session management issue that is confusing for all users.

### 5. Bugs & Stability
**Critical (P0/P1 with high impact):**
- **P0: Gateway Memory Leak (Issue #91588)** — 12 comments, 1 👍. RSS grows from 350MB to 15.5GB over days, causing OOM crashes and restart loops. **No fix PR linked yet; this is a critical infrastructure stability issue.**
- **P1: Text Between Tool Calls Leaks (Issue #25592)** — See above. High security risk.
- **P1: Session Context Confusion (Issue #32296)** — See above. High UX impact.
- **P1: Signal Daemon Race Condition (Issue #22676)** — Orphaned processes and send failures on restart. High stability impact.
- **P1: `exec` Tool Env Inheritance Broken (Issue #31583)** — A regression where environment variables from skills are not passed to subprocesses, breaking secret injection.
- **P1: "Cannot convert undefined or null to object" (Issue #38327)** — A regression on `google-vertex/gemini-3.1-pro-preview`, halting all agent processing.

**Active Fixes:**
- **PR #92040** (Open): Aims to fix custom Anthropic-compatible provider routing.
- **PR #91800** (Open): Adds content provenance to tool call hooks for better security policy enforcement.
- **PR #91533** (Open): Fixes avatar storage to be per-agent instead of global.

### 6. Feature Requests & Roadmap Signals
The following features are highly requested and have clear shape, making them candidates for the next release:
- **Tiered Bootstrap Loading (Issue #22438)** — Already implemented in **PR #22439** (Open). Likely to be merged soon as it directly addresses the high LLM token consumption problem.
- **Memory Trust Tagging (Issue #7707)** — A high-value security feature to prevent memory poisoning by untrusted sources.
- **Prebuilt Android APK (Issue #9443)** — A blocker for mobile adoption.
- **Slack Block Kit Support (Issue #12602)** — A major UX enhancement for enterprise Slack users.
- **Safe/Unsafe ClawdBot (Issue #6731)** — A safety model inspired by Rust, reflecting user demand for sandboxing and memory protection.

### 7. User Feedback Summary
- **Pain Points**: The most common complaints revolve around **security** (leaks, unauthenticated access), **stability** (memory leaks, race conditions, crash loops), and **session management** (context confusion, stale timestamps, missing context).
- **Use Cases**: Users are pushing OpenClaw into high-stakes environments like finance (demanding hard enforcement gates), internal networks (private network access), and multi-agent workflows (better sub-agent orchestration).
- **Satisfaction/Dissatisfaction**: User sentiment is mixed. There is clear excitement for the platform's capabilities (evidenced by feature requests), but frustration with the growing number of regressions and P1/P0 bugs that disrupt daily use.

### 8. Backlog Watch
The following items have been open for **months** without resolution and remain critical:
- **Issue #75 (Linux/Windows Apps)**: Created Jan 1, 2026 — 109 comments. No PR linked. This is the single most requested feature.
- **Issue #25592 (Text Leak)**: Created Feb 24, 2026 — 32 comments. A high-severity security and UX bug with no linked fix PR.
- **Issue #10659 (Masked Secrets)**: Created Feb 6, 2026 — 13 comments. A fundamental security feature that has been stuck in "needs product decision" for over four months.
- **PR #28081 (Config Auto-prune)**: Created Feb 27, 2026 — Awaiting author for weeks. A simple quality-of-life fix that is languishing.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the community digest summaries provided.

---

**Date:** 2026-06-16
**Subject:** Cross-Project Ecosystem Comparison: Personal AI Assistant & Agent OSS Landscape

### 1. Ecosystem Overview

The personal AI agent open-source ecosystem is in a phase of rapid maturation, characterized by high-velocity development, intense community engagement, and a clear shift from experimental features to production-grade stability and security. Leading projects like OpenClaw and CoPaw are managing massive volumes of daily activity (500+ items), but this scale is generating a significant "noise floor" of regressions and critical bugs, indicating that architectural debt is compounding. A strong convergence is emerging around core requirements: robust multi-channel delivery, reliable session and context management, and hardened security for enterprise deployment. While projects excitedly push new features like vision support and MCP integration, the community’s most vocal pain points center on reliability, platform-specific stability (especially Windows), and the silent failure of core components like OAuth flows and tool calls.

### 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | New Release (24h) | Health Score & Notes |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 (updated) | 500 (updated) | **Yes** (v2026.6.8-beta.2) | **High volume, moderate health** - Major push/hotfix cycle, but high backlog of P0/P1 regressions (memory leak, session confusion). |
| **NanoBot** | 4 | 25 | No | **Good health** - Healthy maintenance rhythm with a focus on stability and edge-case hardening. Minor review pipeline backlog. |
| **Hermes Agent** | 50 | 50 | No | **Moderate health** - High triage load with low closure rate; in "hardening" phase with critical OAuth and session-isolation bugs. |
| **PicoClaw** | 3 | 13 | **Yes** (v0.2.9-nightly) | **Good health** - In a code quality and hardening phase. A security vulnerability was closed but may not be fully patched. |
| **NanoClaw** | 0 | 12 | No | **Good health** - Active and improving, with progress on long-standing bugs (media routing, budget errors). |
| **NullClaw** | 2 | 1 | No | **Low activity** - Minimal activity; core development velocity is low, with unresolved stability issues. |
| **IronClaw** | 44 | 50 | No | **High health** - Effective execution against a defined backlog; 19 PRs merged. Focus on UX polish, OAuth fixes, and attachment pipeline. |
| **LobsterAI** | 0 | 11 | No | **Good health** - Focused release prep cycle; stable codebase with no critical bugs filed. Two stale issues from April. |
| **CoPaw** | 50 | 50 | No | **Moderate health** - Very high engagement, strong merge rate (66%), but significant bug backlog (e.g., context zero-out, long-session hang) and fragile platform stability (Windows). |
| **Moltis** | 0 | 2 | No | **Stable** - Quiet, feature-focused development; zero open bugs. |
| **ZeroClaw** | 50 | 50 | No | **Moderate health** - Heavy development for v0.9.0 milestone; significant triage work, but review bandwidth appears bottlenecked. |
| **TinyClaw** | 0 | 0 | No | **Dormant** - No activity. |
| **ZeptoClaw** | 0 | 0 | No | **Dormant** - No activity. |

### 3. OpenClaw's Position

- **Advantages vs. Peers:** OpenClaw is the ecosystem's undisputed core and performance leader. Its `v2026.6.8-beta.2` release showcases advanced rich-text delivery (tables, blockquotes) on Telegram/WhatsApp and a prompt-preserving CLI backend—features that demonstrate deeper message handling capabilities than peers like NanoBot or PicoClaw. Its community size is unmatched, as evidenced by 109 comments on a single cross-platform feature request (Issue #75).
- **Technical Approach Difference:** OpenClaw’s architecture is demonstrably more ambitious and complex, managing a massive surface area of channels, tools, and providers. However, this complexity is its primary weakness. The project is burdened by a significant backlog of critical bugs (P0 memory leak, P1 text leaks) that create a high "noise floor" and erode user trust, a problem less acute in more focused projects like IronClaw or NanoBot.
- **Community Size Comparison:** OpenClaw commands the largest community by a significant margin (e.g., 500+ items vs. 50+ for Hermes or CoPaw). This is both its greatest asset (more contributors, faster feature velocity) and its greatest liability (higher rate of regressions, harder to maintain quality).

### 4. Shared Technical Focus Areas

The following requirements are emerging across multiple projects, signaling ecosystem-wide priorities:

- **Session & Context Reliability:** Nearly all active projects grapple with this.
    - *Issue:* Session cross-contamination, context confusion, "zombie" sessions, and context zero-out are widespread.
    - *Projects:* **OpenClaw** (#32296), **Hermes Agent** (#46303), **CoPaw** (#5171), **NanoBot** (#4286).
- **OAuth & Credential Lifecycle:** A consistent pain point, especially for enterprise integrations.
    - *Issue:* Silent failures after successful OAuth, stale approvals, and credential management gaps.
    - *Projects:* **IronClaw** (#4907, #4887), **OpenClaw** (#10659), **Hermes Agent** (#46675).
- **Multi-Platform & Channel Reliability:** Demand for consistent, robust cross-platform experiences.
    - *Issue:* Fragile channel integrations, platform-specific crashes, missing features (e.g., reactions, media attachments).
    - *Projects:* **PicoClaw** (#3015), **NanoClaw** (#2778), **CoPaw** (#1911), **ZeroClaw** (#7215).
- **Attachment & Media Handling:** A common regression point.
    - *Issue:* Downloads failing or being inaccessible to agent containers; vision support is a newly merged feature but still maturing.
    - *Projects:* **NanoClaw** (#2778), **CoPaw** (#5140), **IronClaw** (#4644), **NanoBot** (#4346).
- **Security & Rate Limiting:** Relates to both safety and production use.
    - *Issue:* Text leaks between tool calls, unauthenticated access, poor error classification for rate limits/budget exhaustion.
    - *Projects:* **OpenClaw** (#25592), **NanoBot** (#4287), **NullClaw** (#957).

### 5. Differentiation Analysis

The projects are diverging along key strategic axes:

- **Feature Focus:**
    - *OpenClaw, IronClaw, ZeroClaw:* Focus on becoming **general-purpose, high-performance infrastructure** for complex agent deployments (multi-agent routing, enterprise channels, rich tool ecosystems).
    - *NanoBot, PicoClaw, NanoClaw:* Focus on **specific user experiences** with a strong emphasis on UI parity, config simplicity, and platform-specific features (e.g., silent cron jobs, WebUI control).
    - *CoPaw, LobsterAI:* Strongly focused on the **Chinese market** and enterprise channels (Feishu, WeChat Work, Xiaoyi), offering deep integration with unique local platforms.
    - *NullClaw, Moltis:* Positioned as **lighter-weight runtimes or frameworks**, with less emphasis on a full-featured client ecosystem.
- **Target Users:**
    - *Advanced/Enterprise:* OpenClaw, ZeroClaw, IronClaw, CoPaw.
    - *Hobbyist/Developer/Personal Use:* NanoBot, PicoClaw, NanoClaw, Moltis.
- **Technical Architecture:**
    - *OpenClaw & ZeroClaw:* Heaviest, most complex architectures, leading to scaling challenges but offering the most power.
    - *IronClaw:* Strong CI and testing culture, leading to better stability despite high activity.
    - *PicoClaw:* Focus on defensive coding and panic recovery ("code hardening"), signifying a Rust-inspired safety mindset.
    - *NullClaw & Moltis:* Minimalist approach with lower feature velocity but fewer regressions.

### 6. Community Momentum & Maturity

- **Tier 1: Rapidly Iterating (High Activity, High Churn):**
    - **OpenClaw:** Highest velocity but plagued by regressions. It is the most feature-rich but also the most unstable.
    - **CoPaw:** Very high engagement and strong contribution rate, but platform stability (especially Windows) and fundamental context management are serious weak points.
    - **ZeroClaw:** Heavy development towards a major milestone (v0.9.0), but review bottlenecks are a concern.
    - **IronClaw:** Strong execution and effective backlog management, making it a model of mature, high-velocity development within the ecosystem.
- **Tier 2: Actively Maturing (Moderate Activity, High Stability):**
    - **NanoBot, NanoClaw, PicoClaw:** Exhibiting healthy development rhythms with a focus on stability and hardening. These projects are building a strong foundation for production use.
    - **Hermes Agent:** In a "hardening" phase after a release, resolving critical issues that emerged from past feature velocity.
- **Tier 3: Stabilized / Low Activity:**
    - **LobsterAI, Moltis:** Stable, lower-activity projects focusing on specific feature sets.
    - **NullClaw, TinyClaw, ZeptoClaw:** Dormant or minimal activity; risk of stagnation.

### 7. Trend Signals

1.  **The "Silent Failure" Crisis:** The most disruptive trend is the proliferation of silent failures. Across the ecosystem, users are reporting that OAuth completions, tool calls, budget exhaustion, and configuration changes result in no feedback, a hang, or an incorrect status, but no error message. This is eroding user trust and is a clear signal that **user-facing observability and robust error handling are the next critical frontier for AI agent OSS.**

2.  **Architecture-Specific Packaging is a Growing Pain Point:** The demand for validated builds and testing on non-standard architectures (RISC-V) and platforms (Wayland) is increasing. The failure to provide these is locking out specific user bases and creating a fragmented user experience.

3.  **Context is King, and Its Management is Broken:** From context zero-out (CoPaw) to session cross-contamination (Hermes) to incomplete streaming (NullClaw), the ability to manage long-term, multi-turn agent sessions is the single biggest source of technical debt and user frustration. This is moving beyond a "nice-to-have" to a **core requirement for any agent expected to perform real work**.

4.  **Enterprise Integration is a Double-Edged Sword:** Projects like IronClaw and CoPaw are integrating deeply with enterprise systems (Google Workspace, Slack, Feishu), which is driving adoption. However, the complexity of OAuth flows, the fragility of these integrations, and the high-stakes nature of the use cases (finance, internal networks) mean that **reliability of these integrations is paramount. Failure here causes immediate and high-profile user churn.**

5.  **The Rise of the "Dogfooding" Agent:** IronClaw’s initiative to automate its own PR review and code repair cycle (Issues #4878, #4880) signals a meta-trend: AI agent projects are beginning to use their own technology to accelerate development. This will likely become a key differentiator for project maturity and velocity.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-16

## 1. Today's Overview
The NanoBot project is **highly active** today with 25 Pull Requests updated in the last 24 hours (21 open, 4 merged/closed) and 4 active issues. The development velocity is strong, with multiple contributors submitting fixes and features across the agent loop, provider compatibility, UI parity, and channel integrations. The project shows healthy maintenance rhythms, though the number of open PRs (21) suggests the review pipeline is slightly backed up. No new releases were cut today. Bug-fix PRs outnumber feature PRs, indicating a current focus on stability and edge-case hardening.

## 2. Releases
**No new releases today.** The latest available version remains v0.2.1 (referenced in Issue #4287). No migration notes or changelogs are available for the current period.

## 3. Project Progress
**Merged/Closed PRs in the last 24 hours (4 total):**

- **#4348** — **fix(session): keep auto compact suffix on user turn** (chengyongru)  
  `CLOSED/MERGED`. Changes idle auto-compact to preserve the recent suffix and extend backward to the containing user turn; adds regression tests.  
  [View PR](https://github.com/HKUDS/nanobot/pull/4348)

- **#4309** — **Closed Issue** — `/v1/chat/completions` always returns zero usage tokens.  
  The associated bug was fixed (likely via related work in the agent loop).  
  [View Issue](https://github.com/HKUDS/nanobot/issues/4309)

- Two other PRs marked merged/closed (details not distinguished in top-20 view).

**Key features that advanced today (open PRs with active work):**
- **Agent goal continuation context (#4359)** — fixes staleness of sustained goals in long-running tasks
- **Empty-response retry without duplicate turns (#4358)** — closes a long-standing bug (#4079)
- **Config refactoring (#4344)** — lazily resolves tool configs, preserving legacy imports

## 4. Community Hot Topics
**Most active issues and PRs by comment count and reactions:**

1. **#4287** — [bug] Empty model responses not triggering fallback to alternative models  
   *Author: glebov* | 2 comments | 0 reactions  
   The underlying need is for **reliable fallback chains** when primary models return empty completions (e.g., DeepSeek during peak hours). The user expects empty responses to be treated as fallback-eligible, but NanoBot classifies them as "non-fallbackable."  
   [View Issue](https://github.com/HKUDS/nanobot/issues/4287)

2. **#4286** — [bug] Nanobot reporting unexpected missing "sustained goal" context  
   *Author: fablau* | 1 comment | 0 reactions  
   User reports that after assigning a long-form article task, NanoBot repeatedly fails with a context error. This is **directly addressed** by PR #4359 (refresh goal continuation context), which is open and updated today.  
   [View Issue](https://github.com/HKUDS/nanobot/issues/4286)

3. **#4322** — [question, stale] `NameError: 'session_key' is not defined` after merge  
   *Author: professionelle-hypnose* | 1 comment | 0 reactions  
   A regression from a merge (f8532448) that extracted `_build_memory_context`. This blocks startup for users on the `fix/prompt-caching` branch.  
   [View Issue](https://github.com/HKUDS/nanobot/issues/4322)

**Analysis:** The community is **most concerned with reliability and regressions**. The two most active issues both relate to core agent behavior (fallback logic and context persistence) that directly impact production usage. There is also a **merge regression** affecting dev-branch users, indicating the need for better merge testing.

## 5. Bugs & Stability
**Bugs reported or addressed in the last 24 hours, ranked by severity:**

- **HIGH** — #4287: Empty model responses not triggering fallback. Affects reliability of multi-model setups. No fix PR yet; likely needs discussion.  
  [Issue](https://github.com/HKUDS/nanobot/issues/4287)

- **HIGH** — #4286: Missing "sustained goal" context during long tasks. Blocks article/essay creation workflows. **Fix PR #4359 is open and updated today.**  
  [Issue](https://github.com/HKUDS/nanobot/issues/4286) | [Fix PR](https://github.com/HKUDS/nanobot/pull/4359)

- **MEDIUM** — #4322: `NameError: session_key` crash on startup after merge. Regression affecting dev-branch users. No fix PR identified yet.  
  [Issue](https://github.com/HKUDS/nanobot/issues/4322)

- **LOW** — #4309 (closed): `/v1/chat/completions` token usage always zero. Now fixed.

**Stability improvements merged today:**
- **#4348**: Session auto-compact now preserves user-turn boundaries, preventing tool-truncation artifacts
- **#4358** (open): Empty-response retry avoids duplicate user turns

**New bugs detected (from today's open PRs):**
- **Anthropic tool ID sanitization (#4356)** — tool IDs from other providers can contain invalid characters (pipes, dots), causing 400 errors
- **WhatsApp audio transcription failures (#4353)** — raw `.ogg`/`.opus` fails with some STT providers (e.g., AssemblyAI)
- **Image path leaking (#4346)** — stripped images leak file paths instead of marking as unviewable

## 6. Feature Requests & Roadmap Signals
**User-requested features identified in today's data:**

1. **Audit logging (#4320)** — Add `tools.audit` config for agent action observability. PR open by bjoshuanoah. Likely for next release.  
   [PR](https://github.com/HKUDS/nanobot/pull/4320)

2. **Silent cron jobs (#4357)** — Allow scheduled jobs to run without auto-delivering a response ("silent" mode). Requested by franciscomaestre.  
   [PR](https://github.com/HKUDS/nanobot/pull/4357)

3. **WhatsApp read receipts (#4354)** — Mark messages as read via blue ticks. Feature-complete PR.  
   [PR](https://github.com/HKUDS/nanobot/pull/4354)

4. **Keenable search provider (#4350)** — Add research-driven web search as a built-in option.  
   [PR](https://github.com/HKUDS/nanobot/pull/4350)

5. **WebUI/config.json parity (#4313)** — Close the gap between UI settings and config.json (temperature, tool limits, memory, channels). Large PR by La-Volpe.  
   [PR](https://github.com/HKUDS/nanobot/pull/4313)

6. **Automation management view (#4330)** — WebUI surface for listing, filtering, running, pausing automations.  
   [PR](https://github.com/HKUDS/nanobot/pull/4330)

**Prediction for next version:** The config parity (#4313), audit tool (#4320), and silent cron jobs (#4357) are all well-scoped and have active PRs with tests. These are strong candidates for the next minor release.

## 7. User Feedback Summary
**Real user pain points expressed today:**
- **Unsatisfying error classification** — glebov reports that legitimate fallback scenarios (empty completions from overloaded providers) are incorrectly classified as non-fallbackable, forcing manual retries.
- **Long-task abandonment** — fablau reports that NanoBot fails mid-article creation with a "sustained goal" context error, erasing progress. This is a **high-frustration** use case.
- **Merge regression frustration** — professionelle-hypnose encountered a `NameError` after a routine merge, blocking their feature branch entirely. This suggests the development branch occasionally introduces instabilities.
- **Zero usage tracking** — alx1379 (now closed) noted that the OpenAI-compatible endpoint always returns zero token usage, making API cost tracking impossible. The fix is already in.

**Satisfaction signals:**
- No negative reactions (thumbs-down) on any issue or PR today
- Multiple contributors (franciscomaestre, chengyongru, La-Volpe) are making repeated, constructive contributions
- The project's modular provider architecture is enabling quick fixes (e.g., Mistral support in #4351)

## 8. Backlog Watch
**Important items needing maintainer attention:**

1. **#4287** — Empty model responses not triggering fallback (OPEN, 6 days old, 2 comments, 0 reactions from maintainers). This is a core reliability issue with no assigned fix PR.  
   [Issue](https://github.com/HKUDS/nanobot/issues/4287)

2. **#4322** — `NameError: session_key` crash after merge (OPEN, 3 days old, 1 comment). Marked `stale` but is a real regression blocking contributors. No fix PR exists.  
   [Issue](https://github.com/HKUDS/nanobot/issues/4322)

3. **#4286** — Missing sustained goal context (OPEN, 6 days old). PR #4359 exists but hasn't been merged yet. This is actively blocking a user's workflow.  
   [Issue](https://github.com/HKUDS/nanobot/issues/4286) | [Fix PR](https://github.com/HKUDS/nanobot/pull/4359)

4. **#4303** — MCP crash on streamableHttp session reconnect (OPEN, 5 days old). No comments from maintainers. Affects MCP server reliability.  
   [PR](https://github.com/HKUDS/nanobot/pull/4303)

**Assessment:** The project is healthy and well-maintained, but the **backlog of 21 open PRs and 3 open bugs with no maintainer response** indicates a review bottleneck. The most critical items are #4287 (fallback logic) and #4322 (merge regression), both of which directly impact user trust in production deployments.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for **2026-06-16**.

---

## Hermes Agent Project Digest — 2026-06-16

### 1. Today’s Overview
The Hermes Agent project shows **very high activity** with 50 Issues and 50 PRs updated in the last 24 hours. However, the closure rate is low relative to the volume (9 issues closed, 4 PRs merged/closed out of 100 items), indicating a high triage load and many items still under active discussion. No new releases were published today. A significant number of the most active issues involve **concurrent session isolation, MCP/OAuth authentication failures, and desktop app stability**, suggesting that the project is currently in a "hardening and bug-fixing" phase following the v0.16.0 release earlier this month.

### 2. Releases
**None.** No new releases were published in the last 24 hours.

### 3. Project Progress (Merged/Closed PRs)
Four PRs were merged or closed today:
- **Docs Update:** [#46977](https://github.com/NousResearch/hermes-agent/pull/46977) *Update Stripe Projects skill docs* — Improved documentation for the Stripe integration skill.
- **Bug Fix (Duplicate):** [#46888](https://github.com/NousResearch/hermes-agent/pull/46888) *[CLOSED]* bedrock: `converse_stream` AttributeError when boto3 < 1.34.59 — A fix for an older boto3 compatibility issue.
- **Bug Fix (Duplicate):** [#46889](https://github.com/NousResearch/hermes-agent/pull/46889) *[CLOSED]* kanban: worker exits rc=0 ... — A duplicate of the "protocol violation" fix now merged via another path.
- **Bug Fix (Duplicate):** [#46593](https://github.com/NousResearch/hermes-agent/pull/46593) *[CLOSED]* kanban: worker exits rc=0 ... — Another duplicate related to the same kanban worker error handling bug.

### 4. Community Hot Topics
The community is heavily engaged on several critical issues. The underlying need is for **robust production deployment** and **better error handling**:

- **[#7237](https://github.com/NousResearch/hermes-agent/issues/7237) [CLOSED] — "Response truncated due to output length limit"** (50 comments, 6 👍)
  - *Analysis:* This is the most active issue historically. While closed, it highlights a long-standing pain point for users generating long-form content via CLI or gateways. The high comment count suggests a deep user frustration with mid-stream truncation.

- **[#46975](https://github.com/NousResearch/hermes-agent/issues/46975) [OPEN] — Desktop app accumulates zombie dashboard backend processes** (2 comments)
  - *Analysis:* A critical stability bug for Desktop users. The issue describes 80+ zombie processes consuming ~700MB RAM after profile switching. This is a key signal for a brittle process lifecycle management system.

- **[#46303](https://github.com/NousResearch/hermes-agent/issues/46303) [OPEN] — Concurrent sessions cross-contaminate** (3 comments)
  - *Analysis:* A high-severity architectural bug. Users are reporting that two concurrent Desktop sessions share memory and git worktrees, leading to data corruption. This is a strong signal that **session isolation is a top-priority technical debt item**.

- **[#46675](https://github.com/NousResearch/hermes-agent/issues/46675) [OPEN] — Max OAuth requests rejected as third-party (HTTP 400)** (2 comments)
  - *Analysis:* This is a **P1** issue affecting users with Anthropic Max OAuth tokens. A simple single-underscore prefix (`mcp_`) is causing all tool-using requests to be rejected. A fix PR [#46687](https://github.com/NousResearch/hermes-agent/pull/46687) is already open.

### 5. Bugs & Stability
Ten new or updated bugs were reported today. Ranked by severity:

- **P1: OAuth tool-name prefix breaks Anthropic Max users** — Issue [#46675](https://github.com/NousResearch/hermes-agent/issues/46675) has a fix PR ready ([#46687](https://github.com/NousResearch/hermes-agent/pull/46687)).
- **P2: Concurrent session cross-contamination** — Issue [#46303](https://github.com/NousResearch/hermes-agent/issues/46303) is a deep-seated architectural issue with no fix yet.
- **P2: Zombie "resume_pending" sessions cause context bleed** — Issue [#46934](https://github.com/NousResearch/hermes-agent/issues/46934). Gateway sessions stuck in a recovery loop.
- **P2: Terminal commands truncated on messaging platforms** — Issue [#46941](https://github.com/NousResearch/hermes-agent/issues/46941). A display/formatting bug on platforms like Feishu.
- **P2: Background-review creates "Skill" but can't load it** — Issue [#46897](https://github.com/NousResearch/hermes-agent/issues/46897). Incorrectly reports success for unloadable skills.
- **P2: Stale `tab_id` causes HTTP 404 in Camofox** — Issue implies a bug, addressed by PR [#46982](https://github.com/NousResearch/hermes-agent/pull/46982).
- **P3: Desktop build fails on Linux (Electron download blocked)** — Issue [#46939](https://github.com/NousResearch/hermes-agent/issues/46939). Likely a regional network issue.
- **P3: "Trigger now" button broken in Cron Jobs dashboard** — Issue [#46918](https://github.com/NousResearch/hermes-agent/issues/46918). A UI/UX bug for cron management.

### 6. Feature Requests & Roadmap Signals
Several feature requests point toward **configuration flexibility, internationalization, and UX polish**:

- **Desktop Font Size Setting** ([#46097](https://github.com/NousResearch/hermes-agent/issues/46097)): High user demand (2 👍), indicating Desktop UX is a priority.
- **Global Concurrent Usage Limit** ([#44761](https://github.com/NousResearch/hermes-agent/issues/44761)): Suggests users are running local/small LLMs and need throttling.
- **Arabic Localization & Full RTL Support** ([PR #44987](https://github.com/NousResearch/hermes-agent/pull/44987)): A large PR ready to merge, indicating expansion to new language markets.
- **Suppress Background-Review Notifications** ([#46908](https://github.com/NousResearch/hermes-agent/issues/46908)): Users want granular control over notification noise.
- **WeCom Native Reply Streaming** ([PR #46992](https://github.com/NousResearch/hermes-agent/pull/46992)): New platform support (WeCom) suggests expansion into the Asian enterprise market.

**Prediction for v0.16.1/v0.17.0:** It is highly likely the next release will include the **Anthropic OAuth fix** (P1), the **Camofox tab recovery fix**, and potentially the **Arabic localization** PR, given its completeness.

### 7. User Feedback Summary
**Core Pain Points:**
1.  **"Silent failures" are a major frustration:** Users report that model switches in the Desktop app ([#46961](https://github.com/NousResearch/hermes-agent/issues/46961)) and MCP misconfigurations ([#31246](https://github.com/NousResearch/hermes-agent/issues/31246)) give zero feedback. This erodes trust in the tool.
2.  **Desktop app feels fragile:** Accumulating zombie processes ([#46975](https://github.com/NousResearch/hermes-agent/issues/46975)) and broken auto-restart on Linux ([#46984](https://github.com/NousResearch/hermes-agent/pull/46984)) suggest the Desktop packaging and lifecycle are unstable.
3.  **Concurrency is dangerous:** Users are expressing anxiety about using multiple sessions simultaneously due to the cross-contamination bug ([#46303]).
4.  **"Forced response" is counterintuitive:** A user is requesting the ability for the agent to remain silent ([#46917]), highlighting a mismatch between user expectation (quiet processing) and system behavior (always outputting a text token).

**Satisfaction Signals:**
- The community is proactively contributing high-quality feature PRs (Arabic locale, WeCom streaming, Blaxel sandbox terminal), indicating a healthy and invested contributor base.
- The near-immediate response to the P1 OAuth bug (issue and fix PR opened same day) shows a responsive development cycle.

### 8. Backlog Watch
The following items require maintainer attention due to age or importance:

- **[#31246](https://github.com/NousResearch/hermes-agent/issues/31246) [OPEN, P2] — MCP server misconfiguration is invisible:** Opened May 24. A critical usability issue for anyone trying to configure MCP servers. The "silent no-op" behavior is dangerous.
- **[#8533](https://github.com/NousResearch/hermes-agent/pull/8533) [OPEN, P0] — fix: strip API keys from request debug dumps:** Opened April 12. This is a *security* PR that has been open for over two months. It prevents API keys from leaking into debug logs. This delay is a significant security risk.
- **[#20809](https://github.com/NousResearch/hermes-agent/pull/20809) [OPEN] — feat(tools): add Blaxel cloud sandbox terminal backend:** Opened May 6. A large feature PR adding a new terminal backend, which has stalled in review.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-16

## 1. Today's Overview
PicoClaw shows **moderate activity** with 13 PRs and 3 issues touched in the last 24 hours. The project is in a **code quality and hardening phase**: 7 of the open PRs are defensive fixes for panic recovery, error handling, and type assertion safety across the codebase. A new **nightly build (v0.2.9-nightly)** was released, though flagged as potentially unstable. One **security vulnerability** (CIDR bypass via reverse proxy) was closed. Community engagement is relatively quiet, with no highly-commented items today.

## 2. Releases
**Nightly Build: v0.2.9-nightly.20260616.c1ff5aa6**  
- Automated build, **marked as potentially unstable**  
- Full changelog: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
- ⚠️ **Note**: No migration guides or breaking changes documented. Users on stable v0.2.9 should not upgrade to nightly builds in production.

## 3. Project Progress
Three PRs were merged/closed today:

- **#3096** (merged) — docs: Added PicoPaw banners to READMEs (documentation polish)  
- **#3126** (closed) — fix(web): Improved launcher allowlist bypass diagnostics, adding explicit logging for `allow_localhost_bypass` settings  
- **#3097** (closed) — feat: Added Shift+Enter hint below web chat composer for newline guidance  

**In-flight features** still open: Telegram reply-as-mention (#2975), full JSONL history restore for sessions (#3047).

## 4. Community Hot Topics
No issues or PRs in today's window have high engagement (max 10 comments, 0 reactions). The most discussed item remains:

- **#2887** [CLOSED] — OpenAI model broken on RISC-V .deb package (10 comments)  
  Underlying need: **architecture-specific packaging quality** — users on RISC-V need validated builds for popular model providers. The closure suggests a fix was applied, but no associated fix PR is visible today.

## 5. Bugs & Stability

| Issue | Severity | Status | Fix PR? |
|-------|----------|--------|---------|
| **#3069** — CIDR bypass via same-host reverse proxy | **CRITICAL** (security) | CLOSED | **#3126** (diagnostics only) — partial, no actual bypass fix visible |
| **#3015** — QQ channel connection timeout on Windows | **HIGH** (platform regression) | OPEN, stale | No fix PR |
| **#2887** — RISC-V + OpenAI not functional | **HIGH** (platform-specific) | CLOSED | No linked PR today |

**Code stability fixes** (all from contributor `chengzhichao-xydt`):  
- #3132 — panic recovery in core-path goroutines (process crash prevention)  
- #3128, #3127, #3129 — explicit Close() error handling in file, HTTP, audio paths  
- #3130 — handle json.Marshal errors gracefully in Seahorse tools  
- #3131 — type assertion safety in tool registry  

**Assessment**: Security vulnerability #3069 was closed but the main fix PR (#3126) only improves diagnostics, suggesting the actual bypass remains unpatched. This is a **medium-risk gap**.

## 6. Feature Requests & Roadmap Signals
- **#2975** (open) — Telegram reply-as-mention in group chats: strong candidate for next stable release  
- **#3047** (open) — Full JSONL history for session detail endpoint: suggests ongoing web dashboard polish  
- **no new feature requests** filed today; project is in a bug-fixing and code-hardening phase  

**Prediction**: Next stable release (v0.3.0) will likely include the Telegram mention feature (#2975), JSONL session history (#3047), and the batch of defensive coding improvements from the `chengzhichao-xydt` PRs.

## 7. User Feedback Summary
- **Positive**: Continued community contributions from external developers (7 PRs from `chengzhichao-xydt` alone)  
- **Pain points**:  
  - RISC-V users still experiencing breakage with OpenAI models (#2887) — suggests insufficient CI coverage for non-x86 architectures  
  - Windows QQ channel connection failure (#3015) remains unresolved after 9 days  
- **Reactions**: No user 👍/👎 reactions on today's items, indicating low engagement or user fatigue  

## 8. Backlog Watch
| Item | Age | Status | Attention Needed |
|------|-----|--------|-----------------|
| **#3015** — QQ channel Windows fail | 10 days | OPEN, stale | 👤 **Need maintainer response** — oldest open bug without fix |
| **#2887** — RISC-V .deb OpenAI issue | 30 days | CLOSED | Verification that user's specific issue is actually resolved |
| **#3059** — Close() error ignore linting | 8 days | OPEN, stale | Low priority — auto-merge candidate |

**Key concern**: The security vulnerability (#3069) was closed without a clear code-level fix. The maintainer should either confirm a separate fix is in progress or reopen the issue.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-16

## Today's Overview
NanoClaw saw a burst of activity today, with 12 pull requests updated in the last 24 hours — the highest single-day count observed recently — though no new releases or new issues were filed. Three PRs were merged/closed, indicating steady progress toward resolving long-standing bugs and documentation gaps. The open PR queue remains heavy (9 open items) but includes several high-impact fixes for media routing, budget error handling, and user-supplied IDs. Overall project health is **active and improving**, with maintainers addressing both infrastructure and end-user pain points.

---

## Releases
**None** — no new versions were published today.

---

## Project Progress (Merged/Closed PRs Today)

Three PRs were closed today, all authored by **Koshkoshinsk**:

### ✅ #2774 — `feat(update-nanoclaw): upgrade OneCLI gateway when its pinned version moves`
**Status: Closed | URL:** [PR #2774](https://github.com/nanocoai/nanoclaw/pull/2774)
- **Impact:** When `versions.json` pins for `onecli-gateway`/`onecli-cli` change, the update script now automatically upgrades the running gateway/CLI to match, preventing silent version mismatches. Previously, a breaking mismatch would go undetected.

### ✅ #2772 — `fix(codex): per-thread conversation archive (CDX-004)`
**Status: Closed | URL:** [PR #2772](https://github.com/nanocoai/nanoclaw/pull/2772)
- **Impact:** Codex conversation history is now archived per-thread instead of generating one file per exchange, eliminating scattered fragment files in `conversations/`. Each exchange is appended to a single thread-based archive.

### ✅ #2773 — `docs(add-codex): drop redundant TTY warning in auth note`
**Status: Closed | URL:** [PR #2773](https://github.com/nanocoai/nanoclaw/pull/2773)
- **Impact:** Removes a duplicated warning line from the `add-codex` skill documentation, reducing noise in setup instructions.

---

## Community Hot Topics

With zero issues and zero comments on PRs today, there are no highly-discussed items. However, the **most impactful open PRs** based on age and scope are:

### 🔥 #2628 — `fix(cli): honor user-supplied --id in ncl groups create`
**URL:** [PR #2628](https://github.com/nanocoai/nanoclaw/pull/2628) | **Age:** 20 days open | **Author:** eldar702
- **Analysis:** Long-standing bug where `--id` flag is silently overridden by a random UUID. Although filed 20 days ago, it has not been merged — possibly blocked by testing or review bandwidth. This is a critical usability fix affecting all CLI group creation commands.

### 🔥 #2627 — `fix(reactions): align MCP add_reaction schema with channel reality`
**URL:** [PR #2627](https://github.com/nanocoai/nanoclaw/pull/2627) | **Age:** 20 days open | **Author:** eldar702
- **Analysis:** Fixes silent reaction failures across WhatsApp/Discord/Telegram/Teams/GChat by correctly mapping emoji shortcodes to unicode per channel. Also ages without merge, suggesting it may need more cross-channel testing.

### 🔥 #2759 — `fix(agent-runner): deliver budget/billing error turns`
**URL:** [PR #2759](https://github.com/nanocoai/nanoclaw/pull/2759) | **Age:** 2 days open | **Author:** assapin
- **Analysis:** Addresses a serious bug where budget/token-exhausted errors (e.g., Anthropic rate limits) were silently dropped instead of being surfaced to the user. This is a high-impact fix for production deployments.

---

## Bugs & Stability

### 🟥 Critical

#### Budget/billing error turns dropped (PR #2759)
- **Issue:** When an LLM API returns budget/token-exhausted errors, the agent-runner currently discards the error turn instead of delivering it to the user.
- **Fix:** PR #2759 (open) changes behavior to surface these errors. **Merging urgency: high** — users may be paying for failed calls without visibility.

### 🟧 Medium

#### WhatsApp inbound media never reaches agent (PR #2778)
- **Issue:** Inbound media files (images, video, audio, documents) from WhatsApp are downloaded to a shared host path (`data/attachments/`) but agent containers only mount per-session directories (`/workspace`). The file path is never accessible inside the agent.
- **Fix:** PR #2778 (opened today) routes the media through the shared session inbox mechanism.
- **Impact:** Affects all agents receiving WhatsApp media — essentially "silent failure" on media messages.

#### `restartService` silently no-ops (PR #2626)
- **Issue:** `signal.ts:restartService()` uses `launchctl kickstart -k` with `stdio: 'ignore'`; if a prior `unload` ran, the call silently fails and the wizard reports false success.
- **Fix:** PR #2626 (open, 20 days) replaces the silent failure with an explicit error.
- **Workaround:** Manually restart the Signal service.

### 🟢 Low

#### `@onecli-sh/sdk` version notice overstates enforcement (PR #2775)
- **Issue:** The changelog's `[BREAKING]` notice misleadingly claimed the pinned version is enforced for existing installs, but the gateway upgrade is a separate operator action.
- **Fix:** PR #2775 (open) clarifies documentation.

---

## Feature Requests & Roadmap Signals

### 🔮 Near-term (likely in next release)

1. **Remote HTTP/SSE MCP Servers** (PR #2776, open, authored 2026-06-15)
   - Extends `McpServerConfig` to support remote HTTP/SSE MCP endpoints alongside existing stdio-only servers.
   - **Why it matters:** Unlocks integration with cloud-hosted MCP servers (e.g., official Strava MCP in PR #2777).
   - **Prediction:** Likely to merge within 1-2 weeks — foundational infrastructure for upcoming skills.

2. **Official Strava MCP Skill** (PR #2777, open, authored 2026-06-15)
   - Adds `/add-strava` skill with OAuth flow, token refresh, and HTTP transport wiring.
   - **Why it matters:** First example of the remote MCP architecture in action; demonstrates real-world OAuth integration.

3. **Agent container performance: `--shm-size=1g` + `--init`** (PR #2771, open)
   - Sets shared memory size to 1GB and uses `--init` for proper process reaping in agent containers.
   - **Why it matters:** Prevents Chromium crashes in `agent-browser` due to 64MB default `/dev/shm`; improves stability of browser-based agents.

### 🗺️ Longer-term signals

- **Conversation/thread archiving** (PR #2772, now merged) — indicates ongoing work on Codex persistence and conversation management.
- **OneCLI gateway upgrade automation** (PR #2774, now merged) — shows maintainer investment in deployment reliability for the OneCLI ecosystem.

---

## User Feedback Summary

No user comments or reactions were recorded today, but the following **latent user pain points** are reflected in open PRs:

| Symptom | Root Cause | User Segment Affected |
|---|---|---|
| WhatsApp media messages received but never processed (PR #2778) | Incorrect mount path for attachments | All WhatsApp users |
| Budget exhausted but agent continues silently (PR #2759) | Error turn dropped in agent-runner | Heavy API users, production deployments |
| `--id` flag ignored on group creation (PR #2628) | `genericCreate` overrides user input | CLI power users, automation scripts |
| Reaction emoji silently fail on most channels (PR #2627) | Shortcode-to-unicode mapping missing | Multi-channel bridge users |
| Signal restart fails without error (PR #2626) | `launchctl kickstart` failure hidden | Signal channel users on macOS |

**Satisfaction signals:** No new issues were filed today, suggesting users are either satisfied or the existing open PRs cover their pain points.

---

## Backlog Watch

### ⏳ Long-running open PRs needing maintainer attention

| PR | Author | Open Since | Title | Risk |
|---|---|---|---|---|
| [#2628](https://github.com/nanocoai/nanoclaw/pull/2628) | eldar702 | 20 days | `fix(cli): honor user-supplied --id in ncl groups create` | **Medium** — CLI usability regression affects all group management |
| [#2627](https://github.com/nanocoai/nanoclaw/pull/2627) | eldar702 | 20 days | `fix(reactions): align MCP add_reaction schema with channel reality` | **Medium** — Reactions silently broken on 4 of 5 supported channels |
| [#2626](https://github.com/nanocoai/nanoclaw/pull/2626) | eldar702 | 20 days | `fix(signal): replace silent restartService failure with explicit error` | **Low** — affects only Signal + macOS users, but degrades setup experience |

**Observation:** All three aged PRs are authored by **eldar702** and have received no comments or updates in 20 days. They may require maintainer review or test infrastructure before merging.

---

*Generated from GitHub data for `nanocoai/nanoclaw` as of 2026-06-16.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest generated from the provided GitHub data for **2026-06-16**.

---

## NullClaw Project Digest (2026-06-16)

### 1. Today's Overview
Project activity today is minimal, characterized by maintenance updates and unresolved user issues. No new releases were published, and no code changes were merged or closed. The two open issues, one concerning a **rate limit configuration** and another regarding **incomplete responses from local models**, indicate ongoing stability concerns in the agent runtime. The sole activity is a routine dependency update via a Dependabot pull request, suggesting that while the project is stable, core development velocity is low.

### 2. Releases
**None.** No new releases were detected in the last 24 hours.

### 3. Project Progress
**No changes merged today.** There are no closed or merged Pull Requests for this date.

### 4. Community Hot Topics
The community's focus is on two unresolved issues:

- **Issue #957: Rate limit issue** ( [Link](https://github.com/nullclaw/nullclaw/issues/957) )
  - *Activity:* 1 comment | Created: 2026-06-15 | Updated: 2026-06-15
  - *Analysis:* The user is experiencing a "config reader rate limit" while using NullClaw as a runtime. This indicates a need for clearer documentation regarding throttling configuration and adjustable thresholds. The lack of response from maintainers suggests this configuration path might not be well-exposed or documented.

- **Issue #952: [bug] Local model using ollama returns incomplete answers** ( [Link](https://github.com/nullclaw/nullclaw/issues/952) )
  - *Activity:* 1 comment | Created: 2026-06-11 | Updated: 2026-06-15
  - *Analysis:* This bug, now 5 days old without a resolution or a linked fix PR, is a critical stability concern. Users running local models (e.g., Gemma) via Ollama are getting truncated responses. The underlying need is for better handling of streaming output or token length limits when interfacing with local inference engines.

### 5. Bugs & Stability
**No new bugs were reported today.** However, the pre-existing bug **#952 (Incomplete answers from Ollama)** remains a **high-severity** issue impacting core functionality. There is currently no associated fix PR. The **rate limit issue (#957)** is classified as a **medium-severity** configuration and usability problem.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were logged today. However, the **rate limit issue (#957)** signals a strong user demand for:
- **Configurable agent throttling:** Users need the ability to adjust rate limits for the configuration reader, likely for high-throughput or non-memory workflows.
- **Better output formatting control:** The user’s requirement to enforce JSON output suggests a need for tighter control over the agent’s response structure.

**Prediction:** The next minor version may include a new configuration parameter for `output_config.reader_rate_limit_threshold` to address Issue #957.

### 7. User Feedback Summary
User feedback reveals two distinct pain points:
- **Configuration Opacity:** A user expressed confusion regarding the "config reader" rate limit, indicating that internal agent limits are not transparent or user-configurable (Issue #957).
- **Reliability with Local Models:** A second user reported that the agent fails to return complete answers when using Ollama with Gemma, leading to dissatisfaction with local model support (Issue #952).

### 8. Backlog Watch
The following item requires **immediate maintainer attention**:

- **Issue #952: [bug] Local model using ollama returns incomplete answers** ( [Link](https://github.com/nullclaw/nullclaw/issues/952) )
  - *Reasoning:* This bug has been open for 5 days with no assignee or linked PR. It represents a regression in core functionality for local model users and is likely to cause user churn if unresolved. A maintainer response or a hotfix is highly recommended.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-16

## 1. Today's Overview

IronClaw is in a period of **high activity**, with 44 issues and 50 pull requests updated in the last 24 hours, and 19 merged/closed PRs pushing substantial improvements across the Reborn stack. The project shows **intense focus on Reborn WebUI v2 UX polish**, OAuth and credential lifecycle correctness, and extension/attachment pipeline robustness. A significant volume of closed issues (13) and merged PRs (19) suggests the team is executing effectively against a well-defined backlog, though recurring themes of authentication fragmentation and tool recovery failures indicate these remain the project's chief stability battlegrounds.

## 2. Releases

**No new releases** in the last 24 hours. The project continues to ship improvements directly on `main` without formal version bumps in this window.

## 3. Project Progress

**19 PRs were merged or closed** today, bringing notable advances:

| PR | Title | Significance |
|----|-------|-------------|
| [#4929](https://github.com/nearai/ironclaw/pull/4929) | fix(traces): resolve #4559 main-merge conflicts + tenant-scoped trace-credits test | Unblocks Trace Commons agent onboarding pipeline |
| [#4947](https://github.com/nearai/ironclaw/pull/4947) | ci(bench): validate /benchmark suite against benchmarks main | Fixes stale CI benchmark pin—test suites now resolve correctly |
| [#4871](https://github.com/nearai/ironclaw/pull/4871) | feat(attachments): image attachment support for vision-capable models | **Major:** inline images now reach vision models as real multimodal content, not text pointers |
| [#4780](https://github.com/nearai/ironclaw/pull/4780) | Steer routine delivery through outbound targets | Model-visible guidance for trigger creation; Slack-aware routing |
| [#4945](https://github.com/nearai/ironclaw/pull/4945) | fix(attachments): post-merge review follow-ups for image vision (#4871) | Vision model prioritization fix + multipart boundary bug + streaming conformance |

**Closed issues** include fixes for OAuth redirects ([#4928](https://github.com/nearai/ironclaw/issues/4928) — Notion OAuth localhost callback in Railway), UI automation panel layout ([#4915](https://github.com/nearai/ironclaw/issues/4915)), extension setup flow fragmentation ([#4890](https://github.com/nearai/ironclaw/issues/4890)), and GitHub tool invocation stuck states ([#4800](https://github.com/nearai/ironclaw/issues/4800)).

## 4. Community Hot Topics

**[#4825](https://github.com/nearai/ironclaw/issues/4825) — "always allow" approvals not persisting across threads** (CLOSED, 3 comments)
The most impactful user-facing fix of the week: users who approve a capability gate with "always allow" were being re-prompted in every new thread. The resolution drops `thread_id` from persistent approval scope, making durable approvals actually durable.

**[#4908](https://github.com/nearai/ironclaw/issues/4908) — Google Calendar shows "Activate" after already active** (OPEN, 3 comments)
Confusing UX where extension status remains "Active" but the configuration dialog still displays "Activate." Underlying need: **status synchronization between extension registry, installed page, and chat auth contexts** is fragmented.

**[#4880](https://github.com/nearai/ironclaw/issues/4880) — Automate Code Review and Review Comment Resolution** (OPEN, 2 comments)
A strategic parent issue (#4878) for automating IronClaw's own PR review workflow. Signals the team's intent to **dogfood their own AI agent for development velocity**.

**[#4644](https://github.com/nearai/ironclaw/issues/4644) — Universal attachments across all channels** (OPEN, 2 comments)
A long-standing epic that generated multiple PRs this week (#4871, #4902, #4945). The community and team are co-invested in making file attachments work uniformly across Reborn, v1/v2, and OpenAI-compatible APIs.

## 5. Bugs & Stability

### Critical Severity

- **[#4942](https://github.com/nearai/ironclaw/issues/4942) — Tool calls failed silently; only appear after re-fetch/reload** (OPEN)
  GSuite tool failures invisible to user until manual refresh. Blocks real-time debugging for Google-integrated workflows. No fix PR yet.

- **[#4887](https://github.com/nearai/ironclaw/issues/4887) — Provider-backed MCP tool approval resume fails with stale capability input_ref** (OPEN)
  After approving an MCP capability (e.g., `nearai.web_search`), the resumed invocation fails before dispatch. Breaks the core OAuth approval->resume contract.

- **[#4907](https://github.com/nearai/ironclaw/issues/4907) — Run fails after successful Google OAuth instead of resuming** (OPEN)
  OAuth completes successfully, but the triggering conversation run dies. Pattern matches #4887—the approval/resume pipeline has a systemic flaw.

### High Severity

- **[#4764](https://github.com/nearai/ironclaw/issues/4764) — Denying shell approval leaves tool invocation pending with no feedback** (OPEN)
  User clicks "Deny," tool stays in "RUNNING" state indefinitely. No fix PR identified—this is a **persistent core interaction failure**.

- **[#4761](https://github.com/nearai/ironclaw/issues/4761) — Agent stops after repeated tool failures instead of recovering** (OPEN)
  Workspace file creation fails silently when the workspace path is misresolved. Agents give up rather than retrying or adapting.

- **[#4921](https://github.com/nearai/ironclaw/issues/4921) — Gmail extension run fails before producing a reply after successful auth** (OPEN)
  Full authorization flow completes, but subsequent Gmail prompts produce zero response. Regression potential in Railway environment.

### Medium Severity (active fix PRs exist)

- **[#4935](https://github.com/nearai/ironclaw/issues/4935) / [#4939](https://github.com/nearai/ironclaw/pull/4939) — Credentials are owner-scoped, not thread-scoped** (OPEN, fix PR open)
  Thread ID leaking into credential identity comparisons. Fix PR #4939 by thisisjoshford removes transient invocation IDs from ownership keys.

- **[#4917](https://github.com/nearai/ironclaw/issues/4917) — Automations never run; status numbers misleading** (CLOSED)
  Scheduled automations stay in "SCHEDULED" state forever. Now fixed—but indicates a gap in automation scheduling integration tests.

## 6. Feature Requests & Roadmap Signals

**Most likely for the next version (implied by PR activity):**

1. **Universal attachments (#4644 family)** — Image vision support (#4871, merged) and OpenAI-compat vision (#4902, open) suggest attachments going GA next release. The epic's sub-tasks show clear **incremental delivery**: image→multipart→streaming→all channels.

2. **Downloadable project files (#4933)** — A new generic path-based filesystem read API for WebChat v2, allowing agents to produce CSV, reports, and exports that users can download. Strong signal for a **productivity/workspace management** feature.

3. **Credentials as owner-scoped (#4935, #4939)** — The credential identity redesign dropping thread_id from scope keys will ship as a correctness fix but effectively enables **cross-thread OAuth reuse**, a major UX improvement.

4. **Slack user-token tool (#4941)** — A new WASM tool (`slack_user_tool`) acting as the user via personal xoxp- tokens, enabling search across all conversations and posting as the user. Signals **Slack-first personal agent use cases**.

**Longer-term signals:**

- **Coding agent cloud workflow (#4882)** — Parent issue #4878 envisions turning PRs over to an AI coding agent for automated fixes. This is a meta-feature for IronClaw's own development.
- **Automated Code Review (#4880)** — Aligned with #4882; the team wants AI to handle first-pass PR review and comment resolution.

## 7. User Feedback Summary

**Pain points** (from issue descriptions and reproduction steps):

- **OAuth/resumption double-fail**: Users experience a complete OAuth flow, then the conversation dies without output. This is the single most damaging UX issue—users believe authorization failed when it actually succeeded.
- **Status ambiguity**: "Active" and "Activate" appearing simultaneously (#4908), "SETUP NEEDED" shown for already-configured MCPs (#4925), and "AUTH NEEDED" with no clear next step (#4886). **Users cannot trust the UI's authorization state indicators.**
- **Approval fatigue**: Even for simple read-only operations (e.g., listing commits), users face multi-step approval chains (#4854). Durable approvals via #4825 fix only part of this.
- **Card layout distortion**: Expanding capabilities stretches all cards in a row (#4926) and log/doc icons are opaque (#4923). Minor but collectively erodes perceived polish.

**Satisfaction signals**:

- The fast closure of #4825 (persistent "always allow") suggests the team prioritizes high-friction UX issues.
- Image attachment support (#4871) directly addresses a commonly requested multimodal capability.
- Workspace path deduplication (#4759) and GitHub tool invocation states (#4800) were fixed quickly after reporting.

## 8. Backlog Watch

**Aging open PRs needing maintainer attention:**

- **[#3705](https://github.com/nearai/ironclaw/pull/3705) — chore(deps): bump rand from 0.8.5 to 0.8.6** (OPEN since 2026-05-16, 31 days)
  Minor dependency bump in `channels-src/wechat`. Stale for a month—likely neglected due to low priority of the WeChat channel.

- **[#3707](https://github.com/nearai/ironclaw/pull/3707) — chore(deps): bump jsonwebtoken from 9.3.1 to 10.3.0** (OPEN since 2026-05-16, 31 days)
  A **major version bump** (9.x → 10.x) that may have breaking changes. Left unmerged for a month—potential security or compatibility risk if the project stays on 9.3.1.

- **[#4876](https://github.com/nearai/ironclaw/pull/4876) — build(deps): bump everything-else group with 43 updates** (OPEN since 2026-06-14)
  Massive aggregated dependency bump including `agent-client-protocol` (0.10.4 → 0.14.0), `refinery` (0.8.16 → 0.9.2), and `rustls-native-certs`. High risk of breakage; needs review before the backlog grows.

**Aging open issues of concern:**

- **[#4644](https://github.com/nearai/ironclaw/issues/4644) — Universal attachments** (OPEN since 2026-06-09)
  While sub-tasks are being delivered, the parent epic remains open. Risk of scope creep if the format registry and cross-channel wiring stall.

- **[#4761](https://github.com/nearai/ironclaw/issues/4761) — Agent stops after repeated tool failures** (OPEN since 2026-06-11)
  Five days without a fix PR. This is a **core agent robustness issue** that undermines user trust in autonomous task completion.

**Total backlog health**: The project has **31 open PRs and 31 open issues**—exactly balanced. However, 2 dependency PRs over a month old and 1 critical agent recovery bug unfixed for 5 days suggest **dependency maintenance and agent reliability are the weakest areas** of backlog hygiene.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-06-16**.

---

# LobsterAI Project Digest – 2026-06-16

## 1. Today's Overview
The project shows moderate-to-high activity today, driven primarily by a focused release preparation cycle. No new releases were cut, but **11 pull requests** were updated in the last 24 hours (5 closed/merged, 6 open), signaling heavy integration work. The two open issues remain stale (last comment two months ago), suggesting no new critical user-facing bugs have surfaced. The majority of developer effort was concentrated on refining the **voice input (ASR) experience** and expanding the **document Artifact sharing system**. CI tooling was also updated by Dependabot across four PRs, indicating ongoing maintenance hygiene.

## 2. Releases
**None** – No new releases were published today.

## 3. Project Progress
The following features advanced or were completed today:

- **Voice Input / Dictation Refinement (merged #2163, #2160)**  
  - Removed legacy "short ASR upload" flow and `asr:recognize` IPC surface.  
  - Cowork voice input now always uses realtime ASR.  
  - Removed the Settings mode switch for `recognitionMode`.  
  - In-memory ASR quota slice ensures renderer tracks daily limits across sessions.

- **Document Artifact Support (merged #2159)**  
  - New `document_file` share source for DOCX, PPTX, XLSX, PDF, CSV, TSV.  
  - Artifact preview panel: DOCX pagination, PDF native fallback, table auto-column-width/wrapping.  
  - Updated CSP for Blob resource access in document preview.  
  - Added pdfjs font & cMap static asset configuration.

- **About Dialog Update (merged #2161)**  
  - Minor UI/content update to the "About" screen.

- **Voice Input Merge Conflict Resolution (merged #2162)**  
  - Preserved release branch's realtime-only ASR flow while keeping draft ownership, stale callback guards, session-switch cancellation, and diagnostic logs.

## 4. Community Hot Topics
The most active discussions (by recency and comment volume) are both **stale issues** (no maintainer reply in 2+ months):

- **#1426 – Adding skills via local upload has no success feedback**  
  Author reports that after uploading a skill, there is no toast/prompt, and the skill list does not refresh to show the newly added skill.  
  *Link: [Issue #1426](https://github.com/netease-youdao/LobsterAI/issues/1426)*

- **#1427 – Duplicate skill names are allowed when adding from local**  
  User can repeatedly upload the same skill file, resulting in multiple skills with identical names.  
  *Link: [Issue #1427](https://github.com/netease-youdao/LobsterAI/issues/1427)*

**Underlying need:** Users are demanding clearer feedback and UI safeguards in the skill management system—specifically, success/error notifications and deduplication logic. These two issues point to a gap in the "upload skill" UX flow.

## 5. Bugs & Stability
**No new bugs or regressions were filed today.** The two existing open issues (#1426 and #1427) are classified as **medium severity** – functional gaps (no feedback, duplicate names) but not crashes or data loss. Neither has an associated fix PR; both have been stale since April 2026. The project appears stable in the current release branch.

## 6. Feature Requests & Roadmap Signals
- **System notifications for background sessions (PR #1428 – stale, open)**  
  This PR (filed April 2026) proposes using Electron’s native `Notification` API to push system notifications when a cowork session completes or errors *while the window is unfocused*. This directly mirrors behavior in tools like Claude Code and Cursor.  
  **Prediction:** Likely to be revived for a future release (v2026.7+), as it addresses a clear competitive UX gap.

- **Document Artifact sharing (PR #2159 – merged today)**  
  While already shipped, the design docs included in this PR suggest the team is investing in **Office/PDF preview** as a first-class feature, possibly leading to more robust multi-format artifact handling.

## 7. User Feedback Summary
**Pain points (directly reported):**
1. Skill upload is "invisible" – no success message, no list refresh (#1426).
2. Duplicate skills can be created without warning (#1427).

**Derived dissatisfaction:** The skill management UI does not provide standard feedback patterns (toast, list update). Users are likely frustrated by needing to manually verify whether an action succeeded.

**No positive user feedback was captured in the last 24 hours** (no new issue comments or reactions on recent features).

## 8. Backlog Watch
The project has **two long-stale open issues** and **one long-stale open PR** that warrant maintainer attention:

| Item | Type | Stale Since | Last Action |
|------|------|-------------|-------------|
| [#1426 – Skill upload no success feedback](https://github.com/netease-youdao/LobsterAI/issues/1426) | Bug | 2026-04-03 | No reply |
| [#1427 – Duplicate skill names allowed](https://github.com/netease-youdao/LobsterAI/issues/1427) | Bug | 2026-04-03 | No reply |
| [#1428 – System notifications for sessions](https://github.com/netease-youdao/LobsterAI/pull/1428) | Feature PR | 2026-04-03 | No reviewer activity |

**Recommendation:** These three items have been untouched for over 2 months. The team should prioritize triaging both the bug reports and the feature PR to avoid user perception of project neglect.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest
**Date:** 2026-06-16

---

## Today's Overview

Moltis saw a quiet day with no new issues, releases, or merged pull requests. However, two open PRs were updated within the last 24 hours, indicating ongoing feature development. Both PRs target user-facing functionality: external agent model/effort configuration and dynamic context injection for chat sessions. The project currently shows no open bug reports or stability concerns, though the absence of closed PRs may indicate a slower integration cycle. Overall, the project appears in a stable, feature-focused development phase.

## Releases

No new releases were published today. The most recent release stands as the latest stable version.

## Project Progress

No pull requests were merged or closed today. All two active PRs remain open:

- **#1125 – Support model and effort selection for external agents**  
  Adds first-class configuration for external-agent providers, including `models` and `efforts` arrays in config, and UI grouping under `/model`.  
  *(No merged PRs today; feature has not yet advanced to merge.)*

- **#1124 – Add context command support for chat turns**  
  Introduces `chat.context_command` to run a command before each turn and append its output to the prompt context, enabling automatic runtime injection.  
  *(No merged PRs today; feature has not yet advanced to merge.)*

## Community Hot Topics

No issues or PRs have generated comments or reactions in the last 24 hours. Both open PRs are freshly created (yesterday) and have not yet attracted community discussion. The lack of engagement may reflect either a smaller user base or that these features are still under review.

## Bugs & Stability

No bugs, crashes, or regressions were reported today. The project has zero open issues, reflecting either a stable codebase or a low volume of user-reported problems. No fix PRs are pending.

## Feature Requests & Roadmap Signals

Today’s activity signals clear roadmap priorities:

1. **External agent provider extensibility** (PR #1125) – Users want to select models and effort levels when using non-native agents, suggesting demand for flexible LLM backend configuration.
2. **Dynamic context automation** (PR #1124) – The ability to inject generated runtime context per turn addresses a real pain point: manually pasting context into sessions. This feature is likely to appear in an upcoming minor release.

Both PRs are authored by `gptme-thomas`, a core contributor, indicating strong maintainer alignment with these features. No user-submitted feature requests were recorded today.

## User Feedback Summary

No explicit user feedback, pain points, or satisfaction signals were recorded today. The absence of issues or comments suggests either a satisfied user base, a quiet development period, or limited community adoption at this stage.

## Backlog Watch

No long-unanswered issues or PRs currently require maintainer attention. The only open items are PR #1125 and PR #1124, both less than 24 hours old and created by a maintainer. No stalled contributions or unanswered community requests exist in the current backlog.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — June 16, 2026

**Generated from GitHub data (agentscope-ai/CoPaw) | 2026-06-16 snapshot**

---

## 1. Today's Overview

CoPaw shows high community engagement with 50 issues and 50 PRs updated in the last 24 hours, indicating a very active development cycle. The issue resolution rate is solid — 36% of updated issues (18/50) are closed, and 66% of updated PRs (33/50) have been merged or closed. However, 32 open issues remain active, suggesting a significant bug-fixing and feature-implementation backlog. Notably, no new releases were published today, with the project currently at **v1.1.11.post2** across multiple related repositories (QwenPaw, CoPaw). The renamed `copaw → qwenpaw` transition continues to generate confusion and legacy-path issues in the community.

---

## 2. Releases

**None today.** The latest available version remains **v1.1.11.post2**, with no patch, minor, or major release published in the last 24 hours.

---

## 3. Project Progress

In the last 24 hours, **33 PRs were merged or closed** — a strong velocity. Key merged fixes and features include:

| PR # | Title | Description |
|------|-------|-------------|
| [#5192](https://github.com/agentscope-ai/QwenPaw/pull/5192) | fix(desktop): guard against Windows console crash and self-kill commands | Fixes two crash causes on Windows: Rich console error on legacy terminals (`OSError: [Errno 22]`), and self-kill commands accidentally terminating the server process. |
| [#5150](https://github.com/agentscope-ai/QwenPaw/pull/5150) | feat(yuanbao): add bot message filtering and environment variable support | Adds `accept_bot_messages` config field (default `false`) to Yuanbao channel, with bot-message detection via `from_account` prefix and env var support. |
| [#5146](https://github.com/agentscope-ai/QwenPaw/pull/5146) | fix(skill): Improve skill-slash-inject and display | Fixes bug [#5031](https://github.com/agentscope-ai/QwenPaw/issues/5031) where skill slash commands expanded full SKILL.md content in Console. Replaced with `<skill>` injection blocks. |
| [#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130) | feat(chat): add per-turn token and context usage popover | Implements a per-response token usage + context ring popover in Console's `ResponseCard`, tracking prompt/completion tokens per session. Closes long-standing feature requests [#4284](https://github.com/agentscope-ai/QwenPaw/issues/4284), [#4647](https://github.com/agentscope-ai/QwenPaw/issues/4647), [#3366](https://github.com/agentscope-ai/QwenPaw/issues/3366), [#4435](https://github.com/agentscope-ai/QwenPaw/issues/4435), [#4782](https://github.com/agentscope-ai/QwenPaw/issues/4782), [#5103](https://github.com/agentscope-ai/QwenPaw/issues/5103). |
| [#5123](https://github.com/agentscope-ai/QwenPaw/pull/5123) | feat(skill): Update skill-market (QwenPaw platform + improved UI) | Adds QwenPaw skill market endpoint, category/skill preview, and UI improvements. |
| [#4310](https://github.com/agentscope-ai/QwenPaw/pull/4310) | feat(console): show context usage | Merged context-usage indicator in chat header with normal/warning/danger levels and backend SSE coverage. |

**Notable work-in-progress PRs still open:**
- [#5203](https://github.com/agentscope-ai/QwenPaw/pull/5203) — Models Page Overhaul (provider aggregation, unified card UI)
- [#5153](https://github.com/agentscope-ai/QwenPaw/pull/5153) — Replicate Tauri instant-window startup to pywebview client
- [#5158](https://github.com/agentscope-ai/QwenPaw/pull/5158) — User input queue in Console
- [#5212](https://github.com/agentscope-ai/QwenPaw/pull/5212) — Wide mode toggle for expanded chat layout

---

## 4. Community Hot Topics

**Most active issues (by comment count):**

| Issue | Comments | Topic |
|-------|----------|-------|
| [#1911](https://github.com/agentscope-ai/QwenPaw/issues/1911) | 22 | Huawei "Xiaoyi" channel integration — agent shows up but returns error messages ("mind wandering", "network congestion"). User cannot find phone chat in CoPaw logs. Likely a channel protocol or permissions issue. |
| [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | 6 | **Attachment download regression in v1.1.11.post2** — docx/pdf gives 404 errors, while plain text (txt/md/py) works. User reports earlier fix only partially resolved. |
| [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) | 5 | **MiniMax-M2.5 model incompatibility** — thinking process returns XML format, causing skill/instruction execution failures and answer interruption. User reports across v1.1.7–1.1.8. |
| [#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181) | 5 | **Plugin dependency installer spawns visible cmd windows** — when PyPI is unreachable, pip retry loops cause infinite cmd.exe popups on Windows. |
| [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) | 4 | **Context compression deletes all context** — when agent persona file token count exceeds compression threshold, entire context is zeroed out, causing task interruption. |
| [#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167) | 4 | **Feishu CardKit streaming latency** — long replies refresh very slowly, "one character at a time," making the experience poor vs. non-streaming + chunked updates. |
| [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) | 4 | **Long conversation lockup** — QwenPaw stops responding entirely after many turns or large context. |
| [#5122](https://github.com/agentscope-ai/QwenPaw/issues/5122) | 2 | **Context compression stats vs actual API input mismatch** — compressed display shows 0.9% usage, but actual model API payload is tens of KB larger. Suspects skill metadata and MCP config inflating input context. |

**Underlying needs analysis:**
- **Channel ecosystem maturity:** The Xiaoyi (#1911) and Feishu CardKit (#5167) issues show that channel integrations remain fragile, especially for non-standard platforms. Users are enthusiastic about new channels but hit hard product-readiness gaps.
- **Context management is the #1 pain point:** Multiple issues (#5171, #5161, #5122, #5025) reveal that context compression, token tracking, and long-session stability are the most urgent reliability concerns.
- **Windows quality gap:** Issues #5192, #5181, #5138 show that Windows desktop users face unique crashes, cmd popups, and process leaks that are either platform-specific or not caught in CI.

---

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **Critical** | [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) | Long conversation causes QwenPaw to hang completely; no response. | No fix PR identified. |
| **Critical** | [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) | Context compression zeroes out all context when persona file exceeds threshold. Task interruption. | No fix PR identified. |
| **Critical** | [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) | MiniMax-M2.5 XML return breaks skill execution, leaving agent mute. | No fix PR identified; user reports across multiple versions. |
| **High** | [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | Attachment download regression (docx/pdf 404). User reports "partially fixed" but still broken. | No new fix PR for this specific issue. |
| **High** | [#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181) | Plugin pip installer spawns infinite cmd windows on Windows when network is unstable. | No fix PR identified. |
| **High** | [#5138](https://github.com/agentscope-ai/QwenPaw/issues/5138) | Windows client process count grows unbounded, memory reaches 90%+. | Fixed in [#5192](https://github.com/agentscope-ai/QwenPaw/pull/5192) (guard against crash, but root cause unclear). |
| **Medium** | [#5122](https://github.com/agentscope-ai/QwenPaw/issues/5122) | Context compression displays 0.9% usage while actual API payload is far larger. | No fix PR identified. |
| **Medium** | [#5031](https://github.com/agentscope-ai/QwenPaw/issues/5031) | Skill slash command expands full SKILL.md in Console. | Fixed in [#5146](https://github.com/agentscope-ai/QwenPaw/pull/5146). |
| **Medium** | [#5199](https://github.com/agentscope-ai/QwenPaw/issues/5199) | File attachment sending still broken post-v1.1.11.post2. | No fix PR identified. |
| **Medium** | [#5184](https://github.com/agentscope-ai/QwenPaw/issues/5184) | Local model providers not showing in v1.1.11.post2. | No fix PR identified. |
| **Low** | [#5183](https://github.com/agentscope-ai/QwenPaw/issues/5183) | Pet feature broken on Wayland (Niri WM). | Low priority; platform-specific. |
| **Low** | [#5190](https://github.com/agentscope-ai/QwenPaw/issues/5190) | WeChat Work approval interface invisible after enabling access control. | No fix PR identified. |

**Regression alert:** Issues #5140 and #5199 both report that attachment download/send functionality, which was "fixed" in earlier 1.1.11 patches, is still broken in `.post2`. This suggests the root cause was not fully addressed.

---

## 6. Feature Requests & Roadmap Signals

**High-demand user features (by engagement):**

| Feature | Issue | Interest | Likelihood for Next Release |
|---------|-------|----------|----------------------------|
| **Conversation input queue** (non-blocking send) | [#5103](https://github.com/agentscope-ai/QwenPaw/issues/5103) | 👍 1, 3 comments | **High** — PR [#5158](https://github.com/agentscope-ai/QwenPaw/pull/5158) already open. |
| **Token/context usage display** (per-turn + overall) | Multiple (#4284, #4647, #3366, #4435, #4782, #5103) | 6+ comments aggregated | **Already merged** — PR [#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130) + PR [#4310](https://github.com/agentscope-ai/QwenPaw/pull/4310) now closed. Arriving in next release. |
| **Agent self-evolution mechanism** (learn from mistakes) | [#5205](https://github.com/agentscope-ai/QwenPaw/issues/5205) | 2 comments, new | **Low** — speculative, no implementation work yet. |
| **UI layout optimization** — vertical space waste | [#5211](https://github.com/agentscope-ai/QwenPaw/issues/5211) | 2 comments, new | **Low-Medium** — PR [#5212](https://github.com/agentscope-ai/QwenPaw/pull/5212) (wide mode toggle) addresses related concern. |
| **Headroom context compression integration** | [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) | 4 comments | **Low** — proposed as plugin, no core integration work yet. |
| **Observability/tracing** (Langfuse/OpenTelemetry) | [#5009](https://github.com/agentscope-ai/QwenPaw/issues/5009) | 3 comments | **Low** — no PR yet, but community interest noted. |
| **Dialogue round count display** | [#4435](https://github.com/agentscope-ai/QwenPaw/issues/4435) | 2 comments | **Already merged** in PR [#4310](https://github.com/agentscope-ai/QwenPaw/pull/4310). |
| **cron update command** (edit existing jobs) | Issue link not provided | New PR | **High** — PR [#5210](https://github.com/agentscope-ai/QwenPaw/pull/5210) already open. |

**Roadmap signal:** The **Models Page Overhaul** PR [#5203](https://github.com/agentscope-ai/QwenPaw/pull/5203) suggests a major UI refactor toward provider aggregation and unified card UI — likely targeting v1.1.12 or v1.2.0.

---

## 7. User Feedback Summary

**Satisfaction Points:**
- Users consistently appreciate the **Feishu CardKit streaming** capability as a positive feature (#5167: "thanks for connecting the Feishu channel and CardKit streaming card").
- The **skill market** improvement PR [#5123](https://github.com/agentscope-ai/QwenPaw/pull/5123) has been well received.
- **Token/context usage display** (PR [#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130)) closes a long-standing feature request community — users have been asking for this since April.

**Pain Points:**
- **Windows stability still fragile.** Multiple users report crash loops (#5192), process leaks (#5138), cmd window spam (#5181), and Wayland incompatibility (#5183). Desktop experience is the weakest platform.
- **Attachment handling regression after multiple "fixes"** (issues #5140, #5199, #5192). The 404 download error for binary files is a repeated pain: "as mentioned before several times" (user quote from #5199).
- **Context compression bugs cause complete task loss.** The zero-out bug (#5171) is arguably the most damaging — it leads to lost conversation context and interrupted workflows with no recovery.
- **Legacy naming confusion.** The `copaw → qwenpaw` rename left behind `~/.copaw/` and `~/.qwenpaw/` directories, causing plugin install failures and path confusion (#5104). Migration was not complete.
- **Xiaoyi (Huawei) channel integration is confusing.** User sees agent on phone but gets error responses, and cannot find mobile chat logs in CoPaw (#1911). Channel documentation and debugging tools appear insufficient.

**Use Cases Driving Development:**
- Long-running agent sessions with skills, MCP tools, and multiple plugins (#5122, #5171, #5161)
- Cross-platform deployment: Windows desktop users are most vocal (#5138, #5181, #5192)
- Enterprise channel integration (Feishu, WeChat Work, Xiaoyi) — users expect production reliability (#1911, #5167, #5190)
- Analytics and cost monitoring — token usage feature request has been the #1 most-requested feature for two months

---

## 8. Backlog Watch

Issues and PRs needing maintainer attention:

| Item | Age (days) | Issue | Why Concerned |
|------|-----------|-------|---------------|
| **#1911** | 88 | Xiaoyi channel — agent shows but fails | No response from maintainers since March. Outdated by 2+ months, yet user reached out yesterday. The channel integration may be abandoned or blocked. |
| **#4625** | 25 | MiniMax M2.5 XML crash | Critical bug blocking a specific model provider. User reports across v1.1.7–1.1.8, no fix PR. The "related PR" link is empty. |
| **#5171** | 3 | Context compression zeroes out everything | **Critical severity.** Newly reported but extremely damaging. No fix PR in sight. |
| **#5025** | 8 | `submit_to_agent` session path bug | FileNotFoundError in background inter-agent tasks. User provided root cause analysis (session path generation mismatch). No fix PR. |
| **#5104** | 5 | copaw→qwenpaw rename path confusion | Affects all macOS users who did clean installs. Dual-directories cause plugin install failures. Migration tool needed. |
| **#5041** | 7 | Backup fails on unreadable files | Open PR [#5041](https://github.com/agentscope-ai/QwenPaw/pull/5041) fixes this but is still under review. Windows users affected. |
| **#5088** | 6 | Governance & sandbox interface | Open PR, "Under Review." No maintainer feedback on timeline. A foundational feature for security. |
| **#5067** | 6 | Agent OS Driver (MCP/A2A/ACP) | **Merged today** — high architectural impact. Needs careful monitoring for regressions. |

**Critical backlog risk:** Issues [#1911](https://github.com/agentscope-ai/QwenPaw/issues/1911) (88 days stale) and [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) (25 days, critical) have no maintainer interaction. The community's China-facing integration requests (Xiaoyi, WeChat Work) may be deprioritized but remain high-visibility.

---

## Project Health Summary

| Metric | Value | Assessment |
|--------|-------|------------|
| Issues updated/24h | 50 | Very high activity |
| PRs updated/24h | 50 | Very high activity |
| Issue close rate (24h) | 36% | Healthy |
| PR merge/close rate (24h) | 66% | Strong |
| New releases (24h) | 0 | Slightly behind community expectations |
| Open critical bugs | 3+ | Concerning (long-session hang, context zero-out, MiniMax crash) |
| Long-stale issues (>14d) | 2 | Need triage attention |

**Overall:** CoPaw is in a high-velocity, bug-fixing phase. The community is vibrant and vocal, especially around Windows quality, context management, and channel integrations. The token/context usage feature (finally merged) will satisfy the #1 long-standing request. However, the project needs to stabilize its regression-prone attachment handling, address the context zero-out bug with urgency, and resolve two stale critical issues to maintain trust.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for **2026-06-16**.

---

## ZeroClaw Project Digest — 2026-06-16

### 1. Today's Overview
Activity remains **very high**, with 50 issues and 50 PRs updated in the last 24 hours. The project is currently in a heavy development phase targeting the **v0.9.0** milestone (auth, security, breaking changes) and the **v0.8.1** integration queue. A significant number of issues are either in "accepted" status or waiting on author action, suggesting the maintainers are actively triaging but may be bottlenecked on review bandwidth. No new releases were published today.

### 2. Releases
**None.** No new releases were cut in the last 24 hours.

### 3. Project Progress
- **PRs merged/closed today:** 1 (PR #7669 by `singlerider`)
- **PR #7669** ([link](https://github.com/zeroclaw-labs/zeroclaw/pull/7669)) was merged: It optimized CI by switching macOS and Windows build legs from full binary linking (`cargo build`) to `cargo check`, saving CI time while still verifying platform-specific compilation.

Other notable open PRs advancing critical fixes (not yet merged):
- **PR #7754** ([link](https://github.com/zeroclaw-labs/zeroclaw/pull/7754)) — Deduplicates per-locale rustdoc assets to reduce gh-pages size.
- **PR #7671** ([link](https://github.com/zeroclaw-labs/zeroclaw/pull/7671)) — Adds`/clear` session reset command for Telegram.
- **PR #7550** ([link](https://github.com/zeroclaw-labs/zeroclaw/pull/7550)) — Centralizes Node.js version to `.nvmrc` with LTS 24.
- **PR #7215** ([link](https://github.com/zeroclaw-labs/zeroclaw/pull/7215)) — Fixes the quickstart wizard missing the `port` field for webhook channels.

### 4. Community Hot Topics
The most active discussions revolve around three themes:

- **Multi-Agent Routing (#2767)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/2767)) — 6 comments, 9 👍. This is a high-priority feature request to allow multiple isolated agents and multiple channel accounts in a single gateway. The community clearly wants heterogeneous agent fleets, not just single-instance bots.

- **Local CA/Self-Signed Certificates (#1458/#551)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/1458), [link](https://github.com/zeroclaw-labs/zeroclaw/issues/551)) — Users running custom or self-hosted inference endpoints are blocked by the inability to specify trust roots or skip SSL verification. This is a recurring pain point for enterprise and homelab deployments.

- **Channel Reply-Intent Performance (#6067)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/6067)) — 5 comments. Users want the reply-intent precheck to use a smaller model and a hard timeout to avoid blocking the main agent turn. This reflects a desire for faster, more predictable response latencies in production channels.

### 5. Bugs & Stability
Several **high-risk** bugs were reported today:

- **S2 — Per-agent MCP scoping silent no-op (#7733)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7733)) — The `mcp_bundles` field is parsed and displayed in Config but **never enforced at runtime**, making per-agent MCP isolation a silent no-op. This is a security-relevant gap. No fix PR exists yet.

- **S2 — Response cache fails for multimodal prompts (#7741)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7741)) — The cache key does not account for `[IMAGE:...]` markers, causing stale or skipped cache hits. No fix PR exists yet.

- **S2 — System prompt not refreshed after tool dispatcher swap (#7742)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7742)) — Mid-session tool changes can leave stale instructions in agent history. No fix PR exists yet.

- **S2 — Channel session persistence race condition (#7753)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7753)) — The dispatch loop processes messages for the same sender concurrently, causing ordering races in session-store mutations. Reported today.

- **S2 — Email channel missing retry for OAuth refresh (#7739)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7739)) — Unlike other provider refresh paths, email's OAuth refresh has no retry/backoff.

- **S2 — Email channel uses random UUID when Message-ID missing (#7738)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7738)) — Leads to duplicate message IDs across session reconnects.

- **S1 — `ask_user` fails in gateway WebSocket sessions (#7542)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7542)) — Closed yesterday; the fix was presumably deployed but the underlying pattern (channel closed before response) is concerning.

**Fix PRs in review for related bugs:**
- **PR #7732** ([link](https://github.com/zeroclaw-labs/zeroclaw/pull/7732)) — Fixes the self-test websocket 401 failure by adding proper authentication headers.
- **PR #7485** ([link](https://github.com/zeroclaw-labs/zeroclaw/pull/7485)) — Fixes doctor incorrectly flagging custom model providers as invalid.
- **PR #7640** ([link](https://github.com/zeroclaw-labs/zeroclaw/pull/7640)) — Fixes delegate handoff credential fallback to OAuth providers.

### 6. Feature Requests & Roadmap Signals
The following are likely to land in **v0.9.0** or **v0.8.1**:

- **Multi-Agent Routing (#2767)** — Likely a v0.9.0 headline feature. The RFC for A2A agent discovery (#7218) is a necessary dependency.
- **Per-agent `prompt_injection_mode` override (#7749)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7749)) — Allows running `full` and `compact` injection modes in the same install. Simple config enhancement, likely v0.8.x.
- **Explicit target-profile authority for delegate handoffs (#7743)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7743)) — Deny-by-default delegation with caller vs. target policy. Security-critical for multi-agent trust boundaries.
- **Native context compression as a provider pipeline decorator (#7673)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7673)) — An RFC for adding a `CompressionDecorator` to compress ChatRequest payloads before sending to the LLM. This is a performance optimization for long-context agents.
- **WebAssembly-first runtime (eliminate Node.js) (#7674)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7674)) — An RFC proposing to remove all npm dependencies from the build and runtime. If accepted, this would be a major architectural change for v0.9.0 or later.
- **Hardened CI with supply-chain scanning (#7675)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7675)) — New security CI gate for SBOM generation and dependency scanning.

### 7. User Feedback Summary
- **Pain Point: Self-hosted inference friction.** Multiple issues (#551, #1458) describe users blocked by self-signed certificate and local CA support. This is the most common complaint among homelab/enterprise users.
- **Pain Point: Configuration save round-trips break user data.** Issue #7498 (PR #7532) shows that serde defaults vs. struct Defaults disagree, causing silent field loss on config save-load cycles. This erodes user trust in config persistence.
- **Pain Point: Quickstart wizard gaps.** Issue #7173 (PR #7215) shows that the new-user FTUE fails for webhook channels because the `port` field is missing from the wizard. This directly impacts first-time user satisfaction.
- **Satisfaction: Reaction parity improving.** PR #7535 adds reaction support for WhatsApp Web, closing a long-standing gap with Telegram/Discord/Matrix. Users of WhatsApp channels will see a better experience.
- **Satisfaction: CI speed improvements.** PR #7669 makes macOS/Windows CI faster, which developers will notice as faster PR feedback loops.

### 8. Backlog Watch
The following long-standing items need maintainer attention:

- **Issue #551 (Feb 2026)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/551)) — Allow insecure HTTPS requests to OpenAI-compatible endpoints. **Status: blocked.** This is 4 months old and is a critical blocker for many self-hosted users. The related #1458 (CA support) is closed but incomplete—users still cannot easily configure custom CAs.

- **Issue #6074 (Apr 2026)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)) — Audit of 153 commits lost in bulk revert. **Status: in-progress, but no visible progress in 7 weeks.** This is a high-risk technical debt item; if not tracked, bug fixes and features may have been silently lost.

- **Issue #7038 (May 2026)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7038)) — `zeroclaw check` fails 11/11 with 401 despite valid auth profile. **Status: blocked, needs-author-action.** The reporter has not provided a reproducer, but this is a high-impact bug (the diagnostic tool itself fails).

- **Issue #6698 (May 2026)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/6698)) — Fluent locale files lag English sources. **Status: in-progress.** i18n gaps are accumulating; Chinese (zh-CN) is notably behind.

- **Issue #7218 (Jun 2026)** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7218)) — RFC for A2A agent discovery. **Status: accepted but no PR.** This is a foundational dependency for multi-agent routing (#2767). If it stalls, multi-agent routing stalls too.

- **PR #6893 (May 2026)** ([link](https://github.com/zeroclaw-labs/zeroclaw/pull/6893)) — Multi-database session backends (Postgres, Oracle, MySQL, Db2). **Size: XL, still open after 3 weeks.** This is a massive PR that needs maintainer review bandwidth. It unlocks multi-worker session persistence but carries high risk.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*