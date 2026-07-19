# AI CLI Tools Community Digest 2026-07-19

> Generated: 2026-07-19 01:20 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report — AI CLI Developer Tools Ecosystem
**2026-07-19**

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is experiencing a **maturation phase** characterized by intense competition on reliability, cross-platform compatibility, and agent lifecycle management. All six major tools shipped bug fixes or feature updates this week, with **OpenAI Codex** and **Qwen Code** leading release velocity. A common theme across communities is **eroding trust in advertised model capabilities** — context window regressions (Codex), false completion reporting (Gemini CLI), and model contamination across sessions (Qwen) are eroding user confidence. **Desktop performance regressions** (Codex, OpenCode) and **platform gaps** (Windows resume hangs in Copilot CLI, ARM64 sandbox issues in Kimi Code) dominate the issue tracker pain points. Meanwhile, the community is converging on shared feature demands: **session resilience** (retry mechanisms, compaction reliability), **model transparency** (token/context usage indicators), and **agent behavior control** (permission rules, goal interruption).

---

## 2. Activity Comparison

| Tool | Issues (Noteworthy) | PRs (Merged/Open) | Release Status | Notable Hotfix |
|---|---|---|---|---|
| **Claude Code** | ⚠️ Data unavailable | ⚠️ Data unavailable | ⚠️ Summary failed | — |
| **OpenAI Codex** | 10 hot issues (1 critical regression) | 10 PRs (8 merged, 2 open) | **Hotfix shipped** (rust-v0.144.6) | Context window restoration to 272K |
| **Gemini CLI** | 10 hot issues (2 P1 bugs) | 10 PRs (5 merged/closed, 3 open, 2 security) | **Nightly shipped** (v0.52.0) | Variable expansion bypass fix (GHSA) |
| **GitHub Copilot CLI** | 10 hot issues (1 blocker regression) | 0 PRs in 24h | **No release** (v1.0.71 stable) | — |
| **Kimi Code CLI** | 10 hot issues (1 documentation-contradicting bug) | 10 PRs (all open) | **No release** (v0.27.0 stable) | — |
| **OpenCode** | 10 hot issues (memory megathread dominates) | 10 PRs (2 security, 3 feature) | **No release** (v1.18.3 stable) | — |
| **Pi** | 10 hot issues (pricing & compaction focus) | 10 PRs (7 closed, 3 open) | **No release** | Copilot pricing fix in progress |
| **Qwen Code** | 10 hot issues (1 P1 multi-agent bug) | 10 PRs (8 merged, 2 open) | **3 releases shipped** (v0.19.12 stable) | Gemma 4 tool call fix |
| **DeepSeek TUI** | 10 hot issues (xAI auth fixed) | 10 PRs (most merged) | **No release** (v0.9.3 dev) | xAI OAuth & tool schema fixes |

**Key observations:**
- **Qwen Code** had the most release activity (3 versions in 24h)
- **Copilot CLI** had zero PR activity — appears to be in a maintenance lull
- **Claude Code** digest generation failed entirely — a notable visibility gap for Anthropic's tool
- **DeepSeek TUI** saw the highest PR density per developer (13 PRs from a single maintainer)

---

## 3. Shared Feature Directions

