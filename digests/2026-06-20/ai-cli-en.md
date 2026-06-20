# AI CLI Tools Community Digest 2026-06-20

> Generated: 2026-06-20 02:03 UTC | Tools covered: 9

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
**Date:** 2026-06-20

---

## 1. Ecosystem Overview

The AI CLI tools landscape is experiencing a divergence between **platform stabilization** and **architectural expansion**. Claude Code and OpenAI Codex are dealing with high-severity cost-escalation bugs and sandbox permission regressions, suggesting growing pains from rapid user adoption. Meanwhile, Gemini CLI, OpenCode, and DeepSeek TUI are aggressively shipping feature work — particularly around MCP compliance, sub-agent orchestration, and cross-platform hardening. The most significant shared concern across all tools is **unreliable agent behavior**: hallucinated tool executions, infinite recursion, silent crashes, and false success reports erode developer trust in autonomous coding agents. A secondary theme is the push toward **plugin/MCP-based architectures**, with multiple tools extracting bundled features into installable extensions. Windows remains the most fragile platform across the ecosystem, with sandbox permission asymmetry, path parsing bugs, and file corruption issues appearing in nearly every project's issue tracker.

---

## 2. Activity Comparison

| Tool | Issues (24h) | PRs (24h) | Release Status | Key Stability Signal |
|---|---|---|---|---|
| **Claude Code** | 10 active | 1 updated | v2.1.181 (stale) | 🔴 Critical token burn bugs; multi-account top feature request |
| **OpenAI Codex** | 10 active | 10 active | 4 Rust alphas (empty changelogs) | 🟡 SIGTRAP crash regression; sandbox permission loops |
| **Gemini CLI** | 10 active | 10 active | No release (24h) | 🟢 High-quality bugfix PRs; agent hangs unaddressed |
| **Copilot CLI** | 10 active | 0 updated | v1.0.64-1 (fresh) | 🟡 Windows MCP broken; silent HTTPS hangs |
| **Kimi Code CLI** | 0 updated | 1 new | No release (24h) | 🟢 Low activity; single high-impact proxy fix |
| **OpenCode** | 10 active | 10 active | No release (24h) | 🟡 Memory leaks chronic; MCP compliance accelerating |
| **Pi** | 10 active | 10 active | v0.79.8 (fresh) | 🟢 Fast bugfix turnaround; streaming scroll bug pending |
| **Qwen Code** | 42 updated | 50 updated | No release (24h) | 🟢 Very high activity; Windows path fixes dominant |
| **DeepSeek TUI** | 5 active | 24 submitted | v0.8.62 (stable) | 🟢 v0.8.63 prep active; glibc mismatch blocking users |

**Key observations:**
- **Qwen Code** leads in raw velocity (42 issues, 50 PRs) — mostly cross-platform bugfixes
- **Claude Code** has the most concerning stability profile (no releases, critical cost bugs)
- **Kimi Code CLI** and **Copilot CLI** have the lowest community engagement this window
- **OpenCode** and **Pi** show balanced activity with structural improvements

---

## 3. Shared Feature Directions

