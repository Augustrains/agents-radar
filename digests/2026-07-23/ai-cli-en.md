# AI CLI Tools Community Digest 2026-07-23

> Generated: 2026-07-23 01:26 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Comparison Report
**Date:** 2026-07-23

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem shows a mature and rapidly evolving landscape, with seven major players demonstrating distinct development velocities and community dynamics. Today's activity reveals a sector grappling with growing pains: Windows platform instability, MCP protocol reliability issues, and subagent lifecycle management are universal pain points. Claude Code leads in community engagement (50+ open issues) and feature velocity, while OpenAI Codex shows intense Rust-alpha iteration (4 releases in 24 hours). A clear divergence is emerging between tools optimizing for enterprise reliability (Gemini CLI, Copilot CLI) versus those racing on feature surface expansion (Claude Code, Pi). The ecosystem is converging on shared architectural patterns—background subagents, context compaction, and structured tool execution—while each tool differentiates on permission models, model support breadth, and platform maturity.

---

## 2. Activity Comparison

| Tool | Open Issues (Today) | Open PRs (Today) | Releases (24h) | Community Engagement Signal |
|------|-------------------|------------------|----------------|---------------------------|
| **Claude Code** | 50 | 10 | 1 (v2.1.218) | Highest engagement; 12 doc issues filed in one day |
| **OpenAI Codex** | ~34 (top 10 shown) | 10 (all closed) | 4 (rust alphas) | Intense Rust iteration; 151 👍 on single feature request |
| **Gemini CLI** | ~28 (top 10 shown) | 10 | 2 (stable + preview) | Balanced; security-focused nightly patch |
| **Copilot CLI** | 34 | 1 | 3 (patch fixes) | Lowest PR activity; Windows stability crisis |
| **Kimi Code CLI** | ~10 (top shown) | 3 | 0 | Quiet day; critical third-party compatibility fix in progress |
| **OpenCode** | ~30 (top 10 shown) | 10 | 0 | High frustration; subscription meltdown dominating |
| **Pi** | 50 (total updated) | 29 | 0 | Highest volume day; retry/abort fixes prominent |
| **Qwen Code** | ~10 (top shown) | 10 | 0 (nightly failed) | CI instability blocking all progress |
| **DeepSeek TUI** | ~10 (top shown) | 10 (8 merged) | 0 (v0.9.1 pending) | Close to release; security gate blocking |

**Key observations:**
- Claude Code and Pi have the most active issue trackers
- OpenAI Codex has the highest release cadence (4 alphas/day)
- Copilot CLI has the least PR throughput (1 stale open PR)
- DeepSeek TUI is closest to a major release (v0.9.1 blocked only by security audit)

---

## 3. Shared Feature Directions

