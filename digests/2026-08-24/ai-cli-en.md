# AI CLI Tools Community Digest 2026-08-24

> Generated: 2026-08-24 00:31 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Ecosystem Comparison Report — 2026-08-24

## 1. Ecosystem Overview

The AI CLI tool landscape is maturing rapidly, with **Claude Code** and **OpenAI Codex** dominating community engagement while **Gemini CLI** and **Qwen Code** are actively hardening their agent architectures. Two cross-cutting themes dominate: **security hardening** (symlink traversal fixes, sandbox escape prevention, PAT isolation) and **reliability engineering** (compaction data loss, stream interruptions, session state corruption). A notable pattern is the **"Keep going" plague** — models stopping mid-generation or delivering silent thinking blocks — affecting Claude Code, OpenCode, and Codex users alike. Windows platform reliability remains the weakest link across nearly every tool, with GPU crashes, file-locking conflicts, and terminal rendering issues recurring universally.

---

## 2. Activity Comparison

| Tool | Issues (24h) | PRs (24h) | Release Status | Community Velocity |
|------|-------------|-----------|----------------|-------------------|
| **Claude Code** | 10 hot; 50+ active | 1 (docs) | v2.1.241 (patch) | High — 351👍 top issue, 4× next |
| **OpenAI Codex** | 10 hot; broad engagement | 10+ (8 merged, bot-heavy) | rust-v0.149.1 + alpha | High — 37👍 top issue, active bot-driven dev |
| **Gemini CLI** | 10 hot; P0/P1 focus | 10 (5 merged) | Nightly v0.56.0 | Medium — security PR closed, memory fixes merged |
| **GitHub Copilot CLI** | 10 hot; mostly new | 1 (spurious rename) | v1.0.81-8 (patch) | Medium — fewer comments, low upvotes |
| **Kimi Code** | 3 open (low activity) | 2 (both open) | None | Low — quiet window, 2 long-pending items |
| **OpenCode** | 10 hot; regressions cluster | 10 (all open) | None (v1.18.21 current) | High — 31-comment tool-calling issue, contributor surge |
| **Pi** | 8 closed/2 open | 10 (7 merged, 2 open) | None | Medium — steady merged PRs, provider interop focus |
| **Qwen Code** | 10 hot; security focus | 10 (mostly open) | Nightly v0.22.0 | Medium-High — active review-pipeline work |
| **DeepSeek TUI (Codewhale)** | 10 hot; v0.9.12 prep | 10 (6 closed) | v0.9.11 (rebrand milestone) | Medium — rebrand moment, structured roadmap |

**Notable**: Claude Code and OpenCode have the highest user engagement; Codex's merged PRs are algorithm-driven (copyberry[bot]); Kimi and Copilot CLI have the quietest community windows.

---

## 3. Shared Feature Directions

