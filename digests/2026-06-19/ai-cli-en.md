# AI CLI Tools Community Digest 2026-06-19

> Generated: 2026-06-19 02:44 UTC | Tools covered: 9

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

# AI CLI Developer Tools Ecosystem Report — 2026-06-19

## 1. Ecosystem Overview

The AI CLI tools landscape in mid-2026 is characterized by rapid iteration tempered by growing pains in reliability and cross-platform parity. The six major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, and the emerging open-source alternatives (Kimi Code CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI/CodeWhale)—are converging on a common feature set while diverging in architectural philosophy. MCP integration, session lifecycle management, and agent safety are universal concerns, but each tool struggles with platform-specific regressions (Windows stability, Linux glibc compatibility, macOS daemon performance) that erode developer trust. The community sentiment has shifted from "what can this tool do?" to "can I trust this tool not to lose my work, over-bill me, or corrupt my files?"

## 2. Activity Comparison — June 19, 2026

| Tool | Hot Issues | PRs Updated | Release Today | Notable Signal |
|---|---|---|---|---|
| **Claude Code** | 10 | 6 | v2.1.183 (git safety) | 53-day stale lock-fix workflow finally merged |
| **OpenAI Codex** | 10 | 10 | CLI v0.141.0, 3 alpha builds | 3-PR remote execution stack; rate-limit crisis emerging |
| **Gemini CLI** | 10 | 10 | None | MIME-type sniffing + write_file corruption fix in review |
| **GitHub Copilot CLI** | 10 | 10 | None | MCP OAuth pipeline broken; WSL2 CPU spin regression |
| **Kimi Code CLI** | 3 | 1 | None | Proxy support fix proposed; Windows packaging broken |
| **OpenCode** | 10 | 10 | None | `/goal` feature race (2 competing PRs); inotify fix landed |
| **Pi** | 10 | 10 | v0.79.7 (auto theme) | Multi-agent session switching request gaining traction |
| **Qwen Code** | 10 | 10 | None | Security-focused day: 3 sandbox/path validation flaws exposed |
| **CodeWhale** | 10 | 10 | v0.8.62 (rebrand) | Rebranding to CodeWhale; monolithic codebase refactoring push |

**Activity volume is high across established tools.** Claude Code, Codex, Gemini, Copilot CLI, and Qwen Code show sustained daily engagement. The open-source tools (OpenCode, Pi, CodeWhale) are closing the gap in community activity, with OpenCode generating the most feature-request excitement this cycle.

## 3. Shared Feature Directions

*Requirements appearing across multiple tool communities:*

