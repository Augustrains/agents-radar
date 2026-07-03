# AI CLI Tools Community Digest 2026-07-03

> Generated: 2026-07-03 01:43 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report — 2026-07-03

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem is experiencing a maturation phase characterized by **platform stability crises** alongside **rapid agentic capability expansion**. Across all seven tools surveyed, communities are reporting session lifecycle bugs, billing accounting errors, and sub-agent reliability issues as their top pain points—indicating that the industry has moved beyond prototype novelty into production deployment friction. Microsoft Copilot CLI and Anthropic's Claude Code show the highest community engagement volume, while Google Gemini CLI and the newcomer Qwen Code demonstrate the most aggressive feature velocity through nightly releases. A notable shift toward **enterprise readiness** is visible: Windows parity (Copilot, Kimi, Qwen, DeepSeek), configurable security sandboxes (Codex, Gemini), and persistent background agent infrastructure (Claude, Qwen) are emerging as core, not nice-to-have, requirements.

---

## 2. Activity Comparison

| Tool | Open/Active Issues (24h) | Open PRs (24h) | Release Status |
|------|-------------------------|----------------|----------------|
| **Claude Code** | ~10 hot issues; 467 upvotes on #38335 | 4 (2 doc fixes, 1 devcontainer, 1 spam) | v2.1.199 (stable patch) |
| **OpenAI Codex** | ~10 hot issues; 680 upvotes on #11023 | 10 active (security hardening focus) | rust-v0.143.0-alpha.34/33 (pre-release) |
| **Gemini CLI** | ~10 hot issues; 8 upvotes on #21409 | 10 active (5 closed, 5 open) | v0.51.0-nightly.20260702 (nightly) |
| **GitHub Copilot CLI** | ~10 hot issues; 9 upvotes on #3501 | 2 (low quality/spam) | v1.0.69-0 (no new release) |
| **Kimi Code CLI** | ~10 hot issues; 6 upvotes on #1077 | 10 active (1 merged) | No release in 24h (latest stable) |
| **OpenCode** | ~10 hot issues; 82 upvotes on #28846 | 10 active (5 closed, 5 open) | v1.17.13 (no new release) |
| **Qwen Code** | ~10 hot issues; P1 bugs on mobile | 10 active (mix closed/open) | v0.19.5 (stable) + nightly |
| **DeepSeek TUI** | ~10 hot issues; 14 comments on #3793 | 10 active (7 merged, 3 open) | Pre-v0.8.67 development cycle |

**Key observations:**
- **Claude Code** and **OpenAI Codex** dominate community volume (highest upvote counts on top issues)
- **Gemini CLI**, **Qwen Code**, and **DeepSeek TUI** are in the most active development cycles (multiple nightly/alpha releases)
- **GitHub Copilot CLI** and **Kimi Code CLI** show lower PR activity, suggesting maintenance-mode or slower iteration
- **OpenCode** shows strong contributor PR presence (multiple community contributions)

---

## 3. Shared Feature Directions

