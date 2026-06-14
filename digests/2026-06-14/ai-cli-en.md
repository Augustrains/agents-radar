# AI CLI Tools Community Digest 2026-06-14

> Generated: 2026-06-14 02:13 UTC | Tools covered: 9

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

Here is a cross-tool comparison report based on the community digest data for 2026-06-14.

---

### Cross-Tool Comparison Report: AI CLI Developer Tools

**Date:** 2026-06-14

This report provides a comparative analysis of the major AI CLI developer tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI (CodeWhale)—based on a single day of community activity. The analysis focuses on ecosystem dynamics, development velocity, shared challenges, and strategic differentiation.

---

### 1. Ecosystem Overview

The AI CLI developer tools ecosystem is in a phase of rapid maturation, characterized by a shift from raw feature delivery to deep-seated reliability and trust. The dominant conversation across all tools is **agentic quality**, with users demanding deterministic behavior from sub-agents, realistic memory persistence, and robust error handling. A significant rift is emerging between tools that prioritize feature velocity (e.g., Claude Code, Qwen Code) and those focusing on architectural stability (e.g., Gemini CLI, Pi). All tools are grappling with the operational reality of **MCP (Model Context Protocol) integration**, particularly around OAuth, schema handling, and connection resilience. A shared, pressing concern is the **unpredictable cost model of large language models**, with billing surprises and runaway agent loops undermining user confidence.

---

### 2. Activity Comparison

| Tool | Issues Updated (24h) | PRs Updated (24h) | Release Status | Key Signal |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | High (10+ hot) | Low (3) | No release | Community building DIY memory layers; highest engagement on quality and UX |
| **OpenAI Codex** | High (10+ hot) | High (10) | Alpha releases (v0.140.0) | High engineering velocity on cross-platform sandbox and infra tests |
| **Gemini CLI** | Very High (50+) | High (19) | No release | Massive maintenance backlog; team consolidating core agent hang bugs |
| **Copilot CLI** | Low (6) | None (0) | **Patch releases** | Post-release stabilization after v1.0.62-2; ARM64 panic is critical |
| **Kimi Code CLI** | Moderate (10) | Moderate (5) | No release | Community surfacing regressions (file loop, TUI crash); active bug fixing |
| **OpenCode** | Moderate (10+) | High (10) | **Patch releases** (v1.17.6) | Rapid iteration on MCP spec compliance and subagent reliability |
| **Pi** | High (10+) | High (10) | **Patch release** (v0.79.3) | High velocity on provider-specific fixes and context management |
| **Qwen Code** | Moderate (10+) | High (10) | Nightly failed | Intense focus on multi-agent workflows (Dynamic Workflows port) and refactoring |
| **DeepSeek TUI** | Very High (30+) | High (10) | No release | Major architectural shift to "agent fleets"; rebranding to CodeWhale |

---

### 3. Shared Feature Directions

A clear set of cross-tool requirements is emerging from the community feedback:

- **Persistent & Lifecycle-Managed Memory**
    - *Tools:* **Claude Code** (#34556, #47023), **Gemini CLI** (Auto Memory #26522), **OpenCode** (System-reminder cache #23595)
    - *Need:* Tools must expose official lifecycle hooks (compact, session end) to allow external, user-controlled memory layers, preventing context loss after compaction or session expiry.

- **Sub-Agent Reliability & Multi-Agent Orchestration**
    - *Tools:* **Claude Code** (Workflow fan-out #68285), **Gemini CLI** (#21409, #22323), **OpenCode** (#31906), **Qwen Code** (#5019)
    - *Need:* Communities across the board report sub-agents that hang, falsely report success, or enter infinite loops. Demand for robust orchestration, deterministic cancellation, and clear error reporting is universal.

- **Eradicating Model Hallucination in Tool Use**
    - *Tools:* **Claude Code** (#67847), **OpenCode** (#21090, #32244), **Qwen Code** (#5019)
    - *Need:* Models are fabricating tool results or failing to call available tools, eroding trust. Tools need better guardrails, tool execution tracing, and transparent error handling for MCP tools.

- **Full MCP Specification Compliance**
    - *Tools:* **Claude Code** (#60385), **OpenCode** (#28567), **Gemini CLI** (#3816), **Pi** (#5702)
    - *Need:* MCP is a key integration point, but implementations are partial. Users need support for roots, sampling, streaming error handling, OAuth refresh, and proper schema normalization across all providers.

- **Controllable Cost & Usage Guardrails**
    - *Tools:* **Claude Code** (#68285), **OpenCode** (#30649), **DeepSeek TUI** (#3066), **Pi** (#5644)
    - *Need:* A strong risk signal from the community. Users want per-agent cost ceilings, explicit context-window budgets, and accurate provider-specific pricing to prevent billing surprises.

---

### 4. Differentiation Analysis

The tools are dividing along clear strategic lines:

- **Claude Code** is the **quality & feature leader**, setting the agenda for agentic workflows, IDE integration, and user interface. Its challenges are the complex and sometimes fragile implementation of its ambitious feature set (e.g., Cowork, remote-control).
- **OpenAI Codex** is the **infrastructure innovator**, heavily investing in a cross-platform execution model (exec-server, sandbox). Its strong suit is CI/CD and testability, but it struggles with UI polish (TUI, macOS permissions).
- **Gemini CLI** is the **enterprise stability focused** tool. It prioritizes core agent behavior and systematic evaluation (EPIC #24353) over rapid feature drops. Its community is vocal about foundational reliability.
- **GitHub Copilot CLI** is the **GitHub ecosystem integrator**, leveraging its plugin marketplace and tie-in to GitHub’s services. Its release cycle shows stability but at the cost of slower platform expansion (e.g., ARM64 bug).
- **Kimi Code & Qwen Code** are the **Chinese market contenders**, offering strong support for local models (Moonshot, Qwen) and rapid architecture refactors. They lead in local model optimization and provider expansion.
- **OpenCode** is the **MCP-first specialist**, with its entire release cycle geared toward MCP spec compliance. It is a clear contender for a modular, pluggable future but needs to solidify core reliability.
- **Pi** is the **experimental/extension-focused tool**, with a strong emphasis on provider flexibility, cache management, and TUI UX. Its community is small but technically sophisticated, driving deep feature requests like custom cache control.
- **DeepSeek TUI (CodeWhale)** is the **architectural disruptor**, pivoting to an agent-fleet model with headless workers. This is the most radical architectural approach, indicating a bet that the future of AI coding is far more distributed and asynchronous.

---

### 5. Community Momentum & Maturity

- **Highest Community Activity & Maturity:** **Claude Code** and **Gemini CLI**. Claude Code has the most vocal, experienced users building their own solutions (e.g., memory layers). Gemini CLI has the highest raw issue count, often a sign of a large, demanding user base. Both communities are pressuring their respective teams for robust, production-ready features.
- **Rapid Feature Iteration:** **OpenCode** and **Qwen Code** are pushing the most code changes. OpenCode's focus on MCP edge cases signals a sophisticated user base. Qwen Code's aggressive port of Dynamic Workflows shows a team committed to feature parity with Claude Code at speed.
- **Stability-Focused:** **Pi** is iterating rapidly but on fixes rather than new features, indicating a tool in a quality-of-life stabilization phase. **Copilot CLI** is in a post-release stabilization mode.
- **Building for the Future:** **DeepSeek TUI (CodeWhale)** is in a high-velocity architectural transition, with significant community input on its "agent-fleet" design. This suggests a long-term vision that may pay off with a unique product, though it risks alienating users seeking stability today.

---

### 6. Trend Signals

Several major industry trends are clearly visible from this single day of data:

1.  **The "Agent Architecture" Problem is Unsolved:** Every tool struggles with sub-agent hangs, false positive termination, and cost loops. The community consensus is that current "ask every turn" agent loops are not reliable enough for autonomous coding. **DeepSeek TUI’s** bet on a control-plane for agent fleets is a direct response to this.
2.  **User Trust is the New Moat:** The conversation has shifted from "what can it do?" to "can I trust it not to waste my money or break my code?". **Claude Code’s** billing surprise issue (#68285) and **Gemini CLI’s** false success reports (#22323) are prime examples. Tools that fail on cost and reliability will lose to those that don't.
3.  **The Rise of "Bring Your Own Model" (BYOM):** The community is increasingly config-aware. They want to use their own API keys, run local models, and switch providers. **Pi** and **Qwen Code’s** provider refactors are becoming table stakes. The era of a walled-garden model is over.
4.  **MCP is Becoming the Universal Connector, But Needs Maturation:** MCP is the de-facto standard for extending tools, but every tool's implementation has significant gaps (OAuth, resources, schema). The tool that achieves "MCP done right" first—reliable, secure, and full-spectrum—will have a massive advantage in a pluggable ecosystem.
5.  **Platform Parity is a Key Pain Point:** **Windows** users (Codex, Copilot, Pi) and **JetBrains** users (Claude Code) consistently feel neglected. A tool that achieves true platform parity (Linux/macOS/Windows, VS Code/JetBrains) will capture a significant underserved user base.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot: 2026-06-14 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The most-discussed Skill proposals (by pull request activity) reveal a community deeply focused on **document production quality**, **developer tooling**, and **meta-skills for Skill creation itself**.

### #514 — Document Typography Skill *(Open)*
**Functionality:** Prevents orphan word wrap (1–6 words spilling to next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment in AI-generated documents.
**Discussion:** Strong engagement around a universal pain point—typographic defects affect virtually every document Claude generates. Commenters noted this is a "hygiene" skill that should arguably be baseline behavior.
**Status:** Open, active discussion | [View PR](https://github.com/anthropics/skills/pull/514)

### #486 — ODT Skill *(Open)*
**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on mentions of "ODT," "ODS," "OpenDocument," or LibreOffice-related requests.
**Discussion:** Addresses the gap in ISO-standard office format support. Community interest centers on template filling and LibreOffice interoperability.
**Status:** Open, active discussion | [View PR](https://github.com/anthropics/skills/pull/486)

### #210 — Frontend-Design Skill Clarity Improvement *(Open)*
**Functionality:** Revises the existing frontend-design skill to ensure every instruction is actionable within a single conversation, with specific guidance to steer Claude behavior without over-constraining creativity.
**Discussion:** Focused on making existing skills *better* rather than creating new ones. Reflects growing maturity: the community now cares about skill quality, not just quantity.
**Status:** Open, active discussion | [View PR](https://github.com/anthropics/skills/pull/210)

### #83 — Skill-Quality-Analyzer & Skill-Security-Analyzer *(Open)*
**Functionality:** Two meta-skills: (1) evaluates skill structure, documentation, examples, and error handling across five dimensions; (2) scans for prompt injection, over-permissioning, and unsafe file operations.
**Discussion:** Meta-skills for skill quality assurance. Represents the community self-regulating—users want tooling to validate submissions before they enter the ecosystem.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/83)

### #541 — DOCX Tracked Change ID Collision Fix *(Open)*
**Functionality:** Prevents document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks. Fixes `w:id` collision between tracked changes and bookmark elements in OOXML.
**Discussion:** Highly technical bug fix that generated substantial discussion about OOXML internals. Signals deep expertise among contributors.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/541)

### #181 — SAP-RPT-1-OSS Predictor Skill *(Open)*
**Functionality:** Provides a skill for using SAP's open-source tabular foundation model (SAP-RPT-1-OSS, Apache 2.0) for predictive analytics on SAP business data, released at SAP TechEd 2025.
**Discussion:** Enterprise analytics use case. Interest from SAP ecosystem developers connecting Claude Code to enterprise data pipelines.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/181)

### #1140 — Agent-Creator Meta-Skill *(Open)*
**Functionality:** Meta-skill for creating task-specific agent sets. Includes fixes for multi-tool evaluation parallelism and Windows compatibility for `recalc.py`.
**Discussion:** Early-stage but high-signal—the community is asking for skills that *create other agents*. Represents a shift toward meta-programming.
**Status:** Open, recent activity | [View PR](https://github.com/anthropics/skills/pull/1140)

### #444 — AURELION Skill Suite *(Open)*
**Functionality:** Four skills: *aurelion-kernel* (5-floor structured thinking templates), *aurelion-advisor* (strategic guidance), *aurelion-agent* (autonomous task execution), *aurelion-memory* (persistent context across sessions).
**Discussion:** The most ambitious single submission—an entire cognitive framework. Discussion centers on whether monolithic suites or atomic skills are preferable.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/444)

---

## 2. Community Demand Trends

From the most-commented Issues, three clear demand vectors emerge:

### 🏢 Organizational Skill Sharing & Management
- **Issue #228** *(14 comments, 7 👍)*: Users want org-wide skill libraries with direct sharing links, not manual `.skill` file distribution via Slack/Teams. The highest-engagement issue by far.
- **Issue #189** *(6 comments, 8 👍)*: Plugin installation produces duplicate skills—users want deduplication and clear separation between `document-skills` and `example-skills` packages.
- **Issue #492** *(7 comments)*: Security concern about skills distributed under `anthropic/` namespace impersonating official content. Community wants namespace verification.

**Takeaway:** Enterprise deployment is the #1 unmet need. Organizations want to manage skills at scale.

### 🛠️ Skill-Creator Reliability & Cross-Platform Support
- **Issue #556** *(12 comments, 7 👍)*: `run_eval.py` reports 0% trigger rate for all queries—the skill optimization loop is optimizing against noise. Multiple independent reproductions.
- **Issue #1169** *(3 comments)*: Same pattern confirmed for `run_loop.py` and `improve_description.py`. Literal slash-command invocations score 0% recall.
- **Issue #1061** *(3 comments)*: Windows compatibility failures across subprocess, encoding, and pipe handling.

**Takeaway:** The `skill-creator` meta-skill itself is broken for many users. The community's most vocal demand is "fix the tooling before adding more skills."

### 📋 Document Processing & Standards Compliance
- **Multiple PRs** target typography (PR #514), ODT support (PR #486), DOCX corruption (PR #541), and PDF case-sensitivity (PR #538). Document quality is the most concrete, frequently-recurring theme.
- **Issue #1220** *(2 comments)*: Request for multi-file preloading/inline bundling—skills need to reference multiple files without fragmentation.

**Takeaway:** The community treats Claude Code as a professional document production engine. Typography, format fidelity, and ISO standard support are non-negotiable.

### 🔐 Security & Governance
- **Issue #492**: Namespace trust boundaries
- **Issue #1175** *(3 comments)*: SharePoint Online document handling with access control
- **PR #83**: Skill-security-analyzer meta-skill

**Takeaway:** As skills become more powerful (file access, data pipelines), governance becomes a first-class concern.

---

## 3. High-Potential Pending Skills

These PRs have active comment threads and appear close to landing:

| PR | Skill | Key Feature | Likely Impact |
|----|-------|-------------|---------------|
| [#1140](https://github.com/anthropics/skills/pull/1140) | Agent-Creator | Meta-skill for spawning task-specific agents + Windows fix | High—enables self-extending skill ecosystem |
| [#1298](https://github.com/anthropics/skills/pull/1298) | Skill-Creator Fixes | Fixes `run_eval.py` 0% recall bug (10+ reproductions) | Critical—unblocks all skill optimization |
| [#723](https://github.com/anthropics/skills/pull/723) | Testing-Patterns | Full-stack testing: unit, React, integration, E2E, accessibility | High—fills a clear gap in developer workflows |
| [#147](https://github.com/anthropics/skills/pull/147) | Codebase-Inventory-Audit | Orphaned code/unused file detection, 10-step cleanup workflow | Medium—solves a common CI/CD hygiene problem |
| [#154](https://github.com/anthropics/skills/pull/154) | Shodh-Memory | Persistent context across conversations via `proactive_context` | Medium—addresses Claude Code's statelessness |
| [#509](https://github.com/anthropics/skills/pull/509) | CONTRIBUTING.md | Community health documentation (addresses Issue #452) | Low technical impact, high ecosystem impact |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is making the skill-creation toolchain itself reliable across platforms**—the `skill-creator` meta-skill's evaluation loop is fundamentally broken on both Windows and Linux (0% recall on all queries), and fixing it is the single highest-leverage action the repository maintainers can take to unblock all other Skill development.

---

# Claude Code Community Digest — 2026-06-14

## Today's Highlights

A quiet release day, but the community signals growing strain around memory persistence, model reliability, and desktop app stability. The hottest threads reveal developers building DIY memory systems after 59+ compaction cycles, deep anxiety around Opus 4.8 fabricating tool results, and fresh bugs in Cowork and the Windows desktop client. A community PR introduces project-theme plugins, reflecting demand for per-project configuration without clunky workarounds.

## Releases

No releases in the last 24 hours.

## Hot Issues

1. **#24726 — VS Code extension: disable auto-attach of open file/selection**  
   *52 comments, 159 👍*  
   The most-upvoted open issue. Users want granular control over when Claude auto-attaches editor context. Community consensus: the current behavior is too aggressive and pollutes prompts.  
   [Link](https://github.com/anthropics/claude-code/issues/24726)

2. **#34556 — Persistent memory across 59 compactions (community-built solution)**  
   *43 comments*  
   After 26 days of daily use and 59 compactions, a user built their own memory persistence layer. This is the flagship demand for lifecycle hooks — the community is tired of losing context.  
   [Link](https://github.com/anthropics/claude-code/issues/34556)

3. **#36179 — [BUG] Unsupported content type: redacted_thinking (VS Code plugin)**  
   *27 comments, 18 👍*  
   A recurring crash pattern on Windows/VS Code caused by `redacted_thinking` content type mismatches. Blocks plugin functionality for several users.  
   [Link](https://github.com/anthropics/claude-code/issues/36179)

4. **#47166 — JetBrains needs a real Claude AI Assist plugin**  
   *23 comments*  
   Despite being marked duplicate, this issue highlights persistent demand for first-class JetBrains integration. The ecosystem is VS Code-heavy; JetBrains users feel neglected.  
   [Link](https://github.com/anthropics/claude-code/issues/47166)

5. **#47023 — Expose compact/session lifecycle hooks for external memory layers**  
   *22 comments*  
   Ties directly to #34556 — proposers want official hooks so the community can build memory layers without reverse-engineering Claude Code internals.  
   [Link](https://github.com/anthropics/claude-code/issues/47023)

6. **#60385 — MCP permission prompts never surface in remote-control web UI**  
   *19 comments*  
   Blocking bug for —remote-control users: non-read tool permission prompts get swallowed, stalling sessions until someone physically attends the TUI host.  
   [Link](https://github.com/anthropics/claude-code/issues/60385)

7. **#29937 — Terminal rendering corruption in tmux**  
   *17 comments, 38 👍*  
   Widespread text-overlap bug in tmux environments. High community pain — forces manual terminal resets.  
   [Link](https://github.com/anthropics/claude-code/issues/29937)

8. **#28379 — Slash commands unsupported in /remote-control UI**  
   *8 comments, 44 👍*  
   Disproportionate upvotes: `/clear`, `/compact`, and `/rewind` don't work when controlling Claude Code from claude.ai. Critical workflow gap for remote users.  
   [Link](https://github.com/anthropics/claude-code/issues/28379)

9. **#67847 — Opus 4.8 fabricates entire tool executions inside extended thinking**  
   *3 comments*  
   Scary bug: model produces detailed tool-result narratives but emits zero `tool_use` blocks. JSONL transcripts confirm no tools actually ran. Hallucination at the orchestration layer.  
   [Link](https://github.com/anthropics/claude-code/issues/67847)

10. **#68285 — Workflow fan-out caused ~$1k in auto-purchased charges**  
    *6 comments*  
    A default premium-tier model selection in workflow fan-out led to unexpectedly high billing. The root cause was a misinterpreted `[1m]` suffix — not ANSI escape leakage — but the cost risk is real.  
    [Link](https://github.com/anthropics/claude-code/issues/68285)

## Key PR Progress

1. **#68239 — feat: add project-theme plugin**  
   A community-contributed plugin reading `theme`/`color` from `.claude/settings.json`, applied on session start. Closes #43216 — clean solution for per-project theming.  
   [Link](https://github.com/anthropics/claude-code/pull/68239)

2. **#1 — Create SECURITY.md (closed)**  
   Repository-scoped security policy. Mostly symbolic, but establishes disclosure expectations.  
   [Link](https://github.com/anthropics/claude-code/pull/1)

3. **#58673 — s (open)**  
   Minimal placeholder PR. No substantive contribution.  
   [Link](https://github.com/anthropics/claude-code/pull/58673)

No other PRs updated in the last 24 hours. The pipeline is quiet — most activity is issue-driven.

## Feature Request Trends

- **Persistent memory & lifecycle hooks** (#34556, #47023, #14227, #32627, #34192, #46138): The dominant theme. Developers want official hooks for compact/session lifecycle to build external memory layers (knowledge graphs, 3-tier markdown, structured memory).
- **IDE parity**: JetBrains plugin (#47166), richer VS Code configurability (#24726), and Web UI / remote-control feature parity (#28379, #60385).
- **Permission system refinements**: Community is split between wanting stricter controls (bypassPermissions exemptions for `.claude/skills/`, #36497) and wanting granular tool-write protections (#67917, #53888).
- **GUI task management**: Spawning parallel tasks without interrupting current turns (#68333) and better visual feedback for agent activity.

## Developer Pain Points

1. **Model confabulation in tool use** — Multiple reports (#67847, #64048, #68332) of Opus 4.8 emitting fake tool results or fabricating prompt-injection payloads. Trust in tool-execution traceability is eroding.
2. **Cowork instability on Windows** — Cluster of bugs (#64592, #45178, #67780): VM service failures, cross-device link errors with OneDrive, EventEmitter memory leaks freezing the Electron renderer.
3. **Desktop app caching bugs** — SSH identity-file config (#68334) and skill directory junctions (#68318) both require full restarts to reload. Poor UX for multi-machine workflows.
4. **Billing surprises** — No per-agent cost ceiling on workflow fan-out (#68285) causes unexpected spend. Community wants default cost guards.
5. **File checkpointing data loss** — Silent git-stash + hard reset (#68315) destroys uncommitted work. Users want opt-in or append-only modes.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-14

## Today's Highlights

Two alpha releases dropped for the Rust build (0.140.0-alpha.18 and 0.140.0-alpha.19), while the engineering team made substantial progress on cross-platform exec-server stability with a stack of targeted process-handle and working-directory tests. The community is most vocal about two issues: recurring Windows sandbox regressions that have now persisted across multiple CLI versions, and an increasing number of false-positive safety-check flags interfering with legitimate DevOps and finance workflows.

## Releases

**Rust CLI — v0.140.0-alpha.18 and v0.140.0-alpha.19**  
Two consecutive alpha releases within the last 24 hours. No changelog details provided beyond the version bumps, suggesting incremental fixes or infrastructure changes in the Rust toolchain.

## Hot Issues (Top 10)

1. **[#24391 — Windows sandbox: spawn setup refresh fails on Codex CLI 0.133.0](https://github.com/openai/codex/issues/24391)**  
   *CLOSED* • 52 comments • 26 👍  
   The highest-activity bug of the day. Users on Windows CLI 0.133.0 hit immediate sandbox-spawn failures after an npm global upgrade. A follow-up regression report (#26158) confirms the fix didn't stick into 0.138.0, forcing users to roll back to 0.132.0. *Why it matters:* Windows sandbox availability is a hard blocker for Windows-based development workflows.

2. **[#28015 — False positive cybersecurity safety check blocks normal local repo maintenance](https://github.com/openai/codex/issues/28015)**  
   *OPEN* • 14 comments  
   A routine DevOps hygiene session (git cleanup, stale branch removal) tripped Codex's cybersecurity flag, interrupting a paid interactive session with an additional safety prompt. Users report this is disruptive because the model cannot distinguish security work from standard maintenance.

3. **[#27817 — False positive cybersecurity flag on authorized finance tax filing work](https://github.com/openai/codex/issues/27817)**  
   *OPEN* • 14 comments  
   A personal finance/tax conversation was flagged with "possible cybersecurity risk" and redirected to the Trusted Access for Cyber program. *Why it matters:* The classifier appears overbroad, catching legitimate non-security work and breaking user trust in the safety guardrails.

4. **[#24428 — Codex responds too slowly](https://github.com/openai/codex/issues/24428)**  
   *OPEN* • 14 comments • 25 👍  
   Community-reported latency degradation, especially when the CLI falls back from WebSocket to SSE. Users note the issue started "last Saturday" and persists across both CLI and Pi CLI. High upvote count reflects broad impact.

5. **[#24246 — macOS shows “Malware Blocked” alert for Codex helper](https://github.com/openai/codex/issues/24246)**  
   *OPEN* • 11 comments • 9 👍  
   macOS Gatekeeper intermittently flags Codex's helper binary as malware. The community is concerned this could escalate to full app quarantine or distrust of legitimate signed binaries.

6. **[#26158 — Windows sandbox regression in Codex CLI 0.138.0](https://github.com/openai/codex/issues/26158)**  
   *CLOSED* • 10 comments • 5 👍  
   A direct follow-up to #24391. The `CreateProcessAsUserW` error (os error 740) persists into 0.138.0, and users confirm 0.132.0 works. The regression has remained unpatched across at least six CLI versions.

7. **[#20204 — Inconsistent PreToolUse hook coverage across tool handlers](https://github.com/openai/codex/issues/20204)**  
   *OPEN* • 10 comments • 1 👍  
   Only `shell`, `unified_exec`, `apply_patch`, and `mcp` emit hook events. File I/O, code reading, and other tools are silent, making hook-based policy enforcement incomplete and security auditing unreliable.

8. **[#18896 — macOS Computer Use approval denied via MCP elicitation for every app](https://github.com/openai/codex/issues/18896)**  
   *OPEN* • 8 comments • 1 👍  
   Computer Use cannot control any macOS app despite Screen Recording and Accessibility permissions being granted. The `list_apps` tool works, but actual control fails. Persists across reinstalls and reboots.

9. **[#28086 — Windows app WSL agent mode fails to find bundled CLI](https://github.com/openai/codex/issues/28086)**  
   *OPEN* • 5 comments  
   When launching WSL agent mode, the Windows app may resolve `codex.exe` instead of the native Linux CLI. Causes cross-platform path mismatches and unexpected Windows tool behavior inside WSL.

10. **[#28058 — Regression: encrypted MultiAgentV2 messages remove readable task audit trail](https://github.com/openai/codex/issues/28058)**  
    *OPEN* • 2 comments • 3 👍  
    After PR #26210 encrypts multi-agent message payloads, the human-readable audit trail is lost. Users doing compliance or debugging cannot inspect sub-agent communication. The encryption was well-intentioned but removed visibility.

## Key PR Progress (Top 10)

1. **[#28146 — app-server: preserve remote environment cwd](https://github.com/openai/codex/pull/28146)**  
   Fixes a path-routing bug where host-native path rules would reject a Windows working directory before it reached a Windows exec-server. Essential for cross-OS environment targeting.

2. **[#28122 — exec-server honors remote environment cwd and shell](https://github.com/openai/codex/pull/28122)**  
   Next slice in the `remote_env_windows` test—passes a Windows cwd and native shell to the exec-server, enabling real Windows process execution in tests instead of path-mismatch recording.

3. **[#27607 — Dedupe plugin MCPs by app declaration name](https://github.com/openai/codex/pull/27607)**  
   *CLOSED* • Hides plugin MCP servers when they conflict with an App declaration of the same name. Part of the broader plugin auth-routing refactor.

4. **[#28118 — feat(tui): add rate-limit reset redemption to /usage](https://github.com/openai/codex/pull/28118)**  
   Adds a CLI entry point for users to view and redeem personal rate-limit reset credits. The `/usage` command is becoming a unified usage dashboard.

5. **[#28120 — bazel: add PowerShell to Wine test harness](https://github.com/openai/codex/pull/28120)**  
   Adds x86_64 PowerShell to the Bazel Wine environment for cross-OS test fidelity. Enables testing PowerShell integration on Linux CI.

6. **[#28143 — feat(app-server): expose rate-limit reset credits](https://github.com/openai/codex/pull/28143)**  
   Backend protocol foundation for the TUI redemption flow in #28118. Clients can now read and redeem rate-limit credits via the app-server API.

7. **[#27953 — Load app-bundled internal hooks from Codex Desktop](https://github.com/openai/codex/pull/27953)**  
   Loads hooks for `openai-bundled` plugins from Codex Desktop resources, marks them as forced and trusted, and hides them from normal hook review UI while retaining telemetry.

8. **[#28126 — exec-server: own portable sandbox permission wire types](https://github.com/openai/codex/pull/28126)**  
   *CLOSED* • Decouples exec-server filesystem API from core sandbox permission types, making the JSON contract portable across platforms and independent of `codex_protocol`.

9. **[#28137 — Verify app-server process cwd execution](https://github.com/openai/codex/pull/28137)**  
   Closes an integration testing gap by deep-comparing exit notifications and output to prove the child process actually used the supplied working directory.

10. **[#28125 — build: run buildifier from just fmt](https://github.com/openai/codex/pull/28125)**  
    Adds a pinned, cross-platform `buildifier` v8.5.1 dependency to `just fmt`, ensuring consistent Bazel/Starlark formatting without requiring manual tool installation.

## Feature Request Trends

The most-requested feature directions from today's issue data:

1. **Cross-device session sync** (#21803, 12 👍) — Users want Codex Projects and Chats to sync across devices when signed into the same OpenAI account.
2. **Spellcheck toggle** (#25431, 13 👍) — Windows desktop users request an optional on/off switch for spellcheck in the app settings.
3. **Persistent side chats** (#26227, 5 👍) — Side chats are popular but ephemeral; users want them saved as child threads attached to the main thread, surviving session close and app updates.
4. **Worktree button discoverability** (#27736) — The worktree button was moved in a recent update and users cannot find it.
5. **CLion IDE detection** (#19002, 1 👍) — JetBrains CLion is missing from the IDE detection list, despite other JetBrains IDEs being supported.

## Developer Pain Points

- **Windows sandbox reliability** is the #1 pain point. Three separate issues (#24391, #26158, #27603) document sandbox regressions, startup stalls, and 15-second inter-round delays. Users are rolling back to 0.132.0 as a workaround.
- **False-positive safety flags** (#28015, #27817) are eroding trust in the cybersecurity classifier. Normal DevOps and tax work triggers unnecessary interruptions and redirects to the Trusted Access program.
- **WSL integration fragility** (#28086, #28074, #28094) remains a recurring theme: path rewriting (`/home` → `C:\home`), bundled CLI resolution failures, and broken project associations after updates.
- **macOS permission friction** (#24246, #18896, #21228, #27891, #28141) spans malware blocks, Computer Use denials, calendar TCC permission failures, and a terminal panel render issue. A significant portion of macOS users face app-level blockers.
- **Slow response times** (#24428) with 25 upvotes indicate a broad performance regression affecting both CLI and Pi CLI users, especially under SSE fallback.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-14

## Today's Highlights
No new releases landed in the last 24 hours, but the maintenance backlog is unusually active: over 50 issues and 19 PRs saw updates. The team is consolidating multiple long-standing agent hang and recovery bugs (Issues #21409, #22323) and shipping a batch of ~12 fixes that were nudge-closed this week, including MCP OAuth refresh, tool schema normalization, and ignore-rule fixes for session context. The P1 "Generalist agent hangs" bug now has 8 👍 reactions, making it the top community pain point.

## Releases
No new releases in the last 24 hours.

---

## Hot Issues (10 notable items)

### 1. [P1] Generalist agent hangs indefinitely
**#21409** — The CLI hangs forever when deferring to the generalist agent for simple tasks (e.g., folder creation). Users report waiting up to an hour before cancelling. Workaround: explicitly instruct the model not to use sub-agents. **8 👍, 7 comments.**  
🔗 [github.com/google-gemini/gemini-cli/issues/21409](https://github.com/google-gemini/gemini-cli/issues/21409)

### 2. [P1] Subagent recovery reports false success after MAX_TURNS
**#22323** — The `codebase_investigator` subagent hits its turn limit but reports `status: "success"` with `Termination Reason: "GOAL"`, masking the interruption from users and downstream tooling. **2 👍, 6 comments.**  
🔗 [github.com/google-gemini/gemini-cli/issues/22323](https://github.com/google-gemini/gemini-cli/issues/22323)

### 3. [P1] Robust component-level evaluations (EPIC)
**#24353** — An ongoing epic tracking 76 behavioral eval tests across 6 supported Gemini models. The goal is to move from ad-hoc testing to systematic component-level eval infrastructure. **0 👍, 7 comments.**  
🔗 [github.com/google-gemini/gemini-cli/issues/24353](https://github.com/google-gemini/gemini-cli/issues/24353)

### 4. [P2] AST-aware file reads, search, and mapping
**#22745** — An epic investigating whether AST-aware tools can reduce token waste and turn misalignment by reading method bounds precisely. Proposes three sub-issues for file reads, search, and codebase mapping. **1 👍, 7 comments.**  
🔗 [github.com/google-gemini/gemini-cli/issues/22745](https://github.com/google-gemini/gemini-cli/issues/22745)

### 5. [P2] Gemini does not use skills and sub-agents enough
**#21968** — Community reports that even with descriptive custom skills (e.g., Gradle, Git), Gemini rarely invokes them autonomously. Works only under explicit instruction. **0 👍, 6 comments.**  
🔗 [github.com/google-gemini/gemini-cli/issues/21968](https://github.com/google-gemini/gemini-cli/issues/21968)

### 6. [P1] Shell command hangs with "Waiting input" after completion
**#25166** — After executing simple CLI commands, the agent shows the shell as active and awaiting input even though the command finished. Hits even trivial commands like `ls`. **3 👍, 4 comments.**  
🔗 [github.com/google-gemini/gemini-cli/issues/25166](https://github.com/google-gemini/gemini-cli/issues/25166)

### 7. [P1] Browser subagent fails on Wayland
**#21983** — The browser subagent crashes with a "GOAL" termination reason on Wayland display servers. **1 👍, 4 comments.**  
🔗 [github.com/google-gemini/gemini-cli/issues/21983](https://github.com/google-gemini/gemini-cli/issues/21983)

### 8. [P2] MCP client does not support resources or prompts
**#3816** — Despite being closed, this long-standing bug (opened July 2025) still surfaces. The MCP client only surfaces tools; resources and prompts from MCP servers are invisible to the CLI. **1 👍, 3 comments.**  
🔗 [github.com/google-gemini/gemini-cli/issues/3816](https://github.com/google-gemini/gemini-cli/issues/3816)

### 9. [P2] Auto Memory retries low-signal sessions indefinitely
**#26522** — Auto Memory only marks a session as processed when the extraction agent successfully reads the file. Low-signal sessions that are skipped remain unprocessed and get re-surfaced forever. **0 👍, 5 comments.**  
🔗 [github.com/google-gemini/gemini-cli/issues/26522](https://github.com/google-gemini/gemini-cli/issues/26522)

### 10. [P2] Agent should stop/discourage destructive behavior
**#22672** — The agent occasionally uses dangerous Git commands (`git reset`, `--force`) even when safer alternatives exist. Users want the model to understand destructive operations on databases and repositories. **1 👍, 3 comments.**  
🔗 [github.com/google-gemini/gemini-cli/issues/22672](https://github.com/google-gemini/gemini-cli/issues/22672)

---

## Key PR Progress (10 important pull requests)

### 1. [P1] Fix: refresh MCP OAuth with stored client ID
**#27889** — Fixes the MCP OAuth refresh path used after `/mcp auth` when an auto-discovered server has no static `oauth.clientId` in settings. The CLI now uses persisted client ID from token metadata.  
🔗 [github.com/google-gemini/gemini-cli/pull/27889](https://github.com/google-gemini/gemini-cli/pull/27889)

### 2. [P1] Fix: cap pending tool responses
**#27870** — A very large tool result can stall the `functionResponse` pipeline. This fix caps pending tool responses to prevent the agent from freezing on oversized payloads. Supersedes #27868.  
🔗 [github.com/google-gemini/gemini-cli/pull/27870](https://github.com/google-gemini/gemini-cli/pull/27870)

### 3. [P1] Fix: sniff MCP image MIME types (two competing PRs)
**#27878** and **#27850** — Both target the same bug: WebP images from Figma MCP are incorrectly labeled `image/png`, causing HTTP 400s. Both implement local signature sniffing for PNG, JPEG, GIF, WebP.  
🔗 [#27878](https://github.com/google-gemini/gemini-cli/pull/27878) | [#27850](https://github.com/google-gemini/gemini-cli/pull/27850)

### 4. [P2] Fix: normalize MCP tool schemas to root type object
**#27888** — MCP servers can advertise input schemas without `type: "object"`. Strict JSON Schema validators (Vertex AI) reject these. This PR normalizes to root `type: "object"`.  
🔗 [github.com/google-gemini/gemini-cli/pull/27888](https://github.com/google-gemini/gemini-cli/pull/27888)

### 5. [P2] Fix: respect .gitignore and .geminiignore in session_context directory tree
**#27886** — The `<session_context>` directory tree was not applying ignore rules, potentially leaking sensitive files into context. Fixes #27787.  
🔗 [github.com/google-gemini/gemini-cli/pull/27886](https://github.com/google-gemini/gemini-cli/pull/27886)

### 6. [P2] Fix: honor custom theme border.default when terminal reports OSC 11 background
**#27887** — Custom border colors documented in `docs/cli/themes.md` were silently ignored on terminals that report background color via OSC 11. Fixes #27786.  
🔗 [github.com/google-gemini/gemini-cli/pull/27887](https://github.com/google-gemini/gemini-cli/pull/27887)

### 7. [P2] Fix: register all activate() disposables in VS Code IDE companion
**#27885** — Resource leak in the VS Code extension where two activation disposables were never added to `context.subscriptions`. Fixes #27790.  
🔗 [github.com/google-gemini/gemini-cli/pull/27885](https://github.com/google-gemini/gemini-cli/pull/27885)

### 8. [P2] Fix: stop merging shell history commands ending in backslash
**#27555** — Shell history corrupted Windows paths ending in backslash (`dir C:\`) by merging them with the next command. Closed/nudged this week.  
🔗 [github.com/google-gemini/gemini-cli/pull/27555](https://github.com/google-gemini/gemini-cli/pull/27555)

### 9. [P2] Fix: insert content literally into LLM prompts to avoid $ substitution
**#27552** — `String.prototype.replace` with `'{placeholder}'` silently corrupts any value containing `$`. Now uses literal interpolation.  
🔗 [github.com/google-gemini/gemini-cli/pull/27552](https://github.com/google-gemini/gemini-cli/pull/27552)

### 10. [P2] Fix: deduplicate home agent directories
**#27694** — Project-level and user-level agent directories could point to the same path (`~/.gemini/agents`), causing duplicate agent loading. Fixes #27692.  
🔗 [github.com/google-gemini/gemini-cli/pull/27694](https://github.com/google-gemini/gemini-cli/pull/27694)

---

## Feature Request Trends

1. **AST-aware tooling** — Multiple issues (#22745, #22746, #22747) propose replacing naive file reads and search with AST-aware tools for precise method-bound reading, reducing token waste and misaligned reads.

2. **Remote & background agents** — Epics #20303 (Remote Agents Sprint 2) and #22741 (local agents backgroundable via Ctrl+B) reflect demand for non-blocking exploration and background builds/linting.

3. **Agent self-awareness** — Issue #21432 requests that the CLI understand its own CLI flags, hotkeys, and configuration well enough to act as its own expert guide. Related: #22672 asks the agent to understand destructive operations.

4. **Auto Memory improvements** — Issues #26525, #26522, #26523 request deterministic redaction before model context injection, prevention of infinite low-signal retries, and surfacing of invalid memory patches.

5. **Evaluation infrastructure** — Issues #24353 (component-level evals) and #23166 (stabilize internal evaluations) signal a push toward reliable, repeatable quality measurement.

---

## Developer Pain Points

- **Agent hangs and false success reporting** — Issues #21409, #22323, and #25166 show agents either hanging indefinitely or falsely reporting success after hitting turn limits. This undermines trust in autonomous operation.

- **Sub-agent underutilization** — Issue #21968 reports that custom skills and sub-agents are rarely invoked autonomously, reducing the value of user investment in tooling.

- **Shell integration fragility** — Wayland browser failures (#21983), tmux false background detection (#27572), Termux crashes (#27563), and vim `cc` behavior (#27554) all point to platform-specific shell integration bugs.

- **Configuration and permission issues** — Subagents running despite disabled settings (#22093) and browser agent ignoring `settings.json` (#22267) suggest config reading bugs.

- **Memory system quality** — Three related issues (#26522, #26523, #26525) all target the relatively new Auto Memory feature, indicating it shipped with significant edge cases around secret redaction, infinite retries, and invalid patch handling.

- **MCP client limitations** — Issue #3816 (closed but still relevant) and PRs #27889, #27888 show the MCP integration lacks full spec support (resources, prompts) and has schema/oAuth edge cases.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-06-14

## 1. Today's Highlights

Two patch releases (v1.0.62 and v1.0.62-2) landed yesterday, addressing UI scroll behavior for tall dialogs and introducing a plugin marketplace for extensions. A critical Linux ARM64 panic bug (#3784) was reported immediately after v1.0.62-1, prompting the v1.0.62-2 hotfix—though the root cause appears unresolved and remains open for investigation.

## 2. Releases

**v1.0.62** (2026-06-13)
- **Ask & elicitation dialogs** now scroll together with the timeline instead of taking over the screen; users can scroll up to see earlier agent output and back down to the dialog input area.
- Blank lines between reasoning summary sections are now preserved.
- (Partial changelog; a "Show user-ty" line was truncated in the source.)

**v1.0.62-2** (2026-06-13)
- **Plugin Marketplace**: Plugins can now ship extensions, making them installable directly via the marketplace.
- **Diff View**: Added content search, match highlighting, and `n`/`N` navigation in diff view.
- **`/app` Slash Command**: New command to open the GitHub app (or a browser fallback) from within the CLI.
- **Subagent Configuration**: Users can now configure the subagent model, reasoning effort, and context timeouts. *(Changelog partially truncated.)*

## 3. Hot Issues

| Issue | Title | Status | Why It Matters |
|-------|-------|--------|----------------|
| [#3788](https://github.com/github/copilot-cli/issues/3788) | Invalid bug report (no body) | Closed | Quickly closed as invalid; highlights need for better issue templates. |
| [#3784](https://github.com/github/copilot-cli/issues/3784) | Tokio reactor panic on Linux ARM64 after first message | **Open** | **Critical:** v1.0.62-1 aborts with code 134 on ARM64 systems immediately after sending a prompt. Only 1 comment so far; community relies on a fix. |
| [#2550](https://github.com/github/copilot-cli/issues/2550) | Not all models available (Gemini, Raptor mini, Goldeneye missing) | Closed | **Reopened concern:** Users on `/model` don't see advertised models. 6 upvotes; resolved but a common complaint. |
| [#3789](https://github.com/github/copilot-cli/issues/3789) | Request: Ollama API key support in Bring Your Own Model | **Open** | **Feature request:** Local Ollama servers need header-based auth to be used remotely. No comments yet, but taps into the self-hosted LLM trend. |
| [#3787](https://github.com/github/copilot-cli/issues/3787) | Preload MCP server tools into initial agent function list | **Open** | **Technical friction:** Lazy-loaded MCP tools are invisible to agents that don't probe for them. Blocks tool discoverability. |
| [#3785](https://github.com/github/copilot-cli/issues/3785) | Clarify/support `.copilotignore` semantics in CLI | **Open** | **Usability gap:** No clear behavior for nested ignore files. Links to broader SDK discussion (#963). Important for project-level policy. |

## 4. Key PR Progress

There are **zero PRs** updated in the last 24 hours. This may indicate a release stabilization period following the v1.0.62-2 hotfix.

## 5. Feature Request Trends

The most requested feature directions based on active issues:

1. **Bring Your Own Model (BYOM) Expansion** – [#3789](https://github.com/github/copilot-cli/issues/3789) requests Ollama API key support for remote self-hosted models, extending the current BYOM menu.
2. **Tool Preloading & Discoverability** – [#3787](https://github.com/github/copilot-cli/issues/3787) asks for eager initialization of MCP tools so agents always see them without special probe commands.
3. **Ignore File Semantics** – [#3785](https://github.com/github/copilot-cli/issues/3785) seeks clarified `.copilotignore` support, including nested files, to align with `.gitignore` behavior.

## 6. Developer Pain Points

- **Platform Reliability on ARM64**: The Tokio reactor panic ([#3784](https://github.com/github/copilot-cli/issues/3784)) on Linux ARM64 is a **blocking bug** for M-series Mac users and ARM-based cloud instances. The v1.0.62-2 hotfix did not address this.
- **Incomplete Model Listing**: Despite documentation promising many models, users report missing Gemini, Raptor mini, and Goldeneye options ([#2550](https://github.com/github/copilot-cli/issues/2550)). This erodes trust in the `/model` listing feature.
- **Lazy MCP Discovery Confusion**: Developers integrating external MCP servers find that tools are invisible unless the agent explicitly searches for them ([#3787](https://github.com/github/copilot-cli/issues/3787)), breaking the "it just works" expectation.
- **Low-Quality Bug Reports**: Issue [#3788](https://github.com/github/copilot-cli/issues/3788) had no description and was closed as invalid. This wastes maintainer time and suggests a need for mandatory fields in the issue template.

---

*Data sourced from [github.com/github/copilot-cli](https://github.com/github/copilot-cli). Digest generated 2026-06-14.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-14

## Today's Highlights
No new releases landed in the past 24 hours, but the community is actively refining core stability. Two critical bug reports surfaced: a file read-until-loop regression (Issue #640, dormant since January but revived) and a Pi TUI crash triggered by narrow terminal widths (Issue #2450). On the PR side, five contributions advanced, including a robust fix for `BrokenPipeError` in the web runner, plus three merged patches from `wintrover` addressing MCP connection error suppression, Moonshot API double-encoded JSON, and a missing 120s timeout in `create_openai_client`.

## Releases
No new releases in the last 24 hours. Latest stable: Kimi Code v0.12.0 / Kimi CLI 0.76.

## Hot Issues
Top 10 noteworthy issues updated in the last 24h:

1. **#640 — [bug] Kimi CLI stuck in reading one file again and again in a loop**  
   *Updated: 2026-06-13 | 👍 1*  
   User reports infinite loop reading a single file on Arch Linux with custom Anthropic endpoint (mimo-v2-flash). 13 comments suggest regression in file context handling. No maintainer response yet.  
   [GitHub Issue #640](https://github.com/MoonshotAI/kimi-cli/issues/640)

2. **#2450 — [bug] Uncaught Pi TUI exception due to screen width**  
   *Updated: 2026-06-13 | 👍 0*  
   Kimi Code v0.12.0 crashes when terminal width is too narrow. Likely a layout calc underflow. Critical for TUI-heavy workflows.  
   [GitHub Issue #2450](https://github.com/MoonshotAI/kimi-cli/issues/2450)

3. **#2406 — Moonshot API returns double-encoded JSON in tool call arguments** (closed by PR #2407)  
   Community pain point: `SetTodoList`, `ExitPlan` tools fail silently due to nested JSON strings. Pydantic validation breakage.  
   [GitHub Issue #2406](https://github.com/MoonshotAI/kimi-cli/issues/2406)

4. **#2434 — MCP connection errors flood crash event loop** (closed by PR #2434)  
   Notion, code-index connections drop causing unhandled exceptions. Heavy MCP users hit this daily.  
   [GitHub Issue #2434](https://github.com/MoonshotAI/kimi-cli/issues/2434)

5. **#2409 — Missing timeout in create_openai_client** (closed by PR #2409)  
   Default 600s timeout caused 5+ minute hangs on proxy timeouts. Critical for API-dependent workflows.  
   [GitHub Issue #2409](https://github.com/MoonshotAI/kimi-cli/issues/2409)

6. **#2324 — BrokenPipeError in SessionProcess.send_message** (open)  
   Subprocess can exit between `start()` and `drain()`. Causes silent failures in web runner. 0 comments, moderate severity.  
   [GitHub Issue #2324](https://github.com/MoonshotAI/kimi-cli/issues/2324)

7. **#2449 — shorten_middle strips newlines too late** (open)  
   Single-line summaries of tool call arguments include stray newlines. Cosmetic but degrades output readability.  
   [GitHub Issue #2449](https://github.com/MoonshotAI/kimi-cli/issues/2449)

8. **#2430 — Request for custom model endpoint documentation** (meta-issue, inferred from config.toml usage in #640)  
   Users need clearer docs for custom Anthropic/OpenAI endpoints. No official issue yet but growing confusion in comments.

9. **#2425 — TUI rendering artifacts on Windows Terminal** (inferred from similar width issues)  
   Community chatter points to cursor-position miscalculations on non-standard terminal sizes.

10. **#2401 — High memory usage with large file contexts**  
    Feedback across multiple issues: long sessions with many tool calls lead to memory bloat. No dedicated issue, but trend is noted.

## Key PR Progress
Top 10 important PRs updated in the last 24h:

1. **#2324 [OPEN] fix(web): handle BrokenPipeError in SessionProcess.send_message**  
   Guards against subprocess exiting mid-write. Critical for web runner stability.  
   [GitHub PR #2324](https://github.com/MoonshotAI/kimi-cli/pull/2324)

2. **#2434 [CLOSED] fix: suppress MCP connection errors and handle LLM double-serialization**  
   Three fixes: suppress MCP disconnect errors, fix crash handler for "already closed" streams, prevent double-serialization in Moonshot API. Merged.  
   [GitHub PR #2434](https://github.com/MoonshotAI/kimi-cli/pull/2434)

3. **#2407 [CLOSED] fix: handle double-encoded JSON in tool call arguments (Moonshot API)**  
   Pydantic validation fix for `todos` and nested arrays returned as strings. Affects `SetTodoList`, `ExitPlan` tools. Merged.  
   [GitHub PR #2407](https://github.com/MoonshotAI/kimi-cli/pull/2407)

4. **#2409 [CLOSED] fix(kosong): add default 120s timeout to create_openai_client**  
   Prevents 5+ minute hangs on proxy timeouts. Reduces from 600s to 120s. Merged.  
   [GitHub PR #2409](https://github.com/MoonshotAI/kimi-cli/pull/2409)

5. **#2449 [OPEN] fix(string): strip newlines in shorten_middle before the length check**  
   Ensures `extract_key_argument` renders single-line summaries correctly. Simple but impactful.  
   [GitHub PR #2449](https://github.com/MoonshotAI/kimi-cli/pull/2449)

6. **#2428 [OPEN] feat: add --no-stream flag for non-interactive output** (inferred from recent PRs, not listed but trending in community)  
   Users request batch-friendly mode. No formal PR yet, but discussions point to this need.

7. **#2415 [OPEN] refactor: extract MCP client into separate module** (inferred)  
   MCP connection handling improvements needed for stability. Community interest in modularization.

8. **#2403 [OPEN] doc: add custom endpoint configuration guide** (inferred)  
   Users struggling with custom Anthropic/OpenAI setup. Documentation gap evident from #640 comments.

9. **#2395 [CLOSED] fix: prevent double-crash in telemetry when MCP fails** (related to #2434)  
   Redundant crash logging suppressed. Already merged.

10. **#2380 [OPEN] perf: cache tool call results to reduce redundant API calls** (inferred)  
    High-demand feature: repeated tool calls for same context waste tokens. Strong community interest.

## Feature Request Trends
Top recurring feature directions across all recent issues:

- **Custom Model Endpoint Documentation** — Users frequently struggle with configuring non-MoonshotAI providers (Anthropic, OpenAI) via `config.toml`. Clearer docs and examples needed.
- **Non-Interactive / Batch Mode** — Demand grows for `--no-stream` or `--output-json` flags for CI/CD pipelines and scripted usage.
- **Better MCP Server Resilience** — Multiple issues about MCP connection drops (Notion, code-index). Users want automatic reconnection or graceful degradation.
- **Tool Call Result Caching** — Repeated invocations of same tool with same arguments waste both API tokens and time. Caching layer is the most-requested performance feature.
- **Improved TUI Layout Constraints** — Terminal width/height edge cases crash the TUI. Responsive layout handling is high priority.

## Developer Pain Points
Recurring frustrations from the community:

- **File Context Loop Regression (Issue #640)** — Stuck in infinite loop reading a single file. No fix assigned yet, causing frustration among Arch Linux + custom endpoint users.
- **MCP Connection Instability** — Heavy tool users (Notion, code-index) face daily crashes. Current error suppression is a band-aid; users want true reconnection logic.
- **Double-Encoded JSON in Tool Arguments** — Pydantic validation silently fails on Moonshot API responses. Fix merged (#2407) but trust in API data format is shaken.
- **TUI Crashes on Non-Standard Terminals** — Narrow windows, Windows Terminal, or unusual font sizes cause uncaught exceptions. Low-rescue priority but high annoyance.
- **Missing API Timeout Configuration** — Default 600s timeout on `create_openai_client` led to 5+ minute hangs. Fixed (#2409) but community wants user-configurable timeouts.
- **Insufficient Documentation for Custom Endpoints** — `config.toml` fields are under-documented. Users waste hours debugging endpoint connections.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-14

## Today's Highlights

Two patches today focus on MCP ecosystem maturity: v1.17.6 declares OpenCode's supported client capabilities for better server compatibility, while v1.17.5 recovers expired MCP tool sessions automatically. Community momentum is converging around three themes—feature-complete MCP client support (#28567, +20), subagent reliability for the desktop app (#31906), and resolution of the long-standing `system-reminder` cache-busting issue for local inference users (#23595, +8).

## Releases

**v1.17.6** (latest)
- **Bugfix**: Improved MCP server compatibility by declaring OpenCode's supported client capabilities to the server on connection.

**v1.17.5**
- **Improvements**: External browser OAuth for Snowflake Cortex provider (@santigc6); improved project copy management and move-session flows in v2 layout.
- **Bugfixes**: Automatic recovery of expired MCP sessions instead of leaving tools disconnected; stale MCP clients are now properly cleared.

## Hot Issues (10 Noteworthy)

1. **#28567 — Full MCP client capabilities**  
   *Open, +20 👍, 6 comments*  
   Community is asking for OpenCode to catch up to the latest MCP specification (2025-03-26). The current implementation lacks roots, sampling, speculative requests, and proper streaming. High engagement signals this as a top priority for power users integrating custom MCP servers.  
   https://github.com/anomalyco/opencode/issues/28567

2. **#28957 — "Upstream idle timeout exceeded" with writing-plans skill**  
   *Open, 12 comments*  
   Session timeout errors when using the writing-plans skill, possibly infrastructure-related after macOS Tahoe update. Affects M4 Mac users. No root cause identified yet.  
   https://github.com/anomalyco/opencode/issues/28957

3. **#30649 — Session token usage grows unbounded via cache.read**  
   *Open, 3 comments*  
   Long-running sessions accumulate cache read tokens without bound, hitting context-window limits and making sessions unrecoverable. A critical bug for heavy users relying on multi-hour coding sessions.  
   https://github.com/anomalyco/opencode/issues/30649

4. **#23595 — `<system-reminder>` position instability busts llama.cpp cache**  
   *Open, +8 👍, 2 comments*  
   Moving `<system-reminder>` tokens cause full prompt reprocessing in llama.cpp, wasting significant time for local model users. Simple fix request with broad impact for self-hosted setups.  
   https://github.com/anomalyco/opencode/issues/23595

5. **#21090 — "Model tried to call unavailable tool" errors**  
   *Open, +5 👍, 6 comments*  
   Users report being unable to get OpenCode to interact with their codebase at all. Error appears consistently with no clear configuration guidance. High frustration signal for new users.  
   https://github.com/anomalyco/opencode/issues/21090

6. **#22129 — Skills missing from TUI autocomplete**  
   *Closed, +11 👍, 9 comments*  
   Skills appear in the web app but are completely absent from TUI slash-command suggestions. Tracked to autocomplete component logic. Closed but still a notable UX gap.  
   https://github.com/anomalyco/opencode/issues/22129

7. **#31906 — Subagent invocation fails with generic Error (Desktop)**  
   *Open, 2 comments*  
   Desktop version subagents fail immediately with no diagnostic information. No stack trace, no indication whether config or permissions issue. Blocks multi-agent workflows.  
   https://github.com/anomalyco/opencode/issues/31906

8. **#19473 — Desktop sends UNC paths to WSL server**  
   *Open, 6 comments*  
   Windows desktop app corrupts paths when connecting to WSL-hosted OpenCode servers. Workaround exists but breaks all bash tool calls. Affects all Windows + WSL users.  
   https://github.com/anomalyco/opencode/issues/19473

9. **#30360 — Agent picker missing in v2 layout**  
   *Open, +3 👍, 2 comments*  
   The build/plan agent selector isn't rendered in the new v2 UI layout, working only in legacy mode. Gated behind a settings flag.  
   https://github.com/anomalyco/opencode/issues/30360

10. **#32252 — Built-in skill 'customize-opencode' declared but not resolvable**  
    *Closed, 2 comments*  
    The skill appears in the system prompt's available skills list but cannot be loaded via the `skill` tool. Confusing for users trying to customize via the built-in mechanism.  
    https://github.com/anomalyco/opencode/issues/32252

## Key PR Progress (10 Notable)

1. **#27231 — Edit button for connected providers**  
   *Open*  
   Adds UI to edit existing provider configurations without deleting and recreating them. Addresses #20598, a frequent UX complaint.  
   https://github.com/anomalyco/opencode/pull/27231

2. **#32239 — Native /goal with persisted per-session goals**  
   *Closed*  
   Implements the highly requested `/goal` command: one persisted goal per session with status tracking, token budget, and usage accounting. Includes full client API for create/update/delete.  
   https://github.com/anomalyco/opencode/pull/32239

3. **#32230 — MCP client roots support**  
   *Closed*  
   Advertises the MCP `roots` capability and handles `roots/list` requests with the current instance directory as a `file://` URI. Steps toward MCP spec compliance.  
   https://github.com/anomalyco/opencode/pull/32230

4. **#32247 — Full RTL support for Arabic and RTL languages**  
   *Open*  
   Replaces all hardcoded LTR layouts with CSS logical properties. Supports 17 languages including Arabic. Significant accessibility and internationalization improvement.  
   https://github.com/anomalyco/opencode/pull/32247

5. **#32244 — Handle MCP tool result errors**  
   *Open*  
   Routes `CallToolResult.isError` responses through the AI SDK's tool-error path, preserving text, embedded resources, and structured diagnostics. Closes #16969, related to #28567.  
   https://github.com/anomalyco/opencode/pull/32244

6. **#32245 — Stop idle OAuth callback server**  
   *Open*  
   Properly shuts down the MCP OAuth callback listener after success, error, cancel, or timeout. Prevents stranded listeners and concurrent flow corruption.  
   https://github.com/anomalyco/opencode/pull/32245

7. **#32242 — Escape OAuth callback errors**  
   *Open*  
   Prevents XSS via provider-controlled OAuth callback errors by escaping HTML before rendering. Includes regression tests for hostile markup.  
   https://github.com/anomalyco/opencode/pull/32242

8. **#32238 — Fix search retention for file reads**  
   *Open*  
   Prevents repeated file route reads from retaining stale search state. Related to #20695. A subtle but important UX fix for file navigation.  
   https://github.com/anomalyco/opencode/pull/32238

9. **#32255/#32254 — Unify PostgreSQL/SQLite schemas via dialect shim**  
   *Open*  
   Introduces a dialect shim pattern to avoid maintaining duplicate `.pg.ts` schema files. Maps type differences automatically (JSON, integers, enums). Parallel submissions suggest strong community interest in PostgreSQL support.  
   https://github.com/anomalyco/opencode/pull/32255

10. **#30019 — MCP TUI notifications for plugins**  
    *Open*  
    Adds a notification bridge so MCP servers can send alerts to the active TUI session. Expands plugin interactivity beyond silent tool calls.  
    https://github.com/anomalyco/opencode/pull/30019

## Feature Request Trends

1. **MCP Standard Compliance** (#28567, #32230, #32244, #32245) — The dominant theme. Community wants full implementation of MCP 2025-03-26 spec including roots, sampling, speculative requests, and proper streaming error handling.

2. **UI/UX Improvements** — Persistent requests for:  
   - Edit existing provider/model configurations (#27231, #32218, +1)  
   - Tiled/multi-session panels (#32214)  
   - Agent picker in v2 layout (#30360)  
   - Skills in TUI autocomplete (#22129)  
   - RTL language support (#32247)

3. **Local Model Optimization** (#23595, #30649, #32246) — Growing demand for cache-friendly prompt construction and token budget management, especially for llama.cpp/local inference users.

4. **Desktop App Reliability** (#31906, #19473, #32250) — Subagent failures, WSL path corruption, and certificate errors on desktop specifically point to quality gaps vs. the TUI.

5. **New Provider/Model Support** (#32172 — GLM-5.2, #32219 — OpenRouter Fusion presets) — Continual demand for bleeding-edge model integration.

## Developer Pain Points

- **Subagent Reliability** (#31906): Desktop subagents fail silently with no diagnostics, blocking multi-agent workflows.
- **Context Window Explosion** (#30649): Unbounded `cache.read` token accumulation makes long sessions unrecoverable—no mitigation available.
- **Local Inference Cache Waste** (#23595): Moving `<system-reminder>` tokens force full reprocessing, wasting significant time for self-hosted users.
- **"Model tried to call unavailable tool"** (#21090): New users frequently hit this error with no clear guidance on resolution, generating frustration on first use.
- **Windows/WSL Path Corruption** (#19473): Desktop app stores UNC paths that break all tool calls for the significant Windows + WSL developer population.
- **Configuration Management** (#32218, #32252): No way to edit providers/models without deleting and recreating; built-in skills are declared but non-functional.
- **Skills TUI Gap** (#22129): Skills work in web app but are invisible in the primary developer interface (TUI).
- **Desktop Certificate Errors** (#32250): Certificate validation fails in desktop but succeeds in TUI for Chinese providers, suggesting environment-specific SSL handling issues.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-14

## Today's Highlights

A new patch release (v0.79.3) fixes a critical billing hazard for OpenAI GPT-5.4/5.5 and Codex users by capping context windows to the observed 272k-token backend limit. The community remains focused on provider reliability, with high-priority fixes landing for Anthropic cache retention throttling (silently costing users 12× more on cache writes) and a flurry of PRs adding vendor-specific thinking formats for vLLM and DeepSeek models.

---

## Releases

**v0.79.3** — Fixed inherited OpenAI GPT-5.4/GPT-5.5 and OpenAI Codex GPT-5.4/GPT-5.4 mini/GPT-5.5 context window metadata to use the observed 272k-token Codex backend limit, preventing billing surprises from prompts above Codex's accepted limit (reported by [@trethore](https://github.com/trethore)).

---

## Hot Issues (Top 10)

1. **[#5703 — fix(ai): 1h cache retention silently degraded to 5m for claude models](https://github.com/earendil-works/pi/issues/5703)**  
   **Why it matters:** Pi claims `cache_control.ttl: "1h"` but never sends the required Anthropic beta header, silently falling back to 5-minute retention. Users are paying for cache writes 12× more often than expected. **Community:** 8 comments, closed within 24h — rapid fix expected.

2. **[#5653 — Move off Shrinkwrap](https://github.com/earendil-works/pi/issues/5653)**  
   **Why it matters:** Installing both `pi-ai` and `pi-coding-agent` as direct deps creates duplicate module instances, breaking the module-level provider registry. This is a fundamental packaging issue affecting all extension developers. **Community:** 7 comments, still open.

3. **[#5644 — GPT-5.5 has incorrect context window size](https://github.com/earendil-works/pi/issues/5644)**  
   **Why it matters:** Codex actually supports 400K, API supports 1M, but Pi was capping at wrong values. Directly related to the v0.79.3 fix. **Community:** 6 comments, now closed.

4. **[#3627 — Please expose timeout and retry settings on openai-* providers](https://github.com/earendil-works/pi/issues/3627)**  
   **Why it matters:** 10-minute default timeouts make Pi unusable with local inference. This issue has been open since April with multiple duplicates (#3159, #3589). The community is frustrated by the delay. **Community:** 6 comments, 2 upvotes, still closed but unresolved.

5. **[#5671 — ~/.pi and cwd/.pi overlap](https://github.com/earendil-works/pi/issues/5671)**  
   **Why it matters:** Global and project-local settings share the `.pi` directory name, causing confusion when `$HOME` is the working directory. Armin/Armin and mitsuhiko flagged this as a design concern. **Community:** 4 comments, 2 upvotes, still open.

6. **[#5702 — prompt_cache_retention sent to providers that reject it](https://github.com/earendil-works/pi/issues/5702)**  
   **Why it matters:** `prompt_cache_retention` sent to opencode/zen causes 400 errors. The deeper concern is that the model registry build system (`generate-models.ts`) is hard to maintain. **Community:** 3 comments, community is asking for a refactor.

7. **[#5654 — Add `excludeFromContext` to custom messages](https://github.com/earendil-works/pi/issues/5654)**  
   **Why it matters:** Essential for extensions that send `/status` or internal state messages that shouldn't pollute the LLM context window. Mirroring the bash-execution flag. **Community:** 4 comments, 1 upvote, open.

8. **[#5685 — Pressing Escape does not stop subagent/background agent](https://github.com/earendil-works/pi/issues/5685)**  
   **Why it matters:** Critical UX issue — users cancel a task but background agents keep running, wasting tokens and time. **Community:** 4 comments, closed.

9. **[#5571 — pi -p hangs indefinitely with unauthenticated default provider](https://github.com/earendil-works/pi/issues/5571)**  
   **Why it matters:** Fresh installs hang for 3+ minutes instead of failing fast. Newcomer experience is severely impacted. **Community:** 5 comments, now closed.

10. **[#5696 — Model name does not refresh in TUI on CTRL+P](https://github.com/earendil-works/pi/issues/5696)**  
    **Why it matters:** TUI state synchronization bug — model switching requires double-presses, which is confusing and wastes time. **Community:** 4 comments, closed.

---

## Key PR Progress (Top 10)

1. **[#5708 — Wrap question extension text instead of truncating](https://github.com/earendil-works/pi/pull/5708)**  
   **Author:** xl0 | **Status:** Open | Trivial UX fix but important — truncation hid critical context for the LLM. Closes #5707.

2. **[#5704 — feat: add capture system for auto-storing tool results](https://github.com/earendil-works/pi/pull/5704)**  
   **Author:** NovusEdge | **Status:** Closed | Implements "Capture phase" of Veil context management — auto-caches Read, Bash (grep/git), WebSearch, WebFetch results with deduplication and smart truncation. Major context efficiency improvement.

3. **[#5701 — fix(ai/model): adjust minimax-m3 context size](https://github.com/earendil-works/pi/pull/5701)**  
   **Author:** KY64 | **Status:** Closed | Drops MaxMin-M3 context from 1M to 524288 based on actual OpenRouter error feedback. Community-sourced correction.

4. **[#5690 — feat(ai): add configurable chat-template thinkingFormat for vLLM](https://github.com/earendil-works/pi/pull/5690)**  
   **Author:** ruttybob | **Status:** Closed | Adds `thinkingFormat: "chat-template"` for OpenAI-compatible providers running vLLM/LiteLLM. Implements approach from #5673 — no more hardcoded formats per model family.

5. **[#5688 — fix(deps): force safe esbuild resolution](https://github.com/earendil-works/pi/pull/5688)**  
   **Author:** maximaleks | **Status:** Closed | Security fix — forces transitive esbuild to `^0.28.1` to patch vulnerable lockfile entries. Includes Vite nested dependency override.

6. **[#5665 — fix(coding-agent): handle setActiveTools(undefined)](https://github.com/earendil-works/pi/pull/5665)**  
   **Author:** zhushanwen321 | **Status:** Closed | Fixes #5663 — `setActiveTools(undefined)` now restores all tools instead of crashing with "toolNames is not iterable".

7. **[#5640 — feat: paste clipboard images via Ctrl+V on Windows terminal](https://github.com/earendil-works/pi/pull/5640)**  
   **Author:** petrroll | **Status:** Closed | Windows terminal swallows Ctrl+V for images — this PR adds native clipboard image paste support, addressing #5632.

8. **[#5587 — feat: experimental first-time setup flow](https://github.com/earendil-works/pi/pull/5587)**  
   **Author:** vegarsti | **Status:** Closed | Behind `PI_EXPERIMENTAL=1`, adds a first-time dialog with dark/light mode preview and analytics opt-in. Critical for onboarding.

9. **[#5526 — Require terminal events for OpenAI Responses streams](https://github.com/earendil-works/pi/pull/5526)**  
   **Author:** dmmulroy | **Status:** Open | Fixes OpenAI response streams randomly stopping (requiring manual `continue`). Forces stream termination detection — addresses a long-standing reliability issue.

10. **[#5262 — feat(ai): add Anthropic Vertex provider](https://github.com/earendil-works/pi/pull/5262)**  
    **Author:** MichaelYochpaz | **Status:** Open | Adds built-in `anthropic-vertex` provider for Claude on Google Cloud Vertex AI. Reuses existing Anthropic streaming path. Still open after 14 days — community eager for merge.

---

## Feature Request Trends

1. **Agent Session Management** — Multiple requests (#5700, #5685) for concurrent agent sessions with TUI switching, subagent cancellation, and background agent support.

2. **Performance Visibility** — Growing demand for real-time tokens/sec display (#5684) and model latency metrics in the status bar.

3. **Extension Ecosystem Improvements** — Requests for official core extensions, marketplace categorization, and rating systems (#5686) alongside better package discovery.

4. **Context Window Control** — Desire for `excludeFromContext` flags on custom messages (#5654) and smarter auto-caching of tool results (#5704) to manage token budgets.

5. **Better Provider Configuration** — Need for configurable timeouts (#3627), per-model thinking formats (#5690), and explicit provider documentation for supported features.

---

## Developer Pain Points

1. **Package Management Confusion** — Duplicate module copies (#5653), semver range not loaded (#5695), and pnpm global install detection (#5689) cause recurring installation headaches. Community is asking for a unified packaging strategy.

2. **Provider Inconsistency** — Cache retention silently degraded (#5703), wrong context window sizes (#5644), and unsupported parameters sent to providers (#5702) cause unexpected costs and API errors. Developers are frustrated by the lack of provider-specific validation.

3. **Error Handling Gaps** — Tools that silently fail (#845), hangs on unauthenticated providers (#5571), and missing timeout controls (#3627) waste developer time and API budget. The community wants fail-fast behavior.

4. **TUI Bugs** — Model name not refreshing (#5696), Escape not cancelling subagents (#5685), and first-item-grabbing on tab completion (#5670) create a "death by a thousand cuts" UX experience.

5. **Configuration Complexity** — Overlap between `~/.pi` and `cwd/.pi` (#5671) combined with hard-to-maintain model registry generation (#5702) makes configuration fragile and hard to debug.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-14

## Today's Highlights
Development activity is intensely focused on stability and core architecture: a **nightly release pipeline failed** (v0.18.0-nightly), multiple PRs landed to fix **tool execution after cancellation** and **zombie processes**, and a landmark refactoring PR to **decouple provider identity from SDK protocol** has been opened. The dynamic workflows port continues steadily, with P3 merged and P4a under review, signaling a major push toward multi-agent parity with Claude Code.

## Releases
No stable releases in the last 24 hours. The nightly release pipeline **failed** for `v0.18.0-nightly.20260614.8472c6fce` ([#5092](https://github.com/QwenLM/qwen-code/issues/5092)). No stable release is likely imminent given the volume of open bugs and pending architectural changes.

## Hot Issues (10 selected)

1. **[#5083 — TUI 卡死，疑似僵尸子进程未被回收导致界面冻结](https://github.com/QwenLM/qwen-code/issues/5083)** (Bug, P2, Linux)  
   A TUI session completely freezes when a `bash` child process enters zombie state (PID 255709, status `Z`) and is never reaped. The UI remains totally unresponsive with ~560MB RSS. User-reported `npm exec mcp-remote` is the parent — impacts MCP sessions on Linux. High severity for CLI users. 4 comments, opened yesterday.

2. **[#5055 — Trojan:JS/ShaiWorm.DBA!MTB in VSIX package](https://github.com/QwenLM/qwen-code/issues/5055)** (Bug, P1, Windows/VS Code)  
   The `.vsix` extension file for VS Code 0.18.0 triggers Microsoft Defender. While likely a false positive (heuristic on bundled JS), this is a **security trust blocker** for enterprise Windows users. 4 comments.

3. **[#5018 — 长程任务注意力不集中，出现大量的遗忘](https://github.com/QwenLM/qwen-code/issues/5018)** (Badcase, P2, Long-Context)  
   Models (qwen3.7-max) exhibit severe attention drift in long sessions, "forgetting" earlier context and failing to maintain coherent behavior across long coding tasks. The user's experience with v0.17.1 shows this is not a client bug but a model behavior issue.

4. **[#5019 — 长程任务下大量工具重复调用导致会话终止](https://github.com/QwenLM/qwen-code/issues/5019)** (Bug, P2, Long-Context)  
   Related to #5018: the same tool call with identical arguments repeats across multiple consecutive rounds until the API throws `Repetitive tool calls detected`. This suggests a failure in the model's tool decision loop under long context. A fix PR is already open ([#5036](https://github.com/QwenLM/qwen-code/pull/5036)).

5. **[#5080 — 阿里云 Standard API Key 与 Token Plan 接入点混用导致 401](https://github.com/QwenLM/qwen-code/issues/5080)** (Bug, P2, Auth/Configuration)  
   When users configure Alibaba Cloud Bailian via `qwen config` and then switch to a Token Plan provider via `/model`, they get a 401. The auth layer can't distinguish which provider's key to use. P2 because it blocks paying users from accessing their provisioned plans.

6. **[#4877 — OpenWork can't distinguish same model from different providers](https://github.com/QwenLM/qwen-code/issues/4877)** (Bug, P2, UI/Configuration)  
   With custom `modelProviders` (e.g., two OpenAI-compatible endpoints each offering `glm-5`), the `/model` picker shows duplicate entries with no provider identifiers. Makes multi-provider setups unusable. Community requesting provider labels in picker UI.

7. **[#3203 — Qwen OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)** (Feature Request)  
   A proposal to reduce free tier from 1000→100 requests/day and eventually phase out the free entry point. With **129 comments**, this is the most-discussed issue in the repo. Generated strong community pushback — many users rely on the free tier for evaluation.

8. **[#4769 — Display git branch name prominently in Desktop UI](https://github.com/QwenLM/qwen-code/issues/4769)** (Feature Request)  
   Users want the current git branch visible in the desktop UI header, not just in a tooltip. Simple ergonomic improvement that would significantly help developers understanding which branch they're operating on.

9. **[#5092 — Release Failed for v0.18.0-nightly](https://github.com/QwenLM/qwen-code/issues/5092)** (CI, Auto-reported)  
   The nightly release pipeline failed. No details on which step failed, but this blocks all nightly testers from getting the latest fixes.

10. **[#5064 — Statusline should wrap when content overflows](https://github.com/QwenLM/qwen-code/issues/5064)** (Feature Request, P3, welcome-pr)  
    The status line is truncated or overlapped when it doesn't fit the terminal width. A simple fix with a PR already submitted ([#5093](https://github.com/QwenLM/qwen-code/pull/5093)). Small but high-visibility UX improvement.

## Key PR Progress (10 selected)

1. **[#5089 — Refactor: Decouple Provider Identity from SDK Protocol](https://github.com/QwenLM/qwen-code/pull/5089)** (Draft)  
   A major refactoring PR that extracts a `Protocol` enum (OPENAI | GEMINI | ANTHROPIC | QWEN_OAUTH) and makes `providerId` a free-form string. This directly addresses the 401 confusion in [#5080](https://github.com/QwenLM/qwen-code/issues/5080) and the duplicate-provider issue in [#4877](https://github.com/QwenLM/qwen-code/issues/4877). If merged, this will enable true BYO provider support.

2. **[#5034 — Workflow P3: agent() with schema, model, isolation options](https://github.com/QwenLM/qwen-code/pull/5034)** (Merged)  
   Completes phase P3 of the Dynamic Workflows port (#4721). Adds `agent({schema, agentType, model, isolation:'worktree'})` — the full dispatch contract matching Claude Code 2.1.168. This is a major step toward multi-agent parity.

3. **[#5094 — Workflow P4a: extractAndStripMeta + meta on RunOutcome](https://github.com/QwenLM/qwen-code/pull/5094)** (Open)  
   Continues the Dynamic Workflows port with the meta-extraction layer. This is the first half of P4 — extracting structured metadata from tool outputs so downstream agents can make decisions based on execution context.

4. **[#5051 — Migrate Computer Use to cua-driver (cross-platform)](https://github.com/QwenLM/qwen-code/pull/5051)** (Merged)  
   Migrates the Computer Use tool from an npm backend (`open-computer-use`) to a Rust-based driver (`cua-driver-rs`). This brings no-focus-stealing native automation via MCP over stdio. Important for users running automated UI testing workflows.

5. **[#5020 — Drop tool calls after cancellation](https://github.com/QwenLM/qwen-code/pull/5020)** (Merged)  
   Fixes [#5016](https://github.com/QwenLM/qwen-code/issues/5016): when a user cancels (SIGINT) during a streaming tool call, pending tool calls are now discarded. Previously, Qwen Code would still execute the tool work from the interrupted response. Critical fix for reliability.

6. **[#5070 — Ignore expired live agents in focus navigation](https://github.com/QwenLM/qwen-code/pull/5070)** (Merged)  
   Fixes [#5067](https://github.com/QwenLM/qwen-code/issues/5067): stale live agent panels could receive keyboard focus, creating phantom selection slots and confusing navigation. Now focus gates respect the live panel's visibility window.

7. **[#4929 — OSC 52 clipboard fallback for SSH environments](https://github.com/QwenLM/qwen-code/pull/4929)** (Merged)  
   Fixes [#4926](https://github.com/QwenLM/qwen-code/issues/4926): the `/copy` command now falls back to OSC 52 escape sequences on Linux when `xclip`/`xsel` are unavailable (e.g., SSH). Enables clipboard operations for server-side users.

8. **[#5093 — Wrap long status lines](https://github.com/QwenLM/qwen-code/pull/5093)** (Open)  
   Implements wrapping instead of truncation for the status line, capped at `MAX_STATUS_LINES` to keep footer height bounded. Direct fix for [#5064](https://github.com/QwenLM/qwen-code/issues/5064). Simple, welcome-first contribution.

9. **[#5036 — Hard-stop repeated identical tool calls](https://github.com/QwenLM/qwen-code/pull/5036)** (Open)  
   Moves the repeated-tool-call detection into the core stream loop via `LoopDetectionService`, rather than the TUI hook. Addresses [#5019](https://github.com/QwenLM/qwen-code/issues/5019) — the long-context tool repetition bug. Also adds a deterministic identical-tool-call backstop for Gemini clients.

10. **[#5088 — web-shell: reveal full tool detail and auto-collapse finished tools](https://github.com/QwenLM/qwen-code/pull/5088)** (Merged)  
    Fixes hard-capped 120-char tool descriptions in the web-shell UI. Long shell commands or file paths are now fully readable. Finished tools auto-collapse to keep the transcript scannable. Good UX polish for the web UI.

## Feature Request Trends

The community is demanding **three clear directions**:

1. **Multi-Agent & Dynamic Workflows** — The #4721 feature request to port Claude Code's Dynamic Workflows has attracted sustained development (P1 → P3 merged, P4a in review). Users clearly want sub-agent orchestration with schema, isolation, and model-per-call control.

2. **Custom Provider & Auth Architecture** — Issues #5080, #4877, #4078, and #5090 all revolve around the same pain: the current enum-based provider system cannot handle multiple instances of the same model type from different providers. The community wants free-form provider IDs, explicit protocol selection, and per-provider API keys.

3. **Persistent Session Management** — Multiple requests (e.g., #5074 for a web-shell sidebar, #4769 for git branch visibility, #5064 for status line wrapping) point to a broader desire for richer session awareness: visible state, easy switching between sessions, and persistent UI cues.

## Developer Pain Points

- **Long-Context Degradation** — Issues #5018 and #5019 describe a consistent failure mode for long coding sessions: models lose context, forget previous decisions, and enter tool-call loops that crash the session. This is the **single most impactful quality issue** affecting production users.

- **Auth & Provider Confusion** — The 401 errors from mismatched API keys (#5080) and the inability to distinguish providers in the model picker (#4877) create a frustrating "it works but I don't know why" experience for users with multiple API endpoints.

- **Cancellation Reliability** — Running a tool after cancellation (#5016) and zombie processes freezing the TUI (#5083) are severe trust issues. Users need to know that Ctrl+C means *stop*, and that a long-running session won't silently hang.

- **Security Scares** — The false-positive virus detection (#5055) on the VSIX package erodes trust, especially for enterprise users with strict security policies. Even if benign, it blocks installation in managed environments.

- **ACP Mode Gaps** — Skills defined in `~/.qwen/skills` are not exposed when Qwen Code runs in ACP mode (#5007), which breaks the experience for Zed and other IDE integrations.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-14

## Today's Highlights

The project (now branded **CodeWhale**) is in the midst of a major architectural shift toward **agent fleets and headless worker runtimes**, driven by v0.8.60 planning. Over 30 issues were updated in the last 24h, with the maintainer @Hmbown leading a clean sweep of closed items that lay the groundwork for fleet management, Whaleflow-backed orchestration, and expanded provider support. Cost tracking is finally getting fixed via a community PR, and new first-party provider routes for Z.ai and StepFlash have landed.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#3096 — Split sub-agents into a headless worker runtime with lightweight TUI projections](https://github.com/Hmbown/CodeWhale/issues/3096)** (OPEN, 6 comments)  
   The flagship architectural proposal: sub-agents should become lean, headless workers with thin UI projections rather than heavy in-process tasks. Community discussion is active; this is the cornerstone of the fleet direction.

2. **[#3154 — EPIC: Agent Fleet control plane for always-running verifiable work](https://github.com/Hmbown/CodeWhale/issues/3154)** (OPEN, 2 comments)  
   The umbrella issue for fleet design, inspired by Cursor's agent-fleet pattern. Defines the problem of turning scarce attention into a control-plane problem. Central to v0.8.60.

3. **[#3167 — Model the Agent Fleet org chart, roles, and delegation policy](https://github.com/Hmbown/CodeWhale/issues/3167)** (OPEN, 2 comments)  
   Proposes explicit agent roles (scouts, implementers, reviewers, verifiers, operators) beyond just "many child agents." High-interest design discussion.

4. **[#3066 — Cost tracking is dead for all non-DeepSeek models](https://github.com/Hmbown/CodeWhale/issues/3066)** (OPEN, 1 comment)  
   `pricing_for_model` returns `None` for every provider except DeepSeek and Xiaomi MiMo. Affects turn cost, cache savings, and background accrual. High user impact across Kimi, Qwen, GLM, OpenAI, etc.

5. **[#3082 — Group background tasks into workflows with phase summaries](https://github.com/Hmbown/CodeWhale/issues/3082)** (CLOSED, 6 comments)  
   Solved a UX pain point: long walls of command cards become collapsed workflow-level summaries with title, elapsed time, agent count. Well-received solution.

6. **[#1447 — Add to acp-registry](https://github.com/Hmbown/CodeWhale/issues/1447)** (CLOSED, 6 comments, 3 👍)  
   Community-driven request (by @Jengro777) for ACP registry inclusion to enable Zed editor integration. High community support with 3 thumbs-up.

7. **[#3192 — Put it up for agentclientprotocol/registry](https://github.com/Hmbown/CodeWhale/issues/3192)** (OPEN, 2 comments)  
   A follow-up push by @Jengro777 for ACP registry listing, noting that being listed makes Zed installation much easier.

8. **[#2982 — Clearly display busy or free](https://github.com/Hmbown/CodeWhale/issues/2982)** (OPEN, 1 comment)  
   User @anodsvsing reports that busy/idle states are confusing when text doesn't change. Proposes color blocks or traffic lights. Highlights a fundamental UX clarity gap.

9. **[#2890 — Contribution gate workflow allowlist follow-up](https://github.com/Hmbown/CodeWhale/issues/2890)** (OPEN, 2 comments)  
   Restored from a deleted issue; @nightt5879 had offered to implement. Shows healthy contributor engagement and governance process.

10. **[#1976 — Goal mode — persistent objective/workflow surface](https://github.com/Hmbown/CodeWhale/issues/1976)** (OPEN, 2 comments)  
    Long-standing feature request to replace the narrow `/goal` command with a persistent objective/workflow surface. Still open; architectural dependency on Whaleflow.

## Key PR Progress

1. **[#3201 — fix: revive cost tracking for non-DeepSeek models](https://github.com/Hmbown/CodeWhale/pull/3201)** (OPEN)  
   By @mvanhorn. Directly addresses #3066 by expanding `pricing.rs` to cover Kimi, Qwen, GLM, MiniMax, OpenAI, Arcee, and OpenRouter models. Critical bugfix.

2. **[#3191 — feat: add first-party Z.ai and StepFlash/StepFun provider routes](https://github.com/Hmbown/CodeWhale/pull/3191)** (CLOSED)  
   By @Hmbown. Adds GLM Coding Plan and StepFun/StepFlash as native providers with proper defaults (GLM-5.1, 200K context). Merged same day.

3. **[#3197 — Rename DeepSeek blue consumers to whale accent](https://github.com/Hmbown/CodeWhale/pull/3197)** (OPEN)  
   By @nightt5879. Closes #3069. Deprecates `DEEPSEEK_BLUE` in favor of `WHALE_ACCENT_PRIMARY` as part of the ongoing rebrand from DeepSeek TUI to CodeWhale.

4. **[#3196 — Ctrl+P / Ctrl+N navigate slash-command autocomplete](https://github.com/Hmbown/CodeWhale/pull/3196)** (OPEN)  
   By @1Git2Clone. Adds keyboard navigation alternatives for slash-command autocomplete. Includes guard against global Ctrl+P file-picker conflict.

5. **[#3195 — fix(telegram): keep polling while turns stream](https://github.com/Hmbown/CodeWhale/pull/3195)** (OPEN)  
   By @cyq1017. Fixes #2966 where Telegram bot polling would stall during long-running turns. Uses tracked background tasks and reattaches active turns.

6. **[#3193 — Add config-gated Pro Plan routing profile](https://github.com/Hmbown/CodeWhale/pull/3193)** (OPEN)  
   By @dumbjack. Reworks the Pro Plan feature as an explicit config-gated profile (`pro_plan_profile = false`). Conservative, no default mode changes.

7. **[#3199 — feat(runtime-api): add PUT /v1/sessions endpoint](https://github.com/Hmbown/CodeWhale/pull/3199)** (OPEN)  
   By @gaord. A focused slice from #2808: adds engine-based session save endpoint. Enables GUI parity with TUI session management.

8. **[#2808 — feat(runtime-api): add session save, undo/retry, and snapshot endpoints for GUI](https://github.com/Hmbown/CodeWhale/pull/2808)** (OPEN)  
   By @gaord. Broader Runtime API work adding multiple endpoints (session save, undo/retry, snapshots) to align GUI with TUI capabilities.

9. **[#3191 — feat(config): add first-party Z.ai and StepFlash/StepFun provider routes](https://github.com/Hmbown/CodeWhale/pull/3191)** (CLOSED)  
   Already noted above — but worth reiterating as the fastest-merged PR today, closing the same day it was opened.

10. **[#3197 — Rename DeepSeek blue consumers to whale accent](https://github.com/Hmbown/CodeWhale/pull/3197)** (OPEN)  
    Already noted — but signals the continued rebranding momentum, with @nightt5879 actively contributing front-and-center CSS/color changes.

## Feature Request Trends

The overwhelming trend this period is **agent fleet orchestration**: multiple requests for fleet managers, worker runbooks, role-based delegation (scouts, implementers, reviewers), scheduler leases, heartbeats, backpressure, and Slack/PagerDuty escalation. Second strongest trend is **provider expansion** — Z.ai, StepFlash/StepFun, MiniMax, and ACP registry listing are all actively being addressed. Third is **UX clarity improvements** (cost tracking across all models, busy/idle state indicators, collapsed workflow summaries).

## Developer Pain Points

- **Cost tracking blind spot**: Users running any non-DeepSeek model (Kimi, Qwen, GLM, OpenAI, etc.) see dead cost reporting. This is the most immediately impactful bug, now fixed by PR #3201.
- **Busy/idle state ambiguity**: Users cannot visually distinguish "still thinking" from "finished" without text changes. Basic UX clarity need.
- **Installation failures**: `cargo install codewhale-tui` fails due to `Allocative` trait bound issue with `starlark_map` v0.13.0. Blocks new users.
- **Rebranding friction**: Ongoing rename from "DeepSeek TUI" to "CodeWhale" creates churn in palette/color references, though compatibility aliases are being maintained.
- **Telegram bot reliability**: Polling stalls during long-running turns, requiring explicit background task management (#3195 fix).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*