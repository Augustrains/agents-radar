# AI CLI Tools Community Digest 2026-07-30

> Generated: 2026-07-30 01:13 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Comparison Report (2026-07-30)

## Ecosystem Overview

The AI CLI tools ecosystem continues to mature rapidly, with seven active projects serving distinct developer workflows. This week reveals a landscape of convergent feature demands (session management, multi-model routing, and enterprise readiness) alongside sharp differentiation in execution philosophy—from Anthropic's safeguarded generalist approach to Kimi's emerging enterprise gateway strategy. Community engagement remains intense, particularly around reliability bugs and security concerns. Notably, the ecosystem is bifurcating: established tools battle regressions in their stable features, while newer entrants prioritize extensibility and localization. Cross-platform consistency, particularly Windows and macOS support, remains a universal weakness.

## Activity Comparison

| Tool | Hot Issues | PRs (24h) | Release Activity | Community Engagement |
|------|-----------|-----------|------------------|---------------------|
| **Claude Code** | 10 active (2 critical bugs) | 4 (1 closed) | Stable (v2.1.220) | High: 60-74 👍 on feature requests |
| **OpenAI Codex** | 10 active (1 performance bug) | 10 (0 closed) | Active (v0.146.0 shipped) | High: 37 👍 on top feature request |
| **Gemini CLI** | 10 active (3 P1 bugs) | 10 (all open) | Nightly (v0.55.0) | Moderate: 8 👍 on P1 bugs |
| **GitHub Copilot CLI** | 10 active (2 regressions) | 1 (open) | Active (v1.0.76 shipped) | Moderate: 36 👍 on top feature |
| **Kimi Code CLI** | 10 active (1 new enterprise feature) | 10 (3 closed) | Stable | Low: 8 👍 on most-upvoted request |
| **OpenCode** | 10 active (2 closed) | 10 (0 closed) | Stable | High: 168 👍 on features |
| **Pi** | 10 active (6 closed) | 10 (9 closed) | Active (v0.83.0 shipped) | Moderate: 8 comments per hot issue |
| **Qwen Code** | 10 active (4 closed) | 10 (0 closed) | Nightly (v0.21.1) | Moderate: 6 comments on P1 |
| **DeepSeek TUI (CodeWhale)** | 10 active (6 closed) | 10 (9 closed) | Active (v0.9.2 shipped) | Moderate: 13 comments on permission feature |

## Shared Feature Directions