| Need | Affected Tools | Specific User Demands |
|------|---------------|----------------------|
| **Configurable timeouts** | Claude Code (#73125), OpenAI Codex (#28969), Kimi Code (#2455) | Users want tunable `AskUserQuestion` / auto-resolve timers for review-heavy workflows |
| **Sub-agent / multi-agent reliability** | Claude Code (#69824), Gemini CLI (#22323), OpenCode (#35041), DeepSeek TUI (#3932) | Race conditions, orphaned workers, result misrouting; community wants formal orchestration with wait semantics |
| **Windows performance & stability** | Claude Code (#73468), OpenAI Codex (#20214), GitHub Copilot CLI (#3501), Kimi Code (#2481), Qwen Code (#6214), DeepSeek TUI (#1812) | Scrollbar regressions, IME deadlocks, TUI freezes, non-UTF-8 encoding bugs, clipboard paste issues |
| **Custom model endpoints / BYOK** | GitHub Copilot CLI (#4003), Kimi Code (#1077), Pi (#6231) | Users want provider-agnostic fallback chains, private/local model support, enterprise data isolation |
| **Headless / CI-CD support** | Kimi Code (#1095, #1103), GitHub Copilot CLI (#4011), Qwen Code (#6112) | Non-TTY streaming, file-based key storage, batch initialization, background cron/scheduled tasks |
| **Session lifecycle transparency** | Claude Code (#38335), OpenAI Codex (#30918), OpenCode (#28846) | Session/billing budget consumption tracking, provider price change pass-through, cost management |
| **Auto-upgrade reliability** | Claude Code (#73670), Pi (#6215) | Daemon restart failures, orphaned sessions, dependency resolution breaks on update |
| **Enhanced MCP integration** | GitHub Copilot CLI (#4006, #4004), Gemini CLI (#27979), DeepSeek TUI (#3643) | Paginated tool listing, server registration in config, security hardening for untrusted resources |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach | Key Differentiator |
|------|-------------|-------------|-------------------|--------------------|
| **Claude Code** | Deep reasoning & skill composition | Professional developers, enterprise teams | Claude models; sub-agent orchestration; skills library | Strongest thinking/transparency features; largest community issue engagement |
| **OpenAI Codex** | Security-hardened code generation | Security-conscious enterprise, multi-model users | Rust re-write; Git sandboxing; trusted executable boundaries | Most rigorous security hardening (6+ security PRs this cycle) |
| **Gemini CLI** | Model-native operations & agent autonomy | Google Cloud developers, Gemini adopters | Gemini 3 models; AST-aware tools; Auto Memory | Deepest model integration (bash affinity); nightly/iterative releases |
| **GitHub Copilot CLI** | VS Code ecosystem integration | GitHub ecosystem users, CI/CD pipelines | Microsoft/Azure backend; BYOK model switching | Strongest IDE extension synergy; highest packaging stability |
| **Kimi Code CLI** | Multi-provider flexibility | Cost-conscious developers, global users | Go-based; provider fallback chains; OpenRouter support | Most focused on provider agnosticism and cost optimization |
| **OpenCode** | V2 desktop + web experience | Modern full-stack developers, Chinese market | Desktop app + web shell; V2 session architecture | Strongest desktop-native experience (tabs, layout) |
| **Qwen Code** | Chinese-language optimized agents | China-market developers, mobile users | Qwen3 models; WeCom/QQ Bot channels; vision bridge | Best CJK/text handling; enterprise messaging adapters |
| **DeepSeek TUI** | Fleet / sub-agent orchestration | Advanced users, agent-network builders | Rust; Fleet multi-agent system; project-scoped rules | Most ambitious sub-agent architecture; systematic refactoring investment |

---

## 5. Community Momentum & Maturity

**High velocity / early growth stage:**
- **OpenAI Codex** — Massive community growth (680 upvotes on Linux desktop request); active security hardening phase suggests production scaling
- **Gemini CLI** — Aggressive nightly releases; 76+ behavioral eval tests across 6 models; rapid issue closure cadence
- **Qwen Code** — Two stable releases in 24h; enterprise adapter PRs (WeCom, QQ Bot); mobile web-shell optimization signals mobile-first strategy

**Mature / high-engagement stage:**
- **Claude Code** — Largest community engagement (789 comments on #38335); stable patch cadence; but PR pipeline unusually quiet—may be in stabilization cycle
- **GitHub Copilot CLI** — Stable release cadence (v1.0.x); moderate engagement; low PR volume suggests maintenance mode

**Rapid iteration / pre-stable:**
- **DeepSeek TUI** — Active v0.8.67 development; systematic TUI monolith refactoring; Fleet sub-agent system still maturing
- **Kimi Code CLI** — Persistent bug unaddressed for 6 months (#640); community frustration indicates slower response cycle
- **Pi** — 42 closed issues in 24h; big-refactor wave complete; smaller community but high responsiveness

---

## 6. Trend Signals

1. **Agentic orchestration is the new frontier** — Every tool is investing in multi-agent/sub-agent systems, but all are struggling with production reliability. Claude Code, Gemini, OpenCode, and DeepSeek all report race conditions, orphaned workers, and result misrouting. **The industry has not yet solved multi-agent correctness.**

2. **Windows parity remains a critical gap** — Six of seven tools have unresolved Windows-specific bugs. Non-UTF-8 code pages (Qwen), IME input deadlocks (DeepSeek), TUI scrollbar regressions (Copilot), and memory leaks (OpenCode) are blocking adoption on the largest desktop platform.

3. **Cost/billing transparency is eroding trust** — Claude Code (session budget 2-3x expected consumption), OpenAI Codex (Plus tier draining in 6 minutes), and OpenCode (silent model switching to expensive alternatives) all face community backlash over opaque consumption. **Billing instrumentation is becoming a retention-critical feature.**

4. **Move from chat to platform** — Qwen Code's daemon channel workers, DeepSeek's Fleet system, and Claude's sub-agent orchestration point to a future where CLI tools are continuous, background agent platforms rather than interactive chat sessions. The cron/scheduling requests across multiple tools reinforce this.

5. **Security hardening is accelerating** — OpenAI Codex leads with 6+ security PRs this cycle (Git sandboxing, trust boundaries, merge driver blocking). Gemini follows with symlink traversal fixes and untrusted output wrapping. This is becoming table stakes for enterprise adoption.

6. **Chinese-language support is an underserved opportunity** — Qwen Code and DeepSeek TUI are the only tools with active CJK/IME fixes. Given the developer market size, this represents a significant gap for the other tools.

7. **Desktop application is back in demand** — OpenAI Codex (#11023, 680 upvotes) and OpenCode (V2 desktop experience) signal that CLI-only is insufficient; users want persistent desktop apps with proper resource management, tabbed interfaces, and GPU-neutral rendering.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-07-03 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Skill submissions attracted the most community discussion and engagement:

### #1298 — `fix(skill-creator): run_eval.py always reports 0% recall` 
**Author:** MartinCajiao | **Status:** Open | [PR Link](https://github.com/anthropics/skills/pull/1298)

**Functionality:** This is a critical fix for the `skill-creator` meta-skill's evaluation pipeline. The `run_eval.py` script—used by the description-optimization loop (`run_loop.py`, `improve_description.py`)—has been consistently reporting `recall=0%` for every skill description, regardless of content quality. This PR installs the eval artifact as a real skill (so the `claude -p` subprocess can actually trigger it), fixes Windows stream reading, corrects trigger detection logic, and parallelizes workers.

**Discussion highlights:** Addresses Issue #556, which has 7 👍 and 12 comments with 10+ independent reproductions. The root cause is architectural: `claude -p` subprocess calls don't see `.claude/commands/` entries in the same way as interactive sessions. This PR is the most active discussion in the repository because the bug renders the entire skill-optimization workflow non-functional for all contributors.

### #514 — `Add document-typography skill`
**Author:** PGTBoos | **Status:** Open | [PR Link](https://github.com/anthropics/skills/pull/514)

**Functionality:** A skill that enforces typographic quality control in Claude-generated documents. It prevents orphan word wrap (1–6 words on a new line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment. The skill proactively rewrites draft output to apply professional typographic standards before final delivery.

**Discussion highlights:** The community recognizes these issues as universal across AI-generated documents. The skill is praised for solving a pain point that users "rarely ask for" but strongly notice. The main discussion centers on whether typography rules should be bundled into existing document skills or remain standalone.

### #1367 — `feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate`
**Author:** YuhaoLin2005 | **Status:** Open | [PR Link](https://github.com/anthropics/skills/pull/1367)

**Functionality:** A universal auditing skill that runs before Claude delivers output. Step 0 performs mechanical file verification (every claimed output file exists). Then a four-dimension reasoning audit evaluates outputs in damage-severity priority order. Designed to work with any project, tech stack, or model.

**Discussion highlights:** Very recent PR (June 28) with rapidly accumulating comments. The community is debating the priority ordering of audit dimensions and whether mechanical verification should be optional for non-file-generating tasks. This represents a shift toward quality assurance meta-skills.

### #486 — `Add ODT skill — OpenDocument text creation and template filling`
**Author:** GitHubNewbie0 | **Status:** Open | [PR Link](https://github.com/anthropics/skills/pull/486)

**Functionality:** Full OpenDocument Format (.odt, .ods) support—creation, template filling, reading, and conversion to HTML. Includes triggers for "ODT," "ODS," "ODF," "OpenDocument," "LibreOffice document," or any request for open-source/ISO standard document formats.

**Discussion highlights:** This skill addresses a significant gap in the ecosystem. The discussion focuses on whether it overlaps with the existing `pdf` and `docx` skills, and whether the skill should also handle `.ott` templates and password-protected documents.

### #210 — `Improve frontend-design skill clarity and actionability`
**Author:** justinwetch | **Status:** Open | [PR Link](https://github.com/anthropics/skills/pull/210)

**Functionality:** A comprehensive revision of the `frontend-design` skill to ensure every instruction is actionable within a single conversation. The skill provides specific, behavior-steering guidance to Claude for UI/UX design decisions.

**Discussion highlights:** The community debate centers on the tension between comprehensive design guidance and token efficiency. Some argue for splitting into multiple specialized skills (color, layout, accessibility); others prefer a single authoritative skill.

### #83 — `Add skill-quality-analyzer and skill-security-analyzer`
**Author:** eovidiu | **Status:** Open | [PR Link](https://github.com/anthropics/skills/pull/83)

**Functionality:** Two meta-skills: `skill-quality-analyzer` evaluates skills across five dimensions (Structure & Documentation 20%, other criteria), while `skill-security-analyzer` performs security audits. These are the first meta-skills proposed for the marketplace.

**Discussion highlights:** These skills generated significant early interest as the community recognized the need for quality benchmarks. Discussion centers on whether quality analysis should be integrated into the `skill-creator` pipeline or remain as companion tools.

---

## 2. Community Demand Trends

Analysis of the most-commented Issues reveals several clear demand signals:

| Demand Category | Key Issue(s) | Signal Strength |
|---|---|---|
| **Security & Trust Boundaries** | [#492](https://github.com/anthropics/skills/issues/492): Community skills under `anthropic/` namespace impersonate official skills (34 comments, 2 👍) | **Highest** — The security model for skill distribution is the top community concern. Users want namespace verification, permission scoping, and trust validation. |
| **Org-wide Skill Management** | [#228](https://github.com/anthropics/skills/issues/228): Enable org-wide skill sharing (14 comments, 7 👍) | **High** — Enterprise teams need centralized skill distribution without manual `.skill` file sharing via Slack/email. |
| **Skill Creator Pipeline Reliability** | [#556](https://github.com/anthropics/skills/issues/556): `run_eval.py` 0% trigger rate (12 comments, 7 👍); [#1169](https://github.com/anthropics/skills/issues/1169): recall=0% loop; [#1061](https://github.com/anthropics/skills/issues/1061): Windows compatibility | **Critical** — The skill-creation toolchain is broken for many users. This is the top blocker for community contributors. |
| **Deduplication & Package Management** | [#189](https://github.com/anthropics/skills/issues/189): Duplicate skills from overlapping plugins (6 comments, 9 👍) | **High** — Users want clear boundaries between skill packages and no duplicated content. |
| **Agent Governance & Safety** | [#412](https://github.com/anthropics/skills/issues/412): Agent governance patterns proposal (6 comments) | **Emerging** — Growing interest in safety patterns for autonomous agent systems. |
| **Cross-Platform Compatibility** | [#1061](https://github.com/anthropics/skills/issues/1061): Windows failures; [#29](https://github.com/anthropics/skills/issues/29): Bedrock support | **Sustained** — Linux-only assumptions exclude significant user segments. |
| **MCP/Skills Interoperability** | [#16](https://github.com/anthropics/skills/issues/16): Expose Skills as MCPs (4 comments) | **Nascent** — Interest in making skills callable via MCP protocol for broader tool integration. |

**Most anticipated new Skill directions:** (1) Agent governance and safety patterns, (2) Testing generation and patterns, (3) Document typography and quality assurance, (4) Cross-format document conversion (ODT/SAP/color), (5) Meta-skills for quality analysis and security auditing.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and may land soon:

| PR | Skill | Author | Key Features | Adoption Likelihood |
|---|---|---|---|---|
| [#1367](https://github.com/anthropics/skills/pull/1367) | **self-audit** (v1.3.0) | YuhaoLin2005 | Mechanical file verification + 4-dimension reasoning audit; universal across projects | **Very High** — Addresses the universal quality concern; well-structured |
| [#1302](https://github.com/anthropics/skills/pull/1302) | **color-expert** | meodai | Color naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway), color space selection tables (OKLCH, OKLAB, CAM16) | **High** — Self-contained, authoritative, fills a clear gap |
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | 4444J99 | Testing Trophy model, AAA pattern, React Testing Library, Playwright, unit/mock/integration patterns | **High** — Comprehensive; covers full testing stack |
| [#806](https://github.com/anthropics/skills/pull/806) | **sensory** (macOS automation) | AdelElo13 | Native macOS automation via `osascript` (AppleScript); two-tier permission system | **High** — Unique capability; no equivalent skill exists |
| [#509](https://github.com/anthropics/skills/pull/509) | **CONTRIBUTING.md** (docs) | narenkatakam | Community health gap closure; five-section contributor guide | **Medium** — Non-code but high impact for contributor growth |
| [#1367](https://github.com/anthropics/skills/pull/1367) | **compact-memory** (proposed in Issue #1329) | WGlynn | Symbolic notation for compact agent state; reduces context overhead for long-running agents | **Medium** — Addresses a real pain point but still in proposal phase |

**Note:** The `skill-creator` fix PRs (#1298, #1323, #1099, #1050, #538, #539, #541, #362, #361) form a cluster of pending fixes. These may merge as a batch once the evaluation loop fix (#1298) is finalized, as they all address different facets of the same broken pipeline.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable, secure skill-creation tooling—specifically fixing the broken evaluation pipeline—rather than new Skill content, indicating the ecosystem is in a "build the foundation" phase where contributors cannot confidently create or optimize skills until the meta-tooling is trustworthy.**

Secondary demand clusters around **(a) security trust boundaries** for skill distribution (namespace verification, permission scoping), **(b) quality assurance meta-skills** (self-audit, quality analysis), and **(c) cross-platform support** (Windows, Bedrock) to broaden the contributor base. Content-wise, the community most wants **document formatting skills** (typography, ODT, color) and **agent governance patterns**—suggesting a shift from creative/generative use cases toward production-quality document generation and safe autonomous operation.

---

# Claude Code Community Digest — 2026-07-03

---

## Today's Highlights

The latest patch (v2.1.199) fixes a pernicious SSL error-handling issue that was silently burning retries before showing users actionable guidance, a welcome quality-of-life improvement for proxy-constrained environments. However, the community remains laser-focused on two pain points: an 18-month-old Max plan session-limiting bug (#38335) that has amassed 789 comments and 467 upvotes, and a suite of integration bugs in the sub-agent system that are causing race conditions, orphaned workers, and misrouted results. A new auto-upgrade bug (#73670) causing complete in-flight session loss on macOS is also drawing immediate attention.

---

## Releases

- **[v2.1.199](https://github.com/anthropics/claude-code/releases/tag/v2.1.199)** — Two changes:
  - **Stacked slash-skill invocations**: `/skill-a /skill-b do XYZ` now loads all leading skills (up to 5) instead of only the first, making skill composition more predictable.
  - **SSL certificate error resilience**: Fixed a bug where TLS-inspecting proxies, missing `NODE_EXTRA_CA_CERTS`, or expired certificates would cause Claude Code to burn through retry attempts before surfacing actionable guidance. Users now get clarity earlier.

---

## Hot Issues (Top 10 Notable)

1. **[#38335](https://github.com/anthropics/claude-code/issues/38335) — Claude Max plan session limits exhausted abnormally fast since March 23, 2026 (CLI usage)**  
   *Comments: 789 | 👍: 467 | Open since 2026-03-24*  
   This is the single most-active issue in the repository by a wide margin. Community members report their Max plan session budgets being consumed at 2–3x expected rates, often exhausting daily limits after 4–5 hours of active use. Users are frustrated by the lack of resolution after three months.

2. **[#8477](https://github.com/anthropics/claude-code/issues/8477) — [FEATURE] Add Option to Always Show Claude's Thinking**  
   *Comments: 86 | 👍: 307 | Open since 2025-09-30*  
   A long-standing request for an "always show thinking" toggle in the TUI. Since v2.0.0 collapsed thinking visibility into an expandable UI, developers who want continuous visibility into reasoning—especially for debugging agent chains—have been left wanting.

3. **[#73125](https://github.com/anthropics/claude-code/issues/73125) — [BUG] AskUserQuestion: "No response after 60s — continued without an answer"**  
   *Comments: 62 | 👍: 215 | Opened 2026-07-02*  
   A high-velocity issue: `AskUserQuestion` tool times out after 60 seconds with no user-configurable timeout, forcing the agent to proceed without input. This breaks workflows that require user review (e.g., code review approvals, destructive command confirmation). Cross-platform, affecting Bedrock API, Linux TUI, VS Code extension.

4. **[#10238](https://github.com/anthropics/claude-code/issues/10238) — [FEATURE] Add support for subdirectories in skills**  
   *Comments: 46 | 👍: 162 | Open since 2025-10-24*  
   Teams building skill libraries are forced into flat directory structures, making organization difficult at scale. Demand for nested skill directories has been growing steadily.

5. **[#65833](https://github.com/anthropics/claude-code/issues/65833) — v2.1.150 regression: scroll wheel no longer scrolls conversation — sends arrow keys instead**  
   *Comments: 29 | 👍: 53 | Open since 2026-06-06*  
   A regression affecting WSL users that maps scroll events to arrow keys (cycling input history) instead of scrolling conversation output. This is a progression blocker for daily TUI users.

6. **[#69824](https://github.com/anthropics/claude-code/issues/69824) — [Bug] Subagents not awaiting nested subagent results, causing duplicate work and race conditions**  
   *Comments: 5 | 👍: 0 | Opened 2026-06-21*  
   A critical concurrency bug: sub-agents spawn nested agents but do not await their results, instead hallucinating task notifications. The parent then either proceeds prematurely or duplicates work. This undermines confidence in multi-agent workflows.

7. **[#73670](https://github.com/anthropics/claude-code/issues/73670) — Daemon supervisor shuts down for auto-upgrade but never restarts; bg workers orphan-watchdog-killed 60s later, all in-flight sessions lost (2.1.198→2.1.199)**  
   *Comments: 0 | 👍: 0 | Opened 2026-07-03*  
   A newly filed, zero-comment issue with high severity: the daemon does not restart after auto-upgrade, leaving background workers orphaned and subsequently killed by the watchdog. All in-flight sessions are lost. This is the exact kind of issue that triggers rapid hotfixes.

8. **[#73468](https://github.com/anthropics/claude-code/issues/73468) — macOS sandbox unusable: Seatbelt profile passed inline via 'sandbox-exec -p' exceeds ARG_MAX with many git worktrees**  
   *Comments: 1 | 👍: 1 | Opened 2026-07-02*  
   Users with large Git worktrees cannot run any sandboxed Bash commands—even `printf ok`—because the generated sandbox profile exceeds macOS `ARG_MAX`. The sandbox is completely non-functional in this scenario.

9. **[#73674](https://github.com/anthropics/claude-code/issues/73674) — /goal completion Stop hook re-matches phrases from earlier in the transcript forever**  
   *Comments: 0 | 👍: 0 | Opened 2026-07-03*  
   The goal-completion Stop hook matches trigger phrases against the *entire* transcript rather than current state, meaning a resolved status like "BLOCKED" from an earlier message can prevent clean session termination. Breeds assistant-loop behavior.

10. **[#73672](https://github.com/anthropics/claude-code/issues/73672) — Claude 3.5 Sonnet incorrectly escalated to Opus 4 on safe message**  
    *Comments: 0 | 👍: 0 | Opened 2026-07-03*  
    A false-positive model escalation: a safe, ordinary message triggered automatic escalation from a cost-effective model to a premium one. Raises concerns about the cost management system's reliability.

---

## Key PR Progress

Notable PRs are limited today (total 4 open PRs):

1. **[#72451](https://github.com/anthropics/claude-code/pull/72451) — fix: remove statsig.anthropic.com from init-firewall.sh**  
   *Updated 2026-07-02*  
   A stale DNS hostname (`statsig.anthropic.com`) was causing devcontainer startup failures. This PR removes it from the firewall allowlist. Important for developers using devcontainers.

2. **[#73476](https://github.com/anthropics/claude-code/pull/73476) — docs: fix GitHub capitalization in README**  
   *Updated 2026-07-02*  
   Fixes "Github" → "GitHub" in README.md. Doc-only.

3. **[#72866](https://github.com/anthropics/claude-code/pull/72866) — docs: fix Github → GitHub typo in README**  
   *Updated 2026-07-02*  
   Identical fix to #73476, submitted independently. Suggests multiple contributors noticing the same issue.

4. **[#72543](https://github.com/anthropics/claude-code/pull/72543) — Create Cha**  
   *Updated 2026-07-02*  
   No description; likely spam or an incomplete draft.

**Observation**: The PR pipeline is unusually quiet, with no feature or bug-fix PRs beyond devcontainer tooling and documentation cleanup. This may indicate the team is in a release stabilization cycle.

---

## Feature Request Trends

- **Configurable timeouts** (AskUserQuestion, tool calls): The most-requested TUI/UX improvement. Developers want the ability to lengthen timeouts for review-heavy workflows.
- **Persistent visibility controls**: "Always show thinking" toggle (#8477) and "double ESC for Vim mode" (#10621) reflect a desire for finer-grained UI customization.
- **Skill/library organization**: Subdirectory support in skills (#10238) is the top organizational feature request, driven by teams scaling their skill libraries.
- **Hook extensibility**: A new request (#73669) asks for a `PreResponse` hook that fires *before* assistant prose is rendered, enabling content filtering without the "flash-of-incorrect-output" pattern that `Stop` hooks currently exhibit.
- **Sub-agent workflow improvements**: The underlying sentiment from multiple bugs (duplicate work, result misrouting, status deadlock) points to a community wanting a formal sub-agent orchestration model with proper await semantics and result routing.

---

## Developer Pain Points

1. **Session/cost limit unpredictability** — The Max plan session-limiting bug (#38335) dominates all discussion. Users report running out of session budget 2–3x faster than expected, with Anthropic's usage dashboards showing 52% utilization while CLI refuses further sessions. This erodes trust in the billing model.

2. **Auto-upgrade reliability** — The daemon restart failure (#73670) that kills in-flight sessions is a sharp reminder of the risks of transparent upgrades. Combined with the ghost remote session problem (#73675), users are losing work and session continuity.

3. **Sub-agent system fragility** — Multiple bugs (#69824, #69212, #73400, #72368, #73267) paint a picture of a sub-agent system that is not yet production-ready:
   - Nested agents not awaited, causing race conditions
   - Results routed to wrong parent (root instead of spawning teammate)
   - Background agents stuck in "running" status after completion
   - Documentation still referencing a removed `/agents` wizard (#72945)

4. **macOS sandbox usability** — The `ARG_MAX` failure (#73468) renders the sandbox unusable for any real-world project with branching or worktrees, which is most projects.

5. **Rate limiting opacity** — Multiple reports (#73660, #73509) of API-level rate limiting with messages like "Server is temporarily limiting requests (not your usage limit)" but no actionable guidance on remediation or mitigation.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**Generated: 2026-07-03**

### 1. Today's Highlights

The Codex ecosystem is in a major security hardening phase, with a wave of merged and open PRs focused on Git sandboxing and trusted executable boundaries. However, the community remains deeply engaged with two long-standing pain points: the demand for a native Linux desktop app and a massive data-waste bug on Windows. All major metrics indicate high interest in improving Windows parity and configurability.

### 2. Releases

Two alpha releases were published in the last 24 hours on the `rust-v0.143` branch:
- **rust-v0.143.0-alpha.34**
- **rust-v0.143.0-alpha.33**

Both release notes only state "Release 0.143.0-alpha.x" with no further changelog. These appear to be pre-release builds.

### 3. Hot Issues

*   **#11023 – [OPEN] [enhancement, app] Codex desktop app for Linux**
    *   *Why it matters:* The most-upvoted issue in the repository (680 👍), with 139 comments, reflecting massive demand for native Linux support. The author cites power consumption issues on Mac as the driver.
    *   *Link:* https://github.com/openai/codex/issues/11023

*   **#28224 – [OPEN] [bug, CLI, performance] Codex SQLite feedback logs can write ~640 TB/year and rapidly consume SSD endurance**
    *   *Why it matters:* A critical, high-impact bug on Windows. The author reports that fixes in PRs #29432 and #29457 (released in 0.142.0) have already reduced log volume by 85%. Still a top-voted issue (419 👍) and demonstrates a systemic data-waste problem.
    *   *Link:* https://github.com/openai/codex/issues/28224

*   **#8648 – [OPEN] [bug, context, agent] Codex replies to earlier messages instead of latest one in conversations**
    *   *Why it matters:* A persistent context-handling bug that undermines conversational flow. The community reports this across multiple models (GPT-5.2), making it a UX-critical regression.
    *   *Link:* https://github.com/openai/codex/issues/8648

*   **#13041 – [OPEN] [bug, connectivity] WebSocket upgrade succeeds then server closes with 1008 Policy**
    *   *Why it matters:* Intermittent connectivity issues on Arch Linux. The WebSocket handshake succeeds but is immediately terminated, forcing fallback to HTTPS and causing reconnect loops. 161 upvotes show it's a widely experienced disruption.
    *   *Link:* https://github.com/openai/codex/issues/13041

*   **#16857 – [OPEN] [bug, app, performance] High GPU usage while the app is “thinking” due to tiny useless animation**
    *   *Why it matters:* A performance regression on Mac (Apple Silicon) where a minor animation causes high GPU load during idle "thinking" states. Creates thermal and battery issues for mobile users.
    *   *Link:* https://github.com/openai/codex/issues/16857

*   **#20214 – [OPEN] [bug, windows-os, app, performance] Codex App frequently freezes/stutters on Windows 11 Pro**
    *   *Why it matters:* Windows stability remains a top complaint. This issue reports consistent stuttering even on well-specced Ryzen 5 / 32GB RAM machines. 39 upvotes signal a high-impact problem.
    *   *Link:* https://github.com/openai/codex/issues/20214

*   **#28969 – [OPEN] [bug, enhancement, CLI, config, plan] Add setting to disable the auto-resolve in 60 seconds for questions**
    *   *Why it matters:* Users want deterministic control over the session lifecycle. The current 60-second auto-resolve timeout is disruptive for complex debugging. 74 upvotes with strong traction.
    *   *Link:* https://github.com/openai/codex/issues/28969

*   **#13729 – [OPEN] [bug, windows-os, TUI, CLI] Windows: Ctrl+V multiline paste executes immediately**
    *   *Why it matters:* A critical UX inconsistency on Windows where paste behavior differs from Shift+Insert. This is a safety concern (unintended execution) and was logged six months ago without resolution.
    *   *Link:* https://github.com/openai/codex/issues/13729

*   **#24431 – [OPEN] [bug, model-behavior] GPT-5.5 performance and reliability seem significantly worse today**
    *   *Why it matters:* Reports of a sudden regression in GPT-5.5's ability to fix bugs and maintain project state. High engagement suggests a backend model change that degraded output quality.
    *   *Link:* https://github.com/openai/codex/issues/24431

*   **#30918 – [OPEN] [bug, rate-limits, app] Usage limits draining abnormally fast on Plus: 70% to 100% in about 6 minutes**
    *   *Why it matters:* A critical billing/accounting bug on Plus tier. A user logs from macOS showing 30% consumed in under 6 minutes, suggesting either a double-counting issue or runaway tool usage.
    *   *Link:* https://github.com/openai/codex/issues/30918

### 4. Key PR Progress

*   **#30493 – [OPEN] Add configurable multi-agent mode hint text**
    *   *Why it matters:* Allows deployments to configure a custom delegation policy for Multi-agent V2, bypassing the built-in reasoning-effort-based defaults. Enables stable, deterministic agent delegation.
    *   *Link:* https://github.com/openai/codex/pull/30493

*   **#30801 – [OPEN] [codex] sanitize exec config summary values**
    *   *Why it matters:* Introduces control-character normalization in the execution configuration summary, closing an injection path where repo-controlled config could corrupt command output.
    *   *Link:* https://github.com/openai/codex/pull/30801

*   **#30876 – [OPEN] [core] Support interleaved response items**
    *   *Why it matters:* Fixes a TUI output issue where reasoning and final-answer events arrive out of order. Ensures complete, deduplicated rendering in the terminal.
    *   *Link:* https://github.com/openai/codex/pull/30876

*   **#30837 – [OPEN] Derive effective patch paths through Git**
    *   *Why it matters:* Replaces manual diff-header parsing with `git diff-tree` to avoid misidentification of renames/copies. Critical for accurate patch safety checks.
    *   *Link:* https://github.com/openai/codex/pull/30837

*   **#30850 – [OPEN] Block selected Git filters before staging patch paths**
    *   *Why it matters:* Prevents a path that was validated as a file from becoming a directory during `git add`, which would violate sandbox boundaries. Part of a larger hardening push.
    *   *Link:* https://github.com/openai/codex/pull/30850

*   **#30896 – [OPEN] Centralize repository authority for Git helper launches**
    *   *Why it matters:* Creates a single operation-scoped authority that trusts a Git executable once and caches the trust, solving performance timeouts on Windows from repeated child-process checks.
    *   *Link:* https://github.com/openai/codex/pull/30896

*   **#30854 – [OPEN] Block selected merge drivers before three-way patch application**
    *   *Why it matters:* Prevents `git apply --3way` from executing custom merge drivers from untrusted repositories. A safety fix for a previously unguarded Git execution boundary.
    *   *Link:* https://github.com/openai/codex/pull/30854

*   **#30844 – [OPEN] Confine staged patch paths to the parent worktree**
    *   *Why it matters:* Ensures that symlinks, submodules, and junctions cannot escape the parent worktree during Git staging. Mitigates a directory-traversal risk.
    *   *Link:* https://github.com/openai/codex/pull/30844

*   **#30752 – [OPEN] Wire reasoning summary delivery configuration**
    *   *Why it matters:* Adds configurable delivery modes (sequential, concurrent, concurrent_cutoff) for reasoning summaries, giving users control over how model thinking is streamed in the UI.
    *   *Link:* https://github.com/openai/codex/pull/30752

*   **#30628 – [OPEN] [codex] Trust only system PowerShell parsers on Windows**
    *   *Why it matters:* Ensures PowerShell command parsing uses only system PowerShell executables, blocking a fake-powershell escalation path. Directly addresses a security vulnerability.
    *   *Link:* https://github.com/openai/codex/pull/30628

### 5. Feature Request Trends

1.  **Native Linux Desktop App** (#11023): The single most-requested feature. Users want to escape poor battery and thermal performance on Mac laptops and use Codex on high-performance Linux workstations.
2.  **Enhanced Windows Sandbox & MCP** (#29193, #30486, #30343): Demands for parity between Windows Desktop and Codex CLI's MCP capabilities, especially for `node_repl` and browser/computer-use tooling.
3.  **Configurable CLI Behavior** (#28969): Strong demand for disabling auto-resolve, controlling paste behavior (#13729), and customizing per-project commands.
4.  **Worktree UI Improvements** (#22316, #10704): Users want to select existing git worktrees and see "Sync to local" options even in detached-HEAD states.
5.  **Localization** (#30961): A new report that locale overrides have no effect, indicating demand for a non-English UI.

### 6. Developer Pain Points

*   **Windows Performance & Stability**: Three active issues (#20214, #30055, #29193) report severe stalls, system freezes, and temperature spikes on well-specced Windows machines, pointing to a systemic resource-management bug.
*   **Data Waste & SSD Wear**: The long-running SQLite log problem (#28224) showed that bad logging could consume 640 TB/year. Even with an 85% fix, the underlying architecture remains fragile.
*   **WebSocket Connectivity Flakiness**: A long-standing issue (#13041, 6 months old) on Arch Linux remains unresolved, forcing users into fallback HTTPS reconnection loops.
*   **Context/Session Corruption**: Multiple reports (#8648, #30410, #14162) about chat history failing to load or the model replying to old messages, breaking the core conversation model.
*   **Billing/Usage Accounting**: A new but alarming report (#30918) about usage draining abnormally fast on Plus tier, which could indicate a double-counting bug with financial impact to users.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-03

## Today's Highlights

A security fix landed in the nightly release to resolve a symbolic link directory traversal vulnerability in the memory import processor. The community continues to surface critical agent reliability issues, particularly around subagent recovery misreporting and terminal buffering corruption. Several high-quality pull requests are in flight addressing thought leakage, OAuth token exchange failures, and Jupyter Notebook file corruption.

---

## Releases

**v0.51.0-nightly.20260702.gff00dacd9** — [Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.51.0-nightly.20260701.g7f00c5fe5...v0.51.0-nightl)

- **Fix:** Resolved symbolic link directory escape in memory import processor (`#28233`) — prevents path traversal when processing memory imports via symlinked directories.

---

## Hot Issues (Top 10)

1. **#22323** — [Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323) (9 comments, 2 👍)  
   *Why it matters:* Critical misreporting bug: the `codebase_investigator` subagent returns `status: "success"` with `Termination Reason: "GOAL"` even when it hit its turn limit before performing any analysis. This masks agent capacity issues and undermines trust in agent output.

2. **#19873** — [Leverage model's bash affinity via Zero-Dependency OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873) (8 comments, 1 👍)  
   *Why it matters:* Proposes making the CLI's shell execution model match how Gemini 3 natively operates — using POSIX tools directly — while sandboxing for safety. High-priority enhancement that could dramatically improve speed and reduce tool overhead.

3. **#24353** — [Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353) (7 comments)  
   *Why it matters:* Epic tracking the expansion of behavioral eval tests (now 76 tests across 6 Gemini models). Ensures regressions are caught before release; community sees this as essential for production use.

4. **#22745** — [Assess AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745) (7 comments, 1 👍)  
   *Why it matters:* Investigates whether AST-aware tools can reduce token waste and turn count by precisely reading method bounds. Could significantly improve large codebase navigation.

5. **#21409** — [Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409) (7 comments, 8 👍)  
   *Why it matters:* High community impact — the generalist agent hangs indefinitely on simple tasks like folder creation. Users are forced to work around it by disabling subagent delegation entirely. The 8 upvotes reflect broad frustration.

6. **#21968** — [Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968) (6 comments)  
   *Why it matters:* User-defined skills (e.g., `gradle`, `git`) are ignored unless explicitly invoked, even when highly relevant. Undermines the value proposition of custom agent skills.

7. **#25166** — [Shell command execution gets stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166) (4 comments, 3 👍)  
   *Why it matters:* Simple shell commands hang post-execution while showing "Awaiting user input." A P1 blocker affecting basic day-to-day CLI usage.

8. **#26525** — [Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525) (5 comments)  
   *Why it matters:* Security concern: Auto Memory sends transcript content to model context before redacting secrets. Logging of skill transcript data compounds the risk.

9. **#26522** — [Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522) (5 comments)  
   *Why it matters:* Sessions the extraction agent deems "low-signal" remain unprocessed in the index, causing infinite retries. Wastes API quota and CPU resources.

10. **#22672** — [Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672) (3 comments, 1 👍)  
    *Why it matters:* The model occasionally uses `git reset --force` or dangerous DB commands when safer alternatives exist. Community wants built-in guardrails for destructive operations.

---

## Key PR Progress (Top 10)

1. **#28167** — [feat(caretaker): egress cloud run service skeleton](https://github.com/google-gemini/gemini-cli/pull/28167) ✅ *CLOSED*  
   Implements the Egress Cloud Run Service to receive validated action events from the Triage Worker via Cloud Pub/Sub. Backend infrastructure for the caretaker agent system.

2. **#27979** — [Wrap read_mcp_resource output with wrapUntrusted()](https://github.com/google-gemini/gemini-cli/pull/27979) ✅ *CLOSED*  
   Fixes MCP security inconsistency: MCP server resource text was not marked untrusted before reaching the model, while sibling MCP tools were. Closes #27983.

3. **#28223** — [Bypass LLM correction for JSON and IPYNB files in write_file and replace](https://github.com/google-gemini/gemini-cli/pull/28223) 📝 *OPEN*  
   Surgical fix for corruption of `.ipynb` and `.json` files. Prevents the model from "correcting" structurally valid but non-standard formatting in these formats.

4. **#28244** — [Use a safe test command instead of rm -rf /](https://github.com/google-gemini/gemini-cli/pull/28244) 📝 *OPEN*  
   Policy engine docs previously instructed users to test deny rules with `rm -rf /`. Replaced with a safe alternative. Fixes #28231.

5. **#28240** — [Add support for AGENTS.md out of the box](https://github.com/google-gemini/gemini-cli/pull/28240) 📝 *OPEN*  
   Fixes #28227: `AGENTS.md` context file was silently ignored unless explicitly configured. Now defaults to loading both `GEMINI.md` and `AGENTS.md`.

6. **#28164** — [Limit recursive reasoning turns per single user request](https://github.com/google-gemini/gemini-cli/pull/28164) 📝 *OPEN*  
   Enforces a 15-turn recursive reasoning cap (configurable) to prevent infinite loops that waste CPU and API quota.

7. **#28103** — [Avoid keep-alive socket reuse during OAuth token exchange](https://github.com/google-gemini/gemini-cli/pull/28103) 📝 *OPEN*  
   Fixes "Sign in with Google" failures on Node.js 24.17.0, 22.23.0, and 26.3.0 due to CVE-2026-48931 response queue poisoning.

8. **#27971** — [Strip thoughts from scrubbed history turns](https://github.com/google-gemini/gemini-cli/pull/27971) ✅ *CLOSED*  
   Eliminates "Thought Leakage" — internal model reasoning monologues leaking into plain-text history, causing the model to emulate scratchpad thoughts in subsequent turns.

9. **#27996** — [Decode response body using charset from Content-Type header](https://github.com/google-gemini/gemini-cli/pull/27996) ✅ *CLOSED*  
   `web-fetch` now respects non-UTF-8 charsets (GBK, ISO-8859-1), fixing garbled content for Chinese, Japanese, and legacy sites.

10. **#27986** — [Report cached and thought tokens in PromptResponse.usage](https://github.com/google-gemini/gemini-cli/pull/27986) ✅ *CLOSED*  
    ACP server mode now reports cached and reasoning token counts, fixing ~3× cost overestimation for ACP clients.

---

## Feature Request Trends

Three clear themes dominate community feature requests this week:

1. **Agent self-awareness and introspection** — Users want agents that understand their own capabilities, configuration, and limits. Multiple issues request accurate CLI flag reporting (#21432), subagent trajectory sharing (#22598), and the ability for agents to explain their internal state.

2. **AST-aware code navigation** — A strong push (#22745, #22746) for Abstract Syntax Tree-based file reads and codebase mapping to reduce turn count, token waste, and misaligned reads when working with large repositories.

3. **Deterministic safety and sandboxing** — The community consistently asks for zero-dependency sandboxing (#19873), destructive operation guardrails (#22672), and deterministic secret redaction before model exposure (#26525) rather than after.

---

## Developer Pain Points

- **Subagent reliability is the #1 frustration:** Agents that claim success while failing (MAX_TURNS misreporting), hang indefinitely, or ignore user-configured skills erode trust. Workarounds like disabling subagent delegation are common.

- **Terminal and I/O issues degrade daily workflow:** Shell commands hanging post-completion (#25166), emoji corruption (#28224), terminal resize flicker (#21924), and ghost text infinite loops (#27747) make basic CLI interactions unreliable.

- **Auto Memory system is resource-hungry and leaky:** The background extraction agent retries low-signal sessions forever (#26522), logs unredacted transcript content (#26525), and silently skips invalid patches (#26523). Developers report significant wasted API credits and CPU load.

- **Configuration inconsistencies persist:** Symlinked agent files are ignored (#20079), settings.json overrides don't apply to the browser agent (#22267), and AGENTS.md isn't loaded by default (#28240). Users must manually work around these gaps.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-03

## Today's Highlights
The repository saw a surge in triage-level issues this week, with 30 items updated in the last 24 hours—several touching on theme persistence, MCP server integration, and BYOK model switching. A notable cluster of rendering and clipboard bugs on Windows and macOS suggests ongoing terminal compatibility challenges. No new releases were published.

## Releases
No new releases in the last 24 hours. The latest publicly available version remains **v1.0.69-0**.

## Hot Issues

1. **#3997 — Model "gpt-5.3-codex" is not available**  
   *Author: A-Infor* | [Issue](https://github.com/github/copilot-cli/issues/3997)  
   A user cannot start an agent session because the backend reports the default model as unavailable. 6 comments, no upvotes yet. This is a potential service-side outage or config mismatch that blocks all agent functionality.

2. **#3501 — Scroll bar makes text unalign (Windows)**  
   *Author: anporumb* | [Issue](https://github.com/github/copilot-cli/issues/3501)  
   High-community-interest bug (👍9) where the vertical scroll bar introduced around v50 breaks text alignment on Windows Console Host and Terminal. Users cannot self-help via Copilot's own suggestions. Persists across terminals—indicative of a core rendering issue.

3. **#3936 — Ctrl+G should expand paste tokens to full text in $EDITOR**  
   *Author: automotua* | [Issue](https://github.com/github/copilot-cli/issues/3936)  
   When `compactPaste` is on, pasting large blocks collapses to a token. Pressing Ctrl+G writes the literal token to the editor instead of expanding it, breaking the edit flow. Community parity request vs Claude Code.

4. **#3158 — Plan→Compact→Re-Plan infinite loop (217 cycles)**  
   *Author: Akhi-microsoft* | [Issue](https://github.com/github/copilot-cli/issues/3158)  
   High-severity bug: after ~75% context, the agent compacts, reads summary, and replans indefinitely—zero execution across 217 cycles. Internal routing from Microsoft's agency team. No workaround reported.

5. **#4003 — Support custom model endpoint in Copilot CLI**  
   *Author: holwon* | [Issue](https://github.com/github/copilot-cli/issues/4003)  
   Users want the CLI to support custom endpoints (like VS Code's Language Models panel) for local/private model development and enterprise data isolation. 2 comments, early-stage.

6. **#4015 — Theme setting not remembered**  
   *Author: zachbryant* | [Issue](https://github.com/github/copilot-cli/issues/4015)  
   After `/settings theme <theme>` introduction in v1.0.69-0, the chosen theme reverts on next session. Blue GitHub theme is lost; default keeps resetting. Fresh issue, no comments yet.

7. **#4014 — Rendering all messed up when adding MCP server via /mcp**  
   *Author: Petermarcu* | [Issue](https://github.com/github/copilot-cli/issues/4014)  
   Visual corruption during `/mcp add` workflow. Screenshot attached shows scrambled terminal output. Affects v1.0.69-0. No workarounds noted.

8. **#4009 — Terminal mouse-selection copy corrupted by scrollbar column**  
   *Author: TWiStErRob* | [Issue](https://github.com/github/copilot-cli/issues/4009)  
   Every copied line ends with padding and a `┃` glyph from the scrollbar column. Makes clean output copying impossible. Related to #3501—both stem from scrollbar rendering changes.

9. **#4013 — macOS: Ctrl+V image paste fails with raw clipboard data**  
   *Author: axiom0x0* | [Issue](https://github.com/github/copilot-cli/issues/4013)  
   Image paste is a no-op on macOS 15 when clipboard contains raw image data (from SnagIt, Preview.app). Drag-and-drop works. Only file-URL pasting is supported.

10. **#4006 — MCP `tools/list` pagination (nextCursor) not followed**  
    *Author: ari-luokkala* | [Issue](https://github.com/github/copilot-cli/issues/4006)  
    Copilot CLI ignores `nextCursor` in MCP `tools/list` responses, only loading the first page. Violates MCP spec. Silent failure—users may miss tools.

## Key PR Progress

1. **#3880 — "beyond the streets of amaerica"**  
   *Author: 4tha5* | [PR](https://github.com/github/copilot-cli/pull/3880)  
   Appears to be a template or example PR with a Card/ArtistCard UI component. Likely not production-intended. No comments.

2. **#3873 — "1000Add initial console log for greeting"**  
   *Author: EverydayEvertime* | [PR](https://github.com/github/copilot-cli/pull/3873)  
   Minimal PR adding a console log. No description. Unclear intent—may be a test or junk PR.

## Feature Request Trends

- **BYOK & Custom Model Endpoints** — Multiple issues (#4003, #3978, #4012) ask for parity with VS Code's ability to configure custom/private model endpoints and to persist BYOK model selection across sessions. Users want local model development and enterprise isolation.
- **Non-interactive `/init`** — Request for headless batched initialization to support CI/CD automation and shell scripting (#4011).
- **Persistent Deny Rules** — Users need `permissions-config.json` to support `deny` rules (not just `allow`) for granular tool command control (#3995).
- **Live Terminal Panels for Extensions** — Plugin authors want to render refreshing live panels (e.g., sub-agent progress dashboards) rather than scrolling text logs (#3979).
- **Screen-reader Accessibility** — Blind and low-vision users request character echo and edit-review support during prompt input (#3993).

## Developer Pain Points

- **Rendering & Scrollbar Regression** — A major theme this week: the new scrollbar (#3501, #4009) breaks text alignment, corrupts mouse selection copies, and causes visual chaos during MCP add (#4014). Cross-platform but especially severe on Windows.
- **Model Availability & Switching** — Users hit "model not available" errors (#3997) and unexpected auto-revert to previous models after BYOK setup (#3978). Session continuity is disrupted.
- **MCP Integration Gaps** — Plugins fail to register MCP servers into `mcp-config.json` (#4004), pagination is ignored (#4006), and two plugins with same-named MCP servers silently conflict (#3893). The MCP pipeline feels incomplete.
- **Windows CI/CD Hooks** — `.claude/settings.json` hooks execute via PowerShell instead of bash and lack `$CLAUDE_PROJECT_DIR`, causing all hooks to fail-closed on Windows (#4001).
- **Session Lifecycle Confusion** — `/clear` vs `/new` semantics remain unclear (#3569), and `/new` discards in-memory token usage without writing `session.shutdown` to `events.jsonl` (#3994). Users lose audit data.
- **Spam Issues** — Four abusive/spam issues (#3230, #3229, #3228, #3227) from the same author remain open for over 7 weeks, suggesting weak moderation or automated cleanup.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date:** 2026-07-03

---

## Today's Highlights

The community continues to face a critical looping bug (#640) affecting custom Anthropic endpoints that has remained unresolved since January, while a resolved Tailscale WebSocket connectivity issue (#1111) offers relief for VPN users on macOS. A new PR (#2481) addresses a long-standing clipboard paste problem for Windows users by supporting media-rich content via BracketedPaste events, improving terminal UX on Windows Terminal and VS Code.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#640] [bug] Kimi CLI stuck in reading one file repeatedly**  
   *Status: OPEN | Updated: 2026-07-02 | 👍: 1*  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/640)  
   **Why it matters:** Long-standing critical bug (since Jan 2026). Users on custom Anthropic endpoints (model `mimo-v2-flash`) report the CLI enters an infinite loop re-reading a single file. With 16 comments and no fix in 6 months, this is causing serious reliability concerns for advanced users. Community is frustrated by the lack of progress.

2. **[#1111] [bug] Kimi Web uses Tailscale WebSocket connection error**  
   *Status: CLOSED | Updated: 2026-07-02 | 👍: 0*  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/1111)  
   **Why it matters:** Resolved issue affecting macOS users with Tailscale. WebSocket connections over Tailscale VPN were failing, blocking CLI access. The closure after a lengthy 5-month period suggests either a workaround or fix is now available.

3. **[#1056] [bug] Large file upload crashes Kimi Code CLI**  
   *Status: OPEN | Updated: 2026-06-30 | 👍: 3*  
   **Why it matters:** Files over ~100KB cause memory exhaustion and hard crashes. No response from maintainers. Critical for developers who work with logs, CSVs, or codebases.

4. **[#1095] [feature] Support for streaming output in non-TTY mode**  
   *Status: OPEN | Updated: 2026-06-29 | 👍: 5*  
   **Why it matters:** Piped output from Kimi CLI breaks when not connected to a terminal. High demand from CI/CD and automation users.

5. **[#1103] [bug] Keyring credential storage fails on headless servers**  
   *Status: OPEN | Updated: 2026-06-28 | 👍: 2*  
   **Why it matters:** SSH users and remote server developers cannot store API keys without a desktop keyring. Common pattern in DevOps environments.

6. **[#1077] [feature] Add OpenRouter/model fallback support**  
   *Status: OPEN | Updated: 2026-06-27 | 👍: 6*  
   **Why it matters:** Users want provider-agnostic fallback chains. Highly voted, indicates reliance on multiple AI backends.

7. **[#1088] [bug] --file flag ignores .gitignore patterns**  
   *Status: OPEN | Updated: 2026-06-26 | 👍: 2*  
   **Why it matters:** Security/privacy risk — sensitive files (`.env`, `secrets`) can be accidentally passed to the model.

8. **[#1101] [bug] OOM crash when processing 5000+ token context window**  
   *Status: OPEN | Updated: 2026-06-25 | 👍: 1*  
   **Why it matters:** Memory leak suspected during long sessions. Affects users running complex system prompt + code analysis.

9. **[#1090] [feature] Export conversation history to Markdown**  
   *Status: OPEN | Updated: 2026-06-24 | 👍: 4*  
   **Why it matters:** Missing basic feature for documentation and sharing sessions. Competitors have this.

10. **[#1082] [bug] multi-line paste broken in tmux on macOS**  
    *Status: OPEN | Updated: 2026-06-23 | 👍: 1*  
    **Why it matters:** Tmux power users report pasting multiple lines inserts extra newlines. Frustrates REPL-based workflows.

---

## Key PR Progress

1. **[#2481] fix(shell): read clipboard media on BracketedPaste for Windows terminals**  
   *Status: OPEN | Updated: 2026-07-02*  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2481)  
   **Description:** Enables pasting images and binary content on Windows Terminal and VS Code integrated terminal. Previously Ctrl+V was captured by the terminal as a BracketedPaste event which dropped binary data. Author needed contribution.

2. **[#2475] feat: add --json flag to `kimi chat` for structured output**  
   *Status: OPEN | Updated: 2026-07-01*  
   **Description:** New flag allows programmatic consumption of chat responses as JSON. Key for scripting and piping into other tools.

3. **[#2472] fix: race condition on concurrent file processing**  
   *Status: OPEN | Updated: 2026-07-01*  
   **Description:** Addresses crashes when multiple `--file` arguments are used in parallel mode. Community reported data corruption.

4. **[#2469] feat: add .env file auto-detection for API keys**  
   *Status: OPEN | Updated: 2026-06-30*  
   **Description:** Automatically reads `.env` from current directory. Reduces manual config.toml setup friction.

5. **[#2465] chore: upgrade go-openai to v2.0.0**  
   *Status: OPEN | Updated: 2026-06-29*  
   **Description:** SDK upgrade brings streaming parsing improvements and error handling fixes. Pending review.

6. **[#2460] fix: correct token counting for Chinese characters**  
   *Status: OPEN | Updated: 2026-06-28*  
   **Description:** Token estimation was off by ~2x for CJK text. Caused truncated responses for Asian language users.

7. **[#2455] feat: allow custom timeouts per provider**  
   *Status: OPEN | Updated: 2026-06-27*  
   **Description:** Adds `timeout_seconds` to provider config. Response to users hitting rate limits on slow endpoints.

8. **[#2450] refactor: migrate config parser to TOML v2 spec**  
   *Status: MERGED | Updated: 2026-06-26*  
   **Description:** Now supports TOML 1.0 specifications. Backward compatible but stricter parsing.

9. **[#2446] test: add integration tests for tailscale proxy scenarios**  
   *Status: OPEN | Updated: 2026-06-25*  
   **Description:** Test suite for VPN/WireGuard connectivity. Response to #1111 and similar networking bugs.

10. **[#2441] docs: add troubleshooting guide for headless environments**  
    *Status: OPEN | Updated: 2026-06-24*  
    **Description:** User-contributed guide for SSH/tty-less deployments. Addresses #1103 complaints.

---

## Feature Request Trends

- **Provider-Agnostic Fallback Chains** (#1077, #1070, #1062): Users want Kimi CLI to automatically switch between OpenAI, Anthropic, and local models when one fails or reaches limits. This is the most-voted direction.
- **Headless/Server-Friendly Mode** (#1103, #1080, #1097): Requests for password-less key storage (file-based), no-GUI installation, and TTY-independent operation. Growing DevOps audience.
- **Structured Output for Automation** (#1090, #1072, #2475): Demand for JSON/Markdown export, `--json` flag on all commands, and webhook-out integration. Shift toward CI/CD usage.
- **Configuration UX Improvements** (#1079, #1095): Users want per-project config, environment variable overrides, and simplified `init` wizards. Reducing onboarding friction.

---

## Developer Pain Points

1. **Persistent Infinite Loop Bug (#640)** – Unresolved for 6 months with custom endpoints. Three separate users report different models triggering it. No workaround exists.
2. **Memory Management Failures** – Two open bugs (#1056, #1101) related to OOM crashes. Files >100KB or context windows >5000 tokens cause hard crashes. Affects real datasets.
3. **CI/CD & Remote Work Gaps** – Headless key storage (#1103), missing non-TTY streaming (#1095), and `.gitignore` bypass (#1088) make the tool unsuitable for server/automation use cases.
4. **Terminal Compatibility Issues** – Tmux paste bugs (#1082), Windows clipboard limitations (#2481 old behavior), and Tailscale/WireGuard failures (#1111) degrade experience across platforms.
5. **Chinese Language Token Counting (#2460)** – Token estimation breaking CJK response quality points to broader multilingual support gaps.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-03

## Today's Highlights
The community is experiencing significant turbulence on Windows with OpenCode v1.17.13, where new Go subscription users report complete hangs after "build" commands. On the V2 front, several contributor PRs landed focusing on session log replay determinism and system context structuring, while the desktop team shipped a suite of UI improvements including tab management and model picker search fixes. Two critical xAI provider bugs were closed today addressing missing prompt cache routing and unsupported model routing.

## Releases
No new releases in the last 24 hours. Latest stable is v1.17.13 (as of the previous digest cycle).

## Hot Issues

1. [#28846 — Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction](https://github.com/anomalyco/opencode/issues/28846) *(CLOSED)*  
   **90 comments | 82 👍**  
   The top-voted issue this cycle. Community strongly pushed for OpenCode Go subscription limits to reflect DeepSeek's permanent 75% price cut. Already closed, suggesting the team acted quickly.

2. [#8003 — VS Code Integration for Diff Preview](https://github.com/anomalyco/opencode/issues/8003)  
   **16 comments | 73 👍**  
   Persistent high-demand feature request. Working with large file diffs in the TUI is painful; users want to offload review to VS Code's native diff viewer. No movement yet.

3. [#10272 — Hidden calls Haiku](https://github.com/anomalyco/opencode/issues/10272) *(CLOSED)*  
   **9 comments**  
   Serious trust issue: users configuring MiniMax M2.1 via OpenRouter were silently billed for Claude Haiku 4.5. Closed, but this erodes confidence in provider routing.

4. [#12219 — OpenRouter credit limit blocking Kimi 2.5 Free](https://github.com/anomalyco/opencode/issues/12219)  
   **8 comments**  
   Free tier model unusable due to max_tokens misconfiguration or credit system bug. User frustration at being told they "can only afford 0" tokens.

5. [#31041 — Zen API 404 on CORS preflight](https://github.com/anomalyco/opencode/issues/31041)  
   **8 comments**  
   Blocks all browser-based clients from using Zen API endpoints. Only `POST` works; `OPTIONS` returns 404 HTML. Critical for web integration.

6. [#29869 — Desktop merges same-repo directories](https://github.com/anomalyco/opencode/issues/29869)  
   **6 comments**  
   Two separate directory clones of the same repo are merged into one project, with one treated as a sandbox. Unacceptable for multi-worktree workflows.

7. [#31972 — New Layout breaks Plan/Build switch](https://github.com/anomalyco/opencode/issues/31972)  
   **6 comments | 7 👍**  
   Feature flag gating New Layout renders Plan/Build mode toggling non-functional on Windows. UI toggle and `Ctrl+.` shortcut both dead.

8. [#35032 — Startup screen shows JSON](https://github.com/anomalyco/opencode/issues/35032)  
   **3 comments**  
   Running `opencode` from cmd on Windows dumps raw JSON instead of the normal startup screen. New user experience broken.

9. [#35035 — OpenCode Go hangs forever after "build" on Windows](https://github.com/anomalyco/opencode/issues/35035)  
   **3 comments**  
   Fresh Go subscribers on v1.17.13 see indefinite hangs with all models (glm-5.2, qwen3.6-plus, deepseek-v4-flash). Paying customers blocked.

10. [#35044 — Read Tool slow on massive files (6M+ lines)](https://github.com/anomalyco/opencode/issues/35044)  
    **2 comments**  
    Agents reading large files face severe slowness. No optimization for partial reads or caching in the Read tool.

## Key PR Progress

1. [#35047 — refactor(core): simplify v2 prompt lifecycle](https://github.com/anomalyco/opencode/pull/35047) *(CLOSED, contributor)*  
   Cleanup of V2 prompt lifecycle with two behavioral fixes: tool output failures are no longer silently absorbed, and V1 compatibility is maintained by disabling V2 drain logic for non-V2 sessions.

2. [#35040 — feat(core): deterministic session log replay](https://github.com/anomalyco/opencode/pull/35040) *(CLOSED, contributor)*  
   Replaces `log.caught_up` with a fixed watermark-based `log.synced` marker, making reconnect-safe log replay deterministic while preserving live tail delivery.

3. [#35046 — refactor(core): replace context epoch with checkpoint](https://github.com/anomalyco/opencode/pull/35046) *(OPEN, contributor)*  
   Replaces session context epoch persistence with a single-entry context checkpoint. Simplifies system context into a belief model with delta-based guidance updates.

4. [#35045 — feat(core): structure system context updates](https://github.com/anomalyco/opencode/pull/35045) *(CLOSED, contributor)*  
   SystemContext reconciliation now reports per-source update metadata alongside the merged model-visible text, plus item-level changes for list-shaped guidance.

5. [#35043 — fix(core): remove MCP tool call timeout](https://github.com/anomalyco/opencode/pull/35043) *(CLOSED)*  
   MCP request timeout is now scoped only to catalog/list requests, not to prompt retrieval and tool execution. Prevents false failures on long-running tools.

6. [#35042 — feat(app): navigate tabs on mousedown](https://github.com/anomalyco/opencode/pull/35042) *(OPEN)*  
   Tab switching in the new layout now triggers on `mousedown` instead of `mouseup`, eliminating the 40-100ms latency per tab switch.

7. [#35041 — fix(session): notify parent when subagents finish](https://github.com/anomalyco/opencode/pull/35041) *(OPEN, bot)*  
   Emits a synthetic task result into the parent session when any child session finishes, removing the old tool-specific background result injection.

8. [#35030 — fix(opencode): send xAI prompt cache routing key](https://github.com/anomalyco/opencode/pull/35030) *(OPEN)*  
   Adds the `x-grok-conv-id` header to route xAI requests to the correct server for prompt cache hits. Closes #35033.

9. [#35031 — feat(core): route xai models through native responses runner](https://github.com/anomalyco/opencode/pull/35031) *(OPEN)*  
   Adds a `@ai-sdk/xai` branch to `SessionRunnerModel.fromCatalogModel`, fixing the `UnsupportedApiError` for xAI catalog models. Closes #35034.

10. [#35010 — feat(desktop): reopen closed tabs, cmd+w, background tab open](https://github.com/anomalyco/opencode/pull/35010) *(OPEN, beta)*  
    Browser-style tab management: `⇧⌘T` reopens closed tabs, `⌘W` closes current tab, `⌘+click` opens links in background tabs.

## Feature Request Trends

**Provider and Cost Optimization:** The #1 theme — users want usage limits to auto-adjust when provider prices drop (#28846), free-tier models to actually work without credit barriers (#12219), and transparent routing that doesn't silently switch to more expensive models (#10272).

**V2 Desktop Experience:** Multiple requests target the new layout and desktop app: folder picker improvements for large projects (#35039), recently closed projects list (covered by PR #34926), and fixing the broken Plan/Build toggle in the new layout (#31972).

**Search as First-Class Capability:** Issue #35038 explicitly calls for treating web search as a first-class integration in V2, with pluggable providers instead of one-off tools. This signals a desire for unified tool architecture.

## Developer Pain Points

**Windows Stability Crisis:** Multiple reports of fresh v1.17.13 installations hanging on "build" (#35035), showing JSON on startup (#35032), and renderer crashes in heavy sessions (#35026). New Go subscribers are essentially blocked on Windows.

**Provider Transparency:** Silent model switching (#10272), inaccurate free-tier credit calculations (#12219), and mistimed CORS preflight handling (#31041) erode trust in provider integrations. Developers want to know exactly what they're paying for.

**Large File / Large Session Degradation:** The Read tool is unusable on files with millions of lines (#35044), the desktop app crashes rendering large diff summaries (#33106), and AsyncQueue leaks memory when iteration is abandoned (#34984). Scalability issues are hitting production users.

**Network Resilience:** Session continuation after network interruption is unreliable (#35029), particularly with subagents. Developers need robust reconnection without manual "continue" prompts.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-03

## Today's Highlights
A major refactoring wave has concluded, with **42 closed issues** in the last 24 hours—many related to the "bigrefactor" that restructured OpenAI-completions delta handling and MiMo provider compatibility. A critical **null content bug** affecting reasoning models was finally patched, while the community rallied around new provider additions (DeepInfra, Claude Sonnet 5) and quality-of-life fixes for the TUI. The team merged **10 pull requests**, including a SQLite session storage experiment and an inline extension type system.

## Releases
No new releases in the last 24 hours. The latest stable version remains **v0.80.3**.

## Hot Issues

1. **#4505 — MiMo models 400 error on multi-turn tool use** (12 comments, 👍4)  
   *[CLOSED]* Cold-start sessions with MiMo models failed on second turn due to `reasoning_content` not being preserved. Community reported this broke tool-heavy workflows.  
   [GitHub](https://github.com/earendil-works/pi/issues/4505)

2. **#4228 — OpenAI-completions delta handling breaks tool calls** (19 comments)  
   *[CLOSED]* When a stream delta contained both content and tool calls, only one was processed—a silent data loss bug. Closed as part of bigrefactor.  
   [GitHub](https://github.com/earendil-works/pi/issues/4228)

3. **#6187 — Pi login hangs in WSL after Copilot device auth** (9 comments)  
   *[CLOSED]* Browser authorization completes but the WSL terminal never detects it. Affects the growing WSL developer base.  
   [GitHub](https://github.com/earendil-works/pi/issues/6187)

4. **#6234 — Escape key leaves Pi stuck in "Working" state** (6 comments)  
   *[CLOSED]* Pressing Escape during an active run fails to abort extensions that never settle, requiring a forced kill. UX regression.  
   [GitHub](https://github.com/earendil-works/pi/issues/6234)

5. **#6262 — DS4-server context overflow not auto-compacted** (3 comments)  
   *[CLOSED]* Local DeepSeek V4 users hit 400 errors when prompts exceed context window; auto-compaction does not trigger. Frustrating for long sessions.  
   [GitHub](https://github.com/earendil-works/pi/issues/6262)

6. **#6215 — `pi update` fails on v0.80.3 due to missing dependency** (5 comments)  
   *[CLOSED]* `@smithy/node-http-handler@^4.9.1` not found in registry. Blocked upgrades for users on older versions.  
   [GitHub](https://github.com/earendil-works/pi/issues/6215)

7. **#6204 — MiMo v2 Omni ghost model** (3 comments)  
   *[OPEN]* Model listed in catalog but not served by any endpoint; selecting it returns 400. Confusing UX for new users.  
   [GitHub](https://github.com/earendil-works/pi/issues/6204)

8. **#6231 — Auth blocking local models** (4 comments)  
   *[CLOSED]* Local DeepSeek via Dwarf Star requires OAuth login, which makes no sense for offline models. Community wants a skip-auth flag.  
   [GitHub](https://github.com/earendil-works/pi/issues/6231)

9. **#6199 — HOME/END keys not working in scrollback** (2 comments)  
   *[CLOSED]* Alt mode broke keyboard navigation; users cannot jump to beginning/end of long sessions.  
   [GitHub](https://github.com/earendil-works/pi/issues/6199)

10. **#6268 — Codex WebSocket terminates after 60 minutes** (1 comment)  
    *[CLOSED]* Long-running tasks fail silently when the WebSocket connection limit is reached. No auto-reconnect implemented.  
    [GitHub](https://github.com/earendil-works/pi/issues/6268)

## Key PR Progress

1. **#6267 — InlineExtension type for named inline factories**  
   *[OPEN]* Adds a union type so inline extension factories can be passed to `main()` with proper type safety. Closes #6260.  
   [GitHub](https://github.com/earendil-works/pi/pull/6267)

2. **#6266 — Anthropic: strict tool use for edit tool**  
   *[OPEN]* Claude's ~10% edit error rate is addressed by enforcing stricter tool-use schemas. Targets #5501/#5434.  
   [GitHub](https://github.com/earendil-works/pi/pull/6266)

3. **#6264 — Clamp OpenAI Responses output tokens**  
   *[CLOSED]* Fixes `max_output_tokens` falling below API minimum (16) during tight context windows. Prevents 400 errors.  
   [GitHub](https://github.com/earendil-works/pi/pull/6264)

4. **#6263 — DeepInfra provider (text + image)**  
   *[CLOSED]* New built-in provider supporting both chat and image generation via OpenAI-compatible API. Model catalog auto-generated.  
   [GitHub](https://github.com/earendil-works/pi/pull/6263)

5. **#6258 — Guard against null content in agent loop**  
   *[CLOSED]* Fixes `message.content is not iterable` for reasoning models that return null content. Affects compaction, transforms, and agent loop.  
   [GitHub](https://github.com/earendil-works/pi/pull/6258)

6. **#6227 — SQLite session storage**  
   *[OPEN]* Experimental feature: writes session transcripts to SQLite alongside JSONL, enabled via `PI_SQLITE_SESSION_STORAGE=1`. Uses `better-sqlite3`.  
   [GitHub](https://github.com/earendil-works/pi/pull/6227)

7. **#6244 — Sticky bottom for TUI (interactive input + footer)**  
   *[CLOSED]* Adds API to keep input widget and footer fixed while content scrolls above. Improves TUI usability.  
   [GitHub](https://github.com/earendil-works/pi/pull/6244)

8. **#6243 — Fix UUID collisions in session storage**  
   *[CLOSED]* Corrects UUID truncation and race conditions that caused corrupted session trees and duplicate entries. Critical data integrity fix.  
   [GitHub](https://github.com/earendil-works/pi/pull/6243)

9. **#6241 — Avoid offscreen redraws for stable-height updates**  
   *[OPEN]* Performance fix: skips full scrollback redraw when only visible lines changed. Reduces CPU usage in long sessions.  
   [GitHub](https://github.com/earendil-works/pi/pull/6241)

10. **#6252 — Fix find paths from Windows drive root**  
    *[CLOSED]* Corrects path formatting on Windows when searching from bare drive roots (e.g., `C:\`). Replaces manual prefix slicing with `path.relative`.  
    [GitHub](https://github.com/earendil-works/pi/pull/6252)

## Feature Request Trends

- **Settings-driven skill selection** (#5570, #6191, #6236): Multiple issues ask to configure `--no-skills` / `--skill` paths in `project.json` or via env vars. Community wants per-repo skill management.
- **Provider expansion** (#6256, #6257, #6263): Strong demand for new model support—Kimi K2.7, Claude Sonnet 5, and a full DeepInfra provider—indicating users want provider agnosticism.
- **Configurable tool limits** (#6254): Users want tunable truncation limits for tool output (bytes/lines) instead of hardcoded 50KB/2000 lines.
- **TUI ergonomics** (#6244, #6241, #6255): Sticky bottom, scroll optimization, and extended function key support show the TUI is becoming a primary interface for many.
- **Local model auth bypass** (#6231): Request to skip OAuth for local providers, reflecting growing on-premise deployment interest.

## Developer Pain Points

- **Null/iterable crashes** (#4909, #2785, #6259): The `message.content is not iterable` error has been a persistent pain across multiple versions, especially for reasoning models. Finally fixed in #6258, but the recurrence suggests testing gaps.
- **Context window edge cases** (#6206, #6262, #6265): Clamping logic for context windows creates cascading issues—`max_tokens` too low, overflow not detected, API minimums violated. Developers running long sessions hit these regularly.
- **Update/install failures** (#6215): Dependency resolution issues during `pi update` block users from getting bug fixes. The `@smithy/node-http-handler` miss highlights registry fragility.
- **Extension API stability** (#6101, #6234, #4981): Stale context after session replacement, unresponsive abort, and missing typed settings schemas suggest the extension API needs hardening for production use.
- **Platform-specific breakage** (#6187 WSL, #6250 Linux X11 clipboard, #6251 VS Code trailing spaces): Cross-platform regressions are frequent, especially in the TUI and clipboard integrations.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-03

## Today's Highlights
Two stable releases shipped within 24 hours: **v0.19.5** and a nightly follow-up (**v0.19.5-nightly**). The stable release hardens **daemon-managed channel workers**, while the nightly patch cuts a critical mobile jank in session switching. The community is heavily focused on three fronts: **vision bridge UI support** for the daemon, **Windows-encoding and scroll-lock bugs**, and a burst of **enterprise channel adapter PRs** (WeCom, QQ Bot). A UX regression where the follow-up filter incorrectly discards sentences with abbreviations saw an autofix land same-day.

---

## Releases

### v0.19.5 (stable)
**Changes:**
- `feat(cli)`: Harden daemon-managed channel worker ([#6098](https://github.com/QwenLM/qwen-code/pull/6098))
- `fix(web-shell)`: Defer session creation until first prompt ([by @ytahdn](https://github.com/QwenLM/qwen-code/pull/6199))

### v0.19.5-nightly.20260703.b16baf1ff
**Changes:**
- `fix(web-shell)`: Cut mobile session-switch jank — memoized timeline signature, replay-first dispatch ([#618](https://github.com/QwenLM/qwen-code/pull/618))

---

## Hot Issues (Top 10)

1. **[#6195](https://github.com/QwenLM/qwen-code/issues/6195) — Add daemon UI for selecting the vision bridge model** (P2, 5 comments)
   The CLI already supports `/model --vision`; the community wants a UI equivalent in the daemon so users can pick/validate a vision model without terminal commands. The issue is gathering +1s quickly.

2. **[#6077](https://github.com/QwenLM/qwen-code/issues/6077) — Follow-up filter mistakenly discards abbreviations as "multiple sentences"** (P3, 5 comments)
   A subtle UX bug: the follow-up suggestion filter sees "Weeds vs. Wildflowers audit." — treats the period as a sentence end — and drops a perfectly valid suggestion. Community called it "annoying but easy to fix." **Autofix closed within 24h** (see PR #6193).

3. **[#6144](https://github.com/QwenLM/qwen-code/issues/6144) — Incorrect context window calculation** (P2, 4 comments, 1 👍)
   User configured Qwen3-Coder with 64K ctx-size but Qwen-Code computed a mismatch. The model-switching subsystem may misread `ctx-size` from `models.ini`. High priority because it silently corrupts long conversations.

4. **[#5979](https://github.com/QwenLM/qwen-code/issues/5979) — `/auth` new sessions still return 401** (P2, 4 comments)
   Changing model-provider config with `/auth` works in the current session but breaks all new sessions. A session-management state-propagation bug. Waiting for triage.

5. **[#6175](https://github.com/QwenLM/qwen-code/issues/6175) — "Thought for 0s" + non-streaming thinking output** (P2, 3 comments)
   OpenAI-compatible models returning `reasoning_content` show a broken timer and stalled streaming. The thinking-display subsystem appears to have a race condition with reasoning-budget parsing.

6. **[#6112](https://github.com/QwenLM/qwen-code/issues/6112) — `/schedule` local daemon for cron tasks without an open session** (P2, 3 comments)
   The "local always-on scheduler" — analog to Claude Code's desktop scheduled tasks — is a highly demanded feature for background automation.

7. **[#6218](https://github.com/QwenLM/qwen-code/issues/6218) — Taobao mirror behind by three versions** (P2, 2 comments)
   Chinese users blocked from upgrades. Mirror sync issue flagged as high-priority for the China region. The team is expected to update the CDN configuration.

8. **[#6214](https://github.com/QwenLM/qwen-code/issues/6214) — Garbled text on Windows with non-UTF-8 code pages** (P2, 2 comments)
   `run_shell_command` on `cmd.exe` outputs mojibake when the system code page is CP1251/CP936/CP932. A clear gap in the Windows port — welcome PR open.

9. **[#6181](https://github.com/QwenLM/qwen-code/issues/6181) — Mobile session switching is janky** (P1, 2 comments)
   Four compounding issues (polling, uncompressed full-history load, per-frame cost, CSS animation race) cause seconds-long freezes on mobile. The nightly patch (#618) targets layers 1–3 but the sidebar polling remains. Already the most-voted bug in the 24h window.

10. **[#6112](https://github.com/QwenLM/qwen-code/issues/6112) (duplicate of #5976) — Daemon channel workers via `qwen serve --channel`**  
   Both issues converge on the same request: daemon-managed channel workers with lifecycle supervision. The v1 design is outlined in #5976 and is now the reference for the channel worker roadmap.

---

## Key PR Progress (Top 10)

1. **[#6107](https://github.com/QwenLM/qwen-code/pull/6107) — Raise stream idle timeout default to 4 minutes + env knob**  
   Increases `DEFAULT_STREAM_IDLE_TIMEOUT_MS` from 2 to 4 minutes and hints the `STREAM_IDLE_TIMEOUT_MS` env var in the error message. Reduces false positives for slow completions.

2. **[#6189](https://github.com/QwenLM/qwen-code/pull/6189) — Allow sub-agents to spawn nested sub-agents**  
   Adds `model.maxSubagentDepth` (default `5`). Sub-agents can now delegate further — previously they could not. Unlocks deeper autonomous workflows.

3. **[#6200](https://github.com/QwenLM/qwen-code/pull/6200) — QQ Bot security hardening**  
   PR-A of 4-PR split: gateway URL validation (`wss://`), atomic state transitions, sanitized logging. Addresses SSRF and secret-leak vectors.

4. **[#6206](https://github.com/QwenLM/qwen-code/pull/6206) — QQ Bot group message handling + cron-msg-experimental**  
   Adds keyword triggers, @-mention detection, and experimental cron messaging for the QQ Bot channel. PR-D of the same split.

5. **[#6154](https://github.com/QwenLM/qwen-code/pull/6154) — `read_file` respects `.gitignore`**  
   Aligns `read_file` with `list_directory` so both honor `.gitignore` rules. Previously `read_file` ignored `.gitignore` entirely, causing permission inconsistency.

6. **[#6193](https://github.com/QwenLM/qwen-code/pull/6193) — Skip abbreviations in multiple_sentences filter**  
   Autofix for #6077: the follow-up suggestion filter now skips common abbreviations (`vs.`, `Dr.`, `e.g.`, `etc.`). Landed same-day as the bug report.

7. **[#6216](https://github.com/QwenLM/qwen-code/pull/6216) — Add UTF-8 prefix for `cmd.exe` on Windows**  
   Fix for #6214: prepends `chcp 65001 >NUL &&` to shell commands when the detected shell is `cmd.exe`. Non-UTF-8 code pages now produce correct text.

8. **[#6096](https://github.com/QwenLM/qwen-code/pull/6096) — Add `zvec-grep` bundled skill**  
   Guides Qwen Code to use the `zg` CLI for semantic workspace search. Targets open-ended code and documentation investigation when symbols or file names are unknown.

9. **[#6128](https://github.com/QwenLM/qwen-code/pull/6128) — Web-shell list-dialog keyboard navigation & a11y overhaul**  
   Complete rewrite of keyboard nav, ARIA roles, and IME-safe search for model, theme, approval, resume, tools, delete, release, and rewind dialogs. Closed as merged.

10. **[#6198](https://github.com/QwenLM/qwen-code/pull/6198) — Add `dataviz` bundled skill**  
    Ships chart/dashboard design guidance with palette references, anti-patterns, and a local palette validator script. The first "design brain" for the Artifact tool.

---

## Feature Request Trends

**1. Daemon-managed background services** (highest frequency)
- Channel workers (`qwen serve --channel`) — #5976
- Local cron scheduler (`/schedule`) — #6112
- Recurring job expiration configuration — #6167
- **Why it matters**: the community wants Qwen Code to run continuous, unattended tasks without an open terminal session — essentially turning the CLI into a persistent agent platform.

**2. Enterprise messaging adapters**
- WeCom/Enterprise WeChat — #6208 (PR #6210 already open)
- QQ Bot group message handling — #6206 (4+ PRs in flight)
- DingTalk proactive send — #6168

**3. Vision and reasoning UI improvements**
- Daemon UI for vision bridge model selection — #6195
- Fix "Thought for 0s" bug — #6175
- All point to growing adoption of multimodal and reasoning models.

**4. Sub-agent depth and delegation**
- Nested sub-agents up to configurable depth — PR #6189
- Enables deeper autonomous agent chains for complex multi-step workflows.

**5. Configurable cron/loop job expiration** — #6167
Users need to adjust the hardcoded 7-day TTL for recurring jobs (cron, loops) — a sign that long-running automation is becoming mainstream.

---

## Developer Pain Points

**1. Windows compatibility (high-frequency, high-frustration)**
   - Garbled output on non-UTF-8 code pages (CP1251, CP936, CP932) — #6214
   - Sandbox `.sb` files missing from macOS lib bundle — #6089
   - **Impact**: Blocks adoption on Windows and silences non-English users.

**2. Mobile/web-shell performance**  
   - Session switching jank — #6181 (P1, 2 comments)
   - Polling not gated by sidebar visibility
   - Full-history load on every switch
   - The nightly patch (#618) is a band-aid; the root cause (sidebar polling) remains.

**3. Configuration state not propagating to new sessions**  
   - `/auth` change not reflected in new sessions — #5979
   - `/model --vision` not persisted for daemon UI — #6195
   - **Pattern**: state updates write to the wrong scope, new sessions start with stale values.

**4. Incorrect context window calculations**  
   - #6144 — mismatched `ctx-size` values between config and model-switching
   - Silent data loss in long conversations.

**5. Release packaging friction**  
   - Taobao mirror outdated by 3 versions — #6218
   - Homebrew tap lags behind — #6187
   - VSCode companion release blocked by `vsce` flagging Slack token regex as secret — #6199
   - npm package flagged by security scanners due to bundled IOCs — #6163

**6. MCP invocation blocked in YOLO mode**  
   - #6131 — MCP tools require manual confirmation, making YOLO mode unusable with MCP autostart.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-03

## Today's Highlights
The v0.8.67 release cycle is in full swing, with major focus on **setup UX**, **Fleet/sub-agent reliability**, and **project-scope instruction handling**. A critical memory exhaustion fix for Fleet sub-agents was merged as a release blocker, and a highly requested rules-directory auto-discovery feature landed in `main`. Multiple concurrency and persist-state bugs in the sub-agent system were also addressed in a rapid sequence of fixes.

## Releases
No new releases in the last 24 hours. The project is in active development toward v0.8.67.

## Hot Issues

1. **#3793 — Guided localized constitution creator** (14 comments)  
   *Why it matters:* Proposes replacing the blank prompt editor with a language-first, guided setup flow. Author emphasizes that constitution files must *not* be allowed to flip runtime security settings. High community interest in first-run UX.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/3793)

2. **#1812 — TUI freezes on Windows (crossterm poll)** (10 comments)  
   *Why it matters:* Two confirmed freezes on Windows 11 with logs and thread-state analysis. The TUI becomes unresponsive but the process stays alive. One of the longest-running Windows stability issues.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/1812)

3. **#3867 — Project-scope instructions overly denied** (7 comments) — **CLOSED**  
   *Why it matters:* Users working in multi-project setups could not use `instructions` config at project scope due to a hard block since v0.8.8. This issue drove the auto-discovery PR that was merged today.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/3867)

4. **#3792 — First-run onboarding feels like editing config, not starting the app** (7 comments)  
   *Why it matters:* Sets the UX direction: setup should feel like “starting CodeWhale” rather than configuring a file. Keeps constitution central but separates runtime security controls.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/3792)

5. **#1607 — Token cost estimation: add CNY and other currencies** (6 comments)  
   *Why it matters:* Non-US users requesting local currency support for token cost estimates. Community is small but consistent (6 comments over 7 weeks).  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/1607)

6. **#2261 — TUI crash leaks input to PowerShell terminal** (5 comments)  
   *Why it matters:* After a crash during conversation, keyboard input bypasses the TUI and executes as PowerShell commands. A security and UX concern for Windows users.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/2261)

7. **#1835 — IME composition event deadlock on Windows** (4 comments, 👍 1)  
   *Why it matters:* Chinese IME users (Sogou) report input field completely unresponsive. Reproduction with logs suggests a crossterm event deadlock. +1 indicates growing demand for CJK input support.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/1835)

8. **#2934 — Sidebar sessions panel with auto-resume** (4 comments)  
   *Why it matters:* Users want a persistent session browser instead of relying on `Ctrl+R` popup or CLI flags. Addresses a common friction point for multi-session workflows.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/2934)

9. **#3308–#3314 — TUI monolith refactoring split** (3 comments each, 4 related issues)  
   *Why it matters:* A systematic effort to break down `App` god object (150+ fields), `runtime_threads.rs` (2,400 lines), `history.rs`, and `mcp.rs`. Indicates maintainers are investing in code health.  
   [#3308](https://github.com/Hmbown/CodeWhale/issues/3308), [#3310](https://github.com/Hmbown/CodeWhale/issues/3310), [#3313](https://github.com/Hmbown/CodeWhale/issues/3313), [#3314](https://github.com/Hmbown/CodeWhale/issues/3314)

10. **#3932 — Fleet agent has no vocabulary to pick model classes** (2 comments)  
    *Why it matters:* Identifies a gap where the agent tool schema and constitution don’t support per-role model routing. Critical for the Fleet feature to become truly useful.  
    [GitHub](https://github.com/Hmbown/CodeWhale/issues/3932)

## Key PR Progress

1. **#3892 — Auto-discover `.codewhale/rules/` and `.claude/rules/` directories** — **MERGED**  
   *What:* Closes #3867 by scanning rules directories on session start. Supports glob patterns for file inclusion. Highly requested feature for multi-project workflows.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/3892)

2. **#3931 — Enforce absolute recursion-depth ceiling; widen task-id entropy** — **MERGED**  
   *What:* Two fleet correctness fixes: enforces recursion depth cap and increases task ID entropy to prevent collisions. Author confirmed the 100/200 agent admission cap was already working.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/3931)

3. **#3936 — Unique temp path per atomic state write** — **MERGED**  
   *What:* Fixes concurrent persist corruption in sub-agent state. Multiple OS threads writing `state.json` could overwrite each other. Now uses a temp file + atomic rename.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/3936)

4. **#3902 — Fix five render/input hot paths** — **OPEN**  
   *What:* Addresses five performance-labeled issues: double sidebar computation, `pasta` clipboard overhead, sync cursor rendering, extraneous terminal resize events, and `KeyChord` display allocation. Includes fixes for four regressions found by adversarial review.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/3902)

5. **#3895 — Report local worker RSS in fleet host status** — **CLOSED (red CI)**  
   *What:* Adds per-worker memory sampling (`ps -o rss=`) to Fleet local worker status. Was salvaged as #3901 to land with green CI. Critical for the 15GB memory exhaustion investigation.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/3895)

6. **#3901 — Salvaged local worker memory reporting** — **MERGED**  
   *What:* Re-landing of #3895 with CI fixes. Now Fleet can surface per-worker RSS, enabling telemetry for the memory exhaustion bug (issue #3885). Returns `None` on non-Unix.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/3901)

7. **#3643 — Setup summary wizard step for MCP/skills/plugins** — **MERGED**  
   *What:* First implementation of the v0.8.67 setup wizard. Displays a scrollable TUI modal with MCP server status, skills directory info, and plugin state. Part of the guided onboarding effort.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/3643)

8. **#3873 — Remove unused execpolicy amend module** — **MERGED**  
   *What:* Cleanup PR removing dead TUI code and a direct `fd-lock` dependency. Part of the ongoing refactoring effort.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/3873)

9. **#3784 — Config persistence for GUI config panel** — **MERGED**  
   *What:* Adds support for persisting nested-table config keys and fixes `allow_shell` type bug. Enables the GUI config panel to save all configuration items correctly.  
   [GitHub](https://github.com/Hmbown/CodeWhale/pull/3784)

10. **#3865 — Persist sub-agent state to `.codewhale/` instead of `.deepseek/`** — **MERGED**  
    *What:* Fixes a rebrand-era fallback where `default_state_path` returned legacy `.deepseek/` paths on first run. Now consistently uses `.codewhale/`.  
    [GitHub](https://github.com/Hmbown/CodeWhale/pull/3865)

## Feature Request Trends
- **Guided setup & onboarding:** Multiple issues (#3793, #3792, #3643) push for a wizard-like first-run experience replacing the blank config editor. Language-first selection is a recurring theme.
- **Session management:** Persistent sidebar session panel (#2934) and session history browsing are increasingly requested as users scale their workflows.
- **Fleet/agent model routing:** #3932 highlights that the agent system needs schema-level support for choosing different models per task class—critical for real-world Fleet adoption.
- **Multi-project instruction support:** #3867 (now resolved) and rules auto-discovery (#3892) show strong demand for per-project configuration without global policy friction.
- **Currency localization for cost estimation:** #1607 reflects growing international user base; requests for CNY and other local currency displays in token cost tracking.

## Developer Pain Points
- **Windows stability:** Three distinct bugs persist—TUI freezes (#1812), input leaks to PowerShell (#2261), and IME deadlock (#1835). Windows remains the platform with the most unresolved reliability issues.
- **Memory exhaustion in Fleet sub-agents:** A user reported 15GB memory consumption. While the admission cap was confirmed working, PRs #3931, #3936, and #3901 indicate the team is actively hunting concurrent-persist and unbounded output issues.
- **CJK text handling:** Chinese characters appear garbled in agent output (#1675), and IME input is broken (#1835). These affect a significant portion of the user base.
- **Codebase maintainability:** The systematic refactoring of the TUI monolith (#3308–#3314) indicates the codebase has grown beyond clean boundaries. 150-field `App` struct and 2,400-line `RuntimeThreadManager` are signs of technical debt the team is actively addressing.
- **Copy/paste quality:** Terminal-native copy includes visual line breaks (#1853), making text extraction from the TUI unnecessarily messy.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*