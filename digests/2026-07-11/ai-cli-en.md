# AI CLI Tools Community Digest 2026-07-11

> Generated: 2026-07-11 01:20 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem Cross-Comparison Report — 2026-07-11

## 1. Ecosystem Overview

The AI CLI tools ecosystem is experiencing rapid convergence around multi-agent orchestration, cost governance, and platform reliability. All major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI—are shipping multiple releases weekly, with agentic workflows and subagent lifecycle management emerging as the dominant architectural challenge. A clear pattern of community demand for session persistence, cross-platform parity, and model flexibility spans every tool, while each vendor differentiates through proprietary model integration, security posture, and TUI sophistication. The ecosystem is maturing from novelty to production-critical infrastructure, with billing-impacting bugs and data loss issues attracting the highest community urgency.

## 2. Activity Comparison

| Tool | Hot Issues (Active) | PRs (Last 24h) | Release Status | Notable Community Signal |
|------|-------------------|----------------|----------------|--------------------------|
| **Claude Code** | 10 | 10 | 2 releases (v2.1.206, v2.1.207) | 792 comments on #38335 (session quota bug) |
| **OpenAI Codex** | 10 | 10 | 2 alpha releases (0.145.0-alpha.3/.4) | 283 👍 on #30364 (reasoning-token clustering) |
| **Gemini CLI** | 10 | 10 | Nightly v0.52.0-nightly | 8 👍 on #21409 (agent hangs) |
| **GitHub Copilot CLI** | 10 | 1 | 2 releases (v1.0.71-0, v1.0.70) | 17 👍 on #3709 (BYOK model selection) |
| **Kimi Code CLI** | 10 | 10 | No new release | P0 bug #2478 (/init corrupts tool bindings) |
| **OpenCode** | 10 | 10 | No new release | 89 👍 on #10288 (mobile version request) |
| **Pi** | 10 | 10 | Stable v0.80.6 | 17 👍 on #6097 (max thinking level) |
| **Qwen Code** | 10 | 10 | v0.19.9 released | 20 comments on #6378 (multi-workspace RFC) |
| **DeepSeek TUI (CodeWhale)** | 10 | 10 | No new release (v0.8.68 stabilization) | 60 comments on #4092 (execution board) |

**Key Insight:** All tools are shipping at least weekly releases. Claude Code and GitHub Copilot CLI lead in release cadence (2 releases each in 24h). Kimi Code CLI and OpenCode are in active development without recent releases. DeepSeek TUI is in a stabilization phase for v0.8.68.

## 3. Shared Feature Directions

