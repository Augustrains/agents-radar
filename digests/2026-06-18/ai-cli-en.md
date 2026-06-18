# AI CLI Tools Community Digest 2026-06-18

> Generated: 2026-06-18 02:14 UTC | Tools covered: 9

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

Here is the cross-tool comparison report based on the June 18, 2026 community digest summaries.

---

## Cross-Tool Comparison Report: AI CLI Developer Tools (2026-06-18)

### 1. Ecosystem Overview

The AI CLI developer tools ecosystem is in a state of rapid maturation, characterized by intense competition and a shared focus on agentic workflows. While core functionalities like code generation and bash automation are now table stakes, the community is demanding robust multi-agent orchestration, cross-platform reliability, and transparent performance metrics. A clear divergence is emerging between tools focused on single-agent depth (Claude Code, Copilot) versus those pushing toward distributed, multi-session architectures (OpenCode, CodeWhale). Across the board, developer pain points highlight a consistent tension between the desire for autonomous agents and the need for predictable, secure, and observable behavior, with regressions and silent failures being the most critical trust-eroding issues.

### 2. Activity Comparison

| Tool | Hot Issues (Active) | Key PRs (Active) | Release Status (Last 24h) |
| :--- | :--- | :--- | :--- |
| **Claude Code** | 10 | 5 | **Released** v2.1.181 |
| **OpenAI Codex** | 10 | 10 | **Released** 3 Alpha Builds (v0.141.0-a.5-7) |
| **Gemini CLI** | 10 | 10 | **Released** v0.47.0 & v0.48.0-preview.0 |
| **GitHub Copilot CLI** | 10 | 0 | **No Release** (Post-outage recovery) |
| **Kimi Code CLI** | 2 | 0 | **No Release** (Quiet period) |
| **OpenCode** | 10 | 10 | **Released** v1.17.8 |
| **Pi** | 10 | 10 | **No Release** (Active dev cycle) |
| **Qwen Code** | 10 | 10 | **Released** v0.18.3 & Nightly |
| **CodeWhale** | 10 | 10 | **No Release** (Active dev cycle for v0.9.0) |

### 3. Shared Feature Directions

Several feature requirements appear consistently across multiple tool communities:

- **Multi-Agent Orchestration & Inter-Session Communication**
    - **Tools:** Claude Code, OpenCode, Gemini CLI, CodeWhale
    - **Need:** The ability to coordinate multiple agents in parallel, either across machines (Claude), in isolated workspaces (OpenCode), or with human oversight (CodeWhale). This goes beyond simple sub-agent spawning to include native protocols and shared state.

- **Dynamic Model & Task Routing**
    - **Tools:** OpenCode, Qwen Code, CodeWhale
    - **Need:** Auto-selecting a model based on the task's complexity (e.g., cheap model for grep, expensive model for reasoning). This is a direct response to controlling costs and latency.

- **Enhanced Tool Whitelisting & Sandboxing**
    - **Tools:** GitHub Copilot CLI, OpenCode, Pi
    - **Need:** A granular, safe alternative to `/allow-all` that permits read-only operations (grep, cat) without approval, while still blocking destructive commands. This is the most significant security gap.

- **Non-Interrupting, Queued Interaction**
    - **Tools:** Claude Code, Copilot CLI
    - **Need:** The ability to queue follow-up thoughts or commands without interrupting an active agent task. This prevents context derailment and improves workflow fluidity.

- **Rate-Limit & Token-Usage Transparency**
    - **Tools:** OpenAI Codex, OpenCode, Qwen Code
    - **Need:** A visible, accurate, and real-time display of token consumption, cost, and rate-limit status. The lack of this is a top frustration, especially with complex billing models.

- **Enterprise Environment Compatibility**
    - **Tools:** Kimi Code CLI, GitHub Copilot CLI
    - **Need:** Support for corporate network constraints, including SSL inspection proxies and enterprise-managed custom models. This is a blocker for professional adoption.

### 4. Differentiation Analysis

The tools are diverging in their core philosophies and target users:

- **Claude Code** is deepening its **remote control and agent-team** capabilities, targeting power users who want a mobile-to-desktop workflow and complex, collaborative agent structures. Its focus is on advanced team-level orchestration.
- **OpenCode** is pivoting toward a **platform model** with **native VS Code integration** and a strong emphasis on **auto-discovery** of providers and local LAN servers. It aims to be a universal, pluggable client for any backend.
- **CodeWhale** (formerly DeepSeek-TUI) is making the most radical bet on a **chat-native, workroom architecture** (v0.9.0). It aims to transcend the terminal to become a shareable, threaded, mobile-accessible workspace, in direct competition with web-based IDEs.
- **Pi** is focusing on **provider extensibility** and **infrastructure reliability** (fixing shrinkwrap, improving error handling). It targets developers who experiment with many model providers and need a clean, modular architecture.
- **Gemini CLI** and **Qwen Code** are both focusing on **hardening their core agent subsystems**, fixing hangs, silent failures, and tool overload errors common to rapidly evolving autonomous modes.
- **GitHub Copilot CLI** is currently in a **defensive posture**, recovering from a major outage and facing foundational issues like tool whitelisting and plugin lifecycle management that limit its maturity.

### 5. Community Momentum & Maturity

- **High Activity & Rapid Iteration:** **OpenCode** and **CodeWhale** are the most active, with a high volume of daily PRs and feature requests. This suggests a large, engaged community and a fast-moving development cycle. CodeWhale's ambitious v0.9.0 vision is generating significant buzz.
- **Active Stabilization & Hardening:** **Gemini CLI**, **Pi**, and **Qwen Code** are in a phase of active bug fixing and infrastructure refactoring. While innovation is slower, the community is actively contributing to reliability, which is a sign of maturity.
- **Focused on Core Pain Points:** **Claude Code** continues to have a highly vocal and sophisticated user base pushing for complex architectural changes (multi-session, remote reliability). The **OpenAI Codex** community is focused on a single, critical pain point: rate-limit and billing transparency.
- **Low Momentum / Defensive:** **GitHub Copilot CLI** is recovering from a community-trust event (the outage) and has had zero PR activity. **Kimi Code CLI** had a very quiet day, which may indicate a consolidation phase or a smaller community.

### 6. Trend Signals

- **The Era of the "Agent Platform" Has Arrived:** The biggest trend is the shift from a single-agent assistant to a platform for orchestrating multiple, specialized agents. The demand for inter-session communication, machine-to-machine protocols, and chat-native workrooms (CodeWhale, Claude Code) signals that users want AI to be a persistent, collaborative member of a team, not just a chatbot.
- **Security and Trust Are the New Battlegrounds:** After the initial rush of features, the community is now laser-focused on security and predictability. The demand for tool sandboxing, whitelisting, and content exclusion reflects a need for safe autonomy. Silent failures, agent scope creep, and ignored configuration are the fastest ways for a tool to lose trust.
- **The "Metering Crisis" is Boiling Over:** The combination of broken rate-limit buttons, opaque token counts, and unpredictable latency (especially GPT models) is a major source of community frustration. Tools that solve **cost transparency and predictable consumption** will have a significant competitive advantage.
- **Local and Hybrid Workflows are a Major Force:** Despite the cloud-native nature of these tools, there is a very strong and vocal community segment invested in **local LLMs** (Ollama, vLLM) and **LAN-based providers**. Tools that first-class citizen this workflow (OpenCode) are capturing significant developer mindshare.
- **Cross-Platform Parity is a Persistent Problem:** The gap between macOS, Windows, and Linux is a constant source of bugs and feature regressions across all tools. Developers on non-macOS platforms are increasingly vocal about feeling like second-class citizens, which is a long-term adoption risk.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-06-18 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Pull Requests represent the most-discussed Skill proposals in the community, ranked by comment volume and cross-referencing activity.

