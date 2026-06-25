# OpenClaw Ecosystem Digest 2026-06-25

> Issues: 403 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-25 02:00 UTC

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

# OpenClaw Project Digest — 2026-06-25

## Today's Overview

The OpenClaw project remains highly active, with 403 issues and 500 pull requests updated in the last 24 hours. Of those, 67 issues were closed and 66 PRs were merged or closed, indicating sustained maintenance velocity. Two new beta releases (v2026.6.11-beta.1 and v2026.6.10) shipped this week, bringing enhanced channel controls and automatic fast mode for conversational turns. The community continues to engage heavily around long-standing feature requests (Linux/Windows desktop apps, now at 109 comments) and emerging regressions from the rapid release cadence.

## Releases

**v2026.6.11-beta.1** (published 2026-06-11) and **v2026.6.10** (published 2026-06-10) introduced:

- **v2026.6.11 Highlights:**
  - More capable channel control: Slack relay mode, native Mattermost `/oc_queue`, and per-DM model overrides
  - Contributions from @sjf-oa, @amknight, @xydigit-zt, @thomaszta, and @gandalf-at-lerian
  - Backend improvements for channel automation and tuning

- **v2026.6.10 Highlights:**
  - Automatic fast mode for talks: OpenClaw can enable fast mode for short conversational turns, then return to normal mode for longer runs with bounded fallback and delivery behavior (#85104, thanks @alexph-dev and @vincentkoc)
  - More reliable model routing via Zai model synthesis improvements

No explicit breaking changes or migration notes were published for either release.

## Project Progress

Today saw **66 merged/closed PRs** and **67 closed issues**, reflecting strong forward momentum. Notable advances include:

- **Session/transcript storage migration (Path 3):** PR #96625 by @jalehman flips sessions and transcripts to per-agent SQLite storage, completing the work tracked by issue #88838. Legacy `sessions.json` and JSONL files become import-only sources for `doctor`.
- **Subagent lifecycle delivery accounting:** PR #95847 by @kklouzal fixes a critical gap where background/cron-owned descendant completions could be incorrectly marked as failed instead of delivered.
- **Native Anthropic thinking block handling:** Active investigation into the `Invalid signature in thinking block` 400 error on long tool-use threads (#94228), with multiple PRs in the pipeline.
- **Cron on-exit schedule:** PR #92037 adds a new `on-exit` cron kind that wakes when a watched command exits — a "process-driven wake" enabling richer automation flows.
- **Append mode for write tool:** PR #77127 by @anyech (rebased from #75549) adds a long-requested append mode to the `write` tool, directly addressing the #40001 data-loss bug.
- **Voice-call status persistence:** PR #96624 fixes `get_status` to fall back to persistent call store when in-memory state is evicted.
- **JSON response bounds:** Multiple PRs (#96618, #96620) apply 1MiB read limits across Discord, Telegram, Feishu, Google Chat, GitHub Copilot, and other modules to prevent OOM from unbounded response parsing.
- **Model alias version comparison:** PR #96609 fixes lexicographic model sorting so `claude-opus-4-10` sorts above `claude-opus-4-9` correctly.

## Community Hot Topics

| Issue/PR | Type | Comments | Reactions | Summary |
|----------|------|----------|-----------|---------|
| [#75](https://openclaw/openclaw/issues/75) Linux/Windows Clawdbot Apps | Issue | **109** | **80 👍** | Long-running request for desktop apps beyond macOS/iOS/Android. The most popular open issue by far. |
| [#88838](https://openclaw/openclaw/issues/88838) Track core session/transcript SQLite migration | Issue | 36 | 1 👍 | Critical infrastructure tracking; Path 3 is nearly complete (PR #96625 merged today). |
| [#22676](https://openclaw/openclaw/issues/22676) Signal daemon stop() race condition | Issue | 17 | 0 👍 | SIGUSR1 restart can orphan processes and cause send failures — a stability risk for gateway deployments. |
| [#22438](https://openclaw/openclaw/issues/22438) Tiered bootstrap file loading | Issue | 17 | 0 👍 | Users want progressive context control to avoid wasting LLM tokens on large workspaces. |
| [#32473](https://openclaw/openclaw/issues/32473) Control UI requires device identity (HTTPS) | Issue | 17 | **5 👍** | Regression affecting VPS/Docker users; secure context requirement blocks remote access. |
| [#29387](https://openclaw/openclaw/issues/29387) Bootstrap files in agentDir silently ignored | Issue | 14 | **5 👍** | Per-agent directory bootstrap files are injected only from workspace, not agentDir. |
| [#12602](https://openclaw/openclaw/issues/12602) Slack Block Kit support | Issue | 13 | 0 👍 | Feature request for rich interactive responses in Slack. |
| [#48003](https://openclaw/openclaw/issues/48003) Steer mode doesn't inject mid-turn | Issue | 13 | **2 👍** | Regression in message steering; messages queue until turn completes instead of mid-turn injection. |
| [#22358](https://openclaw/openclaw/issues/22358) Post-subagent completion hook | Issue | 12 | 1 👍 | Extension hook for structured trajectory generation after subagent completion. |

The community's biggest voice is for **cross-platform desktop support** (#75), which has 4x the comments of any other issue and strong upvote support. The next tier of engagement revolves around **session state correctness** (#88838, #22676, #48003) and **configuration control** (#22438, #29387).

## Bugs & Stability

### Critical (P1, high impact)

| Issue | Summary | Fix Exists? |
|-------|---------|-------------|
| [#22676](https://openclaw/openclaw/issues/22676) Signal daemon race condition — orphaned processes, send failures | No | No |
| [#29387](https://openclaw/openclaw/issues/29387) Bootstrap files in agentDir silently ignored | No | No |
| [#48003](https://openclaw/openclaw/issues/48003) Steer mode fails to inject mid-turn | No | No |
| [#40001](https://openclaw/openclaw/issues/40001) Write tool lacks append mode — shared files overwritten | **PR #77127** (open) | Yes |
| [#86827](https://openclaw/openclaw/issues/86827) Group chat session stuck in 'failed' state — messages dropped | No | No |
| [#87109](https://openclaw/openclaw/issues/87109) Gateway heap grows to 1073MB+ at idle on macOS | No | No |
| [#95833](https://openclaw/openclaw/issues/95833) Subagent abort-settle doesn't release .jsonl.lock | No | No |
| [#95495](https://openclaw/openclaw/issues/95495) (CLOSED) v2026.6.9 silently relocates memory store — 1499 files re-embedded | Closed | Closed (regression acknowledged) |
| [#91804](https://openclaw/openclaw/issues/91804) Internal reasoning leakage in 2026.6.5 — privacy regression | No | No |
| [#39847](https://openclaw/openclaw/issues/39847) Echo contamination: internal metadata leaked in Discord | No | No |
| [#39807](https://openclaw/openclaw/issues/39807) 402 billing error causes infinite retry death spiral | No | No |
| [#78493](https://openclaw/openclaw/issues/78493) `sudo openclaw update` creates mixed ownership | No | No |
| [#86996](https://openclaw/openclaw/issues/86996) Active Memory + Codex causes long latency, hook timeouts | No | No |
| [#85030](https://openclaw/openclaw/issues/85030) MCP tools not injected into subagent sessions | No | No |

### Major (P1-P2, moderate impact)

| Issue | Summary | Fix Exists? |
|-------|---------|-------------|
| [#32473](https://openclaw/openclaw/issues/32473) Control UI requires HTTPS/localhost — blocks VPS users | No | No |
| [#38327](https://openclaw/openclaw/issues/38327) "Cannot convert undefined or null to object" with Gemini 3.1-pro | No | No |
| [#38439](https://openclaw/openclaw/issues/38439) Avatar endpoint returns 404 even with valid IDENTITY.md | No | No |
| [#39476](https://openclaw/openclaw/issues/39476) A2A sessions_send causes duplicate messages | No | No |
| [#31331](https://openclaw/openclaw/issues/31331) Docker + Sandbox can't workspaceAccess at all | No | No |
| [#72031](https://openclaw/openclaw/issues/72031) `image` tool fails for Bedrock with aws-sdk auth | No | No |
| [#58514](https://openclaw/openclaw/issues/58514) Google Chat group messages silently ignored | No | No |
| [#94228](https://openclaw/openclaw/issues/94228) Native Anthropic: thinking blocks brick long tool-use threads | No | No |
| [#85844](https://openclaw/openclaw/issues/85844) Auto-update leaves stale hashed bundle imports | No | No |
| [#95554](https://openclaw/openclaw/issues/95554) (CLOSED) v2026.6.9 Telegram richMessages breaks paragraph/table rendering | Closed | Closed (regression acknowledged) |

**Regressions are a significant concern this week** — three high-severity regressions were reported in recent releases (memory store relocation #95495, reasoning leakage #91804, Telegram rendering #95554). Two were closed but the underlying issue patterns suggest aggressive release testing may be needed.

## Feature Requests & Roadmap Signals

The most significant user-requested features, ranked by likely inclusion in next releases:

| Feature | Issue | Community Interest | Likelihood |
|---------|-------|-------------------|------------|
| Linux/Windows desktop apps | [#75](https://openclaw/openclaw/issues/75) | **109 comments, 80👍** | Low-moderate (massive scope) |
| Tiered bootstrap file loading | [#22438](https://openclaw/openclaw/issues/22438) | 17 comments | Moderate (clear use case) |
| Slack Block Kit support | [#12602](https://openclaw/openclaw/issues/12602) | 13 comments | Moderate-high (channel UX priority) |
| Post-subagent completion hook | [#22358](https://openclaw/openclaw/issues/22358) | 12 comments, 1👍 | Moderate (extension ecosystem) |
| Reaction-triggered agent turns | [#17840](https://openclaw/openclaw/issues/17840) | 6 comments | Low (niche interactivity) |
| Telegram Business Bot support | [#20786](https://openclaw/openclaw/issues/20786) | 8 comments, 6👍 | Moderate-high (telegram channel investment) |
| Capability-based permissions for skills | [#12678](https://openclaw/openclaw/issues/12678) | 6 comments | Moderate (security-focused) |
| Backup/restore utility | [#13616](https://openclaw/openclaw/issues/13616) | 8 comments | Low-moderate (operational need) |
| Gateway-lite mode (no AI harness) | [#86881](https://openclaw/openclaw/issues/86881) | 7 comments | Low (architectural scope) |
| Built-in auto-update with confirmation | [#12855](https://openclaw/openclaw/issues/12855) | 7 comments | Moderate (improves upgrade UX) |
| Path-scoped RWX permissions | [#39979](https://openclaw/openclaw/issues/39979) | 7 comments | Moderate (security) |

**Prediction for v2026.7.x:** The append mode for `write` tool (#77127) is already in PR and likely to land. The SQLite session migration (#88838/#96625) is effectively done. Next-most-likely are Slack Block Kit support (#12602), Telegram Business Bot (#20786), and tiered bootstrap loading (#22438) — all have clear implementation paths and community backing.

## User Feedback Summary

**Satisfaction signals:**
- The new release cadence (two betas this week) shows the team is shipping frequently
- Active maintainer engagement on SQLite migration and channel improvements
- Community contributors are active: multiple @xydigit-*, @moguangyu5-*, and @kklouzal PRs demonstrate a healthy contributor ecosystem

**Pain points (derived from issues):**
- **Upgrade fatigue:** Multiple regressions in consecutive releases (#95495, #91804, #95554) suggest users are experiencing disruptive behavior after minor version bumps
- **Incomplete configuration:** Features like bootstrap file loading (#29387), steer mode (#48003), and model aliasing (#96609 fix) don't behave as documented, eroding trust
- **Data-loss anxiety:** Issues like shared file overwrites (#40001), memory store relocation (#95495), and failed session state (#86827) indicate fragility in state management
- **Deployment friction:** Docker sandboxing (#31331), VPS HTTPS requirements (#32473), and sudo ownership mixing (#78493) add friction for self-hosters
- **Channel fragmentation:** Slack, Telegram, Google Chat, Feishu, and Mattermost all have distinct incompatibility issues, suggesting platform integration testing isn't keeping pace with channel additions

**Overall sentiment:** The community is **actively engaged but increasingly vocal about stability** — the high volume of P1 bugs (many tagged as regressions) indicates the rapid release pace may be trading stability for feature velocity.

## Backlog Watch

Issues and PRs requiring maintainer attention (open for extended periods, no maintainer review):

| Item | Issue/PR | Created | Last Updated | Why Stalled |
|------|----------|---------|--------------|-------------|
| [#75](https://openclaw/openclaw/issues/75) Linux/Windows apps | Issue | 2026-01-01 | 2026-06-24 | Awaiting product decision (needs-product-decision label) |
| [#88838](https://openclaw/openclaw/issues/88838) SQLite migration tracker | Issue | 2026-06-01 | 2026-06-25 | **Resolved today** via PR #96625 |
| [#7722](https://openclaw/openclaw/issues/7722) Filesystem sandboxing config | Issue | 2026-02-03 | 2026-06-24 | Needs maintainer review + product decision + security review |
| [#12678](https://openclaw/openclaw/issues/12678) Capability-based permissions | Issue | 2026-02-09 | 2026-06-24 | Needs maintainer + product + security review |
| [#13616](https://openclaw/openclaw/issues/13616) Backup/restore utility | Issue | 2026-02-10 | 2026-06-24 | Needs maintainer + product + security review |
| [#12855](https://openclaw/openclaw/issues/12855) Built-in auto-update | Issue | 2026-02-09 | 2026-06-24 | Needs maintainer + product + security review |
| [#6615](https://openclaw/openclaw/issues/6615) Denylist for exec-approvals | Issue | 2026-02-01 | 2026-06-24 | Needs maintainer + product + security review |
| [#38626](https://openclaw/openclaw/issues/38626) Subagent lifecycle observability | Issue | 2026-03-07 | 2026-06-25 | Needs maintainer + product + security review |
| [#86881](https://openclaw/openclaw/issues/86881) Gateway-lite mode | Issue | 2026-05-26 | 2026-06-24 | Needs maintainer + product + security review |

**Concerns:** Many enhancements and security-related issues have been awaiting maintainer review and product decisions for months (some since February 2026). The `needs-security-review` label appears on at least 12 open issues, suggesting a potential bottleneck in security review capacity. The `needs-product-decision` label on 15+ issues indicates the product team may be struggling to prioritize an increasingly broad feature surface.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided community digest summaries.

---

### 1. Ecosystem Overview

The open-source personal AI assistant landscape is defined by **rapid iteration** and a **high tolerance for instability** as projects race to build the "operating system" for agentic AI. The ecosystem is bifurcating into two primary archetypes: **feature-rich, generalist platforms** (OpenClaw, ZeroClaw, Hermes Agent) that aim to be the single node for multi-channel, multi-agent orchestration, and **specialized, lightweight runners** (PicoClaw, NanoClaw, TinyClaw) focused on specific hardware or execution environments. A dominant theme across all projects is the tension between **accelerated feature velocity** and **production-grade stability**, with several projects (notably OpenClaw and IronClaw) experiencing high-severity regressions from their aggressive release cadences. The community is simultaneously demanding deep new integrations (MCP, new providers, rich messaging) while vocally suffering from regressions in core reliability (token waste, session corruption, data loss), signaling that the market has not yet converged on a stable, trusted foundation.

### 2. Activity Comparison

| Project | Updated Issues (24hr) | Updated PRs (24hr) | New Releases (24hr) | Health Score (Qualitative) |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 403 | 500 | 2 | **Medium** – High velocity, but significant regressions eroding trust. |
| **NanoBot** | 18 | 44 | 0 | **Medium-High** – Positive momentum, but critical MCP security bypasses need immediate attention. |
| **Hermes Agent** | 50 | 50 | 0 | **Medium** – Intense bug-fixing cycle with critical P1 infrastructure stability issues. |
| **PicoClaw** | 13 | 8 | 0 | **Medium** – Strong security responsiveness, but PR review bottleneck stalling feature work. |
| **NanoClaw** | 0 | 18 | 0 | **Medium-High** – Healthy contributor activity with responsive maintainers, but growing PR backlog. |
| **NullClaw** | 0 | 0 | 0 | **Inactive** – No activity in the last 24 hours. |
| **IronClaw** | 17 | 27 | 0 | **Medium-Low** – High-intensity stabilization period following a production meltdown. |
| **LobsterAI** | 1 | 43 | 0 | **High** – Rapid, effective stabilization with a large batch of fixes merged. |
| **TinyClaw** | 0 | 1 | 0 | **High** – Stable and quiet; low friction, empty backlog. |
| **Moltis** | 0 | 0 | 0 | **Inactive** – No activity in the last 24 hours. |
| **CoPaw** | 23 | 50 | 0 | **Medium** – High community engagement but struggling with post-migration regressions. |
| **ZeptoClaw** | 0 | 0 | 0 | **Inactive** – No activity in the last 24 hours. |
| **ZeroClaw** | 50 | 50 | 0 | **Medium** – High velocity in security and architecture, but significant duplication in fix PRs suggests review bottlenecks. |

### 3. OpenClaw's Position

**Advantages over peers:**
- **Maturity and Breadth:** As the "core reference" implementation, OpenClaw has the most mature feature set, evidenced by its deep integration ecosystem (Slack, Mattermost, Discord, Telegram) and advanced channel controls (per-DM model overrides, relay modes).
- **Community Scale:** The sheer volume of community engagement (403 issues, 500 PRs) and its most popular issue (#75 for desktop apps with 109 comments) demonstrates a massive, invested user base that dwarfs other projects. This network effect is a significant competitive moat.
- **Active Core Development:** The SQLite session migration and the append mode for the write tool are foundational improvements that address long-standing data integrity concerns.

**Technical Approach:**
OpenClaw employs a **monolithic, gateway-centric architecture** that sits as a single control plane for multi-channel, multi-agent orchestration. This contrasts with more modular or lightweight projects.

**Community Comparison:**
OpenClaw’s community is the largest and most vocal, but also the most demanding and risk-averse. The high volume of P1 bugs and regression complaints suggests a user base that has already adopted OpenClaw for serious work and is now pushing back against the instability of its rapid release cadence. This contrasts with projects like ZeroClaw, whose community is more focused on architectural RFCs and future-state security features.

### 4. Shared Technical Focus Areas

Several requirements are emerging in parallel across multiple projects, indicating core market needs.

| Shared Focus Area | Projects Involved | Specific Needs (from digests) |
| :--- | :--- | :--- |
| **Cross-Platform Desktop / CLI** | **OpenClaw** (#75), **Hermes** (Windows UTF-8), **TinyClaw** (#281) | Users are demanding reliable, native experiences on all major operating systems, especially Windows and Linux. |
| **Advanced Channel & Messaging** | **OpenClaw** (Block Kit, Telegram Business), **NanoBot** (Mattermost, Telegram rich messages), **Hermes** (Rocket Chat, LINE security) | A race to support rich, interactive messaging formats (Block Kit, rich text) and new platforms (Mattermost, Rocket Chat, Delta Chat). Telegram compatibility is a recurring pain point. |
| **Security & Multi-Tenancy** | **OpenClaw** (RBAC), **NanoBot** (MCP bypass), **PicoClaw** (SSRF, auth), **NanoClaw** (path traversal), **ZeroClaw** (OIDC, RBAC, supply chain) | A significant shift from "it works" to "it's secure in shared environments." Requirements for OIDC, role-based access, and input/output sanitization are now mainstream. |
| **Token Efficiency & Prompt Optimization** | **OpenClaw** (tiered bootstrap), **Hermes** (lazy tool schemas, token overhead), **IronClaw** (progressive tool disclosure) | The cost and latency of LLM calls is a primary constraint. Multiple projects are building sophisticated context management (lazy loading, tiered context, progressive disclosure) to reduce waste. |
| **Sub-Agent / Delegation Architecture** | **OpenClaw** (lifecycle hooks), **Hermes** (ACP orchestration), **ZeroClaw** (delegation fixes, tool scoping) | As agents perform complex tasks, the need to spawn, manage, and scope sub-agents is universal. Correctness and security of this delegation (tool permissions, context isolation) is a critical pain point. |
| **MCP (Model Context Protocol) Integration** | **NanoBot** (security holes), **Hermes** (project-local MCP), **NanoClaw** (remote MCP servers), **CoPaw** (tool name parsing) | MCP is becoming a standard extension point, but integration is causing both security vulnerabilities and compatibility issues. |
| **Plugin / Skill Ecosystem** | **OpenClaw** (post-subagent hooks), **NanoBot** (subdirectories), **CoPaw** (pip plugins), **ZeroClaw** (discoverability) | All major platforms are investing in a developer ecosystem for extending agent capabilities. |

### 5. Differentiation Analysis

| Dimension | OpenClaw / ZeroClaw / Hermes | NanoBot / LobsterAI | PicoClaw / NanoClaw / TinyClaw |
| :--- | :--- | :--- | :--- |
| **Target User** | Developer/Teams (Self-hosted) | Consumer / Prosumer | Embedded / Lightweight / Edge |
| **Architecture** | Monolithic Gateway | Lightweight Server | CLI / Library / Embedded |
| **Primary Focus** | Multi-channel orchestration, extensibility | Ease of use, frontend UX | Low-resource execution, specific hardware |
| **Differentiator** | **The most feature-complete control plane.** ZeroClaw leans hardest into enterprise security (OIDC, RBAC). Hermes focuses on deep tool integration (ACP). | **The most polished user experience.** NanoBot has strong PWA/mobile investment. LobsterAI is aggressively fixing bugs. | **The most specific purpose.** PicoClaw is tackling enterprise SPA testing. NanoClaw has novel E2EE for Matrix. TinyClaw is purely focused on cross-platform CLI stability. |

**Key Differentiating Details:**
- **ZeroClaw** is the most forward-looking on **infrastructure security**, with RFCs for supply-chain signing (SLSA) and Wasm-first plugin runtimes.
- **NanoBot** is the most **mobile-first** project, with active development on PWA support and mobile voice transcription.
- **PicoClaw** is the only project attempting **SPA automation** (Vue/Element UI), carving a unique niche in enterprise QA/testing.
- **Hermes Agent** is the most focused on **multi-agent orchestration**, with its "Generalized ACP client" feature request to orchestrate agents like Claude Code and Codex CLI.

### 6. Community Momentum & Maturity

**Tier 1: High-Velocity, High-Instability (Active Feature Development)**
- **OpenClaw, ZeroClaw, Hermes Agent:** These are the projects pushing the boundaries of the agent platform concept. They have massive communities, rapid PR throughput, and are accepting a high level of production instability (P1 bugs, regressions) as the cost of speed. They are the most feature-rich but also the most volatile.
- **IronClaw:** An outlier in this tier due to its "post-meltdown" state. Its activity is defensive (stabilization) rather than offensive (new features), but the intensity is just as high.

**Tier 2: Stabilizing / Polishing (Mature Feature Set)**
- **LobsterAI:** After a massive batch of 41 merged PRs, this project is showing strong signs of moving from feature development to a stable maintenance phase. Its single open issue is a low-severity UX bug.
- **NanoClaw, TinyClaw:** These projects have smaller scopes and seem to be in a healthy state of incremental improvement. They lack the "ecosystem" pressure of the Tier 1 projects.
- **PicoClaw:** In a holding pattern, with a strong security posture but a stalled feature pipeline due to PR bottlenecks.

**Tier 3: Inactive / Quiet**
- **NullClaw, Moltis, ZeptoClaw:** These projects show no activity in the last 24 hours, which could indicate a temporary lull, a maintainer bottleneck, or project dormancy.

### 7. Trend Signals

1.  **The "MCP Hangover":** The Model Context Protocol is a double-edged sword. While it’s being adopted as a standard extension mechanism, rapid integration is causing significant security bypasses (NanoBot, ZeroClaw) and compatibility issues (CoPaw). This will be a key area for security audits and API standardization in the next quarter.

2.  **From "Works for Me" to "Works for an Org":** The ecosystem is shifting from single-user tooling to multi-tenant platforms. The volume of issues around OIDC, RBAC, supply-chain signing, and credential isolation (ZeroClaw, OpenClaw) is a clear signal that enterprise production deployment is a primary, unspoken requirement for a growing segment of developers.

3.  **LLM Cost is the New Memory Leak:** Token waste is the most common performance complaint. Features like lazy tool schema loading (Hermes), tiered bootstrapping (OpenClaw), and progressive tool disclosure (IronClaw) are not just nice-to-haves; they are becoming **critical for viability** as users deploy these agents for real workflows.

4.  **The Desktop is the Battleground:** The most popular open issue across the entire ecosystem is OpenClaw’s request for Linux/Windows desktop apps (#75). This is echoed in Hermes’ Windows-specific bugs and TinyClaw’s Windows CLI fix. Users are frustrated with mobile-only or web-only interfaces and want a powerful, native desktop client.

5.  **Platform Integration is Harder Than It Looks:** Almost every project has multiple active bugs related to specific messaging platforms (Telegram rich text, DingTalk timeouts, Feishu misrouting, WeChat failures). The complexity of supporting a single "Channel" abstraction across wildly different API semantics is a constant source of technical debt and user-facing bugs. This suggests a future where either the abstraction is simplified, or deep platform-specific optimization is a necessary moat.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-25

## 1. Today's Overview

NanoBot is experiencing a **high-activity period** with 18 issues and 44 pull requests updated in the last 24 hours, indicating strong community engagement and rapid development velocity. The project shows **positive momentum** with 8 closed issues and 18 merged/closed PRs today, but also reveals **two critical security vulnerabilities** in MCP `enabledTools` enforcement (#4434, #4435) that bypass intended access controls. The Telegram channel is facing **multiple regressions** from the recent v0.2.2 rich messages feature, including empty messages (#4499), unsupported format warnings on Telegram Web (#4488), and line break issues (#4470), all of which have active fix PRs underway. No new releases were published today.

---

## 2. Releases

**No new releases** in the last 24 hours. The most recent release remains **v0.2.2**.

---

## 3. Project Progress

The following PRs were **merged or closed** today, representing tangible project advancement:

- **[#4464]** `feat(provider): add kimi_coding provider for Kimi Coding Plan` — Adds dedicated Anthropic Messages API endpoint support for Kimi's paid coding plan subscribers (merged)
- **[#4475]** `feat: add OpenCode Zen and OpenCode Go as providers` — Adds two new coding-focused provider integrations (merged)
- **[#4465]** `Bug: WebUI renders <thinking/> tags as visible text` — Fixes leak of model control/template text into frontend chat UI (closed)
- **[#4470]** `telegram display bug` — Line breaks and message flickering in Telegram (closed)
- **[#4388]** `[WebUI] iOS Safari 点击输入框触发页面放大` — iOS input zoom bug fix (closed)
- **[#4463]** `feat: Support Kimi Coding Plan` — Provider integration for subscription users (closed)
- **[#4487]** `fix(webui): keep multi-file apply_patch edits` — Prevents file edit records from being lost when a single `apply_patch` modifies multiple files (merged)
- **[#4498]** `Sync/upstream 2026 06 24` — Upstream synchronization (closed as invalid)
- **[#4499]** `Telegram channel: agent replies sent as empty messages` — Empty message bug closed after identification (closed)
- **[#4442]** `Duplicate tool_use ids in streamed responses poison a session` — Session-poisoning bug fixed (closed)
- **[#4413]** `[Request] Telegram Bot API 10.1 rich messages` — Original feature request closed as implemented (closed)

Notable open PRs advancing features:
- **[#4504]** `feat: support skills in subdirectories` — Enables hierarchical skill organization
- **[#4459]** `feat: add Mattermost channel support` — New real-time messaging channel integration
- **[#4502]** `Add gateway webhook triggers` — New inbound webhook system for integration events

---

## 4. Community Hot Topics

### Most Active Issue: [#660] "Project claims to be 'ultra-lightweight' but includes bloated Node.js dependency"
- **11 comments, 5 👍** — Long-standing (Feb 2026) controversy about project's lightweight claim vs. actual Node.js dependency in Dockerfile
- **Underlying need:** Users want architectural clarity and either justification or removal of the contradiction between marketing language and technical reality. This issue remains open with high reaction count, suggesting it resonates with the broader user base.

### Most Active PRs by engagement:
- **[#4505]** `fix(telegram): add rich_message config option for Telegram Web compat` — Direct response to the most disruptive Telegram regression
- **[#4436]** `fix(tools): gate MCP resource and prompt registration behind enabledTools` — Critical security fix for #4434/#4435
- **[#4437]** `add heartbeat trigger command` — New CLI command for workspace heartbeat management

### Analysis:
The community is **most vocal about Telegram reliability** — the rich messages feature (requested in #4413) was implemented and caused cascading compatibility issues (#4488, #4499, #4470). There is tension between adding features (rich messages) and maintaining stability across all Telegram clients (Android, iOS, Web, Telegram X). The **MCP security bypass** issues are attracting attention from security-conscious users who depend on `enabledTools` for sandboxing.

---

## 5. Bugs & Stability

### Critical Severity:
| Bug | Issue | Status | Fix PR |
|-----|-------|--------|--------|
| **MCP `enabledTools` deny-all bypass exposes MCP resources/prompts** | [#4434] | **OPEN** | [#4436] (PR), [#4452] (PR) |
| **MCP `enabledTools` allowlist bypass exposes resource/prompt capabilities** | [#4435] | **OPEN** | [#4436] (PR), [#4452] (PR) |
| **Duplicate `tool_use` ids in streamed responses poison session permanently** | [#4442] | CLOSED | Included in v0.2.2 fix |

### High Severity:
| Bug | Issue | Status | Fix PR |
|-----|-------|--------|--------|
| **Telegram: agent replies sent as empty messages** | [#4499] | CLOSED | Root cause identified |
| **Telegram Web: "This message is not supported" error** | [#4488] | **OPEN** | [#4505] (PR), [#4495] (PR) |
| **DingTalk: HTTP timeout + unsupported richText formatting** | [#4497] | **OPEN** | [#4501] (PR) |
| **Telegram: line breaks not respected; message flickering** | [#4470] | CLOSED | Fix applied |
| **WebUI: Home page send doesn't navigate; stop button broken** | [#4500] | **OPEN** | No fix PR yet |

### Medium Severity:
| Bug | Issue | Status | Fix PR |
|-----|-------|--------|--------|
| **WebUI: WebM→WAV conversion fails for Xiaomi MiMo ASR** | [#4492] | **OPEN** | [#4493] (PR) |
| **WebUI: `<thinking/>` tags rendered as visible text** | [#4465] | CLOSED | Fix applied |
| **iOS Safari: input field triggers page zoom** | [#4388] | CLOSED | Fix applied |

### Regression Watch:
The **Telegram channel stability is degraded** compared to v0.2.1. Multiple fixes are in progress across 4 concurrent PRs (#4505, #4495, #4493, #4487), suggesting the team is treating this as a priority issue.

---

## 6. Feature Requests & Roadmap Signals

### Likely for Next Release:
1. **Telegram rich messages config toggle** — [#4495] proposes `richMessages: True/False` to address compatibility issues with Telegram Web and Telegram X
2. **MCP `enabledTools` full enforcement** — [#4436]/[#4452] fix security bypasses for resources and prompts
3. **DingTalk rich text + timeout fix** — [#4501] addresses production blocking issue [#4497]
4. **WebUI PWA support + mobile swipe** — [#4479] is feature-complete with manifest, service worker, and gesture navigation
5. **Kimi Coding Plan provider** — Already merged as [#4464]

### Potential for Future Releases:
1. **Mattermost channel support** — [#4459] is a full new integration with WebSocket, streaming, file uploads, emoji reactions
2. **Gateway webhook triggers** — [#4502] adds inbound webhooks for CI/CD or external event integration
3. **Skills in subdirectories** — [#4504] addresses usability needs for growing skill libraries
4. **HVTracker trust badge** — [#4503] proposes adding a supply-chain security scorecard badge to README
5. **Cross-channel sends from CLI** — [#4496] allows CLI agents to relay messages to Telegram/other channels
6. **OpenAI API authentication** — [#4490] proposes requiring auth when API binds to non-loopback interfaces

### Roadmap Signals:
- **Provider expansion trend**: OpenCode Zen/Go and Kimi Coding Plan added today indicate focus on coding-focused AI providers
- **Enterprise readiness signals**: Webhook triggers (#4502), Mattermost support (#4459), and API auth (#4490) suggest growing attention to production/enterprise use cases
- **Mobile UX investment**: PWA support (#4479) and iOS Safari fixes show commitment to mobile experience

---

## 7. User Feedback Summary

### Pain Points (reported today):
1. **"This bot is broken on Telegram Web"** — Multiple users report #4488, indicating the rich messages feature broke the web version of Telegram
2. **"I can't use the WebUI on my phone"** — iOS Safari zoom bug (#4388) and home page navigation failure (#4500) degrade mobile WebUI experience
3. **"Session just dies silently"** — The `tool_use` duplicate ID bug (#4442) caused sessions to stop working without any user-visible error
4. **"ASR transcriptions don't work with MiMo"** — WebM→WAV conversion failure (#4492) blocks voice input for Xiaomi users
5. **"DingTalk integration is timing out"** — Production logs in #4497 show connectivity and formatting failures

### Satisfaction Signals:
- **Positive Kimi integration reception** — [#4463] was merged quickly (submitted June 23 → closed June 24)
- **OpenCode providers welcomed** — [#4475] adds two new providers without controversy
- **Gratitude for quick bug fixes** — #4465 (thinking tags) and #4470 (Telegram line breaks) were both closed same-day after reporting

### Underlying Use Cases:
- **Multi-client Telegram usage**: Users simultaneously access bots on Android, iOS, Web, and Telegram X — any feature that breaks one client is immediately disruptive
- **Voice-first interaction**: WebUI voice transcription (MiMo ASR) is important for hands-free or mobile use
- **Production deployment**: DingTalk timeout issues (#4497) and no API auth (#4490) are blocking enterprise adoption
- **Skill library management**: As users accumulate skills, flat directory structure becomes painful (#4504)

---

## 8. Backlog Watch

### Long-Unanswered Issues Needing Attention:

| Issue | Age | Status | Concern |
|-------|-----|--------|---------|
| **#660** "ultra-lightweight" vs Node.js dependency | 132 days (Feb 14) | OPEN — 5 👍 | High community interest with no maintainer response on architectural direction |
| **#4434** MCP deny-all bypass (security) | 4 days | OPEN — 0 maintainer comments | Security vulnerability with fix PRs ready (#4436, #4452); needs review |
| **#4435** MCP allowlist bypass (security) | 4 days | OPEN — 0 maintainer comments | Same as #4434 — both need maintainer triage |
| **#4503** HVTracker trust badge | 1 day | OPEN — 0 comments | Low urgency but easy win for trust signals |
| **#4500** WebUI home page + stop button bugs | 1 day | OPEN — 0 comments | Affects mobile UX directly |

### Recommendation:
- **Priority 1**: Merge #4436/#4452 to close the MCP security bypasses (dangerous exposure of resources/prompts)
- **Priority 2**: Resolve #660 with a clear architectural statement — either remove the "ultra-lightweight" claim or justify the Node.js dependency
- **Priority 3**: Review and merge Telegram fix PRs (#4505, #4495) to stabilize the most-used communication channel

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-25

## Today's Overview

Hermes Agent shows **very high activity** today with 50 issues and 50 PRs updated in the last 24 hours, signaling an intense development cycle. The project maintains a healthy balance of open (39 issues, 38 PRs) and closed/merged work (11 issues, 12 PRs), though closing velocity appears slightly behind incoming volume. No new releases were published today, suggesting the team is in a consolidation and bug-fixing phase rather than preparing a major version launch. The activity is concentrated around serious stability fixes (gateway lock contention, credential loss, context corruption), feature improvements (MCP support, per-channel display, localizations), and the ongoing "scale-to-zero" infrastructure push.

## Releases

**No new releases today.** The last tagged release remains the previously noted v0.6.0/v0.17.0 (Desktop) — users continue running on those versions while the main branch accumulates fixes listed below.

## Project Progress

**12 PRs merged or closed today**, including several important fixes and feature contributions:

- **fix(tui): route /learn through command.dispatch so the prompt fires** (#52232) — Resolves a Desktop GUI bug where `/learn` showed an acknowledgment but never triggered the LLM.
- **fix(soul): installers seed real default persona, upgrade legacy empty SOUL.md** (#52246) — Fresh installs now get a real Hermes persona instead of a blank template; legacy installs upgraded in-place.
- **feat(gateway): scale-to-zero idle detection + dormant-quiesce (Phase 0)** (#52207, #52243) — Two instances (one salvaged) of the gateway-side behavior layer for suspend-when-idle functionality, building on the relay primitives already shipped.
- **fix(gateway): LINE group/room allowlist to gateway authorization** (#52237) — Security fix: allowlisted LINE groups were passing the adapter gate but silently rejected at the gateway auth layer.
- **fix(tui): prevent spurious npm install on every launch** (#52245) — TUI dependency checker was over-comparing `package-lock.json` fields, causing "Installing TUI dependencies…" + rebuild on every startup.
- **cli-code-format: code fences mangled during streaming** (#52158) — Fixed `strip` mode in `cli-code-format` stripping backticks before plugin transforms could run.
- **feat: surface Z.AI account quota usage** (#48475) — Added Z.AI/GLM account quota snapshots to the TUI `/usage` response.
- **fix: add explicit encoding="utf-8" to subprocess.run calls with text=True** (#52249) — Prevents garbled output on non-UTF-8 locales (Windows CP1252, Linux C locale).

## Community Hot Topics

### Most Active Issues

1. **[#6839 — Feature: Lazy Tool Schema Loading](https://github.com/NousResearch/hermes-agent/issues/6839)** (28 comments, 14 👍)
   - **Need:** Users want to inject only relevant tool schemas (~500 tokens) instead of all 50+ tool schemas (~3,500–5,000 tokens per call). This is the #1 token waste complaint. Multiple upstream issue references suggest maintainers are considering this but haven't committed.

2. **[#4379 — Token overhead analysis: 73% fixed overhead](https://github.com/NousResearch/hermes-agent/issues/4379)** (16 comments, 0 👍 — note the discrepancy with comment count, suggesting low visibility despite high interest)  
   - **Need:** A user-built monitoring dashboard shows ~13.9K tokens per call is fixed overhead. Heavy operational users need this fixed for cost viability.

3. **[#3725 — Rocket Chat support](https://github.com/NousResearch/hermes-agent/issues/3725)** (11 comments, 10 👍)  
   - **Need:** Community wants Rocket Chat as a message channel. The author considers it a small change (<50 lines), yet the issue has sat open since March 29.

4. **[#5257 — Generalized ACP client for multi-agent CLI orchestration](https://github.com/NousResearch/hermes-agent/issues/5257)** (11 comments, 16 👍)  
   - **Need:** Users want Hermes to orchestrate Claude Code, Codex CLI, aider, and other ACP-compatible agents from a unified CLI. This is a multi-agent future vision item.

5. **[#39691 — Integrate headroom-ai for tool output compression](https://github.com/NousResearch/hermes-agent/issues/39691)** (7 comments, 10 👍)  
   - **Need:** Current conversation-level compression is insufficient; users want per-message tool output compression with configurable quality budgets.

### Most Active PRs

- **#52245** (fix tui npm install on every launch) — High user frustration with spurious rebuilds.
- **#52250** (continuable cron jobs) — User-requested feature being salvaged from a PR that otherwise diverged from main.
- **#52247** (deterministic skill_route tool) — New skill router with readiness/abstain gates, 4 files.
- **#47705** (scope smart approval owner overrides) — Fix for #46544, scoped approvals instead of broad mode downgrades.

## Bugs & Stability

### Severity P1 (Critical)

- **[#19566 — OpenAI-Codex credential pool drops newly added credential after stale auth.json rewrite during rotation](https://github.com/NousResearch/hermes-agent/issues/19566)** — A newly added credential can be silently lost when another Hermes process rewrites `auth.json` during rotation. **No fix PR yet.** This is a security-relevant data loss bug affecting multi-credential deployments.

- **[#42449 — delegate_task corrupts parent context_length via shared singleton](https://github.com/NousResearch/hermes-agent/issues/42449)** — CLOSED, but was a critical bug where a child agent's initialization overwrote the parent's `ChatCompressor` context_length. The fix presumably went into main recently.

- **[#46762 — Telegram sendRichMessage flood-control retry ignores server retry_after](https://github.com/NousResearch/hermes-agent/issues/46762)** — CLOSED. Final response delivery could fail under Telegram flood control even though the model responded successfully.

- **[#52197 — gateway cross-process agent-cache invalidation stalls event loop, blocks Discord heartbeats](https://github.com/NousResearch/hermes-agent/issues/52197)** — OPEN, P1. Performing expensive cleanup while holding `_agent_cache_lock` can stall the asyncio loop long enough to trigger Discord heartbeat timeouts. **No fix PR yet.** This is a production-reliability issue for gateway deployments.

### Severity P2 (High)

- **[#33801 — Secret redaction corrupts code syntax in tool output](https://github.com/NousResearch/hermes-agent/issues/33801)** — API key redaction replaces values with `***` *before* writing to files or executing code, corrupting Python/Shell syntax. **No fix PR yet.**

- **[#52160 — HTTP 400 after double context compression — first message is assistant, not user](https://github.com/NousResearch/hermes-agent/issues/52160)** — After two or more compactions, the Anthropic adapter sends a request with `messages[0]` having `role: assistant`, which Anthropic rejects. **No fix PR yet.**

- **[#52212 — Non-edit platforms silently drop all tool progress](https://github.com/NousResearch/hermes-agent/issues/52212)** — QQ Bot, WeChat, Signal, email, etc. quietly discard tool progress messages even with `tool_progress_grouping: separate`. **No fix PR yet.**

- **[#52228 — Auxiliary rate-limit fallback bypassed for explicit providers](https://github.com/NousResearch/hermes-agent/issues/52228)** — When an auxiliary task specifies an explicit provider and gets a 429, the fallback chain is never triggered. **Fix PR #52251** is open.

- **[#52244 — Hermes Desktop on Windows truncates UTF-8 agent output](https://github.com/NousResearch/hermes-agent/issues/52244)** — Words cut mid-way and concatenated, making responses unreadable on Windows after the Hermes One rebranding. **No fix PR yet.**

- **[#52216 — BrokenPipeError skips connection-pool rebuild in transport-recovery gate](https://github.com/NousResearch/hermes-agent/issues/52216)** — After `max_retries` exhausted, the recovery helper has an early-return that skips pool rebuild. **No fix PR yet.**

### Severity P3 (Moderate)

- **Multiple open P3 bugs** including: Hindsight drops buffered turns on session end with `retain_every_n_turns > 1` (#36216), vision provider config not honored for Gemini (#33389), Kanban tools unavailable to the agent (#52141), and Desktop GUI PageDown key issue on Windows (#52235).

## Feature Requests & Roadmap Signals

### High-Velocity Features (likely next version)

1. **Scale-to-zero idle detection** — Two PRs merged/closed today (#52207, #52243) for gateway-side idle suspension. This is a clear infrastructure priority for hosted deployments.

2. **Per-channel display overrides** — PR #52248 allows per-channel tuning of display settings (tool progress, interim messages, reasoning display). Addresses high-traffic channel needs.

3. **Continuable cron jobs** — PR #52250 enables replying to cron briefs with context, making cron workflows interactive. Default OFF for backward compatibility.

4. **Deterministic skill router** — PR #52247 adds a `skill_route` tool with readiness and abstain gates, giving the agent explicit control over skill selection.

### Community-Requested Features (Next-Release Candidates)

| Feature | Issue/PR | Support | Likelihood |
|---------|----------|---------|------------|
| Russian localization (ru-RU) | #52137 | 1 comment, new | Low (many locales requested) |
| Multi-agent ACP client orchestration | #5257 | 16 👍, 11 comments | Medium (strategic but large) |
| Lazy tool schema loading | #6839 | 14 👍, 28 comments | **High** (top token waste concern) |
| headroom-ai tool output compression | #39691 | 10 👍, 7 comments | Medium (complementary to lazy loading) |
| Rocket Chat support | #3725 | 10 👍, 11 comments | Low (low maintainer engagement since March) |
| Configurable memory backends | #47349 | 7 comments | Medium |
| Project-local `.mcp.json` support | #51069 | CLOSED as duplicate | Already tracked elsewhere |

### Prediction for Next Version

The **scale-to-zero infrastructure** PRs and the **per-channel display** feature are shipping today, making them near-certain for the next release. The **lazy tool schema loading** (#6839) and **smart approval scoped overrides** (#47705) are the most-requested features with active maintainer discussion. Expect a minor version bump (v0.18.0?) focused on gateway reliability, token efficiency, and multi-channel control, with the scale-to-zero feature as the headline.

## User Feedback Summary

### Pain Points

1. **Token waste is the #1 complaint** — Multiple issues (#6839, #4379, #39691) all point to the same problem: Hermes burns 3,500–13,900 tokens per call on fixed overhead. Users deploying on local models or paying per-token are feeling the cost acutely.

2. **Windows/Desktop reliability issues** — Two new Windows bugs today (#52235, #52244) plus the ongoing TUI spurious npm install (#52245) suggest the Desktop experience on Windows is fragile. The UTF-8 truncation in the Hermes One rebranding is particularly concerning for user trust.

3. **Platform-gap frustration** — Non-edit platforms (QQ, WeChat, Signal, email) silently dropping tool progress (#52212) makes these gateways unusable for workflows that depend on progress feedback. Users are turning off tool_progress entirely as a workaround.

4. **Authentication/session fragility** — The credential pool dropping newly added creds (#19566), session corruption after double compression (#52160), and multi-process auth.json rewrite issues point to systemic design problems in state management.

### Satisfaction Signals

- **Scale-to-zero feature** is being built and shipped — users who requested it are getting their wish.
- **Gateway authorization fixes** (LINE, Signal, SimpleX) show maintainers are methodically closing platform-specific security gaps.
- **The `/learn` fix** (#52232) and **SOUL.md seed fix** (#52246) address basic onboarding friction that directly impacts user activation.
- **Z.AI quota visibility** (#48475) responds to a specific user need for monitoring provider limits.

## Backlog Watch

### Long-Open Issues Needing Maintainer Attention

- **[#13834 — Hermes openai-codex fails on same machine where official Codex CLI works](https://github.com/NousResearch/hermes-agent/issues/13834)** — Created April 22, 12 comments, P2, `needs-repro`. Two months without a reproducible test case. Codex CLI integration is a key feature — this should be a priority.

- **[#3725 — Rocket Chat support](https://github.com/NousResearch/hermes-agent/issues/3725)** — Created March 29, 11 comments, 10 👍, P3. The author says it's <50 lines of code. Three months unanswered suggests maintainers consider the gateway surface area frozen or have a different roadmap for new platforms.

- **[#8427 — Vertex AI provider for Gemini models](https://github.com/NousResearch/hermes-agent/pull/8427)** — PR opened April 12, still open. This is a complete implementation from a community contributor — the fact that it hasn't been merged in 2.5 months signals either maintainer bandwidth constraints or architectural hesitations about provider abstractions.

- **[#17945 — delegate_task returning HTTP 404](https://github.com/NousResearch/hermes-agent/issues/17945)** — Created April 30, P2, `needs-repro`. Blocks "auto research" capability (spawning sub-agents). Two months without resolution for a feature that appears in many use cases.

### Signals

- The **`needs-repro`** label is being applied to multiple bugs (#13834, #17945, #50663, #52244) — this is a healthy quality control practice but also indicates the team is bottlenecked on reproducing user-reported issues.
- The **`sweeper:risk-*`** labels (session-state, security-boundary, message-delivery, platform-windows) indicate an automated risk-classification system is now active. This suggests growing maturity in triage processes.
- The **10 open PRs** with 0 comments on initial review suggests the team may need more code reviewers, or these are awaiting author revisions.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-25

## Today's Overview

PicoClaw showed **high security-focused maintenance activity** today, with 13 issues closed and 8 open PRs updated—though **zero PRs were merged or closed**, indicating a review backlog. The project released no new versions. Eight of the 13 closed issues are stale **security advisories** filed on 2026-06-09 and batch-closed on 2026-06-24, covering SSRF bypass, webhook replay, command whitelist weaknesses, and authorization flaws across multiple channels. Meanwhile, the PR queue continues to accumulate: three new feature/fix PRs were updated today, but none were accepted. The project appears to be undergoing a **coordinated security patch cycle** combined with steady feature development in the PR pipeline.

## Releases

**None.** No new versions were published in the last 24 hours.

## Project Progress

**No PRs were merged or closed today.** However, the following **8 open PRs** were updated:

- **#3165** `fix(openai_compat): recover Seed XML tool calls` — Recovers Volcengine Doubao `<seed:tool_call>` XML blocks from OpenAI-compatible responses. Added by Alix-007.
- **#3166** `fix(openai_compat): use structured logger for native_search warning` — Replaces a plain `log.Printf` that was causing a build failure. Added by Alix-007.
- **#3168** `fix(model): handle error response read failures` — Improves error reporting when OpenAI-compatible model-list fetches fail to read the error body. Added by Alix-007.
- **#3169** `fix(evolution): skip cold path for heartbeat turns` — Prevents draft-mode evolution from spending tokens on periodic heartbeat checks. Stacked on #3166.
- **#3115** `Fix inline data URL media extraction for generic tool output` — Prevents session-history corruption from `data:image/...` strings in plain text tool output (e.g., `read_file`, `exec`). Added by jp39.
- **#3118** `Add remote Pico WebSocket mode to picoclaw agent` — Enables connecting the `picoclaw agent` CLI to a remote WebSocket endpoint. Added by jp39.
- **#3063** `feat: add deltachat gateway` — Adds a new Delta Chat messaging gateway. Added by trufae; stale since 2026-06-08.
- **#3116** `fix(pico): complete turn.done lifecycle signaling` — Fixes three gaps in lifecycle signaling for queued steering/follow-up messages. Added by afjcjsbx; stale since 2026-06-12.

## Community Hot Topics

- **#2404** `[Feature] Add in config to send streaming HTTP request` — The **most commented issue (13 comments, 1 👍)**. This enhancement request to add `"streaming": true` in config for LLM API streaming was **closed today**. It represents strong user demand for real-time LLM output streaming, a common expectation in AI assistant UX. [#2404](https://github.com/sipeed/picoclaw/issues/2404)

- **#3167** `咨询：PageAgent 是否有针对 Vue 等 MVVM 架构的适配方案或规划？` — A **new Chinese-language inquiry** (0 comments, created today) asking whether PageAgent supports Vue 2 + Element UI enterprise admin panels. The author describes challenges with `v-model`, component internal state, and watchers. This reflects real-world demand for **enterprise SPA support**. [#3167](https://github.com/sipeed/picoclaw/issues/3167)

- **#3063** `feat: add deltachat gateway` — Oldest open PR (since June 8) with no maintainer response. A significant feature addition for decentralized messaging. [#3063](https://github.com/sipeed/picoclaw/pull/3063)

## Bugs & Stability

**No new bugs were opened in the last 24 hours.** All 13 closed issues were **existing security advisories resolved by closure**. Notably:

- **8 security issues** (reported 2026-06-09, closed 2026-06-24) were batch-resolved, covering:
  - **SSRF bypass** via HTTP proxy (#3078) and ISATAP IPv6 literals (#3074)
  - **Command injection** via `exec` tool whitelist skipping deny-patterns (#3079) and symlink race in approval hook (#3081)
  - **Authorization bypass** in Feishu (#3082), MQTT (#3068), and WeCom (#3076) channels
  - **CSRF** in launcher first-run password setup (#3072)
  - **Duplicated execution** via LINE webhook replay (#3073)
  - **Unauthenticated config reload** via WebSocket (#3071)
  - **Untrusted skill loading** from CWD (#3075)

**Severity**: High — these patches close critical vulnerabilities that could expose internal networks, bypass authorization, or allow remote code execution. The batch closure suggests a coordinated security release is being prepared.

The open fix PRs address **lower-severity issues**: build failures (#3166), media extraction corruption (#3115), and token waste in heartbeat turns (#3169).

## Feature Requests & Roadmap Signals

- **Streaming LLM support** (#2404, closed) — High-demand feature now resolved. Likely to appear in the next release as a config option to enable server-sent event streaming for OpenAI-compatible backends.
- **Vue/MVVM PageAgent support** (#3167, new) — A clear roadmap signal. User needs DOM mutation observation, `v-model` state handling, and component tree awareness for SPA automation. Could drive a **PageAgent architectural enhancement** in the next 1-2 releases.
- **Delta Chat gateway** (PR #3063, stale) — Significant new integration that would extend PicoClaw into the decentralized messaging ecosystem. Awaiting maintainer review.
- **Remote agent WebSocket mode** (PR #3118, open) — Would allow `picoclaw agent` to operate as a remote client, enabling headless/CLI usage patterns.

**Prediction for next version**: Streaming HTTP config (#2404), Delta Chat gateway (#3063), and remote agent mode (#3118) are strong candidates. The security patches from today's issue closures will almost certainly be included.

## User Feedback Summary

- **Positive signals**: Users are actively building on PicoClaw for enterprise SPA automation (Vue backend testing), requesting streaming support, and contributing Delta Chat integration and remote agent modes.
- **Pain points**: 
  - **PageAgent struggles with modern SPA frameworks** — The Vue inquiry (#3167) highlights that MVVM state management (v-model, watchers, component lifecycle) is a major usability barrier for enterprise users. This is a **structural gap** in PageAgent's DOM-centric approach.
  - **Security posture** — While batch-fixed today, the volume of security advisories (8 in one batch) may raise trust concerns for production deployments.
  - **PR review bottleneck** — Four PRs have been open 12+ days without maintainer feedback, including a major new gateway (#3063) and core lifecycle fixes (#3116). Community contributors may feel stalled.

## Backlog Watch

| Item | Type | Created | Days Open | Concern |
|------|------|---------|-----------|---------|
| [#3063 - Delta Chat gateway](https://github.com/sipeed/picoclaw/pull/3063) | PR | 2026-06-08 | 17 | No maintainer response; major feature addition |
| [#3116 - turn.done lifecycle](https://github.com/sipeed/picoclaw/pull/3116) | PR | 2026-06-12 | 13 | Fixes core lifecycle gaps; stale |
| [#3115 - Media extraction fix](https://github.com/sipeed/picoclaw/pull/3115) | PR | 2026-06-12 | 13 | Prevents session corruption; stale |
| [#3118 - Remote WebSocket mode](https://github.com/sipeed/picoclaw/pull/3118) | PR | 2026-06-12 | 13 | New CLI capability; stale |

**All four items need maintainer review.** The three PRs from June 12 are reaching the 2-week mark without feedback, which risks contributor discouragement. The Delta Chat PR (#3063) is the longest outstanding and represents a significant architectural addition.

**Project health**: Stable with high security responsiveness, but PR throughput is a bottleneck. The project would benefit from a review round targeting the stale June 12–8 PRs.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-25

## Today's Overview

NanoClaw shows **high community engagement** today with 18 pull requests updated in the last 24 hours, though only 2 were merged/closed — suggesting a **busy review pipeline** with many pending contributions. No new releases were published, and the single open issue reflects user frustration with a recently removed feature. The project is actively addressing **security hardening**, **multi-instance messaging support**, and **infrastructure fixes**, with a notable cluster of contributions from a small group of regular committers. Overall, the project is in a **maintenance-heavy phase** with strong contributor activity but a widening backlog of open PRs.

## Releases

No new releases were published today. The most recent release history shows no tagged versions in the visible data window.

## Project Progress

**Merged/Closed PRs (2 total):**

- **[#2849 — Feat(telegram): support multiple bot instances via TELEGRAM_BOT_TOKEN_<SUFFIX>](https://github.com/nanocoai/nanoclaw/pull/2849)** [CLOSED] — Adds support for running multiple Telegram bots from a single NanoClaw instance by discovering `TELEGRAM_BOT_TOKEN_<SUFFIX>` tokens in `.env`. This directly addresses the community pain point raised in Issue #2852.
- **[#2799 — Fix(security): confine send_file reads to /workspace (CVE-2026-29611)](https://github.com/nanocoai/nanoclaw/pull/2799)** [CLOSED] — Closes a security vulnerability where `send_file` could read any container-visible file through path traversal. This is a **high-severity security fix** that prevents prompt-injected or compromised agents from exfiltrating credential state and other sensitive files.

## Community Hot Topics

**Most Active Issue:**

- **[#2852 — telegram multi-bot](https://github.com/nanocoai/nanoclaw/issues/2852)** — *0 comments, 0 reactions* — User reports that multi-bot Telegram support was removed and the current "instance" replacement doesn't work with Claude. Despite low engagement metrics, this issue is **highly significant** because the fix (PR #2849) was already merged today, suggesting the maintainers are responsive to user pain points.

**Major PR Cluster — Multi-Bot Telegram Support:**
The merged PR #2849 was **replicated as an identical re-submission** in PR #2853 (still open), likely a duplicate or follow-up. This indicates the maintainers may be iterating on the same feature rapidly.

**High-Impact Open PRs with Community Interest:**

- **[#2843 — Feat: add /learn skill](https://github.com/nanocoai/nanoclaw/pull/2843)** — New skill that distills reusable skills from any source (directory, URL, past conversations). This is a **powerful meta-feature** that lets the AI agent learn from arbitrary inputs.

- **[#2844 — Matrix native persistent E2EE adapter](https://github.com/nanocoai/nanoclaw/pull/2844)** — Replaces a WASM-crypto-based Matrix bridge with a native Rust binding, providing **persistent end-to-end encryption** for Matrix communications.

## Bugs & Stability

**Critical Severity:**

- **[CVE-2026-29611 — send_file path traversal](https://github.com/nanocoai/nanoclaw/pull/2799)** — **RESOLVED.** File read vulnerability allowing arbitrary container-visible file access. Fix merged today.

**High Severity (Open Fix PRs Exist):**

- **[Stale outbound.db journals after container kills](https://github.com/nanocoai/nanoclaw/pull/2750)** — Open for 13 days. Fixes two related failure modes where host read-only `outbound.db` handles fail after container SIGKILL, causing message loss. **Fix PR #2750 is open.**

- **[ncl socket hardening: timeout, buffer caps, fail-closed](https://github.com/nanocoai/nanoclaw/pull/2802)** — Open for 8 days. Socket transport has no request timeout or response buffer limit; could cause **indefinite hangs** or **unbounded memory use**.

- **[Folder traversal + image tag validation in ncl groups](https://github.com/nanocoai/nanoclaw/pull/2800)** — Open for 8 days. `ncl groups create --folder ../../etc` escapes `GROUPS_DIR` and bypasses security validators (CWE-22).

**Medium Severity:**

- **[Abandoned poll loops stealing test messages](https://github.com/nanocoai/nanoclaw/pull/2851)** — Poll-loop helpers continue running after timeout, stealing messages intended for subsequent tests. Open fix PR exists.

- **[Router safeParseContent fails on primitive JSON](https://github.com/nanocoai/nanoclaw/pull/2815)** — JSON primitives (numbers, booleans, strings) are not handled correctly; router returns `undefined` instead of raw text. Two PRs address this (#2801, #2815).

**Low/Operational:**

- **[OpenCode cwd and .env fallback](https://github.com/nanocoai/nanoclaw/pull/2848)** — Provider/env var loading fails in certain working directory configurations.
- **[Container-runner Docker-in-Docker permissions](https://github.com/nanocoai/nanoclaw/pull/2846)** — `/var/run/docker.sock` not mounted at correct path for DinD agent groups.
- **[q.ts missing positional params](https://github.com/nanocoai/nanoclaw/pull/2845)** — CLI tool doesn't pass positional arguments to SQL parameterized queries.

## Feature Requests & Roadmap Signals

**Likely in Next Release:**

1. **Multi-bot Telegram support** — PR #2849 merged; PR #2853 pending. The community request for running multiple Telegram bots is **now solved**.

2. **Remote (URL-based) MCP servers** — PR #2847: Adds `url` field to `McpServerConfig`, allowing agents to connect to MCP servers over HTTP/SSE in addition to local stdio. This is a **significant architectural expansion**.

3. **Matrix native E2EE** — PR #2844: Persistent end-to-end encryption for Matrix, replacing a WASM-based bridge with a Rust native implementation.

4. **`/learn` skill** — PR #2843: Meta-skill that distills reusable skills from directories, URLs, or conversations.

5. **Generic extension-point seams** — PR #2842: Adds `registerX()`/`applyX()` hooks for container runtime, enabling third-party extensions without modifying core code.

**Speculative Next Features:**
- Signal group message distinction (PR #2850) is a small fix but important for Signal channel reliability.
- The extensive security PR cluster (#2799, #2800, #2801, #2802, #2750) suggests a **coordinated security audit** is ongoing; expect more hardening patches.

## User Feedback Summary

**Pain Points:**

- **Telegram multi-bot removal frustration** (Issue #2852): User Kwisss reports that a previously working multi-bot feature was removed, and the "instance" replacement doesn't work with Claude. The tone suggests **risk of users leaving** the platform ("do we need to look elsewhere?"). The merged PR #2849 directly addresses this.

- **macOS + Rancher Desktop SSL failures** (PR #2854): OneCLI SDK gateway CA bundles aren't mounted correctly on macOS with Rancher Desktop, causing all agent API calls to fail with self-signed certificate errors. This affects **Apple Silicon users** specifically.

**Satisfaction Signals:**
- The rapid merge of the Telegram multi-bot fix (same day as the complaint) demonstrates **strong maintainer responsiveness**.
- Multiple contributors (grantland, sturdy4days, foxsky, robbyczgw-cla) are actively improving the codebase, suggesting a **healthy contributor ecosystem**.

## Backlog Watch

**Long-Open, Unaddressed Issues/PRs Needing Maintainer Attention:**

1. **[PR #2750 — Stale outbound.db journals after container kills](https://github.com/nanocoai/nanoclaw/pull/2750)** — Open 13 days. Fixes two critical bugs (#2516, #2640) causing message loss. This is a **high-severity data loss issue** with a complete fix already written.

2. **[PR #2802 — ncl socket hardening](https://github.com/nanocoai/nanoclaw/pull/2802)** — Open 8 days. No request timeout means connections can hang forever; no response buffer limit means memory can be exhausted.

3. **[PR #2800 — Folder traversal + image tag validation](https://github.com/nanocoai/nanoclaw/pull/2800)** — Open 8 days. CWE-22 vulnerability in `ncl groups` commands.

4. **[PR #2801 — Router safeParseContent hardening](https://github.com/nanocoai/nanoclaw/pull/2801)** — Open 8 days. Duplicated by #2815; unclear which maintainers should prioritize.

5. **[PR #2842 — Generic extension-point seams](https://github.com/nanocoai/nanoclaw/pull/2842)** — Open 2 days, but this is a **foundational architectural change** that touches multiple subsystems. Needs careful review.

**Recommendation:** The three security PRs (#2800, #2801, #2802) along with the data-loss fix (#2750) form a critical batch that should be **reviewed and merged before any new feature work**. Project health is strong, but the security backlog is growing.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for 2026-06-25.

---

## IronClaw Project Digest
**Date:** 2026-06-25

### 1. Today's Overview
The project is in a period of high-intensity stabilization following a major production incident on 2026-06-24. Activity is extremely high, with **17 open issues** and **27 open PRs** updated in the last 24 hours, indicating a focused effort on bug fixing and reliability improvements. A significant "meltdown" involving mass tool execution freezes and provider timeouts is the primary driver of current development, with multiple high-priority fixes in the review queue. The "Reborn" agent runtime, the WebUI v2 interface, and the memory subsystem are the key areas of active development.

### 2. Releases
**None.** No new releases were published today. The project appears to be in a stabilization phase between releases, prioritizing critical bug fixes over packaging.

### 3. Project Progress
While the majority of PRs are still open, several key fixes and features were merged or closed today:
- **Critical Fix (CI):** PR [#5193](https://github.com/nearai/ironclaw/pull/5193) (by BenKurrek) was *closed/merged*, fixing a duplicate workflow key and a test ignore that were breaking the main branch's CI.
- **Memory Subsystem (M2 Lift):** The major refactor PR [#5163](https://github.com/nearai/ironclaw/pull/5163) (by BenKurrek) was *closed/merged*. This lifts the memory layer into a provider-neutral contract crate (`ironclaw_memory`), a foundational step toward milestone #3537.
- **WebUI Fixes:** PR [#5199](https://github.com/nearai/ironclaw/pull/5199) (by think-in-universe) was opened to fix a critical blocker for multi-tenancy users by allowing them to access Web UI logs, a change that has already been merged.

### 4. Community Hot Topics
The most active discussions are centered on the production stability incident and newly discovered UI workflow bugs.

- **Production Meltdown Investigation:** Issue [#5173](https://github.com/nearai/ironclaw/issues/5173) (by pranavraja99) provides a detailed failure taxonomy for 2026-06-23, dominated by benchmark defects and model quality issues. This has spawned multiple fix PRs from core contributors (see Bugs & Stability).
- **WebUI Usability Issues (Dogfooding):** Issues from user `sunglow666` and developer `hanakannzashi` are generating significant activity, highlighting pain points in the new Reborn WebUI.
    - [#5190](https://github.com/nearai/ironclaw/issues/5190) - Invalid bearer tokens cause silent failure.
    - [#5189](https://github.com/nearai/ironclaw/issues/5189) - Successful tool runs don't show activity details until completion.
    - [#5196](https://github.com/nearai/ironclaw/issues/5196) - "Ask each time" tool permission leads to a duplicate approval flow and authorization error.
    - [#5192](https://github.com/nearai/ironclaw/issues/5192) - Denying a tool approval can still trigger further tool approval requests.

### 5. Bugs & Stability
The project is grappling with several high-severity stability issues, many of which have targeted fix PRs already in progress.

- **Critical (System-Wide Freeze):** The "Reborn Meltdown" on 2026-06-24, characterized by a ~4-minute total process freeze and mass `lease_expired` errors, has been traced to two key root causes.
    - *Fix:* PR [#5206](https://github.com/nearai/ironclaw/pull/5206) (by henrypark133) aims to stop WASM execution from starving the tokio worker pool.
    - *Fix:* PR [#5204](https://github.com/nearai/ironclaw/pull/5204) (by henrypark133) addresses NEAR AI provider calls without timeouts hanging below the runner lease.
- **Critical (Provider Unavailability):** A NEAR AI outage was causing every user request to hang for 30+ minutes due to 120s timeouts and retries.
    - *Fix:* PR [#5203](https://github.com/nearai/ironclaw/pull/5203) (by serrrfirat) implements fast-fail for degraded providers.
- **High (Task Init Regressions):** Issue [#5139](https://github.com/nearai/ironclaw/issues/5139) (CLOSED) reports a regression where web/research tasks hang at init, making zero LLM calls. This was fixed, likely by a PR merged today.
- **High (Prompt Safety False Positive):** Issue [#5169](https://github.com/nearai/ironclaw/issues/5169) reports that benign requests fail because bundled skills contain standard API vocabulary ("Bearer", "access token") that trigger a false-positive on the denylist.

### 6. Feature Requests & Roadmap Signals
The project's roadmap is being driven by the stabilization of the Reborn runtime and the WebUI.

- **Improved Observability:** Issue [#5182](https://github.com/nearai/ironclaw/issues/5182) requests meaningful logs and failure diagnostics from the Reborn binary in hosted deployments. This is a clear signal from the team that debugging the meltdown was too difficult, making a logging overhaul likely in the next release.
- **Context Budget Management:** PR [#5149](https://github.com/nearai/ironclaw/pull/5149) (by serrrfirat) introduces "progressive tool disclosure" (flag-gated, off by default) to cut down the massive per-call prompt (~25.8k tokens) that was contributing to provider timeouts. This is a strong candidate for the next release.
- **Memory Feature Completion:** Issue [#5201](https://github.com/nearai/ironclaw/issues/5201) outlines remaining milestones for the memory subsystem following the M2 lift (PR #5163). These include remote storage, tenant isolation, and tool extensions, pointing to a core feature area for future iterations.

### 7. User Feedback Summary
User feedback (primarily from internal dogfooding `sunglow666`) reveals significant dissatisfaction with the reliability and predictability of the Reborn agent and its WebUI.

- **Key Pain Points:**
    - **Unpredictable Agent Behavior:** Tools are not reported as unavailable when disabled; instead, the agent attempts unrelated work ([#5197](https://github.com/nearai/ironclaw/issues/5197)).
    - **Internal Messages Leaking:** "Context budget" and skill orchestration messages clutter the user-facing chat UI ([#5191](https://github.com/nearai/ironclaw/issues/5191)).
    - **Failed Approval Flow:** The "Ask each time" permission model is broken, creating duplicate prompts and authorization errors ([#5196](https://github.com/nearai/ironclaw/issues/5196)).
    - **Automation Blockers:** Recurring automations can become permanently blocked waiting for tool approval ([#4986](https://github.com/nearai/ironclaw/issues/4986)).

### 8. Backlog Watch
Several older, important issues and PRs remain open, requiring maintainer attention.

- **Long-Standing CI Failure:** Issue [#4108](https://github.com/nearai/ironclaw/issues/4108) ("Nightly E2E failed") has been open since May 27 (over 4 weeks) with no recent comments. A persistent CI failure of this type represents a significant project health risk.
- **Large Dependencies Bump:** PR [#5138](https://github.com/nearai/ironclaw/pull/5138) (by dependabot) proposes updating 45 dependencies across the project and has been open for 3 days. While risk is labeled "medium", large dependency bumps require careful review to avoid introducing new regressions, especially during this active stabilization phase.
- **Stale Big-Bang Refactor:** PR [#4002](https://github.com/nearai/ironclaw/pull/4002) (by dependabot for actions) has been open since May 24, a month ago. This suggests that infrastructure updates (GitHub Actions, tooling) may be deprioritized compared to runtime and feature fixes.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-25

**Project Repo:** [github.com/netease-youdao/LobsterAI](https://github.com/netease-youdao/LobsterAI)

---

## 1. Today's Overview

Project activity was exceptionally high, driven by the merging of a large backlog of 41 pull requests over the past 24 hours, although no new releases were cut today. The single open issue remains a long-standing bug related to scheduled task deletion behavior. The merged PRs represent a significant consolidation effort, primarily from the `fisherdaddy` team, addressing numerous bugs across the cowork, OpenClaw, and renderer areas, along with model updates and UI improvements. This suggests the project is in a heavy stabilization and polish phase after a period of active feature development. The project health appears robust with rapid triage and fixes landing in the main branch.

**Total Issues Updated:** 1 (1 open)
**Total PRs Updated:** 43 (2 open, 41 merged/closed)
**New Releases:** 0

---

## 2. Releases

No new releases were published today. Given the volume of merged fixes, a new patch release is likely imminent in the coming days.

---

## 3. Project Progress

A total of **41 pull requests** were merged or closed today, representing a major clean-up of open contributions. Key advancements include:

### Core & OpenClaw Stability
- **PR #2197** ([link](https://github.com/netease-youdao/LobsterAI/pull/2197)): Fixed duplicate assistant prefix segments in cowork when history fallback is used. Added regression test coverage.
- **PR #2196** ([link](https://github.com/netease-youdao/LobsterAI/pull/2196)): Prevented extra dock applications during shell snapshots on macOS/Linux by scoping `ELECTRON_RUN_AS_NODE`.
- **PR #2195** ([link](https://github.com/netease-youdao/LobsterAI/pull/2195)): Unified OpenClaw gateway spawn path across all platforms, fixing nested Electron child invocation issues.
- **PR #2044** ([link](https://github.com/netease-youdao/LobsterAI/pull/2044)): Prevented subagent cleanup finalize from blocking on hook failure.

### Tool Loop & Token Burning Fixes
- **PR #2049** ([link](https://github.com/netease-youdao/LobsterAI/pull/2049)): Fixed aborted tool loops that burned tokens during idle periods by adding an upstream aborted-loop breaker.
- **PR #2051** ([link](https://github.com/netease-youdao/LobsterAI/pull/2051)): Refined the tool loop breaker fix.

### Session & IM Fixes
- **PR #2047** ([link](https://github.com/netease-youdao/LobsterAI/pull/2047)): Resolved session freezing issues.
- **PR #2050** ([link](https://github.com/netease-youdao/LobsterAI/pull/2050)): Fixed gateway sessions.patch timeouts that could block chat.send.
- **PR #2063** ([link](https://github.com/netease-youdao/LobsterAI/pull/2063)): Scoped IM reply assembly to current turn and stripped thinking blocks.

### Model & UI
- **PR #2089** ([link](https://github.com/netease-youdao/LobsterAI/pull/2089)): Added MiniMax M3 model and updated BYOK model default context windows.
- **PR #2102** ([link](https://github.com/netease-youdao/LobsterAI/pull/2102)): Preserved user-configured context windows and added Mimo v2.5 models.
- **PR #2053** ([link](https://github.com/netease-youdao/LobsterAI/pull/2053)): Fixed model selection UI.
- **PR #2088** ([link](https://github.com/netease-youdao/LobsterAI/pull/2088)): Updated kits UI.

### Platform & Automation
- **PR #2057** ([link](https://github.com/netease-youdao/LobsterAI/pull/2057)): Replaced deprecated VBScript launcher with hidden PowerShell for app updates.
- **PR #2078** ([link](https://github.com/netease-youdao/LobsterAI/pull/2078)): Cowork now emits selected-skill routing metadata instead of inlining prompts.
- **PR #2086** ([link](https://github.com/netease-youdao/LobsterAI/pull/2086)): Fixed a WeChat bug during updates/reinstalls on Windows.

---

## 4. Community Hot Topics

### Most Active Issue
The single active issue, **#1394** ([link](https://github.com/netease-youdao/LobsterAI/issues/1394)), remains open for nearly 3 months. It reports that one-time scheduled tasks are permanently deleted after execution, while users expect them to be preserved for future edits and reuse. The issue has 1 comment and 0 reactions, indicating low community engagement but persistent maintenance attention is needed.

### Active Open PRs (2 total)
Two PRs remain open, but both have very low comment activity. The project's recent flood of merged PRs suggests that most community contributions are being rapidly processed.

---

## 5. Bugs & Stability

### Critical / High Severity (Fix PRs Already Merged)
- **Token Burning During Idle** — PR #2049 ([link](https://github.com/netease-youdao/LobsterAI/pull/2049)): Fixed a critical bug where aborted tool loops drained tokens continuously. This was a user-reported issue described as "continuous token burn during idle periods." ✅ Fixed today.
- **Session Freezing** — PR #2047 ([link](https://github.com/netease-youdao/LobsterAI/pull/2047)): Fixed session freezing problems. ✅ Fixed today.

### Medium Severity (Fix PRs Already Merged)
- **Gateway Restart on Copilot Token Refresh** — PR #2043 ([link](https://github.com/netease-youdao/LobsterAI/pull/2043)): Fixed a restart loop caused by GitHub Copilot token refresh. ✅ Fixed today.
- **Empty LLM Streaming Data** — PR #2048 ([link](https://github.com/netease-youdao/LobsterAI/pull/2048)): Filtered out empty data from LLM streaming output. ✅ Fixed today.
- **Duplicate Assistant Prefix** — PR #2197 ([link](https://github.com/netease-youdao/LobsterAI/pull/2197)): Fixed duplicated segments in final summaries. ✅ Fixed today.
- **WeChat Update Bug** — PR #2086 ([link](https://github.com/netease-youdao/LobsterAI/pull/2086)): Fixed a WeChat integration bug during updates/reinstalls on Windows. ✅ Fixed today.

### Low Severity / Still Open
- **Scheduled Task Auto-Deletion (#1394)** — This is a long-standing UX bug where non-repeating scheduled tasks are deleted after execution. Users expect them to be retained for future edits. No fix PR has been submitted yet.

---

## 6. Feature Requests & Roadmap Signals

### Recent Merged Features
- **MiniMax M3 & Mimo v2.5 Model Support** (PRs #2089, #2102): Indicates ongoing expansion of supported LLM providers, likely in response to user demand for more model choices.
- **Cowork Skill Routing Metadata** (PR #2078): Moving from inlined prompts to metadata routing suggests the team is building a more modular and extensible cowork skill system, potentially enabling third-party or user-defined skills.
- **PowerShell Auto-Updater** (PR #2057): Modernizing the updater infrastructure, especially important for Windows users.

### Predicted Next Features
Given the heavy stabilization focus, the next release is likely a **patch/bugfix release** (v1.x.x) rather than a major feature release. However, observed signals suggest:
- **Expanded model backends** (MiniMax, Mimo) will continue.
- **Cowork skill system** may be opened to plugin/extension in the near future.
- **Scheduled task retention** fix may appear if issue #1394 gains priority.

---

## 7. User Feedback Summary

### Pain Points (Addressed Today)
- **Token waste**: Users reported "continuous token burn during idle periods" — now fixed via tool loop breaker (PR #2049).
- **Session freezes**: Users experienced unresponsive sessions — fixed via session freeze solution (PR #2047).
- **Gateway instability**: Repeated gateway restarts caused by Copilot token refresh — fixed (PR #2043).

### Pain Points (Unresolved)
- **Scheduled task management**: Users want one-time tasks to be retained after execution for future reuse (Issue #1394). This has been open for 3 months without a fix.
- **UI/UX**: Model selection UI was buggy (PR #2053, now fixed). Kits UI updates (PR #2088) suggest ongoing polish.

### Satisfaction Indicators
- The rapid merging of 41 PRs indicates a responsive development team that values user-reported issues.
- No negative user reactions on recent PRs suggest fixes are landing well.

---

## 8. Backlog Watch

### Stale / Long-Unanswered Items
| Item | Age | Status | Risk |
|------|-----|--------|------|
| **Issue #1394** ([link](https://github.com/netease-youdao/LobsterAI/issues/1394)) — Scheduled task auto-deletion | 83 days open | No assignee, no fix PR | **High** — Long-standing UX regression left unaddressed despite ongoing development. Given today's stability focus, this should be prioritized. |

### Recommendation
Issue #1394 is the only tracked open item and has been stale for nearly 3 months. While the project has been very active in PR merges, this single bug report was not acknowledged by maintainers today. It should be triaged and either marked as planned or a fix PR should be initiated.

---

**Key Takeaway:** LobsterAI is in a strong stabilization phase with a high volume of bug fixes and infrastructure improvements being merged rapidly. However, the lone open issue (#1394) concerning unsustainable scheduled task deletion represents a notable gap in UX consistency that has persisted for months.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

# TinyClaw Project Digest — 2026-06-25

## Today's Overview
TinyClaw has seen no new issues or releases in the last 24 hours, indicating a quiet period with no active community bug reports or feature requests. One pull request (#281) was merged/closed today, representing the only development activity. The project appears stable and maintainer bandwidth is focused on cross-platform compatibility improvements. Overall, project health is good with low friction, though the lack of new releases suggests no urgent changes have been pushed to users.

## Releases
No new releases have been published as of this digest. The last release date is unknown.

## Project Progress
- **#281 (Merged/Closed)** — `fix: Windows cross-platform support in CLI` by mperkins0155. This PR resolves three Windows-specific bugs that prevented the `tinyagi` CLI from running on native Windows (non-WSL). Specifically, it fixed a doubled drive letter issue in `path.resolve` caused by `new URL('.', import.meta.url).pathname` returning paths like `/C:/Users/...` on Windows, which led to `MODULE_NOT_FOUND` errors. This is a significant stability improvement for Windows users.

## Community Hot Topics
There are no active Issues or PRs with comments or reactions today. The only closed PR (#281) had zero comments and zero reactions, indicating the fix was uncontroversial and merged without discussion.

## Bugs & Stability
No new bugs, crashes, or regressions were reported today. The sole fix merged (#281) addresses a known Windows compatibility issue that would have caused CLI startup failures on native Windows. No remaining open bug reports exist.

## Feature Requests & Roadmap Signals
No feature requests were submitted or discussed today. Based on the merged PR, the project team appears to be prioritizing cross-platform portability. No clear signals for next-version features are available.

## User Feedback Summary
No user feedback was recorded today. The lack of complaints or questions suggests users are either satisfied with the current state or there is low engagement. The Windows fix (#281) implicitly addresses a pain point for Windows users who previously could only run TinyClaw via WSL.

## Backlog Watch
No long-unanswered Issues or PRs are currently open. The backlog is empty, which is a positive sign for project health and maintainer responsiveness.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-25

Generated from GitHub activity data for [`agentscope-ai/CoPaw`](https://github.com/agentscope-ai/CoPaw)

---

## 1. Today's Overview

CoPaw (QwenPaw) saw elevated activity on **2026-06-25**, with **23 issues** updated (15 open, 8 closed) and **50 pull requests** updated (44 open, 6 merged/closed) in the last 24 hours. No new releases were published. The project remains in a high-velocity development phase following the **AgentScope 2.0 schema migration**, which has introduced a wave of regressions across streaming, tool rendering, token usage display, and channel-level identity handling. Despite this, community engagement is strong, with multiple first-time contributors submitting fixes and feature PRs. The maintainer team is actively reviewing and merging bug fixes, particularly around the Console frontend, MCP integration, and provider compatibility, indicating a focused push toward stabilizing the 2.0 codebase.

---

## 2. Releases

**No new releases** were tagged or published in the last 24 hours. The latest available versions remain:
- Stable: **v1.1.12.post2** (pip-installable)
- Beta: **v2.0.0b1** (git `a9ee2e83`)

Note: Several bugs reported against v1.1.12.post1 and .post2 have pending fix PRs (see §5).

---

## 3. Project Progress

**Today's merged/closed PRs (6 total):**

| PR | Title | Status | Notes |
|----|-------|--------|-------|
| [#5498](https://github.com/agentscope-ai/CoPaw/pull/5498) | fix: move Current date from env context to per-user-message dynamic prefix | **CLOSED** (replaced by #5499) | Addressed stale time info in long sessions |
| [#5499](https://github.com/agentscope-ai/CoPaw/pull/5499) | fix: move Current date to per-user-message dynamic prefix | **OPEN** | Improved version of #5498, open for review |

Other closed PRs were merged earlier today — notably several targeting **AgentScope 2.0 migration regressions**:
- `#5487` fixes streaming delta events broken by schema migration
- `#5493` restores the per-turn token/context usage ring in the chat UI
- `#5495` fixes tool call rendering in the frontend under 2.0 SSE envelope protocol
- `#5485` refines MCP tool name parsing for OpenAI API compatibility

**Key feature advancements (open PRs under review):**
- `#5321` — **Scroll context manager**: retrieval-driven context management with SQLite persistence, enabling models to recall past turns on demand via a Python REPL
- `#5448` — **TUI project-scoped code sessions**: `qwenpaw .` and `qwenpaw tui [PROJECT]` bind ACP sessions to Coding Mode project directories
- `#5482` — **Memory search enhancement**: simplifies metadata display while improving search functionality
- `#5492` — **pip plugin support**: allows loading plugins installed via `pip` using Python entry points (first-time contributor)

---

## 4. Community Hot Topics

### Most Active Issues (by comments & engagement)

**#5345** — [Custom OpenAI-compatible providers (e.g. OMLX) don't support function calling](https://github.com/agentscope-ai/CoPaw/issues/5345)  
*8 comments, open since 2026-06-20*  
A user reports that manually adding OMLX (a custom OpenAI-compatible provider) works for basic chat but **fails to invoke tools**, while Ollama (natively supported) works fine. This signals a gap in the custom provider API path for function/tool calling, likely affecting any third-party OpenAI-compatible service.

**#5264** — [Group chat replies sent to private chat when user has active DM session](https://github.com/agentscope-ai/CoPaw/issues/5264)  
*5 comments, closed 2026-06-24*  
A critical channel-level bug in Feishu (Lark) integration: if a user has both a group chat and DM session with the bot, group replies get misrouted to the DM. The issue was resolved, demonstrating the team's responsiveness to channel-specific regressions.

**#5379** — [Internal Server Error on startup after pip install](https://github.com/agentscope-ai/CoPaw/issues/5379)  
*5 comments, open*  
Fresh installation fails with `Internal Server Error` caused by a `get_remote_addr(transport)` error. This suggests a platform-specific (Windows) environment detection issue.

**#5455** — [Move current time to per-user-message prefix vs system context](https://github.com/agentscope-ai/CoPaw/issues/5455)  
*4 comments, open*  
An architectural discussion about timestamp placement — the proposal to move `Current date` from system context to per-message prefixes to improve prompt cache stability. Two PRs (#5498, #5499) already address this, showing rapid community-driven iteration.

### Analysis
The community is primarily focused on: (1) **post-migration stability** — regressions from the AgentScope 2.0 upgrade are the dominant theme; (2) **provider extensibility** — users want seamless support for custom OpenAI-compatible providers including function calling; (3) **performance** — memory usage and large-session rendering are recurrent pain points.

---

## 5. Bugs & Stability

### Bugs reported/updated today (2026-06-24 to 2026-06-25)

| Severity | Issue | Description | Fix Exists? |
|----------|-------|-------------|-------------|
| **Critical** | [#5479](https://github.com/agentscope-ai/CoPaw/issues/5479) | Large sessions (>500KB) crash frontend with "unexpected error" — cannot render at all | ❌ No |
| **Critical** | [#5401](https://github.com/agentscope-ai/CoPaw/issues/5401) | Console crashes on tool-use-heavy sessions — `type: "data"` blocks not handled by frontend | ❌ No |
| **High** | [#5379](https://github.com/agentscope-ai/CoPaw/issues/5379) | Internal Server Error on fresh Windows install (pip) | ❌ No |
| **High** | [#5497](https://github.com/agentscope-ai/CoPaw/issues/5497) | White screen on air-gapped (内网) Windows 10 install | ❌ No |
| **High** | [#5472](https://github.com/agentscope-ai/CoPaw/issues/5472) | GLM-5.x models via OpenCode Go fail with `json_schema_converter.cc` error | ✅ PR #5496 |
| **High** | [#5456](https://github.com/agentscope-ai/CoPaw/issues/5456) | Wrong agent identity for channel-built requests — non-default agent uses `default` id | ❌ No |
| **Medium** | [#5480](https://github.com/agentscope-ai/CoPaw/issues/5480) | Long message layout broken — CSS recalculation issue; fixed by tab switch | ❌ No |
| **Medium** | [#5501](https://github.com/agentscope-ai/CoPaw/issues/5501) | Send button misaligned in wide-screen chat window | ❌ No |
| **Medium** | [#5476](https://github.com/agentscope-ai/CoPaw/issues/5476) | Cannot switch agents on mobile UI (PC works) | ✅ Closed |
| **Low** | [#5474](https://github.com/agentscope-ai/CoPaw/issues/5474) | Invalid YAML front matter in Skill ZIP gives false success + namespace lock | ❌ No |
| **Low** | [#5441](https://github.com/agentscope-ai/CoPaw/issues/5441) | High base memory usage (1.4GB on idle) | ❌ No (duplicate of #5439) |

### Notable Fix PRs Posted Today
- **#5496** — Inlines `$ref/$defs` in tool schemas to fix GLM-5.x compatibility (fixes #5472)
- **#5495** — Aligns 2.0 SSE envelope event translation to fix broken tool call rendering (fixes part of #5401)
- **#5493** — Restores token/context usage display broken by AgentScope 2.0 migration
- **#5487** — Fixes streaming content delta events broken by schema migration
- **#5494** — Fixes cron session visibility, memory isolation, and hot-reload stability

---

## 6. Feature Requests & Roadmap Signals

### Strong Signals (likely next version)

| Feature | Issue/PR | Status |
|---------|----------|--------|
| **Pip-based plugin installation** | [#5484](https://github.com/agentscope-ai/CoPaw/issues/5484), PR [#5492](https://github.com/agentscope-ai/CoPaw/pull/5492) | **OPEN PR** — strong interest, likely to merge |
| **Per-message timestamp prefix** | [#5455](https://github.com/agentscope-ai/CoPaw/issues/5455), PR [#5499](https://github.com/agentscope-ai/CoPaw/pull/5499) | **OPEN PR** — 2 PRs already submitted |
| **OpenAI response format support** | [#5489](https://github.com/agentscope-ai/CoPaw/issues/5489) | **OPEN** — core/backend feature |
| **Kimi K2 Code (Anthropic-compatible) model support** | [#5427](https://github.com/agentscope-ai/CoPaw/issues/5427) | **OPEN** — user wants custom provider for Anthropic-style API |
| **TUI project-scoped code sessions** | PR [#5448](https://github.com/agentscope-ai/CoPaw/pull/5448) | **OPEN** — part of Coding Mode improvements |
| **Scroll context manager (durable history + recall REPL)** | PR [#5321](https://github.com/agentscope-ai/CoPaw/pull/5321) | **OPEN** — novel retrieval-driven approach |

### Weaker Signals (less activity, lower urgency)

| Feature | Issue | Notes |
|---------|-------|-------|
| MCP tool name human-readable display | [#5231](https://github.com/agentscope-ai/CoPaw/issues/5231) | UI enhancement, low comment count |
| Desktop Tauri auto-updater | PR [#4669](https://github.com/agentscope-ai/CoPaw/pull/4669) | Long-running (since May), still open |
| Memory usage optimization | [#5441](https://github.com/agentscope-ai/CoPaw/issues/5441) | User frustration, but duplicates #5439 |

### Prediction
The **next minor release** (likely 1.1.13 or 1.2.0) will almost certainly include:
1. Multiple AgentScope 2.0 migration regression fixes (streaming, tool display, token usage)
2. GLM model compatibility fix (#5496)
3. Per-message timestamp prefix (#5499)
4. Possibly pip plugin support (#5492)

The **2.0 stable** release appears to be delayed until the current regression wave is fully addressed.

---

## 7. User Feedback Summary

### Pain Points (expressed in issues & comments)

1. **Post-migration instability** — Multiple users report broken features after the AgentScope 2.0 upgrade: tool calls not rendering, streaming broken, session pages crashing, token usage display gone. This is the dominant theme across both issues and PR descriptions.

2. **Performance degradation** — Several users report high memory usage (1.4GB idle), slow frontend with large sessions (>500KB crashes), and UI jank on Windows. The "just started, already 1.4GB" complaint (#5441, #5439) was duplicated, indicating genuine user frustration.

3. **Custom provider limitations** — Users running non-Ollama OpenAI-compatible providers (OMLX, Kimi Code) encounter function calling failures. The expectation is "if it speaks OpenAI API, tools should work" — this is a significant adoption barrier for power users.

4. **Platform-specific issues** — Windows Tauri users report Python path issues (#5317). Air-gapped (内网) users get blank UI (#5497). These suggest gaps in cross-platform testing.

5. **Channel reliability** — Feishu group/DM misrouting (#5264, closed), DingTalk sessions invisible in Console (#5177, closed). While these were fixed, they erode trust in channel integration quality.

### Positive Signals

- **Active maintainer response** — Issues like #5264 and #5177 were closed, and many bugs have immediate fix PRs posted
- **Community contributions** — First-time contributors (#5321, #5492) are submitting substantial features
- **Architectural discussions** — #5455 shows users thinking about prompt caching optimization, indicating sophisticated usage

### Notable Use Case
A user integrating **Kimi K2 Code** (#5427) highlights demand for Anthropic-compatible API providers alongside OpenAI-compatible ones — suggesting the project's provider abstraction needs to support multiple API protocols.

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Priority | Reason |
|-------|-----|----------|--------|
| [#5345](https://github.com/agentscope-ai/CoPaw/issues/5345) | 5 days | **High** | Custom provider function calling broken — affects all 3rd-party OpenAI services |
| [#5379](https://github.com/agentscope-ai/CoPaw/issues/5379) | 3 days | **Critical** | Fresh installs failing on Windows — blocks new users |
| [#5497](https://github.com/agentscope-ai/CoPaw/issues/5497) | 1 day | **Critical** | White screen on air-gapped Windows install |
| [#5479](https://github.com/agentscope-ai/CoPaw/issues/5479) | 1 day | **Critical** | Large sessions (>500KB) crash — unrenderable |
| [#5401](https://github.com/agentscope-ai/CoPaw/issues/5401) | 2 days | **Critical** | Tool-heavy sessions crash Console frontend |
| [#5373](https://github.com/agentscope-ai/CoPaw/issues/5373) | 3 days | **Medium** | Shell special characters (pipes, redirection) not parsed — closed but fix may be partial |
| [#5427](https://github.com/agentscope-ai/CoPaw/issues/5427) | 2 days | **Medium** | Anthropic-compatible provider for Kimi Code — user blocked |

### Stale Issues (no update, no response)

| Issue | Created | Notes |
|-------|---------|-------|
| [#5231](https://github.com/agentscope-ai/CoPaw/issues/5231) | 2026-06-16 | MCP tool name display + file card expansion — 9 days without maintainer response |
| [#5177](https://github.com/agentscope-ai/CoPaw/issues/5177) | 2026-06-14 | DingTalk sessions invisible in Console — closed, but fix details not visible |

### PRs Needing Review

| PR | Age | Significance |
|----|-----|-------------|
| [#4669](https://github.com/agentscope-ai/CoPaw/pull/4669) | 31 days | Tauri auto-updater — long-lived, may conflict with current release strategy |
| [#5321](https://github.com/agentscope-ai/CoPaw/pull/5321) | 6 days | Scroll context manager — novel approach, needs architectural review |
| [#5213](https://github.com/agentscope-ai/CoPaw/pull/5213) | 9 days | MCP access policy layout — UI-only, low risk, should merge |

### Risk Assessment
The **highest risk items** are the three "Critical" bugs (#5379, #5497, #5479) that block new users from successfully installing or using the product. Without fixes, they will compound to erode trust and slow adoption. The **AgentScope 2.0 migration regressions** are being actively patched but the sheer volume (at least 6 separate fixes in today's PRs alone) suggests the migration was not fully regression-tested before merging to main.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-25

## Today's Overview

ZeroClaw continues as a high-velocity open-source AI agent platform with **50 updated issues** and **50 updated pull requests** in the last 24 hours. Activity remains intense across security, runtime architecture, and plugin infrastructure domains. The project has **49 open active issues** and **47 open PRs**, with only 1 issue and 3 PRs resolved today — a fairly typical ratio for a project in active feature development. Key themes dominating today's activity include multi-tenant security controls (RBAC, OIDC, per-agent scoping), WebAssembly-first plugin runtime migration, supply-chain signing, and cross-agent delegation fixes. No new releases were published in this window.

## Releases

No new releases today. The project's latest tagged version remains v0.8.x, with v0.9.0 tracked via issue #7141 (OIDC Authentication Provider support) as the target milestone.

## Project Progress

Three PRs were merged or closed today:

- **[PR #8151](https://github.com/zeroclaw-labs/zeroclaw/issues/8151) [CLOSED]** — Bug fix for deferred image attachment losing its re-loadable reference in cached history on the Matrix channel (S1 severity, workflow blocked). The root cause involved cached history failing to preserve attachment references across turns.

The merged/closed PRs and their corresponding fixes that advanced include:

- **[PR #7771](https://github.com/zeroclaw-labs/zeroclaw/pull/7771)** — Fix(observability): propagates `channel`, `agent_alias`, and `turn_id` to agent lifecycle observer events (Otel trace correlation). Addresses a gap where only `Agent::turn` wired these values; all other paths passed `None`.

- **[PR #8285](https://github.com/zeroclaw-labs/zeroclaw/pull/8285)** — Fix(delegate): intersects caller's per-agent tool gate at delegate boundary, preventing sub-agents from invoking tools the parent explicitly forbids.

- **[PR #8284](https://github.com/zeroclaw-labs/zeroclaw/pull/8284)** — Fix(runtime): gates delegate sub-tools with parent agent's `SecurityPolicy`. Duplicate fix for the same class of bug as #8285 (addresses #8279).

Note: ZeroClaw shows a pattern of multiple contributors producing near-identical fixes for the same root cause (see #8284 vs #8285, #7723 vs #7958, #8100 vs #8164, #8232 vs #8280), suggesting coordination or review bottlenecks around hot topics.

## Community Hot Topics

### Most Active Issues (by comment count)

1. **[#5982 — Per-sender RBAC for multi-tenant agent deployments](https://github.com/zeroclaw-labs/zeroclaw/issues/5982)** (9 comments, open since April 22)
   *High-risk enhancement for per-sender role-based access control. Community clearly concerned about multi-tenant isolation — this has been discussed for 2+ months without resolution.*

2. **[#7141 — OIDC Authentication Provider support](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)** (6 comments, open since June 3)
   *Tracking issue for v0.9.0 target. Umbrella for pluggable authentication-provider work. Represents a major security architecture shift.*

3. **[#6289 — Prompt-triggered install suggestions for missing skills/plugins](https://github.com/zeroclaw-labs/zeroclaw/issues/6289)** (5 comments, open since May 2)
   *User-facing quality-of-life feature — discoverability gap in ZeroClaw's growing plugin ecosystem.*

4. **[#8177 — RFC: Supply chain signing, hermetic builds, SLSA provenance](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)** (5 comments, opened June 22)
   *High-assurance infrastructure RFC. Community interest in StageX model with hardware-backed PGP keys and multi-party quorum.*

5. **[#5514 — Telegram multi-image appending bug](https://github.com/zeroclaw-labs/zeroclaw/issues/5514)** (3 comments, open since April 8)
   *Persistent Telegram channel UX issue — each image in a multi-image send triggers a separate agent request.*

### Underlying Community Needs

The most commented issues reveal three core community priorities:
- **Security & multi-tenancy** (RBAC, OIDC, supply-chain signing) — users are deploying ZeroClaw in production/shared environments and need robust isolation
- **Plugin/skill discoverability** — the ecosystem is growing faster than users can track
- **Channel-specific UX polish** — Telegram multi-image handling is a long-standing pain point (#5514, now tracked by #7873)

## Bugs & Stability

### New/Updated Critical Bugs (S1-S2 severity)

| Issue | Severity | Component | Summary | Has Fix PR? |
|-------|----------|-----------|---------|-------------|
| [#8151](https://github.com/zeroclaw-labs/zeroclaw/issues/8151) | S1 (blocked) | channel:matrix | Deferred image loses reference in cached history; bot denies seeing it | ✅ CLOSED |
| [#7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733) | S2 (degraded) | tool:mcp | `mcp_bundles` parsed but never enforced at runtime — silent security no-op | ❌ No |
| [#7623](https://github.com/zeroclaw-labs/zeroclaw/issues/7623) | S2 (degraded) | runtime | Delegate to Codex/OAuth sub-agent still fails after #7266; coordinator's API key forwarded | ❌ No (in-progress) |
| [#7737](https://github.com/zeroclaw-labs/zeroclaw/issues/7737) | S2 (degraded) | channel | Approval attribution depends on global side channel; concurrent approvals can overwrite state | ❌ No |
| [#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903) | S2 (degraded) | runtime | MCP stdio child processes accumulate on daemon (one orphan per heartbeat tick) | ❌ No |

### Notable High-Severity Regressions

**[#8044 — Harden /model --agent scope with per-sender authorization](https://github.com/zeroclaw-labs/zeroclaw/issues/8044)** — Any sender who can message the agent can change the effective model for all users. This is an active security vulnerability in the recently-added scope-selectable model override feature.

### Fix PRs in Review

- [#7485](https://github.com/zeroclaw-labs/zeroclaw/pull/7485) + [#8084](https://github.com/zeroclaw-labs/zeroclaw/pull/8084) — Duplicate fixes for doctor not passing Config context when validating custom model providers
- [#7723](https://github.com/zeroclaw-labs/zeroclaw/pull/7723) + [#7958](https://github.com/zeroclaw-labs/zeroclaw/pull/7958) — Duplicate fixes for Telegram `mention_only` gate bypass for replies to bot messages
- [#8232](https://github.com/zeroclaw-labs/zeroclaw/pull/8232) + [#8280](https://github.com/zeroclaw-labs/zeroclaw/pull/8280) — Duplicate fixes for OpenAI-compatible provider issues with reasoning replay and tool_call_id

## Feature Requests & Roadmap Signals

### Most-Requested Features

1. **Per-agent custom environment variables** ([#8226](https://github.com/zeroclaw-labs/zeroclaw/issues/8226)) — Non-secret `runtime_context` + masked `runtime_secrets` for identity/token multi-tenancy across process lanes and shared MCP instances. High risk, P2 priority.

2. **Delegate mode for specialist handoffs** ([#8238](https://github.com/zeroclaw-labs/zeroclaw/issues/8238)) — Independent delegation mode so specialist agents run under their own policy/toolset. In-progress status.

3. **OpenRouter model fallbacks** ([#8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138)) — Pass `fallback_models` array to OpenRouter's native API for automatic failover. Two competing PRs (#8141, #8207) submitted within 24 hours of each other.

4. **Local username/password AuthProvider** ([#8076](https://github.com/zeroclaw-labs/zeroclaw/issues/8076)) — IdP-less browser login for users without OIDC/SSO infrastructure. Child of #7141.

5. **Telegram webhook mode** ([#8046](https://github.com/zeroclaw-labs/zeroclaw/issues/8046)) — Alternative to getUpdates long polling for production deployments behind ingress.

### Predictions for Next Release (v0.9.0)

Based on priority labels and statuses, the following are likely candidates:
- **OIDC Authentication Provider** (#7141) — explicitly tracked as v0.9.0 target
- **Per-sender RBAC** (#5982) — P2 accepted, foundational for multi-tenant deployments
- **Supply-chain signing** (#8177, #8058, #8059) — CI/security infrastructure work showing three related issues
- **WASM-first plugin runtime** (#8135, #8172) — Multiple RFCs and PRs converging

## User Feedback Summary

### Real Pain Points Expressed

1. **Multi-tenancy isolation gaps** — Multiple issues (#7733 silent MCP isolation no-op, #7623 API key bleed in delegation, #8044 model scope bypass) suggest users are deploying ZeroClaw in environments requiring strong tenant isolation and finding it lacking.

2. **Delegation complexity** — The five separate issues/PRs around delegation tool security (two duplicate fixes today alone) indicate this is a high-friction area for users configuring sub-agent workflows.

3. **Channel UX fragmentation** — Telegram users continue to report multi-image handling issues (#5514, #7873). The tracking issue now has 1 comment, suggesting users are waiting for resolution.

4. **Plugin discovery friction** — Users want ZeroClaw to proactively suggest installable skills when they ask for capabilities (#6289), indicating the current plugin ecosystem lacks discoverability.

5. **Provider compatibility pain** — Multiple PRs for OpenRouter, NVIDIA NIM, and generic OpenAI-compatible providers (#8141, #8164, #8232, #8280) suggest users are hitting integration barriers with non-OpenAI backends.

### Use Cases Driving Development

- **Production multi-tenant deployments** (security/isolation features)
- **Specialist agent ecosystems** (delegation, tool scoping)
- **Self-hosted enterprise** (IdP-less auth, webhook ingress)
- **Plugin/extension marketplace** (discoverability, WASM distribution)

## Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Created | Age | Comments | Status |
|-------|---------|-----|----------|--------|
| [#5982](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) | 2026-04-22 | 64 days | 9 | Accepted, P2 — no PR yet |
| [#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514) | 2026-04-08 | 78 days | 3 | Accepted, P2 — no fix PR |
| [#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903) | 2026-04-19 | 67 days | 3 | Accepted, P1 — memory leak, no fix PR |
| [#5607](https://github.com/zeroclaw-labs/zeroclaw/issues/5607) | 2026-04-10 | 76 days | 2 | Blocked, accepted — cron pre-hook gates |
| [#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289) | 2026-05-02 | 54 days | 5 | Accepted, no-stale — no PR yet |
| [#6943](https://github.com/zeroclaw-labs/zeroclaw/issues/6943) | 2026-05-26 | 30 days | 3 | Accepted, type:rfc — no PR |

### PRs Needing Review

Multiple PRs have `needs-maintainer-review` labels today:

- [#8141](https://github.com/zeroclaw-labs/zeroclaw/pull/8141) — OpenRouter fallback_models (2 days old)
- [#8207](https://github.com/zeroclaw-labs/zeroclaw/pull/8207) — OpenRouter fallback_models (competing PR, 2 days old)
- [#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135) — Wasm-first plugin runtime RFC (3 days old)
- [#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) — Supply chain signing RFC (3 days old)

### Noteworthy Pattern

The duplicate PRs for the same fixes (OpenRouter fallback, Telegram mention_only, compatible provider reasoning, custom model doctor validation) suggest mainatiners may be overwhelmed, or the PR review process has a backlog that encourages contributors to re-submit rather than build on existing work.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*