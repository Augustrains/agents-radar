# AI CLI Tools Community Digest 2026-08-18

> Generated: 2026-08-18 00:29 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report — AI CLI Developer Tools
**Date: 2026-08-18**

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is in a period of rapid maturation, characterized by intense focus on reliability, multi-agent orchestration, and cross-platform parity. Claude Code leads in community engagement and feature richness, while OpenAI Codex is investing heavily in infrastructure hardening (sandbox security, telemetry, TUI dashboards). Gemini CLI shows strong momentum in subagent reliability fixes, and Qwen Code continues aggressive release cadence with enterprise-focused automation. Cross-cutting concerns across all tools include MCP protocol integration fragility, session state management, Windows platform regressions, and context window management — indicating the ecosystem is transitioning from novelty to production-grade tooling.

---

## 2. Activity Comparison

| Tool | Issues (24h) | PRs (24h) | Release Status | Community Signal |
|------|-------------|-----------|-----------------|------------------|
| **Claude Code** | 10 hot + 50 total | 12 merged/updated | v2.1.234 (stable) | 198👍 top issue; 60 comments |
| **OpenAI Codex** | 10 hot | 12 merged (6 OTel batch) | rust-v0.148.0-alpha.21 | 195👍 top issue; 79 comments |
| **Gemini CLI** | 10 hot | 10 (8 merged) | v0.56.0-nightly | 12👍 top issue; moderate engagement |
| **GitHub Copilot CLI** | 10 hot | 1 | 1.0.80 (no new) | 17👍 top issue; 28 comments |
| **OpenCode** | 10 hot | 10 (active) | No release | 32👍 top issue; 18 comments |
| **Pi** | 10 hot | 10 (active) | No release | 39👍 top issue; 18 comments |
| **Qwen Code** | 10 hot | 10 (active) | v0.21.13 (stable) | P1 regressions; active triage |
| **DeepSeek TUI** | 10 hot | 10 (8 merged) | v0.9.9 | 8 comments max; lower signal |

**Notable**: Kimi Code CLI had zero activity in the last 24 hours.

---

## 3. Shared Feature Directions

