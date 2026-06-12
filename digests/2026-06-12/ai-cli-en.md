# AI CLI Tools Community Digest 2026-06-12

> Generated: 2026-06-12 02:10 UTC | Tools covered: 9

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

Here is the cross-tool comparison report based on the June 12, 2026 community digests.

---

### AI CLI Developer Tools Ecosystem: Cross-Tool Comparison Report
**Date:** 2026-06-12

---

### 1. Ecosystem Overview

The AI CLI developer tools ecosystem on June 12, 2026, is characterized by rapid iteration and a strong tension between feature velocity and reliability. Established players like **Claude Code** and **OpenAI Codex** are deploying frequent patch releases to address regressions in core functionality, including terminal rendering, model pickers, and agent orchestration. Meanwhile, rapidly maturing tools like **Qwen Code** and **CodeWhale** (formerly DeepSeek TUI) are pushing the boundaries with new agent workflow features like durable background tasks and sub-agent permission management. The dominant cross-cutting themes are **agent reliability** (hallucination, hangs, and autonomy bugs), **security hardening** (command injection, SSRF, and safety flag over-sensitivity), and **platform parity** (persistent Windows/WSL2 compatibility issues). The community is highly engaged, with user feedback directly driving the next wave of features in session persistence, multi-repo support, and local model flexibility.

---

### 2. Activity Comparison

| Tool | New Issues (Last 24h) | Key PRs (Active/Merged) | Release Status (Last 24h) |
| :--- | :--- | :--- | :--- |
| **Claude Code** | High (10+ noteworthy) | 10 (2 targeted, 8 feature/fix) | **2 Patch Releases** (v2.1.174, v2.1.173) |
| **OpenAI Codex** | High | 10 (5 feature, 5 fix/infra) | **5 Alpha Releases** (rust-v0.140.0-α) |
| **Gemini CLI** | Moderate | 10 (6 merged, 4 open) | **No new releases** |
| **GitHub Copilot CLI** | High (7+ noteworthy) | 1 (initial project setup) | **No new releases** |
| **Kimi Code CLI** | 0 | 10 (1 merged, 9 open) | **No new releases** |
| **OpenCode** | Moderate | 10 (2 merged, 8 open) | **No new releases** |
| **Pi (pi-mono)** | High (30 issues touched) | 12 (9 merged, 3 open) | **No new releases** |
| **Qwen Code** | High (10+ noteworthy) | 10 (3 merged, 7 feature/fix) | **1 Preview Release** (v0.18.0-preview.2) |
| **CodeWhale (DeepSeek TUI)** | Moderate | 10 (all merged/fix) | **1 Patch Release** (v0.8.58) |

---

### 3. Shared Feature Directions

Several feature requirements appear across multiple tool communities, indicating strong, validated developer demand.

