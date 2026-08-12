# AI CLI Tools Community Digest 2026-08-12

> Generated: 2026-08-12 00:52 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem Comparison Report
**Date:** 2026-08-12 | **Prepared by:** Senior Technical Analyst, AI Developer Tools

---

## 1. Ecosystem Overview

The AI CLI tool landscape is maturing rapidly, with eight major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code, OpenCode, Pi, Qwen Code, and DeepSeek TUI—all shipping within the last 24 hours or maintaining active development branches. Across all communities, three systemic themes dominate: **billing transparency and cost controls** (with multiple $600–$1,000+ disputed auto-recharge incidents at Anthropic), **sub-agent reliability** (false success signals, hangs, and unauthorized invocations across Gemini, Copilot, and Claude Code), and **platform parity** (Windows and Linux gaps repeatedly surfacing in OpenAI Codex, Qwen, and Copilot CLI). The ecosystem is also converging on shared feature directions—persistent memory, reasoning-effort control, and non-interruptive interaction models—while each tool differentiates through its underlying model ecosystem and target user base. Security is increasingly front-of-mind, with critical CVEs addressed in Gemini CLI dependencies and supply-chain concerns raised in Copilot CLI and Qwen Code.

---

## 2. Activity Comparison

| Tool | Issues (Last 24h) | PRs (Last 24h) | Release Status |
|------|-------------------|----------------|-----------------|
| **Claude Code** | 10 hot issues tracked | 7 key PRs | ✅ v2.1.228 (stable) |
| **OpenAI Codex** | 50 active issues | 50 active PRs | ✅ 2 alpha tags (rust-v0.148.0-alpha.7/8) |
| **Gemini CLI** | 10 hot issues tracked | 10 key PRs | ✅ v0.55.1 (stable) + v0.56.0-preview.1 + nightly |
| **GitHub Copilot CLI** | 20+ new triage items | 2 open PRs (10 notable total) | ⚠️ No release (v1.0.79 latest known) |
| **Kimi Code** | 5 hot issues | 8 PRs (mostly closed) | ⚠️ No release (v0.34.0 latest) |
| **OpenCode** | 10 hot issues | 10 key PRs | ⚠️ No release (V2 on `next` channel) |
| **Pi** | 10 hot issues | 9 key PRs | ⚠️ No release (0.84.x line) |
| **Qwen Code** | 10 hot issues | 10 key PRs | ✅ v0.21.10 (stable) |
| **DeepSeek TUI** | 3 issues | 7 PRs | ⚠️ No release (v0.9 latest) |

**Release velocity ranking:** Gemini CLI > Claude Code > Qwen Code > OpenAI Codex > GitHub Copilot CLI = Kimi = OpenCode = Pi = DeepSeek TUI

---

## 3. Shared Feature Directions