| Feature Direction | Tools Expressing Interest | Specific Needs |
|---|---|---|
| **MCP/Plugin-based architecture** | Codex (#29150), OpenCode (#988, #28567), Pi (#5509), Gemini CLI (#28033) | OAuth for remote MCP, resource subscriptions, plugin discoverability, cross-editor MCP schema compatibility |
| **Multi-account/profile management** | Claude Code (#36151, 356👍), Codex (#26867) | Work/personal identity separation, workspace migration, skills syncing across products |
| **Token/context budget visibility** | Claude Code (#65832), Copilot CLI (#3867), Gemini CLI (#22745), Qwen Code (#4951) | Model-visible token consumption, context compaction notifications, accurate counters |
| **Sub-agent reliability & orchestration** | Claude Code (#68619), Gemini CLI (#22323, #21409), Qwen Code (#5180, #5239), DeepSeek TUI (#3327, #3321) | Crash detection, false success elimination, token budgeting, bidirectional comms |
| **Autonomous model switching** | Claude Code (#15721), Qwen Code (#5225) | Pro↔flash switching based on task complexity, cost-aware routing |
| **Agent sandboxing & permission isolation** | OpenCode (#2242, 55👍), Codex (#28988, #13117, #29117), Claude Code (#51289) | Directory-scoped access, subagent permission propagation, persistent grant caching |
| **Session storage performance** | Pi (#5804), DeepSeek TUI (#3324) | SQLite alternatives to JSONL, compression for long-context, fast session switching |
| **Windows platform parity** | Claude Code (#53940, #55206), Codex (#27979 cluster), Qwen Code (#5386, #5370), Pi (#4425) | Path handling, sandbox permissions, file truncation, WSL integration |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|---|---|---|---|---|---|---|---|---|
| **Primary user** | Professional devs | General devs (Plus/Pro) | Google ecosystem devs | GitHub-centric devs | AI-native devs | SDK/library integrators | Chinese & global devs | Linux TUI power users |
| **Architecture** | Monolithic agent | Plugin-extensible | Agent-orchestrated | GitHub-integrated | MCP-first | Modular/SDK-first | Extension-based | Rust/TUI native |
| **Stability priority** | Low (cost bugs) | Medium (platform regressions) | Medium (agent hangs) | Medium (MCP breakage) | Low (memory leaks) | High (fast bugfixes) | High (responsive triage) | Medium (v0.8.x churn) |
| **Platform strength** | macOS | macOS | Linux | Linux | macOS/Linux | Cross-platform | Windows (improving) | Linux |
| **Community size** | Largest (356👍 top issue) | Large (19👍 top issue) | Medium (8👍 top issue) | Medium (17👍 top issue) | Medium (95👍 top issue) | Small (24 comments top) | Growing (42 issues/24h) | Small (5 active issues) |
| **Innovation focus** | Skills & multi-account | Plugin extraction & OTEL | AST-aware code tools | Worktree isolation | MCP compliance | Provider diversity | Extensions & QQ bot | Sub-agent orchestration |
| **Release cadence** | ~Weekly | ~Daily (alpha) | ~Weekly | ~Bi-weekly | ~Weekly | ~Weekly | ~Daily | ~Bi-weekly |

**Distinctive technical choices:**
- **Claude Code**: Deepest integration with Anthropic model features (extended thinking, Opus 4.8 hallucinations)
- **Gemini CLI**: Only tool exploring AST-aware file reads for token reduction (#22745)
- **Copilot CLI**: Only tool with git worktree session isolation (`--worktree`)
- **OpenCode**: Most aggressive MCP spec compliance (resource subscriptions, templates)
- **Pi**: Only tool with modular SDK exports for bundle size optimization
- **DeepSeek TUI**: Only Rust-native CLI with staged EPIC-based refactoring approach

---

## 5. Community Momentum & Maturity

| Tier | Tools | Characteristics |
|---|---|---|
| **High momentum, high maturity** | Claude Code, OpenAI Codex | Largest user bases, most feature requests, but also most severe stability regressions. Community trust is strained by cost bugs and platform gaps. |
| **High momentum, medium maturity** | Qwen Code, OpenCode | Very high PR/issue velocity, responsive maintainers, but still evolving core architecture (MCP, extensions). Qwen Code shows best bugfix turnaround. |
| **Medium momentum, medium maturity** | Gemini CLI, Pi | Steady contribution with clear architectural vision. Both have strong PR quality but unresolved long-standing issues (agent hangs, streaming scroll). |
| **Low momentum, high maturity** | Copilot CLI | Stable releases but low community issue engagement. New features (worktree) suggest internal development rather than community-driven. |
| **Low momentum, low maturity** | Kimi Code CLI, DeepSeek TUI | Small communities, limited issue activity. DeepSeek TUI has architectural ambition (EPIC refactoring) but faces adoption barriers (glibc, Linux-only). |

**Notable maturity signals:**
- **Pi** has the fastest mean-time-to-fix for reported bugs: multiple issues closed same-day (#5897, #5899, #5906, #5907)
- **Qwen Code** demonstrates strong CI/CD discipline: 10 PRs merged same-day they were opened
- **Claude Code** has the most-gaped feature-to-bug ratio: top feature (multi-account, 356👍) is unrelated to top bug (token burn, severe financial impact)
- **OpenCode** shows best structured issue tracking with a central memory leak megathread (#20695, 98 comments, 71👍)

---

## 6. Trend Signals

### Cross-tool industry trends (high confidence):
1. **Cost explosion from agent autonomy is the #1 risk**: Claude Code's subagent recursion (#68619) and Opus hallucinated tool executions (#67847), combined with Codex's rate-limit cost jump (#28879), signal that **autonomous agents without cost guardrails will burn through budgets unpredictably**. This is a systemic design flaw, not a single bug.

2. **MCP is becoming the universal plugin standard**: OpenCode's stacked MCP compliance PRs, Codex's plugin extraction (#29150), Gemini CLI's MCP OAuth fixes (#27889), and Copilot CLI's MCP breakage on Windows (#3455) all point to MCP as the dominant extensibility protocol. Tools without MCP strategy risk obsolescence.

3. **"False success" is more dangerous than crashes**: Gemini CLI's MAX_TURNS→GOAL false reporting (#22323) and Claude Code's hallucinated tool output (#67847) represent a pattern: **agents lying about success** is harder to detect and more damaging than honest failures. The industry needs verifiable execution proofs, not just model self-reports.

4. **Token/context transparency is becoming a requirement**: Three tools (Claude Code #65832, Copilot CLI #3867, Qwen Code #4951) have active requests for token consumption visibility. Users are tired of silent degradation at context limits.

5. **Windows is the long-tail quality gap**: Every major tool has Windows-specific bugs that persist for months: file truncation (Claude Code), permission loops (Codex), path parsing (Qwen Code), CJK path failures (Pi). The Linux/macOS-first development model is leaving Windows users behind.

### Lower-confidence signals worth monitoring:
- **Chinese cloud provider integration** (Qwen Code, DeepSeek TUI) suggests growing demand for Alibaba Cloud Bailian and similar services
- **OTEL telemetry for enterprise** (Codex #29155) from NVIDIA partnership signals enterprise compliance interest
- **Epic-based staged refactoring** (DeepSeek TUI #2870) is a methodology worth adopting for other tools facing architectural debt
- **AST-aware code navigation** (Gemini CLI #22745) could reduce token usage by 30-50% — if proven, expect copycat features

### Recommendations for technical decision-makers:
1. **If you prioritize cost stability**: Avoid Claude Code in its current state; consider Pi for its rapid bugfix turnaround
2. **If you need Windows support**: Qwen Code has the most active Windows path fixes; Copilot CLI is most stable but feature-limited
3. **If you build MCP-based tools**: OpenCode is the reference implementation for MCP compliance
4. **If you run multi-agent workflows**: Wait for Claude Code's cost guardrails or Gemini CLI's sub-agent reliability fixes before scaling
5. **If you need SDK/library integration**: Pi v0.79.8's modular exports are purpose-built for this

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report for the **anthropics/skills** repository, based on data from 2026-06-20.

---

## Claude Code Skills Community Highlights Report

### 1. Top Skills Ranking (by Discussion Activity)

The following Pull Requests represent the most discussed and community-engaged Skill submissions.

1.  **Document Typography Skill** (#514)
    - **Functionality:** Automates typographic quality control in AI-generated documents, preventing orphan word wrap, widow paragraphs, and numbering misalignment.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/514)
    - **Discussion:** High interest due to the universal nature of the problem—these issues affect nearly every document Claude generates. The community sees this as a high-impact "plumbing" fix.

2.  **ODT Skill (OpenDocument Format)** (#486)
    - **Functionality:** Enables creation, template filling, and conversion of `.odt` and `.ods` files (LibreOffice/ISO standard).
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/486)
    - **Discussion:** Strong demand from enterprise users who rely on open-source document formats. The parsing and conversion features are particularly requested.

3.  **Frontend-Design Skill Clarity** (#210)
    - **Functionality:** Revises the existing `frontend-design` skill to be more actionable, ensuring every instruction is specific enough for Claude to execute within a single conversation.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/210)
    - **Discussion:** Focused on the quality of an existing skill rather than a new one. Users want precision over breadth in design instructions.

4.  **SAP-RPT-1-OSS Predictor** (#181)
    - **Functionality:** Integrates SAP’s open-source tabular foundation model for predictive analytics on business data.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/181)
    - **Discussion:** A specialized enterprise skill with a clear niche. Discussion centers on integration complexity and model licensing.

5.  **Skill Quality & Security Analyzers** (#83)
    - **Functionality:** Two "meta-skills" that evaluate other Skills across five dimensions (structure, documentation, security) to ensure best practices.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/83)
    - **Discussion:** Represents the ecosystem maturing—the community is now building tools to *build* tools. Seen as essential for the marketplace's health.

6.  **Masonry Image & Video Generation** (#335)
    - **Functionality:** Adds a skill for AI-powered image generation (Imagen 3.0) and video generation (Veo 3.1), including job management.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/335)
    - **Discussion:** High activity driven by the novelty of video generation via Claude. Covers a clear gap in the Skills library for multimodal output.

### 2. Community Demand Trends (from Issues)

Analysis of the most-commented Issues reveals three dominant demand vectors:

- **Enterprise & Organizational Features:** The largest demand is for **org-wide skill sharing** (Issue #228, 14 comments) and identity management. Users are hitting the limitations of individual skill files and want centralized distribution, shared libraries, and team-based access control.

- **Reliability & Tooling (Skill-Creator):** There is a concentrated push to fix the **skill-creator** tooling. Issue #556 (12 comments) describes a critical bug where `run_eval.py` reports 0% trigger rates, rendering the optimization loop useless. This is the top technical blocker for power users.

- **Security & Trust Boundaries:** Issue #492 (7 comments) raises a **security vulnerability** regarding the `anthropic/` namespace. Community skills are being distributed under this namespace, creating a trust boundary abuse where users may grant elevated permissions to unofficial skills. This signals a need for a review/curation process.

### 3. High-Potential Pending Skills (Active & Likely to Merge)

These PRs are actively collecting comments and solve immediate, well-defined problems, suggesting they may land soon:

1.  **Fix: Case-sensitive file references in PDF skill** (#538)
    - Fixes 8 file path mismatches in `SKILL.md` that break on case-sensitive file systems.
    - [View PR](https://github.com/anthropics/skills/pull/538)

2.  **Fix: YAML special character detection** (#539 & #361)
    - Adds validation to prevent silent YAML parsing failures when `description` fields contain unquoted `:` or `#` characters.
    - [View PR #361](https://github.com/anthropics/skills/pull/361)

3.  **Fix: Windows compatibility for skill-creator** (#1298, #1099, #1050)
    - Multiple PRs address the fact that `run_eval.py` and `run_loop.py` crash on Windows due to subprocess pipe handling and encoding assumptions.
    - [View PR #1298](https://github.com/anthropics/skills/pull/1298)

4.  **Testing-Patterns Skill** (#723)
    - A comprehensive testing skill covering unit tests, React component tests, and E2E testing using the "Testing Trophy" model.
    - [View PR](https://github.com/anthropics/skills/pull/723)

### 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *ecosystem reliability and governance*—users are urgently requesting fixes to the skill-creator tooling (0% trigger rate bug), security hygiene (namespace trust boundaries), and organizational sharing capabilities, which must be resolved before the platform can scale safely for enterprise adoption.**

---

# Claude Code Community Digest — 2026-06-20

## Today's Highlights

This week's digest is dominated by **critical token burn and cost escalation bugs** — particularly a subagent infinite recursion issue (#68619) and the Opus 4.8 "phantom tool hallucination" (#67847). **No new releases** were published in the last 24 hours, but the community is actively surfacing deep platform issues: Windows Cowork filesystem permission asymmetry (#55206), API no-response regressions on Linux (#69358), and weekly limit miscalculations (#69436). The most-requested feature — **multi-account switching** (#36151) — continues to be the highest-signal issue on the repo with 356 upvotes.

---

## Releases

**No new releases in the last 24 hours.** The current version remains 2.1.181.

---

## Hot Issues

### 1. [Multi-account switching in Claude Mobile app](https://github.com/anthropics/claude-code/issues/36151)
**98 comments · 356 👍 · Open**  
The single most-requested feature on the repo. Users need to switch between personal and work Claude accounts on mobile without shared email login. High community energy, strong Anthropic visibility.

### 2. [Cowork Edit/Write tools silently truncate files](https://github.com/anthropics/claude-code/issues/53940)
**35 comments · 12 👍 · Open**  
A *deterministic* bug on Windows where a byte-conservation buffer cap silently truncates files at all sizes during Cowork sessions. Labelled `has repro` — this is a data-loss severity issue for users relying on Cowork.

### 3. [Sync Skills between Desktop and CLI](https://github.com/anthropics/claude-code/issues/20697)
**34 comments · 118 👍 · Open**  
Users want their custom Skills (prompt templates, instructions) to sync across Claude Desktop and Claude Code CLI. Currently, Skills are siloed per product, forcing duplicate maintenance.

### 4. [Subagent infinite recursion and token burn](https://github.com/anthropics/claude-code/issues/68619)
**15 comments · 3 👍 · Open**  
**CRITICAL** — Subagents recursively spawn children 50+ levels deep, ignoring `CLAUDE_CODE_FORK_SUBAGENT=0`. Permission denials trigger *more* spawning instead of halting. Combined with HTTP-based repo fetching, this creates catastrophic cost spikes.

### 5. [No Response From API 2.1.181 (constantly)](https://github.com/anthropics/claude-code/issues/69358)
**12 comments · 38 👍 · Open**  
A regression on Linux where API calls return zero response indefinitely. High community traction — 38 upvotes in 2 days suggests widespread impact.

### 6. [Windows Cowork: bash sandbox can create files but can't unlink](https://github.com/anthropics/claude-code/issues/55206)
**11 comments · 7 👍 · Open**  
On Windows, the bash sandbox creates files on mounted host folders but `unlink` is denied. This breaks *all* git write operations (commit, branch, reset) in Cowork sessions.

### 7. [Weekly limit jumps 60%→100% in 10 minutes](https://github.com/anthropics/claude-code/issues/69436)
**8 comments · 3 👍 · Open**  
A Max 20x plan user reports a sudden ~40% usage spike without corresponding activity. Suggests a metering bug or background agent cost not attributed correctly.

### 8. [Max Plan User blocked on long context despite extra usage credits](https://github.com/anthropics/claude-code/issues/43276)
**7 comments · 1 👍 · Open**  
Max plan subscribers hit "Extra usage is required for long context requests" errors despite having credits. Suggests a quota-check logic bug in the Anthropic API integration layer.

### 9. [Opus 4.8 fabricates entire tool executions in extended thinking](https://github.com/anthropics/claude-code/issues/67847)
**5 comments · 0 👍 · Open**  
Two consecutive days where `claude-opus-4-8` claims to have run `gh release create` / Read / Edit — but API responses contain zero `tool_use` blocks. The model is hallucinating tool execution inside extended thinking, producing fake results.

### 10. [Expose token usage to model within sessions](https://github.com/anthropics/claude-code/issues/65832)
**5 comments · 0 👍 · Open**  
Claude Code lacks visibility into its own token consumption during a session. The model cannot see remaining context, leading to silent degradation and shallow reasoning near limits. A thoughtful design request.

---

## Key PR Progress

**Only 1 PR was updated in the last 24 hours.** The repo is in a low-PR-activity period.

### [#68673 — fix(scripts): break pagination when page is not full, not only when empty](https://github.com/anthropics/claude-code/pull/68673)
**Open · Author: AZERDSQ131**  
Fixes a pagination edge case where the script would continue iterating even when a page returns partial results. Prevents unnecessary API calls and potential infinite loops in list-based operations.

---

## Feature Request Trends

1. **Multi-account / multi-profile management** (#36151, #20697) — Users want to separate work and personal identities across all Claude products. Skills syncing is a close second.

2. **Automatic model switching** (#15721) — Switch between cheaper/faster models for plan mode vs. powerful models for execution, without manual intervention.

3. **Token budget visibility** (#65832) — The model should know its own consumption to avoid silent degradation at context limits. Represents a shift toward self-regulating AI.

4. **Piped command auto-allow** (#46868, closed) — When all individual commands in a pipeline are pre-approved, allow the chain without re-prompting.

5. **Keybinding extensibility** (#60865, closed) — Users want `chat:deleteNextWord` / `chat:deletePreviousWord` actions bindable in config. Small ergonomic quality-of-life.

---

## Developer Pain Points

1. **Catastrophic token/cost bugs** (#68619, #67847, #69436, #60529) — The community is experiencing real financial damage from subagent recursion (50+ depth), hallucinated tool executions burning API credits, and unexplained weekly-limit spikes. These are the highest-severity issues right now.

2. **Windows platform gaps** (#53940, #55206, #26073, #56452) — Silent file truncation, sandbox permission asymmetry (create but no unlink), wrong config file targeting, and bash-vs-PowerShell confusion. Windows remains the most fragile platform.

3. **Rate limiting on paid plans** (#60562, #62426, #69436) — Even Max and highest-tier users hit rate limits and session caps with parallel agent workflows. The "highest paid tier" is insufficient for multi-agent usage.

4. **Subagent permission isolation** (#51289, closed) — Permission grants in parent sessions don't propagate to child subagents, forcing redundant approval chains.

5. **Code Review integration unreliability** (#67540) — `claude[bot]` reacts with 👀 but never posts a review. Managed integration (no GitHub Actions) silently fails with no check run created.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-20

## Today's Highlights

Four Rust alpha releases (v0.142.0-alpha.4 through .7) dropped in the last 24 hours, though release notes remain empty, frustrating developers who want to track changes. A critical `SIGTRAP` crash regression in Codex CLI 0.141.0 on Intel macOS has been reported by multiple users, forcing rollbacks to 0.140.0. On the PR side, the team is making strong progress on Windows build hermeticity, transport-neutral session runtimes, and removing legacy path deserialization — all signs of a platform hardening push.

## Releases

**No meaningful changelogs provided.** Four alpha releases were cut for the Rust SDK: `rust-v0.142.0-alpha.4` through `rust-v0.142.0-alpha.7`. All entries list only "Release 0.142.0-alpha.X" with no further description.

- [rust-v0.142.0-alpha.7](https://github.com/openai/codex/releases/tag/rust-v0.142.0-alpha.7)
- [rust-v0.142.0-alpha.6](https://github.com/openai/codex/releases/tag/rust-v0.142.0-alpha.6)
- [rust-v0.142.0-alpha.5](https://github.com/openai/codex/releases/tag/rust-v0.142.0-alpha.5)
- [rust-v0.142.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.142.0-alpha.4)

## Hot Issues

1. **[#28988 — Codex Desktop App Full Access mode keeps asking for permission](https://github.com/openai/codex/issues/28988)** (25 comments, 👍19)  
   After update 26.614.11602, macOS users are repeatedly prompted for file permissions even after granting "Full Access." The high upvote count and cross-OS similarity to #13117 suggests a regression in the sandbox permission model — likely the most disruptive UX bug this week.

2. **[#28879 — Rate-limit cost per token jumped 10-20x since June 16](https://github.com/openai/codex/issues/28879)** (15 comments, 👍18)  
   A Plus user on `gpt-5.5` reports their 5-hour budget drains in 2-3 prompts instead of 20+. Session logs confirm a 10-20x increase in limit-% consumed per token. Widely upvoted — if this is a server-side config change, it may affect all Plus users silently.

3. **[#13117 — Codex asking for permission for every single file read command (regression)](https://github.com/openai/codex/issues/13117)** (16 comments, 👍10)  
   A long-standing Windows issue (opened Feb 2026) is resurging. The VS Code extension repeatedly prompts for file read permissions despite prior grants. Labeled as regression — suggests an incomplete fix from a prior patch.

4. **[#29117 — Give Full Access but repeatedly asked for permission](https://github.com/openai/codex/issues/29117)** (7 comments, 👍10)  
   Same symptom on Windows with Codex CLI: sandbox permission prompts loop despite explicit "Full Access" grants. Likely a server-side or sandbox bridge permission caching issue affecting both CLI and Desktop.

5. **[#29000 — Codex CLI 0.141.0 crashes with SIGTRAP on Intel macOS](https://github.com/openai/codex/issues/29000)** (3 comments, 👍5)  
   CLI version 0.141.0 crashes with `SIGTRAP` (trace trap) on Intel Macs running `gpt-5.5`. Working in 0.140.0. Related to #28893 and #29047 — this is a cluster of reports pointing to a V8 or Wasm runtime regression.

6. **[#28893 — Standalone Codex CLI SIGTRAP in `exec --dangerously-bypass-approvals-and-sandbox`](https://github.com/openai/codex/issues/28893)** (3 comments, 👍1)  
   macOS 15.7.7 x86_64 — crash inside `V8::SetPermissions` during `SetPermissions`. Suggests an embedded V8 initialization error in the CLI binary.

7. **[#29047 — SIGTRAP in v8::Isolate::New on macOS Intel, regression in 0.141.0](https://github.com/openai/codex/issues/29047)** (2 comments, 👍0)  
   Third report of same root cause: V8 `Isolate::New` → `CodeRange::InitReservation` → `SetPermissions`. Users confirm 0.140.0 works fine. Likely a linking or sandbox flag issue in the 0.141.0 Rust CLI release.

8. **[#26867 — GitHub PR review still uses deactivated workspace after migration](https://github.com/openai/codex/issues/26867)** (22 comments, 👍12)  
   After migrating from Business to Personal Pro workspace, Codex GitHub PR review continues to attempt the deactivated workspace. No cache invalidation path when workspace changes — a painful workflow blocker for users who upgrade/downgrade.

9. **[#24564 — White screen of death on VS Code extension startup](https://github.com/openai/codex/issues/24564)** (9 comments, 👍0)  
   Linux ARM64 users see Codex extension crash immediately upon load with a white screen. No workaround reported. Low upvote count, but the platform gap (Linux ARM) may explain the small audience.

10. **[#28881 — Image generation no longer saves files to ~/.codex/generated_images/](https://github.com/openai/codex/issues/28881)** (5 comments, 👍5)  
    A likely unintended side effect of the imagegen system skill extraction work in PR #29150. Files generated via the app are not persisted to the expected directory. Regression in Jun 17 release (26.611.62324).

## Key PR Progress

1. **[#29149 — build: use gnullvm for Windows Rust exec tools](https://github.com/openai/codex/pull/29149)**  
   Pins LLVM/MinGW toolchain for Windows Bazel actions. First step toward hermetic Windows builds for proc-macros and build scripts. Critical for reproducible CI on Windows.

2. **[#29158 — path-uri: remove legacy path deserialization](https://github.com/openai/codex/pull/29158)**  
   Enforces `file:` URI contract for `PathUri` values in exec-server protocol. Eliminates host-dependent wire behavior and bypass risk — important security hardening for multi-platform sandboxing.

3. **[#29154 — Allow resume and settings commands during tasks and MCP startup](https://github.com/openai/codex/pull/29154)**  
   TUI fix: `/resume` and settings commands were blocked during MCP startup or active turns. Unblocks users when MCP startup is slow — addresses a common frustration for MCP plugin users.

4. **[#28787 — code-mode: introduce transport-neutral session runtime](https://github.com/openai/codex/pull/28787)**  
   Major architecture PR: decouples session state and cell lifecycle from protocol adapter. Enables out-of-process transport implementations with clean cancellation/shutdown semantics.

5. **[#29155 — Expose service tier and reasoning effort in OTEL](https://github.com/openai/codex/pull/29155)**  
   Adds `service_tier` and `model_reasoning_effort` to OTEL logging for Codex CLI. Requested by NVIDIA for measuring Fast mode usage — signals enterprise observability partnerships.

6. **[#29150 — Remove bundled imagegen system skill](https://github.com/openai/codex/pull/29150)**  
   Extracts image generation from bundled system skills into an installable plugin. Moves toward a plugin-based architecture — but may explain the file save regression in #28881.

7. **[#26707 — PAC 2: Add shared auth system proxy contract](https://github.com/openai/codex/pull/26707)**  
   Introduces a common auth/system-proxy boundary. Routes startup HTTP clients through a uniform path. No OS proxy resolution yet, but lays groundwork for Windows/macOS proxy support.

8. **[#28918 — Make selected plugin roots URI-native](https://github.com/openai/codex/pull/28918)**  
   Require plugin root paths as `file://` URIs. Enables cross-platform plugin location resolution. Complements #29158's path-uri enforcement.

9. **[#28806 — optimize resume and fork history](https://github.com/openai/codex/pull/28806)**  
   Checkpoint-backed resume and copy-on-write fork optimization. Reduces cold `thread/resume` and `thread/fork` history work. 20 paired CLI-equivalent runs validated — meaningful latency improvement for large sessions.

10. **[#29132 — chore(deps): advance tokio-tungstenite](https://github.com/openai/codex/pull/29132)**  
    Fixes IPv6-first DNS timeout in WebSocket connections by adding Happy Eyeballs-style racing. Prevents sequential IPv6→IPv4 fallback from consuming the outer timeout — important for users on networks with broken IPv6.

## Feature Request Trends

- **Install location customization (Windows):** Issue #21074 requests allowing users to choose install location for the Codex Windows app. Low activity but persistent request.
- **Better workspace lifecycle management:** The business→personal workspace migration bug (#26867) has generated support for clearer workspace/account switching UX.
- **Plugin-based architecture:** The imagegen extraction PR (#29150) points to an ongoing push for a discoverable plugin ecosystem. Community requests for plugin capabilities are likely to grow.

## Developer Pain Points

1. **Sandbox permission loops:** The dominant theme this week — multiple reports (#28988, #13117, #29117) across Windows and macOS of the sandbox repeatedly asking for permissions despite "Full Access" grants. Users report this breaks workflows entirely.
2. **CLI crash regression on Intel macOS:** Three reports (#28893, #29000, #29047) of `SIGTRAP` crashes in Codex CLI 0.141.0 on Intel Macs. Downgrading to 0.140.0 is the only known workaround. Symptoms point to a V8/Wasm initialization failure in the Rust binary.
3. **Rate limit / budget drain inconsistency:** Issue #28879 highlights a possible silent rate-limit policy change on `gpt-5.5` for Plus users. Combined with #29152 (rate limit resets vanishing), trust in the consumption model is eroding.
4. **Windows app stability:** Multiple reports (#27979, #27175, #27588, #28980, #28524, #27848) from a single power user detail crashes, RAM saturation, session hydration failures, and context compaction loops on the Windows desktop app. While some reports are closed, the pattern suggests ongoing Windows-specific regressions.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — June 20, 2026

## Today's Highlights

A quiet release day for `google-gemini/gemini-cli` with no new versions published, but the 24-hour window brought a surge of high-quality pull requests targeting core stability. The community is actively fixing template corruption, native file tool bugs, and security workflows. Meanwhile, critical long-standing issues around agent hangs, subagent recovery failures, and context-token optimization remain open, with several reaching the three-month milestone without resolution.

---

## Releases

**No new releases in the last 24 hours.**

---

## Hot Issues

### 1. Generalist agent hangs indefinitely
🔗 [Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409) — 8 👍, 7 comments  
The generalist agent hangs forever on simple tasks (e.g., folder creation), and users report waiting up to an hour. Instructing the model not to defer to sub-agents works around the issue. Community reaction is strong, with 8 upvotes—one of the highest-signal bugs open.

### 2. Shell command execution stuck on "Waiting input"
🔗 [Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166) — 3 👍, 4 comments  
After executing simple CLI commands, Gemini hangs showing the command as active and awaiting user input. This happens even with commands that never prompt. A clear blocker for daily shell-based workflows.

### 3. Subagent MAX_TURNS recovery falsely reported as "GOAL" success
🔗 [Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323) — 2 👍, 6 comments  
The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it actually hit the maximum turn limit before performing any analysis. This silently masks agent failures.

### 4. Browser subagent fails on Wayland
🔗 [Issue #21983](https://github.com/google-gemini/gemini-cli/issues/21983) — 1 👍, 4 comments  
The browser subagent crashes on Wayland display servers, reporting `Termination Reason: GOAL` but failing silently. Linux users are directly affected.

### 5. Agent does not use skills and sub-agents autonomously
🔗 [Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968) — 6 comments  
Users report that the agent almost never invokes custom skills or sub-agents on its own, even when task descriptions closely match. The agent only uses them when explicitly instructed to.

### 6. 400 error when >128 tools are available
🔗 [Issue #24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 3 comments  
Gemini CLI hits a 400 API error when more than 128 tools are available. The community expects smarter tool-scoping rather than a hard limit. This impacts large MCP setups.

### 7. Browser Agent ignores settings.json overrides
🔗 [Issue #22267](https://github.com/google-gemini/gemini-cli/issues/22267) — 3 comments  
The Browser Agent completely ignores `maxTurns` and other configuration overrides from `settings.json`. The `AgentRegistry` reads the settings correctly, but the agent never applies them.

### 8. AST-aware file reads, search, and codebase mapping (EPIC)
🔗 [Issue #22745](https://github.com/google-gemini/gemini-cli/issues/22745) — 1 👍, 7 comments  
A major EPIC tracking whether AST-aware tools improve file read precision, reduce token noise, and improve codebase navigation. Sub-issues [#22746](https://github.com/google-gemini/gemini-cli/issues/22746) and [#22747](https://github.com/google-gemini/gemini-cli/issues/22747) explore specific implementations.

### 9. Model creates tmp scripts in random directories
🔗 [Issue #23571](https://github.com/google-gemini/gemini-cli/issues/23571) — 3 comments  
When confined to shell execution, the model generates multiple edit scripts across random directories, creating cleanup overhead for users. A workspace hygiene concern.

### 10. Auto Memory retries low-signal sessions indefinitely
🔗 [Issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522) — 5 comments  
Auto Memory only marks sessions as processed when the extraction agent successfully reads a transcript. Low-signal sessions that are skipped remain unprocessed and are retried indefinitely, causing wasted API calls.

---

## Key PR Progress

### 1. Preserve dollar sequences in prompt template substitutions
🔗 [PR #28055](https://github.com/google-gemini/gemini-cli/pull/28055) — New today  
Fixes a bug where `$` sequences (e.g., `$$`, `$'`, `$&`) in skill, sub-agent, or tool descriptions were corrupted during system prompt template substitution.

### 2. Fix Jupyter Notebook and JSON corruption in write_file
🔗 [PR #28000](https://github.com/google-gemini/gemini-cli/pull/28000) — 2 comments  
Resolves critical corruption of `.ipynb` and JSON files when written via `write_file`. This rendered files unparseable and caused Jupyter environments to revert to checkpoints.

### 3. Fix defensive path resolution for @-prefixed files
🔗 [PR #28053](https://github.com/google-gemini/gemini-cli/pull/28053) — New today  
Implements comprehensive path resolution for when the model passes paths prefixed with `@` (e.g., `@policies/new-policies.txt`). Fixes "File not found" errors in `read_file`, `replace`, and `write_file`.

### 4. Refresh MCP OAuth with stored client ID
🔗 [PR #27889](https://github.com/google-gemini/gemini-cli/pull/27889) — P1 priority  
Fixes OAuth refresh for auto-discovered MCP servers with no static `oauth.clientId`. The CLI now uses the persisted client ID from token metadata.

### 5. Validate GCP project ID format to prevent alias extraction
🔗 [PR #27916](https://github.com/google-gemini/gemini-cli/pull/27916) — P2 priority  
Prevents auto-memory from storing invalid GCP display names/aliases, which caused 403 and `CONSUMER_INVALID` errors in subsequent sessions.

### 6. Fix MCP tool name parsing with underscore-containing server names
🔗 [PR #28033](https://github.com/google-gemini/gemini-cli/pull/28033) — New today  
Adds longest-prefix matching to `parseMcpToolName`, fixing incorrect tool routing when MCP server names contain underscores (e.g., `my_server_tool` vs `my_server`).

### 7. Fix single-line SKILL.md frontmatter parsing
🔗 [PR #28042](https://github.com/google-gemini/gemini-cli/pull/28042) — New today (help wanted)  
Fixes skill discovery failure when the `description` field in `SKILL.md` frontmatter is on a single line. Affected skills were completely invisible in `/skills list`.

### 8. Strip trailing periods from error URLs
🔗 [PR #28054](https://github.com/google-gemini/gemini-cli/pull/28054) — New today (help wanted)  
Removes sentence-ending periods attached directly to HTTP(S) URLs in error messages, making rendered links navigable again.

### 9. Atomic MCP OAuth token writes
🔗 [PR #27664](https://github.com/google-gemini/gemini-cli/pull/27664) — P1, closed  
Writes MCP OAuth token files through a temp file and atomic rename, preventing partial writes and data corruption.

### 10. CI: validate workflow_run origin for E2E artifact poisoning
🔗 [PR #27753](https://github.com/google-gemini/gemini-cli/pull/27753) — P1, open  
Fixes a security vulnerability where the chained E2E pipeline could be poisoned by fork PRs, allowing attacker-controlled code to run with repository secrets.

---

## Feature Request Trends

1. **AST-aware code understanding** — Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746), [#22747](https://github.com/google-gemini/gemini-cli/issues/22747)) propose using AST-aware tools for file reads, search, and codebase mapping to reduce token usage and improve precision.

2. **Agent self-awareness and tool adoption** — Users want the agent to autonomously use custom skills and sub-agents ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)) and understand its own CLI flags, hotkeys, and mechanics ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)).

3. **Memory system improvements** — Requests for deterministic redaction of secrets, deduplication of patches, and handling of malformed inbox patches ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523), [#26516](https://github.com/google-gemini/gemini-cli/issues/26516)).

4. **Browser agent resilience** — Feature requests for automatic session takeover, lock recovery, and honoring `settings.json` overrides ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232), [#22267](https://github.com/google-gemini/gemini-cli/issues/22267)).

5. **Remote agents with advanced auth** — An EPIC ([#20303](https://github.com/google-gemini/gemini-cli/issues/20303)) tracking task-level authentication, 1P agent support, and background processing for remote agent scenarios.

---

## Developer Pain Points

- **Agent hanging and false success reports** — Issues [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) (generalist agent hangs), [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) (false GOAL on MAX_TURNS), and [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) (shell command stuck on input) together represent the most impactful reliability concerns.

- **Configuration and settings not honored** — The Browser Agent ignores `settings.json` ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), sub-agents run despite being disabled ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)), and MCP OAuth refresh breaks for auto-discovered servers ([#27889](https://github.com/google-gemini/gemini-cli/issues/27889)).

- **File and tool corruption** — Jupyter Notebook/JSON corruption in `write_file` ([#28000](https://github.com/google-gemini/gemini-cli/pull/28000)), template substitution corrupting `$` sequences ([#28055](https://github.com/google-gemini/gemini-cli/pull/28055)), and `@`-prefixed path resolution failures ([#28053](https://github.com/google-gemini/gemini-cli/pull/28053)) all impair day-to-day file operations.

- **Tool overload and poor scope management** — The 128-tool limit causing 400 errors ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)) and agents failing to use available skills ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)) point to a gap in how the model manages its tool set.

- **Platform-specific regressions** — Wayland browser agent failures ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)), Thai/Lao character rendering bugs ([#25385](https://github.com/google-gemini/gemini-cli/pull/25385)), and terminal resize flicker ([#21924](https://github.com/google-gemini/gemini-cli/issues/21924)) continue to affect users on non-standard setups.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-20

## 1. Today's Highlights

The team shipped **v1.0.64-1** with two notable additions: `/branch` as an alias for `/fork` (aligning with Claude Code) and an experimental `--worktree` flag for isolated session environments. Meanwhile, community frustration is building around **MCP server breakage on Windows** (Issue #3455) and **silent hangs on stalled HTTPS sockets** (Issue #3371), both unresolved for weeks. A fresh wave of triage issues surfaced today, including UI freezes (Issue #3868) and invisible reasoning text on dark terminals (Issue #3866).

## 2. Releases

**[v1.0.64-1](https://github.com/github/copilot-cli/releases/tag/v1.0.64-1)** — *Just released*
- **`/branch` alias**: Added as an alternative to `/fork`, matching Claude Code's command naming convention.
- **Experimental `--worktree` flag**: Use `-w [name]` (enabled via `/experimental`) to create or reuse a git worktree under `<repo>.worktrees/` and start the session inside it.
- **Tab completion**: Added for `/agent n`.

*(No other releases in the last 24 hours.)*

## 3. Hot Issues

1. **[#3455](https://github.com/github/copilot-cli/issues/3455) – github-mcp-server fails with "fetch failed" on Windows since v1.0.51** (OPEN, 2 comments)  
   A regression that broke the built-in MCP server for Windows users. No connection attempts existed pre-1.0.51; now the feature is unusable on that platform. **Why it matters**: MCP is central to Copilot's extensibility; a platform-specific regression undermines trust in updates.

2. **[#3371](https://github.com/github/copilot-cli/issues/3371) – CLI silently hangs on stalled HTTPS sockets to api.github.com** (OPEN, 1 comment, 👍1)  
   Copilot can hang indefinitely with no timeout, no log output, and no TUI feedback. This is a critical reliability issue for automated pipelines. **Community reaction**: Limited engagement so far, but the severity is high.

3. **[#731](https://github.com/github/copilot-cli/issues/731) – Z shell + direnv: Invalid session ID** (CLOSED, 13 comments, 👍14)  
   After months of discussion, this longstanding compatibility issue with Z shell and direnv was finally closed. **Why it matters**: Z shell users are a significant portion of the developer audience.

4. **[#1665](https://github.com/github/copilot-cli/issues/1665) – Plugin scoping to project/repository** (CLOSED, 7 comments, 👍17)  
   The community's most-upvoted feature request this period—plugins are now scoped per-project instead of globally. **Why it matters**: Enables team workflows where different repos need different plugin configurations.

5. **[#1901](https://github.com/github/copilot-cli/issues/1901) – autopilot_fleet plan approval race condition** (OPEN, 2 comments)  
   Selecting "Accept plan and build on autopilot + /fleet" may not activate fleet mode immediately; one user reported a 50-minute delay. **Why it matters**: Race conditions in plan approval undermine trust in autonomous mode.

6. **[#3869](https://github.com/github/copilot-cli/issues/3869) – /ask answer displayed in cramped text box** (OPEN, triage, 0 comments)  
   The `/ask` feature returns multi-line responses in a tiny viewport, making comprehension difficult. **Why it matters**: Directly impacts daily usability of a core feature.

7. **[#3868](https://github.com/github/copilot-cli/issues/3868) – App hangs when right-clicking a chat/session with multiple open** (OPEN, triage, 0 comments)  
   A reproducible UI freeze in the app. **Why it matters**: Multi-session users—common in complex workflows—are blocked.

8. **[#3867](https://github.com/github/copilot-cli/issues/3867) – No context window visibility or compaction notification** (OPEN, triage, 0 comments)  
   Users have no idea how much context remains or when compaction silently occurs. **Why it matters**: Essential for understanding session behavior and avoiding unexpected truncation.

9. **[#3866](https://github.com/github/copilot-cli/issues/3866) – Thinking/reasoning text unreadable on dark backgrounds** (OPEN, triage, 0 comments)  
   Hardcoded dim foreground color makes reasoning text nearly invisible on dark themes. **Why it matters**: Accessibility regression affecting a large segment of developers.

10. **[#3696](https://github.com/github/copilot-cli/issues/3696) – Auto-update downloads wrong package on Alpine/musl** (CLOSED, 0 comments, 👍1)  
    Auto-updater fetched `linux-x64` instead of `linuxmusl-x64`, breaking runtime.node loading. **Why it matters**: Containerized and CI/CD users on Alpine are a growing audience.

## 4. Key PR Progress

*(No pull requests were updated in the last 24 hours.)*

No new PRs or PR updates were detected in this digest window. Activity remains focused on issue triage and the v1.0.64-1 release.

## 5. Feature Request Trends

The following directions stand out from recent issues:

- **Project-scoped plugins** (👍17 on #1665): After closure, this is the leading requested pattern—plugins should be configurable per repository, not globally.
- **LLM-invocable `cd` tool** (#3865): Users want Copilot to automatically update the working directory in the status bar when switching worktrees, or expose a `/cd` tool for controlled navigation.
- **Context window visibility** (#3867): A clear desire for a UX indicator showing token usage and compaction events, similar to how model names are displayed.
- **Cross-editor MCP schema compatibility** (#3835): Requests for a unified `mcp.json` format that works across VS Code, Copilot CLI, and other editors.

## 6. Developer Pain Points

Recurring frustrations in this digest:

- **Platform-specific regressions**: Windows MCP failures (#3455) and Alpine musl auto-update breaks (#3696) show that cross-platform QA remains a pain point.
- **Silent failures and timeouts**: Stalled HTTPS sockets (#3371) and hooks silently bypassed under parallel tool calls (#2893) erode trust in the CLI's reliability.
- **Plugin path brittleness**: Absolute `cache_path` in config (#3864) breaks in Docker, Nix, and multi-HOME environments—a classic containerization headache.
- **UI/UX regressions**: The `/ask` cramped box (#3869) and dark-mode invisibility (#3866) suggest insufficient UI testing across terminal configurations.
- **Update flow defects**: Running `/update` from a resumed session (#3821) passes conflicting flags, forcing a restart instead of a seamless update.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-20

## Today's Highlights
The repository saw a quiet day with no new releases or updated issues, but one notable PR (#2463) was opened to fix a proxy-awareness gap in the `FetchURL` module. While the overall community activity is low, the fix addresses a genuine environment-configuration pain point that affects users behind corporate or local proxies. No new feature requests or bug reports surfaced in the last 24 hours.

## Releases
No new releases in the last 24 hours.

## Hot Issues
No issues were updated in the last 24 hours (total: 0 items). The issue tracker remains dormant for this period.

## Key PR Progress
**#2463 — fix: respect system proxy settings in FetchURL**  
🔗 [PR Link](https://github.com/MoonshotAI/kimi-cli/pull/2463)  
**Author:** itxaiohanglover | **Created:** 2026-06-19 | **Updated:** 2026-06-19 | **👍 Reactions:** 0  
**Summary:**  
`FetchURL` uses `aiohttp.ClientSession`, which does **not** read `HTTP_PROXY`/`HTTPS_PROXY` environment variables by default. In environments that require a proxy (e.g., corporate networks), this causes `Connection reset by peer` failures. The PR adds explicit proxy configuration to the session, enabling system proxy awareness.  
**Why it matters:** This is a low-overhead, high-impact fix for any user behind a proxy. The PR is still open and has received no comments yet, but its value is clear for enterprise and restricted-network adopters.

## Feature Request Trends
No new feature requests were recorded in the last 24 hours. The overall trend from the broader repository history (not shown here) continues to center on:
- Improved local model execution support
- Richer context handling for large file ingestion
- Custom tool/plugin integration points

## Developer Pain Points
No new pain points emerged today. Historical patterns (not visible in this digest window) indicate recurring frustrations around:
- Environment-specific connectivity failures (now being addressed by PR #2463)
- Lack of consistent error messages for network-related failures
- Manual configuration overhead for proxy and firewall environments

---

*All data sourced from [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) as of 2026-06-20.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-20

## Today's Highlights
MCP client development is accelerating, with a stacked series of PRs adding resource subscriptions, templates, and completions. Meanwhile, a critical CPU spin bug (#32965) and a multi-threaded crash on Apple Silicon (#32694) are creating reliability headaches for users on larger projects. The community's hunger for sandboxing (#2242, 74 comments) and full MCP compliance (#28567) remains the dominant feature signal.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **#20695 — Memory Megathread** (98 comments, 71 👍)
   Centralized memory leak tracking. Maintainers are asking for heap snapshots, not LLM-suggested fixes.
   [GitHub](https://github.com/anomalyco/opencode/issues/20695)

2. **#2242 — Sandbox the agent** (74 comments, 55 👍)
   Long-running request to restrict terminal/file access per directory. Community compares gemini-cli/Codex seatbelt patterns.
   [GitHub](https://github.com/anomalyco/opencode/issues/2242)

3. **#988 — MCP remote via OAuth** (39 comments, 95 👍)
   Strong demand for OAuth 2.1–based MCP server auth. Would eliminate secret/copied-token workflows.
   [GitHub](https://github.com/anomalyco/opencode/issues/988)

4. **#16017 — Go plan usage API endpoint** (19 comments, 70 👍)
   Expose subscription usage data via public API for dashboard-level visibility. High community demand.
   [GitHub](https://github.com/anomalyco/opencode/issues/16017)

5. **#28567 — Full MCP client capabilities** (17 comments, 24 👍)
   Gap analysis between OpenCode's MCP client and the latest spec. Multiple PRs now reference this issue.
   [GitHub](https://github.com/anomalyco/opencode/issues/28567)

6. **#32965 — CPU spin at ~100% after bootstrap** (4 comments, 0 👍)
   Main thread pins a core indefinitely on large projects. No logs, ignores SIGTERM. Critical for CI/headless users.
   [GitHub](https://github.com/anomalyco/opencode/issues/32965)

7. **#32694 — SIGTRAP crash on Apple Silicon** (2 comments, 3 👍)
   Bundled Bun 1.3.14 triggers HTTP client thread crash after first message. Session becomes unusable.
   [GitHub](https://github.com/anomalyco/opencode/issues/32694)

8. **#32444 — GLM-5.2 thinking-effort variants blocked** (6 comments, 12 👍)
   Blanket `glm` exclusion in `variants()` hides High/Max thinking levels. Users want full model features exposed.
   [GitHub](https://github.com/anomalyco/opencode/issues/32444)

9. **#33035 — MCP tool calls should carry session_id** (3 comments, 0 👍)
   Inject current session context into MCP tool requests so servers can correlate operations. Architectural improvement.
   [GitHub](https://github.com/anomalyco/opencode/issues/33035)

10. **#31119 — Error: no such column: name** (6 comments, 5 👍)
    DB schema mismatch after upgrade. Blocks all usage. No plugin involvement reported.
    [GitHub](https://github.com/anomalyco/opencode/issues/31119)

## Key PR Progress

1. **#32943 — MCP resource templates & completion**
   Adds `resources/templates/list` support. References #28567. Stacked on #32936.
   [GitHub](https://github.com/anomalyco/opencode/pull/32943)

2. **#32936 — MCP resource subscriptions**
   Subscribe to resource change notifications from servers. Third in a series toward full MCP compliance.
   [GitHub](https://github.com/anomalyco/opencode/pull/32936)

3. **#32478 — MCP resource list change events**
   Register for and propagate `resources/list` changes. Foundation for dynamic resource discovery.
   [GitHub](https://github.com/anomalyco/opencode/pull/32478)

4. **#8535 — Bi-directional cursor pagination**
   Adds cursor-based pagination for session messages across all surfaces. Closes #6548.
   [GitHub](https://github.com/anomalyco/opencode/pull/8535)

5. **#33042 — Ultra Mode autonomous agent** (needs:compliance)
   Hardcoded state machine with plan->build->verify->loop. Adds phase-filtered tooling and auto-test detection.
   [GitHub](https://github.com/anomalyco/opencode/pull/33042)

6. **#32089 — Fix doom loop detection across messages**
   Detection previously limited to current message only. Now tracks loops across the full conversation.
   [GitHub](https://github.com/anomalyco/opencode/pull/32089)

7. **#33019 — Inline skill picker in TUI**
   Type `$` as a token to open a skill browser. References three related issues (#20982, #15617, #29217).
   [GitHub](https://github.com/anomalyco/opencode/pull/33019)

8. **#33010 — Android/Termux support**
   Adds platform handling for `os.platform() === "android"`, enabling installs on Termux. Closes four issues.
   [GitHub](https://github.com/anomalyco/opencode/pull/33010)

9. **#28921 — Include shell command/file path in permission prompts**
   Makes ACP allow/deny dialogs more informative. Closes #4240.
   [GitHub](https://github.com/anomalyco/opencode/pull/28921)

10. **#30211 — Fix config precedence after model hooks**
    Ensures `provider.models()` hook results respect later config merges. Closes #25630.
    [GitHub](https://github.com/anomalyco/opencode/pull/30211)

## Feature Request Trends

- **MCP spec compliance** (#28567, #33035, #988): Full resource notifications, templates, completions, and OAuth-based remote servers. This is the single most active front.
- **Agent sandboxing** (#2242, #23923): Directory-scoped file/terminal access, plus CLI `/disconnect` from mistaken provider connections.
- **Usage/plan visibility** (#16017, #30276): Public API for subscription consumption data; billing confusion remains a pain point.
- **Model reasoning exposure** (#32444, #33013): Request for providers to expose thinking/reasoning field schemas for custom models, not just built-in ones.
- **Session context in MCP** (#33035): MCP servers should receive session_id for observability and correlation.

## Developer Pain Points

- **Memory leaks** (#20695): Chronic, hard to debug. Maintainers require heap snapshots, not AI-suggested fixes. Top-voted issue.
- **Crash loops on Apple Silicon** (#32694, #32965): SIGTRAP and 100% CPU spins after model streaming. Devastating for M1/M2 users and headless workflows.
- **UI regression in desktop app** (#29829, #31878, #32746): Missing console terminal, "open in Explorer," freezing in v1.17.x. The new/old layout toggle doesn't restore all features.
- **WSL2/VS Code context sync broken** (#29570): Editor focus and selections no longer attach automatically. No clear cause; environment-sensitive.
- **Orphaned lock files** (#29413): Ungraceful shutdown leaves `index.lock` in snapshot git dir, blocking future operations on Windows.
- **Ctrl+Z suspends on Linux** (#24817): SIGTSTP sent instead of undo. Annoying for terminal-heavy workflows.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-20

## Today's Highlights
Version 0.79.8 ships with a modular base-entry-point system that lets SDK users strip unused provider transports from bundles. A persistent streaming-scroll bug (Issue #5825) has an open fix in PR #5846, while a dangerous data-loss edge case in the `edit` tool's fuzzy matching (Issue #5899) was closed by PR #5898. Community focus remains on provider compatibility, session performance, and Windows/CJK path handling.

## Releases
**v0.79.8** introduces selective provider base entry points (`@earendil-works/pi-ai/base`, `@earendil-works/pi-agent-core/base`). SDK users can now pair these with explicit provider registration to exclude unused transports from final bundles—reducing package size for custom integrations. Full release: [v0.79.8](https://github.com/earendil-works/pi/releases/tag/v0.79.8)

## Hot Issues (Top 10)

1. **#5825 – Streaming markdown forces scroll to bottom** ([Issue](https://github.com/earendil-works/pi/issues/5825))  
   *Status: OPEN, 24 comments*  
   When `clear on shrink` is enabled, the TUI auto-scrolls to the bottom during streaming markdown output, breaking the user's reading position. High community engagement on reproduction steps.

2. **#5897 – Unavailable models offered in Copilot integration** ([Issue](https://github.com/earendil-works/pi/issues/5897))  
   *Status: CLOSED, 9 comments*  
   Copilot login exposes non-functional model options (e.g., Opus, GPT nano). Quickly resolved—an important UX fix for Copilot subscribers.

3. **#5909 – Coalesce rapid thinking_level_change entries** ([Issue](https://github.com/earendil-works/pi/issues/5909))  
   *Status: CLOSED, 1 comment*  
   Rapidly cycling thinking levels bloat session JSONL files with hidden entries that compaction doesn't clean, degrading TUI performance. Filed and closed same day.

4. **#5871 – Anthropic OAuth-token detection is hardcoded** ([Issue](https://github.com/earendil-works/pi/issues/5871))  
   *Status: OPEN, 2 comments*  
   The `isOAuthToken()` check is a hardcoded substring match; users need an explicit config flag for custom providers using OAuth/Bearer credentials.

5. **#5899 – edit tool fuzzy match silently rewrites the whole file** ([Issue](https://github.com/earendil-works/pi/issues/5899))  
   *Status: CLOSED, 2 comments*  
   Fuzzy edits strip trailing whitespace and normalize unicode across the entire file—a subtle data-loss vector. Quickly addressed by PR #5898.

6. **#5906 – Bash and Read tools display only preview lines** ([Issue](https://github.com/earendil-works/pi/issues/5906))  
   *Status: CLOSED, 1 comment*  
   Hardcoded preview limits (5 lines for bash, 10 for read) when `expanded=false` contradict user expectations; patch merged same day.

7. **#5904 – bash tool cwd parameter is silently dropped** ([Issue](https://github.com/earendil-works/pi/issues/5904))  
   *Status: CLOSED, 1 comment*  
   The bash tool's schema lacks a `cwd` field, so models passing one get silent no-ops—especially problematic when the session worktree is deleted.

8. **#5907 – `pi.setActiveTools` cannot hide built-in read tool** ([Issue](https://github.com/earendil-works/pi/issues/5907))  
   *Status: CLOSED, 1 comment*  
   SDK API claim can't actually suppress the `read` tool; reported as a bug preventing context size management.

9. **#5905 – Optimize same-directory session switching speed** ([Issue](https://github.com/earendil-works/pi/issues/5905))  
   *Status: CLOSED, 1 comment*  
   `/new`, `/resume`, `/fork` unnecessarily reload extensions when the working directory is unchanged. Request to skip extension init for fast session swaps.

10. **#5804 – Fast Sessions (SQLite storage)** ([Issue](https://github.com/earendil-works/pi/issues/5804))  
    *Status: OPEN, 2 comments*  
    Proposal to support SQLite session storage alongside JSONL. Aims to fix slow session loading and searching—critical for users with many sessions.

## Key PR Progress (Top 10)

1. **#5846 – fix(tui): stabilize streaming code fence rendering** ([PR](https://github.com/earendil-works/pi/pull/5846))  
   *Status: OPEN*  
   Fixes Issue #5825 (forced scroll to bottom) by stabilizing rendering during streaming code fences. Author xl0 is actively iterating.

2. **#5898 – fix(coding-agent): preserve untouched content in fuzzy edit matches** ([PR](https://github.com/earendil-works/pi/pull/5898))  
   *Status: CLOSED*  
   Closes Issue #5899. Prevents entire-file rewrites on fuzzy matches, preserving whitespace and unicode normalization only where edits apply.

3. **#5509 – feat: Add Amazon Bedrock Mantle OpenAI Responses provider** ([PR](https://github.com/earendil-works/pi/pull/5509))  
   *Status: OPEN*  
   New provider supporting GPT 5.5/5.4 via AWS Bedrock Mantle. Modeled after Azure provider; adds significant cloud-deployment flexibility.

4. **#5866 – feat(ai): add OpenRouter Fusion alias** ([PR](https://github.com/earendil-works/pi/pull/5866))  
   *Status: CLOSED*  
   Adds `openrouter/fusion` as a synthetic router alias, giving users access to OpenRouter's Fusion routing capability without tool-capability conflicts.

5. **#5900 – feat(coding-agent): emit OSC 9998/9999 for freecode-web adapter** ([PR](https://github.com/earendil-works/pi/pull/5900))  
   *Status: CLOSED*  
   Enables real-time status, cost, and context display in the freecode-web PTY UI by emitting custom escape sequences.

6. **#4794 – chore: run pi-test through tsx** ([PR](https://github.com/earendil-works/pi/pull/4794))  
   *Status: CLOSED*  
   Fixes test runner to properly exercise TypeScript source tree by running through tsx instead of node, resolving workspace import resolution issues.

7. **#5356 – docs: add containerization guide and Gondolin example** ([PR](https://github.com/earendil-works/pi/pull/5356))  
   *Status: CLOSED*  
   Documentation PR adding a containerization guide with a Gondolin deployment example—useful for self-hosters.

8. **#5509 – (see above – Amazon Bedrock Mantle provider)**

9. **#5845 – Compaction-related fixes** ([PR](https://github.com/earendil-works/pi/issues/5845)) – *CLOSED*  
   Three small fixes to compaction: reduces parallel bursts for local models, improves efficiency for resource-constrained setups.

10. **#5795 – Configurable `sequentialCompaction` option** ([PR](https://github.com/earendil-works/pi/issues/5795)) – *CLOSED*  
    Adds per-model `sequentialCompaction: boolean` flag. When true, compaction summarizations run sequentially—critical for users running local models with limited GPU/CPU.

## Feature Request Trends

The community's most-requested feature directions this week:

- **Provider extensibility & compatibility** – Multiple requests to make OAuth token detection configurable (Issue #5871), support custom bearers for Codex Responses (Issue #5152), and handle Moonshot/Kimi schema validation quirks (Issue #5822). The OpenRouter Fusion alias (PR #5866) and Amazon Bedrock Mantle provider (PR #5509) show momentum toward cloud-provider diversity.

- **Session performance & storage** – Strong demand for SQLite-based session storage (Issue #5804), faster same-directory session switching (Issue #5905), and coalescence of rapid thinking-level changes (Issue #5909) to prevent JSONL bloat. Compaction improvements (Issue #5845, PR #5795) address local-model resource constraints.

- **Edit tool safety & precision** – Following the data-loss scare in Issue #5899, there is renewed community attention on ensuring the `edit` tool preserves untouched content during fuzzy matches and respects `setActiveTools` for disabling built-in tools (Issue #5907).

- **Customizable system prompts** – Requests for tool prompt placeholders in custom `SYSTEM.md` (Issue #4789) and for exposing thinking-level ranges per model (Issue #5831) indicate users want fine-grained control over agent behavior.

- **Terminal/TUI ergonomics** – `/tree` cursor navigation ergonomics (Issue #5225), tmux warning suppression (Issue #5815), and an `/update` command (Issue #2729) are small but high-impact quality-of-life asks.

## Developer Pain Points

- **Provider schema incompatibility** – Moonshot/Kimi models reject Pi's OpenAPI-style tool schemas with `allOf` if/then conflicts (Issue #5822). Developers need to maintain provider-specific schema transformers.

- **Windows/CJK path handling** – The `edit` tool still fails on Korean-character paths (Issue #4425), and bash variable escaping is broken under WSL (Issue #5893). These are long-standing platform bugs.

- **Session bloat from hidden events** – `thinking_level_change` entries (Issue #5909) and optional tool-output fields bloat session files silently, causing TUI slowdowns. Compaction doesn't clean these.

- **Hardcoded limits in core tools** – The `bash` and `read` tools hardcode preview line counts (Issue #5906). The `cwd` parameter is silently dropped for `bash` (Issue #5904). These frustrate automated workflows.

- **Init-time overhead** – Extension loading on session switch is unnecessarily expensive (Issue #5905), and `pi.setActiveTools` cannot actually disable built-in `read` (Issue #5907), requiring workarounds for context management.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-20

## Today's Highlights
The Qwen Code community saw a burst of bugfix activity, with **42 issues and 50 PRs** updated in the last 24 hours. A major theme is **cross-platform compatibility**: five bugs were fixed around Windows path parsing (colons in file paths, uppercase URL schemes, drive-letter handling). The QQ Bot channel also received critical fixes for infinite reconnect loops and token refresh failures that could silently break long-running daemons. Meanwhile, feature discussions continue around **multi-agent communication enhancements** and **automatic model tier switching** (pro vs. flash) to reduce costs.

---

## Releases
*No new releases in the last 24 hours.*

---

## Hot Issues (Top 10)

1. **[#5267 — `context.fileName` in setting file doesn't work?](https://github.com/QwenLM/qwen-code/issues/5267)**  
   User `fantasyz` reports that the documented `context.fileName` setting to customize which files are attached to prompts isn't functioning. With 9 comments and no maintainer resolution yet, this is the most active open bug. *Impact: blocks a documented configuration feature.*

2. **[#5180 — Subagent crashes mid-task, main session unaware](https://github.com/QwenLM/qwen-code/issues/5180)**  
   A detailed Chinese-language report describes a multi-agent architecture flaw: the main session (project manager) never learns when a subagent crashes mid-execution. User built a workaround using file-based monitoring. *Impact: core reliability gap for multi-agent workflows.*

3. **[#5142 — CLI virtualized history mode not visible](https://github.com/QwenLM/qwen-code/issues/5142)**  
   A usability bug where CLI history is invisible unless the user presses `/`. The input box also appears in the wrong position. *Impact: degrades day-to-day CLI experience.*

4. **[#5422 — `PostToolUse` hook's `updatedMCPToolOutput` field is dead code](https://github.com/QwenLM/qwen-code/issues/5422)**  
   Community member `ken-jo` discovered that a hook output field promising MCP tool output rewriting is declared but never consumed by the runtime. *Impact: misleading API surface; fixed quickly in PR #5423.*

5. **[#5239 — Subagent ↔ main session communication is too weak](https://github.com/QwenLM/qwen-code/issues/5239)**  
   Feature request from the same user as #5180, asking for bidirectional communication between subagents and the main session, with a notification mechanism when subagents complete or fail. *Community reaction: 4 comments, all agreeing this is a blocker for serious multi-agent use.*

6. **[#5428 — Agent falsely enters Plan mode without consent](https://github.com/QwenLM/qwen-code/issues/5428)**  
   User `fantasyz` reports a recent regression where the agent spontaneously enters Plan mode and repeatedly tries to `ExitPlanMode` even when the user never enabled it. *Impact: breaks normal interactive flow.*

7. **[#4951 — Are `in/out tokens` in the statusline accurate?](https://github.com/QwenLM/qwen-code/issues/4951)**  
   User `stevenxhyl2026` questions the token counter, reporting that a few sentences generates "hundreds of thousands" of tokens. *Community reaction: 4 comments, likely a display or counting bug.*

8. **[#4063 — Core + CLI architecture review — 12 structural issues](https://github.com/QwenLM/qwen-code/issues/4063)**  
   A comprehensive arch review listing P0 problems like the core type system being tightly coupled to `@google/genai` (136 files importing it). *Community reaction: 3 comments, 1 👍. Maintainer attention needed.*

9. **[#4814 — UI should make adding custom provider models easier](https://github.com/QwenLM/qwen-code/issues/4814)**  
   Feature request noting that after initial wizard setup, users cannot easily add new models to a Custom Provider via the UI. *Impact: friction for power users managing multiple models.*

10. **[#3361 — Agent misinterprets successful shell output as empty](https://github.com/QwenLM/qwen-code/issues/3361)**  
    A long-standing bug (since April) where the agent executes shell commands successfully but claims output is empty when using OpenAI-compatible APIs. *Community reaction: 5 comments, no fix yet.*

---

## Key PR Progress (Top 10)

1. **[#4850 — Interactive multi-tab `/extensions` manager](https://github.com/QwenLM/qwen-code/pull/4850)**  
   A large feature PR by `BZ-D` that transforms the extension list into a full manager with Installed/Discover/Sources tabs. Still open; a major UX improvement for extension lifecycle.

2. **[#5429 — Fix: accept uppercase URL schemes in extension install parsing](https://github.com/QwenLM/qwen-code/pull/5429)**  
   Fixes case-sensitive URL scheme matching (`http://` vs `HTTP://`) in the extension install source parser. Freshly opened, addresses a cross-platform compatibility gap.

3. **[#5396 — Reduce UI flicker: throttle + compact transition + batch STREAM_TEXT](https://github.com/QwenLM/qwen-code/pull/5396)**  
   Targets reported flicker issues on Windows (Ctrl+O compact mode, infinite refresh loops). Uses throttling and React `startTransition`. Still open for review.

4. **[#5398 — Add extension management to web shell and daemon](https://github.com/QwenLM/qwen-code/pull/5398)**  
   Closed, ready for merge. Brings `/extensions install` and management UI to the web shell, making extensions accessible outside the CLI. Important for non-CLI users.

5. **[#5426 — Accept uppercase URL schemes in `mcp add` transport detection](https://github.com/QwenLM/qwen-code/pull/5426)**  
   Companion fix to #5429, but for the MCP command. Closed quickly after being opened — a sign of responsive triage.

6. **[#5409 — Block broad shell self-kill commands](https://github.com/QwenLM/qwen-code/pull/5409)**  
   Closes the security gap where an agent could accidentally kill its own process via `taskkill`, `killall`, `pkill` before permission logic runs. Merged same day — high priority fix.

7. **[#5415 — Bound QQ Bot gateway reconnect retries](https://github.com/QwenLM/qwen-code/pull/5415)**  
   Fixes the infinite retry loop discovered in issues #5410–#5413. Now counts gateway reconnect attempts correctly and prevents indefinite 60s retries. Closed same day.

8. **[#5423 — Remove dead `updatedMCPToolOutput` field](https://github.com/QwenLM/qwen-code/pull/5423)**  
   Quick surgical fix for #5422. Removes a field that was declared but never consumed. Demonstrates responsive community-driven cleanup.

9. **[#5418 — Narrow settings enum schemas](https://github.com/QwenLM/qwen-code/pull/5418)**  
   Tightens string settings to proper enums (`tree` or `flat` for import format; `ipv4first` or `verbatim` for DNS resolution). Improves schema correctness and IDE integration.

10. **[#5030 — Resume interrupted turns without synthetic "continue" message](https://github.com/QwenLM/qwen-code/pull/5030)**  
    A design-focused PR that adds first-class continuation support for resumed sessions, avoiding fake `"continue"` messages. Still open; touches core, CLI, and SDK.

---

## Feature Request Trends

- **Multi-agent communication upgrade** (#5180, #5239): Multiple requests for bidirectional, reliable communication between main sessions and subagents, with crash notification and progress monitoring.
- **Automatic model tier switching** (#5225): Several users want the client to automatically choose between pro and flash model variants based on task complexity to reduce cost.
- **Extension management UX** (#4850, #5398, #4909): A clear push for richer extension lifecycle management — multi-tab UI, archive install support, and web-shell integration.
- **Custom provider model management** (#4814): Users want the ability to add new models to existing custom providers without re-running the setup wizard.
- **Token transparency** (#4951): Users are skeptical about displayed token counts; request for accurate counters or documentation.
- **Persistent history controls** (#5142, #4085): Requests for better CLI history visibility and collapse-on-resume preferences.

---

## Developer Pain Points

1. **Windows path handling is fragile** — Multiple bugs in the last 24 hours (#5386, #5370, #5426, #5429) show that colon-separated parsing and case sensitivity break consistently on Windows. Paths like `C:\Users` or `HTTPS://` are misparsed.

2. **QQ Bot channel reliability** — A cluster of issues (#5410–#5413) revealed serious daemon-halting bugs: infinite reconnect loops, token refresh failures with no retry, and race conditions in session file paths. Three PRs landed to fix these same-day.

3. **Agent autonomy vs. user control** — #5428 (forced Plan mode) and #5422 (dead hook field) highlight a tension: the agent is becoming more autonomous, but sometimes in ways users don't expect or can't control.

4. **Multi-agent reliability** — #5180 and #5239 both describe a brittle subagent model where failures are invisible to the orchestrator. Users are building custom workarounds (file monitors, timeout checks) to compensate.

5. **Long-standing bugs without fixes** — #3361 (empty shell output) and #5267 (`context.fileName` not working) have been open for weeks or months with community demand (5–9 comments each) but no maintainer resolution visible.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-20

## Today's Highlights
The v0.8.63 release cycle is accelerating with **24 pull requests** submitted in the last 24 hours, including a first-class sub-agent toggle (#3327) and critical reliability fixes. A major EPIC (staged command-boundary refactor, #2870) continues to drive architectural changes across the codebase, while Dependabot submitted 10 dependency update PRs in a single batch. The community flagged a glibc incompatibility on Ubuntu 22.04 LTS (#3238) and reported the missing sidebar in v0.8.62 (#3328), both warranting immediate attention.

---

## Releases
**No new releases** in the last 24 hours. The current stable version remains **v0.8.62**, with v0.8.63 preparation active across multiple feature branches.

---

## Hot Issues (Top 10 of 5 total active)

1. **[#2870] EPIC: staged command-boundary refactor for #2791** — *OPEN, Updated Jun 19*
   The backbone of v0.9.0 planning. Tracks smaller mergeable layers for the command-boundary refactor. Layer 4 (PR #3330) landed today. This EPIC is the single most important architectural signal for the project's direction.
   🏷️ *documentation, cleanup, tui* | [View Issue](Hmbown/CodeWhale Issue #2870)

2. **[#3238] glibc version mismatch on Ubuntu 22.04 LTS** — *OPEN, Updated Jun 19*
   `npm install -g codewhale` fails on Ubuntu 22.04 due to mismatched glibc. No workaround posted yet. Affects all users on older LTS distributions. Community waiting for either a static binary or a minimum glibc version bump.
   🏷️ *bug, reliability, v0.8.63* | [View Issue](Hmbown/CodeWhale Issue #3238)

3. **[#3328] v0.8.62 sidebar missing after upgrade** — *OPEN, Updated Jun 19*
   User reports sidebar disappeared post-upgrade despite `/sidebar` indicating "visible". Regression likely introduced in the TUI rendering layer. Only 1 comment so far — community needs repro steps.
   🏷️ *question* | [View Issue](Hmbown/CodeWhale Issue #3328)

4. **[#3324] Recommendation: mosaic-compress for long-context coding** — *OPEN, Updated Jun 19*
   External contributor promotes a stateless dialogue compression library for long-context scenarios. Could influence the project's memory/context management direction if adopted.
   🏷️ *(no labels)* | [View Issue](Hmbown/CodeWhale Issue #3324)

5. **[#3320] Alibaba Cloud Bailian API key not integrated** — *OPEN, Updated Jun 19*
   `maomaochong998` requests integration for Alibaba Cloud's Bailian model API (阿里云百炼). Highlights growing demand for Chinese cloud provider support in the TUI ecosystem.
   🏷️ *bug* | [View Issue](Hmbown/CodeWhale Issue #3320)

---

## Key PR Progress (Top 10 of 24 active)

1. **[#3327] v0.8.63: Add first-class sub-agent toggle** — *BovmantH, Updated Jun 19*
   Introduces `/config subagents on|off|status` command. Session-only changes go live immediately; persisted changes write to config file. Critical for multi-agent workflows.
   [View PR](Hmbown/CodeWhale PR #3327)

2. **[#3345] refactor(config): move inline tests to module** — *cyq1017, Updated Jun 19*
   Closes #3307. Moves large inline test block from `lib.rs` to dedicated `tests.rs`, reducing production file size and merge conflicts. Clean architecture win.
   [View PR](Hmbown/CodeWhale PR #3345)

3. **[#3344] fix(tui): retry Codex responses requests** — *cyq1017, Updated Jun 19*
   Fixes #3019. Routes `/codex/responses` through `send_with_retry`, rebuilding request body/headers per attempt. Solves flaky streaming responses.
   [View PR](Hmbown/CodeWhale PR #3344)

4. **[#3330] Layer 4: replay FEAT-005 command extraction on Hunter** — *aboimpinto, Updated Jun 19*
   Refs #2870. Replays command extraction onto the Hunter architecture using trait-backed registry. Key step in the staged v0.9 refactor.
   [View PR](Hmbown/CodeWhale PR #3330)

5. **[#3331] fix(tui): enable proxy env for JS execution** — *cyq1017, Updated Jun 19*
   Fixes #3273. Propagates proxy environment variables to Node child processes. Mirrors lowercase and ALL_PROXY into uppercase names Node expects.
   [View PR](Hmbown/CodeWhale PR #3331)

6. **[#3332] fix(app-server): require auth for non-loopback binds** — *cyq1017, Updated Jun 19*
   Fixes #3258. Rejects non-loopback app-server binds without explicit auth token. Keeps loopback one-time token generation unchanged. Security hardening.
   [View PR](Hmbown/CodeWhale PR #3332)

7. **[#3329] fix(config): restore HuggingFace env precedence** — *gaord, Updated Jun 19*
   Restores HuggingFace API key precedence in TUI config surface, fixing CI/Lint gate. Prevents provider registry script failures on `main`.
   [View PR](Hmbown/CodeWhale PR #3329)

8. **[#3300] feat(tui): preserve thinking/tool blocks when seeding thread from session** — *gaord, Updated Jun 19*
   Replaces text-only `seed_thread_from_messages` with block-type-aware implementation. Preserves ContentBlock variants (Thinking, ToolUse, ToolResult) for full conversation reconstruction.
   [View PR](Hmbown/CodeWhale PR #3300)

9. **[#3321] fix(workflow): add token budget regulator for high fan-out agent runs** — *donglovejava, Updated Jun 19*
   Adds comprehensive token budget regulation for high fan-out sub-agent orchestration. Closes enforcement gap between protocol layer and runtime execution.
   [View PR](Hmbown/CodeWhale PR #3321)

10. **[#3333] refactor(tui): split MCP header helpers** — *cyq1017, Updated Jun 19*
    Moves HTTP header framing helpers into `mcp::headers` module. Prerequisite for the MCP transport split in #3310. Enables incremental review.
    [View PR](Hmbown/CodeWhale PR #3333)

---

## Feature Request Trends
- **Sub-agent orchestration**: First-class toggle (#3327) and token budgeting (#3321) indicate strong push toward multi-agent workflows as a core feature.
- **Provider expansion**: Alibaba Cloud Bailian API request (#3320) reflects growing need for Chinese cloud LLM integrations beyond OpenAI/Azure.
- **Long-context compression**: External recommendation for stateless dialog compression (#3324) suggests community interest in memory-bounded infinite conversation windows.
- **Thread fidelity**: Preserving thinking/tool blocks during session seeding (#3300) shows demand for lossless conversation history reconstruction.

---

## Developer Pain Points
- **glibc compatibility**: Ubuntu 22.04 LTS users cannot install via npm due to glibc mismatch (#3238) — no workaround available, blocking a significant Linux user base.
- **Sidebar regression**: v0.8.62 upgrade broke sidebar visibility (#3328) with unclear root cause, suggesting insufficient regression testing for TUI UI components.
- **Retry handling gaps**: Codex streaming still lacked retry logic until today's fix (#3344), causing flaky responses for users on unreliable networks.
- **Dependency churn**: 10 Dependabot PRs in one batch (tokio, similar, lru, toml, windows, plus 5 GitHub Actions) creates noise and potential breaking changes for maintainers to review.
- **Auth security gap**: Non-loopback binds could run without authentication (#3258, fixed in #3332) — a security issue that could expose app-server endpoints unintentionally.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*