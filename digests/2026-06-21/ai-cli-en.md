# AI CLI Tools Community Digest 2026-06-21

> Generated: 2026-06-21 02:16 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Ecosystem Comparison Report
**Date:** 2026-06-21

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape is undergoing a phase of intense stabilization and feature maturation. Across all six major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI—the dominant themes are **multi-agent orchestration**, **session transparency**, and **cross-platform reliability**. While Claude Code and OpenAI Codex lead in community engagement and feature complexity, tools like Gemini CLI and DeepSeek TUI are rapidly closing gaps in agent reliability and developer experience. The ecosystem is converging on shared architectural patterns—session-as-process primitives, MCP-based extensibility, and sub-agent governance—while diverging in platform specialization and target user segments. A notable pattern is the emergence of **same-ecosystem fork dynamics** (e.g., Pi and OpenCode sharing provider registries), suggesting consolidation pressures ahead.

---

## 2. Activity Comparison

| Tool | Issues Updated (24h) | PRs Active (24h) | Release Status | Community Signal |
|---|---|---|---|---|
| **Claude Code** | 10 | 4 | ✅ v2.1.185 shipped | High—dominant multi-agent discussion |
| **OpenAI Codex** | 10 | 10 | ⏸️ No release (last: 26.616.x) | Very High—sandbox regression crisis |
| **Gemini CLI** | 10 | 10 | ⏸️ No release | High—stability-focused |
| **GitHub Copilot CLI** | 14 | 2 | ⏸️ No release | Moderate—burst activity after quiet period |
| **Kimi Code CLI** | 2 | 1 | ⏸️ No release | Low—stabilization phase |
| **OpenCode** | 10 | 10 | ✅ v1.17.9 shipped | High—test infra overhaul |
| **Pi** | 10 | 10 | ✅ v0.79.9 shipped | Moderate—community PRs active |
| **Qwen Code** | 10 | 10 | ✅ v0.18.4 + nightly shipped | High—security bug sweep |
| **DeepSeek TUI** | 10 | 10 | ⏸️ v0.8.63 in integration | Moderate—maintainer-led refactoring |

