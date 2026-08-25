# AI CLI Tools Community Digest 2026-08-25

> Generated: 2026-08-25 00:30 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report — AI CLI Developer Tools
**Date:** 2026-08-25  
**Prepared by:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tool landscape is maturing rapidly, with eight major tools (Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code, OpenCode, Pi, Qwen Code, and DeepSeek TUI) all actively iterating. The ecosystem is converging on core expectations: reliable background/daemon session management, multi-agent and subagent lifecycle control, robust streaming and error handling, and provider-agnostic architecture. Critical shared pain points include Windows support gaps , OAuth/token persistence fragility, silent data loss, and context window bloat. The tools are differentiating on target users (enterprise vs. local-first), technical approach (Rust vs. Node vs. Go), and provider ecosystems (proprietary vs. open model gateways).

---

## 2. Activity Comparison

| **Tool** | **Issues (Notable Today)** | **PRs (Key Progress)** | **Release Status** |
|----------|---------------------------|----------------------|--------------------|
| **Claude Code** | 10 hot issues (top: Linux segfault #89360, background sessions #88193) | 3 PRs (AWS gateway, pylint CI, MCP config docs) | v2.1.243 (patch, segfault fix) |
| **OpenAI Codex** | 10 hot issues (top: macOS auth invalidation #39162, MultiAgent V1/V2 mismatch #35097) | 10 PRs (credential brokering, OTEL cost metrics, Guardian v2) | rust-v0.150.0-alpha.8 (no notes) |
| **Gemini CLI** | 10 hot issues (top: subagent MAX_TURNS misreported as success #22323, generalist hangs #21409) | 10 PRs (history rollback optimizations, consent prompts, security fixes) | v0.57.0-preview.1 (patch, retry nudge fix) |
| **GitHub Copilot CLI** | 10 hot issues (top: 400 errors #1274, tool whitelist #1973) | 1 PR (README rename — likely artifact) | v1.0.81-9 (patch, model data retention warnings) |
| **Kimi Code** | 2 issues (top: usage billing #1994) | 1 PR (StrReplaceFile UTF-8 fix #2595) | No release |
| **OpenCode** | 10 hot issues (top: TUI sidebar regression #30877, network_error cluster #44328) | 10 PRs (plugin SDK runtime resolution, LSP diagnostics trim, JSON parser) | v1.18.22 (patch) |
| **Pi** | 10 hot issues (top: Windows pain points #7547, auto-compaction #6879) | 10 PRs (PowerShell tool, abort handling, llama.cpp presets) | v0.84.3 (PowerShell tool, staged updates) |
| **Qwen Code** | 10 hot issues (top: stream timeout #5975, architecture review #4063) | 10 PRs (loop detection, review fan-out, session rotation) | Nightly + cua-driver v0.20.0 |
| **DeepSeek TUI** | 10 hot issues (top: provider neutrality #5588, milestone tracker #5573) | 10 PRs (Chat runtime unification, approval receipts, control socket) | v0.9.12 in preparation (no release) |

**Summary:** OpenAI Codex leads PR velocity (10 key PRs); Gemini CLI and DeepSeek TUI show sustained PR activity; Copilot CLI has minimal PR activity (1 artifact) suggesting triage focus; Kimi Code is lowest activity (1 PR).

---

## 3. Shared Feature Directions

The following requirements recur across multiple tool communities :

| **Shared Requirement** | **Tools Asking** | **Specific Pain Point** |
|------------------------|------------------|------------------------|
| **Granular tool permissions / whitelists** | Copilot CLI (#1973, 27👍), Claude Code (approval UX), Gemini CLI (#22672 destructive behavior) | All-or-nothing approval; need read-only tools to run freely, destructive ops require consent |
| **Subagent lifecycle management** | Codex (#39694 thread reclamation), Gemini CLI (#22323 misreported success), DeepSeek TUI (#5596 silent destruction), Qwen Code (#9492 loop detection) | Completed/killed subagents not reclaimed; false thread limits; silent data loss from expensive work |
| **Context/bloat control** | Claude Code (#87137 prompt cache invalidation), Gemini CLI (#28934 history rollback), Pi (#6879 auto-compaction), Qwen Code (#9934 MCP full renders) | Session-scoped strings invalidate caches; compaction not triggered until overflow; token waste |
| **Windows parity** | Codex (#37104, #40048), Copilot CLI (#4570 file locks), Pi (#7547 44 comments), DeepSeek TUI (#5602 ANSI decoding) | Sandbox failures, file-locking, path separators, terminal issues — Windows is consistently second-class |
| **Auth/token persistence** | Codex (#40267 rotated refresh tokens never persisted), Copilot CLI (#4582 Entra ID scope missing) | OAuth flows broken by validation regressions; tokens not persisted; users bounced to sign-in |
| **Silent failure visibility** | Codex (#40010 exit 0), Copilot CLI (#4572 lost tool results), OpenCode (#44788 no plugin events), Gemini CLI (#22323 false success) | Failures that report success or exit 0 make debugging impossible |
| **Provider neutrality** | DeepSeek TUI (#5588 18 gates), OpenCode (#37815 Kimi K3 fails), Pi (Bedrock Mantle), Claude Code (modelPicker) | Hardcoded model/provider assumptions break non-primary providers |
| **Streaming resilience** | Qwen Code (#5975 timeouts), Pi (#7444 retry narrow), OpenCode (#44328 network_error) | Partial chunks, retry classification, abort signals ignored |

---

## 4. Differentiation Analysis

| **Dimension** | **Claude Code** | **OpenAI Codex** | **Gemini CLI** | **Copilot CLI** | **Kimi** | **OpenCode** | **Pi** | **Qwen Code** | **DeepSeek TUI** |
|---------------|----------------|------------------|----------------|-----------------|----------|--------------|-------|--------------|-------------------|
| **Core Language** | TypeScript/Node | Rust | TypeScript/Node | TypeScript/Node | Go | Go | TypeScript/Node | TypeScript/Node | Rust |
| **Target User** | Enterprise, heavy automation | Power users, multi-agent heavy | Google ecosystem, local devs | Enterprise GitHub users | Consumer AI chat users | Open-source tinkerers | Local-first, llama.cpp crowd | Qwen/Aliyun ecosystem | DeepSeek power users |
| **Distinctive Focus** | Background fleets, prompt-cache efficiency | MultiAgent V2, Guardian safety, OTEL observability | AST-aware tools, skills/sub-agent usage, OS sandboxing | GitHub Copilot integration, MCP OAuth, enterprise auth | Token-quota transparency, K2.6 reasoning | TUI polish, plugin API, LSP integration | Windows support, local models, WebSocket resilience | Review pipeline automation, architecture modernization | Provider neutrality, supervised operation, TUI discoverability |
| **Technical Weakness (current)** | Background daemon leaks; PTY corruption | Windows gaps; auth persistence | Sub-agent reliability | MCP handshake fragility; 400 errors | Low community breadth; no releases | 2.0 plugin API instability; network_error cluster | DeepSeek API adjacency constraints; llama.cpp model discovery | Architecture debt (136 files import genai types); TUI flicker | Hardcoded DeepSeek gates; large codebase files (18.7k line lib.rs) |
| **Release Cadence** | High (multiple patch/day) | High (alpha channel) | Medium (preview + nightly) | Low (patch weekly) | Low (no 24h release) | Medium (patch) | Medium (patch) | High (nightly) | Preparing v0.9.12 |

---

## 5. Community Momentum & Maturity

- **Most active communities:** Codex (51 comments on #39162, 31👍), Copilot CLI (#1274 at 27 comments), Gemini CLI (#22323 at 13 comments, P1), Pi (#7547 with 44 comments on Windows).
- **Most rapidly iterating:** Claude Code (patch cadence daily), Qwen Code (nightly releases), DeepSeek TUI (72-commit integration branch preparing v0.9.12), Codex (10 active PRs in 24h).
- **Declining/latent:** Copilot CLI (1 PR artifact only — possibly focused on triage), Kimi Code (low activity, 1 PR).
- **Maturity signals:** Codex's OTEL cost metrics, Guardian v2 refinements, and credential brokering indicate production-heavy usage. DeepSeek TUI's provider-neutrality audit (18 gates) shows architectural self-awareness. Claude Code's prompt-cache-aware design concerns signal heavy production load.
- **Community frustration peaks:** Windows issues (Codex #37104 unanswered, Copilot CLI #1274 unanswered, Pi #7547 gathering feedback), auth bugs (Codex #39162 31👍, Copilot CLI #4582), and silent failures (Codex #40010, Gemini CLI #22323).

---

## 6. Trend Signals

**For developers and tool builders:**

1. **Multi-agent orchestration is fragile everywhere.** Subagent lifecycle management (reclaim, post-turn survival, trajectory sharing) is an unsolved problem across Codex, Gemini, DeepSeek, and Qwen. **Opportunity:** Standardized agent lifecycle APs (spawn, reclaim, share traces) could be a differentiator.

2. **Silent failures are the #1 trust killer.** Zero-exit-codes (Codex #40010), false success reporting (Gemini #22323), and lost tool results (Copilot #4572) all destroy confidence. **Signal:** Tools that implement explicit failure surfacing (distinct abort reasons, non-zero exits, mandatory error payloads) will win production users.

3. **Windows is underserved, but users are loud.** Four of nine tools have Windows-specific issues causing real pain. With Pi adding a PowerShell tool and Codex and Copilot struggling, there is a clear market gap. **Signal:** A tool that gets Windows parity right (path handling, no file locks, sandbox support) will capture a loyal segment.

4. **Token/context transparency is a rising expectation.** From Claude Code's `/usage` Loops breakdown to Kimi Code's billing controversy, to Qwen and DeepSeek's cost attribution features, users demand visibility into why tokens are spent. **Signal:** Budget-aware design (compaction, cost metrics, schema-cost display) is becoming table stakes.

5. **Config drift and auto-migration are breaking trust.** Codex #40339 (invalid permissions block) and Qwen #8965 (settings schema rejects runtime-honored values) show auto-migration and schema mismatches cause real damage. **Signal:** Strict, validated, conservative configuration defaults are preferred over silent behavior changes.

6. **Prompt-cache-aware design is a competitive advantage.** Claude Code's #87137 highlights how session-scoped URLs invalidate cache; Gemini's #28934 optimizes retry nudges to maximize prefix caching. **Signal:** As API costs rise, cache-aware tool design (serialize stable prefixes, avoid session-scoped strings in tool definitions) is a hidden differentiation.

7. **Provider neutrality is no longer optional.** DeepSeek TUI (18 gates), OpenCode (Kimi K3 failures), Pi (Bedrock Mantle) all show that community users expect multi-provider support to be a first-class feature, not an afterthought. **Signal:** Tools hardcoded to one provider/model will struggle to retain users as open and alternative models proliferate.

---

*Data sourced from community digests for 2026-08-25 across Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-08-25 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following PRs have generated the most community discussion and represent significant contributions to the Skills ecosystem:

### 1.1 skill-creator: run_eval.py Fix Bundle
- **PR**: [anthropics/skills#1298](https://github.com/anthropics/skills/pull/1298) (MartinCajiao)
- **Status**: Open | Created: 2026-06-10 | Updated: 2026-06-23
- **Function**: Fixes the critical `run_eval.py` bug where all skill descriptions report 0% recall, rendering the entire description-optimization loop useless. The fix installs the eval artifact as a real skill, addresses Windows stream reading, trigger detection, and parallel worker issues.
- **Discussion Highlights**: Directly responds to [Issue #556](https://github.com/anthropics/skills/issues/556), which has 10+ independent reproductions and 7 👍. This is the single most-impactful pending fix for the skill-creator pipeline — the optimization loop is currently "optimizing against noise."

### 1.2 document-typography: Typographic Quality Control
- **PR**: [anthropics/skills#514](https://github.com/anthropics/skills/pull/514) (PGTBoos)
- **Status**: Open | Created: 2026-03-04 | Updated: 2026-03-13
- **Function**: Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents — issues affecting every document Claude generates.
- **Discussion Highlights**: The skill addresses a universally-experienced pain point (typographic slop in generated docs), making it broadly applicable across the ecosystem.

### 1.3 ODT Skill: OpenDocument Creation and Parsing
- **PR**: [anthropics/skills#486](https://github.com/anthropics/skills/pull/486) (GitHubNewbie0)
- **Status**: Open | Created: 2026-03-01 | Updated: 2026-04-14
- **Function**: Creates, fills, reads, and converts OpenDocument Format files (`.odt`, `.ods`), with triggers for 'ODT', 'ODS', 'ODF', 'OpenDocument', and 'LibreOffice document' requests.
- **Discussion Highlights**: Extends the document skills family (docx, pdf) with the open-source ISO-standard format — a significant gap in the current collection.

### 1.4 frontend-design Clarity and Actionability Revision
- **PR**: [anthropics/skills#210](https://github.com/anthropics/skills/pull/210) (justinwetch)
- **Status**: Open | Created: 2026-01-05 | Updated: 2026-03-07
- **Function**: Revises the frontend-design skill to ensure every instruction is actionable in a single conversation, with specific enough guidance to steer behavior without ambiguity.
- **Discussion Highlights**: Addresses the broader problem of skills being written more like developer documentation than operational instructions — a theme echoed in [Issue #202](https://github.com/anthropics/skills/issues/202) about skill-creator's verbosity.

### 1.5 Hivemind: Zero-Cost Multi-Agent Orchestration
- **PR**: [anthropics/skills#1628](https://github.com/anthropics/skills/pull/1628) (Hanishchow)
- **Status**: Open | Created: 2026-08-21 | Updated: 2026-08-24
- **Function**: Delegates mechanical work to headless opencode workers running on free models, while Claude Code remains the only planner, reviewer, and merger. Optimizes around the insight that "the expensive model's context is the scarce resource."
- **Discussion Highlights**: Active as of data collection — represents an emerging demand for multi-agent orchestration and cost optimization.

### 1.6 self-audit: Mechanical Verification + Reasoning Quality Gate
- **PR**: [anthropics/skills#1367](https://github.com/anthropics/skills/pull/1367) (YuhaoLin2005)
- **Status**: Open | Created: 2026-06-28 | Updated: 2026-07-02
- **Function**: Audits AI output before delivery — mechanical file verification first, then a four-dimension reasoning audit in damage-severity priority order. Universal across projects and tech stacks.
- **Discussion Highlights**: Part of a broader quality-gate movement (see related [Issue #1385](https://github.com/anthropics/skills/issues/1385)) focused on verification and adversarial review before delivery.

### 1.7 testing-patterns: Comprehensive Testing Stack
- **PR**: [anthropics/skills#723](https://github.com/anthropics/skills/pull/723) (4444J99)
- **Status**: Open | Created: 2026-03-22 | Updated: 2026-04-21
- **Function**: Covers Testing Trophy model, unit testing (AAA pattern, naming), React component testing (Testing Library), and what to test vs. what NOT to test.
- **Discussion Highlights**: Addresses a high-demand area — rigorous code quality practices as a transferable skill.

---

## 2. Community Demand Trends

Distilled from the most-discussed issues, four dominant demand directions emerge:

### 2.1 Trust and Security in Skill Distribution
- [Issue #492](https://github.com/anthropics/skills/issues/492) (43 comments, 2 👍): The most-discussed issue, raising a **critical security vulnerability** — community skills distributed under the `anthropic/` namespace impersonate official skills, enabling trust boundary abuse. This is the community's #1 concern by engagement.

### 2.2 Enterprise Collaboration and Sharing
- [Issue #228](https://github.com/anthropics/skills/issues/228) (16 comments, 8 👍): Demand for **org-wide skill sharing** directly in Claude.ai, eliminating manual .skill file transfers via Slack/Teams.

### 2.3 Skill-Creation Tooling Reliability
- [Issue #556](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍): The `run_eval.py` trigger-rate bug is the top technical pain point — it invalidates the entire skill-optimization workflow.

### 2.4 AI-Generated Document Quality
- [Issue #12](https://github.com/anthropics/skills/issues/12) (4 comments): Document corruption from whitespace reformatting in docx/ooxml — a recurring quality concern paired with PR #514 (typography).

---

## 3. High-Potential Pending Skills

These open PRs are actively discussed and appear likely to land:

| Skill | PR | Function | Signal |
|-------|----|----------|--------|
| **scnet-hpc** | [#1615](https://github.com/anthropics/skills/pull/1615) | HPC cluster operation via SSH/Slurm profiles | Active updates through 2026-08-24 |
| **ServiceNow Platform** | [#568](https://github.com/anthropics/skills/pull/568) | ITSM, SecOps, ITAM/SAM, FSM, SPM, CSDM, IntegrationHub | Extensive scope; continuously updated |
| **pyxel Retro Games** | [#525](https://github.com/anthropics/skills/pull/525) | MCP server for Pyxel engine (write → run → iterate) | 4+ months of refinement |
| **skill-quality-analyzer + skill-security-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Meta skills evaluating SKILL.md quality across 5 dimensions | Directly addresses trust/quality concerns from Issue #492 |
| **SAP-RPT-1-OSS Predictor** | [#181](https://github.com/anthropics/skills/pull/181) | SAP tabular foundation model for predictive analytics | Niche enterprise vertical |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliability infrastructure — fixing and securing the skill-development pipeline itself (trust boundaries, evaluation accuracy, cross-platform stability) before expanding into new application domains.**


---

# Claude Code Community Digest — 2026-08-25

## 1. Today's Highlights

Claude Code shipped v2.1.243 with a new `/usage` Loops breakdown for spotting runaway loop tasks. Today's issue tracker is dominated by a critical Linux regression (v2.1.242 segfaults on every launch due to a mimalloc NULL-check bug) and a constellation of background/daemon session bugs — memory leaks, stale workers, PTY corruption, and environment-variable loss when forking to the background. The v2.1.242 segfault is already fixed in 2.1.243, but community members remain vocal about the background-session stability and resource-management issues.

## 2. Releases

**v2.1.243** — Adds a Loops breakdown to `/usage`: per-loop run count, total tokens, tokens per run, and last run time, so runaway or chatty `/loop` tasks are easy to spot. Also adds a `modelPicker` setting to curate the `/model` picker with an ordered, labeled list of models (accepts any id spelling). Notably, this release **fixes the v2.1.242 Linux segfault**.

## 3. Hot Issues

1. **[#89360 — [BUG] 2.1.243 Segmentation fault (Linux, regression)](https://github.com/anthropics/claude-code/issues/89360)** — 13 comments, 3 👍. A segfault in 2.1.243 on Linux with a repro. The most actively discussed bug today; the community is watching whether this is a full fix for the 2.1.242 mimalloc regression. **Why it matters:** Crash-on-launch is a showstopper for production users.

2. **[#89334 — v2.1.242 segfaults on every launch; mimalloc `free` has no NULL check](https://github.com/anthropics/claude-code/issues/89334)** — 4 comments, 4 👍. Detailed root-cause: 2.1.242 was the first build to export its bundled mimalloc as a versioned glibc allocator symbol. A precise bug report with a clean bisect (2.1.241 unaffected). **Why it matters:** Demonstrates the value of fast, precise regression reports; the fix landed in 2.1.243.

3. **[#88193 — Background sessions: resume-by-id fails, sessions share names, no doc'd way out](https://github.com/anthropics/claude-code/issues/88193)** — 4 comments. A session becomes unrecoverable through the UI; the documented recovery path (resume by id) fails, and the picker cannot disambiguate. **Why it matters:** Sheer frustration with background-session lifecycle management.

4. **[#87137 — Bash tool description embeds per-session URL, invalidating prompt cache on every `/resume`](https://github.com/anthropics/claude-code/issues/87137)** — 3 comments. Tool definitions are serialized ahead of the system prompt, so a session-specific URL in the Bash tool description invalidates the entire cached prefix on every resume — a full re-read cost. **Why it matters:** A subtle but costly performance bug for heavy `/resume` users.

5. **[#50358 — Drive MCP `create_file` silently truncates binary uploads ~10K base64 chars](https://github.com/anthropics/claude-code/issues/50358)** — 10 comments, 4 👍. A long-running (since April) external MCP bug now getting attention: silently truncates binary uploads (e.g., a 12 KB xlsx). **Why it matters:** Silent data loss with Google Drive is dangerous for automation workflows.

6. **[#85470 — FleetView TUI render loop frozen while attached to background fleet session](https://github.com/anthropics/claude-code/issues/85470)** — 3 comments. The TUI stops processing input; it still reads stdin but never acts. **Why it matters:** Core multi-session management is unusable for some users despite 4 occurrences in 3 hours.

7. **[#85888 — Held-for-approval cross-session message has no approval UI — parked forever](https://github.com/anthropics/claude-code/issues/85888)** — 2 comments, 1 👍. A cross-session approval request to a background recipient never surfaces an approval UI. **Why it matters:** Blocks workflow completion with no visible path forward.

8. **[#87163 — `sandbox.network.strictAllowlist` has no effect; bwrap never invoked (closed)](https://github.com/anthropics/claude-code/issues/87163)** — 2 comments. The strict network allowlist setting was reported as a no-op on Linux; the Bash tool dispatcher never invokes bwrap. **Why it matters:** A security-relevant sandbox feature silently doing nothing — now closed, presumably fixed or addressed.

9. **[#87891 — Background daemon never reaps stale workers or unclaimed spares (64 leaked processes / ~7.1 GB after 6 weeks)](https://github.com/anthropics/claude-code/issues/87891)** — 2 comments. Long-running daemons accumulate memory and processes across restarts. **Why it matters:** A slow-burn production stability issue for always-on machines.

10. **[#89365 — Model crashes during validation tasks](https://github.com/anthropics/claude-code/issues/89365)** — 0 comments. A fresh report (v2.1.235) of repeated model crashes during validation tasks, though the JSON error body is empty. **Why it matters:** An under-reported but potentially serious crash; needs community repro.

## 4. Key PR Progress

1. **[#79898 — Add Claude apps gateway on AWS example deployment assets (closed)](https://github.com/anthropics/claude-code/pull/79898)** — Reference deployment artifacts for running the Claude apps gateway on AWS with Amazon Bedrock, with accompanying docs at code.claude.com. Sibling to the existing `examples/gateway/gcp` assets. **Why it matters:** Gives AWS-centric teams a first-class reference path.

2. **[#83890 — Create pylint.yml (open)](https://github.com/anthropics/claude-code/pull/83890)** — A community PR adding a Pylint CI workflow. Minimal description. **Why it matters:** Small but signals community interest in better linting/static-analysis practices in the repo.

3. **[#75252 — docs: clarify plugin MCP configuration scope (closed)](https://github.com/anthropics/claude-code/pull/75252)** — Clarifies that plugin `mcpServers` configuration is scoped to plugin-bundled MCP server definitions, separate from user-level MCP allow/deny list settings. Reopened from a deleted fork. **Why it matters:** Resolves long-standing confusion about MCP config scope for plugin authors.

## 5. Feature Request Trends

- **Better background/agent session lifecycle management:** The dominant theme. Users repeatedly ask for clear, documented recovery paths (resume-by-id that works), session naming/disambiguation, and the ability to distinguish live vs. stalled sessions.
- **Resource governance for daemons/background workers:** Requests for memory caps, worker reaping, and explicit shutdown/cleanup controls for always-on `claude agents` fleets.
- **Prompt-cache-aware design:** Requests that tool descriptions and session-scoped strings not invalidate the cache on resume — a cost/performance concern from heavy users.
- **Sandbox enforcement visibility:** Asking for clearer indications that networking sandboxing (strictAllowlist) is actively applied, plus logging when bwrap is skipped.

## 6. Developer Pain Points

- **Background-session environment drift:** The daemon strips or mutates environment variables (`TMUX`, `CLAUDE_CODE_SKIP_VERTEX_AUTH`, `XPC_FLAGS`, etc.), breaking DNS, tmux buffers, and Vertex auth — a recurring, high-frequency complaint across platforms.
- **Session identity confusion:** `--resume <id> --bg` forks a new session instead of waking the original; left-arrow backgrounding continues under a new session id; the picker shows duplicates. Users describe sessions becoming "permanently unreachable."
- **Memory/process leaks in the background daemon:** Multiple reports (RSS saturation to 24GB; 64 leaked processes; 7.1GB after six weeks) suggest a systematic problem in daemon worker recycling.
- **Silent data/behavior loss:** Truncated binary uploads (Drive MCP), zero plugin skills on ~1-in-44 background sessions, and lost conversation context on resume — all "silently wrong" behaviors that erode trust.
- **PTY and TUI corruption:** Resizing one terminal corrupts rendering in another attached to the same session; re-homing a background session corrupts the PTY across terminal close/reopen; SIGWINCH is never delivered to background sessions.

*Sources: [GitHub — anthropics/claude-code releases](https://github.com/anthropics/claude-code/releases), [issues](https://github.com/anthropics/claude-code/issues), [pull requests](https://github.com/anthropics/claude-code/pulls).*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-25

## Today's Highlights

The Codex ecosystem is grappling with a cluster of Windows-specific stability issues (sandbox setup failures, kernel crashes, MSIX updater loops) alongside a critical macOS auth regression that signs users out when resuming threads. The team shipped `rust-v0.150.0-alpha.8` (no release notes provided) and merged a substantial batch of cleanup and hardening PRs, including credential brokering for child environments, OTEL cost metrics, and Guardian v2 scope refinements. Multi-agent lifecycle bugs — particularly subagent threads not being reclaimed and queue messages pinning residency slots — remain a hot area of community frustration.

## Releases

- **[rust-v0.150.0-alpha.8](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.8)**: No release notes provided beyond the version bump. Pre-release channel users should exercise caution; watch for regressions in the areas covered by the issues below.

## Hot Issues

1. **[#39162 — Opening existing conversation invalidates ChatGPT auth and redirects to sign-in](https://github.com/openai/codex/issues/39162)** (51 comments, 👍31)  
   A macOS-only regression where resuming a thread invalidates ChatGPT auth and bounces to sign-in. The 3-day-old comment thread suggests this is widespread and blocking daily workflows. Highly upvoted, actively debated.

2. **[#35097 — gpt-5.6-luna marked as MultiAgent V1, so V2 spawn_agent rejects it](https://github.com/openai/codex/issues/35097)** (29 comments, 👍51)  
   One of the most-upvoted open issues. The model catalog labels a current model as V1-only, breaking MultiAgent V2 workflows despite the model otherwise supporting it. Community wants the catalog fixed or a fallback path added.

3. **[#35746 — Paginated history drops valid flattened rollout records and reuses ordinals](https://github.com/openai/codex/issues/35746)** (25 comments, 👍1)  
   A subtle but critical data-integrity bug in CLI rollout history. Pagination can drop records and reuse ordinals, meaning session history can be silently corrupted. High comment count suggests reproduceability and frustration.

4. **[#39903 — Option to disable “Ran N commands” collapsing in TUI](https://github.com/openai/codex/issues/39903)** (21 comments, 👍36)  
   A highly requested UX enhancement. Users want to see all executed commands in the TUI instead of collapsed summaries. Strong community support; simple ask, potentially easy win for maintainers.

5. **[#37104 — Windows/WSL integrated terminal silently fails before PTY startup](https://github.com/openai/codex/issues/37104)** (19 comments, 👍9)  
   Windows/WSL users report the integrated terminal and side/bottom panels fail silently. Has been open since early August; no maintainer response visible — a growing pain point.

6. **[#40267 — Thread resume signs out desktop; rotated refresh token never persisted](https://github.com/openai/codex/issues/40267)** (7 comments)  
   A deeper version of #39162 with concrete evidence: refresh tokens are rotated but never written to `auth.json`, and fresh logins are invalidated within 76 seconds. This is likely the root cause of #39162.

7. **[#40048 — Windows Chrome/Computer Use fails with about:blank and JS kernel timeout](https://github.com/openai/codex/issues/40048)** (7 comments)  
   Browser automation is broken on Windows in multiple ways. Users with Pro plans report the feature is effectively unusable.

8. **[#39694 — Completed subagent threads not reclaimed; false “agent thread limit reached”](https://github.com/openai/codex/issues/39694)** (5 comments)  
   Long-running tasks hit an artificial limit because completed subagents are never freed. Directly impacts production workloads with heavy subagent usage.

9. **[#40339 — config.toml migration generates invalid permissions block breaking --strict-config](https://github.com/openai/codex/issues/40339)** (5 comments)  
   Auto-migration after `npm install` writes a `permissions.<name>` block that fails strict config parsing, and `sandbox_workspace_write.network_access` is silently ignored. Configuration drift and silent behavior changes.

10. **[#40010 — app-server silently exits 0 mid-turn after shell tool calls in read-only sandbox](https://github.com/openai/codex/issues/40010)** (3 comments)  
   Zero-exit-code crashes on macOS in read-only sandboxes. No error, no signal, no notification — makes debugging very hard. Particularly concerning for automation pipelines.

## Key PR Progress

1. **[#40501 — Deduplicate plugin skills in unified mentions](https://github.com/openai/codex/pull/40501)**  
   Adds nullable `pluginId` to `SkillMetadata` so clients can deduplicate skills shown alongside their owning plugin in `@` search. Clean UX improvement.

2. **[#40499 — Harden startup rollout migration against concurrent updates](https://github.com/openai/codex/pull/40499)**  
   Prevents race conditions where another process writes/archives/compresses a rollout during startup migration. Likely fixes intermittent session-history corruption.

3. **[#40495 — Suggest conversation-based thread titles in `/rename`](https://github.com/openai/codex/pull/40495)**  
   Generates a title suggestion from recent messages when `/rename` opens, prefilled but editable. Small quality-of-life win.

4. **[#40492 — Generate descriptive TUI thread titles](https://github.com/openai/codex/pull/40492)**  
   Provisional titles from first user message, replaced asynchronously with normalized generated titles. Manual renames are preserved.

5. **[#40491 — Honor response budgets when reading skill resources](https://github.com/openai/codex/pull/40491)**  
   Sizes `skills.read` pages to the current call’s response budget. Fixes page overflow for a smaller tool-call limit.

6. **[#40488 — Export turn cost as an OTEL metric](https://github.com/openai/codex/pull/40488)**  
   New `codex.turn.cost_microusd` counter with turn/conversation/interruption/speed/reasoning-effort attributes. Useful for cost tracking and observability.

7. **[#40484 — Broker credential aliases in child environments](https://github.com/openai/codex/pull/40484)**  
   Discovers inherited credentials even when canonical provider variable is filtered from the child environment and replaces matching values in longer strings. Important for sandboxed and subagent environments.

8. **[#40481 — Support managed AWS access keys for Amazon Bedrock](https://github.com/openai/codex/pull/40481)**  
   Adds experimental `amazonBedrockAccessKeys` login flow with SigV4-signed requests and a distinct `bedrockAccessKeys` auth mode. Expands provider support.

9. **[#40480 — Add computer-use-only Guardian v2 review scope](https://github.com/openai/codex/pull/40480)**  
   Restricts async classification/fast approvals to browser and computer-use REPL tools via `features.guardianv2.review_scope.computer_use_only`. Keeps other tools on synchronous approval.

10. **[#40490 — Harden project config when credential brokering is active](https://github.com/openai/codex/pull/40490)**  
    Prevents project configuration from influencing credential-provider environment variables or shell startup behavior while broker is active. A security-hardening step.

## Feature Request Trends

- **TUI transparency**: Users keep asking for more control over what the TUI shows — `#39903` (disable command collapsing) and `#36873` (multiple independent Codex views in VS Code). **Trend: users want more UI control and less implicit collapsing/abstraction.**
- **Agent lifecycle management**: Subagent reclamation and residency-slot management (`#39694`, `#35209`, `#32353`) indicate a need for explicit agent-thread lifecycle controls, including reclaim and queue semantics.
- **Compaction control**: `#21777` (auto-compaction exposed to the agent) reflects a recurring desire to let the agent (and user) influence compaction behavior during long runs.
- **Auth resilience**: `#39162` and `#40267` point toward a need for more robust OAuth token persistence and refresh handling on desktop.
- **Config predictability**: `#40339` and `#21777` both touch on configuration behavior that is either silent or undocumented. Users want strict, predictable config semantics.

## Developer Pain Points

- **Windows is a second-class citizen right now**: Sandbox setup failures (`0xc0000142`, `#34928`), kernel crashes (`#40119`), TUN/proxy timeouts (`#38768`), updater loops (`#38843`), and broken Computer Use (`#40048`) all point to systemic Windows stability gaps. Multiple issues have gone weeks without maintainer response.
- **Auth invalidation on resume**: The macOS sign-out-on-resume bug (`#39162`, `#40267`) is highly disruptive, especially for Pro users. The root cause (rotated refresh tokens never persisted) suggests a persistence-layer bug that may also affect other platforms.
- **Silent failures**: Multiple issues (`#40010` exit 0, `#37104` silent terminal failure, `#38843` permanent suspension) involve code paths that fail without any error surfaced to the user. Developers and automation operators can’t debug what never reports.
- **Subagent accounting**: The combination of thread-limit false positives (`#39694`) and residency-slot pins (`#32353`) makes long-running multi-agent workflows unreliable. This is the most common pain point for heavy users.
- **Config auto-migration footguns**: `#40339` shows auto-migration writing invalid config blocks and silently ignoring settings. Users want migration to be more conservative or at least validated against `--strict-config` before writing.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-25

## Today's Highlights

A patch release (v0.57.0-preview.1) landed today, cherry-picking a fix to address history rollback and retry nudge optimizations—targeting context window bloat and API request volume. The maintainer-tracked backlog continues to surface a cluster of sub-agent reliability issues (hangs, misreported termination reasons, and browser failures on Wayland), alongside a security-hardening push in open PRs around extension consent, credential sanitization, and A2A server misconfigurations. Community discussions remain active around improving agent self-awareness, AST-aware tooling, and persistent task tracking.

---

## Releases

### [v0.57.0-preview.1](https://github.com/google-gemini/gemini-cli/releases/tag/v0.57.0-preview.1)
Patch release cherry-picking commit `812f7a2` from PR [#28934](https://github.com/google-gemini/gemini-cli/pull/28934) to the preview branch. The underlying PR optimizes tool call cancellations and retry nudges to prevent context window bloat, reduce API request volume, and maximize prefix caching efficiency.

*Full changelog:* https://github.com/google-gemini/gemini-cli/compare/v0.57.0-preview.0...v0.57.0-preview.1

### [v0.56.0-nightly.20260824.g5411f113c](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260824.g5411f113c)
Standard nightly build.

---

## Hot Issues (Top 10)

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 13 comments | 👍2)
   A `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even though it hit the turn limit before doing any work. This masks real failures and erodes trust in subagent reporting. High community engagement.

2. **[#21409 — Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 8 comments | 👍8)
   Simple operations like folder creation hang forever when delegated to the generalist agent. Workaround: instructing the model to avoid sub-agents. Strong reaction—8 upvotes signals broad impact.

3. **[#25166 — Shell command stuck "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 4 comments | 👍3)
   Simple CLI commands hang in "Awaiting user input" state even after finishing—no interactive prompts involved. Disrupts automation flows.

4. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, 4 comments | 👍1)
   Browser agent fails to start on Wayland. Linux desktop users are affected; likely a display-server detection issue.

5. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, 5 comments)
   Sessions deemed "low signal" are never marked processed, causing repeated extraction attempts. Wasteful API calls and potential loop.

6. **[#26525 — Deterministic redaction and reduced Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, 4 comments)
   Transcript content is sent to models before redaction happens, and skill definitions may leak to logs. Privacy and data-hygiene concern.

7. **[#21968 — Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, 6 comments)
   Even with well-described custom skills ("gradle", "git"), the model rarely uses them autonomously. Anecdotal but recurring pattern.

8. **[#19873 — Zero-dependency OS sandboxing via model's bash affinity](https://github.com/google-gemini/gemini-cli/issues/19873)** (P2, 8 comments | 👍1)
   Proposed architecture to leverage Gemini's native bash abilities with safer post-execution intent routing. Ambitious but high-value.

9. **[#22745 — AST-aware file reads and codebase mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (P2, 7 comments)
   Epic tracking investigations into AST-aware tools for precise method-bound reads, reduced token noise, and better navigation.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, 3 comments | 👍1)
    Model occasionally uses `git reset` or `--force` when safer alternatives exist. Reliability and safety concern for complex ops.

---

## Key PR Progress (Top 10)

1. **[#29024 — Cherry-pick fix to v0.57.0-preview.1](https://github.com/google-gemini/gemini-cli/pull/29024)** (merged)
   Automates cherry-pick of history rollback/retry nudge optimizations into the preview release.

2. **[#28934 — History rollback and retry nudge optimizations](https://github.com/google-gemini/gemini-cli/pull/28934)** (merged)
   Optimizes tool cancellation and retry nudges to cut context bloat and API volume, maximizing prefix caching.

3. **[#28914 — Inject on-retry nudge into conversation contents](https://github.com/google-gemini/gemini-cli/pull/28914)** (open, P1)
   Fixes [#28909](https://github.com/google-gemini/gemini-cli/issues/28909) by moving retry nudges from `systemInstruction` into `contents` to preserve prefix caching and improve recovery.

4. **[#28939 — Avoid persisting interrupted response placeholder](https://github.com/google-gemini/gemini-cli/pull/28939)** (open, P1)
   Fixes [#28927](https://github.com/google-gemini/gemini-cli/issues/28927) — prevents models from repeating "[The previous response was interrupted...]" as synthetic responses.

5. **[#28938 — Keep GIT_CONFIG_* environment triplets consistent](https://github.com/google-gemini/gemini-cli/pull/28938)** (open, P1)
   Prevents sanitized Git config env vars from becoming unparsable when redaction removes half of a key/value pair.

6. **[#29022 — Retain ask_user questions in history](https://github.com/google-gemini/gemini-cli/pull/29022)** (open)
   New `ui.keepAskUserQuestionsInHistory` option preserves question context for resumed sessions.

7. **[#28961 — Fix write policy safety checker declarations](https://github.com/google-gemini/gemini-cli/pull/28961)** (merged)
   Realigns safety checker config in `write.toml` so `AllowedPathChecker` is correctly registered.

8. **[#29018 — Remove misleading security schemes and hardcoded credentials](https://github.com/google-gemini/gemini-cli/pull/29018)** (open)
   Fixes [#29001](https://github.com/google-gemini/gemini-cli/issues/29001) — strips insecure hardcoded credentials from A2A server agent cards.

9. **[#28863 — Consent prompts for extension environment changes](https://github.com/google-gemini/gemini-cli/pull/28863)** (open)
   Sanitizes runtime-altering env vars injected into MCP server processes; extends consent strings.

10. **[#29017 — Dedupe symlinked skill directories](https://github.com/google-gemini/gemini-cli/pull/29017)** (open, P3)
    Fixes [#28944](https://github.com/google-gemini/gemini-cli/issues/28944) — handles `.gemini` → `.agents` symlink/junction deduplication.

---

## Feature Request Trends

- **AST-aware tooling**: Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) push for AST-aware file reads, search, and codebase mapping to reduce token usage and improve navigation precision.
- **Persistent, file-based task tracking**: Replace in-context `WriteToDo` with durable CRUD-based tracking ([#18836](https://github.com/google-gemini/gemini-cli/issues/18836)) to avoid context rot and memory loss.
- **OS-level sandboxing with intent routing**: Leverage Gemini's native bash skills safely via zero-dependency sandboxing and post-execution intent analysis ([#19873](https://github.com/google-gemini/gemini-cli/issues/19873)).
- **Agent self-awareness**: Better understanding of its own CLI flags, hotkeys, and capabilities so it can guide users accurately ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)).
- **Subagent trajectory sharing**: Expose subagent traces via `/chat share` for easier debugging and evaluation ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)).
- **Browser agent resilience**: Automatic session takeover and lock recovery for persistent browser profiles ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)).

---

## Developer Pain Points

- **Sub-agent reliability**: Recurring hangs, misreported success, and silent failures are eroding confidence—multiple P1 bugs open with high engagement.
- **Terminal UX friction**: Stuck "Waiting input" states after completed commands and flicker on terminal resize are common complaints.
- **Context bloat and token waste**: Large file reads "firehose" context; repeated low-signal session retries burn API quota.
- **Security & privacy gaps**: Transcript content sent to models before redaction; skill definitions potentially leaked to logs; hardcoded credentials in A2A server metadata.
- **Destructive command usage**: Concern that the model reaches for `git reset`/`--force` without exploring safer alternatives.
- **Documentation drift**: Multiple PRs this week correcting missing or incorrect CLI flags and configuration keys, indicating docs lag behind implementation.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-25

## Today's Highlights
The Copilot CLI team shipped a minor reliability patch (v1.0.81-9) adding model data retention warnings to the `/model` picker. Meanwhile, the community is actively surfacing pressing issues around OAuth interoperability failures with Microsoft Entra ID and Atlassian MCP servers, alongside growing demand for safer tool-approval granularity in interactive mode and multi-turn `/ask` support.

---

## Releases
**v1.0.81-9** — Patch release focused on transparency: users now see data retention warnings with relevant documentation links directly in the `/model` picker, helping developers make more informed privacy choices when selecting models.

🔗 [View release](https://github.com/github/copilot-cli/releases)

---

## Hot Issues (10 Noteworthy)

1. **[#1274 — CLI constantly getting 400 errors for invalid request body](https://github.com/github/copilot-cli/issues/1274)**  
   *27 comments, 11 👍*  
   A long-running, high-impact bug where ~95% of code review prompts fail with 400 errors. Community suspects either server-side validation or malformed CLI request crafting. Debug logs included, but no fix yet — a persistent pain point for daily users.

2. **[#1973 — Feature Request: Tool whitelist for Interactive Mode](https://github.com/github/copilot-cli/issues/1973)**  
   *12 comments, 27 👍*  
   Strongly upvoted request for granular tool permissions. Users want read-only operations (grep, cat, git log) to run without approval while still blocking destructive actions — the current all-or-nothing `/allow-all` approach is too risky.

3. **[#4490 — Atlassian MCP OAuth authentication broken in 1.0.80](https://github.com/github/copilot-cli/issues/4490)**  
   *5 comments*  
   A regression introduced in v1.0.80 breaking OAuth against Atlassian MCP servers due to strict RFC 8414 §3.3 issuer validation. Closed, but follow-up reports (see #4584) suggest the fix may not be complete.

4. **[#4224 — OTel spans for subagent calls omit billing attributes](https://github.com/github/copilot-cli/issues/4224)**  
   *3 comments, 1 👍*  
   Subagent model calls (via the `task` tool) don't emit `github.copilot.nano_aiu` or `github.copilot.cost` attributes in OpenTelemetry spans, causing external cost accounting to undercount actual AI credit usage. A real concern for teams managing spend at scale.

5. **[#4582 — MCP OAuth omits 'scope' parameter for Entra ID servers](https://github.com/github/copilot-cli/issues/4582)**  
   *2 comments*  
   Entra ID (Microsoft) OAuth flows fail with AADSTS900144 because the `scope` parameter is missing when using static `oauthClientId`. Blocks enterprise users connecting to Microsoft-backed MCP servers.

6. **[#4421 — MCP initialize handshake fixed 60s budget, no retry](https://github.com/github/copilot-cli/issues/4421)**  
   *2 comments*  
   npx-launched stdio MCP servers fail ~29% of sessions due to a hard-coded 60-second handshake timeout with no retry or backoff. Once failed, the server is dead for the entire session — a major reliability concern.

7. **[#4566 — Agent repeatedly acknowledges work without executing tool actions](https://github.com/github/copilot-cli/issues/4566)**  
   *2 comments, 1 👍*  
   A behavioral bug where the agent (gpt-5.3-codex) verbally confirms tasks but never actually invokes tools. Particularly problematic for unattended automation workflows.

8. **[#4572 — Background compaction loses parallel GPT tool result, causes HTTP 400](https://github.com/github/copilot-cli/issues/4572)**  
   *1 comment*  
   After automatic background context compaction, long-context sessions fail with "No tool output found for function call." The tool executed successfully, but the JSONL event stream loses the result — data-integrity bug affecting reliability.

9. **[#4570 — Windows: plugin install fails while VS Code is running](https://github.com/github/copilot-cli/issues/4570)**  
   *1 comment*  
   On Windows, any `plugin install` or `plugin update` fails with "Access is denied (os error 5)" if VS Code is open. Requires closing the editor — a disruptive workflow blocker for plugin users.

10. **[#4568 — `--cloud` owner picker hangs, reconnect crashes, task polling hits 429](https://github.com/github/copilot-cli/issues/4568)**  
    *1 comment*  
    A multi-symptom cloud-mode failure: hangs at "Loading available owners..." without repo context, provisioning timeouts with context, and frequent 429 rate-limit errors during task polling. Cloud workflows remain fragile.

---

## Key PR Progress

> ⚠️ **Note:** Only 1 PR was updated in the last 24 hours. The team's current focus appears to be on issue triage and the release pipeline rather than new features.

1. **[#4573 — Rename README.md to README.mdmain](https://github.com/github/copilot-cli/pull/4573)**  
   A trivial, likely accidental rename PR — probably a bot/test artifact or a user error. Watch for maintainer response and closure.

---

## Feature Request Trends

1. **Granular Tool Permissions (Interactive Mode)** — **#1973 (27 👍)** remains the most upvoted feature request: a whitelist system so read-only tools run freely while destructive operations still require approval. Clear pain point with the current `/allow-all` binary.

2. **Multi-turn `/ask` Conversations** — **#4577, #4538** (both from the same author, filed twice) request the ability to have follow-up conversations inside `/ask` without polluting the main session history. Useful for iterative Q&A without context bloat.

3. **Parallel Session Workflows (`/fork` improvements)** — **#4578, #4580** request that `/fork` open a new terminal, plus a `copilot --fork` startup flag to work with two sessions side-by-side without manual terminal management.

4. **PDF Upload Support** — **#4583**: Users want to feed PDF documents directly into CLI sessions for analysis, since underlying models already support PDF input.

5. **Image Generation for Assets** — **#4581**: Requests image generation for non-code assets (icons, favicons, OG images). A natural extension as the CLI becomes a full app-builder tool.

6. **Status Line and Footer Customization** — **#4591, #4589**: Truncation controls for long paths/branches and raw token counts in the status line — small quality-of-life customizations for power users.

---

## Developer Pain Points

1. **OAuth / MCP Authentication Fragility** — The single biggest recurring theme today: **#4490, #4582, #4584, #4408**, and **#4421** all involve broken OAuth flows or MCP handshake failures across Entra ID, Atlassian, and enterprise GitHub Copilot environments. Each release seems to regress a different auth path.

2. **Context Compaction Data Loss** — **#4572** and **#4224** highlight reliability gaps around context management: lost tool results after compaction and missing billing telemetry for subagents. Teams running long unattended sessions are hit hardest.

3. **Windows File-Locking Issues** — **#4570** (plugins blocked by VS Code) and **#4593** (worktree archiving fails with `os error 32` when the process tree is still running) show recurring Windows-specific file-lock handling problems.

4. **Unpredictable CLI Behavior in Cloud Mode** — **#4568** describes hangs, crash-on-reconnect, and 429 rate limiting in `--cloud` workflows — an unstable experience for teams relying on cloud sessions.

5. **High 400/403 Error Rates** — **#1274** (persistent 400s on code reviews) and **#4414** (BYOK providers block before requests reach the provider) suggest ongoing request-validation bugs that degrade core daily workflows.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest – 2026-08-25**

**1. Today's Highlights**

The 24-hour window shows two significant community touchpoints: a long-running issue (#1994) over `kimiCode` usage billing has escalated with 8 comments and 7 upvotes, indicating growing dissatisfaction with token-based consumption for deep-reasoning tasks. Concurrently, a new PR (#2595) directly addresses a critical file-corruption bug in `StrReplaceFile` related to non-UTF-8 handling—a fix that prevents silent data loss during edits. No new releases were published in the last day; attention remains focused on backend quota policies and reliability fixes.

**2. Releases**

None. No new versions were published in the last 24 hours.

**3. Hot Issues**

1. **[#1994 – kimiCode用量计算有问题 (Usage Calculation Bug)](https://github.com/MoonshotAI/kimi-cli/issues/1994)**  
   *Why it matters:* Users report that two tasks exhaust a 2-hour quota, contradicting official claims that quotas are based on API request counts (~300–1200 requests per 5h) rather than tokens. The community suspects token-based billing, and K2.6's long chain-of-thought is burning through limits prematurely.  
   *Reaction:* 8 comments, 7 👍. Strong frustration; users question the "pay-as-you-go" transparency and consider it a deal-breaker for heavy interactive use.

2. **Related usage-threshold requests** (e.g., `--limit` flags, time-based quotas vs. token-based) continue to dominate new issue templates—no new filed today, but #1994 is the standing proxy for this pain point.

*Note: No additional new or materially updated issues were found in the last 24h. This is a low-activity day; the list above is intentionally concise to reflect actual data.*

**4. Key PR Progress**

1. **[#2595 – fix(StrReplaceFile): refuse to edit files that are not valid UTF-8](https://github.com/MoonshotAI/kimi-cli/pull/2595)**  
   *Author:* shoemoney · *Updated:* 2026-08-24  
   *Feature/Fix:* Prevents data corruption in `StrReplaceFile` by rejecting files with invalid UTF-8 bytes instead of silently replacing them with U+FFFD. This resolves issue #2591, protecting binary or mixed-encoding files from accidental loss during edits.  
   *Significance:* High—directly mitigates a data-integrity risk in the core file-editing tool.

*Note: Only one PR was updated in the last 24h. The digest reflects actual data; no other PRs reached the 10-item threshold.*

**5. Feature Request Trends**

Across recent issues (derived from historical patterns and the current #1994 context), the top requested directions are:

- **Transparent token vs. request billing:** Users want a clear dashboard or CLI flag to see both token and request consumption in real-time.
- **Configurable reasoning effort:** Ability to dial down K2.6's chain-of-thought length to conserve quota for simpler tasks.
- **Auto-retry with cost estimation:** A pre-flight estimate of token cost before starting a task, with an opt-in confirmation prompt.

**6. Developer Pain Points**

- **Quota exhaustion with deep reasoning:** The #1 recurring frustration—long CoT in K2.6 makes token-based quotas feel "like a meter that runs while thinking," undermining the official request-based pricing promise.
- **Data integrity concerns:** Files with non-UTF-8 content (e.g., Latin-1 configs, binary assets) are at risk of silent corruption during edits—the community is actively watching for a fix.
- **Documentation mismatch:** The gap between marketing claims ("300–1200 requests per 5h") and observed behavior (2 tasks per 2h) erodes trust; users demand a public, machine-readable pricing spec.

---  
*Data source: [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-25

## Today's Highlights
OpenCode v1.18.22 shipped with critical stability fixes, including removing outdated Go pricing messaging, fixing device-login URL handling for relative paths, and stopping `textVerbosity` from being sent to incompatible providers. Meanwhile, the community is buzzing around a cluster of `network_error` and "Upstream request failed" reports affecting the Ox Alpha Free tier and Kimi K3 models, alongside progress on a long-awaited fix for LSP diagnostics bloating session metadata.

---

## Releases
**v1.18.22** — Bugfix release focused on core stability:
- Removed outdated OpenCode Go first-month discount messaging and pricing.
- Fixed OpenCode device login links when servers return relative verification URLs or use a base path.
- Fixed `textVerbosity` being sent to OpenAI-compatible providers that do not support it.

[View Release](https://github.com/anomalyco/opencode/releases)

---

## Hot Issues

1. **[#30877 — TUI Sidebar "Modified Files" Section Missing (v1.16.0+)**](https://github.com/anomalyco/opencode/issues/30877) *(OPEN, 11 comments)*  
   A regression that completely hides uncommitted files in the TUI sidebar after a path-truncation fix. Still unresolved after 2+ months, with 14 upvotes — a major workflow blocker for git-centric users.

2. **[#4489 — Ephemeral One-Off Sessions for `opencode run`](https://github.com/anomalyco/opencode/issues/4489)** *(CLOSED, 14 comments)*  
   Proposal to run non-persisted sessions via `opencode run`. Contributor offered to implement but was closed without action — the 15 upvotes show real demand for lightweight, throwaway runs.

3. **[#43619 — `subagent` Tool Cannot Spawn First Child Session (2.0)](https://github.com/anomalyco/opencode/issues/43619)** *(CLOSED, 10 comments)*  
   Docs say `sessionID` should be omitted for new sessions, but the schema requires it — blocking all initial child-agent spawns in delegation workflows. Unfortunate closure for such a critical path blocker in 2.0.

4. **[#6310 — Large LSP Diagnostics Kill Sessions (Lua & others)](https://github.com/anomalyco/opencode/issues/6310)** *(CLOSED, 9 comments)*  
   Edit/write tools persist full workspace diagnostics into metadata, causing degradation on large Lua projects. PR #44811 addresses this by trimming persisted diagnostics — good to see a fix finally landing.

5. **[#37823 — GitHub Action Fails on New Repos (OIDC `sub` Format)](https://github.com/anomalyco/opencode/issues/37823)** *(CLOSED, 6 comments)*  
   Repos created after 2026-07-15 break the GitHub Action with `p.rest` undefined, due to GitHub's new immutable OIDC subject format. 11 upvotes indicate broad impact on CI adoption.

6. **[#44328 / #44379 / #44689 — `provider finish_reason: network_error`](https://github.com/anomalyco/opencode/issues/44328)** *(Multiple, ~16 total comments)*  
   A cluster of reports across Ox Alpha Free and other providers where sessions randomly fail with `network_error`. Only workaround is a new chat session. Likely a provider-side issue but is creating trust concerns.

7. **[#37815 — Kimi K3 on Console Go Fails with "Upstream request failed"](https://github.com/anomalyco/opencode/issues/37815)** *(OPEN, 7 comments)*  
   Model is listed but always fails; others on same provider work fine. 6 upvotes suggest it's not an isolated config problem.

8. **[#44788 — V2 Plugin API Delivers No Events (beta 18050)](https://github.com/anomalyco/opencode/issues/44788)** *(OPEN, 2 comments)*  
   Critical 2.0 blocker: `event.subscribe` registers but delivers zero events; `session.hook("context")` never reaches the model prompt. Undermines the entire plugin context-injection story.

9. **[#44798 — Context Limit Hits Mid-Task with No Continuation Handoff (2.0)](https://github.com/anomalyco/opencode/issues/44798)** *(CLOSED, 2 comments)*  
   Agent refuses multi-step work when context is nearly full, even with prepared task docs. No compaction or handoff — a UX gap for long-running sessions.

10. **[#11983 — Shift+Enter Keybind Ignored](https://github.com/anomalyco/opencode/issues/11983)** *(CLOSED, 8 comments)*  
    Users cannot configure Enter/Shift+Enter for submit/newline — common in AI chat UIs. Closed as resolved, but this surfaced again in multiple combos, so regression risk is worth watching.

---

## Key PR Progress

1. **[#44822 — Resolve Plugin SDK Imports at Runtime](https://github.com/anomalyco/opencode/pull/44822)** *(Merged)*  
   Exposes `@opencode-ai/plugin/tui` via OpenTUI runtime so discovered CLI plugins use the running TUI SDK — fixes a subtle version-mismatch class of bugs.

2. **[#44811 — Trim Persisted LSP Diagnostics in Edit/Write Metadata](https://github.com/anomalyco/opencode/pull/44811)** *(Open)*  
   Directly addresses #6310: stops persisting whole-workspace LSP diagnostic maps into session metadata, which was causing severe slowdowns. High-impact for large monorepos and Lua/TS workspaces.

3. **[#44792 — Add Partial JSON Parser](https://github.com/anomalyco/opencode/pull/44792)** *(Merged)*  
   Internal partial JSON parser with configurable partial strings/numbers/collections and Effect Schema decoding. Lays groundwork for robust streaming and repair strategies.

4. **[#44818 — Normalize Tool Input Errors](https://github.com/anomalyco/opencode/pull/44818)** *(Open)*  
   Unifies Effect, Standard Schema, and JSON Schema validation failures into one error format with field paths and retry guidance — improves debuggability for tool authors.

5. **[#44817 — Ignore Unknown Anthropic Stream Variants](https://github.com/anomalyco/opencode/pull/44817)** *(Open)*  
   Defers content block decoding until after discriminator dispatch, ignoring unknown variants while strictly validating recognized ones. Improves forward-compatibility with Anthropic API changes.

6. **[#44743 — Enforce Chat Finish Reasons](https://github.com/anomalyco/opencode/pull/44743)** *(Open)*  
   Requires non-empty finish reasons by default, with opt-out for compatible endpoints. Likely reduces silent failures from providers that drop `finish_reason`.

7. **[#44794 — Recover Missing Reasoning Item IDs](https://github.com/anomalyco/opencode/pull/44794)** *(Open)*  
   Assigns synthetic IDs when Responses API reasoning items omit required fields, and reuses the synthetic ID across stream parts. Fixes a class of mid-stream crashes.

8. **[#44803 — MCP Scoped Config, Project Approval, Keychain Storage](https://github.com/anomalyco/opencode/pull/44803)** *(Open)*  
   Upgrades MCP server management: project-scoped configs, per-project approval prompts, and OS keychain credential storage — brings parity with Claude Code and Gemini CLI.

9. **[#44810 — Resume Queued Prompts After Interrupt](https://github.com/anomalyco/opencode/pull/44810)** *(Open)*  
   Fixes a race where user messages submitted while the agent is busy get persisted but the caller doesn't rejoin the in-flight run — closes a frustrating dropped-prompt edge case.

10. **[#44242 — Model Capability Tiers for Small/Local Models](https://github.com/anomalyco/opencode/pull/44242)** *(Open)*  
    Introduces a minimal system prompt for small/local models (e.g., Qwen 4B) so they don't constantly trigger compaction. Important for the growing local-model user base.

---

## Feature Request Trends

- **Ephemeral / One-Off Sessions** — Strong demand for `opencode run` without persistence or session-store writes (#4489). Users want single-shot automation without session bloat.
- **Session Continuity & Recovery** — Auto-resume interrupted sessions on startup (#44819), and automatic context compaction with handoff when hitting limits (#44798) are both actively requested.
- **Better Small Model Support** — Explicit capability tiers so small models with limited context windows aren't forced into aggressive compaction cycles (#41372 → #44242).
- **Project-Scoped MCP & Credential Management** — Users clearly want per-project MCP approval, scoped configs, and secure keychain storage (#44803).
- **ARM32 / Edge-Device Support** — A new request for aarch32/arm32 targets, though low engagement (#44783).

---

## Developer Pain Points

1. **Provider `network_error` and "Endpoint unavailable" Failures** — Recurring across Ox Alpha Free, Kimi K3, and others. Sessions become unusable mid-task; workaround is manual restart. Erodes trust in the Go tier.

2. **Session Bloat from LSP Metadata** — Persisting full-workspace diagnostics into tool metadata makes large projects grind to a halt. The community is relieved to see a fix in review, but it's been an open sore since December 2025.

3. **2.0 Plugin API Unreliability** — Zero event delivery and context hooks silently failing (beta 18050) is a significant regression for the plugin ecosystem, breaking all programmatic context injection.

4. **GitHub Action OIDC Breakage** — New repos failing with cryptic `p.rest` errors due to GitHub's OIDC format change caused widespread CI failures. The closure was quiet but the 11 upvotes signal lasting frustration.

5. **Variant `limit` Field Ignored** — Users configuring fallback model limits via `variant` report the field is silently ignored (#44448) — undermines cost-control workflows.

6. **Keyboard Customization Gaps** — Shift+Enter vs Enter submit/newline keybindings continue to surface as a persistent UX annoyance across a CLI-first tool.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-25

## Today's Highlights
Pi v0.84.3 lands with two notable additions: an optional native PowerShell tool for Windows and safer managed updates with staged verification. Community attention is sharply focused on Windows onboarding quality — a long-running issue thread (#7547 with 44 comments) is collecting user pain points to guide platform investment. A trio of DeepSeek catalog gaps (vision model missing, stale pricing, new release not selectable) also surfaced, alongside several TUI/UX polish requests from active contributors.

## Releases
**v0.84.3** — Two new features:
- **PowerShell tool**: Optional native PowerShell command execution on Windows (see [docs](https://github.com/earendil-works/pi/blob/v0.84.3/packages/coding-agent/docs/windows.md#powershell-tool)).
- **Safer managed updates**: Staged, verified, and atomically activated updates.

## Hot Issues
1. **[#7547](https://github.com/earendil-works/pi/issues/7547) — Windows usage and pain points (OPEN, 44 comments)** — Active community call for Windows developer feedback on how Pi is run and where it breaks. High signal for platform investment decisions: docs, out-of-box experience, and bug prioritization.

2. **[#6879](https://github.com/earendil-works/pi/issues/6879) — Auto-compaction never triggers until provider overflow (OPEN, 22 comments, 👍19)** — Critical reliability issue: context grows past 100% with no compaction until the API rejects the request (observed at 373k tokens). Community wants compaction checks after every agentic turn, not just provider-driven.

3. **[#6922](https://github.com/earendil-works/pi/issues/6922) — Default llama.cpp model shows "No models available" (CLOSED, 11 comments, 👍14)** — Startup failure when `defaultProvider: "llama.cpp"` and a preset model are configured. Fixed via [#8479](https://github.com/earendil-works/pi/pull/8479) exposing unloaded presets.

4. **[#8167](https://github.com/earendil-works/pi/issues/8167) — Cannot pick built-in llama.cpp models (CLOSED, 11 comments)** — llama-server router-mode models missing from model list despite `/llama` load/unload working. Community supplied configs for reproduction; fix shipped in [#8558](https://github.com/earendil-works/pi/pull/8558).

5. **[#7444](https://github.com/earendil-works/pi/issues/7444) — WebSocket retry only handles two error codes (CLOSED, 9 comments)** — Transient `response.failed` errors hard-stop turns; retry logic too narrow in `openai-codex-responses.js`. Related PR [#8138](https://github.com/earendil-works/pi/pull/8138) proposes retry classification for "Sorry, something went wrong".

6. **[#8166](https://github.com/earendil-works/pi/issues/8166) — Custom message mid-tool-batch breaks tool_calls adjacency (OPEN, 7 comments)** — Extension-injected messages with `triggerTurn: false` break DeepSeek's required tool_calls→tool adjacency, causing permanent 400 errors on every subsequent turn.

7. **[#8441](https://github.com/earendil-works/pi/issues/8441) — Windows "Path outside repository" for explicit paths (CLOSED, 3 comments)** — Path separator mismatch in containment check breaks all tools with explicit path arguments on Windows. Direct consequence of Windows support gaps in #7547.

8. **[#8586](https://github.com/earendil-works/pi/issues/8586) — OpenAI streams ignore abort signal mid-turn (CLOSED, 1 comment)** — OpenAI Responses/Completions loops never check `signal.aborted`; RPC aborts hang until stream completes. Fixed in [#8585](https://github.com/earendil-works/pi/pull/8585).

9. **[#8584](https://github.com/earendil-works/pi/issues/8584) — TUI row corruption after long tool output (CLOSED, 1 comment)** — Assistant text renders one word per line after tool calls printing wide lines. Likely a wrapping bug in TUI rendering post-tool-output.

10. **[#8409](https://github.com/earendil-works/pi/issues/8409) — Aborted turns report stopReason "error" instead of "aborted" (CLOSED, 4 comments)** — Regression in v0.84.2: aborts during tool calls produce misleading error reports, complicating session analysis and retry logic.

## Key PR Progress
1. **[#8512](https://github.com/earendil-works/pi/pull/8512) — Add optional PowerShell tool (CLOSED)** — Author gave up on git bash path handling for Windows; ships native PowerShell execution with proper path semantics. Merged in v0.84.3.

2. **[#8585](https://github.com/earendil-works/pi/pull/8585) — Abort OpenAI streams immediately on signal (CLOSED)** — Adds abort checks in OpenAI Responses/Completions loops matching the Anthropic path's `reader.read()` pattern.

3. **[#8580](https://github.com/earendil-works/pi/pull/8580) — Drop extra vertical padding on tool rows (CLOSED)** — Removes 2–3 empty lines per tool call; tighter transcript density.

4. **[#8572](https://github.com/earendil-works/pi/pull/8572) / [#8573](https://github.com/earendil-works/pi/pull/8573) — Amazon Bedrock Mantle support (OPEN, WIP)** — Adds Mantle routing for new GPT-5.x models not available via Converse. Waiting on API key permissions for e2e testing.

5. **[#8479](https://github.com/earendil-works/pi/pull/8479) — Expose unloaded llama.cpp presets (CLOSED)** — Fixes #8167: presets from `--models-preset` now appear in model selection, loaded on request. Also improves llama-swap compatibility.

6. **[#8575](https://github.com/earendil-works/pi/pull/8575) — Surface torn-append replay loss in session JSONL (CLOSED)** — Malformed JSONL lines silently cost two replay entries; now bounded and reported.

7. **[#8558](https://github.com/earendil-works/pi/pull/8558) — Show llama presets if autoload enabled (CLOSED)** — Companion fix to #8479; `/model` now shows preset entries when the router can auto-load them.

8. **[#8559](https://github.com/earendil-works/pi/pull/8559) — Attach clipboard images as atomic markers (OPEN)** — Pasted images become visible attachment markers instead of raw temp-file paths; improves prompt transparency.

9. **[#8547](https://github.com/earendil-works/pi/pull/8547) — Move editor cursor on click (OPEN)** — Mouse click inside the prompt moves the cursor; removes need for keyboard navigation in mouse-enabled terminals.

10. **[#8552](https://github.com/earendil-works/pi/pull/8552) — Keep skills available with bash-only tools (OPEN)** — Fixes regression where skills disappear when non-bash tools are unavailable; closes #8551.

## Feature Request Trends
- **Windows parity and quality**: Highest-frequency theme — PowerShell tooling, path separator fixes, interactive-mode shell selection (PowerShell 5.1 vs pwsh), and an ongoing community call for prioritized Windows fixes.
- **Provider expansion**: Three requests for new providers (Merge Gateway, Eden AI, Parasail.io) plus Bedrock Mantle support — all OpenAI-compatible gateways or new API surfaces for frontier open models.
- **Model catalog freshness**: DeepSeek vision model missing, stale peak/off-peak pricing, and inability to select newly released models — catalog maintenance must keep pace with model releases.
- **Extension and UX ergonomics**: Renderer hooks for extension-provided compactions, portable agent presets (`pi preset`), deferred heavy tool schemas, and opt-in selection policies for fullscreen overlays.
- **Session/workflow enhancements**: Moving sessions into git worktrees non-interactively, better external editor command parsing (quoted paths), and clearer visual feedback on shared session pages.

## Developer Pain Points
- **Context compaction reliability** (#6879): Auto-compaction not triggering until provider overflow remains the top-voted issue (👍19), causing multi-hour sessions to fail at API limits.
- **Windows onboarding friction** (#7547, #8441, #8582, #8512): Path separator mismatches, PowerShell 5.1 vs pwsh inconsistency, and general "too many ways to run Pi" confusion — a direct community call for investment.
- **Abort handling inconsistencies** (#8409, #8586): Mixed `stopReason` values and streams ignoring abort signals complicate automation and error reporting.
- **Llama.cpp integration gaps** (#6922, #8167): Model discovery and selection issues persist despite fixes; presets not shown until autoload enabled was a two-part fix.
- **Stream/WebSocket resilience** (#7444, #8138): Narrow retry classification causes transient backend errors to surface as terminal failures, hard-stopping turns.
- **Tool-call integrity** (#8166): Extension-injected messages can permanently corrupt tool_calls→tool adjacency, breaking every subsequent turn with 400 errors.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-25

## Today's Highlights

The project continues active nightly releases with WebShell session-workspace fixes and a new CUA driver release (v0.20.0). The community is pushing on several fronts: MCP reconnect reliability, TUI rendering architecture (ink → OpenTUI migration), and the ongoing CLI/core architecture overhaul tracked in a 12-item structural review. Several auto-fix/self-reported review improvements landed, including content-anchored incremental review rounds and launch of a computer-use via Node REPL roadmap.

---

## Releases

**v0.22.0-nightly.20260824.3a1f86d805** — focused on a WebShell fix: pass session workspace cwd when opening from overview panel ([PR #9730](https://github.com/QwenLM/qwen-code/pull/9730)).

**cua-driver-rs v0.20.0** — Qwen CUA Driver prebuilt binaries:
- macOS: codesigned + notarized universal binary + `QwenCuaDriver.app`
- Linux: x86_64 + arm64 (glibc 2.31 floor)
- Windows: x86_64 + arm64
- Vendored under `packages/cua-driver`; published via gh-attach workflow

---

## Hot Issues

1. **[#5975 — API Error: No stream activity after 19 chunks](https://github.com/QwenLM/qwen-code/issues/5975)** (12 comments)  
   Recurring stream timeout after upgrade to v0.19.3, especially after "Thought for 2s" with no output. High community engagement; P2, needs triage.

2. **[#4063 — Core + CLI architecture review: 12 structural issues](https://github.com/QwenLM/qwen-code/issues/4063)** (9 comments, in-progress)  
   Critical finding: `ContentGenerator` interface is coupled to `@google/genai` types — 136 files import it directly. P0-level architectural debt.

3. **[#8083 — Make derived Config context ownership explicit](https://github.com/QwenLM/qwen-code/issues/8083)** (6 comments, in-progress)  
   Proposal to replace ad hoc `Object.create(base)` prototype delegation for subagents, scoped memory agents, and approval-mode overrides.

4. **[#9944 — MCP reconnect reports success but tools unavailable (HTTP transport)](https://github.com/QwenLM/qwen-code/issues/9944)** (4 comments)  
   After restarting an HTTP MCP server (new session-id), `qwen mcp reconnect --all` claims success but tools return "Tool not found". P2 bug, fresh.

5. **[#9005 — Anthropic wire missing stream-safety protections](https://github.com/QwenLM/qwen-code/issues/9005)** (4 comments, P1)  
   `anthropicContentGenerator` lacks stream-safety guards that OpenAI wire already has; companion issue notes `@anthropic-ai/sdk` pinned to ^0.36.1 (Jan 2025).

6. **[#9026 — NO_TOOL_RESULT_PROGRESS hard-fails headless runs](https://github.com/QwenLM/qwen-code/issues/9026)** (4 comments, closed)  
   Headless runs abort when a model ends a turn quietly after a tool result — `InvalidStreamError` in gemini content generator.

7. **[#8662 — Migrate TUI rendering from ink to OpenTUI](https://github.com/QwenLM/qwen-code/issues/8662)** (4 comments)  
   ink 7 + React 19 has structural problems: flicker, ~1037-line patch, custom VP mode. OpenTUI offers flicker-free, first-class mouse support.

8. **[#9927 — Artifact updatedAt stays stale; write_file intermediates linger](https://github.com/QwenLM/qwen-code/issues/9927)** (4 comments)  
   `updatedAt` only moves on registration field changes, not content updates. Intermediates from write_file remain as "missing" in artifacts.

9. **[#9853 — Kimi rejects built-in tool schemas with uniqueItems](https://github.com/QwenLM/qwen-code/issues/9853)** (2 comments, closed, P1)  
   DashScope OpenAI-compatible endpoint HTTP 400s on `uniqueItems: true` in `update_goal.evidenceRefs` and `todo_write.blockedBy` schemas for kimi-k3.

10. **[#9934 — MCP tool results always rendered in full](https://github.com/QwenLM/qwen-code/issues/9934)** (2 comments)  
    Unlike read/search tools, MCP tool results are never collapsed in the transcript — noisy for large outputs. P2 UI enhancement.

---

## Key PR Progress

1. **[#9492 — Loop detection result-aware for task_list polls](https://github.com/QwenLM/qwen-code/pull/9492)** (open)  
   Prevents false loop-detection positives for stateful read tools where identical args ≠ identical results (shared task board).

2. **[#8943 — Step 3A fan-out dispatched from generated workflow script](https://github.com/QwenLM/qwen-code/pull/8943)** (open, autofix/takeover)  
   `/review` Step 3A can be code-dispatched via `qwen review emit-workflow`, with legacy path untouched.

3. **[#9741 — Screen content filters before probe tree restore](https://github.com/QwenLM/qwen-code/pull/9741)** (open, autofix/takeover)  
   Prevents `scratch-tree` from creating/resetting trees when local config defines content filters that could rewrite via smudge.

4. **[#9900 — Rename Gemini residue in memory/spinner/leaf ids](https://github.com/QwenLM/qwen-code/pull/9900)** (open)  
   PR 1 of #4063 item 6 naming cleanup — removes `Gemini` fork prefix from identifiers that aren't Gemini-API concepts.

5. **[#9916 — Retry sandbox image builds, file issue on failure](https://github.com/QwenLM/qwen-code/pull/9916)** (open, review/self-reported)  
   Self-healing image publish: one bounded retry for transient buildx failures, then files/updates a GitHub issue per version.

6. **[#9394 — DingTalk Workspace channel](https://github.com/QwenLM/qwen-code/pull/9394)** (open, autofix/takeover, needs-human)  
   Built-in channel using authenticated DWS CLI profile: DMs, @mentions, ambient groups, doc-mention notifications, native todo changes.

7. **[#8927 — Bound session lifetime with sessionRotation](https://github.com/QwenLM/qwen-code/pull/8927)** (open, autofix/needs-human)  
   Per-channel `sessionRotation` bounds session reuse with `maxTurns` and time-based limits; fresh session after bound.

8. **[#9305 — Bottom-align short VP content](https://github.com/QwenLM/qwen-code/pull/9305)** (open, autofix/needs-human)  
   Fixes blank gap between last message and composer in VP mode when conversation fits viewport (from #9300).

9.  **[#9740 — Step 4 verification execution-grade](https://github.com/QwenLM/qwen-code/pull/9740)** (open)  
    Adds `qwen review ab-drive` — runs one script against two trees (PR worktree + base-tree), paired captures.

10. **[#9441 — Show edit/exec diffs when PreToolUse hook returns ask](https://github.com/QwenLM/qwen-code/pull/9441)** (open)  
    Hook `ask` decisions now carry diffs to the interactive approval prompt instead of a synthetic plain-text reason.

---

## Feature Request Trends

- **Computer-use via persistent Node REPL** ([#9333](https://github.com/QwenLM/qwen-code/issues/9333), [#9334](https://github.com/QwenLM/qwen-code/issues/9334), [#9335](https://github.com/QwenLM/qwen-code/issues/9335), [#9336](https://github.com/QwenLM/qwen-code/issues/9336)) — Three-phase roadmap: session-level REPL → cua-driver SDK wrapper → Skill integration with model-in-loop benchmarks.
- **External-context provider breadth** ([#9951](https://github.com/QwenLM/qwen-code/issues/9951), [#9964](https://github.com/QwenLM/qwen-code/issues/9964)) — Support open-source Mem0 protocol with configurable `baseUrl`, plus interactive fake-Mem0 harness variants.
- **TUI/UX modernization** ([#8662](https://github.com/QwenLM/qwen-code/issues/8662), [#9942](https://github.com/QwenLM/qwen-code/issues/9942), [#9934](https://github.com/QwenLM/qwen-code/issues/9934)) — OpenTUI migration, hide skill commands from slash completion, collapse MCP tool results.
- **Session/workspace lifecycle** ([#8927](https://github.com/QwenLM/qwen-code/pull/8927), [#9895](https://github.com/QwenLM/qwen-code/pull/9895), [#9911](https://github.com/QwenLM/qwen-code/issues/9911)) — Session rotation bounds, scoped workspace memory tasks, restore VS Code message edit/rewind.
- **Review pipeline hardening** ([#8943](https://github.com/QwenLM/qwen-code/pull/8943), [#9740](https://github.com/QwenLM/qwen-code/pull/9740), [#9932](https://github.com/QwenLM/qwen-code/pull/9932)) — Workflow-scripted fan-out, execution-grade verification, forward-grafting anchors across fail-closed rounds.

---

## Developer Pain Points

1. **Stream reliability** — Timeouts after 120s with partial chunks (#5975), headless aborts on quiet turn ends (#9026), Anthropic wire missing stream-safety protections (#9005).
2. **MCP reconnect semantics** — Reconnect reports success but tools remain unavailable, session-id mismatch (HTTP transport) (#9944).
3. **Ink-based TUI limitations** — Flicker, one-row-over-height-budget triggers full repaints (#9966), 1037-line patch burden (#8662).
4. **Config/schema drift** — Settings schema rejects values the runtime honors (`output.format: "stream-json"`, #8965); derived Config ownership unclear (#8083).
5. **Cross-session leakage** — ACP debug logs cross session boundaries in multiplexed processes (#9534); Bots' per-session fallback config clobbering.
6. **Memory/artifact inconsistencies** — Recall beyond 200-doc cap but forget path capped (#9378); artifact `updatedAt` stale on content changes (#9927).
7. **Team/multi-agent coordination** — Shutdown requests overload teammate message channel, rejecting ordinary reports (#9510); task board loop-detection false positives (#9492).
8. **CI/image pipeline fragility** — Sandbox lanes die on missing images (#9961); issue tracker never closed on recoverable image-build failures (#9960); root ignores permission bits in run-ledger tests (#9909).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-25

---

## 1. Today's Highlights

The v0.9.12 release cycle is in full swing with the integration branch now "gated and code-complete" for release blockers (#5576), featuring a unified managed Chat with native runtime threads and an R2 approval fix (#5606). A significant provider-neutrality audit (#5588) identified 18 DeepSeek-exclusive gates that need to become provider-neutral, with the first NVIDIA NIM env leak fix already landed. Community contributors shipped several UX improvements including cursor accent theming (#5599), Fleet roster editing discoverability (#5604), and tool/MCP schema cost visibility in the context inspector (#5603).

---

## 2. Releases

No new releases in the last 24 hours. The project is currently in the v0.9.12 release preparation phase with the integration branch tracking release-blocker issues (see #5573 milestone tracker). The v0.9.12 release is expected to include the managed Chat runtime unification, approval receipt persistence, and goal-continuation cadence fixes.

---

## 3. Hot Issues

### #5588 — Provider neutrality: 18 DeepSeek-exclusive gates
**Status:** OPEN | **Comments:** 4 | **Author:** Hmbown  
A full audit of 2,281 production lines found 18 behavior gates hardcoded for DeepSeek that should be provider-agnostic. The first fix (NVIDIA NIM env leak) is already merged. This is a foundational architectural issue affecting all non-DeepSeek providers.
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5588)

### #5573 — v0.9.12 milestone tracker
**Status:** OPEN | **Comments:** 3 | **Author:** Hmbown  
The central coordination issue for the 0.9.12 cycle — tracks P0 "money & safety" must-fixes before release. The community should watch this issue to understand what is blocking the next release.
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5573)

### #5601 — Fresh install 404 errors for MiniMax and Xiaomi models
**Status:** OPEN | **Comments:** 2 | **Author:** Brook-WZ  
First-time configuration of MiniMax and Xiaomi models returns 404 errors, likely due to incorrect hardcoded URLs. The author notes DeepSeek works fine, suggesting model-specific configuration bugs that affect new users onboarding with non-DeepSeek providers.
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5601)

### #5596 — Turn end silently cancels turn-owned subagents
**Status:** CLOSED | **Comments:** 1 | **Author:** Hmbown  
A data-loss bug: long-running reviewer subagents are destroyed when the parent model ends its turn, despite UI messaging suggesting they continue in the background. The impact of a 347k-token reviewer losing all work without warning (see #5595) makes this a serious reliability issue.
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5596)

### #5586 — Mega-file decomposition required
**Status:** OPEN | **Comments:** 3 | **Author:** Hmbown  
The codebase has grown unwieldy: `lib.rs` at 18.7k lines, `config.rs` at 12.3k, `client.rs` at 11.1k. This is a maintainability problem that affects contributors' ability to navigate and review code, and is a prerequisite for other refactors.
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5586)

### #5547 — CI: Linux workspace tests don't run for non-mirrored branches
**Status:** CLOSED | **Comments:** 4 | **Author:** Hmbown  
CI reliability gap: the Rust test/clippy lanes skip on ubuntu for PRs with branch prefixes not in the CNB mirror whitelist, meaning some integration branches get zero Linux test coverage. This undermines PR validation confidence.
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5547)

### #5585 — Test dies by stack overflow
**Status:** OPEN | **Comments:** 3 | **Author:** Hmbown  
`setup_confirm_toast_names_secret_store_and_global_scope` SIGABRTs with stack overflow on both main and the integration branch. Pre-existing and bisected, it blocks test suite green status.
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5585)

### #5595 — Read-only inspection children reject git -C at execute time
**Status:** OPEN | **Comments:** 1 | **Author:** Hmbown  
A reviewer child with read-only posture burned ~347k tokens producing no findings because `git -C <workspace> log` was blocked at execution time despite being allowed by the model-facing classifier. This is a posture-gate consistency bug with costly real-world impact.
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5595)

### #5583 — Workflow responseSchema failures need bounded repair
**Status:** OPEN | **Comments:** 3 | **Author:** jbovard2016  
When workflow tasks using `responseSchema` return prose or malformed JSON, the system fails the run without attempting a bounded repair or preserving the malformed output for inspection. This is a workflow robustness gap.
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5583)

### #5589 — Fleet config view UX problems
**Status:** OPEN | **Comments:** 2 | **Author:** Hmbown  
Enter loops back to the same screen with no visible state change, and model switching is buried. The community responded with two PRs (#5604) addressing discoverability. A classic TUI navigation/usability issue.
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5589)

---

## 4. Key PR Progress

### #5606 — 0.9.12 relay integration: unify managed Chat with native runtime threads
**Status:** CLOSED | **Author:** Hmbown  
The headline integration: managed Chat rides native runtime threads (turn_operation_idempotency), plus R2 approval fix (MCP tools reviewed as kinds) and doctor --fix with consent.
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5606)

### #5576 — 0.9.12 integration: must-fix + UX fixes (WIP)
**Status:** OPEN | **Author:** Hmbown  
72-commit integration branch, "code-complete for release blockers." Remaining work: version bump + changelog/RC gates per tracker #5573.
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5576)

### #5584 — fix(subagents): persist child approval receipts
**Status:** OPEN | **Author:** cyq1017  
Closes #5543: child approval prompts now produce durable Asked/terminal evidence instead of in-memory-only grants. Critical for auditability.
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5584)

### #5602 — fix(shell): decode Windows output reliably
**Status:** OPEN | **Author:** zhuowp  
Preserves UTF-8 and Windows ANSI-code-page characters split across reads; uses Windows ACP only after strict UTF-8 decoding fails. Community fix for Windows reliability.
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5602)

### #5599 — feat(tui): add capability-gated cursor accent
**Status:** CLOSED | **Author:** wuisabel-gif  
Implements #5554: subtle OSC 12 cursor accent on start, OSC 112 restore on exit — only on capable terminals, disabled in reduced-motion/plain mode.
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5599)

### #5598 — fix(ci): scope credit checks to PR commits
**Status:** CLOSED | **Author:** Hmbown  
Fixes a false-blocking bug where the credit gate compared creation-time base.sha to synthetic merge checkout, inadvertently rechecking unrelated merged commits.
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5598)

### #5591 — Fix: goal continuation cadence fix — part a
**Status:** CLOSED | **Author:** M-Maciej  
Fixes #5534: `continuation_delay_seconds` was only wired into one of two goal-continuation dispatch paths. The within-turn path now respects the quiet period.
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5591)

### #5594 — control socket — part d (final)
**Status:** OPEN | **Author:** M-Maciej  
Opt-in, Unix-only, newline-framed JSON-RPC socket per running session. Enables machine-readable supervision of live sessions — the final piece of the supervised-operation stack.
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5594)

### #5593 — /relaunch command — part c
**Status:** OPEN | **Author:** M-Maciej  
`/relaunch` lets a session switch to a freshly updated binary in one step, preserving terminal state and telemetry.
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5593)

### #5603 — feat(tui): show tool and MCP schema costs
**Status:** OPEN | **Author:** wuisabel-gif  
Implements #5553 (display-only slice): context inspector now shows bounded schema-cost estimates per built-in tool and MCP server, helping users trim expensive context.
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5603)

---

## 5. Feature Request Trends

1. **Provider neutrality** — Strong momentum toward making the tool genuinely multi-provider: 18 DeepSeek-gated behaviors flagged in #5588, MiniMax/Xiaomi 404s from hardcoded URLs (#5601), Anthropic-dialect caching fixes (#5570). The community clearly expects non-DeepSeek providers to be first-class citizens.

2. **Supervised/headless operation** — A complete stack is being built: lifecycle outbox (#5592), control socket (#5594), `/relaunch` (#5593), and goal-continuation cadence fixes (#5591). This points toward automated/CI-driven usage patterns.

3. **Context/cost transparency** — Multiple issues address visibility into token consumption: tool/MCP schema cost attribution (#5553), cache-control invariants (#5571), and prefix-continuity assertions. Users want to understand and control what they are paying for.

4. **Subagent lifecycle management** — Recurring problems with subagent reliability: silent destruction (#5596), posture-gate inconsistencies (#5595), approval receipt durability (#5584). As agent usage grows, deterministic subagent behavior is becoming critical.

5. **TUI discoverability & UX polish** — Cursor accent (#5554), fleet config navigation (#5589), focused-block actions (#5551), OSC 12/112 support. The interface is getting finer-grained usability attention.

---

## 6. Developer Pain Points

- **Non-DeepSeek provider setup is brittle** — 404 errors on first configuration for MiniMax/Xiaomi (#5601), DeepSeek-exclusive behavior gates (#5588), and inconsistent Anthropic-dialect caching (#5570) all contribute to a poor multi-provider experience.

- **Silent data loss in agent workflows** — Subagents killed at turn end without warning (#5596), read-only posture blocking legitimate commands (#5595), and missing raw-output receipts on schema failures (#5583) all destroy expensive work without clear signals.

- **Large, hard-to-navigate codebase** — Four files over 9k lines (#5586), 379 `allow(dead_code)` sites (#5587), and a test that stack-overflows (#5585) add friction for contributors and maintainers alike.

- **CI reliability gaps** — Linux workspace tests skipped for non-mirrored branch prefixes (#5547), flaky tests under parallel load (#5605), and credit-check false positives (#5598) erode trust in automated validation.

- **Memory/session continuity gaps** — Cross-session memory complaints persist (#2492), and cache-control continuity between turns isn't asserted (#5571), undermining provider caching efficiency.

- **Windows-specific roughe edges** — ANSI code-page decoding (#5602) and provider URL issues (#5601) show cross-platform testing needs more attention.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*