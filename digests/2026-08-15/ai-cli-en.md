# AI CLI Tools Community Digest 2026-08-15

> Generated: 2026-08-15 00:30 UTC | Tools covered: 9

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
**Date:** 2026-08-15

---

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem is in a phase of rapid maturation marked by intense competition across performance, platform parity, and agentic reliability. Claude Code, OpenAI Codex, and Gemini CLI lead in release velocity, while specialized tools like Qwen Code, Pi, and CodeWhale (formerly DeepSeek TUI) are carving out distinct niches. Cross-tool community feedback converges on several systemic challenges: Windows platform support remains uniformly weak across nearly all tools, context management (compression, persistence, and budgeting) is universally problematic, and silent failures—where tools report success despite not completing work—are eroding developer trust. Meanwhile, an architectural shift is underway toward sub-agent hierarchies, dynamic model discovery, and provider-agnostic protocols, signaling the ecosystem's evolution from single-session assistants to distributed agent platforms.

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | PRs (24h) | Release Status | Notable Signals |
|---|---|---|---|---|
| **Claude Code** | 10+ tracked; #69238 (96👍) long-running API error | 4 (1 feature, 1 fix, 2 minor) | v2.1.233 shipped (GitLab MR support, identity forwarding) | Billing anomalies cluster; safety-filter false positives |
| **OpenAI Codex** | 10 tracked; Windows perf cluster dominant | 10+ (all TUI/sandbox/protocol hardening) | 5 alpha releases (v0.148.0-a.14→a.18), placeholder notes | Rapid Rust iteration; sandbox permission enforcement |
| **Gemini CLI** | 10 tracked; #21409 generalist hang (8👍) | 10+ (7 P1 fixes, 2 large features) | v0.56.0-nightly.20260814 | MAX_TURNS misreporting fixed; subagent delegation coming |
| **GitHub Copilot CLI** | 10 tracked; MCP OAuth RFC 8414 cluster | 3 (2 merged, 1 open) | v1.0.80, v1.0.81-0 shipped | Enterprise model gating issues; security hardening PRs |
| **Kimi Code CLI** | 4 updated; Memory System #1283 (39 comments) | 0 | No releases | Quiet day; memory system remains top ask |
| **OpenCode** | 10 tracked; #42608 48-bit ID wraparound (critical) | 10 (5 open, 5 closed/merged) | No release (stable v1.18.x) | Critical session-wedge bug; dynamic model discovery landing |
| **Pi** | 10 tracked; WSL/Windows #7547 (27 comments) | 10 (mix of fixes and features) | v0.84.2 shipped (fullscreen search) | Provider-specific hotfixes; TUI perf issues |
| **Qwen Code** | 10 tracked; arch refactor + CI flakiness | 10+ (review/autofix infra) | v0.21.12 + v0.21.12-preview.4 | Architectural refactoring; Web Shell expansion |
| **CodeWhale (DeepSeek TUI)** | 10 tracked; rebranding fallout | 10 (all merged, fix-heavy) | v0.9.8 (CodeWhale rebrand) | CI cascades post-rebrand; schema simplification |

---

## 3. Shared Feature Directions

