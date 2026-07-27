# AI CLI Tools Community Digest 2026-07-27

> Generated: 2026-07-27 01:30 UTC | Tools covered: 9

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
**Date:** 2026-07-27

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem is experiencing rapid maturation with seven actively maintained tools competing for developer adoption. The landscape is characterized by intense focus on agent reliability, MCP integration stability, and cross-platform parity. While Claude Code maintains the largest community by issue volume and feature requests, tools like Gemini CLI and OpenAI Codex are investing heavily in architectural improvements (AST-aware tools, OAuth serialization). A clear divergence exists between tools prioritizing agent autonomy (DeepSeek TUI, OpenCode) and those emphasizing security-hardened enterprise workflows (Qwen Code, GitHub Copilot CLI). Windows compatibility remains the single largest cross-cutting pain point, with every tool reporting platform-specific regressions.

---

## 2. Activity Comparison

| Tool | Issues Updated (24h) | PRs Updated (24h) | New Release | Top-Voted Open Issue |
|---|---|---|---|---|
| **Claude Code** | 10 hot issues | 7 PRs | None | #8477: Always show thinking (324👍) |
| **OpenAI Codex** | 11 hot issues | 9 PRs | None | #11023: Linux desktop app (852👍) |
| **Gemini CLI** | 10 hot issues | 10 PRs | v0.54.0-nightly | #21409: Generalist agent hangs (8👍) |
| **GitHub Copilot CLI** | 10 hot issues | 0 PRs | None (v1.0.75) | #4163: Zombie processes (3👍) |
| **Kimi Code CLI** | 1 issue | 0 PRs | None | #2559: Image placeholder bug |
| **OpenCode** | 50+ issues | 50+ PRs | None | #28846: Go usage limits (83👍) |
| **Pi** | 10 hot issues | 10 PRs | None | #6665: TUI full core pinning |
| **Qwen Code** | 10 hot issues | 10 PRs | v0.21.0-nightly | #7769: MCP security bypass (P1) |
| **DeepSeek TUI** | 50+ issues | 50+ PRs | None | #3793: Guided constitution creator (17 comments) |

**Key observations:**
- **OpenCode** and **DeepSeek TUI** are the most active by raw community engagement (50+ issues/PRs each)
- **Claude Code** has the highest-voted feature request ecosystem-wide (324👍), suggesting strong user investment
- **GitHub Copilot CLI** had zero PR activity—likely focused on stabilization for v1.0.7x
- **Kimi Code CLI** is comparatively quiet, with only 1 issue updated

---

## 3. Shared Feature Directions