| Common Feature | Affected Tools | Specific Needs |
|---|---|---|
| **MCP Authentication & Reliability** | Copilot CLI (#3838), Gemini CLI (#27664), Qwen Code (#5381, #5377), Codex (#29017-29020) | OAuth refresh serialization, atomic credential writes, retry-on-nonconnection-errors |
| **Session Lifecycle Management** | Copilot CLI (#3518), OpenCode (#27167/#32924), Pi (#5700), CodeWhale (#3285) | Persisted goals, session archival/restore, multi-agent concurrent sessions |
| **Model Routing & Cost Optimization** | OpenCode (#8456), Copilot CLI (#2896), Claude Code (#47098), Codex (#28879) | Task-based model selection, cache efficiency, token usage dashboards |
| **Agent Safety Guardrails** | Claude Code (v2.1.183), Gemini CLI (#22672), DeepSeek (#3275/#3290), Qwen Code (#5376) | Destructive command blocking, scope discipline, sandbox path enforcement |
| **Enterprise/Team Features** | Claude Code (#35319, #68721), Copilot CLI (#3730), OpenCode (#5391) | Skill usage analytics, custom model support, multi-API-key profiles |
| **Windows Platform Parity** | Codex (8+ issues), Copilot CLI (#3700), Kimi (#2462), Claude Code (#26302), Pi (#2469) | WSL2 stability, Git Bash compatibility, sandbox ACL integrity |

**MCP reliability is the single most pervasive pain point.** Every tool with MCP integration has at least one high-severity authentication or credential-handling issue this cycle. This is the infrastructure layer that must stabilize before the ecosystem can move forward.

## 4. Differentiation Analysis

| Dimension | Anthropic (Claude Code) | OpenAI (Codex) | Google (Gemini CLI) | GitHub (Copilot CLI) | Moonshot (Kimi) | OpenCode | Pi | Qwen | CodeWhale |
|---|---|---|---|---|---|---|---|---|---|
| **Core Philosophy** | Safety-first auto-mode | Remote execution architecture | Agent orchestration | Enterprise MCP hub | Lightweight CLI | Community extensible | Terminal-native UX | Multi-channel platform | Pure Rust, high performance |
| **Primary Strength** | Git safety enforcement, CI automation | Multi-platform remote exec, MCP OAuth | Memory system, sub-agent orchestration | Fleet Mode, enterprise admin | Simple, focused CLI | Plugin ecosystem, /goal system | Terminal ecosystem compat, themes | Security hardening, QQ channel | Rebrand momentum, static binaries |
| **Achilles' Heel** | Data loss, cache costs | Windows stability, rate-limiting | Agent hangs/false reporting | MCP auth pipeline, WSL2 regressions | Cross-platform packaging, proxy support | File watcher reliability, post-update corruption | Thread safety in parallel edits | Sandbox path validation | UI freezes, monolithic codebase |
| **Target User** | Teams, CI/CD pipelines | Multi-platform developers | Data scientists, researchers | Enterprise Fleets | Individual devs in restricted networks | Plugin developers, tinkerers | Terminal power users | East Asian market, QQ ecosystem | Performance-critical devs |
| **Release Velocity** | Weekly stable | Daily (alpha + stable) | Irregular | Weekly | Low | Irregular (v1.16.0) | High (daily releases) | Moderate | High (v0.8.x cadence) |

**Key differentiator:** Claude Code and Copilot CLI are pushing enterprise safety features (git guards, admin-managed models). Codex is investing heavily in remote execution infrastructure. Gemini CLI is betting on agent memory as a differentiator. The open-source tools (Pi, Qwen, CodeWhale) are innovating on terminal experience and platform-specific integration (QQ, Warp detection, Kitty protocol).

## 5. Community Momentum & Maturity

**Mature & well-resourced:**
- **Claude Code** — Most upvoted community issues (351 👍 on #36151), strong PR velocity. But 53-day broken automation and stale PRs suggest maintenance needs scaling.
- **OpenAI Codex** — High PR throughput (10 today, including complex 3-PR stacks). Remote execution infrastructure investment signals long-term architectural thinking. Rate-limit crisis (#28879) could erode trust.
- **Gemini CLI** — Active development (10 PRs), but issues marked "Need retesting" and "Need information" suggest triage backlog. Sub-agent reliability is a recognized weakness.

**Rapidly iterating (high release velocity, early-stage feel):**
- **Pi** — Daily releases (v0.79.7 today), feature-complete with multi-provider support, but thread safety gaps (#2327) reveal immaturity under concurrent loads.
- **CodeWhale** — Rebranding signals maturation, but monolithic file sizes (9,402-line config.rs) indicate growing pains. UI freezes are the #1 issue.
- **OpenCode** — Community energy is high (competing PRs for same feature is a good sign). Inotify fix addresses a long-standing Linux developer grievance.

**Smaller but focused:**
- **Kimi Code CLI** — Lowest activity count (3 issues, 1 PR today). Proxy fix is urgent but narrow. Small community may mean slower issue resolution.
- **Qwen Code** — Security push today is commendable, but 3 fundamental trust bypass bugs suggest earlier security audits were insufficient. QQ Bot integration shows regional specialization.

## 6. Trend Signals

*Industry patterns from this cycle's data:*

1. **Model cost is the new bottleneck.** Both Codex (#28879: 10-20x cost jump) and OpenCode (#32911: Deepseek over-billing) highlight that API pricing volatility is now the #1 unexpected cost risk for CLI tool users. Expect "cost observability" (token dashboards, per-session budgets) to become a must-have feature within 3 months.

2. **Agent safety is a universal requirement.** Claude Code's git safety release is the most noteworthy single feature this cycle, and it's mirrored across the ecosystem: Gemini's destructive-command discouragement (#22672), Qwen's sandbox path enforcement (#5375), CodeWhale's scope-discipline prompts (#3290). **Trust is the new performance metric.**

3. **Windows remains the unsolved problem.** Eight distinct Codex issues, the WSL2 CPU regression in Copilot CLI, Kimi's Git Bash packaging failure, and Pi's clipboard paste bug all point to the same conclusion: no tool has shipped a truly production-grade Windows experience. This is a market opportunity.

4. **MCP is fracturing.** While every major tool integrates MCP, authentication serialization, credential storage, error handling, and schema interpretation all vary. The `missing field inputSchema` error in Codex Desktop (#28978) that works perfectly on CLI suggests code paths are diverging. Standardization (or at least compatibility testing) is needed.

5. **Open-source tools are catching up on features, not reliability.** Pi, OpenCode, and CodeWhale now match commercial tools on features (multi-agent, session goals, provider flexibility) but trail on reliability (freezes, crashes, data loss). The next 6 months will determine whether community-driven tools can close the quality gap.

6. **Security holes are being found at the configuration layer.** Qwen Code's trust-as-boolean-coercion bug (#5368), Copilot CLI's content-exclusion over-blocking (#3860), and CodeWhale's unauthenticated app-server bind (#3258) all represent the same pattern: configuration parsing is a recurring vulnerability surface that deserves fuzz testing.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-19 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following Skills PRs have generated the most community discussion and attention:

**#514 — document-typography** *(OPEN)*
- **Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents—a quality-control layer for typographic polish.
- **Discussion highlights:** Addresses a universal pain point; commenters noted this affects "every document Claude generates." Strong latent demand for output quality assurance.
- **Status:** Open since March 2026; active discussion.
- *github.com/anthropics/skills/pull/514*

**#486 — ODT (OpenDocument) skill** *(OPEN)*
- **Functionality:** Create, fill, read, and convert OpenDocument Format files (.odt, .ods) including template filling and ODT-to-HTML parsing.
- **Discussion highlights:** High interest from LibreOffice/enterprise users seeking ISO-standard document workflows outside the Microsoft ecosystem.
- **Status:** Open since March 2026; extended discussion period.
- *github.com/anthropics/skills/pull/486*

**#210 — frontend-design clarity improvement** *(OPEN)*
- **Functionality:** Revises the existing frontend-design skill with actionable, conversation-scoped instructions for Claude—specific enough to steer behavior without human intervention.
- **Discussion highlights:** Focused on making existing skills *actually usable* rather than adding new ones. Signals community desire for skill quality over quantity.
- **Status:** Open since January 2026.
- *github.com/anthropics/skills/pull/210*

**#83 — skill-quality-analyzer and skill-security-analyzer** *(OPEN)*
- **Functionality:** Meta-skills that evaluate other Skills across five dimensions (structure, documentation, tooling, edge cases, security).
- **Discussion highlights:** First proposal for "skills about skills"—the community is self-organizing quality assurance. Security analysis dimension particularly well-received.
- **Status:** Open since November 2025; extensive review.
- *github.com/anthropics/skills/pull/83*

**#538, #539, #541 — Lubrsy706 bug-fix series** *(OPEN)*
- **Functionality:** Three targeted fixes: case-sensitive file references in PDF skill, YAML parsing validation in skill-creator, and tracked-change ID collision prevention in DOCX skill.
- **Discussion highlights:** Demonstrates growing community investment in correctness for existing skills rather than novel features.
- **Status:** All open; three-PR spike from single contributor.
- *github.com/anthropics/skills/pull/538*, */539*, */541*

**#181 — SAP-RPT-1-OSS predictor** *(OPEN)*
- **Functionality:** Enables Claude to use SAP's open-source tabular foundation model for predictive analytics on enterprise business data.
- **Discussion highlights:** Enterprise analytics use case; signals demand for Claude-SAP integration beyond basic document tasks.
- **Status:** Open since December 2025.
- *github.com/anthropics/skills/pull/181*

**#568 — ServiceNow platform skill** *(OPEN)*
- **Functionality:** Broad coverage of ServiceNow: ITSM, ITOM, ITAM/SAM, FSM, HRSD, SPM, Vulnerability Response, IntegrationHub.
- **Discussion highlights:** Largest single-platform enterprise skill proposed; covers 12+ ServiceNow modules.
- **Status:** Open since March 2026.
- *github.com/anthropics/skills/pull/568*

---

## 2. Community Demand Trends

Analysis of Issues reveals five concentrated demand vectors:

| Direction | Signal | Key Issues |
|---|---|---|
| **Org-wide skill sharing & management** | Most-upvoted open issue (#228, 👍7) requests shared skill libraries within organizations, replacing manual `.skill` file sharing via Slack. | #228 |
| **Windows compatibility** | Three independent issues (#1061, #556, #1169) report broken `run_eval.py` on Windows. Multiple PRs (#1050, #1099, #1298) now address this. | #1061, #556, #1169 |
| **Skill-creator tooling reliability** | #202 (closed) called for best-practice rewrite; #556/#1169 document 0% recall bug in the evaluation loop—10+ independent reproductions. | #202, #556, #1169 |
| **Agent governance & safety** | #412 proposes governance patterns (policy enforcement, threat detection, audit trails). #492 raises security concerns about namespace impersonation. | #412, #492 |
| **MCP/API exposure** | Earlier demand (#16) to expose Skills as MCPs—signal that community wants Skills to interoperate beyond Claude Code. | #16 |

**Cross-cutting theme:** The community is shifting from *creating new Skills* to *fixing/reliably operating existing infrastructure*—Windows support, evaluation tooling, and error handling dominate recent Issues.

---

## 3. High-Potential Pending Skills

These Skill PRs carry active comment threads and may land soon:

- **#1298 — `run_eval.py` fix** *(OPEN, updated June 11)*: Comprehensive repair of the evaluation pipeline—Windows stream reading, trigger detection, parallel workers. The most actively patched area of the codebase.
  - *github.com/anthropics/skills/pull/1298*

- **#361 — YAML special character detection** *(OPEN, updated June 10)*: Prevents silent parsing failures when `description` fields contain `:`, `#`, `{`, `}`. Multiple PRs (#539, #361) address this—duplication suggests urgent need.
  - *github.com/anthropics/skills/pull/361*

- **#362 — UTF-8 panic fix** *(OPEN, updated June 10)*: Replaces character-length checks with byte-length validation to prevent Rust panics on multi-byte characters (e.g., emoji, CJK).
  - *github.com/anthropics/skills/pull/362*

- **#723 — testing-patterns skill** *(OPEN)*: Comprehensive testing coverage (unit, React, end-to-end) following the Testing Trophy model. Directly addresses community calls for code quality tooling.
  - *github.com/anthropics/skills/pull/723*

- **#444 — AURELION skill suite** *(OPEN)*: Four skills (kernel, advisor, agent, memory) for structured cognitive frameworks and persistent memory—targets professional knowledge management.
  - *github.com/anthropics/skills/pull/444*

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *reliable infrastructure*—specifically Windows-compatible evaluation tooling and cross-platform skill management—rather than new Skill content, signaling a maturation phase from "what can Skills do" to "how do Skills work reliably in production environments."**

---

# Claude Code Community Digest — 2026-06-19

## Today's Highlights
Release **v2.1.183** ships with critical auto-mode safety improvements, blocking destructive git commands when the user didn't explicitly request them. The issue tracker remains highly active with 50 updated items, including a long-running discussion on **multi-account mobile switching** (96 comments) and a fresh **API rate-limiting regression** reported across multiple platforms. A community PR fixing the 53-day broken "lock stale issues" workflow was merged today.

## Releases
- **v2.1.183** – [Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.183)
  - **Auto-mode git safety**: Destructive commands (`git reset --hard`, `git checkout -- .`, `git clean -fd`, `git stash drop`) are now blocked unless the user explicitly asked to discard local work.
  - `git commit --amend` is blocked when the commit was not made by the agent in the current session.
  - *No other changes documented in the release.*

## Hot Issues (10 noteworthy)

1. **[#36151] Multi-account switching in Claude Mobile** – *96 comments, 351 👍*  
   The most-upvoted open issue. Users want seamless account switching without shared email, a pain point for teams.  
   [Link](https://github.com/anthropics/claude-code/issues/36151)

2. **[#53915] API rate-limiting errors** – *57 comments*  
   "Server is temporarily limiting requests" affects users on Windows, VS Code, and API directly. Multiple reports suggest a systemic throttling issue, not individual quota problems.  
   [Link](https://github.com/anthropics/claude-code/issues/53915)

3. **[#26302] Severe UI lag on Windows (Desktop 1.1.3189)** – *43 comments*  
   A 4-month-old performance regression still unaddressed. Users report mouse stutter making the desktop app nearly unusable after an update.  
   [Link](https://github.com/anthropics/claude-code/issues/26302)

4. **[#47166] JetBrains plugin need for a real AI Assist interface** – *25 comments*  
   Community frustration that JetBrains integration lags far behind VS Code. Users want a first-class plugin with inline code suggestions.  
   [Link](https://github.com/anthropics/claude-code/issues/47166)

5. **[#59248] Silent retention cleanup deletes session transcripts** – *16 comments*  
   A serious data-loss bug on macOS: Claude Code silently purges conversation transcripts with no opt-in or recovery mechanism. Users losing days of work.  
   [Link](https://github.com/anthropics/claude-code/issues/59248)

6. **[#68721] Team management tools missing in 2.1.178 (regression)** – *15 comments*  
   Native `TeamCreate`/`TeamDelete` tools disappeared after the 2.1.177→2.1.178 update, breaking team workflows on Linux. Marked as regression.  
   [Link](https://github.com/anthropics/claude-code/issues/68721)

7. **[#58429] Built-in text-to-speech for accessibility** – *13 comments*  
   Request to speak Claude's responses aloud for blind/low-vision users and hands-free workflows. Two design patterns proposed.  
   [Link](https://github.com/anthropics/claude-code/issues/58429)

8. **[#47098] New sessions never hit a full cache** – *12 comments*  
   Even after seconds of inactivity, new sessions pay full cache-create costs (~6505 tokens). Users suspect the cache invalidation window is misconfigured for short sessions.  
   [Link](https://github.com/anthropics/claude-code/issues/47098)

9. **[#35319] Skill invocation tracking and analytics** – *5 comments, 29 👍*  
   Enterprise adoption blocker: organizations cannot audit which skills/internal tools are invoked or measure usage patterns.  
   [Link](https://github.com/anthropics/claude-code/issues/35319)

10. **[#69358] No response from API in 2.1.181 (constant)** – *2 comments, 11 👍*  
    Fresh regression on Linux, high reaction count suggests widespread impact. API calls silently fail with no response.  
    [Link](https://github.com/anthropics/claude-code/issues/69358)

## Key PR Progress (6 items)

1. **[#69470] [MERGED] Fix lock-closed-issues workflow** – *37 minutes to merge*  
   Fixes the scheduled workflow that had **53 consecutive daily failures** since April 27. Replaced broken offset pagination with GitHub's search API. Automated maintenance now works again.  
   [Link](https://github.com/anthropics/claude-code/pull/69470)

2. **[#68673] Fix pagination break condition** – *Open, updated today*  
   Fixes scripts to break pagination when a page is not full (not only when empty), preventing missed pages in edge cases.  
   [Link](https://github.com/anthropics/claude-code/pull/68673)

3. **[#45553] Resolve duplicate IPs** – *Open since April, stale*  
   A long-pending contribution addressing duplicate IP address handling. No activity from maintainers.  
   [Link](https://github.com/anthropics/claude-code/pull/45553)

4. **[#23972] Fix hookify: Python 3.8 compat + cwd-independent rules** – *Open since February*  
   Two fixes: Python 3.8 compatibility for `config_loader.py` and making rule loading independent of current working directory. No maintainer review in 4+ months.  
   [Link](https://github.com/anthropics/claude-code/pull/23972)

5. **[#41611] Add missing source to Claude Code** – *Open since March*  
   Unclear scope — "add missing source" with no detailed description. No maintainer engagement.  
   [Link](https://github.com/anthropics/claude-code/pull/41611)

6. **[#41447] "Open source Claude Code ✨"** – *Open since March*  
   A widely-followed community PR claiming to close open-sourcing issues (#59, #456, etc.). Symbolic request; no official response from Anthropic.  
   [Link](https://github.com/anthropics/claude-code/pull/41447)

## Feature Request Trends

- **Multi-platform parity**: Strong and persistent demand for **JetBrains plugin** (real AI Assist interface, not just MCP) and **IntelliJ-first integrations**. VS Code dominance frustrates users on other IDEs.
- **Accessibility & ergonomics**: Requests for **text-to-speech**, configurable UI colors, and **mic input persistence** indicate growing non-developer and accessibility-conscious user base.
- **Account & team management**: **Multi-account switching** (mobile), **skill usage analytics**, and **project group sorting by recency** show enterprise/team adoption pressures.
- **Desktop session reliability**: Multiple feature requests for **persistent chat history**, **configurable session retention**, and **recovery mechanisms**—users want desktop behavior to match CLI reliability.

## Developer Pain Points

1. **Cache cost inefficiency**: Even short idle periods reset cache context, incurring 6,500+ token overhead. Developer frustration over unpredictable billing.
2. **API rate limiting as default experience**: Multiple issues across platforms (Windows, Linux, VS Code) report persistent "server limiting requests" errors—not user quota, but platform throttling.
3. **Data loss without warning**: Silent deletion of session transcripts (#59248) and sessions disappearing after restart (#59736) erode trust in Claude Code for ongoing work.
4. **Stale/unreviewed community contributions**: PRs languishing for 2–4 months with zero maintainer review (#23972, #45553, #41611) despite fixing real bugs. Suggests maintainer bandwidth bottleneck.
5. **Regression velocity**: Two regressions this week alone (#68721 for team tools in 2.1.178, #69358 for API in 2.1.181). Developers report a pattern of new releases breaking core functionality previously working.
6. **Bash/zsh mismatch on macOS**: The Bash tool runs zsh but emits bash-specific syntax causing silent failures—a subtle but persistent cross-shell compatibility bug.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-19

## Today's Highlights

Significant progress on remote execution infrastructure with a three-PR stack adding deferred executor initialization and configurable connection timeouts. The community remains vocal about Windows stability issues, with a cluster of `@oai/sky` package export failures breaking Computer Use on that platform. A major rate-limiting concern emerged: Plus plan users report a 10–20x jump in per-token cost since June 16, draining their 5h budget in 2–3 prompts.

## Releases

**Codex CLI `rust-v0.141.0`** — Stable release featuring authenticated, end-to-end encrypted Noise relay channels for remote executors. Cross-platform remote execution now preserves executor-native working directories, shells, and filesystem permission paths across app-server and exec-server boundaries.

**Alpha channel: `rust-v0.142.0-alpha.1`, `rust-v0.142.0-alpha.2`, `rust-v0.142.0-alpha.3`** — Pre-release builds with no public changelog beyond version bumps.

## Hot Issues

1. **[#20161] Phone number verification doesn't work** — CLOSED. 201 comments, 125 👍. The highest-engagement issue of the quarter. Users hitting SSO-based login loops that demand phone verification despite never having added a phone. OpenAI appears to have resolved this, but community frustration was intense. [Link](https://github.com/openai/codex/issues/20161)

2. **[#25719] macOS: `syspolicyd`/`trustd` CPU and memory runaway** — OPEN. 33 comments, 40 👍. Codex Desktop repeatedly triggers macOS security daemons, causing persistent high CPU and memory on Apple Silicon. A serious performance bug for daily drivers. [Link](https://github.com/openai/codex/issues/25719)

3. **[#15777] Windows sandbox corrupts ACL on AppData** — OPEN. 26 comments. Long-standing Windows sandbox issue corrupting NTFS access control lists. Free-tier users are disproportionately affected. [Link](https://github.com/openai/codex/issues/15777)

4. **[#28988] Full Access mode permission loop** — OPEN. 8 comments, 5 👍. Fresh bug from build 26.614.11602: Full Access mode on macOS repeatedly asks for the same permission on every turn. Released just yesterday. [Link](https://github.com/openai/codex/issues/28988)

5. **[#28879] Rate-limit cost per token jumped 10–20x since June 16** — OPEN. 5 comments, 2 👍. Plus plan users on `gpt-5.5` now exhaust their 5h budget in 2–3 prompts (down from 20+). If confirmed, this represents a silent pricing change for Plus subscribers. [Link](https://github.com/openai/codex/issues/28879)

6. **[#28997] `logs_2.sqlite-wal` grows unbounded** — OPEN. 6 comments. Codex CLI `0.140.0` produces SQLite WAL files ballooning to tens of gigabytes. A disk-space disaster for long-running CLI sessions. [Link](https://github.com/openai/codex/issues/28997)

7. **[#28241] turn-diff tree refs break libgit2-based Git clients** — OPEN. 7 comments, 1 👍. Codex Desktop's `turn-diff` refs are incompatible with libgit2, breaking GitKraken, GitLens, and other popular Git tools on Windows. [Link](https://github.com/openai/codex/issues/28241)

8. **[#28689] Threads disappear after update — migration version-38 checksum mismatch** — OPEN. 2 comments, 1 👍. Threads vanished from sidebar post-update due to a migration checksum mismatch introduced by PR #28655. Affects Pro users with significant thread histories. [Link](https://github.com/openai/codex/issues/28689)

9. **[#28978] Desktop 26.616: new conversations fail with `missing field inputSchema`** — OPEN. 2 comments, 5 👍. MCP integration regression: all new conversations fail with an `Invalid request` error, while CLI with identical config works fine. High impact for MCP plugin users. [Link](https://github.com/openai/codex/issues/28978)

10. **[#29029] Windows: App Bar and Side Menu flicker** — OPEN. 2 comments. User report in Thai describing persistent UI flicker of the top bar and side menu on Windows. Minor but visually disruptive. [Link](https://github.com/openai/codex/issues/29029)

## Key PR Progress

1. **[#29014] Honor startup custom CA bundles with managed MITM** — Ensures `SSL_CERT_FILE` env override works with Codex's managed proxy, preventing corporate CA cert breakage. Enterprise-friendly fix. [Link](https://github.com/openai/codex/pull/29014)

2. **[#29013] Protect managed MITM CA private keys from sandboxed commands** — Security hardening: `$CODEX_HOME/proxy` CA private keys are now inaccessible to sandboxed processes, closing a vulnerability where `chmod 0600` alone was insufficient. [Link](https://github.com/openai/codex/pull/29013)

3. **[#29012] Assign item IDs to compacted replacement history** — CLOSED. Fixes remote v2 compaction, which could return history items without IDs, breaking downstream `item_ids`-enabled requests. [Link](https://github.com/openai/codex/pull/29012)

4. **[#29011] Add `clock.current-time` tool** — CLOSED. Exposes session time provider to models and Code Mode. Returns UTC reminder text or structured JSON. Small but useful for time-aware agent behavior. [Link](https://github.com/openai/codex/pull/29011)

5. **[#28674/28683/29025] Remote environment connection lifecycle** — 3-PR stack adding deferred executor initialization, snapshot tracking of starting environments, and configurable connection timeouts. Moves remote executors toward production-grade reliability. [Link 1](https://github.com/openai/codex/pull/28674), [Link 2](https://github.com/openai/codex/pull/28683), [Link 3](https://github.com/openai/codex/pull/29025)

6. **[#28787] Code-mode: transport-neutral session runtime** — Extracts session ownership into a transport-neutral `SessionRuntime`, preparing for cells and shared session state to move behind a separate-process transport. Architectural refactoring for future sandboxing. [Link](https://github.com/openai/codex/pull/28787)

7. **[#28489] Add indexed web search mode** — Introduces `web_search = "indexed"` alongside existing `disabled`/`cached`/`live` modes. Sends `index_gated_web_access: true` for hosted search. A new tier of web access control. [Link](https://github.com/openai/codex/pull/28489)

8. **[#29006] Preserve skill descriptions outside model context** — Stops discarding skill metadata during loading when descriptions exceed 1024 chars. Full descriptions remain available for UI and plugins; only the model-visible fragment is truncated. [Link](https://github.com/openai/codex/pull/29006)

9. **[#29017/29019/29020] MCP OAuth serialization stack** — 3-PR series serializing MCP OAuth refresh transactions, login/logout, and credential rereading. Prevents race conditions during token refresh for MCP-authenticated servers. [Link 1](https://github.com/openai/codex/pull/29017), [Link 2](https://github.com/openai/codex/pull/29019), [Link 3](https://github.com/openai/codex/pull/29020)

10. **[#26703] TUI plugin sharing — render remote catalog sections** — Part of a multi-PR initiative to bring remote plugin discovery and sharing into the TUI interface. Builds on identity support and section fetching from earlier PRs. [Link](https://github.com/openai/codex/pull/26703)

## Feature Request Trends

- **MCP OAuth and authentication flexibility** — Multiple requests for configurable `base_url` (e.g., `amazon-bedrock`), better SSH key authentication for remote connections, and MCP OAuth serialization to prevent refresh conflicts.
- **Conversation management** — Strong demand for moving conversations between projects and preserving thread state across updates, especially after recent migration bugs caused data loss.
- **Rate-limit transparency** — Growing frustration with unexplained cost-per-token changes, with multiple users requesting clear, banked rate-limit resets rather than immediate hard resets.
- **Windows platform parity** — Continued requests for stable Computer Use support, proper native messaging host registry keys for Chrome extension, and functioning taskbar icons.

## Developer Pain Points

**Windows stability remains Codex's Achilles' heel.** Today's data shows at least 8 distinct Windows-specific issues: ACL corruption, missing `@oai/sky` package exports, WSL agent mode failures, broken libgit2 refs, transparent taskbar icons, PowerShell command conflicts with antivirus, and UI flicker. The `@oai/sky` packaging problem alone blocks Computer Use for all Windows users.

**Rate limiting is approaching a crisis point.** The reported 10–20x cost increase on Plus plan prompted immediate community backlash. Combined with reports of hard resets replacing banked resets, Plus subscribers are facing a dramatically degraded experience without clear communication from OpenAI.

**MCP integration regressions** are a recurring pain point. The `missing field inputSchema` error on Desktop 26.616 (while CLI works) and the MCP OAuth credential race conditions suggest the Desktop and CLI code paths are diverging in problematic ways.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-19

## Today's Highlights
No new releases shipped in the last 24 hours, but the development pipeline is active with important fixes. A critical PR addresses MCP image MIME-type sniffing to prevent corrupted image payloads, and another resolves Jupyter Notebook/JSON file corruption in `write_file`. The team also landed an atomic write fix for MCP OAuth tokens, improving credential safety.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** (🔒)
   - **Why it matters:** A top-voted bug (8 👍) where `gemini-cli` hangs forever when deferring to the generalist agent. Users report that simple folder creation stalls for up to an hour. The workaround—telling the model not to use sub-agents—points to a deep agent orchestration issue.
   - **Priority:** P1 | **Status:** Need retesting

2. **[Subagent recovery after MAX_TURNS falsely reports success](https://github.com/google-gemini/gemini-cli/issues/22323)** (🔒)
   - **Why it matters:** A `codebase_investigator` subagent reports `status: "success"` and `"GOAL"` termination even after hitting its turn limit without doing any analysis. This masks real failures and undermines confidence in agent reporting.
   - **Priority:** P1 | **Comments:** 6

3. **[Shell command execution gets stuck after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (🔒)
   - **Why it matters:** After executing simple CLI commands, the shell status shows "Waiting input" despite the command having finished. This blocks further automation and is extremely disruptive—one of the more popular bugs (3 👍).
   - **Priority:** P1 | **Effort:** Medium

4. **[Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (🔒)
   - **Why it matters:** Auto Memory only marks sessions as processed when the extraction agent successfully reads the file. Low-signal sessions that are skipped remain unprocessed and keep appearing, causing infinite retries and wasted resources.
   - **Priority:** P2

5. **[400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (🔒)
   - **Why it matters:** Users with many custom skills or sub-agents hit API limits (400 errors). The agent should intelligently scope tools instead of exposing all at once. Community reaction is muted but the impact grows with ecosystem complexity.
   - **Priority:** P2 | **Status:** Need information

6. **[Model creates tmp scripts in random directories](https://github.com/google-gemini/gemini-cli/issues/23571)** (🔒)
   - **Why it matters:** When restricted from shell execution, the model writes temporary scripts across multiple directories, creating significant cleanup overhead. Points to a need for better output-confinement strategies.
   - **Priority:** P2 | **Comments:** 3

7. **[Browser agent ignores settings.json overrides](https://github.com/google-gemini/gemini-cli/issues/22267)** (🔒)
   - **Why it matters:** Configuration like `maxTurns` set in `settings.json` is completely ignored by the Browser Agent. The `AgentRegistry` correctly reads settings but the agent itself doesn't apply them—a disconnect that frustrates power users.
   - **Priority:** P2 | **Status:** Need retesting

8. **[Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** (🔒)
   - **Why it matters:** Users who explicitly disabled sub-agents in config report them activating automatically after an update. This is a critical regression in user control and trust.
   - **Priority:** P2 | **Comments:** 2

9. **[Memory system bugs and quality improvements](https://github.com/google-gemini/gemini-cli/issues/26516)** (🔒)
   - **Why it matters:** A tracking issue for multiple Auto Memory bugs (low-signal retries, invalid patches, redaction concerns). The memory system is clearly under active refinement.
   - **Priority:** P2 | **Status:** Need information

10. **[Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (🔒)
    - **Why it matters:** Community feature request (1 👍) asking the agent to avoid `git reset --force` or similar destructive commands when safer alternatives exist. Points to a desire for safer autonomous operation.
    - **Priority:** P2

## Key PR Progress

1. **[fix(core): write MCP OAuth tokens atomically](https://github.com/google-gemini/gemini-cli/pull/27664)** (CLOSED)
   - **What:** Writes legacy MCP OAuth token files via temp file + atomic rename. Prevents partial/corrupt token files on crash.
   - **Why it matters:** Critical credential safety improvement—without this, a crash during token write could leave an empty or corrupt file, breaking MCP connections.

2. **[fix(core): hide ignored folders from session context](https://github.com/google-gemini/gemini-cli/pull/27678)** (CLOSED)
   - **What:** Filters `.gitignore`/`.geminiignore` directories from the initial session context directory tree.
   - **Why it matters:** Reduces noise in agent context, preventing the model from wasting tokens on irrelevant directories (e.g., `node_modules`, build artifacts).

3. **[fix(core): sniff MCP image MIME types](https://github.com/google-gemini/gemini-cli/pull/27850)** (OPEN)
   - **What:** Adds local image signature detection (PNG, JPEG, GIF, WebP) to correct mismatched MIME types in MCP image payloads before sending to the model.
   - **Why it matters:** Fixes #27731—prevents garbled images when servers declare `image/png` for WebP data. A practical quality-of-life fix for multimodal agents.

4. **[feat(cli): add 'models' command to list available Gemini models](https://github.com/google-gemini/gemini-cli/pull/27848)** (OPEN)
   - **What:** New `gemini models` subcommand that lists available models, context windows, and tiers with human-readable and JSON output.
   - **Why it matters:** A long-requested developer utility—no more guessing which models are accessible or digging through docs.

5. **[fix(cli): prompt for folder trust before auth](https://github.com/google-gemini/gemini-cli/pull/27845)** (OPEN)
   - **What:** Adds an early folder-trust prompt for interactive launches before authentication starts. Saves the user's choice then relaunches with correct workspace settings.
   - **Why it matters:** Fixes #27844—prevents auth from starting before trust decisions are made, improving security UX.

6. **[fix(core-tools): resolve Jupyter Notebook and JSON corruption in write_file](https://github.com/google-gemini/gemini-cli/pull/28000)** (OPEN)
   - **What:** Fixes `write_file` silently corrupting `.ipynb` and `.json` files by improperly handling JSON serialization. Prevents data loss in data science workflows.
   - **Why it matters:** Critical for data scientists and researchers using Gemini CLI with notebooks—corrupt files can cause environment rollback in Colab/JupyterLab.

7. **[fix(core): decode response body using charset from Content-Type header](https://github.com/google-gemini/gemini-cli/pull/27996)** (OPEN)
   - **What:** `web-fetch` now respects the `charset` parameter in HTTP `Content-Type` headers instead of always assuming UTF-8.
   - **Why it matters:** Fixes garbled text on non-UTF-8 pages (e.g., Chinese/Japanese sites using GBK or ISO-8859-1). Broadens web agent compatibility.

8. **[fix(prompts): use function replacer in applySubstitutions to prevent $-pattern corruption](https://github.com/google-gemini/gemini-cli/pull/28013)** (OPEN)
   - **What:** String replacements in prompt substitutions now use a function replacer, preventing `$`-prefixed patterns (e.g., `$$`, `$&`) in skill/agent descriptions from being interpreted as replacement patterns.
   - **Why it matters:** Fixes a subtle but dangerous bug—tool descriptions containing `$` could corrupt prompt substitutions, causing unpredictable agent behavior.

9. **[chore(deps): bump @opentelemetry/core from 2.7.1 to 2.8.0](https://github.com/google-gemini/gemini-cli/pull/28024)** (OPEN)
   - **What:** Automated dependency update for OpenTelemetry core instrumentation.
   - **Why it matters:** Telemetry stability is key for debugging agent behavior; staying current with the OTel ecosystem reduces drift and security risk.

10. **[chore(deps): pin dependencies and enforce 14-day update cooldown](https://github.com/google-gemini/gemini-cli/pull/27948)** (CLOSED)
    - **What:** Pins all direct dependencies to exact versions and enforces a 14-day cooldown for automated updates.
    - **Why it matters:** Reduces CI breakage from unexpected transitive updates and gives the team time to vet changes before they land.

## Feature Request Trends
- **AST-aware codebase tools:** Multiple EPICs (#22745, #22746, #22747) investigate using AST-aware CLIs for file reads, search, and codebase mapping. This is clearly a strategic bet—moving beyond text-based file manipulation to syntax-aware understanding for better agent quality.
- **Auto Memory reliability:** A flurry of issues from SandyTao520 (#26516, #26522, #26523, #26525) focus on memory system robustness—stopping infinite retries, quarantining invalid patches, and adding deterministic redaction. Memory is seen as a core differentiator but is currently unstable.
- **Agent self-awareness & safety:** Features like #21432 (knowing its own CLI flags/hotkeys) and #22672 (discouraging destructive commands) indicate a push toward safer, more introspective agents that understand their own boundaries.
- **Browser agent resilience:** Issues #21983 (Wayland failures), #22267 (settings.json ignored), and #22232 (session lock recovery) show the browser subagent as a friction point requiring significant hardening.

## Developer Pain Points
- **Agent hangs and false success reporting:** The #1 pain point. #21409 (generalist hanging), #22323 (false success on MAX_TURNS), and #25166 (stuck at "Waiting input") all describe situations where agents become unresponsive or lie about their state—destroying user trust.
- **Subagent configuration bleed:** #22093 (subagents running without permission) and #22267 (settings.json ignored) reflect a pattern where user configuration is silently overridden. Developers feel loss of control.
- **Context pollution:** The model creates tmp scripts (#23571), considers irrelevant directories (#27678 fix), and handles >128 tools poorly (#24246). Context window hygiene is a recurring frustration.
- **Destructive auto-behavior:** The community wants guardrails against potentially destructive commands (#22672) and is unhappy when agents force destructive operations without consent.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — June 19, 2026

## Today's Highlights
The community is experiencing significant friction with authentication and MCP tool access this week, highlighted by a critical bug where MCP OAuth re-authentication succeeds visibly but still leaves tools without credentials. Several high-severity issues are actively being tracked, including a WSL2 CPU spin regression that renders the TUI unusable and a content-exclusion bug that blocks even basic shell commands like `date` and writes to `/dev/null`. On the feature side, demand for enterprise-managed model support and session archival/restore capabilities continues to grow.

## Releases
No new releases in the last 24 hours. The latest stable version remains **v1.0.63**.

## Hot Issues (10 Noteworthy)

1. **[#3838 – Drive MCP OAuth not attached: tools fail with 'missing required authentication credential' after successful reauth](https://github.com/github/copilot-cli/issues/3838)**  
   **Why it matters:** OAuth flow completes, cache files are created, but Drive tool calls are sent without credentials. This is a critical gap in the MCP authentication pipeline that breaks the core value proposition of integrated MCP tools. Community comments (7) reflect confusion and urgency.

2. **[#3700 – 1.0.60 WSL2 regression: CLI MainThread spins at ~215% CPU while idle, TUI output frozen](https://github.com/github/copilot-cli/issues/3700)**  
   **Why it matters:** High-severity regression making Copilot CLI unusable on WSL2 — the TUI freezes until restart. 2 upvotes reflect strong community impact. Reproduces cleanly on every session.

3. **[#3860 – Content-exclusion over-blocks entire working tree (incl. /dev/null and binaries), sticky to one session](https://github.com/github/copilot-cli/issues/3860)**  
   **Why it matters:** Once triggered, content-exclusion enters a broad-block state denying ALL shell commands and file writes, including to `/dev/null` and system binaries. This is a safety mechanism gone rogue. Filed as high severity.

4. **[#1974 – After upgrading to v1.0.3, generated Markdown links are not clickable](https://github.com/github/copilot-cli/issues/1974)**  
   **Why it matters:** A long-standing bug (opened March 2026) still unresolved. Link rendering regression affects one of the CLI's primary output formats. 1 upvote suggests moderate but persistent frustration.

5. **[#3812 – Subagents can no longer access MCP tools](https://github.com/github/copilot-cli/issues/3812)**  
   **Why it matters:** Regression where subagents cannot see or use MCP tools, which previously worked. The community suspects deferred loading of MCP tools is the root cause. This undermines the agent orchestration model.

6. **[#3839 – Ollama Cloud does not support custom_tool_call payload used by Copilot CLI](https://github.com/github/copilot-cli/issues/3839)**  
   **Why it matters:** Fleet Mode with BYOK models over Ollama Cloud fails with a 400 error. 7 upvotes — the most popular issue this cycle. The `custom_tool_call` payload format is incompatible with Ollama's strict OpenAI-compatible endpoint.

7. **[#3859 – Copilot Subconscious sidekick keeps spawning per-prompt even with memory disabled](https://github.com/github/copilot-cli/issues/3859)**  
   **Why it matters:** The per-prompt memory "voting" agent ignores explicit `/memory off` and `settings.json` `"memory": false`. This wastes context window on unwanted processing and raises privacy concerns.

8. **[#3518 – Add ability to unarchive / restore an archived project session](https://github.com/github/copilot-cli/issues/3518)**  
   **Why it matters:** 5 upvotes — strong demand for session recovery. Accidentally archiving a long-running orchestrator session with accumulated context is irrecoverable today.

9. **[#3730 – Support Enterprise-Managed Custom Models in Copilot CLI](https://github.com/github/copilot-cli/issues/3730)**  
   **Why it matters:** 4 upvotes. Enterprise admins can configure custom models in the Copilot Admin dashboard for VS Code, but the CLI ignores them entirely. This is a blocker for enterprise adoption.

10. **[#3857 – Add "Yes, but only for the current session" option to "Allow directory access" dialog](https://github.com/github/copilot-cli/issues/3857)**  
    **Why it matters:** Users want session-scoped directory permissions — today it's either permanent allow or permanent deny, which is too coarse for many workflows.

## Key PR Progress

1. **[#3847 – Plan review: add compatibility fallback design + test vectors](https://github.com/github/copilot-cli/pull/3847)**  
   **What it does:** Proposes a JSON-first parsing strategy for plan review menus on strict OpenAI-compatible backends that lack `function_call` metadata, with YAML and numbered-list fallbacks. Includes test vectors.

2. **[#3846 – Plan review menus incompatible with strict OpenAI-compatible backends — add compatibility fallback](https://github.com/github/copilot-cli/issues/3846)**  
   **What it does:** Addresses the empty/useless plan review display on backends like Ollama. Related to the PR above.

3. **[#3850 – SDK/server mode: session.create drops mcpServers](https://github.com/github/copilot-cli/issues/3850)**  
   **What it does:** Fix needed for MCP servers never starting when provided programmatically via `SessionConfig.with_mcp_servers()` in SDK mode.

4. **[#3855 – Scrolling does not work](https://github.com/github/copilot-cli/issues/3855)**  
   **What it does:** Regression affecting scrollback in the TUI, likely introduced with the "full screen scrollbar" feature in v1.0.61.

5. **[#3854 – @ syntax for file reference not working anymore](https://github.com/github/copilot-cli/issues/3854)**  
   **What it does:** File autocompletion via `@` broken; only suggests root directory and a temp folder regardless of input.

6. **[#3834 – @filename does not expand anymore](https://github.com/github/copilot-cli/issues/3834)**  
   **What it does:** Similar to #3854 — symbol/file expansion via `@` stopped working. Multiple reports suggest a systematic issue in the autocomplete pipeline.

7. **[#3791 – Malformed attachment poisons session; all subsequent turns fail with 400](https://github.com/github/copilot-cli/issues/3791)**  
   **What it does:** Password-protected `.xlsx` causes a CAPI 400 that persists across all subsequent turns even without the attachment. Session-state corruption bug.

8. **[#3858 – Ctrl+Backspace (delete previous word) doesn't work on Windows](https://github.com/github/copilot-cli/issues/3858)**  
   **What it does:** Missing standard Windows keyboard shortcut. Alt+Backspace works (Unix convention), but Windows users expect Ctrl+Backspace.

9. **[#3856 – Repeated Enter in /resume picker splits a session](https://github.com/github/copilot-cli/issues/3856)**  
   **What it does:** Pressing Enter multiple times during session resume creates multiple active contexts. Extension `session.send()` then targets an invisible context that loses tool access.

10. **[#3296 – v1.0.46 fails to start MCP server on Ubuntu 20.04](https://github.com/github/copilot-cli/issues/3296)**  
    **What it does:** Runtime binary compiled for glibc 2.33+ breaks compatibility with Ubuntu 20.04 (glibc 2.31). Affects Linux MCP server users.

## Feature Request Trends

1. **Enterprise Model Management** — Strong demand (#3730, #3839) for CLI support of admin-managed custom models and BYOK endpoints. The gap between VS Code and CLI enterprise features is a recurring theme.

2. **Session Lifecycle Management** — Multiple requests (#3518, #3856) for session archival, restore, and unarchive capabilities. Users rely on long-running orchestrator sessions and need recovery paths.

3. **Plugin Stability & Distribution** — Requests (#2727, #3136) for lock files, stable plugin installation, and sharing instruction files via plugins rather than manual copy operations.

4. **Model Switching Automation** — Continued interest (#2896) in automatic model selection based on task complexity, rather than manual `/model` commands.

## Developer Pain Points

1. **MCP Tool Reliability** — The #1 pain point this cycle. Authentication failures (#3838), subagent access loss (#3812), server start failures (#3296), and SDK mode drops (#3850) collectively erode trust in MCP integration.

2. **Session State Corruption** — Attachment poisoning (#3791), session splits from double-Enter (#3856), and content-exclusion over-blocking (#3860) show fragility in session state management.

3. **WSL2 & Platform Regressions** — The 215% CPU spin regression (#3700) and Windows keyboard shortcut gaps (#3858) highlight ongoing platform-specific quality issues.

4. **BYOK/Ollama Compatibility** — The `custom_tool_call` payload incompatibility (#3839) and plan review menu blanking on strict OpenAI-compatible backends (#3846) are blocking Fleet Mode adoption with non-GitHub models.

5. **Configuration Ignored** — The `"disabled": true` flag on MCP servers being ignored (#3582) and memory settings not respected (#3859) suggest configuration-layer bugs that erode user control.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-06-19

## Today's Highlights
The community is actively pushing proxy support and Windows compatibility fixes. A critical bug (#2455) where `FetchURL` ignores system proxy env vars under restrictive networks has a proposed fix (#2461) already open. Meanwhile, a new issue (#2462) reports that the VS Code extension bundled CLI fails to extract correctly on Git Bash due to a macOS/zip assumption, highlighting ongoing cross-platform friction. Configuration complexity for MCP servers and plugins also continues to surface as a top complaint.

## Releases
No new releases in the last 24 hours.

## Hot Issues

- **[#2455 – FetchURL does not read system proxy (blocked network)](https://github.com/MoonshotAI/kimi-cli/issues/2455)** – Critical bug that breaks all outbound HTTP (FetchURL, WebSearch) behind proxies; curl works fine. Community voted with 0 👍 but high urgency; a fix PR is already up. *Why it matters:* Blocks users in enterprise/restricted environments entirely.

- **[#2462 – VS Code extension fails on Git Bash (tar vs zip)](https://github.com/MoonshotAI/kimi-cli/issues/2462)** – Extension bundles CLI in a format on macOS that Git Bash’s `tar` cannot handle (expects a zip). New issue, no comments yet. *Why it matters:* Windows + Git Bash is a common dev setup; this is a packaging regression.

- **[#2460 – MCP/plugin/skill configuration is too hard](https://github.com/MoonshotAI/kimi-cli/issues/2460)** – Positive tone but clear friction: onboarding MCP servers, plugins, and sub-skills is “harder than it needs to be.” No replies yet. *Why it matters:* Directly impacts new user retention; developer experience is a core selling point.

- **Other notable (filtered to 1–2):** No other issues updated today met the “noteworthy” bar. Total updated: 3, all covered.

## Key PR Progress

- **[#2461 – fix(net): honour system proxy env vars in aiohttp sessions](https://github.com/MoonshotAI/kimi-cli/pull/2461)** – Direct fix for #2455. Modifies all outbound HTTP in `FetchURL` and `WebSearch` to use `HTTP_PROXY`/`HTTPS_PROXY` env vars via aiohttp’s `ClientSession`. Single commit, clean solution. *Community reaction:* None yet (just opened), but likely to be fast-tracked.

Only one PR was updated in the last 24 hours.

## Feature Request Trends
Based on recent issues, the strongest recurring theme is **outbound networking flexibility**:
- System proxy support (HTTP_PROXY, HTTPS_PROXY, NO_PROXY) – #2455 and related
- Cross-platform packaging compatibility (Windows/Git Bash CLI extraction) – #2462
- Easier configuration for MCP servers, plugins, and sub-skills – #2460

A secondary pattern is **Windows and WSL2 parity** – both #2455 (WSL2) and #2462 (Git Bash) point to a need for more robust Windows integration testing.

## Developer Pain Points
- **Network restrictions in managed environments** – The top frustration: CLI tools that ignore system proxy settings force developers to disable their security stack or switch shells.
- **Platform-specific packaging bugs** – The VS Code extension not extracting on Git Bash because of an assumed tar/zip format is a classic integration pain point that wastes users’ time on setup.
- **Configuration complexity** – Feedback (#2460) indicates that while the core product works well, the configuration surface area (MCP servers, plugins, sub-skills) is too high for an “out of the box” experience. Users want wizards or auto-detect.

*No security advisories, breaking changes, or major version releases noted.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the **OpenCode Community Digest** for **June 19, 2026**.

---

## Today's Highlights
The community is buzzing with two major feature breakthroughs: multiple competing PRs landed for a native **`/goal`** session lifecycle system, and a critical fix for **inotify exhaustion** on Linux prevents OpenCode from hanging at startup. The v1.16.0 release is also driving significant bug reports regarding TUI rendering regressions and plugin provider hooks. A high-impact bug related to **Deepseek API token over-billing** is generating significant concern.

## Releases
No new releases were published in the last 24 hours. The community is currently active on the v1.16.0 and v1.17.x branches.

## Hot Issues
Top 10 noteworthy issues updated in the last 24 hours.

1.  **#27167: [FEATURE] Add native session goals with /goal**
    - **Why it matters:** The most upvoted feature request this week (88 👍). Proposes replacing custom slash commands with a persistent, lifecycle-aware session goal system.
    - **Community:** 51 comments, high engagement.
    - **Link:** [Issue #27167](https://github.com/anomalyco/opencode/issues/27167)

2.  **#27589: TUI fails on Alpine Linux (musl): getcontext symbol not found**
    - **Why it matters:** A regression breaking OpenCode for all musl-based Linux users, blocking adoption on Alpine and other lightweight distros.
    - **Community:** 35 comments, high urgency.
    - **Link:** [Issue #27589](https://github.com/anomalyco/opencode/issues/27589)

3.  **#16610: Opencode hangs at startup if inotify user instances run out**
    - **Why it matters:** A long-standing crash issue on Linux when system file watcher limits are low. A fix PR (#32930) has landed today.
    - **Community:** 12 comments, relief likely pending merge.
    - **Link:** [Issue #16610](https://github.com/anomalyco/opencode/issues/16610)

4.  **#30877: TUI sidebar "Modified Files" section completely hidden (v1.16.0)**
    - **Why it matters:** A critical TUI regression for v1.16.0 users. The "Modified Files" panel is missing entirely, breaking the core review workflow.
    - **Community:** 5 comments, 8 👍.
    - **Link:** [Issue #30877](https://github.com/anomalyco/opencode/issues/30877)

5.  **#25630: Plugin provider.models() hook regression (post #25167)**
    - **Why it matters:** Plugin authors can no longer register models for custom providers. This severely impacts the extensibility ecosystem.
    - **Community:** 12 comments, 3 👍.
    - **Link:** [Issue #25630](https://github.com/anomalyco/opencode/issues/25630)

6.  **#8456: [FEATURE] Auto-select models based on task type**
    - **Why it matters:** High demand (37 👍) for intelligent model routing (e.g., cheap model for linting, expensive model for architecture). Users want a "modes" system similar to competitors.
    - **Community:** 9 comments.
    - **Link:** [Issue #8456](https://github.com/anomalyco/opencode/issues/8456)

7.  **#5391: [FEATURE] Multiple auth profiles per provider**
    - **Why it matters:** Users need to switch between billing accounts or API keys (e.g., personal vs. work) without editing config files. 31 👍.
    - **Community:** 11 comments.
    - **Link:** [Issue #5391](https://github.com/anomalyco/opencode/issues/5391)

8.  **#32911: Deepseek API burning too many tokens**
    - **Why it matters:** A confirmed bug in v1.17.x causing severe over-billing for Deepseek users. High financial impact.
    - **Community:** 2 comments, linked to Reddit thread.
    - **Link:** [Issue #32911](https://github.com/anomalyco/opencode/issues/32911)

9.  **#32704: Bash tool description references Edit/Write tools when unavailable**
    - **Why it matters:** A safety/UX bug where the model’s tool description claims file-editing is available even when the user has disabled it.
    - **Community:** 4 comments.
    - **Link:** [Issue #32704](https://github.com/anomalyco/opencode/issues/32704)

10. **#32747: @ file mentions do not include files created after startup**
    - **Why it matters:** Breaks the "just create a file and reference it" workflow. Requires restart to re-index.
    - **Community:** 2 comments.
    - **Link:** [Issue #32747](https://github.com/anomalyco/opencode/issues/32747)

## Key PR Progress
Top 10 important pull requests updated in the last 24 hours.

1.  **#32924: feat: add native /goal foundation**
    - **Why it matters:** Directly addresses the top-voted feature (#27167). Implements workspace-local goal state machine with persistence and events.
    - **Author:** abyssbugg
    - **Link:** [PR #32924](https://github.com/anomalyco/opencode/pull/32924)

2.  **#32743: feat(session): native per-session goals with /goal**
    - **Why it matters:** A competing implementation for the same feature, offering autonomous goal pursuit.
    - **Author:** dfredriksen
    - **Link:** [PR #32743](https://github.com/anomalyco/opencode/pull/32743)

3.  **#32930: fix(core): prevent hang when inotify watches are exhausted**
    - **Why it matters:** Fixes #16610. Changes the `.git` watcher to use a recursive strategy instead of per-file subscriptions, drastically reducing watch count.
    - **Author:** sailod
    - **Link:** [PR #32930](https://github.com/anomalyco/opencode/pull/32930)

4.  **#32916: feat(provider): add noumena provider**
    - **Why it matters:** Adds first-class OAuth support for a new provider (Noumena) including browser and manual flows. Expands model access.
    - **Author:** altendky
    - **Link:** [PR #32916](https://github.com/anomalyco/opencode/pull/32916)

5.  **#32854: fix(core): tolerate file watcher startup failures**
    - **Why it matters:** Related to inotify issues. Makes watcher failures non-fatal, logging a warning instead of crashing the TUI.
    - **Author:** sailod
    - **Link:** [PR #32854](https://github.com/anomalyco/opencode/pull/32854)

6.  **#32624: fix(shell): apply external_directory check to redirect targets**
    - **Why it matters:** Security fix. The shell tool now properly gates redirect targets (`>`, `>>`) through the `external_directory` sandbox.
    - **Author:** warmjademe
    - **Link:** [PR #32624](https://github.com/anomalyco/opencode/pull/32624)

7.  **#32929: feat(experimental): surface AXI tools alongside MCP resources**
    - **Why it matters:** Experimental integration making AXI CLI tools visible in the `@` autocomplete, bridging local tooling with MCP.
    - **Author:** davidgut1982
    - **Link:** [PR #32929](https://github.com/anomalyco/opencode/pull/32929)

8.  **#32398: feat(app): add session file list and desktop backgrounds**
    - **Why it matters:** UX improvement adding a file browser tab to the side panel, reducing need to switch to IDE.
    - **Author:** liwanspecial
    - **Link:** [PR #32398](https://github.com/anomalyco/opencode/pull/32398)

9.  **#32927: feat(tui): surface compaction progress and context usage indicators**
    - **Why it matters:** Solves user confusion when the UI appears frozen during context compaction.
    - **Author:** MoerAI
    - **Link:** [PR #32927](https://github.com/anomalyco/opencode/pull/32927)

10. **#30102: feat(i18n): add Vietnam (vi) locale support**
    - **Why it matters:** Continues the strong community trend of locale contributions.
    - **Author:** Mytai20100
    - **Link:** [PR #30102](https://github.com/anomalyco/opencode/issues/30102)

## Feature Request Trends
The following themes dominate the recent feature requests:

- **Session Lifecycle Management:** The `/goal` command (###27167, ###32743, #32924) is the single most requested feature. Users want persistent, inspectable, and pausable goals rather than ephemeral chat commands.
- **Intelligent Model Routing:** There is strong demand for automatic model selection based on task complexity (###8456). Developers want to use cheaper models for quick edits and expensive reasoning models for architecture.
- **Identity & Access Management:** Multiple auth profiles per provider (###5391) is a top request. Users need to quickly switch between API keys or billing accounts without editing configs.
- **Visual Indicators for Agent State:** Users want the TUI to show what "mode" or "skill" an agent is using (###32917, #32918) and when context is being compacted (###32927).

## Developer Pain Points
Recurring frustrations based on high-frequency issues:

- **File Watcher Reliability (Linux):** The inotify exhaustion bug (###16610, #32930) is a persistent pain point for Linux devs, causing hard hangs on startup.
- **Stale Index / File Detection:** The TUI frequently fails to pick up newly created files for `@` mentions (###32747), requiring restarts.
- **Plugin Hook Breakage:** The `provider.models()` API regression (###25630) is disrupting the plugin ecosystem, making third-party providers non-functional.
- **Token Over-Billing:** The Deepseek API bug (###32911) is causing real financial loss, making it a high-priority blocker for users on that provider.
- **Post-Update Corruption:** Windows users report self-update processes leaving corrupted executables (###28072, ###30855), breaking the application entirely.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-19

## Today's Highlights
A packed 24 hours for Pi with **v0.79.7** shipping automatic theme mode — allowing separate light/dark themes that follow terminal color-scheme events. The community is buzzing around UX improvements: parallel edit tool calls overwriting each other remains the top complaint (14 comments), while a new feature request for **multiple live agent sessions with TUI switching** (#5700) signals growing demand for multi-agent workflows. Two significant PRs landed — OpenRouter Fusion alias support and a fix for orphaned tool results on Moonshot AI.

---

## Releases
### v0.79.7
- **Automatic theme mode** – `/settings` now supports separate light and dark themes, automatically following terminal color-scheme changes. See [Selecting a Theme docs](https://github.com/earendil-works/pi/blob/v0.79.7/packages/coding-agent/docs/themes.md#selecting-a-theme).
- **Self-only updates** by default (full details truncated in source).

---

## Hot Issues (Top 10)

1. **[#1278] tui: make @ file autocomplete async/streaming (fd)** — [Link](https://github.com/earendil-works/pi/issues/1278)
   - *Why it matters:* `@` autocomplete blocks the UI on large repos. Streaming `fd` results would keep typing responsive. High community demand: **14 comments, 16 👍**.
   - *Status:* CLOSED — solution merged.

2. **[#2327] [bug] Parallel edit tool calls on the same file overwrite each other** — [Link](https://github.com/earendil-works/pi/issues/2327)
   - *Why it matters:* When LLM agents issue simultaneous edits to the same file, only the last one takes effect — silent data loss. **7 comments**.
   - *Community reaction:* Reporter calls the behavior "totally stupid" — frustration is high.

3. **[#5700] [OPEN] Support multiple live agent sessions with TUI switching** — [Link](https://github.com/earendil-works/pi/issues/5700)
   - *Why it matters:* Currently `switchSession` tears down the current session — you can't run background agents. This request wants concurrent sessions with TUI tab switching. **6 comments, still OPEN**.

4. **[#2469] [bug] Clipboard image paste to WSL silently fail** — [Link](https://github.com/earendil-works/pi/issues/2469)
   - *Why it matters:* Windows + WSL users can't paste screenshots. **4 👍** indicate this affects many developers on Windows.

5. **[#5463] [OPEN] fix(coding-agent): auto-compaction after final turn throws error** — [Link](https://github.com/earendil-works/pi/issues/5463)
   - *Why it matters:* Session-ending compaction crashes with `Cannot continue from message role: assistant`. **5 👍** from users hitting this edge case.

6. **[#2022] [bug] Cannot disable thinking for Qwen3.5-plus via Anthropic API compatibility** — [Link](https://github.com/earendil-works/pi/issues/2022)
   - *Why it matters:* Users explicitly set `reasoning: false` but thinking still runs. Integration with Aliyun models is broken.

7. **[#5468] MiniMax-M3 via minimax-cn: tool replay sends unknown tool IDs** — [Link](https://github.com/earendil-works/pi/issues/5468)
   - *Why it matters:* Long sessions (248 tool calls) produce 400 errors from MiniMax because tool result IDs don't match server state. Only compaction or model switch recovers.

8. **[#2055] Oversized image in tool result causes infinite error loop** — [Link](https://github.com/earendil-works/pi/issues/2055)
   - *Why it matters:* Images >5MB stay in message history, causing every subsequent API call to fail with 400 errors. No recovery without manual intervention.

9. **[#5854] [CLOSED] Enable prompt caching for mistral provider** — [Link](https://github.com/earendil-works/pi/issues/5854)
   - *Why it matters:* Mistral API supports prompt caching but Pi doesn't use it — users miss out on cost savings and latency reduction.

10. **[#2447] optimize truncateToWidth for large strings** — [Link](https://github.com/earendil-works/pi/issues/2447)
    - *Why it matters:* Large first messages make the session switcher extremely slow. Simple optimization with high UX impact.

---

## Key PR Progress (Top 10)

1. **[#5874] feat(coding-agent): add automatic theme mode** — [Link](https://github.com/earendil-works/pi/pull/5874)
   - *Description:* Ships the marquee feature of v0.79.7 — dual light/dark themes following terminal color-scheme events.
   - *Author:* mitsuhiko | MERGED

2. **[#5866] feat(ai): add OpenRouter Fusion alias** — [Link](https://github.com/earendil-works/pi/pull/5866)
   - *Description:* Adds `openrouter/fusion` synthetic router alias, matching the existing `openrouter/auto` pattern. Keeps tool-capable model filter unchanged.
   - *Author:* dannote | MERGED

3. **[#5884] fix(ai): handle orphaned tool result messages to prevent Moonshot 400 errors** — [Link](https://github.com/earendil-works/pi/pull/5884)
   - *Description:* Guards against tool result messages without preceding assistant tool_calls — strict OpenAI providers (like Moonshot) reject these with 400.
   - *Author:* g-pelletier | MERGED

4. **[#5841] feat(tui): detect Warp terminal and enable Kitty image protocol** — [Link](https://github.com/earendil-works/pi/pull/5841)
   - *Description:* Enables Kitty graphics protocol and OSC 8 hyperlinks for Warp terminal users (TERM_PROGRAM detection).
   - *Author:* dodiego | MERGED

5. **[#5756] feat(coding-agent): Expose edit-diff for extensions** — [Link](https://github.com/earendil-works/pi/pull/5756)
   - *Description:* Closes #5755 by making edit diffs available to extension hooks — enables richer extension-based review workflows.
   - *Author:* xl0 | MERGED

6. **[#5846] [OPEN] fix(tui): stabilize streaming code fence rendering** — [Link](https://github.com/earendil-works/pi/pull/5846)
   - *Description:* Fixes #5825 — code fences flicker or misrender during streaming. Still under review.
   - *Author:* xl0 | OPEN

7. **[#5796] chore: bump TS target and lib to ES2024, use Promise.withResolvers()** — [Link](https://github.com/earendil-works/pi/pull/5796)
   - *Description:* Modernizes the codebase to ES2024, replacing hand-rolled `Promise.withResolvers()` polyfills.
   - *Author:* Perlence | MERGED

8. **[#5812] fix(tui): protect pipe characters inside inline code in markdown tables** — [Link](https://github.com/earendil-works/pi/pull/5812)
   - *Description:* Fixes table rendering when cells contain `|` in backticks — previously split on those pipes, losing content.
   - *Author:* aliou | MERGED

9. **[#5873] Feat/fireworks glm 5p2** — [Link](https://github.com/earendil-works/pi/pull/5873)
   - *Description:* Adds GLM-5P2 model support for Fireworks provider. Builds on #5801, closes #5872.
   - *Author:* o1lo01ol1o | MERGED

10. **[#5348] Add selective pi-ai base entrypoints** — [Link](https://github.com/earendil-works/pi/pull/5348)
    - *Description:* Side-effect-free base entrypoints for selective transport bundling — reduces bundle size for custom builds.
    - *Author:* FredKSchott | MERGED

---

## Feature Request Trends
- **Multi-agent session management** — The top open request (#5700) wants concurrent agent sessions with TUI switching. This reflects growing adoption where Pi handles multiple parallel coding tasks.
- **Model/provider parity** — Requests for prompt caching (Mistral #5854), thinking control (Qwen #2022), and provider-specific feature support (MiniMax #5468, Moonshot #5884) show users want equal capabilities across all backends.
- **Terminal ecosystem compatibility** — Wars, JetBrains, WSL, Termux — users need Pi to detect and adapt to each terminal's capabilities (Kitty protocol, OSC 8, keyboard events).

---

## Developer Pain Points
- **Thread safety in concurrent tool execution** — #2327 (parallel edits overwriting each other) and #2557 (conflicting edits not detectable by extensions) point to a core reliability gap when agents use multiple tools simultaneously.
- **Error recovery from oversized or orphaned content** — #2055 (images >5MB) and #5468 (tool ID mismatches) trap users in infinite error loops with no recovery mechanism — a major frustration.
- **Extension development friction** — Poorly exported types (#2458), missing events (#2543, #2576), and fragile dependency resolution (#2252) make building extensions harder than it should be.
- **Configuration staleness** — Issues like scoped models not reflecting edits (#2408), themes ignoring export settings (#2565), and custom keybinds not overriding defaults (#2391) erode trust in the settings system.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-19

## Today's Highlights
Today marks a major **security and correctness push** across the codebase, with 15+ issues and PRs focused on path validation, token storage, and sandbox boundary enforcement. A prolific contributor (`tt-a1i`) has filed and fixed a series of subtle but high-impact bugs spanning MCP retry logic, OAuth expiry handling, and cron parsing. Community interest in **usage tracking** (token consumption) and **QQ Bot integration** remains high, with the QQ channel adapter now merged.

## Releases
**None** — No new versions were published in the last 24 hours.

## Hot Issues (Top 10)

1. **#4479 — Token consumption statistics** [CLOSED]  
   *Community's most commented issue (16 comments)*  
   A user discovered they consumed 30 million tokens in a single session, requesting a daily token usage dashboard. This reflects growing demand for cost observability.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4479)

2. **#4987 — Silent revert via PR merge** [CLOSED]  
   PR #4779 reverted a previously merged feature (#4652) without explanation. Highlights a process gap in merge conflict resolution. Community reaction: 5 comments, all flagging process improvements.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4987)

3. **#5261 — Collapsible thinking block broken in v0.18.2** [CLOSED]  
   After upgrading, the "Thought for 1s" timer shows but the thinking content is not expandable. No shortcut exists. Key UX regression for reasoning model users.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5261)

4. **#5147 — OOM on `/quit` with managed auto-memory** [CLOSED]  
   Even with earlier structuredClone fixes, short sessions OOM during exit when auto-memory builds transcripts from large histories. Points to unresolved memory management in background tasks.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5147)

5. **#5201 — QQ Bot channel adapter** [CLOSED]  
   A complete PR-ready implementation for QQ Bot WebSocket gateway. Community enthusiasm: 3 comments, fast-tracked to PR.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5201)

6. **#5381 — MCP retry reconnects on non-connection errors** [OPEN]  
   `handleReconnectOnError` catches ordinary tool errors (e.g., invalid params) and triggers reconnection, potentially hiding real issues. 2 comments, active discussion.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5381)

7. **#5376 — Search tools ignore tilde path expansion** [OPEN]  
   RipGrep/Glob/Grep permission checks use raw `path.resolve` while execution uses `resolveAndValidatePath`, creating a bypass for `~/secret` paths. **P1 priority** — security concern.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5376)

8. **#5373 — Sandbox path checks treat siblings as workspaces** [OPEN]  
   Raw prefix matching (`startsWith`) means `/repo/app` also matches `/repo/application`. Could allow sandbox escape. 2 comments, welcome-pr.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5373)

9. **#5368 — MCP/extensions ignore untrusted workspace state** [CLOSED]  
   `isWorkspaceTrusted()` returns a `TrustResult` object but code casts it to boolean — both `{ isTrusted: true }` and `{ isTrusted: false }` evaluate as `true`. **All trust checks are effectively disabled.**  
   [Link](https://github.com/QwenLM/qwen-code/issues/5368)

10. **#5244 — Windows desktop ghost sessions `(session)`** [CLOSED]  
    After skill/tool tasks, extra empty sessions named `(session)` appear in the list. Affects Windows desktop users. 2 comments, Chinese-language report.  
    [Link](https://github.com/QwenLM/qwen-code/issues/5244)

## Key PR Progress (Top 10)

1. **#5382 — Fix MCP reconnection on tool errors** [OPEN]  
   Stops reconnecting for non-connection errors. Direct response to #5381.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5382)

2. **#5378 — Tilde path resolution for search tools** [OPEN]  
   Aligns permission checks with execution path resolution. Fixes #5376.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5378)

3. **#5380 — Top-level MCP callable error detection** [OPEN]  
   Treats `response.isError` as a tool error in the callable fallback path.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5380)

4. **#5377 — Preserve equals signs in MCP env values** [OPEN]  
   Splits on first `=` only, not all. Required for tokens/base64 values. Fixes #5374.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5377)

5. **#5372 — Parse grep results with colon paths** [OPEN]  
   Adds NUL-delimited output handling for `git grep -z` and `grep --null`. Fixes #5370.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5372)

6. **#5375 — Sandbox path boundary enforcement** [OPEN]  
   Replaces string-prefix check with path-segment boundary check. Fixes #5373.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5375)

7. **#5202 — QQ Bot channel adapter (MERGED)** [CLOSED]  
   New `@qwen-code/channel-qqbot` package with full WebSocket gateway support. Community contribution.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5202)

8. **#5145 — Follow-up suggestion in input placeholder** [OPEN]  
   Shows the model's suggested next prompt directly in the input field using the fast model. UX improvement.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5145)

9. **#5258 — Stop turn on cancelled permissions** [CLOSED]  
   Makes ACP permission cancellation stop the current turn for all tool types, not just `ask_user_question`.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5258)

10. **#5364 — Avoid glob prefix cache reuse** [OPEN]  
    Non-exact glob queries now evaluate from full file list instead of cached prefix set. Prevents stale results.  
    [Link](https://github.com/QwenLM/qwen-code/pull/5364)

## Feature Request Trends

- **Token Usage Analytics** — Multiple users (e.g., #4479) want daily/weekly token consumption dashboards. Cost observability is the #1 missing feature.
- **Estimated Response Time** — #5366 and #4899 request optional display of remaining generation time.
- **QQ Bot Integration** — #5201 / #5202 shows strong East Asian community demand for QQ channel support, now merged.
- **Platform Channel Expansions** — The QQ Bot addition continues the trend of multi-channel support (Telegram, WeChat, DingTalk, Feishu, now QQ).
- **Session Recovery** — #5147 OOM on exit and #5244 ghost sessions suggest users want more robust session lifecycle management.

## Developer Pain Points

- **Trust/Security Model Fragility** — Three separate issues (#5368, #5376, #5373) reveal fundamental flaws in workspace trust, path validation, and sandbox boundary checks. Trust is effectively disabled due to boolean coercion.
- **MCP Edge Cases** — Retry-on-error (#5381), missing `isError` detection (#5379), `expires_in=0` handling (#5355), and env value truncation (#5374) suggest MCP integration needs hardening.
- **Cron/Schema Parser Validation** — Four issues (#5348, #5310, #5322, #5304) show that parsers across the system (cron, OpenAI schema, MCP prompts, OSC codes) accept malformed input silently — a recurring theme of weak input validation.
- **Memory Management on Exit** — #5147 persists even after prior fixes, indicating managed auto-memory lacks proper cleanup for large histories.
- **Windows/Desktop Regressions** — #5244 (ghost sessions) and #5261 (broken collapsible blocks in v0.18.2) highlight that Windows/UI paths receive less testing.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (CodeWhale) Community Digest — 2026-06-19

## Today's Highlights
The project is in the midst of a major **rebranding to CodeWhale**, with v0.8.62 dropping the legacy `deepseek-tui` npm package. A wave of architectural refactoring issues—focused on splitting monolithic Rust files—was filed by core maintainers, signaling a concerted push toward maintainability as v0.9.0 approaches. Reliability remains the top community concern, with multiple open bugs around UI freezes, turn stalls, and agent overreach persisting across recent releases.

## Releases
**v0.8.62** — Renamed to **CodeWhale** as the canonical project, command, npm package, and release-asset name. The legacy `deepseek-tui` npm package is deprecated and receives no further releases. Users on v0.8.x legacy names (`deepseek` / `deepseek-tui`) should migrate using `docs/REBRAND.md`.

## Hot Issues (Top 10)

1. **[#2487] Frequent error: Turn stalled — no completion signal received** — The top-voted open issue (16 comments). Users in `yolo` mode experience freezes where the agent becomes unresponsive, and even `continue` commands fail to resume. Persists across multiple versions. [Link](https://github.com/Hmbown/CodeWhale/issues/2487)

2. **[#1812] TUI freeze on Windows 11 (crossterm poll)** — 7 comments. The UI becomes completely unresponsive while the process stays alive. Two confirmed events with logs and thread-state analysis. Affects Windows users specifically. [Link](https://github.com/Hmbown/CodeWhale/issues/1812)

3. **[#3275] Agent overreach: self-questioning, self-answering, deviating from user intent** — 5 comments. Marked as a regression from #3061. The agent consistently extends scope beyond user requests, entering a self-driven loop without waiting for confirmation. Serious trust/control issue. [Link](https://github.com/Hmbown/CodeWhale/issues/3275)

4. **[#3289] UI freezes after auto-spawning several sub-agents** — 4 comments. Plan mode users experience freezes when CodeWhale spawns multiple sub-agents during conversation. Escalates from plan refinement into full unresponsiveness. [Link](https://github.com/Hmbown/CodeWhale/issues/3289)

5. **[#3240] Legacy `.deepseek` config directory still created despite rebrand** — 3 comments. On Windows, both `.codewhale` and `.deepseek` folders are created in the user directory. Incomplete migration cleanup. [Link](https://github.com/Hmbown/CodeWhale/issues/3240)

6. **[#3238] Does not work on Ubuntu 22.04 LTS — glibc version mismatch** — 3 comments. Installing via `npm install -g codewhale` fails on older LTS distributions due to dynamic linking against a newer glibc. [Link](https://github.com/Hmbown/CodeWhale/issues/3238)

7. **[#3273] `js_execution` Node fetch ignores proxy config on Windows** — 2 comments. Shell tools respect VPN/proxy settings, but the built-in JS execution tool times out with Undici connect timeout even when proxy env vars are set. [Link](https://github.com/Hmbown/CodeWhale/issues/3273)

8. **[#2900] DSML calls output as plain text instead of executing** — 2 comments. The model sometimes emits DSML as raw text for minutes, bloating context. Triggers randomly but then becomes persistent. [Link](https://github.com/Hmbown/CodeWhale/issues/2900)

9. **[#2608] Refactor: extract provider registry from ballooning config files** — 2 comments. `crates/config/src/lib.rs` is now 4,719 lines and `crates/tui/src/config.rs` is 9,402 lines. Every new provider requires updating 15-30 match arms. Serious maintainability debt. [Link](https://github.com/Hmbown/CodeWhale/issues/2608)

10. **[#3258] app-server: fail fast for non-loopback bind without explicit auth** — 1 comment. Running `codewhale app-server --host 0.0.0.0` without `--auth-token` or `--insecure-no-auth` silently proceeds, potentially exposing the server. [Link](https://github.com/Hmbown/CodeWhale/issues/3258)

## Key PR Progress (Top 10)

1. **[#3317] fix(cli): tear down delegated serve/app-server child on dispatcher exit** — Proactively kills the `codewhale-tui` child process when the dispatcher exits, preventing orphaned listeners (refs #3259). [Link](https://github.com/Hmbown/CodeWhale/pull/3317)

2. **[#3300] feat(tui): preserve thinking/tool blocks when seeding thread from session** — Replaces text-only thread seeding with block-type-aware implementation, preserving ContentBlock variants (Thinking, ToolUse, ToolResult) for full conversation reconstruction. [Link](https://github.com/Hmbown/CodeWhale/pull/3300)

3. **[#3301] feat(tui): save ask permission rules from approvals** — Adds an ask-only approval UI action that persists shell approvals as `permissions.toml` rules. Includes TOML preview in the approval modal and a new `s` shortcut. [Link](https://github.com/Hmbown/CodeWhale/pull/3301)

4. **[#3290] fix(prompts): add scope_discipline rules to prevent self-questioning agent loops** — Direct fix for #3273. Adds 47 lines of constitution rules to prevent the agent from entering self-questioning/self-answering loops that deviate from user intent. [Link](https://github.com/Hmbown/CodeWhale/pull/3290)

5. **[#3285] fix(tui): persist session before stall/cancel recovery so `--continue` keeps history** — Fixes #2739 (partial). The stall watchdog and cancel paths now save session state before clearing turn bookkeeping, so `--continue` loads actual progress. [Link](https://github.com/Hmbown/CodeWhale/pull/3285)

6. **[#3274] feat(release): build static Linux x64 binaries with musl** — Switches release builds from dynamic glibc to static musl, resolving the Ubuntu 22.04 incompatibility (fixes #3238). [Link](https://github.com/Hmbown/CodeWhale/pull/3274)

7. **[#3286] fix(tui): ensure `type:object` on Kimi parameters root for all schema shapes** — Fixes #3281. Broadens the `sanitize_for_kimi_parameters` check to handle `$ref`, `allOf`, `anyOf`, `oneOf` root schemas that were previously rejected with 400 errors by Kimi/Moonshot. [Link](https://github.com/Hmbown/CodeWhale/pull/3286)

8. **[#3242] feat: add `workspace_follow_symlinks` setting** — Enables walk-based tools and UI components to follow symbolic links during directory traversal. Configurable per-workspace. [Link](https://github.com/Hmbown/CodeWhale/pull/3242)

9. **[#3293] fix(tui): respect `snapshots.enabled` for per-tool snapshots** — Fixes #3292. Per-tool snapshots were writing commits even when `snapshots.enabled = false`. Adds the missing guard from the pre/post-turn snapshot logic. [Link](https://github.com/Hmbown/CodeWhale/pull/3293)

10. **[#3296] Gate cross-tool skill discovery** — Adds `[skills].scan_codewhale_only` setting to restrict session-time skill scanning to `~/.codewhale/skills/`, improving performance and security. [Link](https://github.com/Hmbown/CodeWhale/pull/3296)

## Feature Request Trends

- **Workrooms & asynchronous execution**: Multiple issues and RFCs around Workrooms (durable, addressable threaded agent conversations) and WhaleFlow (real async executor with bounded concurrency, cancellation, budgets, and synthesis/reduce passes). This is shaping up as the v0.9.0 headline feature.
- **Sub-agent control surfaces**: Strong demand for editable sub-agent recursion depth and concurrency limits from the TUI (#3304), plus better visibility into sub-agent lifecycle and outputs.
- **Permission/approval UX improvements**: Users want granular ask-only permission rules persisted as `permissions.toml`, real-time approval previews, and provenance tracking for write/continue approvals to prevent agent overreach (#3315, #3301).
- **Provider extensibility**: A systematic push to extract the provider registry from monolithic config files into a proper registry crate, making it easier to add new LLM backends without touching dozens of match arms (#2608, #3311).
- **Documentation & terminology alignment**: A documented push toward consistent public-facing naming ("Agents" and "Workflows") with implementation terms (sub-agent, Fleet, WhaleFlow, Workroom) kept internal (#3316).

## Developer Pain Points

- **Recurring UI freezes across platforms**: Windows crossterm polling freezes (#1812), Linux glibc version mismatch (#3238), and sub-agent-induced stalls (#3289) are hitting users on every major platform. The "Turn stalled" error (#2487) remains the most-upvoted open issue.
- **Agent overreach and trust**: The self-questioning/self-answering loop (#3275) and Plan→Agent mode toggle inconsistency (#3279) erode user trust. Multiple fixes are in flight, but the community is clearly frustrated by agents executing without confirmation.
- **Session/data loss on crash**: Users report losing in-progress conversation history when recovering from stalls or cancelling with Esc (#2739). The `--continue` flag loading stale sessions is a persistent pain point, though PR #3285 addresses part of this.
- **Incomplete rebrand**: Despite v0.8.62 renaming to CodeWhale, legacy `.deepseek` configuration directories are still created on Windows (#3240) and onboarding markers are duplicated. Inconsistencies confuse migrating users.
- **Monolithic codebase maintenance**: The maintainers themselves are filing issues to split massive source files (9,402-line `config.rs`, 4,719-line `lib.rs`, 2,400-line `RuntimeThreadManager`). This indicates the project has grown faster than its code organization, and refactoring debt is now a top priority.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*