| Feature Direction | Tools | Specific Needs |
|-------------------|-------|----------------|
| **Context/Compaction Reliability** | Claude Code, Codex, Copilot CLI, Gemini CLI, Pi | Compaction dropping tool results (Copilot #4572), prompt cache instability (Claude #87966), session retention deleting unrelated sessions (Gemini #28981), compaction/retry state disagreement (Pi #7724) |
| **Memory Across Sessions** | Kimi (#1283), Gemini (Auto Memory), Copilot (store_memory breakage) | Persistent project context, prefs, and AI-managed notes; Gemini's Auto Memory retry loops and redaction gaps show immaturity |
| **Sandbox Networking Egress** | Claude Code (#28018 localhost), Gemini (#28935 Docker isolation), Copilot | Local service access without leaving sandbox; Claude's EPERM on socket connect is the top feature request (75👍) |
| **Windows Platform Reliability** | Claude (GPU crash #81698, #85199), Codex (DWM leaks #33192), Copilot (file-locking #4570), Qwen (pinyin #8625, MCP casing #9779), Pi (keybinding conflicts) | Cross-cutting Windows crater: crashes, handle leaks, terminal conflicts, path casing |
| **Mobile/Remote Session Control** | Gemini (#28982), Kimi (#2616), DeepSeek TUI (#5574) | Phone-as-spectator via gbr/1 protocol, veto actions on long-running agents — identical 3-way convergence |
| **Tool-Call Schema Validation** | Pi (#8521, #8513), OpenCode (#44567), Qwen (tool schemas) | Model-generated invalid args (raw control chars, null vs undefined) causing hard failures |
| **Auto-retry on Empty/Network Stops** | OpenCode (#44536), DeepSeek TUI (#5561), Gemini (#21409) | "Keep going" plague: empty finish_reason or reasoning-only clean stops treated as clean, forcing manual resubmits |
| **Provider-Neutral Core** | DeepSeek TUI (rebrand, 18 gates), Pi (strict OpenAI-compat), OpenCode (Ollama) | Multi-provider support exposing latent bugs; strict providers reject what lenient ones tolerate |
| **TUI/CLI Output Transparency** | Codex (#39903 "Ran N commands"), Pi (per-block expansion), OpenCode (Gantt) | Users want more control over execution visibility, not collapsed summaries |
| **Config Deprecation Hygiene** | Codex (approval_policy removal), Gemini (silent behavior shifts) | Hard errors on removed settings without migration paths erode trust |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach | Key Differentiator |
|------|--------------|-------------|--------------------|--------------------|
| **Claude Code** | Production-grade agent tool with desktop app | Enterprise/team workflows | Sandboxed execution, tracked tools, auto-mode | Deepest community trust + most feature-rich undo/review model |
| **OpenAI Codex** | Closed-loop agent with IDE + desktop + cloud | Pro subscribers, ChatGPT ecosystem users | Originator-gated context windows, guardian review threads | Tightest ChatGPT integration (20x weekly quota, scheduled automations) |
| **Gemini CLI** | Secure agent with strict sandboxing | Enterprise security-conscious users | P0 severity culture, rapid security hardening | Most aggressive security posture (symlink, Docker escape, Seatbelt) |
| **GitHub Copilot CLI** | Copilot ecosystem extension | Existing GitHub shop users | Plugin marketplace, ACP protocol, cloud mode | Deepest GitHub/Copilot platform integration |
| **Kimi Code** | Lightweight CLI | MoonshotAI API users | Simple architecture | Smallest surface area; community waiting on memory system |
| **OpenCode** | Open-source V2 architecture | DIY developers, local-model users | Effect schema, OpenTUI, codemode | Highest contributor velocity per issue; community-driven hardening |
| **Pi** | Extensible agent platform | Plugin/extension developers | Provider-agnostic core, llama.cpp/OpenAI-compat | Strongest provider interoperability discipline |
| **Qwen Code** | Fast-iterating agent with review pipeline | Chinese dev community + global | Web Shell + CLI parity, /review skill | Aggressive review-pipeline automation ambition |
| **DeepSeek TUI** | Provider-neutral agent (rebranding) | Cost-conscious users | Rust/Python hybrid, workflow execution | Structured v0.9.12 money-safety roadmap |

---

## 5. Community Momentum & Maturity

**High momentum / rapid iteration:**
- **OpenCode** — Contributor surge (kitlangton, gitRasheed, savagelysubtle) shipping fixes daily; broad infrastructure hardening; v2 in development
- **Claude Code** — Highest user engagement (351👍 quality regression); maintainers in bug-fixing cycle; feature requests gaining traction
- **Codex** — Bot-driven steady merges (10 PRs/24h); focused on content-annotation architecture; active alpha/beta release cadence

**Medium momentum / steady maturation:**
- **Gemini CLI** — Security hardening complete (symlink traversal closed); memory fixes merged; P0 bug culture clear
- **Qwen Code** — Systematic review-pipeline investment; Web Shell parity pushes; nightly release cadence
- **DeepSeek TUI** — Rebrand milestone reached (v0.9.11); v0.9.12 roadmap with P0 money-safety; structured cleanup
- **Pi** — Consistent merged PRs (7/24h); provider interop hardening; Windows gaps acknowledged

**Lower momentum / quiet windows:**
- **Kimi Code** — 3 issues, 2 PRs, no releases; possibly internal stabilization; community waiting on memory feature
- **Copilot CLI** — One patch release; few substantive PRs; enterprise auth issues lingering since March

---

## 6. Trend Signals

**1. "Money-safety" is the next product frontier.** DeepSeek TUI's v0.9.12 P0 work (runaway-spend bounds), Claude's prompt-cache dollar-cost reports (#87966), and Codex's silent quota consumption (#37445) all signal that **unattended spend control** is becoming a make-or-break feature for enterprise adoption.

**2. Model quality regression is the loudest cross-tool complaint.** Claude's #77136 (351👍, 4× next) and OpenCode's "Keep going" plague are symptoms of the same disease — **recent model versions degrade in long-form prose and mid-generation reliability**. AI CLI vendors are exposed to model-quality changes they don't control.

**3. Sandbox security is converging on "default-deny with explicit allowlists."** Gemini's symlink fix, Docker socket isolation, and Claude's localhost egress debate all point toward **fine-grained egress control** as the standard. The tension between safety and local-dev workflows is unresolved community-wide.

**4. Windows is the universal weak spot.** GPU crashes (Claude), DWM leaks (Codex), file-locking (Copilot), pinyin rendering (Qwen), keybinding conflicts (Pi) — every tool has Windows-specific issues. This is a **recurring platform tax** that vendors are slowly paying down.

**5. Compaction and context management is a hidden technical debt.** Copilot losing tool results, Claude's cache instability, Pi's compaction/retry disagreement, Gemini's session retention collision — **history management is the new concurrency problem**. Tools that solve this reliably gain a significant trust advantage.

**6. Cross-session and background agents are the next architecture wave.** Gemini's cross-session messaging (PR #9576), Codex's monitor workflows (#32993), DeepSeek's supervised operation stack (#5535) all push toward **agents that persist, collaborate, and self-heal** beyond single sessions.

**7. Auto-recovery is table stakes.** Empty-stop auto-retry (OpenCode), reasoning-only recovery (DeepSeek), stream-error surfacing (Pi) — communities expect tools to **detect abnormal model behavior and self-correct**, not require manual "Keep going" prompting.

---

*Data window: 2026-08-23 to 2026-08-24. Compiled from public GitHub issue/PR activity across 9 major AI CLI tools.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-08-24 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Skills have generated the most community discussion and attention:

**1. skill-creator fixes (PR #1298, #1099, #1050, #539)** — [PR #1298](https://github.com/anthropics/skills/pull/1298), [PR #1099](https://github.com/anthropics/skills/pull/1099), [PR #1050](https://github.com/anthropics/skills/pull/1050), [PR #539](https://github.com/anthropics/skills/pull/539)
*Status: Open*
The most active cluster of PRs targets the `skill-creator` meta-skill. The core issue (#556, 12 comments) reports that `run_eval.py` always returns 0% recall because the eval harness never triggers the skill under test — meaning the description-optimization loop has been optimizing against noise. Multiple independent fixes address Windows subprocess handling (`claude.cmd` not found via PATHEXT), stream reading on Windows pipes, eval-artifact installation, and YAML frontmatter parsing. These PRs represent a community-wide effort to make the skill-creation toolchain actually work on all platforms.

**2. document-typography skill (PR #514)** — [GitHub](https://github.com/anthropics/skills/pull/514)
*Status: Open*
A quality-control skill targeting typographic defects in AI-generated documents: orphan word wrap (1–6 words spilling onto the next line), widow paragraphs, and numbering misalignment. Addresses a universal pain point — every document Claude generates is affected. Discussion centers on scope validation and whether typography rules belong in the core document skills versus a separate skill.

**3. ODT skill for OpenDocument files (PR #486)** — [GitHub](https://github.com/anthropics/skills/pull/486)
*Status: Open*
Adds full OpenDocument support (.odt, .ods) including creation, template filling, and ODT→HTML conversion. Triggered by any mention of ODT/ODS/ODF/LibreOffice. Represents a meaningful gap in the official document skills, which currently cover PDF, DOCX, and PPTX only.

**4. pdf case-sensitivity fixes (PR #538)** — [GitHub](https://github.com/anthropics/skills/pull/538)
*Status: Open*
Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where file references (`REFERENCE.md` → `reference.md`, `FORMS.md` → `forms.md`) break on case-sensitive filesystems (Linux/macOS). A small but critical reliability fix that has stayed open for 5+ months.

**5. frontend-design skill clarity overhaul (PR #210)** — [GitHub](https://github.com/anthropics/skills/pull/210)
*Status: Open*
Revises the frontend-design skill to ensure every instruction is actionable within a single conversation and that guidance is specific enough to steer Claude's behavior without ambiguity. Community feedback focused on internal coherence and eliminating vague directives.

**6. DOCX tracked-change w:id collision fix (PR #541)** — [GitHub](https://github.com/anthropics/skills/pull/541)
*Status: Open*
Fixes document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks. Root cause: `w:id` is a shared ID space in OOXML across bookmarks, tracked changes, comments, and move ranges — the skill's hardcoded low IDs collide with existing bookmarks. Prevents silent document corruption in real-world usage.

**7. skill-quality-analyzer and skill-security-analyzer (PR #83)** — [GitHub](https://github.com/anthropics/skills/pull/83)
*Status: Open*
Adds two meta-skills to the marketplace: `skill-quality-analyzer` evaluates skills across five dimensions (structure, documentation, examples, and more), and `skill-security-analyzer` audits skills for security risks. A direct community response to the trust-boundary concerns raised in Issue #492.

**8. testing-patterns skill (PR #723)** — [GitHub](https://github.com/anthropics/skills/pull/723)
*Status: Open*
A comprehensive testing-skills package covering unit testing (AAA pattern, naming conventions), React component testing with Testing Library, and a Testing Trophy philosophy with clear "what to test vs. what NOT to test" guidance.

---

## 2. Community Demand Trends

The Issues data reveals the following highest-anticipated Skill directions:

- **Security and trust governance (Issue #492, 43 comments, 2 👍)** — The single most-discussed issue, alerting that community skills distributed under the `anthropic/` namespace enable trust-boundary abuse. Users may grant elevated permissions to community skills they believe are official. This is driving demand for skill security analyzers, provenance verification, and official vs. community skill labeling.

- **Org-wide skill sharing (Issue #228, 16 comments, 8 👍)** — High demand for sharing skills within organizations without manual file transfer. Currently users must download `.skill` files, send via Slack/Teams, and have colleagues manually navigate to Settings → Capabilities → Upload. A shared skill library or direct sharing link is requested.

- **Eval/trigger reliability (Issue #556, 12 comments, 7 👍)** — The eval harness reports 0% trigger rates across all queries, making skill-description optimization a blind process. This blocks iterative skill improvement and is the highest-priority tooling bug.

- **Duplicate skill prevention (Issue #189, 6 comments, 9 👍)** — Installing `document-skills` and `example-skills` plugins results in identical skills, duplicating content in the context window. Demand for dependency-aware plugin design.

- **Context-window optimization (Issue #1487, 4 comments)** — The `claude-api` skill eagerly injects ~156k tokens in a single tool call, exhausting the context window. Community demand for lazy-loading or size-capped skills.

- **Agent governance patterns (Issue #412, 6 comments)** — Proposal for a skill teaching Claude governance patterns for AI agent systems: policy enforcement, threat detection, trust scoring, and audit trails. Closed without merge but indicates forward-looking demand.

---

## 3. High-Potential Pending Skills

Active PRs that may land soon:

- **Hivemind: Zero-Cost Multi-Agent Orchestration (PR #1628)** — [GitHub](https://github.com/anthropics/skills/pull/1628) — Created 2026-08-21, most recent activity. Delegates mechanical work to headless opencode workers running on free models while Claude Code remains the planner/reviewer/merger. Addresses the "expensive model's context is the scarce resource" problem.

- **SCNet HPC Cluster skill (PR #1615)** — [GitHub](https://github.com/anthropics/skills/pull/1615) — Created 2026-08-20. Profile-based SSH and Slurm workflows for HPC cluster operation.

- **Self-audit skill (PR #1367)** — [GitHub](https://github.com/anthropics/skills/pull/1367) — Mechanical file verification plus four-dimension reasoning audit in damage-severity priority order. Universal across any project/tech stack/model.

- **Evaluation serialization fix (PR #1602)** — [GitHub](https://github.com/anthropics/skills/pull/1602) — Resolves multiple reliability, platform-compatibility, and metric-calculation bugs, including MCP result-text extraction and encoding stability.

- **Pyxel retro game development skill (PR #525)** — [GitHub](https://github.com/anthropics/skills/pull/525) — MCP server integration for the Pyxel retro game engine, covering write→run_and_capture→inspect→iterate workflows. Open for 5+ months with recent maintenance activity.

- **ServiceNow platform skill (PR #568)** — [GitHub](https://github.com/anthropics/skills/pull/568) — Broad ServiceNow assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD, CSM, SPM/PPM, Vulnerability Response, and more. Open since March with continued updates.

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is for **quality tooling around skills themselves** — reliable skill evaluation, security auditing, and context-window management — followed closely by document-format completeness (ODT, typography) and enterprise platform coverage (ServiceNow, HPC, SAP).

---

# Claude Code Community Digest — 2026-08-24

## 1. Today's Highlights
The community is abuzz over a long-running model-quality regression (#77136) where recent Claude models fall into repetitive rhetorical patterns despite explicit style instructions — the most-upvoted open issue at 351 👍. Meanwhile, **auto-mode's hardcoded "bashFirst" system prompt** is breaking core workflows: it causes `/rewind` to silently fail on Bash-edited files (#87575) and forces the model to bypass Edit/Write tools entirely (#88041). On the desktop front, Windows users are hit by a GPU process crash that kills all sessions (#81698), and a growing chorus demands **localhost/loopback egress from the sandbox** (#28018, 75 👍).

## 2. Releases
**v2.1.241** shipped within the last 24 hours with only "Bug fixes and reliability improvements" — no feature changes or breaking notes.
https://github.com/anthropics/claude-code/releases

## 3. Hot Issues
1. **[#77136 — Repetitive rhetorical tics in Claude 4.7/4.8/5.0/Fable prose](https://github.com/anthropics/claude-code/issues/77136)** — 92 comments, 351 👍. The volume of upvotes and the two-month-old thread indicates a broad, unresolved quality regression affecting all recent models. Poetic-but-empty phrasing ("delve," "tapestry") persists despite explicit style instructions. This is the community's #1 gripe.

2. **[#81698 — Windows desktop: GPU crash (exit 101457950) kills all sessions](https://github.com/anthropics/claude-code/issues/81698)** — 54 comments. NVIDIA RTX 5080 laptop GPU, driver 610.47. A single GPU process crash nukes every running Claude Code session, suggesting a process-hierarchy design flaw on Windows (MSIX package). No workaround yet.

3. **[#87575 — Auto mode /rewind silently fails on Bash-edited files](https://github.com/anthropics/claude-code/issues/87575)** — 18 👍. Auto mode's system prompt tells the model to use Bash for file edits, bypassing tracked Edit/Write tools — so `/rewind` can't restore anything. This is a fundamental design tension between auto-mode efficiency and undo reliability.

4. **[#88041 — Auto-mode hardcoded "bashFirst" instruction bypasses Edit/Write tools](https://github.com/anthropics/claude-code/issues/88041)** — 9 👍. The sibling issue to #87575. A community member found the offending template hardcoded in the CLI binary (`/opt/claude-code/bin/claude`), not in user config — meaning no settings.json fix exists; only a patch can resolve it.

5. **[#28018 — Sandbox blocks localhost/127.0.0.1 egress even when allowlisted](https://github.com/anthropics/claude-code/issues/28018)** — 8 comments, 75 👍. The most-upvoted *feature request* open right now. Integration tests against local Docker services are impossible in the sandbox. The `EPERM` on `sock.connect()` is a hard blocker for a whole class of local-dev workflows.

6. **[#85199 — Claude Desktop repeatedly crashes; only "Repair" fixes it on Windows](https://github.com/anthropics/claude-code/issues/85199)** — 34 comments. Distinct from the GPU crash (#81698) — this one requires manual "Advanced Options → Repair" each time. A second, independent stability crater on Windows.

7. **[#7134 — File encoding corruption: Windows-1252 not respected](https://github.com/anthropics/claude-code/issues/7134)** — 27 comments, 23 👍. A year-old bug still open. Claude Code assumes UTF-8 and corrupts legacy Windows-1252 files — a painful, silent data-loss issue for teams with legacy codebases. The age of the issue is itself a signal.

8. **[#87966 — Prompt cache fails mid-session; 89 full-context rewrites (~59M excess tokens)](https://github.com/anthropics/claude-code/issues/87966)** — 7 comments. A detailed cost-analysis report: `cache_read` becomes pinned to the stable-prefix boundary, causing repeated full-context rewrites across 9 days. Financial impact is concrete and measurable — this is the kind of bug that erodes trust in the platform's economics.

9. **[#74558 — Fable 5: mid-turn text intermittently delivered as "silent" thinking blocks](https://github.com/anthropics/claude-code/issues/74558)** — 9 comments. The model's assistant text is sometimes delivered as summarized thinking blocks, making turns appear silent. Reproduced in both on-disk transcripts and `stream-json` consumers — this is a wire-protocol/streaming bug, not a UI illusion.

10. **[#88747 — Worktree hooks path: absolute `core.hooksPath` leaks from main checkout](https://github.com/anthropics/claude-code/issues/88747)** — 3 comments. Fresh bug (created 2026-08-22). Worktree creation writes an *absolute* hooks path, so worktrees run the main checkout's hooks — a subtle and dangerous behavior for teams using worktree-based workflows.

Also notable: **Claude speaks broken Japanese on AWS Bedrock** (#88439, 1 comment, 4 👍) — localized-quality regression with a single report but potentially broad impact.

## 4. Key PR Progress
Only **one PR** was updated in the last 24 hours, so highlights are limited:
- **[#83374 — docs(plugin-dev): document MessageDisplay streaming semantics](https://github.com/anthropics/claude-code/pull/83374)** (OPEN, by iCodeCraft) — The bundled Hook Development skill lacks `MessageDisplay` in its trigger description, event guidance, and quick-reference table. This PR adds it to the plugin-development guidance. Small but necessary documentation hygiene for hook authors.

**Broader PR context (from preceding days, low activity is the story here):** The near-total absence of PR updates (1 in 24h) against 50+ issues with active comments suggests maintainers are in a bug-fixing cycle (reading from the v2.1.241 release notes) rather than a feature-merge cycle. The auto-mode "bashFirst" and GPU-crash issues are now old enough that the community expects either merged fixes or explicit acknowledgment soon.

## 5. Feature Request Trends
- **Sandbox networking: allow localhost/loopback egress (#28018, 75 👍)** — Highest-requested capability. Developers need to run integration tests against local Docker services (database, message brokers) from inside the sandbox. The current `EPERM` is a hard blocker.
- **Routines management: richer scheduled-tasks MCP (#73618)** — Community fleet operators need delete tool, grouping, and clearer paused-state for manual-only tasks. Currently they "abuse the description field" to work around gaps.
- **Terminal link/image affordances (#87438)** — macOS terminal: inline images, consistent clickable-text marking, and fix for schemeless markdown links failing with `-50` (iTerm2). A polish issue but with a concrete bug in the middle of it.
- **Mouse/UI: distinguish focus-click from option-click in AskUserQuestion (#76616)** — Small UX fix with clear expected behavior.

## 6. Developer Pain Points
- **Auto-mode is a trap.** The hardcoded "bashFirst" system prompt (#87575, #88041) silently defeats `/rewind` and bypasses the very Edit/Write tools that make Claude Code's undo and review model work. The community can't fix it via config — it's compiled into the binary. This undermines trust in auto-mode.
- **Windows desktop reliability is cratering.** Two independent crash classes (#81698 GPU-process kill-all, #85199 required-Repair) with 88 combined comments. The GPU crash nuking *all* sessions is a severe workflow loss.
- **Model output quality regression is the loudest issue.** #77136 has more than 4× the upvotes of the next issue. Long-form prose quality has degraded across model versions and the community is frustrated by the lack of movement in two months.
- **Prompt-cache instability has real dollar cost.** #87966's "89 full-context rewrites / ~59M excess tokens" is the kind of concrete, quantifiable cost that makes enterprises nervous. Cache behavior shifting mid-session is a silent budget-killer.
- **Local-first development is blocked at the network layer.** The sandbox's localhost egress block (#28018) combined with the LAN browser-pane blocking (#87472) means Claude Code cannot reach local or private-network services without leaving the sandbox, which defeats its purpose.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-24

## Today's Highlights

Two patch releases shipped (rust-v0.149.1 and rust-v0.149.0-alpha.4.3) with no public changelog details. The community remains most vocal about rate-limit consumption by background app activity (#37445, 13 comments, 10 👍) and the abrupt retirement of `approval_policy = "untrusted"` in 0.149.0 (#39973). A significant cluster of merged PRs (nearly all `copyberry[bot]`-authored) focuses on content annotation and metadata preservation across compaction, forking, and model switches — an internal architecture push with little direct user-facing impact.

## Releases

- **rust-v0.149.1** — Patch release; changelog links only to the diff from rust-v0.149.0 with no additional notes.
- **rust-v0.149.0-alpha.4.3** — Alpha patch release; no changelog details provided.

## Hot Issues

1. **[#39392 — Codex App with gpt-5.6-sol aborts with unsupported prompt_cache_retention](https://github.com/openai/codex/issues/39392)** · 39 comments · 37 👍 — The bundled app-server (codex-cli 0.148.0-alpha.15) crashes when using the flagship gpt-5.6-sol model with prompt caching enabled. High engagement suggests this affects many desktop users on the latest model.

2. **[#38350 — Recurring scheduled tasks disable themselves after successful runs](https://github.com/openai/codex/issues/38350)** · 34 comments — Scheduled automations in ChatGPT Web silently flip from enabled to paused with no user action. Four unrelated tasks disabled in one instance; trust in automations is eroding.

3. **[#25928 — VS Code/Cursor extension: submitted prompts randomly disappear before entering queue](https://github.com/openai/codex/issues/25928)** · 28 comments · 18 👍 — Long-standing (since June) Windows-only issue where prompts vanish before queueing in the IDE extension. High comment count indicates a reproducible, frustrating workflow breaker.

4. **[#37445 — Opening the ChatGPT desktop app silently consumes the Codex weekly limit](https://github.com/openai/codex/issues/37445)** · 13 comments · 10 👍 — Controlled experiment shows a fixed 6% weekly-limit deduction from background activity alone, with no user prompt. This is a serious trust/transparency problem for Pro subscribers managing their 20x weekly quota.

5. **[#39903 — Add option to disable "Ran N commands" collapsing in TUI](https://github.com/openai/codex/issues/39903)** · 12 comments · 27 👍 — Users want the TUI to always show executed commands rather than collapsing to a summary line. Strong demand (27 👍) for more transparency in terminal output.

6. **[#33192 — Windows 10: DWM Composition handles accumulate after codex tasks with tool calls](https://github.com/openai/codex/issues/33192)** · 12 comments · 10 👍 — Desktop Window Manager handle leak after terminal tool calls; reproducible, with 22 handles leaked in a single 5-call run. Points to a resource-management bug in the Windows sandbox/tool-call path.

7. **[#38290 — CreateProcess: failed unified exec: helper_unknown_error: setup refresh had errors](https://github.com/openai/codex/issues/38290)** · 10 comments — Windows sandbox failure blocking execution entirely for some users (reported in Russian). Sandbox setup refresh errors prevent any tool calls.

8. **[#34619 — Restore GPT-5.6 Sol's 372k Codex context window, or provide opt-in setting](https://github.com/openai/codex/issues/34619)** · 6 comments · 23 👍 — Users report the context window was slashed (to 272K per #40258) and want it back or configurable. High 👍 count signals strong demand for larger context on the flagship model.

9. **[#39973 — Retiring approval_policy="untrusted" without deprecation weakens the execution-approval boundary](https://github.com/openai/codex/issues/39973)** · 4 comments · 9 👍 — 0.149.0 hard-errors on existing configs containing the removed setting; users are forced into a more restrictive approval flow without a migration path or documented replacement.

10. **[#40258 — GPT-5.6 Sol is originator-gated: coding clients get 272K while same account gets 872K](https://github.com/openai/codex/issues/40258)** — The `/backend-api/codex/models` endpoint serves different context-window variants purely based on the `originator` header. Coding surfaces get a fraction of the context available to other surfaces — a transparency concern with pricing/plan implications.

**Also noteworthy**: [#22316 — support selecting existing worktrees](https://github.com/openai/codex/issues/22316) (14 👍) remains popular, and [#39742 — false-positive invalid_prompt on benign tasks](https://github.com/openai/codex/issues/39742) shows safety filters misfiring on normal software prompts.

## Key PR Progress

1. **[#40297 — Preserve developer instruction annotations in subagent forks](https://github.com/openai/codex/pull/40297)** — Adds a contextual fragment for developer instructions so child agents inherit correctly-tagged instructions when forked from parent history.

2. **[#40292 — Add smoke tests for assembled Codex packages](https://github.com/openai/codex/pull/40292)** — Cross-platform pytest suite that extracts CLI and app-server archives and verifies discovery commands plus code-mode execution through packaged entrypoints.

3. **[#40280 — Budget retained images during remote compaction](https://github.com/openai/codex/pull/40280)** — Adds opt-in `compaction_image_budget` feature so image-heavy history can't exceed the retention budget; previously only text counted.

4. **[#40281 — Preserve content kinds during image preparation](https://github.com/openai/codex/pull/40281)** — Ensures positional content-kind metadata stays aligned when image preparation rewrites message content (including model-visible error substitutions).

5. **[#40275 — Classify additional generated context fragments](https://github.com/openai/codex/pull/40275)** — Typed fragments for compaction summaries and Guardian-approved actions, with request items annotated as `compaction.summary`, `guardian.*`, and subagent notifications.

6. **[#40266 — Preserve content annotations when filtering forked agent history](https://github.com/openai/codex/pull/40266)** — Keeps developer-message content and `content_item_kinds` metadata aligned when preparing parent history for spawned agents.

7. **[#40221 — Distinguish Guardian review threads from subagents](https://github.com/openai/codex/pull/40221)** — Adds `guardian_review` thread source so safety-review threads are identifiable in persisted metadata and analytics (previously lumped in with generic `subagent`).

8. **[#40257 — Support cua_repl as a Node REPL-backed MCP server](https://github.com/openai/codex/pull/40257)** — Treats `cua_repl` like `node_repl` for Guardian evidence collection, computer-use policy, and transcript capture; renders results with compact REPL history.

9. **[#40200 — Remove the Plan mode composer nudge](https://github.com/openai/codex/pull/40200)** — Deletes the contextual "Create a plan?" prompt (and its Escape-dismissal behavior) when a draft contains the word "plan"; composer footer stays visible.

10. **[#31175 — Add MongoDB thread store and session migration](https://github.com/openai/codex/pull/31175)** (OPEN) — Experimental `experimental_thread_store = { type = "mongodb" }` backend plus `codex sessions migrate-to-mongo` for streaming rollout migration with verification and namespace clearing. An open PR still under review since July.

**Also merged**: [#40196 — annotate user input and contextual fragments with content kinds](https://github.com/openai/codex/pull/40196), [#40186 — identify detached memory requests as memory consolidation](https://github.com/openai/codex/pull/40186), [#40184 — preserve context annotations in merged messages](https://github.com/openai/codex/pull/40184).

## Feature Request Trends

- **Context-window transparency and control** — Multiple issues (#34619, #40258) demand the return of GPT-5.6 Sol's full context window (372K–872K) for coding surfaces, or at least an opt-in configuration. Users are frustrated by silent, originator-dependent reductions.
- **TUI/CLI output transparency** — #39903 (disable "Ran N commands" collapsing) and #29049 (restricted filesystems blocking Codex's own binary) reflect a broader desire for configurable, verbose execution reporting and fewer surprise restrictions.
- **Persistent background workflows** — #32993 asks for first-class self-healing "monitor workflows" that return to a thread at a future time; #32519 requests bidirectional task handoff between ChatGPT mobile and Codex desktop. Users want Codex to operate as a long-running autonomous agent, not a single-session tool.
- **Rate-limit transparency and fairness** — #37445 and #39760 both point at silent consumption of weekly limits (background activity, phantom resets). A policy/display change that surfaces exactly what consumes quota is clearly needed.
- **Worktree flexibility** — #22316 (select existing worktrees) continues to gather support; users want Codex to integrate with their existing branch/worktree workflows rather than always creating fresh ones.

## Developer Pain Points

- **Silent quota consumption** — The desktop app's background activity deducting from the weekly limit without user action (#37445) is the most operationally damaging bug this week; it directly affects paying Pro users' ability to work.
- **Breaking config changes without deprecation** — Removing `approval_policy = "untrusted"` in 0.149.0 with a hard error (#39973) forces users to reconfigure under time pressure; the community wants deprecation cycles and migration guidance.
- **Windows-specific instability** — Recurring issues: DWM handle leaks (#33192), sandbox `CreateProcess` failures (#38290), `apply_patch` access-denied in unelevated sandboxes (#34294), and browser/computer-use plugins failing to initialize (#39543, #40228). Windows remains the least-polished platform.
- **Subagent reliability** — Agents closing or abandoning subagents prematurely (#40299) and Guardian review threads being indistinguishable from subagents (#40221) point to immature multi-agent orchestration.
- **Auth and session churn** — Desktop app logging users out every ~1 minute (#39218) and SQLite lock contention between concurrent app-server instances (#30105) highlight desktop-app state-management issues.
- **IDE extension input loss** — Prompt disappearance before queueing (#25928, open since June) remains unresolved, a daily frustration for Windows users relying on the VS Code/Cursor extension.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-24

## Today's Highlights

The Gemini CLI community continues to focus heavily on agent reliability, with recurring themes around subagent execution failures, context retention, and sandbox security hardening. Notably, several high-priority bugs involving subagent recovery after turn limits and generalist agent hangs remain under active investigation. A significant security-focused PR addressing symlink-based path traversal has been closed, and new fixes for session retention data loss and OAuth callback timeouts were merged today.

## Releases

- **[v0.56.0-nightly.20260823.g5411f113c](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260823.g5411f113c)** — Latest nightly release with no explicit changelog details. Compare with previous nightly [here](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260822.g5411f113c...v0.56.0-nightly.20260823.g5411f113c).

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 13 comments, 2 👍) — A `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even after hitting the max turn limit without performing any analysis. This masks real failures and is misleading for debugging agent behavior. The issue remains open needing retesting.

2. **[#21409 — Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 8 comments, 8 👍) — The generalist agent hangs forever on simple tasks like folder creation, requiring users to wait up to an hour before cancellation. High community engagement (8 👍) suggests this is a common pain point. Workaround: explicitly instruct the model not to defer to subagents.

3. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 4 comments, 3 👍) — After executing simple CLI commands, the shell state remains stuck showing "Awaiting user input" even though the command has finished. This severely impacts interactive workflows.

4. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, 4 comments, 1 👍) — Browser subagent fails with `Termination Reason: GOAL` on Wayland environments. Given the growing Wayland user base, this limits browser automation for a significant segment of Linux users.

5. **[#22186 — get-shit-done output hook causes crash](https://github.com/google-gemini/gemini-cli/issues/22186)** (P1, 3 comments) — The GSD output hook crashes Gemini CLI when printing the final user summary. Critical for users relying on this workflow, as it occurs at the final output stage.

6. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, 5 comments) — Auto Memory only marks sessions as processed when the extraction agent reads the transcript; low-signal sessions that are intentionally skipped remain eligible for re-processing, causing infinite retry loops and wasted tokens.

7. **[#26525 — Auto Memory lacks deterministic redaction](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, 4 comments) — Sensitive content (secrets, API keys) is sent to the extraction model *before* redaction instructions are applied. Also, the service can log existing skill names that may be proprietary. A security/privacy concern for enterprise users.

8. **[#21968 — Gemini doesn't use skills and subagents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, 6 comments) — Users report that custom skills and subagents are rarely invoked autonomously, even when clearly relevant. The model only uses them when explicitly instructed, reducing the value proposition of customization.

9. **[#20079 — Symlinked agent files not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** (P2, 4 comments) — `~/.gemini/agents/filename.md` is not recognized as an agent when it's a symlink. Blocks users who manage dotfiles via symlinks (common with version-controlled config).

10. **[#24246 — 400 error with >128 tools enabled](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2, 3 comments) — Gemini CLI hits a 400 error when more than 128 tools are available. Users expect the agent to intelligently scope tools, but no auto-filtering exists yet.

## Key PR Progress

1. **[#2677 — Prevent symlink-based path traversal attacks](https://github.com/google-gemini/gemini-cli/pull/2677)** (P0, Security, CLOSED) — Fixes a critical vulnerability where attackers could bypass workspace restrictions using symbolic links. All file paths now resolve to real locations before validation. This is a major security hardening win.

2. **[#28981 — Stop session retention deleting unrelated sessions on shortId collision](https://github.com/google-gemini/gemini-cli/pull/28981)** (CLOSED) — Fixes a **user-data-loss path** where `cleanupExpiredSessions()` deleted *every* file matching an 8-character shortId suffix, potentially wiping unrelated sessions. Addresses issue #28643.

3. **[#28980 — Clear OAuth callback timeout when callback server closes](https://github.com/google-gemini/gemini-cli/pull/28980)** (CLOSED) — Fixes #28652: the 5-minute OAuth timeout timer was never cleared on terminal paths. The retained timer could outlive the flow, keeping Node process alive unnecessarily.

4. **[#28979 — Handle response and write stream errors in extension downloadFile](https://github.com/google-gemini/gemini-cli/pull/28979)** (CLOSED) — Fixes #28645: `downloadFile()` only listened for `finish`, missing mid-transfer network failures and ENOSPC errors. Now properly handles error events from both response and write streams.

5. **[#28975 — Keep glob results for symlinked workspace roots](https://github.com/google-gemini/gemini-cli/pull/28975)** (OPEN) — Fixes #28416: glob returns "No files found" when the workspace root is reached via symlink (e.g., `/tmp` on macOS → `/private/tmp`). Broader impact than originally scoped.

6. **[#28914 — Inject on-retry nudge into conversation contents to preserve prefix caching](https://github.com/google-gemini/gemini-cli/pull/28914)** (OPEN) — Fixes #28909 by moving the on-retry nudge from `systemInstruction` to the end of `contents`. Preserves static prompt prefix caching and ensures the model sees the nudge immediately before generating.

7. **[#28972 — Guard formatTruncatedToolOutput against non-positive maxChars](https://github.com/google-gemini/gemini-cli/pull/28972)** (OPEN, P1) — Fixes #28620: negative `maxChars` produced corrupt output via negative slice indices. Small but impactful fix for text truncation reliability.

8. **[#28935 — Isolate Docker and container runtime sockets in macOS Seatbelt](https://github.com/google-gemini/gemini-cli/pull/28935)** (CLOSED) — Denies access to container runtime daemon UNIX sockets, CLI binaries, Mach/XPC services, and POSIX shared memory in Seatbelt sandbox profiles. Prevents sandbox escape via Docker Desktop VirtioFS mounts.

9. **[#28983 — Detect mixed line endings instead of flagging CRLF on a single match](https://github.com/google-gemini/gemini-cli/pull/28983)** (OPEN) — Improves `detectLineEnding()` to correctly handle mixed line endings rather than classifying a file as CRLF based on a single `\r\n`.

10. **[#28982 — Add Build Remote Agent phone pairing example](https://github.com/google-gemini/gemini-cli/pull/28982)** (OPEN) — Adds an example extension (not core) allowing a phone running "Build Remote Agent" to spectate a desktop Gemini CLI session via `gbr/1` protocol with QR pairing.

## Feature Request Trends

- **AST-Aware Tooling** (#22745, #22746): Multiple issues investigate AST-aware file reads, search, and codebase mapping for more precise method bounds, reduced token noise, and better navigation. Suggested starting points: `tilth` or `glyph`.
- **Persistent Task Tracking** (#18836, #21000): Move away from in-context `WriteToDo` toward file-based CRUD task tracking — addresses "context rot," high token costs, and memory loss between sessions.
- **Subagent Visibility & Trajectory** (#22598, #21763): Users want subagent trajectories accessible via `/chat share` and included in `/bug` reports for better debugging and evals.
- **Behavioral Guardrails** (#22672): Requests for the agent to discourage destructive behaviors (e.g., `git reset --force`) and prefer safer alternatives when available.
- **Agent Self-Awareness** (#21432): The agent should understand its own CLI flags, hotkeys, and self-execution mechanics to act as a better expert guide.
- **Sandboxing & OS Integration** (#19873): Leverage model's bash affinity via zero-dependency OS sandboxing with post-execution intent routing for secure native tool use.

## Developer Pain Points

- **Agent Hangs & Stalls** (#21409, #25166): Recurring complaints about the CLI hanging on simple operations — shell commands stuck in "Waiting input" and generalist agents freezing. This is a top-priority UX issue.
- **Misleading Success Reporting** (#22323): Subagents reporting `SUCCESS`/`GOAL` when actually interrupted by turn limits — undermines trust in automation and makes failure triage nearly impossible.
- **Configuration & Symlink Issues** (#20079, #28975): Symlinked agent files and workspace roots not recognized or breaking glob/retention logic — particularly painful for macOS users with `/tmp` symlinks and dotfile management workflows.
- **Context & Token Bloat** (#19561, #18836, #26522, #26523): High baseline context (~36.6k tokens/turn), firehosed file reads, and Auto Memory retry loops waste tokens and degrade quality. Memory-related fixes are pending retesting.
- **Tool Overload** (#24246): Hitting 400 errors with >128 tools — the agent needs smarter tool scoping rather than the current all-tools-always approach.
- **Platform-Specific Failures** (#21983, #28935): Wayland browser subagent failures and macOS sandbox escape vectors highlight platform-awareness gaps in the agent layer.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-24

## Today's Highlights

A new patch release (v1.0.81-8) adds xhigh reasoning effort support for Grok 4.6 and significantly improves the local plugin development experience with live-reload capabilities. Meanwhile, the community is actively reporting issues around memory persistence failures, background compaction bugs, and Windows-specific plugin installation conflicts with VS Code.

## Releases

**v1.0.81-8** — [Release Link](https://github.com/github/copilot-cli/releases)

**Added**
- xhigh reasoning effort support for Grok 4.6

**Improved**
- Path-sourced plugins in a local (directory-source) marketplace now load live from their real directory — edits take effect on `/restart` or new sessions without requiring `/plugin update`
- Skills and custom agents are now more discoverable

---

## Hot Issues

**1. [#2306] Enterprise Authorization Errors** — [Issue Link](https://github.com/github/copilot-cli/issues/2306)  
Intermittent "You are not authorized to use this Copilot feature" errors affecting enterprise users, recurring 2–3 times weekly. 9 comments, 3 upvotes. This long-running issue (since March) remains a significant pain point for enterprise deployments.

**2. [#4535] `store_memory` Fails with "Instance id is required"** — [Issue Link](https://github.com/github/copilot-cli/issues/4535)  
Memory persistence fails consistently in v1.0.81 prereleases. The native memory writer is invoked without a required instance ID, breaking context memory features. 5 comments. Critical for users relying on long-term memory.

**3. [#4572] Background Compaction Loses Tool Results (HTTP 400)** — [Issue Link](https://github.com/github/copilot-cli/issues/4572)  
Long-context `gpt-5.6-sol` sessions can fail with `400 No tool output found` after automatic background compaction, even though the tool executed successfully. 1 comment. This is a serious reliability issue for extended sessions.

**4. [#4570] Windows: Plugin Install Fails When VS Code is Running** — [Issue Link](https://github.com/github/copilot-cli/issues/4570)  
`plugin install`/`update` fails with "Access is denied (os error 5)" whenever VS Code is open. Affects all plugins. 1 comment. Likely a file-locking issue between VS Code and the CLI.

**5. [#4566] Agent Acknowledges Work Without Executing Tools** — [Issue Link](https://github.com/github/copilot-cli/issues/4566)  
Agents repeatedly confirm tasks without actually invoking tool actions, wasting turns and confusing users. Model: `gpt-5.3-codex`, version 1.0.80. 1 comment, 1 upvote. A core agent-loop reliability concern.

**6. [#4571] Compaction Triggered at 50% with GPT-5.6 Luna Max** — [Issue Link](https://github.com/github/copilot-cli/issues/4571)  
Compaction fires at 50% context usage for GPT-5.6 Luna Max, causing frequent disruptions even for small tasks. 0 comments. Likely a misconfigured threshold for high-effort models.

**7. [#4560] Model "auto" Disables Reasoning Effort** — [Issue Link](https://github.com/github/copilot-cli/issues/4560)  
Setting model to `auto` sends requests with `reasoningEffort: null` and rejects any user configuration attempts. 0 comments. Impacts users relying on auto-routing for effort level control.

**8. [#4568] `--cloud` Owner Picker Hangs, Reconnect Crashes** — [Issue Link](https://github.com/github/copilot-cli/issues/4568)  
Multiple cloud-mode failures: hangs at owner loading without repo context, provisioning timeouts, reconnect crashes, and 429 rate limits on task polling. 0 comments. Severely impacts cloud-based workflows.

**9. [#4561] ACP Cancel Returns Wrong stopReason** — [Issue Link](https://github.com/github/copilot-cli/issues/4561)  
In ACP mode, `session/cancel` is answered with `stopReason: "end_turn"` instead of `"cancelled"` as the ACP spec requires. 0 comments. Breaks ACP clients that distinguish completion from cancellation.

**10. [#4562] MCP Reload Reuses Stale Workspace Config** — [Issue Link](https://github.com/github/copilot-cli/issues/4562)  
MCP reload keeps the original startup configuration snapshot instead of reading updated `.github/mcp.json`. If a server fails to initialize and the config is corrected, reload retries the old broken command. 0 comments.

---

## Key PR Progress

*Note: Only 1 PR was updated in the last 24 hours.*

**[#4573] Rename README.md to README.mdmain** — [PR Link](https://github.com/github/copilot-cli/pull/4573)  
Opened by phuongnam467. Appears to be a spurious/non-substantive rename PR (likely a typo). 0 comments, 0 upvotes. No meaningful changes; flagged for maintainers to close.

---

## Feature Request Trends

- **Insecure OTLP Endpoint Trust** ([#4567](https://github.com/github/copilot-cli/issues/4567)): Users want an explicit opt-in to trust `http://` OTLP endpoints (e.g., local loopback collectors) rather than silently disabling telemetry export. Aligns with VS Code behavior. Community interest in local observability is growing.
- **Inline Plan Annotations** ([#4563](https://github.com/github/copilot-cli/issues/4563)): Users request the ability to select plan text or steps and attach inline annotations rather than restating full context in chat. A UX improvement for plan review workflows.
- **Effort Level Override for Model "auto"** ([#4560](https://github.com/github/copilot-cli/issues/4560)): Users want to configure reasoning effort even when using model auto-routing, rather than having it forcibly disabled.

---

## Developer Pain Points

1. **Compaction and Context Management Instability**: Two separate issues ([#4572](https://github.com/github/copilot-cli/issues/4572), [#4571](https://github.com/github/copilot-cli/issues/4571)) highlight serious bugs where background compaction either drops tool results or triggers prematurely (at 50% for high-effort models). This is the most critical reliability concern for long-running sessions.

2. **Memory Persistence Breakage in Prereleases**: The `store_memory` failure ([#4535](https://github.com/github/copilot-cli/issues/4535)) in v1.0.81 prereleases breaks a core feature, and regression testing appears insufficient for prerelease quality gates.

3. **Windows File-Locking Conflicts**: VS Code holding locks on plugin files ([#4570](https://github.com/github/copilot-cli/issues/4570)) disrupts plugin management workflows. Users must close VS Code to update plugins — friction in multi-tool setups.

4. **Intermittent Enterprise Authorization Failures**: The long-standing issue ([#2306](https://github.com/github/copilot-cli/issues/2306)) continues to plague enterprise users with random authorization denials, eroding trust in enterprise readiness.

5. **Cloud Mode Reliability**: Multiple interconnected cloud-mode failures ([#4568](https://github.com/github/copilot-cli/issues/4568)) — hangs, crashes, 429s — make `--cloud` usage impractical in its current state.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-08-24**

---

### 1. Today's Highlights
Development activity remains quiet with **no new releases** in the past 24 hours, suggesting the team may be deep in internal stabilization work. However, two long-pending items are gaining renewed traction: the **Memory System feature request (#1283)** continues to accumulate community discussion (27 comments), and a concerning **allowance metering report (#2604)** with hard instrumentation data has surfaced, potentially signaling a silent quota regression. On the contribution side, a novel third-party PR proposes integrating **phone-based remote pairing** for agent sessions, an area the core team has not addressed.

---

### 2. Releases
**No new versions published** in the last 24 hours. The most recent release on record remains from prior days (not specified in this window).

---

### 3. Hot Issues (3 of 3 open items selected; no additional issues in window)

| # | Issue | Why It Matters | Community Reaction |
|---|-------|----------------|-------------------|
| 1 | [#1283 — Memory System: Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283) — *Open* | The **#1 most-upvoted enhancement direction** in the repo. Developers want the CLI to remember project patterns, user prefs, and AI-managed notes across invocations. Currently, each session starts from scratch, forcing repetitive instructions. | **27 comments** — high engagement. Community is actively proposing hybrid auto/manual memory with configurable scopes (global vs. repo). No official response yet. |
| 2 | [#2604 — Effective weekly allowance appears reduced ~3–5× without announcement](https://github.com/MoonshotAI/kimi-cli/issues/2604) — *Open* | **Critical trust issue.** A Vivace-tier member ran wire-level instrumentation (JSONL ledger) tracking token volume across API calls. Their data shows **weekly allowance dropped 3–5×** compared to mid-July, without any changelog or announcement. Could be a metering bug (cache hits counted incorrectly) or a silent terms change. | **3 comments** — low volume but high severity. Commenters are asking for a maintainer response; no acknowledgment yet. This could trigger broader user outrage if unaddressed. |
| 3 | [#2484 — "." (empty title)](https://github.com/MoonshotAI/kimi-cli/issues/2484) — *Closed* | Placeholder or accidental issue; closed without comments. | No signal. Minor housekeeping. |

*(Note: Only 3 issues were updated in the window; 10-target not reached due to low activity.)*

---

### 4. Key PR Progress (2 PRs available; full list in window)

| # | PR | What It Does | Status / Impact |
|---|-----|--------------|----------------|
| 1 | [#2616 — Add Build Remote Agent phone pairing (gbr/1)](https://github.com/MoonshotAI/kimi-cli/pull/2616) — *Open* | Integrates **phone-as-spectator** support via a free MIT protocol (`gbr/1`). The iOS/Android companion app can **view the live session and veto actions** without orchestrating. Built on `gbr-agent`. | **Third-party contribution.** Addresses a real gap: remote monitoring/approval for long-running agent tasks. Backward-compatible (additive). No maintainer comment yet — likely awaiting review. |
| 2 | [#2614 — docs(plugins): document security and persistent data](https://github.com/MoonshotAI/kimi-cli/pull/2614) — *Open* | Documentation-only. Clarifies the **plugin contract**: root `plugin.json`, command-based tools, `inject`, and `~/.kimi/plugins/` installation. Explicitly scopes out any changes to actual plugin behavior. | Low-risk, high-value. Improves trust for plugin developers worried about arbitrary code execution. No conflicts reported. |

*(Note: Only 2 PRs updated in window; 10-target not reached.)*

---

### 5. Feature Request Trends (from all open issues)
Across the current backlog, these are the dominant directions:

1. **Memory & Context Persistence** — (#1283 et al.) Users want the CLI to act like a *junior teammate with a notebook*: remembering decisions, preferences, and project idioms across sessions. Expect this to stay #1 until the core team ships a foundation.
2. **Remote Session Control** — (#2616 signals demand) Developers want to **monitor and gate** agent activity from their phone, especially during long unattended builds. Team does not have an official feature; community is filling the gap.
3. **Transparent Quota & Metering** — (#2604) Users demand **legible usage dashboards** inside the CLI (not just API-side logs), plus changelog notes whenever pricing or allowance semantics change.

*Secondary signals:* Plugin security documentation, deterministic caching, and offline mode requests appear cluster-wide.

---

### 6. Developer Pain Points
- **Allowance & Quota Opaqueness** — The metering regression report exposes a systemic pain: **users cannot trust their quota without building their own telemetry**. High risk of churn if not addressed with public instrumentation.
- **Context Amnesia** — Repeatedly re-explain project structure and preferences each session; fatigue is visible in issue comments. This is the **single most-cited workflow blocker**.
- **Lack of Remote Gating** — Desktop-only operation forces developers to stay at the machine. Users want **approval via mobile** before risky agent actions (e.g., `rm -rf`, mass edits).
- **Silent Behavior Changes** — Undocumented shifts in behavior (allowance, rate limits, model defaults) erode trust fast. Community consistently rewards the team when changelogs are explicit, and punishes silence.

---

*Sources: github.com/MoonshotAI/kimi-cli — data window 2026-08-23 to 2026-08-24.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-24

## Today's Highlights
The OpenCode community is experiencing significant turbulence around the Zen API and Big Pickle model reliability, with multiple reports of persistent rate limiting and mid-generation cutoffs. A coordinated cluster of PRs from **kitlangton** and **gitRasheed** targeting workspace-location bugs, database race conditions, and non-interactive session handling suggests a broad infrastructure hardening push from contributors. Notably, no new releases shipped in the last 24 hours, and the community is actively filing issues around session crashes, network errors, and long-standing plugin/TUI regressions.

## Releases
No new versions were published in the last 24 hours. The community is operating on **v1.18.21** (with several reports of regressions on this version), and an unreleased **V2 (0.0.0-next-17403)** referred to in Issue #42421 appears to be in development alongside a **1.17.10** regression window.

---

## Hot Issues

1. **[#1034 — Local Ollama tool calling either not calling or failing outright](https://github.com/anomalyco/opencode/issues/1034)** — *31 comments, 16 👍* — Despite being closed, this remains one of the most-commented issues in the repo. The `qwen3:32b` tool-calling breakage has frustrated many local-model users. The community's high engagement (31 comments) indicates this is a deeply felt problem that may not be fully resolved.

2. **[#44528 — Bug Report, network error (v1.18.21)](https://github.com/anomalyco/opencode/issues/44528)** — *7 comments* — A newly-reported issue with **Big Pickle** on **Ollama Cloud** where the program fails on startup. This echoes a broader pattern of v1.18.21 introducing instability, with several issues (including #44347) reporting "bricked" sessions post-update.

3. **[#44300 — Zen API: x-preview-f-free / ox-alpha-free fails with "Endpoint is unavailable"](https://github.com/anomalyco/opencode/issues/44300)** — *4 comments, 1 👍* — Any request with a `tools` array fails consistently on both Zen Console and Go routes. This is a high-priority integration break affecting the **Ox Alpha free model**, a critical free-tier entry point for many developers.

4. **[#44447 — Big Pickle Now Frustrating to Use](https://github.com/anomalyco/opencode/issues/44447)** — *2 comments* — Major model regression reported: Big Pickle stops mid-thought every ~2 minutes, requiring a constant "Keep going" cadence. The author notes it "previously worked" — this appeared ~36 hours before filing, suggesting a server-side degradation.

5. **[#43535 — TUI plugins referenced by npm package spec silently fail (OpenTUI 0.4.2)](https://github.com/anomalyco/opencode/issues/33884)** — *6 comments, 1 👍* — A dual-entry regression in v1.17.10 where npm-spec TUI plugins fail to load. The PR was mitigated on `dev` by reverting to OpenTUI 0.3.4, but this is documented as an unresolved underlying loader issue that will resurface.

6. **[#38923 — MCP tool results: structuredContent is dropped](https://github.com/anomalyco/opencode/issues/38923)** — *4 comments, 1 👍* — A reproducibility issue for MCP server users: `structuredContent` is silently discarded and only `content[].text` is forwarded to the model, breaking any tool that relies on structured JSON payloads.

7. **[#44556 — run --session hangs when the model uses the question tool](https://github.com/anomalyco/opencode/issues/44556)** — *2 comments* — A critical headless-mode bug where `opencode run --session` (via external HTTP API) doesn't apply deny rules, causing the question tool to hang indefinitely when invoked. Has a pending fix in PR #44559.

8. **[#38309 — Desktop 1.18.4 + WSL2: "OpenCode not installed" after install](https://github.com/anomalyco/opencode/issues/38309)** — *3 comments* — A disruptive WSL2 integration failure where the Desktop app fails to detect a working CLI installation, breaking the hybrid local/remote workflow for Windows users.

9. **[#42421 — TODO tools missing in V2](https://github.com/anomalyco/opencode/issues/42421)** — *5 comments* — The native `todowrite` / `todoread` tools are gone from the V2 runtime tool catalog, a significant workflow regression for users who relied on in-TUI task lists. Closed, but worth monitoring for resolved-alternative behavior.

10. **[#44101 — Desktop: two clones of same repo show wrong project name/path](https://github.com/anomalyco/opencode/issues/44101)** — *3 comments* — Git-remote-derived project identity causes two separate checkouts to be conflated into one project, causing incorrect paths and persistent UI mislabeling that survives restarts.

---

## Key PR Progress

1. **[#44567 — fix(core): accept null as omitted for optional tool inputs](https://github.com/anomalyco/opencode/pull/44567)** — *kitlangton* — Resolves the perennial friction where JSON Schema permits `null` but Effect schema expects `undefined`. Directly addresses the schema validation issues raised in #29142 and similar reports.

2. **[#44559 — fix(run): apply non-interactive deny rules to resumed sessions](https://github.com/anomalyco/opencode/pull/44559)** — *gitRasheed* — Closes the hang bug #44556 by properly routing `--session`, `--continue`, and `--fork` paths through the same deny-rule logic as new sessions. A solid headless-mode hardening.

3. **[#44558 — fix(db): serialize database init and migrations across processes](https://github.com/anomalyco/opencode/pull/44558)** — *gitRasheed* — Kills the "database is locked" race condition when concurrent `opencode run` processes boot against a fresh SQLite DB — reproduced as 5 failures in ~15ms with 6 processes.

4. **[#44557 — fix(run): add --no-stdin to skip reading piped stdin](https://github.com/anomalyco/opencode/pull/44557)** — *gitRasheed* — Fixes an important CI/automation gap where inherited non-TTY pipes block `opencode run` indefinitely until EOF. Closes #42064.

5. **[#44565 — fix(codemode): package conditional transpilers](https://github.com/anomalyco/opencode/pull/44565)** — *kitlangton* — Makes published `@opencode-ai/codemode` packages loadable again by rewriting conditional `#transpile` imports to their compiled targets, with a verify step against a clean consumer.

6. **[#44536 — feat(session): auto-retry empty stop responses](https://github.com/anomalyco/opencode/pull/44536)** — *savagelysubtle* — Targets the "have to prompt continue" plague (see #44447): providers returning empty `finish_reason: stop` will be auto-retried. Likely the most impactful UX fix in review.

7. **[#44534 — feat(tui): render Mermaid Gantt diagrams](https://github.com/anomalyco/opencode/pull/44534)** — *kitlangton* — Adds terminal-native Gantt chart rendering to the V2 TUI, converting raw Mermaid fences into aligned time-axis charts — a notable TUI polish milestone.

8. **[#44562 — fix(core): resolve external paths through the location environment](https://github.com/anomalyco/opencode/pull/44562)** — *kitlangton* — Fixes external-mutation path classification for workspace-backed (remote sandbox) locations, addressing boot failures where the server probed the wrong filesystem. Coordinates with #44563, #44564, #44560 as a workspace-location fix stack.

9. **[#44545 — feat(tui): discoverable queue controls with terminal-safe keybinds](https://github.com/anomalyco/opencode/pull/44545)** — *savagelysubtle* — Makes queue controls usable inside VS Code integrated terminals by adding leader-chord fallbacks for `ctrl+enter` — a pragmatic ergonomics fix.

10. **[#44485 — fix(core): resolve compatible shells for commands](https://github.com/anomalyco/opencode/pull/44485)** — *opencode-agent[bot]* — Centralizes shell selection through `resolve({ preference })`, preserving configured shells for PTYs and direct callers while letting only the agent tool resolve compatible shells for sandboxed execution.

---

## Feature Request Trends
- **Thinking-block defaults** — #28322 (closed) requested a config option to default thinking/reasoning blocks to *expanded* instead of collapsed. The 7 comments and 5 👍 indicate there's persistent appetite for more control over the TUI's chain-of-thought display.
- **Project/session management** — #37280 requests the ability to remove projects (and their sessions) from OpenCode entirely. This connects to #44101's conflation issues and reflects a need for more granular identity/cleanup controls.
- **Task management continuity** — The V2 TODO-tool removal (#42421) plus the overall roadmap work signals that the community wants native task lists preserved across architecture changes, not just as TUI UI state.
- **Non-interactive hardening** — Across #44556, #44557, and #44559, there's a clear cluster of requests around making `opencode run` genuinely safe for CI and automation: no-stdin flags, deny-rule consistency, and hang-free exits.

---

## Developer Pain Points
- **v1.18.21 instability** — Multiple reports (#44347 "bricked," #44528 network errors, #44522 "network_error" finish reasons, #44505 mid-task stops) point to a systemic reliability regression in the latest release, especially with **Big Pickle** and **Zen API** backends.
- **Zen API rate-limiting and free-tier breakage** — A striking pattern from one user (ahmoodiamorii-boop) across #43627, #44207, #43404, #43480: Zen base URL rate-limiting persists for days, and free-tier models/external CLI usage frequently fail. Trust is eroding in the free-tier story.
- **Mid-generation cutoffs** — The "Keep going" pattern surfaced in #44447 and #43404 has a likely fix in #44536 (auto-retry empty stops), but the community is clearly experiencing provider flakiness as a first-class bug.
- **Windows/WSL and anti-cheat interactions** — #44513 (GameGuard segfaulting embedded Bun) and #38309 (WSL2 false "not installed") reveal platform-specific fragility in the embedded runtime detection.
- **Tool-call schema friction** — #29142 (invalid write/edit args from OpenAI-compatible models) plus #44567's null-vs-undefined fix signal recurring pain at the model/tool boundary, often resulting in unrecoverable UI errors.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-24

## Today's Highlights
The community continues to drive hard on provider interoperability and Windows terminal ergonomics. A cluster of fixes landed for strict OpenAI-compatible providers (Kimi, Nous), addressing history replay validation and silent stream failures that were ending sessions mid-task. On the model management front, llama.cpp unloaded models are now visible in `/model`, removing a long-standing discoverability gap.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#8167 — Cannot pick a model with built-in llama.cpp support](https://earendil-works/pi/issues/8167)** *(Closed)* — Models from llama-server in router mode don't appear in the model list despite working via `/llama`. This drove the PRs to expose unloaded presets; users expect a unified model picker.

2. **[#7885 — npm search not indexing newly published pi-packages](https://earendil-works/pi/issues/7885)** *(Closed)* — Published packages with valid pi manifests never appear in `npm search` or the gallery. Raises a real discoverability concern for the package ecosystem.

3. **[#5932 — Exposing ctx.navigateTree() to agents](https://earendil-works/pi/issues/5932)** *(Open, 2 👍)* — Requesting `navigateTree()` on `ExtensionContext` to match `ExtensionCommandContext`, enabling custom `/goal` implementations. Still open after 2 months; signals a need for richer navigation APIs.

4. **[#8452 — Improve default compaction prompt for continuation-state fidelity](https://earendil-works/pi/issues/8452)** *(Closed)* — Suggests merging/deduplicating summaries over preserving prose; wants the checkpoint to distinguish observed results from inferences.

5. **[#8183 — Windows Terminal's Ctrl+Shift+F conflict with fullscreen search](https://earendil-works/pi/issues/8183)** *(Closed)* — Community wants documented workarounds for the keybinding clash; was resolved with docs, but the frequency of Windows keybinding issues suggests deeper platform work is needed.

6. **[#8344 — Per-tool output expansion in fullscreen TUI](https://earendil-works/pi/issues/8344)** *(Closed)* — Proposes mouse-driven expand/collapse per tool output block, independent of the global `Ctrl+O`. Long sessions produce unwieldy outputs; this would greatly improve TUI usability.

7. **[#8457 — Invoke skills mid-sentence like prompt templates](https://earendil-works/pi/issues/8457)** *(2 👍)* — Users want `/skill:name` to expand inline after the first line, mirroring `/template` behavior in 0.84. Positive community reaction; likely a UX consistency win.

8. **[#7724 — Cold restore replays an overflow assistant removed by live recovery](https://earendil-works/pi/issues/7724)** *(Open)* — After compaction and retry, reopening adds the failed/truncated response back. Persistence and compaction don't agree; this is a correctness issue that can confuse model history.

9. **[#8537 — Kimi 400s on replayed tool history](https://earendil-works/pi/issues/8537)** *(Closed)* — Orphaned tool messages, interleaved user messages, duplicate `tool_call_id`. Strict providers reject what lenient ones tolerate; the community is clearly testing beyond OpenAI/DeepSeek.

10. **[#8521 — edit tool: stringified edits with raw control characters fail validation](https://earendil-works/pi/issues/8521)** *(Closed)* — Follow-up to #3370; models emitting raw newlines/tabs inside strings bypass `JSON.parse`. A pattern of model-generated edge cases requiring more robust argument sanitization.

## Key PR Progress

1. **[#8535 — Show unloaded llama.cpp models in `/model`](https://earendil-works/pi/pulls/8535)** *(Merged)* — The router exposes unloaded models; auto-loads on prompt. Removes manual `/llama` juggling. Direct fix for #8167.

2. **[#8536 — Normalize tool-result history for strict OpenAI-compatible providers](https://earendil-works/pi/pulls/8536)** *(Merged)* — Repairs history replay for Kimi/Moonshot. Lenient providers hid ordering issues; this brings validation discipline across providers.

3. **[#8509 — Surface stream errors and support toolless models](https://earendil-works/pi/pulls/8509)** *(Merged)* — Detects abnormal native finish reasons (`network_error` with 0 tokens) instead of treating them as clean stops. Fixes silent mid-task session ends.

4. **[#8513 — Repair raw control characters in stringified edit args](https://earendil-works/pi/pulls/8513)** *(Merged)* — Sanitizes real newlines/tabs in JSON strings before parsing. Follow-up hardening for model-generated edits.

5. **[#8532 — Cap grep/find child output to protect parent process](https://earendil-works/pi/pulls/8532)** *(Merged)* — Fixes `RangeError: Invalid string length` from unbounded readline growth. A V8 limit met in practice; good defensive fix.

6. **[#8524 — Retain working status until settled](https://earendil-works/pi/pulls/8524)** *(Merged)* — Keeps `Working...` through `agent_end`, clearing only after `agent_settled` callbacks. External observers no longer see premature completion.

7. **[#8505 — Cap agent retry backoff](https://earendil-works/pi/pulls/8505)** *(Merged)* — Adds `retry.maxAgentDelayMs` (default 30s). Preserves exponential backoff while bounding worst-case waits.

8. **[#8512 — Add optional PowerShell tool](https://earendil-works/pi/pulls/8512)** *(Open)* — Author explicitly gives up on git bash for Windows path handling. This could materially improve the native Windows experience. Worth watching.

9. **[#8032 — TUI mouse events on component rows](https://earendil-works/pi/pulls/8032)** *(Open)* — Adds `Component.onMouse(event)`, hit-testing the LayoutBox tree innermost-first. Direct implementation of #7683; had 11 comments on the issue, so interest is measurable.

10. **[#8500 — Eliminate false positives in plan mode bash guard](https://earendil-works/pi/pulls/8500)** *(Merged)* — Fixes paths containing the word "code" being flagged as destructive, plus demo text spoofing the plan extractor.

## Feature Request Trends
- **Model management**: Unloaded llama.cpp models selection, vision model catalog additions, (e.g., `deepseek-v4-flash-vision-exp`), and context ceiling metadata. The community wants the model picker to reflect runtime reality.
- **TUI interactivity**: Per-block expansion, mouse events with relative coordinates, and consistent syntax coloring. There's a clear push to make the fullscreen transcript a first-class interactive surface.
- **Extension/API surface**: `navigateTree()`, user bash completion events, skill visibility APIs, and mid-sentence skill invocation. Extensions are hitting limits of the current event and context APIs.

## Developer Pain Points
- **Windows terminal keybindings and path handling**: A recurring theme — conflicts with Windows Terminal's own shortcuts and broken path handling leading one maintainer to "give up" on git bash.
- **Strict provider validation**: History replay failures with Kimi, Vertex AI's array-wrapped errors being dropped, empty `custom: {}` misrouting tool calls — providers with non-OpenAI quirks surface bugs that lenient ones hide.
- **Silent session failures**: Network errors treated as clean stops, auto-retry stalling on consecutive timeouts, and working status flickering prematurely. Session liveness and observable state matter deeply to users.
- **Agent output hygiene**: Trailing spaces on copy, idempotent todo toggles, and raw control characters in edit strings — small quality-of-life gaps that compound across long agent runs.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-24

## Today's Highlights

The project continues aggressive hardening of its `/review` skill with execution-grade verification (PR #9740), alongside a security-focused fix for PAT-bearing CI jobs requiring runner-level isolation (Issue #9089). Platform reliability is also front-and-center, with a PR repairing Windows/macOS test lanes (PR #9728) and a notable new issue revealing that `permissions.allow` does not actually restrict tool schemas sent to the model (Issue #9827).

---

## Releases

**v0.22.0-nightly.20260823.1007bcacfc** — nightly release focused on a Web Shell UX fix: session workspace cwd is now properly passed when opening from the overview panel (PR #9730). No public stable release in the last 24 hours.

---

## Hot Issues

1. **[#9827 — permissions.allow does not restrict tool schemas sent to the model](https://github.com/QwenLM/qwen-code/issues/9827)** (P2, open, 4 comments) — A security-relevant gap: setting `permissions.allow` only changes what `/tools` displays in the CLI, but the full built-in tool set still goes into the API request payload. High community value since this defeats the purpose of the allowlist.

2. **[#9089 — PAT-bearing jobs share a host with untrusted branch code](https://github.com/QwenLM/qwen-code/issues/9089)** (P1, closed, 7 comments) — Security finding that cannot be fixed inside a GitHub Actions step alone; requires runner-level isolation. Closed by the maintainer after being addressed.

3. **[#5975 — API Error: No stream activity for 120000ms after 19 chunks](https://github.com/QwenLM/qwen-code/issues/5975)** (P2, open, 11 comments, 1 👍) — A recurring stream-timeout bug where the model hangs after "Thought" output with no stream activity; users must press Ctrl+Y to retry. Ongoing friction with long-generation flows.

4. **[#8625 — Windows terminal: pinyin input illegible](https://github.com/QwenLM/qwen-code/issues/8625)** (P2, open, 8 comments, welcome-pr) — Chinese input renders as unreadable pinyin characters in the Windows terminal. Notably flagged as `welcome-pr`, suggesting maintainers want community help.

5. **[#9219 — /review presubmit overlap matching is exact-line only](https://github.com/QwenLM/qwen-code/issues/9219)** (P2, open, 5 comments) — Multi-line ranges and semantic duplicates pass as noConflict in review presubmit checks, letting duplicated findings slip through. Maintainer-authored, pointing at a quality gap in the review pipeline.

6. **[#9821 — Native slash commands intermittently missing from Skill-tool surface](https://github.com/QwenLM/qwen-code/issues/9821)** (P2, open, 3 comments) — User-level native slash commands fail ~50% of the time via the Skill tool due to an async race. Nondeterministic across projects and versions 0.21.8+, frustrating for power users.

7. **[#8586 — Track activeWork and background Agent recovery](https://github.com/QwenLM/qwen-code/issues/8586)** (P2, feature-request, open, 4 comments) — Requests an explicit `activeWork` fact in daemon health plus a recovery path for background agents that outlive their foreground prompt. Signals growing demand for stronger background automation.

8. **[#9832 — DeepSeek v4 flash vision model missing image capability](https://github.com/QwenLM/qwen-code/issues/9832)** (P3, open, 3 comments) — User reports the backend hard-codes hostname checks that block image support for `deepseekv4flash-vision-exp`; the diagnosis insightfully notes the code has a `isDeepSeekHostname()` check but misses `flattenContentPar`. Community actively debugging the backend.

9. **[#8662 — Migrate TUI rendering from ink to OpenTUI](https://github.com/QwenLM/qwen-code/issues/8662)** (P3, open, 3 comments) — Proposes replacing the heavily patched ink 7 renderer (~1037-line patch) with OpenTUI for flicker-free rendering and first-class mouse support. A big architectural bet with `need-discussion` label.

10. **[#9831 — Relationship with craft-agents-oss](https://github.com/QwenLM/qwen-code/issues/9831)** (question, open, 2 comments) — Community member asks why an external project (craft-agents-oss) looks nearly identical and shares sessions. Maintainers have not yet responded; may indicate a fork or rebranding concern worth watching.

---

## Key PR Progress

1. **[#9740 — feat(review): make Step 4 verification execution-grade](https://github.com/QwenLM/qwen-code/pull/9740)** (open) — Adds `qwen review ab-drive` subcommand that runs one script against two trees and reports paired captures. Moves verification from prose to executable evidence.

2. **[#9728 — fix: repair Windows and macOS test lane failures](https://github.com/QwenLM/qwen-code/pull/9728)** (open, autofix/takeover) — Product fixes plus test-fixture and CI-harness repairs to revive the two platform lanes (#9370) without breaking `main`.

3. **[#9813 — feat(ci): request an area reviewer on PRs by changed-file paths](https://github.com/QwenLM/qwen-code/pull/9813)** (open) — Standalone workflow companion to #8668: routes PRs to area owners purely by changed file paths via an owner map.

4. **[#9739 — feat(core): bind PRs created via `gh pr create` in the session shell](https://github.com/QwenLM/qwen-code/pull/9739)** (open, autofix/takeover) — Closes the last binding-source gap for session↔PR features by detecting PRs created in-shell, not just via the Web Shell Git dialog.

5. **[#9805 — feat(review): promote language-pitfall and wrapper/proxy checks out of Agent 1a](https://github.com/QwenLM/qwen-code/pull/9805)** (open, autofix/takeover) — Splits two checks into dedicated Step 3A roles (Agent 1d for language footguns, Agent 1e for wrapper/proxy routing) for higher-effort dedicated scanning.

6. **[#9576 — feat(core): accept cross-session messages behind an inbound gate](https://github.com/QwenLM/qwen-code/pull/9576)** (open, autofix/takeover) — Sessions can bind UNIX sockets and receive marked, non-user messages from sibling sessions. Enables inter-agent communication with policy gating.

7. **[#9779 — fix(cli): normalize win32 drive-letter casing in MCP approval keys](https://github.com/QwenLM/qwen-code/pull/9779)** (open) — Fixes disagreement between `process.cwd()` casing and VS Code's `fsPath` casing, which caused MCP approval records to miss on Windows.

8. **[#9770 — fix(web-shell): cap React dev performance.measure accumulation](https://github.com/QwenLM/qwen-code/pull/9770)** (closed, autofix/takeover) — Bounds a React 19 dev-mode memory leak where the browser's user-timing buffer accumulates without limit, causing an idle Web Shell dev renderer OOM.

9. **[#9761 — feat(review): keep deferred suggestions recoverable off the PR page](https://github.com/QwenLM/qwen-code/pull/9761)** (open, autofix/takeover) — Makes the deferral list in the review body machine-readable so tooling arriving after the review can act on it.

10. **[#9273 — feat(review): capture-tui — rendering claims get pixels, not prose](https://github.com/QwenLM/qwen-code/pull/9273)** (open, autofix/needs-human) — Verifiers can drive a command inside a private tmux server, capture pane text to `.ans`, render a `.png` via `freeze` when available — providing actual visual evidence for TUI rendering claims.

---

## Feature Request Trends

- **Review-pipeline automation**: Multiple issues and PRs target making `/review` deterministic, execution-grade, and self-recovering (deferral lists, do-not-refute lists, area-based routing). The community is pushing for code-review quality gates that are verifiable by machine, not just model opinion.
- **Cross-session & background agents**: Requests for `activeWork` tracking, background-agent recovery, and cross-session messaging (PR #9576, Issue #8586) point toward a vision of Qwen Code as a multi-agent collaboration platform, not just a single-session CLI.
- **Web Shell / VS Code parity**: Repeated asks for drag-and-drop file support (#9743), lazy session creation fixes (#9595), and git update handling on dirty trees (#9769) show the web UI is becoming the primary surface many users expect feature parity with Copilot/Chat.
- **Config as single source of truth**: Issues around approval-mode value domains hand-copied across 20 files (#9145) and settings-schema divergence (#8752) reflect a desire for one canonical config that fails tests when it drifts.

---

## Developer Pain Points

- **Allowlist semantics broken**: `permissions.allow` misleadingly appears to restrict tools but the model still receives the full tool set — a trust issue for users who rely on it for safety or cost control.
- **Stream hangs and timeout errors**: The "No stream activity for 120000ms" error (#5975) is still the top-commented open bug; long outputs or slow providers hit hard timeouts with a retry prompt that loses context.
- **Platform-specific regressions**: Windows (pinyin rendering, MCP approval key casing) and macOS/Windows CI lanes failing (#9728) are recurring friction zones; win32 drive-letter casing is a subtle footgun for cross-IDE workflows.
- **Async races in the skill-tool surface**: Native slash commands intermittently missing (#9821) and session catalog refresh storms (#9562) suggest the async/session layer still has nondeterminism that erodes user trust — failures that work "~50% of the time" are particularly painful to debug.
- **Auth integration friction**: Vertex AI ADC requiring an API key that then breaks ADC (#9016) shows that cloud-provider auth paths still have sharp edges for enterprise users.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-24

*Data source: [github.com/Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI)*

---

## 1. Today's Highlights

The **v0.9.11 release** marks a major rebranding milestone: the project is now publicly known as **Codewhale** (Shannon Labs), with the legacy `deepseek-tui` npm package formally deprecated. The v0.9.12 milestone tracker ([#5573](https://github.com/Hmbown/CodeWhale/issues/5573)) has opened with a strong focus on **runaway-spend protection** and **safety/money P0 fixes**, signaling a maturing product posture. CI reliability is also a hot topic — the Linux workspace test gap for non-mirrored PR branches ([#5547](https://github.com/Hmbown/CodeWhale/issues/5547)) has an approved fix in flight ([#5590](https://github.com/Hmbown/CodeWhale/pull/5590)).

---

## 2. Releases

**[v0.9.11](https://github.com/Hmbown/CodeWhale/releases)** — released within the last 24h:

- Public product name is now **Codewhale** (lowercase technical identifiers: `codewhale` command, npm package, assets).
- Legacy `deepseek-tui` npm package is **deprecated** — no further releases.
- Post-tag fixes were recut at a fixed HEAD (unpublished tag recovery flow documented in [#5565](https://github.com/Hmbown/CodeWhale/pull/5565)).
- Includes truthfulness and tool-output redaction fixes ([#5559](https://github.com/Hmbown/CodeWhale/pull/5559)) landed just before tagging.

*Note: v0.9.12 is in active preparation — see milestone tracker [#5573](https://github.com/Hmbown/CodeWhale/issues/5573).*

---

## 3. Hot Issues (Top 10)

**#3368 — [security, reliability] Security hardening/code-scanning tracker (29 comments)**  
The longest-running public thread, tracking CodeQL findings, advisory-class reports, and integration commits. The community is watching this closely as the definitive security release gate.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/3368)

**#4326 — [bug, performance] RSS after cancelling 32-worker storm (6 comments)**  
A 32-worker PTY benchmark shows RSS increasing *after* cancellation. The debate centers on distinguishing allocator high-water retention from a real leak — a classic post-mortem question for fan-out architectures.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/4326)

**#5573 — [v0.9.12] Milestone tracker — start here (2 comments)**  
The official v0.9.12 roadmap with a P0/P1 priority table, led by **bound runaway spend** ([#5566](https://github.com/Hmbown/CodeWhale/issues/5566), already closed). The community is aligned on money-safety first.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5573)

**#5582 — [v0.9.12] Workflow owner snapshots collapse Degraded → Completed (3 comments)**  
A subtle state-machine bug: `Degraded` workflow runs are projected as `Completed` in owner snapshots, hiding partial failures. Raised by `jbovard2016` with a precise code citation.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5582)

**#5583 — [v0.9.12] workflow responseSchema failures need bounded repair (2 comments)**  
Schema mismatches hard-fail the run without a repair loop or raw-output receipts. The community wants bounded retry, not silent null success.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5583)

**#5547 — [reliability] CI: Linux workspace tests do not run for non-mirrored PR branches (3 comments)**  
The Ubuntu job is a placeholder; only mirrored branch prefixes (`work/v*`, `fix/*`, etc.) get real coverage. This is a silent-coverage landmine for integration branches like `codex/*`.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5547)

**#5585 — [bug] Stack overflow in `setup_confirm_toast_names_secret_store_and_global_scope` (2 comments)**  
A pre-existing SIGABRT on macOS, bisected to a commit before the 0.9.12 cycle. Debugging is blocked by nextest default stack sizing.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5585)

**#5588 — [provider neutrality] 18 DeepSeek-exclusive gates that should be neutral (0 comments)**  
A full audit of 2,281 `deepseek` occurrences identified 18 behavior gates that are conceptually provider-neutral but DeepSeek-gated (e.g., NVIDIA NIM env leak already fixed). This is the long tail of the rebrand.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5588)

**#5589 — [v0.9.12] Fleet config view: Enter loops, model switching buried (0 comments)**  
User-reported UX bug in the role-row selection: Enter appears to do nothing, and model switching is hard to discover.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5589)

**#5587 — [dead code] Dead-code sweep phases 2–4 (1 comment)**  
A methodical sweep of 379 `allow(dead_code)` sites: 18 truly-dead items (Tier B/C), 75 test-only markers, ~242 stale allows. The community appreciates this kind of disciplined cleanup.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5587)

---

## 4. Key PR Progress (Top 10)

**#5590 — CI: run Linux workspace tests on pull requests (CLOSED)**  
Direct answer to [#5547](https://github.com/Hmbown/CodeWhale/issues/5547): runs `cargo nextest run --workspace --all-features` on the GitHub Ubuntu leg regardless of branch prefix, plus workspace doctests and lockfile checks.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5590)

**#5576 — 0.9.12 integration: must-fix + UX fixes (OPEN, 24 commits)**  
The WIP integration branch for v0.9.12: R2 approval-scope family grant fix, R3 Chat-Completions SSE error frames, R4 (expense bounds), plus UX fixes. Tracker: [#5573](https://github.com/Hmbown/CodeWhale/issues/5573).  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5576)

**#5584 — fix(subagents): persist child approval receipts (OPEN)**  
Closes [#5543](https://github.com/Hmbown/CodeWhale/issues/5543): child approval prompts now commit durable `Asked` evidence before prompting and terminal outcomes before close.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5584)

**#5574 — Add Build Remote Agent phone pairing — gbr/1 (OPEN)**  
Optional phone-spectator pairing for desktop agents via `gbr-agent`, QR + 8-char code. Protocol stays gbr/1 (no fourth pair protocol).  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5574)

**#5561 — fix(engine): auto-retry reasoning-only clean-stop (CLOSED)**  
A live user hit a dead-end: reasoning model returned hidden reasoning + clean stop = "provider response was incomplete" with no auto-recovery. Now auto-retries instead of failing.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5561)

**#5563 — fix(onboarding): show all providers on first run (CLOSED)**  
First-run setup was opening on the local/self-hosted view with Ollama pre-selected — hiding DeepSeek and other hosted APIs behind a keypress. Now shows all providers.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5563)

**#5559 — fix(release): close pre-tag v0.9.11 truthfulness and tool-output gaps (CLOSED)**  
Same-version follow-up before tagging: credential-shaped redaction policy for `read`/shell results, plus truthfulness fixes.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5559)

**#5545 — fix(pricing): bill whole Beijing weekends off-peak for DeepSeek V4 (CLOSED)**  
DeepSeek's pricing page changed (effective 2026-08-23): off-peak rates apply all day on weekends (Beijing time). The UTC-hour-only logic was wrong for weekend billings.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5545)

**#5535 — Supervised operation stack (OPEN)**  
Five areas on one seam: lifecycle event outbox (JSONL + webhook), `/relaunch`, per-session control socket, and the goal-continuation quiet-period fix. Machine-readable supervision for long-lived sessions.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5535)

**#5524 — feat(tui): multi-file read_lints operation (CLOSED)**  
The model-visible `lsp` tool now supports `read_lints` for multiple workspace-relative files, reusing the session `LspManager` transport pool. Addresses [#4070](https://github.com/Hmbown/CodeWhale/issues/4070).  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5524)

---

## 5. Feature Request Trends

1. **Provider neutrality (post-rebrand)** — The `DeepSeekClient` rename ([#5103](https://github.com/Hmbown/CodeWhale/issues/5103)), the 18 suspect gates audit ([#5588](https://github.com/Hmbown/CodeWhale/issues/5588)), and the Responses dialect profiling work ([#5092](https://github.com/Hmbown/CodeWhale/issues/5092), [#5093](https://github.com/Hmbown/CodeWhale/issues/5093), [#5094](https://github.com/Hmbown/CodeWhale/issues/5094)) all push toward a provider-agnostic core.

2. **Richer agent tooling (LSP + browser + debugger)** — Three major tool surfaces in flight: LSP navigation/rename/code-actions ([#3975](https://github.com/Hmbown/CodeWhale/issues/3975)), Playwright-backed browser automation ([#3358](https://github.com/Hmbown/CodeWhale/issues/3358)), and a debugger protocol surface ([#3981](https://github.com/Hmbown/CodeWhale/issues/3981)). Visual inspection artifacts ([#3145](https://github.com/Hmbown/CodeWhale/issues/3145)) extend this to UI-task evidence loops.

3. **Architecture cleanup (v0.9.3 umbrella)** — Large refactors converging runtime ownership ([#3306](https://github.com/Hmbown/CodeWhale/issues/3306)), splitting the setup wizard ([#3954](https://github.com/Hmbown/CodeWhale/issues/3954)), and merging JobManager/TaskManager ([#4167](https://github.com/Hmbown/CodeWhale/issues/4167)).

4. **Bounded spend / safety** — The v0.9.12 P0 work (`max_steps` defaults, cumulative wall-clock limits) is the top priority, with community consensus that unattended runaway spend is unacceptable.

5. **Privacy controls** — `.codewhaleignore` ([#4069](https://github.com/Hmbown/CodeWhale/issues/4069)) for excluding secrets/vendor trees from agent discovery, mirroring `.cursorignore`.

---

## 6. Developer Pain Points

- **Silent CI gaps** — Non-mirrored PR branches get zero Linux test coverage ([#5547](https://github.com/Hmbown/CodeWhale/issues/5547)); the fix landed quickly but this is a systemic trust issue.

- **Memory behavior after cancellation** — RSS rising *after* a cancel ([#4326](https://github.com/Hmbown/CodeWhale/issues/4326)) is counterintuitive and hard to attribute to allocator retention vs. a real leak.

- **Spend runaway fear** — Both hosts defaulting to `u32::MAX` turns with an inert tool-call budget ([#5566](https://github.com/Hmbown/CodeWhale/issues/5566)) makes unattended runs a financial risk.

- **Hard-fail on recoverable conditions** — Reasoning-only clean-stop dead-ending ([#5561](https://github.com/Hmbown/CodeWhale/pull/5561)) and `responseSchema` failures without repair ([#5583](https://github.com/Hmbown/CodeWhale/issues/5583)) both force manual resubmits.

- **Stack-overflow debugging** — The macOS SIGABRT in the toast test ([#5585](https://github.com/Hmbown/CodeWhale/issues/5585)) is pre-existing and hard to bisect under default nextest stack sizing.

- **Dead-code debt** — 379 `allow(dead_code)` sites, 18 truly-dead items, and ~242 stale allows ([#5587](https://github.com/Hmbown/CodeWhale/issues/5587)) make refactors riskier than they should be.

- **Legacy-compat naming friction** — The `DeepSeekClient`/`deepseek_client` internals ([#5103](https://github.com/Hmbown/CodeWhale/issues/5103)) create cognitive overhead for contributors coming from the rebrand, even though behavior is provider-neutral.

---

*Digest compiled 2026-08-24 from public GitHub data. All links point to the rebranded Codewhale repository.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*