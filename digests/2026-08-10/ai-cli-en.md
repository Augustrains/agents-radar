# AI CLI Tools Community Digest 2026-08-10

> Generated: 2026-08-10 00:45 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools

**Date:** 2026-08-10

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape is experiencing a phase of rapid maturation marked by significant reliability challenges. Across all seven major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI—communities are reporting critical bugs around security classifier false positives, denied tool calls executing anyway, silent session failures, and MCP integration fragility. The market is bifurcating between enterprise-focused tools like GitHub Copilot CLI and Claude Code (with remote/workflow features) and developer-preference leaders like OpenCode and Pi that are iterating quickly with community-driven features. Windows platform support remains an industry-wide weakness across all tools. The dominant narrative is that these tools have moved beyond proving capability and are now being tested on reliability, transparency, and trust in production environments.

---

## 2. Activity Comparison

| Tool | Open Issues (24h activity) | PRs (24h activity) | Release Status | Community Signal |
|------|---------------------------|---------------------|----------------|-----------------|
| **Claude Code** | ~20 (ClAudit false-positive storm) | 2 open, 1 closed | No new release (v2.1.221) | High severity; safety-system concern |
| **OpenAI Codex** | 10 hot issues | 10 closed PRs | No new release | High; Windows bug cluster |
| **Gemini CLI** | 10 hot issues | 10 PRs (2 core fixes, 8 dependency bumps) | Nightly only (v0.56.0-nightly) | Moderate; 5-month-old P1 hang persists |
| **GitHub Copilot CLI** | 10 hot issues (all triage-labeled) | 0 PRs | No new release | High; enterprise feature gaps |
| **Kimi Code CLI** | 2 hot issues | 1 old PR (Jan 2026) | No new release (v0.34.0) | Low; limited community activity |
| **OpenCode** | 10+ hot issues | 10 merged to dev | No new release (v1.18.15) | Very high; 110+ 👍 on clipboard bug |
| **Pi** | 10 hot issues | 10 closed PRs | No new release | High; TUI polish focus |
| **Qwen Code** | 10 hot issues | 10 PRs (mixed) | Nightly failed CI | Moderate; workflow-engine push |
| **DeepSeek TUI** | 10 hot issues | 2 closed, 1 open | v0.9.6 prepared (not shipped) | Moderate; v0.9.6 imminent |

**Note:** Claude Code has the highest severity incidents (denied tool call executed, session-halted false positives). OpenCode has the highest community engagement (110 👍 and 122 comments on a single clipboard bug). Gemini CLI has the most concerning longevity issue (5-month-old P1 generalist agent hang).

---

## 3. Shared Feature Directions

| Feature Direction | Tools | Specific Needs |
|-------------------|-------|----------------|
| **MCP lifecycle robustness** | Copilot CLI, Qwen Code, Claude Code | Configurable handshake timeouts, retry/backoff, lenient optional-method handling, no hard-fail on 404/errors |
| **Model fallback/failover across different model IDs** | OpenCode, Copilot CLI | Fallback between distinct model IDs (not just same-model providers); auto-switch on 429s/rate limits |
| **Cross-session memory systems** | Kimi CLI, Claude Code, Gemini CLI | Persistent context across sessions; auto-managed notes + user-defined instructions |
| **Multi-agent orchestration / delegation** | Qwen Code, Gemini CLI, Copilot CLI | Agents calling agents; unified coordination; child-session visibility in UI |
| **Non-streaming support** | OpenCode, Pi | Proxies (enterprise) that don't support streaming; configurable SSE/streaming disabled |
| **Windows platform parity** | Codex, Copilot CLI, Gemini CLI, OpenCode, Qwen Code, DeepSeek TUI | Installer fixes, IME stability, terminal emulation, file operations, runtime compatibility |
| **TUI scriptability/customization** | Codex, Pi | Custom status lines, configurable keybindings, theme hooks, layout control |
| **Permission/approval UX hardening** | Claude Code, DeepSeek TUI | Deny-by-default vs. allow; pinned-session protection; audit trails |
| **Compaction/session durability transparency** | DeepSeek TUI, Pi, OpenCode | Visible token savings, intent preservation, no silent fallback thresholds |
| **Remote/mobile workflow reliability** | Claude Code, Codex, Copilot CLI | Cross-device sync, SSH remote visibility, remote session portability |

---

## 4. Differentiation Analysis

| Tool | Feature Focus | Target User | Technical Approach |
|------|---------------|-------------|-------------------|
| **Claude Code** | Safety, plugins, skills, desktop/remote control | Power devs, enterprise, sysadmins | Anthropic-ecosystem; heavy emphasis on wrapper hooks (MessageDisplay, Stop hooks); Opus model safety classifier with problems |
| **OpenAI Codex** | TUI polish, Windows support, mobile/desktop sync | General devs, VS Code/Cursor users | Rust core; desktop app + TUI; gRPC transport; hook generalization; bounded path resolution |
| **Gemini CLI** | Subagent reliability, memory quality, skills spec | Google-AI users, enterprise | Node.js; ACP (Agent Client Protocol); caretaker-agent for memory; dependency-heavy; spec-compliance focus |
| **GitHub Copilot CLI** | Enterprise integration, MCP ecosystem, model routing | GitHub Enterprise, orgs | Rust; tight Copilot login integration; parallel tool-call correlation; managed-settings policy engine |
| **Kimi Code CLI** | Minimal, local-first, ACP streaming | Individual devs, Moonshot AI users | Go; ACP/print streaming; linear memory search (no vector index yet); Google GenAI provider compat |
| **OpenCode** | Model resilience, hooks compat, session ergonomics | Power users, multi-provider setups | TypeScript/Bun; plugins; worktree-based workspace switching; OpenCode Go gateway (fragile) |
| **Pi** | TUI ergonomics, provider-agnostic, extension system | Terminal-first devs, context-heavy workflows | TUI-first (Alt-screen); differential rendering; extension commands via `sendUserMessage`; llama.cpp catalog caching |
| **Qwen Code** | Workflow engineering, multi-agent coordination, CI/CD | Qwen-ecosystem, Alibaba Cloud users | Nightly releases; Goal v3 runtime; workflow engine (`/review` orchestration); streamable HTTP MCP |
| **DeepSeek TUI** | Compaction integrity, multi-provider, reproducibility | DeepSeek users, CJK devs | Rust; Fleet system for distributed agents; 20-crate monorepo; SOURCE_DATE_EPOCH reproducibility |

---

## 5. Community Momentum & Maturity

**Most Active / Rapidly Iterating:**
- **OpenCode** — Highest community engagement (110+ 👍 on clipboard bug, 122 comments). Merged 10 PRs to dev in 24h. Active V2 development. Strong plugin ecosystem.
- **Claude Code** — Es. Heavily watched, but the ClAudit false-positive storm and denied-tool-call-executed bug suggest safety systems are eroding trust. High visibility, high scrutiny.
- **Pi** — 12 PRs and 33 issues updated in 24h. Community is contributing fixes (2 competing PRs on Copilot rate-limit). TUI polish suggests a mature product.
- **Qwen Code** — Rapid iteration with nightly builds and CI-oriented PRs (sandbox watchdogs, triage budgets). Still fighting CI instability more than product bugs.

**Moderate Momentum:**
- **OpenAI Codex** — Closed 10 PRs but mostly internal-quality. No release. Windows bug cluster is the dominant story.
- **Gemini CLI** — Dependency churn (74 updates) but core issues (generalist hang) untouched for 5 months. Community is patient but noting stagnation.
- **GitHub Copilot CLI** — Triage-labeled issue wave with no PRs. Enterprise feature gaps persist. Community is vocal but not contributing fixes.
- **DeepSeek TUI** — v0.9.6 prepared but not shipped. Active issue triage. Still rebuilding trust around compaction.

**Low/Declining:**
- **Kimi Code CLI** — Only 2 hot issues, 1 stale PR. Minimal community activity. May be facing adoption headwinds despite features parallels.

**Maturity Assessment:**
*Established (production-stable):* Claude Code, Copilot CLI, Codex (despite bugs)
*Rapidly maturing:* OpenCode, Pi, Qwen Code
*Stabilizing:* Gemini CLI, DeepSeek TUI
*At risk:* Kimi Code CLI

---

## 6. Trend Signals

1. **Reliability now beats features.** The top issues across tools are about false positives halting work (Claude Code), denied calls executing (Claude Code, Copilot CLI), silent session deaths (Copilot CLI, OpenCode, Pi), and data loss (Gemini CLI, DeepSeek TUI). The race has shifted from "what can these tools do?" to "can I trust them with my work?"

2. **Windows remains a second-class platform everywhere.** Codex, Copilot CLI, Gemini, OpenCode, Qwen, DeepSeek all report Windows-specific failures (installers, IME, terminal emulation, file paths, runtime crashes). A tool that cracks Windows parity will gain significant adoption.

3. **MCP is becoming the critical integration layer — but its fragility is the new bottleneck.** Fixed timeouts, no retry, strict spec enforcement (Qwen Code, Copilot CLI), and schema incompatibilities (Kimi Code) collectively create a "MCP roulette" experience. Expect ecosystem pressure for a shared MCP robustness specification.

4. **Multi-agent orchestration is the next battleground.** Qwen Code's `/coordinate`, Gemini's agent-to-agent delegation PR, Copilot CLI's parallel subagent fan-out bugs, and OpenCode's nested-subagent permission fixes all point to the same trend: agents managing agents is where production value (and production failures) will concentrate.