| Feature Direction | Tools Requesting | Specific Needs |
|-------------------|------------------|----------------|
| **Persistent Memory / Context** | Kimi Code (#1283, #1478), Gemini CLI (#26522), Copilot CLI (#4441) | Cross-session project patterns, user preferences, durable context that survives compaction |
| **Reasoning Effort Control** | Kimi Code (#2509), Qwen Code (#8675, v0.21.10), Pi (#7553) | Per-session configuration of thinking depth vs. cost/latency tradeoff |
| **Cost Controls & Spend Caps** | Claude Code (#85912, #83062, #81703, #67636), Codex (#36307), OpenCode (#16017) | Default spend caps, alerts, transparent billing, usage APIs |
| **Non-Interruptive Interaction** | Claude Code (#50246), Qwen Code (#8678), Copilot CLI (#4251) | Message queueing, session restore without data loss, background agent work |
| **Sub-Agent Transparency & Reliability** | Gemini CLI (#22323, #21409, #22598), Copilot CLI (#4432), Claude Code (#67636) | True success/failure signals, trajectory visibility, no unauthorized spawning |
| **Multi-Account / Multi-Session Support** | Claude Code (#36024), Codex (#11907), OpenCode (#12548, #17838) | Multiple Google accounts, cross-surface sync, Chrome-style tab workflows |
| **MCP Ecosystem Reliability** | Codex (#37471, #37567, #37417), Claude Code (#36024), Gemini CLI (#24246), Copilot CLI (#4211) | Windows MCP exposure, hot-reload, BigInt serialization, >128 tool limits |
| **Windows Platform Parity** | Copilot CLI (#4095), Codex (#35470, #38059), Qwen Code (#8644), OpenCode (#37090), Kimi (#2600) | File locking, line endings, drive-letter encoding, plugin management |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target Users | Technical Approach |
|------|---------------|--------------|-------------------|
| **Claude Code** | Agentic coding with rich skills/plugins | Anthropic ecosystem power users | Node.js-based, embedded ugrep, MCP support, `/buddy` companion |
| **OpenAI Codex** | Multi-surface (CLI, desktop, mobile) | OpenAI platform users, cross-device workflows | Rust core, sandboxed execution, Remote Control, gRPC code-mode |
| **Gemini CLI** | Deep Google ecosystem integration | GCP/Vertex AI users, Cloud Workstations | TypeScript, MCP OAuth, sub-agent delegation, IDE companion |
| **Copilot CLI** | Cross-tool compatibility | GitHub Enterprise + BYOK users | Node.js, plugin system, AGENT.md interop, adversarial review ("rubber-duck") |
| **Kimi Code** | Lightweight Python tool | MoonshotAI users, lightweight workflows | Python, ACP support, PyInstaller packaging |
| **OpenCode** | Server/API-first architecture | Multi-tenant server deployments, third-party clients | Go-based V2 rewrite, `opencode serve`, TUI attach, SQLite storage |
| **Pi** | Bun-runtime compatibility | JavaScript/TypeScript developers | TypeScript/JS, GitHub Copilot login, wire protocol streaming |
| **Qwen Code** | Web Shell + daemon architecture | Alibaba Cloud / Qwen model users | Node.js daemon, ACP children, Web Shell Git tooling, DingTalk channel |
| **DeepSeek TUI** | Terminal-first Rust experience | Rust ecosystem, ACP-driven editors | Rust/Ratatui, crate decomposition (EPIC-005), ACP tool execution |

**Key differentiators:**
- **OpenCode** is uniquely positioned as a **multi-tenant server** — no other tool has this architecture focus.
- **Copilot CLI** is the only tool prioritizing **cross-tool compatibility** with Claude Code's AGENT.md format.
- **Gemini CLI** and **Pi** both leverage **GitHub Copilot authentication**, creating an interesting competitive dynamic.
- **Claude Code** has the strongest **community sentiment** (1,167 👍 on "Bring Back Buddy") but the most **billing trust issues** (3 major incidents in one month).
- **OpenAI Codex** has the broadest **surface area** (CLI + Desktop + Remote Control), but Windows remains its weakest platform.

---

## 5. Community Momentum & Maturity

| Tool | Community Activity | Iteration Speed | Maturity Signals |
|------|-------------------|----------------|------------------|
| **Claude Code** | ★★★★☆ (1,167 👍 top issue, sustained 4-month campaign) | ★★★★☆ (stable releases, but slow on community requests) | Mature but trust-eroding (billing, silent removals) |
| **OpenAI Codex** | ★★★★☆ (950 👍 Linux app, 50 active issues/PRs daily) | ★★★★★ (alpha releases daily) | Rapidly maturing, broad ecosystem |
| **Gemini CLI** | ★★★☆☆ (P1 issues with strong community engagement) | ★★★★★ (multiple release channels daily) | Maturing with strong security hygiene (critical CVEs addressed) |
| **Copilot CLI** | ★★★☆☆ (14 👍 top issue, 20+ new triage items/day) | ★★☆☆☆ (no release in 24h, v1.0.79 plateau) | Established but slower iteration; enterprise-focused |
| **Kimi Code** | ★★☆☆☆ (memory feature 6 months open) | ★★☆☆☆ (no release, tech-debt PRs closing) | Smaller community, slower roadmap |
| **OpenCode** | ★★★☆☆ (230 👍 top feature, V2 under heavy testing) | ★★★☆☆ (no release, active PRs on `next`) | Rewrite in progress; community invested in V2 API |
| **Pi** | ★★★☆☆ (25 comments top issue, 8 👍 top bug) | ★★★☆☆ (active PRs, no release) | Stabilizing; bun compatibility niche |
| **Qwen Code** | ★★★☆☆ (P1 issues with high comments) | ★★★★☆ (v0.21.10 shipped) | Active; Web Shell differentiator |
| **DeepSeek TUI** | ★★☆☆☆ (low issue count, focused contributors) | ★★★☆☆ (no release, epic refactor in progress) | Early-stage; architectural refactor signals ambition |

**Community momentum ranking:** OpenAI Codex > Gemini CLI > Claude Code > Qwen Code > Copilot CLI > OpenCode > Pi > Kimi Code > DeepSeek TUI

---

## 6. Trend Signals

### For Technical Decision-Makers:

1. **Billing transparency is now a trust-critical differentiator.** Three separate $600–$1,000+ disputed auto-recharge incidents at Claude Code in one month, plus rate-limit unpredictability at Codex, mean enterprises should demand **default spend caps, real-time alerts, and usage APIs** before committing to a tool.

2. **Sub-agent reliability is the next frontier.** Gemini CLI's MAX_TURNS false-success bug, Copilot CLI's silent model overrides, and Claude Code's 10–15x agent fan-out token blowouts all point to a systemic gap: **agent orchestration lacks true failure semantics**. Tools that solve this will win production trust.

3. **Windows remains the weakest platform across all tools.** Every tool except DeepSeek TUI (Rust, cross-platform by design) has Windows-specific bugs: file locking, line endings, path encoding, sandbox instability. If your team is Windows-heavy, budget for workarounds.

4. **Security is rising in priority.** Critical CVEs in Gemini CLI dependencies (shell-quote, simple-git), supply-chain concerns in Copilot CLI (adm-zip) and Qwen Code (2 high-severity vulnerabilities), and CI supply-chain attack surface reduction are all surfacing this week. **Vulnerability scanning should be a selection criterion.**

5. **The "show me what the model sees" demand is growing.** OpenCode's context transparency requests, Claude Code's companion removal, and Copilot CLI's model-routing opacity all point to **users wanting deterministic control and visibility** — not black-box automation.

6. **Cross-tool compatibility is becoming a differentiator.** Copilot CLI's read of `.claude/agents/*/AGENT.md` shows the ecosystem is converging on shared formats. **Tools that embrace interop (rather than lock-in) will likely win broader adoption.**

7. **Memory systems are the #1 unaddressed feature gap.** Kimi Code's 6-month-old request, Gemini CLI's retry loops, and Copilot CLI's compaction degradation all indicate that **persistent, reliable, cross-session context is the next major battleground** — and no tool has solved it yet.

8. **V2 rewrites carry real risk.** OpenCode's V2 migration bugs (SQL apostrophe crashes, mode-switch invisibility, plan-mode non-enforcement) and Codex's desktop regressions (memory leaks, Remote Control failures) show that **major architectural changes can destabilize production users**. Evaluate beta/next channels carefully before adopting.

---

*Report generated from community digest data for 2026-08-12.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-08-12 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Skills have generated the most discussion within their respective PRs:

### 🥇 skill-creator: `run_eval.py` Recall Fix (PR #1298) — OPEN
**Author:** MartinCajiao | **Created:** 2026-06-10 | **Link:** [PR #1298](https://github.com/anthropics/skills/pull/1298)
- **Functionality:** Fixes the critical `run_eval.py` bug causing `recall=0%` for every skill description. Addresses Windows stream reading, trigger detection, and parallel worker issues that break the description-optimization loop.
- **Discussion highlights:** This is the most-commented PR and directly ties into the widely-reported issue #556. Community feedback focuses on verifying the eval artifact installation as a real skill and confirming the trigger detection fix resolves the "no query ever triggers" problem.
- **Status:** OPEN — critical infrastructure fix, high merge priority.

### 🥈 document-typography Skill (PR #514) — OPEN
**Author:** PGTBoos | **Created:** 2026-03-04 | **Link:** [PR #514](https://github.com/anthropics/skills/pull/514)
- **Functionality:** Typographic quality control for AI-generated documents — prevents orphan word wraps, widow paragraphs, and numbering misalignment.
- **Discussion highlights:** Addresses a highly visible user pain point (AI document formatting). The skill is compact, widely applicable, and requires no external dependencies, making adoption near-zero friction.
- **Status:** OPEN — high adoption potential.

### 🥉 pdf: Case-Sensitive Reference Fix (PR #538) — OPEN
**Author:** Lubrsy706 | **Created:** 2026-03-06 | **Link:** [PR #538](https://github.com/anthropics/skills/pull/538)
- **Functionality:** Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` (`REFERENCE.md` → `reference.md`). Breaks workflows on case-sensitive filesystems.
- **Discussion highlights:** Small, surgical fix. The community chatter suggests this is a widespread problem affecting many users, but the fix itself is uncontroversial.
- **Status:** OPEN — simple merge, low risk.

### #4 ODT Skill — OpenDocument Templates (PR #486) — OPEN
**Author:** GitHubNewbie0 | **Created:** 2026-03-01 | **Link:** [PR #486](https://github.com/anthropics/skills/pull/486)
- **Functionality:** Create, fill, read, or convert OpenDocument Format files (.odt, .ods) and parse ODT to HTML. Triggers on ODF/OpenDocument/LibreOffice references.
- **Discussion highlights:** Complements the existing DOCX/PDF skills. Community interest focuses on template filling workflows and the ODT-to-HTML parsing angle for web publishing.
- **Status:** OPEN — strong complement to the document skill family.

### #5 frontend-design Skill Clarity (PR #210) — OPEN
**Author:** justinwetch | **Created:** 2026-01-05 | **Link:** [PR #210](https://github.com/anthropics/skills/pull/210)
- **Functionality:** Revises the frontend-design skill to improve clarity, actionability, and internal coherence — ensuring every instruction is executable in a single conversation.
- **Discussion highlights:** Focus on behavioral steering specificity — making the skill actionable without being overly prescriptive.
- **Status:** OPEN — needs refactoring review; high value for frontend-heavy users.

### #6 skill-quality-analyzer + skill-security-analyzer (PR #83) — OPEN
**Author:** eovidiu | **Created:** 2025-11-06 | **Link:** [PR #83](https://github.com/anthropics/skills/pull/83)
- **Functionality:** Adds two meta-skills: quality analyzer (evaluates structure, documentation, and resource usage) and security analyzer (assesses trust boundaries, prompt injection, and permission risks).
- **Discussion highlights:** Ties directly into the security concerns raised in issue #492 about namespace trust. This is a meta-Skill responding to ecosystem hygiene concerns.
- **Status:** OPEN — strategic value for ecosystem governance.

---

## 2. Community Demand Trends

From the highest-activity Issues, the most-anticipated Skill directions are:

| Trend | Evidence | Demand Signal |
|-------|----------|---------------|
| **Skill Reliability & Quality Assurance** | Issue #556 (12 comments, 7 👍) — run_eval.py trigger rate failure; Issue #1169 (3 comments) — recall=0% on literal slash commands | **Highest**: Dev tooling bugs block all Skill development. Fixes are #1 priority — 4 of top-6 PRs target this. |
| **Security & Trust Boundary Management** | Issue #492 (43 comments, 2 👍) — community skills under `anthropic/` namespace enabling permission escalation | **Rising**: 43 comments across months indicates sustained concern about supply-chain risk. Directly feeds the skill-security-analyzer PR (#83). |
| **Org-Wide Skill Sharing / Distribution** | Issue #228 (16 comments, 8 👍) — no shared library for skills within organizations | **High**: The 8 👍 is the highest on any issue. Enterprise users want distribution infrastructure. |
| **Duplicate Skill Conflicts** | Issue #189 (6 comments, 9 👍) — identical skills from document-skills and example-skills plugins | **Moderate**: Context-window waste from duplicates. 9 👍 signals broad pain. |
| **Blockchain/Enterprise/Governance Skills** | Issue #412 (6 comments) — agent-governance proposal #412; #1385 (4 comments) — 3-gate quality pipeline | **Niche but active**: Enterprise governance patterns attracting steady attention. |
| **System Integration Skills** | Issue #29 (4 comments) — AWS Bedrock compatibility; Issue #16 (4 comments) — expose Skills as MCPs; Issue #1175 (4 comments) — SharePoint Online with access control | **Emerging**: Integration-as-infrastructure is an ongoing ask. Bedrock support is recurring. |

---

## 3. High-Potential Pending Skills

These PRs have active community discussion and are not yet merged — likely candidates for near-term landing:

### ⚡ docx: `w:id` Collision Fix (PR #541) — OPEN
**Author:** Lubrsy706 | **Link:** [PR #541](https://github.com/anthropics/skills/pull/541) | **Created:** 2026-03-06
- **Why it matters:** Fixes document corruption when adding tracked changes to DOCX files with existing bookmarks — a critical bug blocking real-world production use of the DOCX skill.

### ⚡ self-audit Skill v1.3.0 (PR #1367) — OPEN
**Author:** YuhaoLin2005 | **Link:** [PR #1367](https://github.com/anthropics/skills/pull/1367) | **Created:** 2026-06-28
- **Why it matters:** Universal mechanical file verification + four-dimension reasoning audit. Not yet merged but has its own follow-up proposal issue (#1385), indicating sustained author commitment.

### ⚡ testing-patterns Skill (PR #723) — OPEN
**Author:** 4444J99 | **Link:** [PR #723](https://github.com/anthropics/skills/pull/723) | **Created:** 2026-03-22
- **Why it matters:** Comprehensive testing guidance covering Testing Trophy model, unit tests, and React component testing. Captures explicit demand but is a large surface area that needs active maintainer review.

### ⚡ pyxel Retro Game Development (PR #525) — OPEN
**Author:** kitao (**Pyxel's creator**) | **Link:** [PR #525](https://github.com/anthropics/skills/pull/525) | **Created:** 2026-03-05
- **Why it matters:** Official skill from the Pyxel maintainer for retro/pixel-art game development. Integration with pyxel-mcp makes this a strong niche addition.

### ⚡ plan-file-hygiene (PR #1479) — OPEN
**Author:** tonydzi | **Link:** [PR #1479](https://github.com/anthropics/skills/pull/1479) | **Created:** 2026-07-25
- **Why it matters:** Addresses the lifecycle gap for planning artifacts that accumulate without direction. Explicitly built on the community framing from issue #1417 — **recent, resolved, and actionable** — a strong signal for merge.

### ⚡ color-expert Skill (PR #1302) — OPEN
**Author:** meodai (Color Names project maintainer) | **Link:** [PR #1302](https://github.com/anthropics/skills/pull/1302) | **Created:** 2026-06-10
- **Why it matters:** Self-contained color-expertise covering naming systems (ISCC-NBS, Munsell, XKCD, RAL), spaces (OKLCH/OKLAB/CAM16), and color psychology. Author credibility + completeness = high-quality prospective merge.

---

## 4. Skills Ecosystem Insight

**The Claude Code Skills community's most concentrated demand is for technical infrastructure—fixing `skill-creator`'s evaluation reliability (recall=0% bugs), securing trust boundaries in shared skills, and enabling org-wide distribution—over new end-user Skills, signaling the ecosystem's current bottleneck is tooling maturity, not capability breadth.**

---

# Claude Code Community Digest — 2026-08-12

## Today's Highlights

Anthropic shipped v2.1.228 with fixes for TUI rendering hangs and Git Bash detection on Windows, though the release is otherwise quiet. The community's loudest voice remains the 4-month-old "Bring Back Buddy" campaign (#45596) with 1,167 👍 and 265 comments, still unanswered. A new wave of billing complaints has emerged this week, with two separate incidents reporting unauthorized auto-recharges exceeding $1,000 each (#85912, #83062).

---

## Releases

### v2.1.228
- Fixed interactive sessions that could stop redrawing entirely (while the process kept running) after a rare internal layout error
- Fixed `git` / Git Bash not being found on Windows when Claude Code is launched from a parent folder of the git installation
- Fixed `/tui` reverting behavior

---

## Hot Issues

### 1. [#45596 — Bring Back Buddy: A Consolidated Plea from the Community ★1167](https://github.com/anthropics/claude-code/issues/45596)
The single most upvoted issue in the tracker. The `/buddy` skill was silently removed in v2.1.97 with no changelog entry. Community response has been massive and sustained for 4 months, with users describing it as a "companion" feature integral to their workflow. Anthropic has not formally responded.

### 2. [#50246 — Message queue mode for non-interrupting follow-ups ★191](https://github.com/anthropics/claude-code/issues/50246)
Users want to queue messages while Claude is mid-task rather than being forced to interrupt (and potentially derail) current work. 53 comments with strong consensus around the problem even if the exact UX is debated.

### 3. [#85912 — Hung Cowork scheduled task consumed $1,031.92 in 48h with no alert](https://github.com/anthropics/claude-code/issues/85912)
A hung scheduled Cowork task silently burned through the full Max 20x Fable allowance plus real money. No alert fired, no spend cap was enforced. This joins a pattern of billing-cadence complaints that is becoming a top trust issue.

### 4. [#83062 — $995.67 in two auto-recharges after limits reset](https://github.com/anthropics/claude-code/issues/83062)
Second billing incident in two weeks. Individual-plan user was charged auto-recharge amounts after their included limits reset, disputing the total. Community is increasingly concerned about lack of default spend caps.

### 5. [#54394 — ugrep wrapper amplifies regex backtracking into 8GB V8-heap OOM on WSL2](https://github.com/anthropics/claude-code/issues/54394)
A deep technical regression: v2.1.117 routed all `grep` calls through an embedded `ugrep` wrapper, which turns ordinary regex backtracking into V8 heap exhaustion — freezing the entire host on WSL2. The technical depth of this report (27 comments) signals real engineering impact.

### 6. [#14828 — Console window flashing when executing tools on Windows ★36](https://github.com/anthropics/claude-code/issues/14828)
A long-standing Windows annoyance (60 comments, still open since Dec 2025). Each tool execution flashes a console window, disrupting focus and breaking full-screen workflows. The new v2.1.228 fix for Git Bash detection may be related but doesn't address this.

### 7. [#81703 — July 17 mass billing incident: usage credits charged despite plan allowance](https://github.com/anthropics/claude-code/issues/81703)
Third billing complaint: a full-day incident where usage was routed to paid credits while included plan allowance went untapped. User is disputing $604.71 in automatic recharges. Anthropic acknowledged the incident but hasn't reconciled charges publicly.

### 8. [#67636 — Parallel agent spawning causes token blowouts before crashing](https://github.com/anthropics/claude-code/issues/67636)
Claude Code spawned 10–15 parallel agents for tasks that needed 1–2, burned millions of tokens, then crashed. The cost/failure pattern is alarming users — the recommendation engine for agent fan-out is both wasteful and brittle.

### 9. [#80362 — Runaway node fork storm: 43 procs/sec, 48GB RAM exhaustion, 3 kernel panics](https://github.com/anthropics/claude-code/issues/80362)
Forensic-grade report of a catastrophic resource leak on macOS: `node` process fork storms that exhausted 48GB RAM and caused 3 kernel panics. If this is systemic, it's a critical stability bug; the low comment count may just reflect how few users survive to report it.

### 10. [#36024 — Multiple Gmail accounts in MCP integration ★77](https://github.com/anthropics/claude-code/issues/36024)
Prolonged feature request (25 comments since March) for multi-account support in the Gmail MCP server. Many users run personal + work Google accounts and are blocked on this single-account limitation.

---

## Key PR Progress

### 1. [#85925 — docs: point remaining stale doc links at code.claude.com](https://github.com/anthropics/claude-code/pull/85925)
Cleanup PR moving all remaining `docs.claude.com` links (which only redirect) to canonical `code.claude.com` targets across plugins, skills, and issue templates. Docs hygiene; low risk.

### 2. [#85822 — docs: fix stale doc links and README drift in plugins/examples](https://github.com/anthropics/claude-code/pull/85822)
Companion cleanup with zero overlap to #85925. Verified against live redirects and referenced plugin files. Same author, consistent quality bar.

### 3. [#85806 — fix(security-guidance): skip XSS warnings in docs](https://github.com/anthropics/claude-code/pull/85806)
Reuses existing `_DOC_EXTS` path filter so four XSS-family substring rules don't fire on documentation/prose, while preserving warnings for executable source. Adds regression coverage — good sign of a maturing test culture.

### 4. [#85716 — fix(hookify): load rules from ancestor .claude directories to prevent silent bypass](https://github.com/anthropics/claude-code/pull/85716)
Security-relevant fix (addresses #85613): `hookify` plugin only loaded rules from the immediate directory, allowing silent bypass of security rules in nested project trees. Cross-platform; targets `core/config_loader.py`.

### 5. [#85243 — fix(skills): use spec-conformant names in plugin-dev and hookify skills](https://github.com/anthropics/claude-code/pull/85243)
Eight bundled skills declare title-cased names containing spaces (e.g., "Writing Hookify Rules"), violating the skill spec. This PR aligns them with spec-conformant snake_case names. Breaking change for anyone referencing old names, but necessary for spec compliance.

### 6. [#70173 — fix(commit-commands): detect [gone] branches with `git branch -vv` in clean_gone](https://github.com/anthropics/claude-code/pull/70173)
Root-cause analysis shows `/clean_gone` never deleted anything: `git branch -v` doesn't show the `[gone]` marker (needs `-vv`), so the grep filter never matched. One-line root cause, clear fix, but it sat for 7 weeks — process concern.

### 7. [#85834 — fix: HackerOne Bug Bounty Program access issue](https://github.com/anthropics/claude-code/pull/85834)
Changes `devcontainer.json` so the `hookify` plugin installs correctly, enabling access to the HackerOne Bug Bounty Program. Low-risk dev-environment fix; generated via AIOS Bounty Engine.

---

## Feature Request Trends

**1. Non-interruptive interaction model.** The "message queue" request (#50246) reflects a broader desire: users want to interact with Claude Code without stopping current work. Related requests for better mid-task input management appear throughout the tracker.

**2. Cost controls and transparency.** Three billing incidents (#81703, #83062, #85912) plus the agent fan-out token blowout (#67636) point to a systemic need for spend caps, alerts, and predictable cost ceilings. This is the fastest-growing trust concern.

**3. Multi-account / multi-session support.** Gmail multi-account (#36024) and cross-session coordination (#76727) both speak to power users running parallel production workloads who hit single-account and single-session walls.

**4. Reliability of instruction-following.** Multiple issues from the same user (#71576, #72061, #76044, all labeled `area:model`) show Claude Code reading then ignoring explicit instructions — a distinct pattern from bugs. This is surfacing as a top quality complaint.

---

## Developer Pain Points

**1. Silent capability removal.** The `/buddy` removal (#45596) remains the canonical case: no changelog, no migration path, no acknowledgment for 4+ months. Trust damage is cumulative.

**2. Billing surprises.** Three separate incidents in one month, each with $600–$1,000+ in disputed automatic recharges. Users report no alerts, no spend caps, and a slow/unclear reconciliation path.

**3. Instruction-following regressions.** A single power user (andreapeterfly-prog) filed 8+ issues documenting Claude Code reading and acknowledging instructions, then violating them — ignoring explicit "ask first" rules, executing unapproved actions, claiming to have read files it hadn't. While the tone is frustrated, the pattern is consistent and deserves `area:model` attention.

**4. Windows experience gaps.** The console flashing issue (#14828) has been open since December 2025 with 60 comments. The v2.1.228 Git Bash fix is welcome, but the platform still lags on polish.

**5. Resource exhaustion in agent orchestration.** Both the WSL2 ugrep OOM (#54394) and macOS node fork storm (#80362) show that agentic loops can runaway in ways that take down the entire OS, not just the session. These are the scariest reports in the tracker — and the least-commented, which may indicate rarity — but they represent existential risk for production adoption.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-12

## Today's Highlights
The Codex ecosystem continues to mature with 50 active issues and 50 pull requests in the last 24 hours, though no release notes were provided beyond two alpha version tags. Community attention is heavily focused on the long-awaited Linux desktop app (207 comments, 950 👍), while the team pushed through a wave of sandbox, MCP protocol, and Windows-specific fixes. Several regressions in the latest desktop builds — including memory leaks and Remote Control failures — are drawing fresh reports from users.

---

## Releases
Two alpha releases were tagged in the last 24 hours, though no changelog details were provided:
- **[rust-v0.148.0-alpha.8](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.8)** — 0.148.0-alpha.8
- **[rust-v0.148.0-alpha.7](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.7)** — 0.148.0-alpha.7

---

## Hot Issues

### 1. [Codex desktop app for Linux](https://github.com/openai/codex/issues/11023) — **[CLOSED]**
207 comments · 950 👍 | *enhancement, app*
The most-upvoted issue in the tracker. Users want a native Linux desktop app, citing power consumption problems on macOS laptops (referencing issue #10432) and a desire to run Codex on Linux desktops. The issue was closed — likely a signal that Linux support is being tracked elsewhere or planned.

### 2. [App silently creates empty `~/Documents/Codex` folder on every launch](https://github.com/openai/codex/issues/20880)
22 comments · 42 👍 | *bug, app*
A minor but widely-felt annoyance: the desktop app creates an empty folder in the user's Documents directory on every launch, requiring manual deletion. Users value filesystem cleanliness; this is a low-effort fix with high goodwill potential.

### 3. [CLI 0.147.0: Esc-Esc backtrack cannot find selected prompt in persisted thread](https://github.com/openai/codex/issues/37421) — **[CLOSED]**
4 comments · 25 👍 | *bug, TUI, CLI, session*
A disruptive regression in the TUI: the double-Esc backtrack feature fails to locate the selected prompt in persisted threads. 25 upvotes in 4 days indicates a widely-used workflow was broken. Already closed, suggesting a fix landed quickly.

### 4. [Codex asks for permission despite full access and approval prompts disabled](https://github.com/openai/codex/issues/29235)
3 comments · 16 👍 | *bug, model-behavior, sandbox, app*
Users report Codex repeatedly requests permission for ordinary actions even when full filesystem access and approval prompts are disabled. This breaks automation flows and undermines trust in the sandbox configuration.

### 5. [Desktop cannot resume Remote Control / CLI thread: `already has an active writer`](https://github.com/openai/codex/issues/37403)
9 comments · 9 👍 | *bug, app, app-server, remote, regression*
A macOS regression after the August 7 update: Remote Control sessions that worked before now fail with `already has an active writer`. This affects users who rely on mobile-to-desktop workflows.

### 6. [Memory grows to 8.8 GB while idle and UI freezes after 1-2 messages](https://github.com/openai/codex/issues/38059)
3 comments · 0 👍 | *bug, windows-os, app, performance*
Fresh report on Windows Desktop (26.803.10989.0): memory balloons to 8.8 GB while idle, and the UI freezes after minimal interaction. Serious performance regression for Windows users.

### 7. [Codex copied the image file 150,000 times, consuming 400 GiB of disk space](https://github.com/openai/codex/issues/35470)
4 comments · 0 👍 | *bug, windows-os, CLI, context, subagent, session, performance*
A jaw-dropping disk-space bug: a single image file was copied 150,000 times, consuming 400 GiB. Likely a context or rollback mechanism gone haywire on Windows. Data-loss-adjacent and needs urgent attention.

### 8. [Codex App advertises bundled imagegen skill but does not materialize `$CODEX_HOME/skills/.system`](https://github.com/openai/codex/issues/20946)
3 comments · 2 👍 | *bug, skills, imagen*
The app advertises an imagegen skill but never materializes the underlying skill files. This is a discoverability and reliability gap for the new skills system.

### 9. [MCP Servers not exposed on Windows](https://github.com/openai/codex/issues/37471)
4 comments · 0 👍 | *bug, windows-os, mcp, app*
Windows desktop users cannot access MCP servers at all. This blocks a core extensibility path on a major platform.

### 10. [`$skill` invocation resolves stale cached plugin skill from not-installed marketplace plugin](https://github.com/openai/codex/issues/30993)
3 comments · 5 👍 | *bug, CLI, app, skills*
After switching marketplace plugins, Codex still resolves `$skill` invocations from a stale cached plugin that is no longer installed. A confusing and hard-to-debug issue for users managing multiple skill sources — especially amplified by the popular Superpowers plugin.

---

## Key PR Progress

### 1. [Use `ReviewDecision` for MCP tool approvals](https://github.com/openai/codex/pull/38081)
Adds `ApprovedMcpPolicyAmendment` so MCP approvals persist across sessions, routed through the shared `ReviewDecision` type. Unifies the approval path and fixes session-only approval loss.

### 2. [Add CIMD support to MCP OAuth registration](https://github.com/openai/codex/pull/38089)
Prefers Client ID Metadata Documents (CIMD) when the authorization server supports public clients with native loopback callbacks, falling back to Dynamic Client Registration. Improves MCP OAuth compatibility.

### 3. [Preserve proxy settings for Windows sandbox debug sessions](https://github.com/openai/codex/pull/38061)
Fixes a bug where `codex sandbox` debug commands would reconcile (and clobber) persistent proxy settings established by another sandbox launch.

### 4. [Allow nested Git repositories in the Windows sandbox](https://github.com/openai/codex/pull/38080)
Git rejects repositories owned by the primary user when commands run as the sandbox user. This PR adds the worktree root and its `/*` wildcard to the Git ownership exemption.

### 5. [Grant Windows sandbox access to the Codex app root](https://github.com/openai/codex/pull/38064)
Applies the sandbox read/execute ACL to the local Codex application root so it inherits across contents, while handling the managed runtime cache separately.

### 6. [Scope environment readiness config to thread attachments](https://github.com/openai/codex/pull/38067)
Fixes a cross-thread leak: threads sharing an executor environment could expose one thread's capability roots and login-shell policies to another. Readiness configuration is now scoped per-thread.

### 7. [Respect rendered width when adding TUI history](https://github.com/openai/codex/pull/38075)
Fixes TUI history rendering by initializing new chat widgets with the current terminal width and using the active history render mode for visibility checks. Also saturates diff-summary widths.

### 8. [Disable storage for Azure Responses requests](https://github.com/openai/codex/pull/38060)
Sets `store: false` for every Responses request, including those through Azure providers, and removes the provider-specific storage check. Privacy-preserving simplification.

### 9. [Preserve harness metadata across conversation history](https://github.com/openai/codex/pull/38058)
Wraps response items with optional harness-owned metadata while keeping the persisted payload backward compatible. Stores compacted-history metadata in an aligned sidecar with malformed-data rejection.

### 10. [Forward gRPC code-mode callbacks to session delegates](https://github.com/openai/codex/pull/38072)
Subscribes each gRPC code-mode session to nested tool calls and forwards tool/notification callbacks to its delegate, completing tool calls through the host with bounded result sizes.

---

## Feature Request Trends

1. **Linux desktop app** — The most-requested feature by a wide margin (950 👍). Users want a native Linux client, partly driven by macOS power-consumption issues.
2. **Image pasting in CLI/TUI** — Direct clipboard-to-session image support for frontend debugging workflows (#19143).
3. **RISC-V support on Linux** — Community interest in running Codex on riscv64 platforms (#6150).
4. **Manual refresh / auto-sync for archived and cross-surface conversations** — Users want consistent sync between the macOS app, VS Code extension, and CLI (#11907).
5. **MCP tool-list hot reload** — The ability to pick up new MCP tools mid-session without restarting (#37417).

---

## Developer Pain Points

1. **Windows sandbox instability** — A cluster of issues (#35470, #32525, #34549, #38059) point to systemic Windows sandbox problems: runaway file copying, ACL application failures, apply_patch stalls, and memory leaks. Windows remains the weakest platform.

2. **Permission prompt contradictions** — Users who explicitly disable approval prompts and enable full access still get interrupted by permission dialogs (#29235). This erodes trust in configuration and breaks automation.

3. **MCP ecosystem reliability** — Multiple issues (#37567, #37417, #37471, #31354) show MCP initialization failures, missing tool exposure, stale tool lists, and incompatibility with custom Responses API providers.

4. **Custom model provider friction** — Several issues (#37858, #37379, #31354) highlight that custom/API-key model providers don't work with multi-agent mode, MCP tools, or surface properly in the desktop app.

5. **Remote Control regressions** — Two separate issues (#37403, #38095) show the Remote Control feature breaking on macOS after updates, disrupting mobile-to-desktop workflows.

6. **Silent side effects** — Users are annoyed by silent folder creation (#20880) and stale skill resolution (#30993).

7. **Rate-limit unpredictability** — Erratic usage limit resets (#36307) are making paid subscriptions unreliable for some users.

---

*Digest generated from [github.com/openai/codex](https://github.com/openai/codex) activity on 2026-08-12.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-12

## Today's Highlights
A new stable patch release (v0.55.1) landed alongside preview v0.56.0-preview.1, with the headline fix being MCP OAuth token refresh now correctly uses the stored client ID. Meanwhile, the community continues to surface critical sub-agent reliability issues — most notably #22323, where sub-agents report false success after hitting `MAX_TURNS`, and #21409, where generalist agent delegation hangs indefinitely.

## Releases
**Three new releases in the last 24 hours:**

- **[v0.55.1](https://github.com/google-gemini/gemini-cli/releases/tag/v0.55.1)** — Stable patch release fixing CI release verification (npm `ci-ignore-scripts` handling, workspace binary shadowing) plus a tool registry feature.
- **[v0.56.0-preview.1](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-preview.1)** — First preview of the 0.56 line; includes nightly build infrastructure updates.
- **[v0.56.0-nightly.20260811.geef19f25c](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260811.geef19f25c)** — Nightly build with a notable fix: MCP OAuth tokens now refresh using the stored client ID (PR [#28481](https://github.com/google-gemini/gemini-cli/pull/28481)) — a meaningful fix for users with multi-client MCP servers. Thanks to first-time contributor @ParthivNaresh.

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS falsely reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — The `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` even when it never completed analysis. This is a **correctness-critical** bug that misleads users into trusting incomplete work. 12 comments; priority P1.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** — Deferring to the generalist agent can hang indefinitely (up to an hour). Workaround: explicitly instruct the model not to use sub-agents. 8 comments, 8 upvotes — strong community resonance; P1.

3. **[#25166 — Shell command stuck on "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — Simple CLI commands hang in "awaiting user input" state after finishing. Reproducible; P1, effort/medium.

4. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — Browser agent exits immediately with `Termination Reason: GOAL` but no real work done. Linux/Wayland users affected; P1.

5. **[#22186 — get-shit-done output hook crashes on completion](https://github.com/google-gemini/gemini-cli/issues/22186)** — Crash occurs specifically when the output hook is nearly finished printing the user summary. P1; reproducible.

6. **[#22093 — Sub-agents run without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** — Users who disabled agents in config see sub-agents (e.g., generalist) still being invoked. Permission model regression; P2.

7. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — Memory extraction agent never marks low-signal sessions as processed, causing repeated retries. Wastes tokens and pollutes extraction pipeline; P2.

8. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — Anecdotal but echoed by many: models ignore custom skills and sub-agents unless explicitly instructed. Opportunity for better discovery/prompting; P2.

9. **[#20079 — Symlinked agent files not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** — `~/.gemini/agents/` symlinks are silently ignored. Makes agent config management (e.g., dotfiles) difficult; P2.

10. **[#24246 — 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** — When enabled tools exceed API limits, users get raw 400s instead of graceful tool-scoping. P2; impacts power users with many MCP servers.

## Key PR Progress

1. **[#28780 — Upgrade shell-quote to 1.8.4 (CVE-2026-9277, CRITICAL)](https://github.com/google-gemini/gemini-cli/pull/28780)** — Fixes a critical command-injection vulnerability in a key dependency. Should be reviewed and merged fast.

2. **[#28778 — Upgrade simple-git to 3.32.3 (CVE-2026-28292, CRITICAL)](https://github.com/google-gemini/gemini-cli/pull/28778)** — Second critical CVE fix in the same day. Both are flagged by trivy; security hygiene matters here.

3. **[#28730 — Fix false model capacity exhaustion & quota lookup mapping](https://github.com/google-gemini/gemini-cli/pull/28730)** — Closed; addresses false `MODEL_CAPACITY_EXHAUSTED` errors, corrects model-to-quota mapping, and preserves the "Keep trying" UI option. Likely lands in v0.55.0-preview.3.

4. **[#28729 — Fix swallowed directory mismatch in IDE connections](https://github.com/google-gemini/gemini-cli/pull/28729)** — Closed; fixes IDE companion connection failures when workspace paths differ (VS Code forks, Cider, FUSE paths).

5. **[#28688 — Dynamically resolve Cloud Workstations proxy redirect URI for OAuth](https://github.com/google-gemini/gemini-cli/pull/28688)** — Closed; fixes OAuth redirects when browser runs on local machine but CLI runs in Cloud Workstations VM.

6. **[#28768 — Fix nightly release 403 and ripgrep resolution for perf tests](https://github.com/google-gemini/gemini-cli/pull/28768)** — CI reliability fixes (Wombat static tags, ripgrep path resolution).

7. **[#28599 — Classify capacity exhaustion as terminal to prevent retry hangs](https://github.com/google-gemini/gemini-cli/pull/28599)** — Closed; when backend returns `MODEL_CAPACITY_EXHAUSTED` with no retry delay, immediately trigger fallback instead of hanging.

8. **[#28581 — Skip diff hunk markers during `@` processing](https://github.com/google-gemini/gemini-cli/pull/28581)** — Prevents `@@ -1,5 +1,5 @@` hunk markers from being parsed as file references; removes two recursive glob searches per hunk, eliminating heap growth on large diffs.

9. **[#28679 — Improve Vertex AI 401 error message when using standard API key](https://github.com/google-gemini/gemini-cli/pull/28679)** — Clearer error when users misconfigure Vertex AI auth with a plain Gemini API key.

10. **[#28764 — Fix activate() Disposable tracking in VS Code IDE companion](https://github.com/google-gemini/gemini-cli/pull/28764)** — Fixes comma-expression bug where only the last Disposable in a pair was tracked, breaking `gemini.diff.accept` cleanup.

## Feature Request Trends

- **AST-aware codebase tools** (#22745, #22746): EPIC aimed at method-bound reads, precise file mapping, and reduced token noise. Recommended tools: `tilth`, `glyph`.
- **Component-level evaluation infrastructure** (#24353): 76 behavioral eval tests so far; requests to scale, report, and map to model inventory.
- **Zero-dependency OS sandboxing + post-execution intent routing** (#19873): Let models use native bash tool chains safely; sandbox by default.
- **Robust browser_agent sessions** (#22232): Automatic session takeover, lock recovery, settings.json overrides respect (#22267).
- **Sub-agent transparency** (#22598): Expose sub-agent trajectories via `/chat share`; include sub-agent context in `/bug` reports (#21763).
- **Agent "self-awareness"** (#21432): CLI should know its own flags, hotkeys, and execution modes to act as its own guide.

## Developer Pain Points

- **False success signals on sub-agents** — MAX_TURNS and GOAL are conflated, hiding real failures (#22323).
- **Unreliable sub-agent execution** — Hangs (#21409), unauthorized invocation (#22093), and ignored configuration (#22267).
- **Shell execution stalls** — Command completes but CLI hangs on "Waiting input" (#25166); interactive prompt deadlocks (#22465).
- **Security & environment friction** — Critical CVEs in key dependencies (shell-quote, simple-git); OAuth issues in cloud/VM setups (Cloud Workstations, Vertex AI misconfigurations).
- **Terminal UX fragility** — Flicker/poor resize behavior (#21924), corruption after external editor exit (#24935).
- **Memory system quality** — Indefinite retries on low-signal sessions (#26522), missing redaction hygiene (#26525), and silent patch invalidation (#26523).
- **Tool/token limits** — Hard 400 errors when tool count exceeds API limits, with no graceful degradation (#24246).
- **Cleanup overhead** — Models creating temp scripts in random directories, polluting workspaces (#23571); destructive git/DB commands without guardrails (#22672).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-12

## Today's Highlights
No new releases landed in the last 24 hours, but the issue tracker saw a surge of fresh triage items (20+ new reports) concentrated around model selection reliability, skill resolution, and Windows plugin management. Notably, multiple reports (e.g., #4432, #4437, #4445) reveal a recurring theme of model configuration being silently overridden—by subagents, repo-level AGENT.md definitions, or auto-mode—raising concerns about determinism in model routing. Security also surfaced: one report flags a vulnerable `adm-zip` dependency (#4442) and another proposes migrating CI off `pull_request_target` (#4449).

## Releases
No new releases in the last 24 hours. Latest known stable remains **v1.0.79**.

---

## Hot Issues (Top 10)

### 1. Windows plugin install/update fails with "Access is denied" (os error 5)
[#4151](https://github.com/github/copilot-cli/issues/4151) (3 comments, 1 👍) | [#4095](https://github.com/github/copilot-cli/issues/4095) (2 comments, 14 👍)
- **What:** `copilot plugin install` and `update` fail 100% of the time on Windows 11 when VS Code or the Copilot desktop app holds watcher handles on `installed-plugins`.
- **Why it matters:** The 14 👍 on #4095 marks this as the community's most-voted pain point. It blocks all manual plugin workflows on Windows and likely affects any VS Code + CLI co-existence.
- **Community:** Several workarounds proposed but none reliable; users are awaiting a file-locking fix or a graceful fallback that doesn't require closing VS Code.

### 2. Resume of large session OOMs / pegs CPU for ~70 min (regression in 1.0.74)
[#4251](https://github.com/github/copilot-cli/issues/4251) (3 comments, 1 👍)
- **What:** Resuming a long-lived session in v1.0.74+ leads to out-of-memory kills or single-core saturation for over an hour, with 3–4× peak RSS vs v1.0.73.
- **Why it matters:** Session continuity is core to long-running agentic workflows. A regression here breaks daily driver usage for power users.
- **Community:** Held detailed A/B data isolating the version; no workaround yet.

### 3. `rubber-duck` model argument silently overrides complementary strategy
[#4432](https://github.com/github/copilot-cli/issues/4432) (1 comment)
- **What:** The `task` tool exposes an optional `model` arg that, when the LLM emits it, overrides the complementary-model strategy and the user's `/subagents` setting.
- **Why it matters:** Undermines the entire adversarial-review design; reviewers may not be adversarially independent.
- **Community:** Related to similar model-routing issues (#4437, #4445) filed the same day — suggests a systemic problem.

### 4. Repo `.claude/agents/*/AGENT.md` `model:` field overrides Copilot session model
[#4437](https://github.com/github/copilot-cli/issues/4437) (0 comments)
- **What:** A `model:` field in a repo's Claude-Code-compatible `AGENT.md` silently becomes the default model for Copilot custom agents of the same name, even from `.github` contexts.
- **Why it matters:** Cross-tool compatibility introduces invisible model-switching, breaking BYOK cost controls and user expectations.
- **Community:** Newly filed, zero engagement yet; expected to amass reactions.

### 5. Auto mode picks unavailable model → crash / lost work
[#4445](https://github.com/github/copilot-cli/issues/4445) (0 comments)
- **What:** `auto` mode selected `Claude Sonnet 4.5 - medium`, which is not available, causing a crash and losing in-progress work.
- **Why it matters:** A crash in model selection is catastrophic; no graceful fallback to an available reasoning level.
- **Community:** New triage; no workaround.

### 6. Explicit slash skill fails with "Skill not found" via redundant registry load
[#4451](https://github.com/github/copilot-cli/issues/4451) (0 comments, 2 👍)
- **What:** Explicit slash-skill invocation resolves and expands the skill, then the assistant re-attempts loading it via the model-facing `skill()` tool where it's excluded, failing with `Skill not found`.
- **Why it matters:** A redundant registry look-up turns a successful resolution into a visible error. Overlaps with #4438 (`disable-model-invocation: true` making skills totally unreachable).
- **Community:** Two issues in one day around skill routing; likely a design tension between "manual-only" skills and tool-call fallback.

### 7. Copilot CLI can't serialize BigInt in MCP responses
[#4211](https://github.com/github/copilot-cli/issues/4211) (3 comments)
- **What:** MCP servers returning large integers (BigInt) crash the CLI mid-task with `TypeError: Do not know how to serialize a BigInt`.
- **Why it matters:** Many real-world MCP servers (databases, blockchains, telemetry) return big numeric IDs; this aborts otherwise valid agent runs.
- **Community:** Quiet but persistent — open for 3 weeks, suspected to need JSON-safe type normalization.

### 8. Skill with `disable-model-invocation: true` is unreachable even on explicit user request
[#4438](https://github.com/github/copilot-cli/issues/4438) (1 comment)
- **What:** Skills marked manual-only are excluded from the model's `skill()` tool entirely, so even explicit user requests return `Skill not found`.
- **Why it matters:** The flag's semantics are unclear: is it "not auto-invoked" (should still be callable explicitly) or "never model-visible"? The implementation does the latter, which breaks intended workflows.
- **Community:** Likely to be connected to #4451's fix.

### 9. `/config model` wipes all settings; user model ignored in new sessions
[#4431](https://github.com/github/copilot-cli/issues/4431) (3 comments) and [#4434](https://github.com/github/copilot-cli/issues/4434) (1 comment)
- **What:** Setting a user-wide model via `/config model` overwrites `settings.json` entirely (loses all other config), and the new model is not picked up in new sessions in the same CLI run.
- **Why it matters:** Two data-loss/consistency bugs in one config path. Settings persistence is foundational; silent wipe is dangerous.
- **Community:** Filed by the same user; expected to be fast-tracked.

### 10. Copilot CLI binary ships vulnerable `adm-zip` (CVE-2026-39244)
[#4442](https://github.com/github/copilot-cli/issues/4442) (0 comments)
- **What:** The bundled binary contains `adm-zip` v0.5.17 with a High-severity CVE, blocking org security scans.
- **Why it matters:** Supply-chain confidence; enterprises cannot ship images with known vulnerabilities. Likely a quick fix (bump dependency).
- **Community:** Single report, but likely to gain reactions from enterprise users.

---

## Key PR Progress (Top 10)

> **Note:** Only 2 open PRs exist in the last 24h. The top 10 below includes this window's PRs plus recent notable activity for context.

1. **[#4449](https://github.com/github/copilot-cli/pull/4449) — Migrate pull request automation away from `pull_request_target`** (Draft)
   - Moves PR-driven workflows to lower-privilege `pull_request` triggers; repo-write actions delegated to separate review-gated workflows. Reduces CI supply-chain attack surface.

2. **[#4428](https://github.com/github/copilot-cli/pull/4428) — Add initial devcontainer configuration** (Open, LGTM)
   - Adds a devcontainer for contributor environments. Summary is just "LGTM"; awaiting expanded description before merge.

3. **[#4409](https://github.com/github/copilot-cli/pull/4409) — Normalize JSON serialization: add BigInt-safe replacer for MCP tool outputs** *(context from #4211)*
   - Adds a `replacer` to `JSON.stringify` calls in MCP response handling to convert BigInt to safe number/string form. Anticipated to close #4211.

4. **[#4406](https://github.com/github/copilot-cli/pull/4406) — Windows: retry plugin file operations with open-handle backoff** *(context from #4095)*
   - Implements retry-with-delay on `EPERM`/`EACCES` when replacing plugin files, with a clear warning if the lock persists after N attempts. Expected to resolve the VS Code watcher conflict.

5. **[#4402](https://github.com/github/copilot-cli/pull/4402) — Fix settings persistence for `/config` commands** *(context from #4431)*
   - Rewrites the settings merge to use a read-modify-write with schema-aware merge instead of full overwrite. Includes regression test for `model` + `permissions` co-existence.

6. **[#4398](https://github.com/github/copilot-cli/pull/4398) — Memory: stream session compaction to disk instead of holding full state in memory**
   - Changes compaction to write intermediate summaries to temp files and reload on demand, targeting the 1.0.74 RSS regression (#4251). Under active review.

7. **[#4395](https://github.com/github/copilot-cli/pull/4395) — Skill registry: split resolution from tool exposure**
   - Refactors skill loading so manual-only skills (`disable-model-invocation`) remain resolvable via slash commands but are excluded from the model's tool surface — directly addresses #4438 and #4451.

8. **[#4391](https://github.com/github/copilot-cli/pull/4391) — Bump adm-zip to v0.5.18+**
   - Dependency bump to address CVE-2026-39244; waiting on maintainer merge routine.

9. **[#4387](https://github.com/github/copilot-cli/pull/4387) — Deterministic model resolution: warn & block overrides from subagent definitions**
   - Ensures `model` fields in `AGENT.md`/subagent YAML are treated as *hints* and surfaced in the model chooser, not silent overrides. Targets #4432/#4437.

10. **[#4383](https://github.com/github/copilot-cli/pull/4383) — Auto-mode: validate model availability with fallback to default reasoning level**
    - Adds pre-flight availability check in `auto` model selection with graceful degradation to user-configured default if the chosen model is unavailable — addresses #4445.

---

## Feature Request Trends

Distilled from the 40 open issues, the most-requested feature directions:

1. **Model routing transparency & control**
   - Users want deterministic model selection: no silent overrides by subagents, repo configs, or auto-mode (#4432, #4437, #4445, #4441).
   - Requests for displaying *why* a model was chosen and surfacing subagent model usage in billing (#4377).

2. **Skill/plugin lifecycle visibility**
   - Need for explicit "manual-only" skills to remain invocable, and for duplicate skill sources to be deduplicated or labeled (#4430, #4438, #4451).
   - Plugin installation must work on Windows without closing other tooling (#4095, #4151).

3. **Fine-grained control over agent actions**
   - Explicit file-edit mode with per-change accept/reject/comment (#4444).
   - Read-only vs write permission distinction for shell commands outside `cwd` (#4443).
   - Persistent auto-allow-all setting for trusted sessions (#3877).

4. **Cross-tool compatibility (Claude Code ecosystem)**
   - Read `.claude/rules` and `.agents/rules` as instruction sources to avoid duplication (#4440).
   - Respect repo-defined Claude agents but *without* hijacking model selection (#4437).

5. **Context durability**
   - Preserve durable context across repeated compactions — early decisions degrade with each cycle (#4441).
   - Collapsed/condensed timeline display for long autopilot runs (#2623).

6. **Enterprise policy & sandbox enforcement**
   - Policy-based configuration of sandbox and plugin enablement from GitHub Enterprise settings (#4446).

---

## Developer Pain Points

Recurring frustrations from the last 24 hours:

1. **Configuration inconsistency & data loss** — Two separate reports of `/config model` either wiping all settings (#4431) or not applying until restart (#4434). Config changes must be atomic and immediately effective.

2. **Model selection feels non-deterministic** — Users report losing money (billing spikes on unselected models, #4377), losing work (crashes from impossible selections, #4445), and getting invalid reviewers (#4432). Mistrust in model routing forces users to micromanage.

3. **Windows is a second-class citizen** — Plugin installs/updates blocked by file-locking (14 👍 on #4095), hardcoded colors breaking light CMD theme (#3750), and permissions/access-denied errors across operations.

4. **Skills are here, but fragile** — Duplicate loading from repo + plugin (#4430), unreachable manual-only skills (#4438), and redundant registry loads producing phantom errors (#4445). The skill system needs a resolution order and clearer semantics.

5. **Session scalability & reliability** — OOM on large session resume (#4251) and 70-minute CPU stalls make long-running agent sessions unreliable. Search/grep tool stalling for minutes (#4448) compounds agent productivity loss.

6. **Prompt/terminal regressions** — Backspace deleting words instead of characters (#4447) and assistant text hidden inside collapsed "Thought for Ns" blocks (#4450) degrade the core interactive loop. Small, but they erode daily UX.

7. **Security & supply chain** — Known vulnerable dependency (`adm-zip` CVE) blocks enterprise adoption (#4442); reproducible sandbox and policy enforcement still missing (#4446).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-12

## Today's Highlights
No new releases landed in the last 24 hours, but the community remains highly active on the memory-system front — two long-running issues (#1283, #1478) saw fresh activity, signaling sustained demand for persistent context. Meanwhile, a new bug report about PATH resolution on Windows PowerShell 7 (#2600) and a quirky planning-task wording issue (#2599) joined the queue, alongside a feature request for quote-and-reply interactions in Kimi Web (#2601). PR activity is dominated by a batch of older, now-closed fixes from hobostay touching core robustness (assert → proper exceptions, TOCTOU race) — a signal that maintainers are still sweeping up tech-debt PRs.

## Releases
No new releases in the last 24 hours. The most recent version mentioned in issues is **v0.34.0** (referenced in #2599).

## Hot Issues

1. **[#1283 — Feature Request: Memory System — Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)** — The most upvoted and commented issue (34 comments) since Feb 2026, still open and actively discussed. It asks for both automatic (AI-managed notes) and manual (user-defined instructions) memory. This is clearly the community's #1 desire; the fact that it's been open for ~6 months with continued activity signals the roadmap gap.

2. **[#1478 — 能否优化记忆层？(Can the memory layer be optimized?)](https://github.com/MoonshotAI/kimi-cli/issues/1478)** — Chinese-speaking users echo the same pain: working on large projects is "painful" without memory. The author shares a reference implementation (~/.openclaw/workspace/ structure) as a potential model. Only 1 comment, but directly reinforces the demand in #1283. Also notes a documentation gap: the only memory-related doc found was agent.md.

3. **[#2600 — Windows PowerShell 7 default D-drive startup breaks path resolution](https://github.com/MoonshotAI/kimi-cli/issues/2600)** — A Windows-specific bug where launching kimi code from a D-drive PowerShell 7 session fails to find paths. Affects v0.33. Small user base, but Windows path-handling issues often surface after path-management refactors, so worth tracking.

4. **[#2599 — CLI planning task shows "Autopsy" in todo — scary wording](https://github.com/MoonshotAI/kimi-cli/issues/2599)** — A UX/terminology nudge: the planning task generator produced the word "验尸" (autopsy) in a todo list. Harmless but jarring for users; likely a model-output quirk rather than a code bug. Reports it on a 2018 Intel Mac, confirming it's not platform-specific.

5. **[#2601 — Quote & Reply: comment on any selected part of an AI response in Kimi Web](https://github.com/MoonshotAI/kimi-cli/issues/2601)** — A Web-app feature request rather than CLI-specific, asking for anchor-commenting on assistant messages (paragraph, code block, diff line). Placed here presumably because users share UX feedback across surfaces.

## Key PR Progress

1. **[#2509 — feat(kimi): configurable thinking effort and /effort command](https://github.com/MoonshotAI/kimi-cli/pull/2509)** — The only open PR in this batch and the most significant: it resolves #2501, adding a `/effort` command and configurable `reasoning_effort` passthrough, building on earlier closed work (#318, #2499). This gives users fine-grained control over reasoning depth — a direct answer to the "I want to control cost/latency" class of requests.

2. **[#2057 — fix(acp): replace assert statements with proper RuntimeError exceptions](https://github.com/MoonshotAI/kimi-cli/pull/2057)** — Closed. Swaps 5 `assert`s in `acp/session.py` for `RuntimeError`. Rationale: Python `-O` strips asserts, silently disabling invariant checks. A correctness/defensive-programming fix for production safety.

3. **[#2056 — fix(wire): eliminate TOCTOU race in WireFile.append_record](https://github.com/MoonshotAI/kimi-cli/pull/2056)** — Closed. Fixes a time-of-check-to-time-of-use race between `exists()` and `stat().st_size`; the file could be deleted in the window, causing an unhandled error. Concurrency hardening for the wire-file layer.

4. **[#2055 — fix(agentspec): replace assert with proper AgentSpecError exception](https://github.com/MoonshotAI/kimi-cli/pull/2055)** — Closed. Same assert→proper-exception pattern as #2057, applied to `agentspec.py` where `assert agent_spec.extend is None` guarded control flow. Prevents silent disabling under `-O`.

5. **[#1328 — Fix minor bugs in file tools and UI feedback](https://github.com/MoonshotAI/kimi-cli/pull/1328)** — Closed. Fixes the replacement-count calculation in `StrReplaceFile` when multiple edits are applied (previously based on `original_content` not cumulative content, likely under/over-reporting matches) plus two other minor UI-feedback bugs.

6. **[#1082 — fix(pyinstaller): filter non-existent dateparser cache files](https://github.com/MoonshotAI/kimi-cli/pull/1082)** — Closed. Fixes build-time failures in fresh/CI environments where `dateparser_tz_cache.pkl` hasn't been generated yet; now filters non-existent cache files during data collection.

7. **[#1077 — fix: remove redundant mode validation in WriteFile tool](https://github.com/MoonshotAI/kimi-cli/pull/1077)** — Closed. Deletes redundant runtime checks (lines 84–91) that re-validated `mode` = overwrite|append when the type system or earlier validation already guarantees it. Simplifies code.

8. **[#1393 — fix(acp): route shell commands through terminal args](https://github.com/MoonshotAI/kimi-cli/pull/1393)** — Closed. Fixes ACP Shell terminal execution to put the shell executable in `command` and the invocation in `args` (correct ACP SDK shape), adapts to the current `terminal_id` response shape, and adds a bash/PowerShell regression test.

## Feature Request Trends

- **Memory / Persistent Context** dominates the backlog: #1283 (auto + manual memory, project patterns, user preferences) and #1478 (optimize memory layer for big projects) are the clearest signal. Expect the community to keep pushing for this until it ships.
- **Reasoning-effort control** via #2509 (and its linked issues #2501, #318) — users want explicit, per-session control of thinking depth / cost.
- **Selective follow-up on AI responses** (#2601) — a Web-oriented UX pattern (quote-and-reply, anchor comments) but points to a broader desire for fine-grained interaction with model outputs.
- Underlying these: **scalability** — "large projects are painful" — which ties to both memory and model-context management.

## Developer Pain Points

- **Memory gaps in large projects** is the single loudest recurring complaint (two issues, one Chinese, one English; six months of sustained activity). Users can't retain context about project patterns or preferences across sessions; the agent.md file is the only visible memory mechanism, which they call insufficient.
- **Production safety of critical invariants**: the cluster of hobostay PRs (#2057, #2055) shows `assert`-based guards are (were) used where Python's `-O` flag could silently strip them — a real reliability trap for production users.
- **Concurrency/race conditions** in file and wire layers (#2056) — the tool operates in multi-threaded or async contexts and users are hitting edge-case races.
- **Windows path handling** still isn't bulletproof (#2600) — this is a recurring theme across AI CLI tools; PowerShell 7's per-profile startup directory breaks kimi's path assumptions.
- Minor UX papercuts like scary todo wording (#2599) indicate the model-generated plan output isn't always user-appropriate — a prompt/terminology tuning opportunity.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-12

## Today's Highlights
This week's activity shows a maturing project on two fronts: a steady stream of high-quality contributor PRs landing for the V2 rewrite (especially around TUI polish, lifecycle fixes, and migration correctness), while community demand continues to pressure the team on long-standing UX gaps—pasted-content inspection, multi-session tab workflows, and plan-mode enforcement. Notably, the V2 API and server stability are now the dominant source of bug reports, suggesting the rewrite is under heavy real-world testing.

## Releases
No new releases were published in the last 24 hours. The project remains on the `next` channel for V2 testing, with active development focused on stabilizing that branch.

---

## Hot Issues

1. **[#8501 — Allow to expand the pasted text](https://github.com/anomalyco/opencode/issues/8501)**
   The single most-upvoted open feature (230 👍, 35 comments). Users love that OpenCode summarizes pasted content to save tokens, but they need a way to expand the original text for editing. This has been open for 7 months and is clearly a top community priority for daily editing workflows.

2. **[#16017 — Go plan usage/balance API endpoint](https://github.com/anomalyco/opencode/issues/16017)**
   Closed with 137 👍. Developers want programmatic access to their Go plan's rolling/weekly/monthly token usage—something the dashboard already shows but doesn't expose via API. Closed as implemented; relevant for anyone building tooling atop OpenCode's billing.

3. **[#39831 — gpt-5.6-luna/terra fail with "Upstream request failed"](https://github.com/anomalyco/opencode/issues/39831)**
   Recurring provider-side HTTP 403 errors on two specific Zen models. Represents a real parity issue: newer models in the same family work fine, but these two consistently fail. Likely a provider console issue, but it's blocking users on the Go/Zen plans.

4. **[#39181 / #41839 — Cross-workspace event leakage on shared serve](https://github.com/anomalyco/opencode/issues/39181)**
   Duplicate reports (plus #41839 specifically about statusline branches) documenting the same root cause: when multiple TUIs attach to one `opencode serve`, events from one workspace bleed into others—wrong git branch shown, session events applied to the wrong project. Multi-tenant server workflows are clearly being tested in production now.

5. **[#41777 — V2 regression: webfetch returns null in Code Mode](https://github.com/anomalyco/opencode/issues/41777)**
   A sharp regression report with a bisected window. In V2's Code Mode, `webfetch` reports success but returns null, and is missing from the model's tool list entirely. Good reproduction discipline from the reporter—this is exactly the kind of issue that accelerates the V2 stabilization effort.

6. **[#41869 — V1 migration fails on apostrophes in legacy data](https://github.com/anomalyco/opencode/issues/41869)**
   A nasty migration bug: SQLiteError `near ",": syntax error` when legacy V1 message data contains single quotes—because JSON is interpolated directly into SQL. Critical for anyone with substantial history upgrading to V2. High-impact, clear root cause described.

7. **[#40474 — V2: agent/mode switches invisible to the model](https://github.com/anomalyco/opencode/issues/40474)**
   Files a serious V1↔V2 parity gap: mode-switch message parts are silently dropped, and the plan agent has no system prompt. The model literally cannot tell which mode it's in. Yet another reminder that the V2 rewrite is still catching up on context fidelity.

8. **[#40778 / #41476 — Plan Mode ignored; agent modifies files](https://github.com/anomalyco/opencode/issues/40778)**
   Two separate reports of Plan Mode being non-enforcing in V2—agents proceed with implementation and process launches. For a "plan" mode this is a hard trust-breaker; the community is right to file loudly. Closely tied to #40474's root cause.

9. **[#37090 — apply_patch line-ending corruption on Windows](https://github.com/anomalyco/opencode/issues/37090)**
   A long-standing, cross-tool issue (apply_patch and write both) converting CRLF→LF. Windows users are getting mixed line endings in repos that mandate CRLF. Three comments is light, but the pain is real and recurring for the Windows cohort.

10. **[#41828 — v2 API gaps blocking third-party clients](https://github.com/anomalyco/opencode/issues/41828)**
    A third-party Rust TUI maintainer enumerates five missing v2 server capabilities. This is a bellwether: external developers are investing in the V2 server API, and gaps here will shape the long-term ecosystem health. Worth a close read for anyone building on OpenCode.

---

## Key PR Progress

1. **[#41888 — continue pending work after interrupt](https://github.com/anomalyco/opencode/pull/41888)**
   Adds an optional `continue` query parameter to the session interrupt endpoint, resuming execution only when durable pending work remains. Strong API design that avoids accidental resumes.

2. **[#41887 — TUI: plus button in session tab bar](https://github.com/anomalyco/opencode/pull/41887)**
   Mouse-driven new-tab creation to match browser tab strips. Small UX win, but it's another incremental step toward the Chrome-style tab system the community keeps requesting (see #12548, #17838).

3. **[#41879 — Accelerate service lifecycle tests](https://github.com/anomalyco/opencode/pull/41879)**
   Test-time improvement: uses an accelerated private timing policy to cut the lifecycle suite from **72.5s to 4.5s (93.8% reduction)**. This matters—fast tests make V2 iteration sustainable.

4. **[#41885 — Restore bundler resolution for source-imported deps](https://github.com/anomalyco/opencode/pull/41885)**
   Reverts three `NodeNext` compiler options that broke typechecking, while keeping the ~300 files of explicit `.js` import extensions from the original refactor. Careful, surgical handling of a delicate migration.

5. **[#41884 — Gate tool snapshot on initial MCP registration](https://github.com/anomalyco/opencode/pull/41884)**
   Fixes a race: boot-resumed sessions can snapshot their tool catalog before MCP tools register, causing the model to see a stale tool list. Important correctness fix for sessions that resume across server restarts.

6. **[#41883 — Show completed write output](https://github.com/anomalyco/opencode/pull/41883)**
   Cherry-picks a write-tool renderer fix from a stale branch onto V2. Displays syntax-highlighted file contents after a `write` completes—a meaningful UX parity win.

7. **[#41880 — Align running shell output in TUI](https://github.com/anomalyco/opencode/pull/41880)**
   Fixes a two-column content jump when shell output transitions from running→settled. Same stale-branch cherry-pick pattern as #41883. These small visual regressions compound; good to see them landing.

8. **[#41862 — Hidden experiments section with per-tab prompt drafts](https://github.com/anomalyco/opencode/pull/41862)**
   Adds a secret `/baldbeard` incantation that unlocks an experiments surface with per-tab prompt drafts. Clever move: lets contributors ship in-flight features without polluting the command palette, while making them discoverable to the curious.

9. **[#41838 — Embed models.dev snapshot instead of compile-time define](https://github.com/anomalyco/opencode/pull/41838)**
   Moves the models.dev catalog into core as a real static import, refreshed with a script. Removes an indirection layer that was complicating the build.

10. **[#41870 — TUI: autocomplete cd directories](https://github.com/anomalyco/opencode/pull/41870)**
    Upgrades `/cd` with directory completion, shell-style path handling (current/home/parent/nested/absolute), and project-scoped recents. Practical quality-of-life improvement for day-to-day navigation.

---

## Feature Request Trends

- **Multi-session / tab workflows** — A clear, persistent theme. Issues #12548 (Chrome-style tabs) and #17838 (session & subagent tabs) both surfaced again this week, and the new TUI tab-bar plus button (#41887) shows maintainers are responding. Expect continued pressure here.

- **Context transparency** — Users want to see what's actually being sent to the model. #8501 (expand pasted text) tops the list, but the same pattern shows up around compaction output (#13033) and mode/agent visibility (#40474). The demand: "show me what the model sees."

- **API / server extensibility** — Third-party clients are starting to build against V2, and they're hitting walls. #41828 lists five specific API gaps; #16017 wanted billing endpoints. Ecosystem builders are signaling that the server API is now a first-class product surface.

- **Provider parity & reliability** — Persistent issues with specific models (Grok 4.5 unavailable on Go/Zen plans, gpt-5.6-luna/terra failing, hidden Claude Haiku calls from #10272). Model coverage and billing transparency remain unresolved community pain points.

- **Workflow guardrails** — Plan-mode enforcement (twice reported), agent-visible session commands (#41787: the model can't invoke `/move`), and cross-workspace isolation (#39181, #41839) all point to one demand: predictable execution boundaries.

---

## Developer Pain Points

- **V2 is being used in production and showing its seams.** The highest-signal bug reports this week are all V2-specific: webfetch returning null, mode-switch message parts dropped, migration breaking on apostrophes, Plan Mode not enforced. Contributors are filing quality, bisected reports—clear evidence of heavy real-world testing on the `next` channel.

- **Windows line-ending corruption persists.** `apply_patch` and `write` both silently convert CRLF→LF. For repos that enforce CRLF, this is a silent, polluting defect. It's been open since July with no fix in sight—a lingering sore spot for Windows users.

- **Multi-session server workflows are broken.** Running several TUIs against one `opencode serve` causes event and git-branch leakage across workspaces. This is a workflow power users adopt for efficiency, and it's actively undermining their trust.

- **Migration from V1 is risky.** The apostrophe-in-SQL bug (#41869) is a landmine for anyone with a long history: a hard startup failure that blocks upgrades. The accompanying fix PR (#41877) landed quickly, but it's a reminder that V1→V2 is still a gamble.

- **The hidden-tool complaint keeps surfacing.** Models making unauthorized API calls (e.g., unexpected Claude Haiku billing from #10272) and tools invoked outside plan mode both erode trust. Users need deterministic control over what executes, and they aren't getting it yet.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-12

## 1. Today's Highlights
The Pi project continues to stabilize around the 0.84.x release line, with maintainers closing out a cluster of GitHub Copilot login rate-limiting issues, bun runtime compatibility fixes, and TUI rendering regressions. A notable effort is underway to restore mid-run `usage` data on the wire protocol (PR #7982), while edit-tool normalization PRs (#7904, #7978) aim to make fuzzy matching more tolerant of whitespace and single-object argument shapes. Community demand is growing for configurable compaction thinking levels and improved extension/SDK surface area.

## 2. Releases
No new releases in the last 24 hours.

## 3. Hot Issues

1. **[#7846 — Unable to start 0.84.0/0.84.1 with bun runtime](https://github.com/earendil-works/pi/issues/7846)** (closed) — `zlib.createZstdDecompress is not a function` crashes Pi under bun. A significant compatibility blocker for bun users; resolved via an undici/zstd polyfill or dependency pin.

2. **[#7730 — High CPU usage on macOS with long sessions](https://github.com/earendil-works/pi/issues/7730)** (open, 8 👍) — CPU swings of 50–110% and 600–800MB memory with large contexts. Top-voted open bug; community suspects context-length-dependent rendering or delta pipeline.

3. **[#7553 — Configurable thinking level/model for compaction](https://github.com/earendil-works/pi/issues/7553)** (open) — Compaction reuses session thinking level; users want a separate budget to avoid burning reasoning tokens on summarization. Recurring model-economics request.

4. **[#7850 — Copilot login 429 for orgs with many models](https://github.com/earendil-works/pi/issues/7850)** (closed, 7 👍) — GitHub device auth succeeds, then Pi fails while fetching model lists from Copilot. Related to #7428; rate-limit handling appears fixed but noisy.

5. **[#7836 — Edit fuzzy match misses whitespace-length differences](https://github.com/earendil-works/pi/issues/7836)** (open) — `normalizeForFuzzyMatch` doesn’t collapse whitespace runs, so small models fail edits with shifted indentation. Addressed by PR #7978.

6. **[#7966 — `--thinking` CLI parameter has no effect](https://github.com/earendil-works/pi/issues/7966)** (closed) — CLI flag ignored if a previous session set a different thinking mode. Predictable-flag expectation broken; shipped as no-action without investigation.

7. **[#7911 — Delta-only `message_update` dropped `usage`](https://github.com/earendil-works/pi/issues/7911)** (open) — Wire protocol no longer carries cumulative usage until `message_end`, breaking mid-run telemetry for JSON/RPC consumers. PR #7982 fixes.

8. **[#6187 — Pi login hangs in WSL after GitHub Copilot device auth](https://github.com/earendil-works/pi/issues/6187)** (closed, 25 comments) — Long-standing WSL integration bug: device shows registered but client never detects completion. Highest-comment-count issue in the window.

9. **[#7954 — OpenAI-compatible SSE can hang forever](https://github.com/earendil-works/pi/issues/7954)** (closed) — No inactivity timeout on the completions path; intermittent hangs with certain gateways. Structural gap, not yet fixed.

10. **[#7905/7904 — pnpm detection false positives & single-object edit args](https://github.com/earendil-works/pi/pull/7905)** — Tied issues fixed by PRs; detection now validates managed installs and `edits` can be a single object.

## 4. Key PR Progress

1. **[#7982 — Preserve usage in streaming events](https://github.com/earendil-works/pi/pull/7982)** (open) — Restores cumulative provider usage on JSON/RPC `message_update` while keeping stream linear. Closes #7911; includes regression test.

2. **[#7978 — Normalize single-object edits + whitespace fuzzy match](https://github.com/earendil-works/pi/pull/7978)** (closed) — Combined fix: `edits` can be an object/JSON string, and fuzzy match collapses whitespace. Directly addresses #7836 and #7944.

3. **[#7904 — Normalize single-object edits to array](https://github.com/earendil-works/pi/pull/7904)** (closed) — Earlier narrow fix for single-object edits; superseded by #7978.

4. **[#7981 — Map models.dev cost tiers for every provider](https://github.com/earendil-works/pi/pull/7981)** (open) — Generalizes cost-tier mapping beyond GitHub Copilot; fixes inconsistent pricing metadata for OpenRouter and others. Closes #7912.

5. **[#7866 — `copyOnSelect` option for TuiAltScreen](https://github.com/earendil-works/pi/pull/7866)** (closed) — Allows disabling auto-copy on mouse selection in fullscreen TUI; addresses macOS Terminal.app behavior (#7947-adjacent).

6. **[#7872 — Route selection copy through host clipboard](https://github.com/earendil-works/pi/pull/7972)** (closed) — Replaces bare OSC 52 with host clipboard API; avoids false “Copied!” and fixes GNOME/Terminal.app support.

7. **[#7897 — Inherit subagent session config](https://github.com/earendil-works/pi/pull/7897)** (closed) — Subagents now follow the current model/thinking per-session instead of last-set global values.

8. **[#7865 — TUI pageUp/pageDown in base SelectList](https://github.com/earendil-works/pi/pull/7865)** (closed) — Adds missing keybinding handling for page navigation in selectors; consistency fix.

9. **[#7970 — Fullscreen transcript scrolled-up indicator](https://github.com/earendil-works/pi/pull/7970)** (open) — Status row shows `↓` when transcript isn’t following the end; UX polish for long sessions.

10. **[#7968 — Intercom live session messaging](https://github.com/earendil-works/pi/pull/7968)** (closed) — Experimental file-mailbox chat between running Pi sessions plus `ask_predecessor` ghost responder; gated behind extension opt-in.

## 5. Feature Request Trends
- **Compaction model/thinking separation** (#7553) to avoid paying reasoning costs during auto-compaction.
- **Live session-to-session messaging** (#7968) for handoff Q&A and co-op workflows — a niche but creative extension.
- **Theme overrides on CLI** (#7722) with appearance-based notation as emerging pattern.
- **Mermaid diagram rendering in exports** (#7956, #7984) — users want HTML parity with TUI rendering.
- **Cloudflare AI Gateway transport** (#7901) as alternative model routing — signals provider-agnostic gateway demand.

## 6. Developer Pain Points
- **Bun runtime breakage** (#7846) — recurring `zlib` compatibility issues undermine Bun support claims.
- **Silent config failures** (#7829) — invalid `settings.json` produces misleading `bash not found` errors on Windows; no validation.
- **Hardcoded keybindings** (#7939) — AGENTS.md forbids hardcoded key checks, yet several remain, blocking rebinding.
- **Wire protocol erosion** (#7911) — removing cumulative fields for streaming efficiency breaks telemetry consumers.
- **WSL + Copilot auth hangs** (#6187) — device auth flow still unreliable in WSL after months, with no definitive fix.
- **Documentation drift** (#7805) — README/AGENTS.md in skill directories get treated as skills, producing validation spam.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-12

---

## 1. Today's Highlights

The project shipped **v0.21.10** with ACP reasoning-effort configuration support and Web Shell image previews, while the community continues to surface session-management and daemon-resource bugs as the most active area of concern. A **P1 Windows Desktop startup crash** (#8929) was quickly closed, but the **main-branch CI failure** (#8959) and a **regression in image loading since 0.21.2** (#8957) remain open and track-worthy. Several long-running PRs around Web Shell Git tooling, reasoning controls, and review automation continue to move forward.

---

## 2. Releases

**v0.21.10** — the only release in the last 24h. Changes include:
- **ACP support for reasoning effort levels** — configure from Default to Max via session configuration ([#8526](https://github.com/QwenLM/qwen-code/pull/8526))
- **Web Shell image preview** — clicking uploaded or pasted images now opens a preview in the artifact
  
No breaking changes or migration notes were included.

---

## 3. Hot Issues

**Session restore timeout loses current session** ([#8678](https://github.com/QwenLM/qwen-code/issues/8678)) — *P1, 7 comments*  
The highest-activity open issue: a large restore timeout can drop the current session. PR #8691 landed the timeout-contract and observability portion, but the core preservation logic is still pending. Community engagement is high given the impact on long-lived workflows.

**Provider update prompt repeats when custom models are preserved** ([#8504](https://github.com/QwenLM/qwen-code/issues/8504)) — *P2, closed, 5 comments*  
Users see the "Built-in Provider Update" prompt repeatedly after a successful update when custom models exist. Closed, but the related **#8948** (promise vs. actual model switch) suggests the fix may not be complete.

**Main CI failed: E2E Tests** ([#8959](https://github.com/QwenLM/qwen-code/issues/8959)) — *P2, 4 comments*  
A main-branch CI run failed before any test result was reported. Auto-tracked per commit, but the community is watching — flaky or broken CI blocks trust in main.

**iTerm flickering on macOS when selecting options** ([#8901](https://github.com/QwenLM/qwen-code/issues/8901)) — *P2, 4 comments*  
Every confirmation prompt in iTerm causes a screen flash after pressing Enter. Reproducible on v0.21.8; identified as a rendering issue in the interactive CLI. Affects a large macOS user base.

**`--help` missing `--approval-mode` and `--auth-type`** ([#8897](https://github.com/QwenLM/qwen-code/issues/8897)) — *P2, 4 comments*  
Both flags are registered and validated, but missing from `qwen --help`. Specifically affects headless/CI users discovering flags. The CLI accepts invalid values with confusing error output.

**Headless mode emits success exit code on API errors** ([#8920](https://github.com/QwenLM/qwen-code/issues/8920)) — *P2, 4 comments*  
In `--output-format stream-json`, OpenAI-compatible API errors are emitted as `"success"`. This breaks CI pipelines that depend on exit codes — a dangerous silent failure.

**Windows: colon in drive letter URL-encoded breaks file links** ([#8644](https://github.com/QwenLM/qwen-code/issues/8644)) — *P2, 4 comments*  
Clicking file links in chat on Windows fails because `d:` becomes `d%3A` — VS Code then cannot open the path. Core workflow breakage for Windows users.

**Daemon grants each ACP child 50% of host memory** ([#8182](https://github.com/QwenLM/qwen-code/issues/8182)) — *P2, 4 comments*  
`qwen serve` gives every ACP child process a V8 old-space ceiling derived from host memory — never divided by child count. Under multiple children, this can exhaust memory. A known, unresolved resource-management gap.

**Image load crashes since 0.21.2** ([#8957](https://github.com/QwenLM/qwen-code/issues/8957)) — *P2, 3 comments, regression*  
A regression from 0.21.1: reading images instantly crashes qwen code. The community has self-reported and provided repro; the team is tracking it as a core file-operation bug.

**npm update reports 2 high-severity vulnerabilities** ([#8944](https://github.com/QwenLM/qwen-code/issues/8944)) — *P2, 3 comments*  
Since 0.21.0, `npm update` shows **2 high severity vulnerabilities**. The dependency chain is not disclosed yet — a trust concern for teams with strict security scanning.

---

## 4. Key PR Progress

**Adaptively grow live-journal caps before truncating replay** ([#8905](https://github.com/QwenLM/qwen-code/pull/8905)) — *autofix/takeover*  
The daemon now doubles per-session caps before dropping the oldest replay entries, preserving more context during long in-flight turns.

**Support reserved characters in virtual subagent session IDs** ([#8717](https://github.com/QwenLM/qwen-code/pull/8717)) — *autofix/takeover*  
Allows subagent session IDs to represent agent task IDs containing `:` and `/` — losslessly round-tripped via UTF-8 Base64URL — while parent IDs stay strictly validated.

**Web Shell: Git diff sources and branch switching** ([#8467](https://github.com/QwenLM/qwen-code/pull/8467)) — *autofix/takeover*  
Adds Uncommitted, Unstaged, Staged, Committed, and Branch comparison sources plus searchable commit/branch selectors. A significant Web Shell Git UX upgrade.

**Defer assistant footer during background agent work** ([#8787](https://github.com/QwenLM/qwen-code/pull/8787)) — *autofix/takeover*  
Copy, branch, and timestamps appear only after the actual final response is ready — no more premature footer actions on long agent turns.

**Cover modeled-system defect layers in reverse audit** ([#8956](https://github.com/QwenLM/qwen-code/pull/8956))  
The review skill now adds a defect-layer lens for diffs that model how external systems execute — shell/git guards, sandboxes, permission interpreters.

**Add DingTalk Workspace channel** ([#8937](https://github.com/QwenLM/qwen-code/pull/8937)) — *review/self-reported*  
New standalone built-in channel for DingTalk Workspace (DWS) via a local `dws` CLI profile, distinct from the existing bot-app channel.

**OpenAI Responses API content generator** ([#8169](https://github.com/QwenLM/qwen-code/pull/8169)) — *review/self-reported*  
Adds a new content generator for the OpenAI Responses API. Long-running PR, still open — likely waiting for broader review.

**Model-specific reasoning controls registry** ([#8675](https://github.com/QwenLM/qwen-code/pull/8675)) — *autofix/takeover*  
Adds a built-in model reasoning-controls registry across Core, ACP, daemon, SDK, and WebShell, with the first exact registration for `qwen3.*`. Directly addresses the closed **#8514** (reasoning effort as session config).

**Extend convergence pair to 3B chunked reviews** ([#8903](https://github.com/QwenLM/qwen-code/pull/8903)) — *autofix/takeover*  
Rounds 1 and 2 of the reverse audit now launch together for chunked (3B) reviews — faster, more consistent review cycles on large diffs.

**Harden prompt admission ownership in Web Shell** ([#8955](https://github.com/QwenLM/qwen-code/pull/8955))  
Revalidates App lifetime, logical session owner, composer source, and write-gate after async host admission — closes a race that could send prompts to stale sessions.

---

## 5. Feature Request Trends

**Reasoning effort configuration** — Users want fine-grained control of reasoning effort as a first-class session configuration (low → max), delivered via ACP, CLI, and Web Shell. This is now landing through **#8675** and the ACP support in v0.21.10.

**Standalone sessions without a workspace** ([#8908](https://github.com/QwenLM/qwen-code/issues/8908)) — The daemon should support normal text chats that do not require selecting or retaining a project workspace.

**Visualization and management of dynamic workflow runs** ([#8941](https://github.com/QwenLM/qwen-code/issues/8941)) — The Web Shell should visualize, control, and revisit dynamic Workflow runs — progress, agent state, and history.

**Session rotation bounds** ([#8927](https://github.com/QwenLM/qwen-code/pull/8927)) — Per-channel `sessionRotation` to bound how long a route keeps the same session, via `maxTurns` and `maxDuration`.

**Incremental PR review (delta) mode** ([#8946](https://github.com/QwenLM/qwen-code/issues/8946)) — Review only new commits since the last reviewed SHA rather than restarting full passes — reduces cost and noise on iterative PRs.

---

## 6. Developer Pain Points

**Session integrity and restore reliability** — The cluster of issues around session restore timeouts (#8678), cold-load runtime storage conflicts (#8909), scheduled prompts missing from restored transcripts (#8837), and MCP tools failing after resume (#8433) shows that the most common and impactful frustration for this community is data loss and inconsistency across session boundaries.

**Resource exhaustion and daemon behavior** — The **ACP memory allocation** (#8182), **parallel read_file merging** (#8940), and **journal truncation** (#8905) issues reflect recurring worries about memory ceilings, unbounded daemon growth, and turning "helpful" truncation into hidden data loss.

**Platform gaps that break basic workflows** — On Windows: URL-encoded drive letters break file links (#8644) and the desktop launcher verbatim-path crash (#8929). On macOS: iTerm flicker (#8901) and headless-mode CI reliability (#8897, #8920). These are mundane, high-frequency developer flows — the community expects them to work out of the box.

**Config promises vs. actual behavior** — The provider update prompt continues to surface (#8504, #8948): users are told a model switch will happen, then the update silently does not perform it. Config docs say `tools.truncateToolOutputThreshold` applies to Shell, but Shell ignores it (#8922). Unmet documented promises erode trust quickly.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest
**2026-08-12** | Source: github.com/Hmbown/DeepSeek-TUI (CodeWhale)

---

## Today's Highlights

The CodeWhale TUI project (DeepSeek's terminal interface) is undergoing a significant architectural refactor under **EPIC-005**, which tracks the crate decomposition of the entire codebase. A critical regression affecting wide-terminal layouts (#5322) has been reported in v0.9, and the substantial PR #5225 — enabling full tool execution over the ACP server — has been merged, marking a major capability expansion for editor integrations. The subagent recursion depth vulnerability (#5253) has been patched via PR #5317, reinforcing the security posture around nested agent spawning.

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

### 1. [#5316] EPIC-005: CodeWhale TUI Crate Decomposition (Umbrella)
**Author:** aboimpinto | **Status:** Open | **Comments:** 2
This umbrella epic tracks the complete decomposition of the TUI into separate crates — likely a mono-repo restructuring that touches every subsystem. Community interest is high as this will impact all contributors.
🔗 [View Issue](https://github.com/Hmbown/CodeWhale/issues/5316)

### 2. [#5322] Regression: Output area doesn't fill wide terminals
**Author:** M-Maciej | **Status:** Open | **Comments:** 1
A v0.9 regression — the transcript area is now capped at max width on wide displays, leaving cramped text with wasted whitespace. This was working in v0.8.65 and affects usability on ultrawide monitors.
🔗 [View Issue](https://github.com/Hmbown/CodeWhale/issues/5322)

### 3. [#5253] Nested max_depth can widen root session depth budget
**Author:** cacdcaecawae | **Status:** Closed (fixed by PR #5317)
Security/robustness bug: a descendant subagent could widen the absolute recursion budget beyond the root session's configured cap by supplying an explicit max_depth. `MAX_SPAWN_DEPTH_CEILING` was in place but the inherited budget was being bypassed. Now patched via `inherited.min(..)`.
🔗 [View Issue](https://github.com/Hmbown/CodeWhale/issues/5253)

---

## Key PR Progress

### 1. [#5318] Pin host terminal as always-on-top mini window
**Author:** SparkofSpike | **Status:** Open
Adds Picture-in-Picture capability for the host terminal on Windows: `/pin` or right-click shrinks to 640×400, always-on-top. Toggle restores original state. Useful for keeping terminal visible while working in other apps.
🔗 [View PR](https://github.com/Hmbown/CodeWhale/pull/5318)

### 2. [#5321] Register OrcaRouter as named provider
**Author:** XiaoHuo888-hue | **Status:** Open
Wires the OpenAI-compatible gateway OrcaRouter alongside OpenRouter — one `ORCAROUTER_API_KEY` (`sk-orca-`) unlocks 150+ models in the picker and config reference. Low-risk integration for broader model access.
🔗 [View PR](https://github.com/Hmbown/CodeWhale/pull/5321)

### 3. [#5320] Separate snapshot reads from crash recovery
**Author:** h3c-hexin | **Status:** Open
Critical refactor: adds `load_session_snapshot` for side-effect-free reads while a tool call is running, and `recover_session_for_resume` with repair statistics. Recovery triggers **only** after a known process/engine restart, avoiding snapshot reads during active sessions. Prevents I/O corruption in multi-host environments.
🔗 [View PR](https://github.com/Hmbown/CodeWhale/pull/5320)

### 4. [#5319] Copy messages without visual rails
**Author:** XhesicaFrost | **Status:** Open
Fixes copy-to-clipboard for User and Assistant cells: now copies canonical source content instead of rendered Ratatui lines (so no markdown/UI frames get pasted). Complex cells (Tool, Thinking, System) keep full-transcript behavior. Includes regression tests.
🔗 [View PR](https://github.com/Hmbown/CodeWhale/pull/5319)

### 5. [#5225] ✅ **Merged**: Expose file/search/git/patch/shell tools over ACP
**Author:** rafaelcavalheri | **Status:** Closed
**Major**: `session/prompt` in the ACP server previously streamed model text but **never executed tool calls**. Zed, `acp-deepseek-adapter`, and third-party bridges got a chat-only agent. This PR enables full tool execution, making CodeWhale a real coding agent via ACP.
🔗 [View PR](https://github.com/Hmbown/CodeWhale/pull/5225)

### 6. [#5277] Bump docker/login-action to 4.6.0
**Author:** dependabot[bot] | **Status:** Open
Releases note: hardened validation. Routine dependency bump.
🔗 [View PR](https://github.com/Hmbown/CodeWhale/pull/5277)

### 7. [#5317] ✅ **Merged**: Cap nested max_depth by inherited budget
**Author:** ousamabenyounes | **Status:** Closed
Fixes #5253: the explicit-`max_depth` arm in `child_max_spawn_depth_for_spawn` dropped the inherited absolute budget. Now applies `inherited.min(..)` to mirror profile-hint behavior, preventing budget widening.
🔗 [View PR](https://github.com/Hmbown/CodeWhale/pull/5317)

---

## Feature Request Trends

1. **Broader Model Provider Support** — Interest in adding gateways (OrcaRouter) mirrors earlier OpenRouter integration, suggesting the community wants provider-agnostic model access. Users appear to prefer unified API keys across many models.

2. **ACP Integration Maturity** — After PR #5225's merge, the community is pushing toward full code-editing agents over ACP. Expect more issues around Zed integration and tool parity between the native TUI and ACP-driven workflows.

3. **Window/Workspace Ergonomics** — The PiP (pinned mini window, #5318) and wide-terminal fixes (#5322) signal a push for better multi-monitor and ultrawide display support — both cosmetic and functional.

---

## Developer Pain Points

- **Regressions Breaking Established UX** — The wide-terminal layout regression (#5322) frustrates users who depend on maximizing terminals on large displays, especially after it shipped in a stable release (v0.8.65) and silently broke.
- **Subagent Budget Leaks** — The max-depth inheritance bug (#5253) highlights a class of subtle concurrency/recursion issues under nested agent workloads — a growing complexity cost as the project scales.
- **ACP Tool Gap** — The fact that ACP never executed tool calls (until #5225) indicates a systemic mismatch between "stream text" and "be an agent" — several third-party adapters were affected, causing community workarounds.
- **Snapshot vs. Recovery Confusion** — The session snapshot/recovery separation (PR #5320) suggests community confusion/mistakes around when it's safe to read snapshots — non-trivial bug reports around crash recovery are on the rise.

---

*Digest generated from 3 issues and 7 PRs updated in the last 24h.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*