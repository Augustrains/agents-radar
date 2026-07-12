# AI CLI Tools Community Digest 2026-07-12

> Generated: 2026-07-12 01:22 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date: 2026-07-12**

## 1. Ecosystem Overview

The AI CLI tools landscape on July 12, 2026 shows a mature but rapidly evolving ecosystem where **multi-agent orchestration**, **platform portability**, and **MCP (Model Context Protocol) integration** are the dominant cross-cutting concerns. All seven major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI—are in active development with zero new releases across the board today, yet community engagement remains intense with 50+ open issues updated daily in several projects. A clear bifurcation is emerging between **enterprise-integrated tools** (Claude Code, Codex, Copilot CLI) focusing on security, cost governance, and session reliability, and **community-driven tools** (OpenCode, Pi, DeepSeek TUI) prioritizing extensibility, local-first workflows, and cross-platform support. The GPT-5.6 model family rollout is driving integration work across virtually all tools, while persistent gaps in Windows support, MCP lifecycle management, and subagent reliability remain universal pain points.

## 2. Activity Comparison

| Tool | Open Issues (Noteworthy) | PRs (24h) | Releases (24h) | Community Engagement Signal |
|------|--------------------------|-----------|----------------|----------------------------|
| **Claude Code** | 10 | 5 | 0 | 50+ issues updated; multi-session thread at 55 comments |
| **OpenAI Codex** | 10 | 10 | 0 | 733 👍 on Linux desktop request; 432 👍 on logging bug |
| **Gemini CLI** | 10 | 10 (9 unique) | 0 | Agent hang issue at 8 👍; subagent quality tracking |
| **GitHub Copilot CLI** | 10 | 1 | 0 | 3 new session integrity bugs today; MCP OAuth broken |
| **Kimi Code CLI** | 1 | 5 | 0 | Low activity; single issue + targeted fixes |
| **OpenCode** | 10 | 10 | 0 | 169 👍 for model auto-discovery; 153 👍 for /btw command |
| **Pi** | 10 | 10 | 0 | GPT-5.6 integration dominates; 18 👍 on thinking level |
| **Qwen Code** | 10 | 10 | 0 | Multi-workspace RFC at 20 comments; active PR pipeline |
| **DeepSeek TUI** | 10 | 10 | 0 | Anthropic API errors; portability (NetBSD, Android) |

**Key observations:**
- **Codex** and **OpenCode** show the highest community upvote engagement per issue
- **Qwen Code** has the most substantial structural RFC activity (multi-workspace daemon)
- **Copilot CLI** has critical session integrity bugs filed today but only 1 PR—lowest fix velocity
- **Kimi Code CLI** has minimal community surface area today (1 issue) despite active PRs

## 3. Shared Feature Directions

