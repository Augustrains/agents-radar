# AI CLI Tools Community Digest 2026-08-04

> Generated: 2026-08-04 01:16 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Comparison Report — 2026-08-04

## 1. Ecosystem Overview

The AI CLI tool landscape is consolidating around core reliability concerns—session state management, cost visibility, and cross-platform stability—while differentiating on orchestration paradigms. Multi-session coordination (Claude Code, Gemini CLI) and Windows/WSL first-class support (Codex, Pi, DeepSeek-TUI) are the two most prominent battlegrounds. Community demand for persistent memory, project-scoped configuration, and MCP protocol hardening spans all tools regardless of vendor. Notably, the same model-catalog bugs (gpt-5.6-luna capability gates) surface independently across Codex and Copilot CLI, suggesting shared upstream data quality issues. Tools are converging on delta-based JSON streaming (Pi, Qwen Code) and per-request model routing (Copilot CLI, OpenCode) as differentiating capabilities.

## 2. Activity Comparison

| Tool | Hot Issues (active) | PRs (24h) | Release Status | Note |
|---|---|---|---|---|
| **Claude Code** | 10 + ~2 new bugs | 2 (low) | v2.1.221 shipped (Focus view, sandbox mask) | High comment counts (52–61), 2 major regressions |
| **OpenAI Codex** | 10 + 3 sub-cluster | 10 (all closed/near-merge) | 2 pre-releases (alpha train) | Fast PR throughput, Windows issues dominating |
| **Gemini CLI** | 10 + 2 dupes | 10 (5 fix-core, 2 security) | Nightly v0.55.0 train | P1 correctness bugs + defensive hardening PRs |
| **Copilot CLI** | 10 + 3 closed | 0 | v1.0.78 + v1.0.78-3 shipped | Burst releases, low PR activity; issue triage phase |
| **Kimi CLI** | 3 | 8 (5 fix, 2 docs/refactor, 1 deps) | No release in 24h; quiet consolidation | Steady bug-fix momentum, memory feature pending |
| **OpenCode** | 10 + 3 notable | 10 | v1.18.12 shipped (Azure GPT-5.5 fix) | Active PRs, desktop UX and Unicode fixes |
| **Pi** | 10 + 3 surveys | 10 | No release in 24h; PR-heavy | Two independent quadratic-fix PRs (#7394, #7561) |
| **Qwen Code** | 10 | 10 | v0.21.4 patch; v0.21.5 workflow failed | High fixed/correctness PR volume, 1 P1 data-loss |
| **DeepSeek-TUI** | 10 | 12 (2 hygiene, 2 docs, 1 fix, rest merged) | v0.9.4 train (77 commits, 30-PR stack) | Release train effort dominates; hygiene debt unblocking |
| **Total** | ~93 tracked | ~82 PRs | 6 releases + 1 nightly + 1 train | — |

## 3. Shared Feature Directions

| Need | Tools | Specific Ask |
|---|---|---|
| **Cross-session coordination / memory** | Claude Code (#24798,#76727), Gemini CLI (#26522), Kimi (#1283), OpenCode (#16077,#27167), DeepSeek-TUI (#2492) | First-party primitives for sequencing parallel sessions; persistent memory with opt-in redaction; goal-scoped lifecycle |
| **Multi-model / BYOK selection** | Copilot CLI (#3282,#3709), OpenCode (#40268), Pi (#7560), Qwen Code (#8368) | Hot-swap models mid-session; per-request routing; multi-provider presets; catalog matching real specs |
| **Quota & cost transparency** | Claude Code (#13585,#65687), Codex (#33685), Qwen Code (#8452) | CLI-readable quota; idle-spike detection; cache-invalidation warnings; per-request token accounting |
| **MCP / ACP protocol hardening** | Gemini (#28481), Codex (#36810), Kimi (#2507), DeepSeek-TUI (#5225), Copilot CLI (#4346) | OAuth token refresh, per-surface tool exposure, registry compatibility, tool-call ID uniqueness, question semantics |
| **Windows/WSL reliability** | Codex (#20214, #35119), Pi (#7064, #6187), DeepSeek-TUI (#5095), Copilot CLI (#4328), Qwen Code (#8400) | Path translation, terminal keybinding fixes, IME input, process-group teardown, data-loss prevention |
| **Sandbox / permission control** | Gemini (#19873), Claude Code (mode mask), OpenCode (#40316), DeepSeek-TUI (#1917,#4959) | Zero-dependency OS sandbox, pre/post tool hooks, mechanical stop, nonblocking approval defaults |
| **Terminal UX polish** | Copilot CLI (#4313), Pi (#7399), Qwen Code (#8319), OpenCode (#20600) | Scrollable history, hover links, OSC 8 truncation, stable layout, clickable links |

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Notable Approach |
|---|---|---|---|
| **Claude Code** | Multi-session coordination, VS Code integration | Enterprise teams, large codebases | Focus view, hook-based `PreToolUse`, sandbox credential masking; weakest on Windows networking |
| **OpenAI Codex** | Agent pipeline robustness, MCP fidelity | Platform engineers, automation-heavy users | Dual-WebSocket transport, state-DB resume, conformance gates; Windows app stability lagging |
| **Gemini CLI** | Agent trust & correctness | Reliability-sensitive users | Deterministic tool boundaries, AST-aware tooling (proposed), behavioral evals; focus on context integrity |
| **Copilot CLI** | GitHub ecosystem integration | GitHub-centric developers | Plugin auto-update, worktree per task, scheduled prompts; terminal UX behind TUI rivals |
| **Kimi CLI** | Lightweight CLI with web preview | Chinese-language users, Moonshot API | Focus on hook reliability (PostToolUse), ACP protocol correctness; memory feature pending |
| **OpenCode** | Desktop + CLI hybrid | Frontend/web developers | Native desktop app, localhost previews, plugin model; version drift between desktop/CLI |
| **Pi** | Configurable, self-hostable agent | Power users, self-hosters | Harness v2 (modular session storage), engine-specific sampling params, JSON delta-only streaming |
| **Qwen Code** | Provider breadth + cache efficiency | Alibaba Cloud ecosystem, cost-sensitive | Prompt-cache preservation, deferred tool discovery, reasoning effort wire-shape hardening |
| **DeepSeek-TUI** | Fleet (distributed compute) vision | Automation-heavy, multi-model users | 18-crate monorepo converging to one executable; Runtime API for remote clients; ACP rich tool exposure |

## 5. Community Momentum & Maturity

**Most active community:** OpenAI Codex leads on raw engagement (88 comments on #20214, 78👍; 3-model cluster of gpt-5.6-luna with 70+ combined upvotes) and PR velocity (10 PRs in 24h, all merged/closed). Claude Code's discussion depth is unmatched for coordination topics (61-comment issue #24798), but PR velocity is unusually low (2 PRs) and a 12-month macOS ECONNRESET bug (#5674, 52 comments) signals a hardening gap.

**Rapidly iterating:** Gemini CLI (10 PRs, nightly train, heavy P1 fixes), Qwen Code (10 PRs including 2 follow-up hardening patches), and DeepSeek-TUI (30-PR release train with hygiene unblocking) are shipping at the highest velocity. Pi stands out for community-driven redundant fixes (two independent delta-stream PRs landed in one cycle), which is a strong signal of demand-pull and contributor health.

**Maturing communities:** Copilot CLI shows a burst-release pattern (2 releases in 24h) with 0 new PRs—the community is consuming rather than contributing, typical of a stable product. Kimi CLI and OpenCode show steady-paced, reliably-reviewed PR flow.

**Emerging risk:** DeepSeek-TUI's 464 dead-code allowances (#4785) and open questions about architecture convergence (#3306) suggest technical debt may be accumulating under release-train pressure. OpenCode's desktop/CLI version drift (#35122) is an architectural concern that erodes trust in a hybrid product.

## 6. Trend Signals

1. **Session orchestration is the next frontier.** Claude Code's #24798 (61 comments) and #30492 (60👍) represent the strongest collective push for first-party multi-session primitives. Developers are hitting hard limits of siloed sessions on large projects; the current workaround (PreToolUse `deny` hooks) is universally described as insufficient. Expect first-party coordination primitives to become a flagship feature across all major CLIs in the next 6 months.

2. **Cost metering is the #1 trust issue.** A 115-👍 quota-API request (#13585), Codex's weekly-limit drain bug (#33685), Claude's idle token spikes (#65687), and Qwen's cache-invalidation cost concerns (#8452) all point to a systemic problem: users cannot see or predict consumption. Tools that ship clear, CLI-readable quota telemetry with per-request cost breakdowns will win developer trust.

3. **Model-catalog accuracy is a shared pain.** The gpt-5.6-luna rejection (Codex #35097, Copilot CLI #4337) and GPT-5.6 Sol context-cap bug (Codex #31860) reveal that model capability metadata lags actual model capabilities across the ecosystem. Two independent tools hit the same upstream data issue in one cycle. This is an opportunity for a shared model-catalog validation layer.

4. **MCP/ACP conformance is becoming a competitive differentiator.** Codex added MCP conformance gates (#36810), Gemini refreshed OAuth with stored client IDs (#28481), Kimi fixed the empty-question ambiguity (#2507), DeepSeek-TUI exposed real tool execution over ACP (#5225), and Copilot CLI hit registry policy failures (#4346). Each tool independently recognizes that protocol fidelity is table stakes for ecosystem integration—but the absence of shared conformance tooling means each is reinventing the wheel.

5. **Windows/WSL is no longer optional.** Three separate tools (Codex #20214, Pi #7064, DeepSeek-TUI #5095) cite specific Windows failures this cycle, and Pi's maintainer launched a community survey (#7547) to prioritize Windows configurations. The trend is clear: developer workforces are heterogeneous, and CLI tools that treat Windows as second-class will see adoption stall.

6. **Unattended/autonomous operation requires mechanical safety controls.** DeepSeek-TUI's stop-command proposal (#4959), Gemini's permission bypass reports, and Claude's silent Stop-hook failures (#83687) all point to a gap: as agents run longer and more independently, developers need hard kill-switches, deterministic redaction, and fail-closed hooks. This is the trust gap that must close before CLI agents run unattended in production CI/CD pipelines.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

*Data as of 2026-08-04 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

### Most-Discussed Skills (by PR attention)

**1. Self-Audit — Reasoning Quality Gate**  
[PR #1367](https://github.com/anthropics/skills/pull/1367) — *Open*  
A universal audit skill performing mechanical file verification first, then a four-dimension reasoning audit in damage-severity priority order. Works across any project, tech stack, or model. Discussion focused on the phased verification approach (files → reasoning → delivery), with the author positioning it as v1.3.0 of a quality-gate pipeline also proposed in Issue #1385.

**2. Plan-File-Hygiene**  
[PR #1479](https://github.com/anthropics/skills/pull/1479) — *Open*  
Addresses the accumulation of planning artifacts with no lifecycle management. The discussion credits community contributors (@halilxibrahim, @xg-gh-25) who framed the problem as a lifecycle gap. Explicitly built on community framing, showing collaborative skill development.

**3. Color-Expert**  
[PR #1302](https://github.com/anthropics/skills/pull/1302) — *Open*  
A self-contained color-expertise skill covering color naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway), color space selection tables, and gradient construction. Notably broad coverage of classic and modern color systems.

**4. Testing-Patterns**  
[PR #723](https://github.com/anthropics/skills/pull/723) — *Open*  
Comprehensive testing skill covering the full stack: Testing Trophy philosophy, AAA pattern, React component testing with Testing Library, and test-naming conventions. Discussion emphasized what *not* to test — a counterweight to pure coverage metrics.

**5. Pyxel Retro Game Development**  
[PR #525](https://github.com/anthropics/skills/pull/525) — *Open*  
Wraps the pyxel-mcp server for the Pyxel retro game engine. Covers a write → run_and_capture → inspect → iterate workflow for creating retro/pixel-art/8-bit games in Python.

**6. ODT Document Skill**  
[PR #486](https://github.com/anthropics/skills/pull/486) — *Open*  
OpenDocument Text creation, template filling, and ODT→HTML conversion. Triggered by ODT/ODS/ODF/OpenDocument/LibreOffice mentions. Long-lived PR (5+ months) with sustained community interest.

**7. Document Typography**  
[PR #514](https://github.com/anthropics/skills/pull/514) — *Open*  
Typographic quality control for AI-generated documents: orphan word wrap prevention, widow paragraph elimination, and numbering alignment. Directly addresses a visible AI-generation quality gap.

**8. Frontend-Design Clarity Overhaul**  
[PR #210](https://github.com/anthropics/skills/pull/210) — *Open*  
Revises the frontend-design skill to improve actionability and ensure every instruction is followable within a single conversation. Focused on specificity over generality.

---

## 2. Community Demand Trends

**Priority: Skill-Creator Reliability (Blocking)**  
The dominant issue cluster centers on `skill-creator` infrastructure bugs (Issues #556, #1169, #1061, #202). The `run_eval.py` recall=0% bug is reproduced by 10+ independent users and makes description-optimization loops optimize against noise. This is a **meta-demand**: the community needs working tooling *before* new skills matter.

**Security & Trust Boundary**  
Issue #492 (43 comments) flags community skills distributed under the `anthropic/` namespace creating trust-boundary abuse. This is the most-commented issue and signals demand for **skills provenance and security verification**.

**Organizational Sharing**  
Issue #228 (16 comments, 8 👍) demands org-wide skill sharing in Claude.ai — removing the manual download/upload flow via Slack/Teams.

**Performance & Context Awareness**  
Issue #1487 surfaces the `claude-api` skill injecting ~156k tokens in a single tool call. Community is sensitive to skills that waste context windows.

**New Skill Directions (from proposals):**
- **Agent governance** — safety patterns for AI agent systems (Issue #412)
- **Compact-memory** — symbolic notation for compact agent state (Issue #1329)
- **Quality gates** — pre-task calibration → adversarial review → delivery verification (Issue #1385)

---

## 3. High-Potential Pending Skills

These PRs have active discussion and may land soon:

| Skill | PR | Description | Status |
|-------|-----|-------------|--------|
| **Self-Audit v1.3.0** | [#1367](https://github.com/anthropics/skills/pull/1367) | Mechanical verification + 4-dimension reasoning gate | Open, recent activity (Jul 2) |
| **Plan-File-Hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Lifecycle management for planning artifacts | Open, recent (Jul 27) |
| **Color-Expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Comprehensive color knowledge | Open, updated Jul 21 |
| **Testing-Patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Full-stack testing guidance | Open, updated Apr 21 |
| **Document Typography** | [#514](https://github.com/anthropics/skills/pull/514) | Typographic QC for generated docs | Open, updated Mar 13 |
| **Skill-Quality/Security Analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Meta-skills evaluating other skills | Open, updated Jan 7 |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is not for new skill domains but for making the existing skill pipeline trustworthy — fixing the skill-creator's broken evaluation loop and establishing clear provenance so community-contributed skills can be adopted without security or quality anxiety.**

---

### Methodology Note
"Comments" data for PRs was undefined in the source feed; ranking uses issue comment counts, PR discussion context, and update recency as proxies for attention. All 50 PRs and 50 issues from the feed were reviewed.

---

# Claude Code Community Digest — 2026-08-04

## Today's Highlights
Version **2.1.221** shipped with a notable UX improvement: a new **Focus view** in VS Code that collapses tool activity into per-turn summaries with a live running-tool indicator, plus `mode: "mask"` for sandbox credential files on Linux. Community attention remains concentrated on **multi-session coordination** (two distinct issues with 61 and 9 comments, plus a related feature request), and a **long-running macOS ECONNRESET bug** (#5674) that continues to draw 52 comments. A concerning **GitHub connector regression** (#71542) — where content access fails for all repos after successful OAuth — is the most commented new bug, flagged as account-wide.

## Releases

### v2.1.221
- **[VSCode] Focus view:** New chat-menu toggle that hides tool activity behind an expandable per-turn summary with a live running-tool indicator. Toggle with `Ctrl+Alt+F` or the "Claude Code: Toggle Focus view" command.
- **Sandbox on Linux:** Added `mode: "mask"` for sandbox credential files.

## Hot Issues

1. **[#24798 — Inter-session communication for multi-Claude workflows](https://github.com/anthropics/claude-code/issues/24798)** — *61 comments, 20 👍*
   The most-discussed open enhancement. Users running parallel sessions on large projects want a first-party way to sequence dependent work across silos. Community is actively proposing coordination primitives.

2. **[#5674 — Persistent ECONNRESET Errors on macOS](https://github.com/anthropics/claude-code/issues/5674)** — *52 comments, 48 👍*
   A 12-month-old bug with high engagement. macOS users experience connection drops that break long tasks, while Windows/Linux on the same network work fine. Remains unfixed despite repro available.

3. **[#71542 — GitHub connector cannot access content for ANY repo (account-wide regression)](https://github.com/anthropics/claude-code/issues/71542)** — *48 comments, 42 👍*
   OAuth links succeed, but Claude cannot read any repository content — public or private. Flagged as a recent regression affecting all repos. Many users confirming; high urgency.

4. **[#30492 — Real-time steering: priority message channel for mid-execution redirect](https://github.com/anthropics/claude-code/issues/30492)** — *31 comments, 60 👍*
   Request to interrupt/redirect Claude during long multi-step tasks via a priority channel. Strong upvote ratio indicates broad demand for mid-flight control.

5. **[#13585 — Add Quota Information Access to CLI](https://github.com/anthropics/claude-code/issues/13585)** — *24 comments, 115 👍*
   Highest 👍 count this week. Users want to view usage/quota from the CLI without needing `user:profile` scope. Repeated requests suggest cost visibility is a top concern.

6. **[#80468 — Claude Desktop crashing on Windows after latest update](https://github.com/anthropics/claude-code/issues/80468)** — *12 comments*
   New regression report. Desktop app crashes post-update on Windows; no workaround yet. High impact for desktop users.

7. **[#65687 — Unexpected token usage spike while inactive (Windows)](https://github.com/anthropics/claude-code/issues/65687)** — *10 comments*
   Users report token consumption continuing even when Claude Code is idle. Cost-related and tied to the broader quota-visibility demand.

8. **[#76727 — Cross-session coordination for independently-launched sessions](https://github.com/anthropics/claude-code/issues/76727)** — *9 comments*
   Companion to #24798. Notes that the only current primitive (PreToolUse `deny` hook) has "silent holes" and is a DIY kit — not a coordination story.

9. **[#41743 — App refuses to start: "another instance is running" (stale)](https://github.com/anthropics/claude-code/issues/41743)** — *9 comments, closed as stale*
   Users hit a phantom lock after updates; no process visible. Closed as stale but still relevant to Windows desktop reliability.

10. **[#82536 — `--continue` cannot find sessions created by `-p`](https://github.com/anthropics/claude-code/issues/82536)** — *5 comments*
    Interactive resume fails for sessions started in print mode. A workflow-breaking bug for scripted → interactive transitions.

## Key PR Progress
*Note: only 2 PRs updated in the last 24h; listing both plus pointing to broader activity.*

1. **[#83374 — docs(plugin-dev): document MessageDisplay streaming semantics](https://github.com/anthropics/claude-code/pull/83374)** — Open, by iCodeCraft
   Documents the `MessageDisplay` hook event, which is currently missing from the bundled plugin-development skill's trigger description, event guidance, and quick-reference table.

2. **[#77977 — docs(plugin-dev): document skipLfs marketplace sources](https://github.com/anthropics/claude-code/pull/77977)** — Open, by superdiaodiao
   Documents the `skipLfs` option for `github` and `git` marketplace sources, with examples for GitHub shorthand and generic Git URLs. Refs #63035.

*PR volume is unusually low today (2 items). Historically, this project sees 5–15 PRs/day; the digest sample may be incomplete.* Other recently merged/active PRs this week include: (a) a Focus view implementation for VS Code (merged in v2.1.221), (b) sandbox `mode: "mask"` support for Linux (merged in v2.1.221), and (c) ongoing work in the hook-documentation area.

## Feature Request Trends

1. **Inter-session / multi-agent coordination (dominant theme)**
   - #24798 (direct project workflow between sessions)
   - #76727 (cross-session coordination with shared working tree)
   - #30492 (real-time steering via priority channel)
   These three collectively represent the strongest push: users need **first-party primitives** to orchestrate multiple Claude Code sessions working on one codebase.

2. **Cost & quota visibility**
   - #13585 (CLI quota information, 115 👍)
   - #65687 (token spike while idle — bug, but reflects cost anxiety)
   - #81015 (read-only usage scope for setup-token)
   Clear demand for **transparent token/usage metering** inside the CLI and API tokens.

3. **Cross-platform reliability (particularly Windows & macOS networking)**
   - #5674 (macOS ECONNRESET)
   - #77733 (ECONNRESET in Desktop in-app CLI)
   - #83656 (unsigned binary on macOS causing exit 127)
   Recurring theme: **network resilience** on macOS and **binary signing/distribution** issues.

4. **Model selection and access control**
   - #83683 (restore access to claude-opus-4 variant)
   - #81317 (per-plan enablement of Microsoft 365 write tools)
   Users want **finer control** over which models are available per plan.

5. **Hooks reliability**
   - #83687 (Stop hook verdict silently discarded)
   - #82323 (PreToolUse hook inert with no signal)
   Hook-related issues keep surfacing — a sign of **growing hook adoption** with **fragile failure modes**.

## Developer Pain Points

- **Siloed sessions are a real bottleneck.** Two separate issues (#24798, #76727) describe the same core problem: users cannot reliably sequence work across parallel Claude Code sessions. The workaround (PreToolUse `deny` hooks) is described as "a build-it-yourself kit" with "silent holes." This is the single most-requested capability this week.

- **Costs are opaque and occasionally surprising.** Between the 115-👍 quota-API request (#13585), a report of token usage while idle (#65687), and OAuth scope failures blocking usage reads (#81015), developers feel they cannot **see or control** what they're spending.

- **Authentication and integration regressions are painful.** The GitHub connector regression (#71542) — account-wide content access failure after successful OAuth — is a **blocker for everyday work**. A second issue (#80874) reports GitHub write operations failing with "403 Resource not accessible by integration." Users are hitting a wall on a core workflow.

- **macOS networking instability persists.** The 12-month-old ECONNRESET issue (#5674) has 52 comments and 48 👍. It's reproducible, but unfixed. The in-app Desktop variant (#77733) is also reported. This is a **chronic reliability gap** on a primary development platform.

- **Session management is fragile.** `--continue` can't find print-mode sessions (#82536), named/teammate agents hang when tmux pane creation fails (#83366), and mobile attach breaks after token rotation (#83677). Developers are bumping into **state-management bugs** across session types.

- **Hooks fail silently.** Both #83687 and #82323 describe hooks that **don't run and don't log anything** — a missing script fails open, a matcher is never registered, an exit-2 verdict is discarded. For a safety-critical feature like Stop/PreToolUse hooks, silent failure is a **trust problem**.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-04

## Today's Highlights

Windows stability remains the dominant theme this week, with high-engagement issues around UI freezes (#20214), OneDrive-backed workspace stream disconnects (#35420), and WSL integration regressions (#35119). A notable cluster of reports around `gpt-5.6-luna` being rejected by `spawn_agent` in MultiAgent V2 (#35097, #34700, #34964) has drawn over 70 combined upvotes, signaling a widely-felt blocker. On the engineering side, a fast-moving series of infrastructure PRs (dual-WebSocket transport, MCP conformance gates, Git process-tree cleanup) suggests active hardening of the core platform.

---

## Releases

Two pre-release versions were published in the last 24 hours:

- **[rust-v0.147.0-alpha.6](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.6)** — Pre-release build
- **[rust-v0.147.0-alpha.1.2](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.1.2)** — Pre-release build

No detailed changelog notes were provided for either release.

---

## Hot Issues

1. **[#20214 — Codex App freezes/stutters on Windows 11 Pro](https://github.com/openai/codex/issues/20214)** — 88 comments, 78 👍
   The top community issue this digest cycle. Users report UI freezing despite 32GB RAM and a capable CPU. Widespread agreement suggests this is a systemic Windows client issue, not user-specific. Notably, it's been open for 3 months — a key indicator of Windows desktop maturity.

2. **[#35420 — OneDrive-backed workspace breaks streams](https://github.com/openai/codex/issues/35420)** — 30 comments
   Work/Codex streams fail with "stream disconnected before completion" when the workspace is OneDrive-backed and OneDrive is degraded. New issue (8 days old) but already hot — likely affects enterprise users frequently.

3. **[#33685 — Weekly limit drains like the old 5-hour limit](https://github.com/openai/codex/issues/33685)** — 25 comments, 10 👍
   Users report the weekly rate limit burns down at nearly the same pace as the old 5-hour limit, despite no usage change. Community suspects that the quota metering is misaligned with the actual model consumption. Potential billing/quota bug.

4. **[#19504 — Full RTL support for Arabic & Hebrew](https://github.com/openai/codex/issues/19504)** — 24 comments, 19 👍
   Community continues to advocate for proper RTL rendering in both Codex and Chat panels. This is a long-standing papercut (open since April) with steady organic support — signals the criticality of localization.

5. **[#35097 — gpt-5.6-luna rejected by MultiAgent V2 spawn_agent](https://github.com/openai/codex/issues/35097)** — 14 comments, 37 👍
   High-visibility bug: `gpt-5.6-luna` is marked as MultiAgent V1, so V2's `spawn_agent` rejects it. Workarounds require downgrading agent architecture or model selection trickery. Upvoted strongly — this reflects a broader pattern of capability-gated model misuse.

6. **[#31860 — GPT-5.6 Sol context capped at 372K vs 1.05M spec](https://github.com/openai/codex/issues/31860)** — 14 comments, 26 👍
   Critical catalog-bug: GPT-5.6 Sol's context window is incorrectly capped to ~350K effective by the model catalog, forcing users to lose context on long agentic runs. Demands urgent attention from the core team.

7. **[#12029 — Multi-account support for Codex surfaces](https://github.com/openai/codex/issues/12029)** — 12 comments, 62 👍
   One of the highest-voted enhancement requests overall (62 👍). Users need separate personal/corporate accounts; the current single-auth model is a blocker for enterprise adoption.

8. **[#35119 — WSL repos marked as "non-Git"](https://github.com/openai/codex/issues/35119)** — 14 comments, 13 👍
   Latest app release (26.721.3404) incorrectly classifies valid WSL repositories as non-Git and disables Git operations. Regressed from previous working version — strong signal of a Windows/WSL detection regression.

9. **[#34700 — Luna model rejection in Codex App](https://github.com/openai/codex/issues/34700)** — 9 comments, 24 👍
   Windows-spec variant of the `spawn_agent`/`gpt-5.6-luna` mismatch. Combined with #35097, this highlights a cross-surface capability bug.

10. **[#15477 — Silent fail + dashboard quota mismatch](https://github.com/openai/codex/issues/15477)** — 11 comments, 6 👍
    Auto code review silently fails in Codex Cloud: dashboard shows quota, but review reports "limit reached." Three bugs in one report — stale GitHub commit handling, silent failure, and quota inconsistency.

---

## Key PR Progress

1. **[#36815 — Identify agents by name in token budget context](https://github.com/openai/codex/pull/36815)** — **Closed**
   Replaces thread IDs with canonical agent paths (`/root`, subagent paths) in `<context_window>` metadata for clearer token accounting.

2. **[#36812 — Dual-WebSocket transport for code mode](https://github.com/openai/codex/pull/36812)** — **Closed**
   Adds optional `dual-websocket-v1` capability to prevent large tool callbacks from blocking session operations on a single connection. Significant architectural improvement for concurrency.

3. **[#36809 — Prefer state DB for `exec resume --last`](https://github.com/openai/codex/pull/36809)** — **Closed**
   `exec resume --last` now queries the SQLite state DB first instead of auditing all rollout files — a performance and correctness improvement for session resume.

4. **[#36810 — MCP conformance regression gates](https://github.com/openai/codex/pull/36810)** — **Closed**
   Adds a harness that runs Codex against the official MCP client conformance suite (HTTP/stdio, OAuth). Strong signal that MCP compatibility is now a first-class support surface.

5. **[#36793 — Terminate timed-out Git process trees](https://github.com/openai/codex/pull/36793)** — **Closed**
   Git metadata commands now run in process groups (Unix) and Job Objects (Windows) to prevent orphaned helpers after timeout — addresses a class of hanging-process bugs.

6. **[#36781 — Per-surface MCP tool exposure controls](https://github.com/openai/codex/pull/36781)** — **Closed**
   Introduces `omit_tools_from` to allow MCP servers to opt out of individual surfaces (direct exposure, tool search, code mode) without disabling worldwide.

7. **[#36772 — Raise host-owned Codex Apps catalog limit](https://github.com/openai/codex/pull/36772)** — **Closed**
   Raises the catalog limit from 2,048 to 8,192 for host-owned `codex_apps` registrations, while keeping the standard MCP limit intact. Unblocks large tool catalogs.

8. **[#36811 — Honor per-environment login shell policy](https://github.com/openai/codex/pull/36811)** — **Closed**
   Stores the effective `allow_login_shell` setting per turn environment and exposes the `login` argument for shell tools when permitted — improves environment-specific shell handling.

9. **[#36792 — Gate plugin usage instructions by model capability](https://github.com/openai/codex/pull/36792)** — **Closed**
   Adds `include_plugin_usage_instructions` to model metadata (defaults false) — prevents earlier models from receiving plugin guidance not applicable to their capabilities.

10. **[#36807 — Extract audio preparation into utility crate](https://github.com/openai/codex/pull/36807)** — **Closed**
    New `codex-utils-audio` workspace crate for canonicalizing audio inputs and estimating token usage — a sign of modularization preceding broader audio/model support.

---

## Feature Request Trends

- **Multi-account / auth separation** — Repeated asks for personal + corporate accounts across all surfaces (#12029). This is a top-tier enterprise adoption blocker. (62 👍)

- **RTL text support (Arabic/Hebrew)** — Not a new request but widely echoed in #19504 (19 👍), emphasizing the localization gap in current app UI.

- **Event-driven monitoring tool** — A single issue (#29922) requests an agent-callable `monitor` tool to wake Codex on background events (logs, files, builds, CI) without polling. This would unlock greater autonomous operation.

- **Model capability transparency** — Several requests implied in bugs (#35097, #31860): users want catalog data that truly matches model specs (context size, MultiAgent version) to avoid misconfiguration.

- **Per-environment/per-session sandbox and permission recovery** — Users want persistent Full Access sessions and approval-mode recovery after restart (#34453), plus granular shell policy per environment (PR #36811).

---

## Developer Pain Points

- **Windows app instability** — Freezes, stutters, approval-button unresponsiveness, OneDrive disconnects, and WSL integration regressions dominate this digest (#20214, #35420, #35119, #30529). Windows users are clearly the most affected cohort, and recent releases have introduced at least one new regression.

- **spawn_agent model compatibility gaps** — The gpt-5.6-luna rejection across CLI and App surfaces (#35097, #34700, #34964) is confusing for developers building agent pipelines, since the model appears selectable in one surface but fails in another.

- **Quota/rate-limit metering inconsistency** — Users see confusing quota behavior: weekly limits draining like 5-hour limits (#33685), silent failures despite dashboard showing quota (#15477), and disappearing 5-hour limits (#32791). This erodes trust and makes cost forecasting impossible.

- **Session state corruption / context leaks** — Reports of concurrent sessions leaking workspace roots (#24224) and `exec resume` appending to Desktop transcripts without updating indexes (#28259) point to underlying state-management debt.

- **WSL-specific workflow breaks** — Clipboard screenshots unavailable (#30529), sandboxCwd resolution issues with Browser Use (#29639), and non-Git misclassification (#35119) make WSL workflows feel second-class despite being a primary dev environment for Windows users.

- **MCP & auth configuration rough edges** — OAuth refresh omitting the RFC 8707 resource parameter (#33403) and per-surface tool controls (PR #36781) indicate MCP tooling is still early-stage and requires hardening for production use.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-04

## Today's Highlights

The community remains highly focused on agent reliability and safety, with recurring reports of subagent hangs, false "success" reporting, and permission bypasses. A notable cluster of PRs targets hardening context integrity around compression, quota fallback, and malformed tool arguments, signaling a push toward production-grade stability. Several contributors are also improving MCP security and extension resilience against malformed API responses.

---

## Releases

- **v0.55.0-nightly.20260803.gf47d6c6f7** — Nightly release published. No standalone changelog beyond the commit diff. [Compare v0.55.0-nightly.20260802...v0.55.0-nightly.20260803](https://github.com/google-gemini/gemini-cli/compare/v0.55.0-nightly.20260802.gf47d6c6f7...v0.55.0-nightly.20260803.gf47d6c6f7)

---

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** · P1 · *12 comments, 2 👍*  
   Critical correctness bug: subagents hitting turn limits report "success"/"GOAL" with zero analysis performed, misleading the parent agent. Community concerned about false-positive task completion.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** · P1 · *8 comments, 8 👍*  
   Highest-reacted issue this week. Deferring to the generalist agent causes indefinite hangs (users waited up to an hour). Workaround: instructing the model to avoid subagents. Clear agent-routing reliability problem.

3. **[#19873 — Leverage model's bash affinity via OS sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** · P2 · *8 comments, 1 👍*  
   Feature proposal arguing Gemini 3 models are native POSIX users; asks for zero-dependency sandboxing while enabling native `grep`/`sed`/`awk` workflows. Active design discussion.

4. **[#24353 — Robust component-level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** · P1 · *7 comments*  
   Epic tracking expansion of behavioral evals (currently 76 tests across 6 model configs). Recognized as essential for catching regressions like the agent-hang issues above.

5. **[#22745 — AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** · P2 · *7 comments, 1 👍*  
   Investigation epic for AST-aware tooling: precise method-bound reads (fewer turns, less noise), smarter codebase navigation. High potential for token-cost reduction.

6. **[#21968 — Gemini doesn't use skills and sub-agents proactively](https://github.com/google-gemini/gemini-cli/issues/21968)** · P2 · *6 comments*  
   Anecdotal but widely echoed: models require explicit instruction to use custom skills. Undermines the value of customizing the agent.

7. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** · P1 · *4 comments, 3 👍*  
   High-frustration UX bug: simple, non-interactive commands remain in "awaiting input" state, blocking the session. Occurs repeatedly for basic commands.

8. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** · P2 · *5 comments*  
   Auto Memory marks sessions as "unprocessed" when skipped, causing them to resurface repeatedly. Inefficient and annoying for long-running sessions.

9. **[#25166 — Shell command execution stuck](https://github.com/google-gemini/gemini-cli/issues/25166)** · P1 · *4 comments, 3 👍*  
   Repeatedly reproduces: after a simple CLI command completes, the shell remains active with "Awaiting user input." Core UX blocker for scripted workflows.

10. **[#26525 — Deterministic redaction for Auto Memory](https://github.com/google-gemini/gemini-cli/issues/26525)** · P2 · *4 comments*  
    Security concern: secrets reach model context before prompt-based redaction, and logs may expose skill content. Community recognizes the risk in memory features.

---

## Key PR Progress

1. **[#28657 — Prevent malformed GitHub JSON from crashing extensions](https://github.com/google-gemini/gemini-cli/pull/28657)** · P2, `area/extensions`  
   Adds error handling around `JSON.parse()` in `fetchJson()` to prevent uncaught exceptions from corrupting extension operations.

2. **[#28663 — Harden fetchJson against malformed JSON and stream failures](https://github.com/google-gemini/gemini-cli/pull/28663)** · P2, `area/extensions`  
   Similar hardening for GitHub fetch; rejects the promise instead of leaking uncaught exceptions. Two parallel PRs addressing the same bug (#28646) — worth watching for overlap.

3. **[#28673 — Add Gemini 3.6 Flash and 3.5 Flash-Lite model configs](https://github.com/google-gemini/gemini-cli/pull/28673)** · P2, `area/core`  
   New model support with capabilities (`thinking`, `multimodalToolUse`) and Code Execution configs. Enables faster/cheaper Flash-tier options.

4. **[#28671 — Resolve context corruption and quota error fallback issues](https://github.com/google-gemini/gemini-cli/pull/28671)**  
   Defensive history hardening for interrupted tool executions; addresses model "autocomplete" prefix-continuation corruption after ESC or quota falls.

5. **[#28672 — Repair /compress session reload and quota-fallback tool response loss](https://github.com/google-gemini/gemini-cli/pull/28672)**  
   Two independent fixes for session corruption: `/compress` reload throws, and tool responses lost during quota fallback. Directly addresses reported context bugs.

6. **[#28670 — Correct model fallback on capacity errors for GCA agent mode](https://github.com/google-gemini/gemini-cli/pull/28670)**  
   Fixes infinite retry loop on `MODEL_CAPACITY_EXHAUSTED`/429 by falling back to available models (e.g., Flash). Critical for reliability under load.

7. **[#28481 — Refresh MCP OAuth tokens with the stored client ID](https://github.com/google-gemini/gemini-cli/pull/28481)** · P1, `area/security`  
   Fixes token refresh failure that deletes stored credentials, forcing re-auth every session. Important security/UX fix for OAuth-based MCP servers.

8. **[#28660 — Keep sendStream alive on malformed tool arguments](https://github.com/google-gemini/gemini-cli/pull/28660)**  
   Defensive parsing of SDK tool arguments so invalid JSON becomes structured `functionResponse` errors instead of crashing the stream. Improves SDK robustness.

9. **[#28664 — Reflect full server config in consent and harden stdio env](https://github.com/google-gemini/gemini-cli/pull/28664)**  
   Consent prompts previously omitted `env`, `cwd`, and `headers` — now shown and compared before re-prompting. Security improvement for MCP server updates.

10. **[#28586 — Preserve thoughtSignature in functionCall parts to fix 400](https://github.com/google-gemini/gemini-cli/pull/28586)** · P2, `area/agent`  
    Fixes a regression from v0.53.0 causing 400 Bad Request on parallel tool calls by preserving `thoughtSignature`. In-flight community contribution.

---

## Feature Request Trends

- **Agent reliability & observability**: Highest demand for subagent trajectory visibility (via `/chat share`), bug reports that include subagent context, and behavioral evals that catch regressions before they ship.
- **AST-aware tooling**: Strong interest in reducing token overhead and turn count via precise code navigation — active epic with concrete tool proposals (`tilth`, `glyph`).
- **Proactive tool adoption**: Users want the model to autonomously use custom skills/subagents based on context, not just when explicitly instructed.
- **Security hardening**: Calls for deterministic secret redaction before content enters model context and better consent/visibility for MCP server configurations.
- **Sandboxing without overhead**: Desire for zero-dependency OS sandboxing that lets models use native POSIX tools without compromising user safety.

---

## Developer Pain Points

- **False "success" reporting**: Subagents hitting `MAX_TURNS` report GOAL success, masking incomplete work — erodes trust in agent results.
- **Hangs & stalls**: Generalist agent hangs, shell commands stuck on "Waiting input," and interactive-prompt deadlocks are recurring, high-frustration issues.
- **Context corruption**: Compression failures, quota-fallback data loss, and `thoughtSignature` stripping in parallel calls — multiple PRs in flight to address.
- **Permission & control**: Subagents running despite disabled config (since v0.33.0); users want explicit opt-in control restored.
- **Memory system transparency**: Low-signal sessions retried indefinitely; secrets sent to model context before redaction; unclear what is persisted and logged.
- **Tool-scope management**: >128 tools trigger 400 errors; models litter temp scripts across directories; destructive commands (`git reset`, `--force`) used when safer options exist.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-04

## Today's Highlights

Two releases shipped yesterday: **v1.0.78** brings a polished UX upgrade with live timing headers that show tool call durations (right-aligned, ticking in real-time), alongside automatic updates for first-party plugins. **v1.0.78-3** introduces an experimental `/new-worktree` command for creating isolated worktrees with fresh conversations, plus a fix that defaults Copilot login to the browser flow for local desktop. Community attention is focused on long-standing gaps: project-scoped plugins (#1665), multi-model BYOK support (#3282), and per-session model switching (#3709) remain the most active and most-upvoted issues.

## Releases

### v1.0.78 (2026-08-03)
- **New:** Timeline headers now display tool call durations, right-aligned, ticking live while the call runs (for calls ≥ 5 seconds). On by default — disable via `/settings showToolDurations`.
- **Improved:** First-party plugins automatically update to the latest version at session start.
- **Improvement in progress:** Release notes truncated ("Add the ex…").

### v1.0.78-3 (2026-08-03)
- **Added:** Experimental `/new-worktree` command — creates a new worktree and starts a fresh conversation within it.
- **Improved:** Interactive shell shortcut now launches on Enter, with an inline hint shown when "$" is armed.
- **Fixed:** Copilot login now defaults to browser flow for local desktop.

---

## Hot Issues

1. **[#1665 — Support Copilot CLI Plugins Scoped to Project or Repository](https://github.com/github/copilot-cli/issues/1665)** — *[CLOSED]* · 14 comments · 👍 18  
   The community is pushing hard for repo-scoped plugins; global-only installation forces users to load irrelevant plugins and blocks team-shared tooling. This issue was closed, but 18 upvotes suggest the conversation will continue.

2. **[#3282 — Add multiple BYOK model capability](https://github.com/github/copilot-cli/issues/3282)** — *[OPEN]* · 7 comments · 👍 20  
   Currently locked to a single BYOK model via env var; switching models requires terminating the session. The 20 upvotes signal strong demand for multi-provider configurations.

3. **[#3709 — Allow /model to switch between multiple models, including BYOK/local providers](https://github.com/github/copilot-cli/issues/3709)** — *[OPEN]* · 3 comments · 👍 20  
   Directly related to #3282 — `/model` only lists GitHub-hosted models, ignoring configured local/BYOK providers. Highest-demand feature area this week.

4. **[#4078 — Scheduled prompts kill the existing prompt queue](https://github.com/github/copilot-cli/issues/4078)** — *[CLOSED]* · 5 comments · 👍 0  
   `/every` or `/after` scheduled prompts interrupt queued items and never resume the queue. Closed, but a significant workflow issues for automation-heavy users.

5. **[#4313 — Allow scrolling through the current conversation history](https://github.com/github/copilot-cli/issues/4313)** — *[OPEN]* · 3 comments  
   Mouse wheel and PageUp/PageDown don't scroll conversation history — a basic terminal-UX expectation missing from the TUI.

6. **[#4337 — gpt-5.6-luna advertised but not accessible via /chat/completions](https://github.com/github/copilot-cli/issues/4337)** — *[CLOSED]* · 2 comments  
   Model advertised in `/models` but fails on the OpenAI-compatible surface; only works via `/responses`. Breaks MoA/aggregator tooling that relies on chat completions.

7. **[#4328 — Ctrl+H misinterpreted as Ctrl+Backspace under WSL2](https://github.com/github/copilot-cli/issues/4328)** — *[OPEN]* · 2 comments  
   WT_SESSION leak from Windows Terminal causes keybinding misbehavior — a classic cross-platform terminal pain point.

8. **[#2714 — Allow toggling plugins enabled/disabled](https://github.com/github/copilot-cli/issues/2714)** — *[OPEN]* · 2 comments · 👍 11  
   Competitors (Gemini CLI, Claude Code) support plugin toggling; Copilot CLI forces full uninstall/reinstall. High demand for basic plugin lifecycle management.

9. **[#4334 — Stashed (ctrl+S) prompt discarded on session switch](https://github.com/github/copilot-cli/issues/4334)** — *[OPEN]* · 0 comments  
   Typed-but-unsubmitted prompts stashed with `ctrl+s` are lost when switching sessions; pop restores nothing. Data-loss bug in an existing feature.

10. **[#4345 — Reasoning effort 'medium' not supported for claude-haiku-4.5](https://github.com/github/copilot-cli/issues/4345)** — *[OPEN]* · 0 comments  
    Feature flags `copilot_cli_opus_medium_effort_default` + `copilot_cli_gpt_5_4_mini_for_explore` together trigger repeated sub-agent errors. Configuration compatibility bug.

---

## Key PR Progress

No pull requests were updated in the last 24h (0 items reported). Community activity is currently focused on issue triage and release stabilization.

---

## Feature Request Trends

1. **Model flexibility is the #1 ask.** Multiple issues (#3282, #3709) request BYOK multi-model support and full `/model` switching including local providers. Users want to hot-swap models mid-session without restarting.

2. **Project/team-scoped configuration.** #1665 (project-scoped plugins) and #4298 (sandbox config for selective tool enabling) indicate demand for per-repo tooling control, enabling team-shared configuration and security policies.

3. **Plugin lifecycle management.** #2714 (toggle plugins) and #2286 (Windows symlink support) show plugins are a core workflow, but management is still rough around the edges.

4. **Terminal UX polish.** Repeated requests for conversation scrolling (#4313), wrapped-URL hyperlinking (#4348), and OSC 9;4 progress bar opt-out (#4352) — the TUI is powerful, but fine-grained terminal control is missing.

5. **Session and context resilience.** #4334 (stash loss), #4351 (compaction cost loss), and #4340 (resume model/context mismatch) point to reliability concerns in session-heavy workflows.

---

## Developer Pain Points

- **Windows/WSL2 terminal quirks** — keybinding misinterpretations (#4328), escape-sequence prefill (#4267), and git symlink issues with plugin installs (#2286) make Windows a second-class experience.
- **BYOK/provider configuration friction** — single-model lock-in (#3282), missing local models in `/model` (#3709), and unreasonable default reasoning settings (#4345) force painful restarts.
- **Tools that promise more than they deliver** — gpt-5.6-luna advertised but unusable via chat completions (#4337); feature flags that activate unsupported combinations (#4345). Both erode trust in the model catalog.
- **Silent data loss** — stashed prompts vanishing on session switch (#4334), prompt queue death on scheduled prompts (#4078), and compaction cost accounting loss (#4351). These are the kinds of bugs that make users lose work or trust.
- **Wrapping/hyperlink rendering** — long-URL hyperlinks break on line wrap (#4348) and streaming Markdown links reflow tables (#4347) — visual noise that interrupts focused terminal work.
- **Enterprise/CI policy friction** — managed-settings validation rejects valid enum values (#4349) and MCP registry policy fetches fail with `GITHUB_TOKEN` in CI (#4346), blocking non-default MCP servers in Actions workflows.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-04

## Today's Highlights
The project is in a quiet consolidation phase with no new releases in the last 24 hours, but the PR queue shows steady bug-fixing momentum—notably around hook reliability, shell process handling, and ACP protocol correctness. The most significant community attention remains on the long-pending **Memory System** feature request (#1283), which has accumulated 15 comments and spans back months. Two new bugs surfaced around streaming hangs and Web UI session-switching, each with minimal community engagement so far.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

1. **#1283 — [enhancement] Memory System: Persistent context across sessions**  
   *Author: CatKang | Comments: 15 | [Link](https://github.com/MoonshotAI/kimi-cli/issues/1283)*  
   The most requested feature in the project: cross-session memory with both AI-managed notes and user-defined instructions. This has been open since February with sustained community discussion—a clear signal that users want Kimi to "remember" project patterns and preferences. Its age and lack of maintainer response is becoming a pain point.

2. **#2582 — [bug] CLI stream hangs indefinitely during generation, session becomes unusable**  
   *Author: bobtu56 | Comments: 0 | [Link](https://github.com/MoonshotAI/kimi-cli/issues/2582)*  
   Fatal UX issue: on Windows with Moonshot Platform API (`kimi-k2.7-code`), the CLI hangs mid-generation and the session is irrecoverable. No workaround documented. Notably the reporter is on **0.31.1**, a significantly older version, which may complicate diagnosis.

3. **#2573 — [bug] Web UI "Connecting to session..." infinite spinner when switching sessions**  
   *Author: belenov-maker | Comments: 1 | [Link](https://github.com/MoonshotAI/kimi-cli/issues/2573)*  
   Encountered in the Technical Preview `kimi web` on Chrome/macOS 26.4. The session list is rendered but switching never connects. For a feature still in preview, stability issues like this will erode confidence.

---

## Key PR Progress

1. **#2581 — chore(release): bump kosong to 0.56.0** *(CLOSED)* — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2581)  
   Routine dependency release; merged to move kosong forward with 0.56.0, updating release notes and dependency pins.

2. **#2580 — fix(kosong): omit empty anthropic-beta header when no beta features declared** *(CLOSED)* — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2580)  
   Verifies the Anthropic provider no longer sends an empty `anthropic-beta` header. Small but correct—avoids confusion with third-party proxies.

3. **#2577 — fix(web,vis): do not crash printing startup banner on legacy console codecs** *(OPEN)* — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2577)  
   Fixes a crash on GBK consoles (e.g., Chinese Windows) where U+279C fails to encode. Important for a tool with a strong Chinese-language user base.

4. **#2575 — fix(hooks): fire PostToolUse hooks through fire_and_forget_trigger** *(OPEN)* — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2575)  
   Fixes dropped `asyncio.create_task` handles in `PostToolUse`/`PostToolUseFailure` hooks, which caused silently skipped hooks. Reliability fix for a core extension mechanism.

5. **#2554 — fix(tools): count StrReplaceFile replacements against running content** *(OPEN)* — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2554)  
   Correctness fix: the success message counted replacements against the original file instead of the growing content. Small but prevents misleading output.

6. **#2530 — fix(shell): stop blocking until timeout when a detached child holds the pipes** *(OPEN)* — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2530)  
   Fixes hang when a command like `daemon & echo done` leaves a child holding stdout/stderr, making `asyncio.wait_for` block until timeout. Significant for automation.

7. **#2507 — fix(acp): signal QuestionNotSupported instead of resolving empty answers** *(OPEN)* — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2507)  
   Previously every `QuestionRequest` in ACP server mode returned an empty dict, indistinguishable from user dismissal. Now properly signals unsupported questions—fixes a real protocol ambiguity.

8. **#2535 — fix(llm): scope prompt cache keys to Moonshot APIs** *(OPEN)* — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2535)  
   Third-party Kimi-compatible endpoints will no longer receive Moonshot's `prompt_cache_key` param. Good hygiene for compatibility with non-Moonshot backends. Addresses a real interoperability gap.

---

## Feature Request Trends
- **Persistent Memory System (#1283):** Clearly the highest-demand feature, with sustained interest from the community, covering automatic AI-managed notes as well as manual user instructions that persist across sessions.
- **Interoperability with third-party endpoints (e.g., #2535, #2580):** Users and contributors are pushing to ensure Kimi works cleanly with non-Moonshot backends—prompt-cache keys, vacant headers, and ACP protocol semantics. The PR activity suggests this is a growing priority.
- **Web UI maturation (e.g., #2573):** The `kimi web` Technical Preview is being treated as a real product by users; expected stability and feature parity with the CLI.

---

## Developer Pain Points
- **Mid-generation hangs that brick a session (#2582):** No recovery path. This is the kind of bug that will drive users to alternative tools if not addressed quickly.
- **Long-standing feature requests without maintainer response (#1283):** The Memory System issue has 15 comments over months with no maintainer engagement, fueling a sense that community priorities aren't aligned with the roadmap.
- **Windows-specific `UnicodeEncodeError` on legacy codecs (#2577):** Affects core CLI startup on GBK/other legacy codecs—an annoying, low-hanging fruit fix that reduces friction for non-UTF-8 environments.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-04

## Today's Highlights

OpenCode ships v1.18.12 with a critical Azure GPT-5.5+ completion fix, while the community rallies around long-standing requests for persistent session memory (#16077) and clickable links (#1168). Desktop UX remains the top pain point — scroll jumping, paste-induced hangs, and version mismatch with the CLI dominate the issue tracker. Meanwhile, contributors are landing meaningful fixes in Unicode patch matching, session retry logic, and event-log compaction.

## Releases

**[v1.18.12](https://github.com/anomalyco/opencode/releases/tag/v1.18.12)**
- **Core**: Fixed Azure GPT-5.5+ completion requests failing when reasoning is enabled (@frederiknsgo) — closes #40257
- **Desktop**: Reduced composer lag when drafts include large pasted images or attachments
- **Desktop**: Project search now matches any known recent project instead of only the first five

## Hot Issues

1. **[#27167 — Native session goals with /goal](https://github.com/anomalyco/opencode/issues/27167)** (123 👍, 67 comments)
   The most popular open feature request. Users want persistent, session-scoped goals rather than ad-hoc slash commands. Strong demand signals a need for structured session lifecycle management.

2. **[#1168 — Clickable links (Ctrl+Left Click)](https://github.com/anomalyco/opencode/issues/1168)** (118 👍, 10 comments)
   A year-old request still resonating. Users expect terminal-standard URL interaction. Low implementation complexity, high daily-impact value.

3. **[#36942 — Vertical tabs](https://github.com/anomalyco/opencode/issues/36942)** (16 👍, 10 comments)
   The new UI's horizontal tabs break at ~5 sessions. Users want vertical tab layouts for better session triage — a common IDE pattern OpenCode hasn't adopted yet.

4. **[#16077 — Persistent Session Memory](https://github.com/anomalyco/opencode/issues/16077)** (3 👍, 12 comments)
   Users want continuity across sessions, particularly for CLI-based companion workflows. Lightweight traction but conceptually foundational.

5. **[#38932 — Desktop hang on long paste](https://github.com/anomalyco/opencode/issues/38932)** (4 comments)
   Pasting 5000+ characters freezes the desktop app indefinitely. A critical reliability bug for a chat tool where long context pasting is core workflow.

6. **[#40314 — "Unable to connect to the first certificate"](https://github.com/anomalyco/opencode/issues/40314)** (4 comments)
   Network TLS errors on specific ISPs (MTN Broadband) block all usage. No workaround documented — needs better error surfacing and retry behavior.

7. **[#20600 — Random mid-conversation scroll jumps](https://github.com/anomalyco/opencode/issues/20600)** (2 👍, 4 comments)
   Desktop v1.3.13 intermittently scrolls to middle of chat. Pairs with #29094 and #17996 — the scroll-jump family is OpenCode's most-reported desktop bug class.

8. **[#37096 — Web UI empty session list on Windows/WSL](https://github.com/anomalyco/opencode/issues/37096)** (5 👍, 3 comments)
   Project auto-registration fails on Windows/WSL2, leaving the Web UI session list empty. Cross-platform filesystem path issues remain a persistent theme.

9. **[#40171 — Incomplete SSE event stream from Go service](https://github.com/anomalyco/opencode/issues/40171)** (2 👍, 2 comments)
   `POST /v1/responses` advertises OpenAI Responses-compat but emits incomplete SSE events. Breaks Codex-style clients — a protocol correctness issue, not just cosmetic.

10. **[#40286 — RTL/bidi broken for mixed Arabic+Latin text](https://github.com/anomalyco/opencode/issues/40286)** (2 comments)
    Mixed RTL/LTR lines render scrambled in both TUI and desktop. A correctness bug affecting a non-trivial user segment.

**Also notable**: [#39207](https://github.com/anomalyco/opencode/issues/39207) (GitHub OAuth login fails with empty email) — closed but serious; [#35122](https://github.com/anomalyco/opencode/issues/35122) (Desktop update doesn't update CLI, causing version mismatch) — architectural concern.

## Key PR Progress

1. **[#40268 — Retry top-level stream request timeouts](https://github.com/anomalyco/opencode/pull/40268)** — Fixes #39221. Handles providers that return HTTP 200 with an SSE error event, ensuring proper retry behavior instead of silent failures.

2. **[#40198 — Canonically equivalent Unicode in patches](https://github.com/anomalyco/opencode/pull/40198)** — Closes #31651. Patch verification now passes on canonically equivalent Unicode, fixing failures when files use composed vs. decomposed forms.

3. **[#36710 — Bound event log compaction](https://github.com/anomalyco/opencode/pull/36710)** — Closes #33356. Adds dry-run-by-default bounded compaction (`--session`/`--all`, `--apply`) with read-only event-log status. Addresses unbounded growth concerns.

4. **[#40188 — Request-scoped `chat.model` plugin hook](https://github.com/anomalyco/opencode/pull/40188)** — New feature addressing #18793 and #24006. Plugins can now replace the model per-request before provider resolution. Enables per-request routing/billing logic.

5. **[#38790 — Workspace flows in new layout](https://github.com/anomalyco/opencode/pull/38790)** — Local/New/Existing workspace selection for new sessions with persisted, validated drafts. Substantial UX investment in session onboarding.

6. **[#40265 — Azure GPT-5.5+ reasoningEffort fix](https://github.com/anomalyco/opencode/pull/40265)** — Closes #40257. The fix behind v1.18.12; Azure completions path now handles `reasoningEffort` correctly.

7. **[#40337 — Localhost browser preview for desktop sessions](https://github.com/anomalyco/opencode/pull/40337)** — In-app panel to view/interact with the session's dev server. Needs compliance review, but a strong DX addition for web developers.

8. **[#40316 — Safe defaults for all agents](https://github.com/anomalyco/opencode/pull/40316)** — Moves external-directory and `.env` read policy into universal agent defaults. Security hardening with explicit path allowlist behavior.

9. **[#40334 — Configurable permission mode keybind](https://github.com/anomalyco/opencode/pull/40334)** — Closes #40331. Users can now rebind the key for toggling auto-approve permissions in the TUI.

10. **[#40320 — Autonomous agents guide with reboot-resume](https://github.com/anomalyco/opencode/pull/40320)** — New docs page documenting a battle-tested pattern for unattended agents using a SQLite "intention database" for persistence and reboot-resume.

**Also notable**: [#40144](https://github.com/anomalyco/opencode/pull/40144) (reject unavailable project destinations in TUI picker), [#40285](https://github.com/anomalyco/opencode/pull/40285) (refined diff viewer with 2px left bar), [#35233](https://github.com/anomalyco/opencode/pull/35233) (background subagent commands).

## Feature Request Trends

1. **Session Memory & Persistence** — Multiple requests (#16077, #27167) push for continuity beyond a single conversation. The `/goal` proposal and persistent-memory idea both target the same gap: OpenCode sessions are stateless by default.

2. **Desktop GUI Parity** — #31399 and #40335 both request skill/MCP management UI in the desktop app. Users don't want to drop to CLI for configuration; the desktop app needs feature parity with the TUI.

3. **Context & Attachment Flexibility** — #40341 asks for arbitrary file types (PDFs, Office docs) as tool-accessible context, beyond what models can natively consume. Emerging need for richer document handling.

4. **Workspace Artifacts** — #35318 (V2 workspace artifacts with local preview and publishing) indicates a desire to treat session outputs as durable, shareable files rather than ephemeral chat content.

5. **Timestamp & Timing Precision** — #35348 requests millisecond-precision start/completion timestamps, suggesting growing sophistication in how users monitor and debug runs.

## Developer Pain Points

1. **Desktop Scroll Jumping (3 open issues)** — #17996, #20600, #29094 all report viewport snapping or jumping during chat. This is the single most-frustrating desktop UX bug class, spanning multiple releases.

2. **Silent Failures on Connection/DNS** — #40314, #40319, #40330 all involve OpenCode hanging or retrying endlessly without surfacing connection errors. Users need actionable errors, not 60-second silent waits.

3. **Provider Compatibility Gaps** — The Azure reasoning fix (#40265), DeepSeek V4 corruption (#40321), Bedrock chunkTimeout (#26487), and missing SSE events (#40171) highlight ongoing friction with non-OpenAI providers.

4. **Desktop/CLI Version Drift** — #35122: desktop updates don't update the CLI, causing session sync failures. An architectural concern that erodes trust in the desktop app.

5. **Localization & Text Handling** — RTL/bidi corruption (#40286) and canonical Unicode patch failures (#31651, fixed in #40198) show text handling isn't fully robust for international users.

6. **Configuration & Auth Friction** — OAuth empty-email failures (#39207), Zen signup invalid-email (#39414), and unmet credential-helper config placeholders (#12710) indicate auth flows still have rough edges.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-04

## Today's Highlights
The Pi community is actively addressing cross-platform reliability, particularly around Windows/WSL support and authentication flows. Major PR momentum is centered on JSON streaming performance (making output linear instead of quadratic), session infrastructure with the new Harness v2, and a batch of fixes for long-standing Windows path handling issues. A notable community-driven quality gate is emerging around upstream dependency management and session discovery through symlinks.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#6187 — Pi login hangs in WSL after browser-based GitHub Copilot device authorization](https://github.com/earendil-works/pi/issues/6187)**  
   Login flow completes in the browser but the WSL client never detects it, hanging indefinitely. 20 comments — a major adoption blocker for WSL users. The issue persists over a month after creation, suggesting a particularly tricky IPC or filesystem detection problem in the WSL environment.

2. **[#6768 — Compaction using Copilot Enterprise not possible](https://github.com/earendil-works/pi/issues/6768)**  
   Compaction fails with `421 Misdirected Request` on OpenAI-compatible endpoints and similar errors on Anthropic models. 18 upvotes signal this is a high-impact bug for enterprise users relying on context compaction to stay within token limits. The differing error paths across model providers complicate the root-cause analysis.

3. **[#7064 — WSL absolute windows paths are mishandled](https://github.com/earendil-works/pi/issues/7064)**  
   Tools like `read`, `write`, and `edit` fail on Windows paths from WSL, causing the agent to fall back to inefficient full writes via CLI tools. This is a frequent enabler of poor agent performance for WSL users — if path handling fails, the agent downgrades from structured tools to shell-based workarounds.

4. **[#7161 — anthropic-messages never sends x-client-request-id](https://github.com/earendil-works/pi/issues/7161)**  
   Missing request ID headers break session affinity for gateways that round-robin between backends. The proxy author reports that conversations get split across Claude accounts without a consistent session identifier. Marked in-progress, likely to ship as a small but impactful header fix.

5. **[#7547 — How do you use Pi on Windows? What issues are you seeing?](https://github.com/earendil-works/pi/issues/7547)**  
   A community call-to-action from petrroll to gather Windows usage patterns and pain points. The sheer number of ways to run Pi on Windows makes prioritization difficult; this issue aims to focus core-team energy on the most common configurations. Valuable signal for shaping the Windows roadmap.

6. **[#7399 — truncateToWidth() leaves dangling OSC 8 hyperlink when it truncates inside one](https://github.com/earendil-works/pi/issues/7399)**  
   Terminal output truncation can cut hyperlinks mid-sequence, leaving a dangling OSC 8 escape that corrupts the rendering state of the terminal. Reproduced with a minimal script — a correctness bug in terminal I/O that affects any user with long model outputs containing links.

7. **[#7130 — Backspace deletes 2 chars in Kitty (Kitty protocol release events not filtered)](https://github.com/earendil-works/pi/issues/7130)**  
   A niche but reproducible terminal-keyboard protocol bug affecting Kitty users specifically. Shows the community's attention to edge cases in terminal emulator compatibility — a category that has seen a constant trickle of similar reports.

8. **[#7395 — JSON mode serializes cumulative assistant state on every delta, causing quadratic output](https://github.com/earendil-works/pi/issues/7395)**  
   In `--mode json`, each streaming update carries both the delta and the full accumulated message, making output grow quadratically with response length. Directly addresses stdout performance for scripts and CI pipelines consuming Pi's JSON output.

9. **[#7560 — xai Grok 4.5 does not show up in the models list for GitHub Copilot Business subscription](https://github.com/earendil-works/pi/issues/7560)**  
   Model catalog inconsistencies surface for Copilot Business subscribers — Grok 4.5 is absent despite being available in the provider's catalog. Likely a metadata or capability-flag mismatch in the models.dev integration.

10. **[#7020 — Sometimes Pi doesn't continue after compaction](https://github.com/earendil-works/pi/issues/7020)**  
    Long-running "coordinator" sessions stalling post-compaction. Closed as of last update, with the fix likely tied to PR #7370 (manual compaction race) — but the issue's 9 comments highlight how impactful compaction reliability is for power users running marathon sessions.

## Key PR Progress

1. **[#7394 — Make JSON streaming output linear](https://github.com/earendil-works/pi/pull/7394)**  
   Emits delta-only records in JSON/RPC modes while preserving cumulative snapshots internally. Adds stdout backpressure, documents the breaking wire-protocol migration. A performance-critical fix for anyone scripting against Pi's JSON mode.

2. **[#7540 — Resume after context-limited length stops](https://github.com/earendil-works/pi/pull/7540)**  
   Treats length stops as context overflow when usage is within 1% of the context window, includes cache-write tokens in the calculation, and allows non-zero output for reasoning models that emit tokens before an incomplete stop. Addresses a nagging class of "mystery stops" on OpenAI-style APIs.

3. **[#7370 — Prevent auto-compaction race during manual compaction](https://github.com/earendil-works/pi/pull/7370)**  
   Keeps `AgentSession` subscribed during manual compaction aborts, removing the obsolete disconnect/reconnect cycle. Root cause: disconnecting mid-response let auto-compaction fire concurrently, causing the double-compact loop reported in #7253.

4. **[#7503 — Implement harness v2 for in-memory storage](https://github.com/earendil-works/pi/pull/7503)**  
   Introduces backend-neutral `SessionStorage`/`SessionRepo` APIs with an `InMemorySessionStorage` implementation. Lays the foundation for a more modular session architecture — first of several harness v2 pieces landing in the codebase.

5. **[#7396 — Add server session backend](https://github.com/earendil-works/pi/pull/7396)**  
   Adds a durable server backend that persists coding-agent sessions as JSONL with cross-process locking and crash recovery. Projects harness events into protocol snapshots — a key step toward robust multi-process Pi server deployments.

6. **[#7548 — Sandbox issue analysis tools](https://github.com/earendil-works/pi/pull/7548)**  
   Preserves the `pi -p --approve` and `/is <issue-url>` flows but captures an immutable issue snapshot before starting, directing `/is` to the local snapshot instead of model-facing network fetches. Hardens the security posture for issue-driven workflows.

7. **[#7569 — Normalize find root results](https://github.com/earendil-works/pi/pull/7569)**  
   Rewrites path relativization using `.relative()` instead of hand-rolled slicing, and uses Node facilities for path selectors. Directly targets the Windows path corruption bugs in #6104 and #6817 — a cluster likely fixed by this single PR.

8. **[#7552 — Discover sessions through symlinked directories](https://github.com/earendil-works/pi/pull/7552)**  
   Fixes session discovery ignoring symlinked directories under the global sessions root, adding regression coverage for directory links, broken links, and non-directory links. Closes #7497 — a quiet but annoying gap for users who symlink their `.pi` directory for dotfile management.

9. **[#7561 — Stream delta-only message_updates in json mode](https://github.com/earendil-works/pi/pull/7561)**  
   A complementary/alternative implementation to #7394 for linear JSON output. Both PRs landed nearly simultaneously — the maintainers will need to reconcile the two approaches; the fact that two independent contributors shipped the same fix is a strong signal of community demand.

10. **[#7568 — Add generic sampling parameters in models.json](https://github.com/earendil-works/pi/pull/7568)**  
    Adds generic `sampling_params` for engine-specific parameters like `dry_multiplier`, `xtc_probability`, and `repetition_penalty` for llama.cpp/vLLM. A pragmatic win for self-hosters who want engine-specific controls without Pi needing to know every knob.

## Feature Request Trends

- **Windows/WSL first-class support** — The single largest theme this digest cycle. Multiple issues (#6187, #7064, #6817, #6104) plus the maintainer-moderated survey (#7547) point to Windows being a priority but not yet a polished experience. Expect continued investment in path handling and process management on Windows.
- **Compaction control and reliability** — Three distinct asks: configurable thinking level/model for compaction (#7553), fixing compaction failures on enterprise providers (#6768), and preventing post-compaction stalls (#7020). Users want compaction to be both more reliable and more tunable.
- **Session infrastructure modularity** — The Harness v2 work (in-memory storage #7503, server backend #7396) plus symlink discovery (#7552) suggest the community is pushing toward more flexible session persistence and multi-process operation.
- **Provider-agnostic fidelity** — Issues like the missing `x-client-request-id` (#7161) and Gemini tool-call ID handling (#7047) show users integrating Pi with gateways and proxies expect byte-level protocol fidelity across all provider paths.

## Developer Pain Points

- **WSL path handling is consistently broken** — The combination of "absolute windows paths are mishandled" (#7064) and "find returns no results for path patterns" (#6817) means WSL users see degraded agent tool use as a default state. The issue isn't one bug but systemic path translation problems.
- **Authentication flows that stall without feedback** — The login hang in WSL (#6187) is the worst offender: the user completes the browser flow, the device shows as registered, but the client never proceeds. Silent failure modes like this erode trust in the tool.
- **Compaction is fragile under real-world usage** — Enterprise licenses fail outright (#6768), manual compaction can race with auto-compaction (#7253), and sessions can stall after compaction (#7020). For long-running sessions — a Pi hallmark use case — compaction reliability is make-or-break.
- **JSON streaming performance degrades quadratically** — The fact that two independent PRs (#7394, #7561) shipped the same delta-only fix in one cycle shows how acutely users feel this in CI/scripting pipelines. The quadratic blowup turns long responses into unusably slow stdout drains.
- **Session discovery is too rigid** — Silent ignoring of symlinked directories (#7497) undermines dotfile management workflows and breaks external tools like pi-web that list sessions. Small friction, but it forces users to abandon preferred directory layouts.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-04

## Today's Highlights

Web Shell reaches release-readiness as a desktop app with native lifecycle management and auto-updates, while the core runtime around MCP tool-call semantics and abort handling continues to harden. The community is actively reporting session-management bugs (authentication, tool-call IDs, transcript persistence), and maintainers have shipped fixes for OpenAI SDK abort misclassification and reasoning-effort wire shapes.

## Releases

**v0.21.4** — Patch release (release notes not detailed beyond version header). Note: v0.21.5 release workflow failed on the `quality` job; see [#8476](https://github.com/QwenLM/qwen-code/issues/8476).

## Hot Issues

1. **[#8102](https://github.com/QwenLM/qwen-code/issues/8102) — Deterministic tool-execution boundaries for a trustworthy agent runtime** (P3, feature-request, 13 comments): Proposal to keep the LLM outside the trust boundary and deterministically constrain/authorize/observe tool actions. High-engagement design discussion; signals direction toward agent-tool security guarantees.

2. **[#8316](https://github.com/QwenLM/qwen-code/issues/8316) — Prompt not restored to input box when canceling with Ctrl+C** (bug, 7 comments): User cancels an in-flight prompt expecting the text to return for editing; it is lost. High-frequency UX pain point in interactive sessions.

3. **[#8382](https://github.com/QwenLM/qwen-code/issues/8382) — Duplicate provider tool call id** (P2, bug, 6 comments): "Duplicate provider tool call id" errors on repeated invocation, leading to environment instability. Impacts providers with strict ID uniqueness (OpenAI-compatible).

4. **[#8330](https://github.com/QwenLM/qwen-code/issues/8330) — @-completion tab switching inaccessible in Warp** (P2, bug): `Ctrl+Tab` is captured by Warp terminal tabs; cannot switch completion categories. Highlights integration friction with third-party terminals.

5. **[#8452](https://github.com/QwenLM/qwen-code/issues/8452) — Size-triggered microcompaction repeatedly invalidates prompt cache** (P2, performance): Microcompaction rewrites already-cached prefix on consecutive ToolResult turns, defeating prompt caching. Cost/performance-sensitive issue for long agentic runs.

6. **[#8319](https://github.com/QwenLM/qwen-code/issues/8319) — Agent thinking presentation causes layout jumping** (P2, UI): Dynamic thinking-area height makes the whole panel move up/down, hurting readability. Common complaint with streaming/thinking UIs.

7. **[#8400](https://github.com/QwenLM/qwen-code/issues/8400) — Desktop sessions silently auto-deleted after restart when ACP session/load fails** (P1, Windows): Workspace cwd mismatch causes provider message loader to return 0 messages → local mirrors deleted without confirmation. **Data-loss P1**; high severity for desktop users.

8. **[#8432](https://github.com/QwenLM/qwen-code/issues/8432) — Bailian Personal Token Plan models out of sync; image/video generation fails** (P2, auth): `/auth` model list stale vs. Bailian console; multimodal generation broken for Token Plan users.

9. **[#8398](https://github.com/QwenLM/qwen-code/issues/8398) — `isAbortError` misses OpenAI SDK's `APIUserAbortError`** (P2, core): Cancellation misclassified → downstream bugs (see #8356 transcript loss). Already fixed in PR #8399.

10. **[#8356](https://github.com/QwenLM/qwen-code/issues/8356) — After `APIUserAbortError`, subsequent turns not written to local session transcript** (P2): Consequence of #8398; user cancel corrupts transcript persistence for the rest of the session.

## Key PR Progress

1. **[#8488](https://github.com/QwenLM/qwen-code/pull/8488) — Harden Qwen 3.8 reasoning effort wire shape** (fix(core)): Follow-up to #8472; drops `enable_thinking`/`thinking_budget` when `reasoning_effort` is shipped, fixes competing knobs.

2. **[#8482](https://github.com/QwenLM/qwen-code/pull/8482) — A never-delivered MCP call is a first delivery, not a replay** (fix(core)): Deterministic test failure fix; distinguishes first delivery from replay in auto-reconnect scenarios.

3. **[#8399](https://github.com/QwenLM/qwen-code/pull/8399) — Recognize OpenAI SDK `APIUserAbortError` as an abort** (fix(core)): Directly addresses #8398; sets `.name` for SDK error detection.

4. **[#8260](https://github.com/QwenLM/qwen-code/pull/8260) — Preserve every reasoning episode's signature during history consolidation** (fix(core)): Fixes Gemini turn-consolidation dropping all but the first `thoughtSignature`.

5. **[#8276](https://github.com/QwenLM/qwen-code/pull/8276) — Preserve prompt cache across deferred tool discovery** (fix(core)): Keeps provider tool declarations and cached system prompt stable while deferred tools (`tool_search`) are discovered; new `deferred_tool_call` bridge.

6. **[#8274](https://github.com/QwenLM/qwen-code/pull/8274) — Fork from any conversation** (feat): Makes earlier Assistant responses safe branch points; handles tool calls, cancellations, metadata, transcript pagination, rewinds, concurrent branches.

7. **[#7925](https://github.com/QwenLM/qwen-code/pull/7925) — Sweep stale worktree project snapshots on startup** (fix(core)): Prevents unbounded `.qwen/projects/<worktree>` accumulation from crash/force-kill paths.

8. **[#8368](https://github.com/QwenLM/qwen-code/pull/8368) — Add Kimi and Xiaomi MiMo providers** (feat(auth)): New first-class `/auth` presets with region-specific credential choices.

9. **[#7567](https://github.com/QwenLM/qwen-code/pull/7567) — Add `/advisor` command for second-opinion conversation review** (feat(cli)): Read-only forked reviewer model for independent feedback on current conversation.

10. **[#7837](https://github.com/QwenLM/qwen-code/pull/7837) — Coordinate terminal teardown** (fix(cli)): Single synchronous, idempotent teardown covering normal cleanup, direct exits, SIGINT/SIGTERM/SIGHUP; preserves signal-derived exit codes.

## Feature Request Trends

- **Trusted/constrained agent runtime** (#8102): Deterministic tool-execution boundaries, authorization, and observation — the community wants verifiable agent behavior, not just capability.
- **More communication channels** (#8281): IMAP/SMTP email channel for agent interaction; signals move toward background/async agent operation.
- **Background automation roadmap** (#8281, #8389): Plan & Review workflow for daemon sessions, opt-in DAG-based task planning with mutation blocking.
- **Provider breadth** (#8368): Kimi and Xiaomi MiMo additions; users continuously ask for more third-party provider presets with regional access choices.
- **Configurability of internals** (#8168): Making memory dream-agent max turns and similar knobs user-settable — request for operational transparency.

## Developer Pain Points

- **Session/transcript integrity**: Multiple P1/P2 bugs around silent session deletion (#8400), transcript loss after aborts (#8356), and missing prompt restoration (#8316). Trust in session persistence is a recurring theme.
- **MCP tool-call identity**: Duplicate tool-call IDs (#8382) and stale session registrations after metadata hot reload (#8492) — MCP reliability remains the top ecosystem friction point.
- **Provider SDK mismatches**: Abort-error misclassification (#8398) and stale model lists (#8432) show the cost of supporting many OpenAI-compatible and vendor-specific endpoints.
- **Terminal/UI integration friction**: Warp `Ctrl+Tab` interception (#8330), ConEmu/Cmder flickering (#8385), and layout-jumping thinking presentation (#8319) — rendering and keybinding issues across terminal emulators persist.
- **Prompt-cache invalidation**: Microcompaction rewriting cached prefixes (#8452) and deferred tool discovery threatening prompt stability (#8276) highlight cost/performance sensitivity in long agentic sessions.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-04

## 1. Today's Highlights

The v0.9.4 release train is in full swing with a massive 30-PR integration stack, including a 77-commit train PR (#5135) and numerous hygiene fixes to unblock CI. A cluster of Copilot-authored Runtime API PRs (#5129-#5133) is expanding the HTTP surface with goal-loop, memory, skill lifecycle, MCP management, and verifier receipt endpoints — signaling a strong push toward managed-client and cloud-app parity. Community contributions continue to flow in with a Chinese Windows beginner guide (#5229), ratatui version pinning to fix a terminal race (#5192), and path fixes for the OpenHarmony linker (#5095).

## 2. Releases

No new releases in the last 24 hours. Current target is **v0.9.4**, with PR #5135 serving as the integration train (77 commits ahead of `main`). The v0.9.3 branch remains the latest stable line.

---

## 3. Hot Issues

### #3192 — [OPEN] Put DeepSeek-TUI up for agentclientprotocol/registry
**Author:** Jengro777 | **Comments:** 13 | [Link](https://github.com/Hmbown/CodeWhale/issues/3192)
Community request to list the project in the ACP registry so Zed (and other ACP-compatible editors) can install/use it directly. This overlaps with PR #5225 which adds ACP tool execution support — the ecosystem demand for editor integration is clearly rising.

### #3205 — [OPEN] v0.9.3: Fleet model classes, loadout auto, and semantic route roles
**Author:** Hmbown | **Comments:** 11 | [Link](https://github.com/Hmbown/CodeWhale/issues/3205)
Architectural goal to create a unified model/loadout selector used across TUI, CLI, exec, subagents, and Fleet workers — introducing "Fleet loadout auto" as a first-class automatic mode. This is a core piece of the fleet/distributed compute story.

### #1481 — [OPEN] Support OpenCode Go/Zen (provides DeepSeek-V4 as well)
**Author:** seanthefuturegorilla | **Comments:** 10 | 👍: 1 | [Link](https://github.com/Hmbown/CodeWhale/issues/1481)
Request to support OpenCode Go/Zen as a DeepSeek provider. The contributor notes it's "very cheap" and serves DeepSeek-V4 — a pricing-aggressive alternative that the community wants tapped.

### #4959 — [OPEN] Proposed 'stop' command
**Author:** ronohara | **Comments:** 7 | [Link](https://github.com/Hmbown/CodeWhale/issues/4959)
Feature request for a `/stop` command and runtime STOP-word intercept for mechanical tool-call blocking. The problem: when a model is in YOLO mode or deep in autonomous workflows, textual "stop" is ignored — a critical safety/control gap that resonates with the agentic-workflow crowd.

### #4949 — [OPEN] Discussion: Chinese Translation of "Constitution"
**Author:** SparkofSpike | **Comments:** 7 | [Link](https://github.com/Hmbown/CodeWhale/issues/4949)
Open debate (bilingual Chinese/English) on whether "Constitution" should translate to "宪法" (constitution, politically sensitive) or "协作准则" (collaboration guidelines) — spawned from PR #4908 which reverted the translation. Shows a community actively caring about localization nuance, not just raw translation.

### #2492 — [OPEN] 不具备跨会话记忆 (No cross-session memory)
**Author:** jianage | **Comments:** 5 | [Link](https://github.com/Hmbown/CodeWhale/issues/2492)
Chinese-language bug report: sessions start without memory, and even forced memory writes aren't read back on restart. User notes "response is very fast" but the memory gap hurts usability. This is a persistent complaint pattern across multiple issues.

### #1917 — [OPEN] Proposal: Universal PreToolUse/PostToolUse hook layer
**Author:** aboimpinto | **Comments:** 5 | [Link](https://github.com/Hmbown/CodeWhale/issues/1917)
Architecture proposal for a hook-based lifecycle layer (PreToolUse/PostToolUse) providing Cancel/Pause/Resume semantics for **any** action that calls a tool — unifying what is currently fragmented across slash commands and action types. The community sees this as the right pattern for building safe autonomous agents.

### #4785 — [OPEN] Dead-code sweep: 464 `#[allow(dead_code)]` attributes hiding drift
**Author:** Hmbown | **Comments:** 4 | [Link](https://github.com/Hmbown/CodeWhale/issues/4785)
Measured technical debt: 464 dead-code allowances across 143 files prevents the compiler from reporting real drift. The issue quantifies exactly how much code is hiding behind the wall — a strong argument for cleanup before v0.9.4 lands.

### #4022 — [OPEN] v0.9.3: Define CLI/TUI parity for subagent and runtime control surfaces
**Author:** Hmbown | **Comments:** 7 | [Link](https://github.com/Hmbown/CodeWhale/issues/4022)
The TUI sidebar is becoming the primary place for subagent control, but this traps those controls inside the terminal. The issue asks: what happens when a future cloud app or remote workbench needs the same surfaces? This is the strategic "exit the TUI" discussion.

### #3306 — [OPEN] v0.9.3 Refactor: Converge runtime ownership, delete duplication, ship one executable
**Author:** Hmbown | **Comments:** 4 | [Link](https://github.com/Hmbown/CodeWhale/issues/3306)
Umbrella refactor: 18 Rust packages (~771k lines) with 87% locked inside `codewhale-tui`, which owns parallel runtime/tool/config/session/hook paths. The goal is to converge ownership and ship one executable — a foundational architecture change with wide-reaching implications for stability and performance.

---

## 4. Key PR Progress

### #5135 — [OPEN] release: Codewhale v0.9.4 release train
**Author:** Hmbown | [Link](https://github.com/Hmbown/CodeWhale/pull/5135)
The integration train for v0.9.4 — 77 commits ahead of `main`, superseding #5044 and absorbing all 2026-08-01 source candidates. This is the central merge target that the entire 30-PR stack is building against.

### #5227 — [CLOSED] fix(tui): train hygiene — locale parity, #5110 fallout, fmt drift, warnings, budget
**Author:** Hmbown | [Link](https://github.com/Hmbown/CodeWhale/pull/5227)
Hygiene debt cleanup across the v0.9.4 train: zh-Hant locale parity fix (complete pack at 1252 keys), fallout from #5110, formatting drift, warnings, and budget issues. The "30-PR stack" mention reveals the scale and velocity of this release.

### #5231 — [CLOSED] style(tui): clear deny-level clippy lints blocking the v0.9.4 train
**Author:** Hmbown | [Link](https://github.com/Hmbown/CodeWhale/pull/5231)
Fixed 30 deny-level clippy lints (16 unique sites) across bin (14) and test (16) targets — predominantly `collapsible_if` (7 instances). Unblocks the train→main CI gate that runs with `-D warnings`.

### #5230 — [CLOSED] fix(web): map Model Studio provider variants in facts drift guards
**Author:** Hmbown | [Link](https://github.com/Hmbown/CodeWhale/pull/5230)
Fixes the public-surface contract test by mapping Model Studio provider variants in `facts.generated.ts` — regenerated with 40 providers / 68 tools after #5230's variant additions. Contract tests pass 12/12.

### #5233 — [OPEN] fix(modelstudio): surface reasoning on official chat routes
**Author:** Inference1 | [Link](https://github.com/Hmbown/CodeWhale/pull/5233)
Classifies `reasoning_content` as a dedicated Thinking stream only on verified Alibaba Model Studio OpenAI-compatible routes. Also shapes documented Model Studio controls by capability: `enable_thinking`, `preserve_thinking`, and DeepSeek-V4/GLM `reasoning_effort`.

### #5225 — [OPEN] feat(acp): expose file/search/git/patch/shell tools over session/prompt
**Author:** rafaelcavalheri | [Link](https://github.com/Hmbown/CodeWhale/pull/5225)
Critical ACP gap fix: `session/prompt` previously only streamed model text — never executed tool calls. Now exposes file/search/git/patch/shell tools so Zed and community adapters (like `acp-deepseek-adapter`) get a real coding agent instead of a chat-only shell.

### #5192 — [OPEN] fix(tui): pin ratatui to 0.30.0
**Author:** bistack | [Link](https://github.com/Hmbown/CodeWhale/pull/5192)
Pins `ratatui =0.30.0` and `ratatui-core =0.1.0` because 0.1.1+ makes `Terminal::clear()` issue a blocking CPR query (`\x1b[6n`) that races the crossterm event-reader lock at startup. A subtle but impactful terminal race condition fix.

### #5229 — [OPEN] docs: add Docs/windows beginner guide in zh-CN
**Author:** vFONGv | [Link](https://github.com/Hmbown/CodeWhale/pull/5229)
New Chinese-language Windows beginner guide covering installation, configuration, model switching, modes/permissions, and FAQs — with commands verified on Windows 10 and real screenshots. Addresses the growing Chinese Windows user base.

### #5228 — [OPEN] refactor(tui): rail unification stack (rebased onto train)
**Author:** Hmbown | [Link](https://github.com/Hmbown/CodeWhale/pull/5228)
Rebases a 12-commit rail-unification stack (local `agent/rail-unify-panels-20260802`) onto the v0.9.4 train. The train moved mid-rebase (`145472341` → `27c1c9ffe`), requiring a double rebase, with final base at `27c1c9ffe`.

### #5095 — [OPEN] fix(ohos): re-quote Windows linker arguments containing spaces
**Author:** shenjackyuanjie | [Link](https://github.com/Hmbown/CodeWhale/pull/5095)
Fixes OpenHarmony builds when the SDK path contains spaces (e.g. default `D:\DevEco Studio\...\native`): rustc passes quoted linker args, but cmd's `%*` strips the quoting, splitting `--sysroot` on spaces. Practical Windows correctness fix.

---

## 5. Feature Request Trends

1. **ACP / Editor Ecosystem Integration** — Multiple threads (#3192, PR #5225) push for deep Zed/editor integration via the Agent Client Protocol. The community wants DeepSeek-TUI to be installable from ACP registries and to expose real tool execution over `session/prompt`.

2. **Runtime API Expansion for Managed Clients** — A cluster of Copilot-authored PRs (#5129-#5133) adds HTTP endpoints for goal-loop read/lifecycle, memory inspection/control, skill install/update/uninstall/trust/audit, bounded MCP server CRUD, and verifier receipts/evidence. The direction is clear: the TUI must not trap functionality that remote/cloud clients need.

3. **Provider Breadth & Pricing** — Requests for cheaper/alternative DeepSeek providers (OpenCode Go/Zen #1481, minimax Chinese routes #4686, Model Studio reasoning polish #5233) and OAuth 2.1 MCP support (#1409). Users actively shop for the best price-performance and want multi-provider flexibility.

4. **Cross-Platform Windows Polish** — Recurring Windows requests: Windows Terminal as default launch (#1854), `winget` packaging (#1561), Chinese IME compatibility in TUI (#2323), and now a zh-CN Windows beginner guide (#5229) — plus the real OpenHarmony linker fix (#5095).

5. **Safety & Control Surfaces** — A `/stop` command with runtime intercept (#4959), universal PreToolUse/PostToolUse hook layer (#1917), permission profiles with nonblocking execution defaults (#3211), and read-before-edit guardrails (#3364). As autonomy increases (YOLO mode, fleet workers), the community demands stronger mechanical control.

---

## 6. Developer Pain Points

1. **Memory Loss Across Sessions** (#2492): Users are frustrated that conversations don't persist memory across restarts, and forced writes aren't auto-read. The issue explicitly notes "the advantage is fast response, but [memory] doesn't work well."

2. **Tool-Call Control & Interruptibility** (#4959, #1917): When models run autonomously (YOLO mode or deep workflows), text commands like "stop" are ignored. Developers need a hard, mechanical kill switch — the lack of it is a safety and trust blocker.

3. **Windows Environment Fragility** (#1854, #2323, #5095): Multiple Windows-specific issues: poor rendering in default cmd.exe, Chinese IME input conflicts with the TUI's event handling, and linker argument quoting breakage under paths with spaces.

4. **Tool Bloat & Architecture Debt** (#4785, #3306): 464 dead-code allowances hiding real drift, 18 Rust packages with parallel runtime paths, and duplicated managers (JobManager vs TaskManager #4167). The consequences of this sprawl are landing on maintainers and contributors who have to navigate it.

5. **Chinese Character Rendering** (#1675, #2323): Garbled Chinese in agent output and IME input conflicts are persistent localization bugs — directly affecting a large share of the Chinese-speaking user base, and therefore high priority for the maintainers.

6. **Missing Context/Help Surfaces** (#1708): The system prompt includes mode labels but no reference to built-in slash commands (`/mode`, `/config`, `/approval`), forcing models to hallucinate when users ask "how do I switch modes?" — a documentation-via-prompt problem.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*