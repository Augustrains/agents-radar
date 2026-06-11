# AI CLI Tools Community Digest 2026-06-11

> Generated: 2026-06-11 02:14 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Ecosystem Comparison Report
**Date:** 2026-06-11

---

## 1. Ecosystem Overview

The AI CLI tools landscape continues to mature rapidly, with **Claude Code** and **OpenAI Codex** maintaining dominant positions in terms of community size and feature velocity, while several Chinese-origin tools (Kimi Code, Qwen Code) and community-driven projects (CodeWhale, Pi) are closing feature gaps at impressive speed. The ecosystem is converging on core patterns—sub-agent orchestration, auto-memory, MCP integration, and autonomous execution modes—while each tool differentiates on model provider strategy, security posture, and platform support. **Terminal stability, Windows compatibility, and streaming reliability** are the most persistent quality gaps across the board, and **provider-agnostic architectures** are emerging as a key competitive battleground.

**Key takeaway:** The market is shifting from "does it work?" to "does it work *reliably* and *efficiently* across my entire stack?"—a maturation that favors tools with strong testing, security, and cross-platform investment.

---

## 2. Activity Comparison

| Tool | Open Issues (≈) | PRs Today | Recent Releases | Release Velocity |
|------|----------------|-----------|-----------------|------------------|
| **Claude Code** (Anthropic) | ~300+ (18 hot) | 10 PRs | v2.1.172 (today) | High; ~weekly releases |
| **OpenAI Codex** | ~250+ (10 hot) | 10 PRs | rust-v0.140.0-alpha.7 (today) | High; alpha churn active |
| **Gemini CLI** (Google) | ~200+ (10 hot) | 10 PRs | None today | Moderate; dependency bumps |
| **GitHub Copilot CLI** | ~150+ (10 hot) | 0 PRs | v1.0.60 (Jun 5) | Low; quiet since v1.0.60 |
| **Kimi Code** (MoonshotAI) | ~100+ (10 hot) | 23 PRs (20 merged) | v0.12.0 (prior) | High; stability fix wave |
| **OpenCode** | ~200+ (10 hot) | 12 PRs | v1.17.1–v1.17.3 (today) | High; patch-triple today |
| **Pi** | ~100+ (10 hot) | 10 PRs | None today | Moderate; active PR pipeline |
| **Qwen Code** (Alibaba) | ~150+ (10 hot) | 14 PRs | None today | High; large feature merges |
| **CodeWhale** (ex-DeepSeek TUI) | ~50+ (10 hot) | 14 PRs | v0.8.56–v0.8.57 (today) | High; rebrand + feature burst |

**Observation:** Claude Code, Kimi Code, and OpenCode are shipping most frequently. OpenAI Codex and Qwen Code are in active alpha/feature merge cycles. GitHub Copilot CLI and Gemini CLI show lower visible release velocity, though internal work is ongoing. CodeWhale is undergoing a rapid rebrand-and-release sprint.

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities, indicating strong cross-cutting demand:

### 3.1 Multi-Provider / Model-Agnostic Architecture
- **Claude Code, OpenAI Codex, Pi, CodeWhale, Qwen Code, Kimi Code** — Users consistently demand the ability to use **non-native models** (Opus via CLI, GPT via non-Codex tools, DeepSeek, Qwen, Ollama local). Tools that hardcode provider assumptions lose users who want **freedom of choice** across cost, latency, and capability dimensions.
- **Specific needs:** Automatic provider fallback on API failure, proper schema coercion for non-native APIs, model-aware system prompts (not assuming "you are DeepSeek V4").

