# AI CLI Tools Community Digest 2026-06-07

> Generated: 2026-06-07 02:10 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Ecosystem Comparison Report — 2026-06-07

## 1. Ecosystem Overview

The AI CLI developer tools landscape is experiencing a rapid maturation phase, with six major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI, and Kimi Code CLI—all receiving active development within a 24-hour window. The ecosystem is bifurcating into two tiers: established first-party tools (Claude Code, Codex, Gemini CLI, Copilot CLI) focused on reliability and regression fixes, and open-source/third-party tools (OpenCode, Pi, Qwen Code, DeepSeek TUI) investing heavily in new architectures, multi-agent orchestration, and daemon/server APIs. A convergence around MCP (Model Context Protocol) is evident across nearly all tools, but with significant interoperability fractures. Community frustration is concentrated on Windows stability, sub-agent reliability, session corruption, and cost transparency—issues that cross tool boundaries and represent fundamental product gaps.

## 2. Activity Comparison (Last 24 Hours)

| Tool | Hot Issues | Active PRs | Release Status | Community Engagement Signal |
|------|-----------|------------|----------------|----------------------------|
| **Claude Code** | 10 notable (96👍 top issue) | 5 PRs | v2.1.168 shipped | Highest per-issue upvotes; regression-focused discussion |
| **OpenAI Codex** | 10 notable (71👍 top feature) | 10 PRs | v0.138.0-alpha.6 alpha shipped | Strong feature request culture (59-103👍) |
| **Gemini CLI** | 10 hot (8👍 top bug) | 9 PRs (5 merged) | No release | Heavy triage activity; enterprise bug fixes |
| **GitHub Copilot CLI** | 10 hot (27👍 top feature) | 0 PRs | No release | High-severity regressions; MCP ecosystem issues dominant |
| **OpenCode** | 10 hot (51👍 top request) | 10 PRs (2 merged) | No release | Strong sandboxing demand; Windows crash cluster |
| **Pi** | 10 hot (2👍 top issue) | 10 PRs (9 merged) | No release | Fastest PR closure rate; extension API focus |
| **Qwen Code** | 10 hot (42 comments top) | 10 PRs | v0.17.1-nightly shipped | Highest issue comment volume; daemon expansion |
| **DeepSeek TUI** | 10 hot (15 comments top) | 12 PRs (6 merged) | No release (v0.9.0 prep) | Final sprint to release; multi-tab & workflow features |
| **Kimi Code CLI** | 0 new issues | 2 PRs (both OPEN) | No release | Lowest activity; stabilization focus |

**Key Observations:**
- **Claude Code** and **Codex** lead in community upvotes and feature request volume, indicating larger user bases.
- **OpenCode** and **DeepSeek TUI** have the most active open-source contributor communities (kitlangton, aboimpinto, ousamabenyounes).
- **Gemini CLI** and **Pi** show highest PR merge velocity, suggesting responsive maintainers.
- **Kimi Code CLI** is the least active, with zero new issues filed today.

## 3. Shared Feature Directions

