# AI CLI Tools Community Digest 2026-07-21

> Generated: 2026-07-21 01:20 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Comparison Report
**Date:** 2026-07-21

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem is maturing rapidly, with seven major tools now serving distinct developer workflows. **Claude Code** and **OpenAI Codex** dominate community engagement by volume, while **Gemini CLI** and **Codewhale** (formerly DeepSeek-TUI) focus on agent reliability and provider neutrality. **GitHub Copilot CLI** has stabilized with rapid patch cycles but faces a surge of Windows regressions. **Kimi Code CLI** and **Qwen Code** represent the growing Asian-Pacific AI CLI presence, with Qwen showing particular strength in CI/CD automation infrastructure. The common thread across all tools is a painful transition from single-session reliability to multi-agent, multi-provider orchestration — and the billing complexity this introduces.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi CLI | OpenCode | Pi | Qwen Code | Codewhale |
|--------|------------|--------------|------------|-------------|----------|----------|-----|-----------|-----------|
| **Open Issues (Hot, today)** | 10 | 10 | 10 | 10 | 10 | 10 | 10 | 10 | 10 |
| **PRs (today)** | 6 | 10 | 10 | 0 | 4 | 10 | 10 | 10 | 10 |
| **Release today** | Yes (v2.1.216) | Yes (rust-v0.145.0-alpha.25) | No | Yes (v1.0.72, v1.0.73) | No | Yes (v1.18.4) | No | Yes (nightly) | No |
| **Release velocity** | Weekly + patches | Weekly + patches | Nightly builds | Daily patches | Weekly | Weekly | Moderate | Daily nightlies | Pre-v0.9.1 surge |
| **Top issue engagement** | 148 comments, 667 👍 | 208 comments, 358 👍 | 12 comments, 8 👍 | 4 comments, 4 👍 | 4 comments, 3 👍 | 20 comments, 13 👍 | 11 comments, 8 👍 | 7 comments (RFC) | 40 comments |

**Key insight:** Claude Code and OpenAI Codex have 10-50x more community engagement per issue than newer tools. However, **Qwen Code** and **Codewhale** show high PR throughput, indicating rapid iteration even with smaller user bases.

---

## 3. Shared Feature Directions

