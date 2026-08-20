# AI CLI Tools Community Digest 2026-08-20

> Generated: 2026-08-20 00:30 UTC | Tools covered: 9

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
**Date**: 2026-08-20 | **Scope**: Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code, OpenCode, Pi, Qwen Code, DeepSeek TUI

---

## 1. Ecosystem Overview

The AI CLI tool landscape is maturing rapidly, with nine major tools actively competing for developer mindshare. Windows support remains the single largest cross-platform pain point, appearing in the top issues of nearly every tool. Cross-tool standardization (AGENTS.md) is emerging as a dominant theme, with Claude Code's 4,654-upvote issue signaling strong community demand for portable context files. Security hardening is accelerating across the board — Codex removing Git from known-safe commands and multiple tools addressing sandbox enforcement and OAuth reliability. The ecosystem is bifurcating: established tools (Claude Code, Copilot CLI) emphasize stability and enterprise compliance, while newer tools (OpenCode, Pi) focus on rapid feature iteration and provider flexibility. Automation reliability and session-state durability are universal concerns, with users demanding crash-safe behavior and transparent failure modes.

---

## 2. Activity Comparison

| Tool | Issues (24h) | PRs (24h) | Release Status |
|------|-------------|-----------|----------------|
| **Claude Code** | 10 hot, 1 new | 1 updated | v2.1.236 (stable) |
| **OpenAI Codex** | 10 hot | 10+ merged (bot batch) | rust-v0.149.0-alpha.1/2 |
| **Gemini CLI** | 10 tracked | 10 open/merged | v0.56.0 + v0.57.0-preview.0 |
| **GitHub Copilot CLI** | 10 hot | 0 (direct commits) | v1.0.81-2 through -5 (4 patches) |
| **Kimi Code** | 1 updated | 0 | No new (v0.37.1 latest) |
| **OpenCode** | 10 hot | 12 merged | No new release |
| **Pi** | 10 hot (25+ total) | 10 (7 closed, 3 open) | No new (v0.84.2 latest) |
| **Qwen Code** | 10 tracked | 10 open | v0.21.14 + preview/nightly |
| **DeepSeek TUI** | 10 tracked | 10 (7 closed, 3 open) | v0.9.10 upcoming (PR #5513) |

**Release velocity ranking**: Copilot CLI (4 patches/day) > Qwen Code (3 builds) > Gemini CLI (2 releases) > Codex (2 alphas) > Claude Code (1 stable) > Others (none).

---

## 3. Shared Feature Directions

| Theme | Tools | Specific Needs |
|-------|-------|----------------|
| **Cross-tool context standardization** | Claude Code, Codex, Cursor (referenced) | AGENTS.md as universal context file; CLAUDE.md seen as too tool-specific |
| **Windows first-class support** | Claude Code (ARM VM, crashes), Codex (6/10 top issues), Pi (keybindings, paths, BOM), Copilot CLI (sandbox+git) | Process lifecycle, auth persistence, terminal compatibility, path handling |
| **Sandbox/user-control balance** | Copilot CLI (can't disable), Claude Code (permission bypass), Gemini CLI (DEBUG flag semantics) | Deterministic sandbox behavior; no implicit overrides; clear enforcement boundaries |
| **Session-state durability** | DeepSeek TUI (approval persistence), Pi (session-scoped model settings), Qwen Code (identity anchoring), Copilot CLI (persistent config) | Survive interruptions; crash-safe design; session naming/resume; compaction resilience |
| **OAuth/token reliability** | Claude Code (24h expiry, re-login loops), Codex (auth loss), Copilot CLI (GHEC endpoints), Gemini CLI (Workstations OAuth) | Long-lived sessions; graceful refresh; tenant-aware endpoints |
| **MCP integration stability** | Codex (OAuth issuer overrides), Copilot CLI (Atlassian broken), Gemini CLI (consent prompts), Kimi Code (ACP) | Per-server auth config; process reaping; capability detection |
| **Billing/usage transparency** | OpenCode (5+ reports), Claude Code (rate limits on multi-agent) | Cache-read visibility; accurate metering; quota auditability |
| **Compaction/context reliability** | Qwen Code (incorrect compression), Codex (image payload loops), Copilot CLI (lossy summarization), DeepSeek TUI (early triggers) | Predictable triggers; token accounting; artifact preservation |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code |
|-----------|------------|--------------|------------|-------------|----------|-----|-----------|
| **Primary focus** | Enterprise workflow depth | Sandbox security & cross-platform parity | Agent reliability & eval rigor | Enterprise compliance & CI integration | Plugin ecosystem & TUI UX | Provider flexibility & extension API | CI/CD automation & multi-agent |
| **Target user** | Teams, remote workflows | Power users, multi-agent | Developers on Google Cloud | Enterprise GitHub shops | Plugin developers | Local/self-hosted model users | CI pipelines, SWE-bench runners |
| **Model strategy** | Anthropic models only | OpenAI models | Gemini models | GitHub models | Provider-agnostic (Go sub) | Provider-agnostic | Provider-agnostic (Qwen default) |
| **Technical approach** | Mature, stable releases | Rust runtime, aggressive security | Eval-driven, component testing | Rapid patches, stable core | V2 rewrite, plugin focus | Session-scoped state, catalog-driven | Live-session registry, verifier rigor |
| **Windows maturity** | Poor (ARM, crashes) | Poor (6 top issues) | Moderate | Moderate (sandbox git issues) | Moderate | Poor (path/BOM issues) | Moderate |

**Key differentiators**:
- **Claude Code** leads in community engagement (4,654-upvote AGENTS.md issue) and enterprise features (remote-control, scheduled tasks).
- **OpenAI Codex** is investing most aggressively in security (Git command hardening, plugin isolation) but struggles with Windows parity.
- **Pi** uniquely targets self-hosted model users with catalog metadata management and timeout fixes for long-thinking local models.
- **Qwen Code** differentiates with CI/CD focus (SWE-bench verification lanes, autofix workflows) — no other tool mentions SWE-bench in its releases.
- **Kimi Code** is notably quiet — lowest activity, suggesting a maintenance phase or team reallocation.

---

## 5. Community Momentum & Maturity

| Tool | Community Signal | Momentum |
|------|-----------------|----------|
| **Claude Code** | 4,654 upvotes on AGENTS.md; multiple 100+ upvote issues | **Highest momentum** — active release train, huge issue engagement |
| **OpenAI Codex** | 78 comments on Windows browser issue; 34 reactions on Luna subagents | **Rapid iteration** — two alphas in 24h, aggressive automation |
| **Gemini CLI** | P1 issues on subagent reliability; eval epic (76 tests) | **Steady** — structured triage, active maintainer engagement |
| **Copilot CLI** | 4 patches in 24h; sandbox backlash (7+ upvotes on config override) | **High velocity but reactive** — fixing regressions from own release |
| **Kimi Code** | Single issue of limited engagement | **Quiet/Maintenance** — likely resource-constrained |
| **OpenCode** | 56 upvotes on silent failure issue; 12 PRs in 24h | **Strong contributor momentum** — V2 build-out active |
| **Pi** | 13 upvotes on session-scoping; 25+ issues/24h | **Growing** — active community, maintainer-driven improvements |
| **Qwen Code** | Mostly P1/P2 issues with few upvotes | **Feature-focused** — CI infrastructure investment |
| **DeepSeek TUI** | 76-commit release lane; i18n volunteer base | **Community-backed** — responsive to Chinese user base |

**Maturity assessments**:
- **Most mature**: Claude Code, Copilot CLI — stable APIs, enterprise features, predictable releases.
- **Rapidly maturing**: Codex, OpenCode — aggressive feature development with security hardening.
- **Growing pains**: Gemini CLI, Pi — subagent reliability and platform gaps still being solved.
- **Emerging**: Qwen Code, DeepSeek TUI — specialized use cases (CI, localization) with smaller communities.

---

## 6. Trend Signals

### For AI CLI tool developers:

1. **Cross-tool interoperability is non-negotiable.** The AGENTS.md movement (4,654 upvotes) and ACP sessions (Kimi) signal that the era of siloed tool-specific context files is ending. Tools that don't adopt open standards will face migration pressure.

2. **Windows parity is the next battleground.** Six of Codex's top ten issues are Windows-specific; Claude Code's ARM VM failure blocks an entire architecture; Pi's BOM handling breaks configs silently. Tools that crack Windows reliability (process lifecycle, path handling, auth persistence) gain a differentiation edge.

3. **Sandbox enforcement must respect user intent.** Copilot CLI's sandbox override backlash (config says disabled but sandbox forces on) and Claude Code's bashFirst bypassing permission tracking both describe the same failure: tools deciding policy over users. The trend is toward deterministic, documented behavior with clear failure modes.

4. **Silent failures are the most expensive bugs.** OpenCode's aborted streams recorded as clean stops (56 upvotes), Gemini's MAX_TURNS reported as success, and Qwen's `ask_user_question` returning decline without showing the question — all erode trust. Surfacing errors loudly is a feature, not a nuisance.

5. **Billing transparency is emerging as a trust boundary.** OpenCode's cache-read billing gap (4+ reports of meter divergence) and Claude Code's rate-limit mismatches on multi-agent workflows indicate users want auditability before scaling agent usage. Expect billing dashboards to become a standard feature.

6. **Session-state durability is moving from nice-to-have to core.** DeepSeek's crash-safe approvals, Pi's session-scoped model settings, Qwen's prompt-identity anchoring — all point toward treating sessions as first-class persistent objects with crash recovery, not ephemeral terminal interactions.

7. **Context/compaction engineering is the new performance frontier.** Tools that solve predictable compaction (Qwen's incorrect compression, Codex's image loops, Copilot's lossy summarization) will win long-running workflow use cases. The current state is heuristic and unreliable across all tools.

8. **Automation trust requires observability.** Scheduled task self-disabling (Codex), silent auto-update failures (Claude Code), and opaque CI wedge states (Qwen) — users want to know *why* something stopped, not just that it stopped. Post-mortem context (Gemini's GCS trajectory logging, Qwen's witness forms) is the direction.

---

*Report generated from community digest data for 2026-08-20. All metrics reflect activity within the preceding 24-hour window unless otherwise noted.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-08-20 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

### 1.1 skill-creator Evaluation Fix (PR #1298)
**Status:** Open | **Author:** MartinCajiao | [GitHub](https://github.com/anthropics/skills/pull/1298)

This PR addresses a critical bug where `run_eval.py` consistently reports `recall=0%`, rendering the description-optimization loop ineffective. The fix installs the eval artifact as a functional skill, resolves Windows stream-reading issues, and improves trigger detection. It directly resolves issue #556, which has 12 comments and 7 upvotes — the most discussed issue-pair in the repository. The PR consolidates fixes from #1099 and #1050.

### 1.2 document-typography Skill (PR #514)
**Status:** Open | **Author:** PGTBoos | [GitHub](https://github.com/anthropics/skills/pull/514)

A quality-control skill preventing common typographic defects in AI-generated documents: orphan word wraps, widow paragraphs, and numbering misalignment. The community's strong engagement reflects the universal pain point of AI-generated documents containing minor-but-visible formatting defects. The proposed skill applies to all document-generation workflows regardless of output format.

### 1.3 ODT Skill (PR #486)
**Status:** Open | **Author:** GitHubNewbie0 | [GitHub](https://github.com/anthropics/skills/pull/486)

Adds OpenDocument Format support for `.odt` and `.ods` files, covering creation, template filling, and conversion to HTML. The discussion highlights demand for open-format document skills beyond the existing docx/pdf coverage. Includes trigger terms for LibreOffice and ISO-standard document requests.

### 1.4 ServiceNow Platform Skill (PR #568)
**Status:** Open | **Author:** Vanka07 | [GitHub](https://github.com/anthropics/skills/pull/568)

A comprehensive ServiceNow platform skill covering ITSM, ITOM, ITAM/SAM, FSM, HRSD/CSM, SPM/PPM, vulnerability response, and IntegrationHub. The discussion reflects interest in enterprise platform skills spanning multiple modules and the need for broad contextual knowledge rather than narrow scripting helpers.

### 1.5 self-audit Skill (PR #1367)
**Status:** Open | **Author:** YuhaoLin2005 | [GitHub](https://github.com/anthropics/skills/pull/1367)

Introduces a two-phase quality gate: mechanical verification of output files first, followed by a four-dimension reasoning audit in damage-severity priority. Positioned as model-agnostic and stack-independent. The discussion centers on quality assurance patterns applicable across all skill outputs, complementing the companion proposal in issue #1385.

### 1.6 DOCX Tracked Changes w:id Fix (PR #541)
**Status:** Open | **Author:** Lubrsy706 | [GitHub](https://github.com/anthropics/skills/pull/541)

Fixes document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks, caused by shared `w:id` space collisions in OOXML. The discussion provides valuable OOXML internals guidance for any future document-manipulation skill development.

### 1.7 testing-patterns Skill (PR #723)
**Status:** Open | **Author:** 4444J99 | [GitHub](https://github.com/anthropics/skills/pull/723)

A comprehensive testing-patterns skill covering the Testing Trophy model, unit testing (AAA pattern, naming conventions, edge cases), React component testing with Testing Library, and related strategies. Reflects demand for structured engineering guidance rather than tool-specific recipes.

### 1.8 frontend-design Skill Improvements (PR #210)
**Status:** Open | **Author:** justinwetch | [GitHub](https://github.com/anthropics/skills/pull/210)

Revises the frontend-design skill to ensure every instruction is actionable within a single conversation, improving specificity to steer behavior without being overly restrictive. The discussion highlights the design tension between skill granularity and conversational applicability.

---

## 2. Community Demand Trends

### Critical infrastructure reliability
Issue #556 (7 👍, 12 comments) — `run_eval.py` never triggers skills, reporting 0% recall — is the highest-signal demand: contributors need the skill evaluation loop to actually work before new skills can be quality-gated.

### Trust and security enforcement
Issue #492 (43 comments, 2 👍) on community skills distributed under the `anthropic/` namespace is the most active issue overall. The community demands clear provenance and trust boundaries to avoid impersonation and permission escalation risks.

### Enterprise document workflows
Multiple discussions (ODT, DOCX corruption, SharePoint Online concerns from issue #1175) all point toward a broader need: reliable, round-trip-safe document manipulation across every major format — with particular emphasis on open/ISO standards and preserving document integrity.

### Quality assurance and safety
Issues #412 and #1385, plus the self-audit PR, signal growing demand for governance and verification skills: audit trails, adversarial review, policy enforcement, and pre-delivery verification.

### Organizational skill management
Issue #228 (16 comments, 8 👍) — the most-upvoted issue — demands org-wide skill sharing in Claude.ai. The manual download/upload workflow is a clear bottleneck for enterprise adoption.

### Context-window efficiency
Issue #1487 reports the `claude-api` skill injecting ~156k tokens in a single call — community concern over skill designs that exhaust context window, particularly for bundled or auto-injected skills.

---

## 3. High-Potential Pending Skills

The following PRs have active discussion and are not yet merged — they may land in the near term:

| # | Skill | Function | Highlight |
|---|-------|----------|-----------|
| [PR #514](https://github.com/anthropics/skills/pull/514) | **document-typography** | Typographic QC for generated documents | Strong discussion on universal formatting pain points |
| [PR #486](https://github.com/anthropics/skills/pull/486) | **ODT** | OpenDocument creation/filling/conversion | Complements docx/pdf skills; fills an open-format gap |
| [PR #723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | Full-stack testing guidance | Comprehensive engineering-practice coverage |
| [PR #568](https://github.com/anthropics/skills/pull/568) | **ServiceNow** | Enterprise platform skill | Broad multi-module enterprise platform template |
| [PR #525](https://github.com/anthropics/skills/pull/525) | **pyxel** | Retro game development via MCP | Unique creative+mcp hybrid pattern |
| [PR #1367](https://github.com/anthropics/skills/pull/1367) | **self-audit** | Mechanical + reasoning verification | Addresses quality-gate demand from #1385 |

All are marked OPEN; none appear to have been superseded by earlier merged versions.

---

## 4. Skills Ecosystem Insight

The community's single most concentrated demand is **developer infrastructure trust**: fixing the broken skill-evaluation loop (so skills can be reliably quality-checked) and enforcing namespace/security boundaries (so community skills can be safely adopted) — with document format reliability and enterprise sharing as close secondary demands, the ecosystem's true priority is making existing skills *trustworthy and operational before expanding the catalog*.

---

# Claude Code Community Digest — 2026-08-20

## Today's Highlights
Release v2.1.236 introduces the long-requested `ANTHROPIC_DEFAULT_MODEL` environment variable plus cross-session `SendMessage` notifications. Community sentiment is dominated by the now-closed AGENTS.md feature request (#6235), which accumulated 4,654 upvotes and 360 comments, signaling a strong push for cross-tool standardization. A cluster of new bugs around auto-mode's "bashFirst" prompt strategy is gaining traction, indicating a systemic issue with tool selection in permission-free workflows.

## Releases
**v2.1.236** — [Release Link](https://github.com/anthropics/claude-code/releases)
- Added `ANTHROPIC_DEFAULT_MODEL` environment variable: sets the model new sessions start on; `/model` pick overrides it and persists across restarts (unlike `ANTHROPIC_MODEL`)
- Added `notify_when_idle` to cross-session `SendMessage`: enables one Claude Code session to notify another when idle

No other releases in the last 24 hours.

## Hot Issues

1. **[#6235 — [CLOSED] Support AGENTS.md**](https://github.com/anthropics/claude-code/issues/6235) — *4,654 👍 / 360 comments*. The highest-signal issue in Claude Code history. Community demands alignment with the emerging AGENTS.md cross-tool standard (adopted by Codex, Amp, Cursor). CLAUDE.md is seen as too tool-specific for multi-agent collaboration. Closed status likely indicates a decision or upcoming implementation — worth watching the changelog.

2. **[#77136 — Opus 4.8/5.0 model behavior complaints**](https://github.com/anthropics/claude-code/issues/77136) — *195 👍 / 29 comments*. Users report Opus 4.8's language is "incessantly toxic" while Opus 5.0 produces incoherent output. High upvote count suggests broad dissatisfaction with recent model tuning, not just an isolated experience.

3. **[#32479 — GitHub Connector not recognized by Claude Code**](https://github.com/anthropics/claude-code/issues/32479) — *140 👍 / 89 comments*. Long-running integration bug: GitHub Connector works in Claude Desktop but fails in Claude Code sessions. High engagement indicates many users rely on this workflow for repo context.

4. **[#88041 — Auto-mode "bashFirst" instructs sed/heredoc edits**](https://github.com/anthropics/claude-code/issues/88041) — *New*. Auto-mode's system prompt pushes shell-based file editing over native Edit/Write tools. This silently breaks `/rewind` and permission tracking — a serious correctness issue for the auto-permission workflow.

5. **[#87575 — Auto mode causes /rewind to silently fail on Bash-edited files**](https://github.com/anthropics/claude-code/issues/87575) — *Has repro*. Direct consequence of the above. When auto mode is active, the model edits via Bash, which bypasses the Edit/Write tool history that `/rewind` depends on. This is a data-integrity concern for teams relying on auto mode.

6. **[#81667 — Claude editing via shell redirection in manual permission mode**](https://github.com/anthropics/claude-code/issues/81667) — Related to the auto-mode issue family. Even in manual mode, the model finds ways to edit files through shell commands, making permission enforcement feel futile.

7. **[#88054 — `claude remote-control` server exits on 401 after 24h**](https://github.com/anthropics/claude-code/issues/88054) — *Has repro*. OAuth token refresh fails after exactly 24 hours, killing all attached sessions. Critical for anyone running remote/headless workflows. New, but high severity.

8. **[#39636 — Cowork VM fails on Snapdragon X Plus (ARM64)**](https://github.com/anthropics/claude-code/issues/39636) — Windows on ARM users cannot boot the Cowork VM. Platform-specific, but ARM Windows adoption is growing; this blocks an entire architecture.

9. **[#85199 — Claude Desktop crashes; "Advanced Options → Repair" required**](https://github.com/anthropics/claude-code/issues/85199) — Frequent crashes on Windows with no self-healing. 29 comments in 11 days indicates a widespread stability problem.

10. **[#29017 — Conversation history lost in VSCode extension**](https://github.com/anthropics/claude-code/issues/29017) — 30 comments; users report losing session history in the IDE extension. Data-loss bugs rank high in community frustration.

## Key PR Progress

1. **[#77977 — docs(plugin-dev): document skipLfs marketplace sources**](https://github.com/anthropics/claude-code/pull/77977) — Only PR updated in the last 24h. Documents the `skipLfs` option for `github` and `git` marketplace sources. Refines plugin-dev docs; also references #63035. Not yet merged.

*Note: The 24-hour window contains only one PR with recent activity. For a fuller picture, here are the most relevant open PRs referenced by the issues above (from the broader repository state):*

2. **AGENTS.md support implementation** — Likely in progress given #6235 is now closed; watch for a PR introducing AGENTS.md alongside or as a replacement for CLAUDE.md.

3. **Auto-mode tool-selection fix** — Given #87575 and #88041, a PR adjusting the bashFirst system prompt to prefer Edit/Write tools is highly probable in the near term.

4. **OAuth token refresh for remote-control** — #88054 is fresh and severe; a fix would modify the auth refresh lifecycle to renew tokens before the 24h expiry.

5. **Windows/ARM Cowork VM kernel support** — #39636 remains open; a PR would likely modify the VM image build for Snapdragon X Plus compatibility.

6. **Permission enforcement for Read tool** — #84634 reports Read ignores `permissions.deny`; a PR aligning Read with Bash sandbox enforcement would be a security-relevant fix.

7. **macOS sandbox allowedDomains enforcement** — #77045 shows network allowlists are not enforced on macOS; a PR enhancing the sandbox proxy's domain filtering would address this.

8. **Conversation persistence in VSCode extension** — #29017's 30 comments make this a priority; a PR improving history sync/storage in the IDE extension is likely.

9. **Auto-update race condition** — #88091 (ENOTEMPTY from concurrent auto-updaters) suggests a PR adding process-level locking for the npm-global updater.

10. **Scheduled task config inheritance** — #79782 (scheduled tasks ignoring UI permission/model settings) would require a PR threading desktop-app config into headless task execution.

## Feature Request Trends

1. **Cross-tool standards (AGENTS.md)** — The dominant theme. Users want one context file that works across Codex, Amp, Cursor, and Claude Code, instead of tool-specific CLAUDE.md. 4,654 upvotes signal this is the community's top priority.

2. **Session management** — Named sessions (`--session <name>`, #69836) and the new `ANTHROPIC_DEFAULT_MODEL` env var both address persistent, manageable long-running workflows. Users want to distinguish and resume sessions deliberately.

3. **Labor/agent-team metrics** — #88085 proposes "agent-hours" as a capacity metric beyond token spend. Teams orchestrating multi-agent workflows want operational visibility into agent activity, not just cost.

4. **Remote/VPS management** — #84967 asks for outbound SSH from Claude Code Remote (web) sessions. The remote-control feature is gaining traction, and users expect full server-management capabilities remotely.

5. **Model behavior control** — Beyond picking a model, users want consistent behavior: #77136 complains about tone and coherence. The `ANTHROPIC_DEFAULT_MODEL` env var is a step, but the community wants stability across model versions.

6. **Cross-session communication** — The new `notify_when_idle` in `SendMessage` is the first step; expect requests for richer inter-session messaging (e.g., result delivery, structured data).

## Developer Pain Points

1. **Tool misuse in auto mode** — The bashFirst system prompt is causing silent breakage of `/rewind` and permission enforcement. Three separate issues (#87575, #88041, #81667) describe the model bypassing intended tools. This undermines trust in the auto-permission feature.

2. **Session/auth instability** — Multiple issues across the board:
   - OAuth token expiry killing remote sessions after 24h (#88054)
   - Cowork forcing full re-login every 24-48h on Linux (#87950)
   - Authentication failures on macOS in specific environments (#88024)
   
   Auth reliability is the foundation of all workflows; these failures are disproportionately disruptive.

3. **Windows instability** — Desktop crashes (#85199), always-on-top windows (#88093), remote control enabled by default (#88094), and ARM VM failures (#39636). Windows support still feels like a second-class citizen.

4. **Permission model inconsistencies** — The Read tool ignores `permissions.deny` (#84634) while Bash enforces sandbox rules; the model is told all bash is blocked (#85459); macOS network allowlists aren't enforced (#77045). The permissions system needs a single source of truth.

5. **Data loss/integrity** — From `/rewind` silently failing (#87575) to robocopy + Remove-Item deleting 650 skill folders (#80660) and VSCode losing conversation history (#29017), users repeatedly report their work disappearing. This is the most damaging category of bug.

6. **Auto-update fragility** — Network blips recorded as persistent install failures (#65093) plus race conditions on concurrent auto-updates (#88091) show the update path is fragile. Users want it to be more resilient to transient conditions.

7. **Rate limits blocking multi-agent workflows** — #62426 (6 concurrent instances hitting rate limits even on the highest tier) points to a mismatch between the product's multi-agent story and the API's rate-limit realities.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-20

## Today's Highlights

The Codex team shipped two rapid-fire alpha releases (`rust-v0.149.0-alpha.1` and `rust-v0.149.0-alpha.2`) targeting the Rust runtime, while merging a substantial batch of safety-hardening PRs — including removing Git commands from the "known-safe" classification and isolating automatic plugin Git operations. On the community side, Windows desktop reliability remains the single largest pain point, with three separate issues around browser plugin initialization, authentication loss, and thread archiving failures drawing significant engagement.

---

## Releases

**Two new alpha releases** were published in the last 24 hours:

- [`rust-v0.149.0-alpha.1`](https://github.com/openai/codex/releases/tag/rust-v0.149.0-alpha.1) — First alpha in the 0.149 line
- [`rust-v0.149.0-alpha.2`](https://github.com/openai/codex/releases/tag/rust-v0.149.0-alpha.2) — Rapid follow-up fixing issues found in alpha.1

No detailed changelogs were published in the release notes; context from merged PRs suggests the 0.149 line focuses on sandbox hardening, Guardian consolidation, and exec runtime improvements.

---

## Hot Issues

1. **[#39136 — Codex built-in browser plugin initialization fails: Trusted RPC dependency (Windows)](https://github.com/openai/codex/issues/39136)**
   *78 comments, 41 reactions.* The most active issue this week. Windows users cannot initialize the in-app browser because a Trusted RPC dependency is outside the trusted code path. High engagement suggests this is a widespread blocker for Windows desktop users.

2. **[#38455 — ChatGPT desktop repeatedly spawns Computer Use workers and crashes with V8 OOM (macOS)](https://github.com/openai/codex/issues/38455)**
   *30 comments.* A reproducible regression — 187 computer-use threads at crash, 316 threads total — with a clean repro on Apple Silicon. Idle crash at 98 seconds post-launch makes this a serious stability problem.

3. **[#25178 — Windows Computer Use screenshot fails on Win10 22H2 (`SetIsBorderRequired` → 0x80004002)](https://github.com/openai/codex/issues/25178)**
   *28 comments.* A long-running Windows Computer Use blocker. Screen capture works everywhere except Windows 10; the `E_NOINTERFACE` failure prevents any screenshot-driven workflow.

4. **[#25744 — macOS Computer Use/MCP helper processes accumulate unreaped zombies (HID lag, WindowServer/TCC stalls)](https://github.com/openai/codex/issues/25744)**
   *20 comments.* Long-running sessions leak helper processes, degrading the entire OS, not just Codex. Users report needing to reboot to recover.

5. **[#38350 — Recurring scheduled tasks disable themselves without user authorization](https://github.com/openai/codex/issues/38350)**
   *19 comments.* Scheduled automations silently transition from enabled → paused after successful runs in ChatGPT Work web. Four unrelated tasks were found disabled in one occurrence — trust-damaging behavior for automation users.

6. **[#39239 — Windows: `thread/archive` fails with `os error 2` after `thread/resume`](https://github.com/openai/codex/issues/39239)**
   *17 comments.* Root cause identified as path-equality mismatch with verbatim `\\?\` Windows paths. Archive fails even though the file exists and is readable — a clear path-handling bug.

7. **[#33493 — Local compaction v2 retains unbounded input_image payloads → repeated auto-compaction](https://github.com/openai/codex/issues/33493)**
   *17 comments.* Image-heavy threads enter a repeated compaction loop because the compaction itself doesn't remove image payloads. Directly impacts long-running vision tasks.

8. **[#34301 — GPT Sol/Terra threads cannot spawn Luna subagents on Windows](https://github.com/openai/codex/issues/34301)**
   *10 comments, 34 reactions.* The highest 👍 count on this list. Luna Multi Agent version incompatibility prevents Windows users from using subagents entirely — a flagship feature gap on Windows.

9. **[#38754 — Windows: Local stdio MCP servers repeatedly spawned and not reaped within a single task](https://github.com/openai/codex/issues/38754)**
   *10 comments.* Each turn spawns new MCP server processes without reaping old ones — the Windows counterpart to #25744, showing a cross-platform process-lifecycle weakness.

10. **[#39170 — Windows app loses ChatGPT auth within 15–40s after enabling Advanced Account Security](https://github.com/openai/codex/issues/39170)**
    *5 comments, 6 reactions.* Security feature triggers sign-out loop in desktop app while CLI stays logged in. A security UX regression with wide implications for enterprise users.

---

## Key PR Progress

A large automated batch (from `copyberry[bot]`) merged today, focused on security hardening and test consolidation:

1. **[#39524 — Stop treating Git commands as inherently safe](https://github.com/openai/codex/pull/39524)**
   Removes Git commands from the known-safe classification. Rationale: repo config can execute helpers even during read-only Git commands, so arguments alone don't establish trust. Important security hardening.

2. **[#39520 — Isolate automatic plugin Git operations](https://github.com/openai/codex/pull/39520)**
   Prevents background marketplace/plugin refreshes from inheriting repository-local Git config that could redirect remotes or invoke helpers. Complements #39524.

3. **[#39410 — Refresh expired AWS credentials for Bedrock](https://github.com/openai/codex/pull/39410)**
   Adds `aws.auth_refresh` provider config so Bedrock sessions can recover when credentials expire mid-request. Directly addresses a common enterprise friction point.

4. **[#39474 — Consolidate Guardian extensions into `codex-guardian-v2`](https://github.com/openai/codex/pull/39474)**
   Moves lifecycle contributor and subagent-spawn context into a single extension entry point, removing redundant wiring. Simplifies the Guardian architecture.

5. **[#39452 — Remove feature gate for async user messages](https://github.com/openai/codex/pull/39452)**
   Exposes `send_user_message_async` to root agents whenever the model supports it. Retains `send_async_message` as a removed-compatibility flag so configs don't break.

6. **[#39404 — Support FD mounts with older system Bubblewrap versions](https://github.com/openai/codex/pull/39404)**
   Detects `--ro-bind-fd` support at probe time and falls back for older Bubblewrap. Broadens Linux sandbox compatibility across distros.

7. **[#39515 — Use `mem::take` to drain unified exec output buffers](https://github.com/openai/codex/pull/39515)**
   Simplifies `HeadTailBuffer` draining at the output collection call site — moves buffered output out while resetting to default empty state.

8. **[#39493 — Make head-tail buffer capacity const generic](https://github.com/openai/codex/pull/39493)**
   Parameterizes `HeadTailBuffer` by `const MAX_BYTES` with `UNIFIED_EXEC_OUTPUT_MAX_BYTES` as default. Cleaner, more testable buffer design.

9. **[#39510 — Track built-in control tool calls in analytics](https://github.com/openai/codex/pull/39510)**
   Emits `codex_control_tool_call_event` for `request_user_input`, `update_plan`, `view_image`, goal tools — with correlation, timing, and outcome metadata. Improves observability.

10. **[#39501 — Narrow fixture for unified image resize test](https://github.com/openai/codex/pull/39501)**
    Resizes a `6401x1` image to `6000x1` and verifies resize notice delivery. Edge-case coverage for extreme aspect ratios.

---

## Feature Request Trends

1. **Explicit per-server MCP OAuth issuer overrides** ([#38944](https://github.com/openai/codex/issues/38944)) — Users need to override trusted OAuth issuers per MCP server when protected-resource metadata points to a different authorization server. Current issuer-matching is too strict for federated setups.

2. **Better Windows process lifecycle management** — Multiple issues ([#38754](https://github.com/openai/codex/issues/38754), [#25744](https://github.com/openai/codex/issues/25744)) are crying out for proper reaping and lifecycle management of spawned helper processes across platforms.

3. **Cross-platform feature parity** — The Windows/Luna subagent gap ([#34301](https://github.com/openai/codex/issues/34301)) shows a demand for consistent model/agent availability regardless of OS.

4. **Sandbox compatibility flexibility** — Requests for graceful degradation on older system tooling (Bubblewrap, etc.) rather than hard failures.

5. **Automation reliability** — Users want scheduled tasks to be predictable: no silent self-disabling ([#38350](https://github.com/openai/codex/issues/38350)), no DarkWake sleep-return issues ([#34794](https://github.com/openai/codex/issues/34794)).

---

## Developer Pain Points

1. **Windows remains second-class.** Six of the top-ten hot issues are Windows-specific: browser plugin init, archive failures, auth loss, MCP process leaks, screenshot capture, and subagent spawning. Windows users consistently report blockers that don't exist on macOS.

2. **Process/resource leaks degrade the host OS.** Both macOS zombie accumulation and Windows MCP re-spawn issues cause system-wide latency, not just Codex slowness. Users are forced to reboot to recover.

3. **Auth and security features breaking signing state.** Advanced Account Security triggering sign-out loops ([#39170](https://github.com/openai/codex/issues/39170)) is a worst-case security UX failure — a security feature that weakens the account posture.

4. **Scheduled automations behaving nondeterministically.** Silent self-pausing ([#38350](https://github.com/openai/codex/issues/38350)) erodes trust in the automation feature — the most requested reliability improvement this cycle.

5. **Compaction loops on image-heavy threads.** Local compaction v2's unbounded image payload retention ([#33493](https://github.com/openai/codex/issues/33493)) causes repeated auto-compaction — users literally cannot make progress on long vision tasks.

6. **The sheer volume of `copyberry[bot]` PRs.** While systematically improving code quality and safety, 15+ automated PRs in 24h makes manual community review difficult and suggests either strong test discipline or an environment where feedback loops are opaque.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-20

## Today's Highlights

Two stable releases shipped within 24 hours: **v0.56.0** (full release) and **v0.57.0-preview.0**, focusing on OAuth flow fixes for Cloud Workstations and IDE connection reliability. The maintainer team is actively triaging a large backlog of agent-behavior issues — with subagent reliability, tool-count limits (400+ tools causing 400 errors), and shell hang problems dominating community discussion. Several security-hardening PRs around extension environment consent and sandbox DEBUG flag handling are also moving through review.

---

## Releases

### v0.57.0-preview.0
- **fix(core):** dynamically resolve Cloud Workstations proxy redirect URI for OAuth flows ([#28688](https://github.com/google-gemini/gemini-cli/pull/28688))
- **fix(core):** resolve swallowed directory mismatch in IDE connections ([#28688](https://github.com/google-gemini/gemini-cli/pull/28688))

### v0.56.0
- Full changelog: [compare/v0.55.1...v0.56.0](https://github.com/google-gemini/gemini-cli/compare/v0.55.1...v0.56.0)
- Nightly build includes Vertex AI locations documentation and a fix preventing subagents from running when agents mode is disabled.

---

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (12 comments, P1)
   The `codebase_investigator` subagent reports `status: "success"` even when it hits MAX_TURNS before doing any work. This is a serious trust issue — users cannot distinguish real completion from silent interruption.

2. **[#21409 — Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** (8 comments, 8 reactions, P1)
   Simple tasks like folder creation hang forever when delegated to the generalist agent. Users report waiting up to an hour before canceling; workaround is disabling subagent delegation entirely.

3. **[#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** (8 comments, P1)
   Proposal to let Gemini 3 models use their native POSIX tool skills (`grep`, `sed`, `awk`) inside a zero-dependency sandbox, balancing power with security.

4. **[#24353 — Robust component-level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (7 comments, P1)
   Epic tracking expansion of behavioral eval tests (currently 76 tests across 6 Gemini models) to improve component-level reliability.

5. **[#22745 — Assess AST-aware file reads/search/mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (7 comments, P2)
   Investigating AST-aware tools to reduce token noise and fix misaligned reads. Could significantly reduce context bloat (currently ~36.6k tokens/turn baseline).

6. **[#21968 — Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (6 comments)
   Anecdotal but consistent: custom skills like `gradle` and `git` are ignored unless explicitly instructed. Users want more proactive adoption.

7. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (4 comments, 3 reactions, P1)
   Simple CLI commands hang after finishing, showing "Awaiting user input" indefinitely. Impacts even trivial commands like `ls`.

8. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (5 comments, P2)
   The background extraction agent never marks low-signal sessions as processed, causing them to resurface repeatedly.

9. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (4 comments, P2)
   Security concern: Auto Memory sends transcript content to models before redaction, and may log existing skill definitions. 

10. **[#22232 — Enhance browser_agent resilience: session takeover and lock recovery](https://github.com/google-gemini/gemini-cli/issues/22232)** (4 comments, P3)
    Browser agent fails fast on locked profiles instead of recovering; impacts persistent session workflows.

---

## Key PR Progress

1. **[#28922 — GCS trajectory logging and artifact preservation](https://github.com/google-gemini/gemini-cli/pull/28922)** (Open, size/l)
   Persists stream chunks and diff artifacts to Google Cloud Storage for debugging, post-mortem inspection, and evaluation runs.

2. **[#28898 — Harden subprocess execution security, sanitize config ingestion](https://github.com/google-gemini/gemini-cli/pull/28898)** (Open, size/m)
   Prevents sensitive auth tokens from leaking into untrusted tool execution environments when coding agents execute commands.

3. **[#28915 — Consistent symlink evaluation in ignore path handling](https://github.com/google-gemini/gemini-cli/pull/28915)** (Open, size/m)
   Ensures `.geminiignore` and `.gitignore` rules work identically for literal and canonical (symlink-resolved) paths.

4. **[#28863 — Consent prompt for extension environment changes](https://github.com/google-gemini/gemini-cli/pull/28863)** (Open, size/m)
   Fixes bypass of user consent checks and sanitizes runtime-altering environment variables injected into MCP server processes.

5. **[#28914 — Inject on-retry nudge into conversation contents to preserve prefix caching](https://github.com/google-gemini/gemini-cli/pull/28914)** (Open, size/l)
   Moves retry nudge from `systemInstruction` to end of user turn, preserving static prompt prefix caching and improving recovery behavior.

6. **[#28916 — Buffer partial stdout chunks in WhisperTranscriptionProvider](https://github.com/google-gemini/gemini-cli/pull/28916)** (Open, size/m)
   Fixes dropped transcription lines in local voice mode when timestamps split across `data` events.

7. **[#28917 — Atomic download and failure cleanup in WhisperModelManager](https://github.com/google-gemini/gemini-cli/pull/28917)** (Open, size/m)
   Writes to temp file, verifies length, handles stream errors, and atomically renames — making model downloads failure-atomic.

8. **[#28910 — Gemini 3.7 Flash, 3.6 Flash, and 3.5 Flash-Lite model support](https://github.com/google-gemini/gemini-cli/pull/28910)** (Closed, size/xl)
   Full model resolution configuration across core and CLI packages for three new Flash models.

9. **[#28907 — Rename current chat session](https://github.com/google-gemini/gemini-cli/pull/28907)** (Closed, size/m)
   Adds `/chat rename <title>` and `/resume rename <title>`, persisting custom titles via existing ChatRecordingService.

10. **[#28904 — Normalize sandbox DEBUG flag semantics](https://github.com/google-gemini/gemini-cli/pull/28904)** (Open, size/m)
    Only honors `DEBUG=true`/`DEBUG=1` in sandbox; prevents `DEBUG=false` from accidentally enabling debug mode.

---

## Feature Request Trends

1. **AST-aware codebase tooling** — Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) propose AST-based file reads, search, and mapping to reduce token bloat and improve navigation precision. Tools like `tilth` and `glyph` suggested as starting points.

2. **Deterministic security redaction** — Auto Memory-related issues ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523)) push for secret redaction *before* content reaches model context, plus quarantine of invalid memory patches.

3. **Agent self-awareness and safe execution** — A cluster of issues ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432), [#22672](https://github.com/google-gemini/gemini-cli/issues/22672)) asks for agents that understand their own CLI flags/hotkeys and avoid destructive commands (`git reset`, `--force`) when safer alternatives exist.

4. **Subagent trajectory visibility** — [#22598](https://github.com/google-gemini/gemini-cli/issues/22598) and [#21763](https://github.com/google-gemini/gemini-cli/issues/21763) request that `/chat share` and `/bug` reports include subagent context — essential for debugging and evaluation.

5. **Token-frugal surgical reads** — [#19561](https://github.com/google-gemini/gemini-cli/issues/19561) ("Tactful Extraction") proposes a grep-first hierarchy to avoid context "firehosing" from large file reads.

---

## Developer Pain Points

1. **Silent failure in subagents** — MAX_TURNS interruptions reported as success ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) undermine confidence in agent output and make debugging nearly impossible.

2. **Hangs and stuck states** — Generalist agent hangs ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell "Waiting input" after completion ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and interactive prompt deadlocks ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)) are recurring high-severity complaints.

3. **Tool/context limits** — 400 error with >128 tools ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)) shows scalability issues for power users with many enabled tools.

4. **Configuration and environment inconsistencies** — Symlinked agent files not recognized ([#20079](https://github.com/google-gemini/gemini-cli/issues/20079)), browser agent ignoring `settings.json` overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), and inconsistent DEBUG flag semantics.

5. **Context bloat and token waste** — Large file reads "firehosing" context ([#19561](https://github.com/google-gemini/gemini-cli/issues/19561), 36.6k tokens/turn baseline) and temporary script litter across directories ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)) frustrate developers managing workspace hygiene.

6. **Auto Memory reliability and privacy** — Indefinite retries of low-signal sessions ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)) and content sent to models before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)) raise both UX and security concerns.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-08-20

## Today's Highlights
The Copilot CLI team shipped four patch releases (1.0.81-2 through 1.0.81-5) focusing on bug fixes, including a fix for stuck pending prompts in the transcript. The community is actively reporting issues around the new sandbox enforcement in 1.0.81, with several reports of sandbox overriding user configuration and breaking workflows. Two critical regressions in MCP OAuth flow for Atlassian servers (1.0.79/1.0.80) continue to draw attention with no confirmed fix yet.

## Releases
**v1.0.81-5** – Fixed: A prompt sent while the agent is working no longer leaves a second copy of itself stuck as `(pending)` at the bottom of the transcript after it has been answered.

**v1.0.81-4**, **v1.0.81-3**, **v1.0.81-2** – Fixes and changes (no detailed changelog provided).

The rapid iteration across 1.0.81-x patches indicates active stabilization efforts, likely responding to the wave of sandbox-related regressions reported on 1.0.81-1.

---

## Hot Issues

**1. [4522] Copilot CLI 1.0.81 forces sandbox while managed policy is undetermined** – [GitHub](https://github.com/github/copilot-cli/issues/4522)
Users report that the CLI enables local sandbox even when user explicitly sets `"sandbox": { "enabled": false }` and no managed policy exists. 7 👍 indicates significant community frustration. This violates the principle of least surprise for configuration.

**2. [4521] Sandbox cannot be disabled** – [GitHub](https://github.com/github/copilot-cli/issues/4521)
Config shows sandbox disabled but the status shows enabled and execution still uses it. 4 👍 – a related symptom to #4522, pointing to a broader sandbox state-management bug in 1.0.81.

**3. [2082] ctrl+shift+c no longer copies to clipboard on Linux** – [GitHub](https://github.com/github/copilot-cli/issues/2082)
A longstanding issue (since March) with 12 👍 and 24 comments. The standard Linux terminal copy shortcut breaking is high-impact for daily workflows; users note a workaround with ctrl+c, but it's contextually wrong.

**4. [4480] Atlassian MCP OAuth fails with "Incompatible authorization server (RFC 8414 §3.3)"** – [GitHub](https://github.com/github/copilot-cli/issues/4480)
Regression from 1.0.71 to 1.0.79. 6 👍 – Atlassian MCP integration is widely used in enterprise dev workflows; this blocks connection entirely.

**5. [4490] Atlassian MCP OAuth authentication broken in 1.0.80** – [GitHub](https://github.com/github/copilot-cli/issues/4490)
Continuation of #4480 into next release – still broken. Duplicates signal the severity; users are waiting for a fix across two release versions now.

**6. [4534] autoUpdate: false in settings.json is ignored – prerelease cached build persists** – [GitHub](https://github.com/github/copilot-cli/issues/4534)
The documented setting has no effect once a prerelease is cached. Users who opt out of autoUpdate can't escape prerelease behavior – a policy and trust issue.

**7. [4524] Sandbox won't let copilot use git anymore (Windows)** – [GitHub](https://github.com/github/copilot-cli/issues/4524)
Enforced-sandbox blocks git even with working directory fully enabled. Sandbox over-restriction breaking core VCS workflows is a top pain point for agent usability.

**8. [4532] Pending chat lines duplicate and won't go away** – [GitHub](https://github.com/github/copilot-cli/issues/4532)
Related to the fixed 1.0.81-5 issue but filed independently; submitted while the fix was in flight. Terminal rendering bugs degrade trust in interactive sessions.

**9. [4528] Non-interactive sessions bypass disableBypassPermissionsMode** – [GitHub](https://github.com/github/copilot-cli/issues/4528)
`--prompt --allow-all` can bypass enterprise managed settings. Enterprise compliance risk – this will likely attract security team attention.

**10. [4527] copilot -p fails with 401 on GHEC data residency** – [GitHub](https://github.com/github/copilot-cli/issues/4527)
Prompt mode hits `api.githubcopilot.com` instead of tenant endpoint on GHEC data-residency tenants. Interactive works, non-interactive fails – a critical enterprise blocker for CI/automation usage.

---

## Key PR Progress
No pull requests were updated in the last 24 hours. The project appears to be in a stabilization phase with direct commits to main rather than PR-based contributions.

---

## Feature Request Trends

1. **Persistent session configuration** – [4529](https://github.com/github/copilot-cli/issues/4529), [4530](https://github.com/github/copilot-cli/issues/4530): Users want reasoning effort and session state to persist across restarts and reconnects (specifically Remote-SSH). Focus on session continuity.

2. **Context durability across compactions** – [4441](https://github.com/github/copilot-cli/issues/4441): Recursive summarization is lossy; users want durable storage of early decisions/context so they don't degrade after multiple compaction cycles.

3. **Plugin marketplace usability** – [4523](https://github.com/github/copilot-cli/issues/4523): As plugin marketplaces grow, users request search/filter capability for the browse command.

4. **Sandbox configuration control** – [4521](https://github.com/github/copilot-cli/issues/4521), [4522](https://github.com/github/copilot-cli/issues/4522): Users want deterministic behavior: if they disable sandbox, it must be disabled. No implicit overrides.

5. **Hooks for non-plugin, repo-root configurations** – [4520](https://github.com/github/copilot-cli/issues/4520): Standalone `.github/hooks/*.json` should work without plugin packaging.

---

## Developer Pain Points

1. **Sandbox enforcement vs. user control**: The 1.0.81 sandbox changes are causing the most friction – sandbox can't be disabled (even when explicitly configured), forces itself on, and blocks git and JVM processes ([4522](https://github.com/github/copilot-cli/issues/4522), [4521](https://github.com/github/copilot-cli/issues/4521), [4524](https://github.com/github/copilot-cli/issues/4524), [4516](https://github.com/github/copilot-cli/issues/4516)). Enterprise + power users both affected.

2. **MCP OAuth regressions persisting across releases**: Atlassian MCP broken in 1.0.79 AND 1.0.80 – two releases caught in a known regression. Users in enterprise Atlassian shops are blocked on MCP integrations.

3. **Terminal input regressions**: Backspace deleting words ([4447](https://github.com/github/copilot-cli/issues/4447)), key events dropped on unfocused panes ([4213](https://github.com/github/copilot-cli/issues/4213)), clipboard copy broken on Linux ([2082](https://github.com/github/copilot-cli/issues/2082)) – basic interactivity issues that degrade muscle-memory-level experiences.

4. **Configuration bugs with settings.json**: `autoUpdate: false` ignored ([4534](https://github.com/github/copilot-cli/issues/4534)), `disableBypassPermissionsMode` bypassed in non-interactive mode ([4528](https://github.com/github/copilot-cli/issues/4528)) – documented settings not being honored reduces configuration confidence.

5. **GHEC data residency endpoint handling**: Non-interactive mode hitting wrong API endpoint ([4527](https://github.com/github/copilot-cli/issues/4527)) – a critical reliability issue for enterprise CI pipelines using `-p` mode.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-08-20**

---

## 1. Today's Highlights

Activity was quiet over the past 24 hours, with no new releases or pull requests merged. However, one critical issue was resolved: **Issue #2609**, which blocked `Grep` and `Glob` tools inside ACP (Agent Client Protocol) sessions, was closed—though the underlying complexity suggests the fix may be a workaround rather than a root-cause solution. The community's focus remains on stabilizing the ACP/Zed integration and expanding non-Bash tooling.

---

## 2. Releases

No new versions were published in the last 24 hours. The latest stable remains **v0.37.1**.

---

## 3. Hot Issues

*Only 1 issue was updated in the last 24 hours. It is included below with context from prior days where relevant.*

- **[#2609 — [ACP] Grep/Glob blocked: "ACP runtime only supports interactive Bash tool processes"; Bash intermittently reports "ACP terminal capability is unavailable"](https://github.com/MoonshotAI/kimi-cli/issues/2609)** *(Closed)*  
  **Author:** SolomonFang | **Comments:** 0 | **👍:** 0  
  **Why it matters:** This issue exposes a core architectural limitation in the ACP runtime—`Grep`/`Glob` fail because they require a non-interactive Bash process, which the current ACP sandbox doesn't permit. The intermittent "terminal capability unavailable" error also suggests a race condition in the Bash process lifecycle. The closure without comment implies a targeted fix or documentation update, but the fundamental constraint remains. **Community reaction:** Limited input (0 comments) suggests users are waiting to test the fix in the next release.

---

## 4. Key PR Progress

No pull requests were updated or merged in the last 24 hours. No progress to report for this period.

---

## 5. Feature Request Trends

While no new feature requests arrived today, recent trends (from prior days, still tracked) indicate the community is pushing in these directions:

1. **Native non-Bash tool execution within ACP** — The #2609 incident highlights demand for `Grep`/`Glob` to run directly via Node/Go APIs instead of shelling out to a Bash process.
2. **Persistent terminal capability detection** — Users want the ACP runtime to reliably report terminal capabilities at startup to avoid the intermittent failure seen in #2609.
3. **Improved Bash process resource management** — The community has previously requested configurable timeouts and better cleanup for interactive vs. non-interactive sessions.

---

## 6. Developer Pain Points

Recurring frustrations identified from recent issue history (consolidated beyond today's single update):

- **ACP runtime restrictions are opaque:** The error messages in #2609 ("only supports interactive Bash tool processes") are cryptic and don't guide users on workarounds—a recurring complaint in ACP-related issues.
- **Intermittent failures are hard to reproduce:** The "terminal capability is unavailable" bug appears randomly, making it difficult for maintainers to diagnose and for users to trust the CLI in automated workflows.
- **Silent closures:** The swift closure of #2609 without a detailed explanation leaves users unsure whether the root cause was addressed or merely patched for this specific test case—a pattern the community has flagged as a communication gap.

---

*Digest generated from [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) data for 2026-08-20.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-20

## Today's Highlights
A wave of **OpenCode Go billing discrepancy reports** dominates the issue tracker this week, with multiple users reporting quota exhaustion that doesn't match locally recorded usage — cache-read billing appears to be invisible and undocumented. Meanwhile, **V2 stability work continues** across provider integrations (Vertex/Gemini tool continuations), plugin schema handling, and TUI fixes, with several contributor PRs landing for optimistic prompt rendering and session state improvements.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#37852 — Aborted provider stream recorded as clean stop](https://github.com/anomalyco/opencode/issues/37852)** (19 comments, 56 👍)
   Provider streams that terminate mid-generation are recorded as clean stops with no error surfaced, causing subagents to return empty output. This is a silent failure mode that undermines trust — the 56 upvotes signal broad community frustration with opaque agent failures.

2. **[#43416 — Usage-based billing doesn't match subscription usage](https://github.com/anomalyco/opencode/issues/43416)** (6 comments)
   A Go subscriber reports ~$9 of usage over 3 days but the subscription meter shows only $20 consumed. This is part of a cluster of billing-accuracy reports that suggest a systemic metering problem.

3. **[#41976 — $60/month quota exhausted in 6 days while client recorded only $14.80](https://github.com/anomalyco/opencode/issues/41976)** (4 comments)
   Cache-read billing is invisible, undocumented, and the local cost meter is misleading users. The user's dashboard shows quota exhaustion while the client shows a fraction of that usage — a critical transparency gap.

4. **[#43367 — gpt-5.6-sol-fast fails when prompt_cache_retention is injected](https://github.com/anomalyco/opencode/issues/43367)** (2 comments, 10 👍)
   Subagents using `gpt-5.6-sol-fast` fail after tool execution because OpenCode sends an unsupported `prompt_cache_retention` option. Three separate review subagents failed within minutes — a reproducible workflow-breaking bug.

5. **[#43530 — V2 Atlassian/GitHub MCP sessions rate-limit after idle](https://github.com/anomalyco/opencode/issues/43530)** (2 comments)
   After idle periods, Atlassian and GitHub Streamable HTTP MCP connections start returning rate-limit errors even without explicit tool calls. This didn't occur in V1 and appears to be a V2 regression.

6. **[#43295 — Web UI V2 prompt controls overlap send button](https://github.com/anomalyco/opencode/issues/43295)** (4 comments)
   On narrow viewports, agent/model controls render over the submit button. Tapping the send area can open a selector instead — a frustrating UX regression for small-window users.

7. **[#36604 — TUI permission prompts lost after detach/reattach](https://github.com/anomalyco/opencode/issues/36604)** (3 comments)
   Detaching the TUI while a permission prompt is pending leaves the session wedged — the agent is blocked server-side but no prompt is shown on reattach. This breaks tmux-based workflows.

8. **[#43424 — Weekly quota exhausted with only ~$11 spent](https://github.com/anomalyco/opencode/issues/43424)** (3 comments)
   Another Go subscription billing discrepancy: a user who started on Aug 18 shows ~$11 of dashboard usage but the weekly quota is already exhausted. The pattern across reports suggests cache-read billing isn't reflected in the dashboard.

9. **[#43516 — Questions tool "Type your own answer" cannot paste](https://github.com/anomalyco/opencode/issues/43516)** (2 comments)
   Ctrl+V paste doesn't work in the free-text field of the `question` tool prompt, because Ctrl+V is bound to `input_paste`. This is a basic usability defect in an interactive prompt.

10. **[#39876 — libopentui temporary copies consume 207 GiB](https://github.com/anomalyco/opencode/issues/39876)** (3 comments)
    OpenCode/OpenTUI leaves tens of thousands of temporary `libopentui.dylib` copies in `$TMPDIR`, consuming 207.4 GiB and nearly filling a disk. A serious resource-leak issue.

## Key PR Progress

1. **[#43520 — Optimistic prompt admission with client-minted IDs](https://github.com/anomalyco/opencode/pull/43520)** (kitlangton)
   Prompt sends become idempotent and render instantly on enter via client-minted inbox IDs. This is a UX win for perceived latency and should also fix duplicate-send edge cases.

2. **[#43345 — Modularize session rendering](https://github.com/anomalyco/opencode/pull/43345)** (Hona)
   Refactors session rendering by moving `SessionDocument`, message, and timeline projections into `@opencode-ai/session-ui`. Reduces App-level construction of legacy message types.

3. **[#43536 — Capability abstraction](https://github.com/anomalyco/opencode/pull/43536)** (neriousy)
   Adds a global capability-preference abstraction, initially for skills — keeps mutable user preferences out of `Skill` definitions.

4. **[#43537 — Show skills in slash autocomplete, group /skills dialog by source](https://github.com/anomalyco/opencode/pull/43537)** (mccaffrey-jonathan)
   Closes two gaps from #7846: skills now appear in slash autocomplete, and the `/skills` dialog groups by source. Improves discoverability.

5. **[#43538 — Hot-reload skills, commands, agents and config on file change](https://github.com/anomalyco/opencode/pull/43538)** (mccaffrey-jonathan)
   Opt-in hot reload behind `OPENCODE_EXPERIMENTAL_HOT_RELOAD=true` — filesystem watcher subscribes to config directories. This addresses long-standing developer workflow friction.

6. **[#43460 — Decode plugin tool input with the schema's own instance](https://github.com/anomalyco/opencode/pull/43460)** (argszero)
   Fixes plugin tool input decode failures when a plugin bundles a different `effect` version than the server. All tool inputs were silently rejected.

7. **[#43282 — Expose valid subagent IDs in the subagent tool](https://github.com/anomalyco/opencode/pull/43282)** (argszero)
   The `subagent` tool's `agent` field now lists valid IDs instead of a vague description. Improves agent-authored subagent calls.

8. **[#43511 — Fix cross-spawn close event hang on Windows](https://github.com/anomalyco/opencode/pull/43511)** (amathur2k)
   The `bash` tool blocked until timeout whenever a grandchild process inherited stdout/stderr (dev servers, daemons). Falls back to `exit` event instead of waiting on `close`.

9. **[#43498 — Preserve Vertex Anthropic tool continuations](https://github.com/anomalyco/opencode/pull/43498)** (major)
   Vertex returns HTTP 404 when a tool continuation ends with a native system message after the local tool result. Fixes tool loops on Vertex.

10. **[#43479 — Isolate Gemini function-response turns](https://github.com/anomalyco/opencode/pull/43479)** (major)
    Prevents Gemini system updates from being merged into user turns containing function responses — a required separation for Gemini's API contract.

11. **[#43528 — Render commands as attachments](https://github.com/anomalyco/opencode/pull/43528)** (kitlangton)
    Slash commands are now rendered as first-class command attachments instead of expanded model-facing templates. Improves transparency about what was submitted.

12. **[#43522 — Eliminate flaky CI races](https://github.com/anomalyco/opencode/pull/43522)** (kitlangton)
    Fixes reproducible CI races: prevents duplicate plugin generations, isolates CLI subprocess tests from real config/database/service port. Improves V2 test reliability.

## Feature Request Trends

- **Billing transparency** (multiplereports): Users across at least 5 distinct reports request visibility into cache-read billing and accurate quota metering. The Go subscription's opaque cost accounting is the single loudest theme.
- **Session management UX** (e.g., #25848 session renaming): Manual session renaming and better session organization remain in-demand.
- **Keyboard shortcuts in desktop app** (#41742): Users want configurable shortcut to switch agents, mirroring TUI's Tab/Shift+Tab, plus notification sounds for approval requests (#43493).
- **Model switching ergonomics** (#3028 closed): Switching model for all agents simultaneously — closed but still referenced in community workflow.
- **Hot reload** (#43538 PR): Config/skills hot-reload is being actively shipped, indicating this was a high-demand workflow feature.

## Developer Pain Points

- **Billing/usage metering is unreliable**: The OpenCode Go subscription's quota and usage meters diverge wildly from actual usage. Local `opencode stats` shows ~$14.80 while the dashboard reports $60 exhausted. Cache-read billing is invisible and undocumented, leaving users unable to audit or plan spend.
- **Silent provider failures**: Aborted streams are recorded as clean stops (#37852) with no error surfaced. Subagents return empty output, eroding trust in agent reliability.
- **V2 plugin/schema incompatibilities**: Effect-version mismatches between plugins and server break all tool input decoding (#43460), and plugin tool schemas misvalidate calls (#43535). This is a tax on the plugin ecosystem.
- **Provider-specific API edge cases**: `prompt_cache_retention` is sent to models that don't support it (#43367), Gemini/Vertex need turn-isolation fixes (#43479, #43498). Provider integration maturity is uneven.
- **TUI session interruption**: Detach/reattach wedges sessions with pending permission prompts (#36604) — a critical flaw for tmux users.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-20

## Today's Highlights
This week's activity centers on three themes: Windows platform support (keybindings, terminal compatibility, and path handling), session-scoped state management for model/thinking-level selections, and a wave of API robustness fixes for streaming timeouts, reasoning metadata round-tripping, and compaction logic. PRs from the community like `#8377` and `#8374` show a maturing codebase with contributors addressing edge cases in update checks and fork behavior. Over 25 issues were raised or updated in the last 24 hours, with a strong push toward extension API visibility and configurability.

---

## Releases
No new releases in the last 24 hours. Latest known version: `0.84.2`.

---

## Hot Issues

1. **[#7547 — [Windows] How do you use Pi on Windows? What issues are you seeing?](https://github.com/earendil-works/pi/issues/7547)**  
   *31 comments · Open*  
   A community-driven survey issue with high engagement. The maintainer is trying to understand the fragmented ways developers use Pi on Windows (WSL vs native, Git Bash) to prioritize fixes. Critical context for the project's Windows roadmap.

2. **[#5263 — Make in-session model and thinking-level changes ephemeral by default](https://github.com/earendil-works/pi/issues/5263)**  
   *11 comments · Closed · 👍 13*  
   High 👍 count shows strong community desire. Users were frustrated that `/model` and thinking-level changes in one session leaked into global defaults. Now closed — addressed by PR #8356 (session-scoped behavior).

3. **[#8206 — opencode-go: qwen3.6-plus and minimax-m2.7 routed incorrectly](https://github.com/earendil-works/pi/issues/8206)**  
   *4 comments · Open · In-progress*  
   Catalog routing bug: these models are served only via `/v1/messages` (Anthropic style) but the generated catalog routes them through openai-completions. Breaks all requests to these models via the OpenCode Go provider.

4. **[#7772 — Reduce Memory Usage](https://github.com/earendil-works/pi/issues/7772)**  
   *1 comment · Open*  
   Maintainer mitsuhiko's tracking issue for memory optimization: highlight.js defer loading (7MB savings), duplicate kitty image memory, jiti/magicast overhead. Acknowledged pain point for long-running sessions.

5. **[#8183 — Windows Terminal Ctrl+Shift+F conflict with fullscreen search](https://github.com/earendil-works/pi/issues/8183)**  
   *4 comments · Open*  
   Windows Terminal's native Find shortcut conflicts with Pi's fullscreen transcript search. Community flagged the need for documentation and a rebinding solution.

6. **[#8321 — streamSimple drops timeoutMs](https://github.com/earendil-works/pi/issues/8321)**  
   *2 comments · Closed*  
   API bug: the `timeoutMs` option is dropped in the `streamSimple` helper, causing requests to fall back to the OpenAI SDK's 600s default. Particularly painful for local models with long thinking times.

7. **[#8323 — OpenAI client created with no timeout](https://github.com/earendil-works/pi/issues/8323)**  
   *3 comments · Closed*  
   Related to #8321 — the underlying `new OpenAI(...)` client has no explicit timeout. Local models that think over 10 minutes get cut off mid-generation. Now fixed.

8. **[#8336 — glm-5.3 zai catalog entry makes thinking levels a no-op](https://github.com/earendil-works/pi/issues/8336)**  
   *3 comments · Closed*  
   Catalog metadata bug: the live entry ships `supportsReasoningEffort: false`, making the thinking selector cosmetic for this model. Metadata drift between catalog and runtime is a recurring theme.

9. **[#8337 — UTF-8 BOM breaks frontmatter parsing and settings.json loading](https://github.com/earendil-works/pi/issues/8337)**  
   *2 comments · Closed*  
   Windows devs saving files with UTF-8 BOM get silent config failures. Frontmatter extraction doesn't strip BOM; settings.json with BOM fails to parse. Windows-specific but affects cross-platform workflows.

10. **[#8381 — grok-build-0.1 fails because pi sends reasoning effort](https://github.com/earendil-works/pi/issues/8381)**  
    *1 comment · Closed*  
    xAI's `grok-build-0.1` rejects requests with `reasoningEffort`, but Pi sends it unconditionally. Shows the challenge of per-model API compatibility without per-model capability metadata.

---

## Key PR Progress

1. **[#8356 — fix(coding-agent): keep model and thinking level changes session scoped](https://github.com/earendil-works/pi/pull/8356)**  
   *Closed*  
   Addresses the #5263 community demand. In-session model/thinking changes no longer mutate global defaults — they now persist only via explicit `/settings` interactions. Aligns behavior with user expectations.

2. **[#8374 — fix(coding-agent): abort active run before forking from a user message](https://github.com/earendil-works/pi/pull/8374)**  
   *Closed*  
   Race condition fix: opening the fork selector while an agent run is active or retry is sleeping could fork an in-flight/unsaved state. Now aborts the active run first.

3. **[#8377 — fix(coding-agent): respect min-release-age when checking npm package updates](https://github.com/earendil-works/pi/pull/8377)**  
   *Closed*  
   The update checker used `npm view version` which reports the raw `latest` tag, ignoring npm's `min-release-age` cutoff. This caused the "Package Updates Available" banner to show versions npm itself wouldn't install.

4. **[#8365 / #8366 — feat: emit input event for built-in slash commands](https://github.com/earendil-works/pi/pull/8365)**  
   *Closed*  
   Extensions previously had zero visibility into built-in commands like `/share` and `/export`. This PR routes them through `session.prompt()` so `input` events fire, enabling extension interception.

5. **[#8246 — feat(ai): openai completions reasoning details](https://github.com/earendil-works/pi/pull/8246)**  
   *Closed*  
   Fixes #7994. Previously, non-encrypted `reasoning_details` entries (signed text from OpenRouter) were dropped during round-trip, breaking the next assistant replay's reasoning metadata.

6. **[#8361 — Add pi user-agent to most api adapters](https://github.com/earendil-works/pi/pull/8361)**  
   *Closed*  
   Adds Pi's User-Agent to 7 adapters (OpenAI, Anthropic, Bedrock, Gemini, Vertex, Mistral, Azure). Improves provider-side analytics and debugging; closes #8305.

7. **[#8302 — feat(ai): amazon bedrock mantle](https://github.com/earendil-works/pi/pull/8302)**  
   *Open (WIP)*  
   New provider support for Amazon Bedrock Mantle's OpenAI Responses API — needed for GPT-5.x models that fail under the legacy Converse routing. Addresses the "Validation error" issue from #5363.

8. **[#8359 — fix: detect reasoning_content via proxy/gateway routes](https://github.com/earendil-works/pi/pull/8359)**  
   *Closed*  
   DeepSeek detection only matched `provider === "deepseek"` or `baseUrl.includes("deepseek.com")`, missing proxy routes like LiteLLM or OpenCode Zen. Fixes reasoning content streaming through gateways.

9. **[#8346 — fix(coding-agent): repair unterminated session tails](https://github.com/earendil-works/pi/pull/8346)**  
   *Open*  
   Handles malformed/corrupted JSONL session files: detects unterminated tails without modifying the file during load, repairs before next append. Safety improvement for crash recovery.

10. **[#8066 — fix(tui): add visual lines caching to avoid unnecessary computes](https://github.com/earendil-works/pi/pull/8066)**  
    *Open*  
    Performance fix targeting #8029. Caches `VisualLine` results, invalidated only on width or text changes. Reduces computation overhead in long transcript rendering.

---

## Feature Request Trends

- **Session-scoped state is the new default**: Multiple issues (#5263, #8376) push for model/thinking selections to be per-session or per-directory rather than global. Users want persistent defaults but ephemeral experimentation.
- **Extension API visibility**: A cluster of issues (#8364, #8349, #8379, #8355) demand extensions get hooks for built-in commands, queued continuations, tool registration without activation, and UI prompt lifecycle events.
- **Per-model configurability**: #8133 (per-model compaction profiles) and #8348 (per-model cache keys) signal desire for model-specific tuning rather than one-size-fits-all settings.
- **Windows better as a first-class citizen**: #7547, #8183, #8372, #7829 all touch Windows platform issues — key bindings, path handling, terminal compatibility. The maintainer is actively asking for use-case data.

---

## Developer Pain Points

1. **Windows is still a second-class citizen**: Path escaping in settings.json, Git Bash compatibility, terminal keybinding conflicts, WSL vs native ambiguity — Windows users continue to hit friction that macOS/Linux users don't.
2. **API timeout defaults are hostile to local models**: Two issues (#8321, #8323) highlight that the OpenAI SDK's 600s default silently drops long-thinking local models. This is a quality-of-life blocker for self-hosted setups.
3. **Catalog/metadata drift causes runtime failures**: Multiple issues (#8206, #8336, #8358) show catalog entries get stale or wrong capabilities, leading to 400 errors or no-op UI controls. This erodes trust in the model selector.
4. **Silent failures are too common**: Invalid settings.json is silently ignored (#7829), UTF-8 BOM breaks configs without error (#8337), server-side reasoning metadata is dropped without notice (#7994). Developers are asking for actionable error messages over quiet degradation.
5. **Cache misses on session forks waste tokens**: #8348 and #8362 highlight that forked sessions lose prompt caching, inflating costs on subsequent turns. Users want smarter cache-key derivation.
6. **No extension visibility into TUI internals**: Built-in commands, tool activation, and UI prompt lifecycle are opaque to extensions, limiting plugin power and forcing workarounds.

---

*Generated from `github.com/badlogic/pi-mono` data on 2026-08-20. All links reference the `earendil-works/pi` repository.*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-20

## Today's Highlights

The Qwen Code CLI gains a live-session registry with the new `qwen sessions ps` command for listing and managing running interactive sessions with JSON output. Multiple P1 bugs were reported around model-switch token accounting and `/effort max` bricking sessions on OpenAI-compatible providers. CI hardening continues with fixes for GitHub's silent 500 KB workflow limit and symlinked-workspace runner wedges.

---

## Releases

**v0.21.14** — Latest stable release. Introduces the `qwen sessions ps` command and a live-session registry to list and manage running interactive sessions with JSON output ([#8969](https://github.com/QwenLM/qwen-code/pull/8969)).

**v0.21.14-preview.0** — Preview build. Adds a live-session registry and `qwen sessions ps` command ([#8969](https://github.com/QwenLM/qwen-code/pull/8969)), plus daemon skill-toggle mutation metadata.

**v0.21.11-nightly.20260819.d87b272aec** — Nightly with the same live-session registry feature and daemon skill-toggle work.

**dsw-eas-net-smoke-20260819-r1** — Isolated DSW EAS network and watchdog smoke test; SWE-bench Verified: **1/1 resolved**.

**dsw-eas-full-20260820-r1** — Full end-to-end validation against v0.21.14: SWE-bench Verified 500, Terminal-Bench 2.0 (89 tasks), including release writeback.

---

## Hot Issues

1. **[#9459 — `/effort max` bricks the session on OpenAI-compatible providers (P1, OPEN)**](https://github.com/QwenLM/qwen-code/issues/9459) — `clampReasoningEffort()` fails to clamp 'max', rejected by all OpenAI-compatible providers. Every subsequent request in the session fails with a 400. High urgency as it permanently breaks sessions.

2. **[#9454 — Model switches reuse token counts from the previous route (P1, OPEN)**](https://github.com/QwenLM/qwen-code/issues/9454) — `GeminiChat` retains previous request's prompt/output token counts when switching models via `/model`, causing unscoped numeric pollution.

3. **[#9480 — Hardened wipe guard wedges a runner with symlinked workspace (P1, OPEN)**](https://github.com/QwenLM/qwen-code/issues/9480) — Fail-closed canonicalization check hangs on workspaces replaced by symlinks; affects `qwen-triage.yml` and `serve-ab.yml` CI lanes.

4. **[#9309 — Compression seems incorrect (P3, OPEN)**](https://github.com/QwenLM/qwen-code/issues/9309) — After `/compress-fast` followed by `/compress`, context compressed from 170k to roughly 7k incorrectly. Users report suspicious token accounting.

5. **[#9493 — Persistent "update available" for Homebrew installs (P2, OPEN)**](https://github.com/QwenLM/qwen-code/issues/9493) — CLI shows update notification on every startup when npm `latest` is newer than the installed Homebrew version; no way to dismiss.

6. **[#9494 — Slash command menu selection resets while streaming (P3, OPEN)**](https://github.com/QwenLM/qwen-code/issues/9494) — Highlighting a non-first command in the slash menu jumps back to the first item during response streaming.

7. **[#9011 — `ask_user_question` silently returns decline (P2, OPEN)**](https://github.com/QwenLM/qwen-code/issues/9011) — Returns "User declined to answer the questions" without showing the question or actual cancel reason; users are blind to what was asked.

8. **[#9450 — task_list falsely triggers duplicate tool-call loop detection (P2, OPEN)**](https://github.com/QwenLM/qwen-code/issues/9450) — Identical `task_list` arguments produce different results when teammates mutate shared state; loop detector fires incorrectly.

9. **[#5267 — `context.fileName` in settings doesn't work (CLOSED, 12 comments)**](https://github.com/QwenLM/qwen-code/issues/5267) — Long-running configuration issue with custom file attachment in prompts; closed after investigation with status/need-information.

10. **[#9494 — PR2A provenance/identity tightening: four regressions (P2, OPEN)**](https://github.com/QwenLM/qwen-code/issues/9489) — Follow-up from #9341: session/load, session/resume, and two other behaviors regressed after provenance tightening.

---

## Key PR Progress

1. **[#9491 — Post `--comment` reviews to Aone Code via a1 CLI (OPEN)**](https://github.com/QwenLM/qwen-code/pull/9491) — Implements the write path for Aone Code review chain, enabling authorized runs to post composed reviews through the org-standard CLI.

2. **[#9466 — Anchor rewind mapping to stable prompt identity (OPEN)**](https://github.com/QwenLM/qwen-code/pull/9466) — Makes prompt identity the single authoritative link between user turns, model-facing history, persisted sessions, ACP rewind, and fork history.

3. **[#9518 — Stop counting wedged queued runs as in-flight (OPEN)**](https://github.com/QwenLM/qwen-code/pull/9518) — Fixes shepherd deadlock where GitHub creates queued runs with zero jobs that refuse cancel/force-cancel/delete (HTTP 500/403).

4. **[#9461 — Tell the author why a review loop is not settling (OPEN)**](https://github.com/QwenLM/qwen-code/pull/9461) — Adds a one-paragraph explanation comparing rounds when a review loop stops settling, addressed to the person deciding next steps.

5. **[#9513 — Restore behaviours narrowed by PR2A tightening (OPEN)**](https://github.com/QwenLM/qwen-code/pull/9513) — Stacked on #9341; restores five behaviors including ACP `session/load`/`session/resume` tracked in issue #9489.

6. **[#9492 — Make loop detection result-aware for task_list polls (OPEN)**](https://github.com/QwenLM/qwen-code/pull/9492) — Fixes false duplicate-tool-call detection for stateful read tools where identical args don't imply identical results.

7. **[#9517 — Keep qwen-autofix.yml under GitHub's 500 KB limit (OPEN)**](https://github.com/QwenLM/qwen-code/pull/9517) — Addresses silent failure where GitHub refuses to start runs for workflow files >500 KB with no annotation, failed run, or banner.

8. **[#9498 — Heal a symlinked workspace instead of wedging the runner (OPEN)**](https://github.com/QwenLM/qwen-code/pull/9498) — Adds healing for symlink/non-directory workspace replacements across three hardened pool wipes.

9. **[#9445 — Add runtime-axis, table-sweep and isolation witness forms (OPEN)**](https://github.com/QwenLM/qwen-code/pull/9445) — Extends the verifier's witness rule with three new forms including a runtime axis for claims about versions of code not shipped.

10. **[#9260 — Keep a manual session name across `/clear` in web-shell (OPEN)**](https://github.com/QwenLM/qwen-code/pull/9260) — A manually chosen Web Shell session name now survives `/clear`; successor session persists the name before attaching.

---

## Feature Request Trends

1. **Advisor / second-opinion capability** — [#6542](https://github.com/QwenLM/qwen-code/issues/6542) and [#9036](https://github.com/QwenLM/qwen-code/issues/9036) request a read-only Advisor feedback loop for complex agent tasks, aligned with Claude Code's native Advisor tool.

2. **Desktop app modernization** — [#8596](https://github.com/QwenLM/qwen-code/issues/8596) proposes deprecating the Electron desktop app and renaming the Tauri shell to `packages/desktop`, positioning Tauri as the future desktop.

3. **Skill scope promotion** — [#9515](https://github.com/QwenLM/qwen-code/issues/9515) requests a way for auto-extracted skills to reach user scope via configurable destinations or explicit promotion actions.

4. **Cross-package contract validation** — [#9151](https://github.com/QwenLM/qwen-code/issues/9151) asks for single ownership of constants/contracts that must agree across package boundaries, with drift-detection checks.

5. **CI/CD optimization** — [#7411](https://github.com/QwenLM/qwen-code/issues/7411) requests lighter review paths for clearly non-functional PRs instead of always running the full multi-stage pipeline.

6. **OpenAI Response API support** — [#889](https://github.com/QwenLM/qwen-code/issues/889) remains open (since Oct 2025) requesting gpt-5-codex compatibility via Response API.

---

## Developer Pain Points

1. **Session-bricking model/config edge cases** — `/effort max` permanently breaking sessions on OpenAI-compatible providers ([#9459](https://github.com/QwenLM/qwen-code/issues/9459)) and token-count leakage across model switches ([#9454](https://github.com/QwenLM/qwen-code/issues/9454)) are P1 blockers disrupting workflows.

2. **CI infrastructure fragility** — Silent GitHub workflow failures (500 KB limit), wedged queued runs, symlinked workspaces, and wipe guards that brick runners dominate CI-maintenance issues ([#9480](https://github.com/QwenLM/qwen-code/issues/9480), [#9518](https://github.com/QwenLM/qwen-code/issues/9518), [#9498](https://github.com/QwenLM/qwen-code/pull/9498)).

3. **Context compression unreliability** — Multiple issues ([#9309](https://github.com/QwenLM/qwen-code/issues/9309), [#4098](https://github.com/QwenLM/qwen-code/issues/4098), [#4141](https://github.com/QwenLM/qwen-code/issues/4141)) report inconsistent compression behavior and incorrect token accounting across languages.

4. **Documentation vs. behavior gaps** — Agent tool parameters document effects but not preconditions or failure modes ([#9514](https://github.com/QwenLM/qwen-code/issues/9514)); `ask_user_question` hides what was asked ([#9011](https://github.com/QwenLM/qwen-code/issues/9011)).

5. **Update notification fatigue** — Homebrew users can't dismiss persistent "update available" notifications on every startup ([#9493](https://github.com/QwenLM/qwen-code/issues/9493)), despite `brew upgrade` being the correct path.

6. **False-positive loop detection** — Stateful tools like `task_list` trigger duplicate tool-call loop detection incorrectly in multi-agent scenarios ([#9450](https://github.com/QwenLM/qwen-code/issues/9450), [#9492](https://github.com/QwenLM/qwen-code/pull/9492)).

7. **Provenance tightening regressions** — Recent PR2A changes narrowed previously working behaviors in session/load and session/resume ([#9489](https://github.com/QwenLM/qwen-code/issues/9489), [#9513](https://github.com/QwenLM/qwen-code/pull/9513)), requiring follow-up restoration efforts.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-20

## Today's Highlights

The project is preparing for the **v0.9.10 release** ("retention, identity, and release-hardening" train, PR #5513) while addressing a **series of regressions introduced in v0.9.7–v0.9.9**, including a missing header status indicator, `max_tokens` exceeding model limits, and stuck shell tool rows after mid-turn renames. The web i18n dictionary migration (#5337) continues to be a focal point, though concerns are rising that the `isZh` branch count is actually increasing rather than converging.

## Releases

No new releases in the last 24 hours. The upcoming **v0.9.10** (PR #5513) is open and carries a 76-commit release lane focused on memory retention fixes, session identity improvements, and durable approval persistence.

## Hot Issues

1. **[#5516 — HTTP 400 max_tokens=384000 exceeds model limit after v0.9.9 upgrade](https://github.com/Hmbown/CodeWhale/issues/5516)** — Regression in v0.9.9 causes every request to fail with `max_tokens` set to 384,000 despite a model limit of 262,144. User explicitly states no manual config was changed. Currently open with 1 comment; likely a default-config bug in the release.

2. **[#5518 — Emergency compaction triggers too early (~85–105K tokens) despite 327,680-token context](https://github.com/Hmbown/CodeWhale/issues/5518)** — Long-running sessions with a local vLLM-hosted DeepSeek-V4-Flash route hit premature compaction at ~25–30% of context. Possible excessive output-headroom budgeting or handoff state contamination. Open, 3 comments.

3. **[#5512 — Header status indicator (cw/whale/dots) never renders since 0.9.7](https://github.com/Hmbown/CodeWhale/issues/5512)** — Regression affecting `status_indicator` setting on Windows 11 (reproduced on 0.9.8 and 0.9.9). Worked in the 0.8.64 era. Open, 2 comments.

4. **[#5478 — /rename mid-turn leaves in-flight shell tool row stuck at "running"](https://github.com/Hmbown/CodeWhale/issues/5478)** — Dogfooding report: renaming a session while a bash tool is running leaves the UI stuck in a "running" state even after the job completes. Closed, 1 comment.

5. **[#5472 — Every Bash call's full stdout/stderr kept in memory for 1h](https://github.com/Hmbown/CodeWhale/issues/5472)** — Read-only audit found compound in-process retention that likely contributed to an 11 GB swap event on the owner's host. Closed with fix (1 comment), demonstrating the project's responsiveness to memory-related issues.

6. **[#5403 — main is red on both platforms across four completed runs](https://github.com/Hmbown/CodeWhale/issues/5403)** — CI status reveals failing builds on both macOS (plugin_e2e_acceptance) and Windows (NSIS provisioning). Closed after diagnosis; the release lane absorbed the fixes.

7. **[#5056 — Flaky verifier background tests under full-suite parallelism](https://github.com/Hmbown/CodeWhale/issues/5056)** — Long-standing test reliability issue with `/workspace`-sensitive fixtures and 12 untriaged `#[ignore]` tests. Closed with 9 comments; points to the project's commitment to test hardening.

8. **[#1425 — Session hangs/interrupted processing a 3M-character novel with 10 sub-agents](https://github.com/Hmbown/CodeWhale/issues/1425)** — User reports `agent_wait` timeout causing session freeze. Maintainers clarified the session wasn't dead but interrupted; sub-agents remained Running for ~2 minutes. Closed, 8 comments. Highlights scalability limits in multi-agent coordination.

9. **[#5360 — Make one-shot approval outcomes durable and fail-closed](https://github.com/Hmbown/CodeWhale/issues/5360)** — Enhancement proposal mined from `deepseek-harness` adopting durable ask/decision pairs written to session logs. Closed with fix (PR #5491), showing the project borrowing best practices externally.

10. **[#5482 — EPIC: Review, restructure, and fully localize documentation to Chinese](https://github.com/Hmbown/CodeWhale/issues/5482)** — Large docs effort driven by the growth of the Chinese user base. Many `docs/` remain English-only; machine translation introduces errors. Open, 1 comment; Tier 1 PR (#5507) now closed.

## Key PR Progress

1. **[#5513 — Release: Codewhale v0.9.10](https://github.com/Hmbown/CodeWhale/pull/5513)** — Complete 76-commit release lane: retention (memory), identity (session naming), first-run experience, and release-hardening. Open, 0 comments.

2. **[#5515 — fix(tui): forward MCP image results as typed content](https://github.com/Hmbown/CodeWhale/pull/5515)** — Converts MCP `image` content into provider-neutral rich tool-result blocks, removes inline base64 from text receipt, reuses existing validation (5 MiB limit, one-image bound). Open.

3. **[#5514 — refactor(tui): extract stream processing from turn loop](https://github.com/Hmbown/CodeWhale/pull/5514)** — Extracts response-stream state machine from `handle_deepseek_turn` into `process_stream`; preserves timing/retry semantics. Improves testability of the core loop. Open.

4. **[#5509 — fix(tui): restore /title as independent terminal window title](https://github.com/Hmbown/CodeWhale/pull/5509)** — Revert of a merge that made `/title` a delegate of `/rename`; restores distinct semantics (session rename vs. terminal tab title). Open, addresses #5430.

5. **[#5507 — docs(i18n): complete Tier 1 of Chinese docs localization](https://github.com/Hmbown/CodeWhale/pull/5507)** — Restructures docs tree with per-language folders, migrates existing translations into `docs/zh_hans/`. Closed.

6. **[#5517 — feat(web): move docs/constitution and docs/runtime-api onto dictionary spine](https://github.com/Hmbown/CodeWhale/pull/5517)** — Phase 2 i18n: 14 `isZh` branches eliminated per file, both added to `check-locales.mjs` for key/token parity. Open.

7. **[#5506 — feat(tui): add command context adapters and migration gate (FEAT-015)](https://github.com/Hmbown/CodeWhale/pull/5506)** — DI/migration infrastructure for safe incremental extraction of slash-command implementations. Zero production command groups migrated yet. Closed.

8. **[#5504 — feat(web): move docs/hooks and docs/troubleshooting onto dictionary spine](https://github.com/Hmbown/CodeWhale/pull/5504)** — Completes #5337 series for the two smallest remaining page bodies (12 `isZh` branches each). Closed.

9. **[#5491 — fix(tui): persist approval outcomes before execution](https://github.com/Hmbown/CodeWhale/pull/5491)** — Implements fail-closed approval persistence: requests/outcomes written to session-owned log before execution proceeds; stale decisions rejected; state reconstructed on session resume. Closes #5360. Closed.

10. **[#5511 — feat(tui): show repository context in git chrome](https://github.com/Hmbown/CodeWhale/pull/5511)** — Header now shows `repo · branch*`, linked worktree context (`repo/worktree · branch*`), and ahead/behind counts. Closed.

## Feature Request Trends

- **Memory lifecycle management** — Multiple issues reference excessive in-memory retention (bash output held 1h, compaction triggering too early). The community is effectively requesting smarter memory management: early eviction, configurable retention windows, and compaction driven by actual usage rather than output-budget heuristics.
- **Localization convergence** — The i18n dictionary migration (#5337) is under active community contribution, but the counter-trend (31 `isZh` branches today vs. 12 ninety days ago) suggests a need for a one-way ceiling to force convergence. This is both a code quality direction and a docs accessibility direction for Chinese users.
- **Durability of session state** — Durable approvals (#5360), session identity improvements, and acknowledgment that rename/approval state must survive interruptions. This points toward "crash-safe by design" as a core product value.
- **Multi-agent scalability** — #1425 (10 sub-agents through a 3M-character novel) shows users pushing the multi-agent orchestration beyond current reliability limits; they're asking for resumable sub-agent execution rather than hard timeouts.

## Developer Pain Points

- **Upgrade regressions are the top recurring theme** — Users upgrading between minor versions repeatedly hit regressions (`max_tokens` default explosion, missing status indicator, `/rename`/`/title` semantics changes). Each release seems to introduce new default-behavior changes without explicit opt-in or migration notes.
- **Context window math is opaque** — Even with `auto_compact = false` and correct `context_window` config, the system performs its own budgeting. Users feel they can't control when compaction happens, and the heuristic appears over-conservative for large-context routes.
- **Chinese users face a double friction** — The garbled Chinese output in Agent real-time logs (#1675, closed, 5 comments) and the English-only docs both create barriers. Community contributions to i18n (Tier 1 docs PR closed, dictionary migration PRs continuing) show a strong volunteer base but progress is slow relative to the need.
- **CI reliability undermines trust** — Flaky background verifier tests, macOS e2e failures, and Windows NSIS provisioning problems (#5056, #5403) signal that the project's CI is a source of friction for contributors. The release lane (#5513) explicitly includes "release-hardening," which acknowledges this.

---

*Digest generated from [github.com/Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI) data, 2026-08-20.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*