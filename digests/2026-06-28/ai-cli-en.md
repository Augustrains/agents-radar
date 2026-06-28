# AI CLI Tools Community Digest 2026-06-28

> Generated: 2026-06-28 02:07 UTC | Tools covered: 9

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

**Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem**
**Date:** 2026-06-28

---

## 1. Ecosystem Overview

The AI CLI tools landscape is experiencing a period of intense, simultaneous maturation and crisis. Across the six major tools actively tracked—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, OpenCode, Qwen Code, DeepSeek TUI, and Pi—communities are grappling with a common set of challenges: runaway token consumption, opaque agent behaviors, and persistent platform-specific regressions that erode developer trust. While each tool pursues distinct architectural visions (Claude Code emphasizes extended reasoning; Gemini CLI invests in security; DeepSeek TUI pushes plugin extensibility), a converging set of feature demands—context compaction, cross-surface parity, agent transparency, and cost governance—indicates that the market is beginning to standardize expectations for what a "professional-grade" AI CLI should provide. The ecosystem is evolving beyond novelty toward reliability, and this week's digests reflect that shift with unusual clarity.

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | Active PRs (24h) | Release Status | Key Signal |
|---|---|---|---|---|
| **Claude Code** | 10 active issues | 2 PRs (1 closed, 1 open) | No new release | Stalled on Opus 4.7 bug; safety filter false-positive flood |
| **OpenAI Codex** | 10 active issues | 10 PRs (mostly open) | 3 alpha releases (Rust CLI) | High churn on MCP OAuth; rate-limit cost crisis |
| **Gemini CLI** | 10 active issues | 10 PRs (mixed open/closed) | 1 nightly release | Security-focused; agent reliability fixes |
| **GitHub Copilot CLI** | 10 active issues | 3 PRs (quiet) | No new release | Windows regressions dominate |
| **OpenCode** | 10 active issues | 10 PRs (mostly merged) | No new release (v1.17.11 stable) | Heavy session UX + tooling improvements |
| **Pi** | 10 active issues | 10 PRs (7 merged, 3 open) | No new release | Extension API expansion; TUI rendering fixes |
| **Qwen Code** | 10 active issues | 10 PRs (mixed) | 1 nightly release | `/loop` transparency; retry loop fixes; cost control |
| **DeepSeek TUI (CodeWhale)** | 10 active issues | 10 PRs (7 closed, 3 open) | No new release (v0.8.66 ledger) | Plugin system launched; cache-hit crisis |

**Observation:** DeepSeek TUI and OpenAI Codex show the most rapid iteration velocity. Claude Code and GitHub Copilot CLI exhibit stalled velocity with unresolved regressions.

---

## 3. Shared Feature Directions

The following themes appear across **three or more** tool communities, indicating broad market demand:

| Shared Requirement | Tools Expressing Need | Specific Details |
|---|---|---|
| **Context/Compaction Control** | Claude Code, OpenCode, Qwen Code | Manual `/compact`, agent-triggered compaction, session-scoped CWD truncation |
| **Non-Destructive Agent Queries** | GitHub Copilot CLI, Gemini CLI, Claude Code | `/btw`-style out-of-band context; ask questions without corrupting session state |
| **Cross-Surface Parity** | Claude Code, OpenAI Codex, Pi | Feature gaps between CLI, VS Code, Desktop, Web; users want consistent capabilities |
| **Cost/Billing Transparency** | OpenAI Codex, Pi, Qwen Code, DeepSeek TUI | Per-token cost breakdowns, credit expiry details, alerting on unexpected consumption |
| **Agent Behavior Visibility** | Gemini CLI, DeepSeek TUI, Claude Code | Visible subagent reasoning, logged trajectory, transparent cron/scheduled tasks |
| **Project-Local Persistence** | Qwen Code, OpenCode, Pi | Git-tracked todos, memories, plans; sync across devices and team members |
| **Windows Parity & Reliability** | GitHub Copilot CLI, Claude Code, OpenAI Codex, OpenCode | Platform-specific bugs (clipboard, sandbox, path handling, auth) eroding trust |
| **Security False-Positive Overrides** | Claude Code, Gemini CLI | "Authorized work" attestation to bypass safety filters without killing sessions |

**Most Convergent Signal:** Context management and cost transparency are the two highest-priority cross-tool demands. Every community reports frustration with opaque memory, unpredictable billing, or both.

---

## 4. Differentiation Analysis

| Dimorphism Factor | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | OpenCode | DeepSeek TUI (CodeWhale) | Pi | Qwen Code |
|---|---|---|---|---|---|---|---|---|
| **Primary Focus** | Extended reasoning | MCP/auth infrastructure | Security & agent reliability | Platform parity (Windows) | Multi-surface session UX | Plugin extensibility + cache optimization | Extension API platform | Background automation + cost control |
| **Target User** | Deep reasoning workflows (research, complex debugging) | Professional developers with enterprise auth needs | Security-conscious enterprise teams | GitHub ecosystem (Linux/Ubuntu users) | Cross-platform & server-mode developers | Cache-conscious power users; Zed ecosystem | Plug-in developers; multilingual users | Automation-first developers; DingTalk/Telegram users |
| **Technical Distinctive** | Thinking summaries, Cowork sub-agents | MCP OAuth concurrency refactor | AST-aware code intelligence; DNS rebinding fixes | GitHub Copilot integration; alt-screen TUI | Path traversal fixes; sandbox project edits | Plugin manifest system; ACP registry | Extension cost reporting API; Devnagri layout fix | `/loop` cron system; multiplayer channel agents |
| **Pain Point Dominance** | Stalled Opus 4.7 bug (10+ weeks) | Rate-limit cost crisis | Agent hangs + false completions | Windows regressions (clipboard, MCP servers) | Memory leaks in server mode | Input cache miss rate vs DeepSeek-Reasonix | TUI flicker; silent failures | Opaque cron tasks; retry loops |
| **Community Mood** | Frustrated (long-standing bug) | Alarmed (billing shock) | Anxious (trust erosion) | Irritated (regressions) | Productive (fixes landing) | Strategically focused (new plugin system) | Engaged (extension API expansion) | Balanced (fixes + new features) |

**Key Differentiation:** Claude Code leads in reasoning depth but is stalled. OpenAI Codex leads in infrastructure velocity. Gemini CLI leads in security rigor. DeepSeek TUI leads in architectural innovation (plugin system, cache-maximal mode). GitHub Copilot CLI lags in all dimensions except niche GitHub integration.

---

## 5. Community Momentum & Maturity

