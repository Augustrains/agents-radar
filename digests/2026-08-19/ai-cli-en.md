# AI CLI Tools Community Digest 2026-08-19

> Generated: 2026-08-19 00:30 UTC | Tools covered: 9

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

# AI CLI Tools Cross-Tool Comparison Report
**Date: 2026-08-19**

---

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem is maturing rapidly, with seven major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI (now CodeWhale)—all shipping active releases and engaging substantial communities. The landscape is characterized by intense competition on three fronts: **reliability** (silent data loss, hangs, and session corruption are the most-reported pain points across all tools), **multi-agent orchestration** (Qwen Code's agent boards, Claude Code's Cowork, and Gemini CLI's subagent improvements), and **enterprise readiness** (sandboxing, security hardening, billing transparency, and compliance features). Cross-session messaging reliability and MCP server lifecycle management remain systemic weaknesses across virtually every tool, suggesting fundamental architectural challenges yet to be solved.

---

## 2. Activity Comparison

| Tool | Releases Today | Hot Issues (24h) | Key PRs (24h) | Notable Issue Volume |
|------|---------------|-------------------|----------------|---------------------|
| **Claude Code** | ✅ v2.1.235 (patch) | 10 tracked | 1 (limited) | #84352: 121 comments, 20👍 |
| **OpenAI Codex** | ✅ rust-v0.148.0 (major TUI) | 10 tracked | 10 active | #39136: 63 comments, Windows RPC |
| **Gemini CLI** | ✅ v0.56.0-nightly | 11 tracked | 12 active | #22323 (P1), #21409 (P1, 8👍) |
| **GitHub Copilot CLI** | ✅ v1.0.81-1 | 10 tracked | 1 (spam PR) | #4522 sandbox regression (5👍) |
| **Kimi Code CLI** | ❌ None | 2 tracked | 2 | #2607 Web UI regression |
| **OpenCode** | ❌ None (v1.18.18 latest) | 10 tracked | 10 tracked | #42935 billing/quota crisis |
| **Pi** | ❌ None | 10 tracked | 10 active | #8331 stream stall hangs |
| **Qwen Code** | ✅ v0.21.11-nightly | 10 tracked | 10 active | #656 P1 API error (11 months) |
| **DeepSeek TUI / CodeWhale** | ✅ v0.9.9 | 10 tracked | 10 active | #5505 system prompt loss |

**Key observations:**
- Claude Code has the **largest community engagement** per issue (#84352: 121 comments)
- Codex ships the **most significant release** (TUI overhaul with session forking, Markdown export)
- Qwen Code and CodeWhale have the **most active PR pipelines** for their size
- Copilot CLI's PR pipeline is **concerningly quiet** (1 stale/spam PR)
- Kimi Code CLI has the **lowest activity**, suggesting a smaller community

---

## 3. Shared Feature Directions

### Cross-Tool Feature Correlations

| Feature Requirement | Tools | Specific Needs |
|--------------------|-------|----------------|
| **Multi-agent / multi-session coordination** | Claude Code (#86279), Qwen Code (#8718, #9276, #9402), Gemini (#21968), Codex (#39269) | Cross-session messaging, agent boards, subagent trajectory transparency, session forking |
| **Sandbox & security hardening** | Copilot CLI (#4521, #4522, #4524), Gemini (#28898), Codex (#39307, #39299, #39301), Claude Code (#73468) | Respect explicit config over policy, credential isolation, fail-closed risk scoring, macOS sandbox E2BIG fix |
| **MCP lifecycle reliability** | Codex (#30408, #38754), Copilot CLI (#4392, #3698, #4096), Gemini (#28863) | Orphaned process reaping, OAuth token bridging, server reconnect/credential refresh, policy false-positives |
| **Billing transparency** | Claude Code (#81703, #83062), OpenCode (#33495, #43208, #42935), Copilot CLI (#4511) | Plan vs. usage reconciliation, quota reset correctness, real-time cost display |
| **Multi-account / identity separation** | Codex (#20500, 107👍), Copilot CLI (#2904), OpenCode (#3787) | Named accounts per connector, per-mode model config, privacy boundaries |
| **Context / memory management** | Codex (#39144), Claude Code (#87783), Gemini (#7040), Qwen Code (#9331) | Auto-memory provenance, context allocation consistency, rewind/compress coherency |
| **AST-aware code intelligence** | Gemini (#22745), Codex (#39296) | Precise method reads, reduced token noise, surgical context loading |
| **i18n / localization** | CodeWhale (#5482, #5337) | Chinese documentation, dictionary-driven UI strings |

---

## 4. Differentiation Analysis

### Claude Code — The Enterprise Incumbent
- **Focus:** Deep IDE integration, copilot-style assistants, compliance (cyber safeguard approvals)
- **Target:** Large enterprises with existing Copilot/Claude contracts
- **Pain points:** Billing disputes ($1,600+ aggregated), cross-session messaging broken, Cowork VM Intel Mac regressions
- **Unique:** VSCode panels, sandbox-exec integration, Cowork VM

### OpenAI Codex — The Developer-Centric CLI
- **Focus:** TUI-based workflows, session exploration (fork/archive), security hardening partnerships
- **Target:** Independent developers and power users who value TUI efficiency
- **Pain points:** Windows instability (40% of top issues), MCP leaks, guardian scoring
- **Unique:** Session forking, Markdown export, Guardian v2, MCP hooks

### Gemini CLI — The Research-Driven Platform
- **Focus:** Agent memory (auto-memory), AST-aware tools roadmap, subagent reliability, evaluation infrastructure (76 behavioral evals)
- **Target:** Researchers and ML engineers requiring reproducible, token-efficient workflows
- **Pain points:** Agent hangs (#21409: 8👍), model ID rewrite bugs, false loop detection
- **Unique:** gVisor runsc sandbox, auto-memory retry logic, SSR agent eval framework

### GitHub Copilot CLI — The Enterprise Reluctant Convert
- **Focus:** Compliance, policy governance, org model catalogues, sandbox enforcement
- **Target:** GitHub Enterprise customers — less innovation-driven, more security-policy-driven
- **Pain points:** Sandbox regressions overriding user config, MCP child leaks, model availability gaps
- **Unique:** Policy-defined sandbox, per-agent usage metrics, Copilot plan integration

### Qwen Code — The Multi-Agent Experimenter
- **Focus:** Agent teams, boards, live-session registry, self-hosted review/CI infrastructure
- **Target:** Teams running agent-driven workflows internally (dogfooding its own tools)
- **Pain points:** P1 API error #656 (11 months), team messaging ambiguity, autofix storms (59% cancel rate)
- **Unique:** Agent boards, mutation-verified testing, `/review` fan-out, ACP sessions

### OpenCode — The Community-Governed Platform
- **Focus:** Provider extension (OpenAI-compatible, Zen, DeepSeek, CommandCode), feature-driven velocity
- **Target:** Developers experimenting with multiple provider backends
- **Pain points:** Billing/quota confusion (multiple duplicate issues), session ID rollover bug, silent failures
- **Unique:** 5x faster iteration, bot contributions, "needs:issue" culture, 50 issues + 50 PRs in 24h

### Pi — The Reliability-Focused OpenSource
- **Focus:** Bug-fix velocity, provider SSE stability, TUI rendering polish, self-hosted extension points
- **Target:** Developers who value open-source control and reliable long-running sessions
- **Pain points:** Stream stalls, context overrides, Windows npm cold-start
- **Unique:** 128k defaults for OpenAI-compatible, streaming watchdog, extension hooks (agent_recovery_exhausted)

### CodeWhale / DeepSeek TUI — The Renaming Rebrand
- **Focus:** Chinese i18n, git chrome (repo/worktree state), session durability, release automation
- **Target:** Chinese-speaking developers + global deepseek power users migrating from deepseek-tui
- **Pain points:** System prompt dropping (fixed), Windows status indicator regression, SSE UTF-8 corruption
- **Unique:** OrcaRouter aggregator pricing, `/title` vs `/rename` separation, Task Manager workers

---

## 5. Community Momentum & Maturity

## 6. Trend Signals

### Maturity Ranking (by community size & engagement)

| Tier | Tools | Evidence |
|------|-------|----------|
| **Mature / High-Engagement** | Claude Code, Codex, Copilot CLI | High issue comments, sustained PR volume, dedicated release cadence |
| **Growing Fast** | Gemini CLI, OpenCode, Qwen Code, Pi | Rapid PR velocity, frequent releases, new feature epics |
| **Niche / Emerging** | Kimi Code CLI, CodeWhale | Lower issue volume, focused user bases |

### Velocity Ranking (by release/PR frequency)

| Rank | Tool | Release Cadence |
|------|------|-----------------|
| 1 | OpenCode | 50 PRs / 50 issues updated in 24h |
| 2 | Qwen Code | 10+ PRs, nightly releases |
| 3 | Gemini CLI | 12 PRs, nightly releases |
| 4 | Pi | 10 PRs, no release today |
| 5 | Codex | 10 PRs, major release today |
| 6 | CodeWhale | 10 PRs, v0.9.9 today |
| 7 | Claude Code | 1 PR, patch release |
| 8 | Copilot CLI | 1 spam PR, hotfix release |
| 9 | Kimi Code | 2 PRs, no release |

### Key Patterns
- **Codex and Copilot CLI** are shipping at enterprise-scale cadence with security hardening PRs
- **Qwen Code and Pi** are iterating fastest on agentic features
- **Kimi Code** appears dormant/emerging — watch for maintainer response
- **Claude Code's** quiet PR day suggests internal-branch pre-releases rather than community-driven velocity

---

## 7. Trend Signals

### For Developers

1. **Agent orchestration is the next battleground.** Cross-session messaging, agent boards, subagent recovery, and session forking are being actively shaped across Qwen, Codex, Claude, and Gemini. Expect agent-team workflows to stabilize in 2-4 quarters.

2. **Reliability beats features.** The #1 user complaint across all tools is **silent failure** — messages that report success but never arrive, prompts that vanish, sessions that revert to wrong points. The tool that wins on explicit error states and fail-closed behavior will build durable trust.

3. **Sandboxing is maturing from optional to enforced—but badly.** Copilot CLI's sandbox regressions and Claude's macOS E2BIG show enforced sandboxing is still causing conflicts. Expect sandbox-aware permission systems (heredoc handling, path grants, JVM processes) to become must-have compatibility features.

4. **Billing transparency is a differentiator.** Multiple high-profile disputes (#81703/$604, #83062/$995, OpenCode's Zen balance issues) show usage-tracking and plan-allowance UI are table-stakes. Expect per-agent cost dashboards and real-time quota monitoring.

5. **Enterprises are standardizing on policy-driven governance.** Models missing from org catalogues, managed settings files (Codex #39306), and sandbox policy overrides define the enterprise requirements. Expect MDM/OIDC integration to become a check-box.

6. **Localization is an underserved opportunity.** CodeWhale's Chinese loCalization EPIC (#5482) and the growing Chinese language user base signal an underserved market. No other tool has a documented i18n roadmap — early movers will capture this audience.

7. **Windows remains the weakest platform.** Across Codex, Copilot, Ollama (PopenCode), Cowork VM Intel Macs, and Claude Code desktop, Windows-specific regressions dominate. Expect a strategic push toward Windows parity as a competitive advantage.

8. **The model context ceiling is becoming a governance issue.** Unequal context allocations (Codex #39144), model ID rewrites (Gemini #28859), and fixed context overrides (Pi #8332) highlight that context-window management is now a platform-level concern, not just a tuning knob.

---

**Recommendation for technical decision-makers:**

- **For AI-first teams**: Evaluate Qwen Code or Pi for their agentic extensibility; monitor Codex's TUI as a UX benchmark.
- **For enterprise compliance**: Copilot CLI and Claude Code remain the safest, but only if sandbox regressions are resolved.
- **For multi-provider flexibility**: OpenCode's provider-agnostic focus offers the most freedom, but billing transparency needs hardening.
- **Watch out**: All tools share MCP lifecycle weaknesses; treat MCP-dependent workflows as risk until reaping/credential refresh bugs are closed.

---

*Compiled from community digest data for 2026-08-19. All statistics are from the referenced GitHub repositories and community reports.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-08-19 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

Most-discussed pull requests by engagement, representing the community's most active contributions:

### 🥇 **skill-creator — eval infrastructure fixes** ([PR #1298](https://github.com/anthropics/skills/pull/1298))
**Status:** OPEN | Author: MartinCajiao | Updated: 2026-06-23
Fixes `run_eval.py`'s persistent `recall=0%` reporting (cross-referencing [Issue #556](https://github.com/anthropics/skills/issues/556) with 10+ independent reproductions). The core problem: description-optimization loops were optimizing against noise. The fix installs eval artifacts as real skills and addresses Windows stream-reading and parallel-worker issues. **Highest-traffic PR** — critical because the eval pipeline underpins every skill's quality loop.

### 🥈 **document-typography — typographic quality control** ([PR #514](https://github.com/anthropics/skills/pull/514))
**Status:** OPEN | Author: PGTBoos | Updated: 2026-03-13
Prevents orphan word wraps, widow paragraphs, and numbering misalignment — issues that affect every AI-generated document. Distinctive: addresses a *quality ceiling* problem rather than feature gaps.

### 🥉 **fix(pdf) — case-sensitive file references** ([PR #538](https://github.com/anthropics/skills/pull/538))
**Status:** OPEN | Author: Lubrsy706 | Updated: 2026-04-29
Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` that break on case-sensitive filesystems. Small but demonstrates the community's growing attention to cross-platform reliability.

### 4. **ODT skill — OpenDocument creation & conversion** ([PR #486](https://github.com/anthropics/skills/pull/486))
**Status:** OPEN | Author: GitHubNewbie0 | Updated: 2026-04-14
Adds .odt/.ods/.odf support: creation, template filling, and parse-to-HTML conversion. Expands the document skills family beyond existing docx/pdf coverage.

### 5. **frontend-design — clarity & actionability** ([PR #210](https://github.com/anthropics/skills/pull/210))
**Status:** OPEN | Author: justinwetch | Updated: 2026-03-07
Revises the frontend-design skill for clearer, single-conversation actionable instructions. Discussion centers on making every instruction something Claude can actually follow — a recurring theme in the ecosystem.

### 6. **skill-quality-analyzer + skill-security-analyzer** ([PR #83](https://github.com/anthropics/skills/pull/83))
**Status:** OPEN | Author: eovidiu | Updated: 2026-01-07
Two meta-skills: quality analysis across five dimensions (structure, docs, examples, resources) plus a dedicated security analyzer. One of the oldest active PRs (Nov 2025), reflecting sustained demand for quality/security guardrails.

### 7. **self-audit — verification + reasoning gate** ([PR #1367](https://github.com/anthropics/skills/pull/1367))
**Status:** OPEN | Author: YuhaoLin2005 | Updated: 2026-07-02
Mechanical file verification followed by a four-dimension reasoning audit in damage-severity order. Universal applicability — any project, stack, or model.

---

## 2. Community Demand Trends

From Issues (sorted by comments), the most-anticipated directions:

| Trend | Signal | Evidence |
|-------|--------|----------|
| **Security & trust hardening** | 🔥 Strongest demand (43 comments) | [#492 — trust boundary abuse](https://github.com/anthropics/skills/issues/492): community skills distributed under `anthropic/` namespace impersonate official skills, creating privilege-escalation risks |
| **Enterprise org sharing** | High (16 comments, 8 👍) | [#228 — org-wide skill sharing](https://github.com/anthropics/skills/issues/228): direct skill library or sharing links instead of manual .skill file downloads |
| **Eval/reliability infrastructure** | High (12 comments, 7 👍) | [#556 — `claude -p` never triggers skills](https://github.com/anthropics/skills/issues/556): 0% trigger rate undermines skill description optimization |
| **Dedup & context efficiency** | Medium (6 comments, 9 👍) | [#189 — duplicate skills in plugins](https://github.com/anthropics/skills/issues/189): identical skills across `document-skills`/`example-skills` bloat context window |
| **Context window management** | Emerging | [#1487 — claude-api injects ~156k tokens](https://github.com/anthropics/skills/issues/1487): single tool call exhausts full context window |

**Notable pattern:** The #1 demand is *not* new skill functionality — it's **trust, governance, and reliability**. Security (#492), org sharing (#228), and eval reliability (#556) dominate. Enterprise adopters are hitting production-scale problems.

---

## 3. High-Potential Pending Skills

Active PRs not yet merged, likely to land soon:

| Skill | PR | Notes |
|-------|-----|-------|
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Comprehensive: Testing Trophy model, AAA pattern, React Testing Library. Author 4444J99. Updated 2026-04-21 |
| **ServiceNow platform skill** | [#568](https://github.com/anthropics/skills/pull/568) | Broad enterprise coverage: ITSM, ITOM, ITAM/SAM, FSM, HRSD, CSM, SPM, Vulnerability Response. Updated 2026-08-12 — still active |
| **pyxel retro game development** | [#525](https://github.com/anthropics/skills/pull/525) | MCP server wrapper for the Pyxel engine — write → run_and_capture → iterate workflow. Updated 2026-07-15 |
| **self-audit (v1.3.0)** | [#1367](https://github.com/anthropics/skills/pull/1367) | Mechanical verification + reasoning quality gate. Author YuhaoLin2005 also proposed the extended pipeline in [#1385](https://github.com/anthropics/skills/issues/1385) |
| **Windows compatibility fixes** | [#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050) | Two PRs fixing Windows subprocess/encoding bugs in skill-creator — prerequisite for broader adoption |

**Watch for:** The `skill-creator` Windows fixes (#1298, #1099, #1050) cluster — three independent authors hitting the same broken pipeline strongly suggests imminent consolidation.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliability, security, and quality-assurance infrastructure around Skills themselves** — not new skill functionality — with 43-comment debates on trust boundaries, broken eval pipelines, and context-window exhaustion signaling that enterprise adoption is hitting production-scale pain points.

---

# Claude Code Community Digest — 2026-08-19

## Today's Highlights

A new patch release (v2.1.235) adds an optional spellcheck feature for the prompt input while fixing cache invalidation bugs related to language server reconnects. The community remains focused on a long-running cyber safeguard false-positive issue (#84352) that has drawn 121 comments, alongside a cluster of new Cowork VM regressions on Intel Macs and Windows. Cross-session messaging reliability continues to be a major pain point, with several new reports of silently dropped or hung messages.

## Releases

**v2.1.235** — [Release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.235)
- Added optional `spellcheck` setting that underlines misspelled words in the prompt input as you type (uses installed `aspell`, `hunspell`, or `ispell`)
- Fixed whole-prompt-cache invalidation when a language server disconnected or reconnected mid-session
- Fixed nested m (truncated in source data — likely a nested menu or markdown fix)

## Hot Issues

1. **[#84352 — CVP-approved org still receives cyber safeguard blocks](https://github.com/anthropics/claude-code/issues/84352)** (121 comments, 20 👍)
   A previously approved Claude.ai organization is again getting cyber-safeguard blocks, and the Verification Portal shows the application as "Under review" despite prior approval. This is the highest-activity issue by far and suggests a systemic false-positive problem affecting compliance-approved users.

2. **[#86298 — Windows desktop: cross-session messages silently dropped](https://github.com/anthropics/claude-code/issues/86298)** (19 comments)
   Regression since app 1.28929.0: messages are held for an approval the UI never shows and expire after ~5 minutes. Community reaction highlights this as a silent data-loss bug — the worst kind for trust.

3. **[#32726 — VSCode: panel steals focus](https://github.com/anthropics/claude-code/issues/32726)** (14 comments, 52 👍)
   Long-running feature request (since March 2026) to stop the panel from auto-revealing and stealing focus. Very high upvote count suggests it's a widely felt UX annoyance in IDE workflows.

4. **[#87503 / #87512 / #87759 — Cowork VM broken on Intel Macs after 1.32352.0](https://github.com/anthropics/claude-code/issues/87503)** (11 + 10 + 1 comments)
   A cluster of regression reports: Cowork VM connection timeouts, guest kernel not enumerating NVMe disks, and hangs at ~1.7s boot. Multiple duplicate reports indicate a recent bundle update broke Intel Mac support specifically.

5. **[#73468 — macOS sandbox E2BIG with many git worktrees](https://github.com/anthropics/claude-code/issues/73468)** (9 comments, 5 👍)
   Every sandboxed Bash command fails with `argument list too long` when the Seatbelt profile is passed inline via `sandbox-exec -p` and the repo has many worktrees. Makes the sandbox 100% unusable in that scenario.

6. **[#81703 / #83062 — Billing incidents: usage credits charged despite plan allowance](https://github.com/anthropics/claude-code/issues/81703)** (12 + 1 comments)
   Two separate billing issues: July 17 ($604.71) and August 1 ($995.67) auto-recharges after included limits reset. Users are disputing the charges. This erodes trust in plan/allowance mechanics.

7. **[#86279 / #87694 — send_message cross-session never delivers](https://github.com/anthropics/claude-code/issues/86279)** (4 + 2 comments)
   `mcp__ccd_session_mgmt__send_message` returns success to sender, renders in recipient UI, but no turn is ever created — recipient hangs indefinitely. Multiple variants filed, suggesting a systemic issue in the session-messaging subsystem.

8. **[#86962 — Cross-session messaging blind to Remote Control connection](https://github.com/anthropics/claude-code/issues/86962)** (3 comments)
   Messaging subsystem reports "Remote Control is not connected" while the same session is live-verified as connected. Both directions fail on a two-machine setup meeting all documented preconditions.

9. **[#87560 — Desktop: conversation view rewinds after auto-update](https://github.com/anthropics/claude-code/issues/87560)** (4 comments)
   After stealth-relaunch, the navigation history is saved with a stale `active` index, sending users back to old conversations. A confusing, jarring UX after an automatic update.

10. **[#87750 — Cowork browser fallback crashes app on Windows](https://github.com/anthropics/claude-code/issues/87750)** (1 comment, 1 👍)
    After a crash in the browser fallback, the app is unable to launch ("This app can't open") and the issue recurs even after reinstall. A hard-to-recover-from desktop bug.

## Key PR Progress

Only 1 PR was updated in the last 24h, so this section is limited:

- **[#41611 — Add the missing source to claude code](https://github.com/anthropics/claude-code/pull/41611)** (open since March 2026)
  A long-dormant PR aiming to add a missing source reference to the project. No reviewer activity visible in the last 24h. Given the complete lack of recent PR activity, this suggests either a quiet development cycle or that fix work is happening in internal branches ahead of release.

## Feature Request Trends

- **Spellcheck (just shipped)** — The new v2.1.235 release directly addresses a long-standing request to catch typos in prompts before sending. Expect follow-ups about dictionary customization and per-project dictionaries.
- **IDE focus control** (#32726, 52 👍) — Stop the VSCode panel from auto-revealing and stealing focus. High upvotes indicate this is a top UX annoyance.
- **Instruction-following improvements** (#13689) — The model still fails to follow instructions in some long-session contexts. Broad, ongoing request with no obvious single fix.
- **Auto-memory provenance** (#87783) — Auto memory persists claims but not observations; users can't distinguish drifted notes from never-bound ones. Growing memory-related issue cluster.
- **Remote Control persistence** (#85269) — Supervisor exits 5s after last client detaches, making overnight availability impossible. Mobile-first workflows are blocked.
- **MCP OAuth scope control** (#83679) — Users want custom "scope" values from `.mcp.json` respected, not hardcoded defaults.

## Developer Pain Points

1. **Cross-session messaging is unreliable** — At least 4 distinct issues this week (#86298, #86279, #87694, #86962) describe messages that report success but never arrive, sessions that hang permanently, and discovery that's blind to live connections. This is the most fragmented and actively-reported problem area.

2. **Cowork VM regressions on Intel Macs** — The 1.32352.0 bundle update broke Intel Mac support in multiple ways (NVMe enumeration, vsock connection, boot hangs). Several duplicates filed within 24h — a sign of a large affected user base and a likely hotfix in progress.

3. **Silent data loss / state corruption** — Recurring theme: messages "successfully sent" but never persisted (#86279), sessions reverting to "Ungrouped" after project moves (#87745), conversation history rewinding after auto-update (#87560). Silent loss erodes user confidence more than visible errors.

4. **Billing disputes keep piling up** — The July 17 and August 1 incidents (#81703, #83062) total over $1,600 in disputed auto-recharges across two reports. Expect continued scrutiny of allowance/reset logic.

5. **macOS sandbox unusable in worktree-heavy repos** — The E2BIG issue (#73468) makes the sandbox completely non-functional for monorepo/worktree workflows, forcing users to disable a security feature to get work done.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-19

## Today's Highlights

The 0.148.0 release line brings substantial TUI quality-of-life improvements including Markdown conversation export and session forking. The community is increasingly vocal about Windows-specific regressions, with a critical browser control failure (Trusted RPC path issue) drawing 63 comments and multiple duplicate reports. Security hardening continues across PRs with a focus on sandboxing, auth token isolation, and Guardian v2 risk-scoring reliability.

## Releases

**rust-v0.148.0** — Major TUI update:
- **`/export` command** — export complete TUI conversations to Markdown (clipboard or file). Closes long-awaited issue #2880 (78 👍, 31 comments) requesting Markdown export for external documentation.
- **Session forking** — `codex exec fork` creates forked sessions; archive/restore options added to the TUI resume picker.
- **Draft prompts during initialization** — type prompts while the TUI boots.

**rust-v0.148.0-alpha.23 / alpha.22** — Maintenance releases with no user-facing changes documented.

## Hot Issues

1. **[#39136 — Browser plugin init fails: Trusted RPC dependency not in trusted path](https://github.com/openai/codex/issues/39136)** (63 comments, 19 👍)
   Windows-only failure where the built-in browser plugin cannot initialize due to a Trusted RPC validation error. This is the day's dominant issue with multiple duplicates (#39173, #39236, #39318) — all reporting the same root cause on Windows 11. The ecosystem impact is significant: browser control is a headline feature for the app.

2. **[#32041 — VS Code extension blank webview on Linux](https://github.com/openai/codex/issues/32041)** (56 comments, 3 👍)
   Extension 26.5707.* renders an empty webview on Linux; the prior 26.5623 works but lacks GPT-5.6-Sol support. Linux users are effectively forced to choose between a broken UI and an outdated model.

3. **[#30408 — MCP server processes leak: 9+ GB RSS](https://github.com/openai/codex/issues/30408)** (29 comments, 8 👍)
   App-server spawns a full set of MCP processes for each thread but never reaps them on archive/close. Memory grows unboundedly. Related Windows-specific issue [#38754](https://github.com/openai/codex/issues/38754) reports repeated spawning within a single task.

4. **[#20500 — Multiple named accounts per connector](https://github.com/openai/codex/issues/20500)** (28 comments, 107 👍)
   The most-upvoted open feature request: explicit account selection with hard privacy boundaries for the same app/connector. High demand from enterprise-adjacent users managing personal + work identities.

5. **[#25928 — Submitted prompts randomly disappear before queue on Windows](https://github.com/openai/codex/issues/25928)** (27 comments, 18 👍)
   Cursor/VS Code extension loses prompts intermittently before they enter the queue. High frustration: work is silently lost with no error.

6. **[#37403 — macOS regression: Remote Control thread resume fails](https://github.com/openai/codex/issues/37403)** (25 comments, 18 👍)
   After the August 7 update, resuming a thread from Remote Control throws `already has an active writer`. Breaks an established mobile-to-desktop workflow.

7. **[#35119 — WSL repos misidentified as non-Git](https://github.com/openai/codex/issues/35119)** (23 comments, 17 👍)
   Since 26.721.3404, valid WSL ext4 repositories are flagged as non-Git with "Git is unavailable." A clear regression from 26.715.10079.0.

8. **[#39144 — GPT-5.6 Sol stuck at 272K context after rollout](https://github.com/openai/codex/issues/39144)** (6 comments, 2 👍)
   Post long-context rollout, Sol retains a 272K `max_context_window` while Terra and Luna receive 872K. Closed, presumably addressed in 0.148.0 — worth verifying.

9. **[#38787 — thread/resume quadratic on large threads](https://github.com/openai/codex/issues/38787)** (4 comments)
   Opening large threads from iOS Remote times out due to quadratic resume behavior. Impact grows as threads accumulate history.

10. **[#39054 — Rejected MCP OAuth refresh tokens stay "usable"](https://github.com/openai/codex/issues/39054)** (5 comments)
    Codex retries rejected refresh tokens indefinitely across all versions 0.140.0–0.148.0-alpha.20, never surfacing re-authentication. Reproduced with a custom app-server.

## Key PR Progress

1. **[#39322 — Enforce workspace restrictions for header authentication](https://github.com/openai/codex/pull/39322)** — Validates externally supplied header credentials against ChatGPT workspace restrictions via `chatgpt-account-id`. Rejects missing/disallowed account IDs. Important for multi-tenant deployments.

2. **[#39319 — Add async user message tool](https://github.com/openai/codex/pull/39319)** — Adds `send_user_message_async` for root agents: emits text as an async agent message and returns immediately without ending the turn. Changes agent interaction semantics.

3. **[#39316 — Support Edu Plus and Edu Pro plans](https://github.com/openai/codex/pull/39316)** — Recognizes `edu_plus`/`edu_pro` across auth, rate limiting, and account schemas. Education-sector eligibility expansion.

4. **[#39314 — Run hooks with captured session environment](https://github.com/openai/codex/pull/39314)** — Captures process environment at hook-registry creation; clears live env before launching hooks; applies hook-spec overrides. Improves hook determinism and security isolation.

5. **[#39311 — Bind unified exec approvals to shell executables](https://github.com/openai/codex/pull/39311)** — Trust in an inner command no longer implicitly trusts the executable that runs it. Unfamiliar executables are evaluated alongside parsed commands. A deliberate security tightening against argument-ignoring binaries.

6. **[#39307 — Fail closed on Guardian V2 risk-scoring errors](https://github.com/openai/codex/pull/39307)** — Config/serialization/thread/classification errors now elevate risk instead of retaining prior low-risk results. Prevents silent approval bypasses.

7. **[#39301 — Prevent Node REPL auth tokens from reaching child processes](https://github.com/openai/codex/pull/39301)** — Adds `NODE_REPL_AUTH_TOKEN` to the non-inheritable environment list, stripped case-insensitively after policy overrides. Direct auth-exfiltration hardening.

8. **[#39299 — Restrict agent roles to bounded config overrides](https://github.com/openai/codex/pull/39299)** — Child agents can customize model behavior and developer message, but cannot change provider configuration or expand authority inherited from parent sessions.

9. **[#39296 — Enable MCP tool hooks in Codex sessions](https://github.com/openai/codex/pull/39296)** — `mcp_tool` hooks now execute through the shared MCP runtime, restricted to connected, cataloged, policy-allowed tools. Unavailable servers fail immediately.

10. **[#39294 — Increase SQLite log sink batching](https://github.com/openai/codex/pull/39294)** — Queue capacity 512→2,048; insert batch 128→512; flush interval 2→10s. Lower I/O pressure for logging-heavy workloads.

## Feature Request Trends

- **Multi-account management** ([#20500](https://github.com/openai/codex/issues/20500), 107 👍): Named accounts per connector with explicit selection and hard privacy boundaries. The single most-supported open request.
- **Markdown export** ([#2880](https://github.com/openai/codex/issues/2880), 78 👍): Now shipped in 0.148.0 via `/export`; long-requested for documentation workflows.
- **Session lifecycle tools** — Fork ([#39269](https://github.com/openai/codex/issues/39269)), archive, restore: fork support lands in 0.148.0, but voice-chat forks lose context and model selection.
- **Managed/MDM configuration support** ([#39306](https://github.com/openai/codex/pull/39306)): Enterprise deployment is a clear strategic priority, with managed-file settings now influencing project discovery.

## Developer Pain Points

- **Windows instability cluster**: The Trusted RPC browser failure (#39136 + 3 duplicates), prompt loss (#25928), WSL Git misdetection (#35119), MCP re-spawning (#38754), and untracked runtime paths (#27230) paint a picture of Windows as the least-polished platform. The Windows issue count in this digest is disproportionate — roughly 40% of the top issues.
- **MCP process/resource leaks** (#30408, #38754): Memory grows without bound; stdio servers repeatedly spawned and never reaped. Matters for anyone running long-lived app-server processes.
- **Stale subagent UI state** (#23930, #35209): Completed subagents remain visibly "Active"; the close/readback path reports no live agent but the UI disagrees.
- **Context window inconsistency** (#39144): Model variants receiving unequal context allocations erodes trust in the rollout process.
- **OAuth failure modes** (#39054, #32164): Rejected tokens never surface re-authentication; Windows enrollment never completes. Silent auth failures are disproportionately costly for developers.
- **Custom model provider friction** (#31354, #36942): MCP tools rejected by non-OpenAI Responses API backends; no flatten-to-functions option. Community workarounds required.
- **Remote/mobile workflow regressions** (#37403, #38787): Thread resume breaking after updates is a recurring pattern this week.
- **Terminal scrollback corruption over SSH** (#24235): TUI remains unreliable on mobile SSH clients, affecting remote-only workflows.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-19

## Today's Highlights

The Gemini CLI team shipped a new nightly release (v0.56.0-nightly.20260818) with SSR Agent fixes for privacy notice wording and TypeScript strict-null errors in integration tests. Meanwhile, a wave of community-contributed PRs landed, addressing long-standing issues around symlinked agent files (#20079), false-positive loop detection (#18551), and OAuth callback timeout crashes (#28512). On the bug front, two high-priority P1 issues remain hot: subagent recovery incorrectly reporting `GOAL` success after hitting `MAX_TURNS` (#22323), and the generalist agent hanging indefinitely on simple tasks (#21409).

---

## Releases

**v0.56.0-nightly.20260818.g194edea47** — Nightly build with two SSR Agent fixes:
- Clarified privacy notice wording and selection options (#28820)
- Fixed TypeScript strict-null errors in integration tests

---

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** · P1 · 12 comments
   The `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` even when it hit the maximum turn limit before doing any analysis. This is dangerously misleading — users think analysis completed when it never started. Community reaction: 2 👍, currently in need-retesting.

2. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** · P1 · 8 comments · 8 👍
   Whenever the CLI defers to the generalist agent, it hangs indefinitely — even for trivial tasks like folder creation. Users report waiting up to an hour before canceling. Workaround: instruct the model not to use subagents. High community engagement signals this is a widespread pain point.

3. **[#19873 — Zero-Dependency OS Sandboxing & Post-Execution Intent Routing](https://github.com/google-gemini/gemini-cli/issues/19873)** · P2 · 8 comments
   Proposal to leverage Gemini 3's native bash affinity by introducing OS-level sandboxing that routes post-execution intent safely. The goal: let the model use its preferred POSIX toolchain (`grep`, `cat`, `sed`, `awk`) without compromising security. Suggests a long-term architectural direction.

4. **[#24353 — Robust component-level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** · P1 · 7 comments
   Epic following up on behavioral evals. Current state: 76 behavioral eval tests running across 6 Gemini models. The ask is to extend this to component-level testing — a significant investment in eval infrastructure.

5. **[#22745 — Assess AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** · P2 · 7 comments
   Investigation into whether AST-aware tools can reduce token noise by precisely reading method bounds in a single call. Potential to cut context bloat (currently ~36.6k tokens/turn baseline) and improve navigation accuracy.

6. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** · P2 · 6 comments
   Anecdotal but resonant: the model rarely self-initiates custom skills or sub-agents, even when highly relevant (e.g., user has `gradle` and `git` skills defined but the model ignores them). Only works when explicitly instructed — suggesting poor tool-discovery heuristics.

7. **[#25166 — Shell command execution stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** · P1 · 4 comments · 3 👍
   After simple CLI commands complete, the shell hangs showing "Awaiting user input" indefinitely. Reproducible with trivial commands that never prompt. Currently need-information; community wants this fixed ASAP.

8. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** · P2 · 5 comments
   Auto Memory only marks sessions processed when the extraction agent successfully reads the transcript. Low-signal sessions that the agent skips remain unprocessed and resurface repeatedly — infinite retry loop wasting resources.

9. **[#28859 / #28893 — Flash model ID rewrite breaking explicit model IDs](https://github.com/google-gemini/gemini-cli/issues/28859)** · P1
   The Gemini 3.5 Flash rollout rewrite incorrectly rewrites explicit model IDs like `gemini-3.6-flash` and `gemini-3.7-flash`. A fix PR is already open (see below), demonstrating the team's fast response to model migration issues.

10. **[#20079 — Symlinked agent markdown files not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** · P2 · 4 comments
    Agent files in `~/.gemini/agents/` that are symlinks get silently ignored. A fix PR (#28883) was merged today — a good example of community-reported issues getting quick resolution.

11. **[#18240 — Markdown table text wrapping](https://github.com/google-gemini/gemini-cli/pull/18240)** · P1/P2 · Large PR
    Adds robust text wrapping and intelligent column-width allocation for markdown tables. Closed today after being open since February — a long-awaited UX improvement for wide tables.

---

## Key PR Progress

1. **[#28892 — Preserve empty text turns with tools or media](https://github.com/google-gemini/gemini-cli/pull/28892)** · Open
   Fixes chat history validation so model turns with empty text parts are preserved when they carry tool requests, tool responses, or media. Prevents context corruption in mixed-content turns.

2. **[#28898 — Harden subprocess execution security](https://github.com/google-gemini/gemini-cli/pull/28898)** · Open
   Prevents credential leakage into untrusted tool execution environments. Sanitizes config ingestion and hardens GitHub API interactions — a security-focused improvement for the PR generator core.

3. **[#28883 — Support symlinked agent markdown files](https://github.com/google-gemini/gemini-cli/pull/28883)** · Closed
   Fixes #20079: agent discovery and loader functions now follow symlinks in `~/.gemini/agents/`. Small fix (size/s) with meaningful impact for users who manage dotfiles via symlinks.

4. **[#28877 — Fix false-positive loop detection on uniform streaming content](https://github.com/google-gemini/gemini-cli/pull/28877)** · Closed
   Loop detection was triggering on consecutive spaces or uniform padding in streamed responses — a false alarm that interrupted sessions. Fixes #18551.

5. **[#28873 — Prevent unhandled promise rejection on OAuth callback timeout](https://github.com/google-gemini/gemini-cli/pull/28873)** · Closed · P1
   The 5-minute OAuth callback timeout caused an unhandled rejection crash. Now properly caught and handled. Fixes #28512.

6. **[#28870 — Emit pending tool call update before requesting permission](https://github.com/google-gemini/gemini-cli/pull/28870)** · Closed · P1
   In ACP mode, tool permission requests now send a `pending` status update first — fixing a protocol violation that caused clients to desynchronize. Fixes #21783.

7. **[#28893 — Preserve explicit flash model IDs](https://github.com/google-gemini/gemini-cli/pull/28893)** · Open · P1
   Restricts the Gemini 3.5 Flash rollout rewrite to the generic `flash` alias. Explicit IDs like `gemini-3.6-flash` are preserved; invalid IDs pass through to the API for proper rejection. Fixes #28859.

8. **[#28895 — Recognize mixed function-call turns](https://github.com/google-gemini/gemini-cli/pull/28895)** · Open · P2
   Fixes #28894: turns containing both function calls and other content are now correctly recognized. Small fix (size/s) for a subtle parsing bug.

9. **[#28863 — Prompt for consent on environment changes](https://github.com/google-gemini/gemini-cli/pull/28863)** · Open
   Extension updates can no longer inject unauthorized environment variables into MCP server processes. Consent strings now include env config, and custom env vars are sanitized. Addresses a security gap.

10. **[#28641 — Prevent ghost text wrapping infinite loop](https://github.com/google-gemini/gemini-cli/pull/28641)** · Closed
    Fixes an infinite loop in `getGhostTextLines` when input width is narrower than a single wide codepoint (CJK/emoji). Adds a regression test that would hang without the guard. Fixes #19985.

11. **[#28891 — Eval retry 429 rate limit](https://github.com/google-gemini/gemini-cli/pull/28891)** · Open
    The eval retry helper was silently missing 429/`RESOURCE_EXHAUSTED` errors, causing false test failures. Now properly caught and retried. Fixes #28696.

12. **[#28869 — Fix host network resolution for gVisor runsc sandbox](https://github.com/google-gemini/gemini-cli/pull/28869)** · Closed · P2
    VSCode IDE companion extension failed when using `GEMINI_SANDBOX=runsc`. gVisor blocks host TCP access; this PR fixes network resolution. Fixes #21331.

---

## Feature Request Trends

1. **AST-aware code intelligence** (#22745, #22746): Multiple issues push for AST-based file reading, search, and codebase mapping. The goal: fewer turns, less token noise, and more surgical context loading. Recommended starting points: `tilth` or `glyph` tools.

2. **Proactive skill/sub-agent adoption** (#21968, #21432): Community wants the model to automatically use defined skills and sub-agents when relevant — not just when explicitly instructed. Also requested: better self-awareness of CLI flags, hotkeys, and self-execution capabilities.

3. **Destructive behavior guardrails** (#22672): Users want the agent to avoid risky commands like `git reset --force` when safer alternatives exist, and to understand the dangers of modifying shared resources (DBs, etc.).

4. **Agent trajectory transparency** (#22598, #21763): Subagent trajectories are saved but not easily accessible. Requests to expose them via `/chat share` and include subagent context in `/bug` reports.

5. **Security hardening for Auto Memory** (#26525, #26523): Users want deterministic secret redaction before content enters model context and better handling of invalid memory patches rather than silent skipping.

---

## Developer Pain Points

1. **Agent hangs and false success reports** (#21409, #22323, #25166): The most commented issues this week all involve agents that either hang indefinitely, report success when they failed, or get stuck waiting for input that never comes. These destroy trust in automation.

2. **Model not using defined skills/agents** (#21968): Defining skills that get ignored is a major frustration — users invest in configuration that the model never leverages unless forced.

3. **`MAX_TURNS` ambiguity** (#22323): Subagent hitting the turn limit and reporting `GOAL` success is worse than reporting failure — it silently produces incomplete results. Users want honest failure reporting.

4. **Context/token bloat** (#19561, #22745): ~36.6k tokens/turn baseline, large file reads "firehosing" context, and model creating tmp scripts in random spots all contribute to messy, token-heavy sessions.

5. **Rate-limit and quota failures** (#28891): 429 errors silently breaking eval runs and test suites — infrastructure issues that waste developer time debugging false failures.

6. **Configuration and symlink edge cases** (#20079): Small but annoying issues like symlinked agent files being ignored. These are quick wins that improve the developer experience meaningfully.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-19

## Today's Highlights

Release v1.0.81-1 brings Gemini 3.7 Flash support and per-agent usage metrics, but the community is most vocal about sandbox enforcement issues introduced in this version — multiple reports indicate the sandbox activates despite explicit `sandbox.enabled: false` configuration. The conversation around model availability (Anthropic models missing for org-enabled accounts) and MCP server connection reliability continues to dominate open issues.

---

## Releases

**v1.0.81-1** ([release](https://github.com/github/copilot-cli/releases/tag/v1.0.81-1))

**Added:**
- Support for Gemini 3.7 Flash
- Ctrl+E shortcut in `/sandbox` to open `settings.json` in your editor
- Per-agent usage metrics included in `--usage-output-file` JSON output

**Improved:**
- Schedule Manager now uses `x` key to remove scheduled `/every` and `/after` prompts

**Fixed:**
- Corrected issue with turning `allow-all` off

---

## Hot Issues

### 1. **Enabled organization models missing from catalogue** ([#4390](https://github.com/github/copilot-cli/issues/4390))
Models enabled by Copilot Business orgs (Claude Sonnet 5, Opus 5, Kimi K3) are absent from the CLI's effective catalogue. Selecting `claude-sonnet-5` returns "This model is disabled by your..." — a foundational availability bug. **10 comments, 7 👍**

### 2. **Allow scrolling through conversation history** ([#4313](https://github.com/github/copilot-cli/issues/4313))
Mouse wheel and PageUp/PageDown don't navigate session history in the terminal UI. A long-standing UX gap for long sessions. **8 comments**

### 3. **Custom Agent YAML should support reasoning effort per agent** ([#2904](https://github.com/github/copilot-cli/issues/2904))
`.agent.md` files can pin a model but not reasoning effort — it remains globally configured only. High demand: **7 comments, 20 👍** — the most-upvoted issue in this digest.

### 4. **MCP registry false-positive: custom servers blocked by policy** ([#3162](https://github.com/github/copilot-cli/issues/3162))
CLI 1.0.42 flags registry-listed MCP servers as "blocked by policy" — a false negative in registry validation. Closed but still attracting comments, suggesting incomplete resolution. **7 comments**

### 5. **Third-party MCP OAuth tools never bridged to CLI sessions** ([#4096](https://github.com/github/copilot-cli/issues/4096))
Atlassian Remote MCP shows "Connected" in the app, but tools never surface in CLI sessions — OAuth token bridging failure. **6 comments, 2 👍**

### 6. **Per-mode default model configuration (plan vs. autopilot)** ([#2958](https://github.com/github/copilot-cli/issues/2958))
Users want different default models for plan mode vs. autopilot. Strong support: **4 comments, 16 👍**.

### 7. **Sandbox forces itself despite `sandbox.enabled: false`** ([#4522](https://github.com/github/copilot-cli/issues/4522))
1.0.81 enables sandbox when server-managed policy is temporarily undetermined, overriding explicit user config. Regression in the latest release — **2 comments, 5 👍**.

### 8. **Sandbox cannot be disabled** ([#4521](https://github.com/github/copilot-cli/issues/4521))
Sandbox config shows disabled, but status reports enabled; the CLI keeps attempting sandboxed execution. Related to #4522 — likely the same regression. **2 comments, 3 👍**.

### 9. **Atlassian MCP OAuth broken in 1.0.80 (RFC 8414 §3.3 regression)** ([#4490](https://github.com/github/copilot-cli/issues/4490))
`MCPOAuthError` — issuer mismatch between advertised and discovered metadata. Worked in 1.0.78, broken in 1.0.80. **3 comments**

### 10. **Orphaned stdio MCP processes after authentication rebuild** ([#4392](https://github.com/github/copilot-cli/issues/4392))
At startup, CLI spawns MCP servers, then rebuilds the client post-auth — first-generation stdio processes are never killed, accumulating over time. Degenerates into resource leak. **2 comments**

Also notable: [#3698](https://github.com/github/copilot-cli/issues/3698) documents the same stdio MCP leak class with unbounded child processes pinning CPU, and [#4524](https://github.com/github/copilot-cli/issues/4524) reports the enforced sandbox breaking git access even with full working directory grants — sandbox-related regressions are today's loudest theme.

---

## Key PR Progress

Only **one PR** was updated in the last 24h:

**#3163 — "ViewSonic monitor"** ([PR #3163](https://github.com/github/copilot-cli/pull/3163))
A stale, possibly automated/spam PR referencing unrelated monitor issues (#2591, #3561, #3559) and a GitHub Action runner. It has been open since May 6 and is **not a substantive contribution** to the codebase. **No comments, no 👍.**

**Note:** With no active feature PRs, development appears focused on release stabilization (v1.0.81-1 hotfixes) rather than new feature merges this cycle. Community attention remains on issue triage and bug confirmation.

---

## Feature Request Trends

1. **Per-mode and per-agent model configuration** — Two high-👎 issues ([#2904](https://github.com/github/copilot-cli/issues/2904), [#2958](https://github.com/github/copilot-cli/issues/2958)) both request finer-grained control: reasoning effort per custom agent, and different default models for plan vs. autopilot mode. Users want deterministic model routing, not just global flags.

2. **Sandbox configurability and opt-out** — Multiple issues ([#4521](https://github.com/github/copilot-cli/issues/4521), [#4522](https://github.com/github/copilot-cli/issues/4522)) ask for the sandbox to respect explicit user configuration. Trust in the enforcement is eroding as it blocks legitimate git and JVM workflows.

3. **MCP server lifecycle reliability** — Persistently requested: no orphaned processes ([#4392](https://github.com/github/copilot-cli/issues/4392), [#3698](https://github.com/github/copilot-cli/issues/3698)), auth bridging for OAuth MCP servers ([#4096](https://github.com/github/copilot-cli/issues/4096)), and no false-positive policy blocks ([#3162](https://github.com/github/copilot-cli/issues/3162)).

4. **Terminal UX improvements** — Scrolling through conversation history ([#4313](https://github.com/github/copilot-cli/issues/4313)) and search/filter in `plugin marketplace browse` ([#4523](https://github.com/github/copilot-cli/issues/4523)) — small but recurrent asks for a better interactive experience.

5. **Credential refresh without restart** — [#3682](https://github.com/github/copilot-cli/issues/3682) wants BYOK provider credentials (short-lived OAuth/OIDC tokens) refreshed at runtime, not only at process start.

---

## Developer Pain Points

- **Sandbox regressions in 1.0.81** — The strongest immediate pain: explicit `sandbox.enabled: false` is overridden by undetermined managed policy ([#4522](https://github.com/github/copilot-cli/issues/4522)); sandbox shows disabled but enforces anyway ([#4521](https://github.com/github/copilot-cli/issues/4521)); and path RW grants aren't honored by JVM processes ([#4516](https://github.com/github/copilot-cli/issues/4516)). The enforced-sandbox build also breaks git despite full-directory grants ([#4524](https://github.com/github/copilot-cli/issues/4524)).

- **MCP server child-process leaks** — stdio servers spawn unbounded, un-reaped processes ([#3698](https://github.com/github/copilot-cli/issues/3698), [#4392](https://github.com/github/copilot-cli/issues/4392)), degrading CPU and machine responsiveness.

- **Model availability inconsistencies for org accounts** — Enabled org models missing from the CLI catalogue ([#4390](https://github.com/github/copilot-cli/issues/4390)), and enterprise accounts failing external lookups with `github-mcp-server` ([#3248](https://github.com/github/copilot-cli/issues/3248)).

- **Session and billing display reliability** — Session AI cost (AIC) display underestimates real consumption for models like Kimi K3 ([#4511](https://github.com/github/copilot-cli/issues/4511)); manual `/rename` gets overwritten by auto-generated names ([#2622](https://github.com/github/copilot-cli/issues/2622)).

- **Configuration and hook frustrations** — `allowed_directories` in permissions config doesn't suppress path-outside prompts ([#4482](https://github.com/github/copilot-cli/issues/4482)); standalone `.github/hooks/*.json` postToolUse hooks never fire ([#4520](https://github.com/github/copilot-cli/issues/4520)); built-in agents ignore custom instructions like "use `uv run python`" ([#1990](https://github.com/github/copilot-cli/issues/1990)).

---

*Digest compiled 2026-08-19 from github.com/github/copilot-cli activity data.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**2026-08-19**

---

## 1. Today's Highlights

Community activity this cycle centers on frontend rendering reliability and the growing adoption of Kimi Code CLI in specialized domains. A notable bug report (#2607) highlights a Web UI rendering regression for non-Kimi provider sessions after tab switches, while a quant-trading content creator has open-sourced a full benchmark report of K3 + Kimi Code for strategy generation (#2608). Additionally, the long-stalled KAOS SSH logging fix (#848) has finally been closed, though no new releases were shipped today.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Hot Issues

**#2607 — [OPEN] Web UI: Assistant messages re-render as one-fragment-per-line after tab switch/reload for non-Kimi providers**
Author: chenxupeng1990-eng | Created: 2026-08-18 | 💬 1 comment | 👍 0
[View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2607)

A critical rendering regression in the Web UI. Messages stream correctly in real-time, but after any remount (tab switch, reload, session reopen), assistant messages for OpenAI-compatible providers break into one streaming delta per line — creating a narrow vertical strip that destroys readability. This affects all non-Kimi providers, making it a high-impact usability bug for users leveraging custom endpoints.

**#2608 — [OPEN] Benchmarked K3 + Kimi Code on out-of-sample quant strategy generation — full report open-sourced**
Author: frank-quant | Created: 2026-08-18 | 💬 0 comments | 👍 0
[View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2608)

A community member running a Chinese-language AI-quant channel (Bilibili/YouTube) has open-sourced a benchmark report using Kimi Code CLI to write an ETH perpetual futures strategy on Freqtrade. This is a strong real-world validation of the tool's coding capabilities under strict constraints. Currently zero comments — community engagement opportunity for the maintainers.

**#2606 — [OPEN] Dev/knowledge plane**
Author: SoMiReMiReDo | Created: 2026-08-18 | 💬 0 comments | 👍 0
[View PR](https://github.com/MoonshotAI/kimi-cli/pull/2606)

A new contributor has submitted a PR proposing a "knowledge plane" concept for the CLI. While the feature scope is unclear, it suggests growing interest in persistent knowledge management inside terminal workflows.

*(Note: Only 2 issues were updated in the last 24h per the data source; the above are the full set.)*

---

## 4. Key PR Progress

**#848 — [CLOSED] fix(kaos): log ssh failures when enabled**
Author: powerfooI | Updated: 2026-08-18
[View PR](https://github.com/MoonshotAI/kimi-cli/pull/848)

After being open since February, this KAOS-related fix has finally been closed. It ensures SSH failures are logged when the logging flag is enabled — improving debuggability for remote operations. The long review cycle suggests it required significant iteration or maintainer back-and-forth.

**#2606 — [OPEN] Dev/knowledge plane**
Author: SoMiReMiReDo | Updated: 2026-08-18
[View PR](https://github.com/MoonshotAI/kimi-cli/pull/2606)

Recently opened PR exploring a "knowledge plane" feature. As a new contribution without prior issue discussion, it may face closure per project guidelines unless maintainers see clear value. Worth watching to gauge maintainer appetite for knowledge-management features.

*(Note: Only 2 PRs were updated in the last 24h per the data source; the above are the full set.)*

---

## 5. Feature Request Trends

Based on historical data and current activity, the most prominent feature directions emerging from the issue tracker include:

- **Provider Compatibility & Rendering Reliability**: The #2607 bug highlights that non-Kimi (OpenAI-compatible) providers are a first-class use case, and the UI must reliably render their output. Expect pressure for a regression fix and test coverage for multi-provider sessions.
- **Persistent Knowledge Management**: The "knowledge plane" PR (#2606) signals community interest in long-term memory/state beyond conversation context — a recurring theme in AI coding tooling.
- **Measured Performance Validation**: Issue #2608 shows community members using Kimi Code CLI in rigorous, reproducible benchmarks (e.g., quant strategy generation) and open-sourcing results. This suggests demand for official benchmarking suites and performance documentation.

---

## 6. Developer Pain Points

- **Web UI Fragility on Remount**: The one-fragment-per-line rendering regression (#2607) is exactly the kind of issue that erodes daily trust — developers switch tabs constantly. The fact that it only manifests for non-Kimi providers suggests insufficient testing coverage for the broader OpenAI-compatible ecosystem.
- **Slow PR Turnaround in Core Areas**: The six-month lifespan of PR #848 (SSH logging fix) points to a bottleneck in review/merge for certain subsystems (KAOS). This can discourage community contributions in infrastructure areas.
- **Contribution Guideline Friction**: PR #2606 was opened without prior maintainer discussion in an issue, which the template explicitly requests. This suggests either contributors are missing the guidance or find the process heavy — a signal to make the "discuss-first" rule more visible.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-19

## Today's Highlights
No new releases shipped in the last 24 hours, but the community remains highly active with 50 issues and 50 PRs updated. The most pressing concerns cluster around OpenCode Go billing/quota inconsistencies—multiple fresh reports describe sudden exhaustion despite paid balances—and a newly discovered message ID timestamp rollover that breaks session ordering. A cluster of older PRs (from July 18) have been swept up by automated cleanup, suggesting maintainers are tidying the queue, while new contributor PRs land daily for TUI fixes, Qwen sampling defaults, and provider documentation.

## Releases
No new releases in the last 24 hours. The latest reported version in use is **v1.18.18**.

## Hot Issues
Here are the 10 most noteworthy issues updated in the last 24 hours:

1. **[#32149 — Opencode Stops Processing Requests Without Response](https://github.com/anomalyco/opencode/issues/32149)** — A long-running (2+ months) critical bug: the app shows "thinking" then silently stops. 15 comments, 6 👍. Open and actively discussed; affects core usability.

2. **[#3787 — [FEATURE]: Linear Agent](https://github.com/anomalyco/opencode/issues/3787)** — Closed feature request (17 comments, 34 👍) to assign Linear issues directly to agents, mirroring Linear's own agentic workflow. High community demand for deeper project-management integration.

3. **[#26338 — [FEATURE]: Add CommandCode as a Provider](https://github.com/anomalyco/opencode/issues/26338)** — Closed with 9 comments and 36 👍. Strong demand for `commandcode.ai` support as a first-class provider/auth option.

4. **[#7648 — Setting to prevent TUI scrolling when new messages stream in](https://github.com/anomalyco/opencode/issues/7648)** — Closed. 11 comments, 18 👍. Users want to read streaming output without the viewport auto-scrolling away.

5. **[#42935 — OpenCode Go quota exhausted in ~20 minutes after DeepSeek V4 Flash cache reads dropped to 0](https://github.com/anomalyco/opencode/issues/42935)** — Fresh and alarming: usage jumped from 11% to 100% in 20 minutes after cache reads collapsed. 4 comments, 3 👍. Touches billing, caching, and provider reliability.

6. **[#43208 — Zen balance has USD 10, but keeps saying 'Free usage exceeded'](https://github.com/anomalyco/opencode/issues/43208)** — New report (3 comments) that paid Zen balances are not lifting free-tier caps. Directly tied to the 429/rate-limit complaints trending.

7. **[#43303 — Message IDs wrapped on 2026-08-14: new messages sort before old ones](https://github.com/anomalyco/opencode/issues/43303)** — A clever find: the 48-bit packed timestamp ID rolled over, making new messages sort *before* old ones, silencing sessions and corrupting history on revert. 2 comments; likely to be a high-priority fix.

8. **[#33495 — Zen balance does not remove free usage cap; paid users still hit 200-request limit](https://github.com/anomalyco/opencode/issues/33495)** — Older but still open (7 comments, 1 👍): duplicates the billing cap complaints with concrete repro across two accounts.

9. **[#43295 — Web UI V2 prompt controls overlap the send button on narrow displays](https://github.com/anomalyco/opencode/issues/43295)** — Usability regression specific to the V2 web TUI; controls render over the submit button on narrow viewports.

10. **[#42748 — message.updated.1 re-serializes summary.diffs on every update, making event writes quadratic in diff size](https://github.com/anomalyco/opencode/issues/42748)** — Performance bug with clear root-cause analysis: full snapshot writes per streamed update cause O(updates × diff) storage blowup.

## Key PR Progress
The following 10 PRs stand out among the 50 updated in the last 24 hours:

1. **[#43314 — fix(session): degrade undecodable image attachments instead of failing the prompt](https://github.com/anomalyco/opencode/pull/43314)** — New (2026-08-19): prevents AVIF/HEIC/BMP images from breaking the whole prompt; degrades gracefully instead. Closes #43262.

2. **[#43310 — [contributor] fix(opencode): remove Qwen sampling defaults](https://github.com/anomalyco/opencode/pull/43310)** — Merged/closed (bot-authored): stops forcing `temperature: 0.55` and `top_p: 1` on all Qwen models, letting provider/server defaults apply. Directly addresses issue #42775.

3. **[#43309 — feat(opencode): make generated title length configurable](https://github.com/anomalyco/opencode/pull/43309)** — Adds `title_max_words` config; caps title generation prompt. Closes #43118.

4. **[#43308 — [contributor] fix(app): limit prompt drag state to files](https://github.com/anomalyco/opencode/pull/43308)** — Bot PR: stops text/link drags (e.g., subagent session cards) from triggering prompt attachment handlers; tags file-tree drags with a custom MIME type.

5. **[#43282 — [needs:issue] fix(core): expose valid subagent IDs in the subagent tool](https://github.com/anomalyco/opencode/pull/43282)** — Closes #36761; documents valid `agent` field values in the `subagent` tool description. Though flagged `needs:issue`, the fix itself is straightforward.

6. **[#42978 — fix(app): show current worktree branch](https://github.com/anomalyco/opencode/pull/42978)** — Fixes branch resolution for manually created Git worktrees when opened in Desktop. Closes #42976.

7. **[#42520 — docs: add SCX.ai to the providers list](https://github.com/anomalyco/opencode/pull/42520)** — Docs-only; SCX.ai provider registration already merged upstream in models.dev.

8. **[#29831 — fix(core): resolve spawn completion on exit, not only close (Windows detached-child hang)](https://github.com/anomalyco/opencode/pull/29831)** — Long-running (since May) fix for shell commands hanging after launching background processes on Windows. Still open; high value.

9. **[#37684 — [automated-pr-cleanup] feat(mcp): bridge runtime-added MCP tools into the core tool registry](https://github.com/anomalyco/opencode/pull/37684)** — Swept up by automated cleanup on 2026-08-18 after 30 days stale. Notable because it addresses the primary user-facing prompt path for runtime MCP tools; worth re-targeting.

10. **[#37678 — [automated-pr-cleanup] feat(session): expose toolChoice via PromptInput and agent config](https://github.com/anomalyco/opencode/pull/37678)** — Also auto-closed after 30 days. Refs #37672 and closes bug #32465; important capability still pending triage.

## Feature Request Trends
Across all issues, the most requested feature directions are:

- **Provider & Model Expansion** — Continuous demand for new providers (CommandCode, SCX.ai) and new model availability in OpenCode Go (Qwen3.8-27B). The ecosystem is growing faster than the integration list.
- **Agent Workflow & Interop** — Linear agent integration (#3787), `/resume` and `/pause` commands (#7226), and subagent tooling improvements.
- **TUI/UX Refinements** — Fine-grained controls over TUI behavior (scrolling, drag targets, narrow-viewport layouts, server switching).
- **Config Extensibility** — A steady stream of requests for configurable knobs: title length, sampling parameters, provider variants.
- **Storage & Performance Optimization** — Repeated asks to stop full-snapshot message writes (#41175, #42748) and to improve context cache invalidation strategy.

## Developer Pain Points
Recurring frustrations from the community this week:

- **Billing & Quota Confusion (High Signal)** — Multiple open issues (#33495, #43208, #42935, #40031, #39891) report mismatches between Zen balance/OpenCode Go quotas and actual usage. The TUI shows different prices than web, quotas "jump" to 100% instantly, and paid users still hit free-tier 429 limits. This is the #1 trust-eroding issue right now.
- **Silent Failures / Hangs** — "No response after thinking" (#32149), tool calls succeeding but OC waiting forever (#43315), sessions permanently stuck (#43277). Users value explicit error states over silence.
- **Windows-Specific Instability** — Detached-child hangs (#29831), MCP stderr drain failures (#37634), and PowerShell quirks keep surfacing as Windows-specific fixes.
- **Data & Storage Bloat** — Multi-GB `opencode.db` growth from full-snapshot event writes is a recurring complaint; developers want delta-based persistence.
- **ID/Ordering Bugs** — The message ID rollover (#43303) and duplicate `project_id` from the same git remote (#42315) are subtle but destructive bugs that erode trust in session/history persistence.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-19

## 1. Today's Highlights
A surge of bug fixes and stability improvements dominated the Pi ecosystem over the last 24 hours, with the most critical being a new stream inactivity watchdog (PR #8330) to prevent hangs when provider SSE streams stall mid-response. Several fixes landed for TUI rendering issues, including long markdown rendering that could freeze the interface and image display bugs in full-screen mode. On the provider front, key PRs address Anthropic fallback pricing, Bedrock redacted reasoning round-tripping, and Copilot login rate-limiting.

## 2. Releases
No new releases in the last 24 hours.

## 3. Hot Issues
1. **[#8331 — Agent loop hangs forever when a provider stream stalls mid-response](https://github.com/earendil-works/pi/issues/8331)** — During an Anthropic 529 overload, four sessions froze mid-turn when SSE streams stopped delivering events without closing. The `for await` in `streamAssistantResponse` waits indefinitely. This critical reliability bug is being addressed by PR #8330.

2. **[#8281 — TUI: full-screen flash on long transcripts](https://github.com/earendil-works/pi/issues/8281)** — With ~10k+ line transcripts, the entire screen clears and redraws with a visible flash when content above the viewport changes. Repeatedly occurs during tool result updates. Related to #8309.

3. **[#8309 — Interface jumps to top and back on long conversations](https://github.com/earendil-works/pi/issues/8309)** — Users on both Windows and Mac report the UI jumping to the top of the transcript then back on each new command execution. A long-standing annoyance per the reporter.

4. **[#8282 — find hangs on Windows with large directories](https://github.com/earendil-works/pi/issues/8282)** — Scanning directories like C:\Windows with built-in `find` completely hangs with no output, consuming high CPU. Community mitigation suggests using `fd`; request to make it the default.

5. **[#8332 — Track Codex's context override ceiling separately](https://github.com/earendil-works/pi/issues/8332)** — GPT-5.6 Sol/Terra/Luna hardcoded at 272K context window default, but their optional context ceiling should be discoverable and refreshable. Currently impossible because `Model` only has a single `contextWindow` field.

6. **[#8251 — GitHub Enterprise Copilot login rate-limits itself](https://github.com/earendil-works/pi/issues/8251)** — Concurrent policy requests via `Promise.all` cause HTTP 429s, invalidating otherwise successful device-flow logins in v0.84.0/0.84.1. PR #8254 proposes a fix.

7. **[#8300 — Two processes share one session file without detection](https://github.com/earendil-works/pi/issues/8300)** — Pi allows two processes to append to the same session JSONL simultaneously with no in-use locking, causing divergent branches and cross-window message delivery.

8. **[#8286 — openai-completions fails over real network, works on loopback](https://github.com/earendil-works/pi/issues/8286)** — Non-deterministic empty output or hallucinated responses when pointing at a remote Ollama host over non-loopback paths, while 127.0.0.1 works reliably.

9. **[#8299 — Windows npm install is 5x slower than release binary](https://github.com/earendil-works/pi/issues/8299)** — The npm package ships unbundled TypeScript output (13k+ files), causing 3.2s startup due to Windows Defender scans on every file open. Docs direct users to the slow path.

10. **[#8298 — pi-claude-cli under --mode rpc hangs on resumed sessions](https://github.com/earendil-works/pi/issues/8298)** — Prompting a resumed session hangs after the user message_end: no assistant message, no turn_end, no agent_settled follows.

## 4. Key PR Progress
1. **[#8330 — Stream inactivity watchdog](https://github.com/earendil-works/pi/pull/8330)** — Adds a watchdog timeout to `streamAssistantResponse` so stalled provider streams no longer hang the agent loop indefinitely. Directly addresses #8331 with a practical solution for provider incidents.

2. **[#8327 — Yield long markdown rendering](https://github.com/earendil-works/pi/pull/8327)** — Adds a `RenderContext` with monotonic deadlines so large Markdown rendering can be chunked, preventing the interactive TUI terminal from freezing during heavy rendering work.

3. **[#8319 — Anthropic fallback usage (proper fix)](https://github.com/earendil-works/pi/pull/8319)** — Threads the actual usage cost from the returned model instead of the originally requested model, correctly handling server-side model fallbacks like `claude-opus-4-8` after `claude-fable-5` refusals.

4. **[#8314 — Round-trip Bedrock redacted reasoning](https://github.com/earendil-works/pi/pull/8314)** — Handles OpenAI models on Bedrock Converse that return encrypted reasoning via `reasoningContent.redactedContent`, preserving this data across turns. Fixes #8315.

5. **[#8254 — Prevent Copilot policy login rate limits](https://github.com/earendil-works/pi/pull/8254)** — Fixes #7850 by fetching the account model catalog before policy updates, updating only known tool-capable unconfigured models, and retrying throttled requests with bounded delay.

6. **[#8307 — Cache-friendly compaction](https://github.com/earendil-works/pi/pull/8307)** — Experimental feature enabling compaction that appends to the main session instead of standalone requests, leveraging warm session caches for significant cost savings.

7. **[#8316 — agent_recovery_exhausted extension hook](https://github.com/earendil-works/pi/pull/8316)** — After native retry and overflow recovery are exhausted, extensions can now hook in, switch models, and continue in the same session rather than settling.

8. **[#8303 — Collapse tool result images until expanded](https://github.com/earendil-works/pi/pull/8303)** — Fixes collapsed tool output still mounting Kitty/iTerm images, causing full-size visual rendering in collapsed views and wasted vertical space.

9. **[#8326 — disabledCommands setting](https://github.com/earendil-works/pi/pull/8326)** — Adds a settings option to hide and block built-in slash commands like `/share` and `/export`, important for organizations concerned about session transcript leakage.

10. **[#8320/#8324 — OpenAI-compatible API provider in /login](https://github.com/earendil-works/pi/pull/8320)** — Adds synthetic provider entries to the login flow for adding OpenAI-compatible endpoints (base URL, model name, API key) with sensible 128k defaults, easing custom provider onboarding.

## 5. Feature Request Trends
- **Extension hook expansion**: Multiple requests for more extension points — pre-persistence message replacement (#8292), agent recovery exhaustion hooks (#8317), namespaced skill identity (#8329), and `disabledCommands` for org control (#8325).
- **Provider configuration UX**: Better on-ramps for custom OpenAI-compatible providers (#8320), locale/language switching UI (#8296), and discoverable context ceilings for models (#8332).
- **Reliability hardening**: Timeout support for OpenAI clients (#8323), stream stall detection (#8331), and session file locking (#8300) show a user-driven push toward production-grade stability.
- **Performance improvements**: Cache-friendly compaction (#8307), `fd` as default file finder (#8282), bundled binaries for Windows (#8299).

## 6. Developer Pain Points
- **TUI rendering glitches dominate this cycle**: Flash on long transcripts (#8281), viewport jumps (#8309), image collapse issues (#8304), and full-screen image rendering errors (#8306) — the interactive terminal experience is under active fire.
- **Rate limiting and 429s**: GitHub Enterprise Copilot logins (#8251) and general provider throttling remain persistent issues for users behind enterprise setups.
- **Network-dependent behavior**: Works on loopback but fails over real networks (#8286) is a frustrating class of bug that's hard to diagnose.
- **Silent failures**: BOM in package.json silently disabling extensions (#8310), `isRecoverableLength` missing exact-limit truncation (#8322), and timeout fields being silently dropped (#8321) — users repeatedly find the system degrading without obvious errors.
- **Resource exhaustion**: Windows `find` hanging on large directories (#8282) and slow npm cold-starts (#8299) highlight platform-specific performance traps.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-19

## Today's Highlights
The team shipped a nightly release (v0.21.11-nightly.20260818) introducing a **live-session registry** with the new `qwen sessions ps` command and daemon-side skill-toggling. Benchmark infrastructure ran three full and two smoke E2E validation passes against SWE-bench Verified and Terminal-Bench 2.0 (one full pass quarantined), while a **P1 regression affecting all API calls (HTTP 400 InvalidParameter)** remains open after ~11 months and is actively discussed. Multi-agent coordination continues to be the hottest theme — new RFCs on cross-session messaging, agent boards, and team-message routing bugs dominate the tracker.

## Releases
**v0.21.11-nightly.20260818.259951c53e**
- `feat(core)`: live-session registry + `qwen sessions ps` command (#8969)
- `feat(daemon)`: attach skill-toggling support

Benchmark releases (dsw-eas-*): Five validation runs against SWE-bench Verified (500 cases) and Terminal-Bench 2.0 (89 cases). One full run (r3) succeeded; one full run (r1) and one smoke (smoke-r1) were quarantined. A new smoke test (smoke-r2) validated end-to-end credential refresh — succeeded.

## Hot Issues
1. **[#656 — P1: API Error 400 `InternalError.Algo.InvalidParameter` on every message](https://github.com/QwenLM/qwen-code/issues/656)** — *Open, 11 comments, created Sep 2025.* Every request fails after 12–16h of use with no config change. Long-running P1 that still affects users; community keeps it alive with environment data points.

2. **[#9194 — Mutation-verified test-pin gaps in review platform](https://github.com/QwenLM/qwen-code/issues/9194)** — *Open, 11 comments.* Automated reviewer found tests that pass despite production mutations — a test-robustness class of gaps. Signals growing rigor in self-hosted CI/review culture.

3. **[#8718 — RFC: Native coordination for independent Qwen sessions](https://github.com/QwenLM/qwen-code/issues/8718)** — *Closed, 10 comments.* Leader/worker dispatch with correlated state observation. Superseded by newer agent-board work but shaped the direction.

4. **[#8316 — Ctrl+C does not restore prompt to input box](https://github.com/QwenLM/qwen-code/issues/8316)** — *Closed, 10 comments.* UX annoyance: cancelled prompts are lost, forcing retyping. High engagement despite being a "small" bug — indicates workflow friction matters.

5. **[#7040 — RFC: Reliable auto-memory recall](https://github.com/QwenLM/qwen-code/issues/7040)** — *Open, 10 comments.* Tracking recall-delivery telemetry (merged), bounded initial-turn recall, and multilingual evaluation (in review). Memory/context management is clearly a top community priority.

6. **[#9276 — Team members cannot send ordinary messages to leader](https://github.com/QwenLM/qwen-code/issues/9276)** — *Open, 7 comments.* Completion/status messages from teammates are misrouted as shutdown requests. Multi-agent correctness bug — directly impacts usability of the new agent-team features.

7. **[#9296 — P1: Qwen Autofix review-event storms waste runner capacity](https://github.com/QwenLM/qwen-code/issues/9296)** — *Open, 5 comments.* 59% of ~500 autofix runs cancelled; reviews on closed/merged PRs still trigger runs. Efficiency problem in the dogfooded CI loop — maintainers actively optimizing their own tooling.

8. **[#8400 — P1: Desktop 0.0.5 / Windows silently auto-deletes sessions](https://github.com/QwenLM/qwen-code/issues/8400)** — *Open, 4 comments.* Sessions vanish after restart when ACP session load fails (cwd mismatch). Data-loss bug in the desktop shell — critical for production use on Windows.

9. **[#9291 — Unsupported image MIME aborts Responses-compatible session](https://github.com/QwenLM/qwen-code/issues/9291)** — *Closed, 4 comments.* `.heic` attachments forwarded as `image/heic` cause request rejection. Edge-case robustness fix — community values graceful handling.

10. **[#9354 — Cross-host chat transcript contract prevalidation](https://github.com/QwenLM/qwen-code/issues/9354)** — *Closed, 5 comments.* Proposes stable transcript schema/versioning across Web Shell, Tauri Desktop, VS Code, and HTML export. Foreshadows export/interop standard work.

## Key PR Progress
1. **[#9402 — feat: agent board — share work across independently started agents](https://github.com/QwenLM/qwen-code/pull/9402)** — *Open.* Repurposed PR; introduces a shared agent board for work distribution across independent sessions. Directly implements the #8718 RFC direction.

2. **[#9436 — Duplicate tool-call ids treated as replays only when args match](https://github.com/QwenLM/qwen-code/pull/9436)** — *Open.* Adds canonical fingerprints (name+args) to the replay guard — prevents false-positive dedup when ids collide with different payloads.

3. **[#9435 — Surface daemon duplicate tool-call breaker as loop-detected stop](https://github.com/QwenLM/qwen-code/pull/9435)** — *Open.* Makes the internal circuit breaker observable via standard loop-detected errors in ACP daemon sessions.

4. **[#9423 — Isolate image payload eviction state](https://github.com/QwenLM/qwen-code/pull/9423)** — *Open.* Consistent image → text-marker rewriting across durable chat history, outgoing requests, and fork snapshots. Prevents memory blowup with inline images.

5. **[#9417 — Keep heredoc bodies out of permission rule splitting](https://github.com/QwenLM/qwen-code/pull/9417)** — *Open.* Fixes #9381: heredocs were split per line, breaking allow rules like `Bash(python *)`. Real-world shell workflow fix for security-tooling correctness.

6. **[#9380 — Measure ACP child peak old-generation heap](https://github.com/QwenLM/qwen-code/pull/9380)** — *Open.* Tracks V8 old-gen high-water marks per ACP child, surfaced via daemon resource poll. Useful for diagnosing memory leaks in long-running serve sessions.

7. **[#9331 — Prevent /rewind dropping history after /compress-fast](https://github.com/QwenLM/qwen-code/pull/9331)** — *Open.* `/compress-fast` emits the same COMPRESSED marker as full compression but isn't a summarizing boundary — rewind was truncating to the wrong point. Bugfix for context-management UX.

8. **[#9389 — Setup wizard recommends live model list](https://github.com/QwenLM/qwen-code/pull/9389)** — *Open.* Provider wizard queries `GET {baseUrl}/models` at setup so recommendations aren't frozen at release time. Modernizes onboarding for evolving provider catalogs.

9. **[#9221 — Run verifier probes in a private scratch worktree](https://github.com/QwenLM/qwen-code/pull/9221)** — *Open.* Isolates the review-verifier's file writes from the shared review worktree — prevents race conditions and inter-agent contamination.

10. **[#8943 — Dispatch review Step 3A fan-out from a generated workflow script](https://github.com/QwenLM/qwen-code/pull/8943)** — *Open.* Opt-in code-driven dispatch for `/review` fan-out, replacing hand-launched orchestrator steps. Automation inside automation.

## Feature Request Trends
- **Multi-agent orchestration** (clearly dominant): coordination primitives (#8718), agent boards (#9402), cross-session messaging (#8724), team-message routing fixes (#9276, #9282), named-teammate flag control (#9430)
- **Memory & context management**: auto-memory recall quality and telemetry (#7040), rewind/compress consistency (#9331), context percentage refresh after compression (#6806)
- **Cross-platform/desktop polish**: session durability on Windows (#8400), transcript portability contracts (#9354), in-app browser panel for Electron shell (#9412)
- **CI/review tooling self-improvement**: flakiness gates (#9125), publish-time convergence advisory (#9278), autofix event storms (#9296)
- **Agent extensibility**: Cursor SDK-backed subagent (#9428), default-off optional agents

## Developer Pain Points
- **API stability**: the 400 InvalidParameter issue (#656) persists across months — a single failure mode blocking all work is the highest-severity complaint.
- **Session/data loss**: silent session auto-deletion on Windows (#8400) and prompt loss on cancel (#8316) erode trust in the interactive shell.
- **Multi-agent confusion**: teammates can't message leaders (#9276), manual task assignment doesn't dispatch work (#9282), `run_in_background: false` ignored (#9430), `list_agents` ambiguous (#9431) — the multi-agent surface ships features faster than the semantics settle.
- **Tooling edge cases**: permission rules break on heredocs (#9417), image MIME aborts sessions (#9291), artifacts not verified against workspace paths (#9083) — security/robustness regressions that interrupt flow.
- **Review/CI fatigue**: autofix storms canceling 59% of runs (#9296), tests passing under mutation (#9194), flaky assertions (~50% failure) (#9125) — the team dogfooding its own `/review` loop is hitting real efficiency ceilings, and the community watches.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-19

## Today's Highlights

The project continues its transition from the legacy `deepseek-tui` name to **CodeWhale**, with v0.9.9 released today. A major architectural effort (EPIC-005) is underway to decompose the TUI crate into modular components, while the community pushes forward on Chinese documentation localization, repository-aware UI chrome, and several critical bug fixes around system prompt handling and SSE UTF-8 decoding.

---

## Releases

### v0.9.9
**Released 2026-08-18**

Codewhale is now the official public product name from Shannon Labs. Key changes in this release:

- **Fixed:** Narrow-terminal compact-row metrics below 60 columns (#5486); strict rustdoc bare URL warnings (#5489)
- **Changed:** Stable concurrency controls for CI workflow jobs (#5495)
- **Breaking:** Legacy npm package `deepseek-tui` is deprecated — no further releases will be published to it. Users on v0.8.x should migrate to the `codewhale` command and package.
- **Note:** Release was folded in via PR #5499, which synchronized root/TUI changelogs and contributor credits.

🔗 [View Release](https://github.com/Hmbown/CodeWhale/releases/tag/v0.9.9)

---

## Hot Issues (10 Selected)

### 1. [#5316 — EPIC-005: CodeWhale TUI Crate Decomposition (Umbrella)](https://github.com/Hmbown/CodeWhale/issues/5316)
**Author:** aboimpinto | **Open** | 7 comments

The master umbrella issue for the TUI crate decomposition. Every sub-EPIC and FEAT reports here, making it the key tracking issue for the project's most significant restructuring effort. Community engagement is high — this will determine how slash commands, DI, and migrations are designed for the foreseeable future.

### 2. [#5505 — System prompt is dropped after `/new`](https://github.com/Hmbown/CodeWhale/issues/5505)
**Author:** LmeSzinc | **Closed** | 2 comments

**Critical bug:** After starting a new session with `/new`, the model receives no system prompt at all — only a folded `<context_update>` line. This is a severe usability regression for anyone relying on project instructions. The bug was reported and closed within 24 hours, suggesting a fix was quickly applied.

### 3. [#5437 — TUI: formalize status-bar color grammar + surface repo/worktree state](https://github.com/Hmbown/CodeWhale/issues/5437)
**Author:** Hmbown | **Open** | 4 comments

An external design review concluded the TUI's color palette is a "color vocabulary" that works — the maintainer agrees to keep it. The actionable follow-up is surfacing repository and worktree state in the header. PR #5511 has already addressed the repo/worktree portion.

### 4. [#5512 — Header status indicator never renders since 0.9.7](https://github.com/Hmbown/CodeWhale/issues/5512)
**Author:** thejayjetson | **Open** | 1 comment

**Regression on Windows:** The `status_indicator` setting (cw / whale / dots / off) rendered in the 0.8.x era but silently stopped working in 0.9.7+. Affects Windows 11 users on Windows Terminal with PowerShell. Likely a rendering issue in newer ratatui versions.

### 5. [#5497 — Terminalize stuck durable executions](https://github.com/Hmbown/CodeWhale/issues/5497)
**Author:** Hmbown | **Open** | 1 comment

A durable Task Manager worker can hang forever when the runtime never emits `turn.completed`. The executor polls every 40ms indefinitely without a grace timeout — a classic resource-leak pattern that could exhaust task workers in production.

### 6. [#5299 — Move npm publication to trusted publishing](https://github.com/Hmbown/CodeWhale/issues/5299)
**Author:** Hmbown | **Open** | 3 comments

**Pain point:** v0.9.5's npm wrapper was gated on a maintainer browser login with 2FA. Every other distribution channel (GitHub, GHCR, Homebrew, CNB, 20 Cargo crates) publishes noninteractively. The fix proposes npm trusted publishing to eliminate the manual step.

### 7. [#5482 — EPIC: Review, restructure, and fully localize documentation to Chinese](https://github.com/Hmbown/CodeWhale/issues/5482)
**Author:** SparkofSpike | **Open** | 1 comment

Recognizes the project's growing Chinese user base. Many docs are English-only, and machine translation introduces errors. The EPIC calls for dedicated per-language folders and migrating existing translations. PR #5507 (Tier 1) has already been submitted.

### 8. [#5337 — Web: finish dictionary spine, retire every `isZh` branch](https://github.com/Hmbown/CodeWhale/issues/5337)
**Author:** Lstarsky0 | **Open** | 5 comments

A continuation of #4934's i18n work. Many page bodies still use two-language ternaries instead of the centralized dictionary. This is the web counterpart to the docs localization EPIC — signaling a strong community push toward proper i18n architecture.

### 9. [#5508 — Continuous loop mode](https://github.com/Hmbown/CodeWhale/issues/5508)
**Author:** M-Maciej | **Open** | 3 comments

**Feature request:** An "infinite turn" option for AI-as-coordinator workflows. Currently users hack around this with sleep cycles inside a single turn. The community wants a native loop until interruption — a pattern relevant to agent orchestration use cases.

### 10. [#5496 — Bound release-candidate and artifact workflow jobs](https://github.com/Hmbown/CodeWhale/issues/5496)
**Author:** Hmbown | **Open** | 0 comments

Follow-up to #5495: the exact-head and post-tag release paths still lack timeout caps. A hung runner on `release-candidate.yml` or `release-artifacts.yml` could stall releases indefinitely. Observed during the v0.9.9 cycle.

---

## Key PR Progress (10 Selected)

### 1. [#5511 — feat(tui): show repository context in git chrome](https://github.com/Hmbown/CodeWhale/pull/5511)
**Author:** wuisabel-gif | **Open**

Addresses the approved repo/worktree status slice of #5437. The TUI header now shows `repo · branch*` (normal checkout) or `repo/worktree · branch*` (linked worktree) with ahead/behind counts. Long names get truncated. Directly implements a community-approved design.

### 2. [#5506 — feat(tui): add command context adapters and migration gate (FEAT-015)](https://github.com/Hmbown/CodeWhale/pull/5506)
**Author:** aboimpinto | **Open**

Core infrastructure for EPIC-005. Builds TUI-owned dependency-injection and migration scaffolding, but deliberately migrates **zero** production command groups — a safe, incremental approach. This is the foundation for all future slash-command extraction.

### 3. [#5509 — fix(tui): restore `/title` as independent terminal window title](https://github.com/Hmbown/CodeWhale/pull/5509)
**Author:** SparkofSpike | **Open**

Fixes #5430: `/title` and `/rename` were merged into one command, making `/title` delegate to rename. This PR separates them so `/title` controls the terminal window title independently from the session name. Addresses a UX regression from the 0.9.x line.

### 4. [#5507 — docs(i18n): complete Tier 1 of Chinese docs localization](https://github.com/Hmbown/CodeWhale/pull/5507)
**Author:** SparkofSpike | **Open**

Delivers the first tier of #5482: restructures docs into per-language folders and migrates existing Chinese translations to `docs/zh_hans/`. A big step for the Chinese-speaking community.

### 5. [#5504 — feat(web): move docs/hooks and docs/troubleshooting onto dictionary spine](https://github.com/Hmbown/CodeWhale/pull/5504)
**Author:** Lstarsky0 | **Open**

Continues the #5337 series after #5488. Migrates the two smallest remaining page bodies (12 `isZh` branches each) to the centralized dictionary. The i18n cleanup is nearly complete.

### 6. [#5491 — fix(tui): persist approval outcomes before execution](https://github.com/Hmbown/CodeWhale/pull/5491)
**Author:** cyq1017 | **Open**

Closes #5360: approval requests and terminal outcomes are now persisted in session-owned logs before execution proceeds. Denies execution when a terminal approval receipt can't be persisted, and reconstructs closed/interrupted approval state on session resume. Important for auditability.

### 7. [#5404 — fix(client): fail closed on SSE UTF-8 split across HTTP/2 DATA](https://github.com/Hmbown/CodeWhale/pull/5404)
**Author:** Hmbown | **Closed**

Fixes #5374: DeepSeek Flash on macOS garbled streaming text (U+FFFD / CJK corruption) because SSE decoded each assembled line with `String::from_utf8_lossy`. HTTP/2 DATA frames can split multi-byte characters — this PR fails closed on incomplete UTF-8 sequences.

### 8. [#5405 — feat(tui): configurable model-visible read/tool-result budgets](https://github.com/Hmbown/CodeWhale/pull/5405)
**Author:** Hmbown | **Closed**

Self-hosted long-context DeepSeek V4 users hit conservative per-result ceilings (read 50 KiB, tool-result 12K chars). This makes those budgets configurable, saving ~20 extra reads on a ~64 KiB file. Directly addresses power-user needs.

### 9. [#5494 — feat(config): configurable auto-router classifier timeout](https://github.com/Hmbown/CodeWhale/pull/5494)
**Author:** Gabriel-Degret | **Closed**

Makes the auto-router classifier timeout configurable via `[auto.router] timeout_secs` (previously hardcoded at 4s). Minor but useful for high-latency networks.

### 10. [#5493 — fix(pricing): classify OrcaRouter as an aggregator billing surface](https://github.com/Hmbown/CodeWhale/pull/5493)
**Author:** Hmbown | **Closed**

Bug fix: `billing_surface_for_route` had OpenRouter/NvidiaNim/OpenCodeZen in the aggregator arm but OrcaRouter fell through to first-party PAYG — a mislabel. OrcaRouter is now correctly classified as a zero-markup aggregator.

---

## Feature Request Trends

1. **AI-as-coordinator patterns (#5508):** Users running AIs that orchestrate other AIs want native infinite-loop modes rather than hacky sleep cycles. Expect more agent-orchestration features.

2. **Repository-aware UI (#5437, #5511):** The community wants the TUI to surface git context — branch, worktree, ahead/behind — directly in the header. Design review approved the color grammar; implementation is underway.

3. **Configurable limits (#5405, #5494):** Self-hosted and long-context users repeatedly push for configurable budgets (read sizes, tool-result ceilings, timeouts). The hardcoded defaults are too conservative for power users.

4. **i18n and localization (#5482, #5337):** Both documentation and web UI are being systematically moved to proper i18n architectures. Chinese localization is a high priority.

5. **Release automation (#5299, #5496):** The community wants fully noninteractive releases — trusted npm publishing and bounded CI jobs to prevent hung runners from stalling releases.

---

## Developer Pain Points

1. **System prompt loss (#5505):** New sessions after `/new` dropping the system prompt entirely is a critical bug that erodes trust in session persistence — fortunately already closed.

2. **Windows regressions (#5512):** The header status indicator silently breaking on Windows since 0.9.7 suggests insufficient cross-platform rendering verification. Users on 0.8.x report features working that break on 0.9.x.

3. **Stuck/hung processes (#5497, #5496, #5495):** Multiple issues revolve around indefinite waits — task workers polling forever, CI jobs hanging for up to 6 hours (GitHub's 360-minute default), and missing timeout caps across release workflows. The project is responding with explicit timeouts across the board.

4. **Manual release friction (#5299):** npm publication still requires maintainer browser login + 2FA while everything else publishes noninteractively. This is a recurring release-bottleneck frustration.

5. **SSE streaming corruption (#5404):** Multi-byte UTF-8 characters split across HTTP/2 DATA frames caused garbled CJK text on macOS. Latent — but a lesson in protocol edge cases that streaming clients must handle fail-closed, not lossy.

---

*Digest generated from GitHub activity on 2026-08-19. All links point to the Hmbown/CodeWhale repository.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*