| Requirement | Appearing In | Specific Needs |
|-------------|-------------|----------------|
| **Subagent lifecycle governance** | Claude Code, OpenAI Codex, Gemini CLI, OpenCode, Qwen Code, DeepSeek TUI | Depth limits on recursion (#68110), selective kill instead of all-or-nothing (#21167), per-subagent cancellation, timeout configuration |
| **Session persistence across restarts** | Kimi Code CLI (#2401), Qwen Code (#6695, #6680), Gemini CLI, DeepSeek TUI | Conversation survival after process kill, session recovery after daemon restart |
| **Windows platform parity** | Claude Code (#14828, #74649), OpenAI Codex (#20214, #32040), Gemini CLI (#28348), Kimi Code CLI (#2415), Pi (#6300), OpenCode (#35828) | ANSI color support, path separator handling, TUI stability, package manager integration |
| **Multi-model/provider flexibility** | OpenAI Codex (#31814), GitHub Copilot CLI (#3709), Kimi Code CLI (#2461), Pi (#6475), DeepSeek TUI (#4334) | Mid-session model switching, BYOK/local provider selection without re-authentication |
| **Cost transparency & billing guardrails** | Claude Code (#38335, #68110), OpenAI Codex (#31668, #31606), Gemini CLI, DeepSeek TUI (#4335) | Live token counters per subagent, rate-limit reliability, budget warnings before unbounded operations |
| **MCP server robustness** | Claude Code, OpenAI Codex (#31359), GitHub Copilot CLI (#4085–#4089) | Graceful degradation on server failure, OAuth flow reliability, connection timeout handling |
| **Agent safety & compliance** | Gemini CLI (#22672), DeepSeek TUI (#4032), OpenCode (#2632) | Prefer safer command alternatives, respect user-provided constraints, permission-aware defaults |
| **Export & documentation** | Kimi Code CLI (#2420), Pi (#6505), OpenCode | Markdown/JSON session export, conversation sharing, structured output for note-taking |
| **Mobile/Web UI** | OpenCode (#10288, 89 👍), Qwen Code (Web Shell improvements), DeepSeek TUI (Android/Termux #4236) | Mobile coding assistance, browser-based TUI, native Android support |
| **Event listener & memory management** | Gemini CLI (#28313), Pi (#6501, #6303) | MaxListenersExceededWarning fixes, unbounded retry capping, embedded library lifecycle |

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|-------------------|-----------|----------|-----|-----------|---------------|
| **Primary model** | Claude (Opus/Sonnet/Fable) | GPT-5.x (Sol/Terra/Luna) | Gemini | GPT + Copilot | Kimi models | Multi-provider | Multi-provider | Qwen | DeepSeek + Multi-provider |
| **Key differentiator** | Auto mode GA, deep agent recursion | OSS-first, subagent environment control | Privacy-first (thought scrubbing) | GitHub ecosystem integration | Plan-mode tooling | V2 TUI, CodeMode sandbox | Constrained sampling, embedding support | Multi-workspace daemon | Fleet/Workflow/Lane orchestration |
| **Target user** | Power developers, enterprise | Open-source developers | Google Cloud/Workspace users | GitHub ecosystem users | East Asian developers | Full-stack devs | Self-hosters | Enterprise teams | Privacy-conscious devs |
| **Security posture** | Security-guidance plugin, permission system | Subagent environment restrictions | A2A path traversal fixes, prompt injection sanitization | Custom HTTP headers for enterprise | Basic | Default "allow all" (controversial) | Constrained sampling, embedded library isolation | Protocol compliance guards | Constitution enforcement, cargo-audit |
| **TUI maturity** | High (scroll-only mode requests) | Medium (Windows stutters) | Medium | Medium (wedge issues) | Low (basic CLI) | High (V2 polish cycle) | Low (Windows broken) | Medium (Web Shell push) | Medium (Fleet model complex) |
| **Windows support** | Poor (console flash, Cowork broken) | Poor (freezes, crashes, hangs) | Poor (auth loop) | Poor (wedge, black screen) | Broken (ANSI, paths) | Poor (startup crash) | Broken (input rendering) | N/A | N/A |
| **Open-source status** | Proprietary (PR #41447 pending) | OSS | OSS | Proprietary | OSS | OSS | OSS | OSS | OSS |

**Key Insight:** Claude Code dominates in TUI polish and auto-mode capabilities but suffers from cost governance crises. OpenAI Codex leads in model variety and OSS contribution infrastructure. Gemini CLI differentiates through privacy engineering and security hardening. GitHub Copilot CLI leverages GitHub ecosystem lock-in. Kimi Code, OpenCode, Pi, Qwen Code, and DeepSeek TUI are OSS alternatives with distinct architectural philosophies—Qwen Code's multi-workspace daemon and DeepSeek TUI's Fleet orchestration model represent the most novel architectural approaches.

## 5. Community Momentum & Maturity

| Tool | Community Size Indicator | Iteration Velocity | Issue Resolution Responsiveness | Risk Level |
|------|------------------------|-------------------|--------------------------------|------------|
| **Claude Code** | Very High (792 comments on #38335) | Very High (2 releases/day) | Medium (key issues open for months) | **Critical** — billing crisis (#38335) and unbounded cost (#68110) |
| **OpenAI Codex** | High (283 👍 on #30364) | High (2 alpha releases) | Medium-High (PRs merge within days) | High — billing regressions (#31668) |
| **Gemini CLI** | Medium (20 comments on #6378 as highest) | High (nightly releases) | High (10 security PRs merged today) | Medium — subagent reliability |
| **GitHub Copilot CLI** | Medium (17 👍 on #3709) | High (2 releases in 2 days) | Low (1 PR active, slow on bugs) | High — MCP OAuth cluster, voice mode broken |
| **Kimi Code CLI** | Low (10 max comments) | Medium (no release today, 10 PRs open) | High (2 critical fix PRs today) | Medium — shared-state corruption (#2478) |
| **OpenCode** | High (89 👍 on mobile request) | Medium (no release, 10 PRs) | High (V2 TUI fixes merging rapidly) | Medium — SQLite corruption, security defaults |
| **Pi** | Medium (17 👍 on #6097) | High (6 PRs merged, 10 active) | High (critical timeout fix in PR #6503) | Medium — regression in v0.80.6 |
| **Qwen Code** | Medium (20 comments on RFC) | High (v0.19.9 released, 10 PRs) | High (fix PRs open same day as issues) | Low — stream timeout regression |
| **DeepSeek TUI** | Low (60 comments internal coordination) | Medium (v0.8.68 stabilization) | High (stopship batch PR merged) | Low — stabilization phase |

**Key Insight:** Claude Code has the largest community but the highest crisis risk. OpenAI Codex and Gemini CLI show the strongest PR/issue ratio. DeepSeek TUI and Qwen Code are rapidly maturing with disciplined release processes. GitHub Copilot CLI shows the slowest issue resolution velocity relative to community size.

## 6. Trend Signals

### For Technical Decision-Makers

1. **Cost governance is the #1 unsolved problem.** Claude Code's #38335 (468 👍, 792 comments) and #68110 (unbounded sub-agent recursion) represent existential risks for enterprise adoption. Any tool lacking budget controls, token counters, or recursion limits is unsuitable for production deployment at scale.

2. **Multi-agent orchestration is the new frontier.** Every major tool is investing in subagent lifecycle management, but none has solved reliability. Users report hanging agents, false success reports, and runaway costs. The tools that solve "controlled parallelism" will win enterprise trust.

3. **Cross-platform parity is table stakes.** Windows and Linux support remains visibly broken across all tools. Any vendor targeting enterprise adoption must prioritize Windows TUI stability, as Windows holds 70%+ developer desktop share in regulated industries.

4. **MCP protocol maturity is accelerating.** With OAuth failures, brittle connections, and tool exposure bugs across multiple tools, MCP interoperability is a pain point. The ecosystem needs standardized MCP client resilience patterns—graceful degradation, retry logic, and server health checks.

5. **Privacy engineering is a differentiator.** Gemini CLI's thought scrubbing, path traversal fixes, and prompt injection sanitization set a benchmark. As AI tools gain access to proprietary codebases, security-hardened tools will command premium adoption.

6. **OSS tools are catching up.** OpenCode, Qwen Code, and DeepSeek TUI are shipping production-quality features (CodeMode sandbox, multi-workspace daemon, Fleet orchestration) that rival proprietary tools. The gap between OSS and proprietary AI CLI tools is narrowing rapidly.

7. **Mobile and web UI demand is underestimated.** OpenCode's #10288 (89 👍 for mobile version) and Qwen Code's Web Shell investment signal that developers want AI coding assistance beyond the terminal. This is an underserved market with high growth potential.

### For Developers

- **Avoid tools without cost governance** for agentic workflows—Claude Code's ongoing crisis is a cautionary tale.
- **Prioritize tools with active OSS communities** (OpenCode, Qwen Code, DeepSeek TUI) for transparency and rapid bug fixes.
- **Budget for cross-platform friction**—no tool delivers parity across macOS, Windows, and Linux.
- **Invest in MCP server redundancy**—single points of failure in external tool connections can block entire workflows.
- **Watch for open-sourcing moves**—Claude Code's #41447 (OSS PR, 3+ months open) could reshape the competitive landscape overnight.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report for the anthropics/skills repository.

## Claude Code Skills Community Highlights Report (Data as of 2026-07-11)

### 1. Top Skills Ranking

The following are the most-discussed Pull Requests (PRs) based on community engagement, representing the highest level of current activity and interest.

1.  **Fix: `run_eval.py` reports 0% recall** ([PR #1298](https://github.com/anthropics/skills/pull/1298))
    - **Functionality:** Fixes the core `run_eval.py` script used by `skill-creator` to evaluate skill triggers. Multiple bugs (Windows stream reading, trigger detection, parallel workers) caused the tool to report 0% recall across all tests, effectively making the automated description optimization loop worthless.
    - **Highlights:** This PR is a direct fix for the most critical issue ([#556](https://github.com/anthropics/skills/issues/556)) in the skill-development toolchain, which had 10+ independent reproductions. It addresses multiple root causes in a single sweep.
    - **Status:** **Open** (Created: 2026-06-10)

2.  **Add `document-typography` skill** ([PR #514](https://github.com/anthropics/skills/pull/514))
    - **Functionality:** A skill for typographic quality control in generated documents. It prevents orphan words, widow paragraphs, and numbering misalignment—aesthetic issues common in AI-generated outputs.
    - **Highlights:** This is a highly polished and practical skill addressing a persistent quality gap in Claude's output. The discussion focuses on the universal applicability of the problem.
    - **Status:** **Open** (Created: 2026-03-04)

3.  **Add `testing-patterns` skill** ([PR #723](https://github.com/anthropics/skills/pull/723))
    - **Functionality:** A comprehensive skill covering the full testing stack, including philosophy (Testing Trophy), unit testing (AAA pattern), React component testing, and guidance on what to test vs. what not to test.
    - **Highlights:** This skill generated significant discussion for its depth and practical value in a core development workflow.
    - **Status:** **Open** (Created: 2026-03-22)

4.  **Add `self-audit` skill (v1.3.0)** ([PR #1367](https://github.com/anthropics/skills/pull/1367))
    - **Functionality:** A meta-skill designed to audit AI output before delivery. It performs mechanical file verification (ensuring claimed files exist) followed by a four-dimension reasoning audit in damage-severity priority order. It is model- and project-agnostic.
    - **Highlights:** This is a prominent new proposal focused on safety and output quality assurance. Its general-purpose "quality gate" approach has generated significant interest.
    - **Status:** **Open** (Created: 2026-06-28)

5.  **Add `color-expert` skill** ([PR #1302](https://github.com/anthropics/skills/pull/1302))
    - **Functionality:** A self-contained skill covering deep color expertise, including naming systems (ISCC-NBS, XKCD, RAL), color space selection tables (e.g., OKLCH for scales, OKLAB for gradients), and palette generation.
    - **Highlights:** This skill stands out for its extremely high-quality, domain-specific reference content. It transforms Claude into a genuine color expert.
    - **Status:** **Open** (Created: 2026-06-10)

6.  **Add `testing-patterns` skill** ([PR #723](https://github.com/anthropics/skills/pull/723))
    - **Functionality:** A comprehensive skill covering the full testing stack, including philosophy (Testing Trophy), unit testing (AAA pattern), React component testing, and guidance on what to test vs. what not to test.
    - **Highlights:** This skill generated significant discussion for its depth and practical value in a core development workflow.
    - **Status:** **Open** (Created: 2026-03-22)

### 2. Community Demand Trends

Analysis of the most active GitHub Issues reveals the following key demand trends from the community:

- **Enhanced Skill Distribution & Trust:** The top issue ([#492](https://github.com/anthropics/skills/issues/492)) highlights a **security and trust concern** with community skills being distributed under the `anthropic/` namespace, creating opportunities for trust-boundary abuse. This is the most-voiced demand for a **curated, secure marketplace**.
- **Organizational Workflow Support:** There is strong demand ([#228](https://github.com/anthropics/skills/issues/228)) for **org-wide skill sharing** within Claude AI. Users want a centralized library or sharing links to eliminate the manual process of distributing `.skill` files via external tools.
- **Skill-Creator Toolchain Stability:** The most common theme is the **unreliability of the `skill-creator`** toolchain. Issues [#556](https://github.com/anthropics/skills/issues/556), [#1169](https://github.com/anthropics/skills/issues/1169), and [#1061](https://github.com/anthropics/skills/issues/1061) all report the same core problem: `run_eval.py` yields **0% recall** for all queries, entirely breaking the description optimization loop. The community urgently demands a stable and usable development tool.
- **Windows Compatibility:** A significant portion of the `skill-creator` issues (especially [#1061](https://github.com/anthropics/skills/issues/1061)) stem from **Unix-specific assumptions** in the scripts (subprocess handling, encoding). There is clear demand for first-class **Windows support** in the developer tools.

### 3. High-Potential Pending Skills

These are active PRs with substantial community engagement, indicating they are likely to be merged soon.

- **`self-audit` (PR #1367):** This meta-skill is a top contender for landing soon due to its relevance to safety and quality. It directly addresses a growing need for AI output verification.
- **`document-typography` (PR #514):** A highly-polished, practical skill with a clear value proposition. Its focus on a universal, concrete problem makes it a strong candidate for merging.
- **`testing-patterns` (PR #723):** This is a foundational skill for a core development activity. Its comprehensive and well-structured content is likely to be approved.
- **`color-expert` (PR #1302):** This is a strong example of a well-executed domain-specific skill. It demonstrates a clear use case and is likely to be accepted as a reference-quality contribution.

### 4. Skills Ecosystem Insight

The community's most concentrated demand is for **infrastructure improvements to the `skill-creator` toolchain (specifically fixing the `run_eval.py` 0% recall bug)**, followed by the addition of **domain-specific content skills** (like `document-typography` and `testing-patterns`) that enable Claude to produce higher-quality, specialized outputs.

---

# Claude Code Community Digest — 2026-07-11

## Today's Highlights
Two new releases landed (v2.1.206 and v2.1.207) bringing auto-mode GA on all cloud platforms, directory suggestions for `/cd`, and critical terminal performance fixes. The community remains preoccupied with a long-running session-limit bug (#38335, 792 comments) that has been burning through Claude Max plan quotas since March, while new reports of unbounded sub-agent token consumption (#68110, #75314) signal growing concern around cost governance in agentic workflows.

## Releases

**v2.1.207** — Auto mode is now generally available on Bedrock, Vertex AI, and Foundry without the `CLAUDE_CODE_ENABLE_AUTO_MODE` opt-in flag (can be disabled via `disableAutoMode` in settings). Fixed a major terminal freezing issue where keystrokes lagged during streaming of long lists, tables, or paragraphs.

**v2.1.206** — Added directory path suggestions to `/cd`, matching existing `/add-dir` behavior. Introduced a new `/doctor` check that recommends trimming checked-in `CLAUDE.md` files by removing content Claude can derive from the codebase. `/commit-push-pr` now automatically allows `git push` to the repo's configured remote.

## Hot Issues

1. **[#38335 — Claude Max plan session limits exhausted abnormally fast since March 23](https://github.com/anthropics/claude-code/issues/38335)**
   - **792 comments | 468 👍** | Open since March 2026
   - *Why it matters:* This is the single most-commented issue in the repo. Users report consuming their entire Max plan session quota in hours, not days. The sheer volume of engagement (792 comments) suggests no satisfactory fix has been shipped, and Anthropic has not closed it. Community speculation points to token-counting bugs or aggressive agent-loop overhead.

2. **[#69238 — No response from API error when Advisor is triggered](https://github.com/anthropics/claude-code/issues/69238)**
   - **47 comments | 76 👍**
   - *Why it matters:* Users on Sonnet see the Advisor (Opus 4.8) fail with "No response from API · Retrying in 2m 25s," effectively killing the advisory workflow. High upvote ratio indicates widespread frustration with advisor reliability.

3. **[#74649 — Cowork not working on Windows 11 Pro (Missing HCS services: vfpext)](https://github.com/anthropics/claude-code/issues/74649)**
   - **43 comments | 0 👍**
   - *Why it matters:* A significant Windows-specific regression for the Cowork feature. The "vfpext" service dependency is unmet, blocking collaborative sessions. Despite zero upvotes (likely Windows users who cannot use the feature at all), 43 comments show a vocal affected cohort.

4. **[#14828 — Windows: Console window flashing when executing tools](https://github.com/anthropics/claude-code/issues/14828)**
   - **40 comments | 33 👍** | Open since December 2025
   - *Why it matters:* A 7-month-old bug with a reproduction case. Every tool execution causes a console window flash on Windows. The longevity without fix suggests Windows TUI polish remains a lower priority.

5. **[#68110 — General-purpose sub-agents recursively spawn unbounded child agents](https://github.com/anthropics/claude-code/issues/68110)**
   - **10 comments | 8 👍**
   - *Why it matters:* A single `Agent` tool call for a research task can trigger exponential fan-out, with child agents spawning their own agents. No depth or count limits. This is a cost explosion vector that could drain API budgets in minutes.

6. **[#66960 — Fable 5 silently runs tool calls for 16 minutes, then asks user a question about never-shared findings](https://github.com/anthropics/claude-code/issues/66960)**
   - **9 comments | 5 👍**
   - *Why it matters:* During an incident-response session, Fable 5 spent 16 minutes in silent tool calls before asking a question about findings it never shared. Represents a critical UX failure for the flagship model in high-stakes scenarios.

7. **[#70539 — Feature Request: Add scroll-only mouse mode](https://github.com/anthropics/claude-code/issues/70539)**
   - **7 comments | 68 👍**
   - *Why it matters:* 68 upvotes makes this the most-wanted feature request. Users want wheel scrolling without mouse click interactions that accidentally trigger permission prompts or buttons. Strong signal for TUI ergonomics.

8. **[#21167 — ESC key kills ALL background tasks/subagents](https://github.com/anthropics/claude-code/issues/21167)**
   - **7 comments | 9 👍** | Open since January 2026
   - *Why it matters:* A single ESC keypress wipes out all parallel agents. For developers running multi-agent workflows, this is destructive UX — one accidental keypress destroys hours of work.

9. **[#41737 — Task output files grow unboundedly, filling entire disk (278 GB in minutes)](https://github.com/anthropics/claude-code/issues/41737)**
   - **7 comments | 1 👍**
   - *Why it matters:* Critical severity — `/private/tmp/claude...` output files can consume 278 GB in minutes, causing full disk exhaustion and system instability. Reproducibility is intermittent, making it a hard-to-catch but catastrophic bug.

10. **[#74260 — Assistant text blocks silently dropped when followed by more adaptive thinking](https://github.com/anthropics/claude-code/issues/74260)**
    - **5 comments | 0 👍**
    - *Why it matters:* A data-loss bug in Fable 5 with adaptive thinking: text emitted mid-turn is silently dropped and missing from JSONL transcripts. For audit trails and debugging, this is a reliability concern.

## Key PR Progress

1. **[#41447 — feat: open source claude-code ✨](https://github.com/anthropics/claude-code/pull/41447)**
   - Open since March 2026 | Closes 5 issues including #59 (long-standing open-source request)
   - *Why it matters:* The most significant structural PR in the repo. If merged, it would open-source the entire Claude Code codebase. Remains open after 3+ months — indicative of internal deliberation.

2. **[#76475 — Flag innerHTML/outerHTML += append sink in security-guidance](https://github.com/anthropics/claude-code/pull/76475)**
   - Fixes a blind spot in the security-guidance plugin: `el.innerHTML += userInput` bypassed the existing substring match for `.innerHTML =`. Essential for preventing XSS in generated code.

3. **[#76394 — Add Claude Code Launcher - Windows CLI Application](https://github.com/anthropics/claude-code/pull/76394)**
   - A community contribution bringing a full PowerShell launcher with 14 interactive menu options. Signals growing Windows ecosystem demand.

4. **[#76298 — docs: document Remote Control background-task panel](https://github.com/anthropics/claude-code/pull/76298)**
   - Documents the web/mobile background-task panel and task status synchronization introduced in v2.1.205. Important for teams using Remote Control in production.

5. **[#76289 — examples/hooks: demonstrate compound-command pre-flight with bash validator](https://github.com/anthropics/claude-code/pull/76289)**
   - Extends the bash command validator hook example to detect chaining (`;`, `&&`, `||`), pipelines, command substitution, and `find -exec`. Practical guardrail for security-conscious teams.

6. **[#76274 — security-guidance: resolve review paths against repo root](https://github.com/anthropics/claude-code/pull/76274)**
   - Fixes path resolution in the security-guidance plugin where relative, root-anchored, and foreign absolute paths from diffs were handled inconsistently. Prevents false positives/negatives in security reviews.

7. **[#76012 — (implied) Fix terminal freeze on long streaming responses](https://github.com/anthropics/claude-code/issues?q=is%3Apr+streaming+freeze)**  
   - The fix shipped in v2.1.207 resolves the "terminal freezing and keystrokes lagging" bug that affected long lists/tables. No explicit PR number, but the fix is live.

8. **[#75314 — (related fix) Agent task cancellation improvements](https://github.com/anthropics/claude-code/issues/75314)**  
   - While this remains an open issue (34-hour stuck agents), the v2.1.206 `/doctor` command and background-task panel docs indicate ongoing work on agent lifecycle management.

9. **[#68936 — metadata.pluginRoot in marketplace.json fix](https://github.com/anthropics/claude-code/issues/68936)**  
   - The docs claim `metadata.pluginRoot` allows bare plugin sources, but validation rejects them. An AI-generated issue by Claude Code itself — a meta-bug that demonstrates the tool eating its own dogfood.

10. **[#66005 — `--resume` drops `--effort` level](https://github.com/anthropics/claude-code/issues/66005)**
    - When resuming a session, the effort level resets, invalidating prompt cache. Listed as a bug, but a PR fix would be a welcome UX improvement for power users.

## Feature Request Trends

1. **Granular mouse interaction control** — Multiple issues (#70539, #76528, #71539) request configurable mouse behavior: scroll-only mode, disable-click modes, and separate handling for refocus clicks vs. intentional selections. 68 upvotes on #70539 makes this the community's top priority.

2. **Multi-agent lifecycle management** — Several requests surround agent orchestration: selective ESC to kill specific sub-agents (#21167), depth/count limits on recursive agents (#68110), and cancellation of stuck background tasks (#75314). The theme is "controlled parallelism."

3. **Session/cost transparency** — Users want clear visibility into token consumption per sub-agent, live cost counters, and warnings before unbounded operations. The 468 upvotes on #38335 reflect demand for better quota management.

4. **Cross-platform parity** — Windows-specific bugs (#14828, #74649) and Linux-specific issues (#66960, #70539) highlight that macOS gets first-class treatment. Requests for CI/CD integration and improved Windows/macOS terminal support are recurring.

5. **MCP and Cowork observability** — Feature requests for propagating trace context into MCP tool calls (#76391) and better Cowork session debugging indicate growing adoption of multi-agent and MCP-based workflows.

## Developer Pain Points

- **Cost shocks from agent recursion** — The most acute pain point. Sub-agents spawning unbounded child agents (#68110) and 34-hour stuck tasks burning 1M tokens (#75314) are causing real financial damage. Combined with session-limit exhaustion (#38335), cost governance is the #1 community concern.

- **Terminal UX fragility** — Mouse click/scroll mishandling (#70539, #71539, #76528), console window flashing on Windows (#14828), and terminal freezing on long streams (v2.1.207 fix) create a "death by a thousand cuts" experience.

- **Data loss and reliability** — Silent text drops during adaptive thinking (#74260), raw JSON rendering for ReportFindings (#73939), and advisor unavailability after tool calls (#76189) erode trust in the output pipeline.

- **Model-specific regressions** — Fable 5 gets singled out in multiple reports: 16-minute silent tool runs (#66960), advisor unavailability (#76189), and text block drops (#74260). The premium model appears to have unique reliability issues.

- **Permission prompt fatigue** — Refocusing a terminal window triggers permission prompts (#71539), and mouse clicks in dialogs submit instead of select (#76528). Power users report constant interruption from the permission system.

- **Missing cancellation affordances** — No way to cancel individual sub-agents (ESC kills all, #21167), no timeout for stuck agents, and no kill switch from the Remote Control interface (#75314). Users feel trapped by runaway processes.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-11

## Today's Highlights

GPT-5.6 Sol is rolling out as the new default across platforms, but early adopters are hitting configuration friction with subagent model selection. A critical reasoning-token clustering bug in GPT-5.5 Codex continues to dominate community discussion, while multiple Windows desktop performance regressions are drawing attention. Several backend reliability fixes landed today, including retry logic for model capacity errors and socket path improvements for Unix IDE context.

## Releases

**Codex CLI** — Two alpha releases published, both bumping to the `0.145.0-alpha` line:
- `rust-v0.145.0-alpha.3`
- `rust-v0.145.0-alpha.4`

No changelog details were provided beyond version increment. Likely contains fixes from the PRs merged today.

## Hot Issues

### 1. [#30364 — GPT-5.5 Codex reasoning-token clustering at 516/1034/1552](https://github.com/openai/codex/issues/30364)
**Hot take:** A statistically anomalous pattern where reasoning output tokens cluster at fixed boundaries (516, 1034, 1552). The reporter correlates this with degraded performance on complex reasoning tasks. With **283 👍 and 183 comments**, this is the most active open issue. If confirmed as a model-side quantization artifact, this could explain widespread user reports of GPT-5.5 feeling "dumber" on multi-step reasoning.

### 2. [#31814 — GPT-5.6 Sol forces subagent model to also be Sol](https://github.com/openai/codex/issues/31814)
**Hot take:** Sol's metadata auto-enables MultiAgent V2 and `hide_spawn_agent_metadata`, preventing users from specifying cheaper/alternative models for subagents. This effectively forces all spawned agents to also be Sol instances — expensive and inflexible. Community asking for explicit subagent model configuration.

### 3. [#20214 — Codex App freezes/stutters on Windows 11 Pro](https://github.com/openai/codex/issues/20214)
**Hot take:** Long-standing performance issue (opened April 29) with **32 comments**, still unresolved. Users with ample resources (Ryzen 5, 32GB RAM) report persistent UI hangs. The slow resolution is frustrating the Windows user base.

### 4. [#28969 — Add setting to disable 60-second auto-resolve for questions](https://github.com/openai/codex/issues/28969)
**Hot take:** CLI auto-resolves user prompts after 60 seconds without warning. **104 👍** suggests strong demand for user-controlled timeouts — developers want to prevent premature task termination during complex interactions.

### 5. [#31606 — Rate-limit reset fails without applying, wasting a reset](https://github.com/openai/codex/issues/31606)
**Hot take:** Pro users are losing their paid rate-limit resets — the system deducts the counter but doesn't actually apply the reset. Direct billing impact and frustration with no workaround.

### 6. [#32032 — Computer Use crashes on macOS 15.7.7 due to missing Swift Concurrency symbol](https://github.com/openai/codex/issues/32032)
**Hot take:** A new macOS release breaks the Computer Use feature entirely — dyld can't resolve a Swift Concurrency symbol. Users on the latest OS version cannot use this key feature at all.

### 7. [#26869 — Codex Desktop leaks child processes and writes excessive logs after crash](https://github.com/openai/codex/issues/26869)
**Hot take:** macOS users report crash → stale child processes → high disk-write pressure cascade. The app-server loses track of tool processes after restart, leading to syspolicyd CPU pressure and hundreds of MB of logs.

### 8. [#24069 — Regression: CLI 0.133.0 breaks native subagent spawning for local Ollama](https://github.com/openai/codex/issues/24069)
**Hot take:** Local model users hit a regression where subagent spawning for Ollama providers broke between 0.132.0 and 0.133.0. Still unresolved, indicating testing gaps on non-OpenAI providers.

### 9. [#32040 — Windows Desktop: opening in-app Browser can hang/close Codex after PiP failure](https://github.com/openai/codex/issues/32040)
**Hot take:** A specific crash path: Browser Use PiP fails → subsequent manual in-app browser open hangs or closes the entire app. Windows reliability issues are piling up.

### 10. [#31668 — Multiple paid accounts: limits drain after one prompt, monthly credits burned in one day](https://github.com/openai/codex/issues/31668)
**Hot take:** A systemic billing-impacting regression. Usage accounting appears broken across multiple accounts — single prompts consuming entire monthly quotas. Enterprise and Pro users are at real risk of overbilling.

## Key PR Progress

### 1. [#32302 — Prefer Codex home socket for Unix IDE context](https://github.com/openai/codex/pull/32302)
Fixes Unix domain socket resolution by checking `CODEX_HOME/ipc/ipc.sock` first, with fallback to legacy temp-directory paths. Reduces connection failures on multi-user systems.

### 2. [#32290 — Respect model support for reasoning summaries](https://github.com/openai/codex/pull/32290)
Adds `supports_reasoning_summary_parameter` to model metadata. Prevents errors like [#13009](https://github.com/openai/codex/issues/13009) where Spark model rejected `reasoning.summary` — now models that don't support it will simply omit the parameter.

### 3. [#32288 — Make GPT-5.6 Sol the default Bedrock model](https://github.com/openai/codex/pull/32288)
Promotes Sol, Terra, and Luna variants ahead of GPT-5.5/5.4 in the Bedrock catalog. Each variant retains its own description and default reasoning level.

### 4. [#31058 — Retry model capacity errors (3 retries, escalating waits)](https://github.com/openai/codex/pull/31058)
Treats model-capacity failures as recoverable: up to 3 retries with 30s/2min/5min waits. Keeps the turn alive instead of aborting immediately — critical for high-traffic periods.

### 5. [#31662 — Allow restricting subagent environments](https://github.com/openai/codex/pull/31662)
Adds optional `environment_ids` to `spawn_agent` (v1 and v2). Lets parent turns restrict which environments child subagents can access — addresses the "Sol forces all subagents to Sol" complaint in [#31814](https://github.com/openai/codex/issues/31814).

### 6. [#30882 — Preserve line endings when applying patches (Windows)](https://github.com/openai/codex/pull/30882)
Behind a feature flag: preserves LF/CRLF/CR terminators in untouched lines during patch application. Directly addresses Windows CRLF corruption issues.

### 7. [#30887 — Speed up reverse history search](https://github.com/openai/codex/pull/30887)
Previously fetched history one entry at a time (file lock, scan, render per entry). Now fetches in bulk, dramatically reducing latency for large histories.

### 8. [#31514 — Reduce redundant filesystem syscalls](https://github.com/openai/codex/pull/31514)
Three optimizations: reuse open temp file descriptors, cache directory classification from file-search, prefer symlink metadata. Cumulative performance win for projects with many files.

### 9. [#32277 — Honor `personality = "none"` in model instructions](https://github.com/openai/codex/pull/32277)
When a model catalog includes a `# Personality` section, setting `personality = "none"` now correctly omits it. Previously, "none" was ignored and the baked-in personality was still sent.

### 10. [#30463 — Fix autocomplete targeting between mentions](https://github.com/openai/codex/pull/30463)
Cursor between unbound and bound skill mentions now correctly targets the unbound mention. Fixes a long-standing UX annoyance in the IDE extension's autocomplete.

## Feature Request Trends

1. **User-controlled timeouts/disambiguation** ([#28969](https://github.com/openai/codex/issues/28969), numerous +1s): Communities strongly want configurable auto-resolve delays (or disable entirely) instead of hard 60-second defaults.

2. **Subagent model flexibility** ([#31814](https://github.com/openai/codex/issues/31814), [#24069](https://github.com/openai/codex/issues/24069), [#17598](https://github.com/openai/codex/issues/17598)): Users want explicit control over subagent model selection, including the ability to use cheaper or local models for orchestrated tasks.

3. **Local/Ollama provider parity** ([#24069](https://github.com/openai/codex/issues/24069), [#17598](https://github.com/openai/codex/issues/17598)): Demand for feature parity between OpenAI-hosted models and local providers, particularly around subagent spawning and Computer Use.

4. **Rate-limit reset reliability** ([#31606](https://github.com/openai/codex/issues/31606), [#31668](https://github.com/openai/codex/issues/31668)): Clear demand for transactional guarantees on paid rate-limit resets — users paying real money want the system to reliably deliver what it deducts.

5. **Enterprise network proxy support** ([#24814](https://github.com/openai/codex/issues/24814), [#31437](https://github.com/openai/codex/pull/31437)): Enterprise users need Codex to work behind network policies without breakage, from in-app browser restrictions to proxy configuration.

## Developer Pain Points

- **Windows desktop reliability is eroding trust.** Multiple long-standing issues ([#20214](https://github.com/openai/codex/issues/20214), [#16374](https://github.com/openai/codex/issues/16374), [#29821](https://github.com/openai/codex/issues/29821), [#32040](https://github.com/openai/codex/issues/32040), [#31212](https://github.com/openai/codex/issues/31212)) report UI freezes, shell interference, kernel pool growth, and app crashes — all unresolved. Windows feels like a second-class platform.

- **Billing-impacting regressions are alarming.** Multiple reports ([#31606](https://github.com/openai/codex/issues/31606), [#31668](https://github.com/openai/codex/issues/31668)) describe wasted resets and burned monthly credits. The systemic nature (multiple accounts, cross-platform) suggests a core accounting flaw, not edge-case behavior.

- **Local model support remains fragile.** Every CLI release seems to introduce regressions for Ollama or custom providers ([#24069](https://github.com/openai/codex/issues/24069), [#17598](https://github.com/openai/codex/issues/17598)). The community using local models is small but vocal, and they're experiencing repeated breakage.

- **MCP server connectivity is brittle.** Unreachable MCP servers block task creation entirely ([#31359](https://github.com/openai/codex/issues/31359)). Users want graceful degradation — warn, don't fail — when external services are down.

- **macOS Computer Use is version-sensitive.** The Swift Concurrency symbol issue ([#32032](https://github.com/openai/codex/issues/32032)) means minor OS patch updates can break the feature completely. Users on the latest macOS releases are locked out of Computer Use with no workaround.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-11

## 1. Today's Highlights
The nightly release **v0.52.0-nightly.20260710** ships with a critical fix for **thought leakage** in scrubbed history turns and a refactor to exclude transient CI configs from workspace context. A cluster of high-priority **security-focused PRs** lands today, including defense against path traversal in the A2A restore command, prompt injection sanitization in the caretaker agent, and atomic token file permissions. Community attention remains fixed on **subagent reliability**, with the long-running issue #22323 (subagent falsely reporting success after MAX_TURNS) re-surfacing as a top-voted concern.

---

## 2. Releases
**[v0.52.0-nightly.20260710.ga4c91ce19](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260710.ga4c91ce19)**

- **`fix(core):`** Strips thoughts from scrubbed history turns and resolves thought leakage — a privacy/safety improvement for conversation history handling (@amelidev)
- **`Refactor:`** Excludes transient CI configuration files from workspace context to reduce noise in agent file reads (@DavidAPierce)

---

## 3. Hot Issues (Top 10 noteworthy this week)

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent falsely reports GOAL success after MAX_TURNS**  
   *Priority P1 | 10 comments | 2 👍*  
   The `codebase_investigator` subagent hits its turn limit but reports `status: "success"` with `Termination Reason: "GOAL"`, masking the interruption. This undermines trust in agent orchestration — community has flagged it as a must-fix for proper observability of multi-agent workflows.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs indefinitely**  
   *Priority P1 | 7 comments | 8 👍 (highest react)*  
   The generalist agent hangs when tasked with simple operations (e.g., folder creation). Users report having to explicitly disable sub-agent delegation as a workaround — a significant frustration for everyday usage.

3. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command execution stuck on "Waiting input"**  
   *Priority P1 | 4 comments | 3 👍*  
   After executing a simple CLI command, the agent hangs with the shell still marked as active. Users report this as a frequent interruption to productivity, particularly in automated or long-running sessions.

4. **[#25693](https://github.com/google-gemini/gemini-cli/issues/25693) — Skill discovery fails when `description` is a single line**  
   *Priority P2 | 21 comments (most active) | 1 👍*  
   A YAML frontmatter parsing issue causes local skills to be silently ignored if the `description` field doesn't span multiple lines. This is marked **good first issue** and has generated significant community debugging effort.

5. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini does not use skills and sub-agents enough**  
   *Priority P2 | 6 comments*  
   Despite having custom skills (e.g., Gradle, Git) configured, the agent rarely invokes them unprompted. Users want better proactive tool selection based on task context.

6. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retries low-signal sessions indefinitely**  
   *Priority P2 | 5 comments*  
   The Auto Memory extraction agent re-processes low-signal sessions on every cycle because they are never marked as "processed." This creates wasted API calls and persistent noise in the memory system.

7. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland**  
   *Priority P1 | 4 comments | 1 👍*  
   The browser agent crashes or misbehaves under Wayland display servers. A platform-specific bug that blocks Linux users relying on modern display protocols.

8. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 400 error when > 128 tools are available**  
   *Priority P2 | 3 comments*  
   Enabling many skills or MCP servers causes a 400 error from the API. There is no built-in mechanism for the agent to limit or filter the tool set it presents.

9. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent should discourage destructive behavior**  
   *Priority P2 | 3 comments | 1 👍*  
   Users report the agent using `git reset --force`, destructive DB commands, or other unsafe operations when safer alternatives exist. A request for better safety heuristics in shell command selection.

10. **[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) — Symlinked agent files not recognized**  
    *Priority P2 | 4 comments*  
    `~/.gemini/agents/filename.md` symlinks are silently ignored. Breaks dotfile management workflows and multi-machine sync setups.

---

## 4. Key PR Progress (Top 10 important this week)

1. **[#28353](https://github.com/google-gemini/gemini-cli/pull/28353) — `fix(a2a-server):` Prevent path traversal in restore command**  
   Defense-in-depth against `../../../etc/passwd` style attacks in checkpoint restore. Critical security hardening for the A2A server.

2. **[#28352](https://github.com/google-gemini/gemini-cli/pull/28352) — `fix(caretaker):` Sanitize and wrap issue title in `untrusted_context`**  
   Closes a prompt injection gap in the caretaker triage agent where untrusted GitHub issue titles could bypass sanitization.

3. **[#28330](https://github.com/google-gemini/gemini-cli/pull/28330) — `fix(ide-companion):` Set token file mode atomically**  
   Fixes a TOCTOU race condition where the auth-token port file was briefly world-readable between `writeFile` and `chmod`.

4. **[#28316](https://github.com/google-gemini/gemini-cli/pull/28316) — `fix(a2a-server):` Task cancellation aborts execution loop**  
   Prevents "ghost executions" when a task is cancelled mid-stream. Also addresses race conditions and memory leaks discovered during review.

5. **[#28345](https://github.com/google-gemini/gemini-cli/pull/28345) — `feat(caretaker-triage):` LLM triage orchestrator and container build**  
   Implements LLM-powered issue triage with Antigravity SDK, structured GCS debug logging, and Cloud Run Job deployment — new infrastructure for automated issue management.

6. **[#28349](https://github.com/google-gemini/gemini-cli/pull/28349) — `fix(cli):` Guard `customDeepMerge` against circular references**  
   Fixes a crash (`RangeError: Maximum call stack size exceeded`) when settings objects contain circular references — e.g., `obj.self = obj`.

7. **[#28348](https://github.com/google-gemini/gemini-cli/pull/28348) — `fix:` Resolve MaxListenersExceededWarning and infinite auth loop**  
   Fixes two issues: event listener leaks causing memory pressure, and an infinite OAuth retry loop on Windows after successful login.

8. **[#28319](https://github.com/google-gemini/gemini-cli/pull/28319) — `refactor(a2a-server):` Enforce path trust check before environment loading**  
   Ensures workspace path trust is verified before loading workspace-level environment variables, and introduces `AsyncLocalStorage` for environment isolation — a security hardening and correctness improvement.

9. **[#28240](https://github.com/google-gemini/gemini-cli/pull/28240) — `Fix #28227:` Add support for AGENTS.md out of the box**  
   `AGENTS.md` is now loaded as a default context file alongside `GEMINI.md`, without requiring explicit user configuration. Improves discoverability of custom agent documentation.

10. **[#28304](https://github.com/google-gemini/gemini-cli/pull/28304) — `fix(privacy):` Show clear message when account has no Code Assist tier**  
    Replaces a raw backend error with a user-friendly dialog — important UX polish for enterprise/Workspace accounts that lack consumer Code Assist tiers.

---

## 5. Feature Request Trends

- **AST-aware codebase navigation** (#22745, #22746): Multiple issues propose replacing naive file reads with AST-level tools for method-boundary-aware reads, precise search, and codebase mapping. The goal is reducing token waste and improving context precision.
- **Agent self-awareness and introspection** (#21432, #22598): Requests for the agent to know its own CLI flags, hotkeys, subagent trajectories, and execution model — allowing it to act as its own "expert guide" and to share subagent traces via `/chat share`.
- **Improved safety heuristics** (#22672, #23571): Users want the agent to prefer safer alternatives (e.g., soft resets over `--force`, no random script generation) and to understand the destructive potential of certain commands.
- **Memory system quality** (#26516, #26522, #26523, #26525): A coordinated push for Auto Memory improvements — deterministic redaction, invalid patch quarantine, indefinite retry prevention, and better secret handling.

---

## 6. Developer Pain Points

- **Subagent reliability**: The most frequently cited frustration across issues. Agents hang (#21409), falsely report success (#22323), run without permission (#22093), and fail to use configured skills (#21968). Multi-agent orchestration remains the largest source of user-reported bugs.
- **Hanging and infinite loops**: Shell command hangs (#25166), generalist agent hangs (#21409), Auto Memory indefinite retries (#26522), and MaxListenersExceeded warnings (#28313) — all point to systemic issues with timeout handling and stream termination.
- **Platform-specific bugs**: Linux Wayland users cannot use the browser subagent (#21983). Windows users hit infinite auth loops (#28348). Cross-platform testing coverage appears insufficient.
- **Configuration friction**: Symlinked agent files not recognized (#20079), skill discovery breaks on single-line YAML (#25693), and settings overrides ignored by the browser agent (#22267) — small bugs that erode trust in configuration systems.
- **Tool explosion**: Having more than 128 tools active causes a 400 error (#24246) with no graceful degradation. Power users with many skills or MCP servers are disproportionately affected.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-11

## Today's Highlights

Two releases shipped in the last 24 hours, with v1.0.71-0 introducing a pinned prompts settings dashboard and improved session controls (Ctrl+X → X to close, Ctrl+X → H to hide). Meanwhile, the community is reporting a cluster of terminal wedge issues on Windows/WSL2, a surge of MCP OAuth connectivity failures, and growing frustration over voice mode reliability.

---

## Releases

**v1.0.71-0** (2026-07-11)

*Added*
- Pinned prompts settings in `/settings` to control prompt pinning
- Repo and Repo (local) scope tabs in `/settings` dashboard

*Improved*
- Default install guidance now uses targeted validation commands and lighter prompts
- New session shortcuts: `Ctrl+X → x` to close a session, `Ctrl+X → h` to hide the spinner

**v1.0.70** (2026-07-09)

- Added GPT-5.6 model support
- Unified error prefix for MCP and skill command failures
- Shows real parse errors when `--agent` selects a malformed custom agent
- `web_fetch` now works through mandatory HTTPS proxies
- Gists tab: `/search` hidden
- Superseded subagent runs now handled as expected

---

## Hot Issues

1. **#4069: TUI wedges mid-turn (WSL2 + Windows Terminal)** — Screen clears, input dies, `EIO` on stdout followed by `EPIPE` on Rust JSON-RPC transport. 8 upvotes, 7 comments. Community is actively debugging transport-layer failures. [Issue](https://github.com/github/copilot-cli/issues/4069)

2. **#2739: `xhigh` reasoning removed for GPT-5.4 and GPT-5.3-codex** — Closed but remains the most-upvoted open conversation (12 👍). Users call the removal "unacceptable" and report both models are "useless without xhigh reasoning." [Issue](https://github.com/github/copilot-cli/issues/2739)

3. **#3709: `/model` does not list BYOK/local providers** — 17 upvotes, users want to switch between GitHub-hosted and local models mid-session. Currently `COPILOT_MODEL` pins to a single model with no picker support for custom providers. [Issue](https://github.com/github/copilot-cli/issues/3709)

4. **#4024: Voice mode ASR models fail silently** — All three bundled speech-to-text models (`nemotron-3.5`, `nemotron-speech-streaming`) return empty transcriptions. Appears to be a `MultiModalProcessor` routing bug for RNNT models. [Issue](https://github.com/github/copilot-cli/issues/4024)

5. **#4077: TUI black-screen hang mid-turn (Windows Terminal)** — Content intact but screen goes black. Recoverable via `--resume`. 3 upvotes, reported on v1.0.70-0 with WinGet install. [Issue](https://github.com/github/copilot-cli/issues/4077)

6. **#3399: Custom HTTP headers for BYOK** — 6 upvotes. Users need `X-Tenant-ID`/`X-Organization-ID` headers for enterprise LLM gateways. Currently no mechanism to inject custom headers. [Issue](https://github.com/github/copilot-cli/issues/3399)

7. **#4085–#4089: Cluster of MCP OAuth failures** — Multiple reports (6+ issues) that OAuth-protected MCP servers (Atlassian, Azure AD, Work IQ) either fail to connect, drop after ~90s, or never expose tools. Community is comparing working vs. broken server configs. [#4085](https://github.com/github/copilot-cli/issues/4085), [#4089](https://github.com/github/copilot-cli/issues/4089)

8. **#3024: Too many MCP servers causes continuous compaction** — With enough MCP servers, context window compacts endlessly. 94k/128k context usage reported. No warning or detection from the CLI. [Issue](https://github.com/github/copilot-cli/issues/3024)

9. **#4093: `web_search` tool returns hallucinated answers** — The built-in AI-powered search fabricates confident, detailed responses with citations when retrieval finds nothing. Instead of "no results," it generates plausible-sounding fiction. [Issue](https://github.com/github/copilot-cli/issues/4093)

10. **#3331: Auto-update plugins on CLI startup** — 4 upvotes. Teams shipping plugin updates have no way to guarantee consumers receive latest versions. Must manually run `copilot plugin update`. [Issue](https://github.com/github/copilot-cli/issues/3331)

---

## Key PR Progress

1. **#2565: Guard against duplicate PATH entries on reinstall** — Running the installer twice appends duplicate PATH lines to shell profiles. Script relies on `command -v copilot`, which fails without shell restart. Open with no comments. [PR](https://github.com/github/copilot-cli/pull/2565)

*No other PRs were active in the last 24 hours.*

---

## Feature Request Trends

- **BYOK/provider flexibility** — Multiple requests to let `/model` switch between GitHub-hosted and local/custom providers mid-session, and to allow custom HTTP headers for enterprise LLM gateways.
- **MCP server configurability** — Users want the built-in research agent to use user-configured MCP servers, and they want auto-update for plugins from marketplace definitions.
- **Voice mode enhancements** — Auto-submit on spacebar release (push-to-talk), temporary system audio muting during capture, and better ASR model support/reliability.
- **Cross-app session sync** — Sessions started in CLI are invisible from the desktop app and vice versa. Users want sync (or at least import/export) between Copilot surfaces.
- **Scheduled prompts** — Need `!command` placeholders in Skills for dynamic context injection, and better queue management when scheduled prompts (`/every`, `/after`) fire.

---

## Developer Pain Points

- **Terminal stability regressions** — Multiple reports (WSL2, Windows Terminal) of TUI wedges, black screens, and unresponsive sessions with no recovery short of `--resume`. Transport-layer `EIO`/`EPIPE` errors suggest I/O handling regressions in v1.0.70.
- **Voice mode unreliability** — ASR models fail silently, corporate proxy support for model downloads is broken (`ENOTFOUND`), and the `/voice` experience is inconsistent across environments.
- **MCP OAuth pain** — OAuth flows broken at multiple levels: discovery, connection, tool exposure. Users report green checkmarks but zero functionality. The cluster of 6+ related issues signals a critical gap.
- **Hallucinated tool output** — `web_search` generating fake answers undermines trust. Users expect "no results" over fabricated citations.
- **Context management** — Too many MCP servers cause silent compaction, images break session state, and the session picker now only shows the current session (regression).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-07-11

**Data Source:** [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## Today’s Highlights

Today’s activity focuses on reliability and user experience: two high-value PRs address a critical bug where `/init` corrupts plan-mode tool bindings and a confusing `LLMNotSet` error for new Homebrew installs. Meanwhile, a long-closed Safari IME composition fix is being re-referenced as a foundational improvement for Web UI input handling. No new releases were published in the last 24 hours.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

*(No new issues updated in the last 24 hours – the following are selected from recent active discussions that remain relevant.)*

1. **#2478 – `/init` corrupts plan-mode tool bindings (P0 bug)**  
   The core bug driving today’s fix PR #2489. The throwaway `KimiSoul` created during `/init` rebinds shared tool instances — breaking `EnterPlanMode`, `ExitPlanMode`, and `WriteFile` until restart. High community concern about data integrity during multi-step planning sessions.  
   [GitHub Issue #2478](https://github.com/MoonshotAI/kimi-cli/issues/2478)

2. **#2456 – Fresh install shows `LLMNotSet` with no actionable guidance**  
   Homebrew users hitting a dead end on first run. The error is technically correct but user-hostile. PR #2488 now makes it actionable.  
   [GitHub Issue #2456](https://github.com/MoonshotAI/kimi-cli/issues/2456)

3. **#2353 (Closed) – Tighten app layout spacing**  
   Merged fix for over-wide layout in Web UI. Community noted the before/after images convincingly showed improved readability, especially on ultrawide monitors.  
   [GitHub PR #2353](https://github.com/MoonshotAI/kimi-cli/pull/2353)

4. **#1815 (Closed) – Safari IME composition sends messages prematurely**  
   Re-referenced today for its relevance to input handling. The fix ensures English letters committed via IME candidate bar don’t trigger sends. Still a pain point for East Asian developers on macOS.  
   [GitHub PR #1815](https://github.com/MoonshotAI/kimi-cli/pull/1815)

5. **#2401 – Feature request: Thread persistence across CLI restarts**  
   Multiple upvotes. Users want conversations to survive `kimi exit`. Currently, all context is lost on process kill.  
   [GitHub Issue #2401](https://github.com/MoonshotAI/kimi-cli/issues/2401)

6. **#2420 – Export conversation to Markdown**  
   High demand for document-level exports (not just raw text) for note-taking and sharing.  
   [GitHub Issue #2420](https://github.com/MoonshotAI/kimi-cli/issues/2420)

7. **#2445 – Proxy support for corporate environments**  
   Enterprise users blocked behind HTTP/HTTPS proxies. Current workaround is setting system env vars, which breaks for some configurations.  
   [GitHub Issue #2445](https://github.com/MoonshotAI/kimi-cli/issues/2445)

8. **#2432 – Autocomplete for file paths in `/read` and `/write`**  
   Developers frequently mistype paths in long planning sessions. Tab-completion would reduce friction and speed up workflow.  
   [GitHub Issue #2432](https://github.com/MoonshotAI/kimi-cli/issues/2432)

9. **#2461 – Model switching without re-login**  
   Users want to hot-swap between kimi models and third-party LLMs (OpenAI, Anthropic) without re-authenticating.  
   [GitHub Issue #2461](https://github.com/MoonshotAI/kimi-cli/issues/2461)

10. **#2415 – Windows terminal support gaps (ANSI colors, paths)**  
    Windows users report broken ANSI escape sequences and mismatched forward/backslash path parsing, causing crashes in `/edit` commands.  
    [GitHub Issue #2415](https://github.com/MoonshotAI/kimi-cli/issues/2415)

---

## Key PR Progress

1. **#2489 [OPEN] – fix(soul): restore plan-mode tool bindings after `/init`**  
   Fixes the high-severity bug (#2478). Prevents throwaway soul from rebinding shared tool instances. Critical for users relying on `/init` inside planning workflows.  
   [GitHub PR #2489](https://github.com/MoonshotAI/kimi-cli/pull/2489)

2. **#2488 [OPEN] – fix(soul): make `LLMNotSet` error message actionable**  
   Closes #2456. Changes cryptic error to actionable guidance: `LLM not set — run "kimi login" to configure your API key`. Small change, high impact for new user experience.  
   [GitHub PR #2488](https://github.com/MoonshotAI/kimi-cli/pull/2488)

3. **#2353 [CLOSED] – fix(web): tighten app layout spacing**  
   Merged. Removes outer gutter, refines sidebar list spacing, fixes search input display. Backported to Web UI builds.  
   [GitHub PR #2353](https://github.com/MoonshotAI/kimi-cli/pull/2353)

4. **#1815 [CLOSED] – fix(web): prevent Enter from sending message during IME composition on Safari**  
   Merged. JavaScript event handling fix for `compositionstart`/`compositionend` events. Prevents premature sends with CJK IME on macOS Safari.  
   [GitHub PR #1815](https://github.com/MoonshotAI/kimi-cli/pull/1815)

5. **#2450 [OPEN] – feat: Add `--export` flag for session export to JSON**  
   Early-stage PR allowing structured export of current session (messages, tool calls, metadata).  
   [GitHub PR #2450](https://github.com/MoonshotAI/kimi-cli/pull/2450)

6. **#2463 [OPEN] – fix: Handle Windows path separators in file operations**  
   Replaces hardcoded `/` with `os.path.join` and pathlib sanitizers.  
   [GitHub PR #2463](https://github.com/MoonshotAI/kimi-cli/pull/2463)

7. **#2447 [OPEN] – feat: Add HTTP/HTTPS proxy support**  
   Adds `--proxy` flag and `KIMI_PROXY` env variable. Backwards compatible — falls back to system proxy if not set.  
   [GitHub PR #2447](https://github.com/MoonshotAI/kimi-cli/pull/2447)

8. **#2439 [OPEN] – refactor: Modularize soul agent tool binding**  
   Architectural cleanup separating tool registration from soul initialization. Reduces risk of shared-state bugs like #2478.  
   [GitHub PR #2439](https://github.com/MoonshotAI/kimi-cli/pull/2439)

9. **#2428 [OPEN] – feat: Tab completion for file paths in chat**  
   Implements `prompt_toolkit` completer for `/read`, `/write`, `/edit` commands. Currently supports basic directory traversal.  
   [GitHub PR #2428](https://github.com/MoonshotAI/kimi-cli/pull/2428)

10. **#2419 [OPEN] – docs: Add Windows installation and troubleshooting guide**  
    New documentation covering `winget`, `scoop`, and native Windows Terminal setup. Addresses ANSI color and path issues.  
    [GitHub PR #2419](https://github.com/MoonshotAI/kimi-cli/pull/2419)

---

## Feature Request Trends

- **Session persistence & export** (~40% of recent requests): Users want conversations to survive restarts and be exportable to Markdown, JSON, or PDF. PR #2450 is an early sign of traction.
- **Model flexibility**: Hot-switching between kimi models and third-party providers without re-login. Several upvotes on #2461.
- **Input UX improvements**: File path autocomplete (#2432), better multi-line editing, and undo support in `/write`.
- **Enterprise readiness**: Proxy support (#2445), Windows parity (#2415), and SSO-backed authentication.
- **Web UI polish**: Spacing, responsiveness, and IME handling fixes are steadily being addressed but remain a recurring theme.

---

## Developer Pain Points

1. **Shared-state corruption during `/init`** – The #2478 bug is the most acute: users lose plan-mode tool bindings mid-session, forcing restarts. The fix in #2489 is urgent.
2. **Poor first-run experience on fresh installs** – `LLMNotSet` with zero guidance is a common complaint. PR #2488 directly addresses this.
3. **Windows terminal compatibility** – Broken ANSI colors, path parsing crashes, and missing package manager support make the CLI nearly unusable on Windows without workarounds.
4. **No session history** – Losing context on every `exit` is a daily annoyance for heavy users. Persistence is the #1 unaddressed feature.
5. **Lack of proxy support** – Blocks adoption in corporate and academic networks with strict egress policies.
6. **Web UI Safari bugs** – IME composition issues (PR #1815) and layout problems (PR #2353) point to broader cross-browser testing debt.

---

*Generated from GitHub data for 2026-07-11. For real-time updates, watch [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli).*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-11

## Today’s Highlights
The community is abuzz over the upcoming **V2 TUI**, with a wave of polish issues and UX fixes landing today from `kitlangton` and `thdxr`. Meanwhile, the long-running debate on **default permissions** remains the most commented issue, and the **GPT-5.6 Luna** model integration hit a snag with ChatGPT OAuth users. New model support and Copilot OAuth porting to V2 are the headline PRs, alongside fixes for subagent navigation, session output caps, and CodeMode promise chaining.

## Releases
No new releases in the last 24 hours.

## Hot Issues (Top 10)

1. **#2632 – Default permissions allow editing files and executing any commands**  
   *Author: NaikSoftware | Comments: 22 | 👍: 4*  
   A long-standing security concern — OpenCode’s default “allow all” behavior is compared unfavorably to other AI tools that prompt for consent on edits and dangerous commands. The issue is **closed**, suggesting a fix or policy change landed.  
   [Link](https://github.com/anomalyco/opencode/issues/2632)

2. **#10288 – Feature Request: Mobile version of OpenCode (Android/iOS/Web UI)**  
   *Author: az0307 | Comments: 14 | 👍: 89*  
   The **most upvoted open feature request**. Developers want mobile AI coding assistance while on the go. No official response yet, but the upvote count signals strong demand.  
   [Link](https://github.com/anomalyco/opencode/issues/10288)

3. **#26772 – [FEATURE]: Integrated browser for desktop**  
   *Author: AlexDelgado20 | Comments: 12 | 👍: 3*  
   Users want an in-app browser to inspect and interact with web pages during agent sessions. A niche but concrete productivity request.  
   [Link](https://github.com/anomalyco/opencode/issues/26772)

4. **#34743 – opencode ACP from Xcode 27 beta 2 uses default model ignoring config**  
   *Author: velouria | Comments: 12 | 👍: 0*  
   Xcode integration bug: the ACP agent ignores `opencode.json` and the TUI-selected model, always falling back to `big-pickle`. Affects LMStudio and Ollama users.  
   [Link](https://github.com/anomalyco/opencode/issues/34743)

5. **#36140 – GPT-5.6 Luna returns model not found with ChatGPT OAuth**  
   *Author: AidenGeunGeun | Comments: 11 | 👍: 45*  
   Highly upvoted — `gpt-5.6-luna` is listed but returns HTTP 404. Reproduced from a clean dev checkout. Blocks users migrating to the new model. A fix PR (#36143) is already open.  
   [Link](https://github.com/anomalyco/opencode/issues/36140)

6. **#14970 – SQLite database corruption when running concurrent sessions on NFS**  
   *Author: jerry-xu0514 | Comments: 10 | 👍: 19*  
   Concurrent sessions on NFS-mounted home directories corrupt the shared SQLite DB. Related to earlier issues (#21215, #19521). Persists despite prior fixes.  
   [Link](https://github.com/anomalyco/opencode/issues/14970)

7. **#9532 – Frequent tool calling errors when using Claude**  
   *Author: soulmz | Comments: 7 | 👍: 3*  
   Models attempt to call unavailable tools like `ProxyRead`, resulting in repeated `invalid` tool errors. Suggests a mismatch between advertised and available tool sets for Claude.  
   [Link](https://github.com/anomalyco/opencode/issues/9532)

8. **#36302 – feat(tui): unify modal interaction and visual behavior**  
   *Author: kitlangton | Comments: 5 | 👍: 0*  
   V2 TUI audit: 37 dialog components reviewed, 20 states reproduced. Decision surface for focused fixes. Important for the V2 polish cycle.  
   [Link](https://github.com/anomalyco/opencode/issues/36302)

9. **#36285 – [bug, perf, 2.0] Managed-service restart causes reconnect herd and resource spikes**  
   *Author: kitlangton | Comments: 3 | 👍: 0*  
   V2 TUI during auto-update triggers a cascade: service replacement, cold-boot of many location graphs, delayed SSE, and slow rendering. A significant performance bug.  
   [Link](https://github.com/anomalyco/opencode/issues/36285)

10. **#35828 – Windows TUI fails when project .opencode already exists**  
    *Author: BB-84C | Comments: 3 | 👍: 2*  
    Windows-specific startup crash: `Config.loadInstanceState` fails trying to create an already-existing `.opencode` directory. Affects v1.17.15.  
    [Link](https://github.com/anomalyco/opencode/issues/35828)

## Key PR Progress (Top 10)

1. **#36339 – feat(codemode): support Promise.any and new Promise construction**  
   *Author: rekram1-node | Status: OPEN*  
   Implements `Promise.any` as the De Morgan dual of `Promise.all` and `new Promise(executor)` in the CodeMode sandbox. Follows up on #36304.  
   [Link](https://github.com/anomalyco/opencode/pull/36339)

2. **#36337 – fix(tui): make composer close action discoverable**  
   *Author: thdxr | Status: CLOSED*  
   Adds a clickable `esc` hint to the composer header, removes redundant footer copy. Closes #36322 (subagent view navigation).  
   [Link](https://github.com/anomalyco/opencode/pull/36337)

3. **#36338 – fix(tui): fork messages with agent attachments**  
   *Author: thdxr | Status: OPEN*  
   Fixes `DataCloneError` when forking messages with Solid store-backed agent attachments.  
   [Link](https://github.com/anomalyco/opencode/pull/36338)

4. **#36143 – fix(opencode): support GPT-5.6 Responses Lite**  
   *Author: AidenGeunGeun | Status: OPEN*  
   Fixes #36140 by routing GPT-5.6 Luna through the correct API envelope (Responses Lite) instead of the legacy one.  
   [Link](https://github.com/anomalyco/opencode/pull/36143)

5. **#36336 – [contributor] feat(core): port GitHub Copilot OAuth**  
   *Author: opencode-agent[bot] | Status: CLOSED*  
   Ports GitHub.com and Enterprise Copilot device OAuth to the V2 integration registry, including credential-aware headers and remote model syncing.  
   [Link](https://github.com/anomalyco/opencode/pull/36336)

6. **#7756 – feat(task): Add subagent-to-subagent delegation with budgets, persistent sessions**  
   *Author: NamedIdentity | Status: CLOSED*  
   Massive feature — adds hierarchical delegation, persistent sessions, and budget management. Closes #7296, #6183, #3291.  
   [Link](https://github.com/anomalyco/opencode/pull/7756)

7. **#34794 – feat(provider): add --model free to pick a random zero-cost model**  
   *Author: caretak3r | Status: OPEN*  
   New `--model free` flag for `opencode run` and TUI, randomly selecting from OpenCode Zen zero-cost models.  
   [Link](https://github.com/anomalyco/opencode/pull/34794)

8. **#36275 – [contributor] fix(cli): report mismatched service status**  
   *Author: kitlangton | Status: OPEN*  
   Improves `service status` output to report JSON inspection states, distinguishing healthy daemons even when versions differ.  
   [Link](https://github.com/anomalyco/opencode/pull/36275)

9. **#36333 – [contributor] fix(core): cap session output tokens**  
   *Author: opencode-agent[bot] | Status: OPEN*  
   Caps V2 provider turns at 32,000 output tokens, preventing models from consuming their entire context window.  
   [Link](https://github.com/anomalyco/opencode/pull/36333)

10. **#36304 – feat(codemode): support promise chaining with .then/.catch/.finally**  
    *Author: rekram1-node | Status: CLOSED*  
    Adds promise chaining to the CodeMode sandbox, building on #35782. Each reaction returns a new scope-owned promise.  
    [Link](https://github.com/anomalyco/opencode/pull/36304)

## Feature Request Trends
- **Mobile & Web UI** (#10288, 👍89): The top-voted request — users want AI coding assistance outside the terminal.
- **Integrated Browser** (#26772): Desktop users want to inspect web pages during agent sessions.
- **Interactive Steering** (#19205, 👍26): Ability to nudge or redirect agents mid-task, inspired by GPT-5.4 capabilities.
- **Shell RC Files** (#36308): Request for interactive shell mode that loads `.zshrc`/`.bashrc` so aliases and plugins are available.
- **V2 Polish & Performance**: Multiple issues focus on TUI consistency (#36302), startup speed (#36285), and provider label simplification (#36270).
- **Nix Support** (#34671, #36328): Community wants V2 branch CI and build support for Nix systems.

## Developer Pain Points
1. **Security defaults** (#2632): The “allow all” default permissions remain a trust and safety concern, though the issue is now closed.
2. **SQLite concurrency** (#14970, #33320): Database corruption and lock errors under concurrent sessions on NFS persist as a reliability issue.
3. **Model compatibility gaps**: GPT-5.6 Luna not working with ChatGPT OAuth (#36140) and GPT-5.6 Sol failing with `reasoning part not found` (#36241) slow model adoption.
4. **Xcode integration** (#34743): ACP agent ignores user model configuration, causing frustration for macOS developers.
5. **Server/Herd behavior** (#36285): Managed-service restart during V2 TUI use causes resource spikes and slow rendering — a critical UX bug.
6. **Windows stability** (#35828): TUI startup crashes when `.opencode` directory already exists, making upgrading painful.
7. **Misleading persistence** (#36326): Users report being told conversations are persistent when they are not, erasing work after shutdown.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-11

## Today's Highlights

The community is buzzing around the GPT-5.6 Sol/Terra/Luna rollout, driving a wave of catalog updates and feature additions across GitHub Copilot and OpenAI Codex providers. A critical `httpIdleTimeoutMs` regression in v0.80.6 is affecting self-hosted users, while several embedded library and session lifecycle bugs continue to surface as Pi sees increased embedding usage. Six pull requests merged in the last 24 hours, including constrained sampling support and OpenRouter session affinity.

## Releases

No new versions released in the last 24 hours. The latest stable remains **v0.80.6**.

## Hot Issues

1. **[#6475 — Add GPT-5.6 (Sol/Terra/Luna) to GitHub Copilot provider catalog](https://github.com/earendil-works/pi/issues/6475)** (8 comments, 6 👍)  
   Top-voted open issue. GitHub Copilot rolled out GPT-5.6 models yesterday; Pi's catalog needs entries for `gpt-5.6-sol`, `gpt-5.6-terra`, and `gpt-5.6-luna`. Community urgency is high.

2. **[#6476 — Regression: httpIdleTimeoutMs no longer respected for self-hosted providers (v0.80.6)](https://github.com/earendil-works/pi/issues/6476)** (5 comments)  
   Critical regression: requests to vLLM/OpenAI-compatible endpoints time out after minutes despite configured `httpIdleTimeoutMs`. Downgrading to v0.80.3 resolves it. In-progress fix via Bun bump.

3. **[#6206 — Clamping to context window prevents artificial context limits](https://github.com/earendil-works/pi/issues/6206)** (8 comments)  
   A prior fix for infinite loops now forces `max_tokens` to equal model context window, breaking users who intentionally set lower limits. Complex tradeoff between safety and configurability.

4. **[#6300 — Windows TUI: input redrawn on every keystroke](https://github.com/earendil-works/pi/issues/6300)** (5 comments)  
   Terminal input renders each character on a new line in cmd.exe and Windows Terminal. Significant UX blocker for Windows developers.

5. **[#6303 — Exponential retry backoff has no cap; unbounded delays](https://github.com/earendil-works/pi/issues/6303)** (4 comments, 1 👍)  
   `getRetrySettings()` omits `maxDelayMs`, so retry delays grow exponentially (~4 minutes by attempt 7). Configurable `maxRetryDelayMs` exists but is not wired.

6. **[#6366 — Support session IDs for OpenRouter](https://github.com/earendil-works/pi/issues/6366)** (7 comments)  
   OpenRouter expects `x-session-id` header or `session_id` JSON field; Pi sends the wrong format, breaking prompt caching. Fixed in PR #6496.

7. **[#6477 — Compaction summary requests omit session ID, breaking on OpenAI-Codex](https://github.com/earendil-works/pi/issues/6477)** (2 comments, 2 👍)  
   Compaction fails entirely on OpenAI Codex's new GPT-5.6 models because the session ID is missing from summarization requests.

8. **[#6472 — compaction.enabled=false bypassed by overflow recovery path](https://github.com/earendil-works/pi/issues/6472)** (2 comments)  
   Setting `compaction.enabled: false` does not fully disable compaction; the overflow recovery path ignores the flag and compacts anyway.

9. **[#6097 — Add support for 'max' thinking level](https://github.com/earendil-works/pi/issues/6097)** (2 comments, 17 👍)  
   Most-upvoted open feature request. GPT-5.6 Sol introduces a sixth thinking level `max`; Anthropic's Opus already supports it. Community strongly wants parity.

10. **[#6485 — Preserve Bedrock ConverseStream stop reasons in errors](https://github.com/earendil-works/pi/issues/6485)** (3 comments)  
    Unknown stop reasons from Bedrock are silently swallowed instead of propagated in error messages, making debugging difficult.

## Key PR Progress

1. **[#6341 — feat(ai): support constrained sampling](https://github.com/earendil-works/pi/pull/6341)** (OPEN)  
    Adds `constrainedSampling` tool config for provider-side JSON-schema and grammar-constrained tool argument generation. Opt-in; no breaking changes.

2. **[#6496 — fix(ai): support OpenRouter session affinity](https://github.com/earendil-works/pi/pull/6496)** (CLOSED)  
    Fixes #6366 by sending `x-session-id` header and `session_id` in JSON body for OpenRouter, enabling prompt caching and sticky sessions.

3. **[#6503 — bump bun to 1.3.14](https://github.com/earendil-works/pi/pull/6503)** (CLOSED)  
    Bumps Bun to 1.3.14 which supports `BUN_CONFIG_HTTP_IDLE_TIMEOUT`. Workaround for #6476's timeout regression; global `httpIdleTimeoutMs` alone cannot override Bun's built-in 5-minute idle timeout.

4. **[#6489 — feat(ai): add ultra thinking level](https://github.com/earendil-works/pi/pull/6489)** (CLOSED)  
    Adds `ultra` as a first-class thinking level across all surfaces. GPT-5.6 Sol and Terra use Ultra; Luna stays at Max. Maps to API `reasoning.effort: ultra`.

5. **[#6474 — feat(ai): support message-anchored tool loading](https://github.com/earendil-works/pi/pull/6474)** (CLOSED)  
    Allows tools to be introduced mid-conversation via `addedTools`, eliminating the need to declare every tool upfront. Supports Anthropic tool-reference backend.

6. **[#6506 — feat: add configurable auto-update on new session](https://github.com/earendil-works/pi/pull/6506)** (CLOSED)  
    New `autoUpdateOnNewSession` setting runs `pi update --all` automatically at session start. Disabled by default; aimed at power users.

7. **[#6505 — feat(coding-agent): add goal extension example](https://github.com/earendil-works/pi/pull/6505)** (CLOSED)  
    Official example for multi-turn autonomous goal execution with pause/resume/cancel lifecycle and session persistence. `/goal <objective>` syntax.

8. **[#6501 — fix(extensions,theme): support embedded library hosts](https://github.com/earendil-works/pi/pull/6501)** (CLOSED)  
    Fixes #6102 (theme Proxy throws "Theme not initialized") and partially #6101 (stale extension runtime across sessions). Critical for library embedding.

9. **[#6481 — fix openrouter models: use context length from top provider](https://github.com/earendil-works/pi/pull/6481)** (CLOSED)  
    Fixes #6378 where OpenRouter model context lengths were incorrect; now uses the top provider's reported limits.

10. **[#6216 — feat: Add Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/6216)** (OPEN)  
    New provider for Bedrock Mantle's OpenAI-compatible Responses API. Supercedes earlier effort; still under discussion.

## Feature Request Trends

- **GPT-5.6 model support** dominates: catalog entries, thinking level (`ultra`/`max`), and provider integration across GitHub Copilot, OpenAI Codex, and OpenRouter are the hottest area of activity.
- **Extension API expansion** is the second major theme: `ctx.ui.setUsage()` for cost reporting, `setExtensionUiContext()` for multi-agent switching, opaque RPC attachment fields, and `goal`-type autonomous task execution all signal growing interest in richer extension capabilities.
- **Provider-specific protocol nuance** continues to surface: OpenRouter session affinity, Bedrock stop reason preservation, and Cloudflare provider GLM compatibility issues show demand for deeper provider integration.

## Developer Pain Points

- **Self-hosted model timeouts** (#6476): The v0.80.6 regression has broken workflows for many self-hosted users, especially those running vLLM. Requires Bun upgrade as workaround.
- **Windows TUI broken** (#6300): Input rendering is fundamentally broken on Windows, representing a significant barrier for a large developer population.
- **Compaction bypasses user settings** (#6472, #6477): Users who explicitly disable compaction find it still triggers, and those who need it find it broken on new models. Configuration integrity is eroding.
- **Embedded library friction** (#6101, #6102, #6512): Multiple issues around theme initialization, stale extension runtimes, and module resolution point to remaining rough edges for library embedding use cases.
- **Settings not respected on initial load** (#6459): Custom keybindings and potentially other settings require a manual `/reload` to take effect, frustrating the immediate "first run" experience.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-11

## Today's Highlights

The project released v0.19.9 with critical fixes for subagent tool-call loops and broken session history chains, though the release pipeline itself encountered Docker integration test failures. The multi-workspace daemon RFC continues to gain momentum with 20 comments, driving a coordinated wave of PRs from the same contributor that add workspace-qualified extensions and channel routing. A notable spike in UI-related feature requests for the Web Shell composer toolbar suggests the team is investing heavily in the web-based interface as a first-class client alongside the CLI.

---

## Releases

**v0.19.9** — [Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.9)
- **Stop repeated subagent tool-call loops** ([PR #6543](https://github.com/QwenLM/qwen-code/pull/6543)) — addresses infinite loops where subagents repeatedly call the same tool without progress
- **Fix broken history chain detection** — sessions with malformed history chains are now explicitly marked rather than silently truncated, preventing subtle data loss

**v0.19.8-nightly.20260711** — [Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.8-nightly.20260711)
- **YOLO mode fix** ([PR #6630](https://github.com/QwenLM/qwen-code/pull/6630)) — prevents the model from reverting to Plan mode when calling `enter_plan_mode` internally
- **CLI: forward ask_user** — enables interactive user prompts through the CLI forwarding layer

---

## Hot Issues

| # | Issue | Why It Matters | Community Signal |
|---|-------|----------------|------------------|
| [#6378](https://github.com/QwenLM/qwen-code/issues/6378) | **RFC: Multiple workspaces in one daemon** | Addresses a core scalability bottleneck; single daemon currently = single workspace. 20 comments reflect strong interest from server/team deployments | Hot (20 comments) |
| [#5975](https://github.com/QwenLM/qwen-code/issues/5975) | **Stream timeout after 19 chunks** | Regression in v0.19.3 causes silent hangs before the dreaded 120s timeout. Users report frequent retries needed | 1 👍, 10 comments; high frustration |
| [#5970](https://github.com/QwenLM/qwen-code/issues/5970) | **Auto Plan mode from Yolo** | Users on `-y` flag expect no-interaction mode; internal mode switching violates that contract | Closed, confirmed fixed |
| [#6384](https://github.com/QwenLM/qwen-code/issues/6384) | **Hard limit: 0 on env-configured models** | Context compression calculates against zero hard limit, failing before any API request | 5 comments; affects custom model configs |
| [#6590](https://github.com/QwenLM/qwen-code/issues/6590) | **macOS clipboard paste broken** | Standalone macOS users cannot paste images via Ctrl+V; missing native binary in package | 4 comments; binary packaging issue |
| [#6654](https://github.com/QwenLM/qwen-code/issues/6654) | **Tool_use blocks missing tool_result** | API error causes session crashes; tool responses not properly paired with their calls | 4 comments; core protocol compliance |
| [#6629](https://github.com/QwenLM/qwen-code/issues/6629) | **Cron parser drops step values** | `5/15` matches only `5`, not stepping every 15 minutes; affects automation schedules | Auto-fix in progress |
| [#6600](https://github.com/QwenLM/qwen-code/issues/6600) | **`--debug` says logging but writes nothing** | Misleading UX: flag prints log path but file never created; wastes debugging time | 4 comments; easy footgun |
| [#6582](https://github.com/QwenLM/qwen-code/issues/6582) | **Mixed-language mode-switch UI** | Approval mode toggles show English and Chinese in the same UI; breaks user expectations for language setting | 3 comments; polish issue |
| [#6595](https://github.com/QwenLM/qwen-code/issues/6595) | **qwen3.7-max leaks `<analysis>` tags** | Protocol tags appearing in normal assistant output causes follow-up actions to stop | Model-specific, confirmed closed |

---

## Key PR Progress

| # | PR | What It Does | Status |
|---|----|--------------|--------|
| [#6697](https://github.com/QwenLM/qwen-code/pull/6697) | **Resume stopped sessions on Web Shell load** | Automatically continues interrupted turns when Web Shell loads or restarts; key for crash recovery UX | Open |
| [#6681](https://github.com/QwenLM/qwen-code/pull/6681) | **Lifecycle-safe goal evaluation** | Prevents `/goal` from evaluating while background agents or workflows are still running; eliminates false negatives | Open |
| [#6580](https://github.com/QwenLM/qwen-code/pull/6580) | **Subagent observability improvements** | Live untruncated command display, transcript path, and approval context; helps debug subagent behavior | Open |
| [#6678](https://github.com/QwenLM/qwen-code/pull/6678) | **Full reasoning content on expand** | Alt+T now renders full thinking content via MarkdownDisplay instead of 4-line tail preview | Open |
| [#6680](https://github.com/QwenLM/qwen-code/pull/6680) | **Recover daemon sessions after restarts** | Preserves channel conversations across daemon restarts; lazily reloads historical sessions | Open |
| [#6682](https://github.com/QwenLM/qwen-code/pull/6682) | **Memory-pressure check in TUI** | Prevents OOM on quit by adding periodic memory checks outside tool-call boundaries | Open |
| [#6683](https://github.com/QwenLM/qwen-code/pull/6683) | **Retry leaked protocol turns** | Extends `<analysis>/<summary>` leak guard to handle cases including tool-call-bearing leaked turns | Open |
| [#6638](https://github.com/QwenLM/qwen-code/pull/6638) | **Workspace-qualified extensions REST** | Enables per-workspace extension management endpoint for multi-workspace daemon | Open |
| [#6635](https://github.com/QwenLM/qwen-code/pull/6635) | **Group channel workers by workspace** | Phase 4b of multi-workspace: daemon-managed channels now work for non-primary workspaces | Open |
| [#6440](https://github.com/QwenLM/qwen-code/pull/6440) | **`/learn` command for skill creation** | Users can create reusable skills from local directories, URLs, or conversation history | Open |

---

## Feature Request Trends

1. **Multi-workspace daemon** — [#6378](https://github.com/QwenLM/qwen-code/issues/6378) and follow-ups [#6646](https://github.com/QwenLM/qwen-code/issues/6646), [#6700](https://github.com/QwenLM/qwen-code/issues/6700) show strong demand for a single `qwen serve` process serving multiple isolated workspaces. This is the dominant architectural topic.

2. **Web Shell as first-class UI** — Three feature requests ([#6699](https://github.com/QwenLM/qwen-code/issues/6699), [#6700](https://github.com/QwenLM/qwen-code/issues/6700), [#6701](https://github.com/QwenLM/qwen-code/issues/6701)) propose redesigning the composer toolbar with workspace selector, git branch display, and execution context picker — directly inspired by the Codex desktop client.

3. **Session continuity** — [#6695](https://github.com/QwenLM/qwen-code/issues/6695) and [#6701](https://github.com/QwenLM/qwen-code/issues/6701) both request automatic continuation of interrupted sessions after restarts, suggesting this is a pain point for long-running automation workflows.

4. **SDK interactivity** — [#6647](https://github.com/QwenLM/qwen-code/issues/6647) calls for `ask_user_question` support in both TypeScript and Python SDKs, enabling interactive tool calls from SDK-driven sessions.

5. **GitHub Actions security** — [#6597](https://github.com/QwenLM/qwen-code/issues/6597) proposes automated moderation for suspicious comment attachments (archives, binaries) in community discussions.

---

## Developer Pain Points

- **Stream timeout regression** — Issue [#5975](https://github.com/QwenLM/qwen-code/issues/5975) continues to draw attention: v0.19.3 introduced a 120-second stream timeout that triggers after 19 chunks, replacing a previous silent hang. Users must retry repeatedly, disrupting workflow.

- **Protocol compliance failures** — Multiple issues ([#6654](https://github.com/QwenLM/qwen-code/issues/6654), [#6595](https://github.com/QwenLM/qwen-code/issues/6595)) involve the model emitting malformed message sequences (missing `tool_result` blocks, leaked `<analysis>` tags), causing session crashes or stopped follow-up actions.

- **macOS packaging gaps** — [#6590](https://github.com/QwenLM/qwen-code/issues/6590) reveals that the standalone macOS distribution ships without the native clipboard module, silently breaking image paste. The error is only logged to `debugLogger` with no user-facing signal.

- **Misleading debug flag** — [#6600](https://github.com/QwenLM/qwen-code/issues/6600): `--debug` prints a log path but never writes the file, wasting troubleshooting time.

- **OOM in glob tool** — [#6614](https://github.com/QwenLM/qwen-code/issues/6614): The Node.js process can hit heap limits when `glob` searches large directories before any output truncation kicks in. Fixed in the release cycle.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

Here is the **DeepSeek TUI Community Digest** for **2026-07-11**, based on the provided GitHub data for the `Hmbown/CodeWhale` repository (which appears to be the active development fork for CodeWhale, the TUI client for DeepSeek).

---

## DeepSeek TUI Community Digest — 2026-07-11

### 1. Today's Highlights
The project is solidifying the **v0.8.68 release** with a heavy focus on the **Fleet/Workflow/Lane/Runtime** orchestration model. A batch of stopship TUI bugs (provider configuration display, blank fields, session restore) has been resolved via a rapid-fire integration PR from the maintainer. Meanwhile, external contributors are strengthening security posture by integrating `cargo-deny` and auditing dependencies, signaling a maturing codebase.

---

### 2. Releases
**No new releases were published in the last 24 hours.** The project is in a release stabilization phase, merging final integration fixes for v0.8.68.

---

### 3. Hot Issues
1. **#4032: CodeWhale Not Following the Constitution** — A recurring frustration where the agent ignores user-provided scripts despite a defined "constitution." High engagement (33 comments) indicates deep frustration with agent compliance.
2. **#4092: v0.8.68 Execution Board (Canonical Agent Packet)** — The single source of truth for the milestone; centralizes lane labels and agent protocol. 60 comments (most in the repo) show intense internal coordination.
3. **#4175: Fleet / Workflow / Lane / Runtime Product Model** — The canonical architecture tracker. This is the "north star" for the new orchestration vocabulary, preventing concept collapse.
4. **#4236: Epic: Official Termux / Android arm64 Support** — Users are demanding native Android TUI support. This blocks the v0.8.68 release and has spawned a dedicated QA issue (#4242).
5. **#4329: Anthropic API Error (Tool Use Mismatch)** — A runtime bug where the agent fails to pair `tool_use` blocks with `tool_result` blocks, causing a 400 Bad Request. Critical for reliability.
6. **#4333: Configured Picker Treats Empty Provider Headers as Configured** — A UX regression where blank TOML tables cause the TUI to show unavailable models as "configured." Low-level but high-impact for v0.8.68.
7. **#4334: Custom Provider Identity Collapses on Session Restore** — Users with custom proxies (`lm-studio`, `my-openai-proxy`) lose provider identity after resume, breaking model routing.
8. **#4335: Offline Scorecard Not Provider-Aware** — Pricing estimates are wrong when the same model name uses different provider pricing. A subtle but important cost-reporting bug.
9. **#2984: OpenAI Codex/ChatGPT OAuth Route Verification** — A long-standing UX request to move the OAuth route from preview to stable. Low activity but high importance for enterprise users.
10. **#3976: Seed Project-Scoped Memory** — A v0.8.68 feature to give agents lightweight per-project recall before the full external-memory backend lands. Strong signal for better context management.

---

### 4. Key PR Progress
1. **#4337: Integrate v0.8.68 TUI and Android QA** — Landed final cancelled-shell transcript state and Android image authentication. The last integration delta before release.
2. **#4336: Dispatch Durable Lanes Without Root Model** — Allows `codewhale workflow run` to bypass the operator-model turn, preserving all runtime config. A major architectural win.
3. **#4332: Fix v0.8.68 TUI State and Routing (Stopship Batch)** — Fixes the "blank provider header" bug (#4333), malformed auth display, and session restore quirks. LGTM-critical.
4. **#4331: Align v0.8.68 Mode FAQ and Workflow Commands** — Replaces non-existent `workflow status` with correct `lane status` in docs. Critical for user onboarding.
5. **#4328: Upgrade Dependencies to Fix Cargo-Audit Vulnerabilities** — Fixes a stack overflow in `lopdf` and a pointer dereference in `crossbeam-epoch`. Security-first PR from community contributor `bistack`.
6. **#4330: Update cargo-deny Advisory Ignore List** — Clears `lopdf` CVE and add ignores for transitive unmaintained crates (`derivative`, `fxhash`). Good dependency hygiene.
7. **#4272: CI: Add RustSec Security Audit and Cargo-Deny Checks** — Introduces non-blocking `cargo-audit` and blocking `cargo-deny` pipelines. Raises the security bar.
8. **#3969: Add Per-Sub-Agent Provider Routing** — Held for v0.8.68 fleet lane; needs rebase to match new profile fields. A key feature for multi-modal subagents.
9. **#4342: Bump `rmcp` from 1.8.0 to 2.2.0** — Major version bump for the MCP Rust SDK. Could bring new protocol features or breaking changes; needs careful review.
10. **#4339: Bump `jsonschema` from 0.46.4 to 0.47.0** — Dependency bump for validation logic. No breaking changes expected.

---

### 5. Feature Request Trends
- **Fleet/Workflow/Lane/Runtime Model** — The overwhelming majority of open issues target the new orchestration paradigm, with sub-features for role-to-role handoffs (#4179), lane dispatching (#4110), and profile separation (#4177).
- **Termux/Android Native Support** — Multiple issues (#4236, #4242) request official Android arm64 builds with shell, PTY, and TUI startup QA.
- **Sidebar Session Panel** — Issue #2934 requests a persistent sidebar for session management, reducing reliance on hotkeys (`Ctrl+R`) and improving discoverability.
- **Project-Scoped Memory** — Seed recall (#3976) is a lightweight stopgap before a full external-memory backend. Users want contextual awareness per-project.
- **OpenAI OAuth Route Stabilization** — Issue #2984 seeks to graduate the Codex/ChatGPT OAuth path from preview to supported status, including usage display.

---

### 6. Developer Pain Points
- **Agent Compliance** — Issue #4032 ("not following the constitution") reflects deep frustration with the agent prioritizing its own scripts over user-provided ones, despite explicit guidelines.
- **Anthropic Tool Use Reliability** — Issue #4329 reveals a frequent HTTP 400 error with Anthropic APIs where `tool_use` is missing a `tool_result`. This breaks multi-turn tool workflows.
- **Provider Identity Fragility** — Issues #4334 and #4333 highlight that custom providers lose identity on session restore and empty config fields are misinterpreted, causing model routing confusion.
- **Cost Reporting Inaccuracy** — Issue #4335 shows that the offline scorecard ignores provider-specific pricing, leading to misleading cost estimates for custom or proxied endpoints.
- **Chaotic Default TUI** — Issue #4092 notes that the default TUI presentation is "too busy," exposing low-level activity. Users want compact mode as the default to reduce cognitive load.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*