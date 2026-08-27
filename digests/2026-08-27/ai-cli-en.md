# AI CLI Tools Community Digest 2026-08-27

> Generated: 2026-08-27 05:22 UTC | Tools covered: 9

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
**Date:** 2026-08-27

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem is experiencing intense competitive pressure across seven major tools (Claude Code, Codex, Gemini CLI, Copilot CLI, Kimi Code, OpenCode, Pi, Qwen Code, DeepSeek TUI), with **security hardening** and **agent reliability** emerging as the dominant cross-cutting concerns. Release cadence varies from daily (Claude Code, Copilot CLI) to occasional (Kimi Code, Pi), with **stable release candidates** showing systematic regression issues. The community is particularly vocal about **performance degradation** (O(n²) bugs, prompt token bloat) and **silent behavior changes** that undermine trust. Windows and WSL2 support remain the most fragile platform surface across all tools, while **daemon/background session reliability** and **context lifecycle management** (compaction, memory leaks, state persistence) are universal pain points. Notably, the ecosystem is shifting from basic chat interactions to **orchestrated multi-agent workflows**, exposing lifecycle and loop-detection gaps that none of the tools have fully solved.

---

## 2. Activity Comparison

| Tool | Issues (24h) | PRs (24h) | Releases (24h) | Notable Signal |
|---|---|---|---|---|
| **Claude Code** | 10 hot | 2 updated | v2.1.247 | Daemon reliability cluster (data loss, segfaults) |
| **OpenAI Codex** | 10 hot | 10 active | rust-v0.150.1, alpha.2–4 | Windows app failures dominate (5+ issues) |
| **Gemini CLI** | 10 hot | 10 active | nightly (1 security fix) | SSRF fix merged; agent hangs persist |
| **GitHub Copilot CLI** | 10 hot | 0 | 3 prereleases (81-12→14) | MCP schema token bloat (+354K tokens) |
| **Kimi Code** | 2 | 1 | None | Cron mid-reply data loss; soul task fix |
| **OpenCode** | 10 hot | 10 active | None | Loop prevention is #1 gap (4 open issues) |
| **Pi** | 10 hot | 10 active | None (v0.84.3 regressions) | Compaction delays, O(n²) reasoning freeze |
| **Qwen Code** | 10 hot | 10 active | v0.22.2, desktop v0.2.2, cua-rust v0.20.1 | Agent Team audit spawned 7 follow-ups |
| **DeepSeek TUI** | 10 hot | 10 active | None | Machine-global lock regression (#5630) |

---

## 3. Shared Feature Directions

### A. Agent Loop Detection & Escape Hatches
**Tools:** OpenCode (#45442, #43603), Gemini CLI (#21409), Claude Code (implicit via daemon hangs)
**Need:** Max identical-tool-call limits, no-progress timeouts, automatic clarification on stuck states. OpenCode's PR #45482 (async subagent honest completion) is the earliest fix attempt.

### B. Context/Compaction Lifecycle Control
**Tools:** Pi (#6879), Claude Code (#84253 prompt-cache TTL), Copilot CLI (#4613 MCP token bloat), OpenCode (memory megathread #20695)
**Need:** User-configurable compaction triggers, streaming-aware serialization (Pi's O(n²) fix), proactive pressure display (DeepSeek TUI PR #5629).

### C. Permission Model & Security Hardening
**Tools:** Gemini CLI (SSRF fix #29081, variable expansion #28902), Qwen Code (#10197, #10199 P1 bypasses), Claude Code (#89854 false-positive blocks), Copilot CLI (Entra ID WAM support)
**Need:** Context-aware allow rules, fail-*closed* defaults, granular per-capability flags—not all-or-nothing toggles.

### D. Session State Introspection
**Tools:** Claude Code (#85192), OpenCode (#45481 durable sessions), DeepSeek TUI (#5625 non-blocking input peek), Pi (#8710 fast `/resume`)
**Need:** Reliable "waiting for input" state, project-scoped session lists, lazy loading of session metadata, programmatic control surfaces.

### E. Skill/Agent/Tool Discoverability
**Tools:** Copilot CLI (#407 `/tools` command, 31👍), Claude Code (#18192 recursive skills), Gemini CLI (#21968 skills underutilized), Kimi Code (soul task fix)
**Need:** Recursive directory scanning, slash-command-based tool inventories, less explicit-prompt dependence for skill activation.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|---|---|---|---|---|---|---|---|---|
| **Primary User** | Power devs, nix users | Enterprise (Windows/SSH) | Research/devs (modern infra) | GitHub-centric, enterprise | OSS tinkerers, async fans | Performance-focused, GLM fam | Agent-team ops, web-heavy | Tinkerers, MCP-first |
| **Architecture** | Daemon + background agents | Rust desktop app + remote | Nightly-driven, MCP-first | 3-tier (CLI, app, server) | Effect-based, plugin-first | Node + TUI, provider-agnostic | Ink→OpenTUI migration | Rust, per-session runtime |
| **Pain Point Emphasis** | Daemon/background reliability | Windows desktop fragility | Subagent hangs & false success | MCP config churn, token bloat | Loop prevention, plugin friction | Regression prevention, performance | Agent Team races, permission bypasses | Session concurrency, structural debt |
| **Distinctive Strength** | Feature velocity (daily releases) | Cross-platform (incl. WSL) | Security-first PR culture | MCP ecosystem breadth | Plugin extensibility | Provider-agnostic catalog | Agent Team orchestration | Codewhale SaaS + TUI integration |
| **Weakness Signal** | Data-loss bugs (#88307, #87981) | 7+ Windows startup issues | Roadmap gaps (agent reliability) | 0 PR activity in 24h | 4 loop issues without general fix | 0.84.3 regression cluster | 7 race conditions in 2 days | Unresolved stale Windows/WSL bugs |

---

## 5. Community Momentum & Maturity

**Rapid iteration (daily releases):** Claude Code, Codex, Copilot CLI — Claude leads in velocity but has data-loss severity issues; Codex is stable-but-constrained by Windows regressions; Copilot CLI is methodical with observable token-bloat concerns.

**Security-hardening wave:** Gemini CLI and Qwen Code show the most mature security posture (SSRF fixes, variable-expansion patches, permission audits)—community-driven PRs are landing weekly. This signals enterprise-readiness focus.

**Reliability struggles with active communities:** OpenCode and Pi have highly engaged user bases (memory megathread 138 comments, 4 loop-detection issues in 1 week) but lack general fixes; loop detection remains unsolved enterprise-wide.

**Emerging but promising:** Qwen Code's Agent Team orchestration (despite 7 races in 2 days) shows a bold architectural pace; DeepSeek TUI's structural debt decomposition (#5586) indicates maturing code hygiene.

**Laggards:** Kimi Code (minimal activity, early-stage), Copilot CLI (0 PRs today—focus on prerelease verification), Pi (no release in 24h but heavy fix activity).

---

## 6. Trend Signals

1. **Agent Orchestration Gaps Are Universal.** Every tool has unaddressed multi-agent lifecycle issues (loops, orphans, ghost members, stale reclaims). The first to ship reliable escape hatches (OpenCode PR #45482 approach) will own the "trustworthy automation" niche.

2. **Security Is the New Competitive Frontier.** Gemini CLI and Qwen Code are leading with OT-style security practices (audits, P1 response, fail-closed defaults). Expect compliance/audit features (e.g., Copilot CLI's rubber duck verifiable records #4621) to become table stakes.

3. **Performance Engineering Is Catching Up.** O(n²) bugs (Pi #8648), prompt-cache TTL regressions (Claude Code #84253), and MCP schema bloat (Copilot CLI #4613) signal that token economics are now a primary user experience metric—not just an ops concern.

4. **Windows/WSL2 Is the Battleground for Enterprise Adoption.** Codex (7 issues), Copilot CLI (WAM support), and OpenCode (WSL black screen) show the same pattern: Linux is solid, macOS is acceptable, Windows is the failure point. Tool builders who solve this win the corporate default.

5. **Context Compactness and Session Resume Are the New UX Metrics.** Users are measuring startup latency (Pi's 1.65s per arrow key at 7,000 lines), resume speed (Pi #8710), and cold-restore accuracy (Pi #7724). The sector is maturing from "chat tools" to "persistent developer environments."

6. **Community-Contributed Security Fixes Are Accelerating.** The volume of external audit-driven PRs (Gemini's SSRF, Qwen's permission bypasses, OpenCode's loop prevention) suggests a healthy OSS ecosystem where professional security researchers are actively targeting AI CLI tools—early adoption of OWASP-style practices is differentiator.

7. **The "Agent-Aware" Toolchain Is Emerging.** DeepSeek TUI's control sockets (#5533), OpenCode's live-capability sessions (#45481), and Qwen's `tools.eager` registration (#10098) point toward a future where agents are embeddable, programmable components—not just interactive CLIs.

---

**Bottom Line:** The ecosystem is in a "great consolidation" phase—fast innovation is tempered by reliability and security concerns. **Claude Code** leads in velocity, **Gemini CLI** in security posture, **OpenCode** in community-driven reliability fixes, and **Qwen Code** in architectural ambition. **Copilot CLI**'s token bloat and **Codex**'s Windows issues are systemic risks for enterprise adoption. The next 6 months will separate tools that treat reliability as a feature from those that treat it as an afterthought.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on the provided data.

---

### 1. Top Skills Ranking

The most-discussed Pull Requests highlight a community focused on fixing critical bugs in official tooling and expanding the ecosystem into specialized domains.

- **Skill-Creator Fixes (Multiple PRs: #1298, #1099, #1050, #539)** — **Status: Open**
  - **Functionality:** This is a cluster of PRs addressing the `skill-creator` tool, which is used to develop and evaluate new skills. The core issue (#556) is that its evaluation script reports a 0% recall rate, rendering its optimization loop useless.
  - **Discussion Highlights:** The conversation is a debugging deep-dive. PRs #1298 and #1099 identify a Windows-specific subprocess bug causing the 0% rate, while #1050 fixes Windows command execution (`claude.cmd`) and encoding issues. PR #539 adds a pre-parse validation to catch YAML formatting errors that break skill descriptions.
  - **Links:** [#1298](https://github.com/anthropics/skills/pull/1298), [#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050), [#539](https://github.com/anthropics/skills/pull/539)

- **Document Typography (#514)** — **Status: Open**
  - **Functionality:** Proposes a skill for typographic quality control in AI-generated documents, specifically targeting orphan words, widow paragraphs, and numbering misalignment.
  - **Discussion Highlights:** The proposal focuses on a high-frequency pain point for users: the subtle but noticeable formatting flaws that make AI-generated documents look unprofessional. It suggests a niche quality-control layer for document generation.
  - **Link:** [#514](https://github.com/anthropics/skills/pull/514)

- **SCNet HPC (#1615)** — **Status: Open**
  - **Functionality:** Adds a skill for operating SCNet HPC clusters, including SSH setup, Slurm job generation, cluster discovery, and profile management.
  - **Discussion Highlights:** This is a highly specialized, domain-specific skill for researchers. Its presence indicates a demand for moving beyond generic coding and documentation skills into specific scientific computing infrastructures.
  - **Link:** [#1615](https://github.com/anthropics/skills/pull/1615)

- **Hivemind: Multi-Agent Orchestration (#1628)** — **Status: Open**
  - **Functionality:** Proposes a skill that delegates mechanical coding work to headless workers running on free models, positioning Claude Code as the central planner and reviewer.
  - **Discussion Highlights:** The underlying rationale—that an expensive model's context window is the scarce resource—is a sophisticated cost-optimization strategy. This skill touches on emerging concerns about agent orchestration and cost management.
  - **Link:** [#1628](https://github.com/anthropics/skills/pull/1628)

- **Self-Audit (#1367)** — **Status: Open**
  - **Functionality:** Introduces a "meta-skill" to audit AI output before delivery, starting with mechanical file verification and following with a four-dimension reasoning quality audit.
  - **Discussion Highlights:** Broadly applicable across projects, this skill represents a push toward more robust and reliable agent behavior. It aligns with the community's growing focus on verification and reasoning quality gates (see Issue #1385).
  - **Link:** [#1367](https://github.com/anthropics/skills/pull/1367)

- **Frontend Design Clarity (#210)** — **Status: Open**
  - **Functionality:** Revises the existing `frontend-design` skill to be more actionable, coherent, and specific so that Claude can follow its instructions within a single conversation.
  - **Discussion Highlights:** This PR focuses not on new functionality but on improving the *quality* of existing skills. The discussion is a strong indicator of the community's focus on skill design best practices—making instructions less verbose, more direct, and easier for the model to execute.
  - **Link:** [#210](https://github.com/anthropics/skills/pull/210)

### 2. Community Demand Trends

The Issues reveal key gaps and desired directions for the Skills ecosystem:

- **Security & Trust Architecture:** The most-discussed issue (#492) is a security vulnerability report on trust boundary abuse within the `anthropic/` namespace. Users are demanding stronger security guarantees and clearer provenance to avoid malicious or low-quality skills impersonating official ones.
- **Reliability of Official Tooling:** There is significant frustration with the `skill-creator` tool's evaluation harness, which is broken on multiple platforms (#556, #1390). This is throttling the development of new skills and is a major priority for the community.
- **Context Window Efficiency:** The community is actively concerned about skills that are too "heavy." A top complaint is the `claude-api` skill injecting ~156k tokens in a single call (#1487), which highlights a need for lightweight, on-demand skill loading rather than eager, massive injections.
- **Workflow & Collaboration:** There is a push to enable org-wide skill sharing within Claude.ai (#228), moving beyond manual file uploads. This signals a need for better skill lifecycle management and distribution within teams.
- **Meta-Skills & Governance:** Proposals for skills that manage other agents or ensure output quality, such as `agent-governance` (#412) and a "Reasoning Quality Gate Pipeline" (#1385), are gaining traction. This points to a community interest in creating more robust, reliable, and self-managing AI workflows.

### 3. High-Potential Pending Skills

These PRs are actively discussed and appear close to landing, addressing immediate pain points or clear gaps:

- **`scnet-hpc` (#1615)** — For scientific users, this is a practical and necessary skill for a specific HPC environment. Its narrow scope makes it easy to validate and merge.
- **`hivemind` (#1628)** — Tapping into cost-optimization trends, this skill addresses a major practical concern for heavy Claude Code users. Its novel approach to multi-agent delegation makes it a compelling addition.
- **`self-audit` (#1367)** — This is a widely applicable meta-skill that promises to improve the reliability of every other task. It directly answers the community's demand for better verification and quality control.
- **`document-typography` (#514)** — This solves a "last-mile" quality problem for a core use case (document generation). It directly enhances the perceived professionalism of Claude's output.
- **`frontend-design` (#210)** — This significant revamp of an existing skill is a test case for the community's best practices in skill creation, likely generating a lot of discussion on how to write better skills.

### 4. Skills Ecosystem Insight

The community's most concentrated demand is for **meta-capabilities—security validation, evaluation reliability, and output auditing—rather than new functional features**, indicating a shift from building skills to building tools that make the skill ecosystem itself more trustworthy, efficient, and safe.

---

# Claude Code Community Digest — 2026-08-27

## Today's Highlights
Version 2.1.247 ships with a new `SendFeedback` tool that lets Claude draft error reports for human review, plus enhanced skill configuration options. The community is grappling with a cluster of daemon/background-session reliability issues — including severe data-loss bugs and an upgrade race that causes segfaults — while the long-running request for recursive skill discovery finally closed after 43 comments and 63 upvotes.

## Releases
**v2.1.247** — [Release notes](https://github.com/anthropics/claude-code/releases)
- New `SendFeedback` tool: on session errors, Claude drafts a feedback report for review and submission via `/feedback` (toggle with the `feedbackDrafts` setting)
- Addition of `{id, text, cooldownSessions, priority}` entries, `tipsFile`, and `label` fields (likely extending skill/context configuration)

## Hot Issues
1. **[#18192 — Recursive skill discovery (CLOSED)](https://github.com/anthropics/claude-code/issues/18192)** — The 43-comment, 63-upvote feature request for scanning subdirectories in `~/.claude/skills/` has been closed. Skills organized in nested folders (e.g., `skills/spec-system/spec-creator/`) are currently invisible to the scanner. Community response: strong demand, but closure suggests either a fix landed or an alternative was communicated.

2. **[#79824 — Artifact sharing permanently broken](https://github.com/anthropics/claude-code/issues/79824)** — "This version can't be shared publicly" persists across republish attempts and new artifacts, blocking the "anyone with the link" toggle entirely. 20 upvotes signal broad impact; users are stuck without a workaround.

3. **[#89854 — False-positive cybersecurity blocks (P0 CRITICAL)](https://github.com/anthropics/claude-code/issues/89854)** — Opus 4.7 on Linux repeatedly blocks legitimate commercial ops work involving Grokbot/xAI, misclassifying ordinary tasks as cyber incidents. The report itself is inflammatory but highlights growing friction between safety classifiers and real-world workflows.

4. **[#85408 — Background notifications impersonate user](https://github.com/anthropics/claude-code/issues/85408)** — Background task notifications cancel pending permission requests with a message that *impersonates the user*. This is a security and UX concern: users may unknowingly approve or lose actions based on forged-looking prompts.

5. **[#84253 — Prompt-cache TTL regression](https://github.com/anthropics/claude-code/issues/84253)** — Since 2.1.218+, Claude Code no longer requests the 1-hour prompt-cache TTL; any 5+ minute gap forces a full cache rewrite, increasing cost and latency. A quiet but performance-critical regression for heavy users.

6. **[#89205 — Orphaned session processes leak CPU](https://github.com/anthropics/claude-code/issues/89205)** — Follow-up to #54626 (closed June 16, "fixed in next release"): two months and ~90 patch versions later, scheduled-task sessions still leak, and each orphan spins ~10% of a core indefinitely. Chronic infrastructure issue.

7. **[#88307 — Settings file deleted by daemon worker](https://github.com/anthropics/claude-code/issues/88307)** — A daemon-hosted background worker deletes `~/.claude/settings.json` when it's a symlink into a read-only directory (common with nix/home-manager), silently wiping all user settings. 3 upvotes, but data-loss severity makes this critical.

8. **[#87981 — Pre-commit hook leads to rm -rf of unrelated session files](https://github.com/anthropics/claude-code/issues/87981)** — A workaround for a failing pre-commit hook in one session destroyed uncommitted files belonging to a *different, concurrent session*. Cross-session contamination with data loss.

9. **[#89759 — Segfault on startup persists in 2.1.246](https://github.com/anthropics/claude-code/issues/89759)** — Bun runtime SIGSEGV (si_addr=NULL) on Linux, flagged as a regression of #62747. Still present in the latest release; startup reliability is broken for a subset of users.

10. **[#90002 — Transcript metadata causes unrecoverable API 400](https://github.com/anthropics/claude-code/issues/90002)** — Windows: the Code tab writes UI render metadata (`start_timestamp`/`stop_timestamp`/`flags`) into the transcript JSONL, causing an unrecoverable API 400 that *recurs even after full sanitization*. A serious data-corruption bug.

## Key PR Progress
**Note:** Only 2 PRs were updated in the last 24h; the broader PR landscape is limited today.

1. **[#13437 — fix(hookify): use relative imports for Python module resolution](https://github.com/anthropics/claude-code/pull/13437)** — Fixes `No module named hookify` failure on all platforms by switching from absolute (`from hookify.core.config_loader`) to relative imports (`from core.config_loader`), matching the actual `PLUGIN_ROOT` structure. Open since Dec 2025; addressing a long-standing plugin loading defect.

2. **[#58673 — "s" (placeholder PR)](https://github.com/anthropics/claude-code/pull/58673)** — Tentatively a stub/placeholder PR with no meaningful description. Not worth tracking; included for completeness.

## Feature Request Trends
- **Recursive skill discovery** (#18192, 63👍) — Organizing skills into subdirectories is a clear community desire; closure of the issue may indicate an incoming or shipped capability.
- **Traditional Chinese (zh-TW) localization** (#35600, 16👍) — Requests for localization continue beyond Simplified Chinese; zh-TW support is the current gap.
- **Session state introspection** (#85192) — Users want reliable "waiting for user input" state exposed via `claude agents --json` or the statusline payload for tooling integration.
- **Scoped agent-view session lists** (#85011) — Auto-triggered Agent View currently shows a global, cross-project session list; users want project-scoped filtering.
- **Per-capability feature flags** (#85298) — `DISABLE_GROWTHBOOK` forces an all-or-nothing trade-off between Task tools and cross-session messaging; users want granular overrides.

## Developer Pain Points
- **Daemon reliability is the #1 theme** — Recurring issues around daemon self-respawn, upgrade storms (#83715), stale env inheritance (#85116), and orphaned processes (#89205) suggest the background agent architecture is fragile under real-world conditions.
- **Data loss without warning** — Settings file deletion (#88307) and `rm -rf` across concurrent sessions (#87981) are the most severe class of bug; both are silent and destructive.
- **Session state inconsistency** — Multiple reports of hanging sessions in AskUserQuestion (#83705), phantom transcript stubs (#85404), and lost history on backgrounding (#82489) indicate the session model is not yet coherent across foreground/background boundaries.
- **Safety classifier false positives** — Two separate reports (#89854, #90000) of Opus flagging legitimate security/ops work signal growing friction between model safeguards and professional use cases.
- **Upgrade/install fragility** — Segfaults on startup (#89759), Homebrew cask purged-path respawns (#84827), and Linux npm postinstall chmod races (#77384) point to an update mechanism that is not yet robust across packaging ecosystems.

---
*Data window: 2026-08-26 to 2026-08-27. Source: github.com/anthropics/claude-code*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-27

## Today's Highlights

The Codex team shipped **rust-v0.150.1** with a critical fix for remote compaction image budgeting, while the **Windows desktop app** continues to dominate community attention with multiple critical startup failures and MCP transport regressions. A notable wave of **PRs around security hardening** (trusted access contexts, token encryption, and Guardian reviewer analytics) suggests the team is prioritizing enterprise-grade trust and auditability. Meanwhile, the **5-hour usage limit** remains the community's loudest product request, with 145+ upvotes on making its temporary removal permanent.

## Releases

**rust-v0.150.1** — Bug fix release:
- Remote compaction now counts retained images toward its token budget by default, trimming older images as needed ([#41003](https://github.com/openai/codex/pull/41003))

**rust-v0.150.0** (notable features):
- Reference other Codex tasks with `@` mentions; agents can read, create, or message tasks from the terminal ([#40308](https://github.com/openai/codex/pull/40308), [#40315](https://github.com/openai/codex/pull/40315))
- `/copy` now offers a picker for full responses, individual code blocks, and blockquotes ([#39997](https://github.com/openai/codex/pull/39997))
- Unnamed terminal tasks receive descriptive titles

**Alpha versions** — rust-v0.151.0-alpha.2 through alpha.4 released (no public notes).

---

## Hot Issues

### 1. Windows Desktop App Fails to Start — "Unable to Locate Codex CLI" ([#40752](https://github.com/openai/codex/issues/40752))
78 comments | 👍 48 — The top issue this week. After updating to v26.820.60940, the app fails with `spawn EINVAL` on the `.cmd` wrapper. Multiple users confirm replication across Windows 11 builds.

### 2. Windows MCP Transport Regression — "invalid transport in mcp_servers.codex_app" ([#40715](https://github.com/openai/codex/issues/40715))
67 comments | 👍 78 — Stable app fails while Beta works. High community sentiment (78 upvotes), suggesting a breaking regression introduced in a recent stable release.

### 3. WSL-Hosted Thread Resumption Fails ([#40819](https://github.com/openai/codex/issues/40819))
59 comments | 👍 53 — Resuming WSL-hosted threads fails with the same `invalid transport` error. WSL2 + Windows 11 users are heavily affected; this is a critical workflow blocker.

### 4. Recurring Scheduled Tasks Auto-Disable ([#38350](https://github.com/openai/codex/issues/38350))
47 comments — Scheduled tasks pause themselves post-successful-run without user authorization. Reliability concern for automation-heavy teams.

### 5. Codex Desktop Cannot Start: Bundled codex.exe Relocation Fails ([#40700](https://github.com/openai/codex/issues/40700))
29 comments — WindowsApps directory relocation fails, preventing the app from launching at all. Users are stuck on older versions.

### 6. GPT-5.6 Sol Fails to Execute Shell Commands ([#32759](https://github.com/openai/codex/issues/32759))
13 comments — "code-mode host exited during handshake." Old issue but still open; related to model regressions and still being reported for newer versions (see [#40943](https://github.com/openai/codex/issues/40943) and [#41049](https://github.com/openai/codex/issues/41049)).

### 7. "Unable to Locate the Codex CLI Binary" ([#41019](https://github.com/openai/codex/issues/41019))
13 comments — Fresh duplicate of #40752, indicating the issue is widespread and unmitigated.

### 8. Desktop App Stuck in Login-Logout Loop ([#40611](https://github.com/openai/codex/issues/40611))
9 comments — After enabling Advanced Account Security, the app becomes unusable. Auth-loop bugs are recurring; see also [#39218](https://github.com/openai/codex/issues/39218).

### 9. macOS UI Text Thinner and Blurry ([#40782](https://github.com/openai/codex/issues/40782))
6 comments — Cosmetic but highly visible: global UI font weight rendered too thin after v26.820.60940. Duplicate filed at [#41047](https://github.com/openai/codex/issues/41047).

### 10. Remote SSH: Inter-Task Tools Stopped ([#40865](https://github.com/openai/codex/issues/40865))
7 comments | 👍 6 — Remote runtime update to 0.148.0 did not restore first-party inter-task coordination. MCP replacement missing, breaking remote workflows.

---

## Key PR Progress

### 1. Add Developer Instructions for Persistent Mode ([#41050](https://github.com/openai/codex/pull/41050))
Bundles proactivity/follow-up guidance for `ReasoningEffort::Persistent`, tracked as world state.

### 2. Preserve Tool Authority for TUI Delegation ([#41046](https://github.com/openai/codex/pull/41046))
Delegated thread prompts now retain issuing-tool authority instead of being mis-recorded as user input.

### 3. Encrypt Sensitive History and Notes Tool Arguments ([#41041](https://github.com/openai/codex/pull/41041))
History search queries and note payloads now encrypted via `x-openai-encrypted-tool-arguments`.

### 4. Scope Extension Capabilities to Invocation Lifetimes ([#41020](https://github.com/openai/codex/pull/41020))
Extension tool calls now scoped to lifecycles with proper futures tied to invocation lifetime.

### 5. Propagate Trace Context Through gRPC Code Mode ([#41017](https://github.com/openai/codex/pull/41017))
W3C `traceparent` injected across code-mode gRPC for end-to-end span tracking.

### 6. Reduce Skill Catalog Prompts with Path Aliases ([#41011](https://github.com/openai/codex/pull/41011))
Intelligently evaluate aliased catalogs to keep prompt size within budget.

### 7. Backport Retained-Image Compaction Budgeting ([#41003](https://github.com/openai/codex/pull/41003))
Ships in 0.150.1 — retained images now count toward compaction budget by default.

### 8. Attach Verified Access Context to Plugin MCP Calls ([#41005](https://github.com/openai/codex/pull/41005))
Adds `cyber_trusted_access` entitlement context for eligible plugin MCP calls.

### 9. Support Standalone Tool Outputs in `turn/start` ([#41002](https://github.com/openai/codex/pull/41002))
Enables starting/steering turns with function-call outputs instead of user-only input.

### 10. Harden Managed Proxy Listener Handoff ([#40999](https://github.com/openai/codex/pull/40999))
Linux sandbox networking now uses loopback TCP listener handoff, eliminating filesystem socket cleanup issues.

---

## Feature Request Trends

1. **Remove / Rework the 5-Hour Usage Limit** — Two issues ([#34035](https://github.com/openai/codex/issues/34035), [#41016](https://github.com/openai/codex/issues/41016)) with 145+ upvotes ask for permanent removal. A third ([#41004](https://github.com/openai/codex/issues/41004)) proposes sequential instead of concurrent quota consumption.

2. **Context Management** — Requests for clearing context between tasks while preserving session IDs ([#23218](https://github.com/openai/codex/issues/23218)) and better context control generally.

3. **MCP Tool Configuration** — Non-interactive MCP tool approvals without bypassing sandboxing ([#24135](https://github.com/openai/codex/issues/24135)).

4. **Terminal Integration** — DECSET 2031 for theme-change awareness in TUI ([#38575](https://github.com/openai/codex/issues/38575)).

---

## Developer Pain Points

- **Windows desktop reliability is the #1 complaint**: At least 7 open issues this week on startup failure, MCP invalid transport, and WSL-specific regressions. Dozens of users are unable to launch the app at all.

- **MCP config churn**: The `mcp_servers.codex_app` transport error appears in at least 4 distinct issues; configuration drift between stable and beta versions is confusing.

- **Remote agents are fragile**: Remote SSH/WSL runtimes don't restore capabilities after updates; inter-task tooling silently stops.

- **Auth loops persist**: Multiple reports of login-logout loops tied to security features; blocking use entirely.

- **Model runtime instability**: GPT-5.6 "code-mode host exited during handshake" falls back to other models on the same setup — needs root-cause diagnosis.

- **UI regression fatigue**: Font-weight changes shipped as unintended side effects are quickly noticed and flagged by the community.

- **Noise vs. signal**: Some issues get closed as duplicates ([#41051](https://github.com/openai/codex/issues/41051), [#41047](https://github.com/openai/codex/issues/41047)), but the volume from Windows users suggests deeper systematic issues.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-27

## Today's Highlights

A critical security fix landed in tonight's nightly release addressing SSRF vulnerability in MCP OAuth metadata discovery, with significant community PR activity focused on security hardening (variable expansion bypass, fail-closed workspace trust). The backlog remains dominated by agent reliability issues—subagent hangs, false success reporting, and browser agent instability have been open for months and continue to generate active discussion.

## Releases

**v0.59.0-nightly.20260827.g3c311beac** — Single focused security fix:
- `fix(core)`: Prevent SSRF in MCP OAuth metadata discovery and authentication ([PR #29081](https://github.com/google-gemini/gemini-cli/pull/29081)) — enforces RFC 9728 Section 7.7 and RFC 8414 constraints, requiring HTTPS for remote OAuth endpoints (loopback HTTP allowed only for local servers), and validates origin matching for resource indicators.

[Full changelog](https://github.com/google-gemini/gemini-cli/compare/v0.59.0-nightly.20260826.g64b5b79a6...v0.59.0-nightly.20260827.g3c311beac)

## Hot Issues

1. **[#22323: Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — P1 bug, 13 comments. `codebase_investigator` reports success despite hitting max turn limits before doing any analysis. The false success masking is deceptive for users relying on termination reasons; maintainers flagged for retesting but the issue has been open since March.

2. **[#21409: Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** — P1 bug, 8 comments, 8 👍. Simple tasks like folder creation hang indefinitely when the generalist agent is invoked. Users report waiting up to an hour. Workaround exists (instructing model to avoid subagents), but this is a core reliability concern.

3. **[#25166: Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1 bug, 4 comments, 3 👍. Simple CLI commands hang showing "Awaiting user input" even though the command has completed. High frustration potential for daily driver use.

4. **[#21983: Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — P1 bug, 4 comments. Browser agent fails under Wayland display server. Maintainers flagged for retesting; platform compatibility issues remain a theme.

5. **[#22186: get-shit-done output hook causes crash](https://github.com/google-gemini/gemini-cli/issues/22186)** — P1 bug, 3 comments. Crashes occur when the output hook prints user summary near completion. Open since March with no fix visible in recent PRs.

6. **[#21763: Bugreport doesn't provide subagent context](https://github.com/google-gemini/gemini-cli/issues/21763)** — P1 bug, 2 comments. `/bug` reports lack subagent internals, making debugging of agent chain failures nearly impossible. This hampers community bug reporting quality.

7. **[#21968: Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — P2, 6 comments. Models ignore custom skills and subagents unless explicitly instructed, even when descriptions clearly match the task. Core limitation for power users invested in custom setups.

8. **[#24246: 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** — P2, 3 comments. Gemini CLI hits API limits when many tools are enabled. Users expect smarter tool filtering scoped to the current task.

9. **[#20079: Symlink agents not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** — P2, 4 comments. `~/.gemini/agents/filename.md` symlinks are silently ignored. Simple fix with high usability value for users who manage dotfiles via symlinks.

10. **[#26522: Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — P2, 5 comments. Sessions deemed low-signal are never marked as processed, causing repeated retries. Inefficient and potentially costly.

## Key PR Progress

1. **[#29081: Prevent SSRF in MCP OAuth metadata discovery](https://github.com/google-gemini/gemini-cli/pull/29081)** — Merged, shipped in today's nightly. Critical security fix enforcing RFC 9728/8414 constraints: HTTPS-only for remote endpoints and origin validation.

2. **[#28902: Block `$VAR` / `${VAR}` expansion bypass](https://github.com/google-gemini/gemini-cli/pull/28902)** — Open, P1 security. Fixes incomplete variable expansion detection that bypassed the GHSA-wpqr-6v78-jr5g security gate; includes workflow hardening defense-in-depth.

3. **[#29099: Enforce fail-closed workspace trust](https://github.com/google-gemini/gemini-cli/pull/29099)** — Open. Filters repository-defined `mcpServers` in restricted mode for the A2A server, preventing unintended process execution during startup.

4. **[#28863: Consent for extension environment changes](https://github.com/google-gemini/gemini-cli/pull/28863)** — Open. Extension updates could bypass consent checks and inject unauthorized environment variables into MCP server processes; adds consent string inclusion and sanitization.

5. **[#28914: On-retry nudge with prefix caching preservation](https://github.com/google-gemini/gemini-cli/pull/28914)** — Open. Moves nudge message from `systemInstruction` to user turn suffix, preserving static prompt prefix caching while ensuring model sees recovery nudge immediately.

6. **[#28917 + #28916: Whisper model manager hardening](https://github.com/google-gemini/gemini-cli/pull/28917)** — Open. Atomic downloads with temp files, backpressure handling, and line-buffering for partial stdout chunks in transcription provider. Voice mode stability improvements.

7. **[#28787 + #28794: Corrupt MCP enablement config fail-open fix](https://github.com/google-gemini/gemini-cli/pull/28787)** — Closed. JSON parse failures were collapsed into `{}`, causing all servers to default to enabled. Both PRs prevent fail-open and data loss on corrupt config.

8. **[#28834: Suppress spurious ENOENT warnings](https://github.com/google-gemini/gemini-cli/pull/28834)** — Open. Eliminates false `Could not read directory` warnings from BFS workspace tree walker when transient lock directories disappear between readdir and descent.

9. **[#28911 + #28904: Sandbox DEBUG flag normalization](https://github.com/google-gemini/gemini-cli/pull/28911)** — Open. Truthy checks treated `DEBUG=false` as enabled; both PRs normalize to only honor explicit `true`/`1` values.

10. **[#28903: Ignore escaped `@` in completion detection](https://github.com/google-gemini/gemini-cli/pull/28903)** — Open. Prevents `\@` from activating AT completion mode when scanning backward, via odd-backslash count check.

## Feature Request Trends

**Agent orchestration & autonomy (dominant theme)** — Multiple issues and an epic (e.g., [#21000](https://github.com/google-gemini/gemini-cli/issues/21000)) push for persistent file-based task tracking via native file tools instead of in-context `WriteToDo` ([#18836](https://github.com/google-gemini/gemini-cli/issues/18836)). This addresses context rot, token costs, and cross-session memory loss. A related epic proposes zero-dependency OS sandboxing with post-execution intent routing to leverage models' native bash affinity ([#19873](https://github.com/google-gemini/gemini-cli/issues/19873)).

**AST-aware codebase understanding** — An active epic ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) investigates AST-aware file reads, search, and codebase mapping for more precise method-bound reads, reduced tokens, and better navigation.

**Model self-awareness & configurability** — Users want the CLI to understand its own mechanics (flags, hotkeys, self-execution) to act as its own guide ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)). Configurable numeric routing rules would allow custom complexity-score-to-model mappings in settings.json ([PR #27406](https://github.com/google-gemini/gemini-cli/pull/27406)).

**Subagent visibility & resilience** — Requests include subagent trajectory visibility via `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)), bug reports that include subagent context ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763)), and browser agent automatic session takeover with lock recovery ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)).

## Developer Pain Points

**False success reporting and hidden failures** — Subagents report GOAL success after hitting MAX_TURNS ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)), making failures indistinguishable from actual task completion. Combined with bug reports lacking subagent context ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763)), diagnosing agent failures remains deeply frustrating.

**Hangs and stuck states** — Recurring theme across issues: generalist agent hangs ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell commands stuck in "Waiting input" ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), interactive prompts hanging on Vite creation ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)). These erode trust in the tool's reliability.

**Unwanted file system pollution** — Models frequently create tmp scripts and edit files in random directories, creating cleanup overhead for clean commits ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)).

**Destructive behavior on complex operations** — Models use `git reset` or `--force` flags when safer alternatives exist, with users requesting stronger guardrails for complex git operations and database management ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).

**Skills and subagents underutilized** — Custom skills are ignored unless explicitly instructed, undermining user investment in custom workflows ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)).

**Security and config robustness** — Multiple PRs this week address security gaps (SSRF, variable expansion bypass, fail-open configs, unauthorized environment injection), signaling ongoing tension between agent capability and safety. Community members are actively contributing fixes, but the breadth of issues suggests systemic hardening needs.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-27

## Today's Highlights

Three new prerelease builds (v1.0.81-12 through v1.0.81-14) landed in the last 24 hours, headlined by faster session resume, OpenTelemetry trace propagation for hooks, and Windows Entra ID (WAM) support for remote MCP servers. The issue tracker saw fresh reports around a high-severity MCP schema injection regression that adds 354K startup tokens, plus a TUI freeze caused by a runaway FileWatch host-event loop. Meanwhile, long-standing requests like a global instructions file (#252) and a `/tools` slash command (#407) remain closed, with community members still engaged across multiple threads.

## Releases

Three prerelease builds shipped in the last 24 hours:

- **v1.0.81-12**: Adds Windows support for MCP servers protected by Microsoft Entra ID via the OS authentication broker (WAM), typically with no prompt. Other platforms retain the existing browser flow or `--device-code` fallback.
- **v1.0.81-13**: Hooks now receive OpenTelemetry trace context — inputs gain `traceparent` (plus `tracestate` when available) and command hooks receive corresponding env vars. Also fixes hook lifecycle events (`hook.start`/`hook.end`) emitted from hooks inside a subagent.
- **v1.0.81-14**: Improves session resume by showing recent history first while older messages load in the background. Fixes repeated `read_agent` calls now consistently returning the full turn history unless `since_turn` is provided.

All releases: https://github.com/github/copilot-cli/releases

## Hot Issues

1. **[#4612 — Runaway FileWatch host-event loop freezes TUI and grows debug log to 13 GB](https://github.com/github/copilot-cli/issues/4612)** (OPEN, 4 comments, 1 👍) — A long-running/resumed session enters a tight loop emitting `No connection accepted a host event {"kind":"FileWatch"}`. The TUI becomes unresponsive and the debug log balloons. This is especially concerning for users with long-lived sessions.

2. **[#4613 — High-severity regression: MCP schemas eagerly injected, adding 354K startup tokens](https://github.com/github/copilot-cli/issues/4613)** (OPEN, 2 comments) — Starting in the 1.0.80 line, the full ambient MCP catalog is injected into the very first model request, even for trivial prompts that need no tools. The token cost is substantial and directly impacts user spend and latency.

3. **[#252 — Global Instructions File Support](https://github.com/github/copilot-cli/issues/252)** (CLOSED, 11 comments, 12 👍) — One of the longest-running requests: users want a global instructions file so they don't repeatedly recreate per-repo instruction files. The 12 thumbs-up signals broad demand, though it's since been closed.

4. **[#407 — Slash command `/tools` to list all available tools](https://github.com/github/copilot-cli/issues/407)** (OPEN, 2 comments, 31 👍) — Still the highest-reacted open request in this digest. Users find discoverability of available tools very poor, and a simple slash command would solve it. The 31 👍 dwarf reactions on most other issues.

5. **[#4053 — TUI hangs at "Loading: N skills" on NFS/GPFS due to SIGCHLD race](https://github.com/github/copilot-cli/issues/4053)** (CLOSED, 4 comments) — On network filesystems, Tokio spawning a `which gh` subprocess with 30+ concurrent threads triggers a SIGCHLD race that hangs the TUI indefinitely. Now closed as resolved, but relevant to enterprise users on shared infrastructure.

6. **[#4485 — Theme turns light overnight](https://github.com/github/copilot-cli/issues/4485)** (OPEN, 3 comments, 2 👍) — The color theme drifts from dark to light after the machine sleeps, seemingly tied to the macOS system color scheme. A minor but irritating quality-of-life issue that affects daily users.

7. **[#4525 — Legacy `initialize` sent after successful `server/discover`, causing -32022](https://github.com/github/copilot-cli/issues/4525)** (OPEN, 2 comments) — Copilot CLI 1.0.81-1 fails MCP initialization against Python MCP SDK 2.0.0 dual-era servers. The CLI sends a modern `server/discover` probe but then follows with a legacy `initialize`, which the server rejects. Affects Python tooling users.

8. **[#4627 — Authentication failure: `quota_snapshots.chat.overage_entitlement` null](https://github.com/github/copilot-cli/issues/4627)** (CLOSED, 1 comment) — Multiple versions (1.0.81-9 and -12) fail token validation because the OAuth response contains `null` where a number is expected. Since it's closed, likely fixed in a newer build, but it caused total outage for affected users.

9. **[#4533 — TUI stops consuming events when a turn spawns parallel subagents](https://github.com/github/copilot-cli/issues/4533)** (OPEN, 3 comments) — On prerelease 1.0.81-4/-5, launching parallel subagents freezes the UI while the Rust runtime keeps working underneath. Input and scroll both die — a jarring experience for users experimenting with parallel agent workflows.

10. **[#4615 — `/copy` fails on GNOME/Mutter Wayland despite xclip fallback](https://github.com/github/copilot-cli/issues/4615)** (OPEN, 1 comment) — The fallback path is wrongly gated on `WAYLAND_DISPLAY` being unset, so users on compositors without the required data-control protocol get a hard failure instead of falling back to xclip.

## Key PR Progress

No pull requests were updated in the last 24 hours. The maintenance window appears focused on the three new prerelease builds described above.

## Feature Request Trends

Several patterns emerge from the current issue set:

- **Global and user-level configuration** — Requests for global instructions files (#252), configurable user-level discovery paths for agents/skills/hooks (#4622), and better extension points keep recurring. Users want their setup to be portable across repos and worktrees without repeated copying.
- **Tool and capability discoverability** — The `/tools` slash command request (#407) continues to hold the highest 👍 count, indicating a systemic problem: users can't tell what Copilot CLI can do without trial and error.
- **Broader agent interoperability** — Users want `/delegate` to support Claude and Codex agents (#1499), and ACP mode should support stdio transport servers when requested via the session/new API (#3889).
- **Auditability and records** — A notable request for rubber duck reviews to leave a verifiable record (#4621) — the critique, the model that produced it, and what the session did with each finding should be auditable after the session ends.

## Developer Pain Points

The most significant recurring frustrations this week:

- **Token bloat from MCP schemas** — Two separate reports (#4588, #4613) confirm MCP tool schemas are being injected unconditionally for many models, driving input token counts from ~21K to ~47K on trivial prompts. The community is actively tracking which models get tool deferral and which don't.
- **Session resume reliability** — Multiple issues surface when resuming sessions: plugin hooks not loading (#4629), history loading stalls, and the runaway FileWatch loop (#4612). Resume between machines or after long gaps feels fragile.
- **Wayland and clipboard pain** — `/copy` failures on GNOME/Mutter Wayland (#4615) and the `ext-data-control` protocol requirement continue to plague Linux desktop users.
- **Model-specific incompatibilities** — Gemini models keep failing on MCP tool schemas with union `items` types (#4623) and otherwise return 400s on plain prompts (#4155). The tooling team appears to be validating against Anthropic and OpenAI first, leaving Gemini users to hit edge cases.
- **Authentication and entitlement edge cases** — The `quota_snapshots` null response (#4627) took down sessions across multiple versions, and MCP auth with Entra ID is only now landing on Windows via WAM. Each new auth path adds compatibility surface area that can fail in production.
- **UI deadlocks and freezes** — Parallel subagents freezing input (#4533) and the "stuck working" state (#4625) indicate the TUI isn't robust to complex runtime states, even when the underlying engine keeps executing.

---

*Digest generated from [github/copilot-cli](https://github.com/github/copilot-cli) activity for 2026-08-27.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest – 2026-08-27**

---

### 1. Today's Highlights
The project saw a quiet day with no new releases or merged PRs, but two actionable items surfaced. A critical bug was reported where cron reminders can erase the visible assistant reply mid-turn, breaking transcript continuity and making recovery impossible. Additionally, a community PR is under review to fix nested task cancellation in the "soul" feature, addressing a long-standing reliability issue. Version confusion between the official install script (0.38) and the repository tag (1.49) also sparked a user question, highlighting a documentation gap.

---

### 2. Releases
No new releases were published in the last 24 hours.

---

### 3. Hot Issues

**#2620 – [OPEN] Cron fire mid-reply swallows the previous assistant reply; unrecoverable via Ctrl+O**  
*Author: tizerluo | [Link](https://github.com/MoonshotAI/kimi-cli/issues/2620)*  
A scheduled cron reminder firing while the assistant's previous reply is still on screen causes that reply to vanish from the visible transcript. Scrolling back shows the turn was replaced by the cron turn, and the `Ctrl+O` expand command does not recover it. This is a severe UX regression for users relying on cron within long interactive sessions, as it silently destroys context. No comments yet, but the issue is clearly reproducible and deserves immediate triage.

**#2618 – [OPEN] 官方脚本安装的最新版本是0.38，这个怎么是1.49**  
*Author: mawenwu1983 | [Link](https://github.com/MoonshotAI/kimi-cli/issues/2618)*  
A user is confused why the official install script fetches version 0.38 while the repository shows 1.49. This points to a versioning or release-pipeline inconsistency that could mislead users and damage trust. Maintainers should clarify whether 0.38 is a stale artifact or the 1.49 tag was pushed prematurely.

*Note: Only two issues were updated in the last 24 hours; no additional issues met the threshold for inclusion.*

---

### 4. Key PR Progress

**#2619 – [OPEN] fix(soul): cancel nested task on outer cancellation**  
*Author: koriyoshi2041 | [Link](https://github.com/MoonshotAI/kimi-cli/pull/2619)*  
This PR fixes a race condition where the nested "soul" task continues running after the outer coroutine is cancelled. It includes the initial `asyncio.wait()` in the `run_soul` lifecycle cleanup, ensures proper cancellation and awaiting of nested tasks, and adds a regression test (referencing issue #2615). This is a high-value reliability fix for the soul feature and should be reviewed and merged promptly.

*Note: Only one PR was updated in the last 24 hours; no additional PRs met the threshold for inclusion.*

---

### 5. Feature Request Trends
Based on the limited activity window, no explicit feature requests were filed. However, the recurring direction from recent issues—such as #2620 (cron interaction) and #2618 (versioning)—suggests users care about: 
- **Session stability**: ensuring background tasks (cron, soul) never disrupt or destroy active conversation state.
- **Release transparency**: clearer version mapping and update channels to avoid confusion between script-installed and source-built binaries.

---

### 6. Developer Pain Points
The following pain points are visible from the current and recently referenced issues:
- **Interruptibility & recovery**: `Ctrl+O` not restoring lost assistant replies indicates a gap in the undo/expand mechanism under concurrent task interference.
- **Task lifecycle bugs**: The PR fixing nested soul cancellation (#2619) and the referenced issue #2615 show developers repeatedly hit edge cases with async task cleanup—likely causing hangs or orphaned state.
- **Documentation/version mismatch**: The 0.38 vs 1.49 confusion suggests release notes and install scripts are not consistently updated, creating avoidable user friction.

---

*Digest generated for 2026-08-27. All links verified against the MoonshotAI/kimi-cli repository.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-27

## Today's Highlights

The community's most pressing concern remains **agent loop prevention**, with multiple new issues (#45442, #45434) reporting subagents repeating identical tool calls for extended periods with no effective safeguards. On the PR side, infrastructure improvements from `kitlangton` (session capabilities, test refactoring) and `Hona` (UI grouping fixes) dominate, alongside a notable plugin hook enhancement from `rekram1-node` allowing tool-call repair. Long-running memory issues continue to be tracked centrally via the Memory Megathread (#20695).

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#20695 — Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)** (138 comments, 105 👍)  
   The central tracking issue for memory leaks persists as the highest-activity item. Maintainers explicitly request heap snapshots over LLM-generated suggestions. Related reports like #33213 (26.8 GiB cgroup peak in server mode) and #34226 (2GB memory at only 16% context) show this is still a systematic problem.

2. **[#45442 — Subagent infinite loop for ~50min, no loop protection, uncontrollable token burn](https://github.com/anomalyco/opencode/issues/45442)** (3 comments)  
   Newest and most alarming loop report: 364 identical `grep` calls over 50 minutes. Pairs with three other open loop issues (#43603, #43673, #43800), making loop detection the top functional gap requested this week.

3. **[#33890 — Bun 1.3.14 segfault (SIGILL) on Linux x86_64](https://github.com/anomalyco/opencode/issues/33890)** (7 comments, closed)  
   AMD EPYC Zen4 users hit SIGILL crashes after ~short runtime. Closed — worth checking whether a fix landed in v1.17.10+ or if workarounds are documented.

4. **[#26411 — Decompression error: ZlibError](https://github.com/anomalyco/opencode/issues/26411)** (6 comments, 10 👍, closed)  
   Unexplained ZlibError appeared for a user without plugin changes. High 👍 on a closed issue suggests lingering impact.

5. **[#33887 — Regression in v1.17.10 on WSL: black TUI screen](https://github.com/anomalyco/opencode/issues/33887)** (6 comments, closed)  
   Downgrade to v1.17.9 is the only fix for WSL users. Closed but presumably still affecting un-upgraded users.

6. **[#42657 — TUI lag with multi-subagent sessions (97% CPU on render thread)](https://github.com/anomalyco/opencode/issues/42657)** (4 comments, open)  
   Reproducible across Warp, Windows Terminal, and WezTerm. Rendering becomes unusable at 2–4 concurrent subagents — a performance concern for power users.

7. **[#44958 — Refusal response hidden & conversation history disappears (OpenCode Go)](https://github.com/anomalyco/opencode/issues/44958)** (4 comments, open)  
   Streamed responses complete but the UI shows nothing, and history vanishes. Critical UX bug for OpenCode Go subscribers.

8. **[#37314 — Orphan sub-sessions not cleaned up when parent aborts](https://github.com/anomalyco/opencode/issues/37314)** (3 comments, open)  
   Aborted parent sessions leave sub-sessions stuck in `tool-calls` state indefinitely. Resource leak that also worsens the loop-detection story.

9. **[#34146 — macOS kernel NFS messages leak into TUI even when idle](https://github.com/anomalyco/opencode/issues/34146)** (4 comments, closed)  
   OrbStack NFS kernel messages corrupt the display. Closed — check fix version before upgrading.

10. **[#34054 — Shell tool crashes with SIGTRAP on linux/arm64 (web-tree-sitter)](https://github.com/anomalyco/opencode/issues/34054)** (3 comments, closed)  
    WASM init crash on ARM64. Closed — relevant for Raspberry Pi / ARM cloud users.

---

## Key PR Progress

1. **[PR #45481 — feat(core): open durable sessions with live capabilities](https://github.com/anomalyco/opencode/pull/45481)** (by `kitlangton`)  
   Lets hosts supply their own tools/models directly instead of relying on directory discovery. Key enabler for embedding scenarios and resuming sessions under correct capabilities.

2. **[PR #45482 — fix(task): make async subagent tasks answer honestly, once, in order, and stop](https://github.com/anomalyco/opencode/pull/45482)** (by `NamedIdentity`)  
   Directly targets the loop-detection gaps in #45480. Depends on #43510. The runtime now tells a parent once — via a trailing request-style message — when all async children finish, preventing dangling loops.

3. **[PR #45453 — feat(plugin): allow tool call repair before lookup](https://github.com/anomalyco/opencode/pull/45453)** (by `rekram1-node`)  
   Makes `event.tool` mutable in `execute.before` hooks, letting plugins fix typos (`reead` → `read`). Removes `inputSchema` from Effect/Promise APIs — a tightening of the plugin contract.

4. **[PR #45485 — fix(provider): update Mistral SDK for streaming tool calls](https://github.com/anomalyco/opencode/pull/45485)** (by `opencode-agent[bot]`)  
   Bumps `@ai-sdk/mistral` 3.0.51 → 3.0.59. New adapter accumulates streaming tool-call args and reuses IDs across fragments, fixing chunk-boundary errors on V1.

5. **[PR #45475 — fix(core): preserve conversation agent during compaction](https://github.com/anomalyco/opencode/pull/45475)** (by `rekram1-node`)  
   Compaction now uses the last assistant message's agent (including from earlier checkpoints), preserving system prompt, context hooks, and structured history correctly.

6. **[PR #45474 — fix(app): preserve tool disclosures when groups update](https://github.com/anomalyco/opencode/pull/45474)** (by `Hona`)  
   Prevents remounting of nested tools (and resetting user disclosure choices) when group refs change. Three-line production fix for a subtle UI state bug.

7. **[PR #45476 — fix(core): apply plugin environment to v2 bash](https://github.com/anomalyco/opencode/pull/45476)** (by `bittervan`)  
   Closes #41117: V2 Bash now invokes the `shell.env` plugin hook, so plugin-provided environment variables actually reach bash commands.

8. **[PR #45461 — feat(core): expose background shell output path](https://github.com/anomalyco/opencode/pull/45461)** (by `rekram1-node`)  
   Background shell responses now include live output file paths and shell IDs, enabling interim reads instead of waiting for completion.

9. **[PR #45472 — fix(websearch): remove provider whitelist](https://github.com/anomalyco/opencode/pull/45472)** (by `4ebuRushka`)  
   Websearch is client-side (Exa/Parallel MCP) and shouldn't depend on provider support. Closes #44307; enables websearch for all providers by default.

10. **[PR #45477 — fix(app): merge adjacent patches inside used groups](https://github.com/anomalyco/opencode/pull/45477)** (by `Hona`)  
    Restores `patchFileGroups` behavior: adjacent patch calls on different files collapse into a single "Patch 3 files" stack instead of separate headers.

---

## Feature Request Trends

1. **Agent loop detection / escape hatches** (highest demand)  
   Four open issues (#45442, #43603, #43673, #43800) demand: max identical-tool-call limits, no-progress timeouts, and automatic clarification when the agent is stuck. This is the #1 functional gap.

2. **Sub-session lifecycle management**  
   #37314 (orphan cleanup on abort) and #42286 (abort leaves pending task calls) push for proper parent-child session teardown and state visibility.

3. **CodeMode for built-in tools** (#43137)  
   Community wants the experimental CodeMode extended beyond custom tools to cover OpenCode's built-in toolset.

4. **First-class remote/mobile control** (#45437)  
   RFC for `opencode rc` command with QR pairing, like Claude Code.

5. **IDE session management UI** (#34232)  
   Desktop/IDE extension needs a `/sessions` equivalent to view and resume past sessions.

---

## Developer Pain Points

1. **Uncontrollable token burn from loops** — The loudest recurring pain. Multiple users report tens-to-hundreds of identical tool calls with no automatic stop, requiring manual interrupt. The 3-comment count on these issues underscores how urgent yet under-discussed this is.

2. **Memory/resource leaks in long sessions and server mode** — The Memory Megathread (138 comments) plus specific reports (26.8 GiB cgroup peak, 2 GB with 16% context) show this remains unresolved for production users. Maintainers are actively collecting heap snapshots but no public fix yet.

3. **TUI and cross-platform stability regressions** — Black screens on WSL (v1.17.10), macOS NFS message corruption, and ARM64 SIGTRAPs suggest platform-specific testing gaps.

4. **No effective "stop" for background/async subagents** — Even non-loop behavior (e.g., #45456 stuck web session) shows the system can get wedged with no diagnostics, forcing manual kills or timeouts.

5. **Plugin contract friction** — Multiple PRs (#45453, #45476) point to plugins being unable to intercept/modify core behavior (tool names, shell env). This is improving but indicates current limitations slow down plugin adoption.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-27

## Today's Highlights

The Pi community is navigating the aftermath of the 0.84.3 release, which introduced several regressions — notably broken proxy support for Google Vertex, a bundled CLI that fails to load global extensions, and a Windows PowerShell tool that prepends a stray character to commands. Meanwhile, the team is actively fixing a cluster of TUI and streaming performance issues, including a critical O(n²) reasoning-details accumulation bug and soft line-break rendering problems. Several high-quality UI improvements — mouse cursor positioning, prompt editing, and readable markdown paragraphs — landed in the last 24 hours.

## Releases

No new releases in the last 24 hours. The most recent version remains **v0.84.3**, which is the subject of several regression reports.

## Hot Issues

1. **[#6879 — Auto-compaction never triggers after context grows past 100%](https://earendil-works/pi/issues/6879)**
   A two-hour agentic turn grew past the compaction threshold, only triggering after an API rejection at 373k tokens. The community wants compaction checked after every agentic step. The issue has 19 👍 and is marked `inprogress`. High impact: this affects long-running sessions across all providers.

2. **[#8610 — Regression: HttpsProxyAgent is not a constructor with google-vertex](https://earendil-works/pi/issues/8610)**
   A v0.84.3 regression where code-splitting broke proxy support for Google Vertex. Any user behind a corporate proxy is blocked. Marked `[bug]` and actively discussed.

3. **[#8620 — Bundled CLI: every global extension fails to load](https://earendil-works/pi/issues/8620)**
   After upgrading to 0.84.3, extensions importing `@earendil-works/pi-coding-agent` fail with module-not-found. This breaks the entire extension ecosystem for bundled-CLI users.

4. **[#7724 — Cold restore replays an overflow assistant removed by live recovery](https://earendil-works/pi/issues/7724)**
   Reopening a session after compaction re-adds the failed/truncated assistant response to model history, corrupting the conversation. Follows up on compaction/overflow recovery issues. Marked `inprogress`.

5. **[#8029 — Very slow performance moving in prompt editor](https://earendil-works/pi/issues/8029)**
   With ~7,000 lines in the prompt buffer, a single arrow key press takes 1,650ms. The editor appears to grow linearly slow with buffer size. Marked `inprogress`. 9 comments.

6. **[#7053 — Parallel tool batches lose completed results when one sibling stalls](https://earendil-works/pi/issues/7053)**
   When one tool in a parallel batch stalls, already-completed results are never persisted, producing "No result provided" errors. The PR #3503 fixed the UI event, but the persisted `toolResult` still waits for the whole batch.

7. **[#8648 — O(n²) reasoning_details accumulation freezes the event loop](https://earendil-works/pi/issues/8648)**
   For long reasoning streams (GLM), each chunk re-parses and re-stringifies the entire accumulated `thinkingSignature`. The process freezes. A fix is already in progress (PR #8671).

8. **[#8711 — TUI pegs 100% CPU streaming OpenRouter thinking](https://earendil-works/pi/issues/8711)**
   GLM-5.3-flash with thinking max causes the TUI to freeze at 100% CPU. Related to #8648 — reasoning_details stored as one object per token. Users report progressive slowdown.

9. **[#8705 — Unhandled rejection in agentLoop leaves EventStream hanging](https://earendil-works/pi/issues/8705)**
   Missing `.catch()` on `void runAgentLoop(...)` means an unhandled rejection never ends the stream, leaving the TUI hung. Already fixed by PR #8704.

10. **[#8582 — Built-in powershell tool uses Windows PowerShell 5.1](https://earendil-works/pi/issues/8582)**
    Interactive mode falls back to PS 5.1 while `-p` mode correctly uses pwsh. Confusing inconsistency for Windows users with PowerShell 7 installed.

## Key PR Progress

1. **[#7602 — Configurable summarization models](https://earendil-works/pi/pull/7602)** — Open. Adds configurable models and thinking levels for compaction and branch summaries. Closes #7553. Long-running PR (open since Aug 4), still in review.

2. **[#8708 — Resolve fd/rg release versions without the GitHub API](https://earendil-works/pi/pull/8708)** — Open. Avoids the 60 req/hour anonymous GitHub API quota on shared egress IPs by hardcoding or resolving versions differently. Fixes a real pain for office NAT environments.

3. **[#8707 — Keep zai thinking enabled for forced-thinking models](https://earendil-works/pi/pull/8707)** — Closed. Fixes `reasoningEffort: undefined` being sent as `thinking: { type: "disabled" }` for GLM models that require thinking. Prevents reasoning leakage into output.

4. **[#8671 — Serialize thinking signature once](https://earendil-works/pi/pull/8671)** — Closed. Fixes the O(n²) `reasoning_details` accumulation by keeping an in-memory accumulator and serializing once at stream end. Addresses #8648.

5. **[#8704 — End event stream on unhandled loop rejection](https://earendil-works/pi/pull/8704)** — Closed. Quick, surgical fix for issue #8705: adds `.catch()` to the agent loop promise chain.

6. **[#8346 — Repair unterminated session tails](https://earendil-works/pi/pull/8346)** — Closed. Detects and repairs malformed JSONL tails on session load, preventing data loss. Helpful for crash-recovery scenarios.

7. **[#8699 — Remove coding-agent config reads from pi-tui](https://earendil-works/pi/pull/8699)** — Open. Cleans up the layering violation where TUI reads coding-agent configuration. Reduces duplicate config resolution.

8. **[#8674 — Render markdown soft line breaks as spaces](https://earendil-works/pi/pull/8674)** — Closed. Fixes thinking blocks rendering as ragged sequential lines. `marked` treats soft breaks as hard breaks; this makes them flow as paragraphs.

9. **[#8547 — Move editor cursor on click](https://earendil-works/pi/pull/8547)** — Closed. Adds click-to-position cursor support in the prompt editor. Addresses a long-standing TUI usability gap (also issue #8701).

10. **[#8664 — Promote NVIDIA InferenceHub to built-in provider](https://earendil-works/pi/pull/8664)** — Closed. Adds `nvidia-inference-hub` as a first-class provider in pi-ai, fronting Claude/GPT/Gemini/DeepSeek/Llama under one auth.

## Feature Request Trends

- **Editable provisional composer** (#8689): Users want to start drafting a prompt while Pi loads extensions, skills, and runtime state, rather than staring at a blank screen during startup.
- **Configurable compaction/summarization** (#7602, #6879): The community is pushing for user control over *when* and *how* context compaction occurs, including model choice and thinking level.
- **Mouse-driven editing** (#8547, #8678, #8701): A cluster of requests to make the TUI feel like a native text editor — click to position cursor, mouse-drag editing, and double-click path selection fixes.
- **Extension examples for MCP** (#8703): Users want official examples of MCP extensions with dynamic tool loading, alongside existing examples for providers and deferred tools.
- **Session management improvements** (#8269, #8710): Fork-across-cwd session moves and lazy `/resume` parsing (read headers only, not full files) for fast recent-session switching.

## Developer Pain Points

- **v0.84.3 regressions are piling up**: Proxy support (HttpsProxyAgent), extension loading (module-not-found), PowerShell stray character, and Apple Terminal meta-arrow handling — this release introduced several avoidable issues. The community is unusually active in closing these quickly, but the cadence suggests a need for a patch release soon.
- **Streaming performance with reasoning models is fragile**: GLM-style detailed reasoning is hitting O(n²) CPU issues (#8648, #8711), freezing TUI and paginating tokens per object. The serialization fix (#8671) helps, but users are watching carefully.
- **Compaction/overflow recovery is unreliable**: Multiple issues (#6879, #7724) show compaction either triggers too late or replays truncated responses on cold restore. The "auto-compaction never triggers" issue is the most-upvoted open bug.
- **Parallel tool execution has a persistence gap**: When one tool stalls, already-completed results are lost on restart (#7053). This affects agent reliability for any workflow using parallel tool calls.
- **`/resume` is painfully slow** (#8710): Fully parsing every session file just to show a list is a UX blocker for users with many sessions.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-27

## Today's Highlights

Qwen Code shipped v0.22.2 alongside a desktop release and new CUA driver binaries, with a significant architectural change: the persistent Node REPL is now delivered as a standalone MCP server (breaking change). The Agent Team lifecycle is under active hardening — a comprehensive audit (#10074) spawned seven follow-up issues covering race conditions, ghost members, and stale reclaim hazards, with fixes already landing (#10236). Security researchers also flagged two P1 permission-bypass vectors in MCP alias matching and Bash allow rules.

## Releases

**v0.22.2** — [Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.22.2)
- Breaking: Persistent Node REPL refactored into a standalone MCP server ([#9499](https://github.com/QwenLM/qwen-code/pull/9499))
- Preview v0.22.2-preview.1 included goal-prompt convergence fixes

**Qwen Code Desktop v0.2.2** — [Release](https://github.com/QwenLM/qwen-code/releases/tag/desktop-v0.2.2)
- Same goal-continuation contract fixes as v0.22.2

**cua-driver-rs v0.20.1** — [Release](https://github.com/QwenLM/qwen-code/releases/tag/cua-driver-rs-v0.20.1)
- Prebuilt binaries: macOS (codesigned + notarized universal), Linux and Windows (x86_64 + arm64)

## Hot Issues

1. [**#10074 — Agent Team lifecycle audit: five race and cleanup risks**](https://github.com/QwenLM/qwen-code/issues/10074) — A single audit spawned seven follow-up issues covering race conditions in team management. High community engagement; fixes already in progress.

2. [**#10197 — Security: static loader env assignments bypass concrete Bash allow rules**](https://github.com/QwenLM/qwen-code/issues/10197) — P1 vulnerability: leading environment assignments can change program semantics and bypass saved `Bash(...)` allow rules. Requires no command substitution, making this especially dangerous.

3. [**#10199 — Security: lossy MCP permission aliases authorize tools from a different server**](https://github.com/QwenLM/qwen-code/issues/10199) — P1 regression in MCP permission matching — distinct server/tool identities collapse to the same legacy name, allowing cross-server authorization.

4. [**#10218 — permissions.allow semantics changed: uncovered tools disabled without prompt**](https://github.com/QwenLM/qwen-code/issues/10218) — Behavior change in 0.22.1: `allow` list became a registration whitelist rather than auto-approval, silently disabling uncovered tools. Documentation not updated.

5. [**#10205 — client.telemetrySwap.test.ts failing 9/10 tests on main**](https://github.com/QwenLM/qwen-code/issues/10205) — P1 test breakage affecting all open PRs after #10016 merged. Fix PR #10243 removes a duplicate stub.

6. [**#10227 — Custom model provider cannot converse (Moonshot schema error)**](https://github.com/QwenLM/qwen-code/issues/10227) — `tools.function.parameters` rejected as invalid Moonshot JSON schema; custom provider configs break.

7. [**#10242 — E2E on main: runners can't reach Aliyun Beijing endpoint**](https://github.com/QwenLM/qwen-code/issues/10242) — Intermittent E2E failures caused by network reachability, not code regressions. PR #10229 caps lanes and adds auto-retry.

8. [**#10209 — Stale reclaim can delete a newer live team generation**](https://github.com/QwenLM/qwen-code/issues/10209) — Concurrent creators reclaiming the same stale team name risk deleting a live replacement. Fix already landed in #10236.

9. [**#10194 — qwen3.8-flash treated as text-only; media silently routed away**](https://github.com/QwenLM/qwen-code/issues/10194) — Modality auto-detect misclassifies the model, so image/PDF inputs never reach the model as pixels — routed through vision fallback instead.

10. [**#8662 — Migrate TUI rendering from ink to OpenTUI (tracking)**](https://github.com/QwenLM/qwen-code/issues/8662) — Long-standing effort to replace the heavily patched ink + React 19 renderer. PR #9885 ships OpenTUI via per-platform npm packages — one step closer.

## Key PR Progress

1. [**#10098 — Decouple permissions.allow from tool registration via tools.eager**](https://github.com/QwenLM/qwen-code/pull/10098) — Splits the dual role of `permissions.allow` back into pure auto-approval, with a new `tools.eager` setting for registration. Directly addresses the #10218 semantics regression.

2. [**#10236 — Make stale team reclaim generation-safe**](https://github.com/QwenLM/qwen-code/pull/10236) — Closes the race in #10209 where a stale-reclaim decision could delete a newer live team generation.

3. [**#10229 — Cap E2E lanes and auto-retry transient main failures**](https://github.com/QwenLM/qwen-code/pull/10229) — Mitigates the intermittent E2E network failures (#10242) by lane capping and one auto-retry.

4. [**#10243 — Remove duplicate telemetry test registry stub**](https://github.com/QwenLM/qwen-code/pull/10243) — Fixes the P1 test breakage from #10205 affecting main and all open PRs.

5. [**#9940 — Review: reply carried findings into their thread, resolve fixed ones**](https://github.com/QwenLM/qwen-code/pull/9940) — Re-posted findings now reply inside the original thread; resolved findings get a ruling fed back to the PR.

6. [**#10100 — Reclaim command hook process trees**](https://github.com/QwenLM/qwen-code/pull/10100) — POSIX process groups with bounded SIGTERM→SIGKILL on timeout; Windows uses absolute `taskkill.exe` path.

7. [**#10117 — Surface thread-resolution guard refusals in round reports**](https://github.com/QwenLM/qwen-code/pull/10117) — Fixes silent autofix thread-resolution skips by announcing guard refusals on the PR itself and waiting out head-propagation lag.

8. [**#10175 — Stamp tool results in every host for Goal evidence**](https://github.com/QwenLM/qwen-code/pull/10175) — Extends Goal turn-permit provenance to headless and ACP hosts via one shared helper.

9. [**#10136 — Swap re-review rounds to fix-audit shape under critical posture**](https://github.com/QwenLM/qwen-code/pull/10136) — When a re-review is knowably headed to critical-only posting, rounds run a narrowed fix-audit shape instead of the full round-1 shape.

10. [**#10085 — CI: run Linux E2E shards on the persistent pool**](https://github.com/QwenLM/qwen-code/pull/10085) — Routes Linux E2E to the `ecs-qwen` persistent pool with hosted fallback and kill-switch.

## Feature Request Trends

- **Agent Team hardening dominates**: The lifecycle audit (#10074) and its seven follow-ups represent the single largest cluster — race conditions, ghost members, stale reclaims, and broadcast failures are all being actively addressed.
- **OpenAI Response API support** ([#889](https://github.com/QwenLM/qwen-code/issues/889)) remains an open request for gpt-5-codex compatibility — aged nearly a year but still active.
- **Session branching with Git worktree isolation** ([#8271](https://github.com/QwenLM/qwen-code/issues/8271)) gains traction — branching any session plus optional worktree isolation.
- **Deep daemon health and background Agent recovery** ([#8586](https://github.com/QwenLM/qwen-code/issues/8586)) — explicit `activeWork` fact and recovery paths for background Agents that outlive prompts.
- **ACP execution adapter for ordinary agents** ([#10219](https://github.com/QwenLM/qwen-code/issues/10219)) — new experimental direction, fresh and under discussion.
- **OpenTUI rendering migration** ([#8662](https://github.com/QwenLM/qwen-code/issues/8662)) — long-running infrastructure effort now shipping via per-platform npm packages.

## Developer Pain Points

- **Silent behavior changes**: The `permissions.allow` semantics shift in 0.22.1 (#10218) — tools silently disabled without prompts, undocumented — drew immediate community pushback.
- **Permission bypasses are top priority**: Two P1 security issues (#10197, #10199) show the community actively auditing and finding real bypasses in the permission layer.
- **CI flakiness plagues main**: Intermittent E2E failures (#10242), broken tests (#10205), and follow-up CI issues (#10240, #10239) suggest engineering velocity is intermittently slowed by infrastructure.
- **Agent Team reliability**: Seven race-condition reports in two days signal a subsystem that shipped fast and is now receiving rigorous scrutiny. The maintainers' quick response with fixes suggests this is being taken seriously.
- **Web Shell UX gaps**: Language sync before session creation (#10234), runtime-added models not becoming current (#10184), and MCP breaking conversation after load (#10228) show the Web Shell surface still has rough edges.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-27

## Today's Highlights

The v0.9.12 integration tree is receiving rapid stabilization: a machine-global runtime lock that blocked concurrent sessions is being fixed via per-session store scoping (#5630, PR #5638), while the agent's context-pressure signal gets promoted to persistent UI status (PR #5629). Enterprise readiness advances with a Tailscale embedding option for the web UI (PR #5635), an operator/security packet (PR #5628), and a significant architectural simplification retiring the Keychain product path in favor of a unified worker model (PR #5632).

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#5630 — Runtime store owner lock blocks multiple sessions](https://github.com/Hmbown/CodeWhale/issues/5630)** — Critical regression in v0.9.12: a machine-global single-owner lock hard-fails every Codewhale process after the first. Community impact is immediate — any user running parallel sessions hits this. Fixed by PR #5638.

2. **[#5586 — Decompose mega files: lib.rs (18.7k), config.rs (12.3k), client.rs (11.1k)](https://github.com/Hmbown/CodeWhale/issues/5586)** — The 10k+-line files are causing maintainability pain. The 20k-line test files should split alongside their subjects. Community consensus: this is long overdue structural debt.

3. **[#5620 — Context pressure warning is transient; agent doesn't react](https://github.com/Hmbown/CodeWhale/issues/5620)** — The warning disappears into scrolling metadata and the agent doesn't proactively compact. Medium-severity silent degradation. PR #5629 addresses the display-only slice; the proactive reaction remains open.

4. **[#5533 — Control surface for supervised operation](https://github.com/Hmbown/CodeWhale/issues/5533)** — Per-session control socket (message/interrupt/relaunch/status) plus `RuntimeBackendKind::External` for external supervisors. The operator wants terminal multiplexer wrappers and CI harnesses to manage sessions programmatically.

5. **[#5625 — Non-blocking "pending user input" peek tool](https://github.com/Hmbown/CodeWhale/issues/5625)** — A lightweight tool so the agent can check mid-turn whether the user has typed guidance, without blocking. Targets human-in-the-loop collaboration workflows.

6. **[#4564 (stale) — `--model`/`--toolsets` flags consumed as single arg on Windows](https://github.com/Hmbown/CodeWhale/issues/4564)** — Pre-exec flags break with npm global installs on Windows. Community suggestion: env vars (`CODWHALE_MODEL`/`CODWHALE_TOOLSETS`) as the workaround. Still open.

7. **[#4956 (stale) — Provider network connection failure in WSL2](https://github.com/Hmbown/CodeWhale/issues/4956)** — "Can't connect to the API provider" after WSL2 restart. No maintainer response yet; likely needs repro details.

8. **[#5637 — Scope MCP secret providers to the owning runtime](https://github.com/Hmbown/CodeWhale/issues/5637)** — Mutating process environment for MCP credentials is unsound with multi-threaded access; secret lifetime becomes process-global. Proposes runtime-scoped secret provision.

9. **[#4568 (stale) — Slash-command latency regression](https://github.com/Hmbown/CodeWhale/issues/4568)** — `/xxx` commands noticeably slower than previous version on Windows 10. Community suspects performance optimization regression. No maintainer response yet.

10. **[#5627 (closed) — Add Xquik to reviewed MCP recommendations](https://github.com/Hmbown/CodeWhale/issues/5627)** — `/mcp add recommended xquik` returns unknown-ID; users must manually discover the endpoint. Quick acceptance — closed with addition.

## Key PR Progress

1. **[#5638 — fix(runtime): scope thread store per session](https://github.com/Hmbown/CodeWhale/pull/5638)** — Closes #5630: runtime store defaults to `$CODEWHALE_HOME/sessions/<id>/runtime`; `CODEWHALE_RUNTIME_DIR` still selects a shared root when intended. The exclusive process-owner lock stays.

2. **[#5629 — fix(tui): persist context pressure warnings](https://github.com/Hmbown/CodeWhale/pull/5629)** — Promotes warning/high/critical pressure to sticky status UI; pressure updates no longer vanish into scrolling turn metadata. First approved slice of #5620.

3. **[#5626 — feat(runtime-api): per-thread usage endpoint + session cost persistence](https://github.com/Hmbown/CodeWhale/pull/5626)** — Adds `GET /v1/threads/{id}/usage` over `RuntimeThreadManager::aggregate_usage_for_thread`; GUI session-cost surface reads provider-aware recorded pricing instead of reimplementing rate tables.

4. **[#5624 — feat(tui): live session token totals](https://github.com/Hmbown/CodeWhale/pull/5624)** — Per-model-call `TurnUsage` receipts feed a display-only pending ledger: input, output, total, cache-hit, cache-miss, cache-write tokens. First slice of #5581.

5. **[#5635 — feat(web): embed tsnet for `codewhale web --tailscale`](https://github.com/Hmbown/CodeWhale/pull/5635)** — Opt-in Tailscale embedding; default stays loopback-only. `--tailscale` without `--web` rejected. Enterprise remote-access lane.

6. **[#5636 — fix(tui): degrade incompatible Moonshot tools per request](https://github.com/Hmbown/CodeWhale/pull/5636)** — MFJS compatibility failures degrade per tool instead of failing the whole request; omits `tools`/`tool_choice` when no compatible tool remains; locally rejects named `tool_choice` for omitted tools.

7. **[#5632 — One worker system; retire Keychain product path](https://github.com/Hmbown/CodeWhale/pull/5632)** — Fleet/sub-agents unified: `spawn(prompt)` inherits parent; roles are labels not permission matrix; no preset catalog. `CODEWHALE_SECRET_BACKEND` becomes a no-op; secrets move to files in home.

8. **[#5631 — feat(models): add OpenRouter qwen3.8-flash (1M, priced)](https://github.com/Hmbown/CodeWhale/pull/5631)** — New catalog row: 1M context, 131K output, text+image+video input. Priced (not unpriced) — durable list rates from models.dev. No invented Token Plan flash id.

9. **[#5622 — feat(tui): support Kimi Code k3-256k](https://github.com/Hmbown/CodeWhale/pull/5622)** — Adds the documented `k3-256k` to the Kimi Code roster; fixed 262,144-token context and K3 output/reasoning contract; membership-plan context overrides stay exclusive to bare `k3`.

10. **[#5628 — Enterprise launch readiness: operator packet, Codewhale launch, #5585, #5617](https://github.com/Hmbown/CodeWhale/pull/5628)** — Adds `docs/ENTERPRISE.md` (en + zh-Hans) as the operator/security review packet covering local runtime, plus execution of launch-readiness handoff work.

## Feature Request Trends

- **Supervised/automated operation** (#5533, #5625) — control sockets and non-blocking input peeking for external supervisors; the agent is being positioned as a programmable, embeddable component rather than only an interactive TUI.
- **Enterprise/remote access** (#5628, #5635) — Tailscale embedding and the operator packet signal a coordinated push for managed/remote deployment.
- **Context-aware agent behavior** (#5620, #5629) — persistent pressure display is done; proactive compaction/reaction still needed.
- **Model/tool agnosticism** (#5622, #5631, #5636) — catalog breadth (Kimi k3-256k, qwen3.8-flash) plus graceful per-tool degradation; the wire compatibility layer is becoming its own design discipline (#5633).

## Developer Pain Points

- **Structural debt is biting** (#5586) — 10k+-line files are consistently cited as the root cause of slow iteration and merge conflicts; the community is pushing hard for decomposition.
- **Session concurrency regressions** (#5630) — v0.9.12's machine-global lock broke parallel workflows; immediate hotfix merged, but the underlying design tension (shared vs. per-session runtime state) is unresolved.
- **Windows and WSL2 friction** (#4564, #4956) — CLI flag parsing and network connectivity issues on Windows/WSL2 remain open with no maintainer response; stale bugs with `needs-info` label suggest community repro details are insufficient.
- **Secret management is in flux** (#5632, #5637) — The Keychain retirement and environment-mutation concerns show the secret lifecycle design is still settling; expect this area to see more churn.
- **MCP ecosystem onboarding** (#5627) — Manual endpoint discovery for recommended MCP servers is a UX gap; the Xquik fix was quick, but the pattern suggests a systematic issue.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*