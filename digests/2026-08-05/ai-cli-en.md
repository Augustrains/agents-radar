# AI CLI Tools Community Digest 2026-08-05

> Generated: 2026-08-05 01:18 UTC | Tools covered: 9

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

# AI CLI Tools Community Digest: Cross-Tool Comparison Report
**Date:** 2026-08-05

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem shows a bifurcated landscape: mature tools (Claude Code, OpenAI Codex) are in stabilization phases with heavy focus on security hardening and platform reliability, while mid-stage tools (Gemini CLI, Qwen Code, DeepSeek TUI) are aggressively addressing foundational correctness issues around agent orchestration, cancellation semantics, and context management. The most prominent cross-cutting theme is **context/compaction economics** — multiple tools face user backlash over silent data loss, expensive summarization, and unpredictable degradation at high token counts. Windows remains the weakest platform across nearly all tools, with recurring issues around process storms, sandbox incompatibilities, and input handling quirks. Notably, the community-driven PR contribution pattern at Claude Code (zero maintainer PRs in 24h) signals a potential release-stabilization pause, while OpenAI Codex's rapid alpha cadence (4 releases/day) suggests active internal iteration.

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | Notable PRs (24h) | Releases (24h) | Momentum Signal |
|------|-----------------|-------------------|----------------|-----------------|
| **Claude Code** | 10 (117 comments on top issue) | 5 (all community) | 1 stable (v2.1.222) | Stabilization; zero maintainer PRs |
| **OpenAI Codex** | 10 (198 comments on top issue) | 10 (all closed, copyberry[bot]) | 4 alpha patches | Rapid iteration; active bot-driven PRs |
| **Gemini CLI** | 10 (12 comments on top issue) | 10 (mixed, 2 closed) | None | Maintainer-driven; P1 triage focus |
| **GitHub Copilot CLI** | 10 (8 comments on top issue) | 2 (low signal) | 1 patch (v1.0.79-1) | Issue-driven; sparse PR activity |
| **Kimi Code CLI** | 5 (17 comments on top issue) | 3 (all open) | None | Feature-request heavy; small community |
| **OpenCode** | 10 (29 comments on top issue) | 10 (9 open, 1 beta) | 1 stable (v1.18.13) | High velocity; active contributor base |
| **Pi** | 10 (19 comments on top issue) | 10 (all open) | None | Infrastructure build-out; v2 harness |
| **Qwen Code** | 10 (17 comments on top issue) | 10 (all open) | 2 stable + 2 pre-release | Strong maintainer response; security focus |
| **DeepSeek TUI** | 9 (6 comments on top issue) | 10 (mostly open) | None (v0.9.4 train in flight) | Performance push; Copilot-generated PRs |

