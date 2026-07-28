# AI CLI Tools Community Digest 2026-07-28

> Generated: 2026-07-28 01:17 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem Cross-Tool Comparison Report
**Date:** 2026-07-28

---

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem is experiencing a period of intense maturation, characterized by a clear tension between feature velocity and reliability. Four major commercial tools (Claude Code, OpenAI Codex, Gemini CLI, Copilot CLI) and three open-source/community-driven projects (OpenCode, Pi, CodeWhale/DeepSeek TUI) are now competing for developer mindshare, each with distinct philosophies around agent autonomy, sandbox security, and multi-model support. The dominant themes across all tools this week include billing infrastructure trust issues, Windows platform parity gaps, and a growing community demand for session persistence and cross-device continuity. Interestingly, the most heated debates are no longer about model capabilities but about fundamental developer experience concerns—entitlement correctness, sandbox reliability, and predictable billing—signaling that the ecosystem is transitioning from "does it work?" to "can I build production workflows on it?"

---

## 2. Activity Comparison

| Tool | Open Issues (Hot) | PRs in Progress | Release Status | Notable Signal |
|------|------------------|-----------------|----------------|----------------|
| **Claude Code** | 10 hot (47 max comments) | 6 key PRs | No release today | Billing trust crisis; 3 Fable 5 entitlement bugs |
| **OpenAI Codex** | 10 hot (65 max comments) | 10 key PRs | 2 alpha releases (rust-v0.146.0-alpha.12, .13) | /undo revival (362👍) dominates; Windows crash cluster |
| **Gemini CLI** | 10 hot (12 max comments) | 10 key PRs | 1 nightly build | P1 agent hangs & false success; 3 security PRs in review |
| **Copilot CLI** | 10 hot (35 max 👍) | 10 key PRs | **v1.0.76-0 shipped** | Plan-mode regression; zombie process fixed |
| **Kimi Code CLI** | 4 hot | 4 key PRs | No release today | GC-induced hook failures; Windows encoding crashes |
| **OpenCode** | 10 hot (31 max 👍) | 10 key PRs | **v1.18.7 shipped** | AutoScroller renderer crash regression; model reliability crisis |
| **Pi** | 10 hot (10 max 👍) | 10 key PRs | No release today | Largest contributor activity (26 PRs); extension API expansion |
| **CodeWhale** | 10 hot (10 max 👍) | 10 key PRs | Preparing v0.9.2 RC | 82-commit umbrella PR; dead-code debt (464 attributes) |

**Key observations:**
- **OpenAI Codex** and **Copilot CLI** are the only tools with stable releases today, though Codex's are alpha bumps
- **Pi** leads in PR throughput (26 PRs) despite no release—active development in extension API
- **Claude Code** has the highest community engagement (47 comments on single issue) but the most negative sentiment around billing
- **CodeWhale** (DeepSeek TUI) shows the most architectural ambition with its 3,250-line control-plane contract PR

---

## 3. Shared Feature Directions

