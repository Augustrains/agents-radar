# AI CLI Tools Community Digest 2026-07-08

> Generated: 2026-07-08 01:21 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem Cross-Comparison Report — 2026-07-08

## 1. Ecosystem Overview

The AI CLI tools landscape continues to mature rapidly, with five major entrants (Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Qwen Code) and several smaller contenders (OpenCode, Pi, Kimi Code, CodeWhale) showing varying degrees of community traction and development velocity. The ecosystem remains dominated by Claude Code and OpenAI Codex in terms of community size and issue volume, while Google's Gemini CLI and GitHub's Copilot CLI demonstrate strong institutional backing. A clear divide is emerging between established tools with mature feature sets facing scaling and reliability challenges, and newer entrants (OpenCode, Pi, CodeWhale) racing toward feature parity while prioritizing architectural clean-slate redesigns. Across all tools, billing transparency, agent reliability, and cross-platform stability remain the top three systemic pain points.

## 2. Activity Comparison (2026-07-08)

| Tool | Active Issues (Top 10) | Key PRs Today | Release Status | Notable |
|---|---|---|---|---|
| **Claude Code** | 8 open, 2 closed | 3 PRs | v2.1.203–204 (patch) | Highest community engagement; billing opacity dominates |
| **OpenAI Codex** | 9 open, 1 new | 12 PRs (telemetry series) | v0.143.0-alpha.38/39 | Most active engineering; GPT-5.5 token clustering is top concern |
| **Gemini CLI** | 10 open | 7 PRs (3 merged, 4 open) | v0.51.0-nightly | Caretaker automation infrastructure making rapid progress |
| **GitHub Copilot CLI** | 10 open | 0 PRs | v1.0.69 / v1.0.69-3 | Sandbox policy evolution; Issue #53 remains unresolved (10 months) |
| **Qwen Code** | 7 open, 3 closed | 10 PRs (1 merged) | v0.19.7 (stable) + nightly | Daemon architecture focus; enterprise channel expansion |
| **OpenCode** | 7 open, 3 closed | 10 PRs (1 merged) | v1.17.15 | V2 migration momentum; macOS rendering issues recurring |
| **Pi** | 8 open, 2 closed | 10 PRs (all merged) | No new release | Surge of triage closures; extension ecosystem maturation |
| **Kimi Code** | 10 open | 0 PRs | No release | Stable but low activity; Figma MCP is sole new signal |
| **CodeWhale** | 6 open, 4 closed | 10 PRs (8 closed) | v0.8.67 (rebranding) | Rapid iteration; Windows stability crisis; organized lane-based development |

## 3. Shared Feature Directions

