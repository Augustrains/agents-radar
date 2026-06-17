# AI CLI Tools Community Digest 2026-06-17

> Generated: 2026-06-17 02:29 UTC | Tools covered: 9

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

# AI CLI Developer Tools Cross-Tool Comparison Report
**Date:** 2026-06-17

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape is experiencing rapid maturation with divergent stability trajectories. Across seven major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI (rebranding to CodeWhale)—the community is converging on shared pain points around session reliability, MCP integration, and agent orchestration while each tool carves distinct philosophical niches. The ecosystem is bifurcating between **platform-first tools** (Claude Code, Codex, Copilot CLI) tightly coupled to their vendor ecosystems, and **aggregator tools** (OpenCode, Pi, Qwen Code) that prioritize provider flexibility. Critical regression velocity remains a concern across the board, with Windows and macOS platform parity emerging as the most consistent under-served demand.

---

## 2. Activity Comparison

| Tool | Open Issues | PRs Active (24h) | Release Activity (24h) | Community Engagement Level |
|---|---|---|---|---|
| **Claude Code** | ~10 hot issues | 10 PRs (9 open, 1 merged) | **v2.1.179** shipped | Very High (sustained, mature) |
| **OpenAI Codex** | ~10 hot issues | 10 PRs (all open) | 2 Rust alpha releases (v0.141.0-a.3/4) | High (strong voting culture) |
| **Gemini CLI** | ~10 hot issues | 10 PRs (1 closed, 9 open) | No release | High (P1 bugs active) |
| **GitHub Copilot CLI** | ~10 hot issues | 0 PRs | **v1.0.64-0** shipped | Moderate (enterprise-leaning) |
| **Kimi Code CLI** | 4 issues updated | 1 PR | No release | Low (smallest community) |
| **OpenCode** | ~10 hot issues | 10 PRs (4 merged, 6 open) | No release | Very High (most voted features) |
| **Pi** | ~10 hot issues | 10 PRs (all open) | **v0.79.5, v0.79.6** shipped | Moderate (niche/enthusiast) |
| **Qwen Code** | ~10 hot issues | 10 PRs (all open) | **v0.18.1-preview.0** shipped | Moderate-High (rapid feature iteration) |
| **DeepSeek TUI (CodeWhale)** | ~10 hot issues | 10 PRs (8 closed, 2 open) | **v0.8.61 (rebrand)** shipped | Moderate (rebranding transition) |

