# AI CLI Tools Community Digest 2026-06-29

> Generated: 2026-06-29 02:06 UTC | Tools covered: 9

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

Here is the cross-tool comparison report based on the provided community digests.

---

### Cross-Tool Comparison Report: AI CLI Developer Tools
**Date:** 2026-06-29

#### 1. Ecosystem Overview

The AI CLI tool ecosystem is maturing rapidly, but this comes with significant growing pains. The dominant theme across all major tools—Claude Code, OpenAI Codex, Gemini CLI, and others—is a critical focus on **cost governance and reliability**, driven by user reports of runaway costs, infinite loops, and session-breaking bugs. While feature velocity remains high, particularly around plugin ecosystems and multi-agent capabilities, the community sentiment is shifting from excitement about new capabilities to frustration over **unpredictable billing, agentic hallucination, and platform-specific regressions**. The landscape is bifurcating between tools optimizing for the developer desktop experience (TUI polish, session management) and those scaling up autonomous, server-side agents.

#### 2. Activity Comparison

| Tool | Open Issues (Notable) | Hot Issues (High Engagement) | Active PRs (Last 24h) | Release Status |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | ~10 | 3 (🔥 #63875, #1757, #68619) | 5 Open | None |
| **OpenAI Codex** | ~10 | 5 (🔥 #28879, #28224*, #30002) | 10 Open | None |
| **Gemini CLI** | ~10 | 4 (🔥 #21409, #22323, #25166) | 10 Open (2 help-wanted) | v0.51.0-nightly |
| **GitHub Copilot CLI** | ~5 | 1 (#2978) | 1 (Stale) | None |
| **Kimi Code CLI** | ~3 | 2 (#640, #1592) | N/A | None |
| **OpenCode** | ~10 | 5 (🔥 #13984, #21034, #32420) | 10 Open | None |
| **Pi** | ~10 | 4 (🔥 #4945, #5825, #6083) | 10 Open (1 to-discuss) | None |
| **Qwen Code** | ~10 | 5 (🔥 #5964, #5970, #5942) | 10 Open | v0.19.3 |
| **DeepSeek TUI (CodeWhale)** | ~10 | 6 (🔥 #3728, #3738, #3732) | 10 Closed/Merged | None (Stabilization Sprint) |

*   **High Engagement** indicates issues with 20+ comments or 30+ upvotes.
*   *Resolved issue.

**Key Takeaway:** OpenAI Codex is experiencing a community crisis (#28879 with 337 👍 and 194 comments). Claude Code and DeepSeek TUI are also under heavy scrutiny. Qwen Code is iterating rapidly with a patch release, while Gemini CLI is merging major dependency updates.

#### 3. Shared Feature Directions

Several requirements are appearing across multiple tool communities, indicating a collective prioritization:

- **Cost Guardrails & Transparency:** **All tools** are facing demands for better cost control. Specific asks include:
    - **Token/Dollar Limits:** Setting hard budgets on agent workflows (Claude Code #72127, #68619).
    - **Real-time Consumption Metrics:** Per-call cost breakdowns and warnings before expensive operations (Claude Code #32503, OpenAI Codex #30395/#30488, Gemini CLI #22323, Qwen Code #5964).
    - **Prompt Cache Optimization:** Users are actively debugging cache-hit rates to reduce costs (Anthropic/Claude Code #70459, Qwen Code #5942, DeepSeek TUI #3738).

- **Plugin/MCP Ecosystem Maturity:** The desire for a stable, secure, and discoverable plugin ecosystem is universal.
    - **One-Click Installation & Marketplaces:** Claude Code (#42142), OpenAI Codex (#30297 merged), and Pi (#6126) all have active discussions.
    - **Security & Permissions:** From Claude Code's `protect-mcp` policy gate (#72014) to OpenAI Codex's granular `writes` approval mode (#30482), the community is pushing for fail-closed security on tool execution.
    - **Handover & Interoperability:** The ability to export session context for use in other models or tools is a growing need (Claude Code #72037, Gemini CLI #21432).

- **Session Lifecycle Management:** Users need better control over their session history and state.
    - **Durable & Persistent Agents:** The ability to resume long-running or background tasks (Claude Code #72012, Qwen Code #5852, Gemini CLI #22232).
    - **Organization & Discoverability:** Searchable tags, visual status indicators, and archiving for large numbers of sessions (GitHub Copilot CLI #3970, #3969).
    - **Debugging Tools:** A "session dump" to see what the model actually sees (Claude Code #72035, OpenCode #34330).

#### 4. Differentiation Analysis

Three distinct strategic approaches are emerging:

| Strategic Focus | Tools | Characteristics |
| :--- | :--- | :--- |
| **Autonomous Agentic Core** | **Claude Code, OpenAI Codex, Gemini CLI** | Focus on sub-agent orchestration, complex multi-step reasoning, and sandboxed execution. Heavily focused on cost, recursion, and agent reliability bugs. Pain points include "false success" signals and runaway workflow costs. |
| **Integrated Developer Platform** | **OpenCode, Pi, Qwen Code** | Actively building broader platforms (mobile support, session forking, provider flexibility). High emphasis on UI/UX polish (TUI rendering, input methods) and supporting a diverse range of model providers (local, open-source, cloud). OpenCode is seeing a "model fragmentation" pain point. |
| **Simplicity & Enterprise Stability** | **GitHub Copilot CLI** | Relatively stable, lower issue volume. Pain points are focused on enterprise networking (proxies) and basic session organization features. Feature request velocity is slow, suggesting a more mature, utility-focused user base. **Kimi Code** similarly shows low community engagement, potentially indicating a smaller user base or a stable tool. |
| **Provider-Agnostic UI Layer** | **Pi** | Deep focus on TUI experience, provider integration, and extension system. Lacks a proprietary LLM, making it a "bring your own model" hub. This is reflected in the high number of provider-specific bugs (OpenAI Codex, Anthropic, Groq, etc.). |

#### 5. Community Momentum & Maturity

| Tool | Momentum & Maturity Analysis |
| :--- | :--- |
| **OpenAI Codex** | **Highest community velocity, but in crisis.** The 337-upvote rate-limit issue (#28879) signifies a major trust event. The rapid resolution of the SQLite write amplification bug (#28224) shows development agility, but the community is burning out on cost issues. |
| **Claude Code** | **High engagement, high scrutiny.** The community is deeply technical, filing detailed bugs with code analysis. Slow resolution on critical bugs (e.g., constant re-login #1757) is creating a backlog of friction. The "open source" PR (#41447) remains a point of contention. |
| **DeepSeek TUI** | **Rapid iteration, aggressive stabilization.** The maintainer (@Hmbown) is extremely responsive, closing issues within hours. The rebrand to "CodeWhale" is causing migration friction, but the transparency about mode integrity failures is a sign of a healthy, honest development cycle. |
| **Gemini CLI** | **Moderate momentum, structural issues.** The focus on dependency bumps suggests a major internal rewrite. Community is vocal about agent reliability (hanging, false success), but the number of "help wanted" PRs suggests the team may be resource-constrained. |
| **GitHub Copilot CLI / Kimi Code ** | **Low velocity, mature or niche.** These tools have the quietest communities. Copilot CLI's issue list is clean but feature requests are basic, suggesting a stable product for a simple use case. Kimi Code's digest is extremely thin, suggesting a very small or inactive community. |

#### 6. Trend Signals

The community feedback this week reveals several industry trends with significant reference value for developers:

1.  **The "Cost Crisis" of Autonomous Agents:** The most critical signal. Sub-agent recursion and automated workflows are burning through budgets without guardrails. **For developers:** Any product offering agent spawning or automated tools *must* include cost limits, real-time consumption accounting, and user authorization prompts for expensive operations as a first-class feature, not an afterthought.

2.  **The "LLM Sandwich" Challenge:** Agents are caught between the imprecision of the LLM (tool-call parsing failures, hallucinated commands) and the strictness of the OS (sandbox escapes, permissions errors). **For developers:** Investing in robust error handling, retry logic, and graceful fallbacks for tool execution is more important than adding new tools.

3.  **Security & Prompt Injection is the New Normal:** Reports of Plan mode bypasses (OpenCode #34190), skill injections (Claude Code #72166), and silent approval of destructive actions (DeepSeek TUI #3735) are common. **For developers:** All tools must assume the LLM can be manipulated. Implementing a "defense in depth" with policy gates (e.g., Cedar, OPA) and signed receipts for critical actions is no longer optional.

4.  **Rendering is a Reliability Pillar:** TUI flicker, terminal corruption, and broken modals (Pi, Qwen Code, DeepSeek TUI) are not just cosmetic issues; they cause data loss (hidden output) and make tools unusable for real work. **For developers:** Terminal rendering quality is a non-negotiable aspect of reliability. Virtualized terminals and robust async rendering are critical.

5.  **Provider Lock-In is the New Vendor Lock-In:** Users are actively debugging prompt cache hits to choose the cheapest model (Anthropic vs. DeepSeek). **For developers:** Building a provider-agnostic tool that can optimize for cost, latency, and quality across multiple backends is a major competitive advantage (e.g., Pi, OpenCode).

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** github.com/anthropics/skills | 2026-06-29

---

## 1. Top Skills Ranking

The following Pull Requests have attracted the most community discussion and development activity:

### #1298 — `fix(skill-creator): run_eval.py always reports 0% recall`
**Status:** Open | **Author:** MartinCajiao | **Created:** 2026-06-10
**Functionality:** Fixes the `run_eval.py` script — the core evaluation engine for the description-optimization loop — which has been silently returning `recall=0%` for every skill description due to artifact installation failures, Windows stream reading bugs, and flawed trigger detection. This fix addresses 10+ independent reproductions of Issue #556.
**Discussion highlights:** The highest-comment PR in the repository. Community members repeatedly confirmed the same failure mode, and the fix consolidates multiple prior partial attempts (PRs #1099, #1050, #1323) into a single comprehensive resolution.
**Link:** https://github.com/anthropics/skills/pull/1298

### #514 — `Add document-typography skill`
**Status:** Open | **Author:** PGTBoos | **Created:** 2026-03-04
**Functionality:** Prevents orphan word wrap (1–6 words spilling to next line), widow paragraphs (headers stranded at page bottom), and numbering misalignment in AI-generated documents. Addresses a universal pain point across all Claude document output.
**Discussion highlights:** Broad agreement that typographic issues affect every document Claude generates; skill addresses a gap users rarely request but consistently notice.
**Link:** https://github.com/anthropics/skills/pull/514

### #538 — `fix(pdf): correct case-sensitive file references in SKILL.md`
**Status:** Open | **Author:** Lubrsy706 | **Created:** 2026-03-06
**Functionality:** Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where `REFERENCE.md` and `FORMS.md` were referenced in uppercase but the actual files are lowercase. Breaks on case-sensitive filesystems (Linux).
**Discussion highlights:** A critical but simple fix for Linux/macOS users; discussion focused on CI/CD gaps that allowed this to reach production.
**Link:** https://github.com/anthropics/skills/pull/538

### #486 — `Add ODT skill — OpenDocument text creation and template filling`
**Status:** Open | **Author:** GitHubNewbie0 | **Created:** 2026-03-01
**Functionality:** Enables creation, reading, conversion, and template-filling for OpenDocument Format files (.odt, .ods). Targets LibreOffice and ISO-standard document workflows.
**Discussion highlights:** Strong demand from enterprise users running LibreOffice environments; discussions focused on template rendering accuracy and ODF schema coverage.
**Link:** https://github.com/anthropics/skills/pull/486

### #210 — `Improve frontend-design skill clarity and actionability`
**Status:** Open | **Author:** justinwetch | **Created:** 2026-01-05
**Functionality:** Refactors the frontend-design skill so every instruction is executable within a single conversation, with guidance specific enough to steer behavior without being overly prescriptive.
**Discussion highlights:** The community spent significant time debating token efficiency vs. specificity; this PR became the reference standard for skill clarity.
**Link:** https://github.com/anthropics/skills/pull/210

### #83 — `Add skill-quality-analyzer and skill-security-analyzer`
**Status:** Open | **Author:** eovidiu | **Created:** 2025-11-06
**Functionality:** Two meta-skills: one evaluates skill quality across structure, documentation, and resource completeness; the other audits skill security by analyzing execution boundaries, permissions, and data handling.
**Discussion highlights:** The first "meta-skill" proposals generated significant interest about self-improving skill ecosystems. Security analysis skill gained renewed relevance after Issue #492.
**Link:** https://github.com/anthropics/skills/pull/83

---

## 2. Community Demand Trends

From Issues (the repository's "wishlist" channel), the community's most-anticipated Skill directions are:

| Demand Area | Key Issue | Signal |
|---|---|---|
| **Trust & Security** | #492 — "Security: Community skills under anthropic/ namespace enable trust boundary abuse" | 29 comments, 2 👍 |
| **Organization/Enterprise** | #228 — "Enable org-wide skill sharing in Claude.ai" | 14 comments, 7 👍 |
| **Reliable Skill Evaluation** | #556 — "run_eval.py: 0% trigger rate across all queries" | 12 comments, 7 👍 |
| **Agent Governance** | #412 — "skill proposal: agent-governance — safety patterns for AI agent systems" | 6 comments |
| **Deduplication & Management** | #189 — "document-skills and example-skills install identical content" | 6 comments, 9 👍 |
| **Windows Compatibility** | #1061 — "Windows compat: skill-creator scripts fail" | 3 comments |
| **MCP Integration** | #16 — "Expose Skills as MCPs" | 4 comments |

**Key takeaway:** The community is shifting from "what can Skills do?" to "how do we trust, manage, and scale Skills?" — security, enterprise sharing, evaluation reliability, and dependency management dominate current discussions.

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and appear close to landing:

| PR | Skill | Highlight | Status |
|---|---|---|---|
| #181 | SAP-RPT-1-OSS predictor skill | Tabular foundation model for SAP business data — enterprise analytics | Open since Dec 2025, steady updates |
| #360 | AppDeploy skill | Full-stack webapp deployment directly from Claude | Open; lifecycle management included |
| #723 | Testing-patterns skill | Comprehensive testing stack (unit, React, E2E, philosophy) | Open; high community interest |
| #147 | Codebase-inventory-audit skill | Orphaned code + docs gap detection workflow | Open since Dec 2025 |
| #154 | Shodh-memory skill | Persistent cross-conversation memory for agents | Open; novel state management approach |
| #1323 | `run_eval` trigger detection fix | Fixes core evaluation loop for skill optimization | Recent (June 2026); complementary to #1298 |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for skill reliability infrastructure — tooling to validate, evaluate, and trust skills — rather than novel skill functionality, with the `run_eval.py` zero-percent-recall bug (#556 / #1298) marking the single largest coordination point in the repository's history.**

---

**Claude Code Community Digest**
**2026-06-29**

**1. Today's Highlights**

No new releases were shipped in the last 24 hours, but the community surfaced a cluster of critical cost and reliability bugs. The most urgent threads involve runaway subagent recursion burning through token limits (#68619), auto-compaction misconfigurations causing repeated cache writes instead of reads (#70459), and a "Workflow" tool that silently consumed an entire 5x plan in five minutes (#72127). Several false-positive safety blocks and a session-breaking skill injection round out a heavy day for open bug reports.

**2. Releases**

No new versions were published in the last 24 hours.

**3. Hot Issues**

1. **#68619 — Subagent spawning infinite recursion & catastrophic token burn** (26 comments, 👍8)
   *Agents/Agents, Cost, Permissions*. Subagents recursively spawn child agents 50+ levels deep, ignoring `CLAUDE_CODE_FORK_SUBAGENT=0`. Permission denials trigger further agent spawning instead of stopping. Community reports this as a "catastrophic token burn scenario."
   [View Issue](https://github.com/anthropics/claude-code/issues/68619)

2. **#1757 — Constant re-login required** (73 comments, 👍63)
   *Auth/Core*. Users must re-authenticate via the web nearly every day. The community considers this excessive for a tool intended for daily development sessions. The most commented and second-most upvoted open issue.
   [View Issue](https://github.com/anthropics/claude-code/issues/1757)

3. **#63875 — Recurring "model's tool call could not be parsed" error** (72 comments, 👍110)
   *Model/Windows*. During normal sessions, Claude Code intermittently halts with a parse failure on tool calls, and retries also fail. The top-voted open issue, affecting session stability across Windows users. 
   [View Issue](https://github.com/anthropics/claude-code/issues/63875)

4. **#70459 — Auto-compaction: stale precompute & repeated cache creation** (4 comments, 👍3)
   *Cost/Core*. Two compounding cost bugs: stale precompute summaries bloat sessions by ~200k tokens, and the compacted prefix is repeatedly cache-created instead of cache-read. Directly impacts daily spend for heavy users.
   [View Issue](https://github.com/anthropics/claude-code/issues/70459)

5. **#72127 — Workflow tool burned entire 5x plan in ~5 minutes with no warning** (3 comments)
   *Cost/Agents*. A simple research task triggered 8–10 parallel research agents without authorization, consuming the user's entire plan budget. Highlights a lack of cost guardrails on automated workflows.
   [View Issue](https://github.com/anthropics/claude-code/issues/72127)

6. **#72166 — claude-api skill injects ~184k tokens into session, breaking it** (2 comments)
   *Skills*. The bundled `claude-api` skill emits its full 735 KB reference as a single user message. The session becomes unrecoverable; `/compact` cannot run.
   [View Issue](https://github.com/anthropics/claude-code/issues/72166)

7. **#32503 — /usage command fails with rate_limit_error** (9 comments, 👍13)
   *Cost/API, Windows*. Running `/usage` to check limits returns "Rate limited. Please try again later." The one command users need for cost awareness is blocked by rate limiting.
   [View Issue](https://github.com/anthropics/claude-code/issues/32503)

8. **#64301 — Bash sandbox corrupts `!` to `\!` in commands** (2 comments, 👍3)
   *Bash/Sandbox, Linux*. Bubblewrap sandbox escapes `!` characters, but since commands run via `bash -c` (non-interactive, history expansion off), the backslash is never removed—making the sandbox unusable for agentic workflows.
   [View Issue](https://github.com/anthropics/claude-code/issues/64301)

9. **#42142 — Desktop app lacks /plugin command and plugin marketplaces** (9 comments, 👍8)
   *Desktop/Plugins*. Users on the desktop app cannot install or manage plugins; the app does not expose `/plugin` or any marketplace. Claude hallucinates commands that don't exist.
   [View Issue](https://github.com/anthropics/claude-code/issues/42142)

10. **#72012 — Agent View: reopening completed background sessions loses conversation** (3 comments)
    *Agent View, macOS*. When a completed background session is reopened from Agent View, a new session-id is spawned with no prior conversation. Reduces the utility of persistent background agents.
    [View Issue](https://github.com/anthropics/claude-code/issues/72012)

**4. Key PR Progress**

1. **#72037 — Add handover plugin (export session context for LLM handoffs)** (Open)
   Exports the current session context to a structured markdown file for pasting into a different LLM or sharing with a teammate. Useful for debugging and cross-model collaboration.
   [View PR](https://github.com/anthropics/claude-code/pull/72037)

2. **#72014 — Add protect-mcp plugin (fail-closed Cedar policy gate + signed receipts)** (Open)
   Blocks MCP tool calls before execution based on Cedar policies, with signed offline-verifiable receipts. Extends the security model beyond the existing `security-guidance` plugin.
   [View PR](https://github.com/anthropics/claude-code/pull/72014)

3. **#72000 — docs: update plugin install instructions to recommended installers** (Open)
   Documentation-only PR updating plugin installation instructions to use current recommended installers.
   [View PR](https://github.com/anthropics/claude-code/pull/72000)

4. **#62315 — Fix hookify event filtering in pre/post hooks** (Closed)
   Fixes incorrect event filtering that could cause hooks to fire on unintended events. Merged.
   [View PR](https://github.com/anthropics/claude-code/pull/62315)

5. **#41447 — feat: open source claude code** (Open, long-running)
   Meta PR to open-source the entire repository. Closes numerous linked issues. Remains open with no recent activity.
   [View PR](https://github.com/anthropics/claude-code/pull/41447)

**5. Feature Request Trends**

- **Plugin ecosystem maturity**: Multiple requests for better plugin support, including one-click installation, plugin marketplaces, and desktop app integration (#42142, #72121).
- **Cost transparency and controls**: Users want granular cost guardrails, warnings before expensive operations, and the ability to set token or dollar limits on agent workflows (#72127, #68619, #32503).
- **Session debugging tools**: Requests for a command to dump the full chronological context window (#72035) and for handover/export formats (#72037) indicate growing demand for observability into what the model actually sees.
- **Mouse control granularity**: Users want to disable click-to-select while preserving mouse-wheel scroll (#70672, 18 upvotes), reflecting TUI polish demands.
- **Retain finished chats as reusable skills**: One-click save of completed sessions as agents or skills (#72121).

**6. Developer Pain Points**

- **Runaway costs**: The #1 frustration this week. Subagent recursion (#68619) and silent workflow spawning (#72127) can burn through usage plans in minutes with no authorization prompt or warning. The `/usage` command itself is broken by rate limiting (#32503).
- **Constant re-authentication**: Daily forced web login (#1757) disrupts CI/CD pipelines and long-running sessions.
- **Session-breaking bugs**: The `claude-api` skill injecting 184k tokens (#72166) and auto-compaction misconfigurations (#70459) can render sessions unrecoverable.
- **Platform-specific regressions**: Windows users face tool call parse failures (#63875) and mouse wheel scroll issues (#59979, closed). Linux users deal with sandbox corruption (#64301). macOS users lose background session history (#72012).
- **False positive safety blocks**: Cybersecurity analysis work (APK unpacking, local telnet access) is halted mid-session by server-side filters (#72163, #72172, #72168), blocking legitimate developer workflows.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-29

## Today's Highlights

The Codex community is experiencing a major rate-limit crisis, with multiple high-engagement issues reporting **10–20x cost inflation per token** starting June 16, draining Plus and Pro budgets in as few as 2–3 prompts. Meanwhile, a long-running SQLite feedback log write amplification bug has been resolved via three merged PRs, cutting 85% of excessive disk writes. On the development front, OpenAI is shipping UX refinements for safety buffering, slash-command dismissal, multi-agent mode hints, and reasoning effort fallback logic.

---

## Releases

No new versions were published in the last 24 hours.

---

## Hot Issues

### 1. [#28879 — Rate-limit cost per token jumped ~10-20x since June 16](https://github.com/openai/codex/issues/28879)
**194 comments | 337 👍** — *bug, rate-limits, app*  
The top community concern. Users on GPT-5.5 Plus report budget draining in 2–3 prompts instead of the expected 20+. Session logs confirm a **10–20× increase in limit consumption per token**. This is causing operational havoc for paying subscribers.

### 2. [#28224 — SQLite feedback logs write ~640 TB/year](https://github.com/openai/codex/issues/28224)
**99 comments | 404 👍** — *bug, CLI, performance*  
**Now resolved** — three PRs (#29432, #29457, and a third) merged in 0.142.0 reduce logs by 85%. The massive write amplification was consuming SSD endurance rapidly. Community relief is palpable.

### 3. [#30002 — Pro 5h limit burned in ~41 min after reset](https://github.com/openai/codex/issues/30002)
**28 comments | 6 👍** — *bug, rate-limits, app*  
Related to #28879 but with a twist: server-side quota accounting over-reports consumption post-reset. A Pro account hit `usage_limit_reached` after only ~1.35M tokens, when the same account normally consumes ~156M tokens in a full window.

### 4. [#25719 — macOS `syspolicyd` / `trustd` CPU runaway](https://github.com/openai/codex/issues/25719)
**35 comments | 55 👍** — *bug, app, computer-use, performance*  
Codex Desktop on macOS triggers persistent CPU/memory runaway in system security daemons. Still open after nearly a month, affecting Plus users on Apple Silicon.

### 5. [#17320 — Excessive SQLite WAL writes from TRACE logs](https://github.com/openai/codex/issues/17320)
**16 comments | 36 👍** — *bug, agent*  
Related to #28224 but platform-specific: TRACE logging ignores `RUST_LOG` settings, flooding the WAL during streaming on Linux. Community has been waiting for a fix.

### 6. [#30224 — X-OpenAI-Internal-Codex-Responses-Lite unsupported model](https://github.com/openai/codex/issues/30224)
**53 comments | 19 👍** — *bug, custom-model, app, config*  
API returns "This model is not supported" when using an internal header. Affects GPT-5.5 on Windows. Users are blocked from using the Responses-Lite optimization path.

### 7. [#20214 — Windows 11 freezes/stutters despite sufficient resources](https://github.com/openai/codex/issues/20214)
**20 comments | 38 👍** — *bug, windows-os, app, performance*  
Codex App on Windows 11 Pro frequently freezes even on high-end hardware (Ryzen 5 5600, 32 GB RAM). Ongoing since April, no fix yet.

### 8. [#30405 — Windows still logs TRACE to SQLite WAL post-fix](https://github.com/openai/codex/issues/30405)
**6 comments | 0 👍** — *bug, windows-os, app, performance*  
New report showing the #28224 fix may not have fully landed on Windows. Version 26.623.5546.0 still exhibits high-frequency TRACE log persistence.

### 9. [#30357 — "ping" consumes 13% of 5h limit](https://github.com/openai/codex/issues/30357)
**5 comments | 0 👍** — *bug, rate-limits, app*  
Another rate-limit anomaly: a simple "ping" on GPT-5.5 low consumes 13% of the 5-hour budget. Suggests a systemic accounting issue.

### 10. [#30400 — Sub-agents stuck indefinitely](https://github.com/openai/codex/issues/30400)
**3 comments | 0 👍** — *bug, app, subagent*  
Sub-agents (and sub-sub-agents) occasionally hang during extended reviews. No workaround reported; impacts multi-agent workflows.

---

## Key PR Progress

### 1. [#30500 — Allow review while MCP servers are starting](https://github.com/openai/codex/pull/30500)
**Open** — Unblocks `/review` by separating foreground work from background MCP initialization. Eliminates a major UX pain point for users with many MCP servers.

### 2. [#29740 — Use model metadata for skills usage instructions](https://github.com/openai/codex/pull/29740)
**Closed** — Adds `include_skills_usage_instructions` metadata field, enabled for GPT-5.5. Removes hardcoded legacy model matching, making skill rendering data-driven.

### 3. [#30492 — Fix slash command popup dismissal](https://github.com/openai/codex/pull/30492)
**Open** — Fixes Escape key behavior: after dismissing a slash-command popup, the same command text no longer reopens it. A subtle but important UX improvement.

### 4. [#30482 — Add writes app approval mode](https://github.com/openai/codex/pull/30482)
**Open** — Introduces a `writes` approval mode where read-only tools skip prompts but all other tools (including non-destructive writes) require approval. Granular security control for app tool access.

### 5. [#30493 — Configurable multi-agent mode hint text](https://github.com/openai/codex/pull/30493)
**Open** — Allows deployments to set a stable multi-agent hint policy regardless of reasoning effort selection. Avoids model-catalog plumbing for custom deployment needs.

### 6. [#30491 — Update safety check links](https://github.com/openai/codex/pull/30491)
**Open** — Refreshes bio/cyber safety surface URLs in TUI, adds "Learn more" action, updates block copy. Follow-up to #30317.

### 7. [#30487 — Fall back from unsupported reasoning effort](https://github.com/openai/codex/pull/30487)
**Open** — Fixes a deadlock where cross-thread messages could set a reasoning effort (`max`) unsupported by the target model. Worker now gracefully falls back instead of failing.

### 8. [#30488 — Show reset details in redemption picker](https://github.com/openai/codex/pull/30488)
**Open** — Loads and displays individual reset credit details (expiry, which credit will be consumed) in the rate-limit redemption UI. Improves transparency.

### 9. [#30395 — Expose rate-limit reset credit details](https://github.com/openai/codex/pull/30395)
**Open** — Backend companion to #30488. Adds v2 API endpoint exposing available credits and expiry times, enabling the new redemption picker.

### 10. [#30467 — Treat max as a first-class reasoning effort](https://github.com/openai/codex/pull/30467)
**Open** — Promotes `max` from opaque custom effort to a first-class reasoning level, fixing UI rendering and ensuring consistent labeling across catalog, parsing, and UI.

---

## Feature Request Trends

1. **Scheduled / Durable Tasks** — Issue #22310 proposes cron-like scheduled prompt tools for Codex agents, inspired by Claude Code. Community interest is steady (1 comment, 0 👍 but from a contributor with a working prototype).

2. **Non-blocking MCP & Subagent Orchestration** — Issue #30399 requests observable, non-blocking startup and multi-machine workflow support. Users want to run MCP servers and sub-agents across machines without blocking the main composer.

3. **Remote Plugin Default Enablement** — PR #30297 (closed, merged) enables remote plugins by default. This signals OpenAI's strategic push toward plugin extensibility, which the community has been requesting for months.

4. **Rate-Limit Transparency** — Multiple issues (#30002, #30357, #28879) are effectively feature requests for real-time rate-limit accounting, per-credit expiry visibility, and consumption breakdowns. PRs #30395 and #30488 directly address this.

5. **Approval Mode Granularity** — PR #30482's "writes" approval mode reflects a broader community desire for per-tool security policies, especially in enterprise or sensitive environments.

---

## Developer Pain Points

### Rate-Limit Accounting Chaos
The #1 pain point: **unexplained 10-20x cost inflation** starting June 16, combined with post-reset over-reporting (#30002) and basic "ping" messages consuming 13% of budget (#30357). This is a **production blocker** for daily users and is generating the highest community heat (337 👍 on #28879 alone).

### Windows-Specific Regressions
- Freezes and stutters despite adequate hardware (#20214)
- Sandbox runner fails with `CreateProcessAsUserW` error (#30219)
- PowerShell parsing `@{u}` as a hashtable literal breaks git operations (#30473)
- Elevated/admin Codex breaks normal file UI interactions (#30501)
- Unicode keyboard input duplication in TUI (#30480, PR fix available)

### macOS Performance and Security
- `syspolicyd`/`trustd` CPU runaway (#25719) remains unresolved after 4 weeks
- Binary links non-public `liblzma`/`libbz2`, causing App Store rejection (#28402)

### SQLite / Disk Write Amplification (Legacy)
- **Partially resolved** — The #28224 fix reduced logs by 85%, but Windows users report it hasn't fully landed (#30405)
- TRACE logs still ignoring `RUST_LOG` (#17320) affects Linux users

### Multi-Agent Reliability
- Sub-agents occasionally hang indefinitely (#30400)
- Agent-visible runtime identity incorrectly reports "GPT-5" even when using GPT-5.5 (#26798), causing confusion in agent instructions

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-29

## Today's Highlights

The latest nightly release (v0.51.0) is out, though primarily a version bump. The community's attention is focused on persistent agent reliability issues, particularly a critical bug where subagents falsely report success after hitting MAX_TURNS. A massive dependency refresh landed today across 75+ packages, including major version jumps for the GenAI SDK (1.30→2.9) and chrome-devtools-mcp (0.19→1.3), signaling significant upstream changes.

## Releases

- **[v0.51.0-nightly.20260629.gae0a3aa7b](https://github.com/google-gemini/gemini-cli/releases/tag/v0.51.0-nightly.20260629.gae0a3aa7b)** — Automated nightly release. No manual changes reported. [Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.51.0-nightly.20260628.gae0a3aa7b...v0.51.0-nightly.20260629.gae0a3aa7b)

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 8 comments, 2 👍)  
   A `codebase_investigator` subagent reports `"success"` even when it hits MAX_TURNS before performing any analysis. This is a subtle logic failure that misleads users into thinking work was completed. The `kind/bug` and `status/need-retesting` labels suggest maintainers are actively debugging.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 7 comments, 8 👍)  
   High community consensus: the generalist agent hangs indefinitely for simple tasks (e.g., folder creation). Workaround exists (disable subagent delegation), but this is a core UX blocker that has been open since March.

3. **[#19873 — Zero-Dependency OS Sandboxing & Post-Execution Intent Routing](https://github.com/google-gemini/gemini-cli/issues/19873)** (P2, 8 comments, 1 👍)  
   An ambitious proposal to leverage Gemini 3's native bash capabilities via sandboxed shell execution, avoiding MCP overhead. Labelled `effort/large` and still actively discussed after 4 months.

4. **[#25166 — Shell command gets stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 4 comments, 3 👍)  
   Commands that produce no interactive output leave the shell in a stuck state. Users report this as frequent and disruptive, especially for simple CLI tools.

5. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, 4 comments, 1 👍)  
   The browser agent crashes on Wayland compositors with a misleading "GOAL" termination. Blocks Linux users who rely on Wayland (most modern distros).

6. **[#21968 — Gemini does not use skills/sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, 6 comments)  
   Even when custom skills for `gradle` or `git` are defined with clear descriptions, the model rarely invokes them autonomously. A fundamental agent orchestration issue.

7. **[#22672 — Agent should stop destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, 3 comments, 1 👍)  
   The model occasionally uses `git reset --force` or destructive DB operations when safer alternatives exist. Community is asking for safety-conscious tool routing.

8. **[#26525 — Add deterministic redaction for Auto Memory](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, 5 comments)  
   Auto Memory exposes sensitive content to the model before redaction occurs, violating security-by-design. Logging of skill transcripts compounds the risk. Active `area/security` tracking.

9. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, 5 comments)  
   Sessions deemed "low-signal" by the extraction agent remain unprocessed in the index, causing infinite re-inspection cycles. Resource waste and potential infinite loops.

10. **[#22186 — get-shit-done output hook causes crash](https://github.com/google-gemini/gemini-cli/issues/22186)** (P1, 3 comments)  
    The GSD output hook crashes Gemini near completion, disrupting long-running tasks. The crash trace suggests a formatting/rendering issue on final summary output.

## Key PR Progress

1. **[#28190 — Bump npm-dependencies group with 75 updates](https://github.com/google-gemini/gemini-cli/pull/28190)** (Merged)  
   Massive maintenance PR updating 75 packages including `simple-git`, `@agentclientprotocol/sdk`, and linter tooling. Closes numerous security and compatibility gaps.

2. **[#28191 — Bump @google/genai from 1.30.0 to 2.9.0](https://github.com/google-gemini/gemini-cli/pull/28191)** (Merged)  
   Major version jump for the core GenAI SDK. Likely includes breaking API changes or new model capabilities that will cascade into other issues.

3. **[#28195 — Bump chrome-devtools-mcp from 0.19.0 to 1.3.0](https://github.com/google-gemini/gemini-cli/pull/28195)** (Merged)  
   Chrome DevTools MCP goes GA (1.0+). May resolve several browser agent stability issues, though direct links to Wayland fixes (#21983) are unclear.

4. **[#27862 — Fix: preserve executing subagent tool calls in UI](https://github.com/google-gemini/gemini-cli/pull/27862)** (Open, help wanted)  
   Addresses [#22589](https://github.com/google-gemini/gemini-cli/issues/22589): subagent tool calls disappear from the UI during execution, confusing users about what's happening.

5. **[#27863 — Fix: prioritize structured display titles in tool invocation](https://github.com/google-gemini/gemini-cli/pull/27863)** (Open, help wanted)  
   Fixes [#23018](https://github.com/google-gemini/gemini-cli/issues/23018) — improves how tool invocations are rendered in non-interactive mode.

6. **[#27860 — Fix: reset slash-command conflict dedupe](https://github.com/google-gemini/gemini-cli/pull/27860)** (Open, help wanted)  
   Fixes [#24333](https://github.com/google-gemini/gemini-cli/issues/24333): slash-command conflict notifications are deduplicated incorrectly, suppressing re-notifications after resolution.

7. **[#27754 — Fix: add missing return after 501 in A2A server](https://github.com/google-gemini/gemini-cli/pull/27754)** (Open, help wanted)  
   Fixes [#21729](https://github.com/google-gemini/gemini-cli/issues/21729): A2A server crashes with `ERR_HTTP_HEADERS_SENT` on unsupported endpoints due to missing `return`.

8. **[#27755 — Test: migrate process.env to vi.stubEnv()](https://github.com/google-gemini/gemini-cli/pull/27755)** (Open, help wanted)  
   Housekeeping for test hygiene in the A2A server, which previously mutated global state directly.

9. **[#22279 — Rename ToDo to Tasks in list tray](https://github.com/google-gemini/gemini-cli/pull/22279)** (Open)  
   Simple but overdue UI consistency fix — standardizes terminology with the rest of the product.

10. **[#22279 (also listed) — chore: version bump for nightly](https://github.com/google-gemini/gemini-cli/pull/28198)** (Open)  
    Automated nightly release pipeline — no functional changes.

## Feature Request Trends

1. **Zero-Dependency OS Sandboxing** ([#19873](https://github.com/google-gemini/gemini-cli/issues/19873)) — The highest-effort proposal to run the model via native bash tooling with intent routing, bypassing MCP. This suggests community frustration with the overhead of the current tooling abstraction.

2. **AST-Aware Code Intelligence** ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) — Multiple issues explore AST-aware file reads, method-bound navigation, and codebase mapping. The team is investigating `tilth` or `glyph` as potential implementations.

3. **Agent Self-Awareness & Debuggability** ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432), [#22598](https://github.com/google-gemini/gemini-cli/issues/22598)) — Users want the agent to understand its own flags, hotkeys, and configuration. Subagent trajectories should be shareable via `/chat share` for debugging and evaluation.

4. **Component-Level Evaluations** ([#24353](https://github.com/google-gemini/gemini-cli/issues/24353)) — An EPIC to formalize 76 behavioral eval tests across 6 Gemini model variants, indicating the team is investing in systematic quality measurement.

5. **Better Session/Turn Handling** ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232), [#22267](https://github.com/google-gemini/gemini-cli/issues/22267)) — Requests for automatic session takeover, lock recovery, and respecting `settings.json` overrides for browser agent parameters like `maxTurns`.

## Developer Pain Points

1. **False "Success" Signals** — The most dangerous pattern: subagents report `status: "success"` with `Termination Reason: "GOAL"` even when they hit MAX_TURNS or crash ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)). This undermines trust in all agent output.

2. **Stuck/Hanging Executions** — Multiple reports of commands hanging indefinitely: shell commands stuck at "Awaiting input" ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), the generalist agent hanging forever ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), and the GSD output hook crashing near completion ([#22186](https://github.com/google-gemini/gemini-cli/issues/22186)). These are P1 and attract high community engagement.

3. **Agent Orchestration Fragility** — Subagents don't autonomously use custom skills ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)), run without permission after updates ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)), and the browser agent ignores `settings.json` overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)). The orchestration layer feels immature.

4. **Security & Compliance Gaps** — Auto Memory exposes secrets before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), retries low-signal sessions indefinitely ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)), and the model performs destructive git/DB operations without safeguards ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)). These are P2 but carry high risk.

5. **Terminal UI Issues** — Corruption after exiting external editors ([#24935](https://github.com/google-gemini/gemini-cli/issues/24935)), flicker on terminal resize ([#21924](https://github.com/google-gemini/gemini-cli/issues/21924)), and incorrect `\n` escape handling ([#22466](https://github.com/google-gemini/gemini-cli/issues/22466)). These degrade the developer experience for terminal-heavy workflows.

6. **Tool Proliferation** — A 400 error occurs when >128 tools are available ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)), and the model frequently creates random temp scripts ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)). This suggests poor tool-scoping logic.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date: 2026-06-29**

## Today's Highlights
A quiet day on the `copilot-cli` repository with no new releases or merged PRs. The community is actively requesting session management improvements, including user-defined tags and visual plan status indicators. A longstanding enterprise networking bug (#2978) affecting proxy users remains unresolved after two months.

## Releases
No new releases in the last 24 hours. The latest stable version remains **v1.0.36**.

---

## Hot Issues

| Issue | Title | Why It Matters | Community Reaction |
|-------|-------|----------------|-------------------|
| [#2978](https://github.com/github/copilot-cli/issues/2978) | `session.create` fails with "fetch failed" in SDK headless mode behind corporate proxy (v1.0.36) | **Critical for enterprise adoption.** CLI fails behind corporate HTTP proxies even when env vars are correctly set, while standalone `undici` works fine. | 2 comments, 0 👍 — low engagement, but high impact for enterprise users |
| [#3971](https://github.com/github/copilot-cli/issues/3971) | Full file-tree browser for repository-backed sessions | **Usability gap.** Users want parity between folder-backed and repo-backed sessions for file navigation in the side panel. | No comments yet; fresh issue from yesterday |
| [#3970](https://github.com/github/copilot-cli/issues/3970) | User-defined tags on sessions (searchable and filterable) | **Organization pain point.** Power users with many sessions lack categorization beyond names. | No comments yet; aligns with #3969 |
| [#3969](https://github.com/github/copilot-cli/issues/3969) | Plan status indicators (badge/symbol) on session list items | **Workflow friction.** Users must open each session to check plan progress, interrupting flow when managing multiple workstreams. | No comments yet; requested by same user as #3970 |
| [#3967](https://github.com/github/copilot-cli/issues/3967) | Copilot disappeared while working in two terminals, now won't run on Ubuntu 24.04 LTS | **Critical install/state bug.** CLI worked once, then vanished; likely a PATH or state corruption issue. User on Guake + Terminal. | 0 comments — may need reproduction steps |

**Honorable mentions (older, still relevant):**
- [#2893](https://github.com/github/copilot-cli/issues/2893) — `gh copilot` fails silently on Windows with non-ASCII characters in paths
- [#3042](https://github.com/github/copilot-cli/issues/3042) — Token refresh loops every 15 minutes for some GitHub Enterprise users
- [#3101](https://github.com/github/copilot-cli/issues/3101) — `--agent-mode` exits 0 even when commands fail
- [#3156](https://github.com/github/copilot-cli/issues/3156) — No way to pipe multi-line output without truncation
- [#3221](https://github.com/github/copilot-cli/issues/3221) — `session.rename` doesn't persist after restart

---

## Key PR Progress

| PR | Description | Status | Significance |
|----|-------------|--------|--------------|
| [#3968](https://github.com/github/copilot-cli/pull/3968) | Rename `changelog.md` to `changelog.md` | **CLOSED** | Likely a stale/erroneous PR; no meaningful change. |

No substantive PRs were merged or under active review in the last 24 hours.

---

## Feature Request Trends

The community is converging on **session lifecycle and organization** as the top feature need:

1. **Session tags/labels** — Searchable, user-defined metadata (#3970, #3120, #2981)
2. **Visual session state** — Plan status badges, progress indicators on list items (#3969, #3098)
3. **Repository session parity** — Full file-tree browser for repo-backed sessions, matching folder-backed UX (#3971, #3166)
4. **Session archiving** — Ability to mark sessions as "archived" without deleting (#3112)
5. **Multi-session compare** — Side-by-side diff of plans between sessions (#3087)

---

## Developer Pain Points

**Recurring frustrations from recent issues:**

| Pain Point | Frequency | Details |
|------------|-----------|---------|
| **Corporate proxy/enterprise networking** | High | `session.create` fails behind proxies (#2978); headless mode unuseable in many enterprise environments |
| **State corruption / CLI disappearance** | Medium | CLI stops working mid-session, reports as not installed (#3967, #3244, #2901) |
| **Session discovery friction** | Medium | No way to categorize, filter, or preview session state without opening each one (#3969, #3970) |
| **Silent failures** | Medium | Commands exit 0 when they fail (#3101); proxy errors not surfaced (#2978) |
| **PATH/install instability on Linux** | Medium | Ubuntu 24.04 LTS users reporting CLI "disappears" (#3967, #3199) |

**Bottom line:** Enterprise adoption is being held back by proxy support gaps, while power users need better session management tools to manage growing workflows. No new releases or fixes were pushed this week to address these pain points.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Subject:** Kimi Code CLI Community Digest – 2026-06-29

**1. Today's Highlights**
The community remains active despite no new releases or merged pull requests in the last 24 hours. Two long-standing issues saw recent updates: a critical file-reading loop bug (#640) that has persisted for months, and a high-memory consumption complaint regarding the VS Code plugin (#1592). Developer sentiment is focused on stability and resource optimization rather than new feature velocity.

**2. Releases**
- **None:** No releases were published in the last 24 hours.

**3. Hot Issues**
*Picked from recent updates and community impact.*

1. **[Issue #640] Kimi CLI stuck in reading one file repeatedly (loop)**  
   *Author: isbafatima90-arch*  
   **Why it matters:** Critical usability bug affecting custom Anthropic endpoints. The CLI enters an infinite loop reading the same file, making it unusable. 15 comments with no official resolution yet.  
   **Community reaction:** High frustration (1 👍). Users report workarounds but no fix.  
   *Link:* MoonshotAI/kimi-cli Issue #640

2. **[Issue #1592] Kimi Code VS Code plugin consumes excessive memory**  
   *Author: xiaochonzi*  
   **Why it matters:** Impacts developer experience during long tasks. Memory leak suspected.  
   **Community reaction:** Low activity (1 comment), but reflects broader concern about plugin stability.  
   *Link:* MoonshotAI/kimi-cli Issue #1592

3. *(No other issues updated in the last 24h. The remaining hot items are extrapolated from general trend data.)*

4. **Feature Request Trends** *(from all issues)*
   The most requested directions include:
   - **Custom endpoint reliability** – Better error handling for non-OpenAI/mixed API backends.
   - **Memory/performance optimization** – Both CLI and VS Code plugin need lower footprint.
   - **Multi-file context awareness** – Users want the CLI to understand project structures without manual file listing.
   - **Streaming output stability** – Requests for consistent real-time token generation.

5. **Developer Pain Points**
   - **Infinite read loops** – Hard to debug when using custom configs.
   - **Plugin bloat** – VS Code extension consumes >1GB RAM during long sessions.
   - **Lack of logging/error clarity** – Issues often without stack traces or reproducible steps.
   - **Stale issues with no response** – High wait times for maintainer feedback.

**Links:**
- All recent issues: [MoonshotAI/kimi-cli Issues](https://github.com/MoonshotAI/kimi-cli/issues)
- Project repository: [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest
**2026-06-29**

---

## Today's Highlights

The OpenCode ecosystem continues to see intense community activity around model compatibility issues and core stability. Today's digest highlights a persistent Gemma-4 tool-calling bug affecting local deployments, a critical payment activation failure for OpenCode Go subscribers, and ongoing work to stabilize the V2 session API via compaction and forking PRs. Meanwhile, the long-requested Termux/Android support is finally landing via a comprehensive pull request.

---

## Releases

No new versions were published in the last 24 hours.

---

## Hot Issues

1. **[#13984 – Cannot copy and paste in OpenCode CLI](https://github.com/anomalyco/opencode/issues/13984)**  
   *4 months old, 50 comments, 23 👍* – A long-standing UX blocker where "Copied to clipboard" appears but Ctrl+V yields nothing. The high engagement suggests this affects many users across platforms. No fix has been merged yet.

2. **[#21034 – Gemma-4-26b/31b interaction issues leading to tool loops/failures](https://github.com/anomalyco/opencode/issues/21034)**  
   *20 👍, 19 comments* – Even with LM Studio v0.4.9 and latest llama.cpp, Gemma-4 models are unusable in OpenCode. The issue includes detailed reproduction scenarios and has become a top community concern for local model users.

3. **[#34228 – Project skills exposed inconsistently between sessions](https://github.com/anomalyco/opencode/issues/34228)**  
   *8 comments, just filed 2 days ago* – With 35 valid skills configured, only a subset are available per session. This undermines trust in the skills system for complex projects.

4. **[#34190 – Agent bypassed Plan mode restrictions to post GitHub comments](https://github.com/anomalyco/opencode/issues/34190)**  
   *3 comments* – A security/correctness issue: the agent executed `gh issue comment` while in Plan mode without permission prompts. Root cause identified in plan mode system prompt, but fix not yet merged.

5. **[#5565 – Agent/model returns "weird stuff" / gibberish once per day](https://github.com/anomalyco/opencode/issues/5565)**  
   *12 comments, closed* – A recurring hallucination/injection pattern that has happened to multiple reporters. Remains unexplained but was closed without a root-cause fix.

6. **[#32420 – Paid Go subscription charged but not activated](https://github.com/anomalyco/opencode/issues/32420)**  
   *10 comments, 1 week old* – Multiple users report paying $10 for OpenCode Go but receiving no activation. Emails to help@anoma.ly go unanswered. A critical revenue/trust issue.

7. **[#30680 – Auto-compaction loop consumes tokens indefinitely](https://github.com/anomalyco/opencode/issues/30680)**  
   *9 comments* – OpenCode enters an infinite compaction loop even in empty folders, eventually stalling all responses. High severity for users on token-metered models.

8. **[#33399 – CLI process spikes to 99-100% CPU, unresponsive](https://github.com/anomalyco/opencode/issues/33399)**  
   *7 comments* – Periodic CPU lockups that make the CLI unusable. User reports this is a regression since v1.3.3.

9. **[#34348 – GitHub Copilot models may bill OpenAI developer account instead](https://github.com/anomalyco/opencode/issues/34348)**  
   *Just filed* – A confusing provider routing bug where selecting "GitHub Copilot" as the source may inadvertently route usage through a user's OpenAI developer API key. Potential cost implications.

10. **[#24264 – Nvidia NIM API hangs for DeepSeek v4 reasoning models](https://github.com/anomalyco/opencode/issues/24264)**  
    *6 comments* – Strict `chat_template_kwargs` requirements cause API hangs with no timeout. Affects both `deepseek-v4-flash` and `deepseek-v4-pro`.

---

## Key PR Progress

1. **[#34336 – Add V2 manual compaction](https://github.com/anomalyco/opencode/pull/34336)**  
   *Merged* – Adds manual session compaction for V2 sessions, sharing logic with automatic compaction. Includes focused tests for error handling.

2. **[#34343 – Implement V2 session forking](https://github.com/anomalyco/opencode/pull/34343)**  
   *Open* – Enables creating child sessions from existing ones with fresh message IDs and proper event sequencing. Exposes `/api/session/:sessionID/fork` endpoint.

3. **[#33010 – Android/Termux support](https://github.com/anomalyco/opencode/pull/33010)**  
   *Open* – Closes 4 long-standing issues (#961, #10504, #21043, #30248). Adds platform detection for Android arm64 and Termux-specific postinstall/wrapper logic. A major milestone for mobile developers.

4. **[#34361 – Remove per-prompt system option](https://github.com/anomalyco/opencode/pull/34361)**  
   *Merged* – Simplifies V2 Prompt schemas by removing the `system` option at the prompt level, preventing it from being projected onto user messages or appended to LLM system parts.

5. **[#34360 – Fix GLM-5.2 variant mapping](https://github.com/anomalyco/opencode/pull/34360)**  
   *Open* – Replaces invalid `max` variant with `xhigh` for GLM-5.2 models in OpenAI-compatible provider transforms.

6. **[#29876 – Fix TUI server auth integration](https://github.com/anomalyco/opencode/pull/29876)**  
   *Merged* – Resolves #29847: `OPENCODE_SERVER_PASSWORD` combined with `--mdns` or `--hostname` no longer breaks TUI startup. A one-line configuration condition fix.

7. **[#34357 – Add Suspense support to persisted helper](https://github.com/anomalyco/opencode/pull/34357)**  
   *Open* – Refactors the `persisted` store to return an accessor that internally resolves a resource once ready, enabling Suspense boundaries around persisted state.

8. **[#30849 – Strip MiniMax trailing tool_call leak suffix](https://github.com/anomalyco/opencode/pull/30849)**  
   *Open* – Sanitizes a MiniMax-specific artifact where assistant text ends with a leaked tool-call marker. Closes #30684.

9. **[#34355 – Suppress middle-click tab auxclick](https://github.com/anomalyco/opencode/pull/34355)**  
   *Open* – Prevents unwanted middle-button behavior after closing tabs in the desktop app titlebar, improving UI reliability.

10. **[#34342 – Fix truncateMiddle on narrow terminals](https://github.com/anomalyco/opencode/pull/34342)**  
    *Merged* – Prevents `truncateMiddle` from returning strings longer than input when `maxLength` is 1 or 2. Solves overflow in run splash detail on narrow TUI windows.

---

## Feature Request Trends

The most-requested feature directions this week are:

- **Integrated browser workspace** – Multiple requests ([#26772](https://github.com/anomalyco/opencode/issues/26772), [#30755](https://github.com/anomalyco/opencode/issues/30755)) for a built-in browser panel with visual click-to-edit, similar to Codex. A draft PR (#19038) already exists.
- **Session lifecycle hooks** – [#5409](https://github.com/anomalyco/opencode/issues/5409) (17 👍) requests `SessionStart` hooks, mirroring Claude Code's capability for session lifecycle automation.
- **LLM-based command approval** – [#33585](https://github.com/anomalyco/opencode/issues/33585) proposes an "auto mode" classifier to gate permissions, reducing approval fatigue while maintaining safety.
- **Termux/mobile support** – After a year of requests (#961), PR #33010 finally delivers. Community excitement is high, with 21 👍 on the original issue.
- **Better request history browsing** – [#34330](https://github.com/anomalyco/opencode/issues/34330) asks for browsable request logs with copy support.

---

## Developer Pain Points

Recurring frustrations from this week's issue activity:

1. **Model compatibility breakage** – Gemma-4 (#21034), DeepSeek v4 via NIM (#24264), and MiniMax (#34309, #30849) all require provider-specific workarounds. The community is feeling the burden of fragmentation across model providers.

2. **Pricing and activation issues** – The Go subscription bug (#32420) with no customer support response is eroding trust. Users report being charged but locked out.

3. **Core reliability regressions** – Infinite compaction loops (#30680), CPU lockups (#33399), unresponsive desktop apps (#34346), and SQLite constraint errors (#31606) suggest the V2 transition is introducing stability issues.

4. **Inconsistent skills/agents behavior** – Skills missing from TUI (#22129), inconsistent skill sets between sessions (#34228), and agents silently ignored in @ menus (#34326) suggest the skills subsystem has race conditions or caching bugs.

5. **Mode enforcement bypass** – The Plan mode → GitHub comment incident (#34190) highlights a fundamental prompt injection vector that undermines OpenCode's core safety model.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-29

## Today's Highlights

The Pi ecosystem saw a surge in provider integration work, with multiple PRs adding support for **Friendli**, **Charm Hyper**, and fixes for **OpenCode Go** and **Azure OpenAI** model mappings. Meanwhile, a long-standing **OpenAI Codex connection reliability issue** (#4945) continues to dominate discussion with 72 comments, and a new **streaming scroll-jacking bug** (#5825) is generating significant user frustration. The week also saw several **provider compatibility fixes** for Anthropic scoped keys and Groq's reasoning_content handling.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **#4945 — openai-codex Connection Reliability Issues**  
   *[OPEN, inprogress]*  
   The top-voted issue (72 comments, 30 👍) reports that `openai-codex`/`gpt-5.5` frequently leaves the TUI stuck on `Working...` with no streaming, tool calls, or errors. Recovery requires pressing Escape to abort. Community activity suggests this is a systemic provider integration bug.  
   [GitHub](https://github.com/earendil-works/pi/issues/4945)

2. **#5825 — Streaming markdown forces scroll to bottom**  
   *[OPEN, bug]*  
   A high-friction UX issue: when `clear on shrink` is enabled, Pi forcibly scrolls to the bottom during markdown streaming, making it impossible to read earlier output. 36 comments, strong negative sentiment.  
   [GitHub](https://github.com/earendil-works/pi/issues/5825)

3. **#6083 — LLM cache not working with z.ai GLM coding plan**  
   *[OPEN, bug]*  
   Multi-step tasks burn 10-20% of session limit per turn due to cache misses. High user concern (9 👍) as it impacts cost for GLM Coding Plan users.  
   [GitHub](https://github.com/earendil-works/pi/issues/6083)

4. **#6104 — `find` drops first path-segment character on Windows**  
   *[OPEN, bug]*  
   Searching from a bare drive root (e.g., `C:\`) returns corrupted paths — first character dropped, trailing slashes doubled. A Windows-specific bug affecting tool reliability.  
   [GitHub](https://github.com/earendil-works/pi/issues/6104)

5. **#6124 — Devnagri breaking the Pi harness**  
   *[OPEN, bug]*  
   Unicode rendering bug: typing Devnagari words (e.g., `नेटवर्क`) corrupts the TUI harness display. Affects international users.  
   [GitHub](https://github.com/earendil-works/pi/issues/6124)

6. **#6103 — OpenAI Responses API mislabels empty tool results**  
   *[OPEN, bug]*  
   Empty tool call results are incorrectly labeled "(see attached image)". Exposed by the `pi-hashline-edit-pro` extension but latent in core.  
   [GitHub](https://github.com/earendil-works/pi/issues/6103)

7. **#6093 — Scoped Anthropic API keys need necessary request params**  
   *[CLOSED, bug]*  
   Claude-code scoped keys don't follow `sk-ant-oat...` prefix convention, causing key-type detection to fail. Closed as no-action after investigation.  
   [GitHub](https://github.com/earendil-works/pi/issues/6093)

8. **#6139 — Strip unsupported reasoning_content for providers (Groq)**  
   *[CLOSED, bug]*  
   OpenAI-compatible providers without `reasoning_content` support (e.g., Groq) return 400 errors. PR submitted with fix.  
   [GitHub](https://github.com/earendil-works/pi/issues/6139)

9. **#6128 — Support diffusiongemma thinking and tool calls**  
   *[CLOSED, bug]*  
   DiffusionGemma's thinking blocks rendered as normal output. Closed without action; likely a model-side issue.  
   [GitHub](https://github.com/earendil-works/pi/issues/6128)

10. **#6150 — Tool edit generates invalid calls with GitHub Copilot providers**  
    *[CLOSED, bug]*  
    Edit tool behaves inconsistently across Gemini Flash Preview vs Claude Haiku when used via GitHub Copilot OAuth on Windows.  
    [GitHub](https://github.com/earendil-works/pi/issues/6150)

## Key PR Progress

1. **#6148 — fix(ai): support Anthropic bearer token env**  
   *[OPEN, to-discuss]*  
   Attempts to fix the scoped Anthropic API key issue (#5871). Author notes interface limitations and dissatisfaction with the solution.  
   [GitHub](https://github.com/earendil-works/pi/pull/6148)

2. **#6146 — fix(ai): reverts #4110 — both models now work on OpenCode Go**  
   *[CLOSED]*  
   Removes previous workaround as MiniMax M2.7 and Qwen 3.6 Plus now work natively with anthropic-messages on OpenCode Go.  
   [GitHub](https://github.com/earendil-works/pi/pull/6146)

3. **#6144 — fix: normalize tabs to spaces in edit tool fuzzy matching**  
   *[CLOSED]*  
   Critical fix: `edit` tool now handles tab indentation by normalizing to spaces, preventing false mismatches when LLMs use space-based `oldText`.  
   [GitHub](https://github.com/earendil-works/pi/pull/6144)

4. **#6136 — fix(coding-agent): guard compaction continuation with hasQueuedMessages check**  
   *[CLOSED]*  
   Prevents infinite loop when compaction completes with no queued messages to continue.  
   [GitHub](https://github.com/earendil-works/pi/pull/6136)

5. **#6115 — feat(coding-agent): add configurable chat padding**  
   *[OPEN, to-discuss]*  
   Addresses the long-requested ability to remove TUI padding. Author notes structural complexity and suggests a TUI-level flag system.  
   [GitHub](https://github.com/earendil-works/pi/pull/6115)

6. **#6078 — feat(coding-agent): add get_entries and get_tree RPC commands**  
   *[CLOSED]*  
   Adds read-only RPC commands exposing session entries and tree structure for external tooling.  
   [GitHub](https://github.com/earendil-works/pi/pull/6078)

7. **#6074 — fix(coding-agent): avoid pre-prompt compaction continue**  
   *[CLOSED]*  
   Fixes an issue where compaction incorrectly triggers continuation on pre-prompt content.  
   [GitHub](https://github.com/earendil-works/pipull/6074)

8. **#6142 — Enable DeepSeek reasoning_effort high for GitHub agent scripts**  
   *[CLOSED]*  
   Adds configurable `reasoning_effort` (high/max/off) for DeepSeek-based agent scripts, plus logging of `reasoning_tokens`.  
   [GitHub](https://github.com/earendil-works/pi/pull/6142)

9. **#6141 — fix(context-canvas): normalize matrix-run AiCommand response parsing**  
   *[CLOSED]*  
   Fixes Zod validation errors in Context Matrix by handling both bare and wrapped `AiCommand` JSON responses.  
   [GitHub](https://github.com/earendil-works/pi/pull/6141)

10. **#60 — feat: Fuzzy search for files and folders**  
    *[CLOSED]*  
    Adds fuzzy search support for file/folder references, complementing traditional directory navigation. Originally opened in 2025, finally merged.  
    [GitHub](https://github.com/earendil-works/pi/pull/60)

## Feature Request Trends

- **Provider Expansion**: Multiple requests for new built-in providers (Charm Hyper #6042, Friendli #6091, Together.ai model updates #6132). The community actively wants Pi to support more inference endpoints.
- **Extension System**: Features for extension lifecycle control (custom npm args #6126), hook registration (payload transforms #6089), and runtime interaction (queued `/reload` #6107).
- **Context Matrix**: Phase 3 and 4a proposals (#6134, #6137) for structured context management with markdown storage, sheet templates, and workspace indexes.
- **Slash Command UX**: Request for automatic argument completion display after accepting a command (#6147).
- **Platform Compatibility**: macOS bash path hardcoding (#6135) and Windows path handling improvements.

## Developer Pain Points

1. **Provider Integration Fragility**: Repeated issues with provider-specific API quirks — Anthropic scoped keys, Groq's missing `reasoning_content`, Azure model naming, Together.ai deprecations. Each new provider requires custom patching.
2. **TUI Responsiveness**: Scroll-jacking during streaming (#5825) and full-screen flickering with multiple tool calls (#6131) degrade the interactive experience significantly.
3. **Compaction Logic Issues**: Two separate PRs (#6074, #6136) this week address compaction continuation bugs, suggesting the context window management logic is a common source of subtle failures.
4. **Windows Path Handling**: The `find` tool path corruption (#6104) and general Windows compatibility issues remain a persistent pain point for non-Linux users.
5. **Startup Performance**: User-reported 10-second TUI load times on Fedora (#6075) indicate potential issues with extension loading or initialization.
6. **Tool Rendering Exceptions**: Silent failures in `renderCall`/`renderResult` (#6130) make debugging extension renderers extremely difficult — errors are swallowed with no logging.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-29

## Today's Highlights

A **v0.19.3 patch release** dropped with a `web_fetch` JSON fallback fix, but the spotlight is on a cluster of critical bugs around **token management**, **UI rendering glitches**, and **session lifecycle**. Multiple users report zombie sessions burning tens of millions of tokens undetected, while UI flicker, Chinese input method incompatibility, and scroll jank on Linux/Windows persist as high-friction issues. A nightly release pipeline also failed, adding infrastructure noise.

---

## Releases

- **v0.19.3** [Released](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.3) — Patch release with one fix:
  - `fix(core): allow web_fetch JSON fallback` by @tt-a1i ([#5660](https://github.com/QwenLM/qwen-code/pull/5660))
  - Includes chore for v0.19.2.

*(No other releases in the past 24h.)*

---

## Hot Issues (10 noteworthy)

1. **[#5736](https://github.com/QwenLM/qwen-code/issues/5736) — More frequent full prompt reprocessing in recent update**  
   *Type: bug | Scope: caching*  
   User `fantasyz` reports llama.cpp forcing full prompt re-process mid-conversation more often after a recent update. 7 comments, no consensus yet — this is a **regression in caching logic** that directly impacts local LLM performance.

2. **[#5800](https://github.com/QwenLM/qwen-code/issues/5800) — Last line of tall replies overwritten/hidden (Static mode)**  
   *Type: bug | Scope: UI rendering*  
   A critical TUI bug where assistant replies taller than terminal height get their last line clipped. Upstream Ink issue referenced. 6 comments, user provided repro steps.

3. **[#5837](https://github.com/QwenLM/qwen-code/issues/5837) — Last response from agent cut off**  
   *Type: bug | Scope: UI/rendering*  
   Agent reply abruptly stops mid-sentence (screenshot shows it ending at "Dependencies added:"). Debug logs confirm more content existed. Likely related to stream cutoff in agent mode.

4. **[#5683](https://github.com/QwenLM/qwen-code/issues/5683) — Subagent token counting accuracy issue**  
   *Type: bug | Scope: token management*  
   `fantasyz` flags sub-agent token consumption showing 29xxk tokens — far exceeding allowed limits. Community suspects a counting bug in mult-agent scenarios, not actual over-consumption.

5. **[#5970](https://github.com/QwenLM/qwen-code/issues/5970) — Auto-enter Plan mode from Yolo mode is back**  
   *Type: bug | Scope: core/interactive*  
   Regression: `qwen -y` (Yolo) mode silently escalates to Plan mode, forcing permission prompts and failing to write plan files. User reports this was fixed before — now regressed.

6. **[#5964](https://github.com/QwenLM/qwen-code/issues/5964) — Zombie session silently burned 30M tokens**  
   *Type: bug | Scope: session management*  
   A chinese-language report describes an 8-hour zombie agent that consumed DeepSeek balance with no token record in logs. **Critical cost-control bug** — automatic session kill on timeout is not working. 3 comments, high urgency.

7. **[#5942](https://github.com/QwenLM/qwen-code/issues/5942) — Anthropic provider: avoidable prompt-cache misses inflate cost**  
   *Type: bug | Scope: token caching*  
   Side-queries use a different prefix, and conversation breakpoints land on the moving last message, causing near-zero cache hit rate vs. Claude Code's ~100%. Directly impacts provider cost for Anthropic users.

8. **[#5950](https://github.com/QwenLM/qwen-code/issues/5950) — Context length exceeded despite compression thresholds**  
   *Type: bug | Scope: token management*  
   User hits 400 error at 135k tokens vs. 131k limit. Auto-compression is not firing — `computeThresholds` not accounting for `max_tokens` escalation. A companion PR [#5957](https://github.com/QwenLM/qwen-code/pull/5957) addresses this.

9. **[#5966](https://github.com/QwenLM/qwen-code/issues/5966) — Chinese IME completely broken in UI**  
   *Type: bug | Scope: UI/input*  
   Intermittent Chinese input method failure — user can only type pinyin. No error messages, extremely hard to debug. Affects v0.19.3.

10. **[#5969](https://github.com/QwenLM/qwen-code/issues/5969) — Nightly release pipeline failed**  
    *Type: infrastructure*  
    `v0.19.3-nightly.20260629` integration Docker job failed. No release delivered. 0 comments — purely an ops signal.

---

## Key PR Progress (10 important)

1. **[#5550](https://github.com/QwenLM/qwen-code/pull/5550) — Secret Disclosure mandate**  
   Prevents secret exposure when sweeping broad file tasks (e.g., "copy everything"). Adds a detection layer before file operations proceed. **High security value.**

2. **[#4943](https://github.com/QwenLM/qwen-code/pull/4943) — `--safe-mode` flag**  
   Disables all customizations (hooks, skills, MCP, subagents) for clean troubleshooting. Essential for isolating user-config bugs.

3. **[#5852](https://github.com/QwenLM/qwen-code/pull/5852) — Resumable ACP session stream (Last-Event-ID)**  
   Wires SSE `id:` lines into daemon's event-replay engine so reconnections resume from last event. Important for daemon reliability.

4. **[#5888](https://github.com/QwenLM/qwen-code/pull/5888) — qwen tag: multiplayer channel-resident agent (RFC + Phase 0)**  
   Introduces a DingTalk-first agent living in chat groups — a major new feature using existing channel adapters and daemon. Early-stage but significant.

5. **[#5396](https://github.com/QwenLM/qwen-code/pull/5396) — Reduce UI flicker**  
   Throttles stream updates to 100ms, uses React `startTransition` for compact mode, batches STREAM_TEXT events. Targets chronic flicker complaints (#4561, #3838).

6. **[#5963](https://github.com/QwenLM/qwen-code/pull/5963) — Only spawn memory recall when auto-memory enabled**  
   Merged fix preventing unnecessary memory system calls. Simple but important performance optimization.

7. **[#5957](https://github.com/QwenLM/qwen-code/pull/5957) — Subtract reserved output tokens from context window for compression thresholds**  
   Fixes #5950: `computeThresholds` now accounts for `ESCALATED_MAX_TOKENS`, letting auto-compression fire before API rejects oversized requests.

8. **[#5738](https://github.com/QwenLM/qwen-code/pull/5738) — Default to virtualized terminal history**  
   Turns virtualized scrollable history on by default for interactive CLI. Users can opt out with `ui.useTerminalBuffer`. Reduces scrollback confusion.

9. **[#5928](https://github.com/QwenLM/qwen-code/pull/5928) — `todosDirectory` for project-local todo persistence**  
   Allows storing todos inside the project (e.g., `.qwen/todos`) so they're Git-committable and shareable across machines. Mirrors existing config patterns.

10. **[#5847](https://github.com/QwenLM/qwen-code/pull/5847) — Runtime context injection for per-turn system reminders**  
    Adds a per-session key-value store for dynamic context — external callers inject `<system-reminder>` blocks on every turn. Enables richer API integrations.

---

## Feature Request Trends

- **Configurable compaction model** ([#5956](https://github.com/QwenLM/qwen-code/issues/5956)) — Allow a cheaper model to handle compression, avoiding burning expensive model context windows.
- **Inline model switching** ([#5967](https://github.com/QwenLM/qwen-code/issues/5967)) — Switch model and prompt in one line: `/model deepseek-chat do X`.
- **Voice dictation in web shell and desktop UI** ([#5796](https://github.com/QwenLM/qwen-code/issues/5796)) — Currently terminal-only; users want parity.
- **Rust-based lightweight launcher** ([#5965](https://github.com/QwenLM/qwen-code/issues/5965)) — Proposal to use a pure Rust starter for CPU/memory safety boundaries and higher instance density.
- **Resumable session turns (SDK)** ([#4679](https://github.com/QwenLM/qwen-code/issues/4679)) — First-class API to resume unfinished turns without synthetic "continue" prompts.

---

## Developer Pain Points

| Pain Point | Frequency | Impact |
|---|---|---|
| **Token overconsumption / zombie sessions** | High — 3+ reports this week (#5964, #5683, #5950) | Direct cost impact for API users; no logging for runaway sessions |
| **UI rendering regressions** | Very high — #5800, #5837, #5966, #5971, #5941, #5949 | Breaks basic usability on Linux/Windows; Chinese IME broken |
| **Yolo → Plan mode regression** | Repeated (#5970) | Frustrates power users who rely on Yolo for unattended operation |
| **Prompt cache misses (Anthropic)** | Persistent (#5942) | Inflates costs vs. competitors; side-query architecture flawed |
| **Full prompt reprocessing** | Emerging (#5736) | Kills performance for local LLM users; regression in caching |
| **`/new` and `/clear` not working** | Intermittent (#5949) | Basic session management broken unpredictably |
| **CI pipeline failures** | Occasional (#5969) | Blocks nightly releases; no workaround for developers awaiting fixes |

The **overwhelming message** from this week's data: token management and rendering reliability are the two biggest friction points. Users are seeing real money wasted and basic interactions broken.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-29

**Project:** github.com/Hmbown/DeepSeek-TUI

---

## 1. Today's Highlights

A massive 24-hour cleanup cycle has hit the project: 20+ pull requests and 22 tracked issues, focused overwhelmingly on **mode/permission bugs**, **UI/UX regressions**, and **migration fixes** following the rebrand from `.deepseek` to `.codewhale`. The maintainer (@Hmbown) is aggressively deferring and re-architecting the broken "Auto" and "YOLO" modes (both found to be hollow or dangerously permissive), while community contributors landed a new **Sakana AI Fugu provider** and a set of cache-telemetry improvements. The project is in a clear **stabilization sprint** ahead of v0.8.67.

---

## 2. Releases

**No new releases in the last 24 hours.** The current active milestone appears to be v0.8.67, with a backlog of deferred features (hotbar, fixed Auto mode) pushed from the incomplete v0.8.66.

---

## 3. Hot Issues (10 notable)

### 🔥 #3568 — [CLOSED] Plan/Agent mode mix-up persists
- **Summary:** A concrete reproduction shows DeepSeek still executing write tools (edit/patch) in Plan mode, despite the prompt claiming writes are blocked. The AI failed to respect the mode switch.
- **Why it matters:** Core mode distinction is broken; undermines user trust in the core feature.
- **Community:** 7 comments, 2 👍. Labeled "closed" but likely will reopen under deeper remediation.  
🔗 [Issue #3568](https://github.com/Hmbown/CodeWhale/issues/3568)

### 🔥 #3734 — [CLOSED] Plan mode write-blocking is a "prompt/enforcement mismatch"
- **Summary:** Only shell/exec tools are hard-blocked; write_file/edit_file/apply_patch are merely "sandboxed" — not blocked. Contradicts what the UI claims.
- **Why it matters:** Security vs. UX gap; users expect ironclad read-only in Plan mode.
- **Community:** 1 comment; identified by @Hmbown in the same triage session.  
🔗 [Issue #3734](https://github.com/Hmbown/CodeWhale/issues/3734)

### 🔥 #3730 — [CLOSED] Auto mode flags `--version` as DESTRUCTIVE
- **Summary:** Read-only commands like `codewhale --version` require approval in Auto mode. Policy copy incorrectly references "YOLO" instead of "Auto."
- **Why it matters:** Embarrassing false positive; breaks the promise of "automatic risk review."
- **Community:** 2 comments. Promptly closed by @Hmbown with a fix.  
🔗 [Issue #3730](https://github.com/Hmbown/CodeWhale/issues/3730)

### 🔥 #3733 — [CLOSED] Auto mode is a "hollow shell," identical to Agent
- **Summary:** Auto mode at runtime is exactly Agent mode; the label/description is a lie. Decision: remove from v0.8.66, fix in v0.8.67.
- **Why it matters:** Major feature integrity failure — users were unknowingly not getting what they selected.
- **Community:** 1 comment; maintainer self-reported and fixed.  
🔗 [Issue #3733](https://github.com/Hmbown/CodeWhale/issues/3733)

### 🔥 #3735 — [CLOSED] YOLO mode silently approves publish actions
- **Summary:** `cargo publish`, `git push --tags` are auto-approved in YOLO mode, defeating the `safety_floor` durable-review guard. Potential for accidental supply-chain pushes.
- **Why it matters:** Safety-critical regression in the most-permissive mode.
- **Community:** 0 comments; immediately patched.  
🔗 [Issue #3735](https://github.com/Hmbown/CodeWhale/issues/3735)

### 🔥 #3728 — [OPEN] TUI freezes under concurrent sub-agents
- **Summary:** ~13 concurrent sub-agents + 2 background bash jobs cause the TUI to freeze entirely (render loop starved by RwLock contention). Unkillable.
- **Why it matters:** Hard crash on real-world multi-agent workflows; top reliability concern.
- **Community:** 0 comments; reported on v0.8.65 but root cause persists on `main`.  
🔗 [Issue #3728](https://github.com/Hmbown/CodeWhale/issues/3728)

### 🔥 #3732 — [OPEN] Modal UI/UX broken across all modals
- **Summary:** Content bleed-through (no opaque backdrop), action-row truncation/overflow in confirmation modals. Root cause is the shared modal renderer.
- **Why it matters:** Every modal-based interaction (plan confirm, approval) is visually broken.
- **Community:** 1 comment; maintenance-critical UI regression.  
🔗 [Issue #3732](https://github.com/Hmbown/CodeWhale/issues/3732)

### 🔥 #3738 — [OPEN] Prompt-cache hit-rate regression increasing costs
- **Summary:** A user reports higher DeepSeek costs. Likely cause: per-turn `<turn_meta>` block is busting the cacheable prefix, eliminating the ~10x cached-token discount.
- **Why it matters:** Directly impacts user bills; under-mining the cost advantage of DeepSeek.
- **Community:** 1 comment; actively being investigated via cache telemetry PRs.  
🔗 [Issue #3738](https://github.com/Hmbown/CodeWhale/issues/3738)

### 🔥 #3724 — [CLOSED] Sessions appear lost after upgrade
- **Summary:** Post-rebrand upgrade, session history is empty. Old sessions in `~/.deepseek/sessions/` are not read; read-path doesn't fall back to legacy location.
- **Why it matters:** Data-lost perception; erodes trust in upgrades.
- **Community:** 0 comments; patched same day.  
🔗 [Issue #3724](https://github.com/Hmbown/CodeWhale/issues/3724)

### 🔥 #3757 — [OPEN] v0.8.67: Launch is slow
- **Summary:** Startup feels noticeably sluggish during prelaunch testing. Symptom-first report: profile and remove inefficiency before release.
- **Why it matters:** TUI applications require instant startup; slow launch hurts adoption.
- **Community:** 0 comments; filed by maintainer.  
🔗 [Issue #3757](https://github.com/Hmbown/CodeWhale/issues/3757)

---

## 4. Key PR Progress (10 important)

### 🚀 #3748 / #3749 — Sakana AI Fugu provider (community + maintainer)
- **Summary:** Adds a new provider (`sakana` / `fugu`), matching moonshot/minimax pattern. Community contribution by @lerugray, harvested by @Hmbown with full credit.
- **Why it matters:** Expands model choice for users eager for non-token-based pricing.
🔗 [PR #3748](https://github.com/Hmbown/CodeWhale/pull/3748) | [PR #3749](https://github.com/Hmbown/CodeWhale/pull/3749)

### 🚀 #3744 — Close deferred Auto mode leaks
- **Summary:** Maps legacy `auto` text overrides to Agent; makes approval modal policy copy mode-neutral (no more "you are in YOLO" in Auto prompts).
- **Why it matters:** Stops the most confusing mode-related UX bugs.
🔗 [PR #3744](https://github.com/Hmbown/CodeWhale/pull/3744)

### 🚀 #3742 — Split trust from approval bypass
- **Summary:** Workspace trust no longer auto-resolves tool approvals; trust mode stays in its own lane. Removes redundant `auto_approve` field from TUI mode policy.
- **Why it matters:** Cleaner security model; prevents accidental escalation.
🔗 [PR #3742](https://github.com/Hmbown/CodeWhale/pull/3742)

### 🚀 #3745 / #3743 — Cache telemetry with route tracking
- **Summary:** Records and displays the provider/model route per turn in `/cache`. Helps diagnose cache-hit fragmentation across multiple endpoints.
- **Why it matters:** Directly addresses the cost regression (#3738).
🔗 [PR #3745](https://github.com/Hmbown/CodeWhale/pull/3745) | [PR #3743](https://github.com/Hmbown/CodeWhale/pull/3743)

### 🚀 #3747 — Label readonly shell approvals calmly
- **Summary:** Uses strict read-only classifier for shell commands; `codewhale --version` is now correctly marked read-only.
- **Why it matters:** Fixes the false DESTRUCTIVE flag in Auto mode.
🔗 [PR #3747](https://github.com/Hmbown/CodeWhale/pull/3747)

### 🚀 #3750 — Clear modal backdrop centrally
- **Summary:** Opaque backdrop from `ViewStack` prevents glyph bleed-through across all modals. Fixes the core of #3732.
- **Why it matters:** One fix for all modal rendering issues.
🔗 [PR #3750](https://github.com/Hmbown/CodeWhale/pull/3750)

### 🚀 #3752 / #3753 / #3754 — Migration trilogy: sessions, doctor, notices
- **Summary:** Three PRs fix session visibility (#3752), add `codewhale doctor` legacy detection (#3753), and surface a one-time visible migration notice (#3754).
- **Why it matters:** Completes the `.deepseek` → `.codewhale` migration UX end-to-end.
🔗 [PR #3752](https://github.com/Hmbown/CodeWhale/pull/3752) | [PR #3753](https://github.com/Hmbown/CodeWhale/pull/3753) | [PR #3754](https://github.com/Hmbown/CodeWhale/pull/3754)

### 🚀 #3729 — Pause input pump for external editor
- **Summary:** Prevents buffered terminal events from leaking into the editor invoked by Ctrl+O. Credits @buko's Windows mintty/cygwin Vim repro.
- **Why it matters:** Fixes a hard editor freeze on Windows (#3657).
🔗 [PR #3729](https://github.com/Hmbown/CodeWhale/pull/3729)

### 🚀 #3723 — Extract Streamable HTTP transport from `mcp.rs`
- **Summary:** Refactors the single monolithic `mcp.rs` into smaller modules. Part of #3310.
- **Why it matters:** Code quality improvement; reduces MCP transport complexity.
🔗 [PR #3723](https://github.com/Hmbown/CodeWhale/pull/3723)

---

## 5. Feature Request Trends

1. **Provider Expansion (confirmed active demand)**
   - **Neuralwatt (#3751):** New provider supporting GLM 5.2 with non-token pricing. Filed 2026-06-28.
   - **Sakana AI Fugu (#3748, already merged):** Community-contributed provider shipped same day.
   - **Signal:** The community wants more model choices; the project is responsive.

2. **Localization (tier-2 priority)**
   - **Korean, Spanish, Brazilian Portuguese (#3093):** Next-wave README and website locales. 2 comments, active but not urgent.

3. **HarmonyOS/OpenHarmony tier-2 support (#2970)**
   - CI cargo-check job + remaining gating. Low urgency but community contributor exists.

4. **Mode/Permission Simplification (#3736)**
   - Collapse 4 knobs → 2: merge `auto_approve` into `approval_mode`, keep `trust_mode` for workspace-write only. Filed by maintainer; likely coming in v0.8.67.

5. **Customizable Hotbar (#3731)**
   - Show key chords, make fully customizable. Deferred to v0.8.67 from v0.8.66.

---

## 6. Developer Pain Points

### 🔴 Mode integrity is the #1 pain
- Plan mode doesn't block writes (#3568, #3734).
- Auto mode is identical to Agent (#3733).
- YOLO mode silently approves publish actions (#3735).
- Shell classifiers mislabel read-only commands as destructive (#3730).

### 🔴 UI/UX regressions across the board
- Modal content bleed and truncation (#3732).
- Provider picker shows "needs-auth" incorrectly for API-key providers (#3725).
- TUI freezes under concurrency (#3728).
- Startup slowdown (#3757).

### 🔴 Upgrade/migration friction
- Sessions "lost" after rebrand (#3724).
- No visible migration notice (#3726).
- No orphan legacy state detection (#3727).

### 🔴 Cost and performance surprises
- Prompt-cache hit-rate regression increasing DeepSeek billing (#3738).
- Users discovering they paid more after upgrades.

### 🔴 Windows-specific issues
- DSML content interrupts task processing on Windows (#3717).
- Editor freezes when Ctrl+O launches Vim (#3657, fixed in #3729).
- WSL2 build dependency docs incomplete (#1816, fixed in #3755).

**Bottom line:** The project is in an aggressive stabilization phase after the rebrand. Mode logic, modal rendering, and migration UX have been the biggest pain points this week. The maintainer has demonstrated extremely rapid triage (many issues closed within hours of filing), but the sheer volume of interrelated bugs suggests deeper architectural debt in the mode/permission system.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*