# AI CLI Tools Community Digest 2026-07-04

> Generated: 2026-07-04 01:30 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem: Cross-Tool Comparison Report
**Date: 2026-07-04**

---

## 1. Ecosystem Overview

The AI CLI tools landscape is experiencing a maturation phase marked by aggressive patching cycles and growing community expectations around reliability. Claude Code and OpenAI Codex lead in absolute issue volume, reflecting their larger user bases, while Gemini CLI and Qwen Code show higher signal-to-noise ratios in well-structured feature discussions. A common theme across all tools is the tension between agent autonomy and user control—communities are demanding configurable safety guardrails, transparent billing, and deterministic tool execution. Notably, the sub-ecosystem of smaller tools (Pi, DeepSeek TUI, OpenCode) is innovating faster on multi-provider routing and sandboxing, suggesting a divergence where incumbents focus on model integration while challengers compete on infrastructure flexibility.

---

## 2. Activity Comparison

| Tool | Open Issues (Today) | PRs (Today) | Release Status | Notable Metric |
|------|--------------------|-------------|----------------|----------------|
| **Claude Code** | 10 hot issues | 7 notable PRs | **2 patch releases** (v2.1.200/201) | Highest issue volume; subagent OOM (#74035) most critical |
| **OpenAI Codex** | 10 hot issues | 10+ security PRs | Alpha release (rust-v0.143.0-alpha.35) | GPT-5.5 reliability crisis (#30364, 53 👍) |
| **Gemini CLI** | 10 hot issues | 10 PRs | Nightly (v0.51.0) | Strongest PR-to-issue ratio; security-focused |
| **GitHub Copilot CLI** | 10 new triage issues | 0 PRs | No release | Regressions across MCP, voice, auth |
| **OpenCode** | 10 hot issues | 10 PRs | No release | V2 architecture migration in progress |
| **Pi** | 10 issues | 10 PRs | v0.80.3 (with known bug) | Fastest fix turnaround (24h hotfix #6283) |
| **Qwen Code** | 10 issues | 10 PRs | **3 releases** (stable + nightly + cua-driver) | Most releases today; stable v0.19.6 |
| **DeepSeek TUI** | 10 issues | 10 PRs | v0.8.67 RC phase | Clean RC process; strong external contributor PRs |
| **Kimi Code CLI** | 0 | 0 | No activity | Inactive digest window |

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities:

### Multi-Model & Provider Routing
- **Claude Code, OpenAI Codex, DeepSeek TUI, OpenCode**: Per-sub-agent provider/model selection—users want heterogeneous model topologies (e.g., local LM Studio for code generation, cloud for reasoning).
- **Pi**: Explicit provider expansion (GLM, Azure Cognitive Services, DeepInfra)

### Context Compaction Control
- **OpenAI Codex** (#25792, #31033): Opaque compaction corrupts agent state; users demand opt-in and visibility
- **DeepSeek TUI** (#3780): Configurable compaction gates PR pending
- **Gemini CLI**: Related to subagent turn-limit false successes (#22323)

### Session & State Management
- **Claude Code**: Session resumption broken on directory rename (#74043), ghost state across restarts
- **OpenAI Codex**: Remote-control session model mismatch, stale lock on IDE auto-connect
- **OpenCode**: Conversations disappearing after app update (#31023)
- **Copilot CLI**: Session recall leaks cross-project history (#4025)

### Billing & Quota Transparency
- **OpenAI Codex**: Rate-limit reset credit details PRs (#30395, #30488); quota consumption while idle (#31054)
- **OpenCode**: Free model exhaustion errors (#35142, #12219); subscription billing failures (#35215)
- **Claude Code**: Multi-account switching (#36151, 415 👍)

### AST-Aware Code Intelligence
- **Gemini CLI** (#22745): Investigating AST-aware file reads and search
- **DeepSeek TUI** (#3980): Structural code search + AST-backed edit previews
- **Claude Code**: Implicit in subagent orchestration needs

### Sandboxing & Security
- **OpenAI Codex**: 10+ security PRs hardening Git ops, PowerShell, sandbox escapes
- **Pi** (#6299): VM-backed filesystem tools for multi-tenant deployments
- **Qwen Code** (#6282): `transform_data` isolation enforcement
- **Gemini CLI** (#28175): Shell parameter expansion confirmation

---

## 4. Differentiation Analysis

### Feature Focus

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|-------------|----------|-----|-----------|--------------|
| **Subagent orchestration** | Heavy (but buggy) | Moderate | Core feature | Limited | V2 migration | Light | Light | Moderate |
| **Security hardening** | Medium | **Highest priority** | High | Low | Low | High (sandboxing) | Medium | Medium |
| **Multi-provider** | Anthropic-only | OpenAI-only | Gemini-only | Copilot-only | **All providers** | **Many** | Qwen + OpenAI-compat | **Heterogeneous** |
| **IDE integration** | VS Code + JetBrains | VS Code | VS Code | **VS Code primary** | Editor-agnostic | TUI-only | VS Code + Web | TUI + Web |
| **Windows support** | Good | **Persistent problems** | Medium | **Crash regressions** | **Paste broken** | WSL issues | Good | Good |
| **Mobile** | Mobile app requested | Desktop app | No | Web | Web UI | No | Web shell | No |

### Target Users

- **Claude Code, OpenAI Codex**: Professional developers using Anthropic/OpenAI ecosystems—prioritize model access over infrastructure flexibility
- **Gemini CLI**: GCP-aligned teams; focus on subagent reliability and agent autonomy
- **Copilot CLI**: GitHub ecosystem users; lightweight agent experience, weakest community engagement
- **OpenCode, Pi**: Power users and tinkerers; value provider diversity and customizability over polished UX
- **Qwen Code**: Chinese-market developers; strong on channel integration (WeCom) and web shell
- **DeepSeek TUI**: Security-conscious developers; constitution-based trust model, multi-tenant deployment

### Technical Approach

- **Claude Code**: Monolithic agent orchestrator with deep subagent nesting—bleeding edge but unstable
- **OpenAI Codex**: Rust rewrite (alpha) with security-first sandboxing; GPT-5.5 dependency is a liability
- **Gemini CLI**: Evaluations-driven development (#24353, 76 tests); methodical but slow to ship UX fixes
- **OpenCode**: V2 architecture migration with MCP-first design; OpenAPI tool adapter signals API-first strategy
- **Pi**: Fastest iteration cycle; hotfix within 24h; pragmatic about accepting LLM imperfections (hallucinated keys)
- **DeepSeek TUI**: Strongest external contributor culture (40% of notable PRs from community); constitution system is unique

---

## 5. Community Momentum & Maturity

### High Momentum / Rapid Iteration

| Tool | Velocity Signal | Risk Factor |
|------|----------------|-------------|
| **Qwen Code** | **3 releases today** (stable + nightly + driver) | Breaking changes not visible to users; context window bug undermines trust |
| **Pi** | 24-hour hotfix cycle; 10 PRs with 7 merged | v0.80.3 self-update broken; dependency fragility |
| **DeepSeek TUI** | Clean RC process (v0.8.67); strong external contributors (4 non-team PRs) | Spam management; RC not yet shipped |
| **OpenCode** | V2 migration progressing (MCP lifecycle, Form service, OpenAPI adapter) | Free-tier billing crisis (#35142) causing community frustration |

### Stable / Mature

| Tool | Maturity Signal | Concern |
|------|----------------|---------|
| **Gemini CLI** | EPIC-based feature development (#24353); measured pace | Generalist agent hangs (#21409) unresolved for months |
| **Claude Code** | Largest community (415 👍 on feature request); Anthropic-backed | Subagent orchestration is unstable; auto-close bugs erode trust |

### Declining / Struggling

| Tool | Signal | Root Cause |
|------|--------|------------|
| **Copilot CLI** | 0 PRs today; 10 new triage-only issues; persistent crash (#4026) across 4 versions | Weak engineering investment; feature staleness |
| **OpenAI Codex** | GPT-5.5 reliability crisis; Windows second-class; 7-month-old unaddressed bug (#7291) | Model dependency bottleneck; Rust rewrite still alpha |

---

## 6. Trend Signals

### For Technical Decision-Makers

1. **The subagent orchestration ceiling is being hit.** Claude Code's OOM crashes (#74035), OpenAI Codex's implicit competition issues, and Gemini's false success reports (#22323) all point to a fundamental challenge: current architectures cannot reliably manage deeply nested agent trees. **Verdict**: Avoid deep subagent fan-out in production until memory lifecycle and error propagation are solved.

2. **Security hardening is shifting left—into the tool itself.** OpenAI Codex's dozen Git/PowerShell security PRs in a single day signal a new baseline expectation: tools must protect against repository-selected filters, merge driver execution, and sandbox escapes. **Verdict**: If your tool supports custom repos, you need this level of hardening—enterprise adoption depends on it.

3. **The multi-provider era has arrived.** DeepSeek TUI's per-sub-agent routing (#3969) and OpenCode's provider-agnostic architecture represent the emerging standard. Single-provider tools (Claude Code, OpenAI Codex, Gemini CLI) risk obsolescence as users demand heterogeneous model topologies. **Verdict**: Plan for provider abstraction layers now; proprietary lock-in will be a competitive disadvantage within 6 months.

4. **Context compaction is broken by design.** Opaque, automatic context compression that corrupts agent state is the #1 trust-destroying behavior across OpenAI Codex and DeepSeek TUI. **Verdict**: Implement configurable, user-visible compaction with opt-in—or lose power users.

5. **Windows is the canary in the coal mine.** Persistent crashes on Copilot CLI (#4026 across 4 versions), broken paste on OpenCode (#35258), and WSL integration failures on Pi (#6187) show that cross-platform AI tools still struggle on Windows. **Verdict**: If you target enterprise developers, Windows compatibility is table stakes—invest in dedicated Windows QA.

6. **Developer pain points converge on four themes:**
   - **State management** — sessions, memory, configuration that don't survive restarts
   - **Billing transparency** — idle consumption, hidden compaction costs, opaque quota
   - **Deterministic tool execution** — agents over-extending scope, ignoring user constraints
   - **Cross-platform consistency** — terminal width, keyboard bindings, paste behavior, display server compatibility

### For Developers Evaluating Tools

| Use Case | Recommended Tool | Reason |
|----------|-----------------|--------|
| **Enterprise security** | OpenAI Codex (strict, but rapidly hardening) | Most security PRs; sandbox-first design |
| **Provider diversity** | DeepSeek TUI or OpenCode | Both support per-role multi-provider routing |
| **Fastest iteration** | Pi | 24h hotfix cycle; pragmatic about edge cases |
| **Chinese market** | Qwen Code | WeCom integration; web shell; native model support |
| **Stability critical** | Gemini CLI | Methodical approach; behavioral eval suite |
| **GitHub ecosystem** | Copilot CLI (with caution) | Poor momentum; regressions across versions |

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-04 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

### #1 — Skill Creator Fixes (PR #1298, #1099, #1050, #362, #1323, #539, #361)
**Status:** Open | **Domain:** Meta-tooling / Infrastructure
**Summary:** A cluster of interlocking PRs addressing critical bugs in the `skill-creator` toolchain, particularly `run_eval.py`. The core issue: `run_eval.py` consistently reports `recall=0%` for every skill description, making the description-optimization loop optimize against noise. Root causes span Windows subprocess incompatibility (`claude.cmd` not found via `PATHEXT`), broken trigger detection that misses real skill names, YAML parsing failures with unquoted special characters, and UTF-8 byte-length panics. These are collectively the most active PRs in the repository, with sustained discussion across May–June 2026.
**Link:** https://github.com/anthropics/skills/pull/1298 | https://github.com/anthropics/skills/pull/1099 | https://github.com/anthropics/skills/pull/1050 | https://github.com/anthropics/skills/pull/362 | https://github.com/anthropics/skills/pull/1323

### #2 — Document Typography Skill (PR #514)
**Status:** Open | **Domain:** Document Quality
**Summary:** Adds typographic quality control for AI-generated documents, targeting orphan word wrap (1–6 words stranded on their own line), widow paragraph headers, and numbering misalignment. Addresses a universal pain point in AI-generated documents. The discussion focuses on whether these rules should be defaults rather than an optional skill.
**Link:** https://github.com/anthropics/skills/pull/514

### #3 — ODT Skill — OpenDocument Format (PR #486)
**Status:** Open | **Domain:** Document Formats
**Summary:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods). Responds to demand for LibreOffice/ISO-standard document support. Discussion highlights the challenge of handling the complex ZIP-based ODF structure within Claude's skill constraints.
**Link:** https://github.com/anthropics/skills/pull/486

### #4 — Self-Audit Skill v1.3.0 (PR #1367)
**Status:** Open (very recent, June 28) | **Domain:** Output Quality Assurance
**Summary:** A universal skill that audits AI output before delivery — starting with mechanical file verification (does every claimed file exist?) then performing a four-dimension reasoning audit prioritized by damage severity. Architecturally ambitious; discussion centers on whether auditing should be a meta-skill or built into the Claude Code core.
**Link:** https://github.com/anthropics/skills/pull/1367

### #5 — Testing Patterns Skill (PR #723)
**Status:** Open | **Domain:** Software Engineering
**Summary:** Comprehensive testing skill covering the full testing stack: Testing Trophy philosophy, AAA pattern, React component testing with Testing Library, mocking strategies, and visual regression testing. Discussion highlights community desire for more engineering-specific skills in the marketplace.
**Link:** https://github.com/anthropics/skills/pull/723

### #6 — macOS Sensory Skill / AppleScript Automation (PR #806)
**Status:** Open | **Domain:** Platform Automation
**Summary:** Teaches Claude to use `osascript` (AppleScript) for native macOS automation as a more reliable alternative to screenshot-based computer use. Features a two-tier permission system: Tier 1 for direct app scripting, Tier 2 for Accessibility API access. Discussion explores security implications of granting Claude direct system scripting capabilities.
**Link:** https://github.com/anthropics/skills/pull/806

### #7 — Color Expert Skill (PR #1302)
**Status:** Open | **Domain:** Design / Data Visualization
**Summary:** Self-contained color expertise covering naming systems (ISCC-NBS, Munsell, XKCD, RAL, CSS named) and color space selection guidance (OKLCH for scales, OKLAB for gradients, CAM16 for perception). Well-received as filling a specific knowledge gap. Author is a known color science contributor.
**Link:** https://github.com/anthropics/skills/pull/1302

---

## 2. Community Demand Trends

From the Issues tracker, the most-anticipated new Skill directions are:

| Demand Area | Signal | Key Issue |
|---|---|---|
| **Security & Trust Boundaries** | Highest engagement (34 comments) | #492: Community skills under `anthropic/` namespace enable trust abuse — demands namespace verification or sandboxing |
| **Org-Wide Skill Sharing** | 14 comments, 7 reactions | #228: Enterprise teams need centralized skill distribution vs. manual .skill file emailing |
| **Agent Governance & Safety** | 6 comments, cross-referenced by PR #1367 | #412: Demand for safety patterns — policy enforcement, threat detection, audit trails |
| **Windows Native Compatibility** | 3 separate issues, 3 PRs | #1061: `skill-creator` toolchain assumes Unix; blocks entire Windows user base from optimization loop |
| **MCP Export Standard** | 4 comments, ongoing relevance | #16: Community wants Skills exposed as MCP servers for cross-platform interoperability |
| **Skill Duplication & Namespace Hygiene** | 6 comments, 9 reactions | #189: `document-skills` and `example-skills` plugins install identical content, causing context-waste |

**Emerging pattern**: The community is moving from "build useful skills" toward "govern the skills ecosystem" — security (#492), sharing (#228), deduplication (#189), and quality gates (#1367) dominate the conversation.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and are likely to land soon:

| Skill | PR | Key Feature | Maturity |
|---|---|---|---|
| **Self-Audit** | #1367 | Mechanical verification + 4-dimension reasoning audit | Very new but high community interest |
| **Testing Patterns** | #723 | Full-stack testing methodology | Strong spec, waiting for merge |
| **Color Expert** | #1302 | Color naming + space selection | Author is recognized expert; likely fast-track |
| **Sensory (macOS)** | #806 | AppleScript automation | Security review in progress |
| **DOCX Fix — Tracked Changes** | #541 | Prevents `w:id` collisions with bookmarks | Bugfix, high probability of merge |
| **PDF Case Sensitivity** | #538 | Fixes 8 file reference mismatches for case-sensitive filesystems | Simple bugfix, likely imminent |

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is **meta-tooling reliability**: the `skill-creator` toolchain's persistent `recall=0%` bug (#556, #1169, #1298, #1323) has become the single largest blocker for the entire Skills ecosystem, effectively breaking the description-optimization loop for all contributors, while security governance and quality assurance have emerged as the next frontier of community concern.

---

# Claude Code Community Digest — 2026-07-04

## Today's Highlights

Two patch releases shipped addressing user control and model behavior: **v2.1.201** fixes Sonnet 5 session harness reminders, while **v2.1.200** makes `AskUserQuestion` dialogs stop auto-continuing and changes the default permission mode to "Manual." The community continues to report serious stability bugs around subagent orchestration, memory blowups, and session restoration failures—several filed in the last 24 hours alone as v2.1.200/201 roll out.

---

## Releases

**v2.1.201** (latest)
- Claude Sonnet 5 sessions no longer use the mid-conversation system role for harness reminders.

**v2.1.200**
- `AskUserQuestion` dialogs no longer auto-continue by default; users can opt into an idle timeout via `/config`.
- Changed the default permission mode to "Manual" across CLI, `--help`, VS Code, and JetBrains. `--permission-mode manual` and `"defaultMode": "manual"` are accepted.

---

## Hot Issues (10 notable)

1. **#36151 — Multi-account switching in Claude Mobile app**  
   *Author: CorneAussems | 116 comments | 415 👍*  
   The highest-reacted open feature request. Users with multiple Pro/Team accounts need seamless switching without shared email. Community resonance is strong—this has remained open since March without maintainer response.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/36151)

2. **#70315 — Hallucinated fake turns with stop_reason=null (re-report)**  
   *Author: imcts | 12 comments*  
   A persistent bug on Opus 4.8 where the model invents user/system turns. The original report was falsely auto-closed as duplicate; user is adamant it's not fixed and renders Opus 4.8 unusable.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/70315)

3. **#73487 — AskUserQuestion auto-selects after ~60s idle**  
   *Author: merttrkr | 7 comments*  
   Ironically filed just before v2.1.200 shipped its fix. Users want this configurable, not just toggled on/off—the new `/config` timeout may not address the "no timeout at all" use case.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/73487)

4. **#74035 — Deeply-nested subagent fan-out causes OOM**  
   *Author: tolldog | 2 comments*  
   A self-reported crash where Claude Code analyzed its own OOM logs. Subagents with deep nesting trigger unbounded memory growth. Critical for anyone using the Workflow/Agent tools heavily.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/74035)

5. **#74032 — Worktree isolation inflates env past ARG_MAX → E2BIG**  
   *Author: lowellbander | 1 comment*  
   After a single subagent with `isolation: 'worktree'`, every subsequent Bash call in the parent session fails. The environment becomes poisoned—unrecoverable without restart.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/74032)

6. **#74043 — Session inaccessible via --resume after directory path change**  
   *Author: Schmed | 1 comment*  
   Transcript files exist but sessions vanish from resumable lists when the project directory is renamed or moved. Stale session index problem affects workflow continuity.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/74043)

7. **#74023 — Settings resolve against cwd, not git root**  
   *Author: ElijahLynn | 2 comments*  
   `.claude/settings.json` is looked up relative to the literal working directory. Launching Claude Code from a subdirectory silently discards all project-level settings—a significant DX regression.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/74023)

8. **#73916 — Background subagent children stuck "Running" after parent completes**  
   *Author: princeradebe | 1 comment*  
   Subagents spawned by background agents remain listed as "Running" permanently in the background tasks panel, and TaskStop cannot reach them. Orphaned subagent lifecycle management is broken.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/73916)

9. **#74006 — Contradictory session limit times; subagents silently die**  
   *Author: jrobgood | 6 comments*  
   A single session shows different "session limit resets at X" times, background subagents fail terminally, and projections silently roll forward. Heavy users of Fable 5 agents are hitting this daily.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/74006)

10. **#74056 — Shift+Enter submits instead of inserting newline (regression ~June 30)**  
    *Author: dwebb-pf | 0 comments | 1 👍*  
    A keyboard-binding regression affecting v2.1.193/200 on macOS. Multi-line input workflow is broken—likely a TUI keybinding refactor gone wrong.  
    [Issue Link](https://github.com/anthropics/claude-code/issues/74056)

---

## Key PR Progress (7 notable)

1. **#74021 — fix(security-guidance): allow null findings in StructuredOutput schema**  
   *Author: sourabharsh | OPEN*  
   Relaxes the schema so that null findings (when no vulnerabilities found) don't trigger a wasteful retry round. Observed in 31 review sessions—small fix with outsized latency impact.  
   [PR Link](https://github.com/anthropics/claude-code/pull/74021)

2. **#74010 — enhance(feature-dev): system design patterns, edge cases, and operational context**  
   *Author: sourabharsh | OPEN*  
   Adds three new analysis steps to the `code-architect` agent: system design patterns, edge case detection, and operational runtime context (logging, metrics, rollback). Bridges high-level design and codebase reality.  
   [PR Link](https://github.com/anthropics/claude-code/pull/74010)

3. **#74009 — fix(plugin-dev): use "asks to" in two missed skill descriptions**  
   *Author: sourabharsh | OPEN*  
   Completes the consistency fix from #13204 for two plugin-dev skills that were missed. Pure documentation/description fix.  
   [PR Link](https://github.com/anthropics/claude-code/pull/74009)

4. **#42701 — fix init-firewall.sh crash from ipset repeated IPs**  
   *Author: michaelkonecny | CLOSED*  
   Devcontainer launch fix: when `marketplace.visualstudio.com` resolves to repeated IP addresses, `ipset` errors out. Adding `-exist` flag resolves this long-standing devcontainer bootstrap issue.  
   [PR Link](https://github.com/anthropics/claude-code/pull/42701)

5. **#74059 — Resume session fails with "undefined is not an object"**  
   *Author: joesh | OPEN*  
   A crash-on-resume with a cryptic `e.includes` error on undefined. Filed against v2.1.201—indicates a null-safety gap in the session index parsing.  
   [PR Link](https://github.com/anthropics/claude-code/issues/74059)

6. **#74049 — Remote-control spawned session ignores UI-selected model**  
   *Author: jonathanmwatson | OPEN*  
   Model picker shows Fable 5 but the first request serves Opus 4-8. Remote-control sessions aren't respecting model selection—likely a race condition in session initialization.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/74049)

7. **#74055 — Scheduler catch-up storm on restart**  
   *Author: Palo-Alto-AI-Research-Lab | OPEN*  
   After app restart, the scheduled-tasks runner fires daily tasks that already ran and even tasks with `enabled: false`. `lastRunAt` isn't updated by these ghost runs—scheduler state is not persistent across restarts.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/74055)

---

## Feature Request Trends

- **Multi-account & session management** (#36151, #74043, #74059) — Users want proper account switching in mobile, reliable session resumption across directory renames, and bulk operations in the desktop app (grouping, moving sessions).
- **Configurable timeouts & idle behavior** (#13922, #73487) — Hardcoded 60-second timeouts on `idle_prompt` and `AskUserQuestion` are too short; users demand tunable or disable-able idle handling.
- **Diff comparison against any branch** (#23626) — `claude code` currently only diffs against `main`. Developers working on feature branches or release branches need to compare against `develop`, `staging`, or any arbitrary ref.
- **In-session navigation** (#63901) — No quick way to jump to earlier user prompts in the current conversation without terminal scrollback. Users want Ctrl+R-style reverse search or jump-to-message.
- **Linux/riscv64 native binary** (#59813) — As RISC-V hardware becomes more common (e.g., Orange Pi 5), the absence of a native binary is blocking adoption on that platform.

---

## Developer Pain Points

- **Subagent lifecycle & memory management** (#74035, #73916, #74032, #74006) — The most critical theme this week. Deeply nested background agents leak memory until OOM, orphan children persist as "Running" forever, worktree isolation corrupts the parent shell's environment, and session-limit tracking is contradictory. The agent orchestration system has serious stability issues for heavy users.
- **Auto-closed bugs that aren't fixed** (#70315) — The bot marking duplicates without user confirmation is eroding trust. Users report that their issues are closed prematurely and the underlying bug persists.
- **Settings resolution is fragile** (#74023) — `.claude/settings.json` is resolved against `cwd` not `git root`, meaning subdirectory launches silently discard all project configuration. Easy to hit, hard to notice.
- **Keyboard binding regressions (#74056)** — Shift+Enter submission instead of newline insertion breaks multi-line input for anyone who composes longer prompts or pastes code blocks. A TUI regression that impacts daily productivity.
- **Safety guardrails over-blocking** (#74058) — Fable 5's broad safeguards are flagging routine authentication code. Anthropic acknowledges the intentional broadness, but developers hitting this mid-session with no bypass mechanism find it disruptive.
- **Ghost state across sessions** (#73675, #65925, #74017) — Remote control sessions, background tasks, and scheduled tasks all suffer from stale/ghost state that persists across restarts. The system lacks proper state reaping.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest
**2026-07-04**

## Today's Highlights
GPT-5.5 is experiencing significant reliability issues this week, with multiple reports of model unavailability via the `Responses-Lite` API path and degraded reasoning quality characterized by artifact clustering at fixed token boundaries. A major security hardening effort is underway across the codebase, with a dozen PRs from `bookholt-oai` focused on Git operation isolation, PowerShell execution safety, and sandbox escape prevention. Additionally, context compaction bugs continue to frustrate users working on long-running tasks, with agents losing progress tracking and workspaces with multiple Git repos still unsupported.

## Releases
**rust-v0.143.0-alpha.35** – Alpha release for the Rust-based CLI. No changelog or release notes provided. Available at: [openai/codex/releases](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.35)

## Hot Issues

1. **[#30364 – GPT-5.5 reasoning-token clustering at 516/1034/1552](https://github.com/openai/codex/issues/30364)**  
   User reports `gpt-5.5` responses disproportionately land at exactly 516, 1034, or 1552 reasoning tokens, coinciding with degraded performance on complex tasks. **53 upvotes** and **37 comments** indicate widespread concern. This suggests a hard-coded token budget or truncation bug in the reasoning pipeline.

2. **[#30224 – Model not supported with X-OpenAI-Internal-Codex-Responses-Lite](https://github.com/openai/codex/issues/30224)**  
   Core API routing bug: certain models fail when the internal `Responses-Lite` header is active. **68 comments** and **22 upvotes**. Multiple duplicates (e.g., #30406, #30912, #30595) confirm a cross-platform, cross-client regression.

3. **[#7291 – VSCode extension fails to revert changes](https://github.com/openai/codex/issues/7291)**  
   Long-standing bug (since Nov 2025) where Codex cannot undo its own file edits in VS Code. **47 comments**, zero resolution in 7+ months. Raises trust concerns for agent-generated patches.

4. **[#20214 – Codex App freezes/stutters on Windows 11](https://github.com/openai/codex/issues/20214)**  
   **40 upvotes** – Performance regression on Windows 11 despite ample system resources (Ryzen 5 5600, 32GB RAM). Suggests a rendering or event-loop bottleneck in the Electron app.

5. **[#25792 – Context compaction forgets AGENTS rules](https://github.com/openai/codex/issues/25792)**  
   Task progress can jump from 97% back to 42% after automatic compaction. Critical for reliability of long-running agent sessions. Only **12 comments** but high severity for power users.

6. **[#30009 – apply_patch fails with Windows sandbox error](https://github.com/openai/codex/issues/30009)**  
   All file edits through the sandbox on Windows fail. **21 comments** – indicates a fundamental sandbox integration issue with the Win32/WSL boundary.

7. **[#31033 – Context automatically compacted](https://github.com/openai/codex/issues/31033)**  
   User reports consuming 2 resets and 50% of monthly quota before noticing silent compaction. No user control or notification for this operation.

8. **[#30137 – GPT-5.5 feels downgraded to 5.3](https://github.com/openai/codex/issues/30137)**  
   Subjective but high-signal report: `gpt-5.5` intelligence has "significantly reduced" in the last two days. Possibly related to the token-clustering bug in #30364.

9. **[#25353 – VS Code browser plugin installed but no session-owned route](https://github.com/openai/codex/issues/25353)**  
   Browser automation plugin appears installed but is non-functional in VS Code sessions. Cross-plugin integration gap between Codex Desktop and extension.

10. **[#31054 – Quota consumption while idle](https://github.com/openai/codex/issues/31054)**  
    Pro users report Exec quota decreasing ~1%/minute even with no interaction. Background polling or heartbeat misconfiguration is burning paid credits.

## Key PR Progress

1. **[#30395 – Expose rate-limit reset credit details](https://github.com/openai/codex/pull/30395)**  
   `app-server` – Adds v2 API endpoints for available reset credits, expiry times, and user-selectable consumption. Paired with CLI PR #30488.

2. **[#30854 – Block selected merge drivers before three-way patch](https://github.com/openai/codex/pull/30854)**  
   Security: prevents `git apply --3way` from running repository-selected custom merge drivers that could execute arbitrary code.

3. **[#31058 – Retry model capacity errors](https://github.com/openai/codex/pull/31058)**  
   Core fix: retries structured model-capacity failures (HTTP 503) up to 3 times with jittered backoff (30s, 2m, 5m). Addresses transient capacity issues without failing user requests.

4. **[#30850 – Block Git filters before staging paths](https://github.com/openai/codex/pull/30850)**  
   Security: prevents `git add` from running repository-selected filters on unvalidated paths, avoiding LFS/smudge filter attacks.

5. **[#30628 – Trust protected PowerShell parsers](https://github.com/openai/codex/pull/30628)**  
   Windows sandbox hardening: inspects PowerShell commands via a protected parser before execution, preventing model-selected `powershell.exe` from bypassing command policy.

6. **[#30990 – Harden namespace-aware executable policy matching](https://github.com/openai/codex/pull/30990)**  
   Windows path normalization fix: verbatim/device paths (e.g., `\\.\...`) could allow `git.exe.` to inherit `Allow` authority and bypass sandbox.

7. **[#30983 – Isolate one-shot command approval retries](https://github.com/openai/codex/pull/30983)**  
   Fixes approval prompt leaking: a one-shot decision could authorize both sandboxed and unsandboxed retries if the user was slow to respond.

8. **[#30896 – Centralize repository authority for Git helper launches](https://github.com/openai/codex/pull/30896)**  
   Creates a single trusted Git executable selector for all operations, avoiding PATH-based lookup that could be hijacked by repository config.

9. **[#28761 – Keep default-branch discovery on local refs](https://github.com/openai/codex/pull/28761)**  
   Prevents `git remote show` from contacting remotes during passive branch discovery, avoiding SSH/credential hijacking from untrusted repos.

10. **[#30313 – Add referral invites to /usage](https://github.com/openai/codex/pull/30313)**  
    Client-side referral invite flow under `/usage` in the CLI, reusing existing ChatGPT HTTP endpoints. Revenue/growth feature for Codex CLI.

## Feature Request Trends

- **Per-subagent model/provider selection** ([#14039](https://github.com/openai/codex/issues/14039), 12 upvotes): Users want spawned subagents to use different models than the parent session. High demand for multi-model orchestration.
- **Multi-repo workspace support** ([#26338](https://github.com/openai/codex/issues/26338), 8 upvotes): Parent folders containing multiple independent Git repositories are unsupported. Frequently raised (#15168, #14218).
- **Real-time session sync** ([#31062](https://github.com/openai/codex/issues/31062)): Request for bidirectional sync between Codex App and CLI clients, enabling seamless switching between interfaces.
- **Rate-limit transparency** ([#30395](https://github.com/openai/codex/pull/30395), [#30488](https://github.com/openai/codex/pull/30488)): Multiple PRs adding reset-credit details to CLI and app-server. Community wants granular visibility into quota state.

## Developer Pain Points

1. **GPT-5.5 reliability crisis** – Token clustering, "downgrade" perception, and `Responses-Lite` routing failures make the flagship model unpredictable. Multiple duplicates across platforms.
2. **Windows is a second-class citizen** – Persistent crashes ([#31029](https://github.com/openai/codex/issues/31029)), sandbox failures ([#30009](https://github.com/openai/codex/issues/30009)), PowerShell window flashing ([#26613](https://github.com/openai/codex/issues/26613)), Computer-Use/WSL incompatibility ([#25301](https://github.com/openai/codex/issues/25301)) – Windows users face most platform-specific bugs.
3. **Context compaction is opaque and destructive** – No user control, no notification, and it corrupts agent state. [#25792](https://github.com/openai/codex/issues/25792) and [#31033](https://github.com/openai/codex/issues/31033) highlight a broken trust model for long-running tasks.
4. **Quota/rate-limit confusion** – Idle consumption ([#31054](https://github.com/openai/codex/issues/31054)), web/desktop desync ([#23192](https://github.com/openai/codex/issues/23192)), and silent exhaustion undermine Pro/Plus value proposition.
5. **VSCode extension reliability** – The revert bug ([#7291](https://github.com/openai/codex/issues/7291)) is 7+ months old with no fix. Approval flow missing ([#30821](https://github.com/openai/codex/issues/30821)) and browser plugin failures ([#25353](https://github.com/openai/codex/issues/25353)) degrade IDE integration.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-04

## Today's Highlights
The v0.51.0 nightly release introduces an egress Cloud Run service skeleton for the caretaker system. Agent reliability remains the top concern, with critical bugs around subagent recovery falsely reporting success after hitting turn limits (Issue #22323) and the generalist agent causing indefinite hangs (Issue #21409). Meanwhile, significant security-focused PRs are advancing, including shell parameter expansion confirmation requirements and stricter bot artifact approval workflows.

## Releases
- **[v0.51.0-nightly.20260703.gf7af4e518](https://github.com/google-gemini/gemini-cli/releases/tag/v0.51.0-nightly.20260703.gf7af4e518)** — Adds a Cloud Run service skeleton for the caretaker egress system ([PR #28167](https://github.com/google-gemini/gemini-cli/pull/28167)). Full changelog available.

## Hot Issues (Top 10)

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent recovery after MAX_TURNS falsely reports GOAL success** (P1, 9 comments, 2 👍)  
   The `codebase_investigator` subagent claims completion with `status: "success"` even when it hit the maximum turn limit before performing any analysis. This is a dangerous reliability bug that misleads users about actual task completion.

2. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — Leverage model's bash affinity via Zero-Dependency OS Sandboxing** (P2, 8 comments, 1 👍)  
   Proposes exploiting Gemini 3's native bash expertise with safe sandboxing, aiming to let the model use standard POSIX tools directly rather than through restricted abstractions.

3. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — Robust component-level evaluations** (P1, 7 comments, 0 👍)  
   An EPIC tracking behavioral eval improvements — currently 76 tests covering 6 models. Critical for catching regressions in agent behavior.

4. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — Assess AST-aware file reads, search, and mapping** (P2, 7 comments, 1 👍)  
   Investigating whether AST-aware tools can reduce token usage and turn count by precisely reading method bounds, navigating codebases, and improving search accuracy.

5. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs indefinitely** (P1, 7 comments, 8 👍)  
   High community impact: simple tasks like folder creation cause indefinite hangs when the generalist agent is invoked. Workaround is instructing the model not to use subagents — not acceptable for production use.

6. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini does not use skills and sub-agents enough** (P2, 6 comments, 0 👍)  
   Custom skills (e.g., Gradle, Git) are largely ignored unless explicitly instructed. Users expect the model to autonomously select relevant tools based on task context.

7. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retries low-signal sessions indefinitely** (P2, 5 comments, 0 👍)  
   The background extraction agent never marks sessions as "processed" when it skips them for low signal, leading to infinite retries. Wasteful and noisy.

8. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell execution gets stuck with "Waiting input" after completion** (P1, 4 comments, 3 👍)  
   Even trivial shell commands leave the CLI hanging in a "waiting for input" state. Extremely disruptive to workflow.

9. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland** (P1, 4 comments, 1 👍)  
   Consistency issue: the browser agent crashes on Wayland display servers, limiting Linux users.

10. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent should discourage destructive behavior** (P2, 3 comments, 1 👍)  
    The model occasionally uses `git reset --force` or similar destructive commands when safer alternatives exist. Users want built-in guardrails.

## Key PR Progress (Top 10)

1. **[#28175](https://github.com/google-gemini/gemini-cli/pull/28175) — Require confirmation for shell parameter expansion**  
   Downgrades allowlisted shell commands with `${VAR}` expansion to require user confirmation in interactive mode, and outright denies in YOLO mode. Addresses a security gap where parameter expansion could be exploited.

2. **[#27971](https://github.com/google-gemini/gemini-cli/pull/27971) — Strip thoughts from scrubbed history turns**  
   Fixes "thought leakage" where the model's internal reasoning spills into plain-text history, causing infinite loops. Critical for long-running sessions.

3. **[#28178](https://github.com/google-gemini/gemini-cli/pull/28178) — Require approved bot patch artifacts**  
   Introduces explicit approval markers before the publish job consumes `bot-changes.patch`. Fail-closed security for the CI/CD pipeline.

4. **[#28248](https://github.com/google-gemini/gemini-cli/pull/28248) — Document MCP env expansion**  
   Adds proper documentation for `$VAR`, `${VAR}`, `${VAR:-fallback}`, and Windows `%VAR%` syntax in MCP server configurations. Clarity for a confusing area.

5. **[#28247](https://github.com/google-gemini/gemini-cli/pull/28247) — Match `ls` ignore globs by relative path**  
   Fixes `ls` ignore patterns with path separators (e.g., `node_modules/.cache`) not being applied. Uses `picomatch` for `**` glob support.

6. **[#28183](https://github.com/google-gemini/gemini-cli/pull/28183) — Preserve terminal focus when closing diff tabs (VS Code)**  
   Usability fix for the VS Code companion extension: diff previews no longer steal keyboard focus from the terminal. Small change, big DX impact.

7. **[#28240](https://github.com/google-gemini/gemini-cli/pull/28240) — Add support for AGENTS.md out of the box**  
   Fixes #28227: `AGENTS.md` is now included as a default context file alongside `GEMINI.md`, without requiring manual configuration.

8. **[#28153](https://github.com/google-gemini/gemini-cli/pull/28153) — Ignore stale `update_topic` calls after session reset**  
   Prevents orphaned `update_topic` tool calls from corrupting the topic state after `/clear`. Race condition fix.

9. **[#28149](https://github.com/google-gemini/gemini-cli/pull/28149) — Respect `.gitignore`/`.geminiignore` in skill resource listing**  
   Skill folder structures now properly filter out ignored files when presented to the model. Cleaner, less noisy context.

10. **[#28144](https://github.com/google-gemini/gemini-cli/pull/28144) — Detect available editors lazily to avoid slow startup**  
    Probes editor availability on-demand instead of at module load time. Fixes multi-second startup delays on Windows.

## Feature Request Trends

- **AST-aware tooling**: Multiple issues (e.g., #22745, #22746) push for Abstract Syntax Tree awareness in file reads, search, and codebase mapping to reduce token waste and improve navigation precision.
- **Better agent autonomy & tool selection**: Users want agents to autonomously select skills and sub-agents based on task context (#21968), without needing explicit instructions.
- **Subagent transparency**: Demand for subagent trajectory visibility in `/chat share` (#22598) and bug reports (#21763) for debugging and eval purposes.
- **Self-awareness**: A recurring theme (#21432) is the model knowing its own flags, hotkeys, and capabilities well enough to guide users internally.
- **Component-level evaluation infrastructure**: Epic #24353 tracks building robust behavioral evals to prevent regressions — a sign of growing maturity in the testing pipeline.

## Developer Pain Points

- **Stuck/hanging shells**: Multiple bugs (#25166, #21409, #22465) report the CLI getting stuck at "Waiting input" after commands complete or during interactive prompts, severely disrupting workflows.
- **Configuration ignored by subagents**: Issues like #22267 (browser agent ignoring `settings.json`) and #20079 (symlinked agents not recognized) show configuration management is brittle.
- **Auto Memory noise and retries**: The memory system retries low-signal sessions indefinitely (#26522), logs content before redaction (#26525), and silently skips invalid patches (#26523) — all pointing to quality issues in the background extraction pipeline.
- **Cross-platform inconsistency**: Wayland browser failures (#21983), WSL `fs.watch` issues (#28012), and slow editor detection on Windows (#28144) highlight platform-specific reliability gaps.
- **Destructive default behavior**: The model's propensity to use `git reset --force` and other destructive commands (#22672) without proper guardrails is a persistent user concern.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — July 4, 2026

## 1. Today's Highlights
A flurry of triage-labeled issues appeared over the last 24 hours, signaling potential regressions in MCP, voice, and authentication flows. The community is actively **demanding alt-screen opt-out** (#1799, 11 comments, 7 👍) as a UX priority, while **Model "gpt-5.3-codex" is unavailable** (#3997) blocks agent workflows for Web users. A new **persistent native crash** (#4026) reported across four versions suggests a fundamental stability regression on Windows.

## 2. Releases
No new releases in the past 24 hours.

## 3. Hot Issues

| Issue | Title (Label) | Why It Matters |
|-------|---------------|----------------|
| [#1799](https://github.com/github/copilot-cli/issues/1799) | How to turn off alt-screen views? (configuration, terminal-rendering) | **11 comments, 7 👍** — Alt-screen mode introduced recently is breaking workflows. Clear demand for a config toggle. |
| [#3997](https://github.com/github/copilot-cli/issues/3997) | Copilot Web: Model "gpt-5.3-codex" is not available (triage) | **9 comments** — Blocks all Copilot Web coding agents. A backend provisioning issue with high blast radius. |
| [#4026](https://github.com/github/copilot-cli/issues/4026) | Copilot CLI crashes repeatedly (native runtime) (triage) | **New today** — Unpredictable crashes on Windows across v1.0.15–v1.0.53. No single repro step identified. |
| [#4024](https://github.com/github/copilot-cli/issues/4024) | Voice mode: all bundled ASR models fail silently (triage) | **New today** — `/voice` records audio but all three models return empty transcriptions. Likely a routing bug in multimodal core. |
| [#1504](https://github.com/github/copilot-cli/issues/1504) | Add custom theme support (theming-accessibility) | **20 👍, 7 comments** — Long-standing request for shareable custom theme JSON files. Strong community support. |
| [#4019](https://github.com/github/copilot-cli/issues/4019) | Built-in web_fetch does not work with HTTP proxies (triage) | **New today** — Corporate/proxy users cannot use `/research` or web retrieval. Common enterprise blocker. |
| [#4014](https://github.com/github/copilot-cli/issues/4014) | Rendering all messed up when adding an MCP server (triage) | **New today** — Terminal corruption when using `/mcp add` on Windows. Affects v1.0.69-0. |
| [#4020](https://github.com/github/copilot-cli/issues/4020) | IDE auto-connect falsely skipped as "already in use" (triage) | **New today** — Session fork/close leads to stale lock. Breaks IDE auto-connect until manual restart. |
| [#4013](https://github.com/github/copilot-cli/issues/4013) | Ctrl+V image paste fails with raw clipboard data (triage) | **New today** — macOS: image paste no-op when clipboard contains raw data (vs. file URL). |
| [#4023](https://github.com/github/copilot-cli/issues/4023) | `web`/`search` tool-category aliases silently resolve to none (triage) | **New today** — Headless `--agent` dispatch silently drops tool categories. No error warning. |

## 4. Key PR Progress
No pull requests updated in the past 24 hours.

## 5. Feature Request Trends
- **Theme & Accessibility**: Custom theme creation and sharing (#1504, 20 👍) alongside reports that theme setting is not remembered (#4015).
- **Non-interactive / Headless Modes**: `/init` hangs in batched scripts (#4011); `web`/`search` tool aliases fail silently in headless mode (#4023).
- **Plugin & MCP UX**: Asynchronous execution for `/mcp show` and `/plugin list` (#3829); MCP server pagination is ignored (#4006).
- **Terminal Configurability**: Configurable scroll speed (#4018) and ability to disable alt-screen (#1799).
- **BYOK & Authentication**: BYOK still broken in `--acp` mode (#4016); reasoning effort unsupported for third-party models (#4012).

## 6. Developer Pain Points
- **Stability regressions**: The persistent Windows crash (#4026) returning across four versions is a major concern, with no root cause yet.
- **Proxy / enterprise blocks**: `web_fetch` ignores HTTP proxies (#4019), making the CLI non-functional in many corporate WSL environments.
- **Feature staleness after session close**: IDE auto-connect lock not released (#4020); session recall leaks cross-project history (#4025).
- **Copy & paste corruption**: Terminal scrollbar column glyph `┃` corrupts mouse selection (#4009); misleading "Copied to clipboard" notification (#4010).
- **Voice reliability**: All ASR models silently fail (#4024), rendering voice mode unusable for transcription tasks.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-04

## Today's Highlights
The community is experiencing a surge of issues related to free model credit exhaustion and subscription billing, with **#35142** becoming the most active thread (39 comments). The V2 architecture migration continues apace, with multiple PRs merging around MCP lifecycle APIs, shell event alignment, and session log replication safety. A notable contributor patch for the long-standing `pkill -f` bash-tool hang (#25664) has been submitted and refined across two PRs today.

## Releases
No new releases in the last 24 hours.

## Hot Issues (Top 10)

1. **[#35142](https://github.com/anomalyco/opencode/issues/35142) — Insufficient balance in free model**  
   *Author: Cebonk03* | 39 comments | 👍 3  
   A user reports being unable to use the DeepSeek V4 Flash Free model. This is the highest-activity issue today, suggesting widespread free-tier provisioning problems.

2. **[#30086](https://github.com/anomalyco/opencode/issues/30086) — High CPU usage in newer versions**  
   *Author: DenisSilent* | 15 comments | 👍 8  
   Performance regression affecting multi-session users; CPU load spiked such that 3 sessions now cause system lag where 10 previously worked. High community endorsement (8 upvotes).

3. **[#13626](https://github.com/anomalyco/opencode/issues/13626) — FEATURE: Auto-sync projects in web UI from server**  
   *Author: BlankParticle* | 10 comments | 👍 8  
   Long-running request (since February) for web UI to fetch project list from server on new device login. Consistent upvote signal indicates strong demand.

4. **[#26038](https://github.com/anomalyco/opencode/issues/26038) — `/exit` in PowerShell exits the terminal**  
   *Author: Tide-Breeze* | 9 comments | 👍 2  
   A UX foot-gun: `/exit` intended for OpenCode's internal command dispatcher instead terminates PowerShell entirely.

5. **[#33696](https://github.com/anomalyco/opencode/issues/33696) — GitHub Copilot provider broken**  
   *Author: jasonfirkus* | 8 comments | 👍 5  
   After fresh auth flow, GitHub Copilot provider returns no models. Possibly a regressions in provider discovery.

6. **[#27474](https://github.com/anomalyco/opencode/issues/27474) — TypeError: Failed to fetch**  
   *Author: QFinn-Penguin* | 7 comments | 👍 0  
   Clicking "Explore" or agent UI without navigating into a sub-agent triggers an unhandled fetch error in the renderer.

7. **[#12219](https://github.com/anomalyco/opencode/issues/12219) — "You requested up to 32000 tokens, but can only afford 0"**  
   *Author: arshadbarves* | 7 comments | 👍 6  
   Kimi 2.5 Free model fails due to OpenRouter credit/token mismatch. Another free-tier friction point.

8. **[#35215](https://github.com/anomalyco/opencode/issues/35215) — Go models not working**  
   *Author: jokker-10* | 4 comments | 👍 0  
   Paid Go subscription models broken after latest update: "Upstream request failed" on every paid model attempt.

9. **[#35258](https://github.com/anomalyco/opencode/issues/35258) — Paste (right-click & Ctrl+V) not working on Windows terminals**  
   *Author: aadiexii* | 2 comments | 👍 0  
   Fresh bug today: clipboard paste is completely non-functional in Windows terminal environments.

10. **[#31909](https://github.com/anomalyco/opencode/issues/31909) — Custom providers fail on Desktop (Electron) with ESM directory import**  
    *Author: holytshirt* | 3 comments | 👍 0  
    Custom npm providers work in CLI (Bun) but break on Electron due to a one-char path resolution difference for ESM directory imports.

## Key PR Progress (Top 10)

1. **[#35235](https://github.com/anomalyco/opencode/pull/35235) — refactor(core): step ledger and classified settlement**  
   *Author: kitlangton* | CLOSED  
   Behavior-preserving refactor of the V2 runner's settlement logic. 144 runner-adjacent tests pass with zero test-logic changes.

2. **[#35257](https://github.com/anomalyco/opencode/pull/35257) — fix(desktop): match rounded window background**  
   *Author: Hona* | OPEN  
   Fixes Electron window background color to match the resolved app theme, keeping rounded Windows corners dark. Includes a Playwright pixel-sampling regression test.

3. **[#35232](https://github.com/anomalyco/opencode/pull/35232) — feat(core): wire execute tool for v2 mcp**  
   *Author: rekram1-node* | OPEN  
   Adds a V2 core execute tool backed by CodeMode over MCP tools. Makes `execute` the default MCP exposure path in V2.

4. **[#35222](https://github.com/anomalyco/opencode/pull/35222) — fix: surface task_id in interrupted tool error text for LLM resume**  
   *Author: flaxodev* | OPEN  
   The sub-agent session ID was persisted in DB metadata but never rendered to the LLM. Now the error text includes `task_id` for resume via the Task tool. Closes #35177.

5. **[#35075](https://github.com/anomalyco/opencode/pull/35075) — docs: add oh-my-loop to ecosystem**  
   *Author: vc999999999* | OPEN  
   Adds `oh-my-loop`, an external loop controller for OpenCode, to the community ecosystem docs in English and Simplified Chinese.

6. **[#35245](https://github.com/anomalyco/opencode/pull/35245) — fix(shell): bound bash-tool hangs via scope teardown**  
   *Author: Levosilimo* | OPEN  
   Fixes the `pkill -f` hang (#25664) by teardown of the shell scope rather than relying on multiple timeouts. A cleaner approach than the earlier #35241.

7. **[#35247](https://github.com/anomalyco/opencode/pull/35247) — feat(tui): compact shell progress output**  
   *Author: ibakaidov* | OPEN  
   Publishes semantic progress snapshots from shell tools and renders them as a compact TUI progress bar, replacing raw redraw spam.

8. **[#35189](https://github.com/anomalyco/opencode/pull/35189) — feat(tui): render forms and route question tool through form service**  
   *Author: rekram1-node* | OPEN  
   Integrates the V2 Form service into the TUI, migrating the question tool onto it. First consumer of the form surface ($#35094 series).

9. **[#35192](https://github.com/anomalyco/opencode/pull/35192) — feat(codemode): add OpenAPI tool adapter**  
   *Author: rekram1-node* | OPEN  
   Adds `OpenAPI.fromSpec` — a basic OpenAPI 3.x document-to-codemode tool adapter, one tool per operation. Auth is never model-visible.

10. **[#17645](https://github.com/anomalyco/opencode/pull/17645) — fix(provider): apply config model cost overrides at runtime**  
    *Author: mollux* | OPEN  
    A long-running PR (since March) that fixes a runtime gap where model price overrides from config were present in resolved config but not applied to cost calculations.

## Feature Request Trends

- **V2 Architecture Alignment**: Multiple requests for porting MCP lifecycle, session shell events, and log replay to the V2 API surface (#34435, #34498, #35018, #35015).
- **Human-in-the-Loop Gating**: #35239 requests an approval gate after plan composition so users can review plans before automatic fix execution.
- **Configuration & Environment Expansion**: #35253 requests `{env:VAR}` expansion in provider/model headers (beyond just `apiKey`). #28527 highlights vars not working in `options.headers`.
- **Ecosystem Plugins**: #35251 requests adding `oh-my-loop` to the official ecosystem list.
- **UI/UX Quality of Life**: #35208 asks for auto-expanding matched directories in explore tool results; #22925 requests returning a pre-allocated assistant message ID in async prompt responses.

## Developer Pain Points

- **Free Model & Subscription Failures**: At least 5 separate issues today (#35142, #12219, #35215, #35191, #35252) involve free model exhaustion errors or paid Go subscriptions returning "free usage exceeded" errors. This is the dominant pain point.
- **Provider/Billing Reliability**: GitHub Copilot provider broken (#33696), Go upstream request failures (#35215), and custom provider ESM import errors on Desktop (#31909) paint a picture of fragile provider integration.
- **Performance Regression**: High CPU usage (#30086) continues to affect multi-session workflows without a merged fix.
- **Windows UX Issues**: Paste not working in Windows terminals (#35258) is a critical usability regression.
- **Session Data Loss**: #31023 reports conversations disappearing after app update; recovery attempts fail.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-04

## Today's Highlights
This week's digest centers on tool-call reliability (especially for the `edit` tool with newer Claude models), the ongoing fallout from the `@smithy/node-http-handler` dependency crash in v0.80.3, and a series of fixes for provider-specific quirks (Cloudflare 404s, stale extension contexts, Codex websocket timeouts). A batch of hardening contributions from the Gondolin sandbox example and subagent example also landed, signalling growing interest in multi-tenant and VM-backed deployments.

## Releases
No new releases in the last 24 hours. The latest published version remains **v0.80.3** (still affected by the `@smithy/node-http-handler` dependency issue described in closed issue #6215).

## Hot Issues (10 noteworthy)

1. **[#4945] openai-codex Connection Reliability Issues** — High volume (73 comments, 30 👍). GPT-5.5 / Codex connections frequently hang with a "Working..." spinner, requiring an Escape abort. Users report it as a daily frustration. Community suspects a race in the TUI stream handler.  
  [Link](https://github.com/earendil-works/pi/issues/4945)

2. **[#6278] New Claude models fail ~20% of edits** — 12 comments. Claude Sonnet 5, Fable 5, Opus 4.8 emit hallucinated extra keys (`newText_x`, `in_file`, `type`, `closeenough`) in the `edit` tool's `edits[]` array. Invalidates the strict schema. A hot fix PR #6283 is already merged.  
  [Link](https://github.com/earendil-works/pi/issues/6278)

3. **[#6215] `pi update` fails on 0.80.3 — missing @smithy/node-http-handler@^4.9.1** — 22 comments. PNPM cannot resolve the dependency; breaking self-update for all users on 0.80.3. Workaround: `pnpm store prune`.  
  [Link](https://github.com/earendil-works/pi/issues/6215)

4. **[#6187] Pi login hangs in WSL after Copilot device authorization** — 15 comments. Browser flow completes, but terminal never detects completion. WSL networking / event-loop integration suspected.  
  [Link](https://github.com/earendil-works/pi/issues/6187)

5. **[#6259] `content is not iterable` when reasoning models return null content** — 3 comments. GLM-5.2 on Fireworks returns `reasoning_content` + `tool_calls` but null `content`. Crashes compaction and rendering. Multiple code paths need null guards.  
  [Link](https://github.com/earendil-works/pi/issues/6259)

6. **[#6268] Codex websocket terminates after 60 minutes, no retry** — 3 comments. Long tasks are dropped without automatic reconnection. User community requesting a reconnect loop with backoff.  
  [Link](https://github.com/earendil-works/pi/issues/6268)

7. **[#6239] HTTP 524 (Cloudflare timeout) should be retryable** — 3 comments. Proxy/gateway users hitting Anthropic API get 524 with no retry logic; session aborts. Simple classification gap.  
  [Link](https://github.com/earendil-works/pi/issues/6239)

8. **[#6238] `supportsDeveloperRole: false` ignored in v0.80.3** — 3 comments. Custom OpenAI-compatible providers now incorrectly send `role: "developer"`. Regression from upstream role-handling refactor.  
  [Link](https://github.com/earendil-works/pi/issues/6238)

9. **[#6101] Embedded library: shared extension runtime poisoned across sessions** — 3 comments. Using `@earendil-works/pi-coding-agent` as a library: `AgentSession` reuse in the same process throws "stale ctx" errors. Blocks library embedding workflows.  
  [Link](https://github.com/earendil-works/pi/issues/6101)

10. **[#6299] Gondolin example: filesystem tools must ALL be VM-backed; grep unsandboxable** — 1 comment (high signal). Security analysis: `ls`, `grep`, `find` not VM-sandboxed in the Gondolin example; `grep` cannot be sandboxed by operations injection alone. Important for multi-tenant hardening.  
  [Link](https://github.com/earendil-works/pi/issues/6299)

## Key PR Progress (10 important)

1. **[#6294] Improve pi config add-ons UX** (merged) — Reworks `pi config` around an Add-ons mental model with package-level toggles, detail panes, and subagent model-fit guidance. A significant UX improvement for managing extensions.  
  [Link](https://github.com/earendil-works/pi/pull/6294)

2. **[#6292] fix(ai): resolve Cloudflare account id from ambient env** (merged) — Fixes the persistent Cloudflare Workers AI 404 on 0.80.x. Reads `CLOUDFLARE_ACCOUNT_ID` from env rather than hardcoding; closes #6021 properly this time.  
  [Link](https://github.com/earendil-works/pi/pull/6292)

3. **[#6290] fix(ai): use "(no tool output)" placeholder for empty tool results** (merged) — Stops hallucinating image attachments when tools produce no output. Prevents GPT from inventing screenshots for empty `grep` results.  
  [Link](https://github.com/earendil-works/pi/pull/6290)

4. **[#6285] fix(ai): stop salvaging malformed tool-call argument JSON** (open) — Strict parsing of tool-call arguments: truncated/malformed JSON preserved on `ToolCall.malformedArguments` instead of silently corrupting state. Invasive; needs careful review.  
  [Link](https://github.com/earendil-works/pi/pull/6285)

5. **[#6283] fix(coding-agent): strip hallucinated extra keys from edit tool edits[]** (merged) — Direct fix for #6278. Strips LLM-invented extra keys from `edits[]` items before validation. Hotfix shipped within 24 hours of the bug report.  
  [Link](https://github.com/earendil-works/pi/pull/6283)

6. **[#6279] fix(coding-agent): add pnpm self-update prune hint** (merged) — Recovery hint for #6215: suggests `pnpm store prune` when self-update fails due to stale registry metadata.  
  [Link](https://github.com/earendil-works/pi/pull/6279)

7. **[#6266] Anthropic: strict tool use for the edit tool** (merged) — Moves the `edit` tool to Anthropic's strict tool-use mode. Reduces hallucinated keys at the source. Complements #6283 for Claude users.  
  [Link](https://github.com/earendil-works/pi/pull/6266)

8. **[#6273] Add Zen mode tool call labels** (merged) — New `/settings zenMode` toggle for compact tool-call labels in TUI. Generates safe fallback labels synchronously, then asynchronously replaces with GPT-5.4-mini summaries.  
  [Link](https://github.com/earendil-works/pi/pull/6273)

9. **[#6271] Add GLM API provider** (merged) — First-class support for Zhipu AI and Z.AI GLM endpoints using `ZAI_API_KEY`. Covers both domestic and international endpoints.  
  [Link](https://github.com/earendil-works/pi/pull/6271)

10. **[#3799] Add Azure Cognitive Services provider** (merged after 2 months) — Adds support for `*.cognitiveservices.azure.com` base URLs alongside existing `*.openai.azure.com`. Normalizes path routing.  
  [Link](https://github.com/earendil-works/pi/pull/3799)

## Feature Request Trends

- **Provider expansion** is the dominant theme: DeepInfra (#6270), Kimi K2.7 for GitHub Copilot (#6256), GLM API (merged #6271), and Azure Cognitive Services (merged #3799).
- **TUI improvements**: Show active built-in tools in the footer (#6277), include session name in resume hints (#6296), AI-generated session titles from conversation content (#6209).
- **Sandboxing & security**: The Gondolin and subagent hardening issues (#6299, #6298, #6297) represent a new wave of requests for production-grade multi-tenant deployment with VM-backed filesystem tools.
- **Resume without sending a message** (#3721, 2 👍) — a long-standing request for continuing the agentic loop without influencing the LLM with an extra message. Still open and popular.

## Developer Pain Points

- **Tool-call reliability with newer models** is the #1 pain point this week. The `edit` tool fails ~10–20% of the time with Claude Sonnet 5 and Fable 5 (#6278). LLMs hallucinate extra keys, requiring both server-side stripping (#6283) and provider-side strict mode (#6266).
- **Self-update breaks on dependency resolution failures** (#6215). PNPM's stale registry metadata prevents `pi update` from completing. The workaround (`pnpm store prune`) is not obvious to users.
- **Codex connection fragility** (#4945, #6268): both the interactive TUI hang and the 60-minute websocket limit cause session aborts. No automatic retry mechanism exists.
- **Null content crashes** (#6259, #6276): reasoning models returning `null` for `content` crash compaction and rendering. Multiple code paths lack null guards.
- **WSL integration issues** (#6187): Copilot device authorization completing in the browser but never being detected in the WSL terminal remains a blocker for Windows developers.
- **Provider compatibility regressions**: The `supportsDeveloperRole: false` override being silently ignored in v0.80.3 (#6238) and Cloudflare Workers AI still returning 404 (#6021, fixed in #6292) show that provider-specific edge cases continue to slip through.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-04

## Today's Highlights
A busy patch day with three releases, including the stable **v0.19.6** with mobile session-switch fixes and a new **cua-driver-rs v0.7.0** bringing relative-coordinate support. The community is actively discussing a critical context window miscalculation bug (#6144) and a performance issue where `/review` consumes excessive tokens (#6264), while the team continues tightening CI gates and expanding channel integrations (WeCom, proactive loop tools).

---

## Releases

- **[v0.19.6-nightly.20260704.5dc2e1501](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.6-nightly.20260704.5dc2e1501)** — Nightly release with a strengthened PR gate: batch detection, problem existence checks, and red flag patterns for triage automation.

- **[v0.19.6](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.6)** — Stable release fixing mobile session-switch jank in web-shell via memoized timeline signature and replay-first dispatch, plus macOS seat resolution.

- **[cua-driver-rs-v0.7.0](https://github.com/QwenLM/qwen-code/releases/tag/cua-driver-rs-v0.7.0)** — Prebuilt binaries for all major platforms (macOS codesigned + notarized, Linux x86_64/arm64, Windows x86_64/arm64). New feature: relative-coordinate fork vendored under `packages/cua-driver`.

---

## Hot Issues

1. **[#6144 — Context window miscalculation](https://github.com/QwenLM/qwen-code/issues/6144)** (OPEN, P2)  
   User configured a Qwen3-Coder instance with 64K ctx but Qwen Code reports incorrect window. 6 comments, 1 👍. Could impact all users with custom model configs.

2. **[#6265 — `tool_search` invalidates KV-cache on every deferred-tool load](https://github.com/QwenLM/qwen-code/issues/6265)** (OPEN, P2)  
   Performance-critical: each `tool_search` call triggers three API steps that clear the LLM's KV-cache. Welcome for community PRs.

3. **[#6264 — `/review` consumes large amount of tokens](https://github.com/QwenLM/qwen-code/issues/6264)** (OPEN, P2)  
   Heavy token usage reported for the review skill, with screenshots showing excessive consumption. Needs triage, awaiting reproduction info.

4. **[#6249 — Empty `arguments` string tool calls silently dropped](https://github.com/QwenLM/qwen-code/issues/6249)** (OPEN, P1)  
   Streaming tool calls with empty arguments cause "Model stream ended with empty response text" retry loops. Affects all OpenAI-compatible providers with parameterless tools.

5. **[#6282 — `transform_data` does not enforce subprocess isolation](https://github.com/QwenLM/qwen-code/issues/6282)** (OPEN, P1)  
   Security concern: the handler skips filesystem/network isolation wrappers when launching transform scripts — a sandbox escape vector.

6. **[#6244 — Extension capability changes not reliably communicated to model](https://github.com/QwenLM/qwen-code/issues/6244)** (OPEN, P2)  
   Enabling/disabling extensions mid-session doesn't consistently update model context, causing stale tool definitions. Welcome for PRs.

7. **[#6237 — Plan Mode content leakage in subsequent responses](https://github.com/QwenLM/qwen-code/issues/6237)** (OPEN, P2)  
   `exit_plan_mode` leaks plan content into next assistant reply instead of delivering actual answers. Privacy concern for plan-heavy workflows.

8. **[#6283 — `settings.env` values silently shadowed by `.env` files](https://github.com/QwenLM/qwen-code/issues/6283)** (OPEN, P2)  
   API keys set via `/auth` get lost on restart because `.env` files load first in no-override mode. 2 comments, in-review PR exists.

9. **[#6246 — `qwen_code` cannot recognize its own process](https://github.com/QwenLM/qwen-code/issues/6246)** (OPEN, P2)  
   When asked to stop a process, it terminates all nodejs processes including itself. Critical for self-hosted backend setups.

10. **[#6218 — Taobao mirror three versions behind](https://github.com/QwenLM/qwen-code/issues/6218)** (CLOSED)  
    npmmirror sync lag reported — community request for faster mirror updates. Closed with autofix, but highlights distribution pain.

---

## Key PR Progress

1. **[#6272 — Daemon Status Dashboard](https://github.com/QwenLM/qwen-code/pull/6272)** (CLOSED, merged)  
   Adds a real-time daemon status page to web-shell showing health badge, triage issues, session/permission/rate-limit state. Backed by `GET /daemon/status` API.

2. **[#6287 — Proactive channel loop tools](https://github.com/QwenLM/qwen-code/pull/6287)** (OPEN)  
   Adds MCP-based recurring reminder system for channels: create, list, cancel loops through chat. Enables proactive agent behavior.

3. **[#6224 — WeCom intelligent robot channel](https://github.com/QwenLM/qwen-code/pull/6224)** (OPEN)  
   Rewrites WeCom integration to use intelligent robot API mode with WebSocket client, removing the need for custom app callbacks.

4. **[#5780 — `qwen update` and `/update` commands](https://github.com/QwenLM/qwen-code/pull/5780)** (OPEN)  
   CLI command + slash command for checking and installing updates. Handles standalone, npm, and yarn install paths. 11 days open but still active.

5. **[#6278 — Multi-folder workspace support](https://github.com/QwenLM/qwen-code/pull/6278)** (OPEN)  
   File system boundary checks now accept multiple workspace folders, fixing VSCode multi-root workspace rejection errors.

6. **[#6284 — Persistent 401 after API key change](https://github.com/QwenLM/qwen-code/pull/6284)** (OPEN)  
   Fixes three failure modes: empty-string env vars blocking, stale class-level cached key, and missing re-authentication trigger.

7. **[#6285 — Enforce `transform_data` isolation](https://github.com/QwenLM/qwen-code/pull/6285)** (OPEN)  
   Addresses #6282 by routing transform scripts through session-tool isolation wrappers with network + filesystem write isolation.

8. **[#6273 — Model fallback chain](https://github.com/QwenLM/qwen-code/pull/6273)** (OPEN)  
   Adds configurable backup models for the main conversation path, auto-switching on capacity/availability errors while preserving retry behavior.

9. **[#6242 — Custom @ mention panel](https://github.com/QwenLM/qwen-code/pull/6242)** (OPEN)  
   Replaces inline autocomplete with multi-level reference panel: categories, files, extensions, MCP resources, with keyboard + mouse support.

10. **[#6276 — Autofix tier-1 fast-path trust gate](https://github.com/QwenLM/qwen-code/pull/6276)** (OPEN)  
    Adds `autofix/approved` label requirement for fast-path automation. Maintainers must apply the label, preventing automated PRs from self-approving.

---

## Feature Request Trends

- **Channel & Chat Platform Integration** — Strong demand for WeCom (#6208, #6224), proactive reminders (#6287), and a general channel abstraction layer.
- **Web Shell Dashboard & Status UI** — Multiple requests for daemon status dashboard (#6252, #6272), visual chart rendering (#6226), and improved @ reference panels (#6242, #6279).
- **Model Management** — Fallback chains (#6273), vision bridge model selection (#6195), and better model context window handling (#6144).
- **Diagnostics & Debugging** — Local diagnostic quality improvements (#4421, #6277), ring buffer for API failures, and debug log structure.
- **Platform Distribution** — npm package size tracking (#6231), auto-update commands (#5780), and mirror sync reliability (#6218).

---

## Developer Pain Points

- **Context Window & Token Accounting** — Incorrect context window calculation (#6144) and massive token consumption from `/review` (#6264) are top complaints.
- **State & Configuration Leakage** — Plan mode content leakage (#6237), extension state not communicated (#6244), and settings/env shadowing (#6283) erode user trust.
- **Subprocess & Sandbox Isolation** — `transform_data` lacks isolation (#6282), and process management is unreliable (#6246 terminates itself).
- **Streaming & Tool Call Reliability** — Empty argument tool calls silently dropped (#6249) and KV-cache invalidation on tool search (#6265) cause frustrating retry loops.
- **Authentication & Key Management** — OAuth 504 timeouts (#6251), persistent 401 after key change (#6284), and QuickPick focus loss during `/auth` (#6230) hurt onboarding.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-04

## Today's Highlights
The v0.8.67 release cycle is in its RC phase, with the team hardening surfaces across provider routing, subagent lifecycle, and UX consistency. Community activity is split between late-stage quality fixes for the ongoing release and early feature proposals for v0.8.68, with notable contributions around dynamic MCP server infrastructure and per-sub-agent provider routing coming from external contributors. Spam continues to be an issue, with one unrelated medical billing post having been closed.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#3275 — CodeWhale over-extends modifications, deviating from user intent](https://github.com/Hmbown/CodeWhale/issues/3275)** 🗣️17 comments  
   Core behavioral regression: the agent enters a self-questioning/answering loop without user confirmation. Highly active, flagged as both security and reliability concerns across versions v0.8.66–v0.8.69. Community reaction suggests this is a top frustration for users expecting deterministic tool execution.

2. **[#3406 — v0.8.67 Setup: runtime posture card with constitution boundary](https://github.com/Hmbown/CodeWhale/issues/3406) (CLOSED)** 🗣️16 comments  
   Closed after introducing a posture selector (`ask-first / normal agent / high-trust local`) that prevents constitution creators from silently changing runtime security. Well-received resolution to a long-standing trust/approval UX gap.

3. **[#3793 — v0.8.67 Setup: guided localized constitution creator](https://github.com/Hmbown/CodeWhale/issues/3793) (OPEN)** 🗣️16 comments  
   Proposes a language-first, guided‑plus‑open‑canvas constitution creation flow. Still open as the team refines the autonomy/risk posture separation from runtime settings.

4. **[#3965 — Per-sub-agent provider assignment + LM Studio support](https://github.com/Hmbown/CodeWhale/issues/3965) (OPEN)** 🗣️7 comments  
   Community member JayBeest proposes explicit provider routing per sub-agent role (e.g., `explore` on local LM Studio, `generate` on cloud). Already has an accompanying PR (#3969). Signals strong demand for heterogeneous provider topologies.

5. **[#3884 — Codex sub-agents fail with "Responses API request failed"](https://github.com/Hmbown/CodeWhale/issues/3884) (CLOSED, release-blocker)** 🗣️4 comments  
   Blocked orchestration work since child agents failed silently. Marked release-blocker and closed within 24 hours, indicating a rapid fix.

6. **[#3961 — Make new-version prompts persistent and actionable](https://github.com/Hmbown/CodeWhale/issues/3961) (OPEN)** 🗣️2 comments  
   Core update machinery exists but the in-app UX for notifying users about new versions is weak. Proposal to make prompts sticky until action is taken.

7. **[#3980 — v0.8.68 Tools: structural code search + AST-backed edit previews](https://github.com/Hmbown/CodeWhale/issues/3980) (OPEN)** 🗣️1 comment  
   Roadmap item for 0.8.68: adds syntax-aware matching for refactors beyond grep/text patches. Low discussion but high strategic importance.

8. **[#3981 — v0.8.68 Tools: debugger protocol surface](https://github.com/Hmbown/CodeWhale/issues/3981) (OPEN)** 🗣️1 comment  
   Proposes DAP-based breakpoints, stepping, and variable inspection. Currently agents can only run tests and read logs—this would close a significant capability gap.

9. **[#3976 — v0.8.68 Memory: project-scoped recall](https://github.com/Hmbown/CodeWhale/issues/3976) (OPEN)** 🗣️1 comment  
   Lightweight per-project memory seed ahead of the full external-memory backend. Addresses the limitation of current user-scoped-only Markdown blocks.

10. **[#4007 — v0.8.67 RC final release-readiness pass](https://github.com/Hmbown/CodeWhale/issues/4007) (CLOSED, release-blocker)** 🗣️0 comments  
    Holistic final pass across binary paths, first-run onboarding, provider routing, and release notes. Closed rapidly—suggests the RC is nearly shippable.

## Key PR Progress
1. **[#3973 — refactor(shell): split output buffer helpers](https://github.com/Hmbown/CodeWhale/pull/3973) (OPEN)**  
   Contributor cyq1017 moves shell output delta/tail helpers into a dedicated module. No behavioral change—pure maintainability improvement for the shell tool surface.

2. **[#4025 — ci: light-classify inert scripts](https://github.com/Hmbown/CodeWhale/pull/4025) (OPEN)**  
   Fixes CI over-allocation where script-only changes triggered full macOS/Windows test suites. Targets cost savings and faster feedback for trivial PRs.

3. **[#4024 — test(setup): align QA script with repo constitution source](https://github.com/Hmbown/CodeWhale/pull/4024) (CLOSED)**  
   Canonicalizes binary paths and updates doctor context assertions. Quick quality fix for the 0.8.67 QA probe.

4. **[#4023 — fix(tui): harden v0.8.67 RC surfaces](https://github.com/Hmbown/CodeWhale/pull/4023) (CLOSED)**  
   Broad hardening: stream timeout config, plugin paths, provider routing, OAuth messaging, cost display, URL punctuation, and subagent sidebar cancellation updates. Likely the main RC cleanup PR.

5. **[#3969 — Add per-sub-agent provider routing](https://github.com/Hmbown/CodeWhale/pull/3969) (OPEN)**  
   External contributor heyparth1 implements explicit routing via `[subagents.routes.<role>]` config table, addressing #3965. Pins sub-agent roles to specific providers/models—highly anticipated feature for multi-provider setups.

6. **[#3869 — feat: add dynamic MCP server infrastructure to McpPool](https://github.com/Hmbown/CodeWhale/pull/3869) (OPEN)**  
   Contributor bistack adds in-memory dynamic server support to McpPool, laying foundation for runtime-started MCP servers from conversation context. Foundation layer for the `start_mcp_server` tool.

7. **[#3866 — feat: LLM can start MCP servers from chat context](https://github.com/Hmbown/CodeWhale/pull/3866) (OPEN)**  
   Companion to #3869: adds `start_mcp_server` tool supporting both stdio and HTTP transports. Enables LLMs to dynamically provision MCP servers during a session.

8. **[#3762 — feat(web): redesign homepage with trust strip](https://github.com/Hmbown/CodeWhale/pull/3762) (OPEN)**  
   Contributor idling11 adds MIT license badge, local-first messaging, provider count, and GitHub nav link. Also adds mirror/provenance links for CN users.

9. **[#3780 — expose context compaction gates](https://github.com/Hmbown/CodeWhale/pull/3780) (OPEN)**  
   Adds `[compaction].enabled` and `[seam_manager].enabled` config switches for Codex engine—gives users explicit control over context compaction behavior without code changes.

10. **[#3761 — defer startup maintenance cleanup](https://github.com/Hmbown/CodeWhale/pull/3761) (OPEN)**  
    Moves non-critical startup cleanup (stale tool-output pruning, old session cleanup) off the synchronous path into a delayed maintenance thread. Improves startup responsiveness.

## Feature Request Trends
- **Multi-provider & heterogeneous routing** (#3965, #3969, #3830): Users want per-sub-agent provider assignment, especially mixing local (LM Studio) with cloud endpoints in a single session.
- **Structural code intelligence** (#3980): Syntax-aware search and AST-backed edit previews to replace grep+text-patch refactors.
- **Debugger integration** (#3981): DAP protocol surface for breakpoints, stack frames, and variable inspection—agents currently blind to debug state.
- **Project-scoped memory** (#3976): Lightweight per-project recall without requiring the full external-memory backend. Users want agents to remember project conventions across sessions.
- **Onboarding automation** (#3978): Auto-import common agent/editor instruction files (`.cursorrules`, `.clinerules`, etc.) during context assembly to reduce manual migration effort.

## Developer Pain Points
- **Agent autonomy vs. user control** (#3275): The most upvoted issue—developers are frustrated by the agent over-extending scope without confirmation. The self-driven Q&A loop is a recurring reliability complaint across multiple versions.
- **Truncated UI at standard terminal widths** (#3994, #3992, #3989, #3988, #4008): Multiple UX issues where descriptions, provider names, and status chips cut mid-word without ellipsis at 80–120 columns. Makes pickers and configuration views feel broken.
- **Plugin state not persisted** (#3918): `/plugin enable|disable` writes to an in-memory map that resets on every restart—basic functionality gap that undermines trust in the plugin system.
- **Spam and noise** (#3893): Unrelated commercial posts continue to appear, requiring manual closure. Community may benefit from stricter issue templates or moderation tooling.
- **Cancellation visibility** (#4009): Cancelled sub-agents don't reflect their state in the sidebar, reducing feedback predictability during multi-agent orchestration.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*