### 3.2 Sub-Agent Reliability & Governance
- **Claude Code, Gemini CLI, Copilot CLI, Qwen Code, CodeWhale** — Sub-agents are a core differentiator, but **false success reporting, silent hangs, and permission surprises** plague every implementation. Users want:
  - True max-turn accounting (not falsely reporting success on interrupt)
  - Approval queues for sub-agent tool calls (not silent deny)
  - Background sub-agent progress without UI freeze
  - Persistent agent teams (Claude Code's v2.1.172 hierarchy is a direct response)

### 3.3 Secrets & Security Infrastructure
- **Claude Code, Gemini CLI, Qwen Code, CodeWhale** — As AI tools enter CI/CD and production pipelines, users demand:
  - **Native secrets management** (not plaintext env vars or dotfiles)
  - **Script-based key retrieval** (KeePassXC, 1Password integration)
  - **Deterministic secret redaction** before memory/transcript processing
  - **Sandboxed tool execution** with granular permission systems

### 3.4 Persistent Memory & Cross-Session State
- **Claude Code, Gemini CLI, Codex, OpenCode, Qwen Code** — Memory is considered table stakes, but users report:
  - **Auto-memory interference** — irrelevant context injected without user control
  - **Session corruption on crash** — orphaned tool calls, broken JSONL
  - **Cross-session analytics** — persistent `/stats` dashboards
  - **Compaction configuration** — context-window management still opaque

### 3.5 Terminal UI Robustness
- **All tools** — Streaming corruption, resize instability, cooked-mode drops, SGR sequence leaks, and copy-paste failures are universal. Specific shared issues:
  - **Wayland compatibility** (Gemini CLI, Pi)
  - **Windows console font resets** (Kimi Code, Pi)
  - **Non-ASCII i18n gaps** (Codex, Pi, CodeWhale)
  - **Ctrl+C / clipboard conflicts** (Copilot CLI, Pi)

### 3.6 Windows & ARM64 Parity
- **Claude Code, Codex, Kimi Code, Copilot CLI, OpenCode** — Windows remains a **second-class platform** despite growing adoption. Specific shared gaps:
  - **ARM64 (Snapdragon X) support** (Claude Code #50674, Codex #27323)
  - **WSL remote integration** (Claude Code #49933)
  - **Crash-on-launch regressions** (Codex #27175, #27367)
  - **Hardcoded POSIX assumptions** in file paths, subprocess flags

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | CodeWhale |
|-----------|-------------|--------------|------------|-------------|-----------|----------|----|-----------|-----------|
| **Primary Model** | Claude (Opus) | GPT-5.5 | Gemini 2.5+ | Multi-model | Kimi K2.6 | Multi-model | Multi-model | Qwen | DeepSeek (rebranding) |
| **Sub-Agent Depth** | 5-level recursive | 1-level | 1-level | 1-level | 1-level | 1-level | 1-level | Team mode (parallel) | 1-level |
| **Autonomous Mode** | Cowork | Goal Mode | (Partial) | (Partial) | YOLO mode | /goal (WIP) | Coding agent | Agent Team | Headless exec |
| **Security Focus** | Moderate | Moderate | High | Enterprise (MCP policy) | Low | Low | Moderate | Low | Low |
| **Windows Support** | Partial (bugs) | Poor (crash) | Partial | Good | Improving | Partial | Moderate | (Unknown) | Partial |
| **Plugin/Ext System** | MCP + plugins | Plugin MCP | (None visible) | MCP (broken) | (Minimal) | Skill/prompt | Extension system | Extension system | Hooks v2 |
| **Local LLM Support** | Limited | No | No | No | Partial | Good (Ollama) | Good (vLLM) | Partial | Partial |
| **CI/CD Headless** | Cowork mode | Goal mode | (Partial) | (No) | YOLO mode | (No) | Experimental | Daemon mode | Headless exec |
| **Community (GitHub)** | Very large | Large | Medium | Medium | Small | Medium | Small | Medium | Small (growing) |

**Key differentiators:**

- **Claude Code** wins on **sub-agent depth** (5-level recursion) and **enterprise features** (Amazon Bedrock region resolution, proxy forwarding), but suffers from **memory leaks** and **model rule non-compliance**.
- **OpenAI Codex** leads on **context-window tooling** (compaction, resize-all-images) and **streaming performance** but has a **Windows stability crisis** and **token consumption alarm**.
- **Gemini CLI** emphasizes **AST-aware code navigation** and **security hardening** (path traversal fixes, CI artifact protection), but **sub-agent reliability** remains its weakest link.
- **Copilot CLI** benefits from **GitHub ecosystem integration** but is **stagnating on feature velocity** and **losing model parity** with VS Code.
- **Kimi Code** is shipping **fast stability fixes** (session resilience, orphan process cleanup) and is strongest on **cross-platform parity** improvements.
- **OpenCode** is the most **provider-agnostic** with good local LLM support, but suffers from **performance regressions** (CPU, snapshot size).
- **Pi** excels at **custom provider support** (Palantir Foundry, Bedrock Mantle) and **i18n quality** (CJK text wrapping), but has **TUI null-safety crashes**.
- **Qwen Code** is investing heavily in **daemon mode** and **agent teams** (parallel sub-agents), with strong **extension management** and **file history snapshots**.
- **CodeWhale** (ex-DeepSeek TUI) is **rapidly rebranding** and adding **hooks v2**, **voice input**, and **headless exec hardening**, but suffers from **rebrand migration friction** and **provider configuration complexity**.

---

## 5. Community Momentum & Maturity

### High Momentum (Rapid iteration, high community engagement)
1. **Claude Code** — Largest community (580 👍 on #18435 alone), weekly releases, mature sub-agent system. Risk: unresolved memory leak (#11315) erodes trust.
2. **OpenAI Codex** — Very active alpha cycle (2 releases today), strong internal infrastructure investment (6 ARM64/Bazel PRs). Risk: Windows stability crisis and token billing concerns.
3. **Qwen Code** — Major feature merges (daemon mode + agent teams = 386 files changed), active UI polish. Highest codebase velocity this period.
4. **Kimi Code** — 23 PRs today (20 merged), aggressively fixing session resilience and Windows bugs. Strongest "stability sprint" signal.
5. **CodeWhale** — Rebranding + feature burst (14 PRs today), community contribution to voice input and hooks. Growing from small base.

### Moderate Momentum (Steady but not sprinting)
6. **OpenCode** — 3 patch releases today, active skill/plugin ecosystem. Performance regressions slowing momentum.
7. **Pi** — Active PR pipeline with enterprise provider expansions. Medium community engagement; trust features controversial.
8. **Gemini CLI** — Security-hardening PRs are welcome, but bug count (agent hangs, false completions) and slow sub-agent fixes frustrate community.

### Low Momentum (Stable but quiet)
9. **GitHub Copilot CLI** — 0 PRs today, last release 6 days ago. Model parity gap (#1703) and MCP policy bugs (#1707, #3756) driving users to alternatives. **Risk of stagnation** if model availability and terminal rendering issues aren't addressed.

---

## 6. Trend Signals

### 6.1 The "Provider Lock-in Backlash"
The single strongest signal across all communities: **users are actively resisting provider lock-in**. Every tool's issue tracker features complaints about:
- Hardcoded model assumptions in system prompts ("you are Claude/GPT/DeepSeek")
- Missing non-native model visibility in tool linters
- Cost arbitrage — users want to route cheap tasks to local LLMs and complex tasks to frontier models within the same session

**Implication:** Tools that invest in **provider-agnostic architectures** (runtime model lookups, automatic fallback chains, schema coercion) will win the next wave of adoption. OpenCode and Pi are currently best positioned; Claude Code and Codex need to open their model gates.

### 6.2 The "Agent Reliability Ceiling"
Sub-agent workflows are universally desired but universally breaking. The pattern is:
- **False success** (agent reports done when interrupted)
- **Silent hangs** (no error, no timeout)
- **Resource exhaustion** (runaway memory/token consumption)
- **State corruption** (orphan tool calls, broken session replay)

**Implication:** The community is hitting the **reliability ceiling** of current agent architectures. Claude Code's 5-level recursion is innovative but will amplify these failure modes. Expect investment in **agentic observability** — structured logging, session replay debugging, and deterministic retry protocols.

### 6.3 The Windows/ARM64 Platform Gap
Windows (especially ARM64) is systematically underserved. Every major tool has open crash-on-launch, font/encoding, or timeout bugs. This is particularly damaging because:
- ARM-based Windows (Snapdragon X) is growing
- WSL integration is a top request
- CI/CD runs on Windows servers

**Implication:** Tools that **invest in Windows CI/CD pipelines, ARM64 cross-compilation, and WSL-native UX** will capture an underserved but growing developer segment. Codex's ARM64 MinGW fix (#27323) and Kimi's Windows font fixes (#2289) are models to follow.

### 6.4 Security as Moat
Enterprise adoption is being gated by:
- Secrets in plaintext (dotfiles, env vars)
- No scriptable key retrieval (1Password/KeePassXC)
- Unredacted transcripts (memory leaks)
- Insecure plugin install paths (path traversal, CI artifact poisoning)

**Implication:** Gemini CLI's security PRs (#27767, #27753) and Claude Code's secrets management request (#29910) signal that **security posture is becoming a purchasing criterion**. Tools without native secret management will be excluded from enterprise procurement.

### 6.5 The "Second-Place" Tooling Renaissance
While Claude Code and Codex dominate mindshare, **OpenCode, Pi, Kimi Code, and CodeWhale** are shipping faster on developer experience gaps:
- OpenCode's provider-agnosticism + skill system
- Pi's custom provider/OAuth extensibility
- Kimi Code's session resilience and YOLO mode
- CodeWhale's voice input and headless exec

**Implication:** The market is fragmenting; no single tool will dominate. Developers will increasingly **maintain multiple AI CLI tools** for different workflows. Interoperability standards (ACP protocol, MCP, shared memory formats) will become infrastructure investments.

---

## Final Summary Table

| Dimension | Most Mature | Most Vulnerable | Emerging Threat |
|-----------|-------------|-----------------|-----------------|
| **Sub-Agent Depth** | Claude Code (5-level) | All others (1-level) | Qwen Code (parallel teams) |
| **Windows Support** | Copilot CLI | OpenAI Codex | Kimi Code (fastest bug-fix rate) |
| **Security** | Gemini CLI | Kimi Code, CodeWhale | Pi (Palantir/OAuth) |
| **Provider Agnostic** | OpenCode, Pi | Claude Code, Codex | CodeWhale (YAML constitution) |
| **CI/CD Readiness** | Claude Code (Cowork) | Copilot CLI | CodeWhale (headless exec) |
| **Community Velocity** | Claude Code, Codex | Copilot CLI | Qwen Code, CodeWhale |
| **i18n/Globalization** | Pi (CJK), CodeWhale (7 locales) | Codex (non-ASCII bug) | Kimi Code (GBK fixes) |

**Bottom line for technical decision-makers:** Choose your AI CLI tool based on your **primary model preference, platform stack, and security requirements** today — but invest in **polyglot tooling** and **provider-agnostic workflows**, because the landscape will look significantly different in 6 months. The tools that solve the reliability ceiling and the Windows gap will define the next generation.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-06-11 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following PRs represent the most-discussed Skill submissions by community engagement and comment volume:

### #83 — Skill-Quality-Analyzer & Skill-Security-Analyzer
**Author:** eovidiu | **Status:** Open  
**Functionality:** Two meta-skills for evaluating other Claude Skills: the quality analyzer scores across five dimensions (structure, documentation, reliability, security, usability); the security analyzer performs automated threat modeling and vulnerability scanning.  
**Discussion highlights:** Community debate centered on whether meta-skills belong in the main repo vs. a separate namespace. Several reviewers requested clearer output formats and integration examples.  
**Link:** [github.com/anthropics/skills/pull/83](https://github.com/anthropics/skills/pull/83)

### #514 — Document-Typography Skill
**Author:** PGTBoos | **Status:** Open  
**Functionality:** Prevents orphan word wrap (1–6 words spilling onto next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment in AI-generated documents.  
**Discussion highlights:** Broad agreement that these typographic issues affect every document Claude generates. The skill directly addresses a pain point users rarely articulate but frequently encounter. Several commenters suggested expanding to LaTeX output.  
**Link:** [github.com/anthropics/skills/pull/514](https://github.com/anthropics/skills/pull/514)

### #486 — ODT Skill (OpenDocument Creation & Parsing)
**Author:** GitHubNewbie0 | **Status:** Open  
**Functionality:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods) and HTML extraction from ODT. Triggers on mentions of "ODT", "ODS", "OpenDocument", or "LibreOffice" requests.  
**Discussion highlights:** Strong demand from enterprise and government users who rely on LibreOffice/OpenOffice. Technical discussion focused on maintaining format fidelity during round-trip conversions.  
**Link:** [github.com/anthropics/skills/pull/486](https://github.com/anthropics/skills/pull/486)

### #210 — Improved Frontend-Design Skill Clarity
**Author:** justinwetch | **Status:** Open  
**Functionality:** A comprehensive revision of the existing frontend-design skill to ensure instructions are specific, actionable, and executable within a single conversation. Clarifies design system conventions, component architecture, and responsive layout guidance.  
**Discussion highlights:** Received strong support for the refactoring approach. Commenters noted the original skill was too abstract; the revision introduces concrete examples and decision trees.  
**Link:** [github.com/anthropics/skills/pull/210](https://github.com/anthropics/skills/pull/210)

### #1046 — Multi-Skill Bundle (Frontend-Design, AI-Experience-Consultant, Automation-Workflows-Builder)
**Author:** ALMMECHANICAL | **Status:** Open  
**Functionality:** Adds three skill definition files simultaneously. The automation-workflows-builder skill is particularly notable for enabling multi-step workflow orchestration within Claude Code.  
**Discussion highlights:** Concerns about scope creep and whether bundling three unrelated skills in one PR complicates review. The automation-workflows component generated the most technical discussion.  
**Link:** [github.com/anthropics/skills/pull/1046](https://github.com/anthropics/skills/pull/1046)

### #723 — Testing-Patterns Skill
**Author:** 4444J99 | **Status:** Open  
**Functionality:** Comprehensive testing skill covering the full stack: testing philosophy (Testing Trophy model), unit testing (AAA pattern, pure functions), React component testing (Testing Library), integration testing, and E2E patterns.  
**Discussion highlights:** Highly praised as filling a critical gap in developer workflows. Reviewers requested additional coverage for mocking strategies and snapshot testing best practices.  
**Link:** [github.com/anthropics/skills/pull/723](https://github.com/anthropics/skills/pull/723)

### #181 — SAP-RPT-1-OSS Predictor Skill
**Author:** amitlals | **Status:** Open  
**Functionality:** Integrates SAP's open-source tabular foundation model (SAP-RPT-1-OSS) for predictive analytics on SAP business data. Teaches Claude to use this model for sales forecasting, inventory prediction, and financial anomaly detection.  
**Discussion highlights:** Niche but enthusiastic reception from enterprise SAP users. Technical discussion centered on data privacy when sending SAP data through the model pipeline.  
**Link:** [github.com/anthropics/skills/pull/181](https://github.com/anthropics/skills/pull/181)

### #806 — Sensory Skill (macOS AppleScript Automation)
**Author:** AdelElo13 | **Status:** Open  
**Functionality:** Teaches Claude to use `osascript` (AppleScript) for native macOS automation — a two-tier permission system: Tier 1 (direct app scripting, works out of the box), Tier 2 (Accessibility permissions for System Events UI scripting).  
**Discussion highlights:** Significant interest as an alternative to screenshot-based computer use. Security discussions around permission boundaries were thorough; the tiered approach became the consensus design.  
**Link:** [github.com/anthropics/skills/pull/806](https://github.com/anthropics/skills/pull/806)

---

## 2. Community Demand Trends

From Issue discussions, the following Skill directions show strongest community anticipation:

| Demand Category | Key Issues | Description |
|---|---|---|
| **Org-Wide Skill Sharing** | [#228](https://github.com/anthropics/skills/issues/228) (13 comments, 7 👍) | Persistent demand for enterprise-grade skill distribution: shared libraries, direct sharing links, and org-level management without manual file transfer |
| **Skill Evaluation & Quality** | [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍), [#1169](https://github.com/anthropics/skills/issues/1169) | Users report that skill evaluation tools (`run_eval.py`) produce 0% trigger rates — blocking any data-driven skill optimization. This is the #1 operational pain point |
| **Security & Trust Boundaries** | [#492](https://github.com/anthropics/skills/issues/492) (7 comments) | Community-made skills distributed under `anthropic/` namespace impersonate official Anthropic skills, creating trust boundary vulnerabilities |
| **Deduplication & Bundling** | [#189](https://github.com/anthropics/skills/issues/189) (6 comments, 8 👍) | `document-skills` and `example-skills` plugins install identical content, wasting context window space. Need for skill deduplication and a proper plugin containment policy |
| **Agent Governance** | [#412](https://github.com/anthropics/skills/issues/412) | Proposed skill for safety patterns in multi-agent systems: policy enforcement, threat detection, trust scoring, and audit trails |
| **Skills as MCPs** | [#16](https://github.com/anthropics/skills/issues/16) (4 comments) | Proposal to expose Skills via the Model Context Protocol, enabling programmatic invocation and composition |

**Key takeaway:** The community's strongest unmet need is not new Skill content, but rather **infrastructure for skill lifecycle management** — sharing, evaluation, security verification, and deduplication.

---

## 3. High-Potential Pending Skills

These PRs are actively discussed, not yet merged, and likely to land in the near term:

| PR | Skill | Why It's Close |
|---|---|---|
| [#1099](https://github.com/anthropics/skills/pull/1099) | Windows crash fix for `run_eval.py` | Critical bug fix for cross-platform parity |
| [#1050](https://github.com/anthropics/skills/pull/1050) | Windows subprocess + encoding fixes | Complementary fix resolving `claude.cmd` detection on Windows |
| [#539](https://github.com/anthropics/skills/pull/539), [#361](https://github.com/anthropics/skills/pull/361) | YAML unquoted description detection (dueling PRs) | Two PRs solving the same problem — resolution likely via merge of one plus credit to both authors |
| [#362](https://github.com/anthropics/skills/pull/362) | UTF-8 multi-byte character fix | Prevents Rust panics; narrow scope, high impact, low merge friction |
| [#509](https://github.com/anthropics/skills/pull/509) | CONTRIBUTING.md | Addresses GitHub community health score (25%); explicit ask from the community via Issue #452 |
| [#1140](https://github.com/anthropics/skills/pull/1140) | Agent-Creator meta-skill | Introduces task-specific agent sets; also fixes multi-tool evaluation and Windows support — large scope but fills a clear gap |
| [#147](https://github.com/anthropics/skills/pull/147) | Codebase-Inventory-Audit | Comprehensive 10-step orphaned code detection workflow; broad appeal for maintenance-heavy teams |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for operational infrastructure over creative content:** users urgently need standardized skill sharing, distribution, evaluation, and security verification tooling, rather than new domain-specific Skills — the ecosystem's bottleneck has shifted from *what Skills exist* to *how Skills are managed, validated, and shared* across teams and platforms.

---

# Claude Code Community Digest — 2026-06-11

## Today's Highlights

Anthropic shipped **v2.1.172** with a major architectural leap: sub-agents can now recursively spawn their own sub-agents up to 5 levels deep, enabling complex hierarchical agent orchestration. On the community side, the most requested feature ever — multi-account management in Claude Desktop (#18435) — continues to gather steam at 580 👍, while a critical memory leak (#11315, 64 comments) remains unresolved after seven months of discussion.

---

## Releases

**v2.1.172** — Notable changes:

- **Sub-agent recursion:** Sub-agents can now spawn their own sub-agents (up to 5 levels deep), enabling hierarchical agent trees for complex workflows
- **Amazon Bedrock region resolution:** Now reads AWS region from `~/.aws` config files when `AWS_REGION` is unset, matching AWS SDK precedence; `/status` command shows region provenance
- **Mark browsing UX:** Added a search bar when browsing a mark

---

## Hot Issues (10 most noteworthy)

1. **[#18435](https://github.com/anthropics/claude-code/issues/18435) — Multi-account profile switching in Claude Desktop**  
   *Enhancement, area:auth, area:ide* — 109 comments, 580 👍  
   The most-upvoted issue in the repo. Users managing multiple Claude teams want friction-free account switching within the desktop app. Community energy is high but Anthropic has yet to assign a milestone.

2. **[#11315](https://github.com/anthropics/claude-code/issues/11315) — Critical memory leak: 129GB RAM consumption**  
   *Bug, platform:linux, area:core, memory* — 64 comments, 52 👍  
   A severe memory leak that exhausted 16GB of system RAM and froze the machine. Still open after 7 months, suggesting the root cause (possibly in the Bash tool's temp-filesystem handling) is deeply systemic.

3. **[#62466](https://github.com/anthropics/claude-code/issues/62466) — "Image couldn't be processed" errors burning API usage limits**  
   *Bug* — 23 comments, 17 👍  
   Repeated image-processing failures that still consume per-request billing. High urgency for users relying on multimodal workflows.

4. **[#26996](https://github.com/anthropics/claude-code/issues/26996) — Edit tool silently converts tabs to spaces**  
   *Bug* — 15 comments, 27 👍  
   A subtle but vexing issue: the Edit tool normalizes indentation, causing pattern-match failures on tab-indented files (Go, Makefile, Python). Silent corruption of developer intent.

5. **[#12513](https://github.com/anthropics/claude-code/issues/12513) — Auto worktree creation cannot be disabled**  
   *Bug/enhancement, platform:macos* — 46 comments, 79 👍  
   Solo developers want to opt out of automatic Git worktree creation. Now closed, but the high engagement signals a persistent UX gap for non-team workflows.

6. **[#50674](https://github.com/anthropics/claude-code/issues/50674) — Cowork fails on ARM64 Windows (Snapdragon X)**  
   *Bug, platform:windows* — 19 comments  
   Cowork mode fails readiness checks on Qualcomm Snapdragon X processors despite passing pre-checks. A growing concern as ARM Windows devices proliferate.

7. **[#46767](https://github.com/anthropics/claude-code/issues/46767) — Tool results silently dropped on Windows (regression in v2.1.101)**  
   *Bug, platform:windows, regression* — 10 comments, 5 👍  
   "Missing due to internal error" across all tools on Windows. A regression that erodes trust in tool outputs — still open after two months.

8. **[#63909](https://github.com/anthropics/claude-code/issues/63909) — ENOSPC on temp filesystem despite free disk space**  
   *Bug, platform:macos, area:bash* — 8 comments, 16 👍  
   The Bash tool's temp-filesystem at `/private/tmp/claude-...` reports no space for subprocess output. Likely related to the deeper memory/fs issues in #11315.

9. **[#29910](https://github.com/anthropics/claude-code/issues/29910) — Built-in secrets management**  
   *Enhancement, area:tui, area:security* — 10 comments, 30 👍  
   Users want native secret-injection rather than hand-rolling environment-variable gymnastics. Growing interest as Claude Code is used in production CI/CD pipelines.

10. **[#49933](https://github.com/anthropics/claude-code/issues/49933) — Native WSL remote integration for Windows Desktop**  
    *Enhancement, platform:windows/wsl* — 9 comments, 55 👍  
    Strong demand (+55) for the Windows desktop app to connect directly to WSL file systems and interpreters, mirroring VS Code's WSL Remote experience.

---

## Key PR Progress (10 important pull requests)

1. **[#66416](https://github.com/anthropics/claude-code/pull/66416) — fix(plugin-dev): validator scripts abort on first finding due to `set -e`**  
   Three validator scripts in `plugin-dev` prematurely abort at the first error because `set -euo pipefail` causes grep/sed failures to exit the process. A straightforward correctness fix for the plugin development SDK.

2. **[#65875](https://github.com/anthropics/claude-code/pull/65875) — fix: Forward `ANTHROPIC_BASE_URL` to agentic_review child process**  
   Proxy/gateway users (LiteLLM, Bifrost) lost the custom base URL when spawning sub-processes for agentic code review. Essential for enterprise deployments behind API gateways.

3. **[#65916](https://github.com/anthropics/claude-code/pull/65916) — docs(mcp-integration): clarify allowed-tools vs agent tools enforcement**  
   Critical documentation fix: distinguishes between `allowed-tools` (auto-approval only) and `tools:` in subagent frontmatter (hard capability boundary). Clears up a common source of MCP integration confusion.

4. **[#63686](https://github.com/anthropics/claude-code/pull/63686) — Bump stale and autoclose timeouts from 14 to 90 days**  
   Proposes tripling the stale-bot timeout to reduce premature closure of legitimate issues. A direct response to community frustration with the current aggressive 14-day window.

5. **[#65314](https://github.com/anthropics/claude-code/pull/65314) — scripts: add detect-theme-color-issues to cluster light-theme color bugs**  
   A triage automation that groups "invisible text on light terminal themes" issues (a recurring family of bugs) into a single tracked parent. Smart community-led QoL improvement.

6. **[#67084](https://github.com/anthropics/claude-code/pull/67084) — [codex] fix Hookify prompt fields and warning context**  
   Maps legacy prompt+pattern rules to the current `UserPromptSubmit` payload, adds backward-compatible alias, and enriches hook warning responses with additional context.

7. **[#64607](https://github.com/anthropics/claude-code/pull/64607) — fix: Plugin `.mcp.json` example incorrectly uses `mcpServers` wrapper**  
   The `.mcp.json` documentation was using a flat `mcpServers` wrapper when the actual format expects a flat JSON object. A correction that saves plugin authors debugging time.

8. **[#65286](https://github.com/anthropics/claude-code/pull/65286) — fix(plugins): add missing plugin.json manifest for plugin-dev**  
   The plugin-dev plugin itself was missing its own manifest, making it undiscoverable through normal plugin installation mechanisms. Dogfooding gap closed.

9. **[#66572](https://github.com/anthropics/claude-code/pull/66572) — [WIP] Fix for "Image couldn't be processed" errors**  
   Work-in-progress fix for #62466. Early stage, but signals that the image-processing billing bug is being actively investigated.

10. **[#66372](https://github.com/anthropics/claude-code/pull/66372) — fix(devcontainer): detect Docker daemon failures via `$LASTEXITCODE`**  
    PowerShell's `try/catch` doesn't trap native command non-zero exits, so the devcontainer script falsely reports Docker as healthy. Pulls in the correct `$LASTEXITCODE` check.

---

## Feature Request Trends

Three dominant themes emerged from the open issues:

1. **Account & workspace management (#18435, #49933)** — The community deeply wants multi-account switching in the desktop app and native WSL integration. Both are "quality of life" features that lower friction for users straddling personal/work identities or Windows/Linux boundaries.

2. **Secrets and security infrastructure (#29910, #54117)** — As Claude Code is pushed into CI/CD and production workflows, users ask for built-in secrets management and stronger adherence to project rules (CLAUDE.md compliance). The latter is particularly telling: users feel the model ignores defined process guardrails.

3. **Cowork parity with Claude Code (#60205)** — Cowork users want feature parity for project-scoped skills and rules that Claude Code already supports, indicating Cowork is being adopted for serious development but missing modular configuration capabilities.

---

## Developer Pain Points

The signal-to-noise ratio in recent issues reveals five recurrent pain points:

1. **Model rule non-compliance** — Multiple users (e.g., #49259, #54117, #65951, #46429) report that Claude Code consistently skips user-defined multi-step workflows, jumping directly to coding. The same user (ktimesk1776) has filed across three model versions (Opus 4.6, 4.7, 4.8) with no resolution.

2. **Windows ecosystem fragility** — A cluster of Windows-specific regressions (#46767 dropped tool results, #50674 ARM64 Cowork failures, #59802 Settings crash, #62086 deleted-directory recovery failure) suggests inadequate Windows testing in the release pipeline.

3. **Resource exhaustion without recovery** — The critical memory leak (#11315), temp-filesystem ENOSPC (#63909), and image-processing billing consumption (#62466) share a theme: the tool can silently eat resources (RAM, disk, API budget) with no user-visible error until it's too late.

4. **Plugin/extension developer friction** — Multiple PRs (#66416, #64607, #65286) fix documentation or manifest bugs in the plugin SDK itself. Community members are spending time on foundational fixes rather than building on top of a stable SDK.

5. **Accessibility regressions** — Issue #67289 (broken tmux scroll-back) and #66398 (missing cursor in agent attach) were filed within the last 24 hours, indicating that v2.1.172 may have introduced TUI regressions that harm power users who rely on terminal multiplexers.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-11

## Today's Highlights
Two new Rust alpha releases (v0.140.0-alpha.7 and v0.140.0-alpha.4) landed, signaling active CLI iteration. The community remains deeply concerned about aggressive token consumption in #14593 (604 comments, 265 reactions), while a wave of Windows crash-on-launch reports after the 26.608.1337 update (issues #27367, #27320, #27175) indicates a broad Windows regression. Internally, the team is investing heavily in cross-platform build reliability — six PRs from @anp-oai focus on ARM64, musl, and Bazel transition fixes.

---

## Releases
Two pre-release versions pushed in the last 24 hours:

- **[rust-v0.140.0-alpha.7](https://github.com/openai/codex/releases/rust-v0.140.0-alpha.7)** — No changelog beyond version bump.
- **[rust-v0.140.0-alpha.4](https://github.com/openai/codex/releases/rust-v0.140.0-alpha.4)** — No changelog beyond version bump.

---

## Hot Issues (10 selected)

1. **[#14593 — Burning tokens very fast](https://github.com/openai/codex/issues/14593)**  
   *604 comments, 265 👍*  
   The longest-running open issue. A Business tier user on VS Code reports the extension consuming tokens at an alarming rate. Massive community engagement suggests this is either a widespread UX/config issue or a genuine billing leak. OpenAI has not yet closed or assigned.

2. **[#26867 — GitHub PR review still uses deactivated workspace after migration](https://github.com/openai/codex/issues/26867)**  
   *13 comments, 7 👍*  
   After migrating from Business to Personal Pro, GitHub PR reviews fail with "workspace is deactivated." Auth/workspace state not being properly refreshed triggers a frustrating loop for users who changed plans.

3. **[#25463 — Desktop project threads disappear from UI while JSONL remains](https://github.com/openai/codex/issues/25463)**  
   *12 comments, 1 👍*  
   Local project conversations vanish from the sidebar and search, but raw session files persist on disk. A data-visibility bug that undermines trust in the Desktop app as a project hub.

4. **[#17642 — `gpt-5.3-codex-spark` model not supported with ChatGPT account](https://github.com/openai/codex/issues/17642)**  
   *12 comments, 0 👍*  
   CLI users on Pro plans hitting a 400 error when using the `spark` model — auth/model compatibility gap between ChatGPT accounts and CLI access.

5. **[#23198 — Codex Desktop on Windows extremely slow](https://github.com/openai/codex/issues/23198)**  
   *12 comments, 31 👍*  
   High community agreement that the Windows app is unusably slow even on capable hardware. Isolated to Codex, not the OS. High priority signal for Windows performance.

6. **[#13553 — Windows Store app fails for non-ASCII usernames](https://github.com/openai/codex/issues/13553)**  
   *11 comments, 9 👍*  
   First launch crashes for users with accented characters or CJK characters in their Windows username. A years-old unicode path bug still unresolved — a significant accessibility and i18n gap.

7. **[#24300 — Goal auto-continuations downgrade Full Access to read-only](https://github.com/openai/codex/issues/24300)**  
   *10 comments* (CLOSED)  
   Critical sandbox UX issue: auto-continuation turns silently lose Full Access permissions while UI still shows it. Closed recently, suggesting a fix is shipping.

8. **[#27175 — Desktop 26.602.71036 crashes after update on Windows](https://github.com/openai/codex/issues/27175)**  
   *8 comments, 2 👍*  
   Newest Windows crash report; app becomes inaccessible even with empty sessions. A `$200/mo Pro` user affected. Suggests a recent release broke startup on certain Win11 builds.

9. **[#27491 — Severe streaming slowdown in Fast mode](https://github.com/openai/codex/issues/27491)**  
   *6 comments*  
   macOS Tahoe + GPT-5.5 Fast mode outputs only a few characters every several seconds. Streaming performance regression — critical for user-perceived responsiveness.

10. **[#27296 — Fn global dictation hotkey stops working after update](https://github.com/openai/codex/issues/27296)**  
    *4 comments, 9 👍*  
    macOS update 26.608.12217 breaks the system-wide dictation hotkey. An unforced system conflict — Codex seems to be capturing or interfering with a native macOS shortcut.

---

## Key PR Progress (10 selected)

1. **[#27514 — Support realtime conversation prompt overrides](https://github.com/openai/codex/pull/27514)**  
   Enables `thread/realtime/start` callers to override start/end instructions, with local config taking precedence. Useful for custom agent behaviors.

2. **[#27488 — Add new context window tool](https://github.com/openai/codex/pull/27488)**  
   Gives the model a requestable way to start a fresh context window without compaction, maintaining full context through initial-context path.

3. **[#27440 — Fall back to manual approval when Guardian times out](https://github.com/openai/codex/pull/27440)**  
   Guardian auto-review timeouts no longer block commands — users get a manual approval prompt instead. Important UX safety net.

4. **[#27508/27509/27510 — TUI goal improvements (3-PR stack)](https://github.com/openai/codex/pull/27508)**  
   Three-chained PRs: long raw objectives, pasted text, and image support in TUI goals. Unblocks rich `/goal` workflows in terminal environments.

5. **[#27246 — Strip image detail from Responses Lite requests](https://github.com/openai/codex/pull/27246)**  
   Removes image `detail` fields from Lite request payloads when `resize_all_images` is enabled, reducing payload size without mutating stored history.

6. **[#27266 — Preserve ICC/EXIF metadata when resizing prompt images](https://github.com/openai/codex/pull/27266)**  
   Retains ICC profiles and EXIF orientation metadata during image resizing. Supports PNG, JPEG, WebP. Important for design/creative workflows.

7. **[#27459 — Gate plugin MCP servers by auth route](https://github.com/openai/codex/pull/27459)**  
   API-key users can now use high-value MCP plugins (Slack, GitHub, Google Drive) even without connected-app auth — enables broader plugin access.

8. **[#27326 — Build all release targets with Bazel transitions](https://github.com/openai/codex/pull/27326)**  
   Overhauls release build configuration to correctly set `v8_target_cpu` and satisfy remote-execution constraints for all six targets.

9. **[#27323 — ARM64 MinGW `powl` compatibility for Windows ARM](https://github.com/openai/codex/pull/27323)**  
   Patches LLVM MinGW to provide `powl` symbol, unblocking Windows ARM64 release builds. Cross-compilation enabler.

10. **[#27247 — Resize all history images behind feature flag](https://github.com/openai/codex/pull/27247)**  
    Centralizes client-side image preparation; covers user input, `view_image`, and structured outputs. Default-off, but architecture is now in place.

---

## Feature Request Trends

1. **Context-aware budget & compaction** — Multiple issues and PRs (#21777, #27488, #27438) push toward exposing context-window budget to the model and giving agents explicit compaction control.
2. **TUI goal enrichment** — The 3-PR stack (#27508–#27510) addresses a clear user desire for richer terminal-based goal definition (long text, images).
3. **Cross-platform build reliability** — Six PRs this week from @anp-oai target ARM64, musl, MinGW, and Bazel transition correctness. A sustained infrastructure push.
4. **Image metadata preservation** — Two PRs (#27246, #27266) indicate OpenAI is standardizing image handling across Lite and full-response paths, particularly for creative/design contexts.

---

## Developer Pain Points

- **Windows stability crisis** — Four open crash-on-launch issues (#27175, #27367, #27320, #25807) across multiple Windows versions. The 26.608.1337 update is clearly broken for many Windows users. High severity.
- **Token consumption alarm** — #14593 (604 comments) reflects deep community anxiety about billing transparency and runaway token usage.
- **Data visibility bugs** — Three separate issues (#25463, #20833, #22796) report local conversations disappearing from the UI while still existing on disk. Undermines confidence in Desktop as a reliable project tool.
- **Auth/workspace migration friction** — #26867 and #17642 highlight that account/workspace transitions (Business→Pro, ChatGPT→CLI) are not smooth, leaving users stuck with stale auth state.
- **Non-ASCII i18n gap** — Issue #13553 (non-ASCII Windows usernames) remains unfixed for over 3 months — a recurring accessibility complaint.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-11

## Today's Highlights
No new releases landed in the last 24 hours, but the repository saw significant activity around bug fixes and infrastructure hardening. A critical PR addresses the long-standing shell hang issue (#25166) where commands complete but the CLI remains stuck awaiting input. A large batch of dependency updates (17 PRs) was merged, bumping core libraries including Zod to v4.4.3, Vitest to v4.1.8, and `cli-spinners` to v3.4.0. Memory system bugs and subagent reliability remain the most active discussion areas.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#21409 – Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, Bug, 7 comments, 👍8)  
   The generalist agent hangs indefinitely on simple tasks like folder creation. Workaround: instructing the model not to defer to sub-agents. This has been open since March and is the highest-voted open bug, indicating a significant user-impacting reliability gap.

2. **[#22323 – Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, Bug, 6 comments, 👍2)  
   The `codebase_investigator` subagent falsely reports success after hitting max turns, masking real interruptions. This erodes trust in agent status reporting and could lead users to believe tasks completed when they didn't.

3. **[#22745 – AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (P2, Feature Investigation, 7 comments, 👍1)  
   An epic investigating whether AST-aware tools can reduce token usage and improve precision in codebase navigation. If successful, this could meaningfully reduce costs and increase accuracy for large-repo workflows.

4. **[#21968 – Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, Bug, 6 comments)  
   Custom skills and sub-agents are underused unless explicitly instructed. This undermines the value of the skill system, a core differentiator for agentic coding tools.

5. **[#25166 – Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, Bug, 4 comments, 👍3)  
   Commands that complete successfully still show "Awaiting user input," blocking further work. Now being addressed by an open PR (#27842). High user frustration reported.

6. **[#26525 – Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, Bug, Security, 5 comments)  
   Auto Memory sends transcripts to model context before redacting secrets. This is a privacy/security concern, especially for enterprise users handling sensitive codebases.

7. **[#26522 – Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, Bug, 5 comments)  
   Auto Memory retries sessions indefinitely if the extraction agent decides not to read them. This wastes API quota and creates stale entries. Part of a broader memory system cleanup tracked in #26516.

8. **[#24246 – 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2, Bug, 3 comments)  
   Enabling too many tools causes a 400 error. Users expect smarter tool pruning. This limits extensibility for power users with rich tool configurations.

9. **[#21983 – Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, Bug, 4 comments, 👍1)  
   The browser subagent crashes on Wayland display servers, which are default on many modern Linux distributions. Affects a growing segment of Linux users.

10. **[#22672 – Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, Customer Issue, 2 comments)  
    Agents occasionally use destructive git commands (`reset`, `--force`) when safer alternatives exist. This is critical for production environments where accidental data loss is unacceptable.

## Key PR Progress

1. **[#27842 – Fix: never let shell exit results hang on output drain](https://github.com/google-gemini/gemini-cli/pull/27842)** (Size: L, Open)  
   Directly addresses the high-impact shell hang bug (#25166). Adds error handling and bounding to the PTY output processing chain. By author MartinCajiao, created today.

2. **[#27767 – Fix: prevent path traversal during skill install](https://github.com/google-gemini/gemini-cli/pull/27767)** (Size: M, Open)  
   Mitigates three path traversal vulnerabilities in `installSkill`, `linkSkill`, and `uninstallSkill`. Important for supply chain security when installing community skills.

3. **[#27753 – CI: validate workflow_run origin to fix artifact poisoning](https://github.com/google-gemini/gemini-cli/pull/27753)** (Size: S, Open)  
   Security hardening: prevents fork PRs from poisoning CI artifacts and running attacker-controlled code with repository secrets.

4. **[#27839 – Fix: make read_background_output delay abort-aware](https://github.com/google-gemini/gemini-cli/pull/27839)** (Size: S, Open)  
   Fixes a UI bug where pressing ESC to cancel background output didn't stop the spinner, and new prompts were incorrectly queued.

5. **[#27698 – Fix: ensure zero-quota limits fail fast to prevent retry loop](https://github.com/google-gemini/gemini-cli/pull/27698)** (Size: M, Open)  
   Stops a 10-attempt retry loop when hitting a hard quota of zero (e.g., unbilled free-tier accounts). Important for new users.

6. **[#27835 – chore: bump ink-gradient 3.0.0 → 4.0.1](https://github.com/google-gemini/gemini-cli/pull/27835)** (Size: S, Closed)  
   Part of the large dependency update batch. Ink-gradient is used for terminal UI rendering.

7. **[#27827 – chore: bump Zod 3.25.76 → 4.4.3](https://github.com/google-gemini/gemini-cli/pull/27827)** (Size: M, Closed)  
   Major version bump for the schema validation library. May introduce breaking changes to tool definitions.

8. **[#27824 – chore: bump Vitest 3.2.4 → 4.1.8](https://github.com/google-gemini/gemini-cli/pull/27824)** (Size: XL, Closed)  
   Significant test framework upgrade. Largest dependency PR in today's batch.

9. **[#27826 – chore: bump https-proxy-agent 7.0.6 → 9.0.0](https://github.com/google-gemini/gemini-cli/pull/27826)** (Size: S, Closed)  
   Security-related proxy agent update.

10. **[#27833 – chore: bump comment-json 4.2.5 → 5.0.0](https://github.com/google-gemini/gemini-cli/pull/27833)** (Size: S, Closed)  
    JSON parser used for configuration files. Major version bump may affect settings parsing.

## Feature Request Trends

1. **AST-aware Code Navigation** – Multiple issues (#22745, #22746, #22747) propose using AST-based tools for file reads, searches, and codebase mapping to reduce token usage and improve precision.

2. **Agent Self-Awareness** – #21432 requests that Gemini CLI understand its own flags, hotkeys, and capabilities well enough to act as its own guide, suggesting a meta-agent layer.

3. **Background & Remote Agents** – #22741 requests that local sub-agents be backgroundable (Ctrl+B), and #20303 tracks advanced auth and background operations for remote agents. This points to a desire for non-blocking, long-running agent workflows.

4. **Memory System Enhancements** – Issues #26516, #26522, #26523, #26525 show strong interest in more robust, secure, and efficient memory management, including deterministic redaction and quarantine of invalid patches.

5. **Browser Agent Resilience** – #22232 and #22267 request persistent session takeover, lock recovery, and proper settings.json override support for the browser subagent, indicating reliability is a top concern.

## Developer Pain Points

1. **Agent Hangs and False Successes** – The combination of #21409 (generalist hangs), #22323 (false success reports), and #25166 (stuck shell) represents the #1 category of frustration: agents that silently fail or never complete.

2. **Subagent Configuration Surprises** – #21968 (agents don't use skills enough) and #22093 (subagents running without permission) show that subagent behavior is unpredictable and hard to control.

3. **Security and Privacy Gaps** – #26525 (unredacted secrets in memory), #27767 (path traversal in skill install), and #27753 (CI artifact poisoning) reveal multiple security holes that could deter enterprise adoption.

4. **Resource Leaks and Waste** – #26522 (indefinite retries of low-signal sessions) and #24246 (400 error with too many tools) point to inefficient resource management that costs users time and API credits.

5. **Display and Environment Incompatibility** – #21983 (Wayland failure), #24935 (terminal corruption after external editors), and #21924 (flicker on resize) show that terminal rendering quality across different environments remains a persistent issue.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-11

## Today’s Highlights
The community remains vocal about a **long-standing model availability gap** between Copilot CLI and VS Code, with users reporting that org-enabled models like Gemini 3.1 Pro are missing from the CLI. A **new wave of terminal rendering bugs** surfaced this week, including stream corruption with duplicated/truncated characters and a broken copy-to-clipboard on Linux. Additionally, **MCP policy enforcement continues to frustrate** personal and enterprise users alike, with reports of third-party MCP servers being blocked even when no such policy exists.

---

## Releases
**No new releases in the last 24 hours.** The latest version remains v1.0.60 (published 2026-06-05).

---

## Hot Issues (10 noteworthy)

### 1. [OPEN] [area:models] Copilot CLI does not list all org-enabled models (e.g. Gemini 3.1 Pro) while VS Code Copilot does
- **Issue #1703** — Closed, but the community is *still* feeling the pain. This is the top-voted issue cluster (75+ reactions combined). Models enabled at the org level in Copilot settings are missing from the CLI’s `/model` list.
- **Why it matters:** CLI users are second-class citizens for model access. This blocks teams standardized on Gemini 3.1 Pro from using the CLI.
- **Community reaction:** Repeated re-open requests and workarounds like `shell-ai` are emerging.

### 2. [OPEN] [area:permissions, area:enterprise] "Copilot Requests" permission for fine-grained tokens should be visible for org-owned tokens
- **Issue #223** — 76 👍, 29 comments. Enterprise admins cannot create org-owned fine-grained tokens with the `Copilot Requests` permission, forcing use of individual PATs.
- **Why it matters:** Security-sensitive orgs need to enforce token ownership without resorting to workarounds.

### 3. [OPEN] [area:input-keyboard] ctrl+shift+c no longer copies to clipboard on Linux (Ubuntu 24.04)
- **Issue #2082** — 21 comments, 8 👍. A fundamental terminal UX regression since v1.0.4.
- **Why it matters:** Linux power users rely heavily on this shortcut. The `ctrl+c` workaround conflicts with interrupt signals.

### 4. [CLOSED] [area:mcp] Third-party MCP servers are disabled, despite no such policy
- **Issue #1707** — 9 comments. Users report 3rd-party MCP servers blocked by a "policy" that does not exist in their org settings. Downgrading to 0.0.417 restores access.
- **Today’s mirror:** **#3756** (opened today) confirms the bug persists on v1.0.59.

### 5. [OPEN] [area:terminal-rendering] BUG: Terminal streaming renderer corrupts output - characters doubled/truncated
- **Issue #3749** (new) — 2 comments, filed 2026-06-10. Streaming output shows duplicated words and truncated tokens.
- **Why it matters:** Pervasive display corruption makes the CLI unusable for reading live reasoning. Companion issue **#3755** reports the same for the thinking display.

### 6. [CLOSED] [area:models] Restore support for Gemini Pro (gemini-3-pro-preview)
- **Issue #2434** — 10 👍, 7 comments. v1.0.14 dropped a popular model with no migration path.
- **Community reaction:** Users chose Copilot CLI *for* model variety. This move pushes users toward Claude Code or Codex.

### 7. [OPEN] [area:authentication, area:sessions] Error loading model list: “Not authenticated” when resuming a session
- **Issue #3596** — 10 👍, 5 comments. Resuming sessions loses authentication state; `/model` command fails. Fresh sessions work fine.
- **Why it matters:** Session resumption is a core workflow. Breaking it erodes trust.

### 8. [OPEN] [area:context-memory, area:plugins] Regression in v1.0.60: userPromptSubmitted hook additionalContext no longer injected
- **Issue #3727** — Filed 2026-06-09, 3 comments. Plugin developers lost the ability to inject context in the latest release.
- **Why it matters:** The CLI’s extensibility promise is broken for anyone building custom plugins.

### 9. [CLOSED] [area:agents, area:models] Background sub-agent silently hangs at total_turns=0 when model="gpt-5.5"
- **Issue #3547** — 7 comments. Sub-agent dispatches succeed but never progress — no error, no timeout, just zero turns forever.
- **Why it matters:** Multi-agent workflows are a key differentiator. This makes background agents unreliable.

### 10. [OPEN] [area:terminal-rendering] Copy to clipboard silently fails on Windows
- **Issue #3622** — 2 👍, 3 comments. Copy operations appear to succeed but paste yields old clipboard content. Regressed between v1.0.48 and v1.0.60.
- **Why it matters:** A silent failure is worse than an error — users lose data without warning.

---

## Key PR Progress

**No pull requests were merged or updated in the last 24 hours.** This is consistent with a quiet period after the v1.0.60 release. The community is primarily reporting bugs rather than contributing patches at this time.

---

## Feature Request Trends

1. **Model parity with VS Code** — The single highest-voted request cluster. Users demand that all models available in VS Code Copilot (especially **Gemini 3.1 Pro**, **Gemini 3 Flash**) be available in CLI without manual configuration.

2. **Enterprise token management** — Org-owned fine-grained tokens need full `Copilot Requests` permission visibility (#223). Enterprises want to stop using individual PATs in automations.

3. **MCP server control** — Power users want a tab-completable shortcut syntax for invoking specific MCP tools (#3752). Enterprise users want policy-enforced MCP blocking to either work correctly or be removable.

4. **Terminal UX improvements** — Users explicitly request bringing back `no-alt-screen` mode (#2334) for scrollback and history access. The forced alt-screen approach is widely criticized.

5. **Custom provider support in ACP mode** — Environment variables like `COPILOT_PROVIDER_BASE_URL` should work in `--acp` mode, not just interactive mode (#3048).

---

## Developer Pain Points

- **Model inconsistency between CLI and IDE** — The #1 frustration: users on the *same org, same account* see different model lists. This is forcing teams to evaluate alternatives like `shell-ai` and Claude Code.
- **Regressions with every release** — v1.0.60 introduced at least two regressions (plugin hook injection, MCP server spawning loop, clipboard silent failure). Users express frustration at having to downgrade frequently.
- **Terminal rendering quality degradation** — Streaming corruption, broken copy shortcuts, and lost BEL notifications indicate the terminal renderer is not getting enough QA attention.
- **Authentication fragility in sessions** — Resuming a session losing auth state (#3596) is a basic reliability issue that undermines the “always-on” workflow promise.
- **MCP policy enforcement bugs** — Personal and enterprise users are both affected by the “blocked by policy” false positive. The lack of a clear off-switch or error message is pushing users to hack around the system.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date:** 2026-06-11

---

## 1. Today's Highlights

The Kimi Code CLI community saw a surge of merged stability fixes from the past month now landing, with 23 PRs updated in the last 24 hours—all but three already closed. Two new bugs surfaced in v0.12.0, both reported by the same user: YOLO mode is prompting for approval unexpectedly, and the agent gets stuck on the final to-do item, never marking it complete. Meanwhile, the backlog is clearing rapidly as a wave of Windows-specific fixes (console font resets, file encoding, subprocess management) have been merged and documented.

## 2. Releases

No new releases in the last 24 hours. The latest stable version remains **Kimi Code v0.12.0**.

---

## 3. Hot Issues

| # | Issue | Why It Matters |
|---|-------|----------------|
| [#2448](https://github.com/MoonshotAI/kimi-cli/issues/2448) | **[bug] Kimi CLI is prompting for approval in yolo mode** | YOLO mode is supposed to be fully autonomous; any approval prompt breaks the core value proposition. Reported on v0.12.0 with k2.6 model. |
| [#2447](https://github.com/MoonshotAI/kimi-cli/issues/2447) | **[bug] Final Todo item never completes** | Agents hang on the last task, failing to close the loop. This disrupts multi-step workflows and wastes compute. |
| [#2233](https://github.com/MoonshotAI/kimi-cli/issues/2233) | **[bug] OpenAI legacy requests fail with empty `tools` array** | vLLM and other OpenAI-compatible backends reject `tools: []`; fixed in #2235. Affects `/compact` and no-tool calls. |
| [#2343](https://github.com/MoonshotAI/kimi-cli/issues/2343) | **[bug] Deferred MCP startup failures abort interactive turn** | MCP server init failures should not crash the whole session; fixed in #2355. Critical for multi-server setups. |
| [#2272](https://github.com/MoonshotAI/kimi-cli/issues/2272) | **[bug] Bash install script fails to find uv after install** | Installation reliability issue; uv binary not in PATH after script completes. Fixed in #2283. |
| [#2197](https://github.com/MoonshotAI/kimi-cli/issues/2197) | **[bug] Windows console font resets when running CLI** | Cosmetic but annoying; causes console appearance changes on subprocess spawn. Fixed in #2289 and #2199. |
| [#2165](https://github.com/MoonshotAI/kimi-cli/issues/2165) | **[bug] Malformed historical tool calls break session replay** | Invalid JSON in tool call arguments causes repeated failures on every turn. Fixed in #2196. |
| [#2310](https://github.com/MoonshotAI/kimi-cli/issues/2310) | **[bug] Shell process trees not terminated on timeout** | Orphaned processes left running after timeout/cancellation. Fixed in #2327. |
| [#2222](https://github.com/MoonshotAI/kimi-cli/issues/2222) | **[bug] `--continue` fails with stale session metadata** | Resume breaks when last_session_id is stale or missing. Fixed in #2239. |
| [#1974](https://github.com/MoonshotAI/kimi-cli/issues/1974) | **[bug] `/undo` mapping broken for slash-command turns** | Wire turn index mismatch with context turns, causing incorrect undo behavior. PR #2386 open. |

*Community reaction*: No comments or reactions on new issues yet, indicating early in the bug life cycle. The reporter (iaindooley) is providing detailed reproduction steps.

---

## 4. Key PR Progress

| PR | Status | Summary |
|----|--------|---------|
| [#2387](https://github.com/MoonshotAI/kimi-cli/pull/2387) | **OPEN** | Fixes shell command headline truncation—stops clipping useful command context in `Used Shell (...)` display. |
| [#2386](https://github.com/MoonshotAI/kimi-cli/pull/2386) | **OPEN** | Maps `/undo` wire turns correctly to context turns, fixing incorrect undos after slash commands. |
| [#2383](https://github.com/MoonshotAI/kimi-cli/pull/2383) | **OPEN** | Repairs orphaned `tool_calls` from mid-turn kills (OOM, kill -9) that corrupt `context.jsonl`. |
| [#2355](https://github.com/MoonshotAI/kimi-cli/pull/2355) | **MERGED** | MCP startup failures no longer abort the interactive turn; logs and continues gracefully. |
| [#2354](https://github.com/MoonshotAI/kimi-cli/pull/2354) | **MERGED** | Windows: per-process log files to avoid concurrent CLI/Web/worker log rotation conflicts. |
| [#2334](https://github.com/MoonshotAI/kimi-cli/pull/2334) | **MERGED** | Sanitizes lone UTF-16 surrogates before Kimi API requests; fixes serialization crashes. |
| [#2327](https://github.com/MoonshotAI/kimi-cli/pull/2327) | **MERGED** | Shell subprocesses run in process groups; entire tree killed on timeout/cancellation. |
| [#2289](https://github.com/MoonshotAI/kimi-cli/pull/2289) | **MERGED** | Windows: uses `CREATE_NO_WINDOW` flag to prevent console font resets during subprocess spawn. |
| [#2239](https://github.com/MoonshotAI/kimi-cli/pull/2239) | **MERGED** | `--continue` falls back to newest non-empty session when metadata is stale or missing. |
| [#2217](https://github.com/MoonshotAI/kimi-cli/pull/2217) | **MERGED** | Background auto-trigger pauses for 10 minutes after 3 consecutive failures, then auto-recovers. |

---

## 5. Feature Request Trends

Based on all open issues (including those not shown in brief), the most-requested feature directions are:

1. **Autonomous Agent Stability**—YOLO mode should be truly headless with no approval prompts (#2448); agents must reliably complete all tasks including the final one (#2447).
2. **Session Resilience**—Better handling of mid-turn crashes (OOM, terminal close) to avoid corrupted `context.jsonl` and orphaned tool calls (#2383, #2336).
3. **Cross-Platform Parity**—Closing the gap between Linux/macOS and Windows functionality: console behaviors, file encoding (GBK vs UTF-8), subprocess management (#2354, #2289, #2199, #1893).
4. **Web Interface Improvements**—Archived session navigation (#2333), AFK mode propagation to workers (#2211), and graceful error handling for Web workers.
5. **Multi-Backend Compatibility**—Proper handling of OpenAI-compatible API quirks, especially empty tool arrays and malformed JSON in history (#2233, #2165).

---

## 6. Developer Pain Points

The following recurring frustrations emerge from recent issue reports and discussions:

1. **YOLO mode approval prompts**—The most critical pain point. Developers using headless/scripted workflows hit unexpected approval gates, defeating the purpose of fully autonomous operation.
2. **Session corruption on crash**—Mid-turn failures (OOM, `kill -9`) produce unusable session files that cannot be replayed or undone, often forcing full session restarts.
3. **Windows as a second-class platform**—Disproportionate number of Windows-specific bugs: console font resets, GBK encoding conflicts with UTF-8 git output, concurrent log rotation failures, missing `CREATE_NO_WINDOW` flags.
4. **MCP server brittleness**—A single failing MCP server can abort an entire interactive session, punishing users who want multi-server tool configurations.
5. **Shell orphan processes**—Timeouts or cancellations of shell commands leave background processes running, wasting system resources.
6. **Undo/fork confusion**—The `/undo` and fork mechanisms behave unpredictably when slash commands or non-user messages are involved, causing trust erosion in session history management.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-11

## Today's Highlights

Three patch releases (*v1.17.1–v1.17.3*) shipped to fix regressions introduced in v1.17.0, including a critical desktop crash and Linux launcher breakage. The community is actively discussing image paste support (#906, 36 comments), and a new `/goal` command PR (#31762) signals growing interest in autonomous task loops. Performance regressions and provider-specific caching issues continue to dominate the bug tracker.

## Releases

**[v1.17.3](https://github.com/anomalyco/opencode/releases/tag/v1.17.3)** — Hotfix for a desktop crash in v1.17.2.

**[v1.17.2](https://github.com/anomalyco/opencode/releases/tag/v1.17.2)**  
- **Core**: Recover from expired remote config auth by re-prompting login (@Ayushlm10); restored subagent permission isolation.  
- **Desktop**: Restored Linux launcher/icon identity so pinned apps correctly open `co` scheme.

**[v1.17.1](https://github.com/anomalyco/opencode/releases/tag/v1.17.1)**  
- References can now include usage descriptions for agents and be hidden from `@` autocomplete.  
- Deprecated `reference` config key entries now load under `references`.  
- MCP prompt/resource fixes.

**[v1.17.0](https://github.com/anomalyco/opencode/releases/tag/v1.17.0)**  
- Faster file search via new `fff`-backed tools (@dmtrKovalenko).  
- `X-Session-Id` headers for proxy sticky routing (@songchaow).  
- Cohere North model support.  
- `reasoning` as an interleaved field option for chat.

## Hot Issues

| # | Title | Why It Matters & Community Sentiment |
|---|-------|--------------------------------------|
| [#906](https://github.com/anomalyco/opencode/issues/906) | Paste to attach image | 36 comments, 22 👍. Longest-running UX request: drag-and-drop only, clipboard paste feels like table stakes for LLM workflows. |
| [#14273](https://github.com/anomalyco/opencode/issues/14273) | Free usage exceeded with Zen free models | 27 comments. Users with positive Zen balances still blocked by "free usage exceeded" on Kimi/MiniMax free tiers. Closed but contentious. |
| [#6330](https://github.com/anomalyco/opencode/issues/6330) | Generic UI Intent Channel | 17 comments. Ambitions cross-client plugin UX; server/plugin-driven UI events. |
| [#25038](https://github.com/anomalyco/opencode/issues/25038) | Long-running shell commands hang after success | 11 comments. Gradle/Android devs hit hard—process completion not detected, blocking workflows. |
| [#26762](https://github.com/anomalyco/opencode/issues/26762) | Cerebras zai-glm-4.7 fails on follow-up turns | 10 comments. `reasoning_content` unsupported on multi-turn; vendor-specific regression. |
| [#6490](https://github.com/anomalyco/opencode/issues/6490) | Web UI cannot browse folders outside user profile | 10 comments, 12 👍. Windows users stuck with `C:\Users\…` only; drives devs away from web client. |
| [#30086](https://github.com/anomalyco/opencode/issues/30086) | High CPU usage in newer versions | 9 comments. Regression causing 10→3 session limit; mouse lag reported. |
| [#31247](https://github.com/anomalyco/opencode/issues/31247) | Opus 4.8 via Copilot leaks tool-call text | 8 comments. Literal `<invoke …>` markup leaks into assistant messages; noisy and persistent. |
| [#26602](https://github.com/anomalyco/opencode/issues/26602) | Desktop hits 5-minute header timeout with local providers | 8 comments. `timeout: false` ignored; local Ollama/LM Studio users blocked on long context. |
| [#24610](https://github.com/anomalyco/opencode/issues/24610) | DeepSeek-V4 "disable thinking" button | 4 comments, 5 👍. Multiple duplicates (#27555); users want toggle for translation tasks. |

## Key PR Progress

| # | Title | What It Does |
|---|-------|--------------|
| [#31817](https://github.com/anomalyco/opencode/pull/31817) | fix(core): add compaction key to isV1 detection | Fixes silent drop of `preserve_recent_tokens` when config only has compaction fields. |
| [#31329](https://github.com/anomalyco/opencode/pull/31329) | fix(opencode): graceful error for PDF/image read failures | Prevents session crash on corrupted PDFs/permission errors. |
| [#31814](https://github.com/anomalyco/opencode/pull/31814) | fix(opencode): retry on xfyun engine busy response | Adds `engine busi` to retryable error list—critical for 讯飞 users. |
| [#31809](https://github.com/anomalyco/opencode/pull/31809) | fix(tool): correct misleading Read prerequisite | Stops tool descriptions falsely claiming Write fails without prior Read. |
| [#31808](https://github.com/anomalyco/opencode/pull/31808) | fix(util): handle URIError in decodeDataUrl | Fixes crash on non-encoded `%` in data URLs (e.g., `100%off`). |
| [#31806](https://github.com/anomalyco/opencode/pull/31806) | fix(tool): remove undocumented +100ms from shell timeout | Shell timeout is now exactly what user specifies, no hidden offset. |
| [#31745](https://github.com/anomalyco/opencode/pull/31745) | fix(opencode): surface content-filter finish reason | Converts silent Anthropic refusals to visible errors. |
| [#29217](https://github.com/anomalyco/opencode/pull/29217) | feat(tui): add inline `$skill` invocations with SKILL pill | New prompt composer: type `$` to autocomplete skills—closes 5 issues. |
| [#31798](https://github.com/anomalyco/opencode/pull/31798) | fix(snapshot): reuse source git objects | Avoids re-hashing 500k-file repos (e.g., Chromium) on session open. |
| [#31811](https://github.com/anomalyco/opencode/pull/31811) | test(opencode): simplify share layer wiring | Replaces manual LayerNode provisioning with cleaner graph wiring for tests. |

## Feature Request Trends

1. **Paste-to-Attach for Images** — #906 (22 👍) and #31791 show strong demand: users want clipboard paste and drag-and-drop for images in both chat and `question` tool UI. Excalidraw → PNG → LLM is a common workflow.

2. **Reasoning/Thinking Toggle** — #24610, #27555, #450 (38 👍 cumulative). DeepSeek V4 Flash thinking enabled by default; users want a UI button to disable for translation/simple tasks. `reasoning_effort` parameter support also requested.

3. **Autonomous Task Completion** — #31762 (`/goal` command), #30658 (plan updates). Community wants persistent goal-driven loops (inspired by Claude Code `/goal`, Codex Goal Mode) with session tracking.

4. **Cross-Client Plugin UX** — #6330 (8 👍). Generic UI Intent Channel for servers/plugins to emit custom UI events—ambitious but high-impact.

5. **Model/Session Config Flexibility** — #31750 (ACP per-session model selection), #5245 (OpenTelemetry), #7625 (base path). Growing need for configuration control per-session rather than only at startup.

## Developer Pain Points

- **Performance regressions** — #30086 (CPU spike), #16438 (16 GB snapshot file), #31747 (fff scan timeout on OneDrive). Recent `fff`-backed file search in v1.17.0 has improved speed for large repos but introduced startup hangs on cloud-synced directories.
- **Provider timeout/resilience** — #26602 (5-min hard timeout for local providers), #31772 (errors silently swallowed by `Effect.orDie`), #31774 (V1 shell lacks destructive command protection). Developers using local LLMs or long-running builds face silent failures.
- **Desktop/Web UX gaps** — #6490 (no folder browsing outside user profile), #28312 (stale TUI permission dialogs), #31804 (file tree cache not clearing deleted folders).
- **Account & billing friction** — #14273 (Zen free tier bugs), #18016 (no account deletion path). Trust issue for paid users.
- **Tool markup leaks** — #31247 (Opus 4.8 leaks raw `<invoke …>` text), #31766 (LM Studio double `/v1` path). Quality-of-life bugs that erode model output trust.

*Data source: github.com/anomalyco/opencode — snapshotted 2026-06-11 23:59 UTC*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-11

**Data Source:** github.com/badlogic/pi-mono

---

## Today’s Highlights

A significant wave of bug fixes landed today, addressing critical TUI crashes, Anthropic stream finalization issues, and provider compatibility gaps. Notably, the team is actively shipping provider support for Palantir Foundry and Amazon Bedrock Mantle, while the community continues to surface pain around subscription login flows, model-switching stability, and local LLM timeout handling.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#5514 — Project Trust Feature Feedback](https://github.com/earendil-works/pi/issues/5514)** (CLOSED, 25 comments)  
   The new trust-gating feature immediately drew community ire. Users dislike being asked to trust folders on every machine, even with known projects. 13 👍 indicate widespread frustration. *Why it matters:* Trust UX can make or break adoption for power users who manage many repos.

2. **[#3715 — `local-llm` streams terminate at 5-min default timeout](https://github.com/earendil-works/pi/issues/3715)** (CLOSED, 10 comments)  
   Long tool calls against vLLM/Qwen3 die with `UND_ERR_BODY_TIMEOUT`. The `retry.provider.timeoutMs` setting doesn't override the underlying undici default. *Why it matters:* Blocks local LLM users running long-thinking chains.

3. **[#5536 — Split-turn compaction causes 429 on single-concurrency backends](https://github.com/earendil-works/pi/issues/5536)** (OPEN, 2 comments)  
   Auto-compaction fires two summarization requests in parallel, hitting `429 Too Many Requests` on single-slot `llama.cpp`. *Why it matters:* Critical for local-first users; a serialization fix is needed.

4. **[#5291 — Sessions hang on "Working" with Anthropic Enterprise](https://github.com/earendil-works/pi/issues/5291)** (CLOSED, 5 comments)  
   Intermittent session freezes, all at once. Interrupt/stop sometimes works. *Why it matters:* Enterprise subscribers are experiencing unreliability at scale.

5. **[#5601 — GHC login fails with unhelpful error](https://github.com/earendil-works/pi/issues/5601)** (CLOSED, 3 comments)  
   Login to GitHub Copilot subscription fails with a generic error. *Why it matters:* First-run friction for new users on Windows/WSL.

6. **[#5598 — Android Termux multiline paste auto-submits](https://github.com/earendil-works/pi/issues/5598)** (CLOSED, 1 comment)  
   Pasting multiline code in Termux auto-submits before pasting finishes. Works fine via SSH. *Why it matters:* Mobile/Termux users are a growing population; this breaks REPL-style workflows.

7. **[#5599 — `getTextOutput` crashes on undefined content](https://github.com/earendil-works/pi/issues/5599)** (CLOSED, 1 comment)  
   Uncaught `TypeError` in `render-utils.js` kills the process. *Why it matters:* A null-safety gap that causes hard crashes for users with missing tool results.

8. **[#5597 — `Box.render` crashes on undefined child component](https://github.com/earendil-works/pi/issues/5597)** (CLOSED, 1 comment)  
   Async render cycles returning `undefined` in `callRenderer`/`resultRenderer` cause fatal TUI crashes. *Why it matters:* Top crash candidate for extension developers.

9. **[#5603 — Cost underreporting: 1-hour cache writes priced at 5-min rate](https://github.com/earendil-works/pi/issues/5603)** (CLOSED, 1 comment)  
   Anthropic cache writes billed at 2× base input for 1-hour retention, but pi prices at 1.25×. *Why it matters:* Misleads users on actual costs; could affect budget decisions.

10. **[#5612 — Switching models mid-session (DeepSeek V4 → Kimi K2.6) causes Connection error](https://github.com/earendil-works/pi/issues/5612)** (CLOSED, 1 comment)  
    Model swap triggers connection errors and tool-calling stops. OpenCode works fine simultaneously. *Why it matters:* Multi-model workflows are broken; likely transport state issue.

---

## Key PR Progress

1. **[#5609 — feat(providers): add Palantir Foundry LLM proxy and OAuth provider](https://github.com/earendil-works/pi/pull/5609)** (CLOSED)  
   New `palantir.ts` provider and OAuth support. Enables routing to Anthropic, Google, xAI, and OpenAI through Foundry. *Impact:* Enterprise expansion into defense/intelligence.

2. **[#5600 — fix(ai): honor Codex SSE header timeout setting](https://github.com/earendil-works/pi/pull/5600)** (OPEN)  
   Hardcoded 10s timeout on Codex SSE response headers now respects `timeoutMs`/`httpIdleTimeoutMs`. *Impact:* Fixes slow-connection failures.

3. **[#5594 — Fix Anthropic stream finalization on message_stop](https://github.com/earendil-works/pi/pull/5594)** (CLOSED)  
   Treats `message_stop` as logical end, cancels body reader immediately. Fixes #5592. *Impact:* Faster stream teardown; fixes proxy/gateway issues.

4. **[#5509 — feat: Add Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/5509)** (OPEN)  
   New provider for Mantle API supporting GPT 5.5 and 5.4. *Impact:* AWS-native users get a direct path without Azure.

5. **[#5587 — feat(coding-agent): add experimental first-time setup flow](https://github.com/earendil-works/pi/pull/5587)** (CLOSED)  
   Behind `PI_EXPERIMENTAL=1`, shows dark/light theme picker and analytics opt-in on first launch. *Impact:* Reduces onboarding friction.

6. **[#5583 — fix(coding-agent): preserve clickable subscription login URLs](https://github.com/earendil-works/pi/pull/5583)** (CLOSED)  
   Removes forced left-padding that broke long login URLs. *Impact:* Users can now click without manual URL repair.

7. **[#5561 — feat(ai): link AWS data retention docs in Bedrock validation errors](https://github.com/earendil-works/pi/pull/5561)** (CLOSED)  
   Claude Fable 5 requires data retention; error now links to AWS docs. *Impact:* Saves debugging time for Bedrock deployers.

8. **[#5562 — fix(tui): separate list items with blank lines in loose lists](https://github.com/earendil-works/pi/pull/5562)** (CLOSED)  
   CommonMark spec compliance: blank lines rendered between items for loose lists. *Impact:* Better Markdown rendering in TUI.

9. **[#5560 — fix(coding-agent): parse `:thinking` suffix from custom model IDs](https://github.com/earendil-works/pi/pull/5560)** (CLOSED)  
   Supports `:thinking` suffix for reasoning models. Fixes #5552. *Impact:* Enables reasoning-tier selection on custom providers.

10. **[#5585 — fix(tui): wrap CJK text at character boundaries in editor](https://github.com/earendil-works/pi/pull/5585)** (CLOSED)  
    Prevents character splitting in Japanese/Chinese text. Fixes #5582. *Impact:* i18n quality improvement for Asian-language users.

---

## Feature Request Trends

- **Multi-model support and model-switching** — Users want seamless mid-session model changes without transport errors (e.g., #5612). This is a top pain point for power users.
- **Custom provider/OAuth extensibility** — Multiple FRs for new providers (Palantir Foundry, Bedrock Mantle) and custom OAuth callback pages (#5372). The community wants a pluggable provider ecosystem.
- **Persona/role override in system prompt** — Users want to repurpose `pi` for non-coding tasks (security, QA, video editing) via agent role specification (#5577).
- **UI component library for extensions** — Requests for `multi-select-list` (#5025) and other core components indicate extension developers are hitting UI capability limits.
- **First-time setup flow** — The experimental PR (#5587) addresses a long-standing pain point; expect more investment in onboarding UX.

---

## Developer Pain Points

- **Timeout and stream finalization bugs** — Multiple issues (#3715, #5600, #5592) show undici default timeouts, hardcoded SSE timeouts, and mis-handled stream termination are recurring reliability gaps.
- **TUI crashes from null/undefined components** — Three separate crashes (#5599, #5597, #5604) on undefined content or children. These are "hard kill" bugs that terminate the process—top priority for stability.
- **Subscription login friction** — GHC (#5601) and Anthropic (#5291) login flows produce unhelpful errors or hang. Breaking login = zero onboarding.
- **Local backends & rate limiting** — Single-concurrency LLM backends hit 429s from parallel compaction (#5536). Local-first developers are underserved.
- **Cost reporting inaccuracies** — Wrong cache pricing (#5603) and the GitLab Duo 90s cutoff (#5611) erode trust in telemetry.
- **Package/theme state management** — `/share` fails on uninstalled themes (#5596); package pages show stale readmes (#5453). State persistence issues degrade the ecosystem experience.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-11

## Today’s Highlights

Terminal UI stability is the dominant theme this week, with multiple bugs reported around virtual viewport scrolling, mouse event handling, and cooked-mode drops during streaming. On the feature side, the Agent Team mode and daemon integration merge are progressing through PR review, while several enhancements around MCP governance and file-operation ergonomics have been proposed. A security issue was also fast-tracked: the `env` command was found to be misclassified as read-only, enabling arbitrary command execution.

## Releases

No new releases in the last 24 hours.

## Hot Issues

*   **[#4942] bug(cli): VP mode — scroll input conflicts with Composer input, no coexistence possible** — Users cannot scroll chat history (keyboard or wheel) when Composer is active in Virtualized History mode. The viewport height is also reported as taller than expected. This blocks enabling VP mode by default and has attracted 4 comments. [Link](https://github.com/QwenLM/qwen-code/issues/4942)
*   **[#4974] bug(cli): SGR mouse wheel sequences leak as typed text into the input box** — When SGR mouse tracking is enabled, wheel events sent by the terminal (`\x1b[<64;50;15M`) are double-consumed: the ink pipeline scrolls correctly, but the same bytes leak into readline as visible text. [Link](https://github.com/QwenLM/qwen-code/issues/4974)
*   **[#4973] bug(cli): terminal drops to cooked mode (all input dead until Enter)** — The `KeypressContext` fails to re-acquire raw mode when the last ink input handler deactivates, leaving the terminal unresponsive until the user presses Enter. [Link](https://github.com/QwenLM/qwen-code/issues/4973)
*   **[#4976] bug: auto-generated memory interferes with normal CLI invocation** — A user reports that automatic memory extraction injects irrelevant tool calls into a focused workflow (batch-reading articles), wasting multiple rounds before the actual task proceeds. [Link](https://github.com/QwenLM/qwen-code/issues/4976)
*   **[#4930] security: `env` in read-only command allowlist enables arbitrary command execution** — The `env` command is included in `READ_ONLY_ROOT_COMMANDS`, but it can be used to spawn sub-processes. This was closed quickly after filing. [Link](https://github.com/QwenLM/qwen-code/issues/4930)
*   **[#4877] bug: OpenWork can't distinguish same model from different providers** — When multiple OpenAI-compatible providers expose a model with the same ID (e.g., `glm-5`), the UI treats them as duplicates. [Link](https://github.com/QwenLM/qwen-code/issues/4877)
*   **[#4966] bug: SchemaValidator missing numeric string coercion causes MCP tool failures** — LLMs frequently emit numeric parameters as strings (`"depth": "3"`). Strict MCP servers reject these, causing tool call failures. [Link](https://github.com/QwenLM/qwen-code/issues/4966)
*   **[#4964] bug: Recover from the previous truncation caused by the max_tokens limit** — A user reports that responses truncated by `max_tokens` leave the session in a broken state, requiring manual recovery. [Link](https://github.com/QwenLM/qwen-code/issues/4964)
*   **[#4597] feat(stats): enhance stats with cross-session global usage tracking** — A well-received feature request (+1 👍, 4 comments) to make `/stats` persistent and add an interactive dashboard, similar to Claude Code. [Link](https://github.com/QwenLM/qwen-code/issues/4597)
*   **[#4891] bug: Terminal resize during streaming leaves fragmented content in scrollback** — Resizing the window mid-generation produces output rendered at inconsistent widths, with tool-call borders terminating at wrong columns. [Link](https://github.com/QwenLM/qwen-code/issues/4891)

## Key PR Progress

*   **[#4844] feat: add Agent Team experimental feature for parallel sub-agent coordination** — This PR (just merged) enables the model to create a named team, spawn parallel sub-agents that communicate with each other and the leader, and consolidate results into a single answer. [Link](https://github.com/QwenLM/qwen-code/pull/4844)
*   **[#4490] feat(daemon): merge daemon-mode feature batch into main** — A large integration merge (46 commits across 386 files, +115k LOC) rolling up the core daemon-mode feature set for v0.16-alpha. [Link](https://github.com/QwenLM/qwen-code/pull/4490)
*   **[#4827] feat(serve): ACP/REST parity — 29 new methods + production hardening** — Rebased on the daemon branch, this PR adds complete ACP/REST parity with 29 new `_qwen/*` dispatch methods. [Link](https://github.com/QwenLM/qwen-code/pull/4827)
*   **[#4959] fix(cli): enable VP scroll at idle prompt and fix viewport height** — Directly addresses the scroll conflict and viewport-height issues from #4942 and #4921, and adds key-binding disambiguation to make virtual viewport ready for default-on. [Link](https://github.com/QwenLM/qwen-code/pull/4959)
*   **[#4975] fix(web-shell): merge adjacent tool calls into one tool_group like native CLI** — The web shell now batches consecutive tool calls into a single card, matching the native CLI's batch rendering. [Link](https://github.com/QwenLM/qwen-code/pull/4975)
*   **[#4977] feat(web-shell): collapse thinking output to a 5-line window** — Thinking output in the Web Shell is collapsed to a 5-line bounded window with expand/collapse toggle, improving readability. [Link](https://github.com/QwenLM/qwen-code/pull/4977)
*   **[#4850] feat(extensions): interactive multi-tab /extensions manager** — Turns the `/extensions` command into a full interactive manager with Installed / Discover / Sources tabs, covering the full lifecycle of extension management. [Link](https://github.com/QwenLM/qwen-code/pull/4850)
*   **[#4979] fix(core): preserve teammate identity when resuming a tool call after approval** — Fixes a bug where approved teammate messages were incorrectly attributed to the leader. [Link](https://github.com/QwenLM/qwen-code/pull/4979)
*   **[#4897] feat(core): persist file history snapshots for cross-session /rewind** — Persists `FileHistorySnapshot` to JSONL, enabling `/rewind` to work across session resumes. [Link](https://github.com/QwenLM/qwen-code/pull/4897)
*   **[#4909] feat(extensions): support archive install sources** — Adds support for installing extensions from local `.zip` and `.tar.gz` archives, plus remote archive URLs. [Link](https://github.com/QwenLM/qwen-code/pull/4909)

## Feature Request Trends

*   **Persistent & Cross-Session Analytics** — Multiple requests ask for `/stats` to survive process exit and aggregate data across sessions (#4597), and for `/context` warnings to scale with the model's actual context window (#4941).
*   **MCP Governance** — Users want finer-grained control over MCP servers: a `deniedMcpServers` blacklist (#4940), and type coercion in the schema validator to fix numeric-string mismatches (#4966).
*   **Background Automation UX** — A cluster of requests wants sub-agent approval prompts to queue to the parent session instead of auto-denying (#4928, #4956), and for `fork` subagents to be enabled by default.
*   **File-Operation Ergonomics** — The community requests that `grep`/`egrep`/`fgrep` satisfy read-before-edit checks (#4939), and that `QWEN.md` length warnings be context-aware (#4941).
*   **UI Polish** — Requests include optional timestamps on responses (#4899), prominent git branch display in Desktop (#4769), and automated CHANGELOG generation (#4872).

## Developer Pain Points

*   **Terminal Rendering Instability** — The highest-frequency frustration area. Resize during streaming (#4891), virtual viewport scroll conflicts (#4942), cooked-mode drops (#4973), and leaked SGR sequences (#4974) all impact the core CLI experience.
*   **Auto-Memory Interference** — Several reports (#4976, #4374) describe auto-memory recall injecting irrelevant context or tool calls that disrupt focused workflows. Users want the ability to disable automatic recall while keeping extraction enabled.
*   **Model Switching & Provider Conflicts** — Users encounter friction when the same model ID from different providers is indistinguishable in the UI (#4877), and when newly available models are not reflected in the Qwen Code provider list (#4904).
*   **Sub-Agent Tool Call Failures** — Sub-agents fail to read image files (#4876) and fail to recover from `max_tokens` truncation (#4964), wasting user time on manual intervention.
*   **Compaction Configuration** — The auto/hard threshold in `/context` is reported as identical (#4945), meaning compaction doesn't trigger until the last possible moment, and issue #4838 highlights a missing microcompaction path for hook continuations.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-11

## Today's Highlights

The project has officially rebranded to **CodeWhale** with the v0.8.57 release — the `deepseek-tui` npm package is deprecated and no longer receives updates, and users must migrate via `docs/REBRAND.md`. The v0.8.56 "Community Harvest" release shipped localization, new providers, and prefix-cache stability improvements, while the repository is buzzing with activity around a significant v0.8.58 milestone that targets multi-provider support, hooks v2, and headless execution hardening. A torrent of 10+ new issues and PRs from the maintainer signal a major feature push in progress.

## Releases

- **v0.8.57** — CodeWhale is now the canonical project, command, npm package, and release-asset name. The legacy `deepseek-tui` npm package is fully deprecated. Migration guide available in `docs/REBRAND.md`.
- **v0.8.56 — "Community Harvest"** — Localization improvements, provider additions (e.g., Atlascloud, Moonshot), prefix-cache stability fixes, and assorted bug fixes. Also includes the first documented remote-workbench setup for DigitalOcean + Telegram.

## Hot Issues

1. [#2369 — Config Paths Fragmented Across OS and Cygwin](https://github.com/Hmbown/CodeWhale/issues/2369) — A deep investigation into how CodeWhale resolves config paths inconsistently across Linux, macOS, Windows, and Cygwin, with a silent migration bug that could corrupt settings. Comment count: 6. High community engagement.

2. [#1806 — Sub-agent 120s API timeout renders agent_open nearly unusable](https://github.com/Hmbown/CodeWhale/issues/1806) — A Windows user reports that all 5 sub-agents fail identically with a 120s timeout when converting a 280-line document. The timeout is too short for any real parallel task. Comment count: 3.

3. [#2574 — Provider fallback chain — auto-switch on API failure](https://github.com/Hmbown/CodeWhale/issues/2574) — Request for automatic fallback chains (e.g., `fallback_providers = ["deepseek", "openrouter"]`) when a provider returns 401/429/5xx errors, instead of requiring manual `/provider` commands. Comment count: 3.

4. [#2969 — CHANGELOG missing v0.8.55](https://github.com/Hmbown/CodeWhale/issues/2969) — A user noticed the changelog skipped v0.8.55 entirely. Quickly closed after maintainer acknowledgment. Comment count: 3.

5. [#3007 — Provider rejection blames a --provider flag the user never passed](https://github.com/Hmbown/CodeWhale/issues/3007) — When the resolved provider isn't TUI-capable, the error message incorrectly tells users to remove a `--provider` flag they never used. Closed with a fix in progress. Comment count: 2.

6. [#2372 — task_shell_start tty:true breaks sshpass and /dev/tty-dependent tools](https://github.com/Hmbown/CodeWhale/issues/2372) — Even with `danger-full-access`, `sshpass` fails because the controlling terminal isn't set properly. Claude Code and OpenAI Codex handle this correctly. Comment count: 2.

7. [#2893 — siliconflow provider config error](https://github.com/Hmbown/CodeWhale/issues/2893) — Two provider entries (`siliconflow` and `siliconflow-CN`) exist for different regions, but setting only the CN variant silently fails; users must duplicate configs. Comment count: 2.

8. [#3004 — api_key should support dynamic retrieval via scripts](https://github.com/Hmbown/CodeWhale/issues/3004) — User wants to fetch API keys from password managers like KeePassXC via shell scripts, similar to Claude Code's approach, instead of storing plaintext in dotfiles. Comment count: 2.

9. [#2989 — Agent stops early but reports "completed" with Ollama + qwen3-coder:30b](https://github.com/Hmbown/CodeWhale/issues/2989) — A critical bug where the agent halts prematurely but falsely reports task completion. Blocks use of local models. Comment count: 1.

10. [#2988 — Are all release channels paused after v0.8.54?](https://github.com/Hmbown/CodeWhale/issues/2988) — Community confusion about version skew across npm (v0.8.53), crates.io (v0.8.54), and GitHub Releases (v0.8.56). Comment count: 1.

## Key PR Progress

1. [#3036 — Hide internal UUIDs from normal UI](https://github.com/Hmbown/CodeWhale/pull/3036) — Replaces raw UUIDs and hex agent IDs with stable user-facing labels, keeping full identifiers accessible in hover/detail text. Closes #3030.

2. [#3035 — Throttle AgentProgress redraws to prevent freeze under subagent load](https://github.com/Hmbown/CodeWhale/pull/3035) — When 4+ sub-agents run concurrently, the render loop saturates and freezes the terminal. Adds throttling to prevent full redraw on every progress event.

3. [#3051 — Add /voice slash command for speech-to-text input](https://github.com/Hmbown/CodeWhale/pull/3051) — Inspired by MiMo Code's voice UX. Adds one-shot speech recording, AI transcription via the active provider, and seamless composer insertion. Community contribution.

4. [#3049 — JSON decision contract, glob matchers, project-local hooks](https://github.com/Hmbown/CodeWhale/pull/3049) — Hooks can now emit `{"decision":"allow"|"deny"|"ask"}` on stdout, plus glob-based file matchers and project-local hook files. Closes #3026.

5. [#3052 — Verbosity settings: normal vs concise modes](https://github.com/Hmbown/CodeWhale/pull/3052) — Reduces agent chatter in non-interactive modes. CLI modes (`exec`, `eval`, `swebench`) default to concise. Community contribution.

6. [#3040 — Clickable sidebar rows for Tasks and Agents panels](https://github.com/Hmbown/CodeWhale/pull/3040) — Mouse-click dispatch for sidebar rows: click a job's label to view it, click its detail row to cancel, click agent rows to open `/subagents`.

7. [#2892 — Localize sandbox elevation dialog across 7 locales](https://github.com/Hmbown/CodeWhale/pull/2892) — Migrates the sandbox elevation widget from hardcoded English to `MessageId`-based translations (En, Ja, ZhHans, ZhHant, PtBr, Es419, Vi). Community contribution.

8. [#3042 — Headless exec hardening flags](https://github.com/Hmbown/CodeWhale/pull/3042) — Adds `--allowed-tools`, `--disallowed-tools`, `--max-turns`, and `--append-system-prompt` to `codewhale exec` for CI/benchmark use. Refs #3027.

9. [#3048 — Parameterize model-specific facts in prompts](https://github.com/Hmbown/CodeWhale/pull/3048) — Stops telling all models they are "DeepSeek V4 with 1M context." Now substitutes real context window, pricing, and thinking capabilities from runtime lookups. Refs #3025.

10. [#3034 — v0.8.58 branch: Constitution refactor, Codex fixes, sidebar improvements](https://github.com/Hmbown/CodeWhale/pull/3034) — The initial v0.8.58 milestone branch carrying a YAML-based constitution prompt, rebrand fixes, split sidebar models panel, and provider error improvements.

## Feature Request Trends

- **Multi-provider / Model-agnostic architecture** (Issues #3025, #3018, #3014, #3048, #3050) — The dominant theme. Users want to use non-DeepSeek models (Qwen, Kimi, GPT, Claude, Ollama) without hardcoded DeepSeek assumptions in prompts, auto-routers, subagent selection, and pricing. This is the core of the v0.8.58 milestone.

- **Provider resilience** (#2574, #3019) — Automatic fallback chains on API failure and proper retry/backoff for the OpenAI Codex provider.

- **Remote workbench / unattended operation** (#1990, #2964, #3027, #3044) — DigitalOcean + Telegram setup, autonomous agent loops, headless exec hardening for CI.

- **Global config & user experience** (#3012, #3004, #2934) — Auto-loading `~/.codewhale/instructions.md`, dynamic API key retrieval from password managers, persistent session sidebar.

- **Voice input** (#3051) — A single community contribution, but noteworthy as a novel modality.

## Developer Pain Points

- **Rebrand migration friction** (#2960, #2664, #2969, #2988) — Config paths still reference `deepseek` after rebrand, update paths from old npm package to `codewhale` are broken or undocumented, changelogs have gaps, and release channels are out of sync. The most frequent source of user confusion.

- **Provider configuration complexity** (#2893, #3018, #3025) — Users must duplicate config entries for region-specific providers, and non-DeepSeek models get wrong system prompts and error out. Hardcoded assumptions about DeepSeek undermine the "all models" vision.

- **Sub-agent & timeout reliability** (#1806, #2989, #3035) — Hard 120s API timeouts make sub-agents unusable for real work, agents falsely report completion with local models, and the UI freezes under concurrent sub-agent load.

- **Config & dotfile management** (#3004, #2574) — API keys stored in plaintext in dotfiles is a security concern; users want script-based key retrieval. No automatic failover when a provider goes down.

- **Sleep/resume corruption** (#2990) — Active turns die with "Stream read error" after the computer sleeps, losing all in-flight work. A significant UX gap for laptop users.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*