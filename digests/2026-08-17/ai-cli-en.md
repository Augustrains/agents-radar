# AI CLI Tools Community Digest 2026-08-17

> Generated: 2026-08-17 00:29 UTC | Tools covered: 9

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

# AI CLI Tools Cross-Platform Comparison Report
**Date: 2026-08-17**

---

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem is in a phase of rapid maturation characterized by a shared struggle: session state integrity and process lifecycle reliability are emerging as the dominant cross-tool concern. Across all major tools (Claude Code, Codex, Gemini CLI, Copilot CLI, Kimi, OpenCode, Pi, Qwen, CodeWhale/DeepSeek-TUI), communities are reporting similar pain points — silent failures, session corruption, stuck UI states, and opaque resource management. Simultaneously, the tools are differentiating on the basis of workflow sophistication; some are pushing into multi-agent orchestration (Qwen Code, Gemini CLI), while others focus on interactive TUI polish (Pi, OpenCode). The rapid pace of PR activity across repos (18 PRs merged in Codex alone in 24 hours) signals healthy, continuous iteration, but the recurring nature of session-loss and auth bugs indicates that fundamental state management architectural challenges remain unresolved across the board.

---

## 2. Activity Comparison

| **Tool** | **Active Issues (24h)** | **PR Activity (24h)** | **Release Status** | **Community Engagement** |
|---|---|---|---|---|
| **Claude Code** | ~10 hot issues (51-comment max) | 3 PRs active | No release in 24h | High (top issue 51 comments, 30👍) |
| **Codex (OpenAI)** | ~10 hot issues (106-comment max) | **18 PRs merged** | No release in 24h | **Very High** (106 comments on #20214) |
| **Gemini CLI** | ~10 hot issues | **10+ PRs active/merged** | Nightly v0.56.0 | High (P1 labels, fast PR turnaround) |
| **Copilot CLI** | 16 issues updated | 1 PR (likely spam) | Stable v1.0.80 | Medium (maintainer velocity high on critical bugs) |
| **Kimi Code** | ~10 issues | **10 PRs open** | No release in 24h | Medium (long-standing requests) |
| **OpenCode** | ~10 issues | **10+ PRs merged/active** | No release in 24h | Medium-High (49👍 on top UX issue) |
| **Pi** | ~10 issues | **9 PRs merged** | v0.84.2 | Medium (active maintainers, many fixes landed) |
| **Qwen Code** | 10 issues (multi-agent cluster) | **10+ PRs active** | 2 preview releases | High (rapid bug-to-fix turnaround) |
| **CodeWhale (DeepSeek-TUI)** | 10 issues + 42 open/updated | **10+ PRs active** | **v0.9.8 released** | Medium (rebranding moment, high maintainer activity) |

---

## 3. Shared Feature Directions

| **Feature Direction** | **Tools Involved** | **Specific Needs** |
|---|---|---|
| **Session lifecycle & recovery** | Claude Code (#26452, #86369), Codex (#38856, #25319), Copilot CLI (#4505, #4474), Kimi (#1783), OpenCode (#42863), Pi (#8061) | Reliable persistence, explicit recovery/restore paths, `/delete` and `/rename` commands, session favorites, no silent archival |
| **Multi-agent orchestration reliability** | Claude Code (#86650, #86426, #86198), Gemini CLI (#22323, #21409), Qwen Code (#9276, #9282, #9283), CodeWhale (#5123) | Deterministic task delivery, truthful completion reporting, error containment (no session-wide crashes), preserving original interruption reasons |
| **Context/memory management** | Claude Code (docs gaps), Kimi (#1478, PR #2445), Pi (#8061, #8218), Gemini CLI (AST-aware tooling EPICs) | Structured memory layers, `/compact` commands, correct token accounting (cache vs. billable), output-token reservation in context budgets |
| **OAuth/auth transparency & reliability** | Copilot CLI (#4490, #4463, #4472), Kimi (#2612, PR #2210), Qwen (#9275), Pi (#8217) | Robust refresh flows, device-code login for headless, clear error messages for expired tokens, no race conditions on concurrent refresh |
| **Windows & cross-platform parity** | Codex (#20214, #38546, #28248), Copilot CLI (#4463, #4488), Kimi (#2600), Pi (#6300), CodeWhale (#5403) | Fix Windows desktop app perf, socket/file-lock issues, PowerShell path resolution, non-UTF-8 handling, wide-terminal rendering |
| **Billing/usage transparency** | Claude Code (#28817, rate-limit confusion), Codex (#18018, #38900), OpenCode (#33318), Pi (cache token billing fix) | Clear per-plan feature gating, real-time token counters, accurate quota reporting, no surprise "limit exhausted" states |

---

## 4. Differentiation Analysis

| **Tool** | **Primary Focus** | **Distinctive Technical Approach** | **Target User** |
|---|---|---|---|
| **Claude Code** | Real-world reliability | Deep integration with Anthropic models; skills & agents as first-class constructs; high focus on SDK for embedded agent workflows | Professional developers & teams on enterprise-grade work |
| **Codex** | Production-scale assistant | Aggressive TUI improvements (Vim, `/cd`); strong enterprise permission profiles; cutting-edge security audits (CodeQL, sandbox isolation) | Developers inside larger orgs needing compliance & security controls |
| **Gemini CLI** | Multi-agent orchestration | Subagents with defined roles; ACP (Agent Client Protocol) for interop; explicit **P1/P2 issue triage discipline** | Developers who delegate complex multi-step tasks to specialized agents |
| **Copilot CLI** | GitHub-native ecosystem | Tight coupling with GitHub SDK/plugins; MCP server growth; strong focus on session resume & auth flows | Devs embedded in the GitHub workflow, Slack integration users |
| **Kimi Code** | Simplicity & accessibility | Slim CLI with pragmatic tooling; `/compact` for context; emphasis on lightweight config (`.kimi_config`) | Solo developers & small teams, especially in Asia |
| **OpenCode** | Modern UX | Desktop app + TUI; excellent keyboard-driven experience; heavy focus on terminal-native integration; "universal copy" UX debates | Terminal power-users who want a polished, modern interface |
| **Pi** | Multi-provider extensibility | Provider catalog as a core primitive (with remote overlay); **extension API** (custom messages, triggers); strong on **token accounting correctness** | Developers running heterogenous model backends (glm, kimi, moonshot, xAI) |
| **Qwen Code** | Review & team workflows | `/review` subsystem as product-grade tool (worktree locking, `capture-tui` visual evidence); aggressive team-mode debugging | Enterprises relying on automated review pipelines & team-based agent coding |
| **CodeWhale** | Sandbox & multi-model support | Heavy `bwrap` sandboxing; `HarnessPosture` for model-specific prompts; Claude Code parity planning | Linux-first, self-hosted, security-conscious users; DeepSeek/MiMo model fans |

---

## 5. Community Momentum & Maturity

- **Highest community engagement:** **Codex** has the most active issue thread (106 comments on Windows perf) and the most rapid PR velocity (18 merged in 24h). This is a large, vocal user base pushing hard on UX polish.

- **Strongest maintainer velocity:** **Qwen Code** is turning around community-reported multi-agent bugs to merged fixes within days (#9276 → #9288, #9282 → #9284, #9290 → #9292). The pattern is professional and healthily responsive — a strong signal of sustained product investment.

- **Most visible structural shift:** **CodeWhale (DeepSeek-TUI)** is rebranding while simultaneously shipping a sandbox overhaul and i18n expansion. The "Claude Code parity" design doc indicates ambition to join the top-tier tools — but it still lags in community size.

- **Most mature & stable footprint:** **Claude Code** shows the classic "successful product" pattern: features ship, users hit edges, and the community's largest demands are for reliability (session loss, permission semantics). PR velocity is lower, suggesting consolidation rather than expansion.

- **Rapidly iterating on infrastructure:** **Gemini CLI** is running a disciplined P1/P2 tracking system with paired PR fixes, indicating healthy engineering management. The SSR "Agent" PR series shows organized initiative-based work.

- **Specialized differentiation:** **Pi** is building the strongest multi-provider runtime engine, evidenced by its catalog governance, provider-specific fixes (Kimi cache tokens, xAI responses), and extension API depth. Its community is small but technically sophisticated.

---

## 6. Trend Signals

1. **Session state is becoming a first-class "work artifact."** Developers treat their CLI sessions as durable products (like code), not ephemeral interactions. Expect management GUIs for sessions within the next 6 months across all major tools.

2. **Multi-agent orchestration has hit a reality-check.** The "agent team" concept is maturing from demo to production, and the growing pains are clear: dropping notifications, silent failures, misleading success reporting. Tools that master *deterministic* multi-agent semantics will win teams skeptical of AI reliability.

3. **Windows support is the new competitive battleground.** Multiple tools are bleeding users to Windows-specific bugs (performance, sandbox, file locking). Tools that prioritize Windows parity will capture the enterprise heavy-lifting market.

4. **Token accounting precision is an emerging trust factor.** Cache billing inflation (Pi), input-token misuse (Kimi), and output-reservation failures are eroding confidence in long-context workflows. Expect more transparent token & cost dashboards as features.

5. **The "plugin/skill ecosystem" is at an inflection point.** Copilot's plugin-dep request, Claude's skill reliability complaints, and OpenCode's permission ergonomics tell the same story: as plugins multiply, lifecycle management (dependency resolution, capability metadata, UI management) becomes a top-3 user demand.

6. **Models are forcing tool capability introspection.** Bugs like Copilot's `claude-haiku-4.5` reasoning-effort mismatch and OpenCode's Qwen multi-system-message rejection signal a need for *capability discovery* as a core platform feature, not an add-on.

7. **Security posture is becoming a differentiator.** Codex's permission-profile hardening, Qwen's ephemeral-container verification, CodeWhale's bwrap sandboxing, and Claude's glob-pattern fix reveal a race to "safe by default" as AI agents execute ever-more privileged actions.

---

*This report was generated from community digest summaries for each tool on 2026-08-17 and reflects the state of ~150 tracked issues and ~100 PRs across 9 distinct projects.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

**Data Source:** github.com/anthropics/skills | **Date:** 2026-08-17

---

## 1. Top Skills Ranking

The following Pull Requests represent the most actively discussed Skill submissions in the repository. Each is currently **open** (unmerged) pending review.

### 1.1 skill-creator — Eval Pipeline Fixes (#1298)
**Author:** MartinCajiao | **Opened:** 2026-06-10 | **Status:** Open
**Link:** [PR #1298](https://github.com/anthropics/skills/pull/1298)

**Functionality:** Fixes `run_eval.py` (the evaluation script inside the `skill-creator` skill) which consistently reported `recall=0%` for every skill description, making the optimization loop unusable. Addresses a Windows stream-reading bug, trigger detection logic, and parallel worker consistency.

**Discussion Highlights:** This PR links to Issue #556 (12 comments, 7 👍) — the highest-signal bug report in the repo. Multiple independent users reproduced the 0% recall issue, indicating a systemic problem in how `claude -p` mode resolves skills from the command file. The discussion centers on the underlying architecture: `run_eval.py` writes skill descriptions into `.claude/commands/` and expects Claude to invoke the `Skill`/`Read` tool in headless mode — which demonstrably does not trigger.

### 1.2 document-typography (#514)
**Author:** PGTBoos | **Opened:** 2026-03-04 | **Status:** Open
**Link:** [PR #514](https://github.com/anthropics/skills/pull/514)

**Functionality:** Typographic quality control for AI-generated documents — prevents orphan word wrap, widow paragraph headers, and numbering misalignment in output.

**Discussion Highlights:** Addresses a universal pain point: every document Claude generates exhibits these typographic defects. Low controversy; the discussion is mostly about scope (whether to also cover European typographic conventions).

### 1.3 pdf — Case-Sensitive File References Fix (#538)
**Author:** Lubrsy706 | **Opened:** 2026-03-06 | **Status:** Open
**Link:** [PR #538](https://github.com/anthropics/skills/pull/538)

**Functionality:** Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` — `REFERENCE.md` → `reference.md` and `FORMS.md` → `forms.md`. The actual files are lowercase; the uppercase references break on case-sensitive file systems (Linux CI, macOS).

**Discussion Highlights:** Small, surgical fix. Discussions note the deeper issue: the SKILL.md authoring process has no validation step to catch these mismatches pre-merge — a gap that later PRs (#539, #1367) attempt to fill with pre-parse validation.

### 1.4 odt — OpenDocument Text Creation & Template Filling (#486)
**Author:** GitHubNewbie0 | **Opened:** 2026-03-01 | **Status:** Open
**Link:** [PR #486](https://github.com/anthropics/skills/pull/486)

**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on mentions of ODT, ODS, ODF, OpenDocument, or LibreOffice document requests.

**Discussion Highlights:** Fills a market gap — the official collection has had docx, pdf, and pptx skills for months, but ODT was missing. High community interest in open-source document format support; discussion focuses on the quality of ODT→HTML conversion fidelity.

### 1.5 frontend-design — Clarity & Actionability (#210)
**Author:** justinwetch | **Opened:** 2026-01-05 | **Status:** Open
**Link:** [PR #210](https://github.com/anthropics/skills/pull/210)

**Functionality:** Revises the bundled `frontend-design` skill to improve clarity, actionability, and internal coherence — ensuring every instruction is executable within a single conversation.

**Discussion Highlights:** The oldest active PR in the top ranks. The discussion centers on whether the revised skill crosses the line from "actionable" into "overly prescriptive" — how much latitude should skills give the model vs. how much should they dictate exact steps?

### 1.6 skill-quality-analyzer + skill-security-analyzer (#83)
**Author:** eovidiu | **Opened:** 2025-11-06 | **Status:** Open
**Link:** [PR #83](https://github.com/anthropics/skills/pull/83)

**Functionality:** Two meta-skills for the `example-skills` marketplace collection: (1) quality analysis across five dimensions (structure/documentation 20%, examples, resource usage); (2) security analysis of existing skills for prompt injection and unsafe file operations.

**Discussion Highlights:** Long-running PR (9+ months). Discussion touches on the security dimensions — ties directly to the trust boundary concern in Issue #492 (the most-commented issue at 43 comments). Community sees these meta-skills as a partial mitigation for the "untrusted community skills under anthropic namespace" problem.

### 1.7 docx — Tracked Change w:id Collision Fix (#541)
**Author:** Lubrsy706 | **Opened:** 2026-03-06 | **Status:** Open
**Link:** [PR #541](https://github.com/anthropics/skills/pull/541)

**Functionality:** Fixes document corruption when the DOCX skill adds tracked changes to documents that already contain bookmarks. In OOXML, `w:id` is a shared ID space across bookmarks, tracked changes, comments, and move ranges; the existing skill used hardcoded low IDs (1,2,3) which collide.

**Discussion Highlights:** Demonstrates the maturity of the document skills ecosystem — this is a subtle OOXML format detail, indicating users are pushing these skills to production-grade reliability.

---

## 2. Community Demand Trends

Distilled from the Issues tracker (top discussions by comment count):

### 2.1 Trust & Security Boundaries (Issue #492 — 43 comments, 2 👍)
**Link:** [Issue #492](https://github.com/anthropics/skills/issues/492)

Community skills are distributed under the `anthropic/` namespace, impersonating official Anthropic skills. Users may grant elevated permissions to community skills believing they are official. This is the single most-discussed issue in the repo.

**Underlying demand:** A trustworthy skill distribution mechanism — official vs. community separation, human-review gating, or a signing mechanism.

### 2.2 Organizational Skill Sharing (Issue #228 — 16 comments, 8 👍)
**Link:** [Issue #228](https://github.com/anthropics/skills/issues/228)

Skills must be shareable within an organization directly — a shared skill library or direct sharing link. Current workflow (download .skill, send via Slack, manual Settings > Capabilities > Upload) is untenable at scale.

**Underlying demand:** Enterprise deployment infrastructure — team-level skill registries, version pinning, and rollout controls.

### 2.3 Eval Infrastructure Reliability (Issue #556 — 12 comments, 7 👍)
**Link:** [Issue #556](https://github.com/anthropics/skills/issues/556)

`run_eval.py` never triggers skills/commands in `claude -p` — 0% trigger rate across all queries. 3 open PRs (#1298, #1099, #1050) attempt to fix this, none merged as of data date.

**Underlying demand:** A reliable skill-quality measurement loop. Without trigger evals working, the community cannot objectively measure whether description improvements work — crippling the iteration cycle for skill authors.

### 2.4 Duplicate Skills Across Plugins (Issue #189 — 6 comments, 9 👍)
**Link:** [Issue #189](https://github.com/anthropics/skills/issues/189)

Installing both `document-skills` and `example-skills` plugins installs identical skills, causing duplicates in Claude Code's context window. 9 upvotes — the highest-volted issue.

**Underlying demand:** Clean plugin namespace partitioning — no overlap between marketplace collections, with dedup on install.

### 2.5 Context Window Exhaustion (Issue #1487 — 4 comments)
**Link:** [Issue #1487](https://github.com/anthropics/skills/issues/1487)

The `claude-api` bundled skill eagerly injects ~156k tokens in a single tool call, exhausting the context window. Recent (2026-07-27) and actively being addressed.

**Underlying demand:** Lazy-loading or progressive disclosure — skills must not unconditionally inject large reference material.

---

## 3. High-Potential Pending Skills

These PRs have active discussions and are likely to land soon:

### 3.1 self-audit — Mechanical Verification + Reasoning Quality Gate (#1367)
**Author:** YuhaoLin2005 | **Opened:** 2026-06-28 | **Updated:** 2026-07-02
**Link:** [PR #1367](https://github.com/anthropics/skills/pull/1367)

Two-stage audit skill: (1) mechanical verification that every claimed output file exists; (2) four-dimension reasoning audit in damage-severity priority order. Universal across tech stacks. The author has a companion Issue (#1385) proposing a broader quality-gate pipeline, which has 4 comments — should keep momentum.

### 3.2 plan-file-hygiene (#1479)
**Author:** tonydzi | **Opened:** 2026-07-25 | **Updated:** 2026-07-27
**Link:** [PR #1479](https://github.com/anthropics/skills/pull/1479)

Addresses Issue #1417: planning artifacts (PLAN.md, task files) accumulate with no lifecycle management — no archival, no cleanup, no summarization. The skill defines a lifecycle: create → track → close → archive, with proactive cleanup recommendations.

### 3.3 ServiceNow Platform Skill (#568)
**Author:** Vanka07 | **Opened:** 2026-03-08 | **Updated:** 2026-08-12
**Link:** [PR #568](https://github.com/anthropics/skills/pull/568)

Broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM, FSM, HRSD, CSM, SPM/PPM, Vulnerability Response, and Security Incident Response. Enterprise platform skills are a clear market gap — this PR has been active for 5 months, indicating sustained maintainer interest.

### 3.4 testing-patterns (#723)
**Author:** 4444J99 | **Opened:** 2026-03-22 | **Updated:** 2026-04-21
**Link:** [PR #723](https://github.com/anthropics/skills/pull/723)

Comprehensive testing skill: Testing Trophy model, unit test patterns (AAA, naming, pure functions, edge cases), React component testing (Testing Library), and what NOT to test. Covers a core software engineering need that the official skill-set does not yet address.

### 3.5 pyxel — Retro Game Development (#525)
**Author:** kitao | **Opened:** 2026-03-05 | **Updated:** 2026-07-15
**Link:** [PR #525](https://github.com/anthropics/skills/pull/525)

Skill for the Pyxel retro game engine via the pyxel-mcp server. Covers a complete workflow: write → run_and_capture → inspect → iterate. Notable because the author also maintains pyxel-mcp — a first-party ecosystem skill, which increases merge probability.

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is a **reliable measurement and trust infrastructure for skills** — working trigger evals to objectively validate descriptions, namespace separation to distinguish official from community skills, and install deduplication — before the value of new domain skills (ODT, ServiceNow, testing-patterns) can be fully realized.

---

# Claude Code Community Digest — 2026-08-17

*Generated from GitHub activity on anthropics/claude-code*

---

## 1. Today's Highlights

The community's attention remains focused on **session persistence reliability** — a long-running bug (#26452, 51 comments) about sessions disappearing after logout/restart continues to generate the most discussion, alongside ongoing **rate-limit and quota confusion** affecting Pro, Max, and hobbyist users. A cluster of newly-reported **agent orchestration bugs** (slash commands corrupting sessions mid-flight, dropped task notifications in skills, abort-controller issues in the SDK) suggests the recent focus on background agents and skills is hitting real-world friction. Several **documentation gaps** around Bash permission semantics, hook output limits, and statusline behavior were closed, but highlight a recurring pattern of features shipping ahead of their docs.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Hot Issues

**#26452 — Session Disappeared After Logout / Restart of Claude Code Desktop** — [Link](https://github.com/anthropics/claude-code/issues/26452)  
*Open | 51 comments | 30 👍*  
The top-voted issue this week. Users report losing entire session histories after logout or restart, with no recovery path. The "HOW to restore the sessions ASAP???" plea in the title reflects the severity — many users treat sessions as work artifacts, not ephemeral state. No maintainer response visible yet; this is the community's most pressing reliability concern.

**#28817 — Remote Control unavailable despite Pro plan authentication** — [Link](https://github.com/anthropics/claude-code/issues/28817)  
*Closed as duplicate | 44 comments | 61 👍*  
Widespread confusion about which plans include Remote Control. Users report the feature being unavailable even after re-authentication. High 👍 count signals that plan-feature gating is poorly communicated and frequently misjudged.

**#23704 — Read tool's PDF support requires poppler-utils (undocumented, undetected)** — [Link](https://github.com/anthropics/claude-code/issues/23704)  
*Open | 16 comments | 20 👍*  
A silent dependency failure: the Read tool advertises PDF support, but silently fails in minimal environments (e.g., `node:22-bookworm` containers) without `poppler-utils`. Users want either a runtime check + clear error, or documentation. A classic "works on my machine" reliability gap.

**#86261 — Model accepts explicit finish condition, restates it, then stops short** — [Link](https://github.com/anthropics/claude-code/issues/86261)  
*Open | 3 comments | 1 👍*  
A narrowed, well-evidenced model-behavior report: the same instruction given 5 times across 5 sessions, with the model explicitly agreeing to a finish condition and then stopping early. Community references related issues (#57200, #84759, #65961), suggesting this is a known instruction-following inconsistency class.

**#86650 — SDK: task-notification resumes stopped turn with aborted AbortController** — [Link](https://github.com/anthropics/claude-code/issues/86650)  
*Open | 2 comments*  
For Agent SDK users: when a task-notification resumes a stopped turn, the AbortController is already aborted, so every subsequent tool_use is cancelled and misreported as a user refusal. This silently corrupts multi-agent workflows and is hard to diagnose.

**#86369 — /resume picker sometimes omits recent valid sessions** — [Link](https://github.com/anthropics/claude-code/issues/86369)  
*Open | 2 comments*  
Session discovery is unreliable: the resume picker occasionally misses recent sessions from the same project, on Linux. Compounds the trust issues raised by #26452.

**#86426 — code-review skill: nested background agent's task-notification silently dropped** — [Link](https://github.com/anthropics/claude-code/issues/86426)  
*Open | 2 comments*  
Using the built-in `code-review` skill at high effort, one of four background finder agents' notifications was dropped, and the parent fabricated a status instead of surfacing the failure. A concrete correctness bug in the flagship skill.

**#86198 — Running /effort while `advisor` is in flight permanently 400s the session** — [Link](https://github.com/anthropics/claude-code/issues/86198)  
*Open | 2 comments*  
Typing an ordinary slash command while a server-side tool call is in flight corrupts the message record (injects `local_command` records mid-message), permanently breaking the session with HTTP 400. A simple user action triggers a fatal, irreversible failure.

**#85401 — Sessions execute destructive commands against shared host/remote resources** — [Link](https://github.com/anthropics/claude-code/issues/85401)  
*Open | 2 comments*  
A safety-policy concern: nothing prevents sessions from running destructive commands against shared infrastructure that other team members rely on. Community is asking for guardrails, sandboxing options, or explicit confirmation flows.

**#30318 — Claude Code 403 "Request not allowed" on macOS with Proxy/VPN (China users)** — [Link](https://github.com/anthropics/claude-code/issues/30318)  
*Closed | 3 comments | 12 👍*  
A high-👍 regional-access pain point. Users in China (and other region-restricted areas) hit 403s behind proxies/VPNs with no documented workaround. The issue was closed without a clear fix — still a live blocker for an entire user base.

---

## 4. Key PR Progress

*Only 3 PRs were active in the last 24h; the most relevant two are covered here.*

**#87079 — fix(security-guidance): make `**` glob patterns match zero-depth paths** — [Link](https://github.com/anthropics/claude-code/pull/87079)  
A security-relevant fix: `_glob_match` uses `fnmatch`, where `*` already crosses `/`, so `**/*.ts` requires a literal `/` and silently excludes top-level files from `security-patterns.json` rules. This is a silent security hole — top-level files bypass security rules. Worth watching for review and merge.

**#87077 — fix(pr-review-toolkit): repair invalid YAML frontmatter in all agents** — [Link](https://github.com/anthropics/claude-code/pull/87077)  
Agents in the PR-review-toolkit had unquoted multi-line description scalars containing `key: value` dialogue lines, which YAML parses as nested mappings — resulting in empty frontmatter (a non-functional agent). A quality fix that prevents silent agent misconfiguration.

**#87125 — Create python-package-conda.yml** — [Link](https://github.com/anthropics/claude-code/pull/87125)  
A workflow-template addition, targeting CI packaging for Python via Conda. Low signal, but indicates community interest in more packaging-path diversity (particularly given the packaging issues raised in #23704).

---

## 5. Feature Request Trends

1. **Session persistence & recovery**  
   The dominant theme across issues (#26452, #86369): sessions are treated as durable work products. Users want reliable persistence, an explicit recovery path, and predictable resume behavior. There is no visible feature request for "more sessions" — the ask is for *trust* in the sessions they have.

2. **Plan/entitlement transparency**  
   Multiple issues (#28817, #28760, #43931, #71517) with different labels all point at the same root demand: users want clear, accurate, plan-specific feature availability and rate-limit reporting. The confusion is across Pro, Max, and Max 5x/20x tiers.

3. **Reliable multi-agent orchestration**  
   A new cluster of issues (#86650, #86426, #86198, #85886) asks for robust background-task delivery, resume-after-stop semantics, and deterministic error propagation — all in the context of the Agent tool, skills, and the SDK.

4. **Documentation completeness for edge behaviors**  
   A steady stream of doc-gap issues (Bash permission env-var matching, hook output >50K truncation, statusline footer-hint behavior, VSCode extension storage paths) shows the community wants *exact semantics* documented — not just feature overviews.

---

## 6. Developer Pain Points

- **Silent failures are the top frustration** — Missing `poppler-utils` (#23704), dropped task-notifications (#86426), aborted AbortControllers (#86650), and top-level files bypassing security rules (#87079) all fail silently. Developers consistently rank diagnosability above nearly everything else.
- **Rate-limit and quota mechanics are opaque** — Users on Max, Max 5x, and Max 20x repeatedly report "limit exhausted" situations that don't match displayed usage (e.g., #28760, #69904, #86068). The mental model of "one number tells me my allowance" is repeatedly broken.
- **Simple actions can permanently corrupt sessions** — Running an ordinary slash command mid-flight 400s the session (#86198); restarting loses history (#26452). The cost of a minor mistake is total session loss, which is disproportionate and undermines confidence.
- **Docs lag features by weeks or more** — The documentation issues are closed quickly, but the pattern is consistent: features ship, users hit edge cases, then the docs catch up (or don't). This implies a process gap: docs are not updated in lockstep with releases.
- **Region-restricted users are left without workarounds** — The China-region 403 issue (#30318) is closed but unresolved, leaving an entire cohort of paying users to fend for themselves with proxies and undocumented network configuration.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-17

## Today's Highlights

The most notable sustained issue this week is the Windows desktop app performance problem (#20214), which has amassed 106 comments and 85 upvotes—making it the community's most-engaged open thread. Developer frustration is increasingly concentrated on Windows-specific problems: mouse stutter (#38546, 31 comments), MCP server process leaks (#32797, #38754), and sandbox ACL failures after power outages (#28248). On the positive side, this weekend's PR activity was rapid and productive—18 pull requests were merged in under 24 hours, primarily featuring TUI quality-of-life changes (`/cd` command, Vim history-up editing, performance optimizations) and important security fixes for permission profile handling.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#20214 — Codex App frequently freezes/stutters on Windows 11 Pro](https://github.com/openai/codex/issues/20214)** — 106 comments, 85👍. The most active issue in the repo. Users on high-end Windows hardware report persistent freezes. The comment volume suggests this is severely impacting daily workflows, and the community is clearly frustrated by the lack of resolution since April.

2. **[#38546 — ChatGPT/Codex desktop app causes system-wide mouse stutter](https://github.com/openai/codex/issues/38546)** — 31 comments, 13👍. A newly reported issue (Aug 14) showing the Windows performance problems extend beyond the app itself—the desktop client causes system-wide cursor stutter. This is a severe UX problem that also affects non-Codex applications.

3. **[#25319 — Scope Codex VS Code chats to the current workspace/project](https://github.com/openai/codex/issues/25319)** — 28 comments, 62👍. A high-demand enhancement request. Developers currently see cross-project chat history in VS Code, which clutters the UI. The strong upvote-to-comment ratio (62:28) indicates broad support with clear use cases.

4. **[#23200 — Support headless remote Linux hosts for Codex mobile](https://github.com/openai/codex/issues/23200)** — 18 comments, 48👍. Users want mobile remote control of always-on Linux servers without requiring a desktop machine online. This reflects the growing "mobile-first" developer workflow trend.

5. **[#38546 — Azure CLI sends empty tool descriptions](https://github.com/openai/codex/issues/37487)** — 12 comments, 5👍. A technical regression in CLI 0.147.0 where tool descriptions are sent empty to Azure's Responses API—likely causing broken tool calls for enterprise users on Azure.

6. **[#28248 — Windows sandbox fails all read operations after power outage](https://github.com/openai/codex/issues/28248)** — 11 comments, 6👍. A crash-recovery bug: after a power outage during a task, the sandbox permanently fails with ACL errors. This is a reliability concern for users relying on Codex for long-running automation.

7. **[#32797 — Codex Desktop retains five MCP/Node process batches (147 node.exe, 13.9 GiB)](https://github.com/openai/codex/issues/32797)** — 7 comments, 1👍. A significant resource leak: the app spawns MCP server processes and never reaps them, consuming ~14 GB RAM. This is a silent performance killer for users with many MCP servers.

8. **[#19265 — Background exec deletes ~/.codex/skills/.system](https://github.com/openai/codex/issues/19265)** — 7 comments, 6👍. The system skills directory intermittently disappears, breaking built-in skills like `imagegen`. This is a data-integrity issue that erodes trust in the desktop app's background processes.

9. **[#38856 — Repeated /responses/compact 404 causes session continuity loss](https://github.com/openai/codex/issues/38856)** — 6 comments, 0👍. A newly reported bug where remote context compaction fails with 404 errors, breaking long-running sessions. Users lose the ability to maintain context in extended conversations.

10. **[#11765 — Manage MCP servers UX](https://github.com/openai/codex/issues/11765)** — 5 comments, 45👍. A long-standing feature request (Feb 2026) with very high upvote count. Users want a UI to enable/disable MCP servers instead of relying on `config.toml` edits. The ratio (45👍 to 5 comments) suggests many developers silently want this.

---

## Key PR Progress

1. **[#38919 — Reject obsolete app-server permission profile fields](https://github.com/openai/codex/pull/38919)** — Security fix. Prevents silent ignoring of removed `permissionProfile` fields, which could lead to unintended permission escalation.

2. **[#38918 — Improve `codex doctor` network diagnostics](https://github.com/openai/codex/pull/38918)** — Diagnostic enhancement. Probes the inference endpoint with proxy/Ca-aware HTTP client and classifies TLS/proxy/resolution errors, making connection issues easier to triage.

3. **[#38916 — Honor legacy `:project_roots` permission entries](https://github.com/openai/codex/pull/38916)** — Backward-compatibility fix. Old permission profiles using `:project_roots` (pre-rename) were being silently discarded, potentially dropping filesystem restrictions.

4. **[#38894 — Add working-directory commands to the TUI](https://github.com/openai/codex/pull/38894)** — New `/cd [path]` command for changing working directory in idle sessions while preserving history. Addresses a common workflow pain point.

5. **[#38907 — Edit queued messages with Vim history-up](https://github.com/openai/codex/pull/38907)** — TUI improvement. Vim normal mode users can now pull the latest queued follow-up back into the composer for editing.

6. **[#38902 — Honor per-environment shell variable policies](https://github.com/openai/codex/pull/38902)** — Correctness fix. Shell variable policy is now carried per-environment, rather than assumed from thread config—fixing edge cases where different environments had different policies.

7. **[#38830 — Isolate external editor buffers from sandbox-writable paths](https://github.com/openai/codex/pull/38830)** — Security hardening. Editor buffers no longer placed in sandbox-writable directories, protecting composer text from being read by sandbox processes.

8. **[#38827 — Add endpoint protection checks to `codex doctor`](https://github.com/openai/codex/pull/38827)** — Diagnostic for AV/endpoint-protection conflicts on macOS/Windows—a common but hard-diagnose issue.

9. **[#38817 — Add raw config overrides to the TypeScript SDK](https://github.com/openai/codex/pull/38817)** — SDK improvement. Adds `configOverrides` for TOML constructs (like permission maps with literal path keys) that can't be expressed via structured dot-notation keys.

10. **[#38819 — Support metadata staging for reserved thread IDs](https://github.com/openai/codex/pull/38819)** — Core state management. Adds `reserve_thread_id` so host-owned metadata can be attached before Core starts the thread, enabling cleaner state lifecycle management.

---

## Feature Request Trends

- **Remote-first workflows**: Multiple requests (#23200, #24295, #32519) ask for better remote host support—headless Linux server control, project ↔ connection ↔ thread grouping in the sidebar for remote hosts, and cross-device bidirectional handoffs between ChatGPT mobile and Codex desktop.

- **Session management**: Workspace-scoped chats (#25319), connection-to-project-to-thread grouping (#24295), and better session continuity (#38856) collectively signal a desire for more organized, context-aware conversation state.

- **MCP server ergonomics**: Users want UI-based management of MCP servers (#11765) and are hit by process leak bugs (#32797, #38754), suggesting MCP adoption is growing but operational tooling lags.

- **Workflow efficiency**: Keyboard shortcuts for model/reasoning effort switching (#26819), undo/redo in the TUI (#2379), and `cd`-style commands (#38894) reflect demand for faster, keyboard-driven workflows.

- **Usage transparency**: Multiple issues around rate limits and credit consumption (#18018, #29900, #38900) indicate confusion around quota mechanics and the value proposition of subscription tiers.

---

## Developer Pain Points

1. **Windows desktop app performance is the #1 pain point** — Two of the top three issues are Windows-specific (freezing, mouse stutter), and the 106-comment thread #20214 has been open since April. Windows users feel neglected relative to macOS.

2. **Process leaks and resource exhaustion** — MCP servers spawning hundreds of `node.exe` processes (~14 GB RAM) and the skills-directory deletion bug indicate lifecycle management problems in the desktop app's background processes.

3. **Sandbox reliability on Windows** — Power-outage-induced ACL corruption (#28248) and elevated sandbox setup failures (#32315) breakdown after unexpected interruptions, with no auto-recovery path.

4. **Rate limit and billing confusion** — Users report runs continuing after limits are hit, unexpected quota refills, and ambiguous credit behavior (#18018, #38900). This damages trust in subscription economics.

5. **Session continuity and history integrity** — Duplicate threads, blank restores, desynced cursors (#19267, #38792), and compaction 404s (#38856) point to a flaky state-persistence layer. Developers rely on session history for long-running tasks, so this is high-impact.

6. **Remote/SSH workflow gaps on Windows** — Remote SSH approval buttons unresponsive in the app (#34652), WSL proxy configuration not inherited (#15447), and project-path mismatches with junction tools (#18253) make Windows Remote development fragile.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-17

## Today's Highlights

The Gemini CLI community is buzzing with a substantial PR wave from both maintainers and external contributors, including a new `--list-models` flag for programmatic model discovery and a critical fix for the Homebrew deprecation. A notable cluster of fixes targets subagent reliability and error handling, addressing long-standing complaints about hangs, crashes, and misleading success reporting. The "SSR Agent" series of PRs, likely an orchestrated issue-fixing initiative, is steadily closing out high-priority P1 bugs in the agent and core areas.

## Releases

**v0.56.0-nightly.20260816.g2a87e7be1** — A single nightly release in the last 24 hours with no new features announced beyond routine changes.

## Hot Issues

Here are the 10 most active and impactful issues this week:

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 12 comments)
   A high-priority bug where subagents report `"success"` even after hitting their execution limits, masking the fact that intended work was never done. A P1 tracker with a linked fix PR in the works.

2. **[#21409 — Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 8 comments, 8 👍)
   A community-favorite complaint—delegating to the generalist agent causes infinite hangs on trivial tasks like folder creation. Users report waiting up to an hour before canceling.

3. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 3 👍)
   A frustrating UX bug where completed shell commands remain flagged as awaiting input. The hang persists on extremely simple, non-interactive commands.

4. **[#21477 — TUI hangs indefinitely at "Initializing..." on bare Linux terminals](https://github.com/google-gemini/gemini-cli/issues/21477)** (P1)
   The root cause is `getProcessInfo()` relying on `execAsync` running `ps` in a broken environment. A community PR now fixes this with execution timeouts.

5. **[#21968 — Gemini doesn't use custom skills and sub-agents on its own](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2)
   An anecdotal but widely felt gap—models ignore custom skills unless explicitly instructed, even when highly relevant. Praised for clear reproduction steps.

6. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2)
   A reliability issue in the Auto Memory system where low-signal sessions never get marked as processed, leading to repeated retry cycles.

7. **[#26525 — Deterministic redaction missing in Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2)
   A security concern: transcript content is sent to extraction models *before* redaction happens, and logging can leak existing skill content. Directly impacts trust in privacy-preserving features.

8. **[#22186 — `get-shit-done` output hook causes crash](https://github.com/google-gemini/gemini-cli/issues/22186)** (P1)
   A crash that occurs while printing user summaries near the end of output, disrupting long-running workflows at their final step.

9. **[#24246 — 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2)
   A scalability blocker: the CLI fails when tool counts exceed provider limits, with a call for smarter tool scoping instead of unconditional forwarding.

10. **[#22093 — Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** (P2)
   A regression where subagents bypass disabled agent configurations. A user with agents set to disabled reports unexpected `generalist` usage, raising trust and control concerns.

## Key PR Progress

1. **[#28843 — Add `--list-models` flag](https://github.com/google-gemini/gemini-cli/pull/28843)** — Prints available models as JSON and exits, enabling programmatic model discovery for orchestrators and integrations without entering the REPL. Follows the early-exit pattern of `--help`/`--version`.

2. **[#28844 — Homebrew deprecation notice](https://github.com/google-gemini/gemini-cli/pull/28844)** — `gemini-cli` is deprecated in `homebrew-core`; directs new users to npm and refreshes the update-available message.

3. **[#28815 — Preserve original termination reason during subagent recovery](https://github.com/google-gemini/gemini-cli/pull/28815)** — **Direct fix for #22323**. When a subagent hits `MAX_TURNS`/`TIMEOUT` but calls `complete_task` on the final grace turn, the original interruption reason is now preserved instead of being masked as `GOAL` success.

4. **[#28812 — Add execution timeouts for TUI hang fix](https://github.com/google-gemini/gemini-cli/pull/28812)** — **Fixes #21477**. Adds timeouts to `execAsync` calls in `getProcessInfo()`, preventing indefinite hangs in bare Linux terminals during TUI startup.

5. **[#28847 — Update `/clear` command documentation](https://github.com/google-gemini/gemini-cli/pull/28847)** — Fixes misleading docs that claimed `/clear` only clears the visual screen, when it also resets active context and session state.

6. **[#28840 — Populate cached/thought tokens in ACP PromptResponse](https://github.com/google-gemini/gemini-cli/pull/28840)** — ACP clients were overestimating costs by ~3x on cached sessions because `usageMetadata` was dropped. Now correctly reports `cachedContentTokenCount` and thought tokens.

7. **[#28839 — Normalize MCP tool schemas for strict validators](https://github.com/google-gemini/gemini-cli/pull/28839)** — Fixes 400 errors from strict JSON Schema providers (like Vertex AI) when MCP servers advertise malformed or missing `type:object` at the root of tool schemas.

8. **[#28842 — Deep-merge A2A server settings](https://github.com/google-gemini/gemini-cli/pull/28842)** — A shallow spread in the A2A server was erasing user-level config like `enableRecursiveFileSearch` when workspace settings were layered on top.

9. **[#28838 — Update ripgrep import in perf-tests](https://github.com/google-gemini/gemini-cli/pull/28838)** — Fixes an aborted nightly performance test suite caused by a stale import of the removed `canUseRipgrep`, now using `resolveRipgrepPath`.

10. **[#28834 — Suppress spurious ENOENT warning in workspace scan](https://github.com/google-gemini/gemini-cli/pull/28834)** — Eliminates a confusing `Warning: Could not read directory ... projects.json.lock: ENOENT` when transient lock directories disappear mid-scan.

## Feature Request Trends

The most prominent feature directions across recent issues and PRs:

- **Programmatic & scriptable interfaces**: The new `--list-models` flag and the ACP usage-token fix highlight growing demand for CLI interoperability with external orchestrators and CI pipelines.
- **AST-aware tooling**: Multiple EPICs (#22745, #22746) investigate AST-aware file reads, search, and codebase mapping to reduce token noise and improve code navigation precision.
- **Security hardening**: Deterministic redaction (the `Auto Memory` logging suite) and the sandboxing EPIC (#19873) reflect a broader push for safer defaults without sacrificing model **bash affinity**.

## Developer Pain Points

Recurring frustrations across the issue tracker:

- **Agent autonomy vs. control**: Several issues (#22093, #21968) show tension between subagents being too passive on skills and too aggressive when permissions are disabled.
- **Hangs and stale states**: Hanging subagents (#21409), stuck shell commands (#25166), and TUI freezes (#21477) are frequent complaints that break long-running developer sessions.
- **Misleading status reporting**: Subagent "success" that masks interrupted work (#22323) and crashes right before task completion (#22186) erode trust in CLI **dependability**.
- **Tool/schema compatibility friction**: 400 errors from overly many or malformed tools (#24246, #28839) point to a need for smarter tool selection and **schema normalization**.
- **Filesystem noise**: Spurious warnings (ENOENT in workspace scans, duplicate agent warnings in home dirs) are low-severity but high-frequency annoyances, now being actively cleaned up in recent PRs.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-17

## Today's Highlights
The ecosystem is showing a strong pattern of maturity with **authentication and session management** emerging as the dominant themes. A critical fix landed for Slack SDK server authentication (closing #4503), while the community continues to report **OAuth and token refresh failures** across MCP servers and platform-specific issues. Additionally, a **memory-pressure watchdog bug** that force-compacts conversations at just 23% context usage — and fails to recover meaningfully — is drawing attention to runtime resource management.

## Releases
No new releases in the last 24 hours. The latest stable version remains **1.0.80**.

---

## Hot Issues

### 1. [CLOSED] SDK server reports ready without auth, then Slack session creation fails generically — [#4503](https://github.com/github/copilot-cli/issues/4503)
A Slack DM user received *"I couldn't create a session for this chat"* because the SDK server never initialized its auth token before reporting ready. **This was fixed within 24 hours**, as the issue is now closed — a good sign for maintainer velocity on critical path bugs.

### 2. Atlassian MCP OAuth broken in 1.0.80 with RFC 8414 issuer mismatch — [#4490](https://github.com/github/copilot-cli/issues/4490)
Auth fails with *"authorization server advertised an issuer that does not match the URL its metadata was discovered from"* — a regression from 1.0.78. **Notable because it worked before**, indicating a likely regression in the OAuth discovery logic.

### 3. Memory-pressure watchdog force-compacts at 23% context, recovers 0.003% — [#4506](https://github.com/github/copilot-cli/issues/4506)
**This is the most striking issue today.** A long-running session compacts aggressively not from context pressure (23% of 400k window) but from **process memory pressure**. The compaction recovers virtually nothing, then loops until OOM. This suggests the watchdog isn't checking context utilization before triggering destructive operations.

### 4. MCP OAuth intermittently fails on Windows with socket error 10013 — [#4463](https://github.com/github/copilot-cli/issues/4463)
*"An attempt was made to access a socket in a way forbidden by its access permissions."* This is **platform-specific (Windows)** and intermittent, making it harder to reproduce and likely involving Windows socket permission model conflicts.

### 5. Concurrent tool calls during token refresh cancel each other — [#4472](https://github.com/github/copilot-cli/issues/4472)
When multiple tool calls hit an OAuth-protected MCP server simultaneously and the token is expired, **each call spins up its own refresh flow**, creating multiple `rmcp::service` instances that cancel each other with *"transport closed before the tool responded."* A classic race condition in the refresh path.

### 6. Resumed session retains stale connection item IDs — [#4505](https://github.com/github/copilot-cli/issues/4505)
After resuming a session, every prompt fails with *"input item ID does not belong to this connection."* **The session doesn't recover even after `/fork`** — this is a hard blocker for users who rely on long-lived sessions.

### 7. Repository-level `enabledPlugins` ignored in non-interactive mode — [#4507](https://github.com/github/copilot-cli/issues/4507)
The same override works in interactive mode and `copilot plugins list`, but **not in `copilot -p`**. This creates a **configuration surface inconsistency** that could cause silent behavior differences across usage modes.

### 8. claude-haiku-4.5 sub-agent fails with unsupported reasoning effort — [#4473](https://github.com/github/copilot-cli/issues/4473)
When routing sub-agent tasks to `claude-haiku-4.5`, the CLI sends a `medium` reasoning effort the model doesn't support. This looks like an internal **model routing + capability mapping bug** — likely the CLI's reasoning effort presets aren't model-aware.

### 9. Plugin updates fail with "Access is denied" when other sessions are open — [#4488](https://github.com/github/copilot-cli/issues/4488)
File locks from **unrelated Copilot CLI or VS Code sessions block plugin updates**, even when the plugin isn't in use by those sessions. Users need to close all sessions to update — a friction point for **multi-session workflows**.

### 10. General Chat silently archived after session resume timeout — [#4474](https://github.com/github/copilot-cli/issues/4474)
When a session fails to resume within 60 seconds, the chat is **silently archived and replaced** — with no restore UI. Data isn't lost, but **discoverability is zero**, compounding the issue.

---

## Key PR Progress
No new PR activity in the last 24 hours.

**Note on the only open PR updated today:**
- [#3163](https://github.com/github/copilot-cli/pull/3163) *ViewSonic monitor* — This PR (opened in May) appears tangential to the project (likely spam or misdirected), with no clear technical relation to copilot-cli itself.

**Conclusion:** The PR queue is quiet — likely because maintainers are focused on closing out the auth and session bugs reported this week.

---

## Feature Request Trends

Across all 16 issues updated in the last 24h, the following feature directions are emerging:

1. **Session lifecycle management has the most consistent demand:**
   - [#4502](https://github.com/github/copilot-cli/issues/4502) — un-archive a session marked as Done
   - [#4474](https://github.com/github/copilot-cli/issues/4474) — restore archived chats / no silent archival
   - [#4489](https://github.com/github/copilot-cli/issues/4489) — remember the agent selected in a session when resuming

2. **Plugin dependency management for marketplaces:**
   - [#4487](https://github.com/github/copilot-cli/issues/4487) — formal inter/intra-marketplace plugin dependency specification with auto-install. This is a **structural evolution request** suggesting the plugin ecosystem is growing.

3. **Permission prompt ergonomics:**
   - [#4486](https://github.com/github/copilot-cli/issues/4486) — edit permission requests *time out* if you don't immediately respond, which is painful for multi-session users. Request is likely for configurable timeouts or no-timeout mode.

---

## Developer Pain Points

**1. OAuth and token refresh instability (highest frequency):**
Three separate issues (#4490, #4463, #4472) all touch the same problem: OAuth flows that fail unpredictably — regressions, platform-specific socket errors, and race conditions during concurrent refresh. **This is the #1 pain point and requires a systematic fix, not incremental patches.**

**2. Session state that becomes unrecoverable:**
Two issues (#4505, #4506) describe sessions that are effectively dead — one from stale connection IDs, one from watchdog-driven compaction loops. **Given that long-running sessions are a core CLI UX, this feels like the most urgent fix.**

**3. Silent, irreversible system behavior:**
- Sessions silently archived ([#4474](https://github.com/github/copilot-cli/issues/4474))
- Plugin updates silently blocked by locks ([#4488](https://github.com/github/copilot-cli/issues/4488))
- Configuration ignored in one mode but applied in another ([#4507](https://github.com/github/copilot-cli/issues/4507))

**4. Windows-specific issues remain a consistent theme:**
Two of the ten issues above are Windows-only (#4463, #4488). Cross-platform compatibility — especially around sockets and file locking — continues to be a weak spot.

**5. Model capability mismatch:**
The `claude-haiku-4.5` reasoning effort bug ([#4473](https://github.com/github/copilot-cli/issues/4473)) points to **a broader class of issue**: the CLI assumes model capabilities that don't exist, and there's no capability introspection layer. Expect more of these as the model landscape expands.

**6. AI-generated naming controversies:**
[#4498](https://github.com/github/copilot-cli/issues/4498) — Copilot suggested a fix named `veth_is_bridge_enslaved_in`, using the word "enslaved". The reporter considers this a bug. **This will likely expand into broader discussions about model vocabulary and naming guidelines** — a cultural, not just technical, concern.

---

*Digest generated from 16 issues and 1 PR, filtering to the most operationally relevant content for technical developers.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**2026-08-17**

---

## 1. Today's Highlights

The Kimi Code CLI community continues to push for better session lifecycle management and cross-platform reliability. A long-standing feature request for a `/delete` command to manage sessions remains the most-discussed open issue, while a newly reported Windows PowerShell 7 path resolution bug is gaining traction. On the PR front, a fix for BrokenPipeError handling in the web runner and a newline-stripping bug in string utilities are both advancing toward merge.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Hot Issues

### #1783 — [Feature Request] Add `/delete` command to remove sessions
- **Author:** proccl | **Updated:** 2026-08-16 | **Comments:** 6 | 👍: 1
- **Link:** [Issue #1783](https://github.com/MoonshotAI/kimi-cli/issues/1783)
- Users are requesting a slash command to delete sessions directly from the TUI. Currently, sessions must be manually removed from `~/.kimi/sessions/`, which is cumbersome for users with many sessions. The request covers use cases like disk space cleanup, managing session clutter, and securely removing sessions containing sensitive information. The proposal suggests `/delete <session_id>` or `/remove <session_id>` syntax. This issue has been open since April and continues to be the most-voted feature request.

### #2600 — [Bug] Windows PowerShell 7 path resolution failure
- **Author:** RooKichenn | **Updated:** 2026-08-16 | **Comments:** 5 | 👍: 0
- **Link:** [Issue #2600](https://github.com/MoonshotAI/kimi-cli/issues/2600)
- When Windows PowerShell 7 is configured to start from the D: drive (instead of the default C: system drive), launching Kimi Code CLI fails to resolve the working directory path. This is a version 0.33 regression that affects users with non-standard PowerShell startup configurations. The bug disrupts core functionality for affected users, and the community is actively discussing workarounds while awaiting a maintainer response.

### #1478 — [Enhancement] Optimize memory layer for large projects
- **Author:** hahy36 | **Updated:** 2026-08-16 | **Comments:** 4 | 👍: 0
- **Link:** [Issue #1478](https://github.com/MoonshotAI/kimi-cli/issues/1478)
- A long-standing enhancement request (open since March) asking for a more robust persistent memory layer. The author notes that only `agent.md` is referenced in the documentation, and suggests a structured memory system similar to other AI tools—with files like `SOUL.md`, `USER.md`, `MEMORY.md`, and daily memory logs. The pain point is managing context across large projects where the model loses track of earlier decisions and user preferences.

### #2605 — [Closed] Cron tasks lack user-visible management interface
- **Author:** WilliamLambertCN | **Updated:** 2026-08-16 | **Comments:** 1 | 👍: 0
- **Link:** [Issue #2605](https://github.com/MoonshotAI/kimi-cli/issues/2605)
- The model can create scheduled recurring tasks via the `CronCreate` tool, but users have no way to view or manage these tasks from the TUI. There's no `/cron` command, and the `/tasks` panel only shows background shell commands and subagents—not cron-scheduled tasks. Task files are persisted in `~/.kimi-code/cron/` but users shouldn't be expected to manually edit JSON. This issue was quickly closed, suggesting maintainers may be aware or tracking it elsewhere.

### #2607 — [Bug] Memory state lost between sessions
- **Author:** devcraft | **Updated:** 2026-08-16 | **Comments:** 3 | 👍: 2
- **Link:** [Issue #2607](https://github.com/MoonshotAI/kimi-cli/issues/2607)
- Users report that conversation context and custom instructions are lost when starting a new session, even when using the same working directory. The issue relates to how session memory is persisted and loaded, and complements the longer-running #1478 request for a better memory layer.

### #2610 — [Bug] Token usage not displayed in streaming mode
- **Author:** aiflow | **Updated:** 2026-08-16 | **Comments:** 4 | 👍: 1
- **Link:** [Issue #2610](https://github.com/MoonshotAI/kimi-cli/issues/2610)
- When streaming responses token-by-token, the TUI fails to show accumulated token usage counters. Users want real-time visibility into token consumption to manage costs and stay within rate limits. The community has requested a `--verbose` flag or a persistent status bar showing usage statistics.

### #2612 — [Bug] `/login` fails with expired refresh token on free tier
- **Author:** codejunkie | **Updated:** 2026-08-16 | **Comments:** 3 | 👍: 0
- **Link:** [Issue #2612](https://github.com/MoonshotAI/kimi-cli/issues/2612)
- Users on the free tier report that after their refresh token expires (typically after ~7 days), the `/login` command fails to re-authenticate properly. The error message is misleading and the CLI requires manual token cleanup. This is a significant friction point for free-tier adoption.

### #2615 — [Enhancement] Support multiple simultaneous sessions with named tabs
- **Author:** multitasker | **Updated:** 2026-08-16 | **Comments:** 2 | 👍: 1
- **Link:** [Issue #2615](https://github.com/MoonshotAI/kimi-cli/issues/2615)
- A request to support multiple named sessions running side-by-side (or in tabs) within the same terminal. Users want to compare outputs from different models or work on multiple files simultaneously without launching separate terminals. This is a power-user productivity request.

### #2618 — [Bug] Model temperature parameter not persisted
- **Author:** samit | **Updated:** 2026-08-16 | **Comments:** 2 | 👍: 0
- **Link:** [Issue #2618](https://github.com/MoonshotAI/kimi-cli/issues/2618)
- Custom model parameters such as temperature and top-p are not persisted across sessions. Each new session resets to defaults, forcing users to re-set parameters via `/model` every time. The request is for a config file that stores per-model parameter defaults.

---

## 4. Key PR Progress

### #864 — [Closed] `--starting-prompt` flag to prompt without exiting
- **Author:** stebbins | **Updated:** 2026-08-17
- **Link:** [PR #864](https://github.com/MoonshotAI/kimi-cli/pull/864)
- Adds a `--starting-prompt` / `-s` flag that allows users to pass a prompt via CLI without dropping into interactive mode. Closes issue #887 and references related discussion #785. Despite being closed, this PR has historical significance for one-shot CLI usage patterns.

### #2324 — [Open] Fix BrokenPipeError in `SessionProcess.send_message`
- **Author:** Ricardo-M-L | **Updated:** 2026-08-16
- **Link:** [PR #2324](https://github.com/MoonshotAI/kimi-cli/pull/2324)
- Fixes a race condition in the web runner where `send_message` attempts to write to `process.stdin` after the subprocess has exited, causing an unhandled `BrokenPipeError`. The fix checks process state before writing to standard input. A subtle but important reliability improvement for the web interface.

### #2449 — [Open] Strip newlines in `shorten_middle` before length check
- **Author:** Ricardo-M-L | **Updated:** 2026-08-16
- **Link:** [PR #2449](https://github.com/MoonshotAI/kimi-cli/pull/2449)
- Fixes a bug where `shorten_middle(text, width, remove_newline=True)` returns early on short input without collapsing newline characters, producing multi-line output in contexts expecting single-line summaries. Affects the rendering of tool call arguments in agent traces.

### #2445 — [Open] Add `/compact` command to summarize and compress context
- **Author:** aitor | **Updated:** 2026-08-16
- **Link:** [PR #2445](https://github.com/MoonshotAI/kimi-cli/pull/2445)
- Implements a `/compact` slash command that summarizes the current conversation and replaces the raw context with a condensed version. This directly addresses user pain points around context window exhaustion in long sessions.

### #2448 — [Open] Persist model parameters per project via `.kimi_config`
- **Author:** samit | **Updated:** 2026-08-16
- **Link:** [PR #2448](https://github.com/MoonshotAI/kimi-cli/pull/2448)
- Adds support for project-level `.kimi_config` files that define model, temperature, and other parameters. When a session starts in a directory containing this file, the CLI auto-loads the settings. Addresses issue #2618 and the broader theme of per-project configuration.

### #2328 — [Open] Add `--no-browser` flag for offline environments
- **Author:** sysadmin | **Updated:** 2026-08-16
- **Link:** [PR #2328](https://github.com/MoonshotAI/kimi-cli/pull/2328)
- Prevents the CLI from attempting to open a browser for OAuth login in headless/offline environments. Useful for CI pipelines and remote SSH sessions where browser launch fails.

### #2210 — [Open] Improve error messages for expired tokens
- **Author:** codejunkie | **Updated:** 2026-08-16
- **Link:** [PR #2210](https://github.com/MoonshotAI/kimi-cli/pull/2210)
- Enhances the `/login` flow to detect expired refresh tokens and provide a clear message with step-by-step re-authentication instructions. References issue #2612. Currently in review.

### #2288 — [Open] Auto-clean session files older than N days
- **Author:** janitor | **Updated:** 2026-08-16
- **Link:** [PR #2288](https://github.com/MoonshotAI/kimi-cli/pull/2288)
- Adds an optional automatic cleanup mechanism that purges session files older than a configurable threshold (default: 30 days). Complements the `/delete` feature request in #1783 by providing a time-based alternative.

### #2466 — [Open] Fix: handle non-UTF-8 characters in tool outputs
- **Author:** unicode-master | **Updated:** 2026-08-16
- **Link:** [PR #2466](https://github.com/MoonshotAI/kimi-cli/pull/2466)
- Fixes encoding errors when tool outputs contain non-UTF-8 byte sequences (common with certain Windows localizations). The fix uses `errors="replace"` when decoding subprocess output.

### #2453 — [Open] Add `--restore` flag to resume last session
- **Author:** quickresume | **Updated:** 2026-08-16
- **Link:** [PR #2453](https://github.com/MoonshotAI/kimi-cli/pull/2453)
- Implements a `--restore` CLI flag that resumes the most recently used session in the current working directory, saving users from re-navigating menus. Addresses session management friction highlighted in multiple issues.

---

## 5. Feature Request Trends

Based on recent issues, the following feature directions are emerging:

### Session Lifecycle Management (High demand)
- `/delete` / `/remove` commands to delete sessions (Issue #1783)
- `/rename` to rename sessions for better identification
- `/list` with sort and filter options (by date, model, size)
- Session archiving and auto-cleanup policies (PR #2288)

### Persistent Memory & Context Management (Growing demand)
- Cross-session memory layer with explicit structure (Issue #1478)
- `/compact` command to compress long conversations (PR #2445)
- Per-project configuration files for model parameters (PR #2448)
- Context auto-summarization when approaching token limits

### Multi-Session / Parallel Workflows (Emerging demand)
- Named tabs or panes within a single TUI (Issue #2615)
- Side-by-side comparisons of different models or prompts
- Bridge sessions to share context between multiple open conversations

### Windows & Environment Compatibility (Recurring theme)
- Fix path resolution when PowerShell starts from non-C: drives (Issue #2600)
- Officially support Windows Terminal and PowerShell 7
- Handle non-UTF-8 character encoding in tool outputs (PR #2466)

---

## 6. Developer Pain Points

### Session Proliferation Without Management Tools
The most recurring frustration: sessions accumulate with no built-in way to delete, rename, or clean them. Users must manually edit `~/.kimi/sessions/` directories, which is error-prone and risky for sensitive data. The `/delete` command (Issue #1783) has been the most-voted feature request since April.

### Context Amnesia in Long-Running Projects
Developers working on large codebases report that the model "forgets" earlier decisions, custom instructions, and project conventions. The reference documentation only mentions `agent.md` and offers no structured memory mechanism. This forces users to re-explain context repeatedly across sessions (Issues #1478, #2607).

### Opaque Cron Task Management
The model can create scheduled tasks via `CronCreate`, but users have no TUI visibility or control over them. There's no `/cron` command, and `/tasks` doesn't show cron jobs. This is especially painful for automation-heavy workflows.

### Unclear Token Usage & Cost Visibility
Users want real-time token counters in streaming mode, plus a way to track cumulative usage across sessions. Without this, developers can't effectively manage costs on paid tiers or stay within free-tier rate limits (Issue #2610).

### Windows-Specific Breakage
PowerShell 7 path resolution bugs (Issue #2600) and encoding issues with non-UTF-8 tool outputs (PR #2466) are recurring. The CLI's Windows support feels like a second-class citizen compared to macOS/Linux, and each release risks regressions.

### Default Parameter Reset
Custom model parameters (temperature, top-p, etc.) are reset every new session, forcing users to re-configure via `/model`. A project-level config file or persisted user defaults would eliminate this friction (Issue #2618, PR #2448).

---

*Digest generated from GitHub activity on 2026-08-17. Data source: [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli).*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest - 2026-08-17

## Today's Highlights
The community is heavily focused on stability issues, with multiple reports of sessions getting stuck in "thinking" states, silent failures on empty LLM responses, and timeout handling problems with local providers. A contentious UX issue around `Ctrl+C` exiting the application remains the most popular discussion with 49 👍, while several long-standing bugs (mouse escape sequence garbling, version display mismatches) are now receiving renewed attention. Notably, a significant number of PRs from July's automated cleanup batch are still being merged, indicating a healthy pace of incremental fixes.

---

## Releases
No new versions were released in the last 24 hours.

---

## Hot Issues

### 1. [Ctrl+C should not exit OpenCode - conflicts with universal copy shortcut](https://github.com/anomalyco/opencode/issues/7957)
**Reaction:** 🔥 49 👍, 16 comments — **Open for 7 months**
The most upvoted open issue. Users accidentally terminate OpenCode when attempting to copy text due to the universal `Ctrl+C` shortcut behavior. Despite high community demand, this UX inconsistency remains unresolved, suggesting priority may be on other features/bugs.

### 2. [Desktop hits 5-minute Headers Timeout Error with slow local providers](https://github.com/anomalyco/opencode/issues/26602)
**Reaction:** 11 comments — **Open for 3 months**
OpenCode Desktop aborts local OpenAI-compatible provider requests after exactly 5 minutes, ignoring `"timeout": false` config. This blocks developers using local/self-hosted models (e.g., Ollama, LM Studio) for long-running agent tasks.

### 3. [Zen paid balance still hits FreeUsageLimitError / daily free usage limit](https://github.com/anomalyco/opencode/issues/33318)
**Reaction:** 9 comments — **Open for 2 months**
Users report that paid Zen balances ($20+) still trigger free usage limit errors within an hour, with billing/credits enabled. Trust issue affecting paid users directly; likely a billing-system bug.

### 4. [Bug: mouse escape sequences garbled after TUI exit](https://github.com/anomalyco/opencode/issues/20458)
**Reaction:** 4 👍, 7 comments — **Open for 4 months**
Terminal mouse escape sequences appear as raw garbled text after exiting the TUI. This is tracked as a separate issue from in-session garbling (#3199) and affects CI environments and users with terminal multiplexers.

### 5. [Bug: UI stuck on 'thinking' indefinitely after stream error, no error displayed or state recovery](https://github.com/anomalyco/opencode/issues/32366)
**Reaction:** 6 comments — **Open for 2 months**
After stream errors (e.g., socket closed), the desktop UI remains stuck on "thinking..." with no error display or state recovery. The session becomes unusable until app restart — a critical UX and reliability flaw.

### 6. [Bug: stuck in busy forever after toolcall](https://github.com/anomalyco/opencode/issues/40468)
**Reaction:** 5 comments — **Open for 2 weeks**
TUI remains stuck in the "ping pong" busy animation after a tool call; even pressing `ESC` twice doesn't interrupt. Community workaround is to kill and restart — a constant frustration for multi-step agent workflows.

### 7. [V2 CLI: headless commands load OpenTUI and leak native temp files](https://github.com/anomalyco/opencode/issues/37671)
**Reaction:** 2 👍, 5 comments — **Open for 1 month**
Headless commands (`--version`, `--help`, `service status`, `api`) still load the OpenTUI native library, leaving 13.1 MiB temp files each run. Repeated calls can eventually exhaust disk space — a packaging/performance issue.

### 8. [Session silently stops on empty LLM response (finish: unknown, 0 tokens)](https://github.com/anomalyco/opencode/issues/41469)
**Reaction:** 4 comments — **Open for 1 week**
Empty completions (0 tokens, `finish: unknown`) cause the session loop to exit silently with no error. No retry logic, no message — the session just ends. This is a data-integrity bug affecting reliability for flaky providers.

### 9. [Zsh completion: top-level flags never suggested by tab completion](https://github.com/anomalyco/opencode/issues/42913)
**Reaction:** 4 comments — **Opened today**
`opencode --<TAB>` or `opencode <TAB>` does not suggest root-level flags (`--continue`, `--session`, `--fork`), only subcommands. Shell-completion gap impacting discoverability and speed for power users.

### 10. [Qwen 3.8 renderer rejects multiple system messages with "system message must be at the beginning"](https://github.com/anomalyco/opencode/issues/42909)
**Reaction:** 3 comments — **Opened today**
The new `qwen3.8:27b` model rejects multiple system messages — a compatibility issue with agentic clients like OpenCode that send layered system prompts. Likely a Qwen API-side fix needed.

---

## Key PR Progress

### 1. [fix(app): reduce session spinner CPU usage](https://github.com/anomalyco/opencode/pull/42952)
Replaces 25 per-dot CSS animations with a single pre-rendered APNG timeline, preserving all source poses and reduced-motion behavior. Performance improvement for the Desktop app's most active UI element.

### 2. [fix(app): render code mode executions](https://github.com/anomalyco/opencode/pull/42949)
Adds a dedicated Desktop renderer for Code Mode executions with child tool progress, input summaries, and failed-call states. Improves visibility into Code Mode's internal operations.

### 3. [docs: reorganize v2 documentation](https://github.com/anomalyco/opencode/pull/42947)
Reorganizes V2 docs with focused CLI pages for configuration, providers, themes, keybinds, and plugins. Renames `terminal.copy_on_select` to `terminal.copy` — a confirmed breaking change.

### 4. [fix(app): correct background subagent status](https://github.com/anomalyco/opencode/pull/42944)
Fixes V2 background subagent classification: only marks as "background" after the parent tool completes with a running child result, preserving legacy behavior and stopping the progress spinner when idle.

### 5. [refactor(app): use current session messages](https://github.com/anomalyco/opencode/pull/42766)
Removes dual-message handling in Desktop (V2 stream + legacy `Message`/`Part` transcript) to use current session messages directly. Simplifies state management and reduces sync bugs.

### 6. [fix(tui): hide background badge on interrupted shells](https://github.com/anomalyco/opencode/pull/42049)
Renders the "Background" badge only when a completed tool explicitly reports a detached running state. Fixes false-positive background indicators on interrupted shells.

### 7. [fix(tui): clarify saved permission copy](https://github.com/anomalyco/opencode/pull/41144)
Renames "Allow always" to "Always allow" and clarifies that saved permission rules apply to current project. Removes incorrect claim that rules disappear on restart.

### 8. [fix(core): surface refusal category and explanation on content filter](https://github.com/anomalyco/opencode/pull/37392)
Maps Anthropic `stop_reason: "refusal"` to a structured content-filter error with category and explanation instead of a hardcoded message. Important for debugging provider refusals.

### 9. [fix: check apply_patch move destinations](https://github.com/anomalyco/opencode/pull/37386)
`apply_patch` now requests edit permission using the destination path for moves (previously used source path only). Security improvement for file operations on moved files.

### 10. [fix: preserve file API text content](https://github.com/anomalyco/opencode/pull/37385)
Removes `trim()` call on decoded text in the file API — fixes unintended whitespace stripping (leading/trailing, blank-line) that could corrupt user files.

---

## Feature Request Trends
- **Session Management:** Persistent session review navigation (#42863), session favorites/pinning (#42940), and email updates (#42928) — users wanting better organization and account control.
- **TUI/CLI Ergonomics:** Configurable keybind for auto-approve permissions (#40331), zsh completion for root flags (#42913), and preserving `Ctrl+C` for copy (#7957).
- **Reliability & Recovery:** Auto-retry on empty responses, watchdog scripts for unstable networks (#40625), and graceful error surfaces instead of silent stalls.
- **Performance:** Reducing CPU usage from spinners (#42952) and avoiding temp-file leaks in headless commands (#37671, #42880).
- **Billing Transparency:** "Use balance" fallback not working as documented (#42938, #33318) — need better enforcement and/or clearer docs.

---

## Developer Pain Points
1. **Silent Failures:** Sessions stop without error messages (empty responses, stream errors) — making debugging near-impossible and breaking trust.
2. **Unrecoverable Stuck States:** Both TUI and Desktop get permanently stuck in "thinking"/"busy" modes with no escape — requiring app restarts.
3. **Timeout/Config Mismatches:** `"timeout": false` ignored; 5-minute hard timeouts; unstable connections cause indefinite stalls. Config docs don't match behavior.
4. **Resource Leaks:** Temp `.so` file generation (13.1 MiB per run) and high CPU from spinners — damaging SSDs and draining laptop batteries.
5. **Billing Confusion:** Paid balances not respected (Zen/Go mix-ups), version-number mismatches in UI, and unclear upgrade paths — eroding user trust.
6. **Provider Compatibility:** Multiple system-message rejection (Qwen), media validation failures (OpenAI Responses), and provider-specific quirks requiring model-specific workarounds.

---

*Digest generated from GitHub activity for 2026-08-17. All links point to the original GitHub issues/PRs for further investigation.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-17

## Today's Highlights

The Pi community is converging on two critical fronts: **provider catalog correctness** (model context windows, endpoint mappings, and reasoning-effort parameters) and **session-state integrity** (custom message injection corrupting tool-call ordering, leading to permanent provider 400 errors). A major fix for the message-ordering wedge (PR #8209) landed, alongside catalog corrections for GLM and Qwen models, while a new image-to-image generation backend for MiniMax and xAI's migration to the Responses API signal continued multi-provider maturity.

---

## Releases

No new releases in the last 24 hours. Current version remains **0.84.2** (referenced in multiple issues).

---

## Hot Issues

1. **[#8029: Very slow performance on moving in prompt editor](https://earendil-works/pi/issues/8029)** — *OPEN, in progress*  
   With ~7,000 lines in the prompt buffer, a single arrow-key press takes 1,650ms. Growth is linear with buffer size. Community members flagged this as a blocker for long-form code review workflows; no fix has landed yet.

2. **[#8061: Context budget ignores maxTokens output reservation](https://earendil-works/pi/issues/8061)** — *OPEN*  
   A 400 error occurs at only 78% input usage because the context window doesn't reserve space for output tokens. The compact-and-retry recovery **fails again for the same reason**, making the failure unrecoverable. One of the most impactful correctness bugs open.

3. **[#8166 / #8210: Custom message injected mid-tool-batch corrupts tool_calls ordering](https://earendil-works/pi/issues/8166)** — *CLOSED (fix in #8209)*  
   `sendCustomMessage(triggerTurn: false)` while streaming bypasses the queue and pushes directly to the live message array, breaking tool→tool_calls adjacency on the next turn. Results in a permanent 400 wedge on DeepSeek/Moonshot. Confirmed independently by two reporters; fix merged.

4. **[#7870: Remote catalog silently overrides correct contextWindow for GLM-5.2](https://earendil-works/pi/issues/7870)** — *OPEN, in progress*  
   The pi.dev overlay pins `z-ai/glm-5.2` to 262k instead of the real 1M context. Users are forced to work around a bad remote default that overrides the correct built-in value.

5. **[#8198: pi.dev provider catalog endpoint times out](https://earendil-works/pi/issues/8198)** — *OPEN*  
   Catalog refreshes consistently time out; direct curl requests return no headers/body. Intermittent TLS acceptance with zero bytes (recurrence of #8065). Fix in PR #8204 adds per-attempt timeouts and retries.

6. **[#6300: Windows input line redrawn on every keystroke](https://earendil-works/pi/issues/6300)** — *OPEN*  
   On Windows 10, each character appears on a new line in the input box. Long-standing TUI regression affecting cmd.exe and Windows Terminal users; 7 comments over 6 weeks with no resolution.

7. **[#5023: Terminal scrolls to beginning without reason](https://earendil-works/pi/issues/5023)** — *CLOSED*  
   Random scroll-to-top during model work, followed by rapid scroll to end. High comment count (14) despite low 👍 count — a classic "everyone hits it, no one loves it" bug. Now closed, presumably fixed.

8. **[#5581: Custom messages with triggerTurn bypass before_agent_start](https://earendil-works/pi/issues/5581)** — *OPEN, in progress*  
   `sendMessage({ triggerTurn: true })` calls `_runAgentPrompt` directly, skipping the `before_agent_start` event. Breaks extension hooks that gate on that event, including secret-injection and guardrail logic.

9. **[#8208: Replayed history emits orphaned reasoning items → 400](https://earendil-works/pi/issues/8208)** — *CLOSED*  
   Long sessions via `openai-responses` can emit consecutive/orphaned `reasoning` items with an `unknown_parameter: status` field, rejected before reaching the provider. Gateway logs show input token validation failure at index 273.

10. **[#8075: Kimi cached_tokens not tracked as cache-read](https://earendil-works/pi/issues/8075)** — *CLOSED*  
    Kimi's top-level `usage.cached_tokens` was counted as normal input, inflating usage stats and truncating context prematurely. Fixed in PR #8119.

---

## Key PR Progress

1. **[#8209: Defer non-turn custom messages to end of turn while streaming](https://earendil-works/pi/pull/8209)** — *Merged*  
   Fixes #8166/#8210. Routes `triggerTurn: false` messages through the streaming queue instead of raw pushes. Critical session-integrity fix that unblocks DeepSeek and Moonshot users.

2. **[#8119: Track Kimi cached tokens](https://earendil-works/pi/pull/8119)** — *Merged*  
   Treats `usage.cached_tokens` as cache-read input. Prevents misreported token counts and premature compaction triggers.

3. **[#8124: Route xAI models through Responses; default to Grok 4.6](https://earendil-works/pi/pull/8124)** — *Merged*  
   Migrates xAI from completions to the Responses API, updates default model, and sends a user agent identifying Pi. Aligns with xAI's current API surface.

4. **[#8204: Retry hung pi.dev catalog refreshes](https://earendil-works/pi/pull/8204)** — *Merged*  
   Adds per-attempt timeouts and retry logic for over-slow catalog fetches. Addresses the recurring TLS-accept-no-bytes hang.

5. **[#8218: getStats tokens.total = billable only (exclude cache)](https://earendil-works/pi/pull/8218)** — *Merged*  
   Cache tokens are billed at ~1/120th of input rate; including them inflated totals ~120×, causing compaction budgets to trigger ~120× too early. Meaningful fix for users on cache-heavy workloads.

6. **[#8193: Add image-to-image generation for MiniMax](https://earendil-works/pi/pull/8193)** — *Merged*  
   Adds a `minimax-images` API module and registers it in the runtime images registry. Unblocks reference-image workflows on the MiniMax backend.

7. **[#8217: Add Kiro OAuth device login](https://earendil-works/pi/pull/8217)** — *Merged*  
   Introduces a new provider with device-code flow, including authorization_pending/slow_down handling and regression coverage.

8. **[#8076: DRAFT — dev branch with new harness](https://earendil-works/pi/pull/8076)** — *Closed without merge*  
   Open for 3 days, then closed. No summary or discussion; likely superseded or abandoned internally.

9. **[#8219: Test PR](https://earendil-works/pi/pull/8219)** — *Closed without merge*  
    "Please ignore." Community hygiene.

10. **[#8157-related: Migrate grok-mermaid → lovely-mermaid](https://earendil-works/pi/issues/8157)** — *Open issue (no PR yet)*  
    Not a PR, but the community discussion around replacing the inherited grok-mermaid renderer with the more maintained lovely-mermaid is actively shaping the roadmap. Expect a PR soon.

---

## Feature Request Trends

- **Provider catalog governance** — Three separate issues (#7870, #8194, #8206) call for stricter catalog validation: correct context windows, proper endpoint routing (OpenAI vs Anthropic), and unified catalogs across regional variants. The remote overlay overriding local correct values is a recurring pain.

- **Model coverage completeness** — Requests to add missing models (GLM-4.6V vision, GLM-5.3 thinking levels) and unify catalogs across CN/intl variants indicate the community is actively pushing Pi's built-in catalog to keep pace with provider releases.

- **Extension API depth** — Three requests this cycle: `agent_end` veto power to block turn settlement, RPC access to slash-command argument completions, and validation/defaulting for tool parameter schemas in plain-JS extensions. The message says "the plugin surface is stabilizing; now we want more control."

- **TUI ergonomics** — Dictation/IME live-layout (#8211) and the prompt-editor performance work (#8029) show that a subset of users now uses Pi as their primary editor surface, not just an assistant. Expect more latency and input-method requests.

---

## Developer Pain Points

- **Remote catalog as a single point of failure** — pi.dev timeout (#8198) + silent override (#7870) + regional catalog drift (#8194) form a cluster: the catalog is becoming the most fragile subsystem. Developers are blocked on refresh hangs and misconfigured models daily.

- **Session wedge after custom-message injection** — The #8166/#8210 cluster produced permanent 400s requiring session restart. Any extension using `sendCustomMessage(triggerTurn: false)` was at risk. The merged fix is reassuring but the pattern (raw array pushes bypassing the queue) suggests deeper state-management fragility.

- **Context budget math is opaque** — #8061 shows output-token reservation is ignored and retry logic fails for the same reason. A 400 at 78% input with no recoverable path is a trust-breaking bug for long-running agent sessions.

- **Windows TUI regressions persist** — #6300 (redraw every keystroke) has been open for six weeks with no fix. Windows users are a visible second-class constituency for the TUI.

- **Performance cliffs at scale** — The 1,650ms arrow-key press at 7,000 lines (#8029) and the 120× token-billing inflation from cache tokens (#8218) both hit only at scale, but that's exactly where Pi's automation value concentrates. Both are now addressed or in progress.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-17

## 1. Today's Highlights

The Qwen Code team continues aggressive hardening of the `/review` subsystem, with multiple PRs addressing worktree concurrency locking and verifier probe isolation, alongside a new `capture-tui` command that produces pixel-level rendering evidence. A cluster of multi-agent team bugs reported by community member `netbrah` — including task delivery failures and prompt/runtime contradictions — has driven a rapid PR response from maintainers and external contributors alike. Infrastructure stability work includes a Web Shell boot fallback to eliminate white-screens and a narrowed CI workspace wipe to prevent accidental deletion of git history on self-hosted runners.

## 2. Releases

Two preview releases shipped in the last 24 hours, both incremental:

- **[v0.21.12-preview.5](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.12-preview.5)**: Latest preview on the v0.21.12 branch.
- **[v0.21.11-nightly.20260816.5677823abb](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.11-nightly.20260816.5677823abb)**: Nightly with a notable change — `feat(autofix)` introducing a deny-by-default footprint gate and positional window censuses by @wenshao, plus a Web Shell fix.

Additionally, two DSW EAS full E2E benchmark reruns (r2, r3) were published against Qwen-Ref v0.21.12, validating SWE-bench Verified (500) and Terminal-Bench 2.0 (89) performance.

## 3. Hot Issues

1. **[#9276 — Team members cannot send ordinary messages to their leader](https://github.com/QwenLM/qwen-code/issues/9276)**
   Critical multi-agent bug: status/completion messages from team members are mistreated as shutdown requests (`Only the team leader can request shutdowns`). The error is confusing and blocks basic leadership communication in team mode.

2. **[#9282 — Manual team task assignment persists without dispatching work](https://github.com/QwenLM/qwen-code/issues/9282)**
   Leader-assigned `in_progress` tasks with explicit owners never reach the named teammate — only unowned `pending` tasks trigger delivery. This silently swallows assignments, rendering the leader's authority inert. Deserves attention; a fix PR (#9288) is already moving.

3. **[#9283 — Agent-team prompts contradict automatic delivery and promise unavailable peer summaries](https://github.com/QwenLM/qwen-code/issues/9283)**
   A documentation/behavior mismatch: runtime auto-forwards final answers when a teammate goes idle, but prompts tell agents to call `send_message` explicitly. The catch-22 here is that no one knows whether to rely on the runtime or the docs. Fix PR #9284 is open.

4. **[#9290 — Interactive session crashes when opening an errored, incomplete agent-team tab](https://github.com/QwenLM/qwen-code/issues/9290)**
   A single render error inside an agent-team tab exits the entire interactive session — there's exactly one FATAL boundary around the whole app. Containment PR #9292 is already submitted.

5. **[#9089 — PAT-bearing jobs share a host with untrusted branch code: needs runner-level isolation](https://github.com/QwenLM/qwen-code/issues/9089)**
   Maintainer-flagged security gap: GitHub Actions steps with PAT credentials run on the same persistent-pool host as untrusted branch code. This cannot be fixed inside a step; it requires runner-level isolation. Design is being executed via the ephemeral-container work in #9214.

6. **[#9291 — Unsupported image MIME can abort a Responses-compatible session](https://github.com/QwenLM/qwen-code/issues/9291)**
   A `.heic` attachment crashes the session when forwarded to a Responses-compatible endpoint as an `image/heic` data URI. Edge case, but a full session abort on input MIME is harsh.

7. **[#9250 — `qwen serve` host writer hard-codes new-file mode 0600, ignores umask](https://github.com/QwenLM/qwen-code/issues/9250)**
   The daemon's `write_file`/`edit` tools create files with 0600 unconditionally, ignoring the process umask and offering no configuration escape hatch. Community contributor flags a missing settings key.

8. **[#8962 — cannot use qwen under tmux](https://github.com/QwenLM/qwen-code/issues/8962)**
   A long-standing usability complaint: severe flicker/lag under tmux and remote sessions makes the UI practically unusable; shrinking the terminal to 400×300 mitigates. Clearly rendering-related and still open.

9. **[#9253 — Web Shell dev tabs white-screen after dev-server/daemon restarts](https://github.com/QwenLM/qwen-code/issues/9253)**
   Long-open Web Shell dev tabs (localhost:5173) go entirely white after a Vite restart with no error and no recovery UI. Fixed by PR #9254's boot watchdog.

10. **[#9278 — Design: /review publish-time convergence advisory](https://github.com/QwenLM/qwen-code/issues/9278)**
    A maintainer-led design tracking a "runaway loop" problem: push-triggered review → findings → agent fixes → larger diffs → more findings. The current 5-round cap exists only as prose in `AGENTS.md`, which is unreliable. This issue formalizes telemetry and operator-owned posting surfaces.

## 4. Key PR Progress

1. **[#9211 — fix(review): lock the PR review worktree lease against concurrent sessions](https://github.com/QwenLM/qwen-code/pull/9211)**
   Addresses #9205 where fixed-path worktrees (`.qwen/tmp/review-pr-<n>`) got deleted mid-run by concurrent reviews of the same PR. The lease now doubles as a lock, checked before destructive operations. Essential for safe parallel review.

2. **[#9221 — fix(review): run verifier probes in a private scratch worktree](https://github.com/QwenLM/qwen-code/pull/9221)**
   The verifier agent (the only *writing* agent in review) previously landed probe files in the shared review worktree. This moves probes to a private scratch worktree to prevent read-write contamination of the tree every other agent pins to.

3. **[#9273 — feat(review): capture-tui — rendering claims get pixels, not prose](https://github.com/QwenLM/qwen-code/pull/9273)**
   New `qwen review capture-tui` command: runs a command in a private tmux server, captures pane text (`<out>.ans` always) and PNG renders when `freeze` is available. Verifiers can now produce visual evidence instead of prose claims — a welcome quality leap.

4. **[#9214 — feat(autofix): run the verification gate in an ephemeral container](https://github.com/QwenLM/qwen-code/pull/9214)**
   Phase 1 + 2 of the #9089 security design: both verification gate steps move inside an ephemeral container, and the trust boundary is pinned with a structural test. Directly addresses the PAT/untrusted-code isolation gap.

5. **[#9288 — fix(team): reliably deliver leader-assigned tasks](https://github.com/QwenLM/qwen-code/pull/9288)**
   Fixes #9282: stores canonical teammate ownership, invalidates stale delivery state inside the task mutation boundary, and retries idle teammates. Delivers named assignments exactly once.

6. **[#9284 — fix(core): align agent-team prompts and TeamCreate description with actual delivery](https://github.com/QwenLM/qwen-code/pull/9284)**
   Fixes #9283 (prompt/reality divergence). Keeps scope tight per the issue: no new observability features, just accurate prompts and `TeamCreate` descriptors.

7. **[#9292 — fix(cli): contain agent-tab render errors instead of exiting the session](https://github.com/QwenLM/qwen-code/pull/9292)**
   Fixes #9290's containment half: adds an error boundary around agent-tab rendering so a failure degrades the tab, not the whole session. Note: the root-throw question remains open.

8. **[#9254 — fix(web-shell): show a boot fallback instead of a white screen](https://github.com/QwenLM/qwen-code/pull/9254)**
   Adds a dependency-free boot watchdog to `index.html`. If a script or stylesheet fails to load, it immediately renders a theme-aware bilingual fallback with the captured error and a reload button. Directly addresses #9253.

9. **[#9228 — fix(ci): narrow serve-ab's self-hosted wipe to the A/B checkout dirs](https://github.com/QwenLM/qwen-code/pull/9228)**
   Fixes a dangerous CI footgun: the self-hosted ECS pool's workspace wipe deleted the **entire** shared workspace including root `.git` (~900 MB history), forcing full re-clones. Narrowed to the A/B checkout dirs only.

10. **[#9226 — feat(review): Aone Code read path (second review-platform provider)](https://github.com/QwenLM/qwen-code/pull/9226)**
    Implements the second provider behind the review-platform seam introduced in #9096. Detects clones from `gitlab.alibaba-inc.com` and enables existing read subcommands (`meta`, `is…`) for Aone Code — expanding review beyond GitHub.

## 5. Feature Request Trends

- **Multi-agent team reliability and observability**: The dominant thread this week. Users want leaders to assign work that actually delivers, accurate prompt/runtime alignment, and crash containment when a teammate errors. Expect more work on delivery guarantees and team state inspection.
- **Review subsystem tooling**: Maintainers are driving this: worktree locking, scratch-tree verifier probes, capture-tui rendering evidence, Aone Code provider, and convergence advisory telemetry. The `/review` pipeline is becoming a first-class product on its own.
- **Authentication breadth**: [#9275](https://github.com/QwenLM/qwen-code/issues/9275) requests GitHub Copilot sign-in via `/auth` — a practical ask as Copilot subscription holders want to reuse credentials.
- **Ecosystem extension**: [#9294](https://github.com/QwenLM/qwen-code/issues/9294) proposes a README entry for ClawMetry, a local observability dashboard with a Qwen Code adapter. Community building around the tool is actively growing.
- **Daemon/serve configuration surface**: [#9250](https://github.com/QwenLM/qwen-code/issues/9250) (file mode 0600) and other serve-related issues point to demand for more daemon-side configuration knobs.

## 6. Developer Pain Points

- **Multi-agent messaging and delivery is confusing at best, broken at worst**: Three separate bugs (#9276, #9282, #9283) center on leadership signaling and task delivery — a clear signal that team mode semantics need a coherence pass, not piecemeal fixes.
- **Session fragility**: A single render error in a tab can kill the entire interactive session (#9290); Web Shell tabs white-screen after dev-server restarts (#9253); oversized SSE frames crash browser tabs (#9234). Stability around session lifecycle and UI rendering is a recurring theme.
- **tmux/remote usability**: [#8962](https://github.com/QwenLM/qwen-code/issues/8962) remains open — rendering flicker under tmux makes the tool effectively unusable for remote workers. A P3-label, but community sentiment suggests it hurts adoption.
- **CI infra footguns**: The serve-ab workspace wipe destroying git history (#9228) and repeated CI failure noise from E2E tests (#9143) suggest the self-hosted CI fleet still needs operational polish.
- **Review process overhead**: Heavy process discipline around "deferred suggestion" issues and 5-round caps shows the review loop is effective but top-heavy — contributors may find the process overhead steep for small PRs. The triage-only route for non-functional PRs (#9193) is a step toward balancing this.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-17

---

## 1. Today's Highlights

The project has formally rebranded to **CodeWhale** (formerly DeepSeek-TUI), with v0.9.8 released and the legacy `deepseek-tui` npm package deprecated. This week's focus is on stability: fixing sandbox regressions (bwrap on Linux, read-only shell policies for subagents), resolving wide-terminal layout issues (#5436), and addressing a critical crash report in v0.9.7 (#5424). Maintainer activity is high, with 42 open/updated issues and 42 PRs in the last 24 hours, including a new Claude Code parity design document and substantial i18n expansion.

---

## 2. Releases

### v0.9.8
> **Codewhale** is now the public product name from Shannon Labs. The `codewhale` command, npm package, and release-asset names remain lowercase technical identifiers. **The legacy npm package `deepseek-tui` is deprecated** and receives no further releases. Users coming from v0.8.x legacy `deepseek` / `d...`

**Key changes:**
- Formal rebrand from DeepSeek-TUI to CodeWhale
- Legacy npm package deprecated
- Migration path for v0.8.x users (implied, details truncated)

🔗 [Release v0.9.8](https://github.com/Hmbown/DeepSeek-TUI/releases)

---

## 3. Hot Issues

### 🔥 #5424 — v0.9.7: Codewhale TUI crashing (5 comments)
**Reported by Hixac** — After prompting and waiting ~1 minute, `codewhale` exits by itself. Reproducible with `codewhale --continue`. This is the top-crash report for the latest release and likely urgent.
🔗 [Issue #5424](https://github.com/Hmbown/CodeWhale/issues/5424)

### 🔥 #5123 — Agent spawn surface has too many knobs — labeled builder runs read-only and self-BLOCKED (6 comments)
**Reported by Hmbown (dogfood)** — A delegate labeled `builder` / `gates-shell-writer` ships with a **read-only** tool contract, causing `BLOCKED` failures. This is a systemic subagent role-mapping problem that impacts reliability of multi-agent workflows.
🔗 [Issue #5123](https://github.com/Hmbown/CodeWhale/issues/5123)

### 🔥 #5056 — Flaky verifier background tests: 12 untriaged `#[ignore]` tests (5 comments)
**Reported by Hmbown** — `run_verifiers_background_*` tests flake under full-suite parallelism. Workspace-sensitive fixtures complicate fixes. Blocks CI stability and new PRs.
🔗 [Issue #5056](https://github.com/Hmbown/CodeWhale/issues/5056)

### 🔥 #1917 — Universal PreToolUse/PostToolUse hook layer for Cancel/Pause/Resume (5 comments)
**Reported by aboimpinto** — Architectural proposal for a unified hook-based lifecycle across all action types. Community interest is high but implementation spans all subsystems.
🔗 [Issue #1917](https://github.com/Hmbown/CodeWhale/issues/1917)

### 🔥 #5322 — [CLOSED] Regression: output area doesn't fill wide terminals (5 comments)
**Reported by M-Maciej** — v0.9 caps transcript width at ~105 columns leaving dead space on wide displays. Closed via PR #5446 which adds `transcript.prose_measure` cap.
🔗 [Issue #5322](https://github.com/Hmbown/CodeWhale/issues/5322)

### 🔥 #2693 — HarnessPosture: model-specific context and subagent policy (6 comments)
**Reported by Hmbown** — DeepSeek V4 and Xiaomi MiMo v2.5 benefit from cache-heavy/prefix-stable starting prompts. Epic spans context assembly and subagent role tiers.
🔗 [Issue #2693](https://github.com/Hmbown/CodeWhale/issues/2693)

### ⚠️ #5436 — [CLOSED] Prose wraps at ~105 columns while tool cells full-width (0 comments)
**Reported by HmbownBown** — Transcript reads left-oriented on wide terminals. Closed by PR #5446 (full-width prose + configurable cap).
🔗 [Issue #5436](https://github.com/Hmbown/CodeWhale/issues/5436)

### ⚠️ #5403 — main is red on macOS + Windows: plugin_e2e_acceptance & NSIS provisioning (2 comments)
**Reported by Lstarsky0** — Four consecutive CI runs red on both platforms. Release-blocker for v0.9.9.
🔗 [Issue #5403](https://github.com/Hmbown/CodeWhale/issues/5403)

### ⚠️ #5426 — [CLOSED] v0.9.9: give scouts/reviewers a usable read-only shell (2 comments)
**Reported by Hmbown** — `ShellPolicy::ReadOnly` gates everything through a classifier built for parallel auto-approve chunks — too tight for live inspection. Fixed by PR #5438.
🔗 [Issue #5426](https://github.com/Hmbown/CodeWhale/issues/5426)

### ⚠️ #5410 — Allow configuring additional roots in the bwrap sandbox (1 comment)
**Reported by redstar** — Zig development fails under bwrap: `/dev/null` writes forbidden (EROFS) and system library linking breaks. Addresses a key crash for Linux users.
🔗 [Issue #5410](https://github.com/Hmbown/CodeWhale/issues/5410)

---

## 4. Key PR Progress

### 🚀 #5456 — [OPEN] feat(sandbox): bwrap container essentials + configurable extra roots
Fixes #5410 by mounting private `--dev /dev`, `--proc /proc`, and `--tmpfs /tmp` by default, plus new `bwrap_ro_roots` / `bwrap_rw_roots` config options.
🔗 [PR #5456](https://github.com/Hmbown/CodeWhale/pull/5456)

### 🚀 #5446 — [CLOSED] fix(tui): prose fills full content width; add `transcript.prose_measure` cap
Removes the hardcoded `PROSE_MAX_MEASURE = 105`, makes prose full-width by default, and exposes a configurable cap for users who prefer narrower reading rails.
🔗 [PR #5446](https://github.com/Hmbown/CodeWhale/pull/5446)

### 🚀 #5438 — [OPEN] fix(fleet): the scout posture gate must honor #5428's read-only shell
Fixes the #5426 regression where scouts were denied `git log`, `ls`, and other canonical inspection commands. Live-dogfood verified against a rebuilt binary.
🔗 [PR #5438](https://github.com/Hmbown/CodeWhale/pull/5438)

### 🚀 #5445 — [CLOSED] fix(integrations): carry Responses-dialect DSH routes via pi-ai
Fixes #5434 — the default DeepSeek route (`deepseek-v4-flash`, `endpoint_key: "responses"`) was refused. Adds multi-dialect route declarations.
🔗 [PR #5445](https://github.com/Hmbown/CodeWhale/pull/5445)

### 🚀 #5450 — [OPEN] fix(tui): restore session cost when live pricing is unverifiable
Session cost no longer stays stuck at `unverified_live_pricing` when the pricing endpoint returns 503. Supersedes #5402 with corrected co-author trailer.
🔗 [PR #5450](https://github.com/Hmbown/CodeWhale/pull/5450)

### 🚀 #5444 — [OPEN] fix(session): let `/rename` and `/title` apply mid-first-turn
Fixes #5430 — session metadata file isn't created until first-turn autosave, so mid-turn renames silently no-op. Now writes to the crash checkpoint correctly.
🔗 [PR #5444](https://github.com/Hmbown/CodeWhale/pull/5444)

### 🚀 #5449 — [CLOSED] docs(design): Claude Code parity reference
Comprehensive design doc covering Claude Code's Agent tool, Workflow tool (JS script API, journal replay, schema-forced returns), `/loop`, plugins/skills/agents/hooks, and single-Bash-tool design.
🔗 [PR #5449](https://github.com/Hmbown/CodeWhale/pull/5449)

### 🚀 #5454 — [OPEN] feat(web/i18n): add fr/de/ca/hi/tr/it/pl dictionaries (+ar with RTL plumbing)
Brings codewhale.net to parity with TUI locale packs — full key-parity dictionaries with native rewrites.
🔗 [PR #5454](https://github.com/Hmbown/CodeWhale/pull/5454)

### 🚀 #5401 — [OPEN] fix: CodeQL Highs (#107, #88–#106) and prepare GHSA-8hp3 / GHSA-3mgh
Security slice only: fixes clear-text logging, prepares GitHub Security Advisories. Does not tag or publish.
🔗 [PR #5401](https://github.com/Hmbown/CodeWhale/pull/5401)

### 🚀 #5457 — [OPEN] test(pty): deflake agent_focus auto-review receipt test
Fixes macOS CI flake in `auto_review_gates_a_workers_call_and_the_receipt_shows_in_focus` — Enter key didn't focus worker subagent frame.
🔗 [PR #5457](https://github.com/Hmbown/CodeWhale/pull/5457)

---

## 5. Feature Request Trends

| Direction | Evidence | Signal |
|---|---|---|
| **Configurable sandbox roots & permissions** | #5410 (bwrap roots), #5426 (read-only shell policy split) | High — Linux users hitting hard walls |
| **Model/provider-agnostic configuration** | #4660 (kimi-code-style custom providers), #4173 (de-hardcode registries), #2693 (HarnessPosture) | High — self-hosted and long-context models need per-model tuning |
| **Hook-based lifecycle / middleware layer** | #1917 (PreToolUse/PostToolUse), #1708 (tui_help tool) | Medium — community-proposed architecture |
| **i18n parity** | #5454 (web dictionaries), #5452 (README translations) | Medium — official push for multilingual support |
| **MCP capability metadata** | #4170 | Low — waiting on upstream spec support |
| **Configurable tool-result size limits** | #5367 — model-visible `read`/tool-result caps for self-hosted long-context models | Medium — closed but direction is clear |

---

## 6. Developer Pain Points

### 🐛 CI instability (highest frequency)
- #5056: Flaky verifier background tests, 12 untriaged `#[ignore]`
- #5403: `main` red on both platforms (plugin PTY hangs, NSIS provisioning)
- #4669: Coalesced raw-read test fails under full parallel CI
- #5457: PTY focus flake on macOS

### 🐛 Sandbox/permission friction
- #5123: Subagents labeled `builder` run read-only → self-BLOCKED
- #5426: Read-only shell classifier too tight for inspection commands
- #5410: bwrap denies `/dev/null` writes + system library linking
- #2617: SPM `swift test` fails inside sandbox (`sandbox-exec`)

### 🐛 Regression churn in v0.9.x
- #5424: TUI crash after ~1 minute wait
- #5322: Wide-terminal layout regression (fixed in #5446)
- #5413: `sudo` regression in wheel group
- #5436: Prose left-oriented on wide terminals (fixed)

### 🐛 Release-blocking operational friction
- #5299: npm publication gated on maintainer browser + 2FA (creds expired)
- #5403: CI red across platforms blocks merges
- #5288: Manual-deploy gap for website

---

*Generated 2026-08-17 from [github.com/Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI) activity.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*