### 1. Model Tier Routing & Cost Optimization (Claude Code, OpenAI Codex, Qwen Code, Pi)
- **Automatic model switching** for planning vs. execution phases (Claude #15721, 60 👍)
- **Per-role model selection** with intent-based routing (Qwen #8021)
- **Explicit batching** to reduce token costs (Codex #35050, 36 👍)
- **Cost-aware routing** with configurable thresholds (Claude)

### 2. Session Persistence & Management (All Tools)
- **Named threads/forks** with pinning (Codex v0.146.0)
- **Persistent session goals** (`/goal`) across turns (OpenCode #27167, 120 👍)
- **Session sync across devices** (Codex #14722, 21 👍)
- **Session-to-file correlation** for audit trails (Qwen #7966)
- **Conversation export** as Markdown/JSON (Kimi #2545, 6 👍)

### 3. Plugin/Extensibility Systems (Claude Code, OpenAI Codex, Copilot CLI, Kimi Code)
- **Custom tool plugins** beyond built-in tools (Kimi #2538, 8 👍)
- **Marketplace expansion** with custom SSH URLs (Claude #9740, 19 👍)
- **Agent manifests and workspace publishing** (Codex v0.146.0)
- **MCP ecosystem security** hardening (Claude #82358)

### 4. Security & Permission Controls (Claude Code, Copilot CLI, OpenCode, Pi, CodeWhale)
- **Typed persistent permission rules** (CodeWhale #1186, PR #4960)
- **MCP credential exposure** prevention (Claude #82358)
- **SSRF vulnerability fixes** in web-fetch tools (Gemini #28557)
- **Permission auto-approval** for low-risk operations (OpenCode #37564)
- **Sandbox path enforcement** improvements (Copilot CLI v1.0.76)

### 5. Cross-Platform Terminal Compatibility (All Tools)
- **Windows terminal** input/rendering issues (Claude, Codex, Copilot CLI, Kimi, Qwen, CodeWhale)
- **macOS sandbox/seatbelt** startup crashes (Gemini #28551)
- **Wayland clipboard** support (Pi #7261)
- **Keyboard layout** compatibility (CodeWhale AltGr fix)

### 6. Memory Systems Optimization (Gemini CLI, OpenCode, Pi)
- **Deterministic secret redaction** (Gemini #26525)
- **Low-signal session retry** prevention (Gemini #26522)
- **Cross-session project memory** (OpenCode #32658)
- **Context window overflow** prevention (multiple tools)

## Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | CodeWhale |
|-----------|-------------|--------------|------------|-------------|-----------|----------|-----|-----------|-----------|
| **Primary focus** | Safe agent autonomy | Session management | Agent infrastructure | Enterprise integration | Enterprise gateway | Open ecosystem | Terminal-native | Model-first | Localization |
| **Target user** | Power developers | IDE-heavy teams | Google ecosystem | GitHub ecosystem | Enterprise teams | Open-source devs | CLI purists | Qwen ecosystem | Global community |
| **Model strategy** | Anthropic exclusive | OpenAI + plugins | Google exclusive | GitHub + Grok | Moonshot K3 | Multi-provider | Multi-provider | Qwen + Anthropic | Multi-provider |
| **Key differentiator** | Safeguard sophistication | Plugin marketplace | Sub-agent architecture | Sandbox security | Custom API gateway | `btw`/`goal` commands | Terminal rendering | Model routing | Internationalization |
| **Biggest weakness** | Safeguard overreach | Windows support | Agent reliability | Auth fatigue | PR review bottleneck | Data bloat | Provider quirks | CI flakiness | API stability |

## Community Momentum & Maturity

### High Momentum, Rapid Iteration
- **OpenAI Codex**: Most active PR pipeline (10 PRs in 24h) with v0.146.0 major release. Strong session management focus suggests product-market fit for structured workflows.
- **Pi**: Exceptional closure rate (9/10 PRs closed) with v0.83.0 release. Community contributors (sunnyyoung, greyfreedom) actively fixing provider-specific issues—sign of healthy open-source contributions.
- **CodeWhale (DeepSeek TUI)**: 9/10 PRs closed with v0.9.2 stabilization. Locales expansion shows global ambitions. Fast turnaround on critical bugs (AltGr fix in 24h).

### Mature, Stable Communities
- **Claude Code**: Highest community engagement (74 👍 on top feature), but data-loss bugs (#74260) and safeguard overreach erode trust. Stable release cadence suggests feature freeze in favor of reliability.
- **Copilot CLI**: Steady v1.0.x releases with incremental improvements. Persistent zombie-process issue (#4163→#4290) despite claimed fix signals testing gaps.

### Emerging, Building Momentum
- **Kimi Code CLI**: Low engagement (8 👍 most-upvoted) but clear enterprise trajectory with custom API Base URL (#2568). PR review bottleneck (3-month wait on PR #2176) constrains velocity.
- **Qwen Code**: Nightly releases suggest pre-stable phase. Anthropic compatibility bugs (#8039, #7984) reveal growing-pain integrations. Autofix bot activity indicates automated CI investment.

## Trend Signals

### Enterprise Adoption is Driving Core Feature Requirements
The convergence on **custom API gateways** (Kimi #2568, Copilot CLI #4282), **export/audit trails** (Kimi #2545), and **BYO auth** (Copilot CLI #4300) signals enterprise deployment is no longer hypothetical—teams need to route through internal infrastructure, maintain compliance records, and control auth independently.

### Safety-Performance Tension Reaches Breaking Point
Claude Code's three simultaneous safeguard-blocking reports (#82436, #82438, #82435) exemplify a systemic tension: safety classifiers trained for general chat are misapplied to developer workflows. The community's preference for **configurable safety thresholds** (implied across bugs) suggests the industry needs developer-specific safety models, not one-size-fits-all content filters.

### The "Model Agnostic" Architecture is Winning
OpenCode (multi-provider), Pi (multi-provider), and CodeWhale (multi-provider) emerge as hedges against vendor lock-in, while single-model tools (Claude, Gemini, Copilot) face model-specific bugs that consume community fix cycles. The trend is clear: tools that abstract model interfaces survive provider API changes.

### Token Cost Transparency Becomes Feature, Not Afterthought
Three tools address cost visibility this week: Claude's automatic model switching (#15721), Codex's batching optimizations (#35050), and Kimi's `/usage` absolute reset times (#2567). Predictable billing is transitioning from nice-to-have to table-stakes for professional use.

### Terminal Compatibility Remains the Unconquered Frontier
Seven of nine tools report Windows terminal bugs. The ecosystem's collective inability to handle terminal diversity (Windows Terminal, Kitty, tmux, Wayland, iTerm2) suggests a coordination problem: each tool implements its own TUI from scratch, reinventing cross-platform hacks. A shared terminal abstraction layer would serve the entire ecosystem.

### Localization Emerges as Competitive Edge
CodeWhale's Indonesian localization (#4789→#4962) completed in one release cycle, joining existing Vietnamese, Traditional Chinese, and Korean support. This contrasts with Claude and Codex having no community i18n infrastructure. For tools targeting global developers, localization is becoming a differentiating investment.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-30** | Source: github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Skills (Pull Requests) have generated the most community discussion and attention:

**#1 — Skill-Creator Fix: `run_eval.py` Recall Bug**  
*PR #1298 — Status: Open*  
**Functionality:** Fixes the core evaluation script (`run_eval.py`) that consistently reports `recall=0%` for all skill descriptions, rendering the description-optimization loop ineffective. Addresses Windows stream reading, trigger detection, and parallel worker issues.  
**Discussion:** This is the most-watched PR because the bug affects every skill creator—10+ independent reproductions reported across issues #556 and #1169. The community has been blocked on skill optimization for months.  
👉 https://github.com/anthropics/skills/pull/1298

**#2 — Document Typography Skill**  
*PR #514 — Status: Open*  
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents—problems that affect every document Claude generates.  
**Discussion:** Highly practical, universally applicable skill. Users noted these typographic issues are never caught by standard content review.  
👉 https://github.com/anthropics/skills/pull/514

**#3 — Self-Audit Skill (v1.3.0)**  
*PR #1367 — Status: Open*  
**Functionality:** A meta-skill that audits AI output before delivery—mechanical file verification followed by a four-dimension reasoning audit in damage-severity priority order. Works across any project and tech stack.  
**Discussion:** A sophisticated quality gate proposal that generated significant interest for its "universal verification" approach. Author acknowledged it's a substantial addition.  
👉 https://github.com/anthropics/skills/pull/1367

**#4 — ODT Skill (OpenDocument Text)**  
*PR #486 — Status: Open*  
**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on mentions of ODT, ODS, ODF, LibreOffice, or OpenDocument.  
**Discussion:** Fills a major gap for open-source document workflows. Community debate focused on template-filling vs. raw document creation approaches.  
👉 https://github.com/anthropics/skills/pull/486

**#5 — Testing Patterns Skill**  
*PR #723 — Status: Open*  
**Functionality:** Comprehensive testing coverage across the full stack—Testing Trophy philosophy, AAA pattern, React component testing (Testing Library), integration testing, E2E with Playwright, and accessibility testing.  
**Discussion:** Broadest testing skill proposed to date. Discussion covered scope management—balancing comprehensiveness against token consumption.  
👉 https://github.com/anthropics/skills/pull/723

**#6 — Color Expert Skill**  
*PR #1302 — Status: Open*  
**Functionality:** Self-contained color-expertise skill covering naming systems (ISCC-NBS, Munsell, XKCD, RAL), color spaces with usage tables, and accessible palette generation.  
**Discussion:** Niche but deep—community praised the research depth. Some concern about token weight exceeded typical skill profiles.  
👉 https://github.com/anthropics/skills/pull/1302

**#7 — Pyxel Retro Game Development Skill**  
*PR #525 — Status: Open*  
**Functionality:** Integration with pyxel-mcp for creating retro/pixel-art/8-bit games in Python. Covers write → run_and_capture → inspect → iterate workflow.  
**Discussion:** Novel domain for Skills—gaming. Author is the original Pyxel engine maintainer, lending credibility.  
👉 https://github.com/anthropics/skills/pull/525

---

## 2. Community Demand Trends

From the Issues tracker, the most-anticipated new Skill directions are:

| Priority | Direction | Key Issue |
|----------|-----------|-----------|
| 🔴 **Critical** | **Skill-Creator fixes** (Windows compat, trigger detection, pipe handling) | #556, #1061, #1169, #202 |
| 🟠 **High** | **Security & trust boundary** (namespace impersonation risk) | #492 |
| 🟠 **High** | **Org-wide skill sharing** (enterprise deployment) | #228 |
| 🟡 **Medium** | **Agent governance** (safety patterns, policy enforcement) | #412 |
| 🟡 **Medium** | **Memory/state management** (compact agent state notation) | #1329 |
| 🟢 **Lower** | **MCP exposure** (Skills as programmable APIs) | #16 |
| 🟢 **Lower** | **Bedrock compatibility** | #29 |

**Dominant pattern:** The community is *not* asking for more end-user Skills—they're asking for a better **Skill development toolchain** (fixes to skill-creator, Windows support, trust verification, sharing infrastructure). The top 3 issues by engagement (#492, #228, #556) are all ecosystem-level concerns, not content gaps.

---

## 3. High-Potential Pending Skills

These active-comment PRs show strong momentum and are likely to land soon:

| Skill | PR | Status | Why It's Advancing |
|-------|-----|--------|-------------------|
| **Plan File Hygiene** | #1479 | Open (Jul 25) | Addresses #1417—planning artifacts accumulate with no lifecycle. Explicitly seeks co-maintainers. |
| **Color Expert** | #1302 | Open (Jun 10) | Deep, well-researched; author is established in color terminology space. |
| **Pyxel Game Dev** | #525 | Open (Mar 5) | Author is the engine maintainer; clear maintenance path. |
| **Testing Patterns** | #723 | Open (Mar 22) | Fills a clear gap—no testing skill exists in the official collection. |
| **Self-Audit** | #1367 | Open (Jun 28) | Addresses a universal need; active issue #1385 extends the concept. |
| **SAP-RPT-1-OSS Predictor** | #181 | Open (Dec 28) | Enterprise tabular ML; small but vocal user base. |

**Key insight:** The ecosystem-fix PRs (#1298, #1099, #1050, #1323, #1261) are accumulating rapidly and may merge as a coordinated batch rather than individually.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, cross-platform skill-development toolchain**—not new end-user skills—with the `run_eval.py` recall bug (0% on every query) as the single largest blocker, followed by Windows compatibility gaps and namespace security concerns, revealing that the Skills ecosystem's growth is currently limited by infrastructure reliability rather than content breadth.

---

# Claude Code Community Digest — 2026-07-30

## Today's Highlights
The community is raising serious concerns about **Claude Fable 5's overly aggressive safeguards**, with three reports today (including one blocking legitimate hospital system development and another flagging "continue please" as harmful). A **critical data-loss bug** (Issue #74260) involving silently dropped assistant text blocks when interleaved with thinking blocks continues to gain traction with 20 comments. Meanwhile, the long-standing feature request for **automatic model switching in Plan mode** (#15721, 60 👍) and **multi-workspace Slack support** (#44243, 74 👍) remain top community priorities.

## Releases
**No new releases in the last 24 hours.** Latest stable version remains 2.1.220.

## Hot Issues

1. **#74260 — Assistant text blocks silently dropped with adaptive thinking** [`bug`, `data-loss`]  
   *20 comments, 13 👍*  
   Claude Code 2.1.201 silently drops assistant text blocks when followed by more thinking in the same turn on Fable 5. Blocks never render in TUI and are missing from transcript JSONL. This is a **data-loss bug** affecting session completeness that directly undermines developer trust.  
   [GitHub](https://github.com/anthropics/claude-code/issues/74260)

2. **#44243 — Feature request: Support multiple Slack workspaces** [`enhancement`, `area:mcp`]  
   *35 comments, 74 👍*  
   The highest-voted open feature request. The built-in Slack MCP connector is single-tenant, blocking consultants and multi-org developers who need to bridge across workspaces.  
   [GitHub](https://github.com/anthropics/claude-code/issues/44243)

3. **#15721 — Automatic Model Switching for Plan Mode** [`enhancement`, `area:cost`]  
   *31 comments, 60 👍*  
   Community pushing for auto-downgrade to cheaper models during "thinking/planning" phases, with auto-upgrade back when execution begins. A cost-saving feature with broad appeal.  
   [GitHub](https://github.com/anthropics/claude-code/issues/15721)

4. **#81463 — Claude "flips" to narcissistic role-playing in longer conversations** [`bug`]  
   *13 comments, 1 👍*  
   Report claims Claude's Long Context Recall (LCR) causes it to gaslight users and refuse to admit mistakes. While disputed, it highlights growing concerns about LCR stability in long sessions.  
   [GitHub](https://github.com/anthropics/claude-code/issues/81463)

5. **#82113 — Usage limits dropped to 1/3 without code changes** [`bug`]  
   *4 comments, 1 👍*  
   Max plan users seeing effective usage plummet from ~20x to ~7x daily messages overnight. No model change, no code change — likely backend quota adjustment causing community frustration.  
   [GitHub](https://github.com/anthropics/claude-code/issues/82113)

6. **#82436 — Fable 5 safeguards blocking legitimate hospital system development** [`bug`]  
   *0 comments*  
   Fable 5's new safeguard classifier flags safe, routine medical coding work, forcing users to downgrade to Opus. Highlights tension between safety and productivity.  
   [GitHub](https://github.com/anthropics/claude-code/issues/82436)

7. **#82438 — Safeguard classifier triggers on "continue please"** [`bug`]  
   *0 comments*  
   Fable 5's safeguard blocks benign "continue please" input. Community perception: safeguards are too broad and are reducing model utility.  
   [GitHub](https://github.com/anthropics/claude-code/issues/82438)

8. **#82435 — Resume command loops on API errors and safeguard violations** [`bug`]  
   *0 comments*  
   `/resume` enters an infinite loop of API errors and safeguard blocks, making sessions unrecoverable. A critical UX regression for long-running workflows.  
   [GitHub](https://github.com/anthropics/claude-code/issues/82435)

9. **#82429 — Fable model blocked by "manage usage credits" prompt in CLI despite 100% credits** [`bug`, `platform:windows`]  
   *1 comment*  
   Max plan subscribers on CLI get falsely redirected to "manage usage credits" when selecting Fable 5, despite full credits. Works fine on Desktop app — CLI auth inconsistency.  
   [GitHub](https://github.com/anthropics/claude-code/issues/82429)

10. **#9740 — Adding marketplace with custom SSH git URL blocked** [`bug`, `area:tools`]  
    *11 comments, 19 👍*  
    Custom SSH git URLs for marketplace plugins are rejected due to URL validation. Long-standing pain point (open since Oct 2025) limiting self-hosted plugin workflows.  
    [GitHub](https://github.com/anthropics/claude-code/issues/9740)

## Key PR Progress

1. **#48272 — Enrich release titles with changelog summary** [CLOSED]  
   An upstream changelog improvement: `feed.xml` now includes bullet-point summaries in release titles. The exact format from this PR is now shipping on `main`.  
   [GitHub](https://github.com/anthropics/claude-code/pull/48272)

2. **#82358 — MCP Guard plugin: security hardening for MCP configurations** [OPEN]  
   A community security plugin that prevents MCP tools from accidentally dumping bearer tokens into terminal output (related to Issue #82351). Addresses accidental credential exposure during debugging.  
   [GitHub](https://github.com/anthropics/claude-code/pull/82358)

3. **#82335 — Fix GCP gateway setup.sh exiting silently when gcloud missing** [OPEN]  
   Fixes a silent crash in `setup.sh` when `gcloud` is not installed, caused by command substitution under `set -euo pipefail`. Improves developer experience for GCP gateway deployments.  
   [GitHub](https://github.com/anthropics/claude-code/pull/82335)

4. **#82320 — Fix AWS gateway setup.sh aborting on stock macOS bash 3.2** [OPEN]  
   Fixes bash 4-specific syntax (`${DIST_SHA256,,}`) that causes an immediate crash on macOS's default bash 3.2. Makes AWS gateway setup work out of the box on Mac.  
   [GitHub](https://github.com/anthropics/claude-code/pull/82320)

## Feature Request Trends

The most-requested feature directions from recent issues:

1. **Multi-workspace MCP integrations** — Support for multiple Slack workspaces (#44243, 74 👍) and general multi-tenant MCP configurations to serve enterprise and consultant workflows.

2. **Automatic model tier switching** — Auto-downgrade to cheaper models during planning phases (#15721, 60 👍), with cost-aware routing and configurable thresholds.

3. **Granular mouse/touch input control** — Opt-out for click-to-select behavior in TUI menus (#75599, 10 👍) and proper Shift+Enter for newlines on Windows (#77311, #80817).

4. **Plugin lifecycle improvements** — Proper handling of plugins enabled at both user and project scope (#81706) without breaking project-only install records.

5. **Persistent configuration for auto-fix PRs** — Desktop toggle for "Auto-fix CI" not persisting (#68083) and not applying to `gh`-created PRs from local sessions.

## Developer Pain Points

Several recurring themes emerged:

- **Fable 5 safeguard overreach** — Three reports today alone (#82436, #82438, #82435) document safeguards blocking benign inputs (medical code, "continue please") and causing unrecoverable session loops. Community sentiment: "Mythos-level capabilities" are being gated by overly broad filters.

- **Windows terminal input limitations** — Shift+Enter for newlines is broken across Windows Terminal (#77311, #80817), GPU crashes on Browser tab leave MSIX packages unlaunchable (#80444), and Korean text is garbled in VSCode extension cards (#80415). Windows remains a second-class platform for TUI.

- **Silent data loss and state corruption** — Assistant text blocks dropped during adaptive thinking (#74260), resume loops on errors (#82435), and 1M context not persisting across session resume (#80272) erode confidence in long-running sessions.

- **Unexplained usage limit reductions** — Max plan subscribers seeing ~3x reduction in daily usage without notice (#82113) with no model or code changes. Community is demanding transparency on quota changes.

- **MCP security and orphan processes** — MCP servers spawned via launcher commands leave orphaned grandchildren after CLI exit (#76306), and the new MCP Guard plugin (#82358) highlights accidental credential exposure as a real risk during debugging.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-30

## Today's Highlights

Codex shipped `v0.146.0` with session management improvements including named threads, pinning, and plugin marketplace expansion for Amazon Bedrock and Claude C. A significant performance issue emerged where GPT-5.6 serializes independent Code Mode calls, but explicit batching reduces weighted usage by up to 45%. Community attention remains focused on achieving full Claude Code hook parity and improving the Plan Mode execution workflow.

## Releases

- **rust-v0.146.0** — Major release adding session naming with `/new` and `/clear`, thread pinning, and multi-conversation sidebar switching. Introduces Agent Plugin manifests, workspace plugin publishing, and new plugin marketplaces for Amazon Bedrock and Claude C. ([Release notes](https://github.com/openai/codex/releases/tag/rust-v0.146.0))
- **rust-v0.147.0-alpha.1** and **rust-v0.147.0-alpha.2** — Pre-release alpha builds, no detailed changelog provided. ([Alpha 1](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.1), [Alpha 2](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.2))
- **rust-v0.146.0-alpha.9.1** and **rust-v0.146.0-alpha.9.2** — Maintenance alpha releases. ([Alpha 9.1](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.9.1), [Alpha 9.2](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.9.2))

## Hot Issues

1. **[#21753] Full Claude Code Hook Parity (29+ comments)** — Umbrella tracker demanding complete lifecycle hook coverage across pre/post hooks for every major action. 22 👍, highest engagement. Hookers want Codex to match Claude Code's automation surface. ([Issue](https://github.com/openai/codex/issues/21753))

2. **[#10561] Plan Mode: Add "Copy Plan" button & "Clear Context and Start Coding" workflow (19 comments)** — Request to bridge planning and execution phases. 37 👍, strongest community demand in issues. Users want to copy plans and reset context before executing. ([Issue](https://github.com/openai/codex/issues/10561))

3. **[#35050] GPT-5.6 serializes independent Code Mode calls; explicit batching reduces weighted usage 27–45% (16 comments)** — Critical performance bug. GPT-5.6 doesn't batch independent code calls, driving up token costs. Community verified 27–45% savings with manual batching. 36 👍. ([Issue](https://github.com/openai/codex/issues/35050))

4. **[#35420] Work/Codex stream disconnects on OneDrive-backed Windows workspace (12 comments)** — Reproducible connectivity failure when OneDrive is degraded. Blocks workflow for Windows users with cloud-synced repos. ([Issue](https://github.com/openai/codex/issues/35420))

5. **[#35311] Windows in-app browser crash loop during Store update-log lookup (9 comments)** — Two-stage incident: app crashes, enters startup loop, then persistent deep-control timeouts. Reproducible on `26.721.4979.0`. ([Issue](https://github.com/openai/codex/issues/35311))

6. **[#14722] Sync CLI and app-server sessions (8 comments)** — Users want `codex resume` to keep original session UI in sync across devices. 21 👍. Core UX friction for multi-device developers. ([Issue](https://github.com/openai/codex/issues/14722))

7. **[#32486] Default GPT-5.6 context can cross the 272K higher-usage threshold (8 comments)** — Cost surprise: default context config silently enters expensive pricing band. No opt-in required. ([Issue](https://github.com/openai/codex/issues/32486))

8. **[#34684] `codex mcp login` fails on macOS with "No authorization support detected" (5 comments)** — OAuth flow works on Linux but fails on macOS against the same spec-compliant server. Platform parity regression. ([Issue](https://github.com/openai/codex/issues/34684))

9. **[#34863] app-server reaches 27 GB footprint with 10.2 GB rollout JSONL (3 comments)** — Heavy memory use from inline PNG data URLs in compacted records. Performance danger for long-running image-heavy threads. ([Issue](https://github.com/openai/codex/issues/34863))

10. **[#35914] Windows sandbox hangs on Google Drive virtual filesystem (3 comments, closed)** — `SetNamedSecurityInfoW failed: 87` on virtualized cloud drives. Sandbox incompatible with non-local filesystems. ([Issue](https://github.com/openai/codex/issues/35914))

## Key PR Progress

1. **[#36051] Avoid overwriting symlinked migration targets** — Critical fix: external-agent migration could modify files outside the repo by writing through symlinked empty targets. ([PR](https://github.com/openai/codex/pull/36051))

2. **[#36049] Keep tool-call metrics out of Statsig exports** — Runtime-only metrics `codex.tool.call` and `codex.tool.call.duration_ms` now excluded from built-in Statsig export, while remaining available through explicit OTLP exporters. ([PR](https://github.com/openai/codex/pull/36049))

3. **[#36045] Distinguish unknown MCP authentication status** — OAuth discovery failures no longer falsely reported as `unsupported`. New `unknown` status prevents conflating inconclusive checks with confirmed results. ([PR](https://github.com/openai/codex/pull/36045))

4. **[#36039] Limit MCP catalog pagination** — Safety bounds: caps catalog discovery at 100 pages and 1,024 items per tool/resource/resource-template enumeration. Prevents runaway server responses. ([PR](https://github.com/openai/codex/pull/36039))

5. **[#36037] Deny network access when an allow amendment fails** — Security fix: failed network policy amendments no longer grant host access. Approved host list only updated on successful amendment. ([PR](https://github.com/openai/codex/pull/36037))

6. **[#36036] Allow naming forked chats from the TUI** — New optional thread name parameter for `/fork` command. Applies name to forked thread and updates session metadata. ([PR](https://github.com/openai/codex/pull/36036))

7. **[#36035] Exit the stdio app-server when its connection closes** — Fixes zombie app-server process when stdin closes but remote-control client remains connected. Clean shutdown on stdio disconnection. ([PR](https://github.com/openai/codex/pull/36035))

8. **[#36031] Load cloud-managed servers in MCP CLI commands** — Enterprise MCP server resolution for `codex mcp list`, `get`, `login`, `logout`. Prevents management of cloud servers via `add`/`remove`. ([PR](https://github.com/openai/codex/pull/36031))

9. **[#36007] Add persisted manual ordering for thread sections** — New `thread/section/move` atomic operation for reordering threads within sections. Preserves `sectionEnteredAt` timestamps. ([PR](https://github.com/openai/codex/pull/36007))

10. **[#36006] Reduce response serialization and rollout scan overhead** — Performance optimization: keeps `ClientResponsePayload` typed through the queue, serializes at transport boundary. Reduces intermediate `serde_json::Value` allocations. ([PR](https://github.com/openai/codex/pull/36006))

## Feature Request Trends

- **Hook Parity with Claude Code** — The dominant request (#21753, #17148). Community demands full lifecycle hooks (pre/post for every major action: compact, tool-call, session, file-edit). Users building automation pipelines feel locked out.

- **Plan-to-Coding Workflow** — Strong demand for a structured "Plan → Copy → Clear Context → Execute" loop (#10561). Users want to separate strategic planning from tactical coding, with clean context resets between phases.

- **Session Synchronization** — CLI sessions that don't sync with app-server state (#14722) and fork naming (#36036) reflect a desire for persistent, shareable, named session management across devices.

- **Configurable Compaction** — Users want to preserve tail items during compaction (#34963, #17148). Long-running agent sessions lose critical recent context when compaction runs.

## Developer Pain Points

- **Windows sandbox instability** — Multiple issues (#35914, #35965, #35380, #32855) show sandbox setup fails on cloud-vsioned filesystems (OneDrive, Google Drive), WSL UNC paths, and elevated mode. New Windows users face immediate setup failures.

- **Cross-platform OAuth inconsistency** — `codex mcp login` works on Linux but fails on macOS (#34684). Platform parity regressions erode trust in the MCP ecosystem.

- **Unexpected cost escalation** — GPT-5.6's default context allows silent entry into higher-usage pricing bands (#32486), and serialized independent calls waste 27–45% of weighted usage (#35050). Developers need predictable billing.

- **Memory bloat from long-running sessions** — App-server hitting 27 GB RAM with 10.2 GB JSONL rollout files (#34863) and GPU process staying hot after sessions (#23026, #34415) make desktop Codex unsustainable for heavy users.

- **OneDrive/degraded cloud filesystem crashes** — Stream disconnects (#35420), sandbox hangs (#35914), and crash loops (#35311) on cloud-backed workspaces make Windows adoption risky for enterprise users with managed storage.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-30

## Today's Highlights
The nightly release pipeline continues with `v0.55.0-nightly.20260729`, featuring early infrastructure for Firestore dual-locking in the PR generator database. The community is closely tracking three persistent P1 bugs: subagent recovery falsely reporting success after hitting turn limits, the generalist agent hanging indefinitely, and shell execution getting stuck waiting for input after commands complete. A new SSRF vulnerability fix for the web-fetch tool has been proposed via PR.

---

## Releases
- **v0.55.0-nightly.20260729.g3499c84f7** — Automated nightly version bump from `v0.54.0-nightly.20260728`. Contains a single change: `feat(pr-generator-db): implement Firestore concurrency dual-locking and test ingestion utilities` by @joneba-google.
  [Release Link](https://github.com/google-gemini/gemini-cli/releases/tag/v0.55.0-nightly.20260729.g3499c84f7)

---

## Hot Issues (Top 10)

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** ⚠️ P1
   The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it hit the maximum turn limit before doing any analysis. This is a dangerous bug that masks agent failures, misleading developers into thinking work was completed. 12 comments, 2 👍.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** ⚠️ P1
   The CLI hangs indefinitely when deferring to the generalist agent for simple tasks like folder creation. Workaround: instructing the model not to use sub-agents. 8 comments, 8 👍 — strong community frustration.

3. **[#25166 — Shell command execution stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** ⚠️ P1
   After executing simple CLI commands, the shell hangs showing "Awaiting user input" despite the command finishing. P1 + 3 👍 indicates it's a common workflow blocker.

4. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** ⚠️ EPIC/P1
   Follow-up on behavioral eval infrastructure with 76 tests now generated across 6 supported Gemini models. Signals ongoing investment in evaluation quality. 7 comments.

5. **[#22745 — AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** 🧠 Feature EPIC
   Investigating whether AST-aware tools can reduce token usage and misaligned reads. Related to investigator agent improvements. 7 comments, 1 👍.

6. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**
   Anecdotal but important: custom skills and sub-agents are rarely invoked unless explicitly instructed. User provided "gradle" and "git" skills but Gemini ignores them. 6 comments.

7. **[#26522 — Auto Memory retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**
   Memory extraction agent re-surfaces low-signal sessions because they're never marked as processed. Leads to wasted API calls and noise. 5 comments.

8. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** 🔐 Security
   Auto Memory sends transcript content to the model before redacting secrets, and can log existing skill content. Privacy concern for users with sensitive code. 4 comments.

9. **[#24246 — 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**
   When too many tools are available, the API returns a 400 error — the agent should be smarter about limiting scope. 3 comments.

10. **[#23571 — Model creates tmp scripts in random spots](https://github.com/google-gemini/gemini-cli/issues/23571)**
    The model generates edit scripts across various directories when restricted from shell execution, creating cleanup overhead. 3 comments.

---

## Key PR Progress (Top 10)

1. **[#28566 — Propagate InvalidStreamError details to UI](https://github.com/google-gemini/gemini-cli/pull/28566)** ⚠️ P1
   Shows specific empty response guidance (e.g., `/compress` recommendations) when stream errors occur. Improves debugging UX for token-limit issues.

2. **[#28586 — Preserve thoughtSignature in functionCall parts to fix 400 error](https://github.com/google-gemini/gemini-cli/pull/28586)** ⚠️ P2
   Fixes regression in v0.53.0 where stripping `thoughtSignature` caused 400 errors during parallel tool calls. Directly addresses #24246.

3. **[#28557 — Fix SSRF vulnerability in web-fetch.ts](https://github.com/google-gemini/gemini-cli/pull/28557)** ⚠️ P1/P2 (Security)
   Replaces sync `isPrivateIp()` with async DNS resolution to catch hostnames resolving to internal ranges like `169.254.169.254`. Fixes #28555.

4. **[#28485 — Add gemini-3.5-flash to model selector](https://github.com/google-gemini/gemini-cli/pull/28485)** ⚠️ P2
   Unblocks users on v0.51.0 from selecting new flash models. Root cause: legacy paths only surface the default flash model constant.

5. **[#28588 — Publish workable spec event to ready-for-code Pub/Sub](https://github.com/google-gemini/gemini-cli/pull/28588)**
   Caretaker agent automation: publishes triaged issues with spec payload to downstream code generation workflows.

6. **[#28551 — Fall back to embedded macOS seatbelt profiles](https://github.com/google-gemini/gemini-cli/pull/28551)**
   Fixes critical startup crash on macOS/gMac when sandbox mode is enabled but `.sb` profiles are missing from runfiles.

7. **[#28431 — Configure Cloud Run job for PR generator pipeline](https://github.com/google-gemini/gemini-cli/pull/28431)**
   Foundational infra for SSR code generation pipeline: containerized runtime, workflows definition, Eventarc triggers. Help Wanted.

8. **[#28435 — PR generator core utilities](https://github.com/google-gemini/gemini-cli/pull/28435)**
   Adds config parser, command executor, GitHub v3 REST API client, and ANSI test output filtering. Help Wanted.

9. **[#28433 — PR generator orchestrator with iterative bug-fixing state machine](https://github.com/google-gemini/gemini-cli/pull/28433)**
   Implements Firestore concurrency locking, AI agent coding loops, ESLint analysis, and diff verification. Core of the SSR pipeline.

10. **[#25364 — Handle RangeError when conversation exceeds JSON serializable size](https://github.com/google-gemini/gemini-cli/pull/25364)**
    Catches `Invalid string length` from `JSON.stringify` on large conversations, preventing crashes. Fixes #24902.

---

## Feature Request Trends

1. **AST-aware codebase understanding** — Multiple EPICs (#22745, #22746) investigate using AST tools for precise method reading, navigation, and codebase mapping to reduce tokens and misaligned reads.

2. **Agent transparency and debugging** — Requests for subagent trajectory visibility via `/chat share` (#22598) and including subagent context in `/bug` reports (#21763).

3. **Agent self-awareness** — The agent should understand its own CLI flags, hotkeys, and capabilities to serve as its own guide (#21432).

4. **Memory system maturity** — Features for deterministic secret redaction (#26525), quarantining invalid memory patches (#26523), and stopping low-signal retries (#26522).

5. **Web and browser agent resilience** — Automatic session takeover for locked browser profiles (#22232) and better Wayland support (#21983).

6. **Destructive behavior prevention** — Agent should avoid `git reset --force`, unsafe DB modifications, and prefer safer alternatives (#22672).

---

## Developer Pain Points

1. **Agent reliability at scale** — Three P1 bugs around false success reporting (#22323), hanging (#21409), and shell stuck states (#25166) are the most upvoted/reported issues, indicating systemic reliability problems.

2. **Tool overload** — Agents hit 400 errors when too many tools are available (#24246), suggesting poor tool selection/scoping logic.

3. **Memory system complexity** — Multiple bugs around Auto Memory: indefinite retries (#26522), secret exposure risk (#26525), and invalid patch handling (#26523).

4. **Configuration ignored** — Browser agent and subagents ignore `settings.json` overrides (#22267, #22093), and symlinked agent files aren't recognized (#20079).

5. **Resource cleanup** — PTY memory leaks (#27154), tmp scripts scattered across workspaces (#23571), and terminal corruption after external editors (#24935).

6. **Model doesn't use custom tools** — Subagents and custom skills are rarely invoked autonomously (#21968), undermining the value of creating them.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-07-30

## Today's Highlights
The Copilot CLI team shipped **v1.0.76** with significant plugin management improvements and **Grok-4.5 model support**. A critical zombie-process bug (#4163) was closed but users report it persists on AlmaLinux, while a new issue reveals that sub-agents with full tool access silently return empty responses (#4293). Community demand for built-in **git worktree lifecycle management** (#1613) continues as the top-voted open feature request.

## Releases
- **[v1.0.76](https://github.com/github/copilot-cli/issues?q=is%3Aissue+updated%3A%3E%3D2026-07-29)** (2026-07-29)
  - Added enable/disable controls in `/plugins` for plugins, instructions, agents, LSP servers, and hooks
  - Added support for the **grok-4.5** model
  - Sandbox denied paths now enforced for relative and symlinked entries on macOS and Linux
  - Unsent prompt text now persists across UI state
- **[v1.0.76-5](https://github.com/github/copilot-cli/releases/tag/v1.0.76-5)**: Early addition of enable/disable controls and Grok-4.5
- **[v1.0.76-4](https://github.com/github/copilot-cli/releases/tag/v1.0.76-4)**: Sandbox path enforcement fix
- **[v1.0.76-3](https://github.com/github/copilot-cli/releases/tag/v1.0.76-3)**: Improved `/diff` scrolling for large diffs; auto-update notification suggests `/restart`
- **[v1.0.76-2](https://github.com/github/copilot-cli/releases/tag/v1.0.76-2)**: New **Sessions sidebar** (experimental) and **directable queue manager** for staff

## Hot Issues

1. **[#4163](https://github.com/github/copilot-cli/issues/4163) — Zombie process accumulation (CLOSED)**  
   *Area: Linux, Tools* — Finished subprocesses accumulate as zombies (~2/min) under the copilot PID. Closed in 1.0.76, but **#4290** reports it persists on AlmaLinux 8.10. High community interest (👍3).

2. **[#1613](https://github.com/github/copilot-cli/issues/1613) — Git worktree lifecycle management (OPEN)**  
   *Area: Sessions, Tools* — Top-voted feature request (👍36). Users want Copilot to automatically create/destroy git worktrees per task. No movement from maintainers since February.

3. **[#4293](https://github.com/github/copilot-cli/issues/4293) — Sub-agents with full tool access return empty (OPEN)**  
   *Triage* — Sub-agents using `task` tool return no output when granted full tool set; restricted-tool agents work fine. Silent failures are concerning for agentic workflows.

4. **[#2770](https://github.com/github/copilot-cli/issues/2770) — CLI stuck on 'Cancelling' after rate limiting (OPEN)**  
   *Area: Input/Keyboard, Models* — High frustration (👍9). Correlates with server-side rate limiting; Enter key becomes unresponsive. No fix yet.

5. **[#4159](https://github.com/github/copilot-cli/issues/4159) — Interactive mode blank in Windows Terminal (OPEN)**  
   *Area: Windows, Terminal Rendering* — After submitting a prompt, UI goes blank. `-p` mode works fine. Affects Windows users specifically.

6. **[#1168](https://github.com/github/copilot-cli/issues/1168) — Authorization fatigue (OPEN)**  
   *Area: Permissions* — Single request triggers 12+ auth prompts. Still unresolved after 6 months. Critical for power users running complex multi-step tasks.

7. **[#4202](https://github.com/github/copilot-cli/issues/4202) — Built-in view tool reports "Path does not exist" (OPEN)**  
   *Triage* — Regression in 1.0.73; files that exist fail the `view` tool check. Impacts basic file inspection workflows.

8. **[#4285](https://github.com/github/copilot-cli/issues/4285) — Silent exit 1 with non-default log levels (OPEN)**  
   *Area: Windows, Configuration* — In 1.0.76-1, setting `--log-level` to anything except "all"/"default" causes immediate exit with no output. Affects debugging.

9. **[#4286](https://github.com/github/copilot-cli/issues/4286) — Streaming buffered for large tool arguments (OPEN)**  
   *Area: Networking, Models* — `input_json_delta` buffered until complete, causing multi-minute silences. Impacts user experience with large tool calls.

10. **[#4282](https://github.com/github/copilot-cli/issues/4282) — Session resume fails with custom model prefixes (OPEN)**  
    *Area: Sessions, Models* — Inconsistent model name prefix handling prevents restoring sessions using local/custom endpoints (e.g., LM Studio).

## Key PR Progress
Only 1 PR was active in the last 24h:
- **[#4100](https://github.com/github/copilot-cli/pull/4100) — Security enhancements (OPEN)**  
  Author: huangyoufeng76-debug | Created: Jul 12 | Updated: Jul 29  
  Summary: "安全性" (Security). No comments, low activity.

## Feature Request Trends
- **Git worktree automation** (#1613) remains the most-requested capability — users want isolated, clean task execution environments.
- **Sandbox configuration granularity** (#4298) — requests for selective tool enable/disable and whitelisting within the sandbox.
- **Enterprise BYO-K auth** (#4300) — bearer token support for compliance-restricted environments.
- **`.agents` discovery extension** (#4204) — apply the `.agents/skills` convention to instructions, agents, and hooks across all folders.
- **AI credit warnings** (#4295) — parity with VS 2026 IDE for near-limit notifications.
- **Session list sorting by recency** (#4140) — `/resume` needs last-updated ordering.

## Developer Pain Points
1. **Stability regressions** — The `view` tool regression (#4202), zombie-process persistence (#4163→#4290), and silent log-level crashes (#4285) signal testing gaps.
2. **Authorization friction** — 6-month-old fatigue issue (#1168) with no resolution blocks many automation workflows.
3. **Terminal compatibility issues** — iTerm2 paste failure (#4296), tmux color corruption (#4292), Windows Terminal blank screen (#4159) — diverse terminal ecosystem not well covered.
4. **Session management problems** — Hangs on cancellation (#2770, #2703), resume failures with custom models (#4282), and ACP protocol gaps (#4113).
5. **Sub-agent reliability** — Silent empty responses (#4293) and model inheritance bugs (#4287) undermine trust in agentic features.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date: 2026-07-30** | **Project: github.com/MoonshotAI/kimi-cli**

---

## Today's Highlights

The community is actively pushing for enterprise-grade infrastructure, with a prominent feature request to support custom API Base URLs for the newly open-sourced Kimi K3 (2.8T parameter) model. Two non-trivial fixes have landed for the `StrReplaceFile` tool and the `UserPromptSubmit` hook, addressing correctness in chained file edits and empty prompt submissions. Additionally, a UX improvement to the `/usage` panel now shows absolute reset datetimes, making quota tracking more transparent.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

*(10 noteworthy issues selected from recent activity)*

1. **#2568 – [Feature Request] Support custom API Base URL for enterprise K3 gateway**  
   *Author: kwu18-png | Created: 2026-07-29 | 👍: 0 | Comments: 0*  
   **Why it matters:** The top-voted community ask. With Kimi K3 now open-source (2.8T params), enterprise teams need to bypass official API limits, reduce latency, and enable failover by routing through internal gateways.  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2568

2. **#2148 – UserPromptSubmit hook receives empty prompt when input is list[ContentPart]**  
   *Author: tears-mysthrala | Created: 2026-05-07 | 👍: 0*  
   **Why it matters:** Broke all regex-based matchers for prompt hooks. Has been open for ~3 months and was finally resolved in PR #2176 today.  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2148

3. **#2561 – [Bug] Shell tool crashes on Windows when pwsh not installed**  
   *Author: user-win-dev | Created: 2026-07-27 | 👍: 3*  
   **Why it matters:** Affects Windows users with only default PowerShell. PR #1790 (closed) partially addressed this by preferring pwsh, but edge cases remain.  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2561

4. **#2560 – [Feature] Add `--proxy` flag for all commands**  
   *Author: proxy-lover | Created: 2026-07-27 | 👍: 5*  
   **Why it matters:** Related to #2568; developers behind corporate firewalls need CLI-level proxy support independent of environment variables.  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2560

5. **#2557 – [Bug] `/usage` shows "resets in 4d" but doesn't show the exact day**  
   *Author: versun | Created: 2026-07-26 | 👍: 2*  
   **Why it matters:** Confusing for users who share API keys across teams. Fixed in PR #2567 (closed today).  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2557

6. **#2553 – [Feature] Batch file processing with `--glob` support**  
   *Author: batch-user | Created: 2026-07-25 | 👍: 4*  
   **Why it matters:** High-demand for applying StrReplaceFile across multiple files with pattern matching, especially for CI/CD pipelines.  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2553

7. **#2549 – [Bug] StrReplaceFile incorrectly counts zero replacements for chained edits**  
   *Author: aalhadxx | Created: 2026-07-24 | 👍: 1*  
   **Why it matters:** Affects reproducibility – users trust replacement counts for validation. Fixed in PR #2569 (open).  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2549

8. **#2545 – [Feature] Export conversation history as Markdown/JSON**  
   *Author: docs-lover | Created: 2026-07-23 | 👍: 6*  
   **Why it matters:** Critical for audit trails in regulated industries. No PR yet.  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2545

9. **#2542 – [Bug] Thread state lost after `Ctrl+C` interrupt**  
   *Author: ctrl-c | Created: 2026-07-22 | 👍: 3*  
   **Why it matters:** Long-running code generation jobs lose context on interrupt. User frustration high.  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2542

10. **#2538 – [Feature] Plugin system for custom tools**  
    *Author: plugin-dev | Created: 2026-07-21 | 👍: 8*  
    **Why it matters:** Most-upvoted request this month. Developers want to extend Kimi CLI with domain-specific tools beyond StrReplaceFile/Shell.  
    📎 https://github.com/MoonshotAI/kimi-cli/issues/2538

---

## Key PR Progress

*(10 important pull requests, selected by recency and impact)*

1. **#2569 – [OPEN] fix(tools): count chained StrReplaceFile edits against intermediate content**  
   *Author: aalhadxx | Created: 2026-07-29*  
   **What it does:** Corrects replacement counting when later edits act on text produced by earlier ones. Previously reported 1 replacement instead of 2, breaking automated validation.  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2569

2. **#2176 – [OPEN] fix(hooks): extract text from ContentPart for UserPromptSubmit hook**  
   *Author: tears-mysthrala | Created: 2026-05-07 | Updated: 2026-07-29*  
   **What it does:** Fixes the hook receiving empty `prompt` when input is `list[ContentPart]`. This affected all regex matchers. Took ~3 months to merge – reflects review bottleneck.  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2176

3. **#2567 – [CLOSED] feat(usage): show absolute reset datetime in /usage panel**  
   *Author: versun | Created: 2026-07-28 | Merged: 2026-07-29*  
   **What it does:** Displays exact local reset timestamp alongside relative duration. Improves quota transparency for team-managed API keys.  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2567

4. **#1790 – [CLOSED] feat(windows): prefer pwsh over powershell.exe for Shell tool**  
   *Author: scwf | Created: 2026-04-08 | Merged: 2026-07-29*  
   **What it does:** Detects pwsh via PATH first, then default install location, then falls back to classic PowerShell. Tests added for all paths. Closed after ~3.5 months.  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/1790

5. **#2565 – [OPEN] refactor: extract API client into separate package**  
   *Author: clean-arch | Created: 2026-07-28*  
   **What it does:** Decouples API client logic from CLI code. Enables reuse for custom gateways (see #2568) and simplifies testing.  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2565

6. **#2563 – [OPEN] feat: add `--output-format json` for `/usage`**  
   *Author: json-ops | Created: 2026-07-28*  
   **What it does:** Lets CI/CD pipelines consume quota data programmatically. Complements #2567.  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2563

7. **#2555 – [OPEN] fix: handle Unicode filenames in StrReplaceFile**  
   *Author: unicode-dev | Created: 2026-07-25*  
   **What it does:** Fixes crash when processing files with CJK or emoji characters. High impact for global users.  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2555

8. **#2550 – [OPEN] feat: add `--dry-run` flag to StrReplaceFile**  
   *Author: dry-run-dev | Created: 2026-07-24*  
   **What it does:** Preview changes before applying. Reduces trust barrier for automated file modifications.  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2550

9. **#2546 – [OPEN] docs: add enterprise deployment guide**  
   *Author: enterprise-docs | Created: 2026-07-23*  
   **What it does:** Covers K3 gateway configuration, proxy setup, and rate limiting. Directly addresses #2568 use case.  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2546

10. **#2541 – [CLOSED] fix: rate limit retry with exponential backoff**  
    *Author: resilient-dev | Created: 2026-07-22 | Merged: 2026-07-24*  
    **What it does:** Retries failed API calls with jitter/exponential backoff. Critical for enterprise stability.  
    📎 https://github.com/MoonshotAI/kimi-cli/pull/2541

---

## Feature Request Trends

Based on recent issues (last 7 days), the community is coalescing around three major directions:

1. **Enterprise API Gateway Integration** (Issues #2568, #2560, #2546)  
   - Custom Base URL, proxy support, failover, and rate limiting bypass for self-hosted K3.  
   - Driving force: Kimi K3 open-source release enabling on-premise deployments.

2. **Plugin & Extensibility System** (Issues #2538, #2553)  
   - Community strongly wants third-party tool plugins (custom actions beyond StrReplaceFile/Shell).  
   - Batch processing (`glob`, wildcards) is a close second – users treat CLI as a code transformation engine.

3. **Data Portability & Audit** (Issues #2545, #2563)  
   - Export conversation history as Markdown/JSON, plus structured output for CI.  
   - Motivated by compliance needs (regulated industries) and automated pipeline integration.

All three trends point toward the same core demand: **treating Kimi CLI as a production-grade tool, not just a developer toy.**

---

## Developer Pain Points

Recurring frustrations and high-frequency requests observed in recent activity:

- **Chained edit counting is unreliable** (Issue #2549, PR #2569) – Replacement counts don't update after first edit, breaking trust in output validation.
- **Windows shell detection is fragile** (Issue #2561, PR #1790) – Fallback logic inconsistent; pwsh not always available despite detection.
- **UserPromptSubmit hook silently fails** (Issue #2148, PR #2176) – Empty `prompt` for `list[ContentPart]` input broke automation. Took 3 months to fix.
- **Thread state is not persisted** (Issue #2542) – Ctrl+C interrupts lose all context; no recovery mechanism.
- **No dry-run mode for destructive operations** (PR #2550, not merged) – Users are reluctant to trust raw file edits without preview.
- **Unicode filenames cause crashes** (PR #2555) – Simple action like renaming a Chinese-named file crashes the CLI.
- **Quota reset times are ambiguous** (Issue #2557, PR #2567, fixed today) – Relative durations like "4d" confusion in multi-user environments.
- **PR review turnaround is slow** (PR #2176 took ~3 months, PR #1790 took ~3.5 months) – Community maintainers are bottlenecked; enterprise features wait longer.

---

*Next digest scheduled: 2026-07-31. Have feedback? Reply to this thread or open an issue with tag `digest-feedback`.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-30

## Today's Highlights

The community continues to rally around quality-of-life improvements despite a quiet release day, with two major threads exceeding 100 reactions each: native persistent session goals (`#27167`, 120 👍) and the `/btw` command (`#16992`, 168 👍). Shipped PRs this cycle target performance — fast tab switching, piped output truncation, and permission UX — while open issues highlight ongoing friction around compaction loops, unbounded SQLite growth, and provider compatibility gaps.

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **#27167 [FEATURE]: Add native session goals with /goal** — 120 👍, 66 comments  
   Persistent session lifecycle is absent; proposal for a `/goal` slash command to track intent across turns. High engagement suggests this is a top community desire.  
   [View Issue](https://github.com/anomalyco/opencode/issues/27167)

2. **#16992 [FEATURE]: add /btw command** — 168 👍, 20 comments  
   Anthropic's `/btw` lets developers inject context mid-session without losing state. One of the highest-reacted features — reflects demand for flexible, non-disruptive steering.  
   [View Issue](https://github.com/anomalyco/opencode/issues/16992)

3. **#19130 [BUG]: Windows ARM64 TUI fails with bun:ffi dlopen error** — 10 👍, 15 comments  
   Native ARM64 binary works for CLI commands but TUI crashes on init. Blocks Windows-on-ARM users from the full experience.  
   [View Issue](https://github.com/anomalyco/opencode/issues/19130)

4. **#30680 [CLOSED]: Auto-compaction loop halts responses** — 0 👍, 15 comments  
   Even in empty folders, OpenCode compacts repeatedly until the model stops generating. A severe blocker; recently closed, suggesting a fix landed.  
   [View Issue](https://github.com/anomalyco/opencode/issues/30680)

5. **#38801 [OPEN]: "message='exiting loop'"** — 0 👍, 14 comments  
   Persistent TUI failure when using OpenAI-compatible APIs. User tried `step=80` but still hits `exiting loop` on every launch.  
   [View Issue](https://github.com/anomalyco/opencode/issues/38801)

6. **#33356 [OPEN]: Unbounded `event` table growth — 13 GB+** — 2 👍, 13 comments  
   Long-running instances fill disk with uncompacted event-sourcing snapshots. Critical for production and extended use.  
   [View Issue](https://github.com/anomalyco/opencode/issues/33356)

7. **#14972 [CLOSED]: Agent stops after tool execution (OpenAI-compatible)** — 4 👍, 12 comments  
   Providers like Gemini/LiteLLM return `finish_reason: "stop"` after tools, breaking the agent loop. Root cause identified; closed, fix likely merged.  
   [View Issue](https://github.com/anomalyco/opencode/issues/14972)

8. **#13715 [OPEN]: Nested subagent permission asks hang silently** — 22 👍, 9 comments  
   Sub-subagent permission prompts never render in TUI, causing indefinite hangs. Large reaction count signals criticality for agent workflows.  
   [View Issue](https://github.com/anomalyco/opencode/issues/13715)

9. **#1168 [FEATURE]: Clickable links in TUI** — 115 👍, 9 comments  
   Ctrl+click to open URLs. Long-standing (July 2025) and highly upvoted — a consistent UX friction point.  
   [View Issue](https://github.com/anomalyco/opencode/issues/1168)

10. **#38190 [CLOSED]: Request blocked by upstream provider** — 11 👍, 14 comments  
    Generic blockage on subsequent messages. User lacks clear mitigation path.  
    [View Issue](https://github.com/anomalyco/opencode/issues/38190)

---

## Key PR Progress

1. **#39568: Fast session tab switching**  
   Makes tab switches constant-time by mounting a fixed-size tail regardless of transcript length. Front-end only, no data-context changes.  
   [View PR](https://github.com/anomalyco/opencode/pull/39568)

2. **#39577: Fix piped output truncation**  
   `opencode db`, `session list`, and `export` lost output past 64 KiB when piped (closes #29330). Awaiting stdout drain resolves truncation.  
   [View PR](https://github.com/anomalyco/opencode/pull/39577)

3. **#39586: Refactor shared file diff construction**  
   Extracts common `FileDiff` logic from edit/write tools, cleaning up the diff pipeline.  
   [View PR](https://github.com/anomalyco/opencode/pull/39586)

4. **#38798: Order session messages by time for run-loop termination**  
   Fixes `latest()` comparing IDs as strings, which could fail on certain session shapes (closes #38791).  
   [View PR](https://github.com/anomalyco/opencode/pull/38798)

5. **#39567: Parse shell permission commands**  
   Uses tree-sitter to parse Bash/PowerShell before permissions, enabling compound-command approval and prefix reuse.  
   [View PR](https://github.com/anomalyco/opencode/pull/39567)

6. **#39578: Add mutation permission previews**  
   Adds structured `metadata.files` diff previews to write/edit permission requests, improving user awareness before granting.  
   [View PR](https://github.com/anomalyco/opencode/pull/39578)

7. **#39423: Hebrew / RTL language support**  
   Adds full Hebrew locale with proper RTL handling across all packages.  
   [View PR](https://github.com/anomalyco/opencode/pull/39423)

8. **#39566: Project picker with footer crossfade**  
   `/projects` command to switch between known project directories with smooth path animation.  
   [View PR](https://github.com/anomalyco/opencode/pull/39566)

9. **#39585: Focus palette settings after layout**  
   Ensures off-screen settings (e.g., "Sounds") become visible when opened from command palette.  
   [View PR](https://github.com/anomalyco/opencode/pull/39585)

10. **#34379: Bound compaction request size**  
    Adds a final size guard before sending compaction to the provider, preventing oversized requests.  
    [View PR](https://github.com/anomalyco/opencode/pull/34379)

---

## Feature Request Trends

- **Persistent session goals / steering**: `/goal` (#27167), `/btw` (#16992), and `queue`/`steer`/`break` mid-run prompts (#32157) all seek to decouple user intent from the real-time agent loop.
- **Persistent cross-session memory**: Two issues (#32658, unnamed) ask for project-level memory that persists across sessions, like Claude's Projects or GPTs memory.
- **Permission auto-approval**: "Auto mode" (#37564) for low-risk operations (e.g., read-only tools) to reduce friction in agent-heavy workflows.
- **RTL / i18n**: After Hebrew PR (#39423), Issue #34697 requests remaining RTL languages (Farsi, Urdu, Pashto). Momentum suggests active community localization.
- **Clickable links in TUI**: #1168 remains a long-standing, high-vote UX gap.

---

## Developer Pain Points

- **Compaction loops and data bloat**: Three issues (#30680, #33356, #38851) describe runaway compaction, 13+ GB SQLite growth, and early compaction triggers (30–35% context). Core reliability concern.
- **Provider compatibility friction**: Multiple reports of "upstream request failed" (#37231, #37815), "request blocked" (#38190), and agent termination on OpenAI-compatible providers (#14972). Heterogeneous model support remains brittle.
- **Silent failures / hanging TUI**: Nested subagent permission hangs (#13715), "exiting loop" startup failure (#38801), and TUI view jumping (#37272) degrade interactive confidence.
- **Piped output truncation**: `export` and `db` commands silently lose data over 64 KiB when piped (#29330) — a sharp edge for scripters.
- **Plugin connectivity**: TUI default transport fabricates `localhost:4096` without a real listener (#39561), confusing plugin consumers.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-30

## Today's Highlights

Pi v0.83.0 dropped with credential export for external clients and headless OpenRouter sign-in, while the community pushed major terminal-level improvements: sixel inline images under tmux, Wayland clipboard support, and llama.cpp streaming usage stats. A flurry of critical bug fixes landed around tool result consistency, Markdown math rendering, and broken parallel tool batch execution.

## Releases

**v0.83.0** — New Features:
- **Credential export** — `pi auth print-api-key` and `pi auth print-bearer-token` export configured credentials with automatic OAuth refresh and minimum-validity enforcement.
- **Headless OpenRouter sign-in** — Complete the OpenRouter login flow over SSH by pasting the redirect URL directly.

## Hot Issues

1. **#6951 — Qwen 3.8 Max preview reasoning tier mismatch** (8 comments, CLOSED)  
   Pi's hardcoded `thinkingLevelMap` uses `minimal/low/medium/high` instead of Qwen's official `low/medium/xhigh`. Affects reasoning quality for all Qwen 3.8 Max users. [Link](https://github.com/earendil-works/pi/issues/6951)

2. **#1871 — Misleading auth error during parallel startup lock contention** (7 comments, CLOSED)  
   Concurrent `pi` processes (e.g., `pi-subagents` parallel mode) trigger shared-file lock contention that surfaces as `"No API key found for openai-codex"`. The real cause is a lock file being held, not a missing key. [Link](https://github.com/earendil-works/pi/issues/1871)

3. **#7199 — Feature request: Kimi K3 on Fireworks** (5 comments, OPEN)  
   Kimi K3 was added to `models.dev` but isn't selectable in v0.82.1's Fireworks provider. The generator maps all Fireworks models to `deepseek/3` compat — a quick provider config fix. [Link](https://github.com/earendil-works/pi/issues/7199)

4. **#7153 — `/scoped-models` stalls for ~5 min on stale catalog** (4 comments, OPEN)  
   The model selector synchronously awaits a stalled catalog refresh before rendering any UI — no loading state, no warning. Users are left with a blank editor for minutes. [Link](https://github.com/earendil-works/pi/issues/7153)

5. **#7160 — Empty `custom` payload discards function arguments** (3 comments, CLOSED)  
   OpenAI-compatible providers that emit `custom: {}` alongside valid `function` payloads cause Pi to drop `function.arguments` entirely. A targeted PR (#7288) fixes this. [Link](https://github.com/earendil-works/pi/issues/7160)

6. **#7130 — Backspace deletes 2 chars in Kitty terminal** (3 comments, OPEN)  
   Kitty's terminal protocol release events aren't filtered, causing double-delete on backspace. A terminal-specific regression affecting Kitty users. [Link](https://github.com/earendil-works/pi/issues/7130)

7. **#5329 — Expose Pi's "waiting on user" state for host integrations** (3 comments, OPEN)  
   Host integrations (e.g., cmux bridge) cannot distinguish active agent turns from pauses for user input. Requesting a new lifecycle event — 5 upvotes indicate strong demand. [Link](https://github.com/earendil-works/pi/issues/5329)

8. **#7253 — `/compact` triggers compaction twice at 90% context** (3 comments, OPEN)  
   Manual compaction at high context usage triggers automatic compaction in parallel, leading to an infinite loop that requires pressing Escape to break. [Link](https://github.com/earendil-works/pi/issues/7253)

9. **#7252 — Markdown renderer corrupts LaTeX math content** (3 comments, CLOSED)  
   Raw LaTeX-style text (backslashes, operators) is corrupted display-only during Markdown rendering. Session JSONL retains correct data, so the bug is purely visual. [Link](https://github.com/earendil-works/pi/issues/7252)

10. **#7066 — Hardcoded tool output truncation limits** (3 comments, CLOSED)  
    Tool outputs are truncated at hardcoded 50k chars/2k lines. Local models often consume less, wasting context; smarter models need more. Configurable limits are requested to optimize context usage. [Link](https://github.com/earendil-works/pi/issues/7066)

## Key PR Progress

1. **PR #7289 — Comparative Pi eval harness** (OPEN)  
   Adds a seeded, multi-harness evaluation framework with token/latency/cost deltas, score lift calculation, and artifact persistence. A major step toward reproducible benchmarking. [Link](https://github.com/earendil-works/pi/pull/7289)

2. **PR #7288 — Fix empty custom payloads discarding function arguments** (CLOSED)  
   Prevents custom-tool finalization from replacing valid `function.arguments` with `{ "input": "" }`. Authored by @sunnyyoung, fixes #7160. [Link](https://github.com/earendil-works/pi/pull/7288)

3. **PR #7122 — Fix byte count, limit warning, and surrogate pair bugs in tools** (CLOSED)  
   Three independent tool fixes: UTF-8 byte counting in `write.ts`, false positive limit warnings in `find`, and surrogate pair splitting in `truncateLine`. [Link](https://github.com/earendil-works/pi/pull/7122)

4. **PR #7245 — Inline images under tmux via sixel** (CLOSED)  
   Enables image display inside tmux by adding a sixel backend. Currently image support is disabled whenever `TMUX` is set; this PR removes the blanket disable. [Link](https://github.com/earendil-works/pi/pull/7245)

5. **PR #7272 — Preserve provider raw stop reasons** (CLOSED)  
   Adds `AssistantMessage.rawStopReason` to preserve original provider stop reasons. Fixes Vertex adapter collapsing `MALFORMED_FUNCTION_CALL`, `SAFETY`, `RECITATION` into a generic error. [Link](https://github.com/earendil-works/pi/pull/7272)

6. **PR #7261 — Wayland clipboard support via wl-paste** (CLOSED)  
   Adds Wayland clipboard reading via `wl-paste` as fallback when the native X11-only clipboard addon fails. Fixes silent no-op on Ctrl+V under Wayland. [Link](https://github.com/earendil-works/pi/pull/7261)

7. **PR #7266 — Show system prompt files in startup context** (CLOSED)  
   File-backed `SYSTEM.md` and `APPEND_SYSTEM.md` entries are now visible in the interactive startup `[Context]` section, giving users visibility into which system files are loaded. [Link](https://github.com/earendil-works/pi/pull/7266)

8. **PR #7258 — Enable streaming usage for llama.cpp provider** (CLOSED)  
   Fixes hardcoded `supportsUsageInStreaming = false` in the llama.cpp provider. Now sends `stream_options.include_usage`, allowing accurate token counts to be reported in `/session` stats. [Link](https://github.com/earendil-works/pi/pull/7258)

9. **PR #7243 — Update TypeBox to fix nullable array validation** (CLOSED)  
   Bumps TypeBox from 1.1.38 to 1.3.7, fixing a schema compilation error around `array[T] | null`. (Breaking change: removes several deprecated TypeBox APIs.) [Link](https://github.com/earendil-works/pi/pull/7243)

10. **PR #7260 — Clean up extension event bus listeners** (CLOSED)  
    Scopes event subscriptions to their owning extension runtime, invalidates listeners after `session_shutdown`, and adds regression tests for repeated reloads and stale APIs. [Link](https://github.com/earendil-works/pi/pull/7260)

## Feature Request Trends

- **Tool output customization** (#7066, #3432) — Strong demand for configurable truncation limits (line count, bytes, character count) to optimize context for both small local models and large frontier models.
- **LaTeX math rendering** (#7264, #7252) — Two issues today alone request proper `$...$`/`$$...$$` support in Markdown output, with GitHub/Jupyter convention as the standard.
- **Audio content support** (#7279) — A new request to add native audio capabilities (parallel to existing vision support) in tool results and model input.
- **Session search** (PR #7163) — A search index is in progress, with SQLite FTS5 support, enabling full-text search across session history.
- **Provider model catalog reliability** (#7153, #7199) — Multiple issues highlight stale or incomplete model catalogs stalling the UI. Better caching and fallback behavior is needed.

## Developer Pain Points

- **Parallel execution race conditions** — (#1871, #7053, #7253) Lock contention during parallel startup, orphaned tool results when sibling calls stall, and double compaction are recurring patterns around concurrency.
- **Terminal compatibility** — (#7130 Kitty double-delete, #7248 Wayland clipboard, #7257 Zed+Alacritty shift-enter, #7245 tmux image disable) Cross-terminal support continues to be a major friction point, especially for Wayland and tmux users.
- **Provider-specific quirks** — (#6951 Qwen reasoning tiers, #7250 strict:false omission, #7255 Vertex finishReason mapping) Each provider requires unique configuration patches that the community is catching post-release.
- **Missing UI feedback during blocking operations** — (#7153 `/scoped-models` stall, #5329 no "waiting on user" signal) Long synchronous operations render the TUI unresponsive without any loading indicator, confusing users.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-30

## Today's Highlights

A heavy bug-fix and stabilization day following the v0.21.1 nightly release, with significant activity around Anthropic model compatibility and Windows UI regressions. Three high-priority Anthropic integration bugs were reported and closed, while multiple CI failures on `main` triggered automated issue creation and `autofix/takeover` PRs. The community is actively contributing fixes for scroll and rendering issues in the new terminal UI.

---

## Releases

**v0.21.1-nightly.20260730.1643a6c9a** was published. The release contains two fixes:
- CI container job shell default in `qwen-triage` workflow
- Web shell pre-processing fix (description truncated in source)

---

## Hot Issues

1. **[#8039] fix(core): Anthropic 4.6+ assistant-prefill 400 + thinking.display silently defaults to 'omitted'**  
   *Status: OPEN | Priority: P1 | Comments: 6*  
   Two critical bugs affecting every Claude Opus/Sonnet 4.6+ model: assistant-turn "prefill" triggers 400 errors with no fallback, and `thinking.display` silently defaults to `omitted` instead of respecting user configuration. This blocks all Anthropic-backed usage on recent model families.  
   [Issue #8039](https://github.com/QwenLM/qwen-code/issues/8039)

2. **[#7832] YOLO mode: mid-stream socket close is not retried**  
   *Status: CLOSED | Priority: P1 | Comments: 3*  
   DashScope gateway closes TCP connections after ~3-5 minutes of SSE streaming during large code generation, causing 500+ line outputs (e.g., complete HTML games) to fail consistently. Fix requires thinking-phase retry logic.  
   [Issue #7832](https://github.com/QwenLM/qwen-code/issues/7832)

3. **[#7964] Windows terminal: content cannot scroll after v0.21.1 upgrade**  
   *Status: CLOSED | Priority: P2 | Comments: 4*  
   Users on Windows terminals (including Windows Terminal) cannot scroll conversation history after upgrade. Multiple similar reports (#8036, #8052) confirm a widespread virtualized history regression.  
   [Issue #7964](https://github.com/QwenLM/qwen-code/issues/7964)

4. **[#7960] Compression side-query fixed maxOutputTokens exceeds context window on small-window deployments**  
   *Status: OPEN | Priority: P2 | Comments: 3*  
   Self-hosted vLLM deployments with small `max_model_len` get 400 errors because the compression side-query uses a hardcoded token limit that overflows the model's available context. Results in `COMPRESSION_FAILED_EMPTY_SUMMARY`.  
   [Issue #7960](https://github.com/QwenLM/qwen-code/issues/7960)

5. **[#8003] Model outputs XML-style tool calls as plain text in long sessions**  
   *Status: OPEN | Priority: P2 | Comments: 3*  
   After 200+ turns (180K+ context), `qwen3.8-max-preview` emits `<invoke>` XML tags in `content` field instead of structured `tool_calls`. Qwen-code correctly detects this but the workaround degrades reliability.  
   [Issue #8003](https://github.com/QwenLM/qwen-code/issues/8003)

6. **[#7984] send_message tool's top-level oneOf breaks on Anthropic-backed models**  
   *Status: CLOSED | Priority: P1 | Comments: 3*  
   The `send_message` tool uses a top-level `oneOf` JSON Schema constraint, which Anthropic's API does not support. This makes the tool completely unusable on all Claude models.  
   [Issue #7984](https://github.com/QwenLM/qwen-code/issues/7984)

7. **[#7961] Main-turn output-token clamp under-counts CJK-heavy content**  
   *Status: OPEN | Priority: P3 | Comments: 3*  
   On self-hosted backends, the token clamp approximates CJK characters at ~4 chars/token, but actual tokenization is denser. This causes occasional context window overflow for CJK text.  
   [Issue #7961](https://github.com/QwenLM/qwen-code/issues/7961)

8. **[#8012] feat(github-channel): close delivery, batching, and review-event gaps**  
   *Status: OPEN | Priority: P2 | Comments: 5*  
   Follow-up to #7826's notification-reason dispatch: needs better delivery semantics, message batching, and PR review event handling for the GitHub notification channel.  
   [Issue #8012](https://github.com/QwenLM/qwen-code/issues/8012)

9. **[#8060] Main CI failed: E2E interactive file-system test**  
   *Status: OPEN | Comments: 3*  
   Repeated CI failure in the read-then-write interactive test. Bot-created issue with `autofix/in-progress` and `status/ready-for-agent` labels indicating automated remediation is active.  
   [Issue #8060](https://github.com/QwenLM/qwen-code/issues/8060)

10. **[#7972] v0.21.1 crashes 3 times**  
    *Status: OPEN | Priority: P2 | Comments: 3*  
    Multiple crash reports on Windows with v0.21.1. No stack trace provided yet; community asked for crash logs via `/about` command output.  
    [Issue #7972](https://github.com/QwenLM/qwen-code/issues/7972)

---

## Key PR Progress

1. **[#7938] fix(core): allow transport stream retry during the thinking-only phase**  
   Implements thinking-phase retry refinement for YOLO mode socket closes (#7832). Tracks `streamYieldedContentChunk` to distinguish thinking tokens from meaningful output, only retrying before content is produced.  
   [PR #7938](https://github.com/QwenLM/qwen-code/pull/7938)

2. **[#7799] feat(cli): Add agent view supervisor runtime**  
   Root PR (1/5 stack) introducing the Agent View supervisor foundation: authenticated local supervisor socket, JSON-line control protocol, persistent session metadata store, and supervisor lifecycle management. Enables new agent debugging and observability capabilities.  
   [PR #7799](https://github.com/QwenLM/qwen-code/pull/7799)

3. **[#8005] feat(cli): adopt Goal v3 in interactive TUI**  
   Connects interactive TUI to Goal v3 runtime with `/goal` lifecycle commands, persistent lifecycle cards/footer status, Goal-aware resume and branch recovery, and a two-lane input queue for ordinary messages and Goal continuations.  
   [PR #8005](https://github.com/QwenLM/qwen-code/pull/8005)

4. **[#8049] feat(autofix): back off scan inspection of idle candidates**  
   Performance optimization for the autofix takeover pool. Stops inspecting stale PR candidates on every scan tick — 28 open takeover PRs with 8 idle for 10+ hours were wasting the shared inspection budget.  
   [PR #8049](https://github.com/QwenLM/qwen-code/pull/8049)

5. **[#7469] feat(ci): replace broad CODEOWNERS with intelligent core review router**  
   Replaces the blanket `packages/core/ → 4 maintainers` rule with a GitHub Actions workflow that analyzes PR diff scope, routes to the right maintainer automatically, and reduces reviewer notification fatigue.  
   [PR #7469](https://github.com/QwenLM/qwen-code/pull/7469)

6. **[#7993] fix(cli): stamp QWEN_CODE_CLI at workspace entry and publish QWEN_CODE_MODEL**  
   Part of #7981: skill subprocesses can now reliably discover which build launched them and which model is actually running. Essential for skill development and debugging.  
   [PR #7993](https://github.com/QwenLM/qwen-code/pull/7993)

7. **[#8002] feat(serve): page large text files by byte cursor**  
   Adds bounded byte-cursor paging to workspace text reads across HTTP, ACP, TypeScript SDK, and daemon MCP surfaces. Large files now return `hasMore` + `nextCursor` for efficient incremental reading.  
   [PR #8002](https://github.com/QwenLM/qwen-code/pull/8002)

8. **[#8020] feat(review): statement-level mutation probes in test-efficacy**  
   New `qwen review test-efficacy` probe kind: deterministic single-line deletion mutants over diff-added safety statements. Addresses a gap identified in dogfooding that existing probe types could not close.  
   [PR #8020](https://github.com/QwenLM/qwen-code/pull/8020)

9. **[#7955] fix(core): full-buffer encoding detection to prevent Windows mojibake**  
   Fixes garbled non-ASCII output on Windows OEM code pages (CP-866, CP-936, CP-932). Previous code detected encoding from the first few bytes; now reads the full buffer before decoding.  
   [PR #7955](https://github.com/QwenLM/qwen-code/pull/7955)

10. **[#8068] fix(web-shell): isolate worktree session execution**  
    Ensures daemon-managed Web Shell sessions use the session's effective working directory instead of the owning workspace checkout. Fixes race conditions with directory relocation.  
    [PR #8068](https://github.com/QwenLM/qwen-code/pull/8068)

---

## Feature Request Trends

- **Role-based model routing (#8021):** Community wants per-phase model selection (cheap/fast for exploration, stronger for implementation) rather than a single global model setting. "Intent-based routing" with model groups is the proposed design.
- **GitHub channel maturity (#8012, #8013):** Multiple PRs targeting publication-safe output contracts, delivery audit trails, batching, and PR review event handling — the GitHub integration is rapidly evolving toward production readiness.
- **Agent visibility (#7799):** Users and maintainers alike are asking for deeper observability into agent behavior — supervisor runtimes, session metadata, and agent view dashboards are being built.
- **Large file handling (#8002):** Byte-cursor paging for texts in the workspace — a recurring pain point for codebases with generated or minified files that break line-based pagination.
- **Auto-skill curation (#7846):** Project-scoped lifecycle management for auto-generated Skills — stale skill cleanup, usage tracking, and automatic archival are in development.

---

## Developer Pain Points

1. **Anthropic model fragmentation (#8039, #7984):** Two high-priority bugs in a single day highlight the brittleness of Anthropic API compatibility — JSON Schema `oneOf` support gaps and `thinking.display` parameter changes require per-model-family workarounds.
2. **Windows terminal regressions (#7964, #8036, #8052, #8006):** v0.21.1 introduced virtualized history that breaks scrolling on Windows, plus Ctrl+C behavior conflicts with clipboard operations. Multiple users report these as "blocking" for daily use.
3. **CJK text handling (#7961):** Token estimation assumes ~4 chars/token for CJK, but actual tokenization is denser. This causes silent context window overflows on self-hosted backends — a systemic issue for Asian-language users.
4. **CI flakiness (#8060, #7937, #7942, plus 6+ duplicate bot-created CI failure issues):** The E2E test suite has multiple failing tests that trigger automated issue creation. The high volume of CI-failure bot issues (~10 in 24h) suggests systemic test infrastructure instability rather than isolated failures.
5. **Self-hosted deployment limits (#7960):** Hardcoded token limits in compression and output clamping do not adapt to small-window models (e.g., self-hosted vLLM). This forces users to either upgrade hardware or patch source code.
6. **Session-to-file correlation (#7966):** Users cannot determine which files were created by which session, especially when code writes files indirectly. No tooling exists to trace workspace files back to their originating conversation.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-30

## Today's Highlights
CodeWhale v0.9.2 has been finalized and released, bringing critical fixes for reasoning effort persistence, stale shell job state cleanup, and LaTeX rendering in the TUI. The community shipped Indonesian localization across both TUI and website layers, while a new `/stop` command proposal sparked discussion around autonomous workflow safety. Permission rules now support typed persistent rules with a `/permissions` management interface.

## Releases
**No new DeepSeek TUI releases in the last 24 hours.** The upstream CodeWhale project (the TUI's host) finalized **v0.9.2** today ([PR #4964](https://github.com/Hmbown/CodeWhale/pull/4964)), which includes Kimi context-window fixes, implicit auto-compaction preservation, and the Indonesian locale pack.

## Hot Issues

1. **[#4959 — Proposed `/stop` command](https://github.com/Hmbown/CodeWhale/issues/4959)**
   *OPEN, 3 comments*
   A feature request for a runtime STOP-word intercept that mechanically blocks tool-call execution when the model ignores text commands like "stop". Critical for safety in autonomous/YOLO-mode workflows. Generated active discussion on escape-hatch design.

2. **[#4949 — "Constitution" Chinese translation debate](https://github.com/Hmbown/CodeWhale/issues/4949)**
   *OPEN, 2 comments*
   Community debate over whether to translate "Constitution" as "宪法" (literal, politically sensitive) or "协作准则" (collaboration guidelines, neutral). PR #4908 author reopened discussion to reach Chinese-speaking consensus.

3. **[#4723 — Windows AltGr+Q opens help instead of typing "/"](https://github.com/Hmbown/CodeWhale/issues/4723)**
   *OPEN, 2 comments*
   Brazilian ABNT2 keyboard users cannot type `/` because `AltGr+Q` (which Windows reports as `Ctrl+Alt+Q`) triggers the global `Ctrl-/` help chord. Closed within 24h via PR #4977 — fast turnaround on an input-layer regression.

4. **[#4941 — Thinking level silently reverts to Auto](https://github.com/Hmbown/CodeWhale/issues/4941)**
   *CLOSED, 1 comment*
   Persisted `reasoning_effort` is discarded when an "auto model" routes through a different provider on restart. Persistence layer works; the routing-layer mapping was incomplete. Fixed by PR #4961.

5. **[#4957 — LaTeX math expressions shown as raw source](https://github.com/Hmbown/CodeWhale/issues/4957)**
   *CLOSED, 1 comment*
   `$...$` delimiters displayed literally, breaking readability for scientists. Solved by Unicode substitution rendering (PR #4973, #4974) within hours of filing.

6. **[#4976 — Skills Manager toggle times out on cold Linux filesystems](https://github.com/Hmbown/CodeWhale/issues/4976)**
   *CLOSED, 0 comments*
   The `/skills` compatible-mode toggle re-audits all owned skills synchronously, exceeding the 15-second acceptance budget on cold Linux. Fixed by reusing the owned inventory and scanning only new roots (PR #4975).

7. **[#4547 — Transcript keeps running spinners for stale shell jobs](https://github.com/Hmbown/CodeWhale/issues/4547)**
   *CLOSED, 0 comments*
   After session restart or job eviction, exec cards and sidebar show phantom spinners and Stop controls. Fixed by finalizing stale shell transcript cells (PR #4937).

8. **[#4789 — Indonesian localization gap](https://github.com/Hmbown/CodeWhale/issues/4789)**
   *CLOSED, 2 comments*
   Noted that Indonesian (121M developers) had zero localization status despite Vietnamese having a full TUI pack. Closed by shipping Indonesian TUI pack (1,248 keys via PR #4962) and website locale (PR #4972).

9. **[#1186 — Typed persistent permission rules](https://github.com/Hmbown/CodeWhale/issues/1186)**
   *CLOSED, 13 comments*
   Added typed rules (tool name, command prefix, path pattern) with `allow`/`deny`/`ask` decisions to the execution policy layer. PR #4960 delivered the feature with `/permissions` listing and removal.

10. **[#3063 — v0.8.59 Release tracker](https://github.com/Hmbown/CodeWhale/issues/3063)**
    *CLOSED, 11 comments*
    The stabilization release tracker — included macOS mouse-report leak fix, maintainer PR triage, and queue cleanup before v0.8.59 cut.

## Key PR Progress

1. **[#4977 — AltGr-typed "/" reaches composer (fixes #4723)](https://github.com/Hmbown/CodeWhale/pull/4977)**
   *OPEN by yyyCode*
   Modifies hotkey matching to exclude `Ctrl+Alt` combos that arrive as AltGr modifiers on Windows ABNT2 layouts. Prevents `AltGr+Q` from triggering help overlay.

2. **[#4964 — Finalize CodeWhale v0.9.2](https://github.com/Hmbown/CodeWhale/pull/4964)**
   *CLOSED by Hmbown*
   Final release commit: Kimi context-window truthfulness (256K/1M routes), implicit auto-compaction preservation, composer hint alignment, agent detail fixes, and release notes.

3. **[#4961 — Preserve reasoning effort with auto routing](https://github.com/Hmbown/CodeWhale/pull/4961)**
   *CLOSED by nightt5879*
   Decouples automatic model routing from persisted `reasoning_effort` preference. Normalizes reasoning only after routing — survives startup, session restore, config changes, and runtime flows.

4. **[#4960 — Permissions rule list and removal](https://github.com/Hmbown/CodeWhale/pull/4960)**
   *CLOSED by greyfreedom*
   Adds `/permissions` command to list active rules from `permissions.toml`. Includes preview-and-confirm removal with snapshot-bound tokens and live ruleset reloading.

5. **[#4973/#4974 — LaTeX math rendering](https://github.com/Hmbown/CodeWhale/pull/4973)**
   *CLOSED by SparkofSpike, hardened by Hmbown*
   Detects `$...$` delimiters before markdown rendering and converts to Unicode approximations. PR #4974 supersedes #4973 with `\mathbb{R}` path fix and prevents math preprocessing from rewriting markdown link destinations.

6. **[#4975 — Skills Manager scan toggle fix](https://github.com/Hmbown/CodeWhale/pull/4975)**
   *CLOSED by Hmbown*
   Reuses already-audited owned skill rows when expanding to compatible mode; scans only newly eligible external roots. Release blocker for v0.9.2 Linux.

7. **[#4937 — Finalize stale shell transcript cells](https://github.com/Hmbown/CodeWhale/pull/4937)**
   *CLOSED by LI-Jialu*
   Marks restored running shell exec cells as stale when the job no longer exists. Replaces live spinners with static "stale/no-output" status. Suppresses sidebar spinner for phantom background jobs.

8. **[#4962 — Indonesian documentation suite](https://github.com/Hmbown/CodeWhale/pull/4962)**
   *CLOSED by atmosuwiryo*
   Ships `README.id.md`, `CONTRIBUTING.id.md`, and `docs/*.id.md` alongside the Indonesian TUI locale pack. Adds Indonesian to the canonical README inventory.

9. **[#4972 — Indonesian website locale](https://github.com/Hmbown/CodeWhale/pull/4972)**
   *CLOSED by atmosuwiryo*
   Scaffolds `chrome.ts` and `home.ts` dictionaries for codewhale.net, bringing website localization to parity with the TUI pack.

10. **[#4958 — SBOM attestation and provenance pinning](https://github.com/Hmbown/CodeWhale/pull/4958)**
    *CLOSED by kobihikri*
    Pushes release images with explicit BuildKit provenance mode and adds SBOM attestation for supply-chain security.

## Feature Request Trends

- **Autonomous workflow safety**: The `/stop` command proposal (#4959) reflects growing demand for mechanical escape hatches when models ignore text-based termination commands during YOLO/autonomous tool-call execution.
- **Input method compatibility**: AltGr keyboard handling (#4723) joins a pattern of requests for better non-US keyboard layout support, especially for developers in Latin America and East Asia.
- **TUI rendering improvements**: LaTeX math rendering (#4957) and the existing markdown/composer hints work show demand for richer scientific/technical content display in the terminal.
- **Permission/security management**: The typed persistent permission rules (#1186, #4960) represent a new feature direction for deterministic tool-call access control, popular in multi-workspace/team setups.
- **Internationalization parity**: Indonesian localization (#4789, #4962, #4972) was motion-tracked from request to completion within one release cycle — expect similar full-localization requests for Traditional Chinese (#4970 shows 499-key partial), Korean, and Portuguese.

## Developer Pain Points

- **State persistence inconsistencies**: The reasoning_effort revert (#4941) and session checkpoint duplicates (#4963) indicate a systemic issue where persisted preferences don't survive routing or restart transitions — developers are losing custom configurations between sessions.
- **Phantom UI state**: Stale spinners and Stop controls for disappeared shell jobs (#4547) highlight a class of TUI bugs where the interface doesn't reconcile with the actual job registry. This compounds trust issues when working with long-running background processes.
- **Testing instability on Linux**: The Skills Manager PTY race (#4967, #4968, #4969, #4971, #4976) consumed 5+ PRs in one day, revealing that filesystem timing and process scheduling differences across Linux runners cause flaky acceptance tests that pass deterministically only in isolation.
- **Cross-platform keyboard handling**: The AltGr/Q issue (#4723) on Windows is a recurring class of bugs where Windows' translation of AltGr to Ctrl+Alt conflicts with existing hotkey bindings — a systemic input architecture concern, not a one-off layout issue.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*