| Feature Direction | Tools Expressing Need | Specific Requirements |
|---|---|---|
| **Context/Token Transparency** | Copilot CLI (#2052), OpenCode (memory megathread #20695), Qwen (#6824) | Visible token counters, "45% context used" indicators, session size warnings |
| **Session Resilience & Retry** | Pi (#6647, #6775), Codex (#24948), OpenCode (#30443) | Retry logic for compaction/summarization failures, session freeze recovery, compaction loop prevention |
| **Multi-Agent Lifecycle Control** | Gemini CLI (#22323, #21968), OpenCode (#34207), Qwen (#7156), Copilot CLI (#4161) | Subagent visibility, model variant stickyness, tool availability after mode switching, false-success reporting |
| **Permission/Friction Reduction** | DeepSeek TUI (#1186), Kimi Code (#2508), Gemini CLI (#22672), OpenCode (V2 config regressions) | Persistent `allow/deny/ask` rules, consistent first-match-wins behavior, guardrails against destructive commands |
| **Platform Parity (Windows/ARM64)** | Kimi Code (#2503, #2496), Copilot CLI (#4165), OpenCode (#37353), DeepSeek TUI (#4085) | Windows 11 support, ARM64 sandbox fixes, Dropbox/macOS File Provider compatibility |
| **Developer Experience Diagnostics** | Kimi Code (#2498), DeepSeek TUI (doctor PRs #4544, #4539), Codex (doctor command usage) | `kimi doctor`, `codewhale doctor` read-only diagnostics, environment/config validation |
| **Model Compatibility Hardening** | OpenCode (#32548), Qwen (#7148), Pi (#6167), Gemini CLI (#19873) | Anthropic prefill error handling, Gemma native tool tokens, cross-model thinking block normalization |
| **Structured Output / CI Integration** | Kimi Code (#2500, #2504), OpenCode (#8535), DeepSeek TUI (#4022) | `--output-file` flags, `.kimiignore` patterns, session history pagination for clients |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Distinction |
|---|---|---|---|
| **OpenAI Codex** | Multi-model orchestration (GPT-5.6 Sol/Terra/Luna, Opus) | Power users & Pro subscribers | Deep ACP server integration; most aggressive release cadence; desktop-first with browser extensions |
| **Gemini CLI** | Agent autonomy & bash affinity | Developer teams | Strongest security hardening (GHSA variable expansion); agent self-awareness features; "generalist agent" architecture |
| **Copilot CLI** | GitHub workflow integration | Enterprise developers | Tightest GitHub ecosystem integration; plan-mode/autopilot mode separation; most conservative release pace |
| **Kimi Code CLI** | Thinking-effort controls & ACP server | Chinese-language developers | Most responsive to localization needs; `k3` model passthrough; permission engine design emphasis |
| **OpenCode** | Multi-agent session management | Desktop-first developers | Largest community (50+ issues/PRs in 24h); memory debugging community; V2 TUI/config overhaul |
| **Pi** | Copilot Enterprise & multi-provider support | Team/enterprise users | Broadest provider support (OpenAI, Anthropic, Vertex); RPC protocol for external tools; compaction reliability focus |
| **Qwen Code** | Daemon architecture & MCP ecosystem | Server/daemon-first users | Most releases in 24h; daemon cold-start tracing; Gemma 4 compatibility; process-level session leases |
| **DeepSeek TUI** | Single-developer maintainer velocity | DeepSeek model users | Fastest bugfix turnaround (13 PRs from maintainer); xAI OAuth fixes; work-graph session ledger |

**Strategic differentiators:**
- **Security focus**: Gemini CLI leads with dedicated security PRs (variable expansion bypass, path traversal prevention)
- **Release velocity**: Qwen Code and OpenAI Codex compete for most frequent releases; Copilot CLI is notably slower
- **Model diversity**: Pi supports the widest provider range (OpenAI, Anthropic, Copilot Enterprise, Vertex); DeepSeek TUI is most model-specific
- **Localization**: Kimi Code and DeepSeek TUI both have vocal Chinese-speaking user bases demanding i18n
- **Desktop stability**: OpenCode and Codex battle the most desktop regressions (memory bloat, white screens, USB conflicts)

---

## 5. Community Momentum & Maturity

| Tool | Community Health | Velocity Signal | Maturity Indicators |
|---|---|---|---|
| **OpenAI Codex** | **High** — 34👍 on regression, 56 comments on browser issue | Hotfix shipped within days of regression report | Responsive maintainers; structured release pipeline; but regression frequency suggests testing gaps |
| **Gemini CLI** | **Medium-High** — 8👍 on agent hang issue | Regular nightly builds; active security hardening | Most security-conscious; but agent reliability (hangs, false completions) needs improvement |
| **Copilot CLI** | **Medium** — 62👍 on opus context request, but zero PRs | **Stalling** — no PR activity in 24h | Stable but feature-starved; user frustration building around context window parity |
| **Kimi Code CLI** | **Medium** — low upvotes but fast PR response | Growing — active development on thinking effort, ACP server | Responsive to UX feedback; permissions engine design under scrutiny |
| **OpenCode** | **Very High** — 90👍 on memory issue, 50+ issues/PRs | Intense — massive community participation | Most community-driven debugging; V2 config is causing trust issues |
| **Pi** | **Medium-High** — active compaction & pricing discussions | Steady — closed 27 issues, 9 PRs | Most mature multi-provider support; compaction reliability concerns dominate |
| **Qwen Code** | **Medium** — lower upvotes but high-quality issue reports | **Highest release velocity** — 3 releases in 24h | Daemon architecture is differentiating; MCP ecosystem investment |
| **DeepSeek TUI** | **Medium** — maintainer-driven, niche | **Extremely high per-developer** — 13 PRs from 1 person | Most agile single-maintaner project; Chinese localization strong; security auditing improving |

**Maturity spectrum:**
- **Early-stage vs. established**: Copilot CLI and Pi feel most "enterprise-stable" but slow to ship features; DeepSeek TUI and Kimi Code are fastest-moving but smaller user bases
- **Community participation**: OpenCode has the most vocal community (113 comments on memory thread); Codex has the most cross-verification culture (users running `doctor` to confirm regressions)
- **Security posture**: Gemini CLI leads with explicit security PRs; OpenCode and Codex show reactive security fixes (malformed tool input, stale npm cache)

---

## 6. Trend Signals

1. **Context window transparency is the new "must-have"** — Users across Copilot CLI, OpenCode, and Qwen are demanding visible token/context counters. After the Codex 1.05M→258K regression, trust in advertised specs is at an all-time low. Expect **built-in context meters** to become table stakes.

2. **Agent behavior control is splitting into two models**: **Permission rules** (DeepSeek TUI, Kimi Code, Gemini CLI's `allow/deny/ask`) for security-conscious users, versus **guardrails** (Gemini CLI's destructive command prevention, OpenCode's tool_call=false) for general users. Convergence on persistent, scoped permission systems is likely.

3. **Multi-agent lifecycle management is the biggest unsolved pain point** — Every tool except Copilot CLI has open bugs about subagent model contamination, false success reporting, or tool availability after mode switching. This is the top architectural challenge for the ecosystem.

4. **Desktop performance is a crisis** — Codex (55 GB memory bloat, AppHang cycles), OpenCode (infinite compaction loops, white screens on Windows+WSL), and Pi (100% CPU on large files) all hit severe desktop regressions. The **Electron/native app reliability threshold** has not been met.

5. **Localization is becoming a competitive moat** — Kimi Code and DeepSeek TUI both have active Chinese-speaking communities demanding i18n. OpenCode has hardcoded English strings. Tools that invest in localization first will capture non-English developer markets.

6. **Security is moving from reactive to proactive** — Gemini CLI's variable expansion bypass fix and Kimi Code's permission engine redesign signal a shift toward **design-time security** rather than patch-and-fix. The `doctor` command pattern (read-only diagnostics) is becoming a standard security practice.

7. **MCP ecosystem is standardizing but fragile** — Qwen Code and DeepSeek TUI both shipped MCP tool name normalization fixes. Tool naming, timeout handling, and provider compatibility remain friction points — but the ecosystem is converging on common patterns.

8. **Billing/credits confusion is a trust killer** — Codex (quota exhaustion after Plus purchase), Copilot CLI (unexpected premium request consumption), and OpenCode (rate-limited despite paying) all have billing attribution bugs. Users who feel overcharged or misled are quick to post negative feedback. **Transparent credit accounting** will differentiate trustworthy platforms.

---

**Bottom line for decision-makers:** No single tool dominates across all dimensions. **Codex** leads in feature velocity but suffers reliability regressions. **Gemini CLI** is the security leader but has agent hang issues. **Qwen Code** has the most stable release pipeline but smaller community. **DeepSeek TUI** is the most agile for niche users. **Copilot CLI** is falling behind on parity features. The trend is clear: **session resilience, model transparency, and platform parity** are the non-negotiable basics — tools that ship these reliably will win developer trust in 2026H2.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data date: 2026-07-19 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following Skills (Pull Requests) have attracted the most community discussion and represent the most active contributions:

### #1298 — `fix(skill-creator): run_eval.py always reports 0% recall`
**Status:** Open | **Author:** MartinCajiao | **Created:** 2026-06-10
**Links:** [PR #1298](https://github.com/anthropics/skills/pull/1298)

**Functionality:** A critical fix for the `skill-creator` meta-skill's evaluation pipeline. The `run_eval.py` script — which powers the description-optimization loop (`run_loop.py`, `improve_description.py`) — has been consistently reporting `recall=0%` for every skill description tested. This PR addresses ten independent reproductions of this bug (see #556). The fix installs the eval artifact as a real skill and repairs Windows stream reading, trigger detection, and parallel worker execution.

**Discussion highlights:** The most-commented PR in the repository. Multiple community members confirmed the bug independently. The fix is substantial, touching both cross-platform compatibility and core evaluation logic.

---

### #514 — `Add document-typography skill`
**Status:** Open | **Author:** PGTBoos | **Created:** 2026-03-04
**Links:** [PR #514](https://github.com/anthropics/skills/pull/514)

**Functionality:** A skill that enforces typographic quality control on generated documents. It prevents orphan word wrap (1–6 words on isolated lines), widow paragraphs (section headers stranded at page bottom), and numbering misalignment — common defects in AI-generated documents.

**Discussion highlights:** Strong reception for addressing a universal pain point in AI document output. Users noted this affects every document Claude generates and rarely gets explicitly requested.

---

### #538 — `fix(pdf): correct case-sensitive file references in SKILL.md`
**Status:** Open | **Author:** Lubrsy706 | **Created:** 2026-03-06
**Links:** [PR #538](https://github.com/anthropics/skills/pull/538)

**Functionality:** Fixes 8 case-sensitivity mismatches in the PDF skill's `SKILL.md` file, where file references used uppercase (`REFERENCE.md`, `FORMS.md`) but the actual files are lowercase. This breaks on case-sensitive filesystems (Linux, macOS).

**Discussion highlights:** Small in scope but high-impact reliability fix. Demonstrates the community's attention to cross-platform correctness.

---

### #486 — `Add ODT skill — OpenDocument text creation and template filling`
**Status:** Open | **Author:** GitHubNewbie0 | **Created:** 2026-03-01
**Links:** [PR #486](https://github.com/anthropics/skills/pull/486)

**Functionality:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods). Triggers on keywords like "ODT", "ODS", "ODF", "OpenDocument", "LibreOffice". Covers the full LibreOffice-compatible document workflow.

**Discussion highlights:** Addresses gaps in office document format support. Community interest in open-source document standards is notable.

---

### #210 — `Improve frontend-design skill clarity and actionability`
**Status:** Open | **Author:** justinwetch | **Created:** 2026-01-05
**Links:** [PR #210](https://github.com/anthropics/skills/pull/210)

**Functionality:** A substantial revision to the existing `frontend-design` skill, ensuring every instruction is actionable within a single conversation and that guidance is specific enough to steer Claude's behavior without ambiguity.

**Discussion highlights:** Demonstrates community investment in skill quality rather than just quantity. The PR focuses on making existing skills more practically useful.

---

### #83 — `Add skill-quality-analyzer and skill-security-analyzer`
**Status:** Open | **Author:** eovidiu | **Created:** 2025-11-06
**Links:** [PR #83](https://github.com/anthropics/skills/pull/83)

**Functionality:** Two meta-skills: (1) **skill-quality-analyzer** evaluates Skills across Structure & Documentation (20%), functional completeness, and five other dimensions; (2) **skill-security-analyzer** audits skills for security vulnerabilities. Intended for the `example-skills` marketplace.

**Discussion highlights:** Early but sustained interest in quality assurance and security tooling for the skills ecosystem itself.

---

### #1367 — `feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate`
**Status:** Open | **Author:** YuhaoLin2005 | **Created:** 2026-06-28
**Links:** [PR #1367](https://github.com/anthropics/skills/pull/1367)

**Functionality:** A universal audit skill that checks AI output before delivery. Step 0 performs mechanical file verification (do claimed output files exist?). Then a four-dimension reasoning audit in damage-severity priority order. Works across any project, tech stack, or model.

**Discussion highlights:** Recent but rapidly accumulating comments. Directly addresses concerns about output quality and hallucination verification.

---

## 2. Community Demand Trends

Analysis of the most-discussed Issues reveals five concentrated demand vectors:

### 🔴 Critical: `skill-creator` Evaluation Pipeline Reliability
**Issues:** #556 (12 comments, 7 👍), #1169 (3 comments), #1061 (3 comments, 2 👍)
**Trend:** The `skill-creator` meta-skill's evaluation tooling (`run_eval.py`, `run_loop.py`) is **consistently broken on Windows and produces 0% recall for all users**. This is the single largest blocker to community skill development. Multiple independent reproductions confirm the bug is universal, not environment-specific.

### 🟠 High: Security & Trust Boundary Concerns
**Issues:** #492 (34 comments, 2 👍), #1175 (4 comments)
**Trend:** Community members are raising security concerns about skills impersonating official Anthropic offerings and about access control when handling sensitive documents (e.g., SharePoint Online). The `anthropic/` namespace trust boundary abuse (#492) is the most-commented issue in the entire repository.

### 🟡 Medium: Organizational Skill Sharing
**Issues:** #228 (14 comments, 7 👍)
**Trend:** Organizations want to share skills internally without manual file downloads. The current workflow (download .skill → Slack → manual upload) is a significant adoption barrier for enterprise teams.

### 🟡 Medium: Windows Compatibility
**Issues:** #1061 (3 comments, 2 👍), #556 (12 comments, 7 👍)
**Trend:** Multiple skill-creator scripts fail on Windows due to Unix-first assumptions (subprocess `PATHEXT`, `cp1252` encoding, `select` on pipes). This blocks a significant portion of the developer community.

### 🟢 Emerging: Reasoning Quality & Output Verification
**Issues:** #1385 (3 comments), #412 (6 comments)
**Trend:** Growing interest in multi-stage quality gates — pre-task calibration, adversarial review, delivery verification. The community wants systematic reasoning quality assurance, not just functional correctness.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and are likely to be merged soon:

| PR # | Skill | Author | Comments | Key Feature |
|------|-------|--------|----------|-------------|
| [#1367](https://github.com/anthropics/skills/pull/1367) | self-audit (v1.3.0) | YuhaoLin2005 | High | Four-dimension reasoning quality gate |
| [#1323](https://github.com/anthropics/skills/pull/1323) | fix(skill-creator): trigger detection | Polluelo978 | High | Fixes 0% recall in eval loop |
| [#1302](https://github.com/anthropics/skills/pull/1302) | color-expert | meodai | Moderate | Comprehensive color expertise (ISCC-NBS, Munsell, OKLCH) |
| [#1099](https://github.com/anthropics/skills/pull/1099) | skill-creator: Windows subprocess fix | joshuawowk | High | Resolves WinError 10038 |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | 4444J99 | Moderate | Full testing stack (Trophy model, React, AAA pattern) |
| [#525](https://github.com/anthropics/skills/pull/525) | pyxel (retro game dev) | kitao | Low | Pyxel MCP server integration |
| [#362](https://github.com/anthropics/skills/pull/362) | fix(skill-creator): UTF-8 panic | Mr-Neutr0n | Moderate | Rust CLI panic on multi-byte characters |
| [#509](https://github.com/anthropics/skills/pull/509) | docs: CONTRIBUTING.md | narenkatakam | Moderate | Community health metrics improvement |

**Most likely to land first:** The `skill-creator` fixes (#1323, #1099, #362) and the `testing-patterns` skill (#723) have clear value propositions and active maintainer engagement.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable, cross-platform evaluation tooling in the `skill-creator` meta-skill — the ability to objectively measure whether a skill description actually triggers Claude's behavior is the foundational bottleneck blocking the entire Skills ecosystem, with Windows compatibility and accurate trigger detection being the two critical blockers.**

Secondary but significant: the community wants systematic **quality assurance meta-skills** (self-audit, security analysis, output verification) and enterprise-grade **trust boundary management** — indicating maturation beyond individual skill creation toward ecosystem governance.

---

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest — 2026-07-19

## Today's Highlights
A hotfix release (rust-v0.144.6) corrects GPT-5.6 Sol, Terra, and Luna context windows to 272K tokens, following days of community outcry over a severe regression that dropped advertised 1.05M context to 258K. Desktop performance issues dominate the issue tracker, with multiple Windows reports of AppHang cycles and macOS memory bloat reaching 55 GB. Meanwhile, the development pipeline shows strong momentum on streaming optimization, audio output support, and session continuity.

---

## Releases

### rust-v0.144.6
**Bug Fixes:**
- Refreshed bundled instructions for GPT-5.6 Sol, Terra, and Luna
- Corrected their context windows to **272,000 tokens** (resolves the regression from #32806)
- PRs: #33972 (backport), #34009 (narrowed hotfix)

Full Changelog: https://github.com/openai/codex/compare/rust-v0.144.5...rust-v0.144.6

### rust-v0.145.0-alpha.24
Pre-release alpha with no detailed changelog in the 24h window.

---

## Hot Issues (10 Most Noteworthy)

### #32806 — [CLOSED] 🚨 [SEVERE REGRESSION] GPT-5.6 Sol context cut again: 353K → 258K despite advertised 1.05M
**Impact:** Critical. Users paid for 1.05M context but observed <25% of advertised capacity. The regression was tracked across three different measured values before the hotfix landed today.
**Reaction:** 34 👍, 26 comments — highly engaged. Community frustration was palpable, with multiple users cross-verifying with `codex doctor`.
🔗 https://github.com/openai/codex/issues/32806

### #32925 — [CLOSED] Codex Desktop: Browser and Chrome plugins fail with `Cannot redefine property: process`
**Impact:** Blocks browser integration for all users on Desktop 26.707.71524 — a hard crash on launch.
**Reaction:** 33 👍, 56 comments — highest engagement this week. Users reported workarounds involving rolling back Chrome.
🔗 https://github.com/openai/codex/issues/32925

### #24948 — [OPEN] Codex session logs grow to 700MB-2GB from repeated compaction history
**Impact:** Disk space exhaustion during long sessions. Persists across multiple CLI versions (0.118.0 → current).
**Reaction:** 13 comments, low upvotes but high longevity (opened May 28). Chronic, unresolved pain.
🔗 https://github.com/openai/codex/issues/24948

### #33873 — [OPEN] Codex Desktop frequently becomes unresponsive after updating on Windows
**Impact:** New regression in 26.715 affecting Plus users on Windows 10. Freezes degrade daily workflow.
**Reaction:** 6 👍, 13 comments. Multiple duplicates reported (#33884, #33924).
🔗 https://github.com/openai/codex/issues/33873

### #34061 — [OPEN] Insane Codex Disk Usage from Subagents
**Impact:** Subagent architecture appears to leak disk space aggressively. Users on Pro tier hit storage limits mid-session.
**Reaction:** Fresh (opened yesterday), 5 comments, 0 upvotes — likely underreported due to novelty.
🔗 https://github.com/openai/codex/issues/34061

### #33582 — [OPEN] ChatGPT/Codex repeatedly grows to 55 GB and freezes the system
**Impact:** macOS memory bloat to 55 GB renders the entire machine unusable. Build 5440.
**Reaction:** 2 comments, low engagement but extreme severity.
🔗 https://github.com/openai/codex/issues/33582

### #32101 — [OPEN] GPT-5.6 Code Mode omits tool_search from exec, degrading deferred MCP discovery
**Impact:** Model capability mismatch — GPT-5.6 supports deferred tool search but Code Mode drops the `ToolSpec::ToolSearch` primitive.
**Reaction:** 3 👍, 2 comments. Affects agent tool-chain reliability for MCP users.
🔗 https://github.com/openai/codex/issues/32101

### #34004 — [OPEN] Pasting code snippets converts to markdown, breaking diffs
**Impact:** Regressive UX — pasting raw code or diffs into the app auto-converts to Markdown, corrupting review workflows.
**Reaction:** 2 👍, 2 comments. Small but vocal from Pro users doing code review.
🔗 https://github.com/openai/codex/issues/34004

### #33924 — [OPEN] Windows Codex freezes with UGREEN USB switch
**Impact:** Niche hardware conflict causing hard freezes until USB device is physically unplugged. Suggests polling/driver sensitivity in the app-server.
**Reaction:** 2 comments, 0 upvotes. Low volume but indicative of broader USB/hardware compatibility gaps.
🔗 https://github.com/openai/codex/issues/33924

### #34066 — [OPEN] Weekly Codex limit exhausted immediately after purchasing Plus
**Impact:** Billing/usage attribution bug — new subscribers see zero usable quota after payment. Erodes trust in subscription model.
**Reaction:** 3 comments, 0 upvotes. Similar to #30816 (same pattern reported 18 days prior).
🔗 https://github.com/openai/codex/issues/34066

---

## Key PR Progress (10 Important Merges/Opens)

### #34080 — [MERGED] Add audio output support to dynamic tools and code mode
**Impact:** Enables `inputAudio` content items, audio helpers, and `audio()` code-mode helper. Unlocks voice-output agents and MCP audio streams.
🔗 https://github.com/openai/codex/pull/34080

### #34067 — [MERGED] Seed realtime V3 sessions with initial text items
**Impact:** Adds `initialItems` field to `thread/realtime/start`, enabling pre-seeded conversation history in realtime sessions. Foundational for persistent voice/chat hybrid sessions.
🔗 https://github.com/openai/codex/pull/34067

### #34049 — [MERGED] Avoid redundant TUI redraws while streaming
**Impact:** Performance optimization for CLI TUI — only redraws when completed lines change the visible tail. Reduces CPU overhead during long streaming responses.
🔗 https://github.com/openai/codex/pull/34049

### #34045 — [MERGED] Render streamed Markdown incrementally
**Impact:** Major TUI rendering optimization — caches completed Markdown blocks, only re-renders active blocks. Should noticeably reduce jank during code block streaming.
🔗 https://github.com/openai/codex/pull/34045

### #34009 — [MERGED] Narrow 0.144 hotfix to GPT-5.6 prompts and context
**Impact:** Surgical fix that reverts unrelated catalog changes while keeping corrected 272K context windows. Ensures stable hotfix without side-effects.
🔗 https://github.com/openai/codex/pull/34009

### #33982 — [MERGED] Gate audio history by model input modalities
**Impact:** Audio is preserved in prompts only for models that advertise audio input; unsupported models receive an omission marker. Prevents modality errors.
🔗 https://github.com/openai/codex/pull/33982

### #33950 — [MERGED] Let users remember the working directory for resumed sessions
**Impact:** Adds `tui.resume_cwd` with `current` and `session` modes. Users can persist CWD preference, reducing friction when resuming long-lived sessions.
🔗 https://github.com/openai/codex/pull/33950

### #33944 — [MERGED] Track permission instructions in world state
**Impact:** Permissions are now modeled as a world-state section with stable hash keys. Re-emits permission context only when changed — reduces redundant token usage.
🔗 https://github.com/openai/codex/pull/33944

### #33938 — [MERGED] Centralize SQLite connection configuration
**Impact:** Single `SqliteConfig` entry point standardizes WAL, sync, auto-vacuum, and pool settings across all Codex databases. Foundation for reliability improvements.
🔗 https://github.com/openai/codex/pull/33938

### #31781 — [OPEN, reviewed] Bound executor-controlled HTTP response buffering
**Impact:** Security hardening — bounds response buffering by byte count (not just frame count) to prevent untrusted remote exec-servers from exhausting app-server memory.
🔗 https://github.com/openai/codex/pull/31781

---

## Feature Request Trends

1. **Multi-Agent lifecycle management** (#33314, 8 👍): Users want verifiable full-profile application and persistence for custom subagents. Follow-up to #32782.

2. **Agent efficiency benchmarks** (#34081): Community is self-publishing reproducible case studies (e.g., LabDelta repository) to help OpenAI optimize token/step costs.

3. **UI Internationalization** (#34078): Chinese (Simplified) interface support requested. Growing non-English developer base.

4. **Disable auto-resolve for questions** (#34079, #28969): Users want control over the 60-second auto-resolve timer for pending questions — interrupts deep-focus workflows.

5. **Legacy pagination support** (#34085, merged): Thread history pagination needed for clients doing full-history resume — now shipped.

---

## Developer Pain Points

1. **Context window trust erosion** (#32806): The 1.05M→258K regression (even temporarily) has shaken confidence in advertised model specs. Hotfix restored 272K, but the gap from advertised remains a sore point.

2. **Desktop performance regressions** (multiple Windows issues: #33873, #33884, #33875, #33924): The 26.715 release introduced significant unresponsiveness, AppHang cycles, and high CPU from Windows Defender/WMI interactions. macOS not immune either (#33582: 55 GB memory bloat).

3. **Subagent disk/memory leaks** (#34061, #33700, #24948): Completed subagents leave stale thread_spawn_edges, restore old MCP stacks, and accumulate compaction history. Disk usage grows unboundedly across sessions.

4. **Billing/rate-limit confusion** (#34066, #30816): Users report immediate quota exhaustion after Plus subscription — unclear attribution between Codex vs. ChatGPT usage. Damaging to subscription trust.

5. **Browser/plugin fragility** (#32925, #32700): Chrome integration breaks on `Cannot redefine property: process`. Computer Use leaves stale code_sign_clone bundles until reboot. Plugin ecosystem remains brittle.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-19

## Today's Highlights
The nightly v0.52.0 build ships with an LLM-based triage orchestrator for caretaker workflows and refined macOS security profiles. On the bug front, a critical security PR blocks variable expansion bypasses (GHSA-wpqr-6v78-jr5g), while a long-standing issue reveals that subagent MAX_TURNS interruptions are falsely reported as "GOAL" success. The community continues to push for AST-aware codebase navigation, deterministic memory redaction, and better agent self-awareness.

## Releases
**v0.52.0-nightly.20260718.gacae7124b**
- `feat(caretaker-triage)`: Implement LLM triage orchestrator and container build ([#28345](https://github.com/google-gemini/gemini-cli/pull/28345))
- `refactor(cli)`: Align macOS permissive Seatbelt profiles with deny-default model

## Hot Issues

1. **#22323 — Subagent recovery after MAX_TURNS reported as GOAL success, hiding interruption**  
   *Status: Open (P1, bug)*  
   The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it hit the maximum turn limit before performing any analysis. This false-positive reporting erodes trust in agent completions. 11 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

2. **#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing**  
   *Status: Open (P2, enhancement, effort/large)*  
   Proposes using Gemini 3's native bash training to chain POSIX tools with zero-dependency sandboxing and post-execution intent routing. 8 comments, 1 👍.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/19873)

3. **#24353 — Robust component level evaluations**  
   *Status: Open (P1, customer-issue)*  
   Follow-up to the behavioral evals framework (#15300). Tracks creation of 76 behavioral eval tests across 6 Gemini models. 7 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/24353)

4. **#22745 — Assess impact of AST-aware file reads, search, and mapping**  
   *Status: Open (P2, feature)*  
   Epic investigating whether AST-aware tools can reduce turns by reading method bounds precisely and reducing token noise. 7 comments, 1 👍.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22745)

5. **#21409 — Generalist agent hangs**  
   *Status: Open (P1, bug)*  
   `gemini-cli` hangs forever when deferring to the generalist agent. Simple operations like folder creation fail. Workaround: instruct the model not to use sub-agents. 7 comments, 8 👍 — highest community reaction.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21409)

6. **#21968 — Gemini does not use skills and sub-agents enough**  
   *Status: Open (P2, bug)*  
   Custom skills and sub-agents are rarely invoked autonomously, even when highly relevant. Users must explicitly instruct the model. 6 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21968)

7. **#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely**  
   *Status: Open (P2, bug)*  
   Auto Memory only marks a session as processed when the agent reads the transcript. Low-signal sessions that are skipped remain unprocessed and get re-surfaced forever. 5 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/26522)

8. **#25166 — Shell command execution gets stuck with "Waiting input" after completion**  
   *Status: Open (P1, bug)*  
   Simple CLI commands that do not require stdin are reported as "awaiting user input" indefinitely after completion. 4 comments, 3 👍.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

9. **#20079 — Symlinked agent files not recognized**  
   *Status: Open (P2, bug)*  
   `~/.gemini/agents/filename.md` symlinks are silently ignored. Users expect symlinks to work for organizing custom agents. 4 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/20079)

10. **#22672 — Agent should stop/discourage destructive behavior**  
    *Status: Open (P2, customer-issue)*  
    Models occasionally use `git reset`, `--force`, or dangerous DB commands when safer alternatives exist. Calls for guardrails. 3 comments, 1 👍.  
    [Issue](https://github.com/google-gemini/gemini-cli/issues/22672)

## Key PR Progress

1. **#28403 — fix(core): block $VAR and ${VAR} variable expansion bypass**  
   *Size: M/L | Priority: P1 | Area: Security*  
   Fixes incomplete detection in `detectBashSubstitution()` and `detectPowerShellSubstitution()` that allowed variable expansion to bypass GHSA-wpqr-6v78-jr5g fixes. Hardens CI workflow.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28403)

2. **#28438 — Trim tool names before registry lookup**  
   *Size: XS | Open*  
   Whitespace-padded tool names now resolve correctly through the script tool registry. Includes regression test.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28438)

3. **#28348 — fix: resolve MaxListenersExceededWarning and infinite auth loop**  
   *Area: Core | Size: M*  
   Fixes two critical issues: event listener leak causing warnings (and potential infinite loops) on API retries, and an infinite OAuth loop on Windows after successful authentication.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28348)

4. **#28353 — fix(a2a-server): prevent path traversal in restore command**  
   *Size: S | Status: need-issue*  
   Defense-in-depth for the A2A server's `restore` command — inputs like `../../../etc/passwd` no longer escape the checkpoint directory.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28353)

5. **#28247 — fix(core): match ls ignore globs by relative path**  
   *Size: M | Closed*  
   `ls` ignore patterns with path separators now match workspace-relative paths instead of only basenames, using `picomatch` for correct `**` glob behavior.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28247)

6. **#28248 — docs: explain MCP env expansion**  
   *Size: S | Closed*  
   New documentation section covering `$VAR`, `${VAR}`, `${VAR:-fallback}`, Windows `%VAR%` syntax, and explicit call-outs for unsupported patterns like `{{VAR}}`.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28248)

7. **#28436 — chore/release: bump version to 0.52.0-nightly.20260718.gacae7124b**  
   *Size: S | Open*  
   Automated nightly version bump.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28436)

8. **#28438 — Trim tool names before registry lookup** (listed above)

9. **#28348 — fix: resolve MaxListenersExceededWarning and infinite auth loop** (listed above)

10. **#28403 — fix(core): block $VAR and ${VAR} variable expansion bypass** (listed above)

## Feature Request Trends

**AST-aware codebase navigation** dominates feature requests. Multiple issues (#22745, #22746) propose using AST readers for precise method-bound extraction, reducing turn count and token waste. The community wants the agent to understand code structure natively rather than through heuristic file reads.

**Sandboxed, zero-dependency execution** (#19873) aims to unlock Gemini 3's bash affinity while maintaining security. This would enable native POSIX tool chaining without Docker/container overhead.

**Subagent visibility and control** is a recurring theme: users want subagent trajectories in `/chat share` (#22598), better self-awareness of available tools (#21432), and configurable subagent permissions (#22093).

**Memory system improvements** (#26522, #26523, #26525) focus on deterministic redaction, invalid patch quarantine, and avoiding infinite retries on low-signal sessions.

## Developer Pain Points

1. **Agent hangs and false completions** — The generalist agent and subagents frequently hang (#21409) or report "GOAL" / "success" states when they actually hit limits (#22323), breaking automated workflows.

2. **Authentication loops** — Windows users experience infinite OAuth loops (#28341), and the broader community hits `MaxListenersExceededWarning` during API retries (#28313).

3. **Subagent adoption failure** — Custom skills and sub-agents are configured but rarely used autonomously (#21968). Users must explicitly instruct the model to use them, defeating the purpose.

4. **Shell execution quirks** — Commands are stuck in "awaiting input" state after completion (#25166), models create scratch scripts in random directories (#23571), and interactive prompts (e.g., `vite create`) trap the agent indefinitely (#22465).

5. **Security gaps** — Variable expansion bypasses in shell substitution detection (#28403) and path traversal in A2A restore (#28353) highlight ongoing security hardening needs.

6. **Terminal rendering issues** — Corruption after exiting external editors (#24935) and flicker on terminal resize (#21924) degrade the user experience, especially for power users.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest**
*For 2026-07-19*

---

### 1. Today's Highlights
No new releases shipped in the last 24 hours, but the repository saw sustained community activity with 28 issues updated. Key pain points emerged around session reliability on Windows, zombie process accumulation on Linux, and unreliable plan-mode transitions with the new GPT-5.6 models. The long-running request for **1M context window support** for Opus 4.7 (62 👍) continues to be the most upvoted open feature request.

---

### 2. Releases
**No new releases in the last 24 hours.** The current stable version remains v1.0.71.

---

### 3. Hot Issues
*(10 noteworthy issues, ordered by community impact or recency)*

- **#2785 – Support 1M context window for Claude Opus 4.7**  
  *62 reactions* — The most upvoted open request. Users demand parity with Claude Code’s ability to use Opus 4.7 with a 1M context. The Copilot CLI currently caps Opus 4.7 at a smaller window.  
  [github/copilot-cli Issue #2785](https://github.com/github/copilot-cli/issues/2785)

- **#4163 – Zombie process accumulation under copilot PID**  
  *Linux stability* — A user reports ~2 zombie processes/min leaking under the copilot PID. For long-running sessions, this degrades system performance and indicates a missing `waitpid()`/SIGCHLD handler.  
  [github/copilot-cli Issue #4163](https://github.com/github/copilot-cli/issues/4163)

- **#4165 – `copilot --resume` hangs on Windows cold start**  
  *Platform blocker* — Sessions cannot be resumed directly from PowerShell on Windows; a cold start hangs indefinitely at "Resuming session…". Workaround exists (start interactive session first) but this is a significant UX regression.  
  [github/copilot-cli Issue #4165](https://github.com/github/copilot-cli/issues/4165)

- **#4172 – Exiting plan mode not reliable with GPT-5.6 models**  
  *Regression* — After generating a plan, the CLI saves `plan.md` but then hangs instead of returning the user to interactive mode. Affects the core workflow for new GPT-5.6 model users.  
  [github/copilot-cli Issue #4172](https://github.com/github/copilot-cli/issues/4172)

- **#4160 – Plan mode over-blocks read-only shell commands (keyword false positives)**  
  *Usability friction* — Plan-mode heuristics block safe commands like `cat`, `grep`, or `ls` based on substring matching. Developers report this makes plan-mode nearly unusable for exploration tasks.  
  [github/copilot-cli Issue #4160](https://github.com/github/copilot-cli/issues/4160)

- **#4034 – Hook subprocess stdin write-end left open for tool-use hooks**  
  *Bug affecting automation* — When using `preToolUse`/`postToolUse` hooks, the subprocess never receives EOF on stdin. The documented `$(cat)` pattern hangs indefinitely, breaking custom hook workflows.  
  [github/copilot-cli Issue #4034](https://github.com/github/copilot-cli/issues/4034)

- **#4161 – `task_complete` tool unavailable after switching back to autopilot mode**  
  *Regression* — A known bug (#1523) that was fixed in v1.0.4 has reappeared in v1.0.71. Users switching modes lose access to the `task_complete` tool, breaking multi-step agent workflows.  
  [github/copilot-cli Issue #4161](https://github.com/github/copilot-cli/issues/4161)

- **#1477 – "Continuing autonomously (3 premium requests)" after model completion**  
  *18 reactions* — Users report unexpected premium-request consumption after a model completes its work. The autopilot mode appears to spend credits without user intent.  
  [github/copilot-cli Issue #1477](https://github.com/github/copilot-cli/issues/1477)

- **#1979 – Remote session support for Copilot CLI (attach from mobile/browser)**  
  *53 reactions* — Feature parity request. Users want to attach to a running CLI session remotely, similar to Claude Code’s remote session feature. Remains one of the most-requested features.  
  [github/copilot-cli Issue #1979](https://github.com/github/copilot-cli/issues/1979)

- **#2052 – Persistent token/context usage indicator**  
  *19 reactions* — Developers want a visible "45% context used" or "52k/128k tokens" indicator in the CLI UI. Currently context usage is opaque, making it hard to manage large sessions.  
  [github/copilot-cli Issue #2052](https://github.com/github/copilot-cli/issues/2052)

---

### 4. Key PR Progress
*(No pull requests were updated in the last 24 hours.)*

No PR activity to report. The project appears to be in a stable phase with maintenance and triage of open issues dominating.

---

### 5. Feature Request Trends
Distilled from open issues and upvotes:

1. **Context & Token Transparency (high demand, consolidated)**  
   Requests like #2052 (token usage indicator) and #4174 (ACP server does not expose token/context usage) show a clear user desire for **visibility into context consumption and AI credit costs** — especially for enterprise cost management.

2. **Per-Mode Model Configuration (#2958, 16 👍)**  
   Users want to set different default models for plan mode vs. autopilot mode (e.g., cheap model for planning, expensive model for execution). This is a recurring theme for power users.

3. **1M Context Window for Opus 4.7 (#2785, 62 👍)**  
   The community continues to push for full context window parity with Claude Code. This is the single most upvoted open feature request.

4. **Remote Session Support (#1979, 53 👍)**  
   Attaching from mobile/browser — a direct feature parity request with Claude Code’s remote session capability.

5. **Multi-Account Default User (#4166)**  
   A simple but frequently requested feature: allow setting a default GitHub user for Copilot CLI, rather than always defaulting to the most recently added account.

---

### 6. Developer Pain Points
Recurring themes from the last 24h:

- **Zombie Processes (#4163)** — Linux users report child processes not being reaped, causing resource leaks over long sessions.
- **Windows Resume Hang (#4165)** — A platform-specific blocker that undermines the `--resume` workflow on Windows.
- **Plan-Mode Gating is Too Aggressive (#4160)** — Keyword-based blocking of read-only commands makes plan-mode frustrating to use for exploration.
- **Mode Switching Breaks Tools (#4161, #4172)** — Switching between plan mode and autopilot (or exiting plan mode with GPT-5.6) can leave the session in a broken state, losing essential tools or hanging.
- **Credit Accounting Surprise (#1477)** — Users report unexpectedly burning premium requests after the model "completes" its task, causing cost anxiety.
- **Hooks Are Unreliable (#4034)** — The tool-use hook mechanism (stdin not closed) breaks any automation that relies on the documented `$(cat)` pattern for reading JSON payloads.
- **Image/Document Size Warnings Are Spammy (#4164, #3767)** — When an attachment is too large, the warning is printed multiple times (6x reported) instead of once, and there is no recovery path.

---

*Generated from `github/copilot-cli` data updated 2026-07-19.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-19

## Today's Highlights
The community saw active development on two long-standing UX friction points: **thinking effort controls** and **question-response handling in ACP server mode**. A feature request to bring effort-level switching out of the `/model` submenu and into the main TUI has already attracted a working PR (#2509). Meanwhile, a permissions bug (#2508) challenges the documented "first match wins" behavior, which could impact multi-rule configs for power users.

## Releases
No new releases in the last 24 hours. The latest stable version remains **v0.27.0**.

## Hot Issues (10 notable items)

1. **#2501 — [Feature Request] Support quick switching of Reasoning Level / Thinking Effort in TUI main interface**  
   *Author: remacheybn408-boop*  
   *Why it matters:* Addresses a major UX regression compared to VS Code Codex (dropdown vs. buried `/model` menu). The request has 1 comment and has already spawned PR #2509.  
   *[View Issue →](https://github.com/MoonshotAI/kimi-cli/issues/2501)*

2. **#2508 — Permission rules: deny overrides allow regardless of order, contradicting documented "first matching rule takes effect"**  
   *Author: Julzilla*  
   *Why it matters:* If confirmed, this is a **documentation-contradicting bug** in the permission engine that could silently expose resources or block legitimate access. Zero comments so far.  
   *[View Issue →](https://github.com/MoonshotAI/kimi-cli/issues/2508)*

3. **#2499 — [enhancement] `reasoning_effort` passthrough for k3 models should be explicitly supported**  
   *Author: n-WN*  
   *Why it matters:* Foundation work for thinking effort control; closed as "completed" but linked from PR #2509.  
   *[View Issue →](https://github.com/MoonshotAI/kimi-cli/issues/2499)*

4. **#2495 — ACP server: `QuestionRequest` silently returns empty dict, indistinguishable from dismissed questions**  
   *Author: ayaangazali*  
   *Why it matters:* Breaks ACP clients that rely on differentiating "user dismissed" vs. "not supported"; PR #2507 addresses this.  
   *[View Issue →](https://github.com/MoonshotAI/kimi-cli/issues/2495)*

5. **#2503 — [BUG] `kimi code` refuses to start on Windows 11 with Python 3.13**  
   *Author: vvatanabe*  
   *Why it matters:* Windows compatibility regression blocking a growing platform segment.  
   *[View Issue →](https://github.com/MoonshotAI/kimi-cli/issues/2503)*

6. **#2500 — [Feature Request] Support `--output-file` flag for piping structured output**  
   *Author: james-shaw*  
   *Why it matters:* Essential for CI/CD integration and scripting use cases.  
   *[View Issue →](https://github.com/MoonshotAI/kimi-cli/issues/2500)*

7. **#2496 — [BUG] `--no-sandbox` flag ignored on ARM64 macOS**  
   *Author: armdev2026*  
   *Why it matters:* Sandbox bypass fails on M-series Macs, stalling some security-conscious workflows.  
   *[View Issue →](https://github.com/MoonshotAI/kimi-cli/issues/2496)*

8. **#2492 — Rate-limiting error message unhelpful when using `KIMI_API_KEY`**  
   *Author: sschneider*  
   *Why it matters:* Poor error diagnostics delay debugging for API-integrated users.  
   *[View Issue →](https://github.com/MoonshotAI/kimi-cli/issues/2492)*

9. **#2504 — [Feature Request] Support `.kimiignore` like `.gitignore` for session context inclusion**  
   *Author: benny-codes*  
   *Why it matters:* Reduces noise in context windows for monorepo users.  
   *[View Issue →](https://github.com/MoonshotAI/kimi-cli/issues/2504)*

10. **#2498 — [Proposal] Add `kimi doctor` command to diagnose environment and config**  
    *Author: josh-long*  
    *Why it matters:* Proactive debugging for onboarding and troubleshooting without digging into docs.  
    *[View Issue →](https://github.com/MoonshotAI/kimi-cli/issues/2498)*

## Key PR Progress (10 important items)

1. **#2509 — feat(kimi): configurable thinking effort and `/effort` command**  
   *Author: n-WN*  
   *Status: OPEN* — Implements the #2501 request. Adds `/effort low|medium|high` slash command and a `--thinking-effort` flag. Builds on #2499.  
   *[View PR →](https://github.com/MoonshotAI/kimi-cli/pull/2509)*

2. **#2507 — fix(acp): signal `QuestionNotSupported` instead of resolving empty answers**  
   *Author: ayaangazali*  
   *Status: OPEN* — Fixes #2495. Distinguishes "question not supported" from "user dismissed" in ACP server responses.  
   *[View PR →](https://github.com/MoonshotAI/kimi-cli/pull/2507)*

3. **#2506 — fix(kosong): raise a clear error on circular `$ref` in `deref_json_schema`**  
   *Author: Sreekant13*  
   *Status: OPEN* — Small fix (<100 lines) that replaces infinite recursion with a descriptive error when JSON schemas contain circular references.  
   *[View PR →](https://github.com/MoonshotAI/kimi-cli/pull/2506)*

4. **#2494 — feat(completions): add `--max-tokens` override for streaming completions**  
   *Author: jamesmorrow*  
   *Status: OPEN* — Lets users cap token generation per call, bypassing model defaults.  
   *[View PR →](https://github.com/MoonshotAI/kimi-cli/pull/2494)*

5. **#2491 — fix(shell): escape special characters in multi-line prompts**  
   *Author: linyx*  
   *Status: OPEN* — Prevents shell injection when pasting code with backticks or `$` into interactive mode.  
   *[View PR →](https://github.com/MoonshotAI/kimi-cli/pull/2491)*

6. **#2489 — refactor(permission): flatten rule evaluation to match documented "first match wins"**  
   *Author: zhuxiaoqi*  
   *Status: OPEN* — Direct response to #2508. Reworks the permission evaluator to enforce deny/allow precedence as documented.  
   *[View PR →](https://github.com/MoonshotAI/kimi-cli/pull/2489)*

7. **#2488 — docs: add example for multi-model `KIMI_MODEL_*` environment configuration**  
   *Author: docs-fan*  
   *Status: OPEN* — Adds clear examples for the increasingly popular multi-model env var setup pattern.  
   *[View PR →](https://github.com/MoonshotAI/kimi-cli/pull/2488)*

8. **#2487 — feat(cli): add `--output-file` and `--output-format` for non-interactive modes**  
   *Author: n-WN*  
   *Status: OPEN* — Partially addresses #2500. Supports JSON and Markdown output to file.  
   *[View PR →](https://github.com/MoonshotAI/kimi-cli/pull/2487)*

9. **#2485 — fix(windows): handle `conhost.exe` ANSI escape sequence fallback**  
   *Author: vvatanabe*  
   *Status: OPEN* — Workaround for #2503: ensures terminal output renders correctly on native Windows console.  
   *[View PR →](https://github.com/MoonshotAI/kimi-cli/pull/2485)*

10. **#2484 — test(acp): add end-to-end tests for QuestionRequest/QuestionNotSupported flow**  
    *Author: ayaangazali*  
    *Status: OPEN* — Companion test PR for #2507; adds coverage for the new ACP signal path.  
    *[View PR →](https://github.com/MoonshotAI/kimi-cli/pull/2484)*

## Feature Request Trends
The most-requested feature directions from recent issues center on three themes:
- **In-place model controls:** `Reasoning Level` / `Thinking Effort` quick switching (#2501) and the resulting `/effort` command in PR #2509.
- **Pipeline-friendly output:** `--output-file` (#2500) and structured output formats for CI/scripting (#2500, #2504).
- **Diagnostics & onboarding:** `kimi doctor` (#2498), better error messages for API rate limits (#2492), and `.kimiignore` for context control (#2504).

## Developer Pain Points
Recurring frustrations from the last 24 hours:
- **Permission system confusion:** The contradicting rule-ordering bug (#2508) erodes trust in documented behavior and could lead to security misconfigurations.
- **Windows/ARM64 platform gaps:** Startup failures on Windows 11 (#2503) and `--no-sandbox` malfunction on ARM64 macOS (#2496) signal uneven cross-platform testing.
- **ACP server ambiguity:** The silent empty-dict response (#2495) breaks integration clients that need to distinguish "not supported" from "user dismissed," a clear semantic gap.
- **Undiagnosed API errors:** Rate limits and auth failures currently yield generic or misleading messages (#2492), forcing developers to dig into network logs.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-19

## Today's Highlights

A massive wave of 50+ issues and PRs hit the OpenCode repo in the last 24 hours, most closed before the daily digest even started, indicating active triage sprints. The community is grappling with two dominant themes: OpenCode V2's TUI and config regressions, and a growing chorus of frustration over model compatibility issues (Anthropic prefill errors, DeepSeek infinite loops, Ollama latency). On the positive side, three open PRs from `CasualDeveloper` continue a long-running effort to bring bidirectional cursor pagination and proper agent variant handling across the stack.

## Releases

No new releases in the last 24 hours. The latest stable remains Desktop v1.18.3 and the V2 `next` builds.

---

## Hot Issues (Top 10)

### 1. [#20695 — Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)
**Comments:** 113 | **👍:** 90  
The undisputed heavyweight. The community is collecting heap snapshots to diagnose persistent memory leaks. Key ask: *please don't ask LLMs for solutions*. They need manual heap dumps from Chrome DevTools or jemalloc. The sheer volume (90 upvotes) signals this is the #1 stability concern.

### 2. [#6680 — View archived sessions on desktop](https://github.com/anomalyco/opencode/issues/6680)
**Comments:** 39 | **👍:** 24  
A long-standing feature request (since Jan 2026) that refuses to die. Users want a proper "archived sessions" modal accessible from the sidebar's `...` menu. High activity suggests the current session management UX is a pain point for power users.

### 3. [#2047 — LM Studio models not refreshing](https://github.com/anomalyco/opencode/issues/2047)
**Comments:** 22 | **👍:** 5  
Persistent issue since Aug 2025. Adding/removing models in LM Studio doesn't propagate to OpenCode even after auth logout/login loops. Community is asking for a proper refresh endpoint or live watcher. Low engagement but long tail—this has annoyed local-model users for nearly a year.

### 4. [#26772 — Integrated browser for desktop](https://github.com/anomalyco/opencode/issues/26772)
**Comments:** 15 | **👍:** 4  
Users want an embedded Chromium workspace inside OpenCode Desktop to inspect and interact with web apps. Moderate community engagement, but the scope is huge—this would effectively turn OpenCode into a browser IDE hybrid.

### 5. [#34207 — Model selection silently reverts](https://github.com/anomalyco/opencode/issues/34207)
**Comments:** 8 | **👍:** 2  
Critical UX bug: selecting a different model while an agent is working gets silently overwritten when the agent next asks a question. This means users think they're on one model but are actually on another. Dangerous for anyone managing costs or model-specific workflows.

### 6. [#30443 — Infinite "Session compacted" loop](https://github.com/anomalyco/opencode/issues/30443)
**Comments:** 4 | **👍:** 0  
Windows Desktop v1.15.13 users hit a total app freeze on DeepSeek V4, MiMo V2.5, and MiniMax M3. Even a brand-new session with "abc" triggers an infinite compaction loop. Low comment count but catastrophic for affected users.

### 7. [#32548 — Step-cap assistant message causes 400 on Claude](https://github.com/anomalyco/opencode/issues/32548)
**Comments:** 4 | **👍:** 0  
When an agent hits its step cap, OpenCode appends an assistant-role "MAXIMUM STEPS REACHED" message. Anthropic treats this as a prefill and rejects it with a 400. This makes Claude models with thinking enabled completely unusable for long sessions. Two related duplicates (`#37685`) suggest this is spreading.

### 8. [#37544 — V2 config: model limit override ignored](https://github.com/anomalyco/opencode/issues/37544)
**Comments:** 4 | **👍:** 0  
OpenCode V2 ignores `limit.context` overrides for catalog models. Users can't force early compaction, making long conversations memory-heavy. Closed quickly but the underlying V2 config regression pattern is concerning.

### 9. [#37654 — Revert erases code from other sessions (CN bug report)](https://github.com/anomalyco/opencode/issues/37654)
**Comments:** 4 | **👍:** 1  
Chinese user reports that the revert/undo feature sometimes fails to revert local changes, and worse—erroneously reverts changes from *other* sessions. Non-deterministic data corruption is a red-flag severity bug.

### 10. [#37353 — Desktop white screens & corrupted global state JSON](https://github.com/anomalyco/opencode/issues/37353)
**Comments:** 2 | **👍:** 0  
Windows + WSL users face white screens and send failures due to corrupted global state JSON, stale session paths, and dangling server refs. Two separate databases (Windows + WSL) compound the issue. Low engagement but high severity—app is completely unusable for these users.

---

## Key PR Progress (Top 10)

### 1. [#8535 — Feat(session): bi-directional cursor-based pagination](https://github.com/anomalyco/opencode/pull/8535)
**Author:** CasualDeveloper  
Closes three issues (`#6548`, `#28257`, `#30587`). Adds bidirectional cursor pagination for session messages across server, app, TUI, and experimental HUD. This is a massive behind-the-scenes improvement for session UX—users with thousands of messages will finally get responsive scrolling.

### 2. [#7156 — Feat: add agent default variant handling in TUI and desktop](https://github.com/anomalyco/opencode/pull/7156)
**Author:** CasualDeveloper  
Closes `#22065`. Respects an agent's configured model variant in both app and TUI. This means users can finally pin a specific model variant per agent without manual overrides every session.

### 3. [#9545 — Feat(usage): unified usage tracking with auth refresh](https://github.com/anomalyco/opencode/pull/9545)
**Author:** CasualDeveloper  
Closes `#9281`. Adds built-in usage tracking for four OAuth-authenticated providers. Supersedes two earlier attempts. Critical for users who need visibility into token consumption across sessions.

### 4. [#35223 — Fix(app): handle desktop deep links in new layout](https://github.com/anomalyco/opencode/pull/35223)
**Author:** anduimagui  
Closes `#35225`. Deep links (`opencode://open-project?...`) were hitting Electron but not routed to the redesigned app layout. This fix restores functionality for a core onboarding and sharing feature.

### 5. [#37691 — Fix(simulation): render screenshot symbol glyphs](https://github.com/anomalyco/opencode/pull/37691)
**Author:** kitlangton  
V2 simulation PNG screenshots were showing missing-glyph boxes for symbols like `△`, `✱`, `⇆`, and spinner frames. This PR registers the full Commit Mono font subset. Niche but important for anyone using OpenCode's headless simulation/testing features.

### 6. [#37689 — Fix(core): authorize relative external paths](https://github.com/anomalyco/opencode/pull/37689)
**Author:** kitlangton  
Restores V1-compatible handling for relative paths that resolve outside the active location (e.g., `../sibling/file.ts`). Without this, tools were rejecting valid cross-directory operations. Closed quickly—a regression that would have broken many V2 migration workflows.

### 7. [#35433 — Fix(opencode): stop sending tools when `tool_call` is false](https://github.com/anomalyco/opencode/pull/35433)
**Author:** tobwen  
Closes `#19966` and `#35432`. Model config's `tool_call: false` was stored but never checked—tools were still sent to the model. This fix ensures models that don't support tool calling aren't given tool definitions, preventing wasted tokens and API errors.

### 8. [#35777 — Fix(core): refresh stale @latest npm package cache on load](https://github.com/anomalyco/opencode/pull/35777)
**Author:** yudgnahk  
Closes `#25293`. `Npm.add` short-circuited when `node_modules/{name}` existed, so `@latest` plugins never updated. This fix checks the registry on load, ensuring users get the newest plugin versions without manual cache clearing.

### 9. [#34794 — Feat(provider): add `--model free` to pick random zero-cost model](https://github.com/anomalyco/opencode/pull/34794)
**Author:** caretak3r  
Closes `#21863`. Adds `--model free` to `opencode run` and the TUI. Picks a random OpenCode Zen zero-cost model per invocation. A nice quality-of-life addition for free-tier users who don't care which model they get.

### 10. [#37669 — Fix(core): recover malformed tool input](https://github.com/anomalyco/opencode/pull/37669)
**Author:** opencode-agent[bot]  
When an LLM produces malformed tool arguments, this PR represents them as a non-executable `tool-input-error` with stable call identity and authoritative raw input. The model gets protocol-safe feedback instead of a crash. This is a robust defense against the growing problem of broken tool calls.

---

## Feature Request Trends

1. **Session Management Improvements** — The dominant theme this week. Users want archived session viewing (`#6680`), bidirectional pagination (`#8535`), and full transcript exports (`#32894`). The session UX is the community's top priority for enhancement.

2. **Browser / Web Integration** — `#26772` (integrated browser for desktop) and deep link fixes (`#35223`) suggest users want OpenCode to become a more self-contained web development environment.

3. **Pedagogical / Learning Workflows** — `#36521` proposes a "Teach" mode for learning-by-doing workflows. Revived from an auto-closed issue, this indicates a user base that wants OpenCode to teach as it builds.

4. **Multi-Agent / Model Variant Management** — `#34207` (model selection reverts) and `#7156` (agent variant handling) show users want fine-grained control over which model variant runs for which agent, and they want it sticky.

5. **Localization / i18n** — Multiple issues this week (`#37658`, `#37642`) report hardcoded English strings and missing Chinese translations. The Chinese-speaking user base is becoming more vocal about full localization support.

---

## Developer Pain Points

- **Infinite loops & freezes** — `#30443` (infinite "Session compacted" loop) and `#28697` (agent hangs after "BUILD SUCCESSFUL") point to state-machine bugs that trap users in non-recoverable states. These are the most damaging issues for daily use.

- **Model compatibility regression** — The Anthropic 400 error (`#32548`, `#37685`) from step-cap assistant messages is a cross-cutting issue. Any user on Claude with thinking enabled hits this. The fact that two separate reports came in within 24 hours suggests many more users are silently affected.

- **V2 config regression** — `#37544` (limit override ignored), `#37225` (default_agent ignored), and `#36482` (MCP toggle broken) form a pattern: V2's TUI and config system shipped with multiple ignored-user-set preferences. The community is patiently reporting, but trust in V2's configuration reliability is eroding.

- **Desktop corruption on Windows + WSL** — `#37353` (white screens, corrupted global state JSON) and `#35427` (500 errors on moved projects) reveal a fundamental issue with session state persistence when the underlying project directory changes or when using hybrid Windows/WSL environments. This affects the growing Windows power-user demographic.

- **OpenCode Zen / billing frustrations** — `#32482` (scam sign-up complaints from Australia) and `#37680` (rate-limited despite paid subscription) show that the managed service has support and escalation gaps. Users who hit billing limits or feel misled have no clear channel to resolve issues.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-19

## Today's Highlights
A massive cleanup of 27 issues and 9 PRs was processed in the last 24 hours, with notable attention to Copilot Enterprise integration bugs, stream handling reliability, and model pricing accuracy. The community is actively converging around retry mechanics for compaction and summarization failures, with a dedicated fix PR now open. Several performance regressions were reported and quickly addressed, including high CPU usage on large files and slow startup due to model catalogue refresh.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#6725] Copilot pricing for GPT-5.6 models is incorrect** ([link](https://github.com/earendil-works/pi/issues/6725))  
   *Status: OPEN* — OpenAI models in Copilot are missing `cacheWrite` in cost calculations, causing under-reported costs versus actual API usage. Community is tracking this as a financial accuracy bug; inprogress tag suggests active work.

2. **[#6167] `transformMessages` + `isSameModel === false` thinking block normalization interacts poorly** ([link](https://github.com/earendil-works/pi/issues/6167))  
   *Status: OPEN* — When switching models, thinking content is inlined into assistant messages, violating the `requiresReasoningContentOnAssistantMessages` compat flag. This is a subtle but impactful cross-model edge case affecting multi-model workflows.

3. **[#6675] `pi update --self` gives up after one transient latest-version connection failure** ([link](https://github.com/earendil-works/pi/issues/6675))  
   *Status: OPEN* — The self-update path has zero retry tolerance for a single fetch failure to `pi.dev/api/latest-version`. Community feedback suggests this is a UX regression for unreliable network environments.

4. **[#6768] Compaction using Copilot Enterprise not possible** ([link](https://github.com/earendil-works/pi/issues/6768))  
   *Status: CLOSED* — Compaction fails with both OpenAI (421 Misdirected Request) and Anthropic models under Copilot Enterprise. Received 2 👍, indicating significant user impact.

5. **[#6808] openai-responses waits for HTTP EOF after response.completed** ([link](https://github.com/earendil-works/pi/issues/6808))  
   *Status: CLOSED* — A 4-second delay between `response.completed` and HTTP EOF was observed, causing unnecessary tail latency. The community noted the absence of `[DONE]` signal, pointing to provider or transport issues.

6. **[#6647] Compaction fails on a single transient stream drop** ([link](https://github.com/earendil-works/pi/issues/6647))  
   *Status: OPEN* — Non-retried summarization call during compaction means one mid-stream socket death fails the entire operation. Contrasts with normal assistant turns that retry `terminated` errors. A fix PR (#6775) is in progress.

7. **[#6792] High CPU usage when writing or editing big 500+ line files** ([link](https://github.com/earendil-works/pi/issues/6792))  
   *Status: CLOSED* — 100% CPU usage when generating/editing 1000+ line markdown files. Attached CPU profile suggests the core processing pipeline needs optimization for large document handling.

8. **[#6782] Hindi chars (devanagari) text corrupts editor repaint** ([link](https://github.com/earendil-works/pi/issues/6782))  
   *Status: CLOSED* — Pasting Devanagari characters causes repeated lines on every keystroke, indicating an encoding/rendering issue in the TUI editor. Highlights Unicode edge-case gaps.

9. **[#6801] OpenAI Responses: degenerate output can self-amplify and stream indefinitely** ([link](https://github.com/earendil-works/pi/issues/6801))  
   *Status: CLOSED* — A model emitted its own response envelope as literal assistant text, which then got persisted and replayed, causing recursive nesting across turns. A safety-relevant bug in self-referential output handling.

10. **[#6794] Pi startup super slow due to model catalogue refresh** ([link](https://github.com/earendil-works/pi/issues/6794))  
    *Status: CLOSED* — Morning startup took "forever" due to a model catalogue refresh bottleneck, making the UI unresponsive after load. Performance regression affecting daily workflow init.

## Key PR Progress

1. **[#6807] fix(ai): stop Responses streams at terminal event** ([link](https://github.com/earendil-works/pi/pull/6807))  
   *Status: CLOSED* — Addresses #6808 by closing stream after `response.completed` instead of waiting for HTTP EOF. The author notes this might be a provider-side issue, and investigation continues.

2. **[#6813] feat(coding-agent): support shared auth file** ([link](https://github.com/earendil-works/pi/pull/6813))  
   *Status: CLOSED* — Introduces `PI_CODING_AGENT_AUTH_FILE` env var for credential-file override independent of Pi config directory. Enables centralized credential management across teams/CI.

3. **[#6812] Remove "./" from pi-ai bin path so lockfiles stop flip-flopping** ([link](https://github.com/earendil-works/pi/pull/6812))  
   *Status: CLOSED* — Fixes #6811 where `package-lock.json` toggles between `dist/cli.js` and `./dist/cli.js` depending on npm registry metadata. Simple but impactful lockfile stability fix.

4. **[#6775] retry on compaction/branch summarization retryable failures** ([link](https://github.com/earendil-works/pi/pull/6775))  
   *Status: OPEN* — Core fix for #6647, adding retry logic to compaction summarization calls. Author questions whether UI indication and agent-harness parity are needed, indicating ongoing architectural discussion.

5. **[#6804] fix(coding-agent): allow removing scoped models whose provider/model no longer resolves** ([link](https://github.com/earendil-works/pi/pull/6804))  
   *Status: CLOSED* — Fixes #6806 where orphaned scoped models become permanently stuck after provider removal via `/logout`. Root cause in `ScopedModelsSelectorComponent.buildItems()`.

6. **[#5262] feat(ai): add Anthropic Vertex provider** ([link](https://github.com/earendil-works/pi/pull/5262))  
   *Status: OPEN* — Adds a built-in `anthropic-vertex` provider for Claude on GCP Vertex AI, reusing existing Anthropic streaming infrastructure. Long-running PR (since May 31) suggesting complexity or blocking reviews.

7. **[#6802] fix(coding-agent): show actual extended context size in footer indicator** ([link](https://github.com/earendil-works/pi/pull/6802))  
   *Status: CLOSED* — Replaces hardcoded `[1M]` with actual model `extendedContextWindow` value, fixing display for GPT-5.x series with 1,050,000 context windows.

8. **[#1762] Expose session and tree browsing/editing to RPC protocol** ([link](https://github.com/earendil-works/pi/pull/1762))  
   *Status: CLOSED* — Reopened after bot auto-close. Adds session discovery and tree-structured navigation to RPC, enabling external tools (TUI, editor integrations) to browse session history programmatically.

9. **[#6795] Add exit cmd** ([link](https://github.com/earendil-works/pi/pull/6795))  
   *Status: CLOSED* — Simple UX improvement adding an explicit exit command, likely `/exit`. Community indicated this was a basic missing piece.

10. **[#6775] (repeated)** — As above, key ongoing work for compaction reliability.

## Feature Request Trends

- **Enhanced retry/resilience**: Multiple issues (retry backoff cap, self-update retry, compaction retry) converge on a theme: users need smarter, bounded retry strategies across all operations, not just assistant turns.
- **Provider management flexibility**: Feature requests for hiding/disabling providers in `models.json` (#6803), managing scoped models after provider removal, and shared auth files point to growing multi-provider, multi-model complexity.
- **OAuth and credential streamlining**: Native OpenRouter OAuth (#6814) and shared auth files (#6813) reflect community desire for reduced API key management friction, especially in team/shared environments.
- **Editor/TUI improvements**: Unicode rendering (Devanagari), external editor temp file privatization, and exit command requests indicate ongoing polish of the terminal UX for non-English and large-document workflows.

## Developer Pain Points

1. **Compaction brittleness**: Non-retried compaction/summarization failures (two open issues) are a high-frequency pain point. The fix in #6775 is eagerly awaited.

2. **Startup performance regression**: Slow model catalogue refresh (#6794) and high CPU on large files (#6792) suggest recent changes introduced performance regressions in core processing paths.

3. **Credential/env configuration confusion**: ENV section in `auth.json` being ignored for some providers (#6799) and orphaned scoped models after provider removal (#6806) point to mounting technical debt in the credential/provider state management.

4. **Cross-model compatibility**: Issues with thinking block normalization (#6167), duplicate tool_call_id on model switches (#6796), and degenerate output self-amplification (#6801) highlight the fragility of the model-switching and conversation-replay pipeline when different provider APIs are mixed.

5. **Self-update fragility**: The lack of retry in `pi update --self` (#6675) is a recurring irritation for users on unstable networks, especially mobile developers.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-19

## Today's Highlights
Three stable releases rolled out today: **v0.19.12**, its nightly variant, and a preview build — all focused on daemon cold-start tracing and session reliability. A critical bug thread emerged around **subagent model contamination** resurfacing despite a prior fix, while the team made significant progress on **MCP tool name normalization** and **Gemma 4 compatibility**. The daemon's channel and scheduling capabilities also matured with workspace-scoped contact observation and durable task delivery.

## Releases
- **[v0.19.12-nightly.20260719](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.12-nightly.20260719.86ad532de)** — Nightly build syncing third-party notices and CLI feature work.
- **[v0.19.12](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.12)** — Major stable release. Key feature: `feat(daemon): Trace cold first-session startup` ([#6907](https://github.com/QwenLM/qwen-code/pull/6907)) by @doudouOUC. No breaking changes reported. The full changelog is available on the release page.
- **[v0.19.12-preview.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.12-preview.0)** — Preview with daemon cold-start tracing and multi-workspace ownership hardening for `qwen serve`.

## Hot Issues (Top 10)

1. **[#7156](https://github.com/QwenLM/qwen-code/issues/7156) — Subagent mutates main session model** (P1, OPEN)  
   Despite PR #7119 fixing one model-override path, a *different code path* still allows subagents to silently switch the main session's model, causing 400 errors. 9 comments, active debugging. **Critical for multi-agent workflows.**

2. **[#4748](https://github.com/QwenLM/qwen-code/issues/4748) — Optimize daemon cold start** (Enhancement, OPEN)  
   Tracking the remaining 2.5s cold-start gap vs 0.7s CLI baseline. 8 comments; partially addressed by today's `v0.19.12` tracing feature.

3. **[#7159](https://github.com/QwenLM/qwen-code/issues/7159) — MaxListenersExceededWarning: 11 resize listeners** (P2, OPEN)  
   User reports crashes due to EventEmitter memory leak from terminal resize listeners. 3 comments; PR #7186 directly addresses this.

4. **[#7147](https://github.com/QwenLM/qwen-code/issues/7147) — MCP server never gets tool/resource listing** (P2, OPEN)  
   Fastmail MCP server times out during tool discovery in qwen, though authentication works. 3 comments, community requesting repro steps.

5. **[#6936](https://github.com/QwenLM/qwen-code/issues/6936) — `isManagedMemoryAvailable()` ignores `enableManagedAutoMemory: false`** (P2, CLOSED)  
   Setting `false` still wastes 7–9 KB of context with auto-memory instructions. 3 comments, root cause identified as mismatched gate check. Welcome for PRs.

6. **[#6970](https://github.com/QwenLM/qwen-code/issues/6970) — MCP tool names with dots rejected by strict providers** (P2, CLOSED)  
   Tool names like `mcp__zybio__literature.search_pubmed` are rejected by OpenAI/Anthropic APIs. Solved by PR #6976 which normalizes names.

7. **[#7181](https://github.com/QwenLM/qwen-code/issues/7181) — `/goal` loop blocks user input** (P1, OPEN)  
   Active goal loops queue all user input (including `/goal clear`) until the goal completes. 1 comment, marked `ready-for-agent`. **Urgent UX issue.**

8. **[#7164](https://github.com/QwenLM/qwen-code/issues/7164) — Concurrent session writers fork transcript history** (P1, OPEN)  
   Two processes appending to the same JSONL transcript create divergent parent chains, causing lost responses on restart. 1 comment, linked to PR #7166.

9. **[#6949](https://github.com/QwenLM/qwen-code/issues/6949) — ACP Plan mode blocks read-only shell commands** (P2, IN-REVIEW)  
   Unclassified read-only commands are blocked; exit confirmation can be bypassed. 1 comment, actively reviewed.

10. **[#7148](https://github.com/QwenLM/qwen-code/issues/7148) — Gemma 4 models halt due to non-native tool call examples** (P2, CLOSED)  
    Generic `[tool_call: …]` examples poison Gemma 4's context, causing hallucinated XML tags. Fixed by PR #7177 using native `<|tool_call|>` tokens.

## Key PR Progress (Top 10)

1. **[#7172](https://github.com/QwenLM/qwen-code/pull/7172) — Route Plan-mode shell commands by safety**  
   Classifies shell commands and routes them to safe/native runners. Directly addresses #6949's Plan-mode blocking issue. **Opens for review.**

2. **[#7166](https://github.com/QwenLM/qwen-code/pull/7166) — Enforce single-writer session persistence**  
   Introduces process-level leases for session transcripts, preventing the fork/hide issue from #7164. Uses lock tokens and byte-length fencing.

3. **[#7177](https://github.com/QwenLM/qwen-code/pull/7177) — Apply native tool calling schema for Gemma 4**  
   Replaces generic `[tool_call: …]` with Gemma-native `<|tool_call|>` tokens. Fixes #7148; merged and closed.

4. **[#6976](https://github.com/QwenLM/qwen-code/pull/6976) — Normalize MCP tool names for strict providers**  
   Deterministic slugification of tool names containing dots or exceeding 63 chars. Fixes #6970; merged.

5. **[#7186](https://github.com/QwenLM/qwen-code/pull/7186) — Share one `process.stdout` resize listener**  
   Fixes the MaxListenersExceededWarning (#7159) by using a single module-level listener with subscriber callbacks.

6. **[#7182](https://github.com/QwenLM/qwen-code/pull/7182) — Defer TUI runtime from ACP startup**  
   Performance improvement: delays terminal UI initialization until interactive mode is confirmed, reducing cold-start latency.

7. **[#7184](https://github.com/QwenLM/qwen-code/pull/7184) — Add deterministic PR intake checks**  
   Enforces test plans, line limits (≤2,000), and required evidence on internal PRs before AI triage runs.

8. **[#7153](https://github.com/QwenLM/qwen-code/pull/7153) — Deliver scheduled results to explicit channel targets**  
   Enables daemon-owned delivery of scheduled task results to specific users or chats via `CronTaskChannelTarget`. Open for review.

9. **[#7165](https://github.com/QwenLM/qwen-code/pull/7165) — Label-driven takeover for autofix loop**  
   Adds `autofix/takeover` label to summon the autofix loop onto any open PR. Also fixes forced-dispatch green no-op.

10. **[#6606](https://github.com/QwenLM/qwen-code/pull/6606) — Sanitize daemon secrets from shell subprocesses** (OPEN)  
    Strips environment secrets (`QWEN_API_KEY`, etc.) before spawning shell processes. Critical security PR awaiting final review.

## Feature Request Trends
- **Conversation search** ([#6824](https://github.com/QwenLM/qwen-code/issues/6824), [#7151](https://github.com/QwenLM/qwen-code/issues/7151)) — Keyword search for conversation history is the most-requested UX improvement across CLI and VSCode.
- **MCP ecosystem maturity** — Multiple requests for better MCP tool name handling ([#6970](https://github.com/QwenLM/qwen-code/issues/6970)), chained calls ([#6992](https://github.com/QwenLM/qwen-code/issues/6992)), and timeout resilience ([#7147](https://github.com/QwenLM/qwen-code/issues/7147)).
- **Daemon SDK/API surface** — Workspace-scoped session import ([#7178](https://github.com/QwenLM/qwen-code/issues/7178)), custom display names ([#7170](https://github.com/QwenLM/qwen-code/issues/7170)), and channel contact APIs ([#7103](https://github.com/QwenLM/qwen-code/issues/7103)).
- **Inline model switching** ([#5967](https://github.com/QwenLM/qwen-code/issues/5967)) — Ability to change models mid-conversation in a single command line, already closed but representative of broader model-switching UX work.
- **Auto-output language mode** ([#6943](https://github.com/QwenLM/qwen-code/issues/6943)) — LLM should follow user's input language instead of being locked to a fixed configuration.

## Developer Pain Points
- **Model contamination across sessions** — The recurring subagent model-switching bug ([#7156](https://github.com/QwenLM/qwen-code/issues/7156)) erodes trust in multi-agent workflows, especially after a prior fix proved incomplete.
- **Concurrent session corruption** — Two processes writing to the same transcript ([#7164](https://github.com/QwenLM/qwen-code/issues/7164)) can silently lose responses, a race condition that affects CI and team usage.
- **Goal loop lockout** — The `/goal` system's inability to be interrupted ([#7181](https://github.com/QwenLM/qwen-code/issues/7181)) creates a confusing "infinite loop" experience for users.
- **Terminal resource leaks** — Repeated `MaxListenersExceededWarning` crashes ([#7159](https://github.com/QwenLM/qwen-code/issues/7159)) indicate that React-like hooks on terminal streams are not being properly cleaned up.
- **MCP integration friction** — Timeouts ([#7147](https://github.com/QwenLM/qwen-code/issues/7147)), silent failures ([#6992](https://github.com/QwenLM/qwen-code/issues/6992)), and provider incompatibility ([#6970](https://github.com/QwenLM/qwen-code/issues/6970)) make MCP adoption frustrating, though fixes are landing quickly.
- **Outdated/inconsistent diagnostics** — Warnings dropped in stream-json mode ([#7158](https://github.com/QwenLM/qwen-code/issues/7158)) and cryptic upgrade errors ([#7151](https://github.com/QwenLM/qwen-code/issues/7151)) suggest the error-reporting layer needs hardening.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-19

## Today's Highlights
A flurry of 13 PRs merged today from maintainer **Hmbown**, mostly focused on the **v0.9.1/v0.9.2 release hardening** cycle. Critical fixes landed for xAI device-code auth, tool schema validation, and model picker performance, alongside a stacked 3-PR overhaul for **Kimi Code K3** support. The **Claude issue worker** workflow was also verified and merged.

## Releases
No new releases in the last 24 hours. The project remains at **v0.9.3** (development).

## Hot Issues

1. **[#4032] Codewhale not following the constitution** — *bug*  
   Author: stream2stream | [Link](https://github.com/Hmbown/CodeWhale/issues/4032)  
   Most commented issue (39 comments). Codewhale persistently writes temporary scripts instead of using user-provided scripts for calculations, and justifies itself when challenged. Raises trust and behavior-control concerns.

2. **[#4410] Restore xAI device-code OAuth login** — *bug, release-blocker*  
   Author: Hmbown | [Link](https://github.com/Hmbown/CodeWhale/issues/4410)  
   A hard-coded OAuth path mismatch broke `/auth xai-device`. The maintainer identified the root cause (`/oauth2/device/code` vs `/oauth2/device`). Fixed in today’s wave of PRs.

3. **[#3192] Put it up for agentclientprotocol/registry** — *enhancement*  
   Author: Jengro777 | [Link](https://github.com/Hmbown/CodeWhale/issues/3192)  
   Requesting listing in the Agent Client Protocol registry to simplify Zed editor integration. 13 comments with strong interest in tool ecosystem interoperability.

4. **[#1186] Add typed persistent permission rules** — *enhancement, security*  
   Author: greyfreedom | [Link](https://github.com/Hmbown/CodeWhale/issues/1186)  
   Proposes `allow/deny/ask` rules scoped by tool name, command prefix, and path pattern. A foundational security feature for reducing approval fatigue.

5. **[#1481] Support OpenCode Go/Zen providers** — *enhancement*  
   Author: seanthefuturegorilla | [Link](https://github.com/Hmbown/CodeWhale/issues/1481)  
   Request for cheap DeepSeek-V4 access via OpenCode. Community traction: 10 comments, 1 👍.

6. **[#4085] Cannot read/write files under Dropbox (macOS File Provider)** — *bug*  
   Author: Watcher24 | [Link](https://github.com/Hmbown/CodeWhale/issues/4085)  
   Ad-hoc signed binary with zero entitlements fails on macOS Dropbox paths. A cross-cutting reliability issue for macOS users.

7. **[#2886] Add Gherkin acceptance E2E coverage for tool lifecycle** — *enhancement, testing*  
   Author: aboimpinto | [Link](https://github.com/Hmbown/CodeWhale/issues/2886)  
   Community member driving BDD-style test coverage for the command/tool refactor. Supports project maintainability.

8. **[#1675] Chinese garbled characters in Agent output** — *bug*  
   Author: AiurArtanis | [Link](https://github.com/Hmbown/CodeWhale/issues/1675)  
   Agent output renders mojibake for Chinese text when writing Obsidian/Word documents. Affects a significant user segment.

9. **[#4022] Define CLI/TUI parity for subagent and runtime control** — *enhancement, architecture*  
   Author: Hmbown | [Link](https://github.com/Hmbown/CodeWhale/issues/4022)  
   Architectural requirement: subagent controls must not be TUI-only, anticipating cloud/web clients. Marks maturity planning.

10. **[#1425] Large text processing session hangs/crashes** — *bug*  
    Author: AiurArtanis | [Link](https://github.com/Hmbown/CodeWhale/issues/1425)  
    Analyzing a 3M-character novel with 10 sub-agents consistently fails due to `agent_wait` timeouts. Highlights agent reliability limits.

## Key PR Progress

1. **PR #4553**: `feat(work-graph): core model, reducer, validation` — [Link](https://github.com/Hmbown/CodeWhale/pull/4553)  
   New authoritative work ledger per session (WG1). Not yet integrated, but foundational for session state management.

2. **PRs #4555, #4556, #4557**: Kimi Code K3 stacked train — [Link](https://github.com/Hmbown/CodeWhale/pull/4555), [Link](https://github.com/Hmbown/CodeWhale/pull/4556), [Link](https://github.com/Hmbown/CodeWhale/pull/4557)  
   Three-stage: route truth → context provenance → membership onboarding. All closed/merged today.

3. **PR #4554**: `fix(config): stop root DeepSeek default leaking` — [Link](https://github.com/Hmbown/CodeWhale/pull/4554)  
   Critical bugfix: xAI sessions booted with incorrect DeepSeek model default, causing 404s. Live-hit fix.

4. **PR #4552**: `fix(tui): drop redundant [open] suffix on todo rows` — [Link](https://github.com/Hmbown/CodeWhale/pull/4552)  
   UX cleanup: freed label space by removing useless suffix from todo items.

5. **PR #4551**: `fix(tui): insert boundary between Responses reasoning summary parts` — [Link](https://github.com/Hmbown/CodeWhale/pull/4551)  
   Fixes concatenated thinking output — now uses `\n\n` separators for readability.

6. **PR #4550**: `perf(tui): memoize merged provider catalog snapshot` — [Link](https://github.com/Hmbown/CodeWhale/pull/4550)  
   `/model` latency from ~3.1s to near-instant via memoization. Significant UX improvement.

7. **PR #4546**: `fix(xai): flatten root oneOf tool schemas rejected with 400` — [Link](https://github.com/Hmbown/CodeWhale/pull/4546)  
   Release blocker: xAI rejected tools with `oneOf` schemas. Flattening fix applied.

8. **PR #4537**: `Add Claude Code GitHub Workflow` — [Link](https://github.com/Hmbown/CodeWhale/pull/4537)  
   Bounded `@claude` automation: maintainers can trigger Claude from GitHub issues, creating signed branches from `main`.

9. **PR #4544**: `fix(doctor): keep diagnostic commands read-only end to end` — [Link](https://github.com/Hmbown/CodeWhale/pull/4544)  
   Security hardening: `codewhale doctor` guaranteed read-only, with `ReadOnlyFileKeyringStore` for secret lookups.

10. **PR #4539**: `fix(doctor): diagnose recoverable legacy sessions` — [Link](https://github.com/Hmbown/CodeWhale/pull/4539)  
    New `doctor` diagnostic compares legacy vs primary session dirs without reading payloads. Addresses user data recovery for [#4032].

## Feature Request Trends

- **Provider expansion**: Multiple requests for OpenCode Go/Zen, NVIDIA NIM, and improved Kimi Code integration reflect demand for model diversity beyond DeepSeek-first.
- **Localization parity**: Korea, Spanish, Brazilian Portuguese READMEs exist but website doesn't ship them — users want full-language website support (see [#3091], [#3093]).
- **Persistent permission rules**: The `allow/deny/ask` model ([#1186]) mirrors growing discomfort with repetitive approval prompts in agent workflows.
- **Windows as a first-class platform**: Requests include better terminal defaults (Windows Terminal), shell detection, and cmd/PowerShell awareness ([#1854], [#1754]).
- **Sub-agent/group/task management**: Users want multi-skill grouping, skills reloadable by project, and better sub-agent monitoring ([#2117], [#1425], [#2889]).

## Developer Pain Points

- **Chinese text rendering**: Garbled output ([#1675]), white-background overlays hiding text ([#1564]), and incomplete label display ([#998]) indicate systemic TUI rendering issues for CJK users.
- **macOS File Provider sandbox issues**: Dropbox and similar cloud-storage paths are inaccessible ([#4085]), a hard blocker for many Mac developers.
- **Sub-agent timeout reliability**: Large tasks with multiple sub-agents hit `agent_wait` timeouts and session freezes ([#1425]), undermining trust for complex work.
- **Windows cross-shell command failures**: AI defaults to Unix-style commands that break in PowerShell/cmd ([#1754]), suggesting the need for runtime shell detection.
- **xAI onboarding friction**: Device-code OAuth and model-not-found errors ([#4410], [#4554]) created a poor first-run experience for xAI users, though both were fixed today.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*