**Key observations:**
- **Codex** and **OpenCode** dominate in community voting engagement (87 👍 on OpenCode's top feature request)
- **Gemini CLI** has highest-priority active bugs (2 P1 issues open 3+ months)
- **Copilot CLI** shows zero PR activity—suggests closed/internal development model
- **Kimi Code CLI** has lowest activity; may be lagging in community investment
- **Claude Code** and **OpenCode** show the most balanced issue/PR/release cadence

---

## 3. Shared Feature Directions

| Common Requirement | Tools Affected | Specific Need |
|---|---|---|
| **Multi-Agent Coordination** | Claude Code, Gemini CLI, CodeWhale, Qwen Code | Agent hangs, false success reporting, deadlocks, coordination bugs (12 identified in Claude Code alone) |
| **MCP Plugin/Server Reliability** | Claude Code, Codex, Gemini CLI, Copilot CLI, Kimi Code, Pi, Qwen Code | OAuth token persistence, auto-discovery bugs, sub-agent tool isolation, Unicode headers, atomic writes, cross-server URI confusion |
| **Session Lifecycle Control** | Codex, Copilot CLI, OpenCode, Claude Code | `/cwd` commands, `/goal` persistent objectives, session resumption, worktree cleanup, archive/restore bugs |
| **Platform Parity (Windows/macOS)** | Claude Code, Codex, Copilot CLI, Gemini CLI, OpenCode, Pi, CodeWhale | Silent tool drops, PTY leaks, non-ASCII path crashes, GPU process issues, clipboard bugs, scroll regressions |
| **Smarter Context Management** | Claude Code, OpenCode, Pi, Gemini CLI | Tool response diffing, configurable fallback chains, oversized context warnings, CPU inefficiency from high token overhead |
| **Provider Model Flexibility** | Pi, Qwen Code, CodeWhale, OpenCode | Provider-specific config consolidation, thinking model compatibility, model metadata registries, multi-provider fallback |
| **Security Hardening** | Claude Code, Gemini CLI, Codex, Qwen Code | Symlink escape blocking, shell injection fixes, credential brokers, artifact poisoning prevention, atomic token writes |

**Cross-cutting insight:** **MCP plugin reliability** is the single most universally-shared pain point—every tool except Kimi Code CLI has active issues around MCP OAuth token handling, auto-discovery, or tool isolation. This suggests the MCP ecosystem is still in early standardization.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | CodeWhale |
|---|---|---|---|---|---|---|---|---|---|
| **Primary Model** | Anthropic Claude | OpenAI GPT | Google Gemini | OpenAI GPT (via Copilot) | Moonshot Kimi | Multi-provider | Multi-provider | Qwen / Multi | DeepSeek / Multi |
| **Architecture Philosophy** | Platform-first (Claude ecosystem) | Platform-first (OpenAI ecosystem) | Platform-first (Google ecosystem) | Platform-first (GitHub ecosystem) | Platform-first (Moonshot) | **Aggregator** | **Aggregator** | **Aggregator** | **Aggregator** |
| **Target User** | Professional devs, monorepo teams | TUI power users, Rust SDK users | Google Cloud / AI Studio ecosystem | Enterprise GitHub shops | Moonshot cloud users | Self-hosters, price-sensitive | Enthusiasts, Nix users | ML engineers, Chinese market | Open-source hackers |
| **Differentiator** | Highest MCP extensibility, JetBrains gap | Session management heaviest focus | Agent reliability issues dominant | Enterprise model support gap, MCP isolation | Smallest scope, basic UX issues | Highest community feature engagement | Most provider model compat work | Fastest multi-agent + `/loop` iteration | Rebranding to CodeWhale, Hippocampal memory system |
| **Windows Support** | **Poor** (2 critical bugs) | **Poor** (non-ASCII crashes) | **Moderate** | **Moderate** | Unknown | **Poor** (SIGILL, clipboard) | **Moderate** | **Poor** (AV false positive) | **Moderate** |
| **Open Source Model** | Partially open (plugin ecosystem) | Closed source | Closed source | Closed source | Closed source | **Fully open** | **Fully open** | **Fully open** | **Fully open** |

**Key differentiators:**
- **Claude Code** leads in plugin/MCP extensibility but has the most severe Windows regressions
- **OpenCode** has the most engaged community (87 👍 on top feature) and strongest feature voting culture
- **Pi** and **Qwen Code** are iterating fastest on provider model compatibility (thinking models, fallback chains)
- **Gemini CLI** has the highest-severity unresolved bugs (agent hangs, false success reporting)
- **CodeWhale** is undergoing identity rebranding while investing in memory systems (Hippocampal v2)
- **Copilot CLI** follows a closed, enterprise release model with zero community PR visibility

---

## 5. Community Momentum & Maturity

**High Momentum (Rapid Iteration / Growing Community):**
- **Qwen Code** — Fastest feature iteration this week: `/loop` alignment, QQ Bot channel, vision bridge, multi-model fallback. Release pipeline showed failure but fixes are rapid.
- **Pi** — Two patch releases in 24 hours, 10 active PRs. Tight feedback loop between bugs and fixes. Nix packaging signals growing infrastructure community.
- **OpenCode** — Highest community engagement (87 👍, 50 comments on top feature). Auto-cleanup batch (5 merged PRs) shows active maintenance investment.

**Stable / Mature (Established user base, slower iteration):**
- **Claude Code** — Highest issue volume but established maturity. The 14-PR wave from contributor AZERDSQ131 signals healthy open-source contribution pipeline. Regression velocity is a growing concern.
- **OpenAI Codex** — Strong voting culture but Rust alpha releases suggest core architecture still in flux. Session data loss bugs are top concern.
- **Gemini CLI** — Most critical unresolved bugs (2 P1 issues open 3+ months). Community trust may erode if agent hangs and false success issues persist.

**Emerging / Transitional:**
- **CodeWhale (DeepSeek TUI)** — Rebranding is a double-edged signal: fresh identity but migration friction. Hippocampal memory v2 PR is ambitious. Stalled-turn bug (#2487) is a reliability red flag.
- **Kimi Code CLI** — Lowest activity. Few issues, 1 PR. Risk of stagnation unless community investment increases.
- **Copilot CLI** — Zero PR visibility suggests closed development. `/diagnose` and `/security-review` GA are good signals but community cannot see roadmap.

**Community Sentiment Summary:**
- **Trust erosion risk**: Gemini CLI (unresolved P1 bugs), Claude Code (regression velocity), CodeWhale (stalled turns)
- **Trust strength**: OpenCode (responsive, feature voting), Pi (fast patches), Qwen Code (rapid feature delivery)

---

## 6. Trend Signals

### 6.1 The MCP Standardization Gap
Every tool has MCP-related issues—OAuth token handling, auto-discovery, sub-agent isolation, cross-server URI confusion. The community is pushing MCP harder than the standardization work can support. **Recommendation:** Developers building MCP integrations should expect fragmentation across tools and budget for tool-specific shims.

### 6.2 Agent Autonomy vs. User Control Tension
Multiple tools (Gemini CLI #22672, CodeWhale #3275, OpenCode #27167) show users demanding more control over agent behavior: `/goal` commands, clarification UI, destructive command safeguards, safe modes. **The trend is toward** **structured agent lifecycle management** over open-ended autonomy. Tools that provide session-level objectives and explicit permission boundaries will win trust.

### 6.3 Platform Maturity Divergence
Windows and macOS are consistently second-class citizens across all tools. Issues span silent failures, non-ASCII paths, clipboard bugs, PTY leaks, and GPU process crashes. **This is a market opportunity**—any tool that invests in true cross-platform parity (especially Windows ARM64, macOS Tahoe) will capture frustrated users.

### 6.4 Provider Model Compatibility Debt
As models proliferate (DeepSeek V4 thinking, MiniMax M3, Moonshot/Kimi), aggregator tools (Pi, OpenCode, Qwen Code) are accumulating per-provider compatibility shims. **The industry needs a standardized tool-call format**—currently each provider has unique quirks (empty parameters, thinking replay, serialization errors).

### 6.5 Context Window Management Maturity
The 1M context window is becoming table stakes (Claude Code, OpenCode), but tools are struggling with: oversized context warnings, CPU overhead from token processing, and opaque usage billing. **Expect a new class of features**: tool response diffing/delta compression, configurable fallback chains, and per-provider concurrency limits.

### 6.6 Security Hardening Acceleration
A wave of security-focused PRs across Claude Code (symlink escape, shell injection), Gemini CLI (artifact poisoning, credential broker), and Qwen Code (atomic token writes) suggests the ecosystem is moving from "move fast" to "move securely." **Developers should expect** supply-chain security, credential management, and sandbox integrity to become table stakes within 6 months.

### 6.7 Rebranding/Identity Shifts
DeepSeek TUI → CodeWhale signals that standalone CLI tools are seeking distinct identities beyond their model provider names. **This may reflect** the maturation of AI CLI tools as product categories rather than just model wrappers.

---

## Summary Recommendation for Technical Decision-Makers

| Evaluation Criterion | Top Pick | Runner-Up |
|---|---|---|
| **Most stable for production** | Claude Code (despite regression velocity) | Copilot CLI (enterprise support) |
| **Best cross-provider flexibility** | OpenCode | Pi |
| **Fastest feature iteration** | Qwen Code | Pi |
| **Best community responsiveness** | OpenCode | Qwen Code |
| **Best for Windows users** | *None recommended* | *Copilot CLI least problematic* |
| **Best for MCP plugin developers** | Claude Code (most mature plugin ecosystem) | OpenCode (community plugins) |
| **Most security-conscious** | Gemini CLI (active hardening PRs) | Claude Code (AZERDSQ131 security wave) |
| **Best value for self-hosters** | Pi | OpenCode |

**Key watch item:** If Claude Code resolves its Windows critical bugs (#46767, #65514, #68287) and regression velocity, it remains the most complete offering. If not, OpenCode or Qwen Code could capture market share among multi-platform teams.

---

*Report generated from community digests of Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI (CodeWhale) activity as of 2026-06-17 23:59 UTC.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-17 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following pull requests have attracted the most community discussion and represent the most actively watched Skill submissions:

### 1. Add document-typography skill (#514)
**Author:** PGTBoos | **Status:** Open | **Updated:** 2026-03-13
[View PR →](https://github.com/anthropics/skills/pull/514)

**Functionality:** Prevents common typographic defects in AI-generated documents—orphan word wrap (1–6 words spilling to next line), widow paragraphs (headers stranded at page bottom), and numbering misalignment. Addresses systemic quality issues affecting every document Claude generates.

**Discussion highlights:** The community recognizes this as solving a universal pain point. No significant objections; discussion centers on scope boundaries (whether to include LaTeX-specific rules) and integration depth with existing document skills.

---

### 2. Add ODT skill (#486)
**Author:** GitHubNewbie0 | **Status:** Open | **Updated:** 2026-04-14
[View PR →](https://github.com/anthropics/skills/pull/486)

**Functionality:** Enables creation, template filling, and reading/conversion of OpenDocument Format files (.odt, .ods, ODF). Triggers on mentions of LibreOffice, OpenDocument, or open-source document formats.

**Discussion highlights:** High demand from enterprise users who rely on LibreOffice/OpenOffice ecosystems. Key discussion points: handling complex ODT templates, metadata preservation, and interoperability with the existing DOCX skill.

---

### 3. Improve frontend-design skill clarity (#210)
**Author:** justinwetch | **Status:** Open | **Updated:** 2026-03-07
[View PR →](https://github.com/anthropics/skills/pull/210)

**Functionality:** Substantial revision to the frontend-design skill, emphasizing actionable instructions Claude can follow within a single conversation. Improves specificity, coherence, and practical steerability.

**Discussion highlights:** Strong community interest in skill quality refinement. The PR represents a pattern many contributors want to replicate—improving existing skills rather than only creating new ones.

---

### 4. Add skill-quality-analyzer and skill-security-analyzer (#83)
**Author:** eovidiu | **Status:** Open | **Updated:** 2026-01-07
[View PR →](https://github.com/anthropics/skills/pull/83)

**Functionality:** Two meta-skills: (1) a quality analyzer evaluating Skills across Structure & Documentation, Examples, and Resources; (2) a security analyzer for vulnerability assessment of Skill implementations.

**Discussion highlights:** Early meta-skills proposal that anticipated the need for Skill quality governance. Discussion explores integration with CI pipelines and potential for automated PR review.

---

### 5. Multiple skill-creator infrastructure fixes (#538, #539, #541, #1298, #1099, #1050, #362, #361)
**Authors:** Lubrsy706, MartinCajiao, joshuawowk, gstreet-ops, Mr-Neutr0n | **Status:** Open | **Updated:** various

**Functionality:** A cluster of PRs addressing systemic issues in the `skill-creator` tooling:
- Case-sensitive file references breaking on Linux (#538)
- Unquoted YAML descriptions with special characters (#539, #361)
- DOCX tracked change ID collisions (#541)
- Windows subprocess and encoding failures (#1099, #1050)
- UTF-8 multi-byte character panics (#362)

**Discussion highlights:** The most active area of community contribution. Windows compatibility and YAML parsing reliability are recurring pain points. Multiple PRs address the same 0% recall bug (#556), indicating this is the ecosystem's most critical stability issue.

---

### 6. Add testing-patterns skill (#723)
**Author:** 4444J99 | **Status:** Open | **Updated:** 2026-04-21
[View PR →](https://github.com/anthropics/skills/pull/723)

**Functionality:** Comprehensive testing skill covering the Testing Trophy model, AAA pattern, unit testing, React component testing (Testing Library), integration/E2E testing, mocking strategies, and performance testing.

**Discussion highlights:** Broad support for a testing-focused skill. Discussion explores scope—whether to maintain one unified skill or split into specialized sub-skills per testing layer.

---

### 7. Add ServiceNow platform skill (#568)
**Author:** Vanka07 | **Status:** Open | **Updated:** 2026-04-23
[View PR →](https://github.com/anthropics/skills/pull/568)

**Functionality:** Broad ServiceNow assistant covering ITSM, ITOM, ITAM/SAM, FSM, HRSD, CSM, SPM, Vulnerability Response, Security Incident Response, CSDM, and IntegrationHub.

**Discussion highlights:** Enterprise demand is clear—this is the most comprehensive enterprise platform skill proposed. Discussion covers maintainability of such a broad skill vs. modular sub-skills.

---

## 2. Community Demand Trends

Analysis of GitHub Issues reveals five clear demand clusters:

### 1. Skill-Creator Stability & Cross-Platform Support (Highest Urgency)
- **Issue #556** (12 comments, 7👍): `run_eval.py`—every query returns 0% trigger rate, making the optimization loop non-functional
- **Issue #1169** (3 comments, 1👍): Same bug confirmed even with literal slash-command queries
- **Issue #1061** (3 comments): Three distinct Windows compatibility failures (PATHEXT, cp1252 encoding, select on pipes)

**Insight:** The skill-creator tooling is the ecosystem's most critical dependency and is currently unreliable on Windows and silently broken in its evaluation pipeline. This blocks all Skill optimization work.

### 2. Enterprise & Platform Integration
- **Issue #228** (14 comments, 7👍): Org-wide skill sharing via shared libraries or direct links (most active issue)
- **Issue #1175** (4 comments): Security and context window concerns for SharePoint Online document handling
- **Issue #492** (7 comments, 2👍): Trust boundary abuse via community skills under `anthropic/` namespace

**Insight:** Enterprise users demand organizational governance—skill sharing infrastructure, security boundaries, and platform integration.

### 3. Skill Ecosystem Hygiene
- **Issue #189** (6 comments, 9👍): Duplicate skills from overlapping plugin installations
- **Issue #202** (8 comments, 1👍): skill-creator reads like developer documentation, not an operational Skill
- **Issue #184** (3 comments, 4👍): agentskills.io reference site broken ("too many redirects")

**Insight:** The community is frustrated by ecosystem fragmentation and documentation quality gaps that undermine Skill usability.

### 4. Feature Requests for New Skill Categories
- **Issue #412** (6 comments): Agent governance—safety patterns, threat detection, trust scoring
- **Issue #1220** (2 comments): Multi-file preload/inline bundling for Skill reference files
- **Issue #29** (4 comments): AWS Bedrock compatibility

### 5. Bug Reports (Reliability)
- **Issue #62** (10 comments): Skills disappearing after file rename
- **Issue #61** (3 comments): 404 errors loading skills on Claude.ai (Team plan)

---

## 3. High-Potential Pending Skills

These active-comment PRs are **not yet merged** but show strong momentum and are likely to land soon:

| PR | Skill | Author | Last Updated | Why It May Land Soon |
|---|---|---|---|---|
| #514 | **document-typography** | PGTBoos | 2026-03-13 | Solves universal pain point; no controversy; complements existing document skills |
| #723 | **testing-patterns** | 4444J99 | 2026-04-21 | High community interest; fills obvious gap in skill coverage |
| #568 | **servicenow** | Vanka07 | 2026-04-23 | Enterprise demand; comprehensive scope; no competing PRs |
| #444 | **AURELION suite** (4 skills) | Chase-Key | 2026-05-06 | Structured cognitive framework; multiple modular skills in one submission |
| #154 | **shodh-memory** | varun29ankuS | 2026-03-03 | Persistent AI agent memory; novel category with clear use cases |
| #335 | **masonry-generate** (images/video) | junaid1460 | 2026-03-14 | Media generation; fills creative tool gap; well-defined scope |
| #181 | **SAP-RPT-1-OSS** (predictor) | amitlals | 2026-03-16 | Enterprise analytics with SAP's open-source model; niche but strong demand |

**Notable:** The **skill-creator infrastructure fixes** (#1298, #1099, #1050, #362, #361, #538, #539, #541) collectively have the highest probability of merging, as they directly unblock the entire Skill development pipeline.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for tooling reliability and cross-platform parity**—specifically, fixing the skill-creator's evaluation pipeline (which reports 0% recall for all queries) and resolving Windows compatibility—before the ecosystem can sustainably absorb the growing pipeline of enterprise and testing-focused Skill submissions.

---

# Claude Code Community Digest
**Date:** 2026-06-17

---

## Today's Highlights

Anthropic shipped **v2.1.179** with critical fixes for mid-stream connection drops and WSL2 scrolling regression, while the community buzzes around a **JetBrains plugin feature request (#47166)** that has been running hot for two months. A wave of infrastructure-focused PRs from contributor **AZERDSQ131** (14+ pull requests in 48 hours) targets security, hook scripting, and CI reliability — signaling a maturing open-source pipeline for Claude Code's plugin ecosystem.

---

## Releases

**v2.1.179** — [View Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.179)
- **Fixed:** Mid-stream connection drops — partial responses are now preserved instead of showing a raw error; the spinner no longer gets stuck at "running tool"
- **Fixed:** Mouse-wheel scrolling in WSL2 under Windows Terminal and VS Code (regression in v2.1.172)
- **Fixed:** A sandbox `denyR` issue (details truncated in changelog)

Notably *absent* from this release: fixes for the file descriptor leak regression (#61299) or the Windows tool results bug (#46767), both of which remain open.

---

## Hot Issues (Top 10 By Significance)

### 1. [#47166 — [FEATURE] JetBrains need some love - a real Claude AI Assist interface plugin](https://github.com/anthropics/claude-code/issues/47166)
- **Votes/Reaction:** 24 comments, 1 👍 (low vote but high engagement)
- **Why it matters:** The top-voted IDE integration request. The JetBrains ecosystem (IntelliJ, PyCharm, WebStorm) remains a glaring gap in Claude Code's IDE coverage. Community comments describe workarounds using `/ide` from the terminal, but demand a native plugin.
- **Heat:** Open since April 13, still no official response.

### 2. [#46140 — CRITICAL: claude.ai MCP OAuth completes but Bearer token never sent](https://github.com/anthropics/claude-code/issues/46140)
- **Votes/Reaction:** 18 comments, 5 👍
- **Why it matters:** A critical authentication bug — the OAuth 2.1 + PKCE flow completes successfully, but the server never receives the Bearer token. This breaks all MCP integrations that rely on OAuth-based auth for Claude Code Web.
- **Heat:** Updated today; marked CRITICAL/URGENT by the reporter.

### 3. [#65514 — [BUG] Usage credits required for 1M context - Pro plan blocked despite 17% usage](https://github.com/anthropics/claude-code/issues/65514)
- **Votes/Reaction:** 16 comments, 2 👍
- **Why it matters:** Users on the Pro plan are being blocked from using the 1M context window despite having 83% of their usage remaining. This suggests either a bug in entitlement checking or unclear policy enforcement. Duplicate reports suggest this affects multiple users.
- **Heat:** Open since June 4; updated yesterday.

### 4. [#54393 — Post-mortem: 12 multi-agent coordination bugs surfaced in one overnight cycle](https://github.com/anthropics/claude-code/issues/54393)
- **Votes/Reaction:** 15 comments, 0 👍
- **Why it matters:** A comprehensive community post-mortem cataloging 12 distinct multi-agent coordination bugs. While framed as a single user's experiment, it's become a reference for agent orchestration issues. The author explicitly filed it as generic, not specific to a single feature request.
- **Heat:** Being referenced in other multi-agent discussions.

### 5. [#46767 — [BUG] Tool results silently dropped with "missing due to internal error" on Windows](https://github.com/anthropics/claude-code/issues/46767)
- **Votes/Reaction:** 11 comments, 5 👍 (highest 👍 count among open bugs)
- **Why it matters:** A regression since v2.1.101 that silently drops all tool results on Windows. This makes Claude Code effectively unusable on Windows for tool-based workflows. The "silent" nature makes it particularly insidious — users may not notice until outputs go missing.
- **Heat:** Updated today; still unresolved after 2+ months.

### 6. [#68484 — [BUG] Desktop extension installs silently fail on macOS Tahoe 26.5](https://github.com/anthropics/claude-code/issues/68484)
- **Votes/Reaction:** 9 comments, 0 👍
- **Why it matters:** macOS Tahoe 26.5 compatibility issue — extensions fail to install with zero error feedback. This is a user-experience regression for early adopters of the latest macOS.
- **Heat:** Opened June 14; updated today.

### 7. [#61299 — [BUG] File descriptor leak regression in large monorepos (2.1.143+)](https://github.com/anthropics/claude-code/issues/61299)
- **Votes/Reaction:** 7 comments, 1 👍
- **Why it matters:** Affects teams using Claude Code in large monorepos — the tool gradually exhausts file descriptors, causing crashes after extended sessions. Has a reproducible test case attached.
- **Heat:** Open since May 21; updated today with additional confirmation from other users.

### 8. [#64235 — [BUG] Intermittent "tool call was malformed" regression since 2026-05-29](https://github.com/anthropics/claude-code/issues/64235)
- **Votes/Reaction:** 5 comments, 2 👍
- **Why it matters:** A model-level regression where Claude sometimes says it's making a tool call (`stop_reason=tool_use`) but sends no actual tool_use block. This causes silent failures where the agent "thinks" but does nothing.
- **Heat:** Updated today; multiple users confirming the intermittent nature.

### 9. [#68287 — [BUG] Max plan: Opus 4.8 only shows 256k context, 1M option missing](https://github.com/anthropics/claude-code/issues/68287)
- **Votes/Reaction:** 5 comments, 1 👍
- **Why it matters:** Affects Max plan subscribers who expect access to Opus 4.8's full 1M context window. The model picker truncates to 256k. Screenshots provided.
- **Heat:** Open since June 13; updated today.

### 10. [#68961 — [BUG] Excessive agentic loop iterations consuming API usage quota](https://github.com/anthropics/claude-code/issues/68961)
- **Votes/Reaction:** 2 comments, 0 👍
- **Why it matters:** A fresh report (opened today) of the agent getting stuck in "dozens/hundreds" of unnecessary agentic loop iterations, burning through API quota. The reporter's frustration is palpable: "it's so unnecessary. It needs to be smarter about this." Could indicate a systemic issue with agent termination logic.
- **Heat:** Newly opened; watch for escalation.

---

## Key PR Progress (Top 10)

### 1. [#46351 — Enable PowerShell tool on macOS and Linux](https://github.com/anthropics/claude-code/pull/46351)
- **Status:** CLOSED (merged)
- **Why it matters:** Unlocks PowerShell tool support on macOS and Linux when `pwsh` is available, removing the hard-coded Windows-only gate. This has been a long-standing friction point for cross-platform developers.
- **Trigger:** `CLAUDE_CODE_USE_POWERSHELL_TOOL=1`

### 2. [#68707 — Add /bug command to file GitHub issues from terminal](https://github.com/anthropics/claude-code/pull/68707)
- **Status:** OPEN
- **Why it matters:** A quality-of-life feature for power users — allows filing bug reports directly from the Claude Code terminal without leaving the session. Streamlines the feedback loop.
- **Author:** AZERDSQ131

### 3. [#68689 — Block symlink escape in extensibility config reads](https://github.com/anthropics/claude-code/pull/68689)
- **Status:** OPEN
- **Why it matters:** Security hardening — prevents a class of symlink-based path traversal attacks in plugin configuration loading.
- **Author:** AZERDSQ131

### 4. [#68786 — Avoid shell injection in test-hook.sh](https://github.com/anthropics/claude-code/pull/68786)
- **Status:** OPEN
- **Why it matters:** Fixes a shell injection vulnerability in the hook development test script where `$TEST_INPUT` was embedded unsafely inside a `bash -c` string.
- **Author:** AZERDSQ131

### 5. [#68785 — Fix hook JSON to stdout, tighten glob, fix CI detection in examples](https://github.com/anthropics/claude-code/pull/68785)
- **Status:** OPEN
- **Why it matters:** Fixes three example hook scripts that were incorrect reference implementations — including one writing JSON responses to stderr (breaking the hook protocol).
- **Author:** AZERDSQ131

### 6. [#68673 — Break pagination when page is not full](https://github.com/anthropics/claude-code/pull/68673)
- **Status:** OPEN
- **Why it matters:** Optimizes CI scripts to stop paginating early when the current page isn't full, reducing API calls.
- **Author:** AZERDSQ131

### 7. [#68680 — Safe JSON construction in log-issue-events workflow](https://github.com/anthropics/claude-code/pull/68680)
- **Status:** OPEN
- **Why it matters:** Prevents malformed JSON in CI workflow outputs, which could break downstream automation.
- **Author:** AZERDSQ131

### 8. [#68694 — Normalize CLAUDE_PLUGIN_ROOT path separators on Windows](https://github.com/anthropics/claude-code/pull/68694)
- **Status:** OPEN
- **Why it matters:** Fixes plugin path handling on Windows where backslash/forward-slash inconsistencies could break plugin discovery.
- **Author:** AZERDSQ131

### 9. [#68690 — Correct state file path in help.md](https://github.com/anthropics/claude-code/pull/68690)
- **Status:** OPEN
- **Why it matters:** Fixes documentation for the ralph-wiggum tool where an incorrect file path was documented.
- **Author:** AZERDSQ131

### 10. [#68702 — Guard PROMPT_PARTS expansion against set -u on bash 3.x (macOS)](https://github.com/anthropics/claude-code/pull/68702)
- **Status:** OPEN
- **Why it matters:** macOS ships bash 3.2 by default; this fix prevents the ralph-wiggum tool from crashing on older bash versions when `set -u` is active.
- **Author:** AZERDSQ131

---

## Feature Request Trends

The current issue corpus reveals **five dominant feature request themes**:

1. **IDE Integration Expansion** — The JetBrains request (#47166) is the most visible, but there's growing demand for desktop app ↔ IDE bridging (#61306) and universal `/ide` support. The community wants Claude Code to be a first-class citizen in *all* major IDEs, not just VS Code.

2. **Multi-Agent & Orchestration** — Issue #54393 (the 12-bug post-mortem) and the "excessive agentic loops" bug (#68961) point to a community actively pushing Claude Code beyond single-session usage. Demand is rising for proper multi-agent coordination, deterministic session control (#58933), and worktree-aware session management (#62309).

3. **Context Window Management** — Multiple threads (#68921, #58933) request smarter context handling: tool response diffing/delta to reduce token consumption, deterministic behavior for automation users, and clearer cost/usage metrics (#68964).

4. **Plugin & Extensibility Improvements** — The flood of PRs from AZERDSQ131 reflects community investment in the plugin system. Specific requests include: custom header support for API providers (#68960), better MCP stdio server documentation (#47635), and in-session `/remote-control` toggling (#60699).

5. **Windows & macOS Platform Parity** — Persistent Windows issues (#46767, #65514, #68287) and the macOS Tahoe regression (#68484) show the community is multi-platform but feels Claude Code's Windows/macOS support lags behind Linux.

---

## Developer Pain Points

The **top recurring frustrations** evident from this week's data:

1. **Silent Failures** — Multiple bugs (#46767, #68484, #64235) involve errors that produce no user-visible feedback. Tool results silently dropped, extension installs with no error, malformed tool calls with no explanation — these erode trust in the tool.

2. **Windows as Second-Class Platform** — Windows-specific bugs dominate the critical list: silent tool result drops, missing 1M context option, GPU process crash loops (#68956), and worktree mounting issues (#68954). The community sentiment is that Windows fixes lag significantly.

3. **Regression Velocity** — Several bugs are explicitly marked as regressions (v2.1.101, v2.1.143+, v2.1.172), suggesting the rapid release cadence is introducing new issues faster than old ones are resolved. The file descriptor leak (#61299) and Windows tool results bug (#46767) have been open for weeks.

4. **Opaque Cost/Usage Model** — Issues #68961 and #68964 highlight that developers are frustrated by: (a) agents burning through quota in loops they can't control, and (b) unclear separation between model-specific and pooled usage buckets.

5. **Worktree & Multi-Session Footguns** — Multiple issues (#62309, #62431, #65216) detail painful interactions with the worktree system — accidental session destruction, branch naming surprises, and crash loops when reconnecting to background agents. Teams running parallel sessions are hitting these hard.

6. **MCP OAuth Dead-End** — Issue #46140 remains critical: the OAuth flow completes but authorization is never passed to the server. For teams building MCP integrations, this is a complete blocker.

---

*Digest generated from `github.com/anthropics/claude-code` activity in the 24 hours prior to 2026-06-17 23:59 UTC.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-17

## Today's Highlights

Two Rust alpha releases (v0.141.0-alpha.3 and v0.141.0-alpha.4) landed within hours, while the community remains vocal about session management issues—particularly the silent disappearance of project conversations in Codex Desktop and instability in thread hydration. On the development side, a large batch of PRs from the core team focuses on plugin and skill loading performance, namespace cleanup, and the groundwork for a credential broker.

## Releases

**rust-v0.141.0-alpha.3** and **rust-v0.141.0-alpha.4** — two rapid sequential alpha bumps. No changelog details are provided in the release notes, but the version jump signals active iteration on the Rust SDK/crate packaging ahead of a stable 0.141.0 release.

| Release | Tag |
|---|---|
| rust-v0.141.0-alpha.3 | 0.141.0-alpha.3 |
| rust-v0.141.0-alpha.4 | 0.141.0-alpha.4 |

## Hot Issues

1. **#21128 — Desktop silently hides project conversations outside global recent-50 window**  
   *27 comments, 17 👍*  
   The top-voted open bug. Users report that long-lived project conversations become invisible once they fall outside a hard-coded 50-item recency window, making Codex Desktop unreliable as persistent project memory. Community reaction is strong—this undermines trust in the app for real workflows.  
   [View Issue](https://github.com/openai/codex/issues/21128)

2. **#28095 — Archived chats show a non-functional Delete button**  
   *10 comments, 4 👍*  
   A UI/UX mismatch: the archive view displays a Delete button but the action silently fails. Users expect data management to work as advertised.  
   [View Issue](https://github.com/openai/codex/issues/28095)

3. **#27506 — Windows app crashes on launch with non-ASCII user profile paths (Korean characters)**  
   *9 comments, 6 👍*  
   A regionalization bug: the `windows-updater.node` crashes on `Illegal byte sequence` when the Windows profile contains Korean characters. Blocks non-English users from even launching the app after an auto-update.  
   [View Issue](https://github.com/openai/codex/issues/27506)

4. **#25321 — macOS composer caret/focus intermittently disappears**  
   *9 comments, 4 👍*  
   Intermittent focus loss in the input field—a high-friction UX bug that forces users to alt-tab away and back to regain input focus.  
   [View Issue](https://github.com/openai/codex/issues/25321)

5. **#27287 — Computer Use bootstrap fails on Windows: `@oai/sky` internal subpath not exported**  
   *8 comments, 9 👍*  
   A packaging issue prevents Computer Use from initializing on Windows. Community engagement is high, suggesting this feature is heavily anticipated on that platform.  
   [View Issue](https://github.com/openai/codex/issues/27287)

6. **#12464 — Feature request: `/cwd` command to switch working directory without session restart**  
   *7 comments, 21 👍*  
   The highest-voted feature request this period. CLI users want to change the working directory mid-session without killing the current context—a workflow-critical improvement for long-running TUI sessions.  
   [View Issue](https://github.com/openai/codex/issues/12464)

7. **#27570 — `review-summary` spawns thousands of `git hash-object` processes with nested repos**  
   *4 comments, 1 👍*  
   A performance pathology: the code-review feature forks excessive git subprocesses when nested repositories are present, potentially freezing the desktop app.  
   [View Issue](https://github.com/openai/codex/issues/27570)

8. **#14372 — Permissions error with git fsmonitor in sandbox**  
   *7 comments, 5 👍*  
   Sandboxed sessions fail when `git fsmonitor` is active, breaking git operations inside isolated environments. A blocker for developers using modern git workflows inside Codex.  
   [View Issue](https://github.com/openai/codex/issues/14372)

9. **#26341 — Codex triggers macOS `syspolicyd` file descriptor leak, corrupts DMG files**  
   *3 comments, 0 👍*  
   A sophisticated system-level bug: Codex leaks file descriptors into `syspolicyd`, causing *all* downloaded DMG files on the system to be reported as "damaged." Affects the broader macOS ecosystem beyond Codex itself.  
   [View Issue](https://github.com/openai/codex/issues/26341)

10. **#28606 — Windows: Codex lost all chat history, won't save settings (26.611.61049)**  
    *3 comments, 0 👍*  
    A data-loss critical bug in the latest release. The app silently resets session state, erasing project history and preferences.  
    [View Issue](https://github.com/openai/codex/issues/28606)

## Key PR Progress

1. **#28638 — core: remove redundant TurnContext and Prompt fields**  
   A cleanup PR removing stale, duplicated fields from `TurnContext` to prevent split-brain state between configs and model metadata. Core architecture hardening.  
   [View PR](https://github.com/openai/codex/pull/28638)

2. **#28599 — code-mode: move cell state into library actor**  
   Extracts the per-cell execution lifecycle into a dedicated actor. Primarily an ownership/encapsulation change, but lays groundwork for better isolation of code-mode cell execution.  
   [View PR](https://github.com/openai/codex/pull/28599)

3. **#28034 — Add experimental local credential broker**  
   A security-focused PR that moves injectable child-process credentials behind a managed network proxy to prevent exfiltration by commands. Early-stage, but addresses a genuine attack surface.  
   [View PR](https://github.com/openai/codex/pull/28034)

4. **#28580 — Support object-valued plugin MCP manifests**  
   Fixes plugin parsing to accept `mcpServers` declared as an inline object (not just string paths). Resolves a compatibility gap with community MCP plugins.  
   [View PR](https://github.com/openai/codex/pull/28580)

5. **#28632 — Tell codex to avoid changing rollout format**  
   Adds a skill requirement to nudge the model away from modifying internal rollout format types during path migrations. A correctness guardrail.  
   [View PR](https://github.com/openai/codex/pull/28632)

6. **#28629 — core: restore absolute turn context cwd**  
   Reverts a premature change that moved rollout format to store URIs, restoring backward compatibility. A pragmatic rollback to avoid breaking existing features.  
   [View PR](https://github.com/openai/codex/pull/28629)

7. **#28624 — Load plugins and skill roots concurrently**  
   Performance optimization: cold startup now loads up to 8 configured plugins concurrently instead of serially, reducing initial launch latency.  
   [View PR](https://github.com/openai/codex/pull/28624)

8. **#28623 — Reuse parsed plugin skill root snapshots**  
   Eliminates duplicate filesystem scans during plugin and skill loading. Shares raw root snapshots across the two passes to cut cold-start parsing work in half.  
   [View PR](https://github.com/openai/codex/pull/28623)

9. **#27713 — Prototype workload identity federation for CLI auth**  
   A do-not-merge prototype adding workload identity federation for CI/CD pipeline authentication. Signals future investment in non-interactive auth flows.  
   [View PR](https://github.com/openai/codex/pull/27713)

10. **#27946 — Use input items for Responses Lite tools**  
    Moves tool definitions into `additional_tools` and developer items for the Responses Lite API, keeping the internal representation 1-to-1 with the new API shape.  
    [View PR](https://github.com/openai/codex/pull/27946)

## Feature Request Trends

The most-requested feature direction remains **session lifecycle control**:

- **`/cwd` command** (#12464, 21 👍) — TUI users want to switch working directories without restarting sessions.
- **PreToolUse hooks with native approval prompts** (#28437) — Hooks should be able to escalate tool calls to explicit human approval.
- **Open Codex Chat in a new VS Code window** (#16615, 12 👍) — IDE extension users want floating, independent chat panels.
- **Plugin catalog polish** (TUI Plugin Sharing PRs #26703–#26705) — Users want a browsable, searchable remote plugin directory, not just a raw marketplace list.

The common thread: users want more control over their session environment, better persistence guarantees, and richer plugin management without leaving the TUI.

## Developer Pain Points

Recurring themes from this digest's issues:

- **Session data loss and invisibility** — #21128 (conversations hidden), #28606 (full history loss), #26012 (command details lost after restore). Multiple distinct bugs all pointing to fragile session state management.
- **Windows-specific launch failures** — #27506 (non-ASCII paths), #27809 (VCPkgSrv.exe crashes), #27287 (Computer Use bootstrap). Windows continues to be the platform with the highest density of critical launch blockers.
- **Rollout/history JSONL bloat** — #22991, #25215, #26161, #28524. Many issues trace back to single-file JSONL rollouts growing to hundreds of MB, causing freezes during hydration, pinning, and restore.
- **Performance under load** — #13809 (long git diffs lag), #27570 (thousands of git processes), #26341 (descriptor leak affecting whole OS). These aren't edge cases; they manifest in normal long-running sessions.
- **Archive/restore inconsistency** — #28095 (delete button broken), #26201 (stale active session after archive), #26012 (path inconsistency). The archive workflow is buggy across both Windows and macOS.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-06-17

## Today's Highlights
No new releases landed in the last 24 hours, but the community continued to surface two critical themes: **agent reliability** (hangs, false success reports, subagent coordination failures) and **security hardening** of memory systems, MCP token handling, and CI/CD pipelines. A cluster of 10+ open PRs targeting memory bugs, OAuth atomic writes, and artifact poisoning in CI signal the maintainers are prioritizing defense-in-depth ahead of a likely minor release.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues (10 selected)

**1. Generalist agent hangs indefinitely** ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409))  
`[P1]` – Agent hangs forever on simple tasks (e.g., folder creation). Workaround: disable sub‑agent delegation. 8 👍 indicate this is the most upvoted active bug. **Why it matters:** blocks core workflow for any user relying on the generalist agent.

**2. Subagent MAX_TURNS falsely reported as GOAL success** ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323))  
`[P1]` – `codebase_investigator` returns `status: "success"` with `Termination Reason: "GOAL"` even when it hit the max-turn limit without doing any analysis. **Why it matters:** masks real agent failures from users and auto-evals.

**3. Shell command gets stuck in "Waiting input"** ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166))  
`[P1]` – After a simple CLI command finishes, Gemini hangs showing "Awaiting user input." 3 👍. **Why it matters:** breaks interactive shell workflows on macOS/Linux.

**4. PTY leak exhausts macOS PTYs** ([#27628](https://github.com/google-gemini/gemini-cli/issues/27628)) – *CLOSED*  
`[P2]` – `enableInteractiveShell=true` leaks PTY file descriptors, causing system-wide PTY exhaustion. 1 👍. **Why it matters:** can crash the entire OS session for heavy users.

**5. Auto Memory indefinite retry on low-signal sessions** ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522))  
`[P2]` – If the extraction agent decides a session is "low-signal" and doesn't read it, that session remains unprocessed and keeps being re-surfaced. **Why it matters:** causes memory extraction loops that waste API tokens and degrade memory quality.

**6. Non-deterministic secret redaction in Auto Memory** ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525))  
`[P2]` – Secrets are redacted *after* they've already been sent to model context. Also logs existing skill transcripts (`.transcript` files) containing secrets. **Community reaction:** no upvotes yet, but this is a compliance and trust risk.

**7. >128 tools causes 400 error** ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246))  
`[P2]` – When >128 tools are registered, the API call fails with a 400. The agent should scope tools to avoid this. **Why it matters:** impacts users with many MCP servers enabled.

**8. Agent doesn't use custom skills/sub-agents autonomously** ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968))  
`[P2]` – Users report Gemini almost never invokes custom skills (gradle, git) or sub-agents without explicit prompting. **Why it matters:** undermines the value proposition of agent extensibility.

**9. Browser agent ignores settings.json overrides** ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267))  
`[P2]` – The BrowserAgent reads `settings.json` during init but then ignores overrides like `maxTurns`. **Why it matters:** no workaround; users cannot control browser agent behavior.

**10. Destructive command execution not discouraged** ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672))  
`[P2]` – Agent uses `git reset --force`, `rm -rf`, etc., even when safer alternatives exist. 1 👍. **Why it matters:** risk of data loss; the agent lacks a "safe mode" for destructive operations.

---

## Key PR Progress (10 selected)

**1. Fix parallel workspace build race condition** ([#27643](https://github.com/google-gemini/gemini-cli/pull/27643)) – *CLOSED*  
Split build into sequential topological stages (Core → Libraries → Apps). Fixes flaky CI builds.

**2. Validate workflow_run origin (fork artifact poisoning)** ([#27753](https://github.com/google-gemini/gemini-cli/pull/27753))  
`[P1]` – Prevents fork PRs from poisoning E2E artifacts and running attacker code with repo secrets. Critical supply-chain security fix.

**3. Fix MCP header encoding for non-ASCII values** ([#27771](https://github.com/google-gemini/gemini-cli/pull/27771))  
`[P2]` – Encodes Unicode header values (e.g., `mąka`) before passing to Fetch as ByteString. Fixes MCP discovery failures with internationalized configs.

**4. Document read_file 20MB limit** ([#27763](https://github.com/google-gemini/gemini-cli/pull/27763))  
`[P1]` – Adds docs for the existing `read_file` size enforcement. Removes user confusion when hitting "File size exceeds the 20MB limit."

**5. Strip thoughts from scrubbed history (thought leakage)** ([#27971](https://github.com/google-gemini/gemini-cli/pull/27971))  
Fixes a bug where the model's internal monologue leaks into plain‑text history, causing infinite‑loop monologues in subsequent turns.

**6. Case-insensitive sensitive path blocklist + VS Code HITL** ([#27966](https://github.com/google-gemini/gemini-cli/pull/27966))  
`[P2]` – Enforces case‑insensitive blocking for `.git`, `.env`, `node_modules` and adds human‑in‑the‑loop for VS Code tool calls. Addresses the `/../Security Bypass` scenario.

**7. Write MCP OAuth tokens atomically** ([#27664](https://github.com/google-gemini/gemini-cli/pull/27664))  
`[P1]` – Uses temp file + atomic rename to prevent partial/corrupt token writes. Fixes #27663.

**8. Refresh MCP OAuth with stored client ID** ([#27889](https://github.com/google-gemini/gemini-cli/pull/27889))  
`[P1]` – After `/mcp auth`, auto‑discovered servers had missing `oauth.clientId` in config; now uses persisted token metadata. Fixes auth refresh failures.

**9. Scope flash model names per auth backend** ([#27760](https://github.com/google-gemini/gemini-cli/pull/27760))  
`[P1]` – Differentiates `gemini-3.5-flash` (Vertex AI) from `gemini-3-flash` (AI Studio). Fixes #27759.

**10. Scope MCP resource resolution to prevent cross-server URI confusion** ([#27964](https://github.com/google-gemini/gemini-cli/pull/27964))  
Fails closed when >1 server exposes the same URI, preventing one MCP server from silently shadowing another's resource.

---

## Feature Request Trends

- **AST‑aware tooling**: Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746), [#22747](https://github.com/google-gemini/gemini-cli/issues/22747)) request AST‑aware file reads, searches, and codebase mapping to reduce token waste and improve precision.
- **Agent self‑awareness**: Users want the agent to know its own CLI flags, hotkeys, and configuration ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)) so it can act as an expert guide.
- **Browser agent resilience**: Requests for automatic session takeover, lock recovery, and `settings.json` compliance ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)).
- **Eval infrastructure stabilization**: A push toward always‑passing steering evals, component‑level evaluation frameworks, and reliable internal quality tracking ([#23313](https://github.com/google-gemini/gemini-cli/issues/23313), [#23166](https://github.com/google-gemini/gemini-cli/issues/23166), [#24353](https://github.com/google-gemini/gemini-cli/issues/24353)).

---

## Developer Pain Points

- **Agent hangs and false success reporting**: The top two P1 bugs—generalist agent hangs and subagent false MAX_TURNS success—erode user trust. Both have been open for 3+ months.
- **Shell execution ghost state**: Commands that finish but leave the shell in "Waiting input" mode break terminal‑based workflows. Repeatedly reported.
- **MCP OAuth friction**: Non‑atomic token writes, missing client IDs on auto‑discovery, and Unicode encoding failures create a fragile auth experience for MCP users.
- **Memory system side effects**: Auto Memory's indefinite retries, non‑deterministic redaction, and silent patch invalidation create unpredictable token usage and potential secret exposure.
- **Destructive command risk**: The agent's willingness to use `--force`, `git reset`, and other dangerous commands with no built‑in safeguards is a recurring theme of user concern.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest**
**Date:** 2026-06-17

## 1. Today's Highlights
Version 1.0.64-0 dropped today, bringing the `/diagnose` command for session log analysis and making `/security-review` available to all users. The community is heavily focused on sub-agent model mismatches and MCP reliability, with several high-severity bugs reported around the new plugin ecosystem and tool loading.

## 2. Releases
**v1.0.64-0** was published. Key additions:
- `/diagnose` command for analyzing session logs
- `/mcp` registry installation for browsing and installing MCP servers
- `/security-review` is no longer experimental (available to all users)
- Automatic discovery of MCP servers from installed plugins
- CSV output support for MCP tools

## 3. Hot Issues
- **#3687 – [OPEN] copilot.exe fatal-aborts under load on Windows ARM64**  
  A critical crash (BEX64 / 0xc0000409) occurring under memory pressure or during multi-session startup. High impact for Windows ARM64 users; 5 comments, 1 thumbs-up.  
  [Link](https://github.com/github/copilot-cli/issues/3687)

- **#1168 – [OPEN] Excessive authorization prompts during single request ("authorization fatigue")**  
  A single high-level prompt can trigger “more than a dozen” consecutive authorization dialogs. Severe UX degradation for power users; 2 comments, 2 thumbs-up.  
  [Link](https://github.com/github/copilot-cli/issues/1168)

- **#3828 – [OPEN] ContentExclusionFilter.isExcluded crash**  
  The `rg` tool crashes with `TypeError: Cannot read properties of undefined` when the content exclusion filter accesses an unexpected structure. Regressed in recent builds.  
  [Link](https://github.com/github/copilot-cli/issues/3828)

- **#3821 – [OPEN] /update from a resumed session leaves conflicting flags**  
  Running `/update` inside a resumed session causes a restart with both `--session-id` and `-r` flags, breaking the resume workflow.  
  [Link](https://github.com/github/copilot-cli/issues/3821)

- **#3730 – [OPEN] No support for Enterprise-Managed Custom Models in CLI**  
  Enterprise admins can set custom models in Copilot Admin, but they don’t appear in the CLI. 4 thumbs-up reflect strong demand.  
  [Link](https://github.com/github/copilot-cli/issues/3730)

- **#2790 – [OPEN] Figma Desktop MCP incorrectly classified as SSE**  
  HTTP-based MCP server is shown as SSE type, causing a non-200 error. Works fine in Codex CLI.  
  [Link](https://github.com/github/copilot-cli/issues/2790)

- **#3812 – [OPEN] Sub-agents can no longer access MCP tools**  
  Custom sub-agents lose visibility of MCP tools due to deferred loading. Top-level agent still works.  
  [Link](https://github.com/github/copilot-cli/issues/3812)

- **#3826 – [OPEN] "Operation cancelled by user" re-injected as user message**  
  Cancelling a turn via Esc/Ctrl-C sends the cancellation text back to the model as a new instruction, causing confusing "replies."  
  [Link](https://github.com/github/copilot-cli/issues/3826)

- **#3824 – [OPEN] Sub-agents can run a different model than the configured session model**  
  Sub-agents default to a different model without any UI indication. Two distinct mechanisms cause this: agent-type defaults and experiment overrides.  
  [Link](https://github.com/github/copilot-cli/issues/3824)

- **#3823 – [OPEN] Reasoning effort "xhigh" silently downgraded to "medium"**  
  When a model doesn’t advertise `xhigh`, the CLI falls back to the model default instead of clamping to `max`, surprising users expecting maximum reasoning.  
  [Link](https://github.com/github/copilot-cli/issues/3823)

## 4. Key PR Progress
No pull requests were updated in the last 24 hours. (0 items)

## 5. Feature Request Trends
The community is requesting three clear improvements:
- **Enterprise model support** (#3730) – Custom models configured in Copilot Admin should be selectable in the CLI.
- **Bulk plugin management** (#3830, #3829) – A single command to update all plugins, and making read-only slash commands like `/mcp show` asynchronous for smoother UX.
- **Multi-repo skills** (#3822) – Allowing `skillDirectories` to work at the repository level for monorepo setups.

## 6. Developer Pain Points
- **Sub-agent model misalignment** (#3824, #3823): Sub-agents silently using different models or reasoning efforts than configured. High frustration for users expecting predictable behavior.
- **Permission/authorization friction** (#1168, #3825): Excessive prompts and `--allow-all` leaking read permissions that wedge the TUI on startup.
- **MCP tool isolation** (#3812, #2790): Sub-agents losing access to MCP tools and incorrect protocol detection for HTTP-based servers.
- **Session management gaps** (#3821, #3518, #3826): Update crashes in resumed sessions, no way to unarchive projects, and cancellation messages being treated as user input.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-17

**Data Source:** [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## Today's Highlights

Two critical bugs surfaced in the last 24 hours: a fresh install via Homebrew yields an unhelpful "LLM not set" error with no prompt to run `kimi login`, and the CLI can auto-discover a deleted MCP server, leading to unfixable 400 errors. Meanwhile, improvements continue for thinking models with a popular merged feature to hide the thinking process, and a long-standing enhancement request to raise the default max steps per turn gains renewed traction.

---

## Releases

No new releases in the last 24 hours. The latest stable version remains **v1.47**.

---

## Hot Issues (10 Noteworthy)

### 1. [#2456 – Fresh install reports "LLM not set" with no guidance to run login](https://github.com/MoonshotAI/kimi-cli/issues/2456)
- **Status:** OPEN | **Updated:** 2026-06-16 | **Comments:** 0 | **👍:** 0
- **Why it matters:** A first-run experience blocker that immediately halts new users. The message "LLM not set" is ambiguous — no hint to run `kimi login`. This is a high-impact UX regression for any Homebrew install path.

### 2. [#2457 – CLI auto-discovers MCP server after user deleted it, causing unfixable 400 errors](https://github.com/MoonshotAI/kimi-cli/issues/2457)
- **Status:** OPEN | **Updated:** 2026-06-16 | **Comments:** 0 | **👍:** 0
- **Why it matters:** A persistent state bug where the CLI re-discovers a manually deleted MCP server, resulting in repeated 400 errors with no workaround. Could degrade trust in the MCP integration.

### 3. [#1327 – [enhancement] More steps per turn by default](https://github.com/MoonshotAI/kimi-cli/issues/1327)
- **Status:** OPEN | **Updated:** 2026-06-16 | **Comments:** 3 | **👍:** 0
- **Why it matters:** Users hit the 100-step ceiling while context is only 34.5% used. The reporter argues the default is too low and wastes ongoing sessions. A long-standing UX complaint that resurfaces with no official response.

### 4. [#1632 – [CLOSED] Option to hide thinking content while using thinking models](https://github.com/MoonshotAI/kimi-cli/issues/1632)
- **Status:** CLOSED | **Updated:** 2026-06-16 | **Comments:** 2 | **👍:** 3
- **Why it matters:** Now likely merged/implemented. Users want to use K2 thinking models for better reasoning but without the constant "Thinking…" spinner and grey italic output cluttering the terminal. Popular request with broad appeal.

### 5. *(Remaining issues filtered by relevance)*  
Only 4 open issues were updated in the last 24h. No additional issues meet the 10-item threshold for this digest.

---

## Key PR Progress (10 Important PRs)

### 1. [#1771 – fix: always stringify tool message content in Chat Completions provider](https://github.com/MoonshotAI/kimi-cli/pull/1771)
- **Status:** OPEN | **Updated:** 2026-06-16 | **Comments:** 0 | **👍:** 0
- **Summary:** Fixes #1762 (400 error) by ensuring `content` is always a **string** for `role: "tool"` messages. Previously, multi-part tool results (e.g., system reminder + actual output) caused array-format, breaking the API contract. This directly unblocks users getting `400: Failed...` during tool calls.

*(Only 1 PR was updated in the last 24h. The remaining slots are below the threshold.)*

---

## Feature Request Trends

- **Higher default max steps per turn:** Users consistently hit the 100-step ceiling well before exhausting context. The community clearly expects a higher default — possibly 500 or unlimited — to avoid mid-session interruptions.
- **Thinking model output toggles:** The desire to suppress "Thinking…" spinner and grey text while still using advanced reasoning models is a recurring theme. This suggests a preference for a cleaner terminal UX that prioritizes final output.
- **Auto-discovery opt-out:** The MCP server auto-discovery bug (#2457) hints at a broader desire for explicit control over what the CLI scans and re-attaches, especially after manual deletion.

---

## Developer Pain Points

- **Poor first-run experience:** The "LLM not set" blocker (#2456) with zero guidance is a significant onboarding friction. Developers expect either an auto-login hint or a more descriptive error message.
- **Persistent server state bugs:** Users who delete MCP servers expect clean removal; the CLI re-discovering them and causing 400 errors (#2457) violates the principle of least surprise and has no documented workaround.
- **Tool call serialization fragility:** The multi-part tool content array issue (#1771) reveals an edge case in the Chat Completions provider that can silently corrupt tool interactions. Developers need more robust type enforcement at the serialization layer.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest
**Date:** 2026-06-17

---

## Today's Highlights

The OpenCode community saw a flurry of activity around model compatibility and session lifecycle issues, with **3 separate reports** of MiniMax M3 rejecting sessions containing tool-call history. A major PR chain from an automated cleanup batch (PRs #27934–#27940) has landed, bringing service worker caching, zstd compression, concurrency limits, and a configurable fallback model chain. The perennially hot issue of random TUI hangs (Issue #2940) reached **39 comments** without resolution, remaining the community's most persistent frustration.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#27167 – Add native session goals with /goal](https://github.com/anomalyco/opencode/issues/27167)**  
   *Author: jorgitin02* | **87 👍, 50 comments**  
   This highly popular feature request proposes a persistent `/goal` slash command to define session-level objectives that survive context resets. The community strongly resonated with the idea of explicit session lifecycle management over ad-hoc prompting. The high engagement suggests this may land on the roadmap soon.

2. **[#2940 – OpenCode just hangs randomly](https://github.com/anomalyco/opencode/issues/2940)**  
   *Author: rrapstine* | **18 👍, 39 comments**  
   A long-running (since Oct 2025) critical bug where OpenCode becomes unresponsive, especially on Laravel projects with Boost. `/compact` helps inconsistently, and Ctrl+C is often the only escape. Still unresolved—this is the community's #1 stability concern.

3. **[#7048 – "Copied to clipboard" never works](https://github.com/anomalyco/opencode/issues/7048)**  
   *Author: ambedded* | **13 👍, 23 comments**  
   Ubuntu + GhostTTY users report that right-click copy always shows "Copied to clipboard" but never populates the clipboard buffer. A surprisingly high-impact UX issue affecting daily workflows.

4. **[#25832 – OpenCode cannot read images anymore](https://github.com/anomalyco/opencode/issues/25832)**  
   *Author: arduinosvv* | **4 👍, 13 comments**  
   Image vision capabilities broke between April 29 and May 5, 2026. Users who relied on OpenCode to interpret UI mockups from PNG/JPEG are blocked. This regression in the vision pipeline needs urgent investigation.

5. **[#21470 – OpenCode is heavily CPU-bound](https://github.com/anomalyco/opencode/issues/21470)**  
   *Author: tom-neara* | **10 👍, 11 comments**  
   With Gemini-3.1, OpenCode itself consumes more CPU than the model API calls. A 300k-token session spent $8.30 on the model but 50× that in local processing. Points to inefficiencies in the agent loop or token accounting.

6. **[#18001 – Implement /loop for iterative task execution](https://github.com/anomalyco/opencode/issues/18001)**  
   *Author: doko89* | **27 👍, 9 comments**  
   Strong demand for a built-in loop/repeat command to avoid verbose natural-language prompts for repetitive tasks. Would complement the `/goal` proposal well.

7. **[#28957 – "Upstream idle timeout exceeded"](https://github.com/anomalyco/opencode/issues/28957)**  
   *Author: VENAXIS* | **0 👍, 15 comments**  
   macOS Tahoe + Apple M4 users hitting infrastructure timeouts specifically when using the "writing-plans" skill. The error message ("The upstream connection between the client and the model service idled out") suggests a session-layer timeout bug.

8. **[#8345 – zsh: illegal hardware instruction opencode](https://github.com/anomalyco/opencode/issues/8345)**  
   *Author: yujianfeikong* | **6 👍, 15 comments**  
   Darwin x64 users getting SIGILL on launch after installing the dmg. Likely a CPU feature detection issue or binary targeting an unsupported instruction set.

9. **[#31849 – DeepSeek edit tool fails frequently](https://github.com/anomalyco/opencode/issues/31849)**  
   *Author: laisea* | **1 👍, 4 comments**  
   On OpenCode 1.17.0 with DeepSeek models, the code editing tool often fails to invoke correctly. Model-specific tool-call compatibility is becoming a recurring theme across multiple providers.

10. **[#30697 – OpenCode navigates to deleted project path](https://github.com/anomalyco/opencode/issues/30697)**  
    *Author: mrxiaoxingx* | **0 👍, 4 comments**  
    Windows users report that after moving a project folder, OpenCode Desktop still resolves to the old (now-deleted) path. Session persistence logic doesn't validate directory existence.

---

## Key PR Progress

1. **[#32609 – fix(provider): stub orphan MiniMax tool results](https://github.com/anomalyco/opencode/pull/32609)**  
   *Author: megamen32* | **Open**  
   Direct fix for #32608: MiniMax M3 rejects sessions with prior tool-call history. This PR stubs orphan tool results to maintain compatibility. Closely related to #32611 and #32614.

2. **[#32604 – fix(session): preserve reasoning part type on model switch](https://github.com/anomalyco/opencode/pull/32604)**  
   *Author: malventano* | **Open**  
   Switching models triggers massive prefix cache invalidation. This fix preserves the reasoning part type to avoid full re-processing. Directly addresses performance regression when swapping providers mid-session.

3. **[#32612 – fix(codex): exclude `-pro` models from ChatGPT-account model list](https://github.com/anomalyco/opencode/pull/32612)**  
   *Author: devinoldenburg* | **Open**  
   `gpt-5.5-pro` shows up as selectable for OAuth ChatGPT users but fails on every request. This PR filters `-pro` models from the non-Plus account model list.

4. **[#27554 – feat(opencode): local LAN provider discovery](https://github.com/anomalyco/opencode/pull/27554)**  
   *Author: androidand* | **Open**  
   Adds mDNS-based auto-discovery for local OpenAI-compatible servers (e.g., llama.cpp, vLLM) in the `/connect` flow. A significant UX improvement for self-hosters.

5. **[#27940 – fix(plugin): refresh mutable specs during install](https://github.com/anomalyco/opencode/pull/27940)**  
   *Author: samiralibabic* | **Merged**  
   Part of the large automated cleanup batch. Fixes a bug where plugin specs weren't refreshed during explicit install/update commands. Startup auto-refresh for floating specs remains out of scope.

6. **[#27939 – feat(session): add configurable fallback model chain](https://github.com/anomalyco/opencode/pull/27939)**  
   *Author: loss-and-quick* | **Merged**  
   Adds a configurable fallback chain so that when the primary model fails or hits rate limits, OpenCode gracefully degrades to secondary models. Closes #7602.

7. **[#27938 – feat: add provider and per-model concurrency limits](https://github.com/anomalyco/opencode/pull/27938)**  
   *Author: tjokinen* | **Merged**  
   Adds optional `maxConcurrency` fields per provider/model to prevent rejection from providers with concurrent-request caps. Closes #12019 and #26314.

8. **[#27936 – fix(app): add service worker for cache-first static asset loading](https://github.com/anomalyco/opencode/pull/27936)**  
   *Author: BYK* | **Merged**  
   Three frontend optimizations: service worker with cache-first strategy, inline critical CSS, and preload module scripts. Aims to improve web app load time significantly.

9. **[#27935 – fix(server): add zstd HTTP compression with gzip fallback](https://github.com/anomalyco/opencode/pull/27935)**  
   *Author: BYK* | **Merged**  
   Adds zstd (Zstandard) compression as the preferred encoding, falling back to gzip/deflate. Modern browsers will see faster asset transfers.

10. **[#26861 – fix(tui): Old messages disappearing during long sessions](https://github.com/anomalyco/opencode/pull/26861)**  
    *Author: vpetrigo* | **Open**  
    Implements lazy-scroll loading in the TUI to prevent message loss in long sessions. Scroll-up triggers loading of next 50 older messages. Fixes #7380.

---

## Feature Request Trends

- **Session Lifecycle Commands**: The `/goal` proposal (#27167) and `/loop` execution (#18001) signal strong desire for structured, persistent session behavior beyond ad-hoc prompting. Combined, these two features would allow users to define objectives and iterate automatically.
- **Skill Discovery & Selection**: Issues #21495 (recursive skill discovery) and #22129 (TUI autocomplete for skills) indicate that the skills system has adoption friction—users want skills to be discoverable and selectable from any interface.
- **Plugin/Middleware Pipeline**: Issue #5148 asks for middleware-style data flow control in the plugin system, suggesting power users want to intercept and transform data at multiple stages of the agent loop.
- **Pricing Flexibility**: Issues #24879 (Go Pro tier) and #32605 (more Go plan suggestions) show users hitting usage caps and requesting intermediate pricing tiers between Go and Zen.

---

## Developer Pain Points

1. **Random Hangs / Freezes** (#2940, #8345): OpenCode becoming completely unresponsive remains the most-reported stability issue. Users on Laravel projects, macOS Tahoe, and various shells all report similar symptoms with no consistent workaround.
2. **Model Compatibility Regressions**: Multiple reports of previously working models breaking—vision (image reading, #25832), DeepSeek edit tool (#31849), MiniMax M3 tool-call history (#32608, #32611, #32614). Tool-call format divergence between providers is a recurring theme.
3. **CPU & Memory Inefficiency** (#21470): Users report OpenCode consuming 50× more CPU than the model API calls, suggesting heavy local processing overhead in the agent loop or context management.
4. **Clipboard & Input/Output Bugs** (#7048): The "Copied to clipboard" bug on Linux persists, blocking basic copy-paste workflows in the TUI.
5. **LM Studio Model Refresh** (#2047): Users running local models face a workflow blocker—adding/removing models in LM Studio requires cumbersome auth cycles to refresh the model list in OpenCode.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-17

## Today's Highlights
Two minor patch releases (v0.79.5 and v0.79.6) landed with focused fixes for HTTP dispatcher behavior and DeepSeek V4 thinking compatibility. Community attention remains concentrated on connection reliability with OpenAI Codex and provider-specific configuration gaps, with a notable surge of PRs addressing error handling, latency metrics, and tool call validation.

## Releases

**v0.79.6** — [Release](https://github.com/earendil-works/pi/releases/tag/v0.79.6)
- Fixed HTTP dispatcher to preserve caller's deliberate `fetch` override instead of reinstalling global undici fetch
- Fixed inherited DeepSeek V4 thinking-off requests to send `thinking: { type: "disabled" }` compatibility parameter

**v0.79.5** — [Release](https://github.com/earendil-works/pi/releases/tag/v0.79.5)
- **Provider-scoped API key environments**: `auth.json` entries can now include per-provider `env` overrides for Cloudflare, Azure OpenAI, Google Vertex, Amazon Bedrock, cache retention, and proxy settings without modifying the project shell

## Hot Issues

1. **[#4945] openai-codex Connection Reliability Issues** ([Issue](https://github.com/earendil-works/pi/issues/4945))  
   ⚡ 59 comments, 30 👍 — TUI hangs on `Working...` with no output or error; only escape key recovers. Ongoing for 3+ weeks, highest community engagement.

2. **[#4877] Session folder collision** ([Issue](https://github.com/earendil-works/pi/issues/4877))  
   ⚡ 19 comments — Different file paths can hash to the same session folder (e.g., `/a/b/c/d` vs `/a-b/c-d`). Low severity but potential data confusion.

3. **[#5696] Model name not refreshing in TUI on CTRL+P** ([Issue](https://github.com/earendil-works/pi/issues/5696))  
   ⚡ 9 comments — Switching models via CTRL+P shows stale display; actually skips the first press. UX regression.

4. **[#5687] `pi list` and `pi update` hang with MCP servers** ([Issue](https://github.com/earendil-works/pi/issues/5687))  
   ⚡ 8 comments — Package subcommands never exit when an extension runs a long-lived MCP server. Affects automation.

5. **[#5816] `search` tool not found** ([Issue](https://github.com/earendil-works/pi/issues/5816))  
   ⚡ 7 comments — v0.79.4 regression: Pi keeps trying `search` tool and failing with "Tool search not found." Blocks codebase changes.

6. **[#5790] Support httpProxy in settings.json** ([Issue](https://github.com/earendil-works/pi/issues/5790))  
   ⚡ 7 comments — Request to set HTTP proxy in config instead of environment variables. Cleaner for corporate environments.

7. **[#5571] `pi -p` hangs on non-TTY stdin** ([Issue](https://github.com/earendil-works/pi/issues/5571))  
   ⚡ 7 comments — Fails to error fast when provider has no credentials; hangs 3+ minutes. CI/CD and pipe users affected.

8. **[#5728] Provider-specific config in auth.json** ([Issue](https://github.com/earendil-works/pi/issues/5728))  
   ⚡ 7 comments — Some providers need more than API keys (e.g., Cloudflare needs accountId/gatewayId). Users want all config in one file.

9. **[#5763] Providers swallow HTTP error bodies** ([Issue](https://github.com/earendil-works/pi/issues/5763))  
   ⚡ 4 comments — Behind proxies/gateways, non-2xx responses lose the body. Debugging becomes guesswork.

10. **[#5811] DeepSeek V4 tool call serialization error** ([Issue](https://github.com/earendil-works/pi/issues/5811))  
    ⚡ 3 comments — Valid tool call/result pairs produce "Messages with role 'tool' must be a response to a preceding message with 'tool_calls'" — thinking/tool replay issue.

## Key PR Progress

1. **[#5820] Preserve raw HTTP error status and bodies** ([PR](https://github.com/earendil-works/pi/pull/5820))  
   Shared error helper to surface HTTP status and raw body from non-schema errors. Closes #5763.

2. **[#5812] Protect pipe chars inside inline code in markdown tables** ([PR](https://github.com/earendil-works/pi/pull/5812))  
   Custom tokenizer prevents `|` inside backticks from being misinterpreted as column delimiters.

3. **[#5807] Provider-scoped environment overrides** ([PR](https://github.com/earendil-works/pi/pull/5807))  
   `auth.json` entries can include `env` object. Takes precedence over process env vars for provider config.

4. **[#5809] Add durationMs and timeToFirstTokenMs to Usage** ([PR](https://github.com/earendil-works/pi/pull/5809))  
   Adds latency/throughput metrics to `AssistantMessage.usage`; displays tokens/sec in footer.

5. **[#5789] Restore cursorUp line-start jump** ([PR](https://github.com/earendil-works/pi/pull/5789))  
   Fixes history browsing regression where pressing Up on first line would enter history instead of jumping to line start.

6. **[#5803] Reject malformed OpenAI tool calls** ([PR](https://github.com/earendil-works/pi/pull/5803))  
   Prevents persistence of tool calls missing id or function name from streamed responses.

7. **[#5801] Nix flake packaging** ([PR](https://github.com/earendil-works/pi/pull/5801))  
   Adds `nix build` and `nix run` support; enables reproducible builds and NixOS integration.

8. **[#5798] Vercel AI Gateway attribution headers** ([PR](https://github.com/earendil-works/pi/pull/5798))  
   Adds `http-referer` and `x-title` headers for Vercel AI Gateway identification.

9. **[#5796] Bump TS target to ES2024, use Promise.withResolvers()** ([PR](https://github.com/earendil-works/pi/pull/5796))  
   Replaces hand-rolled deferred implementations with native `Promise.withResolvers()`.

## Feature Request Trends

- **Provider configuration consolidation**: Strong demand for `auth.json` to host all provider-specific settings (account IDs, gateway IDs, regions) rather than splitting across env vars and config files
- **Proxy support**: Corporate users want config-file-based HTTP proxy settings, not just environment variables
- **OAuth customization**: Callers want to provide custom callback page renderers for OAuth login flows
- **RPC session access**: Request for `get_entries` and `get_tree` RPC commands to enable external tool integration
- **Nix/NixOS support**: Flake-based packaging now submitted (PR #5801), reflecting growing Nix community

## Developer Pain Points

- **Connection reliability**: OpenAI Codex users consistently report TUI freezes on `Working...` with no recovery path
- **Provider-specific serialization bugs**: DeepSeek V4 (thinking/tool replay), Moonshot/Kimi (schema conflicts), and OpenAI-responses (null-content drops) reveal ongoing LLM compatibility friction
- **Tool call fragility**: Multiple reports of tool calls being lost, malformed, or failing silently during streaming
- **Terminal compatibility**: Kitty (double backspace/enter), Warp (broken OSC 8 links), and Windows Terminal (scroll jumps) show ongoing TUI polish gaps
- **Startup/self-update issues**: Update banner suggests `pi update` even for Nix-installed versions that cannot self-update

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-06-17

## Today's Highlights
Release v0.18.1-preview.0 shipped with a fix for oversized context instructions, but the release pipeline encountered failures for subsequent builds. Community activity surged around the OAuth free tier policy change (Issue #3203, 136 comments), terminal SGR mouse mode cleanup, and foundational work for a self-paced `/loop` alignment with Claude Code's `ScheduleWakeup`. The team also merged critical fixes for glibc compatibility during auto-update and SGR mouse mode cleanup on exit.

## Releases
- **v0.18.1-preview.0**: Patch release that warns on oversized context instructions and fixes stale defaults, CLI syntax, and tool naming drift in documentation. [Release Notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.1-preview.0)
- Release workflows for `v0.18.1-preview.1` and `v0.18.1-nightly.20260617.4c6faf01a` both failed; see [Issue #5215](https://github.com/QwenLM/qwen-code/issues/5215) and [#5214](https://github.com/QwenLM/qwen-code/issues/5214).

## Hot Issues (10 noteworthy)

1. **[#3203 – Qwen OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)**  
   *Status: OPEN, 136 comments*  
   Proposes reducing daily free quota from 1,000 to 100 requests/day and phasing out the free tier entirely. Heavily debated — community reaction is intense.

2. **[#5055 – Trojan:JS/ShaiWorm.DBA!MTB](https://github.com/QwenLM/qwen-code/issues/5055)**  
   *Status: OPEN, Priority P1*  
   Windows Defender flags the VSCode extension VSIX as a trojan. Has serious trust implications for Windows users.

3. **[#5212 – Terminal stuck in SGR mouse mode after qwen exits](https://github.com/QwenLM/qwen-code/issues/5212)**  
   *Status: CLOSED*  
   Mouse unusable after abnormal termination; cause traced to missing writeSync in exit handler. Fixed within 24 hours.

4. **[#5210 – 0.18.1 ExitPlanMode stuck](https://github.com/QwenLM/qwen-code/issues/5210)**  
   *Status: OPEN, Priority P2*  
   Chinese user reports model frozen in ExitPlanMode for 7+ hours. Related to plan gate AbortSignal isolation issues in #5185.

5. **[#5206 – Auto-update fails on older glibc (CentOS 7)](https://github.com/QwenLM/qwen-code/issues/5206)**  
   *Status: CLOSED*  
   `sudo-required npm installs` silently migrate to standalone installer which bundles Node 22 requiring glibc ≥ 2.28. Fixed in PR #5207.

6. **[#5180 – Multi-agent task crash halfway](https://github.com/QwenLM/qwen-code/issues/5180)**  
   *Status: OPEN, Priority P2*  
   A 12-hour multi-agent session crashed mid-execution during a master/subagent workflow. Token management or memory issue suspected.

7. **[#5160 – `/model` shows discontinued OAuth model even without OAuth configured](https://github.com/QwenLM/qwen-code/issues/5160)**  
   *Status: CLOSED*  
   UI bug causing confusion; model selector incorrectly lists discontinued qwen-oauth coder-model. Welcome PR.

8. **[#5208 – Stale `.qwen-session` marker blocks worktree cleanup across sessions](https://github.com/QwenLM/qwen-code/issues/5208)**  
   *Status: OPEN, Priority P2*  
   Session marker prevents cleanup of worktrees created by previous sessions — disrupts git workflow.

9. **[#5124 – Track `/loop` alignment work](https://github.com/QwenLM/qwen-code/issues/5124)**  
   *Status: OPEN*  
   Parent issue tracking staged alignment of `/loop` with Claude Code's self-paced loop behavior. 3 child issues/PRs already filed.

10. **[#5177 – `exit_plan_mode` fails with empty plan parameter, causing wasted retry turns](https://github.com/QwenLM/qwen-code/issues/5177)**  
    *Status: CLOSED*  
    Model calls exit_plan_mode with empty `plan` param, triggering API retries. Simple validation fix landed.

## Key PR Progress (10 important)

1. **[#5207 – fix(cli): keep sudo-required npm installs on npm instead of migrating to standalone](https://github.com/QwenLM/qwen-code/pull/5207)**  
   Critical fix: prevents silent migration to standalone installer on older glibc systems (CentOS 7). Closes #5206.

2. **[#5213 – fix(cli): use writeSync in exit handler to disable SGR mouse mode](https://github.com/QwenLM/qwen-code/pull/5213)**  
   Fast turnaround on terminal usability bug (#5212). Ensures mouse mode is always reset on exit.

3. **[#5182 – feat(loop): add second-resolution session wakeup engine](https://github.com/QwenLM/qwen-code/pull/5182)**  
   Step 1 of `/loop` alignment: introduces `CronScheduler` engine for self-paced wakeup. Closes #5156.

4. **[#5197 – feat(loop): wire prompt-only /loop to self-paced wakeups](https://github.com/QwenLM/qwen-code/pull/5197)**  
   Step 2: `/loop <prompt>` now runs the prompt immediately and schedules at most one future continuation. Closes #5184.

5. **[#5202 – feat(channel): add QQ Bot channel adapter](https://github.com/QwenLM/qwen-code/pull/5202)**  
   New `@qwen-code/channel-qqbot` adapter with WebSocket Gateway support, joining telegram/weixin/dingtalk/feishu.

6. **[#5179 – fix(model): remember selected provider when multiple share a model id](https://github.com/QwenLM/qwen-code/pull/5179)**  
   Persists `baseUrl` along with model name so provider selection survives session restarts.

7. **[#5126 – feat(vision-bridge): transcribe images to text for text-only models](https://github.com/QwenLM/qwen-code/pull/5126)**  
   Opt-in feature: sends images to a multimodal model and returns text to the primary text-only model. Disabled by default.

8. **[#5189 – fix(web-shell): localize remaining hardcoded UI strings](https://github.com/QwenLM/qwen-code/pull/5189)**  
   Routes dialog close button tooltips and other strings through i18n. English + Simplified Chinese added.

9. **[#5185 – fix(plan-gate): isolate gate agent AbortSignal from parent signal chain](https://github.com/QwenLM/qwen-code/pull/5185)**  
   Fixes infinite retry loop in plan approval gate when using `exit_plan_mode` in AUTO/YOLO mode. Addresses #5210 symptoms.

10. **[#4918 – feat(hooks): pass original API call ID (toolCallId) to hook system](https://github.com/QwenLM/qwen-code/pull/4918)**  
    Adds `tool_call_id` to all hook interfaces, enabling tracing across PreToolUse → PostToolUse → Failure → PermissionDenied.

## Feature Request Trends
- **Multi-agent & background automation**: Strong demand for self-paced `/loop` (#5124, #5156, #5184), dynamic workflows a la Claude Code (#4721), and background task scheduling.  
- **Channel expansion**: QQ Bot adapter (#5201) is merged; community expects more regional chat platforms.  
- **Smarter model/provider selection**: Remember user's provider choice across sessions (#5179), filter discontinued models (#5160).  
- **Vision bridge**: Transcribe images into text for text-only models (#5126) — opt-in but highly requested.  
- **Internationalization**: Multiple PRs localize hardcoded English strings (#5186, #5189); Chinese locale is top priority.

## Developer Pain Points
- **Auto-update fragility on Linux**: `glibc` mismatch (#5206) and `sudo`-required npm install migration cause silent failures on CentOS 7 / older glibc systems.  
- **Terminal state pollution**: SGR mouse mode stuck on exit (#5212) — basic UX issue that disrupts developer workflow.  
- **OAuth model confusion**: Discontinued OAuth model still appears in menus (#5160); users unsure which model/provider to use.  
- **Windows-specific issues**: AV false positive (#5055), React minified error (#5199), cmd vs pwsh confusion (#4562).  
- **Plan mode stalls**: `exit_plan_mode` fails with empty params (#5177) or hangs indefinitely (#5210) — critical for users relying on plan-then-execute workflows.  
- **Multi-agent session crashes**: 12-hour sessions crash midway (#5180); no clear root cause yet, suspected memory/token management.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-17

## Today's Highlights
The project has officially **rebranded from `deepseek-tui` to `CodeWhale`** with v0.8.61 as the canonical release — the legacy npm package is deprecated. A flurry of activity around **provider compatibility** (DeepInfra, Novita, Moonshot fixes land) and **TUI UX regressions** (digit key hijacking, paste behavior) dominated the last 24h. Meanwhile, the stalled-turn issue (#2487) remains the most painful open bug, now spanning two weeks with 14 comments.

## Releases
- **v0.8.61 (CodeWhale)**: Rebranded project — npm package is now `codewhale`. The legacy `deepseek-tui` package receives no further updates. Users must migrate per `docs/REBRAND.md`.
  - *Link*: [v0.8.61](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.61)

## Hot Issues
1. **#2487 — Stalled turn / no completion signal (OPEN)**  
   *Severity: Critical.* Yolo-mode operations freeze with "Turn stalled" prompt; even `continue` cannot resume. 14 comments, 2 weeks unresolved. Community is frustrated — this is a core reliability blocker.  
   *Link*: [Issue #2487](https://github.com/Hmbown/CodeWhale/issues/2487)

2. **#3275 — CodeWhale over-extends scope, self-questioning loop (OPEN)**  
   A regression from #3061: the agent modifies beyond user intent, enters self-driven Q&A without waiting for confirmation. Community reports loss of control.  
   *Link*: [Issue #3275](https://github.com/Hmbown/CodeWhale/issues/3275)

3. **#3264 — Restrict skill scanning directory (OPEN)**  
   Request to limit skill discovery to `~/.codewhale/skills/` only — currently scans too broadly, causing startup slowdowns. Low effort, high impact.  
   *Link*: [Issue #3264](https://github.com/Hmbown/CodeWhale/issues/3264)

4. **#3240 — Legacy `.deepseek` config directory still created (OPEN)**  
   Post-rebrand, Windows users get both `.codewhale` **and** `.deepseek` folders. Clean migration bug.  
   *Link*: [Issue #3240](https://github.com/Hmbown/CodeWhale/issues/3240)

5. **#3238 — glibc mismatch on Ubuntu 22.04 (OPEN)**  
   Pre-built binary fails due to glibc version requirement. Blocks adoption on older LTS. Workaround: build from source.  
   *Link*: [Issue #3238](https://github.com/Hmbown/CodeWhale/issues/3238)

6. **#3273 — js_execution ignores proxy config on Windows (OPEN)**  
   Shell tools work behind VPN/proxy, but built-in `js_execution` times out. Windows-specific, affects enterprise users.  
   *Link*: [Issue #3273](https://github.com/Hmbown/CodeWhale/issues/3273)

7. **#2739 — Chinese user: task freeze during long operations (OPEN)**  
   Freezing on long bug-fix tasks; `--continue` loses all session context. User says "unbearable" — same bug keeps recurring across versions.  
   *Link*: [Issue #2739](https://github.com/Hmbown/CodeWhale/issues/2739)

8. **#3102 — Clarification question UI for agents (CLOSED)**  
   Agents can now ask users clarifying questions through modal UI instead of chat noise. Closed as implemented — improves agent reliability.  
   *Link*: [Issue #3102](https://github.com/Hmbown/CodeWhale/issues/3102)

9. **#3266 — Sub-agent `agent_eval` with `block=True` causes deadlock (CLOSED)**  
   Multiple sub-agents with blocking eval freeze TUI. Fixed — important for multi-agent workflows.  
   *Link*: [Issue #3266](https://github.com/Hmbown/CodeWhale/issues/3266)

10. **#3265 — Moonshot/Kimi API rejects empty tool parameters (CLOSED)**  
    Every request failed with `tools.function.parameters.type` required bug. Fixed by ensuring `"type": "object"` in tool definitions.  
    *Link*: [Issue #3265](https://github.com/Hmbown/CodeWhale/issues/3265)

## Key PR Progress
1. **#3271 — Add Ponytail personality reference (CLOSED)**  
   Docs addition — CodeWhale will officially recommend Ponytail as an agent personality. Blocked upstream.  
   *Link*: [PR #3271](https://github.com/Hmbown/CodeWhale/pull/3271)

2. **#3269 — Slash commands as hotbar actions (CLOSED)**  
   Users can now bind `slash.mode`, `slash.task`, etc. to hotbar slots. Key UX improvement for power users.  
   *Link*: [PR #3269](https://github.com/Hmbown/CodeWhale/pull/3269)

3. **#3270 — Linux build deps documentation (CLOSED)**  
   Adds `libdbus-1-dev` and `pkg-config` to cargo install guide. Fixes bare Ubuntu install failures.  
   *Link*: [PR #3270](https://github.com/Hmbown/CodeWhale/pull/3270)

4. **#3274 — Static musl Linux binaries (OPEN)**  
   Switches release builds from glibc to musl for static linking. Solves glibc version mismatch on older distros.  
   *Link*: [PR #3274](https://github.com/Hmbown/CodeWhale/pull/3274)

5. **#3236 — DeepInfra provider support (CLOSED)**  
   Adds DeepInfra as a first-class provider with alias wiring, registry docs. Community-contributed.  
   *Link*: [PR #3236](https://github.com/Hmbown/CodeWhale/pull/3236)

6. **#3267 — Keep large pasted text editable (CLOSED)**  
   Instead of replacing paste with `@file` mention, keeps text inline with truncation + auto-expand. Solves #3263 UX regression.  
   *Link*: [PR #3267](https://github.com/Hmbown/CodeWhale/pull/3267)

7. **#2933 — Hippocampal memory v2 system (OPEN)**  
   Major upgrade: glossary, namespaces, rollback, auto-inject, background daemon. Still needs human review. High-risk, high-reward.  
   *Link*: [PR #2933](https://github.com/Hmbown/CodeWhale/pull/2933)

8. **#2998 — Tailwind v3→v4 migration for /web (CLOSED)**  
   Dependabot-driven migration closed; superseded by issue #3276 for proper planning.  
   *Link*: [PR #2998](https://github.com/Hmbown/CodeWhale/pull/2998)

9. **#3071, #3072, #3073 — Model metadata registry (all CLOSED)**  
   Trio of PRs: introduce registry, hydrate from provider APIs, audit hard-coded lists. Foundation for future model management.  
   *Link*: [#3071](https://github.com/Hmbown/CodeWhale/pull/3071), [#3072](https://github.com/Hmbown/CodeWhale/pull/3072), [#3073](https://github.com/Hmbown/CodeWhale/pull/3073)

10. **#3255 — Fix Novita provider 404 (CLOSED)**  
    Missing `/openai` segment in base URL fixed — Novita is now usable.  
    *Link*: [PR #3255](https://github.com/Hmbown/CodeWhale/pull/3255)

## Feature Request Trends
- **Provider expansion**: DeepInfra (#3231), Novita (#3255), Moonshot/Kimi (#3265) — community wants broad provider support, especially alternative API-compatible backends.
- **Memory & context systems**: Hippocampal v2 (#2933) and model metadata registry (#3071-3073) indicate a push toward persistent, structured agent memory.
- **Clarification & confirmation UI**: Agents asking direct questions (#3102) and respecting user intent boundaries (#3275) — users want more control over agent autonomy.
- **TUI ergonomics**: Hotbar enhancements (#3269), paste handling (#3267), digit key fix (#3243) — continuous polish of the terminal experience.
- **Skill scanning control**: Request to restrict skill discovery scope (#3264) — performance and security concerns.

## Developer Pain Points
- **Stalled turns / freezing (#2487, #2739)**: The #1 reliability issue. Turns stall without completion signal; sessions are lost. Multiple users report this across versions. **Needs urgent attention.**
- **Agent over-autonomy (#3275)**: Regression where agents modify beyond requests without waiting for confirmation. Frustrates users who want predictable behavior.
- **Cross-platform build problems**: glibc mismatch (#3238), missing build deps (#3270), static binary requests (#3274) — Linux packaging is inconsistent.
- **Rebrand migration bugs**: Legacy config folders still created (#3240), npm package deprecated but docs still reference old names.
- **Proxy/VPN incompatibility**: js_execution tool ignores proxy env on Windows (#3273) — blocks enterprise adoption.
- **Sub-agent deadlocks**: Blocking eval freeze (#3266) — multi-agent workflows still fragile.
- **Provider API quirks**: Moonshot/Kimi required `"type": "object"` in tool params (#3265), Novita missing path segment (#3255) — each provider needs individual compatibility shims.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*