### Multi-Account / Multi-Profile Management
- **Claude Code** (#18435, 667👍): Desktop account switching for personal/work/client billing
- **Pi** (#5263, 8👍): Ephemeral in-session model changes without persisting

### Subagent Cost Control & Model Pinning
- **Claude Code** (#75055): Sub-agents inherit expensive models, no override capability
- **Gemini CLI** (#22093): Subagents run without permission despite "disabled" setting
- **Qwen Code** (#7315, #7316): OpenAI providers break subagent dispatch due to schema conflicts
- **Codewhale** (#4600): Auto-fork caching to reduce subagent cold-start costs

### Session Resilience & Persistence
- **Claude Code** (#62272): Chat history silently deleted despite retention settings
- **Kimi Code** (#2523): Context compaction resurrects completed/deleted tasks
- **OpenCode** (#23248): Sessions orphaned when project directory renamed
- **Pi** (#6820): Queued messages dropped during auto-compaction

### Background/Remote Session Management
- **Claude Code** (#49790): SSH remote sessions should survive client disconnect
- **OpenAI Codex** (#23200): Headless remote Linux hosts for mobile Codex
- **Gemini CLI** (#21409): Generalist agent hangs indefinitely

### Provider-Neutral Architecture
- **Codewhale** (#4644): Removing DeepSeek-specific fallback for provider-neutral state
- **Qwen Code** (#7316): Addressing OpenAI-compatible provider schema conflicts
- **Pi** (#6881): Using provider-reported costs instead of catalog calculations

### Windows Parity
- **Claude Code**: Text selection broken in VS Code terminal (#61021)
- **OpenAI Codex**: Multiple freezes/stutters on Windows 11 (#20214)
- **Kimi Code**: Migration tooling missing (#2522), broken arrow keys (#2521)
- **Codewhale**: Hooks process leak (#4489), Enter key lag (#4605)

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Qwen Code | Codewhale |
|-----------|------------|--------------|------------|-------------|-----------|-----------|
| **Core strength** | Depth of IDE integration | Rate-limit & cost management | Agent orchestration | GitHub ecosystem hooks | CI/CD automation | Provider-agnostic TUI |
| **Primary user** | Enterprise/desktop developers | Plus-plan power users | Google ecosystem devs | GitHub-centric teams | Asian-Pacific market | Multi-provider users |
| **Agent approach** | Workflow sub-agents | Managed permission profiles | Role-based (Generalist, etc.) | Code-review task agents | Autofix loop with CI fleet | Planner/Worker/Reviewer roles |
| **Release strategy** | Patch-then-stabilize | Weekly alpha releases | Nightly builds | Rapid daily patches | Nightly + autofix | Pre-release hardening |
| **Top pain point** | Data loss trust (#62272, #78273) | Rate-limit cost explosion (10-20x) | Agent hangs/freezes | Windows clipboard regressions | TokenPlan thinking restriction | Subagent cold-start cost |
| **Platform coverage** | macOS (best), Linux, Windows | macOS (best), Windows, mobile | Linux (best), macOS, Windows | Windows (regressing), macOS, Linux | Linux (best), Windows (weak) | Linux (best), Windows (growing) |

---

## 5. Community Momentum & Maturity

### Mature & High-Engagement
- **Claude Code**: Largest community by engagement volume (667👍 on top issue). Strong enterprise adoption signals. However, **trust erosion** from data-loss bugs (#62272, #78273) is a concerning trend.
- **OpenAI Codex**: Second-highest engagement (800👍 for Linux desktop request). Dominant conversation is rate-limit cost — a **pricing model crisis** that could drive churn.

### Rapidly Iterating
- **Qwen Code**: Highest PR volume of any tool this week (10+ merged). The autofix loop infrastructure (gate retry, real-time fork PR pickup, review-thread resolution) is technologically ambitious and shows strong engineering investment.
- **Codewhale**: 10 PRs in 24 hours targeting v0.9.1 stabilization. The rebrand from DeepSeek-TUI to Codewhale signals strategic pivot to provider agnosticism.

### Growing but Niche
- **Gemini CLI**: P1 bugs dominate (subagent recovery, shell hangs). Smaller community but strong Google ecosystem integration potential.
- **Pi**: Steady feature development (Amazon Bedrock, cost accuracy). The extension API surface is growing, suggesting plans for plugin ecosystem.

### Mature but Stalling
- **Copilot CLI**: Zero PRs today despite releasing two patches. The rapid release cycle masks underlying regressions (Windows clipboard, plan-mode lockdown). Community frustration is visible but muted.

---

## 6. Trend Signals

### 1. The Multi-Agent Cost Crisis
Every major tool is wrestling with **unpredictable agent-driven costs**. Claude Code's subagent model inheritance (#75055), Gemini's unauthorized subagent activation (#22093), and Qwen's subagent schema conflicts (#7315) all point to the same problem: developers want delegation without financial surprise. The tools that solve **transparent billing + cost caps per agent** will win trust.

**Signal:** Expect a wave of "agent budget" features — per-agent token limits, cost dashboards, and alerting — within 3-6 months.

### 2. Data-Loss Erosion of Trust
Claude Code (#62272, #78273) and Kimi Code (#2523) have bugs where the tool **silently destroys user work**. This is the highest-severity class of bug for AI coding tools — once trust is lost, adoption collapses. The community is unusually vocal about this.

**Signal:** 2026 H2 will see mandatory confirmation dialogs for write operations, cryptographically verified session logs, and Time Machine/Git-based recovery as table stakes.

### 3. The "Bring Your Own Model" Arms Race
Codewhale (#4644), Qwen (#7316), and Pi (#6881) are all investing in provider-neutral architectures. Users want to use their own API keys, switch models mid-session, and avoid vendor lock-in. This is a direct response to the pricing volatility seen in OpenAI Codex's 10-20x cost jump.

**Signal:** The market is consolidating around a "universal AI CLI" interface, with model-as-pluggable-resource becoming the standard. Tools that resist this will be commoditized.

### 4. Windows as the Battleground
Every tool shows Windows-specific regressions this cycle — Claude Code's terminal text selection, Codex's UI freezes, Kimi's missing migration tooling, Copilot's clipboard failures, Codewhale's process leaks. The developer desktop is shifting from macOS-only to cross-platform, and the tools are not keeping pace.

**Signal:** A dedicated Windows QA pass will differentiate tools in 2026-2027. The first tool to deliver a truly stable Windows experience will capture a growing market segment.

### 5. CI/CD Integration as Moonshot
Qwen Code's autofix loop (automated PR generation, gate retry, review-thread resolution) represents the **most ambitious CI/CD integration** of any tool. While still experimental, this points to a future where AI CLI tools are not just coding assistants but autonomous pull-request authors.

**Signal:** Look for Copilot CLI and Gemini CLI to respond with server-side agent capabilities within 6 months. The "agent writes your PR" workflow is the next frontier.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on the provided data.

---

## Claude Code Skills Community Highlights Report (Data as of 2026-07-21)

### 1. Top Skills Ranking

The most-discussed pull requests reveal a community heavily focused on fixing a critical, systemic bug in the `skill-creator` tooling, alongside a strong interest in document-generation and typographic quality.

1.  **#1298: `fix(skill-creator): run_eval.py always reports 0% recall`**
    - **Functionality:** Fixes a critical bug in the SKill creation/evaluation pipeline (`run_eval.py`, `run_loop.py`, `improve_description.py`) where the optimization loop was optimizing against noise (reporting 0% recall for every query). The fix installs the eval artifact as a real skill and addresses Windows stream reading, trigger detection, and parallel workers.
    - **Discussion Highlights:** The PR directly addresses root cause #556 (10+ independent reproductions). The discussion focuses on the deep, systemic nature of the bug affecting the entire skill optimization workflow.
    - **Status:** Open. URL: [PR #1298](https://github.com/anthropics/skills/pull/1298)

2.  **#514: `Add document-typography skill`**
    - **Functionality:** A skill for typographic quality control on AI-generated documents. It prevents orphan word wrap, widow paragraphs, and numbering misalignment—common but often overlooked issues in generated content.
    - **Discussion Highlights:** The high engagement suggests strong community demand for "polish" skills that improve the final output quality of Claude-generated documents, moving beyond basic generation.
    - **Status:** Open. URL: [PR #514](https://github.com/anthropics/skills/pull/514)

3.  **#538: `fix(pdf): correct case-sensitive file references in SKILL.md`**
    - **Functionality:** A straightforward but critical fix for the `pdf` skill, correcting 8 case-sensitivity mismatches in file references (e.g., `REFERENCE.md` → `reference.md`). This breaks builds on case-sensitive file systems (e.g., Linux).
    - **Discussion Highlights:** The extended discussion period (Mar 6 - Apr 29) indicates careful review of component file structure and cross-platform compatibility concerns.
    - **Status:** Open. URL: [PR #538](https://github.com/anthropics/skills/pull/538)

4.  **#486: `Add ODT skill`**
    - **Functionality:** Adds a comprehensive skill for creating, filling, reading, and converting OpenDocument Format files (.odt, .ods), covering triggers for any OpenDocument, LibreOffice, or open-source document request.
    - **Discussion Highlights:** The extended timeline (Mar 1 - Apr 14) suggests thorough review of the skill's trigger conditions and scope, which are quite broad. It represents a call for better open-standard interoperability.
    - **Status:** Open. URL: [PR #486](https://github.com/anthropics/skills/pull/486)

5.  **#210: `Improve frontend-design skill clarity and actionability`**
    - **Functionality:** A major revision of the `frontend-design` skill to improve clarity, actionability, and internal coherence. The goal is to make every instruction something Claude can execute within a single conversation.
    - **Discussion Highlights:** The discussion revolves around defining an effective "scope" for a skill—ensuring it is specific enough to steer behavior without being overly verbose or generic.
    - **Status:** Open. URL: [PR #210](https://github.com/anthropics/skills/pull/210)

6.  **#83: `Add skill-quality-analyzer and skill-security-analyzer to marketplace`**
    - **Functionality:** Proposes two "meta-skills": one for comprehensive quality analysis of other skills (Structure & Documentation, Completeness, etc.) and one for security analysis (injection, secret exposure, sandboxing).
    - **Discussion Highlights:** Represents a clear desire from the community for validation, quality assurance, and security auditing tooling for the Skills ecosystem itself.
    - **Status:** Open. URL: [PR #83](https://github.com/anthropics/skills/pull/83)

7.  **#1367: `feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate`**
    - **Functionality:** A universal skill that audits AI output before delivery. It performs mechanical file verification first, then a four-dimension reasoning audit (in damage-severity priority order) applicable to any project or tech stack.
    - **Discussion Highlights:** The focus is on a "last mile" quality gate for AI output, addressing the community's need for reliability and self-correction mechanisms before delivery.
    - **Status:** Open. URL: [PR #1367](https://github.com/anthropics/skills/pull/1367)

### 2. Community Demand Trends

Analysis of the most active Issues reveals three core demands:

- **Quality & Reliability Assurance:** The dominant demand is for tooling and skills that ensure output quality. This is seen in bug reports for the `skill-creator` (#556: `run_eval.py` 0% trigger rate; #1169: `recall=0%`; #1061: Windows compatibility) and proposals for audit/validation skills (#1385: Reasoning Quality Gate Pipeline). The community is actively struggling with and seeking to fix the skill optimization and evaluation pipeline.
- **Governance, Security, and Identity:** There is growing concern about the trust and security boundaries of the Skills ecosystem. Issue #492 (Security: Community skills under `anthropic/` namespace) is the single most commented-on item, highlighting a major trust boundary vulnerability. Issue #228 (Org-wide skill sharing) and #1175 (Security concerns with SharePoint Online) show demand for enterprise-grade sharing and security controls.
- **Tooling & Ecosystem Stability:** Beyond specific skills, there is a high demand for fixing and improving the core skill-creation and management tooling. This includes the `skill-creator` pipeline issues, Windows compatibility blockers (#1061), and requests to expose skills as MCPs (#16).

### 3. High-Potential Pending Skills

These PRs have active discussion and address critical pain points or highly desired features, suggesting they are likely to be merged soon.

- **Document Polish & Interoperability:** (#514) `document-typography` and (#486) `odt` skill are heavily discussed and address a clear need for higher-quality document output and better open-standard support.
- **Meta-Skills for Quality & Safety:** (#83) `skill-quality-analyzer` and `skill-security-analyzer`, along with (#1367) `self-audit`, are well-received proposals that address the community's most significant concern: the reliability and security of AI output and the skills themselves.
- **Skill-Creator Patch Cascade:** Multiple PRs (#1298, #1099, #1050, #1323, #362, #361) are in-flight to fix the critical "0% recall" bug and the related Windows compatibility issues. The resolution of these patches is the highest priority for the ecosystem's usability.

### 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, auditable, and secure Skills infrastructure—specifically, fixing the broken skill-evaluation pipeline and establishing trust boundaries—before they can confidently adopt and distribute specialized content-generation skills.**

---

# Claude Code Community Digest — 2026-07-21

## Today's Highlights
The latest patch (v2.1.216) fixes a quadratic slowdown in long sessions and adds granular filesystem sandbox controls. The community remains most vocal about **multi-account profile management** (#18435, 148 comments, 667 👍) and **session resumption reliability**, with a new data-loss bug (#62272) revealing that chat history is silently deleted despite configured retention settings. A concerning flurry of issues around **model overrides, billing confusion, and unexpected agent costs** suggests growing friction between the new Fable 5 model tier and existing plan structures.

---

## Releases

### v2.1.216
- **New setting:** `sandbox.filesystem.disabled` — allows skipping filesystem isolation while retaining network egress control, useful for trust-but-verify sandbox configurations.
- **Performance fix:** Resolved a quadratic slowdown in message normalization cost that caused multi-second stalls and slow resumes in long sessions.
- **Other fixes:** Truncated release notes mention a fix in progress (cut off), indicating additional changes likely shipped.

---

## Hot Issues (Top 10 by Community Impact)

1. **#18435 — Multi-account profile switching in Claude Desktop** [OPEN]  
   *Tags: enhancement, auth, IDE*  
   The top-voted feature request (667 👍, 148 comments) asks for seamless account switching within the desktop app. This reflects growing enterprise adoption where engineers juggle personal, work, and client billing accounts.  
   [GitHub →](https://github.com/anthropics/claude-code/issues/18435)

2. **#62272 — Chat history silently deleted despite `cleanupPeriodDays` setting** [OPEN]  
   *Tags: bug, macOS, data-loss*  
   User reports that chat JSONLs are deleted from `~/.claude/projects/` on updates/restarts, ignoring configured retention. A recovery script (via macOS Time Machine) is offered as a band-aid. **Critical concern** — trust in local persistence is shaken.  
   [GitHub →](https://github.com/anthropics/claude-code/issues/62272)

3. **#79341 — Fable 5 incorrectly requires usage credits on Max 20x plan** [OPEN]  
   *Tags: duplicate, cost, model*  
   Mid-session, Claude Code auto-switches off Fable 5 claiming "requires usage credits" even when the user has unused weekly allowance. This points to a plan-model mapping bug that could surprise power users financially.  
   [GitHub →](https://github.com/anthropics/claude-code/issues/79341)

4. **#65036 — MCP OAuth tokens never auto-refresh** [OPEN]  
   *Tags: bug, auth, MCP*  
   MCP connections expire daily despite valid refresh tokens. For teams relying on MCP for tool orchestration, this breaks automated workflows — and the fix appears non-trivial (likely missing token refresh logic in the OAuth client).  
   [GitHub →](https://github.com/anthropics/claude-code/issues/65036)

5. **#23626 — Diff comparison against non-main branches** [OPEN]  
   *Tags: enhancement, IDE*  
   A long-running request (95 👍, 33 comments) asking for Claude to support diff comparisons against any branch, not just `main`. Feature branches, release branches, and preview environments are common in CI/CD workflows.  
   [GitHub →](https://github.com/anthropics/claude-code/issues/23626)

6. **#61021 — Text selection broken in VS Code terminal** [OPEN]  
   *Tags: bug, Windows, TUI, VS Code*  
   A regression prevents simple text copying via mouse + Ctrl+C in the VS Code terminal when Claude Code is active. For developers who live in their editors, this is a significant workflow disruption.  
   [GitHub →](https://github.com/anthropics/claude-code/issues/61021)

7. **#75055 — Sub-agents inherit session model without override capability** [OPEN]  
   *Tags: enhancement, cost, agents*  
   Workflow `agent()` spawns cannot pin a cheaper model, so one user's deep-research run launched 84 agents on Fable 5 — an expensive surprise. Lack of `CLAUDE_CODE_SUBAGENT_MODEL` hook bypasses user-controlled cost management.  
   [GitHub →](https://github.com/anthropics/claude-code/issues/75055)

8. **#49790 — SSH remote sessions should survive client disconnect** [OPEN]  
   *Tags: enhancement, desktop*  
   When Claude Desktop's SSH remote client disconnects (network drop, lid close), the remote process dies. Reconnect/resume semantics (à la tmux/screen) are critically missing for remote development workflows.  
   [GitHub →](https://github.com/anthropics/claude-code/issues/49790)

9. **#72504 — Cowork tab missing on macOS M4 (regression)** [OPEN]  
   *Tags: bug, macOS, cowork, regression*  
   The Cowork sidebar tab fails to initialize entirely on Apple Silicon (M4). Runtime initialization seems broken in v1.15962.1, blocking all collaborative features for affected users.  
   [GitHub →](https://github.com/anthropics/claude-code/issues/72504)

10. **#78273 — Claude overwrote existing user file without confirmation** [OPEN]  
    *Tags: bug, tools, permissions, data-loss*  
    A deeply concerning report: Claude Code read 5 lines of user content, confirmed it, then silently overwrote the entire file containing custom mathematical notation. No tool-permission prompt, no diff preview. This is a **trust-breaking** incident for write operations.  
    [GitHub →](https://github.com/anthropics/claude-code/issues/78273)

---

## Key PR Progress

1. **#66650 — Fix author name in `pr-review-toolkit` plugin manifest** [CLOSED]  
   Corrects `"Daisy"` → `"Daisy Hollman"` for consistency across bundled plugins. Small but shows Anthropic's attention to internal consistency.  
   [GitHub →](https://github.com/anthropics/claude-code/pull/66650)

2. **#74722 — Conventional Branch naming for `/commit-push-pr`** [OPEN]  
   Adds an optional `conventional` flag to auto-generate branch names per Conventional Branch 1.0.0 (`feature/`, `bugfix/`, `hotfix/`, etc.). Useful for teams enforcing branch naming conventions.  
   [GitHub →](https://github.com/anthropics/claude-code/pull/74722)

3. **#79387 — Error message when `edit-issue-labels.sh` called without args** [OPEN]  
   Silently exits with code 1 when no `--add-label`/`--remove-label` args provided. Adds a clear `stderr` message. Fixes #69913.  
   [GitHub →](https://github.com/anthropics/claude-code/pull/79387)

4. **#79385 — Honor any user's thumbs-down, not just issue author's** [OPEN]  
   The auto-close-duplicates bot's UX promised "anyone's 👎" would prevent closure, but the code only checked the issue author. This fix aligns code with the documented contract.  
   [GitHub →](https://github.com/anthropics/claude-code/pull/79385)

5. **#78532 — GCP gateway: optional internal ALB + PG16 Cloud SQL fix** [OPEN]  
   Fixes Terraform deployments failing on PG16 (defaulting to `ENTERPRISE_PLUS` tier rejecting shared-core). Adds optional internal ALB support for private deployments.  
   [GitHub →](https://github.com/anthropics/claude-code/pull/78532)

6. **#1 — Create SECURITY.md** [CLOSED]  
   The very first repository PR (from Feb 2025) is still being referenced, likely as a template or foundational commit.  
   [GitHub →](https://github.com/anthropics/claude-code/pull/1)

---

## Feature Request Trends

1. **Multi-account / multi-profile management** (#18435) — The #1 request by far (667 👍). Users need easy switching between personal, work, and client billing accounts in the desktop app. This is the single most-demanded missing feature.

2. **Model/cost control for sub-agents** (#75055, #79341) — Users want to pin cheaper models for workflow sub-agents, and they want transparent billing (no surprise Fable 5 switches). The Max 20x plan billing bug (#79341) amplifies this anxiety.

3. **Resilient remote sessions** (#49790) — SSH remote sessions that survive client disconnects (reconnect/resume). This is a foundational feature for headless/remote development.

4. **Diff comparisons against any branch** (#23626) — Beyond just `main`. Common in CI/CD, release branches, and preview environments.

5. **API credit balance exposure** (#47574, closed but still in conversation) — Programmatic access to remaining organizational credits via `statusLine` scripts. Multiple related issues suggest this is still unresolved.

6. **TTS readback and voice mode** (#42700) — Accessibility-driven request for voice output in Remote Control sessions. Gaining traction for hands-free workflows.

---

## Developer Pain Points

1. **Data loss / unexpected file overwrites**  
   #62272 (chat deletion despite retention settings) and #78273 (file overwrite without confirmation) represent the **highest-severity trust issues**. Developers cannot tolerate tools that silently destroy work.

2. **MCP OAuth refresh failures** (#65036) — Connections expire daily with no auto-refresh. Breaks automation; requires manual re-authentication. High friction for teams building MCP-first workflows.

3. **Fable 5 billing confusion** (#79341, #75055) — The new model tier creates unexpected costs. Users report being force-switched to usage-based billing despite having unused plan allowances. Sub-agents inheriting expensive models compound the problem.

4. **Terminal/UI regressions**  
   - VS Code text selection broken (#61021, 27 days open)  
   - Cowork tab missing on M4 Macs (#72504, 21 days open)  
   - TUI fullscreen clipping without tmux (#74322, 16 days open)  
   These suggest a regression-prone development cycle.

5. **Windows-specific pain points**  
   - Installer fails on Windows Home (#62116, closed but indicative)  
   - Uncached path keys create duplicate project entries (#69066)  
   - Windows Home users lack Cowork features entirely  
   Platform parity remains a gap.

6. **Session resumption UX** (#60848) — The "Don't ask me again" option in the resume prompt is ambiguous: does it silence the prompt forever, or just for this session? Users want deterministic, documented behavior.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-21

## Today's Highlights

The Codex community continues to wrestle with **rate-limit cost inflation** that has ballooned per-prompt consumption by 10–20x since mid-June, draining Plus plan budgets in as few as 2–3 prompts. A surge of **Windows and macOS performance bugs** — including UI freezes, hung sandbox processes, and system-wide stuttering — dominates recent issue activity. Meanwhile, the engineering team merged a substantial batch of PRs improving **sandboxing, proxy resolution, permission profiles, and compaction performance**, signaling focused infrastructure hardening.

## Releases

- **rust-v0.145.0-alpha.25** — 0.145.0-alpha.25 release (no changelog details provided)

*GitHub: [rust-v0.145.0-alpha.25](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.25)*

## Hot Issues (10 Selected)

1. **[#28879 — Rate-limit cost jumped ~10-20x since June 16](https://github.com/openai/codex/issues/28879)** (208 comments, 358 👍)  
   **Why it matters:** The highest-engagement open issue by a wide margin. Users report Plus plan budgets exhausted after 2-3 prompts on `gpt-5.5`, where previously 20+ were possible. Token-level rate-limit logs show 10-20× consumption increase. This is a **critical billing/usage concern** affecting the core value proposition.

2. **[#11023 — Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)** (181 comments, 800 👍)  
   **Why it matters:** Most upvoted issue overall. Linux developers are effectively locked out of the desktop app due to macOS performance issues (#10432). Demand for native Linux support is intense and sustained.

3. **[#20214 — Codex App freezes/stutters on Windows 11](https://github.com/openai/codex/issues/20214)** (60 comments, 68 👍)  
   **Why it matters:** A flagship platform experience issue. Users with ample system resources (Ryzen 5, 32GB RAM) report persistent UI freezes. Multiple related Windows performance bugs (#33711, #34025, #34305) suggest an underlying architectural problem.

4. **[#13733 — Background polling wastes tokens on full API turns](https://github.com/openai/codex/issues/13733)** (31 comments, 29 👍)  
   **Why it matters:** During builds/tests, each status poll triggers a full API round-trip with entire conversation history. This is a **direct contributor to the rate-limit cost problem** (#28879) — token burn scales with history size × poll count.

5. **[#31836 — Projects "Sort By Last updated" doesn't sort projects](https://github.com/openai/codex/issues/31836)** (23 comments, 26 👍)  
   **Why it matters:** A basic UX regression — the sort control is non-functional for projects, sorting only tasks within groups. Points to broader project management UX immaturity.

6. **[#24287 — Desktop UI stuck in Thinking; Stop fails](https://github.com/openai/codex/issues/24287)** (16 comments, 5 👍)  
   **Why it matters:** Session-termination failure. Users lose ability to stop or restart, and turns become invisible after app restart. Core reliability bug for Pro subscribers.

7. **[#26633 — Desktop automations ignore timezone in RRULE scheduling](https://github.com/openai/codex/issues/26633)** (15 comments, 3 👍)  
   **Why it matters:** Automations are a key differentiation feature. Timezone bugs in scheduling make them unreliable for cross-timezone development workflows.

8. **[#31969 — Unsupported parameter 'reasoning.summary' with gpt-5.3-codex-spark](https://github.com/openai/codex/issues/31969)** (14 comments, 8 👍)  
   **Why it matters:** Model configuration mismatch that breaks the "spark" model variant. Indicates insufficient parameter validation or documentation gaps between model capabilities.

9. **[#23200 — Support headless remote Linux hosts for Codex mobile](https://github.com/openai/codex/issues/23200)** (12 comments, 41 👍)  
   **Why it matters:** Mobile Codex is hamstrung by requiring a desktop machine to stay online. Always-on Linux servers are the standard dev infrastructure; this limits mobile's utility as a "control layer."

10. **[#16127 — 'yeet' skill is over-opinionated](https://github.com/openai/codex/issues/16127)** (11 comments, 26 👍)  
    **Why it matters:** The `yeet` skill auto-modifies branch names and PR titles without opt-in, and runs `git` commands on repos managed by `jj`. Highlights tension between automation convenience and user control.

## Key PR Progress (10 Selected)

1. **[#34438 — Increase patch approval test timeout](https://github.com/openai/codex/pull/34438)** (merged today)  
   Extends patch approval test timeout to 15s to accommodate slower approval events. Minor but addresses flaky test infrastructure.

2. **[#34436 — Honor managed permission profiles in network proxy resolution](https://github.com/openai/codex/pull/34436)** (merged today)  
   Fixes a gap where `requirements.toml` permission profiles were selected but their network configuration was ignored during proxy resolution. Critical for enterprise network policy compliance.

3. **[#34435 — Resolve outbound proxy routes explicitly](https://github.com/openai/codex/pull/34435)** (merged today)  
   Eliminates blocking system proxy discovery and inconsistent fallback behavior. Directly addresses network reliability for sandboxed execution.

4. **[#34398 — Support per-environment permission profiles](https://github.com/openai/codex/pull/34398)** (merged yesterday)  
   Allows each selected environment to override the thread's `PermissionProfile`. Impacts shell, exec, filesystem, approval, and network decisions. A significant step toward granular security controls.

5. **[#34431 — Optimize remote compaction history handling](https://github.com/openai/codex/pull/34431)** (merged yesterday)  
   Reduces CPU/memory overhead during remote compaction by estimating token counts once and avoiding redundant history replacement. Targets the performance degradation in large-session workflows.

6. **[#34423 — Support Windows sandboxing in exec server](https://github.com/openai/codex/pull/34423)** (merged yesterday)  
   Adds Windows sandbox session backend for the exec server. Directly addresses a major platform gap — previously only Linux sandboxing was supported server-side.

7. **[#34417 — Enrich app/read connector metadata](https://github.com/openai/codex/pull/34417)** (merged yesterday)  
   Adds dark icon, distribution channel, install URL, and plugin display names to connector metadata. Improves MCP connector interoperability and UI rendering.

8. **[#34416 — Show completed hook warnings in TUI headers](https://github.com/openai/codex/pull/34416)** (merged yesterday)  
   Renders hook warnings inline in the TUI hook header. Improves visibility of post-execution warnings that were previously hidden.

9. **[#30235 — Kill timed-out Git status process groups](https://github.com/openai/codex/pull/30235)** (merged today)  
   On Unix, places `git status` in its own process group and kills the entire group on timeout. Fixes runaway wrapper processes scanning the worktree after five-second timeout.

10. **[#34413 — Remove CSV-backed agent jobs](https://github.com/openai/codex/pull/34413)** (merged yesterday)  
    Removes legacy CSV-based agent job tools and database tables. Housecleaning that indicates a pivot toward more structured agent orchestration.

## Feature Request Trends

The following directions emerge from cross-cutting analysis of open enhancement issues:

- **Linux desktop app** (#11023, 800 👍) — Far and away the most demanded feature. The macOS app's performance issues (#10432) have pushed Linux users to the front of the line.
- **Headless remote execution for mobile** (#23200) — Users want Codex mobile to work with always-on Linux servers without requiring a personal desktop to stay online.
- **Project/chat organization UX** — Multiple requests for project names in pinned chats (#26070, #29681), proper sort functionality (#31836), and auto-expanding working sections (#22334).
- **Timezone-aware scheduling** — For automations and reset cards (#26633, #32726), users want explicit timezone handling in recurring rules.
- **Background process token efficiency** — Not strictly a feature request, but #13733's polling-loop token waste is a systemic inefficiency that should be treated as a design requirement.

## Developer Pain Points

- **Rate-limit cost explosion (#28879, #13733)** — The dominant pain point. Per-token consumption increased 10-20x in June, and background polling compounds the problem. This is eroding trust in the Plus pricing model.
- **Windows performance degradation** — At least six distinct Windows issues (#20214, #33711, #26401, #34025, #33737, #34305) describe UI freezes, system-wide lag, Defender CPU spikes, and sandbox hangs. The density suggests a systemic Windows client issue.
- **Session reliability** — Multiple reports of stuck "Thinking" states, invisible turns, and disappearing history (#24287, #29069, #21244) undermine confidence in the session persistence layer.
- **Sandbox/resource overhead on Windows** — Elevated sandbox scanning (`codex-windows-sandbox-setup.exe`) causes 100% disk usage and 30-130s tool latency (#33737). Zombie helper processes accumulate per command (#32194), busy-spinning CPU cores.
- **MacOS sidebar/UI freezes** — New in this digest (#34376): sidebar interactions trigger 3-10s freezes due to recursive FSEvents watcher teardown. A recurring theme of filesystem watcher issues across platforms.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-21

## Today's Highlights
Agent reliability takes center stage this week as the community grapples with subagent misreporting, indefinite hangs, and shell execution freezes. A major security patch for the A2A server enforces workspace trust to prevent RCE, while the team is laying groundwork for automated PR generation pipelines and a caretaker triage workflow. The nightly build v0.52.0 continues rolling.

## Releases
- **v0.52.0-nightly.20260720.gacae7124b** — No breaking changes or feature announcements in the release notes. [Full changelog](https://github.com/google-gemini/gemini-cli/compare/v0.52.0-nightly.20260719.gacae7124b...v0.52.0-nightly.20260720.gacae7124b)

## Hot Issues

1. **[#22323 – Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 12 comments) — `codebase_investigator` subagent reports `status: "success"` even after hitting max turn limits without doing any analysis. This masks real failure and has attracted strong community attention (👍2). A bug that silently corrupts agent decision logs.

2. **[#19873 – Zero-Dependency OS Sandboxing & Post-Execution Intent Routing](https://github.com/google-gemini/gemini-cli/issues/19873)** (P2, 8 comments) — Long-running enhancement request to leverage Gemini 3's native bash affinity with secure sandboxing. Community sees this as foundational for safe autonomous agent operation.

3. **[#24353 – Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (P1 EPIC, 7 comments) — Tracks expansion of behavioral eval tests beyond the initial 76. Critical for ensuring agent quality as subagent count grows.

4. **[#21409 – Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 7 comments, 👍8) — The most upvoted bug this cycle. CLI hangs forever when deferring to the generalist agent for simple tasks like folder creation. Users report workarounds (disabling subagents) but this is a major reliability blocker.

5. **[#22745 – AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (P2 EPIC, 7 comments) — Investigates whether AST-aware tools can reduce turns, improve token efficiency, and enable precise codebase navigation. Directly ties to reducing agent latency.

6. **[#21968 – Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, 6 comments) — Users report custom skills and sub-agents are rarely invoked autonomously even when contextually relevant. Suggests poor intent routing or prompt engineering gaps.

7. **[#25166 – Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 4 comments, 👍3) — Simple CLI commands hang after completion while CLI still shows "Awaiting user input." High impact as it blocks all subsequent automation.

8. **[#26522 – Auto Memory retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, 5 comments) — Auto Memory agent re-surfaces low-signal sessions because it never marks them as processed. Leads to infinite loops and wasted token spend.

9. **[#22672 – Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, 3 comments) — Model occasionally uses `git reset --force` or other destructive commands when safer alternatives exist. Community asks for built-in safeguards.

10. **[#22093 – Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** (P2, 3 comments) — Agents mode set to "disabled" is ignored; subagents activate anyway. Breaks user expectations and can lead to unexpected behavior in CI environments.

## Key PR Progress

1. **[#28470 – Fix A2A server: workspace trust and task isolation to prevent RCE](https://github.com/google-gemini/gemini-cli/pull/28470)** (XL, security-critical) — Refactors environment loading and task isolation in the A2A server to prevent zero-click RCE. A top priority for maintainers.

2. **[#28469 – Rotate session ID on model fallback](https://github.com/google-gemini/gemini-cli/pull/28469)** (M) — Fixes stateful API errors when falling back to `gemini-2.5-flash`. Prevents "submit a new query" blocking errors.

3. **[#28410 – Shorten MCP tools/list discovery timeout](https://github.com/google-gemini/gemini-cli/pull/28410)** (P1, M) — MCP discovery could freeze the CLI for 10 minutes on unresponsive servers. Now fails fast with a short timeout.

4. **[#28405 – Prevent scroll position jump on content updates](https://github.com/google-gemini/gemini-cli/pull/28405)** (P1, XS) — Fixes #5009 where scrolling up to review changes causes jump to bottom when new content arrives. A long-standing UX annoyance.

5. **[#28411 – Caretaker: post comment before auto-closing feature requests](https://github.com/google-gemini/gemini-cli/pull/28411)** (S) — Improves issue triage UX by explaining auto-closure with a comment before labeling. Shows focus on community communication.

6. **[#28435 – PR Generator Core: environment parser, command executor, GitHub REST client](https://github.com/google-gemini/gemini-cli/pull/28435)** (L) — Foundational utilities for automated PR generation pipeline. Part of a larger SSR (Self-Service Repair) initiative.

7. **[#28433 – PR Generator Orchestrator: bug-fixing state machine & container entrypoint](https://github.com/google-gemini/gemini-cli/pull/28433)** (XL) — Implements iterative AI coding loops with ESLint analysis and diff limits. Automates bug fixing at scale.

8. **[#28319 – Refactor A2A: enforce path trust check before environment loading](https://github.com/google-gemini/gemini-cli/pull/28319)** (XL) — Prevents environment poisoning attacks by ensuring trust checks happen before workspace env vars are loaded.

9. **[#28447 – Windows PowerShell troubleshooting for `gemini` command](https://github.com/google-gemini/gemini-cli/pull/28447)** (S) — Adds Windows-specific installation guidance. Addresses a common onboarding failure point.

10. **[#28256 – Add /nix/store to trusted system paths](https://github.com/google-gemini/gemini-cli/pull/28256)** (S, closed) — Enables Nix users to use `rg` and other tools from the Nix store. A small but impactful fix for the Nix community.

## Feature Request Trends
- **AST-aware tooling** (#22745, #22746): Multiple EPICs explore AST integration for file reads, search, and codebase mapping to reduce turn count and token waste.
- **Agent self-awareness** (#21432): Requests for agents to understand their own CLI flags, hotkeys, and capabilities to act as self-guides.
- **Subagent trajectory visibility** (#22598): Community wants to inspect and share subagent decision logs via `/chat share` for debugging and eval.
- **Browser agent resilience** (#22232): Automatic session takeover, lock recovery, and Wayland compatibility are recurring asks.
- **Component-level evaluations** (#24353): Growing demand for structured, repeatable eval suites as agent count increases.

## Developer Pain Points
- **Hangs and freezes**: #21409 (generalist hangs), #25166 (shell command stuck), #22465 (Vite creation stuck at interactive prompt) — reliability continues to be the top frustration.
- **Subagent governance**: #22323 (false success reports), #22093 (unauthorized agent activation), #20079 (symlink agents not recognized) — the agent orchestration layer has trust and consistency issues.
- **Tool overloading**: #24246 (>128 tools causes 400 errors) — tool-scaling issues emerge as users add more MCP and custom agents.
- **Memory system bugs**: #26522 (infinite retries), #26525 (logging secrets before redaction), #26523 (silent patch skips) — the Auto Memory feature shows systemic quality gaps.
- **Terminal UX regressions**: #24935 (corruption after external editors), #21924 (flicker on resize) — terminal emulation quality impacts professional workflow.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-07-21

---

## Today's Highlights

Two rapid-fire releases (v1.0.72 and v1.0.73) dropped yesterday, bringing critical fixes for agent hook looping and new Anthropic subagent support for multi-directory setups. Meanwhile, the community is reporting a surge of regressions—particularly around clipboard functionality on Windows, shell command blocking in plan-mode, and a nasty poison-pill timeout triggered by the text "WAITFOR DELAY." The issue tracker saw 21 items updated in the last 24 hours, with several high-impact bugs receiving the `triage` label.

---

## Releases

Two versions published on 2026-07-20:

- **v1.0.73** — Anthropic subagents now continue working when additional directories are configured. Relative links in custom agent instructions are resolved from the agent file location.
- **v1.0.72** — Fixed an `agentStop` hook that previously looped indefinitely; the CLI now ends the turn after 8 consecutive blocks, and `agentStop` hooks receive a `stop_hook_active` flag for self-limiting. Added opt-in git and gh authentication inside the O.

---

## Hot Issues (10 Notable)

1. **[#3622 — Copy to clipboard silently fails on Windows](https://github.com/github/copilot-cli/issues/3622)** (OPEN, 4 comments, 👍4)  
   Regression since v1.0.48: copy appears to succeed but clipboard is never updated. Windows users are stuck without a workaround, making terminal-based workflows broken.

2. **[#3747 — Unrecoverable timeouts when "WAITFOR DELAY" appears](https://github.com/github/copilot-cli/issues/3747)** (OPEN, 1 comment, 👍1)  
   Any prompt or file containing "WAITFOR DELAY" (MSSQL syntax) causes a permanent fault state across all models. A clear poison-pill bug that blocks SQL-focused developers.

3. **[#4188 — Regression on plan-mode: shell commands blocked](https://github.com/github/copilot-cli/issues/4188)** (OPEN, 1 comment, 👍1)  
   Plan-mode in the latest version now blocks shell commands (e.g., `gh` CLI) that were previously used to enrich plans. This breaks issue creation/reading during planning.

4. **[#4185 — `--add-dir` causes Claude sub-agent dispatch failure](https://github.com/github/copilot-cli/issues/4185)** (OPEN, 0 comments)  
   Launching with `--add-dir` flags causes a 400 error on Anthropic models: "A maximum of 4 blocks with cache_control... Found 5." Blocks multi-repo workflows on Claude.

5. **[#4183 — Auto-compaction does not prevent CAPI 5 MB failure](https://github.com/github/copilot-cli/issues/4183)** (OPEN, 0 comments, 👍2)  
   Long, tool-heavy sessions stay under token limits but hit the independent 5 MB serialized request body limit. Auto-compaction doesn't address this, causing hard failures.

6. **[#4195 — Code-review task agents can mutate shared parent worktree](https://github.com/github/copilot-cli/issues/4195)** (OPEN, 0 comments)  
   Despite being described as read-only, `code-review` agents with `agent_type: code-review` can modify the shared worktree. A security/reliability concern for review panels.

7. **[#1688 — Configurable auto-compaction threshold](https://github.com/github/copilot-cli/issues/1688)** (OPEN, 2 comments, 👍5)  
   Users of slower, high-capacity models like Claude Opus 4.6 want a user-configurable threshold in `config.json` to trigger compaction before latency degrades.

8. **[#4194 — "Severe levels of hard-coding"](https://github.com/github/copilot-cli/issues/4194)** (OPEN, 2 comments)  
   Vague but emotionally charged report about hard-coding issues. Low detail, but the title suggests user frustration with inflexible configuration.

9. **[#4180 — Interactive TUI ignores PTY keyboard input](https://github.com/github/copilot-cli/issues/4180)** (OPEN, 0 comments)  
   Automation/orchestration tools (tmux send-keys, expect, pty.fork()) cannot interact with the TUI—only Ctrl+C works. Breaks headless and scripted usage.

10. **[#4189 — `/context` reports un-deferred MCP tool-schema footprint](https://github.com/github/copilot-cli/issues/4189)** (OPEN, 0 comments)  
    The `/context` command shows the full MCP tool schema size rather than actual deferred cost sent to the model, misleading developers about context usage.

---

## Key PR Progress

No pull requests were updated in the last 24 hours. The repository had 0 items in the PR list for this period.

---

## Feature Request Trends

- **Model Selection & Configuration Switching** — Multiple requests ([#4190](https://github.com/github/copilot-cli/issues/4190), [#4192](https://github.com/github/copilot-cli/issues/4192)) for rapid model/effort switching, BYOK model selection in background agents, and pre-set model configs to avoid repetitive `/model` menu navigation.
- **Session Management Improvements** — Users want easy session creation from `/btw` conversations ([#4182](https://github.com/github/copilot-cli/issues/4182)) and the ability to edit enqueued messages via mouse clicks in the TUI ([#4179](https://github.com/github/copilot-cli/issues/4179)).
- **Configurable Context Compaction** — A re-emerging request ([#1688](https://github.com/github/copilot-cli/issues/1688)) for letting users set their own auto-compaction thresholds, especially for high-capacity models where default triggers are too late.

---

## Developer Pain Points

- **Clipboard & Terminal Rendering Regressions** — Windows clipboard silently fails ([#3622](https://github.com/github/copilot-cli/issues/3622)), path copying yields whitespace ([#4184](https://github.com/github/copilot-cli/issues/4184)), and clipboard access breaks under tmux/screen in WSL ([#4191](https://github.com/github/copilot-cli/issues/4191)).
- **Plan-Mode Lockdown** — The latest regression blocks essential developer tools (`gh`, shell commands) during planning ([#4188](https://github.com/github/copilot-cli/issues/4188)), frustrating workflows that depend on enriched plans.
- **Automation & TUI Incompatibility** — The interactive TUI ignores programmatic PTY input ([#4180](https://github.com/github/copilot-cli/issues/4180)), locking out CI/CD and automation tooling.
- **Context Bloat & Hard Limits** — Even with auto-compaction, sessions hit hard 5 MB CAPI body limits ([#4183](https://github.com/github/copilot-cli/issues/4183)), and the `/context` display is misleading for MCP users ([#4189](https://github.com/github/copilot-cli/issues/4189)).
- **Anthropic Cache-Control Limit** — Adding extra directories breaks Claude sub-agent dispatch due to hard 4-block cache_control limit ([#4185](https://github.com/github/copilot-cli/issues/4185)).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date: 2026-07-21**

---

## Today's Highlights
The Kimi Code CLI community is currently grappling with a cluster of regressions spanning session migration, context compaction, and goal-mode resource exhaustion. A notable fix is in review to correct `StrReplaceFile` replacement counting for chained edits, while a long-standing 429 engine overload issue on remote servers remains unresolved for over 70 days. Windows-specific migration and UI bugs are also drawing attention as the `kimi` v1.x migration completes.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

1. **[#2209] Persistent 429 engine_overloaded on remote server (48+ hours)**  
   *Author: yuermodi | Updated: 2026-07-20 | Comments: 4 | 👍: 3*  
   **Why it matters:** User on Linux x86_64 remote server reports continuous `429 engine_overloaded` errors lasting over 48 hours, persisting across upgrades from v1.24.0 to v1.41.0 and model switches (K2.5 to K2.6). This suggests a systemic throttling issue rather than transient load.  
   [GitHub Issue #2209](https://github.com/MoonshotAI/kimi-cli/issues/2209)

2. **[#2526] StrReplaceFile reports too few replacements for chained edits**  
   *Author: Sreekant13 | Updated: 2026-07-21 | Comments: 0 | 👍: 0*  
   **Why it matters:** Sequential string replacements in chained edits are counted against the original file content instead of the running content. This causes undercounting and can lead to edit failures when one edit's `old` string is produced by an earlier edit.  
   [GitHub Issue #2526](https://github.com/MoonshotAI/kimi-cli/issues/2526)

3. **[#2525] Goal mode: no-op continuation fires indefinitely, burning tokens**  
   *Author: zedi2000 | Updated: 2026-07-20 | Comments: 0 | 👍: 0*  
   **Why it matters:** In goal mode, when waiting on external conditions (long training jobs, GPU availability), the agent repeatedly re-injects the full goal context every few seconds. This wastes tokens and quickly exhausts context windows on slow operations.  
   [GitHub Issue #2525](https://github.com/MoonshotAI/kimi-cli/issues/2525)

4. **[#2523] Context compaction bug: reopens already completed and deleted tasks**  
   *Author: Frogzter | Updated: 2026-07-20 | Comments: 0 | 👍: 0*  
   **Why it matters:** User on Windows reports that context compaction in v0.6.3 (K2.7 model) resurrects completed and deleted tasks, causing workflow confusion and potential cascading errors in long-running sessions.  
   [GitHub Issue #2523](https://github.com/MoonshotAI/kimi-cli/issues/2523)

5. **[#2522] Windows: old kimi-code sessions not migrated to .kimi after upgrade**  
   *Author: sunnywang666 | Updated: 2026-07-20 | Comments: 0 | 👍: 0*  
   **Why it matters:** Upgrade from legacy `kimi-code` to new `kimi` v1.49.0 on Windows fails to migrate session data from `%USERPROFILE%\.kimi-code` to `.kimi`. The `kimi migrate` command is missing entirely, leaving users with orphaned data.  
   [GitHub Issue #2522](https://github.com/MoonshotAI/kimi-cli/issues/2522)

6. **[#2521] Windows herdr: arrow keys unusable for selection**  
   *Author: RambleRainbow | Updated: 2026-07-20 | Comments: 0 | 👍: 0*  
   **Why it matters:** In the Windows version of `herdr` (likely a TUI component), arrow keys cannot be used to navigate selection lists. This breaks interactive workflows on Windows, a growing platform for Kimi users.  
   [GitHub Issue #2521](https://github.com/MoonshotAI/kimi-cli/issues/2521)

7. **[#2517] Fork/undo context truncation misalignment**  
   *Related PR: #2520 | Comments: 0*  
   **Why it matters:** Wire turns and context turns become misaligned after fork/undo operations, causing history mismatch errors. This has been a recurring pain point (referenced in #1974, #2049) and a root cause fix is in review.  
   [GitHub Issue #2517](https://github.com/MoonshotAI/kimi-cli/issues/2517)

8. **[#2420] Frozen system prompt on session resume**  
   *Related PR: #2519 | Comments: 0*  
   **Why it matters:** Resuming a session ignores `~/.kimi/skills/` additions and `AGENTS.md` edits because the frozen `_system_prompt` in `context.jsonl` is always adopted. Users must restart sessions to pick up new skills.  
   [GitHub Issue #2420](https://github.com/MoonshotAI/kimi-cli/issues/2420)

9. **[#1974] Wire-only slash turns shift undo cut**  
   *Related PR: #2520 | Comments: 0*  
   **Why it matters:** Slash commands executed without body content can shift the undo cut point, making it impossible to undo previous steps correctly. This subtle bug has been reported across multiple versions.  
   [GitHub Issue #1974](https://github.com/MoonshotAI/kimi-cli/issues/1974)

10. **[#2049] History mismatch after forks/undos**  
    *Related PR: #2520 | Comments: 0*  
    **Why it matters:** Collaborative history tracking breaks after undo/redo operations, making it difficult to audit or replay session state. The upcoming PR #2520 aims to resolve this through wire turn alignment.  
    [GitHub Issue #2049](https://github.com/MoonshotAI/kimi-cli/issues/2049)

---

## Key PR Progress

1. **[#2524] fix(tools): count StrReplaceFile replacements against the running content**  
   *Author: Sreekant13 | Updated: 2026-07-21 | Resolves: #2526*  
   **Description:** Corrects the replacement count to track against the progressively edited content rather than original text, enabling accurate reporting for chained edits.  
   [GitHub PR #2524](https://github.com/MoonshotAI/kimi-cli/pull/2524)

2. **[#2520] fix(session): align fork/undo context truncation to wire turns**  
   *Author: Nas01010101 | Updated: 2026-07-20 | Resolves: #2517, #1974, #2049*  
   **Description:** Maps wire turns to context turns for slash-commands and reorganizes dataflow to prevent misalignment. Includes regression test for #1974.  
   [GitHub PR #2520](https://github.com/MoonshotAI/kimi-cli/pull/2520)

3. **[#2519] fix(app): refresh stale frozen system prompt on session resume**  
   *Author: Nas01010101 | Updated: 2026-07-20 | Resolves: #2420*  
   **Description:** Instead of unconditionally adopting the frozen `_system_prompt` from `context.jsonl`, the PR checks for updates to `~/.kimi/skills/` and `AGENTS.md`, applying them on resume.  
   [GitHub PR #2519](https://github.com/MoonshotAI/kimi-cli/pull/2519)

4. **[#2386] (Status needed)**  
   *Related to PR #2520 for context turn mapping.*  
   **Description:** Earlier attempt at wire-to-context turn mapping for slash commands; PR #2520 notes it resolves the same root cause.  
   [GitHub PR #2386](https://github.com/MoonshotAI/kimi-cli/pull/2386)

---

## Feature Request Trends

- **Session portability across major upgrades:** Users repeatedly request that session data be automatically migrated or that a `kimi migrate` command exist to handle the `kimi-code` → `kimi` transition, especially on Windows.
- **Context awareness for external dependencies:** Several issues (especially #2525) ask for smarter pause/resume logic when the agent is waiting on external operations, to avoid token waste and context explosion.
- **Better Windows TUI/CLI support:** Arrow key selection, migration scripts, and session path handling are all recurring pain points for Windows users, suggesting the need for a dedicated Windows QA pass.
- **System prompt live reload:** Users want the ability to add skills or modify `AGENTS.md` without restarting the entire session (#2420-related feedback).

---

## Developer Pain Points

- **Unrecoverable 429 throttling on remote servers:** The unresolved #2209 highlights a critical reliability issue where users on cloud infrastructure can be locked out for days without a clear escalation path or automatic backoff strategy.
- **Session state corruption after compaction/undo:** Issues like #2523 (task resurrection) and #2520-related history mismatches create trust issues for long-running coding sessions, forcing users to frequently restart.
- **Windows-specific regression with no fallback:** The migration tooling missing entirely (#2522) combined with broken interactive UI (#2521) makes Windows a second-class platform for critical workflows.
- **Chained edit fragility:** The `StrReplaceFile` counting bug (#2526) shows that chained edits—common in refactoring workflows—are brittle and their reported result cannot be trusted without manual verification.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest
**2026-07-21**

## Today's Highlights
OpenCode v1.18.4 shipped with adaptive thinking controls for Kimi models, while the community continues grappling with WSL notification server crashes that have spawned multiple related issues. The TUI's "Plan/Build mode" removal in v1.18.0 is causing confusion, and a rash of "Object has been destroyed" Electron crashes persists across desktop clients.

## Releases
**[v1.18.4](https://github.com/anomalyco/opencode/releases/tag/v1.18.4)** — Core improvements: adaptive thinking controls for Kimi models on Anthropic-compatible providers, with summarized reasoning output by default (@chouqin). Bugfixes: reduced OpenAI provider header timeouts during slow connection setup; proper handling of provider-defined reasoning options.

## Hot Issues
1. **[#27906](https://github.com/anomalyco/opencode/issues/27906) — v1.15.1+ Breaks Bun Installs** (20 comments, 13 👍)  
   Postinstall lifecycle script requirement breaks global package installation on Bun, which blocks such scripts by default. Significant since Bun adoption is growing among JS developers.

2. **[#29363](https://github.com/anomalyco/opencode/issues/29363) — `limit.output` silently capped at 32k** (15 comments, 7 👍)  
   Per-step `maxOutputTokens` capped at 32K despite config values up to 384K. The only workaround is an experimental env var. Affects users of large-context models like DeepSeek and Claude.

3. **[#37171](https://github.com/anomalyco/opencode/issues/37171) — Desktop crashes: "Notification server not found: wsl:Ubuntu"** (9 comments, 4 👍)  
   — **CLOSED** — WSL integration crash on restart. Signal of wider WSL notification server instability.

4. **[#37970](https://github.com/anomalyco/opencode/issues/37970) — Plan/Build mode removed** (9 comments)  
   v1.18.0 removed the Plan/Build mode toggle. Users report unpredictable behavior when asking the model to plan without executing. Workflow regression for cautious developers.

5. **[#23539](https://github.com/anomalyco/opencode/issues/23539) — Plugin API for custom status bar widgets** (6 comments, 4 👍)  
   Consolidated request building on prior feature suggestions (#8619, #18969). Strong community interest in extensible UI.

6. **[#35686](https://github.com/anomalyco/opencode/issues/35686) — Infinite startup crash loop with notification server error** (6 comments, 1 👍)  
   — **CLOSED** — Desktop v1.17.14 enters crash loop when notification server URL contains an IP:port. Related to #37171 and #37331.

7. **[#36826](https://github.com/anomalyco/opencode/issues/36826) — DeepSeek V4 Flash: "Failed to send prompt"** (6 comments, 1 👍)  
   Unexpected server errors when using DeepSeek V4 Flash model. Provider-specific reliability issue.

8. **[#23248](https://github.com/anomalyco/opencode/issues/23248) — Sessions orphaned when project directory renamed** (5 comments, 6 👍)  
   — **OPEN** — Absolute path binding causes session invisibility after directory rename. Affects users who reorganize workspaces.

9. **[#37428](https://github.com/anomalyco/opencode/issues/37428) — Desktop brightness values "chosen by a Ringwraith"** (4 comments, 1 👍)  
   Title text absurdly dark on desktop client compared to TUI. User experience complaint with vivid language.

10. **[#37815](https://github.com/anomalyco/opencode/issues/37815) — Kimi K3 "Upstream request failed" on Console Go** (2 comments, 1 👍)  
    Specific model fails while others on same provider work. Isolated provider compatibility issue.

## Key PR Progress
1. **[#38014](https://github.com/anomalyco/opencode/pull/38014) — Fix npm plugin entry point as file URL on Windows**  
   `import.meta.resolve()` returns raw paths on Windows; this PR converts to `file://` URLs. Critical for cross-platform plugin support.

2. **[#38019](https://github.com/anomalyco/opencode/pull/38019) — Bound shell output after exit**  
   Resolves child process status on direct exit, adds 500ms EOF wait, marks incomplete output. Addresses race conditions in shell integration.

3. **[#37647](https://github.com/anomalyco/opencode/pull/37647) — Build opencode2 (TUI) alongside opencode in Nix**  
   Nix build now provides `opencode2` binary. Infrastructure improvement for Nix users.

4. **[#37219](https://github.com/anomalyco/opencode/pull/37219) — Ignore node_modules during config and skill discovery**  
   Prevents recursive glob scans from traversing `node_modules`. Closes #30337. Performance and correctness fix.

5. **[#37956](https://github.com/anomalyco/opencode/pull/37956) — Add image backgrounds**  
   Background image support in appearance settings for web and desktop, with Cache Storage and managed file persistence.

6. **[#38016](https://github.com/anomalyco/opencode/pull/38016) — Improve patch errors**  
   Typed parser errors for missing boundaries, line numbers for invalid hunk headers, preserves filesystem failure details. Developer experience improvement.

7. **[#38006](https://github.com/anomalyco/opencode/pull/38006) — Support JSON callbacks in CodeMode**  
   Plumbing for `JSON.parse` revivers and `JSON.stringify` replacers/arrays. Test262 coverage added.

8. **[#35688](https://github.com/anomalyco/opencode/pull/35688) — Guard missing notification server state**  
   Prevents renderer crash when notification state is requested for unknown server key. Closes #35686 crash-loop bug.

9. **[#38005](https://github.com/anomalyco/opencode/pull/38005) — Support BigInt arithmetic in CodeMode**  
   Decimal/binary/octal/hex BigInt literals with 4096-bit cap. CodeMode feature parity expansion.

10. **[#33127](https://github.com/anomalyco/opencode/pull/33127) — TUI sidebar history and scroll-to-message**  
    Adds History sidebar panel listing user messages with click-to-scroll. Closes #32165. TUI navigability improvement.

## Feature Request Trends
- **Session portability** (#23248, #29703, #36509): Multiple requests for path-independent session storage and cross-device sync. Users want to rename/move projects without losing history.
- **UI customization** (#23539, #37428, #37956): Status bar plugin API, brightness/theme fixes, background images. Growing demand for visual personalization.
- **Opt-out controls** (#37958, #38010): Close confirmation dialogs and exit splash removal. Users want to prevent accidental closure and support embedded/white-label use cases.
- **Proxy/network support** (#37993): Built-in proxy with auto-start/stop for restricted environments. Important for enterprise deployments.

## Developer Pain Points
- **WSL notification server crashes** (#37171, #35686, #36977, #37331, #38012): At least 5 issues in the last 2 weeks involve "Notification server not found" errors, especially under WSL. High recurrence suggests deep integration issue.
- **Desktop Electron crashes** (#30627, #30297, #35501, #32923, #32389): Four "Object has been destroyed" reports and one `AttachConsole` failure. Persistent instability in Electron desktop client.
- **Provider-specific failures** (#36826, #37815, #37056): DeepSeek V4 Flash, Kimi K3, and Console Go subscribers report "Upstream request failed" errors. Provider compatibility remains fragile.
- **Silent config caps** (#29363): `limit.output` silently truncated at 32K tokens with only an experimental env var workaround. Frustrating for users of high-capacity models.
- **Workflow mode confusion** (#37970): Removal of Plan/Build toggle without clear replacement leaves users uncertain how to constrain model behavior.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-21

## Today’s Highlights
A significant regression in `httpIdleTimeoutMs` affecting self-hosted OpenAI-compatible providers (v0.80.6) has attracted the most community attention. The project saw a burst of activity around provider cost accuracy, with merged PRs to honor provider-reported billing from Vercel AI Gateway and fix Copilot GPT-5.6 pricing. Several important fixes landed for auth.json environment variable handling and session compaction reliability.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#6476 — Regression: httpIdleTimeoutMs no longer respected for self-hosted OpenAI-compatible provider](https://github.com/earendil-works/pi/issues/6476)**  
   *Author: hoho51 | Comments: 11 | Status: OPEN, inprogress*  
   The top-voted issue. After upgrading to v0.80.6, self-hosted vLLM instances time out despite explicit `httpIdleTimeoutMs` settings. Downgrading to v0.80.3 restores correct behavior. High priority for users running local models.

2. **[#5263 — Make in-session model changes ephemeral by default](https://github.com/earendil-works/pi/issues/5263)**  
   *Author: vanvlack | Comments: 8 | 👍: 8 | Status: OPEN*  
   A popular feature request to keep model/thinking-level changes session-only unless explicitly saved. Proposes a "Default model" entry in `/settings`. The 8 upvotes signal strong community desire for this workflow improvement.

3. **[#6725 — Copilot pricing for GPT-5.6 models is incorrect](https://github.com/earendil-works/pi/issues/6725)**  
   *Author: krzyk | Comments: 7 | Status: CLOSED*  
   Copilot's GPT-5.6 cost calculations excluded cache write costs, causing reported session costs to be ~$1.67 vs actual $10.72. Closed as fixed—demonstrates active maintenance of provider pricing accuracy.

4. **[#5931 — Copy-paste from TUI introduces extra spaces and line breaks](https://github.com/earendil-works/pi/issues/5931)**  
   *Author: smithyyang | Comments: 6 | Status: CLOSED*  
   Long-standing TUI copy-paste quality issue at line-wrapping points. Important for users who frequently extract code or text from sessions.

5. **[#3200 — Support video/audio content in prompt command](https://github.com/earendil-works/pi/issues/3200)**  
   *Author: louis030195 | Comments: 6 | 👍: 4 | Status: OPEN*  
   Extending multimodal support beyond images for prompts. Key for users of `gemma4` and `gpt-4o` who want video/audio inputs. Growing demand signalled by upvotes.

6. **[#6652 — pi-tui crash log hardcodes ~/.pi/agent/, ignoring PI_CODING_AGENT_DIR](https://github.com/earendil-works/pi/issues/6652)**  
   *Author: luminary19 | Comments: 4 | Status: OPEN, inprogress*  
   TUI crash logs ignore custom directory configuration, cluttering home directories. Impacts users with non-default `.pi` locations.

7. **[#6794 — Pi startup super slow due to model catalogue refresh](https://github.com/earendil-works/pi/issues/6794)**  
   *Author: LarsEckart | Comments: 3 | Status: CLOSED*  
   Startup latency issue caused by synchronous model catalogue refresh. Affected morning load times and initial responsiveness. Closed with fix.

8. **[#6647 — Compaction fails on a single transient stream drop (no retry)](https://github.com/earendil-works/pi/issues/6647)**  
   *Author: axelbaumlisto | Comments: 2 | Status: OPEN, inprogress*  
   Auto-compaction lacks retry logic for transient failures, causing entire compaction to fail. Contrasts with normal assistant turns that handle `terminated` errors gracefully.

9. **[#6888 — Default system prompt causes Claude Pro/Max OAuth failures](https://github.com/earendil-works/pi/issues/6888)**  
   *Author: itligt | Comments: 1 | Status: CLOSED*  
   Pi's system prompt triggers third-party classification on Claude OAuth, causing 400 errors on Pro/Max accounts. Critical for Anthropic users with overage disabled.

10. **[#6820 — Queued message dropped after threshold auto-compaction](https://github.com/earendil-works/pi/issues/6820)**  
    *Author: lallenlowe | Comments: 2 | Status: CLOSED*  
    Messages typed during auto-compaction are silently dropped, showing `Agent is already processing`. Affects interactive users during compaction events.

## Key PR Progress

1. **[#6216 — Add Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/6216)**  
   *Author: unexge | Status: OPEN*  
   Integrates Amazon Bedrock Mantle's OpenAI-compatible endpoint. Significant for AWS users seeking Bedrock integration with existing Pi workflows. Supersedes an earlier PR.

2. **[#6881 — Use provider-reported cost when responses include it](https://github.com/earendil-works/pi/pull/6881)**  
   *Author: R-Taneja | Status: OPEN*  
   Respects billed cost from provider responses (e.g., Vercel AI Gateway) instead of always computing from catalog rates. Improves cost accuracy for gateway-mediated providers.

3. **[#6775 — Retry on compaction/branch summarization retryable failures](https://github.com/earendil-works/pi/pull/6775)**  
   *Author: davidbrai | Status: OPEN*  
   Directly addresses #6647. Adds retry logic to compaction summarization for transient failures. The author asks whether to add UI retry indication—community input needed.

4. **[#6765 — Separate generated model data into JSON files](https://github.com/earendil-works/pi/pull/6765)**  
   *Author: mitsuhiko | Status: CLOSED*  
   Structural improvement: moves generated model values to separate JSON files while keeping TS catalog structure. Expected to reduce repo churn from model additions.

5. **[#6864 — Fix: env section ignored in auth.json](https://github.com/earendil-works/pi/pull/6864)**  
   *Author: cristinaponcela | Status: CLOSED*  
   Fixes #6799 where provider-scoped env values (e.g., `AZURE_OPENAI_BASE_URL`) in auth.json were silently ignored. Critical for Azure and custom endpoint users.

6. **[#6858 — Add Qwen Token Plan as built-in provider](https://github.com/earendil-works/pi/pull/6858)**  
   *Author: QuintinShaw | Status: CLOSED*  
   Adds Qwen Token Plan (international and China) following the Xiaomi Token Plan pattern. Expands built-in provider coverage for Alibaba Cloud models.

7. **[#6854 — Fix tool_call_id error when switching models](https://github.com/earendil-works/pi/pull/6854)**  
   *Author: cristinaponcela | Status: CLOSED*  
   Resolves tool call ID normalization when switching from OpenAI Responses to completions models. Prevents session corruption from suffix stripping.

8. **[#6859 — Use bun info for package update checks](https://github.com/earendil-works/pi/pull/6859)**  
   *Author: yolonir | Status: CLOSED*  
   Small but quality-of-life fix: `bun view` treated as missing command; switches to `bun info` for extension update notifications. Helps the growing Bun user base.

9. **[#6874 — Add Ctrl+A archive shortcut to session picker](https://github.com/earendil-works/pi/pull/6874)**  
   *Author: GaussAA | Status: CLOSED*  
   New keyboard shortcut to archive sessions in the `/resume` picker. Archive preserves data while cleaning active list—useful for power users.

10. **[#6837 — Align GPT-5.6 Codex context with official client](https://github.com/earendil-works/pi/pull/6837)**  
    *Author: artplan1 | Status: CLOSED*  
    Sets GPT-5.6 (Sol, Terra, Luna) context windows to 272K for openai-codex. Keeps long-context pricing tiers. Responds to accuracy gap with official client.

## Feature Request Trends

- **Ephemeral model/session scoping** (#5263, #6820, #6844): Strong momentum for session-scoped model settings and paste marker management. Users want local changes without persisting to defaults.
- **Multimodal prompt expansion** (#3200): Extending image-only prompts to video/audio. Driven by new multimodal models (Gemma 4, GPT-4o) and expected to grow.
- **Extension API surface growth** (#6509, #6876, #6863): Multiple requests for richer extension hooks—custom usage reporting, message rendering overrides, session file rewrite capabilities, and lifecycle metadata exposure.
- **Provider ecosystem expansion** (#6216, #6858, #6886): Steady demand for new providers (Bedrock Mantle, Qwen Token Plan, Anthropic fallback) and cost accuracy improvements.

## Developer Pain Points

1. **Provider cost calculation inaccuracies** (#6725, #6877, #6881): Repeated issues with mismatched billing between Pi's catalog and actual provider charges. The Copilot GPT-5.6 pricing bug and Gateway cost integration highlight this as a persistent pain point.
2. **Configuration/environment variable handling** (#6799, #6652, #5034): auth.json environment scoping ignored for some providers, crash log directory hardcoded, and misleading proxy-related error messages. Configuration consistency remains fragile.
3. **Session corruption and compaction reliability** (#6820, #6647, #6883, #6844): Messages dropped during compaction, single-failure compaction crash, paste registry corruption, and general session invalidation from extension errors. Session lifecycle robustness is a recurring theme.
4. **Startup performance** (#6794): Model catalogue refresh delays blocking startup. Users sensitive to latency in CLI tools.
5. **TUI text handling** (#5931, #5407): Copy-paste quality issues and terminal-specific double-keypress bugs (Kitty vs COSMIC Terminal). Small but frequent annoyances.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-21

## Today's Highlights

A massive day for the **autofix loop** — the CI fleet and managed-PR automation stack saw major improvements including gate-crash retry, real-time fork PR pickup, and review-thread resolution. Meanwhile, the **TokenPlan `enable_thinking` bug** generated multiple duplicates before a fix landed, and the Web Shell token persistence issue drew two competing PRs. The `subagent` tool schema interplay with OpenAI-compatible providers also emerged as a critical friction point.

---

## Releases

**v0.20.0-nightly.20260721.cda0e0348** — [Release Notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.20.0-nightly.20260721.cda0e0348)
- feat(autofix): label-driven takeover and release; fix forced-dispatch green no-op
- fix(autofix)

---

## Hot Issues (10 Selected)

1. **#7284** — `bug(core): side-query forces enable_thinking=false, breaking TokenPlan endpoints`  
   *P1, 3 comments. [Link](https://github.com/QwenLM/qwen-code/issues/7284)*  
   `runSideQuery` (used by `web_fetch`, classifiers, etc.) hardcodes `enable_thinking: false`, causing 400 errors on endpoints that require it `true`. This is the root cause that triggered two duplicate reports (#7359, #7366). **Hot today** because it blocks all TokenPlan users from using web_fetch and other side-query tools.

2. **#7316** — `Bug: OpenAI toolCall特殊反应导致 subAgent 完全无法使用`  
   *P2, 3 comments. [Link](https://github.com/QwenLM/qwen-code/issues/7316)*  
   OpenAI-compatible models return empty strings for optional `working_dir`, despite schema only requiring `description` & `prompt`. This produces semantically conflicting fields, making `agent` tool (with `isolation: "worktree"`) completely unusable. **High friction** because many users rely on OpenAI-compatible providers.

3. **#7040** — `RFC: Reliable auto-memory recall — timing, quality, and telemetry`  
   *P2, 7 comments. [Link](https://github.com/QwenLM/qwen-code/issues/7040)*  
   Narrowed RFC (per core-memory maintainer feedback) focusing on recall-path improvements for all users, rather than a full enterprise memory governance platform. Three independently-reviewable work items. **Most commented active RFC**.

4. **#7147** — `MCP server never successfully get tool and resource listing`  
   *P2, 6 comments. [Link](https://github.com/QwenLM/qwen-code/issues/7147)*  
   Fastmail MCP server authentication works, but tool listing times out. A real-world integration failing silently. **Welcomes PRs**.

5. **#6414** — `vscode qwen code Failed to connect to Qwen agent`  
   *5 comments. [Link](https://github.com/QwenLM/qwen-code/issues/6414)*  
   Long-standing VS Code extension connectivity issue, still needing information from reporter. Frequent stub for Windows/VSCode connection problems.

6. **#7301** — `Web Shell loses bearer token on page refresh when daemon started with --token`  
   *P2, 2 comments. [Link](https://github.com/QwenLM/qwen-code/issues/7301)*  
   `qwen serve --token "xxx" --open` works on initial load, but a page refresh drops the `Authorization` header. **Now has two competing PRs** (#7372 and #7374).

7. **#7315** — `Agent tool schema forces mutually exclusive working_dir and isolation parameters`  
   *P1, 2 comments. [Link](https://github.com/QwenLM/qwen-code/issues/7315)*  
   OpenAI-compatible providers cause `working_dir` and `isolation` to both be treated as required, breaking all subagent launch modes. Compounded with #7316 — **P1 severity** for subagent users.

8. **#7023** — `Model switch can invalidate a loaded daemon session`  
   *P2, 3 comments. [Link](https://github.com/QwenLM/qwen-code/issues/7023)*  
   Daemon session becomes unavailable after model switch. Affects WebShell/daemon users with multiple configured models. **Includes daemon label**.

9. **#7306** — `Harden tool-output budgeting, observability, and artifact lifecycle`  
   *P2, 2 comments. [Link](https://github.com/QwenLM/qwen-code/issues/7306)*  
   Tool outputs pass through multiple independent truncation paths (shell, scheduler, batch-offload), each with different thresholds. Proposes unified budget, telemetry, and explicit artifact lifecycle. **Needs discussion**.

10. **#7348** — `Support context-inheriting subagents in headless mode without silent fallback`  
    *P2, 1 comment. [Link](https://github.com/QwenLM/qwen-code/issues/7348)*  
    `subagent_type: "fork"` request is only honored interactively; headless/sdk/CI silently falls back. Blocks automated evaluation and CI/CD subagent use cases. **Roadmap: subagents-tools, background-automation**.

---

## Key PR Progress (10 Selected)

1. **#7374** — `fix(web-shell): persist the daemon bearer token per-tab so it survives refresh`  
   *Open. [Link](https://github.com/QwenLM/qwen-code/pull/7374)*  
   Writes token from URL into `sessionStorage` on first load; falls back to it on refresh. Competitor #7372 takes a similar approach. Both address #7301.

2. **#7367** — `fix(cli): show worktree branch in status line instead of workspace branch`  
   *Open, autofix/takeover. [Link](https://github.com/QwenLM/qwen-code/pull/7367)*  
   Fixes git branch indicator in CLI TUI and Web Shell composer to show worktree's branch when a worktree session is active. Small UX win for parallel-worktree users.

3. **#7364** — `feat(autofix): resolve the review threads whose findings it implemented`  
   *Open, autofix/takeover. [Link](https://github.com/QwenLM/qwen-code/pull/7364)*  
   Autofix loop now resolves review threads that it actually addressed, so human re-reviewers see only what's still open. Referenced by issue #7308.

4. **#7350** — `feat(autofix): pick up managed fork PRs in real time instead of waiting for throttled schedule`  
   *Open, autofix/takeover. [Link](https://github.com/QwenLM/qwen-code/pull/7350)*  
   The `pull_request_review` trigger now admits more than just feedback from core-team members — opens real-time feedback to managed fork PRs. Reduces latency from hours to seconds.

5. **#7351** — `fix(autofix): retry a verification-gate crash instead of burying the agent's fix`  
   *Open, autofix/takeover. [Link](https://github.com/QwenLM/qwen-code/pull/7351)*  
   Distinguishes gate rejection from gate crash; retries crash so the agent's work is preserved. Base PR for #7368.

6. **#7358** — `fix(ci): stop a slow patrol classifier from killing every flaky rerun`  
   *Open, autofix/takeover. [Link](https://github.com/QwenLM/qwen-code/pull/7358)*  
   CI Failure Patrol was 28/30 runs cancelled due to one slow classifier step. This PR isolates that step. **Keeps the patrol running**.

7. **#7365** — `feat(web-shell): surface worktree isolation in the new-session empty state`  
   *Open, autofix/takeover. [Link](https://github.com/QwenLM/qwen-code/pull/7365)*  
   Moves worktree-isolated session entry from sidebar pill to chat empty state — a visible toggle below the welcome header. **UX improvement for discoverability**.

8. **#7368** — `feat(autofix): feed the gate's rejection back so the retry can fix what it broke`  
   *Open, autofix/takeover. [Link](https://github.com/QwenLM/qwen-code/pull/7368)*  
   Stacked on #7351. Carries gate rejection reason back into the loop so mechanical rejections are auto-fixed. **Closes the autofix feedback loop**.

9. **#7346** — `feat(core): add fork_turns to fork subagents`  
   *Open. [Link](https://github.com/QwenLM/qwen-code/pull/7346)*  
   Optional `fork_turns` parameter limits inherited context to N real user turns. Omitting or `"all"` preserves current behavior. **Targets #7348's headless subagent gap**.

10. **#7369** — `chore: add CODEOWNERS for cua-driver and mobile-mcp`  
    *Open. [Link](https://github.com/QwenLM/qwen-code/pull/7369)*  
    Sets @LaZzyMan as code owner for `packages/cua-driver/` and `packages/mobile-mcp/`. Community PRs touching these will require owner approval. **Process improvement for new package domains**.

---

## Feature Request Trends

1. **Subagent/Fork Robustness** — Multiple requests for real context inheritance in headless mode (#7348), `fork_turns` parameter (#7346), and fixing schema conflicts with OpenAI-compatible providers (#7315, #7316).

2. **Memory & Telemetry** — RFC for reliable auto-memory recall (#7040) and content-safe runtime telemetry for channel memory recall (#7335) signal growing investment in memory observability and quality.

3. **CI/CD & Automation Governance** — CODEOWNERS for core harness (#7299), PR intake automation (#3957), tool-output budgeting and artifact lifecycle (#7306). The project is maturing its automation governance.

4. **Configuration & SDK** — Custom display names for registered workspaces (#7170), overridable default-disabled for skills (#7347), configurable ACP initialize handshake timeout (#7244). SDK consumers want more control.

5. **Web Shell UX** — Token persistence across refresh (two competing PRs), worktree isolation in empty state (#7365). Web Shell is becoming a first-class surface.

---

## Developer Pain Points

1. **TokenPlan `enable_thinking` restriction** — The `runSideQuery` hardcode caused three duplicate reports (#7284, #7359, #7366). This single bug blocked web_fetch and all side-query tools for TokenPlan users. **Most impactful bug of the day.**

2. **OpenAI-compatible provider compatibility** — Issues #7315 and #7316 both stem from OpenAI models returning empty strings for optional parameters. The `agent` tool schema doesn't guard against this, making subagents completely unusable. **P1-level friction for the "bring your own model" crowd.**

3. **Web Shell token loss on refresh** — The `qwen serve --token` flow breaks on the simplest user action (Ctrl+R). Two competing PRs (#7372 and #7374) suggest the fix is non-trivial and the community is waiting.

4. **Daemon session invalidation on model switch** (#7023) — Switching models while a daemon session is loaded silently breaks the session. Affects power users with multiple configured models.

5. **CI Failure Patrol instability** (#7358) — 28/30 runs cancelled, effectively offline for hours. The patrol is a key maintenance mechanism; its fragility creates blind spots for regressions.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest
**Date:** 2026-07-21 | **Project:** Codewhale (formerly DeepSeek-TUI)

---

## Today's Highlights

A massive v0.9.1 stabilization push dominated the past 24 hours, with maintainer **Hmbown** closing over 20 release-blocker issues targeting child execution isolation, permission model unification, and session identity pinning. Community contributions landed key fixes for Moonshot/Kimi provider compatibility, Windows TUI rendering, and HarmonyOS build support, signaling the project is hardening for a v0.9.1 launch.

---

## Releases

No new releases in the last 24 hours. The project remains at **v0.9.0** while the surge of v0.9.1 release-blocker fixes queued above continues.

---

## Hot Issues

| # | Title | State | Comments | Why It Matters |
|---|-------|-------|----------|----------------|
| [#4032](https://github.com/Hmbown/CodeWhale/issues/4032) | Codewhale not following the constitution | OPEN | 40 | **Most-discussed bug.** Codewhale ignores user-provided scripts and writes its own temporary ones, then rationalizes the behavior. A fundamental trust/reliability issue that erodes the "agent-ready" promise. Community frustrated by lack of resolution. |
| [#4605](https://github.com/Hmbown/CodeWhale/issues/4605) | Enter key send lag — UI freezes for hundreds of ms | OPEN | 2 | **P1 performance regression.** Unfixed across v0.6.0–v0.9.0 on Windows. A core UX touchpoint that makes the TUI feel sluggish. Reported by **bevis-wong** who has been filing detailed Windows bugs. |
| [#4603](https://github.com/Hmbown/CodeWhale/issues/4603) | Long output content cannot scroll | OPEN | 2 | **Major accessibility gap.** Content is truncated beyond viewport with no scroll mechanism. Critical for reviewing large diffs/multi-turn conversations. A PR (#4653) already landed today to address this. |
| [#4604](https://github.com/Hmbown/CodeWhale/issues/4604) | Setup wizard forced on every restart | CLOSED | 2 | **Rapidly resolved blocking bug.** First-run flag not persisted — users saw onboarding flow every session. Fixed within hours by PR #4616. Good example of the project's current velocity. |
| [#4598](https://github.com/Hmbown/CodeWhale/issues/4598) | Make Operate delegate bounded leaves by default | OPEN | 1 | **Architecture shift.** Automating leaf delegation in Operate mode, currently just a prompt-policy change — no new scheduler or cost model. Foundational for scalable agent decomposition. |
| [#2889](https://github.com/Hmbown/CodeWhale/issues/2889) | Work Agent rows: real sub-agent details | OPEN | 4 | **UX quality-of-life.** Sidebar currently shows opaque agent rows. Community member **aboimpinto** volunteered to drive this. High-value for multi-agent workflow visibility. |
| [#4412](https://github.com/Hmbown/CodeWhale/issues/4412) | Resolve Ask, Auto-Review, and Full Access through one permission contract | OPEN | 1 | **Security unification.** Currently three separate permission paths — this merges them into one typed decision before every tool call. Critical for consistent security posture. |
| [#3934](https://github.com/Hmbown/CodeWhale/issues/3934) | Collapse Fleet and agent roles to Planner/Worker/Reviewer/Verifier | OPEN | 2 | **Role simplification.** Reduces cognitive overhead by standardizing roles across all contexts (sub-agents, Fleet, MCP). Part of the v0.9.1 cleanup. |
| [#4644](https://github.com/Hmbown/CodeWhale/issues/4644) | Replace DeepSeek-specific fallback with provider-neutral state | CLOSED | 1 | **Provider neutrality.** Removes hardcoded DeepSeek fallback so other providers (Moonshot, xAI) never silently inherit the wrong model. Strategic move toward multi-provider readiness. |
| [#4489](https://github.com/Hmbown/CodeWhale/issues/4489) | Hooks process leak on Windows | CLOSED | 6 | **Windows reliability.** Hook commands leak `node.exe` processes because only `cmd.exe` is killed on timeout. Persistent pain point for Windows users. |

---

## Key PR Progress

| # | Title | State | What It Does |
|---|-------|-------|--------------|
| [#4653](https://github.com/Hmbown/CodeWhale/pull/4653) | Lock long-output transcript scrolling with PTY scenario | OPEN | Tests the fix for #4603 (truncated output). Uses a sealed loopback reply spanning 3+ viewports. Ensures content is retained, scrollable, and not truncated. |
| [#4618](https://github.com/Hmbown/CodeWhale/pull/4618) | Keep long-running tools live | CLOSED | Prevents the 10-minute TUI stall watchdog from killing healthy long-running tool calls. Adds cancellable heartbeats around tool execution. |
| [#4613](https://github.com/Hmbown/CodeWhale/pull/4613) | Sanitize Moonshot tool parameters per MFJS spec | CLOSED | Community contributor **bistack** fixes Moonshot/Kimi compatibility: root-level `anyOf`/`oneOf`/`allOf` are rejected by MFJS. Recursively normalizes schemas so `apply_patch` and `financial_analysis` tools work. |
| [#4616](https://github.com/Hmbown/CodeWhale/pull/4616) | Make onboarding completion durable | CLOSED | Fixes the "setup wizard every restart" bug (#4604). Persists first-run marker through `CODEWHALE_HOME` state, keeps existing experiments intact. |
| [#4609](https://github.com/Hmbown/CodeWhale/pull/4609) | Respect umask for workspace atomic writes | CLOSED | **SamhandsomeLee** separates workspace file permission policy from Codewhale's private persistence. Prevents overly permissive temp files. |
| [#4566](https://github.com/Hmbown/CodeWhale/pull/4566) | Update TUI Cargo.toml for HarmonyOS build | OPEN | Community member **shenyongqing** keeps HarmonyOS support alive. Moves `portable-pty` to unix gate; successfully compiled and ran TUI on HarmonyOS PC. |
| [#4610](https://github.com/Hmbown/CodeWhale/pull/4610) | Add configurable session token header | OPEN | **XhesicaFrost** adds opt-in token usage display to the TUI header (cumulative input/cache-hit/output counts). Configurable via `tui.header_items`. |
| [#4600](https://github.com/Hmbown/CodeWhale/pull/4600) | Auto-fork read-only children onto parent's cached prefix | CLOSED | **Major token-cost reduction.** Previously each subagent cold-started (~100K input tokens). Now read-only children share parent's cached system prompt/tools/context. |
| [#4602](https://github.com/Hmbown/CodeWhale/pull/4602) | CODEWHALE_* precedence and product-identity cleanup | CLOSED | Naming migration: `CODEWHALE_*` env vars now take priority with `DEEPSEEK_*` as fallback. No legacy variables removed. Part of the DeepSeek→Codewhale rebranding. |
| [#4510](https://github.com/Hmbown/CodeWhale/pull/4510) | Keep keycap and emoji rendering grapheme-safe | CLOSED | **SparkofSpike** fixes TUI corruption on Windows where keycap/emoji sequences broke column counting. A long-standing rendering issue. |

---

## Feature Request Trends

1. **Provider-Agnostic Architecture** — Multiple issues (#4644, #4613, #4617) push to remove DeepSeek-specific assumptions. Users want seamless switching between DeepSeek, Moonshot, xAI, and custom providers without silent fallback surprises.

2. **Permission Model Unification** — The old Ask/Auto-Review/Full Access split is being collapsed into one typed permission decision (#4412). Users want a consistent, predictable security model rather than three different paths.

3. **Role and Terminology Simplification** — The "Planner/Worker/Reviewer/Verifier" consolidation (#3934) and "Plan/Act/Operate" composer colors (#4642) show demand for reduced cognitive overhead in multi-agent workflows.

4. **Windows UX Parity** — Three high-severity Windows bugs this week (#4605, #4603, #4604) plus the process leak (#4489) indicate Windows support is a critical growth area. Frequent reporter **bevis-wong** is highlighting gaps.

5. **Token Cost Transparency** — The session token header (#4610) and auto-fork caching (#4600) are user-driven responses to token waste. The ecosystem is demanding visibility and efficiency in expensive multi-agent calls.

---

## Developer Pain Points

- **Subagent Cold-Start Cost:** Every subagent re-prefilled ~100K input tokens of system prompt, tools, and context that the parent already paid for. PR #4600 (auto-fork read-only children) addresses this, but it's a strong signal the architecture wasn't optimizing for multi-agent token reuse.

- **Windows Reliability Gap:** Hooks leak processes (#4489), setup wizard fails to persist (#4604), and Enter-key freezes persist across 3+ minor versions (#4605). The TUI's Windows experience lags behind Linux/macOS significantly.

- **Permission Confusion:** Three separate permission paths (Ask, Auto-Review, Full Access) with inconsistent modal/automatic behavior. Issue #4412 and PR #4608 aim to unify, but the current state creates developer uncertainty about what will happen when a tool is called.

- **Scrolling and Output Truncation:** Long outputs cannot be scrolled (#4603), and the TUI freezes during message send (#4605). Both are fundamental usability issues for a CLI tool where developers review large diffs and logs.

- **Model Schema Fragility:** Moonshot/Kimi reject standard JSON Schema constructs (`anyOf`, `oneOf`) at the root level (#4613), causing tools like `apply_patch` to silently fail. Each provider has unique schema quirks, and the project lacks a universal normalization layer.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*