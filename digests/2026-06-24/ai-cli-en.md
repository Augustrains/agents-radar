# AI CLI Tools Community Digest 2026-06-24

> Generated: 2026-06-24 01:58 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem: Cross-Tool Comparison Report
**Date:** 2026-06-24 | **Prepared for:** Technical Decision-Makers & Developers

---

## 1. Ecosystem Overview

The AI CLI tools landscape on June 24, 2026 shows a mature but rapidly evolving ecosystem with **six active competing tools**, each carving distinct positions between enterprise reliability, developer autonomy, and platform integration. The day's data reveals **Claude Code and Gemini CLI** leading in community engagement and architectural ambition, while **OpenAI Codex** battles critical cost-regression issues that have eroded user trust. A notable **validation-gap crisis** emerged across Qwen Code (20+ bugs in a single day) and Pi (3 concurrent provider regressions in one minor release), suggesting the ecosystem's quality assurance practices are straining under rapid iteration. **Kimi Code and DeepSeek TUI (CodeWhale)** represent the long tail—quiet consolidation versus aggressive architectural overhaul. The dominant cross-cutting theme is the tension between **autonomous agent ambition** and **reliability safety nets**, with every community demanding better sandboxing, credential protection, and failure transparency.

---

## 2. Activity Comparison

| Tool | Issues Updated (24h) | PRs Active (24h) | Release Status | Notable Signal |
|------|---------------------|------------------|----------------|----------------|
| **Claude Code** | 10 hot issues | 1 PR (stale, 5mo) | **v2.1.187** shipped today | Sandbox credentials + org model restrictions |
| **OpenAI Codex** | 10 hot issues | 10 PRs active | 6 alpha Rust releases | Rate-limit cost regression (#28879) dominates |
| **Gemini CLI** | 10 hot issues | 10 PRs active | No release today | OAuth fix + SSRF protection PRs |
| **GitHub Copilot CLI** | 10 new triage issues | 1 PR (minor) | **v1.0.64** yesterday | Path access transparency + PAYG budget display |
| **Kimi Code** | 1 issue updated | 0 PRs | v0.12.0 (stale) | Lowest activity in ecosystem |
| **OpenCode** | 10 hot issues | 10 PRs active | No release today | Desktop UX polish wave; WSL regression |
| **Pi** | 10 hot issues | 10 PRs active | **v0.80.0/1/2** today | 3 provider regressions in one minor release |
| **Qwen Code** | 10 hot issues | 10 PRs active | **v0.19.0/1** today | 20+ validation bugs from single contributor |
| **DeepSeek TUI** | 10 hot issues | 10 PRs active | No release today | Heavy Fleet architecture PRs; "turn stalled" persists |

**Key observations:**
- **Gemini CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI** all show 10+ active PRs—indicating high development velocity.
- **Kimi Code** is notably quiet with zero PRs and one stale issue, suggesting stalled or consolidating development.
- **Claude Code** has the most active issue tracker but negligible PR activity, possibly indicating a maintainer-bottleneck or PR review queue.

---

## 3. Shared Feature Directions

The following requirements appear across **3+ tool communities**, indicating strong market demand:

| Requirement | Tools Requesting | Specific Manifestation |
|------------|-----------------|----------------------|
| **Agent Self-Awareness & Telemetry** | Claude Code, Gemini CLI, DeepSeek TUI, Pi | Token/resource visibility, sub-agent status, context pressure readouts, cost transparency |
| **MCP/Plugin Ecosystem Stability** | All 9 tools | Connection drops, duplicate instances, startup latency, lifecycle bugs, schema mismatches |
| **Sandboxed Credential Management** | Claude Code, OpenAI Codex, Gemini CLI, Qwen Code | Credential brokers, secret redaction, URL/path blocklists, case-insensitive blocking |
| **Multi-Provider / Model Routing** | DeepSeek TUI, Qwen Code, Pi, OpenAI Codex | Provider-agnostic routing, fallback chains, live model catalogs, atomic route switching |
| **Autonomous Mode Safety Rails** | DeepSeek TUI, Kimi Code, Claude Code, GitHub Copilot | Review gates, yolo-mode contract enforcement, pre-push policies, user-defined guardrails |
| **Desktop/CLI Session Continuity** | Claude Code, OpenCode, Gemini CLI, DeepSeek TUI | Cross-session memory, persistent history across moves, session export/restore |
| **Cross-Platform Terminal Compatibility** | GitHub Copilot, OpenCode, DeepSeek TUI, Qwen Code | Windows rendering (scroll bars, contrast), Wayland, Alacritty, WSL path handling |
| **Accessibility & Internationalization** | Claude Code, OpenCode, Qwen Code, GitHub Copilot | Screen-reader support, Arabic RTL, contrast fixes, theming improvements |

**Most demanded single feature (cross-tool):** **Token/resource cost visibility** — users across Claude Code (#65500), OpenAI Codex (#28879), DeepSeek TUI (#2666), and Pi (context estimates) all demand real-time budget tracking to prevent runaway costs.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|------------|-------------|------------|----------------|-----------|----------|-----|-----------|--------------|
| **Primary Focus** | Enterprise governance | Cost + model availability | Agent orchestration | GitHub integration | Minimalist autonomy | Desktop + TUI hybrid | Multi-provider extensibility | Daemon-based architecture | Fleet/multi-agent routing |
| **Target User** | Enterprise teams | ChatGPT Plus users | Research/experimental | GitHub ecosystem | Solo developers | Full-stack devs | Provider-agnostic power users | Qwen/Local LLM users | Chinese & global devs |
| **Unique Strength** | Sandbox credentials | Rust performance | AST-aware tools | WSL/VS Code deep integration | Yolo simplicity | Tab-based UX polish | Provider normalization | Validation sweep (20+ bugs) | Fleet worker execution |
| **Weakness** | Android/Termux broken iOS crash cluster | Cost regression 10-20x | Subagent false success | Windows rendering | Zero PR activity | Silent Write failure | 3 provider regressions | Configuration fragmentation | "Turn stalled" freeze |
| **Release Velocity** | Moderate | High (alpha Rust) | Moderate | Low (stable) | Very Low | Moderate | High | High | Very High |
| **Community Size** | Largest (59 comments/issue) | High (257 👍/issue) | Medium | Medium | Very Small | Medium | Medium | Growing | Small but active |

**Strategic observations:**
- **Claude Code** is leaning hard into enterprise compliance (org model restrictions, sandbox credentials) while suffering critical iOS/mobile gaps.
- **OpenAI Codex** is caught between shipping Rust alpha releases and a cost-regression crisis that undermines its core value proposition.
- **Gemini CLI** differentiates with AST-aware code intelligence and SSRF protection—security-first approach.
- **DeepSeek TUI** is the most architecturally ambitious, rebuilding around Fleet/multi-agent routing in a single version push.
- **Kimi Code** is dangerously quiet—0 PRs, 1 stale bug, no releases—risking irrelevance.

---

## 5. Community Momentum & Maturity

### Highest Momentum (Rapidly Iterating)
- **DeepSeek TUI (CodeWhale):** 10+ PRs/day, architectural rewrite (Fleet), fastest bug-to-fix turnaround (24h for contrast bug). High velocity but reliability suffers ("turn stalled" open 3 weeks).
- **Qwen Code:** 4 releases + 10 PRs in 24h + validation sweep. Aggressive quality push but fragmentation between CLI/ACP/VSCode.
- **Pi:** Triple release day (v0.80.0/1/2) shows rapid patch cycles, but 3 regressions in one minor release signals QA gaps.
- **OpenAI Codex:** 6 Rust alpha releases + 10 PRs. High engineering output but cost regression (#28879) is dampening community goodwill.

### Established & Stable
- **Claude Code:** Largest community, most mature feature set, but PR pipeline is virtually stalled (1 PR, 5mo stale). Enterprise features shipping but critical bugs unaddressed (Android #50270, iOS crash cluster).
- **GitHub Copilot CLI:** Stable release cadence, focused improvements (path transparency, PAYG budget). Smallest PR pipeline but high-quality triage process (10 new issues today).

### At Risk
- **Kimi Code:** 0 PRs, 1 issue, stale release (v0.12.0). No community engagement. Unclear if project is maintained.
- **OpenCode:** Moderate activity but key bugs (Write tool silent failure, WSL path mangling) persist across releases. Desktop focus may be dividing TUI/CLI resources.

### Community Sentiment Summary
- **Most frustrated:** OpenAI Codex users (cost 10-20x, model 404 errors)
- **Most engaged:** DeepSeek TUI (architectural discussion) and Qwen Code (validation contributor @tt-a1i)
- **Most enterprise-focused:** Claude Code (org policies, credential protection)
- **Most underserved:** Android/Termux users (Claude Code #50270, 51 upvotes, 60+ days unfixed)

---

## 6. Trend Signals

### 1. **The Cost-Transparency Mandate**
OpenAI Codex's #28879 (257 👍) and Claude Code's #65500 (3.5M token waste) signal a **non-negotiable user demand for itemized cost tracking**. Tools that don't expose per-call token consumption will face backlash as budgets tighten. **Signal:** Expect all tools to ship budget dashboards within 2 quarters.

### 2. **Agent Orchestration Hits a Reliability Wall**
The cluster of "false success" bugs (Gemini CLI #22323, DeepSeek TUI #3275, Claude Code #65500) shows that **current sub-agent architectures lack failure transparency**. Subagents reporting `GOAL` when hitting turn limits or burning tokens with zero output erodes trust in autonomous workflows. **Signal:** Expect a wave of "agent telemetry" features—subagent status, context pressure, elapsed time visible in TUI.

### 3. **Platform Fragmentation Is the New Vendor Lock-In**
Every tool has platform-specific regressions: Claude Code (Android/Termux, iOS), GitHub Copilot (WSL, Windows scroll), Gemini CLI (Wayland), OpenCode (macOS lock screen). **No tool is cross-platform reliable.** This creates switching costs and forces developers to evaluate based on their primary OS. **Signal:** Cross-platform testing will become a competitive differentiator; tools that ship Linux/macOS/Windows simultaneously will win.

### 4. **Validation Is the Weakest Link**
Qwen Code's 20+ bugs from a single contributor expose that **even mature codebases lack systematic input validation** (fractional values, NaN, negative cursors, type mismatches in JSON schemas). This pattern likely exists in all tools—most just haven't been audited yet. **Signal:** Expect a "validation sweep" wave across the ecosystem as tools copy Qwen's pattern.

### 5. **MCP Server Lifecycle Is an Urgent Reliability Gap**
Duplicate MCP processes (DeepSeek TUI #3461), HTTPS CONNECT tunneling failures (Claude Code #11791), startup latency (OpenAI Codex #28630), and Cloudflare blocks (OpenAI Codex #29197) all point to **MCP being the ecosystem's most fragile integration point**. **Signal:** Tool maintainers should prioritize MCP connection monitoring, graceful degradation, and error surfacing.

### 6. **Desktop Supremacy vs. CLI Purity**
OpenCode's 10 PRs for desktop tab improvements and DeepSeek TUI's Fleet TUI view contrast sharply with Kimi Code's bare CLI. The market is **voting for richer desktop UIs** (tabs, live model picks, agent status views) over pure terminal experiences. **Signal:** Pure-CLI tools without some visual layer will struggle to retain power users.

### 7. **The Chinese Model Ecosystem Is Maturing**
DeepSeek TUI (#3439, GLM-5.2 integration) and Qwen Code (growing Chinese community) show that **Chinese LLM providers are building dedicated CLI tooling**, not just APIs. This will accelerate localization and domestic model support. **Signal:** Global tools should plan for Multi-provider routing that includes Chinese endpoints natively.

### Reference Value for Developers

| If you care about... | Consider... |
|---------------------|-------------|
| **Enterprise governance** | Claude Code (org restrictions, sandbox credentials) |
| **Cost control** | None are mature—watch OpenAI Codex resolution of #28879 |
| **Multi-provider flexibility** | Pi or DeepSeek TUI (but brace for regressions) |
| **GitHub integration** | GitHub Copilot CLI (WSL, VS Code) |
| **Agent orchestration research** | Gemini CLI (AST-aware) or DeepSeek TUI (Fleet) |
| **Cross-platform reliability** | None—evaluate per-OS |
| **Active development / community** | Qwen Code or DeepSeek TUI |
| **Stability over features** | Claude Code (despite Android/iOS issues) |

**Bottom line for decision-makers:** The AI CLI ecosystem is in a **quality vs. velocity tension**—every tool is shipping fast, but every tool has at least one critical reliability gap. Budget for evaluation time, plan for regressions, and maintain fallback tool options. The winning tool will be the one that solves **trust** (cost transparency + agent telemetry + platform reliability) before the next feature.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Date**: 2026-06-24 | **Source**: [github.com/anthropics/skills](https://github.com/anthropics/skills)

---

## 1. Top Skills Ranking

The following Pull Requests have generated the most community discussion, indicating strong interest and active review.

### 🥇 #1298 — `fix(skill-creator): run_eval.py always reports 0% recall`
**Functionality**: Fixes the core evaluation script used by the skill-creation optimization loop. Without this fix, the description-optimization process (`run_loop.py`, `improve_description.py`) optimizes against noise—every skill description scores `recall=0%`, making the entire feedback loop useless.
**Status**: ⏳ **Open** (Created 2026-06-10, last updated 2026-06-23)
**Discussion Highlights**: Addresses Issue #556 (see below) with 10+ independent reproductions. The fix installs the eval artifact as a real skill, corrects Windows stream reading, trigger detection, and parallel worker logic.
**👁️ Attention**: Highest comment count in the repository
[→ PR #1298](https://github.com/anthropics/skills/pull/1298)

### 🥈 #514 — `Add document-typography skill`
**Functionality**: A skill for typographic quality control in Claude-generated documents. Prevents orphan word wrap (1-6 words on a new line), widow paragraphs (headers stranded at page bottom), and numbering misalignment—issues endemic to AI-generated documents.
**Status**: ⏳ **Open** (Created 2026-03-04, last updated 2026-03-13)
**Discussion Highlights**: The author notes these issues "affect every document Claude generates" and that "users rarely ask for good typography"—making this a silent quality-of-life improvement.
[→ PR #514](https://github.com/anthropics/skills/pull/514)

### 🥉 #538 — `fix(pdf): correct case-sensitive file references`
**Functionality**: Fixes 8 case-sensitivity mismatches in the PDF skill's `SKILL.md`, where file references used uppercase (`REFERENCE.md`, `FORMS.md`) but actual files are lowercase (`reference.md`, `forms.md`). This breaks on case-sensitive file systems (Linux, macOS).
**Status**: ⏳ **Open** (Created 2026-03-06, last updated 2026-04-29)
**Discussion Highlights**: Highlights the cross-platform compatibility challenge in the skills ecosystem.
[→ PR #538](https://github.com/anthropics/skills/pull/538)

### #486 — `Add ODT skill — OpenDocument text creation`
**Functionality**: Enables Claude to create, fill, read, and convert OpenDocument Format files (.odt, .ods). Triggered by mentions of ODT, ODS, ODF, OpenDocument, or LibreOffice. Covers document creation, template filling, and ODT-to-HTML conversion.
**Status**: ⏳ **Open** (Created 2026-03-01, last updated 2026-04-14)
**Discussion Highlights**: Addresses demand for open-source document format support, complementing the existing DOCX and PDF skills.
[→ PR #486](https://github.com/anthropics/skills/pull/486)

### #210 — `Improve frontend-design skill clarity`
**Functionality**: Revises the frontend-design skill for better clarity, actionability, and internal coherence. Ensures every instruction is actionable within a single conversation with specific enough guidance to steer behavior.
**Status**: ⏳ **Open** (Created 2026-01-05, last updated 2026-03-07)
**Discussion Highlights**: Represents the community's desire for higher-quality, more actionable skill instructions rather than verbose explanations.
[→ PR #210](https://github.com/anthropics/skills/pull/210)

### #83 — `Add skill-quality-analyzer and skill-security-analyzer`
**Functionality**: Two "meta skills" for evaluating other Claude Skills: a quality analyzer (evaluating structure, documentation, examples, resource references, trigger precision, security, token efficiency) and a security analyzer (scanning for code injection, prompt injection, data exfiltration risks).
**Status**: ⏳ **Open** (Created 2025-11-06, last updated 2026-01-07)
**Discussion Highlights**: Represents the ecosystem maturing—the community is now building tools to assess the quality and security of skills themselves.
[→ PR #83](https://github.com/anthropics/skills/pull/83)

### #1323 — `fix(skill-creator): trigger detection misses real skill name`
**Functionality**: Fixes a bug where `run_eval.py::run_single_query` fails to detect that a skill triggered, causing the optimization loop to report `recall=0%` for all should-trigger queries. Related to #1298 but identifies a separate root cause.
**Status**: ⏳ **Open** (Created 2026-06-16, last updated 2026-06-23)
**Discussion Highlights**: The second major effort in a month to fix the broken evaluation pipeline—indicating this is the community's top pain point.
[→ PR #1323](https://github.com/anthropics/skills/pull/1323)

---

## 2. Community Demand Trends

Analysis of the most-discussed Issues reveals five dominant request themes:

### 🏆 Most Critical: **Skill-Creator Evaluation Pipeline Reliability**
- **[#556](https://github.com/anthropics/skills/issues/556)**: `run_eval.py` yields 0% trigger rate across all queries (12 comments, 7 👍)
- **[#1169](https://github.com/anthropics/skills/issues/1169)**: `recall=0%` on every iteration of the optimization loop (3 comments, 1 👍)
- **[#1061](https://github.com/anthropics/skills/issues/1061)**: Windows compatibility: subprocess, encoding, pipe failures (3 comments, 1 👍)

**Insight**: The evaluation and optimization tooling is currently broken—this is the single biggest blocker for skill creators. Without a working `run_eval.py`, the entire skill development workflow is non-functional.

### 📊 Data: **Enterprise Document & Office Format Support**
- [#486] ODT/ODS/LibreOffice support (new skill, high discussion)
- [#514] Document typography quality control
- [#1175] SharePoint Online (SPO) document handling via skills

**Insight**: The community wants Claude to be a capable office document assistant across the full format ecosystem (Microsoft Office, OpenDocument, PDF with proper typography).

### 🔒 Security: **Trust Boundary & Governance**
- **[#492](https://github.com/anthropics/skills/issues/492)**: Community skills under `anthropic/` namespace impersonate official skills (9 comments, 2 👍)
- **[#1175](https://github.com/anthropics/skills/issues/1175)**: Security concerns with SPO access control logic in SKILL.md (4 comments)
- [#412] Agent governance patterns: policy enforcement, threat detection

**Insight**: As the skills ecosystem grows, users are increasingly concerned about trust, permissions, and governance—both for official vs. community skills and for skills that access sensitive systems.

### 🪟 Platform: **Cross-Platform Reliability (Especially Windows)**
- **[#1061](https://github.com/anthropics/skills/issues/1061)**: Three Unix-first assumptions break skill-creator on Windows
- [#1099], [#1050], [#1298]: Multiple PRs addressing Windows pipe, encoding, and subprocess issues

**Insight**: The skills tooling was built for macOS/Linux first. With growing Windows adoption, the community is investing heavily in compatibility fixes.

### 🧠 Memory & Context: **Persistent Agent State**
- [#154] `shodh-memory` skill: persistent context across conversations
- **[#1329](https://github.com/anthropics/skills/issues/1329)**: `compact-memory` with symbolic notation (new proposal)

**Insight**: Developers want skills that help Claude maintain long-running context efficiently, suggesting a need for standardized memory management patterns.

---

## 3. High-Potential Pending Skills

These PRs are actively under discussion and likely to land soon:

| PR | Skill | Potential Impact |
|---|---|---|
| [#514](https://github.com/anthropics/skills/pull/514) | **Document Typography** | Immediate quality improvement for all doc generation |
| [#486](https://github.com/anthropics/skills/pull/486) | **ODT/OpenDocument** | Fills critical gap in office format support |
| [#723](https://github.com/anthropics/skills/pull/723) | **Testing Patterns** | Comprehensive guide: unit, React, integration, E2E |
| [#360](https://github.com/anthropics/skills/pull/360) | **AppDeploy** | Deploy full-stack web apps directly from Claude |
| [#147](https://github.com/anthropics/skills/pull/147) | **Codebase Inventory Audit** | Orphaned code, doc gaps, infrastructure bloat detection |
| [#154](https://github.com/anthropics/skills/pull/154) | **Shodh Memory** | Persistent context across conversations |
| [#181](https://github.com/anthropics/skills/pull/181) | **SAP-RPT-1 OSS Predictor** | Enterprise tabular prediction via SAP's open model |

**Probability of Landing (this quarter)**: Document Typography (#514) and Testing Patterns (#723) have the cleanest scope and least controversy. The ODT skill (#486) and Shodh Memory (#154) fill clear gaps but may require more review.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is fixing the skill-creation evaluation pipeline**—because *that's broken, and nothing else works until it's fixed.*

This single bottleneck (#1298, #1323, #556, #1169) has absorbed more community attention than any new skill feature. Once resolved, the community is poised to deliver document format expansion (ODT, typography), cross-platform support (Windows), security governance, and persistent memory capabilities—the ecosystem is healthy and waiting for its core tooling to be reliable.

---

# Claude Code Community Digest — 2026-06-24

## Today's Highlights
Anthropic shipped **v2.1.187** with new `sandbox.credentials` setting for credential protection and org-level model restrictions. A **critical iOS crash cluster** is dominating the issue tracker, with multiple reports of instant crashes when opening Remote Control sessions. Meanwhile, **Termux/Android users remain broken** since v2.1.113 — the issue (#50270) now has 59 comments and 51 upvotes with no fix in sight.

---

## Releases
**v2.1.187** was released in the last 24 hours. Changes:
- **`sandbox.credentials`** — New setting to block sandboxed commands from reading credential files and secret environment variables
- **Org-configured model restrictions** — Enforced through the model picker, `--model` flag, `/model` command, and `ANTHROPIC_MODEL` environment variable; displays "restricted by your organization's set" for blocked models

---

## Hot Issues (10 Most Noteworthy)

### 1. [#50270] Android/Termux Broken Since v2.1.113
- **Tags:** bug, has repro, platform:android, regression, area:packaging
- **Summary:** The switch from a JS entry point to a native glibc Linux binary completely breaks Claude Code on Termux (Android). `process.platform` reports `android`, not `linux`, and Android's kernel rejects the binary.
- **Why it matters:** 59 comments, 51 upvotes — this is the top-voted open issue. Android/Chromebook developers are locked out with no workaround.
- **Link:** https://github.com/anthropics/claude-code/issues/50270

### 2. [#27492] Claude Cowork MCP Issues Persist
- **Tags:** bug, area:agents
- **Summary:** Long-running issue (since February 2026) where the Cowork MCP integration has unresolved bugs affecting collaboration workflows.
- **Why it matters:** 25 comments, 22 upvotes. This has been open for 4+ months, suggesting a systemic issue in the Cowork/MCP integration rather than a simple fix.
- **Link:** https://github.com/anthropics/claude-code/issues/27492

### 3. [#70165] iOS Remote Control Hard Crash – Swift KeyPath Stack Overflow
- **Tags:** bug, platform:ios, regression
- **Summary:** iOS app 1.260618.0 hard-crashes with a main-thread stack overflow in Swift KeyPath metadata when opening a Remote Control session.
- **Why it matters:** This is part of a crash cluster (#70262, #70288, #70382, #70359 all report identical symptoms). A Swift runtime-level bug is very concerning.
- **Link:** https://github.com/anthropics/claude-code/issues/70165

### 4. [#65500] Deep-Research Workflow Aborts on Schema Failure – Burns Millions of Tokens
- **Tags:** bug, platform:macos, area:cost, area:agents, area:skills
- **Summary:** The deep-research skill consistently fails in the Verify phase when any subagent fails to emit `StructuredOutput`, consuming ~3.5M tokens across three attempts with zero usable output.
- **Why it matters:** Token waste at this scale is a cost liability. Users are paying for failed runs with no recovery mechanism.
- **Link:** https://github.com/anthropics/claude-code/issues/65500

### 5. [#14375] Mermaid Rendering Support (Feature Request)
- **Tags:** enhancement
- **Summary:** Request for native Mermaid diagram/chart rendering in Claude Code output.
- **Why it matters:** 38 upvotes — the highest-voted feature request. Developers commonly use Mermaid for architecture diagrams, flowcharts, and sequence diagrams in documentation.
- **Link:** https://github.com/anthropics/claude-code/issues/14375

### 6. [#11791] Browser Automation Incompatible with Web Sandbox Proxy
- **Tags:** DOCS/BUG
- **Summary:** Playwright, Puppeteer, and Selenium cannot run in the Claude Code web sandbox because the security proxy doesn't support HTTPS CONNECT tunneling.
- **Why it matters:** 14 upvotes. This is an architectural limitation, not a bug — but users keep hitting it. Better documentation is the minimum ask.
- **Link:** https://github.com/anthropics/claude-code/issues/11791

### 7. [#70465] SessionEnd Hook Killed Before Completion
- **Tags:** bug, platform:windows, area:tui, area:hooks
- **Summary:** Long-running `SessionEnd` hooks are forcibly terminated on exit (`Ctrl+D` / `/exit`), preventing `EXIT` trap handlers from running and leaving partial state behind.
- **Why it matters:** Data integrity issue — users relying on cleanup hooks (temp files, state saves) get inconsistent results.
- **Link:** https://github.com/anthropics/claude-code/issues/70465

### 8. [#70483] Background-Task stdout Leaks into Foreground Bash Output
- **Tags:** bug, platform:macos, area:bash, area:agents
- **Summary:** In Claude Desktop (macOS), background tasks' stdout leaks into foreground Bash tool output via a shared controlling PTY, corrupting command results.
- **Why it matters:** PTY multiplexing issue is a fundamental terminal architecture bug. Could cause subtle automation failures.
- **Link:** https://github.com/anthropics/claude-code/issues/70483

### 9. [#70474] CCR Routine Sessions Can't Reach GitHub
- **Tags:** bug, platform:web, area:networking, area:sandbox, area:routines
- **Summary:** Claude Code Remote routine sessions have outbound traffic routed through a broken internal proxy, blocking GitHub access.
- **Why it matters:** GitHub is the primary origin for most developer workflows. This effectively breaks routine automations that need to clone repos or fetch packages.
- **Link:** https://github.com/anthropics/claude-code/issues/70474

### 10. [#43255] Chrome MCP Tools: "Navigation to this domain is not allowed"
- **Tags:** bug, has repro, platform:macos, regression, area:chrome
- **Summary:** Claude's Chrome MCP tools block navigation to all domains with the error "Navigation to this domain is not allowed" since v1.0.66.
- **Why it matters:** 16 comments, 8 upvotes. If Chrome MCP can't navigate, the entire browser automation use case is dead.
- **Link:** https://github.com/anthropics/claude-code/issues/43255

---

## Key PR Progress

**Only 1 PR was updated in the last 24 hours:**

### [#20448] Web4 Governance Plugin
- **Status:** OPEN (since 2026-01-23)
- **Summary:** Adds a `web4-governance` plugin for AI governance with trust tensors, entity witnessing, and R6 audit trails. Positioned as "trust-native internet infrastructure" for the AI agent era.
- **Why it matters:** This is the *only* PR active right now, and it has been open for 5 months with no comments. The lack of community engagement suggests either niche appeal or governance concerns about the approach.
- **Link:** https://github.com/anthropics/claude-code/pull/20448

---

## Feature Request Trends

### Highest Demand Features
1. **Mermaid Rendering** (#14375, 38 👍) — Native diagram rendering is the most-requested feature. Developers want to see architecture diagrams, flowcharts, and sequence charts inline.
2. **Async/Event-Driven Agent Communication** (#55981, 0 👍 but ongoing discussion) — Request for first-class async communication between Claude Code agents, enabling event-driven workflows rather than synchronous blocking calls.
3. **Accessibility Improvements** (#70425, new) — A blind accessibility architect is calling for audio cues, heading discipline, and humanized announcements for screen-reader users. This is Claude Code's first serious accessibility feature request.
4. **Custom Display Names/Aliases** (#70478, closed immediately) — Users want to rename sessions or agents with custom aliases. The speed of closure may indicate a known limitation.
5. **Persistent Session History Across Moves** (#70470, new) — When a project directory is moved, session history is lost. Users want path-independent session tracking.

### Policy & Configuration Requests
- **Org model restrictions** (now shipped in v2.1.187) — Organizations wanted to enforce model usage policies
- **SessionEnd hook grace period** (implied by #70465) — Users want configurable timeout before hooks are killed on exit

---

## Developer Pain Points

### Critical: iOS Remote Control Crash Cluster
Four separate issues (#70165, #70262, #70288, #70382, #70359) report identical symptoms: the iOS app crashes instantly when tapping into a Remote Control session. The root cause appears to be a Swift KeyPath stack overflow (#70165) introduced in the latest iOS app release. This affects both iOS 26.5 stable and iOS 27 Beta 2 users, suggesting a deep runtime-level regression.

### Platform Fragmentation Pain
- **Android/Termux:** Broken since v2.1.113 (60+ days, #50270) with no fix
- **ARM64 Windows (Snapdragon X):** Cowork fails despite passing readiness checks (#50674)
- **macOS:** Background PTY multiplexing leaks (#70483)
- **Web:** Proxy blocks GitHub access for routines (#70474)

### Cost & Reliability Concerns
- **Deep-research token waste** (#65500) — 3.5M tokens burned with zero output when subagents fail
- **SessionEnd hooks killed prematurely** (#70465) — Cleanup logic is unreliable
- **Remote session compaction disabled** (#70477) — No automatic compaction in bridge-attached sessions, leading to unbounded context growth

### Rendering & File Handling Issues (Recently Closed but Recurring)
A cluster of related issues about file attachments rendering as unclickable/empty chips was closed today (#67869, #69780, #65677, #69279). These spanned Windows and macOS desktop apps and affected both inline images and file deliveries. The fixes appear to have been rolled up, but the pattern suggests fragile rendering logic in the desktop webview.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-24

## Today's Highlights

A major rate-limit cost regression affecting `gpt-5.5` (Issue #28879) remains the hottest open issue, with 130 comments and 257 upvotes after users reported budget draining 10–20x faster since June 16. The team shipped six Rust alpha releases (v0.143.0-alpha.3 through .11) and merged critical PRs addressing SQLite log churn and context window history reuse. Enterprise feature work continues with experimental credential broker integration and marketplace source policy enforcement.

## Releases

Six pre-release versions of the Rust component were published in the last 24 hours: `rust-v0.143.0-alpha.3` through `rust-v0.143.0-alpha.11`. No changelog details were provided beyond version bump announcements.

---

## Hot Issues

1. **[#28879 — Rate-limit cost per token jumped ~10-20x since June 16, draining 5h budget in 2-3 prompts](https://github.com/openai/codex/issues/28879)** 🔥
   - *Status: Open | 130 comments, 257 👍*
   - **Why it matters:** This is the highest-engagement open issue. Users on ChatGPT Plus report `gpt-5.5` consumption skyrocketing from 20+ prompts per budget window to just 2–3. Session logs show `limit-% consumed per token` increased 10–20x with no model/plan change. Community is demanding a rollback or budget recalibration.

2. **[#26892 — gpt-5.5 listed as available locally but real requests fail with 404 'Model not found'](https://github.com/openai/codex/issues/26892)**
   - *Status: Closed | 84 comments, 28 👍*
   - **Why it matters:** Affected users on both Desktop and CLI. The model picker shows `gpt-5.5` but requests return 404. Closed as resolved in last 24h — significant for those who lost access for ~17 days.

3. **[#28224 — Codex SQLite feedback logs can write ~640 TB/year, consuming SSD endurance](https://github.com/openai/codex/issues/28224)**
   - *Status: Open (author closing) | 71 comments, 331 👍*
   - **Why it matters:** Eye-popping scale: 640 TB/year projected. Three merged PRs (#29432, #29457 in 0.142.0) reduced logs by ~85%. Community reaction is relief mixed with concern that this wasn't caught earlier. Highest 👍 count of any issue.

4. **[#16767 — Codex Desktop triggers sustained syspolicyd/trustd CPU spikes on macOS](https://github.com/openai/codex/issues/16767)**
   - *Status: Open | 18 comments, 26 👍*
   - **Why it matters:** Persistent macOS system daemon (syspolicyd) CPU exhaustion on launch. Affects system-wide performance. No fix yet after 80+ days open.

5. **[#29197 — Codex WebSearch receives Cloudflare 403 managed challenge](https://github.com/openai/codex/issues/29197)**
   - *Status: Open | 11 comments*
   - **Why it matters:** Windows users hit Cloudflare anti-bot pages on `/backend-api/codex/alpha/search`, breaking WebSearch functionality. Affects both Desktop and CLI.

6. **[#29532 — Persistent SQLite TRACE log churn remains after rust-v0.142.0 on macOS](https://github.com/openai/codex/issues/29532)**
   - *Status: Open | 10 comments, 7 👍*
   - **Why it matters:** Follow-up to #28224 — the partial fix didn't fully resolve the issue. `codex_api::endpoint::responses_websocket` improved, but `#29457` fix not effective for this user.

7. **[#25667 — macOS app leaves code_sign_clone directories after quit (~965MB per launch)](https://github.com/openai/codex/issues/25667)**
   - *Status: Open | 9 comments, 17 👍*
   - **Why it matters:** Nearly 1GB of leaked disk space per launch. macOS code signing clones not being cleaned up. Significant for users with limited SSD space.

8. **[#19871 — MCP tool invocation regressed for custom/local providers (Ollama) in v0.117.0+](https://github.com/openai/codex/issues/19871)**
   - *Status: Open | 8 comments, 5 👍*
   - **Why it matters:** Long-standing regression (since April) affecting custom model providers. Bisected to v0.117.0. Community using local/Ollama setups is blocked.

9. **[#27662 — Codex Desktop exhausts syspolicyd, causing spctl "Too many open files" globally](https://github.com/openai/codex/issues/27662)**
   - *Status: Open | 7 comments, 3 👍*
   - **Why it matters:** Systemic macOS issue — Gatekeeper breaks for *all* binaries including `/bin/ls`. Codex Desktop's fd leak affects entire system, not just the app.

10. **[#29000 — Codex CLI 0.141.0 crashes with SIGTRAP on Intel macOS](https://github.com/openai/codex/issues/29000)**
    - *Status: Closed | 12 comments, 11 👍*
    - **Why it matters:** Crash on Intel Macs — signal TRAP indicates assertion failure or illegal instruction. Closed as resolved in last 24h.

---

## Key PR Progress

1. **[#29752 — Integrate experimental credential broker](https://github.com/openai/codex/pull/29752)**
   - *Status: Open*
   - **What it does:** Integration layer for the proxy-owned credential broker (#28034). Preserves brokered values across shell snapshots. Critical for secure credential handling in child processes.

2. **[#29762 — Reuse compacted history replacement for new context windows](https://github.com/openai/codex/pull/29762)**
   - *Status: Closed/merged*
   - **What it does:** Fixes history compaction bypass when starting new context windows. Ensures consistent item-ID assignment. Directly related to context window reliability.

3. **[#29765 — Ignore local curated plugins when remote catalog is active](https://github.com/openai/codex/pull/29765)**
   - *Status: Open, code-reviewed*
   - **What it does:** Suppresses `openai-curated` plugins during remote plugin mode. Central to the ongoing plugin marketplace architecture.

4. **[#29758 — Fix token-budget compaction baselines](https://github.com/openai/codex/pull/29758)**
   - *Status: Open, code-reviewed*
   - **What it does:** Fixes two P2 review comments from #29743. Prevents stale model context from being captured during token-budget compaction. Performance-critical.

5. **[#29709 — Add gated Ultra reasoning effort](https://github.com/openai/codex/pull/29709)**
   - *Status: Open, code-reviewed*
   - **What it does:** Introduces "Ultra" reasoning effort — maximum backend reasoning. Gated behind model catalog and `multi_agent_mode` feature flags. New product-level capability.

6. **[#29710 — Derive multi-agent mode from Ultra effort](https://github.com/openai/codex/pull/29710)**
   - *Status: Open, code-reviewed*
   - **What it does:** Makes multi-agent mode deterministic by deriving it from the turn's reasoning effort instead of having separate client selection. Prevents conflicts across thread lifecycle.

7. **[#28630 — Trace MCP startup latency](https://github.com/openai/codex/pull/28630)**
   - *Status: Closed/merged*
   - **What it does:** Adds trace-level instrumentation for MCP server startup — per-server setup, client construction, initialization, tool listing. Attaches `server_name` to spans. Diagnostic improvement for MCP reliability.

8. **[#29733 — Allow ChatGPT-hosted MCP servers to use session auth](https://github.com/openai/codex/pull/29733)**
   - *Status: Open*
   - **What it does:** Decouples session authentication from Codex Apps-specific server name matching. Enables ChatGPT-hosted MCP endpoints to explicitly use session auth. Security boundary improvement.

9. **[#29683 — Add managed new-thread model settings](https://github.com/openai/codex/pull/29683)**
   - *Status: Open*
   - **What it does:** Parses `model`, `model_reasoning_effort`, and `service_tier` from `requirements.toml` `[models.new_thread]`. Applies managed defaults in ThreadManager. Enterprise configuration governance.

10. **[#29711 — Let image generation extension hosts control output persistence](https://github.com/openai/codex/pull/29711)**
    - *Status: Closed/merged*
    - **What it does:** Allows extension hosts to return generated images without writing to filesystem. Solves model path-leakage concerns for image gen extensions.

---

## Feature Request Trends

- **Enterprise configuration governance** — Multiple PRs and issues target `requirements.toml`, marketplace source policies, and managed defaults. The ecosystem is clearly moving toward administrator-controlled settings for workplace deployments.
- **Ultra reasoning / multi-agent mode** — The two PRs on Ultra effort and derived multi-agent mode suggest a new product tier focused on maximally capable reasoning with autonomous subagent delegation.
- **Plugin marketplace architecture** — A family of PRs (#29765, #29690, #29691, #29753) build out remote catalog activation, source admission policies, and runtime enforcement. Indicates a major plugin distribution overhaul.
- **Credential security** — The experimental credential broker (#28034, #29752) addresses child-process credential exfiltration. Security architecture upgrade for local credential management.
- **HTTPS-only transport** — Issue #27381 requests a transport option to skip WebSocket and use HTTPS first, reflecting pain with corporate proxies and VPNs.

---

## Developer Pain Points

1. **Rate-limit cost instability** — Issue #28879 is the most intense: budget consumption spiking 10–20x without warning. Developers feel they can't trust their plan limits.
2. **Model availability inconsistency** — `gpt-5.5` continues to cause confusion with 404 errors despite appearing in pickers (#26892, #26910, #29761). Multiple issues reopened over weeks.
3. **MacOS system-level resource leaks** — Three active issues (#16767, #25667, #27662) describe Codex degrading the entire macOS system: CPU spikes, SSD disk space leaks, and Gatekeeper file-descriptor exhaustion.
4. **SQLite log amplification** — The 640 TB/year projection (#28224) shocked the community. Even the 85% reduction leaves ongoing write amplification concerns (#29532).
5. **Windows path encoding failures** — Issue #28258 reveals Chinese-character user paths producing mojibake and filling disk with staging directories. Localization edge cases remain unaddressed.
6. **MCP reliability regressions** — Custom/local model providers (#19871), session lifecycle tool disappearances (#15508), and startup latency all point to MCP as a fragile integration point.
7. **Stale local image caching** — Issue #24446 describes a subtle UX bug: Codex caches images by filesystem path, so regenerated files show stale content. Affects workflows where tools overwrite local artifacts.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-24

## Today's Highlights
Multiple high-priority agent reliability bugs remain under active discussion, including subagents falsely reporting success after hitting turn limits and generalist agent hangs. A significant security-focused PR addresses OAuth keep-alive socket reuse failures on Node.js 24+, while the team continues to push forward on SSRF protection, AST-aware codebase mapping, and improved Auto Memory handling. No new releases were published in the last 24 hours.

## Releases
No new releases in the last 24 hours.

---

## Hot Issues (Top 10 by Activity)

### 1. Subagent recovery after MAX_TURNS reported as GOAL success
**#22323** — [OPEN, P1, bug]  
Community reaction: 2 👍, 8 comments  
The `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` even when it hit its max turn limit before performing any analysis. This masks real failures and misleads users into thinking work was completed.  
🔗 [github.com/google-gemini/gemini-cli/issues/22323](https://github.com/google-gemini/gemini-cli/issues/22323)

### 2. Robust component-level evaluations
**#24353** — [OPEN, P1, EPIC]  
Community reaction: 0 👍, 7 comments  
An epic tracking the need for structured, repeatable evaluations of individual components. Builds on earlier work (issue #15300) that introduced behavioral evals; the team now has 76 tests across 6 Gemini models, but needs better infrastructure.  
🔗 [github.com/google-gemini/gemini-cli/issues/24353](https://github.com/google-gemini/gemini-cli/issues/24353)

### 3. Generalist agent hangs
**#21409** — [OPEN, P1, bug]  
Community reaction: 8 👍, 7 comments  
The generalist agent hangs indefinitely when invoked, even for trivial tasks like folder creation. Users report waiting up to an hour before cancelling. Workaround: instructing the model not to use sub-agents. High community pain.  
🔗 [github.com/google-gemini/gemini-cli/issues/21409](https://github.com/google-gemini/gemini-cli/issues/21409)

### 4. Assess impact of AST-aware file reads, search, and mapping
**#22745** — [OPEN, P2, EPIC]  
Community reaction: 1 👍, 7 comments  
Investigating whether AST-aware tools can reduce token waste, improve codebase navigation, and enable method-level reads in a single tool call. Potential for significant quality and efficiency gains.  
🔗 [github.com/google-gemini/gemini-cli/issues/22745](https://github.com/google-gemini/gemini-cli/issues/22745)

### 5. Gemini does not use skills and sub-agents enough
**#21968** — [OPEN, P2, bug]  
Community reaction: 0 👍, 6 comments  
Anecdotal but concerning: the model rarely invokes custom skills or sub-agents on its own, even when prompted with relevant descriptions. Users must explicitly instruct the model to delegate.  
🔗 [github.com/google-gemini/gemini-cli/issues/21968](https://github.com/google-gemini/gemini-cli/issues/21968)

### 6. Auto Memory: low-signal sessions retried indefinitely
**#26522** — [OPEN, P2, bug]  
Community reaction: 0 👍, 5 comments  
Auto Memory only marks a session as processed after a successful `read_file`. If the extraction agent skips a low-signal session, it remains unprocessed and gets repeatedly resurfaced — causing infinite retry loops.  
🔗 [github.com/google-gemini/gemini-cli/issues/26522](https://github.com/google-gemini/gemini-cli/issues/26522)

### 7. Add deterministic redaction and reduce Auto Memory logging
**#26525** — [OPEN, P2, bug]  
Community reaction: 0 👍, 5 comments  
Auto Memory sends local transcripts to the model for extraction, with a prompt to redact secrets — but this is after content is already in the model context. Skills can also be logged. Needs pre-context redaction.  
🔗 [github.com/google-gemini/gemini-cli/issues/26525](https://github.com/google-gemini/gemini-cli/issues/26525)

### 8. Shell command stuck with "Waiting input" after completion
**#25166** — [OPEN, P1, bug]  
Community reaction: 3 👍, 4 comments  
After executing simple CLI commands, Gemini stays in "awaiting user input" state even though the command has finished. Happens with trivially non-interactive commands.  
🔗 [github.com/google-gemini/gemini-cli/issues/25166](https://github.com/google-gemini/gemini-cli/issues/25166)

### 9. Browser subagent fails on Wayland
**#21983** — [OPEN, P1, bug]  
Community reaction: 1 👍, 4 comments  
The browser subagent crashes under Wayland display servers. Termination reason is `GOAL` but no useful work was done. Affects Linux users on modern desktop environments.  
🔗 [github.com/google-gemini/gemini-cli/issues/21983](https://github.com/google-gemini/gemini-cli/issues/21983)

### 10. 400 error with > 128 tools
**#24246** — [OPEN, P2, bug]  
Community reaction: 0 👍, 3 comments  
Gemini CLI returns a 400 error when the total number of available tools exceeds 128. Users expect the agent to intelligently filter tools to stay within model limits.  
🔗 [github.com/google-gemini/gemini-cli/issues/24246](https://github.com/google-gemini/gemini-cli/issues/24246)

---

## Key PR Progress (Top 10)

### 1. OAuth keep-alive socket reuse fix
**#28103** — [OPEN, P2, security]  
Fixes a Node.js 24.17.0+ regression where keep-alive socket reuse causes `ERR_STREAM_PREMATURE_CLOSE` during "Sign in with Google" OAuth token exchange. Critical for users on newer Node versions.  
🔗 [github.com/google-gemini/gemini-cli/pull/28103](https://github.com/google-gemini/gemini-cli/pull/28103)

### 2. Tool registry discovery with AST extraction
**#28113** — [OPEN, size/l]  
Adds a tool registry for eval reporting, including AST-based extraction of tool names used in eval assertions. Groups built-in tools into categories and builds from `ALL_BUILTIN_TOOL_NAMES`.  
🔗 [github.com/google-gemini/gemini-cli/pull/28113](https://github.com/google-gemini/gemini-cli/pull/28113)

### 3. Fix thought leakage from scrubbed history
**#27971** — [OPEN, size/m]  
Resolves a bug where the model's internal reasoning thoughts leaked into plain-text history turns, causing confusion and infinite-loop monologues in subsequent conversations.  
🔗 [github.com/google-gemini/gemini-cli/pull/27971](https://github.com/google-gemini/gemini-cli/pull/27971)

### 4. Case-insensitive sensitive path blocklist + VS Code HITL
**#27966** — [OPEN, size/m]  
Enforces case-insensitive blocking of `.git`, `.env`, `node_modules`, and prevents prompting users if a VS Code Human-in-the-Loop (HITL) file or path is involved. Addresses a prompt injection vector.  
🔗 [github.com/google-gemini/gemini-cli/pull/27966](https://github.com/google-gemini/gemini-cli/pull/27966)

### 5. SSRF protection for OAuth metadata discovery in MCP
**#28112** — [OPEN, size/l]  
Closes an SSRF coverage gap by adding hostname validation and DNS resolution checks to MCP OAuth discovery flows, matching protections already in `web-fetch.ts`.  
🔗 [github.com/google-gemini/gemini-cli/pull/28112](https://github.com/google-gemini/gemini-cli/pull/28112)

### 6. Don't offer to resume unsaved sessions
**#27914** — [OPEN, P2, size/m]  
Fixes a UX bug where the CLI would print "To resume this session: gemini --resume <id>" even when disk writes failed (ENOSPC) and the session was never actually saved.  
🔗 [github.com/google-gemini/gemini-cli/pull/27914](https://github.com/google-gemini/gemini-cli/pull/27914)

### 7. Show descriptive sandbox label instead of 'current process'
**#28099** — [OPEN, P2, size/s]  
Fixes the footer's SandboxIndicator to display the actual seatbelt profile name on macOS, replacing the unhelpful hardcoded "current process" label.  
🔗 [github.com/google-gemini/gemini-cli/pull/28099](https://github.com/google-gemini/gemini-cli/pull/28099)

### 8. Fix ellipsis logic in EditTool getDescription()
**#28105** — [OPEN, size/m]  
Corrects a subtle display bug where the `...` suffix in edit description snippets was incorrectly computed, causing truncated or mangled previews.  
🔗 [github.com/google-gemini/gemini-cli/pull/28105](https://github.com/google-gemini/gemini-cli/pull/28105)

### 9. Cloud Run webhook ingestion service for Caretaker Agent
**#28015** — [OPEN, size/l]  
Implements a Cloud Run service that ingests GitHub webhooks, verifies payload signatures, stores issues via Firestore, and publishes sanitized metadata to Pub/Sub for the Caretaker Agent.  
🔗 [github.com/google-gemini/gemini-cli/pull/28015](https://github.com/google-gemini/gemini-cli/pull/28015)

### 10. Fix missing activate() Disposables in VS Code companion
**#27936** — [OPEN, P2, size/s]  
Fixes a JavaScript comma-expression bug in `activate()` that caused two groups of registrations to not be properly pushed into `context.subscriptions`, leading to disposal issues.  
🔗 [github.com/google-gemini/gemini-cli/pull/27936](https://github.com/google-gemini/gemini-cli/pull/27936)

---

## Feature Request Trends

1. **AST-aware code intelligence** — Multiple issues request deeper code understanding: method-level reads, AST-based codebase mapping, and improved navigation to reduce token waste and tool call misalignment.

2. **Agent self-awareness & transparency** — Users want the CLI to understand its own capabilities (hotkeys, flags, subagent trajectories) and to expose subagent context in `/bug` reports and shared chat sessions for debugging.

3. **Better destructive action guards** — The agent should prefer safer alternatives to `git reset --force`, destructive database operations, and other high-risk commands, especially during complex git or resource management tasks.

4. **Subagent adoption improvement** — The model should proactively use custom skills and sub-agents without requiring explicit user instruction, and should respect `settings.json` configurations for agents like the Browser Agent.

5. **Evaluation infrastructure** — Community and maintainers are pushing for robust component-level evaluations, behavioral tests, and shared eval infrastructure to ensure quality across model updates and agent changes.

---

## Developer Pain Points

1. **Agent hangs and false success reports** — The generalist agent hangs indefinitely (issue #21409), while subagents like `codebase_investigator` falsely claim `GOAL` success despite hitting turn limits (#22323). This erodes trust and wastes developer time.

2. **Shell execution confusion** — The CLI gets stuck with "Waiting input" after commands complete (#25166), creates temp scripts in random directories (#23571), and gets stuck on interactive prompts like `vite create` (#22465).

3. **Configuration and permission issues** — Symlinked agent files not recognized (#20079), subagents running despite being disabled (#22093), and Browser Agent ignoring `settings.json` overrides (#22267) create a frustrating configuration experience.

4. **Memory system instability** — Auto Memory retries low-signal sessions indefinitely (#26522), silently skips invalid memory patches (#26523), and may leak secrets by sending content to the model before redaction (#26525).

5. **Scale limitations** — The CLI returns 400 errors when more than 128 tools are available (#24246), and the Browser Agent's fail-fast approach to locked profiles prevents session recovery (#22232).

6. **Terminal / rendering issues** — Terminal resize causes flickering (#21924), exiting external editors in `terminalBuffer` mode corrupts the display (#24935), and the Browser Agent fails entirely on Wayland (#21983).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-24

## Today's Highlights
Release **v1.0.64** landed with improved transparency around path access grants and pay-as-you-go budgeting. The community is buzzing with **10 new triage-labeled issues** filed today alone, covering critical problems like secret scanning freezing the TUI, session-state file-descriptor exhaustion, and sub-agent model overrides being silently dropped in BYOK mode. Windows users continue to face a cluster of rendering and sandbox compatibility issues.

## Releases
**v1.0.64** (2026-06-23) — [View Release](https://github.com/github/copilot-cli/releases/tag/v1.0.64)
- Path access prompts now show resolved symlink targets for full transparency.
- Pay-as-you-go additional usage budget is displayed at launch, refreshed after a request is rejected for hitting the spend limit, with a friendly over-limit message.

## Hot Issues
1. **#3901 — Copilot cannot launch from WSL after v1.0.64 upgrade** [OPEN] — [Link](https://github.com/github/copilot-cli/issues/3901)  
   Freshly reported today: upgrading the Windows installation breaks WSL launch with "Failed to load" error. Critical for the significant WSL developer base. 👍 0 (new).

2. **#3900 — Secret filtering blocks the CLI UI thread** [OPEN] — [Link](https://github.com/github/copilot-cli/issues/3900)  
   Synchronous secret scanning on the UI thread can freeze the TUI, especially with large response objects. Performance and responsiveness risk. 👍 0 (new).

3. **#3892 — Session-state directory never pruned, causes EMFILE exhaustion** [OPEN] — [Link](https://github.com/github/copilot-cli/issues/3892)  
   Thousands of `~/.copilot/session-state/` folders accumulate over time, crashing Copilot Chat in VS Code. A silent reliability bomb for heavy users. 👍 0 (new).

4. **#3891 — Sub-agent `model:` override silently dropped in BYOK mode** [OPEN] — [Link](https://github.com/github/copilot-cli/issues/3891)  
   Custom providers see sub-agent model directives ignored with no warning. Breaks predictability for enterprise BYOK setups. 👍 0 (new).

5. **#3881 — Quota deduction mismatch: 5% subtracted instead of expected 2%** [OPEN] — [Link](https://github.com/github/copilot-cli/issues/3881)  
   User reports Claude Sonnet 4.5 (6x multiplier) consumed 5% quota instead of 2%. Billing/transparency concern with strong user reaction. 👍 0.

6. **#3866 — Thinking/reasoning text unreadable on dark backgrounds** [OPEN] — [Link](https://github.com/github/copilot-cli/issues/3866)  
   Hardcoded dark gray foreground for reasoning text is invisible on dark terminals. Accessibility regression since recent update. 👍 2.

7. **#3501 — Scroll bar misaligns text on Windows** [OPEN] — [Link](https://github.com/github/copilot-cli/issues/3501)  
   Vertical scroll bar causes text rendering misalignment in Windows Console Host and Terminal. Long-standing, highly upvoted (👍 9) Windows rendering bug.

8. **#1944 — Mouse wheel scroll captured by input box instead of conversation history (Windows)** [CLOSED] — [Link](https://github.com/github/copilot-cli/issues/1944)  
   Regression fixed after 3+ months. Mouse wheel now correctly scrolls chat history rather than the input box. 👍 3 — community win.

9. **#2486 — MCP server blocked by policy on personal Pro+ account** [CLOSED] — [Link](https://github.com/github/copilot-cli/issues/2486)  
   User found a hack to bypass policy blocking; issue closed without official GitHub reply, raising transparency concerns. 👍 0.

10. **#3898 — Black text on dark blue background due to OSC 11** [OPEN] — [Link](https://github.com/github/copilot-cli/issues/3898)  
    Custom terminal background color (OSC 11) causes unreadable black-on-dark-blue text — a fresh accessibility issue. 👍 0 (new).

## Key PR Progress
Only **1 PR** was active in the last 24 hours:

- **#3873 — Add initial console log for greeting** [OPEN] — [Link](https://github.com/github/copilot-cli/pull/3873)  
  Adds a simple startup log message. Minimal change; likely the author's first contribution. 👍 0.

PR activity is unusually low today, likely because the team is addressing the influx of triage issues.

## Feature Request Trends
The community's most demanded directions are:

1. **Recurring/Scheduled Agent Prompts** (#2056, 👍 4) — Users want agents to act on a timer, not just on manual input.
2. **Shell Command History in `!` Mode** (#2680, 👍 0) — Recall previous shell commands via Up/Down (currently only Copilot chat history works).
3. **Private Network Access for `web_fetch`** (#3731, 👍 2) — Restore ability to fetch from corporate/protected networks for agentic workflows.
4. **Transparent Model/Quota Debugging** (#3881, 👍 0) — Users demand itemized quota deductions and clearer billing.
5. **Multi-Account Identity Handling** (#3897, 👍 0) — Copilot CLI should correctly select the right GitHub account when pushing, especially for EMU + personal setups.

## Developer Pain Points
Recurring frustrations from today's issue set:

- **Windows rendering regressions** — Scroll bar misalignment (#3501) and mouse wheel capture (#1944, now fixed) plague Windows users.
- **TUI freezes and performance** — Synchronous secret scanning (#3900) and unpruned session-state (#3892) cause UI hangs and even crash VS Code.
- **BYOK / custom provider pitfalls** — Sub-agent model overrides ignored (#3891), MCP stdio transport rejected (#3889), and plugins unavailable via ACP (#2590).
- **Accessibility ignored** — Hardcoded dark reasoning text (#3866) and OSC 11 color clash (#3898) show insufficient theming/testing.
- **Policy and documentation gaps** — MCP servers blocked without explanation (#2486), undocumented sandbox limitations on ReFS (#3712), and unclear `/rubber-duck` availability (#3899).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-06-24

**Generated for developers building with AI-powered terminal workflows.**

## Today's Highlights

Activity on the Kimi Code CLI repository remains low today, with no new releases or pull requests in the last 24 hours. The community's focus continues to be on a single open bug where `yolo` mode fails to suppress approval prompts, undermining a core feature for automated workflows. With zero PR activity and only one updated issue, the project appears to be in a quiet or consolidation phase.

## Releases

No new releases in the last 24 hours. The latest available version remains **Kimi Code v0.12.0**.

## Hot Issues

**1. [Bug] Kimi CLI is prompting for approval in yolo mode**  
[#2448](https://github.com/MoonshotAI/kimi-cli/issues/2448)  
*Why it matters:* The `yolo` mode is designed for fully autonomous, no-confirmation execution. This bug directly breaks that promise, forcing users to manually approve actions—defeating the purpose of the flag. The issue has been open since June 10 with only one comment and zero upvotes, suggesting either low community engagement or a narrow reproduction path. Expect this to be a priority fix once triaged by maintainers.

*No other issues were updated in the last 24 hours.*

## Key PR Progress

No pull requests were updated in the last 24 hours.

## Feature Request Trends

With no new feature requests surfaced in today's data, the most requested direction remains implicit from prior issues: **reliable autonomous execution modes** (e.g., `yolo` mode obeying its contract). Users consistently want to reduce friction in agentic CLI workflows, especially around permissions and approvals.

## Developer Pain Points

- **Mode contract violations:** The top pain point is that `yolo` mode, which should imply no user interaction, still prompts for approval. This undermines trust in the mode system.
- **Low signal environment:** With zero PRs and one stale issue, developers may be frustrated by lack of visible progress on known bugs or slow response times from maintainers.
- **API key confusion:** The issue reporter mentions "the one with the api key" as their subscription, reflecting ongoing developer friction around authentication and plan selection.

*No other recurring frustrations were identified in today's limited dataset.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-24

**Prepared for:** AI developer tool engineers and community contributors  
**Data source:** [github.com/anomalyco/opencode](https://github.com/anomalyco/opencode)

---

## Today's Highlights

A burst of activity across the desktop app: three PRs landed today improving session tab behavior, prompt state preservation, and keyboard shortcut management. On the infrastructure side, the team merged a core refactor mapping providers to integrations and a fix for the OpenCode connection flow. Community attention remains focused on a long-running TUI search feature request (28 comments) and a high-impact bug where the `Write` tool fails silently on files over 1000 lines.

---

## Releases

No new releases were published in the last 24 hours.

---

## Hot Issues

| # | Title | Comments | 👍 | Why it matters |
|---|-------|----------|---|----------------|
| [#4714](https://github.com/anomalyco/opencode/issues/4714) | [FEATURE] TUI – Search for string in session buffer | 28 | 35 | Long-standing ask (8 months old) for in-session text search; 35 upvotes show strong demand from TUI users |
| [#15035](https://github.com/anomalyco/opencode/issues/15035) | When will agent-teams be added? | 25 | 4 | Consistent community interest in multi-agent orchestration patterns despite being closed |
| [#19604](https://github.com/anomalyco/opencode/issues/19604) | `Write` tool fails silently on large files (~1000+ lines) | 12 | 9 | **High impact**: silent failures corrupt workflows for users editing substantial files |
| [#14212](https://github.com/anomalyco/opencode/issues/14212) | Support more DBMS for state storage | 11 | 21 | Post-Drizzle migration opens up PostgreSQL etc.; 21 upvotes signal strong interest in production-scale deployments |
| [#10908](https://github.com/anomalyco/opencode/issues/10908) | [docs] Add RTL support for Arabic | 10 | 7 | Closed with i18n improvements; important for global accessibility |
| [#6792](https://github.com/anomalyco/opencode/issues/6792) | Task tool timeouts in multi-agent conductor pattern | 10 | 2 | Closed but symptomatic of deeper sub-agent reliability issues |
| [#32747](https://github.com/anomalyco/opencode/issues/32747) | `@` file mentions exclude newly created files | 6 | 3 | Fresh bug: stale search state in TUI forces restarts |
| [#15431](https://github.com/anomalyco/opencode/issues/15431) | Session freezes after macOS lock screen | 5 | 6 | Persistent issue for macOS laptop users; task stays "In Progress" but UI dead |
| [#27474](https://github.com/anomalyco/opencode/issues/27474) | TypeError: Failed to fetch on agent/explore | 6 | 0 | Frontend crash on explorer page; may affect plugin discovery |
| [#30895](https://github.com/anomalyco/opencode/issues/30895) | v1.16.0 WSL path conversion breaks sessions | 5 | 0 | Regression: Desktop converts WSL `/mnt/c/` to Windows `C:\`, breaking file resolution |

---

## Key PR Progress

| # | Title | Status | What it does |
|---|-------|--------|-------------|
| [#33572](https://github.com/anomalyco/opencode/pull/33572) | fix(app): use fixed titlebar tab widths | OPEN | Stabilizes tab sizing at 224px; preserves horizontal scroll when tabs overflow – a UX polish PR |
| [#33569](https://github.com/anomalyco/opencode/pull/33569) | fix(app): make session navigation stable and fast | OPEN | Eliminates loading screens during session switches by keeping the previous view painted until the new one is ready |
| [#33571](https://github.com/anomalyco/opencode/pull/33571) | refactor(schema): extract shared public schemas | OPEN | Creates a private `@opencode-ai/schema` package for 10 core schema types – a foundation for API consistency |
| [#33566](https://github.com/anomalyco/opencode/pull/33566) | feat(app): keep prompt state in tabs | CLOSED | Persists prompt text across tab switches without reloading – addresses a common workflow friction |
| [#33567](https://github.com/anomalyco/opencode/pull/33567) | fix(app): mount shortcuts per titlebar tab | CLOSED | Fixes `mod+1..9` keyboard shortcuts so they only register for visible tabs; prevents ghost bindings |
| [#33565](https://github.com/anomalyco/opencode/pull/33565) | fix(tui): restore file mention mime | OPEN | Restores `text/plain` MIME for file mentions, preventing binary source files from being incorrectly sent as media |
| [#33562](https://github.com/anomalyco/opencode/pull/33562) | feat(core): map providers to integrations | CLOSED | Adds optional integration IDs to providers; enables credential resolution through catalog – important for multi-cloud setups |
| [#33560](https://github.com/anomalyco/opencode/pull/33560) | fix(core): simplify opencode connection flow | CLOSED | Streamlines OAuth: uses Console URL directly, picks first org alphabetically, renames auth methods for clarity |
| [#33281](https://github.com/anomalyco/opencode/pull/33281) | feat(cli): add standalone v2 session flow | OPEN | Introduces `--standalone` mode spawning an authenticated private server child process – a major architecture shift for CLI users |
| [#33483](https://github.com/anomalyco/opencode/pull/33483) | feat(mcp): add resource read tools | CLOSED | Adds model-callable MCP resource list/read tools; fixes `@`-mentioned resource reads and binary attachment handling |

---

## Feature Request Trends

1. **Session buffer search (TUI)** – #4714 (28 comments, 35 👍) remains the top feature request. Users want `find`-like text search in agent output, matching text-editor conventions.

2. **Multi-agent / agent-teams** – Multiple threads (#15035, #6792, #17607) ask for better sub-agent orchestration, including per-agent tool permissions and hierarchical task plans (#13928).

3. **Portable session data** – Users consistently want `/export` on desktop (#31453), session export/restore (#19513), and support for PostgreSQL and other DBMS backends (#14212) for production workloads.

4. **Keybinding customization** – #11898 (closed) and #14797 reflect ongoing demand for customizable Enter/Submit behavior and scrolling keybinds in permission dialogs.

5. **Plugin API expansion** – Questions about image data access (#20001), custom provider headers (#15306), and the `config` hook pattern (#24065) show the community pushing plugin capabilities beyond documented boundaries.

---

## Developer Pain Points

- **Silent failures erode trust** – `Write` tool failing on large files (#19604) with no error message is the week's most cited high-severity bug. Users report multiple retries produce the same abort.
- **WSL path mangling breaks Windows workflows** – #30895 shows Desktop v1.16.0 converting `/mnt/c/` to `C:\` paths, corrupting file resolution. WSL clipboard issues (#7297) and path problems compound the Linux-on-Windows experience.
- **Session state fragility** – macOS lock-screen freezes (#15431), disappeared session histories (#26505), and stale file index (#32747) all point to unreliable session lifecycle management.
- **Sub-agent reliability gaps** – Timeout patterns (#6792), `ProviderModelNotFoundError` for sub-agents (#21615), and missing Scout autocomplete (#28100) suggest the sub-agent execution path needs hardening.
- **Accidental system modification** – #32080 (Node.js deleted, PATH corrupted) is a stark reminder that agent actions need stronger sandboxing guardrails.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-24

## Today's Highlights
Pi v0.80.2 shipped with critical API-key credential and provider-scoped environment fixes, while v0.80.1 introduced regressions for Nvidia, DeepSeek, and Cloudflare Workers.AI. The community is actively debating multi-agent TUI visibility and session-tree enhancements, with a notable spike in issues around session data integrity and provider-specific compatibility.

## Releases

**v0.80.2** — [View Release](https://github.com/earendil-works/pi/releases/tag/v0.80.2)
- Changed inherited `ApiKeyCredential` to use `auth.json`-compatible discriminator `type: "api_key"` with provider-scoped `env` values (breaking from `type: "api-key"` and metadata).
- Renamed public harness shell execution options type from `ExecutionEnvExe`.

**v0.80.1** — [View Release](https://github.com/earendil-works/pi/releases/tag/v0.80.1)
- Fixed Amazon Bedrock `AWS_PROFILE` endpoint resolution for built-in inference profile endpoints.
- Fixed Fireworks Anthropic-compatible requests for session-affinity and unsupported tool-field defaults.
- Fixed Together provider compatibility.

**v0.80.0** — [View Release](https://github.com/earendil-works/pi/releases/tag/v0.80.0)
- Added `Ctrl+J` as a default newline keybinding alongside `Shift+Enter`.
- Renamed `zai` provider label to "ZAI Coding Plan (Global)".
- Deprecated old global API (`stream`/`complete`/`completeSimple`).

## Hot Issues (10 noteworthy)

1. **[#5825] Streaming markdown forces scroll to bottom** *(OPEN, 30 comments)* — [Issue](https://github.com/earendil-works/pi/issues/5825)  
   Users with "clear on shrink" enabled experience forced scroll-to-bottom while reading long Markdown responses. High community engagement suggests this is a top UX pain point.

2. **[#6020] DeepSeek provider broken in 0.80** *(CLOSED, 11 comments)* — [Issue](https://github.com/earendil-works/pi/issues/6020)  
   v0.80 fails with `unknown variant "developer"` for DeepSeek. The `developer` role is not in pi's allowed list, hinting at a version mismatch with DeepSeek's API evolution.

3. **[#5700] Support multiple live agent sessions with TUI switching** *(CLOSED, 8 comments)* — [Issue](https://github.com/earendil-works/pi/issues/5700)  
   Users want concurrent agent sessions (e.g., background analysis while chatting). Current `switchSession` tears down the running session — a long-requested architectural change.

4. **[#6016] Nvidia provider broken in 0.80.1** *(CLOSED, 7 comments)* — [Issue](https://github.com/earendil-works/pi/issues/6016)  
   `streamSimpleOpenAICompletions` is not a function after upgrading. Rolling back to 0.79.10 is the only workaround. This pattern also appears for local models (#6017).

5. **[#5556] Session listing retains full transcript text** *(CLOSED, 6 comments)* — [Issue](https://github.com/earendil-works/pi/issues/5556)  
   Despite streaming JSONL optimization, `buildSessionInfo()` still concatenates all messages into memory — a performance regression for long sessions.

6. **[#5989] Extension pi-lovely-codex broken by update** *(CLOSED, 6 comments)* — [Issue](https://github.com/earendil-works/pi/issues/5989)  
   v0.80 update broke a community extension with no backward-compatibility window — highlights need for extension API stability.

7. **[#5996] Footer rendering breaks with newline in session name** *(CLOSED, 4 comments)* — [Issue](https://github.com/earendil-works/pi/issues/5996)  
   LLM-generated session names with `\n` cause TUI footer to overflow. Fix provided by the community (normalization via #5999).

8. **[#5730] Expose raw provider responses after response** *(CLOSED, 4 comments)* — [Issue](https://github.com/earendil-works/pi/issues/5730)  
   `after_provider_response` only exposes status/headers, not the raw response body. Extension authors need this for custom logging and debugging.

9. **[#6002] SessionManager.open() truncates non-session files** *(OPEN, 2 comments)* — [Issue](https://github.com/earendil-works/pi/issues/6002)  
   Opening a non-session file via `--session` overwrites it with a 133-byte header. Silent data loss — a serious safety issue.

10. **[#6021] Cloudflare Workers.AI 404 on 0.80.1** *(CLOSED, 1 comment)* — [Issue](https://github.com/earendil-works/pi/issues/6021)  
    URL template expansion leaves `{CLOUDFLARE_ACCOUNT_ID}` unsubstituted. Downgrade to 0.79.10 works.

## Key PR Progress (10 important PRs)

1. **[#6026] fix(tui): stabilize working status row** *(OPEN)* — [PR](https://github.com/earendil-works/pi/pull/6026)  
   References the forced-scroll-to-bottom bug (#5825). Aims to fix TUI status row flickering during streaming.

2. **[#6022] fix(ai): omit reasoning replay items for Codex responses** *(CLOSED)* — [PR](https://github.com/earendil-works/pi/pull/6022)  
   Removes `reasoning` items with `encrypted_content` from replay for Codex provider — fixes downstream rejection.

3. **[#6018] feature(coding-agent): show context estimates in session tree** *(OPEN)* — [PR](https://github.com/earendil-works/pi/pull/6018)  
   Displays context usage estimates in session tree for quick scanning — a highly-practical UX enhancement.

4. **[#5832] fix(ai): surface provider HTTP error body instead of opaque SDK message** *(OPEN)* — [PR](https://github.com/earendil-works/pi/pull/5832)  
   Fixes #5763. When behind a proxy/gateway, HTTP error bodies were suppressed — now surfaces the actual provider response.

5. **[#5526] Require terminal events for OpenAI Responses streams** *(CLOSED)* — [PR](https://github.com/earendil-works/pi/pull/5526)  
   Fixes random stream stoppage by requiring a terminal response event before processing — solves "context counter borked" issue.

6. **[#6004] feat: Normalize modern Microsoft Foundry Responses API endpoints** *(CLOSED)* — [PR](https://github.com/earendil-works/pi/pull/6004)  
   Handles `*.ai.azure.com` endpoints that current normalization misses — important for Azure AI Foundry users.

7. **[#5784] fix(coding-agent): sort threaded sessions by latest activity** *(CLOSED)* — [PR](https://github.com/earendil-works/pi/pull/5784)  
   Sorts threaded sessions by subtree latest activity rather than root modification date — ideal for multi-day forking workflows.

8. **[#5999] fix(coding-agent): normalize session names** *(CLOSED)* — [PR](https://github.com/earendil-works/pi/pull/5999)  
   Fixes #5996 — sanitizes newline characters from session names to prevent TUI footer breakage.

9. **[#5262] feat(ai): add Anthropic Vertex provider** *(OPEN)* — [PR](https://github.com/earendil-works/pi/pull/5262)  
   Adds built-in `anthropic-vertex` provider for Claude on Google Cloud Vertex AI — reuses existing Anthropic messaging path.

10. **[#5994] fix(ai): route OpenCode Go models through Anthropic** *(CLOSED)* — [PR](https://github.com/earendil-works/pi/pull/5994)  
    Routes Anthropic-compatible OpenCode Go models (e.g., `minimax-m2.7`) to the Anthropic SDK path instead of OpenAI chat-completions.

## Feature Request Trends

**1. Multi-Agent Session Management** — Multiple issues (#5700, #6011, #6012, #6013) request persistent background agent sessions with TUI switching, slash commands (`/swarm`, `/swarm-team`), and visual progress indicators — sign of growing adoption for parallel agent workflows.

**2. Provider-Agnostic Extensibility** — Requests for new provider integrations (#5986 Merge Gateway, #6024 MiniMax Image, #5262 Anthropic Vertex) and raw response access (#5730) indicate demand for pluggable, transparent provider layers.

**3. Session Tree UX Enhancements** — #6018 (context estimates), #5784 (activity-based sorting), and #5556 (transcript trimming) show users want richer session introspection without performance degradation.

**4. Prompt & Workflow UI** — #6012 asks for `swarm` as a default mode with prompt keyword triggering — similar to `/goal`. Suggests power users want declarative, context-aware automation.

## Developer Pain Points

**1. 0.80.x Provider Regressions** — 3 providers (Nvidia, DeepSeek, Cloudflare) broke in a single minor release. The shared error pattern `streamSimpleOpenAICompletions is not a function` points to a refactoring gap in the streaming abstraction.

**2. Silent Data Corruption** — `SessionManager.open()` truncating non-session files (#6002) and session file bloat from rapid thinking-level changes (#5909) expose unsafe file I/O patterns that can destroy user data.

**3. Extension API Fragility** — v0.80 breaking `pi-lovely-codex` (#5989) without migration path — community extension authors need stable hooks and deprecation warnings prior to breaking changes.

**4. CLI Surprise Behaviors** — `/model` silently overwriting `defaultModel` (#5976), `pi remove` not actually removing packages (#5966), and `--session` accepting invalid files (#6002) demonstrate inconsistent side-effect semantics in the CLI surface.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-24

## Today's Highlights
The Qwen Code team shipped **four releases** (v0.19.0, v0.19.1, plus two nightly variants) with notable features including MCP resource completion matching and a remote LSP status route. A major **input validation cleanup wave** swept through the codebase — 20+ issues from contributor `@tt-a1i` exposed fractional-value bugs across CLI, LSP, session management, and tools. Meanwhile, a **daemon-first architecture** is taking shape, with multiple PRs adding workspace permissions APIs, voice dictation, and optimized server startup.

## Releases
### v0.19.0
- **What's Changed**:
  - CI: Auto-publish VSCode companion after stable releases ([@yiliang114](https://github.com/yiliang114))
- [View Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.0)

### v0.19.1
- **What's Changed**:
  - `feat(cli)`: Match MCP resource completions by name and discover servers ([@wenshao](https://github.com/wenshao) in [#5733](https://github.com/QwenLM/qwen-code/pull/5733))
- [View Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.1)

### v0.18.5-preview.0 & v0.19.1-nightly.20260624.a234860a4
- `feat(serve)`: Add remote LSP status route ([@doudouOUC](https://github.com/doudouOUC))

## Hot Issues (Top 10 by Comment Count)

1. **[#4488](https://github.com/QwenLM/qwen-code/issues/4488) — VSCode plugin not showing in sidebar (v0.16.0)** (7 comments)
   - *Closed* | Category: UI, Scope: VSCode
   - **Why it matters**: A regression affecting VSCode 1.120.0+ users — the plugin icon appears briefly then disappears. The community is actively debugging version compatibility.

2. **[#5708](https://github.com/QwenLM/qwen-code/issues/5708) — Session list cursor accepts negative/unsafe values** (6 comments)
   - *Closed* | Priority: P3, welcome-pr
   - **Why it matters**: Pagination cursors derived from `mtimeMs` are not sanitized against invalid finite values, potentially causing infinite loops or corrupted session feeds.

3. **[#3877](https://github.com/QwenLM/qwen-code/issues/3877) — OPENCODE_GO_API_KEY env var not respected** (5 comments)
   - *Closed* | Status: needs-triage
   - **Why it matters**: Users who carefully set `.env` files are forced through auth selection on every startup — a persistent configuration reliability issue.

4. **[#5758](https://github.com/QwenLM/qwen-code/issues/5758) — Protocol/AuthType decoupling: config compatibility** (5 comments)
   - *Open* | Priority: P2, need-discussion
   - **Why it matters**: `modelId + baseUrl` works only in CLI; ACP and VSCode pass different parameter shapes. A proposal to map `providerId` to protocol — community seeking consensus on PR #5089.

5. **[#5736](https://github.com/QwenLM/qwen-code/issues/5736) — More frequent full prompt reprocessing after update** (4 comments)
   - *Open* | Welcome-pr
   - **Why it matters**: Local LLM users report regression in cache hit rate — every conversation continuation triggers full re-processing, increasing latency and compute cost.

6. **[#5562](https://github.com/QwenLM/qwen-code/issues/5562) — Input line-wrapping background color discontinuity** (4 comments)
   - *Closed* | Priority: P3, welcome-pr
   - **Why it matters**: A visual polish bug in the TUI — multi-line input backgrounds break mid-line, creating a jarring visual seam.

7. **[#5713](https://github.com/QwenLM/qwen-code/issues/5713) — Semi-invisible cursor in Alacritty** (4 comments)
   - *Closed* | Welcome-pr
   - **Why it matters**: Terminal emulator-specific rendering bug — cursor becomes nearly invisible in Alacritty while showing correctly in Xterm. Affects a popular terminal on Linux.

8. **[#5690](https://github.com/QwenLM/qwen-code/issues/5690) — LSP maxRestarts accepts fractional values** (4 comments)
   - *Closed* | Priority: P3
   - **Why it matters**: Part of the validation sweep — `maxRestarts: 1.5` silently floor-compares, giving misleading retry behavior.

9. **[#5694](https://github.com/QwenLM/qwen-code/issues/5694) — LSP position/limit params accept fractional values** (4 comments)
   - *Closed* | Welcome-pr
   - **Why it matters**: Line/character/endLine/endCharacter fields accept decimals — could cause off-by-one errors in tool calls.

10. **[#5698](https://github.com/QwenLM/qwen-code/issues/5698) — Shell/monitor integer-only params advertised as numbers** (4 comments)
    - *Closed* | Welcome-pr
    - **Why it matters**: JSON schema advertises `number` but runtime validation expects `integer` — API inconsistency that frustrates tool integration and LLM function calling.

## Key PR Progress (Top 10)

1. **[#5784](https://github.com/QwenLM/qwen-code/pull/5784) — fix(daemon): Reject stale prompt client admission** — Prevents async failures by invalidating unregistered prompt client IDs early. _(@doudouOUC)_

2. **[#5727](https://github.com/QwenLM/qwen-code/pull/5727) — docs: Add vertex-ai auth, missing commands, qc-helper index** — Audits 6 documentation files against current codebase. _(@DragonnZhang)_

3. **[#5783](https://github.com/QwenLM/qwen-code/pull/5783) — fix(core): Reject userinfo URLs in WebFetch validation** — Blocks `https://user:pass@example.com` before the HTTP request fires. _(@VectorPeak)_

4. **[#5743](https://github.com/QwenLM/qwen-code/pull/5743) — feat(cli): Add workspace permissions rules API** — Minimal daemon HTTP surface for managing allow/ask/deny permission lists. _(@doudouOUC)_ (Merged)

5. **[#5738](https://github.com/QwenLM/qwen-code/pull/5738) — fix(cli): Default to virtualized terminal history** — New users get scrollable in-app history by default. _(@ZevGit)_

6. **[#5781](https://github.com/QwenLM/qwen-code/pull/5781) — Expose MCP resource read tool** — Makes MCP resources callable by the model without requiring `@`-syntax injection. _(@yiliang114)_

7. **[#5788](https://github.com/QwenLM/qwen-code/pull/5788) — fix(cli): Replace emoji thinking/summary icons with Unicode text symbols** — Removes emoji rendering issues in terminals. _(@pomelo-nwu)_

8. **[#5668](https://github.com/QwenLM/qwen-code/pull/5668) — feat(cli): Show model thinking intent in loading indicator** — Replaces random witty phrases with real-time model `ThoughtSummary`. _(@pomelo-nwu)_

9. **[#5786](https://github.com/QwenLM/qwen-code/pull/5786) — feat(review): Route suggestion-level findings to an updatable PR comment** — Stops accumulating stale suggestion threads per review run. _(@pomelo-nwu)_

10. **[#5785](https://github.com/QwenLM/qwen-code/pull/5785) — perf(cli): Optimize serve daemon startup** — Deferred non-essential initialization to reach HTTP listener faster. _(@doudouOUC)_

## Feature Request Trends

- **Daemon-based architecture is the dominant direction**: Multiple requests ([#5768](https://github.com/QwenLM/qwen-code/issues/5768), [#5626](https://github.com/QwenLM/qwen-code/issues/5626)) and PRs ([#5785](https://github.com/QwenLM/qwen-code/pull/5785), [#5765](https://github.com/QwenLM/qwen-code/pull/5765)) push toward a persistent system service that hosts scheduled tasks, voice dictation, Chrome extension, and workspace control APIs.
- **Auto-update and lifecycle management**: PR [#5780](https://github.com/QwenLM/qwen-code/pull/5780) introduces `qwen update` + `/update` commands — the community clearly wants CLI-native upgrade workflows.
- **MCP resource read capability**: PR [#5781](https://github.com/QwenLM/qwen-code/pull/5781) and related discussion show strong interest in making MCP resources directly accessible to the LLM model without user-manual injection.
- **Status line defaults**: Issue [#5789](https://github.com/QwenLM/qwen-code/issues/5789) suggests enabling the status line preset by default for new users — a UX quality-of-life improvement.
- **Fallback vision model**: Issue [#5597](https://github.com/QwenLM/qwen-code/issues/5597) requests `/model --vision` to auto-fallback when the primary model lacks vision support.

## Developer Pain Points

- **Validation gaps across the board**: Over 20 issues from `@tt-a1i` in a single day reveal that fraction, negative, and `NaN` values pass through CLI flags, tool schemas, env var parsers, and LSP configuration — the codebase needs a systematic integer/string validation pattern.
- **Session/compatibility fragmentation**: The `modelId + baseUrl` vs `providerId + modelId` split between CLI, ACP, and VSCode (issue [#5758](https://github.com/QwenLM/qwen-code/issues/5758)) creates config friction — developers must implement protocol-specific mapping.
- **Configuration reliability**: Environment variable parsing (e.g., `Number()` for integer fields in [#5752](https://github.com/QwenLM/qwen-code/pull/5752)) silently accepts hex, scientific, and fractional inputs — causing subtle runtime misbehavior.
- **Prompt cache regressions**: Issue [#5736](https://github.com/QwenLM/qwen-code/issues/5736) suggests local LLM users experience increased full-prompt reprocessing after updates, hurting response time and token economy.
- **Tool parameter schema inconsistencies**: Several tool declarations advertise `number` in JSON schema but enforce `integer` at runtime ([#5698](https://github.com/QwenLM/qwen-code/issues/5698)), breaking LLM function calling when the model sends fractional arguments.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-24

## Today's Highlights

The project (now branded as **CodeWhale**) continues its intensive v0.8.65 "Fleet" architecture push, with 10+ PRs merged today spanning route resolution, Fleet worker execution, and TUI usability. A significant cluster of issues around provider/model routing separation and atomic route switching signals that the team is deep in a foundational refactor of how models and providers are selected, resolved, and cached. Community contributions picked up notably, with harvested PRs from @donglovejava improving provenance docs and approval modal UX, and a fast-closed contrast fix for `/model` and `/sessions` pickers.

## Releases

No new releases in the last 24 hours. The project remains at v0.8.71 (latest tagged version visible in issue labels).

---

## Hot Issues (10 Noteworthy)

### 1. [#2487 — Frequent error: "Turn stalled" with yolo mode](https://github.com/Hmbown/CodeWhale/issues/2487)
**Why it matters:** 17 comments, opened June 1 but still active. The "turn stalled" freeze is a longstanding reliability headache. Users in `yolo` mode lose all interactivity and `continue` doesn't recover. High-priority bug affecting daily workflows.

### 2. [#3144 — Add natural-language auto-review policy and pre-push gate](https://github.com/Hmbown/CodeWhale/issues/3144)
**Why it matters:** 12 comments, authored by Hmbown. Proposes a Cursor-inspired middle ground between manual approvals and full autonomy. Includes research signal from Cursor's SDK/review work. Signals the project's strategic direction toward safer autonomous agent execution.

### 3. [#3275 — CodeWhale over-extends scope with self-questioning loops](https://github.com/Hmbown/CodeWhale/issues/3275)
**Why it matters:** 11 comments, marked regression from #3061. Core UX complaint: the tool fails to follow user intent, instead entering self-driven proposal/execution loops. Community frustration is palpable — this undermines trust in autonomous mode.

### 4. [#3439 — Integrate GLM-5.2 as provider route fixture](https://github.com/Hmbown/CodeWhale/issues/3439)
**Why it matters:** 6 comments, opened June 23. Chinese community request (written in Chinese) for ZhiPu GLM-5.2 support, specifically for sub-agent tasks. The author has already mapped `model_strength` for the GLM family in existing Constitution config — low friction to accept.

### 5. [#3384 — Resolve every provider/model switch through ReadyRouteCandidate](https://github.com/Hmbown/CodeWhale/issues/3384)
**Why it matters:** 5 comments, authored by Hmbown. Makes provider/model switching atomic: TUI, slash commands, fallback, picker — all must resolve a complete route candidate before mutating state. This is the safety rail for multi-provider routing.

### 6. [#3385 — Provider-owned live catalogs and secret-free model cache](https://github.com/Hmbown/CodeWhale/issues/3385)
**Why it matters:** 5 comments. Addresses the pain of hardcoded model lists. Live `/models` endpoints feed provider-scoped wire IDs into a cache that doesn't store API keys. Enables hosted aggregators and local runtimes to self-register.

### 7. [#3461 — MCP duplicate server instance lifecycle](https://github.com/Hmbown/CodeWhale/issues/3461)
**Why it matters:** 4 comments, opened June 23. A single `mcp.json` entry spawns two MCP processes — one orphaned, wasting 4MB RAM and sharing stdio. Killing either kills both. Fresh bug with immediate resource/cleanup impact.

### 8. [#3474 — /model /sessions popup extremely low text contrast (macOS)](https://github.com/Hmbown/CodeWhale/issues/3474)
**Why it matters:** CLOSED within 24 hours of being filed. Contrast bug on macOS terminal — `/config` works fine, `/model` and `/sessions` don't. Implicated `tui::text::Line` styling. Fastest turn-around in this digest. Fixed by PR #3500.

### 9. [#2492 — No cross-session memory](https://github.com/Hmbown/CodeWhale/issues/2492)
**Why it matters:** 5 comments, opened June 1. User complaint that restarting loses all session memory; forced memory writes aren't read on restart. "Good response speed, but poor overall experience." A foundational UX gap for long-running projects.

### 10. [#2666 — Agents need visible token/resource usage during long tasks](https://github.com/Hmbown/CodeWhale/issues/2666)
**Why it matters:** 3 comments, authored by Hmbown. From agent harness testing: agents have no visibility into token budget, context pressure, elapsed time, child-agent status, or cost. Critical for trust in autonomous multi-agent workflows.

---

## Key PR Progress (10 Important PRs)

### 1. [#3524 — fix(tui): make MCP connection drops explicit](https://github.com/Hmbown/CodeWhale/pull/3524)
**What:** Centralizes MCP connection teardown through lifecycle helpers that log why connections drop. Adds reload regression test asserting live transports are dropped on config changes. 💡 Directly addresses the duplicate MCP server issue (#3461).

### 2. [#3523 — feat(tui): feed route limits into context budgets](https://github.com/Hmbown/CodeWhale/pull/3523)
**What:** New `route_budget` adapter drives context windows, output caps, compaction thresholds, and visible pressure readouts from resolved `RouteLimits`. Threads through `App`, `EngineConfig`, `SetModel`, provider switches, and `/model`. 🎯 Enables token/resource visibility (#2666).

### 3. [#3521 — feat(route): gate runtime switches on RouteResolver](https://github.com/Hmbown/CodeWhale/pull/3521)
**What:** (CLOSED) Adds a TUI runtime-route adapter around `RouteResolver` so provider/model choices produce a `ReadyRouteCandidate` before state mutation. Routes `/provider`, model picker, slash `/model`, provider fallback, and engine activation through this gate. 🧱 Implements #3384.

### 4. [#3519 — feat(tui): mouse-wheel scrolling for pickers + type-ahead](https://github.com/Hmbown/CodeWhale/pull/3519)
**What:** (CLOSED) Adds two most-requested picker behaviors: mouse-wheel scrolling (provider, help, session, command palette, theme pickers) and type-ahead filter that catches `Z → Z.ai` instead of requiring `z`. ☑️ UX polish for modal navigation.

### 5. [#3520 — feat(fleet): expose worker runtime through Runtime API](https://github.com/Hmbown/CodeWhale/pull/3520)
**What:** (CLOSED) Attaches Runtime API Fleet managers to the shared sub-agent manager. Threads configured `[fleet.exec]` policy through. Exposes `worker_runtime` capability and Fleet worker state in API JSON. 🏗️ Building the Fleet execution substrate.

### 6. [#3518 — feat(fleet): resolve agent profiles into worker runtime](https://github.com/Hmbown/CodeWhale/pull/3518)
**What:** (CLOSED) Resolves `agent_profile` references against workspace `.codewhale/agents` profiles. Composes profile instructions into sub-agent specs and `codewhale exec` subprocess prompts. Maps Fleet role/loadout intent into existing `AgentWorkerSpec`. 🧩 Connects profiles to execution.

### 7. [#3516 — feat(tui): add Fleet setup loadout view](https://github.com/Hmbown/CodeWhale/pull/3516)
**What:** (CLOSED) New `/fleet` TUI view — left-to-right lanes for role, profile, loadout, and policy/recursion. Surfaces provider/model route, sub-agent concurrency, Fleet exec recursion depth, token/timeout policy, and `.codewhale/agents` profile location. 📊 Fleet management UI.

### 8. [#3513 — feat(fleet): load workspace agent profiles](https://github.com/Hmbown/CodeWhale/pull/3513)
**What:** (CLOSED) Discovers `.codewhale/agents/*.toml` profiles, normalizes into `FleetProfile` vocabulary, and rejects hidden provider/model policy fields. 🛡️ Security boundary: prevents profiles from expanding permissions.

### 9. [#3511 — test(tui): add Fleet manager smoke proof](https://github.com/Hmbown/CodeWhale/pull/3511)
**What:** (CLOSED) CI-safe smoke test driving real Fleet manager/executor/ledger bridge. Creates 10 deterministic local tasks across `scout`, `builder`, `verifier` roles, schedules through 3 concurrent workers, verifies all complete. ✅ E2E proof for Fleet architecture (#3166).

### 10. [#3500 — fix(tui): harden picker selection contrast](https://github.com/Hmbown/CodeWhale/pull/3500)
**What:** (CLOSED) Fixes the low-contrast `/model` and `/sessions` picker selection on macOS (#3474). Styles selected-row marker/spacing with muted selection colors, adds render-buffer regression tests. ⚡️ Turned around in <24 hours from bug report.

---

## Feature Request Trends

1. **Fleet Architecture & Multi-Provider Routing (dominant trend)**: ~20 issues/PRs. The v0.8.65 push to separate provider facts, model facts, offerings, and route resolution. Key themes: atomic route switching (#3384), provider-owned live catalogs (#3385), capability-aware fallback chains (#2574), and cross-provider model search (#3075).

2. **Autonomous Agent Safety**: Review gates (#3144), user-defined personas/role policies (#3367), pre-push review (#3144), and the "over-extension" regression (#3275) all point to a need for safe, predictable autonomous execution.

3. **Chinese/Local Model Provider Integration**: GLM-5.2 support (#3439) mirrors earlier requests for vLLM, Ollama, and other local endpoints. Community wants provider-agnostic routing that works with domestic Chinese models.

4. **Visual & Telemetry Improvements**: Token/resource usage visibility (#2666), visual inspection artifacts for browser/UI tasks (#3145), and config editability from TUI (#3303) — users want more insight and control mid-session.

5. **Memory & Context Continuity**: Cross-session memory (#2492) and route budget/context pressure display (#3523) — agents lose state between sessions and lack awareness of resource limits during long tasks.

---

## Developer Pain Points

- **"Turn stalled" freeze (#2487)**: The most-commented issue remains open after 3 weeks. yolo mode users hit an unrecoverable stall that doesn't respond to `continue`. High visibility, no fix yet.

- **Scope creep / agent over-extension (#3275)**: Marked regression from a previous fix. Agents enter self-questioning loops, ignoring user intent. This is the #1 trust-breaker in autonomous mode.

- **Low contrast / TUI rendering bugs on macOS (#3474)**: Even though fixed quickly, the frequency of cross-platform rendering issues (Windows freeze #1812 still open; macOS contrast) suggests terminal compatibility testing is insufficient.

- **MCP server lifecycle bugs (#3461)**: Duplicate MCP processes, orphaned processes wasting 4MB RAM, shared stdio causing double-kill. In MCP-centric workflows, this is a reliability blocker.

- **No cross-session memory (#2492)**: Fundamental UX gap. Restarting the tool resets all context — users feel the tool "forgets" everything. The project's agent/autonomy ambitions are undermined without persistent memory.

- **Configuration discoverability (#3303)**: Users can't find, edit, and persist documented config knobs from the TUI. Important runtime behaviors feel hardcoded even when config model supports them.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*