### #514 — Document Typography Skill (Open)
**Skill:** Enforces typographic quality control on AI-generated documents — orphan word wrap prevention, widow paragraph elimination, and numbering alignment fixes.  
**Discussion:** Community members confirmed these issues plague *every* document Claude generates, yet no existing skill addressed them. The thread debates whether typography rules should be bundled into a single skill vs. distributed across document-type skills.  
**Status:** Open, active discussion  
🔗 [github.com/anthropics/skills/pull/514](https://github.com/anthropics/skills/pull/514)

### #486 — ODT Skill (Open)
**Skill:** Full OpenDocument Format (.odt, .ods) creation, template filling, and conversion to HTML. Triggers on mentions of "ODT," "LibreOffice," or "OpenDocument."  
**Discussion:** High interest from enterprise users who rely on LibreOffice/OpenOffice for document workflows. Reviewers requested clarification on template variable syntax and schema validation approach.  
**Status:** Open, undergoing revision  
🔗 [github.com/anthropics/skills/pull/486](https://github.com/anthropics/skills/pull/486)

### #210 — Frontend-Design Skill Improvement (Open)
**Skill:** Revises the existing `frontend-design` skill for clarity, actionability, and internal coherence — ensuring every instruction is executable within a single conversation.  
**Discussion:** The thread surfaced broader concerns about skill maintainability: several skills contain conflicting guidance when loaded simultaneously. The PR proposes a "single-responsibility" convention for skill authors.  
**Status:** Open, discussed as a model for skill refactoring  
🔗 [github.com/anthropics/skills/pull/210](https://github.com/anthropics/skills/pull/210)

### #83 — Meta-Skills: Quality & Security Analyzers (Open)
**Skill:** Two meta-skills for skill authors — `skill-quality-analyzer` evaluates Structure, Documentation, Examples, Resources, and Prompts (5 dimensions, weighted scoring), while `skill-security-analyzer` checks for injection vectors and dangerous tool usage.  
**Discussion:** High-value for the skill-creation community; reviewers suggested integrating these into CI checks rather than leaving them as standalone skills.  
**Status:** Open, awaiting CI integration proposal  
🔗 [github.com/anthropics/skills/pull/83](https://github.com/anthropics/skills/pull/83)

### #181 — SAP RPT-1-OSS Predictor (Open)
**Skill:** Wraps SAP's open-source tabular foundation model (Apache 2.0, released at SAP TechEd 2025) for predictive analytics on SAP business data.  
**Discussion:** First enterprise-ERP-specific skill in the repository. Generated interest from SAP ecosystem developers, but also raised questions about data privacy when passing SAP data through Claude.  
**Status:** Open, privacy discussion ongoing  
🔗 [github.com/anthropics/skills/pull/181](https://github.com/anthropics/skills/pull/181)

### #723 — Testing Patterns Skill (Open)
**Skill:** Comprehensive testing methodology skill covering unit testing (AAA pattern), React component testing (Testing Library), integration testing, and the "Testing Trophy" philosophy.  
**Discussion:** Broad support — community notes this fills a significant gap. Some concern about over-specificity to React/testing-library, with requests for Vue/Angular equivalents.  
**Status:** Open, positive reception  
🔗 [github.com/anthropics/skills/pull/723](https://github.com/anthropics/skills/pull/723)

### #154 — Shodh-Memory Skill (Open)
**Skill:** Persistent memory system for AI agents — maintains context across conversations via `proactive_context` calls, structured memory organization, and retrieval.  
**Discussion:** Technically ambitious; reviewers debated whether memory persistence belongs client-side vs. in skill logic. A subset of the conversation explored this as a foundation for "agentic" skills.  
**Status:** Open, architectural discussion active  
🔗 [github.com/anthropics/skills/pull/154](https://github.com/anthropics/skills/pull/154)

---

## 2. Community Demand Trends

From Issue activity, the community's most-anticipated new Skill directions are:

**a) Organizational Skill Sharing (#228)** — 14 comments, 7 👍  
Users want org-wide skill libraries and direct sharing links. The current download-and-upload workflow is a major friction point for teams.  
🔗 [github.com/anthropics/skills/issues/228](https://github.com/anthropics/skills/issues/228)

**b) Skill-Creator Tooling Reliability (#556, #1169, #1061)** — 18 total comments  
A cluster of issues reports that `run_eval.py` and its optimization loop produce 0% recall on every query — effectively breaking the skill description optimization workflow. This is the single largest blocker for skill authors.  
🔗 [github.com/anthropics/skills/issues/556](https://github.com/anthropics/skills/issues/556) | [#1169](https://github.com/anthropics/skills/issues/1169) | [#1061](https://github.com/anthropics/skills/issues/1061)

**c) Agent Governance & Safety (#412)** — 6 comments, closed as proposal  
A proposal for governance patterns — policy enforcement, threat detection, trust scoring, audit trails. The closure without implementation suggests the community wants this but the skill format may not yet support it.  
🔗 [github.com/anthropics/skills/issues/412](https://github.com/anthropics/skills/issues/412)

**d) Namespace Trust & Security (#492)** — 7 comments  
Community skills impersonating official Anthropic skills under the `anthropic/` namespace. This trust-boundary vulnerability has active discussion on mitigation strategies.  
🔗 [github.com/anthropics/skills/issues/492](https://github.com/anthropics/skills/issues/492)

**e) Multi-File Reference Bundling (#1220)** — 2 comments, recent  
Skills split across multiple reference files (`refs/`) only deliver `SKILL.md` into the agent context. Users need a bundling mechanism for reference dependencies.  
🔗 [github.com/anthropics/skills/issues/1220](https://github.com/anthropics/skills/issues/1220)

---

## 3. High-Potential Pending Skills

These actively-discussed PRs remain open and show momentum toward merge:

| PR | Skill | Last Update | Key Signal |
|----|-------|-------------|------------|
| #1298 | `skill-creator` eval fix (0% recall, Windows streams) | 2026-06-11 | Unblocks entire skill optimization pipeline |
| #1099 | `run_eval.py` Windows pipe crash fix | 2026-05-24 | Resolves #1061 sub-issues |
| #1050 | Windows subprocess + encoding fix | 2026-05-24 | Complements #1099 |
| #538 | PDF skill case-sensitive file references | 2026-04-29 | Blocks PDF skill on case-sensitive OS |
| #539 | YAML description quoting validation | 2026-04-16 | Prevents silent parsing errors |
| #541 | DOCX tracked change ID collision fix | 2026-04-16 | Fixes document corruption bug |
| #568 | ServiceNow platform skill | 2026-04-23 | Broad enterprise demand |
| #444 | AURELION cognitive framework suite (4 skills) | 2026-05-06 | Large, multi-skill contribution |

**Notable:** PRs #1298, #1099, and #1050 collectively address the same root cause — the skill-creator pipeline is broken on Windows, and these fixes are interdependent.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for skill-creation tooling reliability and infrastructure hardening** — specifically fixing the broken `run_eval.py` optimization loop (0% recall bug), adding YAML validation, resolving Windows compatibility gaps, and enabling multi-file reference bundling — reflecting a community that has moved beyond authoring individual skills to building a professional-grade ecosystem around skill development, quality assurance, and enterprise deployment.

---

# Claude Code Community Digest — 2026-06-18

## 1. Today's Highlights
Version **2.1.181** ships today with an inline `/config key=value` syntax that allows developers to toggle settings like `thinking` directly from the prompt — a quality-of-life win for power users. Meanwhile, community heat remains focused on **remote control reliability** (Issue #34255, 50 comments) and a popular **message queue mode** proposal (Issue #50246, 99 👍) that would let users queue follow-ups without interrupting active tasks. Agent-team and multi-session workflows continue to dominate feature requests, though a new crop of Linux and Windows bugs suggests platform-specific polish is lagging.

## 2. Releases
**[v2.1.181](https://github.com/anthropics/claude-code/releases/tag/v2.1.181)** — released today.
- **`/config key=value` syntax** — set any setting from the prompt in interactive, `-p`, and Remote Control modes (e.g., `/config thinking=false`)
- **`sandbox.allowAppleEvents` opt-in** — lets sandboxed commands send Apple Events on macOS
- **`CLAUDE_CLIENT_P`** — new environment variable (truncated in source data; likely a client-path or proxy setting)

No other versions were released in the last 24 hours.

## 3. Hot Issues (10 noteworthy)

1. **[#34255 — Remote Control: automatic reconnection silently drops](https://github.com/anthropics/claude-code/issues/34255)**  
   50 comments, 90 👍. **Top-voted bug.** Connections fail with no recovery mechanism. Affects macOS and iOS, blocks mobile-to-desktop workflows at scale.

2. **[#50246 — Message queue mode: queue messages instead of interrupting](https://github.com/anthropics/claude-code/issues/50246)**  
   31 comments, 99 👍. **Most-upvoted open feature.** Users want to queue follow-up thoughts while Claude is mid-task, avoiding costly context derailment.

3. **[#24798 — Inter-session communication for multi-Claude workflows](https://github.com/anthropics/claude-code/issues/24798)**  
   35 comments, 16 👍. Parallel sessions cannot coordinate. Users hacking workarounds with shared files; native IPC protocol requested.

4. **[#29214 — Remote Control: mobile app ignores `--dangerously-skip-permissions`](https://github.com/anthropics/claude-code/issues/29214)**  
   30 comments, 76 👍. Mobile interface shows permission prompts despite CLI flags. Undermines trust in permission-modes parity.

5. **[#44243 — Support multiple Slack workspaces in built-in connector](https://github.com/anthropics/claude-code/issues/44243)**  
   27 comments, 57 👍. Consultants and multi-org users blocked: only one Slack workspace per account.

6. **[#28300 — Multi-agent collaboration across machines (Agent-to-Agent)](https://github.com/anthropics/claude-code/issues/28300)**  
   26 comments, 0 👍 (likely miscounted). Distributed agent teams need a cross-machine protocol — a longer-term architectural ask.

7. **[#23669 — Agent Teams: per-teammate working directories and configs](https://github.com/anthropics/claude-code/issues/23669)**  
   24 comments, 28 👍. Multi-repo projects require each team member to have its own workspace, CLAUDE.md, and MCP configs.

8. **[#25128 — Drag and drop broken in VS Code extension chat panel](https://github.com/anthropics/claude-code/issues/25128)**  
   20 comments, 40 👍. Regression from v2.1.6. Terminal mode works; VS Code panel does not. Lingering for months.

9. **[#61993 — Sub-agents cannot spawn sub-agents on Windows](https://github.com/anthropics/claude-code/issues/61993)**  
   18 comments. `Task`/`Agent` primitives not exposed in nested contexts. Blocks recursive decomposition patterns on Windows.

10. **[#68721 — Native team-management tools missing in v2.1.178 (Linux regression)](https://github.com/anthropics/claude-code/issues/68721)**  
    6 comments, 4 👍. `TeamCreate`/`TeamDelete` tools disappeared between 2.1.177→2.1.178. Users blocked from managing teams.

## 4. Key PR Progress

1. **[#69226 — Update frontend-design skill](https://github.com/anthropics/claude-code/pull/69226)**  
   Bumps plugin version to 1.1.0. Installed copies auto-update. New improvements to the frontend-design skill.

2. **[#19867 — Fix code-review: allow re-reviews on new commits](https://github.com/anthropics/claude-code/pull/19867)**  
   Smarter skip logic: skips review only if no new commits since Claude's last comment. `--force` flag bypasses check. Solves a common CI grievance.

3. **[#33443 — Update Dockerfile to use native installer](https://github.com/anthropics/claude-code/pull/33443)**  
   Moves from deprecated `npm install` to native installer. Node 24.14 base. Modernizes dev-container setup.

4. **[#60427 — docs: standardize GitHub capitalization in README](https://github.com/anthropics/claude-code/pull/60427)** *(closed)*  
   Minor but signal of documentation quality attention.

5. **[#60732 — Polish plugins README wording](https://github.com/anthropics/claude-code/pull/60732)** *(closed)*  
   Tiny documentation improvement — slightly more natural phrasing in plugin ecosystem description.

*(Only 5 PRs were updated in the last 24h; the remainder of the top 10 slots are unfilled due to low activity.)*

## 5. Feature Request Trends

- **Message Queuing & Non-Interrupting Interaction** — #50246 (99 👍) signals strong demand for queuing follow-ups instead of interrupting active agent tasks. Related: #24798 (inter-session messaging).
- **Multi-Agent & Multi-Machine Orchestration** — #28300 (agent-to-agent protocol), #23669 (per-teammate configs), and #67485 (background subagent visibility) all push toward richer team and distributed agent primitives.
- **Multi-Workspace Integrations** — #44243 (multiple Slack workspaces) is the leading example; users want connectors to handle multiple auth contexts.
- **Cross-Platform Parity** — Issues around permission modes (#29214), model switching (#48973), and image paste (#69234) all highlight platform inconsistency between macOS, Windows, and Linux.

## 6. Developer Pain Points

- **Remote Control reliability** — #34255 (automatic reconnection drops) and #29214 (permission override ignored) together make the Remote Control feature unreliable for daily use. High comment/upvote counts reflect real workflow disruption.
- **Agent nesting limitations** — #61993 (sub-agents can't spawn on Windows) and #68336 (replay storms in agent teams) expose fragility in the agent hierarchy. Developers wanting recursive decomposition hit hard walls.
- **Silent failures & no visibility** — #67485 (background subagent activity invisible), #69062 (tasks stuck in "spare" state), and #68931 (idle CPU spin on macOS) erode trust: the tool appears idle or broken while work may or may not be happening.
- **Regressions in critical paths** — #68721 (missing team tools in v2.1.178) and #48973 (model switching broken after redesign) suggest insufficient regression testing for agent-team and Cowork features.
- **VS Code extension environment pollution** — #69227 (extension sets `NoDefaultCurrentDirectoryInExePath=1` globally) is a subtle but serious bug affecting all other extensions on Windows.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-18

## Today's Highlights
Three pre-release Rust alpha builds (0.141.0-alpha.5–7) shipped overnight, suggesting active iteration on the CLI/packaging layer. The community is increasingly vocal about rate-limit mechanics, with multiple reports (#28823, #28811, #28740, #28380) describing broken reset buttons, misapplied banked resets, and faster-than-expected consumption of the 5-hour meter. The top-voted issue (#23794, 👍168) remains the missing context/token usage indicator — closed but still generating commentary.

---

## Releases
- **rust-v0.141.0-alpha.5**, **rust-v0.141.0-alpha.6**, **rust-v0.141.0-alpha.7** — published consecutively; no individual changelog details. Likely hotfix iteration on the Rust-based Codex CLI or core library.

---

## Hot Issues

1. **#23794 – Codex Desktop no longer shows visible context/token usage indicator**  
   *Closed, 170 comments, 👍168*  
   The most-upvoted open problem. Users across platforms report the token/cost indicator vanished after an update. Closed, but the volume of engagement signals it remains unresolved in users’ perception.  
   [View Issue](https://github.com/openai/codex/issues/23794)

2. **#25670 – Authentication for Codex has literally broken**  
   *Open, 33 comments, 👍19*  
   Multi-layer MFA (passkey + phone + authenticator app) loops back to phone-number entry, likely due to stale phone metadata. Affects Pro/Business users onboarding with old accounts.  
   [View Issue](https://github.com/openai/codex/issues/25670)

3. **#25719 – Codex Desktop triggers syspolicyd/trustd CPU/memory runaway on macOS**  
   *Open, 31 comments, 👍39*  
   Persistent kernel-level process leaks. Desktop consumes resources even when idle. High concern for laptop users who rely on battery life.  
   [View Issue](https://github.com/openai/codex/issues/25719)

4. **#25178 – Windows Computer Use screenshot fails with SetIsBorderRequired error**  
   *Open, 11 comments, 👍4*  
   Blocks screenshot-based UI automation on Win10 22H2. Active investigation by author and maintainers.  
   [View Issue](https://github.com/openai/codex/issues/25178)

5. **#25921 – Crashpad pending dumps grow without limit (+5GB/day)**  
   *Open, 9 comments, 👍2*  
   macOS Desktop generates 50k+ crash dump files per day. Serious storage and performance regression.  
   [View Issue](https://github.com/openai/codex/issues/25921)

6. **#28823 – 5-hour usage meter consumes much faster than historical usage**  
   *Open, 4 comments, 👍0*  
   Regression in quota accounting. Users report 2–3x faster consumption for comparable sessions. Possibly related to model routing or token counting changes.  
   [View Issue](https://github.com/openai/codex/issues/28823)

7. **#28811 – Public rate-limit reset applied immediately instead of banked**  
   *Open, 4 comments, 👍3*  
   Contradicts OpenAI’s reset-banking messaging. Users lost a full reset cycle.  
   [View Issue](https://github.com/openai/codex/issues/28811)

8. **#28380 – Limits reset button not working**  
   *Open, 3 comments, 👍0*  
   Pressing “reset” instantly jumps to 100% without actual reset. Confirmed on Windows Pro.  
   [View Issue](https://github.com/openai/codex/issues/28380)

9. **#28740 – Rate resets cannot be obtained (multiple-user crisis)**  
   *Open, 2 comments, 👍4*  
   Declared a “critical vulnerability” by reporter. High frustration; no official acknowledgment yet.  
   [View Issue](https://github.com/openai/codex/issues/28740)

10. **#28606 – Codex lost all chat history; won’t save settings (Windows)**  
    *Closed, 4 comments, 👍1*  
    Third instance of this bug (#27998, #28588 were prior duplicates). Suggests a recurring Windows configuration persistence failure.  
    [View Issue](https://github.com/openai/codex/issues/28606)

---

## Key PR Progress

1. **#28826 – Use unique IDs for realtime-routed turns**  
   *Merged*  
   Prevents identity collisions across Session restarts in durable realtime voice orchestrator. Critical for reliable voice handoff.  
   [View PR](https://github.com/openai/codex/pull/28826)

2. **#28784 – fix(install): support older awk checksum parsing**  
   *Merged*  
   Fixes broken standalone installer on Debian/Ubuntu systems using mawk. Resolves issue #24219.  
   [View PR](https://github.com/openai/codex/pull/28784)

3. **#28822 – Add Config for Time Reminders (varlatency 1/n)**  
   *Open*  
   First PR in a series to inject current-time reminders into model requests. Config-driven, system-clock based.  
   [View PR](https://github.com/openai/codex/pull/28822)

4. **#28824 – current time reminders impl for system clock (varlatency 2/n)**  
   *Open*  
   Stacked on #28822. Implements host-injectable time provider, records developer reminders in history.  
   [View PR](https://github.com/openai/codex/pull/28824)

5. **#28814 – Assign response item IDs when recording history**  
   *Open*  
   Ensures client-created response items survive session persistence and resume. Fixes identity loss for rollouts.  
   [View PR](https://github.com/openai/codex/pull/28814)

6. **#28812 – Add optional IDs to response items**  
   *Closed*  
   Foundation PR for #28814. Standardizes Internal ID shape across ResponseItem variants.  
   [View PR](https://github.com/openai/codex/pull/28812)

7. **#27132 – Emit Trusted MCP App Identity on Tool-Call Items**  
   *Open*  
   Adds appContext to MCP tool calls so backend can link results to the originating app.  
   [View PR](https://github.com/openai/codex/pull/27132)

8. **#28829 – feat(app-server): complete filesystem host semantics**  
   *Open*  
   Adds lstat, readdir with type, file-type detection, and symlink handling to app-server filesystem API.  
   [View PR](https://github.com/openai/codex/pull/28829)

9. **#28825 – Expose selected MCP namespaces as direct model tools**  
   *Open*  
   Allows history/notes tools to stay top-level even when MCP deferral is enabled.  
   [View PR](https://github.com/openai/codex/pull/28825)

10. **#28593 – suppress usage warnings with credits**  
    *Open*  
    Hides proactive rate-limit warnings in TUI when workspace credits are available. Aligns UX with credit-based billing.  
    [View PR](https://github.com/openai/codex/pull/28593)

---

## Feature Request Trends

1. **Better rate-limit transparency** — users want visible, accurate meters and predictable reset mechanics (banked resets, working reset buttons).  
2. **Desktop resource management** — strong demand for crash dump caps, memory leak fixes, and idle CPU throttling.  
3. **Reliable local development environment** — persistent requests for stable Windows configuration saving, non-English filesystem support (@ file picker non-ASCII search, Korean profile crashes).  
4. **Workflow interruption guardrails** — TUI users want the model not to prompt while they’re typing, and typed input should not be lost during model questions.  
5. **Remote/sync fidelity** — repo-local skills and remote conversations should sync reliably across devices without data loss.

---

## Developer Pain Points

- **Rate-limit chaos**: Three distinct issues (#28823, #28811, #28380) all point to quota accounting regressions. The reset button is broken, meters run hot, and banked resets aren’t applied correctly. High cumulative community frustration.  
- **Windows data loss**: Repeated reports (#28606, #27998, #28588, #28797) of lost chat history and settings on Windows. Pattern suggests a deterministic bug tied to specific release builds.  
- **macOS resource leaks**: syspolicyd runaway and Crashpad dump accumulation are severe for power users who keep Codex Desktop open long-term.  
- **Authentication loops**: MFA setup can become circular if a user’s phone number is stale — no recovery path without contacting support.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-18

## Today's Highlights
Two new versions landed today: v0.47.0 (stable) and v0.48.0-preview.0 (preview). The agent subsystem continues to draw intense focus, with multiple high-priority open issues around subagent hang, recovery masking, and tool-overload errors. A wave of bug-fix PRs targeting core tooling — including Jupyter/JSON corruption, charset decoding in web-fetch, and macOS symlink mismatches — signals the team is actively hardening the reliability surface.

## Releases
- **v0.47.0** (stable) — Changelog auto-generated, includes backend definition respect and release infrastructure improvements.  
  [Release v0.47.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.47.0)

- **v0.48.0-preview.0** (preview) — Pre-release featuring a new Dependabot cooldown period for npm packages and additional refactoring.  
  [Release v0.48.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.48.0-preview.0)

## Hot Issues (Top 10 by Community Activity)

1. **#21409 — Generalist agent hangs** — The agent defers to a subagent and hangs indefinitely on simple tasks (folder creation). Workaround exists: instruct the model not to use subagents. 8 👍 indicate broad user pain.  
  [Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)

2. **#24353 — Robust component-level evaluations** — Epic tracking 76 behavioral eval tests across 6 supported Gemini models. The community is eager for deeper eval coverage.  
  [Issue #24353](https://github.com/google-gemini/gemini-cli/issues/24353)

3. **#22323 — Subagent recovery after MAX_TURNS reported as GOAL success** — The `codebase_investigator` subagent falsely reports success when it hits the turn limit, hiding interruptions. A critical transparency bug for trust in autonomous workflows. 2 👍.  
  [Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)

4. **#22745 — AST-aware file reads, search, and mapping** — Epic investigating whether AST-based tooling can reduce token waste and improve navigation precision. 1 👍 reflects niche but strategic interest.  
  [Issue #22745](https://github.com/google-gemini/gemini-cli/issues/22745)

5. **#25166 — Shell command hangs after completion ("Waiting input")** — Reproducible with trivial commands. High frequency (3 👍, P1) — a reliability blocker for shell-interactive workflows.  
  [Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)

6. **#21968 — Gemini does not use skills and sub-agents enough** — Even with custom skills defined, the model rarely self-delegates. Community anecdotal evidence suggests prompt engineering workaround needed.  
  [Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)

7. **#26525 — Add deterministic redaction and reduce Auto Memory logging** — Secrets can reach model context before redaction; Auto Memory logs skill content. A clear security and compliance concern. 5 comments.  
  [Issue #26525](https://github.com/google-gemini/gemini-cli/issues/26525)

8. **#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely** — Sessions without meaningful content get re-examined repeatedly, wasting tokens. A straightforward optimization with user-visible cost implications.  
  [Issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522)

9. **#21983 — Browser subagent fails on Wayland** — The `browser_agent` fails with "GOAL" termination under Wayland, likely due to display-server incompatibility. 1 👍.  
  [Issue #21983](https://github.com/google-gemini/gemini-cli/issues/21983)

10. **#24246 — 400 error with >128 tools** — When tool count exceeds a threshold, the CLI returns a 400 error. Users expect smarter tool-scoping.  
  [Issue #24246](https://github.com/google-gemini/gemini-cli/issues/24246)

## Key PR Progress (Top 10 by Impact)

1. **#28000 — `fix(core-tools): resolve Jupyter Notebook and JSON corruption in write_file`** — Critical fix for `.ipynb` and `.json` files being silently corrupted on write. Blocks collaborative notebook workflows.  
  [PR #28000](https://github.com/google-gemini/gemini-cli/pull/28000)

2. **#27996 — `fix(core): decode response body using charset from Content-Type header`** — `web-fetch` now respects charset headers, fixing garbled text on CJK/legacy sites. High-value for global users.  
  [PR #27996](https://github.com/google-gemini/gemini-cli/pull/27996)

3. **#27994 — `fix(core): insert skill/agent content literally in system prompt substitutions`** — Prevents injected content from being misinterpreted as `$` patterns, closing a subtle injection-class bug.  
  [PR #27994](https://github.com/google-gemini/gemini-cli/pull/27994)

4. **#27987 — `fix(cli): throw FatalConfigError instead of process.exit in parseArguments`** — Replaces abrupt `process.exit(1)` with proper error handling, improving E2E test compatibility.  
  [PR #27987](https://github.com/google-gemini/gemini-cli/pull/27987)

5. **#27986 — `feat(acp): report cached and thought tokens in PromptResponse.usage`** — Adds cached/reasoning token counts to ACP responses, fixing ~3× cost overestimation for ACP clients.  
  [PR #27986](https://github.com/google-gemini/gemini-cli/pull/27986)

6. **#27859 — `feat(cli): add native drag-and-drop and Cmd+V clipboard image pasting`** — Brings visual multimodal parity via terminal drag-and-drop and clipboard image insertion. A long-awaited UX improvement.  
  [PR #27859](https://github.com/google-gemini/gemini-cli/pull/27859)

7. **#27979 — `Wrap read_mcp_resource output with wrapUntrusted()`** — Security fix: MCP resource output now wrapped with untrusted marking, consistent with existing MCP-tool handling.  
  [PR #27979](https://github.com/google-gemini/gemini-cli/pull/27979)

8. **#27753 — `ci: validate workflow_run origin before consuming the E2E artifact`** — Prevents fork-based artifact poisoning in CI pipeline. Important supply-chain security hardening.  
  [PR #27753](https://github.com/google-gemini/gemini-cli/pull/27753)

9. **#27948 — `chore(deps): pin dependencies and enforce 14-day update cooldown`** — Strict pinning and cooldown period for npm dependencies. Reduces supply-chain risk from premature updates.  
  [PR #27948](https://github.com/google-gemini/gemini-cli/pull/27948)

10. **#27990 — `test(core-tools): resolve macOS symlink path mismatches in tests`** — Fixes false-positive test failures on macOS due to `/var -> /private/var` symlink. Essential for cross-platform CI reliability.  
  [PR #27990](https://github.com/google-gemini/gemini-cli/pull/27990)

## Feature Request Trends

- **AST-aware code understanding** — Multiple issues (#22745, #22746, #22747) explore using AST tools for file reads, search, and codebase mapping to reduce token consumption and improve method-boundary precision.
- **Agent self-awareness and configuration** — Users consistently request that the agent understand its own CLI flags, hotkeys, and configuration files to act as its own guide (#21432, #22267).
- **Destructive action prevention** — Safeguards against dangerous git/database operations (#22672) and uncontrolled temp script creation (#23571) are high-priority community asks.
- **Browser agent resilience** — Persistent session takeover, lock recovery, and Wayland support (#22232, #21983) are sought-after improvements for browser-automation reliability.

## Developer Pain Points

1. **Agent hangs and silent failures** — The generalist agent hangs indefinitely (#21409) and subagents mask MAX_TURNS interruptions as "GOAL success" (#22323), eroding trust in autonomous mode.
2. **Tool overload crashes** — Having >128 tools triggers a 400 error with no graceful degradation (#24246).
3. **Auto Memory waste and security leaks** — Low-signal sessions retried indefinitely (#26522), and secrets reach model context before redaction (#26525).
4. **Shell and terminal issues** — Commands hang after completion on "Awaiting input" (#25166), terminal resize causes flicker (#21924), and external editor exits leave corruption (#24935).
5. **Cross-platform fragility** — Wayland browser failures (#21983), macOS symlink test mismatches (#27990), and encoding issues on non-UTF-8 pages (#27996) fragment the user experience across environments.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-18

## Today's Highlights
The community is recovering from the June 16 Copilot outage, which caused widespread "Blocked/Disabled" model states and transient API errors. Meanwhile, long-running feature requests around tool whitelisting and plugin improvements continue to gain traction. Several new triage issues have been filed regarding content exclusion enforcement and custom alias support.

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 selected)

1. **[#3832 — All models show as 'Blocked/Disabled' after June 16 outage](https://github.com/github/copilot-cli/issues/3832)** (CLOSED, 👍 13)  
   Post-outage side effect: model selection interface rendered unusable. High community impact; resolved quickly.

2. **[#3831 — Request failed due to transient API error; retrying loop](https://github.com/github/copilot-cli/issues/3831)** (CLOSED, 👍 2)  
   Workflow-breaking infinite retry loop after the June 16 outage. Users had to kill sessions manually.

3. **[#1973 — Feature Request: Tool whitelist for Interactive Mode](https://github.com/github/copilot-cli/issues/1973)** (OPEN, 👍 20)  
   Top-voted open feature: allow safe read-only tools (grep, cat, git log) without manual approval. `/allow-all` is too coarse.

4. **[#2643 — preToolUse hook: silent rewrite still shows confirmation dialog](https://github.com/github/copilot-cli/issues/2643)** (OPEN, 👍 1)  
   Plugin hooks cannot silently rewrite commands even with `permissionDecision: allow`. Blocks automation workflows.

5. **[#3839 — Ollama Cloud doesn't support `custom_tool_call` payload](https://github.com/github/copilot-cli/issues/3839)** (OPEN, 👍 7)  
   BYOK Fleet Mode broken with Ollama Cloud due to incompatible payload format. Limits self-hosted model options.

6. **[#3560 — CAPIError: 400 Duplicate item found with id](https://github.com/github/copilot-cli/issues/3560)** (OPEN, 👍 1)  
   Tool call ID duplication error appears suddenly after a tool execution. Plain chat works; tool calls fail.

7. **[#3355 — Allow configurable context window for Claude Opus 4.6](https://github.com/github/copilot-cli/issues/3355)** (OPEN, 👍 4)  
   CLI caps at 200K tokens vs model's 1M capability. Heavy users hit compaction in deep sessions.

8. **[#3730 — Support Enterprise-Managed Custom Models in Copilot CLI](https://github.com/github/copilot-cli/issues/3730)** (OPEN, 👍 4)  
   Enterprise custom models not available in CLI despite being available in VS Code. Blocks enterprise adoption.

9. **[#3812 — Subagents can no longer access MCP tools](https://github.com/github/copilot-cli/issues/3812)** (OPEN)  
   Regression: MCP tools inaccessible from subagents. Top-level agent works. Related to deferred MCP loading.

10. **[#3841 — Copilot CLI incorrectly enforces content exclusions](https://github.com/github/copilot-cli/issues/3841)** (OPEN)  
    Organization content-exclusion policy applied to CLI despite documentation stating otherwise. Blocks local file operations.

## Key PR Progress
No pull requests updated in the last 24 hours.

## Feature Request Trends
- **Plugin lifecycle management**: Multiple requests for `copilot plugin update --all` and bulk plugin management ([#3830](https://github.com/github/copilot-cli/issues/3830))
- **Custom aliases and commands**: Users want user-defined `/commands` mapped to models/prompts ([#3844](https://github.com/github/copilot-cli/issues/3844), [#3074](https://github.com/github/copilot-cli/issues/3074) for `/effort`)
- **Persistent session configurations**: `/instructions` opt-out should persist per-repo, not reset each session ([#3840](https://github.com/github/copilot-cli/issues/3840))
- **MCP tool preloading**: Lazy loading of MCP tools causes subagent incompatibility; requests for eager loading ([#3787](https://github.com/github/copilot-cli/issues/3787), [#3292](https://github.com/github/copilot-cli/issues/3292))
- **Enterprise model support**: Demand for custom/self-hosted models in CLI ([#3730](https://github.com/github/copilot-cli/issues/3730), [#3839](https://github.com/github/copilot-cli/issues/3839))

## Developer Pain Points
1. **June 16 outage aftermath**: Transient API errors and model selection UI glitches disrupted workflows for many users; recovery required manual intervention.
2. **No safe tool whitelisting**: Interactive mode forces per-tool approval for read-only operations, while `/allow-all` permits destructive commands ([#1973](https://github.com/github/copilot-cli/issues/1973)). This is the most-upvoted open issue (👍 20).
3. **Plugin hook limitations**: `preToolUse` hooks cannot silently rewrite commands even with explicit permission grants ([#2643](https://github.com/github/copilot-cli/issues/2643)). Plugin installation also fails when `git core.fsmonitor` is enabled ([#3842](https://github.com/github/copilot-cli/issues/3842)).
4. **Session resume fragility**: `--resume` fails silently with names containing spaces ([#3754](https://github.com/github/copilot-cli/issues/3754)). Resume also doesn't show the working directory ([#3837](https://github.com/github/copilot-cli/issues/3837)).
5. **Context window caps**: Hard 200K token limit on models supporting 1M tokens forces premature compaction in complex sessions ([#3355](https://github.com/github/copilot-cli/issues/3355)).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Okay, here is the Kimi Code CLI community digest for 2026-06-18.

---

## Kimi Code CLI Community Digest - 2026-06-18

### Today's Highlights
Today marks a quiet period for the Kimi CLI, with no new releases or pull requests in the last 24 hours. The community activity is focused on two new feature requests: one for dynamic runtime mode switching between Agent and Cluster, and another for a critical SSL certificate ignore option needed for restricted enterprise environments. The absence of PRs suggests the development team may be consolidating recent changes.

### Releases
- **No new releases** were published in the last 24 hours.

### Hot Issues
- **#2459 - [Feature Request] 支持会话运行中切换执行模式（Agent ↔ 集群）** (Opened 2026-06-17)
  - **Significance:** This is a highly requested workflow flexibility feature. Users want to start a session in a simple Agent mode, and then scale it up to a Cluster mode for complex tasks without losing context. This would bridge the gap between quick prototyping and production-grade execution.
  - **Community Reaction:** No comments or reactions yet, but the request is clear and addresses a major pain point for advanced users.
  - **Link:** [Issue #2459](https://github.com/MoonshotAI/kimi-cli/issues/2459)

- **#2458 - [enhancement] Add option to ignore ssl certificate** (Opened 2026-06-17)
  - **Significance:** This is a critical blocker for users in large enterprises with strict IT security policies (e.g., SSL inspection via MITM). Without this flag, the CLI is effectively unusable on many corporate or managed PCs. This is a "table-stakes" feature for enterprise adoption.
  - **Community Reaction:** No comments yet, but this is a high-urgency fix. The author's detailed explanation of an antivirus SSL MITM scenario highlights a very common enterprise infrastructure pattern.
  - **Link:** [Issue #2458](https://github.com/MoonshotAI/kimi-cli/issues/2458)

### Key PR Progress
- **No pull requests** were updated or created in the last 24 hours.

### Feature Request Trends
- **Dynamic Execution Mode Switching:** Users are no longer content with static configurations. The request in #2459 for real-time switching between Agent and Cluster modes indicates a strong desire for a unified, fluid workflow where tasks can scale seamlessly from single-agent reasoning to distributed execution.
- **Enterprise Network Compatibility:** The request for an SSL certificate ignore option (#2458) confirms that a significant portion of the user base (or potential user base) is operating behind corporate firewalls and manages networks. The CLI's adoption in these environments is currently blocked.

### Developer Pain Points
- **Enterprise Security Restrictions:** The most tangible developer pain point today is the inability to use the CLI behind corporate SSL inspection proxies. This is not a "nice-to-have" but a fundamental blocker for deployment in the most common enterprise environments. Users are forced to either disable their antivirus or find workarounds, which is unacceptable for production use.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-18

## Today's Highlights

OpenCode v1.17.8 ships with faster session timeline loading and two critical provider fixes (MCP schema validation and Cloudflare AI Gateway API key passing). The community is heavily focused on GPT model latency (117 comments) and sandboxing agent capabilities (72 comments), while multiple PRs target auto-model discovery and session management UX improvements.

## Releases

**v1.17.8** — [Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.8)
- **Core**: Session timelines load much faster with reduced flicker and scroll jumps.
- **Bugfixes**:
  - OpenAI-compatible providers now correctly accept MCP tool schemas that previously failed validation. ([@jquense](https://github.com/jquense))
  - Cloudflare AI Gateway now properly receives the configured API key. ([@keefetang](https://github.com/keefetang))

## Hot Issues

1. **[#29079 — GPT Models takes too long to respond](https://github.com/anomalyco/opencode/issues/29079)** (117 comments, 49 👍)  
   *Why it matters*: GPT models (especially GPT-5.4 xhigh) show erratic response times from seconds to *minutes* for simple commands. This is the #1 performance complaint and likely top priority for the core team.

2. **[#2242 — Is there a way to sandbox the agent?](https://github.com/anomalyco/opencode/issues/2242)** (72 comments, 54 👍)  
   *Why it matters*: Users want to restrict agent terminal commands to the current project directory. The request compares against Gemini CLI and Codex CLI's seatbelt (macOS) functionality—a clear security gap.

3. **[#11176 — Official OpenCode VS Code extension](https://github.com/anomalyco/opencode/issues/11176)** (23 comments, 110 👍)  
   *Why it matters*: Highest-reacted issue. The community desires native VS Code integration to run OpenCode as a side panel natively, reducing context-switching friction.

4. **[#17994 — Multi-agent orchestration in isolated workspaces](https://github.com/anomalyco/opencode/issues/17994)** (21 comments, 2 👍)  
   *Why it matters*: Growing demand for "team" workflows—coordinating multiple coding agents in isolated workspaces, similar to specialized coding tools.

5. **[#6096 — Tokens per second (TPS) display](https://github.com/anomalyco/opencode/issues/6096)** (18 comments, 55 👍)  
   *Why it matters*: Users want performance transparency per model response to compare providers and model variants.

6. **[#8456 — Auto-select models based on task type](https://github.com/anomalyco/opencode/issues/8456)** (7 comments, 36 👍)  
   *Why it matters*: Leading competitors (e.g., Codex) offer per-task model routing (e.g., cheap model for file search, expensive model for complex reasoning). High interest in adaptive model selection.

7. **[#20902 — bash tool hangs with background child processes](https://github.com/anomalyco/opencode/issues/20902)** (9 comments, 9 👍)  
   *Why it matters*: Commands like `npm run build &` or `nohup` cause indefinite hangs until 2-minute timeout—a critical workflow blocker.

8. **[#19466 — CPU usage spikes during API rate-limit waiting](https://github.com/anomalyco/opencode/issues/19466)** (9 comments, 8 👍)  
   *Why it matters*: A single core spikes to ~50% while the app is actively doing nothing (waiting for rate-limit retry). Indicates a tight polling or busy-wait issue.

9. **[#32444 — GLM-5.2 thinking-effort variants not exposed](https://github.com/anomalyco/opencode/issues/32444)** (3 comments, 8 👍)  
   *Why it matters*: Z.AI's latest GLM-5.2 model supports thinking-effort levels (High/Max) but code in `transform.ts` blanket-excludes any model ID containing "glm" from variant selector. Active community frustration.

10. **[#32749 — Explore agent is a huge waste of tokens](https://github.com/anomalyco/opencode/issues/32749)** (2 comments, 0 👍)  
    *Why it matters*: Fresh complaint — the explore subagent spawns eagerly even for trivial tasks where `grep` would suffice, forcing the main agent to re-read all touched files. Costly for API-usage-sensitive users.

## Key PR Progress

1. **[#32752 — `opencode session select` interactive picker](https://github.com/anomalyco/opencode/pull/32752)** (NEW, OPEN)  
   Adds a `/sessions` interactive dialog with `@clack/prompts` autocomplete for selecting project-scoped sessions.

2. **[#32750 — Global session list scope toggle](https://github.com/anomalyco/opencode/pull/32750)** (NEW, OPEN)  
   A new keybinding (Ctrl+G) cycles session list between local ↔ project ↔ global scopes. Improves multi-project workflow.

3. **[#32753 — Clipboard fallback for non-HTTPS contexts](https://github.com/anomalyco/opencode/pull/32753)** (NEW, OPEN)  
   Fixes copy-to-clipboard for code blocks when running on localhost without HTTPS. Targets web deployment UX gap.

4. **[#32731 — Auto-discover models from OpenAI-compatible providers](https://github.com/anomalyco/opencode/pull/32731)** (NEW, OPEN)  
   Calls `GET /v1/models` on configured base URLs to auto-populate model list instead of requiring manual entries. Closes #6231.

5. **[#30879 — ACP shell command display & replay improvements](https://github.com/anomalyco/opencode/pull/30879)** (OPEN)  
   Title now shows actual command, outputs streamed in real-time on TUI. Enhances the agent communication protocol (ACP) debugging experience.

6. **[#27163 / #32743 — Native per-session goals](https://github.com/anomalyco/opencode/pull/27163)** (OPEN)  
   Two competing implementations add `/goal` commands for persisted session goals with status (active/paused/completed), exposed via HTTP APIs. Community debate on direction.

7. **[#27554 — Local LAN provider discovery + auto-discover models](https://github.com/anomalyco/opencode/pull/27554)** (OPEN)  
   Combines mDNS, SSDP, and manual IP scanning to discover local AI servers. Aims to solve the "Ollama LAN" setup pain. Closes #6231, #27553.

8. **[#32734 — OpenRouter model variant support](https://github.com/anomalyco/opencode/pull/32734)** (CLOSED)  
   Enables variants like `:free`, `:extended`, `:thinking` by resolving variant-suffixed IDs to base catalog entries while passing full suffixed ID to OpenRouter API.

9. **[#20491 — Kiro (AWS) provider plugin](https://github.com/anomalyco/opencode/pull/20491)** (OPEN)  
   Adds AWS/Kiro as a bundled provider plugin. Expands cloud provider ecosystem.

10. **[#32052 — Cloudflare AI Gateway API key fix](https://github.com/anomalyco/opencode/pull/32052)** (CLOSED, MERGED)  
    `createUnified()` now receives `apiKey` for Cloudflare AI Gateway. Fix in v1.17.8 release.

## Feature Request Trends

1. **Auto model selection** — Multiple issues/PRs (#8456, #32736, #32731) request the system to automatically choose models based on task type (cheap model for grep, expensive model for complex reasoning).

2. **Sandboxing & security** — #2242 (sandbox agent), #1852 (sudo break), and #7928 (runtime permission toggle) show strong demand for restricting agent actions, permissions, and file access.

3. **Session management UX** — #32750 (scope toggle), #32752 (picker), #27163/#32743 (per-session goals) indicate the community wants better session organization, searchability, and lifecycle control.

4. **Local/self-hosted first-class support** — #27554 (LAN discovery), #32744 (local qwen3-coder frustrations), and multiple local provider issues reflect a large segment using local models.

5. **Model provider expansion** — GLM-5.2 variants (#32444), Z.AI support (#32172), Kiro (#20491), Devin.ai provider request (#24072) show continuous appetite for new model backends.

## Developer Pain Points

- **GPT latency unpredictability** — #29079 (117 comments) is the hottest issue. Response times vary from seconds to minutes for identical simple tasks.
- **Background process hangs** — #20902: any `&`, `nohup`, or `bash -c` pattern triggers 2-minute hangs. Forces workarounds like `timeout`.
- **Clipboard & input breakage** — #24817 (Ctrl+Z suspends on Linux), #32753 (clipboard broken on HTTP), #32754 (garbled escape codes on Windows after reinstall) indicate cross-platform UX regressions.
- **Forceful subagent spawning** — #32749 (explore agent token waste) and #19466 (CPU spike during rate-limit) show resource optimization gaps.
- **Provider onboarding friction** — #32745 (OpenRouter authorization stuck), #32720/#32722 (AI models stopped working after apparent random failure), #29748 (server error after adding OpenRouter) suggest fragile provider initialization flows.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-18

## Today's Highlights
The community is actively working through two major infrastructure migrations: moving off Shrinkwrap to fix module duplication issues (#5653) and improving provider error handling so gateway/proxy errors are no longer opaque (#5763, #5832, #5828). On the model front, support for "max" thinking levels on Anthropic models has been added (#5829), and a new Azure AI Foundry provider for Anthropic Claude was merged (#5849).

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **#5825 — Streaming markdown forces scroll to bottom** *(OPEN, 12 comments)*
   - User reports that when `clear on shrink` is enabled, Pi forces scroll-to-bottom during streaming, making it impossible to read earlier output while the agent is still generating. A fix PR (#5846) has been opened to stabilize streaming code fence rendering.
   - [GitHub](https://github.com/earendil-works/pi/issues/5825)

2. **#5653 — Move off Shrinkwrap** *(OPEN, 11 comments)*
   - Installing both `@earendil-works/pi-ai` and `@earendil-works/pi-coding-agent` as direct dependencies places two identical copies of `pi-ai` on disk. Since the API provider registry is a module-level `Map`, the two copies are separate module instances. This is a critical architecture fix.
   - [GitHub](https://github.com/earendil-works/pi/issues/5653)

3. **#3715 — `local-llm` streams terminate at 5 min from undici default `bodyTimeout`** *(CLOSED, 11 comments)*
   - Long `Write` tool calls against local OpenAI-compatible backends (vLLM) die with `UND_ERR_BODY_TIMEOUT` after exactly 5 minutes. The `retry.provider.timeoutMs` setting does not override undici's default. Heavy community demand (4 👍). Now closed.
   - [GitHub](https://github.com/earendil-works/pi/issues/3715)

4. **#534 — Config folder is out of place on Linux** *(CLOSED, 9 comments)*
   - The most upvoted issue this week (20 👍). Config is stored directly in `$HOME` instead of following the XDG Base Directory spec. A long-standing request that was finally addressed.
   - [GitHub](https://github.com/earendil-works/pi/issues/534)

5. **#5763 — Providers swallow the HTTP error body** *(OPEN, 5 comments)*
   - Behind a proxy/gateway, non-2xx responses with meaningful error bodies are dropped. The same 403 surfaces differently per provider (`Unknown: UnknownError` on Bedrock, `403 status code (no body)` on OpenAI). Multiple PRs now target this (#5832, #5828).
   - [GitHub](https://github.com/earendil-works/pi/issues/5763)

6. **#5700 — Support multiple live agent sessions with TUI switching** *(OPEN, 5 comments)*
   - User requests the ability to juggle multiple concurrent agent sessions, switching between them in the TUI without tearing down the current session. Currently `switchSession` destroys state.
   - [GitHub](https://github.com/earendil-works/pi/issues/5700)

7. **#5830 — Tree navigator truncates long entries** *(CLOSED, 4 comments)*
   - The tree navigator (Esc+Esc) renders every entry with `truncateToWidth`, making deep or verbose chat entries unreadable. Fixed in the latest builds.
   - [GitHub](https://github.com/earendil-works/pi/issues/5830)

8. **#5827 — Warp terminal not detected for Kitty image protocol** *(OPEN, 3 comments)*
   - Pi's TUI does not detect Warp as an image-capable terminal, so images fall back to text. A fix PR (#5841) detects Warp via `TERM_PROGRAM`, `WARP_SESSION_ID`, or `WARP_TERMINAL_SESSION_UUID` environment variables.
   - [GitHub](https://github.com/earendil-works/pi/issues/5827)

9. **#5862 — Codex Subscription Error: quota exceeded but Codex CLI works** *(CLOSED, 2 comments)*
   - Users with ChatGPT Plus/Pro (Codex Subscription) can authenticate but receive quota errors when chatting. The Codex CLI itself works fine, suggesting an API usage tracking mismatch in Pi.
   - [GitHub](https://github.com/earendil-works/pi/issues/5862)

10. **#5861 — Allow persistent, customizable display of content not sent in requests** *(CLOSED, 1 comment)*
    - Requests the ability to have persistent (session-stored, visible on resume) display of content that is *not* sent to the LLM, mirroring the behavior of `custom_message` but with an `excludeFromContext` flag.
    - [GitHub](https://github.com/earendil-works/pi/issues/5861)

## Key PR Progress

1. **#5846 — fix(tui): stabilize streaming code fence rendering** *(OPEN)*
   - Closes #5825. Addresses the scroll-jumping issue during streaming markdown generation. @xl0's fix targets the rendering pipeline for code fences during active streams.
   - [GitHub](https://github.com/earendil-works/pi/pull/5846)

2. **#5849 — feat(ai): add Azure AI Foundry provider for Anthropic Claude** *(CLOSED)*
   - Adds first-class support for Azure AI Foundry hosted Anthropic Claude models via a new `azure-foundry` provider. Includes full Python `AnthropicFoundry` SDK parity with Entra ID auth support.
   - [GitHub](https://github.com/earendil-works/pi/pull/5849)

3. **#5829 — feat: add "max" thinking level for adaptive reasoning models** *(CLOSED)*
   - Extends `ThinkingLevel` beyond `xhigh` to support `max` reasoning effort. Models affected: `claude-opus-4.8`, `claude-opus-4.7` (both add `max`); `claude-opus-4.6`, `claude-sonnet-4.6` (add both `xhigh` and `max`).
   - [GitHub](https://github.com/earendil-works/pi/pull/5829)

4. **#5832 — fix(ai): surface provider HTTP error body instead of opaque SDK message** *(OPEN)*
   - Fixes #5763. Behind a proxy/gateway, non-2xx response bodies are now surfaced instead of `Unknown: UnknownError` or `403 status code (no body)`.
   - [GitHub](https://github.com/earendil-works/pi/pull/5832)

5. **#5859 — fix(ai): send responses prompts as instructions** *(OPEN)*
   - OpenAI Responses APIs expect system prompts in top-level `instructions`, not replayed `input` messages. Affects OpenAI, Azure OpenAI, and Codex Responses providers.
   - [GitHub](https://github.com/earendil-works/pi/pull/5859)

6. **#5841 — feat(tui): detect Warp terminal and enable Kitty image protocol** *(OPEN)*
   - Fixes #5827. Detects Warp terminal via environment variables, enabling inline image rendering (Kitty protocol) and OSC 8 hyperlinks without the `TERM_PROGRAM=kitty` workaround.
   - [GitHub](https://github.com/earendil-works/pi/pull/5841)

7. **#5801 — Nixify pi** *(CLOSED)*
   - Adds Nix flake packaging to Pi, enabling `nix build`, `nix run`, and `nix profile add` for reproducible builds.
   - [GitHub](https://github.com/earendil-works/pi/pull/5801)

8. **#5833 — Compaction-related fixes** *(CLOSED)*
   - Three fixes to the compaction mechanism: reordering suppressed token recalculations, preventing unnecessary compaction runs, and ensuring `systemPrompt` changes trigger proper compaction.
   - [GitHub](https://github.com/earendil-works/pi/pull/5833)

9. **#5701 — fix(ai/model): adjust minimax-m3 context size** *(CLOSED)*
   - Corrects the Minimax-M3 context size from 1M to 524,288 tokens, matching the OpenRouter endpoint limit. Users were hitting "maximum context length" errors.
   - [GitHub](https://github.com/earendil-works/pi/pull/5701)

10. **#5847 — Comath/research exploration mode** *(CLOSED)*
    - A draft checkpoint for collaborative math research exploration. Adds natural research entrypoints, path management, async research workstream lifecycle, source-backed intake, and paper-alignment checkpoint tests.
    - [GitHub](https://github.com/earendil-works/pi/pull/5847)

## Feature Request Trends

- **Extended thinking/reasoning levels**: Multiple requests for exposing `max` thinking level on Anthropic models (#5831) and effort level configuration for Zhipu/GLM-5.2 (#5770) and GitHub Copilot models (#5768).
- **Multiple concurrent sessions**: Strong demand for background agent sessions that don't require tearing down the active session (#5700), plus RPC commands to inspect entry trees (#5810).
- **Multi-modal support**: Requests to extend the `prompt` command to forward video/audio content alongside existing image support (#3200).
- **Persistent non-LLM content**: Ability to store and display session content that is explicitly excluded from LLM context (#5861), mirroring `excludeFromContext` on custom messages (#5654).
- **Project-level configuration**: Requests to control `--no-skills` / `--skill` behavior in `.pi/settings.json` (#5570).

## Developer Pain Points

- **Provider error opacity**: Swallowed HTTP error bodies from gateways/proxies is the #1 infrastructure pain point, with two independent PRs (#5832, #5828) and an issue (#5763) all targeting the same problem this week.
- **Shrinkwrap module duplication**: The Shrinkwrap bundling strategy causes duplicated `pi-ai` module instances, breaking provider registries (#5653). This is a blocking issue for anyone using multiple Pi packages.
- **Streaming UI regressions**: The scroll-to-bottom behavior during streaming (#5825) disrupts the reading experience, especially for users who read slower than the agent generates.
- **Model context window mismatches**: Multiple issues about incorrect context window limits for Minimax (#5701), GLM-5.2 (#5692), and GitHub Copilot models (#5768), suggesting the provider configs need ongoing maintenance.
- **Terminal detection gaps**: Warp terminal not recognized for image protocol (#5827) and tree navigator truncation (#5830) highlight ongoing TUI polish needs across terminal emulators.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-18

## 1. Today's Highlights

Qwen Code shipped **v0.18.3** (stable) with a critical fix for CLI cancellation and tracked sed edits in file history. Meanwhile, the community is intensely debating the proposed **OAuth free tier reduction** (from 1,000 to 100 requests/day) across 151 comments — the most active thread in the repo. On the PR side, a new **tool-call circuit breaker** is under review to prevent runaway loops (addressing issue #5234), and several long-skipped test suites are being re-enabled by community contributors.

## 2. Releases

- **v0.18.3-nightly.20260618** — Nightly build with latest commits.
- **v0.18.3** (stable) — **What's Changed:**
  - `fix(core): Track supported sed edits in file history` by @doud
  - `fix(cli): Stop after cancelled ask_user_question` by @doudouOUC
- **v0.18.3-preview.0** — Preview of same fixes.
- **v0.18.2** — **What's Changed:**
  - `fix: warn on oversized context instructions` by @he-yufeng
  - `docs: fix stale defaults, CLI syntax, and tool naming drift` by @DragonnZhan
- **v0.18.1-preview.1** — Same fixes as v0.18.2, preview.

## 3. Hot Issues (Top 10)

1. **#3203 [OPEN] — Qwen OAuth Free Tier Policy Adjustment**  
   Proposal to slash daily free quota from 1,000 to 100 requests, and phase out OAuth free entry by July. **151 comments** — the community is pushing back hard. 💥  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/3203)

2. **#4479 [OPEN] — Feature: Daily Token Consumption Statistics**  
   User shocked by 30M token usage in one session. Requests a built-in dashboard for daily token tracking. High consensus (16 comments).  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4479)

3. **#3384 [OPEN] — Unable to add OpenAI-compatible local LLM**  
   Configuration `modelProviders` fails for VLLM-hosted Qwen3.6-35B. **15 comments** — affects self-hosters.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/3384)

4. **#5267 [OPEN] — `context.fileName` setting doesn't work**  
   User reports `setting.json` `context.fileName` directive ignored on latest v0.18.3.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/5267)

5. **#5210 [CLOSED] — ExitPlanMode stuck for 7+ hours**  
   On qwen3.7-max, exiting Plan Mode hangs indefinitely. Community reports "frequent" recurrence.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/5210)

6. **#5090 [OPEN] — Refactor: Decouple Provider Identity from SDK Protocol**  
   Proposal to allow custom provider IDs + explicit `Protocol` enum. 5 comments, in-review — architecturally significant.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/5090)

7. **#5234 [OPEN] — Tool calls stuck in infinite loop**  
   Tools repeat same call without termination. Reported on qwen3.7-plus with custom OpenAI provider.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/5234)

8. **#3914 [OPEN] — API connected, no errors but then fail to fetch**  
   OpenRouter + Node.js 26 users hit `fetch failed`. 9 comments, 3 👍 — growing pain with newer runtime.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/3914)

9. **#5180 [OPEN] — Subagent crashes mid-task in multi-agent setup**  
   Session analysis shows 12h 13m runtime before crash. Long-context session management fragility.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/5180)

10. **#5265 [CLOSED] — `content` field missing after forced reboot**  
    Session state not persisted across OS reboot; causes `400 InternalError`. Same root as #5237 (tool call repetition).  
    [GitHub](https://github.com/QwenLM/qwen-code/issues/5265)

## 4. Key PR Progress (Top 10)

1. **#5279 [OPEN] — fix(core): always-on tool-call circuit breaker for runaway loops**  
   Re-scoped fix for #5234. Maintainer-led; strips unrelated changes from earlier PR.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/5279)

2. **#5256 [OPEN] — fix(core): detect .dat files by content**  
   Stops treating all `.dat` files as binary; uses content-based fallback. Prevents false binary classification.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/5256)

3. **#5266 [OPEN] — fix(daemon): centralize mid-turn event constant + recover timed-out drains**  
   Follow-up to #5175. Consolidates SSE event type constants and fixes drain recovery.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/5266)

4. **#5220 [OPEN] — feat(i18n): localize tool display names in TUI and web-shell badges**  
   Routes tool badges (`TodoWrite`, `Shell`, etc.) through i18n — English-only today; Chinese support incoming.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/5220)

5. **#5202 [OPEN] — feat(channel): add QQ Bot (QQ机器人) channel adapter**  
   New `@qwen-code/channel-qqbot` package with WebSocket Gateway, HELLO/IDENTIFY/HEARTBEAT support. PR-ready.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/5202)

6. **#5030 [OPEN] — feat(core,cli,sdk): resume an interrupted turn without synthetic "continue" message**  
   First-class session resume after crash/interruption — no more fake `"continue"` in transcript.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/5030)

7. **#5179 [OPEN] — fix(model): remember selected provider when multiple share a model id**  
   Model picker now persists `baseUrl` alongside model name. Direct fix for #5173.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/5179)

8. **#5145 [OPEN] — feat(cli): show follow-up suggestion in input placeholder**  
   Uses fast model to suggest next prompt in the input field placeholder — no more chip hunting.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/5145)

9. **#5245 [OPEN] — fix: hide empty native sessions on Windows**  
   Two Windows fixes: tilde `~\` path expansion and hiding empty sessions in the session list.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/5245)

10. **#5283 [OPEN] — test(cli): enable command search long suggestion coverage**  
    Community member re-enables a long-skipped test for prompt suggestion expand/collapse.  
    [GitHub](https://github.com/QwenLM/qwen-code/pull/5283)

## 5. Feature Request Trends

- **Token usage transparency** — Multiple requests (#4479, #3267) for daily/weekly token consumption dashboards, rate limit visibility, and per-session cost breakdown.
- **Custom provider flexibility** — High demand for arbitrary provider IDs, explicit protocol selection (OpenAI/Gemini/Anthropic/QwenOAuth), and easier model addition from the UI (#5090, #4814).
- **Session management improvements** — `qwen sessions list` with `--json`, tags, date filters (#4825); session tagging and persistence control (#5237, #5265).
- **I18n and UX polish** — Localized tool display names (#5220), vim-mode dropdown navigation (#2561), and follow-up suggestions in-place (#5145).
- **Multi-agent reliability** — Subagent crash resilience, long-context session stability (#5180).

## 6. Developer Pain Points

- **OAuth free tier anxiety** — The proposed 100 req/day cap (#3203) has the community worried about viability for casual/learning use. Many ask for a viable Pro plan alternative (#3272, #3307).
- **Authentication confusion** — Swapping between OAuth and API keys leaves stale sessions; 401 errors plague users (#1855, #3335, #3281). Token refresh after expiry is unreliable.
- **Windows/macOS edge cases** — Trackpad scroll hijacked by tmux (#5159), tilde path expansion broken on Windows (#5245), Node.js 26 fetch failures (#3914, #4274).
- **Model provider disambiguation** — Identical model IDs from different providers cause persistent confusion; selection doesn't stick across sessions (#5173, #3384).
- **Tool call loops** — Repetitive tool invocation without termination (#5234, #5237) is a top frustration, with the circuit breaker PR (#5279) seen as a long-needed safeguard.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-18

## Today's Highlights
The project has undergone a significant identity shift: the repository is now **CodeWhale** (formerly DeepSeek-TUI), with migration issues like #2917 surfacing from the rename. Despite the rebrand, the team is pushing aggressively toward v0.9.0 with two major EPICs in flight: a command-boundary refactor (#2870) and a chat-native workroom system (#3209). The community is reporting several regressions around mode toggling, scope creep, and snapshot behavior, all of which have incoming fixes in today's PR batch.

## Releases
No new releases in the last 24 hours. The latest stable remains **v0.8.61**, with v0.9.0 tracked in EPIC #3209.

---

## Hot Issues (10 of 13 updated in last 24h)

### 1. [#3275 — CodeWhale overly involved in self-questioning/answering, deviating from user intent](https://github.com/Hmbown/CodeWhale/issues/3275)
- **Why it matters:** A regression from #3061 where the agent enters a self-sustaining loop of proposing, answering, and executing without user confirmation. This is a fundamental UX trust issue — developers need an assistant that follows intent, not an autonomous script generator.
- **Reaction:** 4 comments, opened by yekern. Already has a targeted PR (#3290) with `scope_discipline` prompt rules.

### 2. [#3279 — Plan/Agent Mode Toggle Inconsistency & Tool Permission Chaos](https://github.com/Hmbown/CodeWhale/issues/3279)
- **Why it matters:** Switching from Plan to Agent mode fails to restore `write_file`/`exec_shell` permissions properly, and after fixing, the AI auto-executes plans without permission. Double failure in mode semantics.
- **Reaction:** 3 comments, opened by yekern. PR #3283 addresses both issues.

### 3. [#3289 — v0.8.61 UI froze after auto-spawning several agents](https://github.com/Hmbown/CodeWhale/issues/3289)
- **Why it matters:** Plan mode spawns multiple agents automatically, freezing the TUI entirely. Blocks any multi-agent workflow on v0.8.61.
- **Reaction:** 2 comments — opened by bruce6135, minimal discussion yet.

### 4. [#3292 — `pre_tool_snapshot` did not respect `snapshots.enabled=false`](https://github.com/Hmbown/CodeWhale/issues/3292)
- **Why it matters:** Users disabling snapshots still have their entire git repo copied to `~/.deepseek/snapshots/`, eating GBs of disk space. Config was ignored entirely.
- **Reaction:** 1 comment — opened by LmeSzinc; PR #3293 fixes immediately.

### 5. [#3281 — Moonshot/Kimi parameters still missing `type:object` after v0.8.61 fix](https://github.com/Hmbown/CodeWhale/issues/3281)
- **Why it matters:** A partial fix for #3265 only handled narrow schema patterns. Schemas using `$ref`, `anyOf`, or `allOf` at root still cause 400 errors from Kimi/Moonshot API.
- **Reaction:** 2 comments, opened by jghwwnq. PR #3286 provides a more robust `sanitize_for_kimi_parameters`.

### 6. [#3282 — `config.toml` comments erased on TUI modification](https://github.com/Hmbown/CodeWhale/issues/3282)
- **Why it matters:** TUI config edits silently strip all comments and commented-out keys. Devs rely on those for notes and temporary disablement.
- **Reaction:** 1 comment — opened by Artenx. PR #3291 fixes with `toml_edit` merge.

### 7. [#2870 — EPIC: Staged command-boundary refactor for v0.9.0](https://github.com/Hmbown/CodeWhale/issues/2870)
- **Why it matters:** The structural refactor of how commands are defined and dispatched. This is the foundation for v0.9.0's command system.
- **Reaction:** 5 comments, opened by aboimpinto. Tracks multiple mergeable PRs.

### 8. [#3209 — EPIC: Chat-native CodeWhale workrooms for threaded, shareable agent work](https://github.com/Hmbown/CodeWhale/issues/3209)
- **Why it matters:** Vision for v0.9.0 — moving from terminal-only to chat-native workrooms with threads, mentions, shareable links, and mobile access. Ambition is huge.
- **Reaction:** 2 comments, opened by Hmbown. The project's north-star direction.

### 9. [#2917 — Cargo distribution: `codewhale` not found after rename from `deepseek-tui`](https://github.com/Hmbown/CodeWhale/issues/2917)
- **Why it matters:** Users who installed via `deepseek update` are left with a broken binary after the rename. PATH and update mechanism failed.
- **Reaction:** 4 comments, closed. Shipped in a previous fix.

### 10. [#1530 — Feature: Support session continuity in non-interactive mode](https://github.com/Hmbown/CodeWhale/issues/1530)
- **Why it matters:** `exec` and `--prompt` always start fresh. No way to continue a session non-interactively, blocking CI/CD and multi-turn automation.
- **Reaction:** 2 comments, closed as superseded. Noted in EPIC #3209.

---

## Key PR Progress (10 of 22 updated in last 24h)

### 1. [#3293 — fix(tui): respect `snapshots.enabled` for per-tool snapshots](https://github.com/Hmbown/CodeWhale/pull/3293)
- **What it does:** Adds the missing guard in `turn_loop.rs` so `write_file`/`edit_file`/`apply_patch` no longer create snapshots when `snapshots.enabled = false`.
- **Why it matters:** Direct fix for #3292, preventing GB-level disk waste.

### 2. [#3291 — Fix/preserve comments in config files](https://github.com/Hmbown/CodeWhale/pull/3291)
- **What it does:** All config write paths now use `toml_edit` to merge user comments with serialized output.
- **Why it matters:** Fixes #3282 — user annotations survive TUI edits.

### 3. [#3290 — fix(prompts): add `scope_discipline` rules to prevent self-questioning loops](https://github.com/Hmbown/CodeWhale/pull/3290)
- **What it does:** Adds +47 lines to `constitution.md` instructing the agent to stay within user-defined scope and not generate self-contained Q&A loops.
- **Why it matters:** Direct fix for #3275; prompt architecture change to enforce behavioral guardrails.

### 4. [#3283 — Fix: Plan/Agent Mode Toggle — `approval_mode` restore + auto‑execution guard](https://github.com/Hmbown/CodeWhale/pull/3283)
- **What it does:** Two fixes: (1) `approval_mode` is properly restored on Plan→Agent switch, (2) auto-execution is blocked until user confirms mode. Fixes #3279.
- **Why it matters:** Restores trust in mode semantics.

### 5. [#3286 — fix(tui): ensure `type:object` on Kimi parameters root for all schema shapes](https://github.com/Hmbown/CodeWhale/pull/3286)
- **What it does:** Replaces the narrow pattern match with a general schema walk that injects `type:object` on any root without it.
- **Why it matters:** Fixes #3281 — Kimi/Moonshot integration for complex schemas.

### 6. [#3285 — fix(tui): persist session before stall/cancel recovery so `--continue` keeps history](https://github.com/Hmbown/CodeWhale/pull/3285)
- **What it does:** Saves session state before stall recovery or cancellation, so `--continue` doesn't lose the in-progress turn.
- **Why it matters:** Fixes #2739 — critical for long-running tasks that stall.

### 7. [#3284 — perf(tui): debounce thinking-stream re-renders](https://github.com/Hmbown/CodeWhale/pull/3284)
- **What it does:** Throttles rendering of reasoning token deltas to avoid one-character-at-a-time display on fast models.
- **Why it matters:** Fixes #1620 — massive UX improvement for reasoning model users.

### 8. [#3280 — fix(auto): allow heuristic-only auto routing when flash router unavailable](https://github.com/Hmbown/CodeWhale/pull/3280)
- **What it does:** Falls back to heuristic routing when the flash router (DeepSeek API) is unavailable, instead of failing with "requires a DeepSeek API key".
- **Why it matters:** Enables `--model auto` for non-DeepSeek providers.

### 9. [#3278 — Replay EPIC-001 command boundary on Hunter](https://github.com/Hmbown/CodeWhale/pull/3278)
- **What it does:** Replays the command-boundary refactor (`UserCommandRegistry`, nested group-owned command tree) onto the `hunter/0.8.62-glm-subagents` branch.
- **Why it matters:** Keeps the Hunter experimental branch in sync with v0.9.0 foundation.

### 10. [#3239 — docs: add Atlas Cloud as OpenAI-compatible LLM backend](https://github.com/Hmbown/CodeWhale/pull/3239)
- **What it does:** Adds documentation for 59 Atlas Cloud models, provider logo, and `.env.example` snippet.
- **Why it matters:** Community-driven provider expansion, no code changes. Lowers onboarding friction for Atlas Cloud users.

---

## Feature Request Trends

1. **Chat-native workrooms & session persistence** — EPIC #3209 is the most ambitious feature direction. Multiple issues (#1530, #3209) demand non-interactive session continuity, shareable agent work, and mobile/web access. The community wants CodeWhale to become a platform, not just a terminal tool.

2. **Multi-agent orchestration with human oversight** — #2007 (migration runs for coordinated agents) and #3279 (mode toggle chaos) highlight a tension: users want multi-agent workflows, but they also want granular permission control and no autonomous execution. The demand is for **bounded parallelism with clear human-in-the-loop**.

3. **Config comment preservation** — #3282 is a small but frequently requested UX polish. Users rely on config file annotations for notes, temporary disablement, and team documentation.

4. **Provider-agnostic auto-routing** — #3280's fix (heuristic fallback when flash router is unavailable) reflects a broader need: users want `--model auto` to work with any provider, not just DeepSeek's API.

5. **External memory & thread persistence** — EPIC #3209 mentions "external memory" and "subagents." Combined with #1530 (session continuity) and #2870 (command boundary refactor), the direction is toward persistent, shareable agent sessions with inspectable history.

---

## Developer Pain Points

1. **Binary rename migration broken** — Issue #2917 exposed that `deepseek update` leaves users with a broken binary after rename. Developers who installed via Cargo had no clear migration path. The fix exists but the trust damage is real.

2. **Config file comment erasure** — Issue #3282: every TUI config edit silently destroys user annotations. For developers managing complex configurations, this is a frustrating regression that wastes time.

3. **Mode semantics are unreliable** — #3279 shows that Plan/Agent mode toggles are broken in two directions: permissions don't restore, and auto-execution bypasses approval. This undermines confidence in any multi-mode workflow.

4. **Snapshots ignore user configuration** — #3292: `snapshots.enabled = false` is silently ignored for per-tool snapshots, filling disks with GBs of copied git repos. Configuration should be respected unconditionally.

5. **Agent scope creep (self-loops)** — #3275: the agent generates its own questions and answers, deviating from user intent. This regression from #3061 suggests the prompt architecture changes (constitution system) introduced behavioral instability that needs active discipline.

6. **Kimi/Moonshot integration incomplete** — #3281: the v0.8.61 fix was partial, leaving complex schemas broken. Third-party API compatibility continues to be a maintenance burden.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*