**Context & Memory Management (Demanded Across: Kimi, Claude Code, OpenAI Codex, Gemini CLI, OpenCode, Pi)**
- Persistent memory across sessions (#1283 Kimi, #30869 Claude Code, #26522 Gemini CLI)
- Reliable context compression: Codex's compact fails ~85% (#31375); Claude Code's auto-compact fires at wrong thresholds (#85205); OpenCode wants smarter cache reuse (#37489)
- Transparent context-window reasoning and budgeting

**Sub-Agent Architecture & Delegation (Gemini CLI, OpenCode, CodeWhale, Claude Code)**
- Agents calling agents: Gemini CLI PR #28738; OpenCode subagent ID validation (#36883)
- Sub-agent reliability: Gemini MAX_TURNS misreporting (#22323); CodeWhale stale write-claims (#5372)
- Visible sub-agent trajectories and better ID schema simplification (#5324 CodeWhale)

**Dynamic Model Discovery & Provider-Agnosticism (OpenCode, Copilot CLI, Pi, Kimi)**
- Auto-discover models via `/v1/models` (OpenCode PR #42660, #27554)
- Model catalog freshness for enterprise (Copilot CLI #4390, #4422)
- Provider parity gaps: Bedrock Ultra reasoning (Codex #37160), z.ai GLM-5.1 drift (Pi #8096)

**Windows/WSL Platform Parity (Codex, Claude Code, Gemini CLI, Pi, OpenCode, Qwen Code)**
- Performance regressions (Codex Windows stutter cluster 7 of top 10 issues)
- Git Bash permission spam (Claude Code #86619)
- WSL clipboard gaps (Gemini CLI #27588), Windows ripgrep EFTYPE (#25378)
- Pi's WSL auth hangs (#6187), OpenCode WSL SIGKILL (#42626)

**Permission & Safety Guardrails (Claude Code, Gemini CLI, Copilot CLI, CodeWhale)**
- False-positive safety blocks (Claude Code cluster; Gemini #22672)
- Configurable approval defaults (CodeWhale #5293)
- Cross-session write safety (Copilot CLI #4491 — /spawn can inject into unrelated sessions)

**Billing Transparency (Claude Code, Codex, OpenCode)**
- Silent cost drains (#86794, #83062 Claude Code); rate limit reset bugs (Codex #37442, #38652); credit not reflecting (OpenCode #42606, #42637)

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach |
|---|---|---|---|
| **Claude Code** | Enterprise-grade stability, GitLab/GitHub PR integration | Professional developers in orgs | Mature TUI + desktop; worktree-oriented; strong safety filter (sometimes overly aggressive) |
| **OpenAI Codex** | Fast-moving TUI + desktop with sandboxing | Developers wanting bleeding-edge features | Rust codebase; aggressive alpha cadence; sandbox permission profiles; gRPC protocol |
| **Gemini CLI** | Sub-agent orchestration, memory quality, AST-aware tools | Power users running agent hierarchies | Node/TypeScript; MessageBus architecture; PTY management focus; memory extraction agent |
| **Copilot CLI** | Enterprise GitHub/Copilot integration, autopilot/fleet mode | GitHub-centric orgs | Tight coupling to Copilot platform; MCP server support; OAuth flow management |
| **Kimi Code** | Persistent memory, session handoff | Multi-device developers | Small community; memory system as #1 gap; Windows fixes shipping |
| **OpenCode** | Protocol-driven extensibility, provider-agnostic | Developers with custom/self-hosted setups | Schema-driven protocol (V2 HttpApi); plugin adapters; dynamic model discovery |
| **Pi** | Lightweight, fast TUI; provider hotfixes | Casual-to-serious CLI users | Minimal dependencies; jiti extension system; compact transcript rendering |
| **Qwen Code** | Review/autofix infrastructure, Web Shell | Teams using Qwen models | Architectural refactors; channel-based findings; CI autofix investment |
| **CodeWhale** | DeepSeek-native experience, rebranding | DeepSeek model users | Rust toolchain; two-layer auto-review (model guardian); provider presets |

---

## 5. Community Momentum & Maturity

**Highest Momentum (Rapid Iteration + Active Communities):**
- **OpenAI Codex** — 5 releases/day, 10+ PRs, but community frustration with placeholder changelogs and unresolved Windows regressions.
- **Gemini CLI** — 10+ PRs including 7 P1 fixes; tackling deep architectural issues (subagent delegation, PTY leaks) with high community engagement.
- **Pi** — Steady release cadence (v0.84.2) with 10 PRs covering provider hotfixes and TUI improvements; strong community on WSL topics.

**Stabilizing / Post-Release Churn:**
- **CodeWhale** — Rebrand created CI cascade ("main is red" × 2), but the team fixed all within 24 hours. Community is engaged but small.
- **Qwen Code** — Active but focused on internal architecture and CI reliability rather than end-user features.

**Mature but Facing Pain Points:**
- **Claude Code** — Large community (96👍 on top issue) but long-running unresolved bugs and billing anomalies are testing trust.
- **Copilot CLI** — Quiet PR day (3), suggesting stabilization; MCP OAuth regression affecting real-world usage.

**Low Activity:**
- **Kimi Code** — No releases, no PRs; community discussion persists around memory systems.

---

## 6. Trend Signals

1. **Windows Support Is the Universal Weak Point** — Seven of Codex's top 10 issues are Windows-specific; Claude Code has Git Bash regressions; Gemini CLI still has open WSL fixes. Cross-platform parity is an underserved opportunity for any tool that solves it well.

2. **Silent Failures Are the #1 Trust Killer** — Tools reporting success when they failed (Gemini MAX_TURNS misreporting, Copilot `/spawn` context injection, OpenCode session wedge, Claude Code PR posting) dominate the highest-severity complaints. Invest in honest failure signaling.

3. **Context Management Is the Next Competitive Frontier** — Every tool has a context problem: unreliable compression (Codex), premature compaction (Claude Code), unbounded memory growth (Qwen, Gemini), and poor cache reuse (OpenCode). Tools that crack predictable, transparent context handling will win power users.

4. **Sub-Agent Hierarchies Are the Architectural Direction** — Gemini's "agents calling agents" PR, CodeWhale's schema simplification, and OpenCode's subagent ID validation all point toward delegation as the core scalability strategy. Expect this to become table stakes.

5. **Dynamic Model Discovery Is the New Onboarding Baseline** — OpenCode's two parallel PRs (#42660, #27554) for `/v1/models` auto-discovery reflect a broader demand. Users are tired of manual model listing; provider-agnostic tools need this.

6. **Billing Transparency Is a Rising Trust Issue** — Claude Code's silent credential fallback and auto-recharge bugs, plus Codex's rate-limit reset failures, suggest metering and billing are lagging behind feature development. This has direct revenue implications.

7. **Enterprise Model Gating Is Fractured** — Copilot CLI's Claude model availability issues and Codex's Bedrock gaps indicate enterprise model catalogs are inconsistent across tiers. Paying users can't access what they're promised.

8. **CI/CD Integration Is Moving from Nice-to-Have to Critical** — Qwen's autofix infrastructure, OpenCode's headless run fixes, and Claude Code's workflow PR posting failures all signal that CI integration reliability is becoming a primary use case, not an edge case.

---

*Report compiled from public GitHub community digests dated 2026-08-15. Data reflects issues, PRs, and releases captured for each tool within the preceding 24-hour window.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on the provided data.

---

### 1. Top Skills Ranking

The most-discussed Pull Requests reveal a community intensely focused on tooling reliability and practical, high-volume document generation.

- **`skill-creator` Fixes (PR #1298, #1099, #1050)** | [PR #1298](https://github.com/anthropics/skills/pull/1298), [PR #1099](https://github.com/anthropics/skills/pull/1099), [PR #1050](https://github.com/anthropics/skills/pull/1050)
  - **Functionality:** These PRs address critical bugs in the `skill-creator`'s evaluation scripts, which were incorrectly reporting `0%` recall and failing on Windows due to subprocess and encoding issues.
  - **Discussion:** The high volume of comments indicates that the inability to properly test and optimize Skill descriptions is a major pain point for Skill developers, effectively making the tool's feedback loop noisy or broken.
  - **Status:** All Open (as of data date).

- **Document Typography Skill (PR #514)** | [PR #514](https://github.com/anthropics/skills/pull/514)
  - **Functionality:** A skill designed for typographic quality control in AI-generated documents, preventing issues like orphan words, widow paragraphs, and numbering misalignment.
  - **Discussion:** Highlights a demand for "finishing" touches on AI output—quality control that goes beyond content correctness to professional presentation.
  - **Status:** Open.

- **ODT Skill (PR #486)** | [PR #486](https://github.com/anthropics/skills/pull/486)
  - **Functionality:** A comprehensive skill for creating, filling, reading, and converting OpenDocument Format files (.odt, .ods), a common requirement for open-source and ISO-standard document workflows.
  - **Discussion:** Complements the existing PDF and DOCX skills, showing a clear community drive toward a full suite of document-handling automation tools.
  - **Status:** Open.

- **Security Analyzer Skills (PR #83)** | [PR #83](https://github.com/anthropics/skills/pull/83)
  - **Functionality:** Proposes two "meta" skills: `skill-quality-analyzer` and `skill-security-analyzer`, which evaluate other Skills for structural quality and potential security vulnerabilities.
  - **Discussion:** This reflects the ecosystem's maturation, signaling a community need for governance, QA, and security tooling for the Skills themselves.
  - **Status:** Open.

- **Self-Audit Skill (PR #1367)** | [PR #1367](https://github.com/anthropics/skills/pull/1367)
  - **Functionality:** A universal skill that audits AI output before delivery, using mechanical file verification followed by a four-dimension reasoning audit to catch errors.
  - **Discussion:** This is a strong indicator of demand for reliability. The community seeks assurances that AI-generated work products are complete and correct before they are delivered.
  - **Status:** Open.

- **ServiceNow Platform Skill (PR #568)** | [PR #568](https://github.com/anthropics/skills/pull/568)
  - **Functionality:** A broad platform assistant covering scripting, architecture, and various ServiceNow modules (ITSM, ITOM, ITAM, etc.) rather than a narrow scripting helper.
  - **Discussion:** Shows demand for deep, complex enterprise platform support that can act as an assistant across an entire domain.
  - **Status:** Open.

---

### 2. Community Demand Trends

Analysis of the Issues reveals the following core demands:

- **Trust, Security, and Governance:** The most-commented issue (#492) raises a serious security concern about community skills impersonating official Anthropic skills. This, along with skill duplicates (#189) and context-window security for SharePoint (#1175), shows a critical demand for a more secure, vetted, and manageable Skills ecosystem. The community wants to trust the skills they install.

- **Reliable and Functional Tooling:** The `run_eval.py` failures (#556, #1169) are the most concrete pain point, followed by requests for org-wide sharing (#228). There is strong demand for the development workflow to just work—both in terms of functional scripts and in terms of sharing/distribution mechanisms.

- **Quality Assurance and Reasoning Audits:** The community is actively proposing and requesting skills that check AI output quality. This is evidenced by the self-audit PR, the reasoning quality gate proposal (#1385), and the agent-governance skill proposal (#412).

---

### 3. High-Potential Pending Skills

These active PRs are not yet merged but have significant discussion and could land soon:

- **The `skill-creator` Bug-Fix Cluster:** PRs #1298, #1099, and #1050 are all critical fixes for the same broken evaluation loop. The community's reliance on this tool suggests that once solutions are agreed upon, they will be merged quickly.
- **Document Handling Expansion:** PRs #514 (Typography) and #486 (ODT) represent clear gaps in the current document suite. Their functionality is well-defined, and the demand is evident, making them likely candidates for near-term merge.
- **Meta-Skills for Quality:** PR #83 (skill-quality-analyzer) and PR #1367 (self-audit) align with the community's strong focus on verification. These are ambitious but could see merge activity as the ecosystem matures.

---

### 4. Skills Ecosystem Insight

The community's most concentrated demand is for **trust and reliability**: they are actively seeking tooling for security, verification, and quality control, while struggling to fix the core development and evaluation infrastructure that builds those skills.

---

# Claude Code Community Digest — 2026-08-15

---

## 1. Today's Highlights

v2.1.233 ships GitLab merge request URL support for `--worktree` and the agents view, plus an opt-in identity forwarding setting for enterprise proxies. Meanwhile, the community is rallying around a long-running macOS API error (#69238, 96 👍) and a new Windows regression that spams permission prompts on read-only commands (#86619). A cluster of safety-filter false-positive reports (many closed) continues to surface, indicating ongoing tension between guardrails and legitimate security work.

---

## 2. Releases

**v2.1.233** — Two notable changes:
- **GitLab MR support**: The `--worktree` flag and `claude agents` view now recognize GitLab merge requests (displayed as `!N`), extending the existing GitHub/PR integration.
- **`forward_user_identity` setting**: New opt-in apps gateway setting for Anthropic upstreams that passes the signed-in user's identity as headers — useful for proxies needing per-user attribution.

No other releases in the last 24 hours.

---

## 3. Hot Issues

### 🔥 #69238 — [BUG] No response from API error when Advisor is triggered
**macOS · TUI/API · 63 comments · 96 👍** · [Link](https://github.com/anthropics/claude-code/issues/69238)
Users on Sonnet as the base model hit a dead-end "No response from API" error when the Advisor (Opus 4.8) kicks in, followed by retry loops. Long-running, heavily-upvoted — the community's top pain point right now.

### 🔥 #86619 — [BUG] Windows Git Bash: false-positive permission prompts on read-only commands (since 2.1.232)
**Windows · Bash/permissions · 9 comments · 9 👍** · [Link](https://github.com/anthropics/claude-code/issues/86619)
New regression in the auto-mode rollout: read-only `cd`-compound commands trigger unsuppressable permission prompts on two independent machines. Onset correlates with 2.1.232 — community suspects the new permission heuristics are mis-firing on Git Bash compound commands.

### 🔥 #86794 — Silent fallback to legacy credentials drains Console credits
**macOS · Cost/auth · 2 comments** · [Link](https://github.com/anthropics/claude-code/issues/86794)
Expired OAuth sessions silently fall back to legacy API keys, billing the user's Console credits instead of prompting for re-auth. Cost-related — the community has flagged several billing anomalies this week.

### 🔥 #83062 — $995.67 in auto-recharges after included limits reset
**Billing · 1 comment** · [Link](https://github.com/anthropics/claude-code/issues/83062)
Two Individual-plan auto-recharges triggered back-to-back after the monthly included-limit reset. High-impact billing bug — the community is watching for Anthropic's response.

### 🔥 #84607 — Same-day 17x variance in tokens charged per weekly quota point
**Cost · 2 comments · 2 👍** · [Link](https://github.com/anthropics/claude-code/issues/84607)
Users report wildly inconsistent token billing per quota point (up to 20x variance). Puzzling cost-accounting issue that undermines trust in usage metering.

### 🔥 #86473 — Persistent ECONNRESET on all Code surfaces (Windows 11)
**Windows · Networking · 2 comments · 2 👍** · [Link](https://github.com/anthropics/claude-code/issues/86473)
Connection drops mid-response on Windows even when raw HTTPS to `api.anthropic.com` is healthy. Duplicate reports suggest a wider Windows-specific networking regression.

### 🔥 #85205 — Auto-compact fires at 150k on a 1M-context model
**Model/context · 1 comment** · [Link](https://github.com/anthropics/claude-code/issues/85205)
Some sessions on `claude-opus-5[1m]` run with a 150k compact window instead of the full 1M — `/context` even confirms it. Inconsistent context-window sizing across sessions is a real usability issue.

### 🔥 #84474 — Workflow-backed PR comment posting silently fails
**Workflows · 3 comments** · [Link](https://github.com/anthropics/claude-code/issues/84474)
The "post review to PR" step reports success with full findings but never actually posts. Silent failure mode — a trust breaker for CI-integrated workflows.

### 🔥 #86786 — Plugin marketplace add fails with EFAULT on macOS 26
**macOS · Plugins · 1 comment** · [Link](https://github.com/anthropics/claude-code/issues/86786)
`/plugin marketplace add` fails with `EFAULT: bad address in system call argument`; deleting cache doesn't break the loop. Reproduces an older locked issue (#53181) — the reproduction narrowing is valuable.

### 🔥 #72707 — VS Code: long prompt cannot be collapsed
**macOS/VS Code · UI · 2 comments · 11 👍** · [Link](https://github.com/anthropics/claude-code/issues/72707)
The expand/collapse chevron stops responding on long user prompts, leaving the full text permanently expanded. Small UI bug, but heavily upvoted — it affects daily flow.

---

## 4. Key PR Progress

### #86746 — fix(security-guidance): preserve Python probe errors
[Link](https://github.com/anthropics/claude-code/pull/86746)
Fixes #86709 by preserving stderr from Python interpreter probes. Previously stderr was redirected to `/dev/null`, so multi-interpreter failures showed only a generic error. This PR surfaces actual diagnostics — important for debugging broken Python setups.

### #86626 — feat: add shell completions (bash, zsh, fish)
[Link](https://github.com/anthropics/claude-code/pull/86626)
Adds tab-completion scripts for the `claude` CLI that stay in sync with the installed CLI. Works with stock macOS bash 3.2, no extra package needed. Small QoL win for heavy terminal users.

### #83890 — Create pylint.yml
[Link](https://github.com/anthropics/claude-code/pull/83890)
Adds a GitHub Actions workflow running pylint. Minor CI hygiene work — age of the PR (11 days open) suggests low-priority review.

### #41611 — add the missing source to claude code
[Link](https://github.com/anthropics/claude-code/pull/41611)
Open since March; unclear scope from the title, but the lack of maintainer attention on a 5-month-old PR says something about the review queue depth.

---

## 5. Feature Request Trends

- **Session/archive management**: Unarchiving sessions in the desktop app (#30869, 57 👍) remains the top feature ask. Users want parity between desktop, VS Code, and web UIs for session lifecycle.
- **Context/browser persistence**: The Browser Agent MCP lacks the ability to list persisted browser contexts/logins — a gap vs. Browserbase (#86807). Users want enumeration and management of saved logins.
- **Background tasks in VS Code**: A "Background Tasks" panel is requested for parity with the Desktop app (#75863). Cross-platform UI parity is the recurring theme.
- **UI configurability**: Disabling prompt suggestions in claude.ai web/app (#66117) — users want more control over the surface chrome.
- **Better context-window reasoning**: Auto-compact inconsistency (#85205) feeds into a broader desire for transparent, predictable context management.

---

## 6. Developer Pain Points

- **False-positive safety blocks**: A major recurring theme. The closed issue cluster from sworrl (drone firmware analysis, SSH config, web app work — all blocked) plus #86804 (Fable 5 dual-use safeguard tripping on WAF code) points to significant frustration with overly aggressive model-level guardrails. The fact that these are marked CLOSED without visible resolution may amplify the noise.
- **Billing surprise and silent cost drains**: #86794 and #83062 both involve unexpected account charges — from silent credential fallback to back-to-back auto-recharges. Cost transparency is clearly a trust issue.
- **Windows-specific regressions**: Between Git Bash permission spam (#86619), ECONNRESET issues (#86473), and the MSIX file-lock update failure (#86555), Windows support is a persistent sore spot.
- **Silent failures**: PR posting that reports success but doesn't post (#84474), auto-compact that fires at the wrong threshold (#85205), and API errors with no response (#69238) — silent or misleading status signals are eroding workflow confidence.
- **Session-state anomalies**: Frozen sessions (#86016), unarchivable local projects (#85272), and VS Code UI toggles that stop responding (#72707) — reliability of interactive state is a nagging problem.

---

*Digest generated from public GitHub data for 2026-08-15.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest
**2026-08-15**

---

## 1. Today's Highlights

The Codex team shipped a rapid succession of Rust releases (v0.148.0-alpha.14 through alpha.18) alongside a burst of 15+ closed PRs focused on TUI startup hardening, sandbox permission enforcement, and gRPC protocol refinements. Meanwhile, the community continues to report a concentrated cluster of Windows performance issues — stuttering, mouse lag, and high CPU usage — with several new reports filed in the last 24 hours, suggesting the problem is widespread and unresolved. Notably, the team also removed repository-local skills (including the issue-triage and digest skills) from the repository.

---

## 2. Releases

**Five Rust releases in the last 24 hours:**

- [rust-v0.148.0-alpha.14](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.14)
- [rust-v0.148.0-alpha.15](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.15)
- [rust-v0.148.0-alpha.16](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.16)
- [rust-v0.148.0-alpha.17](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.17)
- [rust-v0.148.0-alpha.18](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.18)

All release notes are placeholder text ("Release 0.148.0-alpha.X") with no detailed changelogs provided. Developers should check the linked PRs for substantive changes.

---

## 3. Hot Issues

**1. Windows System-Wide Mouse Lag & Stuttering** — [Issue #38583](https://github.com/openai/codex/issues/38583) | 10 comments | 👍6
The most recent report (26.813.12317) of Windows ChatGPT/Codex causing ~10% idle CPU and persistent mouse lag. Part of a growing cluster of similar reports. Community reaction is frustrated; several users confirm the pattern across versions.

**2. macOS Severe Performance Regression** — [Issue #38468](https://github.com/openai/codex/issues/38468) | 5 comments
100%+ CPU, 10+ GB RAM, and frequent UI hangs on macOS 26.810.41047. Notably, this is a macOS-specific counterpart to the Windows performance cluster, indicating broader cross-platform regressions.

**3. Windows Update Causes Immediate System Stutter** — [Issue #38554](https://github.com/openai/codex/issues/38554) | 8 comments | 👍3
Version 26.810.4967.0 makes the entire PC stutter; fully exiting Codex fixes it immediately. User reports the problem began at install time, strongly suggesting a regression introduced in this build.

**4. Codex App Freezes on Windows 11** — [Issue #20214](https://github.com/openai/codex/issues/20214) | 101 comments | 👍84
The longest-running issue (since April) with a massive community response. Frequent freezes/stutters despite 32 GB RAM and sufficient resources. Remains open after ~3.5 months — the highest-signal performance complaint.

**5. Persistent SQLite Log Churn on macOS** — [Issue #29532](https://github.com/openai/codex/issues/29532) | 47 comments | 👍9
`~/.codex/logs_2.sqlite` continues to grow even after partial fixes in 0.142.0. Users report disk/IO churn; the community has verified the bug persists with detailed logs.

**6. HID Discovery Blocks Electron Main Thread** — [Issue #33912](https://github.com/openai/codex/issues/33912) | 18 comments | 👍2
Work Louder/Codex Micro HID discovery freezes the desktop app on Windows. Pinpoints a specific device-integration code path causing the freeze.

**7. PowerShell Spawned Every Second** — [Issue #25453](https://github.com/openai/codex/issues/25453) | 26 comments | 👍7
Codex Desktop spawns `powershell.exe` every second for full process polling, causing high CPU. Community has identified the likely culprit (process polling loop) — a clear engineering inefficiency.

**8. System-Wide Input Lag Despite Clean Logs** — [Issue #28855](https://github.com/openai/codex/issues/28855) | 18 comments | 👍20
Intermittent whole-system input lag with clean logs and plugins disabled. High community confidence the issue is in the app itself; 20 upvotes indicates broad impact.

**9. "Open in Folder" Fails for Mapped Drives** — [Issue #38668](https://github.com/openai/codex/issues/38668) | 2 comments
File Explorer opens at `C:\` for mapped-drive/UNC project files — a minor but annoying bug for enterprise users on network drives.

**10. Context Compression Fails 85% of the Time** — [Issue #31375](https://github.com/openai/codex/issues/31375) | 6 comments
Remote compact task disconnects, loses pre-compression reasoning, and diverts to unrelated plans. Critical for long sessions; community reports high failure rate.

---

## 4. Key PR Progress

**1. [PR #38673](https://github.com/openai/codex/pull/38673) — Honor per-environment permission profiles**
Adds resolved `permission_profile` to each `EnvironmentConfig`; allows `Ready` environments to override thread permissions while `FromThread` inherits. Improves sandboxing granularity.

**2. [PR #38660](https://github.com/openai/codex/pull/38660) — Enforce managed deny-read rules in Windows sandbox**
Ensures Windows sandbox requests preserve filesystem deny rules across all execution paths; fails closed for unsupported policies. Directly addresses security hardening.

**3. [PR #38662](https://github.com/openai/codex/pull/38662) — Delete Thai combining marks one at a time**
Correctly handles Thai vowel/tone marks as individual backspace boundaries. A UX polish fix for I18N.

**4. [PR #38649](https://github.com/openai/codex/pull/38649) — Reuse TUI startup account response**
Eliminates a redundant account read during bootstrap, reducing startup latency.

**5. [PR #38647](https://github.com/openai/codex/pull/38647) — Add override to skip project configuration**
New `LoaderOverrides::ignore_project_config` bypasses project-root discovery and all project configuration layers — useful for scripting/CI.

**6. [PR #38642](https://github.com/openai/codex/pull/38642) — Keep composer editable during TUI startup**
Shows a provisional composer while startup work runs; carries text, cursor position, and history into the main TUI. Improves perceived responsiveness.

**7. [PR #38641](https://github.com/openai/codex/pull/38641) — Harden TUI startup input handling**
Prevents buffered keys/control sequences from accidentally selecting actions during bootstrap; typeahead for the composer still works. Important robustness fix.

**8. [PR #38635](https://github.com/openai/codex/pull/38635) — Remove repository-local Codex skills**
Removes `codex-bug` triage, `codex-issue-digest`, and `pushing-ci-changes` skills. Signals a shift away from repo-embedded skills (potentially to external/cloud-managed skills).

**9. [PR #38634](https://github.com/openai/codex/pull/38634) — Add MCP protocol discovery metrics**
Records counters and durations for MCP client protocol discovery, tagged by mode (legacy/auto) and outcome — useful for diagnostics.

**10. [PR #38645](https://github.com/openai/codex/pull/38645) — Deliver gRPC code-mode notifications without truncation**
Removes the 1,024-byte truncation limit for code-mode notifications; includes oversized multibyte test. Fixes silent data loss on long messages.

---

## 5. Feature Request Trends

1. **Repository-Aware Task Handoff** — [Issue #34582](https://github.com/openai/codex/issues/34582)
   Users want a sanitized, repository-aware handoff contract shared across Codex App and CLI to move context between workspaces without leaking sensitive data.

2. **Restore Commit Attribution** — [Issue #31619](https://github.com/openai/codex/issues/31619)
   Enterprise users want the removed commit-attribution feature back; likely used for auditability.

3. **Bedrock Support for Ultra Reasoning** — [Issue #37160](https://github.com/openai/codex/issues/37160)
   Users on AWS Bedrock want parity with the default model catalog (GPT-5.6 Ultra reasoning unavailable on Bedrock).

4. **Git Diagnostics for Windows** — [Issue #24484](https://github.com/openai/codex/issues/24484)
   Request for the desktop app to proactively diagnose Git `safe.directory`/ownership failures when WorkTree project association fails.

5. **Papercut: Auto-Scroll Behavior** — [Issue #34303](https://github.com/openai/codex/issues/34303)
   Users want auto-scroll to keep the beginning of a response visible instead of following generated text; part of the broader "Papercuts" initiative.

---

## 6. Developer Pain Points

1. **Windows Performance Is the Dominant Pain Point** — 7 of the top 10 issues relate to Windows-specific stuttering, mouse lag, CPU spikes, or memory leaks. The cluster of reports near-identical (system-wide lag, resolves on exit) suggests a single underlying regression, likely in the 26.8xx builds.

2. **Rate Limit Reset Bugs** — Two separate reports ([#37442](https://github.com/openai/codex/issues/37442), [#38652](https://github.com/openai/codex/issues/38652)) describe weekly limits not resetting at the indicated time. Recurring billing/entitlement bugs erode trust.

3. **Context Compression Unreliability** — [Issue #31375](https://github.com/openai/codex/issues/31375) highlights that the remote compact task fails ~85% of the time, losing prior reasoning. For long coding sessions, this is severe.

4. **Session Ownership Confusion** — [Issue #38629](https://github.com/openai/codex/issues/38629): Opening the same conversation in two VS Code windows can silently transfer ownership and allow concurrent turns — a dangerous state for team workflows.

5. **Background Process & Disk I/O Churn** — Persistent SQLite log churn ([#29532](https://github.com/openai/codex/issues/29532)) and PowerShell polling ([#25453](https://github.com/openai/codex/issues/25453)) indicate inefficient background loops that waste resources even when idle.

6. **No Detailed Changelogs in Alpha Releases** — All five releases today carry placeholder notes. For users tracking regressions (especially with the Windows issues), minimal release transparency is a community frustration.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-15

## Today's Highlights
A new nightly release (v0.56.0-nightly.20260814) landed with fixes for e2e test stability on slow runners and context-aware silent retries for capacity errors. Meanwhile, the project saw a wave of "SSR Agent" automated pull requests — 10+ PRs in a single day, including a high-priority fix for the long-standing subagent MAX_TURNS misreporting issue (#22323). Developer attention remains heavily focused on subagent reliability, shell execution hangs, and memory system quality.

## Releases
**v0.56.0-nightly.20260814.gc0d192452** — Nightly release with two notable changes:
- `test(e2e)`: Stabilize file-system-interactive test on slow runners (PR #28793)
- `fix(core)`: Context-aware silent retries and availability TTL for capacity errors (#28761)

---

## Hot Issues (Top 10)

1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — P1 bug, 12 comments. A `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` even when it hits MAX_TURNS before doing any work. This masks real failures and is especially dangerous for long-running investigations. Community upvoted (👍2); a fix PR (#28815) landed today.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** — P1 bug, 8 comments, 👍8. The most-upvoted open issue. Simple operations like folder creation hang indefinitely when deferred to the generalist agent. Users report waiting up to an hour before cancelling. Workaround exists, but this remains a top community pain point.

3. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1 bug, 4 comments, 👍3. Shell commands hang indefinitely while showing "Awaiting user input" even after the command has clearly finished. Happens for trivial commands that never prompt for input. Related to PTY handling issues (#15945, fixed in PR #20916).

4. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — P2 bug, 6 comments. Anecdotal but persistent: custom skills and sub-agents are rarely invoked autonomously, even in highly relevant contexts, without explicit user instruction. Community suggests better automatic matching.

5. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — P2 bug, 5 comments. Sessions judged "low-signal" by the extraction agent are never marked processed, so the background extractor re-surfaces them endlessly — wasted API calls and token spend.

6. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — P1 bug, 4 comments. The browser subagent crashes or fails to launch on Wayland sessions, a growing Linux population. Maintainers label it `status/need-retesting` — likely fixed but awaiting verification.

7. **[#24246 — 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** — P2 bug, 3 comments. Gemini CLI throws a 400 error when more than 128 tools are available (MCP servers, custom tools, built-ins). Community expects smarter tool selection/scoping; maintainers flag it as bot-triaged.

8. **[#22093 — Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** — P2 bug, 3 comments. After updating to v0.33.0, subagents (e.g., `generalist`) started being invoked despite agent mode set to disabled in all configs. Users expect strict opt-in behavior.

9. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** — P2 feature, 3 comments. The model occasionally uses `git reset --force` or other destructive commands when safer alternatives exist. Community asks for guardrails around destructive operations, especially on DB resources.

10. **[#20079 — Symlinked agent files not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** — P2 bug, 4 comments. `~/.gemini/agents/filename.md` is ignored when `filename.md` is a symlink. Breaking for users who manage agent definitions in dotfiles repos.

---

## Key PR Progress (Top 10)

1. **[#28815 — Fix #22323: Preserve original termination reason during subagent recovery](https://github.com/google-gemini/gemini-cli/pull/28815)** — P1, area/agent. Fixes the MAX_TURNS misreporting bug. The LocalAgentExecutor now preserves the original termination reason when a subagent hits execution limits but completes `complete_task` in a grace recovery turn. Also adds regression tests. **High impact.**

2. **[#28812 — Fix #21477: Prevent indefinite TUI hang with execution timeouts](https://github.com/google-gemini/gemini-cli/pull/28812)** — P1, area/core. Addresses the "Initializing..." hang on bare Linux terminals by adding execution timeouts to `getProcessInfo()`. Small fix (size/s) for a blocking initialization hang.

3. **[#28817 — Fix #22589: Retain executing subagent tool calls in hook state](https://github.com/google-gemini/gemini-cli/pull/28817)** — size/m. Fixes dropped tool calls from subagents in hook state. Background scheduler tool calls (e.g., backend calls that don't require approval) were being filtered out, breaking hook-based observability.

4. **[#28816 — Fix #22588: Fix silent hang in MessageBus.request](https://github.com/google-gemini/gemini-cli/pull/28816)** — size/s. `MessageBus.request()` had a floating promise (fix: `this.publish()`) that could hang for 60 seconds silently on publish failure. Now registers failure and propagates errors.

5. **[#28813 — Fix #21911: Add composite flag to packages/cli tsconfig](https://github.com/google-gemini/gemini-cli/pull/28813)** — P1, area/platform. Build/typecheck failure: `evals/tsconfig.json` references `../packages/cli` but that package lacks `"composite": true`. Build-blocking fix.

6. **[#28738 — Allow agents to call agents](https://github.com/google-gemini/gemini-cli/pull/28738)** — P2, size/l, open. Lets subagents delegate to other subagents (or recurse) via `tools:` frontmatter. Fixes #22092. This enables hierarchical agent architectures but is still under review. **Community interest: high.**

7. **[#20916 — Fix: prevent PTY file descriptor leak in ShellExecutionService](https://github.com/google-gemini/gemini-cli/pull/20916)** — P1, size/m, closed. Fixes #15945: PTY master FDs were never closed after exit/kill, leading to system-wide PTY exhaustion on long sessions (macOS `kern.tty.ptmx_max` = 511). Closed, likely merged — likely fixes the "Waiting input" class of issues.

8. **[#27154 — Fix: prevent PTY memory leak by synchronously deleting active entries](https://github.com/google-gemini/gemini-cli/pull/27154)** — P2, size/m, closed. Complements #20916: `activePtys.delete(pid)` now synchronous rather than in a Promise `.then()` — avoids leaked entries if log stream cleanup hangs.

9. **[#25378 — Fix Windows ripgrep EFTYPE error](https://github.com/google-gemini/gemini-cli/pull/25378)** — P2, multi-area, open. `grep_search` fails on Windows with `spawn EFTYPE` when executing a downloaded binary that mismatches host arch (ARM vs x64). Fixes #22784. **Windows users, watch this.**

10. **[#27588 — Support WSL2 clipboard image paste](https://github.com/google-gemini/gemini-cli/pull/27588)** — P2, size/l, open. Detects WSL, uses PowerShell interop to read the Windows clipboard for image paste from WSL. Fixes #22274. WSL users frequently hit clipboard gaps — worth the wait.

---

## Feature Request Trends

1. **Subagent autonomy and recursion** — Highest-demand area. Users want agents to delegate to each other (#22092, PR #28738), better autonomous skill/sub-agent usage (#21968), and visible subagent trajectories via `/chat share` (#22598).

2. **AST-aware tools** — Several EPICs (#22745, #22746) track investigating AST-aware file reads, search, and codebase mapping — promising token reduction, fewer misaligned reads, and precise method-bound navigation.

3. **Safety and permission guardrails** — Users want agents to (a) default to non-destructive operations (#22672) and (b) respect explicit permission toggles (agents disabled must stay disabled — #22093).

4. **Sandboxing** — Proposal (#19873) to leverage Gemini 3's native "bash affinity" via zero-dependency OS sandboxing with post-execution intent routing. The goal: keep the model's native power safe.

5. **Better memory hygiene** — Auto Memory improvements are tracking broadly (#26516): deterministic redaction of secrets (#26525), skip low-signal sessions (#26522), and quarantine invalid patches (#26523).

---

## Developer Pain Points

1. **Hangs and silent stalls (the #1 complaint)** — Three distinct hangs keep resurfacing: generalist agent infinite hangs (#21409), shell commands stuck in "Waiting input" (#25166), TUI hanging at "Initializing..." (PR #28812). Timeouts and explicit failure signalling are desperately needed.

2. **Misleading success reporting** — Subagents report "GOAL success" when they actually hit MAX_TURNS (#22323). This destroys trust in agent execution results; the fix in #28815 is welcome but broader reporting transparency is needed.

3. **Windows and WSL gaps** — Windows ripgrep EFTYPE (#22784/PR #25378) and WSL2 clipboard paste (#22274/PR #27588) highlight ongoing platform parity issues.

4. **PTY/resource leaks** — Long-running sessions still exhaust PTY/file descriptors on macOS and Linux (PR #20916, #27154). Users running overnight agent tasks feel this most.

5. **Overly eager (or overly lazy) agent invocation** — Two sides of the same coin: subagents invoked against config (#22093) and skills/subagents *not* invoked when they should be (#21968). The agent needs better "self-awareness" (#21432) about its own capabilities and user preferences.

6. **Tool-count limits** — Hitting 400 errors with >128 tools (#24246) is a hard blocker for power users with many MCP servers, and the model needs smarter automatic tool selection/scoping.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-15

## Today's Highlights

Two patch releases (v1.0.80, v1.0.81-0) shipped with model configuration updates, though a new regression in v1.0.80 has broken Atlassian MCP OAuth authentication for some users. The community is actively reporting enterprise model availability issues (Claude models disabled, catalog staleness) and a recurring RFC 8414 issuer-mismatch problem affecting multiple MCP servers. A significant infrastructure PR migrated pull request automation away from `pull_request_target` to improve security for fork-originated PRs.

---

## Releases

**v1.0.81-0** — Improved: Model configurations updated.  
**v1.0.80** — Model configurations updated.  
**v1.0.80-1** — Fixes and changes.

*Note: Despite the "fixes" label on v1.0.80-1, new issues report that Atlassian MCP OAuth remains broken in 1.0.80, suggesting the fix may be incomplete or regressed.*

---

## Hot Issues

1. **[#4345 — Reasoning effort 'medium' not supported for 'claude-haiku-4.5'](https://github.com/github/copilot-cli/issues/4345)**  
   When two specific feature flags are active server-side, sub-agent execution fails repeatedly. High engagement (6 comments, 4 👍) suggests this impacts users with progressive rollout configurations. The error indicates a model/feature-flag compatibility gap.

2. **[#4390 — Enabled organization models missing from catalogue](https://github.com/github/copilot-cli/issues/4390)**  
   Models explicitly enabled by Copilot Business orgs (Claude Sonnet 5, Opus 5, Kimi K3) don't appear in the CLI model catalogue. This is a recurring enterprise pain point with serious productivity implications — users pay for models they cannot access. 6 comments, 4 👍.

3. **[#4480 — Atlassian MCP OAuth fails with RFC 8414 §3.3 error (regression)](https://github.com/github/copilot-cli/issues/4480)**  
   Upgrading to 1.0.79 broke Atlassian remote MCP server authentication. The error indicates an issuer mismatch between advertised and discovered metadata. 4 comments, 6 👍 — the most-upvoted issue in 24h, signaling strong community impact. A duplicate (#4490) confirms it persists in 1.0.80.

4. **[#4422 — All Claude models disabled under CLI model selection](https://github.com/github/copilot-cli/issues/4422)**  
   Enterprise users report Claude models (sonnet 5, 4.8) becoming unavailable overnight despite being enabled in GitHub settings. Rollback doesn't help — suggests a server-side policy or catalog issue. 3 comments, 3 👍.

5. **[#4439 — GitLab MCP OAuth rejected with RFC 8414 issuer mismatch](https://github.com/github/copilot-cli/issues/4439)**  
   Same RFC 8414 issue as Atlassian, but with GitLab Self-Managed MCP servers. This pattern suggests a systemic problem with the OAuth metadata validation logic rather than a server-specific bug. 3 comments, 2 👍.

6. **[#4306 — Subtasks freeze and stop responding in autopilot mode](https://github.com/github/copilot-cli/issues/4306)**  
   In autopilot with `/fleet use`, subtasks hang mid-session. This is a workflow-critical reliability issue for agent-heavy usage. 3 comments, 2 👍.

7. **[#4499 — Fatal "Committing semi space failed" OOM in autopilot](https://github.com/github/copilot-cli/issues/4499)**  
   v1.0.79 crashes with a V8 heap OOM even though the heap is only ~14% utilized (607 MB / 4.3 GB). This points to a host-RAM commit failure, not a heap limit — likely a memory management bug in long-running sessions.

8. **[#4491 — /spawn template contradicts itself; no approval gate on cross-session write](https://github.com/github/copilot-cli/issues/4491)**  
   A safety-relevant finding: the `/spawn` command's prompt template can silently turn "create a child session" into "inject context into an unrelated running session" with no approval gate. This is a potentially destructive behavior worth immediate attention.

9. **[#2934 — Support protobuf OTLP export](https://github.com/github/copilot-cli/issues/2934)**  
   Closed, but notable: Copilot CLI's OpenTelemetry support only exports `application/json`, silently ignoring `OTEL_EXPORTER_OTLP_PROTOCOL`. The standard env var is ignored — a compatibility issue for teams with protobuf-based observability pipelines. 6 👍.

10. **[#4346 — MCP registry policy fetch returns 403 for Actions GITHUB_TOKEN](https://github.com/github/copilot-cli/issues/4346)**  
    In GitHub Actions CI with the documented PAT-less setup, MCP registry policy fetches fail with 403, blocking all non-default MCP servers. This undermines the "no PAT needed" promise for CI workflows. Closed but relevant for CI users.

---

## Key PR Progress

1. **[#4449 — Migrate pull request automation away from pull_request_target](https://github.com/github/copilot-cli/pull/4449)** *(Merged)*  
   Closes invalid-label automation using an issue-scoped write token, uses a no-permission `pull_request` signal for prompt handling, and runs privileged workflows with appropriate restrictions. A meaningful security hardening move against a well-known attack vector.

2. **[#4497 — Handle fork PR associations in invalid-label writer](https://github.com/github/copilot-cli/pull/4497)** *(Open)*  
   Companion fix to #4449: when GitHub doesn't populate the PR association for fork-originated workflow runs, the writer searches trusted metadata and requires exactly one open PR match. Prevents mislabeling fork PRs.

3. **[#4496 — Verify pull request workflow migration (canary)](https://github.com/github/copilot-cli/pull/4496)** *(Closed)*  
   A temporary documentation-only canary PR to verify the migrated automation for fork-originated PRs. Confirms the team is testing the new workflow path before full reliance.

*Note: Only 3 PRs were updated in the last 24 hours. The low volume suggests the team is in a stabilization phase following the recent releases, with focus on workflow infrastructure rather than new features.*

---

## Feature Request Trends

1. **Model Catalog Refresh / Caching** — Multiple issues (#4390, #4422, #4494) report that newly enabled or org-configured models don't appear in the CLI until local state is cleared. The model catalog appears to be cached too aggressively or not refreshed on demand.

2. **GPT-5.6 Reasoning Mode Support** — [#4495](https://github.com/github/copilot-cli/issues/4495) requests a way to select the new `reasoning.mode` parameter ("standard" vs "pro") for GPT-5.6. Expect more requests as OpenAI rolls out this feature.

3. **Plugin Dependency Management** — [#4487](https://github.com/github/copilot-cli/issues/4487) proposes a dependency model for marketplace plugins (inter- and intra-marketplace) with automatic installation. This signals plugin ecosystem maturation.

4. **MCP Server Improvements** — Pagination support ([#4006](https://github.com/github/copilot-cli/issues/4006)) and case-insensitive collision detection ([#4478](https://github.com/github/copilot-cli/issues/4478)) for MCP servers. Both are correctness issues that matter as MCP adoption grows.

5. **Clarified Startup Messaging** — [#4475](https://github.com/github/copilot-cli/issues/4475) asks to disambiguate "No copilot-instructions.md found" to clarify it means the repo-scoped file. Small UX win for reducing confusion.

---

## Developer Pain Points

1. **MCP OAuth Instability** — The RFC 8414 §3.3 issuer-mismatch error is affecting multiple providers (Atlassian, GitLab), regressed between versions, and persists across releases. This is the highest-signal pain point this week, blocking real-world MCP usage.

2. **Enterprise Model Gating** — A cluster of issues around Claude models being unavailable, disabled, or missing from the catalogue in enterprise settings. Model selection feels unreliable for org users.

3. **Long-Running Session Reliability** — OOM crashes ([#4499](https://github.com/github/copilot-cli/issues/4499)), session loss on stop ([#4477](https://github.com/github/copilot-cli/issues/4477)), subtask freezes ([#4306](https://github.com/github/copilot-cli/issues/4306)), and `/restart` failures in worktree sessions ([#4493](https://github.com/github/copilot-cli/issues/4493)) all point to stability problems in longer agent sessions.

4. **Permission / Directory Configuration Gaps** — [#4482](https://github.com/github/copilot-cli/issues/4482) reports `allowed_directories` in `permissions-config.json` not suppressing prompts for shell commands, while [#4486](https://github.com/github/copilot-cli/issues/4486) reports edit-permission requests "timing out" — both frustrate non-interactive and multi-session workflows.

5. **CI Authentication for MCP** — Even with no-PAT setup, MCP registry policy fetches fail with 403 ([#4346](https://github.com/github/copilot-cli/issues/4346)), blocking non-default MCP servers in GitHub Actions.

6. **Context Loss on Interruption** — Stopping an action deletes the session and prompt ([#4477](https://github.com/github/copilot-cli/issues/4477)). For long-running tasks, this is destructive and forces full rework.

7. **Cross-Session Safety** — The `/spawn` template contradiction ([#4491](https://github.com/github/copilot-cli/issues/4491)) is a subtle but serious safety concern: it can silently write to unrelated sessions without approval.

---

*Data current as of 2026-08-15. All links point to the public GitHub repository: [github.com/github/copilot-cli](https://github.com/github/copilot-cli).*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest – 2026-08-15**

**1. Today's Highlights**  
No new releases or pull requests were published in the last 24 hours. However, community activity centered on long-standing feature gaps, particularly the high-demand **Memory System** (Issue #1283, 39 comments) and **Multi-Device Session Handoff** (Issue #2269). A notable closed PR (#1136) demonstrates ongoing Windows-specific shell tooling improvements, signaling a push for more robust cross-platform support.

**2. Releases**  
No new versions released in the last 24 hours. No digest content.

**3. Hot Issues**  
*(4 issues updated in the last 24 hours; all included below)*

- **[#1283] Feature Request: Memory System - Persistent context across sessions** — The top-voted open request (👍 0 despite 39 comments), it calls for automatic (AI-managed notes) and manual (user-defined) persistent memory. This is the community's most vocal demand, with extensive discussion on workflow impact for large codebases. [Link](https://github.com/MoonshotAI/kimi-cli/issues/1283)
- **[#2269] Remote Control / Multi-Device Session Handoff** — Requests seamless session transfer across laptop, web, or mobile. Captures a real pain point for developers working across environments, with early community support (👍 1) and 6 comments. [Link](https://github.com/MoonshotAI/kimi-cli/issues/2269)
- **[#1478] Optimize the Memory Layer** — A bilingual complaint reiterating that memory features are undocumented (only `agent.md` found) and painful for large projects. References third-party memory file structures (e.g., `MEMORY.md`) as a possible solution. Community reaction highlights documentation gaps, not just implementation. [Link](https://github.com/MoonshotAI/kimi-cli/issues/1478)
- **[#1136] [CLOSED] Enhance Shell Tool with version-aware PowerShell context** — This PR-based issue identifies three critical Windows-specific bugs (e.g., ambiguous shebang handling) that degraded K2.5 agent performance in command generation. The closure signals the fix merged into the codebase, a win for Windows users. [Link](https://github.com/MoonshotAI/kimi-cli/issues/1136)

**4. Key PR Progress**  
No pull requests were updated in the last 24 hours. No digest content.

**5. Feature Request Trends**  
Across the reviewed issues, two dominant feature directions emerge:

- **Persistent Memory Systems** (Issues #1283, #1478): The clear #1 request. Developers demand both automatic context retention and user-controlled memory, with explicit documentation. The absence of an official spec is a major friction point.
- **Session Continuity & Portability** (Issue #2269): A secondary trend toward multi-device workflows, mirroring broader industry moves toward cloud-continuity in coding assistants.

**6. Developer Pain Points**  
- **Memory failure on large projects**: Users report context loss is "painful" and undocumented, forcing workarounds or manual context reloading.
- **Documentation gaps**: Complaints reference missing memory documentation (Issue #1478) and unclear configuration paths, despite an existing `agent.md` file.
- **Windows-specific instability**: Resolved issue #1136 highlights lingering cross-platform inconsistencies, though the fix reduces immediate friction.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-15

## Today's Highlights

A **critical 48-bit ID timestamp wraparound** (#42608) struck on 2026-08-14 at 12:39:55 UTC, causing all pre-existing sessions to silently stop processing prompts — this is the root cause behind multiple "session not responding" reports (#42605, #42594, #42611). Meanwhile, **dynamic model discovery** for OpenAI-compatible providers is finally landing via two parallel PRs (#42660 and the long-running #27554), addressing one of the most-persistent feature requests. On the infrastructure side, work continues on protocol hardening (#42628, #42667) and a schema-driven plugin adapter (#42669) from contributor **kitlangton**.

## Releases

No new releases in the last 24 hours. Current stable remains **v1.18.x** (desktop app referenced at v1.18.1 and CLI at 1.18.15).

## Hot Issues

1. **[#42608 — 48-bit ID timestamp wraparound wedges all pre-existing sessions](https://github.com/anomalyco/opencode/issues/42608)** *(CLOSED, 5 comments, 👍3)*  
   **Critical bug**: The ID generator's 48-bit timestamp wrapped at `2026-08-14 12:39:55 UTC`, causing every session created before that moment to stop processing prompts. This is the single most impactful issue today — likely affecting thousands of users. Community reaction is one of urgency and relief that a root cause was found quickly.

2. **[#36997 — Desktop App v1.18.1 new layout hides agent (Plan/Build) switching UI](https://github.com/anomalyco/opencode/issues/36997)** *(OPEN, 12 comments, 👍6)*  
   After auto-update to the new layout, the Plan/Build agent toggle disappeared — users can't see or switch the active agent, and Tab switching is broken. High engagement signals many users hit this.

3. **[#42083 — GitHub Copilot provider shows zero models](https://github.com/anomalyco/opencode/issues/42083)** *(OPEN, 8 comments, 👍2)*  
   `github-copilot` auth succeeds but all models return `model_picker_enabled: false`; the provider never appears in the picker. Blocks Copilot subscribers from using OpenCode.

4. **[#38791 — Run loop never exits when message IDs are not time-sortable](https://github.com/anomalyco/opencode/issues/38791)** *(OPEN, 6 comments)*  
   Sessions imported from third-party tools (with non-timestamp IDs) cause the run loop to never terminate, looping until the provider returns 400. Root cause: message IDs compared as plain strings, not timestamps.

5. **[#41518 — gpt-5.6-luna via OpenCode Go relay returns 403 region error](https://github.com/anomalyco/opencode/issues/41518)** *(OPEN, 6 comments)*  
   Chinese-language report: `gpt-5.6-luna` through the OpenCode Go relay returns HTTP 403 "not available in your region". Region restrictions on the relay are frustrating international users.

6. **[#37489 — Context cache invalidation causes performance issues with local LLMs](https://github.com/anomalyco/opencode/issues/37489)** *(OPEN, 5 comments, 👍1)*  
   Switching modes or compacting invalidates the context cache, causing slow re-processing on vLLM/Ollama. Users want smarter cache reuse.

7. **[#42605 — Session remains open but agent stops processing prompts](https://github.com/anomalyco/opencode/issues/42605)** *(OPEN, 4 comments)*  
   Reported the same day as the ID wraparound — almost certainly a symptom of #42608. Agent asks a question, user replies, no response.

8. **[#42626 — Bash tool subprocess SIGKILL on many small stdout writes](https://github.com/anomalyco/opencode/issues/42626)** *(CLOSED, 3 comments)*  
   Running `pytest tests/` (streaming lots of small writes) kills the subprocess with SIGKILL under WSL. Likely a pipe-buffer or resource-limit issue.

9. **[#42657 — TUI lag with multi-subagent sessions (97% CPU on render thread)](https://github.com/anomalyco/opencode/issues/42657)** *(OPEN, 2 comments)*  
   With 2–4 concurrent subagents, the TUI render thread hits 97% CPU causing 1–3s typing latency across all tested terminals. Performance regression in the render loop.

10. **[#42215 — 429 rate-limited in new session on Zen free models](https://github.com/anomalyco/opencode/issues/42215)** *(CLOSED, 2 comments, 👍2)*  
    Free model daily quota not resetting correctly; intermittent "Free Usage Exceeded" errors persist past the 24-hour window.

## Key PR Progress

1. **[#42669 — fix(plugin): derive promise adapter from protocol schemas](https://github.com/anomalyco/opencode/pull/42669)** *(OPEN, kitlangton)*  
    Replaces hand-written Promise plugin translation with a schema-driven adapter derived from the canonical V2 `HttpApi` contract — ensures consistency for `session.create.title`, branded IDs, and DateTime handling.

2. **[#42628 — refactor(protocol): harden simulation wire contract](https://github.com/anomalyco/opencode/pull/42628)** *(CLOSED, kitlangton)*  
    Standalone Drive will delete its copied schema; this PR makes the canonical `@opencode-ai/protocol/simulation` module the single source of truth with typed notifications and exact success/error unions.

3. **[#42667 — fix(core): unify patch path resolution](https://github.com/anomalyco/opencode/pull/42667)** *(OPEN, kitlangton)*  
    Aligns V2 patch tool's path/permission resources with the canonical `LocationMutation` service used by write/edit tools — fixes path resolution inconsistencies.

4. **[#42662 — fix(mcp): fail loudly on MCP server config missing type](https://github.com/anomalyco/opencode/pull/42662)** *(OPEN, shreeyachand, closes #41229)*  
    Many Claude Code MCP configs lack `type`/`enabled` fields; OpenCode now fails with a clear error instead of silently misbehaving.

5. **[#42663 — feat(core): persist web search provider selection](https://github.com/anomalyco/opencode/pull/42663)** *(CLOSED, thdxr)*  
    Web search provider consent now stored in the first file-backed config document instead of KV state — fixes disappearing provider preference.

6. **[#42666 — fix(app): use location VCS state](https://github.com/anomalyco/opencode/pull/42666)** *(OPEN, opencode-agent[bot])*  
    Desktop app now derives new-session Git state from the directory-scoped VCS store (same model as TUI), with regression coverage for stale global project inventory cases.

7. **[#27554 — feat(opencode): local LAN provider discovery + auto-discover models](https://github.com/anomalyco/opencode/pull/27554)** *(OPEN, androidand, closes #6231 & #27553)*  
    **Long-awaited**: adds "Local (LAN)" discovery in `/connect` for OpenAI-compatible servers using mDNS combined with `/v1/models` auto-discovery. Open since May — community eager for merge.

8. **[#42660 — feat(provider): add dynamic model discovery for custom providers](https://github.com/anomalyco/opencode/pull/42660)** *(OPEN, Gr33ndev, closes 6 issues)*  
    Companion to #27554: auto-discovers models from OpenAI-compatible providers (LiteLLM, LM Studio, etc.) via `/v1/models` — closes #13891, #29308, #28999, #25624, #23327, #26863.

9. **[#36943 — fix(core): keep interrupted sessions stopped](https://github.com/anomalyco/opencode/pull/36943)** *(CLOSED, opencode-agent[bot])*  
    Fences advisory session wakes by durable admission sequence; suppresses stale prompt wakes after interrupts while preserving genuinely newer prompts.

10. **[#36883 — fix(core): expose valid subagent IDs to the model in the subagent tool](https://github.com/anomalyco/opencode/pull/36883)** *(CLOSED, Robin1987China, closes #36761)*  
    The `subagent` tool now lists valid agent IDs in its schema, so models stop guessing (`explorer` vs `explore`) — eliminates a class of silent failures.

## Feature Request Trends

1. **Dynamic model discovery for OpenAI-compatible providers** — Users are tired of manually listing every model in `opencode.json` when the provider exposes `/v1/models`. Requests in #27553, #42660, plus Androidand's LAN discovery — this is the #1 recurring ask.

2. **Runtime permission toggles** — A `/approve on|off` slash command (like Claude Code) to toggle approval mode mid-session is requested in #41909. Permissions are currently fixed at startup.

3. **OAuth callback host configurability** — #33966: recent PR #30022 bound the OAuth server to 127.0.0.1; users with remote setups need a configurable `OAUTH_CALLBACK_HOST`.

4. **New provider integrations** — Requests continue for niche/regional routers, e.g. #42664 asking for "nara router" (router.bynara.id) support.

5. **Better context cache management** — #37489: users with local LLMs (vLLM/Ollama) want cache invalidation to be smarter — avoid full re-processing on mode switches or compaction.

## Developer Pain Points

- **Session reliability** — The ID wraparound (#42608) exposed systemic fragility in session ID handling; related reports of hanging sessions (#42605, #42594) and run-loop exit bugs (#38791) indicate core execution-loop weaknesses.
- **Desktop app regressions** — The v1.18.1 layout hiding the Plan/Build toggle (#36997) and WSL mirrored-networking sidecar failures (#37718) show desktop polish issues remain.
- **Provider quirks** — Zero-model Copilot (#42083), regional 403s on the Go relay (#41518), and DeepSeek reasoning_content pass-back errors (#25000) frustrate multi-provider users.
- **Billing/rate-limit confusion** — Multiple reports of paid credits not reflecting (#42606, #42637) and free-tier quota resets not working (#42215) suggest billing-system bugs are eroding trust.
- **TUI performance with concurrency** — 97% render-thread CPU with multi-subagents (#42657) makes parallel workflows painful — a growing concern as subagents become more popular.
- **Imported session compatibility** — Third-party importers producing non-timestamp IDs break core loop logic (#38791) — validation gaps for foreign session data.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-15

## 1. Today's Highlights
Pi **v0.84.2** shipped with fullscreen transcript search and configurable default tools. The community is heavily focused on **Windows and WSL support** (#7547 with 27 comments), plus a wave of **provider-specific fixes** — including a hotfix for OpenAI's invalid `session_id` header (#8149), a Baseten DeepSeek output cap (#8146), and a TUI clipboard truthfulness fix (#8110). Performance issues around TUI rendering and streaming remain prominent.

## 2. Releases
**v0.84.2** (latest)
- **Fullscreen transcript search** — search and navigate matches in fullscreen mode ([docs](https://github.com/earendil-works/pi/blob/v0.84.2/packages/coding-agent/docs/keybindings.md#tui-fullscreen-viewport)).
- **Configurable default tools** — choose which tools are available at startup.

## 3. Hot Issues (Top 10)

1. **[#7547 — [Windows] How do you use Pi on Windows?](https://github.com/earendil-works/pi/issues/7547)** — *27 comments, 1 👍*  
   An open call for Windows usage feedback. The sheer number of run methods (WSL, native, MSYS) makes it hard to prioritize fixes. The community is actively discussing pain points, making this the most significant open thread.

2. **[#6187 — Pi login hangs in WSL after Copilot device authorization](https://github.com/earendil-works/pi/issues/6187)** — *26 comments*  
   A closed bug that generated heavy discussion. The client never detects completed browser-based auth in WSL, leaving users stuck. High frustration due to the broken first-run experience.

3. **[#5223 — Anthropic provider modifies thinking blocks, causing 400 with Opus 4.8](https://github.com/earendil-works/pi/issues/5223)** — *17 comments, 6 👍*  
   Multi-turn sessions fail mid-conversation because the provider mutates `thinking` blocks in the latest message. A critical correctness bug for heavy Claude users.

4. **[#6665 — TUI pins full core while streaming](https://github.com/earendil-works/pi/issues/6665)** — *12 comments, 3 👍*  
   `Intl.Segmenter` is uncached and Markdown rebuilds per chunk, leading to ~100% CPU on one core. Marked `inprogress`; this is a key performance blocker for long sessions.

5. **[#5023 — Terminal scrolls to beginning without reason](https://github.com/earendil-works/pi/issues/5023)** — *12 comments, 2 👍*  
   Random, non-interactive scrolling during model output. Closed but still resonates with users experiencing TUI instability.

6. **[#7850 — Copilot login fails with 429 for orgs with many models](https://github.com/earendil-works/pi/issues/7850)** — *9 comments, 7 👍*  
   GitHub device auth succeeds but Copilot login rate-limits when an org has 20+ models. Marked no-action, but the high 👍 count indicates corporate users are hitting this.

7. **[#8096 — Z.AI Coding Plan defaults reference removed model `glm-5.1`](https://github.com/earendil-works/pi/issues/8096)** — *5 comments*  
   Generated provider catalogs no longer contain `glm-5.1`, but `defaultModelPerProvider` still selects it. Simple config drift, quickly closed.

8. **[#8092 — Extension loader fails with pnpm + jiti isolated node_modules](https://github.com/earendil-works/pi/issues/8092)** — *5 comments*  
   jiti doesn't realpath entries before resolving imports, breaking extension deps under pnpm's isolated layout. Resolved by PR #8112.

9. **[#8010 — Copilot login fails with 429 after model refresh](https://github.com/earendil-works/pi/issues/8010)** — *4 comments, 2 👍*  
   Users who log out/in to see new models get hit with 429. Related to #7850; a pattern is emerging around Copilot rate-limit handling.

10. **[#8047 — Pi Server tests fail on Windows (Unix socket bind EACCES)](https://github.com/earendil-works/pi/issues/8047)** — *3 comments*  
    31 test failures on Win11 due to Unix transport tests trying to bind filesystem sockets. Highlights ongoing Windows portability gaps.

## 4. Key PR Progress (Top 10)

1. **[#8149 — fix(ai): omit invalid OpenAI session header](https://github.com/earendil-works/pi/pull/8149)**  
   Stops sending `session_id` headers that HTTP/1 proxies (Envoy) reject due to underscores. Fixes production `400` errors with zero upstream duration.

2. **[#8148 — fix(coding-agent): scope bash PI_* guideline to session questions](https://github.com/earendil-works/pi/pull/8148)**  
   Fixes #7787. Models were running `env` on unrelated tasks because the guideline read as startup work. Now scoped to relevant sessions.

3. **[#8146 — fix(ai): cap Baseten DeepSeek V4 Flash output at 384k tokens](https://github.com/earendil-works/pi/pull/8146)**  
   Fixes #8147. Clamps `maxTokens` to 384k despite models.dev advertising 1M. Prevents request failures.

4. **[#8143 — perf(tui): window fullscreen transcripts](https://github.com/earendil-works/pi/pull/8143)**  
   Rewrites fullscreen rendering to draw only visible blocks, keeping full history while model context stays compacted. Addresses rendering performance.

5. **[#8139 — feat(ai): add ChatGPT OAuth image generation](https://github.com/earendil-works/pi/pull/8139)**  
   New native image-generation transport reusing OpenAI Codex OAuth and Responses infra. No API key needed — uses ChatGPT entitlement.

6. **[#8124 — feat(ai): route xAI models through Responses, default Grok 4.6](https://github.com/earendil-works/pi/pull/8124)**  
   Switches xAI from completions to the Responses API with a user agent, and bumps the default model from Grok 4.5 to 4.6.

7. **[#8120 — feat(coding-agent): add experimental append compaction](https://github.com/earendil-works/pi/pull/8120)**  
   Append mode reuses active system prompt, tools, and routing session so compacted prefixes hit provider prompt caches. Gated behind `PI_EXPERIMENTAL=1`.

8. **[#8119 — fix: track Kimi cached tokens](https://github.com/earendil-works/pi/pull/8119)**  
   Fixes #8075. Kimi's top-level `usage.cached_tokens` was counted as normal input; now correctly treated as cache-read.

9. **[#8110 — fix(tui): route selection copy through the host clipboard](https://github.com/earendil-works/pi/pull/8110)**  
   Fixes #7761. OSC 52 alone isn't enough on VTE terminals; now uses host clipboard so "Copied!" is truthful.

10. **[#8112 — fix(coding-agent): realpath extension entries before jiti import](https://github.com/earendil-works/pi/pull/8112)**  
    Fixes #8092. Resolves pnpm's symlinked layout before jiti resolves imports, unblocking npm-installed extensions.

## 5. Feature Request Trends
- **Windows-native and WSL support** — the most active area (#7547, #6187, #8047). Users want clear guidance and fewer platform-specific crashes.
- **Provider-agnostic reliability** — multiple requests for better retry classification (#8138), fallback handling (#8125), and output caps (#8146).
- **Per-model configuration** — requests for per-model compaction profiles (#8133) and thinking-level maps (#8135) signal a need for finer-grained control.
- **TUI ergonomics** — autocomplete in the middle of prompts (#8144), configurable autocomplete position (#8132), and better clipboard handling (#8110).
- **Cache-aware usage tracking** — Kimi and other providers' `cached_tokens` should be visible in usage stats (#8075, #8119).

## 6. Developer Pain Points
- **Copilot login rate limits (429)** — recurring across issues (#7850, #8010), especially for orgs with many models. High community resonance (7 👍 and 2 👍).
- **TUI CPU stalls and random scrolling** — #6665 and #5023 indicate the rendering layer still needs performance hardening for long sessions.
- **Provider protocol edge cases** — thinking-block mutation (#5223), strict-null tool params (#8105), and reasoning-only completions (#8115) are breaking multi-turn flows.
- **Windows test failures** — Unix socket binding in tests (#8047) and WSL auth hangs (#6187) suggest Windows is still a second-class platform for testing and auth flows.
- **Extension loading fragility** — pnpm + jiti resolution (#8092) and autocomplete-in-middle-of-prompt (#8144) point to rough edges in the extension and input systems.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-15

## Today's Highlights

The v0.21.12 release line continues to mature with Web Shell workspace file uploads and session management improvements, while the team is actively addressing several CI reliability issues through automated tracking. A notable shift toward architectural refactoring is visible, with multiple issues targeting dependency inversions, layer violations, and removal of internal coupling between CLI and serve components.

## Releases

**v0.21.12** and **v0.21.12-preview.4** are now available. Key changes include:
- **Web Shell workspace file uploads** — supports drag-and-drop and `@` file panel with progress tracking ([#8874](https://github.com/QwenLM/qwen-code/pull/8874))
- **Autofix review diff growth brake** — limits unbounded diff expansion
- **Session target preservation fix** for standalone Web Shell sessions ([#9038](https://github.com/QwenLM/qwen-code/pull/9038))

## Hot Issues

1. **[#8678 — Session restore timeout handling (CLOSED)](https://github.com/QwenLM/qwen-code/issues/8678)** — Large session restores timing out lost the current session context. Marked partially addressed and superseded; request-scoped timeout and late-result safety were the critical components. 9 comments.

2. **[#8051 — Bound multi-workspace daemon resource usage](https://github.com/QwenLM/qwen-code/issues/8051)** — Count-only limits don't bound actual bytes held by request bodies, WebSocket assembly buffers and other memory-heavy paths in `qwen serve` daemon. Open P2 tracking issue with active discussion. 9 comments.

3. **[#9160 — E2E CI failure: live journal recovery stream test](https://github.com/QwenLM/qwen-code/issues/9160)** — Three test failures in `cli/qwen-serve-live-journal-recovery.test.ts` around compatible live chunk streams during replay entries. Marked `autofix/in-progress` with 4 comments.

4. **[#9146 — utils/ layer cycle: 107 upward imports](https://github.com/QwenLM/qwen-code/issues/9146)** — A structural refactor tracking issue: 51 files in `utils/` import domain directories, creating a cyclic directory graph. Provides detailed table of upward imports per package. 4 comments.

5. **[#9002 — Python SDK rejects `permission_mode="auto"`](https://github.com/QwenLM/qwen-code/issues/9002)** — Client-side validation rejects a value the CLI accepts. `ValidationError: Invalid permission_mode: 'auto'` blocks SDK users from plan-mode workflows. 6 comments.

6. **[#9026 — `NO_TOOL_RESULT_PROGRESS` hard-fails headless runs](https://github.com/QwenLM/qwen-code/issues/9026)** — When a model legitimately ends a turn quietly after a tool result, headless runs abort with `InvalidStreamError`. Related PR #9196 is now open with a fix. 4 comments.

7. **[#2128 — Unbounded memory growth in long sessions](https://github.com/QwenLM/qwen-code/issues/2128)** — Long-running sessions accumulate UI History entries without limit, causing memory to grow indefinitely. Root cause identified in `useHistoryManager.history`. Open P1 since March. 4 comments.

8. **[#9089 — Autofix PAT-bearing jobs need runner isolation](https://github.com/QwenLM/qwen-code/issues/9089)** — Security issue: PAT-bearing jobs share a host with untrusted branch code. Cannot be fixed from within a GitHub Actions step; needs runner-level isolation. P1 security. 3 comments.

9. **[#9137 — Release v0.21.12-preview.2 publish failed](https://github.com/QwenLM/qwen-code/issues/9137)** — Release workflow failed in `publish` job. Related fix in PR #9082 force-pushes release branches so retries replace failed attempts. 3 comments.

10. **[#8871 — ACP child process fails with "Unknown argument: acp"](https://github.com/QwenLM/qwen-code/issues/8871)** — `qwen serve --http-bridge=true` spawns ACP child with unsupported `--acp` flag, causing token auth failure (401). 5 comments.

## Key PR Progress

1. **[#9196 — Accept quiet post-tool-result completions after retry exhaustion](https://github.com/QwenLM/qwen-code/pull/9196)** — Fixes `NO_TOOL_RESULT_PROGRESS` false positives: valid `finish_reason` with no visible text and no further tool call should not trip the guard or burn retry budget.

2. **[#9096 — Absorb prose `gh` commands into platform-backed subcommands](https://github.com/QwenLM/qwen-code/pull/9096)** — Refactors the `/review` skill: raw `gh` commands in prompt prose (repo resolution, head-SHA fetches, issue evidence) move into first-class CLI subcommands.

3. **[#9100 — Validate and scope the incremental anchor inside `fetch-pr`](https://github.com/QwenLM/qwen-code/pull/9100)** — Adds `--since <sha>` to `qwen review fetch-pr` for validated incremental review scoping with hex allowlist checking.

4. **[#9122 — Web Shell sidebar session management](https://github.com/QwenLM/qwen-code/pull/9122)** — Adds hover previews, folder expansion controls, fade/scroll for long titles, and visual running-session states.

5. **[#9027 — Plain-prose review comments; severity markers follow `review.attribution`](https://github.com/QwenLM/qwen-code/pull/9027)** — Makes readability the criterion for posted review comments, with phrasing separated into plain vs. attributed layers.

6. **[#9082 — Force-push release branch so retries replace failed attempts](https://github.com/QwenLM/qwen-code/pull/9082)** — Fixes the release retry loop where stale per-release branches block subsequent attempts in "Commit and Condition" step.

7. **[#8978 — No-op on empty channel set and restore only active channels (`--channel all`)](https://github.com/QwenLM/qwen-code/pull/8978)** — Converts `exit(1)` on empty effective channel set into a graceful no-op, plus restores only active channels.

8. **[#9189 — Defer verified out-of-footprint findings to a surviving follow-up queue](https://github.com/QwenLM/qwen-code/pull/9189)** — Adds a fourth anti-drift outcome to SKILL's address-review: verified findings outside PR footprint are recorded in a machine-readable queue for follow-up.

9. **[#9040 — Prevent dialog clipping in short terminals](https://github.com/QwenLM/qwen-code/pull/9040)** — `/statusline` gets a compact layout below 16 rows; `/skills` limits locked-skill rows under height constraints.

10. **[#8938 — Reject upstream fail-fast placeholder responses](https://github.com/QwenLM/qwen-code/pull/8938)** — Detects HTTP 200 responses with normal finish reason but placeholder body (e.g., `(request timed out)`) and fails fast with an actionable error.

## Feature Request Trends

- **Web Shell expansion** — Multiple PRs and issues target Web Shell: workspace uploads, sidebar session management, session media references, HTML export refactor, Electron host evaluation.
- **Review/autofix infrastructure hardening** — Dominant theme: typed channels for findings, incremental anchors, deferral queues, plain-prose comments, growth-divergence comparability windows.
- **Architecture cleanups** — Consistent direction: make `utils/` a leaf layer, remove ACP integration dependencies on serve internals, break the `@google/genai` type coupling in core.
- **Channel/daemon lifecycle improvements** — DingTalk workspace channel, outbound file delivery, no-op empty channel sets, restore-only-active-channels semantics.

## Developer Pain Points

- **CI flakiness** — Multiple automated issues (#9143, #9159, #9160, #9137) track main-branch E2E failures and release publish failures, often before test results are even reported. The team is investing heavily in autofix tooling rather than simply fixing individual tests.
- **Architecture friction** — Repeated issues (#4063, #9146, #8084) document structural problems: cyclic dependencies, layering violations, and over-coupling to specific SDK types. These create maintenance overhead for contributors.
- **Resource exhaustion in long-running sessions** — Unbounded memory growth (#2128) and unbounded daemon resource usage (#8051) are recurring concerns for production users running multi-day sessions.
- **CLI/SDK inconsistency** — SDK rejecting values the CLI accepts (#9002) and child processes failing on unsupported flags (#8871) indicate incomplete parity between interfaces.
- **Surprising hard failures** — Headless runs aborting on legitimate model behavior (#9026) and release retries being blocked by stale branches (#9137) show edge cases that frustrate automation and unattended operation.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-15

## Today's Highlights

The v0.9.8 release is out, rebranding the project as **CodeWhale** (with a codewhale CLI and npm package) while deprecating the legacy `deepseek-tui` package. The community is actively stabilizing this release: several "main is red" issues on macOS/Windows were filed and fixed within 24 hours by re-pinning test assertions. Meanwhile, the maintainer (Hmbown) is driving major architectural improvements, including simplifying a 32-field agent tool schema and adding a model-guardian tier for Auto-Review.

---

## Releases

### v0.9.8 (released ~2026-08-14)

From the release notes snippet:
- Project is now publicly branded as **CodeWhale** (Shannon Labs product)
- CLI command renamed to `codewhale`; npm package also `codewhale`
- Legacy `deepseek-tui` npm package is deprecated and receives no further releases
- Note: v0.9.8 was previously referenced as having known issues (#5355), and several CI-breaking tests were patched in this release window

---

## Hot Issues (10 selected)

1. **[#5324] agent tool: simplify the 32-field schema so models stop erroring on it**  
   Maintainer-driven redesign: the model-facing `agent` tool has 32 properties, zero required fields, and 8 actions in one schema — too complex, causing model errors. Community has 8 comments discussing schema-slicing strategies.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/5324)

2. **[#5373] Output-token ceiling clamped below the documented catalogue limit; truncation kills the turn**  
   CodeWhale requests 65,536 output tokens for deepseek-v4-flash/pro while the documented limit is 384,000. A competing harness requests the full amount; Terminal-Bench tasks crash due to truncation. Closed — presumably fixed or will be fixed promptly.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/5373)

3. **[#5372] Stale write-claims from closed sessions block new sub-agents (dead owners counted as active)**  
   Real-world blocker: after a session closes, prior agents still hold write claims on directories; new sessions are rejected with write-scope contention errors. Models incorrectly see dead agents as active. Closed.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/5372)

4. **[#5370] P0: web UI looks broken — audit and rebuild look/features against harness references**  
   Maintainer reports the public web UI is "totally broken" in looks and features. Scoped between the public `web/` Next.js app and the managed CWC app. High priority (P0).  
   [Link](https://github.com/Hmbown/CodeWhale/issues/5370)

5. **[#5374] The writing its weird (the agent)**  
   macOS user reports corrupted text output when the agent writes — garbled rendering. Community: 4 comments, no resolution yet. Likely a TUI rendering regression.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/5374)

6. **[#5383] main is red on v0.9.8: cli provider-count assertions still hold the pre-release numbers**  
   CI failing on v0.9.8 head: provider-count assertions in `crates/cli/src/lib.rs` still expect old numbers (43/38 vs 45/40). Fixed by PR #5384 within hours.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/5383)

7. **[#5377] main is red on macOS and Windows: nine reasoning-effort tests still assert the pre-ladder vocabulary**  
   Second "main is red" issue — nine tests assert the old reasoning-effort vocabulary. Bisects to a specific commit, reproduces identically. Fixed by PR #5378.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/5377)

8. **[#5380] bug: session-index JSONL writes are unsynchronized, causing silent data loss under concurrent StateStore clones**  
   Concurrency bug: `append_thread_name` writes to session_index.jsonl outside the `Arc<Mutex<Connection>>`, risking data loss when StateStore is cloned. Closed (fixed via PR #5382).  
   [Link](https://github.com/Hmbown/CodeWhale/issues/5380)

9. **[#5293] TUI: make deny-by-default approval selection configurable and clearly explained**  
   Behavioral regression: v0.9.4 changed the default highlighted option in permission request dialogs to "deny", causing accidental denials when users intend to confirm quickly. Community: 5 comments, 1 👍. Closed — hopefully configurable now.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/5293)

10. **[#5340] doctor: `first-run` / `update checkpoint` permanently stuck on `needs action` after upgrade**  
    After upgrading v0.9.4 → v0.9.6, `codewhale doctor` permanently reports first-run and update checkpoint as "needs action" even after completing onboarding. Setup can never be marked complete. Closed.  
    [Link](https://github.com/Hmbown/CodeWhale/issues/5340)

---

## Key PR Progress (10 selected)

1. **[#5365] feat(provider): add first-class local DS4 setup** — `feat(provider): add first-class local DS4 setup`  
   Makes DwarfStar (DS4) a first-class local DeepSeek route with a prefilled keyless loopback preset; reuses OpenAI-compatible transport. Closed/merged.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/5365)

2. **[#5353] feat(tui): model guardian tier for Auto-Review (v0.9.8)** — `feat(tui): model guardian tier for Auto-Review (v0.9.8)`  
   Auto-Review becomes a two-layer mode: deterministic floor stays non-bypassable, fallback holds escalate to a one-shot model guardian. Aligns with Codex `auto_review` semantics and Kimi mode vocabulary. Closed/merged.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/5353)

3. **[#5384] test(cli): re-pin the provider-count assertions to the v0.9.8 registry** — `test(cli): re-pin the provider-count assertions to the v0.9.8 registry`  
   Fixes #5383. Updates numbers from 43/38 → 45/40 after v0.9.8 shipped more providers (e.g., Google Gemini as its own backend).  
   [Link](https://github.com/Hmbown/CodeWhale/pull/5384)

4. **[#5378] test(tui): re-pin the thinking-ladder assertions** — `test(tui): re-pin the thinking-ladder assertions`  
   Fixes #5377. Nine tests that asserted the old off/high/max shortcut, replaced by the thinking-ladder vocabulary. No production changes. Closed/merged.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/5378)

5. **[#5382] fix(state): serialize session-index writes to prevent silent data loss** — `fix(state): serialize session-index writes to prevent silent data loss`  
   Fixes #5380. Moves session-index JSONL operations under the same `Arc<Mutex<Connection>>` that serializes SQLite access, preventing concurrent-clone data loss. Closed/merged.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/5382)

6. **[#5381] fix(hooks): do not panic when the webhook HTTP client fails to build** — `fix(hooks): do not panic when the webhook HTTP client fails to build`  
   Fixes #5379. Replaces `.expect()` with graceful error handling for reqwest client build failures (e.g., misconfigured TLS backend). Closed/merged.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/5381)

7. **[#5369] fix(tools): degrade Moonshot schemas instead of refusing conditionals** — `fix(tools): degrade Moonshot schemas instead of refusing conditionals`  
   Pre-requisite for #5324; sends schema improvements separately so #5324 stays focused. Degrades unsupported conditionals gracefully rather than failing. Closed/merged.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/5369)

8. **[#5368] fix(tui): confine unguarded tests to the isolated state root** — `fix(tui): confine unguarded tests to the isolated state root`  
   Fixes #5359. Three independent fixes: lock-holder trust hole in `settings_path_candidates()`, plus two others — each with a test that fails when only its own fix is reverted. Closed/merged.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/5368)

9. **[#5364] feat(tui): render markdown blockquotes with a quote rail** — `feat(tui): render markdown blockquotes with a quote rail`  
   Renders `>` blockquotes with a proper visual rail in the TUI transcript. Supports nesting, inline formatting, wrapping, and correct selection-copy. Closed/merged. Community contributor (SparkofSpike).  
   [Link](https://github.com/Hmbown/CodeWhale/pull/5364)

10. **[#5376] fix(tui): keep internal runtime events out of the session peek** — `fix(tui): keep internal runtime events out of the session peek`  
    Fixes #5375 (not in the issue list above). Internal runtime events were leaking into the session peek projection; now filtered out. Closed/merged.  
    [Link](https://github.com/Hmbown/CodeWhale/pull/5376)

---

## Feature Request Trends

1. **Simpler agent-tool schema** (#5324, #5369): The 32-field agent tool schema is too complex for models to use reliably. Community and maintainer agree on schema slicing / degradation instead of refusal.

2. **Plugin system maturity** (#5311): Community wants a complete plugin product: federated marketplaces, easier discovery, and more installation sources (beyond GitHub/tarball). Kimi-level plugin system is the explicit benchmark.

3. **Third-party model presets** (#5350): Users want pre-built templates for third-party compatible providers (OpenCode Zen, Agnes, etc.) with fixed URLs, model lists, and only the API key required. Also request a "test connection" button.

4. **TUI usability polish**: Update notices + one-chord update-and-relaunch (#5053), configurable approval defaults (#5293), and sub-agent display identity consistency (#5287) all point to a theme: the TUI should communicate more clearly and require fewer keystrokes for common operations.

5. **Preview-before-send** (#1004): Users want a `/dryrun` command to preview the exact next chat-completion request (system prompt, cached files, tool defs, etc.) before paying for it — especially relevant for V4 Pro long turns.

---

## Developer Pain Points

1. **"Main is red" CI cascades**: Multiple issues this week (#5383, #5377) where tests failed on macOS/Windows due to versioned assertions. The community is frustrated by repeated, preventable CI breaks; fixing these quickly requires re-pinning test expectations.

2. **Concurrency / data-loss bugs**: #5380 (session-index JSONL race), #5372 (stale write-claims blocking new sub-agents), and #5379 (panic on hook-sink build failure) all stem from subtle concurrency or error-handling gaps. These are hard-to-diagnose, high-impact bugs.

3. **Upgrade friction**: #5340 shows that upgrading from v0.9.4 → v0.9.6 can permanently break `doctor` health checks, making the setup checklist never complete. Upgrade health is a growing concern.

4. **Security/UX tension on approvals**: #5293 highlights that changing the default approval option to "deny" breaks established interaction patterns — users accidentally deny actions they meant to confirm. The community wants configurability *and* clearer explanation of defaults.

5. **Output truncation on long tasks**: #5373 shows that clamping output tokens to 65,536 (while the model supports 384,000) causes crashes on long Terminal-Bench tasks. Users expect the tool to respect documented catalogue limits.

---

*Generated 2026-08-15 from github.com/Hmbown/DeepSeek-TUI (now CodeWhale) activity.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*