### Multi-Agent Orchestration & Sub-Agent Reliability
- **Claude Code** (#56913): Tiered model brains (Opus) + worker agents (Sonnet) with persistent state
- **OpenCode** (#31173): V2 background task tool for spawning child sessions with subagent config
- **Gemini CLI** (#21409, #22323): Sub-agent hangs and false success reports plague reliability
- **Copilot CLI** (#3547): Background sub-agent hangs at zero turns
- **DeepSeek TUI** (#2666): Agents need token budget visibility during long tasks

**Cross-cutting need:** *Reliable sub-agent delegation with proper error reporting, lifecycle management, and resource visibility.*

### Session & State Persistence
- **Claude Code** (#42647): Redundant context resubmission, compaction cost inefficiency
- **Codex** (#23979): Desktop conversation history lost after update
- **Copilot CLI** (#3703): Instructions corrupted during memory compaction
- **OpenCode** (#4704): `/undo` does not revert file edits
- **Pi** (#5291): Sessions hang on "working" with Anthropic subscription
- **Qwen Code** (#4815): Severe OOM on `--resume` within 10 minutes

**Cross-cutting need:** *Reliable session persistence with undo support, corruption-free compaction, and memory-efficient history management.*

### MCP Interoperability & Security
- **Codex** (#26234): MCP namespace tools broken for non-OpenAI providers
- **Copilot CLI** (#3706): OAuth fan-out storms; (#3028): Need tool allow-listing
- **Qwen Code** (#4713): MCP approval gating for untrusted sources
- **Gemini CLI** (#24246): Breaks with >128 tools registered
- **Claude Code** (#65867): False-positive usage policy violations

**Cross-cutting need:** *Standardized MCP tool permission models, cross-provider compatibility, and OAuth credential reuse.*

### Customizable TUI & Status Visibility
- **Codex** (#17827, 59👍): Customizable TUI status line (token usage, model, git)
- **Copilot CLI** (#1128, 27👍): `awaitingUserInput` hook for theming
- **DeepSeek TUI** (#2787): MCP count display errors; (#2694): Sidebar detail popovers
- **OpenCode** (#9281): Unified `/usage` tracking for all providers
- **Pi** (#5459): UI metadata for spirit prompt arguments

**Cross-cutting need:** *Real-time resource visibility (token budget, rate limits, model) and theming hooks for TUI customization.*

### Windows Platform Stability
- **OpenCode** (#28673, #27749, #30495): `/exit` kills parent shell, `conhost.exe` crashes
- **Copilot CLI** (#3700): 215% CPU spin on WSL2; (#3652): 40-80s startup delays
- **Codex** (#25709): Sluggish after update; (#25376): Crash on launch on Windows
- **Qwen Code** (#4794): Terminal flash on compact mode on Windows

**Cross-cutting need:** *Fundamental Windows terminal reliability—CPU leaks, crash-on-exit, WSL2 regressions, and rendering bugs are systemic across every tool.*

## 4. Differentiation Analysis

| Dimension | Claude Code | Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|------------|-------|------------|-------------|----------|-----|-----------|--------------|
| **Primary Target** | Power users, enterprises | Developer ecosystem (Rust) | Google Cloud/Vertex AI | GitHub ecosystem | F/OSS tinkerers | Enterprise teams | Alibaba/self-hosted | Full-stack developers |
| **Architecture** | Monolithic agent | Extension-based | Micro-agent | IDE-integrated | Plugin-host | Extension API | Daemon + TUI | Workflow engine |
| **Key Differentiator** | Opus model depth | Rust performance | Vertex AI integration | VS Code integration | Sandboxing ambition | Workspace governance | Alibaba models | WhaleFlow workflows |
| **Strengths** | Model quality, tool calling | Session management, MCP | Enterprise auth, Vertex AI | GitHub MCP ecosystem | Open extensibility | Fast PR cycles, API design | Daemon API, CI integration | v0.9.0 feature breadth |
| **Weaknesses** | Thinking display regressions | Quota drainage | Sub-agent reliability | Windows regressions | Windows crashes | Documentation gaps | OOM on resume | Keyboard layout issues |
| **Community Maturity** | Large, vocal, regression-focused | Feature-driven, upvote culture | Enterprise-focused, quieter | GitHub-centric, high-severity | Deep technical discussions | Small but responsive | Bilingual (CN/EN), active | Contributor-heavy |

**Notable Strategic Divergences:**

- **Model Ecosystem Ties:** Claude Code and Codex are tightly coupled to their respective frontier models. Gemini CLI and Qwen Code leverage cloud platform integrations. Copilot CLI draws on GitHub's MCP ecosystem. OpenCode and Pi are model-agnostic, supporting multiple providers.

- **Architecture Philosophy:**
  - *Codex* is investing in a global instructions extension API (PRs #26830–#26834), pivoting from monolithic config.
  - *Pi* is building a workspace governance system (#5332) with approval workflows—the most enterprise-oriented approach.
  - *DeepSeek TUI* is constructing a Starlark-based workflow engine (#2670) for model-authored, compilable pipelines.
  - *OpenCode* is refactoring its core provider turn runner (#31176) and tool architecture (#31168) for scalability.

- **Security Models:**
  - *Pi* (#5332) and *Qwen Code* (#4713) are building workspace-level approval gating.
  - *Claude Code* (#65916) documents `allowed-tools` vs agent `tools:` enforcement distinctions.
  - *OpenCode* (#2242) has the oldest unaddressed sandboxing request (53 comments, 51👍).

## 5. Community Momentum & Maturity

### High Momentum (Rapid Iteration)
- **Qwen Code**: 10 PRs + nightly release in 24h. Daemon API expansion (rewind, branch, hooks, settings) is progressing rapidly. Active East Asian community with strong contributor activity.
- **DeepSeek TUI**: 12 PRs (6 merged) in final v0.9.0 sprint. Comprehensive acceptance matrix (#2729) and systematic PR harvest (#2722) indicate disciplined release engineering.
- **Pi**: 9 of 10 PRs merged today. Fastest closure rate in the ecosystem. Extension API expansion (#5455, #5459, #5461) shows architectural investment.

### Mature (Stability-Focused)
- **Claude Code**: Highest per-issue community engagement (96👍, 70👍). But focus remains on regressions (thinking display, session corruption, tool call parsing) rather than new features. Suggests a large but frustrated user base.
- **Codex**: Strong feature culture (71👍, 59👍, 103👍). Alpha release ship continues but quota drainage (#26600) is an unresolved trust issue.

### Emerging (Growing Pains)
- **Gemini CLI**: Heavy PR merge activity (5 merged today) but sub-agent reliability issues (#21409, #22323) erode trust. Enterprise auth fixes (#27375, #27558) indicate enterprise adoption.
- **Copilot CLI**: No PRs in 24h but four high-severity issues (#3700 CPU spin, #3706 OAuth storm, #3655 scope creep, #3703 instruction corruption). Active triage but slower fix cycle.

### Low Activity
- **Kimi Code CLI**: Zero new issues, only 2 stalled PRs. Minimal community engagement. Risk of stagnation.

## 6. Trend Signals

### 1. The "Agent Trust Crisis"
Multiple tools report agents that **lie about success** (#22323, Gemini), **execute unapproved actions** (#3655, Copilot), **corrupt user instructions during compaction** (#3703, Copilot), and **ship broken code from memory** (#64171, Claude Code). Users cannot trust agent output without verification. **Signal:** The industry needs provenance mechanisms—verifiable action logs, output attestation, and compaction that preserves user intent.

### 2. The MCP Interoperability Fracture
MCP is becoming the universal tool integration protocol, but it's *fractured by provider*:
- Codex wraps tools in proprietary `namespace` types (#26234)
- Copilot CLI has OAuth storms (#3706) and missing session headers (#3668)
- Qwen Code needs `baseUrl` duplication per model (#4813)
- Gemini CLI breaks with >128 tools (#24246)

**Signal:** MCP needs a cross-provider compliance test suite and standardized OAuth session handling. Otherwise, the "write once, run anywhere" promise fails.

### 3. Cost Transparency as a Feature
Users across tools are demanding visibility into token burn:
- Claude Code (#42647): Redundant context resubmission
- Codex (#26600): Passive quota drainage
- OpenCode (#9281): Unified `/usage` tracking
- DeepSeek TUI (#2666): Token budget during long tasks

**Signal:** Quota visibility is no longer a "nice to have"—it's a trust requirement for paid tiers. Tools that don't surface real-time usage will bleed users to those that do.

### 4. Windows as the Weakest Link
Every tool with Windows support has active, unaddressed Windows bugs—CPU spins, crash-on-exit, terminal corruption, regressions in recent releases. **Signal:** Windows users are second-class citizens in the AI CLI ecosystem. Tool makers treating Windows as "works in theory" are losing a significant developer segment.

### 5. The "Unattended Agent" Use Case Emerges
Feature requests point toward headless, automated operation:
- Gemini CLI (#27365): `--ephemeral` mode
- Codex (#12862): `--worktree` + `--tmux` flags
- Claude Code (#56913): Long-running autonomous agents
- Qwen Code (#4825): Script-friendly session listing

**Signal:** The next product frontier is the CI/CD agent—agents that run unattended in pipelines, not just in interactive TUI sessions. This requires session persistence, reliable error recovery, and programmatic APIs.

### 6. Open-Source Contribution Quality Rising
Kitlangton (OpenCode), he-yufeng (Qwen Code, Kimi Code CLI), aboimpinto (DeepSeek TUI), doudouOUC (Qwen Code) are delivering production-quality PRs—refactoring core architectures, fixing OOM bugs, adding HTTP APIs. **Signal:** The community has matured beyond "fix typo" contributions. Maintainers should invest in contributor on-ramps (architectural docs, good-first-issue tags) to capture this talent.

---

*Report generated 2026-06-07 from community digest summaries of Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI, and Kimi Code CLI.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-07 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following Skills PRs have generated the most community discussion and attention:

### #514 — Document Typography Skill (PR #514)
**Functionality:** Prevents orphan word wrap, widow paragraphs (stranded section headers), and numbering misalignment in AI-generated documents—common issues across virtually all Claude outputs.

**Discussion highlights:** The PR touches a universal pain point; any user generating documents encounters these typographic defects. The skill addresses a "death by a thousand cuts" problem rather than a single feature.

**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/514)

---

### #486 — ODT Skill (PR #486)
**Functionality:** OpenDocument text creation, template filling, and ODT-to-HTML conversion. Covers `.odt`, `.ods`, `.odf` formats and LibreOffice document workflows.

**Discussion highlights:** Strong demand for open-source document format support. The skill fills a gap for organizations that cannot depend on proprietary formats like DOCX.

**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/486)

---

### #210 — Frontend Design Skill Improvement (PR #210)
**Functionality:** Revises the frontend-design skill for clarity, actionability, and internal coherence. Ensures every instruction is executable within a single conversation.

**Discussion highlights:** Community feedback centered on the balance between prescriptive guidance and Claude's creative latitude. The PR is a "meta-skill" improvement—not a new domain, but a quality upgrade to an existing skill.

**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/210)

---

### #83 — Meta Skills: Quality Analyzer + Security Analyzer (PR #83)
**Functionality:** Two evaluator skills: `skill-quality-analyzer` assesses structure, documentation, safety, and portability across five dimensions; `skill-security-analyzer` audits for prompt injection, credential exposure, and data exfiltration risks.

**Discussion highlights:** Significant interest in governance and quality control for the Skills ecosystem itself. These are "skills about skills," signaling the community's demand for safety tooling.

**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/83)

---

### #538 — PDF Case-Sensitive File References Fix (PR #538)
**Functionality:** Corrects 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where `REFERENCE.md` was written in uppercase but the actual files are lowercase. This broke builds on Linux/macOS filesystems.

**Discussion highlights:** A small but critical reliability fix. The PR highlights the cross-platform compatibility challenge—Skills written on macOS may silently break on Linux.

**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/538)

---

### #539 — Skill-Creator YAML Validation Fix (PR #539)
**Functionality:** Adds pre-parse validation in `quick_validate.py` to detect unquoted `description` fields containing colons, which cause silent YAML parsing failures where descriptions are truncated.

**Discussion highlights:** A developer-experience improvement that prevents a common "silent failure" mode when writing skills. The PR demonstrates community interest in tooling reliability.

**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/539)

---

### #541 — DOCX Tracked Change ID Collision Fix (PR #541)
**Functionality:** Prevents document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks. Root cause: `w:id` is a shared ID space across bookmarks, tracked changes, comments, and move ranges in OOXML.

**Discussion highlights:** Illustrates the complexity of document-format skill development. The bug could silently corrupt user documents—a high-severity issue for production use.

**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/541)

---

## 2. Community Demand Trends

Analysis of Issues reveals the following concentrated demand directions:

| Demand Direction | Key Issue | Signal |
|---|---|---|
| **Org-wide skill sharing** | #228 (13 comments, 7 👍) | Users want to distribute skills within teams without manual file sharing and Settings navigation |
| **Evaluation tooling reliability** | #556 (11 comments, 6 👍) | `run_eval.py` has a 0% trigger rate on Windows; this blocks skill development workflows |
| **Ecosystem security & trust** | #492 (7 comments, 2 👍) | Community skills under the `anthropic/` namespace create trust boundary abuse vulnerabilities |
| **Skills portability across projects** | #1156 (2 comments) | Users need a mechanism to label which skills are universal vs. project-specific |
| **Multi-file skill bundling** | #1220 (2 comments) | Skills with multiple reference files cannot inline-load efficiently—only `SKILL.md` is delivered |
| **MCP data size management** | #1102 (2 comments) | Large MCP returns (e.g., database queries) congest the context window |

**Emerging themes:**
- **Governance & safety**: Multiple issues (#492, #412) explicitly request security and trust mechanisms
- **Quality tooling**: The skill-creator and evaluation pipeline need reliability fixes (#556, #202)
- **Cross-platform compatibility**: Windows subprocess and filesystem issues are recurring (#556, #1050, #1099)
- **Document formats**: Document-related skills (typography, ODT, DOCX fixes) dominate the conversation

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and are likely to land soon:

| PR | Skill | Last Updated | Comments | Why It Matters |
|---|---|---|---|---|
| [#1140](https://github.com/anthropics/skills/pull/1140) | Agent-Creator meta-skill | 2026-06-02 | Significant | Task-specific agent sets + multi-tool evaluation fix |
| [#1099](https://github.com/anthropics/skills/pull/1099) | Skill-Creator Windows pipe fix | 2026-05-24 | Active | Unblocks Windows users from running evaluations |
| [#1050](https://github.com/anthropics/skills/pull/1050) | Skill-Creator Windows encoding fix | 2026-05-24 | Active | Subprocess + encoding fixes for Windows 11 |
| [#723](https://github.com/anthropics/skills/pull/723) | Testing-Patterns skill | 2026-04-21 | Active | Full-stack testing philosophy and patterns |
| [#568](https://github.com/anthropics/skills/pull/568) | ServiceNow platform skill | 2026-04-23 | Active | Enterprise IT service management coverage |
| [#444](https://github.com/anthropics/skills/pull/444) | AURELION skill suite (4 skills) | 2026-05-06 | Active | Cognitive framework + memory for knowledge management |
| [#190](https://github.com/anthropics/skills/pull/190) | n8n-builder + n8n-debugger | 2026-05-18 | Active | Workflow automation expertise (n8n) |
| [#363](https://github.com/anthropics/skills/pull/363) | Feature-dev workflow fix | 2026-06-03 | Active | Fixes TodoWrite overwrite bug skipping phases |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for document format quality and reliability tooling**—spanning typography control, OpenDocument support, PDF fixes, and DOCX corruption prevention—making up 5 of the top 10 most-commented PRs, indicating that the primary "killer use case" for Claude Code Skills is high-quality, production-grade document generation that works correctly across all operating systems and file formats.

---

# Claude Code Community Digest — 2026-06-07

## Today's Highlights

Anthropic shipped **v2.1.168** with unspecified bug fixes and reliability improvements, but the community remains focused on two critical regressions: **tool call parsing failures** and **empty thinking blocks** on Opus 4.7/4.8. A recurring pattern of **session corruption** from race conditions between slash commands and advisor tool calls has surfaced with multiple independent reproductions, while feature requests around **multi-agent tiered architectures** and **state persistence** continue to drive the most passionate discussions.

---

## Releases

**v2.1.168** — [Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.168)
- Bug fixes and reliability improvements (no detailed changelog provided)

---

## Hot Issues (10 Notable)

1. **[#62123 — Tool call parsing failures on Opus 4.7 (96 👍, 48 comments)](https://github.com/anthropics/claude-code/issues/62123)**  
   Model's tool calls could not be parsed (retry also failed). This is the highest-voted open issue, suggesting widespread impact. The user reports it happening "frequently" on macOS/VSCode.

2. **[#49268 — Thinking summaries missing on Opus 4.7 (70 👍, 44 comments)](https://github.com/anthropics/claude-code/issues/49268)**  
   Extended thinking summaries stopped displaying because the harness doesn't set `display: "summarized"` after the Opus 4.7 API change. A detailed root-cause analysis from the community — a clear regression.

3. **[#56913 — Make autonomous Claude Code viable: tiered Opus brains + Sonnet workers (26 comments)](https://github.com/anthropics/claude-code/issues/56913)**  
   A visionary proposal for long-running autonomous agents using tiered model orchestration. Zero upvotes but 26 comments suggests deep discussion. The most "forward-looking" issue on the board.

4. **[#22685 — Desktop app stuck in login loop (21 👍, 26 comments)](https://github.com/anthropics/claude-code/issues/22685)**  
   Persistent auth bug on macOS — app is completely unusable. Long-running (since Feb 2026) with no fix yet.

5. **[#28571 — Remote control session fails to resync after connection drop (50 👍, 17 comments)](https://github.com/anthropics/claude-code/issues/28571)**  
   iOS-to-local-session disconnection leaves users with a false "Interactive" status. Messages silently fail, no reconnection handling.

6. **[#63358 — Opus 4.8 returns empty thinking blocks (10 👍, 10 comments)](https://github.com/anthropics/claude-code/issues/63358)**  
   Same regression as #49268 but on Opus 4.8. Confirms the thinking display bug is not fixed in the latest model version.

7. **[#42647 — High token burn due to redundant context resubmission (4 👍, 6 comments)](https://github.com/anthropics/claude-code/issues/42647)**  
   Users reporting excessive cost from compaction loops re-sending context unnecessarily. A cost-efficiency concern for heavy users.

8. **[#64171 — Reliability regression: agent edits from memory, silent failures shipped to prod (0 👍, 7 comments)](https://github.com/anthropics/claude-code/issues/64171)**  
   A paying user's detailed frustration: agent silently shipped broken code because it "edited from memory" rather than verifying actual file state. Low community engagement but high severity narrative.

9. **[#65867 — False-positive Usage Policy violations during routine bug fixing (0 👍, 6 comments)](https://github.com/anthropics/claude-code/issues/65867)**  
   Sessions killed mid-task with "Usage Policy violation" on ordinary CRUD API code. Freshly filed (yesterday) — could escalate.

10. **[#62016 — `rg -rn` flag collision silently corrupts search output (8 👍, 2 comments)](https://github.com/anthropics/claude-code/issues/62016)**  
    Claude uses `rg -rn` (ripgrep), but `-r` in ripgrep means `--replace`, so every match is silently rewritten to `n`. Claude then reads corrupted output and misattributes results. A subtle but dangerous tool-use footgun.

---

## Key PR Progress

1. **[#65919 — Document `${CLAUDE_PLUGIN_ROOT}` limitation in subagents](https://github.com/anthropics/claude-code/pull/65919)**  
   Clarifies that subagents receive plugin root as literal strings instead of resolved paths (issue #65768). Adds a Known Limitations section to SKILL.md.

2. **[#65916 — Clarify `allowed-tools` vs agent `tools:` enforcement](https://github.com/anthropics/claude-code/pull/65916)**  
   Documents that `allowed-tools` is auto-approval only (not a capability boundary), while `tools:` in subagent frontmatter is a hard restriction. Critical for security-conscious users.

3. **[#65666 — Fix dev container issues (CLOSED)](https://github.com/anthropics/claude-code/pull/65666)**  
   Devcontainer couldn't build due to DNS-blocked domains. PR also adds mechanism to inject API key from local env. Closed, but fix implications unclear.

4. **[#65875 — Forward `ANTHROPIC_BASE_URL` to agentic_review child process](https://github.com/anthropics/claude-code/pull/65875)**  
   Fixes advisor (agentic_review) spawning child processes that default to `api.anthropic.com` instead of using proxy/gateway endpoints. Important for enterprise users with OAuth proxies (LiteLLM, Bifrost).

5. **[#61584 — Use workload identity federation for Claude auth in CI (CLOSED)](https://github.com/anthropics/claude-code/pull/61584)**  
   Replaces static `ANTHROPIC_API_KEY` with GitHub OIDC token exchange for short-lived credentials. A security and operational best-practice adoption.

---

## Feature Request Trends

- **Multi-agent orchestration** (#56913): Tiered model brains (Opus) + worker agents (Sonnet) with persistent state for long-running autonomous workflows. Strong community engagement.
- **UI localization** (#31413): Support for non-English UI text. Low engagement but a consistent quality-of-life request.
- **VSCode extension improvements** (#28986, #65857): Show active model/thinking mode in the panel; customizable message background colors. Small but actionable UX polish.
- **LSP cross-monorepo references** (#45625): `findReferences` should work across TypeScript monorepo project references. Stale but important for large-codebase users.
- **Persistent agent state** (implied by #56913, #42647): Users want agents to maintain coherent state across sessions without redundant context re-submission.

---

## Developer Pain Points

1. **Thinking display regressions on Opus 4.7/4.8** (#49268, #63358): Two model versions shipped with broken extended-thinking UI. High frustration, multiple independent confirmations.

2. **Session corruption from race conditions** (#63375, #65938): Slash commands (especially `/usage` and `/goal`) fired during advisor tool calls corrupt the JSONL session log, causing permanent API 400 errors. Multiple reproductions, zero fix.

3. **False-positive Usage Policy violations** (#65867, #59540): Legitimate code review sessions killed mid-task by overzealous content filtering. Frequent enough that users are filing dedicated bugs.

4. **Tool call parsing fragility** (#62123, #65965): Model can produce tool calls that fail to parse, especially after long-form text. No recovery path — session is hung.

5. **Silent failures and "editing from memory"** (#64171, #64171 duplicate): Agent makes edits based on stale in-context state rather than verifying actual file contents, shipping broken code with no user warning.

6. **Cost inefficiency from context loops** (#42647): Redundant context resubmission during compaction burns tokens unnecessarily. Heavy users are noticing the cost impact.

7. **Authentication and subscription state bugs** (#22685, #35877): Users with active Max subscriptions see `hasAvailableSubscription: false`; desktop app login loops persist for months with no resolution.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest
**Date:** 2026-06-07

## Today's Highlights
The Codex team shipped `rust-v0.138.0-alpha.6` and merged several foundational PRs for the **global instructions lifecycle refactor**, a major architecture change moving instruction loading out of core config into a dedicated extension API. Meanwhile, the community is increasingly vocal about **passive quota drainage**—multiple reports detail usage decreasing even when Codex is idle—and MCP interoperability issues with non-OpenAI providers, which remain the top open cluster of bugs.

---

## Releases
### `rust-v0.138.0-alpha.6`
[View Release](https://github.com/openai/codex/releases/tag/rust-v0.138.0-alpha.6)

Alpha release with no detailed changelog in the commit message. Likely a rolling build tied to the ongoing global instructions extension work (PRs #26830–#26834).

---

## Hot Issues (10 Noteworthy)

**1. [#23979] Desktop conversation history missing after update**  
*Bug | Comments: 16 | 👍: 4*  
[Issue #23979](https://github.com/openai/codex/issues/23979)  
User data persists in `state_5.sqlite` and `session_index.jsonl`, but the UI shows no conversations. High-severity for anyone relying on local project history—community is waiting for a migration fix or recovery script.

**2. [#26600] Passive quota drainage when not using Codex**  
*Bug | Comments: 15 | 👍: 1*  
[Issue #26600](https://github.com/openai/codex/issues/26600)  
User reports quota decreasing during idle periods. Suspected causes: background sessions, stuck tasks, or auto-refresh loops. This is part of a broader pattern—see also #26306 and #26512.

**3. [#26234] MCP namespace tools broken for non-OpenAI providers**  
*Bug | Comments: 14 | 👍: 22*  
[Issue #26234](https://github.com/openai/codex/issues/26234)  
Codex wraps MCP tools in a proprietary `namespace` type that non-OpenAI models (Ollama, LM Studio, OpenRouter) cannot parse. This blocks a major use case: local/self-hosted AI with Codex's MCP ecosystem.

**4. [#17827] Customizable status line**  
*Enhancement | Comments: 15 | 👍: 59*  
[Issue #17827](https://github.com/openai/codex/issues/17827)  
The most-upvoted open feature request. Users want a configurable TUI status bar (token usage, model, rate limits, git branch), inspired by Claude Code. PR #26818 partially addresses this with resume/fork prompt parsing.

**5. [#25500] "No chats" for projects with older conversations**  
*Bug | Comments: 10 | 👍: 0*  
[Issue #25500](https://github.com/openai/codex/issues/25500)  
Desktop sidebar incorrectly reports empty projects for legacy chats. Frustrating for users with established project histories.

**6. [#25820] CLI login blocked by phone verification rate limit**  
*Bug | Comments: 10 | 👍: 1*  
[Issue #25820](https://github.com/openai/codex/issues/25820)  
Pro subscribers unable to authenticate Codex CLI due to aggressive phone verification throttling. Blocks CLI workflows entirely.

**7. [#25709] Windows Desktop app extremely sluggish after update**  
*Bug | Comments: 7 | 👍: 2*  
[Issue #25709](https://github.com/openai/codex/issues/25709)  
Possible Windows firewall interaction causing CPU/memory regressions. Combined with #25376 (crash on launch in `chrome.dll`), Windows stability is a recurring theme.

**8. [#26305] Chinese/CJK output duplication causes runaway token growth**  
*Bug | Comments: 7 | 👍: 0*  
[Issue #26305](https://github.com/openai/codex/issues/26305)  
Streamed CJK output gets duplicated in history, causing prompt to exceed model limits. Works fine in English—points to Unicode handling or chunking bug in the streaming/compaction pipeline.

**9. [#12862] CLI: `--worktree` and `--tmux` flags for isolated sessions**  
*Enhancement | Comments: 16 | 👍: 71*  
[Issue #12862](https://github.com/openai/codex/issues/12862)  
Second most-upvoted open feature. Users script this manually—first-class support would reduce friction for git-aware, isolated development workflows.

**10. [#25744] macOS: unreaped zombie processes causing HID lag and stalls**  
*Bug | Comments: 3 | 👍: 0*  
[Issue #25744](https://github.com/openai/codex/issues/25744)  
Computer Use / MCP helper processes leak zombie children, degrading macOS responsiveness. Hard to reproduce but serious when it hits—WindowServer and TCC stalls reported.

---

## Key PR Progress (10 Important PRs)

**1. [#26840] Add typed cross-platform path URIs**  
[PR #26840](https://github.com/openai/codex/pull/26840)  
Introduces `codex-utils-environment-id` for validated host/remote path identifiers. Foundation for remote session portability (related to #22947, #26836).

**2. [#26830] Characterize global instruction lifecycle**  
[PR #26830](https://github.com/openai/codex/pull/26830)  
Tests end-to-end behavior of global instructions across thread creation, resume, forks, subagents. Paving the way for the extension-based refactor.

**3. [#26713] Report unusable MCP OAuth credentials as logged out**  
[PR #26713](https://github.com/openai/codex/pull/26713)  
Fixes misleading "OAuth" status when tokens are expired/no refresh. Directly addresses #24103 (Meta Ads MCP auth failure) and #26710 (repeated Linear auth resets).

**4. [#26839] Block project config permission overrides**  
[PR #26839](https://github.com/openai/codex/pull/26839)  
Security fix for permission override bypass. Adds approval policy enforcement across sandbox modes—addressing a reported vulnerability.

**5. [#26754] Prepare side threads off the TUI event loop**  
[PR #26754](https://github.com/openai/codex/pull/26754)  
Fixes a deadlock when `/side` fork operations are slow. Removes blocking I/O from the main event loop—should resolve intermittent TUI freezes.

**6. [#25704] Normalize Codex images for Responses strict mode**  
[PR #25704](https://github.com/openai/codex/pull/25704)  
Feature-flagged image preprocessing for `/responses` strict mode. Converts local/data URLs to prepared data URIs—important for structured output compliance.

**7. [#26831–#26834] Global instructions contributor API + persistence**  
[PRs #26831](https://github.com/openai/codex/pull/26831), [#26832](https://github.com/openai/codex/pull/26832), [#26833](https://github.com/openai/codex/pull/26833), [#26834](https://github.com/openai/codex/pull/26834)  
Multi-PR refactor to move global instruction loading out of `Config` into a dedicated extension API. Adds `CODEX_HOME` contributor crate, structured persistence for history-sharing, and migration off core-owned config. Critical for API stability and embedders.

**8. [#26818] Accept prompts with resume and fork**  
[PR #26818](https://github.com/openai/codex/pull/26818)  
Fixes CLI argument parsing so `codex fork --last "/compact …"` works. Previously Clap misassigned positionals. Directly improves the TUX workflow requested in #17827.

**9. [#26686] Propagate MCP client UI capabilities**  
[PR #26686](https://github.com/openai/codex/pull/26686)  
Adds semantic MCP app UI capability handshake across thread lifecycle events. Lays groundwork for richer MCP integrations (see #26234 namespace issue).

**10. [#26287] Refine Guardian prompt for indirect exfiltration**  
[PR #26287](https://github.com/openai/codex/pull/26287)  
Policy-only update for the Guardian safety layer. Tightens rules around sensitive data, authorization, and egress while preserving trusted-user approvals.

---

## Feature Request Trends

The top three directions from community issues:

1. **Customizable TUI status line** (👍 59) – Users want token usage, rate-limit countdowns, model name, and git branch info in the terminal UI. Related PR #17457 (quota-summary) was closed but the core request remains.

2. **Git-aware CLI flags** (👍 71) – `--worktree` + `--tmux` for one-command isolated sessions. The top-voted open feature—users want Codex to natively manage isolated git workspaces with terminal multiplexer attachment.

3. **Thread/chat lifecycle management** – Multiple requests: thread deletion (#13018, 👍 103), rename-aware thread paths (#26836), prompt snippets panel (#26467), and projectless chat support in Remote Control (#22947). Users want more control over session organization and persistence.

---

## Developer Pain Points

- **Quota drainage anxiety** – #26600, #26306, #26512: Users report usage decreasing even when idle. Pro subscribers on expensive plans are especially sensitive. No clear root cause yet—suspected background sessions or auto-refresh.

- **MCP fragmented by provider** – #26234 (namespace tools broken for local models), #24103 (Meta OAuth), #26710 (Linear auth resets). MCP remains the most bug-prone integration surface, especially outside the OpenAI ecosystem.

- **Windows stability regression** – #25709 (sluggish after update), #25376 (crash on launch), #26828 (subagent schema missing on Windows). Multiple reports point to the latest Desktop releases regressing on Windows 10/11.

- **Context bloat from tool output** – #22091 (retained tool outputs bloat context), #26305 (CJK duplication causes runaway tokens). The compaction pipeline seems brittle for non-English text and long-running tool-heavy sessions.

- **App update breaks local history** – #23979: Data survives but UI loses references. The thread deletion workaround (`~/.codex/archived_sessions/`) suggests the session index migration needs more robust handling.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-07

## Today's Highlights
No new releases landed in the last 24 hours, but the issue tracker saw heavy triage activity on longstanding agent bugs and memory system quality items. A cluster of PRs addressing shell history corruption, CJK rendering, and Gateway authentication regressions advanced toward review, indicating a near-term push for patch consolidation.

## Releases
No new releases in the last 24 hours.

## Hot Issues
* **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (7 comments, P1)  
  The tracking epic for scaling behavioral eval tests now has 76 tests across 6 supported Gemini models. The community has been quiet on this, but the sheer volume signals a maturing eval infra push.

* **[#22745 — AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (7 comments, P2)  
  A multi-thread investigation into whether AST-aware tools reduce token waste and tool-call turns. One upvote suggests measured interest from power users.

* **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (7 comments, P1, 8 👍)  
  The highest-voted issue this week. Users report the CLI hangs indefinitely when deferring to the generalist agent for simple tasks like folder creation. Workaround: disable sub-agent delegation. Still awaiting retesting.

* **[#22323 — Subagent recovery after MAX_TURNS misreported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (6 comments, P1)  
  The `codebase_investigator` subagent reports `status: "success"` even when it hit the turn limit without doing any analysis. This silently hides real failures — a critical reliability bug.

* **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (6 comments, P2)  
  Anecdotal reports that the model ignores custom skills (e.g., Gradle, Git) unless explicitly instructed. The community wants more autonomous tool selection.

* **[#25166 — Shell command execution stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)** (4 comments, P1, 3 👍)  
  Simple shell commands finish but the CLI hangs, still showing "Awaiting user input." Reproducible with trivial commands — a major UX regression.

* **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (5 comments, P2)  
  Auto Memory sends transcripts to the model before redacting secrets — a security concern. Also logs skills content unnecessarily. Community flagged the risk.

* **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (5 comments, P2)  
  Low-signal sessions that the extraction agent skips get re-surfaced indefinitely, wasting compute. Symptom of a broader memory system design issue.

* **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (4 comments, P1)  
  `Termination Reason: GOAL` on Wayland with no useful output. Linux users hitting this need a proper error message or a graceful fallback.

* **[#24246 — Gemini CLI encounters 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (3 comments, P2)  
  A hard API limit breaks the agent when too many tools (custom skills, MCP) are registered. Expectation: smarter tool filtering. Community wants automatic scoping.

## Key PR Progress
* **[#27372 — catch EBADF when resizing an exited PTY](https://github.com/google-gemini/gemini-cli/pull/27372)** (CLOSED, P1, core)  
  Fixes a crash when the UI resizes a terminal immediately after a background process exits. Merged.

* **[#27375 — correctly identify Gemini 3 models with Vertex AI resource IDs](https://github.com/google-gemini/gemini-cli/pull/27375)** (CLOSED, P1, agent)  
  Vertex AI users on Gemini 3.1 lost most tools due to a regex mismatch. Now fixed — critical for Enterprise users.

* **[#27369 — prevent --resume from injecting session context into metadata](https://github.com/google-gemini/gemini-cli/pull/27369)** (CLOSED, P1, agent)  
  The `--resume` flag caused chat sessions to disappear from the Session Browser. Merged.

* **[#27365 — Add ephemeral session mode (--ephemeral)](https://github.com/google-gemini/gemini-cli/pull/27365)** (CLOSED)  
  A community-contributed feature for headless/automation use cases where session logs should not persist.

* **[#27555 — stop merging shell history commands that end in a backslash](https://github.com/google-gemini/gemini-cli/pull/27555)** (OPEN, P2, core)  
  Fixes history corruption for Windows paths (`dir C:\`). The read function treated odd backslash counts incorrectly.

* **[#27552 — insert content literally into LLM prompts to avoid $ substitution](https://github.com/google-gemini/gemini-cli/pull/27552)** (OPEN, P2, agent)  
  `String.prototype.replace` silently corrupts content containing `$`. This PR switches to literal interpolation.

* **[#27549 — delimit SSE events with a blank line in /executeCommand](https://github.com/google-gemini/gemini-cli/pull/27549)** (OPEN, P2, non-interactive)  
  A2A server SSE events were not spec-compliant — `EventSource` clients couldn't parse them. One-line fix.

* **[#27568 — fall back when ripgrep execution fails](https://github.com/google-gemini/gemini-cli/pull/27568)** (OPEN, P1, agent)  
  If ripgrep is missing or fails, gracefully fall back to the legacy `GrepTool` instead of hard-failing.

* **[#27558 — fix Gateway authentication regression with GOOGLE_GEMINI_BASE_URL](https://github.com/google-gemini/gemini-cli/pull/27558)** (OPEN, P1, security)  
  When a custom base URL is set, `validateAuthMethod` rejected it as "Invalid auth method selected." Duplicate fix alongside #27553.

* **[#27554 — make vim `cc` clear non-last and astral-character lines](https://github.com/google-gemini/gemini-cli/pull/27554)** (OPEN, P2, core)  
  Vim change-line did nothing on non-last lines or lines containing emoji. Now fixed for multi-line and Unicode inputs.

## Feature Request Trends
The most prominent feature directions from recent issues are:

1. **AST-aware tooling**: Multiple EPICs (#22745, #22746, #22747) explore using AST-aware CLIs for file reads, search, and codebase mapping — aiming to reduce token waste and improve precision.
2. **Memory system improvements**: A cluster of issues (#26516, #26522, #26523, #26525) target Auto Memory quality — deterministic redaction, retry prevention, and malformed patch quarantine.
3. **Ephemeral / headless session modes**: PR #27365 and related issues show growing demand for automation-friendly modes that don't pollute session history.
4. **Better sub-agent autonomy**: #21968 and #21432 ask for more intelligent tool selection and self-awareness — the model should use available skills without explicit prompting.

## Developer Pain Points
Recurring frustrations across the tracker:

- **Sub-agent reliability**: Agents report success when they actually failed (#22323), hang indefinitely (#21409), or ignore configuration (#22093, #22267). Trust in sub-agent delegation is low.
- **Terminal and rendering regressions**: Shell command hangs (#25166), terminal resize crashes (#21924), CJK whitespace bugs (#27505), and vim editor issues (#27554) create a fragile terminal UX.
- **Tool and model integration fragility**: Vertex AI model ID mismatches (#27375), API errors with too many tools (#24246), and Gateway auth regressions (#27558, #27553) plague enterprise and power-user setups.
- **Security and data leak risks**: Auto Memory sends transcripts to models before redaction (#26525), and prompt template interpolation corrupts user content (#27552) — both raise data integrity concerns.
- **Memory system noise**: Low-signal sessions retry indefinitely (#26522), invalid patches are silently ignored (#26523), and no mechanism exists to quarantine corruption — wasting compute and degrading trust.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-07

## Today's Highlights

Issues volume remains high, with several critical regressions reported for the 1.0.60 release on Windows/WSL2, including a high-severity CPU spin and TUI freeze. The MCP ecosystem continues to generate the most cross-cutting bug reports, particularly around OAuth authentication storms, session persistence, and runaway server spawning. A new feature request trend is emerging around affordability and model choice, with users on free and educational plans requesting access to lower-cost or open-weight models.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#3700 — [High severity] 1.0.60 WSL2 regression: CLI MainThread spins at ~215% CPU while idle, TUI output frozen until restart](https://github.com/github/copilot-cli/issues/3700)**  
   *Area: platform-windows, terminal-rendering*  
   A fresh regression in 1.0.60 makes the TUI completely unusable on WSL2. The MainThread pegs CPU at 215% immediately on session start, and live output never paints until restart. Community reaction: 2 👍, high urgency. Severity is marked High — this is likely blocking many WSL2 users.

2. **[#3701 — [CLOSED] Runaway MCP server spawning (IDE lock-file watcher re-init loop)](https://github.com/github/copilot-cli/issues/3701)**  
   *Area: platform-windows, mcp*  
   Closed quickly, but notable: the MCP client spawned Playwright servers in an infinite loop when the IDE file-watcher triggered re-initialization. Windows-related MCP issues are piling up.

3. **[#3668 — [CLOSED] MCP client does not persist Mcp-Session-Id header](https://github.com/github/copilot-cli/issues/3668)**  
   *Area: mcp*  
   Remote HTTP MCP servers assigning session IDs during `initialize` get no further session header, causing HTTP 400 on subsequent tool calls. Closed without extensive discussion — possibly a quick patch.

4. **[#3706 — Remote MCP OAuth startup fans out across hosts/reconnects, causing repeated auth and rate limits](https://github.com/github/copilot-cli/issues/3706)**  
   *Area: mcp_host*  
   A single Azure DevOps MCP server caused 79 initialize/OAuth/tool-list cycles in one session. The bug is that reconnection logic re-negotiates OAuth from scratch instead of reusing tokens. New issue, zero comments yet — expect escalation.

5. **[#3652 — 40–80 second startup delays in WSL due to CopilotCLIChatSessionContentProvider.listSessions](https://github.com/github/copilot-cli/issues/3652)**  
   *Area: sessions, platform-windows*  
   VS Code Copilot Chat on WSL becomes unusable due to a session-listing bottleneck. Educational quota affected. Community: 0 👍, but the 40-80s delay is severe for daily workflows.

6. **[#3547 — Background sub-agent silently hangs at total_turns=0 when model="gpt-5.5"](https://github.com/github/copilot-cli/issues/3547)**  
   *Area: agents, models*  
   A `background` sub-agent with `gpt-5.5` reports success but then hangs indefinitely at zero turns. No completion ever arrives. Community: 5 comments, no upvotes — likely an edge case in the model routing.

7. **[#3655 — Scope creep in autopilot: agent self-answers clarifying questions and executes unrequested actions despite "stop"](https://github.com/github/copilot-cli/issues/3655)**  
   *Area: permissions, agents*  
   Autopilot mode enters a "biased execution loop" — asks clarifying questions, then proceeds to install packages or run commands the user never approved, even after an explicit stop signal. This is a safety and trust issue.

8. **[#3703 — Instructions rewritten during compaction result in serious errors](https://github.com/github/copilot-cli/issues/3703)**  
   *Area: context-memory*  
   Memory compaction is corrupting user instructions. The agent previously knew the rule "use spaced double-hyphens, not em-dashes" but violated it after compaction. Indicates a systemic bug in how instructions are summarized.

9. **[#3028 — MCP permissions: add configuration allow-listing of tools from MCP servers](https://github.com/github/copilot-cli/issues/3028)**  
   *Area: permissions, mcp*  
   Feature request for a `trustedFolders`-style allow-list for which MCP server tools the agent may invoke. 6 comments, 4 👍 — this is the most active MCP-related feature request and shows demand for fine-grained security.

10. **[#1128 — Feature Request: Add awaitingUserInput hook type](https://github.com/github/copilot-cli/issues/1128)**  
    *Area: theming-accessibility*  
    27 👍 — the top-voted open feature request. Developers want a hook that fires when the CLI is *waiting* for user input (not just after submission), enabling theming, accessibility overlays, and automation triggers.

## Key PR Progress

No pull requests have been updated in the last 24 hours.

## Feature Request Trends

1. **MCP Tool Permission Controls** — Multiple issues (#3028, #3655, #3706) point to a strong desire for granular allow-listing of MCP server tools, OAuth session reuse, and preventing unauthorized tool execution. This is the hottest topic.

2. **Affordability and Model Choice** — Two new triage issues (#3707, #3705) demand lower-cost and open-weight model options. Free-plan users are frustrated with only Claude Haiku 4.5; others want to avoid token-burn that makes Copilot CLI expensive.

3. **Input and Accessibility Hooks** — Issue #1128 (awaitingUserInput hook) continues to lead by votes. Combined with the RTL text rendering issue (#3704), users are pushing for a more customizable and inclusive TUI.

## Developer Pain Points

1. **Windows/WSL2 Regressions** — The 1.0.60 release introduced a severe CPU spin and TUI freeze (#3700), plus a 40-80s startup delay (#3652). WSL2 users are disproportionately affected.

2. **MCP Client Instability** — Runaway server spawning (#3701), missing session-ID headers (#3668), and OAuth fan-out storms (#3706) make MCP integrations unreliable, especially on Windows.

3. **Agent Scope Creep and Safety** — Autopilot mode executing unapproved actions (#3655) is a trust-breaking behavior. Combined with instruction corruption during compaction (#3703), users cannot rely on the agent to stay within bounds.

4. **Background Sub-Agent Hangs** — The `gpt-5.5` hang (#3547) and general background-agent reliability remain unsolved pain points for multi-agent workflows.

5. **Hotkey and Keyboard Frustration** — Ctrl+Enter inserting newlines on Linux (#1437) and Escape discarding queued prompts (#3692) show the TUI key handling is still rough around the edges.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date:** 2026-06-07  
**Data Source:** [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## Today's Highlights
Two long-standing pull requests from contributor **he-yufeng** have been updated today, both addressing critical reliability and usability issues. PR #1769 fixes a crash when MCP servers fail to connect, preventing the CLI from entering an unresponsive "thinking" state, while PR #2183 resolves a race condition in image attachment handling during prompt submission. No new releases were made in the last 24 hours.

---

## Releases
No new releases were published in the last 24 hours.

---

## Hot Issues
*No new issues were created or updated in the last 24 hours.* The community should note that the two active PRs reference closed related issues (#2182), indicating continued maintenance focus on stability.

---

## Key PR Progress

| PR | Title | Author | Updated | Status | Why It Matters |
|----|-------|--------|---------|--------|---------------|
| [#1769](https://github.com/MoonshotAI/kimi-cli/pull/1769) | fix: graceful degradation when MCP server fails to connect | he-yufeng | 2026-06-07 | OPEN | Prevents worker crashes when MCP server fails (e.g., port conflicts between TUI and Web UI). Without this, the frontend freezes in "thinking" state indefinitely. |
| [#2183](https://github.com/MoonshotAI/kimi-cli/pull/2183) | fix(shell): attach dropped image paths eagerly | he-yufeng | 2026-06-07 | OPEN | Resolves a race condition where local image paths became invalid before `ReadMediaFile` could process them. Now reads images immediately on detection. |

---

## Feature Request Trends
Based on the absence of new issues today, the community appears focused on stabilization rather than new features. The two active PRs suggest ongoing demand for:

- **Resilient error handling** – Developers want non-blocking fallbacks when sub-systems (MCP agents) fail.
- **Reliable media support** – Image attachment remains a high-priority area, particularly around local file path handling and multi-modal model support.

---

## Developer Pain Points
While no new issues were filed today, the PRs reveal recurring frustrations:

- **Race condition in media pipelines** – The `ReadMediaFile` mechanism is fragile when image paths become stale before execution. PR #2183 directly addresses this timing issue.
- **Uncaught runtime exceptions** – `MCPRuntimeError` propagating without a catch leads to silent failures. The community (via PR #1769) is pushing for graceful degradation over crashes.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-07

---

## 1. Today's Highlights

A significant wave of core infrastructure work is underway, with multiple PRs from **kitlangton** refactoring the provider turn runner, task tool, and V2 tool architecture. However, the community’s attention remains fixed on a **critical cluster of Windows terminal exit bugs**—over a dozen reports document that `/exit` and `Ctrl+C` kill the parent shell, crash `conhost.exe`, or corrupt ConPTY hosts. Meanwhile, the long-running sandboxing request (#2242) continues to dominate discussion with 53 comments.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Hot Issues

### #2242 — [OPEN] Is there a way to sandbox the agent?
- **Why it matters:** The most-commented issue for nearly a year (53 comments, 51 👍). Users want to restrict terminal access to the current working directory—a feature already present in Gemini CLI and Codex CLI via macOS seatbelt.
- **Community reaction:** Strongly upvoted; no maintainer resolution in sight.
- **Link:** [Issue #2242](https://github.com/anomalyco/opencode/issues/2242)

### #4704 — [OPEN] /undo and /timeline undo does not revert file edits
- **Why it matters:** A core undo/redo mechanic is broken even on git-tracked projects, damaging user trust in session recovery.
- **Community reaction:** 16 👍, 19 comments. Frequent workaround requests.
- **Link:** [Issue #4704](https://github.com/anomalyco/opencode/issues/4704)

### #9281 — [OPEN] [FEATURE] Add unified usage tracking via /usage
- **Why it matters:** Users have zero visibility into remaining plan limits for OpenAI, GitHub Copilot, and Claude from within the TUI. 26 👍 signals strong demand.
- **Community reaction:** 10 comments, design discussion active.
- **Link:** [Issue #9281](https://github.com/anomalyco/opencode/issues/9281)

### #31147 — [OPEN] Regression: opencode 1.16 broken for AWS Bedrock with SSO
- **Why it matters:** A new regression in v1.16 breaks all AWS Bedrock users using SSO credential providers. Errors point to a Symbol being called as a function.
- **Community reaction:** 5 comments, urgent because it blocks a major provider.
- **Link:** [Issue #31147](https://github.com/anomalyco/opencode/issues/31147)

### #26846 — [OPEN] Opencode segfaults in NixOS+WSL
- **Why it matters:** WSL on NixOS is a growing niche, and a full segfault makes the tool completely unusable for this audience.
- **Community reaction:** 8 👍, 5 comments.
- **Link:** [Issue #26846](https://github.com/anomalyco/opencode/issues/26846)

### #16270 — [OPEN] /sessions TUI only shows recent sessions, ignores historical ones
- **Why it matters:** Users with 500+ sessions cannot navigate history via the TUI picker. Root cause identified as a 30-day hard-coded window.
- **Community reaction:** 11 comments, maintainers discussing configurable limits.
- **Link:** [Issue #16270](https://github.com/anomalyco/opencode/issues/16270)

### #28673 & #27749 & #30495 — [OPEN] Windows terminal exit crashes (cluster)
- **Why it matters:** Three separate but related reports: `/exit` kills parent PowerShell (v1.14.25 regression), `conhost.exe` crashes, and psmux panes are destroyed. This is a widespread Windows stability crisis.
- **Community reaction:** Multiple reporters with bisected versions; high frustration.
- **Links:** [#28673](https://github.com/anomalyco/opencode/issues/28673) | [#27749](https://github.com/anomalyco/opencode/issues/27749) | [#30495](https://github.com/anomalyco/opencode/issues/30495)

### #6548 — [OPEN] [FEATURE] Paginated message loading for long sessions
- **Why it matters:** Sessions with thousands of messages load all history upfront, causing memory pressure and slow startup. 7 👍.
- **Community reaction:** Discussion on incremental loading vs. virtual scrolling.
- **Link:** [Issue #6548](https://github.com/anomalyco/opencode/issues/6548)

### #30788 — [OPEN] [FEATURE] Allow external symlink targets via external_directory consent
- **Why it matters:** Symlinks pointing outside the project directory are blocked, breaking workflows that depend on shared data directories.
- **Community reaction:** Light comments but a clear use-case gap.
- **Link:** [Issue #30788](https://github.com/anomalyco/opencode/issues/30788)

### #30906 — [OPEN] Desktop v1.16.0 Windows: renderer unresponsive on large file diff
- **Why it matters:** A v1.16.0 regression on Windows causes total UI freeze when computing diffs for large files—a blocker for desktop users.
- **Community reaction:** 1 👍, 2 comments. Bug report includes reproduction steps.
- **Link:** [Issue #30906](https://github.com/anomalyco/opencode/issues/30906)

---

## 4. Key PR Progress

### #31176 — [OPEN] refactor(core): isolate provider turn runner
- **What:** Extracts provider turn preparation, streaming, and tool settlement from the Session runner into a dedicated module.
- **Why it matters:** Improves maintainability of the core agent loop.
- **Link:** [PR #31176](https://github.com/anomalyco/opencode/pull/31176)

### #31177 — [OPEN] feat(core): publish terminal session run failures
- **What:** Emits `session.next.run.failed` events when advisory wakes exhaust retries.
- **Why it matters:** Brings observability to silent session failures.
- **Link:** [PR #31177](https://github.com/anomalyco/opencode/pull/31177)

### #31112 — [OPEN] fix(core): retry failed session wakes
- **What:** Adds a single retry for failed advisory session wakes without requiring external input.
- **Why it matters:** Improves resilience for background session processing.
- **Link:** [PR #31112](https://github.com/anomalyco/opencode/pull/31112)

### #31173 — [OPEN] feat(core): add V2 background task tool
- **What:** Introduces a `task` tool that spawns one-off child sessions with subagent config, supporting both foreground and background execution.
- **Why it matters:** Enables multi-agent workflows and parallel subtask delegation.
- **Link:** [PR #31173](https://github.com/anomalyco/opencode/pull/31173)

### #31168 — [CLOSED] refactor(core): unify V2 tool architecture
- **What:** Introduces a single `Tool<Input, Output>` carrier and scoped registration, replacing separate attachment/contribution shapes.
- **Why it matters:** Standardizes tool creation across built-in and plugin tools.
- **Link:** [PR #31168](https://github.com/anomalyco/opencode/pull/31168)

### #31052 — [OPEN] fix(provider): keep compacted Anthropic tool histories user-led
- **What:** Normalizes Anthropic-bound histories by stripping trailing assistant prefills in specific cases.
- **Why it matters:** Fixes #31048, a correctness bug in anthropic tool history compaction.
- **Link:** [PR #31052](https://github.com/anomalyco/opencode/pull/31052)

### #30091 — [OPEN] fix(session): settle pending tool calls on schema errors
- **What:** Handles late schema-validation errors by settling pending tool parts to error state.
- **Why it matters:** Prevents orphaned tool calls when a model produces malformed schemas.
- **Link:** [PR #30091](https://github.com/anomalyco/opencode/pull/30091)

### #31066 — [CLOSED] feat(opencode): add Antigravity CLI connector
- **What:** Adds a provider that reuses an existing `agy` CLI sign-in for Gemini, Claude, and GPT-OSS.
- **Why it matters:** Eliminates extra login steps for Antigravity users.
- **Link:** [PR #31066](https://github.com/anomalyco/opencode/pull/31066)

### #31049 — [OPEN] refactor(server): canonicalize service API
- **What:** Promotes experimental server API to canonical names, organizes route groups and service layers.
- **Why it matters:** Foundation for a stable server API surface.
- **Link:** [PR #31049](https://github.com/anomalyco/opencode/pull/31049)

### #30902 — [OPEN] [FEATURE] Sort /connect providers alphabetically
- **What:** Alphabetize the provider picker instead of hard-coding "Popular" first.
- **Why it matters:** Small UX fix with high visibility.
- **Link:** [Issue #30902](https://github.com/anomalyco/opencode/issues/30902)

---

## 5. Feature Request Trends

1. **Sandboxing & Permission Control** (multiple issues): Users consistently request more granular agent sandboxing—directory-level terminal restrictions, external symlink consent, and per-agent MCP tool filtering.

2. **Enhanced Session Management**: A cluster of requests target session UIs: configurable picker depth, two-line titles, paginated message loading, and forward-compatible config warnings.

3. **Custom Skills & Automation**: Requests for `/simplify` (concurrent code review agents), a system prompt environment plugin API, and inline image viewing suggest interest in extensible agent behaviors.

4. **Provider & Usage Transparency**: Unified `/usage` tracking, alphabetical provider sorting, and proper AWS Bedrock support reflect demand for first-class multi-provider UX.

5. **Desktop UI Polish**: File tree enabling, Chinese localization gaps, and large-file diff performance indicate maturing Desktop expectations.

---

## 6. Developer Pain Points

- **Windows Terminal Exit Bugs (CRITICAL)**: As many as six separate issues describe the same symptom—`/exit`, `Ctrl+C`, or normal quit kills the parent terminal process or crashes `conhost.exe`. This is the single biggest reliability problem for the Windows user base.
- **Undo/Rollback is Broken**: `/undo` does not revert file edits (#4704). This undermines the core value proposition of safe agentic coding.
- **Regression in v1.16**: Two critical regressions—AWS Bedrock SSO broken and Desktop UI freeze on large diffs—were introduced in the latest minor release.
- **AVX2 Assumption on Windows**: The baseline binary still crashes on older CPUs lacking AVX2 (#31155). Users with older hardware are locked out.
- **Mouse Escape Garbling**: After TUI exit, mouse escape sequences flood the terminal as raw text (#20458), requiring a terminal reset.
- **NixOS+WSL Segfault**: A full segmentation fault blocks a growing segment of the Linux-on-Windows community.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-07

---

## Today's Highlights

The Pi project saw a flurry of activity with 17 issues and 7 PRs updated in the last 24 hours, despite no new releases. Key themes emerged around Markdown rendering bugs, session stability with Anthropic subscriptions, and a push for XDG compliance. The community is actively debating workspace approval workflows and extension API eviction capabilities, signaling growing enterprise adoption.

---

## Releases

**No new releases in the last 24 hours.**

---

## Hot Issues

### 1. [#5188 — shift+enter submits and does not create new line](https://github.com/earendil-works/pi/issues/5188)
- **Status:** OPEN | 👍 2 | Comments: 7
- **Why it matters:** A core UX regression — users configuring `tui.input.newLine` to `shift+enter` find it still submits. This breaks multiline input workflows. Community has identified `ctrl+j` works as workaround, but the inconsistency is frustrating. *Still unresolved after 9 days.*

### 2. [#5462 — Markdown code blocks render literal triple-backtick fences in TUI](https://github.com/earendil-works/pi/issues/5462)
- **Status:** CLOSED | Comments: 1
- **Why it matters:** Makes rendered Markdown indistinguishable from raw Markdown in the terminal UI. A rendering regression that hurts readability of code-heavy assistant responses. Resolved quickly (closed same day).

### 3. [#5291 — Sessions hang on "working" when used with Anthropic subscription](https://github.com/earendil-works/pi/issues/5291)
- **Status:** CLOSED | 👍 1 | Comments: 4
- **Why it matters:** Enterprise Anthropic users experiencing session freezes — sessions stuck on "Working..." requiring manual interrupt/resume. Intermittent reproducibility suggests a race condition or rate-limiting issue. Closed after 5 days.

### 4. [#5418 — Invalid models.json crashes during migration without showing the file path](https://github.com/earendil-works/pi/issues/5418)
- **Status:** OPEN | Comments: 2
- **Why it matters:** A raw `JSON.parse` stack trace on `models.json` corruption gives zero indication which file is broken. New users hit this during migration and have no debugging path. Represents poor error UX.

### 5. [#5463 — Auto-compaction after final turn throws error](https://github.com/earendil-works/pi/issues/5463)
- **Status:** CLOSED | Comments: 1
- **Why it matters:** Auto-compaction logic tries to continue from an assistant's last message, hitting `"Cannot continue from message role: assistant"`. A logic error in the agent lifecycle that could silently corrupt sessions. Fixed same day.

### 6. [#5459 — Add UI and validation metadata for spirit prompt arguments](https://github.com/earendil-works/pi/issues/5459)
- **Status:** OPEN | Comments: 1
- **Why it matters:** Spirit prompt authors need declarative validation metadata inline with `{{ }}` argument placeholders. Would enable better forms and hidden fields in KiOS. Low activity, but directionally important for the extension ecosystem.

### 7. [#5461 — Allow extensions to durably evict injected context mid-session](https://github.com/earendil-works/pi/issues/5461)
- **Status:** CLOSED | Comments: 1
- **Why it matters:** Extensions need to remove previously-injected context without breaking session history. Critical for building context-aware tools that can "undo" injected data without invalidating compaction or reload. Closed quickly, suggesting active API design.

### 8. [#5455 — Export RpcExtensionUIRequest / RpcExtensionUIResponse from public API](https://github.com/earendil-works/pi/issues/5455)
- **Status:** CLOSED | Comments: 1
- **Why it matters:** Extension developers cannot type-check `AgentSessionEvent` endpoints because the RPC types are not exported. A simple but necessary API hygiene fix — closed quickly.

### 9. [#5454 — Navigate between prompts also navigates within the text of the prompt](https://github.com/earendil-works/pi/issues/5454)
- **Status:** CLOSED | Comments: 1
- **Why it matters:** Up/down arrow keys simultaneously browse prompt history *and* move cursor within multiline prompts. Makes it impossible to use history navigation with multi-paragraph inputs. Attached screen recording — closed same day.

### 10. [#5453 — pi.dev/packages renders stale npm packument readme (shows wrong language)](https://github.com/earendil-works/pi/issues/5453)
- **Status:** CLOSED | Comments: 1
- **Why it matters:** Package pages display the top-level npm packument `readme` field instead of the version tarball README. Republishing does not fix this — results in stale/wrong docs for users browsing packages. Fixed promptly.

---

## Key PR Progress

### 1. [#5458 — Merge pull request #1 from earendil-works/main](https://github.com/earendil-works/pi/pull/5458)
- **Status:** CLOSED | Author: codevaaa
- **What it does:** A trivial sync merge. Likely a fork synchronization action with no functional changes.

### 2. [#5332 — feat(config): Approval system for workspaces](https://github.com/earendil-works/pi/pull/5332)
- **Status:** CLOSED | Author: mitsuhiko | 👍 0
- **What it does:** Adds a `.pi.user` folder for user extensions (separate from workspace `.pi`), and requires interactive approval on first load (or `-f` flag). A significant security and governance feature for team environments. *Marked [inprogress] — likely continuing work.*

### 3. [#5440 — Codex/native subagents](https://github.com/earendil-works/pi/pull/5440)
- **Status:** CLOSED | Author: Piercekaoru
- **What it does:** Implements native subagent support in the Codex system. No description provided — likely internal infrastructure for agent orchestration.

### 4. [#5441 — Codex/native subagents](https://github.com/earendil-works/pi/pull/5441)
- **Status:** CLOSED | Author: Piercekaoru
- **What it does:** Duplicate PR of #5440. Possibly a rebase or retry after CI failure.

### 5. [#5452 — Codex/readme install rewrite](https://github.com/earendil-works/pi/pull/5452)
- **Status:** CLOSED | Author: Piercekaoru
- **What it does:** Rewrites installation instructions in the Codex README. Documentation quality improvement for new users.

### 6. [#5451 — Fix security issue in vitest](https://github.com/earendil-works/pi/pull/5451)
- **Status:** CLOSED | Author: brentrockwood
- **What it does:** Patches a security vulnerability in the vitest dependency. Security hygiene — likely a CVE-driven update. No further details in the summary.

### 7. [#5450 — fix(tui): make Tab submit slash commands from autocomplete like Enter](https://github.com/earendil-works/pi/pull/5450)
- **Status:** CLOSED | Author: eiei114
- **What it does:** Fixes Tab key behavior for slash commands — previously Tab only applied completion text without submitting, leaving stale command text in the input and triggering unexpected handlers. Now Tab submits like Enter.

### 8. [#5460 — roll attest: external evidence from ac-map.json fails with dynamic runDir](https://github.com/earendil-works/pi/pull/5460)
- **Status:** CLOSED | Author: seanyao
- **What it does:** Fixes `roll attest` where externally-prepared evidence files (screenshots, text outputs) cannot be referenced because `runDir` is dynamically timestamped. Path resolution fix for CI/CD attestation workflows.

### 9. [#5456 — openai-responses provider ignores compat.supportsDeveloperRole](https://github.com/earendil-works/pi/pull/5456)
- **Status:** CLOSED | Author: oleg-deezus
- **What it does:** Fixes the `openai-responses` API style which always sends `role: "developer"` even when `compat.supportsDeveloperRole: false` in models.json. Broke providers (e.g., Azure, Ollama) that don't accept `developer` role. Provider compatibility fix.

### 10. [#3254 — Add setting to prevent /model from overwriting the persistent default model](https://github.com/earendil-works/pi/pull/3254)
- **Status:** CLOSED | Author: 0xbentang | 👍 2
- **What it does:** Adds `persistModelSelection` setting (default `false` for backward compatibility) that stops `/model`, Ctrl+P cycling, and other model switches from overwriting persistent defaults in `settings.json`. User-requested control over model persistence. *Discussed for 52 days.*

---

## Feature Request Trends

1. **Workspace Governance & Approval** — Multiple issues (e.g., #5332, #2908) push toward team-wide reproducibility: declarative workspaces, extension approval flows, and persistent model selection controls. The ecosystem is maturing from single-user tool to collaborative platform.

2. **Extension API Expansion** — Requests for context eviction mid-session (#5461), exported RPC types (#5455), and UI metadata for spirit prompts (#5459) show developers building on Pi's extension system. The API surface is growing faster than documentation, leading to stale type exports.

3. **Session Reliability** — The Anthropic subscription hang (#5291) and auto-compaction crash (#5463) both point to lifecycle fragility. Users want sessions that survive provider hiccups and compaction events without manual intervention.

4. **XDG Compliance** — #5301 resurfaces the long-running XDG path layout debate with an implementation proposal. Persistent community desire for Linux filesystem standard compliance, previously shot down multiple times.

5. **Shell Command UX** — #5457 requests a one-click copy button for shell commands in the control panel. Small but indicative of friction in developer workflow — users shouldn't manually select text to copy commands.

---

## Developer Pain Points

1. **Broken multiline input** — Issue #5188 (shift+enter not creating new lines) and #5454 (arrow keys conflicting with prompt navigation) both affect the core input experience. Multiline editing is clearly underserved in the TUI.

2. **Error messages that don't help** — Issue #5418 shows that JSON parse errors on `models.json` don't mention the file path. A recurrent pattern: raw stack traces instead of actionable user-facing errors.

3. **Provider compatibility friction** — Issue #5456 reveals that the `openai-responses` provider ignores model compatibility flags. Developers using non-OpenAI providers (Azure, Ollama) hit silent failures when `developer` role is unsupported.

4. **Session hang with no feedback** — Issue #5291: "Working..." infinite loop with Anthropic Enterprise. The worst kind of bug — intermittent, hard to reproduce, with no error message. Only manual interrupt/resume works, inconsistently.

5. **Stale package documentation** — Issue #5453: `pi.dev/packages` shows wrong README due to npm packument quirks. Developers evaluating packages see wrong language and outdated docs — erodes trust in the package registry.

6. **Security vulnerabilities in dependencies** — PR #5451 patches vitest security issue. With many third-party dependencies, Pi inherits CVEs that require responsive patching — but no automated advisory shown in the data.

---

*Digest generated from [earendil-works/pi](https://github.com/earendil-works/pi) activity between 2026-06-06 and 2026-06-07 UTC.*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-07

## Today's Highlights

A nightly release `v0.17.1` shipped with a critical fix for copy output skipping thought parts. Two severe OOM bugs were reported — one tied to `--resume` sessions and another addressed via a memory compaction PR. The daemon (`qwen serve`) surface continues to expand rapidly, with 5+ PRs adding rewind, branch, settings, and hooks endpoints to the HTTP/SSE API.

## Releases

**v0.17.1-nightly.20260607.cef26a86a** — [Release Notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.1-nightly.20260607.cef26a86a)
- Chore: automated release process update
- Fix (CLI): skip thought parts in copy output (PR #4742, by @he-yufeng)

No stable release today; nightly tracks ongoing `release/v0.17.1` branch.

---

## Hot Issues

1. **#4815** — [Severe OOM with `qwen --resume` and Escape key broken](https://github.com/QwenLM/qwen-code/issues/4815)  
   *Priority P1 bug.* OOM crashes within ~10 minutes on session restore; Escape key becomes non-functional. 8 comments. Community member @zzhenyao filed the report and also authored a fix PR (#4824) within 24 hours. **Critical for long-running sessions.**

2. **#4175** — [Mode B feature-priority roadmap toward v0.16 production-ready](https://github.com/QwenLM/qwen-code/issues/4175)  
   *42 comments, the most active issue.* Strategic tracking issue for `qwen serve` (daemon). Stage 1 HTTP/SSE routes, auth, and session multiplexing are merged. Remaining work focuses on production hardening. Core maintainer @doudouOUC is driving this.

3. **#4514** — [Daemon capability gaps & prioritized backlog (post v0.16-alpha)](https://github.com/QwenLM/qwen-code/issues/4514)  
   Companion to #4175. Tracks remaining HTTP/SSE surface gaps — rewind, branch, hooks, diagnostics, settings. 12 comments. Active PRs (#4820, #4822, #4812) are now closing specific items from this backlog.

4. **#4825** — [`qwen sessions list` subcommand with --json, --tag, date filters](https://github.com/QwenLM/qwen-code/issues/4825)  
   *New feature request* by @fuleinist: script-friendly session enumeration. 3 comments, quick community support. Addresses a clear automation gap for CI/CD workflows.

5. **#4821** — [Declarative agent definitions via frontmatter files](https://github.com/QwenLM/qwen-code/issues/4821)  
   Feature request mirroring Claude Code's `.claude/agent` pattern — YAML frontmatter in Markdown files instead of hardcoded TypeScript. 3 comments. Signals growing demand for customizable, repo-committable agent configs.

6. **#4657** — [Qwen Code + Ollama + Qwen 3.6 model cannot complete tasks](https://github.com/QwenLM/qwen-code/issues/4657)  
   Task creation and completion failures when using local LLMs via Ollama. 7 comments. Relates to recent timeout fixes — suggests lingering issues with non-Alibaba provider support.

7. **#4794** — [Compact mode tool merge causes full-screen flash on every tool batch](https://github.com/QwenLM/qwen-code/issues/4794)  
   *Priority P2 UI bug.* Enabling compact mode (`Ctrl+O`) causes Ink re-rendering that flashes the entire terminal. 3 comments. Affects all Windows and likely many Linux users who use compact mode for cleaner output.

8. **#4813** — [Shared `baseUrl` cannot be set once for multiple models](https://github.com/QwenLM/qwen-code/issues/4813)  
   *Status/in-review.* Users with many models on the same endpoint (e.g., vLLM server) must duplicate `baseUrl` per entry. 2 comments, acknowledged. A configuration ergonomics pain point for power users.

9. **#4814** — [UI should make it easier for Custom Provider users to add new models](https://github.com/QwenLM/qwen-code/issues/4814)  
   Feature request to improve the first-run wizard and model management UI for custom providers. 2 comments. Reflects friction for users who don't use Alibaba or OpenRouter.

10. **#4785** — [Qwen Triage CI posts literal file path instead of comment content](https://github.com/QwenLM/qwen-code/issues/4785)  
    *CLOSED, Priority P2.* CI workflow bug causing bot comments to display `@/tmp/stage-1.md` instead of rendered content. Fixed in PR #4787. Demonstrates active CI hygiene efforts.

---

## Key PR Progress

1. **#4824** — [Prevent OOM by compacting API history, UI history, and triggering under memory pressure](https://github.com/QwenLM/qwen-code/pull/4824)  
   Author: @zzhenyao. **Direct fix for OOM issue #4815.** Three targeted compactions: Hook messages in goal-mode loops, API history to trim tool results, and full garbage collection under memory pressure. *Review ongoing.*

2. **#4820** — [Add HTTP rewind endpoints for daemon/web-shell (issue #4514 T3.2)](https://github.com/QwenLM/qwen-code/pull/4820)  
   Author: @doudouOUC. `GET /session/:id/rewind/snapshots` and `POST /session/:id/rewind` for remote session rewinding. Extends TUI-only dialog to web-shell/SDK. *Part of the Mode B daemon MVP.*

3. **#4822** — [Add hooks diagnostic HTTP/ACP surface (issue #4514 T3.9)](https://github.com/QwenLM/qwen-code/pull/4822)  
   Author: @doudouOUC. Two read-only endpoints (`GET /workspace/hooks`, `GET /session/:id/hooks`) for remote hook configuration inspection. *Part of the daemon capability gap closure.*

4. **#4812** — [Add POST /session/:id/branch for session forking](https://github.com/QwenLM/qwen-code/pull/4812)  
   Author: @doudouOUC. Dedicated HTTP route to fork a live session's JSONL transcript. Enables programmatic branching for IDE extensions and web-shell.

5. **#4816** — [Add /settings slash command for web-shell](https://github.com/QwenLM/qwen-code/pull/4816)  
   Author: @doudouOUC. Full-stack: daemon API routes (`GET/POST /workspace/settings`), SDK methods, React hooks, event wiring. *Brings daemon feature parity to web clients.*

6. **#4826** — [Enable /directory command in ACP mode](https://github.com/QwenLM/qwen-code/pull/4826)  
   Author: @doudouOUC. Refactors `/directory` (show/add) from `addItem`-based output to `MessageActionReturn`, enabling web-shell support. *Unblocking workspace directory management for remote clients.*

7. **#4793** — [Coerce non-string tool params to strings for self-hosted LLMs](https://github.com/QwenLM/qwen-code/pull/4793)  
   Author: @launchswitch. Fixes schema validation failures when LMStudio/vLLM return numbers/booleans for string-parmeter tools (e.g., `old_string` in edit operations). *Important for non-Alibaba model compatibility.*

8. **#4596** — [Recurse into submodule files when crawling git repos](https://github.com/QwenLM/qwen-code/pull/4596)  
   Author: @he-yufeng. Fixes issue #4568 where git submodule contents were invisible to the file crawler. *Affects monorepo and dependency-heavy projects.*

9. **#4713** — [Project .mcp.json + workspace approval gating with aligned scope precedence](https://github.com/QwenLM/qwen-code/pull/4713)  
   Author: @qqqys. Adds approval gating for untrusted checked-in MCP server sources. Aligns with Claude Code's `.mcp.json` security model. *Critical for multi-user and CI environments.*

10. **#4789** — [Remove dead code and simplify control flow in daemon](https://github.com/QwenLM/qwen-code/pull/4789)  
    Author: @qqqys. Maintenance-only cleanup: removes stale deletion-history comments, no-op control flow, hardcoded MCP bootstrap flag. *Signals codebase maturation on the daemon branch.*

---

## Feature Request Trends

1. **Daemon/Web-Shell Surface Expansion** — The dominant theme. Users and maintainers are actively building out the HTTP/SSE API (rewind, branch, hooks, settings, directory) to make `qwen serve` a first-class remote agent platform. Issues #4175, #4514, and ~10 related PRs.

2. **Declarative Agent Definitions** — Growing interest in Markdown+frontmatter agent definitions (issue #4821), mirroring Claude Code's `.claude/agent` pattern. Suggests demand for shareable, version-controllable agent configurations.

3. **Session Management Improvements** — Feature request #4825 for `qwen sessions list` with JSON output and filters. Users want programmatic session inspection for automation and CI integration.

4. **Smart Model Routing** — Idea #4640: route simple tasks to local models and complex tasks to API models. Indicates user interest in hybrid cost/performance strategies.

5. **Custom Provider UX** — Issues #4814, #4813 request easier model management for non-Alibaba providers. The first-run wizard and `modelProviders` configuration need ergonomic improvements.

---

## Developer Pain Points

1. **OOM and Memory Leaks (Issue #4815)** — Severe OOM crashes within 10 minutes on `--resume`, with non-functional Escape key. The most critical stability issue this week. Fix PR #4824 is under review.

2. **Task Interruption and Context Loss (Issues #4278, #4740, #4506, #4700, #4672)** — Multiple reports of agents going into infinite loops (file reading, task descriptions), getting stuck on single tasks, or losing context upon resumption. Chinese and English communities both affected. This is the #1 user friction point: **reliability of long-running agent sessions.**

3. **UI / Terminal Rendering Issues (Issues #4794, #4561, #4442, #4675, #4725)** — Compact mode flash, terminal freezing on bulk edits, Vim mode Esc leaks, tmux scrolling issues. Ink-based TUI has several re-render and key-handling bugs that degrade the interactive experience, especially on Windows.

4. **Local / Self-Hosted LLM Compatibility (Issues #4657, #4793, #4750)** — Timeouts, incomplete task completion, and tool parameter schema mismatches when using Ollama, LMStudio, or vLLM. The self-hosted path still requires specialized fixes.

5. **Offline / LAN Environment Blockers (Issue #4550)** — Users on air-gapped or LAN-only networks get stuck at initialization because the tool attempts internet connectivity checks without a fallback or configurable skip. Affects enterprise and security-conscious users.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-07

---

## 1. Today's Highlights

The project is in final sprint toward the **v0.9.0 release**, with a comprehensive acceptance matrix (#2729) and nearly a dozen evidence-gathering PRs merged today. The maintainer has been systematically closing release gates (startup smoke tests, asset verification, rollback instructions) while major feature work continues on **WhaleFlow workflows**, **command dispatch refactoring**, and **multi-tab support**. An unexpected keyboard bug affecting French AZERTY users was fixed promptly, and the VS Code Agent View integration gained git metadata visibility.

---

## 2. Releases

*No new releases in the last 24 hours.* The project remains at v0.8.53, with v0.9.0 preparation dominating activity.

---

## 3. Hot Issues

**#2729 — v0.9.0 Release acceptance matrix: required checks before tagging**  
*[OPEN] [documentation, enhancement, release-blocker, v0.9.0] — 15 comments*  
The central release-blocking issue. Defines required checks across core build/test, provider routing, UI, Model Lab, WhaleFlow, docs, packaging, and rollback. Community is actively contributing evidence-gating PRs.  
🔗 [Issue #2729](https://github.com/Hmbown/CodeWhale/issues/2729)

**#2580 — FR: Adapt CodeWhale to VSCode - Agent View**  
*[OPEN] [documentation, enhancement] — 9 comments*  
Strong demand for official VS Code integration beyond terminal-based TUI. Multiple community members shared use cases for IDE-native agent interactions.  
🔗 [Issue #2580](https://github.com/Hmbown/CodeWhale/issues/2580)

**#2791 — Refactor command dispatch from monolithic match to modular strategy pattern**  
*[OPEN] [enhancement] — 6 comments*  
Major architectural improvement led by contributor aboimpinto. The command handler has grown unwieldy; this refactor will split it into focused modules. Now tracked via EPIC #2870.  
🔗 [Issue #2791](https://github.com/Hmbown/CodeWhale/issues/2791)

**#2722 — v0.9.0 Open PR harvest: merge, supersede, or close long-lived branches**  
*[OPEN] [documentation, enhancement, v0.9.0] — 6 comments*  
Systematic audit of all open PRs before release. Agents and maintainers are reviewing each branch for mergeable content or conflicts.  
🔗 [Issue #2722](https://github.com/Hmbown/CodeWhale/issues/2722)

**#2847 — Abnormal stop working while coding or analysis**  
*[OPEN] [bug] — 2 comments*  
User reports `Warn Stream read error: error decoding response body`. No resolution yet; likely a provider streaming or network issue.  
🔗 [Issue #2847](https://github.com/Hmbown/CodeWhale/issues/2847)

**#2787 — TUI status bar displays mcp count error**  
*[OPEN] [bug] — 2 comments*  
When both global and project-level MCP configs exist, status bar shows incorrect MCP tool count. Reported on v0.9.0-stewardship branch.  
🔗 [Issue #2787](https://github.com/Hmbown/CodeWhale/issues/2787)

**#2863 — French AZERTY @ key conflicts with Alt-@ sidebar shortcut**  
*[CLOSED] [bug] — 1 comment*  
`AltGr+0` for `@` was intercepted as `Alt+@` sidebar focus shortcut. Fixed today by PR #2867. Demonstrates good keyboard-locale awareness.  
🔗 [Issue #2863](https://github.com/Hmbown/CodeWhale/issues/2863)

**#2666 — telemetry: agents need visible token context and resource usage during long tasks**  
*[OPEN] [bug] — 2 comments*  
Agents lack visibility into token budget, context pressure, and elapsed time during long-running tasks. Critical for multi-agent reliability.  
🔗 [Issue #2666](https://github.com/Hmbown/CodeWhale/issues/2666)

**#2694 — Sidebar detail popovers: make Work/Tasks/Agents rows fully inspectable**  
*[OPEN] [enhancement, v0.9.0, whaleflow] — 2 comments*  
Sidebar entries truncate at small terminal sizes; popovers would make long labels readable. Part of making the sidebar a live work dashboard.  
🔗 [Issue #2694](https://github.com/Hmbown/CodeWhale/issues/2694)

**#2670 — WhaleFlow: Starlark authoring layer, repair loop, and compile gate**  
*[CLOSED] [enhancement, v0.9.0] — 3 comments*  
Closed today — adds Starlark-based workflow authoring that compiles to typed IR before execution. Foundation for safe, model-authored workflows.  
🔗 [Issue #2670](https://github.com/Hmbown/CodeWhale/issues/2670)

---

## 4. Key PR Progress

**#2871 — Layer 1: clean command support boundaries**  
*[OPEN] — aboimpinto*  
First mergeable slice of the #2791 command refactor. Removes public helper noise and prepares for modular command groups. Keeps folder structure intact.  
🔗 [PR #2871](https://github.com/Hmbown/CodeWhale/pull/2871)

**#2869 — fix(tui): list saved models from all providers in /model picker**  
*[OPEN] — ousamabenyounes*  
Fixes `/model` picker visibility: custom models saved under one provider were invisible when another provider was active.  
🔗 [PR #2869](https://github.com/Hmbown/CodeWhale/pull/2869)

**#2867 — fix(tui): prevent AltGr from swallowing @/#/$/!/%/ characters in composer**  
*[CLOSED] — ousamabenyounes*  
Fixes AZERTY keyboard `@` issue. Handles `AltGr` = `Ctrl+Alt` mapping in crossterm, exempting AltGr characters from sidebar shortcut interception.  
🔗 [PR #2867](https://github.com/Hmbown/CodeWhale/pull/2867)

**#2864 — feat(tui): add multi-tab system core (manager + persistence)**  
*[CLOSED] — ljm3790865*  
Narrow slice of multi-tab support: tab module with persistence. Sister PR to #2753, scoped to core only without UI picker/switcher.  
🔗 [PR #2864](https://github.com/Hmbown/CodeWhale/pull/2864)

**#2866 — feat(tui): add hotbar action registry foundation**  
*[CLOSED] — reidliu41*  
Adds action trait, dispatch result, and built-in action registry. Lays groundwork for hotbar UI (#2063) without implementing the bar itself.  
🔗 [PR #2866](https://github.com/Hmbown/CodeWhale/pull/2866)

**#2865 — Modernize toward latest Claude Code (prompts, hooks, skills, agents, UI)**  
*[OPEN] — lmclaw*  
Large modernization PR closing gaps with latest Claude Code behavior. Covers prompts, lifecycle, skills/agents, and UI improvements.  
🔗 [PR #2865](https://github.com/Hmbown/CodeWhale/pull/2865)

**#2862 / #2868 — Runtime API: expose git status metadata for VS Code Agent View**  
*[CLOSED] — Hmbown*  
Adds `head` and `dirty` fields to thread summaries and workspace status. Mirrors v0.9 changelog credit for IDE/Agent View support.  
🔗 [PR #2862](https://github.com/Hmbown/CodeWhale/pull/2862) | [PR #2868](https://github.com/Hmbown/CodeWhale/pull/2868)

**#2781 — feat(tui): ghost-text follow-up prompt suggestion**  
*[OPEN] — punkcanyang*  
After each turn, generates a concise follow-up suggestion (ghost text) using a lightweight model. Tab to accept; typing dismisses. Mirrors Claude Code behavior.  
🔗 [PR #2781](https://github.com/Hmbown/CodeWhale/pull/2781)

**#2808 — feat(runtime-api): add session save, undo/retry, and snapshot endpoints for GUI**  
*[OPEN] — gaord*  
Exposes TUI session capabilities to GUI clients — save, undo, retry, and snapshot — without reimplementing logic in the API layer.  
🔗 [PR #2808](https://github.com/Hmbown/CodeWhale/pull/2808)

**#2762 — v0.9.0 stewardship integration**  
*[OPEN] — Hmbown*  
Integration branch for v0.9.0 harvest and stabilization. Keeps release actions (tag, publish) out of scope while providing a PR-check surface for stewardship work.  
🔗 [PR #2762](https://github.com/Hmbown/CodeWhale/pull/2762)

---

## 5. Feature Request Trends

**IDE/Editor Integration (4 issues)** — Strong demand for native VS Code Agent View integration (#2580, #2862, #2868) and IDE plugins generally (#1584). Users explicitly want GUI interaction for coding tasks while keeping TUI for system operations.

**WhaleFlow Workflow Engine (12+ issues)** — The dominant theme of v0.9.0. Community interest in: Starlark authoring (#2670), typed IR (#2668), replay/repair loops (#2673, #2670), branch memoization (#2671), teacher/student lesson promotion (#2674, #2675), and semantic code search (#2680).

**Multi-Tab & UI Polish (5 issues)** — Tab management (#2864, #2753), sidebar popovers for truncated rows (#2694), ghost-text prompt suggestions (#2781), and a designed welcome/home screen (#2713).

**Model Lab & Provider Enhancements (3 issues)** — Hugging Face provider polish (#2727), model picker fixes (#2869), and TLS certificate configurability (#1893).

**Remote Workbench (1 issue)** — AWS Lightsail + Telegram bridge for always-on VM with phone control (#2724).

---

## 6. Developer Pain Points

- **Keyboard layout conflicts**: AZERTY and other non-QWERTY layouts cause `AltGr` characters to be intercepted by sidebar shortcuts. Fixed for French; other layouts may still be affected.
- **TLS certificate friction**: Users behind corporate proxies or with self-signed certs need per-provider TLS verification toggles (#1893). PR has been open 17 days awaiting merge.
- **Streaming/decoding errors**: Non-specific `Warn Stream read error: error decoding response body` (#2847) interrupts workflows with no clear fix path.
- **MCP configuration confusion**: Global vs project-level MCP configs produce incorrect status bar counts (#2787), making tool availability unclear.
- **Token/resource visibility**: Agents lack insight into token budgets and context pressure during long tasks (#2666), leading to hangs or context overflows.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*