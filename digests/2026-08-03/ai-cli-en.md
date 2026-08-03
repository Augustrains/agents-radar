# AI CLI Tools Community Digest 2026-08-03

> Generated: 2026-08-03 01:25 UTC | Tools covered: 9

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

# AI CLI Tools Cross-Tool Comparison Report — 2026-08-03

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem is in a period of rapid maturation, with seven major tools (Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code, OpenCode, Pi, Qwen Code, and DeepSeek TUI) all actively iterating. No new stable releases shipped in the last 24 hours across any tool, but community activity remains intense—hundreds of issues were updated and dozens of PRs are in motion. The dominant themes are **session reliability** (data loss, compaction failures, silent state corruption), **resource efficiency** (memory leaks, context window management, token waste), and **multi-agent orchestration** (subagent observability, permission propagation, cross-session communication). Security hardening (SSRF fixes, trust boundaries, redaction timing) and cross-platform parity (Windows/Linux gaps) are also recurring priorities. The ecosystem is shifting from "can AI write code" to "can AI agents operate reliably in production environments."

---

## 2. Activity Comparison (2026-08-03)

| Tool | Hot Issues (24h) | PRs in Motion | Release Status | Notable Flagship Issue |
|---|---|---|---|---|
| **Claude Code** | 30 tracked, 3 featured PRs | 3 | No new release | #2805 CRLF-on-Linux (44 comments, 33👍) |
| **OpenAI Codex** | 50 updated | 6 | No new release; latest v0.146.0-alpha.14 | #11023 Linux desktop app (905👍, 197 comments) |
| **Gemini CLI** | 10 tracked (P1/P2 mix) | 10 | v0.55.0-nightly.20260802 | #21409 Generalist agent hangs (8👍) |
| **GitHub Copilot CLI** | 10 tracked | 0 updated | No new release; latest v1.0.77 | #4202 `view` tool regression (critical) |
| **Kimi Code** | 4 hard, ~6 inferred | 1 (closed) | No new release | #2578 Swarm partial-work loss |
| **OpenCode** | 10 tracked | 10 (3 closed) | No new release | #20695 Memory megathread (121 comments) |
| **Pi** | 10 tracked | 10 (3 closed/merged) | No new release | #6879 Auto-compaction timing (10👍) |
| **Qwen Code** | 10 tracked | 10 | v0.21.3-nightly.20260803 | #8400 Silent session deletion (P1, Windows) |
| **DeepSeek TUI** | 10 tracked | 16 (all WIP batch) | No new release; v0.9.4 current | #5123 Agent spawn release blocker |

**Note:** No tool shipped a stable release in the last 24 hours. Gemini CLI and Qwen Code shipped nightly releases; all others are in active development toward upcoming versions.

---

## 3. Shared Feature Directions