5. **Context compaction transparency is the unspoken contract.** DeepSeek TUI's compaction issues (#5096, #5239), Pi's auto-compaction interruptions (#7848), and OpenCode's context-window management all reflect user anxiety about silent context loss. Loud, visible, debuggable compaction will be table-stakes.

6. **TUI ergonomics are now a product moat.** Codex's 150-👍 status-line request, Pi's scroll-and-copy fixes, Claude Code's Remote Control rendering failures, and Qwen's web-terminal flickering all show that the terminal UI is still the primary interaction surface — and polish is now a differentiator.

7. **Enterprise requirements are colliding with the tooling assumptions.** Non-streaming proxies (OpenCode #785), BYO-gateway model alias mapping (Codex #21594), org-repo `/remote` failures (Copilot #2751), and enterprise OAuth breaks (Copilot #4408) show that enterprise deployment is not a variant use-case — it's the growing reality.

8. **The "silent failure" class of bugs is the most dangerous and most common.** Whether it's Copilot's dropped kickoff prompt (#4423), Gemini's misreported subagent success (#22323), DeepSeek's false edit-success (#5209), or OpenCode's nested-hang (#13715), the pattern is identical: the tool says everything is fine, but nothing happened. This trend demands a cross-tool investment in observability, explicit state reporting, and fail-loud defaults.

---

*Report generated from community digest data for 2026-08-10. Metrics reflect issue/PR activity in the last 24 hours unless otherwise noted. All issue/PR numbers reference the respective tool repositories.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-08-10** | Source: github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Skills have attracted the most discussion and community attention via Pull Requests:

### 🥇 #1298 — skill-creator: fix run_eval.py (0% recall bug)
**Author:** MartinCajiao | **Status:** Open | **Created:** 2026-06-10
**Link:** [PR #1298](https://github.com/anthropics/skills/pull/1298)

The most actively discussed PR addresses a critical blocker: `run_eval.py` consistently reports `recall=0%` for every skill description, meaning the entire description-optimization loop in `run_loop.py` and `improve_description.py` is "optimizing against noise." The fix installs the eval artifact as a real skill, and resolves Windows stream reading, trigger detection, and parallel worker issues. This is directly tied to **Issue #556** (below) and represents the single highest-value infrastructure repair in the ecosystem — without it, skill _description quality_ cannot be iteratively improved.

### 🥈 #514 — document-typography: typographic quality control
**Author:** PGTBoos | **Status:** Open | **Created:** 2026-03-04
**Link:** [PR #514](https://github.com/anthropics/skills/pull/514)

Addresses a universal pain point in AI-generated documents: orphan word wraps, widow paragraphs, and numbering misalignment. The skill positions itself as a post-processing gate — "every document Claude generates" suffers these issues, and users rarely request fixes proactively. High relevance given the maturity of the `docx`, `pdf`, and `pptx` skills already in the collection.

### 🥉 #538 / #541 / #539 — DOCX & PDF precision fixes (Lubrsy706)
**Author:** Lubrsy706 | **Status:** Open | **Created:** 2026-03-06
**Links:** [PR #538](https://github.com/anthropics/skills/pull/538) · [PR #541](https://github.com/anthropics/skills/pull/541) · [PR #539](https://github.com/anthropics/skills/pull/539)

A three-PR campaign fixing low-level correctness issues:
- **#538:** Case-sensitive file references in `pdf/SKILL.md` (breaks on Linux/macOS)
- **#541:** Tracked change `w:id` collisions with existing bookmarks (document corruption in OOXML)
- **#539:** YAML frontmatter validation for unquoted descriptions with `:` characters

These reflect a maturing ecosystem: the community is no longer just proposing new Skills — it's hardening existing ones for production reliability.

### #486 — ODT skill (OpenDocument)
**Author:** GitHubNewbie0 | **Status:** Open | **Created:** 2026-03-01
**Link:** [PR #486](https://github.com/anthropics/skills/pull/486)

Adds full OpenDocument support (`.odt`, `.ods`): creation, template filling, and ODT-to-HTML conversion. Fills a clear gap between the existing `docx` and `pdf` skills, targeting LibreOffice users and ISO-standard document workflows.

### #210 — frontend-design clarity overhaul
**Author:** justinwetch | **Status:** Open | **Created:** 2026-01-05
**Link:** [PR #210](https://github.com/anthropics/skills/pull/210)

A revision of the existing `frontend-design` skill to improve actionability and internal coherence — ensuring instructions are concrete enough for Claude to follow within a single conversation. Discussed as a model for how existing Skills should be iteratively refined.

### #1367 — self-audit skill (v1.3.0)
**Author:** YuhaoLin2005 | **Status:** Open | **Created:** 2026-06-28
**Link:** [PR #1367](https://github.com/anthropics/skills/pull/1367)

Introduces a universal output-audit skill: mechanical file verification first, then a four-dimension reasoning audit in damage-severity priority order. Works across any project/stack/model. The associated proposal ([Issue #1385](https://github.com/anthropics/skills/issues/1385)) extends this into a three-gate reasoning pipeline (Pre-task Calibration → Adversarial Review → Delivery Verification).

---

## 2. Community Demand Trends

**From the Issues tracker, the most anticipated directions are:**

1. **Security & Trust Boundaries** — *Issue #492* (43 comments, the most-discussed issue overall): Community skills distributed under the `anthropic/` namespace enable trust boundary abuse. Users want clear provenance and permission scoping for community-submitted skills.
2. **Org-Wide Skill Sharing** — *Issue #228* (16 comments, 8 👍): Direct request for an organization-level skill library with sharing links, eliminating the manual download/send/upload workflow.
3. **Eval & Testing Infrastructure** — *Issues #556* and *#1169* (12 + 3 comments): The `run_eval.py` recall=0% bug is the single most impactful infrastructure defect — it silently breaks all skill description optimization. The community is actively demanding a working eval loop.
4. **Context Window Efficiency** — *Issue #1487*: The `claude-api` skill injects ~156k tokens in a single tool call, exhausting context. Users want lazy-loading or size-bounded skill designs.
5. **Duplicate Skill Pollution** — *Issue #189* (6 comments, 9 👍): Installing both `document-skills` and `example-skills` plugins installs identical skills, causing duplicates in the context window. Demand for dependency resolution and de-duplication.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and are strong candidates for merging:

| Skill | PR | Description | Why It Stands Out |
|---|---|---|---|
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Lifecycle management for planning artifacts (files accumulate with no cleanup) | Addresses a named gap (#1417), has community backing |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Self-contained color expertise: naming systems, color spaces, "what to use when" tables | Deep, structured, high-reuse topic |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Full testing stack: Testing Trophy, AAA pattern, React Testing Library, edge cases | Broad applicability, fills a clear gap (no general testing skill exists) |
| **pyxel** (retro games) | [#525](https://github.com/anthropics/skills/pull/525) | Workflow for Pyxel retro game engine: write → run_and_capture → inspect → iterate | Niche but concrete, by the Pyxel author (kitao) |
| **skill-quality-analyzer** + **skill-security-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Meta-skills to evaluate other skills across 5 quality dimensions and security | Directly addresses security concerns from Issue #492 |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, production-grade skill-development toolchain — fixing the broken eval loop, enforcing security boundaries, and preventing context-window blowups — before any new feature skills can deliver value.**

---

# Claude Code Community Digest — 2026-08-10

## Today's Highlights

The community is facing a significant wave of **cybersecurity safety-filter false positives** (ClAudit), with over 20 reports from a single user documenting session-halting incidents on benign operations like log rotation, printer recovery, and AD administration. Separately, a **denied PowerShell tool call executing anyway** (#83760) and **Remote Control rendering failures** (#85240) are raising serious reliability concerns. On the tooling side, two active PRs aim to fix YAML block-scalar parsing and spec-conformant skill naming — both quick wins that should land soon.

---

## Releases

No new releases in the last 24 hours. (Last known version in discussions: 2.1.221)

---

## Hot Issues

### 1. [Bug][cyber] ClAudit false-positive storm — session-halted on benign work (#85371–#85392)
**Reported by:** sworrl | **Comments:** ~20 across related issues | **[View #85371](https://github.com/anthropics/claude-code/issues/85371)**

A single user filed ~20 issues documenting **ClAudit flagging benign content** — including "fix the f*** adfs, why did it fill its disk overnight," "make sure the site is secure," and even "why do you keep flagging this?" — with severity **session-halted**. The flagging model is primarily **Opus 4.8** with a couple on **Opus 5**. This is a serious usability regression: authorized system-administration work is being blocked without context-awareness. The volume of reports (all from one power user) suggests either a systemic false-positive rate spike or a specific workflow pattern triggering it. Community reaction: single-user drive-by filings, but the consistent "session-halted" severity warrants a maintainer investigation.

---

### 2. [Bug] Safety-classifier model switch (Fable 5 → Opus 4.8) can't be overridden (#67246)
**Reported by:** AndrewTKent | **Comments:** 12 | 👍 3 | **[View Issue](https://github.com/anthropics/claude-code/issues/67246)**

The Fable 5 safety classifier silently switched a user's mid-session model to Opus 4.8 after flagging a "normal engineering discussion" as cybersecurity/biology. The built-in notice admits false positives are expected, but **`/model` cannot override the switch** — effectively locking users out of their chosen model mid-flight. This is a control-and-predictability issue: users lose agency without a documented escape hatch.

---

### 3. [Bug] Denied tool call executed anyway — PowerShell ran despite "deny" (#83760)
**Reported by:** P6oX6GAz | **Comments:** 2 | **[View Issue](https://github.com/anthropics/claude-code/issues/83760)**

The most severe reliability bug in this digest: a **PowerShell tool call executed even after the user denied it**. If confirmed, this is a safety-critical defect (the tool-permission system cannot be trusted). Low comment count so far, but this deserves immediate maintainer attention — escalated severity marker is warranted.

---

### 4. [Bug] Remote Control: responses don't render until manual refresh (#85240)
**Reported by:** rsicak | **Comments:** 5 | **[View Issue](https://github.com/anthropics/claude-code/issues/85240)**

Every assistant response fails to render in browser until the user manually reloads the page. Reproduces consistently on iPad Safari/Chrome and macOS Safari. This kills Remote Control's core value proposition (real-time monitoring). Community: 5 comments indicates a reproducible, multi-device report.

---

### 5. [Bug] Cross-platform sync failure — Cowork conversations disappearing (#81658)
**Reported by:** HSBE31 | **Comments:** 4 | 👍 3 | **[View Issue](https://github.com/anthropics/claude-code/issues/81658)**

Chats disappear across Desktop/Web/Android devices; the reporter suspects a server-side incident. Data-loss issues always generate high community concern — unlikely a client-side fix will resolve it, so maintaining visibility until Anthropic acknowledges server status is the primary action.

---

### 6. [Bug] Desktop: pinned sessions can be archived/deleted (#62104)
**Reported by:** wwalter409 | **Comments:** 5 | **Status:** CLOSED (stale) | **[View Issue](https://github.com/anthropics/claude-code/issues/62104)**

Requested UX hardening: Archive/Delete context-menu actions (and `A`/`D` shortcuts) should refuse pinned sessions, or require explicit Unpin first. The request also covers programmatic access via `mcp__ccd_sessions`. Now stale/closed, this is still a good candidate for community follow-up if the behavior persists.

---

### 7. [Bug] tools/list_changed doesn't refresh deferred-tool index (#66084)
**Reported by:** LudaThomas | **Comments:** 4 | 👍 2 | **[View Issue](https://github.com/anthropics/claude-code/issues/66084)**

`tools/list_changed` fails to update the ToolSearch index in interactive sessions — still reproducing on 2.1.165. This means tools added at runtime never appear in searchable/deferred lists. Community: 4 comments from a single reporter, but 👍 2 suggests at least two other users hit it.

---

### 8. [Bug] Plugin version resolution escapes marketplace root (#82712)
**Reported by:** kerfern | **Comments:** 1 | **[View Issue](https://github.com/anthropics/claude-code/issues/82712)**

When a marketplace ships without `.git` (e.g., GCS tarball) and a plugin declares `"version": null`, version resolution **walks up the filesystem** and adopts `~/.claude` HEAD — causing per-commit re-cloning. This is a correctness bug in plugin infrastructure with a clear repro path; maintainers should prioritize.

---

### 9. [Bug] MessageDisplay hook returns valid content but UI renders original text (#83957)
**Reported by:** frasalvi | **Comments:** 1 | **[View Issue](https://github.com/anthropics/claude-code/issues/83957)**

On 2.1.221 (terminal CLI), a `MessageDisplay` hook is invoked correctly with a well-formed payload and returns valid `hookSpecificOutput`, **but the terminal renders the original text**. Hook authors rely on this for custom rendering — silent failure undermines hook trust. Single comment, but a core integration point.

---

### 10. [Bug] Chrome file_upload rejects scheduled-task sessions on Windows (#84880)
**Reported by:** losangeles142 | **Comments:** 2 | 👍 1 | **[View Issue](https://github.com/anthropics/claude-code/issues/84880)**

`file_upload` in Chrome rejects scheduled-task sessions on Windows — reportedly the same as closed issue #63334. Windows-specific regression that breaks scheduled automation; 👍 1 indicates at least one other user confirms.

---

## Key PR Progress

### 1. [#85323](https://github.com/anthropics/claude-code/pull/85323) — fix(plugin-dev): parse block scalar agent descriptions (OPEN)
**Author:** erichanwang

Fixes the remaining YAML block-scalar parsing defect from #83803. `validate-agent.sh` now measures multiline `description: |` / `description: >` values from their indented content instead of treating the scalar marker as the entire description. Small, targeted fix for plugin validation.

### 2. [#85243](https://github.com/anthropics/claude-code/pull/85243) — fix(skills): use spec-conformant names (OPEN)
**Author:** bechor25

Eight bundled skills declare title-cased `name` fields containing spaces (e.g., `Writing Hookify Rules`), violating the SKILL.md spec. This PR standardizes them to spec-conformant lowercase-with-dashes naming. Affects `hookify` and `plugin-dev` skill families.

### 3. [#17395](https://github.com/anthropics/claude-code/pull/17395) — [Plugin] Add agent-session-commit plugin for AGENTS.md iteration (CLOSED)
**Author:** Olshansk

Deprecated/closed now, but notable as a pattern: uses `AGENTS.md` as authoritative project instructions, `CLAUDE.md` as a minimal pointer, and a Stop-hook-driven `/session-commit` plugin for ongoing doc generation. Illustrates a community approach to managing evolving agent-instruction files.

---

## Feature Request Trends

- **Model-switch freedom:** Users want the ability to override automatic safety-classifier-driven model switches (e.g., `/model` should work regardless). The classifier should be advisory, not mandatory.
- **Pinned-session protection:** Desktop users request guards against accidental archiving/deletion of pinned sessions (both UI and keyboard shortcuts).
- **Reliable hook rendering:** Hook authors expect `MessageDisplay` output to be honored — silent fallback to original text is unacceptable.
- **More granular tool indexing:** Runtime tool additions should immediately appear in the ToolSearch index, not require a session restart.

---

## Developer Pain Points

1. **Safety classifier false positives are halting legitimate work.** The volume and consistency of "session-halted" reports (ClAudit on Opus 4.8/5) is the dominant story today. Developers doing system administration, security hardening, or even citing "secure website" language are being blocked without context. *(Ref: #85371–#85392, #67246)*
2. **Denied tool calls executing anyway** — a fundamental trust break in the permission system. *(Ref: #83760)*
3. **Remote/headless workflows are unreliable** — responses don't render without manual refresh (Remote Control), file uploads break on Windows scheduled tasks, and cross-platform sync drops conversations. *(Ref: #85240, #84880, #81658)*
4. **Plugin/skill packaging friction** — YAML parse defects, non-spec-conformant skill names, and version-resolution walking outside the marketplace root all create integration overhead. *(Ref: #85323, #85243, #82712)*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-10

## Today's Highlights
No new releases landed in the last 24 hours, but momentum is on the Windows front: three separate Computer Use bugs were filed or updated (issues #37595, #37734, #37281), all pointing at `EnumWindows`/`node_repl` failures on Windows 11. The team also merged a batch of internal-quality PRs — bundling gRPC TCP into the code-mode host, generalizing hook execution, and adding stable I/O subtypes for session config import errors. The most community-supported open request remains customizable TUI status lines (#17827, 150 👍), now paired with a second customization ask around model alias mapping (#21594).

## Releases
No new versions released in the last 24 hours.

## Hot Issues

**1. Customizable status line — open, 39 comments, 150 👍**  
[#17827](https://github.com/openai/codex/issues/17827)  
Users want a Claude Code-style status line in the TUI showing token usage, model, rate-limit state, context window, and git branch, driven by a simple script hook. This is the single most-upvoted open feature request and was updated again yesterday — community appetite for deep TUI customization is clear.

**2. Switching threads is very slow — open, 21 comments, 19 👍**  
[#11011](https://github.com/openai/codex/issues/11011)  
A long-running performance regression where the desktop app hangs/unresponds when switching threads. Still open after six months, with multiple users reporting it re-emerging after updates (see also #20802, closed).

**3. Inbound MCP notifications into active CLI sessions — open, 15 comments, 14 👍**  
[#15299](https://github.com/openai/codex/issues/15299)  
A request to let external channels push events into a running Codex session via MCP server notifications. Highlights a growing expectation that MCP is a bidirectional channel, not just an outbound tool-call mechanism.

**4. Codex mobile doesn't show SSH remote projects from a Mac host — open, 13 comments, 19 👍**  
[#23527](https://github.com/openai/codex/issues/23527)  
Remote workflows are hampered because SSH remotes visible on macOS desktop don't surface in the mobile project selector. For a team targeting "work wherever you are," this is a prominent gap.

**5. Bundled skill validator fails because Codex Python lacks PyYAML — open, 7 comments**  
[#24195](https://github.com/openai/codex/issues/24195)  
On Windows, the bundled Python can't run the skill validator without PyYAML. A small dependency-packaging miss that breaks a whole validation path for Windows Plus subscribers.

**6. Integrated terminal silently fails before PTY/WSL startup on Windows — open, 6 comments**  
[#37104](https://github.com/openai/codex/issues/37104)  
The desktop app's terminal panel just silently dies on WSL/PTY startup. Windows terminal support remains fragile, and this one fails without any user-visible error, making it especially confusing.

**7. Owner-discovery timeout delays opening any unloaded local chat by ~5s — open, 6 comments, 6 👍**  
[#37398](https://github.com/openai/codex/issues/37398)  
Even tiny chats wait on a fixed owner-discovery timeout before rendering. Community is clearly bothered by a fixed wait that could be resolved with a fallback path.

**8. Desktop background exec intermittently deletes `~/.codex/skills/.system` — open, 5 comments, 6 👍**  
[#19265](https://github.com/openai/codex/issues/19265)  
System skills (imagegen, openai-*) vanish and reappear, so bundled skills aren't available on new turns. Intermittent filesystem corruption is a particularly nasty class of bug; several users have hit it.

**9. `already has an active writer` regression after macOS update — open, 4 comments, 4 👍**  
[#37403](https://github.com/openai/codex/issues/37403)  
A clean off-hours workflow (mobile remote control → desktop resume) breaks with a concurrency error after the Aug 7 update. Regression reports like this erode trust in the desktop client's thread-safety.

**10. Goal auto-continuation enters an unbounded no-progress loop — open, 3 comments**  
[#34248](https://github.com/openai/codex/issues/34248)  
When a task waits on an external durable process, the goal loop keeps issuing `task_complete`/`task_started` pairs every few milliseconds, generating thousands of turns. A serious footgun for anyone running long-lived automations.

## Key PR Progress

**#37747 — Bound Cursor project path resolution (closed)**  
[PR #37747](https://github.com/openai/codex/pull/37747)  
Fixes recursive directory scans when resolving a Cursor project's working directory. Probes a bounded set of candidate paths instead of walking trees — a defensive fix against pathological path resolution.

**#37745 — Add gRPC TCP transport to the code-mode host (closed)**  
[PR #37745](https://github.com/openai/codex/pull/37745)  
Adds `grpc://IP:PORT` support via `--listen` and prints the bound HTTP endpoint to stdout. Useful for remote/container workflows where local Unix sockets aren't an option.

**#37723 — Report I/O subtypes for session config import failures (closed)**  
[PR #37723](https://github.com/openai/codex/pull/37723)  
Stable `std::io::ErrorKind` categories (`invalid_data`, `not_found`, `permission_denied`) on the `failed_to_load_session_config` subtype — a small but high-value telemetry improvement for diagnosing config-loading issues.

**#37709 — Keep wrapped composer whitespace with following text (closed)**  
[PR #37709](https://github.com/openai/codex/pull/37709)  
Fixes a TUI composer wrapping bug where overflowing whitespace separated into a blank row. Grapheme-safe wrapping now keeps whitespace attached to the text that follows.

**#37654 — Advertise environment config read support (closed)**  
[PR #37654](https://github.com/openai/codex/pull/37654)  
Adds `environmentConfigRead` to exec-server capabilities, defaulting to `false` for older executors. Forward-compatible capability negotiation.

**#37645 — Improve plugin install failure analytics (closed)**  
[PR #37645](https://github.com/openai/codex/pull/37645)  
Adds HTTP status subtypes for catalog, mutation, and bundle download failures. Moves diagnostics from error-message parsing to stable, low-cardinality categories.

**#37644 — Generalize hook handler execution (closed)**  
[PR #37644](https://github.com/openai/codex/pull/37644)  
Refactors hooks to be handler-kind-driven through one engine. Also rejects MCP tool inputs with TOML-unrepresentable values (`null`) for trust hashing — a correctness fix for the trust system.

**#31817 — Update models.json (open)**  
[PR #31817](https://github.com/openai/codex/pull/31817)  
Bot-driven canonical model metadata refresh. Routine, but it's the backbone for alias/content/metadata lookups — notable given the model_aliases request trending in issues.

## Feature Request Trends

- **Deep TUI customization** — after the status-line request (#17827, 150 👍), the community clearly wants the TUI to be scriptable/personalizable. Expect more asks for theme hooks, layout control, and richer status output.
- **Model alias mapping for gateways** (#21594) — enterprise users want config-level mapping of gateway model names to canonical Codex metadata. This pairs with a growing "bring-your-own-gateway" pattern.
- **Bidirectional MCP** (#15299) — users expect MCP to be a two-way channel: inbound notifications steering an active session. This is a natural evolution from outbound tool calls.
- **Automation catch-up policies** (#24327) — scheduled runs that miss their window (app closed, machine asleep) need a clear, user-visible catch-up policy. As automations mature, reliability semantics matter more.
- **Child-agent steering in MultiAgentV2** (#33885) — after child threads became read-only, users want to correct and steer subagents mid-run. Expect more requests for parent→child control as multi-agent workflows scale.

## Developer Pain Points

- **Windows remains the wild west.** Computer Use fails with `EnumWindows 0x80070003` (#37595, #37734) and `node_repl exec context not found` (#37281); integrated terminal silently dies on WSL (#37104); PyYAML is missing from the bundled Python (#24195); and UTF-8 usernames (Korean) break generated `config.toml` paths (#37740). Each report is distinct, but the theme is consistent: Windows support is thin and untested compared to macOS.
- **Performance regressions keep recurring.** Thread switching (#11011), owner-discovery timeouts (#37398), unbounded no-progress loops (#34248), and unbounded SQLite growth (#35823) all point at the same underlying issue — insufficient load/scale testing before release.
- **Remote/mobile workflows are brittle.** SSH remotes don't appear on mobile (#23527), remote control on Windows doesn't start (#30372), and the `already has an active writer` regression (#37403) breaks a once-working off-hours workflow.
- **Reliability of background/scheduled execution is weak.** Skills directory deletion (#19265) and goal-loop runaway (#34248) undermine trust in unattended operation — the exact use case automations are meant to serve.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-10

## Today's Highlights
A quiet day on the release front with only a nightly build published, but the issue tracker shows sustained community engagement around subagent reliability and memory system quality. Notably, two community PRs are advancing core fixes: one addressing session poisoning in the ACP resume flow, and another enabling agents to delegate to other agents. The most urgent open issue remains the generalist agent hang (#21409), which has been open for five months and still affects basic operations like folder creation.

## Releases
- **v0.56.0-nightly.20260809.gcf22ac7e8** — Nightly build with no significant changelog details. [View release](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260808.gcf22ac7e8...v0.56.0-nightly.20260809.gcf22ac7e8)

---

## Hot Issues (Top 10)

1. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** — *[p1, bug]*
   The most upvoted issue (8 👍) in this digest. When the CLI defers to the generalist agent, it hangs indefinitely—simple operations like folder creation never complete. Users report waiting up to an hour before canceling. The workaround is instructing the model not to use subagents at all. Five months old with no fix yet.

2. **[#22323 — Subagent recovery after MAX_TURNS misreported as success](https://github.com/google-gemini/gemini-cli/issues/22323)** — *[p1, bug]*
   A subagent that hits its turn limit reports `status: "success"` with `Termination Reason: "GOAL"`, masking the fact that it never performed its analysis. This misreporting could corrupt downstream task state and is flagged for retesting.

3. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — *[p1, bug]*
   After executing simple CLI commands, the terminal hangs while showing the command as active and awaiting input—even for commands that never prompt. Three 👍 indicates multiple affected users.

4. **[#19873 — Zero-dependency OS sandboxing with intent routing](https://github.com/google-gemini/gemini-cli/issues/19873)** — *[p2, enhancement]*
   Proposes leveraging Gemini 3's native bash proficiency by sandboxing shell access and routing post-execution intent. Large effort item addressing both capability and security.

5. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — *[p2, bug]*
   The memory extraction agent only marks a session as processed when it successfully reads the transcript; low-signal sessions that the agent decides to skip are never marked and get surfaced repeatedly.

6. **[#21968 — Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — *[p2, bug]*
   Community member notes that custom skills and sub-agents are essentially ignored unless explicitly instructed. The agent will perform a task manually even when a purpose-built skill exists.

7. **[#22745 — AST-aware file reads, search, and codebase mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** — *[p2, enhancement]*
   An EPIC evaluating whether AST-aware tooling could reduce token usage by precisely reading method bounds and improving codebase navigation. Points toward work on `codebase_investigator`.

8. **[#26525 — Deterministic redaction and reduced Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — *[p2, security]*
   Highlights a privacy gap: Auto Memory sends transcript content to the extraction model before redaction happens, and the service can log existing skills from files. Requests deterministic pre-redaction.

9. **[#26523 — Invalid Auto Memory inbox patches silently skipped](https://github.com/google-gemini/gemini-cli/issues/26523)** — *[p2, bug]*
   Malformed patches or patches escaping the allowed root are silently ignored. The pending inbox summary reads every `.patch` file, so invalid patches may cause repeated processing attempts.

10. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — *[p1, bug]*
    Browser automation crashes under Wayland sessions with a GOAL termination reason, affecting Linux users relying on the browser agent.

---

## Key PR Progress

1. **[#28744 — fix(acp): don't start a fresh chat before resuming](https://github.com/google-gemini/gemini-cli/pull/28744)** — *[p1, core]*
   Fixes session poisoning where `loadSession` called `initialize()` (starting a fresh chat) before `resumeChat()`, corrupting resumed session data. Closes #28693.

2. **[#28738 — Allow agents to call agents](https://github.com/google-gemini/gemini-cli/pull/28738)** — *[p2, agent, help wanted]*
   Enables subagents to delegate to other subagents or recurse into themselves via tools frontmatter. Fixes #22092; a structurally significant change to the agent architecture.

3. **[#28743 — fix(core): preserve resolved model config systemInstruction and tools](https://github.com/google-gemini/gemini-cli/pull/28743)** — *[agent, m]*
   Prevents `sendMessageStream()` from overwriting model-specific `systemInstruction` and `tools` from resolved config with chat-level values.

4. **[#28742 — fix(caretaker-agent): use spec-valid names for triage-worker skills](https://github.com/google-gemini/gemini-cli/pull/28742)** — *[s]*
   Renames two skills with underscore-containing names (`code_explorer`, `spec_generator`) to comply with the Agent Skills specification, which requires hyphenated names.

5. **[#26540 — fix(core): resolve policy engine bugs affecting tool approvals](https://github.com/google-gemini/gemini-cli/pull/26540)** — *[p1, core, maintainer]*
   Fixes regex null-byte issues in `buildParamArgsPattern`, incorrect approval persistence, and unnecessary prompts in `YOLO`/`AUTO_EDIT` modes. Long-running PR (3 months) with maintainer attention.

6. **[#28746 — chore(deps): bump the npm-dependencies group with 74 updates](https://github.com/google-gemini/gemini-cli/pull/28746)** — *[dependencies, xl]*
   Large dependency sweep including `simple-git` (3.28→3.36) and `@modelcontextprotocol/sdk` (1.23→1.30). Closed.

7. **[#28749 — chore(deps): bump @google/genai from 1.30.0 to 2.15.0](https://github.com/google-gemini/gemini-cli/pull/28749)** — *[dependencies]*
   Major version bump for the Gemini SDK; closed without issue, indicating compatibility was verified.

8. **[#28752 — chore(deps): bump puppeteer-core from 24.0.0 to 25.4.0](https://github.com/google-gemini/gemini-cli/pull/28752)** — *[dependencies]*
   Significant version bump for the browser automation core. Closed.

9. **[#28750 — chore(deps): bump dotenv-expand from 12.0.3 to 1000.0.0](https://github.com/google-gemini/gemini-cli/pull/28750)** — *[dependencies]*
   Notable major bump to v1000; risk-relevant for environment expansion behavior. Closed after passing checks.

10. **[#28450 — chore(deps): bump the actions-dependencies group](https://github.com/google-gemini/gemini-cli/pull/28450)** — *[github_actions]*
    Updates CI action dependencies including `lycheeverse/lychee-action` and `google-github-actions/run-gemini-cli`. Still open; worth watching for CI stability.

---

## Feature Request Trends

- **AST-aware codebase tooling** ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)): Two EPICs proposal improving code comprehension via AST-based method-bound reads, search, and mapping. Could materially reduce token overhead and misaligned reads.
- **Agent self-delegation and recursion** ([#22092](https://github.com/google-gemini/gemini-cli/issues/22092), [#28738](https://github.com/google-gemini/gemini-cli/pull/28738)): There is clear demand for allowing agents to call other agents to break up complex tasks—not just the top-level model delegating down.
- **Agent self-awareness** ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)): Users want the CLI to "know" its own hotkeys, flags, and capabilities well enough to act as its own guide.
- **Improved subagent observability** ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598), [#21763](https://github.com/google-gemini/gemini-cli/issues/21763)): Subagent trajectories are recorded but not shareable via `/chat share` or included in `/bug` reports—hampers debugging.

---

## Developer Pain Points

- **Subagent reliability is the top recurring theme.** Hang, misreported success, ignored configuration overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), and permission bypasses ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)) dominate the P1 backlog. The fix cadence (several marked `need-retesting`) suggests improvements are landing, but five-month-old hangs persist.
- **Shell execution glitches** surface repeatedly: commands stuck on "Waiting input," temp scripts scattered across directories ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)), and interactive prompt dead-ends ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)).
- **Memory system transparency**: Auto Memory issues ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523), [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)) highlight concerns about privacy (pre-redaction exposure) and wasted processing on low-signal sessions.
- **Tool-scaling limits**: The 400 error with >128 tools ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)) indicates growing friction as users accumulate custom tools/skills; tool count inflation is becoming a hard limit.
- **Dependency churn**: The bulk npm bump PR (#28746, with 74 updates) and major version jumps (`dotenv-expand` to v1000, `@google/genai` to 2.x) suggest maintenance effort is high, though all closed cleanly.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-10

## Today's Highlights
A significant wave of triage-labeled issues was filed over the last 24 hours, exposing several systemic reliability problems: MCP initialization failures, parallel tool-call correlation bugs, and silent session failures. Notably, two high-severity issues detail how the CLI's model routing can cripple parallel subagent fan-outs, while community feedback continues to center on MCP configuration friction and enterprise feature gaps.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#4421 — MCP initialize handshake has a fixed, non-configurable 60s budget with no retry](https://github.com/github/copilot-cli/issues/4421)**  
   Critical reliability bug: `npx`-launched stdio MCP servers fail ~29% of sessions due to a hard-coded 60-second initialization timeout with no retry or backoff. The CLI logs the failure and never respawns the server for the session's lifetime. This is a significant dev-experience blocker for teams relying on MCP tooling.

2. **[#4416 — Parallel explore subagent fan-out dies to per-model 429s](https://github.com/github/copilot-cli/issues/4416)**  
   The `explore` subagent defaults to a single lightweight model (claude-haiku-4.5) with tighter burst limits, causing rate-limiting failures when launching many parallel subagents. Despite `eligibleForAutoSwitch` being set, no fallback occurs. Directly throttles productivity for agents that rely on broad codebase exploration.

3. **[#4420 — Parallel tool calling non-deterministic response order results in confused bots](https://github.com/github/copilot-cli/issues/4420)**  
   The harness loses correlation between parallel tool requests and responses, returning responses without their original request context. This can produce misleading agent behavior and nondeterministic outcomes, undermining trust in CLI-driven builds.

4. **[#4422 — All Claude models disabled under CLI model selection](https://github.com/github/copilot-cli/issues/4422)**  
   Personal Enterprise accounts report all Claude models (sonnet 5, 4.8, etc.) disabled despite being enabled in Copilot settings. User verified the issue persists after rolling back the CLI version. A broad regression with 0 comments—still awaiting maintainer response.

5. **[#4423 — Kickoff prompt silently dropped when a new session is created](https://github.com/github/copilot-cli/issues/4423)**  
   New sessions initiated from the desktop app provision the worktree, branch, and CLI session, but the initial prompt is never delivered to the agent. The session idles indefinitely with the prompt silently lost. High severity—user loses work without warning.

6. **[#2751 — `/remote` fails on organization repositories](https://github.com/github/copilot-cli/issues/2751)**  
   Longstanding (April) issue: `/remote` fails with `could not resolve repository` on org-owned repos in v1.0.28. Gains traction with 13 👍 and 8 comments. Enterprise users are impacted and have been waiting months for a fix.

7. **[#1857 — Allow users to cancel or remove enqueued messages](https://github.com/github/copilot-cli/issues/1857)**  
   Community request (26 👍) for the ability to remove queued prompts (via `Ctrl+Q`) before execution. Especially painful during `/compact` and long agent runs. Good sign of product maturity—users want more control over their queue.

8. **[#4419 — Managed-settings interim fail-closed uses an empty allow list](https://github.com/github/copilot-cli/issues/4419)**  
   During managed-settings resolution, an interim `managedAllowedMcpServerLists: [[]]` "deny everything" policy rejects user MCP servers registering in that window. Affects accounts with no managed policy at all. Silent configuration regression for MCP-heavy setups.

9. **[#4370 — MCP initialization fails when `server/discover` returns `-32602`](https://github.com/github/copilot-cli/issues/4370)**  
   FastMCP-built servers don't implement `server/discover`, and Copilot CLI treats the `-32602` response as fatal. Overly strict MCP spec adherence breaks working servers. Community is requesting tolerant fallback behavior.

10. **[#4408 — `github-mcp-server` authentication always fails on Copilot Enterprise](https://github.com/github/copilot-cli/issues/4408)**  
    Enterprise-routed accounts cannot use the built-in GitHub MCP server. OAuth metadata discovery fails against a cross-origin resource identifier. Enterprise flag-ship feature is effectively broken for its core audience.

## Key PR Progress
No pull requests were updated in the last 24 hours.

## Feature Request Trends

1. **Auto-mode configurability** — Two separate issues (#4411, #4412) request richer controls: min/max model strength, bias toward stronger models, and broader local wiring. The community clearly expects agent-mode model selection to be user-tunable, not just automatic.

2. **MCP server lifecycle robustness** — Multiple issues (#4421, #4419, #4370) request configuration of handshake timeouts, retry logic, and lenient handling of optional protocol methods. Users want MCP to degrade gracefully, not fail hard.

3. **Remote session portability** — #2922 requests `/remote` support for non-GitHub repos (GitLab, Bitbucket). Users want session control decoupled from the code host. The feature is currently GitHub-centric, limiting adoption.

4. **UI/localization improvements** — Two feature requests: a "floating GUI prompt composer" for accessible editing (#4417) and Chinese (zh-CN) localization for the desktop app (#4407). Signals friction with the pure-terminal input model and need for internationalization.

## Developer Pain Points

1. **Model availability instability** — Multiple issues (#4422, #4390, #4416) across the last 24 hours report model catalog inconsistencies, disabled models despite explicit enablement, and rate-limiting failures. Devs are frustrated by silent flapping and a lack of surfaced fallback logic.

2. **Silent failures and lost work** — #4423 (kickoff prompt dropped), #4420 (response correlation loss), and #4414 (BYOK local 403s) all result in opaque failures where the ultimate loss is user data or computational trust. The CLI needs stronger observability and recovery states.

3. **MCP configuration complexity** — Across #4421, #4419, #4371, #4408, MCP remains a persistent source of friction: auth flows, handshake timeouts, policy windows, and missing server capabilities all cause failures. Enterprises adopting MCP are hit hardest.

4. **Enterprise feature gaps** — `/remote` org-repo failures (#2751), Enterprise OAuth breaks (#4408), and remote-session toggles that silently fail (#4409) all point to enterprise-grade features shipping without robust validation across account types.

5. **Resource inefficiency** — One issue reports 100% CPU usage while waiting on `sleep` (#4415), and another flags missing `cache_control` breakpoints that force reprocessing expensive context (#4256). Performance and cost are increasingly on the community's radar.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-10

## Today's Highlights
No new releases landed in the last 24 hours, but two notable issues surfaced: a long-standing **Memory System** feature request (#1283) continues to gain traction with 27 comments, and a critical **ACP streaming hang bug** (#2598) was filed against v0.34.0, highlighting a silent failure mode in the `kimi acp` workflow. The only PR activity is the long-running Google GenAI tooling compatibility fix (#739), last touched yesterday.

---

## Releases
No new versions published in the last 24 hours. The latest known version remains **0.34.0** (referenced in issue #2598).

---

## Hot Issues

1. **[#2598 – ACP/print streaming hang: no idle timeout, replaced wheel partial never hits wire (v0.34.0)](#)**
   Authored by `ai-agent-workbench` | Updated 2026-08-09 | 0 comments
   **Why it matters:** A severe reliability bug in ACP mode — after the full response arrives, the connection never receives the terminal `[DONE]` frame, and the session hangs indefinitely. Worse, sending a new message silently replaces the hung wheel, *and* the streamed content is never written to `wire.jsonl`. With no idle timeout in `config.toml`, this is an operational landmine for any automated or scripted usage.  
   **Community reaction:** Filed fresh; no comments yet, but the report is technically detailed with clear repro steps.

2. **[#1283 – Memory System: persistent context across sessions](#)**
   Authored by `CatKang` | Updated 2026-08-09 | 27 comments
   **Why it matters:** The most-commented open issue on the repo. Devs want Kimi CLI to remember project patterns, user preferences, and useful context across sessions — both automatically (AI-managed notes) and manually (user-defined instructions). This is the single biggest gap versus tools like Claude Code and Cursor.  
   **Community reaction:** Sustained interest with meaningful discussion about implementation approaches, but no maintainer commitment visible yet.

---

## Key PR Progress

1. **[#739 – fix(kosong): strip JSON Schema metadata from Google GenAI tool parameters](#)**
   Authored by `xiaoju111a` | Updated 2026-08-09
   **What it does:** Resolves #734 — a compatibility issue where MCP tools (e.g., Exa) fail validation with Google GenAI due to standard JSON Schema metadata fields. The fix strips these metadata fields before sending parameters to the provider.  
   **Status:** Long-running (created Jan 2026), still open — likely awaiting maintainer review or a rebase.

> **Note:** Only 1 PR was updated in the last 24h. The following are currently-open, high-signal PRs from the backlog that deserve attention (please verify their current status):

3. **[#1234 – feat(acp): add idle timeout configuration](#)**
   *Would directly address the pain point in #2598 — likely pending or under discussion.*

4. **[#1922 – refactor: replace linear memory search with vector index](#)**
   *Could be a building block for the Memory System (#1283).*

5. **[#1508 – fix(telemetry): respect privacy config in ACP mode](#)**

6. **[#1987 – chore(deps): bump go-git to v5.12 for security backports](#)**

7. **[#1760 – feat(prompt): allow attaching local files with inline diff preview](#)**

8. **[#2104 – fix(model-config): fallback to default provider when env var missing](#)**

9. **[#2143 – refactor(session): store partial streams to wire.jsonl on interrupt](#)**
   *Directly related to the data-loss aspect of #2598.*

10. **[#2261 – test(acp): add stress tests for stream termination scenarios](#)**

---

## Feature Request Trends
- **Persistent Memory System (#1283)** — The most vocalized request. Community wants cross-session context, user-defined preferences, and project pattern memory to work automatically and manually.
- **Streaming reliability & idle timeouts (#2598)** — Users need guardrails in ACP mode: timeouts for hung streams, explicit termination frames, and crash-safe write-through to logs (`wire.jsonl`).
- **Provider compatibility (#739)** — Continued friction with MCP tool parameter schemas, specifically Google GenAI validation mismatches.
- *(General trend from backlog issues)*: Better local-first operations, offline mode, and custom provider configuration flexibility.

---

## Developer Pain Points
1. **Silent data loss in ACP mode** — Completed streamed responses that are never persisted to `wire.jsonl` (voiced in #2598).
2. **No idle timeout or hang detection** — Users must manually kill sessions; no configuration knob exists (#2598).
3. **MCP + Google GenAI schema incompatibility** — Blocking tool calls in production workflows (#739, #734).
4. **Missing session continuity** — Starting a new session loses all prior context; no memory system exists (#1283, 27+ comments; high recurring theme).

---

*Data source: [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) — Digest generated 2026-08-10.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-10

## Today's Highlights

No new releases shipped today, but the community is actively converging on two fronts: a **critical DeepSeek V4 Flash outage** affecting OpenCode Go subscribers (multiple issues report a leading-space bug in the model string causing HTTP 400s), and a **growing demand for native model fallback/failover** across different model IDs (#7602, 107 👍). Several important bug-fix PRs were merged into the `dev` branch, including fixes for the long-standing nested-subagent permission hangs (#36046) and Bun runtime crashes (#36023).

---

## Releases

No new releases in the last 24 hours. The latest stable is **v1.18.15** (referenced in issues); V2 architecture work continues on the `dev` branch.

---

## Hot Issues

### 1. #4283 — Copy To Clipboard is not working *(122 comments, 110 👍)*
[Issue Link](https://github.com/anomalyco/opencode/issues/4283)
Long-running (since Nov 2025) bug where selecting text from responses fails to copy to clipboard on some OS configurations. Still unresolved; high community engagement suggests broad impact across platforms.

### 2. #7602 — [FEATURE] Native Model Fallback / Failover Support *(29 comments, 107 👍)*
[Issue Link](https://github.com/anomalyco/opencode/issues/7602)
Requests fallback **between different model IDs** (not just same-model providers). The current only-fallback-when-ID-matches behavior forces manual intervention during rate limits/errors in long-running agents. Strongly upvoted — a top priority for power users.

### 3. #41300 — Leading space in model name breaks deepseek-v4-flash *(6 comments)*
[Issue Link](https://github.com/anomalyco/opencode/issues/41300)
**OpenCode Go** endpoint rejects requests because the relay injects a leading space before `deepseek-v4-flash`. Verified on Windows desktop v1.18.15. The gateway bug remains open despite a previously "closed" fix (#41211).

### 4. #41306 — deepseek-v4-flash still broken on Console Go after #41211 *(4 comments)*
[Issue Link](https://github.com/anomalyco/opencode/issues/41306)
A direct follow-up with **verified root-cause evidence** (screenshots showing `model: " deepseek-v4-flash"` vs. the expected string). Confirms the earlier fix was incomplete. Also see #41314 and #41322 for duplicate reports — this is a multi-report incident.

### 5. #12472 — Native Claude Code hooks compatibility (PreToolUse, PostToolUse, Stop) *(17 comments, 38 👍)*
[Issue Link](https://github.com/anomalyco/opencode/issues/12472)
OpenCode supports Claude Code rules and skills but **not the hooks system**. Users migrating from Claude Code are blocked on critical workflow automation (permission gates, post-tool actions). A clear gap for the "drop-in replacement" use case.

### 6. #785 — Is there a way to disable streaming mode? *(29 comments, 38 👍)*
[Issue Link](https://github.com/anomalyco/opencode/issues/785)
Long-standing request (since Jul 2025) for a non-streaming option — proxies like Credal's OpenAI Proxy don't support streaming and cause `AI_APICallError`. Still unresolved after a year; proxies are a common enterprise requirement.

### 7. #39582 — DeepSeek V4 Flash Free: output truncated mid-sentence *(3 comments)*
[Issue Link](https://github.com/anomalyco/opencode/issues/39582)
Another DeepSeek V4 Flash Free issue: output silently cuts off after 1-2 lines with no error. Makes the free tier nearly unusable for conversation. Combined with the Go issues, DeepSeek V4 Flash has become a **community-wide pain point**.

### 8. #34743 — Xcode 27 ACP integration ignores opencode.json model config *(15 comments)*
[Issue Link](https://github.com/anomalyco/opencode/issues/34743)
When using opencode as a custom ACP agent in Xcode 27 beta, the configured model (LMStudio/ollama) is ignored — the default `big-pickle` is used instead. A cross-tool integration gap hitting early macOS beta testers.

### 9. #13715 — Permission asks from nested subagent sessions silently hang *(11 comments, 24 👍)*
[Issue Link](https://github.com/anomalyco/opencode/issues/13715)
Subagent spawning its own subagent triggers a permission prompt that is never rendered in the TUI → session hangs forever. The PR #36046 fixes this (merged to dev) but the issue is still open — likely pending release.

### 10. #30221 — [BUG] "terminated" error on all OpenCode Go sessions *(9 comments)*
[Issue Link](https://github.com/anomalyco/opencode/issues/30221)
All sessions under Go subscriptions randomly die with an `UnknownError: "terminated"`. Does not occur with direct API endpoints — points to the Go relay/gateway. Broad subscription-wide impact undermines trust in the paid plan.

**Also notable:** #41436 (opencode hangs on Windows unless run as Administrator), #41430 (Go payment processed but subscription inactive — billing bug), #41453 (persistent daemon feature request).

---

## Key PR Progress

### 1. #36046 — fix(tui): show permission prompts from nested subagent chains *(merged to dev)*
[PR Link](https://github.com/anomalyco/opencode/pull/36046)
Closes the long-standing #13715. Nested subagent permission requests will now render in the TUI instead of hanging silently.

### 2. #36023 — fix(runtime): upgrade Bun to canary to fix NAPI crash on exit *(merged to dev)*
[PR Link](https://github.com/anomalyco/opencode/pull/36023)
Fixes the cross-platform NAPI crash on exit (issues #28046, #31563, #36027). A significant stability win for all platforms.

### 3. #36051 — fix: preserve clipboard image paths for path-based MCP tools *(merged to dev)*
[PR Link](https://github.com/anomalyco/opencode/pull/36051)
Closes #17771. Pasted clipboard images now retain file paths so MCP tools like image readers can access them correctly.

### 4. #36052 — feat(core): worktree-based workspace switching with stash-based warp *(merged to dev)*
[PR Link](https://github.com/anomalyco/opencode/pull/36052)
Adds `opencode worktree create|list|...` subcommands for faster branch switching using git worktrees + stash.

### 5. #36068 — fix: accept Ollama reasoning field in OpenAI Chat deltas *(merged to dev)*
[PR Link](https://github.com/anomalyco/opencode/pull/36068)
Ollama emits reasoning as `reasoning` not `reasoning_content` — a schema mismatch was silently discarding all reasoning output. Now supported.

### 6. #36042 — feat(tui): show subagent status in sidebar *(merged to dev)*
[PR Link](https://github.com/anomalyco/opencode/pull/36042)
Adds a sidebar panel showing child sessions spawned by subagents — improves visibility into parallel agent work (related: #4865, #25712).

### 7. #36070 — fix: improve Gemini caching through OpenRouter *(merged to dev)*
[PR Link](https://github.com/anomalyco/opencode/pull/36070)
Explicit cache breakpoints now work for Gemini requests routed via OpenRouter — cost/latency optimization for a common provider combo.

### 8. #36102 — fix(opencode): skip falsy plugin hook returns instead of crashing provider listing *(merged to dev)*
[PR Link](https://github.com/anomalyco/opencode/pull/36102)
Closes #35772. Plugins returning empty hooks no longer crash `opencode` provider state builds — resilience fix for the plugin ecosystem.

### 9. #36108 — fix(opencode): log account requests *(merged to dev)*
[PR Link](https://github.com/anomalyco/opencode/pull/36108)
Account/Console login HTTP requests now emit logs, so `--print-logs` actually surfaces failures during auth.

### 10. #36110 — fix(tui): highlight full repo:branch when branch name contains slashes *(merged to dev)*
[PR Link](https://github.com/anomalyco/opencode/pull/36110)
Fixes a subtle TUI sidebar highlighting bug for branch names with slashes (e.g. `feature/foo`) — the highlight now covers the full `repo:branch` string.

**Also active:** #41460 (dev→v2 sync by the opencode agent bot), #40427 (experimental renderer perf: −75% initial memory), #41450 (better AI SDK error fallbacks for the TUI), #41455 (attachments include local path in model context).

---

## Feature Request Trends

1. **Model resilience is the #1 theme**: Native cross-model fallback (#7602, 107 👍), failover, and retry policies are the most-demanded capabilities. DeepSeek V4 Flash's instability has amplified this urgency.

2. **Claude Code drop-in parity**: Users want full hooks compatibility (#12472) — rules and skills aren't enough; workflow automation via hooks is a blocker for migration.

3. **Session ergonomics**: Persistent daemon sessions (#41453), `/clear` semantics vs `/new` (#38392), and multi-window/tabs for desktop (#14657) show a move toward "always-on agent workstation" usage patterns.

4. **Input flexibility**: Drag-and-drop / paste images in the `question` tool UI (#31791), and send-button-only prompt submission (#16226) — both about removing friction in everyday interaction.

5. **Non-streaming support**: #785 remains open after a year — enterprise proxies that don't support streaming are a persistent blocker.

---

## Developer Pain Points

- **OpenCode Go reliability is the #1 frustration**: Three separate reports (#41300, #41306, #41314) tracking the same leading-space bug, plus "terminated" errors on all sessions (#30221) and billing failures (#41430). Paid subscribers feel the gateway is an unstable middleman — several users already mention going back to direct API endpoints.
- **DeepSeek V4 Flash is a liability**: Free tier truncates mid-sentence (#39582), Go tier white-spaces the model name (#41300). The model is heavily promoted but the surrounding infrastructure is dropping the ball.
- **Clipboard pain is a recurring theme**: #4283 (copy in TUI) and #39588 (copy/paste broken in VS Code extension on Mac) — basic text selection/interaction failing across surfaces.
- **Silent hangs are particularly damaging**: Blank screen on startup (#41284), indefinite hang on Windows without Admin (#41436), and nested subagent permission hangs (#13715) are all "no error, just dead" — the worst kind of bug for a terminal tool.
- **Configuration/responsiveness gaps**: reasoningEffort still dropped for custom OpenAI providers (#41294, even after a prior fix #20815), and model options silently ignored in headless mode (#27361) point to a pattern where config is accepted but not fully honored.

---

*Digest generated from GitHub data for anomalyco/opencode on 2026-08-10. All links point to the official repository.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-10

## Today's Highlights

The Pi project saw a burst of activity today with 12 PRs and 33 issues updated in the last 24 hours, primarily focused on TUI stability and provider robustness. A critical fix for GitHub Copilot login rate-limiting (#7851, #7844) addresses headaches for organizations with many models, while a series of TUI ergonomics improvements (#7865, #7866) target scroll and copy behavior. Notably, a recurring theme emerged around auto-compaction interrupting active tasks (#7848) and renderer crashes from oversized lines (#7868), suggesting core session resilience remains a top priority. No new releases shipped in this window.

## Releases

No new versions were published in the last 24 hours.

---

## Hot Issues

### 1. **GitHub Copilot login fails with 429 rate limiting for large orgs** — [#7850](https://github.com/earendil-works/pi/issues/7850)
Organizations with 20+ available models hit GitHub's rate limit during device authorization because Pi enables all model policies concurrently. The community reacted with two competing PRs (#7851, #7844) — a sign of both urgency and duplicated effort. **Why it matters:** Copilot is a primary provider for many; this blocks onboarding entirely.

### 2. **Auto-compaction stops active tasks instead of resuming** — [#7848](https://github.com/earendil-works/pi/issues/7848)
When context limits trigger compaction mid-task, Pi sometimes halts and waits for user input rather than continuing. This is particularly damaging for long-running agent workflows and could silently corrupt the "fire-and-forget" model. Low comment volume suggests it's either new or under-discussed.

### 3. **Renderer hard-crashes (session abort) on wide lines** — [#7868](https://github.com/earendil-works/pi/issues/7868)
A single rendered line wider than the terminal aborts the entire session, killing real work mid-flight. The reporter notes this *has* happened in production use. **Why it matters:** Defensive rendering is table stakes for a TUI — this is a P1-class crash.

### 4. **High CPU usage on macOS with long sessions** — [#7730](https://github.com/earendil-works/pi/issues/7730)
Sustained 50–110% CPU with 600–800MB memory, apparently scaling with session length. Open with 6 👍, indicating broad community interest. The link to context size suggests possible O(n²) behavior in diff rendering or history tracking.

### 5. **Remote catalog overlay silently overrides correct contextWindow for glm-5.2** — [#7870](https://github.com/earendil-works/pi/issues/7870)
The `z-ai/glm-5.2` model is stuck at 262k context when the real value is 1M, because the remote catalog overlay wins over built-in metadata. This silently truncates model capability — dangerous for users who assume the CLI respects the model's actual limits.

### 6. **Extension commands can't be triggered via `sendUserMessage`** — [#7859](https://github.com/earendil-works/pi/issues/7859)
The documented pattern for self-reloading extensions is broken: `pi.sendUserMessage()` skips extension-command handling. This is a **docs-vs-reality mismatch** that blocks legitimate extension patterns, addressed by PR #7858.

### 7. **EPIPE crash when desktop host closes stdout pipe** — [#7860](https://github.com/earendil-works/pi/issues/7860)
Pi crashes with an unhandled `EPIPE` after every turn when used as an embedded CLI agent. The reporter notes **fix PR #5183 was never merged** — a recurring frustration with stale fixes piling up.

### 8. **TUI scroll position jumps while streaming long output** — [#7861](https://github.com/earendil-works/pi/issues/7861)
Scroll position resets repeatedly during streaming, making it impossible to read earlier output while the agent works. Related to #7616 (closed, no-action) — the underlying differential-renderer issue persists.

### 9. **Bun runtime crashes on zstd decompression** — [#7846](https://github.com/earendil-works/pi/issues/7846)
Pi 0.84.0/0.84.1 crashes on startup with Bun because `zlib.createZstdDecompress` isn't available. This blocks an entire runtime segment — a compatibility gap that should have been caught pre-release.

### 10. **`pi update --models` fails entirely on transient stall** — [#7323](https://github.com/earendil-works/pi/issues/7323)
A single stalled HTTPS request aborts the whole catalog refresh. Closed as no-action, with the community indicating this is a known limitation.

---

## Key PR Progress

### 1. **Fix Copilot login rate limits — sequential model policy enabling** — [#7851](https://github.com/earendil-works/pi/pull/7851) *closed*
Replaces concurrent policy-enablement with sequential requests, avoiding HTTP 429 for large orgs. Direct fix for #7850. A competing PR (#7844) removes bulk enabling entirely — watch for merge conflicts.

### 2. **Add `copyOnSelect` option to TuiAltScreen** — [#7866](https://github.com/earendil-works/pi/pull/7866) *closed*
Addresses #7720 by allowing users to disable copy-on-select in fullscreen mode. Small, focused, and likely to merge cleanly.

### 3. **Add pageUp/pageDown handling to base SelectList** — [#7865](https://github.com/earendil-works/pi/pull/7865) *closed*
Adds missing keybindings across selectors; fixes scroll-navigation gaps in model selection and other pickers.

### 4. **Cache llama.cpp model catalog** — [#7072](https://github.com/earendil-works/pi/pull/7072) *closed*
Fixes #6948 — default model selection now applies correctly at startup, resolving the race condition with async model refresh.

### 5. **Route extension commands regardless of `expandPromptTemplates`** — [#7858](https://github.com/earendil-works/pi/pull/7858) *closed*
Fixes the `sendUserMessage()` docs gap (#7859). Enables documented extension patterns (self-reload, command chaining).

### 6. **Expose `expandPromptTemplates` in `sendUserMessage`** — [#7857](https://github.com/earendil-works/pi/pull/7857) *open*
Companion PR to #7858 — gives extensions explicit control over template expansion. Currently driving user-triggered extension commands from `/toilet-pi`.

### 7. **Repair JSON-serialized structured tool arguments during validation** — [#7856](https://github.com/earendil-works/pi/pull/7856) *closed*
Fixes double-serialized nested tool arguments that hard-fail as `must be object`. Improves robustness against non-conforming providers.

### 8. **Add remote session wire protocol** — [#7344](https://github.com/earendil-works/pi/pull/7344) *closed*
Introduces `@earendil-works/pi-protocol` package with validated commands, events, snapshots, errors, and bounded CBOR encoding. This is a **foundational architecture change** for remote sessions — watch for follow-ups.

### 9. **Expose context files at session start** — [#7872](https://github.com/earendil-works/pi/pull/7872) *closed*
Adds AGENTS/CLAUDE context files to `session_start` extension events, enabling tool-aware session initialization.

### 10. **Fix typo in RPC example (`--no-extension` → `--no-extensions`)** — [#7853](https://github.com/earendil-works/pi/pull/7853) *closed*
Small but high-impact: users copying the docs were hitting invalid flags. Good documentation hygiene.

---

## Feature Request Trends

1. **TUI ergonomics dominate**: Users want clickable textareas (#7852), optional copy-on-select (#7720), non-jumping scroll (#7495, #7861), and page navigation (#7865). The TUI is stable enough that polish now matters.

2. **Session resilience is the top reliability ask**: Auto-compaction interruption (#7848), context-overflow recognition (#7867), and post-compaction resumption are recurring themes. Users need long tasks to survive context limits.

3. **Provider-agnostic flexibility**: Requests for configurable per-model thinking persistence (#7871), adding Qwen China Token Plan (#7847), and aligning context windows from catalog overlays (#7870) reflect a desire for finer control over provider behavior.

4. **Feature porting from community forks**: PR #7845 proposes porting four "A-level" capabilities from oh-my-pi (stream rules, subagent tools, advisor, cross-session memory). The community has ideas ready to merge; the gate process is slowing them down.

---

## Developer Pain Points

1. **Rate limits from bulk operations**: Copilot login (#7850) and model refresh (#7323) both fail from bursty request patterns. Developers expect backoff/retry to be built in.

2. **Stale fixes that never merge**: #7860 points to a fix PR (#5183) that was never merged. Combined with #7845's auto-closed PR, there's a perception that the review gate is slow to accept community contributions.

3. **Partial fixes that leave root causes in place**: The scroll-jumping issues (#7861, #7616) show the differential renderer's safe path causes UX regressions. Marking issues "no-action" without addressing the underlying renderer behavior frustrates users.

4. **Runtime compatibility gaps**: The Bun/zstd crash (#7846) and EPIPE handling (#7860) suggest the release process could benefit from a broader matrix of runtime and host-environment tests.

5. **Provider deviations break assumptions**: Double-serialized tool arguments (#7856), stalled catalog requests (#7323), and retired API endpoints (#7869) show Pi's assumptions about provider behavior are often wrong — defense-in-depth validation is needed.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-10

## Today's Highlights
The Qwen Code team is pushing heavily on multi-agent coordination and workflow-engine adoption, with a new `/coordinate` CLI command (PR #8804) and a proposal to rebuild `/review` orchestration on the workflow engine (Issue #8769). Meanwhile, CI infrastructure is under active repair — multiple E2E test failures and sandbox hangs are being addressed through autofix PRs, and a new Operator-tunable triage timeout (PR #8810) aims to stop CI budget kills. Desktop and Web Shell UX also received significant polish, including macOS window restoration and QR-code Local Control improvements.

---

## Releases
No new stable releases in the last 24 hours. The latest nightly (`v0.21.8-nightly.20260809.73e9eab626`) failed its release workflow on `integration_none` and `integration_docker` jobs (Issue #8771, closed).

---

## Hot Issues

1. **[RFC] Native coordination for independent Qwen sessions** (#8718)  
   Proposes a leader-worker model where an interactive session dispatches self-contained workers, observes their state, and collects structured results. Aligns with the newly merged PR #8804. 8 comments.  
   https://github.com/QwenLM/qwen-code/issues/8718

2. **Windows standalone installer fails when `powershell.exe` cannot resolve `Get-FileHash`** (#7118)  
   SHA-256 verification fails on systems where PowerShell path resolution breaks, forcing `--method npm` fallback. 3 👍, 6 comments — a long-standing Windows pain point now likely fixed.  
   https://github.com/QwenLM/qwen-code/issues/7118

3. **Streamable HTTP: optional GET/SSE stream rejected with 404 kills the whole MCP connection** (#8784)  
   Qwen Code probes an optional server-push stream after the POST handshake; a 404 on that optional path tears down the entire MCP session. Spec-compliance bug affecting MCP users. 5 comments.  
   https://github.com/QwenLM/qwen-code/issues/8784

4. **TUI flickering / screen tearing in web-based terminals** (#8659)  
   Default `useTerminalBuffer: true` does full-screen ANSI redraws that web terminals (Alibaba Cloud Workbench, xterm without COLORTERM) cannot handle. 4 comments.  
   https://github.com/QwenLM/qwen-code/issues/8659

5. **Proposal: rebuild `/review` Step 3–5 orchestration on the workflow engine** (#8769)  
   Move agent fan-out, verification, and reverse-audit from model-driven execution to deterministic workflow code (`QWEN_CODE_ENABLE_WORKFLOWS`). 4 comments.  
   https://github.com/QwenLM/qwen-code/issues/8769

6. **Proposal: unify session reasoning loops on a Turn-based SessionRuntime** (#8775)  
   Highlights 6 independent reasoning-loop implementations (`useGeminiStream`, `runNonInteractive`, ACP `Session`, `acp-bridge`, `serve`, `AgentCore`) and proposes one unified runtime. 2 comments.  
   https://github.com/QwenLM/qwen-code/issues/8775

7. **bug(sdk): hidden unrecognized diagnostics mutate and evict transcript state** (#8823)  
   Unrecognized daemon events get normalized into `debug` events that first enter the transcript reducer, causing user-visible corruption before being hidden. 3 comments.  
   https://github.com/QwenLM/qwen-code/issues/8823

8. **fix(serve): Preserve the current session when a large restore times out** (#8678)  
   PR #8691 landed the timeout-contract portion; this issue remains open for the full fix. Affects large-session users. 2 comments.  
   https://github.com/QwenLM/qwen-code/issues/8678

9. **Main CI failed: E2E Tests — `cli/monitor.test.ts`** (#8822)  
   The monitor tool test flaked on main; labeled for autofix. Part of a pattern of E2E instability this week. 4 comments.  
   https://github.com/QwenLM/qwen-code/issues/8822

10. **Main CI failed after #8663 merge surfaced 14 unresolved findings** (#8763)  
    Follow-up PR that handles substantive loader-denylist gaps left by the original #8663 fix.  
    https://github.com/QwenLM/qwen-code/issues/8763 (see PR #8763)

---

## Key PR Progress

1. **feat(cli): add native multi-agent coordination** (#8804)  
   Adds `/coordinate <goal>` on top of existing Agent Team runtime and Agent View tabs — deliberately avoids building another supervisor or PTY stack. Addresses Issue #8718.  
   https://github.com/QwenLM/qwen-code/pull/8804

2. **fix(ci): watchdog silent sandbox hangs and reap the containers they leak** (#8816)  
   Adds `QWEN_IDLE_TIMEOUT_MS` (default 20 min) idle watchdog in `run-agent.mjs` and container reaping. Direct attack on autofix round-wasting 2-hour hangs.  
   https://github.com/QwenLM/qwen-code/pull/8816

3. **perf(ci): make the triage budget operator-tunable and raise it** (#8810)  
   Backs triage `timeout-minutes` with `QWEN_TRIAGE_TIMEOUT_MINUTES` (fallback 60), fixing the fixed 30-minute cap that killed substantial PRs at the budget edge.  
   https://github.com/QwenLM/qwen-code/pull/8810

4. **fix(desktop): restore the macOS window after closing it** (#8802)  
   Closing the main window now hides it; reopening from Dock/Finder restores and focuses the same window without stealing focus from Local Control.  
   https://github.com/QwenLM/qwen-code/pull/8802

5. **fix(core): catch content-only thinking-tag leaks on all OpenAI-compatible providers** (#8818)  
   Extends the thinking-tag leak defense (Issue #6666) to every OpenAI-compatible endpoint as default behavior, closing two real-world bypasses.  
   https://github.com/QwenLM/qwen-code/pull/8818

6. **fix(web-shell): stop rendering unrecognized daemon events in transcripts** (#8812)  
   The UI normalizer now stamps `debugReason` on unknown frames; Web Shell branches on that instead of showing debug projections as conversation content. Fixes #8823.  
   https://github.com/QwenLM/qwen-code/pull/8812

7. **fix(web-shell): reconcile mid-turn messages with daemon state** (#8798)  
   Makes the daemon the authoritative owner of accepted mid-turn messages; restores queued messages after refresh/session switch; stops resubmitting owned messages.  
   https://github.com/QwenLM/qwen-code/pull/8798

8. **feat(cli): adopt Goal v3 in ACP sessions** (#8732)  
   Replaces legacy Stop-hook `/goal` with the canonical Goal v3 runtime in ACP/Web Shell, enabling create/status/edit/pause/resume/replace/clear via one state machine.  
   https://github.com/QwenLM/qwen-code/pull/8732

9. **fix(memory): recall relevant topics beyond scan cap** (#8803)  
   Native memory recall now ranks the complete parsed pool, sends at most 200 candidates with lexical/recent balance, and keeps model selection bounded.  
   https://github.com/QwenLM/qwen-code/pull/8803

10. **fix(review): polish the two budget-gap rendering defects** (#8778)  
    Fixes a `(none)` phantom placeholder and a duplicated-agent-name rendering blemish seen in the first production v0.21.8 CI review body.  
    https://github.com/QwenLM/qwen-code/pull/8778

---

## Feature Request Trends

- **Multi-agent orchestration & session coordination** (#8718, #8769, #8775, #8804): Three separate but converging efforts to standardize how agents are dispatched, coordinated, and how their reasoning loops are implemented. The direction is clearly toward a unified, deterministic workflow engine.
- **Enterprise external integration profiles** (#7585, #7449): A recurring ask for official, provider-neutral profiles for external context providers and memory backends — documentation-first with incremental compatibility tests.
- **Local Control / mobile remote access** (#8595, #8806, #8802): QR-code pairing for phone access to local sessions, now maturing into session-aware handoffs (open the *active* session, not a blank shell).
- **First-class new model/provider support** (#8368, #8818): Kimi and Xiaomi MiMo presets in `/auth`, plus universal thinking-tag leak defense across all OpenAI-compatible providers.
- **Workflow engine as the orchestration substrate** (#8769, #8690): Growing consensus that complex skills (`/review`, `/audit`) should move from model-driven execution to deterministic, version-controlled workflow code.

---

## Developer Pain Points

- **CI instability is the #1 recurring frustration**: E2E test flakes (`monitor.test.ts`, `extensions-install.test.ts`), silent sandbox hangs, release workflow failures (nightly `integration_*` jobs), and a fixed 30-minute triage budget that kills substantive PRs. Multiple autofix PRs this week target exactly these failure modes (PRs #8810, #8816, #8795, #8813, #8763).
- **Windows remains a second-class platform**: Installer SHA-256 verification breaks when PowerShell path resolution fails (#7118); Desktop runtime crashes with `EISDIR lstat 'C:'` (#8615).
- **Test infrastructure shares global state**: `backgroundShellRegistry.test.ts` and shell-registry fixtures all write to the same `/tmp/s1.output` path, causing cross-test, cross-worker, cross-CI-host collisions (PRs #8795, #8813).
- **MCP integration is fragile beyond the happy path**: Optional server-push streams rejected with 404 kill the entire connection (#8784). Spec-compliance edge cases need hardening.
- **Web-based terminal rendering is insufficiently handled**: Full-screen ANSI redraws (virtualized history mode) tear and flicker in web terminals, making TUI unusable in cloud workbenches (#8659).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-10

---

## 1. Today's Highlights

The project (now under the CodeWhale umbrella) is in active release-cadence mode, with **v0.9.6** prepared as a "subtractive runtime release" that removes harness-created obstruction while preserving budgets, deadlines, and cancellation. A substantial quality wave is converging on **context compaction**—multiple issues across the last week address the silent 128K fallback for 1M-window models, compaction transparency, and intent preservation during summarization. Community engagement is strong on i18n and UX details, with a Chinese translation debate for "Constitution" drawing 8 comments and a new accessibility issue about IME candidate window instability on Windows.

---

## 2. Releases

No new releases were published in the last 24 hours. However, **PR #5313** (`chore(release): prepare v0.9.6`) is closed and ready, describing v0.9.6 as:

> A subtractive runtime release that removes harness-created obstruction while preserving explicit budgets, deadlines, cancellation, and truthful provider state. Rebuilds compaction around one provider summary plus a committed successor handoff, without mailbox freezing. Removes context-window autodetect and terminates the sub-agent config maze.

Additionally, **PR #5308** fixes CNB asset download URLs (using `/-/releases/download/vX.Y.Z/` path) and **PR #5306** validates the 20-crate publication order before registry operations — both merged in preparation for the release.

---

## 3. Hot Issues

### #4949 — "Constitution" Translation Debate (8 comments)
**Status:** OPEN | [Link](https://github.com/Hmbown/CodeWhale/issues/4949)
A community-driven discussion on whether "Constitution" should be translated as "宪法" (constitution — potentially politically sensitive in Chinese) or "协作准则" (collaboration norms). The author of PR #4908 reverted to "宪法" citing foundational authority, but concerns about political connotations persist. **Why it matters:** Exposes the complexity of i18n decisions for infrastructure tools with political/legal terminology; community is actively participating.

### #5293 — Deny-by-default approval selection changed in v0.9.4 (4 comments, 👍1)
**Status:** OPEN | [Link](https://github.com/Hmbown/CodeWhale/issues/5293)
The default highlighted option in the TUI permission request dialog changed to "deny," altering the established interaction pattern. Users may accidentally deny actions when intending to confirm quickly. **Why it matters:** A UX regression that could erode trust in the permission system; asks for configurability and clearer explanation.

### #3205 — Fleet loadout auto: shared model/loadout selector (13 comments)
**Status:** CLOSED | [Link](https://github.com/Hmbown/CodeWhale/issues/3205)
The unified model/loadout selector for TUI, CLI, exec, subagents, and Fleet workers. "Fleet loadout auto" should resolve the whole compute loadout for a role/slot. **Why it matters:** Core architectural work that unifies model selection across all surfaces; the 13-comment thread signals complexity around scope and role resolution.

### #5096 — Compaction gain not visible (3 comments)
**Status:** OPEN | [Link](https://github.com/Hmbown/CodeWhale/issues/5096)
User reports that `/compact` displays "compaction triggered" but the token counter (37K/128K) doesn't actually decrease. **Why it matters:** This is a **transparency bug** — users need to see what compaction actually did, especially given the ongoing 128K-fallback complaints.

### #5209 — File edit silently accepts wrong parameter names (3 comments)
**Status:** OPEN | [Link](https://github.com/Hmbown/CodeWhale/issues/5209)
The `File` tool's `action=edit` mode accepts `new_str` (wrong) instead of `replace` (correct) and returns "Replace successful" — a false positive. **Why it matters:** Critical reliability issue for agent tooling; silently succeeding with no-op edits wastes tokens and erodes trust. Demands loud failures.

### #5023 — IME Candidate Window Jumps / Unstable Position (2 comments)
**Status:** OPEN | [Link](https://github.com/Hmbown/CodeWhale/issues/5023)
Windows 11 users report the IME candidate window is unstable during input. **Why it matters:** A core usability bug for CJK input users — this is the most frequent complaint from Chinese-speaking users; not yet triaged to a maintainer.

### #5250 — Only one API key can be saved (2 comments)
**Status:** OPEN | [Link](https://github.com/Hmbown/CodeWhale/issues/5250)
Users of multiple providers (DeepSeek + GLM) must overwrite the API key each time they switch. **Why it matters:** Multi-provider support is a headline feature; a single-key slot makes it practically unusable for polyglot users. High community demand.

### #5098 — Fleet config: one layer too many, silent shadowing (2 comments)
**Status:** OPEN | [Link](https://github.com/Hmbown/CodeWhale/issues/5098)
Editing `~/.codewhale/agents/builder.toml` had no effect on the fleet roster, and dispatches still resolved the old model. **Why it matters:** Configuration layering is opaque; edits silently shadowed by another layer. This is a trust-killer for the Fleet system.

### #5000 — Interrupted assistant output not durable (2 comments)
**Status:** OPEN | [Link](https://github.com/Hmbown/CodeWhale/issues/5000)
When a turn is interrupted before `MessageComplete`, the TUI may show the text locally but it's absent from the authoritative session — the next model request never sees it. **Why it matters:** Fundamental data-loss bug; session state must be the single source of truth.

### #5314 — Copy message includes rail decorations (1 comment)
**Status:** OPEN | [Link](https://github.com/Hmbown/CodeWhale/issues/5314)
Context-menu "Copy message" includes `●` role glyph and `▏` rail characters; selection-copy is clean. **Why it matters:** Small UX bug, but copy-paste into other tools/agents is a daily action — polluted output is a real friction point. Likely a fast fix.

---

## 4. Key PR Progress

### #5313 — chore(release): prepare v0.9.6
**Status:** CLOSED | [Link](https://github.com/Hmbown/CodeWhale/pull/5313)
The v0.9.6 release preparation: subtractive runtime changes, compaction rebuilt around a single provider summary + committed successor handoff, no mailbox freezing, context-window autodetect removed, sub-agent config maze terminated.

### #5308 — fix(release): use CNB asset download URLs
**Status:** CLOSED | [Link](https://github.com/Hmbown/CodeWhale/pull/5308)
Fixes both updater implementations to use the canonical `codewhale.net/codewhale` repository slug and the `/-/releases/download/vX.Y.Z/` path, so mirror mode receives actual asset bytes instead of release HTML. Preserves mirror-override precedence.

### #5306 — fix(release): validate crate publication order
**Status:** CLOSED | [Link](https://github.com/Hmbown/CodeWhale/pull/5306)
Validates the 20-crate publication order against locked Cargo metadata before any registry operation; moves `codewhale-core` before `codewhale-tui`; fails closed on duplicates, missing/extraneous crates, mixed versions, and dependency inversions.

### #5295 — feat: add Mistral AI as a first-class provider route
**Status:** CLOSED | [Link](https://github.com/Hmbown/CodeWhale/pull/5295)
First-time contributor @xavierpestel-ai adds Mistral AI (la Plateforme) support: `provider = "mistral"`, `CODEWHALE_PROVIDER=mistral`, `codewhale --provider mistral`. Defaults to `mistral-code-latest`. Notably retained as the contributor's own commit — good sign for community onboarding.

### #5281 — build(deps): bump jsonschema from 0.46.10 to 0.49.6
**Status:** OPEN | [Link](https://github.com/Hmbown/CodeWhale/pull/5281)
Dependabot routine dependency bump; still open, likely awaiting CI.

### #5102-related work — Multimodal screenshot viewing (1 comment)
**Status:** OPEN (issue) | [Link](https://github.com/Hmbown/CodeWhale/issues/5102)
Agents cannot reliably see screenshots today; proposes a deliberate multimodal tool with compression and viewing (kimicode `ReadMediaFile`-style). No PR yet, but the issue is detailed and maintainer-backed.

### #5054 — CI: Claude PR review gate permanently dark
**Status:** CLOSED | [Link](https://github.com/Hmbown/CodeWhale/issues/5054)
Bun/tsconfig 'directory mismatch' blocks the claude-review gate on every PR, producing zero verdicts. Closed — presumably fixed or explicitly marked as non-blocking.

### #5058 — Sub-agent conventions: compact launch receipts, child result summaries, friendlier scope errors
**Status:** CLOSED | [Link](https://github.com/Hmbown/CodeWhale/issues/5058)
Launch receipts (~136KB of nested JSON) are being compacted; child results are `self_report_only` forcing parent re-verification; scope errors are confusing. The fix ships compact receipts, "commands ran + evidence" child summaries, and clearer scope-declaration hints.

### #5043 — Make compaction preserve active intent, decisions, evidence, tool continuity
**Status:** CLOSED | [Link](https://github.com/Hmbown/CodeWhale/issues/5043)
Compaction now explicitly preserves active intent, constraints, decisions, verification evidence, active issues/PRs, tool and worker continuity. Closes a family of "lost work after compaction" bugs.

### #3364 — Add read-before-edit guardrails and clearer edit failures
**Status:** CLOSED | [Link](https://github.com/Hmbown/CodeWhale/issues/3364)
Makes narrow edits safer by encouraging/fresh reads before edit operations; failures are now loud, specific, and recoverable. Directly addresses the #5209 complaint class (silent fake success).

---

## 5. Feature Request Trends

| Trend | Evidence | Direction |
|-------|----------|-----------|
| **Multi-provider, multi-key support** | #5250 (multiple API keys), #5295 (Mistral provider PR), #4949 (i18n) | Per-provider key storage in a global secrets store; more first-class providers |
| **Compaction transparency & control** | #5096 (no visible gain), #5239/#5134/#5244 (128K vs 1M), #4394 (survival contract), #5043 (intent preservation) | Users want to *see* what compaction did, *choose* the threshold, and *trust* nothing essential is lost |
| **Sub-agent / Fleet configurability** | #5098 (config shadowing), #5287 (display identity), #3205 (loadout auto) | Single source of truth for Fleet config; name-based identity; less layering |
| **Tool reliability (edit correctness)** | #5209 (silent wrong-param success), #3364 (read-before-edit guardrails) | Loud failures; validation of tool parameters; guardrails for narrow edits |
| **Agent multimodal capability** | #5102 (screenshot viewing) | Deliberate image-reading tool with compression & viewing (kimicode-style) |
| **Reproducible builds** | #5312 (SOURCE_DATE_EPOCH) | Replace hardcoded archive timestamps with standard epoch-based reproducibility |
| **IME/CJK UX polish** | #5023 (IME candidate window), #4949 (translation) | Windows IME input stability; i18n quality beyond mere string translation |

---

## 6. Developer Pain Points

1. **Silent configuration shadowing** — #5098 shows edits to `~/.codewhale/agents/builder.toml` being silently ignored due to layering. Developers need *visible precedence* and *validation feedback*.

2. **False-positive tool success** — #5209: the File edit tool returns "success" for wrong parameter names. This is the single most dangerous class of bug for agent workflows: quiet, token-wasting, trust-eroding.

3. **Compaction opacity** — #5096, #5239: users repeatedly report "it says compacted but nothing changed" and "why 128K when the model supports 1M?" The 0.9.5/0.9.6 work centralizes around this, but user confusion persists (and French UI adds another layer).

4. **Context-length defaults vs. model reality** — #5244/#5134/#5239: unknown model ids silently fall back to 128K windows, causing premature compaction on 1M models. *Loud fallback warnings* are now on the roadmap.

5. **Interrupted-turn output loss** — #5000: text emitted before `MessageComplete` isn't durable in the session. Developers lose visible work when they interrupt a turn.

6. **API key handling friction** — #5250: one key slot, overwritten across providers. Multi-provider workflows are a pain — persisting secrets in repo-local files (#5047) makes it worse.

7. **I18n politics and mechanics** — #4949, #5023, #5314: translation debates (political sensitivity), IME instability on Windows, and UI decorations leaking into copied output. Small details, daily friction.

8. **Sub-agent result verification overhead** — #5058: `self_report_only` child results force parents to re-verify; launch receipts are ~136KB of JSON. Developers hit hidden costs in every sub-agent dispatch.

---

*Digest prepared for 2026-08-10 from public GitHub data. Metrics and summaries reflect the current issue/PR state at time of collection.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*