**Key observations:**
- **OpenAI Codex** leads raw PR velocity (10 closed PRs in 24h, albeit bot-assisted)
- **Claude Code** has highest issue engagement (117 comments on #42776)
- **DeepSeek TUI** shows the most dramatic community->maintainer feedback loop (#4991 discussion → #5249 epic)
- **Gemini CLI** and **Qwen Code** demonstrate strongest maintainer-to-community responsiveness on correctness issues

---

## 3. Shared Feature Directions

| Requirement | Tools | Specific Needs |
|-------------|-------|----------------|
| **RTL/LTR text support** | Claude Code (#38005, 90👍), OpenCode (v1.18.13 RTL fixes) | Hebrew/Arabic rendering in TUI/Desktop; OpenCode has fixed but Claude Code still pending |
| **Persistent memory/session state** | Kimi (#1283), Pi (#7396 server backend), DeepSeek (#5131 memory API) | Cross-session context, durable storage, HTTP-accessible memory management |
| **Remote/device mobility** | Kimi (#1282), Pi (#7599 RPC-over-sockets), Claude Code (desktop relaunch) | Continue sessions from any device, out-of-process clients, socket-based RPC |
| **Configurable compaction** | Pi (#7553/#7602), Claude Code (#82131/#82144), DeepSeek (#5239/#5244) | Independent compaction model/thinking level; fix silent 128K fallback; avoid 4× re-injection cost |
| **Session forking/branching** | Copilot CLI (#1697, 25👍), Pi (#7619 resume failed turns) | Parallel workstreams from shared context; resume failed/interrupted turns |
| **MCP lifecycle management** | OpenAI Codex (#30408), Copilot CLI (#4370), Qwen Code (#8550), DeepSeek (#5130) | Process cleanup, `server/discover` tolerance, timeout handling, HTTP-based server management |
| **Subagent governance** | Gemini CLI (#22323/#21409), Claude Code (#79953), OpenCode (#40549) | Honest termination reasons, apply hooks to subagents, cumulative runtime budgets |
| **Custom theming** | Copilot CLI (#1504, 23👍), Claude Code (#13378 configurable formatting) | User-defined themes; adjustable indent/wrap in code blocks |
| **Usage/cost transparency** | OpenCode (#16017, 126👍), DeepSeek (#5241), Copilot CLI (#2532/#4174) | Public usage APIs, live pricing verification, persistent token/context indicators |
| **Windows parity** | Claude Code (#42776/#83243), OpenAI Codex (#30009/#33776), Qwen Code (#8538), Pi (#7547) | Fix process storms, apply_patch sandbox, input handling, file locks |

---

## 4. Differentiation Analysis

**By Feature Focus:**

| Tool | Primary Focus | Distinctive Differentiator |
|------|---------------|---------------------------|
| **Claude Code** | Worktree isolation, hooks/plugins | Security-first architecture; strongest plugin ecosystem |
| **OpenAI Codex** | Desktop app performance, MCP integration | Responses API alignment; rapid alpha iteration |
| **Gemini CLI** | Agent correctness, subagent orchestration | Maintainer-led correctness fixes; behavioral evals (LLM-as-Judge) |
| **Copilot CLI** | Enterprise integration, sandboxing | GitHub org/enterprise alignment; dev-tool access controls |
| **Kimi Code** | ACP protocol, persistence | ACP maturity push; mobile-first client support |
| **OpenCode** | Multi-provider output reliability | 5 provider-specific tool-call classification PRs in 24h |
| **Pi** | v2 harness, RPC/embedding | Server session backend; SQLite lane-aware storage |
| **Qwen Code** | Security hardening, daemon governance | Trust-boundary work; cost-ledger forensics |
| **DeepSeek TUI** | Build performance, runtime API | Monolith decomposition; Copilot-assisted API expansion |

**By Target User:**
- **Power developers**: Claude Code, Gemini CLI (advanced plugins, worktree isolation)
- **Enterprise**: Copilot CLI (org agents, billing entity, SSO), Pi (Copilot Enterprise seats)
- **Performance-sensitive**: OpenCode (75% renderer memory reduction), DeepSeek (build-time)
- **Mobile/embedded**: Kimi (ACP protocol), DeepSeek (RPC API)

**Technical Approach Differences:**
- **Claude Code**: TS/JS, hook-based security model
- **OpenAI Codex**: Rust rewrite, alpha-rapid iteration
- **Gemini CLI**: TS, P1-tagged triage discipline
- **DeepSeek TUI**: Rust, Copilot-assisted API generation
- **Qwen Code**: TS, daemon-based multi-workspace model

---

## 5. Community Momentum & Maturity

**Most Active Communities:**

1. **Claude Code** — Largest engagement (117 comments on #42776; 4-month persistence), 90👍 on RTL request, 8-month-old issues still active. Most "sticky" community that keeps issues alive despite maintainer struggle to reproduce.
2. **OpenCode** — Fastest-growing; 126👍 on usage API in relatively short time; 5 provider-specific PRs in 24h shows contributor depth.
3. **OpenAI Codex** — Large install base (917👍 Linux desktop request); strong reaction economy (80 comments, 387👍 on macOS bug); frustration with Windows performance is reaching critical mass.

**Rapidly Iterating:**
- **OpenAI Codex** — 4 alpha releases/24h; bot-assisted PR pipeline (10 closed)
- **OpenCode** — 1 stable release + 10 PRs/24h
- **Qwen Code** — 4 releases/24h (1 stable + 1 preview + 2 nightly); 10 PRs open

**Stabilizing/Consolidating:**
- **Claude Code** — Zero maintainer PRs; security patch in latest release
- **Copilot CLI** — Sparse PR activity; breaking config change in patch release

**Community-Driven Maintainer Adoption:**
- **DeepSeek TUI** — Community discussion (#4991) directly spawned maintainer epic (#5249)
- **Pi** — Maintainers opening community triage issues (#7547 "How do you use Pi on Windows?")

**Maturity Indicators:**
- **Most mature plugin ecosystem**: Claude Code (hook-testing utilities, skill documentation PRs)
- **Most robust CI/eval infrastructure**: Gemini CLI (LLM-as-Judge triage, behavioral eval framework)
- **Best cross-provider compatibility**: OpenCode (Anthropic, Gemini, OpenAI-compatible)
- **Most comprehensive security response**: Qwen Code (trust-boundary hooks, SSRF checks)

---

## 6. Trend Signals

**1. Context/Compaction Economics Have Become a First-Class Concern**
- Multiple tools report: autocompact thrashing (#82131, Claude), 4× re-injection cost (#82144, Claude), silent 128K fallback on 1M-window models (#5244, DeepSeek), quadratic JSON output (#7395, Pi), degradation at ~500K tokens (#2586, Kimi). Expect: **configurable compaction models, warning on fallbacks, and context-window marketing honesty** to become differentiators.

**2. Windows Has Become a Strategic Blind Spot Across the Ecosystem**
- WMI storms and PowerShell polling (#33776, #25453, #29499 — Codex); file locks preventing relaunch (#42776 — Claude); apply_patch sandbox failures (#30009 — Codex); Bash failing on trivial commands (#83243 — Claude); IME duplication (#2584 — Kimi). The cumulative signal is: **Windows users are a growing, underserved population** in the AI CLI space.

**3. Security-by-Design Is Moving From Optional to Table-Stakes**
- Claude Code worktree isolation, Qwen Code trust-boundary hook hardening (#8396), OpenAI Codex project-directory trust prompts (#36960), Pi OAuth error message sanitization (#7605), Copilot CLI `allowDevToolAccess` rename. **Security is becoming a release-blocking concern, not an afterthought.**

**4. Subagent Orchestration Is the New Frontier of Correctness**
- Gemini CLI's misleading GOAL terminations (#22323, #21983), Claude Code subagent hook bypasses (#79953), OpenCode's 5 PRs on tool-call finish-reason semantics (#40545–40549), DeepSeek's agent checkpoint resume (#5242). **The industry is converging on the insight that subagent output trustworthiness is the gating factor for complex multi-step workflows.**

**5. MCP Integration Maturity Is a Competitive Battleground**
- Every tool except Gemini CLI has MCP issues in their top 10: server discovery failures (#4370, Copilot), process leaks (#30408, Codex), SSE hangs (#8550, Qwen), registry-first tool selection (#5238, DeepSeek), consent transparency (#28664, Gemini). **The tool that can offer robust, production-grade MCP lifecycle management will have a significant advantage.**

**6. User-Controlled Visibility Is a Growing Demand**
- Usage APIs (OpenCode #16017), model attribution in JSON output (OpenCode #40545), cost ledgers (Qwen #8471), live pricing verification (DeepSeek #5241), context/compaction visibility (Pi #7553). **Users want observability into what the agent is doing, why, and at what cost — not just final output.**

---

## For Developers: Actionable Takeaways

1. **For Windows developers**: Expect recurring issues; plan workarounds for sandboxing and process management. OpenCode's rapid iteration suggests best hope for near-term Windows improvements.
2. **For enterprise teams**: Copilot CLI still has rough edges (billing entity, view tool regression). Pi's Copilot Enterprise compaction bug (#6768) suggests caution when standardizing on enterprise GitHub plans for AI CLIs.
3. **For long-session users**: Watch context/compaction behavior carefully. Claude Code and DeepSeek currently penalize extended sessions; Gemini's `/compress` fix (#28672) may offer the most reliable path.
4. **For MCP-heavy workflows**: Codex's concurrent dispatch (#36987) and DeepSeek's registry discovery (#5238) are the most promising directions; but expect friction until lifecycle management matures.
5. **For plugin/maintainer contributors**: Claude Code has the most community-tolerant plugin tooling; Gemini CLI's caretake-eval framework (#28530) offers a model for test-driven agent development.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-08-05 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Skills have generated the most discussion and community attention:

| # | Skill | Author | Status | Discussion Focus |
|---|-------|--------|--------|-----------------|
| 1 | **skill-creator fixes** (multiple PRs: #1298, #1099, #1050, #1323, #1261) | MartinCajiao, joshuawowk, gstreet-ops, Polluelo978, alvingarcia | Open | The most actively discussed topic — critical bugs in `run_eval.py` causing 0% recall rates on Windows and Linux, making the skill optimization loop useless |
| 2 | **document-typography** (#514) | PGTBoos | Open | Typographic quality control for generated documents — orphan words, widow paragraphs, numbering alignment |
| 3 | **ODT skill** (#486) | GitHubNewbie0 | Open | OpenDocument Text creation, template filling, and ODT→HTML conversion |
| 4 | **self-audit** (#1367) | YuhaoLin2005 | Open | Mechanical file verification + four-dimension reasoning quality gate for AI output |
| 5 | **testing-patterns** (#723) | 4444J99 | Open | Comprehensive testing skill — Testing Trophy model, unit testing, React component testing |
| 6 | **color-expert** (#1302) | meodai | Open | Color naming systems, color spaces (OKLCH, OKLAB, CAM16), color expertise |
| 7 | **frontend-design revision** (#210) | justinwetch | Open | Skill clarity and actionability improvements for frontend-design |
| 8 | **pyxel skill** (#525) | kitao | Open | Retro game development with Pyxel engine via MCP server |

**Key Discussion Highlights:**
- **skill-creator bug fixes** dominate conversations — 5 separate PRs (#1298, #1099, #1050, #1323, #1261) all address the same root cause: `run_eval.py` reports `recall=0%` for all queries, rendering the description-optimization loop ineffective. Issue #556 has 12 comments and 7 👍, confirming widespread impact.
- **document-typography** addresses a universal pain point — AI-generated documents consistently suffer from typographic issues that users rarely explicitly request to fix.
- **testing-patterns** fills a clear gap with comprehensive coverage across the testing stack, including the Testing Trophy model philosophy.

---

## 2. Community Demand Trends

From Issues analysis, the community's most-anticipated directions are:

1. **Skill Reliability & Tooling** (highest demand): Multiple issues (#556, #1061, #1169, #1329) focus on making skill-creator tools work reliably across platforms. Windows compatibility, subprocess handling, and trigger detection are critical blockers. Issue #556 alone has 12 comments and 7 👍.

2. **Security & Trust** (Issue #492, 43 comments, 2 👍): The #1 most-commented issue raises concerns about community skills distributed under the `anthropic/` namespace, creating trust boundary vulnerabilities. Users want clear separation between official and community skills.

3. **Enterprise Collaboration** (Issue #228, 16 comments, 8 👍): Org-wide skill sharing is a top request — users want shared skill libraries and direct sharing links rather than manual file transfers.

4. **Context Window Efficiency** (Issue #1487): The `claude-api` skill's 156k-token eager injection exposes a systemic problem — skills must be more judicious about context consumption.

5. **Governance & Safety** (Issues #412, #1385): Users are proposing safety patterns for agent systems — policy enforcement, threat detection, trust scoring, and quality gate pipelines.

---

## 3. High-Potential Pending Skills

These active PRs may land soon based on community engagement:

1. **self-audit** (#1367) — Author: YuhaoLin2005 | Created: 2026-06-28
   - Mechanical file verification before delivery + four-dimension reasoning audit
   - Related proposal in Issue #1385 shows active iteration direction

2. **plan-file-hygiene** (#1479) — Author: Palo-Alto-AI-Research-Lab | Created: 2026-07-25
   - Addresses issue #1417 about planning artifacts accumulating without lifecycle management

3. **testing-patterns** (#723) — Author: 4444J99 | Created: 2026-03-22
   - Comprehensive testing skill with philosophy, unit testing, and React coverage

4. **color-expert** (#1302) — Author: meodai | Created: 2026-06-10
   - Self-contained color expertise with naming systems and color space guidance

5. **compact-memory** (Issue #1329 proposal) — Author: WGlynn
   - Symbolic notation for compact agent state to reduce context overhead on persistent memory

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is for **reliable, cross-platform skill development tooling** — specifically fixing `skill-creator`'s evaluation pipeline on Windows (5+ PRs, 2 issues, 12+ comments) — followed closely by **security/trust boundaries** (43 comments on the namespace impersonation issue) and **context-window efficiency** for production-grade skills.

---

# Claude Code Community Digest — 2026-08-05

## 1. Today's Highlights

Worktree isolation hardening arrived in v2.1.222, closing a security gap where subagents in worktree-isolated sessions could run destructive git commands against the main checkout. Meanwhile, the community's attention remains focused on two long-running issues: the Windows Desktop relaunch bug (#42776, 117 comments) with a possible orphaned process file lock at its core, and the RTL support request for Hebrew & Arabic (#38005, 90 👍). Plugin development tooling is seeing active community contribution, with two new PRs improving hook-testing utilities.

## 2. Releases

**v2.1.222** (latest)
- **Security fix**: Worktree-isolated sessions and their subagents can no longer run destructive git commands against the main checkout; isolation now applies to file edits and Bash in every session type.
- **Bug fix**: PreToolUse auto-allow hooks no longer bypass tool restrictions in background agent tasks.

## 3. Hot Issues

1. **[#42776 — Desktop fails to Relaunch on Windows due to orphaned process file lock](https://github.com/anthropics/claude-code/issues/42776)** (117 comments, 51 👍)
   The longest-running open issue, active for 4 months. Users report the Desktop app cannot restart after closing due to a lingering file lock. The "invalid" label suggests maintainers may be struggling to reproduce, but the community keeps it alive with workarounds.

2. **[#38005 — RTL Support for Hebrew & Arabic in Desktop/Cowork](https://github.com/anthropics/claude-code/issues/38005)** (41 comments, 90 👍)
   The most-upvoted open feature request. Marked duplicate, but the demand is clear: RTL text rendering in the Desktop/Cowork UI is essential for a significant user base. Duplicate status may be splitting the signal.

3. **[#74260 — Assistant text blocks silently dropped when followed by more thinking](https://github.com/anthropics/claude-code/issues/74260)** (24 comments, 15 👍)
   Data-loss bug: text emitted mid-turn never renders and is missing from the JSONL transcript. Reproduced with adaptive thinking on `claude-fable-5`. Serious trust issue for users relying on transcripts.

4. **[#13378 — 2-space indent and hard wrap at 80 breaks copy-paste](https://github.com/anthropics/claude-code/issues/13378)** (15 comments, 72 👍)
   A long-standing UX complaint (8 months). The fixed code-block formatting interferes with copying code out of the TUI. High 👍 count indicates a widely shared annoyance with no configurable workaround.

5. **[#23704 — Read tool's PDF support requires undocumented poppler-utils](https://github.com/anthropics/claude-code/issues/23704)** (15 comments, 19 👍)
   The Read tool advertises PDF support, but silently fails when `poppler-utils` is absent — which is common in containers. The key complaint is the missing detection: the tool should say what's missing, not just fail.

6. **[#61021 — Can no longer easily select text to copy in VS Code terminal](https://github.com/anthropics/claude-code/issues/61021)** (15 comments, 11 👍)
   Regression in the VS Code terminal integration. Mouse-based text selection conflicts with Claude Code's TUI event handling. Actively affects daily workflow for terminal users.

7. **[#82536 — `--continue` cannot find sessions created by `-p`](https://github.com/anthropics/claude-code/issues/82536)** (7 comments)
   Interactive resume of print-mode sessions fails. Break in the session lifecycle that forces users to manually locate and pass session IDs.

8. **[#82131 — Autocompact is thrashing: context refills within 3 turns, 3× in a row](https://github.com/anthropics/claude-code/issues/82131)** (3 comments)
   Compaction is not solving the context problem — the summary is too lossy, and the model refills context almost immediately. Anecdotal reports of this undermine trust in auto-compaction for long sessions.

9. **[#82144 — Post-compaction skill re-injection costs ~4× the compaction summary](https://github.com/anthropics/claude-code/issues/82144)** (1 comment)
   After compaction, full skill bodies are re-injected (byte-truncated), consuming 4× the tokens of the compaction summary itself. The "fix" is nearly as expensive as the problem, which defeats the purpose of compaction.

10. **[#83243 — Bash tool fails on trivial commands on Windows v2.1.220](https://github.com/anthropics/claude-code/issues/83243)** (2 comments)
   Recent Windows regression where even `echo` fails with "unexpected EOF...line 86". Potential release-blocker for Windows users; waiting on maintainer confirmation.

## 4. Key PR Progress

No official maintainer PRs merged in the last 24h — the list is entirely community contributions:

1. **[#83992 — fix(plugin-dev): assert expected hook decision](https://github.com/anthropics/claude-code/pull/83992)** — Adds `--expect allow|deny|ask` flag to `test-hook.sh` so tests can verify a hook denied an operation it should deny, not just that it ran. Fixes #83800.

2. **[#83990 — fix(plugin-dev): report missing jq dependency](https://github.com/anthropics/claude-code/pull/83990)** — `test-hook.sh` silently misreported missing `jq` as invalid JSON; now checks for the binary upfront. Fixes #83802.

3. **[#83890 — Create pylint.yml](https://github.com/anthropics/claude-code/pull/83890)** — Adds a GitHub Actions workflow for pylint (likely for a plugin repo; PR body is empty).

4. **[#83374 — docs(plugin-dev): document MessageDisplay streaming semantics](https://github.com/anthropics/claude-code/pull/83374)** — The Hook Development skill omits `MessageDisplay` entirely; this adds it to the trigger description, event guidance, and quick-reference table.

5. **[#83738 — Fix/83484 symlink path expansion](https://github.com/anthropics/claude-code/pull/83738)** — Fixes `claude install` creating broken symlinks pointing to `%h/...` instead of the expanded home path on some Linux installs.

**Notable omission:** No PRs from Anthropic staff in this window. All activity is community-driven, which suggests the team may be in a release stabilization phase.

## 5. Feature Request Trends

- **RTL support (#38005)** — The highest-demand feature overall (90 👍). The duplicate label suggests multiple requests are being folded together; community is waiting for a commitment.
- **Configurable display formatting (#13378)** — Users want control over indent width and line-wrap behavior in code blocks. The "hard-coded and unfixable without a setting" aspect is the core complaint.
- **Workflow/agent runtime governance (#79953)** — A `PreToolUse` hook can block the outer workflow, but internal `agent()` calls bypass hook restrictions entirely. Users want a cumulative budget for agent runtime.
- **Desktop project identification (#81628)** — Multiple clones of the same repo are indistinguishable in the session list; requesting folder-name-derived tags or a configurable label.
- **Startup progress indicators (#83988)** — Desktop app shows a blank window for up to 117s with no feedback; users want visibility into what's loading.

## 6. Developer Pain Points

- **Context/compaction economics (#82131, #82144)** — Autocompact is both thrashing (refilling within 3 turns) and expensive (skill re-injection costs 4× the summary). Long-session users are actively penalized.
- **Silent data loss (#74260)** — Text blocks vanishing from both UI and transcripts is the most trust-damaging bug type. If output isn't guaranteed, users can't rely on the tool for record-keeping.
- **Undocumented runtime dependencies (#23704, #66563)** — PDF support requires external tools that are neither documented nor detected. Users get cryptic errors ("password-protected" for a plain PDF) instead of actionable messages.
- **Windows instability (#42776, #83243, #83130)** — File locks preventing relaunch, Bash failures on trivial commands, and MSIX WebGPU crashes. Windows remains the weakest platform.
- **Session lifecycle inconsistencies (#82536, #83971)** — `--continue` can't find `-p` sessions; backgrounding drops prior context. Users get sessions that "forget" what they were doing.
- **Hook/plugin governance gaps (#79953, #83643)** — Hooks don't apply consistently across workflows, subagents, or remote desktop sessions. Security-conscious users are exposed.

---

*Digest generated from GitHub data retrieved 2026-08-05. All links point to anthropics/claude-code.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-05

## Today's Highlights

Four alpha releases (`0.147.0-alpha.7` down to `0.147.0-alpha.6.1`) shipped within the last 24 hours, continuing the rapid cadence of the Rust-based CLI. The most significant community activity centers on a cluster of Windows Performance issues — WMI Provider Host saturation, PowerShell polling storms, and system-wide input lag — that have accumulated dozens of comments and multiple consolidated reports. Meanwhile, a dense batch of closed PRs from the `copyberry[bot]` reveals active work on tool-search deferral, paginated thread reads, concurrent exec-server dispatch, and security hardening around project-directory trust.

---

## Releases

Four alpha releases published in the last 24 hours, all `rust-v0.147.0-alpha.*`:

- **rust-v0.147.0-alpha.7** — Latest alpha release
- **rust-v0.147.0-alpha.6.4** — Patch release
- **rust-v0.147.0-alpha.6.3** — Patch release
- **rust-v0.147.0-alpha.6.1** — Patch release

No release notes or changelogs were attached, consistent with the project's typical fast-iteration alpha pipeline. The concentrated patch cadence suggests active bug-fixing in the current alpha series.

---

## Hot Issues

**1. [Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)** — 198 comments, 917 👍
The most-requested feature in the tracker. Linux users want a native desktop app, motivated by macOS power-consumption bugs and general performance concerns. The high engagement shows a strong Linux developer audience that currently relies on CLI/TUI workarounds.

**2. [Codex Desktop macOS: syspolicyd/trustd CPU and memory runaway](https://github.com/openai/codex/issues/25719)** — 80 comments, 387 👍
Desktop app triggers persistent `syspolicyd`/`trustd` CPU and memory growth on macOS. The long-running nature of this bug (since June) with substantial reactions suggests it significantly impacts daily usability on Apple Silicon.

**3. [Please make "/undo" back](https://github.com/openai/codex/issues/9203)** — 68 comments, 372 👍
Users report losing work when Codex unintentionally deletes untracked files or modifies uncommitted changes. The `/undo` feature was removed, and the community wants it restored. High upvote count indicates this is a key workflow regression.

**4. [High GPU usage while the app is "thinking" due to tiny useless animation](https://github.com/openai/codex/issues/16857)** — 38 comments, 46 👍
The desktop app's "thinking" state animation causes disproportionate GPU usage. Illustrates a broader concern about inefficient UI rendering in the desktop client, particularly on macOS.

**5. [apply_patch fails with a Windows sandbox related error](https://github.com/openai/codex/issues/30009)** — 30 comments, 10 👍
Windows users cannot apply file edits through `apply_patch` due to sandbox conflicts. This blocks a core Codex workflow on Windows, making it a high-priority platform gap.

**6. [ChatGPT.exe spawns hundreds of taskkill.exe/conhost.exe processes](https://github.com/openai/codex/issues/33776)** — 29 comments, 26 👍
On Windows, the desktop app spawns hundreds of `taskkill.exe`/`conhost.exe` processes, causing WMI storms and DWM degradation. The reported 287 processes in one session underscores the severity of process-management problems on Windows.

**7. [Custom stdio MCP server discovered but tools not exposed to Desktop threads](https://github.com/openai/codex/issues/19425)** — 28 comments, 5 👍
A regression in the app-server (`0.124.0-alpha.2`) prevents MCP tools from being exposed despite successful discovery via `tools/list`. Critical for developers relying on custom MCP integrations.

**8. [MCP server processes leak: per-thread processes never cleaned up](https://github.com/openai/codex/issues/30408)** — 22 comments, 6 👍
MCP server processes accumulate per-thread and are never killed on archive/close, reaching 9+ GB RSS. Memory-leak behavior that degrades long-running desktop sessions.

**9. [Codex triggers high CPU usage in WMI Provider Host on Windows](https://github.com/openai/codex/issues/29499)** — 17 comments, 23 👍
After startup, Codex drives WMI Provider Host CPU usage up. Combined with #33776, #32562, #36025, #36176, and #25453, this reflects a systemic Windows process-polling problem.

**10. [Windows Codex Desktop spawns powershell.exe every second for full process polling](https://github.com/openai/codex/issues/25453)** — 22 comments, 6 👍
The desktop app continuously spawns PowerShell processes to poll the full process list, causing high CPU. This is the root cause behind multiple Windows performance complaints and has significant community frustration.

---

## Key PR Progress

**1. [Support deferred custom tools in tool search](https://github.com/openai/codex/pull/36998)** — Closed
Integrates top-level freeform tools into the tool-search index with deferred loading; serializes searched tools as Responses API `custom` tools and converts back to executable specs after discovery.

**2. [Support includeTurns reads for paginated threads](https://github.com/openai/codex/pull/36993)** — Closed
Reconstructs full projected turns from paginated history so clients using `thread/read` with `includeTurns: true` retain the legacy full-history view.

**3. [Add opt-in concurrent exec-server request dispatch](https://github.com/openai/codex/pull/36987)** — Closed
Adds `--concurrent-requests <COUNT>` flag to prevent long-running requests from blocking health checks and cleanup on the same connection. Notable for MCP-related performance.

**4. [Add process-scoped PSP routing for ChatGPT requests](https://github.com/openai/codex/pull/36986)** — Closed
Adds a hidden global `--psp` flag propagated through TUI, exec, app-server, and remote-control paths; attaches `oai-chat-psp=true` cookie to first-party ChatGPT requests.

**5. [Support configured ChatGPT cookies in HTTP clients](https://github.com/openai/codex/pull/36984)** — Closed
Extends `HttpClientFactory` to carry additional ChatGPT cookies and share the store across cloned factories, enabling cookie-based auth where configured.

**6. [Enable remote compaction for Amazon Bedrock](https://github.com/openai/codex/pull/36981)** — Closed
Adds provider-owned remote compaction capabilities; marks Bedrock as v1-only so compaction uses `/v1/responses/compact` even when v2 is enabled.

**7. [Prompt before trusting local project directories](https://github.com/openai/codex/pull/36960)** — Closed
Requires explicit user decision before trusting a project directory, addressing prompt-injection exposure via project-local config, hooks, and exec policies.

**8. [Make token budget context identity configurable](https://github.com/openai/codex/pull/36970)** — Closed
Adds `features.token_budget.mode` setting with `thread` and `name` options, defaulting context-window metadata to thread ID while preserving agent-name configuration.

**9. [Skip symlinks when installing plugins](https://github.com/openai/codex/pull/36967)** — Closed
Ignores symlinks and non-file/directory entries during plugin installation instead of rejecting the install; covers symlinked skill files and executables.

**10. [Preserve working directories when importing external sessions](https://github.com/openai/codex/pull/36964)** — Closed
Fixes Cursor imports where projectless chats use the reserved `empty-window` project; resolves such sessions to the parent of the Cursor workspace, preserving working-directory context.

---

## Feature Request Trends

- **Linux Desktop App (🔥 #1):** The desire for a native Codex desktop app on Linux remains by far the most-upvoted open request. The macOS performance bugs (#25719, #16857) appear to be driving Linux users to request a more efficient desktop experience.

- **Session and History Management:** Strong demand for restoring `/undo` (#9203), exposing CLI sessions in desktop history (#21079), and providing clear chat deletion/archiving in the desktop app (#33589). Users want more control over their session lifecycle and recovery.

- **MCP Integration Maturity:** Requests center on reliable MCP server lifecycle management (#30408), proper tool exposure in Desktop threads (#19425), and propagating client input IDs to tool execution context (#36994). The community is pushing for production-grade MCP support.

- **Desktop-Local Persistence:** Users want desktop and CLI sessions to interoperate seamlessly, including importing Claude Code history (already partially supported) and native Codex CLI history into desktop.

- **Configurability and Control:** The trend toward opt-in flags and configurable behavior (concurrent dispatch, token budget identity, image viewer disable) suggests the community values runtime configurability and performance controls.

---

## Developer Pain Points

- **Windows Desktop Performance is a Recurring Nightmare:** The largest pain-point cluster this week. Multiple issues report WMI Provider Host saturation (#29499, #32562), PowerShell polling storms (#25453, #36176), `taskkill.exe`/`conhost.exe` proliferation (#33776), and system-wide input lag (#36025, #34158). The community is clearly frustrated that these issues persist across multiple versions (26.506 through 26.721).

- **MCP Process Leaks and Handler Loss:** Developers integrating custom MCP servers hit two distinct problems: orphaned processes accumulating memory (#30408) and tools losing handlers mid-session (`No handler registered`, #28080). Both break long-running desktop workflows.

- **macOS Resource Waste:** The "thinking" animation causing GPU spikes (#16857) and syspolicyd/trustd runaway (#25719) point to inefficient resource usage in the Electron-based desktop app on macOS — particularly noticeable on laptops.

- **Windows Sandbox and Tool-Call Failures:** `apply_patch` failing on Windows sandbox (#30009) blocks core editing workflows. The platform-specific sandboxing behavior remains an ongoing friction point for Windows users.

- **Lost/Invisible Session Data:** Users report lost CLI history in desktop (#21079), disappearing local history after provider switches (#31625), and the inability to delete chats (#33589). Trust in session persistence is eroding.

- **Subagent Configuration Ignored:** Desktop subagents ignoring model and reasoning settings (#28719) creates unpredictable behavior and cost implications, with affected users expressing strong frustration.

---

*Digest compiled from public GitHub data for openai/codex, covering activity from 2026-08-04 to 2026-08-05.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-05

## Today's Highlights

The Gemini CLI maintainers are prioritizing agent reliability: a long-standing issue where MAX_TURNS interruptions are misreported as successful "GOAL" completions is flagged for retesting, while a separate P1 issue on generalist agent hangs continues to attract community attention. A wave of new PRs targets core stability, including fixes for shell command hangs, OAuth callback leaks, and environment variable loading order. Notably, there are no new releases in the last 24 hours.

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

### 1. Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption
- **Issue:** [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
- **Priority:** P1 (Area: agent) | 12 comments | 2 👍 | **Status:** Need Retesting

This is a serious correctness problem. A `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` even though it hit the maximum turn limit before doing any analysis. This means the main agent may trust bad output from a subagent that actually failed. The high comment count (12) suggests active maintainer debugging.

### 2. Generalist agent hangs
- **Issue:** [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
- **Priority:** P1 (Area: agent) | 8 comments | 8 👍 | **Status:** Need Retesting

User reports simple operations (like folder creation) hang indefinitely when delegated to the generalist agent. It was noted that instructing the model to not defer to subagents resolves the issue—narrowing the problem to subagent orchestration, not the model itself. 8 upvotes suggests many users hit this.

### 3. Shell command execution gets stuck with "Waiting input" after command completes
- **Issue:** [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
- **Priority:** P1 (Area: core) | 4 comments | 3 👍 | **Status:** Bot-triaged

A very common UX annoyance—the CLI hangs in a "Waiting input" state even after simple shell commands (e.g., `ls`, `echo`) have completed. The agent appears to hang indefinitely on trivial commands that don't request input. Community is calling for a fix to this P1 core bug.

### 4. Browser subagent fails in Wayland
- **Issue:** [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)
- **Priority:** P1 (Area: agent/browser) | 4 comments | 1 👍 | **Status:** Need Retesting

The browser agent fails on Wayland display servers, a common Linux environment. The termination reason shows "GOAL" but does not distinguish between a successful goal and a crash. This is another symptom of the broader issue around misleading termination reasons.

### 5. Gemini CLI encounters 400 error with > 128 tools
- **Issue:** [#24246](https://github.com/google-gemini/gemini-cli/issues/24246)
- **Priority:** P2 (Area: agent) | 3 comments | 0 👍 | **Status:** Need Information

Power users with many MCP servers and built-in tools hit API 400 errors when tool count exceeds limits. The expectation is that the agent should intelligently limit the set of tools in scope. This affects multi-server workflows.

### 6. Gemini CLI gets stuck at interactive prompt creating Vite app
- **Issue:** [#22465](https://github.com/google-gemini/gemini-cli/issues/22465)
- **Priority:** P2 (Area: agent) | 2 comments | 0 👍 | **Status:** Bot-triaged

Model fails to handle interactive prompts in the terminal (e.g., `npm create vite` prompts). Maintainer suggests adding a behavioral eval to catch this regression in the future. This is a common new-user experience that should be smoothed out.

### 7. Gemini does not use skills and sub-agents enough
- **Issue:** [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)
- **Priority:** P2 (Area: agent) | 6 comments | 0 👍 | **Status:** Need Retesting

Anecdotally, model rarely auto-invokes custom skills or sub-agents even when clearly relevant (e.g., a `gradle` skill exists and the task is a Gradle build). Users must explicitly force it. This diminishes the value of custom skills and is a key feature gap.

### 8. Stop Auto Memory from retrying low-signal sessions indefinitely
- **Issue:** [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)
- **Priority:** P2 (Area: agent) | 5 comments | 0 👍 | **Status:** Bot-triaged

The Auto Memory background agent will repeatedly re-process sessions it already deemed "low signal," because they were never marked as processed. This wastes tokens and is a clear efficiency bug in the memory pipeline.

### 9. Agent should stop/discourage destructive behavior
- **Issue:** [#22672](https://github.com/google-gemini/gemini-cli/issues/22672)
- **Priority:** P2 (Area: agent) | 3 comments | 1 👍 | **Status:** Bot-triaged

Communities report the model sometimes uses `git reset` or `--force` when safer alternatives exist. It also lacks awareness of dangerous DB modifications. The community is calling for guardrails or prompt-level discouragement of destructive operations.

### 10. Add deterministic redaction and reduce Auto Memory logging
- **Issue:** [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)
- **Priority:** P2 (Area: security) | 4 comments | 0 👍 | **Status:** Bot-triaged

A security concern: Auto Memory sends local transcript content to the extraction model before redaction happens (i.e., secrets are exposed in the prompt). The service may also log existing skills. The community and maintainers agree this should be fixed with deterministic pre-send redaction.

---

## Key PR Progress

### 1. fix(core): unwrap and parse nested gaxios streaming errors from cause message
- **PR:** [#28689](https://github.com/google-gemini/gemini-cli/pull/28689) | Size: M | Open
- **What it does:** Adds a fallback to parse nested Google API errors from `error.cause.message` during streaming. This surfaces accurate rate-limit and capacity errors instead of opaque failures.

### 2. feat(caretaker-evals): add triage evaluation framework and judge runner
- **PR:** [#28530](https://github.com/google-gemini/gemini-cli/pull/28530) | Size: L | Open
- **What it does:** Introduces an LLM-as-a-Judge evaluation framework and a parallel Git worktree benchmark runner for the Caretaker Agent issue triage pipeline.

### 3. feat(ingestion): add issue comment handling and re-triage workflow
- **PR:** [#28690](https://github.com/google-gemini/gemini-cli/pull/28690) | Size: L | Closed
- **What it does:** Adds `issue_comment.created` webhook processing, enabling `@caretaker-agent` mentions or `/caretaker triage` to trigger re-triage on `NEEDS_INFO` issues.

### 4. fix(core): guard formatTruncatedToolOutput against non-positive maxChars
- **PR:** [#28639](https://github.com/google-gemini/gemini-cli/pull/28639) | Size: S | P1 | Open
- **What it does:** Guards against negative `maxChars` which previously inflated output ~2x via `slice()` negative-index behavior. Adds regression tests. Fixes [#28620](https://github.com/google-gemini/gemini-cli/issues/28620).

### 5. fix(cli): prevent ghost text wrapping infinite loop at narrow widths
- **PR:** [#28641](https://github.com/google-gemini/gemini-cli/pull/28641) | Size: S | Help Wanted | Open
- **What it does:** Fixes an infinite loop in `getGhostTextLines` when terminal width is narrower than a single wide codepoint (CJK/emoji). Fixes [#19985](https://github.com/google-gemini/gemini-cli/issues/19985).

### 6. fix(core): dynamically resolve Cloud Workstations proxy redirect URI for OAuth flows
- **PR:** [#28688](https://github.com/google-gemini/gemini-cli/pull/28688) | Size: M | P3 | Open
- **What it does:** Resolves OAuth failures inside Google Cloud Workstations by dynamically computing the proxy redirect URI instead of hardcoding `localhost`.

### 7. fix(mcp): reflect full server config in consent and harden stdio env
- **PR:** [#28664](https://github.com/google-gemini/gemini-cli/pull/28664) | Size: L | Open
- **What it does:** Consent prompts now show all MCP execution-affecting fields (env, cwd, headers), not just command/args, improving security transparency.

### 8. fix(core,cli): repair /compress session reload and quota-fallback tool response loss
- **PR:** [#28672](https://github.com/google-gemini/gemini-cli/pull/28672) | Size: M-L | Help Wanted | Open
- **What it does:** Two fixes: (1) `/compress` no longer fails on resume; (2) quota-fallback no longer loses tool responses. Also addresses context corruption from interrupted tool executions.

### 9. fix(cli): load environment variables before resolving settings placeholders
- **PR:** [#28597](https://github.com/google-gemini/gemini-cli/pull/28597) | Size: L | Open
- **What it does:** Fixes a race condition where settings files were parsed and expanded against `process.env` before `.env` files were loaded, causing placeholder mis-resolution at startup.

### 10. fix(core): add timeout to IdeClient.getInstance() process traversal
- **PR:** [#28677](https://github.com/google-gemini/gemini-cli/pull/28677) | Size: M | Help Wanted | Open
- **What it does:** Adds a 3-second timeout to IDE process-tree traversal. Prevents the TUI from hanging on "Initializing..." forever when run in a bare terminal.

---

## Feature Request Trends

The following are the most commonly requested feature directions distilled from recent issues:

### 1. AST-Aware Tooling (Codebase Mapping & File Reads)
- **Related Issues:** [#22745](https://github.com/google-gemini/gemini-cli/issues/22745) | [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)
- **Trend:** Users want the CLI to understand code structure precisely—reading method bounds in one call rather than guessing line ranges.

### 2. Agent "Self-Awareness" & Sub-agent Trajectory Visibility
- **Related Issues:** [#21432](https://github.com/google-gemini/gemini-cli/issues/21432) | [#22598](https://github.com/google-gemini/gemini-cli/issues/22598) | [#21763](https://github.com/google-gemini/gemini-cli/issues/21763)
- **Trend:** Users want the CLI to know its own flags/hotkeys, and they want subagent trajectories visible in `/chat share` and `/bug` reports for debugging and review.

### 3. Better Component-Level Evaluations (Behavioral Evals)
- **Related Issues:** [#24353](https://github.com/google-gemini/gemini-cli/issues/24353)
- **Trend:** A large EPIC for systematic evals across 6 supported models, particularly for subagent behaviors like browser and generalist.

### 4. OS Sandboxing with Zero-Dependency
- **Related Issues:** [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)
- **Trend:** The community wants robust sandboxing for bash operations that leverages the model's natural affinity for POSIX tools without risking user security.

### 5. Native File Tools for Task Tracking
- **Related Issues:** [#21000](https://github.com/google-gemini/gemini-cli/issues/21000)
- **Trend:** Experiment with using native file tools instead of separate task-tracking mechanisms to reduce complexity and failures.

---

## Developer Pain Points

The following are recurring frustrations from the community and maintainers in the past 24 hours of issue traffic:

### 1. Misleading Termination Reasons
- **Pain Point:** Subagents report "GOAL success" when they actually hit MAX_TURNS or crashed (e.g., Wayland).
- **Impact:** The main agent trusts bad subagent output, causing silent failures.
- **Evidence:** [#22323](https://github.com/google-gemini/gemini-cli/issues/22323), [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)

### 2. Model Over-Delegation & Ignoring Developer Instructions
- **Pain Point:** Model defers to subagents even when configurations disable them; it also under-utilizes custom skills (skills won't activate without explicit prompting).
- **Impact:** Broken workflows, disabled feature surprise, inefficiency.
- **Evidence:** [#22093](https://github.com/google-gemini/gemini-cli/issues/22093), [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)

### 3. Shell Hangs & Interactive Prompt Stalls
- **Pain Point:** The CLI hangs on completed shell commands (shows "Waiting input") or gets stuck at interactive prompts (e.g., Vite scaffolders).
- **Impact:** Long timeouts; community notices P1 core bugs around these.
- **Evidence:** [#25166](https://github.com/google-gemini/gemini-cli/issues/25166), [#22465](https://github.com/google-gemini/gemini-cli/issues/22465)

### 4. Random tmp Script Sprawl
- **Pain Point:** Model creates scattered temporary scripts when restricted from direct shell editing, polluting the workspace for clean commits.
- **Impact:** Developer cleanup overhead and increased error surface.
- **Evidence:** [#23571](https://github.com/google-gemini/gemini-cli/issues/23571)

### 5. Memory System Inefficiency & Security Concerns
- **Pain Point:** Auto Memory retries low-signal sessions indefinitely; bad patches are silently skipped; secrets sent to the model unredacted.
- **Impact:** Wasted tokens, potential data leakage, memory index inconsistency.
- **Evidence:** [#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523), [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)

### 6. Tools Overhead (>128 tools) causing 400 Errors
- **Pain Point:** Users with many MCP servers hit API limits with tool counts >128 but the CLI doesn't scope or prune tools automatically.
- **Impact:** Requests fail entirely; poor "power user" experience.
- **Evidence:** [#24246](https://github.com/google-gemini/gemini-cli/issues/24246)

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-05

## Today's Highlights
A new patch release (v1.0.79-1) introduces a breaking configuration change renaming `allowDevToolCaches` to `allowDevToolAccess`, which will require action from users who had explicitly opted out. Meanwhile, the community is raising concerns around a new MCP initialization failure with FastMCP servers, a `view` tool regression that has persisted since v1.0.72, and a growing chorus for custom themes and session management features. Several low-quality/spam issues were filed and closed, but the signal-to-noise ratio remains strong.

---

## Releases

### v1.0.79-1
- **Breaking change**: The sandbox setting `allowDevToolCaches` has been renamed to `allowDevToolAccess`. The new key now grants dev-tool config and registry access in addition to caches. The old key is **silently ignored** — if you had set it to `false` (opt-out), the behavior reverts to the default (enabled). You must rename the key in your settings.
- Smaller improvements included; no further details provided in the release notes.

---

## Hot Issues (Top 10)

1. **[#1504 — Add custom theme support](https://github.com/github/copilot-cli/issues/1504)** · *Open* · 8 💬 · 23 👍  
   Users want to define and share custom themes (e.g., JSON files) via `/theme`. Strong community demand; one of the most-upvoted open feature requests.

2. **[#1285 — Org-level Agents not showing up](https://github.com/github/copilot-cli/issues/1285)** · *Open* · 7 💬 · 9 👍  
   Agents defined in `{org}/.github-private` don't appear in CLI or VS Code. Despite correct templating, discovery fails — a friction point for enterprise adoption.

3. **[#2692 — Web Search tool fails via github-mcp-server](https://github.com/github/copilot-cli/issues/2692)** · *Closed* · 6 💬 · 2 👍  
   MCP streamable HTTP errors when using Web Search tools. Contributors are debugging POST endpoint failures between the CLI and the MCP server.

4. **[#4328 — Ctrl+H misread as Ctrl+Backspace under WSL2](https://github.com/github/copilot-cli/issues/4328)** · *Open* · 5 💬  
   `WT_SESSION` leaks from Windows Terminal into WSL2, causing `ctrl+h` (delete char) to behave like `ctrl+w` (delete word). A subtle but annoying terminal-environment bug.

5. **[#4005 — Copilot billing entity isn’t selected](https://github.com/github/copilot-cli/issues/4005)** · *Open* · 4 💬 · 3 👍  
   In enterprise setups, memory saving fails with "Copilot billing entity isn't selected" even though everything else works. Likely an entitlements/SSO edge case.

6. **[#4202 — Built-in view tool: "Path does not exist" regression](https://github.com/github/copilot-cli/issues/4202)** · *Open* · 4 💬  
   `view` tool fails on existing files since v1.0.72; v1.0.71 works. Isolated repro shows the CLI, not the SDK, is at fault. Still unresolved in v1.0.73.

7. **[#1697 — Session forking for parallel workstreams](https://github.com/github/copilot-cli/issues/1697)** · *Open* · 3 💬 · 25 👍  
   Request to branch a conversation into parallel sessions with shared context. High demand (25 👍) — a popular power-user workflow enabler.

8. **[#4370 — MCP init fails when server/discover returns -32602](https://github.com/github/copilot-cli/issues/4370)** · *Open* · 1 💬  
   New (filed today): FastMCP servers don't implement `server/discover`; the CLI treats the `-32602` error as fatal, blocking MCP initialization entirely.

9. **[#4267 — Input box pre-filled with DA1 escape sequence](https://github.com/github/copilot-cli/issues/4267)** · *Open* · 2 💬  
   On native-Windows zellij, the input box starts pre-filled with raw terminal escape codes (`[?61;6;7;…c`) — a terminal-handshake parsing bug.

10. **[#4361 — Plugin slash commands now fire doomed RPC](https://github.com/github/copilot-cli/issues/4361)** · *Open* · 1 💬  
    Desktop-app client used to rewrite `/plugin-skill` to natural language; now it invokes `session.commands.invoke` which fails. Regression likely at CLI boundary.

---

## Key PR Progress

1. **[#4355 — "Merge"](https://github.com/github/copilot-cli/pull/4355)** · *Open*  
   Title-only; no description. Appears to be a placeholder or a WIP merge PR. Low signal.

2. **[#4366 — Security findings resolution (Vault)](https://github.com/github/copilot-cli/pull/4366)** · *Open*  
   Automated PR from `vault-chatops[bot]` addressing fundamentals security findings for `copilot-cli` in `ci` and `production`. Requires manual review and placeholder replacement before merge.

> **Note:** Only 2 PRs were updated in the last 24 hours, and neither adds user-facing features. Community PRs are sparse today; the majority of activity is issue-driven.

---

## Feature Request Trends

- **Custom themes & theming accessibility** — Multiple requests for user-created, shareable themes (#1504) and complaints about contrast issues (#3898).
- **Session lifecycle control** — Cloud-synced sessions (#1947), session forking (#1697), and explicit session deletion (#2019) all remain popular.
- **BYOK / third-party model support** — Interest in connecting custom LLM endpoints (e.g., Azure, GCP, local) remains steady (#4139).
- **Plugin auto-update** — Strong demand (29 👍) for automatic plugin updates (#1709).
- **Usage/cost visibility** — Requests for persistent token/context indicators (#2532, #4174) signal a need for better observability.

---

## Developer Pain Points

- **Cross-platform terminal quirks** — WSL2 and native-Windows issues (Ctrl+H misinterpretation #4328, DA1 pre-fill #4267) highlight recurring input-handling bugs on Windows/Linux hybrids.
- **MCP integration fragility** — Errors with `server/discover`, streamable HTTP POST failures, and strict schema validation are blocking real-world MCP server usage (#2692, #4370, #4349).
- **Enterprise configuration friction** — Billing entity not selected (#4005), managed policy enum mismatch (#4349), and org-level agent discovery failures (#1285) complicate enterprise rollouts.
- **Silent breaking changes** — The `allowDevToolCaches` → `allowDevToolAccess` rename is silently ignored if outdated, reverting security opt-outs to defaults. Community expects fail-loud behavior for deprecated keys.
- **Regression-prone built-in tools** — The `view` tool bug (#4202) has persisted across multiple versions (1.0.72 → 1.0.73+), eroding trust in built-in file operations.

---

*Digest generated from public GitHub data for `github/copilot-cli` on 2026-08-05.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-08-05**

---

### 1. Today's Highlights

The community's long-standing feature requests for a persistent **Memory System** (#1283) and **Remote Control** (#1282) remain the hottest discussion topics, with continued engagement 5 months after their creation. A newly filed issue (#2586) highlights a critical reliability concern: agent behavior degrades sharply at roughly **500K tokens** of context fill, leading to repetitive action loops and instruction drift in long-running sessions. Meanwhile, two PRs aiming to stabilize long shell commands (#2200) and introduce a universal `AI_AGENT` environment marker (#2585) are making progress.

---

### 2. Releases

No new releases in the last 24 hours.

---

### 3. Hot Issues

1. **[#1283] Feature Request: Memory System - Persistent context across sessions**  
   *Author: CatKang | Comments: 17*  
   One of the most awaited features: automatic AI-managed memory plus user-defined instructions to persist across sessions. The high comment count indicates strong community demand for reducing repetitive setup.  
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/1283)

2. **[#1282] Feature Request: Remote Control - Continue local sessions from any device**  
   *Author: CatKang | Comments: 12 | 👍 24*  
   Users want to move between devices while keeping their local session context. The 24 thumbs-up show this is a broadly shared workflow pain point.  
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/1282)

3. **[#2586] Agent reliability degrades at high context fill (~500K tokens)**  
   *Author: GrokBuildMJW | Comments: 1*  
   Critical bug report describing **repetitive action loops**, **no escalation**, and **instruction drift** in long sessions. Potentially a blocking issue for deep agentic workflows.  
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2586)

4. **[#2584] Bug: Thai (and other IME-based) characters duplicated on Windows**  
   *Author: mgprona | Comments: 0*  
   Input duplication affects Thai and other IME users on Windows 11; a quality-of-life blocker for non-Latin script users.  
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2584)

5. **[#2583] ACP: advertise available models + mid-session switching**  
   *Author: tizerluo | Comments: 0*  
   Mobile and IDE clients currently cannot discover or switch models mid-session; needed for full ACP protocol parity.  
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2583)

---

### 4. Key PR Progress

1. **[#2200] fix(shell): adapt timeouts for long commands**  
   *Author: he-yufeng*  
   Automatically extends timeouts for slow operations (git fetch, installs, builds) while keeping 60s default for normal commands. Reduces false failures in CI and batch processing.  
   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2200)

2. **[#2585] feat(cli): set AI_AGENT for subprocesses**  
   *Author: complynx*  
   Exposes `AI_AGENT=kimi` to subprocesses for both pip/uv and binary entrypoints, with support for wrapper-provided overrides. Standardizes agent detection in build tooling.  
   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2585)

3. **[#2364] feat(acp): support permission mode switching**  
   *Author: huntharo*  
   Adds protocol-level ACP permission mode switching (stacks on #2363). Required for safe file-system edits from mobile/IDE clients, and addresses issue #1414.  
   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2364)

---

### 5. Feature Request Trends

- **Persistence & mobility**: The highest-demand features are **persistent memory** (#1283) and **remote session continuation** (#1282), both from the same author and unchanged in popularity.
- **ACP protocol maturity**: Requests for model advertisement, mid-session switching (#2583), and permission mode switching (#2364) indicate the community is pushing for a complete ACP integration, particularly for mobile-first clients.
- **Subprocess integration**: The `AI_AGENT` marker (#2585) reflects a desire for external tooling (build systems, CI) to reliably detect Kimi CLI as the orchestration agent.

---

### 6. Developer Pain Points

- **High-context degradation**: Issue #2586 describes non-linear reliability loss around ~500K tokens; involving repetitive loops and instruction drift. This is a systemic risk for users running multi-step, tool-heavy coding sessions.
- **IME input bugs on Windows**: Issue #2584 highlights input duplication for Thai and other IMEs—an accessibility issue that disproportionately affects non-English developers.
- **Model discoverability in ACP**: Clients like Zed and mobile apps cannot see or change models mid-session (#2583), limiting configuration options for context-heavy tasks.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-05

## Today's Highlights
A wave of reports emerged today around **DeepSeek V4 Flash** instability across both the Go plan and free tiers, with users seeing blank responses, 403 errors, and model mismatches on the same API key. This is compounded by a growing call for a **public usage/balance API** for the Go plan (#16017), which has accumulated significant traction. On the positive side, the team is actively merging contributor fixes that harden tool-call classification across Anthropic, Gemini, and OpenAI-compatible providers, signaling a strong push toward output reliability.

## Releases
**v1.18.13** — Focused on interface reliability:
- **TUI:** GitHub pull request review context now includes PR number and URL.
- **Desktop:** Fixed multiple right-to-left (RTL) layout issues across tabs, drawers, resizing, and titlebar interactions, plus shared directional icon behavior.

## Hot Issues
1. **[#16017](https://github.com/anomalyco/opencode/issues/16017) — [FEATURE] Go plan usage/balance API endpoint** — 29 comments, 126 👍. Long-standing request to expose subscription usage via public API; dashboard-only visibility is limiting for developers building tooling around the Go plan.
2. **[#39845](https://github.com/anomalyco/opencode/issues/39845) — DeepSeek V4 Flash suddenly requires "Enable models hosted in China"** — 15 comments, 22 👍. Mid-session breakage that forces an explicit opt-in for China-hosted models, interrupting workflows on the Go subscription.
3. **[#40471](https://github.com/anomalyco/opencode/issues/40471) — OpenCode Agents not replying** — 13 comments. Agent hangs at "thinking" indefinitely; high volume of similar reports suggests a systemic issue with model output handling.
4. **[#22235](https://github.com/anomalyco/opencode/issues/22235) — IDE (VSCode) `Context Awareness` function didn’t take effect** — 12 comments, 7 👍. Long-running complaint; selection-based context attachment works in Claude Code but not in the OpenCode VSCode extension, affecting code-assist workflows.
5. **[#40533](https://github.com/anomalyco/opencode/issues/40533) — [CLOSED] Abusive spam issue** — 9 comments. Content removed for compliance; highlights ongoing moderation challenges and potential bot-driven spam in the tracker.
6. **[#34498](https://github.com/anomalyco/opencode/issues/34498) — [FEATURE] Respect `disable-model-invocation: true` in SKILL.md frontmatter** — 9 comments, 48 👍. Request to align with Claude Code and Cursor's behavior for skills; strong community support indicates growing dependency on SKILL.md-driven workflows.
7. **[#40483](https://github.com/anomalyco/opencode/issues/40483) — DeepSeek v4 Flash Free returns blank response in Desktop on Windows 11** — 7 comments. Visual "thinking" and completion sound play but the response area stays blank; UI appears hung.
8. **[#40485](https://github.com/anomalyco/opencode/issues/40485) — `deepseek-v4-flash` via opencode-go returns 403/hangs, while pro and minimax-m3 work** — 6 comments, 6 👍. Provider-specific failure isolated to the flash model on the Go plan, not the API key or config.
9. **[#40460](https://github.com/anomalyco/opencode/issues/40460) — [CLOSED] DeepSeek v4 Flash Model not responding** — 5 comments, 7 👍. Same root cause family: stuck at "Thinking..." with no output; closed likely as duplicate.
10. **[#38723](https://github.com/anomalyco/opencode/issues/38723) — `opencode run` intermittently hangs during init (~56% failure)** — 4 comments, 1 👍. Serious headless reliability issue: no session, no output, no error; external timeout required.

## Key PR Progress
1. **[#40549](https://github.com/anomalyco/opencode/pull/40549) — fix(ai): classify malformed Responses tool calls** — Distinguishes successfully decoded function calls from malformed input; treats output with only malformed tool calls as `error` instead of `tool-calls`. Aims to reduce false-positive tool result handling.
2. **[#40547](https://github.com/anomalyco/opencode/pull/40547) — fix(ai): derive Anthropic tool finish reason** — Normalizes benign `end_turn`/`stop_sequence` as `tool-calls` when local tool work exists, preserving raw provider values for diagnostics.
3. **[#40546](https://github.com/anomalyco/opencode/pull/40546) — fix(ai): preserve Gemini tool finish semantics** — Treats parsed client tool calls as `tool-calls` even when `finishReason` is absent, preserving provider-native null reason.
4. **[#40545](https://github.com/anomalyco/opencode/pull/40545) — fix(opencode): add model attribution to `run --format json` step events** — Adds model info to `step_start`/`step_finish`, enabling headless consumers to attribute token/cost per step.
5. **[#40538](https://github.com/anomalyco/opencode/pull/40538) — fix(core): make xAI OAuth device-only** — Replaces loopback OAuth with RFC 8628 device flow for local and remote SuperGrok access; removes PKCE/CORS complexity.
6. **[#40537](https://github.com/anomalyco/opencode/pull/40537) — fix(opencode): make xAI OAuth device-only** — Parallel implementation in the opencode package; same intent as #40538 with tests and docs updates.
7. **[#40542](https://github.com/anomalyco/opencode/pull/40542) — fix(core): clarify platform tool failures** — Improves error messages for missing shell working directories; formats Effect platform failures with reason/target/OS details.
8. **[#40427](https://github.com/anomalyco/opencode/pull/40427) — [beta] some experimental perf improvements** — Big renderer win: initial entry memory drops from 7.45 MB to 1.82 MB (-75.5%) against a fixed corpus; significant for large sessions.
9. **[#40487](https://github.com/anomalyco/opencode/pull/40487) — fix(core): retire legacy provider aliases** — Removes Azure Cognitive Services and Vertex Anthropic as standalone providers; migrates legacy provider IDs in configs and policies.
10. **[#40535](https://github.com/anomalyco/opencode/pull/40535) — fix: retry empty incomplete streams** — Classifies terminal-less streams as `incomplete-stream` and retries them only when no model output has started, avoiding silent empty turns.

## Feature Request Trends
- **Usage analytics API (#16017):** Strong demand for a public API exposing Go plan usage and balance across rolling/weekly/monthly windows, likely to power third-party dashboards and cost controls.
- **SKILL.md frontmatter (#34498):** Aligning with Claude Code/Cursor by honoring `disable-model-invocation`, indicating community adoption of declarative skill configurations.
- **Flatpak first-class support (#39670):** Gate auto-updater on `FLATPAK_ID` and use Flatpak UpdateMonitor portal; signals growing Linux desktop usage.
- **UX safety on macOS (#40510):** Request for configurable confirmation before `Ctrl+D` exit to prevent accidental session loss in Ghostty.
- **Session lifecycle automation (#40403):** Auto-compaction of stale long-running sessions to reduce token/cost waste on resume.

## Developer Pain Points
- **DeepSeek V4 Flash instability is the top friction point today:** Recurring themes are blank responses after "thinking," 403s via the Go plan, and model mismatch (returning V3.2 rather than V4 Flash 0731). Multiple closed duplicates and global reports (English, Spanish, Turkish) indicate a service-side issue, not user config.
- **Headless reliability remains fragile:** `opencode run` hanging ~56% of the time during init with no output or error (#38723) is a serious blocker for CI/integration use cases.
- **Inconsistent SSE/streaming behavior:** The Go service's `/v1/responses` endpoint emits incomplete SSE event sequences (#40171), breaking Codex-style clients — a pain point for API consumers.
- **Desktop app startup flakiness (#40516):** Failure to load provider/model/MCP information in ~80% of starts across v1.18.5–v1.18.13 (v1.18.4 works) is a notable regression for enterprise adoption.
- **VSCode extension context blindness (#22235, #40540):** The IDE extension fails to see active selections or tabs, undermining context-awareness features that developers expect from a modern AI coding tool.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-05

## Today's Highlights
The past 24 hours saw a significant cluster of compaction-related bug reports, particularly for GitHub Copilot Enterprise seats, with multiple issues and fixes converging on the same root cause: summarization requests bypassing the resolved `baseUrl` and provider-specific headers. Meanwhile, the project continues its steady march toward a v2 harness with a new server session backend, SQLite lane-aware storage, and RPC-over-socket support landing in PRs.

## Releases
No new releases in the last 24 hours.

## Hot Issues
Here are 10 noteworthy issues that caught the community's attention:

1. **[#6768 — Compaction using Copilot Enterprise not possible](https://earendil-works/pi/issues/6768)** · 19 comments · 18 👍
   The most-discussed bug of the day: compaction fails on Copilot Enterprise licenses with `421 Misdirected Request` errors for both OpenAI and Anthropic paths. Multiple reports confirm this is a systemic issue with how compaction requests are routed on enterprise seats.

2. **[#5023 — Terminal scrolls to beginning without reason](https://earendil-works/pi/issues/5023)** · 11 comments · 1 👍
   A long-standing, unresolved UX annoyance: the terminal randomly jumps to the start of the session while a model is generating output, then scrolls back to the end. This has been open since May and continues to attract reports.

3. **[#7547 — How do you use Pi on Windows? What issues are you seeing?](https://earendil-works/pi/issues/7547)** · 11 comments
   An intentionally opened community-gathering issue to systematically identify Windows-specific problems. Several Windows bugs from the last 24h (find tool, loadSkills, SQLite) suggest this is a much-needed triage effort.

4. **[#7161 — anthropic-messages never sends x-client-request-id](https://earendil-works/pi/issues/7161)** · 10 comments
   A protocol-consistency bug: the Anthropic path omits `x-client-request-id`, breaking session affinity for gateways that round-robin between multiple Claude accounts. This breaks proxy setups that work fine with OpenAI paths.

5. **[#7413 — Compaction fails on GHE.com enterprise accounts — "unknown stamp" error](https://earendil-works/pi/issues/7413)** · 6 comments
   A sibling of #6768: `/compact` on GHE.com accounts fails with `unknown stamp "prod-cus-01"` during IDE authentication. Normal chat works fine — only compaction is affected, making it particularly confusing for users.

6. **[#7553 — Configurable thinking level/model for compaction](https://earendil-works/pi/issues/7553)** · 6 comments
   A well-reasoned feature request: compaction currently reuses the session's thinking level, which is wasteful and uncontrollable on reasoning models. Pull request #7602 is already addressing this.

7. **[#7508 — GitHub Copilot / OpenAI Codex OAuth refresh has no request timeout](https://earendil-works/pi/issues/7508)** · 5 comments
   A serious reliability bug: a stalled token refresh holds the cross-process credential-store lock, freezing the session for ~5 minutes. This is a classic "one bad network moment ruins the whole day" issue.

8. **[#7395 — JSON mode serializes cumulative assistant state on every delta](https://earendil-works/pi/issues/7395)** · 3 comments
   A performance bug with quadratic output growth: every `message_update` in `--mode json` contains the full accumulated assistant message, causing massive stdout drains on long sessions.

9. **[#7594 — node:sqlite missing in release binary causing plugin breakage](https://earendil-works/pi/issues/7594)** · 4 comments
   A packaging regression: extensions using the `node:sqlite` built-in fail to load in release binaries with `No such built-in module`. This blocks plugins like `pi-total-recall` and any future SQLite-dependent extensions.

10. **[#7628 — Security: 0.83.0 shrinkwrap pins vulnerable undici and brace-expansion](https://earendil-works/pi/issues/7628)** · 1 comment
    A security advisory: the published package pins `undici@8.5.0` (patched in 8.9.0) and `brace-expansion@5.0.7` (patched in 5.0.8/5.0.9). `npm audit` flags both, which is a red flag for teams with strict supply-chain policies.

## Key PR Progress
Ten PRs worth watching:

1. **[#7632 — fix: retry transient management HTTP requests](https://earendil-works/pi/pulls/7632)** — Retries idempotent management requests to pi.dev, GitHub releases, and tools. Fixes #6675 and likely several flaky-proxy issues. A robust resilience improvement.

2. **[#7602 — feat(coding-agent): configurable summarization models](https://earendil-works/pi/pulls/7602)** — Adds configurable models and thinking levels for compaction and branch summaries, with provider-error handling for context-window limits. Directly closes #7553.

3. **[#7619 — feat(coding-agent): resume failed turn by selecting it in /tree](https://earendil-works/pi/pulls/7619)** — Failed assistant entries in the tree view can now be selected to retry the turn, with retried responses continuing under the original error entry. Closes #7609. Great for flaky-network resilience.

4. **[#7396 — feat(coding-agent): add server session backend](https://earendil-works/pi/pulls/7396)** — A durable JSONL-based backend for `PiServer` with cross-process locking, crash recovery, and project-harness event streaming. Core infrastructure for the v2 architecture.

5. **[#7591 — refactor: update sqlite for lanes](https://earendil-works/pi/pulls/7591)** — Lane-aware SQLite session storage: lane records, moves, global facts, and branch-cache split across tables. Closes the durability gap in the v2 harness.

6. **[#7624 — feat(coding-agent): render Mermaid diagrams](https://earendil-works/pi/pulls/7624)** — Closes #7623. Likely long-awaited by users who want readable architecture diagrams in chat output.

7. **[#7612 — fix(tui): add size param to iterm2 image encoder](https://earendil-works/pi/pulls/7612)** — Fixes image rendering for xterm.js: `@xterm/addon-image@0.9.0` rejects OSC 1337 sequences without `size`. A small fix with a wide impact for web-based terminals.

8. **[#7621 — feat(rpc): expose argument completions via get_argument_completions](https://earendil-works/pi/pulls/7621)** — Unlocks slash-command argument completions for embedded clients (e.g., web UIs) that previously only existed in the TUI.

9. **[#7605 — fix(ai): keep response bodies out of OAuth error messages](https://earendil-works/pi/pulls/7605)** — Security hardening: token-endpoint response bodies (which contain tokens and echoed request parameters) were leaking into logs, telemetry, and user-facing dialogs. Now sanitized.

10. **[#7599 — rpc over sockets](https://earendil-works/pi/pulls/7599)** — Adds `--listen` for RPC over Unix socket or TCP, plus a `connectAddress` option for `RpcClient`. Enables out-of-process and remote clients — a significant step for embedding Pi.

## Feature Request Trends
- **Configurable compaction** — Several issues and PRs converge on making compaction independent from session settings (model, thinking level, and provider routing). As context windows grow, users want summarization to be a first-class, tunable operation.
- **Richer terminal integration** — Mermaid rendering, iTerm2 image size parameters, and fullscreen-dock fixes show a drive toward making Pi a full-fledged rich terminal app, not just a chat REPL.
- **Provider breadth** — New providers (Cortecs, LLM Gateway, Qwen Token Plan Individual) keep arriving. The trend is toward router-style providers and enterprise-specific subscription tiers.
- **RPC/embedding enhancements** — Argument completions, socket listeners, and provider auth exposure via RPC indicate a clear push toward building UIs and tooling on top of Pi.

## Developer Pain Points
- **Copilot Enterprise compaction is consistently broken** — The recurring theme of #6768 and #7413 (plus the merged fix in #7579) suggests compaction on enterprise seats has been flaky for weeks, and users are getting frustrated.
- **Cross-provider protocol inconsistencies** — Anthropic paths missing headers and Deepseek rejecting `developer` roles (#7603) highlight the cost of supporting many backends. Users expect identical behavior regardless of provider.
- **Windows remains a second-class citizen** — `find` glob patterns fail (#6817), `loadSkills` throws path-relative errors (#7427), and the maintainers explicitly asked "what issues are you seeing?" (#7547). Windows users can expect a wave of fixes soon, but the problems are clearly systemic.
- **Diagnostics are hard to get right** — `pi version` doesn't report the runtime (bun vs node), JSON mode has quadratic output, and transient errors leave permanent red lines in the chat (#7613). Developers want better observability and non-destructive error reporting.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-05

## Today's Highlights

The Qwen Code team shipped stable v0.21.5 with a key migration bridge for macOS users moving from the legacy Electron shell to the new Tauri-based desktop app, alongside detailed tool-call outcome tracking. Meanwhile, the community is actively surfacing reliability issues around cancellation semantics, daemon resource governance, and ACP/JetBrains integration gaps, with over a dozen high-traffic issues and PRs converging on execution boundaries and session-state integrity. The maintainers are responding with a wave of PRs focused on hardening the `/review` pipeline, closing trust-boundary holes in hooks, and improving Web Shell multi-workspace handling.

## Releases

### v0.21.5 (stable)
- **macOS Electron → Tauri migration bridge**: opt-in one-time update path for desktop users ([#8392](https://github.com/QwenLM/qwen-code/pull/8392))
- **Detailed execution-specific outcome tracking** for tool calls

### v0.21.6-preview.0
- **Browser extension alpha readiness diagnostics** ([#6739](https://github.com/QwenLM/qwen-code/pull/6739))
- **Documentation for headless Goal workflows**

### v0.21.5-nightly.20260805
- Same browser-ext diagnostics and headless Goal docs as preview

### v0.21.4-nightly.20260804
- Electron-to-Tauri bridge (same as #8392)
- Web shell table dialog fixes

## Hot Issues

1. **[#8102 — Deterministic tool-execution boundaries for trustworthy agent runtime](https://github.com/QwenLM/qwen-code/issues/8102)** (17 comments)  
   A foundational proposal to keep the LM outside the trust boundary and constrain/authorize/observe model actions deterministically. High engagement signals strong community appetite for runtime-level safety guarantees.

2. **[#8519 — Severe screen flickering in tmux](https://github.com/QwenLM/qwen-code/issues/8519)** (11 comments)  
   Qwen Code flickers 1–2× per second under tmux on Linux. Closed, but the volume of similar rendering complaints suggests broader terminal-rendering quality concerns.

3. **[#8051 — Bound multi-workspace daemon resource usage](https://github.com/QwenLM/qwen-code/issues/8051)** (9 comments)  
   Count-only limits don't bound bytes held by request bodies, WebSocket assembly, or other memory. Continues the theme of daemon resource governance.

4. **[#8136 — Provider warning sanitizer truncates ports, leaks passwords containing `@`](https://github.com/QwenLM/qwen-code/issues/8136)** (6 comments)  
   Security-relevant URL sanitization bug with an easy-to-trigger, potentially credential-exposing edge case.

5. **[#8356 — After APIUserAbortError, subsequent turns not written to transcript](https://github.com/QwenLM/qwen-code/issues/8356)** (5 comments)  
   Session transcript corruption after interruption—directly undermines `--resume` reliability.

6. **[#8493 — Cancelled file tools can still mutate files](https://github.com/QwenLM/qwen-code/issues/8493)** (5 comments)  
   `write_file`/`edit` proceed with filesystem writes even after abort. Serious safety/cancellation-semantics defect raised by maintainer `ryan-mt`.

7. **[#8532 — CI logs make mocked disk-full tests look like runner ENOSPC](https://github.com/QwenLM/qwen-code/issues/8532)** (4 comments)  
   Test noise masquerading as infrastructure failure—highlighted by `yiliang114`. Wastes maintainer triage time.

8. **[#8550 — `qwen mcp list` hangs indefinitely on SSE server without `endpoint`](https://github.com/QwenLM/qwen-code/issues/8550)** (3 comments)  
   Fresh issue (today) with a clear repro: missing timeout handling in SSE MCP transport.

9. **[#8533 — Content[]/Part[] cannot safely encode per-provider reasoning-replay contracts](https://github.com/QwenLM/qwen-code/issues/8533)** (4 comments)  
   Foundational data-model problem for provider-specific reasoning metadata. Impact spans session resume, auditability, and multi-provider consistency.

10. **[#8544 — ACP task list not rendered in JetBrains](https://github.com/QwenLM/qwen-code/issues/8544)** (3 comments)  
    Compared unfavorably to Claude Code/Codex in the same ACP UI. Part of a broader JetBrains/ACP feature gap (see also #8513, #8514).

## Key PR Progress

1. **[#8392 — Bridge Electron users to Tauri updates](https://github.com/QwenLM/qwen-code/pull/8392)**  
   Opt-in one-time migration path for macOS desktop users. Shipped in v0.21.5.

2. **[#8396 — Close four trust-boundary holes in hook execution](https://github.com/QwenLM/qwen-code/pull/8396)**  
   HTTP hooks no longer follow redirects; SSRF/DNS-level checks; other execution/network egress hardening. Critical security work.

3. **[#8213 — Establish workspace runtime ownership](https://github.com/QwenLM/qwen-code/pull/8213)**  
   Five-state runtime snapshot, workspace-scoped epochs, physical work leases, bounded startup/teardown. Directly addresses daemon resource-governance issues.

4. **[#8498 — Retire dry chunks and pipeline verification in reverse audit](https://github.com/QwenLM/qwen-code/pull/8498)**  
   Performance fix for `/review` on large PRs—removes the slowest loop in the reverse-audit path.

5. **[#8471 — Cost ledger from records already on disk](https://github.com/QwenLM/qwen-code/pull/8471)**  
   Forensic tooling to explain "0.21.3 was fine, 0.21.4 got slow" without hours of manual telemetry replay. Strong observability win.

6. **[#8443 — Click to expand/collapse thought while streaming](https://github.com/QwenLM/qwen-code/pull/8443)**  
   UX fix in the interactive CLI: enables thought-block toggling during streaming.

7. **[#8439 — Ctrl+click hyperlinks and right-click context menu in VP mode](https://github.com/QwenLM/qwen-code/pull/8439)**  
   Restores two native terminal capabilities lost when SGR mouse tracking was enabled.

8. **[#8353 — ESC cancels ongoing work before popping queued messages](https://github.com/QwenLM/qwen-code/pull/8353)**  
   Fixes a frustrating interaction where ESC during streaming was swallowed by prompt-queue logic.

9. **[#8548 — Build review CLI bundle once per scan, fan out to legs](https://github.com/QwenLM/qwen-code/pull/8548)**  
   Eliminates repeated `npm ci` + build in autofix review fan-out. Meaningful CI cost reduction.

10. **[#8445 — Web Shell session refresh with daemon auth](https://github.com/QwenLM/qwen-code/pull/8445)**  
    Allows document navigation to load before bearer auth while protecting session API subpaths.

## Feature Request Trends

- **Deterministic, trustworthy agent runtime** (#8102): community pushing for hard guarantees on tool execution boundaries, authorization, and observability
- **ACP/JetBrains parity** (#8513, #8514, #8544): repeated demand for context-usage indicators, reasoning-effort tiers, and task-list rendering in ACP clients
- **Daemon resource governance** (#8051, #8182, #8213): bounded memory/CPU per workspace and per child process, not just per-count limits
- **Provider ecosystem expansion** (#8368): first-class presets for Kimi and Xiaomi MiMo
- **CI worktree/review hygiene** (#8474, #8548, #8549): automation reliability and cost reduction

## Developer Pain Points

- **Cancellation semantics are inconsistent**: file tools mutate after abort (#8493), ESC behaves unpredictably (#8353), signal-terminated shells report success (#8491), interrupted turns corrupt transcripts (#8356)
- **Daemon/child memory governance is fragile**: 50% of host memory per ACP child regardless of count (#8182), unbounded request-body buffering (#8051)
- **Resume/session reconstruction hazards**: `--resume` can rebuild a dangling-unsigned-thought bug (#8535); transcript gaps after aborts (#8356)
- **Terminal rendering issues**: tmux flicker (#8519), lost native mouse capabilities (#8439), copy-response button broken on Windows (#8538)
- **MCP and config edge cases**: indefinite SSE hangs (#8550), stale session registrations on metadata hot reload (#8492), provider-warning sanitizer leaking passwords (#8136)

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-05

## 1. Today's Highlights

The DeepSeek TUI community is in the middle of a substantial performance-focused push, with maintainer Hmbown opening a coordinated set of build-time optimization issues (#5244–#5249) targeting the monolith `codewhale-tui` crate that dominates workspace compile times. Concurrently, the v0.9.4 release train (#5135) is in flight with 77 commits ahead of `main`, carrying extensive Runtime API additions generated by Copilot (goal-loop state, verifier receipts, memory, MCP lifecycle, skill lifecycle). Active community contributions are landing across MCP Registry discovery (#5238), subagent checkpoint resume (#5242), and several Windows/OpenHarmony fixes, while critical bugs around pricing endpoint failures and silent context-window degradation continue to draw attention.

## 2. Releases

No new releases in the last 24 hours. The v0.9.4 release train PR (#5135) is actively being integrated, and the v0.9.3 branch remains the latest stable.

## 3. Hot Issues

**#5209 — File edit silently accepts wrong parameter names** *(👍 0, 3 comments, NEW)*  
The `File` tool's `action=edit` mode accepts invalid parameter names (e.g., `new_str` instead of `replace`) and reports false success, forcing 3–5x re-edits per location. Critical tool-contract correctness bug that erodes agent trust in the tool layer.

**#4991 — Compilation times and the TUI crate monolith** *(👍 0, 4 comments)*  
Community member aboimpinto opens a discussion about the 682K-line, 620-file `codewhale-tui` crate being recompiled as one unit. This directly influenced maintainer Hmbown to spin up the build-performance epic (#5249) — a good example of community discussion driving maintainer action.

**#5249 — Epic: v0.9.5 build-time lane — stop the monolith tax** *(👍 0, 0 comments, NEW)*  
Maintainer-authored epic covering edit-compile, commit, test, and release loops. The `codewhale-tui` crate is 86% of the workspace and rebuilds entirely on any change. The most significant planned axis of improvement.

**#5239 — 1M context model triggers compression at 128K** *(👍 0, 1 comment)*  
Model context window is correctly advertised as 1M, but the tool triggers context compaction at the 128K legacy default. High-impact correctness bug for long-session users; the maintainer identified the root cause and opened follow-up #5244.

**#5241 — Pricing endpoint returns 503, all sessions show unverified_live_pricing** *(👍 0, 1 comment)*  
Cost display broke after upgrading from 0.8.67 to 0.9.3 across all providers. Session metadata consistently reports `unpriced_reasons = ["unverified_live_pricing"]` after a 503 from the pricing endpoint. Core UX regression for paid users.

**#4978 — Anthropic API error: 'type' must be in ["enabled","disabled","auto"]** *(👍 0, 6 comments)*  
Frequent 400 errors with OpenModel providers using the Anthropic-compatible Messages API. Intermittent failures with no fixed pattern — likely a schema-validation mismatch. Highest comment count in this batch indicates community engagement.

**#5248 — Shrink the 708-package build graph** *(👍 0, 0 comments, NEW)*  
Dependency graph has 708 packages, 95 with build scripts, 52 proc-macros all serialized ahead of use. At least 10 dependencies compile at 2–3 versions simultaneously. Direct contributor to the compile-time problem.

**#5245 — Local git commit forces full rebuild via HEAD-sha stamp** *(👍 0, 0 comments, NEW)*  
Build scripts watch the git branch ref so the embedded SHA stays fresh — every local commit recompiles the entire TUI+CLI even with zero source changes. The SHA is a `--version` flag that shouldn't dictate compile time.

**#5244 — Unknown model IDs silently degrade to 128K context** *(👍 0, 0 comments, NEW)*  
Residual class of #5239: unknown model IDs fall through to `LEGACY_DEEPSEEK_CONTEXT_WINDOW_TOKENS` (128K) with no surfaced hint. Users with 1M-window models get silent compaction at 128K. Maintainer flags 0.9.4 mitigates partially — still needs user-visible warnings.

**#5243 — OAuth login doesn't adopt freshly minted token** *(👍 0, 0 comments, NEW)*  
LIVE DOGFOOD bug (build 4a4f28768): successful xAI device login leaves the session without working credentials; the user must return to the provider picker and manually press `e` for the stored token to take effect. Broken first-run OAuth flow for xAI and ChatGPT/Codex.

**#4955 — Zero-sandbox / --no-sandbox mode for local dev** *(👍 1, 4 comments)*  
Request to run CodeWhale without any sandbox on the dev machine. The kernel-level Seatbelt sandbox breaks common shell commands daily. The only item with a 👍 in this batch — clear community demand.

## 4. Key PR Progress

**#5135 — Release: Codewhale v0.9.4 release train** *(OPEN, Hmbown)*  
77 commits ahead of `main`; supersedes #5044. Contains 18 train commits plus the 2026-08-01 source candidate. The integration point for all v0.9.4 features; most active PR in the repo.

**#5242 — Resume interrupted children from checkpoint via followup** *(OPEN, SparkofSpike)*  
Previously, `agents/followup` on an `interrupted_continuable` child queued a dead-letter — the checkpoint was preserved but resume was impossible. This enables true resume for long tasks (document review, multi-step search). Significant workflow-continuity upgrade.

**#5238 — MCP Registry discovery with Registry-first tool selection** *(OPEN, bistack)*  
Adds `registry_sync` to fetch eligible zero-environment stdio servers and selects registry MCP tools before falling back to `exec_shell` or custom code. Potential shift in how tools are sourced and used.

**#5225 — Expose file/search/git/patch/shell tools over ACP session/prompt** *(OPEN, rafaelcavalheri)*  
ACP server previously only streamed model text — tool calls were never executed. This enables real code-editing capabilities for Zed and third-party ACP bridges (community `acp-deepseek-adapter`). If merged, this turns CodeWhale into a full agent backend, not just a chat stream.

**#5133 — Expose persistent goal-loop state and completion controls** *(OPEN, Copilot)*  
Adds `GET /v1/threads/{id}/goal` and lifecycle transition endpoints. Closes the gap where managed clients could not read or drive active goals via the runtime boundary — critical for managed/automated deployments.

**#5132 — Expose verifier receipts and evidence beyond aggregate counter** *(OPEN, Copilot)*  
Adds read-only endpoints under `/v1/fleet/runs/{run_id}/` — `receipts` (durable task receipts), plus task-level failure identification and retry guidance. Fleet users get actionable verifier intelligence instead of a single `verifier_failed` counter.

**#5131 — Runtime API memory endpoints — bounded inspection and lifecycle** *(OPEN, Copilot)*  
Adds `/v1/memory` routes behind `require_runtime_token` for inspecting active memory, understanding provenance/scope, and applying lifecycle controls. Closes the gap where managed clients could not manage memory via HTTP.

**#5130 — Bounded MCP server configuration and lifecycle over HTTP** *(OPEN, Copilot)*  
Adds `POST /v1/apps/mcp/servers` and related mutation routes to add/update/remove MCP servers without hand-editing TOML/JSON. Managed clients no longer need config-file surgery.

**#5129 — Skill lifecycle endpoints — install, update, uninstall, trust, audit** *(OPEN, Copilot)*  
Previously only read/skill discovery and enable/disable were exposed; this PR adds full lifecycle (install, update, uninstall, trust, audit) behind `require_runtime_token`. Brings TUI-level skill management to the HTTP API.

**#5140 — Surface real wait elapsed time in tool content** *(OPEN, SparkofSpike)*  
Bash `wait`/delta tool results keep `duration_ms` in metadata only — the model cannot see it, so every wait looks identical whether it started or ran for minutes. This exposes elapsed time in tool content, fixing model busy-polling behavior.

## 5. Feature Request Trends

**Performance and build-time** — A dominant theme. The maintainer's #5249 epic, #5248 deps graph, #5245 SHA stamp, #5247 test binaries, #5246 profile split all target the monolith tax. Community discussion #4991 validates the pain.

**Sandbox flexibility** — #4955 requests `--no-sandbox` mode; the kernel-level Seatbelt sandbox breaks daily work on dev machines.

**Context window correctness** — #5239 (1M context compacts at 128K) and #5244 (silent fallback on unknown models) together demand user-visible context-window awareness; 0.9.4 mitigation is incomplete.

**OAuth token lifecycle** — #5243 reveals a broken first-run flow: fresh tokens don't get adopted without manual provider-picker intervention. Direct UX regression in onboarding.

**Pricing/reliability** — #5241's 503 pricing endpoint breaks session cost display across all providers post-0.9.3. Core paid-feature regression.

**Interoperability via ACP** — #5225 introduces real agent tool execution over ACP, signaling growing interest in driving CodeWhale from external editors (Zed, community bridges).

**Runtime API expansion** — Four Copilot-generated PRs (#5129–#5132) broaden the HTTP boundary: skills lifecycle, MCP management, memory inspection, verifier receipts, goal-loop controls. Managed-deployment path is being systematically completed.

## 6. Developer Pain Points

**Crushing compile times** — The 682K-line, 620-file `codewhale-tui` crate recompiles as one unit on every change, every SHA-stamped commit, and across 25 integration-test binaries. Developers spend more time watching cargo than coding. The 708-package graph adds 95 build scripts and 52 serialized proc-macros on clean builds. Explicitly raised in #4991; addressed by the #5240-series.

**Silent failures and false successes** — #5209's tool accepting invalid parameters and returning "Replacement applied" when no replacement happened is a trust-eroding pattern. #5244's silent context-window fallback compounds it. Developers can't tell when the tool actually did what was asked.

**Model/provider capability mismatches** — 1M-window models compacting at 128K, providers hitting "type must be in..." schema mismatches, unknown models falling back to legacy defaults — all point to a systemic need for capability discovery and honest surfacing of fallbacks.

**Unreliable sandbox** — #4955's "basic shell commands break daily" distillation isn't new; it's the loudest signal yet that the sandbox opt-in/opt-out design needs rethinking.

**First-run auth friction** — #5243's stale-token flow means users complete OAuth and still can't use the product until they manually trip the provider picker. Onboarding friction at the moment of highest user intent.

**Regression-prone release gates** — #5241's pricing 503 between patch versions, plus #5209's tool contract drift, suggest the release process needs stronger integration testing and contract checks — exactly what the build-time optimizations (#5246) will pay for with faster pre-push cycles.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*