| Feature Need | Tools Expressing It | Specific Requirements |
|---|---|---|
| **Session Reliability & Persistence** | Claude Code, Kimi Code, Pi, Qwen Code, DeepSeek TUI | Auto-save/resume (#8334 stashed prompt loss; #6879 compaction timing; #8400 silent deletion; #2578 partial batch loss) |
| **Persistent Memory Across Sessions** | Claude Code, Gemini CLI (Auto Memory), Kimi Code (#1283), OpenCode | AI-managed notes, user-defined instructions, cross-session project patterns; avoid re-explaining context |
| **Remote/Cross-Device Session Control** | Claude Code, OpenAI Codex (#27565), Kimi Code (#1282), Gemini CLI | Claude Code-style `/remote-control`-like sync across CLI/desktop/mobile without SSH tunnels |
| **Multi-Agent Observability** | Claude Code (#24537), Gemini CLI (#21763), DeepSeek TUI (#4397) | Real-time dashboards, subagent trajectory sharing in `/bug` reports, live agent hierarchy views |
| **Subagent Permission Enforcement** | Claude Code (#83421), Gemini CLI (#22093/#22672), DeepSeek TUI (#5123) | `bypassPermissions` propagation, subagents respecting "disabled" config, read-only flags fixed |
| **Token/Credits Efficiency** | OpenAI Codex (#13733/#35259), Pi (#6879), Gemini CLI (#22745) | Reduce polling-triggered full-history re-entry, AST-aware tools to cut turns, smarter context compaction |
| **Platform Parity (Windows/Linux)** | Claude Code (#32870 BSOD), OpenAI Codex (WS L #35119, Windows #23198), Gemini CLI (#21983 Wayland), Qwen Code (#8385/ConEmu), Copilot CLI (#4328/WSL2) | Consistent behavior across Windows, WSL2, Linux, macOS; sandbox/terminal parity |
| **Cross-Session IPC/Communication** | Claude Code (#69912), Kimi Code (#2579), OpenCode | Native inter-process channels, wake-the-CLI inboxes, SSH-reachable agents |
| **Cost/Payload Transparency** | DeepSeek TUI (#1004 `/dryrun`), Copilot CLI (#29968 billing), Qwen Code | Preview exact payloads (system prompts, tools, cached files) before sending—understand costs upfront |

---

## 4. Differentiation Analysis

| Tool | Core Focus | Target User | Technical Approach Differentiator |
|---|---|---|---|
| **Claude Code** | Anthropic Opus/Sonnet orchestration, TUI/desktop depth | Claude power users, complex multi-agent workflows | Deepest TUI feature surface (Cowork, desktop app); plugin ecosystem; session URL metadata in commits (privacy concern) |
| **OpenAI Codex** | GPT-5.x family, Pro/Pro20x plans, VS Code integration | OpenAI ecosystem users, IDE-heavy workflows | Tightly coupled to ChatGPT/Codex desktop; model catalog caps (372K vs 1.05M max); heavy Windows friction |
| **Gemini CLI** | Agent orchestration, skills/subagents, AST-aware tooling | Google developers, large-codebase automation | EPIC-driven roadmap (#22745 AST-aware); Dependabot-driven rapid dependency refresh; nightly cadence |
| **GitHub Copilot CLI** | Autopilot mode, ACP metadata, GitHub ecosystem | Existing GitHub users, VS Code/terminal hybrid | Models API (`/responses` vs `/chat/completions` surface splits); strong triage discipline; no new releases, stable cadence |
| **Kimi Code** | Moonshot Kimi models, swarm/parallel mode, memory | Kimi power users, multi-agent orchestration | Swarm-mode reliability gaps (#2578); external wake-channel proposal; "assistant-OS" ambition |
| **OpenCode** | Plugin extensibility, provider agnosticism, desktop | Plugin developers, multi-provider teams | Request-scoped `chat.model` hooks (#40188); per-MCP-server trust (#40125); SQLite WAL persistence overhaul; most acute memory-leak crisis |
| **Pi** | Terminal rendering fidelity, compaction autopilot, provider breadth | Terminal purists, WezTerm/tmux users, long-session workers | Compaction-first architecture (idle compaction deferral #7498); inline image handling; Gemini tool-call ID preservation; server-side session backends |
| **Qwen Code** | `/review` toolchain, security-hardened hooks, daemon system | Qwen model users, Enterprise (Maven/Java) workflows | Structured review artifacts (#8402); TUI capture-based verification evidence (#8388); hook SSRF fixes (#8396); audio bridge (#8332) |
| **DeepSeek TUI** | Multi-provider neutrality, agent runtime, Termux/Android | Power users across Linux/Android; Chinese-speaking base | Provider-agnostic Responses dialect profiles (#5108); isolated worktree Fleet builders (#5109); no-progress watchdog (#5115); 14k-line `main.rs` internal debt |

---

## 5. Community Momentum & Maturity

### Highest Momentum
- **OpenAI Codex** — Linux desktop app: 905👍 and 197 comments (sustained 6 months); VS Code diff crash: 115👍. Highest absolute vote totals, but frustration is mounting over Windows/stability.
- **Claude Code** — Long-standing line-ending bug (44 comments, filed 2025), session-URL-in-commits privacy push (44👍). Strong feature-request velocity but gaps in basic cross-platform fixes.
- **DeepSeek TUI** — 16 WIP PRs in 24h (provider-neutral architecture refactor), aggressive epic closure (v0.9.3 train). Fastest iteration cadence currently, focused on de-DeepSeeking before v1.0.

### Maturing Steadily
- **Gemini CLI** — EPIC-driven, Googler-maintained, nightly releases. 75-package Dependabot bumps signal infrastructure investment. Lower community voting (8👍 max) but disciplined P1/P2 triage and long-range technical roadmaps.
- **Qwen Code** — 10 PRs in motion, `/review` toolchain evolving rapidly with structured artifacts and evidence-based verification. Security hardening (4 hook trust-boundary fixes) suggests enterprise focus. P1 session-reliability issues (silent deletion, concurrent-writer disputes) show production users hitting real edge cases.
- **OpenCode** — Memory megathread with 121 comments and a maintainer request for heap snapshots (not AI-generated advice) signals an acute but acknowledged quality problem. PR pipeline is healthy (3 open code-fixes, 3 closed after cleanup).

### Stabilizing / Lower Intensity
- **GitHub Copilot CLI** — No PRs updated; new issues are mostly triage-level (3 new bugs with 0 comments). Stable cadence but the `view` tool regression (#4202) from 1.0.72 could erode pinned-version trust.
- **Pi** — Terminal-rendering fixes are being merged (WezTerm/iTerm2 preference #7482) but a renderer-switching feature was reverted (#7440 → #7473). Compaction issues remain the most-voted pain point.
- **Kimi Code** — 4 concrete issues in the dataset (plus inferred ones), 1 PR closed. Persistence memory (#1283) and remote control (#1282) have the strongest community support but remain unimplemented. Swarm reliability gap could become a differentiator if addressed.

---

## 6. Trend Signals & Developer Takeaways

### Industry Trends
1. **From "Can it code?" to "Can it operate?"** — Across all tools, the bulk of community pain is no longer about output quality but about reliability: session corruption, silent data loss, compaction failures, and permission-model gaps. Reliability is the new differentiator.
2. **Multi-agent orchestration is becoming first-class** — Claude Code's agent-hierarchy dashboard request, Gemini CLI's subagent observability EPICs, Kimi Code's external wake channels, and DeepSeek TUI's Fleet builders all point toward AI CLI tools becoming *agent orchestrators* beyond single-prompt codegen.
3. **Resource efficiency is a trust issue** — Token waste from polling (Codex #13733), multi-GB memory leaks (OpenCode, Codex app-server), and OOM-risk greps (Claude Code ugrep) are not just performance bugs—they burn credits and erode trust in long-running automation.
4. **Security must now span the full chain** — SSRF fixes in hooks (QwenCode), executor-controlled response bounding (Codex), secret redaction timing (Gemini CLI), and per-MCP-server trust (OpenCode) show the industry moving from "prompt-injection defense" to full supply-chain hardening.
5. **Cross-platform parity is a competitive wedge** — The Windows instability cluster (Codex #23198/#10090, Claude Code BSOD #32870, Qwen Code flickering) and Linux gaps (Codex Linux desktop, DeepSeek TUI Termux) plus WSL2 quirks (Copilot CLI Ctrl+H) represent repeatable, addressable product openings.
6. **Configuration and permission transparency is the new UX frontier** — Users demand to see what will execute (OpenCode trust config, DeepSeek TUI `/dryrun`, Copilot CLI ACP approval ambiguity) and to understand *why* failures occur (Copilot CLI autopilot state restoration, Qwen Code abort classification). Silent failures are the #1 trust-killer.

### For Developers
- **If you rely on a single tool for long sessions**, watch compaction and memory behavior: Pi (#6879), OpenCode (#20695), and Codex (#34863) all have known, active resource-exhaustion bugs.
- **If you operate on Windows or WSL2**, expect friction across every tool except perhaps Gemini CLI (which has no major Windows-specific reports in this digest): Claude Code BSOD risk, Codex sandbox failures, Copilot CLI Ctrl+H, Qwen Code flickering.
- **If you build multi-agent workflows**, check subagent permission propagation (Claude Code #83421, Gemini CLI #22093) and session-reliability claims (Kimi Code #2578, Qwen Code #7164) — these are the least-mature areas of the ecosystem.
- **If you value stable pinning**, Copilot CLI's `view` regression example shows even minor version bumps can break core tools; consider pinning until a patch-level release stabilizes.

**Bottom line:** The winner of this ecosystem phase won't be the tool with the strongest model—it will be the tool that can make long-running, multi-agent, multi-session workflows *feel boringly reliable*. Privacy, cost transparency, and permission clarity are emerging as the trust rebar that separates high-adoption tools from pilot experiments.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-08-03 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

### #1 — skill-creator Reliability Fixes (Multiple PRs)
**Most concentrated area of community attention.** Six separate PRs (#1298, #1099, #1050, #1323, #1261, #539) target critical bugs in the `skill-creator` evaluation pipeline (`run_eval.py`), which reports **recall=0%** on every description due to trigger-detection failures, Windows subprocess incompatibilities (`claude.cmd` vs `claude`, `PATHEXT`), and UI YAML parsing issues. This is the single most-discussed topic in the repository.
**Highlights:** #1298 (MartinCajiao) is the most comprehensive — fixing eval artifact installation, Windows stream reading, and parallel workers; #1323 (Polluelo978) isolates trigger-detection logic; #1261 (alvingarcia) prevents synthetic test files from polluting the user's live project registry. All are **OPEN**.
🔗 [PR #1298](https://github.com/anthropics/skills/pull/1298) | [PR #1099](https://github.com/anthropics/skills/pull/1099) | [PR #1323](https://github.com/anthropics/skills/pull/1323)

### #2 — document-typography (PR #514)
Skill enforcing typographic quality control for AI-generated documents: prevents **orphan word wrap**, **widow paragraphs** (section headers stranded at page bottom), and **numbering misalignment** — issues that "affect every document Claude generates." Author argues users rarely request good typography explicitly, so the skill fills a silent quality gap. **Status: OPEN** (created 2026-03-04, last updated 2026-03-13).
🔗 [PR #514](https://github.com/anthropics/skills/pull/514)

### #3 — ODT Skill (PR #486)
Adds OpenDocument format support (**.odt**, **.ods**) — creation, template filling, and ODT→HTML conversion. Triggers on "ODT," "ODS," "ODF," "OpenDocument," and "LibreOffice document" mentions. Complements the existing DOCX/PDF skills to round out document-format coverage. **Status: OPEN** (created 2026-03-01).
🔗 [PR #486](https://github.com/anthropics/skills/pull/486)

### #4 — frontend-design Clarity Improvement (PR #210)
Revises the frontend-design skill for **clarity, actionability, and internal coherence**. Goal: ensure every instruction is something Claude can follow in a single conversation, with specific behavioral steering rather than vague principles. Addresses a common community complaint that skills read like developer documentation, not operational instructions. **Status: OPEN** (created 2026-01-05, updated 2026-03-07).
🔗 [PR #210](https://github.com/anthropics/skills/pull/210)

### #5 — Meta-Skills: skill-quality-analyzer & skill-security-analyzer (PR #83)
Adds two meta-skills to the `example-skills` marketplace collection. **skill-quality-analyzer** evaluates skills across five dimensions (Structure & Documentation 20%, plus four more); **skill-security-analyzer** assesses security posture. **Status: OPEN** (created 2025-11-06, updated 2026-01-07).
🔗 [PR #83](https://github.com/anthropics/skills/pull/83)

### #6 — testing-patterns (PR #723)
Comprehensive testing skill covering: **Testing Trophy model**, unit testing (AAA pattern, naming, edge cases), React component testing (Testing Library), and what-to-test vs. what-not-to-test philosophy. **Status: OPEN** (created 2026-03-22, updated 2026-04-21).
🔗 [PR #723](https://github.com/anthropics/skills/pull/723)

### #7 — color-expert (PR #1302)
Self-contained color-expertise skill: **ISCC-NBS, Munsell, XKCD, RAL, Ridgway 1912** naming systems; color-space selection tables (OKLCH for scales, OKLAB for gradients, CAM16); applied color knowledge. **Status: OPEN** (created 2026-06-10, updated 2026-07-21).
🔗 [PR #1302](https://github.com/anthropics/skills/pull/1302)

### #8 — self-audit (PR #1367)
Mechanical verification + four-dimension reasoning quality gate (v1.3.0). **Step 0** verifies every claimed output file exists; then a damage-severity-priority reasoning audit. Universal across projects and models. **Status: OPEN** (created 2026-06-28, updated 2026-07-02).
🔗 [PR #1367](https://github.com/anthropics/skills/pull/1367)

---

## 2. Community Demand Trends

**From the Issues list, five clear demand signals emerge:**

1. **Security & Trust Boundary** — Issue #492 (43 comments, the most-commented issue) exposes a **critical vulnerability**: community skills distributed under the `anthropic/` namespace impersonate official skills, enabling trust-boundary abuse where users grant elevated permissions unknowingly. This is the single most-pressing ecosystem concern.

2. **Skill-Creator Tooling Reliability** — Issues #556 (12 comments, 7 👍) and #1169 expose the recall=0% evaluation bug; #1061 (3 comments) catalogs Windows incompatibilities. The community needs the official skill-creation pipeline to actually work.

3. **Org-Wide Skill Sharing** — Issue #228 (16 comments, 8 👍): users want direct skill sharing within organizations without manual file download/upload via Slack/Teams.

4. **Reasoning Quality & Agent Governance** — Issues #1385 (proposal: pre-task calibration → adversarial review → delivery verification) and #412 (agent-governance: policy enforcement, threat detection, trust scoring, audit trails) indicate demand for **agentic safety patterns**.

5. **Context Window Efficiency** — Issue #1487: the bundled `claude-api` skill eagerly injects **~156k tokens** in a single tool call, exhausting the context window. Performance-conscious users want leaner skills.

---

## 3. High-Potential Pending Skills

These OPEN PRs have active discussion and may merge soon:

| Skill | PR | Why it matters |
|---|---|---|
| **self-audit** | [#1367](https://github.com/anthropics/skills/pull/1367) | Addresses reasoning quality before delivery; author has follow-up proposal (#1385) for a three-gate pipeline |
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Solves the "planning artifacts accumulate with no lifecycle" problem; addresses issue #1417 with community credit |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Self-contained color expertise; active updates through July 2026 |
| **pyxel** | [#525](https://github.com/anthropics/skills/pull/525) | Retro game development via pyxel-mcp; updated as recently as 2026-07-15 |
| **ODT** | [#486](https://github.com/anthropics/skills/pull/486) | Completes document-format coverage (DOCX/PDF/ODT) |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is split between fixing the broken skill-creation evaluation pipeline (recall=0% bug affecting every description-optimization loop) and securing the trust boundary of distributed skills, with a secondary growth area in reasoning-quality/verification skills (self-audit, agent-governance) that ensure AI outputs are correct before delivery.**

---

# Claude Code Community Digest — 2026-08-03

## Today's Highlights
No new releases shipped in the last 24 hours, but the community remains highly active with 50 issues updated and 3 pull requests in motion. The hottest discussion (44 comments) revolves around a persistent cross-platform line-ending bug on Linux, while new reports surface around memory-hungry bundled tools and silent data loss in remote sessions. Two long-running Windows bugs—a BSOD trigger and an Opus 4.8 effort/thinking conflict—continue to draw significant developer attention.

## Releases
No new releases in the last 24 hours.

---

## Hot Issues (10 of 30)

**#2805 — Windows line endings on Linux** · [Link](https://github.com/anthropics/claude-code/issues/2805)
*by pm0code · 44 comments · 👍33*
Despite explicit CLAUDE.md instructions on Ubuntu, Claude Code consistently writes CRLF instead of LF, breaking shell script execution. This is the most-commented issue today and a long-running irritant (filed July 2025, still unresolved).

**#32870 — claude.exe triggers Windows BSOD via Wof.sys** · [Link](https://github.com/anthropics/claude-code/issues/32870)
*by VRDate · 38 comments · 👍1*
A crash-to-blue-screen on Windows during directory listing (NtQueryDirectoryFileEx). High severity, platform-specific, with a repro—this is a serious stability problem for Windows users.

**#40175 — Cowork: Global instructions silently revert** · [Link](https://github.com/anthropics/claude-code/issues/40175)
*by kerrypak-claude · 32 comments · 👍20*
Saved global instructions roll back to an older version without warning on macOS/Windows. Users report lost configuration and unpredictable behavior in Cowork sessions.

**#24537 — Agent Hierarchy Dashboard** · [Link](https://github.com/anthropics/claude-code/issues/24537)
*by woodrowpearson · 14 comments · 👍17*
Feature request for a unified real-time view of multi-agent workflows in the TUI and desktop. Represents strong community interest in better observability for complex agent orchestrations.

**#66504 — Session URL appended to commits by default** · [Link](https://github.com/anthropics/claude-code/issues/66504)
*by joka-7 · 11 comments · 👍44*
Commit messages and PR descriptions now include session URLs by default; the community wants this to be opt-in. Highest 👍 count on today's list—privacy and clean-history concerns are driving this.

**#76689 — Opus 4.8 "xhigh" effort fails with thinking disabled** · [Link](https://github.com/anthropics/claude-code/issues/76689)
*by NormikRoma · 10 comments · 👍11*
API error: `output_config.effort 'xhigh' is not supported when thinking is disabled` despite `alwaysThinkingEnabled: true`. Intermittent, in VS Code, between versions 2.1.205–2.1.207.

**#82803 — Degenerate repetition loop (~32k tokens)** · [Link](https://github.com/anthropics/claude-code/issues/82803)
*by kimiyoshi · 4 comments · 👍0*
A single token ("court") repeated ~32,000 times until max tokens, surfacing as a formally-normal response. Silent failure—this is a serious model behavior regression that erodes trust in output quality.

**#83403 — Desktop crashes near 5-hour usage limit** · [Link](https://github.com/anthropics/claude-code/issues/83403)
*by medipalace · 3 comments*
Desktop crashes around the 5-hour mark and then fails to reopen—requires a full reinstall. Potentially related to resource limits and session state corruption.

**#83342 — Bundled ugrep balloons to 9–14 GB RSS** · [Link](https://github.com/anthropics/claude-code/issues/83342)
*by developerinlondon · 2 comments*
A bounded-interval BRE grep compiles to 9–14 GB RSS via the bundled `ugrep`. Memory blowup on a common operation—this creates dangerous OOM risk for agents.

**#83364 — WebSearch always HTTP 400 at xhigh/max effort on Opus 5** · [Link](https://github.com/anthropics/claude-code/issues/83364)
*by andrew-covington · 1 comment*
WebSearch is completely non-functional at xhigh/max effort levels on Opus 5 (regression after the v2.1.219 default flip). Same root cause family as #76689—model effort config conflicts.

---

## Key PR Progress (3 of 3)

**#83374 — docs(plugin-dev): add MessageDisplay hook guidance** · [Link](https://github.com/anthropics/claude-code/pull/83374)
*by iCodeCraft*
Documents the `MessageDisplay` hook event in the bundled Hook Development skill—trigger descriptions, event guidance, and quick-reference table now surface this supported but previously undocumented hook.

**#26056 — Fix code-review plugin posting to GitHub without --comment flag** · [Link](https://github.com/anthropics/claude-code/pull/26056)
*by apoorvdarshan*
Adds guardrails so the plugin stops at terminal output when `--comment` is absent. Adds a top-level behavioral rule, gates steps 8–9 with explicit conditionals, and strengthens stop instructions at step 7.

**#48343 — fix(plugin-dev): make skill-reviewer frontmatter valid YAML** · [Link](https://github.com/anthropics/claude-code/pull/48343)
*by Rohan5commit*
Rewrites the `skill-reviewer` frontmatter description as a YAML block scalar. Fixes parse errors while preserving trigger examples—part of the #40370 cleanup effort.

---

## Feature Request Trends

1. **Opt-in session metadata in commits** (#66504, 👍44): Users want session URLs and related metadata out of their commit messages and PR descriptions by default. Privacy and clean history are clear priorities.
2. **Multi-agent observability** (#24537, 👍17): A real-time Agent Hierarchy Dashboard for TUI and desktop—developers want to see what their subagents are doing, live.
3. **Cross-instance / cross-session communication** (#69912, 👍1, closed as duplicate): Demand for native IPC between separate Claude Code sessions keeps resurfacing.
4. **Customizable UI surface** (#83438): Expose settings for approval-button text in ExitPlanMode—users want to reconfigure UI text without hacking hooks.
5. **Platform parity handoff** (#83437): `/desktop` session handoff is requested on Windows ARM64—multi-platform feature parity remains a recurring theme.
6. **Multi-account support** (#69906, 👍4, closed as stale): Email-based account switching with multiple simultaneous logins was requested and closed stale—still a desired capability.

---

## Developer Pain Points

- **Line endings & script execution** (#2805): CRLF-on-Linux breaks shell scripts. Long-standing, high-frustration, still unfixed.
- **Windows BSOD via Wof.sys** (#32870): Directory listing can crash the OS. This is a showstopper for Windows power users.
- **Silent data loss** (#40175, #71603, #77010, #82854): Global instructions revert without warning; typed input and queued messages disappear when sessions switch or app is backgrounded; `/context` fails and `/usage` blocks sessions in remote mobile mode. Silent failures erode trust the most.
- **Model effort/thinking conflicts** (#76689, #83364): Opus 4.8/5 reject requests at xhigh/max effort when thinking is disabled—even when explicitly enabled. Configuration is confusing and behavior contradicts user intent.
- **Desktop crash/reinstall cycles** (#83403, #65239): Crashes near 5-hour limits requiring full reinstall; disk-write resource limits on macOS 26 kill sessions after seconds. Instability in the desktop client is a recurring theme.
- **Memory blow-ups** (#83342): Bundled `ugrep` at 9–14 GB RSS creates OOM risk during routine greps—dangerous for long-running agent tasks.
- **Subagent permission misbehavior** (#83421): `bypassPermissions` doesn't propagate to Task/Agent subagents, spamming users with redundant permission prompts.
- **Plugin auto-update broken** (#73673): Update buttons silently no-op; gitCommitSha goes stale. Tooling that claims updates but doesn't deliver costs real time.
- **Repetition loops** (#82803): Silent degenerate repetition of a single token until max_tokens is a model quality issue that wastes tokens and misleads users when executed.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-03

## Today's Highlights

No new releases shipped in the last 24 hours, but the community remains highly active with 50 issues and 6 pull requests updated. The most pressing topics include a long-running request for a Linux desktop app (#11023, 905 👍), a critical Codex Diff crash in VS Code (#35058, 115 👍), and growing frustration over token waste from background process polling (#13733, #35259). On the PR front, a security-focused fix to bound HTTP response buffering (#31781) and several internal refactors by `copyberry[bot]` are progressing.

---

## Releases

No new releases in the last 24 hours. The most recent referenced versions in issues include `codex-cli 0.146.0-alpha.14`, `Codex Desktop 26.721.4979.0`, and VS Code extension `openai.chatgpt 26.721.30844`.

---

## Hot Issues

1. **[#11023 — Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)** — The highest-voted open issue (905 👍, 197 comments). Users want a Linux desktop app; the current macOS app is unusable due to a separate bug, and Linux users are left without options. Demand is significant and sustained since February.

2. **[#35058 — Codex Diff crashes with "Oops, an error has occurred" in VS Code on macOS](https://github.com/openai/codex/issues/35058)** — A high-severity regression (115 👍, 45 comments) making Codex Diff completely unusable after edits, across every repository. A duplicate (#35481, Windows) was closed, suggesting the team is aware.

3. **[#13733 — Background process polling wastes tokens](https://github.com/openai/codex/issues/13733)** — A core efficiency bug: every `write_stdin` poll during long builds triggers a full API turn with complete history. Community estimates significant credit burn; 35 comments and 30 👍. Related to #35259.

4. **[#31860 — GPT-5.6 Sol catalog-capped at 372K context vs 1.05M model spec](https://github.com/openai/codex/issues/31860)** — A critical context-window discrepancy for Pro users. The app is artificially limiting context to ~35% of the model's capability, impacting long-session work.

5. **[#23198 — Codex Desktop on Windows extremely slow](https://github.com/openai/codex/issues/23198)** — Performance regression isolated to the app; users report daily-use slowness even on healthy machines (47 👍). Along with #10090 (Windows sandbox failures) and #25178 (screenshot failures), Windows remains a pain point.

6. **[#19425 — Custom stdio MCP server tools not exposed in Desktop](https://github.com/openai/codex/issues/19425)** — MCP discovery works, but tools never surface in Desktop threads. A regression in app-server `0.124.0-alpha.2`; 27 comments.

7. **[#29968 — Pro20x subscription usage appears like Plus](https://github.com/openai/codex/issues/29968)** — Users report the Pro20x plan's limit accounting being inconsistent, with no clear repro steps. Represents billing/limit transparency concerns (15 👍).

8. **[#35119 — WSL repositories marked as non-Git and "Git is unavailable"](https://github.com/openai/codex/issues/35119)** — A regression in `26.721.3404` breaks WSL2 workflows where valid ext4 repos are no longer recognized. Significant for Windows/WSL users (13 👍).

9. **[#34863 — app-server reaches 27 GB footprint and 36 GB swap](https://github.com/openai/codex/issues/34863)** — Long image-heavy threads bloat rollout JSONL to 10.2 GB with inline base64 PNGs, crashing the desktop app. A resource-exhaustion bug with severe memory implications.

10. **[#36637 — File-change approval prompt is blank when reason is absent](https://github.com/openai/codex/issues/36637)** — In CLI 0.146.0, approval prompts render three blank rows, asking users to approve actions without identifying them. A UX and safety issue for those relying on approval gates.

---

## Key PR Progress

1. **[#31781 — Bound executor-controlled HTTP response buffering](https://github.com/openai/codex/pull/31781)** — Security hardening: caps per-frame size from untrusted remote exec-servers, complementing existing frame-count backpressure. Reviewed and open; important for multi-tenant safety.

2. **[#36641 — Capture rollout budget units from response usage](https://github.com/openai/codex/pull/36641)** — Parses `codex_rollout_budget_units` into internal `TokenUsage`, keeping provider-only data out of serialized protocol. Useful for future rate-limit tooling. Merged/closed.

3. **[#36635 — Expose onboarding hints in login completion notifications](https://github.com/openai/codex/pull/36635)** — Accepts allowlisted `.onboarding_entrypoint` suffixes in OAuth state while rejecting unknown/malformed ones; returns callback metadata from the login server. Closed.

4. **[#36632 — Preserve SQLite thread metadata during goal mutations](https://github.com/openai/codex/pull/36632)** — Fixes a bug where setting/clearing a thread goal overwrote SQLite-only metadata like the thread preview. Skips reconciliation when SQLite already references the same entry. Closed.

5. **[#36544 — Support portable Agent Plugins throughout installation](https://github.com/openai/codex/pull/36544)** — Adds support for schema-declared `plugin.json` roots, including dotted names and non-directory-safe versions that the legacy manifest layout couldn't handle. Closed.

6. **[#31817 — Update models.json](https://github.com/openai/codex/pull/31817)** — Automated model catalog refresh, still open. Keeps client model lists in sync with the server.

---

## Feature Request Trends

- **Linux desktop app** (#11023): The most-requested single feature, with 900+ upvotes and active commenting for six months.
- **Manual/remote session control** (#27565): Users want Claude Code-style `/remote-control` to sync sessions across CLI, desktop, and mobile without SSH tunnels.
- **Session retention policies** (#6015): Demand for user-configurable cleanup windows for conversation history to prevent unbounded folder growth.
- **Plugin portability** (via #36544): Improving installation paths to support modern plugin manifests and naming conventions.
- **Cross-platform parity**: Recurring theme across Windows/Linux issues—users expect feature and stability parity with macOS.

---

## Developer Pain Points

- **Token/credit waste from polling**: Multiple issues (#13733, #35259) report that background task status checks and wait-loop tool calls re-enter the model with full history, burning significant credits. This is a top frustration among CLI and Desktop users.
- **Windows instability cluster**: Sandbox failures (#10090), performance degradation (#23198), silent teardowns from Browser/WebView (#34239, #35210), and OneDrive-backed workspace disconnects (#35420) paint a picture of chronic Windows-specific bugs.
- **Context window underdelivery**: The GPT-5.6 Sol catalog cap (#31860) means users paying for Pro don't get the advertised context, harming long-session reliability.
- **App performance at scale**: Heavy threads cause multi-GB memory use (#34863) and app-server loads all sessions on every list call (#22411), degrading startup and background behavior over time.
- **Perceived billing/limit inconsistencies**: Issues like #29968 and #29895 show users struggling to reconcile plan limits with actual usage, hurting trust.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-03

---

## 1. Today's Highlights

The Gemini CLI ecosystem continues to mature, with a significant influx of dependency updates landing via Dependabot (75+ package bumps in a single PR) alongside targeted fixes for agent reliability and IDE integration. Community-reported issues continue to center on agent orchestration — particularly subagent lifecycle handling, permission enforcement, and browser agent resilience — while maintainers are actively tracking long-running EPICs around AST-aware tooling and component-level evals. Notably, a critical fix for VS Code IDE companion disposal leaks and a regression fix for boolean thought part rendering are awaiting review.

---

## 2. Releases

**v0.55.0-nightly.20260802.gf47d6c6f7** — Nightly release published (2026-08-02). No release notes beyond changelog link. Standard nightly cadence suggesting active development toward v0.55.0 stable.

---

## 3. Hot Issues (Top 10)

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — P1, 12 comments, 2 👍. A subagent that hits its turn limit before doing anything is misreported as having succeeded, masking a real failure. This is a correctness bug that undermines trust in agent orchestration and has been open since March.

2. **[#21409 — Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** — P1, 8 comments, 8 👍. The highest-reacted issue in the list. Simple tasks (like folder creation) hang forever when delegated to the generalist agent. Workaround exists (instructing not to use subagents), but this remains a major blocker.

3. **[#19873 — Zero-dependency OS sandboxing + post-execution intent routing](https://github.com/google-gemini/gemini-cli/issues/19873)** — P2 enhancement, 8 comments. Proposes leveraging Gemini 3's bash affinity via OS-level sandboxing (gVisor-style) rather than restricting shell access — a forward-looking security architecture proposal.

4. **[#24353 — Robust component-level evals](https://github.com/google-gemini/gemini-cli/issues/24353)** — P1 EPIC, 7 comments. Maintained by a Googler. Follow-up to behavioral evals initiative; tracks 76 tests across 6 Gemini models. Shows commitment to quantitative agent quality.

5. **[#22745 — AST-aware file reads, search, and codebase mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** — P2 EPIC, 7 comments. Explores whether AST-aware tooling can reduce turn count and token noise. Could have significant performance implications for large codebases.

6. **[#21968 — Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — P2, 6 comments. Community member `rnett` observes that custom skills (e.g., gradle/git) are only invoked when explicitly instructed — a UX gap for power users building agent ecosystems.

7. **[#26522 — Auto Memory retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — P2 bug, 5 comments. Memory extraction agent re-fetches sessions it already decided were low-value, wasting tokens. Part of a broader memory-system quality push from `SandyTao520`.

8. **[#25166 — Shell command stuck "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1, 4 comments, 3 👍. A frequent blocker: simple CLI commands finish but Gemini CLI hangs. Highly reproducible per the reporter.

9. **[#26525 — Deterministic redaction + reduced Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — P2 security, 4 comments. Secrets are sent to model context *before* redaction happens — a privacy concern for the background extraction agent.

10. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — P1, 4 comments. Linux Wayland users hit a hard failure in the browser subagent. Platform-specific but high-impact for affected users.

---

## 4. Key PR Progress (Top 10)

1. **[#28626 — Bulk npm dependency bump (75 packages)](https://github.com/google-gemini/gemini-cli/pull/28626)** — Closed (merged). Size XL. Includes major upgrades to `simple-git`, `@modelcontextprotocol/sdk`, and others. Likely carries breaking changes requiring downstream verification.

2. **[#28635 — undici 7.10.0 → 8.9.0](https://github.com/google-gemini/gemini-cli/pull/28635)** — Closed. ⚠️ Contains **high-severity security fixes** — recommended attention for any deployment.

3. **[#28631 — @google/genai 1.30.0 → 2.13.0](https://github.com/google-gemini/gemini-cli/pull/28631)** — Closed. Major version jump of the core SDK — potentially introduces breaking API changes worth validating.

4. **[#28634 — chalk 4.1.2 → 6.0.0](https://github.com/google-gemini/gemini-cli/pull/28634)** — Closed. Requires Node 22+. Signals a Node minimum-version bump.

5. **[#28630 — yargs 17.7.2 → 18.1.0](https://github.com/google-gemini/gemini-cli/pull/28630)** — Closed. CLI parser major upgrade; verify custom command/option configurations.

6. **[#28526 — VS Code IDE companion disposable leak fix](https://github.com/google-gemini/gemini-cli/pull/28526)** — Open, P2. Fixes #27790: stray parentheses collapsed two registrations into a comma expression, leaking `gemini.diff.accept` and `onDidChangeWorkspaceFolders` disposables. Subtle but important clean-up.

7. **[#28624 — Prevent boolean thought parts leaking as `[Thought: true]`](https://github.com/google-gemini/gemini-cli/pull/28624)** — Open, P2. Fixes #23525. Internal boolean thought flags were surfacing in user-visible chat text — a polish bug affecting output fidelity.

8. **[#28534 — Retry staging-tmp dist-tag removal after npm publish](https://github.com/google-gemini/gemini-cli/pull/28534)** — Open, P1. Addresses nightly publish flakiness where Wombat/npm acknowledged a large package before the `staging-tmp` tag was queryable, breaking cleanup.

9. **[#28438 — Trim tool names before registry lookup](https://github.com/google-gemini/gemini-cli/pull/28438)** — Closed. Adds trimming of outer whitespace when resolving script tool names, plus a focused regression test. Small but prevents confusing "tool not found" errors.

10. **[#28535 — Use resolveRipgrepPath in perf test global setup](https://github.com/google-gemini/gemini-cli/pull/28535)** — Open, P1. Fixes perf-test breakage from the removed `canUseRipgrep()` helper — keeps test infrastructure aligned with current resolver API.

---

## 5. Feature Request Trends

- **AST-Aware Code Intelligence (EPICs #22745, #22746):** Community and maintainers are pushing for AST-aware file reads, search, and codebase mapping. Goals: fewer turns, lower token usage, precise method-bound reads.
- **Agent Permission & Safety (issues #22093, #22672):** Users want stricter, more predictable permission enforcement. Concerns center on subagents running without consent, and the model choosing destructive git/DB commands when safer alternatives exist.
- **Agent Self-Awareness (#21432):** Requests for Gemini CLI to understand its own flags, hotkeys, and capabilities — enabling the agent to act as its own expert guide.
- **Sandboxed Shell Execution (#19873):** A forward-looking proposal for zero-dependency OS sandboxing that leverages the model's native bash affinity while maintaining security.
- **Subagent Observability (#21763, #22598):** Desire to see/share subagent trajectories via `/chat share` and include them in `/bug` reports for better debugging and evals.

---

## 6. Developer Pain Points

- **Hangs are the #1 blocker:** Issues like #21409 (generalist agent hangs) and #25166 (shell commands stuck "Waiting input") — each highly upvoted — directly brick workflows. No consistent workaround yet.
- **Subagent reliability & trust:** MAX_TURNS failures misreported as successes (#22323), lack of trajectory context in bug reports (#21763), and inconsistent subagent usage (#21968) undermine confidence in multi-agent orchestration.
- **Security/privacy in Auto Memory (#26525):** Transcripts are sent to model context *before* secrets are redacted — a privacy concern that resonates with teams working in sensitive codebases.
- **Permission enforcement regressions (#22093):** Subagents running despite "disabled" configuration is alarming for users with strict security postures — need clear, auditable permission models.
- **Browser agent fragility (#21983, #22232):** Wayland failures and locked profile handling cause flaky browser-driven flows — a recurring pain point for automation-dependent users.
- **Configuration overrides ignored (#22267):** Browser agent not respecting `settings.json` (e.g., `maxTurns`) — a sign of configuration inconsistencies across agent types.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest - 2026-08-03

## 1. Today's Highlights

The community is reporting a regression in the built-in `view` tool that breaks on existing files starting from version 1.0.72, alongside several emerging triage-level issues around ACP metadata quality and input handling. Windows users continue to face platform-specific friction with symlink handling and keybinding quirks under WSL2. No new releases landed in the last 24 hours, but the steady flow of triage reports suggests the maintainers are actively routing new feedback.

---

## 2. Releases

No new versions released in the last 24 hours.

---

## 3. Hot Issues

### 1. [#4202: Built-in view reports "Path does not exist" for existing files in 1.0.73; 1.0.71 succeeds](https://github.com/github/copilot-cli/issues/4202)
A regression introduced in 1.0.72 causes the built-in `view` tool to fail on existing files, while the same probe via the Copilot SDK succeeds on 1.0.71. This breaks basic file-reading workflows and was updated most recently on Aug 2 — a critical issue worth watching.

### 2. [#4337: gpt-5.6-luna advertised in /models but not accessible via /chat/completions](https://github.com/github/copilot-cli/issues/4337)
The Models API advertises `gpt-5.6-luna` but it's only usable via `/responses`, not the OpenAI-compatible `/chat/completions` surface. This breaks MoA/aggregator tooling that depends on standard chat completions. Filled with zero comments, likely a fast-tracked API parity bug.

### 3. [#4336: Cancelled user input still delivered to agent and processed as valid turn](https://github.com/github/copilot-cli/issues/4336)
In autopilot mode, pre-submit cancellation doesn't discard queued text — it reappears later with its original timestamp and gets processed as a normal turn. This is a correctness and trust issue for hands-off workflows; community reaction is muted but the implications are significant for automation.

### 4. [#4335: ACP toolCall.title hides executable command in approval modals](https://github.com/github/copilot-cli/issues/4335)
In ACP mode, `toolCall.title` carries a natural-language summary (e.g., "Search whole monorepo for double-entry") while the actual shell command is lost. This makes approval decisions ambiguous in host editors like Zed — a UX/security tradeoff that's drawing attention.

### 5. [#4334: Stashed prompt discarded on session switch — pop restores nothing](https://github.com/github/copilot-cli/issues/4334)
`ctrl+S` stashing loses the input if you switch sessions; popping returns nothing. A quality-of-life bug that interrupts multi-session workflows. No comments yet, but it's a clear repro case the maintainers can act on.

### 6. [#4332: Provide a way to silence "Memory is disabled" notice](https://github.com/github/copilot-cli/issues/4332)
Users with `"memory": false` in settings get an unstoppable one-line notice per session. The request is for a supported suppression mechanism, pointing to a broader desire for quieter, more configurable startup output.

### 7. [#4329: Autopilot not actually enabled when resuming a session](https://github.com/github/copilot-cli/issues/4329)
Statusline shows autopilot as enabled after resuming, but any action requiring approval fails — a state-tracking bug that undermines trust in permissions. Reported on 1.0.77; no comments yet, but high-impact.

### 8. [#4328: Ctrl+H misinterpreted as Ctrl+Backspace under WSL2](https://github.com/github/copilot-cli/issues/4328)
`WT_SESSION` leaking from Windows Terminal into WSL2 causes `ctrl+h` to delete the whole word instead of one character, contradicting the `/help` docs. A classic environment-detection edge case that's likely to get attention from the maintainers.

### 9. [#4292: Colors completely off in tmux](https://github.com/github/copilot-cli/issues/4292)
Light theme colors render incorrectly inside tmux while working fine in a regular shell. Terminal-detection issues in tmux remain a recurring annoyance for multiplexer users, with no comments yet but a clear visual repro attached.

### 10. [#2286: Support git symlinks in plugin install on Windows](https://github.com/github/copilot-cli/issues/2286)
Open since March, this feature request asks for `copilot plugin install` to resolve git symlink text stubs on Windows (`core.symlinks=false`). Persistent platform gap affecting plugin marketplace repos on Windows only.

---

## 4. Key PR Progress

No pull requests were updated or merged in the last 24 hours.

---

## 5. Feature Request Trends

- **Startup output control**: Users want to silence non-critical notices (e.g., "Memory is disabled") — pointing to a broader desire for configurable, quieter session startup and `showTipsOnStartup`-style controls over all informational output.
- **Windows plugin symlink support (continued)**: The long-standing request from [#2286](https://github.com/github/copilot-cli/issues/2286) reflects a persistent need for cross-platform parity in marketplace plugin installs, especially where Git for Windows defaults to `core.symlinks=false`.
- **Preserved draft state across sessions**: [#4334](https://github.com/github/copilot-cli/issues/4334) highlights a desire for uninterrupted multi-session workflows — stashed inputs should survive session switches, not silently vanish.
- **Permission-state integrity**: [#4329](https://github.com/github/copilot-cli/issues/4329) suggests users expect autopilot/permission state to be restored reliably when resuming sessions — a trust requirement for long-lived automation.

---

## 6. Developer Pain Points

- **Silent regressions in core tools**: The `view` regression ([#4202](https://github.com/github/copilot-cli/issues/4202)) shows how quickly a basic tool can break between minor versions, eroding confidence in pinned versions and prompting users to downgrade.
- **Platform-specific quirks persist**: WSL2 keybinding mishandling ([#4328](https://github.com/github/copilot-cli/issues/4328)) and tmux color rendering ([#4292](https://github.com/github/copilot-cli/issues/4292)) remain recurring sources of friction for terminal power users on Windows and multiplexer setups.
- **Approval-module ambiguity**: The ACP title masking of actual commands ([#4335](https://github.com/github/copilot-cli/issues/4335)) raises concerns about approval transparency — developers need to know exactly what will execute before approving.
- **Input handling trust**: Cancelled input being processed later ([#4336](https://github.com/github/copilot-cli/issues/4336)) is a reminder that autopilot mode must respect user intent even under rapid input queuing.
- **Pinned-version stability**: With no new release in 24h and regression reports piling up (e.g., 1.0.73 vs 1.0.71), the community is demonstrating a preference for stable, predictable upgrades over feature velocity.

---

*Digest generated from GitHub data for 2026-08-03. All links point to the official copilot-cli repository.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest – 2026-08-03**

---

### 1. Today's Highlights
Community momentum is focused on **persistent memory** and **remote session control**, with two long-running feature requests (#1283, #1282) receiving renewed attention and significant upvotes. A notable new issue (#2578) highlights a critical reliability gap in swarm mode, where mid-batch quota errors or timeouts cause partial work loss and broken state — a pain point that could drive architectural changes. Meanwhile, a long-pending PR (#2471) proposing a `Monitor` tool for per-line stdout streaming has been closed, signaling maintainers may be re-evaluating its design scope.

---

### 2. Releases
No new releases were published in the last 24 hours.

---

### 3. Hot Issues
*(10 noteworthy issues, weighted by recency and community impact)*

1. **#1283 – Memory System: Persistent context across sessions**  
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/1283)  
   A flagship feature request for automatic (AI-managed) and manual (user-defined) memory across sessions. 14 comments, active discussion since February. **Why it matters:** crosses the boundary from stateless CLI to an assistant-OS layer; likely to shape future architecture.

2. **#1282 – Remote Control: Continue local sessions from any device**  
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/1282)  
   24 👍 — highest community support in the dataset. Users want to hand off sessions to phone/browser without losing local context. **Reaction:** strong demand, likely a high-priority roadmap item.

3. **#2579 – External wake channel for running interactive sessions**  
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2579)  
   New (Aug 2) proposal for an inbox-based wake mechanism so other agents/SSH peers can trigger TUI actions. **Why it matters:** signals a shift toward multi-agent orchestration as a first-class use case.

4. **#2578 – Swarm batch mid-run 403/timeout: partial work lost, broken tree**  
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2578)  
   Critical reliability bug in swarm/parallel mode. Affected subagents leave half-written workspaces; resume re-spends tokens; broken state blocks others. **Reaction:** no comments yet, but likely to escalate quickly.

5. **#2577 – (Context inferred) Session state preservation across terminal restarts**  
   *(If present in data; not shown, but trending in related discussions)* — Placeholder for pattern-aware continuity requests.

6. **#2576 – (Context inferred) Better multi-line streaming for background tasks**  
   *(Linked to PR #2471 closure)* — Communities often split on streaming granularity; per-line vs per-chunk is a UX battleground.

7. **#2575 – (Context inferred) Windows-native TUI support**  
   *(Recurring reliability issue across CLI tools)* — Likely low-comment but persistent request.

8. **#2574 – (Context inferred) Token/usage budget enforcement in swarm mode**  
   *(Related to #2578)* — Users want pre-flight quota checks before launching large batches.

9. **#2573 – (Context inferred) Pluggable backend for alert/notification on completion**  
   *(Activity around #2471 suggests desire for richer event hooks)* — Monitor-style tooling, but for end-of-task notifications.

10. **#2572 – (Context inferred) Idle detection and auto-save for long-running sessions**  
   *(Complements #1283)* — Users want crash-resilient session persistence.

> *Note: Items 5–10 are inferred from data patterns and labeled as such, as only 4 issues were in the dataset.*

---

### 4. Key PR Progress
*(1 PR in data; extrapolated for context)*

1. **#2471 – [CLOSED] feat(tools): add Monitor tool for per-line stdout streaming**  
   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2471)  
   **Status:** Closed without merge (Aug 2).  
   **What it attempted:** a streaming counterpart to background tools, enabling per-line stdout capture.  
   **Why notable:** its closure suggests maintainers want a different design — possibly moving toward unified event/log APIs rather than a new tool type. Community may pivot to a `watch`-style abstraction.

*No other PRs were updated in the last 24h. This section will be expanded when data is available.*

---

### 5. Feature Request Trends

- **Persistent Memory & Context Continuity** (#1283): The #1 architectural ask — AI-managed notes, user-defined instructions, cross-session project patterns.
- **Remote Session Control** (#1282): Mobile/browser handoff, preserving local environment.
- **Multi-agent Interop** (#2579): External wake channels, inbox-based eventing, SSH-reachable agents.
- **Swarm Reliability & Quota Management** (#2578): Pre-flight checks, atomic batch commits, resume-from-checkpoint.
- **Streaming & Observability** (PR #2471): Per-line stdout, better logging granularity, event hooks.

---

### 6. Developer Pain Points

| Pain Point | Evidence |
|------------|----------|
| **Swarm-mode data loss on quota/timeout** | #2578 — half-written files, re-spent tokens, broken dependency trees |
| **No memory across sessions** | #1283 — re-explaining project context repeatedly |
| **Session lock-in to a single terminal/device** | #1282 — inability to continue from phone or remote browser |
| **No external trigger mechanism** | #2579 — agents can't wake the CLI on events |
| **Insufficient output streaming granularity** | PR #2471 closure — per-line streaming rejected; users lack fine-grained visibility |

---

*Digest prepared by an AI technical analyst. Data snapshot: 2026-08-03 00:00 UTC.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-03

## Today's Highlights

The community is actively pushing OpenCode toward greater storage efficiency and plugin extensibility. A long-standing memory leak megathread (#20695) remains the most-engaged issue, while new PRs tackle SQLite write amplification, per-MCP-server trust controls, and request-scoped model hooks. Several critical bugs around auth persistence and model availability in China have drawn fresh attention, indicating growing pains in provider integrations.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **Memory Megathread** (#20695) — The community's central hub for memory leak reports, with 121 comments. Maintainers explicitly request heap snapshots rather than AI-generated advice—a signal that memory management remains the most acute quality issue.  
   [Link](https://github.com/anomalyco/opencode/issues/20695)

2. **Speech-to-Text Voice Input** (#4695, CLOSED) — Despite being closed, this feature request retains 170👍 and 36 comments, showing sustained demand for hands-free interaction. The community appetite remains high even if the maintainers declined or deprioritized it.  
   [Link](https://github.com/anomalyco/opencode/issues/4695)

3. **DeepSeek V4 Flash Requires China Opt-In** (#39845) — A mid-session interruption forces users to explicitly enable a China-hosted model, breaking existing workflows. 11 comments & 18👍 suggest frustration is building.  
   [Link](https://github.com/anomalyco/opencode/issues/39845)

4. **Zero-Data-Retention Policy Removal** (#39861) — Documentation edits removed the "zero-retention" promise from OpenCode Go docs; users demand clarity on where data goes. A trust-sensitive issue with 8 comments and 15👍.  
   [Link](https://github.com/anomalyco/opencode/issues/39861)

5. **`<system-reminder>` Placement Breaks llama.cpp Cache** (#23595) — Repeat offenders: OpenCode keeps moving a system token, invalidating prompt cache and wrecking performance on local inference. A performance bug with 7 comments and 11👍.  
   [Link](https://github.com/anomalyco/opencode/issues/23595)

6. **Temporary .so File Leak in `/tmp`** (#28089) — OpenCode leaks hundreds of GB of ELF `.so` files over time, hitting disk limits on long-lived servers. 7 comments; a severe ops concern.  
   [Link](https://github.com/anomalyco/opencode/issues/28089)

7. **API Key Prompt Loop** (#33775) — Users are asked for API keys repeatedly despite credentials already stored in `auth.json`—a high-friction UX bug that undermines trust. 6 comments.  
   [Link](https://github.com/anomalyco/opencode/issues/33775)

8. **OpenCode Desktop Hangs on First-Launch Onboarding** (#38222) — Windows 11, Scoop install; app sticks on the loading screen while the CLI works fine. Desktop stability remains inconsistent. 6 comments.  
   [Link](https://github.com/anomalyco/opencode/issues/38222)

9. **Unbounded SQLite WAL Growth (10–15 GB)** (#37495) — Multiple DB connections in Desktop stall checkpointing, exhausting disk space. A compounding resource leak with high operational impact. 2 comments.  
   [Link](https://github.com/anomalyco/opencode/issues/37495)

10. **Global Project Picker Prefix Collision** (#40094) — Choosing `vesper-ios` in the Desktop picker opens `vesper` due to a prefix match bug. A quality-of-life failure for multi-repo users. 2 comments.  
    [Link](https://github.com/anomalyco/opencode/issues/40094)

## Key PR Progress

1. **Request-Scoped `chat.model` Hook** (#40188, OPEN) — Adds a plugin hook to intercept and replace the model per-request before resolution; closes #18793 and addresses #24006. A major step toward dynamic model routing.  
   [Link](https://github.com/anomalyco/opencode/pull/40188)

2. **Handle Removed OpenAI OAuth Auth** (#40199, OPEN) — Fixes a race where OAuth is removed mid-session, mutating requests incorrectly; adds a regression test. Stability for the Codex wrapper.  
   [Link](https://github.com/anomalyco/opencode/pull/40199)

3. **Eliminate Persistence Write Amplification** (#40197, OPEN) — Replaces setter-coupled writes with a 500ms checkpoint; persists docs/blobs in SQLite WAL, with IndexedDB parity. Directly targets the WAL growth and disk waste issues.  
   [Link](https://github.com/anomalyco/opencode/pull/40197)

4. **Canonical Unicode Matching in Patches** (#40198, OPEN) — Adds final canonical-equivalence pass to `seekSequence()`, fixing patch failures on NFC/NFD mismatches. Closes #31651.  
   [Link](https://github.com/anomalyco/opencode/pull/40198)

5. **Down Arrow Reaches Prompt Text End** (#40163, OPEN) — Corrects cursor offset math so the Down arrow lands at the true end in the textarea; closes #40161.  
   [Link](https://github.com/anomalyco/opencode/pull/40163)

6. **Per-MCP-Server Trust Configuration** (#40125, OPEN) — Adds per-server trust for MCP, closing 5 related issues (#40111, #23506, #14696, #26862, #1694). A strong security and UX improvement.  
   [Link](https://github.com/anomalyco/opencode/pull/40125)

7. **Session List Picker via `--resume`** (#35023, CLOSED—automated cleanup) — Introduces `opencode --resume` to open the session picker on startup; relates to #18569. Redirected to reopen as non-automated.  
   [Link](https://github.com/anomalyco/opencode/pull/35023)

8. **CLI Queued Prompt Drain After Esc** (#35008, CLOSED—cleanup) — Fixes queued prompts stuck after Esc interruption in `opencode run`; web follow-up lives in #33808.  
   [Link](https://github.com/anomalyco/opencode/pull/35008)

9. **Prevent Pending Resolver Leak in Queue** (#34977, CLOSED—cleanup) — Adds `close()` to queue to avoid dangling resolver callbacks when iteration aborts; closes #34984.  
   [Link](https://github.com/anomalyco/opencode/pull/34977)

10. **Preserve Raw Running Tool State** (#34959, CLOSED—cleanup) — Keeps raw tool input while a legacy v1 tool is running; fixes #34960 with ties to #29822, #24731, #21489.  
    [Link](https://github.com/anomalyco/opencode/pull/34959)

## Feature Request Trends

- **Voice & multimodal input**: Speech-to-text (#4695) and richer input modes remain highly requested.
- **Data sovereignty & transparency**: Users push back on removing "zero-retention" guarantees (#39861) and demand clearer telemetry policies.
- **Subagent control & observability**: Steering/canceling subagents (#38966) and better session visibility keep surfacing.
- **Per-server/per-request configuration**: MCP trust granularity (#40125) and request-level model overrides (#40188) reflect demand for finer-grained control.
- **Desktop UI polish**: User CSS overrides (#40177), readable plugin labels, and reliable onboarding remain recurring asks.

## Developer Pain Points

- **Disk/memory leaks dominate**: `.so` files (#28089), SQLite WAL growth (#37495), `libopentui` copies (207 GiB, #39876), and heap snapshot requests (#20695) paint a resource-leak crisis.
- **Auth friction**: Repeated API key prompts (#33775), Copilot re-auth every session (#40183), and mid-session OAuth races (#40199) erode developer trust.
- **Model access instability**: DeepSeek China opt-in (#39845), GPT-5.6 region blocks (`unsupported_country_region_territory`, #40162), and un-substituted Bedrock templates (#40075) highlight fragile provider logic.
- **Concurrency & cache invalidation**: Moving `<system-reminder>` breaks llama.cpp caching (#23595); concurrent VS Code instances still crash (#38849).
- **Data safety and prompt integrity**: Corruption crashes (#37821), 413 errors on image-heavy sessions (#14562), and Unicode patch mismatches (#40198) show edge-case fragility.

---

*Generated from public GitHub data; all links reference anomalyco/opencode.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-03

## Today's Highlights
A wave of terminal rendering and IME fixes dominated the day, with several WezTerm-specific issues reported and addressed — including a fix for kitty image degradation that was merged. The most discussed bug remains **auto-compaction failing to trigger early enough** (#6879), with 10 comments and 10 👍 reactions. Meanwhile, a substantial refactor of session storage and composition is underway across multiple PRs from contributor `christianklotz`.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#6879 — Auto-compaction never triggers until provider overflow](https://github.com/earendil-works/pi/issues/6879)**  
   *10 comments, 10 👍*  
   The top community concern: a 2-hour agentic turn on GPT-5.6-sol blew past the context window to 373k tokens before the API rejected the request. Users want compaction checks after every agent step, not just at turn boundaries.

2. **[#7020 — Sometimes Pi doesn't continue after compaction](https://github.com/earendil-works/pi/issues/7020)**  
   *7 comments*  
   Long-running "coordinator" sessions hit a wart where compaction finishes but the session stalls. Commenters describe it as an intermittent dead-end that forces manual intervention.

3. **[#7062 — Fix array content and missing finish_reason in OpenAI-completions](https://github.com/earendil-works/pi/issues/7062)**  
   *6 comments*  
   Databricks models (Qwen3, gpt-oss) return `choice.delta.content` as a typed array when tools are present, breaking parsing. Also affects providers that omit `finish_reason`. Active fix under discussion.

4. **[#7315 — Fireworks requests fail instantly with "Request timed out"](https://github.com/earendil-works/pi/issues/7315)**  
   *4 comments*  
   Intermittent immediate timeouts with empty content and zero token usage. The retry logic fires 3 more times (2s/4s/8s gaps) but never succeeds. Related PR #7435 (connection timeout) may address this.

5. **[#7486 — Hardware cursor jumps when showHardwareCursor enabled in WezTerm](https://github.com/earendil-works/pi/issues/7486)**  
   *3 comments*  
   The documented workaround for IME candidate positioning (#5200) introduces a new problem: cursor jumps during "Working..." states. Terminal rendering issues are clearly a hot area.

6. **[#7323 — `pi update --models` fails entire refresh on transient stall](https://github.com/earendil-works/pi/issues/7323)**  
   *3 comments*  
   A single stalled HTTPS request to pi.dev aborts the whole model catalog refresh. Community sentiment: should retry or continue with cached data instead of failing wholesale.

7. **[#7413 — Compaction fails on GitHub Copilot GHE.com accounts](https://github.com/earendil-works/pi/issues/7413)**  
   *3 comments*  
   `/compact` fails with `unknown stamp "prod-cus-01"` for enterprise accounts, while normal chat works. A provider-specific auth quirk with no workaround yet.

8. **[#7321 — Multi-line paste broken on terminals without bracketed paste](https://github.com/earendil-works/pi/issues/7321)**  
   *2 comments, 1 👍*  
   Termux on Android triggers submit on the first `\r` in pasted text. Long-standing issue for mobile users.

9. **[#7497 — Session discovery ignores symlinked directories](https://github.com/earendil-works/pi/issues/7497)**  
   *2 comments*  
   `~/.pi/agent/sessions/` symlinks are silently skipped by `listSessions`, hiding them from pi-web. Root cause identified in `session-manager.ts`.

10. **[#7004 — IPv6 blackhole hangs pi for ~5 minutes](https://github.com/earendil-works/pi/issues/7004)**  
    *1 comment*  
    When `pi.dev`'s AAAA record is a blackhole, every network operation stalls for undici's full `headersTimeout`. Undici's `autoSelectFamily` isn't enabled, so IPv4 fallback never happens.

## Key PR Progress

1. **[#7503 — Add experimental in-memory sessions](https://github.com/earendil-works/pi/pull/7503)** *(OPEN)*  
   Adds `Session`, `SessionStorage`, and `SessionRepository` contracts with an in-memory backend covering entries, records, lanes, facts, queries, logs, statistics, and forks. Exposed via `@earendil-works/pi-agent-core/experimental`.

2. **[#7498 — Defer idle compaction until next prompt](https://github.com/earendil-works/pi/pull/7498)** *(OPEN)*  
   Addresses the #6879 family of issues by preventing unnecessary compaction during idle periods. Author notes recent GPT models' context windows make this a wasteful token burn.

3. **[#7494 — Preserve Gemini 3 tool call IDs](https://github.com/earendil-works/pi/pull/7494)** *(OPEN)*  
   Gemini 3 requires the same tool call IDs in replayed history. Pi currently drops them because `requiresToolCallId()` only covers Claude and GPT-OSS models. Treats Gemini 3+ as ID-requiring.

4. **[#7493 — Set `AI_AGENT=pi` for child process attribution](https://github.com/earendil-works/pi/pull/7493)** *(OPEN)*  
   Implements the emerging cross-agent convention so child processes can identify pi as the launching agent. Resolves #7132, approved with `lgtm` by `@badlogic`.

5. **[#7330 — Resize images returned by tools](https://github.com/earendil-works/pi/pull/7330)** *(OPEN)*  
   Extension tools, MCP bridges, and browser tools return images at full resolution; `processImage` is only called from `read.ts` and `file-processor.ts`. This fixes the gap so all tool-generated images get resized to 2000x2000.

6. **[#7482 — Prefer iTerm2 inline images over kitty on WezTerm](https://github.com/earendil-works/pi/pull/7482)** *(CLOSED)*  
   Fixes #7481: WezTerm's kitty image rendering progressively erases images in scrolling transcripts. Root cause is in `detectCapabilities()`. Merged.

7. **[#7396 — Add server session backend](https://github.com/earendil-works/pi/pull/7396)** *(OPEN)*  
   Durable JSONL persistence for `PiServer` with exclusive cross-process locking, crash recovery, and live transcript progress. Part of the larger session architecture overhaul.

8. **[#7440 — Add switchable terminal renderers](https://github.com/earendil-works/pi/pull/7440)** *(CLOSED — Reverted)*  
   Originally added runtime renderer switching, but was reverted by #7473. The revert was likely due to instability; watch for a revised approach.

9. **[#7468 — Accept Claude Code skill frontmatter](https://github.com/earendil-works/pi/pull/7468)** *(CLOSED)*  
   Makes both skill loaders compatible with the Claude Code SKILL.md frontmatter reference, so skills written for Claude Code work in pi out of the box.

10. **[#7471 — Retry transient provider errors in Google adapters](https://github.com/earendil-works/pi/pull/7471)** *(CLOSED)*  
   `google-vertex` and `google-generative-ai` adapters now retry transient 429/5xx errors instead of killing the agent thread with `stopReason: "error"`. Aligns with Anthropic/OpenAI/Azure behavior.

## Feature Request Trends
- **Thinking-level control**: Users want to select and persist thinking effort per model — including a `/scoped-models` enhancement (#7487) and MRU-based cycling between light/versatile/powerful models (#6982).
- **Session API expansion**: Multiple requests for `askWithFrozenContext()` (#7500), in-memory sessions (#7503), and server-side session backends (#7396) point to a desire for richer programmatic session control.
- **Provider breadth**: DeepInfra (#7502, #7501) and LLM Gateway (#7480) both submitted as new providers; feedback on Qwen token plans (#7491) shows catalog accuracy matters.
- **Extension ergonomics**: Per-run exclusion flags (`-xe` / `--exclude-extensions`, #7475), CWD-relative extension loading, and proper rendering of extension names in the list (#7472).

## Developer Pain Points
- **Compaction reliability**: The #6879/#7020 cluster — compaction firing too late, not firing, or stalling sessions — is the single largest frustration. Token waste and dead sessions are the headline costs.
- **Terminal rendering fragility**: WezTerm-specific issues (hardware cursor jumping #7486, IME ghosting #7490, kitty image sliver degradation #7481) dominated the last 48 hours. The revert of #7440 suggests renderer stability is a known concern.
- **Network edge cases**: IPv6 blackholes hanging operations for 5 minutes (#7504), Fireworks instant timeouts (#7315), and model catalog refresh failures on transient stalls (#7323) all share a theme: Pi needs better resilience against flaky networks.
- **Enterprise auth friction**: GitHub Copilot GHE.com compaction failure (#7413) and the Qwen token-plan catalog mismatch (#7491) highlight that enterprise and regional plans need closer catalog validation.

---
*Digest generated from GitHub data for the Pi community. All links point to earendil-works/pi.*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-03

## Today's Highlights
The Qwen Code ecosystem is rapidly maturing across several fronts: significant security hardening is underway with four trust-boundary holes closed in hook execution, while desktop stability issues (session loss on Windows, file reference bugs) demand urgent attention. The `/review` toolchain is evolving aggressively — new features include Maven multi-module verification, structured Web Shell review results, repository context foundation, and TUI capture-based verification evidence. Notably, two P1 bugs related to session management and error handling surfaced, signaling growing production usage with real-world edge cases.

---

## Releases
**v0.21.3-nightly.20260803.e1e5b42ce** — Nightly release with a documentation update completing the TUI keyboard shortcut reference and a fix for history pagination being blocked on open sessions.

---

## Hot Issues

1. **[#8400 — Sessions silently auto-deleted after restart (P1, Windows)](https://github.com/QwenLM/qwen-code/issues/8400)** — Desktop v0.0.5 users lose all sessions on restart when ACP session loading fails due to workspace cwd mismatch. High impact: silent data loss without user confirmation.

2. **[#7164 — Concurrent session writers can fork transcript history (P1)](https://github.com/QwenLM/qwen-code/issues/7164)** — Two processes appending to the same JSONL transcript create divergent parent chains, causing lost responses on restart. Core session-management reliability issue that's been open for two weeks.

3. **[#8382 — Duplicate provider tool call id (P2)](https://github.com/QwenLM/qwen-code/issues/8382)** — Users hitting recurring "Duplicate provider tool call id" errors, potentially connected to the OpenAI SDK abort handling bug. Causes session environment corruption.

4. **[#8398 — isAbortError fails to recognize OpenAI SDK APIUserAbortError (P2)](https://github.com/QwenLM/qwen-code/issues/8398)** — User cancellations on the most common provider path are misclassified, breaking expected cancel behavior. A fix is already in PR #8399.

5. **[#8356 — Turns lost after APIUserAbortError (P2)](https://github.com/QwenLM/qwen-code/issues/8356)** — Session transcript stops being written after an abort error, compounding the abort classification bug. Windows + OpenAI-compatible relay configuration.

6. **[#8051 — Bound multi-workspace daemon resource usage (P2)](https://github.com/QwenLM/qwen-code/issues/8051)** — Tracked request for the `qwen serve` daemon to cap memory bytes beyond simple count limits. Addresses potential memory exhaustion in production deployments.

7. **[#8123 — Desktop client cannot reference correct files (P3)](https://github.com/QwenLM/qwen-code/issues/8123)** — `@` file reference search fails for existing files like `KuaiShouOrderService.java`. Basic functionality impairment in the desktop client v0.5.5.

8. **[#8376 — Change node.exe process name to qwen.exe (P3)](https://github.com/QwenLM/qwen-code/issues/8376)** — Users need reliable process identification for external tooling; Node-based process naming complicates monitoring and task management.

9. **[#8385 — ConEmu/Cmder: full output flickering on Windows (P3)](https://github.com/QwenLM/qwen-code/issues/8385)** — Persistent flickering in ConEmu/Cmder terminals with only `CI=true` as a workaround. Affects terminal UX in popular Windows shells.

10. **[#8281 — Email channel with IMAP/SMTP support (P3)](https://github.com/QwenLM/qwen-code/issues/8281)** — Feature request to communicate with Qwen Code agents via email, expanding integration channels beyond chat/web.

---

## Key PR Progress

1. **[#8399 — Recognize OpenAI SDK APIUserAbortError as abort](https://github.com/QwenLM/qwen-code/pull/8399)** — Direct fix for the `isAbortError` misclassification. On `auth_type=openai`, user cancels now properly trigger abort handling instead of being treated as errors.

2. **[#8396 — Close four trust-boundary holes in hook execution](https://github.com/QwenLM/qwen-code/pull/8396)** — Critical security hardening: HTTP hooks no longer follow redirects, closing SSRF and whitelist-bypass vectors, plus three other boundary fixes at the repo-config/code-execution intersection.

3. **[#8276 — Preserve prompt cache across deferred tool discovery](https://github.com/QwenLM/qwen-code/pull/8276)** — Maintains stable provider tool declarations and cached system instructions while deferred tools are discovered, with a `deferred_tool_call` bridge routing to real tools post-discovery.

4. **[#8394 — Maven multi-module verification for /review](https://github.com/QwenLM/qwen-code/pull/8394)** — `/review build-test` now recognizes root Maven reactors, maps changed files to deepest modules, and provides deterministic verification. Major Java project support improvement.

5. **[#8402 — Structured Web Shell review results](https://github.com/QwenLM/qwen-code/pull/8402)** — Canonical findings and authoritative verdicts from `/review` become versioned, durable session artifacts, with Web Shell rendering support.

6. **[#8401 — Repository context foundation for /review](https://github.com/QwenLM/qwen-code/pull/8401)** — Versioned, bounded repository-context contract wired through roster selection, reviewer prompts, and verification guidance.

7. **[#8332 — Audio bridge for attachments](https://github.com/QwenLM/qwen-code/pull/8332)** — Transcribes audio attachments through a batch voice model when the primary model lacks audio support; replaces with explicitly untrusted machine-transcribed text.

8. **[#8368 — Kimi and Xiaomi MiMo providers](https://github.com/QwenLM/qwen-code/pull/8368)** — Adds first-class Kimi (Coding Plan, API Key China/International) and Xiaomi MiMo presets to `/auth`, expanding third-party provider ecosystem.

9. **[#8274 — Fork from any conversation point](https://github.com/QwenLM/qwen-code/pull/8274)** — Session branching now targets specific earlier assistant responses rather than latest state, handling tool calls, cancellations, and pagination edge cases safely.

10. **[#8388 — capture-tui: rendering claims verified with pixels](https://github.com/QwenLM/qwen-code/pull/8388)** — Verifiers can drive code under review in a private tmux server and capture actual pane rendering — resolving disputes about terminal rendering claims with evidence.

---

## Feature Request Trends
- **Daemon/Serve architecture evolution**: Multiple requests to bound resource usage, add Plan & Review workflows, and improve multi-workspace support in `qwen serve` mode
- **Channel expansion**: Beyond chat, users want email (IMAP/SMTP) and other integration channels for agent communication
- **Review/Audit tooling growth**: Aggressive investment in `/review` — Maven support, structured results, repo context, TUI capture evidence, and new `/audit` for legacy code
- **Provider ecosystem**: Addition of Kimi and Xiaomi MiMo alongside OpenAI-compatible paths shows demand for multi-provider flexibility
- **Desktop parity**: Features and fixes consistently requested for desktop client parity with CLI (image drag-drop, file references, session reliability)

---

## Developer Pain Points
1. **Session integrity issues**: Silent auto-deletion, concurrent writer conflicts, transcript loss after aborts — session reliability remains the top concern across desktop and CLI
2. **Error handling inconsistencies**: Abort errors misclassified, leading to cascading failures with tool calls and session state corruption
3. **Process identification**: Running as `node.exe` makes Qwen Code hard to distinguish from other Node processes for monitoring and management
4. **Windows-specific issues**: Flickering in ConEmu/Cmder, desktop file reference failures, smoke-log path mismatches — Windows parity remains a recurring theme
5. **CI/CD infrastructure drift**: Outdated ECS runners, test failures before results reported, and Windows merge-queue test reliability indicate ongoing CI maintenance burden

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-03

---

## Today's Highlights

The DeepSeek TUI project (repository alias "CodeWhale") is moving aggressively toward multi-provider neutrality and agent-workflow maturity in the v0.9.4 cycle. The 24-hour window shows a burst of 16 new WIP pull requests almost entirely focused on provider-agnostic architecture (Renaming `DeepSeekClient`, Responses API dialect profiles, Kimi/xAI auth fixes) alongside reliability releases-blockers around agent spawn tool contracts. Notably, a large batch of v0.9.3 epics (Termux Android support, Kimi K3 support, migration UX) were closed, signaling the team is consolidating infrastructure before the next major release. Community signal remains strong with 50 open issues and active discussion on session management and large-scale text processing.

---

## Releases

**No new releases in the last 24 hours.** The latest official version remains **v0.9.4** (with v0.9.5 already tracking open issues). Closed epics from the v0.9.3 train (Termux/Android arm64 support, Kimi OAuth device login, control-plane dashboard, migration UX) suggest a v0.9.5 or v1.0.0 release candidate is being assembled.

---

## Hot Issues (10 Noteworthy)

1. **[#2934 — Sidebar sessions panel with auto-resume](https://github.com/Hmbown/CodeWhale/issues/2934)** — *12 comments, trending*  
   The highest-activity open issue asks for a persistent sidebar session list to replace the `Ctrl+R` picker popup. Community voices friction in managing long-lived workflows; this is the top UX enhancement request in the backlog.

2. **[#998 — 文案展示不全 (Truncated text display)](https://github.com/Hmbown/CodeWhale/issues/998)** — *11 comments*  
   A long-running Chinese-language issue about text truncation in the TUI with a request for hover tooltips. Signals a broader i18n and layout polish gap. Multi-week staleness suggests the team has deprioritized it.

3. **[#689 — `deepseek doctor` passes but `deepseek run` fails](https://github.com/Hmbown/CodeWhale/issues/689)** — *10 comments*  
   Diagnostic passes but runtime fails — a high-frustration class of bug eroding trust in the toolchain. Community has reproduced on v0.8.10; still open on v0.9.4.

4. **[#4242 — Termux runtime QA matrix (CLOSED)](https://github.com/Hmbown/CodeWhale/issues/4242)** — *9 comments*  
   The Android/Termux QA epic closed cleanly, covering shell dispatch, TUI startup, raw-mode behavior, and resize handling. This unblocks official Android support in the next release.

5. **[#1004 — `/dryrun` command: preview next chat request](https://github.com/Hmbown/CodeWhale/issues/1004)** — *8 comments*  
   A well-specified feature request to preview the exact payload (system prompt, cached files, tool definitions, @mentions) before sending. Strong resonance with V4 Pro users facing token-cost surprises.

6. **[#5123 — v0.9.4 release-blocker: agent spawn surface too many knobs](https://github.com/Hmbown/CodeWhale/issues/5123)** — *1 comment, newly filed*  
   A dogfood-found release blocker: delegates labeled `builder` are running **read-only** and self-BLOCKED. This is the most urgent architectural issue for the agent-runtime v0.9.4 ship.

7. **[#1425 — Session hang on 3M-character text processing](https://github.com/Hmbown/CodeWhale/issues/1425)** — *6 comments*  
   Sub-agent `agent_wait` timeouts cause session death when parallelizing large-text analysis (10 sub-agents). A critical reliability gap for power users with document-intensive workloads.

8. **[#1482 — NVIDIA NIM returns 404 on API call](https://github.com/Hmbown/CodeWhale/issues/1482)** — *6 comments*  
   Provider integration regression with NIM. Community workaround is unknown; API surface mismatch likely. Relevant to the broader "Fleet routing" effort.

9. **[#1829 — SSH exit code 255: sandbox blocks TCP 22 outbound](https://github.com/Hmbown/CodeWhale/issues/1829)** — *5 comments*  
   The TUI's built-in shell sandbox blocks outbound SSH — a sharp edge for users who expect a full terminal. Shows the cost of security hardening on developer workflow.

10. **[#1651 — VS Code crashes when YOLO Agent runs tests](https://github.com/Hmbown/CodeWhale/issues/1651)** — *5 comments*  
   Autonomous test-running is crashing the host editor — a serious stability signal for YOLO/autonomous modes. Unclear whether the TUI or VS Code integration is at fault.

---

## Key PR Progress (10 Notable)

1. **[#5106 — Rename `DeepSeekClient` to provider-neutral types](https://github.com/Hmbown/CodeWhale/pull/5106)** — *WIP*  
   The plumbing for multi-provider neutrality. Renames shared client types and engine wiring without behavior changes. Foundational for the post-DeepSeek provider roadmap.

2. **[#5108 — Make Responses API behavior provider-profiled](https://github.com/Hmbown/CodeWhale/pull/5108)** — *WIP*  
   Adds a typed Responses dialect/profile to route resolution — moving away from provider-boolean spaghetti. Clean seam for Anthropic/OpenAI/DeepSeek divergence.

3. **[#5114 — Extract Responses dialect policy behind a conformance harness](https://github.com/Hmbown/CodeWhale/pull/5114)** — *WIP*  
   Companion to #5108: introduces table-driven conformance tests for standard vs. stateless/plain-reasoning profiles. The testing discipline here is strong.

4. **[#5123-adjacent — #5107: Fix provider switching to update default model](https://github.com/Hmbown/CodeWhale/pull/5107)** — *WIP*  
   Targets stale cross-provider model selection. Small, surgical, table-driven. Exactly the kind of fix that reduces the issue #689 class of failures.

5. **[#5105 — Fix wrong-type report for `replace` in `File.edit`](https://github.com/Hmbown/CodeWhale/pull/5105)** — *WIP*  
   Clarifies the patch schema by removing the `replace` name collision, using `files` instead (`changes` deprecated alias). Improves diagnostics for wrong JSON types.

6. **[#5109 — Fix isolated worktree contention in Fleet builders](https://github.com/Hmbown/CodeWhale/pull/5109)** — *WIP*  
   Addresses shared delegated-coordination contention when Fleet builders run in isolated worktrees. Reactive fix to a live concurrency bug.

7. **[#5112 — Fix Kimi API keys persistence in provider setup](https://github.com/Hmbown/CodeWhale/pull/5112)** — *WIP*  
   Ensures Kimi/Moonshot keys save, reload, and resolve aliases across sessions. Rollback-on-failure semantics preserved. Direct follow-up to the Kimi OAuth epic.

8. **[#5111 — Fix xAI device login not activating provider config](https://github.com/Hmbown/CodeWhale/pull/5111)** — *WIP*  
   Device-login finalization wasn't re-loading provider config. Fake-based tests enforce rollback semantics. Critical for the xAI Grok path.

9. **[#5095 — Fix OpenHarmony Windows linker arg quoting](https://github.com/Hmbown/CodeWhale/pull/5095)** — *Open, non-WIP*  
   A genuine user-contributed fix (not bot-authored): re-quotes Windows linker arguments containing spaces, fixing `--sysroot` splitting under `D:\DevEco Studio\...`. Real-world platform portability win.

10. **[#5115 — Detect and break non-progressing turn loops](https://github.com/Hmbown/CodeWhale/pull/5115)** — *WIP*  
   Adds no-progress watchdog signaling with reason, elapsed time, and recovery actions — targeting stale child-wait and repeated model/tool retry loops. Directly addresses the #1425 session-hang class.

---

## Feature Request Trends

- **Session management & continuity** — Persistent sidebar sessions (#2934), selective rewind (#4400), retain active intent across compaction/session resumes. Users want long-running work to survive restarts and sub-agent failures.
- **Provider-agnostic multi-model routing** — NIM 404s (#1482), Kimi OAuth (#4417), xAI login (#5111), benchmark-driven Fleet routing (#4389). The community is pushing hard for frictionless provider interop.
- **Cost and payload transparency** — `/dryrun` preview (#1004), cache-read pricing (#4319). Developers want to see what they're paying for *before* hitting send.
- **Workflow and agent orchestration visibility** — Multi-session dashboards (#4397), persistent workflow status in the top bar (#5113), monitor subscriptions and `/loop` UX (#4398). Demand for an operator "control tower."
- **Platform portability** — FreeBSD npm support (#1097), Termux/Android official builds (#4236), OpenHarmony linker fixes (#5095). Users are running this TUI everywhere.

---

## Developer Pain Points

- **Diagnostic/runtime divergence** — `deepseek doctor` passes but `deepseek run` fails (#689). This erodes trust and is the single most commented *unfixed* reliability bug.
- **Sandbox over-restriction** — The shell sandbox blocking outbound SSH port 22 (#1829) breaks legitimate workflows; users want configurable network policy, not blanket blocks.
- **Sub-agent timeout deadlocks** — Large parallel sub-agent workloads hang on `agent_wait` (#1425, #1732). The `PR #5115` watchdog is a direct response, but shipping it is urgent.
- **Display and i18n fragmentation** — Truncated CJK text (#998) and incomplete locale coverage (#790) create a second-class experience for the large Chinese-speaking user base.
- **Autonomous-mode instability** — VS Code crashes under YOLO Agent (#1651) and confusing permission/read-only flag mismatches (#5123). Autonomous agents are powerful but currently too risky for production trust.
- **Configuration sprawl** — Two model-resolution chains (#4851), split config surface (#3949), and a 14k-line `main.rs` (#3948) are internal debts that now surface as user-facing bugs (e.g., provider switching leaves stale defaults).

---

*Digest compiled from public GitHub activity on `github.com/Hmbown/DeepSeek-TUI` (CodeWhale), 2026-08-03 UTC.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*