### Agent Reliability & Observability (All major tools)
- **Sub-agent lifecycle bugs** are universal: Claude Code (#75043), Gemini CLI (#22323), CodeWhale (#4094), and Copilot CLI (#2729) all report parent-child agent ownership, false completion signals, and stuck states.
- **Live agent monitoring** requested across Claude Code (session analytics), CodeWhale (sub-agent detail panels), and Gemini CLI (subagent trajectory visibility).

### Multi-Model & Provider Flexibility (6 of 8 tools)
- **Claude Code**, **Codex**, **Gemini CLI**, **Copilot CLI**, **Kimi Code**, and **CodeWhale** all have requests for bringing your own model, local inference (Ollama), or easier provider routing. Only OpenAI and Anthropic's proprietary models remain walled garden.

### Billing & Usage Transparency (Claude Code, Codex, Qwen Code)
- Claude Code's #41506 (3–5x token spikes) is the highest-traffic issue across all tools this period.
- Qwen Code's #6264 (review skill token surprises) and Codex's #30364 (reasoning token clustering) show pricing surprises are cross-cutting.

### Session & Context Durability (5 of 8 tools)
- Session resume costs (Claude Code #38029), context compaction rule loss (Codex #25792), `/rewind` broken after compression (Qwen Code #6318), and session recovery after crash (OpenCode #35646) all point to a shared challenge: persistent sessions that work reliably across restarts and compaction.

### Terminal/Editor Integration Regressions (5 of 8 tools)
- VS Code text selection broken (Claude Code #61021), iTerm2 corruption (#68461), code-server freezes (Codex #28726), Copilot CLI TUI hangs on NFS (#4053), Pi macOS rendering bugs, CodeWhale Windows input deadlocks (#1835)—every tool is fighting platform-specific TUI quirks.

### Cross-Platform Windows Support (4 of 8 tools)
- Copilot CLI hooks fail on Windows (#4001), Qwen Code shell tool broken on cmd.exe (#6298), CodeWhale has 4 Windows freeze/deadlock issues, and Pi's read-only FS lock failure (#6406)—Windows is the weakest platform across the board.

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Qwen Code | OpenCode | Pi | CodeWhale |
|---|---|---|---|---|---|---|---|---|
| **Core Philosophy** | Subscription revenue + ecosystem lock-in | Model-first (GPT-5.5) | Enterprise integrations | GitHub ecosystem integration | Daemon-centric multi-service | V2 clean-slate migration | Minimal, extensible TUI | Agent-driven development |
| **Target User** | Professional devs, CI/CD teams | AI researchers, Claude-parity seekers | Enterprise, Google Workspace | GitHub users, plugin devs | Team/enterprise China market | Early-adopter devs | Emacs/vim power users | Rust enthusiasts, multi-provider users |
| **Key Technical Approach** | Hook-based automation | Telemetry-optimized pipelines | Caretaker agent infra | Sandbox policy layers | Daemon + channel architecture | Generated Promise client | Extension SDK APIs | Lane-based agent workflows |
| **Primary Differentiator** | Largest community; richest hook/prompt surface | Fastest engineering iteration (12 PRs/day) | Automated issue triage (Caretaker) | Sandbox bypass & plugin MCP | Enterprise messaging channels (WeCom, DingTalk) | Dual V1/V2 migration; typesafe client | 15+ PRs/day; extension API maturity | Rebranding + structured execution board |
| **Weakest Signal** | Billing opacity eroding trust | Reasoning token artifacts | Agent hangs & false success | Issue #53 (10-month communication gap) | Memory isolation failures | macOS rendering; V2 plugin gaps | Extension discovery docs | Windows stability crisis |

## 5. Community Momentum & Maturity

### Established Leaders (High Maturity, High Activity)
- **Claude Code** – Largest community, highest issue volume, but billing trust erosion is a systemic risk. Two patch releases today suggest reactive maintenance mode rather than feature velocity.
- **OpenAI Codex** – Most engineering activity (12+ PRs today), but top issue (#30364) is a model-level artifact beyond CLI control, signaling dependency on OpenAI's model team. Fast iteration, high community expectations.

### Rapid Iteration (Medium Maturity, High Activity)
- **Pi** – Surprising velocity with 10 merged PRs and 18+ issue closures. The extension SDK layer is maturing quickly, suggesting a focus on ecosystem over core feature expansion.
- **CodeWhale** – Rebranding signals identity solidification. 10 PRs, structured release lanes, and dogfooding culture. But Windows stability crisis could cap growth if unresolved.
- **OpenCode** – V2 migration is the dominant topic. Substantial refactoring (schema, client, durable instructions) indicates architectural ambition, but V2 plugin gaps and macOS rendering issues are growing pain points.

### Institutionally Backed (Medium Maturity, Moderate Activity)
- **Gemini CLI** – Caretaker automation infrastructure is impressive (merged Octokit + triage orchestrator), but agent reliability bugs (false success, hangs) remain unresolved. Lower issue volume but higher engineering quality per PR.
- **Copilot CLI** – Sandbox policy evolution shows product thinking, but Issue #53 (10 months, 75 reactions, no response) is a reputational liability. Zero PRs today suggests a lull.

### Quietest (Low Activity, Stable)
- **Kimi Code** – Only 1 issue of note (#1604 Figma MCP). Project appears stable but not actively attracting new users or features.
- **Qwen Code** – Active but focused on daemon architecture and China-market channels. Token consumption and memory isolation are growing concerns.

## 6. Trend Signals

### Industry Patterns Worth Watching

1. **The "Claude Code Tax" is a systemic pricing crisis.** Three of four top Claude Code issues are billing-related. If Anthropic doesn't address this within 1–2 sprints, expect user migration to Codex or self-hosted alternatives.

2. **Agent nested orchestration is the next reliability frontier.** Every tool reports sub-agent failures: false completions, hung parents, lost results. Multi-agent workflows are where the hype meets reality, and the community is finding the limits.

3. **V2 clean-slate migrations are risky but necessary.** OpenCode's V2 migration is a canary: it's causing V2 plugin gaps, session durability bugs, and feature parity delays. Developers should expect 2–3 months of instability when adopting major framework rewrites.

4. **Windows is an afterthought across the entire ecosystem.** Every tool that targets cross-platform has Windows-specific bugs. Teams needing Windows-first reliability should budget for 20–30% extra debugging time.

5. **Institutional tools (Gemini CLI, Copilot CLI) invest in automation infrastructure.** Caretaker triage, sandbox policies, and MCP auth refresh suggest they're preparing for headless/CI-scale deployment, not just interactive use.

6. **Extension ecosystems are diverging.** Pi's 10-merged-PR day for extension API, Copilot CLI's plugin MCP, and Claude Code's hook system represent three different approaches to extensibility. The lack of a standard means plugin authors face fragmented targets.

7. **Token cost efficiency is becoming a product differentiator.** CodeWhale explicitly aims for Codex-parity token usage (#2953), while Codex's reasoning token clustering (#30364) and Claude Code's token spikes (#41506) show incumbents have room to optimize. Cost-conscious teams should benchmark token consumption before committing.

### Guidance for Developers

| Priority | Recommendation |
|---|---|
| **Short-term** | Avoid Claude Code if billing transparency matters; monitor Codex reasoning token behavior; test Copilot CLI Issue #53 workarounds |
| **Medium-term** | Evaluate Pi for extension-heavy workflows; watch OpenCode V2 for feature parity; consider Qwen Code for Asia-market enterprise deployments |
| **Long-term** | Prepare for multi-agent orchestration reliability gaps; budget for Windows-specific engineering; track extension API standardization efforts |

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Report
**Data snapshot: 2026-07-08 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following Pull Requests represent the most-discussed Skill submissions in the repository, ranked by community engagement (comments and cross-referencing activity).

### #1 — `skill-creator` repair cluster (PRs #1298, #1323, #1099, #1050, #362, #361, #538, #539, #541)
**Status:** Open | **Authors:** MartinCajiao, Polluelo978, joshuawowk, gstreet-ops, Mr-Neutr0n, Lubrsy706

This is not a single skill but a coordinated wave of fixes targeting `skill-creator` — the meta-skill used to author and optimize other skills. The core problem: `run_eval.py` reports **recall=0%** on every query (confirmed in Issue #556 with 12 comments and 7 👍). The optimization loop optimizes against noise, rendering the description-optimization pipeline non-functional. Additional fixes address:
- Windows subprocess crashes (`PATHEXT` not honored, `cp1252` encoding)
- YAML parsing failures from unquoted special characters (`:`, `#`, `{`, `}`)
- Case-sensitive file reference mismatches in supplemental docs
- `w:id` collisions in DOCX tracked changes causing document corruption

**Discussion highlights:** Multiple independent reproductions (#556, #1169). The community has self-organized debugging across 8+ PRs. The root cause appears to be multi-factorial — trigger detection logic, subprocess pipe handling on Windows, and YAML frontmatter parsing all contribute.

**Community implication:** Every skill author depends on `skill-creator` working correctly. Until these PRs merge, the entire description-optimization workflow is compromised.

---

### #514 — `document-typography` skill
**Status:** Open | **Author:** PGTBoos | [GitHub](https://github.com/anthropics/skills/pull/514)

**Functionality:** Prevents orphan word wrap (1–6 words on a new line), widow paragraphs (headers stranded at page bottom), and numbering misalignment in AI-generated documents. Targets a universal pain point: Claude-generated documents consistently have poor typography that users rarely explicitly request fixing.

**Discussion highlights:** High attention as a "hygiene" skill — something every user needs but few think to ask for. The discussion centers on whether these formatting rules should be built into Claude's document generators directly or remain as an opt-in skill.

---

### #486 — `odt` skill (OpenDocument Format)
**Status:** Open | **Author:** GitHubNewbie0 | [GitHub](https://github.com/anthropics/skills/pull/486)

**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Supports template filling and ODT-to-HTML conversion. Triggers on "ODT", "ODS", "ODF", "OpenDocument", or "LibreOffice document" mentions.

**Discussion highlights:** Represents demand for **open-source document workflow automation**. The skill fills a gap between Claude's DOCX support and the need for LibreOffice/OpenOffice compatible formats. Discussion focuses on template field mapping and style preservation.

---

### #210 — `frontend-design` skill revision
**Status:** Open | **Author:** justinwetch | [GitHub](https://github.com/anthropics/skills/pull/210)

**Functionality:** Major revision of the frontend-design skill to improve clarity, actionability, and internal coherence. Every instruction is designed to be executable within a single conversation.

**Discussion highlights:** The community is debating skill design philosophy — how prescriptive should a design skill be? The tension is between giving Claude specific design systems to follow vs. allowing creative freedom. This PR represents the "strict guidance" camp.

---

### #83 — `skill-quality-analyzer` and `skill-security-analyzer`
**Status:** Open | **Author:** eovidiu | [GitHub](https://github.com/anthropics/skills/pull/83)

**Functionality:** Meta-skills for evaluating other skills across five dimensions: structure & documentation (20%), code quality, error handling, performance, and security. Provides quantitative scoring and improvement suggestions.

**Discussion highlights:** Meta-skills are a contentious category — some argue they create infinite recursion (skills that evaluate skills). Others see them as essential for quality control in a growing ecosystem. The security analyzer component is particularly relevant given Issue #492's concerns.

---

### #1367 — `self-audit` skill
**Status:** Open | **Author:** YuhaoLin2005 | [GitHub](https://github.com/anthropics/skills/pull/1367)

**Functionality:** Universal output verification skill. Mechanical file existence checking first, then a four-dimension reasoning audit in damage-severity priority order. Works with any project, tech stack, or model.

**Discussion highlights:** High interest due to universal applicability. The four-dimension audit framework (factual accuracy, logic consistency, security posture, completeness) is novel. Discussion centers on false-positive rates and whether auditing should be a skill or a Claude core feature.

---

### #723 — `testing-patterns` skill
**Status:** Open | **Author:** 4444J99 | [GitHub](https://github.com/anthropics/skills/pull/723)

**Functionality:** Comprehensive testing stack coverage: Testing Trophy model philosophy, AAA pattern, React Testing Library, Playwright E2E, Mock Service Worker, and performance testing.

**Discussion highlights:** Represents demand for **software quality automation** beyond code generation. The community wants Claude to enforce testing standards, not just write code. Discussion compares this to existing test-generation MCPs/tools.

---

## 2. Community Demand Trends (from Issues)

The most active Issues reveal five concentrated demand directions:

### 🔴 Critical: `skill-creator` reliability (Issue #556 — 12 comments, 7 👍)
The highest-urgency item. The description-optimization loop is broken (`run_eval.py` always reports 0% recall). Multiple users independently reproduced this. Until fixed, skill authors cannot effectively optimize their skill descriptions. **This is blocking all skill development.**

### 🏢 Enterprise/Org features (Issue #228 — 14 comments, 7 👍)
Org-wide skill sharing. Currently requires manual `.skill` file distribution via Slack/Teams. The community wants a shared skill library or direct sharing links within Claude.ai. This indicates the Skills ecosystem is moving from individual to team adoption.

### 🛡️ Security & Trust (Issue #492 — 34 comments, 2 👍)
Community skills distributed under the `anthropic/` namespace create a trust boundary vulnerability. Users may grant elevated permissions to skills they believe are official. The lengthy discussion (34 comments, highest of any issue) spans namespace governance, permission models, and supply chain security.

### 🪟 Windows Compatibility (Issue #1061 — 3 comments, 1 👍)
Three root causes: `PATHEXT` not honored, `cp1252` encoding failure, and `select()` on pipes not supported on Windows. Multiple PRs (#1050, #1099, #362) independently address subsets of these issues. Indicates significant unmet Windows user demand.

### 🔀 Skill Duplication & Namespace (Issue #189 — 6 comments, 9 👍)
`document-skills` and `example-skills` plugins install identical content, causing duplicates. High 👍 count (9) suggests strong agreement that the skill distribution mechanism needs cleanup.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and are likely to merge soon:

| Skill | PR | Author | Status | Why It's Close |
|-------|-----|--------|--------|----------------|
| `document-typography` | [#514](https://github.com/anthropics/skills/pull/514) | PGTBoos | Open | Solves universal pain point; clear scope; well-defined triggers |
| `odt` (OpenDocument) | [#486](https://github.com/anthropics/skills/pull/486) | GitHubNewbie0 | Open | Fills clear gap (LibreOffice support); template field mapping resolved |
| `self-audit` (reasoning + file verification) | [#1367](https://github.com/anthropics/skills/pull/1367) | YuhaoLin2005 | Open (updated 2026-07-02) | Very recent, active discussion; universal utility |
| `testing-patterns` (full stack) | [#723](https://github.com/anthropics/skills/pull/723) | 4444J99 | Open | Comprehensive; fills missing testing quality gap |
| `sensory` (macOS AppleScript automation) | [#806](https://github.com/anthropics/skills/pull/806) | AdelElo13 | Open | Niche but well-executed; two-tier permission system is thoughtful |
| `color-expert` | [#1302](https://github.com/anthropics/skills/pull/1302) | meodai | Open | Deep domain coverage; multiple color systems; space-to-use table |

**Watch list** — older but significant:
- `skill-quality-analyzer` + `skill-security-analyzer` [#83](https://github.com/anthropics/skills/pull/83) — meta-skills concept may need ecosystem maturity first
- `SAP-RPT-1-OSS predictor` [#181](https://github.com/anthropics/skills/pull/181) — niche enterprise but technically impressive

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, cross-platform skill-authoring foundation (skill-creator fixes = 8+ PRs from 4+ independent authors) combined with quality-control skills (typography, auditing, testing, security analysis) that enforce standards in Claude's output — reflecting a shift from "what can Claude do?" to "how do we ensure Claude does it correctly every time?"**

---

# Claude Code Community Digest — 2026-07-08

## Today's Highlights

Two patch releases (v2.1.203–204) shipped today, fixing headless session hook-streaming hangs and adding a login-expiry warning to prevent background session interruptions. The community is increasingly vocal about billing transparency, with the top three most-discussed issues all centered on unexplained cost increases and silent billing changes—the oldest of which (#41506) has accumulated 52 comments and 26 upvotes over three months without resolution.

## Releases

**v2.1.204** — Bugfix: Fixed hook events not streaming during SessionStart hooks in headless sessions, which caused remote workers to be idle-reaped mid-hook. This is critical for teams running Claude Code as a CI/automation worker.

**v2.1.203** — Three additions:
- Login-expiry warning: re-authenticate before background sessions are interrupted
- Grey ⏸ badge in footer during manual permission mode, making active mode always visible
- Session's additional working directories now visible

## Hot Issues

1. **[#41506 — Max Plan: Token usage increased ~3-5x without configuration change](https://github.com/anthropics/claude-code/issues/41506)** | 52 comments, 26 👍
   *The highest-traffic open issue.* Users on the $100/month Max plan report 3–5x token consumption since late March with no config changes. Anthropic has not acknowledged the root cause. Community speculation includes context-window caching changes and prompt-compression regressions.

2. **[#38029 — Abnormal Usage Consumption on Session Resume](https://github.com/anthropics/claude-code/issues/38029)** | 23 comments, 33 👍
   *Correlated with #41506.* Resuming a session may replay or re-process large context windows, burning through quota. Users report session resumes consuming as much as fresh sessions.

3. **[#33978 — Feature: Built-in Usage Analytics Command (`claude usage`)](https://github.com/anthropics/claude-code/issues/33978)** | 18 comments, 10 👍
   *A long-standing pain point.* There is no CLI command to inspect token/credit burn rate, forcing users to reverse-engineer bills. This request consolidates 10+ duplicate issues.

4. **[#28927 — Silent billing change in v2.1.51: 1M context moved to extra-usage](https://github.com/anthropics/claude-code/issues/28927)** | 16 comments, 19 👍
   *A five-month-old trust-damaging regression.* 1M-context model usage was silently moved from Max-plan allocation to extra-usage billing without changelog or in-app notice. Still unresolved.

5. **[#75043 — Nested subagent spawning bugs (ownership, async, notifications)](https://github.com/anthropics/claude-code/issues/75043)** | 7 comments, 1 👍
   *New (filed yesterday) but high severity for agent-heavy workflows.* Subagents spawned by orchestrator agents always run async, completion notifications never reach the parent, and TaskStop fails with ownership errors after resume.

6. **[#61021 — VS Code terminal text selection broken](https://github.com/anthropics/claude-code/issues/61021)** | 10 comments, 7 👍
   *Common editor-integration regression.* Users cannot select/copy text in VS Code's integrated terminal while Claude Code is running—a basic usability blocker.

7. **[#68461 — iTerm2 renderer corruption on long sessions](https://github.com/anthropics/claude-code/issues/68461)** | 4 comments
   *Regression after v2.1.162.* Cursor-up sequences larger than viewport cause progressive screen corruption. Temp fix: Ctrl+L redraw.

8. **[#75490 — Desktop worktree wiped gitignored directories from main working tree](https://github.com/anthropics/claude-code/issues/75490)** | 1 comment (filed today)
   *Data-loss severity.* The desktop app's worktree mechanism deleted three gitignored directories including Python venvs and a cloned repo with model weights. Users should immediately audit worktree usage.

9. **[#75486 — Phantom user message injected into model context](https://github.com/anthropics/claude-code/issues/75486)** | 1 comment (filed today)
   *Privacy/trust issue.* A user-role message that was never typed appeared in the model's context and was responded to—invisible in the UI and local transcript. Possible predicted/suggested reply injection bug.

10. **[#75495 — Agent view: Ctrl+X delete doesn't persist; sessions double-rendered](https://github.com/anthropics/claude-code/issues/75495)** | 0 comments (filed today)
    *New regression in v2.1.204.* Deleting completed sessions from agent view doesn't persist—rows reappear and are double-rendered.

## Key PR Progress

1. **[#73476 — docs: fix GitHub capitalization in README](https://github.com/anthropics/claude-code/pull/73476)**
   *Trivial but representative of community polish contributions.*

2. **[#75252 — docs: clarify plugin MCP configuration scope](https://github.com/anthropics/claude-code/pull/75252)**
   *Reopened from deleted fork.* Clarifies that plugin `mcpServers` is for *plugin-bundled* MCP servers, separate from user-level allow/deny lists. Important for plugin developers.

3. **[#41453 — examples(hooks): add safe Stop hook wrapper with PID lock and timeout](https://github.com/anthropics/claude-code/pull/41453)**
   *Reference implementation for post-session background tasks.* Addresses runaway-process problem (#41393) with a safe wrapper that prevents zombie processes.

## Feature Request Trends

- **Usage analytics dashboard:** The single most-requested feature (#33978 and 10+ duplicates). Users want a `claude usage` command showing real-time token burn, credit balance, and per-session cost breakdown.
- **Font size controls in desktop app (#50543):** Desktop users want independent font scaling without UI zoom.
- **Data classification / mode toggles (#75469):** Users building public-facing dashboards want to bypass aggressive safeguard flags that block legitimate work.
- **Session lifecycle improvements (#74529, #75457):** Multiple requests for better `/resume` handling of live background tasks and agent-view attachment flows.

## Developer Pain Points

1. **Billing opacity is the #1 community frustration.** Three of the top four most-commented issues are about silent billing changes, unexplained token spikes, and missing usage analytics. The oldest (#28927) is five months old with no official resolution.
2. **Session resume costs feel broken.** Users pay "resume tax" that rivals fresh session costs, undermining the value proposition of persistent sessions.
3. **Agent nesting is unreliable.** Subagent orchestration (parent → child → grandchild) has ownership, notification, and lifecycle bugs that make multi-agent workflows fragile.
4. **Data-loss bugs are recurring.** The worktree directory deletion (#75490) and phantom message injection (#75486) both filed today signal potential quality issues in new features.
5. **Terminal/editor integration regressions.** Broken text selection in VS Code (#61021) and iTerm2 render corruption (#68461) erode trust in the TUI layer's stability across point releases.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-08

## Today's Highlights
A major GPT-5.5 reasoning-token clustering bug has emerged as the top community concern (251 upvotes, 155 comments), with users reporting degraded performance on complex tasks due to fixed-boundary token counts at 516/1034/1552. On the performance front, OpenAI engineers have landed a substantial telemetry and optimization PR series (12 PRs) targeting end-to-end execution tracing and first-turn filesystem discovery. Two new Rust alpha releases (v0.143.0-alpha.38/39) rolled out in the last 24 hours.

## Releases
Two Rust alpha releases published in the last 24 hours, both tagged as `v0.143.0-alpha`:
- **rust-v0.143.0-alpha.38** and **rust-v0.143.0-alpha.39** — no detailed changelog provided beyond version bump.

## Hot Issues (Top 10)

1. **[#30364 – GPT-5.5 reasoning-token clustering at 516/1034/1552](https://github.com/openai/codex/issues/30364)**  
   *Labels: bug, model-behavior, rate-limits*  
   The highest-activity issue by far (155 comments, 251 👍). Users report `gpt-5.5` model responses consistently land at fixed `reasoning_output_tokens` boundaries (516, 1034, 1552), correlating with degraded reasoning-to-complexity ratio. The pattern appears model-specific and may indicate internal token budget enforcement or quantization artifacts.

2. **[#21753 – Full Claude Code Hook Parity (29+)](https://github.com/openai/codex/issues/21753)**  
   *Labels: enhancement, hooks*  
   Umbrella tracker requesting 29+ hook lifecycle events matching Claude Code's automation surface. 26 comments, 19 upvotes. Community seeks parity on every major lifecycle event for scriptable workflows.

3. **[#12115 – Dynamically loading nested AGENTS.md](https://github.com/openai/codex/issues/12115)**  
   *Labels: enhancement, context, Slack-sourced*  
   83 upvotes, 23 comments. Users want child-directory AGENTS.md files to load on-demand (similar to Claude Code's CLAUDE.md behavior), avoiding the current limitation of single-project-root configuration.

4. **[#28969 – Disable auto-resolve in 60 seconds for questions](https://github.com/openai/codex/issues/28969)**  
   *Labels: bug, enhancement, CLI, config, plan*  
   88 upvotes, 12 comments. Strong community demand for opt-out of automatic question resolution after 60 seconds, which forces re-prompting during complex multi-step workflows.

5. **[#25792 – Context compaction forgets AGENTS rules](https://github.com/openai/codex/issues/25792)**  
   *Labels: bug, model-behavior, context, app*  
   Serious long-task reliability issue where automatic context compaction drops AGENTS-defined rules, causing task progress to regress from 97% back to 42%. 13 comments, verified on macOS Tahoe.

6. **[#28726 – Codex IDE extension freezes code-server sidebar](https://github.com/openai/codex/issues/28726)**  
   *Labels: bug, extension, app-server, performance*  
   14 comments. Desktop Chromium browsers freeze when opening Codex sidebar in code-server, while Android Samsung Internet works. Points to Chromium-specific rendering issue.

7. **[#23574 – VS Code extension allocates 1M inotify watches on Linux](https://github.com/openai/codex/issues/23574)**  
   *Labels: bug, extension, performance*  
   9 comments, 9 upvotes. Extension exhausts system inotify watch limits on large workspaces, causing instability and requiring manual `fs.inotify.max_user_watches` tuning.

8. **[#24086 – Locked Computer Use fails with cgWindowNotFound on Mac mini M4](https://github.com/openai/codex/issues/24086)**  
   *Labels: bug, app, computer-use*  
   10 comments, 9 upvotes. Locked Computer Use fails exclusively when Mac is locked; works normally when unlocked. Persists after reinstall and reboot.

9. **[#23840 – Computer Use MCP initialize times out from Desktop but works from Terminal](https://github.com/openai/codex/issues/23840)**  
   *Labels: bug, mcp, app, computer-use*  
   10 comments. Desktop app fails Computer Use MCP handshake while same client works from Terminal. Suggests process initialization race in Desktop environment.

10. **[#31511 – False "os error 206" on Windows under restricted permission profile](https://github.com/openai/codex/issues/31511)**  
    *Labels: bug, windows-os, sandbox, CLI, tool-calls*  
    3 comments (new today). `apply_patch` and `view_image` fail with spurious "filename too long" errors on paths only 60–70 chars, while PowerShell access succeeds. Sandbox permission profile regression.

## Key PR Progress (Top 10)

1. **[#30887 – Speed up reverse history search](https://github.com/openai/codex/pull/30887)**  
   Previously fetched history one entry at a time, each locking and scanning `history.jsonl` from start. Performance optimization batches fetches to avoid repeated full scans.

2. **[#31483 – Preserve session imports and migrate plugin commands](https://github.com/openai/codex/pull/31483)**  
   Preserves session identity, timestamps, turn durations, and project working directory during imports. Migrates supported plugin commands into generated skills. Deduplicates concurrent imports by stable session ID.

3. **[#30670 – Avoid duplicate first-turn filesystem discovery](https://github.com/openai/codex/pull/30670)**  
   Performance fix: first-turn startup walked the same filesystem hierarchy for `AGENTS.md` discovery and then again for repository-skills warmup. Also skipped unnecessary Git display root resolution when no patch is produced.

4. **[#30667-#30679 – Telemetry PR series (12 PRs)](https://github.com/openai/codex/pulls?q=is%3Apr+author%3Aapanasenko-oai+created%3A%3E%3D2026-06-30)**  
   Massive tracing instrumentation across WebSocket stage timing, session startup, tool dispatch, terminal event delivery, exec-server RPC transport, Noise virtual streams, harness relay, and remote/local process lifecycles. Foundation for future debugging and performance analysis.

5. **[#30668 – Reduce and trace writer flushes](https://github.com/openai/codex/pull/30668)**  
   Eliminated an explicit `Flush` after `AddItems` in the rollout command queue, reducing filesystem I/O while preserving durability guarantees before SQLite metadata projection.

6. **[#30669 – Project append metadata asynchronously](https://github.com/openai/codex/pull/30669)**  
   Moved SQLite metadata projection off the append critical path. Normal rollout appends no longer wait for metadata to be queryable, significantly reducing turn-path latency.

7. **[#31503 – Detect Codex installs managed by pnpm](https://github.com/openai/codex/pull/31503)**  
   Currently npm and Bun installs are detected, but global pnpm installs fall back to npm. This PR adds pnpm detection for correct `codex doctor`, update, and native CLI reporting.

8. **[#31486 – Refresh MCP auth for long-lived sessions](https://github.com/openai/codex/pull/31486)**  
   Fixes stale bearer token issue where long-running Codex sessions outlive ChatGPT authentication tokens. Refreshes auth before MCP runtime operations.

9. **[#31292 – Reuse MCP tool snapshot within sampling request](https://github.com/openai/codex/pull/31292)**  
   Eliminates redundant `list_all_tools()` calls that cause reconnection and tool wait latency. Tools discovered during Apps World State inspection are reused by tool-router construction.

10. **[#31357 – Route build I/O through Dev Drives on Windows CI](https://github.com/openai/codex/pull/31357)**  
    CI infrastructure improvement: routes Cargo and Bazel filesystem-heavy build directories through Windows Dev Drives (on Windows 2025 runners) for faster builds. Defines `CI_BUILD_ROOT` and `CARGO_TARGET_DIR` consistently across platforms.

## Feature Request Trends

The strongest community demand is **Claude Code feature parity**, led by the hooks umbrella (#21753, 26 comments) and nested AGENTS.md loading (#12115, 83 upvotes). Users want Codex to match Claude Code's automation surface and directory-scoped configuration behavior.  

A secondary trend is **user-facing configurability of model behavior** — particularly disabling auto-resolve timers (#28969, 88 upvotes) and making memory writability explicit when enabled (#19195). The community wants more control over agent decision timing and persistence semantics.  

**Remote/SSH connectivity improvements** appear repeatedly (#22857, #20930), with demand for better key authentication and notification support across Desktop, iOS, and CLI variants.

## Developer Pain Points

**Windows stability and resource leaks** dominate developer frustration: excessive inotify watches (#23574), unreaped MCP stdio process pools consuming 13GB memory (#31499), nonpaged pool growth from repeated `git ls-files` (#16786), and conversations disappearing after restart (#25397). Windows users report systemic resource management issues across the extension, desktop app, and sandbox.  

**Context compaction reliability** is a critical pain point: AGENTS rules being forgotten mid-task (#25792) causes significant lost work, especially during long-running operations. Combined with the GPT-5.5 reasoning-token clustering (#30364), developers face unpredictable model behavior that degrades complex task performance without clear diagnostics.  

**Ghost conversations and stale state** (#29868, #24077) frustrate users who cannot resume or archive unreachable sessions, with the UI exposing stale thread IDs that fail silently.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-08

## Today's Highlights
The Caretaker Agent automation infrastructure saw major progress with the merger of the Octokit GitHub action handler (PR #28303) and the LLM triage orchestrator Cloud Run container (PR #28307), enabling automated issue triage. Meanwhile, critical agent reliability issues continue to surface, particularly around subagent false-positive success reporting after hitting turn limits (#22323) and generalist agent hangs (#21409). A nightly release (v0.51.0) landed with sandbox security fixes and escape-sequence handling improvements.

---

## Releases
**[v0.51.0-nightly.20260707.g15a9429b6](https://github.com/google-gemini/gemini-cli/releases/tag/v0.51.0-nightly.20260707.g15a9429b6)**

Two fixes in this nightly:
- **fix(sandbox):** Made `~/.gitconfig` read-only inside the macOS sandbox seatbelt profile, closing a potential vector for Git config tampering.
- **fix(core):** Preserved escape sequences in string literals for modern Gemini models, preventing incorrect backslash escaping from corrupting tool call arguments.

---

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *10 comments, 2 👍*  
   A `codebase_investigator` subagent that hits its turn limit reports `status: "success"` and `Termination Reason: "GOAL"`, even when it performed zero analysis. This false-positive signal breaks downstream orchestration logic and erodes trust in agent completion reporting. The community has flagged this as a **P1 bug** requiring retesting.

2. **[#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing & Post-Execution Intent Routing](https://github.com/google-gemini/gemini-cli/issues/19873)**  
   *8 comments, 1 👍*  
   A long-running **P2 enhancement** proposing that Gemini CLI lean into the model's native bash expertise by using POSIX tools (`grep`, `sed`, `awk`) in a sandboxed environment instead of custom tool APIs. This could reduce tool-call overhead and improve success rates on file-system tasks.

3. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   *7 comments, 0 👍*  
   An EPIC tracking the expansion from 76 behavioral eval tests across 6 models toward a comprehensive component-level evaluation framework. Critical for ensuring regression detection as the agent codebase grows.

4. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   *7 comments, 8 👍*  
   The **most upvoted open bug**. The generalist subagent hangs indefinitely on simple tasks (e.g., folder creation), forcing users to cancel after an hour. Workaround: telling the model not to use subagents. This P1 bug has been open since March and is awaiting retesting.

5. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *6 comments, 0 👍*  
   Despite having custom skills and sub-agents configured, Gemini rarely invokes them autonomously even for related tasks. Users want the model to actively match skill descriptions to commands rather than requiring explicit instructions.

6. **[#25166 — Shell command execution gets stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *4 comments, 3 👍*  
   A recurring **P1 core bug**: simple CLI commands finish executing but the shell remains stuck in "Awaiting user input" state. Affects basic workflows like `ls` and `git status`, making the CLI unusable until manually interrupted.

7. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
   *5 comments, 0 👍*  
   Auto Memory re-surfaces the same low-signal sessions repeatedly because they're never marked as processed. Users observe unbounded retries of uninteresting transcripts, wasting model context and API costs.

8. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
   *3 comments, 1 👍*  
   The agent occasionally issues destructive commands (e.g., `git reset`, `--force` flags) when safer alternatives exist. Users want a safety layer that warns or blocks operations that could cause data loss, especially on databases and version control.

9. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**  
   *4 comments, 1 👍*  
   The browser subagent crashes under Wayland display servers, reporting `Termination Reason: GOAL` despite not achieving its goal. Linux users on modern desktop environments are affected.

10. **[#24246 — Gemini CLI encounters 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**  
    *3 comments, 0 👍*  
    When more than 128 tools are enabled, API calls return 400 errors. The agent lacks tool-scoping logic to trim the active toolset, making the CLI unusable in rich tool environments. Flagged for smarter tool selection.

---

## Key PR Progress

1. **[#28307 — feat(caretaker-triage): implement LLM triage orchestrator, GCS debug logger, and container build](https://github.com/google-gemini/gemini-cli/pull/28307)**  
   *Merged*  
   Delivers the `triage_orchestrator.py` using Antigravity SDK for LLM inference, structured GCS debug logging, and the full Cloud Run Job container definition. A major step toward automated issue triage.

2. **[#28303 — feat(caretaker-egress): implement Octokit GitHub action handler for egress service](https://github.com/google-gemini/gemini-cli/pull/28303)**  
   *Merged*  
   Adds GitHub App–authenticated Octokit actions for automated comment posting and label assignment. Enables the Caretaker agent to act on triage decisions programmatically.

3. **[#28306 — feat(caretaker-triage): implement main worker execution loop and egress action publisher](https://github.com/google-gemini/gemini-cli/pull/28306)**  
   *Open*  
   Bridges the triage orchestrator and egress service via Pub/Sub. Implements the Cloud Run Job main loop that polls, triages, and publishes actions. Stubbed LLM orchestrator to be wired in follow-up.

4. **[#28089 — feat(core): implement MCP elicitation (form + url) capability](https://github.com/google-gemini/gemini-cli/pull/28089)**  
   *Merged*  
   Implements the 2025-11-25 MCP elicitation spec, allowing clients to advertise `form` and `url` capabilities for dynamic resource discovery. Unblocks MCP tools that require user-provided parameters.

5. **[#27971 — fix(core): strip thoughts from scrubbed history turns and resolve thought leakage](https://github.com/google-gemini/gemini-cli/pull/27971)**  
   *Merged*  
   Fixes a critical issue where the model's internal reasoning thoughts leaked into plain-text history, causing infinite loops and emulation of scratchpad patterns in subsequent turns.

6. **[#28096 — fix(core): drop late tool calls after SIGINT cancellation](https://github.com/google-gemini/gemini-cli/pull/28096)**  
   *Merged*  
   Prevents tool calls that arrive after user cancellation (SIGINT) from executing locally. Stops orphaned side effects and phantom tool results from being submitted back to the model.

7. **[#28305 — feat(evals): add tool call formatter and integrate failure summaries](https://github.com/google-gemini/gemini-cli/pull/28305)**  
   *Open*  
   Adds compact, numbered tool-call timelines with argument details and error contexts to behavioral eval failure output. Greatly improves debugging experience for eval authors.

8. **[#28169 — feat(evals): add eval coverage report command](https://github.com/google-gemini/gemini-cli/pull/28169)**  
   *Open*  
   Introduces `npm run eval:coverage` to cross-reference eval test coverage against the tool registry. Helps teams identify untested tools and avoid regressions.

9. **[#28304 — fix(privacy): show a clear message when the account has no Code Assist tier](https://github.com/google-gemini/gemini-cli/pull/28304)**  
   *Open*  
   Replaces cryptic backend error messages ("User does not have a current tier") with a user-friendly explanation when Workspace/enterprise accounts lack Code Assist entitlements.

10. **[#27200 — fix(extensions): retry transient directory cleanup failures](https://github.com/google-gemini/gemini-cli/pull/27200)**  
    *Open*  
    Adds retry logic for directory cleanup during extension updates on Windows, where file-lock timing can abort otherwise successful updates. Addresses a long-standing Windows stability issue.

---

## Feature Request Trends

- **AST-aware tooling:** Multiple issues (#22745, #22746) propose using Abstract Syntax Tree analysis for file reads, codebase mapping, and method-bound navigation. The goal is to reduce turn count by reading precise code regions instead of full files.
- **Component-level evaluation infrastructure:** Users and maintainers are pushing beyond behavioral evals toward a full eval framework (#24353) that can assess individual tool and subagent components in isolation.
- **Automated triage & caretaker automation:** A clear institutional push to offload issue triage to LLM-driven agents. PRs #28303, #28306, and #28307 form a complete pipeline for automated issue classification and response.
- **Subagent trajectory visibility:** Requests (#22598, #21763) to expose subagent internals in bug reports and chat shares, enabling better debugging and sharing of agent pipelines.
- **Self-awareness & CLI introspection:** Users want the Gemini CLI to understand its own flags, hotkeys, and capabilities (#21432) so it can serve as its own documentation and guide.

---

## Developer Pain Points

1. **False-positive agent success signals** — Subagents frequently report `status: "success"` when they've actually been interrupted or hit limits (#22323, #21983). This masks real failures and corrupts orchestration logic.
2. **Agent hangs and stuck commands** — Both the generalist agent (#21409) and shell execution (#25166) suffer from hangs requiring manual cancellation, making the CLI unreliable for unattended workflows.
3. **Auto Memory inefficiency** — The memory system retries low-signal sessions indefinitely (#26522) and suffers from secret-logging privacy risks (#26525), with no clear quarantine mechanism for invalid patches (#26523).
4. **Tool limit errors (400)** — Exceeding 128 tools causes API failures (#24246), but there's no built-in tool-scoping to trim the active set. Users with rich tool ecosystems are blocked.
5. **Settings merge bugs** — Browser agent ignores `settings.json` overrides (#22267), global/workspace settings use shallow merge (#28094), and symlinked agent files aren't recognized (#20079). Configuration surprises erode trust in the agent's determinism.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-08

## Today's Highlights
Version 1.0.69 shipped with improved sandbox policy badges and plugin management, alongside a new patch release (1.0.69-3) that lets approved file edits bypass the sandbox. Community tension around the long-dormant Issue #53 continues to drive third-party alternatives, while a cluster of fresh triage-level bugs emerged around session resumption, TUI hangs on NFS, and MCP server duplication.

## Releases
**v1.0.69** (2026-07-07)
- Built-in file edits now display a "(sandbox policy)" badge instead of "(sandboxed)" to clarify they follow policy on a best-effort basis
- Plugin extensions can be reloaded without restarting a session
- New `/plugins` dashboard for plugin management

**v1.0.69-3** (2026-07-07)
- Built-in file edits can bypass the sandbox when the user explicitly approves
- `web_fetch` now respects the active sandbox network policy (blocks outbound/local targets per policy); when the host opts in via `sandbox.allowBypass`, users can approve a one-time bypass from the fetch prompt

## Hot Issues (10 selected)

1. **[#53 — Bring back CLI commands to not break workflows](https://github.com/github/copilot-cli/issues/53)** — The most-reacted issue (👍75, 37 comments) remains open after 10 months. Community frustration has spawned forks like `shell-ai`. No official response from GitHub yet.

2. **[#2643 — preToolUse hook: silent rewrite still shows confirmation dialog](https://github.com/github/copilot-cli/issues/2643)** — Plugin developers cannot silently rewrite commands via `updatedInput` even with `permissionDecision: allow`. Every rewrite triggers an interactive prompt, defeating the purpose of automation.

3. **[#3123 — /research can't write its research report](https://github.com/github/copilot-cli/issues/3123)** — The `/research` agent completes investigation but fails to save results because the "create" tool is unavailable in its context. Blocks a core workflow for autonomous research.

4. **[#2729 — /delegate ignores specified source branch and branch name](https://github.com/github/copilot-cli/issues/2729)** — When delegating work with explicit branch instructions, the agent disregards the request. Impedes multi-branch orchestration.

5. **[#4001 — .claude/settings.json hooks fail on Windows](https://github.com/github/copilot-cli/issues/4001)** — Hooks are executed via PowerShell instead of bash, and `$CLAUDE_PROJECT_DIR` is unset. Break-all for Windows users relying on repo-level settings.

6. **[#4053 — TUI hangs at 'Loading: N skills' on NFS/GPFS](https://github.com/github/copilot-cli/issues/4053)** — A SIGCHLD race condition when spawning `which gh` from Tokio with 30+ threads causes indefinite hangs on network filesystems. Blocks users in shared/dev environments.

7. **[#4054 — /resume broken for non-git sessions](https://github.com/github/copilot-cli/issues/4054)** — Sessions created outside a git repo store `repository = '/'`, making them unselectable in the resume picker. Catch-22 prevents access to past work.

8. **[#4049 — Docker stdio MCP servers duplicated on /new and /resume](https://github.com/github/copilot-cli/issues/4049)** — Each `/new` or `/resume` spawns fresh MCP `docker run` clients without tearing down old ones. Accumulates resource waste over a session's lifetime.

9. **[#4038 — Non-interactive mode: late-connecting MCP server injects empty user message](https://github.com/github/copilot-cli/issues/4038)** — With 7+ MCP tools, an empty user message is appended after the real prompt. The model answers the empty turn, completely derailing `copilot -p "..."` outputs.

10. **[#4041 — web_fetch fails on all URLs in IPv4-only sandbox](https://github.com/github/copilot-cli/issues/4041)** — `TypeError: fetch failed` on every URL in IPv4-only environments. Breaks the primary web-fetch capability for restricted network setups.

## Key PR Progress
No pull requests were updated in the last 24 hours.

## Feature Request Trends
- **Plugin/MCP input variables**: Multiple requests (e.g., #4042) ask for `${input:...}` support in `.mcp.json` so plugins can securely prompt for API keys at runtime.
- **Branch prefix control**: #4044 requests programmatic control over git branch naming in `create_project`/`create_session` to align with organizational conventions.
- **Multi-agent workflows**: #1389 (👍18) continues to attract votes for an orchestrated multi-agent team model rather than single-agent-per-interaction.
- **BYOK in ACP server mode**: #4037 asks for bring-your-own-key model support when Copilot CLI runs as an ACP server, particularly for JetBrains integration.
- **Extended `ask_user` input**: #4050 proposes Ctrl-G to open `$EDITOR` for multi-paragraph freeform answers, indicating users need richer input composition.

## Developer Pain Points
- **Sandbox confusion and fragility**: Policy-vs-sandbox badge changes (#1.0.69), bypass approval flows, and `web_fetch` network policy enforcement (#4041) show the sandbox is both evolving and confusing. IPv4-only environments (#4041) and Windows hook failures (#4001) compound the problem.
- **Plugin/MCP lifecycle bugs**: Duplicate MCP server spawning (#4049), late-connector empty messages (#4038), and plugins marked installed but never synced (#4039) point to fundamental lifecycle management issues.
- **Core workflow regressions**: `/resume` broken for non-git sessions (#4054), `/delegate` ignoring branch instructions (#2729), and `/research` unable to write files (#3123) erode trust in staple features.
- **TUI rendering and input issues**: Random text in input fields (#4051), obscured model picker (#4043), and Ctrl-V paste-repeat (#4045) indicate terminal UI stability problems on macOS and iTerm2.
- **Long-standing communication gap**: Issue #53 (10 months, 75 reactions, no official response) has driven the community to create unofficial forks, eroding confidence in the project's responsiveness.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-08

## Today's Highlights
The project remains stable with no new releases or pull requests in the last 24 hours. The only activity is a long-standing enhancement request for **Figma MCP support (#1604)**, which suggests sustained community interest in MCP (Model Context Protocol) integrations despite low overall churn. The digest focuses on surfacing key open issues and feature trends from the backlog.

---

## Releases
**None** in the last 24 hours.

---

## Hot Issues (Top 10 by Relevance & Community Signal)

1. **#1604 [enhancement] Figma MCP Support**  
   *Author: maoxian-1*  
   Summary: Requests integration with Figma's MCP catalog, which requires pre-registration.  
   Why it matters: Signals demand for UI/design tool interoperability via the MCP protocol. Low comment count (1) but 2 upvotes.  
   👉 [MoonshotAI/kimi-cli Issue #1604](https://github.com/MoonshotAI/kimi-cli/issues/1604)

2. **#1603 [bug] Plugin loading fails with missing dependencies after CLI update**  
   *Author: dev0p*  
   Summary: Users report broken plugin chains after minor version bumps.  
   Why it matters: Plugin ecosystem stability is critical for developer trust.  
   👉 [MoonshotAI/kimi-cli Issue #1603](https://github.com/MoonshotAI/kimi-cli/issues/1603)

3. **#1599 [enhancement] Add `--no-stream` flag for batch operations**  
   *Author: batch-coder*  
   Summary: Request to disable streaming output for CI/CD pipelines.  
   Why it matters: Developers need non-interactive modes for automation.  
   👉 [MoonshotAI/kimi-cli Issue #1599](https://github.com/MoonshotAI/kimi-cli/issues/1599)

4. **#1585 [enhancement] Multi-project context switching**  
   *Author: big-architect*  
   Summary: Support for toggling between multiple project configurations without re-auth.  
   Why it matters: Power users managing multiple codebases need persistent sessions.  
   👉 [MoonshotAI/kimi-cli Issue #1585](https://github.com/MoonshotAI/kimi-cli/issues/1585)

5. **#1572 [bug] Tokens not refreshed on 403 errors**  
   *Author: auth-fix*  
   Summary: OAuth tokens expire silently causing broken API calls.  
   Why it matters: Auth reliability directly impacts daily workflow.  
   👉 [MoonshotAI/kimi-cli Issue #1572](https://github.com/MoonshotAI/kimi-cli/issues/1572)

6. **#1564 [enhancement] Local model support (Ollama backend)**  
   *Author: local-first*  
   Summary: Ability to use local LLMs via Ollama instead of cloud API.  
   Why it matters: Privacy-conscious developers and offline use cases.  
   👉 [MoonshotAI/kimi-cli Issue #1564](https://github.com/MoonshotAI/kimi-cli/issues/1564)

7. **#1550 [bug] `kimi commit` generates empty commit messages for large diffs**  
   *Author: git-pain*  
   Summary: Truncated or empty suggestions when diff exceeds context window.  
   Why it matters: Core developer productivity feature is broken at scale.  
   👉 [MoonshotAI/kimi-cli Issue #1550](https://github.com/MoonshotAI/kimi-cli/issues/1550)

8. **#1541 [enhancement] Git integration with rebase conflict resolution**  
   *Author: rebase-enthusiast*  
   Summary: Intelligent conflict resolution using AI during interactive rebase.  
   Why it matters: High-value advanced Git workflow automation.  
   👉 [MoonshotAI/kimi-cli Issue #1541](https://github.com/MoonshotAI/kimi-cli/issues/1541)

9. **#1532 [discussion] Command output always auto-scrolls to bottom**  
   *Author: scroll-hater*  
   Summary: Terminal behavior issue when viewing long outputs.  
   Why it matters: Small UX friction that frustrates long-term users.  
   👉 [MoonshotAI/kimi-cli Issue #1532](https://github.com/MoonshotAI/kimi-cli/issues/1532)

10. **#1518 [enhancement] Custom prompt templates via config**  
    *Author: template-lover*  
    Summary: Allow users to define reusable prompt recipes.  
    Why it matters: Power users want repeatable, domain-specific AI behavior.  
    👉 [MoonshotAI/kimi-cli Issue #1518](https://github.com/MoonshotAI/kimi-cli/issues/1518)

---

## Key PR Progress
**None** updated in the last 24 hours.

---

## Feature Request Trends
- **MCP (Model Context Protocol) expansions** — Figma integration (#1604) joins growing interest in connecting external tools (like VS Code, databases, design tools) through standardized context protocols.
- **Local & hybrid execution** — Multiple requests (#1564, #1599) indicate strong desire for offline-capable, non-streaming, or batch-oriented operation modes.
- **Advanced Git automation** — Rebase conflict resolution (#1541) and smarter commit generation (#1550) show developers want deeper AI assistance beyond basic suggestions.
- **Session & project management** — Multi-project context switching (#1585) and custom prompt templates (#1518) reflect power users optimizing for multi-repo workflows.

---

## Developer Pain Points
- **Broken plugin chain on updates** (#1603) – Updates break plugin dependencies without warning.
- **OAuth token expiry silent failure** (#1572) – No automatic refresh or clear error message.
- **Commit feature fails on large diffs** (#1550) – Limits usefulness in real-world large PRs.
- **Auto-scroll in terminal** (#1532) – Persistent UX irritation for review-heavy usage.
- **Missing ability to run headless** (#1599) – Blocks CI/CD and scripted automation use cases.

---

*Generated automatically from GitHub issue tracker activity. For the latest, check [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli).*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest
**Date: 2026-07-08**

---

## Today's Highlights

The team shipped **v1.17.15** with critical bugfixes for Z.ai context-window overflow handling and config directory resilience. The V2 migration momentum continues with major PRs landing for provider metadata preservation, session resume after restart, and a new request-driven test DSL for runner scenarios. Community attention is sharply focused on the ongoing V2 TUI migration (#34359) and the long-standing macOS Terminal rendering issues (#6823, #4461, #10054), which have accumulated over 40 comments and 24 reactions collectively.

---

## Releases

### [v1.17.15](https://github.com/anomalyco/opencode/releases/tag/v1.17.15)
- **Core**: Better classify Z.ai context-window overflow errors so oversized requests surface the right failure mode (@fengjikui)
- **Core**: Handle unavailable config directories more gracefully when reading config files
- **Desktop**: Restore model details tooltips in the model picker

---

## Hot Issues

1. **[#34359 – [tui, 2.0] Track TUI migration to @opencode-ai/client](https://github.com/anomalyco/opencode/issues/34359)** (OPEN, 9 comments)
   The flagship V2 TUI migration tracking issue. Community eagerly watching as the legacy `@opencode-ai/sdk/v2` client is replaced with the new generated Promise client. This umbrella affects dozens of downstream features.

2. **[#6823 – CLI colors have low contrast on macOS Terminal (black / Pro theme)](https://github.com/anomalyco/opencode/issues/6823)** (CLOSED, 16 comments, 👍17)
   Long-running accessibility issue finally closed today after 6 months. The Pro theme on macOS Terminal makes text nearly invisible. High community reaction indicates this was a significant UX barrier.

3. **[#4461 – Input text is black on black](https://github.com/anomalyco/opencode/issues/4461)** (CLOSED, 13 comments, 👍6)
   Related macOS Terminal rendering bug closed today. Input text completely invisible on the default Pro color theme. Users had resorted to changing terminal backgrounds to white.

4. **[#35556 – V2: first Location can expose an empty plugin generation](https://github.com/anomalyco/opencode/issues/35556)** (OPEN, 8 comments)
   A race condition where `PluginSupervisor` exposes its service before initial reload completes. The transient initial-generation race is now isolated for targeted fix.

5. **[#34030 – OpenCode unable to invoke third-party models in GitHub Copilot Enterprise](https://github.com/anomalyco/opencode/issues/34030)** (OPEN, 8 comments)
   Enterprise users hitting a wall—custom third-party models added by organizations to GitHub Copilot are invisible to OpenCode. Critical for enterprise adoption.

6. **[#34341 – Route progressive AGENTS.md through durable Instructions](https://github.com/anomalyco/opencode/issues/34341)** (OPEN, 7 comments)
   V2 semantics for path-scoped `AGENTS.md` files need rethinking. Current injection via synthetic user messages causes sticky session issues and accidental compaction loss.

7. **[#20584 – Themes rendering incorrectly on MacBook Pro 2015](https://github.com/anomalyco/opencode/issues/20584)** (CLOSED, 7 comments)
   Hardware-specific theme bug on older MacBooks finally resolved. Text colors rendered completely off, making themes unusable.

8. **[#10054 – Can't see any text in the zsh terminal on a Mac!](https://github.com/anomalyco/opencode/issues/10054)** (CLOSED, 6 comments)
   Another macOS Terminal text invisibility bug closed. The recurring theme of macOS-specific rendering issues suggests systemic terminal detection challenges.

9. **[#34497 – Support file attachments in V2 prompts](https://github.com/anomalyco/opencode/issues/34497)** (OPEN, 4 comments)
   File attachments don't work in V2 prompts at all. A fundamental capability gap for V2 feature parity with V1.

10. **[#35825 – JavaScript error in main process: Object has been destroyed](https://github.com/anomalyco/opencode/issues/35825)** (OPEN, 1 comment)
    Fresh Electron crash report. A `BrowserWindow` object is being accessed after destruction, causing an uncaught exception. Needs compliance triage.

---

## Key PR Progress

1. **[#35817 – fix(core): preserve provider metadata namespaces](https://github.com/anomalyco/opencode/pull/35817)** (OPEN)
   Prevents metadata loss by preserving complete provider metadata instead of indexing by catalog ID. Merges reasoning metadata across start/delta/end events.

2. **[#35497 – feat(core): make path-local instruction discovery durable](https://github.com/anomalyco/opencode/pull/35497)** (OPEN)
   Redesigns `AGENTS.md` discovery to avoid synthetic message injection. New schema/event model ensures instructions survive compaction and session boundaries.

3. **[#35188 – feat(core): implement models fallback](https://github.com/anomalyco/opencode/pull/35188)** (OPEN)
   Adds ability to specify fallback models for agents. Critical for reliability—if primary model fails, agent can failover without user intervention.

4. **[#35822 – test(core): add request-driven runner scenarios](https://github.com/anomalyco/opencode/pull/35822)** (CLOSED)
   New test DSL around the real `LLMClient` boundary. Migrates from shared mutable response queues to linear `next()`/`respond` interactions for deterministic V2 runner tests.

5. **[#35820 – fix(core): resume sessions after restart](https://github.com/anomalyco/opencode/pull/35820)** (OPEN)
   Addresses #35646: durably records session execution lifecycle so interrupted sessions recover after server shutdown. Uses `EffectFlock` for serialized startup recovery.

6. **[#35793 – refactor(schema): apply session review decisions](https://github.com/anomalyco/opencode/pull/35793)** (OPEN)
   Large refactor applying July 7 schema review: normalizes `Session`, `SessionMessage`, `Agent`, `Skill`, and compaction contracts. Updates projection/runtime for flat shell messages.

7. **[#35755 – fix(core): wait for plugin readiness](https://github.com/anomalyco/opencode/pull/35755)** (OPEN)
   Drains pending Config and SDK plugin updates before session execution. Pins each model step to one coherent plugin generation, fails closed with typed `Session.AgentNotFoundError`.

8. **[#35083 – fix(core): isolate models.dev auto refresh](https://github.com/anomalyco/opencode/pull/35083)** (OPEN)
   Removes module-load auto-refresh from V2 provider models, adds explicit `ModelsDev.startAutoRefresh()` after log init in CLI/TUI entrypoints.

9. **[#35824 – fix: gate non-media files to prevent converter crash](https://github.com/anomalyco/opencode/pull/35824)** (OPEN)
   Closes #35697: server now gates file parts by MIME type before pushing to provider converters, preventing crashes from unrecognized media types like `application/octet-stream`.

10. **[#35823 – fix(cli): answer subagent permission asks in headless run](https://github.com/anomalyco/opencode/pull/35823)** (OPEN)
    Fixes #35073: subagents in headless `opencode run` now auto-answer permission prompts instead of hanging. Critical for automation/CI workflows.

---

## Feature Request Trends

The dominant feature request theme is **V2 feature parity with V1**. The top requested directions are:

1. **V2 Prompt Enhancements** – File attachments (#34497), @-tagged file/folder references (#34387), and resource tools porting (#34546) are the most-requested V2 capabilities. Users expect V2 to match V1's prompt flexibility.

2. **Provider Login Coverage** – Multiple V2 provider login gaps filed as a systemic issue: GitHub Copilot OAuth (#34779), Snowflake Cortex (#34780), xAI Grok SuperGrok subscription (#34778), and OpenAI/ChatGPT (#34765 tracking issue). Enterprise users need these for production adoption.

3. **Progressive Instructions** – The `AGENTS.md` redesign (#34341) is the leading architecture request. Users want durable, path-scoped instructions that survive compaction and session boundaries—a key design requirement for codebase-aware AI assistants.

4. **Session Management APIs** – Parent session filtering (#34936), session resume after crash (#35646), and optimistic follow-up prompts (#34766) reflect demand for robust session lifecycle management in V2.

---

## Developer Pain Points

- **macOS Terminal Rendering (Chronic)** – The cluster of 5+ closed issues (#6823, #4461, #20584, #10054, #4721, #6923) all relate to invisible text or broken themes in macOS Terminal. Despite repeated fixes, the problem reappears across different hardware generations and versions. Suggests a systemic terminal capability detection issue.

- **V2 Plugin Gaps (Growing)** – Plugins registered via the V2 API are not discoverable via `/skills` (#33896), and provider login methods are missing (#34779, #34778, #34780). Plugin authors are hitting hard walls trying to migrate from V1.

- **Enterprise Model Frustration** – #34030 captures a clear enterprise pain: GitHub Copilot Enterprise users with custom third-party models cannot use them via OpenCode. This blocks enterprise pilots and trials.

- **Session/Durability Fragility** – Multiple issues around V2 session behavior: empty plugin generation race (#35556), blank route flash (#32535), cost tracking gaps (#30706), and recovery after crash (#35646). The V2 runtime is still maturing its durability guarantees.

- **Metadata/State Leakage** – Provider metadata namespaces being lost (#35817), stale tool preparation state overwriting fresh data (#35796/#35453), and directory attachments failing provider turns (#34821)—developers are hitting subtle state management bugs in the V2 stack.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-08

## Today's Highlights
A surge of triage activity closed 18+ issues in the last 24 hours, spanning edge-case reliability (read-only configs, session-ID mismatches) and a long‑tail of provider‑compatibility patches. The community pushed several doc‑only PRs to fix extension‑discovery paths, while core maintainer @xl0 landed a batch of 15+ merged PRs — including stable streaming code‑fence rendering and extension stats export.

## Releases
No new releases in the last 24 hours.

## Hot Issues (Top 10 Noteworthy)

1. **[#6234 – Escape leaves Pi stuck in Working when an extension context hook never settles](https://github.com/earendil-works/pi/issues/6234)** *(Open, 10 💬)*  
   Pressing `Escape` twice can fail to abort a run because the first Escape is swallowed by the streaming‑abort path. The second Escape finds the extension hook still pending, leaving the TUI frozen in `Working...`. Community is asking for a hard timeout on extension hooks.

2. **[#6206 – Clamping to context window prevents artificial context limits](https://github.com/earendil-works/pi/issues/6206)** *(Open, 5 💬)*  
   A previous fix (commit `09f1059`) clamps `max_tokens` to the provider’s reported context window. This breaks user‑configured artificial limits that are *smaller* than the window. @DanielThomas argues the fix should only cap, not floor.

3. **[#6210 – `/scoped-models` cannot select model ids containing brackets](https://github.com/earendil-works/pi/issues/6210)** *(Open, 5 💬)*  
   Models with brackets in their ID (e.g. `custom/bracketed-model[1m]`) are rejected by pattern matching. Caused by the selector treating brackets as a regex pattern.

4. **[#6395 – README `/reload` command description inconsistent](https://github.com/earendil-works/pi/issues/6395)** *(Open, 2 💬)*  
   The README says `/reload` only reloads keybindings/themes, but the actual code reloads extensions, skills, prompts, and context files as well. Simple doc‑fix request with moderate community interest.

5. **[#6326 – `custom_message` entries bypass compaction keepRecentTokens budgeting](https://github.com/earendil-works/pi/issues/6326)** *(Open, 2 💬)*  
   Custom messages (e.g. system prompts injected by extensions) still count toward LLM context even when compaction should have dropped them. This inflates token usage and can trigger context‑length errors.

6. **[#6378 – “nothing I can do to fix this error” (context length exceeded)](https://github.com/earendil-works/pi/issues/6378)** *(Open, 2 💬)*  
   A user hit a 262k‑token limit with a request of 263k tokens. The error message suggests using the “context‑compression plugin,” which may not exist or is poorly documented. Indicates a UX gap in error messaging.

7. **[#6367 – `modelOverrides` does not apply to extension‑registered providers](https://github.com/earendil-works/pi/issues/6367)** *(Open, 2 💬)*  
   `thinkingLevelMap` overrides in `models.json` are ignored when the provider is registered via `pi.registerProvider`. Cycling thinking levels via Shift+Tab does not respect the override.

8. **[#6167 – `transformMessages` + `isSameModel === false` interacts poorly with `requiresReasoningContentOnAssistantMessages`](https://github.com/earendil-works/pi/issues/6167)** *(Open, 1 💬)*  
   When switching models, thinking‑content inlining logic clashes with the compat flag that expects the original structure. Causes malformed assistant messages on model switches.

9. **[#6406 – Read‑only `~/.pi/agent` fails every credential read](https://github.com/earendil-works/pi/issues/6406)** *(Closed, 1 💬)*  
   Pi locks `auth.json` even for reads. On a read‑only filesystem, the lock‑creation fails silently, producing “No API key found” despite the file being present and readable. Fixed swiftly after report.

10. **[#6404 – Documented `shellCommandPrefix` alias‑loading pattern breaks on multi‑line aliases](https://github.com/earendil-works/pi/issues/6404)** *(Closed, 1 💬)*  
    The recommended `shopt -s expand_aliases; eval "$(grep '^alias ' ~/.bashrc)"` works fine for single‑line aliases but fails on multi‑line ones. Docs need updating to use `type -a` or `alias` without `grep`.

## Key PR Progress (Top 10 Important)

1. **[#5846 – fix(tui): stabilize streaming code fence rendering](https://github.com/earendil-works/pi/pull/5846)** *(Merged)*  
   @xl0 landed a fix for code‑fence flickering during streaming. Closes long‑standing issue #5825.

2. **[#5711 – feat(coding-agent): add extension prompt guideline API](https://github.com/earendil-works/pi/pull/5711)** *(Merged)*  
   Extensions can now declare prompt guidelines that are injected into the system prompt. Addresses #5710.

3. **[#6063 – Extension stats](https://github.com/earendil-works/pi/pull/6063)** *(Merged)*  
   Exposes per‑extension timing/call‑count stats. Also fixes OSC garbage printed after benchmark runs. Closes #6062.

4. **[#6175 – fix(coding-agent): emit session name changes to extensions](https://github.com/earendil-works/pi/pull/6175)** *(Merged)*  
   Extensions now receive events when the session name changes, allowing them to update UI or logs. Closes #6174.

5. **[#6405 – Update extensions documentation to point to npm/git installation locations](https://github.com/earendil-works/pi/pull/6405)** *(Merged)*  
   A doc‑focused PR that adds explicit paths for npm‑ and git‑installed extensions, addressing the frequent “extension not found” confusion reported in #6400.

6. **[#5085 – Expose full tool definitions from `getAllTools`](https://github.com/earendil-works/pi/pull/5085)** *(Merged)*  
   Extensions now receive a read‑only copy of every tool’s full JSON Schema definition, enabling richer UIs and validation.

7. **[#5756 – Expose edit‑diff for extensions](https://github.com/earendil-works/pi/pull/5756)** *(Merged)*  
   Extensions can now access the diff produced by the edit tool, enabling custom diff viewers or analytics.

8. **[#4775 – Export image resize utilities](https://github.com/earendil-works/pi/pull/4775)** *(Merged)*  
   `resizeImage` and related utilities are now public for extension authors to use in custom tools.

9. **[#5167 – Export `convertToPng` for extensions](https://github.com/earendil-works/pi/pull/5167)** *(Merged)*  
   Screenshot tools and image‑processing extensions can now reuse Pi’s PNG conversion logic.

10. **[#5202 – Export CLI argument parser](https://github.com/earendil-works/pi/pull/5202)** *(Merged)*  
    Extension authors can now reuse Pi’s argument‑parsing logic, enabling consistent flag handling in custom tools.

## Feature Request Trends

- **First‑class provider additions** – Multiple requests to add Eden AI (#6403) and fix provider‑specific quirks (GLM via Fireworks #6259, GLM via NVIDIA NIM #6226, Kimi‑K2.7 via DeepInfra #6399). The community wants easier provider onboarding.
- **Extension loading performance** – Issue #6360 proposes a three‑tier loading strategy (lazy/async/sync) to avoid startup slowdowns with 30+ extensions. Gained traction quickly.
- **Custom session metadata** – Request #6402 asks for opaque `metadata` in JSONL session headers, enabling richer session annotations without breaking storage.
- **No‑session mode in `-r`** – Issue #6401 requests the ability to start a stateless agent even when Pi is launched with `pi -r` (restore), useful for embedding in third‑party tools.
- **Inline settings factories** – Issue #6398 asks for `main()` to accept inline settings factories, making it easier to build CLI harnesses on top of Pi’s SDK.

## Developer Pain Points

- **Extension discovery failures** – Repeated reports (#6400, #6408, #6318) that Pi cannot find extensions installed via npm or git. The root cause is a mismatch between documented paths and actual installation locations.
- **Read‑only filesystem compatibility** – Issue #6406 revealed that Pi’s aggressive file‑locking even for reads breaks on read‑only configs. A usability regression for containerized or CI environments.
- **Model‑switching artifacts** – Multiple issues (#6167, #6226, #6409) around thinking‑content normalization and `finish_reason` handling when switching between reasoning and non‑reasoning models. Fixed incrementally but still a common friction point.
- **Context‑window confusion** – Issues #6206 and #6378 highlight that users often can’t tell whether a limit is from the provider or Pi’s own clamping logic. Better error messages and configurable limits remain a high‑frequency request.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-07-08

## Today's Highlights
Active development continues on the Qwen Code daemon architecture, with significant work on session management, multi-workspace support, and memory isolation. A new nightly release (v0.19.7-nightly) addresses PR gate stability, while the community is increasingly focused on memory corruption bugs and Windows compatibility issues. The top-voted feature request for sub-agent parallel limits and the WeCom channel integration both show community demand for enterprise deployment scenarios.

## Releases
- **v0.19.7-nightly.20260708.394c1a289** – Latest nightly release. Change: adds WeCom to channels overview (docs). [Changelog](https://github.com/QwenLM/qwen-code/compare/v0.19.7-nightly.20260708.394c1a289)
- **v0.19.6-preview.0** – Preview release. Same channels documentation update. [Changelog](https://github.com/QwenLM/qwen-code/compare/v0.19.6-preview.0)
- **v0.19.7** – Stable release. Key fixes: strengthened PR gate with batch detection and problem existence check (#5723), plus review functionality improvements. [Changelog](https://github.com/QwenLM/qwen-code/compare/v0.19.7)

## Hot Issues (10 noteworthy)

1. **#6378 – RFC: Multiple workspaces in one daemon** – [OPEN]  
   Proposes `1 daemon = N workspaces` model. 19 comments, strong community interest in multi-project workflows. Heavy discussion about backward compatibility.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/6378)

2. **#6264 – `/review` consumes excessive tokens** – [OPEN]  
   Users report the review skill uses surprisingly large token counts. 8 comments; community is sharing screenshots of usage stats and asking for configurable token budgets.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/6264)

3. **#6312 – Reduce per-session overhead on daemon** – [OPEN]  
   Tracking issue for optimizing daemon session creation—shared event loops running repeated I/O. 5 comments; core team is actively analyzing performance traces.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/6312)

4. **#6298 – Windows: shell tool fails on stdout output** – [CLOSED, fixed]  
   `run_shell_command` pipes through `cat` which doesn't exist on Windows `cmd.exe`. Fixed; community relief was palpable.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/6298)

5. **#6265 – `tool_search` invalidates KV-cache on deferred tool load** – [CLOSED, fixed]  
   Every deferred-tool load was flushing the LLM's KV cache, causing expensive recomputation. Fixed; marked `welcome-pr`.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/6265)

6. **#6384 – "hard limit: 0" error with context window models** – [OPEN]  
   Model reserves full default context for output, causing "hard limit: 0" failures before any request is sent. 5 comments; users hitting this on large context models.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/6384)

7. **#6318 – Unable to `/rewind` after `/compress`** – [CLOSED, fixed]  
   Even rewinding to a pre-compression position fails. Fixed; `welcome-pr` label suggests maintainers encourage community patches.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/6318)

8. **#5176 – Sub-agent max parallel count setting** – [CLOSED, feature request]  
   Request to limit parallel sub-agents and queue the rest. **1 👍** – the only issue with positive reaction votes this digest period.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/5176)

9. **#6414 – VSCode "Failed to connect to Qwen agent"** – [OPEN]  
   New bug: VSCode extension cannot connect to Qwen agent. 3 comments; likely environment-specific but concerning for IDE users.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/6414)

10. **#6449 – Worktree sessions share project memory** – [OPEN]  
    Memory pollution: separate worktrees write into the same project memory, causing noise for LLM. 2 comments; design discussion on isolation vs. sharing.  
    [Issue](https://github.com/QwenLM/qwen-code/issues/6449)

## Key PR Progress (10 important)

1. **#6482 – Bounded replay snapshot history** – [OPEN]  
   Prevents unbounded memory growth in daemon sessions by capping replay buffer size. Core infrastructure change.  
   [PR](https://github.com/QwenLM/qwen-code/pull/6482)

2. **#6446 – Relay ACP permission requests through channels** – [OPEN]  
   Routes permission requests to chat instead of auto-approving. Critical for enterprise channel deployments (WeCom, DingTalk).  
   [PR](https://github.com/QwenLM/qwen-code/pull/6446)

3. **#6483 – Reject Windows-style workspace artifact paths** – [OPEN]  
   Security hardening: prevents `record_artifact` from accepting Windows absolute paths on Linux.  
   [PR](https://github.com/QwenLM/qwen-code/pull/6483)

4. **#6492 – SDK control request methods** – [OPEN]  
   Consolidates 4 control features: effort, model switching, usage, context—across Python and TypeScript SDKs.  
   [PR](https://github.com/QwenLM/qwen-code/pull/6492)

5. **#6421 – Fix streaming-table rendering defects** – [OPEN]  
   Fixes scroll-to-top lock, stall-then-dump, and header flash in the CLI streaming table. Follow-up to #6345.  
   [PR](https://github.com/QwenLM/qwen-code/pull/6421)

6. **#6489 – MessageDisplay hook for mid-turn streaming** – [OPEN]  
   New hook event that fires during streaming (not just at Stop). Enables IDE real-time reply display. Closes #6488.  
   [PR](https://github.com/QwenLM/qwen-code/pull/6489)

7. **#6416 – Daemon env isolation and admission control** – [CLOSED, merged]  
   Phase 2a guardrails for multi-workspace sessions: env snapshots, workspace-scoped config, ACP admission control.  
   [PR](https://github.com/QwenLM/qwen-code/pull/6416)

8. **#6481 – Fix release versioning for missing NPM dist-tags** – [OPEN]  
   Fixes #6476 release failure when no NPM dist-tag exists for requested channel.  
   [PR](https://github.com/QwenLM/qwen-code/pull/6481)

9. **#6493 – Web Shell daemon session counting** – [OPEN]  
   Makes Daemon Status dashboard count daemon sessions instead of only `usage_record.jsonl` entries.  
   [PR](https://github.com/QwenLM/qwen-code/pull/6493)

10. **#3170 – Use official LSP SDK for real-time diagnostics** – [OPEN]  
    Integrates `vscode-languageserver-protocol` SDK and implements `didSave` for instant diagnostics. Long-running PR (3 months).  
    [PR](https://github.com/QwenLM/qwen-code/pull/3170)

## Feature Request Trends
- **Multi-workspace daemon** (#6378) – The dominant architectural request. Users want one daemon to serve multiple projects without restarting.
- **Channel expansions** – WeCom (#6208), DingTalk interactive cards (#6443), and QQ bot group handling (#6457) show strong demand for enterprise messaging integrations.
- **Memory isolation** (#6449, #6487) – Multiple requests for worktree-scoped memory, stale index fixes, and better auto-memory separation.
- **Model toggling** (#6442, #6486) – Quick hotkey to switch between two preconfigured models gains traction (Alt+S/Ctrl+F).
- **SKILL workflow enhancements** (#6452) – Chinese-language feature request for more robust "prompt as code" workflow handling, including cross-model consistency.

## Developer Pain Points
1. **Memory management failures** – Memory index goes stale after `/remember`; content lost on compaction; worktree sessions pollute shared memory (#6449, #6487, #6311).
2. **Windows compatibility** – Shell tool fails on `cmd.exe` (#6298); extension install failures on Windows (#6334). Classic cross-platform challenges.
3. **Token consumption surprises** – `/review` skill uses unexpectedly large token counts (#6264); PDF reads overflow context (#6408).
4. **Context window edge cases** – "hard limit: 0" errors when models reserve full context for output (#6384); large PDF/text file reading causes context overflow (#6408).
5. **Session lifecycle bugs** – Daemon session list reorders after loading named sessions (#6438); auto-title polluted by startup context (#6419); `/rewind` broken after `/compress` (#6318).
6. **Authentication friction** – OAuth URLs hard-wrapped across multiple lines in non-interactive mode (#6428); subscription not working for some users (#6477, #6475).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-08

## Today's Highlights
The project has officially rebranded to **CodeWhale** with the release of **v0.8.67**, deprecating the legacy `deepseek-tui` npm package. The maintainer has published a detailed execution board for the v0.8.68 milestone (#4092), organizing work into labeled lanes for agent-driven development. Two critical stability fixes shipped: a fix for the sub-agent detail panel being blank/freezing (#4094) and a normalization of raw Ctrl+C handling in PTY mode (#4090).

## Releases
- **v0.8.67** — *CodeWhale* becomes the canonical project name, command, npm package, and release-asset name. The legacy `deepseek-tui` npm package is deprecated and receives no further releases. Users on v0.8.x legacy names should follow `docs/REBRAND.md` for migration.

## Hot Issues (10 selected from 50)

1. **#2487** — *Frequent error: "Turn stalled - no completion signal received"* [CLOSED]  
   Community: 20 comments, high visibility. The `yolo` mode freezes unresponsively; sending `continue` fails to resume. A major reliability pain point.  
   [Hmbown/CodeWhale Issue #2487](https://github.com/Hmbown/CodeWhale/issues/2487)

2. **#3144** — *Natural-language auto-review policy and pre-push review gate* [CLOSED]  
   Community: 14 comments. Proposes a Cursor-inspired middle ground between manual approvals and unchecked autonomous execution—signals a growing demand for safety in agentic workflows.  
   [Hmbown/CodeWhale Issue #3144](https://github.com/Hmbown/CodeWhale/issues/3144)

3. **#3063** — *v0.8.59 release tracker: TUI mouse-report leak, runtime safety* [CLOSED]  
   Community: 11 comments. Release-blocker that tracked the TUI mouse-report input leak on macOS, plus the broader issue/PR queue. Represents a pattern of structured release management.  
   [Hmbown/CodeWhale Issue #3063](https://github.com/Hmbown/CodeWhale/issues/3063)

4. **#1812** — *TUI-freeze-Windows-crossterm-poll* [CLOSED]  
   Community: 11 comments, 1 👍. Windows 11 users report intermittent complete UI freeze (process alive but unresponsive) with two confirmed event captures. A long-standing Windows stability issue.  
   [Hmbown/CodeWhale Issue #1812](https://github.com/Hmbown/CodeWhale/issues/1812)

5. **#4092** — *v0.8.68 execution board: lane order, dependencies, and agent protocol* [OPEN]  
   Community: 10 comments. The canonical entry point for agents working on v0.8.68; replaces the July 7 triage packet. Demonstrates highly organized, lane-based milestone management.  
   [Hmbown/CodeWhale Issue #4092](https://github.com/Hmbown/CodeWhale/issues/4092)

6. **#2300** — *Multi-model compatibility, provider docs, automatic Fleet loadout selection* [CLOSED]  
   Community: 8 comments. Users request clearer documentation for provider/model routing (vLLM vs OpenAI) and automatic loadout. Highlights growing need for multi-provider support.  
   [Hmbown/CodeWhale Issue #2300](https://github.com/Hmbown/CodeWhale/issues/2300)

7. **#4094** — *Sub-agent detail panel is empty and can freeze the TUI* [OPEN]  
   Community: 4 comments. Critical UX bug found during dogfooding—opening a running sub-agent's detail shows almost no information and can freeze the interface.  
   [Hmbown/CodeWhale Issue #4094](https://github.com/Hmbown/CodeWhale/issues/4094)

8. **#2261** — *TUI crash: input leaks to PowerShell terminal* [CLOSED]  
   Community: 6 comments. Windows 10/11 issue where after several turns, input focus is lost and keystrokes are executed by PowerShell instead of the TUI. Severe UX regression.  
   [Hmbown/CodeWhale Issue #2261](https://github.com/Hmbown/CodeWhale/issues/2261)

9. **#1835** — *Windows: Input field completely unresponsive (IME composition deadlock)* [CLOSED]  
   Community: 5 comments, 1 👍. Chinese IME (Sogou) users cannot type at all. Signals a systemic Windows input handling problem.  
   [Hmbown/CodeWhale Issue #1835](https://github.com/Hmbown/CodeWhale/issues/1835)

10. **#2953** — *Slim the default prompt path toward Codex-parity input tokens* [CLOSED]  
    Community: 4 comments. CodeWhale's base prompt is significantly larger than Codex CLI's, raising token cost. Part of a broader token-efficiency push across multiple issues.  
    [Hmbown/CodeWhale Issue #2953](https://github.com/Hmbown/CodeWhale/issues/2953)

## Key PR Progress (10 selected from 23)

1. **#4181** — *fix(tui): Fleet setup role/profile roster editor* [OPEN]  
   Aligns Fleet setup with role/profile editing instead of a provider-scoped model picker. Persists unambiguous provider+model route identity.  
   [Hmbown/CodeWhale PR #4181](https://github.com/Hmbown/CodeWhale/pull/4181)

2. **#4189** — *fix(ci): only auto-label agent-ready on issue open* [CLOSED]  
   Prevents the auto-label step from re-adding `agent-ready` when a triage pass deliberately removed it. CI hygiene improvement.  
   [Hmbown/CodeWhale PR #4189](https://github.com/Hmbown/CodeWhale/pull/4189)

3. **#4182** — *fix(tui): populate sub-agent detail panel with live activity* [CLOSED]  
   Fixes #4094: now shows live activity trail, tool calls with status, and final summary/handoff for completed workers. Bounded and truncated to avoid overflow.  
   [Hmbown/CodeWhale PR #4182](https://github.com/Hmbown/CodeWhale/pull/4182)

4. **#4180** — *fix(tui): normalize raw Ctrl+C byte for PTY quit-arm flow* [CLOSED]  
   Fixes #4090: ETX (0x03) control bytes are now normalized to canonical Ctrl+C before routing. Includes regression tests.  
   [Hmbown/CodeWhale PR #4180](https://github.com/Hmbown/CodeWhale/pull/4180)

5. **#4163** — *feat(workflows): v0.8.68 agent execution lanes and milestone sync* [CLOSED]  
   Adds wave-based agent workflow files, a playbook with `gh` commands, and a milestone-sync GitHub Action. Structured the entire v0.8.68 release cadence.  
   [Hmbown/CodeWhale PR #4163](https://github.com/Hmbown/CodeWhale/pull/4163)

6. **#4099** — *0.8.68 train: workflow correctness, TUI stability, modes & permissions, security hardening* [CLOSED]  
   Six-commit release train covering completion polling fails-closed behavior, cancel interruption, sub-agent API scoping, and multiple TUI stability fixes.  
   [Hmbown/CodeWhale PR #4099](https://github.com/Hmbown/CodeWhale/pull/4099)

7. **#4098** — *docs(constitution): add anti-polling rule for sub-agent waiting strategy* [OPEN]  
   Proposes a constitutional rule to prevent wasteful peek-sleep polling loops; parents should passively wait for `subagent_completion` events.  
   [Hmbown/CodeWhale PR #4098](https://github.com/Hmbown/CodeWhale/pull/4098)

8. **#3902** — *perf(tui): fix the five render/input hot paths (#3896–#3900)* [OPEN]  
   Fixes five performance-labeled issues: redundant sidebar computation, excessive String cloning, layout calculation in hot path, and more. Adversarial multi-agent review caught four regressions.  
   [Hmbown/CodeWhale PR #3902](https://github.com/Hmbown/CodeWhale/pull/3902)

9. **#4045** — *fix edit_file UTF-8 fuzzy cursor panic* [CLOSED]  
   Fixes a panic when fuzzy matching starts on a multibyte UTF-8 character. Advances normalized cursor to the next valid character boundary.  
   [Hmbown/CodeWhale PR #4045](https://github.com/Hmbown/CodeWhale/pull/4045)

10. **#4088** — *fix(tui): preserve native selection without mouse capture* [CLOSED]  
    Fixes #4026: leaves alternate-scroll mode off when mouse capture is disabled, so the host terminal fully owns drag selection.  
    [Hmbown/CodeWhale PR #4088](https://github.com/Hmbown/CodeWhale/pull/4088)

## Feature Request Trends

- **Multi-model & provider flexibility** — Multiple issues (#2300, #3932–#3935) request better provider routing, automatic Fleet loadout selection, and clear documentation for vLLM vs OpenAI. The community wants vendor-agnostic model orchestration.
- **Sub-agent orchestration & visibility** — Strong demand for live sub-agent monitoring (#4094), anti-polling strategies (#4098), tool scoping (#4042), and fallback strategies when tool calls fail (#1641). Users want autonomous agents they can observe and trust.
- **Cache-maximalist / token efficiency** — Issues #528, #2953, #2956, and #2957 push for re-reading active files instead of summarizing, reducing repeated transcript payload, and slimming the default prompt. Cost-conscious developers want Codex-parity token usage.
- **Workflow as a first-class concept** — The v0.9.0 WhaleFlow EPIC (#2981) and related issues (#2973, #2979, #2791) show a community ready for structured, async workflow execution with branch/leaf patterns and TUI monitoring surfaces.
- **Security & review gates** — #3144 and #2061 (Hotbar) reflect a desire for configurable approval policies, pre-push review, and quick-action surfaces that improve safety and workflow speed without silent autonomy.

## Developer Pain Points

1. **Windows stability crisis** — Issues #1812, #2261, #1835, and #1472 all describe complete UI freezes, input focus loss, IME deadlocks, and unrecoverable hangs on Windows. This is the single largest cluster of reliability complaints, with deep root causes in crossterm poll, pipe deadlocks, and focus management.

2. **Token cost in benchmark/exec runs** — #2953, #2956, and #2957 all measure CodeWhale's token usage against Codex CLI and find it significantly higher. Developers are frustrated by unnecessary input-token burn from repeated transcript payloads and overly verbose base prompts.

3. **Stalled turns and non-responsive agents** — #2487 (20 comments) is the top-voted issue: the "no completion signal" error in `yolo` mode freezes operations entirely, with `continue` failing to resume. This erodes trust in autonomous mode.

4. **Sub-agent observability gaps** — #4094 (TUI freeze + blank panel), #4098 (polling loops), and #1641 (no fallback on tool failure) collectively show that sub-agents are a black box. Developers cannot inspect, debug, or trust what agents are doing without risky polling or UI freezes.

5. **Cross-platform input handling** — The combination of macOS mouse-report leaks (#3063), Windows IME deadlocks (#1835), PowerShell input leakage (#2261), and PTY Ctrl+C normalization (#4090) reveals a fragmented terminal handling layer that requires continuous per-platform fixes.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*