| Theme | Tools Involved | Specific Community Needs |
|-------|---------------|-------------------------|
| **Mid-task steering / message injection** | Claude Code (#71726), Codex CLI, Gemini CLI (#25166) | Inject messages between tool calls without waiting for turn completion |
| **Per-agent model selection** | Kimi Code (#2533), OpenCode (#37226), Claude Code (plugin system) | Assign different models to subtasks for cost optimization |
| **Context compaction & budget management** | Claude Code (#80196), Copilot CLI (#4183), Pi (#6768), DeepSeek TUI (#4704) | Auto-compaction triggers, hard serialization limits, token budget visibility |
| **MCP/subprocess lifecycle reliability** | Claude Code (#79992, #80002), Codex (#12491), Copilot CLI (#2282, #4163), Gemini CLI (#22093) | Zombie reaping, silent failures, permission bypass issues |
| **Platform stability (Windows/WSL)** | Codex (#20214, #34025), Copilot CLI (#4217, #4222), Kimi Code (#2532), Claude Code (regression) | Windows crashes, WSL path translation, tmux compatibility |
| **Cross-model / provider flexibility** | Gemini CLI (#28485), Pi (#6476, #6922), Kimi Code (#2534), DeepSeek TUI (#4686) | Custom provider support, model auto-discovery, fallback handling |
| **Structured task tracking reliability** | Claude Code (#80210, #80213), Qwen Code (#7306), Gemini CLI (#22323) | TaskCreate/TodoWrite regression, subagent progress visibility |
| **Documentation completeness** | Claude Code (12 doc issues), Gemini CLI (#28447), OpenCode (global community) | Missing docs for plugins, subagents, fast-mode, MCP configuration |

**Industry signal:** The convergence on subagent lifecycle, context management, and provider flexibility suggests the ecosystem is moving from "can it code?" to "can it operate reliably at scale?"

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|-------------|-----------|----------|-----|-----------|--------------|
| **Primary Users** | Pro devs, power users | Enterprise dev teams | Google ecosystem devs | GitHub ecosystem devs | Cost-sensitive devs | Open-source community | Self-hosted/local model users | Asian enterprise teams | CLI purists, FOSS community |
| **Model Strategy** | Anthropic-only (Claude) | OpenAI-only (GPT-4) | Google Gemini | Multi-model (BYOK) | Moonshot Kimi | Multi-provider | Multi-provider + self-hosted | Qwen + multi | DeepSeek + custom |
| **Permission Model** | Granular (bypass bugs) | Sandbox-based | Workspace trust zones | Sandbox + BYOK | API-key gated | Token-based subscriptions | Full-access (extensible) | Session-state based | danger-full-access |
| **Unique Strength** | Background subagents, stacked commands | Multi-agent orchestration, Rust performance | A2A protocol, security hardening | GitHub integration, enterprise MCP | Cost efficiency, MCP-first | V2 branch architecture | Constrained sampling, extension API | Channel delivery, Goal v3 protocol | Skill packs, theme system |
| **Platform Pain** | macOS regression | Windows stability | Wayland/WSL gaps | Windows crashes, tmux | Windows encoding | Subscription meltdown | Self-hosted breakage | CI instability | Windows PATH bug |
| **Release Cadence** | ~weekly stable | Daily alphas | Weekly stable + preview | Patch-driven | Slow (weeks) | Moderate | Fast (multiple/week) | Frequent nightly | Major version trains |

**Strategic insight:** Claude Code and OpenAI Codex are in a feature race for desktop power users. Gemini CLI and Copilot CLI are targeting enterprise reliability. Kimi Code and Qwen Code serve regional Asian markets. Pi and DeepSeek TUI cater to self-hosters and CLI-first developers respectively.

---

## 5. Community Momentum & Maturity

| Tool | Momentum Signal | Maturity Level | Community Health |
|------|----------------|----------------|------------------|
| **Claude Code** | 🟢 Very High | Mature (v2.1.x) | Strong; 50+ open issues reflect active user base; documentation efforts show community self-organization |
| **OpenAI Codex** | 🟢 High | Alpha (Rust rewrite) | Active power users; 151 👍 feature requests show strong engagement; Windows bugs causing frustration |
| **Gemini CLI** | 🟡 Moderate | Mature (v0.52.x) | Stable but slower growth; security patches well-received; subagent bugs persist |
| **Copilot CLI** | 🔴 Low | Mature (v1.0.x) | Community engagement declining; only 1 open PR; 3 new crash bugs indicate stagnation |
| **Kimi Code CLI** | 🟡 Moderate | Early (v2.6) | Small but focused; third-party API breakage showing integration complexity |
| **OpenCode** | 🔴 Stressed | Beta (V2 migration) | High frustration level; subscription meltdown eroding trust; many duplicate issues |
| **Pi** | 🟢 Very High | Mature (v0.80.x) | Highest issue/PR volume; 29 PRs in one day shows active development; self-hosted community growing |
| **Qwen Code** | 🟡 Moderate | Early (v0.20.x) | CI failures blocking progress; regional focus limits global engagement |
| **DeepSeek TUI** | 🟢 High | Pre-release (v0.9.x) | Close to major release; skill pack development shows ecosystem thinking; security gate demonstrates maturity |

**Iteration velocity ranking (today):**
1. OpenAI Codex (4 releases) + Pi (29 PRs updated)
2. DeepSeek TUI (8 PRs merged in one day)
3. Claude Code (1 release, 10 PRs)
4. Gemini CLI (2 releases, 10 PRs)
5. Qwen Code (10 PRs, but CI broken)
6. Copilot CLI (3 patches, 1 PR)
7. OpenCode (10 PRs, but critical bugs)
8. Kimi Code (3 PRs, no release)

---

## 6. Trend Signals

### For Tool Developers

1. **Windows is the new frontier—and the biggest liability.** Every major tool except Gemini CLI has critical Windows bugs. Platforms that invest in Windows stability will win enterprise adoption. Copilot CLI's 3 Windows crash bugs in one day is a warning sign.

2. **MCP protocol reliability is the #1 infrastructure challenge.** Silent failures (#79992, #80002), zombie subprocesses (#12491), and schema mismatches (#2531) plague the ecosystem. The community demands observability: tool execution timestamps, failure traces, and confirmation of dispatch.

3. **Context management is becoming a competitive differentiator.** With compaction bugs (#80196), 5 MB serialization limits (#4183), and "Context Diet" epics (#4704), the tools that solve context optimization will win heavy users. Auto-compaction that actually works, budget visibility, and token-efficient prompt strategies are in high demand.

4. **Subagent orchestration patterns are converging.** Claude Code's background subagents, OpenAI Codex's multi-agent mode, and Gemini CLI's subagent lifecycle all face similar reliability issues: false success reporting, hangs, and permission bypass. The community is converging on "subagent observability" as the next required feature.

5. **Permission/approval UX is a trust bottleneck.** Nine months of unresolved `bypassPermissions` bugs (#39523), silent domain denials (#50842), and false-positive safety checks (#28015) show that current permission models harm more than help. The winning tools will offer auditable, configurably permissive models.

### For Developers Choosing a Tool

- **Choose Claude Code** for the richest feature surface and fastest iteration, but accept macOS risk and permission instability.
- **Choose Gemini CLI** for enterprise security posture (A2A protocol, workspace trust isolation) and Google ecosystem integration.
- **Choose Copilot CLI** if deeply embedded in GitHub workflows, but verify Windows stability before production use.
- **Choose Pi** for self-hosted/local model workloads and extension API flexibility; expect to troubleshoot provider config.
- **Choose Kimi Code or Qwen Code** if serving Asian enterprise markets or optimizing for cost with regional providers.
- **Choose OpenAI Codex** if you need cutting-edge multi-agent capabilities and can tolerate alpha-stage Rust instability.
- **Choose DeepSeek TUI** for a fresh, skill-pack-oriented experience with strong community design, but wait for v0.9.1 stable.

### For Platform Engineers

- **Invest in MCP monitoring and recovery.** Silent failures are the top community pain point. Build timeouts, retry logic, and dispatch confirmation into your tooling layer.
- **Expect account-gated feature regressions.** Task tools disappearing overnight (#80210), subscription meltdowns (#38218), and feature flag reversions are increasing. Build robust feature detection and fallback behavior.
- **Prioritize Windows and WSL testing.** The ecosystem is disproportionately tested on macOS/Linux. Windows users are vocal and numerous—neglect them at your platform's peril.

---

*Report generated 2026-07-23 from community digest data. All issue/PR numbers reference the respective GitHub repositories.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-07-23 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

### #1 — Skill-Creator Bug Fixes (PR #1298)
**Functionality:** Fixes `run_eval.py` consistently reporting 0% recall across all skill descriptions (#556, 10+ independent reproductions). Addresses Windows stream reading, trigger detection, and parallel worker issues that rendered the description-optimization loop useless.
**Discussion:** Central pain point for skill authors — the evaluation pipeline was optimizing against noise, making skill description improvements impossible to validate. Multiple contributors reproduced the same symptom before root-cause was identified.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/1298)

### #2 — Self-Audit Skill v1.3.0 (PR #1367)
**Functionality:** A universal output quality gate combining mechanical file verification with a four-dimension reasoning audit in damage-severity priority order. Works across any project, tech stack, or model.
**Discussion:** Active discussion on integrating with the proposed Reasoning Quality Gate Pipeline (Issue #1385). Proposes pre-task calibration → adversarial review → delivery verification lifecycle.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/1367)

### #3 — Document Typography Skill (PR #514)
**Functionality:** Prevents orphan word wrap (1-6 words spilling onto next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment in AI-generated documents.
**Discussion:** Addresses a universal pain point — every document Claude generates suffers from these issues. Users rarely request typographic fixes explicitly, making this a proactive quality skill.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/514)

### #4 — ODT Skill — OpenDocument Text Creation (PR #486)
**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Supports template filling and ODT-to-HTML conversion.
**Discussion:** Responding to demand for LibreOffice/OpenOffice compatibility in enterprise workflows. Triggers on "ODT", "ODS", "ODF", "OpenDocument", or "LibreOffice document" mentions.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/486)

### #5 — Pyxel Skill for Retro Game Development (PR #525)
**Functionality:** Integrates with pyxel-mcp (MCP server for Pyxel retro game engine). Covers iterative workflow: write → run_and_capture → inspect → iterate.
**Discussion:** Signals community interest in game development workflows and MCP server integration patterns. Updated most recently (2026-07-15) suggesting ongoing refinement.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/525)

### #6 — Testing Patterns Skill (PR #723)
**Functionality:** Comprehensive testing coverage across the full stack: Testing Trophy model, AAA pattern, unit testing, React Testing Library, integration/E2E testing, and what NOT to test.
**Discussion:** Strong interest in structured testing guidance. Covers the gap between "write tests" and "write good tests" that generic instructions miss.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/723)

### #7 — Skill Quality & Security Analyzer (PR #83)
**Functionality:** Two meta-skills: quality analysis across five dimensions (structure, documentation, correctness, efficiency, security) and security analysis for community-contributed skills.
**Discussion:** Early entry (Nov 2025) with sustained interest. Addresses the trust boundary concern raised in Issue #492 — community skills under `anthropic/` namespace require verification.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/83)

### #8 — Color Expert Skill (PR #1302)
**Functionality:** Self-contained color expertise for any task involving color knowledge. Covers naming systems (ISCC-NBS, Munsell, XKCD, RAL), color spaces with "what to use when" guidance, and accessibility.
**Discussion:** Niche but well-received — fills a gap in design-domain expertise that generic instructions cannot provide.
**Status:** Open | [View PR](https://github.com/anthropics/skills/pull/1302)

---

## 2. Community Demand Trends

### 🚨 Security & Trust Boundary (Issue #492 — 43 comments)
**Trend:** Strongest demand signal. Community skills distributed under `anthropic/` namespace impersonate official skills, creating trust boundary vulnerabilities. Users may grant elevated permissions believing skills are sanctioned. **2 upvotes** reflect widespread concern.

### 🔧 Skill-Creator Tooling Reliability (Issues #556, #1169, #1061 — 18 combined comments)
**Trend:** The `run_eval.py` pipeline is the most consistently broken component. Three independent issues report 0% trigger rates, Windows compatibility failures (PATHEXT, cp1252 encoding, select-on-pipe), and silent crashes. This is the **critical path blocker** for skill development.

### 🏢 Enterprise Skill Sharing (Issue #228 — 14 comments, 7 upvotes)
**Trend:** Strong demand for org-wide skill libraries and direct sharing links (vs. manual `.skill` file distribution via Slack/Teams). **7 upvotes** — highest engagement signal in the issue tracker.

### 🧠 Agent Governance & Safety (Issue #412 — 6 comments)
**Trend:** Proposal for policy enforcement, threat detection, trust scoring, and audit trails for AI agent systems. No equivalent skill exists in the collection. Aligns with broader agent safety ecosystem demand.

### 📦 Duplicate Skill Management (Issue #189 — 6 comments, 9 upvotes)
**Trend:** `document-skills` and `example-skills` plugins install identical content, causing context window waste. **9 upvotes** — highest raw support. Demonstrates concern for skill deduplication and plugin architecture clarity.

---

## 3. High-Potential Pending Skills

| Skill | PR | Activity | Status |
|-------|----|----------|--------|
| **Self-Audit (Reasoning Quality Gate)** | [#1367](https://github.com/anthropics/skills/pull/1367) | Updated Jul 2; 40+ line description with companion issue [#1385](https://github.com/anthropics/skills/issues/1385) | Open, active |
| **Document Typography** | [#514](https://github.com/anthropics/skills/pull/514) | Updated Mar 13; addresses universal document quality issue | Open |
| **ODT/OpenDocument** | [#486](https://github.com/anthropics/skills/pull/486) | Updated Apr 14; enterprise format demand | Open |
| **Pyxel (Retro Games)** | [#525](https://github.com/anthropics/skills/pull/525) | Updated Jul 15; most recent update among top skills | Open |
| **Testing Patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Updated Apr 21; full-stack coverage | Open |
| **Color Expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Updated Jul 21; second-most recent | Open |

**All top skills remain open** — none have merged as of reporting date. The skill-creator pipeline bug (#1298) is likely to merge earliest given its blocker status.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable, trustable skill development infrastructure** — fixing the evaluation pipeline (0% recall bug), establishing security review for community submissions, and enabling enterprise-grade sharing — rather than for any single domain-specific skill, reflecting a community that has outgrown experimental contribution and now requires production-quality tooling and governance.

---

# Claude Code Community Digest — 2026-07-23

## Today's Highlights

Claude Code v2.1.218 drops with a long-awaited architectural change: `/code-review` now runs as a background subagent, keeping your conversation clean and allowing stacked slash commands to target it. Meanwhile, a **major macOS regression** is under investigation — filesystem-class MCP tool calls are being silently dropped between approval and server dispatch, affecting all users starting 2026-07-21. A massive documentation cleanup landed in the issue tracker today, with the community filing 12 detailed gaps across skill plugins, subagents, fast-mode, and ultrareview docs.

---

## Releases

**v2.1.218** [Release Link](https://github.com/anthropics/claude-code/releases/tag/v2.1.218)
- `/code-review` now runs as a background subagent — reviews no longer fill your conversation history
- Stacked slash commands can now target the background review subagent
- Added screen-reader announcements for word/line deletions (`Option+Delete`, `Ctrl+W`, `Cmd+Backspace`)

---

## Hot Issues

1. **[#80002 — macOS: Claude Desktop never dispatches tools/call to first-party Filesystem extension](https://github.com/anthropics/claude-code/issues/80002)** — 56 comments, 25 👍
   The top-voted open bug. `tools/list` succeeds but `tools/call` never fires for the built-in Filesystem MCP server. Community speculation points to a broken approval gate dispatch path in the latest desktop app builds.

2. **[#39523 — Bypass permissions mode fundamentally broken — 9-month trail, 12+ duplicates, no resolution](https://github.com/anthropics/claude-code/issues/39523)** — 33 comments, 18 👍
   A meta-issue tracking a **9-month-old** regression where `bypassPermissions` doesn't actually bypass permissions. The community is frustrated by repeated "we fixed it" claims that don't hold. Still open since July 2025.

3. **[#79992 — Filesystem-class MCP tool calls silently dropped between approval gate and local server dispatch](https://github.com/anthropics/claude-code/issues/79992)** — 16 comments, 4 👍
   Appears related to #80002 but more specific: tool calls survive the renderer approval gate then vanish. Survives app rollback, extension reinstall, and new connector identity. Started overnight 2026-07-21 without any local change — strongly suggests a server-side deployment issue.

4. **[#62272 — Chat JSONLs deleted despite high cleanupPeriodDays](https://github.com/anthropics/claude-code/issues/62272)** — 19 comments, 3 👍
   User-provided recovery script for macOS Time Machine. The deletion appears triggered by app updates/restarts, ignoring user-configured retention settings. Community is calling for opt-in destructive operations and journaled deletion logs.

5. **[#61682 — GitHub connector shows "Connected" but exposes no tools in Cowork (Windows 11)](https://github.com/anthropics/claude-code/issues/61682)** — 17 comments, 19 👍
   Windows-exclusive: the GitHub MCP connector authenticates successfully but presents zero tools to the Cowork workspace. No workaround known.

6. **[#50842 — Claude in Chrome silently denies non-pre-approved domains — no approval path exists](https://github.com/anthropics/claude-code/issues/50842)** — 13 comments, 6 👍
   Browser extension's `navigate` tool fails silently for any domain not pre-approved. There is no user-facing approval UI anywhere in the flow, making the tool effectively single-use for most users.

7. **[#71726 — Desktop app needs mid-task message injection (CLI steering parity)](https://github.com/anthropics/claude-code/issues/71726)** — 9 comments, 16 👍
   Feature parity request: CLI users can type a message during a task and have it injected between tool calls. Desktop app queues these messages until the turn finishes. High community demand for this UX improvement.

8. **[#50894 — Focus mode hides substantive assistant messages, not just tool output](https://github.com/anthropics/claude-code/issues/50894)** — 5 comments, 4 👍
   Recently closed, but the core complaint remains: focus mode can't distinguish "status update between tool calls" from "direct answer," so users miss substantive responses.

9. **[#80213 / #80210 — Task tools (TaskCreate/TaskList/TaskGet/TaskUpdate) regressed ~2026-07-21](https://github.com/anthropics/claude-code/issues/80213)** — 2+2 comments, 4 👍 total
   Two reports that task-tracking tools stopped being exposed after 2026-07-21. One user confirms the same account/version exposes them in Desktop but not CLI — suggests an account-gated feature flag that regressed.

10. **[#80348 — Fable 5: confidently claimed "verified" against user's correct "no change" report](https://github.com/anthropics/claude-code/issues/80348)** — 3 comments, 0 👍
    Behavioral issue with Fable 5 model: it presented self-scoped verification (it checked its own code change) as verification of the user's request. Community highlighting the need for hallucination-resistant verification workflows.

---

## Key PR Progress

1. **[#18217 — feat(plugins): add /planwith command for inline plan mode prompts](https://github.com/anthropics/claude-code/pull/18217)** — *CLOSED*
   Adds `/planwith <prompt>` to skip the two-step `/plan` + type flow. Closed — likely merged or superseded. A long-standing (January 2026) quality-of-life improvement.

2. **[#80353 — docs(gcp): stop on checksum mismatch](https://github.com/anthropics/claude-code/pull/80353)** — *OPEN*
   Hardens GCP gateway deployment: fails early with cleanup when the downloaded binary fails checksum verification. Important for CI/CD reliability.

3. **[#80326 — Add account profiles plugin](https://github.com/anthropics/claude-code/pull/80326)** — *OPEN*
   Experimental plugin managing isolated `CLAUDE_CONFIG_DIR` environments for personal/work/client accounts on one machine. Commands for create, list, launch, assign, remove — addresses a common pain point.

4. **[#80294 / #80229 — fix broken docs link(s) via archive.org](https://github.com/anthropics/claude-code/pull/80294)** — *OPEN* (2 PRs)
   LinkMedic-powered fixes for broken npmjs.com outbound links in README docs. Low-risk maintenance.

5. **[#80241 — Fix: Console scrolling to top when Claude adds text](https://github.com/anthropics/claude-code/pull/80241)** — *OPEN*
   EMP_Agent-automated PR fixing scroll-jump behavior in the TUI. Functional fix for a UX annoyance where new output resets scroll position.

6. **[#80196 — Fix: Auto-compact never triggers despite "100% context used"](https://github.com/anthropics/claude-code/pull/80196)** — *OPEN*
   Addresses a critical bug where auto-compaction never fires even when the statusline reports full context (v2.1.153, Max subscription, 200K mode). High impact for heavy users.

7. **[#80195 — Fix: Instantly hitting usage limits with Max subscription](https://github.com/anthropics/claude-code/pull/80195)** — *OPEN*
   Another EMP_Agent-automated PR. If accurate, this fixes Max-tier users being rate-limited immediately on session start — a severe billing/UX bug.

8. **[#80112 — Make devcontainer firewall init resilient to DNS resolution failures](https://github.com/anthropics/claude-code/pull/80112)** — *OPEN*
   Hardens `.devcontainer/init-firewall.sh` so a single DNS failure doesn't abort the entire firewall setup. Practical for CI environments with transient DNS issues.

9. **[#80008 — Add twilight plugin: spec-first design/implement with durable focus stack](https://github.com/anthropics/claude-code/pull/80008)** — *OPEN*
   Submitter acknowledges this needs significant modification but presents it as a demo for spec-first workflows with a "focus stack" — design, implement, verify cycle that survives context resets.

10. **[#18217 (again) — Several EMP_Agent automated fixes](https://github.com/anthropics/claude-code/pulls?q=is%3Apr+author%3Aemirhanempi5285-glitch)**
    A recurring pattern: automated PRs with "Static Security Check: PASSED" and "Local Execution Verified" stamps. The community should review these carefully — they may be useful automation, but the generic signing is a red flag for auditability.

---

## Feature Request Trends

1. **Mid-task steering parity (CLI→Desktop)**: Multiple issues (#71726, #80395) demand that Desktop users get CLI's ability to inject messages mid-task. The CLI's "steering" capability is a key differentiator that Desktop users now want.

2. **Fable "plan" mode**: Users want a `fableplan` equivalent to `opusplan` (#80359) — a token-efficient planning mode using Fable 5 for lower costs on complex tasks.

3. **Desktop ↔ CLI feature convergence**: Recurring requests for the Desktop app to match CLI capabilities: keyboard shortcuts (#68859), task injection, remote control reliability (#80400, #78933).

4. **Documentation completeness cascade**: A single user (coygeek) filed 12 documentation issues in one day covering skill plugins, subagents, fast-mode, MCP configuration, agent view, code review, and ultrareview. The community is systematically documenting undocumented behavior.

5. **Structured task tool reliability**: After the ~2026-07-21 regression of `TaskCreate`/`TodoWrite` tools (#80210, #80213), users want clearer visibility into feature-gate status and better error messaging when tools are account-restricted.

---

## Developer Pain Points

1. **Silent MCP tool failures**: The #1 pain point this week. Tool calls that pass approval but never reach the MCP server (#79992, #80002) with zero error surface. Users can't tell if a tool ran or not — a debugging nightmare.

2. **Permissions bypass unreliability**: 9 months of unresolved issues (#39523) with `bypassPermissions`. Developers can't trust the permission system, leading to workarounds that weaken security.

3. **Data loss without warning**: Chat history deletion (#62272) that ignores user-configured retention settings, triggered by app updates. No confirmation dialogs, no deletion logs.

4. **Account-gated feature regressions**: Task tools (#80210, #80213) that work one day and vanish the next without any user action. No visibility into feature flags or account-level provisioning state.

5. **Model behavior unpredictability**: Fable 5's "verified" hallucination (#80348) and silent hangs during browser automation (#80399) erode trust. Developers need reliable verification signals and better timeout/error surfacing.

*Generated 2026-07-23 from `github.com/anthropics/claude-code` — 50 open issues, 10 open PRs, 1 new release.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-23

## Today's Highlights

Four new Rust alpha releases (v0.146.0-alpha.1 through .4) landed today, signaling an active development push on the CLI side. Meanwhile, the community continues to flag deep-seated Windows stability issues, with **issue #20214** (Codex App freezes on Windows 11) and **issue #34025** (300+ `taskkill.exe` spawns on cold launch) underscoring persistent platform pain. A burst of closed PRs from the `copyberry[bot]` suggests internal momentum on process hygiene, plugin caching, and thread lifecycle fixes.

## Releases

The `openai/codex` repository published four Rust tagged releases in the last 24 hours, all under the `rust-v0.146.0-alpha` series. Release notes are minimal — each states only "Release 0.146.0-alpha.N" — so the exact changes are not publicly annotated. Given the rapid iteration (four alphas in one day), these likely include hotfixes or incremental patches. No stable or beta releases were cut.

**Releases (latest to earliest):**
- [rust-v0.146.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.4)
- [rust-v0.146.0-alpha.3](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.3)
- [rust-v0.146.0-alpha.2](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.2)
- [rust-v0.146.0-alpha.1](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.1)

---

## Hot Issues (Top 10 by community impact)

### 1. [#20214 — Codex App frequently freezes/stutters on Windows 11](https://github.com/openai/codex/issues/20214)
- **72 comments, 71 👍**
- **Why it matters:** A top-voted, long-running issue (since April). Users report UI freezes despite 32 GB RAM and modern CPUs. The 72-comment thread indicates ongoing frustration with Windows performance — a flagship stability concern that has not been resolved in three months.

### 2. [#28969 — Add setting to disable auto-resolve in 60 seconds for questions](https://github.com/openai/codex/issues/28969)
- **53 comments, 151 👍**
- **Why it matters:** Highest 👍 count today. Users strongly dislike the forced 60-second auto-resolve timer for CLI questions, which can interrupt workflows. The feature request for a configurable timeout has broad cross-platform appeal.

### 3. [#12491 — MCP child processes not reaped — 1300+ zombies, 37GB memory leak](https://github.com/openai/codex/issues/12491)
- **27 comments, 5 👍**
- **Why it matters:** Extreme resource exhaustion scenario in the GUI app (Codex.app). MCP subprocesses accumulate as zombies, leading to gigabytes of leaked memory. A systemic process-management bug affecting Pro-tier users on macOS.

### 4. [#21639 — Hooks no longer run after Codex Desktop update](https://github.com/openai/codex/issues/21639)
- **23 comments, 6 👍**
- **Why it matters:** A regression affecting hook execution — a core integration mechanism. Users were forced to downgrade or manually patch. Still open after two months, suggesting a tricky dependency chain bug.

### 5. [#16815 — WSL agent mode fails on Windows: "AbsolutePathBuf deserialized without a base path"](https://github.com/openai/codex/issues/16815)
- **22 comments, 13 👍**
- **Why it matters:** Blocks WSL-based development on Windows entirely. The error (`AbsolutePathBuf`) points to path-handling logic that cannot handle Windows-to-WSL path translation. A critical workflow blocker for hybrid Windows/Linux users.

### 6. [#28015 — False positive cybersecurity safety check blocks normal repo maintenance](https://github.com/openai/codex/issues/28015)
- **22 comments, 3 👍**
- **Why it matters:** Safety-check overreach interrupts legitimate `git` operations (status, fetch, prune). Users report paid sessions being interrupted for "cybersecurity risk" during routine maintenance. Raises trust and productivity concerns.

### 7. [#27458 — Codex appears to timeout while waiting for user input](https://github.com/openai/codex/issues/27458)
- **12 comments, 43 👍**
- **Why it matters:** High 👍 count for a timeout bug. The agent seems to hang indefinitely when waiting for user input, especially in WSL environments. Disrupts interactive coding sessions.

### 8. [#23200 — Support headless remote Linux hosts for Codex mobile](https://github.com/openai/codex/issues/23200)
- **13 comments, 42 👍**
- **Why it matters:** A frequently requested feature: using Codex mobile to control always-on Linux servers without keeping the desktop app online. The 42 👍 shows strong interest from server-side developers.

### 9. [#34025 — Cold launch spawns 300+ taskkill.exe/conhost.exe and freezes PC](https://github.com/openai/codex/issues/34025)
- **7 comments, 0 👍**
- **Why it matters:** Recent (filed July 18). A new Windows app version causes severe system-wide freeze on cold launch. Although low on votes, the severity (300+ orphan processes) is alarming and may be under-reported.

### 10. [#32791 — Five-hour Codex usage limit disappeared from Plus account](https://github.com/openai/codex/issues/32791)
- **8 comments, 3 👍**
- **Why it matters:** A subtle billing/rate-limit UI bug: Plus users see only a weekly cap, losing the 5-hour daily usage display. Could cause unexpected throttling for users who rely on the visible daily limit.

---

## Key PR Progress (Top 10)

### 1. [#34852 — Wake sleeping threads for queued agent mail](https://github.com/openai/codex/pull/34852)
- **CLOSED.** Treats pending mailbox messages as wake-up work during durable sleep. Fixes an inter-agent communication deadlock.

### 2. [#34850 — Disable image generation for Free-plan accounts](https://github.com/openai/codex/pull/34850)
- **CLOSED.** Skips registering the standalone `image_generation` tool for free-tier accounts. Prevents confusing API errors for unentitled users.

### 3. [#34847 — Use Guardian model limits for review sessions](https://github.com/openai/codex/pull/34847)
- **CLOSED.** Ensures the review (Guardian) session uses the correct context-window limit, rather than inheriting parent settings. Fixes context overflow in review mode.

### 4. [#34846 — Allow custom providers to opt into standalone web search](https://github.com/openai/codex/pull/34846)
- **CLOSED.** Adds a `supports_standalone_web_search` flag for custom model providers, enabling the `web.run` tool for third-party backends.

### 5. [#34845 — Track multi-agent mode in world state](https://github.com/openai/codex/pull/34845)
- **CLOSED.** Persists multi-agent mode instructions in world state, preventing repeated re-emission of setup hints on history changes.

### 6. [#34840 — Add persisted thread pinning to the app server](https://github.com/openai/codex/pull/34840)
- **CLOSED.** Adds server-side thread pinning with `isPinned` fields, filter, and pagination. Enables a long-requested UX feature without local-only workarounds.

### 7. [#34839 — Preserve user input when MCP startup is interrupted](https://github.com/openai/codex/pull/34839)
- **CLOSED.** Fixes a data-loss bug: if MCP tool startup is interrupted, the submitted user input is now retained in conversation history.

### 8. [#34835 — Track compaction time in turn profiles](https://github.com/openai/codex/pull/34835)
- **CLOSED.** Adds `compaction_ms` metric to turn profiles, separating compaction from idle time. Improves observability for performance debugging.

### 9. [#34831 — Flush analytics before in-process app server shutdown](https://github.com/openai/codex/pull/34831)
- **CLOSED.** Prevents analytics data loss when the in-process app server shuts down while events are still queued. Fixes missing turn-completion and acceptance-line telemetry.

### 10. [#34819 — Enable git attribution across Codex entry points](https://github.com/openai/codex/pull/34819)
- **CLOSED.** Installs git attribution logic in app server, MCP server, and debug prompt. Ensures commit/PR attribution instructions respect workspace policy across all entry points.

---

## Feature Request Trends

- **Configurable auto-resolve timeout** — Issue #28969 (151 👍) is the top-voted feature request. Users want to disable or extend the 60-second auto-answer timer in CLI.
- **Headless remote Linux support for mobile** — Issue #23200 (42 👍). Developers want to control remote Linux hosts via Codex mobile without tethering a desktop app.
- **Persistent side chats as child threads** — Issue #26227 (17 👍). Users want ephemeral side-chat context to survive app restarts and updates.
- **Custom worktree location** — Issue #10599 (66 👍). Users want to choose where Git worktrees are created, rather than a hardcoded path.
- **Thread pinning** — Addressed in PR #34840 (closed today). Server-side pinning directly responds to community requests for organizing long-running threads.

---

## Developer Pain Points

1. **Windows process/metadata leaks** — Multiple open issues (##12491, #26984, #34025, #34841) describe runaway zombie processes, FD exhaustion (`EMFILE`), ACL-state corruption, and sandbox bootstrap failures. Windows remains the platform with the most severe resource-leak bugs.

2. **WSL path- and sandbox-incompatibility** — Issues #16815, #20730, #22428, #34782, #33774 all report path-resolution failures, sandbox setup errors, and thread assignment chaos specifically in WSL environments. The WSL integration appears fragile after recent updates.

3. **Safety-check overreach** — Issues #28015 and #30744 document false-positive cybersecurity blocks on ordinary git/DevOps operations and Slack integrations. This erodes trust in the safety layer.

4. **Post-update regressions** — Three separate issues (##21639, #30385, #33774) describe existing features breaking after desktop updates — hooks stop running, sidebar threads disappear, projects are reassigned to legacy IDs. Update hygiene is a recurring pain.

5. **MCP subprocess lifecycle** — Issues #12491, #26984, #17574, and PR #34839 collectively show that MCP child processes (stdio servers, browser tools, xcodebuild) are not reliably reaped or interrupted, leading to leaks, crashes, and data loss. This is a top priority area for the core team.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-23

## Today's Highlights

Two releases shipped today: a stable **v0.52.0** and a preview **v0.53.0-preview.0** that includes a critical A2A protocol fix for 400 Bad Request errors. A significant security patching landed in the nightly build addressing a potential RCE in the A2A server. Meanwhile, the highest-activity issue tracker item is a long-running bug (#22323) where subagent failure from MAX_TURNS is incorrectly reported as success, which continues to generate community discussion.

## Releases

- **[v0.53.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.53.0-preview.0)** — Fixes a core/A2A bug where cancelled tool responses with consecutive roles triggered `400 Bad Request` errors. Also introduces an LLM triage orchestrator for caretaker automation.
- **[v0.52.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0)** — Stable release that refactors transient CI configuration files out of workspace context and adds foundational triage worker modules.
- **[v0.52.0-nightly.20260722](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260722.gc776c665b)** — Critical security fix: enforces workspace trust and task isolation in the A2A server to prevent remote code execution (RCE).

## Hot Issues

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent recovery after MAX_TURNS reported as GOAL success** (P1, 12 comments)  
   The `codebase_investigator` subagent reports `status: "success"` even when hitting the max turn limit before doing any analysis. This masking of interruptions is a high-priority reliability bug causing misleading user-visible outcomes. Strong community engagement with 2 👍.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs forever** (P1, 8 comments, 8 👍)  
   Simple tasks like folder creation hang indefinitely when delegated to the generalist agent. Users report that explicitly instructing the model not to use sub-agents works around the issue. High community frustration — this is the most upvoted open issue.

3. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command execution stuck in "Waiting input" after completion** (P1, 4 comments, 3 👍)  
   After executing simple CLI commands that do not require user input, the CLI hangs showing an active shell awaiting input. Reproducible with trivial commands. A frequent workflow blocker.

4. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland** (P1, 4 comments, 1 👍)  
   The browser subagent terminates with `GOAL` status on Wayland displays but provides no actionable feedback. Wayland compatibility gaps are affecting Linux desktop users.

5. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retries low-signal sessions indefinitely** (P2, 5 comments)  
   If the extraction agent decides a session is "low-signal" and skips reading it, that session remains unprocessed and is resurfaced repeatedly. The system should mark low-signal sessions as processed after a threshold.

6. **[#28479](https://github.com/google-gemini/gemini-cli/issues/28479) — GeminiCLI.com feedback: JetBrains Rider authentication error** (P2, 5 comments)  
   Users on JetBrains Rider via the ACP Gemini CLI plugin get `{"error":{"...}}` responses when using an API key. New issue but already attracting attention.

7. **[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) — Symlinked agent files not recognized** (P2, 4 comments)  
   `~/.gemini/agents/filename.md` is ignored when it's a symlink. Users who manage agent definitions via symlinks into repositories lose functionality.

8. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 400 error with > 128 tools** (P2, 3 comments)  
   The CLI hits API limits when too many tools are available. Request for smarter scoping of enabled tools rather than a hard limit.

9. **[#22093](https://github.com/google-gemini/gemini-cli/issues/22093) — Subagents running without permission since v0.33.0** (P2, 3 comments)  
   Users who explicitly disabled agents in configuration report subagents being invoked anyway. MCP-only users are affected. Regression is ongoing.

10. **[#22186](https://github.com/google-gemini/gemini-cli/issues/22186) — get-shit-done output hook causes crash** (P1, 3 comments)  
    The output hook crashes when nearing completion during user summary printing. Blocks the "get-shit-done" workflow entirely.

## Key PR Progress

1. **[#28407](https://github.com/google-gemini/gemini-cli/pull/28407) — Fix(core,a2a): group cancelled tool responses and coalesce consecutive roles** (merged in v0.53.0-preview.0)  
   Resolves `400 Bad Request` errors by properly handling cancelled tool responses in the A2A protocol.

2. **[#28470](https://github.com/google-gemini/gemini-cli/pull/28470) — Fix(a2a-server): enforce workspace trust and task isolation** (nightly)  
   Security fix preventing RCE by enforcing workspace trust boundaries and task isolation in the A2A server.

3. **[#28469](https://github.com/google-gemini/gemini-cli/pull/28469) — Fix(core): rotate session ID on model fallback**  
   Prevents `[API Error: Please submit a new query]` when falling back to `gemini-2.5-flash` by rotating the session ID.

4. **[#28485](https://github.com/google-gemini/gemini-cli/pull/28485) — Fix(cli): add gemini-3.5-flash to model selector**  
   Fixes a regression where `gemini-3.5-flash` was missing from the model selector for some users due to a legacy code path.

5. **[#28509](https://github.com/google-gemini/gemini-cli/pull/28509) — Fix(core): filter thought parts from getHistoryTurns**  
   Prevents internal monologue/thinking parts from leaking into history when context management is disabled, which was causing duplicate reasoning blocks.

6. **[#28446](https://github.com/google-gemini/gemini-cli/pull/28446) — Fix(auth): use native fetch for OAuth token exchange** (P1)  
   Fixes `Premature close` errors on headless VPS by switching from Node's `http` to native `fetch` for OAuth token exchange.

7. **[#28447](https://github.com/google-gemini/gemini-cli/pull/28447) — Docs: add Windows PowerShell troubleshooting**  
   Documentation improvement for Windows users encountering `gemini` command failures after global npm install in PowerShell.

8. **[#28431](https://github.com/google-gemini/gemini-cli/pull/28431) — Feat(pr-generator-infra): Cloud Run job and Workflows definition**  
   Foundational infrastructure for an SSR Code Generation Pipeline, including container configs and Eventarc-triggered Workflows.

9. **[#28499](https://github.com/google-gemini/gemini-cli/pull/28499) — Fix(policy): restrict tools.core wildcard DENY to built-in tools**  
   Fixes a bug where wildcard DENY rules were silently excluding all MCP tools. The `excludeMcp` property scopes wildcards to core tools only.

10. **[#28506](https://github.com/google-gemini/gemini-cli/pull/28506) — Fix(cli): propagate AbortSignal in /compress command**  
    The `/compress` command now passes an `AbortSignal`, allowing cancellation of background compression when users start a new prompt or press Escape.

## Feature Request Trends

The most-requested capabilities from open issues cluster around four themes:

1. **Agent self-awareness and observability** — Users want agents to understand their own CLI flags, hotkeys, and execution limits. Multiple issues request that subagent trajectories be visible via `/chat share` (#22598) and that bug reports include subagent context (#21763).

2. **Smarter tool selection and scoping** — The 128-tool limit (#24246) and AST-aware file operations (#22745, #22746) both point to demand for precision: the agent should automatically limit available tools and use AST information to reduce token waste and turns.

3. **Memory system robustness** — Auto Memory improvements (#26522, #26523, #26516) are a concentrated area: users want deterministic redaction of secrets, proper session quarantine, and termination of retry loops for low-signal content.

4. **Resilience under failure** — Browser agent session takeover and lock recovery (#22232), automatic model fallback retry, and graceful handling of interactive prompts (#22465) indicate a strong desire for agents to recover from failures without user intervention.

## Developer Pain Points

- **Subagent reliability is the #1 frustration.** Issues #22323 (false success reporting), #21409 (hangs), and #22093 (running without permission) represent three different failure modes all related to subagent behavior. The community workaround of "instruct the model not to use sub-agents" is telling.

- **Hidden failures and silent hangs** are pervasive. The CLI gets stuck at interactive prompts (#22465), on already-completed shell commands (#25166), and during output hook execution (#22186). None of these produce useful error messages, forcing users to cancel and retry blindly.

- **Configuration and tool discovery issues** create onboarding friction. Agents ignoring `settings.json` overrides (#22267), symlinked agents not being recognized (#20079), and JetBrains plugin authentication failures (#28479) suggest gaps in both configuration parsing and cross-platform testing.

- **Security and data exposure concerns** are rising. Auto Memory sending content to models before redaction (#26525) and the A2A RCE vulnerability (just patched in nightly) indicate that trust boundaries are still being hardened. Users are increasingly aware of these risks.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-23

## Today's Highlights
Three patch releases (v1.0.74-1 through v1.0.74-3) shipped today, bringing Gemini 3.6 Flash support and fixing a session leakage bug. Meanwhile, the community reported **seven new triage issues** in the last 24 hours, with regressions in Windows crash behavior, tmux compatibility, and React/Ink render loops dominating the discourse. A major BYOK authentication regression (#4016) also received maintainer attention.

## Releases
**Three versions published today** — v1.0.74-1, v1.0.74-2, v1.0.74-3 — all primarily fixes and minor changes.

**v1.0.74-1** notable additions:
- **First-run splash** to opt into the default sandbox
- **Gemini 3.6 Flash support** added
- **Session multiplexing fix**: open dialogs no longer leak between sessions; eligible pickers reopen on switch-back
- **Shell shortcut improvement**: `$` interactive shortcut now properly opens (description truncated in source)

## Hot Issues
| Issue | Title | Why It Matters | Community Reaction |
|-------|-------|----------------|-------------------|
| [#2282](https://github.com/github/copilot-cli/issues/2282) | [CLOSED] Not Able to connect to MCP servers | Windows users hitting MCP handshake failures with `github-mcp-server` — fundamental usability block for MCP adopters | 11 comments, 1 👍; closed |
| [#443](https://github.com/github/copilot-cli/issues/443) | Feature Request: Built-in PDF Reading Support | Long-running request (since Oct 2025) for native PDF parsing — critical for academic/enterprise workflows | 6 comments, **33 👍** — highest demand in list |
| [#4016](https://github.com/github/copilot-cli/issues/4016) | BYOK rejected in `--acp` mode (regression) | Custom provider users cannot use Agent Client Protocol without GitHub login — breaks air-gapped/enterprise setups | 5 comments, 4 👍; regression from fixed #3048 |
| [#4163](https://github.com/github/copilot-cli/issues/4163) | Child process zombie accumulation on Linux | Unreaped zombies (~2/min) degrade system resources over long sessions — reliability concern | 3 comments, 2 👍 |
| [#4183](https://github.com/github/copilot-cli/issues/4183) | Auto-compaction doesn't prevent 5 MB CAPI limit failure | Tool-heavy sessions hit hard serialization limit not mitigated by token-based compaction | 2 comments, **7 👍** — high agreement |
| [#4222](https://github.com/github/copilot-cli/issues/4222) | Regression #2802: Infinite React/Ink render loop on v1.0.72+ | Main pane freezes on Windows VS Code integrated terminal — core UX blocker returned | New triage, 0 comments yet |
| [#4217](https://github.com/github/copilot-cli/issues/4217) | Windows crash on exit (libuv async handle) | Consistent `FAST_FAIL_FATAL_APP_EXIT` during teardown — clean shutdown broken on Windows | 0 comments, 1 👍 |
| [#4219](https://github.com/github/copilot-cli/issues/4219) | Windows crash when `notifications` enabled | Native access violation with OS toast notifications — crash-on-feature-use for Windows users | 0 comments |
| [#4212](https://github.com/github/copilot-cli/issues/4212) | Dark-on-dark rendering inside tmux | Prompt box and menu items invisible — accessibility issue for tmux users | 1 comment |
| [#4223](https://github.com/github/copilot-cli/issues/4223) | Shell command completion never detected in tmux | Commands execute but CLI hangs on "still running" — destroys tmux workflow entirely | New triage |

## Key PR Progress
*Only 1 PR updated in the last 24 hours.* This is unusually low activity, suggesting maintainers are focused on triaging the 34 open issues rather than merging new code.

| PR | Title | Status & Significance |
|----|-------|----------------------|
| [#3163](https://github.com/github/copilot-cli/pull/3163) | ViewSonic monitor | [OPEN] — Spam/irrelevant PR referencing monitors; no code changes. Unlikely to merge. |

**Note**: The PR pipeline is essentially frozen today. The community should watch for tomorrow whether this is a one-day lull or a pattern.

## Feature Request Trends
1. **Custom agent orchestration** (#4208): Users want inline agent invocation and chaining within prompts — "use agent X for this subtask" without losing conversation context.
2. **Configurable model pools** (#4218): Auto mode should let users constrain which models it selects from, to control cost and behavior.
3. **Per-agent credit accounting** (#4207): Break down cumulative AI credit usage by subagent/custom agent for cost tracking.
4. **Skill tool aliases** (#4209): Custom agents need access to the `skill` tool — currently blocked by limited frontmatter aliases.
5. **Built-in PDF reading** (#443): Persistent highly-upvoted request (33 👍) for native document parsing.

## Developer Pain Points
1. **Windows stability crisis**: Three separate crash bugs (#4217, #4219, #4222) reported in a single day — exit crashes, notification crashes, and render-loop freezes. Windows is the most fragile platform in current releases.
2. **tmux incompatibility**: Two distinct bugs (#4212, #4223) make Copilot CLI nearly unusable inside tmux — invisible UI and hung command detection.
3. **BYOK/Air-gapped regression**: The on-again, off-again BYOK authentication bug (#4016) persists through multiple "fixed" releases. Enterprise users cannot trust `--acp` mode with custom providers.
4. **Context-bloat hard limits**: Despite auto-compaction, users hit the 5 MB CAPI serialization limit (#4183) — a ceiling that token-based strategies can't address. High community agreement (7 👍) signals this is widespread.
5. **MCP reliability**: Both the `github-mcp-server` connection failure (#2282) and the stalled MCP handshake (#4206) show the MCP integration layer is fragile, especially under enterprise policies.

---

*Data snapshot: 2026-07-23 23:59 UTC — 34 open issues, 1 open PR, 3 releases today.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date:** 2026-07-23

---

## 1. Today's Highlights

The Kimi Code CLI project saw a quiet day with no new releases, but several critical bug fixes are in motion. A PR to resolve a 400 error caused by Moonshot-specific `prompt_cache_key` parameters being sent to third-party APIs has been opened, directly addressing a regression reported earlier today. Meanwhile, a feature request for per-agent model selection in multi-agent workflows signals growing community interest in cost-optimized architecture.

---

## 2. Releases

No new releases in the last 24 hours. The latest stable version remains **kimi 2.6** (as noted in Issue #2318).

---

## 3. Hot Issues

### #2534 — Model API error 400 Validation: Unsupported parameter(s): `prompt_cache_key`
- **Author:** dewrama | **Created:** 2026-07-23 | **Reactions:** 0
- **Link:** [Issue #2534](https://github.com/MoonshotAI/kimi-cli/issues/2534)
- **Why it matters:** A recent update broke compatibility with third-party APIs (Nvidia nim models) by sending Moonshot-exclusive `prompt_cache_key` parameters. This is a regression from working behavior and affects users on non-Moonshot backends. A fix PR (#2535) was opened the same day.

### #2531 — MCP tool names & schemas rejected by Moonshot API (HTTP 400)
- **Author:** sbdsam | **Created:** 2026-07-22 | **Reactions:** 0
- **Link:** [Issue #2531](https://github.com/MoonshotAI/kimi-cli/issues/2531)
- **Why it matters:** MCP tool schemas using `anyOf` without explicit `type` fields are rejected by the Moonshot API. This requires client-side schema sanitization before sending, representing a compliance gap between the MCP spec and Moonshot's strict schema validation.

### #2532 — `kimi web` crashes on Windows with redirected stdout: UnicodeEncodeError (gbk)
- **Author:** BFour666 | **Created:** 2026-07-22 | **Reactions:** 0
- **Link:** [Issue #2532](https://github.com/MoonshotAI/kimi-cli/issues/2532)
- **Why it matters:** The startup banner uses the `➜` (U+279C) character, which crashes on Chinese-locale Windows when stdout is piped. This is a common pattern for CI/CD and IDE integration—a critical UX blocker for Windows power users.

### #2533 — Feature Request: Per-agent model selection for sub-agents
- **Author:** bob0x-ai | **Created:** 2026-07-23 | **Reactions:** 0
- **Link:** [Issue #2533](https://github.com/MoonshotAI/kimi-cli/issues/2533)
- **Why it matters:** Users want cost-tiered multi-agent workflows, assigning cheap models to simple sub-tasks and capable models to complex ones. This is a natural evolution for Kimi's agent system, enabling cost-efficient orchestration.

### #2318 — Request reached organization TPD rate limit (current: 1,505,241)
- **Author:** globalvideos272-lab | **Created:** 2026-05-18 | **Updated:** 2026-07-22 | **Reactions:** 2👍
- **Link:** [Issue #2318](https://github.com/MoonshotAI/kimi-cli/issues/2318)
- **Why it matters:** Long-running issue about incorrect TPD (tokens per day) rate limit calculation. User reports hitting limits prematurely. The 2 upvotes indicate broader community interest in rate limit transparency and handling.

### #2524 — `StrReplaceFile` replacement count computed against original content
- **Author:** Sreekant13 (PR author) | **Updated:** 2026-07-22
- **Link:** [PR #2524](https://github.com/MoonshotAI/kimi-cli/pull/2524)
- **Why it matters:** A subtle bug where chained string replacements counted edits against the original file, not the running content. This could cause incorrect edit reporting in agent workflows.

### #2530 — Shell blocking until timeout when detached child holds pipes
- **Author:** ayaangazali (PR author) | **Updated:** 2026-07-22
- **Link:** [PR #2530](https://github.com/MoonshotAI/kimi-cli/pull/2530)
- **Why it matters:** Commands like `some_daemon & echo done` cause indefinite blocking because stdout/stderr EOF is never reached. This impacts any workflow using background processes.

---

## 4. Key PR Progress

### #2535 — fix(llm): scope prompt cache keys to Moonshot APIs
- **Author:** Sanjays2402 | **Opened:** 2026-07-23
- **Link:** [PR #2535](https://github.com/MoonshotAI/kimi-cli/pull/2535)
- **What it does:** Resolves #2534 by only sending `prompt_cache_key` to official Kimi/Moonshot APIs. Third-party endpoints are now excluded, restoring compatibility with Nvidia nim and similar providers.

### #2524 — fix(tools): count StrReplaceFile replacements against the running content
- **Author:** Sreekant13 | **Opened:** 2026-07-20 | **Updated:** 2026-07-22
- **Link:** [PR #2524](https://github.com/MoonshotAI/kimi-cli/pull/2524)
- **What it does:** Fixes a bug where sequential `StrReplaceFile` edits reported an incorrect count. Edits that produced a string matched by a later edit were miscounted.

### #2530 — fix(shell): stop blocking until timeout when a detached child holds the pipes
- **Author:** ayaangazali | **Opened:** 2026-07-21 | **Updated:** 2026-07-22
- **Link:** [PR #2530](https://github.com/MoonshotAI/kimi-cli/pull/2530)
- **What it does:** Prevents infinite blocking on shell commands with background processes by checking exit code before waiting for EOF on stdout/stderr pipes.

---

## 5. Feature Request Trends

The community is requesting:
- **Per-agent model selection** (#2533) — Cost-tiered multi-agent workflows where sub-agents can use different models than the session default.
- **Better third-party API compatibility** (implicit in #2534 regression) — Users want reliable support for non-Moonshot backends.
- **Windows encoding fixes** (#2532) — Cross-platform stability, especially for non-ASCII output in piped environments.
- **Rate limit transparency** (#2318) — Better error messages and handling when TPD limits are approached.

---

## 6. Developer Pain Points

1. **Third-party API breakage** — The `prompt_cache_key` regression (#2534) is the most acute pain point, breaking workflows that were working before a recent update.
2. **Schema validation mismatch** (#2531) — Moonshot's API rejects valid MCP tool schemas, requiring client-side workarounds.
3. **Windows encoding issues** (#2532) — A recurring theme: the CLI crashes on Chinese-locale Windows when stdout is piped, a common scenario in CI and IDE integration.
4. **Shell command blocking** (#2530) — Background processes in shell commands cause indefinite hangs, affecting automation scripts.
5. **Rate limit opacity** (#2318) — High TPD usage without clear feedback creates uncertainty for heavy users.

*Digest generated from data available on 2026-07-23.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-23

---

## Today's Highlights

A wave of subscription access issues dominates today's activity, with multiple reports that `opencode-go` subscribers are receiving "Request blocked by upstream provider" errors across all models. Meanwhile, critical infrastructure bugs emerged including the V2 server caching failed boots for the full 60-minute TTL without recovery and a persistent CPU-burning allocation loop in long-lived server processes. On the positive side, several important PRs landed to fix agent color migration, dynamic model loading for `/api/generate`, and TUI theme generation from V2 tokens.

---

## Releases

**No new versions published in the last 24 hours.**

---

## Hot Issues

### 1. [#38218 — All subscription models return "Request blocked by upstream provider"](https://github.com/anomalyco/opencode/issues/38218)
- **Why it matters:** This is the most critical live bug—a regressive issue affecting paid `opencode-go` subscribers. Users report that after logging in, absolutely no models work, rendering the entire subscription useless. The issue has erupted with 22 comments in 24 hours.
- **Community reaction:** High frustration; two duplicate threads (#38368, #38293, #38269) confirm the pattern.

### 2. [#19466 — opencode using 50% CPU while rate-limit waiting](https://github.com/anomalyco/opencode/issues/19466)
- **Why it matters:** Passive rate-limit waiting should be near-zero CPU. An i9-14900 burning half a core while doing "nothing" is a significant performance bug affecting all users with aggressive rate limits.
- **Community reaction:** 15 comments, 11 👍; still unresolved after 4 months.

### 3. [#6231 — Auto-discover models from OpenAI-compatible providers](https://github.com/anomalyco/opencode/issues/6231)
- **Why it matters:** The single most upvoted open feature request (185 👍). Users of LM Studio, Ollama, and llama.cpp must manually list models—a painful workflow. This is the community's top quality-of-life ask.
- **Community reaction:** 28 comments, sustained interest since Dec 2025.

### 4. [#38269 — "思考一直不成功，浪费了许多token" (Thinking always fails, wastes tokens)](https://github.com/anomalyco/opencode/issues/38269)
- **Why it matters:** Represents a class of model/tool interaction bugs where LLM outputs fail schema validation for the bash tool, causing retry loops that burn API credits. Affects users globally (Chinese reporter here).
- **Community reaction:** Screenshot evidence of repeated "SchemaError: Missing key at description" errors.

### 5. [#38399 / #38400 — Duplicate "no such column: data" tool errors](https://github.com/anomalyco/opencode/issues/38399)
- **Why it matters:** Every tool (bash, read, glob, grep, webfetch, websearch) returns SQLite schema errors. This is likely a database migration or cache corruption bug that completely blocks tool usage.
- **Community reaction:** Two identical reports filed minutes apart by the same user, indicating a systematic breakdown.

### 6. [#37970 — Plan/Build mode removed in latest version](https://github.com/anomalyco/opencode/issues/37970)
- **Why it matters:** A planned workflow mode appears to have been removed unintentionally. Users report inconsistent behavior where the tool sometimes plans and sometimes doesn't.
- **Community reaction:** 10 comments; the reporter is clearly familiar with prior behavior and considers this a regression.

### 7. [#36677 — V2 server enters persistent CPU/memory allocation loop while idle](https://github.com/anomalyco/opencode/issues/36677)
- **Why it matters:** A long-lived `opencode2 serve` instance consumes 1.1–1.3 GB RSS and a full CPU core while idle. This is a showstopper for production deployments of V2.
- **Community reaction:** Only 2 comments so far, but the severity rating is high (labeled `bug, perf, core, 2.0`).

### 8. [#38416 — New UI "as ugly as feces" — strong negative feedback on redesign](https://github.com/anomalyco/opencode/issues/38416)
- **Why it matters:** Strong emotional reaction to the new UI, suggesting UX changes may have alienated power users. Even if hyperbolic, the sentiment warrants attention.
- **Community reaction:** 1 comment, but the language is notable; labeled `needs:compliance`.

### 9. [#18011 — LM Studio shows only 3/9 models despite full /v1/models list](https://github.com/anomalyco/opencode/issues/18011)
- **Why it matters:** Directly related to #6231—auto-discovery is broken for LM Studio. Users manually see 9 models but OpenCode only picks up 3.
- **Community reaction:** 6 comments, 4 👍; open since March 2026.

### 10. [#26220 — Infinite loop after tool calls complete (Zen/big-pickle)](https://github.com/anomalyco/opencode/issues/26220)
- **Why it matters:** After tool execution, the process hangs indefinitely and ignores user input. This is a critical UX bug for agentic workflows.
- **Community reaction:** 6 comments, reproducible across versions.

---

## Key PR Progress

### 1. [#38417 — [contributor] fix(ai): preserve OpenAI message phases](https://github.com/anomalyco/opencode/pull/38417)
- **What:** Decodes OpenAI Responses message phases (`commentary` / `final_answer`) and preserves item IDs through canonical text provider metadata. Splits and phase-tags assistant text when lowering follow-up requests.
- **Why important:** Aligns with the official OpenAI SDK contract; fixes potential phase-loss in multi-turn conversations.

### 2. [#38414 — [contributor] fix(core): migrate named agent colors](https://github.com/anomalyco/opencode/pull/38414)
- **What:** Preserves named agent colors in the V1 config schema and migrates legacy named colors to `#aaaaaa` before V2 validation, keeping existing hex colors unchanged.
- **Why important:** Prevents data loss during the V1→V2 migration for users with custom agent color configurations.

### 3. [#38401 — [contributor] fix(core): load dynamic models for generation](https://github.com/anomalyco/opencode/pull/38401)
- **What:** Allows stateless `/api/generate` requests to use dynamically loaded AI SDK or native provider packages. Fixes failure for Gemini models.
- **Why important:** Enables API users to access all provider models, not just statically registered ones.

### 4. [#38397 — [contributor] refactor(tui): generate syntax from V2 theme](https://github.com/anomalyco/opencode/pull/38397)
- **What:** Generates the full TUI `SyntaxStyle` directly from resolved V2 tokens, mapping prompt extmarks, language syntax, Markdown, feedback, and diff scopes to V2 semantics.
- **Why important:** Major internal refactor to unify the theming system; preserves all 101+ existing test cases.

### 5. [#38406 — [needs:issue] fix(core): retry failed location boot instead of caching the failure for the idle TTL](https://github.com/anomalyco/opencode/pull/38406)
- **What:** Resolves the issue where a failed location boot is cached for the full 60-minute `idleTimeToLive` without recovery. Now retries on failure.
- **Why important:** Directly fixes a serious reliability bug in V2 service graph boot (see Issue #38404).

### 6. [#38408 — fix: pr-standards falsely flags v2-based PRs as missing a linked issue](https://github.com/anomalyco/opencode/pull/38408)
- **What:** Fixes the automated PR standards check to use proper GitHub API references, which are only populated for PRs targeting the default branch.
- **Why important:** Eliminates false negatives for V2 branch PRs, improving CI reliability.

### 7. [#38403 — [contributor, beta] fix(ui): standardize tooltip delay](https://github.com/anomalyco/opencode/pull/38403)
- **What:** Standardizes all tooltip hover delays to 400ms across the product, with an `instant` mode for model-picker details only.
- **Why important:** Improves UX consistency; removes per-call-site `openDelay` control.

### 8. [#37226 — feat(core): per-agent subagent_depth override](https://github.com/anomalyco/opencode/pull/37226)
- **What:** Adds optional `subagent_depth` field to agent config, overriding the global setting. Falls back to `global → 1` if unset.
- **Why important:** Gives power users granular control over agent recursion depth without changing global defaults.

### 9. [#38022 — docs(ecosystem): add opencode-hypa plugin](https://github.com/anomalyco/opencode/pull/38022)
- **What:** Adds the `opencode-hypa` plugin to the official ecosystem plugins table.
- **Why important:** Expands the ecosystem with a community-developed plugin for enhanced functionality.

### 10. [#38033 — docs(readme): add Indonesian language version](https://github.com/anomalyco/opencode/pull/38033)
- **What:** Adds an Indonesian README translation (`README.id.md`).
- **Why important:** Reflects the growing global community; improves accessibility for Indonesian-speaking developers.

---

## Feature Request Trends

1. **Model auto-discovery from OpenAI-compatible providers** — The #1 community ask (185 👍). Users want OpenCode to fetch the `/v1/models` endpoint from LM Studio, Ollama, etc., rather than requiring manual config entries.

2. **Per-agent configuration overrides** — Multiple requests for agent-level settings (subagent depth via #37226, model override via #38333). Users want granular control without editing global config.

3. **TUI/UI improvements with urgency:**
   - FPS limiting for remote work (RDP/XRDP) to reduce CPU load
   - Timestamp and duration on tool execution blocks
   - Right-side user-message quick-jump sidebar
   - Inline LaTeX rendering in CLI

4. **Session and project management:**
   - Global session picker to resume sessions across projects
   - Persistent Edit Project dialog (color/name changes currently lost)
   - Session sync across devices

5. **V2 branch stabilization:** Requests for retry-on-boot-failure, avoiding allocation loops, and reducing per-turn token accumulation are all V2-specific.

---

## Developer Pain Points

1. **Subscription/authentication meltdown** — The `opencode-go` subscription returning "Request blocked by upstream provider" for all models is the dominant pain point today. Multiple duplicate issues, non-English reporters, and zero workaround known.

2. **Silent data loss / state corruption:**
   - Edit Project dialog accepts changes but reverts on reopen
   - Session summary zeroed out after PR #30127
   - "no such column: data" SQLite errors breaking all tools
   - Null-byte file corruption by subagents (#38356)

3. **Performance regressions:**
   - 50% CPU while rate-limit waiting
   - V2 server consuming 1.1 GB RAM and a full core while idle
   - Desktop dialog lag after conversation starts (#38412)

4. **Tool execution reliability:**
   - Infinite loops after tool calls
   - Schema validation errors on bash tool input
   - Wrong model applied when agent selected in new session
   - Inconsistent Plan/Build mode behavior

5. **Lack of error feedback to users:**
   - API errors in `useMutation` are silently swallowed
   - Failed location boots cache error for 60 minutes without retry
   - No indication of tool start time or duration during execution

---

*Digest generated from `anomalyco/opencode` GitHub data — 2026-07-23*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-23

## Today's Highlights

The ecosystem saw an unusually high volume of activity, with 50 issues and 29 PRs updated. A major theme emerged around retry/abort behavior where the OpenAI SDK can sleep for days on 429 errors, alongside a long-standing regression in `httpIdleTimeoutMs` for self-hosted providers that was finally closed. Several infrastructure fixes landed around crash log location, external editor performance, and test environment isolation.

## Releases

No new releases in the last 24 hours. Latest stable remains v0.80.6/v0.80.7.

## Hot Issues

1. **[#6476 – Regression: httpIdleTimeoutMs ignored for self-hosted OpenAI providers](https://github.com/earendil-works/pi/issues/6476)** — 12 comments, CLOSED. After upgrading from v0.80.3→v0.80.6, self-hosted vLLM requests time out after minutes despite explicit timeout settings. Critical for anyone running local models; the 12 comments reflect broad impact on self-hosted users.

2. **[#6686 – Pi automatically logs out of GitHub](https://github.com/earendil-works/pi/issues/6686)** — 10 comments, CLOSED. A recurring issue (relates to #2725) where Pi loses GitHub authentication across restarts on both macOS and Linux. The high comment count suggests this is a persistent pain point for many users.

3. **[#6768 – Compaction broken with Copilot Enterprise](https://github.com/earendil-works/pi/issues/6768)** — 8 comments, OPEN, 8 👍. Context compaction fails entirely for Copilot Enterprise users, with distinct errors for OpenAI ("421 Misdirected Request") and Anthropic models. High community engagement (8 upvotes) signals many enterprise users are blocked.

4. **[#6210 – /scoped-models fails on brackets in model IDs](https://github.com/earendil-works/pi/issues/6210)** — 8 comments, OPEN, tagged `inprogress`. Custom models like `custom/bracketed-model[1m]` cannot be selected because brackets are interpreted as regex patterns. Important for users with unusual model naming conventions.

5. **[#6922 – llama.cpp as default provider shows "No models available"](https://github.com/earendil-works/pi/issues/6922)** — 2 comments, OPEN, 7 👍. Setting `defaultProvider: "llama.cpp"` causes startup failure with no models available. Despite few comments, 7 upvotes indicate many local-model users are impacted by this regression.

6. **[#6911 – OpenAI SDK retry sleeps for days on 429, Escape cannot abort](https://github.com/earendil-works/pi/issues/6911)** — 5 comments, CLOSED. When `maxRetries > 0`, the SDK sleeps the full `Retry-After` header with no cap and ignores `AbortSignal`. Extremely dangerous behavior that can lock up Pi for days; PR #6980 addresses this directly.

7. **[#6652 – Crash log hardcodes ~/.pi/agent/, ignores PI_CODING_AGENT_DIR](https://github.com/earendil-works/pi/issues/6652)** — 4 comments, CLOSED. When using a custom agent directory, TUI crashes still write logs to the default `~/.pi` location, creating a duplicate config tree. Fixed in PR #6958.

8. **[#6940 – OpenRouter cache breakpoint stops before tool results](https://github.com/earendil-works/pi/issues/6940)** — 4 comments, CLOSED. For Anthropic models via OpenRouter, consecutive tool-only turns cause cache breakpoint to stall while uncached input grows, wasting tokens. Impacts cost and latency for tool-heavy workflows.

9. **[#6975 – TUI startup benchmark exits before interactive mode](https://github.com/earendil-works/pi/issues/6975)** — 2 comments, CLOSED. The official profiling script `profile-coding-agent-node.mjs` fails to properly initialize the TUI, providing no useful benchmarks. Fixed in PR #6976.

10. **[#6957 – AWS Bedrock ignores profile when AWS_* env vars present](https://github.com/earendil-works/pi/issues/6957)** — 2 comments, CLOSED. Environment variables take precedence over explicit profile configuration, breaking setups that need to override env-based credentials.

## Key PR Progress

1. **[#6987 – fix(tui): align grapheme widths with terminal cells](https://github.com/earendil-works/pi/pull/6987)** — OPEN. Addresses the notoriously difficult problem of Unicode grapheme width calculation in terminals. Author acknowledges it's a "hacky approach" but necessary for correct rendering of CJK and emoji.

2. **[#6341 – feat(ai): support constrained sampling](https://github.com/earendil-works/pi/pull/6341)** — OPEN, tagged `to-discuss`. Adds opt-in JSON-schema constrained sampling for tool arguments. Enables provider-side structural validation of tool inputs, a powerful feature for deterministic tool output.

3. **[#6984 – feat(ai): honor compat.forceAdaptiveThinking in bedrock-converse-stream](https://github.com/earendil-works/pi/pull/6984)** — CLOSED. Fixes a bug where Claude models requiring adaptive thinking format but not in the allowlist got the wrong thinking type, causing `ValidationException`. Essential for newer Anthropic models on Bedrock.

4. **[#6980 – fix(ai): make provider retries abortable](https://github.com/earendil-works/pi/pull/6980)** — OPEN. Replaces native OpenAI/Anthropic SDK retries with a custom helper that enforces a max delay cap and respects `AbortSignal`. Directly addresses the dangerous day-long sleep issue from #6911.

5. **[#6967 – feat(coding-agent): expose session metadata to bash tools](https://github.com/earendil-works/pi/pull/6967)** — CLOSED. Exposes active session ID, provider, model, and reasoning level as environment variables to subprocesses. Eliminates the need for extensions to manually thread this information.

6. **[#6971 – feat(coding-agent): emit bash_execution_update events](https://github.com/earendil-works/pi/pull/6971)** — OPEN. Adds real-time bash execution events with unique IDs for parallel execution tracking. Useful for editor integrations (e.g., Emacs) that need to correlate output with specific shell commands.

7. **[#6965 – fix: isolate test environment](https://github.com/earendil-works/pi/pull/6965)** — OPEN. Runs test suite from an explicit environment allowlist, isolating home, temp, Git, npm, and XDG state. Prevents flaky tests caused by developer-specific config leaking into the test harness.

8. **[#6881 – feat(ai): use provider-reported cost when available](https://github.com/earendil-works/pi/pull/6881)** — OPEN. Falls back to catalog rates only when the API response doesn't include actual cost. Reads `usage.cost` and `cost_details.upstream_inference_cost` for more accurate billing, especially with BYOK setups.

9. **[#6927 – Add native OpenRouter OAuth support](https://github.com/earendil-works/pi/pull/6927)** — CLOSED. Implements PKCE S256 OAuth flow for OpenRouter with browser authorization and ephemeral localhost callback. Eliminates manual API key management for OpenRouter users.

10. **[#6916 – feat(agent): add AgentHarness execution tools](https://github.com/earendil-works/pi/pull/6916)** — CLOSED. Introduces `AgentHarnessTool` abstraction that passes arbitrary app-specific context (execution environment, session ID) to tool execution. Enables deeper integration for custom agent frameworks built on Pi.

## Feature Request Trends

The most requested feature directions this cycle center on **extension API improvements** and **model/provider flexibility**. Key themes include:

- **Structured approval APIs** (#5954): Extensions want an optional request-for-approval primitive without changing Pi's default full-access behavior.
- **MRU model switching** (#6982): Users want most-recently-used model cycling (via hotkeys) instead of alphabetical ordering.
- **Thinking effort control** (#6974): Requests to enable thinking effort cycling (`shift-Tab`) in tree view and summary dialogs.
- **Per-block thinking labels** (#6988): Extensions need a callback API for dynamic labels per hidden thinking block, not a single global label.
- **VS Code integration** (#6985): Community member built a VS Code extension for Pi and requests listing in the packages repository.

## Developer Pain Points

Recurring frustrations visible in this cycle:

- **Self-hosted / local model breakage**: Multiple issues (#6476, #6922) show that self-hosted setups (vLLM, llama.cpp) are disproportionately affected by regressions, with slow resolution times.
- **Startup and configuration friction**: Crash logs writing to wrong directories (#6652), temp sessions not cleaned up (#6924), and slow external editor launches (#6774) create a rough on-ramp for new users.
- **SDK retry behavior**: The OpenAI/Anthropic SDKs' unconstrained retry logic (#6911) is a latent denial-of-service vector. The community reaction (closed with quick PR fix) suggests this was considered a high-priority bug.
- **Extension discovery**: An extension publisher (#6991) reported that properly configured npm packages are not appearing in the `pi.dev/packages` gallery, indicating potential indexing or validation gaps.
- **OAuth billing confusion**: OAuth-authenticated Anthropic users (#6979) are surprised to find their usage billed as metered API rather than Pro/Max sessions, suggesting unclear documentation or separate code paths.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-23

## Today's Highlights

The v0.20.1 nightly release pipeline failed on `main` due to a red core test suite, cascading into CI breaks across E2E tests and release automation. The team is actively addressing the root cause — a flaky fork dispatch test — while several high-priority bug fixes landed, including critical patches for credential exposure in subprocesses (`#6601`) and the `enable_thinking` parameter bug (`#7284`) that had broken `web_fetch` for all users. On the enhancement front, PRs for channel delivery in the daemon and a new Goal v3 state protocol signal progress toward multi-agent and session-state management capabilities.

## Releases

No stable releases in the last 24 hours. A temporary prerelease `v0.0.0-benchmark-poc.20260722.1` was published solely to validate the GitHub Actions → ECS benchmark worker pipeline; it is not a Qwen Code product release.

## Hot Issues

1. **#7284 [CLOSED/P1] `enable_thinking` forced false in side-query breaks TokenPlan endpoints**  
   A core bug where `runSideQuery` (used by `web_fetch`, classifiers, etc.) always sends `enable_thinking: false`, causing 400 errors on endpoints requiring it. Quickly closed with a fix merged. *Community impact: high — broke web_fetch for all users.*  
   [Issue](https://github.com/QwenLM/qwen-code/issues/7284)

2. **#7537 [CLOSED/P1] Core test suite red on main — fork dispatch test never sees registry.complete**  
   A test flake that turns every open PR's CI red regardless of content. The team closed it, likely with a fix, but the nightly release still failed.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/7537)

3. **#7306 [OPEN/P2] Harden tool-output budgeting, observability, and artifact lifecycle**  
   Phase 1 contracts merged, and shell no-artifact regression coverage landed. The shared finalization implementation is in place. This is critical for predictable agent tool behavior.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/7306)

4. **#6601 [CLOSED/P1] Shell subprocess inherits sensitive env vars (credential exposure)**  
   A security vulnerability: shell subprocesses leaked `QWEN_SERVER_TOKEN` and API keys. Closed with #7256 merged. *Community sentiment: glad this was caught early.*  
   [Issue](https://github.com/QwenLM/qwen-code/issues/6601)

5. **#7489 [OPEN] VS Code Companion: file picker inserts @filename but image not attached**  
   A UX bug: attaching an image inserts text rather than sending image data to the model. Blocks image-based workflows in the VS Code extension.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/7489)

6. **#7449 [OPEN/P3] Enterprise external-memory integration profile**  
   A proposal for provider-neutral external memory integration. Community discussions show interest but the team wants a docs-first approach before API changes.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/7449)

7. **#7516 [OPEN] Main CI failed: E2E Tests on d064bd7dcf98**  
   The primary CI failure that blocked the nightly release. Labeled for autofix.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/7516)

8. **#7452 [CLOSED/P2] cronParser: `*/N` deviates from vixie semantics**  
   A subtle bug where day-of-month/week step patterns didn't follow documented vixie-cron semantics. Closed with a fix.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/7452)

9. **#7404 [CLOSED/P3] Update check timeout too short with long sessions on startup**  
   Chinese-language bug report: the startup version-check would always time out when loading long history sessions. Fixed.  
   [Issue](https://github.com/QwenLM/qwen-code/issues/7404)

10. **#7549 [OPEN] Release Failed for v0.20.1-nightly**  
    The "quality" job failed in the nightly release workflow, cascading from the red core test suite. Shows current instability on `main`.  
    [Issue](https://github.com/QwenLM/qwen-code/issues/7549)

## Key PR Progress

1. **#7490 [OPEN] fix(autofix): retry a skipped-Prepare instead of stranding**  
   Stops infrastructure failures from permanently blocking autofix PRs. Retries instead of going terminal.  
   [PR](https://github.com/QwenLM/qwen-code/pull/7490)

2. **#7517 [OPEN] feat(core): add Goal v3 state protocol**  
   First independently reviewable slice of major session-state work. Defines lifecycle, optimistic concurrency, and turn-boundary persistence.  
   [PR](https://github.com/QwenLM/qwen-code/pull/7517)

3. **#7530 [OPEN] refactor(core): tier prompt fragments by cache stability**  
   Marks prompt fragments with explicit cache-stability tiers and reorders rendering for better LLM cache hit rates.  
   [PR](https://github.com/QwenLM/qwen-code/pull/7530)

4. **#7388 [OPEN] feat(daemon): add explicit channel delivery**  
   Adds named channels for daemon notifications, agent prompt finals, and scheduled tasks. Enables authenticated routing to specific workspace workers.  
   [PR](https://github.com/QwenLM/qwen-code/pull/7388)

5. **#7514 [OPEN] feat(serve): persist workspace channel configuration**  
   First part of channel management for DingTalk, WeCom, and Feishu. Adds workspace-scoped settings store.  
   [PR](https://github.com/QwenLM/qwen-code/pull/7514)

6. **#7534 [OPEN] fix(core): retry requests when providers require thinking**  
   Fixes the `enable_thinking` bug: retries once when a provider returns 400 requiring thinking=true. Complements the #7284 fix.  
   [PR](https://github.com/QwenLM/qwen-code/pull/7534)

7. **#7527 [OPEN] fix(core): strip daemon secrets from hook and tool-discovery child env**  
   Closes remaining credential exposure gaps by applying `sanitizeChildEnv()` to hooks and tool-discovery paths.  
   [PR](https://github.com/QwenLM/qwen-code/pull/7527)

8. **#7186 [CLOSED] fix(cli): share one process.stdout resize listener**  
   Single listener for terminal resize events instead of one per component mount. Reduces memory pressure in long sessions.  
   [PR](https://github.com/QwenLM/qwen-code/pull/7186)

9. **#7542 [OPEN] feat(cli): add version upgrade notices**  
   Startup "What's New" notices for releases with curated highlights. Lightweight and respects existing tip history.  
   [PR](https://github.com/QwenLM/qwen-code/pull/7542)

10. **#7535 [OPEN] fix(scripts): retry model calls and surface degraded release notes**  
    Release notes generator now retries model calls before falling back, and makes degraded runs visible (red) instead of silently green.  
    [PR](https://github.com/QwenLM/qwen-code/pull/7535)

## Feature Request Trends

- **Multi-agent and session visualization** (#7525): Demand for visualizing plan DAGs and linking Todo nodes to subagent executions — users want to see agent orchestration live.
- **External memory / enterprise integration** (#7449): Growing interest in provider-neutral memory profiles and third-party knowledge store integration.
- **Git workflow management** (#6701, #7471): Multiple requests for Git context selectors (local vs. worktree branches) in the Web Shell composer, reflecting real multi-branch workflows.
- **Channel and notification routing** (#7388, #7514): Requests for explicit channel delivery (DingTalk, WeCom, Feishu) and persisted channel configuration — targeting enterprise team use.

## Developer Pain Points

- **CI instability on main**: The red core test suite (#7537) and subsequent CI failures (#7516, #7549) are the top immediate concern, blocking all PRs and nightly releases.
- **Update/registry issues**: Multiple reports (#7404, #7515, #7543) of startup update checks failing due to timeouts, mise wrapper confusion, and registry configuration problems on Windows.
- **Web Shell mobile and VS Code extension UX**: Cumulative frustration with CodeMirror not working on mobile (#5958), image attachment broken in VS Code (#7489), and stale port handling (#7500).
- **Memory/file-read-cache mismatch** (#7287): The auto-memory system loads MEMORY.md into the system prompt but doesn't register the read, causing `write_file` to be rejected on first update — a confusing developer experience for memory-enabled agents.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-23

## Today’s Highlights
The v0.9.1 release train reached near-completion today with 20+ PRs merged addressing the final TUI chrome, skill pack, and security gates. A new Context Diet epic (v0.9.2) was opened, signaling the team’s focus shift toward prompt efficiency and cross-model portability. Several critical bugs were fixed, including a Windows PATH overwriting installer and a Dropbox file access regression, though the latter remains unresolved.

## Releases
No new versions were published in the last 24 hours. The v0.9.1 tag is pending completion of the security gate (Issue #4713) and final dependency audit.

## Hot Issues

1. **#2870 — Epic: staged command-boundary refactor**  
   *Opened by aboimpinto* — Tracks splitting a large refactor into mergeable layers. High comment count (17) reflects continued community design collaboration.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/2870)

2. **#4227 — Help map the CodeWhale tsunami**  
   *Opened by JayBeest* — A skill/workflow to automate dev environment setup. 12 comments from maintainers actively steering the contributor onboarding experience.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4227)

3. **#4684 — `danger-full-access` does not disable tools-layer boundary check**  
   *Opened by AnonymousUser443* — Critical security bypass: the sandbox flag fails to disable file-level access control, breaking legitimate use cases. 2 comments, still open.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4684)

4. **#4085 — Cannot read/write under Dropbox on macOS**  
   *Opened by Watcher24* — Long-standing File Provider limitation. 4 comments, still unresolved. Blocks many macOS users with cloud storage workflows.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4085)

5. **#4685 — CodeWhaleSetup.exe overwrites user PATH on Windows**  
   *Opened by MuRongMoQing* — Installer bug destroys all user PATH entries. 1 comment, open. High severity for Windows users.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4685)

6. **#4683 — Wrong DeepSeek completions URL**  
   *Opened by demian-welt* — Flaky network error hitting `api.deepseek.com`. 1 comment, open. Likely a routing or DNS stability issue.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4683)

7. **#4682 — Custom provider causes launch failure**  
   *Opened by e792a8* — Using `/provider` with a custom name crashes the app. 1 comment, open.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4682)

8. **#4704 — Context diet: minimize every model-facing prompt, schema, and payload**  
   *Opened by Hmbown* — Parent epic of the v0.9.2 performance push. Touches prompt size, duplication, tool descriptions, and attribution gates.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4704)

9. **#4713 — v0.9.1 security gate: deep scan and dependency alert disposition**  
   *Opened by Hmbown* — Release blocker: 17 open Dependabot alerts (7 high, 10 moderate) across npm families like axios, brace-expansion, and fast-uri.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4713)

10. **#4691 — Ship the model-invoked default CodeWhale skill pack**  
    *Opened by Hmbown* — The UX goal that drove much of today’s PR activity: a first-party skill pack comparable to Kimi Code, Devin CLI, and Claude Code. Closed with PR #4692.  
    [GitHub](https://github.com/Hmbown/CodeWhale/issues/4691)

## Key PR Progress

1. **#4675 — Integrate CodeWhale v0.9.1 runtime and release surface** *(Merged)*  
   The main integration PR delivering final TUI color grammar, empty-Work fix, and public release surface. Foundation for the day’s subsequent fixes.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/4675)

2. **#4679 — Unified /skills manager with audit and owned mutations** *(Merged)*  
   *Author: SamhandsomeLee* — Delivers the single Skills lane: install, update, remove, trust across all roots. Closes v0.9.1 completion board item #4650.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/4679)

3. **#4695 — Default CodeWhale skill pack (bundled v5)** *(Merged)*  
   Ships the end-user skill pack (interview, plan, implement, debug, test, review, etc.) required by #4691.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/4695)

4. **#4694 — fix(kimi): fail closed on K3 model-ID cross-pairings** *(Merged)*  
   Hardens provider routing by treating base URL + model ID as one identity.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/4694)

5. **#4711 — fix(tui): focus v0.9.1 chrome on todos and agents** *(Merged)*  
   Replaces generic Work chrome with resizable To-do + Sub-agent bar and theme-native rails.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/4711)

6. **#4696 — feat(tui): ship staged /uwu theme** *(Merged)*  
   Delivers the community-anticipating `uwu` theme with aliases `owo` and `kawaii`.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/4696)

7. **#4714 — chore(deps): patch npm lockfiles for Dependabot alerts** *(Open)*  
   *Author: Hmbown* — Applies `npm audit fix` across workspaces to resolve 17 alerts. Required for v0.9.1 release.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/4714)

8. **#4508 — docs: refresh the Codewhale product screenshot** *(Merged)*  
   Replaces the stale v0.8.61 screenshot with a canonical v0.9.1 TUI capture across README and website.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/4508)

9. **#4680 — fix(tui): register debt compatibility aliases** *(Merged)*  
   *Author: nightt5879* — Adds `/slop` and `/canzha` as `/debt` aliases, improving international discoverability.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/4680)

10. **#4686 — feat(minimax): add China / Token Plan provider routes** *(Open)*  
    *Author: ffaacceelee* — Adds `minimax-cn` and `minimax-anthropic-cn` for api.minimaxi.com, including Anthropic-over-Minimax routing.  
    [GitHub](https://github.com/Hmbown/CodeWhale/pull/4686)

## Feature Request Trends
- **Unified skill management** — The `/skills` PRs dominate: the community wants one CLI surface for discovering, installing, updating, and trusting skills without separate commands.
- **Context efficiency** — The v0.9.2 “Context Diet” epic (#4704) and its 5 sub-issues show strong maintainer demand for reducing prompt bloat, deduplicating project/env/skill context, and adding cross-model ablation gates.
- **Provider flexibility** — Minimax CN routing (#4686), TelecomJS support (#4370), and custom provider fixes (#4682) indicate growing international and multi-provider adoption.
- **Theme and visual polish** — The `/uwu` theme and TUI color grammar work (#4676, #4677) reflect a maturing product where community identity and visual composition become first-class concerns.

## Developer Pain Points
- **Windows installer breaks PATH** — Issue #4685: `CodeWhaleSetup.exe` overwrites PATH instead of appending. High severity, very reproducible, but limited maintainer attention so far.
- **macOS Dropbox accessibility** — Issue #4085: files under File Provider-backed locations are unreadable. Ad-hoc signing with zero entitlements is confirmed. Workaround unclear.
- **`danger-full-access` is not fully effective** — Issue #4684: the sandbox flag doesn’t disable the tools-layer boundary check, breaking global skill access. Expect this to rise in priority as skills adoption increases.
- **Custom providers crash on launch** — Issue #4682: setting a non-default provider name via `/provider` causes a fatal error. New users are the most affected.
- **Flaky DeepSeek API routing** — Issue #4683: intermittent URL failures with no clear resolution path. May be a deeper Rust HTTP client issue.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*