| Metric | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | OpenCode | DeepSeek TUI (CodeWhale) | Pi | Qwen Code |
|---|---|---|---|---|---|---|---|---|
| **Community Engagement** | High (150+ reactions on top bug) | Very High (334👍 on #28879) | Moderate (8👍 on #21409) | Low (20👍 on #2165) | High (34👍 on #8816) | High (24 comments on #1177) | Moderate (34 comments on #5825) | Moderate (6 comments on #5838) |
| **Release Velocity** | Stalled | High (3 alpha releases/day) | Moderate (1 nightly) | Stalled | Moderate (no release today) | Low (no release today; ledger finalized) | Moderate (no release today; many PRs merged) | Moderate (1 nightly) |
| **Feature Velocity** | Low (2 PRs, mostly minor) | High (10 PRs, major auth refactor) | High (10 PRs, security fixes) | Low (3 PRs, mostly doc/stale) | High (10 PRs, session UX + tooling) | High (10 PRs, plugin system + ACP) | High (10 PRs, extension API + fixes) | High (10 PRs, retry loop fix + automation) |
| **Maturity Assessment** | **Maturing slowly** | **Rapidly iterating** | **Pivoting to security** | **Stagnating** | **Healthy growth** | **Architectural leap** | **Platform evolution** | **Balanced maturity** |

**Rapidly Iterating:** OpenAI Codex (infrastructure), DeepSeek TUI (plugin system), OpenCode (session UX)
**Stagnating:** Claude Code (unresolved bug), GitHub Copilot CLI (regression wave)

---

## 6. Trend Signals

The following industry signals emerge from cross-tool community feedback, with direct reference value for developers evaluating AI CLI tools:

1. **Context Management Is the New Battleground** — Every major tool faces user demands for manual compaction, agent-initiated compaction, and transparent session memory. Tools that solve opaqueness and unpredictability (e.g., OpenCode's compaction guard, Qwen Code's `.qwen/loop.md`) will gain trust.

2. **Cost Governance Cannot Be an Afterthought** — OpenAI Codex's rate-limit cost bug (#28879), DeepSeek TUI's cache miss crisis (#1177), and Qwen Code's silent model upgrade (#5819) all demonstrate that billing surprises rapidly erode user confidence. Expect dedicated "cost dashboard" features to become table stakes.

3. **Platform Parity Is a Reliability Signal** — Windows regressions in Copilot CLI and Claude Code correlate with community frustration. Cross-platform consistency (or lack thereof) is increasingly read as a proxy for engineering quality.

4. **Extension/Plugin Systems Are the Next Growth Frontier** — DeepSeek TUI's plugin launch (#3708), Pi's extension API expansion (7 merged PRs), and OpenCode's MiMo tool port (#34270) indicate that extensibility is becoming a competitive differentiator. The battle is shifting from "tool features" to "platform capabilities."

5. **Security as Feature, Not Compliance** — Gemini CLI's three security PRs (DNS rebinding, symlink traversal, env var leaks) and Claude Code's safety filter false-positive reports (#71910–#71920) show that security is no longer a checkbox but a core UX concern. "Authorized work" attestation and user-controlled safety overrides are emerging as requested features.

6. **Agent Transparency Is Non-Negotiable** — Hiding agent behavior (silent scope expansion in Gemini CLI, self-questioning loops in DeepSeek TUI, unlistable cron tasks in Qwen Code) destroys trust. Tools that expose agent reasoning, logged trajectories, and visible subagent activity will win developer confidence.

7. **The "Opus 4.7 Bug" Is a Metaphor** — Claude Code's unresolved thinking summaries bug (10+ weeks, >150 reactions) signals a deeper problem: even the most capable models cannot compensate for broken integration layers. API-handson mismatches (like the missing `display: "summarized"` flag) will become the new class of critical bugs as tools increasingly rely on model-specific API parameters.

---

**Bottom Line for Decision-Makers:**
- **If you prioritize reasoning depth and can tolerate instability:** Claude Code remains unmatched but is risky for production workflows.
- **If you need enterprise-grade infrastructure and rapid iteration:** OpenAI Codex offers the highest velocity, but watch billing closely.
- **If security is your top concern:** Gemini CLI is investing heavily; the DNS rebinding fix and symlink traversal patches are production-ready.
- **If you are a Windows/Linux parity-seeking GitHub user:** Copilot CLI is currently the weakest option due to regression density.
- **If you want a stable, extensible platform:** OpenCode and Pi offer the best balance of reliability and innovation.
- **If cost efficiency is critical:** DeepSeek TUI (CodeWhale) is making the most aggressive moves on cache optimization, but its plugin system is still nascent.
- **If you need background automation and multi-channel integration:** Qwen Code's `/loop` and DingTalk/Telegram agents are unique.

The ecosystem is converging on context transparency, cost governance, and extensibility as the three pillars of professional-grade AI CLI tools. Tools that fail on any of these dimensions will likely lose developer trust in the coming quarters.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-28** | Source: github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Pull Requests have attracted the most community discussion and represent the Skills generating greatest interest:

### #1298 — Skill Creator Eval Fix (Open)
**Functionality:** Fixes `run_eval.py` which consistently reports 0% recall for every skill description, rendering the description-optimization loop useless. Addresses Windows stream reading, trigger detection, and parallel worker issues.
**Discussion highlights:** 10+ independent reproductions of the 0% recall bug (#556). The PR reveals the optimization loop has been "optimizing against noise." Multiple contributors (joshuawowk, Polluelo978) submitted overlapping fixes; this PR consolidates them.
**Status:** 🔴 Open | [GitHub](https://github.com/anthropics/skills/pull/1298)

### #514 — Document Typography Skill (Open)
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Covers typographic quality control for every document Claude generates.
**Discussion highlights:** Community consensus that orphan/widow issues affect "every document Claude generates." Users noted these are rarely requested but consistently needed.
**Status:** 🔴 Open | [GitHub](https://github.com/anthropics/skills/pull/514)

### #486 — ODT Skill: OpenDocument Creation (Open)
**Functionality:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods). Triggers on mentions of "ODT," "ODS," "LibreOffice," etc.
**Discussion highlights:** Strong interest from open-source ecosystem. Community flagged LibreOffice document handling as a critical gap. Cross-platform compatibility questions raised.
**Status:** 🔴 Open | [GitHub](https://github.com/anthropics/skills/pull/486)

### #83 — Skill Quality & Security Analyzers (Open)
**Functionality:** Two meta-skills: `skill-quality-analyzer` evaluates skills across five dimensions (Structure 20%, Documentation, Examples, Resources, Testing 20%); `skill-security-analyzer` audits for risks.
**Discussion highlights:** First meta-skills submitted to the collection. Community debated whether quality analysis should be built into the skill-creator pipeline rather than a separate skill.
**Status:** 🔴 Open | [GitHub](https://github.com/anthropics/skills/pull/83)

### #723 — Testing Patterns Skill (Open)
**Functionality:** Comprehensive testing coverage including Testing Trophy model, AAA pattern, React Testing Library, mocking strategies, Playwright E2E, accessibility testing, and performance testing.
**Discussion highlights:** Community requested coverage of testing philosophy (what NOT to test). React component testing patterns generated most discussion.
**Status:** 🔴 Open | [GitHub](https://github.com/anthropics/skills/pull/723)

### #360 — AppDeploy Skill (Open)
**Functionality:** Enables Claude to deploy and manage full-stack web apps via AppDeploy.ai, including lifecycle management, environment variables, and rollbacks.
**Discussion highlights:** Deployment from within conversations seen as high-value. Community raised security concerns about granting deployment permissions within chat.
**Status:** 🔴 Open | [GitHub](https://github.com/anthropics/skills/pull/360)

### #181 — SAP-RPT-1-OSS Predictor (Open)
**Functionality:** Integrates SAP's open-source tabular foundation model for predictive analytics on SAP business data.
**Discussion highlights:** First enterprise-ERP integration in the collection. Community discussed training data requirements and SAP-specific data formats.
**Status:** 🔴 Open | [GitHub](https://github.com/anthropics/skills/pull/181)

### #154 — Shodh-Memory Skill (Open)
**Functionality:** Persistent memory system maintaining context across conversations. Uses `proactive_context` calls and rich memory structuring.
**Discussion highlights:** Cross-session memory is the most-requested capability. Community worried about context window bloat and memory reliability.
**Status:** 🔴 Open | [GitHub](https://github.com/anthropics/skills/pull/154)

---

## 2. Community Demand Trends

From the most-discussed Issues, these skill directions show strongest community demand:

| Demand Direction | Key Issue | Demand Signal |
|---|---|---|
| **Skill distribution & trust** | #492 (23 comments) — Community skills under `anthropic/` namespace create trust-boundary vulnerabilities | **Highest:** Namespace security is the top community concern |
| **Org-wide skill sharing** | #228 (14 comments) — Skills should be shareable within organizations without manual file transfers | **High:** Enterprise deployment friction |
| **Skill-creator tooling fixes** | #556, #1169, #1061 (18+ comments combined) — The eval loop consistently reports 0% recall | **Critical:** Blocking all skill optimization workflows |
| **Skill duplication prevention** | #189 (6 comments) — `document-skills` and `example-skills` install identical content | **Moderate:** User experience degradation |
| **Agent governance / safety** | #412 (6 comments) — Safety patterns for AI agent systems | **Emerging:** Security-focused skill demand |
| **Compact memory / context optimization** | #1329 (6 comments) — Symbolic notation for compact agent state | **Emerging:** Long-running agent efficiency |

---

## 3. High-Potential Pending Skills

These PRs have active community engagement and are likely to merge soon:

| PR | Skill | Why It May Land Soon |
|---|---|---|
| #1323 | Skill Creator trigger detection fix | Addresses core 0% recall bug (#556); multiple overlapping efforts converging |
| #1050 | Windows subprocess + encoding fixes | Two 1-line fixes unblocking Windows users; low risk to merge |
| #1099 | Windows pipe reading fix | Unblocks Windows eval pipeline; community has isolated root cause |
| #538 | PDF case-sensitive file references | Simple 8-line fix; broken on case-sensitive filesystems |
| #539 | YAML unquoted description warning | Prevents silent parsing failures; no breaking changes |
| #509 | CONTRIBUTING.md | Addresses community health gap; repo scores 25% on GitHub metrics |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable skill-creation tooling (eval fixes, Windows compatibility, validation) and trust infrastructure (namespace security, org sharing), outpacing demand for any single functional skill.**

The volume of overlapping PRs addressing the same `run_eval.py` 0% recall bug (#556, #1169, #1298, #1323) indicates that the skill-creation *pipeline itself* is the community's primary bottleneck—functional skills cannot be effectively optimized until the evaluation loop works correctly.

---

# Claude Code Community Digest — 2026-06-28

## Today's Highlights

The community remains **most visibly engaged with the unresolved Opus 4.7 thinking summaries bug**—three related issues (#49322, #49268, #59844) have persisted for over two months, accruing 150+ combined reactions and 100+ comments. A new wave of **safety-filter false-positive reports** (#71910–#71920) around drone-related development is flooding the issue tracker, all filed by the same author. Meanwhile, feature requests around **context compaction** (#65114, #71803) and **cross-surface parity** (#71941) are gaining traction.

## Releases

**No new releases in the last 24 hours.** The latest stable version remains at the version reported in prior digests.

## Hot Issues

1. **[#49322 — Opus 4.7 thinking summaries not rendered in VS Code extension](https://github.com/anthropics/claude-code/issues/49322)** — 47 comments, 41 👍. The longest-running open bug. Community frustrated that `showThinkingSummaries: true` does not render thinking blocks in the extension UI. Author reports thorough preflight check.

2. **[#49268 — Thinking summaries missing on Opus 4.7 — harness doesn't set `display: "summarized"`](https://github.com/anthropics/claude-code/issues/49268)** — 46 comments, 75 👍. Digs into root cause: the extended-thinking API changed the default `display` parameter in Opus 4.7. Claude Code's request harness apparently does not propagate this flag. High engagement suggests many users are affected.

3. **[#69706 — API Error: 401 Invalid authentication credentials](https://github.com/anthropics/claude-code/issues/69706)** — 21 comments, 10 👍. A recent (June 20) authentication bug on Windows. Users report valid keys failing mid-session. No official acknowledgment yet; likely a session token expiry issue.

4. **[#49902 — Opus 4.7 thinking summaries not rendered (VSCode extension 2.1.112)](https://github.com/anthropics/claude-code/issues/49902)** — 14 comments, 41 👍. Duplicate of #49322 but significant community overlap. The fact that two issues with identical symptoms persist side-by-side suggests the team has not yet shipped a fix.

5. **[#59844 — `showThinkingSummaries: true` silently no-ops on Opus 4.7](https://github.com/anthropics/claude-code/issues/59844)** — 10 comments, 6 👍. More precise diagnosis: the setting works in interactive CLI but not in VS Code, SDK, or `--print` mode. Author proposes a one-line fix for each surface, adding pressure for maintainers.

6. **[#65114 — Cowork: give users a manual `/compact`](https://github.com/anthropics/claude-code/issues/65114)** — 5 comments, 1 👍. Cowork's auto-compaction fires at unpredictable times, and users have no manual trigger. Growing support for agent-side compaction awareness (#71803 filed today as well).

7. **[#71910 — Safety block stops legitimate drone firmware analysis](https://github.com/anthropics/claude-code/issues/71910)** — 4 comments, 0 👍. First of eight similar reports filed by `sworrl`. Author describes safety filter falsely classifying USB protocol inspection as "cyber" threat. Sessions halted mid-work, reproducible server-side.

8. **[#43474 — MCP server instructions silently truncated](https://github.com/anthropics/claude-code/issues/43474)** — 3 comments, 2 👍. When multiple MCP servers are configured, the instructions block in the system prompt is truncated mid-sentence without warning. Affects context-rich setups.

9. **[#67220 — Native Windows toast notifications](https://github.com/anthropics/claude-code/issues/67220)** — 3 comments, 0 👍. Feature request for a `windows_toast` notification channel. Windows users are parity-gapped with macOS/Linux which already have native notifications.

10. **[#71803 — Let the agent trigger `/compact` itself](https://github.com/anthropics/claude-code/issues/71803)** — 1 comment, 1 👍. Filed yesterday. Proposes that Claude should be able to request compaction autonomously when it detects context pressure. Complements #65114.

## Key PR Progress

1. **[#71798 — (title: ".")](https://github.com/anthropics/claude-code/pull/71798)** — Closed. Likely a test or accidental PR. No content beyond a period. Not actionable.

2. **[#68787 — fix(scripts): add error message to `edit-issue-labels.sh`](https://github.com/anthropics/claude-code/pull/68787)** — Open. Adds a meaningful error message when label arguments are missing, instead of a silent `exit 1`. Small quality-of-life improvement for CI maintainers and manual runs.

*(Only 2 PRs were active in the last 24 hours. No significant code changes landed.)*

## Feature Request Trends

- **Agent-invokable compaction**: Two separate requests (#65114, #71803) argue for either manual or autonomous context compaction. This signals user frustration with opaque memory management in long sessions.
- **Cross-surface parity** (#71941): Users are noting arbitrary feature gaps between Claude Code, Cowork, and claude.ai. No single request dominates, but the theme recurs across enhancement tags.
- **Self-improving memory** (#71937): A call for Claude to generate its own learning signal between sessions, rather than relying solely on user correction. Indicates advanced users pushing beyond current memory capabilities.
- **Actionable mobile/desktop notifications** (#62458, #67220): Users want to approve/deny permission prompts from their phone and get native Windows toast alerts—important for gateway-heavy workflows.
- **Cybersecurity false-positive mitigation** (#71910–#71920): Eight identical-pattern reports from one user; collectively they ask for a way to override or flag false positives without killing sessions. Domain-specific "authorized work" attestation would help.

## Developer Pain Points

1. **Opus 4.7 thinking summaries remain broken after 10+ weeks.** The most impactful open bug. The root cause is identified (missing `display: "summarized"` in API requests), but neither CLI nor VS Code extension have been patched. This erodes trust for users relying on extended thinking for complex reasoning tasks.

2. **Safety filter false positives block legitimate work.** Sudden mid-session halts for drone-related development are hitting hardware/embedded developers hard. The lack of a "this is authorized work" override forces users to restart sessions and hope the filter doesn't re-fire.

3. **MCP instructions truncated without warning (#43474).** A silent data-loss bug for anyone running multiple MCP servers. Undocumented behavior makes debugging difficult—users only notice when tools behave unexpectedly.

4. **Authentication instability on Windows (#69706, #70002).** Users report intermittent 401 errors and corrupted config files. Not clearly tied to any specific version, which makes root-causing harder. Some must re-authenticate multiple times per day.

5. **No cross-surface parity governance.** Feature requests like native Windows notifications (#67220) and Cowork compaction (#65114) expose a pattern: features land on one surface and never propagate. The lack of a documented roadmap or parity matrix frustrates developers who use multiple Claude surfaces.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**OpenAI Codex Community Digest**
**Date:** 2026-06-28

**1. Today's Highlights**
The community is in an uproar over a suspected rate-limit cost bug in `gpt-5.5` on the Plus plan, with one issue (#28879) exploding to 186 comments and 334 reactions, reporting a 10-20x jump in per-token cost since June 16. On the engineering front, a massive MCP OAuth concurrency and recovery refactor (7 PRs from `stevenlee-oai`) has been superseded and replaced with a cleaner stack, signaling significant internal churn on authentication infrastructure. Meanwhile, the long-running Linux desktop app request (#11023) remains the most popular open feature request, and a new PR (#30395) aims to bring transparency to usage-limit reset expiry details.

**2. Releases**
Three alpha releases were published in the last 24 hours targeting the Rust CLI: `rust-v0.143.0-alpha.27`, `.28`, and `.29`. No changelog details were provided beyond version bumps. This rapid iteration likely addresses the high-severity SQLite logging fix that was recently merged.

**3. Hot Issues**

1.  **#28879 – Rate-limit cost per token jumped ~10-20x** (186 comments, 334 👍)
    - **Why it matters:** A suspected bug on the Plus plan is draining the 5-hour usage budget in 2-3 prompts with `gpt-5.5`. This is the highest-activity issue in the repo, indicating a potentially critical backend pricing or metering regression.
    - [Link](https://github.com/openai/codex/issues/28879)

2.  **#11023 – Codex desktop app for Linux** (130 comments, 650 👍)
    - **Why it matters:** The most upvoted open feature request. Power users on high-end Linux workstations are still locked out of the native app experience due to missing platform support.
    - [Link](https://github.com/openai/codex/issues/11023)

3.  **#28224 – SQLite feedback logs write ~640 TB/year** (93 comments, 399 👍)
    - **Why it matters:** A critical bug rapidly consuming SSD endurance. The reporter notes that three PRs have been merged that cut logs by 85%, but the severity of the original bug (terabytes of writes) caused widespread alarm.
    - [Link](https://github.com/openai/codex/issues/28224)

4.  **#2847 – Feature request: way to exclude sensitive files** (79 comments, 414 👍)
    - **Why it matters:** A cross-variant request for a `.codexignore` mechanism. Developers are concerned about leaking secrets, with significant traction across CLI and IDE users.
    - [Link](https://github.com/openai/codex/issues/2847)

5.  **#30224 – Model not supported with X-OpenAI-Internal-Codex-Responses-Lite** (52 comments)
    - **Why it matters:** A fresh bug in the latest app build where the API rejects valid model requests due to an internal header conflict, blocking users of the Responses-Lite feature.
    - [Link](https://github.com/openai/codex/issues/30224)

6.  **#9203 – Please make "/undo" back** (50 comments, 300 👍)
    - **Why it matters:** A high-demand UX regression. The removal of `/undo` has caused data loss for users whose agents accidentally delete or modify uncommitted files.
    - [Link](https://github.com/openai/codex/issues/9203)

7.  **#29955 – Quota drained instantly: 100 credits gone after 1 message** (29 comments)
    - **Why it matters:** Likely related to #28879. Pro*5 users are reporting that their entire credit balance is consumed in a single message, suggesting a broader metering issue beyond Plus plans.
    - [Link](https://github.com/openai/codex/issues/29955)

8.  **#29072 – Windows sandbox: apply_patch fails to launch** (22 comments)
    - **Why it matters:** A platform-specific blocker on Windows where the sandbox setup executable fails to launch from the package path, rendering the `apply_patch` tool broken for enterprise Windows users.
    - [Link](https://github.com/openai/codex/issues/29072)

9.  **#30390 – ambient_suggestions consumes ~70k tokens in background** (3 comments, filed today)
    - **Why it matters:** A fresh discovery of silent background token consumption. Codex Desktop on Windows is burning credits on ambient suggestions without user interaction, exacerbating the rate-limit crisis.
    - [Link](https://github.com/openai/codex/issues/30390)

10. **#24389 – multi_agent_v1.close_agent can hang for hours** (14 comments)
    - **Why it matters:** A concerning stability issue where closing an unresponsive subagent blocks the parent thread for over 8 hours, impacting users running complex multi-agent workflows.
    - [Link](https://github.com/openai/codex/issues/24389)

**4. Key PR Progress**

1.  **#30395 – Show usage-limit reset expiry details** (jayp-oai)
    - **What:** Exposes reset-credit expiry dates in the rate-limits RPC, enabling clients to show when banked resets expire.
    - **Why it matters:** Directly addresses user frustration (#29618) by bringing transparency to the reset credit system.
    - [Link](https://github.com/openai/codex/pull/30395)

2.  **#30334 – Telemetry: log structured tool and inference timing events** (bolinfest)
    - **What:** Adds structured logs for distinguishing dispatch/queue time from handler time in tool calls.
    - **Why it matters:** Improves operational diagnostics for app-server deployments and will help debug latency issues.
    - [Link](https://github.com/openai/codex/pull/30334)

3.  **#30269 – Disable Nagle on Rendezvous WebSockets** (richardopenai)
    - **What:** Disables Nagle's algorithm for WebSocket connections to exec-server Rendezvous, reducing latency.
    - **Why it matters:** A network-level performance fix to improve responsiveness of remote code execution.
    - [Link](https://github.com/openai/codex/pull/30269)

4.  **#30292–#30296 – MCP OAuth Concurrency & Recovery Stack** (stevenlee-oai, 5 PRs)
    - **What:** A complete rewrite of MCP OAuth handling: serializing shared stores, login/logout, refresh transactions, and drift reporting.
    - **Why it matters:** This supersedes a previous 7-PR stack, indicating a significant architectural shift to fix race conditions and token refresh failures (#27165).
    - [Link](https://github.com/openai/codex/pull/30292)

5.  **#30089 – Test MCP OAuth concurrency and recovery** (stevenlee-oai)
    - **What:** Adds concurrency and recovery tests for the new MCP OAuth stack.
    - **Why it matters:** Essential for validating the correctness of the new serialization strategy.
    - [Link](https://github.com/openai/codex/pull/30089)

6.  **#30327 – stabilize synthesized call output IDs** (bolinfest)
    - **What:** Assigns stable IDs to synthesized "aborted" call outputs to prevent identity churn on retries.
    - **Why it matters:** Fixes a conversation identity stability bug that could cause issues with branching and retries in agent sessions.
    - [Link](https://github.com/openai/codex/pull/30327)

7.  **#30291 – expose environment info RPC** (maxj-oai)
    - **What:** Exposes shell and working directory for named execution environments to clients.
    - **Why it matters:** Enables better tool discovery and configuration for multi-environment setups.
    - [Link](https://github.com/openai/codex/pull/30291)

8.  **#29691 – Enforce marketplace source policy at runtime** (xl-openai)
    - **What:** Blocks installed plugins that violate enterprise source policy and filters marketplace discovery accordingly.
    - **Why it matters:** Critical for enterprise deployments needing to enforce plugin whitelists/blacklists.
    - [Link](https://github.com/openai/codex/pull/29691)

9.  **#30384 – increase currentTime/read timeout** (rka-oai)
    - **What:** Increases the external time service request timeout from 5s to 10s to reduce failures.
    - **Why it matters:** A quick fix for intermittent time-out failures in app-server operations.
    - [Link](https://github.com/openai/codex/pull/30384)

10. **#30294 – Route MCP OAuth recovery through Codex** (stevenlee-oai)
    - **What:** Routes all OAuth recovery flows through Codex's managed credential store instead of raw HTTP redirects.
    - **Why it matters:** Ensures recovery flows are logged, serialized, and consistent with the new auth architecture.
    - [Link](https://github.com/openai/codex/pull/30294)

**5. Feature Request Trends**

- **Ignoring Paths (`.codexignore`):** The most prominent theme (Issues #2847, #24993, #24325) spans all variants (CLI, IDE, Desktop, Web). Developers want a global or repo-local ignore file to prevent sensitive files (e.g., `.env`, `node_modules`) from being sent to the model or manipulated by agents.
- **Undo / Confirm Before Edit:** A strong resurgence of requests (#9203, #24325) for declarative undo and per-edit confirmation prompts, driven by accidental file mutations.
- **Desktop Linux Support:** Persistent demand (#11023) with 650 upvotes—remains the single most-requested feature.
- **Rate-Limit Transparency:** Users want detailed credit expiry, reset schedules, and per-token pricing breakdowns (#29618, #30395 PR).
- **Clickable Thread References:** A niche but growing request (#26200) for rendering subagent and thread IDs as clickable chips in agent output.

**6. Developer Pain Points**

- **Rate-Limit & Billing Shock:** Three high-activity issues (#28879, #29955, #30390) all report a severe regression in credit consumption, draining budgets unnaturally fast. This is the #1 pain point this week.
- **Windows Sandbox Instability:** Multiple bugs (#29072, #24259, #20570) report intermittent sandbox failures, runner errors, and permission issues on Windows, making the CLI less reliable on that platform.
- **MCP OAuth Token Refresh Failures:** Issue #27165 and the massive PR stack indicate that OAuth-backed MCP servers frequently fail to refresh tokens, requiring manual re-authentication.
- **Spellcheck Broken on Windows:** Issue #26478 highlights a surprising UX failure where the spellcheck dialog detects errors but shows no suggestions on Windows, impacting desktop users.
- **Stuck Processes and Memory Leaks:** Reports of `git.exe` polling processes accumulating on Windows (#29408) and agents hanging for hours during subagent cleanup (#24389) suggest underlying resource management issues.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-28

## Today’s Highlights
A security-focused nightly release (v0.51.0-nightly) ships with a critical fix for case-insensitive path blocklist enforcement in VS Code HITL mode. Three new security PRs tackle DNS rebinding SSRF bypasses, path traversal via symlinks, and CI environment variable leaks. Agent reliability remains the dominant theme, with unresolved hangs, silent scope expansion bugs, and subagent recovery false positives drawing heavy community engagement.

## Releases
**v0.51.0-nightly.20260628.gae0a3aa7b** ([changelog](https://github.com/google-gemini/gemini-cli/compare/v0.51.0-nightly.20260626.gb14416447...v0.51.0-ni))
- `fix(security): enforce case-insensitive sensitive path blocklist and vscode hitl` — ensures `.env`, `.git`, and other sensitive paths are blocked regardless of casing across all platforms and VS Code integrations.

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (8 comments, 2 👍)  
   A `codebase_investigator` subagent that hits `MAX_TURNS` reports `status: "success"` and `Termination Reason: "GOAL"`, masking the interruption. This is a dangerous false positive — users believe analysis completed when it did not. Community frustration is high; the issue has been open since March and re-triaged as `need-retesting`.

2. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (7 comments, 8 👍)  
   The most upvoted open bug. The generalist agent hangs indefinitely on simple tasks (e.g., folder creation), forcing users to wait up to an hour or cancel. Workaround: disable subagent delegation entirely. No fix committed despite P1 priority and March creation date.

3. **[#25166 — Shell execution stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)** (4 comments, 3 👍)  
   Simple CLI commands (e.g., `echo hello`) leave the shell in a "Waiting input" state after completion. The agent hangs, believing the shell is still active. This directly undermines basic agent functionality and is a recurring pain point.

4. **[#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** (8 comments, 1 👍)  
   A large enhancement proposal: Gemini 3 models are natively trained as bash users. Rather than restricting them, the issue advocates for OS-level sandboxing that lets the model use native POSIX tools (`grep`, `sed`, `awk`) directly while maintaining security. This could fundamentally change the agent's architecture.

5. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (6 comments)  
   Anecdotal but widely felt: agents ignore custom skills and sub-agents unless explicitly directed, even for highly relevant tasks (e.g., having a `gradle` skill but not using it during Gradle builds). This undermines the sub-agent system's value proposition.

6. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (5 comments)  
   Auto Memory reads local transcripts and sends content to the extraction model before redacting secrets, creating a security exposure. Additionally, the system can log skill configurations with API keys. A structural privacy concern.

7. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (5 comments)  
   Auto Memory only marks a session as processed when the extraction agent successfully reads it. Low-signal sessions that are skipped remain "unprocessed" and get surfaced forever. This accumulates retry debt and wastes model calls.

8. **[#22745 — Assess impact of AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (7 comments, 1 👍)  
   Epic investigating whether AST-aware tools can reduce token waste from misaligned file reads and enable precise method-level navigation. Could dramatically improve large-codebase efficiency.

9. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (3 comments, 1 👍)  
   The model occasionally uses `git reset`, `--force`, or risky DB commands when safer alternatives exist. Community wants the agent to understand destructive operations and prompt for confirmation or suggest safer paths.

10. **[#28155 — Silent scope expansion on task failure](https://github.com/google-gemini/gemini-cli/issues/28155)** (new, linked from PRs #28171/#28172)  
    When reviewing specific code lines fails, the agent silently expands scope—running scripts and reading full files without user approval. Two PRs now address this, indicating the team is actively fixing this trust-damaging behavior.

## Key PR Progress

1. **[#28181 — fix(security): prevent DNS rebinding bypass of SSRF protection](https://github.com/google-gemini/gemini-cli/pull/28181)**  
   The `web_fetch` tool's SSRF protection only inspected hostname strings synchronously, making it trivially bypassable via DNS rebinding. This PR adds proper DNS resolution to `isPrivateIp()` checks.

2. **[#28180 — fix(security): restore defensive path resolution for at-reference files](https://github.com/google-gemini/gemini-cli/pull/28180)** [size/l]  
   Re-applies a fix (from #27943) that was previously reverted. Restores `resolveDefensiveToolPath` and `resolveToRealPath` to `read_file`, `write_file`, and `edit` tools to prevent symlink-based path traversal attacks.

3. **[#28179 — fix(security): remove ISSUE_BODY and ISSUE_TITLE from ALWAYS_ALLOWED env vars](https://github.com/google-gemini/gemini-cli/pull/28179)**  
   `ISSUE_BODY` and `ISSUE_TITLE` bypassed all sanitization—including strict CI mode—allowing unredacted issue content to reach AI prompts. Removes them from `ALWAYS_ALLOWED_ENVIRONMENT_VARIABLES`.

4. **[#28172 / #28171 — fix(agent): prevent silent scope expansion on task failure](https://github.com/google-gemini/gemini-cli/pull/28172)** (fixes #28155)  
   Two PRs (XS and XL size) that add explicit instructions to `mandateConfirm` to prevent the agent from silently expanding scope when it cannot complete a precise review request. Critical for user trust.

5. **[#28178 — fix(security): require approved bot patch artifacts](https://github.com/google-gemini/gemini-cli/pull/28178)**  
   Requires an explicit approval marker before the bot publish job consumes `bot-changes.patch`. Rejected critique runs now remove stale PR artifacts, enforcing a fail-closed reasoning-to-publish boundary.

6. **[#28169 — feat(evals): add eval coverage report command](https://github.com/google-gemini/gemini-cli/pull/28169)** [size/l]  
   Adds `eval:coverage` to cross-reference eval inventory with the tool registry. Helps identify gaps in behavioral test coverage for built-in tools—directly supporting the Component Level Evaluations epic (#24353).

7. **[#28175 — fix(policy): require confirmation for shell parameter expansion](https://github.com/google-gemini/gemini-cli/pull/28175)**  
   Downgrades allowlisted shell commands containing `$` expansion to confirmation in interactive mode; denies entirely in YOLO mode. Addresses a stealthy injection vector.

8. **[#28053 — fix(core-tools): resolve defensive path resolution for at-reference files + macOS tests](https://github.com/google-gemini/gemini-cli/pull/28053)** [size/xl]  
   Comprehensive fix for the production bug where tools fail when the model passes `@`-prefixed paths (e.g., `@policies/new-policies.txt`). Includes macOS test suite improvements.

9. **[#28055 — fix(core): preserve dollar sequences in prompt template substitutions](https://github.com/google-gemini/gemini-cli/pull/28055)**  
   Template substitution in `applySubstitutions()` was corrupting `$$`, `$'`, `$&` sequences inside skill/agent/tool descriptions when they resembled regex patterns. Fix preserves literal dollar strings.

10. **[#28033 — fix(mcp): use longest-prefix matching for server names with underscores](https://github.com/google-gemini/gemini-cli/pull/28033)** (fixes #27981)  
    `parseMcpToolName` was incorrectly splitting tool names at the first underscore, causing routing failures for MCP servers with underscores in their names. Adds `knownServerNames` parameter for longest-prefix matching.

## Feature Request Trends

- **AST-Aware Code Intelligence** (#22745, #22746): Multiple epics propose replacing naive file reads with Abstract Syntax Tree-aware tools for precise method/class navigation, reduced token waste, and better codebase mapping.
- **Agent Self-Awareness & Transparency** (#21432, #22598, #21763): Growing demand for agents to understand their own CLI flags, hotkeys, and trajectories. Users want visible subagent reasoning (via `/chat share`), accurate self-help, and bug reports that include subagent context.
- **Auto Memory Reliability** (#26525, #26522, #26523): The community wants deterministic secret redaction (not post-hoc model-based), graceful handling of low-signal sessions, and quarantine for invalid memory patches instead of silent skipping.
- **Sandboxed Native Bash Execution** (#19873): A paradigm shift—let Gemini 3 use its native POSIX skills under OS-level sandboxing rather than forcing it through constrained tool APIs. Could reduce tool overhead and improve task completion quality.

## Developer Pain Points

- **Agent Hangs & False Completions** (#21409, #25166, #22323): The top frustration. Agents hang indefinitely on simple tasks, report success when they hit turn limits, or get stuck in terminal states. Erodes trust in autonomous operation.
- **Silent Scope Expansion** (#28155, #22672): Agents that silently expand their task scope—reading full files when asked for a few lines, or using destructive `git reset`/`--force` commands without warning. Multiple fixes in flight, suggesting this is a recognized architectural issue.
- **Configuration Ignorance** (#22267, #22093, #20079): Subagents and browser agents ignore `settings.json` overrides, run without permission after updates, and fail to recognize symlinked agent definitions. Users feel their configured constraints are systematically bypassed.
- **Subagent Underutilization** (#21968): The subagent/skill system is architecturally sound but practically ignored by the model unless explicitly prompted. This creates a gap between the feature set and actual behavior.
- **Tool Overload** (#24246): Cli encounters 400 errors when more than ~128 tools are available. The agent lacks a mechanism for scoping available tools to the current task context, forcing users to prune their own tool registries.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-28

**Data source:** [github.com/github/copilot-cli](https://github.com/github/copilot-cli)

---

## 1. Today's Highlights

A wave of regressions hit the Windows platform, including a critical startup failure for stdio MCP servers using `.bat`/`.cmd` commands (v1.0.66) and a persistent clipboard copy bug on Windows 11. The long-running alt-screen controversy continues, with users requesting an opt-out. Meanwhile, a significant session-context feature inspired by Claude Code's `/btw` continues to accumulate support.

---

## 2. Releases

No releases in the last 24 hours.

---

## 3. Hot Issues

| # | Title | Why It Matters | Community Reaction |
|---|-------|----------------|--------------------|
| [#2165](https://github.com/github/copilot-cli/issues/2165) | Ubuntu keychain support is broken | Auth is a blocker for Linux users; documentation is also wrong. | 20 👍 — highest reaction count; high severity for Linux adoption. |
| [#1799](https://github.com/github/copilot-cli/issues/1799) | How to turn off alt-screen views? | Alt-screen mode introduced in a recent release is controversial; power users want a toggle. | 7 👍, 10 comments — active discussion around UX preference. |
| [#3949](https://github.com/github/copilot-cli/issues/3949) | Copy on Windows 11 does not work | Clipboard is a fundamental UX action; tool claims success but fails silently. | 0 👍 but time-critical — filed 2 days ago, reopened quickly. |
| [#3958](https://github.com/github/copilot-cli/issues/3958) | v1.0.66 fails to start stdio MCP servers with `.bat`/`.cmd` (Windows) | Regression blocks all Windows users who rely on MCP server plugins. | Filed yesterday, marked triage — fast-moving critical issue. |
| [#2778](https://github.com/github/copilot-cli/issues/2778) | When is `/btw` from Claude Code coming? | Feature parity request for non-destructive, out-of-band context queries. | Low 👍 count, but represents a major competitive gap. |
| [#3964](https://github.com/github/copilot-cli/issues/3964) | Copying soft-wrapped output drops space at wrap boundary (CLOSED) | Fix for #3666 was incomplete, reopened and reclosed. Inconsistent user experience. | 1 comment — community patience wearing thin on repeated regressions. |
| [#3959](https://github.com/github/copilot-cli/issues/3959) | Ghost characters remain after deleting text | Terminal rendering artifacts degrade usability at the prompt. | Filed yesterday, no comments yet — fresh graphic bug. |
| [#3957](https://github.com/github/copilot-cli/issues/3957) | Cannot scroll history with trackpad on MBP | macOS scrolling hijacked by prompt selection — blocks navigation. | Filed yesterday, zero comments — potential macOS user friction. |
| [#3815](https://github.com/github/copilot-cli/issues/3815) | Debug logs path missing `\` on Windows | Copy-pasting path into Explorer fails; minor but irritating for debugging. | No comments — low urgency but low-effort fix. |
| [#3874](https://github.com/github/copilot-cli/issues/3874) | VS Code agent `preToolUse` hook denial does not work | Security hooks intended to deny commands are ignored — trust boundary issue. | 1 comment — moderate security impact for CI/CD contexts. |

---

## 4. Key PR Progress

| # | Title | Status | Description |
|---|-------|--------|-------------|
| [#3928](https://github.com/github/copilot-cli/pull/3928) | Add .gitignore and settings configuration | **OPEN** | Adds project-level config files; likely aimed at DX improvements. No comments yet. |
| [#570](https://github.com/github/copilot-cli/pull/570) | [WIP] Add macOS installation instructions to README.md | **CLOSED** | Started by Copilot agent in 2025; closed after long inactivity. Illustrates agent-driven contributions. |
| [#3737](https://github.com/github/copilot-cli/pull/3737) | Jigg empire ai | **OPEN** | Unclear description ("Let’s try this new method"); likely experimental or test PR. |

**Note:** Only 3 PRs updated in the last 24 hours, indicating a quiet day for code contributions.

---

## 5. Feature Request Trends

- **Non-destructive context queries:** Request to add a `/btw`-like command (from Claude Code) that allows asking questions without corrupting session context ([#2778](https://github.com/github/copilot-cli/issues/2778)).
- **Session lifecycle visibility:** Users want to see session retention/expiration dates in the status line ([#3963](https://github.com/github/copilot-cli/issues/3963)).
- **Customizable keyboard shortcuts:** Request to remap the `/voice` dictation toggle ([#3672](https://github.com/github/copilot-cli/issues/3672)).
- **Custom model provider quota isolation:** Users want usage of alternative model providers to not consume GitHub AI quota ([#3960](https://github.com/github/copilot-cli/issues/3960)).

---

## 6. Developer Pain Points

- **Windows regressions are the #1 pain point:** Two separate clipboard bugs (copy and soft-wrapped text), MCP server startup failures, and a missing `\` in debug paths — Windows quality is eroding rapidly.
- **Alt-screen mode lacks opt-out:** Users repeatedly request the ability to disable the new full-screen view introduced in a recent release ([#1799](https://github.com/github/copilot-cli/issues/1799)).
- **Ubuntu authentication broken with no working documentation:** Keychain access failure combined with wrong docs creates a frustrating onboarding roadblock for Linux users ([#2165](https://github.com/github/copilot-cli/issues/2165)).
- **Incomplete bug fixes erode trust:** Issue #3666 (copying wrapped text) was "fixed" in v1.0.49, then re-reported on v1.0.59, and now reopened as #3964 on v1.0.65 — the fix was not complete.
- **Terminal rendering issues on macOS:** Ghost characters and broken trackpad scrolling suggest the TUI layer has interactive bugs across platforms.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-28

## Today's Highlights

A busy day for OpenCode with robust activity around WSL path handling, session management UX improvements, and model provider compatibility. Multiple critical PRs landed to fix sandbox project edits, scoped session errors, and foreign directory hints in server mode. The community also logged several new issues around model selection reverting, NIM provider hangs, and memory leaks in long-running server instances.

## Releases

No new releases in the last 24 hours. Current stable: v1.17.11.

## Hot Issues

1. **[Feature: Provide llms.txt and docs as markdown](https://github.com/anomalyco/opencode/issues/8816)** (15 comments, 34 👍) — Long-running request (since Jan) for structured documentation export. High community interest suggests strong demand for LLM-friendly docs ingestion.

2. **[Pay Go with crypto](https://github.com/anomalyco/opencode/issues/23153)** (13 comments, 24 👍) — Feature request for crypto payment support for opencode-go. Strongly upvoted, indicating significant user desire for alternative payment methods in the Go tier.

3. **[Desktop App sends UNC paths to WSL-hosted server](https://github.com/anomalyco/opencode/issues/19473)** (7 comments, workaround available) — Windows/WSL integration pain point. Desktop app stores `\\wsl.localhost\Debian` paths that break tool calls. Related to #30895 and newly filed #34255.

4. **[Bun 1.3.14 segfault on Linux x86_64](https://github.com/anomalyco/opencode/issues/33890)** (6 comments, 5 👍) — SIGILL crash on AMD EPYC Zen4 systems with AVX-512. Critical for production deployments on modern hardware. Affects 1.17.10-1.17.11.

5. **[Server mode memory leak: 26.8 GiB cgroup peak](https://github.com/anomalyco/opencode/issues/33213)** (5 comments) — Long-running `opencode serve` accumulates anonymous JS heap/swap. Peak at 26.8 GiB over ~1.5 days. Major concern for production deployments.

6. **[Project skills unstable/incomplete across sessions](https://github.com/anomalyco/opencode/issues/34228)** (5 comments) — Skills configured via `.opencode/skills` show inconsistently between sessions. Breaks reliability of skill-based workflows.

7. **[Model selection silently reverts after answering](https://github.com/anomalyco/opencode/issues/34207)** (4 comments) — Selecting a different model while agent is working gets overwritten on user response. UX bug that silently wastes credits on wrong model.

8. **[Copilot Enterprise third-party models inaccessible](https://github.com/anomalyco/opencode/issues/34030)** (4 comments) — Enterprise Copilot users cannot use company-added third-party models in OpenCode. Blocks enterprise adoption.

9. **[macOS NFS kernel messages corrupt TUI](https://github.com/anomalyco/opencode/issues/34146)** (3 comments) — NFS status messages from OrbStack leak into TUI display. Niche but disruptive for macOS users with NFS mounts.

10. **[GLM-5.1 prompt cache randomly drops to 0 on opencode-go](https://github.com/anomalyco/opencode/issues/31348)** (4 comments, 2 👍) — Unpredictable cache drops causing cost spikes. Contrasts with stable DeepSeek V4 Flash caching.

## Key PR Progress

1. **[fix(app): resolve sandbox project edits](https://github.com/anomalyco/opencode/pull/34253)** — Merges project metadata lookup by ID, worktree, or sandbox membership. Fixes edit actions in sandbox directories with regression coverage.

2. **[fix(app): scope session page errors](https://github.com/anomalyco/opencode/pull/34254)** — Adds ErrorBoundary inside session page panel to prevent load errors from killing the entire tab shell.

3. **[fix(server): reject foreign directory hints before instance lookup](https://github.com/anomalyco/opencode/pull/34256)** — Closes #34255, addresses the WSL path confusion chain (#30895, #19473). Critical security/correctness fix.

4. **[feat(tools): port MiMo tools and subsystems to opencode](https://github.com/anomalyco/opencode/pull/34270)** — Major addition: multiedit, codesearch, memory (BM25), history (BM25), change_directory. DB-free subsystems for session-scoped CWD.

5. **[fix(sdk): preserve V2Event name for SSE streams](https://github.com/anomalyco/opencode/pull/34171)** — Patches effect@4.0.0-beta.83 for proper SSE event naming. Regenerates JS SDK and OpenAPI spec.

6. **[feat(tui): add session rename](https://github.com/anomalyco/opencode/pull/34264)** — End-to-end session renaming: new durable event, core interface, projector handler, protocol endpoint, server+TUI wiring.

7. **[feat(tui): wire up undo/redo and revert for V2 sessions](https://github.com/anomalyco/opencode/pull/34263)** — Replaces not-implemented stubs with working revert API, including busy guard to prevent race conditions.

8. **[fix(core): guard non-reducing compaction](https://github.com/anomalyco/opencode/pull/34261)** — Closes #27924. Prevents infinite overflow recovery loops when compaction makes no progress.

9. **[fix: preserve attachment file paths](https://github.com/anomalyco/opencode/pull/34234)** — Closes #23801 and #17488. Agents can now access original filesystem paths for pasted/dragged attachments.

10. **[fix(tui): prevent piped stdin from breaking UI](https://github.com/anomalyco/opencode/pull/34242)** — Closes 4 issues (#28538, #24195, #3871, #6220) by handling piped stdin gracefully in TUI.

## Feature Request Trends

- **Documentation/LLM integration** (#8816, #34232): strong demand for structured docs export (`llms.txt`) and IDE extension session management UI to match TUI capabilities.
- **Payment flexibility** (#23153): crypto payment support for opencode-go remains a top community ask.
- **Model provider parity** (#34030, #34177): users want support for enterprise Copilot third-party models and up-to-date NVIDIA NIM model listings.
- **Session UX improvements** (#34232, #34264): better session list/rename/resume across desktop and TUI interfaces.

## Developer Pain Points

- **WSL/Windows path handling** (#19473, #30895, #34255): recurring breakage with UNC paths, server instance confusion. Two new PRs (#34256, #34233) address this but the pattern suggests fundamental fragility.
- **Memory leaks in server mode** (#22422, #28492, #33213): multiple reports of MaxListenersExceededWarning and heap growth in long-running processes. Affects production deployments.
- **Model caching/cost unpredictability** (#12219, #31348): users face unexpected credit exhaustion from prompt cache drops and token limit errors. Comparison with more stable providers (DeepSeek) suggests infrastructure issues.
- **Inconsistent project/skills behavior** (#34228): skills not reliably exposed across sessions undermines skill-based workflows.
- **ARM64 compatibility** (#19130, #34054): crashes on Windows ARM64 (TinyCC ffi) and Linux arm64 (tree-sitter SIGTRAP). Growing pain as ARM adoption increases.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-28

## Today's Highlights

A burst of extension API improvements and polish landed today, with seven PRs merged addressing everything from extension cost reporting to external editor configuration. The biggest tension this week is around TUI behavior: streaming markdown auto-scroll remains a high-traffic open issue, and a new flicker-on-multiple-tool-calls bug (#6131) was just reported. On the provider side, a critical fix to surface HTTP error bodies from gateways (PR #5832) is still open and awaiting review.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#5825 — Streaming markdown forces scroll to bottom](https://github.com/earendil-works/pi/issues/5825)** — Open, 34 comments, massive community engagement. Users with "clear on shrink" enabled cannot read streaming responses because Pi periodically forces a scroll-to-bottom, overriding manual scroll-up. A core UX blocker for heavy readers.

2. **[#5763 — Providers swallow HTTP error body](https://github.com/earendil-works/pi/issues/5763)** — Open, in-progress. Behind a proxy, 403 errors surface as opaque messages like `Unknown: UnknownError` (Bedrock) or `403 status code (no body)` (OpenAI). Makes debugging gateway issues nearly impossible. A fix is in PR #5832.

3. **[#6131 — Full screen redraw flicker on multiple tool calls](https://github.com/earendil-works/pi/issues/6131)** — Just filed. When a model returns several tool calls in one turn, the TUI clears and redraws from the top, worsening as more tool call blocks accumulate. Likely a rendering optimization issue.

4. **[#6130 — renderCall/renderResult silently ignore exceptions](https://github.com/earendil-works/pi/issues/6130)** — Fresh report. If a custom renderer throws (e.g., due to a hallucinated import), Pi silently falls back to the default renderer with no error output. Caused multiple hours of wasted debugging for the reporter.

5. **[#6129 — Package report: @hypabolic/pi-hypa](https://github.com/earendil-works/pi/issues/6129)** — Malicious behavior report. Community member flags a package that appears to be gaming install counts for self-promotion. Though no malware is confirmed, the manipulation is concerning for the extension ecosystem.

6. **[#6128 — Support diffusiongemma thinking and tool calls](https://github.com/earendil-works/pi/issues/6128)** — Diffusiongemma's thinking blocks render as normal output instead of being visually separated. Critical for users exploring diffusion-based models via Unsloth.

7. **[#6124 — Devnagri characters break the harness UI](https://github.com/earendil-works/pi/issues/6124)** — Typing non-Latin scripts (e.g., नेटवर्क) causes layout corruption in the TUI. An accessibility and internationalization issue affecting a significant user base.

8. **[#6116 — opencode-go streaming ignores "thinking: disabled" for mimo models](https://github.com/earendil-works/pi/issues/6116)** — Even when users set thinking to "off", mimo models still perform reasoning in streaming mode. Confirmed as an upstream opencode-go gateway bug, but Pi users are affected today.

9. **[#6113 — High session usage on GLM Coding Plan](https://github.com/earendil-works/pi/issues/6113)** — Community Reddit thread cross-referenced. Users on Z.ai Lite coding plan noticed non-uniform session token consumption. A potential billing or tracking issue for Pi's GLM integration.

10. **[#6110 — Extension session_start fires before initTheme](https://github.com/earendil-works/pi/issues/6110)** — Pi-web specific: extensions that access `theme` during `session_start` crash because the theme system isn't ready yet. A timing/ordering bug in the web client initialization.

## Key PR Progress

1. **[#5735 — Defer extension reload requests safely](https://github.com/earendil-works/pi/pull/5735)** — Open. Makes `ctx.reload()` available from any extension context (not just slash commands), with a deferral mechanism that runs reloads only at safe boundaries. A significant extension API improvement.

2. **[#5678 — Add excludeFromContext for custom messages](https://github.com/earendil-works/pi/pull/5678)** — Open. Allows custom messages to be persisted and rendered but excluded from model context. Extends to compaction and branch summarization. Useful for metadata or debug messages the model shouldn't see.

3. **[#6123 — Add externalEditor setting for Ctrl+G](https://github.com/earendil-works/pi/pull/6123)** — Merged. Solves the long-standing problem where `$EDITOR`/`$VISUAL` env vars are locked on Windows. Now configurable in `settings.json`. Small but high-impact fix for Windows users.

4. **[#6119 — Add reportUsage API for extensions](https://github.com/earendil-works/pi/pull/6119)** — Merged. Extensions (like subagent) can now feed token/cost usage back into the main session footer and `/session` totals. Previously costs only appeared in expandable tool result cards.

5. **[#5832 — Surface provider HTTP error body](https://github.com/earendil-works/pi/pull/5832)** — Open, fixes #5763. The most critical open PR today. Wires through the original HTTP error body so providers like Bedrock and OpenAI-shaped APIs show meaningful error messages instead of opaque SDK fallbacks.

6. **[#6115 — Add configurable chat padding](https://github.com/earendil-works/pi/pull/6115)** — Open, to-discuss. Frequently requested on Discord. The author is not convinced a TUI-level padding flag is the right approach, opening the discussion for alternatives.

7. **[#6099 — Rename model key from gpt-5.2-chat-latest to gpt-5.2-chat](https://github.com/earendil-works/pi/pull/6099)** — Merged. Corrects Azure OpenAI model definitions. The `-chat-latest` variant doesn't exist; the correct key is `gpt-5.2-chat`.

8. **[#6111 — Report settings write failures in install/remove](https://github.com/earendil-works/pi/pull/6111)** — Merged. Fixes a silent failure: `pi install` could exit 0 even when `settings.json` is read-only, leaving the extension installed on disk but unregistered. Now reports an error.

9. **[#6109 — Preserve dependency cache on extension reload](https://github.com/earendil-works/pi/pull/6109)** — Merged. Fixes release binary reloads that re-evaluated dependency side effects (e.g., registering themes multiple times). Now caches and reuses dependency modules.

10. **[#6125 / #6126 — Allow extra package manager args for extension install/update](https://github.com/earendil-works/pi/issues/6125)** — Merged via two related PRs. Adds `npmInstallArgs` and `npmUpdateArgs` settings so users can pass flags like `--min-release-age` to the package manager.

## Feature Request Trends

- **Extension API expansion** is the dominant theme: extensions want to report usage/costs (#6120, #6119), execute registered tools (#6121), reload from any context (#5735), and pass audio through RPC (#6118). The extension system is becoming a platform, and users are hitting its current limits.
- **Configurable TUI** continues as a strong undercurrent: padding removal (#6115), external editor override (#6122), and queuing `/reload` during streaming (#6107) all reflect demand for more user control over the terminal interface.
- **Internationalization** is emerging as a concern: Devnagri breaking the UI (#6124) and non-Latin character handling more broadly need attention as Pi's global user base grows.
- **Provider model accuracy** remains a steady source of requests: correctly naming Azure OpenAI models (#6114), supporting new architectures like diffusiongemma (#6128), and fixing upstream provider bugs (#6116).

## Developer Pain Points

1. **Silent failures waste developer time** — The top pain point this week. Issues #6130 (silent renderer fallback), #6111 (silent install failure), and #6110 (silent crash on session_start) all lead to hours of debugging before the real cause is found. The community is loudly asking for Pi to surface errors instead of swallowing them.

2. **TUI rendering glitches under load** — Multi-tool-call flicker (#6131) and streaming scroll-jacking (#5825) are the most upvoted issues. These directly impact daily workflow, making Pi hard to use for complex, multi-step interactions.

3. **Debugging non-standard providers is opaque** — HTTP error body swallowing (#5763), upstream gateway bugs (#6116), and incorrect model definitions (#6114) all force developers to debug at the network/proxy level rather than getting clear messages from Pi.

4. **Reload/re-evaluation side effects** — Extension dependencies re-evaluating on reload (#6108) causes theme registration duplication and other unpredictable behavior. The fix (#6109) addresses the symptom, but the underlying caching model needs hardening.

5. **Cross-platform environment inconsistencies** — Windows env var locking (#6122) and settings file permission handling (#6112) continue to frustrate developers moving between platforms. These are small fixes that have outsized impact on user trust.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-28

## Today's Highlights
The v0.19.2-nightly release cycle brought targeted fixes for WebSocket session parent-tracking and MCP UI rendering, while a major break-fix PR (#5934) landed to resolve a costly unbounded retry loop caused by an overly aggressive 8K default output cap. Community attention is concentrated on three themes: making scheduled `/loop` tasks visible and editable, enabling cross-device (Git-tracked) persistence for todos and memories, and tightening privacy/security around unintended model or provider upgrades.

## Releases
- **[v0.19.2-nightly.20260628.714513df2](https://github.com/QwenLM/qwen-code/releases/v0.19.2-nightly.20260628.714513df2)** — Bug fix and release iteration: `fix(core): allow web_fetch JSON fallback` by @tt-a1i. No user-facing features in this nightly.

## Hot Issues
1. **#5838** — **Allow user to adjust agent initiated cmd timeout** – A frequently-requested ergonomics improvement: processes spawned by the agent can block indefinitely. Adding a configurable threshold would prevent runaway subprocesses without killing legitimate long-running builds. *6 comments, strongly favored by the community.*

2. **#5875** — **Improve skill command name auto-complete matching** – Currently `/skill_name` only matches from the start of the name. Users want substring matching so `/store` finds `front-end-store-rules`. Simple UX win, welcomed in comments.

3. **#5819** — **Auto-upgrade switches to a more expensive model** – A serious user-reported regression: v0.19 auto-updated `settings.json` from DeepSeek-4 Flash → DeepSeek-4 Pro without notice, draining credits. Raised alarm about silent model changes on self-update. *Active triage, user blocked their API key in response.*

4. **#5836** — **Persist todos inside the project for cross-device sync** – The `create todos` tool only writes to `~/.qwen/todos/`. Users want a prompt to save into `.qwen/todos` so task state travels with the Git repo. Also requested for plans and memories. *High demand, 4 comments.*

5. **#5823** — **`/loop cron tasks fire silently with no visibility`** – A cron scheduled during testing continued to fire days later across new chat sessions, automatically starting work unseen. The model can neither list nor stop its own scheduled tasks. *4 comments, all agree the current design is too opaque.*

6. **#5756** – **Default 8K output cap truncates large writes, causing retry loops** – Root cause of a painful failure mode: `write_file` output > 8K gets truncated, the scheduler rejects it, and the model retries the same oversized call repeatedly. *Drives PR #5934 below. 3 comments confirming the bug.*

7. **#5942** — **Anthropic provider: avoidable prompt-cache misses inflate cost** – Qwen Code’s Anthropic integration scores ~0% cache hit rate while Claude Code on the same backend scores ~100%. Two independent prefix mismatches cause every turn to miss cache. *Cost-essential bug, a few users reported 2–3× token spend.*

8. **#5920** — **`/rewind` records have `parentUuid: null`** – Session resumption loses all turns except the last because `parentUuid` is stored as null. Full history exists on disk but is logically disconnected. *3 comments, marked for immediate fix.*

9. **#5626** — **Revive Chrome Extension via Daemon + WebUI Architecture** – A well-received proposal to bring back the Chrome extension (scrapped from PR #1432) by reusing the daemon’s WebUI. Users miss browser-tool integration (27 tools originally). *3 comments, maintainers showing interest.*

10. **#5897** – **Repeating `unknown format "uint64" ignored in schema` messages** – Startup now spams ~30 irrelevant schema warnings from an MCP server’s `lastModifiedTime` property. Bad user first impression. *Closed with a quick one-line fix, but indicates schema validation gaps.*

## Key PR Progress
1. **[#5934](https://github.com/QwenLM/qwen-code/pull/5934)** – **Fix repeated truncated write_file/edit retries from looping** – *Closed.* The most impactful fix this digest: changes default `max_tokens` from 8K → model’s real output limit, and tightens retry detection. Two-layer fix eliminates the #5756 retry loop.

2. **[#5946](https://github.com/QwenLM/qwen-code/pull/5946)** – **Isolate Anthropic SDK abort listener leak** – *Open, new.* Each request was leaking abort listeners. This wraps per-request child controllers to prevent stale listeners from accumulating—important for long-lived daemon sessions.

3. **[#5890](https://github.com/QwenLM/qwen-code/pull/5890)** – **Inject `.qwen/loop.md` task file at fire time** – *Open.* Addresses #5889: `/loop` can now carry a durable, user-editable task list. Model opts in via a sentinel prompt. A key step toward background automation transparency.

4. **[#5848](https://github.com/QwenLM/qwen-code/pull/5848)** – **`ui.history.collapsePreviewCount` setting** – *Open.* When resuming collapsed sessions, shows the last N user turns while hiding older history. Solves the “where was I?” problem without overwhelming the UI.

5. **[#5888](https://github.com/QwenLM/qwen-code/pull/5888)** – **RFC: Multiplayer channel-resident agent (qwen tag)** – *Open.* Phase 0 of a group-chat agent for DingTalk, built on existing channel adapters and the daemon. Opens a new deployment model for team-based code review agents.

6. **[#5943](https://github.com/QwenLM/qwen-code/pull/5943)** – **Error boundaries for web-shell** – *Closed.* Three-layer React error boundaries: generic, per-message, and per-code-block. A single render crash no longer white-screens the entire web shell.

7. **[#5927](https://github.com/QwenLM/qwen-code/pull/5927)** – **Improve cron tool search intents** – *Closed.* Makes `tool_search` surface `cron_delete` for “how do I stop this cron?” queries. Directly addresses the #5823 visibility concern.

8. **[#5912](https://github.com/QwenLM/qwen-code/pull/5912)** – **Fix ACP permission votes across connections** – *Open.* Permission request IDs are now connection-qualified so a user voting on one WebSocket can resolve a prompt that came in on another. Critical for multi-client daemon setups.

9. **[#5928](https://github.com/QwenLM/qwen-code/pull/5928)** – **`todosDirectory` setting for project-local persistence** – *Open.* Mirrors the request in #5836: adds a configurable path so todos can live inside the project repo and be Git-committed.

10. **[#5795](https://github.com/QwenLM/qwen-code/pull/5795)** – **Enrich subagent crash notifications** – *Open.* When a subagent crashes, the parent now receives partial results and recent activity logs instead of a bare “task failed.” Improves debugging in multi-agent workflows.

## Feature Request Trends
- **Background automation transparency** – Multiple issues (#5823, #5889, #5890) demand that `/loop` and `/cron` tasks be listable, stoppable, and surfaced in a visible task file rather than firing silently in the background.
- **Project-local persistence** – Users want todos, plans, and memories to be optionally stored inside `.qwen/` or a configurable directory so they can be committed to Git and synced across devices and team members (#5836, #5867, #5928).
- **Multi-channel & multiplayer agents** – Two PRs (#5888, #5907) expand Qwen Code beyond the CLI/IDE: a DingTalk-resident “qwen tag” and full Telegram command parity. The Chrome extension revival proposal (#5626) adds browser integration to this trend.
- **Model & provider controls** – Users want explicit guardrails against silent model upgrades (#5819) and a `/model --vision` fallback for text-only models (#5597), plus configurable timeout for spawned agents (#5838).

## Developer Pain Points
- **Opaque background processes** – Scheduled tasks that fire invisibly (#5823) and agents that leak subprocesses or CPU after idle (#5922) erode trust in the tool. Developers want visibility into what the agent is doing and did.
- **Unbounded retry loops** – The 8K default output cap (#5756) and the edit-tool result duplication (#5894) cause the agent to get stuck in expensive retry cycles. The #5934 fix addresses the former; the latter still needs a solution.
- **Cross-session state loss** – `/rewind` with `parentUuid: null` (#5920) and scroll-position resets during model output (#5941) break session continuity. Users can’t reliably resume long conversations.
- **Silent model/credential changes** – Upgrading the tool itself switches models (#5819) without user notification. Combined with invisible cron tasks, this creates a trust deficit.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-28

**Project:** Hmbown/CodeWhale (DeepSeek TUI)  
**Ref:** github.com/Hmbown/DeepSeek-TUI

---

## 1. Today’s Highlights

The CodeWhale team has pushed a major wave of PRs today focused on **three strategic fronts**: (a) a new **plugin system** with manifest parsing, discovery, and injection; (b) **ACP (Agent Client Protocol) compliance** for Zed compatibility and streaming deltas; and (c) **token/cache discipline** fixes including cache-maximal context mode and fallback hints for tool errors. Community attention remains fixed on the gap in **input cache hit rates** versus DeepSeek-Reasonix, with multiple long-running bugs still open. The v0.8.66 release ledger was also finalized, closing the milestone with a token/cache scorecard.

---

## 2. Releases

**No new releases in the last 24 hours.**  
The v0.8.66 release ledger was documented in PR #3707, but no new tag was cut.

---

## 3. Hot Issues (Top 10 by Comment Count)

### #1177 — [BUG] Input cache hit rate too low
- **Author:** trytsomile · 24 comments · [Link](https://github.com/Hmbown/CodeWhale/issues/1177)
- **Why it matters:** The top community grievance: DeepSeek-Reasonix achieves 95%+ cache hit rate; CodeWhale lags far behind. This directly impacts user cost and latency.
- **Community reaction:** Zero 👍 indicates frustration has shifted from voting to raw complaint volume.

### #1120 — [BUG] Cache hit problems persist
- **Author:** pmsleepcheck · 21 comments · [Link](https://github.com/Hmbown/CodeWhale/issues/1120)
- **Why it matters:** Follow-up to #1177; user reports that even after v0.8.17, input_cache_miss remains broken for repeated project modifications.
- **Community reaction:** Bilingual discussion (ZH/EN) — maintainers still investigating root cause.

### #743 — [BUG] Token consumption exploded
- **Author:** YaYII · 13 comments · [Link](https://github.com/Hmbown/CodeWhale/issues/743)
- **Why it matters:** 400M tokens consumed in half a day. User suspects excessive request density and conversational loop duplication.
- **Community reaction:** High-cost alarm — directly ties to the cache-maximalism effort.

### #3192 — [ENHANCEMENT] ACP Registry listing for Zed support
- **Author:** Jengro777 · 12 comments · [Link](https://github.com/Hmbown/CodeWhale/issues/3192)
- **Why it matters:** Being listed on agentclientprotocol/registry unlocks easy installation from the Zed editor — a key adoption channel.
- **Community reaction:** Positive; the team is actively working on ACP streams (PR #3702, #3698).

### #3275 — [BUG] CodeWhale over-modifies and self-answers
- **Author:** yekern · 12 comments · [Link](https://github.com/Hmbown/CodeWhale/issues/3275)
- **Why it matters:** Regression from #3061; the agent enters a self-driven loop of proposing, answering, and executing without user confirmation.
- **Community reaction:** Triggered by the "always execute" mode — users want more granular control.

### #3205 — [BUG/ENHANCEMENT] Fleet loadout auto and model classes
- **Author:** Hmbown · 10 comments · [Link](https://github.com/Hmbown/CodeWhale/issues/3205)
- **Why it matters:** Core design issue for Fleet mode — needs a unified loadout selector for TUI, CLI, exec, subagents, and workers.
- **Community reaction:** Maintainer-led; part of the larger orchestration refactor.

### #2870 — [DOCUMENTATION] Staged command-boundary refactor (EPIC)
- **Author:** aboimpinto · 9 comments · [Link](https://github.com/Hmbown/CodeWhale/issues/2870)
- **Why it matters:** Tracks PR #2851 and sub-layers; cleaning up how commands are parsed and dispatched — impacts all CLI/TUI users.
- **Community reaction:** Low visibility but structurally important.

### #3568 — [BUG] Plan and agent mode mixed up again
- **Author:** DracheTek · 6 comments · [+1 👍](https://github.com/Hmbown/CodeWhale/issues/3568)
- **Why it matters:** The model ignores plan/agent mode flags and uses agent behaviors in plan mode, including unauthorized file modifications.
- **Community reaction:** Recurring issue — suggests the mode-switching signal is weak or ignored by the model.

### #1747 — [ENHANCEMENT] Cache hit problem (TUI readability)
- **Author:** Amund · 4 comments · [+3 👍](https://github.com/Hmbown/CodeWhale/issues/1747)
- **Why it matters:** Experienced opencode/deepseek user finds the TUI hard to read despite functional correctness.
- **Community reaction:** 3 👍 suggests moderate agreement on UX need.

### #3495 — [ENHANCEMENT] Adopt Moraine as memory backend
- **Author:** Hmbown · 4 comments · [Link](https://github.com/Hmbown/CodeWhale/issues/3495)
- **Why it matters:** Proposes integrating Moraine (Apache-2.0) for lossless session persistence and MCP-based recall — a significant architecture shift.
- **Community reaction:** Early-stage design discussion.

---

## 4. Key PR Progress (Top 10 by Impact)

### #3708 — [OPEN] feat(plugins): manifest parsing, discovery, and registry
- **Author:** pkeging · [Link](https://github.com/Hmbown/CodeWhale/pull/3708)
- **Description:** Core plugin infrastructure: `PluginManifest` from `plugin.toml`, enable/disable/list, built-in + user plugin discovery with `[when]` conditions (OS, binaries). Includes built-in `rust-toolkit` plugin.
- **Impact:** Foundation for extensibility — enables community-contributed plugins.

### #3702 — [CLOSED] feat(acp): stream session/prompt deltas
- **Author:** findshan · [Link](https://github.com/Hmbown/CodeWhale/pull/3702)
- **Description:** Makes ACP adapter stream incrementally instead of buffering full turns. Directly improves Zed editor integration.
- **Impact:** Key for #3192 — editors like Zed now see real-time agent output.

### #3698 — [CLOSED] feat(acp): cancel in-flight session/prompt on session/cancel
- **Author:** findshan · [Link](https://github.com/Hmbown/CodeWhale/pull/3698)
- **Description:** Enables reading `session/cancel` before the provider call completes — previously impossible due to serial read loop.
- **Impact:** Non-blocking cancellation for Zed/ACP clients.

### #3697 — [CLOSED] feat(working-set): cache-maximal context mode
- **Author:** findshan · [Link](https://github.com/Hmbown/CodeWhale/pull/3697)
- **Description:** Implements #528: opt-in mode that injects full active-file contents instead of just file paths, avoiding tool calls for re-reading.
- **Impact:** Directly addresses the cache-hit and token-consumption crises (#1177, #743).

### #3705 — [CLOSED] fix(engine): suggest direct URLs after repeated search errors
- **Author:** cyq1017 · [Link](https://github.com/Hmbown/CodeWhale/pull/3705)
- **Description:** When web search fails repeatedly, the engine collects domains from failed queries and suggests `fetch_url` as a fallback.
- **Impact:** Improves agent resilience — refs #1641.

### #3703 — [CLOSED] fix(engine): nudge fallback after repeated tool errors
- **Author:** cyq1017 · [Link](https://github.com/Hmbown/CodeWhale/pull/3703)
- **Description:** Adds runtime hints after repeated tool error steps, including failed tool names, suggested alternatives.
- **Impact:** Prevents the model from looping on broken tool calls.

### #3696 — [CLOSED] feat(prompts): override base prompt from config dir
- **Author:** findshan · [Link](https://github.com/Hmbown/CodeWhale/pull/3696)
- **Description:** Closes #3638 — lets users swap the base/constitutional prompt from a config-directory file for non-software use cases (writing, document review).
- **Impact:** Major UX flexibility for non-developer audiences.

### #3706 — [CLOSED] Layer 4.2: Registry cleanup, docs, and validation (FEAT-008)
- **Author:** aboimpinto · [Link](https://github.com/Hmbown/CodeWhale/pull/3706)
- **Description:** Completes the command-boundary refactor (ref #2870): registry cleanup, source-verified architecture docs, final validation.
- **Impact:** Finishes a multi-layer architectural cleanup.

### #3707 — [CLOSED] docs: add v0.8.66 release ledger
- **Author:** Hmbown · [Link](https://github.com/Hmbown/CodeWhale/pull/3707)
- **Description:** Records release candidate state, ACP registry submission, issue triage, and gated items. Updates changelog with token/cache scorecard and shell-only benchmark hardening.
- **Impact:** Provides transparency on release readiness.

### #3700 — [CLOSED] fix(verifier): emit hunt verdict mapping
- **Author:** cyq1017 · [Link](https://github.com/Hmbown/CodeWhale/pull/3700)
- **Description:** Maps verifier results (pass/partial/fail) to hunt verdicts (hunted/wounded/escaped) with structured fields.
- **Impact:** Closes #2093 — formalizes verifier output for trophy/audit use.

---

## 5. Feature Request Trends

**Top 5 requested directions across all issues (last 24h):**

1. **Cache-hit optimization (urgency: critical)**
   - 8+ issues directly reference low input cache hit rates vs DeepSeek-Reasonix (95%+).
   - Users demand parity; cost pressure is high.

2. **Plugin/extension system (urgency: high)**
   - PR #3708/#3699/#3692 land today; community has long requested modular MCP, skills, and slash commands.
   - Hotbar MVP (Fleet data, config, key dispatch) is also a priority (#3389).

3. **ACP Protocol compliance for Zed integration (urgency: high)**
   - Being listed on agentclientprotocol/registry (#3192) is a clear adoption goal.
   - Streaming and cancellation are now delivered; remaining: full ACP spec conformance.

4. **Agent mode/behavior discipline (urgency: moderate)**
   - Multiple reports of plan/agent mode mixing (#3568) and self-questioning loops (#3275).
   - Users want reliable mode switching and execution boundaries.

5. **Token/context discipline (urgency: moderate)**
   - 400M token burn in half a day (#743), excessive prompt footprint (#2953), and repeated transcript input (#2956).
   - The cache-maximal PR (#3697) is the first systematic fix.

---

## 6. Developer Pain Points

**Recurring frustrations and high-frequency requests:**

- **Input cache misses** dominate the issue tracker. Users comparing with DeepSeek-Reasonix feel CodeWhale wastes 2–3× tokens for the same task.
- **Unpredictable token consumption** — one user burned 400M tokens in a single half-day session with no explanation.
- **Plan/agent mode confusion** — the model consistently ignores mode flags, executing agent behaviors during planning sessions (file modifications, tool calls).
- **Self-driven execution loops** — the agent proposes, answers, and acts without user confirmation, particularly after recent workflow changes.
- **Slow report/document operations** — combining analysis reports into local documents triggers abysmal cache hits and minute-long waits.
- **Tool error resilience** — when web searches or APIs fail, the agent retries the same failing call indefinitely instead of falling back gracefully.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*