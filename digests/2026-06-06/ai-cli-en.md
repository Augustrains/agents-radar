# AI CLI Tools Community Digest 2026-06-06

> Generated: 2026-06-06 08:20 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date:** 2026-06-06

---

## 1. Ecosystem Overview

The AI CLI tool landscape is experiencing a phase of rapid maturation and community-driven feature expansion, with six major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code, OpenCode, Pi, Qwen Code, and DeepSeek TUI (CodeWhale)—all actively releasing patches and engaging with vocal user bases. A clear trend toward **cross-platform standardization** (notably `AGENTS.md`), **multi-model resilience**, and **persistent memory/state** across sessions unifies otherwise divergent roadmaps. Meanwhile, infrastructure pain points such as Windows second-class support, context compaction amnesia, and escalating API costs are recurring friction themes across nearly every project. The ecosystem is bifurcating between tools doubling down on **pair-programming assistant** UX and those pivoting toward **autonomous orchestrator** architectures.

---

## 2. Activity Comparison

| Tool | Open Issues (Hot) | PRs Today | Release Status | Community Velocity |
|---|---|---|---|---|
| **Claude Code** | 10 hot issues (4k+ upvotes on #6235) | 5 PRs | v2.1.167 patch; 2 releases this week | Very high; dominant community voice |
| **OpenAI Codex** | 10 hot issues (46 👍 #20500) | 10 PRs | 3 alpha releases (Rust/V8) | High; active infrastructure hardening |
| **Gemini CLI** | 10 hot issues (#21409 P1 hang) | 10 PRs | 2 patches (v0.46.0-preview.2, v0.45.2) | Medium; steady but fewer extreme spikes |
| **GitHub Copilot CLI** | 10 hot issues (#3700 WSL2 regression) | 0 PRs today | v1.0.60 (triggering regressions) | Medium; high severity regressions |
| **Kimi Code** | 10 issues (1 new today) | 5 PRs | v1.47.0 (migration-focused) | Medium-low; ecosystem transitioning |
| **OpenCode** | 10 hot issues (#27530 startup blocker) | 10 PRs | v1.16.2 (bugfix) | Medium; feature-rich but server issues |
| **Pi** | 10 hot issues (#4945 freeze bug) | 10 PRs | No new release (v0.75.5 latest) | High; intense 24h activity, 30+ issues |
| **Qwen Code** | 10 hot issues (#4815 OOM crash) | 10 PRs | v0.17.1-nightly | Very high; daemon-mode feature batch |
| **DeepSeek TUI (CodeWhale)** | 10 hot issues (#2580 VS Code integration) | 10 PRs | No release (v0.9.0 prep) | High; release-blocker activity |

---

## 3. Shared Feature Directions

### 3.1 Persistent Memory / State Across Compactions
- **Claude Code** (#34556, #47023): Users building bespoke 3-tier markdown systems; 59 compactions tracked by one user.
- **Gemini CLI** (#26522, #26525): Auto Memory retries low-signal sessions indefinitely; secrets leak before redaction.
- **Pi** (#5420): Auto-compaction crashes when conversation ends on assistant message — lack of valid compaction state.
- **DeepSeek TUI** (#2838): Dormant hard compaction planner that summarizes middle history while preserving system prompt.

### 3.2 Multi-Provider & Custom Model Flexibility
- **Claude Code**: `fallbackModel` (up to 3 fallbacks) just shipped in v2.1.166.
- **OpenAI Codex** (#10867, 33👍): Custom model providers in the app; CLI supports but app ignores.
- **Gemini CLI**: Vertex AI model detection fix (#27375); gateway auth rejected with custom `GOOGLE_GEMINI_BASE_URL`.
- **Qwen Code** (#3384, #4813): Unable to add OpenAI-compatible local LLMs; shared `baseUrl` duplication.
- **DeepSeek TUI** (#2574): Provider fallback chain for automatic failover on 401/429/5xx errors.
- **Pi** (#5262): Anthropic Vertex provider PR adding built-in `anthropic-vertex`.

### 3.3 Autonomous Agent / Orchestrator Mode
- **Claude Code** (#56913): Tiered Opus brains + Sonnet workers for long-lived autonomous orchestration.
- **Gemini CLI** (#21409, #22323): Subagent hangs and false GOAL success — unreliable subagent orchestration.
- **Qwen Code** (#4780): `/fork` background-agent command for parallel non-blocking tasks.
- **Kimi Code**: RalphFlow architecture (PR #1960) with ephemeral context and convergence detection to prevent infinite loops.
- **DeepSeek TUI**: WhaleFlow Starlark authoring (#2670) — model-authored workflows compiled to IR.

### 3.4 VS Code / IDE Integration
- **DeepSeek TUI** (#2580, #1584): VS Code Agent View adaptation is the #1 community demand.
- **Claude Code**: Desktop ↔ VS Code session sync gaps; `/desktop` command failures.
- **OpenAI Codex** (#25319): Scope VS Code chats to current workspace — cross-project chat pollution.
- **Kimi Code**: Transition toward `kimi-code` standalone binary with IDE integration.

### 3.5 Declarative Agent Definitions
- **Claude Code**: `AGENTS.md` standard (#6235, 4k+ upvotes) — write once, run on any agent.
- **Qwen Code** (#4821): Frontmatter YAML in `.qwen/agents/*.md` files.
- **OpenCode**: Plugin event hooks (#31051) for session lifecycle reactions.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|---|---|---|---|---|---|---|---|---|---|
| **Primary Use Case** | Pair programming + autonomous orchestration | Multi-provider frontend with sandbox | Long-running agent orchestration | Git-integrated assistant | Migration to standalone binary | Extensible provider ecosystem | Experimental self-evolution | Daemon/web-shell architecture | Workflow automation (WhaleFlow) |
| **Target User** | Power developers, enterprise | Multi-tool power users | Cloud-native developers | GitHub-centric developers | Existing Kimi ecosystem users | Self-hosters, multi-provider | Experimental/advanced users | Local LLM enthusiasts | Workflow engineers |
| **Architecture** | CLI-first, plugin hooks | Rust+V8 sandbox, TUI | Preview-track, subagent-based | VS Code integration | Python→Node migration | Server+CLI, provider abstraction | Extension-based, 5D memory | Daemon+HTTP API, web-shell | Starlark-compiled IR |
| **Security Posture** | Deny rules, glob patterns | Guardian prompts, OAuth hardening | Auto Memory redaction (flawed) | Parallel session permission corruption | Migration uncertainty | Local LAN discovery | Token validation | Self-modification hardening | TLS skip-verify (optional) |
| **Unique Strength** | Largest community, `AGENTS.md` push | Provider flexibility | Model infrastructure (3.1 Flash Lite) | Git-native, slash commands | RalphFlow convergence detection | FFF search tools | 5D gene/genome memory | Session branching API | Teacher-harness promotion |
| **Unique Weakness** | Context compaction amnesia | Windows second-class | Subagent reliability | Alt-screen, clipboard issues | Migration confusion | Startup server errors | Undici timeouts, freeze bugs | OOM crashes | IDE integration gap |

---

## 5. Community Momentum & Maturity

### Most Active Communities (by Issue Velocity)
1. **Claude Code** — 4k+ upvotes on single issue (#6235); 59 compactions tracked; highest sustained engagement.
2. **Qwen Code** — 386 files changed in daemon-mode PR; OOM crash reports spanning 9 months; very high PR throughput.
3. **Pi** — 30+ issues updated in 24h; 28👍 on freeze bug; high-velocity development period.
4. **DeepSeek TUI** — 10+ PRs from maintainer today; active v0.9.0 preparation with release acceptance matrix.

### Most Rapidly Iterating (by Release Cadence)
1. **OpenAI Codex** — 3 alpha releases in 24h (Rust/V8 bumps); 10 PRs today.
2. **Claude Code** — v2.1.167 and v2.1.166 this week; feature-rich patches.
3. **Gemini CLI** — v0.46.0-preview.2 and v0.45.2; critical regression fix.
4. **GitHub Copilot CLI** — v1.0.60; but high regression risk.

### Maturity Assessment
- **Established (production-grade):** Claude Code, GitHub Copilot CLI, OpenAI Codex
- **Growing (active development):** Gemini CLI, Qwen Code, OpenCode
- **Emerging (experimental/preview):** Kimi Code (transitioning), Pi (self-evolver), DeepSeek TUI (pre-v0.9.0)

---

## 6. Trend Signals

### 6.1 Cross-Platform Standardization Pressure
The 4k+ upvotes on `AGENTS.md` (#6235) signal that developers are **tired of tool-specific configuration files**. They want a write-once-run-anywhere agent instructions file that works across Claude Code, Codex, Amp, and Cursor. This is the strongest community signal in the entire ecosystem today.

### 6.2 Persistent Memory as the Next Frontier
Every major tool has at least one open issue about memory surviving context compaction. Solutions range from user-built 3-tier markdown (Claude Code) to Gemini's Auto Memory (with security flaws) to Pi's 5D gene/genome. **Built-in persistent state** is the #1 feature gap across the ecosystem — whoever ships it first and securely will have a powerful differentiator.

### 6.3 Autonomous Orchestrator > Pair Programming Buddy
The community is increasingly asking agents to **operate independently** — forking background tasks (Qwen Code), running tiered model architectures (Claude Code), and authoring workflows in safe DSLs (DeepSeek TUI WhaleFlow). The "agent as assistant" paradigm is giving way to "agent as autonomous teammate."

### 6.4 Cost Control Becomes Critical
1M context windows caused bill shock across tools. Users want granular caps (`--max-context`), plan-level usage visibility, and model selection guardrails. The **DeepSeek V4 Pro 75% price cut** (#28846) triggered immediate demands for plan limit adjustments — cost efficiency is now a competitive dimension.

### 6.5 Windows Community Growing Impatient
Windows issues dominate the top complaints for OpenAI Codex (4 of top 10), GitHub Copilot CLI (WSL2 regression), and Kimi Code (WebSocket daemon broken). The **Windows developer audience is underserved** and increasingly vocal — this is a market opportunity for tools that invest in native Windows support.

### 6.6 Security & Trust Erosion
- Gemini CLI's Auto Memory **leaks secrets into model context before redaction** (#26525).
- GitHub Copilot CLI's **parallel session permission corruption** (#3563) undermines trust in persisted approvals.
- OpenCode's **server errors on startup** (#27530) block all providers.
- Qwen Code's **stale CI merges** (#4805) risk production regressions.

Security hardening is no longer optional — it's table stakes for enterprise adoption.

### 6.7 Multi-Provider is the New Normal
The loudest feature request across OpenAI Codex (#10867, 33👍), Qwen Code (#3384), and DeepSeek TUI (#2574) is **custom model provider support**. Developers want a single CLI frontend that can switch between OpenAI, Anthropic, Google, local LLMs, and third-party providers without friction. The "one model to rule them all" era is over.

---

**Summary for Decision-Makers:**
- **For enterprise adoption:** Claude Code leads on community scale and feature maturity; invest in `AGENTS.md` compatibility and persistent memory.
- **For multi-provider workflows:** OpenAI Codex or OpenCode — the former has stronger sandbox security, the latter better local LLM support.
- **For autonomous agent workflows:** Qwen Code (session branching, fork command) or DeepSeek TUI (WhaleFlow Starlark) — both in active development but delivering on the orchestrator vision.
- **For GitHub-centric teams:** GitHub Copilot CLI is tightening but regressions (WSL2, MCP spawning) need attention; watch for alt-screen fix.
- **Windows developers:** Unsatisfied across the board — consider OpenCode or Claude Code (which has fewer Windows-specific blocker bugs).
- **Cost-sensitive teams:** Monitor DeepSeek V4 Pro price cuts; demand `--max-context` flags and plan-level visibility from all tools.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data: github.com/anthropics/skills | Snapshot: 2026-06-06*

---

## 1. Top Skills Ranking

| # | Skill PR | Functionality | Status | Key Discussion Points |
|---|----------|---------------|--------|----------------------|
| 1 | **[Add document-typography skill](https://github.com/anthropics/skills/pull/514)** | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents | **Open** (Mar 2026) | Core UX problem affecting every Claude document output; high community resonance |
| 2 | **[Add ODT skill](https://github.com/anthropics/skills/pull/486)** | OpenDocument text creation, template filling, and ODT-to-HTML conversion | **Open** (Mar 2026) | Demand for LibreOffice/OASIS standard file format support; niche but technically deep |
| 3 | **[Improve frontend-design skill](https://github.com/anthropics/skills/pull/210)** | Revises frontend-design for clarity, actionability, and single-conversation execution | **Open** (Jan 2026) | Long-running quality improvement; focus on specificity and internal coherence |
| 4 | **[Add skill-quality-analyzer and skill-security-analyzer](https://github.com/anthropics/skills/pull/83)** | Meta-skills evaluating Skills across 5 dimensions (structure, documentation, security) | **Open** (Nov 2025) | Foundational quality assurance for the entire ecosystem; meta-tooling demand |
| 5 | **[Fix PDF case-sensitive file references](https://github.com/anthropics/skills/pull/538)** | Corrects 8 case-sensitivity mismatches in PDF skill's SKILL.md | **Open** (Mar 2026) | Cross-platform compatibility (Linux/macOS vs Windows); low-complexity but blocking |
| 6 | **[Fix skill-creator YAML validation](https://github.com/anthropics/skills/pull/539)** | Pre-parse validation for unquoted description fields containing `:` | **Open** (Mar 2026) | Prevents silent YAML parsing failures; developer ergonomics |
| 7 | **[Fix DOCX tracked change ID collision](https://github.com/anthropics/skills/pull/541)** | Prevents document corruption when w:id collides with existing bookmarks | **Open** (Mar 2026) | OOXML technical depth; hardcoded low IDs caused real-world corruption |
| 8 | **[Add SAP-RPT-1-OSS predictor](https://github.com/anthropics/skills/pull/181)** | Wraps SAP's open-source tabular foundation model for predictive analytics | **Open** (Dec 2025) | Enterprise ML integration; SAP TechEd 2025 release |

---

## 2. Community Demand Trends

The most-anticipated new Skill directions from Issues (ranked by comment volume):

| Direction | Representative Issue | Signal |
|-----------|---------------------|--------|
| **Org-wide skill sharing** | [#228: Enable org-wide skill sharing](https://github.com/anthropics/skills/issues/228) (13 comments, 7 👍) | Highest-discussed Issue; users want shared skill libraries and direct sharing links within organizations |
| **Evaluation/trigger reliability** | [#556: run_eval.py 0% trigger rate](https://github.com/anthropics/skills/issues/556) (11 comments, 6 👍) | Second-highest; evaluation pipelines are broken on basic functionality, blocking skill optimization |
| **Skill persistence/recovery** | [#62: All skills disappeared](https://github.com/anthropics/skills/issues/62) (10 comments) | Data loss anxiety; skill files missing after rename/upload operations |
| **Skill-creator best practices** | [#202: Skill-creator should be updated](https://github.com/anthropics/skills/issues/202) (8 comments) | Demand for operational, token-efficient skill instruction format vs. verbose documentation |
| **Trust boundary security** | [#492: Community skills under anthropic/ namespace](https://github.com/anthropics/skills/issues/492) (7 comments) | Trust boundary vulnerability; users may grant elevated permissions to impersonated official skills |
| **Deduplication** | [#189: document-skills and example-skills install duplicates](https://github.com/anthropics/skills/issues/189) (6 comments, 8 👍) | Most-upvoted issue; duplicate skills waste context window and confuse users |
| **MCP/Skills integration** | [#16: Expose Skills as MCPs](https://github.com/anthropics/skills/issues/16) (4 comments) | Long-standing request to bridge Skills and MCP protocols |
| **Agent governance** | [#412: agent-governance skill proposal](https://github.com/anthropics/skills/issues/412) (4 comments) | Safety patterns for AI agent systems — policy enforcement, threat detection, audit trails |

**Emerging trend**: The community is moving from individual skill creation toward **ecosystem infrastructure** — skill sharing, security boundaries, evaluation pipelines, deduplication, and MCP integration. Pure content skills are stable; tooling skills are accelerating.

---

## 3. High-Potential Pending Skills

Active open PRs with sustained discussion and contributor momentum:

| Skill PR | Status | Last Activity | Why It May Land Soon |
|----------|--------|---------------|----------------------|
| **[agent-creator skill + multi-tool evaluation fix](https://github.com/anthropics/skills/pull/1140)** | **Open** | 2026-06-02 | Addresses Issue #1120 directly; includes Windows support and evaluation stability fixes |
| **[Windows subprocess/encoding fixes for skill-creator](https://github.com/anthropics/skills/pull/1050)** | **Open** | 2026-05-24 | Two 1-line fixes enabling Windows compatibility; low-risk, high-impact |
| **[Windows subprocess pipe crash fix](https://github.com/anthropics/skills/pull/1099)** | **Open** | 2026-05-24 | `run_eval.py` is completely broken on Windows; fix is straightforward |
| **[testing-patterns skill](https://github.com/anthropics/skills/pull/723)** | **Open** | 2026-04-21 | Comprehensive testing stack coverage (unit, React, integration); aligned with quality trend |
| **[ServiceNow platform skill](https://github.com/anthropics/skills/pull/568)** | **Open** | 2026-04-23 | Broad enterprise platform coverage; sustained contributor activity |
| **[AURELION skill suite (kernel, advisor, agent, memory)](https://github.com/anthropics/skills/pull/444)** | **Open** | 2026-05-06 | Four-skill cognitive/memory framework; structured professional knowledge management |
| **[n8n-builder + n8n-debugger + faf-expert](https://github.com/anthropics/skills/pull/190)** | **Open** | 2026-05-18 | Four production-tested community skills; long-standing PR with repeated updates |
| **[feature-dev workflow fix for TodoWrite overwrite](https://github.com/anthropics/skills/pull/363)** | **Open** | 2026-06-03 | Fixes critical workflow bug (phases 6-7 skipped); recent update with continued discussion |

**Key insight**: Windows compatibility fixes dominate recent activity (3 PRs in top pending). The `feature-dev` and `agent-creator` PRs are the most actively discussed at time of snapshot (2026-06-06).

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is shifting from individual skill content toward ecosystem infrastructure — evaluation reliability (0% trigger rates), Windows compatibility, security trust boundaries, skill deduplication, and organizational sharing — as the Skills ecosystem matures past novelty into production-grade adoption.**

---

# Claude Code Community Digest — 2026-06-06

## Today's Highlights

Two patch releases rolled out, including a significant new `fallbackModel` configuration for multi-model resilience and glob-pattern support in deny rules. The community remains intensely focused on persistent memory across context compactions (now with 59 documented compactions by a single user), while the `AGENTS.md` standardization proposal (#6235) continues to dominate with 4,068 upvotes and 313 comments. Escalating cost-concern issues around 1M context windows and rate limiting emerged as fresh pain points.

## Releases

**v2.1.167** — Bug fixes and reliability improvements.

**v2.1.166** — Two notable additions:
- `fallbackModel` setting: configure up to three fallback models tried in order when the primary model is overloaded or unavailable. The `--fallback-model` flag now applies to interactive sessions as well.
- Glob pattern support in deny rule tool-name position: `"*"` denies all tools, enabling more expressive security policies.

[Compare releases](https://github.com/anthropics/claude-code/releases)

---

## Hot Issues

1. **[#6235 — Support AGENTS.md](https://github.com/anthropics/claude-code/issues/6235)** 🔥
   *4,068 upvotes, 313 comments. Enhancement request for Claude Code to read `AGENTS.md`, a cross-platform standard emerging across Codex, Amp, and Cursor. CLAUDE.md is seen as too Anthropic-specific — this is the community’s most-wanted compatibility feature.*

2. **[#63060 — API Error: Usage credits required for 1M context](https://github.com/anthropics/claude-code/issues/63060)**
   *23 upvotes, 73 comments. Users hitting "Usage credits required" errors when attempting 1M context sessions. Duplicate reports suggest this is a widespread billing/entitlement issue on macOS. High frustration in comments around silent failures.*

3. **[#34556 — Persistent Memory Across Context Compactions](https://github.com/anthropics/claude-code/issues/34556)**
   *3 upvotes, 41 comments. A user who endured 59 compactions over 26 days built their own memory persistence system. The core plea: Claude Code has zero built-in memory between context compactions, forcing external solutions.*

4. **[#53915 — Server limiting requests (not your usage limit)](https://github.com/anthropics/claude-code/issues/53915)**
   *9 upvotes, 36 comments. Windows + VS Code users reporting "Server is temporarily limiting requests" errors — distinct from personal rate limits. Particularly painful for CI and automated workflows.*

5. **[#34650 — Add --max-context flag](https://github.com/anthropics/claude-code/issues/34650)** *(CLOSED)*
   *24 upvotes, 13 comments. Opus 4.6’s 1M context upgrade caused 5x API burn. Community wants a `--max-context` cap. Closed status without clear resolution is notable — cost management remains a live issue.*

6. **[#56913 — Tiered Opus brains + Sonnet workers + persistent state](https://github.com/anthropics/claude-code/issues/56913)**
   *0 upvotes, 24 comments. Deep proposal for running Claude Code as a long-lived autonomous orchestrator — not a pair-programming buddy — using tiered models for cost efficiency. Reflects growing "agent-as-orchestrator" trend.*

7. **[#9001 — Scroll regression in 2.0.8](https://github.com/anthropics/claude-code/issues/9001)**
   *28 upvotes, 20 comments. Terminal scroll regression that has persisted since October 2025. Users can only view last ~20 lines. 8-month-old bug still open — a longstanding UX pain.*

8. **[#12676 — Video Input Support](https://github.com/anthropics/claude-code/issues/12676)**
   *41 upvotes, 16 comments. Request to add video input support in Claude Code, reflecting broader multimodal expectations from the developer community.*

9. **[#63456 — Opus 4.8 not selectable in CLI /model](https://github.com/anthropics/claude-code/issues/63456)**
   *11 upvotes, 18 comments. CLI `/model` picker only shows up to Opus 4.6 despite user accounts having Opus 4.8. Mismatch between web and CLI availability — undermines model flexibility promises.*

10. **[#47023 — Expose compact/session lifecycle hooks for external memory](https://github.com/anthropics/claude-code/issues/47023)**
    *3 upvotes, 19 comments. Proposal to expose lifecycle hooks so the community doesn't have to re-invent transcript interception. References 5 related open issues. Formal request for the hook API that would unblock #34556 and others.*

---

## Key PR Progress

1. **[#61584 — Workload identity federation for CI auth](https://github.com/anthropics/claude-code/pull/61584)** *(CLOSED)*
   *Replaces static `ANTHROPIC_API_KEY` in CI workflows with OIDC-based Workload Identity Federation — short-lived tokens instead of long-lived secrets. Directly addresses #53915-style auth friction in CI.*

2. **[#65619 — Fix plugin author metadata alignment](https://github.com/anthropics/claude-code/pull/65619)**
   *Fixes malformed `plugin.json` where two authors were packed into single fields. UI rendering fix for the plugin marketplace. Community contributor fix for #61785.*

3. **[#65666 — Fix dev container issues](https://github.com/anthropics/claude-code/pull/65666)**
   *Removes DNS-borking domains from devcontainer firewall config and adds env-based mechanism for ANTHROPIC_API_KEY injection. Lowers onboarding friction for contributors.*

4. **[#58673 — WIP / testing PR](https://github.com/anthropics/claude-code/pull/58673)**
   *Minimal PR with description "s". Low signal, included for completeness of open PRs.*

5. **[#65723 — Subscription debate chat rx ewi](https://github.com/anthropics/claude-code/pull/65723)**
   *Title suggests a Claude subscription/chat experiment. No description. Low signal.*

---

## Feature Request Trends

**1. Cross-Platform Standardization (AGENTS.md)**
The dominant signal (#6235, 4k+ upvotes). The community wants Claude Code to adopt the emerging `AGENTS.md` standard being embraced by Codex, Amp, and Cursor — rather than forcing `CLAUDE.md`. This is a "write once, run on any agent" expectation.

**2. Persistent Memory / State Across Sessions**
Multiple issues (#34556, #47023, #14227, #32627, #34192, #46138) all cry for memory that survives compaction. Users are building bespoke solutions (3-tier markdown, knowledge graphs). The ask is not just hooks — it's *built-in* persistent state.

**3. Autonomous Agent Architecture**
#56913 crystallizes a trend: developers want Claude Code to operate as a long-lived autonomous agent — orchestrating pipelines, builds, monitoring — using tiered models (Opus for reasoning, Sonnet for execution). This is a step beyond "pair programming buddy."

**4. Cost Control Mechanisms**
- `--max-context` flag (#34650)
- Model-level cost caps (#65809: "Users should pay for results, not internal reasoning inefficiency")
- Plan-level usage in status line (#22221)
- 1M context credit requirements (#63060) — cost management is top-of-mind as context windows grow.

**5. Multimodal Input**
- Video input (#12676, 41 👍)
- Semantic file attachment via hooks (#65825)
- Rich media support across CLI and Desktop.

**6. Desktop ↔ IDE ↔ CLI Session Sync**
Multiple threads (#65674, #65554, #64191, #62017, #49545) about session portability gaps between Desktop app, VS Code/Cursor extension, and CLI. `/desktop` command failures are a recurring theme.

**7. Security Defaults**
- Default deny for `.env` files (#65816)
- Glob-pattern deny rules (just shipped in v2.1.166) — community wants stronger out-of-box security posture.

---

## Developer Pain Points

**🔴 Context Compaction Amnesia (Highest Friction)**
The #1 developer pain point. After even a single compaction, Claude Code forgets everything not externally saved. Users building workarounds, tracking 59+ compactions — this is blocking long-running agent use cases.

**🔴 Escalating API Costs**
1M context windows caused "bill shock." Users want granular caps (`--max-context`), model selection guardrails, and plan-level visibility. "Usage credits required" errors (#63060) on legitimate 1M usage suggests entitlement/billing bugs compounding the problem.

**🔴 Desktop App Reliability**
Desktop ↔ CLI session transfer often fails (`/desktop` transcript not found, wrong working directory restored across worktrees, "desktop appears offline" persisting for weeks). Claude Dispatch (cowork mode) connectivity seems fragile on both macOS and Windows.

**🔴 Rate Limiting Confusion**
#53915 highlights opaque "server is temporarily limiting requests" errors — distinct from personal limits but indistinguishable to users. Worsened when using fallback models that then rate-limit faster.

**🔴 Model Selectivity Gaps**
#63456: Opus 4.8 available on web but not in CLI `/model` picker. Users feel they can't access models they're paying for.

**🔴 Scroll Regression (#9001)**
Eight-month-old bug where long conversations are unreviewable in terminal mode. Low priority but high frustration — a fundamental UX regression that should be a critical fix.

**🔴 Windows Experience**
Flash/broken conhost windows (#58606), sidebar disappearing (#60003), WSL network sandbox intermittency (#62743) — Windows remains a second-class platform.

**🔴 `advisor()` Post-Compaction Breaks**
Even after six duplicate reports (#60523), `advisor()` breaks sessions post-compaction due to `parentUuid` tree mismatch. Users feel ignored — "zero human resolution or fix."

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**OpenAI Codex Community Digest – 2026-06-06**

---

### 1. Today's Highlights

A significant community backlash is forming around Windows sandbox and WSL2 performance, with the highest-traffic issue (#25715) showing 32 comments in just five days. Meanwhile, OpenAI is actively shipping infrastructure hardening: key PRs landed today fixing deadlocks in the TUI event loop (#26754) and securing the remote-control enrollment pathway against false 404s (#26741). On the feature frontier, 46 community members are now demanding multi-account support (#20500), signaling a clear pivot toward enterprise-grade identity management.

---

### 2. Releases

Three releases shipped in the last 24 hours, primarily iterative Rust and V8 upgrades:

- **`rust-v0.138.0-alpha.6`** (Jun 6): Alpha release targeting the Rust core layer; no detailed changelog.
- **`rusty-v8-v149.2.0`** (Jun 6): Updated V8 bindings for the Rust sandbox runtime.
- **`rust-v0.138.0-alpha.5`** (Jun 5): Previous alpha release for Rust core.

All three are dependency-level bumps with no user-facing feature changes documented.

---

### 3. Hot Issues (10 Noteworthy)

1. **#25715 – Codex App Unusable Slow with WSL** (32 comments, 30 👍)  
   [Link](https://github.com/openai/codex/issues/25715)  
   A ChatGPT Pro user reports routine operations "taking minutes" when Codex uses WSL2 as its agent environment. The top-voted Windows performance complaint; suggests native Windows agent support is badly needed.

2. **#24391 – Windows sandbox spawn fails on CLI 0.133.0** (31 comments, 23 👍)  
   [Link](https://github.com/openai/codex/issues/24391)  
   CLI sandbox setup refresh breaks post-update. Reproducible on npm global install; blocking many Windows CLI users.

3. **#24990 – ChatGPT login flow fails for paid subscribers** (21 comments, 15 👍)  
   [Link](https://openai/codex/issues/24990)  
   Plus users are redirected to phone-verification instead of the advertised login flow. Auth routing bug affecting new onboarding.

4. **#17392 – Remote compaction fails with "stream disconnected"** (18 comments, 6 👍)  
   [Link](https://github.com/openai/codex/issues/17392)  
   Intermittent failure on macOS during remote context compaction. Long-standing bug (April) with no fix in sight; high impact for Pro users with large contexts.

5. **#10867 – Support custom model providers in the app** (14 comments, 33 👍)  
   [Link](https://github.com/openai/codex/issues/10867)  
   CLI `/model` switching works, but the app ignores custom providers. The top-voted enhancement request after multi-account; users want local-first model freedom.

6. **#24438 – Computer Use disabled for individual accounts in Central Asia** (11 comments, 1 👍)  
   [Link](https://github.com/openai/codex/issues/24438)  
   Geographic restriction on Computer Use features for non-org accounts; raises parity concerns across regions.

7. **#20500 – Multi-account support per connector** (10 comments, 46 👍)  
   [Link](https://github.com/openai/codex/issues/20500)  
   Strongest community demand of the week: users want separate authorized identities within one Codex session for privacy/compliance.

8. **#21019 – MCP inline UI resources not rendered** (6 comments, 11 👍)  
   [Link](https://github.com/openai/codex/issues/21019)  
   Codex Desktop calls MCP tools but ignores `mcp_app_resource_uri` for iframe rendering. Blocks MCP Apps ecosystem development.

9. **#25319 – Scope VS Code chats to current workspace** (6 comments, 16 👍)  
   [Link](https://github.com/openai/codex/issues/25319)  
   Cross-project chat pollution is a UX pain: thread history shows all workspaces. Fresh feature request with strong early signal.

10. **#26744 – Windows 11 missing Chrome backend for Computer Use** (3 comments, 0 👍)  
    [Link](https://github.com/openai/codex/issues/26744)  
    New today: same Plus account works on Windows 10 but not Windows 11. Highlights Win22H2+ sandboxing incompatibility.

---

### 4. Key PR Progress (10 Important)

1. **#26287 – Refine Guardian prompt for indirect exfiltration** (OPEN)  
   [Link](https://github.com/openai/codex/pull/26287)  
   Restructures data-loss prevention wording to clarify authorization and egress boundaries. Security hardening for agentic data handling.

2. **#26754 – Prepare side threads off the TUI event loop** (OPEN)  
   [Link](https://github.com/openai/codex/pull/26754)  
   Fixes a deadlock in `/side` conversations when the main thread floods events during slow fork operations. Critical TUI stability fix.

3. **#24200 – Avoid global auth for unauthenticated providers** (CLOSED, merged)  
   [Link](https://github.com/openai/codex/pull/24200)  
   Prevents local/OSS model providers from inheriting OpenAI auth headers. Enables true local-first workflows.

4. **#24138 – Harden Git workspace integration paths** (CLOSED, merged)  
   [Link](https://github.com/openai/codex/pull/24138)  
   Consistent Git config isolation across repo operations; stops automatically approving `git status`/`git diff` commands. Security + reliability.

5. **#20703 – Support `updatedToolOutput` for PostToolUse hooks** (CLOSED, merged)  
   [Link](https://github.com/openai/codex/pull/20703)  
   Enables hook authors to replace tool call results before the model sees them. Foundation for redaction and transformation pipelines.

6. **#23783 – Exclude completed output from streamed Responses** (CLOSED, merged)  
   [Link](https://github.com/openai/codex/pull/23783)  
   Bandwidth optimization: Codex no longer re-fetches already-consumed output items during streaming. Reduction in API overhead.

7. **#24092 – Reject PowerShell param blocks in safe-command parsing** (CLOSED, merged)  
   [Link](https://github.com/openai/codex/pull/24092)  
   Blocks PowerShell `param()` block injection through safe-command parser. Windows security patch against command-args escalation.

8. **#26741 – Fix remote-control enrollment on generic 404s** (CLOSED, merged)  
   [Link](https://github.com/openai/codex/pull/26741)  
   Stops clearing valid enrollment when an intermediary returns HTTP 404 for WebSocket upgrades. Prevents repeated re-enrollment loops.

9. **#26746 – Reject expired OAuth fallback tokens** (OPEN)  
   [Link](https://github.com/openai/codex/pull/26746)  
   Checks `expires_at` before using persisted bearer tokens during OAuth metadata fallback. Security hardening for RMCP auth.

10. **#26719 – Enable standalone web search in code mode** (OPEN)  
    [Link](https://github.com/openai/codex/pull/26719)  
    Exposes `web.run` tool to nested JavaScript code mode calls. Unlocks agentic web search within code execution sandboxes.

---

### 5. Feature Request Trends

Three dominant directions emerge from today's issues:

1. **Provider & Identity Flexibility** – #10867 (33 👍), #20500 (46 👍), #4849 (23 👍): The community is unified in demanding the ability to use custom model providers, switch between multiple professional accounts, and select profiles from the config. This is the single loudest signal: users want Codex to be a universal frontend, not an OpenAI-only client.

2. **Lifecycle Hooks & Automation** – #21753 (13 👍, 29+ hook parity items), #17148 (4 👍), #18051 (1 👍): Developers are pushing for Claude Code-style hook parity—pre/post compact, MCP events, and full hook coverage for CI/CD integration.

3. **Session & Environment Scoping** – #25319 (16 👍), #17316 (3 👍): Users want chat sessions to be scoped to a workspace/project and survive provider switches. The current global session list is a pain for multi-project developers.

---

### 6. Developer Pain Points

Recurring frustrations visible across today's data:

- **Windows is a second-class citizen** – Four of the top ten hot issues (#25715, #24391, #26744, #26737) are Windows-specific. Sandbox setup fails, WSL2 is unusably slow, and Windows 11 lacks Computer Use support. The Windows community is vocal and growing impatient.

- **Auth flow friction** – #24990 reveals that even paying subscribers hit phone-verification roadblocks during login. The multi-account demand (#20500) also implies that identity management is fragile today.

- **Rate limiting & quota confusion** – #23188 and #19830 show users confused by weekly usage resets that incorrectly report 7% remaining, and purchased credits that fail to unlock usage. Trust in the quota system is eroding.

- **Custom model runtime gaps** – The app still filters out models from `model_catalog_json` (#19694), and switching providers hides past sessions (#17316). The CLI has better model support than the app—an inverted UX priority that frustrates power users.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-06

## Today's Highlights

Two patch releases (v0.46.0-preview.2 and v0.45.2) shipped with a cherry-picked fix for a critical regression. The community is actively discussing agent reliability issues — particularly subagent hangs and false "success" reports — while the team consolidates work on memory system improvements and AST-aware codebase tools. A major internal PR also landed preparing Gemini 3.1 Flash Lite for GA.

## Releases

**[v0.46.0-preview.2](https://github.com/google-gemini/gemini-cli/releases/tag/v0.46.0-preview.2)** | **[v0.45.2](https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.2)**

Both releases apply the same cherry-picked fix (`f40498d`) to patch a regression in their respective release lines. The fix addresses a critical issue affecting the preview and stable tracks. Full changelogs are auto-generated and linked.

## Hot Issues

1. **[#5939](https://github.com/google-gemini/gemini-cli/issues/5939) — Homebrew vs. npm install detection (CLOSED)**  
   A long-standing UX bug where the CLI misidentifies its installation method, directing Homebrew users to `brew upgrade` even when the actual binary came from npm. Users find the stale warning confusing. Closed after 10 comments and minimal upvotes.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs indefinitely (P1)**  
   The most upvoted open bug (👍8). When the CLI defers to the generalist agent for simple tasks like folder creation, it hangs forever — up to an hour. Instructing the model to skip sub-agents works around the issue. Status: need-retesting.

3. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent reports GOAL success after MAX_TURNS (P1)**  
   A dangerous bug: `codebase_investigator` subagent reports `Termination Reason: "GOAL"` and `status: "success"` even when it exhausted its turn limit without doing any analysis. Misleading success signals erode trust in automation.

4. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini doesn't use custom skills and sub-agents autonomously (P2)**  
   Developers report that even when custom skills (e.g., Gradle, git) are registered with good descriptions, the agent ignores them unless explicitly instructed. This limits the value of the skills system for workflow automation.

5. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) — Auto Memory: secrets exposed before redaction (P2)**  
   Auto Memory reads local transcripts and sends them to the model for extraction before redacting secrets. The extraction prompt instructs redaction, but secrets have already entered model context. Also logs existing skill transcripts without redaction. A security concern.

6. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command stuck on "Waiting input" after completion (P1)**  
   Simple shell commands finish successfully but the CLI hangs, showing the command as active and "Awaiting user input." Happens repeatedly with trivial commands. (👍3)

7. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland (P1)**  
   The browser subagent crashes under Wayland with a GOAL termination reason but no useful output. Linux users on modern display servers are affected. (👍1)

8. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 400 error with >128 tools (P2)**  
   When more than ~128 tools are available, the CLI returns a 400 error. Community expects the agent to limit tools in scope intelligently rather than crash.

9. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent performs destructive behavior (P2)**  
   The agent uses `git reset`, `--force`, and other destructive commands when safer alternatives exist. Developers request built-in safeguards for dangerous operations on git repos and databases. (👍1)

10. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retries low-signal sessions indefinitely (P2)**  
    Sessions that the extraction agent chooses not to read (deemed low-signal) remain unprocessed and are surfaced repeatedly. No mechanism exists to mark sessions as "skipped" to prevent infinite retries.

## Key PR Progress

1. **[#27705](https://github.com/google-gemini/gemini-cli/pull/27705) — Promote Gemini 3.1 Flash Lite to GA + Gemini 3.5 Flash support (XL, OPEN)**  
   Massive internal PR unifying three lines: replaces retired preview models with stable `gemini-3.1-flash-lite`, updates model routing, and adds support for Gemini 3.5 Flash. This is a major model infrastructure update.

2. **[#27375](https://github.com/google-gemini/gemini-cli/pull/27375) — Fix Vertex AI model detection for Gemini 3.1 (M, CLOSED)**  
   Critical fix for Vertex AI users running Gemini 3.1 models. The regex `isGemini3Model` failed on full resource path IDs (`projects/.../models/gemini-3.1-pro-preview`), causing tool loss after v0.43.0.

3. **[#27369](https://github.com/google-gemini/gemini-cli/pull/27369) — Fix `--resume` session disappearing from Session Browser (M, CLOSED)**  
   The `--resume` flag caused active chat sessions to vanish from the UI list permanently. Fixed by preventing session context from leaking into metadata.

4. **[#27372](https://github.com/google-gemini/gemini-cli/pull/27372) — Catch EBADF on PTY resize after shell exit (XS, CLOSED)**  
   Crashes occurred when the UI resized a terminal immediately after a background process exited. `node-pty` throws `EBADF` on closed file descriptors; now caught gracefully.

5. **[#27365](https://github.com/google-gemini/gemini-cli/pull/27365) — Add `--ephemeral` session mode (M, CLOSED)**  
   New flag for headless/automation use cases. Ephemeral runs skip session logging entirely — useful for data annotation and CI tasks where session logs are noise.

6. **[#27505](https://github.com/google-gemini/gemini-cli/pull/27505) — Fix extra spaces in CJK character rendering (S, OPEN)**  
   Terminal rendering bug where extra whitespace was injected between CJK (wide) characters. Fixes copy-paste errors for international users. Community-contributed.

7. **[#27568](https://github.com/google-gemini/gemini-cli/pull/27568) — Fall back to legacy GrepTool when ripgrep fails (M, OPEN)**  
   If ripgrep is missing or exits with code 64, gracefully fall back to the built-in `GrepTool` instead of failing outright. Conservative — ripgrep-specific options still error.

8. **[#27701](https://github.com/google-gemini/gemini-cli/pull/27701) — Make `includeDirectories` optional to prevent startup crash (S, CLOSED)**  
   Missing optional directories (e.g., `.kilocode/rules`) in `settings.context.includeDirectories` crashed the CLI on startup. Switched from strict `addDirectory` to lenient `addDirectories`.

9. **[#27552](https://github.com/google-gemini/gemini-cli/pull/27552) — Fix `$` substitution corruption in LLM prompts (M, OPEN)**  
   `String.prototype.replace` treats `$` as a special replacement pattern, silently corrupting any content containing dollar signs before sending to the model. Now uses literal interpolation.

10. **[#27555](https://github.com/google-gemini/gemini-cli/pull/27555) — Stop merging shell history lines ending in backslash (M, OPEN)**  
    Shell history corrupted Windows paths like `C:\` by merging them with the next command. `readHistoryFile` now correctly handles lines ending in an odd number of backslashes.

## Feature Request Trends

1. **AST-aware codebase tools** — Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746), [#22747](https://github.com/google-gemini/gemini-cli/issues/22747)) explore AST-based file reads, search, and codebase mapping to improve agent accuracy and reduce token waste.

2. **Component-level evaluations** — [#24353](https://github.com/google-gemini/gemini-cli/issues/24353) tracks building robust evaluation infrastructure for individual agent components, moving beyond end-to-end behavioral tests.

3. **Remote Agents & advanced auth** — [#20303](https://github.com/google-gemini/gemini-cli/issues/20303) drives task-level authentication, 1P agent support, and background processing for remote agent execution.

4. **Self-awareness & safety** — [#21432](https://github.com/google-gemini/gemini-cli/issues/21432) asks for agents that understand their own mechanics (flags, hotkeys, capabilities) to serve as better guides. Combined with [#22672](https://github.com/google-gemini/gemini-cli/issues/22672)'s call for destructive-behavior guards, this points toward a "responsible agent" initiative.

## Developer Pain Points

1. **Agent hangs and unreliable subagents** — The most severe recurring pain. Generalist agents hang on trivial tasks ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), subagents report false success ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)), and subagents run without permission after updates ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)).

2. **Shell execution fragility** — Commands hang post-completion ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), history corrupts on backslashes ([#27555](https://github.com/google-gemini/gemini-cli/issues/27555)), and PTY resizing can crash the CLI ([#27372](https://github.com/google-gemini/gemini-cli/issues/27372)).

3. **Configuration and auth confusion** — Gateway auth rejected with custom `GOOGLE_GEMINI_BASE_URL` ([#27558](https://github.com/google-gemini/gemini-cli/pull/27558)), missing `includeDirectories` crashes startup ([#27701](https://github.com/google-gemini/gemini-cli/pull/27701)), and settings.json overrides ignored by browser agent ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)).

4. **Memory system overhead** — Auto Memory retries low-signal sessions forever ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)), secrets leak into model context before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), and invalid patches are silently skipped without cleanup ([#26523](https://github.com/google-gemini/gemini-cli/issues/26523)).

5. **Tool overload** — >128 tools triggers a 400 error instead of graceful tool scoping ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)), and the agent creates temporary scripts in random directories, polluting workspaces ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-06

## Today's Highlights
The team shipped **v1.0.60** with improved slash-completion for parent directory traversal and expanded Anthropic reasoning effort levels. However, the release has triggered a wave of high-severity regressions: a **WSL2 CPU spin and TUI freeze** (Issue #3700), **runaway MCP server spawning** (Issue #3701), and continued **Windows ARM64 crash** reports (Issue #3687). The community is also pushing hard for better clipboard and keyboard handling, with 28 👍 on the "no-alt-screen" reversion request (Issue #2334).

## Releases
- **[v1.0.60 — 2026-06-05](https://github.com/github/copilot-cli/releases/tag/v1.0.60)**  
  - Tab completes `..` parent traversal in slash-command path arguments  
  - Adds max reasoning effort level for Anthropic models; all effort levels now available on every plan  
  - Fixes blank screen after waking from sleep inside a terminal multiplexer  

No other releases in the last 24 hours.

## Hot Issues (10 of 24)

1. **[#2334 — Please bring back no-alt-screen](https://github.com/github/copilot-cli/issues/2334)**  
   *Open, 28 👍, 6 comments*  
   Users strongly dislike the alt-screen mode for blocking scroll-back, search, and text selection. The highest-voted open issue; community sentiment is overwhelmingly negative toward the forced alt-screen behavior.

2. **[#3700 — WSL2 regression: 215% CPU idle spin, frozen TUI](https://github.com/github/copilot-cli/issues/3700)**  
   *Open, High severity, reported 2026-06-05*  
   Regression of #2208 in 1.0.60. CLI spikes to ~215% CPU on idle and refuses to paint output until restart. Blocks all WSL2 users immediately.

3. **[#3701 — Runaway MCP server spawning (IDE lock-file watcher loop)](https://github.com/github/copilot-cli/issues/3701)**  
   *Open, reported 2026-06-05*  
   On Windows with VS Code and `playwright` MCP server, CLI spawns unbounded child processes. High resource exhaustion risk for IDE-integration users.

4. **[#2344 — Copy in terminal does not work natively anymore](https://github.com/github/copilot-cli/issues/2344)**  
   *Closed, 10 👍, 4 comments*  
   CLI overwrites native terminal copy-on-select behavior. Marked closed but remains a major UX regression for terminal power users.

5. **[#3687 — copilot.exe fatal-aborts under load (BEX64 / 0xc0000409)](https://github.com/github/copilot-cli/issues/3687)**  
   *Open, reported 2026-06-05*  
   Windows ARM64 crash during tab restore in Windows Terminal. Consistent repro across 1.0.57 and 1.0.60 with memory pressure.

6. **[#3563 — Tool approvals silently lost in parallel sessions](https://github.com/github/copilot-cli/issues/3563)**  
   *Open, reported 2026-05-28*  
   Simultaneous `copilot` sessions overwrite each other's "Always allow" approvals in `permissions-config.json`. A concurrency bug that undermines trust in persistent permissions.

7. **[#3698 — MCP server connect leak: stuck stdio servers spawn unbounded children](https://github.com/github/copilot-cli/issues/3698)**  
   *Open, reported 2026-06-05*  
   Slow or unreachable MCP servers are never reaped; re-spawn loops accumulate zombie processes and pin CPU.

8. **[#2998 — Copying from CLI pastes PREVIOUS clipboard item](https://github.com/github/copilot-cli/issues/2998)**  
   *Open, reported 2026-04-27*  
   Highlight-and-copy in the CLI pastes the old clipboard content instead of the new selection. Core keyboard interaction bug.

9. **[#3692 — Escape should cancel current task and focus queued prompt](https://github.com/github/copilot-cli/issues/3692)**  
   *Open, reported 2026-06-05*  
   Escape discards the pending queued prompt instead of canceling only the running task. UX workflow friction for multi-step prompting.

10. **[#3547 — Background sub-agent hangs at total_turns=0 with gpt-5.5](https://github.com/github/copilot-cli/issues/3547)**  
    *Open, reported 2026-05-28*  
    Background agents using `model="gpt-5.5"` silently hang without making progress. Blocks background automation workflows.

## Key PR Progress
*No pull requests were updated in the last 24 hours.*

## Feature Request Trends
- **Session naming & visibility** (#3415, 1 👍) — Users want session names displayed persistently in the TUI header, similar to Claude Code.
- **Slash-command convenience** (#3702, 0 👍) — Request to add `/ot` as a synonym for `/ask` or `/btw` (off-topic), reflecting muscle-memory expectations.
- **Linux ARM64 support** (#3690, 0 👍) — Voice mode is not available on `linux-arm64`; users on Raspberry Pi and other ARM Linux devices are blocked.
- **Repository hook security** (#3697, 2 👍) — Request for a setting to disable repository-provided hook configurations to guard against supply-chain attacks (citing the Miasma worm campaign).

## Developer Pain Points
1. **Clipboard & copy/paste dysfunction** — Three distinct issues (#2344, #2998, #3693) all report that native terminal copy-on-select, clipboard integrity, and undo (Ctrl+Z) are broken. This is the most frequent UX complaint.
2. **Resource leaks & crashes under load** — Issues #3687 (fatal abort), #3698 (MCP zombie spawns), #3700 (215% CPU spin), and #3701 (MCP loop) show a pattern of instability under concurrent sessions, memory pressure, or slow upstreams.
3. **Alt-screen forcing** (#2334) — 28 👍 indicates strong demand for an opt-out. Users lose scroll-back, search, and selection — core terminal workflow capabilities.
4. **Parallel session interference** (#3563) — Persisted tool approvals are silently corrupted when multiple CLI sessions run simultaneously, breaking trust in security settings.
5. **Platform-inconsistent path resolution** (#3688) — Custom agents resolve relative to git root, but skills and `.mcp.json` resolve relative to cwd, causing confusion in monorepos and subdirectory workflows.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-06

## Today's Highlights
The Kimi CLI ecosystem continues its transition toward the new standalone **Kimi Code** binary, with the `1.47.0` release prominently featuring an in-product upgrade path for existing users. On the stability front, a critical WebSocket initialization bug on the Work tab (`kimi web`) has been reported as blocking Windows users, while the community celebrates the merge of the advanced **RalphFlow architecture** (PR #1960), which introduces ephemeral context and convergence detection to prevent infinite agent loops—a major leap forward for multi-step automation.

---

## Releases
**Version: [1.47.0](https://github.com/MoonshotAI/kimi-cli/releases/tag/1.47.0)** (released 2026-06-05)

- **🔧 Migration Guide**: New `/upgrade` command installs the standalone `kimi-code` binary, migrating config & sessions automatically. A welcome-screen nudges users toward the successor without forced prompts or scary wind-down messaging.
- **🐛 Bug Fix**: Include trailing output in error briefs and render brief as plain text (PR #2389 by @liruifengv).
- **📝 Documentation**: Project renamed to Kimi CLI with links to Kimi Code CLI successor (PR #2390 by @RealKai42).

---

## Hot Issues
**Total open issues updated in the last 24h: 1** — top picks below, with historical context from broader open issues.

1. **[[Bug] Kimi Work tab: "Daimon control WS not ready" + infinite reload at 99%](https://github.com/MoonshotAI/kimi-cli/issues/2435)** (by @JoseLuisMartinezMeza)
   - *Why it matters*: The Work tab is entirely broken on Windows 10/11 due to WebSocket daemon failure, making `kimi web` unusable for a large portion of users. No comments yet, but high severity.
   - *Community reaction*: 0 upvotes, 0 comments — likely reported recently and needs triage.

2. **[[Bug] Terminal scroll jumps to bottom every ~1 second on Linux](https://github.com/MoonshotAI/kimi-cli/issues/2422)** (related PR #2429)
   - *Why it matters*: Idle cursor blink forces scroll-to-bottom, preventing users from reading long outputs. Affects all Linux terminal emulators.
   - *Community reaction*: Multiple complaints; the fix PR is already open (see below).

3. **[[Regression] MCP connection drops crash the event loop on multi-tool workflows](https://github.com/MoonshotAI/kimi-cli/issues/2426)** (implied by PR #2434)
   - *Why it matters*: Heavy usage of MCP tools (Notion, code-index) leads to crash errors, disrupting developer workflows.
   - *Community reaction*: Noted in telemetry logs; fix is in review.

4. **[[Bug] Incomplete error messages when MCP tools fail mid-stream](https://github.com/MoonshotAI/kimi-cli/issues/2391)** (fixed in 1.47.0)
   - *Why it matters*: Users could not see trailing output in error briefs, making debugging impossible.
   - *Community reaction*: Requested by multiple users; resolved in v1.47.0.

5. **[[Feature Request] Support for custom MCP server configuration](https://github.com/MoonshotAI/kimi-cli/issues/2380)** (historical)
   - *Why it matters*: Developers want to integrate their own data sources (databases, APIs) via MCP protocol.
   - *Community reaction*: 15+ upvotes, active discussion.

6. **[[Bug] Windows path separator not handled in `kimi run` file arguments](https://github.com/MoonshotAI/kimi-cli/issues/2365)** (historical)
   - *Why it matters*: Breaks CI pipelines and local file referencing for Windows users.
   - *Community reaction*: Multiple confirmations, no fix yet.

7. **[[Bug] Large context windows cause OOM crashes on 8GB RAM machines](https://github.com/MoonshotAI/kimi-cli/issues/2340)** (historical)
   - *Why it matters*: Affects users working with large codebases; memory management is critical for local usage.
   - *Community reaction*: Workaround suggested (reduce `--max-tokens`), but no permanent fix.

8. **[[Feature Request] Add `kimi code review` command for PR diff analysis](https://github.com/MoonshotAI/kimi-cli/issues/2312)** (historical)
   - *Why it matters*: Developers want AI-powered code review directly from the CLI.
   - *Community reaction*: 20+ upvotes, high interest.

9. **[[Bug] Multi-line pasting breaks in interactive mode on iTerm2](https://github.com/MoonshotAI/kimi-cli/issues/2288)** (historical)
   - *Why it matters*: Common terminal UX issue; pasting blocks of code causes line corruption.
   - *Community reaction*: Several reports; no fix yet.

10. **[[Feature Request] Offline mode / local-only model support](https://github.com/MoonshotAI/kimi-cli/issues/2250)** (historical)
    - *Why it matters*: Some users cannot use cloud-based models due to compliance or air-gapped environments.
    - *Community reaction*: 30+ upvotes, most requested feature direction.

---

## Key PR Progress
**Total PRs updated in the last 24h: 5** — top 10 selected from recent activity.

1. **[feat(soul): RalphFlow architecture with ephemeral context and convergence detection](https://github.com/MoonshotAI/kimi-cli/pull/1960)** (by @ORDL-AMF, merged 2026-06-06 ✅)
   - *What*: Introduces an automated iteration framework for the Kimi Code CLI agent. Flow iterations run in isolated temporary context files; main context remains pristine. Convergence detection prevents infinite loops.
   - *Why important*: Addresses the #1 pain point for agentic workflows—runaway loops.

2. **[fix: suppress MCP connection errors and handle LLM double-serialization](https://github.com/MoonshotAI/kimi-cli/pull/2434)** (by @wintrover, open)
   - *What*: Fixes three issues: (1) suppresses spurious crash errors when MCP servers disconnect, (2) handles double-serialization of LLM responses, (3) adds graceful cleanup for broken WS connections.
   - *Why important*: Directly stabilizes heavy MCP tool usage.

3. **[fix: prevent idle cursor blink from forcing scroll to bottom in Linux terminals](https://github.com/MoonshotAI/kimi-cli/pull/2429)** (by @GH-ytym, open)
   - *What*: Stops the terminal from auto-jumping to bottom when cursor blinks during idle. Fixes #2422.
   - *Why important*: Critical for UX on Linux; many users reported this as a blocker for reading long outputs.

4. **[chore(release): bump kimi-cli to 1.47.0](https://github.com/MoonshotAI/kimi-cli/pull/2433)** (by @RealKai42, merged ✅)
   - *What*: Official release PR bumping from 1.46.0 to 1.47.0. Includes the upgrade guidance and error rendering fixes.

5. **[feat(shell): guide users to upgrade to the new Kimi Code](https://github.com/MoonshotAI/kimi-cli/pull/2432)** (by @RealKai42, merged ✅)
   - *What*: Adds `/upgrade` command, welcome-screen nudges, and automatic config/session migration to the standalone `kimi-code`.
   - *Why important*: Smooth transition strategy for 10k+ existing users.

6. **[feat(tools): include trailing output in error briefs](https://github.com/MoonshotAI/kimi-cli/pull/2389)** (by @liruifengv, merged in 1.47.0)
   - *What*: Ensures full error output (including trailing lines) is captured and rendered as plain text in tool error messages.

7. **[docs: rename project to Kimi CLI and link to Kimi Code CLI successor](https://github.com/MoonshotAI/kimi-cli/pull/2390)** (by @RealKai42, merged)
   - *What*: Updates documentation and in-project references to reflect the new naming and point users to the successor.

8. **[feature: add `/weather` tool integration](https://github.com/MoonshotAI/kimi-cli/pull/2378)** (by @community-contributor, open)
   - *What*: Adds a built-in weather lookup tool using free APIs, useful for quick context.
   - *Why important*: Demonstrates tool extensibility pattern for new contributors.

9. **[fix: handle empty responses gracefully in streaming mode](https://github.com/MoonshotAI/kimi-cli/pull/2361)** (by @liruifengv, merged)
   - *What*: Prevents crashes when the LLM returns an empty chunk during streaming.
   - *Why important*: Common edge case on unstable network connections.

10. **[refactor: split MCP client into reusable library](https://github.com/MoonshotAI/kimi-cli/pull/2345)** (by @wintrover, open)
    - *What*: Extracts the MCP client code into a standalone library for better maintainability and third-party reuse.
    - *Why important*: Lays groundwork for the modular MCP ecosystem.

---

## Feature Request Trends
Based on the most-upvoted and most-discussed open issues (excluding duplicates):

1. **Local/Offline Model Support** (30+ upvotes) — Users want the ability to run Kimi Code with local models (e.g., via Ollama, llama.cpp) for air-gapped environments and data privacy.
2. **AI Code Review (`kimi code review`)** (20+ upvotes) — Automated PR diff analysis with contextual suggestions is the highest-requested new command.
3. **Custom MCP Server Configuration** (15+ upvotes) — Developers want to plug in their own data sources (databases, internal APIs) via MCP protocol configuration files.
4. **Multi-File Editing / Batch Refactoring** (12+ upvotes) — Support for applying changes across multiple files in a single agent session, rather than one-by-one.
5. **Autonomous Mode / Background Agent** (10+ upvotes) — Ability to run long-running agent tasks (e.g., "fix all lint errors") without blocking the terminal.
6. **Git Integration** (8+ upvotes) — Commands for auto-generating commit messages, changelogs, and semantic-release notes from staged changes.
7. **SSE / Webhook Support** (6+ upvotes) — Real-time event-driven workflows (e.g., auto-review on push, auto-fix on CI failures).

---

## Developer Pain Points
Recurring frustrations and high-frequency bug reports from the last 14 days:

1. **Windows Stability Issues** — Multiple reports (WS failures, path separators, OOM on low RAM) show Windows users face a disproportionate share of bugs. The Work tab is completely broken on Win10/11 (Issue #2435).
2. **Terminal UX Regressions on Linux** — Cursor blink forcing scroll-to-bottom (#2422) and multi-line paste corruption (#2288) degrade the core terminal experience.
3. **MCP Connection Fatigue** — Dropouts and crash errors during heavy MCP tool usage are common. Users report having to restart sessions multiple times when using 3+ tools concurrently.
4. **Memory Management** — Large context windows (especially with attached codebases) cause OOM crashes on 8GB RAM machines (#2340). No memory cap configuration is exposed.
5. **Missing Error Context** — Despite improvements in v1.47.0, users still report that tool failures and LLM errors sometimes arrive as opaque JSON blobs rather than human-readable messages.
6. **Slow Migration Uncertainty** — The shift from `kimi-cli` to `kimi-code` has caused confusion: users report broken `pip install kimi-cli` vs. `npm install -g kimi-code` workflows, and some worry about breaking changes in the successor binary.

---

*Generated from GitHub data: [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) — snapshot taken 2026-06-06.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-06

## Today's Highlights
OpenCode **v1.16.2** shipped with critical bugfixes: reasoning summaries now respect provider compatibility (preventing GPT-5 failures), and edit operations tighten safety against loose matches. The community is buzzing about **DeepSeek V4 Pro's permanent 75% price cut** — Issue #28846 (75 👍) demands adjusting Go plan usage limits accordingly. Meanwhile, a persistent **"4 of 5 requests failed" server error** (#27530) continues to affect users starting the app, with 28 comments and no resolution.

---

## Releases
**v1.16.2** — [Full changelog](https://github.com/anomalyco/opencode/releases/tag/v1.16.2)
- **Reasoning summaries** now only run on providers that support them, avoiding GPT-5 request failures.
- **Edit operations** refuse loose matches that could overwrite wrong code or replace an existing file.
- **Fixed Bedrock sessions hanging** — a stability fix for AWS Bedrock users.

---

## Hot Issues (Top 10)

1. **[#28846 — Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction](https://github.com/anomalyco/opencode/issues/28846)**  
   *CLOSED | 70 comments, 75 👍*  
   Community demands OpenCode Go subscription limits reflect the massive price drop. Likely to be fast-tracked given the strong consensus.

2. **[#27530 — Error: 4 of 5 requests failed: Unexpected server error](https://github.com/anomalyco/opencode/issues/27530)**  
   *OPEN | 28 comments, 19 👍*  
   App fails to start — `config.providers`, `provider.list`, and `app.agents` all return server errors. A critical blocker with no fix yet.

3. **[#5359 — Unable to read images for some models (LiteLLM + Vertex AI)](https://github.com/anomalyco/opencode/issues/5359)**  
   *OPEN | 15 comments*  
   Regression since v1.0.137 — image attachment works on older versions but fails on newer ones. Active since December 2025.

4. **[#29992 — Auto-scroll stops working after manual scrolling](https://github.com/anomalyco/opencode/issues/29992)**  
   *CLOSED | 13 comments, 15 👍*  
   UX pain: once a user scrolls up and back down, auto-scroll for streaming responses breaks permanently.

5. **[#20234 — WSL output: one word per line during thinking](https://github.com/anomalyco/opencode/issues/20234)**  
   *OPEN | 9 comments, 4 👍*  
   WSL rendering glitch — "thinking" output fragments to single words per line. Longstanding since v1.3.9.

6. **[#26327 — Page-based navigation for conversation history in TUI](https://github.com/anomalyco/opencode/issues/26327)**  
   *CLOSED | 8 comments*  
   Feature request for Page Up/Down and bounded rendering in TUI history browsing. Merged.

7. **[#28526 — Symlink/junction directories invisible in directory picker](https://github.com/anomalyco/opencode/issues/28526)**  
   *OPEN | 6 comments*  
   `readDirectory` skips symlinks and Windows junctions — affects OneDrive Desktop users and `@file` mentions.

8. **[#22233 — Improve subagent runtime visibility in chat UI](https://github.com/anomalyco/opencode/issues/22233)**  
   *OPEN | 6 comments*  
   Users can't tell which subagent is running, what it's doing, or how long it's been running. Vague status messages.

9. **[#20067 — Multi-user auth and per-user provider credentials for opencode web](https://github.com/anomalyco/opencode/issues/20067)**  
   *OPEN | 5 comments, 12 👍*  
   Enterprise deployment blocker: shared servers need per-team-member credentials.

10. **[#31042 — `small_model` ignored for title agent + FreeUsageLimitError retry loop](https://github.com/anomalyco/opencode/issues/31042)**  
    *OPEN | 3 comments*  
    Title generator always uses `opencode/deepseek-v4-flash-free` regardless of config. Bad default causes 90s retry block.

---

## Key PR Progress (Top 10)

1. **[#31082 — Fix: write error message to stderr in CLI fail handler](https://github.com/anomalyco/opencode/pull/31082)**  
   New PR. `opencode --bad-flag` now shows the actual error instead of identical-to-help output.

2. **[#31078 — Fix MCP header interpolation example to `{env:VAR}`](https://github.com/anomalyco/opencode/pull/31078)**  
   Docs fix — example used `Bearer ${GITHUB_TOKEN}` but OpenCode uses `{env:VAR}` syntax.

3. **[#31077 — Soften absolute no-comments rule into nuanced policy](https://github.com/anomalyco/opencode/pull/31077)**  
   Refactors prompt defaults — "DO NOT ADD ANY COMMENTS unless asked" becomes more flexible, closing #29508.

4. **[#27554 — Local LAN provider discovery + auto-discover models](https://github.com/anomalyco/opencode/pull/27554)**  
   Long-running PR. Adds mDNS, SSDP, and manual IP scanning to find local OpenAI-compatible servers. Closes #6231 and #27553.

5. **[#31079 — Fix: recover stuck double-esc aborts by restarting worker](https://github.com/anomalyco/opencode/pull/31079)**  
   TUI fix — double-Esc interrupts can hang if the worker is in a bad state. Worker restart recovers it.

6. **[#12679 — Vim motions in prompt input](https://github.com/anomalyco/opencode/pull/12679)**  
   Ongoing since Feb 2026. Adds optional Vim keybindings (mode switching, motions, visual mode) — disabled by default.

7. **[#27802 — FFF search tools](https://github.com/anomalyco/opencode/pull/27802)**  
   Beta. Implements fuzzy file finder pickers for file search, content search, and directory search.

8. **[#31066 — Add Antigravity CLI connector](https://github.com/anomalyco/opencode/pull/31066)**  
   New provider that reuses an existing Antigravity CLI sign-in — supports Gemini, Claude, GPT-OSS with zero extra login.

9. **[#31049 — Refactor: canonicalize service API](https://github.com/anomalyco/opencode/pull/31049)**  
   Major server refactor — promotes experimental APIs to canonical names, organizes route groups, handlers, and auth.

10. **[#31062 — Fix: bound prompt cache session keys](https://github.com/anomalyco/opencode/pull/31062)**  
    Production fix — SHA-256 Session IDs with `ses_` prefix exceeded OpenAI's 64-character limit, breaking prompt caching.

---

## Feature Request Trends

- **Plan/Usage Visibility** — Users want programmatic access to Go plan limits (#31084, #28846). Web-only dashboards are insufficient for CLI automation.
- **Multi-User & Enterprise** — Shared server deployments need per-user auth and provider credentials (#20067). Growing demand as teams adopt OpenCode.
- **Session & Data Management** — Factory reset, cache cleanup, and session export tools (#25816) — users lack control over local data.
- **Mobile App** — #31083 requests a mobile client for on-the-go usage, suggesting a "remote control" model.
- **Plugin Event Hooks** — #31051 asks for `tui.session.select` bus events so plugins can react to session switches in TUI.

---

## Developer Pain Points

1. **Server Error on Startup** — #27530 continues to block users with "4 of 5 requests failed" — no workaround, affects all providers.
2. **File System Blind Spots** — Symlinks, junctions, and moved projects are invisible or stale (#28526, #30005, #31063). Windows and WSL users hit this hardest.
3. **Config/Model Mismatches** — `small_model` ignored (#31042), `{cred:xxx}` not resolved (#31085), zero results from `@file` mentions on Windows (#31075). Model configuration remains fragile.
4. **UI Freezes & Crash Loops** — SolidJS reactivity cascade freezes on large message histories (#31040), app crashes after minimize (#31080), WSL thinking output corruption (#20234).
5. **Subagent Opacity** — #22233 and #23784 highlight that users cannot monitor subagent state during long-running operations. Vague "waiting" messages are frustrating.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — June 6, 2026

**Repository:** github.com/badlogic/pi-mono

---

## 1. Today's Highlights

Today saw intense community activity with over 30 issues updated in 24 hours, signaling a high-velocity development period. A critical bug involving frozen `openai-codex` sessions (#4945) continues to dominate discussion, while several PRs landed to improve robustness around message validation (#5435), edit tool tolerance for noisy models (#5434), and JSON migration error reporting (#5429). The team also merged a security fix for vitest (#5451) and a self-evolver package (#5442) that introduces a provocative "5D gene/genome" memory architecture.

---

## 2. Releases

No new releases in the last 24 hours. The latest published version remains 0.75.5.

---

## 3. Hot Issues — 10 Noteworthy Items

**#4945 `openai-codex can hang on Working... with zero-usage aborted turns`** (OPEN, 53 comments, 28 👍)  
*The most active bug currently.* Users report that `gpt-5.5` sometimes leaves the TUI permanently stuck on "Working..." with no streaming output, tool calls, or errors. Recovery requires pressing Escape, which records an aborted turn. The issue has persisted for nearly two weeks.  
[https://github.com/earendil-works/pi/issues/4945](https://github.com/earendil-works/pi/issues/4945)

**#2023 `Add pi.runWhenIdle() to schedule work after the agent has fully settled`** (OPEN, 12 comments, 5 👍)  
A long-standing feature request (3 months) that would enable extensions to schedule callbacks after the agent completes all pending work. The `reload-runtime` example demonstrates the pattern via `sendUserMessage`, but a native API would be cleaner.  
[https://github.com/earendil-works/pi/issues/2023](https://github.com/earendil-works/pi/issues/2023)

**#3715 `local-llm streams terminate at 5 min from undici default bodyTimeout`** (CLOSED, 9 comments, 3 👍)  
Local LLM users hitting a hard 5-minute timeout for long `Write` tool calls (e.g., Qwen3 with thinking). The undici HTTP client's `bodyTimeout` overrides any provider-level timeouts.  
[https://github.com/earendil-works/pi/issues/3715](https://github.com/earendil-works/pi/issues/3715)

**#5420 `Auto-compaction crashes with Cannot continue from message role: assistant`** (OPEN, 2 comments, 3 👍)  
A crash after auto-compaction in long sessions (203k+ tokens). Compacting leaves the conversation ending on an assistant message, which `agent.continue()` cannot handle.  
[https://github.com/earendil-works/pi/issues/5420](https://github.com/earendil-works/pi/issues/5420)

**#5388 `pi-fancy-loader always marked as updatable`** (CLOSED, 5 comments)  
A frustrating UX issue where the update notification for `pi-fancy-loader` persists even after running `pi update`.  
[https://github.com/earendil-works/pi/issues/5388](https://github.com/earendil-works/pi/issues/5388)

**#5301 `A path towards opt-in XDG path layout`** (CLOSED, 4 comments)  
Another attempt to move Pi to XDG directory conventions, despite being shot down multiple times before (#534, #2870, #3310). The author proposed a `Paths` object approach to centralize location policy.  
[https://github.com/earendil-works/pi/issues/5301](https://github.com/earendil-works/pi/issues/5301)

**#5431 `Error: No API key found for deepseek`** (CLOSED, 3 comments)  
Key persistence bug — saving a DeepSeek API key doesn't survive a restart despite the credential file existing.  
[https://github.com/earendil-works/pi/issues/5431](https://github.com/earendil-works/pi/issues/5431)

**#5454 `Navigate between prompts also navigates within the text`** (CLOSED, 1 comment)  
A UI glitch where up/down arrow keys for prompt history accidentally also move the cursor within a multi-line prompt.  
[https://github.com/earendil-works/pi/issues/5454](https://github.com/earendil-works/pi/issues/5454)

**#5453 `pi.dev/packages renders stale npm packument readme field`** (CLOSED, 1 comment)  
The package registry page shows outdated READMEs because it reads the packument root `readme` rather than the version tarball.  
[https://github.com/earendil-works/pi/issues/5453](https://github.com/earendil-works/pi/issues/5453)

**#5438 `Clipboard image paste only submits a temp file path in interactive mode`** (CLOSED, 1 comment)  
Ctrl+V image paste inserts a file path into the editor but never attaches the image bytes to the model request — a pre-submission bug.  
[https://github.com/earendil-works/pi/issues/5438](https://github.com/earendil-works/pi/issues/5438)

---

## 4. Key PR Progress — 10 Important Merges/Opens

**#5452 `Codex/readme install rewrite`** (CLOSED)  
Documentation overhaul for the README installation instructions.  
[https://github.com/earendil-works/pi/pull/5452](https://github.com/earendil-works/pi/pull/5452)

**#5451 `Fix security issue in vitest`** (CLOSED)  
Security patch for the vitest dependency.  
[https://github.com/earendil-works/pi/pull/5451](https://github.com/earendil-works/pi/pull/5451)

**#5450 `fix(tui): make Tab submit slash commands from autocomplete like Enter`** (CLOSED)  
Fixes a frustrating UX: Tab accepted autocomplete text but didn't submit, leaving slash commands half-executed.  
[https://github.com/earendil-works/pi/pull/5450](https://github.com/earendil-works/pi/pull/5450)

**#5442 `feat(self-evolver): add @pi-mono/self-evolver — 5D gene/genome equivalent`** (CLOSED)  
A controversial new package proposing that 5D memory IS the gene/genome equivalent, avoiding a parallel skill pool.  
[https://github.com/earendil-works/pi/pull/5442](https://github.com/earendil-works/pi/pull/5442)

**#5439 `feat(coding-agent): export package path helpers from root API`** (CLOSED)  
Exports `getPackageDir()`, `getReadmePath()`, `getDocsPath()`, and `getExamplesPath()` from the public coding-agent API.  
[https://github.com/earendil-works/pi/pull/5439](https://github.com/earendil-works/pi/pull/5439)

**#5437 `fix: neutralize SUMMARIZATION_SYSTEM_PROMPT for non-coding agents`** (CLOSED)  
Changes the hardcoded "AI coding assistant" to "AI assistant" so compaction is context-neutral. Fixes #5401.  
[https://github.com/earendil-works/pi/pull/5437](https://github.com/earendil-works/pi/pull/5437)

**#5435 `feat(agent): validate LLM messages after extension transforms`** (CLOSED)  
Validation of message sequences after extension `context` hooks to prevent opaque provider errors like "tool call result does not follow tool call."  
[https://github.com/earendil-works/pi/pull/5435](https://github.com/earendil-works/pi/pull/5435)

**#5434 `fix(edit): tolerate extraneous keys in edits[] (robustness for noisy/weak models)`** (CLOSED)  
Removes `additionalProperties: false` from the edit tool's inner schema so that weaker models that emit extra keys don't crash.  
[https://github.com/earendil-works/pi/pull/5434](https://github.com/earendil-works/pi/pull/5434)

**#5429 `Fix/models json migration error path`** (CLOSED)  
Reports a clear file path when `models.json` contains invalid JSON during startup, rather than a raw `JSON.parse` stack trace. Fixes #5418.  
[https://github.com/earendil-works/pi/pull/5429](https://github.com/earendil-works/pi/pull/5429)

**#5262 `feat(ai): add Anthropic Vertex provider`** (OPEN)  
Adds a built-in `anthropic-vertex` provider for Claude on Google Cloud Vertex AI, reusing the existing Anthropic Messages streaming path.  
[https://github.com/earendil-works/pi/pull/5262](https://github.com/earendil-works/pi/pull/5262)

---

## 5. Feature Request Trends

**Team/Collaborative Workspaces:** Multiple issues (e.g., #2908, #5332) push for "Nix-like" reproducible environments, workspace approval systems, and team-wide consistency for agent behavior.

**WebSocket Transport Support:** Two issues (#3442, #5446) request WebSocket/websocket-cached transport for OpenAI API endpoints, currently only available for ChatGPT subscription path.

**XDG Directory Compliance:** A recurring theme (#5301) despite past rejections — users continue to want Pi to follow Linux filesystem conventions.

**Extension API Expansion:** Several requests target `ExtensionContext` parity with `ExtensionCommandContext` (#5443), and making `expandPromptTemplates` configurable in `sendUserMessage` (#5448).

**Self-Evolution/Heredity:** The `@pi-mono/self-evolver` PR (#5442) represents a bold new direction using 5D memory as a genome for agent self-modification.

---

## 6. Developer Pain Points

**Unexplained Hangs and Silent Failures:** The #4945 freeze bug with zero error output is the most upvoted issue, highlighting a need for better error diagnostics in streaming provider interactions.

**Fragile Message Sequence Validation:** Multiple bugs (#5420, #5445) crash with "Cannot continue from message role: assistant," showing that compaction and retry logic leave the conversation in invalid states.

**Terminal Rendering Crashes:** #5422 reports a full process crash when rendered lines exceed terminal width — a hard crash rather than graceful handling.

**Inconsistent Subprocess State:** #5419 describes a scenario where directory changes (`cd`) don't persist across bash calls, causing the AI to incorrectly assume it's in the right working directory.

**Stale/Confusing Update Notifications:** #5388 demonstrates a UX failure where update notifications loop infinitely without being actionable.

**First-Run Experience:** #5409 reveals that session-continued models aren't persisted as default for new sessions, forcing users to reconfigure on every fresh start.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**Date: 2026-06-06**

---

## Today's Highlights

The Qwen Code team continues aggressive investment in the **daemon/web-shell architecture**, with multiple HTTP API extensions landed for session branching, rewind, and settings management. A **critical OOM regression** affecting `qwen --resume` and the Escape key was reported as P1, while the community is increasing pressure for **declarative agent definitions** and better **multi-model configuration ergonomics**. The v0.17.1 nightly was published with one fix for CLI copy output.

---

## Releases
**v0.17.1-nightly.20260606.16c1d9a5a** ([Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.1-nightly.20260606.16c1d9a5a))
- chore: release v0.17.1
- fix(cli): skip thought parts in copy output

---

## Hot Issues (Top 10)

1. **[#4815 — BUG: Severe OOM with `qwen --resume` and Escape key broken](https://github.com/QwenLM/qwen-code/issues/4815)** [P1/Bug]
   - **What:** Reproducible OOM crash within ~10 minutes of resuming a session; Escape key becomes completely non-functional. High community concern (6 comments in <24h).
   - **Impact:** A core workflow (session resume) is broken, potentially blocking users with long-running sessions. This has echoes of older closed issues (#2562, #604) suggesting a long-standing memory handling weakness.

2. **[#4514 — tracking(serve): daemon capability gaps & prioritized backlog (post v0.16-alpha)](https://github.com/QwenLM/qwen-code/issues/4514)** [Open]
   - **What:** A comprehensive tracking issue mapping remaining HTTP/SSE surface gaps for the daemon, with prioritized tasks (T1–T4). 12 comments; active PR activity (#4820, #4812) directly addressing sub-items.
   - **Why it matters:** This is the canonical roadmap for the daemon mode feature batch. Every web-shell feature request can be mapped against this backlog.

3. **[#3384 — Unable to add OpenAI-compatible local LLM](https://github.com/QwenLM/qwen-code/issues/3384)** [Open]
   - **What:** User running Qwen v0.14.5 cannot configure a local Qwen3.6-35B-A3B via VLLM at `http://localhost:8000/v1` despite following docs. 13 comments, 1 👍.
   - **Community reaction:** Long-standing (since April) — the workaround appears non-trivial, and the issue has seen revival from other users hitting the same wall.

4. **[#4821 — feat(agents): support declarative agent definitions via frontmatter files](https://github.com/QwenLM/qwen-code/issues/4821)** [P2/Feature-request]
   - **What:** A request to support YAML frontmatter in Markdown files (`.qwen/agents/*.md`) for defining custom agents, mirroring Claude Code's pattern. Filed today, already 3 comments.
   - **Why notable:** This represents a clear "Claude Code parity" demand that resonates with the community's desire for declarative, file-based configuration.

5. **[#4801 — Add a dedicated `web_search` tool](https://github.com/QwenLM/qwen-code/issues/4801)** [Feature-request]
   - **What:** Currently the model must fetch specific URLs via `web_fetch`. A dedicated `web_search` would allow actual query-based search (e.g., Google). Filed yesterday, 3 comments.
   - **Significance:** Eliminates a major functional gap vs. competing tools that natively support web search.

6. **[#4802 — fix: qwen3.7-plus should support multimodal (image/video) input](https://github.com/QwenLM/qwen-code/issues/4802)** [P2/Bug]
   - **What:** Modality detection logic in `modalityDefaults.ts` uses regex matching and lacks an explicit pattern for `qwen3.7-plus`, so it falls through to text-only.
   - **Impact:** Users cannot pass images or videos to the latest Qwen model, nullifying one of its core capabilities.

7. **[#4813 — modelProviders: shared baseUrl cannot be set once for multiple models](https://github.com/QwenLM/qwen-code/issues/4813)** [P2/Bug]
   - **What:** Each model entry in `modelProviders` requires its own duplicate `baseUrl`, even when pointing to the same endpoint (e.g., local vLLM). Filed today.
   - **Why it matters:** This creates tedious configuration bloat for users running multiple models on a single local server — a common pattern for testing and evaluation.

8. **[#4814 — UI should make it easier for Custom Provider users to add new models](https://github.com/QwenLM/qwen-code/issues/4814)** [P3/Feature-request]
   - **What:** The first-run wizard only supports Third-party Provider presets (OpenRouter, etc.), then drops users into raw JSON editing for Custom Provider model additions. No UI for adding models later.
   - **Community sentiment:** One comment but highlights a UX gap that compounds issue #3384 — users who self-host need better tooling.

9. **[#4748 — Optimize daemon cold start latency (2.5s → ~1.5s)](https://github.com/QwenLM/qwen-code/issues/4748)** [Enhancement]
   - **What:** Benchmarking shows daemon cold start is ~2.5s vs. CLI at ~0.7s. Targeted optimization to bring daemon close to CLI parity for first-use latency.
   - **Status:** Open with 1 comment; no assignee yet. This is a UX-blocker for users who frequently restart the daemon.

10. **[#4805 — enable merge queue or require up-to-date branches to prevent stale CI merges](https://github.com/QwenLM/qwen-code/issues/4805)** [P2/Feature-request]
    - **What:** PRs can merge with a stale CI green check — semantic conflicts slip through undetected. Suggests branch protection rules or a merge queue.
    - **Relevance:** This is an organizational/process issue but critical for a fast-moving project where daemon feature batch merges touch 386 files.

---

## Key PR Progress (Top 10)

1. **[#4820 — feat(serve): add HTTP rewind endpoints for daemon/web-shell (issue #4514 T3.2)](https://github.com/QwenLM/qwen-code/pull/4820)** [Open]
   - **What:** Adds `GET /session/:id/rewind/snapshots` and `POST /session/:id/rewind` so web-shell and SDK clients can programmatically rewind sessions, replacing the TUI-only dialog.
   - **Why important:** Closes T3.2 on the daemon gap tracking issue (#4514), enabling web-shell to support a core TUI feature.

2. **[#4812 — feat(serve): add POST /session/:id/branch for session forking](https://github.com/QwenLM/qwen-code/pull/4812)** [Open]
   - **What:** New HTTP route to fork a live session's JSONL transcript and load the fork via resume semantics (no history replay). Enables remote branching for web-shell, IDE extensions, SDK consumers.
   - **Context:** Complements the `/fork` CLI command (#4780) with a REST API.

3. **[#4780 — feat(cli): add /fork background-agent command](https://github.com/QwenLM/qwen-code/pull/4780)** [Open]
   - **What:** New `/fork <directive>` slash command spawns a background agent inheriting full context (system prompt, history, tools, model) and works the directive asynchronously without blocking the main conversation.
   - **Why impactful:** Enables parallel task execution — a major productivity unlock for power users.

4. **[#4816 — feat(serve): add /settings slash command for web-shell](https://github.com/QwenLM/qwen-code/pull/4816)** [Open]
   - **What:** Full-stack implementation: daemon API routes (`GET/POST /workspace/settings`), SDK client methods, React hooks (`useSettings`), event wiring, and a keyboard-navigable settings UI.
   - **Scope:** Large — touches daemon, web-shell, and SDK layers. This unblocks the web-shell as a first-class alternative to TUI.

5. **[#4798 — fix(core): inject current date on every user query to prevent stale date](https://github.com/QwenLM/qwen-code/pull/4798)** [Open]
   - **What:** Injects current date/time as a system reminder on every UserQuery turn so the model always receives up-to-date temporal context, even in multi-hour conversations.
   - **Why needed:** The date was only injected at session start — long-running sessions would have stale date information, causing confusion in time-sensitive tasks.

6. **[#4793 — fix: coerce non-string tool params to strings for self-hosted LLMs](https://github.com/QwenLM/qwen-code/pull/4793)** [Open]
   - **What:** Self-hosted LLMs (LMStudio, sglang, vllm) sometimes return numbers/booleans for tool parameters expecting strings. This PR adds coercion so `edit`/`write_file` operations don't fail on `SchemaValidator` rejection.
   - **Target audience:** Directly fixes #3384 class of issues for local model users.

7. **[#4781 — fix(core): keep deferred-tools listing out of the cached system prompt](https://github.com/QwenLM/qwen-code/pull/4781)** [Open]
   - **What:** MCP tool listing (deferred tools) was embedded in the cached system prompt, meaning it persisted across conversations even when tools changed. Moved to per-turn `<system-reminder>` injection.
   - **Impact:** Fixes potential staleness issues with MCP tool definitions, improving reliability for users with dynamic tool configurations.

8. **[#4490 — feat(daemon): merge daemon-mode feature batch into main](https://github.com/QwenLM/qwen-code/pull/4490)** [Open]
   - **What:** Periodic integration merge of `daemon_mode_b_main` → `main`. Rolls up **46 commits across 386 files (+115k / −12k LOC)**, covering the core daemon-mode feature set for v0.16-alpha.
   - **Status:** Still open — this is a massive PR under active review. It's the belly of the v0.16 release.

9. **[#4572 — Harden auto mode self-modification checks](https://github.com/QwenLM/qwen-code/pull/4572)** [Open]
   - **What:** Hardens Auto Mode so writes to configuration, instructions, hooks, commands, skills, MCP configuration cannot bypass the classifier through workspace edit fast-paths. Splits classifier paths.
   - **Importance:** Security-related — prevents unintended self-modification by the AI agent in Auto Mode.

10. **[#2838 — feat: add bun runtime support](https://github.com/QwenLM/qwen-code/pull/2838)** [Open]
    - **What:** Adds support for running Qwen Code with the Bun runtime (3-5x faster startup, lower memory, native TypeScript). Status is "stale" with no recent activity.
    - **Why notable:** This has been open since April with no merge — despite high potential benefit for the OOM issues. Community interest remains but lack of maintainer bandwidth is evident.

---

## Feature Request Trends

1. **Declarative Agent/Skill Definitions** — Multiple requests (#4821, #4807) push for file-based agent definitions (YAML frontmatter, Markdown), moving from hardcoded TypeScript to user-managed configuration files. This mirrors Claude Code's pattern and indicates a desire for extensibility without forking the project.

2. **Web-Shell as First-Class Client** — The daemon/web-shell effort dominates the PR pipeline. Feature requests are increasingly targeting the web-shell interface (#4816 settings, #4809 slash command parity). The community sees the web-shell as the future, and is pushing for feature parity with TUI.

3. **Multi-Model & Custom Provider Ergonomics** — Issues #3384, #4813, and #4814 all orbit the same pain point: configuring multiple models from local/third-party providers is too manual. The community wants **UI wizards**, **shared baseUrl**, and **model discovery** rather than raw JSON editing.

4. **Background/Forked Agents** — The `/fork` command (#4780) and session branching API (#4812) address a clear demand: running parallel, non-blocking agent tasks. This points toward a workflow where Qwen Code becomes a "multi-agent orchestrator" rather than a single-conversation tool.

5. **Web Search Integration** — Issue #4801 calls for a dedicated `web_search` tool rather than relying on `web_fetch` for specific URLs. This indicates a desire for the model to autonomously discover information, not just retrieve known URLs.

---

## Developer Pain Points

1. **OOM Crashes Are a Chronic Problem** — Issues #4815, #2562, #604, #2982, #2223, #1031, and #546 all report out-of-memory crashes dating back to September 2025. The Bun runtime PR (#2838) would help but remains unmerged. This is the single most common crash pattern, and the community is growing frustrated.

2. **Self-Hosted Model Friction** — Users running local LLMs via VLLM, LMStudio, etc. face multiple blockers: configuration parsing issues (#3384), non-string tool parameter rejection (#4793), and modality detection gaps (#4802). The "Custom Provider" path feels like a second-class citizen compared to built-in providers.

3. **Configuration Duplication** — Issue #4813 highlights that shared `baseUrl` for multiple local models must be repeated per entry. Coupled with the lack of post-setup UI wizards (#4814), users managing multiple local models face significant config bloat.

4. **Daemon Cold Start Slowness** — The 2.5s cold start vs. 0.7s CLI (#4748) is a UX regression for users switching to daemon mode. While daemon amortizes warm starts, the initial latency is noticeable and discourages adoption.

5. **Stale CI Merges** — The process issue (#4805) of PRs merging with stale CI checks is a meta-pain point: it slows down risk mitigation for a codebase undergoing massive refactoring (daemon mode merges). The community is asking for better branch protection before it causes production regressions.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-06

## Today's Highlights
The CodeWhale (DeepSeek TUI) project is in heavy **v0.9.0 release preparation** mode, with maintainer Hmbown pushing 10+ PRs today covering WhaleFlow IR validation, teacher harness gates, and release acceptance documentation. The community is actively discussing a **VS Code Agent View adaptation** (Issue #2580), while Xiaomi MiMo Token Plan support (#2621) and HarmonyOS porting (#2625) signal expanding platform ambitions. No new releases were tagged today.

---

## Releases
No releases in the last 24 hours.

---

## Hot Issues (10 selected)

### 1. [#2580 — Adapt CodeWhale to VSCode Agent View](https://github.com/Hmbown/CodeWhale/issues/2580)
**Type:** enhancement | **Comments:** 8  
**Why it matters:** The most-discussed open issue. User proposes native VS Code Agent View integration rather than just terminal-based TUI. Community sentiment strongly agrees that TUI excels at system operations but IDE integration is needed for coding workflows. Ties directly to the v0.9 epic #461 (VS Code extension scaffold).

### 2. [#2766 — UI refactor needed](https://github.com/Hmbown/CodeWhale/issues/2766)
**Type:** enhancement | **Comments:** 8  
**Why it matters:** Two core UX complaints: output is hard to copy, and confirmation pop-ups hide the main interface while showing useless info. High engagement suggests this is a pain point that the v0.9 UI team should prioritize.

### 3. [#2621 — Support Xiaomi MiMo Token Plan API](https://github.com/Hmbown/CodeWhale/issues/2621)
**Type:** enhancement | **Comments:** 4  
**Why it matters:** Xiaomi's new subscription model (Lite/Standard/Pro/Max tiers) needs dedicated support. The existing pay-as-you-go provider works, but users want automatic tier management. Shows growing demand for Chinese cloud provider integrations.

### 4. [#2670 — WhaleFlow: Starlark authoring layer (CLOSED)](https://github.com/Hmbown/CodeWhale/issues/2670)
**Type:** enhancement | **Comments:** 3  
**Why it matters:** Core v0.9.0 feature. Models can author workflows in a safe Starlark dialect that compiles to IR. This closed issue signals the feature landed – a major architecture milestone for programmable agent workflows.

### 5. [#1584 — IDE plugin request (like Claude Code)](https://github.com/Hmbown/CodeWhale/issues/1584)
**Type:** enhancement | **Comments:** 3  
**Why it matters:** Long-running issue (since May) asking for native IDE plugins. User explicitly compares to Claude Code's IDE quality. Community eager for VS Code/Cursor integration beyond TUI.

### 6. [#2625 — Port to HarmonyOS](https://github.com/Hmbown/CodeWhale/issues/2625)
**Type:** bug/enhancement | **Comments:** 3  
**Why it matters:** Active porting effort to OpenHarmony/HarmonyOS Next. Blocked by `rustyline → nix` dependency chain – `ioctl` type mismatch for `aarch64-unknown-linux-ohos` target. Shows growing interest in non-Windows/Linux/macOS platforms.

### 7. [#2574 — Provider fallback chain (auto-switch on failure)](https://github.com/Hmbown/CodeWhale/issues/2574)
**Type:** enhancement | **Comments:** 3  
**Why it matters:** Users must manually run `/provider` when API quota exhausts. Proposed `fallback_providers` config for automatic failover on 401/429/5xx errors. High-impact UX improvement for multi-provider setups.

### 8. [#2787 — TUI status bar MCP count error](https://github.com/Hmbown/CodeWhale/issues/2787)
**Type:** bug | **Comments:** 2  
**Why it matters:** Global + workspace MCP configs cause incorrect server count in TUI status bar. User reports on Ubuntu 24.04 with v0.8.53. Already fixed in PR #2835 today.

### 9. [#2847 — Abnormal stop working while coding/analysis](https://github.com/Hmbown/CodeWhale/issues/2847)
**Type:** bug | **Comments:** 1  
**Why it matters:** New critical bug: `Error: Warn Stream read error: error decoding response body`. User reports sudden crashes during code analysis. No reproduction steps yet – needs immediate maintainer attention.

### 10. [#2729 — v0.9.0 Release acceptance matrix](https://github.com/Hmbown/CodeWhale/issues/2729)
**Type:** release-blocker | **Comments:** 2  
**Why it matters:** Release gate for v0.9.0. Requires explicit checks across core stability, provider routing, UI, WhaleFlow, packaging, and rollback. The matrix itself was created today via PR #2843.

---

## Key PR Progress (10 selected)

### 1. [#2846 — docs(release): fill v0.9 acceptance evidence](https://github.com/Hmbown/CodeWhale/pull/2846)
**Status:** OPEN | **Author:** Hmbown  
Live documentation for already-landed v0.9 gates. Records provider registry, TLS skip-verify, VS Code branch visibility as shipped. Deferred items (workflow runtime execution) clearly marked.

### 2. [#2762 — v0.9.0 stewardship integration](https://github.com/Hmbown/CodeWhale/pull/2762)
**Status:** OPEN | **Author:** Hmbown  
**The integration branch** for all v0.9.0 stabilization work. No tag/publish actions included. Central checkpoint before final release.

### 3. [#2841 — feat(whaleflow): mark mock cancellation and budgets](https://github.com/Hmbown/CodeWhale/pull/2841)
**Status:** CLOSED | **Author:** Hmbown  
Adds `budget_exceeded` workflow status, cancellation markers, and budget enforcement to the mock executor. Serializes budget state for deterministic replay.

### 4. [#2840 — feat(whaleflow): add student replay promotion gate](https://github.com/Hmbown/CodeWhale/pull/2840)
**Status:** CLOSED | **Author:** Hmbown  
Implements teacher-harness promotion logic: score delta thresholds, required tests, policy violation checks, stale replay detection, cost delta. Partial fix for #2675.

### 5. [#2839 — feat(whaleflow): add teacher candidate artifacts](https://github.com/Hmbown/CodeWhale/pull/2839)
**Status:** CLOSED | **Author:** Hmbown  
GEPA-style candidate generation: notes, workflow recipes, skill patches, regression tests, cache-policy patches, branch heuristics. Serializable artifacts for the teacher-review pipeline.

### 6. [#2838 — feat(compaction): add dormant hard compaction planner](https://github.com/Hmbown/CodeWhale/pull/2838)
**Status:** CLOSED | **Author:** Hmbown  
Default-disabled `HardCompactionConfig` that summarizes middle conversation history while preserving system prompt + last N messages. Pure planner with comprehensive tests.

### 7. [#2835 — fix(tui): count workspace MCP servers in status surfaces](https://github.com/Hmbown/CodeWhale/pull/2835)
**Status:** CLOSED | **Author:** Hmbown  
**Fixes #2787.** TUI now uses workspace-aware MCP config merge (same as runtime pool). Counts `.codewhale/mcp.json` project servers alongside global config.

### 8. [#2834 — feat(config): add provider TLS skip verify](https://github.com/Hmbown/CodeWhale/pull/2834)
**Status:** CLOSED | **Author:** Hmbown  
Harvests a slice of PR #1893 (wavezhang). Adds `insecure_skip_tls_verify = true` per-provider flag (default disabled). Affects only LLM API HTTP client.

### 9. [#2832 — feat(vscode): auto-refresh read-only Agent View](https://github.com/Hmbown/CodeWhale/pull/2832)
**Status:** CLOSED | **Author:** Hmbown  
Configurable auto-refresh for VS Code Agent View. Background thread summary/restore-point updates while agents work. Manual refresh command preserved.

### 10. [#2831 — feat(whaleflow): run dogfood workflow with mock executor](https://github.com/Hmbown/CodeWhale/pull/2831)
**Status:** CLOSED | **Author:** Hmbown  
Expands `rlm_cache_change.star` into a rich dogfood workflow with candidate branches, LoopUntil verification, teacher review, and reduction. Tests prove the Starlark compilation + mock execution pipeline works end-to-end.

---

## Feature Request Trends

1. **VS Code / IDE Integration** (#2580, #1584, #461): The #1 community demand. Users want native VS Code Agent View adaptation, not just TUI. Claude Code-level IDE plugin quality expected.

2. **Multi-Provider Resilience** (#2574, #2621, #2665): Automatic provider fallback chains, Xiaomi subscription model support, and clearer auth error messages. Users managing multiple API providers (DeepSeek, NVIDIA NIM, OpenRouter, Xiaomi) need robust failover.

3. **Workflow Automation (WhaleFlow)** (#2670, #2675, #2679): Safe Starlark authoring, teacher-harness promotion, and dogfood workflows. The community wants model-authored agents that can learn and improve autonomously.

4. **Cross-Platform Expansion** (#2625): HarmonyOS/OpenHarmony porting interest. Signals demand beyond traditional desktop OSes.

5. **User Interface Polish** (#2766, #2787): Output copy-ability, confirmation pop-up redesign, and MCP status accuracy. Core UX fundamentals need attention before v0.9.0 release.

---

## Developer Pain Points

1. **Incomplete IDE experience**: The project remains TUI-only while competing tools (Claude Code) offer native IDE plugins. Users feel forced to context-switch between terminal and editor.

2. **Provider failure handling is manual**: No automatic fallback when API keys expire or rate limits hit. Users must watch for errors and manually `/provider` switch – disruptive during long coding sessions.

3. **UI output friction**: Copying output is hard, confirmation dialogs obscure content. The UI refactor (#2766) represents a long-standing pain point that affects daily use.

4. **API error messages are too generic**: Auth failures (#2665) don't show which provider or key source caused the issue. Multi-provider debugging is confusing.

5. **Unexpected crashes during analysis** (#2847): New `Warn Stream read error` bug appears mid-workflow, losing context. No clear reproduction steps yet – likely a response body deserialization issue.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*