| Feature Direction | Tools | Specific Needs |
|-------------------|-------|----------------|
| **Message Queue / Non-blocking Interaction** | Claude Code (#50246, 198👍), OpenAI Codex (queue PR #39092) | Queue follow-ups instead of interrupting active tasks; async submission to existing sessions |
| **Multi-Agent Orchestration** | Claude Code (#28300), OpenAI Codex (#15723, #13491), Gemini CLI (subagent fixes), Pi (#8250), DeepSeek TUI (#5123) | Cross-machine protocols, subagent wake-ups on completion, preventing recursive delegation loops, accurate terminal states |
| **MCP Protocol Reliability** | Copilot CLI (#4439, #4480), OpenCode (#33027, #43074), Claude Code (skill context bloat) | OAuth token refresh, RFC 8414 issuer validation strictness, tools connected but not exposed, serialized token refresh |
| **Configurable Timeouts** | OpenAI Codex (#28969, 195👍), GitHub Copilot CLI (#4506) | Auto-resolve duration control, memory-pressure watchdog tuning |
| **Context Window Management** | Claude Code (#87191, 230k token skill bloat), Pi (#6879, #7995), Qwen Code (#9320, #6806), DeepSeek TUI (#5239) | Proactive compaction, language-aware skill loading, compression reliability, 1M context retention |
| **Session State Integrity** | OpenCode (#43133), Copilot CLI (#4505), Qwen Code (#9320), Claude Code (#86237, #86298) | Liveness checks, resume reliability, no silent message drops, round-trip integrity |
| **Windows Parity** | OpenCode (5+ issues), Qwen Code (#9061 P1), Claude Code (#80444), Copilot CLI (#38518) | Ctrl+V paste, GPU crashes, ARM64 TUI, disk read loops |
| **Terminal UX Polish** | Gemini CLI (#28868), Copilot CLI (#1481), Pi (#8253, #8249), Qwen Code (#9300) | Line-break keybindings, no full-render flashing, alt-screen opt-out, autocomplete spacing |

---

## 4. Differentiation Analysis

| Tool | Feature Focus | Target Users | Technical Approach |
|------|---------------|--------------|-------------------|
| **Claude Code** | Plugin/hook tooling, desktop app robustness, skill context efficiency | Enterprise developers, multi-platform teams | Mature plugin ecosystem, per-project config dirs, heavy community governance |
| **OpenAI Codex** | Infrastructure hardening, sandbox security, TUI dashboard, telemetry | Production engineers, multi-agent workflows | Rust-based, capability dropping, unified HTTP proxy stack, 872K context PR |
| **Gemini CLI** | Subagent reliability, hook system, memory system quality | Developers needing deterministic agent behavior | Nightly release cadence, aggressive bug-fix merging, ACP protocol compliance |
| **GitHub Copilot CLI** | MCP OAuth, plugin marketplace, session restoration | Enterprise orgs (Copilot Business), mixed-model teams | Strict protocol validation, plugin caching, marketplace ecosystem |
| **OpenCode** | V2 rewrite, MCP extensibility, Windows fixes | Cross-platform developers, model-provider agnostic | Shared server data layer, session liveness checks, adapter selection per provider |
| **Pi** | TUI performance, compaction reliability, provider parity | Local-model users, heavy context workloads | Differential rendering, append compaction with cache reuse, OpenRouter benchmarks |
| **Qwen Code** | Autofix automation, multi-channel (Weixin), enterprise review pipelines | Large teams, CI/CD integration, Alibaba ecosystem | Daemon-based serving, review-platform seams, growth-brake philosophy |
| **DeepSeek TUI** | Pricing accuracy, sandbox configurability, i18n | Cost-sensitive users, deep-research workflows | Token-level theme seams, tiered peak/off-peak pricing, fail-closed approvals |

---

## 5. Community Momentum & Maturity

**Highest Momentum (Rapid Iteration):**
- **Claude Code** — Most mature (v2.1.x), deepest community engagement (198👍 issues), but faces Windows desktop stability concerns that could erode trust
- **OpenAI Codex** — Rapid infrastructure evolution (12 PRs/day), clean security posture, but 0.148 release still in alpha; poised for significant stability jump
- **Qwen Code** — Fastest release cadence (v0.21.13), active enterprise feature development, but Windows regressions suggest QA gaps on that platform

**Steady Growth:**
- **Gemini CLI** — High PR-merge rate (8/10 merged), focused bug-fix strategy, smaller but engaged community
- **Pi** — Linux-focused power-user base, strong TUI performance focus, catching up on standards compliance (XDG)
- **DeepSeek TUI** — Budget-friendly positioning, solid release discipline, but CI flakiness is a bottleneck

**Consolidating:**
- **GitHub Copilot CLI** — Low PR activity (1 PR), platform stability focus, community frustration over removed flags; market position relies on GitHub ecosystem integration
- **OpenCode** — High activity but asymmetric (many Windows fixes), V2 rewrite signals architecture pivot; community is engaged but experiencing migration friction

**Stagnant:** Kimi Code CLI — Zero activity, possibly deprioritized by MoonshotAI

---

## 6. Trend Signals

**For Developers:**

1. **MCP is the new API gateway — but it's not ready for production.** Token refresh races (OpenCode), RFC 8414 validation breaking GitLab/Atlassian (Copilot CLI), and tools connected-but-not-exposed (OpenCode) mean MCP adoption requires tolerance for protocol rough edges. If you're building MCP servers, expect to handle OAuth refresh and issuer-validation quirks.

2. **Session state is the new "database."** Every major tool shipped at least one session-related bug this week (dropped messages, stale item IDs, cross-instance injection, lost context after compression). If you depend on session continuity for long-running agent workflows, budget for recovery paths and don't assume resume is atomic.

3. **Context window management is the #1 frustration.** ~230k skill bundles, 2.5x cost penalties from missing cache formats, compaction firing too late (373k tokens before trigger) — the model context is the scarcest resource, and tool vendors are still learning to manage it. Choose tools with proactive compaction and language-aware skill loading.

4. **Windows remains the weak link.** Every major tool has at least one P1 Windows regression (GPU crashes, broken paste, disk loops, ARM64 TUI). If you're a Windows-only developer, expect friction; if you're shipping tools, Windows testing is a market differentiator.

5. **Subagent reliability is the new battleground.** Misreported completion states (Gemini), context misinheritance (OpenAI Codex), read-only self-gates (DeepSeek TUI), 9.5 GiB memory blowups (Claude Code) — multi-agent orchestration is the future, but today's implementations are fragile. Tools that solve subagent determinism will win production adoption.

6. **Configurable timeouts are universally demanded.** Whether it's auto-resolve (195👍), memory-pressure watchdogs, or approval dialogs, developers want control over when agents pause and when they act. Fixed timeouts and silent auto-resolution are trust-eroding.

7. **Pricing transparency builds trust.** The DeepSeek TUI's focus on honest unverified pricing labels and Qwen's AIC display issues signal a broader need: developers need to know what their agent runs cost, in real time, with real accuracy.

8. **Terminal UX is a differentiator, not a detail.** From Shift+Enter (17👍 for 6 months) to full-screen flashing in long transcripts, terminal rendering quality directly impacts developer satisfaction. Tools investing in differential rendering (Pi) and TUI dashboards (Codex) are ahead of the curve.

---

*Report generated from community digest data on 2026-08-18 across 8 active AI CLI tools.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-08-18 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

### #1 — skill-creator fixes (PR #1298, #1099, #1050)
**Status:** All OPEN | **Skill:** skill-creator (meta-skill for building other skills)

The most concentrated development effort in this repository. Three separate PRs address critical bugs in `run_eval.py` and `run_loop.py`: the eval harness reports **0% recall on every query** (issue #556, 12 comments, 7 👍), meaning the description-optimization loop optimizes against noise. Additional fixes cover Windows subprocess crashes (`[WinError 10038]`), stream reading failures, and trigger detection.

- [PR #1298](https://github.com/anthropics/skills/pull/1298) — Full fix: eval artifact installation, Windows streams, parallel workers
- [PR #1099](https://github.com/anthropics/skills/pull/1099) — Windows subprocess pipe fix
- [PR #1050](https://github.com/anthropics/skills/pull/1050) — Windows `claude.cmd` resolution + encoding fixes

**Highlights:** 10+ independent reproductions of the 0% recall bug. Multiple overlapping PRs suggest maintainer coordination needed — the skill-creator tooling is the community's top priority.

---

### #2 — document-typography (PR #514)
**Status:** OPEN | **Skill:** Typographic quality control for generated documents

Prevents orphan word wrap (1–6 words on a new line), widow paragraphs (headers stranded at page bottom), and numbering misalignment in AI-generated documents.

- [PR #514](https://github.com/anthropics/skills/pull/514)

**Highlights:** Addresses a universal pain point — every document Claude generates. Broad applicability across DOCX, PDF, and ODT outputs.

---

### #3 — ODT skill (PR #486)
**Status:** OPEN | **Skill:** OpenDocument text creation, template filling, ODT→HTML parsing

Full support for `.odt`/`.ods` files — creation, template filling, reading, and conversion. Big win for LibreOffice/ISO-standard workflows.

- [PR #486](https://github.com/anthropics/skills/pull/486)

**Highlights:** Signals demand for open-source document ecosystem support alongside the existing DOCX focus.

---

### #4 — DOCX/PDF bug-fix cluster (PR #538, #541, #539)
**Status:** All OPEN | **Skills:** docx, pdf, skill-creator

- [PR #538](https://github.com/anthropics/skills/pull/538) — Fixes 8 case-sensitivity mismatches in pdf/SKILL.md (breaks case-sensitive filesystems)
- [PR #541](https://github.com/anthropics/skills/pull/541) — Prevents `w:id` collisions in DOCX tracked changes (causes document corruption)
- [PR #539](https://github.com/anthropics/skills/pull/539) — Warns on unquoted YAML descriptions with `:` (silent parse failures)

**Highlights:** Real-world reliability fixes, not features. The ecosystem is hitting production-hardening pain.

---

### #5 — self-audit skill (PR #1367)
**Status:** OPEN | **Skill:** Mechanical file verification + four-dimension reasoning quality gate

Audits agent output before delivery: verifies every claimed output file exists, then applies a reasoning audit in damage-severity priority order. Universal across stacks.

- [PR #1367](https://github.com/anthropics/skills/pull/1367)

**Highlights:** Complements the related proposal in issue #1385 (3-gate pipeline). Quality assurance is an emerging category.

---

### #6 — testing-patterns skill (PR #723)
**Status:** OPEN | **Skill:** Comprehensive testing patterns — Testing Trophy model, AAA pattern, React Testing Library, unit/component/e2e

- [PR #723](https://github.com/anthropics/skills/pull/723)

**Highlights:** Covers the full testing stack with philosophy and practical patterns. Test generation is a top community demand.

---

### #7 — ServiceNow platform skill (PR #568)
**Status:** OPEN | **Skill:** Broad ServiceNow platform assistant — ITSM, ITOM, ITAM/SAM, FSM, HRSD, SPM, Vulnerability Response, IntegrationHub

- [PR #568](https://github.com/anthropics/skills/pull/568)

**Highlights:** Extensive enterprise coverage for a single platform. Open since March — indicates large enterprise workflow demand.

---

## 2. Community Demand Trends

Distilled from 15 top issues:

### 🔴 Security & Trust (highest urgency — 43 comments)
[Issue #492](https://github.com/anthropics/skills/issues/492): Community skills distributed under the `anthropic/` namespace enable **trust boundary abuse** — users may grant elevated permissions to skills they believe are official. 2 👍. This is the single most-discussed issue and a governance gap.

### 📤 Org-wide skill sharing (16 comments, 8 👍)
[Issue #228](https://github.com/anthropics/skills/issues/228): Direct skill sharing within organizations — currently requires manual download, Slack/Teams transfer, and manual upload to Settings. A shared skill library or share links would streamline this. **Strong enterprise adoption signal.**

### 🐛 Eval tooling reliability (12 comments, 7 👍)
[Issue #556](https://github.com/anthropics/skills/issues/556): `run_eval.py` never triggers skills — 0% trigger rate across all queries. Makes skill description optimization impossible.

### 🧠 Agent memory & state management (9 comments)
[Issue #1329](https://github.com/anthropics/skills/issues/1329): Proposed `compact-memory` skill — symbolic notation for compact agent state, addressing context-window bloat from prose memory.

### ⚠️ Context window safety (4 comments)
[Issue #1487](https://github.com/anthropics/skills/issues/1487): `claude-api` skill eagerly injects **~156k tokens** — exhausts the context window in a single tool call. Skills need injection-budget awareness.

---

## 3. High-Potential Pending Skills

| PR | Skill | Why it matters |
|---|---|---|
| [#514](https://github.com/anthropics/skills/pull/514) | document-typography | Universal need; improves every generated document |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | Covers full testing stack; strong category demand |
| [#486](https://github.com/anthropics/skills/pull/486) | ODT | Fills open-source document-format gap |
| [#525](https://github.com/anthropics/skills/pull/525) | pyxel (retro games) | Niche but creative; active author (kitao) |
| [#83](https://github.com/anthropics/skills/pull/83) | skill-quality-analyzer + skill-security-analyzer | Meta-skills for QA; aligns with #492 security concerns |
| [#181](https://github.com/anthropics/skills/pull/181) | SAP-RPT-1-OSS predictor | Enterprise predictive analytics on SAP data |
| [#210](https://github.com/anthropics/skills/pull/210) | frontend-design clarity | Revises existing skill for real actionability |

The bug-fix cluster ([#538](https://github.com/anthropics/skills/pull/538), [#541](https://github.com/anthropics/skills/pull/541), [#539](https://github.com/anthropics/skills/pull/539)) will likely merge earliest — small, surgical, and broadly beneficial.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for production reliability — fixing skill-creator's broken eval harness, hardening DOCX/PDF handling against corruption, and closing the `anthropic/`-namespace trust gap — over any single new feature skill.**

---

# Claude Code Community Digest — 2026-08-18

## Today's Highlights

Claude Code shipped v2.1.234 with two quality-of-life improvements: a new environment variable for per-project transcript directory naming and a `selection:clear` keybinding action. Meanwhile, the community is actively discussing a long-awaited message queue mode (198 👍) and a critical Windows desktop app GPU crash that renders the MSIX package unlaunchable, while several reports of cross-session message dropping in the desktop app have surfaced as potential regressions.

## Releases

**v2.1.234** — Two changes:
- New optional `CLAUDE_CODE_PROJECT_DIR_NAME` environment variable for hosts that give each session its own config directory, allowing a short name for the per-project transcript directory.
- Added `selection:clear` keybinding action, enabling users to bind a key to clear an in-app selection.

---

## Hot Issues

### 🔥 Most Discussed

1. **[#50246 — Message queue mode — queue messages instead of interrupting active tasks](https://github.com/anthropics/claude-code/issues/50246)** *(CLOSED)*
   - **60 comments, 198 👍** — The most-upvoted open feature request. Users want to queue follow-up messages while Claude is mid-task rather than forcing an interrupt. The 198 upvotes signal strong demand for non-blocking async interaction. Although closed, this likely means it was triaged internally; community is watching for implementation.

2. **[#80444 — Windows desktop app fatal GPU-process crash leaves MSIX unlaunchable](https://github.com/anthropics/claude-code/issues/80444)** *(OPEN)*
   - **39 comments** — A severe Windows-specific bug where the in-app Browser tab triggers a GPU crash (0x060C201E) that corrupts the MSIX package state (appxState=2), requiring a full Repair. Reproduced across two driver versions. This is a release-blocking-quality issue for Windows desktop users.

3. **[#28300 — Multi-agent collaboration across machines (Agent-to-Agent protocol)](https://github.com/anthropics/claude-code/issues/28300)** *(OPEN)*
   - **38 comments** — A long-standing feature request for distributed agent coordination. Community interest is growing as multi-agent workflows become more central to developer tooling.

### 🐛 Notable Bugs

4. **[#86298 — Cross-session messages silently dropped on Windows desktop app](https://github.com/anthropics/claude-code/issues/86298)** *(OPEN)*
   - **13 comments** — Messages are held for an approval the UI never shows, then expire after ~5 minutes. Marked as a regression since app 1.28929.0. Related to #86237 (below), suggesting a systemic issue with the desktop app's message pipeline.

5. **[#86237 — Cross-session messages render but never reach runtime input queue](https://github.com/anthropics/claude-code/issues/86237)** *(OPEN)*
   - **8 comments** — A sibling regression (2.1.222 → 2.1.227) where messages display in the target session's UI but never actually process. Two separate reports of the same class of bug points to a recent refactor regression.

6. **[#19649 — Model overuses Bash tools when builtin tools (Read/Grep) are better suited](https://github.com/anthropics/claude-code/issues/19649)** *(OPEN)*
   - **27 comments, 97 👍** — Long-running complaint that Claude frequently uses `sed`/`grep` via Bash instead of the purpose-built Read/Grep tools. High upvote count indicates broad frustration with tool-selection quality. Cross-referenced across Bedrock API deployments.

7. **[#64568 — Esc in /btw mode rejects pending tool-use prompt instead of exiting](https://github.com/anthropics/claude-code/issues/64568)** *(OPEN)*
   - **10 comments, 9 👍** — An interaction bug: pressing Esc to exit `/btw` mode gets intercepted by a pending permission prompt, accidentally denying a tool use. Reproduced on macOS. Dangerous because it silently changes outcomes.

8. **[#81343 — Background subagent balloons to 9.5 GiB in ~100s → global kernel OOM](https://github.com/anthropics/claude-code/issues/81343)** *(OPEN)*
   - **5 comments** — A single non-nested background subagent grows to 9.5 GiB RSS in under two minutes and OOM-kills a 15.6 GiB Linux host. Severe memory leak or runaway allocation in the Task tool's background execution path.

9. **[#86865 — Fable 5 thinking blocks come back empty in VS Code extension 2.1.233](https://github.com/anthropics/claude-code/issues/86865)** *(OPEN)*
   - **3 comments, 4 👍** — A regression affecting the new Fable 5 model's reasoning visibility in VS Code. Empty `"thinking":""` blocks on 2.1.233; Opus 5 unaffected. Matters for users who rely on visible reasoning traces for debugging and trust.

10. **[#87191 — /claude-api skill loads entire multi-language bundle (~230k tokens) instead of detected project language](https://github.com/anthropics/claude-code/issues/87191)** *(CLOSED)*
    - **4 comments** — The bundled `/claude-api` skill loads every language's documentation regardless of project context, consuming ~230k tokens. Notably closed — likely a fix is in flight. Related to #63566 (also closed), suggesting the team is actively addressing skill context bloat.

---

## Key PR Progress

### 🛠️ Plugin/Hook Tooling Fixes (Batch from RerankerGuo — all merged 2026-08-17)

These eight PRs harden the plugin development toolkit (`plugin-dev`) and related scripts:

1. **[#83990 — Report missing jq dependency](https://github.com/anthropics/claude-code/pull/83990)** — `test-hook.sh` previously misreported missing `jq` as invalid JSON. Now checks for `jq` upfront and reports the missing dependency clearly.

2. **[#83992 — Assert expected hook decision](https://github.com/anthropics/claude-code/pull/83992)** — Fixes #83800. Adds `--expect allow|deny|ask` flag to `test-hook.sh` so tests can verify a hook *denies* what it should deny, not just that it ran.

3. **[#83993 — Reject self-referential duplicates](https://github.com/anthropics/claude-code/pull/83993)** — Prevents `comment-on-duplicates.sh` from proposing an issue as a duplicate of itself, which previously posted nonsense comments.

4. **[#83995 — Validate label option values](https://github.com/anthropics/claude-code/pull/83995)** — Fixes unbound-variable crashes when `--add-label`/`--remove-label` are called without values, and prevents consuming a following option as the label name.

5. **[#83999 — Validate gh flag values](https://github.com/anthropics/claude-code/pull/83999)** — Closes a validation bypass in the `gh` wrapper where incomplete commands like `gh issue list --limit` slipped through.

6. **[#84003 — Propagate top-level failures](https://github.com/anthropics/claude-code/pull/84003)** — Both duplicate-maintenance scripts now fail with nonzero exit codes instead of silently resolving via `.catch(console.error)`.

7. **[#84004 — Limit frontmatter parsing](https://github.com/anthropics/claude-code/pull/84004)** — Parses only the opening YAML frontmatter block; previously, horizontal rules in Markdown body were misinterpreted as frontmatter delimiters.

### 📦 Packaging & Configuration

8. **[#72451 — Remove dead statsig.anthropic.com from init-firewall.sh](https://github.com/anthropics/claude-code/pull/72451)** — The hostname no longer resolves, causing devcontainer startup failures. Clean regression fix.

9. **[#79131 — Don't abort validate-settings.sh when no lowercase frontmatter keys exist](https://github.com/anthropics/claude-code/pull/79131)** *(OPEN)* — `grep` returning 1 with `set -euo pipefail` kills the script without diagnostic. Fixes silent exits and reports skipped keys.

10. **[#87395 — Prevent model self-invocation of /ralph-loop](https://github.com/anthropics/claude-code/pull/87395)** — Uses the proper `disable-model-invocation` frontmatter field (the previous `hide-from-slash-command-tool` was unsupported and ineffective). Prevents the model from starting a loop without user intent.

---

## Feature Request Trends

1. **Non-Interruptive Interaction (Queue Mode)** — The top-voted request (#50246, 198 👍) seeks a message queue so follow-ups don't derail active tasks. Strong signal for more async, parallel interaction patterns.
2. **Multi-Agent Collaboration** — #28300 continues to attract attention for cross-machine agent-to-agent protocols. The community is preparing for distributed agent orchestration.
3. **Permission Dialog Consistency** — Multiple threads (#73325, #83567) complain about inconsistent keyboard shortcuts across terminal vs. desktop app, and across 2-option vs. 3-option variants. Users want stable muscle-memory mappings.
4. **Skill Context Efficiency** — The `/claude-api` skill loading ~230k tokens (#87191) and unconditional `shared/` inlining (#80190) point to a demand for language-aware, minimal-context skill loading.
5. **Account & Configuration Ergonomics** — In-place email changes (#76624), `$HOME` expansion in permission rules (#87139), and ignored frontmatter fields (#87395) show ongoing friction around configuration UX.

---

## Developer Pain Points

- **Windows Desktop App Stability** — The GPU crash (#80444) that bricks the MSIX package, plus the cross-session message-dropping regressions (#86298, #86237), make Windows desktop feel fragile. Two independent reports of dropped messages suggest a systemic refactor regression in the 2.1.22x range.
- **Accidental Destructive Actions via UI Misdirection** — Esc rejecting tool-use prompts (#64568) and the 1=Approve/Deny split between terminal and desktop (#73325) are dangerous: both silently change outcomes based on muscle memory.
- **Context Window Waste** — Skill bundles loading all languages (~230k tokens) and unconditional `shared/` inlining frustrate users who are conscious of context limits and costs.
- **Memory Blowups in Background Agents** — The 9.5 GiB subagent OOM (#81343) is a stark reminder that background execution paths need tighter resource governance.
- **Tool-Selection Quality** — The 97-👍 complaint (#19649) that Claude prefers Bash over purpose-built tools has gone unaddressed for 7 months. This remains a top quality-of-life issue for efficiency-minded developers.

---

*Digest generated from 50 issues + 12 PRs updated in the last 24h as of 2026-08-18.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-18

## Today's Highlights

The Codex team shipped a substantial infrastructure overhaul this week, routing all telemetry, feedback, and OTLP exports through a unified proxy-aware HTTP client stack, while simultaneously expanding the TUI with a new agents dashboard and interactive task management. A significant sandbox hardening PR drops all Linux capabilities in bubblewrap launch modes, addressing long-standing container escape concerns. Community attention remains focused on configurable auto-resolve timeouts (the top-voted issue this week) and a persistent OAuth token refresh bug for routed MCP servers.

## Releases

- **rust-v0.148.0-alpha.21** — Patch release for the alpha channel. No detailed changelog provided; expect incremental fixes toward the 0.148.0 stable release.

## Hot Issues

1. **[#28969 — Add setting to disable the auto-resolve in 60 seconds for questions](https://github.com/openai/codex/issues/28969)** — 79 comments, 195 👍
   The most upvoted issue this week. Users want configurable timeouts for interactive questions; the current hardcoded 60-second auto-resolve disrupts workflows requiring longer deliberation, especially in complex debugging sessions.

2. **[#17265 — Codex does not auto-refresh routed MCP OAuth tokens even when a refresh token is stored](https://github.com/openai/codex/issues/17265)** — 31 comments, 57 👍
   MCP server integrations break silently when access tokens expire because Codex stores `refresh_token` but never uses it. Tool calls fail mid-task without re-authentication prompts — a critical reliability gap for production MCP workflows.

3. **[#37403 — Desktop cannot resume Remote Control/CLI thread: `already has an active writer`](https://github.com/openai/codex/issues/37403)** — 21 comments, 17 👍
   Regression after the August 7 desktop update breaks the mobile-remote-to-desktop handoff workflow. Users who rely on controlling their Mac from ChatGPT mobile during off-hours are hit hardest; the desktop client claims the thread is already active elsewhere.

4. **[#15723 — Background subprocesses/subagents do not wake the calling agent on completion](https://github.com/openai/codex/issues/15723)** — 18 comments, 8 👍
   Long-running background tasks complete but the parent agent never resumes or receives results. Open since March; the community is increasingly vocal about this blocking multi-agent orchestration use cases.

5. **[#17793 — Backspace deletes more than one character in TUI](https://github.com/openai/codex/issues/17793)** — 16 comments, 5 👍
   Prompt editing in the TUI is unreliable on Kitty and other modern terminals; multi-character deletion makes iterative prompting frustrating. Small but highly visible UX regression.

6. **[#13491 — Forked Worker Inherits Parent User Intent and Misinterprets It as Direct Instruction](https://github.com/openai/codex/issues/13491)** — 10 comments, 11 👍
   Recursive delegation attempts fail because subagents copy the parent's full user context and treat it as their own instructions, causing recursive loops. Open since March with no fix in sight.

7. **[#39059 — GPT-5.6 Codex turns bounded codebase work into self-reinforcing verification layers](https://github.com/openai/codex/issues/39059)** — 3 comments (new)
   Fresh report: the latest model spends excessive turns building verification and governance layers instead of completing the requested code change — a possible prompt/model-behavior regression worth monitoring.

8. **[#38518 — Windows Desktop: persistent 350-800 MiB/s read loop causing system-wide stutter](https://github.com/openai/codex/issues/38518)** — 6 comments
   Switching conversations on Windows triggers a sustained disk read loop that degrades system responsiveness. Severity is high for affected users; the issue is only 4 days old but gaining traction.

9. **[#38350 — Recurring scheduled tasks disable themselves after successful runs without authorization](https://github.com/openai/codex/issues/38350)** — 5 comments
   Scheduled automations silently flip from enabled to paused after executing successfully — a trust-destroying bug for users who depend on unattended recurring tasks. No user action triggers the state change.

10. **[#39085 — Documentation recommends unsafe prefix rules as examples of safe ones](https://github.com/openai/codex/issues/39085)** — 2 comments (new)
    The official auto-review documentation suggests prefix rules that are actually insufficiently scoped, potentially leading users to create sandbox escape vectors. Security-relevant documentation bug.

## Key PR Progress

1. **[#39103 — Drop capabilities from Linux sandbox processes](https://github.com/openai/codex/pull/39103)**
   Hardens the sandbox by passing `--cap-drop ALL` in both bubblewrap launch modes and verifies empty effective/permitted capability sets before executing commands. Significant security improvement.

2. **[#39102 — Raise the GPT-5.6 maximum context window](https://github.com/openai/codex/pull/39102)**
   Allows context-window overrides up to **872,000 tokens** for `gpt-5.6-sol`, `gpt-5.6-terra`, and `gpt-5.6-luna`, with corresponding Amazon Bedrock entries.

3. **[#39094 — Add an agents overview dashboard to the TUI](https://github.com/openai/codex/pull/39094)**
   New `/agents` command opens a full-screen dashboard of loaded root sessions with subagent status, supporting search, navigation, and grouping by project or status.

4. **[#39112 — Make the agents overview an interactive task dashboard](https://github.com/openai/codex/pull/39112)**
   Builds on the dashboard: start tasks, open root sessions, rename tasks, and stop active work directly from the agents overview.

5. **[#39113 — Surface interactive requests in realtime conversations](https://github.com/openai/codex/pull/39113)**
   Mirrors execution, permission, and patch approval requests into active realtime conversations with prompts to review or respond in the app.

6. **[#39101 — Update rmcp to 3.1.2](https://github.com/openai/codex/pull/39101)**
   Upgrades the MCP client library, uses native JSON-RPC decoding (removing a local compatibility layer), and supports OAuth protected-resource metadata.

7. **[#39092 — Add a command to queue messages for existing sessions](https://github.com/openai/codex/pull/39092)**
   New `codex queue --thread <THREAD> --message <TEXT>` command submits messages via the `thread/queue/add` API, resolving sessions by UUID or exact name.

8. **[#39088 — Harden TUI subagent navigation](https://github.com/openai/codex/pull/39088)**
   Standardizes on `/subagents` (removes `/agent` alias), preserves subagent settings when rejoining threads, and routes notifications only to the active thread.

9. **[#39104 / #39105 / #39106 / #39107 / #39108 / #39091 — OTel proxy stack (6 PRs)](https://github.com/openai/codex/pull/39104)**
   A coordinated series routing all telemetry through proxy-aware transports: custom CA support for blocking clients, proxy-aware async/blocking transports, policy routing for OTLP exporters, and Windows elevated-sandbox propagation.

10. **[#39089 — Clarify the external contribution policy](https://github.com/openai/codex/pull/39089)**
    Explicitly states the project prefers detailed issue reports and design discussion over external code changes. Likely a response to community contribution friction.

## Feature Request Trends

1. **Configurable interaction timeouts** — Users repeatedly request control over auto-resolve behavior, approval dialogs, and session watchdogs. The 60-second fixed timeout is the leading pain point (#28969).

2. **Better multi-agent orchestration** — Requests cluster around subagent wake-ups on completion (#15723), preventing recursive delegation loops (#13491), and richer visual task management (#39094, #39112). The TUI dashboard is clearly responsive to this demand.

3. **Mobile/desktop/CLI session convergence** — Users want seamless handoff between ChatGPT mobile, Codex Desktop, and CLI threads with preserved context, project association, and run-location options (#37403, #23418, #32519, #28238).

4. **Observability and control of model behavior** — Opt-in OTel logging of agent responses (#22230, 13 👍), collapsing code snippets in progress output (#32817), and tracking verification-layer overreach (#39059) show a desire for transparency plus noise reduction.

5. **Extended context handling** — Beyond the 872K context-window PR, users are asking for better compaction reliability (#38706) and clearer behavior when contexts auto-compact.

## Developer Pain Points

1. **MCP integration fragility** — Token refresh failures (#17265), stdio server spawning leaks on Windows (#38754), and silent node_repl tool attachment failures on desktop (#33599) make MCP-based workflows unreliable across platforms.

2. **Windows-specific degradation** — Disk read loops (#38518), capability/approval inheritance bugs (#33282), Chrome plugin native messaging host failures (#23283), and MCP process reaping issues (#38754) paint a picture of Windows as the least-polished platform.

3. **Session and migration data loss** — `migrate-rollouts` breaking thread names (#38761) and leaving empty projected history (#38762), plus remote compact 404s (#38706), erode trust in the persistence layer.

4. **TUI/UX regressions** — Backspace over-deletion (#17793), hidden worktree options (#28238), Ctrl+PgUp/PgDown cycling failures (#32878), and `/resume` filter resetting (#36010) indicate accumulating polish debt.

5. **Model behavior unpredictability** — Verification-layer over-engineering (#39059) and subagent context misinheritance (#13491) suggest users are struggling with emergent model behaviors that produce wasted turns or surprising actions.

6. **Credential and rate-limit recognition** — The community is actively asking for reward programs for high-quality bug reports (#37585), signaling a desire for more structured contributor acknowledgment.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-18

## Today's Highlights
The Gemini CLI team shipped a nightly release with SSR Agent fixes and merged six SSR-driven pull requests addressing critical bugs, including subagent termination reason handling and the agent-disabled mode regression. Community attention remains focused on subagent reliability—particularly hangs, misreported success states—and memory system quality issues. Notably, a fix for the widely-reported "subagent reports GOAL success after MAX_TURNS interruption" issue (the top-voted open issue with 12 comments) was merged via PR #28815.

## Releases
- **v0.56.0-nightly.20260817.g9a15c45fb** — Includes SSR Agent fix for composite flag in packages/cli tsconfig (PR #28813).
  - [Release notes](https://github.com/google-gemini/gemini-cli/releases)

## Hot Issues
1. **Subagent recovery after MAX_TURNS reported as GOAL success** — The `codebase_investigator` subagent reports `status: "success"` and "GOAL" termination even when it hit the turn limit without performing analysis. This misreporting undermines trust in agent outcomes. [Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)
2. **Generalist agent hangs indefinitely** — Simple tasks like folder creation hang for up to an hour when delegated to the generalist agent. 8 upvotes indicate broad impact; users can work around by disabling subagent delegation. [Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)
3. **Shell command stuck at "Waiting input" after completion** — Simple CLI commands appear hung after finishing, confusing both users and the agent's own state. [Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)
4. **Subagents running when agents mode disabled** — Since v0.33.0, subagents (e.g., generalist) execute and initialize even when disabled in configuration. Listed with `status/need-retesting`; PR #28867 has been merged. [Issue #22093](https://github.com/google-gemini/gemini-cli/issues/22093)
5. **Auto Memory retries low-signal sessions indefinitely** — Sessions that the extraction agent skips are never marked processed, causing repeated retrieval. [Issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522)
6. **Model creates temp scripts in random locations** — When shell execution is restricted, the model scatters temp files across the workspace, creating cleanup overhead. [Issue #23571](https://github.com/google-gemini/gemini-cli/issues/23571)
7. **Gemini doesn't use skills and subagents proactively** — The model fails to leverage available custom skills (e.g., git, gradle) unless explicitly instructed. [Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)
8. **Browser agent fails on Wayland** — Launching the browser subagent fails with "Termination Reason: GOAL" without useful diagnostics. [Issue #21983](https://github.com/google-gemini/gemini-cli/issues/21983)
9. **400 error when >128 tools configured** — Gemini CLI errors out with excessive registered tools; expected behavior is smart scoping of available tools. [Issue #24246](https://github.com/google-gemini/gemini-cli/issues/24246)
10. **Per-account model availability errors are misleading** — Users on personal accounts get enterprise-specific error messages when a model isn't available. [Issue #24587](https://github.com/google-gemini/gemini-cli/issues/24587) — fix merged via PR #28819.

## Key PR Progress
1. **Fix (22323): Preserve original termination reason during subagent recovery** — Ensures MAX_TURNS and TIMEOUT are reported accurately even when `complete_task` succeeds during the final grace turn. [PR #28815](https://github.com/google-gemini/gemini-cli/pull/28815) — **merged**
2. **Fix (22093): Prevent subagents from running when agents mode is disabled** — Reorders `AgentRegistry.loadAgents` logic so `loadBuiltInAgents()` respects the disabled setting. [PR #28867](https://github.com/google-gemini/gemini-cli/pull/28867) — **merged**
3. **Fix (21783): Emit pending tool call update before requesting permission** — Addresses ACP protocol violation where `session/request_permission` was sent without a preceding pending `tool_call` update. [PR #28870](https://github.com/google-gemini/gemini-cli/pull/28870) — **open**
4. **Fix (23954): Add trailing space to autocomplete suggestions** — Autocomplete now appends a space for executable commands, allowing immediate execution on Enter. [PR #28868](https://github.com/google-gemini/gemini-cli/pull/28868) — **merged**
5. **Fix (21331): Host network resolution for gVisor runsc sandbox** — Resolves IDE companion extension connection failures when `GEMINI_SANDBOX=runsc`; gVisor blocks host TCP. [PR #28869](https://github.com/google-gemini/gemini-cli/pull/28869) — **open**
6. **Fix (14724): Translate compact matchers to compress and update enum** — Converts Claude Code hook matchers (`compact`) to Gemini CLI's `compress`; likely to merge soon. [PR #28871](https://github.com/google-gemini/gemini-cli/pull/28871) — **open**
7. **Fix (24587): Misleading admin error for personal accounts** — Replaces enterprise-specific error messaging with accurate personal-account guidance. [PR #28819](https://github.com/google-gemini/gemini-cli/pull/28819) — **merged**
8. **Fix (22589): Retain executing subagent tool calls in hook state** — Prevents loss of subagent tool calls (e.g., background tasks) before hook state is populated. [PR #28817](https://github.com/google-gemini/gemini-cli/pull/28817) — **merged**
9. **Fix (22588): Fix silent hang in MessageBus.request when publish fails** — Floating promise rejection caused 60-second hangs; rejection is now registered and surfaced. [PR #28816](https://github.com/google-gemini/gemini-cli/pull/28816) — **merged**
10. **Fix (21477): Prevent indefinite TUI hang by adding execution timeouts** — Adds execution timeouts for `getProcessInfo()` on bare Linux terminals, avoiding endless "Initializing..." states. [PR #28812](https://github.com/google-gemini/gemini-cli/pull/28812) — **merged**

## Feature Request Trends
- **AST-aware tooling** — Multiple EPICs explore AST-based file reads, codebase mapping, and search/replace precision (Issues #22745, #22746). The goal is to reduce token noise and improve turn efficiency in large codebases.
- **Subagent self-awareness & configurability** — Requests for agents to understand their own CLI flags, use skills proactively, honor configuration overrides (e.g., `maxTurns` in settings.json), and expose subagent trajectories via `/chat share` for debugging and evals.
- **Memory system hardening** — Demands include deterministic secret redaction before model context, quarantining invalid patch files, and skipping low-signal sessions to avoid retry storms.
- **Risk-averse behavior** — Users want agents to prefer safe operations (no forced git resets) and avoid destructive modifications to persistent resources.

## Developer Pain Points
- **Unclear subagent terminal states** — Misreported statuses (e.g., MAX_TURNS as GOAL success) and missing subagent context in bug reports make debugging difficult.
- **Hangs and stalls** — Recurring issues with interactive prompts (vite scaffolds), shell command completion detection, and indefinite TUI initialization are high-frequency complaints.
- **Configuration not respected** — Agent mode being ignored and browser agent overrides not applying indicate a deeper pattern of settings not being honored.
- **Tool/token bloat** — Errors with >128 tools and reliance on many small text-based files (vs. AST-based methods) pressure context windows and increase latency.
- **Workspace hygiene** — Model-generated temp scripts and unexpected file writes create noise in otherwise clean repos.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**2026-08-18**

---

## Today's Highlights

The Copilot CLI ecosystem is seeing a wave of MCP (Model Context Protocol) integration issues, with OAuth authentication regressions against remote MCP servers (GitLab, Atlassian) being among the most impactful. Users are also reporting significant reliability problems with session restoration, memory-pressure watchdog behavior, and plugin marketplace caching. On the feature side, there's growing demand for plugin dependency management and mid-session instruction reloading.

---

## Releases

No new releases in the last 24 hours. The latest version remains **1.0.80**, referenced in the `account.getQuota` bug report (#4504).

---

## Hot Issues

1. **[#1481 — SHIFT + ENTER should spawn a line break, but executes the prompt instead](https://github.com/github/copilot-cli/issues/1481)**
   - **Status:** Closed | 👍 17 | 28 comments
   - The long-standing keyboard shortcut issue where SHIFT+ENTER (universal in chat apps) executes the prompt instead of inserting a line break, while CTRL+ENTER does the opposite. Was open for 6 months before closing — users are visibly frustrated by the non-standard behavior.

2. **[#4390 — Enabled organization models missing from catalogue (Claude Sonnet 5/Opus 5 and Kimi K3)](https://github.com/github/copilot-cli/issues/4390)**
   - **Status:** Open | 👍 7 | 8 comments
   - Copilot Business orgs explicitly enable models like `claude-sonnet-5` but they don't appear in the CLI's model catalogue, reporting "This model is disabled by your organization." A significant parity gap between Copilot surfaces.

3. **[#4439 — Copilot CLI 1.0.79 rejects GitLab MCP OAuth metadata with RFC 8414 issuer mismatch](https://github.com/github/copilot-cli/issues/4439)**
   - **Status:** Closed | 👍 3 | 5 comments
   - Remote MCP server authentication fails against GitLab Self-Managed due to strict RFC 8414 issuer validation. Closed, suggesting a fix landed or workaround was documented, but the pattern of MCP OAuth regressions continues.

4. **[#4480 — Atlassian MCP OAuth fails with "Incompatible authorization server" — regression from 1.0.71](https://github.com/github/copilot-cli/issues/4480)**
   - **Status:** Open | 👍 6 | 5 comments
   - An explicit regression from 1.0.71 to 1.0.79 — Atlassian's remote MCP server (mcp.atlassian.com) fails OAuth discovery. This is a production blocker for teams using Atlassian's MCP offerings, and the RFC 8414 validation appears too strict.

5. **[#4503 — SDK server reports ready without auth, then Slack session creation fails generically](https://github.com/github/copilot-cli/issues/4503)**
   - **Status:** Open | 5 comments
   - The SDK server reports itself ready before initializing a workspace, leading to cryptic "I couldn't create a session for this chat" failures in Slack. A failure of basic server readiness signaling.

6. **[#4506 — Memory-pressure watchdog force-compacts at 23% context usage, recovers 0.003%, then loops until OOM](https://github.com/github/copilot-cli/issues/4506)**
   - **Status:** Open
   - The memory-pressure watchdog force-compacts conversations when process memory is high, but does so even at ~23% context usage, recovering nearly zero tokens while degrading session quality. A vicious cycle that can terminate long-running sessions.

7. **[#4505 — Resumed session retains stale connection item IDs after interrupted response](https://github.com/github/copilot-cli/issues/4505)**
   - **Status:** Open
   - After resuming a session, every prompt fails with `CAPIError: 400 input item ID does not belong to this connection`. The session does not recover from retries, and even `/fork` doesn't help. A critical data-integrity bug for session continuity.

8. **[#4513 — Plugin marketplace cache ignores `ref` when shared across projects with different branches](https://github.com/github/copilot-cli/issues/4513)**
   - **Status:** Open
   - Git-based marketplace sources are cached by URL/path only, not by branch ref. Projects pinning different branches collide on the same cache entry, loading the wrong marketplace plugins — a subtle but dangerous configuration bug.

9. **[#4509 — `--no-alt-screen` was silently removed — alt-screen is now unavoidable and broken](https://github.com/github/copilot-cli/issues/4509)**
   - **Status:** Open | 👍 1
   - The opt-out flag for alt-screen (fullscreen) mode was removed without deprecation notice. Earlier reports (#1799, #2334) date back to March. For users who prefer inline mode (e.g., in tmux, CI, or embedded terminals), this is a genuine regression with no workaround.

10. **[#4511 — Session AIC display is not reliable (Kimi K3 underestimates real consumption)](https://github.com/github/copilot-cli/issues/4511)**
    - **Status:** Open
    - The reported Agentic Interaction Credit (AIC) count for sessions is wrong, particularly with Kimi K3. For teams tracking usage/costs, this undermines trust in the billing telemetry.

---

## Key PR Progress

Only **1 PR** was updated in the last 24 hours:

1. **[#4510 — Remove GitHub Copilot CLI documentation from README](https://github.com/github/copilot-cli/pull/4510)**
   - **Status:** Open | Author: prioritizedprotection086
   - Removes detailed installation instructions and usage guidelines from the README. No comments yet — likely redirecting users to official docs, but concerning if the intent is to reduce community-accessible documentation.

> **Note:** No other PRs were updated in the last 24 hours. Community PR activity is lower today, likely reflecting a weekend pattern.

---

## Feature Request Trends

From the broader issue set, several clear feature directions emerge:

1. **Plugin ecosystem maturity** — Multiple requests around plugin dependency management ([#4487](https://github.com/github/copilot-cli/issues/4487) — inter/intra marketplace dependencies, similar to Claude Code's model), and repository-level plugin settings applied consistently across modes ([#4507](https://github.com/github/copilot-cli/issues/4507)).

2. **MCP resilience and policy fallback** — [#4512](https://github.com/github/copilot-cli/issues/4512) requests that locally-defined stdio MCP servers run even when the MCP registry policy fetch fails, rather than failing closed.

3. **Session ergonomics** — [#4508](https://github.com/github/copilot-cli/issues/4508) asks for mid-session reload of `.github/instructions/*.instructions.md` files — long-running sessions across many compactions never pick up instruction updates.

4. **Configuration parity** — [#4275](https://github.com/github/copilot-cli/issues/4275) requests `contextTier` exposure as an ACP session config option, matching interactive mode's `/model` picker.

5. **Terminal rendering control** — [#4509](https://github.com/github/copilot-cli/issues/4509) (alt-screen opt-out) and [#4313](https://github.com/github/copilot-cli/issues/4313) (scrolling through conversation history) signal a need for more terminal-behavior customization.

---

## Developer Pain Points

Several recurring developer frustrations are visible across today's issues:

**1. MCP OAuth is fragile and regression-prone.** Issues #4439 and #4480 show RFC 8414 validation breaking against real-world MCP servers (GitLab, Atlassian). The strictness introduced in 1.0.79 broke what worked in 1.0.71 — a compatibility regression that blocks production workflows.

**2. Long-running sessions degrade or break.** #4506 (watchdog loop until OOM), #4508 (stale instructions), and #4505 (stale item IDs after resume) all point at the same pain: sessions spanning days/compactions are unstable.

**3. Hidden or undocumented flag removal.** #4509 shows `--no-alt-screen` removed silently, with the issue having been reported since March. Developers cite the lack of deprecation notices and replacement options as a trust issue.

**4. MCP protocol handling gaps.** #4211 (BigInt serialization failure), #4515 (both `content` and `structuredContent` exposed), and #4512 (fail-closed on registry policy fetch) show the MCP integration is still maturing in edge cases.

**5. Inconsistent behavior across surfaces.** #4507 shows repository-level plugin settings applied in interactive mode but ignored in `copilot -p`, and #4275 notes ACP vs. interactive config gaps — leading to "your config behaves differently depending on how you invoke the CLI."

**6. Keyboard input expectations.** #1481 (SHIFT+ENTER vs CTRL+ENTER) had 28 comments and 17 upvotes over 6 months — a small but vocal cohort of users who expect universal chat-app conventions.

---

*Digest generated 2026-08-18 from github.com/github/copilot-cli activity.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-18

## Today's Highlights

A busy day with no new releases but substantial bug-fix activity. The community reported a high number of Windows-specific issues, ranging from ARM64 TUI failures and broken ripgrep extraction to stuck stub binaries and permission problems. Meanwhile, multiple PRs landed to address core stability concerns — including MCP token refresh serialization, Azure DeepSeek adapter selection, and a critical fix preventing `--continue` from injecting prompts into sessions actively used by other running instances.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#19130 — Windows ARM64 native: OpenTUI fails to initialize with bun:ffi dlopen TinyCC error](https://github.com/anomalyco/opencode/issues/19130)**  
   The 18-comment thread shows a long-running (since March) ARM64 issue. Non-interactive commands work on Windows 11 ARM64, but the TUI crashes on startup via a TinyCC/bun:ffi dlopen error. `👍 12` signals a niche-but-persistent sentiment.

2. **[#43105 — [2.0] BUG: enpoint error](https://github.com/anomalyco/opencode/issues/43105)**  
   User reports `status 410 · Gone: Legacy inference endpoint retired` when using `https://opencode.ai/inference/v1` in nearly every CLI — but it works fine in opencode2 beta. 15 comments suggest a confusing split between v1 (legacy) and v2 (current) endpoints. Closed without code changes.

3. **[#7801 — [FEATURE]: Plan Mode + Question tool can auto switch to Build mode](https://github.com/anomalyco/opencode/issues/7801)**  
   Popular request (`👍 32`) with 11 comments. Users want Plan Mode to automatically transition to Build mode when a clarifying question is answered by the model — reducing friction in multi-step workflows.

4. **[#22861 — Bug: Big Pickle stops response early](https://github.com/anomalyco/opencode/issues/22861)**  
   Community reports Big Pickle truncating responses at the exact same spot repeatedly when asked to describe feature implementations — suggests a deterministic bug (possibly token-limit) rather than flaky truncation.

5. **[#40243 — ChatGPT OAuth rejects GPT-5.6 models for an EU-resident workspace, while official Codex CLI succeeds](https://github.com/anomalyco/opencode/issues/40243)**  
   EU inference residency breaks GPT-5.6 access via OAuth in OpenCode, while the official Codex CLI succeeds. 9 comments, closed — but highlights a compatibility gap with OpenAI's regional data policies.

6. **[#33027 — [BUG] MCP tools connected but not exposed to agent](https://github.com/anomalyco/opencode/issues/33027)**  
   MCP server `pdfrag` connects fine (`tools/list` shows 6 tools) but the agent never sees them. An ongoing integration bug (`OPEN` with 8 comments) that blocks a whole class of MCP-based workflows.

7. **[#24153 — [FEATURE]: Add unarchive/restore for archived sessions](https://github.com/anomalyco/opencode/issues/24153)**  
   `👍 11` — Archiving is currently one-way, and users want a restore path instead of permanently losing sessions from the sidebar. Request dates back to April and remains open.

8. **[#36681 — [Bug] Windows path references and permissions on external directory path not working](https://github.com/anomalyco/opencode/issues/36681)**  
   Windows users struggle with path configs (`external_directory` with backslashes) — docs don't cover Windows path handling. Related upstream: `cmdlet permissions` (#36696) also fail — a double Windows-config whammy.

9. **[#43102 — Opencode is unavailable — Upstream request failed: Endpoint is unavailable](https://github.com/anomalyco/opencode/issues/43102)**  
   Fresh (2026-08-17) report: both models in a new session fail with the same upstream-endpoint error — likely a transient infrastructure failure, but came up again in the same time frame as the endpoint-length confusion.

10. **[#43133 — opencode run --continue injects the prompt into a session actively in use by another running opencode instance](https://github.com/anomalyco/opencode/issues/43133)**  
    `--continue` selects the most-recently-updated session without a liveness check — so a CLI prompt can be silently injected into a foreign active conversation. Easy to trigger if two instances share a project. A PR is already up (see #43140).

---

## Key PR Progress

1. **[#43125 — feat(plugin): expose MCP server transforms](https://github.com/anomalyco/opencode/pull/43125)**  
   Decouples MCP server definitions from config via `State.create`; exposes `list/get/set/update/remove` transforms to Effect and Promise plugins. Registered before external plugins so URL-based policies can mutate fields — major MCP extensibility win.

2. **[#43142 — fix(core): support older previous-channel databases](https://github.com/anomalyco/opencode/pull/43142)**  
   Makes the importer tolerant of older `opencode-next.db` schemas whose `project`/`session` columns are missing or typed differently. Fixes #43139 and #41341 — silent migration failure for long-standing users.

3. **[#43141 — fix(core): disable WAL on network filesystems](https://github.com/anomalyco/opencode/pull/43141)**  
   Detects NFS/SMB/CIFS/9P/FUSE via `statfs` and falls back to rollback journaling. Adds `OPENCODE_DB_WAL` env override — a must-have for multi-machine workflows where WAL corruption is common.

4. **[#43017 — refactor(app): use shared server data](https://github.com/anomalyco/opencode/pull/43017)**  
   Migrates app consumers to the shared server data layer from #42999; removes duplicated app sync, session reducers, and legacy caches. Centralizes location-scoped access and session authority — a big architectural cleanup under the V2 rewrite.

5. **[#43140 — fix(session): skip in-flight sessions in --continue selection](https://github.com/anomalyco/opencode/pull/43140)**  
   Direct fix for #43133: adds a process-liveness check (via SessionStatus) so `--continue` never steals an active session. Community quickly turned a nasty UX bug into a shipped-adjacent patch.

6. **[#43074 — fix(core): serialize MCP token refresh](https://github.com/anomalyco/opencode/pull/43074)**  
   Prevents concurrent MCP clients from exchanging the same rotating OAuth refresh token — which otherwise causes one request to succeed while another fails with `invalid_grant`. Subtle race that surfaces only under moderate load.

7. **[#43136 — fix(ai): settle pending Anthropic tool calls](https://github.com/anomalyco/opencode/pull/43136)**  
   Handles `message_stop` arriving without `content_block_stop`; strictly parses accumulated input before emitting an executable tool call, and preserves malformed local input as a non-executable `tool-input-error`. Robustness fix for Anthropic tool-stream edge cases.

8. **[#43129 — feat(ai): support Vertex request labels](https://github.com/anomalyco/opencode/pull/43129)**  
   Adds billing labels to Vertex Gemini provider options (request-body only; does not affect the Gemini API route). Related to #41932, the V2 protocol-correctness audit tracker.

9. **[#43135 — fix(provider): select Azure DeepSeek adapter](https://github.com/anomalyco/opencode/pull/43135)**  
   Closes #43106 — Azure DeepSeek deployments now use the dedicated `deepseek()` adapter instead of the generic Azure chat/responses adapter, restoring custom `reasoningEffort` variants.

10. **[#37504 — Automated PR cleanup — feat(opencode): add session loop command (updated)](https://github.com/anomalyco/opencode/pull/37504)**  
    Long-stale PR (originally #23575) revived: adds `/loop` command (alias `/proactive`) to run a session until interrupted — a productivity feature that the community has been asking for since mid-summer.

---

## Feature Request Trends

- **Plan→Build auto-switching** (via Question tool) — #7801; high demand, low complexity.
- **Session lifecycle improvements** — #24153 (unarchive/restore), plus #43126 (auto pause/resume on rate-limit reset) and #43133's liveness fix — session state management is the trend.
- **Plugin UI for web/desktop** — #43132 mirrors the TUI plugin API (dialogs, slots, slash commands) — V2 needs parity across surfaces.
- **Multi-step workflow automation** — #37504 `/loop` and #37499 `/workflow` YAML pipelines point to a wider appetite for scriptable, repeatable multi-step tasks.
- **Model-provider parity** — #40243 (EU residency), #43106 (Azure DeepSeek), #43135 (adapter selection) — users want adapter correctness, not just "it kind of works".

---

## Developer Pain Points

- **Windows is a second-class citizen.** Nearly a third of today's top issues are Windows-only: ARM64 TUI crashes (#19130), ripgrep extraction broken by MSIX PowerShell (#40623), failed binary copy on npm install (#41370), broken path/permission configs (#36681, #36696), and OAuth/token issues (#40243). Expect community pushback until Windows parity is treated as a first-class concern.

- **Session state is fragile.** `--continue` hijacking active sessions (#43133), sessions stalling under the new layout (#36731), and unarchive not existing (#24153) paint a picture of session management that lags behind the feature set.

- **MCP tooling still has rough edges.** "Connected but not exposed" (#33027) and token-refresh races (#43074) — the MCP integration works for basic cases but fails at the margins that matter to power users.

- **Rate limits and unknown endpoints.** #43102 (endpoint unavailable), #43126 (rate-limit reset handling), and #43105 (legacy endpoint confusion) — a large bucket of "which endpoint, why 410, and can you just wait for me?" friction.

- **Free-tier model lock-in.** #43054: everything except `hy3-free` and `deepseek flash free` gets a Forbidden error referencing "big-pickle" — no transparency, no fallback — which understandably frustrates users exploring the free tier.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-18

## Today's Highlights

A dense day of fixes targeting provider compatibility and TUI stability. Anthropic refusal fallback (#8017) landed via #8258, addressing compaction failures from API-level refusals. A cluster of PRs around TUI rendering performance (#8253, #8249) targets crashes and flashing in long transcripts. Long-standing issues like nested skills (#6479) and the XDG config spec (#534) finally see fixes.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

**1. [#6879 — [bug] auto-compaction never triggers after context grows past 100% until provider overflow](https://github.com/earendil-works/pi/issues/6879)**  
A 2-hour agentic turn on GPT-5.6-sol grew past the compaction threshold to 373k tokens, and compaction only fired when the API rejected the request. Community is clamoring (18 comments, 17 👍) for proactive compaction checks after every agentic step, not just post-run. This is the most upvoted open issue and a core reliability gap.

**2. [#534 — config folder is out of place on Linux](https://github.com/earendil-works/pi/issues/534)**  
Config lives directly in `$HOME` instead of following the XDG Base Directory Spec. 39 👍, 15 comments — one of the most-liked issues overall. The XDG compliance fix finally appears to be in scope after months of community pushback.

**3. [#8029 — [bug] Very slow performance on moving in prompt editor](https://github.com/earendil-works/pi/issues/8029)**  
A single arrow-up press on a 7,000-line prompt buffer takes 1,650ms. Linear growth in editor navigation latency is a severe quality-of-life bug for multi-file or long-context prompt editing. The TUI performance PRs (#8253, #8249) may partially address this, but it deserves a dedicated fix.

**4. [#7995 — openai-responses: no cacheControlFormat 'anthropic' support](https://github.com/earendil-works/pi/issues/7995)**  
From an 870-trial OpenRouter benchmark: missing Anthropic-style prompt caching in `openai-responses` costs **2.5x** on Claude via OpenRouter. Filed on behalf of an OpenRouter engineer — a data-backed, significant cost issue with high business impact.

**5. [#8028 — [bug] TUI `fullRender` crashes with `RangeError` when rendered output exceeds V8 string limit](https://github.com/earendil-works/pi/issues/8028)**  
A video production agent analyzing many frames hits a V8 string-length `RangeError` in the TUI renderer. This is a hard crash, not a degradation — blocks heavy multimodal workflows entirely. Related to the large-diff TUI crash in #8036.

**6. [#8036 — [bug] Edit tool crashes TUI when rendering a large diff during execution and session resume](https://github.com/earendil-works/pi/issues/8036)**  
A 14.5MB diff from HTML files with very long lines crashed the TUI during edit rendering and again on session resume. The edit completed, but the renderer couldn't handle the output. Doubles as a session-resume reliability issue.

**7. [#3200 — Support video/audio content in prompt command](https://github.com/earendil-works/pi/issues/3200)**  
Users want `prompt` RPC to forward video/audio alongside existing image support for multimodal models (Gemma 4, GPT-4o). A clear extension of the multimodal roadmap, 5 👍 and active discussion.

**8. [#8166 — custom message injected mid-tool-batch breaks tool_calls→tool adjacency (DeepSeek 400)](https://github.com/earendil-works/pi/issues/8166)**  
An extension calling `sendMessage` with `triggerTurn: false` mid-tool-batch breaks message ordering — every subsequent turn fails with DeepSeek's 400. A tricky extension-API contract issue that can brick sessions permanently.

**9. [#7756 — detectInstallMethod mislabels non-pnpm installs under PNPM_HOME](https://github.com/earendil-works/pi/issues/7756)**  
Installs sharing `PNPM_HOME` get mislabeled as pnpm-managed, then wrongly rejected. Confusing error text ("not managed by global package manager") for users who never touched pnpm. Small but annoying edge case at install time.

**10. [#8252 — pi crashes when tmux resizes the pane to 1 column](https://github.com/earendil-works/pi/issues/8252)**  
Pi exits with code 1 when tmux reports a terminal width of 1 — the spinner's width check trips. Hit six times in a few days by one user with dual-attached tmux clients. Terminal-edge-case crashes like this erode trust in the TUI.

---

## Key PR Progress

**1. [#8258 — fix(coding-agent/ai): anthropic refusal error and fallbacks](https://github.com/earendil-works/pi/pull/8258)**  
Fixes #8017: reproduces the compaction failure live on `claude-fable-5` (Anthropic returned `stop_reason: "refusal"` with `reasoning_extraction` during summarization). Adds API-level `allowed_fallback_models` metadata to the generated model registry — critical for compaction reliability on refusal-prone models.

**2. [#8255 — fix(coding-agent): load nested markdown skills](https://github.com/earendil-works/pi/pull/8255)**  
Fixes #6479: nested standalone skills at `~/.agents/skills/third-party/child-skill.md` were silently skipped because discovery only handled recursive `SKILL.md` directories. Straightforward fix for a long-standing pain point.

**3. [#8253 — fix(tui): avoid full-screen flashing when content changes above the viewport in long transcripts](https://github.com/earendil-works/pi/pull/8253)**  
Differential rendering only handled visible viewport changes; edits above streaming content in 10k+ line transcripts cleared and reprinted everything — visibly flashing. This is a serious UX win for long-session users.

**4. [#8262 — feat(coding-agent): dispatch hooks on every turn-start path (cancellable turn preflight)](https://github.com/earendil-works/pi/pull/8262)**  
`sendCustomMessage(triggerTurn: true)` skipped the `input` hook and `before_agent_start` entirely. This PR dispatches hooks on every turn-start path, including a cancellable preflight — closes a real extension-API gap.

**5. [#8120 — feat(coding-agent): add experimental append compaction](https://github.com/earendil-works/pi/pull/8120)**  
Append compaction reuses the active system prompt, tools, and routing session so the compacted prefix can reuse provider prompt caches. Experimental via `PI_EXPERIMENTAL=1`; standalone remains default. This could meaningfully cut compaction costs.

**6. [#8254 — fix(ai): prevent copilot policy login rate limits](https://github.com/earendil-works/pi/pull/8254)**  
Addresses #7850: fetches the account model catalog before policy updates, updates only known/tool-capable/unconfigured models, retries throttled login requests with bounded delay. A pragmatic fix for a rate-limit footgun.

**7. [#8250 — fix(coding-agent): make subagent progress and failures reliable](https://github.com/earendil-works/pi/pull/8250)**  
The subagent example could report "done" while still working, lose failure details, and return success-looking results on failure. Also addresses tool-result size limits for chain outputs. Improves observability for the subagent pattern.

**8. [#8240 — fix(ai): align Qwen Token Plan model catalogs](https://github.com/earendil-works/pi/pull/8240)**  
Unifies `qwen-token-plan` and `qwen-token-plan-cn` on one shared eight-model allowlist (including `deepseek-v4-pro-0813` and `deepseek-v4-flash-0731`), keeps the individual plan separate. Clean catalog hygiene.

**9. [#8257 — Skip project-agent confirm when project is already trusted](https://github.com/earendil-works/pi/pull/8257)**  
The subagent extension prompts for project-local agents on **every** run, even when the project is already in `~/.pi/agent/trust.json`. Removes redundant confirmation dialogs for trusted repos — a small but daily-annoying friction point.

**10. [#8249 — fix(coding-agent,tui): refresh theme-derived text on invalidation](https://github.com/earendil-works/pi/pull/8249)**  
Clears Markdown's cached default-style prefix on invalidation, rebuilds the startup header, and recomputes mounted warning text when the active theme changes so ANSI colors don't go stale. Theme-switching reliability across TUI components.

---

## Feature Request Trends

- **Proactive resource management**: The #6879 cluster shows the community wants compaction checks *during* agentic runs, not only after. Local providers can still overflow between tool turns (#8229) — same theme.
- **Provider surface parity**: A steady stream of requests to align catalogs (GLM-5.3 thinking levels #8190, GLM-4.6V model addition #8220, Qwen Token Plan alignment #8194) plus caching support parity across API surfaces (#7995, #7996).
- **Multimodal expansion**: Video/audio in the prompt command (#3200) and vision models in coding plans (#8220) — multimodal coding-agent workflows are a clear directional ask.
- **Resilience and recovery**: Automatic session resume after rate-limit resets (#8277) and PR-discussion-aware reviews (#8280) — the community wants more automation around failure handling and context gathering.
- **XDG and standards compliance**: #534's popularity (39 👍) signals Linux users expect platform conventions, not just working paths.

---

## Developer Pain Points

1. **Context window edge cases**: Compaction firing too late (#6879), overflowing between tool turns (#8229), and Anthropic refusals breaking summarization (#8017) — context management is the single most active pain cluster.
2. **TUI fragility with large payloads**: `RangeError` on large renders (#8028), crashes on 14.5MB diffs (#8036), and slow prompt-editor navigation (#8029) — the TUI breaks down exactly when power users need it most.
3. **Provider API quirks**: From missing `cacheControlFormat` (2.5x cost penalty, #7995) to signed-text replay gaps (#7994) and root-composed tool schemas being rejected by Bedrock (#8279) — model-catalog and API-surface gaps translate directly into user-facing failures.
4. **Extension API contract surprises**: Hooks not firing on all turn paths (#8166, #8262), `agent_end` firing too early (#7350, fixed in #8242), and no `compaction_failed` event for extensions (#8175, fixed in #8241) — extension developers are discovering hidden contracts the hard way.
5. **Linux desktop friction**: XDG compliance (#534), SELinux `:Z` volume mappings (#8276), and terminal-specific bugs like Shift+Enter in Konsole (#8278) — desktop-Linux users hit recurring environment-specific issues.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-18

## Today's Highlights

Qwen Code v0.21.13 shipped with two notable UX improvements: Web Shell composer now supports drag-and-drop/paste for text file attachments, and users can fork conversations from any Assistant response. The team also ran four full end-to-end SWE-bench + Terminal-Bench validation suites (500 + 89 benchmarks, all passing), confirming release-stability after the DSW Harbor workflow fixes. On the automation front, significant engineering effort is concentrated on hardening Qwen Autofix and review pipelines against event storms, runner capacity waste, and flaky gates.

## Releases

**v0.21.13** — Released 2026-08-17 (nightly: v0.21.11-nightly.20260817.195128a17a)
- Web Shell composer: drag-and-drop, paste, and attach text files as named attachments alongside images ([#9180](https://github.com/QwenLM/qwen-code/pull/9180))
- Fork conversations from any specific Assistant response
- Autofix improvements: deny-by-default footprint gate, positional window censuses ([#9156](https://github.com/QwenLM/qwen-code/pull/9156))
- Four successful full SWE-bench Verified (500) + Terminal-Bench 2.0 (89) end-to-end validation runs, all passing

## Hot Issues

1. **[#9296](https://github.com/QwenLM/qwen-code/issues/9296) — Qwen Autofix: review-event storms and duplicate address dispatch waste runner capacity** (P1)  
   This is the highest-signal infra issue this week. Analysis of ~500 autofix runs showed 59% cancelled, with reviews on closed/merged PRs still triggering runs and duplicate dispatch squandering CI resources. The maintainers are actively restructuring the pipeline — a key reliability concern for large teams.

2. **[#9061](https://github.com/QwenLM/qwen-code/issues/9061) — Ctrl+V paste completely unresponsive in CLI on Windows (regression since 0.21.x)** (P1)  
   A breaking Windows regression across versions 0.21.1–0.21.11 (working on 0.21.0). Unresolved for 5 days and generating engagement — likely a top-priority fix for the next release.

3. **[#9324](https://github.com/QwenLM/qwen-code/issues/9324) — Messages delivered in multiple copies without user redirection** (P3)  
   Qwen Desktop Code (Qwen 3.8 Max) reports receiving messages multiple times mid-turn, interrupting focus. A Curious session-duplication bug that affects conversation quality in the desktop client.

4. **[#9320](https://github.com/QwenLM/qwen-code/issues/9320) — Lost context after /compress-fast and /rewind?** (P2)  
   User compressed 102k→87k tokens, launched a new llama-server, and context was lost. This is a follow-on to the known compression accuracy discussion — points to deeper session-resume issues.

5. **[#8316](https://github.com/QwenLM/qwen-code/issues/8316) — Prompt not restored to input box when canceling (ctrl+c)** (P2)  
   Two-week-old bug: canceling a prompt erases the text from the input box, forcing users to retype. Simple-to-fix but high-frequency annoyance during long agent runs.

6. **[#9307](https://github.com/QwenLM/qwen-code/issues/9307) + [#9353](https://github.com/QwenLM/qwen-code/issues/9353) — Weixin channel fixes and enhancements** (P1/P2)  
   Weixin integration has two open items: 64-bit message ID overflow beyond `Number.MAX_SAFE_INTEGER` (data corruption), and typing indicator expiring during long turns (user-visible state loss). An active channel with real production users.

7. **[#8051](https://github.com/QwenLM/qwen-code/issues/8051) — Bound multi-workspace daemon resource usage** (P2, tracking)  
   The daemon limits workspaces/sessions by count but not by bytes (request bodies, WebSocket assembly, etc.). Community continues to push for memory-bounded operation — critical for production `qwen serve` deployments.

8. **[#9300](https://github.com/QwenLM/qwen-code/issues/9300) — VP mode: content not bottom-aligned, blank space above composer** (P2)  
   A rendering regression in default terminal-buffer mode with visible layout gap. Minor but clips everyday usability.

9. **[#6806](https://github.com/QwenLM/qwen-code/issues/6806) — Status line context percentage doesn't refresh after /compress** (P2)  
   Token usage display stays stale after compression until next model request. Persistent issue (open since July 13) — feels like an easily-fixable feedback bug that erodes trust in compression features.

10. **[#9290](https://github.com/QwenLM/qwen-code/issues/9290) — Interactive session crashes on errored agent-team tabs** (P2, CLOSED)  
    Selecting a teammate tab that errored crashes the session. Closed — good sign the multi-agent team runtime is stabilizing after last week's prompt-contradiction fixes.

## Key PR Progress

1. **[#9303](https://github.com/QwenLM/qwen-code/pull/9303) — Bound daemon transcript retention to stop renderer OOM crashes**  
   Fixes web-shell memory exhaustion by releasing raw replay snapshots after injection and applying the same block caps to replay rebuilds as live growth. A critical stability fix for long-running sessions.

2. **[#9297](https://github.com/QwenLM/qwen-code/pull/9297) — Make the brake's BLOCKED handoff a first-class round outcome**  
   Fixes the autofix growth-brake flow where following instructions produced "finished without required output file(s)" errors. Makes the documented handoff path actually executable by the agent.

3. **[#9342](https://github.com/QwenLM/qwen-code/pull/9342) — Clear the deferred-suggestion backlog from #9175's review rounds**  
   Applies 19 deferred review findings (none critical) from 15 review rounds. Half are behavior fixes including a safety-shaped API — shows disciplined backlog hygiene under the one-blocker-per-round policy.

4. **[#9247](https://github.com/QwenLM/qwen-code/pull/9247) — Budget the composed review body against GitHub's 65,536-char limit**  
   Smart engineering: trims the Chinese translation fold first (no content loss) before dropping English content. This avoids silent review-posting failures and is a proper edge-case fix.

5. **[#9130](https://github.com/QwenLM/qwen-code/pull/9130) — Deterministic flakiness gate for sandboxed verification**  
   Re-runs added/modified unit tests N times (default 5, clamp 2–10) in CI to catch flaky tests deterministically. Solid investment in debuggable, reliable CI.

6. **[#9262](https://github.com/QwenLM/qwen-code/pull/9262) — Audit the approach instead of stopping on growth-budget breach**  
   Changes takeover-round behavior: instead of cold-stopping on budget breach, the agent audits the change's approach. Represents a meaningful philosophy shift in the automation loop — less brittle, more thoughtful intervention.

7. **[#9226](https://github.com/QwenLM/qwen-code/pull/9226) — Aone Code read path (second review-platform provider)**  
   Adds `gitlab.alibaba-inc.com` detection to the review platform seam — enabling Alibaba-internal repos to use the same review tooling. Important for enterprise adoption.

8. **[#9092](https://github.com/QwenLM/qwen-code/pull/9092) — Resume an interrupted PR review from its on-disk state**  
   `fetch-pr --resume` validates on-disk state against its own facts before continuing. Critical for long-running review automation that currently dies with failures.

9. **[#9364](https://github.com/QwenLM/qwen-code/pull/9364) — Make serve new-file mode configurable (`QWEN_SERVE_NEW_FILE_MODE`)**  
   Addresses [#9250](https://github.com/QwenLM/qwen-code/issues/9250): lets `qwen serve` honor umask-derived modes instead of hard-coded owner-only `0600`. Direct community-driven fix; nice quick win.

10. **[#8992](https://github.com/QwenLM/qwen-code/pull/8992) — Add MCP 2026 core and WebShell Apps host**  
    First slice of MCP 2026 client support: modern protocol negotiation, `ui://` tool metadata preservation, HTML resource validation. Forward-looking integration for the next protocol generation.

## Feature Request Trends

**Response summarization:**
- **MCP 2026 protocol support** — Active development for next-gen Model Context Protocol with Apps extension ([#8992](https://github.com/QwenLM/qwen-code/pull/8992))
- **Session-level job control** — Scheduled tasks with existing sessions, daemon resource bounding, session rotation for channels ([#8906](https://github.com/QwenLM/qwen-code/issues/8906), [#8051](https://github.com/QwenLM/qwen-code/issues/8051), [#8927](https://github.com/QwenLM/qwen-code/pull/8927))
- **Direct daemon-to-channel file delivery** — Outbound files to Weixin via `[FILE: /path]` markers ([#9352](https://github.com/QwenLM/qwen-code/issues/9352))
- **Export/archive improvements** — Expand/collapse all in HTML exports, cross-host transcript contracts ([#9367](https://github.com/QwenLM/qwen-code/pull/9367), [#9354](https://github.com/QwenLM/qwen-code/issues/9354))
- **Dynamic provider model lists** — Fetch ModelStudio Token/Coding Plan models from API instead of hardcoding ([#9368](https://github.com/QwenLM/qwen-code/issues/9368))
- **Unified web-shell chat panel** — Consolidating chat panel across web-shell, VSCode webview, desktop — dormant but still discussed ([#5883](https://github.com/QwenLM/qwen-code/issues/5883))

## Developer Pain Points

1. **Compression reliability** — Three separate issues this week on `compress`/`compress-fast`: context loss after `/rewind`, incorrect usage reports ([#9309](https://github.com/QwenLM/qwen-code/issues/9309)), stale UI stats ([#6806](https://github.com/QwenLM/qwen-code/issues/6806)), and lost sessions after model switches. The community is actively testing these workflows and finding them unstable at the edges.

2. **Windows platform regressions** — Ctrl+V paste broken in 0.21.x ([#9061](https://github.com/QwenLM/qwen-code/issues/9061)) is a standing P1. Combined with recurring multi-copy message bugs in the desktop client, Windows users seem to be getting testing-short shrift.

3. **Autofix reliability and stewardship** — A cluster of PRs (wenshao's autofix/takeover series) is actively hardening the Qwen Autofix bot: event storms, runner waste, flaky gates, closed-PR triggers. The bot is aggressive and can cancel ~59% of runs — visibility into why runs cancel is a real concern for teams adopting it.

4. **Daemon resource limiting** — Persistent demand for bounded memory/CPU in `qwen serve` beyond count-only limits. Production users (and reviewers) want byte-level control ([#8051](https://github.com/QwenLM/qwen-code/issues/8051), [#8091](https://github.com/QwenLM/qwen-code/issues/8091)).

5. **Terminal UX regressions (non-Windows)** — "New version fields cannot be copied" ([#9315](https://github.com/QwenLM/qwen-code/issues/9315)), blinking/rendering issues ([#3806](https://github.com/QwenLM/qwen-code/issues/3806)), and VP-mode layout gaps ([#9300](https://github.com/QwenLM/qwen-code/issues/9300)) suggest the rewritten terminal interaction layer still has rough edges several versions in.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-18

## Today's Highlights

v0.9.9 shipped as a "truth-and-resilience" release, fixing a critical session-wedge bug when the host exhausts disk/descriptors and making unverified pricing/telemetry defaults honestly labeled. Concurrently, significant work landed on internationalization (retiring `isZh` branches in the web dictionary spine, expanding docs to 8 partial locales) and the DeepSeek Harness (DSH) integration (Codewhale palette via token-level theme seam, ambient ocean scene, tiered peak/off-peak pricing per turn). The release train also saw CI turn red on both platforms across four completed runs, with a separate docs-lint failure forcing hotfixes.

---

## Releases

**v0.9.9 — Truth and Resilience** ([PR #5476](https://github.com/Hmbown/CodeWhale/pull/5476))

- Shell tool can no longer wedge a session when host runs out of disk/descriptors (#5465)
- Unverified context windows / output ceilings / telemetry defaults labeled honestly
- Live pricing unverifiable path fixed — session cost no longer stuck as `unverified_live_pricing` when pricing endpoint returns 503 (#5402)
- DeepSeek V4 tiered peak/off-peak pricing resolved per turn (#5470)
- DSH: Codewhale palette via `overrideTokens` (#5469), ambient ocean scene (#5484)
- Model catalog currency sweep (#5485), website copy rewrite (#5483)
- Community fixes: config casing resolution (#5475), noisy web-tool result compaction (#5474)
- Two follow-up hotfixes: rustdoc bare-URL lint fix (#5489), CHANGELOG addenda (#5487, #5477)

---

## Hot Issues

1. **[#5424 — v0.9.7: Codewhale TUI crashing after ~1 minute of prompt/wait](https://github.com/Hmbown/CodeWhale/issues/5424)** — CLOSED (7 comments). Reproducible exit-after-wait regression. High severity: crash on normal use, not edge case.

2. **[#5056 — Flaky verifier background tests + /workspace-sensitive fixtures](https://github.com/Hmbown/CodeWhale/issues/5056)** — OPEN (8 comments). Two documented flakes under full-suite parallelism, plus 12 untriaged `#[ignore]` tests. CI reliability is a persistent drain.

3. **[#5324 — Agent tool schema too complex (32 fields, 0 required, 8 actions)](https://github.com/Hmbown/CodeWhale/issues/5324)** — CLOSED (8 comments). Models error on the oversized schema. Higher-level problem: schema must stay model-parseable, not just spec-correct.

4. **[#1425 — 300万字小说分析后会话卡死 (agent_wait timeout)](https://github.com/Hmbown/CodeWhale/issues/1425)** — OPEN (7 comments). Large text jobs spawn 10 sub-agents; `agent_wait` timeouts interrupt sessions. Big-context workflows still not reliable for heavy parallel fan-out.

5. **[#5123 — Agent spawn: read-only builder blocks self-gates](https://github.com/Hmbown/CodeWhale/issues/5123)** — OPEN (7 comments). Live dogfood failure: delegate labeled `builder` gets read-only tool contract, then reports BLOCKED. Contradiction between role label and live tool permissions.

6. **[#1651 — VS Code crashes when YOLO Agent runs test scripts](https://github.com/Hmbown/CodeWhale/issues/1651)** — OPEN (6 comments). Autonomous test execution with DeepSeek v4-pro/flash crashes the host editor. Still unresolved after three months.

7. **[#1829 — SSH exit code 255 (sandbox TCP 22 egress blocked)](https://github.com/Hmbown/CodeWhale/issues/1829)** — OPEN (6 comments). Sandbox silently blocks outbound SSH/SCP; user only sees generic exit code. Diagnosability problem, not just connectivity.

8. **[#5360 — One-shot approval outcomes: durable and fail-closed](https://github.com/Hmbown/CodeWhale/issues/5360)** — OPEN (1 comment). Mining `deepseek-harness` 0.1.0-rc.5 found a better approval pattern: every ask/decision pair written to session log, fail-closed. Adoption in-flight via PR #5491.

9. **[#4683 — Wrong DeepSeek completions URL (flaky)](https://github.com/Hmbown/CodeWhale/issues/4683)** — OPEN (4 comments). `https://api.deepseek.com/v1/chat/completions` fails intermittently after long-running asks. User-visible network flake, still needs-info.

10. **[#5403 — main red on both platforms across all four completed runs](https://github.com/Hmbown/CodeWhale/issues/5403)** — OPEN (3 comments). macOS `plugin_e2e_acceptance` + Windows NSIS provisioning failing. CI is a bottleneck; release confidence degrading.

---

## Key PR Progress

1. **[#5476 — release: 0.9.9](https://github.com/Hmbown/CodeWhale/pull/5476)** — CLOSED. Truth-and-resilience theme; fixes critical shell-wedge bug, honest unverified labels, per-turn tiered pricing.

2. **[#5490 — route shared components' locale picks through pickText](https://github.com/Hmbown/CodeWhale/pull/5490)** — CLOSED. Retires 9 remaining `isZh` ternaries in shared components; 8 partial locales (ja/vi/ko/ru/uk/es/pt-BR/id) move toward full dictionary spine (#5337).

3. **[#5488 — docs shell onto the dictionary spine](https://github.com/Hmbown/CodeWhale/pull/5488)** — CLOSED. Portal hero above docs pages had 5 `isZh` ternaries; now translatable without TSX edits.

4. **[#5491 — persist approval outcomes before execution](https://github.com/Hmbown/CodeWhale/pull/5491)** — OPEN. Fail-closed approval receipts; reconstructs interrupted approvals on session resume. Directly addresses #5360.

5. **[#5484 — DSH ambient ocean scene](https://github.com/Hmbown/CodeWhale/pull/5484)** — CLOSED. Whales and glyph fish (`><((((‘>`) behind DSH UI. Cosmetic but notable product polish for the Codewhale+DeepSeek Harness bundle.

6. **[#5475 — resolve owned direct model casing safely](https://github.com/Hmbown/CodeWhale/pull/5475)** — CLOSED (community, @h3c-hexin). `glm-5.2` saved as lowercase no longer misfiled as foreign provider wire id; case-fold fallback only when exactly one provider-owned match.

7. **[#5474 — compact all noisy web tool results](https://github.com/Hmbown/CodeWhale/pull/5474)** — CLOSED (community, @h3c-hexin). Applies existing soft limit to `Web`, `web_search`, `web.run`, `fetch_url`; keeps hard limit for `read_file`. Context compaction win.

8. **[#5470 — DeepSeek V4 tiered peak/off-peak pricing per turn](https://github.com/Hmbown/CodeWhale/pull/5470)** — CLOSED. Replaces flat rates with UTC-hour tiered rates resolved from each turn's timestamp. Pricing accuracy for first-party models.

9. **[#5402 — restore session cost when live pricing unverifiable](https://github.com/Hmbown/CodeWhale/pull/5402)** — CLOSED. Fixes #5241. `unverified_live_pricing` no longer permanent when pricing endpoint 503s.

10. **[#5480 — show and open live /rc session link; stable device id](https://github.com/Hmbown/CodeWhale/pull/5480)** — CLOSED. TUI now surfaces/prints/opens the live web session link; no more new "computer" identity per `/rc` session.

---

## Feature Request Trends

1. **Third-party model config simplification** (#5350): Pre-built templates for OpenCode Zen/Go, Agnes, Sensenova — fixed URLs + model lists, "Test Connection" button, cache-load fix. One-minute setup for newcomers.

2. **Multimodal agent capability** (#5102): First-class screenshot/image viewing for agents — deliberate multimodal tool with compression, not incidental File-read luck.

3. **Plugin ecosystem maturity** (#5311): Ship Kimi-level plugin system with federated marketplaces; extends existing plugin security/installation foundation into a complete product.

4. **Sandbox configurability** (#5410): Allow additional roots in bwrap sandbox — `/dev/null` redirection and system library linking get blocked, breaking Zig workflows.

5. **Workflow discoverability** (#5439, #5442): `/workflow`, `/goal`, `/auto` shipped but buried; advanced commands (~34) demoted from discovery root; config-only capabilities invisible. Make orchestration trio one-keystroke usable.

6. **Docs localization to Chinese** (#5482): Growing Chinese user base; many docs English-only; MT introduces errors; stale source docs compound the problem.

7. **MCP capability metadata** (#4170): Spec-compatible capability metadata so tool discovery/UI can distinguish capabilities without scraping prose.

8. **1M context retention** (#5239): Users want to actually use the 1M context window instead of triggering compression at 128K.

---

## Developer Pain Points

1. **CI flakiness is endemic** — Parallel-load flakes (#5056, #5355), cross-platform red mains (#5403), docs-lint failures forcing hotfix PRs (#5489). Release confidence is repeatedly undercut by infrastructure noise.

2. **Configuration paths are fragmented** — CodeWhale config paths differ across OS/Cygwin #2369, owned-vs-bare model casing ambiguity #5475, fleet config shadowing #5098. Users keep hitting "my edit did nothing" or "works here, not there."

3. **Sandbox silently blocking legitimate operations** — SSH egress (exit 255, no output) #1829, `/dev/null` redirection + system libraries in bwrap #5410. Errors arrive as cryptic exit codes, not actionable diagnostics.

4. **Long-running sessions still wedge or crash** — 1-minute crash after prompt #5424, 300万字 novel analysis hanging on `agent_wait` #1425, VS Code crashes under YOLO Agent #1651. Reliability under sustained use is the top recurring complaint.

5. **Model-facing tool contracts too complex** — 32-field schema with 8 actions errors models #5324; role-labeled read-only builds self-BLOCK #5123. Tool design must respect model parseability, not just spec completeness.

6. **Context compression mismatch** — 1M context advertised but forced compaction at 128K #5239; web tool results flooding context (#5474). Users feel the platform under-utilizes what the model offers.

7. **Pricing/telemetry honesty friction** — `unverified_live_pricing` stuck permanently (#5241, #5402) and wrong DeepSeek URL flakiness (#4683). Cost accuracy is a trust issue — now partially addressed in v0.9.9.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*