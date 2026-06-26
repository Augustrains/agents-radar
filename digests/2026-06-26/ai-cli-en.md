# AI CLI Tools Community Digest 2026-06-26

> Generated: 2026-06-26 02:02 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem — Cross-Tool Comparison Report
**2026-06-26**

---

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem continues to mature rapidly, with six major tools now competing for developer workflows. This week's data reveals an ecosystem in a **trust recalibration phase**: model quality concerns, cost transparency issues, and reliability regressions dominate community sentiment across every major tool. Claude Code faces a "trust earthquake" over silent model upgrades and Opus degradation allegations. OpenAI Codex is battling a severe server-side quota accounting bug that has consumed Pro users' budgets in minutes. Meanwhile, smaller tools like Pi and Qwen Code are shipping aggressively—Pi with a new orchestration daemon and Qwen Code with voice dictation—but struggling with Windows stability. The common thread: **reliability and predictability have overtaken feature velocity** as the primary community concern.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|--------|-------------|-------------|------------|-------------|-----------|----------|-----|-----------|--------------|
| **Issues (24h)** | 10 hot | 10 hot | 10 hot | 10 hot | 2 | 10 hot | 10 hot | 10 hot | 10 hot |
| **PRs (24h)** | 1 merged | 10 active | 10 active | 1 open | 0 | 10 active | 10 active | 10 active | 10 active |
| **Releases (24h)** | 1 (v2.1.193) | 6 (rust alphas + zsh) | 3 (stable, preview, nightly) | 1 (v1.0.66-0) | 0 | 1 (v1.17.11) | 0 | 0 | 1 (v0.8.65) |
| **Release cadence** | Weekly | Weekly+ ×3 | Daily | Bi-weekly | Sparse | Weekly | Weekly | Weekly | Daily |
| **Top issue engagement** | 32 👍 (#49747) | 385 👍 (#28224) | 8 👍 (#21409) | 11 👍 (#3596) | 0 👍 | 74 👍 (#20695) | 30 👍 (#4945) | P1 (#5873) | 4 comments (#3568) |

**Key observations:**
- **OpenAI Codex** has the highest community engagement by far (385 👍 on storage bug), but engagement masks frustration—it's the highest-pain community.
- **Claude Code** has concentrated engagement (32 👍 on a single tool-call bug) but lower overall voting volume than Codex.
- **Smaller tools** (Kimi, DeepSeek TUI) show dramatically lower engagement, reflecting smaller user bases.
- **Release velocity** varies 3×: Gemini CLI ships daily, while Kimi Code and Qwen Code shipped nothing this week.

---

## 3. Shared Feature Directions

Requirements appearing across multiple tool communities—these represent **industry-wide developer demands**:

| Feature Need | Appears In | Evidence |
|-------------|-----------|----------|
| **`/undo` command** | Codex CLI (#9203, 297👍), Qwen Code (#2342), Gemini CLI (implicit in session revert) | 3 tools, high demand. Users want safety nets for unintended changes. |
| **Model transparency / cost controls** | Claude Code (#71481, $506 shock), Codex CLI (#28879, 10-20× cost spike), OpenCode (#15585, free tier cap) | 3 tools. Developers demand predictable billing and model-selection visibility. |
| **MCP tool scaling & reliability** | Kimi Code (#2475, 212 tools), Gemini CLI (#24246, >128 tools 400 error), OpenCode (#33977, timeout budgets) | 3 tools. MCP ecosystem growing faster than CLI scaling logic. |
| **Session persistence & recovery** | Claude Code (#29017, VSCode history loss), Codex CLI (#3596, resume auth failure), Copilot CLI (#3596, #3680) | 3 tools. Session state is fragile across tool boundaries. |
| **Windows platform stability** | OpenCode (#33742, Bun segfault), Qwen Code (#5873, PowerShell OOM), Copilot CLI (#3501, scroll bar) | 3 tools. Windows is a consistent second-class platform. |
| **Live syntax highlighting** | Qwen Code (#5869, streaming code blocks), Pi (implicit TUI rendering) | 2 tools. Streaming UI polish is becoming table stakes. |
| **Headless / CI integration** | Pi (#6078, RPC session introspection), Gemini CLI (Cloud Run webhook), Copilot CLI (#3909, enterprise settings) | 3 tools. Enterprise wants automated, server-deployable agents. |
| **Accessibility (screen readers, localization)** | Claude Code (#3412, 269👍 paste preview), Codex CLI (#20489, VoiceOver), Claude Code (#71479, Japanese i18n) | 2 tools. Accessibility requests are rising, driven by enterprise compliance. |

**Emerging convergence:** The `AGENTS.md` file pattern (Qwen Code #4534, now closed) suggests the industry is moving toward standardized agent configuration files, akin to `.gitignore` or `Dockerfile`.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code |
|-----------|-------------|-------------|------------|-------------|----------|-----|-----------|
| **Primary model** | Claude Opus/Sonnet | GPT-5.5 | Gemini 2.5 | GPT-4o + multi | Multi-provider | Multi-provider | Qwen/GLM |
| **Target user** | Professional devs (pay-per-use) | Pro/Enterprise | Google ecosystem | GitHub ecosystem | Open-source devs | Tinkerers, SDK users | Chinese devs, cost-conscious |
| **Safety approach** | Auto-mode classifier (tightening) | Rate-limit enforcement | Sub-agent architecture | MCP + hook system | Provider-agnostic | Extension SDK | PreToolUse hooks |
| **Key differentiator** | Best-in-class reasoning (when working) | GPT-5.5 model quality | Deep Google Cloud integration | GitHub Copilot ecosystem | Session snapshots + revert | RPC SDK + orchestration | Chinese language support, low cost |
| **Weakest area** | Cost predictability, model regression | Quota accounting bugs | Sub-agent reliability | Windows/WSL2 rendering | Windows stability | TUI viewport stability | Windows PowerShell leaks |

**Strategic positions:**
- **Claude Code** and **OpenAI Codex** are competing head-to-head for the same "professional developer" segment, with Claude leading on feature velocity but Codex leading on community size.
- **Copilot CLI** is differentiating on enterprise integration (GitHub ecosystem, managed settings) rather than raw feature innovation.
- **Pi** and **OpenCode** are carving niches: Pi as an SDK/automation platform, OpenCode as a session-management leader.
- **Qwen Code** is the only tool explicitly targeting Chinese-speaking developers, giving it a unique moat.

---

## 5. Community Momentum & Maturity

### High Momentum (rapid iteration, growing community)
| Tool | Signal | Risk Factor |
|------|--------|------------|
| **Pi** | Orchestration daemon (#6064), RPC introspection (#6078), 10 PRs in 24h | Very small community; 30 👍 top issue |
| **Gemini CLI** | 3 releases/day, 10 PRs active, stable release | Low engagement (8 👍 top bug); slow community growth |
| **OpenCode** | Session snapshots (v1.17.11), MCP service scaffolding (#33988) | Memory megathread (74👍) unresolved; Windows segfault blocking upgrades |

### Moderate Momentum (established, but slower movement)
| Tool | Signal | Risk Factor |
|------|--------|------------|
| **Claude Code** | Auto-mode expansion, denial transparency | Trust crisis from model regression + cost shock |
| **OpenAI Codex** | MCP server re-use optimization (#30148), Codex Apps prototype | Severest pain point in ecosystem (quota bug); 385👍 on storage issue |

### Stalled / Low Activity
| Tool | Signal |
|------|--------|
| **Kimi Code** | 0 releases, 2 issues, 0 PRs in 24h; tiny community |
| **DeepSeek TUI** | Rebranding to CodeWhale causing confusion; only 1 release (rebrand only) |

**Maturity assessment:** OpenAI Codex and Claude Code are the most **mature** (largest communities, most infrastructure), but both face **trust crises** this week. Pi and OpenCode are the most **innovative** (shipping novel features like orchestration and session snapshots). Kimi Code appears to be **stalling**—minimal activity suggests maintainer bandwidth issues.

---

## 6. Trend Signals

### Critical Trend: Model Trust Deficit
The combination of:
- Claude Code: Opus 4.8 degradation allegations (#68780) + silent model upgrade ($506 cost, #71481)
- Codex CLI: 10-20× cost-per-token spikes (#28879, 302👍)
- Gemini CLI: Generalist agent hangs (#21409)

...creates a **systemic trust deficit** across the ecosystem. Developers can no longer assume models will perform consistently or cost predictably. **This is the highest-priority signal for tool maintainers to address.**

### Emerging Trend: Multi-Agent Orchestration
Three tools shipped orchestration features this week:
- Pi: `pi-orchestrator` daemon (#6064) managing multiple Pi instances via IPC
- Claude Code: Mesh-agent enrollment (#71482) + sub-agent improvements
- OpenAI Codex: Codex Apps as virtual HTTP MCP servers (#30000)

The industry is converging on **agent-as-service** architectures where CLIs manage agent lifecycles programmatically.

### Persistent Trend: MCP Ecosystem Scaling Pain
Across 4 tools, MCP server management is a top pain point:
- Tool count limits (Kimi: 212 tools, Gemini: >128 returns 400)
- Timeout management (OpenCode: split startup/request budgets)
- Resource confusion across servers (Gemini: #28143)
- OAuth token refresh failures (Codex CLI: #17265)

MCP is winning as the integration protocol, but **tool infrastructure hasn't caught up** to real-world MCP server counts (50-200+ tools).

### Warning Signal: Windows as Second-Class Platform
Windows-specific bugs appear in nearly every tool's top issues:
- OpenCode: Bun segfault (#33742) → blocking upgrade
- Qwen Code: PowerShell OOM (#5873) → profanity-level frustration
- Copilot CLI: Scroll bar corruption (#3501), clipboard quoting (#3534)
- Gemini CLI: Editor probing startup delay (#28144)

The Windows experience is **consistently worse** across the board, which will limit enterprise adoption where Windows is standard.

### Actionable Recommendations for Developers

1. **If you value cost predictability:** Avoid Claude Code's Opus models until Anthropic addresses silent upgrades (#71481). Use Sonnet or specify models explicitly.
2. **If you need Windows support:** OpenCode and Qwen Code have the most active Windows issues—monitor before upgrading. Consider Pi (fewer Windows issues reported).
3. **If you need multi-agent orchestration:** Pi's new orchestrator (#6064) is experimental but promising. Claude Code's mesh-agents are more mature but have safety false-positives (#71482).
4. **If you're an enterprise buyer:** Copilot CLI's managed settings (#3909) and authentication controls make it the safest choice for compliance. Codex CLI's quota bugs (#28879) are a liability.
5. **If you're building on MCP:** Budget for tool-scaling issues. Kimi Code (#2475) and Gemini CLI (#24246) are hitting limits at 128-212 tools. Plan to prioritize or group tools.

---

*Data sourced from community digests for Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code, OpenCode, Pi, Qwen Code, and DeepSeek TUI/CodeWhale. All dates: 2026-06-26.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of: 2026-06-26** | **Source:** [github.com/anthropics/skills](https://github.com/anthropics/skills)

---

## 1. Top Skills Ranking

The following Skills (Pull Requests) have generated the most community discussion and attention:

### #1: fix(skill-creator): run_eval.py always reports 0% recall — install the eval artifact as a real skill; fix Windows stream reading, trigger detection, and parallel workers
- **Author:** MartinCajiao | **Created:** 2026-06-10 | **Status:** Open
- **Functionality:** Comprehensive fix for the `skill-creator` evaluation pipeline, addressing a critical bug where `run_eval.py` consistently reports 0% recall. The fix installs the eval artifact as a real skill, corrects Windows stream reading, improves trigger detection, and enables parallel workers.
- **Discussion Highlights:** This PR addresses the most-discussed bug in the ecosystem—Issue #556, which has 10+ independent reproductions. The description-optimization loop was optimizing against noise, making every skill description appear equally ineffective. The community has been deeply engaged in diagnosing root causes across multiple platforms.
- **🔗 [PR #1298](https://github.com/anthropics/skills/pull/1298)**

### #2: Add document-typography skill: typographic quality control for generated documents
- **Author:** PGTBoos | **Created:** 2026-03-04 | **Status:** Open
- **Functionality:** Prevents common typographic problems in AI-generated documents—orphan word wrap (1-6 words spilling to next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment. These issues affect virtually every document Claude generates.
- **Discussion Highlights:** The community recognized this as addressing a universal pain point in AI document generation. The skill's specificity (orphan/widow detection) and the fact that users "rarely ask for good typography" made it a strong candidate for inclusion.
- **🔗 [PR #514](https://github.com/anthropics/skills/pull/514)**

### #3: fix(pdf): correct case-sensitive file references in SKILL.md
- **Author:** Lubrsy706 | **Created:** 2026-03-06 | **Status:** Open
- **Functionality:** Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where `REFERENCE.md` was referenced but the actual files use lowercase (`reference.md`, `forms.md`). This breaks on case-sensitive file systems (Linux/macOS).
- **Discussion Highlights:** A critical infrastructure fix that reveals systemic upstream quality issues. The PR has been open since March with slow maintainer response, reflecting community concern about PR review velocity.
- **🔗 [PR #538](https://github.com/anthropics/skills/pull/538)**

### #4: Add ODT skill — OpenDocument text creation and template filling and parse ODT to HTML
- **Author:** GitHubNewbie0 | **Created:** 2026-03-01 | **Status:** Open
- **Functionality:** Enables Claude to create, fill, read, and convert OpenDocument Format files (.odt, .ods). Supports template filling, ODT-to-HTML conversion, and triggers on mentions of "ODT", "ODS", "ODF", "OpenDocument", or "LibreOffice".
- **Discussion Highlights:** High community interest in expanding office format support beyond the existing DOCX skill. The bidirectional conversion (ODT ↔ HTML) was particularly noted as valuable for enterprise workflows.
- **🔗 [PR #486](https://github.com/anthropics/skills/pull/486)**

### #5: Improve frontend-design skill clarity and actionability
- **Author:** justinwetch | **Created:** 2026-01-05 | **Status:** Open
- **Functionality:** Revises the frontend-design skill to improve clarity, actionability, and internal coherence. Every instruction is designed to be executable within a single conversation, with guidance specific enough to steer behavior without over-constraining.
- **Discussion Highlights:** Exemplifies the community's growing sophistication around skill design principles—balancing specificity with flexibility, and ensuring skills are "actual instructions" rather than "vague suggestions."
- **🔗 [PR #210](https://github.com/anthropics/skills/pull/210)**

### #6: Add skill-quality-analyzer and skill-security-analyzer to marketplace
- **Author:** eovidiu | **Created:** 2025-11-06 | **Status:** Open
- **Functionality:** Two "meta skills" for evaluating other skills: the quality analyzer assesses across five dimensions (Structure & Documentation 20%, plus others), while the security analyzer identifies trust boundary vulnerabilities.
- **Discussion Highlights:** Directly addresses the community's growing concern about skill quality and security (see Issue #492). Meta-skills that "check other skills" represent a new category that the community is actively exploring.
- **🔗 [PR #83](https://github.com/anthropics/skills/pull/83)**

### #7: fix(docx): prevent tracked change w:id collision with existing bookmarks
- **Author:** Lubrsy706 | **Created:** 2026-03-06 | **Status:** Open
- **Functionality:** Fixes document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks. Root cause: OOXML shares `w:id` across bookmarks, tracked changes, comments, and move ranges—hardcoded IDs caused collisions.
- **Discussion Highlights:** Revealed the complexity of OOXML document manipulation. The community appreciated the detailed root-cause analysis and the specific fix to use dynamic ID generation with proper validation.
- **🔗 [PR #541](https://github.com/anthropics/skills/pull/541)**

### #8: fix(skill-creator): warn on unquoted description with YAML special characters
- **Author:** Lubrsy706 | **Created:** 2026-03-06 | **Status:** Open
- **Functionality:** Adds pre-parse validation in `quick_validate.py` to detect unquoted `description` fields containing `:` characters before YAML parsing, preventing silent truncation or multi-key splitting.
- **Discussion Highlights:** Multiple authors (Lubrsy706, Mr-Neutr0n in PR #361) independently identified and fixed this bug, indicating it was a widespread issue. The YAML parsing fragility is a recurring theme in skill-creator infrastructure.
- **🔗 [PR #539](https://github.com/anthropics/skills/pull/539)**

---

## 2. Community Demand Trends

From Issues analysis, the most-anticipated new Skill directions and community concerns are:

### 🔥 Critical Infrastructure Fixes (Highest Priority)
- **`run_eval.py` 0% recall bug** — Issue #556 (12 comments, 7 👍) is the most active bug. The optimization loop produces `precision=100% recall=0%` on every iteration, making the entire skill-creator pipeline non-functional. This affects PR #1298, #1323, and Issue #1169.
- **Windows compatibility** — Issues #1061 and #556 document three blockers: subprocess `PATHEXT` handling, `cp1252` encoding, and `select` on pipes. Multiple PRs (#1050, #1099, #1298) attempt fixes.

### 🔒 Security & Trust Boundaries
- **Issue #492 "Security: Community skills distributed under anthropic/ namespace enable trust boundary abuse"** — The most-commented issue (19 comments, 2 👍). Community skills impersonate official Anthropic skills, creating a vulnerability where users grant elevated permissions to unverified code.
- **Issue #1175** — Concerns about access control and permission logic within SKILL.md files, particularly for SharePoint Online integrations.

### 🏢 Enterprise & Organizational Features
- **Issue #228 "Enable org-wide skill sharing in Claude.ai"** (14 comments, 7 👍) — High demand for direct skill sharing within organizations without manual file transfer and upload.
- **ODT/ODS support** — PR #486 addresses the LibreOffice ecosystem, complementing DOCX and PDF skills.

### 🧠 Advanced Agent Patterns
- **Issue #412 "agent-governance"** — Safety patterns for AI agent systems, including policy enforcement and audit trails.
- **Issue #1329 "compact-memory"** — Symbolic notation for compact agent state, addressing context window efficiency for long-running agents.
- **PR #154 "shodh-memory"** — Persistent memory across conversations, using proactive context retrieval.

### ⚠️ Community Health Concerns
- **Slow PR review** — PRs like #538 (case-sensitivity fix) have been open since March 2026 with no merge action.
- **Duplicate skills** — Issue #189 (6 comments, 9 👍) reports that `document-skills` and `example-skills` plugins install identical content, wasting context window space.

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and are likely to land soon:

| Skill | PR | Created | Description | Why It's High-Potential |
|-------|-----|---------|-------------|------------------------|
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | 2026-03-22 | Full testing stack: Testing Trophy model, unit testing (AAA pattern), React component testing, accessibility testing, E2E with Playwright | Addresses universal developer need; comprehensive scope |
| **compact-memory** (Issue #1329 proposal) | [#1329](https://github.com/anthropics/skills/issues/1329) | 2026-06-17 | Symbolic notation for compact agent state—reduces long-running agent context waste | Directly addresses context window efficiency; follow-up to #1328 |
| **AppDeploy** | [#360](https://github.com/anthropics/skills/pull/360) | 2026-02-09 | Deploy and manage full-stack web apps to public URLs, including lifecycle management | Real-world deployment capability; author actively engaged |
| **codebase-inventory-audit** | [#147](https://github.com/anthropics/skills/pull/147) | 2025-12-16 | Systematic 10-step workflow for identifying orphaned code, unused files, documentation gaps | Practical maintenance tool; low-complexity value |
| **agent-governance** (Issue #412 proposal) | [#412](https://github.com/anthropics/skills/issues/412) | 2026-02-18 | Safety patterns: policy enforcement, threat detection, trust scoring, audit trails | Emerging category; security-conscious community demand |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a functional, cross-platform skill-creator pipeline**—the `run_eval.py` 0% recall bug has generated 3+ dedicated PRs (#1298, #1323, #1099), 2 parallel Issues (#556, #1169), and 4+ Windows compatibility patches, all converging on the same root problem: the core toolchain for building and evaluating skills is effectively broken on Windows and produces unreliable metrics on all platforms. Until this pipeline is stabilized, every other skill contribution is operating without a reliable evaluation mechanism.

---

# Claude Code Community Digest — 2026-06-26

## Today's Highlights

Anthropic shipped **v2.1.193** with a significant expansion to auto-mode: the `classifyAllShell` setting now routes **all** Bash/PowerShell commands through the classifier, not just arbitrary-code patterns — a major shift in how safety classification works. Meanwhile, a volatile sentiment wave is cresting: two separate reports (Issues #71481 and #68780) allege silent model upgrades and performance degradation in Opus 4.7/4.8, with one user reporting **$506 in unexpected charges**. The community is also watching a fresh zero-day bug (#71482) where the auto-mode safety block is misreading legitimate admin operations as security threats.

## Releases

**v2.1.193** — [View on GitHub](https://github.com/anthropics/claude-code/releases/tag/v2.1.193)

Key changes:
- **`autoMode.classifyAllShell` setting** — Extends auto-mode classification to all Bash/PowerShell commands (previously only arbitrary-code-execution patterns). This is a significant tightening for security-conscious teams.
- **Enhanced denial transparency** — Auto-mode denial reasons now appear in the transcript, as a denial toast notification, and in `/permissions` recent denials list. This directly addresses long-standing user feedback about opaque denials (see #71482).

## Hot Issues (10 Noteworthy)

**1. [#71481 — Silent default model upgrade to Opus 4.7 caused $506 in unexpected charges](https://github.com/anthropics/claude-code/issues/71481)** 🔥
- **Status:** Open | 👍: 0 (just filed)
- **Why it matters:** User reports Claude Code silently changed its default model from Sonnet 4.6 to Opus 4.7 with zero notification, triggering 15 automatic recharges. This is a **monetary trust crisis** — if true, it undermines cost-predictability assumptions for all API-billed users.

**2. [#68780 — Claude Opus 4.8 reasoning degradation, speed and performance regression](https://github.com/anthropics/claude-code/issues/68780)** 🔥
- **Status:** Open | 👍: 16 | Comments: 12
- **Why it matters:** User alleges "extremely poor reasoning, even on Max effort" and is threatening EU legal action for deceptive business practices. Matches pattern from #71446 ("Opus feels like old sonnet"). This aggregate sentiment wave could signal a real regression.

**3. [#71482 — Safety block halts authorized mesh-agent enrollment by misreading temporary loopback-only admin](https://github.com/anthropics/claude-code/issues/71482)**
- **Status:** Open | 👍: 0
- **Why it matters:** **Zero-day false positive** — the auto-mode classifier blocks legitimate defensive-hardening admin work. Critical for any team using mesh-agents or automation tooling. Filed today, so expect rapid attention.

**4. [#49747 — Opus 4.7 mixes legacy XML tool-use format into JSON tool calls on longer payloads](https://github.com/anthropics/claude-code/issues/49747)**
- **Status:** Open | 👍: 32 | Comments: 29
- **Why it matters:** Model outputs malformed tool calls mixing legacy XML with JSON schemas under load. This is a **reproducible** regression affecting MCP tooling and structured agent workflows. High engagement signals widespread impact.

**5. [#3412 — Allow viewing and editing content of “pasted text” blocks before submission](https://github.com/anthropics/claude-code/issues/3412)** 🏆
- **Status:** Open (enhancement, area:a11y) | 👍: 269 | Comments: 76
- **Why it matters:** **Highest-voted open issue.** Dictation/mobility users can't review pasted text before submission — blocker for accessibility. A year old and still unresolved; community frustration is visible in 76 comments.

**6. [#9516 — User Interrupt Hook](https://github.com/anthropics/claude-code/issues/9516)**
- **Status:** Open (enhancement) | 👍: 43 | Comments: 23
- **Why it matters:** Users want programmable hooks that fire when they interrupt Claude mid-response (e.g., to save state, log context). High demand for integration-style extensibility.

**7. [#18009 — Slack plugin fails to authenticate](https://github.com/anthropics/claude-code/issues/18009)**
- **Status:** Open | 👍: 49 | Comments: 19
- **Why it matters:** "Does not support dynamic client registration" — a core integration broken for Slack users. 5+ months open with high thumbs but low dev response.

**8. [#71486 — Feature request: `/feedback` without attaching session/context](https://github.com/anthropics/claude-code/issues/71486)**
- **Status:** Open (enhancement) | 👍: 0
- **Why it matters:** Privacy-conscious users want opt-out for context sharing in feedback submissions. Important for enterprise adoption where session data may be sensitive.

**9. [#71479 — Permission dialog / tool approval UI should support localization (Japanese)](https://github.com/anthropics/claude-code/issues/71479)**
- **Status:** Open (enhancement, area:tui) | 👍: 0
- **Why it matters:** First filed request for UI localization. Signals growing non-English user base hitting language barriers in critical tool-approval dialogs.

**10. [#71480 — API Error: Server is temporarily limiting requests](https://github.com/anthropics/claude-code/issues/71480)**
- **Status:** Open (duplicate) | 👍: 0
- **Why it matters:** Rate limiting errors reported for Windows. Though marked duplicate, adds to pattern of API reliability complaints, especially on Windows platform.

## Key PR Progress

**1. [#63686 — Bump stale and autoclose timeouts from 14 to 90 days](https://github.com/anthropics/claude-code/pull/63686)** ✅ *Merged*
- **Why it matters:** Massively increases the window before issues are marked stale/closed. Direct response to community frustration that issues were being auto-closed before maintainers could triage them. Now merged — expect fewer abrupt "closed due to inactivity" surprises.

## Feature Request Trends

The community is converging around these key unmet needs:

- **Desktop & IDE UX parity** — Multiple issues (#61415 macOS permissions bypass, #29017 VSCode history loss, #70885 chat panel doesn't scroll to session start) show the desktop app and VSCode extension are feature-incomplete compared to CLI. This is a major friction point for enterprise users who prefer GUI workflows.

- **Sandbox customization (Linux)** — Issue #44180 calls for `allowUnixSockets` equivalents for bwrap/seccomp BPF on Linux, mirroring macOS capabilities. Power users need consistent sandbox controls across platforms.

- **Agent & multi-session ergonomics** — #54179 (GUI SSH sessions invalidating each other), #70958 (sub-agent auth failures misreported), and #70219 (tmux sessions lose transcript files) reveal growing pains in the sub-agent / Cowork ecosystem. The architecture needs hardening for production multi-session use.

- **Cost transparency & model defaults** — #71481 (silent model upgrade) and #68780 (perceived Opus degradation) represent a **trust deficit**. Users want explicit model selection, cost caps, and change logs for default model assignments.

- **Localization** — #71479 (Japanese localization for permission dialogs) is the first explicit l10n request, but signals an emerging need as the user base globalizes.

## Developer Pain Points

| Pain Point | Signal | Issues |
|---|---|---|
| **Model regression anxiety** | 5+ reports in 2 weeks that Opus 4.8/4.7 performs worse than previous versions | #68780, #71446, #63687, #68354, #71481 |
| **Unexpected costs / silent upgrades** | User reports $506 shock; model changes without notification | #71481, #61869 (usage credits confusion) |
| **Auto-mode false positives** | Legitimate admin operations flagged as security threats | #71482, #30832 (cd + git whitelist bypass) |
| **Cross-platform inconsistency** | macOS features not available on Linux/Windows; VSCode vs CLI gaps | #44180, #29017, #71485 |
| **Session state fragility** | Loss of conversation history, truncated transcripts, auth token invalidation | #29017, #70219, #54179, #70501 |
| **Accessibility / input methods** | Dictation users can't preview pasted text; no interrupt hooks | #3412, #9516 |
| **Opus 4.8 tool-call malformation** | Mixed XML/JSON in tool outputs; stray tokens before calls | #49747, #63687, #68354 |

**Emerging theme this week:** The combination of **model-reliability complaints** (#68780, #71446) with **cost transparency issues** (#71481) is creating a "trust earthquake" in the community. Developers who bet on Claude Code as a daily driver are now questioning both the quality and cost-predictability of the Opus models. This is the single highest-risk signal for Anthropic to address in the coming week.

*Digest generated 2026-06-26 from 50 issues, 1 PR, and 1 release on [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code).*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-26

## Today's Highlights

A severe server-side rate-limit over-reporting bug is causing widespread quota exhaustion, with Pro users seeing 5-hour budgets consumed in under 41 minutes and Plus users reporting 10–20x cost-per-token spikes since June 16. On the infrastructure side, the team merged critical fixes reducing SQLite feedback log write amplification by ~85%, and new PRs signal a push toward "Codex Apps" as virtual HTTP MCP servers and managed thread defaults for enterprise deployments.

## Releases

- **rust-v0.142.2**: MCP tools now use tool search by default when supported (improving discovery while preserving backward compatibility). macOS authentication clients can honor system proxy/PAC/WPAD settings with `respect_system_proxy`.
- **rust-v0.143.0-alpha.25**, **alpha.22**, **alpha.21**, **alpha.16**: Successive alpha releases in the 0.143 pipeline.
- **codex-zsh-v0.1.0**: Initial Zsh plugin release.

## Hot Issues

1. **[#28879 — Codex (gpt-5.5, Plus) rate-limit cost per token jumped ~10-20x since June 16](https://github.com/openai/codex/issues/28879)**  
   302 👍, 152 comments. The top community pain point. Plus users report their 5-hour budget draining in 2–3 prompts. Session logs confirm limit-% consumed per token increased 10–20× with no model/plan changes. No official response yet.

2. **[#28224 — SQLite feedback logs can write ~640 TB/year, rapidly consuming SSD endurance](https://github.com/openai/codex/issues/28224)**  
   385 👍, 86 comments. Community-driven fix merged: three PRs reduce log volume by ~85%. Original issue closed by reporter after verifying the fix.

3. **[#30002 — Server-side quota over-reports consumption after 5h reset](https://github.com/openai/codex/issues/30002)**  
   4 👍, 24 comments. Pro accounts hitting `usage_limit_reached` after ~41 min / 1.35M tokens, while the same account earlier needed ~156M tokens for a full 5h window. Points to server-side accounting bug.

4. **[#29955 — Quota drained instantly: 100 credits gone after 1 message](https://github.com/openai/codex/issues/29955)**  
   4 👍, 23 comments. Pro 5h limit reset to 0% after a single message. Likely same root cause as #30002.

5. **[#9203 — Request to restore `/undo` command](https://github.com/openai/codex/issues/9203)**  
   297 👍, 50 comments. Users need `/undo` for recovering from unintended file deletions/modifications, especially when changes aren't tracked by git. Open since January 2026.

6. **[#30008 — "Selected model is at capacity" on multiple plans](https://github.com/openai/codex/issues/30008)**  
   1 👍, 22 comments. Both Codex app and CLI users on Pro 20 plans hitting model capacity errors. Suggests infrastructure scaling issues.

7. **[#25749 — No recovery path for inaccessible legacy phone number MFA](https://github.com/openai/codex/issues/25749)**  
   38 👍, 64 comments. Users signed in via Google OAuth cannot bypass legacy phone verification. No account recovery path exists.

8. **[#5957 — Auto compaction causes GPT-5-Codex to lose task context](https://github.com/openai/codex/issues/5957)**  
   9 👍, 31 comments. Compaction causes the model to forget mid-task edits, stops responding. Affects Enterprise users on `gpt-5-codex-high`.

9. **[#13733 — Background process polling wastes tokens with full history round-trips](https://github.com/openai/codex/issues/13733)**  
   23 👍, 30 comments. Each `write_stdin` poll during background builds triggers a full API round-trip with entire conversation history. Token burn scales with history × poll count.

10. **[#25719 — macOS syspolicyd/trustd CPU and memory runaway](https://github.com/openai/codex/issues/25719)**  
    54 👍, 34 comments. Codex Desktop on macOS repeatedly triggers macOS security daemon resource exhaustion, requiring system restart.

## Key PR Progress

1. **[#30148 — Reuse MCP runtimes when selected availability changes nothing](https://github.com/openai/codex/pull/30148)**  
   Prevents unnecessary MCP runtime teardown when a newly ready environment contributes no MCP servers or connectors. Performance optimization for multi-environment workflows.

2. **[#30000 — Prototype Codex Apps as virtual HTTP MCP servers](https://github.com/openai/codex/pull/30000)**  
   New `codex-apps` crate serving one authenticated loopback streamable-HTTP MCP endpoint per connector. Enables running Codex Apps via standard MCP infrastructure.

3. **[#30154 — Preserve status for evicted V2 agents](https://github.com/openai/codex/pull/30154)**  
   Fixes completed/errored agents becoming `NotFound` after LRU eviction by keeping bounded final status in `AgentMetadata`.

4. **[#30147 — Use managed defaults for TUI threads](https://github.com/openai/codex/pull/30147)**  
   Makes the TUI consume admin-configured defaults for new-thread model settings, enabling consistent model selection across CLI and Desktop.

5. **[#29683 — Add managed new-thread model settings](https://github.com/openai/codex/pull/29683)**  
   Server-side support for admin-defined persistent defaults for model, reasoning effort, and service tier on new thread creation.

6. **[#30149 — Make generated image directory configurable](https://github.com/openai/codex/pull/30149)**  
   Adds `generated_images_dir` config setting. When unset, maintains existing `$CODEX_HOME/generated_images/` behavior.

7. **[#30016 — Core: inherit current step environments in subagents](https://github.com/openai/codex/pull/30016)**  
   Fixes environment visibility for subagents spawned after deferred executors attach mid-turn.

8. **[#29516 — Persist Cloudflare affinity cookies for MCP HTTP](https://github.com/openai/codex/pull/29516)**  
   Ensures sticky sessions for hosted plugin-service Streamable HTTP MCP traffic behind Cloudflare.

9. **[#30112 — Add process-owned code-mode session client](https://github.com/openai/codex/pull/30112)**  
   New `ProcessOwnedCodeModeSessionProvider` with cancellation-safe ownership handoff for supervised child processes.

10. **[#29909 — Allow CCA image generation and web search extensions](https://github.com/openai/codex/pull/29909)**  
    Enables standalone image-generation and web-search extensions for the actor-authorized provider shape used by CCA, preserving legacy flows.

## Feature Request Trends

- **Session Reliability & Recovery**: Persistent demand for `/undo` command restoration (#9203, 297 👍) and better auto-compaction behavior that preserves task context (#5957).
- **Accessibility**: Screen-reader-friendly TUI mode with VoiceOver support (#20489). Community contributor has a local fix ready.
- **MCP Improvements**: Auto-refresh of OAuth-backed MCP tokens (#17265, #27165), better error handling for MCP tool discovery (#28640).
- **Desktop Controls**: Ability to disable automatic app updates (#18546), configurable image output directory (PR #30149).

## Developer Pain Points

- **Rate Limit & Quota Bugs**: The dominant theme this week. Multiple reports of phantom quota consumption (#28879, #30002, #29955, #30034, #29947). Server-side accounting appears broken since June 16, with no official acknowledgment.
- **Windows Instability**: Desktop sandbox helper (`codex-windows-sandbox-setup.exe`) triggers error dialogs on `apply_patch` (#29200, #30009). Update causes severe memory pressure destabilizing Windows (#30050).
- **macOS Security Daemon Exhaustion**: `syspolicyd`/`trustd` CPU and memory runaway persists across multiple versions (#25719, #28071).
- **Token Waste**: Background process polling burns tokens on every status check (#13733). MCP tool discovery blocks first model request on slow servers (#28640).
- **Compaction Reliability**: Auto-compaction causing model to lose mid-task context and stop responding (#5957). Context burn remains high even after compaction/new session (#29947).

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-26

## Today's Highlights

Three releases landed today: the stable **v0.49.0**, a **v0.50.0-preview.1** bringing tool registry dependency injection and critical CI fixes, and the **v0.51.0-nightly** build. The project's top-voted bug—generalist agent hangs (Issue #21409)—remains open with 8 thumbs-up after nearly four months, while new fixes landed for MCP cross-server resource confusion, thought leakage in history, and stale update_topic calls after session resets.

## Releases

- **[v0.51.0-nightly.20260626.gb14416447](https://github.com/google-gemini/gemini-cli/releases/tag/v0.51.0-nightly.20260626.gb14416447)** — Nightly build with CI fix from @galdawave preventing bad NPM releases and promote job crashes (PR #28147).
- **[v0.50.0-preview.1](https://github.com/google-gemini/gemini-cli/releases/tag/v0.50.0-preview.1)** — Preview release featuring tool registry dependency injection (`Feat/tool registry di`), workspace binary shadowing fix in release verification (PR #28132), and NPM publish script hardening (PR #28116).
- **[v0.49.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.49.0)** — Stable release with dependabot cooldown period for npm packages (PR #27743) and version bump scaffolding.

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — P1 bug where `codebase_investigator` subagent reports `status: "success"` after hitting the turn limit without doing any analysis. This masks real failures from users and downstream evaluation pipelines. 8 comments, 2 👍.

2. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** — P1 EPIC tracking the evolution of behavioral eval tests beyond the initial 76 tests introduced in Issue #15300. Critical for ensuring quality across the 6 supported Gemini models. 7 comments.

3. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** — The most upvoted open bug (8 👍). Simple folder creation causes indefinite hangs when the CLI defers to the generalist agent. Workaround exists (disabling sub-agents) but underscores systemic reliability concerns. 7 comments, open since March 6.

4. **[#22745 — Assess AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** — EPIC investigating whether AST-aware tools can reduce turn count, token noise, and misaligned reads. The downstream issue [#22746](https://github.com/google-gemini/gemini-cli/issues/22746) suggests tilth or glyph as starting points. 7 comments.

5. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — Despite custom skills and sub-agents being a core feature, the model rarely invokes them autonomously. User reports the model will use them only when explicitly instructed, even for highly related tasks (e.g., gradle/git skills). 6 comments.

6. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — Security concern: Auto Memory reads local transcripts and sends them to the model *before* the extraction prompt attempts redaction. Content is already in model context before any filtering occurs. 5 comments.

7. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — Sessions are only marked "processed" on successful `read_file`. Low-signal sessions the agent skips remain unprocessed and keep getting re-surfaced. 5 comments.

8. **[#25166 — Shell command execution gets stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1 core bug with 3 👍. After simple CLI commands (that do not request user input), the shell hangs showing "Awaiting user input". High frequency of community reports. 4 comments.

9. **[#24246 — Gemini CLI encounters 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** — When more than ~128 tools are available, the API returns a 400 error. No tool-scoping or prioritization logic exists. 3 comments.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** — The model occasionally uses `git reset --force` or other destructive commands when safer alternatives exist. Community member @abhipatel12 flags the need for guardrails around database modifications and branch management. 3 comments.

## Key PR Progress

1. **[#28147 — Prevent bad NPM releases and promote job crashes](https://github.com/google-gemini/gemini-cli/pull/28147)** — Critical CI fix: reorders release verification so integration tests run *before* `npm publish`, preventing dangling NPM packages without GitHub tags. Merged into nightly.

2. **[#27971 — Strip thoughts from scrubbed history turns](https://github.com/google-gemini/gemini-cli/pull/27971)** — Fixes "Thought Leakage" where model internal monologues leak into plain-text history, causing infinite loops and confusion. Surgical regex stripping plus a new public reporting surface for upstream fixes.

3. **[#28143 — Resolve MCP resources by server](https://github.com/google-gemini/gemini-cli/pull/28143)** — Fixes `read_mcp_resource` returning wrong server's content when two MCP servers share a URI. Splits resources by server; solves "always allow" approval reading from every server.

4. **[#28153 — Ignore stale update_topic calls after session reset](https://github.com/google-gemini/gemini-cli/pull/28153)** — Prevents orphaned `update_topic` tool calls from writing to `topicState` after a `/clear`. Race condition fix with version-checking on topicState.

5. **[#28015 — Cloud Run webhook ingestion service for Caretaker Agent](https://github.com/google-gemini/gemini-cli/pull/28015)** — New service architecture: GitHub webhook payload verification, Firestore transaction storage, and Pub/Sub sanitized issue metadata. Large feature (size/xl).

6. **[#28149 — Respect .gitignore/.geminiignore in skill resource listing](https://github.com/google-gemini/gemini-cli/pull/28149)** — Fix: `getFolderStructure()` was called without a file service for skill activation, meaning ignored files leaked into the model's view of available resources.

7. **[#27979 — Wrap read_mcp_resource output with wrapUntrusted()](https://github.com/google-gemini/gemini-cli/pull/27979)** — Security consistency fix: MCP resource text from servers now receives the same trust boundary treatment as MCP tool output.

8. **[#28144 — Detect available editors lazily to avoid slow startup](https://github.com/google-gemini/gemini-cli/pull/28144)** — `EditorSettingsManager` now defers editor probing. On Windows, `execSync` per editor was causing multi-second startup delays.

9. **[#28142 — Honor GOOGLE_CLOUD_LOCATION for Vertex AI with API key](https://github.com/google-gemini/gemini-cli/pull/28142)** — Fix: when using `GOOGLE_API_KEY` with Vertex AI, `GOOGLE_CLOUD_LOCATION` was silently ignored and requests routed to the global endpoint. Root cause in `@google/genai`.

10. **[#28148 — Copy packed artifacts from the builder stage in Dockerfile](https://github.com/google-gemini/gemini-cli/pull/28148)** — Multi-stage build bug: runtime stage was copying `.tgz` files from the wrong stage, causing build failures.

## Feature Request Trends

- **AST-aware file operations** (#22745, #22746): Strong community interest in moving beyond line-based file reads to method-level precision, reducing token waste and turn count.
- **Self-aware agent capabilities** (#21432): Users want the CLI to understand its own mechanics—hotkeys, CLI flags, configuration—well enough to act as its own guide.
- **Subagent trajectory sharing** (#22598): Request to expose subagent execution traces via `/chat share` for easier debugging and evaluation.
- **Automatic session takeover and lock recovery** (#22232): Browser agent resilience feature, requesting the agent handle orphaned Chrome profile locks gracefully instead of fail-fast.
- **Stop destructive behavior** (#22672): Guardrails around dangerous git commands and database operations, with model understanding of consequences.

## Developer Pain Points

1. **Agent hangs and indefinite waiting** — Issues #21409 (generalist hang), #25166 (shell stuck on "Waiting input"), and #22465 (stuck at interactive prompt) show a recurring pattern: the CLI gets into unresponsive states that require user cancellation. The #21409 workaround (disabling sub-agents) is a drastic mitigation.

2. **Sub-agent reliability and transparency** — #22323 (MAX_TURNS falsely reported as GOAL), #21763 (bug reports missing sub-agent context), and #21968 (sub-agents not used autonomously) reveal that sub-agents are both unreliable and opaque. Developers cannot inspect or debug sub-agent behavior easily.

3. **Memory system fragility** — #26522 (indefinite retries on low-signal sessions), #26525 (no pre-context redaction), and #26523 (silently skipped invalid patches) show the Auto Memory system has multiple failure modes that silently degrade performance or leak data.

4. **Tool overload and 400 errors** — #24246 (>128 tools triggers API error) and #21968 (model ignores available tools) highlight friction as the tool ecosystem grows. No intelligent tool selection or prioritization exists.

5. **Configuration and discovery gaps** — #20079 (symlinked agents not recognized), #22267 (browser agent ignoring settings.json), and #22093 (sub-agents running without permission after update) show configuration handling still has edge cases that surprise users.

---

*Data sourced from [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli). Digest generated 2026-06-26.*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-26

## Today's Highlights

A new patch release (v1.0.66-0) ships with experimental response budget controls and MCP server toggling, plus improved OpenTelemetry export for managed settings. The community is sharply focused on authentication bugs in resumed sessions—two separate issues (#3596, #3680) report model listing failures with `Error: Not authenticated` after resuming a session, drawing 18 combined upvotes. Additionally, Windows rendering problems and WSL2 clipboard failures continue to frustrate users.

## Releases

**v1.0.66-0** — [Release](https://github.com/github/copilot-cli/releases/tag/v1.0.66-0)

- **Added** toggle to enable/disable MCP servers from the MCP list view
- **Added** experimental response budget controls to CLI settings
- **Added** managed settings support for OpenTelemetry export configuration
- **Fixed** MCP tools on OAuth-authenticated remote servers now recover automatically after mid-session token expiry

## Hot Issues

1. **[#700 — List all supported models](https://github.com/github/copilot-cli/issues/700)** *(14 comments, 4 👍)*  
   Long-standing feature request for a `copilot --list-models` command showing available models and multiplier info. Community still actively discussing the API shape.

2. **[#2643 — preToolUse silent rewrite still shows confirmation](https://github.com/github/copilot-cli/issues/2643)** *(12 comments, 2 👍)*  
   Plugin hook authors cannot silently rewrite commands even when `permissionDecision: allow` is set. Forces interactive prompts on every hook execution.

3. **[#3596 — Error loading model list: Not Authenticated in resumed sessions](https://github.com/github/copilot-cli/issues/3596)** *(7 comments, 11 👍)*  
   **Hottest bug this week.** Resuming a session breaks `/model` command entirely. Users report this regression in v1.0.56. Similar issue [#3680](https://github.com/github/copilot-cli/issues/3680) confirms the pattern.

4. **[#3501 — Windows scroll bar misaligns text](https://github.com/github/copilot-cli/issues/3501)** *(5 comments, 9 👍)*  
   Vertical scroll bar introduced around v1.0.50 causes text rendering corruption on Windows Console Host and Terminal. No self-fix via Copilot prompts possible.

5. **[#3534 — WSL2 ARM64: `/copy` fails with clip.exe error](https://github.com/github/copilot-cli/issues/3534)** *(4 comments, 4 👍)*  
   `cmd.exe` quoting bug in 1.0.55-1 breaks clipboard writes on ARM64 WSL2. Reproducible on Ubuntu + aarch64.

6. **[#3636 — Voice mode fails due to unreachable model catalog on VPN](https://github.com/github/copilot-cli/issues/3636)** *(3 comments, 5 👍)*  
   Enterprise users on corporate VPNs cannot enable voice mode. Catalog fetch blocks the entire feature.

7. **[#3909 — Enterprise managed settings for local CLI](https://github.com/github/copilot-cli/issues/3909)** *(2 comments)*  
   Org admins need server-pushed configuration (especially `env` vars) for local CLI installs—currently only possible in cloud Agents/Codespaces.

8. **[#3925 — Linux AppImage leaks LD_LIBRARY_PATH to spawned git](https://github.com/github/copilot-cli/issues/3925)** *(1 comment)*  
   AppImage bundles break `git fetch` over HTTPS due to symbol lookup errors in libnghttp2. Blocks session creation entirely.

9. **[#3929 — argument-hint format validation too strict](https://github.com/github/copilot-cli/issues/3929)** *(1 comment)*  
   Skills fail to load when `argument-hint` uses array syntax (e.g., `[regression directory]`) instead of plain string. Breaks VS Code compatibility.

10. **[#3934 — MCP server blocked by policy with unclear reason](https://github.com/github/copilot-cli/issues/3934)** *(0 comments)*  
    Custom MCP registries trigger "blocked by policy" despite valid configs. No error details provided to users.

## Key PR Progress

*(Only 1 PR updated in last 24h)*

- **[#3928 — Add .gitignore and settings configuration](https://github.com/github/copilot-cli/pull/3928)** *(OPEN)*  
  Adds project `.gitignore` and basic settings scaffolding. No functional changes.

## Feature Request Trends

- **Model visibility** (#700, #3932): Users want `--list-models` for available models and a `/usage` command showing monthly quota/limits analogous to IDE plugins.
- **MCP management UX** (#2956, #3564, #3829): Multiple requests to make `/mcp show` editable (enable/disable) and asynchronous like `/tasks`.
- **Enterprise policy push** (#3909): Growing demand for org-admin control over local CLI settings, especially environment variables and model restrictions.
- **Session reliability** (#3596, #3680, #3931): Session resumption is the top pain point—authentication state is lost, sessions disappear from the list.
- **Fine-grained theming** (#2123, #3935): Users want per-element color control (borders, chevrons, prompt/response) beyond auto/dark/light themes.

## Developer Pain Points

1. **Session authentication decay** (#3596, #3680): Resumed sessions consistently lose model catalog access. Users forced to start new sessions to change models.
2. **Windows/WSL2 rendering bugs** (#3501, #3534): Two distinct platform issues—scroll bar text corruption and clipboard quoting—with no fixes in current release.
3. **Plugin/hook silent execution broken** (#2643): `preToolUse` with `permissionDecision: allow` cannot bypass confirmation dialogs, defeating the purpose of automated hooks.
4. **Enterprise network restrictions** (#3636, #3925, #3934): Multiple reports of VPN/corporate proxy breaking voice mode, git operations, and MCP server validation.
5. **Skill migration fragility** (#3938): Claude Code skills migrated to Copilot CLI are lost on update, no persistence guarantee documented.
6. **Feature parity gaps** (#3936, #3829): Claude Code parity requests (Ctrl+G paste expansion, async slash commands) indicate users switching between tools.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest**
**Date:** 2026-06-26  
**Analysis by:** Technical Analyst – AI Developer Tools

---

### 1. Today’s Highlights

No new releases were published in the last 24 hours, but two new bugs emerged on v0.19.2 highlighting instability in high‑MCP‑tool environments and persistent terminal re‑rendering on Linux. The community is watching closely as both issues directly impact developer productivity. No pull requests were updated or merged today.

---

### 2. Releases

- **None** – No releases were created in the last 24 hours. The current stable version remains **Kimi Code v0.19.2**.

---

### 3. Hot Issues

*Only two issues were updated in the last 24 hours. All are included below.*

1. **#2475 – [bug] MCP tools**  
   *Reported by ptyll* – User has an MCP server with **212 tools**, but the CLI experiences issues when handling this scale.  
   **Why it matters:** MCP (Model Context Protocol) is a core integration point; scaling beyond a handful of tools is a common enterprise requirement. Zero comments so far suggests early awareness.  
   *Link:* [MoonshotAI/kimi-cli Issue #2475](https://github.com/MoonshotAI/kimi-cli/issues/2475)

2. **#2474 – [bug] CLI interface shaking / full re‑rendering**  
   *Reported by yudichimiantiao* – On Linux (Kernel 5.10), the terminal constantly re‑renders the entire conversation from scratch, making the CLI unusable.  
   **Why it matters:** Affects the core user experience on a major platform. No comments yet, but the title has already received 👍 (emoji reactions likely incoming).  
   *Link:* [MoonshotAI/kimi-cli Issue #2474](https://github.com/MoonshotAI/kimi-cli/issues/2474)

---

### 4. Key PR Progress

- **None** – No pull requests were updated, merged, or opened in the last 24 hours.

---

### 5. Feature Request Trends

*Based on the two active issues,* the most visible requests from the community today center on:

- **MCP tool scaling** – Support for MCP servers with hundreds of tools without errors or performance degradation.
- **Terminal stability** – Elimination of unnecessary re‑rendering on Linux terminals, especially on older kernels (5.10+).

No broader trends can be inferred from such a small sample. However, these two issues point to a pattern: **reliability at scale** (MCP) and **platform‑specific rendering** are top of mind for early adopters on v0.19.2.

---

### 6. Developer Pain Points

- **High‑tool‑count MCP servers cause bugs** – Developers integrating rich MCP ecosystems (200+ tools) encounter blocking issues. This is a scalability pain point for power users.
- **Linux terminal instability** – Spontaneous full re‑renders break the chat workflow on Linux, making the CLI effectively unusable for affected users.
- **Lack of workarounds** – Neither issue has comments or PRs yet, indicating the community is still assessing the severity or waiting for maintainer guidance.

---

**Note:** This digest was compiled from a very low‑activity day (only 2 Issues, 0 Releases, 0 PRs). For a more complete picture, please follow the GitHub repository directly.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-26

## Today's Highlights
The OpenCode team shipped **v1.17.11** with a core usability breakthrough—session snapshots with revert controls—and a critical OAuth fix for headless environments. Meanwhile, the community is grappling with a **Bun segmentation fault on Windows** (45 comments) that makes v1.17.10 unstable, while the SDK team landed two important `sdk-next` PRs for embedded host configuration and session metadata support.

## Releases
**v1.17.11** — [View Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.11)

**Core:**
- **Session snapshots & revert controls:** Users can now roll a session back to an earlier message, including file changes—a major quality-of-life improvement for long coding sessions.
- **MCP OAuth URL fix:** The OAuth URL is now always printed to stdout, so manual sign-in works when the browser auto-open flow fails.

**Desktop:**
- Added Chrome-style behavior (details cut off in source, likely improved window/focus handling).

---

## Hot Issues (Top 10)

### #20695 — Memory Megathread [OPEN]  
[*103 comments · 74 👍*](https://github.com/anomalyco/opencode/issues/20695)  
The community's central hub for memory leak reports. Maintainers are requesting heap snapshots rather than AI-suggested fixes. This remains OpenCode's most-heated thread, indicating systemic memory pressure that v1.17.11's session snapshots may partially address.

### #33742 — v1.17.10 crashes with Bun segfault on Windows [OPEN]  
[*45 comments · 42 👍*](https://github.com/anomalyco/opencode/issues/33742)  
**Critical regression.** Upgrading to v1.17.10 triggers native Bun segmentation faults on Windows; v1.17.9 is stable. A related issue (#33903) shows the error persists even after reinstall/downgrade attempts. Community urgency is high—this is blocking Windows users from the latest features.

### #15585 — "Free usage exceed" on free models [CLOSED]  
[*52 comments · 13 👍*](https://github.com/anomalyco/opencode/issues/15585)  
Users hitting an undocumented free-tier cap on models advertised as "free." The community is split between those who see this as a bug vs. a soft limit. Closed without clear resolution, which may resurface.

### #16610 — Startup hang when inotify instances exhausted [OPEN]  
[*14 comments · 7 👍*](https://github.com/anomalyco/opencode/issues/16610)  
OpenCode hangs at startup when `fs.inotify.max_user_instances` is low—common on shared Linux servers or containers. No graceful degradation or error messaging.

### #32821 — GLM-5.2 returns 400: invalid message content [OPEN]  
[*8 comments*](https://github.com/anomalyco/opencode/issues/32821)  
OpenCode sends message content as an array `[{"text": "..."}]` instead of a plain string for GLM-5.2 via the Go provider. Model-specific serialization inconsistency.

### #33815 — v1.17.10 "internal server error" retrying, extremely slow [OPEN]  
[*3 comments*](https://github.com/anomalyco/opencode/issues/33815)  
Post-update to v1.17.10, responses are delayed by "years" and the app shows retry loops. Possibly related to the Bun segfault issue.

### #33945 — `ctx_execute(language: "javascript")` crashes desktop on Windows [CLOSED]  
[*3 comments*](https://github.com/anomalyco/opencode/issues/33945)  
Electron process crash when executing JavaScript via context tools on desktop. Closed quickly, suggesting a hotfix.

### #33399 — OpenCode CLI at 99-100% CPU, unresponsive [OPEN]  
[*6 comments*](https://github.com/anomalyco/opencode/issues/33399)  
Periodic CPU spikes make the terminal uninterruptible. Not present before v1.3.3. Possibly a regression in the TUI event loop.

### #33938 — Desktop app ConfigInvalidError after upgrade [OPEN]  
[*3 comments*](https://github.com/anomalyco/opencode/issues/33938)  
Post-v1.17.11 upgrade on Windows, the desktop app shows `ConfigInvalidError` in renderer.log and an empty sidebar despite valid SQLite data. Two root causes identified: a legacy fallback race and session filtering mismatch.

### #33966 — [FEATURE] Make OAUTH_CALLBACK_HOST configurable [OPEN]  
[*2 comments*](https://github.com/anomalyco/opencode/issues/33966)  
A recent PR bound the OAuth server to 127.0.0.1, breaking remote/Docker usage. Request to expose `OAUTH_CALLBACK_HOST` as a configuration option.

---

## Key PR Progress (Top 10)

### #33822 — Use Bun canary for beta channel [OPEN]  
[PR #33822](https://github.com/anomalyco/opencode/pull/33822)  
Bumps CI to Bun canary because "Bun 1.3.14 segfaults lots on Windows." Direct response to #33742. The Rust rewrite of Bun is noted as more stable—high impact if merged.

### #33281 — Standalone v2 session flow [OPEN]  
[PR #33281](https://github.com/anomalyco/opencode/pull/33281)  
Adds a `--standalone` mode with a private server child process, v2 API session creation, and persisted share/revert state. This is architectural groundwork for session snapshots (#33945) and the session redesign.

### #33988 — Scaffold MCP service [OPEN]  
[PR #33988](https://github.com/anomalyco/opencode/pull/33988)  
New `MCP.Service` skeleton with connection lifecycle management (child Scope with connect/disconnect/finalizer wiring). Part of a larger MCP reliability push.

### #33977 — Split MCP timeout into startup/request budgets [CLOSED]  
[PR #33977](https://github.com/anomalyco/opencode/pull/33977)  
Replaces a single MCP timeout with independent `startup` and `request` budgets. Fixes flaky MCP tool calls and allows finer-grained user control. Merged quickly.

### #33926 — Refine small model defaults [CLOSED]  
[PR #33926](https://github.com/anomalyco/opencode/pull/33926)  
Fixes Azure and Vertex model fallback logic to avoid assuming catalog deployments. Prioritizes `gemini-flash` for Vertex. Important for enterprise users.

### #33922 — Gate session redesign to new layout [CLOSED]  
[PR #33922](https://github.com/anomalyco/opencode/pull/33922)  
Gates all visual changes from #33860 behind the new layout setting, preserving legacy styling as default. Prevents UI breakage for users who haven't opted in.

### #33860 — Refine session UI styling [OPEN]  
[PR #33860](https://github.com/anomalyco/opencode/pull/33860)  
Updates markdown/timeline UI to v2 tokens, fixes inline code path detection. Active design work on the session interface.

### #32490 — Append MCP server instructions to context [CLOSED]  
[PR #32490](https://github.com/anomalyco/opencode/pull/32490)  
Appends MCP server `InitializeResult.instructions` to the system context, making server-provided guidance visible to the LLM. Closes #30084 and #7373.

### #33984 — Use dropdown for project selector [OPEN]  
[PR #33984](https://github.com/anomalyco/opencode/pull/33984)  
Migrates prompt project selector from Popover to Kobalte DropdownMenu + RadioGroup. Improves accessibility and UX consistency. Alternative to #33978.

### #33918 — Include v2 plugin skills in legacy list [OPEN]  
[PR #33918](https://github.com/anomalyco/opencode/pull/33918)  
Fixes `/skills` and skill API to include v2 plugin-registered skills that were hidden from the legacy list. addresses #33896.

---

## Feature Request Trends

1. **MCP reliability & observability:** Multiple requests for better MCP timeout control (#33977, #33988), debug output obfuscation (#33711), and server instruction injection (#32490).
2. **Session lifecycle enhancements:** Rename sessions from UI (#33932), automatic title generation fixes (#31879), and session metadata APIs (#33964).
3. **Provider model auto-detection:** LM Studio (#23327) and GLM series users want automatic model discovery instead of hardcoded lists.
4. **Docker/headless support:** Making `OAUTH_CALLBACK_HOST` configurable (#33966) to support remote and containerized use cases.
5. **Keyboard shortcut forwarding:** IDE integration regressions (#27006) where shortcuts no longer pass through the embedded terminal.

---

## Developer Pain Points

- **Windows instability is the #1 pain point.** The Bun segfault (#33742) and related crashes (#33903, #33945) are blocking Windows users from upgrading. The PR moving to Bun canary (#33822) suggests the team is aware and acting.
- **Memory and CPU leaks are chronic.** The Memory Megathread (#20695) has been open since April with 100+ comments, and the 99% CPU utilization bug (#33399) is still unresolved. Session snapshots may help, but the root causes remain.
- **Model-specific payload bugs frustrate users.** GLM-5.2 (#32821) and OpenAI/GPT MCP serialization (#33341) show that OpenCode's abstraction layer doesn't handle model-specific quirks gracefully.
- **Slow startup times** are still a concern (#22227, 4 comments, 4 👍), especially for users with large repositories or many `.git` directories.
- **The `/compact` command doesn't work** (#17557) and actually *increases* context tokens—a silent failure that wastes user time and money on LLM calls.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-26

## Today's Highlights
A major TUI scroll-jumping bug (#6050) was closed after causing widespread frustration, while the community pushed forward on RPC session introspection (#6078) and a new experimental orchestration daemon (#6064). The most active discussion remains the long-standing `openai-codex` connection reliability issue (#4945), now with 71 comments and ongoing debugging.

## Releases
No new releases in the last 24 hours.

---
## Hot Issues

1. **#4945 — openai-codex Connection Reliability Issues** [OPEN, 71 comments, 👍30]  
   GPT-5.5 streaming leaves the TUI stuck on `Working...` with no output or error. Pressing Escape aborts the turn. Community has been debugging for over a month; 30 upvotes signal this affects many users.  
   https://github.com/earendil-works/pi/issues/4945

2. **#5825 — Streaming markdown forces scroll to bottom** [OPEN, 31 comments]  
   With `clear on shrink` enabled, Pi overrides manual scroll-up during fast streaming. This breaks reading longer responses mid-generation. High engagement suggests a common workflow complaint.  
   https://github.com/earendil-works/pi/issues/5825

3. **#5103 — pi-windows-x64.zip can't detect git-bash from PATH** [CLOSED, 23 comments]  
   Git Bash on Windows not found by the built-in bash tool. One of the more disruptive Windows-specific bugs, now resolved.  
   https://github.com/earendil-works/pi/issues/5103

4. **#6050 — TUI full redraw clears terminal scrollback** [CLOSED, 10 comments]  
   Frequent custom-UI redraws cause terminal scrollback to jump to session start. Root cause in core TUI renderer; fix deployed in last 24h.  
   https://github.com/earendil-works/pi/issues/6050

5. **#5595 — openai-completions maxTokens not passing through** [CLOSED, 8 comments, 👍2]  
   Together.ai / DeepSeek v4pro runs out of output tokens regardless of user `maxTokens` setting. Affects reasoning-heavy workflows.  
   https://github.com/earendil-works/pi/issues/5595

6. **#5989 — pi update broke extension pi-lovely-codex** [CLOSED, 7 comments]  
   Extension loading regression after update. Highlights the fragility of the npm-based extension resolver, especially in compiled binary builds.  
   https://github.com/earendil-works/pi/issues/5989

7. **#5671 — ~/.pi and cwd/.pi overlap** [CLOSED, 6 comments, 👍5]  
   Home-directory `.pi` collides with project-local `.pi` for users whose home is their working directory. Sparked architectural discussion about migrating to `~/.config/pi`. Highly upvoted.  
   https://github.com/earendil-works/pi/issues/5671

8. **#6061 — MiniMax-M2.7-highspeed context budget smaller than expected** [CLOSED, 4 comments]  
   Long conversations fail at ~131k tokens despite higher advertised limits. Provider-level issue with context window enforcement.  
   https://github.com/earendil-works/pi/issues/6061

9. **#6060 — TypeError: content is not iterable when TUI footer renders tool-call-only messages** [CLOSED, 4 comments]  
   Uncaught crash in token estimation when assistant messages contain only tool calls. Highlights edge case in compaction logic.  
   https://github.com/earendil-works/pi/issues/6060

10. **#6073 — TUI viewport jumps when expanding tool output inside tmux** [CLOSED, 2 comments]  
    Destructive full redraw fallback in tmux environments causes visual jumps on expand/collapse. Related to #6050 fix area.  
    https://github.com/earendil-works/pi/issues/6073

---
## Key PR Progress

1. **#6087 — fix(coding-agent): remove hardcoded RPC wait timeout** [CLOSED]  
   Eliminates 60s hard limit on `RpcClient.waitForIdle()` that killed long-running MCP sessions. Adds configurable `waitTimeoutMs`. Critical for MCP extension users.  
   https://github.com/earendil-works/pi/pull/6087

2. **#6081 — feat: add #RRGGBBAA alpha support for theme colors** [CLOSED]  
   8-digit hex colors with alpha blending against terminal background. Enables semi-transparent overlays in custom TUI widgets.  
   https://github.com/earendil-works/pi/pull/6081

3. **#6084 — fix(tui): preserve custom widget render order on background tick refreshes** [CLOSED]  
   Fixes widget order jitter caused by `Map.delete(key)+set(key)` in extension timers. Ensures predictable Z-order for custom UI components.  
   https://github.com/earendil-works/pi/pull/6084

4. **#6078 — feat(coding-agent): add get_entries and get_tree RPC commands** [OPEN]  
   Two new read-only RPC commands for headless SDK integrations: `get_entries` (append-ordered session entries with cursor) and `get_tree` (entry tree with leafId).  
   https://github.com/earendil-works/pi/pull/6078

5. **#6074 — fix(coding-agent): avoid pre-prompt compaction continue** [OPEN]  
   Prevents unnecessary context compaction on pre-prompt continuation. Aims to reduce latency in long coding sessions.  
   https://github.com/earendil-works/pi/pull/6074

6. **#6064 — feat(experimental): pi orchestrator** [OPEN]  
   New `@earendil-works/pi-orchestrator` package — a local daemon managing Pi instances over IPC sockets. Allows programmatic lifecycle: start, list, kill, connect. Experimental.  
   https://github.com/earendil-works/pi/pull/6064

7. **#6063 — Extension stats** [CLOSED]  
   Addresses #6062: fixes OSC garbage printed on exit when `PI_STARTUP_BENCHMARK=1`. Important for extension developers debugging startup time.  
   https://github.com/earendil-works/pi/pull/6063

8. **#6067 — fix(prompt): add overeager scope-discipline rule to system prompt** [CLOSED]  
   One-line prompt change akin to aider's `overeager_prompt`: instructs the agent to stay within request scope and avoid modifying unrelated code.  
   https://github.com/earendil-works/pi/pull/6067

9. **#5832 — fix(ai): surface provider HTTP error body instead of opaque SDK message** [OPEN]  
   Proxy/gateway 403s currently show `Unknown: UnknownError`. This PR surfaces the real HTTP body to help users debug proxy auth issues.  
   https://github.com/earendil-works/pi/pull/5832

10. **#5270 — Ephemeral session model and thinking level selection** [CLOSED, inprogress]  
    Makes `setModel`/`cycleThinkingLevel` session-only by default; global defaults preserved unless `persist: true`. Prevents accidental overwrites of user config.  
    https://github.com/earendil-works/pi/pull/5270

---
## Feature Request Trends

- **Headless/CI integration**: Multiple requests for RPC session introspection (#6078, #5810), deterministic in-memory session IDs (#6070), and HITL tool-call interrupts (#5901). Community is building automation workflows around Pi's SDK.
- **Standalone binary packaging**: Users want Pi to ship as a single executable bundling its Node.js runtime (#6065), avoiding conflicts with project-specific Node versions. Deno/esbuild comparison cited.
- **Shell autocompletion**: Request for bash/zsh/fish completions for Pi CLI flags (`--provider`, `--tool`, etc.) rather than filesystem path completion (#6086).
- **Orchestration daemon**: The orchestrator PR (#6064) and the HITL interrupt proposal (#5901) both point toward multi-instance lifecycle management and human-in-the-loop approval workflows.
- **Provider feature parity**: Users want reasoning token counts exposed in `Usage` (#6057), `maxTokens` propogation fixed for non-OpenAI providers (#5595), and custom fetch support for proxy auth (#6034).

---
## Developer Pain Points

- **TUI scroll/viewport instability**: At least 4 issues in 24h (#6050, #5825, #6073, #6058) involve terminal scroll jumps or crashes on line overflow. The scrollback clearing bug (#6050) was the most disruptive, causing a full redraw that resets the terminal state mid-session.
- **Extension ecosystem fragility**: Compiled binary resolver fails on npm imports from subdirectories (#6085); a Pi update broke `pi-lovely-codex` (#5989); and an extension using `setEditorComponent` loses input history after `/resume` (#6066). Extension developers face compatibility breaks across releases.
- **Provider-specific silent failures**: OpenAI's reasoning state dropped on out-of-order streaming (#6009), MiniMax context window enforcement at lower-than-advertised limits (#6061), and `maxTokens` not forwarded to Together.ai/DeepSeek (#5595) — all examples of providers behaving differently than expected, with no clear error messages.
- **Session file safety**: `SessionManager.open()` silently truncates non-session files (#6002) — a destructive IO bug that destroyed a 3.2MB log file. The community reaction (4 comments, critical severity) suggests this erodes trust in file operations.
- **Global vs project config collision**: The `~/.pi` / `cwd/.pi` overlap (#5671, 👍5) is a longstanding design issue. While mitigated by `.pi/agent` subdirectory separation, the configuration surface remains confusing for users who develop from their home directory.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-26

## Today's Highlights
The community is buzzing with several critical Windows-specific bugs and a strong push for improved session management and memory features. A major PowerShell resource leak (Issue #5873) generated significant frustration, while feature requests for team-shared auto-memory and enhanced `/loop` behavior signal growing enterprise adoption. On the PR side, new contributions landed for voice dictation, live syntax highlighting in the web shell, and an extension creator skill.

## Releases
No new releases in the last 24 hours.

## Hot Issues (Top 10)

1. **[#5873 — Windows: PowerShell leak until OOM](https://github.com/QwenLM/qwen-code/issues/5873)**  
   *Status: OPEN, P1 priority*  
   **Why it matters:** Each tool call spawns a new PowerShell process that never closes, leading to memory exhaustion. Developer reaction is very frustrated, marking it as a critical regression on Windows. No workaround given yet.

2. **[#401 — Streaming setup timeout](https://github.com/QwenLM/qwen-code/issues/401)**  
   *Status: OPEN, P1 bug*  
   **Why it matters:** Affects users with large inputs or slow networks. The 6s default timeout is too tight for many real-world workflows. Community is requesting configurable timeout guidance.

3. **[#1897 — Chinese path spaces in tool calls](https://github.com/QwenLM/qwen-code/issues/1897)**  
   *Status: CLOSED*  
   **Why it matters:** LLM incorrectly inserts spaces into Chinese directory names (e.g., `DNF私服研究` → `DNF 私服研究`), breaking file system tools. This is a high-impact i18n bug that was eventually fixed.

4. **[#5867 — Team-level auto-memory](https://github.com/QwenLM/qwen-code/issues/5867)**  
   *Status: OPEN, P2 feature request*  
   **Why it matters:** Proposes a Git-shared "team" tier for auto-memory, enabling context sharing across developers on the same repo. Community is excited about collaborative capabilities.

5. **[#4534 — Global AGENTS.md support](https://github.com/QwenLM/qwen-code/issues/4534)**  
   *Status: CLOSED*  
   **Why it matters:** Developers running multiple agent CLIs wanted a single `~/.agents/AGENTS.md` file to avoid duplicate prompt engineering. This represents a step toward industry-wide standards.

6. **[#3025 — Adopt iflow CLI chat features](https://github.com/QwenLM/qwen-code/issues/3025)**  
   *Status: CLOSED*  
   **Why it matters:** Community requested `/chat` command for session browsing, saving, and deletion. Also flagged a bug with `/qc-helper` not auto-linking to official skills.

7. **[#5641 — Repeated shell tool results](https://github.com/QwenLM/qwen-code/issues/5641)**  
   *Status: CLOSED*  
   **Why it matters:** Deterministic OpenAI-compatible providers cause duplicate submission of completed tool results, leading to infinite loops. Community helped provide standalone reproducer.

8. **[#5861 — Context compression should stream](https://github.com/QwenLM/qwen-code/issues/5861)**  
   *Status: CLOSED, P1*  
   **Why it matters:** Non-streaming compression requests cause gateway timeouts in deployments with long conversations. Community flagged this as a performance bottleneck.

9. **[#5840 — VSCode extension internal connection error](https://github.com/QwenLM/qwen-code/issues/5840)**  
   *Status: CLOSED*  
   **Why it matters:** VSCode users hit a generic "Internal error: Connection error." No clear cause identified yet. Community is awaiting more information.

10. **[#2342 — `/undo` command](https://github.com/QwenLM/qwen-code/issues/2342)**  
    *Status: CLOSED*  
    **Why it matters:** Repeatedly requested as a basic safety net. Community sentiment: "how is it possible they didn't implement this?" Highlights a longstanding usability gap.

## Key PR Progress (Top 10)

1. **[#5666 — Design: Ctrl+O transcript view, removing compact mode](https://github.com/QwenLM/qwen-code/pull/5666)**  
   *Status: OPEN*  
   **What it does:** Proposes a new frozen transcript view (Ctrl+O) with a single concise baseline, removing the compact/detailed mode toggle. Follows design-first process.

2. **[#5828 — Bundled extension creator skill](https://github.com/QwenLM/qwen-code/pull/5828)**  
   *Status: OPEN*  
   **What it does:** Adds an `extension-creator` skill to guide agents through scaffolding, customizing, and testing Qwen Code extensions. Includes MCP server workflow.

3. **[#5629 — PreToolUse hook 'ask' as TUI confirmation](https://github.com/QwenLM/qwen-code/pull/5629)**  
   *Status: OPEN*  
   **What it does:** Converts `PreToolUse` hooks returning `"ask"` into native TUI confirmations instead of silently denying the tool call. Enhances safety for sensitive operations.

4. **[#5856 — Voice dictation in desktop app](https://github.com/QwenLM/qwen-code/pull/5856)**  
   *Status: OPEN*  
   **What it does:** Brings `/voice` dictation to the desktop app, matching CLI and Web Shell capabilities. Includes microphone button and recording bar UI.

5. **[#5869 — Live syntax highlighting for streaming code blocks](https://github.com/QwenLM/qwen-code/pull/5869)**  
   *Status: OPEN*  
   **What it does:** Implements real-time syntax highlighting while code blocks are still streaming, plus fixes fence-language alias resolution. Prevents flickering between plain and highlighted states.

6. **[#5780 — `qwen update` and `/update` commands](https://github.com/QwenLM/qwen-code/pull/5780)**  
   *Status: OPEN*  
   **What it does:** Adds automatic update checking and installation for standalone builds, with manual guidance for npm/yarn/pnpm users.

7. **[#5821 — Skip follow-up suggestions on local OpenAI backends](https://github.com/QwenLM/qwen-code/pull/5821)**  
   *Status: OPEN*  
   **What it does:** Defaults follow-up suggestions to off for loopback OpenAI-compatible servers, preventing unnecessary network calls.

8. **[#5829 — Reject unsafe source slugs before deletion](https://github.com/QwenLM/qwen-code/pull/5829)**  
   *Status: OPEN*  
   **What it does:** Prevents path-traversal attacks via source deletion by rejecting slug-like inputs (e.g., `../sessions`).

9. **[#5860 — Loosen autofix issue candidate filters](https://github.com/QwenLM/qwen-code/pull/5860)**  
   *Status: OPEN*  
   **What it does:** Fixes an autofix workflow that was finding zero candidates by relaxing the filter logic. Increases automated bug-fix coverage.

10. **[#5835 — Preserve model selection on provider reinstall](https://github.com/QwenLM/qwen-code/pull/5835)**  
    *Status: OPEN*  
    **What it does:** Ensures re-running provider setup doesn't reset the active model, fixing a common annoyance when re-authenticating or upgrading providers.

## Feature Request Trends

- **Collaborative Memory & Instructions (3 requests):** Team-shared auto-memory (#5867), global AGENTS.md (#4534), and multi-session management (#5855, #5863) show a clear push toward team-scale usage.
- **UI/UX Polish (4 requests):** Live syntax highlighting (#5866), collapsed session preview (#5759), default status line (#5789), and `/undo` (#2342) reflect demand for a more polished, professional CLI experience.
- **Session Management (3 requests):** Queryable session status (#5855, #5863), conversation persistence (#3025), and the `/update` command (#5780) indicate maturing operational needs.
- **Deployment & Integration (2 requests):** Daemon mode with HTTP endpoints and A2A server protocol (#951) suggest enterprise deployment scenarios.

## Developer Pain Points

- **Windows Instability:** The PowerShell leak issue (#5873) drew intense developer frustration, with explicit profanity in the report. Combined with the Chinese path bug (#1897) and VSCode connection errors (#5840), Windows users face significant reliability issues.
- **Streaming & Timeout Problems:** Multiple reports (#401, #5861) highlight that default streaming timeouts (6s) and non-streaming compression requests create real-world bottlenecks, especially with longer conversations.
- **Missing Basic UX:** The repeated demand for `/undo` (#2342) and `/clear` functionality (#1882) signals that developers consider these table-stakes features that are still absent.
- **Configuration Friction:** Users report issues with `.env` handling on first run (#948), multiple providers with the same model (#3555), and unclear auth reset logic (#3074).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-26

## Today's Highlights

The project has officially **rebranded to CodeWhale**, with the legacy `deepseek-tui` npm package deprecated and no longer receiving updates. Today saw a flurry of activity around **v0.8.66 Hotbar MVP** work, with 8+ PRs landed addressing the Hotbar dispatch, safety, and rendering pipeline. A critical bug fix landed for **plan/agent mode confusion** (Issue #3568), and the team shipped **auto-approval mode fixes** to restore YOLO mode behavior broken in recent releases.

---

## Releases

**v0.8.65** — released within the last 24h. This version introduces **CodeWhale** as the canonical project name, replaces the legacy `deepseek-tui` npm package, and includes a rebranding migration guide in `docs/REBRAND.md`. No feature changes are listed for this release; it is purely a naming and distribution transition.

---

## Hot Issues

1. **[#3568 — plan and agent mode mixed up YET AGAIN](https://github.com/Hmbown/CodeWhale/issues/3568)** (`OPEN`, [4 comments])
   A Chinese-language report with a detailed chat export showing that the AI assistant failed to respect plan/agent mode switching even in the latest version. The reporter includes specific evidence from thinking traces. 1 👍 signals that this is a widely felt regression.

2. **[#3205 — Fleet model classes, loadout auto, and semantic route roles](https://github.com/Hmbown/CodeWhale/issues/3205)** (`OPEN`, [10 comments])
   A deep architectural issue defining the Fleet compute loadout selector shared across TUI, CLI, exec, and subagents. The "Fleet loadout auto" mode is a key user-facing feature, and 10 comments suggest active technical debate on the design.

3. **[#3466 — Approval modal cancellation and review-required semantics](https://github.com/Hmbown/CodeWhale/issues/3466)** (`CLOSED`, [5 comments])
   A user complains that v0.8.64 asks for destructive approval on every action. They want the old no-confirmation workflow back. This issue's closure likely stems from the auto-approval fixes landed today (PR #3613).

4. **[#3541 — Rust-based native runtime/desktop client](https://github.com/Hmbown/CodeWhale/issues/3541)** (`OPEN`, [3 comments])
   A feature request for a Rust-native desktop client to reduce Node.js cold-start latency and memory overhead. 3 comments with no thumbs-up yet, but the discussion signals serious user interest in lower-level performance.

5. **[#3546 — Extend ACP support to expose provider and model selection](https://github.com/Hmbown/CodeWhale/issues/3546)** (`CLOSED`, [3 comments])
   A request from a Paseo integration user who needs CodeWhale's provider/model selection exposed through the ACP stdio adapter. Closed without detail on the resolution.

6. **[#2300 — Multi-model compatibility, provider docs, and automatic Fleet loadout](https://github.com/Hmbown/CodeWhale/issues/2300)** (`OPEN`, [7 comments])
   A longstanding (since May 28) umbrella issue for docs explaining provider/routing differences (vllm vs. openai). 7 comments suggest ongoing confusion about multi-provider configuration.

7. **[#3606 — Agent asks for confirmation in YOLO mode](https://github.com/Hmbown/CodeWhale/issues/3606)** (`CLOSED`, [1 comment])
   Another YOLO mode regression: after upgrade, the agent requires permission even in a mode explicitly designed to be permissionless. Fixed by today's PR #3613.

8. **[#1846 — Proposed changes can't be seen before approving](https://github.com/Hmbown/CodeWhale/issues/1846)** (`CLOSED`, [1 comment, 1 👍])
   Long-standing UX grievance: the approval modal obscures proposed diffs. Closed today by PR #3619 which adds expandable change previews to approval cards.

9. **[#3545 — Custom context window size per provider](https://github.com/Hmbown/CodeWhale/issues/3545)** (`CLOSED`, [1 comment])
   A Chinese user requests the ability to override the 128k default context window for providers with 1M context models (Alibaba Bailian / Qwen). Closed without visible resolution — a potential gap for power users.

10. **[#2959 — Reduce user-visible agent chatter and verbose transcript text](https://github.com/Hmbown/CodeWhale/issues/2959)** (`CLOSED`, [2 comments])
    An ongoing effort to reduce noise in agent transcripts. Closed today — likely related to the prompt audit work in PR #3609.

---

## Key PR Progress

1. **[PR #3623 — fix(tui): surface mode policy in turn metadata](https://github.com/Hmbown/CodeWhale/pull/3623)** (`OPEN`)
   Adds active mode and policy delta to each user turn's metadata block, specifically targeting the plan/agent mode confusion issue (#3568). Reuses existing prompt snippets instead of duplicating policy copy.

2. **[PR #3617 — test(tui): add token cache report fixtures](https://github.com/Hmbown/CodeWhale/pull/3617)** (`OPEN`)
   Adds cache hit-ratio fixtures derived from real user reports (issues #1177, #1747). Enables regression testing for token cache telemetry without requiring live API calls.

3. **[PR #3624 — Codex/lsp php custom servers](https://github.com/Hmbown/CodeWhale/pull/3624)** (`OPEN`)
   Adds PHP (intelephense) to the built-in LSP registry and introduces a `[lsp.custom]` config section for registering arbitrary language servers by file extension. Covers Ruby, C#, Swift, Lua, Kotlin, etc. — a significant expansion for polyglot developers.

4. **[PR #3621 — Fix provider links docs fallback](https://github.com/Hmbown/CodeWhale/pull/3621)** (`OPEN`)
   Updates stale docs URLs and adds Qianfan-specific links. The install.sh endpoint was serving HTML instead of a script (Issue #3582), suggesting documentation infrastructure issues.

5. **[PR #3619 — fix(tui): show proposed file changes in approvals](https://github.com/Hmbown/CodeWhale/pull/3619)** (`CLOSED`)
   **Closes #1846** with bounded change previews inside expanded approval cards for write_file, edit_file, and apply_patch. Keeps compact cards focused on controls. Includes Chinese-locale support for preview sublabels.

6. **[PR #3616 — fix(tui): surface resource usage in turn metadata](https://github.com/Hmbown/CodeWhale/pull/3616)** (`CLOSED`)
   **Closes #2666** — agents now see context pressure, session token totals, cache totals, and active goal resource usage in each `<turn_meta>` block. Critical for long-running multi-agent tasks.

7. **[PR #3615 — fix(tui): harden session diagnostics classifier](https://github.com/Hmbown/CodeWhale/pull/3615)** (`CLOSED`)
   Hardens the diagnostics classifier for issue #2022 to avoid generic `id`/`name` field replacements and empty sentinels. Keeps authentication failures classified as model-quality issues.

8. **[PR #3613 — fix(tui): honor auto approval mode in dispatch](https://github.com/Hmbown/CodeWhale/pull/3613)** (`CLOSED`)
   **Closes #3606** — routes normal user turns and bang-shell commands through `auto_approve` when live approval mode is AUTO, not only when the mode label is YOLO. Directly addresses the YOLO regression reports.

9. **[PR #3612 — fix(tui): gate unsafe hotbar dispatch paths](https://github.com/Hmbown/CodeWhale/pull/3612)** (`CLOSED`)
   Core Hotbar safety: adds explicit source safety modes (direct-fire, composer-prefill, disabled, approval-gated). Blocks MCP/skill/plugin sources from registering bindable actions before their safety path is wired.

10. **[PR #3607 — chore: reactivate stale issue cleanup](https://github.com/Hmbown/CodeWhale/pull/3607)** (`OPEN`)
    Creates missing GitHub stale-policy labels (`needs-info`, `stale`, `keep-open`, `pinned`) and lets `bug` + `needs-info` issues age out unless marked as release-blockers or security. Suggests the maintainer is actively managing issue debt.

---

## Feature Request Trends

1. **Rust-native runtime** — multiple users requesting a desktop client built in Rust (Issue #3541) for lower latency and smaller memory footprint compared to the Node.js/TypeScript TUI.

2. **Customizable provider context windows** — power users want to override the default 128k context limit per provider (Issue #3545), especially for Chinese cloud models (Qwen, Ali Bailian) that support 1M tokens.

3. **Multi-provider docs and Fleet loadout** — persistent confusion about `provider = vllm` vs `provider = openai` semantics, compounded by the new Fleet automatic loadout feature needing clearer documentation (Issue #2300).

4. **ACP provider exposure** — integration users want CodeWhale's provider and model selection exposed through the Agent Communication Protocol adapter (Issue #3546), allowing tools like Paseo to mirror exact model choices.

5. **Hotbar action expansion** — the Hotbar MVP landed with built-in app actions and slash commands, but the umbrella issue (#3389) explicitly defers MCP tools, skills, and plugin sources to future milestones.

---

## Developer Pain Points

1. **Mode confusion persists** — Issue #3568 and its predecessor reports show that plan/agent mode switching remains unreliable for the LLM to respect. The community is frustrated with repeated regressions despite explicit thinking traces proving the misbehavior.

2. **YOLO mode broken in recent releases** — Two separate reports (Issues #3606, #3466) confirm that the "no confirmation needed" mode is broken in v0.8.64/v0.8.65. The auto-approval fix landed today (PR #3613), but the back-to-back regressions erode trust.

3. **Windows environment variable issues** — Issue #3572 reports that user-level environment variables (set via System Properties) are not inherited by CodeWhale's shell executor. This impacts Windows dev workflows with build tools.

4. **Installation documentation wrong** — Issue #3582 reports that `curl -fsSL https://codewhale.net/install.sh` returns an HTML page instead of a shell script. Combined with the rebranding, this makes first-time installation confusing.

5. **Proposed diffs invisible during approvals** — Issue #1846 (now closed by PR #3619) had been open since May 20, indicating that this UX blind spot was a long-standing pain point before today's fix.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*