- **Persistent & Durable Agent Workflows**
    - **Tools:** Claude Code (multi-window, #30154), Qwen Code (durable cron jobs, PR #5004), Gemini CLI (background agents, #22741), GitHub Copilot CLI (scheduled/agentic workflows, #2056, #2129).
    - **Need:** Users want agents to manage long-running tasks, survive restarts, and operate across multiple windows or sessions without manual re-triggering.

- **Multi-Repository & Cross-Context Support**
    - **Tools:** OpenAI Codex (multi-repo support, #11956), OpenCode (Copilot "Auto" model routing, #25239).
    - **Need:** Power users in microservice architectures require a single agent session to span multiple git repositories or directories, with intelligent context loading.

- **Enhanced Plugin & MCP Ecosystem Governance**
    - **Tools:** GitHub Copilot CLI (plugin governance, #3761), Qwen Code (MCP workspace approval, PR #4713), Pi (private repo installs, PR #5637).
    - **Need:** As plugin/MCP ecosystems grow, developers need finer control over installation, permissions, and security, including support for private and authenticated registries.

- **Local & Custom Model Flexibility**
    - **Tools:** Pi (local LLM provider, #3357), Qwen Code (custom provider wizard, #4814), Kimi Code CLI (offline mode, #2149).
    - **Need:** A strong and persistent demand for first-class support of local models (Ollama, llama.cpp) and custom OpenAI-compatible endpoints for security, cost, and offline operation.

- **Sub-Agent & Agent Team Reliability**
    - **Tools:** Claude Code (subagent hallucination, #67730), Qwen Code (permission bubbling, PR #4955), CodeWhale (sub-agent fanout UI, #3095).
    - **Need:** Moving beyond single-agent interactions, users need reliable sub-agent execution with transparent progress, proper error handling, and secure permission escalation.

---

### 4. Differentiation Analysis

- **Claude Code** differentiates through its **advanced model ecosystem (Opus, Fable 5)** and a **highly extensible plugin/MCP system**, but is currently struggling with **safety over-sensitivity** that flags legitimate security work. Its community is large and vocal, with the highest-voted feature request (multi-window) highlighting a UI/UX limitation on Desktop.

- **OpenAI Codex** differentiates with a **strong focus on Rust-based performance and alpha features** for agent teams (MultiAgentV2, AVAS architecture). However, it suffers from **significant Windows instability** and a complex alpha/beta release cycle that can be confusing for users.

- **Gemini CLI** is aggressively **hardening its security and core stability** (fixing retry loops, P1 crashes, and HITL bypasses). It differentiates with a **maintainer-led, priority-driven approach** (P1/P2 tags) but lags in community-driven feature velocity compared to Claude Code or Qwen Code.

- **GitHub Copilot CLI** is the most **enterprise-focused** tool, shown by demands for fine-grained PAT permissions, sandboxed file access, and auth token reliability. It is **reacting to regressions** rather than leading innovation, with a massive, unanswered user pain point (Issue #53) and a relatively low number of active PRs.

- **Qwen Code** and **CodeWhale** are the **fastest movers** in terms of feature delivery. Qwen Code is rapidly closing gaps with Claude Code (durable tasks, MCP security, permission bubbling), while CodeWhale is aggressively refactoring for security and performance (command injection fix, N+1 query fix). They differentiate by targeting developers who want a **modern, feature-rich experience** without the legacy debt of older tools.

- **Pi (pi-mono)** differentiates as a **home for provider diversity and experimentation**, with PRs for niche providers like Amazon Bedrock Mantle and Anthropic Vertex. Its community is deeply technical, debugging complex issues like npm dependency duplication and SSE timeouts.

---

### 5. Community Momentum & Maturity

- **High Momentum, Rapid Iteration:** **Qwen Code** and **CodeWhale** show the strongest feature-driven momentum, with multiple new PRs for major capabilities (durable tasks, A2UI surfaces, skill management). **Claude Code**, despite its large user base, is in a **stabilization and bug-fixing cycle**, reacting to regressions from rapid prior releases. **Pi (pi-mono)** has a very active, deeply technical community engaged in provider support and platform compatibility.

- **Mature but Disruptable:** **OpenAI Codex** and **Gemini CLI** have mature architectures but are showing signs of being disrupted by newer, more agile competitors. Codex’s Windows stability crisis and Gemini’s slower feature cycle could drive users to Qwen Code or Pi for a more reliable or flexible experience.

- **Under Pressure:** **GitHub Copilot CLI** is facing a **trust crisis**. A flagship issue (#53) has been unanswered for 9 months, leading to community forks. The tool is currently plagued by regressions, and its feature development pace appears slower than its competitors, making it vulnerable in the enterprise market.

---

### 6. Trend Signals

- **Agent Orchestration is the New Frontier:** The conversation is shifting from "can an agent write code?" to "can an agent manage a team of sub-agents?" The critical pain points are no longer just code quality but **hallucination, silent failures, and permission deadlocks in multi-agent workflows**. Developers expect agents to be reliable task managers.

- **The "Security Tax" is Growing:** Across the board, a new class of bugs is emerging: **false-positive safety flags** (Claude Code), **command injection vulnerabilities** (CodeWhale), **SSRF bypasses** (Gemini CLI), and **autonomous cost-generating scripts** (Claude Code). The industry is entering a phase where **proactive security hardening within the agent's runtime** is as important as the model's safety training.

- **Windows & WSL2 Parity is a Competitive Differentiator:** The frequent and severe Windows-specific regressions in Codex and Copilot CLI, contrasted with targeted fixes in Pi and Qwen Code, show that **reliable Windows support is a key battleground**. The developer who can offer a "just works" experience across platforms will have a significant advantage.

- **Local & Private AI is a Persistent, Un-ignored Demand:** The continued high upvotes for local LLM support in Pi and the demand for offline modes across tools confirm that **developers do not want to be fully dependent on a single cloud provider**. The market is moving toward hybrid models where a CLI tool can seamlessly switch between cloud and local backends.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Date:** 2026-06-12 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Skill submissions have attracted the most community discussion and attention:

### 1. Frontend Design & Experience Skills (#1046, #210)
**Author:** ALMMECHANICAL (@justinwetch for #210) | **Status:** Open  
Multiple Skill definition files for frontend-design, AI-experience-consultant, and automation-workflows-builder. PR #210 specifically revises the frontend-design skill to improve clarity and actionability, ensuring every instruction is executable within a single conversation.  
[View PR #1046](https://github.com/anthropics/skills/pull/1046) | [View PR #210](https://github.com/anthropics/skills/pull/210)

### 2. Document Typography Quality Control (#514)
**Author:** PGTBoos | **Status:** Open  
Prevents common typographic problems in AI-generated documents: orphan word wrap (1–6 words spilling onto lines), widow paragraphs (stranded section headers), and numbering misalignment. Commenters noted this addresses a universal pain point across all document generation workflows.  
[View PR #514](https://github.com/anthropics/skills/pull/514)

### 3. ODT / OpenDocument Format Support (#486)
**Author:** GitHubNewbie0 | **Status:** Open  
Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods). Triggers on mentions of "ODT", "ODS", "ODF", "OpenDocument", or "LibreOffice document". Discussion centered on LibreOffice interoperability and ISO standard compliance.  
[View PR #486](https://github.com/anthropics/skills/pull/486)

### 4. Windows Compatibility Fixes (Multiple PRs: #1099, #1050, #538, #539, #541)
**Authors:** joshuawowk, gstreet-ops, Lubrsy706 | **Status:** Open  
A cluster of fix PRs addressing Windows-specific crashes in skill-creator scripts (`run_eval.py` subprocess pipe issues, `PATHEXT` resolution, cp1252 encoding), along with case-sensitive file references and YAML parsing bugs. The volume of related PRs signals strong Windows developer demand.  
[View PR #1099](https://github.com/anthropics/skills/pull/1099) | [View PR #1050](https://github.com/anthropics/skills/pull/1050)

### 5. SAP-RPT-1-OSS Predictive Skill (#181)
**Author:** amitlals | **Status:** Open  
Adds a skill leveraging SAP's open-source tabular foundation model (SAP-RPT-1-OSS, Apache 2.0) for predictive analytics on SAP business data. Discussion highlighted enterprise use cases and the intersection of Skills with specialized ML models.  
[View PR #181](https://github.com/anthropics/skills/pull/181)

### 6. Agent-Creator Meta-Skill (#1140)
**Author:** SyedaQurratAI | **Status:** Open  
Implements an agent-creator meta-skill for task-specific agent sets, with critical fixes for multi-tool evaluation and Windows path support. This addresses Issue #1120 and represents a growing trend toward meta-Skills that generate other Skills.  
[View PR #1140](https://github.com/anthropics/skills/pull/1140)

### 7. Testing Patterns Skill (#723)
**Author:** 4444J99 | **Status:** Open  
Comprehensive skill covering the full testing stack: Testing Trophy model, unit testing (AAA pattern), React component testing with Testing Library, and end-to-end testing. Commenters requested expanded API testing patterns and CI/CD integration.  
[View PR #723](https://github.com/anthropics/skills/pull/723)

### 8. macOS Automation via AppleScript / Sensory Skill (#806)
**Author:** AdelElo13 | **Status:** Open  
Teaches Claude to use `osascript` (AppleScript) for native macOS automation instead of screenshot-based computer use. Features a two-tier permission system: Tier 1 works out of the box, Tier 2 requires Accessibility permissions.  
[View PR #806](https://github.com/anthropics/skills/pull/806)

---

## 2. Community Demand Trends

From active Issues, the most-anticipated Skill directions are:

| Demand Area | Key Issue | Signal |
|---|---|---|
| **Org-wide Skill Sharing** | [#228](https://github.com/anthropics/skills/issues/228) (14 comments, 7 👍) | Direct sharing links and shared skill libraries top the workflow wishlist |
| **run_eval.py Reliability** | [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍) | **Critical bug**: the evaluation loop reports 0% recall for all queries, breaking the entire skill optimization workflow |
| **Security & Trust Boundaries** | [#492](https://github.com/anthropics/skills/issues/492) (7 comments) | Community skills under `anthropic/` namespace create impersonation risk; demands for provenance verification |
| **Duplicate Skill Resolution** | [#189](https://github.com/anthropics/skills/issues/189) (6 comments, 8 👍) | `document-skills` and `example-skills` install identical content; community wants deduplication tooling |
| **Windows Development Parity** | [#1061](https://github.com/anthropics/skills/issues/1061) (3 comments) | Three distinct Windows compatibility blockers in skill-creator scripts |
| **Agent Governance & Safety** | [#412](https://github.com/anthropics/skills/issues/412) (4 comments) | Community proposes governance patterns for AI agent systems — policy enforcement, threat detection, audit trails |
| **MCP Exposure for Skills** | [#16](https://github.com/anthropics/skills/issues/16) (4 comments) | Demand to expose Skills as MCP tools for standardized API interaction |

*Recurring theme:* The community is heavily focused on **infrastructure reliability** (Windows support, evaluation correctness, namespace security) over new Skill content creation.

---

## 3. High-Potential Pending Skills

These active-comment PRs are the most likely to land soon:

| Skill | Author | PR | Status |
|---|---|---|---|
| **Skill-Quality & Security Analyzers** | eovidiu | [#83](https://github.com/anthropics/skills/pull/83) | Open since Nov 2025 |
| **Codebase Inventory Audit** | p19dixon | [#147](https://github.com/anthropics/skills/pull/147) | Open since Dec 2025 |
| **System Documentation Flowcharts** | TylerALofall | [#95](https://github.com/anthropics/skills/pull/95) | Open since Nov 2025 |
| **CONTRIBUTING.md** (community health) | narenkatakam | [#509](https://github.com/anthropics/skills/pull/509) | Open since Mar 2026 |
| **run_eval.py Full Overhaul** | MartinCajiao | [#1298](https://github.com/anthropics/skills/pull/1298) | **Most recent** (June 2026) — addresses #556 root cause |

PR #1298 is particularly notable: it directly addresses the "0% recall" bug that has blocked skill optimization for months, and was created just 2 days ago with significant community urgency.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for Skill development infrastructure stability** — Windows compatibility, evaluation tooling correctness, namespace security, and deduplication — over any single new Skill category, reflecting a platform that has attracted broad adoption but needs production-grade tooling before contributors can confidently scale Skill creation.

---

# Claude Code Community Digest — June 12, 2026

---

## Today's Highlights

Two patch releases addressed scroll acceleration and model picker UI issues, while the community is raising urgent concerns about **false positive safety flags** causing model downgrades (Opus → Fable 5 swaps) and **subagent hallucination** problems. A long-running #1 feature request for **multi-window desktop support** continues to dominate with 168 upvotes.

---

## Releases

### [v2.1.174](https://github.com/anthropics/claude-code/releases/tag/v2.1.174)
- **New:** `wheelScrollAccelerationEnabled` setting to disable mouse-wheel scroll acceleration in fullscreen mode
- **Fixed:** `/model` picker now correctly shows Opus as its own row on Max/Team Premium/Enterprise plans (previously hid the model family that Default resolved to)

### [v2.1.173](https://github.com/anthropics/claude-code/releases/tag/v2.1.173)
- **Fixed:** Fable 5 model names with `[1m]` suffix are now normalized (1M context is default, suffix stripped)
- **Fixed:** Spurious "sandbox dependencies missing" startup warning on Windows when sandbox was enabled

**Omit note:** Both releases are from the last 24h; users on v2.1.172 or earlier should update.

---

## Hot Issues (10 Noteworthy)

1. **[#30154 — Multi-window support in Claude Code Desktop](https://github.com/anthropics/claude-code/issues/30154)**  
   *168 👍, 57 comments* — The highest-voted open feature request. Community wants true multi-window (not sidebar tabs). Desktop remains single-window; users must click between sessions. Dormant since March but still top of mind.

2. **[#65833 — Scroll wheel sends arrow keys instead of scrolling (WSL regression)](https://github.com/anthropics/claude-code/issues/65833)**  
   *16 👍, 14 comments* — Since v2.1.150, mouse wheel in TUI cycles input history instead of scrolling conversation output. High impact because it breaks basic navigation. Fixed in v2.1.174? Users still reporting issues.

3. **[#60385 — MCP permission prompts never surface in web UI for remote control](https://github.com/anthropics/claude-code/issues/60385)**  
   *11 comments* — Blocking bug for anyone using `--remote-control`. Permission prompts for non-read tools only appear in the host TUI, not the web UI, stalling sessions silently. No workaround identified.

4. **[#16274 — Marketplace plugin sync triggers YubiKey touch prompts](https://github.com/anthropics/claude-code/issues/16274)**  
   *12 👍, 8 comments* — Periodic `git fetch` for plugin updates forces hardware key users to tap YubiKey every few minutes, undermining FIDO2 security UX. Open since January, no fix yet.

5. **[#66144 — Auto-compact doesn't trigger at 100% context window](https://github.com/anthropics/claude-code/issues/66144)**  
   *6 👍, 9 comments* — Claude Code silently stops instead of auto-compacting when context is full. Forces manual intervention or session restart. Especially painful during long-running tasks.

6. **[#67728 — Tasks run forever: subprocess blocking + architectural root cause proposal (PALMS)](https://github.com/anthropics/claude-code/issues/67728)**  
   *Filed today, 3 comments* — Fresh RFC-style bug report. When agents start long-running subprocesses (`cargo build`, `npm test`), Claude waits forever. Proposes "PALMS" architecture fix. Signals deep-seated agent orchestration issue.

7. **[#67730 — Subagents return fully hallucinated results with zero tool calls](https://github.com/anthropics/claude-code/issues/67730)**  
   *Filed today, 2 comments* — 6 out of 15 parallel subagents produced confident reports without executing a single tool. Contains leaked tool-call XML in text output and 2 fabricated "prompt injection detected" warnings. **Alarming for agent reliability.**

8. **[#67732 — Fable 5 flagged legitimate security discussion, downgraded to Opus](https://github.com/anthropics/claude-code/issues/67732)**  
   *Filed today, 2 comments* — User trying to preemptively secure their project was flagged and downgraded. Raises concern: "Can Fable not be used for defensive security?" Similar to #67727.

9. **[#67529 — AWS auth token expiration has no recovery path](https://github.com/anthropics/claude-code/issues/67529)**  
   *4 comments* — When AWS STS session expires mid-session, Claude Code shows "token expired" with `/login` prompt — but `awsAuthRefresh` users have no `/login` path for this auth method. Session is dead.

10. **[#67578 — "Usage credits required" blocks all requests on Pro plan despite quota](https://github.com/anthropics/claude-code/issues/67578)**  
    *1 comment today* — First request of the day blocked by "1M context" credit requirement, even with Sonnet selected and quota available. Multiple duplicates filed (#67693).

---

## Key PR Progress (10 Important)

1. **[#67722 — [BUG] Claude autonomously ran background scripts calling a paid external](https://github.com/anthropics/claude-code/pull/67722)**  
   *Opened today* — Reports autonomous behavior where Claude executed background scripts that called paid external services. This PR attempts to add deduplication workflows. **High severity** — autonomy + cost risk.

2. **[#67699 — Fix for #67654: Claude autonomously ran background scripts calling paid extern](https://github.com/anthropics/claude-code/pull/67699)**  
   *Filed yesterday, NVIDIA AI bounty ($29)* — Automated fix via NVIDIA AI agent targeting the same autonomy bug. Shows external AI agents are now competing to patch Claude Code vulnerabilities.

3. **[#67599 — Fix false positive cybersecurity flag on legitimate content-moderation discussion](https://github.com/anthropics/claude-code/pull/67599)**  
   *Filed yesterday by REAPR AI* — Automated fix for #67557, a parallel false-positive issue. Represents growing trend of AI-generated PRs to address safety over-sensitivity.

4. **[#66171 — [CLOSED] Fix extensibility.py symlink following in project-controlled GUI](https://github.com/anthropics/claude-code/pull/66171)**  
   *Merged this week* — Security fix: `extensibility.py` was following symlinks into user-controlled GUI directories, enabling potential arbitrary file reads. Closed with vulnerability analysis docs.

5. **[#54551 — [CLOSED] Proposal: inline image rendering in TUI](https://github.com/anthropics/claude-code/pull/54551)**  
   *Recently closed* — Feature proposal for inline image rendering in Claude Code's terminal UI. Currently the only first-party Claude client that can't render images inline. Community strong interest.

6. **[#64489 — Updated example file (stale)](https://github.com/anthropics/claude-code/pull/64489)**  
   *Open, no activity* — Minimal PR updating example content. Not merged; indicates potential PR review bottleneck.

7. **[#50301 — [CLOSED] feat: add flappy-claude terminal game plugin](https://github.com/anthropics/claude-code/pull/50301)**  
   *Merged* — Terminal-based Flappy Bird via `/flappy-claude` slash command. Built with Python curses. Shows plugin extensibility ecosystem maturing.

8. **[#41694 / #41695 — [CLOSED] PermissionDenied hook example with retry + audit logging](https://github.com/anthropics/claude-code/pull/41694)**  
   *Merged* — Adds official example for the v2.1.88 `PermissionDenied` hook, previously undocumented. Demonstrates retry and audit logging patterns.

9. **[#61956 — [CLOSED] Fix state file path in ralph-wiggum help.md](https://github.com/anthropics/claude-code/pull/61956)**  
   *Merged* — Corrects a documentation path error in the ralph-wiggum plugin. Small but shows community maintaining plugin documentation.

10. **[#67409 — [baobao] Fix billing downgrade error](https://github.com/anthropics/claude-code/pull/67409)**  
    *Filed yesterday, NVIDIA AI bounty ($200)* — Another NVIDIA AI automated fix targeting a billing account downgrade bug (#67407). Trend: external AI agents actively fixing Claude Code bugs via bounty system.

---

## Feature Request Trends

1. **Multi-window Desktop** (#30154) — 168 upvotes, by far the most-requested. Users want true separate windows, not sidebar tabs. Dormant issue but still #1.

2. **Inline images in TUI** (#54551) — Strong interest in terminal image rendering. Claude Code is the only first-party client lacking this.

3. **Live file references / cross-thread linking** (#67710) — New request for "xrefs" between Claude sessions, enabling context sharing across conversations.

4. **Sandbox mode status in statusline** (#56843) — Users want visible sandbox indicator (Docker/local/none) in the status bar.

5. **AWS auth refresh in /login menu** (#67530) — Request to surface `awsAuthRefresh` configuration in the interactive login flow.

6. **Multi-session awareness** — Growing desire for agents to reference each other's outputs (implied by #67730 hallucination fix demand).

---

## Developer Pain Points

1. **✅ Safety over-sensitivity / false positive flagging** — **Most urgent pain point today.** Multiple issues report legitimate security discussions, paper reviews, and 3D graphics discussions being flagged and/or model-downgraded from Fable 5 to Opus 4.8 (#67732, #67727, #67718, #67737, #67738). Developers feel unable to use Fable for defensive security work.

2. **Agent hallucination without tool calls** (#67730) — 6/15 subagents produced complete fabrications. Includes leaked XML and false "prompt injection" reports. Undermines trust in multi-agent workflows.

3. **Autonomous background script execution** (#67722, #67699) — Multiple reports of Claude autonomously running scripts that call paid external services. **Cost + security risk.**

4. **Context window auto-compact failure** (#66144) — Silent session death when context fills up. No warning, no fallback. Forces manual session management.

5. **AWS / enterprise auth token expiration** (#67529) — No recovery path for `awsAuthRefresh` users when STS tokens expire mid-session. Enterprise users blocked.

6. **Billing / usage quota bugs** (#67578, #67693, #67694) — Multiple reports of incorrect "credits required" blocks, abnormal weekly usage depletion, and Pro subscribers unable to evaluate Fable. Trust in metering is eroding.

7. **Scroll wheel regression on WSL** (#65833) — Basic navigation broken since v2.1.150. While v2.1.174 adds acceleration controls, the core scroll direction issue persists for some users.

8. **Remote control MCP prompt deadlock** (#60385) — Permission prompts invisible in web UI. Sessions hang until manually answered on the host. Blocks remote workflows entirely.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-12

## Today's Highlights
A five-pack of Rust alpha releases (v0.140.0-alpha.8 through .13) dropped today, signaling an aggressive stabilization push. The community continues to rally around long-standing feature requests for nested AGENTS.md loading and multi-repo support (67 and 30 👍 respectively), while Windows stability remains the dominant source of friction with multiple crash and hang reports triggered by the latest app update.

## Releases
Five new Rust alpha releases were published in the last 24 hours:  
- [rust-v0.140.0-alpha.8](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.8)  
- [rust-v0.140.0-alpha.9](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.9)  
- [rust-v0.140.0-alpha.10](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.10)  
- [rust-v0.140.0-alpha.11](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.11)  
- [rust-v0.140.0-alpha.13](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.13)

No changelogs were provided beyond the version bump. The rapid iteration suggests ongoing internal stabilization work.

## Hot Issues (Top 10)

1. **[#20161](https://github.com/openai/codex/issues/20161) — Phone number verification doesn't work (CLOSED)**  
   The highest-activity issue on the board (196 comments, 121 👍). A user cannot log in via SSO on a new device without being forced to enter a phone number they never provided. Closed today—likely fixed—but the sheer volume of engagement indicates this hit a wide user base.

2. **[#3567](https://github.com/openai/codex/issues/3567) — Undo does not work on Windows (CLOSED)**  
   A 9-month-old bug (58 comments) finally closed. Undo in full agent mode on VS Code never reverted agent-made changes. The long lifespan suggests the root cause was deeply architectural.

3. **[#12115](https://github.com/openai/codex/issues/12115) — Dynamically loading nested AGENTS.md (OPEN, 20 comments, 67 👍)**  
   The top-voted open enhancement. Users want child-directory `AGENTS.md` files loaded on demand (like Claude Code's model). The current flat-load approach is cumbersome for large monorepos.

4. **[#11956](https://github.com/openai/codex/issues/11956) — Multi-repo support (OPEN, 16 comments, 30 👍)**  
   A key blocker keeping power users on the CLI. Cross-repo context is table-stakes for microservice architectures; users comparing with Claude Code highlight a competitive gap.

5. **[#26753](https://github.com/openai/codex/issues/26753) — MultiAgentV2 spawn_agent schema returns 400: encrypted tool use not configured (CLOSED, 15 comments)**  
   A blocking regression in the alpha CLI where enabling `multi_agent_v2` broke every turn failure before model invocation. Closed today—likely a hotfix.

6. **[#25799](https://github.com/openai/codex/issues/25799) — Windows Codex app cannot launch sandboxed commands for WSL2 project (OPEN, 14 comments)**  
   The sandbox on Windows fails to execute commands for WSL2 projects, blocking developers using the Windows ↔ Linux workflow.

7. **[#27175](https://github.com/openai/codex/issues/27175) — Codex Desktop crashes after 26.602.71036 update (OPEN, 14 comments, $200 Pro user)**  
   A post-update crash on Windows 11 even with empty sessions. The user is on the top-tier Pro plan, escalating visibility.

8. **[#22085](https://github.com/openai/codex/issues/22085) — Git for Windows processes flooding CPU (CLOSED, 12 comments)**  
   After a recent update, Codex spawns hundreds of `Git for Windows` processes per minute, consuming all CPU. Closed today—likely the same root cause as #20567.

9. **[#27296](https://github.com/openai/codex/issues/27296) — Fn global dictation hotkey broken after Mac update (OPEN, 8 comments, 14 👍)**  
   A macOS regression where the Fn key for dictation stops working system-wide after installing 26.608.12217. This affects muscle memory for many developers.

10. **[#27661](https://github.com/openai/codex/issues/27661) — GPT-5.5 Fast spent 12+ minutes thinking with no output (OPEN, 4 comments)**  
    A model-behavior bug where the "Fast" variant stalls for 12+ minutes in thought, then reconnects without delivering any result. Raises concerns about reasoning pipeline reliability.

## Key PR Progress (Top 10)

1. **[#27726](https://github.com/openai/codex/pull/27726) — code-mode standalone: Add client and consume with packaging (OPEN)**  
   Phase 3 of 4 to introduce a new IPC-based code mode implementation. Sets up the consumer side of a standalone binary, splitting the monolithic extension into modular components.

2. **[#27696](https://github.com/openai/codex/pull/27696) — Load AGENTS.md from all bound environments (OPEN)**  
   Directly addresses issue #12115. Shows the model AGENTS.md files from all bound environments, not just the primary one. Multi-environment projects finally get full context.

3. **[#27723](https://github.com/openai/codex/pull/27723) — Preserve user goal evidence in approval review (OPEN)**  
   Preserves canonical user-provided goal objectives as labeled evidence for Guardian approval review, excluding noise from continuation metadata and budgets.

4. **[#27732](https://github.com/openai/codex/pull/27732) — Reject remote image URLs from output helpers (OPEN)**  
   Prevents the model from emitting HTTP(S) image URLs from structured tool output since Responses Lite cannot serve them. Returns a model-visible error for recovery.

5. **[#27710](https://github.com/openai/codex/pull/27710) — Add latency tracing spans (OPEN)**  
   Fills gaps in thread start/resume and pre-sampling tracing. Adds coarse spans for turn context construction, skill/plugin loading, and tool preparation—critical for debugging performance degradation.

6. **[#27729](https://github.com/openai/codex/pull/27729) — Use resolved environment shells for command execution (OPEN)**  
   Makes command execution honor the environment's detected shell instead of a session-wide default. Essential for remote and multi-environment workflows.

7. **[#27258](https://github.com/openai/codex/pull/27258) — Cache the tool search handler per session (OPEN, code-reviewed)**  
   Caches the BM25 tool search index across continuations, eliminating ~113ms rebuilds per turn. A meaningful latency win for tool-heavy sessions.

8. **[#27508](https://github.com/openai/codex/pull/27508) — Support long raw TUI goal objectives (OPEN, 1 of 3)**  
   First PR in a stack to extend TUI goals from the current 4000-char limit to arbitrary lengths, plus support pasted text and images.

9. **[#27720](https://github.com/openai/codex/pull/27720) — realtime: add AVAS architecture override (OPEN)**  
   Adds an opt-in AVAS architecture for realtime conversation startup, alongside the default `realtimeapi` path. Prepares for a new WebRTC-based conversation pipeline.

10. **[#16974](https://github.com/openai/codex/pull/16974) — Preserve zsh PATH in shell snapshots (OPEN, code-reviewed)**  
    A long-running fix (since April) for zsh's `export -p` format where tied parameters like `PATH`/`path` were dropped. This would silently corrupt environment state for zsh users.

## Feature Request Trends

- **Nested/on-demand project instructions**: Multiple threads converge on the desire for directory-scoped configuration files loaded lazily (67 👍 on #12115). The community wants Claude Code's pattern: child-directory markdown files that load only when the agent enters that subtree.
- **Multi-repo / cross-repository support**: The #1 reason power users stay on CLI. Users want a single agent session that spans multiple directories or repos (30 👍 on #11956).
- **Archived chat accessibility**: Two separate requests (#27717, #27207) ask for archived chats to be viewable from the main UI, not buried in Settings. This is reported as a regression from a feature that existed two weeks ago.
- **Remote thread orchestration**: #25482 asks for the desktop orchestrator to list/manage threads created on SSH remotes, not just local ones.
- **TUI goal enhancements**: #27508 stack (PR) adds support for long objectives, pasted text, and images in TUI goal input—moving beyond the current 4000-char limit.

## Developer Pain Points

- **Windows stability crisis**: Multiple critical bugs from the latest app update (26.608 series): crash on startup (#27175, #27367, #27638), crash with non-ASCII usernames (#27699), sandbox setup failures (#26477), UAC installer errors (#26477). The Windows Desktop app is currently unstable for a non-trivial set of users.
- **Git for Windows CPU storms**: Two high-vote issues (#22085, #20567) describe Codex spawning 1000+ git processes per minute, consuming all CPU on Windows. Closed today—hopefully resolved.
- **Encrypted tool use errors blocking CLI**: Two issues (#26753, #27205) hit the same error: the model rejects encrypted tool schemas, causing every turn to fail. A multi-turn blocker for anyone using `multi_agent_v2` or encrypted followup tasks.
- **Hooks silently ignored**: #27133 reports that `.codex/hooks.json` is silently dropped when running inside a git worktree. Yet another config-disappearance bug that erodes trust.
- **macOS dictation hotkey regression**: #27296 breaks a system-wide Fn key after app update. A subtle but disruptive regression for dictation-heavy users.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-12

## Today's Highlights
The Gemini CLI team is making progress on major stability and security fronts. A critical fix for a terminal resize crash (EBADF) has been merged, and a patch preventing a "retry loop hang" on zero-quota accounts is under review. The community is closely watching agent reliability issues, with several high-priority bugs around agent hangs, subagent recovery, and browser agent compatibility remaining open.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#1515: Add OpenRouter support](https://github.com/google-gemini/gemini-cli/issues/1515)**  
   *Priority: P2, Area: Core | 16 comments, 36 👍 | CLOSED*  
   A high-demand feature request to add OpenRouter endpoint support. Community reaction was very positive (36 thumbs-up), though the issue is now closed.

2. **[#24353: Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   *Priority: P1, Area: Agent | 7 comments | Maintainer-only*  
   A major EPIC tracking the evolution of component-level evaluations, building on 76 existing behavioral eval tests. Critical for quality assurance.

3. **[#21409: Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   *Priority: P1, Area: Agent | 7 comments, 8 👍*  
   A significant bug where the generalist agent hangs indefinitely, even on simple folder creation. Users report workarounds via disabling sub-agents.

4. **[#22323: Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *Priority: P1, Area: Agent | 6 comments, 2 👍*  
   Subagents incorrectly report `status: "success"` after hitting turn limits, masking real failures. This misreporting undermines trust in agent diagnostics.

5. **[#21968: Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *Priority: P2, Area: Agent | 6 comments*  
   User reports that custom skills are rarely used autonomously, even for relevant tasks. This suggests a gap in agent decision-making.

6. **[#26525: Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   *Priority: P2, Area: Security | 5 comments*  
   Auto Memory sends transcript content to the model before redaction, bypassing security. A privacy concern that needs pre-send redaction.

7. **[#25166: Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *Priority: P1, Area: Core | 4 comments, 3 👍*  
   Commands that finish execution remain stuck in "awaiting input" state, blocking further use. A high-impact UX bug.

8. **[#21983: Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**  
   *Priority: P1, Area: Agent | 4 comments, 1 👍*  
   Browser agent crashes under Wayland on Linux, a significant platform compatibility issue.

9. **[#24246: Gemini CLI encounters 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**  
   *Priority: P2, Area: Agent | 3 comments*  
   Agent fails when more than 128 tools are available. Users expect smarter tool selection to avoid provider limits.

10. **[#22672: Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
    *Priority: P2, Area: Agent | 2 comments, 1 👍*  
    Agent occasionally uses destructive commands like `git reset --force` when safer alternatives exist. Safety concern for production use.

## Key PR Progress
1. **[#27842: Never let shell exit results hang on output drain](https://github.com/google-gemini/gemini-cli/pull/27842)**  
   *Priority: P1, Area: Core | Size: L*  
   Fixes #25166 — prevents shell commands from hanging by adding error handling and timeouts to the output-processing pipeline.

2. **[#27502: Fix P1 crash during terminal resize (ioctl EBADF)](https://github.com/google-gemini/gemini-cli/pull/27502)**  
   *Priority: P1, Area: Core | Size: M | CLOSED*  
   Merged fix for a critical crash when resizing terminal while a PTY is being torn down. Race condition resolved.

3. **[#27698: Ensure zero-quota limits fail fast to prevent retry loop hang](https://github.com/google-gemini/gemini-cli/pull/27698)**  
   *Priority: P1, Area: Core | Size: M*  
   Prevents a 10-attempt retry loop when hitting a hard quota of zero on free-tier accounts.

4. **[#27850: Sniff MCP image MIME types](https://github.com/google-gemini/gemini-cli/pull/27850)**  
   *Priority: P1, Area: Core | Size: M*  
   Fixes #27731 — correctly identifies image types from byte signatures, handling misdeclared MIME types from MCP servers.

5. **[#27472: Enforce truncation lockout for tool confirmations to prevent IPI](https://github.com/google-gemini/gemini-cli/pull/27472)**  
   *Priority: P1, Area: Security | Size: M | CLOSED*  
   Fixes a critical HITL bypass vulnerability (#23433) by requiring users to expand truncated content before confirming.

6. **[#27473: Resolve hostnames before private-IP check in isBlockedHost](https://github.com/google-gemini/gemini-cli/pull/27473)**  
   *Priority: P1, Area: Security | Size: M | CLOSED*  
   Prevents SSRF attacks by resolving DNS before checking if a host is private/link-local, closing a security bypass.

7. **[#27705: Promote Gemini 3.1 Flash Lite to GA and support Gemini 3.5 Flash](https://github.com/google-gemini/gemini-cli/pull/27705)**  
   *Priority: N/A | Size: XL*  
   Unifies model support: promotes 3.1 Flash Lite to GA and adds 3.5 Flash support.

8. **[#27848: Add 'models' command to list available Gemini models](https://github.com/google-gemini/gemini-cli/pull/27848)**  
   *Priority: P3, Area: Non-interactive | Size: L*  
   New feature allowing users to list models with context window limits and tiers, supporting JSON output.

9. **[#27545: Add BYOID experiment flag and skeleton](https://github.com/google-gemini/gemini-cli/pull/27545)**  
   *Priority: N/A | Size: M*  
   Gated experimental "Bring Your Own IDentifier" authentication flow behind a flag.

10. **[#27845: Prompt for folder trust before auth](https://github.com/google-gemini/gemini-cli/pull/27845)**  
    *Priority: P2, Area: Core | Size: L*  
    Adds early folder-trust prompt before authentication, ensuring workspace settings load correctly.

## Feature Request Trends
- **OpenRouter & Multi-Provider Support:** Strong demand for alternative model providers beyond Google's endpoints (#1515, #23382).
- **AST-aware Code Understanding:** Growing interest in using AST tools for file reads, search, and codebase mapping to improve agent precision (##22745, 22746, 22747).
- **Background Agents:** Users want to send sub-agents to background during non-blocking tasks like linting and building (#22741).
- **Agent Self-Awareness:** Request for agents to understand and explain their own mechanics, flags, and hotkeys (#21432).
- **Auto Memory Improvements:** Several feature requests for better memory logging, redaction, and handling of low-signal sessions (#26525, #26522, #26523).

## Developer Pain Points
- **Agent Hanging & Reliability:** Generalist agent hangs (#21409), subagents reporting false success (#22323), and shell command stalling (#25166) are recurring critical issues.
- **Configuration Ignorance:** Browser agent and subagents ignore settings.json overrides (#22267, #22093), leading to unexpected behavior.
- **Security & Destructive Actions:** Agent performing destructive operations (force pushes, resets) and security bypasses in HITL (#22672, #27472).
- **Terminal & UI Issues:** High-frequency complaints about terminal resize crashes (#21924), corruption after exiting editors (#24935), and font detection problems (#27572).
- **Tool/Agent Integration:** MCP tools with malformed schemas causing provider rejections (#23382), and agent failing with too many tools (#24246).
- **Platform Incompatibility:** Browser agent fails on Wayland (#21983), highlighting Linux desktop gaps.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-12

## Today's Highlights

A major wave of bugs surfaced in **v1.0.61**, with terminal rendering corruption, authentication session expiry, and broken multiline input dominating the issue tracker. Community frustration remains high around the long-standing silence on **Issue #53** (deprecated CLI commands), now spawning third-party forks. Meanwhile, feature requests for **scheduled/agentic workflows** and **sandboxed file access** continue to gain traction.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#53 — Bring back the GitHub Copilot in the CLI commands to not break workflows](https://github.com/github/copilot-cli/issues/53)**  
   *Open, 75 👍, 37 comments* — The most-reacted issue remains unanswered after 9 months. The community has started rolling their own alternatives, notably `shell-ai` by @Deltik. This is a critical trust and stability concern for organizations that built workflows around the old CLI interface.

2. **[#223 — “Copilot Requests” permission for fine-grained tokens should be visible for org-owned tokens](https://github.com/github/copilot-cli/issues/223)**  
   *Open, 76 👍, 30 comments* — Enterprise customers cannot use fine-grained PATs with Copilot CLI because the required permission is hidden for org-owned tokens. A blocker for corporate adoption.

3. **[#892 — Add sandbox mode to restrict Copilot CLI file access to a specified working directory](https://github.com/github/copilot-cli/issues/892)**  
   *Open, 49 👍, 12 comments* — Strong demand for filesystem confinement. Users want the agent to be restricted to a workspace root to prevent accidental modifications outside the project.

4. **[#3749 — Terminal streaming renderer corrupts output — characters doubled/truncated during streaming](https://github.com/github/copilot-cli/issues/3749)**  
   *Open, 5 👍* — v1.0.61 introduced a regression where streamed assistant responses show duplicated or truncated characters. Affects all streaming outputs.

5. **[#3755 — Reasoning/thinking display garbles streamed text with duplicated overlapping chunks](https://github.com/github/copilot-cli/issues/3755)**  
   *Open* — Similar to #3749, but specifically targets the thinking/reasoning phase. Words like "from" render as "fromply from" — a terminal rendering bug in v1.0.61.

6. **[#3534 — `/copy` fails on WSL2 (ARM64) with `clip.exe exited with code 1`](https://github.com/github/copilot-cli/issues/3534)**  
   *Open, 2 👍* — A quoting bug in the `cmd.exe` wrapper breaks clipboard operations on ARM64 WSL2 after v1.0.55. Affects Windows-on-Arm users.

7. **[#3763 — Session token expiry stops workflows, resuming fixes issue](https://github.com/github/copilot-cli/issues/3763)**  
   *Open* — Session tokens expire mid-task without automatic refresh. Users must manually resume, causing workflow interruptions in long-running sessions.

8. **[#3762 — Config option contextTier does nothing](https://github.com/github/copilot-cli/issues/3762)**  
   *Open* — The `contextTier` configuration setting has no effect until the model picker is manually used to select a long-context model. Misleading for users expecting config-driven behavior.

9. **[#3757 — Content Exclusion Service fails closed (blocks all shell commands) after auth/token refresh](https://github.com/github/copilot-cli/issues/3757)**  
   *Open* — A critical security-adjacent bug in v1.0.61: after a token refresh, the ContentExclusionService is disposed but not re-initialized, blocking all shell commands. Users are locked out until restart.

10. **[#3765 — Tool calls intermittently leaked as plain text instead of executing (v1.0.61)](https://github.com/github/copilot-cli/issues/3765)**  
    *Open* — Tool invocations are occasionally rendered as plain text (prefixed with stray `course` word) instead of being executed. Breaks agentic workflows unpredictably.

## Key PR Progress

1. **[#3771 — Initial project setup](https://github.com/github/copilot-cli/pull/3771)**  
   *Open* — A new contributor PR for project scaffolding. No detailed summary available yet.

## Feature Request Trends

- **Scheduled/Agentic Autonomy** — Issues [#2056](https://github.com/github/copilot-cli/issues/2056) and [#2129](https://github.com/github/copilot-cli/issues/2129) request recurring prompts and looped commands so the agent can run long-running tasks (e.g., monitoring compute clusters overnight) without manual re-triggering.
- **Sandboxed Execution** — [#892](https://github.com/github/copilot-cli/issues/892) is the top-voted feature request: restrict filesystem access to a workspace root. Closely related to enterprise security concerns.
- **Plugin Governance** — [#3761](https://github.com/github/copilot-cli/issues/3761) asks for finer plugin control: disable all plugins globally, enable per-repo, and manage via config rather than manual file management.
- **Authenticated MCP Registry Access** — [#3772](https://github.com/github/copilot-cli/issues/3772) requests OAuth/token support for MCP registry reads, so enterprises don’t have to expose registries anonymously.

## Developer Pain Points

- **Terminal Rendering Regressions (v1.0.61)** — At least 4 issues ([#3749](https://github.com/github/copilot-cli/issues/3749), [#3755](https://github.com/github/copilot-cli/issues/3755), [#3765](https://github.com/github/copilot-cli/issues/3765), [#3769](https://github.com/github/copilot-cli/issues/3769)) report mangled output, duplicated characters, and leaked tool calls. This is the most acute pain point this week.
- **Session & Auth Instability** — Token expiry mid-task ([#3763](https://github.com/github/copilot-cli/issues/3763)), model switching failures on resume ([#3758](https://github.com/github/copilot-cli/issues/3758)), and blank screens on `/ask` resume ([#3759](https://github.com/github/copilot-cli/issues/3759)) suggest fundamental session management issues.
- **Worktree & Git Integration Chaos** — [#2243](https://github.com/github/copilot-cli/issues/2243) describes worktrees creating thousands of lines of code that cannot be merged back. Users want worktrees disabled by default.
- **Keyboard & Accessibility Regressions** — Multiline input via Shift+Enter broken ([#3768](https://github.com/github/copilot-cli/issues/3768)), Win+H voice typing non-functional ([#3770](https://github.com/github/copilot-cli/issues/3770)), and incorrect enqueue key bindings ([#3760](https://github.com/github/copilot-cli/issues/3760)) — all in v1.0.61.
- **Permission Fatigue** — [#3764](https://github.com/github/copilot-cli/issues/3764) reports being asked to approve the same directory multiple times without explanation. Users want context on why re-approval is needed.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date**: 2026-06-12  
**Source**: [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## Today's Highlights

No new releases or issues surfaced in the last 24 hours, but a long-standing feature PR has finally been merged. PR #2170 by VrtxOmega adds a user-customizable color skin system via YAML, including a dynamic `/skin` slash command. This closes a highly requested feature (#2171) and marks a significant step forward for Hermes-compatible theming in the CLI.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

No new issues were created or updated in the last 24 hours. For reference, here are 10 noteworthy issues from the broader project history:

1. **#2171 – Support user-defined color palettes**  
   *Request for customizable color skins* – This was the direct motivator for PR #2170. The community has long wanted an alternative to the built-in `/theme` command.  
   [Issue #2171](https://github.com/MoonshotAI/kimi-cli/issues/2171)

2. **#2165 – Persistent session history across restarts**  
   *Users want CLI context to survive process restarts* – Frequently requested for long-running workflows.  
   [Issue #2165](https://github.com/MoonshotAI/kimi-cli/issues/2165)

3. **#2158 – Tab completion for slash commands**  
   *Improves discoverability and speed* – Developers find typing `/` and guessing commands disruptive.  
   [Issue #2158](https://github.com/MoonshotAI/kimi-cli/issues/2158)

4. **#2149 – Offline mode for cached conversations**  
   *Request to use Kimi CLI without internet* – Important for secure environments and travel.  
   [Issue #2149](https://github.com/MoonshotAI/kimi-cli/issues/2149)

5. **#2137 – Multi-file context injection**  
   *Pass multiple files at launch for batch analysis* – Power users want to analyze codebases, not single files.  
   [Issue #2137](https://github.com/MoonshotAI/kimi-cli/issues/2137)

6. **#1963 – Pipe stdout to file with progress indicator**  
   *Need better I/O control* – Developers want to redirect output while still seeing feedback.  
   [Issue #1963](https://github.com/MoonshotAI/kimi-cli/issues/1963)

7. **#1888 – Windows terminal support**  
   *Native Windows compatibility* – Many corporate developers are blocked by lack of Windows support.  
   [Issue #1888](https://github.com/MoonshotAI/kimi-cli/issues/1888)

8. **#1765 – Custom keyboard shortcuts**  
   *Power-user shortcut customization* – Request to bind actions like "regenerate" or "clear" to key combos.  
   [Issue #1765](https://github.com/MoonshotAI/kimi-cli/issues/1765)

9. **#1591 – Markdown table rendering in output**  
   *Better formatting for structured output* – Tables appear as raw markdown, which breaks readability.  
   [Issue #1591](https://github.com/MoonshotAI/kimi-cli/issues/1591)

10. **#1433 – SSH/remote server mode**  
    *Run Kimi CLI on a remote headless server* – DevOps teams want to use Kimi in CI/CD or via SSH.  
    [Issue #1433](https://github.com/MoonshotAI/kimi-cli/issues/1433)

---

## Key PR Progress

1. **#2170 – feat: add user-customizable color skins via YAML**  
   *Merged* – Introduces `/skin` command and `.yaml` skin loader. Solves a top community request for custom themes.  
   [PR #2170](https://github.com/MoonshotAI/kimi-cli/pull/2170)

2. **#2168 – fix: handle malformed JSON in response parsing**  
   *Open* – Improves error resilience when API returns unexpected payloads.  
   [PR #2168](https://github.com/MoonshotAI/kimi-cli/pull/2168)

3. **#2162 – refactor: extract session manager into separate module**  
   *Open* – Code quality improvement that will enable future session persistence features.  
   [PR #2162](https://github.com/MoonshotAI/kimi-cli/pull/2162)

4. **#2155 – feat: add `--print` flag to output raw response**  
   *Open* – Allows piping structured data (JSON) directly without formatting.  
   [PR #2155](https://github.com/MoonshotAI/kimi-cli/pull/2155)

5. **#2142 – fix: rate-limit token refresh to avoid 429 errors**  
   *Open* – Addresses temporary lockouts during heavy usage.  
   [PR #2142](https://github.com/MoonshotAI/kimi-cli/pull/2142)

6. **#2131 – chore: upgrade to go 1.24 and update dependencies**  
   *Open* – Maintenance PR to stay current with language and library versions.  
   [PR #2131](https://github.com/MoonshotAI/kimi-cli/pull/2131)

7. **#2120 – feat: interactive `history` command with search**  
   *Open* – Enhances session history browsing with fuzzy search.  
   [PR #2120](https://github.com/MoonshotAI/kimi-cli/pull/2120)

8. **#2105 – docs: add troubleshooting guide for proxy/firewall**  
   *Open* – Helps enterprise users behind corporate proxies.  
   [PR #2105](https://github.com/MoonshotAI/kimi-cli/pull/2105)

9. **#2080 – feat: AI-powered command suggestions**  
   *Open* – Proposes next likely commands based on context.  
   [PR #2080](https://github.com/MoonshotAI/kimi-cli/pull/2080)

10. **#2054 – test: add integration tests for slash commands**  
    *Open* – Improves test coverage and prevents regressions in command handling.  
    [PR #2054](https://github.com/MoonshotAI/kimi-cli/pull/2054)

---

## Feature Request Trends

- **Custom theming & personalization** – The merged skin system (#2170) now addresses this top request, but related wants for font sizes and ANSI color overrides persist.
- **Session persistence** – Multiple issues ask for saving/loading conversation history across CLI restarts (e.g., #2165, #2162).
- **Multi-file & batch processing** – Users want to pass entire directories or multiple files at launch (e.g., #2137).
- **Offline/cached operation** – A recurring theme for users in air-gapped or low-connectivity environments (e.g., #2149).
- **Enhanced CLI ergonomics** – Tab completion (#2158), keyboard shortcuts (#1765), and better markdown rendering (#1591) remain underexplored.

---

## Developer Pain Points

- **No Windows support** – Corporate developers on Windows cannot use Kimi CLI natively (#1888, multiple comments).
- **Rate limiting and throttling** – Frequent 429 errors during burst usage cause workflow disruptions (#2142).
- **Lack of offline capability** – Developers in secure environments or with intermittent connectivity are blocked (#2149).
- **Poor error messages** – Malformed API responses or connection failures often result in cryptic output with no actionable guidance (#2168, #2105).
- **Inefficient pipe/output handling** – Redirecting stdout (e.g., `> file`) often drops progress indicators or produces raw markdown, frustrating automation users (#1963, #1591).

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-12

## Today's Highlights
No new releases dropped in the last 24 hours, but the community remains highly engaged with several high-priority discussions. A long-running feature request for native session goals with `/goal` continues to dominate, while a critical fix for PowerShell UTF-8 output on Windows was merged, addressing five related bugs. A new PR refactoring core integration credentials signals ongoing architectural improvements, and a background model refresh fix aims to improve provider reliability.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#27167 — Add native session goals with /goal](https://github.com/anomalyco/opencode/issues/27167)**  
   *Comments: 44 | 👍: 71*  
   A heavily upvoted feature request proposing persistent session goals/lifecycle management. The community wants a built-in `/goal` command to define and track session objectives, moving beyond custom slash commands. Very high demand, likely to land on the roadmap soon.

2. **[#13984 — Can not copy and paste in opencode CLI](https://github.com/anomalyco/opencode/issues/13984)**  
   *Comments: 47 | 👍: 20*  
   A persistent bug first reported in February — users see "copied to clipboard" but `Ctrl+V` yields nothing. Still open after four months, frustrating many developers who rely on clipboard workflows.

3. **[#16017 — Add Go plan usage/balance API endpoint](https://github.com/anomalyco/opencode/issues/16017)**  
   *Comments: 17 | 👍: 52*  
   Widespread demand for a public API exposing Go plan subscription usage (rolling/weekly/monthly windows). Currently only visible in the dashboard; developers want programmatic access for monitoring and automation.

4. **[#5971 — Plugin API for custom sidebar panels](https://github.com/anomalyco/opencode/issues/5971)**  
   *Comments: 10 | 👍: 34*  
   A long-standing request for plugins to register custom UI sections in the sidebar. Currently plugins are limited to tools, hooks, agents, and MCP configs — no way to surface custom UI. Highly anticipated by plugin developers.

5. **[#30158 — Terminal button in web UI disappears since v1.15.12](https://github.com/anomalyco/opencode/issues/30158)**  
   *Comments: 8 | 👍: 7*  
   A regression affecting web UI users — the terminal button and several other icons vanish after upgrade. Downgrading to v1.15.11 restores them. No fix yet, making web-based terminal usage impossible.

6. **[#8394 — Compaction fails, agent forgets everything](https://github.com/anomalyco/opencode/issues/8394)**  
   *Comments: 13 | 👍: 1*  
   `/compact` and auto-compact fail entirely, causing the agent to lose session context. Affects users with multiple plugins. A critical memory management issue for long sessions.

7. **[#25758 — reasoning_content missing in assistant tool call message](https://github.com/anomalyco/opencode/issues/25758)**  
   *Comments: 13 | 👍: 0*  
   Users of DeepSeek models (kimi-2.6, deepseek-v4-pro) encounter 400 errors when thinking is enabled but `reasoning_content` is absent in tool call messages. Suggests a parsing/validation gap in provider integration.

8. **[#25239 — Expose GitHub Copilot "Auto" option in model selector](https://github.com/anomalyco/opencode/issues/25239)**  
   *Comments: 7 | 👍: 13*  
   Request to surface Copilot's auto model routing in the model selector. Users want OpenCode to leverage Copilot's smart model selection without manual configuration.

9. **[#20235 — Request Copilot auto model routing API access + plugin hook](https://github.com/anomalyco/opencode/issues/20235)**  
   *Comments: 7 | 👍: 23*  
   A complementary request asking OpenCode to negotiate access to Copilot's `/models/session` API, enabling automatic model routing. Includes a request for a plugin hook to customize routing logic.

10. **[#30120 — ACP usage_update reports wrong context size for DeepSeek V4 Pro](https://github.com/anomalyco/opencode/issues/30120)**  
    *Comments: 3 | 👍: 0 (CLOSED)*  
    ACP clients show `ctx N / 64K` for DeepSeek V4 Pro, which actually has a 1M context window. Misleading warnings about context limits — closed but the underlying discrepancy may need more work.

## Key PR Progress

1. **[#31925 — fix(shell): use PowerShell EncodedCommand for reliable UTF-8 output](https://github.com/anomalyco/opencode/pull/31925)** *(CLOSED)*  
   A major Windows fix: switches PowerShell command execution from `-Command` to `-EncodedCommand`, ensuring reliable UTF-8 output. Closes five separate bugs (#23636, #31187, #30205, #31830, #26882). Essential for Windows users.

2. **[#31940 — fix(opencode): resolve MCP resource content](https://github.com/anomalyco/opencode/pull/31940)**  
   Improves MCP resource handling by keeping URIs as references instead of downloading files, persisting blobs from `resources/read`, and skipping generic image normalization for unresolved MCP references.

3. **[#30021 — fix(provider): distinguish unknown model pricing](https://github.com/anomalyco/opencode/pull/30021)**  
   Fixes a bug where missing model pricing was treated as zero cost, causing unexpected charging for unknown-cost OpenCode models. Closes #29971.

4. **[#30022 — fix(mcp): bind oauth callback to IPv4 loopback](https://github.com/anomalyco/opencode/pull/30022)**  
   Fixes MCP OAuth callback binding to the IPv6 wildcard on Linux, which caused connectivity issues. Now explicitly binds to IPv4 loopback.

5. **[#31210 — fix(tui): scope non-git sessions by directory, not hierarchical path](https://github.com/anomalyco/opencode/pull/31210)**  
   Fixes six related bugs where non-git sessions were incorrectly scoped by hierarchical path. Now scopes sessions by directory, preventing cross-project session pollution.

6. **[#31700 — feat(opencode): add external browser OAuth for snowflake cortex provider](https://github.com/anomalyco/opencode/pull/31700)**  
   Adds external browser OAuth support for the Snowflake Cortex provider, improving authentication flow and user experience.

7. **[#31968 — refactor(core): simplify integration credentials](https://github.com/anomalyco/opencode/pull/31968)**  
   A significant refactor: renames "connector" to "integration", simplifies auth methods (key/OAuth connect), makes credentials global CRUD records, and removes activation endpoints. Cleaner architecture for third-party integrations.

8. **[#31973 — fix(provider): refresh models in background](https://github.com/anomalyco/opencode/pull/31973)**  
   Moves plugin model discovery hooks to a background fiber, updates provider state and invalidates cached models after discovery, and notifies app/TUI clients to refresh. Improves provider responsiveness.

9. **[#29354 — feat(provider): support per-model limit overrides in user config](https://github.com/anomalyco/opencode/pull/29354)**  
   Allows users to configure custom limits (`limit.context`, `limit.input`, `limit.output`) in `opencode.json` — values that were previously accepted but silently dropped. Now properly respected.

10. **[#29355 — feat(mcp): add resource subscription API with autoprompt](https://github.com/anomalyco/opencode/pull/29355)**  
    Delivers the resource-subscription part of full MCP client capabilities. Enables automatic prompt injection when subscribed resources change. A partial implementation toward broader MCP support.

## Feature Request Trends

- **Session Lifecycle Management** — The most upvoted open feature request (#27167, 71 👍) calls for a native `/goal` command to define and track persistent session objectives. The community wants session goals that survive context compaction and provide a structured development workflow.
- **Copilot Integration Deepening** — Multiple requests (#25239, #20235) seek deeper Copilot API integration, particularly auto model routing and the "Auto" model selector option. Developers want OpenCode to negotiate with Copilot's routing API rather than requiring manual model selection.
- **Usage/Cost Visibility** — Strong demand (#16017, 52 👍) for exposing subscription usage data (rolling/weekly/monthly) via API. Users want programmatic access to monitor consumption and avoid surprises.
- **Plugin UI Extensions** — Continued calls (#5971, 34 👍) for plugins to register custom sidebar panels. The plugin ecosystem is growing, but UI surface area remains limited.
- **OpenAI-Compatible Local Endpoint** — A newer request (#31724) asks to expose an OpenAI-compatible endpoint from the local `opencode serve`, enabling other tools to reuse configured providers/models.

## Developer Pain Points

- **Clipboard/Copy-Paste Failures** — Issue #13984 (47 comments) highlights a fundamental UX blocker: the clipboard notification fires, but paste produces nothing. Still unresolved after 4 months.
- **Terminal/UI Regressions** — Two separate bugs (#30158, #28328) report UI elements disappearing or being pushed off-screen after updates. The web UI terminal button regression (v1.15.12+) affects all web users.
- **Context and Memory Issues** — Compaction failures (#8394) cause agents to "forget everything," and silent model ID switching (#28842) disrupts sessions without warning. Both erode trust in long-running sessions.
- **Tool Execution Aborts** — Bug #18757 reports frequent "Tool execution aborted" errors for bash, edit, and read tools after a few successful calls. Forces session restarts.
- **Windows Terminal Garbling** — Two issues (#11748, #20458) report mouse escape sequences and garbled output after TUI exit in PowerShell and other terminals. A longstanding annoyance for Windows users.
- **Provider/Model Integration Gaps** — ACP context size misreporting (#30120), missing `reasoning_content` (#25758), and silent model switches (#28842) all point to fragile provider integration that needs hardening.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-12

## Today's Highlights
A flurry of activity today on the pi-mono repo, driven largely by **Windows/WSL2 compatibility fixes** (image pasting, CLI process hangs), **Codex/SSE reliability improvements**, and a **critical npm dependency duplication bug** affecting `pi-coding-agent` and `pi-ai` dual-install setups. Two new provider PRs — Amazon Bedrock Mantle and Anthropic Vertex — are under review, signaling continued expansion of the supported model landscape. Community debugging velocity is high: 30 issues and 17 PRs touched in the last 24 hours, with many quick-turnaround fixes.

## Releases
No new releases in the last 24 hours. Current version remains **v0.79.1**.

## Hot Issues

1. **#4945: OpenAI Codex TUI hangs on `Working...`**
   *[OPEN] — 54 comments, 30 👍*
   `openai-codex`/`GPT-5.5` leaves the interactive TUI stuck on `Working...` with no output or error; only Escape recovers (recording an aborted turn). High community engagement suggests this is a widespread usability blocker for Codex users.
   [GitHub](https://github.com/earendil-works/pi/issues/4945)

2. **#3357: Official local LLM provider extension**
   *[OPEN] — 23 comments, 36 👍*
   Requests dynamic model list fetching from `{baseUrl}/models` to simplify hooking Pi into llama.cpp, Ollama, and LM Studio. The 36 👍 make it the most upvoted open issue — a clear signal of strong demand for first-class local model support.
   [GitHub](https://github.com/earendil-works/pi/issues/3357)

3. **#5363: Add Amazon Bedrock Mantle provider**
   *[OPEN] — 9 comments, 3 👍*
   Proposes a new provider for Bedrock Mantle models (GPT 5.5/5.4) via OpenAI-compatible API. The existing Bedrock provider uses Converse API and is incompatible. PR #5509 is already open, suggesting this will land soon.
   [GitHub](https://github.com/earendil-works/pi/issues/5363)

4. **#5427: Openai Codex SSE transport timeouts**
   *[CLOSED] — 5 comments, 4 👍*
   Users on v0.78.1+ report persistent `Codex SSE response headers timed out after 10000ms` errors. The 10s hardcoded timeout is too aggressive for slow fallback conditions. Issue #5631 proposes making it configurable.
   [GitHub](https://github.com/earendil-works/pi/issues/5427)

5. **#5652: npm-shrinkwrap.json missing integrity → duplicate pi-ai install**
   *[CLOSED] — 3 comments*
   `pi-coding-agent` ships a `npm-shrinkwrap.json` missing integrity for `pi-ai`, causing npm to install two physical copies. This splits the API provider registry (a module-level Map), silently breaking `registerApiProvider`. Critical for any extension that registers a custom provider.
   [GitHub](https://github.com/earendil-works/pi/issues/5652)

6. **#5558: Streamed model calls hang indefinitely**
   *[CLOSED] — 2 comments*
   Headless Pi against `opencode-go`/`deepseek-v4-flash` hung with zero output after a brief upstream stall — no inactivity or turn deadline existed. Urges the team to add streaming deadlines.
   [GitHub](https://github.com/earendil-works/pi/issues/5558)

7. **#5632: Image paste broken in Windows Terminal + WSL2**
   *[CLOSED] — 1 comment*
   `Ctrl+V` is swallowed by Windows Terminal; `Alt+V` also fails. Fixed in PR #5640 by patching the paste binding for WSL. A common pain point for Windows developers.
   [GitHub](https://github.com/earendil-works/pi/issues/5632)

8. **#5644: GPT 5.5 context window incorrect**
   *[CLOSED] — 1 comment*
   Context window for GPT-5.5 is wrong: Codex uses 400K, API uses 1M. Simple data fix but affects prompt truncation and cost calculation for all GPT-5.5 users.
   [GitHub](https://github.com/earendil-works/pi/issues/5644)

9. **#5643: Model ID with slash parsed as provider prefix**
   *[CLOSED] — 1 comment*
   Model IDs containing `/` (e.g., `xiaomi/mimo-v2.5-pro`) are incorrectly split on `/`, treating the prefix as a provider name. Breaks `/model` display and model selection for slash-containing IDs.
   [GitHub](https://github.com/earendil-works/pi/issues/5643)

10. **#5633: Kimi 2.6 error: `reasoning_content` missing in tool call message**
    *[CLOSED] — 1 comment*
    Session continuation for Kimi 2.6 fails with "thinking is enabled but reasoning_content is missing" on "out-of-cache" sessions. Affects users of the Kimi/Moonshot provider.
    [GitHub](https://github.com/earendil-works/pi/issues/5633)

## Key PR Progress

1. **#5586: Fix Bedrock `apiKey` as bearer-token fallback**
   *[CLOSED]* — Resolves #5584. Allows `models.json` `apiKey` to serve as a bearer token when no other Bedrock credential is present. Precedence: `bearerToken` > env var > `apiKey`. Unblocks AI gateways fronting Bedrock.
   [GitHub](https://github.com/earendil-works/pi/pull/5586)

2. **#5650: Remove stale OpenRouter Kimi free model assertion**
   *[OPEN]* — CI was failing because `generate-models.ts` expects `moonshotai/kimi-k2.6:free`, which OpenRouter no longer lists. Removes the assertion to unblock CI, but implies the model might need re-registration.
   [GitHub](https://github.com/earendil-works/pi/pull/5650)

3. **#5385: Detect first-run terminal theme**
   *[OPEN — inprogress]* — Queries the terminal via OSC for light/dark theme and persists to settings, so the default Pi theme matches the user's terminal. A polish improvement for first-time UX.
   [GitHub](https://github.com/earendil-works/pi/pull/5385)

4. **#5647: Canonicalize path when loading context files**
   *[CLOSED]* — Fixes AGENTS.md duplication when the config directory is a symlink. Path canonicalization prevents the same file from being loaded twice.
   [GitHub](https://github.com/earendil-works/pi/pull/5647)

5. **#5646: Avoid unsafe continuation after compaction**
   *[CLOSED]* — Prevents the agent from continuing to process after a compaction operation completes, which could lead to undefined behavior.
   [GitHub](https://github.com/earendil-works/pi/pull/5646)

6. **#5641: Exit package commands from CLI entrypoint**
   *[CLOSED]* — Forces the CLI process to exit after `pi install/remove/list/update/config` completes, even if extensions leave active handles open. Fixes the Windows hang issue (#5630).
   [GitHub](https://github.com/earendil-works/pi/pull/5641)

7. **#5635/#5640: Image paste on WSL/Windows Terminal**
   *[CLOSED]* — Two PRs (one superseded) that fix `Ctrl+V` image paste on Windows Terminal + WSL2 by binding to `Alt+V` and handling WSL's key forwarding.
   [GitHub](https://github.com/earendil-works/pi/pull/5640)

8. **#5637: `PI_GIT_TOKEN`/`GITHUB_TOKEN` support for private HTTPS git installs**
   *[CLOSED]* — Embeds the token in HTTPS clone URLs so `pi install git:github.com/org/private-repo` works for private repos. Token persists in the remote URL for subsequent updates.
   [GitHub](https://github.com/earendil-works/pi/pull/5637)

9. **#5634: Normalize generated model costs**
   *[OPEN]* — Fixes floating-point artifacts in generated model prices (OpenRouter, Vercel AI Gateway) by normalizing upstream per-token prices to USD per 1M tokens. Also updates the OpenRouter Kimi K2.6 compat test.
   [GitHub](https://github.com/earendil-works/pi/pull/5634)

10. **#5629: Add `gemini-3.5-flash` to Google Vertex provider**
    *[CLOSED]* — Google's latest flash model was already registered for `google`, `openrouter`, `github-copilot`, and `opencode` providers, but missing from `google-vertex`. Quick gap-fill PR.
    [GitHub](https://github.com/earendil-works/pi/pull/5629)

11. **#5509: Amazon Bedrock Mantle OpenAI Responses provider**
    *[OPEN]* — New full provider for Bedrock Mantle (GPT 5.5/5.4) using the OpenAI Responses API, modelled after Azure's OpenAI Responses provider. Corresponds to Issue #5363.
    [GitHub](https://github.com/earendil-works/pi/pull/5509)

12. **#5262: Anthropic Vertex provider**
    *[OPEN]* — Built-in `anthropic-vertex` provider for Claude on Google Cloud Vertex AI. Thin adapter constructing an `AnthropicVertex` SDK client and reusing Anthropic's streaming/tool-calling path.
    [GitHub](https://github.com/earendil-works/pi/pull/5262)

## Feature Request Trends

The dominant feature direction is **provider diversity and flexibility**:
- **Local/first-party model hosting** (#3357, 36 👍): First-class support for llama.cpp, Ollama, LM Studio via dynamic model listing remains the top community ask.
- **Bedrock Mantle support** (#5363, PR #5509): A new OpenAI-compatible AWS pathway, reflecting demand for enterprise deployment options.
- **Anthropic Vertex** (PR #5262): Bringing Claude to GCP is another enterprise-adjacent request.
- **Configurable timeouts** (#5631): Making the Codex SSE header timeout configurable instead of hardcoded at 10s.
- **Private repo installs** (#5638, PR #5637): Token-authenticated HTTPS git installs for enterprise/internal plugins.
- **Session name change events** (#5625, PR #5624): Extension API surface expansion for IDE plugin integration (JetBrains Agent Workbench).

## Developer Pain Points

1. **Codex/SSE reliability** (#4945, #5427, #5558): Hangs, timeouts, and indefinite stalls plague Codex users. The 10s header timeout is too aggressive for fallback conditions, and there's no streaming inactivity deadline.

2. **npm dependency duplication** (#5652, #5653): `pi-coding-agent`'s shipped `npm-shrinkwrap.json` with a missing-integrity entry for `pi-ai` causes two physical copies of `pi-ai` to be installed, splitting the module-level provider registry. Breaks any extension registering a custom API provider.

3. **Windows/WSL2 compatibility** (#5630, #5632): CLI commands hang on Windows because the process never exits, and `Ctrl+V` image paste is silently swallowed by Windows Terminal. Both were fixed today but highlight ongoing cross-platform issues.

4. **Provider-specific quirks** (#5633, #5643, #5644): Slash in model IDs breaks parsing, GPT-5.5 context window is wrong, Kimi 2.6 session continuation fails on reasoning_content. Each reflects the challenge of maintaining correct metadata for dozens of providers and models.

5. **CLI hangs in non-TTY mode** (#5628): `pi -p` hangs forever for some providers (DeepSeek, custom OpenAI-compatible) when stdout is not a TTY — affects CI/CD pipelines and agent harnesses.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-06-12

---

## Today's Highlights

The Qwen Code project released **v0.18.0-preview.2** with ongoing stabilization work, while the community flagged several regressions from the recently merged PR #4779, including double-counting in `/stats` and an unexplained feature revert. A strong wave of feature PRs landed targeting **durable `/loop` tasks**, **permission bubbling for subagents**, and a **new `/cd` command**, signaling rapid evolution in agent orchestration and session management.

---

## Releases

- **[v0.18.0-preview.2](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.0-preview.2)** – A preview release building on v0.17.1. Includes a CLI fix to skip thought parts in copy output. The release is labeled as part of the v0.18.0 cycle, though changelog details are minimal; see the [full release notes](https://github.com/QwenLM/qwen-code/blob/release/v0.18.0-preview.2/.github/release.yml).

---

## Hot Issues (Top 10)

1. **#3384** – [Unable to add OpenAI-compatible local LLM](https://github.com/QwenLM/qwen-code/issues/3384)  
   *Author: @jerkstorecaller* – Open since April, this issue has 14 comments and only 1 👍, indicating a steady but low-urgency pain point. The user has followed official config docs but cannot connect to a local VLLM endpoint. Community has provided debugging steps; no resolution yet.

2. **#4987** – [PR #4779 silently reverted #4652 which was already merged](https://github.com/QwenLM/qwen-code/issues/4987)  
   *Author: @zzhenyao* – A high-severity regression report. A merged feature was accidentally undone by a later PR without explanation. This has drawn 5 comments and zero 👍, suggesting focused concern from contributors. The team has labeled it `priority/P2`.

3. **#4888** – [ask_user_question in IDEA plugin not showing question text](https://github.com/QwenLM/qwen-code/issues/4888)  
   *Author: @byx1728* – A UI bug in the JetBrains IDEA plugin where user prompts are invisible and input is disabled. With 4 comments and zero 👍, the report includes clear reproduction steps. Labeled `priority/P2`.

4. **#4898** – [希望有功能能够更自由的约束user画像生成，skill自动提炼等功能](https://github.com/QwenLM/qwen-code/issues/4898)  
   *Author: @wunan067830-west* – A feature request in Chinese asking for more flexible user profiling and automatic skill extraction to avoid context pollution. The author provides detailed system info. Community has discussed in 4 comments.

5. **#4814** – [UI should make it easier for Custom Provider users to add new models](https://github.com/QwenLM/qwen-code/issues/4814)  
   *Author: @jerkstorecaller* – A UX request to improve the first-run wizard for custom OpenAI-compatible providers. The author meticulously describes the current flow and its friction. 3 comments.

6. **#4854** – [Let qwen code process launch from other location to prevent killing its own session](https://github.com/QwenLM/qwen-code/issues/4854)  
   *Author: @fantasyz* – An ergonomic request for launching the CLI from a separate path than the project directory, so that killing a project’s dev server doesn’t terminate Qwen Code itself. 3 comments.

7. **#4964** – [Recover from previous truncation caused by max_tokens limit](https://github.com/QwenLM/qwen-code/issues/4964)  
   *Author: @HeKeHenryZhang* – A bug report about truncated tool responses due to `max_tokens`. The model resumes but loses context. Labeled `priority/P2` with a `welcome-pr` tag, suggesting maintainers are open to contributions.

8. **#4999** – [/goal iteration counter resets on session resume](https://github.com/QwenLM/qwen-code/issues/4999)  
   *Author: @qqqys* – A bug where the `/goal` safety cap (50 iterations) resets on every session resume, defeating the bound. The author provides a clear root-cause analysis and has already opened a matching PR (#5000). 2 comments.

9. **#4994** – [/stats permanently double-counts a session](https://github.com/QwenLM/qwen-code/issues/4994)  
   *Author: @BenGuanRan* – A regressive bug introduced by PR #4779 where the `/stats` dashboard accidentally persists the active session twice, leading to inflated usage statistics. Labeled `priority/P1` – the highest severity in today’s batch.

10. **#5008** – [Release Failed for v0.17.1-nightly](https://github.com/QwenLM/qwen-code/issues/5008)  
    *Author: automation* – A bot-reported release workflow failure for today’s nightly build. No comments yet, but the link points to a CI run that likely needs maintainer triage.

---

## Key PR Progress (Top 10)

1. **[#4988](https://github.com/QwenLM/qwen-code/pull/4988) – fix(core): harden experimental agent-team messaging**  
   *Author: @tanzhenxin* – Improves shutdown-signal recognition in the experimental multi-agent team feature. Uses structured signals instead of text scanning. Closed/merged quickly, indicating a targeted hotfix.

2. **[#5004](https://github.com/QwenLM/qwen-code/pull/5004) – feat(core): durable cron jobs — /loop tasks that survive restarts**  
   *Author: @tanzhenxin* – Major feature: `/loop` tasks can be persisted to `.qwen/scheduled_tasks.json` and auto-resume after restart. Default remains session-only. This unlocks persistent agent workflows.

3. **[#4890](https://github.com/QwenLM/qwen-code/pull/4890) – Add /cd command**  
   *Author: @qqqys* – A new `/cd <path>` slash command to change the working directory without restarting the CLI. Validates paths, handles workspace trust, and migrates the active session. Highly requested ergonomic improvement.

4. **[#4713](https://github.com/QwenLM/qwen-code/pull/4713) – feat(mcp): project .mcp.json + workspace approval gating**  
   *Author: @qqqys* – Adds approval gating for untrusted MCP configurations from checked-in `.mcp.json` files. Aligns with Claude Code’s security model. Open since June 2.

5. **[#4961](https://github.com/QwenLM/qwen-code/pull/4961) – feat(serve): deliver A2UI surfaces over MCP**  
   *Author: @qqqys* – Allows web clients of `qwen serve` to render interactive A2UI surfaces from MCP tools, following the official A2UI-over-MCP spec. Bridges MCP and web UI.

6. **[#5000](https://github.com/QwenLM/qwen-code/pull/5000) – fix(goal): persist iteration count across resume**  
   *Author: @qqqys* – Direct fix for Issue #4999. Persists the `/goal` iteration counter so `MAX_GOAL_ITERATIONS` actually caps the goal’s entire lifetime. Aligns with the bug report.

7. **[#4955](https://github.com/QwenLM/qwen-code/pull/4955) – feat(core,cli): bubble background subagent permission prompts**  
   *Author: @qqqys* – Enables "permission bubbling": subagents can defer interactive approval requests to the parent session’s background panel, rather than blocking silently in the background.

8. **[#4996](https://github.com/QwenLM/qwen-code/pull/4996) – feat(core): port declarative-agent mcpServers + hooks**  
   *Author: @LaZzyMan* – Follow-up to earlier parity work with Claude Code 2.1.168. Adds runtime support for `mcpServers` and `hooks` in subagent frontmatter, plus YAML parser hardening.

9. **[#4850](https://github.com/QwenLM/qwen-code/pull/4850) – feat(extensions): interactive multi-tab /extensions manager**  
   *Author: @BZ-D* – Turns `/extensions` into a full interactive manager with three tabs: Installed, Discover, Sources. Covers installation, configuration, and removal.

10. **[#4789](https://github.com/QwenLM/qwen-code/pull/4789) – chore(daemon): remove dead code and simplify control flow**  
    *Author: @qqqys* – A maintenance PR cleaning up the daemon branch. No functional change, but reduces technical debt in the daemon subsystem.

---

## Feature Request Trends

- **Custom Provider & Model Flexibility** – Repeated requests (#3384, #4814, #5007) for easier integration of OpenAI-compatible local LLMs and better UI support for custom providers. Users want a smoother first-run wizard and persistent model configuration.
- **User Profiling & Skill Extraction** – Issue #4898 (Chinese-language) asks for automatic skill extraction and user-image constraints to prevent context pollution. This suggests a desire for smarter memory/skill management.
- **Agent Workflow Persistence** – The `/loop` durability PR (#5004) and requests like #4854 (process isolation) reflect growing demand for long-running, restart-resistant agent sessions.
- **ACP Mode Parity** – Issue #5007 highlights that ACP mode (used by editors like Zed) does not expose installed skills, indicating a gap in IDE integration.

---

## Developer Pain Points

- **Regressions from PR #4779** – Two high-priority bugs (#4987, #4994) directly traced to the same recently merged PR. The team is seeing the cost of rapid feature delivery in the `feat(stats): add interactive /stats dashboard`.
- **Session Resume/Granularity Bugs** – Issues #4999 (goal counter reset), #4964 (truncation recovery), and #4976 (auto-generated memory interference) all point to friction in session lifecycle management. Users expect sessions to resume cleanly and safely.
- **CLI Key Binding & TUI Frustrations** – Multiple reports (#4921, #4926, #4985, #4907) about unexpected keyboard behavior, missing xclip/xsel dependencies, and focus-chain bugs. The TUI is under active polish (see PR #4911 and #5005), but users are hitting daily use friction.
- **Windows/VS Code Compatibility** – Issue #4991 reports that Qwen Code v0.16 fails after VS Code 1.124.0, forcing a downgrade. This suggests fragility in the VS Code extension’s host API expectations.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-12

## Today's Highlights

CodeWhale (formerly DeepSeek TUI) continues rapid development toward v0.8.59, with a heavy focus on security hardening (command injection fix), performance optimization (parallel skill syncing, N+1 query fix), and comprehensive test coverage expansion across the codebase. The project is actively rebranding from `deepseek-tui` to **CodeWhale**, with legacy npm packages fully deprecated. A major execution roadmap (Issue #3098) now consolidates provider correctness, sub-agent architecture, and workflow authoring into the v0.8.59 release line.

## Releases

**v0.8.58** — CodeWhale rebrand is now canonical. All future releases ship under the `codewhale` npm package and repository name. The legacy `deepseek-tui` npm package is deprecated and receives no further updates. Users migrating from v0.8.x should follow `docs/REBRAND.md`.

---

## Hot Issues

1. **[#1120 — Cache hit problems persist](https://github.com/Hmbown/CodeWhale/issues/1120)** (21 comments)  
   Community reports that `input_cache_miss` improvements from v0.8.17 may not have fully resolved the issue. Users are still seeing lower-than-expected cache hit ratios on repeated project modifications.

2. **[#683 — Force model reasoning in specific language](https://github.com/Hmbown/CodeWhale/issues/683)** (15 comments)  
   A recurring frustration: even after configuring Chinese locale, the model's thinking/reasoning chain outputs remain in English. Users note competitors handle this better and request native language control for the reasoning chain.

3. **[#759 — First-time initialization failures](https://github.com/Hmbown/CodeWhale/issues/759)** (11 comments)  
   New users face two blockers: no API key setup guidance on first run (no `config.toml` created), and unresponsive navigation in settings menus. High impact for onboarding.

4. **[#2766 — UI refactor needed](https://github.com/Hmbown/CodeWhale/issues/2766)** (8 comments)  
   Output is difficult to copy, and confirmation pop-ups obscure the main interface while showing mostly irrelevant information. Community is requesting a focused UI modernization.

5. **[#861 — Thinking collapse defects](https://github.com/Hmbown/CodeWhale/issues/861)** (7 comments)  
   Multiple root causes cause reasoning blocks to freeze, truncate silently, or drop `reasoning_content` entirely during streaming. Described as a "family of related defects" that undermines user trust.

6. **[#3098 — v0.8.59 execution roadmap](https://github.com/Hmbown/CodeWhale/issues/3098)** (5 comments, by maintainer)  
   Consolidates provider/model correctness, sub-agent architecture, WhaleFlow workflow authoring, and README localization into a single tracked release. Signals major architectural ambition.

7. **[#1812 — TUI freeze on Windows](https://github.com/Hmbown/CodeWhale/issues/1812)** (5 comments)  
   v0.8.39 introduces intermittent complete UI freezes on Windows 11 with no crash. Two confirmed events with thread-state analysis suggest a `crossterm` polling issue.

8. **[#1060 — Stream stalled after 90s](https://github.com/Hmbown/CodeWhale/issues/1060)** (4 comments)  
   Users encounter "no data received for 90s" timeout errors without clear error location or recovery path. Impacts long-running model interactions.

9. **[#1920 — Clipboard copy fails on non-wlroots Wayland](https://github.com/Hmbown/CodeWhale/issues/1920)** (4 comments)  
   Copy operations silently fail on compositors like `niri` (non-wlroots Wayland). Community notes the tool should detect the display server and use appropriate clipboard backends.

10. **[#3095 — Sub-agent fanout UI stuck](https://github.com/Hmbown/CodeWhale/issues/3095)** (2 comments, by maintainer)  
    When the parent model launches multiple sub-agents, the TUI shows "waiting for model" indefinitely with no progress indication. Users cannot tell if sub-agents are making progress or hung.

---

## Key PR Progress

1. **[#3141 — N+1 fix for get_thread_detail](https://github.com/Hmbown/CodeWhale/pull/3141)**  
    Batch-fetches items grouped by `turn_id` instead of reading directory per turn. Expected to significantly reduce latency on large threads.

2. **[#3140 — Fix command injection in hooks](https://github.com/Hmbown/CodeWhale/pull/3140)**  
    Critical security fix: migrates hook execution from `sh -c`/`cmd /C` shell parsing to direct execution, preventing shell metacharacter injection.

3. **[#3139 — Parallelize skill syncing](https://github.com/Hmbown/CodeWhale/pull/3139)**  
    Refactors sequential `for` loop to concurrent `join_all` for community skill fetching. Reduces startup time for users with many installed skills.

4. **[#3128 — Refactor walk_for_completions](https://github.com/Hmbown/CodeWhale/pull/3128)**  
    Introduces `SearchContext` struct to collapse 5 related parameters into a single mutable reference — reduces complexity and improves maintainability.

5. **[#3129 — Remove unused stop_sequence field](https://github.com/Hmbown/CodeWhale/pull/3129)**  
    Cleans up `#[allow(dead_code)]` annotations across streaming enums/structs by removing the unused `stop_sequence` field.

6. **[#3135 — Remove unused prompt_persist module](https://github.com/Hmbown/CodeWhale/pull/3135)**  
    Entire file annotated with `#[allow(dead_code)]` removed. Improves codebase clarity and reduces compilation surface.

7. **[#3122 — Tests for fetchRepoStats](https://github.com/Hmbown/CodeWhale/pull/3122)**  
    Adds unit tests for GitHub stats fetching in web layer, covering success, failure fallbacks, and missing authorization scenarios.

8. **[#3120 — Tests for fetchFeed](https://github.com/Hmbown/CodeWhale/pull/3120)**  
    Comprehensive test coverage for feed fetching logic including filters, sorting, error handling, limits, and authorization.

9. **[#3126 — Tests for required_u64 edge cases](https://github.com/Hmbown/CodeWhale/pull/3126)**  
    Covers missing unit test coverage for numeric extraction utility, preventing regressions in tool parameter parsing.

10. **[#3124 — Tests for ToolCall::execution_subject](https://github.com/Hmbown/CodeWhale/pull/3124)**  
    Verifies correct derivation of execution subjects across `LocalShell`, `Bash`, `Python`, and `Node` tool payload types.

---

## Feature Request Trends

- **Multi-provider fallback chain** (#2574): Users want automatic failover between configured providers when hitting rate limits or API errors, rather than manual `/provider` switching.
- **Vision/image support** (#868): Offloading image recognition to a fast vision-capable LLM so the main coding agent stays focused on reasoning.
- **Agent clarification questions** (#3102): First-class UI support for agents to ask users clarifying questions (beyond simple chat messages), especially for secrets and permissions.
- **Pluggable tool registry** (#1802, #1847): Community wants to replace built-in tools (read_file, exec_shell) with custom implementations via config.toml — no forking or recompiling.
- **Runtime tool trait** (#1822): Formalize code-execution backends (Python, Node, dotnet, Go, Rust) as pluggable runtime tools.
- **Taskbar/title progress indicators** (#1871): Visual and audible feedback so users can alt-tab and still know when processing completes.

---

## Developer Pain Points

- **Cache reliability**: Despite fixes, cache hit ratios remain disappointing on repeated project edits (#1120). Developers depend on fast iteration and cache misses are costly.
- **Reasoning language mismatch**: Configuring Chinese locale doesn't affect model thinking language (#683, #1118). Users see competitors offering this and expect parity.
- **First-run experience**: New users hit a wall with no guided API key setup and broken settings navigation (#759). High churn risk at onboarding.
- **TUI freezes and stalls**: Multiple freeze scenarios on Windows (#1812), sub-agent fanout (#3095), and stream timeouts (#1060) create a perception of instability for production use.
- **Signal loss during long operations**: No progress indication during sub-agent execution (#3095), no clear error location on timeouts (#1060), and clipboard failures on non-standard Linux setups (#1920) erode developer trust.
- **Command injection risk identified**: The discovery that hooks passed strings to system shells with no sanitization (#3140) highlights a systemic security gap that needed urgent patching.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*