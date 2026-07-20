# AI CLI Tools Community Digest 2026-07-20

> Generated: 2026-07-20 01:26 UTC | Tools covered: 9

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
**Date: 2026-07-20**

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape continues to mature rapidly, with seven major tools now demonstrating distinct community dynamics and feature trajectories. Today's digest reveals a community-wide emphasis on **agent reliability**, **security hardening**, and **platform parity**, with Windows and ARM64 compatibility emerging as persistent pain points across multiple tools. A notable undercurrent is the growing concern around **provider lock-in and silent server-side changes**, particularly from Claude Code users facing opaque model downgrades and feature removal. The ecosystem is also witnessing convergence around **hook/plugin architectures**, **multi-agent orchestration patterns**, and **observability requirements** for production deployments, signaling a shift from experimental adoption to enterprise-grade expectations.

---

## 2. Activity Comparison

| Tool | New/Updated Issues | PRs Active Today | Release Status | Community Engagement Signal |
|------|-------------------|------------------|----------------|---------------------------|
| **Claude Code** | 10 hot issues highlighted | 10 active PRs | v2.1.215 released (minor) | Highest issue engagement (#18170: 133 comments, 275👍) |
| **OpenAI Codex** | 10 hot issues highlighted | 10 active PRs | No new release | Strong Windows-focused activity (6/10 top issues) |
| **Gemini CLI** | 10 hot issues highlighted | 10 active PRs | Nightly v0.52.0 (daily train) | Agent-focused discussion (#3132: 45 comments) |
| **GitHub Copilot CLI** | 10 hot issues highlighted | 1 PR (admin only) | No new release | Regression-heavy day (plan mode, context limits) |
| **Kimi Code CLI** | 10 hot issues highlighted | 9 active PRs | No new release | High session-management fix activity (3 PRs from Nas01010101) |
| **OpenCode** | 10 hot issues highlighted | 10 active PRs | No new release | 2.0 architecture stabilization push |
| **Pi** | 10 hot issues highlighted | 9 PRs merged | No new release (active dev) | Highest PR velocity (9 merged today) |
| **Qwen Code** | 10 hot issues highlighted | 10 active PRs | v0.20.0 + v0.20.1-preview released | Dual-release day; subagent resource contention focus |
| **DeepSeek TUI (CodeWhale)** | 10 hot issues highlighted | 10 active PRs (6 closed, 4 open) | No new release | Localization + MCP infrastructure push (19 closed PRs today) |

**Key observation:** Claude Code and OpenCode show the highest community engagement per issue, while Pi and DeepSeek TUI demonstrate the fastest PR throughput. Gemini CLI maintains a stable nightly release cadence, whereas GitHub Copilot CLI shows a development lull (1 PR today).

---

## 3. Shared Feature Directions

### 3.1 Multi-Agent & Sub-Orchestration (7/7 tools)
- **All tools** have open issues around subagent reliability, resource contention, and observability
- **Claude Code**: Nested subagent ownership bugs (#75043), async completion failures
- **Gemini CLI**: Subagent MAX_TURNS misreported as success (#22323), generalist agent hangs (#21409)
- **Qwen Code**: Subagent mutates main session model (#7156), resource starvation (#7254)
- **Kimi Code**: Fork/undo corruption in multi-turn sessions (#2517)
- **OpenCode**: Event-stream scaling for V2 multi-TUI architecture

### 3.2 Platform Parity & Windows Support (6/7 tools)
- **OpenAI Codex**: 6/10 top issues are Windows-specific performance bugs (WMI, DWM, HID enumeration)
- **Claude Code**: macOS copy-paste failures (#66192)
- **Qwen Code**: Windows Docker sandbox invalid workspace CWD (#7139)
- **DeepSeek TUI**: Windows argument parsing regression (#4564)
- **Pi**: Windows path handling broken in `find` tool (#6817)
- **Gemini CLI**: PowerShell installation guidance needed (#28447)

### 3.3 Hook/Plugin System Evolution (5/7 tools)
- **Claude Code**: PreToolUse prompt-hook regression (#78527), rule prefix requirements (#79148)
- **Kimi Code**: New `MessageDisplay` streaming hook proposed (#2511/#2512)
- **OpenCode**: Skill picker inline selector (#33019)
- **Pi**: Extension hooks for retry lifecycle, raw response streams
- **DeepSeek TUI**: MCP hot-reload capability (#4588)

### 3.4 Observability & Cost Tracking (5/7 tools)
- **GitHub Copilot CLI**: ACP server lacks token/context usage (#4174)
- **Qwen Code**: Missing `reasoning_tokens` in local inference (#7236)
- **OpenCode**: Event table unbounded growth (#33356, 13GB+)
- **Pi**: Retry lifecycle observability for extensions (#6836)
- **Claude Code**: Model/thinking mode indicators in VS Code (#28986)

### 3.5 Safety, Security & Trust (4/7 tools)
- **Claude Code**: Silent server-side experiments (#75607), PDF hallucination with exfil payload (#79265), prompt injection in subagents (#79269)
- **OpenCode**: Open redirect vulnerability in OAuth flow (#37807)
- **Qwen Code**: Credential leakage to subprocesses (#7256)
- **DeepSeek TUI**: Environment-level tool sandboxing (#4042, closed today)

### 3.6 Configuration & Session Persistence (4/7 tools)
- **Kimi Code**: Frozen system prompt on session resume (#2420)
- **Pi**: `model_change` silently overwritten on session restore (#6822)
- **Claude Code**: Auto-update override despite `autoUpdates: false` (#75607)
- **OpenCode**: Cmd+O shortcut registration regression in new layout (#37830)

---

## 4. Differentiation Analysis

### Feature Focus & Target Users

| Tool | Core Differentiation | Primary Target User | Current Development Phase |
|------|---------------------|-------------------|-------------------------|
| **Claude Code** | Deep agentic workflows, complex orchestration | Professional developers needing autonomous multi-step tasks | **Maturity** — v2.x stable; community demanding stability & trust |
| **OpenAI Codex** | Desktop-first IDE integration, rich TUI | Enterprise teams in IDE-centric workflows | **Scaling** — Windows performance catch-up; desktop app focus |
| **Gemini CLI** | Agent sub-class architecture, nightly innovation | Developers exploring cutting-edge Google AI features | **Rapid iteration** — daily nightlies; agent extensibility |
| **GitHub Copilot CLI** | GitHub ecosystem integration, plan-mode | GitHub-centric DevOps workflows | **Consolidation** — regressions suggest refactoring churn |
| **Kimi Code CLI** | Clean session model, growing hooks system | Developers needing reliable session workflows | **Maturing** — Session model hardening; hooks expansion |
| **OpenCode** | V2 event-sourcing architecture, high customizability | Power users who want deep configuration | **Architecture transition** — 2.0 stabilization with growing pains |
| **Pi** | Provider-agnostic design, broad model support | Multi-provider users, cost-conscious teams | **Growth** — Fastest PR velocity; provider diversity focus |
| **Qwen Code** | Alibaba/DashScope ecosystem, daemon architecture | Users in Qwen/Chinese cloud ecosystem | **Dual-track** — Stable release + preview features |
| **DeepSeek TUI** | Rust-based performance, localization | Users wanting fast, localized CLI experience | **Feature acceleration** — MCP, localization, first-run UX |

### Technical Approach Distinctions

- **Architecture**: OpenCode (event-sourcing V2) vs. Qwen Code (daemon process) vs. Gemini CLI (nightly monorepo)
- **Platform Strategy**: OpenAI Codex (Desktop app) vs. Claude Code (CLI-only, VS Code extension) vs. Pi (provider-agnostic)
- **Safety Model**: Claude Code (server-side classifiers, prompt hooks) vs. DeepSeek TUI (environment-level tool sandboxing) vs. Pi (configurable permission rules)
- **Release Cadence**: Gemini CLI (daily nightlies) vs. Qwen Code (stable + preview dual-track) vs. GitHub Copilot CLI (infrequent, major version)

---

## 5. Community Momentum & Maturity

### High Activity, Rapid Iteration
- **Pi**: Highest PR velocity (9 merged today), broad provider support expansion, active issue resolution
- **DeepSeek TUI (CodeWhale)**: 19 closed PRs, major MCP infrastructure, localization push — indicating rapid feature development
- **Gemini CLI**: Daily nightlies, major dependency upgrades (TypeScript v7, GenAI SDK v2.11), strong agent extensibility discussion

### Mature but Cautious
- **Claude Code**: Highest community engagement per issue; community is vocal about trust and reliability concerns
- **OpenAI Codex**: Active Windows performance focus suggests a maturing product addressing platform gaps
- **GitHub Copilot CLI**: Development lull (1 PR) despite regression influx; signals possible prioritization shift

### Emerging Concerns
- **Claude Code**: Trust erosion from silent server-side experiments, safety classifier false positives, and hallucination security risks
- **GitHub Copilot CLI**: Plan-mode regressions and context limits suggest architectural strain
- **Kimi Code CLI**: Session corruption bugs indicate foundational reliability work still in progress

---

## 6. Trend Signals

### Critical for Technical Decision-Makers

1. **Agent Orchestration Reliability is the #1 Cross-Cutting Concern**
   - Every tool has open issues about subagent failures, resource contention, or state corruption
   - **Implication**: Production deployments of multi-agent workflows should incorporate defensive patterns — session isolation, timeout guards, and explicit error handling

2. **Windows Experience Remains the Weakest Link**
   - OpenAI Codex, Qwen Code, DeepSeek TUI, and Pi all show significant Windows-specific bugs
   - **Implication**: Teams with mixed-OS environments should budget for Windows-specific testing and workaround time

3. **Security Incidents Are Increasing in Sophistication**
   - Claude Code's PDF hallucination with exfiltration payload (#79265) and prompt injection in subagents (#79269) represent a new class of risk
   - **Implication**: Implement output sanitization, credential redaction, and audit trails — especially for tools with agentic file-reading capabilities

4. **Provider Lock-In Fears Are Driving Multi-Provider Architectures**
   - Pi's provider-agnostic design and OpenCode's auto-discovery demands reflect a broader push against vendor lock-in
   - **Implication**: Evaluate tools that support multiple backends; expect increased investment in cross-provider compatibility

5. **Observability Is Transitioning from Nice-to-Have to Must-Have**
   - Token tracking, cost metrics, and session debugging are now requested across all major tools
   - **Implication**: Production adoption of AI CLI tools requires hooking into token usage and session replay capabilities

6. **Platform-Specific Optimizations Are Becoming Critical**
   - ARM64 native support (OpenCode #19130), Wayland compatibility (Gemini CLI #21983), and PTY automation support (GitHub Copilot CLI #4180) indicate that general compatibility is no longer sufficient
   - **Implication**: Tool selection should include a platform compatibility matrix for your target deployment environments

7. **Open Source Contributions Are Driving Feature Velocity**
   - Pi (9 PRs merged), DeepSeek TUI (19 closed PRs), and Claude Code (10 active PRs) demonstrate active contributor bases
   - **Implication**: Community health and PR review responsiveness are leading indicators of long-term tool sustainability

---

**Bottom Line for Technical Decision-Makers:**
The AI CLI tools ecosystem is in a **consolidation through maturation** phase. Claude Code leads in raw capability but faces trust challenges. Pi offers the best multi-provider flexibility and development velocity. OpenAI Codex is the strongest IDE-integrated experience but struggles with Windows. Gemini CLI is the most innovative daily driver. **Choose based on your platform mix, provider dependencies, and tolerance for rapid-change risk.**

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report based on the analysis of the `anthropics/skills` repository.

---

## Claude Code Skills Community Highlights Report (Data as of 2026-07-20)

### 1. Top Skills Ranking

The following Skills (Pull Requests) garnered the most community attention and discussion, primarily driven by critical fixes to the core `skill-creator` toolchain.

1.  **#1298: fix(skill-creator): run_eval.py always reports 0% recall**
    - **Functionality:** Fixes the `run_eval.py` script, which is central to the skill-description optimization loop. The bug caused a 0% recall rate across all queries, effectively making the optimization process useless.
    - **Discussion:** High traffic due to a critical bug affecting all skill creators. The PR addresses a well-documented issue (#556) with multiple independent reproductions, covering fixes for artifact installation, Windows stream reading, and trigger detection.
    - **Status:** Open
    - **Link:** [PR #1298](https://github.com/anthropics/skills/pull/1298)

2.  **#1367: feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate**
    - **Functionality:** Proposes a meta-skill that audits AI output before delivery. It performs mechanical file verification followed by a four-dimension reasoning audit prioritized by damage severity. Designed to be universal across projects and tech stacks.
    - **Discussion:** Represents a high level of community sophistication, moving beyond simple skill creation to implementing quality assurance and governance for AI outputs. The concept of a "reasoning quality gate" generated significant interest.
    - **Status:** Open
    - **Link:** [PR #1367](https://github.com/anthropics/skills/pull/1367)

3.  **#1323: fix(skill-creator): run_eval trigger detection misses real skill name**
    - **Functionality:** Another critical fix for `run_eval.py`. This PR addresses a specific scenario where the trigger detection logic fails to identify a skill that has been triggered, causing the optimization loop to report 0% recall and fail to improve descriptions.
    - **Discussion:** This is a follow-on fix to the core `skill-creator` reliability problem, highlighting that the system is undergoing a period of intense refinement and debugging within the community.
    - **Status:** Open
    - **Link:** [PR #1323](https://github.com/anthropics/skills/pull/1323)

4.  **#514: Add document-typography skill**
    - **Functionality:** A skill for typographic quality control in generated documents. It prevents common problems like orphan words, widow paragraphs, and numbering misalignment in AI-generated documents.
    - **Discussion:** A highly practical skill addressing a universal pain point for AI-generated content. The discussion focused on the specific typographic rules and their implementation.
    - **Status:** Open
    - **Link:** [PR #514](https://github.com/anthropics/skills/pull/514)

5.  **#486: Add ODT skill — OpenDocument text creation and template filling**
    - **Functionality:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods), targeting users of LibreOffice and open-source standards.
    - **Discussion:** Strong demand for interoperability with non-Microsoft document formats. The community showed interest in robust template filling and parsing capabilities.
    - **Status:** Open
    - **Link:** [PR #486](https://github.com/anthropics/skills/pull/486)

6.  **#1099 / #1050: fix(skill-creator): Windows subprocess & encoding bugs**
    - **Functionality:** A pair of PRs addressing the fact that `skill-creator` scripts were functionally broken on Windows due to Unix-specific assumptions about subprocess handling, PATH extensions, and character encoding.
    - **Discussion:** High engagement from Windows users. The community identified and collaborated on fixes for `[WinError 2]`, `[WinError 10038]`, and `cp1252` encoding issues, which blocked a significant portion of developers from using the toolchain.
    - **Status:** Open
    - **Link:** [PR #1099](https://github.com/anthropics/skills/pull/1099) | [PR #1050](https://github.com/anthropics/skills/pull/1050)

### 2. Community Demand Trends

Analysis of the most-discussed Issues reveals the following key demand trends:

- **Cross-Platform Compatibility (Windows):** The single biggest pain point. Three of the top-10 most-commented issues (#1061, #556, #1175) deal with the `skill-creator` toolchain being broken on Windows, specifically around subprocess handling and encoding errors. This is the community's most urgent infrastructure need.
- **Security & Trust Boundaries:** Issue #492 ("Security: Community skills distributed under anthropic/ namespace") is the most-commented issue overall (39 comments). There is deep concern about trust abuse, where community skills hosted under the `anthropic/` namespace could deceive users into granting elevated permissions.
- **Skill Sharing & Management:** There is strong demand for better distribution and management of skills, especially within organizations. Issue #228 ("Enable org-wide skill sharing") and #189 ("duplicate skills") show a need for a proper library or registry. Issue #62 ("All my skills have disappeared") indicates fragility in the local skill management UX.
- **Quality Assurance & Governance:** The community is moving beyond "what can a skill do?" to "how do we trust what a skill does?" Issues #412 (agent-governance) and #1385 (Reasoning Quality Gate Pipeline) show a desire for meta-skills that provide safety, audit trails, and validation.

### 3. High-Potential Pending Skills

These PRs are actively discussed and represent near-term additions to the ecosystem:

- **`#1367: self-audit skill` - [Link](https://github.com/anthropics/skills/pull/1367):** A quality gate pipeline for reasoning and file verification. The most advanced skill concept in active discussion.
- **`#1323: fix skill-creator trigger detection` - [Link](https://github.com/anthropics/skills/pull/1323):** A critical fix for the `skill-creator` toolchain's core bug. Likely to be merged quickly to unblock other development.
- **`#1302: color-expert skill` - [Link](https://github.com/anthropics/skills/pull/1302):** A domain-specific skill for color naming, spaces (OKLCH, CAM16), and palettes. Likely to be merged as a self-contained, high-value skill.
- **`#1298: fix skill-creator 0% recall` - [Link](https://github.com/anthropics/skills/pull/1298):** The most comprehensive fix for the `skill-creator` pipeline bug. This is the likely merge candidate for resolving the `run_eval` problem.
- **`#723: testing-patterns skill` - [Link](https://github.com/anthropics/skills/pull/723):** A comprehensive testing skill covering the full stack (unit, React, E2E, visual). High community value for developers.

### 4. Skills Ecosystem Insight

The community's most concentrated demand is not for any single domain-specific skill, but for **the reliability and trustworthiness of the skill-creation toolchain itself**, on all major platforms, followed closely by the demand for **meta-skills that govern and audit AI behavior**.

---

# Claude Code Community Digest — 2026-07-20

## Today's Highlights

A minor release (v2.1.215) landed that removes automatic `/verify` and `/code-review` invocation — Claude now waits for explicit user commands. The community remains heavily focused on copy-paste bugs in the TUI (the top issue has 133 comments and 275 👍), with a broader undercurrent of concern about silent server-side experiments, model downgrades, and safety classifier false positives. Several PRs from contributor `Codeturion` fix documentation drift and shell compatibility issues across the open-source plugin system.

## Releases

**v2.1.215** — Claude no longer runs `/verify` and `/code-review` skills automatically; invoke them with `/verify` or `/code-review` when desired. This is a quality-of-life change for users who found the auto-run disruptive.

https://github.com/anthropics/claude-code/releases/tag/v2.1.215

## Hot Issues

1. **#18170 — Copy/paste includes unwanted indentation and trailing spaces** (133 comments, 275 👍)  
   The most-voted issue by far. Terminal output copies with leading tabs/spaces matching prompt visuals, plus trailing whitespace. Persistent since January; community frustration is high.  
   https://github.com/anthropics/claude-code/issues/18170

2. **#66192 — Copy-paste does not work (macOS, TUI)** (28 comments, 29 👍)  
   Related but distinct: complete copy-paste failure on macOS. Likely a regression.  
   https://github.com/anthropics/claude-code/issues/66192

3. **#64108 — Tool calls emitted as literal text instead of executing** (16 comments, 30 👍)  
   Critical reliability bug: during long sessions, tool calls leak as raw XML with a stray `court` token. Affects Opus on CLI; undermines trust in agentic workflows.  
   https://github.com/anthropics/claude-code/issues/64108

4. **#75043 — Nested subagent ownership and async bugs** (13 comments, 3 👍)  
   Spawned agents always run async, completion notifications never reach parent, TaskStop fails after resume. Complex multi-agent orchestration is broken.  
   https://github.com/anthropics/claude-code/issues/75043

5. **#75607 — Server-side experiment silently removed Opus thinking summaries + override of autoUpdates** (6 comments, 8 👍)  
   Alarming: Anthropic pushed a server-side experiment (`x-cc-atis`) that removed thinking summaries without notice. CLI also self-updated despite `autoUpdates: false`. Privacy and trust concerns.  
   https://github.com/anthropics/claude-code/issues/75607

6. **#78527 — PreToolUse prompt-hook deny stops entire turn instead of returning tool error** (1 comment, 1 👍)  
   Regression in v2.1.210: security hooks using `{ok: false}` now halt the turn instead of returning a tool error, breaking LLM-judge security workflows.  
   https://github.com/anthropics/claude-code/issues/78527

7. **#79254 — Anthropic API Error: 500 Internal Server Error** (1 comment)  
   Fresh API outage reported today. No response yet; concern about backend stability.  
   https://github.com/anthropics/claude-code/issues/79254

8. **#79278 — Claude Code caused system corruption during Debian installation** (0 comments)  
   User reports Fable model performed unsafe file modifications that corrupted a Chromebook's Debian install. Safeguard downgraded to Opus when user tried to fix.  
   https://github.com/anthropics/claude-code/issues/79278

9. **#79269 — Prompt injection appeared in subagent context** (0 comments)  
   Possible security incident: injected instruction framework found in subagent output that wasn't in parent prompt or on disk. Coincided with safety classifier being unavailable.  
   https://github.com/anthropics/claude-code/issues/79269

10. **#79265 — Opus 4.8 fabricated attached-PDF content with embedded prompt injection payload** (0 comments)  
    Serious hallucination/security issue: model emitted fake document with exfil URL and concealment instruction instead of reading the actual PDF.  
    https://github.com/anthropics/claude-code/issues/79265

## Key PR Progress

1. **#79237 — Fix: add `_is_isolated_worktree` guard**  
   Prevents spawn tasks from mutating parent repo checkout by ensuring git isolation. Important for safe multi-agent git operations.  
   https://github.com/anthropics/claude-code/pull/79237

2. **#79211 — Fix: remove stray `re` syntax error in `rule_engine.py`**  
   A dangling `re` statement broke the module, causing hooks to error out and incorrectly flag computational work.  
   https://github.com/anthropics/claude-code/pull/79211

3. **#79210 — Fix: strip ANSI escape fragments from model value before persisting to settings.json**  
   `/model` picker was saving ANSI bold fragments like `[1m` into config instead of the raw model ID.  
   https://github.com/anthropics/claude-code/pull/79210

4. **#54094 — Fix: quote `$CLAUDE_PLUGIN_ROOT` in plugin hook commands**  
   Unquoted paths break when the plugin root contains spaces. Affects five in-tree plugins. Long-open (since April).  
   https://github.com/anthropics/claude-code/pull/54094

5. **#79152 — Fix: only log Statsig duplicate-comment metric when a duplicate was posted**  
   Unconditional metric emission was inflating Statsig counts with false positives.  
   https://github.com/anthropics/claude-code/pull/79152

6. **#79151 — Fix: honor thumbs-down from any user when skipping duplicate auto-close**  
   Only the issue author's 👎 was respected; now any user's reaction prevents auto-close.  
   https://github.com/anthropics/claude-code/pull/79151

7. **#79150 — Docs: align code-review README with current validation-based command**  
   README described a pipeline (blame agent, confidence scoring) that no longer exists.  
   https://github.com/anthropics/claude-code/pull/79150

8. **#79148 — Fix: add mandatory `hookify.` prefix to example rule filenames**  
   Shipped examples lacked the required prefix, causing silent non-discovery when copied into `.claude/`.  
   https://github.com/anthropics/claude-code/pull/79148

9. **#79140 — Fix: use `disable-model-invocation` to hide ralph-wiggum commands**  
   `/ralph-loop` was invocable by the model despite being user-only, creating infinite loop risk. Uses documented hidden-key for the first time.  
   https://github.com/anthropics/claude-code/pull/79140

10. **#79129 — Fix: guard empty FLAGS array expansion in `gh.sh` for bash < 4.4**  
    macOS default bash (3.2) crashes on empty array expansion under `set -u`. Fixes usage example and basic invocations.  
    https://github.com/anthropics/claude-code/pull/79129

## Feature Request Trends

- **Real-time steering (#64624, 12 👍):** Send messages mid-generation without queueing or discarding progress. Highly requested — the "Interrupt and steer" documentation mentions it but it's not implemented.
- **Configurable background session idle timeout (#79268):** Supervisor kills background sessions after ~1 hour; users want configurable timeouts.
- **Model and thinking mode indicators in VS Code (#28986, 58 👍):** Currently invisible which model is active or whether thinking is enabled.
- **Option to disable image path interpretation (#73813, 2 👍):** Pasted paths like `/some/path/image.png` get treated as image content, breaking CLI workflows.

## Developer Pain Points

1. **Copy-paste is fundamentally broken in the TUI** — Issues #18170 and #66192 together show that terminal copy behavior is the #1 pain point, spanning unwanted indentation, trailing spaces, and complete failure on macOS.

2. **Safety/security classifiers are overzealous and unreliable** — Multiple reports today alone (#79264, #79266, #79271, #79249) of false positive flags on benign content (R code minification, dictionary lookups, court search). Several users report model downgrades from Fable to Opus triggered by security-related tasks.

3. **Silent server-side changes erode trust** — Issue #75607 demonstrates Anthropic can push experiments that remove features, override local settings (`autoUpdates: false`), and provide no notice. This is a governance and transparency concern for professional users.

4. **Model hallucination is now a security risk** — Issue #79265 (fabricated PDF with exfil URL) and #79269 (prompt injection in subagent) suggest that large-context hallucination can produce output that mimics attacks. These need urgent investigation.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-20

## Today's Highlights
The Codex community is experiencing a sustained surge in Windows performance issues, with four separate bug reports updated today covering CPU/memory runaway in WMI, Windows Defender conflicts, DWM handle leaks, and periodic app hangs. On a positive note, the team merged 14 performance-oriented PRs from `copyberry[bot]` focused on TUI rendering optimization, memory reduction, and thread notification buffering. The long-running `syspolicyd`/`trustd` macOS resource leak (Issue #25719) remains the most active thread with 63 comments and 251 upvotes.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[macOS] Codex Desktop triggers `syspolicyd`/`trustd` CPU/memory runaway** (#25719)  
   *63 comments, 251 👍* — The top-voted open bug. macOS users report persistent resource drain from system security daemons when Codex runs. Still unresolved after 7 weeks.  
   [View Issue](https://github.com/openai/codex/issues/25719)

2. **[Windows] App frequently freezes/stutters on Windows 11 Pro** (#20214)  
   *54 comments, 68 👍* — Despite adequate hardware (Ryzen 5, 32GB RAM), users experience systemic UI lag. Updated today, indicating this is still actively investigated.  
   [View Issue](https://github.com/openai/codex/issues/20214)

3. **[Windows] `serialport.node` delay-load failures cause severe UI lag** (#33375) — *CLOSED*  
   *46 comments, 30 👍* — A high-impact fix was deployed. The root cause was repeated native module loading failures in the Electron renderer.  
   [View Issue](https://github.com/openai/codex/issues/33375)

4. **[Windows] App hangs at launch due to HID device enumeration blocking** (#33780)  
   *39 comments, 8 👍* — A non-responsive HID device causes the main process to block in `hid.dll` indefinitely. Emerging as a major Windows startup issue.  
   [View Issue](https://github.com/openai/codex/issues/33780)

5. **[Windows] CrBrowserMain crash when Browser Use opens a page** (#32683)  
   *25 comments, 7 👍* — Codex crashes with `0xC0000005` (access violation) in Chrome DLL when using in-app browser features. Affects ChatGPT Pro subscribers.  
   [View Issue](https://github.com/openai/codex/issues/32683)

6. **[Regression] Encrypted MultiAgentV2 messages remove readable audit trail** (#28058)  
   *21 comments, 99 👍* — Privacy-related encryption for multi-agent messages inadvertently broke debugging transparency. High community concern with strong upvote ratio.  
   [View Issue](https://github.com/openai/codex/issues/28058)

7. **[Windows] Orphan `git.exe`/`conhost.exe` process spawning** (#17229)  
   *24 comments, 6 👍* — Codex repeatedly spawns `git status --porcelain` processes that never terminate, leaving orphaned console processes. Open since April.  
   [View Issue](https://github.com/openai/codex/issues/17229)

8. **[Windows] Periodic 15s AppHang / 10s responsive cycle in 26.715** (#33884)  
   *15 comments* — New regression in latest Windows build. UI alternates between frozen and responsive states in a predictable cycle.  
   [View Issue](https://github.com/openai/codex/issues/33884)

9. **[Linux] VS Code extension panel stuck loading — `net::ERR_FAILED`** (#32530)  
   *11 comments, 12 👍* — Local webview assets fail to load on Ubuntu 26.04. Pro subscribers affected. Suggests packaging issues for Linux distribution.  
   [View Issue](https://github.com/openai/codex/issues/32530)

10. **[Hooks] Hooks no longer run after Desktop update** (#21639)  
    *22 comments, 6 👍* — Post-update regression where custom hooks stop executing entirely. Still unaddressed after 73 days.  
    [View Issue](https://github.com/openai/codex/issues/21639)

## Key PR Progress

1. **[CLOSED] Avoid redundant TUI subagent metadata requests** (#34234) — Skip backfill for fresh/forked threads that cannot have pre-existing descendants. Reduces unnecessary API calls on new conversations.  
   [View PR](https://github.com/openai/codex/pull/34234)

2. **[CLOSED] Persist names for paginated threads** (#34229) — Adds a nullable `name` column to thread metadata, enabling distinct user-facing names for paginated threads without needing rollout metadata writes.  
   [View PR](https://github.com/openai/codex/pull/34229)

3. **[CLOSED] Cache finalized Markdown history rendering** (#34223) — Caches rendered lines for finalized agent messages and plans, invalidating only on width changes. Directly reduces UI jank in long threads.  
   [View PR](https://github.com/openai/codex/pull/34223)

4. **[CLOSED] Avoid buffering replay-irrelevant thread notifications** (#34222) — Filters out raw response items, realtime audio, and other non-consumed notifications from TUI replay buffers, reducing memory pressure.  
   [View PR](https://github.com/openai/codex/pull/34222)

5. **[CLOSED] Speed up TUI Markdown layout** (#34216) — Bulk-allocates table widths, reuses styled-line data, and optimizes URL detection across span boundaries. A pure performance win for terminal rendering.  
   [View PR](https://github.com/openai/codex/pull/34216)

6. **[CLOSED] Avoid retaining decoded MCP images in history cells** (#34206) — Decodes MCP image content only for validation, then discards the decoded buffer. History cells store only a placeholder. Memory optimization.  
   [View PR](https://github.com/openai/codex/pull/34206)

7. **[OPEN] Kill timed-out Git status process groups** (#30235) — On Unix, runs `git status` in its own process group so that timeouts kill both the wrapper and the actual Git process. Addresses the orphan process problem from #17229.  
   [View PR](https://github.com/openai/codex/pull/30235)

8. **[CLOSED] Avoid liveness races when starting side conversations** (#34199) — Seeds agent navigation data before the fork response completes, preventing false "thread unavailable" errors during rapid conversation forking.  
   [View PR](https://github.com/openai/codex/pull/34199)

9. **[CLOSED] Start side conversations without replaying inherited turns** (#34198) — Newly forked side conversations now start with an empty UI instead of replaying the parent thread's history. Clean UX improvement for multi-thread workflows.  
   [View PR](https://github.com/openai/codex/pull/34198)

10. **[CLOSED] Avoid cloning thread data when rendering transcripts** (#34194) — Makes `thread_to_transcript_cells` consume the `Thread`, moving owned data into history cells instead of cloning. Reduces allocations during transcript rendering.  
   [View PR](https://github.com/openai/codex/pull/34194)

## Feature Request Trends

- **Voice/Push-to-Talk for IDE extension** (Issue #3000, 193 👍) — Strong demand for dictation directly within the Codex IDE panel. Community has been asking for ~11 months.
- **Configurable worktree location** (Issue #10599, 66 👍) — macOS users want control over where Git worktrees are created, instead of always landing in a default directory.
- **Credit usage control toggle** (Issue #28382, 6 👍) — Users want a setting to pause Codex when included usage is exhausted rather than automatically consuming purchased credits.
- **Explicit session deletion controls** (Issue #24610, 15 👍) — Privacy-conscious developers want proper deletion (not just archiving) of cloud sessions that may contain sensitive project context.
- **Reduced motion/accessibility controls** (Issue #31382, 3 👍) — Pet overlay animations ignore per-app settings when Windows animation effects are disabled, indicating broader accessibility polish gaps.

## Developer Pain Points

- **Windows performance degradation dominates the tracker** — 6 of the top 10 updated issues today are Windows-specific performance bugs: WMI Provider Host CPU spikes, Windows Defender conflicts, DWM handle accumulation, HID enumeration hangs, periodic app freezes, and orphaned Git processes. The Windows experience remains the platform with the most friction.
- **Long-standing regression resolution is slow** — Bugs like the hooks regression (#21639, 73 days open) and the `syspolicyd` macOS leak (#25719, 49 days open) remain unfixed despite high community engagement. The encryption audit trail issue (#28058) has 99 upvotes but no visible resolution path.
- **Linux ecosystem gaps** — The VS Code extension blank panel issue (#32530) on Linux, combined with the continued absence of native Linux desktop app support, leaves Linux developers in a second-class position despite the platform's popularity for development.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-20

## Today's Highlights

The nightly release train continues with **v0.52.0-nightly.20260720** shipping today. The community's attention remains heavily focused on agent reliability, with the long-running **Post V1.0 Agents** issue (#3132) overwhelmingly leading discussion at 45 comments and 50 upvotes. Two critical security and auth fixes landed today — one resolving a `Premature close` error during OAuth token exchange on headless systems, and another fixing a Windows PowerShell installation issue.

## Releases

No stable releases today. Two nightly builds were published:

- **[v0.52.0-nightly.20260720.gacae7124b](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260720.gacae7124b)** — Automated version bump for nightly release. Full diff from yesterday's nightly available [here](https://github.com/google-gemini/gemini-cli/compare/v0.52.0-nightly.20260719.gacae7124b...v0.52.0-nightly.20260720.gacae7124b).
- **[v0.52.0-nightly.20260719.gacae7124b](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260719.gacae7124b)** — Prior nightly release.

## Hot Issues

1. **[#3132 — [Agents] Post V1.0 Work](https://github.com/google-gemini/gemini-cli/issues/3132)** (45 comments, 50 👍)  
   The most-discussed open issue by far. Proposes a new `SubAgent` class for reusable LLM-driven tool orchestration. Community strongly supports the direction, indicating agent extensibility is the #1 requested feature.

2. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (11 comments, 2 👍)  
   Critical bug: `codebase_investigator` subagent reports `"success"` when it actually hit maximum turn limits. This misreporting undermines trust in agent diagnostics and could mask deeper issues in agent workflows.

3. **[#3716 — Infra: Build and Tag Docker for PR's](https://github.com/google-gemini/gemini-cli/issues/3716)** (13 comments)  
   A long-standing infrastructure issue (since July 2025) blocking seamless sandbox testing of PR branches. Staleness suggests this is a known pain point with no resolution yet.

4. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (7 comments, 8 👍)  
   The generalist agent hangs indefinitely on simple operations like folder creation. Users have resorted to manually instructing the model not to defer to subagents. Significant community interest given the upvote count.

5. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (7 comments)  
   Epic tracking the maturation of behavioral eval tests (76 tests across 6 Gemini models). Signals the team's investment in systematic quality assurance for agent components.

6. **[#25166 — Shell command gets stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (4 comments, 3 👍)  
   Simple CLI commands hang after completion, showing "Awaiting user input." Affects core shell execution reliability — a frequent complaint from developers.

7. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (4 comments, 1 👍)  
   Wayland users cannot use the browser subagent. Platform-specific compatibility remains an ongoing issue.

8. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (6 comments)  
   Anecdotal but telling: custom skills and sub-agents are rarely invoked by the model autonomously, even for highly relevant tasks. Undermines the value of custom tooling.

9. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (3 comments, 1 👍)  
   The model occasionally uses dangerous git operations (`git reset`, `--force`) when safer alternatives exist. User demand for safety guardrails is growing.

10. **[#22232 — Enhance browser_agent resilience: Automatic session takeover and lock recovery](https://github.com/google-gemini/gemini-cli/issues/22232)** (3 comments)  
    The browser agent's "fail-fast" strategy on locked profiles is too restrictive. Users want automatic recovery from orphaned browser sessions.

## Key PR Progress

1. **[#28451 — chore(deps): bump github/codeql-action/init to 4.37.1](https://github.com/google-gemini/gemini-cli/pull/28451)**  
   Security infrastructure update. CodeQL scanning upgraded from v3 to v4, improving static analysis coverage.

2. **[#28456 — chore(deps): bump npm-dependencies group with 75 updates](https://github.com/google-gemini/gemini-cli/pull/28456)**  
   Large-scale dependency refresh touching 75 npm packages. High risk of regressions; community should watch for breakage.

3. **[#28459 — chore(deps): bump @google/genai from 1.30.0 to 2.11.0](https://github.com/google-gemini/gemini-cli/pull/28459)**  
   Major version bump for the core GenAI SDK. Could bring API changes affecting Gemini CLI's model interactions.

4. **[#28463 — chore(deps): bump @agentclientprotocol/sdk from 0.16.1 to 1.2.1](https://github.com/google-gemini/gemini-cli/pull/28463)**  
   Agent Client Protocol SDK jumps to v1.2.1. Signals maturing standards for agent interoperability.

5. **[#28461 — chore(deps-dev): bump typescript from 5.8.3 to 7.0.2](https://github.com/google-gemini/gemini-cli/pull/28461)**  
   TypeScript v7 upgrade. Potential breaking changes but important for type safety and modern language features.

6. **[#28446 — fix(auth): use native fetch for OAuth token exchange to avoid "Premature close"](https://github.com/google-gemini/gemini-cli/pull/28446)** (Priority P1)  
   Fixes a critical login failure on headless VPSes where OAuth token exchange fails with `Premature close`. Uses native fetch instead of problematic HTTP client.

7. **[#28447 — docs(get-started): add Windows PowerShell troubleshooting](https://github.com/google-gemini/gemini-cli/pull/28447)** (Priority P2)  
   Addresses Windows user pain point: `gemini` command not found after global npm install. Adds PowerShell-specific guidance to docs.

8. **[#28386 — fix(vscode): track activation disposables](https://github.com/google-gemini/gemini-cli/pull/28386)** (Priority P2)  
   Fixes #27790: VS Code companion extension was not properly tracking disposables due to JavaScript comma expression bug. Prevents resource leaks.

9. **[#28462 — chore(deps-dev): bump eslint from 9.24.0 to 10.7.0](https://github.com/google-gemini/gemini-cli/pull/28462)**  
   ESLint v10 upgrade. New lint rules may surface additional code quality issues across the codebase.

10. **[#28450 — chore(deps): bump actions-dependencies group](https://github.com/google-gemini/gemini-cli/pull/28450)**  
    Updates to lychee (link checker), compressed-size action, and google-github-actions/run-gemini-cli. Infrastructure reliability improvements.

## Feature Request Trends

- **Agent Extensibility & Subagent Architecture (#3132, #21968, #21432):** The dominant theme. Users want a reusable `SubAgent` class, better autonomous skill invocation, and self-awareness of CLI capabilities.
- **Browser Agent Robustness (#22232, #21983):** Multiple requests for automatic session recovery, Wayland support, and configuration override respect.
- **AST-Aware Code Understanding (#22745, #22746):** Growing interest in using Abstract Syntax Trees for more precise file reads, method bounds detection, and codebase mapping.
- **Safety & Destructive Action Prevention (#22672, #23571):** Users want the agent to avoid `--force` flags, respect resource safety, and clean up temporary scripts.
- **Observability & Debugging (#22598, #21763, #24353):** Demand for better subagent trajectory sharing via chat, richer bug reports including subagent context, and robust component-level evaluations.

## Developer Pain Points

1. **Agent Reliability:** The generalist agent hangs indefinitely (#21409), subagents mask failures as successes (#22323), and shell commands get stuck after completion (#25166). These are core workflow blockers.
2. **Autonomous Skill Usage:** Custom skills and sub-agents are largely ignored by the model (#21968), rendering user investment in tooling ineffective.
3. **Configuration Ignorance:** Browser agent ignores `settings.json` overrides (#22267), and subagents run without permission on upgrade (#22093). Users feel a loss of control.
4. **Platform Compatibility:** Wayland browser agent failures (#21983), Windows installation issues (#28447), and terminal resize flicker (#21924) create friction across environments.
5. **Memory System Quality:** Auto Memory retries low-signal sessions indefinitely (#26522), silently skips invalid patches (#26523), and logs sensitive content before redaction (#26525).
6. **Tool Limit Hard Crash:** Encountering a 400 error when more than ~128 tools are available (#24246) — a hard scalability ceiling that affects advanced users.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-20

## Today's Highlights

A significant regression in plan-mode (#4188) was reported today, where shell commands are now blocked—breaking workflows that previously used `gh` CLI to enrich plans. Additionally, a critical bug (#4185) emerged where `--add-dir` flags cause Claude sub-agent dispatches to fail due to cache control block limits. On the UI front, three usability issues around `/btw` (image pasting, session creation, and popup workflow) signal growing community adoption of the quick-ask feature.

## Releases

No new releases in the last 24 hours. The latest known version remains **GitHub Copilot CLI 1.0.72-0**.

## Hot Issues (10 Noteworthy)

1. **[#4188 — Regression on plan-mode](https://github.com/github/copilot-cli/issues/4188)** (NEW)
   Plan mode now blocks shell commands that were previously allowed (e.g., `gh` CLI for issue creation). Community considers this a regression as it breaks agent-enrichment workflows. *0 comments, just filed today.*

2. **[#4185 — `--add-dir` causes Claude sub-agent dispatch to fail](https://github.com/github/copilot-cli/issues/4185)** (NEW)
   Launching with `--add-dir` triggers a 400 error on Anthropic models: “A maximum of 4 blocks with cache_control… Found 5.” Blocks all sub-agent dispatches on Claude models. *Critical for users relying on directory context injection.*

3. **[#4024 — Voice mode: all bundled ASR models fail silently](https://github.com/github/copilot-cli/issues/4024)**
   Multi-modal speech routing bug (`nemotron_speech` RNNT) returns empty transcriptions for all three ASR models. Microphone capture confirmed working; model routing is the likely culprit. *13 comments, no upvotes—suggests voice is niche but broken for early adopters.*

4. **[#1857 — Allow users to cancel or remove enqueued messages](https://github.com/github/copilot-cli/issues/1857)**
   Highly requested (👍24): once a message is enqueued via `Ctrl+Q`/`Ctrl+Enter`, there is no way to cancel it. Users must wait for the queue to drain. *8 comments; oldest hot issue still open.*

5. **[#4179 — Click to edit enqueued entries in TUI](https://github.com/github/copilot-cli/issues/4179)** (NEW)
   Mouse clicks on enqueued messages don’t allow editing. TUI supports clicks for other elements; this feels like an omission. *Related to #1857.*

6. **[#4183 — Auto-compaction doesn't prevent CAPI 5 MB body limit failure](https://github.com/github/copilot-cli/issues/4183)** (NEW)
   Long tool-heavy sessions hit a 5 MB CAPI request body limit even when context-token capacity is fine. Auto-compaction ignores this independent limit. *Affects power users with complex sessions.*

7. **[#4180 — Interactive TUI ignores keyboard input in PTY environments](https://github.com/github/copilot-cli/issues/4180)** (NEW)
   When run inside programmatic PTYs (tmux send-keys, `pty.fork()`), the TUI ignores all keystrokes except `Ctrl+C`. Breaks automation/orchestration tooling. *Blocks CI/CD integration.*

8. **[#4173 — Child writing tasks retain plan-mode write gates after approved exit](https://github.com/github/copilot-cli/issues/4173)**
   Background tasks launched after a plan-mode exit can inherit stale write gates, falsely blocking operations and consuming retry budgets. *Stalls fleet execution; impacts enterprise users.*

9. **[#4172 — Exiting plan mode not reliable with GPT-5.6 models](https://github.com/github/copilot-cli/issues/4172)**
   New GPT-5.6 models leave users in a dead end: “Plan saved” but no follow-up prompt. Interaction gets stuck. *Reported 2 days ago; high severity for early GPT-5.6 adopters.*

10. **[#4174 — ACP server lacks token/context usage in protocol](https://github.com/github/copilot-cli/issues/4174)** (NEW)
    The `copilot --acp` mode exposes no token usage, context consumption, or cost metrics in any protocol message. *Missing observability for production deployments.*

## Key PR Progress

Only **1 PR** was updated in the last 24 hours, and it is largely administrative:

- **[#1 — Create ownership.yaml](https://github.com/github/copilot-cli/pull/1)** (CLOSED)
  Repository metadata file. Authored by johanrosenkilde in 2023, only updated today. *No substantive code changes.*

*No active feature or bugfix PRs were updated in the last 24 hours. This may indicate a lull in development or that teams are focused on triaging the spike of new issues.*

## Feature Request Trends

The most-requested feature directions emerging from this week’s issues include:

1. **Queue Management** — Ability to cancel, edit, or reorder enqueued messages (👍24 across #1857, #4179). Users want finer control over agent interaction flow.

2. **Observability & Metrics** — Token/context usage exposure (#4174), skill-level spans in traces (#3725), and model attribution in background agents (#4178). Enterprise users need cost tracking and debugging.

3. **Session Ergonomics** — Quick creation of sessions from `/btw` popups (#4182), image pasting in `/btw` (#4181), and better visual cues for enqueued items. The `/btw` workflow is growing but has rough edges.

4. **Multi-Modal / Voice** — Despite the ASR bug (#4024), voice mode is an active area. Users want it to work reliably across model backends.

5. **Non-Interactive & Automation** — ACP server improvements (#4174), PTY compatibility (#4180), and CI-friendly compaction signals growing demand for headless operation.

## Developer Pain Points

Four recurring frustrations stand out:

1. **Plan-Mode Instability** — Regression in shell command blocking (#4188), GPT-5.6 exit failures (#4172), and stale write gates (#4173) make plan-mode unreliable for production use. This is the most critical pain point this week.

2. **Context & Cache Limits** — The 5 MB CAPI body limit (#4183) and Claude’s 4-block cache limit (#4185) are hitting users in long or context-rich sessions. Workarounds are unclear.

3. **Windows Performance** — Desktop app takes 1–2 minutes to start on Windows (#4176), launching multiple CLI processes. Slow onboarding for Windows developers.

4. **PTY / Automation Incompatibility** — The TUI’s refusal to accept keyboard input in programmatic PTYs (#4180) blocks CI/CD, tmux users, and orchestration frameworks. A significant barrier to headless adoption.

---

*Digest generated 2026-07-20 from 21 issues and 1 PR in github/copilot-cli.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-07-20

## Today's Highlights
This week's digest is dominated by critical session-management fixes and new hooks infrastructure. **Nas01010101** submitted three PRs tackling long-standing undoing/forking bugs and session-resume roulette with frozen prompts. Meanwhile, **yanchenko** introduced a mid-turn streaming hook (`MessageDisplay`) that finally lets external consumers react to assistant replies in real time. On the API-side, **nitishagar** surfaced a double-encoded tool-call argument bug that broke Pydantic validation, and a separate permission-rules order mismatch issue (#2508) continues to gather concern.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **#2508 – Permission rules: `deny` overrides `allow` regardless of order**  
   *Author: Julzilla | 👍: 0 | Comments: 1*  
   The documented "first matching rule takes effect" behavior is broken—`deny` always wins even when `allow` appears first. This is a safety-critical regression for any user relying on granular permission files.  
   [GitHub Issue #2508](https://github.com/MoonshotAI/kimi-cli/issues/2508)

2. **#2517 – `/undo` and `/fork` truncate `context.jsonl` at the wrong turn in compacted/steered sessions**  
   *Author: Nas01010101 | 👍: 0 | Comments: 0*  
   Provider-independent bug affecting local session file handling. Reproduced on `main` commit 4a550ef. Could lead to corrupted session histories after undo or fork operations.  
   [GitHub Issue #2517](https://github.com/MoonshotAI/kimi-cli/issues/2517)

3. **#2511 – `feat(hooks)`: mid-turn streaming hook (`MessageDisplay`)**
   *Author: yanchenko | 👍: 0 | Comments: 0*  
   The Hooks system Beta lacks a way to observe assistant reply text while it streams. `Stop` fires only at turn-end, so live TTS, incremental logging, or progress UI are impossible today.  
   [GitHub Issue #2511](https://github.com/MoonshotAI/kimi-cli/issues/2511)

4. **#1282 – Feature Request: Remote Control – Continue local sessions from any device**  
   *Author: CatKang | 👍: 13 | Comments: 5*  
   High-community-interest request for remote session resumption from phones/tablets/browsers. Seamless workflow continuity when away from desk. Most-upvoted open issue.  
   [GitHub Issue #1282](https://github.com/MoonshotAI/kimi-cli/issues/1282)

5. **#2413 – Every restart resends previously uploaded files**  
   *Author: (not listed in digest data)*  
   `kimi web` re-sends all previously uploaded files (including images) after any server restart, polluting the session history. Now being fixed in PR #2518.  
   [GitHub Issue #2413](https://github.com/MoonshotAI/kimi-cli/issues/2413)

6. **#2420 – Frozen system prompt on session resume**  
   *Author: (not listed in digest data)*  
   Skills added to `~/.kimi/skills/` and `AGENTS.md` edits never appear in resumed sessions because the system prompt is frozen at creation time.  
   [GitHub Issue #2420](https://github.com/MoonshotAI/kimi-cli/issues/2420)

7. **#2049 – History mismatch after forks/undos**  
   *Author: (not listed in digest data)*  
   Likely root cause being addressed by PR #2520. Session history becomes inconsistent after fork/undo in certain workflows.  
   [GitHub Issue #2049](https://github.com/MoonshotAI/kimi-cli/issues/2049)

8. **#1974 – Wire-only slash commands shift undo cut**  
   *Author: (not listed in digest data)*  
   Slash commands that exist only in the wire representation cause incorrect truncation points when undoing. Regression test included in PR #2520.  
   [GitHub Issue #1974](https://github.com/MoonshotAI/kimi-cli/issues/1974)

9. **#2386 – Wire turn vs. context turn mapping**  
   *Author: (not listed in digest data)*  
   Related open PR that maps wire turns to context turns for slash-command sessions. Part of the larger session-model alignment effort.  
   [GitHub Issue #2386](https://github.com/MoonshotAI/kimi-cli/issues/2386)

10. **Double-encoded tool-call arguments** (referenced in PR #2513 context, issue not linked)  
    The Moonshot API can return `function.arguments` with nested JSON strings inside objects/arrays. After `json.loads`, values remain strings, failing Pydantic validation.  
    *(No dedicated GitHub issue linked in digest data)*

## Key PR Progress
1. **#2520 – `fix(session)`: align fork/undo context truncation to wire turns**  
   *Author: Nas01010101 | Status: OPEN*  
   Resolves #2517, #1974, and likely #2049. Maps context turns to wire turns for slash-command sessions. Related to PR #2386.  
   [GitHub PR #2520](https://github.com/MoonshotAI/kimi-cli/pull/2520)

2. **#2515 – `perf(kosong)`: buffer stream merges, avoid deep-copying every delta**  
   *Author: parthgupta9999 | Status: OPEN*  
   Fixes quadratic string concatenation (`str +=`) and expensive `model_copy(deep=True)` calls on long streaming responses.  
   [GitHub PR #2515](https://github.com/MoonshotAI/kimi-cli/pull/2515)

3. **#2518 – `fix(web)`: persist uploads `.sent` marker so restarts do not re-send files**  
   *Author: Nas01010101 | Status: OPEN*  
   Resolves #2413. Adds persistence so `kimi web` does not re-send previously uploaded files after server restart.  
   [GitHub PR #2518](https://github.com/MoonshotAI/kimi-cli/pull/2518)

4. **#2519 – `fix(app)`: refresh stale frozen system prompt on session resume**  
   *Author: Nas01010101 | Status: OPEN*  
   Resolves #2420. Skills and `AGENTS.md` edits now appear in resumed sessions instead of being locked to the prompt frozen at creation.  
   [GitHub PR #2519](https://github.com/MoonshotAI/kimi-cli/pull/2519)

5. **#2513 – `fix(kosong)`: recursively decode double-encoded tool-call arguments**  
   *Author: nitishagar | Status: OPEN*  
   Adds `decode_tool_arguments` helper to handle nested double-encoded JSON from the Moonshot API. Prevents Pydantic validation failures on tool calls.  
   [GitHub PR #2513](https://github.com/MoonshotAI/kimi-cli/pull/2513)

6. **#2514 – `fix(skill)`: ignore stray markdown in plugins container during skill discovery**  
   *Author: nitishagar | Status: OPEN*  
   Prevents flat `.md` files in the plugins directory from being misinterpreted as skills, matching the documented directory structure.  
   [GitHub PR #2514](https://github.com/MoonshotAI/kimi-cli/pull/2514)

7. **#2512 – `feat(hooks)`: add MessageDisplay hook for mid-turn streaming**  
   *Author: yanchenko | Status: OPEN*  
   Closes #2511. Fire-and-forget hook that fires repeatedly during assistant reply streaming. Modeled on Qwen Code feature.  
   [GitHub PR #2512](https://github.com/MoonshotAI/kimi-cli/pull/2512)

8. **#2516 – `Create kimi-cli` (spam)**  
   *Author: owndaboubi1993-cyber | Status: CLOSED*  
   Low-quality PR titled "skills n plugins", likely spam or placeholder content. Closed.  
   [GitHub PR #2516](https://github.com/MoonshotAI/kimi-cli/pull/2516)

9. **#2386 – Wire turn to context turn mapping** (referenced in #2520)  
   *Status: OPEN*  
   Addresses the mapping of wire turns to context turns for slash-command sessions, foundational to fixing session truncation.  
   *(No direct link provided in digest data)*

10. **#2520 (already listed above)**  
    *Note: PR #2520 is the most impactful PR this week, combining bug fixes for multiple session-history issues.*

## Feature Request Trends
- **Remote session continuity** (#1282, 👍13): The "Remote Control" feature to resume local sessions from mobile devices is the most-upvoted open feature request, indicating strong demand for cross-device workflow persistence.
- **Observable mid-turn streaming** (#2511): The Hooks system is growing—developers want to integrate with live TTS, incremental logging, and progress indicators.
- **Session model hardening**: Multiple issues and PRs target session history accuracy, system prompt freshness, and undo/fork reliability. This is clearly an area of active community frustration and development investment.

## Developer Pain Points
1. **Permission rule ordering broken** (#2508): `deny` always wins regardless of rule order, contradicting documented "first match" semantics. Critical for security-conscious users.
2. **Session truncation on undo/fork** (#2517, #1974, #2049): Undo and fork operations corrupt `context.jsonl` at the wrong turn, especially in compacted or steered sessions. Affects any user who uses these features for workflow iteration.
3. **Stale frozen prompts on resume** (#2420): Skills and `AGENTS.md` updates are invisible in resumed sessions, breaking the "edit-and-retry" workflow.
4. **Web file re-upload on restart** (#2413): Server restarts re-send all previously uploaded files, causing session pollution and extra API usage.
5. **Tool-call double encoding** (#2513): Moonshot API double-encodes nested JSON in tool arguments, causing Pydantic validation failures—especially blocking for developers building tool-equipped agents.
6. **Plugins vs. skills confusion** (#2514): Stray markdown files in the plugins directory trigger false-positive skill discovery, violating documented directory structure.

---

*Digest generated from GitHub data for `github.com/MoonshotAI/kimi-cli` (2026-07-19 to 2026-07-20 UTC)*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-20

## Today's Highlights

Today's activity is dominated by a major push to stabilize the new **OpenCode 2.0 architecture**, with multiple issues from maintainer `kitlangton` detailing event-stream scaling and memory management problems. A long-standing UX pain point — **manual model discovery for local providers** — remains the top-voted open issue (182 👍), while the community also flagged a security vulnerability in the console's OAuth flow. The PR queue is busy with cleanup and fixes, including a critical SQLite auto-recovery patch and a Windows git diff fix.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#6231 — Auto-discover models from OpenAI-compatible provider endpoints](https://github.com/anomalyco/opencode/issues/6231)**
   - **Why it matters:** Users with local providers (LM Studio, Ollama) must manually maintain model lists in `opencode.json`, which breaks when models change. The overwhelming community consensus (182 👍, 25 comments) demands API-driven auto-discovery.
   - **Community reaction:** Highly active; users sharing workarounds and provider-specific endpoint variations.

2. **[#19130 — Windows ARM64 native: OpenTUI fails with bun:ffi dlopen TinyCC error](https://github.com/anomalyco/opencode/issues/19130)**
   - **Why it matters:** Blocks TUI usage entirely on Windows ARM64 — a growing platform for developers using native ARM hardware. Non-interactive commands work, but the TUI is dead-on-arrival.
   - **Community reaction:** 8 👍; users on Snapdragon X and Surface Pro 11 reporting same crash.

3. **[#35265 — ResourceExhausted: Worker local total request limit reached](https://github.com/anomalyco/opencode/issues/35265)**
   - **Why it matters:** Hitting hard rate limits on OpenAI-compatible backends disrupts long sessions. Community has tried prior fixes (issues #34613, #34657) but this is a fresh instance without resolution.
   - **Community reaction:** 9 comments; user provided detailed logs but no resolution yet.

4. **[#33356 — Unbounded growth of event table: opencode.db reaches 13GB+](https://github.com/anomalyco/opencode/issues/33356)**
   - **Why it matters:** A serious production concern — the event-sourcing store never prunes `message.updated.1` snapshots, filling disk volumes. Affects long-running instances severely.
   - **Community reaction:** Report from a team running two instances; 1 👍 but high urgency for anyone using OpenCode heavily.

5. **[#9955 — TUI has too much padding and unnecessary large height elements](https://github.com/anomalyco/opencode/issues/9955)**
   - **Why it matters:** Vertical space is wasted in the TUI on desktop/laptop screens. Users want a denser layout similar to other CLI agents.
   - **Community reaction:** 17 👍; controversial — some like the spacious design, but many agree it needs an optional compact mode.

6. **[#7801 — Plan Mode + Question tool can auto-switch to Build mode](https://github.com/anomalyco/opencode/issues/7801)**
   - **Why it matters:** When the AI asks "Should I proceed?" and the user confirms, it should automatically transition to execution. Current behavior wastes a turn.
   - **Community reaction:** 26 👍; users strongly agree this is a natural UX flow that would save tokens.

7. **[#37789 — Plan mode re-asks confirmation after switching to build mode](https://github.com/anomalyco/opencode/issues/37789)**
   - **Why it matters:** Related to #7801 — users report the AI asks the same confirmation twice, wasting tokens on redundant queries.
   - **Community reaction:** New issue (2 comments), but taps into a broader frustration with mode transitions.

8. **[#37807 — Open redirect vulnerability in console /auth/authorize](https://github.com/anomalyco/opencode/issues/37807)**
   - **Why it matters:** CWE-601 open redirect via the `continue` parameter. An attacker can phish users after login by redirecting to an attacker-controlled origin.
   - **Community reaction:** Reported responsibly by `sebastiondev`; closed quickly — indicating the team treats security seriously.

9. **[#37803 — TUI screen goes completely black when agent starts working](https://github.com/anomalyco/opencode/issues/37803)**
   - **Why it matters:** Render loop silently stalls. The process stays alive but the display is unusable until switching terminal tabs.
   - **Community reaction:** New issue; linked to PR #37805 which bumps `@opentui/core` to fix the render loop race condition.

10. **[#36826 — "Failed to send prompt. Unexpected server error" with DeepSeek V4 Flash](https://github.com/anomalyco/opencode/issues/36826)**
    - **Why it matters:** A specific model is completely broken on a popular provider, blocking users who paid for that model tier.
    - **Community reaction:** 5 comments; user on OpenCode 1.17.20; no fix yet.

## Key PR Progress

1. **[#37830 — fix(app): register open project shortcut in new layout](https://github.com/anomalyco/opencode/pull/37830)**
   - **What it does:** Restores `Cmd+O` to open the folder picker in the new layout. The command was registered only in the old layout.
   - **Why it matters:** A minor regression that breaks a core navigation shortcut.

2. **[#37828 — refactor: extract shared util package](https://github.com/anomalyco/opencode/pull/37828)**
   - **What it does:** Creates `@opencode-ai/util` and moves shared host/runtime infrastructure out of Core. Rewrites CLI, Server, TUI, etc. to import directly.
   - **Why it matters:** Major architectural cleanup that reduces cross-module dependencies and makes the codebase more maintainable.

3. **[#35654 — fix(git): add --ignore-cr-at-eol to git diff commands](https://github.com/anomalyco/opencode/pull/35654)**
   - **What it does:** Fixes the Review window showing entire files as rewritten on Windows due to CRLF differences.
   - **Why it matters:** Closes two issues (#27276, #30357); a long-standing Windows usability bug.

4. **[#37822 — fix(core): auto-recover corrupted sqlite database on startup](https://github.com/anomalyco/opencode/pull/37822)**
   - **What it does:** Automatically runs recovery when SQLite reports `database disk image is malformed`, preventing crash-on-startup.
   - **Why it matters:** Prevents total data loss; critical for users who experience sudden shutdowns.

5. **[#37827 — fix(app): dismiss session sidebar on selection for narrow displays](https://github.com/anomalyco/opencode/pull/37827)**
   - **What it does:** Auto-dismisses the session sidebar on mobile/narrow screens after selecting a session.
   - **Why it matters:** Improves responsive UX; references issue #37746 about mobile usability.

6. **[#33037 — fix(acp): list sessions across projects](https://github.com/anomalyco/opencode/pull/33037)**
   - **What it does:** Makes `session/list` treat `cwd` as optional, returning sessions across all projects when omitted.
   - **Why it matters:** Closes three issues; a behavioral fix that matches client expectations.

7. **[#32998 — fix(session): cap OpenAI Responses tool count to avoid 500 server_error loop](https://github.com/anomalyco/opencode/pull/32998)**
   - **What it does:** Limits the number of tools sent in a single OpenAI Responses request to prevent backend rejection.
   - **Why it matters:** Users with many MCP servers hit a hard error loop; this is a pragmatic workaround.

8. **[#32991 — fix: Don't git snapshot huge untracked directories](https://github.com/anomalyco/opencode/pull/32991)**
   - **What it does:** Skips git snapshots of large untracked directories (e.g., `node_modules`), eliminating pre-response hangs.
   - **Why it matters:** Dramatically improves first-response latency for projects with large directories.

9. **[#37805 — chore: bump @opentui/core to fix render loop stall](https://github.com/anomalyco/opencode/pull/37805)**
   - **What it does:** Bumps `@opentui/core` to a fix commit that resolves the race condition in the render loop's `finally` block.
   - **Why it matters:** Directly addresses the "black screen" TUI bug (#37803).

10. **[#33019 — feat(tui): add inline skill picker](https://github.com/anomalyco/opencode/pull/33019)**
    - **What it does:** Adds a `$` skill picker in the TUI — typing `$` opens an inline selector for skills.
    - **Why it matters:** A UX improvement for power users who frequently switch skills mid-session.

## Feature Request Trends

- **Auto-discovery of provider models:** Issue #6231 dominates with 182 👍. Users want the tool to query OpenAI-compatible endpoints for the model list rather than manual configuration.
- **Suspend/Resume for agents:** Issue #27511 (5 👍) requests the ability to pause a running agent and subagent, then resume — useful for long-running tasks or debugging.
- **Subagent session continuity:** Issue #36654 asks for session IDs and resume capability for subagents, so multi-turn conversations with spawned agents don't lose context.
- **Plan-to-Build auto-transition:** Issues #7801 and #37789 both describe the same pain: the AI asks for confirmation but stays in Plan mode, wasting a turn. The community wants seamless mode switching.
- **Ecosystem integrations:** Issues #37656 (Heym) and #37677 (`opencode-session-id-plugin`) show demand for better plugin/extensibility documentation and community integration listings.

## Developer Pain Points

1. **Memory and storage leaks:** The unbounded event table growth (#33356) reaching 13GB+ and the `MaxListenersExceededWarning` (#22422) indicate systemic issues with event-sourcing store management.

2. **Windows-specific rendering bugs:** ARM64 TUI crash (#19130) and CRLF git diffs (#35654) continue to plague Windows users, especially with the shift to ARM hardware.

3. **Provider API fragility:** DeepSeek V4 Flash (#36826), Kimi K3 (#37815), and the worker rate limiter (#35265) show that provider compatibility is a recurring headache — models appear in selection but fail at runtime.

4. **2.0 event-stream scaling:** Kit Langton's suite of issues (#36441, #36443, #36445, #36285) document serious architectural problems in V2: process-global event streams that scale poorly with multiple TUIs, and reconnect storms that spike server resources.

5. **Clipboard in web terminals:** Issue #26459 (5 comments) — clipboard copy fails in code-server, Codespaces, and Gitpod. A small UX issue that breaks a commonly used workflow for remote developers.

6. **Subscription/billing confusion:** Issues #31403 and #37790 report the "Insufficient balance" error persisting after successful payment. This erodes trust in the paid tier and needs immediate attention.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-20

## Today's Highlights
A busy day with 32 issues updated and 9 PRs merged, reflecting a maturing project with intense focus on reliability. Key themes include **provider interoperability fixes** (OpenCode Go, Upstage Solar LLMs, Copilot Enterprise compaction), **crash/error handling robustness** (undefined `usage` fields, orphan tool results, session corruption), and **quality-of-life enhancements** (configurable retries, scroll navigation toggles, async compaction improvements). Notably, a new **Upstage (Solar LLMs) provider** was contributed and merged as a built-in option.

## Releases
No new releases were published in the last 24 hours. The project remains at the previously tagged version (last tagged release prior to 0.80.10).

## Hot Issues

1. **[#5023 Terminal scrolls to beginning without reason](https://github.com/earendil-works/pi/issues/5023)** — Closed. Random terminal jump-to-top behavior reported by multiple users. Community engaged (9 comments) but root cause not publicly resolved; likely tied to TUI rendering or buffer flush logic.

2. **[#6210 `/scoped-models` cannot select model ids containing brackets](https://github.com/earendil-works/pi/issues/6210)** — Open. A parsing bug where bracket characters in custom model IDs (e.g., `custom/bracketed-model[1m]`) break model selection. Trivial to reproduce, has sat unresolved for 19 days.

3. **[#6792 High CPU usage when editing 500+ line files](https://github.com/earendil-works/pi/issues/6792)** — Closed (with attached CPU profile). 100% CPU on large file operations. Community provided a flamegraph; indicates a performance regression in the editor integration layer.

4. **[#1871 Misleading 'No API key found' during parallel startup](https://github.com/earendil-works/pi/issues/1871)** — Closed. Lock contention on auth files during concurrent pi-subagents startup surfaces as a fake API key error. Affects parallel/multi-agent workflows.

5. **[#6774 Ctrl+G external editor slow with crowded `os.tmpdir()`](https://github.com/earendil-works/pi/issues/6774)** — Closed. Suggests using `mkdtemp` subdirectory instead of dumping straight into tmpdir. A common pattern for avoiding tmpdir congestion — low-risk UX win.

6. **[#6675 `pi update --self` fails on transient network errors](https://github.com/earendil-works/pi/issues/6675)** — Open. Single-request update mechanism is fragile; no retry logic, no fallback. Community requesting exponential backoff.

7. **[#6825 `--system-prompt` flag not taking effect](https://github.com/earendil-works/pi/issues/6825)** — Closed (very recent). A critical regression — system prompt overrides silently ignored. Would affect any custom-prompt workflow; appears to have been promptly fixed.

8. **[#6832 Orphan toolResult survives compaction → unrecoverable 400](https://github.com/earendil-works/pi/issues/6832)** — Closed, but marked as regression of #4570/#1764. An old bug re-surfaced on 0.80.10 where long sessions become permanently broken. High impact; community attached a `👍` indicating shared frustration.

9. **[#6822 Promptless sessions restore default model over persisted `model_change`](https://github.com/earendil-works/pi/issues/6822)** — Closed. Silent model overwrite when reopening sessions with only model changes but no messages. Breaks model continuity for CLI-driven session management.

10. **[#6819 `assistant.usage` undefined crashes session permanently](https://github.com/earendil-works/pi/issues/6819)** — Closed. Multiple places assume `usage` is always present — DeepSeek V4 and other providers omit it in streaming responses, causing unrecoverable crashes. Simple null-guard fix, but underscores wider testing gaps with non-OpenAI providers.

## Key PR Progress

1. **[#6828 fix(ai): support OpenCode Go Responses models](https://github.com/earendil-works/pi/pull/6828)** — Merged. Registers OpenAI Responses API implementation for OpenCode Go (Grok 4.5). Explicitly declares API union for type safety. Key for multi-provider parity.

2. **[#6840 feat(ai): add shared `contentText` utility](https://github.com/earendil-works/pi/pull/6840)** — Merged. Small code-share improvement — creates a central `contentText` helper, reducing duplication across providers.

3. **[#6834 fix(ai,agent,coding-agent): share UUIDv7 and use for Codex](https://github.com/earendil-works/pi/pull/6834)** — Merged. Moves UUIDv7 generation into shared `pi-ai` package and uses it as default for Codex requests without session IDs. Improves request traceability.

4. **[#6837 fix(ai): align GPT-5.6 Codex context with official client](https://github.com/earendil-works/pi/pull/6837)** — Merged. Corrects GPT-5.6 context window from 372K to 272K to match official client specs. Keeps pricing tiers for overridden models.

5. **[#6775 retry on compaction/branch summarization retryable failures](https://github.com/earendil-works/pi/pull/6775)** — Open. Adds retry logic for compaction failures (fixes #6647). Author asks about UI indication for retries; still under review.

6. **[#836 feat(coding-agent): add ACP mode for editor integration](https://github.com/earendil-works/pi/pull/836)** — Merged (old PR finally merged). Adds Agent Client Protocol support via `--mode acp`, enabling integration with Zed and JetBrains IDEs. Significant milestone for editor-agnostic usage.

7. **[#6824 feat(ai): add Upstage (Solar LLMs) as built-in provider](https://github.com/earendil-works/pi/pull/6824)** — Merged. Four Solar models added (mini, pro2, two sizes). Competitive pricing ($0.15/$0.15 per 1K tokens) with reasoning support. Good for budget-conscious users.

8. **[#6818 fix: guard against undefined `assistant.usage`](https://github.com/earendil-works/pi/pull/6818)** — Merged. Adds null guards to prevent session-bricking crashes when providers omit usage data. Addresses a high-painpoint bug.

9. **[#6833 Option to hide scroll navigation help](https://github.com/earendil-works/pi/pull/6833)** — Merged? (linked to issue). Resolves the "scroll navigation help box covers content" annoyance. Minor UX win.

10. **[#6836 Observable retry lifecycle for agent-core consumers](https://github.com/earendil-works/pi/pull/6836)** — Merged. Exposes `auto_retry_start`, `auto_retry_end`, and `willRetry` to extension consumers. Enables custom retry UI/logging.

## Feature Request Trends

1. **Provider & Model Diversity** — Strong demand for more built-in providers (Upstage Solar merged; OpenCode Go support merged). Users want easier local model connectivity (LAN broadcast discovery) and broader model catalog alignment.

2. **Extension/Plugin Hooks** — Multiple requests for deeper extension hooks: access to raw response streams (#3605), batch tool call judgement (#6816), forward `willRetry` to extension events (#6827). The ecosystem is maturing.

3. **Recovery & Retry UX** — `/retry` command (#6810), retry lifecycle observability (#6836), compaction retry logic (#6775). Users want graceful degradation in poor network conditions.

4. **Editor & Terminal Ergonomics** — Markdown table theming (#6826), scroll navigation toggle (#6833), message rendering API (#6821). Ongoing polish of the TUI experience.

5. **Remote Execution** — SSH/remote container support (#5341) continues to be requested, indicating users want Pi to operate on remote development environments.

## Developer Pain Points

- **Session corruption & unrecoverable errors** — Undefined `usage` (#6819), orphan tool results after compaction (#6832), queued messages dropped after auto-compaction (#6820). Sessions becoming "bricked" is the single highest-impact recurring issue.
- **Silent configuration failures** — `--system-prompt` not applied (#6825), `model_change` overwritten on session restore (#6822), misleading auth errors during lock contention (#1871). Configuration bugs erode trust.
- **Windows path handling** — `find` tool broken with path separators (#6817). Platform parity remains an afterthought.
- **Transient network fragility** — `update --self` fails on single failure (#6675), manual retries not possible (#6810). Users on unreliable connections face repeated friction.
- **Fragmentary provider testing** — Multiple crashes from non-OpenAI providers (DeepSeek, Upstage) suggest test coverage is skewed toward the default provider. Community is effectively doing integration QA.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**Date: 2026-07-20**

---

## Today's Highlights

Two significant releases landed today: a minor **v0.20.0** feature release and a patch preview **v0.20.1-preview.7215** with an autofix feature. The community is actively discussing subagent-related bugs, with two high-priority issues (#7156 and #7254) pointing to resource contention and model mutation during multi-agent sessions. Additionally, MCP server connectivity issues (#7147) and token tracking gaps (#7236) for local inference remain pain points.

---

## Releases

### [v0.20.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.20.0)
- **Features:** Added bounded daemon log rotation ([#6969](https://github.com/QwenLM/qwen-code/pull/6969))
- **Breaking Changes:** None reported
- **Status:** Stable release

### [v0.20.1-preview.7215](https://github.com/QwenLM/qwen-code/releases/tag/v0.20.1-preview.7215)
- **Features:** Label-driven takeover and release for autofix ([#7165](https://github.com/QwenLM/qwen-code/pull/7165))
- **Fixes:** Fixed forced-dispatch green no-op behavior
- **Status:** Preview release

---

## Hot Issues (Top 10 by Activity)

1. **[#4748](https://github.com/QwenLM/qwen-code/issues/4748) — Optimize daemon cold start and fast-path latency** (CLOSED)
   *Why it matters:* The original daemon cold-start benchmark showed a 2.5s gap vs 0.7s CLI initialization. After substantial optimization, the community considers this resolved.
   *Author:* @doudouOUC | Comments: 11

2. **[#7156](https://github.com/QwenLM/qwen-code/issues/7156) — Subagent mutates main session model => context overflow** (OPEN, P1)
   *Why it matters:* Critical bug where subagent execution overwrites the user's chosen model on the main session, causing 400 errors. Circumvents the previous fix in #7119.
   *Author:* @Aleks-0 | Comments: 11

3. **[#4801](https://github.com/QwenLM/qwen-code/issues/4801) — Add dedicated `web_search` tool** (CLOSED)
   *Why it matters:* Qwen Code was the only major code agent CLI without a web search tool. The feature is now implemented via PR #7215.
   *Author:* @ZijianZhang989 | Comments: 5

4. **[#7147](https://github.com/QwenLM/qwen-code/issues/7147) — MCP server never successfully gets tool/resource listing** (OPEN, P2)
   *Why it matters:* Affects all MCP integrations with Fastmail and potentially other providers. Authentication succeeds but tool listing times out.
   *Author:* @imrehg | Comments: 5

5. **[#6569](https://github.com/QwenLM/qwen-code/issues/6569) — Improve subagent observability** (OPEN, P2)
   *Why it matters:* Users need real-time visibility into subagent execution, full traces after completion, and ability to intervene — currently subagents are a black box.
   *Author:* @azurecgx | Comments: 3

6. **[#7198](https://github.com/QwenLM/qwen-code/issues/7198) — Add `qwen3.8-max-preview` to built-in model list** (CLOSED)
   *Why it matters:* New model from Alibaba Cloud Model Studio Token Plan. Community member @xxlaura confirmed it works well with custom config, requests built-in support.
   *Author:* @xxlaura | Comments: 3

7. **[#6237](https://github.com/QwenLM/qwen-code/issues/6237) — Plan Mode content leakage in subsequent responses** (OPEN, P2)
   *Why it matters:* The plan content passed to `exit_plan_mode` leaks into later assistant responses instead of being confined to planning.
   *Author:* @DamienJScott | Comments: 3

8. **[#6996](https://github.com/QwenLM/qwen-code/issues/6996) — Custom OpenAI provider fails with generic connection error** (CLOSED, P2)
   *Why it matters:* Root cause (e.g., TLS, proxy) is discarded before logging, making debugging impossible. Fixed via improved error propagation.
   *Author:* @jzupnick | Comments: 3

9. **[#7139](https://github.com/QwenLM/qwen-code/issues/7139) — Windows Docker sandbox passes invalid workspace cwd** (OPEN, P1)
   *Why it matters:* Blocks all shell tool calls on Windows 11 when using Docker sandbox with `qwen serve`. Community asking for platform parity.
   *Author:* @matt3ho | Comments: 2

10. **[#7254](https://github.com/QwenLM/qwen-code/issues/7254) — Main agent keeps thinking while waiting for subagent** (OPEN, P2)
    *Why it matters:* Resource contention with `maxConcurrency: 1` — main agent occupies the slot while subagent can't work, causing deadlock-like behavior.
    *Author:* @fantasyz | Comments: 1

---

## Key PR Progress (Top 10 by Impact)

1. **[#7215](https://github.com/QwenLM/qwen-code/pull/7215) — Add opt-in built-in `web_search` (DashScope Responses API)** (OPEN)
   *Description:* Brings back a built-in web search tool using DashScope's server-side search. Opt-in, off by default — no MCP server or extra API key needed.
   *Author:* @tanzhenxin

2. **[#7221](https://github.com/QwenLM/qwen-code/pull/7221) — Worktree-isolated sessions for parallel tasks** (CLOSED)
   *Description:* Enables creating sessions in isolated git worktrees from Web Shell, allowing parallel tasks without polluting the main working directory.
   *Author:* @wenshao

3. **[#7239](https://github.com/QwenLM/qwen-code/pull/7239) — Estimate thinking tokens when `reasoning_tokens` is missing** (OPEN)
   *Description:* Fallback for OpenAI-compatible providers that omit reasoning tokens from usage response — critical for accurate token accounting.
   *Author:* @yiliang114

4. **[#7257](https://github.com/QwenLM/qwen-code/pull/7257) — Abort SSE request on iterator exit to release daemon subscriber** (OPEN)
   *Description:* Fixes #7238 — prevents SSE subscriber leaks that cause daemon-wide outage (HTTP 429) on normal iterator exit.
   *Author:* @chinesepowered

5. **[#7237](https://github.com/QwenLM/qwen-code/pull/7237) — Fence concurrent ACP session writers** (OPEN)
   *Description:* Protects ACP/daemon sessions from concurrent write corruption via atomic hard-link lease. Extracted from #7166.
   *Author:* @doudouOUC

6. **[#7256](https://github.com/QwenLM/qwen-code/pull/7256) — Strip Qwen-internal daemon secrets from child process env** (OPEN)
   *Description:* Fixes #6601 — prevents credential leakage (`QWEN_SERVER_TOKEN`) to shell subprocesses, monitor tool, and stdio MCP servers.
   *Author:* @chinesepowered

7. **[#7248](https://github.com/QwenLM/qwen-code/pull/7248) — Enforce Plan mode entry boundary** (OPEN)
   *Description:* Makes `enter_plan_mode` an execution boundary — runs the entry call, returns terminal denials for same-batch siblings, prevents mode confusion.
   *Author:* @doudouOUC

8. **[#7258](https://github.com/QwenLM/qwen-code/pull/7258) — Yield to single-slot background agents** (OPEN)
   *Description:* Prevents main agent from starving the subagent when only one background slot is available. Records tool result and yields.
   *Author:* @hogeheer499-commits

9. **[#7247](https://github.com/QwenLM/qwen-code/pull/7247) — Retry model API errors instead of stranding PRs** (OPEN)
   *Description:* Prevents autofix PRs from getting stuck when model API returns 403/429/5xx — retries instead of treating it as evaluated handoff.
   *Author:* @wenshao

10. **[#7255](https://github.com/QwenLM/qwen-code/pull/7255) — Emit OAuth login URL as single OSC 8 hyperlink** (OPEN)
    *Description:* Fixes #6428 — URL was hard-wrapped across multiple lines when printed in non-TUI/SSH environments, making it unclickable.
    *Author:* @chinesepowered

---

## Feature Request Trends

- **Subagent & Multi-Agent Improvements:** Multiple issues request better observability (#6569), resource arbitration (#7254), and isolation (#7221) for subagent execution.
- **Web Search & External Tool Integration:** After successful closure of #4801 (dedicated web_search), community interest is turning toward MCP server reliability (#7147) and tool listing stability.
- **Daemon & Server Configuration:** Requests for configurable timeouts (#7244), token plan region selection (#7252), and multilingual evaluation baselines (#7216) show a maturing infrastructure.
- **Platform Parity:** Windows Docker sandbox issues (#7139) remain the biggest platform gap, with users calling for consistent shell and sandbox behavior across OSes.

---

## Developer Pain Points

- **Subagent Resource Contention:** The most frequently reported category — subagents blocking the main agent (#7254), mutating session state (#7156), and lacking observability (#6569). The `maxConcurrency: 1` edge case is particularly frustrating for local inference users.
- **MCP/API Integration Fragility:** MCP servers timing out (#7147), missing `reasoning_tokens` (#7236), and generic connection errors that discard root causes (#6996) highlight a need for better error reporting and compliance with the MCP spec.
- **Session & Context Management:** Plan mode content leakage (#6237), plan boundary enforcement (#7248), and background completion leaking into final replies (#7222) indicate the session management layer needs hardening.
- **Windows & Docker Sandbox:** The invalid workspace CWD bug on Windows (#7139) and the desire for full Channel management in Web Shell (#7209) show infrastructure gaps for non-macOS/Linux users.
- **Token/Quota Visibility:** Users struggle with missing reasoning tokens in stats (#7236), token plan region selection UI (#7252), and understanding background agent costs — a theme across multiple open issues.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-20

**Project:** [Hmbown/CodeWhale (DeepSeek TUI)](https://github.com/Hmbown/DeepSeek-TUI) (Note: Issues/PRs reference the `CodeWhale` repository)

---

## Today's Highlights

A burst of localization, performance, and MCP infrastructure work lands today, with 19 closed PRs and 4 open. The Blue Stage default grammar goes live, bringing semantic color tokens and localized session/route pickers. On the bug front, a Windows argument parsing regression and a scroll overflow in the sidebar list demand immediate attention. The community's long-standing request for environment-level tool sandboxing is finally resolved after a 2-week design discussion.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues (10 selected)

**#4594** | **Scrolling broken in sidebar for long To-do lists** (OPEN)  
*Author: Hmbown* | [Issue](https://github.com/Hmbown/CodeWhale/issues/4594)  
A core UX bug: the top bar / sidebar list won't scroll past ~5 items when a 10-item list is present. The maintainer themselves reported this, signaling high priority. Any user relying on the Work list for task tracking is blocked. 👎 0 yet — likely just filed.

**#4568** | **Slash commands (`/xxx`) lagging — regression from prior version** (OPEN)  
*Author: whp233* | [Issue](https://github.com/Hmbown/CodeWhale/issues/4568)  
A perceived performance backslide. Users on Windows 10 report near-instant responses in older builds vs. seconds-long delays now. Suspects a perf optimization rollback. Low comment volume but high impact for daily drivers.

**#4564** | **Windows argument parsing breaks `--model` and `--toolsets` flags** (OPEN)  
*Author: alozano978-spec* | [Issue](https://github.com/Hmbown/CodeWhale/issues/4564)  
Flags placed before `exec --auto` are concatenated into a single arg on Windows (npm global install). Workaround exists (place flags after `exec`), but the request for `CODWHALE_MODEL` / `CODWHALE_TOOLSETS` env vars is a clean fix. 1 comment — sparse but specific.

**#4042** | **Environment-level tool sandboxing for sub-agents** (CLOSED)  
*Author: JayBeest* | [Issue](https://github.com/Hmbown/CodeWhale/issues/4042)  
**Closed today** after 14 days of discussion. Tracks runtime enforcement of `tool_restrictions` across sessions, sub-agents, Fleet workers, and MCP servers. The `--disallowed-tools` flag is confirmed working. This is a major security milestone for multi-agent setups. 16 comments — highest engagement on the board.

**#4582** | **MCP tools deferred even in Full Access Agent mode** (CLOSED)  
*Author: Angel-Hair* | [Issue](https://github.com/Hmbown/CodeWhale/issues/4582) (tracked by PR #4582)  
In `trust_mode=true` / `auto_approve=true`, MCP tools still had `defer_loading=true`, making them invisible. Fixed by skipping deferral when bypass approval is active. Addressed a core trust-mode usability gap.

**#4589** | **Quiet behavioral guidance tips** (CLOSED)  
*Author: Hmbown* | [Issue](https://github.com/Hmbown/CodeWhale/issues/4589) (tracked by PR #4589)  
Adds contextual tooltips for planning, background receipts, recovery after input clear, MCP failure recovery, and repetitive manual commands. Capped at one tip per session, two lifetime impressions per tip. A subtle UX improvement to reduce friction for new users.

**#4585** | **Coalesced read-only duplicate calls** (CLOSED)  
*Author: Hmbown* | [Issue](https://github.com/Hmbown/CodeWhale/issues/4585) (tracked by PR #4585)  
When the model issues duplicate read-only tool calls within the same turn, the system now executes only one and replays results. Reduces API cost and latency — a silent optimization that pays off in agentic loops.

**#4584** | **Debt gate removed from system prompt prefix** (CLOSED)  
*Author: Hmbown* | [Issue](https://github.com/Hmbown/CodeWhale/issues/4584) (tracked by PR #4584)  
The SlopLedger completion gate was fingerprinting the system prompt, breaking caching. Now attached only to the user-turn tail. Critical for prompt caching efficiency with long-running sessions.

**#4583** | **Blue Stage default grammar** (CLOSED)  
*Author: Hmbown* | [Issue](https://github.com/Hmbown/CodeWhale/issues/4583) (tracked by PR #4583)  
Semantic color tokens: action blue (`#6AAEF2`) for interaction, Signal Gold for attention, ice for Plan. Replaces hardcoded literals. A design system foundation that touches every surface — risky but already merged.

**#4564** | *(see above — also relevant to Developer Pain Points)*

---

## Key PR Progress (10 selected)

**#4593** | `fix(tui): harden PowerShell invocation for safe Windows execution` | [PR](https://github.com/Hmbown/CodeWhale/pull/4593)  
OPen. Adds `-NoLogo -NoProfile -NonInteractive` to all PowerShell spawns, captures `$LASTEXITCODE`. Directly addresses Windows stability and script exit-code fidelity.

**#4592** | `fix(tui): give every genuine Kimi K3 route a 1M context` | [PR](https://github.com/Hmbown/CodeWhale/pull/4592)  
OPen. Fixes Kimi K3 showing 128K instead of 1M due to fallback metadata gaps. Direct Moonshot route was fine; bare Code membership route had wrong floor. Model parity fix.

**#4591** | `fix(tui): advertise Alt+V for details, never bare v` | [PR](https://github.com/Hmbown/CodeWhale/pull/4591)  
OPen. Removes documentation that bare `v` opens details — the correct binding is Alt+V (⌥V on macOS). Fixes a user-facing documentation inconsistency that could lead to keybinding confusion.

**#4590** | `feat(tui): localize session and route picker surfaces` | [PR](https://github.com/Hmbown/CodeWhale/pull/4590)  
Closed. Completes Blue Stage localization for session picker status, errors, metadata, and model/provider list states. Languages: locales wired via existing `rust-i18n` infrastructure.

**#4588** | `feat(mcp): hot-reload the live tool pool` | [PR](https://github.com/Hmbown/CodeWhale/pull/4588)  
Closed. Adds `/mcp reload` command that atomically re-reads config, reconnects unchanged servers, and preserves runtime-added servers. Malformed initial config recovery included. Big for MCP server DX.

**#4587** | `docs(web): align the public surface with Blue Stage` | [PR](https://github.com/Hmbown/CodeWhale/pull/4587)  
Closed. Carries Blue Stage semantic tokens to the public site. Routes install, providers, and docs links to first-party pages. Synchronizes visual language across TUI and web.

**#4586** | `feat(tui): sharpen first-run control discovery` | [PR](https://github.com/Hmbown/CodeWhale/pull/4586)  
Closed. New first-run experience surfaces `/help`, `Ctrl+K`, and `codewhale doctor`, plus a mental-model step for Modes and permissions. Lowers onboarding barrier.

**#4581** | `feat(tui): export safe structured conversations` | [PR](https://github.com/Hmbown/CodeWhale/pull/4581)  
Closed. `/export` now clipboard-first, outputs the canonical API message stream with roles, tool calls, and redacted secrets/URLs. Enables audit and sharing without leaking credentials.

**#4579** | `feat(web): add provider-native search backend` | [PR](https://github.com/Hmbown/CodeWhale/pull/4579)  
Closed. Gates provider-native web search on exact capability facts for OpenAI, Anthropic, and xAI. Aggregators and custom endpoints fail closed. Preserves SSRF-guarded fetch path.

**#4576** | `feat(web): add shared fetch and extraction pipeline` | [PR](https://github.com/Hmbown/CodeWhale/pull/4576)  
Closed. Foundation for all web tooling: guarded fetch with retry, TTL cache, redirect revalidation, content classification, and HTML-to-Markdown extraction. Serves as the backbone for `fetch_url`, search, and citations.

---

## Feature Request Trends

1. **MCP hot-reload and lifecycle management** — PR #4588 delivers the `/mcp reload` command; the community has been asking for zero-downtime MCP server config changes.
2. **Environment-level tool sandboxing** — Issue #4042 (closed) finally enforces `tool_restrictions` across execution contexts: sessions, sub-agents, Fleet, MCP. Multi-tenant and security-conscious users are the primary drivers.
3. **Provider-native web search** — PR #4579 gates direct integration with OpenAI, Anthropic, and xAI search. Users want to stop relying on DuckDuckGo as the sole backend.
4. **Structured conversation export** — PR #4581 adds safe `/export` with credential redaction. Driven by needs for sharing sessions without leaking API keys or tokens.
5. **First-run and onboarding improvements** — PR #4586 adds `/help` and mental-model steps. Newcomers found the initial state confusing, especially around Modes and permissions.

---

## Developer Pain Points

1. **Windows argument parsing regression** — Issue #4564: flags consumed as a single concatenated argument. Forces workarounds and blocks CI scripting on Windows. Community is asking for env-var fallbacks (`CODWHALE_MODEL`, `CODWHALE_TOOLSETS`).
2. **Slash command latency regression** — Issue #4568: `/xxx` commands are sluggish in the latest version vs. older builds. Suspected perf optimization rollback; no root cause identified yet.
3. **Sidebar scroll breakage** — Issue #4594: To-do lists with 10+ items cannot be scrolled fully. Last items invisible — a core list-view bug that reduces productivity for task-heavy workflows.
4. **Kimi K3 context window cap** — PR #4592: despite documented 1M context, users saw 128K in some routes. Root cause: metadata fallback gaps. Fixed, but points to fragility in model metadata pipelines.
5. **MCP tool visibility in trust mode** — PR #4582: Full Access Agent mode bypassed approval but MCP tools still deferred. Required explicit fix; trust-mode users expect all tools visible.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*