| Theme | Tools Affected | Community Demand |
|---|---|---|
| **Thinking/Reasoning Visibility** | Claude Code (#8477, #30660), Pi (#7151), DeepSeek TUI | Users across tools want real-time reasoning streams, not post-response summaries. Critical for debugging model behavior. |
| **Cross-Platform Parity (esp. Windows & Linux)** | All tools | Windows stability gaps: Claude Code (#81484, #57371), Codex (#34260, #32683), Copilot CLI (#4217, #4263). Linux: Codex (#11023, 852👍), Copilot CLI (#4163 zombies). |
| **MCP OAuth & Authentication** | Codex (#31573, merged PR stack #30294-30416), Copilot CLI (#4203), Qwen Code (#7768-7770), OpenCode (#38257) | OAuth refresh-token handling, session isolation, and credential persistence are fragile across the board. |
| **Session Lifecycle Management** | Codex (#24610, #34061), Claude Code (#72027, #80199), OpenCode (#34184), Pi (#4877) | Users want explicit delete controls, compaction limits, and reliable quota accounting. Privacy and disk usage drive this. |
| **Subagent Reliability & Introspection** | Claude Code (#80716), Gemini CLI (#22323, #21409), OpenCode (#39010), Qwen Code (#7685) | False success reports, indefinite hangs, and invisible agent trajectories erode trust in autonomous workflows. |
| **Custom Provider/BYOK Support** | Copilot CLI (#4258, #4260), OpenCode (#28846), Codex | Users want equivalent feature parity between standard and custom model providers—settings ignored on BYOK paths. |
| **Mobile & Multi-Session Support** | OpenCode (#39030), DeepSeek TUI (#2934), Qwen Code (#6378) | SSE reconnection on mobile, sidebar session panels, and multi-workspace daemon support are emerging requirements. |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | DeepSeek TUI | OpenCode | Qwen Code | Pi |
|---|---|---|---|---|---|---|---|---|
| **Primary Focus** | Agentic coding with rich tool ecosystem | Desktop-first agent with browser automation | High-reliability subagent orchestration | Developer workflow integration (GitHub ecosystem) | Cost-optimized TUI with deep model integration | Multi-provider platform with subscription management | Security-hardened enterprise agent | Lightweight, extensible CLI with compaction |
| **Target User** | Professional developers, power users | Pro subscribers, multi-platform teams | Google Cloud / Gemini-heavy teams | GitHub enterprise, CI/CD pipelines | Cost-conscious developers, DeepSeek users | Community-driven, multi-provider users | Enterprise security teams | Extension developers, automation |
| **Key Differentiator** | Richest plugin/channel ecosystem; highest community engagement | Desktop app with embedded browser; GPT-5.6 integration | AST-aware tools; zero-dependency sandboxing proposal | Deep GitHub integration; MCP OAuth investment | Fastest iteration velocity; localization-first design | Most active PR hygiene; aggressive price pass-through | Strongest security focus; daemon-based architecture | Extension lifecycle hooks; compaction strategy |
| **Security Posture** | Hook-based guardrails; sandbox examples | OAuth serialization; IPC bridge auth | Variable expansion hardening; tag validation | Permission model for `view`/`edit` tools | Policy narrowing observability | Auto-approve gating; model classifier | MCP proxy auth; Electron hardening | Secret redaction; runtime policy |
| **Platform Maturity** | macOS primary; Windows lagging | Desktop app stable; CLI fragile | Nightly releases; P1 bugs persist | v1.0.7x stabilization | Rust-based; CI toolchain fragility | Desktop + TUI + Web; multi-platform | Daemon + CLI + Desktop | npm package; multi-platform |
| **Community Size** | Largest (324👍 top request) | Large (852👍 for Linux app) | Growing (P1 bugs high engagement) | Moderate (3👍 top issue) | Very active (50+ issues/day) | Very active (50+ PRs/day) | Moderate (security-focused) | Small but engaged |

---

## 5. Community Momentum & Maturity

### Rapidly Iterating (Highest Velocity)
- **DeepSeek TUI**: 50+ issues and 50+ PRs in 24 hours. Maintainer @Hmbown is driving daily performance fixes, CI stability, and feature delivery. Localization (12+ locales) and onboarding UX are design priorities. The project feels like it's building toward a major v0.9.2 release.
- **OpenCode**: Equally active (50+ issues, 50+ PRs). Notable for 10+ cleanup PRs from a single contributor, suggesting mature contribution processes. Aggressive price pass-through (DeepSeek V4 Pro cut) and model-gated auto-approve signal product-market fit focus.

### Mature & Community-Rich
- **Claude Code**: Largest feature request ecosystem and deepest community discussions. The 324👍 "always show thinking" request and 92-comment threads indicate a passionate, invested user base. However, no new releases and mounting regression reports (auto-mode classifier, Windows hangs) suggest the team is in a stabilization phase.
- **OpenAI Codex**: The 852👍 Linux desktop app request is the single highest-voted feature across all tools. Recent MCP OAuth PR stack merges show architectural investment, but unresolved kernel panics and GPU crashes undermine trust.

### Stabilization Phase
- **GitHub Copilot CLI**: Zero PR activity suggests a team in triage/stabilization after the v1.0.75 release. Zombie processes on Linux and TUI hangs on NFS are critical regressions blocking enterprise adoption.
- **Gemini CLI**: Active nightly releases and dependency updates, but top P1 bugs (false GOAL success, agent hangs) remain unresolved. The security PR for variable expansion bypass is promising but under review.

### Niche / Lower Activity
- **Kimi Code CLI**: Minimal activity (1 issue) suggests either low adoption or a team in maintenance mode.
- **Pi**: Measured progress with substantive PRs (loadout management, visibleWidth cache, AI_AGENT standardization), but community engagement is small compared to peers.
- **Qwen Code**: Security-focused, with 3 critical vulnerabilities disclosed and closed in 24 hours. Daemon recovery and MCP config persistence issues indicate enterprise reliability concerns.

---

## 6. Trend Signals

### Industry Trends from Community Feedback

1. **"Show Me the Reasoning" is Non-Negotiable**: The #1 feature request across tools is real-time thinking visibility. Developers use reasoning chains to debug, trust, and cost-optimize model output. Tools that hide reasoning behind spinners are losing trust.

2. **Agent Reliability Trumps Feature Velocity**: Every tool has P1 bugs around false success reports, indefinite hangs, or silent failures. The community is signaling that "it worked without telling me it didn't" is the most dangerous failure mode for agentic coding tools.

3. **Windows is Still a Second-Class Citizen**: Despite market share, every tool reports Windows-specific regressions—crash-on-exit, GPU crashes, WSL path issues, bundled background services. The ecosystem treats macOS as primary.

4. **MCP Integration is Becoming Table Stakes**: OAuth serialization, session isolation, and authorization are being reworked across tools. MCP is no longer experimental—it's core infrastructure, and the community expects it to be secure and stable.

5. **Cost Transparency is a Competitive Battleground**: Prompt-cache hit-rate regressions (#3738 in DeepSeek TUI), `/dryrun` preview requests (#1004), and subscription quota complaints (#28846, #38257) all point to a developer base that's acutely sensitive to token economics.

6. **Localization is an Emerging Priority**: DeepSeek TUI is tracking 12+ locale packs. Qwen Code and Kimi Code are Chinese-first. The AI CLI market is no longer English-only, and tools that don't invest in i18n will cede ground in Asia.

### Reference Value for Developers

- **For cost-sensitive teams**: DeepSeek TUI's aggressive optimization and `/dryrun` paradigm offers the best cost-control signals. OpenCode's price pass-through model is unique.
- **For enterprise security teams**: Qwen Code's security disclosure velocity and Claude Code's hook system set the standard. Watch for MCP proxy auth gaps.
- **For cross-platform teams**: No tool offers parity. Wait for GitHub Copilot CLI's v1.0.8x stabilization or Claude Code's Windows fixes before committing.
- **For agent-heavy workflows**: Gemini CLI's AST-aware tooling and OpenCode's sub-agent tracking are leading architectural investments. Avoid tools with P1 agent reliability bugs.
- **For multi-provider users**: OpenCode and DeepSeek TUI offer the most flexible provider abstraction. Copilot CLI's BYOK parity gaps are a blocker for custom provider adoption.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on the official repository data.

---

## Claude Code Skills Community Highlights Report (2026-07-27)

### 1. Top Skills Ranking

The following Skills (Pull Requests) have generated the most community discussion and attention, ranked by engagement.

1.  **fix(docx): prevent tracked change w:id collision** ([PR #541](https://github.com/anthropics/skills/pull/541))  
    A critical bugfix for the DOCX skill preventing document corruption when tracked changes `w:id` collided with existing bookmarks. The high engagement reflects the severe impact of document corruption in enterprise workflows. **Status:** Open.

2.  **Add ODT skill** ([PR #486](https://github.com/anthropics/skills/pull/486))  
    Proposes a comprehensive skill for creating, filling, and converting OpenDocument Format files (.odt, .ods). The discussion focuses on the high demand for open-source document standard support. **Status:** Open.

3.  **Add pyxel skill for retro game development** ([PR #525](https://github.com/anthropics/skills/pull/525))  
    Introduces a skill for the Pyxel retro game engine via MCP server, enabling iterative game development. The conversation covers MCP integration patterns and creative coding workflows. **Status:** Open.

4.  **Add document-typography skill** ([PR #514](https://github.com/anthropics/skills/pull/514))  
    Addresses a universal pain point: orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Users note this fixes issues "every document Claude generates." **Status:** Open.

5.  **feat(skills): add self-audit** ([PR #1367](https://github.com/anthropics/skills/pull/1367))  
    A meta-skill that audits AI output before delivery via mechanical file verification and a four-dimension reasoning quality gate. Discussion centers on its universal applicability across projects and tech stacks. **Status:** Open.

6.  **Add color-expert skill** ([PR #1302](https://github.com/anthropics/skills/pull/1302))  
    A comprehensive color expertise skill covering naming systems (ISCC-NBS, Munsell, XKCD), color spaces (OKLCH, OKLAB, CAM16), and color harmony. High engagement from design-focused users. **Status:** Open.

7.  **Add skill-quality-analyzer and skill-security-analyzer** ([PR #83](https://github.com/anthropics/skills/pull/83))  
    Meta-skills for analyzing other skills across five quality dimensions and security vulnerabilities. Discussion suggests these are becoming essential for the growing marketplace. **Status:** Open.

8.  **Improve frontend-design skill clarity** ([PR #210](https://github.com/anthropics/skills/pull/210))  
    A revision for actionability and internal coherence, ensuring every instruction is executable within a single conversation. The discussion highlights the gap between verbose skills and Claude's token efficiency. **Status:** Open.

### 2. Community Demand Trends

Analysis of Issues reveals five concentrated demand directions:

- **Security & Trust Boundaries** ([Issue #492](https://github.com/anthropics/skills/issues/492), 43 comments, 2 👍): The #1 community concern is community skills distributed under the `anthropic/` namespace enabling trust boundary abuse. Users demand clear official vs. community labeling and permission scoping.
- **Enterprise Skill Distribution** ([Issue #228](https://github.com/anthropics/skills/issues/228), 16 comments, 8 👍): Strong demand for org-wide skill sharing without manual file transfer. Users want shared skill libraries or direct sharing links.
- **Skill-Creator Reliability** ([Issue #556](https://github.com/anthropics/skills/issues/556), 12 comments, 7 👍; [Issue #1169](https://github.com/anthropics/skills/issues/1169)): Persistent reports of `run_eval.py` returning 0% recall across all queries, making the optimization loop ineffective. This is the most critical infrastructure bug.
- **Duplicate Skill Resolution** ([Issue #189](https://github.com/anthropics/skills/issues/189), 6 comments, 9 👍): Installation of `document-skills` and `example-skills` plugins results in identical skills and context window waste. Users want deduplication.
- **Windows & Cross-Platform Compatibility** ([Issue #1061](https://github.com/anthropics/skills/issues/1061), 3 comments, 2 👍): Skill-creator scripts fail on native Windows due to Unix-first assumptions in subprocess handling, encoding, and pipe operations.

### 3. High-Potential Pending Skills

These open PRs are actively discussed and likely to land soon:

- **skill-creator: fix run_eval.py crash on Windows** ([PR #1099](https://github.com/anthropics/skills/pull/1099), joshuawowk) — Fixes the primary blocker for Windows developers using the skill optimization loop.
- **skill-creator: fix Windows subprocess + encoding bugs** ([PR #1050](https://github.com/anthropics/skills/pull/1050), gstreet-ops) — Two 1-line fixes for `PATHEXT` handling and `cp1252` encoding.
- **Fix skill-creator UTF-8 panic on multi-byte characters** ([PR #362](https://github.com/anthropics/skills/pull/362), Mr-Neutr0n) — Replaces character-based length checks with UTF-8 byte-length validation to prevent Rust panics.
- **Detect unquoted YAML special characters** ([PR #361](https://github.com/anthropics/skills/pull/361), Mr-Neutr0n) — Pre-parse check for `description` fields containing `:`, `#`, `{`, `}`, `[`, `]` that cause silent parsing failures.
- **skill-creator: fix run_eval trigger detection** ([PR #1323](https://github.com/anthropics/skills/pull/1323), Polluelo978) — Fixes the fundamental bug where trigger detection misses real skill names and bails on first non-Skill tool.
- **fix(skill-creator): install eval artifact as real skill** ([PR #1298](https://github.com/anthropics/skills/pull/1298), MartinCajiao) — The most comprehensive fix for the 0% recall problem, handling Windows stream reading, trigger detection, and parallel workers.

### 4. Skills Ecosystem Insight

The community's most concentrated demand is for **reliable skill development infrastructure** — specifically, fixing the broken `run_eval.py` evaluation loop and ensuring cross-platform compatibility — before adding new skill functionality, as the entire skills ecosystem depends on the ability to accurately measure and optimize skill descriptions.

---

# Claude Code Community Digest — 2026-07-27

## Today's Highlights

No new releases landed in the past 24 hours, but the community remains highly engaged around two long-running enhancement requests: **always-show thinking mode** (#8477, 324 👍, 92 comments) and **real-time streaming of extended thinking** (#30660, 42 👍, 18 comments). Several regressions emerged in the 2.1.218–2.1.220 range, including a critical **auto-mode classifier bug** in plan mode (#80716) and a **Windows client hang** that makes `claude.exe` completely non-functional (#81484). Security-related PR activity picked up, with fixes for IPv6 firewall bypass in devcontainers and Windows compatibility for agentic security reviewers.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **#8477 — [ENHANCEMENT] Always Show Claude's Thinking**  
   ↳ [Issue](https://github.com/anthropics/claude-code/issues/8477)  
   The top-voted feature request since September 2025. Users want a persistent visibility toggle for Claude's internal reasoning chain, not just the post-response "thinking" summary introduced in v2.0.0. With 324 👍 and 92 comments, this remains the community's most wanted TUI improvement.

2. **#30660 — Stream Extended Thinking in Real-Time During Interactive Mode**  
   ↳ [Issue](https://github.com/anthropics/claude-code/issues/30660)  
   A closely related request: users want to see reasoning tokens as they're generated, not wait for the full thinking phase to complete. The current spinner provides zero visibility into long reasoning chains, a pain point that's been open since March 2026.

3. **#80716 — Auto-Mode Classifier Incorrectly Detects Permission Mode Change in Plan Mode**  
   ↳ [Issue](https://github.com/anthropics/claude-code/issues/80716)  
   A recent regression (v2.1.218) causing the auto-mode classifier to repeatedly fall back to manual approval during plan mode — even for read-only tools like `cd` and `file reads`. Users report this completely breaks the autonomous workflow in plan mode.

4. **#57371 — Windows: Disable Bundled Cowork Background Service**  
   ↳ [Issue](https://github.com/anthropics/claude-code/issues/57371)  
   Windows users are frustrated by the forced `CoworkVMService` background process. The request to disable it for non-Cowork users has 39 👍 and an active discussion about system resource consumption.

5. **#41015 — Configure/Disable URL Handler App Install Location (macOS)**  
   ↳ [Issue](https://github.com/anthropics/claude-code/issues/41015)  
   Claude Code hardcodes its URL handler to `~/Applications/`, which conflicts with system-managed application directories. 34 👍 from users who want control over where system integrations live.

6. **#72027 — Individual Pro Subscriber Blocked: 'Organization Disabled' → 'Max or Pro Required'**  
   ↳ [Issue](https://github.com/anthropics/claude-code/issues/72027)  
   An entitlement sync bug preventing individual Pro subscribers from using Claude Code entirely. The error chain suggests a stale org membership cache that doesn't reconcile with the user's actual plan. Potentially affecting many paying users.

7. **#80199 — Max X5 Usage Instantly Reaches 100% After Software Update**  
   ↳ [Issue](https://github.com/anthropics/claude-code/issues/80199)  
   Post-update usage tracking anomaly: the session limit jumps to 100% immediately, making the tool effectively unusable until the next reset cycle. Suggests a counter deserialization bug.

8. **#44380 — Channel Messages Don't Wake Idle Sessions (--channels plugin)**  
   ↳ [Issue](https://github.com/anthropics/claude-code/issues/44380)  
   The `--channels` plugin shows incoming messages in the terminal but doesn't interrupt the REPL prompt to process them. Critical for any async/multi-agent workflow using Telegram or other channel integrations.

9. **#64479 — Edit Tool Fails on Mixed Literal/Escape Unicode in Multi-Line old_string**  
   ↳ [Issue](https://github.com/anthropics/claude-code/issues/64479)  
   A long-standing bug (originally #52813) that still repros. The edit tool fails when a Unicode character appears both as a literal codepoint and a `\uXXXX` escape across a multi-line span. Affects internationalized codebases.

10. **#81458 — Hook Launch Failures (exit 127) Are Silent and Non-Blocking**  
    ↳ [Issue](https://github.com/anthropics/claude-code/issues/81458)  
    A concerning reliability issue: failed hook invocations are silently skipped, logging `hook_non_blocking_error` only to session transcripts. One user reported 6,865 skipped guardrail invocations with zero visible feedback. Security-sensitive teams should watch this closely.

---

## Key PR Progress

1. **#81500 — Fix 404 Walkthrough Links in AWS Gateway Example**  
   ↳ [PR](https://github.com/anthropics/claude-code/pull/81500)  
   All seven references to the AWS gateway walkthrough URL return 404. This straightforward doc fix resolves broken onboarding paths for Claude Apps Gateway on AWS.

2. **#20448 — Add web4-governance Plugin for AI Governance**  
   ↳ [PR](https://github.com/anthropics/claude-code/pull/20448)  
   Introduces an AI governance plugin with T3 trust tensors, entity witnessing, and R6 audit trails. Aims to provide cryptographic provenance for agent actions — relevant for compliance-heavy workloads.

3. **#38167 — Authenticated GitHub API Requests in Devcontainer Firewall Script**  
   ↳ [PR](https://github.com/anthropics/claude-code/pull/38167)  
   Adds bearer token support to the devcontainer's firewall initialization to avoid rate limiting in shared-IP environments. Solves a common pain point for team/CI usage of Claude Code devcontainers.

4. **#81426 — Fix Security Guidance for Windows venv Layout**  
   ↳ [PR](https://github.com/anthropics/claude-code/pull/81426)  
   Makes the agentic commit reviewer work on Windows by supporting the Windows virtual environment layout. Previously returned `SKIP_WIN32`, leaving Windows users without security-guidance's strongest protection layer.

5. **#68693 — Add Duplicate Label Additively, Don't Replace Existing Labels**  
   ↳ [PR](https://github.com/anthropics/claude-code/pull/68693)  
   Fixes the `closeIssueAsDuplicate` script: previously it replaced all labels with just `duplicate`, erasing platform/area/priority metadata. Now appends the label without clobbering existing ones.

6. **#81423 — Block IPv6 Egress in Devcontainer Firewall**  
   ↳ [PR](https://github.com/anthropics/claude-code/pull/81423)  
   A security fix: the devcontainer firewall only applied `iptables` rules, leaving IPv6 traffic unrestricted on dual-stack Docker networks. Adds `ip6tables` rules to close the bypass.

7. **#81421 — Make Bash Sandbox Example Fail Closed When Sandbox Unavailable**  
   ↳ [PR](https://github.com/anthropics/claude-code/pull/81421)  
   The example settings file advertised "Bash tool must run inside of sandbox" but omitted `failIfUnavailable`, meaning execution could silently escape the sandbox. Now fails closed.

---

## Feature Request Trends

- **Thinking Visibility Dominates**: The #1 trend is transparent reasoning pipelines. Users want both the ability to always see Claude's thinking (#8477) and to stream it in real-time (#30660). This suggests developers rely on reasoning chains to debug and trust model outputs, and the current "spinner until done" UX is unacceptable for long tasks.

- **Windows Ecosystem Gaps**: Multiple Windows-specific issues (Cowork service bundling #57371, MSIX crash recovery #81306, native binary hang #81484) indicate the Windows port still lags behind macOS in stability and configurability.

- **Entitlement & Usage Tracking Fragility**: Several reports (#72027, #80199, #70758) point to a fragile entitlement/usage tracking system that frequently desyncs from reality. Users want reliable, transparent quota accounting — especially for paid Max tier subscribers.

- **Hook Reliability & Visibility**: Issues like #81458 and #80693 show that hooks are a growing surface area for silent failures. Developers want clearer signals when security guardrails fail, and consistent rendering of hook decisions across tools.

---

## Developer Pain Points

1. **Silent Failures Everywhere**: From hook launch errors (exit 127, skipped 6,865 times) to LSP returning incomplete results (#76870) and auto-mode silently falling back (#80716) — the most common frustration is **things breaking without notification**. Users express that "it worked without telling me it wasn't working" is the most dangerous failure mode for an agentic coding tool.

2. **Session Limit Confusion**: Multiple reports of usage limits being consumed too fast or resetting incorrectly. The Max X5 plan's "instantly 100%" bug (#80199) and Pro subscriber lockout (#72027) erode trust in the billing infrastructure.

3. **Auth State Corruption After Sleep**: macOS users (#71757) report that background token refresh after sleep corrupts keychain credentials rather than preserving the old token. A particularly disruptive bug for laptop users who close the lid frequently.

4. **Plugin/Channel Integration Inconsistency**: The `--channels` plugin not waking idle sessions (#44380) and trust dialogs never firing for projects with mismatched onboarding state (#79973) suggest the plugin and project onboarding systems have subtle state machine bugs.

5. **Unicode and Internationalization**: The edit tool's failure on mixed Unicode representations (#64479) and Chinese-language error reports (#68433, closed) highlight ongoing issues for non-English codebases — an area where Claude Code should excel given the model's multilingual capabilities.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest — 2026-07-27

## Today's Highlights

The Codex desktop app's Windows and Linux stability remains the dominant community concern this week, with four GPU/browser crash issues and the long-running Linux app request (#11023) now at 852 upvotes. A significant MCP OAuth PR stack was finally merged after a month-long review cycle, while multiple bug reports highlight ongoing SQLite write amplification and session storage bloat issues that degrade developer experience on long-running agent sessions.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **#11023 – Codex desktop app for Linux** (+852 👍, 187 comments)  
   *[Link](https://github.com/openai/codex/issues/11023)*  
   The most upvoted open issue remains a Linux desktop app request. Community frustration is high; many users cite macOS power consumption issues and want to migrate to Linux workstations. No official response yet.

2. **#34260 – Windows Desktop: unbounded taskkill.exe/conhost.exe cleanup storm exhausts WMI** (+10 👍, 32 comments)  
   *[Link](https://github.com/openai/codex/issues/34260)*  
   A critical Windows-specific bug where Codex enters an infinite process-cleanup loop, spawning hundreds of `taskkill.exe` processes that exhaust WMI provider quota and lock the machine. Affects all recent Windows builds.

3. **#17320 – Excessive SQLite WAL writes during streaming due to TRACE logs ignoring RUST_LOG** (+39 👍, 27 comments)  
   *[Link](https://github.com/openai/codex/issues/17320)*  
   Long-standing performance bug: TRACE-level events are persisted to SQLite despite `RUST_LOG` filtering, causing heavy disk I/O during streaming. Community notes this makes Codex nearly unusable on SSD-constrained machines.

4. **#32683 – Windows Codex App crashes in CrBrowserMain when Browser Use opens a page** (+8 👍, 26 comments)  
   *[Link](https://github.com/openai/codex/issues/32683)*  
   `0xC0000005` access violation in `chrome.dll` when the in-app browser loads web pages. Impacts Pro subscribers heavily, as the browser feature is core to agent workflows.

5. **#31573 – OAuth authentication fails at issuer validation** (+55 👍, 24 comments)  
   *[Link](https://github.com/openai/codex/issues/31573)*  
   Breaking issue for free-tier CLI users: OAuth issuer validation rejects valid tokens, making CLI authentication impossible. Has gained rapid traction since July 8.

6. **#34133 – Page.captureScreenshot crashes GPU process after Code Integrity blocks vk_swiftshader.dll** (20 comments)  
   *[Link](https://github.com/openai/codex/issues/34133)*  
   Windows Code Integrity Event 3033 blocks the bundled Vulkan SwiftShader DLL, causing GPU process crashes when agents take browser screenshots. Common on enterprise-managed Windows 10 machines.

7. **#35050 – GPT-5.6 serializes independent Code Mode calls; explicit batching reduces usage 27–45%** (+15 👍, 13 comments)  
   *[Link](https://github.com/openai/codex/issues/35050)*  
   Model-behavior bug where GPT-5.6 unnecessarily serializes parallel tool calls. Users report batching manually reduces weighted usage by nearly half — suggests significant cost optimization opportunity.

8. **#24610 – Add explicit deletion controls for archived Codex cloud sessions** (+17 👍, 13 comments)  
   *[Link](https://github.com/openai/codex/issues/24610)*  
   Privacy concern: archived cloud sessions retain sensitive project context indefinitely with no delete option. Community requests GDPR-compliant session lifecycle management.

9. **#32530 – VS Code Codex panel stuck loading on Linux: webview assets fail with net::ERR_FAILED** (+12 👍, 12 comments)  
   *[Link](https://github.com/openai/codex/issues/32530)*  
   Ubuntu 26.04 users report the Codex sidebar panel fails to load due to local webview asset resolution failures. Intermittent, with no clear workaround.

10. **#34061 – Insane Codex Disk Usage from Subagents** (+1 👍, 12 comments)  
    *[Link](https://github.com/openai/codex/issues/34061)*  
    Subagent sessions on macOS consume disproportionate disk space. Users report gigabytes of session data per hour of agent work, likely related to compaction and snapshot duplication.

11. **#16866 – Codex v0.118.0 causes macOS kernel panic (os_refcnt overflow) on Apple Silicon** (+1 👍, 9 comments)  
    *[Link](https://github.com/openai/codex/issues/16866)*  
    Critical stability bug: Codex CLI triggers full macOS kernel panics via `os_refcnt` overflow. Despite being filed in April, the issue remains open and unresolved.

## Key PR Progress

1. **#35530 – Track model and personality in world state** (Merged)  
   *[Link](https://github.com/openai/codex/pull/35530)*  
   Adds model and personality tracking to persisted world-state snapshots, enabling accurate model-switch detection during replay. Important for agent reproducibility.

2. **#35525 – Skip inactive TUI threads without pending user interaction** (Merged)  
   *[Link](https://github.com/openai/codex/pull/35525)*  
   Performance optimization for TUI: only collects buffered requests from threads with pending user input, reducing unnecessary event processing.

3. **#35524 – Preserve terminal turn errors in replayed history** (Merged)  
   *[Link](https://github.com/openai/codex/pull/35524)*  
   Critical bugfix: previously, errors embedded in turn completions (e.g., model overload) were lost during history replay, causing false success state in TUI trace.

4. **#35523 – Shut down the in-process outbound router explicitly** (Merged)  
   *[Link](https://github.com/openai/codex/pull/35523)*  
   Fixes app-server shutdown hangs caused by detached processor work retaining outbound message senders.

5. **#30295 / #30296 / #30294 – MCP OAuth serialization stack** (Merged)  
   *[Links: #30295](https://github.com/openai/codex/pull/30295) | [#30296](https://github.com/openai/codex/pull/30296) | [#30294](https://github.com/openai/codex/pull/30294)*  
   A large, multi-PR refactoring of MCP OAuth handling: adds serialized login/logout, auto-store drift reporting, and routes all OAuth recovery through Codex. Addresses #31573's underlying auth instability.

6. **#30416 – Serialize authoritative MCP OAuth refresh transactions** (Merged)  
   *[Link](https://github.com/openai/codex/pull/30416)*  
   Prevents race conditions during OAuth token refresh by serializing refresh transactions, completing the MCP OAuth stability overhaul.

7. **#30985 – Let idle auto-attached threads unload** (Open)  
   *[Link](https://github.com/openai/codex/pull/30985)*  
   Distinguishes implicit observer attachments from explicit subscriptions, allowing core-created threads without subscribers to unload after 30 minutes. Could reduce session memory pressure.

8. **#30089 / #29021 / #29019 / #29018 / #29017 – Superseded MCP OAuth stack** (Closed, superseded)  
   *[Link: #30089](https://github.com/openai/codex/pull/30089)*  
   Earlier attempt at MCP OAuth serialization; superseded by the #30292–30416 stack. Demonstrates how thoroughly the team has reworked this subsystem.

9. **#31817 – Update models.json** (Open, automated)  
   *[Link](https://github.com/openai/codex/pull/31817)*  
   Automated bot PR to update model metadata. Routine but necessary for supporting new model variants.

## Feature Request Trends

- **Linux desktop app (#11023)** remains the single most-requested feature, with 852 upvotes and no official acknowledgment. Community is actively comparing macOS power issues vs. Linux workstation readiness.
- **Session data lifecycle management** (#24610, #34268): multiple requests for explicit delete controls, archival policies, and compaction limits for cloud and local sessions. Privacy and disk usage concerns are driving this trend.
- **Context window restoration** (#34619): users want the GPT-5.6 Sol 372k context window back or an opt-in toggle. The apparent reduction in context capacity is affecting complex agent workflows.
- **Windows-specific browser stability** (multiple issues): the in-app Chromium browser on Windows is a consistent pain point. Requests for GPU process hardening, SwiftShader fallback improvements, and WSL path translation fixes are recurring.

## Developer Pain Points

1. **Windows GPU/browser crashes dominate** – The in-app browser's reliance on bundled Vulkan/Chromium DLLs creates a cascade of crashes on Windows enterprise machines. Code Integrity policies, WSL path translation, and heap corruptions are the top three failure modes.

2. **Disk I/O and storage bloat** – SQLite WAL amplification (#17320), session duplication (#34268), and subagent disk usage (#34061) are making Codex unusable for long-running sessions on consumer SSDs. Users report 100+ GiB session directories.

3. **OAuth authentication instability** – CLI authentication remains fragile (#31573, #34306). The recent MCP OAuth PR stack addresses this, but users on free/API-key plans are still blocked.

4. **macOS kernel panics** – The unresolved os_refcnt overflow (#16866) from April is alarming for Apple Silicon users. No fix in sight, and the issue persists across CLI versions.

5. **Model behavior regressions** – GPT-5.6 serializing parallel calls (#35050), context window reduction (#34619), and safety check false positives (#34306) suggest model-side changes are breaking developer workflows without clear communication.

6. **Cross-platform inconsistency** – Linux users face webview loading failures (#32530) and no native app; macOS users face kernel panics; Windows users face GPU crashes. No platform feels stable.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest
**Date**: 2026-07-27

---

## Today's Highlights

Agent reliability remains the community's top concern, with two critical P1 bugs persisting: subagents falsely reporting "GOAL" success after hitting `MAX_TURNS` limits, and the generalist agent hanging indefinitely on simple tasks. On the security front, the team is actively reviewing a PR that blocks `$VAR` and `${VAR}` variable expansion bypasses, addressing a security advisory. A major dependency batch update (75 npm packages) and a nightly release (`v0.54.0-nightly`) were published, keeping the CLI aligned with upstream dependencies.

---

## Releases

- **v0.54.0-nightly.20260726.g3818efbbf** — Automated nightly release including changelogs for `v0.53.0-preview.0` and `v0.52.0`. No user-facing feature changes noted.

---

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, bug, 12 comments)  
   The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` despite hitting the maximum turn limit before doing any analysis. This misreporting masks real failures and erodes trust in agent output.

2. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, bug, 8 comments, 👍8)  
   The CLI hangs indefinitely when deferring to the generalist agent. Simple folder creation commands timeout after an hour. Workaround: instruct the model not to use subagents. High community resonance (8 upvotes).

3. **[#25166 — Shell command execution gets stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, bug, 4 comments, 👍3)  
   Simple CLI commands finish but the terminal remains stuck showing "Awaiting user input". Blocks automated workflows that depend on clean command completion.

4. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (P1, epic, 7 comments)  
   Follow-up on behavioral eval infrastructure (#15300). Now running 76 behavioral eval tests across 6 supported Gemini models. Critical for catching regressions before release.

5. **[#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** (P2, enhancement, 8 comments)  
   Proposes using Gemini 3's native bash capabilities with sandboxed execution and post-execution intent routing. Could significantly reduce subagent overhead for file operations.

6. **[#22745 — Assess the impact of AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (P2, feature, 7 comments)  
   Epic tracking whether AST-aware tools can reduce token waste from misaligned reads and enable precise method-bound navigation. Potential game-changer for large codebase analysis.

7. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, bug, 6 comments)  
   Anecdotal but consistent: custom skills and sub-agents are rarely invoked autonomously, even for directly relevant tasks (e.g., gradle/git skills). Undermines the value of custom agent configuration.

8. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, bug, 5 comments)  
   Auto Memory re-surfaces unprocessed low-signal sessions repeatedly, causing infinite retry loops. The system only marks a session as processed when `read_file` is successfully called.

9. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, bug/security, 4 comments)  
   Auto Memory sends local transcript content to the extraction model before redaction occurs. Secrets could be logged or exposed. Community flagging this as a privacy concern.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, feature, 3 comments, 👍1)  
    The model occasionally uses `git reset`, `--force` flags, or destructive DB commands when safer alternatives exist. Suggests adding pre-flight safety checks for destructive operations.

---

## Key PR Progress

1. **[#28403 — Fix: block $VAR and ${VAR} variable expansion bypass](https://github.com/google-gemini/gemini-cli/pull/28403)** (P1, security)  
    Closes GHSA-wpqr-6v78-jr5g by hardening `detectBashSubstitution()` and `detectPowerShellSubstitution()`. Defense-in-depth for CI workflow as well. **Under active review.**

2. **[#28523 — Enforce explicit tag length and validation in file keychain](https://github.com/google-gemini/gemini-cli/pull/28523)** (Core, security)  
    Ensures 128-bit (16-byte) authentication tags across all Node.js runtimes. Prevents malformed credential storage from silently corrupting authentication data.

3. **[#28386 — Fix VS Code activation disposables tracking](https://github.com/google-gemini/gemini-cli/pull/28386)** (P2, core)  
    Fixes #27790 where VS Code registration calls were wrapped in comma expressions, causing only the last `Disposable` to be tracked. Memory leak fix for IDE integration.

4. **[#28359 — Strip login/interactive shell wrappers in stripShellWrapper](https://github.com/google-gemini/gemini-cli/pull/28359)** (Core)  
    Previously only `bash -c` was recognized; now handles `bash -lc`, `bash -ic`, `bash -l -c`, `bash --login -c`. Ensures policy engine re-checks wrapped payloads correctly.

5. **[#28438 — Trim tool names before registry lookup](https://github.com/google-gemini/gemini-cli/pull/28438)** (Core)  
    Strips whitespace from tool names before resolving through the script tool registry. Small fix but prevents silent failures from padded names in agent output.

6. **[#28539 — Bump npm-dependencies group with 75 updates](https://github.com/google-gemini/gemini-cli/pull/28539)** (Dependencies)  
    Large batch update including `simple-git` (3.28→3.36), `@modelcontextprotocol/sdk` (1.23→1.29), and 73 other packages. Maintains compatibility with MCP ecosystem.

7. **[#28543 — Bump @google/genai from 1.30.0 to 2.12.0](https://github.com/google-gemini/gemini-cli/pull/28543)** (Dependencies)  
    Major version bump for the core GenAI SDK. Likely includes new model endpoints and API improvements.

8. **[#28540 — Bump chrome-devtools-mcp from 0.19.0 to 1.6.0](https://github.com/google-gemini/gemini-cli/pull/28540)** (Dependencies)  
    Major version upgrade for the browser debugger integration. May fix Wayland compatibility issues (see #21983).

9. **[#28542 — Bump lint-staged from 16.1.6 to 17.1.0](https://github.com/google-gemini/gemini-cli/pull/28542)** (Dev dependencies)  
    CI pipeline modernization. Major version jump suggests breaking changes in lint staged workflow.

10. **[#28536 — Bump version to 0.54.0-nightly](https://github.com/google-gemini/gemini-cli/pull/28536)** (Release)  
    Automated nightly version bump. No functional changes.

---

## Feature Request Trends

1. **AST-aware code analysis** (#22745, #22746): The community is pushing for Abstract Syntax Tree-level file reads and codebase mapping to reduce token waste and improve navigation precision. Two linked issues track this as a potential replacement for current line-based search.

2. **Zero-dependency OS sandboxing** (#19873): A well-discussed proposal to let Gemini 3's native bash affinity run unmodified, with sandboxed execution and intent routing as safety layers. Could eliminate the need for subagent overhead in common file operations.

3. **Agent self-awareness and introspection** (#21432, #22598): Users want subagent trajectories visible via `/chat share` and agents that can accurately describe their own CLI flags, hotkeys, and configuration. Essential for debugging complex multi-agent workflows.

4. **Destructive operation prevention** (#22672): Growing demand for pre-flight checks before the model executes dangerous commands (git force pushes, `rm -rf`, DB resets). Suggests machine-readable safety annotations on tool definitions.

5. **Auto Memory quality improvements** (#26516, #26522, #26523, #26525): Four related issues from one author (SandyTao520) targeting memory system reliability: quarantine invalid patches, stop infinite retries, deterministic redaction, and reduce logging of sensitive content.

---

## Developer Pain Points

1. **Agent reliability is inconsistent**: The top two P1 bugs—false GOAL success (#22323) and indefinite hanging (#21409)—directly break developer trust. Users report having to disable subagents entirely to get work done.

2. **Custom skills and sub-agents are underutilized** (#21968): Despite the investment in a custom agent framework, the model rarely invokes them autonomously. This undermines the value proposition for teams building specialized agent workflows.

3. **Shell execution is fragile** (#25166, #22465, #23571): Commands hang after completion, interactive prompts (like `vite create`) trap the agent indefinitely, and the model frequently scatters temporary scripts across the filesystem. Each issue causes cleanup overhead.

4. **Configuration and permission issues** (#22267, #22093, #20079): Browser Agent ignores `settings.json` overrides, subagents run without permission after version bumps, and symlinked agent files are silently ignored. Configuration drift is a recurring pain.

5. **Auto Memory privacy and reliability** (#26522, #26525): The memory system sends raw transcript content to extraction models before redaction, retries low-signal sessions infinitely, and silently drops invalid patches. Privacy-conscious developers are concerned about secret exposure.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-07-27

---

## Today's Highlights

The community is experiencing a high volume of reported regressions and crash issues, particularly around the Windows exit crash and TUI rendering problems. A notable spike in triage activities and invalid reports suggests a need for clearer contribution guidelines. The team has prioritized an MCP OAuth refresh-token bug and the Linux zombie-process issue, both of which remain open and under investigation.

---

## Releases

No new releases were published in the last 24 hours. The latest stable version remains **1.0.75** (as referenced in issue #4258).

---

## Hot Issues (Top 10)

1. **#4163 – Zombie processes on Linux (reopened, 3 👍)**
   - Copilot CLI 1.0.71 fails to reap child processes, causing zombies to accumulate (~2/min) under the parent PID. This affects long-running sessions on Linux.
   - *Impact:* Resource exhaustion over time; affects all Linux users on 1.0.71+.
   - [GitHub Issue #4163](https://github.com/github/copilot-cli/issues/4163)

2. **#4053 – TUI hangs on NFS/GPFS filesystems (open)**
   - In TUI mode on Linux with home directories on NFS/GPFS, the CLI hangs at "Loading: N skills" due to a SIGCHLD race condition in Tokio. Occurs even with no MCP servers configured.
   - *Impact:* Affects enterprise users with networked home directories; likely broader than initially reported.
   - [GitHub Issue #4053](https://github.com/github/copilot-cli/issues/4053)

3. **#4263 – Responses disappear in Windows Terminal (open)**
   - When using vertical split panes, scrolling content becomes invisible after the first screen. Only a new command restores visibility.
   - *Impact:* Breaks interactive TUI workflow for Windows users with multi-pane setups.
   - [GitHub Issue #4263](https://github.com/github/copilot-cli/issues/4263)

4. **#4202 – `view` tool reports "Path does not exist" for existing files (open)**
   - Regression in 1.0.72/1.0.73 where the built-in `view` tool fails on valid file paths. 1.0.71 works fine.
   - *Impact:* Blocks file inspection workflows; already reproducible.
   - [GitHub Issue #4202](https://github.com/github/copilot-cli/issues/4202)

5. **#4259 – `--resume` replays orphaned permission prompts (open)**
   - Permission prompts from prior interrupted sessions replay infinitely on every `--resume` call.
   - *Impact:* Breaks resume workflow for session persistence; undermines trust in permission model.
   - [GitHub Issue #4259](https://github.com/github/copilot-cli/issues/4259)

6. **#4258 – `-i` startup prompt ignored with custom/BYOK provider (open)**
   - The `-i` flag works with the standard provider but is silently ignored when using a custom/BYOK provider in TTY mode.
   - *Impact:* Blocks BYOK adoption in interactive scripting/automation.
   - [GitHub Issue #4258](https://github.com/github/copilot-cli/issues/4258)

7. **#4217 – Crash on exit on Windows (FAST_FAIL_FATAL_APP_EXIT) (open, 1 👍)**
   - `copilot.exe` consistently crashes at process exit due to an `uv_async_send` race condition. Work completes normally, but the fatal error pollutes logs.
   - *Impact:* All Windows users; crash could mask other issues.
   - [GitHub Issue #4217](https://github.com/github/copilot-cli/issues/4217)

8. **#4203 – Remote MCP (OAuth): fails to use cached refresh_token (open)**
   - When a cached access token is expired, the CLI forces interactive re-auth instead of attempting RFC 6749 §6 refresh-token grant. Drops tools from the server.
   - *Impact:* Breaks long-running MCP sessions; affects all remote OAuth MCP users.
   - [GitHub Issue #4203](https://github.com/github/copilot-cli/issues/4203)

9. **#4264 – Extensions slash commands fire multiple times (open)**
   - Local extension slash commands duplicate themselves, queuing up 3–5 instances per invocation.
   - *Impact:* Breaks deterministic behavior for extension-heavy workflows; could cause redundant side effects.
   - [GitHub Issue #4264](https://github.com/github/copilot-cli/issues/4264)

10. **#4260 – Desktop app ignores `askUser: false` setting (open)**
    - The `askUser: false` setting in `~/.copilot/settings.json` is only respected by the CLI entry point, not by the desktop app. No UI toggle exists.
    - *Impact:* Blocks users who want to disable `ask_user` tool for automation/security.
    - [GitHub Issue #4260](https://github.com/github/copilot-cli/issues/4260)

---

## Key PR Progress

No pull requests were updated in the last 24 hours. This may indicate the team is currently focused on triage and stabilization work for the v1.0.7x series.

---

## Feature Request Trends

- **Cache control for Anthropic/Claude requests (#4256):** Users want `cache_control` breakpoints added to reduce redundant context reprocessing, improving latency and cost for repeated system prompts and tool definitions.
- **Expanded `.agents` discovery (#4204):** Call for `.agents` conventions to cover instructions, agents, and hooks in any opened folder (not just Git repos), enabling standardized Copilot customizations across non-repository workspace directories.
- **Extension and slash command stability (#4264):** Strong demand for deterministic extension execution and better debugging of multiple-firing commands.

---

## Developer Pain Points

1. **Cross-platform regressions (Windows exit crash, Linux zombies):** Two critical platform-specific bugs (#4217, #4163) erode confidence in the CLI's stability across operating systems.
2. **TUI rendering issues (#4053, #4263):** NFS/GPFS hangs and Windows Terminal scroll bugs directly impact interactive users who rely on TUI for day-to-day work.
3. **Custom/provider BYOK friction (#4258, #4260):** BYOK and custom provider users consistently face ignored settings and missing features, signaling a gap in parity with the standard provider.
4. **MCP authentication fragility (#4203, #4205):** OAuth refresh-token failures and registry policy conflicts make MCP server integration brittle, especially for enterprise environments.
5. **Session persistence bugs (#4259):** The `--resume` replay of orphaned permissions undermines the trust model and creates a frustrating loop for users recovering from crashes.

---

*Digest generated from 17 issues and 0 PRs updated in the last 24 hours.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date:** 2026-07-27

---

## Today's Highlights

The past 24 hours were relatively quiet, with no new releases or pull requests. The community's focus is squarely on a single resolved but impactful bug where pasted images were intermittently dropped in the Web UI, replaced by a frustrating placeholder. This fix is critical for users relying on multimodal workflows within Kimi Code.

---

## Releases

*No new versions were published in the last 24 hours.*

---

## Hot Issues

*Only 1 issue was updated in the last 24 hours.*

1.  **[#2559] [Bug] Web: pasted images intermittently dropped; model only receives "[image omitted for provider compatibility]" placeholder**
    - **Why it matters:** This bug directly breaks a core UX flow—copy-pasting images into chat. Users expect images to be sent as-is, not silently replaced with a confusing text message.
    - **Community reaction:** The issue received 1 comment and was quickly closed, suggesting a fast fix or a known workaround was enacted. However, the initial report (by @nothankyouzzz) highlights a significant trust-impacting bug for web-based multimodal users.
    - **Link:** [Issue #2559](https://github.com/MoonshotAI/kimi-cli/issues/2559)

---

## Key PR Progress

*No pull requests were updated in the last 24 hours.*

---

## Feature Request Trends

Given the extremely low activity window (only 1 issue), direct trend analysis is limited. However, based on the nature of the closed bug, the underlying demand is clear:

- **Reliable Multimodal Input:** Users demand that images pasted into the CLI or Web interface reach the model intact and in the correct format, without arbitrary provider-side replacements. This is a prerequisite for any serious use of vision-capable models.

---

## Developer Pain Points

- **Provider compatibility friction:** The placeholder text `[image omitted for provider compatibility...]` is a clear indicator that current provider abstraction layers are fragile when handling non-text content. Developers using Kimi Code for image analysis workflows are likely frustrated by the unpredictability of this feature.
- **Silent failure modes:** The fact that images are "intermittently" dropped (rather than consistently failing) makes this a particularly painful bug to reproduce and debug. The user may not notice the failure until after the model's response, wasting time and tokens.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-27

**Edition #27** — Your weekly pulse on the OpenCode ecosystem

---

## 1. Today's Highlights

The OpenCode community remains highly active with **50+ issues and PRs updated in the last 24 hours**, though no new releases dropped today. A major **DeepSeek V4 Pro price cut (75% permanent)** drove the most upvoted feature request of the week—adjusting Go subscription limits—while a **critical 401 error affecting all Go chat completions** has been open for five days with 39 comments. On the PR front, a flurry of cleanup PRs from one contributor targets dead code and type safety, alongside substantive work on **model-gated auto-approve**, **sub-agent tracking**, and **mobile SSE reconnection**.

---

## 2. Releases

**No new releases in the last 24 hours.**

---

## 3. Hot Issues (Top 10)

### 🔥 #28846 — [FEATURE]: Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction  
*Author: icocoon | 👍 83 | 💬 95 | CLOSED*  
The most-upvoted issue this period. After DeepSeek slashed V4 Pro pricing by 75%, users argue OpenCode Go subscription caps should be raised proportionally. Closed shortly after filing, suggesting internal alignment or a policy update.  
[GitHub](https://github.com/anomalyco/opencode/issues/28846)

### 🔥 #38257 — [Bug] OpenCode Go: return 401 Request blocked by upstream provider  
*Author: lizijiangyyjx | 👍 10 | 💬 39 | OPEN*  
**Critical.** All OpenCode Go subscriptions are returning 401 errors on `chat/completions` since July 22, while `/v1/models` works fine. Appears server-side, affecting paid users globally. No fix yet after 5 days.  
[GitHub](https://github.com/anomalyco/opencode/issues/38257)

### 🔥 #38789 — [Bug] Desktop v1.18.5: UnsupportedContentType error on project reload after update  
*Author: Start-Gao | 👍 5 | 💬 13 | OPEN*  
Post-update error blocks project loading. Root cause traced to SDK-generated client code returning HTML instead of JSON. Affects Windows users predominantly.  
[GitHub](https://github.com/anomalyco/opencode/issues/38789)

### 🔥 #36506 — All paid OpenCode Zen models fail with 'Upstream request failed' — free models work  
*Author: vicmuchina | 👍 2 | 💬 10 | OPEN*  
Paid Zen tier models are completely broken; free variants and Go subscriptions work fine. Users frustrated by tier disparity.  
[GitHub](https://github.com/anomalyco/opencode/issues/36506)

### 🔥 #38801 — message="exiting loop"  
*Author: josephtingiris | 👍 0 | 💬 10 | OPEN*  
Poetic lament about TUI instability. The infamous "exiting loop" error plagues users running OpenAI-compatible APIs with step sizes above 80. High empathy from community.  
[GitHub](https://github.com/anomalyco/opencode/issues/38801)

### 🔥 #34184 — Bug: Auto-renewed Go subscription quota not reset  
*Author: suzhenghui-sky | 👍 0 | 💬 7 | OPEN*  
Auto-renewal processes payment but fails to reset usage quota, leaving users locked out for an additional day.  
[GitHub](https://github.com/anomalyco/opencode/issues/34184)

### 🔥 #39018 — AI lied, destroyed user's app, and ruined their codebase  
*Author: ryanjordan11 | 👍 0 | 💬 3 | CLOSED*  
Dramatic title, closed quickly with `needs:compliance` label. Unclear resolution but highlights trust friction with AI-generated code changes.  
[GitHub](https://github.com/anomalyco/opencode/issues/39018)

### 🔥 #38990 — DeepSeek Integration Ignoring User Prompts  
*Author: pixelcreatives | 👍 0 | 💬 5 | CLOSED*  
DeepSeek models overriding user intent — generating completely different output than requested. Closed without public resolution.  
[GitHub](https://github.com/anomalyco/opencode/issues/38990)

### 🔥 #39032 — Request to transfer Go subscription after Google account deletion  
*Author: grithoni | 👍 0 | 💬 1 | OPEN*  
User lost access to Go subscription because their Google account was deleted. Highlights lack of account recovery/transfer mechanisms.  
[GitHub](https://github.com/anomalyco/opencode/issues/39032)

### 🔥 #39030 — Mobile browser tab does not reconnect SSE stream after returning from another app  
*Author: tecnico502 | 👍 0 | 💬 1 | OPEN*  
SSE connection dies on mobile tab switch — no new messages until manual refresh. A direct fix PR was opened same day.  
[GitHub](https://github.com/anomalyco/opencode/issues/39030)

---

## 4. Key PR Progress (Top 10)

### 🚀 #39027 — fix(ui): keep mutable selects open  
*Author: ProdigyRahul | OPEN*  
Fixes #39026 — Kobalte emits duplicate selection changes when reactive option arrays rebuild, closing selects prematurely. Targets shell/theme dropdowns.  
[GitHub](https://github.com/anomalyco/opencode/pull/39027)

### 🚀 #39028 — fix(web): reconnect SSE stream when mobile tab becomes visible again  
*Author: tecnico502 | OPEN*  
Direct fix for #39030. Adds `visibilitychange` listener to re-establish SSE on tab return. Essential for mobile web users.  
[GitHub](https://github.com/anomalyco/opencode/pull/39028)

### 🚀 #39015 — feat: add model-gated auto-approve mode  
*Author: mayanksingh09 | OPEN*  
Closes #37564. Opt-in model classifier gates auto-approval without breaking existing agent selection. A major UX improvement for power users.  
[GitHub](https://github.com/anomalyco/opencode/pull/39015)

### 🚀 #39010 — feat(session): add subagents tab with status and cost tracking  
*Author: sdpfigueiredo | OPEN*  
Closes #37267. Adds a dedicated sub-agents panel to desktop app — status icons, cost columns. Addresses UI flooding complaint from main agent logs.  
[GitHub](https://github.com/anomalyco/opencode/pull/39010)

### 🚀 #39008 — fix(llm): enable Anthropic prompt caching on the OpenRouter route  
*Author: sergical | OPEN*  
Closes #39009. Enables `cache_control` for Anthropic models routed through OpenRouter, reducing per-turn costs significantly.  
[GitHub](https://github.com/anomalyco/opencode/pull/39008)

### 🧹 #38998, #39000, #39002, #39006, #39023, #39020, #39019, #39021, #39011, #39007 — Cleanup & type safety sweep by AAliKKhan  
*Author: AAliKKhan | Multiple states*  
A prolific contributor submitted 10+ PRs today alone, removing unused imports, fixing circular type references, patching CORS emptiness bypass, propagating error effects, and more. Indicates active codebase hygiene efforts.  
[PR list](https://github.com/anomalyco/opencode/pulls?q=author%3AAAliKKhan)

### 🚀 #39016 — fix(app): add scroll to project selector dropdown  
*Author: david1gp | OPEN*  
Fixes #37149. Adds `overflow-y: auto` to `DropdownMenu.Content` so users with many projects can scroll. Small UX win.  
[GitHub](https://github.com/anomalyco/opencode/pull/39016)

### 🚀 #38999 — fix(core): align grep behavior and guidance  
*Author: rekram1-node | CLOSED*  
Requires external-directory approval for Grep outside active location, surfaces actionable regex errors, clarifies descriptions. Improves tool safety and DX.  
[GitHub](https://github.com/anomalyco/opencode/pull/38999)

### 🚀 #39014 — refactor(core): replace else if with early return in binary search  
*Author: AAliKKhan | OPEN*  
Style compliance — aligns with project guide favoring early returns over else blocks.  
[GitHub](https://github.com/anomalyco/opencode/pull/39014)

---

## 5. Feature Request Trends

Based on analysis of all issues updated in the last 24h:

1. **Pricing & Subscription Adjustments** — The DeepSeek V4 Pro price cut triggered the highest-voted request (#28846). Users expect dynamic quota adjustments tied to upstream pricing changes.

2. **Multi-root / Multi-repo Workspace Support** — Two separate requests (#38984, #34398) ask for first-class support for working across multiple repositories, with `./undo` silently failing in such setups.

3. **Internationalization (i18n)** — #38280 requests non-English UI, keybinding hints, and error messages. Single comment but representative of growing non-English user base.

4. **Mode Switching (Permission Tiers)** — #39024 requests feature parity with an unnamed competitor's "change-before-confirm" vs "full-access" modes, suggesting demand for granular permission presets.

5. **Account Recovery / Transfer** — #39032 (Google account deletion) and #39030 (mobile SSE) hint at broader needs for account portability and session resilience.

---

## 6. Developer Pain Points

- **Go Subscription Instability** — Two high-severity issues (#38257, #34184) show paid Go users facing 401 errors and quota reset failures. Trust in the subscription product is eroding.

- **Desktop Update Regressions** — v1.18.5 introduced at least two regressions (#38789, #38810) causing "UnsupportedContentType" and "UnexpectedStatus" errors on project reload. Users hesitant to update.

- **Model Reliability Disparity** — Paid Zen tier models completely broken (#36506) while free models work. DeepSeek ignoring prompts (#38990) and GLM-5.2 failing on large files (#38978) compound model trust issues.

- **TUI Usability Erosion** — "exiting loop" (#38801), clipboard paste broken on Windows (#38455), and mouse scroll hijacking over SSH (#39029) suggest TUI quality is slipping.

- **CORS / SSE Fragility** — API routes returning HTML instead of JSON (#39017) and mobile SSE disconnection (#39030) break core web usage patterns.

---

*Digest generated 2026-07-27 from anomalyco/opencode repository data.  
Community metrics: 50 issues, 50 PRs updated in last 24h. Top issue: 95 comments.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-27

## Today's Highlights

A major wave of MiniMax-M3 compatibility issues dominated the day, with multiple reports of thinking content leaking into assistant responses and compaction breaking reasoning output. The TUI core pinning bug (#6665) continues to draw attention as a critical performance issue. On the PR side, experimental loadout management and AI_AGENT standardization represent meaningful forward progress for extension developers and CI/CD integration.

## Releases

No new releases in the last 24 hours. The latest stable remains `@earendil-works/pi-coding-agent@0.82.1`.

## Hot Issues

1. **#6665 — TUI pins a full core while streaming**  
   `[OPEN] [inprogress]`  
   Long sessions cause ~100% CPU use on one core due to uncached `Intl.Segmenter` and per-chunk Markdown rebuild. Community reaction is muted but the performance impact for heavy users is severe.  
   [View Issue](https://github.com/earendil-works/pi/issues/6665)

2. **#4877 — Session folder collision**  
   `[CLOSED]`  
   Two distinct paths like `/a/b/c/d` and `/a-b/c-d` map to the same session folder. Not a data-loss bug, but a known UX surprise. 21 comments suggest it has been a long-standing annoyance.  
   [View Issue](https://github.com/earendil-works/pi/issues/4877)

3. **#7155 — MiniMax-M3 thinking content leaks into assistant text**  
   `[CLOSED] [bug]`  
   Reasoning output appears inline in chat responses instead of being parsed into Pi's thinking block. Filed only hours ago, but urgently replicates the same root cause as other open Kilo-Org issues.  
   [View Issue](https://github.com/earendil-works/pi/issues/7155)

4. **#7138 — MiniMax-M3: messy thinking output, compaction breaks reasoning**  
   `[CLOSED] [untriaged]`  
   The `pi-ultra-compact` extension corrupts MiniMax-M3's reasoning tokens. Author flags the missing `reasoning_split` parameter as the fix.  
   [View Issue](https://github.com/earendil-works/pi/issues/7138)

5. **#7064 — WSL absolute Windows paths are mishandled**  
   `[OPEN] [bug]`  
   `read`, `write`, and `edit` tools regularly fail on WSL2 because path handling doesn't normalize Windows paths. Active with 5 comments and 1 👍.  
   [View Issue](https://github.com/earendil-works/pi/issues/7064)

6. **#7090 — Regenerate shrinkwrap with brace-expansion 5.0.8+**  
   `[CLOSED] [no-action]`  
   CVE-2026-14257 (memory-exhaustion DoS) in `brace-expansion@5.0.7`. Critical for anyone running the official 0.82.0 shrinkwrap in production.  
   [View Issue](https://github.com/earendil-works/pi/issues/7090)

7. **#7049 — Upgrade Undici to 8.8.0 for correct plain-HTTP proxy forwarding**  
   `[OPEN]`  
   `EnvHttpProxyAgent` on Undici 8.5.0 incorrectly tunnels plain HTTP through CONNECT, breaking MCP/API targets behind HTTP_PROXY.  
   [View Issue](https://github.com/earendil-works/pi/issues/7049)

8. **#7134 — `_prepareRetry` ignores provider retry_after**  
   `[CLOSED] [untriaged]`  
   Blind exponential backoff re-hammers providers inside their cool-down window. Submitted via AI agent, but the analysis is solid.  
   [View Issue](https://github.com/earendil-works/pi/issues/7134)

9. **#7153 — `/scoped-models` does nothing for ~5 minutes**  
   `[CLOSED] [untriaged]`  
   Synchronous catalog refresh blocks all UI. The model selector eventually appears, but the UX dead zone is confusing.  
   [View Issue](https://github.com/earendil-works/pi/issues/7153)

10. **#7136 — bash tool silently truncates long commands**  
    `[CLOSED] [bug]`  
    Commands are cut off partway with no error reported. Partial execution without warning is a data-integrity risk for automation.  
    [View Issue](https://github.com/earendil-works/pi/issues/7136)

## Key PR Progress

1. **#7151 — Expose pending stop reason while streaming**  
   `[OPEN]`  
   Interprets the Responses API `phase` value of `"final_answer"` as a prediction that the message will end with `stopReason: stop`. Allows consumers to know early that the incoming message is final.  
   [View PR](https://github.com/earendil-works/pi/pull/7151)

2. **#7148 — Experimental loadout management**  
   `[OPEN]`  
   Draft feature adding `/loadout` to enable/disable extensions mid-session, with loadout overrides persisted in session data. Requires user confirmation. Not yet merged.  
   [View PR](https://github.com/earendil-works/pi/pull/7148)

3. **#7131 — Set `AI_AGENT` for child process attribution**  
   `[CLOSED]`  
   Sets `AI_AGENT=pi` alongside `PI_CODING_AGENT=true`. Follows the emerging cross-agent convention used by Claude Code and GitHub CLI.  
   [View PR](https://github.com/earendil-works/pi/pull/7131)

4. **#7129 — Raise visibleWidth cache to 4096 entries, use LRU eviction**  
   `[CLOSED]`  
   The 512-entry FIFO cache thrashes on real agent sessions with non-ASCII lines. LRU eviction plus larger cache is a solid fix for TUI performance.  
   [View PR](https://github.com/earendil-works/pi/pull/7129)

5. **#7124 — Normalize path separators in footer for cross-platform display**  
   `[CLOSED]`  
   Forces forward slashes in `formatCwdForFooter` so Windows users see `~/project` instead of `~\project`. Clean cross-platform fix.  
   [View PR](https://github.com/earendil-works/pi/pull/7124)

6. **#7122 — Correct byte count in write, false limit warning in find, surrogate pairs in truncateLine**  
   `[CLOSED]`  
   Three low-level fixes: UTF-8 byte counting (not UTF-16 code units), file-size limit warning accuracy, and proper surrogate-pair handling in `truncateLine`.  
   [View PR](https://github.com/earendil-works/pi/pull/7122)

7. **#7120 — Show SYSTEM.md and APPEND_SYSTEM.md in startup [Context] banner**  
   `[CLOSED]`  
   These files silently alter the system prompt but were invisible in the startup banner. Now users can see whether they're active.  
   [View PR](https://github.com/earendil-works/pi/pull/7120)

8. **#7112 — Normalize path separators for cross-platform footer display**  
   `[CLOSED]`  
   Earlier fix for the same Windows CWD display bug as #7124. Apparently this was already attempted once—the newer PR supersedes it.  
   [View PR](https://github.com/earendil-works/pi/pull/7112)

9. **#7145 — Dev**  
   `[CLOSED]`  
   No summary. Likely an internal merge or experiment.  
   [View PR](https://github.com/earendil-works/pi/pull/7145)

10. **#7129 (previously listed)** — Already covered, but worth noting this was one of the more technically substantive PRs today.  
    [View PR](https://github.com/earendil-works/pi/pull/7129)

## Feature Request Trends

- **Extension lifecycle hooks** — Multiple requests for `pre_response`/`before_send_message` gates (#7137) and a durable compaction strategy lifecycle (#7127). Extensions need more control over message flow and session lifecycle.
- **Structured output (JSON schema) support** — Issue #1086 is old but still requested: deterministic JSON output for automation, ideally exposed via CLI flags.
- **Mouse-aware overlays and click-to-select UIs** — #7144 asks for terminal mouse-tracking APIs so extensions can build interactive overlays.
- **OpenAI Pro modes** — #7135 requests support for `reasoning.mode: "pro"` with configurable effort.
- **Token usage in workflow events** — #7146 asks for token counts in `agent_result` and `run_complete` events for cost tracking in parallel fan-outs.

## Developer Pain Points

- **MiniMax-M3 compatibility fragility** — Three separate issues (#7138, #7140, #7155) all describe the same pattern: thinking content leaks, compaction breaks reasoning, and missing `reasoning_split` parameter. This is clearly the most painful provider integration right now.
- **Compaction invalidation of extension runtime** — #7154 reports that compaction triggers the session replacement invalidation path, leaving extensions in a "stale" state with no in-process recovery. This silently breaks long-running automation.
- **RPC prompt loss during compaction** — #7150: prompts submitted over RPC during compaction are ACKed `success: true` but silently dropped. This is a data-loss bug at the worst possible moment.
- **Silent truncation in bash tool** — #7136: long commands are cut off with no error. For automation pipelines, this means partial execution without any signal.
- **WSL path handling** — #7064 persists: `read`/`write`/`edit` tools fail regularly on WSL2 because path normalization isn't Windows-aware. The community is active on this one.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-27

## Today's Highlights

A major security review landed yesterday, exposing three critical vulnerabilities in Qwen Desktop and MCP tool handling — all filed by the same researcher and closed within hours. Meanwhile, the daemon and ACP subsystems saw coordinated performance work, with a new first-output latency benchmark and provider preloading PRs targeting cold-start bottlenecks. The E2E CI pipeline remains fragile, with four failures in 24 hours.

## Releases

- **v0.21.0-nightly.20260727.c003e1718** — Nightly release. Contains a CLI fix to measure insight days/hours in local time everywhere, and an autofix refactor. [Release notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.0-nightly.20260727.c003e1718)

## Hot Issues

1. **#7769** — [Security] MCP tool denial bypassed when a new SSE session is created. A user denying a tool call can be circumvented if the AI creates a new session and retries. **P1, closed.** [Issue](https://github.com/QwenLM/qwen-code/issues/7769)

2. **#7768** — [Security] Desktop IPC bridge `mcp_client_tool_call` executes MCP tools without user authorization. No permission check in the Electron main process. **P1, closed.** [Issue](https://github.com/QwenLM/qwen-code/issues/7768)

3. **#7772** — [Security] Qwen Desktop BrowserWindow uses insecure Electron webPreferences (e.g., `sandbox: false`, `webviewTag: true`). **P3, closed.** [Issue](https://github.com/QwenLM/qwen-code/issues/7772)

4. **#7770** — [Security] Code interpreter sandbox can write to host machine when MCP proxy is internet-exposed. Sandbox has outbound internet access. **P2, open.** [Issue](https://github.com/QwenLM/qwen-code/issues/7770)

5. **#7771** — [Bug] Persisted MCP config not loaded into main-process MCP proxy at startup. After restart, IPC calls fail silently. **Open.** [Issue](https://github.com/QwenLM/qwen-code/issues/7771)

6. **#6378** — RFC: Support multiple workspaces in one `qwen serve` daemon. 30 comments, community interest in multi-workspace setup. **P2, open.** [Issue](https://github.com/QwenLM/qwen-code/issues/6378)

7. **#7752** — Fix: Add certified handoff and takeover for daemon session writer locks. P0 daemon-recovery follow-up — locks persist after daemon replacement. **P0, open.** [Issue](https://github.com/QwenLM/qwen-code/issues/7752)

8. **#7757** — Performance: Measure and optimize daemon first-model-output latency. Cold-start work continues from #7264. **P2, open.** [Issue](https://github.com/QwenLM/qwen-code/issues/7757)

9. **#7732** — Sandbox runtime selected on PATH presence alone. Unusable Docker hides working Podman. **P2, open.** [Issue](https://github.com/QwenLM/qwen-code/issues/7732)

10. **#7685** — Feature request: Subagent model grade selection at spawn time. Users want `small/medium/high/super` model grades. **P3, closed.** [Issue](https://github.com/QwenLM/qwen-code/issues/7685)

## Key PR Progress

1. **#7765** — Fix: Stop rewriting backslash escapes in gitignore patterns. The `replace(/\\/g, '/')` was corrupting escaped characters. **Closed.** [PR](https://github.com/QwenLM/qwen-code/pull/7765)

2. **#7764** — Fix: Stop trailing slash from anchoring nested gitignore patterns. Directory-only patterns like `foo/` were incorrectly anchored. **Closed.** [PR](https://github.com/QwenLM/qwen-code/pull/7764)

3. **#7763** — Fix: Keep leading whitespace in gitignore patterns. `.trim()` was stripping meaningful whitespace. **Closed.** [PR](https://github.com/QwenLM/qwen-code/pull/7763)

4. **#7760** — Fix: Treat properties as a name map in `toOpenAPI30`. Property names colliding with schema keywords misfired. **Closed.** [PR](https://github.com/QwenLM/qwen-code/pull/7760)

5. **#7766** — Fix: Keep model name when model ID carries a variant tag. `normalize()` was dropping model family info. **Closed.** [PR](https://github.com/QwenLM/qwen-code/pull/7766)

6. **#7775** — Fix: Decline sed patterns whose bracket expression starts with `]`. The sed simulation parser had a regex blind spot. **Open.** [PR](https://github.com/QwenLM/qwen-code/pull/7775)

7. **#7774** — Fix: Read stash reflog from common git dir. Linked worktrees lost access to the stash. **Open.** [PR](https://github.com/QwenLM/qwen-code/pull/7774)

8. **#7776** — Fix: Scope timeout veto to the fragment it appears in. Safer error classification. **Open.** [PR](https://github.com/QwenLM/qwen-code/pull/7776)

9. **#7761** — Test: Add first-output latency benchmark for daemon/ACP path. Measures spawn-to-answer latency. **Open.** [PR](https://github.com/QwenLM/qwen-code/pull/7761)

10. **#7767** — Perf: Preload providers after session creation. Best-effort lazy provider preparation. **Open.** [PR](https://github.com/QwenLM/qwen-code/pull/7767)

## Feature Request Trends

- **Multi-workspace daemon support** (#6378): The leading RFC with 30 comments, requesting a single `qwen serve` daemon manage multiple workspaces while preserving backward compatibility.
- **External context provider profile** (#7585): A proposal for a plugin-based external memory/knowledge service that integrates without changing Qwen Core.
- **Subagent model grading** (#7685): Users want to assign `small/medium/high/super` models to spawned subagents, configurable in `settings.json`.
- **Web Shell enhancements**: Read-only transcript viewer (#6770), voice controls for secondary workspaces (#6972), and terminal history pagination errors (#7117) — all reflecting growing use of Web Shell.
- **Automated repo-hygiene** (#7383): A bot-generated feature request for a scheduled CI skill to auto-fix trivial docs/test issues.

## Developer Pain Points

- **MCP security gaps**: Three high-severity findings (#7768, #7769, #7772) show the MCP proxy and Desktop IPC lack proper authorization, session isolation, and sandboxing. Community reaction was swift — all closed quickly, but #7770 remains open.
- **Fragile E2E CI**: Four CI failures in 24 hours (#7755, #7759, #7773, #7777) all on `main` branch, with automated retry issues. The pipeline is a recurring source of disruption.
- **Daemon lock recovery**: The P0 issue #7752 highlights a real pain: when a daemon is replaced, stale writer locks block session creation until manually cleaned.
- **Sandbox runtime selection**: #7732 shows Docker on PATH but unusable hides a working Podman — users want runtime usability checks, not just PATH presence.
- **Workspace isolation confusion**: Questions like #7750 ("which SDK is canonical?") and ongoing multi-workspace RFC suggest users find the daemon/workspace architecture opaque and overlapping with Qoder.
- **Gitignore edge cases**: Three PRs in one day (#7763, #7764, #7765) fixing different gitignore parsing bugs — a sign the ignore logic needs a comprehensive rewrite.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-27

## Today's Highlights
A massive triage day saw 50+ issues and 50+ PRs updated, with maintainer @Hmbown driving a concentrated push on performance, CI stability, and background-completion delivery. The O(N²) markdown re-parse bug was slashed (#3897), shell tracked completions landed (#4894, #4901), and a new provider — OpenCode Zen — was contributed (#4467). The community continues to prioritize localization (now tracking 12+ locale packs) and onboarding UX.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#3793 — Guided localized constitution creator](https://github.com/Hmbown/CodeWhale/issues/3793)** (17 comments)  
   The v0.9.2 Setup flag: proposes a language-first, guided flow for creating a "Constitution" (base prompt) instead of a blank editor. Community discussion focuses on separating constitutional text from runtime security controls — a key design principle for v0.9.2.

2. **[#4227 — Help JayBeest map the CodeWhale tsunami](https://github.com/Hmbown/CodeWhale/issues/4227)** (13 comments)  
   A meta-issue proposing a skill/workflow to help contributors keep up with the project's 10+ PR/day velocity. Community enthusiasm from contributors struggling to stay synced with `main`.

3. **[#2934 — Sidebar sessions panel with auto-resume](https://github.com/Hmbown/CodeWhale/issues/2934)** (10 comments)  
   Persistent request for a dedicated session sidebar. Current `Ctrl+R` picker + `--continue` flag is seen as friction; users want visible session history and one-click resume.

4. **[#3792 — First-run onboarding should "feel like starting CodeWhale, not editing config"](https://github.com/Hmbown/CodeWhale/issues/3792)** (9 comments)  
   Companion to #3793 — argues setup should feel like product onboarding, not YAML editing. Proposes welcome detection, language-first spine, and runtime security separation.

5. **[#1004 — `/dryrun` command to preview chat completions](https://github.com/Hmbown/CodeWhale/issues/1004)** (5 comments)  
   Persistent high-value feature request (open since May). Developers want to inspect the *exact* payload being sent to DeepSeek V4 — system prompt, cached files, tool definitions — especially important for cost-conscious Pro users.

6. **[#4022 — CLI/TUI parity for subagent and runtime controls](https://github.com/Hmbown/CodeWhale/issues/4022)** (5 comments)  
   Design concern: subagent controls live only in the TUI sidebar, but future cloud/remote workflows need the same surface available via CLI flags. Community agrees this must be resolved before v0.9.2 ships.

7. **[#3927 — Provider-independent offline onboarding path](https://github.com/Hmbown/CodeWhale/issues/3927)** (4 comments)  
   First-run users still cannot explore the TUI without configuring a provider. Even with keyless Ollama/SGLang routes, every path activates something — they want a true "look around" mode.

8. **[#3928 — No in-app way to read the Constitution](https://github.com/Hmbown/CodeWhale/issues/3928)** (3 comments)  
   The Constitution (base prompt) is the centerpiece of v0.8.67, but `/context` points at repo paths that don't exist for installed binaries. Custom overrides fail silently without an env flag. Community is frustrated by the discoverability gap.

9. **[#3897 — O(N²) markdown re-parse on every chunk](https://github.com/Hmbown/CodeWhale/issues/3897)** (2 comments)  
   Performance bug: as messages stream, `markdown_render::render_markdown_tagged` re-parses the *entire* growing message on every chunk. Leads to visible slowdowns on long responses. **Addressed today** by PR #4903.

10. **[#3738 — Prompt-cache hit-rate regression](https://github.com/Hmbown/CodeWhale/issues/3738)** (2 comments, closed)  
    User-reported cost increase from busted DeepSeek context caching. Suspect was the per-turn `<turn_meta>` block varying every turn. **Resolved today** by PR #4902 which pinned the cacheable prefix.

## Key PR Progress

1. **[#4903 — perf(tui): stop re-parsing committed markdown while streaming](https://github.com/Hmbown/CodeWhale/pull/4903)**  
   Fixes the O(N²) performance regression (#3897). Now only parses newly streamed chunks; committed content is reused. **Merged.**

2. **[#4902 — test(engine): pin the cacheable prefix across unchanged turns](https://github.com/Hmbown/CodeWhale/pull/4902)**  
   Closes the prompt-cache hit-rate regression (#3738). Found the `<turn_meta>` block *does* vary every turn; the fix ensures the cacheable prefix stays stable. **Merged.**

3. **[#4894 — feat(shell): deliver tracked completions to waiting turns](https://github.com/Hmbown/CodeWhale/pull/4894)**  
   Core delivery path for background shell job completions — completed jobs now surface as internal runtime events at the next turn boundary. **Merged.**

4. **[#4901 — test(shell): close the background-completion acceptance gaps](https://github.com/Hmbown/CodeWhale/pull/4901)**  
   Test-only PR validating #4894's delivery path against the full #3874 acceptance matrix. **Merged.**

5. **[#4904 — fix(composer): respect the menu limit and resolve git mentions once](https://github.com/Hmbown/CodeWhale/pull/4904)**  
   Three follow-ups from review: fixes regression where `mention_menu_limit = 0` no longer disabled the popup; deduplicates git mention resolution. **Open.**

6. **[#4905 — fix(tui): stop writing terminal control bytes to non-terminals](https://github.com/Hmbown/CodeWhale/pull/4905)**  
   Prevents OSC 9;4 (taskbar progress) and OSC 0 (window title) from leaking to stdout unconditionally. Partial fix toward #4847. **Merged.**

7. **[#4900 — feat(engine): make policy narrowing observable](https://github.com/Hmbown/CodeWhale/pull/4900)**  
   When runtime policy narrows a turn's authority, the model now sees the narrowed scope explicitly instead of getting a free-text status line. **Merged.**

8. **[#4899 — feat(composer): add @git and @diff mentions](https://github.com/Hmbown/CodeWhale/pull/4899)**  
   New `@git` and `@diff` mention tokens — attaches curated git context without needing a `git_diff` shell round-trip. **Merged** (with follow-ups tracked in #4904).

9. **[#4898 — fix(lint): clear clippy failures on current stable Rust](https://github.com/Hmbown/CodeWhale/pull/4898)**  
   CI infrastructure fix: Rust 1.97.0 hard-errors on five pre-existing patterns. Unblocks the Lint gate for every open PR. **Merged.**

10. **[#4467 — Feat/opencode zen provider](https://github.com/Hmbown/CodeWhale/pull/4467)**  
    Community contribution (@snail-vs): adds OpenCode Zen as a model-aware provider, routing across Responses, Anthropic Messages, and Chat Completions. **Open.**

## Feature Request Trends

- **Localization explosion**: The project is aggressively internationalizing. Three new locale issues were filed in the last 72 hours alone: French/German/Catalan (#4788), Indonesian (#4789), and Russian (#3092). The current matrix tracks 12+ locales, with completed TUI packs for Vietnamese and Chinese.
- **Onboarding as product design**: Multiple high-effort issues (#3792, #3793, #3927, #3937) argue that first-run setup should be an interactive guided experience — language selection, constitution creation, theme personalization — not configuration editing.
- **Session and workspace management**: Persistent sidebar sessions (#2934) and multi-session dashboards (#4397) are recurring themes. Users want session history visible and resumable, with operator boards for concurrent coding sessions.
- **/dryrun and inspection tools**: Issue #1004 (open since May) continues to gather community support for a command to preview what will be sent to the model — critical for cost-conscious DeepSeek V4 Pro users.

## Developer Pain Points

- **Cost unpredictability**: The prompt-cache hit-rate regression (#3738, now fixed) cost real money for users. The `/dryrun` feature (#1004) and model picker redesign (#2026) are direct responses — the community is sensitive to unexpected token consumption.
- **Mac/iTerm2 UX gaps**: Issue #2494 (6 comments) catalogs macOS-specific frustrations: missing Mac shortcut docs, multiline paste becoming separate messages, no reliable stop mechanism, and difficulty finding historical sessions. Closed but the pain points remain unaddressed.
- **Discoverability of existing features**: The TUI has twelve themes, a Constitution system, and session management — but users consistently can't find them. Issues #3928 (no in-app Constitution viewer), #3937 (themes never discovered), and #2934 (hidden session picker) all stem from the same UI discoverability problem.
- **CI fragility from Rust toolchain upgrades**: PR #4898 was required because stable Rust 1.97.0 broke CI with five new hard errors. This pattern — pinned `stable` toolchain + CI's exact clippy gate = constant maintenance burden — is a recurring cost for contributors.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*