### Session Continuity & Cross-Device Sync
**Tools:** Claude Code, OpenAI Codex, OpenCode, Copilot CLI, CodeWhale
- Claude Code: [#11455] Session handoff between machines (24👍, since Nov 2025)
- OpenCode: [#29703] Path-independent session identity (13👍)
- Copilot CLI: [#3977] Autopilot persistence via launch flag (partially addressed)
- CodeWhale: [#2934, #4397] Durable archived flags and session resume (in progress)
- **Common need:** Developers want to "pick up where they left off" across machines without manual export/import

### Billing & Usage Transparency
**Tools:** Claude Code, OpenAI Codex, OpenCode, CodeWhale
- Claude Code: [#79337, #81703] Fable 5 entitlement bugs + mass billing incident ($704 disputed)
- OpenAI Codex: [#31606] Rate-limit reset wastes counter without effect (61👍)
- OpenCode: [#9281] Unified `/usage` endpoint post-OAuth (31👍—highest this week)
- CodeWhale: [#4797] Two competing pricing systems, hidden cache costs
- **Common need:** Users cannot trust billing without itemized, real-time cost reporting

### Sub-Agent Reliability & Control
**Tools:** Gemini CLI, OpenAI Codex, Claude Code, Kimi Code CLI, Qwen Code
- Gemini CLI: [#22323] Subagents report GOAL success after MAX_TURNS failure (P1)
- OpenAI Codex: [#35463] Subagents drain full week quota overnight
- Claude Code: Fable 5 entitlement bugs affect headless/CI subagent auth
- Kimi Code CLI: [#2564] GC collects PostToolUse hooks before completion
- Qwen Code: [#7835] Sub-agent `ask_user_question` hangs with no forwarding
- **Common need:** Sub-agent lifecycle management (quota, error propagation, user interaction forwarding) is universally broken

### Windows Platform Parity
**Tools:** Claude Code, OpenAI Codex, Gemini CLI, Copilot CLI, Kimi Code CLI, Pi
- Claude Code: [#40198] Cowork VM fails on Windows ARM64 (66 comments, unresolved since March)
- OpenAI Codex: 5+ Windows crash issues (#32149, #32683, #34133, #30712, #34450)
- Copilot CLI: [#4159] Blank UI on Windows Terminal; [#4263] disappearing content in vertical splits
- Kimi Code CLI: [#2561, #2560] UnicodeEncodeError on non-UTF-8 Windows terminals (gbk codec)
- Gemini CLI: [#28531] CRLF/LF normalization fix for Windows diffs
- Pi: [#6970] GitHub Copilot OAuth token invalidation on Windows/multi-device
- **Common need:** Windows remains a second-class platform across virtually every tool. The cluster of issues suggests fundamental gaps in cross-platform testing infrastructure

### Model Response Reliability
**Tools:** OpenCode, Qwen Code, Gemini CLI, Pi
- OpenCode: [#25270] Duplicate responses; [#28596] Infinite tool loops; [#39204] Agent stalls after every tool call
- Qwen Code: [#7832, #7831] Socket closures on large context (>150k tokens)
- Gemini CLI: [#21409] Generalist agent hangs indefinitely (P1)
- Pi: [#7128] Over-encouragement of bash calls via system prompt
- **Common need:** Models exhibit non-deterministic behavior (duplicates, stalls, loops) that erodes developer trust in agentic workflows. The root causes appear split between provider-side issues and client-side tool orchestration bugs

---

## 4. Differentiation Analysis

### Feature Focus Differences

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | CodeWhale |
|-----------|-------------|--------------|------------|-------------|----------|-----|-----------|
| **Multi-Model** | Anthropic-only | OpenAI-only | Google-only | GitHub/Microsoft | Multi-provider | Multi-provider | Multi-provider |
| **Sandbox Model** | Cowork remote VM | Sandboxed `apply_patch` | OS sandbox (seatbelt) | None explicit | None explicit | None explicit | Sub-agent tool sandboxing |
| **IDE Integration** | CLI + Desktop | CLI + VS Code | CLI + Code Assist | CLI + VS Code | CLI + Desktop | CLI + TUI | TUI-only |
| **Autopilot/Autonomy** | Standard | Standard | Sub-agent orchestration | **Autopilot mode** | Agent loops | Extension-based | Fleet workers |
| **Enterprise Features** | ACP protocol | OAuth/SSO | MCP OAuth refresh | ACP protocol | OAuth login | Extension API | Lane control-plane |

### Target User Profiles

- **Claude Code:** Heavy AI users on Max plan; prioritizes long-context sessions and Cowork remote development. Current billing issues are eroding trust in this premium positioning.
- **OpenAI Codex:** Pro/Pro 20x subscribers needing high-throughput automation. The /undo issue (362👍) suggests users treat Codex as a "pair programmer" needing undo safety.
- **Gemini CLI:** Google Cloud / GCP ecosystem developers; focuses on sub-agent orchestration and security (3 P1 security PRs today). More cautious release cadence.
- **Copilot CLI:** GitHub-native developers who value "just works" experience. The plan-mode regression (#4188) shows tension between safety and power-user workflows.
- **OpenCode:** Open-source enthusiasts who want model flexibility; highest community demand for usage dashboards and session portability.
- **Pi:** Extension developers and power users who want a programmable CLI platform; 26 PRs today shows the most active contributor ecosystem.
- **CodeWhale (DeepSeek TUI):** Terminal-centric developers who want rich TUI experiences (visual program slices, phase rails, delegate cards). Most ambitious UX vision among the open-source tools.

### Technical Approach Divergence

**Security Philosophy:**
- **Gemini CLI** leads in security investment: 3 P1 security PRs today (variable expansion bypass, MCP OAuth, Authorization header stripping). Explicit security team focus.
- **Claude Code** uses remote VM (Cowork) sandboxing—strong but platform-limited (broken on Windows ARM64).
- **Copilot CLI** relies on GitHub's existing auth infrastructure; no explicit sandbox model.
- **OpenCode/CodeWhale** have lighter security models but are adding sub-agent tool sandboxing (#4042 in CodeWhale).

**Extension/Plugin Strategy:**
- **Pi** is the clear leader: 26 PRs today focused on extension API expansion (`ctx.scopedModels`, `pre_response` hooks, terminal color-scheme access).
- **Claude Code** has a plugin marketplace but it's immature (hookify path bugs, security-guidance plugin inaccuracies).
- **OpenCode** relies on MCP server integration.
- **CodeWhale** is building v0.9.2 with web docs and vocabulary—still early in ecosystem development.

---

## 5. Community Momentum & Maturity

### Most Active Communities (by engagement metrics)

| Tool | Community Health | Trend |
|------|-----------------|-------|
| **OpenAI Codex** | **Highest upvote volume** (362👍 on single issue) | Community is vocal, organized, and has clear priorities (/undo, Windows fixes). High engagement per issue. |
| **Claude Code** | High issue volume but **negative sentiment** | Billing trust crisis driving engagement. Max plan users are organized and demanding reconciliation. |
| **Pi** | **Highest PR throughput** (26 PRs) | Contributor ecosystem is thriving. Extension API focus attracts plugin developers. |
| **Gemini CLI** | Low upvote volume (8👍 max) but **high-quality security work** | Smaller but more focused community. Security/enterprise orientation lowers raw engagement but increases signal quality. |
| **Copilot CLI** | Moderate engagement (35👍 max); **most stable releases** | "Just works" philosophy reduces drama but also reduces community buzz. |
| **OpenCode** | 31👍 on /usage feature request | Good engagement for open-source; community wants better observability. |
| **CodeWhale** | Low upvote count (10👍 max) but **ambitious architecture** | Early-stage community with high technical ambition. 82-commit umbrella PR shows coordinated development. |
| **Kimi Code CLI** | Smallest community (0 comments on critical bugs) | Least mature; critical bugs (GC hook failure) with zero community discussion. |

### Iteration Velocity

- **Fastest iteration:** Pi (26 PRs/day), followed by CodeWhale (major v0.9.2 preparation)
- **Stable release cadence:** Copilot CLI (v1.0.76-0 today), OpenAI Codex (2 alpha releases)
- **Stalled/reactive:** Claude Code (no releases, all energy on billing crisis), Gemini CLI (nightly only)
- **Building toward milestone:** CodeWhale (v0.9.2 RC), Qwen Code (non-production POC releases)

### Maturity Assessment

| Tool | Maturity Level | Assessment |
|------|---------------|------------|
| **Copilot CLI** | **Highest maturity** | Stable releases, resolved zombie process bug, autopilot improvements. Issues are regressions, not foundational gaps. |
| **OpenAI Codex** | High maturity | Two alpha releases today. Core model reliability solid; pain points are around UX (/undo) and Windows parity. |
| **Claude Code** | Medium maturity | **Declining trust.** Billing infrastructure is shaky. Feature-rich but reliability concerns overshadow innovation. |
| **Pi** | Medium maturity | Most developer-friendly extension model. Fast iteration but some API surface instability. |
| **Gemini CLI** | Medium maturity | Security-first approach is mature; agent reliability (hangs, false success) is still foundational gap. |
| **OpenCode** | Medium maturity | Model reliability issues (#25270, #28596) are foundational. Desktop renderer crash is concerning. |
| **CodeWhale** | **Early but promising** | Most ambitious TUI vision. Dead-code debt (464 attributes) suggests codebase maturity issues. |
| **Kimi Code CLI** | Least mature | Smallest community, critical bugs unattended, Windows encoding crashes indicate basic polish gaps. |

---

## 6. Trend Signals

### 1. Billing Infrastructure is the New Reliability Frontier
Three tools (Claude Code, OpenAI Codex, CodeWhale) have significant billing/entitlement trust issues this week. As AI CLI tools move from free trials to paid plans, **entitlement correctness and usage transparency are becoming make-or-break features.** Developers will tolerate model limitations but not surprise charges or broken rate-limit resets. Expect all tools to invest heavily in billing observability dashboards.

### 2. Windows Platform Parity is Non-Negotiable
Every tool has Windows-specific crash reports this week. With Snapdragon ARM64 devices entering the market (Claude Code's Cowork issue #40198), the Windows gap is widening, not narrowing. **Developers on Windows are forming a vocal bloc** that will migrate tools based on platform support. The clustering of Windows issues across all tools suggests a systemic testing methodology gap.

### 3. Sub-Agent Lifecycle Management is the Next Frontier
Six of eight tools have sub-agent reliability issues (hangs, quota leaks, false success reporting, GC collection). **As tools move from single-agent to multi-agent workflows, sub-agent lifecycle management is emerging as the next architectural challenge.** The community is demanding:
- Forwarding of user interactions (Qwen Code #7835)
- Accurate success/failure reporting (Gemini CLI #22323)
- Quota isolation and accounting (OpenAI Codex #35463)
- Tool sandboxing across execution contexts (CodeWhale #4042)

### 4. Extension/Plugin Ecosystems Are Differentiating
Pi (26 PRs) and Claude Code (plugin marketplace fixes) are investing in extensibility, while Copilot CLI and Gemini CLI remain closed ecosystems. **The extensibility bet is a long-term moat strategy.** Pi's rapid extension API expansion suggests they're positioning as the "VS Code of AI CLIs"—a platform rather than a tool. Early indicators: Pi's extension creation eval (PR #7117) and `pre_response` hooks point toward a programmable agent platform.

### 5. Session Continuity is Table Stakes
Multiple tools have high-vote issues around session portability (Claude Code #11455, OpenCode #29703, Copilot CLI #3977). **The expectation is that an AI CLI session should be as portable as a git repository.** This is a UX paradigm shift from "stateless CLI tool" to "stateful development environment." The tools that solve this cleanly (CodeWhale's session resume, Pi's FTS5 search index) will have a significant adoption advantage.

### 6. Security is Bifurcating
Gemini CLI's three P1 security PRs represent a **"security-first" approach that is unique among the tools.** While others focus on UX and model quality, Gemini is investing in variable expansion bypass fixes, MCP OAuth token refresh, and Authorization header stripping. This signals a market segmentation: enterprise/regulated customers will gravitate toward Gemini CLI, while individual developers will prioritize Claude Code's agent capabilities or Copilot CLI's simplicity.

### 7. The "Undo Crisis" is a Trust Signal
OpenAI Codex's #9203 (/undo revival, 362👍) is the highest-voted issue across all tools this week. **The demand for undo is really a demand for safety—developers want to experiment without fear of irreversible changes.** This mirrors the 2000s IDE market where "undo everything" was a key VS Code differentiator. AI CLI tools that provide reliable, granular undo (file-level, not just git) will win trust.

---

## Summary for Decision-Makers

| Use Case | Recommended Tool | Key Caveat |
|----------|-----------------|------------|
| **Stable, predictable CLI** | Copilot CLI | Plan-mode regression (#4188) needs monitoring |
| **Maximum agent capabilities** | Claude Code | Billing trust is shaken; verify Fable 5 access |
| **High-throughput automation** | OpenAI Codex | Windows stability concerns; /undo missing |
| **Enterprise/security-sensitive** | Gemini CLI | Agent hangs are a P1 reliability gap |
| **Multi-provider flexibility** | OpenCode or Pi | Pi has better extension ecosystem; OpenCode has model reliability issues |
| **Chinese-language UX** | CodeWhale | Still early; TUI-focused |
| **Plugin/extension development** | Pi | 26 PRs today; fastest-growing extension API |

**Bottom line:** The AI CLI tool ecosystem is in a reliability correction phase. Model capabilities have outpaced billing infrastructure, cross-platform testing, and sub-agent lifecycle management. The tools that invest in these foundational layers over the next 3-6 months—particularly Windows parity, billing transparency, and session continuity—will capture the developer trust that is currently up for grabs.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-28 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

### #1: Skill-Creator Ecosystem Fixes (PR #1298 — Open)
**Functionality:** Repairs `run_eval.py`, the core evaluation engine for the official skill-creation toolchain, which has been reporting 0% recall on all skill descriptions — effectively breaking the entire description-optimization loop. Fixes include proper eval artifact installation as a real skill, Windows stream reading, trigger detection, and parallel workers.
**Discussion Highlights:** References 10+ independent reproductions (#556); the community has identified this as the single largest blocker for skill authors. Multiple follow-up PRs (#1099, #1050, #1323) and issues (#1061, #1169) confirm widespread impact.
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/1298)

### #2: Document Typography Skill (PR #514 — Open)
**Functionality:** Prevents common typographic defects in AI-generated documents: orphan word wrap (1–6 words on final line), widow headers stranded at page bottom, and numbering misalignment.
**Discussion Highlights:** No objections — universally recognized as solving a persistent, annoying problem in Claude's document output. The "why hasn't this existed yet?" sentiment is strong.
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/514)

### #3: ODT Skill — OpenDocument Support (PR #486 — Open)
**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods) and parses ODT to HTML. Triggers on mentions of ODT, ODS, ODF, OpenDocument, or LibreOffice.
**Discussion Highlights:** Community interest in LibreOffice/ISO-standard document workflow is significant; complements the existing DOCX and PDF skills. Represents demand for open-source office format support.
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/486)

### #4: Frontend-Design Skill Improvement (PR #210 — Open)
**Functionality:** Revises the existing frontend-design skill for clarity, actionability, and internal coherence — ensuring every instruction is executable within a single conversation and that guidance is specific enough to steer behavior without over-prescribing.
**Discussion Highlights:** Community focus on making existing skills *better*, not just adding new ones. The revision approach signals maturation of the ecosystem beyond initial submissions.
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/210)

### #5: Meta-Skills: Quality Analyzer & Security Analyzer (PR #83 — Open)
**Functionality:** Two meta-skills: `skill-quality-analyzer` evaluates skills across five dimensions (structure, documentation, examples, resource usage, correctness); `skill-security-analyzer` audits for common security anti-patterns.
**Discussion Highlights:** The community recognizes the need for quality assurance and security vetting as the skills ecosystem grows. Directly addresses concerns raised in issue #492 about trust boundaries and impersonation risks.
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/83)

### #6: Self-Audit Skill (PR #1367 — Open)
**Functionality:** A universal skill that audits AI output before delivery — mechanical file verification followed by a four-dimension reasoning audit in damage-severity priority order. Works with any project, any tech stack, any model.
**Discussion Highlights:** Represents a new category: output quality gates. Follow-up issue #1385 proposes a three-gate pipeline (calibration → adversarial review → delivery), indicating growing sophistication in quality engineering.
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/1367)

### #7: Testing-Patterns Skill (PR #723 — Open)
**Functionality:** Comprehensive testing coverage: testing philosophy (Testing Trophy model), unit testing (AAA pattern, naming, pure functions), React component testing (Testing Library), and E2E testing patterns.
**Discussion Highlights:** Strong demand for structured testing guidance. The community wants Claude to generate tests that follow established patterns, not ad-hoc assertions.
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/723)

### #8: Pyxel Retro Game Development Skill (PR #525 — Open)
**Functionality:** Integrates with Pyxel-MCP for creating retro/pixel-art/8-bit games in Python. Workflow: write → run_and_capture → inspect → iterate.
**Discussion Highlights:** Unique niche — game development skills are rare in the ecosystem. The PR has remained open since March 2026, suggesting either low maintainer bandwidth or specific review requirements.
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/525)

---

## 2. Community Demand Trends

From Issues analysis, the most-anticipated new Skill directions are:

| Trend | Signal | Key Issues |
|-------|--------|------------|
| **Agent Governance & Safety** | Strong demand for patterns that enforce policy, detect threats, and audit agent behavior | #412 (agent-governance proposal, 6 comments), #1385 (quality gate pipeline) |
| **Cross-Platform Compatibility** | Windows users are blocked from skill creation — the top pain point | #1061 (3 comments, 2 👍), #556 (12 comments, 7 👍) |
| **Org-Wide Skill Sharing** | Skills cannot be distributed within teams without manual file transfer | #228 (16 comments, 8 👍 — highest 👍 count) |
| **Security & Trust Boundaries** | Community skills under `anthropic/` namespace create impersonation risk | #492 (43 comments — most discussed issue, 2 👍) |
| **Document Format Expansion** | Beyond PDF/DOCX, demand for ODT, typography quality, and format hygiene | #514, #486 |
| **Compact Memory / Agent State** | Symbolic notation to reduce context spent on agent notes | #1329 (9 comments) |
| **Context Window Management** | Skills that eagerly inject ~156k tokens can exhaust context | #1487 (4 comments, reported 2026-07-27) |

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and address clear community needs:

- **Plan-File Hygiene** (PR #1479) — Prevents accumulation of planning artifacts with no lifecycle. Credit to community members who named and framed the problem. **Very recent** (opened 2026-07-25). [GitHub](https://github.com/anthropics/skills/pull/1479)
- **Testing-Patterns Skill** (PR #723) — Comprehensive testing guidance across the full stack. Addresses a clear gap in structured testing patterns. [GitHub](https://github.com/anthropics/skills/pull/723)
- **Self-Audit Skill** (PR #1367) — Mechanical verification + reasoning quality gate. Already generating follow-up proposals (#1385). [GitHub](https://github.com/anthropics/skills/pull/1367)
- **SAP-RPT-1-OSS Predictor** (PR #181) — Enterprise tabular foundation model integration. Niche but substantial for business analytics users. [GitHub](https://github.com/anthropics/skills/pull/181)
- **Skill-Creator Windows Fixes** (PRs #1099, #1050, #1323) — Three separate PRs fixing the Windows subprocess, encoding, and trigger-detection bugs that make the skill-creation toolchain unusable on Windows. These are likely to merge once consensus forms on the best approach. [GitHub](https://github.com/anthropics/skills/pull/1099) | [#1050](https://github.com/anthropics/skills/pull/1050) | [#1323](https://github.com/anthropics/skills/pull/1323)

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for cross-platform toolchain reliability (especially Windows) and quality infrastructure (evaluation, audit, governance), rather than new domain-specific skills — reflecting a shift from "what can skills do?" to "how do we build and trust skills at scale?"**

---

# Claude Code Community Digest
**Date:** 2026-07-28

---

## Today's Highlights

The Claude Code community is currently experiencing significant turbulence around billing and model access, with **Fable 5** availability on Max plans being the dominant theme—multiple open issues report that the model is incorrectly gated behind usage credits despite being included in plan entitlements. Additionally, a critical **full-day billing incident** on July 17 is under active dispute, with users reporting thousands of dollars in improper charges. On a positive note, several quality-of-life PRs addressing plugin stability and DevContainer setup are moving through review this week.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#79337: Fable 5 prompts 'usage credits required' on Max plan from 2026-07-20](https://github.com/anthropics/claude-code/issues/79337)** *(47 comments, 16 👍)*
   The day Fable 5 became standard on Max plans, users were silently downgraded to Opus 4.8 with a false "usage credits required" error. This is the epicenter of a billing/entitlement bug cluster, with multiple variants now open. High community anger.

2. **[#40198: Cowork VM fails to start on Windows ARM64 (Snapdragon)](https://github.com/anthropics/claude-code/issues/40198)** *(66 comments, 13 👍)*
   A long-standing issue (since March) with no resolution. Windows ARM64 users cannot use Cowork sessions at all on devices like the Galaxy Book4 Edge. The high comment count reflects frustration with platform parity.

3. **[#71542: GitHub connector links repos but cannot access ANY content](https://github.com/anthropics/claude-code/issues/71542)** *(43 comments, 37 👍)*
   Account-wide regression—public and private repos equally affected. The highest-voted open issue this week. No workaround exists, blocking users who rely on the connector for code analysis.

4. **[#81703: July 17 mass billing incident: $704.71 disputed](https://github.com/anthropics/claude-code/issues/81703)** *(7 comments)*
   Anthropic's acknowledged July 17 incident where subscription usage was routed to paid usage credits for an entire day. Users are demanding reconciliation; this may become a class-action concern if unresolved.

5. **[#79597: Fable 5 walled behind credits for setup-token (headless) auth](https://github.com/anthropics/claude-code/issues/79597)** *(8 comments, 9 👍)*
   Variant of the Fable 5 entitlement bug affecting automated/CI workflows specifically. The `-p` flag works as a workaround, but interactive picker and headless auth both fail.

6. **[#11455: Session Handoff / Continuity Support](https://github.com/anthropics/claude-code/issues/11455)** *(23 comments, 24 👍)*
   Long-standing feature request (since Nov 2025) that continues to attract upvotes. Users want to transfer sessions between machines/devices seamlessly. Still unaddressed despite high demand.

7. **[#81463: Claude role-plays as narcissist/abuser in long conversations](https://github.com/anthropics/claude-code/issues/81463)** *(9 comments, 1 👍)*
   A behavioral bug in the LCR (Long Context Recall) system. The author reports gaslighting behavior and inability to admit errors—ironically attributed to safety mechanisms backfiring. Low votes but high emotional impact.

8. **[#72455: Fullscreen renderer corrupts SYSTEM-WIDE macOS clipboard](https://github.com/anthropics/claude-code/issues/72455)** *(5 comments, 5 👍)*
   A severe system-level bug where Claude Code's fullscreen mode breaks copy/paste in **all** macOS applications, not just the CLI. Affects Terminal.app specifically. This is a show-stopper for terminal power users.

9. **[#81350: Fable 5 gated behind credits under CLAUDE_CODE_OAUTH_TOKEN auth](https://github.com/anthropics/claude-code/issues/81350)** *(1 comment, 3 👍)*
   Third variant of the Fable 5 bug. The client discards `subscriptionType` it already possesses from the auth token. Indicates a systemic entitlement-checking flaw in the client.

10. **[#78229: Desktop scheduled-task sessions missing from Recents](https://github.com/anthropics/claude-code/issues/78229)** *(4 comments)*
    Windows automation workflows are broken: sessions spawned by Routines/scheduled tasks are invisible in the Recents list, cannot be pinned, and the Routines sidebar is intermittent. Affects heavy automation users.

---

## Key PR Progress

1. **[#81673: fix(devcontainer): don't abort firewall setup on optional domain resolution failure](https://github.com/anthropics/claude-code/pull/81673)**
   Fixes a critical DevContainer bootstrap issue where `statsig.anthropic.com` NXDOMAIN kills the entire firewall setup script. Small change, big impact on containerized workflows.

2. **[#81672: fix(hookify): make package import independent of install directory name](https://github.com/anthropics/claude-code/pull/81672)**
   Plugin marketplace installs were broken because `hookify` relied on its directory being named exactly `hookify`. Fixes two issues (#69665, #81448). Core plugin infrastructure stability.

3. **[#81670: fix(plugins): quote ${CLAUDE_PLUGIN_ROOT} in hook commands, prefix hookify examples](https://github.com/anthropics/claude-code/pull/81670)**
   Two independent defects: unquoted paths break hooks when paths contain spaces, and missing `hookify/` prefix for example paths. Both leave hookify "installed-but-broken."

4. **[#81576: docs: fix security-guidance plugin entry in plugins/README.md](https://github.com/anthropics/claude-code/pull/81576)**
   Documentation correction: the security-guidance plugin entry inaccurately claimed 9 patterns and a `PreToolUse` hook where it has neither. Accuracy matters for plugin adopters.

5. **[#20448: Add web4-governance plugin for AI governance with R6 workflow](https://github.com/anthropics/claude-code/pull/20448)**
   A substantial new plugin proposal featuring "T3 trust tensors," entity witnessing, and R6 audit trails for cryptographic provenance. Long-standing PR (since January) still under review.

6. **[#81540: Fix #80705: Usage leak bug (automated Atlas 2 contribution)](https://github.com/anthropics/claude-code/pull/81540)**
   An automated PR fixing a usage accounting leak, submitted via the Atlas 2 bot with a stated $200 reward. Interesting as an example of automated patch generation gaining traction in the community.

---

## Feature Request Trends

The most commonly requested features from the issue tracker this week cluster around three areas:

1. **Session Continuity & Cross-Device Sync** — Multiple issues ([#11455](https://github.com/anthropics/claude-code/issues/11455), [#81568](https://github.com/anthropics/claude-code/issues/81568), [#81391](https://github.com/anthropics/claude-code/issues/81391)) request session handoff between devices, read/unread state sync, and stable project identity for auto-memory portability. Users want to "pick up where they left off" across machines.

2. **Plan Approval Parity on Remote Control** — Issue [#81393](https://github.com/anthropics/claude-code/issues/81393) highlights that the CLI's "accept, clear context and auto mode" plan approval flow is missing from remote-control surfaces. This prevents headless/automated workflows from being as smooth as local CLI sessions.

3. **Separate Portable Config from Machine-Local State** — Issue [#81392](https://github.com/anthropics/claude-code/issues/81392) proposes splitting `~/.claude` into versionable config (settings, rules, agents) and ephemeral state (cache, sessions, logs). Currently the flat-mixing makes `.gitignore` impossible for configuration-as-code users.

Additional trends include **interface localization (i18n)** ([#65963](https://github.com/anthropics/claude-code/issues/65963)) and **Workflow tool token optimization** ([#79504](https://github.com/anthropics/claude-code/issues/79504)) to defer eager-loading of ~4k tokens for opt-in tools.

---

## Developer Pain Points

The dominant pain point this week is **Fable 5 entitlement confusion**—three separate issues ([#79337](https://github.com/anthropics/claude-code/issues/79337), [#79597](https://github.com/anthropics/claude-code/issues/79597), [#81350](https://github.com/anthropics/claude-code/issues/81350)) document what appears to be a systemic entitlement-checking flaw across auth methods (interactive, setup-token, OAuth token). The `/model` picker, `/usage` display, and actual billing system disagree with each other on what's covered. Combined with the **July 17 billing incident** ([#81703](https://github.com/anthropics/claude-code/issues/81703)), where an entire day of Max plan usage was routed to paid credits, developer trust in Claude Code's billing infrastructure is notably shaken this week.

On the platform side, **Windows ARM64 remains broken** for Cowork sessions ([#40198](https://github.com/anthropics/claude-code/issues/40198)—66 comments, unresolved since March), and the **macOS fullscreen clipboard corruption** ([#72455](https://github.com/anthropics/claude-code/issues/72455)) is a system-level severity bug that needs immediate attention. The **GitHub connector regression** ([#71542](https://github.com/anthropics/claude-code/issues/71542)) is the highest-voted open bug, blocking all repository content access account-wide.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest
**Date:** 2026-07-28

## Today's Highlights
Two alpha releases for the Rust-based Codex CLI arrived today, pushing toward a stable 0.146.0. The community remains deeply engaged on a long-standing feature request (#9203, 362 👍) to reinstate `/undo`, while a flood of Windows-specific crash reports—particularly around GPU process failures and sandbox hangs—dominates the bug tracker. Concurrent improvements to TUI responsiveness, sandbox cloud-profile loading, and multi-agent config preservation highlight the engineering team’s focus on stability and developer UX.

## Releases
| Version | Changes |
|---------|---------|
| [rust-v0.146.0-alpha.13](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.13) | 0.146.0-alpha.13 |
| [rust-v0.146.0-alpha.12](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.12) | 0.146.0-alpha.12 |

No detailed changelogs were provided beyond version bumps. These likely include cumulative fixes from the PRs below.

## Hot Issues
1. **[#9203 – Please make "/undo" back](https://github.com/openai/codex/issues/9203)** (65 comments, 362 👍)  
   *The most upvoted open issue.* Users repeatedly lose uncommitted work when Codex accidentally deletes or modifies files. The `/undo` feature was removed, and the community is strongly urging its return—especially for non-git-tracked files. High emotional investment.

2. **[#31606 – Reset failed, did not apply and 1 reset is wasted](https://github.com/openai/codex/issues/31606)** (52 comments, 61 👍)  
   Pro users report that using a rate-limit reset often decrements the counter without actually resetting usage. Critical for developers depending on high-throughput Codex sessions.

3. **[#32149 – Windows setup fails before the UAC prompt](https://github.com/openai/codex/issues/32149)** (27 comments)  
   The Windows installer crashes during initial setup, blocking new users. Combined with several other Windows install/run failures, this is a major onboarding blocker.

4. **[#32683 – Codex App crashes in CrBrowserMain when Browser Use opens a page](https://github.com/openai/codex/issues/32683)** (27 comments, 8 👍)  
   The in-app browser GPU crash (`0xC0000005` at `chrome.dll`) makes the “Browser Use” feature unusable on Windows. Affects Pro (20x) subscribers.

5. **[#35058 – Codex Diff crashes with “Oops, an error has occurred” in VS Code on macOS](https://github.com/openai/codex/issues/35058)** (20 comments, 48 👍)  
   A high-visibility regression: the “Codex Diff” tab is completely broken on Apple Silicon, affecting every repository. macOS developers are especially vocal.

6. **[#30712 – split writable roots cause apply_patch to fail on Windows](https://github.com/openai/codex/issues/30712)** (15 comments, 13 👍)  
   The safe sandboxed `apply_patch` tool fails on Windows, forcing agents to fall back to PowerShell file writes—defeating the sandbox security model. A serious confidence issue for Windows Pro users.

7. **[#34061 – Insane Codex Disk Usage from Subagents](https://github.com/openai/codex/issues/34061)** (14 comments)  
   Reported with Codex CLI 0.144.6 and `gpt-5.6` on macOS. Subagents consume disproportionate disk space, potentially flooding SSDs. Performance concern for long-running agent workflows.

8. **[#34133 – Page.captureScreenshot crashes GPU process](https://github.com/openai/codex/issues/34133)** (24 comments)  
   Code Integrity Event 3033 blocks bundled `vk_swiftshader.dll`, causing the GPU process to crash during screenshot capture. Systematic Windows issue tied to driver signing policies.

9. **[#35613 – Code mode reports completion with live nested exec sessions but no model-visible handles](https://github.com/openai/codex/issues/35613)** (3 comments, fresh)  
   The agent reports “done” while child processes are still running, and there is no handle for the model to inspect them. A safety and correctness risk for automation.

10. **[#35463 – Subagents drain full week quota overnight](https://github.com/openai/codex/issues/35463)** (3 comments)  
    Pro 20x users report subagent usage counting is broken, exhausting an entire week’s quota in a single night. Financially and operationally severe.

## Key PR Progress
1. **[#35695 – Honor the configured SQLite home in the logs client](https://github.com/openai/codex/pull/35695)**  
   Fixes `just log` reading the wrong database when `sqlite_home` or `CODEX_SQLITE_HOME` is set. Critical for users with custom data directories.

2. **[#35693 – Refresh the subagent picker in the background](https://github.com/openai/codex/pull/35693)** (CLOSED)  
   Eliminates blocking TUI input while the subagent picker loads thread metadata and event-store locks. Directly improves interactive CLI responsiveness.

3. **[#35691 – Include empty-preview threads in relationship listings](https://github.com/openai/codex/pull/35691)** (CLOSED)  
   Ensures threads without preview text still appear in parent/child relationship queries, fixing an omission in the spawn graph.

4. **[#35685 – Load cloud-managed profiles for `codex sandbox`](https://github.com/openai/codex/pull/35685)** (CLOSED)  
   Introduces `--include-managed-config` flag to load cloud-managed sandbox profiles. A step toward enterprise policy enforcement.

5. **[#35675 – Prepare MCP and plugin recommendations concurrently](https://github.com/openai/codex/pull/35675)** (CLOSED)  
   Reduces startup latency by fetching MCP runtime capabilities and plugin recommendations in parallel instead of sequentially.

6. **[#35670 – Raise the Windows exec yield floor to 10 seconds](https://github.com/openai/codex/pull/35670)** (CLOSED)  
   Addresses premature `exec_command` yields on Windows by clamping the minimum yield time. Targets Windows-specific tool reliability.

7. **[#35655 – Terminate Windows non-TTY processes on interrupt](https://github.com/openai/codex/pull/35655)** (CLOSED)  
   Fixes an issue where sending Ctrl-C to non-TTY Windows exec sessions wasn’t stopping the process. Improves interrupt handling parity with Unix.

8. **[#35649 – Preserve TUI input when terminal focus returns](https://github.com/openai/codex/pull/35649)** (CLOSED)  
   Prevents keystroke loss when a terminal gains focus by caching the palette. Improves CLI typing experience on focus events.

9. **[#35656 – Preserve multi-agent settings across config representations](https://github.com/openai/codex/pull/35656)** (CLOSED)  
   Fixes a config layering bug where `features.multi_agent_v2` could be silently replaced when mixing legacy boolean and table forms.

10. **[#35663 – Evaluate character matching over skill routing metadata](https://github.com/openai/codex/pull/35663)** (CLOSED)  
    Adds n-gram matching across skill descriptions, host interfaces, and tool dependencies for smarter skill routing—improving agent accuracy.

## Feature Request Trends
- **/undo Revival (High Urgency)** – Issue #9203 (362 👍) is the single most requested feature. Users want a reliable way to revert unintended file modifications and deletions, especially for files not tracked by git.
- **Enterprise MCP OAuth Lifecycle** – Issue #35006 tracks end-to-end OAuth reliability for enterprise SSO, indicating growing demand for production auth flows.
- **Faithful Residual Fidelity** – Issue #35528 proposes that Codex should expose a durable statement of what was captured, elided, or omitted during tool output—important for auditability.
- **Residual/Blocked Goal Transitions** – Issue #29370 requests better UI state management when agents are blocked and manually resumed.

## Developer Pain Points
- **Windows Stability Crisis** – A cluster of 5+ high-comment issues (#32149, #32683, #34133, #34450, #30712) describe crashes, GPU failures, sandbox hangs, and input lag exclusive to Windows. This is the #1 platform pain point.
- **Rate-Limit & Reset Issues** – Two issues (#31606, #35463) involve broken reset counting and quota exhaustion. These erode trust in the Pro/Pro 20x subscription model.
- **Subagent & Disk Usage** – Subagents cause excessive disk consumption (#34061) and can drain quotas overnight (#35463). Combined with the multi-agent V1/V2 model rejection bug (#35097), subagent reliability is a recurring frustration.
- **macOS Diff & Permissions** – The Codex Diff crash (#35058) on macOS Silicon and repeated privacy prompts (#35140) show that macOS UX also has rough edges.
- **Sandbox Bypass on Windows** – Issue #30712 highlights that the safe patch path is broken, forcing agents to bypass the sandbox—undermining a core security promise.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-28

## Today's Highlights

Agent reliability remains the dominant theme, with two critical P1 bugs—subagents falsely reporting success after hitting turn limits and the generalist agent hanging indefinitely—still active after months. On the security front, three P1 PRs targeting variable expansion bypasses, MCP OAuth token refresh, and Authorization header stripping are under active review. A new nightly build (v0.54.0-nightly.20260727) was published.

---

## Releases

- **[v0.54.0-nightly.20260727.g3818efbbf](https://github.com/google-gemini/gemini-cli/releases/tag/v0.54.0-nightly.20260727.g3818efbbf)** — Automated nightly release. No detailed changelog beyond the version bump. [Full diff](https://github.com/google-gemini/gemini-cli/compare/v0.54.0-nightly.20260726.g3818efbbf...v0.54.0-nightly.20260727.g3818efbbf).

---

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**
   P1 bug. A `codebase_investigator` subagent hits its turn limit before any analysis, yet reports `status: "success"` with `Termination Reason: "GOAL"`. Hides true failure from users. 12 comments, 2 👍. Open since March.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)**
   P1 bug. Simple tasks like folder creation cause an indefinite hang when the CLI defers to the generalist agent. Workaround: instructing the model not to use sub-agents. 8 comments, 8 👍 — highest community reaction.

3. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)**
   P1 bug. After executing simple CLI commands, Gemini hangs showing "Awaiting user input" even though the command finished. Persistent and reproducible. 4 comments, 3 👍.

4. **[#19873 — Leverage model's bash affinity via zero-dependency OS sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)**
   P2 enhancement. Proposes capitalizing on Gemini 3's native bash proficiency with POSIX tools while ensuring security through sandboxing. Large effort, 8 comments.

5. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**
   P2 bug. The extraction agent only marks sessions as processed when it calls `read_file`. Sessions deemed low-signal remain unprocessed and keep resurfacing. 5 comments. Part of a memory system bug cluster.

6. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**
   P2 bug. Custom skills and sub-agents are rarely invoked autonomously; they work only when the user explicitly instructs. Affects discoverability and utility. 6 comments.

7. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**
   P1 bug. The browser agent terminates with "GOAL" but fails silently in Wayland environments. 4 comments, 1 👍. Affects Linux users.

8. **[#24246 — 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**
   P2 bug. When tool count exceeds 128, the CLI hits a 400 error from the API. Suggests smarter tool scoping. 3 comments.

9. **[#22672 — Agent should discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**
   P2 feature. The model occasionally uses `git reset`, `--force`, or dangerous DB commands when safer alternatives exist. Needs harm-reduction heuristics. 3 comments, 1 👍.

10. **[#22093 — Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)**
    P2 bug. Subagents activate despite being disabled in configuration. User expected only MCP functionality. 3 comments. Affects trust in configuration system.

---

## Key PR Progress

1. **[#28403 — Block $VAR and ${VAR} variable expansion bypass](https://github.com/google-gemini/gemini-cli/pull/28403)**
   P1, area/security. Fixes an incomplete check in `detectBashSubstitution()` and `detectPowerShellSubstitution()` that allowed shell variable expansion to bypass security gates added for GHSA-wpqr-6v78-jr5g. Also hardens the deduplication workflow.

2. **[#28481 — Refresh MCP OAuth tokens with stored client ID](https://github.com/google-gemini/gemini-cli/pull/28481)**
   P1, area/security. Fixes MCP OAuth token refresh for servers configured via OAuth discovery. Previously, refresh failed locally before any network I/O and deleted stored credentials, forcing re-auth.

3. **[#28551 — Fall back to embedded macOS seatbelt profiles](https://github.com/google-gemini/gemini-cli/pull/28551)**
   Size/l. Fixes a critical startup crash when running sandbox mode (`-s`) on macOS/gMac where static `.sb` seatbelt profiles are missing from runfiles or bundle folders.

4. **[#28546 — Strip Authorization header with GEMINI_API_KEY auth](https://github.com/google-gemini/gemini-cli/pull/28546)**
   P1, area/security. Removes leftover `Authorization` headers when using `x-goog-api-key` auth, preventing conflicts with Google API endpoints.

5. **[#28485 — Add gemini-3.5-flash to model selector](https://github.com/google-gemini/gemini-cli/pull/28485)**
   P2, area/core. Fixes an issue where users on v0.51.0 cannot select newer model versions because the selector only surfaces legacy model constants. Runtime detection is added.

6. **[#28446 — Use native fetch for OAuth token exchange](https://github.com/google-gemini/gemini-cli/pull/28446)**
   P1, area/security. Replaces the fetch implementation for OAuth token exchange to avoid "Premature close" errors on headless VPS environments.

7. **[#28549 — Disclose Plan Mode read-only status as server claim](https://github.com/google-gemini/gemini-cli/pull/28549)**
   area/security. Fixes a gap where `plan.toml` promoted MCP tools with `readOnlyHint` out of the deny-all into `ask_user`, without independent verification.

8. **[#28523 — Enforce explicit tag length in file keychain](https://github.com/google-gemini/gemini-cli/pull/28523)**
   CLOSED, size/m. Configures explicit 128-bit authentication tag length and validation for file-based credential storage, hardening against malformed data across Node.js runtimes.

9. **[#28531 — Normalize CRLF to LF in a2a-server](https://github.com/google-gemini/gemini-cli/pull/28531)**
   CLOSED, size/m. Fixes a Windows-only bug where side-by-side diffs in Gemini Code Assist showed no changes due to CRLF/LF line ending mismatches.

10. **[#28363 — Prevent AbortSignal listener leak in ShellExecutionService](https://github.com/google-gemini/gemini-cli/pull/28363)**
    CLOSED, size/xs. Ensures `AbortSignal` event listeners are removed when processes finish, preventing memory leaks in long-lived sessions.

---

## Feature Request Trends

- **AST-aware codebase analysis**: [Issue #22745](https://github.com/google-gemini/gemini-cli/issues/22745) and [Issue #22746](https://github.com/google-gemini/gemini-cli/issues/22746) propose using AST tools for precise method-bound reading, reducing misaligned reads and token noise. This is a recurring theme from the evaluations team.

- **Zero-dependency OS sandboxing**: [Issue #19873](https://github.com/google-gemini/gemini-cli/issues/19873) advocates for leveraging Gemini 3's native bash abilities while sandboxing execution, a balance of performance and security.

- **Subagent trajectory sharing**: [Issue #22598](https://github.com/google-gemini/gemini-cli/issues/22598) asks for subagent trajectories to be visible via `/chat share` for easier review and evaluation.

- **Agent self-awareness**: [Issue #21432](https://github.com/google-gemini/gemini-cli/issues/21432) wants the CLI to understand its own mechanics—flags, hotkeys, and execution—well enough to act as its own guide.

- **Component-level evaluations**: [Issue #24353](https://github.com/google-gemini/gemini-cli/issues/24353) tracks scaling behavioral evals from 76 tests to cover all supported models and common workflows.

---

## Developer Pain Points

- **False success reporting**: Agents (especially subagents) terminating with "GOAL" status despite hitting limits or failing silently is the top frustration. [Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323) and [Issue #21763](https://github.com/google-gemini/gemini-cli/issues/21763) both highlight this.

- **Indefinite hangs**: The generalist agent hanging [Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409) and shell commands stuck at "Waiting input" [Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166) represent persistent reliability gaps.

- **Configuration ignored/overridden**: Subagents activating despite being disabled [Issue #22093](https://github.com/google-gemini/gemini-cli/issues/22093) and the browser agent ignoring `settings.json` overrides [Issue #22267](https://github.com/google-gemini/gemini-cli/issues/22267) erode user trust in configuration.

- **Memory system loops**: Auto Memory retrying low-signal sessions indefinitely [Issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522) and silently skipping invalid patches [Issue #26523](https://github.com/google-gemini/gemini-cli/issues/26523) indicate quality gaps in the persistence layer.

- **Destructive operations**: The model's occasional use of `--force` and `git reset` without user confirmation [Issue #22672](https://github.com/google-gemini/gemini-cli/issues/22672) raises safety concerns for production workflows.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest – 2026-07-28**

---

## 1. Today's Highlights

The Copilot CLI shipped **v1.0.76-0**, bringing faster MCP tool loading and improved autopilot persistence. A key **regression in plan-mode** (Issue #4188) is drawing heavy community attention, while a major **zombie process bug** on Linux (Issue #4163) has been resolved. Community demand for **ACP protocol parity** and **context-tier exposure** continues to grow.

---

## 2. Releases

- **v1.0.76-0** (latest): 
  - **Improved**: MCP tools now load faster from definition-scoped snapshots; new cache opt-outs per server and process-wide.
  - **Autopilot**: Stays selected after `task_complete` by default. Set `stayInAutopilot: false` to return to interactive mode after each task.
  - **Fixed**: Restored early warning logic (details partially truncated in changelog).

---

## 3. Hot Issues

1. **#4188 – Regression on plan-mode** *(OPEN, +3👍)* – Plan-mode in the latest version blocks shell commands (e.g., `gh` CLI), breaking workflows that relied on them to enrich plans. Considered a critical regression by the community.
   - [View Issue](https://github.com/github/copilot-cli/issues/4188)

2. **#4163 – Zombie child processes on Linux** *(CLOSED, +3👍)* – Resolved. Child processes accumulated as zombies (~2/min), leading to PID exhaustion. Fix included in recent release.
   - [View Issue](https://github.com/github/copilot-cli/issues/4163)

3. **#4183 – Auto-compaction fails vs. 5 MB CAPI body limit** *(CLOSED, +10👍)* – Long sessions with many tool calls hit a 5MB HTTP body limit even when under context-token capacity. Auto-compaction didn't prevent it.
   - [View Issue](https://github.com/github/copilot-cli/issues/4183)

4. **#2792 – Auto-switch between planning & execution models** *(CLOSED, +16👍)* – Feature request for one model for planning, another for execution. Now closed, suggesting it may be in the works.
   - [View Issue](https://github.com/github/copilot-cli/issues/2792)

5. **#4161 – `task_complete` tool unavailable after autopilot re-entry** *(OPEN, +3👍)* – Regression: `task_complete` is filtered out after switching *back* to autopilot mode, despite earlier fix claiming it's always available.
   - [View Issue](https://github.com/github/copilot-cli/issues/4161)

6. **#4159 – Blank interactive UI on Windows Terminal** *(OPEN, +3👍)* – Submitting a prompt in interactive mode on Windows Terminal clears all output. Non-interactive (`-p`) mode works fine.
   - [View Issue](https://github.com/github/copilot-cli/issues/4159)

7. **#1381 – Rewind fails without git** *(OPEN, +9👍)* – Rewind feature is tied to git; users of alternative VCS (e.g., `jj`) are blocked. High demand for decoupling.
   - [View Issue](https://github.com/github/copilot-cli/issues/1381)

8. **#4233 – ACP missing `usage_update` emission** *(OPEN, +2👍)* – `copilot --acp` never sends usage updates for context window or AI credits. Clients like Zed can't show usage indicators despite the CLI having the data.
   - [View Issue](https://github.com/github/copilot-cli/issues/4233)

9. **#4263 – Responses disappear on Windows Terminal vertical splits** *(OPEN, +0👍)* – Scrolling renders first screen only; content disappears. Requires command resubmission to see output.
   - [View Issue](https://github.com/github/copilot-cli/issues/4263)

10. **#4118 – `/app` doesn't default to current directory** *(OPEN, +35👍)* – The `/app` slash command forces manual directory selection. Strong community support for auto-detection.
    - [View Issue](https://github.com/github/copilot-cli/issues/4118)

---

## 4. Key PR Progress

1. **#1609 – Update PAT permission instructions** – Clarifies that `Copilot Requests` is under the *Account* tab in PAT UI, often missed.
   - [View PR](https://github.com/github/copilot-cli/pull/1609)

2. **#1598 – Fix: clean up temp directory on unexpected exit** – Adds a trap to `install.sh` to remove `/tmp` artifacts on command failure, preventing leaks.
   - [View PR](https://github.com/github/copilot-cli/pull/1598)

3. **#1116 – Fix doc: 0x models don't reduce quota** – Corrects README implying quota reduction; 0x models actually don't deduct quota per use.
   - [View PR](https://github.com/github/copilot-cli/pull/1116)

4. **#1333 – Fix grammar and Markdown formatting** – Minimal changes but demonstrates attention to documentation quality.
   - [View PR](https://github.com/github/copilot-cli/pull/1333)

5. **#988 – Fix brew install prefix** – Missing formula prefix in README; fixes installation via Homebrew.
   - [View PR](https://github.com/github/copilot-cli/pull/988)

6. **#4030 – Add Jekyll deployment workflow** – Automates Jekyll build + deploy to GitHub Pages with dependencies.
   - [View PR](https://github.com/github/copilot-cli/pull/4030)

7. **#3928 – Add .gitignore and settings configuration** – Generic improvement for repository hygiene.
   - [View PR](https://github.com/github/copilot-cli/pull/3928)

8. **#2800 – Initial devcontainer configuration** – Adds devcontainer support, likely for easier contributor onboarding.
   - [View PR](https://github.com/github/copilot-cli/pull/2800)

9. **#3873 – Add console log greeting** – Simple initial log message (low impact but open).
   - [View PR](https://github.com/github/copilot-cli/pull/3873)

10. **#4057 – Install** – Generic install script update (open, no details).
    - [View PR](https://github.com/github/copilot-cli/pull/4057)

---

## 5. Feature Request Trends

1. **Autopilot persistence via launch flag** – Multiple requests (e.g., #3977) for `--autopilot` to persist across turns, now partially addressed in v1.0.76-0.
2. **ACP parity with interactive mode** – Users want `usage_update` (#4233), `contextTier` exposure (#4275), and token/context information (#4174) in the ACP protocol.
3. **Multi-model planning/execution** – #2792 (closed) suggests this is under investigation; community strongly supports separate models for planning vs. execution.
4. **Non-git rewind support** – #1381: decouple Rewind from git to support other VCS like `jj`.
5. **`/app` default directory** – #4118: auto-select current working directory for the `/app` command.

---

## 6. Developer Pain Points

1. **Plan-mode regression (shell command blocking)** – #4188: Users rely on tools like `gh` to enrich plans; blocking them feels like a backward step.
2. **UI breakage on Windows Terminal** – #4159, #4263: Blank output after prompts in interactive/split-pane modes; persists across versions.
3. **Clipboard failures in tmux/WSL** – #4191: Copy-paste breaks when chaining VS Code → WSL → tmux/screen.
4. **Zombie processes** – #4163 (fixed): PID leaks causing session degradation; a relief that this is resolved.
5. **ACI credit consumption on restart** – #3886: `/restart` and `/resume` consume a non-trivial fixed number of credits (174), surprising users.
6. **MCP/OAuth keychain conflicts on macOS** – #4273: Dual-signed binaries (GitHub vs. Microsoft) cause repeated keychain prompts due to partition ACL mismatch.
7. **`glob` tool broken for path-separators** – #4271: Multi-segment patterns fail unless prefixed with `**/`, breaking common use cases.

---

*Data aggregated from github.com/github/copilot-cli (2026-07-28).*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-28

## Today's Highlights

After a quiet release cadence, the community is actively patching two critical Windows encoding crashes and a GC-related hook bug that silently drops post-tool tasks. A new PR introduces configurable prompt cache key disabling, giving developers more control over caching behavior in managed Kimi provider setups. Meanwhile, the longstanding VSCode extension issue of invisible approval prompts continues to frustrate users on the Allegretto plan.

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **#1070 – Login failed: Network unreachable** (CLOSED, 8 comments)  
   A months-old network connectivity bug that was resolved but serves as a reference for users experiencing auth.kimi.com access issues.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/1070)

2. **#2317 – VSCode: Plan mode file path not clickable in chat webview** (OPEN, 3 comments)  
   A UX pain point: file paths rendered in the chat webview during Plan mode are plain text instead of clickable links, disrupting developer workflow.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2317)

3. **#2564 – Hooks: PostToolUse / PostToolUseFailure tasks collected by GC before completion** (OPEN, 0 comments)  
   **Critical:** Registered hook subprocesses are silently dropped because the GC collects hook tasks before they finish. This causes non-deterministic hook execution and broken post-tool pipelines.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2564)

4. **#2563 – VS Code extension: approval prompts intermittently never render** (OPEN, 0 comments)  
   **Critical:** `ExitPlanMode` and tool permission prompts stall indefinitely or timeout silently after 600s. Affects Allegretto plan users on macOS with extension `0.6.4`. High impact on daily workflow reliability.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2563)

---

## Key PR Progress

1. **#2539 – fix(mcp): normalize tools for Moonshot API** (OPEN, 0 comments)  
   Generates stable Moonshot-compatible aliases for MCP tool names while preserving originals for upstream routing. Fixes missing root `object` type in MCP schemas and corrects `anyOf`/required shape issues.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2539)

2. **#2562 – fix(llm): allow disabling prompt cache key** (OPEN, 0 comments)  
   Adds a `prompt_cache_key` boolean to `kimi` provider config. When set to `false`, omits the session-derived prompt cache key field from requests. Default behavior unchanged. Documentation included in English and Chinese.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2562)

3. **#2561 – Fix UnicodeEncodeError on startup when stdio uses non-UTF-8 encoding** (OPEN, 0 comments)  
   Fixes #1436. On Windows Git Bash, the welcome banner logo (`▐█▛█▛█▌`) crashes with `gbk` codec error. This PR handles the encoding gracefully so the CLI can start on non-English-locale terminals.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2561)

4. **#2560 – Fix UnicodeEncodeError in web banner when stdout is non-UTF-8 (Windows)** (OPEN, 0 comments)  
   Fixes #2532. Similar encoding crash but for `kimi web` when stdout is redirected in Chinese locale (codepage 936). Error: `'gbk' codec can't encode character '➜'`. Patches `print_banner` before the HTTP server binds.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2560)

---

## Feature Request Trends

- **Prompt cache control:** Developers want explicit toggles for prompt caching in managed provider configs (see PR #2562). This addresses cost and latency optimization needs.
- **MCP tool normalization:** There is growing demand for stable, API-compatible tool naming and schema handling when bridging MCP to Moonshot endpoints (PR #2539).
- **Windows encoding resilience:** Repeated crashes on non-UTF-8 Windows terminals (Git Bash, redirected stdout, Chinese locale) are driving systematic encoding hygiene improvements across CLI entry points.

---

## Developer Pain Points

1. **Silent hook failures (GC-driven):** `PostToolUse`/`PostToolUseFailure` hooks being garbage collected without warning is a high-severity reliability issue — developers cannot trust their post-tool automation pipelines.
2. **VSCode extension approval prompt unreliability:** Intermittently invisible `ExitPlanMode` and tool permission dialogs cause indefinite stalls, making the extension unusable for extended periods, especially on the Allegretto plan.
3. **Windows encoding crashes:** Two separate UnicodeEncodeError issues surfaced this week alone (startup and `kimi web`), indicating that non-UTF-8 Windows configurations remain a persistent compatibility blind spot.
4. **Non-clickable file paths in chat:** The inability to click file paths in Plan mode chat webview adds friction to reviewing and navigating generated changes.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-28

## Today's Highlights
Two critical renderer crashes plaguing **Desktop 1.18.7** were identified and acted upon: the `AutoScroller`/`Scroller` dependency error makes Settings and drag-and-drop views unusable. Meanwhile, the community is raising serious alarms about **model reliability** — duplicate responses, infinite tool-call loops, and the `deepseek-v4-flash-free` agent dropping after every tool call are top friction points. On the positive side, **kitlangton** landed three major test-infrastructure PRs, including the final acceptance criterion for native-watcher command reloads.

## Releases

### v1.18.7 (today)
**Desktop bugfixes:**
- Removed extra titlebar inset on macOS fullscreen
- Fixed shadowed command palette entries reappearing after removal
- Added scrolling to long project selector dropdowns (@david1gp)
- **Known regression:** Introduces `AutoScroller` renderer crash when opening Settings or any drag-and-drop view (see #39162, #38107, #38830)

### v1.18.6 (yesterday)
**Core:**
- Fixed branch-specific repository caches: refreshing one reference no longer moves another branch checkout

**Desktop:**
- Improved compatibility with newer client API across directory, project, session, and terminal flows
- Fixed legacy MCP issues

## Hot Issues

1. **#25270 — Bug: Model generates identical response twice** (23 comments, 4 👍)  
   *Persistent, 3 months old.* Model outputs exact duplicate responses. Screenshots show identical token sequences. Community suspects provider-side deduplication logic failure or client-level replay. [Issue Link](https://github.com/anomalyco/opencode/issues/25270)

2. **#9281 — [FEATURE] Add unified usage tracking via /usage** (11 comments, 31 👍)  
   *Highest 👍 count this week.* Users want a single `/usage` endpoint after OAuth login to view plan limits and rate consumption across providers. No built-in dashboard exists. [Issue Link](https://github.com/anomalyco/opencode/issues/9281)

3. **#29703 — Allow changing project folder path without losing session history** (9 comments, 13 👍)  
   Session data is tied to absolute paths. Renaming or moving a directory nukes all history. Popular demand for path-independent session identity. [Issue Link](https://github.com/anomalyco/opencode/issues/29703)

4. **#28596 — Bug: repeated tool calls** (5 comments)  
   Model enters infinite loop of identical tool/exec calls. Requires manual interruption. Agent should self-detect and recover. Likely related to #25270. [Issue Link](https://github.com/anomalyco/opencode/issues/28596)

5. **#38107 — fix(desktop v2) fatal renderer error with Auto Scroller** (4 comments)  
   Dev build crashes on home navigation: `Error: AutoScroller plugin depends on Scroller plugin`. Affects 1.18.4+. [Issue Link](https://github.com/anomalyco/opencode/issues/38107)

6. **#38830 — AutoScroller plugin depends on Scroller plugin** (4 comments)  
   Same crash in production 1.18.7, reproduced by multiple users. Renderer completely unusable after navigating to settings. [Issue Link](https://github.com/anomalyco/opencode/issues/38830)

7. **#38979 — Desktop UI freezes after closing a project on macOS** (4 comments)  
   After closing a project via context menu, entire UI becomes unresponsive. Hover effects still work, suggesting renderer is alive but event loop is blocked. [Issue Link](https://github.com/anomalyco/opencode/issues/38979)

8. **#39162 — Desktop 1.18.7: renderer crashes with AutoScroller when opening Settings** (3 comments)  
   *Closed with PR #39217 now awaiting verification.* The crash is reliably triggered by any screen with sortable/drag-and-drop lists. [Issue Link](https://github.com/anomalyco/opencode/issues/39162)

9. **#39181 — TUI applies events from other directories when several TUIs share one server** (2 comments)  
   Running multiple `opencode serve` TUIs causes branch names from other projects to leak into the sidebar. [Issue Link](https://github.com/anomalyco/opencode/issues/39181)

10. **#39204 — deepseek-v4-flash-free stops the agent loop after nearly every tool call** (1 comment)  
    New issue with high impact: `read`, `grep`, `glob`, `todowrite` all cause the agent to halt. User must type "continue" repeatedly. [Issue Link](https://github.com/anomalyco/opencode/issues/39204)

## Key PR Progress

1. **#39217 — fix(app): use blue for server status attention** (merged today)  
   Uses blue accent for MCP auth/registration attention states, preserves orange for errors, green for healthy, red for disconnected. Direct fix for #39162 AutoScroller crash. [PR Link](https://github.com/anomalyco/opencode/pull/39217)

2. **#39223 — test(core): synchronize overflow interruption** (open)  
   Makes overflow-recovery tests synchronize on provider-start milestones using `Deferred` instead of polling. Improves test determinism. [PR Link](https://github.com/anomalyco/opencode/pull/39223)

3. **#39220 — fix(app): refresh global provider state** (merged)  
   Refreshes all active provider catalogs after connecting a new provider. Keeps home settings in sync with new-session connections. [PR Link](https://github.com/anomalyco/opencode/pull/39220)

4. **#39216 — test(core): add native watcher command reload test** (merged)  
   Final acceptance criterion for #37429. End-to-end test that a real markdown file write reaches the live command registry through parcel native watcher → Config watch topology. [PR Link](https://github.com/anomalyco/opencode/pull/39216)

5. **#39172 — test(core): align tool contract expectations** (merged)  
   Restores V2 unit suite after consolidated tool architecture. Fixes runner request envelope, tool result shape, and test service dependencies. [PR Link](https://github.com/anomalyco/opencode/pull/39172)

6. **#39211 — feat(core): improve edit tool output** (merged)  
   Replaces synthetic diff previews with concise replacement-count output. Reports actual match count on ambiguous edits, includes target path in failures. [PR Link](https://github.com/anomalyco/opencode/pull/39211)

7. **#39213 — docs(opencode): clarify task_id source and when to resume a subagent** (open)  
   Closes #39212 — adds two clarifications to the Task tool prompt about where task_id comes from and when parent should retry vs. let the subagent's error surface. [PR Link](https://github.com/anomalyco/opencode/pull/39213)

8. **#39203 — refactor(core): manage watcher lifecycle with RcMap** (merged)  
   Makes `Watcher` acquisition interruption-safe. Previously a pending native Parcel subscription (up to 10s timeout) ran inside a locked region, making it uninterruptible during shutdown. [PR Link](https://github.com/anomalyco/opencode/pull/39203)

9. **#39206 — fix(desktop): make file:// chat links clickable** (open)  
   Closes #37891. DOMPurify was stripping `file://` protocols, and the shell `open` command wasn't called. Now absolute paths in chat become clickable desktop links. [PR Link](https://github.com/anomalyco/opencode/pull/39206)

10. **#38534 — feat(tui): emit toast mount event** (open)  
    Adds `tui.toast.mount` lifecycle event for server plugins, enabling plugin-driven toast interactions. [PR Link](https://github.com/anomalyco/opencode/pull/38534)

## Feature Request Trends

- **Unified usage/rate-limit dashboard** (#9281, 31 👍) — strong community demand for `/usage` endpoint post-OAuth
- **Portable session identity** (#29703, #39199) — sessions should survive folder renames/moves; multiple PRs now in flight for dynamic root directory changes
- **Better desktop link support** (#37891, partially addressed by #39206) — users want file:// and absolute path links to work natively in chat
- **AppStream metadata for Linux packages** (#35984, now closed by #36872) — `.deb`/`.rpm` packages now include proper metainfo for software center display

## Developer Pain Points

- **Model response reliability is the #1 frustration.** Duplicate responses (#25270), infinite tool loops (#28596), and agent stalling after every tool call (#39204, #39219) collectively dominate the issue tracker. Users report these across multiple providers (DeepSeek V4 Flash, generic models).
- **Desktop renderer crashes on 1.18.7** — the `AutoScroller` dependency error (#38107, #38830, #39162) makes Settings and project management views completely unusable. This is a critical regression from the latest release.
- **Multi-session TUIs leak state** (#39181) — branch names and events from one project appear in another when sharing a server, undermining the TUI multi-project workflow.
- **Provider authentication friction** — OpenCode Go subs blocked by upstream 401 (#39215); Kimi K3 rejects temperature parameter (#39214); OAuth users have no visibility into plan consumption (#9281).
- **Subagent failure recovery is opaque** (#39196) — when a foreground subagent fails, no `task_id` is returned, leaving the parent model unable to resume partial work.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-28

*Generated from github.com/badlogic/pi-mono*

---

## Today's Highlights

A major patch day with 26 PRs and 50 updated issues, dominated by extension API surface expansion (`ctx.scopedModels`, `pre_response` hooks, terminal color-scheme access) and client-side crash fixes. Several high-profile bugs were resolved: the terminal "spontaneous scroll" issue was closed after a two-month investigation, and the `github-copilot` provider token invalidation race has a confirmed root cause. Notably, the community is pushing hard for ephemeral model-scoping by default (#5263), which would fundamentally change Pi's session configuration model.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

**#5263 – Make in-session model and thinking-level changes ephemeral by default** (OPEN, 10 comments, 👍10)  
The most-upvoted open issue proposes a paradigm shift: all model/thinking-level changes affect only the active session unless explicitly made default in `/settings`. Introduces a "Default model" picker. Strong community consensus — this would eliminate the common footgun of accidental global changes.  
[GitHub](https://github.com/earendil-works/pi/issues/5263)

**#6747 – API for enhancing agent message markdown** (OPEN, 8 comments, 👍2)  
Extension authors want to mutate agent message rendering (e.g., LaTeX formula rendering) without altering the LLM payload. The proposal is a `message_render` hook — currently there's no clean extension surface for post-hoc UI transformations. Active design discussion.  
[GitHub](https://github.com/earendil-works/pi/issues/6747)

**#6970 – `github-copilot` provider token invalidation due to wrong OAuth flow** (CLOSED, 4 comments, 👍1)  
Root-cause analysis: Pi uses `GitHub Copilot Plugin` auth instead of proper `OAuth`, causing Copilot servers to invalidate tokens when Pi is used concurrently with `copilot-lsp` or on multiple devices. The fix requires switching to the standard OAuth flow. A significant blocker for multi-device users.  
[GitHub](https://github.com/earendil-works/pi/issues/6970)

**#7161 – `anthropic-messages` never sends `x-client-request-id`** (OPEN, 4 comments)  
Breaks session affinity for proxies that round-robin between Claude accounts. Only the OpenAI paths send this header; Anthropic path is missing it. Simple fix with large impact for users behind API gateways.  
[GitHub](https://github.com/earendil-works/pi/issues/7161)

**#7157 – OpenCode Go provider displays as "OpenCode Zen Go"** (OPEN, 5 comments)  
Trivial but confusing display-name bug in `--list-models`. The label mismatch suggests possibly stale model metadata propagation.  
[GitHub](https://github.com/earendil-works/pi/issues/7157)

**#7143 – Z.AI providers ignore `max_completion_tokens`, need `max_tokens`** (CLOSED, 4 comments)  
Z.AI silently ignores `max_completion_tokens`, falling back to a 65k default — causing truncated long-reasoning outputs mid-tool-call. `detectCompat()` was setting the wrong field. Quickly closed as actionable.  
[GitHub](https://github.com/earendil-works/pi/issues/7143)

**#7132 – Set `AI_AGENT=pi` for child process attribution** (CLOSED, 4 comments)  
Aligns with industry convention (Claude Code, etc.). Minor but important for process tree analysis and tooling interop.  
[GitHub](https://github.com/earendil-works/pi/issues/7132)

**#7128 – New `PI_*` guideline over-encourages bash calls** (CLOSED, 3 comments)  
A recently-introduced system prompt line ("Inspect PI_* environment variables...") is causing models to frequently issue unnecessary `env`-inspection bash commands. Users report increased latency and tool call noise. Closed as acknowledged.  
[GitHub](https://github.com/earendil-works/pi/issues/7128)

**#7171 – Dedupe byte-identical context files in cwd→root walk** (CLOSED, 3 comments)  
When worktrees or symlinked directories contain identical `AGENTS.md`/`CLAUDE.md` files, the current path-only dedup loads duplicate content. Proposed content-hash-based dedup to save token budget.  
[GitHub](https://github.com/earendil-works/pi/issues/7171)

**#7192 – Expose session scoped models to extensions via `ctx.scopedModels`** (CLOSED, 2 comments)  
Companion apps building model pickers have no way to read the session's resolved model set. Would expose `ScopedModel[]` read-only. Merged quickly (see PR #7191).  
[GitHub](https://github.com/earendil-works/pi/issues/7192)

---

## Key PR Progress

**#6881 – Use provider-reported cost when responses include it** (OPEN, `inprogress`)  
Reads `usage.cost` and `cost_details.upstream_inference_cost` from OpenAI-compatible responses. Falls back to catalog rates. Pending broader provider adoption — critical for accurate billing in BYOK setups.  
[GitHub](https://github.com/earendil-works/pi/pull/6881)

**#7022 – Guard tree navigation during agent responses** (OPEN, WIP)  
Blocks `/tree` command while agent is streaming to prevent navigation corruption. Current PoC — design decision pending on whether to block or queue.  
[GitHub](https://github.com/earendil-works/pi/pull/7022)

**#7081 – Support Claude Opus 5 on Bedrock** (CLOSED)  
Configures adaptive thinking for Opus 5, fixes error message verbosity on Bedrock provider.  
[GitHub](https://github.com/earendil-works/pi/pull/7081)

**#7163 – Search index: SQLite FTS5** (OPEN)  
Adds `SessionRepo.search()` with a contentless FTS5 virtual table for SQLite backend. JSONL and memory backends still use in-memory scan. A foundational piece for full-text session search.  
[GitHub](https://github.com/earendil-works/pi/pull/7163)

**#7168 – Auth print commands** (CLOSED)  
Adds `pi auth print-api-key` and `print-bearer-token` for provider/model pairs. Supports debugging and CI credential validation.  
[GitHub](https://github.com/earendil-works/pi/pull/7168)

**#7172 – Send `x-client-request-id` on anthropic-messages** (CLOSED)  
Fixes session affinity gap #7161. Now matches OpenAI behavior.  
[GitHub](https://github.com/earendil-works/pi/pull/7172)

**#7173 – Rename OpenCode Zen Go → OpenCode Go** (CLOSED)  
Fixes #7157. Provider display name now matches the provider slug.  
[GitHub](https://github.com/earendil-works/pi/pull/7173)

**#7174 – Send `max_tokens` for Z.AI providers** (OPEN)  
Fixes #7143. Adds `isZAI` check to `detectCompat()` and uses `max_tokens` instead of `max_completion_tokens`.  
[GitHub](https://github.com/earendil-works/pi/pull/7174)

**#7176 – Prefer configured Bedrock profile over ambient AWS keys** (OPEN)  
Fixes bug where `AWS_ACCESS_KEY_ID`/`AWS_SECRET_ACCESS_KEY` env vars would override Pi's configured profile. The SDK treats explicit credentials over profile config.  
[GitHub](https://github.com/earendil-works/pi/pull/7176)

**#7117 – Add extension creation eval** (CLOSED)  
Replaces a general-knowledge test with a focused Coding Agent eval that creates, reloads, and invokes a Pi extension. Adds `AgentSession` adapter for `vitest-evals`.  
[GitHub](https://github.com/earendil-works/pi/pull/7117)

---

## Feature Request Trends

1. **Extension API expansion** — Multiple requests for new hooks: `pre_response`/`before_send_message` gate (#7137), `ctx.scopedModels` (#7192), terminal color-scheme access (#7197), and durable compaction lifecycle hooks (#7127). Clear pattern: the community wants Pi to be a programmable platform, not just a CLI.

2. **Session model scoping** — #5263 (ephemeral model changes by default) is the most-upvoted open issue. Users are frustrated by accidental global model changes bleeding across sessions.

3. **Compatibility & interop** — `AI_AGENT` env var (#7132), OAuth for GitHub Copilot (#6970), `x-client-request-id` for Anthropic (#7161). Growing emphasis on Pi playing well in enterprise proxy/gateway environments.

4. **Provider auth tooling** — Request for a read-only `pi auth check --json --no-refresh` (#7152) to validate credentials without mutation. Suggests CI/automation use cases are on the rise.

5. **Custom editor rendering** — `setCustomEditorComponent` bug (#7190) and `message_render` hook (#6747) both point to demand for richer UI customization from extensions.

---

## Developer Pain Points

- **Cache thrashing in large sessions** — The terminal `visibleWidth` cache uses FIFO eviction, causing 15% CPU for sessions >512 lines (#7196). A frequent performance complaint among heavy users.

- **Extension installation failures poison directories** — Failed git-based extension installs leave incomplete directories that block future installs (#7189). No retry/recovery mechanism.

- **TUI re-render storms** — Pi does full re-renders every 1s when an active tool card scrolls off viewport (#7194). Painful for remote/websocket session viewers.

- **Symlink extension directories silently ignored** — Extensions fail to load if the directory is a symlink (#7195). Breaks dotfile management workflows.

- **`git install` vs `npm install` inconsistency** — `pi install git:` installs peerDependencies while `npm:` does not (#7182). Inconsistent package manager behavior surprises users.

- **Silent crashes from package manifest typos** — A third-party package typo permanently disables all sessions for a user (#7187). No graceful degradation or user-visible error.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**Date:** 2026-07-28

---

## Today's Highlights

The Qwen Code project is experiencing significant CI turbulence, with a wave of E2E test failures on `main` prompting multiple auto-filed issues and several fix PRs in flight. Concurrently, the community is actively contributing critical fixes for sub-agent hangs, socket retry logic in YOLO mode, and long-context streaming robustness. Two non-production benchmark prereleases (DSW manual POC) were published, while the SWE-bench Verified dataset remains in **QUARANTINED** status.

---

## Releases

- **[dsw-manual-poc-20260727-2]**: Non-production benchmark prerelease. (Ref: v0.20.0-nightly.20260722.b98306b7e)
- **[dsw-manual-poc-20260727-1]**: Non-production benchmark prerelease. (Ref: v0.20.0-nightly.20260722.b98306b7e)

> **SWE-bench Verified Status: QUARANTINED** (500/500 completed; 376 resolved, 116 unresolved, 1 execution)

No stable releases were published today.

---

## Hot Issues (Top 10)

1. **[#7832 – YOLO mode: mid-stream socket close is not retried, making large code generation impossible](https://github.com/QwenLM/qwen-code/issues/7832)** (P1, Bug)
   - Large code output (500+ lines) in headless YOLO mode consistently fails with `UND_ERR_SOCKET`. Community frustration is high given the P1 priority and impact on automated workflows.

2. **[#7831 – Repeated ECONNRESET on streaming responses when context exceeds ~150k tokens](https://github.com/QwenLM/qwen-code/issues/7831)** (P2, Bug)
   - Long sessions hit ECONNRESET errors repeatedly, making sustained interactions unreliable. Points to a deeper long-context stability issue.

3. **[#7835 – Sub-agent asks questions but user has no way to answer](https://github.com/QwenLM/qwen-code/issues/7835)** (P2, Bug)
   - Sub-agents calling `ask_user_question` hang forever with no forwarding mechanism. Critical for any multi-agent workflow. Already triggered two fix PRs (#7880, #7882).

4. **[#7841 – Quota-exhausted 429s retry silently and surface no error to the user](https://github.com/QwenLM/qwen-code/issues/7841)** (P2, Bug)
   - Permanent quota exhaustion (non-transient 429) is misclassified as a rate limit, leading to silent infinite retries. Users are left unaware of billing issues.

5. **[#7819 – `--safe-mode` unconditionally drops ACP session MCP servers](https://github.com/QwenLM/qwen-code/issues/7819)** (P2, Bug)
   - Safe mode strips user-provided MCP configs passed via ACP, breaking integration workflows. Community welcomes the welcome-pr tag.

6. **[#7828 – Git branch display in footer becomes stale after branch switch](https://github.com/QwenLM/qwen-code/issues/7828)** (P3, Bug)
   - UI state not refreshing post-git operations. Minor but high-visibility for daily users.

7. **[#7779 – VP teardown can leave Kitty keyboard flags enabled on the main screen](https://github.com/QwenLM/qwen-code/issues/7779)** (P2, Bug)
   - Terminal corruption on exit when virtual viewport mode is used with Kitty protocol. Affects UX polish for terminal-centric users.

8. **[#7781 – SIGTERM and SIGHUP can leave VP terminal modes active](https://github.com/QwenLM/qwen-code/issues/7781)** (P2, Bug)
   - Incomplete cleanup on process termination signals. Community notes this compounds with the Kitty flag issue above.

9. **[#7856 – Main CI failure cascade: E2E Tests on multiple commits](https://github.com/QwenLM/qwen-code/issues/7878)** (P2, Bug)
   - A stream of auto-filed E2E test failures (`#7878`, `#7860`, `#7813`, `#7804`, `#7797`, `#7794`, `#7787`, `#7780`, `#7773`, `#7759`) suggests a systemic testing infrastructure issue. Community reaction is muted but expectation for a root-cause fix is high.

10. **[#6762 – Feature Request: Skill Context Lifecycle Management](https://github.com/QwenLM/qwen-code/issues/6762)** (P2, Feature)
    - Persistent community ask for unloading/compressing skill context. Discussion remains active with 5 comments and roadmap alignment.

---

## Key PR Progress (Top 10)

1. **[#7882 – fix(core): exclude ask_user_question from subagent tools to prevent hangs](https://github.com/QwenLM/qwen-code/pull/7882)** (OPEN)
   - Direct fix for #7835. Blocks `ask_user_question` from background sub-agents, resolving indefinite waits.

2. **[#7836 – feat(serve): support caller-supplied sessionId in POST /session](https://github.com/QwenLM/qwen-code/pull/7836)** (OPEN)
   - Fixes silent sessionID drop from #7831. Allows clients to supply a sessionId, enabling session continuity across restarts.

3. **[#7856 – feat(web-shell): add composer footer renderer](https://github.com/QwenLM/qwen-code/pull/7856)** (CLOSED)
   - Adds optional `renderComposerFooter` hook for hosts to render contextual content below the composer. Already merged.

4. **[#7849 – feat(web-shell): add native workspace folder picker](https://github.com/QwenLM/qwen-code/pull/7849)** (OPEN)
   - Introduces OS-native folder picker in Web Shell, addressing a long-standing UX gap for workspace selection.

5. **[#7859 – feat(web-shell): add native Live Voice](https://github.com/QwenLM/qwen-code/pull/7859)** (OPEN)
   - Opt-in macOS Live Voice experience with double-Command activation. Ambitious feature for hands-free interaction.

6. **[#7881 – fix(integration): configure Docker sandbox networking for submitted-prompt provenance test](https://github.com/QwenLM/qwen-code/pull/7881)** (OPEN)
   - Makes integration tests work inside container sandboxes by networking CLI ↔ fake server. Important for CI reliability.

7. **[#7871 – fix(cli): pick the memory unit from the rounded figure, not the raw bytes](https://github.com/QwenLM/qwen-code/pull/7871)** (OPEN)
   - Corrects memory unit labeling when values round to the next boundary (e.g., 1023 MiB → 1 GiB). Small but correct.

8. **[#7484 – fix(core): bridge tool-result images for text-only models](https://github.com/QwenLM/qwen-code/pull/7484)** (OPEN)
   - Allows text-only models to "see" images from tool results via shared routing. Significant for multimodal pipeline compatibility.

9. **[#7731 – feat(web-shell): add git branch picker, commit dialog, and create PR flow](https://github.com/QwenLM/qwen-code/pull/7731)** (OPEN)
   - IntelliJ-style git branch management in Web Shell. Large feature with branch checkout, PR creation, and conflict resolution.

10. **[#7812 – fix(serve): Release managed session writer locks on shutdown](https://github.com/QwenLM/qwen-code/pull/7812)** (OPEN)
    - Cooperative daemon shutdown with atomic lock retirement. Prevents resource leaks and orphaned sessions on restart.

---

## Feature Request Trends

Based on active issues, the most-requested feature directions this week:

- **External Context & Memory Integration**: Two detailed proposals (#7585, #7449) advocate for a standardized profile connecting Qwen Code to external knowledge/memory services. Both are documentation-first, provider-neutral designs.
- **Skill Context Lifecycle Management**: Persistent demand (#6762) for loading/unloading/compressing skill bodies in conversation context to manage token budgets.
- **GitHub Channel Notification Dispatching**: Request (#7807) to route issue/PR comments based on GitHub notification reason (mention, review requested, CI failure, etc.).
- **DingTalk Image Delivery**: Request (#7687) to allow agents to send local images (screenshots, charts) through the DingTalk channel instead of file paths.
- **Web Shell Git Workflows**: In-flight PRs (#7731) for branch picker, commit dialog, and PR flows, indicating strong community interest in IDE-grade Git UX within the web terminal.

---

## Developer Pain Points

Recurring developer frustrations from today's issues:

1. **Streaming Stability in Large Sessions**: Multiple reports of socket closures (ECONNRESET, UND_ERR_SOCKET) when context exceeds ~150k tokens or large outputs are generated. The lack of transparent retry in YOLO mode (#7832) is especially painful for automation.
2. **Unreliable CI Pipeline**: A cascade of E2E test failures on `main` (~15 auto-filed issues in 24 hours) undermines developer confidence. The testing infrastructure itself appears to need attention.
3. **Silent Failures**: Quota-exhaustion 429s (#7841), sub-agent hangs (#7835), and socket drops (#7832) all share a common pattern: the system fails without meaningful user feedback. This frustrates debugging and erodes trust.
4. **Terminal State Pollution**: Kitty protocol and SIGHUP teardown issues (#7779, #7781) leave the terminal in a broken state after exit, a recurring complaint for CLI-heavy users.
5. **Safe Mode Overreach**: The `--safe-mode` flag dropping legitimate MCP configurations (#7819) is counterproductive, forcing users to choose between security and functionality.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-28

## Today's Highlights

The project (now branded **CodeWhale**) is in full v0.9.2 release-candidate mode, with an 82-commit umbrella PR opened and ~25 companion harvest PRs landed or in review. A major `#[allow(dead_code)]` debt surfaced (464 attributes across 143 files), cost-modeling accuracy was challenged, and the web/docs presence got a significant upgrade with guide/vocabulary routes and a real-session media manifest. Community contributions are active: a new `thinking_default_expanded` setting shipped, Simplified Chinese translations received a second-pass adversarial review, and an avante.nvim JSON-RPC compatibility fix was merged.

## Releases

None in the last 24 hours. The project is preparing v0.9.2 via integration branch `codex/v092-integration-direct-main`.

## Hot Issues

1. **[🔥 #4797 — Renovate cost: two pricing systems, unpriced cache writes, and a /cost that is one number](https://github.com/Hmbown/CodeWhale/issues/4797)**  
   *Bug, Open* — An audit reveals 2,003 lines of hand-maintained pricing rates, two competing pricing systems, unpriced cache-write costs, and a `/cost` command that returns a single misleading number. Community reaction is muted (2 comments) but this is a high-impact structural debt that could lead to user trust issues. *Why it matters:* Correct billing is foundational for a paid tool.

2. **[🔥 #4785 — Dead-code sweep: 464 #[allow(dead_code)] attributes are hiding drift](https://github.com/Hmbown/CodeWhale/issues/4785)**  
   *Documentation, Open* — The tree carries 464 dead-code suppression annotations across 143 files. When stripped, the compiler reports dead enums, unused variants, and dead functions. *Why it matters:* This blocks the compiler from detecting real structural drift in a large Rust codebase.

3. **[🔥 #4042 — feat: Environment-level tool sandboxing for sub-agents](https://github.com/Hmbown/CodeWhale/issues/4042)**  
   *Bug/Enhancement, CLOSED* — Tracks runtime enforcement of `--disallowed-tools` across sessions, sub-agents, Fleet workers, and MCP servers. Received 20 comments with deep technical discussion on execution-context boundaries. *Why it matters:* Sub-agent security is critical for multi-agent workflows.

4. **[🔥 #4934 — Website non-critique](https://github.com/Hmbown/CodeWhale/issues/4934)**  
   *Open* — A meta-discussion about the website's theming and the fact that the project now has a "super-active website" that deserves better presentation. *Why it matters:* Community cares about project branding and first impressions.

5. **[🔥 #4906 — Show, don't tell: record a real Codewhale session for the site and a README GIF](https://github.com/Hmbown/CodeWhale/issues/4906)**  
   *Documentation, Open* — A request for motion-heavy demo content (Work surface, phase rail, delegate cards). *Why it matters:* Terminal-agent products are inherently visual; prose-only docs hurt adoption.

6. **[🔥 #998 — 文案展示不全 (Partial text display)](https://github.com/Hmbown/CodeWhale/issues/998)**  
   *Enhancement, Open, 10 comments* — A long-standing UI issue where tooltips are truncated. User requests hover-to-show-full-text. *Why it matters:* 10 comments across 2 months indicates persistent UX friction for Chinese-speaking users.

7. **[🔥 #2342 — 输出内容中的文件，能不能支持点击后打开预览 (Click to preview files in output)](https://github.com/Hmbown/CodeWhale/issues/2342)**  
   *Enhancement, Open* — Users want clickable file references in output that open a preview directly, avoiding manual directory navigation. *Why it matters:* A core ergonomic request for terminal-based development.

8. **[🔥 #4930 — Enter during foreground shell should detach it before steering](https://github.com/Hmbown/CodeWhale/issues/4930)**  
   *Bug, Open* — When a foreground shell command blocks (e.g., `sleep 30`), user keystrokes are lost. Natural "type and Enter" impulse fails confusingly. *Why it matters:* A major UX papercut for interactive development.

9. **[🔥 #4925 — Add thinking_default_expanded setting for always-expanded reasoning blocks](https://github.com/Hmbown/CodeWhale/issues/4925)**  
   *Enhancement, CLOSED (shipped)* — Community request from SSH/tmux users where Space key is captured. *Community reaction:* Fast turnaround — opened 2026-07-27, PR merged same day.

10. **[🔥 #3897 — perf(tui): streaming re-parses the whole growing message every chunk (O(N²) markdown)](https://github.com/Hmbown/CodeWhale/issues/3897)**  
    *Performance, CLOSED* — Identified a quadratic-time markdown re-parse on every streaming chunk. Root-caused to `message.rs:53`. *Why it matters:* Streaming performance is table-stakes for a TUI agent.

## Key PR Progress

1. **[#4912 — feat(web): v0.9.2 docs guide/vocabulary, getting-started path, pending media manifest](https://github.com/Hmbown/CodeWhale/pull/4912)**  
   *Open* — Adds `/docs/guide` and `/docs/vocabulary` routes, homepage getting-started flow, and accessibility landmarks. Targets the v0.9.2 integration branch.

2. **[#4931 — Migrate QA PTY test harness from vt100 to rio-vt](https://github.com/Hmbown/CodeWhale/pull/4931)**  
   *Open* — Swaps the TUI PTY test harness to Rio's terminal engine. By @raphamorim (Rio author). *Significance:* Better correctness for TUI rendering tests.

3. **[#4929 — fix(acp): preserve numeric JSON-RPC IDs for avante.nvim compatibility](https://github.com/Hmbown/CodeWhale/pull/4929)**  
   *CLOSED* — By @atmosuwiryo. Fixes a regression where numeric IDs were coerced to strings, breaking Lua callback dispatch in avante.nvim. *Significance:* Shows responsive community maintenance.

4. **[#4928 — feat(tui): add thinking_default_expanded setting](https://github.com/Hmbown/CodeWhale/pull/4928)**  
   *CLOSED* — By @M-Maciej. Ships the always-expanded reasoning blocks feature. Merged same day as issue was filed.

5. **[#4904 — fix(composer): respect the menu limit and resolve git mentions once](https://github.com/Hmbown/CodeWhale/pull/4904)**  
   *CLOSED* — Fixes a regression where `mention_menu_limit = 0` no longer disabled the popup. Self-identified by the author as "a real regression I shipped."

6. **[#4919 — feat: lane control-plane contract, nonblocking /lane interrupt, CLI/TUI fleet parity](https://github.com/Hmbown/CodeWhale/pull/4919)**  
   *CLOSED* — A massive 3,250-line control-plane contract. Introduces stable `<domain>.<verb>` IDs, authority checks, and bounded receipts for Fleet operations.

7. **[#4926 — feat(onboarding): remote mode matrix, offline explore, appearance step, contributor skill](https://github.com/Hmbown/CodeWhale/pull/4926)**  
   *CLOSED* — Completely reworks onboarding: remote/mobile/chat-bridge mode detection, Ctrl+O for offline exit, and contributor skill integration.

8. **[#4923 — feat(tui): visual program slices — luminance audit, selection vocabulary, focus texture, opt-in sound, jellyfish](https://github.com/Hmbown/CodeWhale/pull/4923)**  
   *CLOSED* — Harvest bundle of 5 reviewed visual-supervision PRs including theme contrast audit, selection vocabulary, and accessibility documentation.

9. **[#4927 — fix(billing): dispatch-receipt classification, Moonshot/MiniMax product truth, honest ceilings](https://github.com/Hmbown/CodeWhale/pull/4927)**  
   *CLOSED* — Fixes 8 billing defects including mid-turn provider re-billing, incorrect Moonshot/MiniMax rates, and stale environment URLs.

10. **[#4908 — I18n(zh-Hans): update simplified-Chinese translations to match latest en.json](https://github.com/Hmbown/CodeWhale/pull/4908)**  
    *CLOSED* — By @SparkofSpike. Second-pass adversarial review of all 1,134 translation keys. A reviewer sub-agent independently verified correctness.

## Feature Request Trends

- **Sub-agent safety & tool sandboxing** (#4042) — Community wants environment-level enforcement of allowed/disallowed tools across all execution contexts (sessions, Fleet workers, MCP servers).
- **Rich terminal interactivity** (#2342, #998) — Clickable file previews, hover tooltips, and better inline artifact display are recurring requests from Chinese-speaking users.
- **Session persistence & lifecycle** (#2934, #4397, shipped in #4922) — Durable archived flags, session resume, and sidebar rail management are being actively built.
- **Billing transparency** (#4797) — Users expect accurate, itemized cost tracking rather than a single `/cost` number.
- **Onboarding & discoverability** (#4906, #3413) — Video/session demos, guided first-run experience, and better vocabulary documentation are high priority.

## Developer Pain Points

1. **Dead-code rot** (#4785) — 464 suppressed warnings mask real dead code, making refactoring risky and compiler feedback useless.
2. **Streaming performance regression** (#3897) — O(N²) markdown re-parsing on every chunk is a known performance trap that was recently fixed.
3. **Billing inaccuracy** (#4797) — Two pricing systems, hidden cache costs, and a non-transparent `/cost` command erode user trust in a paid tool.
4. **Keyboard input conflicts** (#4930, #4925) — Foreground shell blocks user keystrokes; SSH/tmux users lose Space key for expansion. Both are being addressed.
5. **Chinese-language UX gaps** (#998, #2342) — Truncated text and non-clickable file references persist despite 10+ comments on each issue.
6. **CI fragility** (#4907) — Deployment workflow always fails on `main` because of a trigger/preflight contradiction, creating noise for contributors.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*