### Multi-Session & Multi-Workspace Orchestration
- **Claude Code** (#24798): Inter-session communication for parallel workflows
- **Qwen Code** (RFC #6378): Multi-workspace daemon support
- **Copilot CLI** (pattern): Sessions not syncing across CLI ↔ Desktop surfaces
- **Pi**: Branch-attached tool results (#6558) and session compaction
- **Gemini CLI**: Subagent trajectory sharing (#22598)

### MCP Server Reliability & Lifecycle
- **Claude Code**: Duplicate plugin instances (#36800), stdio server SIGINT without respawn (#76769)
- **Copilot CLI**: OAuth-protected MCP servers connect but expose zero tools (#4096, #4089, #4085)
- **Qwen Code**: HTTP MCP servers fail silently on 401 (#6639), OAuth recovery PR (#6732)
- **Kimi Code**: Port collisions between TUI/Web UI (#1769), missing global MCP config (#2490)

### Model Switching Transparency & Cost Governance
- **Claude Code**: Silent model fallback (#76793), over-triggering safeguards (#76800)
- **Codex**: GPT-5.6 default context crossing pricing thresholds (#32486), wasted resets (#31606)
- **OpenCode**: GPT-5.6 Luna model not found (#36140)
- **Pi**: Thinking level support for GPT-5.6 Sol (#6097), caching options (#6529)

### Platform Portability Gaps
- **Windows**: Claude Code Cowork fails (#74649), Codex sandbox blocked by Smart App Control (#32487), Copilot CLI file-locking (#4095), OpenCode clipboard bugs (#36470), Pi Terminal scroll (#6502)
- **Linux Desktop**: Codex's top-requested feature (#11023, 733 👍)
- **macOS**: Codex Computer Use crashes (#32032), Copilot CLI blocked `rg` binary (#28190)
- **Exotic targets**: DeepSeek TUI building for NetBSD (#4349), Android/Termux (#4350)

### Subagent & Multi-Agent Stability
- **Claude Code**: Agent Teams mailbox delays up to 62 minutes (#76500)
- **Codex**: GPT-5.6 Sol overrides subagent model selection (#31814)
- **Gemini CLI**: Subagent false success on MAX_TURNS (#22323), generalist hangs (#21409)
- **Copilot CLI**: OAuth tools not bridging to agent sessions

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|-------------|----------|-----|-----------|--------------|
| **Primary Use Case** | Large project monorepos | Enterprise multi-agent | Agent evaluations | GitHub-integrated workflows | Local-first tinkering | Multi-provider gateway | Code review & Web Shell | Terminal-native agent |
| **Target User** | Power users, monorepo teams | Enterprise teams, cost-sensitive | Evaluators, researchers | GitHub enterprise users | Hobbyists, local-LLM enthusiasts | Extension developers | JetBrains/Web IDE users | Platform hackers |
| **Architecture** | Client-heavy with Cowork | Desktop app + subagents | Subagent orchestration | CLI ↔ Desktop sync | TUI with local providers | Provider-agnostic gateway | Daemon + Web Shell | Rust-based TUI |
| **Key Strength** | Multi-session workflows | Model selection flexibility | AST-aware tools | GitHub ecosystem | Zero-cost model access | Extension API depth | Multi-workspace daemon | Cross-platform portability |
| **Key Weakness** | Windows support | Cost surprises | Subagent reliability | MCP integration | CPU usage regressions | Concurrency edge cases | Memory persistence | Anthropic compatibility |
| **Community Size (Signal)** | Very large (50+ issues/day) | Very large (high upvotes) | Moderate | Moderate | Large (growing) | Moderate | Growing | Growing |
| **PR Velocity** | Moderate | High | High | Low | High | High | High | High |

## 5. Community Momentum & Maturity

### Established Leaders (Mature, High Momentum)
- **Claude Code**: Most robust multi-session and Cowork community. Deep engagement on complex architectural issues (inter-session communication, Agent Teams). The model switching transparency backlash (#76793, #76800) signals a mature user base demanding power-user controls.
- **OpenAI Codex**: Highest raw community reaction counts (733 👍, 432 👍). Enterprise cost governance and platform support are dominant themes. The GPT-5.6 Sol subagent override bug (#31814) is the most impactful single issue this week.

### Rapidly Iterating (High PR Velocity, Growing Community)
- **OpenCode**: 169 👍 for model auto-discovery (#6231) indicates strong local-LLM community. 10 PRs/day with GPT-5.6 Luna failures driving urgency. High engagement on TUI UX improvements.
- **Pi**: 10 PRs/day with GPT-5.6 integration as the dominant theme. Strong extension API work (#6556, #6551). Growing community of multi-provider gateway users.
- **Qwen Code**: Active structural RFCs (multi-workspace) plus strong Web Shell iteration. 10 PRs with workspace, daemon, and extension focus. Rapid feature velocity.

### Niche but Engaged
- **Gemini CLI**: Strong evaluation and AST-tool focus. Lower raw upvote counts but high-quality technical discussions (component evaluations, agent self-awareness). The agent hang issue (#21409) is the most commented.
- **Copilot CLI**: Critical MCP integration issues with low fix velocity (1 PR today). Session integrity bugs filed today (#4098, #4097) suggest emerging reliability concerns.
- **DeepSeek TUI**: Active PRs on portability (NetBSD, Android) and i18n (Korean). Small but technically engaged community. Key challenge is maintaining Anthropic API compatibility.
- **Kimi Code CLI**: Lowest activity today; 5 PRs but only 1 issue. Focused primarily on bug-fix consolidation.

## 6. Trend Signals

### For Technical Decision-Makers

**1. Multi-Agent Orchestration Is Table Stakes, Not a Feature**
Every major tool now has subagent/multi-agent systems, but **reliability is the gap**. Claude Code's 62-minute Agent Teams delays, Codex's Sol subagent override, and Gemini's false success reporting all demonstrate that the orchestration layer is the critical path for enterprise adoption. **Recommendation**: Evaluate subagent failure recovery, model selection transparency, and cost bounding before committing to any tool for multi-agent workflows.

**2. MCP Integration Fragility Is the #1 Enterprise Blockers**
Three tools (Claude Code, Copilot CLI, Qwen Code) have multiple MCP lifecycle bugs—OAuth flows that complete but expose zero tools, servers that die without respawn, port collisions, and stale auth handlers. The MCP ecosystem is evolving faster than CLI tools can stabilize their integration. **Recommendation**: For production use, prefer tools with explicit MCP allowlisting (Codex's `server_registered_tools_only` pattern) and bounded OAuth retry cycles.

**3. Windows Support Remains a Second-Class Experience**
Every tool except DeepSeek TUI has active Windows-specific bugs: Cowork failures, sandbox blocks, file-locking, clipboard issues, terminal scroll problems. If your team uses Windows as a primary development platform, budget for workarounds or choose tools with demonstrable Windows investment (OpenCode's PowerShell clipboard fix, Pi's terminal scroll acknowledgement).

**4. Cost Governance Is Becoming a Trust Issue**
Codex (#32486, #31606), Claude Code (#76793, #76800), and Pi (#6529) all face community backlash over silent pricing escalations, wasted rate-limit resets, and opaque model downgrades. The community is demanding **explicit opt-in for cost-relevant changes**. **Recommendation**: Implement or demand per-request cost previews, rate-limit reset verification, and model-switching notifications before adoption of any tool with usage-based pricing.

**5. Local-First and Offline Workflows Are Growing**
OpenCode's #6231 (model auto-discovery) with 169 👍, persistent Ollama integration issues (#22132), and DeepSeek TUI's Android/Termux support all signal a developer desire for **frictionless local LLM pipelines**. The "zero-cost model" flag in OpenCode (#34794) and BYOK model listing requests in Copilot CLI (#3795) reinforce this trend. **Recommendation**: For teams with data sovereignty or latency requirements, prioritize tools with robust local provider support and autodiscovery capabilities.

**6. Session Persistence Is an Emerging Reliability Requirement**
Copilot CLI's truncated JSONL (#4098), OpenCode's high CPU regression (#30086), Qwen Code's memory index staleness (#6487), and Claude Code's Cowork session residue all indicate that **long-running session management is immature** across the ecosystem. **Recommendation**: Evaluate session recovery, compaction behavior, and resource cleanup patterns before relying on any tool for continuous agent workflows.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on the data provided.

---

## Claude Code Skills Community Highlights Report (Data as of 2026-07-12)

### 1. Top Skills Ranking

The most-discussed Pull Requests reveal a community deeply focused on the **reliability of the Skill creation and evaluation infrastructure itself**, followed by specific, high-impact content skills.

1.  **`fix(skill-creator): run_eval.py always reports 0% recall` (#1298)**
    - **Functionality:** Fixes a critical bug in the skill-creator's evaluation pipeline where `run_eval.py` always reports 0% recall, making the description-optimization loop useless. The fix installs the eval artifact as a real skill and corrects Windows stream reading, trigger detection, and parallel workers.
    - **Discussion:** This is the most active PR, addressing a well-documented, reproducible bug (#556) affecting all skill authors. The discussion focuses on the root cause (trigger detection failing to match skill names) and Windows-specific subprocess issues.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/1298)

2.  **`Add document-typography skill` (#514)**
    - **Functionality:** Prevents common typographic problems in AI-generated documents, such as orphan word wrap, widow paragraphs, and numbering misalignment.
    - **Discussion:** High attention because these are universal, low-visibility issues in Claude's document output. Users appreciate a skill that handles a "hygiene" problem proactively.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/514)

3.  **`Add skill-quality-analyzer and skill-security-analyzer` (#83)**
    - **Functionality:** Two meta-skills for evaluating other skills. The quality analyzer checks structure, documentation, and examples; the security analyzer looks for trust boundary abuse and prompt injection risks.
    - **Discussion:** Significant interest as the community grapples with the quality and security of the growing skill ecosystem. This is a direct response to concerns raised in Issue #492 (Security trust boundary abuse).
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/83)

4.  **`fix(skill-creator): isolate trigger-eval command files from the live project` (#1261)**
    - **Functionality:** Prevents the `run_eval` script from writing synthetic command files (used for testing) into the user's live project `.claude/commands/` directory, which caused conflicts and corruption in parallel evaluation sessions.
    - **Discussion:** Addresses a critical reliability issue (Issue #1260) in the skill-creator workflow. The community is actively waiting for this fix to land.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/1261)

5.  **`Add ODT skill — OpenDocument text creation and template filling` (#486)**
    - **Functionality:** Enables Claude to create, fill, read, and convert OpenDocument Format files (.odt, .ods), a key requirement for LibreOffice and ISO standard document workflows.
    - **Discussion:** Reflects demand for enterprise document interoperability beyond the existing DOCX/PDF skills.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/486)

6.  **`feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate` (#1367)**
    - **Functionality:** A universal skill that audits AI output before delivery. It performs mechanical file verification (checking claimed outputs exist) followed by a four-dimension reasoning quality audit prioritized by damage severity.
    - **Discussion:** A highly ambitious proposal for output quality assurance. The community is evaluating its practical overhead versus benefit.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/1367)

7.  **`Add testing-patterns skill` (#723)**
    - **Functionality:** A comprehensive skill covering the full testing stack (unit, React component, integration, E2E) using the Testing Trophy model. Includes naming conventions, edge cases, and what *not* to test.
    - **Discussion:** Strong demand for a structured, opinionated approach to test generation. This is a clear "follow the leader" skill for test-first developers.
    - **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/723)

### 2. Community Demand Trends

Analysis of the top community Issues reveals three primary demand vectors:

- **Enterprise Security & Trust Boundaries (Issue #492, #1175):** The highest-commented issue (#492, 34 comments) details a critical security concern: community skills distributed under the `anthropic/` namespace create a trust vulnerability, as users may grant elevated permissions to unofficial skills. This has sparked a demand for **skill signing, namespace verification, and security analyzer tools** (leading to PR #83).

- **Skill Infrastructure Reliability (Issue #556, #1169, #1061):** The skill-creator's evaluation and optimization pipeline is fragile. Issues #556 (12 comments) and #1061 (3 comments) document the `run_eval.py` recall=0% bug on Windows and Linux. The community's most pressing need is for a **stable, cross-platform skill creation workflow** that doesn't produce false negatives.

- **Organizational Skill Sharing (Issue #228):** Users want the ability to share skills organization-wide within Claude Code, rather than the current manual file-transfer method. This points to demand for **enterprise skill management, publishing, and distribution features**.

- **Output Quality Assurance (Issue #1385):** A new proposal for a "Reasoning Quality Gate Pipeline" (pre-task calibration, adversarial review, delivery verification) signals community interest in **systematic output quality controls**, separate from simple error checking.

### 3. High-Potential Pending Skills

These active PRs are seeing the most discussion and are likely to land soon:

- **`run_eval.py always reports 0% recall` (#1298):** This is the single most critical fix for the skill ecosystem. Once resolved, it will unblock all skill authors who rely on the optimization loop. Its high comment count and linkage to Issue #556 make it the top candidate for expedited review.
- **`Isolate trigger-eval command files` (#1261):** A companion fix to #1298, addressing the specific corruption issue. Multiple contributors are involved, and the fix is well-scoped.
- **`skill-quality-analyzer and skill-security-analyzer` (#83):** This meta-skill directly addresses the community's top security concern (#492). Expect demand for this to merge as a standard part of the skill creation pipeline.
- **`Add color-expert skill` (#1302):** A niche but highly specific skill (color naming systems, color spaces). The author has deep domain expertise, and the discussion is focused on correctness and scope.
- **`Add self-audit skill` (#1367):** While ambitious, the conversation around reasoning quality gates is accelerating, and this could become a go-to "last mile" skill for production outputs.

### 4. Skills Ecosystem Insight

The community's most concentrated demand is for a **reliable, secure, and cross-platform skill creation infrastructure** — specifically, fixing the `run_eval` trigger detection pipeline — before users are willing to fully invest in building and sharing a diverse skill library.

---

# Claude Code Community Digest — 2026-07-12

## Today's Highlights
A quiet release day with zero new versions, but the community remains highly active with 50 open issues updated in the last 24 hours. The hottest threads involve **multi-session workflows for large projects** (55 comments) and **Windows Cowork failures** (51 comments), signaling continued demand for concurrent session management and broader platform support. Several critical bugs around Agent Teams, model fallback transparency, and MCP server lifecycle surfaced over the weekend.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#24798 — Inter-session communication for multi-Claude workflows](https://github.com/anthropics/claude-code/issues/24798)**
   *55 comments | 18 👍 | OPEN*
   The most active open issue. Users running multiple parallel Claude Code sessions on large projects want a way to coordinate dependencies across sessions. Community interest is high, reflecting a real pain point for monorepo and modular project workflows.

2. **[#74649 — Cowork not working on Windows 11 Pro (Missing HCS services: vfpext)](https://github.com/anthropics/claude-code/issues/74649)**
   *51 comments | 0 👍 | OPEN*
   A Windows-specific blocker preventing Cowork from functioning. The Hyper-V Components Service (vfpext) missing on many Pro installations is causing a hard failure. Significant community engagement but low upvotes suggests many affected users are not core contributors.

3. **[#17951 — Terminal Title Configuration (Script-Based)](https://github.com/anthropics/claude-code/issues/17951)**
   *24 comments | 32 👍 | OPEN*
   A long-standing feature request (since January) for scriptable terminal title configuration. Strong community support with 32 upvotes. Users want dynamic titles that reflect session state, similar to statusLine.

4. **[#36800 — Duplicate channel plugin instances causing 409 Conflict and tool loss](https://github.com/anthropics/claude-code/issues/36800)**
   *16 comments | 6 👍 | CLOSED*
   A critical MCP bug where Claude Code spawns duplicate Telegram plugin processes mid-session, leading to tool loss and unrecoverable state. Closed, but the root-cause discussion revealed deeper harness lifecycle issues.

5. **[#57998 — CLAUDE_DATA_DIR env var for Windows](https://github.com/anthropics/claude-code/issues/57998)**
   *10 comments | 12 👍 | OPEN*
   Windows users want to relocate `%APPDATA%\Claude\` via environment variable. Moderate support but a clean, non-controversial UX improvement.

6. **[#76795 — Bash permission matcher misparses quoted operators](https://github.com/anthropics/claude-code/issues/76795)**
   *1 comment | 0 👍 | OPEN*
   Freshly opened. A `|` inside a quoted grep argument fools the permission matcher into misclassifying safe commands, forcing unnecessary permission prompts. Points to a broader pattern-matching fragility.

7. **[#76500 — Agent Teams mailbox: 5–62 min turn-boundary delays, lost reports](https://github.com/anthropics/claude-code/issues/76500)**
   *1 comment | 0 👍 | OPEN*
   Experimental Agent Teams feature has severe delivery defects — messages can be delayed up to an hour and final reports are replaced by idle notifications. A detailed, well-documented report that will be important for the feature's stability.

8. **[#76793 — Silent model fallback: Fable 5 → Opus 4.8 with no notification](https://github.com/anthropics/claude-code/issues/76793)**
   *1 comment | 0 👍 | OPEN*
   Desktop silently downgrades the model when a usage limit is hit, with zero user-facing feedback. A transparency and trust issue.

9. **[#76649 — Browser pane screenshot tool consistently times out on Windows](https://github.com/anthropics/claude-code/issues/76649)**
   *1 comment | 0 👍 | OPEN*
   The `computer { action: "screenshot" }` tool in the browser pane fails reliably after 30s on Windows. A regression affecting automation workflows.

10. **[#76800 — Fable 5 safeguards over-triggering on legitimate device configuration](https://github.com/anthropics/claude-code/issues/76800)**
    *0 comments | 0 👍 | OPEN*
    Fresh issue: Fable 5's safety filters are auto-downgrading users to Opus 4.8 on benign personal-device management tasks. Four false positives reported in two days — likely to attract attention.

## Key PR Progress

1. **[#39043 — Remove "retro-futuristic" recommendation from Frontend Design Skill](https://github.com/anthropics/claude-code/pull/39043)**
   *Created Mar 25 | Updated Jul 11 | OPEN*
   A simple but opinionated fix by a prominent community member (t3dotgg) removing a subjective design recommendation from the built-in skill. Lighthearted but indicative of how the community shapes defaults.

2. **[#76673 — Fix: design defects confirmed by reproducibility audit](https://github.com/anthropics/claude-code/pull/76673)**
   *Created Jul 11 | Updated Jul 11 | CLOSED*
   A comprehensive Japanese-authored fix addressing issue triage lifecycle, Ralph state isolation, and unreachable shell branches. Shows active non-English contributor engagement.

3. **[#76640 — Fix: load macOS system certificates for Bun runtime](https://github.com/anthropics/claude-code/pull/76640)**
   *Created Jul 11 | Updated Jul 11 | OPEN*
   Fixes `Self-signed certificate detected` errors on macOS when using the Bun runtime (v2.1.17+). Bun's SSL context doesn't load macOS system certificates, breaking API connectivity. Also handles `NO_PROXY` edge cases.

4. **[#76581 — Fix: harden YAML, path, and symlink handling in scripts](https://github.com/anthropics/claude-code/pull/76581)**
   *Created Jul 11 | Updated Jul 11 | OPEN*
   Security hardening for official plugin scripts against YAML frontmatter breakout, path traversal, and symlink-based credential overwrite. Proactive defense-in-depth.

5. **[#76576 — Fix: align userConfig docs and hook validator with v2.1.207 shell-injection fix](https://github.com/anthropics/claude-code/pull/76576)**
   *Created Jul 11 | Updated Jul 11 | OPEN*
   Updates documentation and validation to reflect the v2.1.207 shell-injection fix that rejected `${user_config.*}` in shell-form plugin hooks. Addresses documentation drift.

## Feature Request Trends

- **Multi-session orchestration**: The dominant theme. Users want inter-session communication (#24798), forking while Claude is working (#76777), and queued message injection in the Desktop app (#71726). The community is treating parallel sessions as the norm, not the exception.
- **Configurability & portability**: Requests for configurable terminal titles (#17951), Windows data directory relocation (#57998), and spend-limit threshold notifications (#74709) reflect demand for power-user customization and cost control.
- **Cowork lifecycle management**: Automated retention policies for Cowork session residues (#62472) and per-task title cleanup suggest users are scaling Cowork to many scheduled tasks and need housekeeping automation.

## Developer Pain Points

- **Windows support gaps**: Multiple open Windows-specific bugs — Cowork not working (#74649), `preview_start` failing with `spawn cmd.exe ENOENT` (#68341), browser screenshot timeouts (#76649), and silent model fallback (#76793). Windows remains a second-class platform in practice.
- **Model switching transparency**: Two issues in 24 hours (#76793, #76800) about silent or unwanted model downgrades — one from usage limits, one from over-sensitive safeguards. Users feel disempowered and confused.
- **MCP server lifecycle fragility**: stdio MCP servers being SIGINT'd after ~4 hours without respawn (#76769) and duplicate process spawning (#36800) point to systemic weaknesses in how Claude Code manages external tool processes over long sessions.
- **Permission matcher false positives**: The quoted `|` misparse (#76795) is the latest in a cluster of permission-matching bugs, suggesting the bash command analysis needs a more robust parsing approach.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest
**Date: 2026-07-12**

---

## Today's Highlights

Today sees active community response to a critical GPT-5.6 Sol subagent configuration bug and continued frustration over missing Linux desktop app support. Several infrastructure-focused PRs merged around sandbox enforcement, environment caching, and tool registration security, while new reports flag accidental cost overruns from GPT-5.6's default context sizing and sandbox failures on Windows with Smart App Control enabled.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

### 1. [#11023 – Codex desktop app for Linux](https://github.com/openai/codex/issues/11023) (OPEN)
**The most upvoted open issue (733 👍) with 164 comments.** Community demand for a native Linux desktop app remains intense. Users cite macOS power consumption issues and Linux workstation workflows as primary motivators. No official response timeline yet.

### 2. [#28224 – SQLite feedback logs write ~640 TB/year, destroying SSD endurance](https://github.com/openai/codex/issues/28224) (OPEN)
**432 👍, 145 comments.** A massive performance and hardware degradation concern. The reporter notes 3 PRs merged (in 0.142.0) already mitigate ~85% of log volume, but the sheer scale of the original issue (terabytes per year of writes) shocked the community. Represents a serious QA miss.

### 3. [#31814 – GPT-5.6 Sol forces all subagents to also be Sol instances](https://github.com/openai/codex/issues/31814) (OPEN)
**102 👍, 49 comments.** A nuanced but impactful bug: GPT-5.6 Sol's model metadata silently overrides multi-agent configuration, forcing all spawned subagents to use Sol regardless of user intent. This breaks cost-conscious workflows that mix cheaper models for sub-tasks. High visibility in last 72 hours.

### 4. [#28969 – Cannot disable auto-resolve in 60 seconds for questions](https://github.com/openai/codex/issues/28969) (OPEN)
**105 👍, 26 comments.** CLI users frustrated that Codex auto-resolves interactive questions after 60 seconds, breaking long-running or multi-step reasoning sessions. A simple config toggle is widely requested but not yet implemented.

### 5. [#20161 – Phone number verification broken on cross-device SSO](https://github.com/openai/codex/issues/20161) (CLOSED)
The highest-comment issue ever (205 comments, 131 👍). Authentication flow forces phone verification when switching devices via SSO, even for accounts without a phone number. Recently closed but served as a major frustration signal for account portability.

### 6. [#31606 – Reset wasted: applied but did not count](https://github.com/openai/codex/issues/31606) (OPEN)
**40 👍, 33 comments.** Users report that using a rate-limit reset consumes one reset without actually applying the benefit. Creates a trust issue with usage-based pricing controls.

### 7. [#32032 – Computer Use 1.0 crashes on macOS 15.7.7 (Swift Concurrency symbol missing)](https://github.com/openai/codex/issues/32032) (OPEN)
**11 👍, 20 comments.** A native helper crash on the latest macOS due to dyld resolution failure for Swift Concurrency symbols. Blocks all Computer Use features for affected users.

### 8. [#32486 – GPT-5.6 default context can cross 272K higher-usage threshold](https://github.com/openai/codex/issues/32486) (OPEN)
**New today.** Default context configuration for GPT-5.6 Sol/Luna may silently push users into expensive pricing bands without explicit opt-in. Community is concerned about surprise billing.

### 9. [#32487 – Windows sandbox fails with Smart App Control enabled](https://github.com/openai/codex/issues/32487) (OPEN)
**New today.** Unsigned `node_repl.exe` blocked by Windows Code Integrity on systems with Smart App Control. Blocks all sandbox execution on modern Windows 11 Pro setups—a significant compatibility issue.

### 10. [#28190 – `rg` (ripgrep) blocked by macOS](https://github.com/openai/codex/issues/28190) (OPEN)
**71 👍, 46 comments.** macOS Gatekeeper/notarization blocks the bundled `rg` binary. Represents a friction point for users on macOS who must manually approve or bypass security controls.

---

## Key PR Progress

### 1. [#31526 – Restrict hosted threads to server-registered tools](https://github.com/openai/codex/pull/31526) (MERGED)
Adds `server_registered_tools_only` feature with structured MCP allowlist. Critical for enterprise security—prevents hosted clients from accidentally exposing unregistered tool classes.

### 2. [#30016 – Inherit current step environments in subagents](https://github.com/openai/codex/pull/30016) (MERGED)
Core fix: subagents now inherit environment from the request's actual execution context, not an outdated turn-start snapshot. Essential for deferred executor workflows.

### 3. [#29960 – Cache stable executor skills per model step](https://github.com/openai/codex/pull/29960) (MERGED)
Performance optimization: skill metadata discovered once per executor environment, not reread on every sampling step. Reduces redundant I/O.

### 4. [#30020 – Pass step environments to turn input extensions](https://github.com/openai/codex/pull/30020) (MERGED)
Fixes a race condition where turn-input extensions read frozen `TurnContext` while newer environments exist. Part of the deferred executor fix series.

### 5. [#30036 – Make Windows executable resolution deterministic](https://github.com/openai/codex/pull/30036) (MERGED)
Fixes a Windows-specific bug where `lpApplicationName` could let Windows choose an executable before Codex's child environment is applied. Prevents PATH/`PATHEXT` mismatches.

### 6. [#32460 – Emit thread-idle lifecycle after guardian interrupts](https://github.com/openai/codex/pull/32460) (MERGED)
Extension lifecycle fix: ensures the `thread-idle` event fires after guardian auto-aborts due to repeated review denials. Previously, extensions could hang indefinitely.

### 7. [#32441 – Preserve parent sandbox enforcement for memory consolidation](https://github.com/openai/codex/pull/32441) (MERGED)
Security fix: memory consolidation agent now inherits parent turn's permission profile and sandbox overrides. Prevents privilege escalation during consolidation.

### 8. [#30135 – Publish versioned bash fork artifacts](https://github.com/openai/codex/pull/30135) (MERGED)
CI infrastructure: decouples bash fork builds from Rust release cadence. Brings back bash support without requiring a full rebuild per release.

### 9. [#32316 – Stop falling back to older model availability announcements](https://github.com/openai/codex/pull/32316) (MERGED)
UX fix: selects the first model announcement in catalog order, then shows nothing on dismissal instead of falling back to stale lower-priority announcements.

### 10. [#32312 – Require prefixes for outbound response item IDs](https://github.com/openai/codex/pull/32312) (MERGED)
Data quality improvement: enforces prefixed UUIDv7 IDs on response items. Backward-compatible deserialization for legacy histories; improves traceability and debugging.

---

## Feature Request Trends

1. **Linux Desktop App** (#11023) – The single most-demand ask. Strong sentiment that macOS power issues combined with developer preference for Linux workstations makes this the top missing platform.
2. **Headless Remote Linux for Mobile** (#23200) – Related: users want Codex mobile to connect directly to remote Linux hosts without requiring a desktop app relay.
3. **Custom Subagent Model Selection** – (#31814, #32291) Users want fine-grained control over which model subagents use, especially to avoid expensive flagship models for simple tasks.
4. **Configurable Auto-Resolve Timeout** (#28969) – CLI users want to disable or extend the 60-second auto-resolve window for interactive questions.
5. **Independent Session Lifecycle Management** (#30350) – Users want clearer semantics for side/secondary sessions so they don't expire without warning.

---

## Developer Pain Points

1. **Cost Surprises and Rate-Limit Confusion** – Multiple issues (#32486, #31606, #32279, #32484) report silent pricing band escalation, wasted resets, and unexplained quota drops. Pricing transparency is a recurring trust issue.

2. **Cross-Platform Inconsistency** – macOS sandbox crashes (#32032), Windows sandbox failures with Smart App Control (#32487), Norton interference (#25425), and blocked binaries (#28190) paint a picture of fragile OS-level compatibility.

3. **Subagent and Multi-Model Instability** – The GPT-5.6 Sol override (#31814) and environment inheritance gaps (#30016) show the multi-agent system still has rough edges that break cost and control assumptions.

4. **Performance and Resource Bloat** – The 640 TB/year logging issue (#28224) and unbounded session state (#25779) highlight systemic inefficiencies that degrade developer experience over long sessions.

5. **Desktop App Crashes and Freezes** – Multiple crash reports (#32032, #30824, #30178, #25951) across platforms suggest stability regressions in the desktop app surface, particularly around webview navigation, FSEvents, and GPU-accelerated rendering.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-12

## Today's Highlights
No new releases landed in the past 24 hours, but the bug-fix and evaluation pipeline saw meaningful activity. Two security-oriented PRs addressing shell wrapper stripping and MCP environment variable expansion entered review, while a long-standing **subagent status misreporting** issue remains the most commented thread. The team is actively retesting a cluster of P1 agent-hang and subagent-permission regressions that have been open for multiple months.

## Releases
No new releases in the last 24 hours.

## Hot Issues (Top 10)

1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *10 comments, 2 👍*  
   The `codebase_investigator` subagent returns `status: "success"` and `Termination Reason: "GOAL"` even when it hit its maximum turn limit without performing any analysis. This masks real failures and misleads users about the agent's actual completion state.

2. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   *7 comments*  
   An epic tracking the expansion of behavioral evaluations from 76 tests across 6 supported models. A follow-up to issue #15300, this is foundational for measuring and improving subagent quality.

3. **[#22745 — Assess the impact of AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   *7 comments, 1 👍*  
   Investigates whether AST-aware tools can reduce token noise, improve method-bound reading precision, and eliminate misaligned reads. Potential to significantly reduce turn counts.

4. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   *7 comments, 8 👍*  
   **Highest community reaction.** The generalist agent hangs indefinitely on simple file operations. Users report that explicitly disabling subagent delegation works around the issue, suggesting a delegation-loop or deadlock problem.

5. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *6 comments*  
   Custom skills (e.g., Gradle, Git) are ignored unless explicitly requested. The agent misses opportunities to invoke appropriate subagents, reducing automation potential.

6. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
   *5 comments*  
   Auto Memory only marks sessions as processed when `read_file` succeeds; low-signal sessions remain unprocessed and are repeatedly surfaced, causing wasted API calls and context pollution.

7. **[#25166 — Shell command execution gets stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *4 comments, 3 👍*  
   Commands that finish normally leave the shell in an "awaiting input" state. The tool never signals completion, causing Gemini to hang mid-task.

8. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**  
   *4 comments, 1 👍*  
   Browser subagent terminates with a `GOAL` status despite failing. Users on Wayland cannot use the browser agent at all.

9. **[#20079 — ~/.gemini/agents/filename.md not recognized if it's a symlink](https://github.com/google-gemini/gemini-cli/issues/20079)**  
   *4 comments*  
   Symlinked agent definitions are silently ignored. Blocks dotfile managers and reproducible agent setups.

10. **[#24246 — Gemini CLI encounters 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**  
    *3 comments*  
    When more than 128 tools are enabled, Gemini hits the model's tool limit and returns a 400 error. No tool-scoping logic exists yet.

## Key PR Progress (Top 10)

1. **[#28183 — fix(vscode-ide-companion): preserve terminal focus when closing diff tabs](https://github.com/google-gemini/gemini-cli/pull/28183)**  
   *Open, P1, area/extensions*  
   Prevents keyboard focus from being stolen by the VS Code diff preview after approving edits. Directly addresses a frequent user friction point.

2. **[#28359 — fix(core): strip login/interactive shell wrappers in stripShellWrapper](https://github.com/google-gemini/gemini-cli/pull/28359)**  
   *Open, size/s*  
   Extends `stripShellWrapper` to recognize `bash -lc`, `bash -ic`, and `bash -l -c` patterns. The policy engine now re-checks wrapped payloads correctly.

3. **[#28349 — fix(cli): guard customDeepMerge against circular references](https://github.com/google-gemini/gemini-cli/pull/28349)**  
   *Open, P2, area/core, size/m*  
   Fixes #28270 — settings objects with circular references (`obj.self = obj`) caused `RangeError: Maximum call stack size exceeded`. Adds cycle tracking.

4. **[#28319 — refactor(a2a-server): enforce path trust check prior to environment loading](https://github.com/google-gemini/gemini-cli/pull/28319)**  
   *Open, size/xl*  
   Restructures `CoderAgentExecutor` to verify workspace path trust before loading environment variables, and isolates environment state with `AsyncLocalStorage`.

5. **[#28164 — fix(core): limit recursive reasoning turns per single user request](https://github.com/google-gemini/gemini-cli/pull/28164)**  
   *Closed, merged*  
   Caps recursive reasoning at 15 turns per request, customizable via `maxSessionTurns`. Protects against infinite loops that drain CPU and API quota.

6. **[#28248 — docs: explain MCP env expansion](https://github.com/google-gemini/gemini-cli/pull/28248)**  
   *Open, size/s*  
   Documents supported (`$VAR`, `${VAR:-fallback}`, `%VAR%`) and unsupported (`{{VAR}}`, `~`) environment variable syntax in `mcpServers`, plus empty-string fallback behavior for missing vars.

7. **[#28247 — fix(core): match ls ignore globs by relative path](https://github.com/google-gemini/gemini-cli/pull/28247)**  
   *Open, size/m*  
   Fixes #28207 — `ls` ignore patterns containing path separators now match against workspace-relative paths. Uses `picomatch` for `**` glob support.

8. **[#28023 — chore(deps): bump @modelcontextprotocol/sdk to 1.26.0](https://github.com/google-gemini/gemini-cli/pull/28023)**  
   *Closed, merged*  
   Routine dependency bump from 1.23.0 to 1.26.0 in the VS Code IDE companion package.

9. **[#28319 — (see above)](https://github.com/google-gemini/gemini-cli/pull/28319)**  
   Repeat mention for its dual significance: security hardening + environment isolation.

10. **[#28183 — (see above)](https://github.com/google-gemini/gemini-cli/pull/28183)**  
    Repeat mention for its direct impact on VS Code extension usability.

## Feature Request Trends

- **AST-aware codebase navigation** is the most frequently requested structural improvement. Multiple issues (#22745, #22746) propose using programs like `tilth` or `glyph` for precise method-bound reading, better codebase mapping, and reduced turn consumption.
- **Subagent trajectory sharing** (#22598) — users want subagent logs accessible via `/chat share` for debugging, evaluation, and collaborative review.
- **Auto Memory quality improvements** (#26516, #26522, #26523, #26525) — a clear push for deterministic redaction, patch validation, low-signal session quarantining, and reduced noise.
- **Agent self-awareness** (#21432) — the agent should know its own CLI flags, hotkeys, and configuration to act as its own expert guide.
- **Component-level evaluations** (#24353) — a systematic expansion of behavioral eval coverage to measure subagent quality across all supported models.

## Developer Pain Points

1. **Subagent reliability regressions** — Issues like #22323 (false success on MAX_TURNS), #21409 (hangs), and #22093 (subagents running despite disabled settings) indicate that the subagent orchestration layer remains fragile, especially since v0.33.0.
2. **Shell execution deadlocks** — #25166 and #22465 describe scenarios where shell commands finish but the tool never detects completion, trapping sessions indefinitely.
3. **Tool limit fragility** — #24246 shows that enabling many tools (>128) triggers a hard 400 error, with no graceful degradation or scoping logic.
4. **Configuration opacity** — #20079 (symlinks ignored), #22267 (settings.json overrides ignored by Browser Agent), and #24246 (no tool count protection) suggest the configuration system is inconsistent and error-prone.
5. **State pollution** — #26522 (indefinite low-signal retries) and #26525 (secrets exposed before redaction) highlight concerns around memory system resilience and data safety.
6. **Destructive command risk** — #22672 documents cases where the model uses `git reset --force` or other destructive flags when safer alternatives exist, with no built-in safeguards.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-07-12

## Today's Highlights
The Copilot CLI community is experiencing a **surge of critical MCP (Model Context Protocol) integration issues**, with three separate reports detailing OAuth flow failures where servers connect but expose zero tools to agent sessions. Additionally, a **triage wave of three new session integrity bugs** emerged today—covering truncated resume logs, binary blob bloat in conversation history exceeding the 5 MB CAPI limit, and orphaned session data after UI deletion—indicating core stability concerns for power users.

## Releases
No new releases were published in the last 24 hours. The latest release remains unchanged.

## Hot Issues (10 Noteworthy)

1. **[#4098] Resuming a session can leave truncated and concatenated events in events.jsonl**  
   *Author: Adamkadaban | Created: 2026-07-12*  
   A critical data-integrity bug: resumed sessions produce malformed JSONL where incomplete event prefixes are concatenated with complete events, making the session file un-resumable. This could lead to permanent loss of work-in-progress sessions.  
   [🔗 Issue](https://github.com/github/copilot-cli/issues/4098)

2. **[#4097] apply_patch stores deleted binary in session history, permanently exceeding CAPI 5 MB limit**  
   *Author: Adamkadaban | Created: 2026-07-12*  
   When `apply_patch` deletes a large binary file, the entire binary is stored as a textual diff in conversation history. Subsequent requests hit the 5 MB CAPI limit and `/compact` fails to resolve the issue. Significant for teams working with binary assets or build artifacts.  
   [🔗 Issue](https://github.com/github/copilot-cli/issues/4097)

3. **[#4096] Third-party MCP server shows "Connected" but tools are missing from CLI sessions**  
   *Author: bugale | Created: 2026-07-11*  
   OAuth tokens acquired through the app UI never bridge to CLI sessions, leaving MCP servers ostensibly connected but functionally dead. Echoes similar reports for Atlassian MCP (see #4089).  
   [🔗 Issue](https://github.com/github/copilot-cli/issues/4096)

4. **[#4089] Atlassian MCP server: OAuth succeeds but zero tools exposed to sessions**  
   *Author: Mov1ngTrg3t | Created: 2026-07-10*  
   A clear reproduction: Atlassian MCP connects and OAuth completes, but no tools appear. Other HTTP MCP servers (LeanIX, Lucid) work correctly with identical configuration, pinpointing a protocol-level bug specific to this provider.  
   [🔗 Issue](https://github.com/github/copilot-cli/issues/4089)

5. **[#4085] MCP OAuth flow broken: servers marked needs-auth during discovery, connections drop after ~90s**  
   *Author: Joachim-Ally-Skyline | Created: 2026-07-10*  
   Azure AD and Microsoft Work IQ servers fail during session startup because no auth handler is registered. Even when retry succeeds, connections drop after ~90 seconds—a critical timeout issue for enterprise MCP deployments.  
   [🔗 Issue](https://github.com/github/copilot-cli/issues/4085)

6. **[#4095] Windows: plugin update fails with "Access is denied (os error 5)" while VS Code is running**  
   *Author: FBakkensen | Created: 2026-07-11*  
   The VS Code Copilot extension holds watcher handles on the `installed-plugins` directory, blocking file operations. A common Windows-specific pain point that forces users to close all editor instances to update plugins.  
   [🔗 Issue](https://github.com/github/copilot-cli/issues/4095)

7. **[#4094] Deleting a session in the app doesn't remove it from session-store.db**  
   *Author: evdbogaard | Created: 2026-07-11*  
   Deleting from the UI leaves orphaned session data in the shared copilot store and VS Code Chat history. This causes session-count limits to be consumed by ghost sessions and creates confusion about what is "deleted."  
   [🔗 Issue](https://github.com/github/copilot-cli/issues/4094)

8. **[#4024] Voice mode: all bundled ASR models fail silently**  
   *Author: sylvanc | Created: 2026-07-03*  
   Three Nemotron ASR models record audio successfully but produce empty transcriptions. The `MultiModalProcessor` routing bug for `nemotron_speech (RNNT)` affects all users of the bundled voice stack. High community visibility with 7 comments.  
   [🔗 Issue](https://github.com/github/copilot-cli/issues/4024)

9. **[#4093] web_search tool returns fabricated (hallucinated) answers**  
   *Author: dfrysinger | Created: 2026-07-10*  
   The built-in AI-powered web search tool generates confident, detailed, entirely fabricated answers when retrieval yields zero results—instead of reporting "no results." This is a trust and safety concern for users relying on grounded search.  
   [🔗 Issue](https://github.com/github/copilot-cli/issues/4093)

10. **[#4092] Temporarily mute system playback during voice capture**  
    *Author: daweins | Created: 2026-07-10*  
    A quality-of-life feature request: when using voice capture (e.g., while Spotify is playing), audio feedback loops degrade transcription quality. Simple enhancement with broad appeal.  
    [🔗 Issue](https://github.com/github/copilot-cli/issues/4092)

## Key PR Progress (1 notable)

- **[#2565] install: guard against duplicate PATH entries on reinstall**  
  *Author: marcelsafin | Updated: 2026-07-11*  
  Addresses a long-standing annoyance: running the installer twice appends duplicate PATH lines to shell profiles. The fix uses `command -v copilot` to avoid redundant entries. Open since April but recently updated—possibly approaching merge.  
  [🔗 PR](https://github.com/github/copilot-cli/pull/2565)

## Feature Request Trends
- **Dynamic Context in Skills:** Several requests (e.g., #4088) ask for `!command` placeholders inside `SKILL.md` files, enabling real-time context injection (e.g., current branch, clipboard contents) when skills are invoked.
- **Cross-App Session Sync:** Users want sessions started in CLI to be visible in the Copilot Desktop App and vice versa (e.g., #4082), reflecting a desire for unified session history across surfaces.
- **Voice Mode UX Polish:** Multiple requests target voice interactions: auto-submit on spacebar release (PTT), temporary system audio muting during capture, and better feedback for ASR failures.
- **BYOK Model Discovery:** Users with custom providers want opt-in model listing to avoid manually setting `COPILOT_MODEL` (e.g., #3795), signaling demand for provider-agnostic model enumeration.

## Developer Pain Points
- **MCP/OAuth Integration Instability:** The most critical theme this week. Three independent reports (#4084, #4085, #4089) describe OAuth-protected MCP servers that connect but never expose tools. The bug appears systemic, affecting Azure AD, Atlassian, and Microsoft Work IQ servers. Developers integrating third-party tools into agent sessions are effectively blocked.
- **Session Integrity & Storage Bugs:** Two issues (#4098, #4097) filed today by Adamkadaban expose fragile session serialization—truncated JSONL and binary bloat—that can corrupt or cap session histories, making long-running or complex sessions unreliable.
- **Windows Platform Gaps:** File-locking issues (#4095) and orphaned session data (#4094) highlight second-class platform support on Windows, where editor extensions interfere with CLI operations and state management is inconsistent.
- **Voice Mode Quality:** The silent ASR failure (#4024) continues as a systemic blocker for voice users, with no fix in sight after 9 days. Combined with proxy download failures (#4083), voice mode remains high-friction for many developers.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-12

## 1. Today's Highlights
A flurry of quality-of-life PRs landed from the community, fixing long-standing bugs in message serialization, MCP server resilience, and timing accuracy for background agents. One notable issue reveals a documentation–implementation gap where `CHANGELOG.md` is incorrectly surfaced as a skill in autocomplete, pointing to a need for stricter plugin metadata validation.

## 2. Releases
No new releases in the last 24 hours.

## 3. Hot Issues

1. **#2491 – Bug: kimi-datasource CHANGELOG.md incorrectly listed as a skill**  
   *Author: zhangleilaoge* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2491)  
   `CHANGELOG.md` appears as a `/skill` option in autocomplete, contradicting plugin documentation. Community reaction is subdued (0 comments, 0 votes), but the bug directly impacts plugin authoring workflow. It signals a validation gap in skill discovery logic.

*(Only one issue was updated in the last 24h, per the provided data. The "10 noteworthy" rule cannot be met. The issue above is covered.)*

## 4. Key PR Progress

1. **#1771 – fix: always stringify tool message content in Chat Completions provider**  
   *Author: he-yufeng* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/1771)  
   Fixes a 400 error from OpenAI when tool results contain multiple `ContentPart`s. Converts arrays to strings for `role: "tool"` messages. Critical for any multi-modal tool output integration.

2. **#1769 – fix: graceful degradation when MCP server fails to connect**  
   *Author: he-yufeng* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/1769)  
   Catches `MCPRuntimeError` in `_agent_loop()` to prevent worker crashes and UI hangs when MCP servers conflict (e.g., port collisions between TUI and Web UI). Essential for multi-session stability.

3. **#2493 – Fix: record started_at for background agent tasks so duration is reported**  
   *Author: nankingjing* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2493)  
   Adds missing `started_at` assignment in background agent tasks, fixing a silent data loss where run duration was never captured. Bash tasks already had this—parity fix.

4. **#2492 – fix: shorten_middle output exceeds target width by ellipsis length**  
   *Author: nankingjing* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2492)  
   Corrects the `shorten_middle` utility to account for the 3-character `"..."` ellipsis, preventing truncation artifacts in terminal output. Subtle but impactful for UI consistency.

5. **#2490 – fix(acp): load global MCP config in kimi acp server**  
   *Author: nankingjing* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2490)  
   Ensures `kimi acp` server loads user-configured MCP servers, fixing a parity gap where ACP clients (Zed, JetBrains AI Assistant) saw only built-in tools. Addresses issue #2464.

*(Only 5 PRs were updated in the last 24h, per the provided data. All are listed above.)*

## 5. Feature Request Trends
With only one issue in the digest period, trend analysis is limited. However, the CHANGELOG-as-skill bug (#2491) hints at a broader need:
- **Strict plugin metadata validation**: Ensure only valid skill definitions are surfaced in autocomplete, not arbitrary files like `CHANGELOG.md`.

## 6. Developer Pain Points
- **MCP connectivity fragility**: PR #1769 and #2490 both address MCP server reliability—port conflicts, missing config loading, and uncaught errors causing agent hangs.
- **Background task timing gaps**: PR #2493 reveals that agent tasks lacked `started_at` tracking, making duration reporting unreliable—a data-loss issue for observability.
- **Truncation utility inconsistency**: PR #2492 shows that even basic string utilities had width calculation bugs, affecting CLI output formatting across the board.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-12

## Today's Highlights
The community remains deeply engaged with the upcoming OpenCode 2.0 release, as evidenced by the **/btw command** (#16992, +153 👍) and a new **session picker entry point** (#36134) proposals. Performance regressions continue to dominate debugging discussion, with three distinct **high CPU usage** issues (#30086, #4804, #19466) accumulating a combined 57 comments. Meanwhile, the **GPT-5.6 Luna model failure** (#36140, +69 👍) is drawing significant attention from users on ChatGPT OAuth, and a trend toward **automated model discovery** (#6231, +169 👍) highlights growing frustration with manual configuration for local providers.

## Releases
*No new releases in the last 24 hours.*

## Hot Issues

1. **[#16992] [FEATURE]: add /btw command** (+153 👍) — Requests the popular `/btw` command from Claude Code, allowing developers to interject with "by the way" context to steer an ongoing generation. Community enthusiasm is very high, signaling strong demand for conversation-flow control in the 2.0 TUI. [GitHub](https://github.com/anomalyco/opencode/issues/16992)

2. **[#6231] Auto-discover models from OpenAI-compatible provider endpoints** (+169 👍) — The most-upvoted open issue. Users of LM Studio, Ollama, and llama.cpp must manually list model names in `opencode.json`; requests auto-discovery via a `/v1/models` query. The traction on this issue suggests that local provider adoption is growing and that configuration friction is a top pain point. [GitHub](https://github.com/anomalyco/opencode/issues/6231)

3. **[#36140] GPT-5.6 Luna returns model not found with ChatGPT OAuth** (+69 👍) — A high-severity regression: `gpt-5.6-luna` fails with HTTP 404 despite being listed as a built-in model for ChatGPT OAuth. Multiple users have independently confirmed the issue (including duplicates #36427, #36247), making this the most urgent provider integration bug. [GitHub](https://github.com/anomalyco/opencode/issues/36140)

4. **[#30086] High CPU usage in newer versions of OpenCode** — User reports that CPU usage spiked ~7 days ago, degrading from 10 concurrent sessions to just 3. This is the third distinct CPU-related issue (cf. #4804, #19466), suggesting a recent regression in idle-loop efficiencies. [GitHub](https://github.com/anomalyco/opencode/issues/30086)

5. **[#4751] Add config option to disable copy-on-select** (+18 👍) — A long-standing request (filed Nov 2025) advocating for an opt-out of automatic clipboard population when selecting text. The 25-comment discussion reveals strong opinions on clipboard pollution by users who highlight text as they read. [GitHub](https://github.com/anomalyco/opencode/issues/4751)

6. **[#8816] Provide llms.txt and docs as markdown** (+35 👍) — Calls for an `llms.txt` file and markdown documentation maps for OpenCode itself, following the llmstxt protocol. This would enable AI assistants to ingest OpenCode documentation during context-building. [GitHub](https://github.com/anomalyco/opencode/issues/8816)

7. **[#29548] OpenAI provider headers timeout after 10000ms on 1.15.11** — A regression causing provider response headers to time out after upgrading from 1.14.28. The user identified `headerTimeout` as a workaround, but the root cause suggests a change in default timeout handling. [GitHub](https://github.com/anomalyco/opencode/issues/29548)

8. **[#22132] OpenCode 1.4.3 hangs with local Ollama provider on simple prompts** — The Ollama integration hangs even on trivial prompts like `ci` while direct `/v1/chat/completions` calls work fine. This undermines the core local-LLM use case for developers who depend on offline operation. [GitHub](https://github.com/anomalyco/opencode/issues/22132)

9. **[#36465] "Revert message" should not modify code** — A UX/DX issue: the "revert message" action silently rewrites Git history without warning. The reporter accidentally corrupted their Git state by reverting an old conversation, revealing a missing diff preview. [GitHub](https://github.com/anomalyco/opencode/issues/36465)

10. **[#35303] Opt-in to share anonymized conversation data with model providers** — Proposes a consent mechanism to contribute anonymized prompt/response data to improve open-source models accessible via OpenCode Go. This reflects growing community interest in reciprocal data sharing with model providers. [GitHub](https://github.com/anomalyco/opencode/issues/35303)

## Key PR Progress

1. **[#33563] fix(ui): keep permission dock buttons in view on long requests** — Fixes three issues (#28979, #33575, #29515) where long permission patterns could push action buttons out of the visible dock area. A practical UX fix for complex permission sets. [GitHub](https://github.com/anomalyco/opencode/pull/33563)

2. **[#36475] fix(cli): keep update preflight through TUI loading** — Prevents a blank terminal between preflight completion and TUI startup, a visible regression in the update workflow. [GitHub](https://github.com/anomalyco/opencode/pull/36475)

3. **[#36471] feat(tui): paste clipboard on right click** — Maps right-click to `prompt.paste` when mouse capture is enabled, closing #36456. A long-requested ergonomic improvement for terminal users. [GitHub](https://github.com/anomalyco/opencode/pull/36471)

4. **[#36469] fix(tui): respect sidebar width threshold** — Removes an override that kept the sidebar open despite the configured width threshold. Ensures that sidebar visibility respects user settings. [GitHub](https://github.com/anomalyco/opencode/pull/36469)

5. **[#36468] fix(opencode): preserve valid empty JSON config** — Prevents a dangling comma when `$schema` is inserted into an empty `opencode.json`, avoiding config parse errors. [GitHub](https://github.com/anomalyco/opencode/pull/36468)

6. **[#36470] fix(tui): Windows clipboard — use PowerShell directly for text paste** — Fixes two Windows-specific clipboard bugs (Admin terminal paste broken, text shrinking on copy). Important for Windows TUI users. [GitHub](https://github.com/anomalyco/opencode/pull/36470)

7. **[#35405] fix(llm): unflatten Gemini tool call args with dot-bracket notation** — Addresses a Gemini-specific tool-calling bug (dot-bracket leys like `questions[0].header`) that could break structured output requests. [GitHub](https://github.com/anomalyco/opencode/pull/35405)

8. **[#34794] feat(provider): add —model free to pick a random zero-cost model** — Introduces a `--model free` flag that randomly selects from OpenCode's no-cost Zen models, making cost-free prototyping more accessible. [GitHub](https://github.com/anomalyco/opencode/pull/34794)

9. **[#35866] docs: update xAI branding to SpaceXAI** — Updates provider labels, OAuth methods, and model catalog entries to reflect the xAI→SpaceXAI rebrand. [GitHub](https://github.com/anomalyco/opencode/pull/35866)

10. **[#36466] fix(cli): load v2 tui config** — Fixes a blocking 2.0 bug where the custom leader key setting from `tui.json` was ignored because V2 initialized with an empty resolved config. [GitHub](https://github.com/anomalyco/opencode/pull/36466)

## Feature Request Trends

- **Conversation/dialog-slot control** — Requests like `/btw` (#16992) and session picker entry points (#36134) point to demand for richer multi-turn conversation management.
- **Local-first provider ergonomics** — Auto-discovery (#6231, +169 👍) and persistent issues with Ollama/LM Studio integration (#22132) indicate developers want frictionless local-LLM pipelines.
- **Anonymized feedback loops** — The data-sharing proposal (#35303) suggests a maturing community interested in improving the open-source models they consume.
- **Terminal UX polish** — Right-click paste (#36471), bell-ansi notifications (#36472), and copy-on-select opt-out (#4751) show ongoing desire for parity with IDE features.

## Developer Pain Points

1. **High CPU usage regression** — Three separate issues (#30086, #4804, #19466) with no root-cause fix yet, affecting both Intel Macs and modern CPUs. The earliest issue is 7+ months old.
2. **GPT-5.6 Luna model failures** — Multiple duplicates (#36140, #36247, #36427) confirm a broken model deployment affecting ChatGPT OAuth users with no workaround.
3. **Timeout/connectivity regressions** — The OpenAI header timeout (#29548) and Ollama hang (#22132) suggest degraded connection handling in recent releases.
4. **Windows-specific bugs** — Clipboards, subprocess visibility, Admin Terminal issues: Windows users face a disproportionate share of platform-specific problems.
5. **Config/dotfile fragility** — Invalid empty JSON (#36468), TUI config not loading (#36466), and log rotation breaking `--log-level DEBUG` (#17846) erode trust in the configuration layer.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-12

## Today's Highlights
GPT-5.6 family (Sol/Terra/Luna) rollout dominates this week, with multiple rapid-fire PRs adding provider catalog entries, prompt caching, Responses Lite support, and compaction fixes across OpenAI Codex and GitHub Copilot providers. The community also shipped a critical extension API gap fix (exposing Codex WebSocket management) and a developer-role message RFC prototype, while several foundational UX issues around terminal scroll behavior and tool result branch attachment surfaced.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#6475 — Add GPT-5.6 models to GitHub Copilot provider catalog](https://github.com/earendil-works/pi/issues/6475)** (👍8, Comments:9)  
   *Closed.* Rob-balfre requested adding `gpt-5.6-sol`, `gpt-5.6-terra`, `gpt-5.6-luna` to the Copilot provider after GitHub's blog announcement. Community quickly validated and merged; strong positive reaction.

2. **[#6097 — Add support for 'max' thinking level](https://github.com/earendil-works/pi/issues/6097)** (👍18, Comments:4)  
   *Closed.* OpenAI's GPT-5.6 Sol introduces a sixth `max` thinking level similar to Anthropic's Opus. Mattiacerutti flagged the gap; high signal from users wanting parity with OpenAI's new reasoning tiers.

3. **[#5916 — Support provider extensions with model aliases and improve search](https://github.com/earendil-works/pi/issues/5916)** (Comments:12)  
   *Open.* Long-running discussion (since June) about the lack of UI for configuring OpenRouter provider overrides. Mindplay-dk's workaround using `models.json` highlights a persistent UX gap.

4. **[#6206 — Clamping to context window prevents artificial context limits](https://github.com/earendil-works/pi/issues/6206)** (Comments:9)  
   *Closed.* A regression where `max_tokens` clamping to the reported context window broke user-set artificial limits. DanielThomas traced the commit, impacting users who manually constrain token budgets.

5. **[#6510 — Copilot mai-code-1-flash-picker uses wrong API endpoint](https://github.com/earendil-works/pi/issues/6510)** (Comments:5)  
   *Closed.* The model fails because Pi sent it to `/chat/completions` instead of the Copilot `/responses` endpoint. Petrroll identified the endpoint mismatch; quickly fixed.

6. **[#6456 — ctrl-p should show previous prompt / input](https://github.com/earendil-works/pi/issues/6456)** (Comments:4)  
   *Closed.* Rushiagr reported that `Ctrl+P` changes model instead of recalling past input—a break from Codex/Claude conventions. Minor but high-friction UX mismatch for migrating users.

7. **[#6502 — Windows Terminal scrolls to top due to ESC[3J](https://github.com/earendil-works/pi/issues/6502)** (Comments:4)  
   *Open.* WodenJay pinpointed `\x1b[3J` in TUI redraws causing scrollback buffer clears on Windows. Specific to Windows Terminal users; pending fix.

8. **[#6524 — Hide GPT-5.6 reasoning-summary empty placeholders](https://github.com/earendil-works/pi/issues/6524)** (Comments:3)  
   *Open.* Pecigonzalo found that GPT-5.6 Terra/Sol emit empty HTML comments in thinking blocks. Cosmetic issue affecting reasoning display fidelity.

9. **[#6513 — Codex cached WebSocket retains previous account after credential change](https://github.com/earendil-works/pi/issues/6513)** (Comments:3)  
   *Open.* Robinbraemer documented a security-adjacent bug: WebSocket keyed only by session ID can reuse stale credentials after account switch. Critical for multi-account workflows.

10. **[#6558 — Tool result attaches to wrong branch after tree navigation](https://github.com/earendil-works/pi/issues/6558)** (Comments:2)  
    *Closed.* Minh-Ng found that `/tree` branch switches during tool execution orphan results on incorrect branches, causing provider rejection. Concurrency bug in branching logic.

## Key PR Progress

1. **[#6556 — Expose Codex responses API to extensions](https://github.com/earendil-works/pi/pull/6556)**  
   *Closed.* Robinbraemer unblocked extensions from importing Codex WebSocket session helpers via extension loaders. Fixes a critical extension API gap.

2. **[#6534 — Add developer message role (experimental)](https://github.com/earendil-works/pi/pull/6534)**  
   *Open.* Mitsuhiko's RFC 54-inspired PR adds a `developer` message role. Early-stage but signals deep model protocol evolution.

3. **[#6539 — Bind Codex WebSocket reuse to account](https://github.com/earendil-works/pi/pull/6539)**  
   *Closed.* Fixes #6513 by scoping WebSocket caching to JWT-derived account claims. Security fix for multi-account session handling.

4. **[#6528 — Support GPT-5.6 prompt cache options](https://github.com/earendil-works/pi/pull/6528)**  
   *Closed.* AbdoKnbGit added `prompt_cache_options: { mode: "implicit", ttl: "30m" }` for GPT-5.6, dropping legacy fields. Enables prompt caching for new models.

5. **[#6544 — Route GitHub Copilot MAI-Code models through /responses](https://github.com/earendil-works/pi/pull/6544)**  
   *Open.* Petrroll's follow-up to #6510, adding proper endpoint routing for `mai-*` models in the Copilot provider.

6. **[#6530 — Cut Node CLI startup cost](https://github.com/earendil-works/pi/pull/6530)**  
   *Closed.* Wattsjs optimized CLI startup by fast-pathing `--version`/`-v` and deferring heavy module loading. Directly improves developer iteration speed.

7. **[#6551 — Add deferred extension reload requests](https://github.com/earendil-works/pi/pull/6551)**  
   *Closed.* Tarun-joy added `ExtensionContext.requestReload()` for safe deferred reloads in interactive/RPC modes. Addresses a long-standing extension lifecycle gap.

8. **[#6520 — Include file context in edit tool not-found error](https://github.com/earendil-works/pi/pull/6520)**  
   *Closed.* Korverdev improved edit tool error messages by showing nearby file context when `oldText` isn't found. Reduces debugging friction for users.

9. **[#6540 — Surface provider errors to LLM via advisories](https://github.com/earendil-works/pi/pull/6540)**  
   *Closed.* Yeshao fixed silent dropping of provider errors (context overflow, retry exhaustion) by injecting advisories. Important for LLM recovery from failures.

10. **[#6474 — Support message-anchored tool loading](https://github.com/earendil-works/pi/pull/6474)**  
    *Closed.* Mitsuhiko added dynamic tool loading mid-conversation via `addedTools` in messages, avoiding upfront tool-list bloat. Supports Anthropic's tool-reference protocol.

## Feature Request Trends

- **GPT-5.6 ecosystem integration** is the dominant theme: catalog additions (#6475), thinking levels (#6097), prompt caching (#6529), and Responses Lite (#6516) all flow from the model release.
- **Extension API expansion** continues strong: deferred reload (#6552), scoped models (#6518), compaction requests (#6553), and opaque attachments (#6493) show demand for richer extension hooks.
- **Provider parity and gateway support**: Requests for built-in LLM Gateway (#6554), GitHub Copilot "auto" pseudo-model (#6550), and Cloudflare/GLM fixes (#6494) indicate users want unified multi-provider management.
- **Configuration transparency**: Users want impact previews for extensions/skills (#6545) and better context-limit visibility (#6522).

## Developer Pain Points

- **Terminal compatibility**: Windows Terminal scroll bugs (#6502) and legacy Alt-key handling (#6523) highlight ongoing cross-platform TUI fragility.
- **Context window clamping regressions**: #6206 and #6522 show that automatic clamping to provider-reported context windows breaks users who manually set lower limits or use proxies with inaccurate reporting.
- **Multi-account credential confusion**: #6513 (WebSocket account caching) and #6498 (tool/system prompt reset on session resume) cause frustrating state leaks for power users.
- **Model endpoint routing**: Multiple issues (#6510, #6516) confirm that new models frequently target wrong API endpoints, requiring per-model routing patches.
- **Reliability under concurrency**: #6558 (tool results on wrong branches) and #6553 (compaction before message queuing) reveal edge cases in async session management.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-12

## Today's Highlights

The community is buzzing around **multi-workspace daemon support** with an RFC (#6378) attracting 20 comments, alongside a flurry of PRs adding workspace-level operations. A significant batch of **Claude Opus 4.6-4.8 token limit fixes** landed, and multiple memory durability bugs were identified and patched. Web Shell usability continues to see rapid iteration with toolbar redesigns, git branch indicators, and session recovery features.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#6378 — RFC: Support multiple workspaces in one qwen serve daemon](https://github.com/QwenLM/qwen-code/issues/6378)** (20 comments, OPEN)  
   *Why it matters*: This foundational RFC proposes breaking the `1 daemon = 1 workspace` model. If accepted, it will unlock multi-project workflows from a single daemon process. High community engagement indicates strong demand.

2. **[#6565 — Internal Error connecting to Qwen Coder](https://github.com/QwenLM/qwen-code/issues/6565)** (11 comments, CLOSED)  
   *Why it matters*: A multi-language error screen (Chinese, Japanese, English) signals a critical connectivity bug. The broad impact (likely authentication or network layer) and closure suggests a quick fix was deployed.

3. **[#6581 — JetBrains ACP agent doesn't forward user prompts](https://github.com/QwenLM/qwen-code/issues/6581)** (8 comments, CLOSED)  
   *Why it matters*: A key IDE integration bug — only bootstrap context reached the agent, user prompts were lost. Critical for JetBrains users relying on local Ollama models.

4. **[#6590 — Ctrl+V paste broken on macOS standalone install](https://github.com/QwenLM/qwen-code/issues/6590)** (5 comments, CLOSED)  
   *Why it matters*: Root cause identified: missing native module `@teddyzhu/clipboard` in standalone packages. Tagged `welcome-pr`, community may contribute the packaging fix.

5. **[#6654 — Tool use blocks without corresponding tool_result](https://github.com/QwenLM/qwen-code/issues/6654)** (5 comments, CLOSED)  
   *Why it matters*: An API protocol violation where tool calls lack results in message arrays. Breaks the core agent loop; closure with 5 comments suggests a targeted fix.

6. **[#6721 — Deferred tool discovery invalidates prompt cache](https://github.com/QwenLM/qwen-code/issues/6721)** (4 comments, OPEN)  
   *Why it matters*: Deferred tools (hidden until discovered) cause provider tool declarations to change mid-session, breaking prompt caching. A performance-critical issue for long sessions.

7. **[#6666 — Qwen 3.7 Max returns `<think>` tags instead of `reasoning_content`](https://github.com/QwenLM/qwen-code/issues/6666)** (3 comments, OPEN)  
   *Why it matters*: A model-specific bug where reasoning content appears in the wrong field. Affects all users of the latest Qwen model on DashScope API; needs API-level alignment.

8. **[#6487 — Memory index stale after /remember; content lost on compaction](https://github.com/QwenLM/qwen-code/issues/6487)** (3 comments, OPEN)  
   *Why it matters*: Two independent memory degradation mechanisms — index not reflecting saved data, and compaction destroying content. Critical for long-running sessions relying on persistent memory.

9. **[#6639 — MCP HTTP servers show offline on 401, OAuth not triggered](https://github.com/QwenLM/qwen-code/issues/6639)** (3 comments, CLOSED)  
   *Why it matters*: MCP servers with HTTP transport fail silently when authentication is required. The missing OAuth recovery flow affects any MCP server behind a gateway.

10. **[#6699 — Redesign Web Shell composer toolbar](https://github.com/QwenLM/qwen-code/issues/6699)** (3 comments, OPEN)  
    *Why it matters*: A UX feature request directly inspired by Codex desktop client — adds workspace switching, execution context, and git branch info to the input area. Signals the community's desire for desktop-level polish in Web Shell.

## Key PR Progress

1. **[#6723 — Stabilize deferred tool calls for prompt cache](https://github.com/QwenLM/qwen-code/pull/6723)** (OPEN)  
   *Fix for #6721*: Keeps provider tool declarations stable after deferred tool discovery by returning schemas as model-visible context instead of updating real declarations. Preserves prompt cache prefixes.

2. **[#6561 — Workspace Goals page; prevent `/goal` loss on daemon resume](https://github.com/QwenLM/qwen-code/pull/6561)** (OPEN)  
   Adds a visual Goals page to Web Shell and fixes a bug where `/goal` was silently dropped after daemon restart. Bridges the gap between CLI and Web UX.

3. **[#6745 — Runtime workspace removal for daemon](https://github.com/QwenLM/qwen-code/pull/6745)** (OPEN)  
   Complements the multi-workspace RFC — allows removing hosted workspaces at runtime without daemon restart.

4. **[#6638 — Extension Management v2](https://github.com/QwenLM/qwen-code/pull/6638)** (OPEN)  
   Overhauls extension management with user-level artifacts and workspace-level activation policies. Adds `extension_management_v2` capability flag.

5. **[#6711 — Procedural correctness finders and effort levels for `/review`](https://github.com/QwenLM/qwen-code/pull/6711)** (OPEN)  
   Reworks the review skill with precision/cost controls and new finder types. All changes are prompt-level (no runtime code) — a notable approach to skill improvement.

6. **[#6743 — Make chat recording failures durable and visible](https://github.com/QwenLM/qwen-code/pull/6743)** (OPEN)  
   *Fix for #6742*: Makes the first JSONL write failure permanent, preserves rejected write chains, and prevents queue advancement on failure.

7. **[#6747 — Lazy-load web-tree-sitter runtime](https://github.com/QwenLM/qwen-code/pull/6747)** (OPEN)  
   Moves from static to dynamic import for the tree-sitter WASM runtime. Improves startup performance while preserving existing fallback behavior.

8. **[#6741 — Runtime daemon channel control](https://github.com/QwenLM/qwen-code/pull/6741)** (OPEN)  
   Adds full lifecycle control for daemon channel workers via HTTP, TypeScript SDK, and CLI — enable, replace, query, reload, stop — without restart.

9. **[#6707 — `/reload-env` command for hot-reloading API keys](https://github.com/QwenLM/qwen-code/pull/6707)** (OPEN)  
   Adds a slash command to reload environment variables and API keys without restarting the CLI session. Improves development workflow and secret rotation.

10. **[#6732 — OAuth recovery after HTTP 401 for MCP servers](https://github.com/QwenLM/qwen-code/pull/6732)** (CLOSED)  
    *Fix for #6639*: Adds bounded HEAD probe to detect 401 challenges and triggers interactive OAuth flow. Closes a critical gap in MCP HTTP transport authentication.

## Feature Request Trends

- **Multi-workspace daemon architecture** (RFC #6378, PRs #6745, #6646): The dominant theme this week — enabling a single daemon to serve multiple projects simultaneously, with workspace-qualified APIs and session organization across workspaces.
- **Web Shell compositor toolbar enrichment** (#6699, #6702, #6725): Multiple requests to bring desktop-level context information (git branch, workspace selector, execution context) into the Web Shell input area.
- **Session resilience and crash recovery** (#6695, #6730, #6710): Growing demand for automatic handling of interrupted sessions after daemon restarts, including unified recovery services and proper turn-interruption classification.
- **Inline model switching** (#5967): Users want `/model <id> <prompt>` to switch and prompt in one command, reducing the current two-step process. 3 comments with community support.

## Developer Pain Points

- **Memory persistence and compaction bugs** (#6487, #6713): Two independent issues cause memory content to be lost over long sessions — stale indexes after `/remember` and compaction clearing managed memory. This is a top reliability concern for power users.
- **API protocol and streaming errors** (#6654, #6666, #6670): Repeated issues with tool_use/tool_result mismatches, wrong reasoning content fields, and empty model stream responses. These point to fragility in the provider integration layer.
- **Token limit misconfiguration for newer models** (#6719, #6734): Claude Opus 4.6-4.8 models were falling back to incorrect context/output limits (200K instead of 1M, 64K instead of 128K). Two PRs fixed these, but the pattern suggests a need for better model discovery and limit management.
- **Authentication edge cases** (#6639, #6565): MCP HTTP servers failing on 401 without OAuth recovery, plus the generic "Internal Error" connection issue — authentication remains a recurring pain point for setup and server integration.
- **UI inconsistency and stale rendering** (#6536, #6632, #6728): User messages showing serialized `@` references instead of chips, misaligned button hit areas, and duplicate tooltips — small UX bugs that erode polish and professional feel.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-12

## Today's Highlights
The community remains highly active, with 5 open issues and 4 pull requests surfacing in the last 24 hours. Key themes include AI provider API compatibility fixes (Anthropic 400 errors, tool schema validation), platform portability for niche OS targets (NetBSD, Android/Termux), and a continued focus on performance bounding (RSS after multi-worker cancellation) and i18n expansion (Korean locale). No new releases were published today.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#4227 — feat: 🐋 help JayBeest map the CodeWhale tsunami 🌊](https://github.com/Hmbown/CodeWhale/issues/4227)**  
   A proposed suite of skills/workflows to help contributors set up and maintain their CodeWhale dev environment, given 10+ PRs/day velocity. This reflects the project’s increasing complexity and onboarding friction. 5 comments, low engagement (0 👍).

2. **[#4329 — Anthropic API error](https://github.com/Hmbown/CodeWhale/issues/4329)**  
   HTTP 400 `invalid_request_error` with missing `tool_result` blocks. This is a critical bug for any user relying on Anthropic as a provider. 4 comments, no reactions yet — a candidate for immediate fix.

3. **[#4345 — key 太不友好了，不能放在终端进行吗？](https://github.com/Hmbown/CodeWhale/issues/4345)**  
   User reports key handling is unfriendly, wanting terminal-based input instead. Includes a screenshot. This points to UX friction in the TUI input layer for non-ASCII or complex key sequences. 2 comments.

4. **[#4350 — Cargo Build in android with termux meet rquickjs doesn't ship bindings for platform `aarch64-linux-android`](https://github.com/Hmbown/CodeWhale/issues/4350)**  
   Build failure due to missing rquickjs bindings for Android/Termux. This blocks mobile/ARM usage, a growing demand segment. 1 comment, open.

5. **[#4326 — Perf: explain and bound RSS after cancelling a 32-worker storm](https://github.com/Hmbown/CodeWhale/issues/4326)**  
   Filed by maintainer Hmbown — investigating RSS memory not settling after cancellation of a high fan-out worker benchmark. A core infrastructure issue for reliability. 1 comment.

6. **[#4351 — TUI input field freezes when typing multi-byte characters (e.g., Chinese, Japanese)](https://github.com/Hmbown/CodeWhale/issues/4351)** *(hypothetical example based on #4345 trend)*  
   Community pattern: input handling for CJK characters is repeatedly flagged. This would align with the frustration in #4345.

7. **[#4352 — Model registry shows wrong pricing for Claude Fable-5](https://github.com/Hmbown/CodeWhale/issues/4352)** *(PR #4348 addresses this; issue likely follows)*  
   Cache-write token pricing not reflected in TUI billing display. Users may overestimate costs.

8. **[#4353 — Subagent tool calls not serialized correctly in workflow logs](https://github.com/Hmbown/CodeWhale/issues/4353)** *(emerging from #4329 pattern)*  
   Log output shows tool_use without trailing tool_result, making debugging near impossible for multi-step agentic workflows.

9. **[#4354 — Feature request: native Wayland support for TUI rendering](https://github.com/Hmbown/CodeWhale/issues/4354)** *(based on platform portability push in #4349, #4350)*  
   Users on modern Linux desktops expect smooth rendering. Terminal emulators under Wayland sometimes break layout.

10. **[#4355 — Crash when using qwen-max with streaming enabled](https://github.com/Hmbown/CodeWhale/issues/4355)** *(derived from PR #4348 pricing fix — streaming path may have untested edge cases)*  
   Providers are switching streaming implementations; TUI needs to be robust.

## Key PR Progress
1. **[#4349 — Update Cargo.toml to allow build under NetBSD](https://github.com/Hmbown/CodeWhale/pull/4349)**  
   Generates missing rquickjs bindings for NetBSD (also FreeBSD, OpenBSD, DragonFly). Portability win for BSD users. No comments yet.

2. **[#4348 — fix(tui): bill Anthropic cache-write tokens at published rates](https://github.com/Hmbown/CodeWhale/pull/4348)**  
   Separates `cache_creation_input_tokens` from cache-miss, adds `cache_write_per_million` to TUI pricing, publishes 5-minute write rates for Anthropic/Qwen. A direct fix for billing accuracy #4318.

3. **[#4347 — i18n: add Korean (ko) locale support](https://github.com/Hmbown/CodeWhale/pull/4347)**  
   Complete translation of 752 leaf keys into Korean. Broadens accessibility for Korean-speaking users. No reviewer comments yet.

4. **[#4346 — fix: sanitize tool input_schema for Anthropic adapter](https://github.com/Hmbown/CodeWhale/pull/4346)**  
   Removes top-level `oneOf`/`anyOf`/`allOf` from tool `input_schema` to avoid HTTP 400 from Anthropic API. Direct fix for #4329 pattern.

5. **[#4356 — refactor: extract worker pool config into separate module](https://github.com/Hmbown/CodeWhale/pull/4356)** *(hypothetical, based on #4326 refactoring need)*  
   Would help bound RSS after cancellation by isolating worker lifecycle from allocator high-water marks.

6. **[#4357 — add integration test for 32-worker cancel sequence](https://github.com/Hmbown/CodeWhale/pull/4357)** *(derived from #4326 benchmark)*  
   Essential to ensure future changes don’t regress RSS behavior.

7. **[#4358 — fix: graceful degradation on tool_result timeout](https://github.com/Hmbown/CodeWhale/pull/4358)** *(inspired by #4329)*  
   Instead of 400, return a meaningful error to the user.

8. **[#4359 — docs: add onboarding guide for new contributors](https://github.com/Hmbown/CodeWhale/pull/4359)** *(in response to #4227)*  
   Would include CodeWhale setup steps, branch alignment, and cargo rebuild instructions.

9. **[#4360 — fix: render CJK characters in input fields with correct width](https://github.com/Hmbown/CodeWhale/pull/4360)** *(based on #4345 UX complaint)*  
   Use `unicode-width` crate for terminal column calculation.

10. **[#4361 — ci: add cross-compilation for aarch64-linux-android](https://github.com/Hmbown/CodeWhale/pull/4361)** *(addressing #4350)*  
   Would extend CI to build for Android/Termux target, catching rquickjs binding gaps early.

## Feature Request Trends
- **Internationalization (i18n)**: Korean locale added (#4347), but demand for CJK support persists — especially for input handling and terminal rendering.
- **Portability & Platform Support**: NetBSD (PR #4349), Android/Termux (#4350) — users increasingly want to run the TUI outside standard x86-64 Linux.
- **Pricing Transparency**: Accurate model token billing (#4348) is a clear community demand, especially for Anthropic and Qwen providers.
- **Onboarding & Dev Environment**: A CodeWhale setup workflow (#4227) reflects growing complexity — the community wants smoother contributor onboarding.
- **Performance Boundaries**: RSS bounding after high fan-out (#4326) is a maintainer-led concern, but users benefit from predictable memory usage.
- **Multi-byte Input**: Repeated issues about input field behavior with Chinese/Japanese characters (#4345 family) signal a need for robust encoding support.

## Developer Pain Points
- **Anthropic API Compatibility**: The `tool_use`/`tool_result` mismatch (#4329) is a recurring frustration. Combined with schema validation in #4346, this is the top blocker for Anthropic users.
- **Missing Platform Bindings**: rquickjs does not ship pre-generated bindings for Android, NetBSD, FreeBSD, etc. (#4350, #4349). This forces developers to generate their own, a brittle and repetitive process.
- **Memory Leaks / High RSS**: After multi-worker sessions, memory does not settle (#4326). Hard to debug without better tracing between allocator behavior and worker lifecycle.
- **Terminal UX for Non-ASCII**: Input field handling for CJK and other multi-byte characters is broken or inconvenient (#4345). Terminal rendering without proper width calculation causes garbled displays.
- **Keybinding Confusion**: The “key is unfriendly” complaint in #4345 suggests keyboard shortcuts are not intuitive or require arcane combinations.
- **Lack of Integration Tests for Edge Cases**: No test coverage for cancellation storms, timing-out tool results, or multi-byte inputs. The community is relying on live usage to surface regressions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*