**Key observations:**
- **Claude Code** and **OpenCode** are the only tools shipping stable releases today, with Claude Code's v2.1.185 focusing on UX polish and OpenCode's v1.17.9 on agent step limits.
- **OpenAI Codex** and **Gemini CLI** are in a "fix-first" mode, with Codex facing a sandbox regression crisis (#29189, 55 comments) and Gemini grappling with agent hang bugs (#21409).
- **Qwen Code** stands out for shipping both a stable release and a nightly build, indicating rapid iteration velocity.
- **DeepSeek TUI**'s v0.8.63 integration branch (PR #3347) accumulating 29 commits signals a substantial upcoming release.

---

## 3. Shared Feature Directions

### Multi-Agent Orchestration (Highest Signal)
| Requirement | Tools | Specific Issues/PRs |
|---|---|---|
| Cross-session messaging | **Claude Code**, **OpenAI Codex**, **OpenCode** | CC #24798, OpenAI #14923, OpenCode #5887 |
| Parallel/background agents | **Claude Code**, **OpenCode**, **DeepSeek TUI** | CC #28300, OC #17994, DSTUI #3289 |
| Sub-agent governance (budgets, limits) | **DeepSeek TUI**, **Gemini CLI** | DSTUI #3321, Gemini #22323 |
| Parent-child agent telemetry | **Claude Code**, **Gemini CLI** | CC #1770, Gemini #22092 |

### Session & Context Transparency
| Requirement | Tools |
|---|---|
| Context window visualization | **Claude Code**, **OpenCode**, **GitHub Copilot CLI** |
| Token/credit consumption tracking | **OpenAI Codex** (#28879), **GitHub Copilot CLI** (#1240), **OpenCode** (#6152) |
| Compaction notifications | **GitHub Copilot CLI** (#3867), **OpenAI Codex** (#29255) |

### Extensibility & Plugin Quality
| Requirement | Tools |
|---|---|
| Hooks/hookify compatibility | **Claude Code**, **GitHub Copilot CLI**, **Pi** |
| MCP notification reliability | **Claude Code** (#36431), **OpenAI Codex** (#29279) |
| Plugin discoverability (list/get commands) | **GitHub Copilot CLI**, **Gemini CLI** |

### Security & Input Validation
| Requirement | Tools |
|---|---|
| Sensitive file exclusion (`.codexignore`) | **OpenAI Codex** (#2847) |
| Case-sensitive URL scheme checks | **Qwen Code** (10+ issues today) |
| `parseInt` input validation hardening | **Qwen Code** (#5485, #5499) |
| OAuth credential normalization | **Qwen Code** (#5442) |

### Platform Reliability
| Requirement | Affected Tools |
|---|---|
| Windows sandbox persistence | **OpenAI Codex**, **Kimi Code CLI** |
| Linux musl compatibility | **OpenCode** (#27589), **DeepSeek TUI** (#3238) |
| macOS binary signing | **Claude Code** (#61114) |
| WebSocket reconnect reliability | **OpenAI Codex** (#18960, #22898) |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Kimi Code CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|---|---|---|---|---|---|---|---|---|---|
| **Primary user** | Power devs, team leads | Enterprise, mobile-first | Google ecosystem | GitHub ecosystem | VS Code users | Open-source devs | CLI minimalists | Qwen model users | Rust/DeepSeek fans |
| **Multi-agent maturity** | Highest (3 canonical issues, design docs) | Medium (cross-thread primitives) | Medium (hierarchical) | Low (subagent bugs) | N/A | High (3 proposals) | Low | N/A | Medium (token budgets) |
| **Extensibility model** | Hooks + MCP + Cowork | MCP + plugins | Skills + auto-memory | Hooks + MCP + plugins | Skills + config | LayerNode architecture | Provider registry | Custom providers | TOML config + crates |
| **Platform strength** | macOS/Universal | macOS/Windows (regressing) | Linux-first | GitHub integration | Windows + Git Bash | Cross-platform (musl broken) | Cross-platform | Cross-platform | Linux/Windows (TUI freezes) |
| **Mobile/remote** | Remote Control (iOS) | Mobile app (iOS, Android) | N/A | N/A | N/A | Slack integration planned | N/A | N/A | N/A |
| **Model ecosystem** | Anthropic Claude | OpenAI (GPT-5.5) | Google Gemini | GitHub Models | Kimi (Moonshot) | Multi-model (Devstral, GLM, etc.) | Multi-provider (Fireworks, Neuralwatt) | Qwen-first, OpenAI-compatible | DeepSeek-first, multi-provider |
| **Threat model awareness** | High (Cowork data loss) | High (sandbox metadata) | Medium (Auto Memory sec) | Medium (hook misconfig) | Low | Medium (skill enumeration) | Low | High (URL validation sweep) | High (agent scope creep) |

**Key differentiation insights:**
- **Claude Code** is the most mature in multi-agent orchestration thinking, with three-year-old design docs (#1770) still being referenced.
- **OpenAI Codex** is the only tool with a mobile-first strategy (iOS/Android apps), but platform reliability is its weakest link.
- **Gemini CLI** has the most sophisticated memory system (Auto Memory), but security gaps and retry loops undermine trust.
- **Qwen Code** is uniquely aggressive in security hardening—10 URL case-sensitive issues filed in one day, with matching PRs.
- **DeepSeek TUI** is the only tool written in Rust, with a maintainer-led modularization effort that signals architectural debt.

---

## 5. Community Momentum & Maturity

| Metric | Leading Tools | Commentary |
|---|---|---|
| **Highest community engagement** | Claude Code, OpenAI Codex | Both have 10+ hot issues with extensive discussion (25+ comments), suggesting deep user investment. |
| **Fastest iteration velocity** | Qwen Code, OpenCode | Shipping both stable and nightly releases; Qwen Code's 10 security fix PRs in 24h signal rapid triage. |
| **Most upvoted issue** | OpenAI Codex (#2847, 409 👍 for `.codexignore`) | Indicates feature demand that outpaces tool capacity. |
| **Most commented issue** | OpenAI Codex (#29189, 55 comments for sandbox regression) | Crisis-level community attention. |
| **Highest PR volume** | OpenCode (18 PRs from jlongster alone), DeepSeek TUI (10+ PRs active) | Indicates major architectural refactoring. |
| **Maintainer responsiveness** | DeepSeek TUI (maintainer filed 15+ refactoring issues) | Transparent about technical debt; good signal for long-term health. |
| **Stability concerns** | OpenAI Codex (sandboxPolicy regression), Claude Code (pty leak, unsigned binary) | Both have launch-blocking bugs for some users. |
| **Newcomer-friendly** | Pi (v0.79.9 with streaming fix from community), Kimi Code CLI (low activity but responsive) | Lower engagement but lower breakage risk. |

---

## 6. Trend Signals

### 1. **The "Session-as-Process" Pattern is Emerging as an Industry Standard**
Across Claude Code (#24798, #28300, #1770), OpenAI Codex (#14923), OpenCode (#5887, #12711), and DeepSeek TUI (#3321), the community is demanding programmable session primitives. The convergence on IPC messaging, background delegation, and token budgets suggests this will become an expected baseline feature within 6–12 months.

### 2. **Security Hygiene is Becoming a Competitive Moats**
Qwen Code's systematic URL validation sweep (10+ issues), OpenAI Codex's `.codexignore` demand (409 👍), and Gemini CLI's Auto Memory security concerns (#26525) indicate that input validation and secret management are emerging as differentiators. Tools that ship robust threat models early will win enterprise trust.

### 3. **Multi-Platform Reliability is the New Minimum Viable Product**
The number of platform-specific bugs (macOS signing, Windows sandbox, Linux musl, Wayland, Git Bash) suggests that cross-platform support is still immature. The tools that invest in Windows/Linux parity early (notably Qwen Code and OpenCode) will capture growing markets outside the macOS-centric early adopter base.

### 4. **MCP Protocol is Becoming a Bottleneck**
Both Claude Code (#36431) and OpenAI Codex (#29279) have high-severity MCP notification bugs where inbound messages are silently dropped or OAuth state is not propagated. As MCP becomes the primary extensibility mechanism, these reliability issues will become existential for plugin/marketplace strategies.

### 5. **Agent Reliability is Table Stakes, Not a Feature**
The most impactful bugs across all tools are not missing features—they are agents that hang (Gemini #21409, DeepSeek #2487), exceed scope (DeepSeek #3275), or silently lose data (Claude Code #40175, #48945). The community is signaling that trust in autonomous agents requires deterministic failure modes, **not** just more capabilities.

### 6. **Rate-Limit and Cost Transparency is Critical for Adoption**
OpenAI Codex's 10–20× token cost jump (#28879) is the most explosive issue this week, resonating with broader community frustration across GitHub Copilot CLI (#1240) and OpenCode (#6152). Users are demanding per-session cost breakdowns, compaction visibility, and predictable billing. Tools that fail to provide these will lose power users to competitors that do.

### 7. **The Kimi Code Anomaly: Low Activity May Signal Strategic Pivot**
Kimi Code CLI's near-zero activity (2 issues, 1 PR) in a week of intense activity elsewhere is notable. This could indicate a stabilization phase, a resource reallocation, or a strategic reassessment—either way, it warrants monitoring for ecosystem fragmentation risks.

---

**Bottom line for technical decision-makers:** If you need **production-grade multi-agent orchestration today**, Claude Code is the most mature choice despite pty leaks and silent data loss. If you're **embedded in the OpenAI ecosystem**, Codex's mobile workflow and MCP extensibility are compelling, but its sandbox regression and cost instability are risks. For **multi-platform teams**, OpenCode or Qwen Code offer better cross-platform reliability at the cost of smaller plugin ecosystems. DeepSeek TUI is a dark horse for Rust-native performance and maintainer transparency, but UI freezes and agent scope creep are unresolved. The market is consolidating around session-as-process and MCP extensibility—choose a tool that invests deeply in both.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot:** github.com/anthropics/skills · 2026-06-21

---

## 1. Top Skills Ranking

The following Skills (Pull Requests) have attracted the most community discussion and attention:

### #514 — Document Typography Skill *(Open)*
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses a universal pain point: Claude-generated documents regularly exhibit typographic flaws that human editors must fix manually.

**Discussion highlights:** Commenters noted that nearly every document Claude generates suffers from these issues, making this one of the highest-impact quality-of-life Skills proposed. The PR has remained open for over 3 months without merge, suggesting substantive review.

**Status:** Open (created 2026-03-04, updated 2026-03-13)
[View PR #514](https://github.com/anthropics/skills/pull/514)

---

### #486 — ODT Skill *(Open)*
**Functionality:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods). Includes template filling and ODT-to-HTML parsing. Targeted at LibreOffice/OpenOffice users and organizations requiring ISO-standard document formats.

**Discussion highlights:** The PR addresses a format gap—most existing Skills focus on .docx and .pdf. Community interest centers on interoperability with enterprise document workflows.

**Status:** Open (created 2026-03-01, updated 2026-04-14)
[View PR #486](https://github.com/anthropics/skills/pull/486)

---

### #210 — Frontend-Design Skill Improvement *(Open)*
**Functionality:** Revises the existing frontend-design skill to improve clarity, actionability, and internal coherence. Ensures every instruction is executable within a single Claude conversation and that guidance is specific enough to steer behavior without ambiguity.

**Discussion highlights:** The PR represents a community-driven refactor of an existing Skill, suggesting users found the original insufficiently actionable. Commenters focused on making instructions Claude-executable rather than human-readable.

**Status:** Open (created 2026-01-05, updated 2026-03-07)
[View PR #210](https://github.com/anthropics/skills/pull/210)

---

### #83 — Skill-Quality-Analyzer & Skill-Security-Analyzer *(Open)*
**Functionality:** Two meta-skills: a comprehensive quality analysis tool evaluating Skills across structure/documentation, correctness, completeness, security, and UX; and a security analyzer scanning for prompt injection, dangerous command execution, and unsafe file operations.

**Discussion highlights:** As "meta-skills" that evaluate other Skills, these generated significant debate about how the Skills ecosystem should self-govern. The security analyzer addresses a recognized trust gap in the community.

**Status:** Open (created 2025-11-06, updated 2026-01-07)
[View PR #83](https://github.com/anthropics/skills/pull/83)

---

### #538 — Fix Case-Sensitive File References in PDF Skill *(Open)*
**Functionality:** Corrects 8 case-sensitivity mismatches between SKILL.md references and actual filenames (`REFERENCE.md` → `reference.md`, `FORMS.md` → `forms.md`). Fixes breakage on case-sensitive filesystems (Linux/macOS).

**Discussion highlights:** While a mechanical fix, the PR attracted comments due to its broader implication: existing Skills in the repository have cross-platform compatibility issues. Community members flagged that this is likely not an isolated case.

**Status:** Open (created 2026-03-06, updated 2026-04-29)
[View PR #538](https://github.com/anthropics/skills/pull/538)

---

### #539 — Warn on Unquoted YAML Descriptions *(Open)*
**Functionality:** Adds pre-parse validation in `quick_validate.py` to detect unquoted `description` fields containing YAML special characters (`:`, `#`, etc.). Prevents silent YAML parsing failures that truncate or corrupt skill descriptions.

**Discussion highlights:** This fix addresses a recurring pattern of skill submission bugs—multiple PRs (#361, #539) tackle the same root cause, indicating widespread confusion about YAML frontmatter requirements.

**Status:** Open (created 2026-03-06, updated 2026-04-16)
[View PR #539](https://github.com/anthropics/skills/pull/539)

---

### #1298 — Fix run_eval.py Always Reporting 0% Recall *(Open)*
**Functionality:** Repairs the skill-creator evaluation pipeline where `run_eval.py` reports `recall=0%` for every skill description regardless of content. Fixes include installing the eval artifact as a real skill, Windows stream reading, trigger detection, and parallel workers.

**Discussion highlights:** This fix addresses the most-discussed bug in the community (Issue #556 with 12 comments). The description-optimization loop has been "optimizing against noise" for months, rendering the skill-creator toolchain unreliable.

**Status:** Open (created 2026-06-10, updated 2026-06-20)
[View PR #1298](https://github.com/anthropics/skills/pull/1298)

---

## 2. Community Demand Trends

From the most-commented Issues, three clear demand patterns emerge:

### 1. Skill Sharing & Distribution Infrastructure
**Issue #228** (14 comments, 7 👍) — "Enable org-wide skill sharing in Claude.ai" — The top-voted issue demands a shared skill library or direct sharing links within organizations. Current workflow requires downloading `.skill` files and manually uploading them—a friction point for teams adopting Skills at scale.

### 2. Evaluation & Optimization Pipeline Reliability
**Issues #556** (12 comments, 7 👍) and **#1169** (3 comments) — Both report the same critical bug: `run_eval.py` returns 0% trigger rate across all queries, making the description-optimization loop inoperable. This is the single largest blocker for skill creators—without reliable evaluation, iterative improvement is impossible.

### 3. Trust & Security Framework
**Issue #492** (7 comments, 2 👍) — "Security: Community skills distributed under anthropic/ namespace enable trust boundary abuse" — Community members have identified that user-uploaded Skills appear under the `anthropic/` namespace, creating a trust vulnerability. Users may grant elevated permissions to community Skills they mistake for official Anthropic offerings.

**Additional signals:**
- **Windows compatibility** is a persistent pain point (Issues #1061, #1169, plus PRs #1050, #1099)
- **Duplicate Skill installation** (Issue #189, 6 comments, 9 👍): plugin duplication causes context window waste
- **Agent governance** (Issue #412): a proposed Skill for safety patterns in AI agent systems

---

## 3. High-Potential Pending Skills

These active-comment PRs show strong community engagement and may land soon:

### #1298 — Fix run_eval.py Recall Bug *(Open, very active)*
The most recent major bugfix PR (created 2026-06-10). Addresses the critical `recall=0%` bug in the skill-creator eval pipeline. With 10+ independent reproductions reported, this fix has high community urgency.

### #1099 — Fix run_eval.py Windows Crash *(Open)*
Fixes `run_eval.py` being unusable on Windows due to subprocess pipe errors (`[WinError 10038]`). Complements #1298 with Windows-specific fixes.

### #1050 — Fix Windows Subprocess + Encoding Bugs *(Open)*
Solves two Windows compatibility issues: `PATHEXT` handling for `claude.cmd` and UTF-8 encoding over pipes. Minimal changes (1-line each) suggest quick merge potential.

### #723 — Testing-Patterns Skill *(Open)*
Adds a comprehensive testing skill covering unit testing, React component testing, end-to-end testing, and testing philosophy (Testing Trophy model). Addresses a clear gap—no testing skill currently exists in the repository.

### #568 — ServiceNow Platform Skill *(Open)*
A broad ServiceNow platform assistant covering ITSM, ITOM, ITAM, FSM, HRSD, CSM, SPM, Security Incident Response, and IntegrationHub. Targets enterprise ServiceNow users—a large potential audience.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, cross-platform skill development toolchain**—specifically, fixing the broken evaluation pipeline that prevents skill creators from iterating effectively, while simultaneously requesting infrastructure for skill sharing, security boundaries, and Windows compatibility.

---

# Claude Code Community Digest — 2026-06-21

## Today's Highlights
A cluster of long-running feature requests around **multi-agent orchestration and inter-session communication** continues to dominate the community's attention, with Issue #24798 (37 comments) and #28300 (29 comments) nearing resolution-level discussion. A **new desktop app pty leak** (Issue #66434) was confirmed, and v2.1.185 shipped a small but welcome quality-of-life fix to the stream-stall timeout UX. The community's top request direction is now unambiguously a **first-class session-as-process primitive** for programmatic multi-session workflows.

## Releases
**v2.1.185** — Stream-stall hint text changed from `"No response from API · Retrying in …"` to `"Waiting for API response · will retry in …"`; timeout threshold increased from 10s to 20s. Small UX improvement reduces false-alarm anxiety during long model thinking.  
[View release](https://github.com/anthropics/claude-code/releases/tag/v2.1.185)

## Hot Issues
1. **[#24798] Inter-session communication for multi-Claude workflows** — 37 comments, 18 👍. Long-running (Feb '26) proposal for direct message passing between parallel Claude Code sessions. Community has added sequence diagrams and API proposals. This is the *de facto* canonical feature request for multi-agent chat.  
   [View issue](https://github.com/anthropics/claude-code/issues/24798)

2. **[#28300] Multi-agent collaboration across machines (Agent-to-Agent protocol)** — 29 comments. Extends inter-session comms to cross-host scenarios. Growing interest from teams running fleet orchestrations.  
   [View issue](https://github.com/anthropics/claude-code/issues/28300)

3. **[#40175] Cowork: Global instructions silently revert to older version** — 25 comments, 12 👍. A nasty data-loss bug where saved Cowork instructions are replaced by stale versions. Reproduced on both macOS and Windows. High urgency for team users.  
   [View issue](https://github.com/anthropics/claude-code/issues/40175)

4. **[#36431] Telegram plugin: inbound MCP channel notifications not delivered** — 19 comments, 31 👍. Inbound messages are received but never surface in the active conversation. Outbound works fine. Highly upvoted — suggests strong demand for MCP-driven notification workflows.  
   [View issue](https://github.com/anthropics/claude-code/issues/36431)

5. **[#1770] Parent-Child Agent Communication and Monitoring in Task Tool** — 14 comments, 25 👍. The oldest open multi-agent feature request (June 2025). Contains an extensively detailed design doc with sequence diagrams. A foundational reference.  
   [View issue](https://github.com/anthropics/claude-code/issues/1770)

6. **[#48945] Plan-file inline comments don't reach the model on resume** — 12 comments, 6 👍. Plan comments (`"Leave a comment for Claude"`) are silently lost when resuming a session from a plan file. Closed as bug — impacts anyone using structured planning workflows.  
   [View issue](https://github.com/anthropics/claude-code/issues/48945)

7. **[#17088] PreToolUse hook shows 'error' label even for successful (exit 0) hook runs** — 11 comments, 27 👍. Misleading UI noise: successful hooks are labeled as errors. Simple fix, high noise factor for heavy hook users.  
   [View issue](https://github.com/anthropics/claude-code/issues/17088)

8. **[#29438] Remote Control: Push notifications on iOS when permission approval is needed** — 10 comments, 56 👍. *Highest upvoted open issue.* Request for push notifications when a remote control session blocks on user consent. Currently users must keep the app open.  
   [View issue](https://github.com/anthropics/claude-code/issues/29438)

9. **[#66434] Desktop app leaks pseudo-terminals (ptys) until system runs out** — 7 comments, 4 👍. A single long-running desktop app instance accumulated 508 open ptys. Causes `forkpty: Device not configured` crashes. Potentially severe for power users keeping sessions alive for days.  
   [View issue](https://github.com/anthropics/claude-code/issues/66434)

10. **[#61114] Desktop app crashes on launch: bundled Claude Code binary is unsigned/malformed** — 7 comments. Regression affecting macOS arm64 v1.8089.1. The bundled `2.1.142` binary is not code-signed. Blocks all usage until patch.  
    [View issue](https://github.com/anthropics/claude-code/issues/61114)

## Key PR Progress
1. **[#69727] fix(hookify): match file rules against Write tool content** — Fixes a silent bug where `event: file` hookify rules (e.g., "Warn About Debug Code") never fired when Claude created a file via the `Write` tool. Root cause: config loader inferred wrong field name.  
   [View PR](https://github.com/anthropics/claude-code/pull/69727)

2. **[#69716] fix(workflows): send Statsig event time in milliseconds** — Fixes a type mismatch where `claude-dedupe-issues.yml` sent epoch seconds (as string) to an API expecting milliseconds (number).  
   [View PR](https://github.com/anthropics/claude-code/pull/69716)

3. **[#69710] docs: Update plugins README to use recommended install methods** — Removes deprecated `npm install -g @anthropic-ai/claude-code` instructions from `plugins/README.md`. Aligns with top-level README's `curl -fsSL` approach.  
   [View PR](https://github.com/anthropics/claude-code/pull/69710)

4. **[#69698] fix(hookify): use root-relative imports to fix marketplace install** — Fixes import path resolution when hookify is installed via the marketplace rather than bundled.  
   [View PR](https://github.com/anthropics/claude-code/pull/69698)

*(Note: Only 4 PRs were active in the last 24h.)*

## Feature Request Trends
The dominant theme this week is **session-as-a-primitive for programmatic multi-agent coordination**. The community is coalescing around three concrete asks:

1. **Cross-session messaging** — Issue #24798, #28300, #35072, #55981. A reliable IPC mechanism so parallel Claude Code sessions can send messages, wake each other up, and coordinate dependencies without manual human intervention.

2. **Session handoff / spawn-and-read-back** — Issue #65456, #68996. Users want to programmatically spawn an autonomous Claude Code session in a different project directory, hand it a prompt, let it run to completion, and read its results — essentially treating a session like a subprocess with stdout/stdin.

3. **Multi-user real-time collaboration** — Issue #60082. Users want Google Docs / VS Code Live Share-style simultaneous editing of a single Claude Code session from different user accounts.

A secondary theme: **Remote Control improvements** (#29438, #47926) — push notifications for blocked permission prompts and cross-device session resume.

## Developer Pain Points
- **Silent data loss** remains the #1 pain category: plan-file comments lost on resume (#48945), Cowork instructions silently reverted (#40175), and desktop session transcripts not persisted to host (#69764). These erode trust.
- **Misleading UI noise** frustrates heavy users: successful hooks labeled as errors (#17088) and `/goal` long prompts lacking collapse controls (#61675).
- **Plugin/hook reliability**: Telegram MCP plugin silently drops inbound notifications (#36431), and hookify file rules never fire for `Write` tool content (#69727).
- **Desktop stability regressions**: unsigned binary blocks launch on macOS (#61114) and pty leaks crash long-running sessions (#66434). Both are launch-blockers for affected users.
- **Authentication friction**: 401 errors on Windows (#69706) and "Buy credits" button permanently disabled with erroneous $500 limit display (#62644) suggest billing/API auth state management issues.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-21

## Today's Highlights

A major `sandboxPolicy` metadata bug surfaced across Windows and macOS Codex Desktop releases (26.616.x), breaking `node_repl`, Browser Use, and Computer Use for a significant number of users. On the development side, OpenAI engineers merged or prepared several infrastructure PRs improving token budget management, MCP history injection, and environment context serialization. Community feature requests remain focused on cross-thread orchestration, external integrations (Telegram, Slack), and event-driven session wake primitives.

## Releases

**No new releases in the last 24 hours.** The latest tagged release remains at Codex Desktop 26.616.41845 / CLI 0.142.0-alpha.6.

## Hot Issues (10 selected)

### [#29189 — Codex Desktop 26.616.41845 node_repl fails: sandbox-state-meta missing sandboxPolicy](https://github.com/openai/codex/issues/29189)
**Why it matters:** This is the most commented issue today (55 comments, 63 👍), affecting macOS users with Chrome plugin/REPL workflows. The error `codex/sandbox-state-meta missing sandboxPolicy` blocks all REPL tooling, making @Browser and @Computer Use unavailable. Appears to be a regression in the 26.616 build’s sandbox metadata propagation.

### [#2847 — Feature request: a way to exclude sensitive files](https://github.com/openai/codex/issues/2847)
**Why it matters:** The highest-reacted open issue (409 👍, 78 comments). The community strongly wants `.codexignore`-style mechanisms—both repo-local and global—to prevent the agent from reading or uploading sensitive files. No official response on timeline yet, but clearly a top pain point.

### [#29219 — Codex Desktop ignores node_repl args and sends malformed sandbox metadata](https://github.com/openai/codex/issues/29219)
**Why it matters:** Related to #29189 but from a different angle: user reports `mcp__node_repl.js` rejects JavaScript calls before execution. A local workaround exists via managing sandbox endpoints, but this confirms the `sandboxPolicy` field is not being correctly propagated from server configuration to the tool call payload.

### [#28879 — Rate-limit cost per token jumped ~10-20x since June 16](https://github.com/openai/codex/issues/28879)
**Why it matters:** 72 👍 and 37 comments. Users on Plus plans report budget draining in 2-3 prompts instead of 20+. Session logs confirm `rate_limits` consumption increased 10–20× with no model change. A critical cost-of-use regression that may be driving user dissatisfaction.

### [#22898 — Codex mobile shows running desktop as offline; Reconnect silently does nothing](https://github.com/openai/codex/issues/22898)
**Why it matters:** 40 👍, 14 comments. The iOS app cannot see an active Mac desktop, and the Reconnect button has no feedback. This breaks remote monitoring and approval workflows—a key use case for the ecosystem.

### [#18960 — Frequent reconnect loop in Codex App: websocket closed by server](https://github.com/openai/codex/issues/18960)
**Why it matters:** 50 comments, 35 👍. Streaming failures cause repeated reconnect cycles with no backoff. Users on macOS Pro plans report this happens multiple times per session, making long-running tasks unreliable.

### [#29117 — Windows sandbox repeatedly asks for permission despite “Full Access”](https://github.com/openai/codex/issues/29117)
**Why it matters:** 10 👍, 9 comments. On Windows 11, granting full access does not persist; Codex CLI re-prompts for every operation. This is breaking automation on the platform.

### [#29000 — Codex CLI 0.141.0 crashes with SIGTRAP on Intel macOS](https://github.com/openai/codex/issues/29000)
**Why it matters:** A native crash (SIGTRAP) on Intel Macs affects users running `gpt-5.5`. 7 👍, 7 comments. No workaround reported; likely an arch-specific codegen or memory alignment issue in the CLI binary.

### [#14923 — Feature request: explicit cross-thread orchestration](https://github.com/openai/codex/issues/14923)
**Why it matters:** 12 comments, thoughtful discussion. The community wants primitives to orchestrate threads (`thread/wait`, `thread/signal`, `thread/cancel`) from within agent code, enabling multi-agent parallelism and job orchestration patterns.

### [#29279 — MCP OAuth login succeeds but thread remains stuck on “OAuth authorization required”](https://github.com/openai/codex/issues/29279)
**Why it matters:** Latest report today (2 comments, urgent). MCP OAuth flow completes in the browser, but the active Desktop thread does not recognize the updated authorization state. Blocks all remote MCP tool usage until thread restart.

## Key PR Progress (10 selected)

### [#29255 — Add configurable token budget compaction reminder](https://github.com/openai/codex/pull/29255)
**What it does:** Adds a model-facing prompt before automatic compaction fires, with configurable thresholds. Addresses the gap where compaction happens silently mid-task. *Merged.*

### [#29249 — Migrate environment context to model world state](https://github.com/openai/codex/pull/29249)
**What it does:** Introduces a typed, replayable "world state" slice for environments, replacing transient turn-value rendering. Enables deterministic resume and fork behavior. *Open, code-reviewed.*

### [#29259 — Prototype mcp_history thread hint injection](https://github.com/openai/codex/pull/29259)
**What it does:** Tests calling `mcp_history` MCP during context construction to expose thread hints to the model without requiring a tool call. Reduces latency for history-aware decisions. *Merged.*

### [#26229 — Add protected data mode to core and app server](https://github.com/openai/codex/pull/26229)
**What it does:** Introduces core-managed Protected Data Mode. When active via a shared marker, connector calls require explicit OAuth consent before proceeding, with state preserved across resume and fork. *Merged.*

### [#28806 — Optimize resume and fork history (checkpoint + COW)](https://github.com/openai/codex/pull/28806)
**What it does:** Applies checkpoint-backed resume and copy-on-write fork to reduce cold-start history work for `thread/resume` and `thread/fork`. Includes fallback for legacy metadata. *Open.*

### [#28232 — Add workspace headline statusline item](https://github.com/openai/codex/pull/28232)
**What it does:** Adds a configurable TUI status-line item showing active workspace headline from ChatGPT/Codex backend. Refreshes every 10 seconds via app-server. *Open.*

### [#28845 — Support plugin agent roles](https://github.com/openai/codex/pull/28845)
**What it does:** Bundles agent role TOML manifests inside plugins, enabling `spawn_agent` with namespaced types like `sample:researcher`. Includes scaffolding and manifest doc updates. *Open.*

### [#29143 — CI: restore custom Windows runner with hermetic LLVM 0.7.9](https://github.com/openai/codex/pull/29143)
**What it does:** Returns the argument-comment-lint CI job to the custom Windows runner after fixing hermetic LLVM extraction failures on `windows-2022`. *Open.*

### [#29266 — Route image generation writes through ExecutorFileSystem](https://github.com/openai/codex/pull/29266)
**What it does:** Routes generated image directory/file writes through `ExecutorFileSystem` while preserving existing `CODEX_HOME/generated_images` destination. Enables sandbox-aware image output management. *Open.*

### [#29268 — Revert “Scope MCP sandbox metadata to server environment”](https://github.com/openai/codex/pull/29268)
**What it does:** Reverts commit #28914, which appears to have caused the `sandboxPolicy` missing-field regression affecting node_repl, Browser, and Computer Use across platforms in build 26.616. *Open.*

## Feature Request Trends

1. **Sensitive file exclusion (.codexignore)** — Across repo-local and global levels, this is the most upvoted request. Users want explicit denylist semantics instead of relying on agent instruction prompts.

2. **Event-driven session wake** — Multiple issues ([#20312](https://github.com/openai/codex/issues/20312), [#15299](https://github.com/openai/codex/issues/15299), [#14923](https://github.com/openai/codex/issues/14923)) ask for native primitives for idle sessions to react to external events (MCP notifications, chat mentions, file changes). Currently Codex is strictly turn-driven.

3. **External platform integrations** — Requests for official Telegram ([#21166](https://github.com/openai/codex/issues/21166)) and Slack ([#20475](https://github.com/openai/codex/issues/20475)) plugins, with mobile push notifications for agents ([#11820](https://github.com/openai/codex/issues/11820)).

4. **Cross-thread orchestration** — Community wants explicit thread synchronization primitives (wait, signal, cancel, join) for multi-agent and parallel job patterns.

5. **Local ingress for CLI/TUI sessions** — Opt-in local pipes for trusted processes to send input with session semantics rather than PTY emulation.

## Developer Pain Points

- **Sandbox metadata regression (sandboxPolicy)** — The dominant pain point today. Multiple issues ([#29189](https://github.com/openai/codex/issues/29189), [#29219](https://github.com/openai/codex/issues/29219), [#29205](https://github.com/openai/codex/issues/29205), [#29242](https://github.com/openai/codex/issues/29242)) report tool failures on both macOS and Windows after the 26.616 update. The proposed revert [#29268](https://github.com/openai/codex/pull/29268) suggests the root cause is an overly-scoped sandbox metadata change in commit #28914.

- **Rate-limit budget surprise** — The 10–20× token cost increase reported in [#28879](https://github.com/openai/codex/issues/28879) is causing significant frustration. Users feel they are burning paid credits with no explanation or recourse.

- **Windows sandbox persistence** — Permission prompts ([#29117](https://github.com/openai/codex/issues/29117)), ACL corruption after crashes ([#28248](https://github.com/openai/codex/issues/28248)), and WSL incompatibility ([#26424](https://github.com/openai/codex/issues/26424)) make Windows a second-class platform for sandboxed agent operations.

- **WebSocket reliability** — Reconnect loops ([#18960](https://github.com/openai/codex/issues/18960)) and silent offline state on mobile ([#22898](https://github.com/openai/codex/issues/22898)) degrade the remote-aware workflow. Users report no diagnostic feedback during failures.

- **Git compatibility on Windows** — Libgit2-based clients break when Codex writes turn-diff tree refs ([#28241](https://github.com/openai/codex/issues/28241)). Niche but deeply impacts Windows Git workflows.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-06-21

## Today's Highlights

This week's digest shows the Gemini CLI team and community continue to tackle fundamental agent reliability challenges, with significant work on sub-agent control flow, memory system hygiene, and tool execution stability. The open issues reveal strong demand for multi-agent collaboration patterns and better agent self-awareness, while the PR pipeline demonstrates active work on security fixes, documentation accuracy, and multimodal input support. Despite no new releases in the last 24 hours, the volume of high-quality community contributions and critical bug reports suggests a period of intensive stabilization.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **Multi-Agent Collaboration Architecture ([[#19430](https://github.com/google-gemini/gemini-cli/issues/19430)])** – One of the highest-signal community requests with 43 👍. Users want true parallel agent teams similar to Claude Code’s implementation, including local and remote agents running as co-workers rather than in a strict hierarchy. This reflects a growing expectation for Gemini to support complex, concurrent workflows.

2. **Generalist Agent Hangs ([[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)])** – A critical P1 bug where the generalist agent hangs indefinitely on simple tasks like folder creation. The workaround (disabling sub-agent delegation) highlights a deep issue in agent orchestration that erodes user trust.

3. **Subagent MAX_TURNS Masked as Success ([[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)])** – Sub-agents hitting their turn limit report `status: "success"` instead of surfacing the interruption. This false-positive reporting makes debugging agent failures much harder and undermines confidence in the agent’s feedback loop.

4. **Tool Limit 400 Error ([[#24246](https://github.com/google-gemini/gemini-cli/issues/24246)])** – A practical scalability issue: the CLI hits a 400 error when more than ~128 tools are available, without smart tool scoping. For power users with many custom tools, this is a hard blocker.

5. **AST-Aware File Operations Investigation ([[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)])** – A significant EPIC exploring whether AST-based file reads and codebase mapping could reduce token waste and improve agent accuracy. This work could dramatically improve how Gemini understands code structure.

6. **Auto Memory Security Concerns ([[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)])** – Critical feedback that Auto Memory sends transcript content to the model before redacting secrets, and can log existing skill definitions with embedded secrets in logs. A fundamental security gap in the memory pipeline.

7. **Shell Execution Stuck on "Waiting Input" ([[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)])** – A P1 bug where completed shell commands remain marked as awaiting input, causing hangs. This is a recurring frustration affecting core CLI reliability.

8. **Browser Agent Wayland Failure ([[#21983](https://github.com/google-gemini/gemini-cli/issues/21983)])** – The browser subagent crashes on Wayland systems, limiting accessibility for Linux users on modern display servers.

9. **Subagents Running Without Permission ([[#22093](https://github.com/google-gemini/gemini-cli/issues/22093)])** – A concerning behavioral issue where agents run sub-agents despite disabled agent modes in config. This breaks the trust model of user-configured safety settings.

10. **Memory System Low-Signal Retry Loop ([[#26522](https://github.com/google-gemini/gemini-cli/issues/26522)])** – Auto Memory can retry low-signal sessions indefinitely because it only marks sessions as processed after a successful `read_file`. This creates inefficiency and potential infinite loops in the memory pipeline.

## Key PR Progress

1. **MCP Image MIME Type Detection Fix ([[#27878](https://github.com/google-gemini/gemini-cli/pull/27878)])** – A critical P1 fix for WebP images from Figma MCP being mislabeled as PNG, causing HTTP 400 errors. Implements local image signature sniffing for accurate MIME detection—a practical win for designers using Gemini with design tools.

2. **Drag-and-Drop and Clipboard Image Pasting ([[#27859](https://github.com/google-gemini/gemini-cli/pull/27859)])** – Adds native terminal drag-and-drop and Cmd+V image pasting, addressing a long-standing gap in multimodal input. This brings Gemini CLI closer to visual parity with other AI tools.

3. **Pending Tool Response Capping ([[#27870](https://github.com/google-gemini/gemini-cli/pull/27870)])** – Fixes a crash where very large tool results could overwhelm the pending `functionResponse` buffer. An important stability improvement for heavy tool usage.

4. **Shell-quote Security Upgrade ([[#27856](https://github.com/google-gemini/gemini-cli/pull/27856)])** – Upgrades `shell-quote` to fix CVE-2026-9277 (CRITICAL severity). Essential security hygiene for command execution safety.

5. **Dollar Sequence Preservation in Prompt Templates ([[#28055](https://github.com/google-gemini/gemini-cli/pull/28055)])** – Fixes corruption of `$` sequences (e.g., `$$`, `$'`, `$&`) in skill and tool descriptions during template substitution. A subtle but important bug for anyone using shell-style templating.

6. **Perioid Stripping from Error URLs ([[#28054](https://github.com/google-gemini/gemini-cli/pull/28054)])** – Removes trailing periods from error message URLs so links remain clickable. Small UX improvement with outsized impact on developer debugging flow.

7. **CLI Crash in Cloud Shell on Unreadable .env ([[#28059](https://github.com/google-gemini/gemini-cli/pull/28059)])** – Gracefully handles `EACCES` errors on `.env` files in Cloud Shell environments, preventing a startup crash that cascaded into Docker failures.

8. **JSON Output for Eval Inventory ([[#28058](https://github.com/google-gemini/gemini-cli/pull/28058)])** – Adds `--json` flag to eval inventory for CI/script consumption. A practical quality-of-life improvement for teams running automated evaluations.

9. **Documentation Fixes: Hooks and Manifests ([[#28064](https://github.com/google-gemini/gemini-cli/pull/28064), [#28057](https://github.com/google-gemini/gemini-cli/pull/28057)])** – Two PRs correcting documentation: documenting the `"ask"` decision in `BeforeTool` hooks and fixing the `usageMetadata` token field docs. Shows active investment in making the hooks system accurately documented.

10. **Vitest Security Upgrade ([[#27857](https://github.com/google-gemini/gemini-cli/pull/27857)])** – Upgrades vitest to fix CVE-2026-47429 (CRITICAL). Part of a broader security sweep in the test infrastructure.

## Feature Request Trends

The community is clearly pushing for **multi-agent collaboration** as the next major capability. Issue #19430 (43 👍) and #22092 both argue for teams of agents working in parallel, not just hierarchical delegation. Users want the ability to offload exploration, linting, and building to background agents while the main agent continues reasoning ([[#22741](https://github.com/google-gemini/gemini-cli/issues/22741)]).

There is also strong interest in **AST-aware tooling** (#22745, #22746, #22747) to make codebase understanding more precise and less token-intensive. This suggests the community values efficiency and accuracy over brute-force context loading.

A quieter but significant trend is **agent self-awareness** ([[#21432](https://github.com/google-gemini/gemini-cli/issues/21432)])—users want Gemini to know its own capabilities, hotkeys, and CLI flags well enough to act as its own documentation. This reflects a desire for the tool to be self-explanatory and easier to onboard.

## Developer Pain Points

**Agent reliability** remains the dominant frustration. The generalist agent hanging ([[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)]), sub-agents falsely reporting success ([[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)]), and shell commands getting stuck ([[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)]) all point to a core stability gap that undermines production use.

**Unwanted sub-agent activation** is a recurring theme. Users report agents using sub-agents despite explicit configuration disabling them ([[#22093](https://github.com/google-gemini/gemini-cli/issues/22093)]), and failing to invoke custom skills unless explicitly instructed ([[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)]). This suggests the agent's tool selection heuristics need better respect for user preferences.

**Memory system bugs** are accumulating fast, with five related issues filed on the same day by the same author (#26516, #26522, #26523, #26525). The concerns span security (secrets in logs), infinite retry loops, and silent patch skipping—suggesting the Auto Memory feature may have been rushed and needs significant hardening.

**Terminal/UI issues** like the browser agent failing on Wayland ([[#21983](https://github.com/google-gemini/gemini-cli/issues/21983)]), terminal resize flickering ([[#21924](https://github.com/google-gemini/gemini-cli/issues/21924)]), and post-external-editor display corruption ([[#24935](https://github.com/google-gemini/gemini-cli/issues/24935)]) indicate that the cross-platform terminal experience still has rough edges, particularly on Linux.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI Community Digest — 2026-06-21

### Today's Highlights
The Copilot CLI saw a burst of community activity today with 14 issues updated in 24 hours, signaling strong user engagement after a quiet release window. The most significant development is the closure of Issue #1665 (project-scoped plugins), a long-running request since February, which could reshape how teams manage plugin configurations. Additionally, a new PR (#3873) and several bug reports around hooks, terminal rendering, and agent subagent spawning highlight growing pains as the platform's plugin and agent ecosystems mature.

### Releases
No new releases in the last 24 hours.

### Hot Issues (10 noteworthy)

1. **[#1665 – Support Copilot CLI Plugins Scoped to Project or Repository](https://github.com/github/copilot-cli/issues/1665)** [CLOSED]
   - **Why it matters:** Closed after 4 months, this resolves a major pain point where per-user plugin installation made team-level configuration impossible. With 17 👍, it's the most upvoted issue today.
   - **Community reaction:** The closure indicates the team is likely shipping project-scoped plugin support soon.

2. **[#1240 – Support session-usage in copilot --acp](https://github.com/github/copilot-cli/issues/1240)** [OPEN]
   - **Why it matters:** Author josevalim (Elixir creator) proposes implementing the Agent Client Protocol session-usage RFD, giving users visibility into token consumption and session cost. 8 👍 signal strong interest from power users.

3. **[#3876 – Mouse tracking is incorrectly disabled on exit](https://github.com/github/copilot-cli/issues/3876)** [CLOSED]
   - **Why it matters:** A severe terminal UX bug where CLI exit breaks mouse scrolling. Quickly triaged and closed within a day, suggesting a fast fix.

4. **[#3871 – No way to list installed hooks](https://github.com/github/copilot-cli/issues/3871)** [OPEN]
   - **Why it matters:** Hooks are a core extensibility feature, but there's no discoverability surface. Community expects parity with `copilot mcp list`.

5. **[#3872 – Hook config with mis-cased event key silently dropped](https://github.com/github/copilot-cli/issues/3872)** [CLOSED]
   - **Why it matters:** Silently dropping hook configurations is a reliability hazard. User ken-jo caught a subtle bug that could cause silent failures in production pipelines.

6. **[#3878 – Revert back to Plan mode after plan implemented](https://github.com/github/copilot-cli/issues/3878)** [OPEN]
   - **Why it matters:** Workflow automation enthusiasts want Plan-as-default mode, but auto-switch to Autopilot disrupts repeat planning cycles.

7. **[#3877 – Auto-allow permissions on session start](https://github.com/github/copilot-cli/issues/3877)** [OPEN]
   - **Why it matters:** Permissions fatigue is a real UX concern. Requesting a persistent `/allow-all` setting shows users want faster workflows despite security trade-offs.

8. **[#3875 – Unable to spawn subagents with mai-code-1-flash-picker](https://github.com/github/copilot-cli/issues/3875)** [OPEN]
   - **Why it matters:** Multi-agent orchestration is cutting-edge; this bug breaks subagent spawning with specific model/`deferTools` configurations, impacting advanced Copilot users.

9. **[#3874 – VS Code agent preToolUse hook denial does not work](https://github.com/github/copilot-cli/issues/3874)** [OPEN]
   - **Why it matters:** Hooks are supposed to enforce policy, but denial logic fails in VS Code contexts—a critical gap for enterprise security.

10. **[#3867 – No context window visibility or compaction notification](https://github.com/github/copilot-cli/issues/3867)** [OPEN]
    - **Why it matters:** Context window management is a top UX challenge for long sessions. Users want token gauges and compaction alerts, similar to IDE indicators.

### Key PR Progress (2 notable)

1. **[#2587 – Add automated issue classification with GitHub Agentic Workflows](https://github.com/github/copilot-cli/pull/2587)** [CLOSED]
   - **What it does:** Introduces AI-powered labeling (`area:`, `triage`) via `gh-aw`. This explains today's #3870 (a duplicate test issue with Vietnamese text). The PR is merged, indicating the maintainers are operationalizing triage automation.

2. **[#3873 – 1000Add initial console log for greeting](https://github.com/github/copilot-cli/pull/3873)** [OPEN]
   - **What it does:** A small PR adding a startup greeting log. While trivial, it shows new contributors engaging with the codebase.

### Feature Request Trends
- **Plugin & Hook Discoverability:** Users repeatedly ask for `list`/`get` commands for hooks (matching MCP server tooling). The community expects parity across all plugin types.
- **Session & Context Transparency:** Multiple requests (sessions-usage, context window visibility, compaction notifications) converge on a theme: users want to see what the AI "sees" and how much it costs.
- **Workflow Automation:** Plan-mode defaults, auto-permissions, and session lifecycle control indicate power users want Copilot CLI to operate as a programmable agent, not just an interactive tool.

### Developer Pain Points
- **Silent Failures:** Hooks with mis-cased event keys (#3872) and `preToolUse` denial not working (#3874) erode trust in plugin-based security. Users need explicit validation and error messages.
- **Terminal Hygiene:** Mouse tracking breakage (#3876) and cramped `/ask` output (#3869) degrade the terminal experience. These are low-level but high-friction issues.
- **Multi-Channel Inconsistency:** Hooks behave differently in VS Code vs. CLI (#3874). Developers expect consistent policy enforcement across all Copilot surfaces.
- **Fragile Multi-Agent Orchestration:** Subagent spawning failures (#3875) with specific model/tool configurations show the cutting edge is still bleeding—users with complex setups face unique breakages.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-21

## Today's Highlights
The community saw active maintenance with two long-standing issues resolved, including a critical Windows+Git Bash VS Code extension bug (async). A new open PR addresses system proxy configuration, a recurring pain point for enterprise users. The feature request for clickable symbol references in the chat panel was closed, signaling that inline code navigation may be on the roadmap.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **#2462 [CLOSED] Windows + Git Bash: VS Code extension fails to extract bundled CLI**  
   *Author: yplgame | Updated: 2026-06-20*  
   [GitHub Issue #2462](https://github.com/MoonshotAI/kimi-cli/issues/2462)  
   A critical bug for Windows developers using Git Bash (MSYS2): `tar` cannot handle Zip archives. The issue received a fix and was closed. **Why it matters**: Blocks Windows users from using the VS Code extension, a major adoption gate.

2. **#2440 [CLOSED] Clickable symbol / line references in Kimi Code chat panel**  
   *Author: ElPrg | Updated: 2026-06-20*  
   [GitHub Issue #2440](https://github.com/MoonshotAI/kimi-cli/issues/2440)  
   Request to make function/method names in chat clickable to jump to definitions. Closed without comments – likely merged into a broader roadmap. **Why it matters**: Directly impacts developer workflow efficiency when reviewing AI suggestions.

3. *(No further hot issues in the last 24h)*  
   *Note: Only 2 issues received updates in the reporting period. Both are covered above.*

## Key PR Progress

1. **#2063 [CLOSED] feat(config): add default_skills config for auto-activating skills**  
   *Author: maxBRT | Updated: 2026-06-20*  
   [GitHub PR #2063](https://github.com/MoonshotAI/kimi-cli/pull/2063)  
   Implements #2062: new `default_skills` config key to auto-activate skills on session start. **Impact**: Reduces repetitive setup for users who rely on custom skill chains.

2. **#2463 [OPEN] fix: respect system proxy settings in FetchURL**  
   *Author: itxaiohanglover | Updated: 2026-06-20*  
   [GitHub PR #2463](https://github.com/MoonshotAI/kimi-cli/pull/2463)  
   Fixes `aiohttp.ClientSession` ignoring `HTTP_PROXY`/`HTTPS_PROXY` env vars, causing `Connection reset by peer` in proxied environments. **Impact**: Critical for corporate/enterprise users behind firewalls.

3. *(No other PRs updated in the last 24h)*

## Feature Request Trends
- **Contextual navigation in chat**: Requests for clickable symbol references (issue #2440) are a recurring theme. Developers want to quickly jump between AI suggestions and their codebase.
- **Proxy support**: Multiple reports (including #2463) indicate users struggle with network restrictions. Enterprise adoption depends on proper proxy configuration.
- **Skill auto-activation**: PR #2063 addresses a long-standing request to streamline startup workflows, especially for power users with complex skill environments.

## Developer Pain Points
- **Windows hybrid environments**: The Git Bash + VS Code extension bug (#2462) highlights the fragility of cross-platform tooling, especially with archive formats. Community reaction was neutral (0 👍), but the issue severity is high.
- **Network configuration gaps**: Proxy handling remains a top frustration. The `Connection reset by peer` error in corporate settings forces manual workarounds. PR #2463 is an awaited fix.
- **Low community engagement**: Many issues and PRs lack upvotes or comments, suggesting either a small active user base or low urgency. The absence of new releases may signal a stabilization phase.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-21

## Today's Highlights
The core team is executing a major test infrastructure overhaul with **18 PRs from jlongster** simplifying LayerNode wiring across core modules. Community demand for **multi-agent orchestration** continues to dominate, with three distinct feature proposals (#5887, #12711, #19999) all gaining traction. A critical **musl compatibility regression** (#27589) remains unresolved after 36 comments, blocking Alpine Linux users since v1.14.50.

---

## Releases
**v1.17.9** was released in the last 24 hours, focusing on stability fixes:
- **Bugfixes**: Honor configured agent step limits (force final text response instead of failing); fix Devstral model detection for case-insensitive provider IDs (@Robin1987China); pass custom headers to Copilot model requests
- **Improvements**: Add `high`... *(changelog truncated in source data)*

---

## Hot Issues

1. **#27589 — TUI fails on Alpine Linux (musl)** — Regression blocking musl-based systems since v1.14.50. `getcontext` symbol missing in bundled shared library. 36 comments, 12 👍. [Link](https://github.com/anomalyco/opencode/issues/27589)

2. **#8501 — Expand pasted text summaries** — Users want to expand `[Pasted ~1 lines]` placeholders for editing. High demand (183 👍, 26 comments) with no official response yet. [Link](https://github.com/anomalyco/opencode/issues/8501)

3. **#5887 — True async/background sub-agent delegation** — Fire-and-forget background agents that don't block the primary flow. 73 👍, 25 comments. Community building on this concept across multiple issues. [Link](https://github.com/anomalyco/opencode/issues/5887)

4. **#17994 — Multi-agent orchestration in isolated workspaces** — A "team of coding agents" running in sandboxed environments. 22 comments. Growing interest in parallel agent workflows. [Link](https://github.com/anomalyco/opencode/issues/17994)

5. **#6152 — Session context usage tool** — Similar to Claude's `/context` command. 112 👍 indicates strong demand for debugging/observing token usage. [Link](https://github.com/anomalyco/opencode/issues/6152)

6. **#28957 — "Upstream idle timeout exceeded" with writing-plans skill** — macOS Tahoe users hitting timeouts during plan generation. 16 comments, likely infrastructure-side but blocking skill workflows. [Link](https://github.com/anomalyco/opencode/issues/28957)

7. **#32444 — GLM-5.2 thinking variants hidden** — Blanket `glm` exclusion in `variants()` blocks High/Max reasoning toggles. 9 comments, 15 👍. Duplicate of #18598 — this keeps getting raised. [Link](https://github.com/anomalyco/opencode/issues/32444)

8. **#12711 — Agent Teams design proposal** — Flat teams with named messaging, multi-model support, TUI integration. 12 comments, comprehensive design doc. Builds toward more sophisticated agent coordination. [Link](https://github.com/anomalyco/opencode/issues/12711)

9. **#32694 — SIGTRAP crash on HTTP Client thread (macOS/Apple Silicon)** — Bundled Bun 1.3.14 crashes after first message. 4 comments, possibly runtime incompatibility with newer macOS 26. [Link](https://github.com/anomalyco/opencode/issues/32694)

10. **#29462 — Skills tool enumerates all skills with no upper bound** — 100k+ skills injected into every system prompt. Performance concern. 11 comments, no response yet. [Link](https://github.com/anomalyco/opencode/issues/29462)

---

## Key PR Progress

1. **#33190 — Simplify session projector layer wiring** — Builds test environment from canonical LayerNode graph. Part of jlongster's large-scale test refactor. [Link](https://github.com/anomalyco/opencode/pull/33190)

2. **#33189 — Simplify repository cache layer wiring** — Adds canonical LayerNode definition for RepositoryCache. Replaces manual wrappers. [Link](https://github.com/anomalyco/opencode/pull/33189)

3. **#33188 — Simplify session prompt layer wiring** — Adds canonical nodes for SessionV2, SessionStore, SessionExecution. [Link](https://github.com/anomalyco/opencode/pull/33188)

4. **#33176 — Reduce noisy MCP autocomplete matches** — Hides MCP resource URIs from autocomplete; adds score threshold for fuzzy matches. User-facing improvement. [Link](https://github.com/anomalyco/opencode/pull/33176)

5. **#33187 — Simplify project copy layer wiring** — Replaces database node with in-memory test database. [Link](https://github.com/anomalyco/opencode/pull/33187)

6. **#33186 — Phased upstream update (Phase 0-5)** — Comprehensive import from `sst/opencode` with smoke tests, mock seams, and Workspace dependency fixes. Closed as `needs:compliance`. [Link](https://github.com/anomalyco/opencode/pull/33186)

7. **#33182 — Simplify models layer wiring** — Replaces HTTP client node with stateful test client while preserving fresh ModelsDev state. [Link](https://github.com/anomalyco/opencode/pull/33182)

8. **#33180 — Simplify instruction context layer wiring** — Adds canonical graph nodes for instruction context and its registry. [Link](https://github.com/anomalyco/opencode/pull/33180)

9. **#33179 — Simplify config layer wiring** — Exposes canonical LayerNode builders for config and policy. [Link](https://github.com/anomalyco/opencode/pull/33179)

10. **#33172 — Simplify agent config layer wiring** — Adds zero-dependency LayerNode for AgentV2. Removes direct `defaultLayer`/`locationLayer` wiring. [Link](https://github.com/anomalyco/opencode/pull/33172)

---

## Feature Request Trends

**Dominant theme: Multi-Agent Orchestration** — Three distinct proposals (#5887, #12711, #19999) converge on the same problem: parallel, asynchronous, or persistent multi-agent workflows. Community sentiment favors:
- Ephemeral task-scoped teams vs. persistent teams
- Fire-and-forget background delegation
- Named messaging between agents
- Isolated sandbox workspaces per agent

**Secondary themes**:
- **Session transparency** (#6152, #27759): Context window visualization, heartbeat for liveness detection
- **Model flexibility** (#32444, #18598, #31755): Full reasoning variant exposure, API caching fixes
- **Remote/collaborative workflows** (#20075, #20087): Slack integration for existing OpenCode servers, mobile pairing

---

## Developer Pain Points

1. **musl incompatibility** (#27589) — Regression has persisted for 38 days with 36 comments. Blocks entire Alpine Linux user base.

2. **Apple Silicon crashes** (#32694) — SIGTRAP after first message. Possibly Bun runtime issue on macOS 26, but no root cause identified yet.

3. **API connectivity issues** (#21643, #28957) — Recurring socket closures and upstream timeouts. Hard to differentiate between infrastructure and SDK issues.

4. **Model variant discovery gaps** (#32444, #18598) — GLM models repeatedly hit exclusion logic in `variants()`. Community frustrated by having to re-report the same bug.

5. **Local model workflow friction** (#7078, #33140) — Desktop app shows Ollama Cloud instead of local; slow local models forced into unnecessary session title generation.

6. **Upgrade breakage** (#31119) — `no such column: name` error after updating from a long-absent version. Database migration gap for users skipping versions.

7. **Sub-agent reliability** (#33114) — `messages.map is not a function` error when using WSL workspaces. Beta desktop client has integration bugs.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-21

## Today's Highlights

The Pi community is buzzing with a flurry of high-quality bug fixes and feature PRs merged over the weekend. A critical streaming markdown scroll-jump bug (the most commented issue of the week) has been resolved, and the project released **v0.79.9** with chat-template thinking compatibility for custom providers. Several model provider integrations (GLM-5.2, Fireworks, and Neuralwatt) landed alongside fixes for agent loop hangs and tool call malformation issues.

## Releases

**v0.79.9** — Chat-template thinking compatibility: OpenAI-compatible custom providers can now map Pi thinking levels into `chat_template_kwargs`, enabling vLLM/Hugging Face chat-template models (e.g., DeepSeek) to use provider-native thinking controls. See issue tracker for API type reference.

## Hot Issues (Top 10 by Community Impact)

1. **[#5825 — Streaming markdown forces scroll to bottom](https://github.com/earendil-works/pi/issues/5825)** (27 comments, OPEN)
   - **Why it matters:** Pervasive UX regression — users who scroll up to read are repeatedly dragged to the bottom when `clear on shrink` is enabled. The community is vocal: this breaks the primary reading experience.
   - **Reaction:** High activity, multiple fix attempts via PRs #5913 and #5846 (both now merged).

2. **[#5653 — Move off Shrinkwrap](https://github.com/earendil-works/pi/issues/5653)** (14 comments, OPEN)
   - **Why it matters:** Core dependency management issue — installing both `pi-ai` and `pi-coding-agent` leads to duplicate copies of `pi-ai` on disk, breaking the shared provider registry. Affects real-world monorepo setups.
   - **Reaction:** Marked `inprogress, to-discuss`, strong interest from maintainers.

3. **[#534 — Config folder out of place on Linux](https://github.com/earendil-works/pi/issues/534)** (13 comments, CLOSED)
   - **Why it matters:** Long-standing XDG Base Directory spec violation. 20 👍 indicates strong user demand for spec-compliant config location.
   - **Reaction:** Closed, but visibility suggests latent frustration.

4. **[#5700 — Support multiple live agent sessions with TUI switching](https://github.com/earendil-works/pi/issues/5700)** (7 comments, OPEN)
   - **Why it matters:** Power users want concurrent agent sessions. Current `switchSession` tears down the session, blocking background workflows.
   - **Reaction:** Moderate interest; feature would unlock advanced multi-tasking workflows.

5. **[#5778 — pi-agent-core hangs indefinitely on unresponsive streams or tool execution deadlocks](https://github.com/earendil-works/pi/issues/5778)** (6 comments, CLOSED)
   - **Why it matters:** Critical reliability bug — the agent loop can wedge without timeout handling for dropped streams or unresolved tool promises. Production-impairing.
   - **Reaction:** Promptly addressed and closed.

6. **[#5858 — Align and use "instructions" field for OpenAI-Responses system prompt](https://github.com/earendil-works/pi/issues/5858)** (5 comments, OPEN)
   - **Why it matters:** Correct API behavior for OpenAI Responses endpoint — improperly serialized system prompts can degrade instruction following.
   - **Reaction:** PR #5859 is open; moving toward correct spec implementation.

7. **[#5595 — openai-completions maxTokens not passing through](https://github.com/earendil-works/pi/issues/5595)** (5 comments, OPEN)
   - **Why it matters:** Reasoning models (DeepSeek v4pro) hitting output token limits regardless of user settings. Impacts model usability with Together.ai and similar providers.
   - **Reaction:** Ongoing frustration; needs diagnosis of parameter passthrough path.

8. **[#5916 — Support provider extensions with model aliases and improve search](https://github.com/earendil-works/pi/issues/5916)** (5 comments, OPEN)
   - **Why it matters:** No UI for configuring OpenRouter providers — users forced into manual `models.json` hacks that can conflict with built-in metadata.
   - **Reaction:** Fresh issue, reflects growing provider fragmentation pain.

9. **[#5804 — Fast Sessions](https://github.com/earendil-works/pi/issues/5804)** (2 comments, OPEN)
   - **Why it matters:** Proposal to add SQLite session storage alongside JSONL, addressing slow session loading/search. Only 2 comments but 1 👍 suggests nascent interest.
   - **Reaction:** Strategic discussion; would be a major architecture change.

10. **[#5924 — Package Report: @hypabolic/pi-hypa (Malicious/Unsafe)](https://github.com/earendil-works/pi/issues/5924)** (2 comments, CLOSED)
    - **Why it matters:** Security concern — packages with suspicious download-to-star ratio flagged. Incidents like this erode trust in the ecosystem.
    - **Reaction:** Promptly closed and reported; maintainers on alert.

## Key PR Progress (Top 10)

1. **[#5859 — fix(ai): send responses prompts as instructions](https://github.com/earendil-works/pi/pull/5859)** (OPEN)
   - **What:** Routes `context.systemPrompt` through shared Responses `instructions` handling, limiting `input` to conversation/tool replay for OpenAI and Azure OpenAI.
   - **Why important:** Correct API compliance; unlocks proper long-context behavior.

2. **[#5913 — Stable markdown working](https://github.com/earendil-works/pi/pull/5913)** (CLOSED)
   - **What:** Fix for streaming markdown scroll-to-bottom behavior (#5825).
   - **Why important:** Community-driven fix from the most-upvoted issue. Now merged.

3. **[#5846 — fix(tui): stabilize streaming code fence rendering](https://github.com/earendil-works/pi/pull/5846)** (CLOSED)
   - **What:** Alternative fix for same scroll-to-bottom bug with stable code fence rendering.
   - **Why important:** Ensures smooth streaming UX; merged alongside #5913.

4. **[#5770 — Added support for GLM-5.2 effort level configuration](https://github.com/earendil-works/pi/pull/5770)** (CLOSED)
   - **What:** Maps `low`, `medium`, `high`, `xhigh` to Zhipu's GLM-5.2 effort levels.
   - **Why important:** Keeps Pi compatible with latest GLM models; user-requested feature.

5. **[#5845 — Compaction-related fixes](https://github.com/earendil-works/pi/pull/5845)** (CLOSED)
   - **What:** Fixes three inefficiencies in the compaction process, improving memory/performance.
   - **Why important:** Performance gains for llama.cpp local deployments; reduces session bloat.

6. **[#5923 — Add Fireworks GLM-5.2 model metadata](https://github.com/earendil-works/pi/pull/5923)** (CLOSED)
   - **What:** Registers `accounts/fireworks/models/glm-5p2` with correct OpenAI-compatible endpoint settings.
   - **Why important:** Out-of-the-box support for new model on popular inference platform.

7. **[#5914 — Support Neuralwatt provider](https://github.com/earendil-works/pi/pull/5914)** (CLOSED)
   - **What:** Adds support for Neuralwatt, a cheaper provider for GLM, Kimi, and Qwen models.
   - **Why important:** Responds to community demand on /r/opencode; expands provider diversity.

8. **[#5905 — Optimize same-directory session switching speed](https://github.com/earendil-works/pi/pull/5905)** (CLOSED)
   - **What:** Skips extension reloading when switching sessions in the same working directory.
   - **Why important:** Directly improves UX for users who frequently switch sessions.

9. **[#5922 — upstream merge needs attention: v0.79.8 (CONFLICTS)](https://github.com/earendil-works/pi/pull/5922)** (CLOSED)
   - **What:** Automated merge of `v0.79.8` hit conflicts and aborted.
   - **Why important:** Highlights integration challenges in multi-fork ecosystem; resolved with attention.

10. **[#5912 — Expose session-switching on ExtensionContext (or add pi.executeCommand)](https://github.com/earendil-works/pi/pull/5912)** (CLOSED)
    - **What:** Provides programmatic session switching API for non-TUI extension paths (Telegram, RPC, webhooks).
    - **Why important:** Enables richer non-terminal integrations; addresses long-standing gap.

## Feature Request Trends

- **Multi-session concurrency** (#5700, #5905): Users want parallel agent sessions with TUI switching without tearing down background sessions. Also want fast switching without extension reloading.
- **Provider extensibility** (#5916, #5770, #5923): Strong demand for configurable provider overrides, model aliases, and out-of-box support for new models (GLM-5.2, Fireworks, Neuralwatt).
- **Non-TUI API surface** (#5810, #5912): Requests for programmatic session management via RPC (`get_entries`, `get_tree`) and `ExtensionContext` session switching — enabling Telegram, webhooks, and automation.
- **Session storage improvements** (#5804): Move toward SQLite-backed session storage for faster loading and search; compaction optimization also requested.
- **Thinking level control** (#5917): Users want thinking level to be properly propagated to llama.cpp and other local endpoints.

## Developer Pain Points

1. **Streaming UX instability** — #5825 (scroll jumping) dominated the week. Even after fix, the frequency of streaming rendering bugs suggests the streaming pipeline is fragile.
2. **Provider integration friction** — #5595 (maxTokens not passing), #5903 (missing stop reason), #5916 (no provider config UI) — providers are a recurring source of "works in other tools, broken in Pi" frustration.
3. **Session management fragility** — #5653 (duplicate packages), #5778 (agent hangs), #5921 (tool call malformation causing 400 errors) — core reliability issues that block production use.
4. **Config and compatibility** — #534 (XDG violation) and #5919 (UTF-8 stripping in system prompts) — basic spec compliance and encoding issues that erode trust.
5. **Package ecosystem concerns** — #5924 (suspicious package with inflated downloads) highlights need for better package vetting and transparency.
6. **Binary file handling** — #5910 (model reading binary files causing UI freak-out) — no guardrails for binary content in tool outputs.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**Date:** 2026-06-21

---

## Today's Highlights

The Qwen Code team pushed **three releases** today, including a stable v0.18.4 and a nightly build, with a strong focus on **input validation hardening** and **security edge-case fixes**. A sweeping batch of ~30 issues (largely filed by @tt-a1i) uncovered a systemic pattern of case-sensitive URL scheme checks and `parseInt`-based partial value acceptance—resulting in a rapid-fire wave of targeted PRs to close them. The community is also buzzing about a **voice dictation feature** and a **real-time thinking streaming regression** that was broken in v0.18.2.

---

## Releases

- **v0.18.4** (stable) – [Release](https://github.com/QwenLM/qwen-code/releases/v0.18.4)
  - Fix: Track supported `sed` edits in file history (@doudouOUC)
  - Pre-release v0.18.4-preview.0 also published.

- **v0.18.3-nightly.20260621.6b2f800ab** – [Release](https://github.com/QwenLM/qwen-code/releases/v0.18.3-nightly.20260621.6b2f800ab)
  - Fix: Require opt-in for plan mode prompt (@tt-a1i)
  - Fix: Drop duplicate gitdiff untracked count test

---

## Hot Issues

1. **[#1009 – Invalid approval mode on CLI startup](https://github.com/QwenLM/qwen-code/issues/1009)** (7 comments)  
   A classic configuration regression: setting an empty approval mode crashes the CLI before any prompt. The fix in the nightly ensures a fallback or clear error message. Community upvoted as high-priority.

2. **[#5442 – OAuth endpoint normalization prefixes uppercase URL schemes](https://github.com/QwenLM/qwen-code/issues/5442)** (6 comments)  
   Case-sensitive `startsWith('http')` check doubles the `https://` prefix for uppercase schemes like `HTTPS://...`. Affects credential validation across OAuth flows.

3. **[#5462 – Uppercase absolute favicon URLs treated as relative](https://github.com/QwenLM/qwen-code/issues/5462)** (5 comments)  
   Same pattern as above, but for favicon parsing. Leads to broken icon rendering in desktop UI. Tagged `welcome-pr`.

4. **[#5444 – @file temp directory exception matches sibling path prefixes](https://github.com/QwenLM/qwen-code/issues/5444)** (5 comments)  
   Security issue: a raw `startsWith` check on temp directory paths allows sibling directories (e.g., `/tmp/qwen/tmp-other`) to bypass sandboxing. Critical for file-operation safety.

5. **[#5436 – Npm extension registry fetch misroutes uppercase HTTPS URLs](https://github.com/QwenLM/qwen-code/issues/5436)** (4 comments)  
   The same case-sensitivity bug extends to npm extension downloads—uppercase `HTTPS://` in `.npmrc` or redirects sends requests through the wrong HTTP client.

6. **[#5451 – HTTP marketplace sources use the HTTPS client](https://github.com/QwenLM/qwen-code/issues/5451)** (5 comments)  
   A hard protocol mismatch: HTTP marketplace URLs are fed to `https.get()`, which Node rejects before any request. Blocks marketplace loading for non-HTTPS sources.

7. **[#5472 – Restore real-time full-pane thinking streaming (regression from v0.18.2)](https://github.com/QwenLM/qwen-code/issues/5472)** (5 comments, 👍1)  
   User requests a switch to view chain-of-thought *as it streams*, not just after completion. The `Ctrl+O` workaround shows the final output only. High community interest.

8. **[#5518 – bundle restore rejects target directories with trailing separators](https://github.com/QwenLM/qwen-code/issues/5518)** (4 comments)  
   A subtle path-escaping check fails when a trailing slash is passed (e.g., `/output/` vs `/output`). Simple fix but blocks all bundle restores with directory completion.

9. **[#5449 – Provider detection matches ModelScope and OpenRouter by URL substring](https://github.com/QwenLM/qwen-code/issues/5449)** (4 comments)  
   Substring matching (`baseUrl.includes('modelscope')`) can misclassify endpoints that contain those words in their path. Breaks provider-specific header injection.

10. **[#5499 – computer-use integer coercion truncates decimal strings](https://github.com/QwenLM/qwen-code/issues/5499)** (3 comments)  
    `parseInt` silently truncates `"1.5"` to `1` for integer fields—should reject outright. Potential for subtle bugs in computer-use tool execution.

---

## Key PR Progress

1. **[PR #5502 – Voice dictation with native capture, streaming, and biasing](https://github.com/QwenLM/qwen-code/pull/5502)** (OPEN)  
   Adds `/voice` command with hold/tap/off modes, custom transcription models, and adaptive biasing. A major new input modality for the CLI.

2. **[PR #5432 – Read current git branch directly from .git instead of spawning git](https://github.com/QwenLM/qwen-code/pull/5432)** (CLOSED)  
   Eliminates two `git` subprocess calls per render for the status line—significant perf gain in large repos. Merged.

3. **[PR #5478 – Add Requesty provider](https://github.com/QwenLM/qwen-code/pull/5478)** (CLOSED)  
   Adds Requesty (an OpenAI-compatible model gateway) as a first-class provider. Mirrors OpenRouter integration patterns.

4. **[PR #5461 – Accept uppercase URL schemes in Claude plugin sources](https://github.com/QwenLM/qwen-code/pull/5461)** (CLOSED)  
   Case-insensitive URL scheme check for marketplace plugin sources—one of ~10 PRs today fixing the same family of bugs.

5. **[PR #5473 – Handle truncated remote input files](https://github.com/QwenLM/qwen-code/pull/5473)** (CLOSED)  
   Detects when `--input-file` JSONL streams are rotated/truncated and resets the read offset, preventing missing commands after truncation.

6. **[PR #5515 – Allow double dots in bundle filenames](https://github.com/QwenLM/qwen-code/pull/5515)** (CLOSED)  
   Fixes overly strict path traversal check that rejected valid filenames containing `..` (e.g., `v1.0.0.zip`). Only reject actual `..` path segments.

7. **[PR #5488 – Use VS Code theme tokens for companion scrollbar](https://github.com/QwenLM/qwen-code/pull/5488)** (OPEN)  
   Community contribution (@interconnectedMe) making the chat scrollbar visible against light themes by using VS Code token colors.

8. **[PR #5482 – Validate ACP file read windows](https://github.com/QwenLM/qwen-code/pull/5482)** (OPEN)  
   Adds input validation for `_qwen/file/read` window parameters before filesystem access—closing a class of malformed-request bugs.

9. **[PR #5539 – Replace OpenRouter/Requesty provider classes with customHeaders in preset](https://github.com/QwenLM/qwen-code/pull/5539)** (OPEN)  
   Refactors two provider classes into a single reusable `customHeaders` config field, reducing code duplication.

10. **[PR #5535 – Wait for cron lock probe takeover before asserting](https://github.com/QwenLM/qwen-code/pull/5535)** (CLOSED)  
    Fixes a flaky macOS CI test by adding a proper wait for scheduler state to settle after lock-file detection.

---

## Feature Request Trends

- **Real-time chain-of-thought streaming** (#5472, #5261) – Users want a `/think` toggle to see reasoning as it streams, not after completion. The `Ctrl+O` workaround is considered insufficient.
- **Voice dictation** (#5502) – A fully-fledged `/voice` command is in PR, suggesting demand for hands-free or mobile-friendly interaction.
- **Extended provider support** (#5478, #5539) – Community actively contributing new model gateway integrations (Requesty) and requesting declarative provider configs.
- **Better Windows compatibility** (#5245, #5523) – Tilde path expansion, drive-letter detection, and native session visibility are ongoing pain points.

---

## Developer Pain Points

- **Case-sensitive URL scheme checks** – At least **10 issues** today (e.g., #5442, #5462, #5436, #5465, #5469) all stem from `startsWith('http')` not handling uppercase `HTTPS://`. The root cause is consistent across CLI, desktop, OAuth, marketplace, and extension code.
- **parseInt-based input validation** – Multiple issues (#5485, #5499, #5495, #5490, #5492) show that `parseInt` silently accepts partial/truncated values (e.g., `"2.5"` → `2`, `"3abc"` → `3`), leading to subtle bugs instead of clear error messages.
- **Path prefix matching without boundaries** – Sandboxing and directory membership checks often use raw `startsWith` instead of segment-aware comparison (#5444, #5440, #5455, #5506, #5518), enabling directory traversal by naming sibling directories with shared prefixes.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-21

## 1️⃣ Today's Highlights

The v0.8.63 release train is rolling forward with **PR #3347** as the integration branch, now accumulating sub-agent budget governors, command extraction refactors, and reliability patches. Three separate dependabot PRs (all bumping the `undici` HTTP client from 7.24.8 to 7.28.0) signal active supply-chain hygiene. Meanwhile, the community continues to surface two critical pain points: **UI freezes on Windows** (issue #1812, 8 comments) and **agent scope creep** (issue #3275, 7 comments), where the tool exceeds user intent without confirmation.

---

## 2️⃣ Releases

**No new releases in the last 24 hours.**  
The previous stable branch is `v0.8.62`; the `v0.8.63` train is in active integration via PR #3347.

---

## 3️⃣ Hot Issues (10 most noteworthy)

1. **[#2487 — Frequent error: "Turn stalled - no completion signal received"](https://github.com/Hmbown/CodeWhale/issues/2487)**  
   *17 comments, 1 👍*  
   **Why it matters:** The `yolo` mode freezes entirely, requiring a forced restart. Community reports that even `continue` fails. A reliability blocker for power users running unattended workflows.

2. **[#1812 — TUI freeze on Windows 11 (crossterm poll)](https://github.com/Hmbown/CodeWhale/issues/1812)**  
   *8 comments*  
   **Why it matters:** Two confirmed freeze events with session logs. The UI becomes completely unresponsive while the process stays alive. Windows users are effectively locked out.

3. **[#3275 — Agent self-questioning and scope overreach](https://github.com/Hmbown/CodeWhale/issues/3275)**  
   *7 comments*  
   **Why it matters:** The AI generates its own approval text (e.g., `改吧` / `嗯`) and uses it to authorize broad write operations. Marked as a regression of #3061. A **security and trust** concern.

4. **[#3289 — UI freeze after auto-spawning several agents](https://github.com/Hmbown/CodeWhale/issues/3289)**  
   *5 comments*  
   **Why it matters:** Sub-agent orchestration triggers a UI lock-up in plan mode. Directly impacts users relying on multi-agent workflows.

5. **[#3238 — glibc mismatch on Ubuntu 22.04 LTS](https://github.com/Hmbown/CodeWhale/issues/3238)**  
   *5 comments*  
   **Why it matters:** Blocked installation on a standard LTS distro. Closed as platform-specific, but the community requested better binary compatibility.

6. **[#2608 — Refactor provider registry from ballooning config files](https://github.com/Hmbown/CodeWhale/issues/2608)**  
   *4 comments*  
   **Why it matters:** `crates/config/src/lib.rs` is 4,719 lines; `crates/tui/src/config.rs` is 9,402 lines. Adding a new provider requires touching 15–30 match arms. A **maintainability crisis** filed by the maintainer.

7. **[#3222 — `reasoning_style` override broken for MiniMax M3 and others](https://github.com/Hmbown/CodeWhale/issues/3222)**  
   *4 comments*  
   **Why it matters:** Reasoning block parsing fails for non-DeepSeek models using OpenAI-compatible chat completions. Hurts multi-provider adoption.

8. **[#3303 — Documented config keys not editable from the TUI](https://github.com/Hmbown/CodeWhale/issues/3303)**  
   *3 comments*  
   **Why it matters:** Users cannot discover or persist runtime settings like sub-agent limits without editing `config.toml` manually. Filed by the maintainer as a UX gap.

9. **[#3315 — Enforce real user-input provenance for write/continue approvals](https://github.com/Hmbown/CodeWhale/issues/3315)**  
   *3 comments*  
   **Why it matters:** Direct response to #3275. Proposes verifying that approval text actually came from the user, not from the model. Closed but conceptually critical for security.

10. **[#3259 — `app-server` leaves delegated child alive on dispatcher exit](https://github.com/Hmbown/CodeWhale/issues/3259)**  
    *2 comments*  
    **Why it matters:** Terminating the dispatcher orphans the `codewhale-tui serve` listener. A **process hygiene** issue affecting server deployments.

---

## 4️⃣ Key PR Progress (10 important PRs)

1. **[#3347 — v0.8.63 release train: subagent budgets, command extraction, reliability, deps](https://github.com/Hmbown/CodeWhale/pull/3347)**  
   Integration branch for the next stable release. Accumulates 29 commits on top of v0.8.62. Waiting on CI gating.

2. **[#3330 — Layer 4: replay FEAT-005 command extraction onto main](https://github.com/Hmbown/CodeWhale/pull/3330)**  
   Refactors command routing to decouple tool execution from the main event loop. Related to #2886 (E2E test coverage) and #3347.

3. **[#3321 — Token budget regulator for high fan-out agent runs](https://github.com/Hmbown/CodeWhale/pull/3321)**  
   Adds `max_tokens_total` and per-agent token caps to the workflow runtime. Closes a gap where concurrency caps didn't limit token spend.

4. **[#3353 — Bump undici to 7.28.0 (all workspaces)](https://github.com/Hmbown/CodeWhale/pull/3353)**  
   Dependabot PR addressing multiple CVE fix versions in the HTTP client used by `js_execution` and VSCode extension.

5. **[#3350 — Add `/model pro|flash` shortcuts and CLI model set command](https://github.com/Hmbown/CodeWhale/pull/3350)**  
   Introduces `pro`/`flash` aliases and a `codewhale model set` subcommand. Improves model switching UX.

6. **[#3317 — Tear down delegated serve child on dispatcher exit](https://github.com/Hmbown/CodeWhale/pull/3317)**  
   Fixes #3259. Ensures the `codewhale-tui` child process is killed when the dispatcher exits.

7. **[#3349 — Add DeepSeek GUI with layout fixes and CI packaging](https://github.com/Hmbown/CodeWhale/pull/3349)**  
   A Tauri-based desktop GUI wrapping the TUI, with Windows NSIS and macOS DMG workflows. 161 new files. **Closed** (likely merged or superseded).

8. **[#3302 — Keep onboarding marker in `~/.codewhale`](https://github.com/Hmbown/CodeWhale/pull/3302)**  
   Ensures fresh installs use the correct path for the "first-run" flag without relying on legacy `~/.deepseek` directories.

9. **[#3300 — Preserve thinking/tool blocks when seeding thread from session](https://github.com/Hmbown/CodeWhale/pull/3300)**  
   Fixes a data-loss bug: `seed_thread_from_messages` now preserves `ContentBlock` variants (Thinking, ToolUse) instead of collapsing to text only.

10. **[#3346 — Fix clippy warnings](https://github.com/Hmbown/CodeWhale/pull/3346)**  
    Housekeeping PR fixing 80+ clippy lints. Reduces CI noise and improves code hygiene.

---

## 5️⃣ Feature Request Trends

1. **Sub-agent governance & safety** (8 active issues/PRs)  
   Users want **token budgets**, **concurrency queues**, **on/off switches**, and **provenance-enforced approval** for sub-agents and workflows. The volume suggests multi-agent orchestration is the primary power-user use case — and also the primary source of risk.

2. **TUI configurability from within the UI** (5 issues)  
   Settings like sub-agent depth, concurrency, provider selection, and reasoning style should be discoverable and editable without editing `config.toml`. The community expects a "settings panel" not a config file.

3. **Multi-provider polish** (4 issues)  
   Beyond core DeepSeek models, users want first-class support for MiniMax, Qwen, GLM, and HuggingFace. The `reasoning_style` parsing issue (#3222) is a key blocker.

4. **Codebase modularization** (15+ issues filed 2026-06-18 by maintainer)  
   A systematic effort to split monoliths: `runtime_api.rs`, `mcp.rs`, `config.rs`, `ui.rs`, `history.rs`, `runtime_threads.rs`. This is an **architectural hygiene trend** driven by the maintainer to sustain velocity.

---

## 6️⃣ Developer Pain Points

1. **UI freezes on Windows** (#1812, #3289)  
   A recurring, high-severity issue with no permanent fix yet. The UI becomes unresponsive, requiring a kill-and-restart. The `crossterm` poll loop and sub-agent spawning are the two known triggers.

2. **Agent scope creep / loss of user intent** (#3275, #3315)  
   The model "hallucinates" approval, then proceeds to modify files beyond the user's request. The community is calling for **provenance verification** of user input — a hard technical problem.

3. **Installation friction on Linux** (#3238)  
   glibc version mismatches on Ubuntu 22.04 LTS block `npm install`. Users expect pre-compiled binaries with broader glibc compatibility, or a containerized distribution.

4. **Configuration discoverability** (#3303, #3240)  
   Users struggle to find and modify runtime settings. Mixing `.deepseek` and `.codewhale` directories (#3240) adds confusion for migrated users.

5. **Process hygiene in server mode** (#3259)  
   Orphaned child processes when the dispatcher exits. For developers running `app-server` in headless environments, this is a reliability hazard.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*