# AI CLI Tools Community Digest 2026-06-09

> Generated: 2026-06-09 01:52 UTC | Tools covered: 9

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

# AI CLI Developer Tools Ecosystem Report
**Cross-Tool Comparison | 2026-06-09**

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape continues to mature rapidly, with eight major projects showing distinct evolutionary trajectories. Claude Code and OpenAI Codex lead in feature velocity and community scale, while Gemini CLI and OpenCode demonstrate steady infrastructure investment with growing user bases. The ecosystem is fragmenting around protocol adoption—Agent Client Protocol (ACP) support becomes a key differentiator, with Qwen Code and CodeWhale making strategic bets. A common pain point across all tools is agent cost control and runaway token consumption, signaling that economic efficiency is now the community's primary concern over raw capability. The TypeScript CLI rewrite trend (Kimi Code, CodeWhale rebranding) indicates a structural shift from Python to TypeScript/Go/Rust for performance and cross-platform reliability.

---

## 2. Activity Comparison

| Tool | Open Issues | PRs (24h) | Latest Release | Release Velocity |
|------|------------|-----------|----------------|------------------|
| **Claude Code** | High (~600+) | 5 active | v2.1.169 (today) | Rapid (multiple/week) |
| **OpenAI Codex** | High (~500+) | 10 active | rust-v0.138.0 (today) | Rapid (weekly) |
| **Gemini CLI** | Moderate (~200+) | 8 active | v0.47.0-nightly (today) | Moderate (weekly) |
| **GitHub Copilot CLI** | Moderate (~300+) | 10 notable | None (24h) | Moderate (bi-weekly) |
| **OpenCode** | High (~500+) | 10 active | None (24h) | Rapid (weekly) |
| **Pi** | Moderate (~150+) | 10 active | v0.79.0 (today) | Rapid (weekly) |
| **Kimi Code** | Low (~50+) | 0 active | v0.11.0 (prior) | Slow (monthly+) |
| **Qwen Code** | Moderate (~100+) | 10 active | None (24h) | Moderate (bi-weekly) |
| **CodeWhale** | High (~200+) | 10 active | v0.8.54 (today) | Rapid (weekly) |

**Key observations:**
- Claude Code and OpenCode show highest issue volume, reflecting large user bases and rapid feature iteration
- Kimi Code has stalled—zero PR activity and critical regressions in v0.11.0 suggest migration pains
- Pi and CodeWhale show surprising burst activity (19 and 30 PRs closed in 24h respectively)
- All major tools released in last 7 days except Copilot CLI and OpenCode

---

## 3. Shared Feature Directions

### 3.1 Agent Cost Control & Token Efficiency
| Tool | Evidence |
|------|----------|
| **Claude Code** | #66353 (56-agent spawn for image upload), #65920 (272 agents, 10M+ tokens) |
| **Gemini CLI** | #26522 (Auto Memory infinite retry loops), #27698 (zero-quota retry hangs) |
| **OpenCode** | #31204 (session_message seq constraint failure wastes tokens) |
| **Kimi Code** | #2390 (hangs on large files, freezing without feedback) |
| **CodeWhale** | #743 (400M tokens in half-day), #1177 (cache hit rate sub-50%) |

**Requirement:** Users demand better heuristic guardrails, configurable agent spawning limits, and transparent token cost visibility across all tools.

### 3.2 Multi-Agent Orchestration & Workflows
| Tool | Evidence |
|------|----------|
| **Claude Code** | #4721 (Dynamic Workflows port from v2.1.160) |
| **Qwen Code** | #4161 (auto-improve command), #4721 (dynamic workflows) |
| **CodeWhale** | #2482 (WhaleFlow declarative multi-agent orchestration) |
| **OpenAI Codex** | #27107 (turn orchestration tracing), #26953 (goal API) |
| **Pi** | #5427 (Codex transport issues), #5509 (Bedrock Mantle provider) |

**Requirement:** Declarative multi-agent workflows with topological scheduling, semaphore concurrency, and file-scoped context are emerging as a major differentiation area.

### 3.3 Persistent Session & Memory Management
| Tool | Evidence |
|------|----------|
| **Claude Code** | #27725 (detachable windows), /cd command (shipped today) |
| **OpenCode** | #27167 (native /goal sessions), #31204 (session seq crashes) |
| **Copilot CLI** | #1928 (pause/resume), #2966 (concurrent session tooling) |
| **Gemini CLI** | #26522 (Auto Memory retry loops), #26525 (redaction before extraction) |
| **Kimi Code** | #2341 (persistent chat history) |
| **CodeWhale** | #2492 (no cross-session memory), #2904 (KV cache capsules) |

**Requirement:** Session mobility (local-to-cloud handoff), persistent goals, and reliable context preservation across restarts are universal needs.

### 3.4 MCP Protocol & Plugin Ecosystem
| Tool | Evidence |
|------|----------|
| **Claude Code** | #61044 (MCP approval deadlock), #66352 (cross-agent skill sharing) |
| **OpenCode** | #15535 (MCP Resources support), #31442 (MCP catalog pagination) |
| **Copilot CLI** | #3436 (custom MCP registry URL construction), #2540 (preToolUse hooks) |
| **Gemini CLI** | #27619 (atomic MCP tool discovery) |
| **Qwen Code** | #4773 (ACP WebSocket transport), #4782 (ACP Streamable HTTP) |

**Requirement:** Full MCP/ACP protocol parity (Resources + Tools + Prompts), reliable plugin hooks, and custom registry support are table stakes for enterprise adoption.

### 3.5 Internationalization & Encoding
| Tool | Evidence |
|------|----------|
| **Claude Code** | #66396 (Japanese text corruption on Windows) |
| **Gemini CLI** | #27505 (CJK continuation cell spacing) |
| **Kimi Code** | #2401 (Chinese characters garbled) |
| **CodeWhale** | #2919, #2918 (i18n localization PRs for 7 locales) |

**Requirement:** Non-ASCII text handling remains broken across multiple tools; CodeWhale's coordinated i18n push sets a positive example.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | CodeWhale |
|-----------|-------------|--------------|------------|-------------|----------|-----|-----------|-----------|
| **Primary Language** | TypeScript | Rust | TypeScript | TypeScript | TypeScript | Go | TypeScript | Rust |
| **Core Model** | Claude Opus 4.x | GPT-5.x | Gemini 2.x | Multiple (BYOK) | Multi-provider | Multi-provider | Qwen | DeepSeek + Multi |
| **Key Differentiator** | Plugin ecosystem, agent spawning | Desktop-to-CLI handoff | Google Cloud enterprise | GitHub integration, hooks | MCP-first, open | Local models (Ollama) | ACP protocol | Multi-agent workflows |
| **Target User** | Power devs, plugin creators | Enterprise, CI/CD | GCP enterprise | GitHub ecosystem | Open-source advocates | Local model users | Protocol innovators | Cost-conscious, global |
| **Release Style** | Aggressive (multiple/week) | Rapid (weekly) | Steady (weekly) | Conservative (bi-weekly) | Rapid (weekly) | Rapid (weekly) | Moderate (bi-weekly) | Rapid (weekly) |
| **Major Pain Point** | Agent cost explosion | Model availability confusion | Agent reliability | Extensibility broken | SQLite migrations | Local model latency | Memory leaks | Token overuse |

**Key differentiators emerging:**

1. **Protocol Strategy**: Qwen Code is making a bet on ACP as the universal transport, while Claude Code and OpenCode deepen MCP support. This could become a standards conflict.

2. **Model Architecture**: OpenAI Codex and Claude Code optimize for their proprietary models; Gemini CLI, OpenCode, Pi, and CodeWhale bet on multi-provider flexibility. The multi-provider model is winning community mindshare.

3. **Desktop vs. CLI**: OpenAI Codex pushes "seamless CLI-to-Desktop handoff" (rust-v0.138.0). Claude Code ships `/cd` for session mobility. Copilot CLI stays pure CLI. The hybrid approach appears to be the future.

4. **Enterprise Readiness**: Gemini CLI focuses on Vertex AI integration and telemetry. Copilot CLI targets GitHub workflows. Qwen Code targets protocol standards. Each serves a different enterprise entry point.

5. **Performance/Local Models**: Pi differentiates on local model support (Ollama, llama.cpp) but suffers multi-minute latencies. Everything else is cloud-first.

6. **Cost Transparency**: CodeWhale's token usage tracking (#4564) and Claude Code's agent spawning controls lead; Gemini CLI and Copilot CLI lag significantly on cost observability.

---

## 5. Community Momentum & Maturity

| Tier | Tools | Characteristics |
|------|-------|-----------------|
| **Established** | Claude Code, OpenAI Codex | 500+ open issues, daily new issues, multiple weekly releases, professional plugin marketplaces, large contributor bases |
| **Growing** | OpenCode, Gemini CLI | 200-500 issues, weekly releases, active PRs, building enterprise features, maturing APIs |
| **Emerging** | Pi, CodeWhale, Qwen Code | 100-200 issues, rapid iteration (19/30 PRs closed in 24h), strong foundational work, smaller but committed communities |
| **Constrained** | Copilot CLI, Kimi Code | <50 PRs/month, fewer releases, slow issue response, migration/transition pains |

**Maturity markers:**
- **Claude Code** shows the most mature plugin ecosystem (#65286, #65619) with marketplace integration and manifest validation
- **OpenAI Codex** has the strongest enterprise tracing infrastructure (#27107, #27091) with Guardian reviews and span-level telemetry
- **Qwen Code** demonstrates the deepest protocol thinking (ACP WebSocket, Streamable HTTP, daemon architecture)
- **Pi** has the most active bug-fixing velocity (19 PRs closed in 24h, patching quadratic CPU, missing assets, parallel compaction)
- **CodeWhale** shows the broadest localization effort (7 locales, coordinated PRs) and the most sophisticated orchestration (WhaleFlow)

**Warning signals:**
- **Kimi Code** has zero PR activity and critical regressions (#2442, #2441) in the latest release—users may migrate to alternatives
- **Copilot CLI** has broken extensibility (#2540, #2201) and multiple platform inconsistencies (#3652, #3662)—trust in plugin system eroding
- **All tools** show serious i18n/encoding bugs—this is a systemic quality gap

---

## 6. Trend Signals

### 🚨 Critical Industry Signals

**1. Agent Cost Explosion is the #1 Problem**
Multiple independent user reports across Claude Code, CodeWhale, and Gemini CLI describe 10M-400M token burns for simple tasks. The industry lacks:
- Configurable agent spawning caps
- Token budget alerts and kill switches
- Pre-execution cost estimates
- Per-agent token accounting

This is a market-shaping issue—the first tool to ship robust cost controls will win enterprise trust.

**2. Multi-Protocol Fragmentation is Accelerating**
- **ACP** (Agent Client Protocol) gains ground via Qwen Code (#4773, #4782)
- **MCP** (Model Context Protocol) deepens via Claude Code, OpenCode
- **SSE/REST** continues as default but with growing limitations

The ecosystem needs interoperability—tools that bridge protocols will have strategic advantage.

**3. TypeScript-to-Rust Migration**
- CodeWhale (Rust) vs. Claude Code (TypeScript)
- Pi (Go) vs. Copilot CLI (TypeScript)
- Kimi Code struggling with Python→TypeScript migration

Rust/Go tools show better performance, lower memory usage, and fewer runtime errors. Expect more tools to follow.

### 📈 Strategic Opportunities

**4. Local Model Renaissance**
Pi's Ollama support and CodeWhale's local benchmarks (#2902) suggest growing demand for offline/local AI CLI workflows. The bottleneck is local model latency (Pi #5464: 3-5 minute delays). First tool to solve "fast local inference" wins developers with privacy requirements.

**5. Session Lifecycle Management**
Every major tool now has session-related features in development:
- Persistent goals (OpenCode #27167)
- Pause/resume (Copilot CLI #1928)
- Session handoff (OpenAI Codex rust-v0.138.0)
- Session export/import (Pi #5533)
- KV cache capsules (CodeWhale #2904)

This is becoming table stakes—expect standardization within 6 months.

**6. Vim/Modal Editing Parity**
Copilot CLI (#13, 63 👍), Qwen Code (#4675), and CodeWhale all show strong demand for vim keybindings. This is a clear UX differentiator for developer adoption.

**7. WebSearch Integration**
Claude Code and OpenAI Codex have had web search for months; Qwen Code just added it (#4801). Gemini CLI and CodeWhale still lack it. This is increasingly expected as a core tool, not a premium feature.

**8. Declarative Agent Definitions**
Qwen Code (#4821), CodeWhale (#2482 WhaleFlow), and Claude Code's `.claude/agents/` pattern point to a future where agents are defined in YAML/Markdown frontmatter rather than code. This lowers the barrier to customization and enables community sharing.

### ⚠️ Systemic Risks

**9. CI/CD Reliability Crisis**
Qwen Code (#4864) merged code with all CI failing. OpenCode (#31434, #31446) has JSON output issues in CI. Copilot CLI (#3652) has 40-80s WSL startup delays. As AI CLIs become CI/CD pipeline components, reliability gaps will cause cascading failures.

**10. Security Fragility**
- SSRF via DNS hostnames (Gemini CLI #27744, #27739)
- Binary content causing hallucinated model responses (Gemini CLI #27412)
- Secrets exposure before redaction (Gemini CLI #26525)
- Tool-call markup leakage (OpenCode #31247)
- Credential Manager limits (Codex #17931)

Security issues are distributed and tool-specific—expect increased auditing pressure from enterprise buyers.

---

**Bottom line for technical decision-makers:**

*Choose Claude Code for plugin ecosystem depth and rapid iteration. Choose OpenAI Codex for enterprise tracing and desktop integration. Evaluate Qwen Code for protocol standards leadership. Watch Pi and CodeWhale for local model and cost optimization breakthroughs. Be cautious with Kimi Code until migration stabilizes. The tools that solve agent cost control in Q3 2026 will define the next competitive cycle.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-09 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following Pull Requests attracted the most community discussion and attention:

### #514 — Document Typography Skill *(Open, Created 2026-03-04)*
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents — addressing quality issues that affect virtually every document Claude produces.
**Discussion highlights:** Community identified this as a pervasive pain point; the PR author noted "these issues affect every document Claude generates." No objections or substantial revision requests.
**Link:** [PR #514](https://github.com/anthropics/skills/pull/514)

### #486 — ODT Skill — OpenDocument Creation & Template Filling *(Open, Created 2026-03-01)*
**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on mentions of ODT, ODS, LibreOffice, or ISO-standard document formats.
**Discussion highlights:** Strong demand for LibreOffice/OOXML interoperability. The skill covers both creation and parsing (ODT→HTML), making it a dual-purpose addition.
**Link:** [PR #486](https://github.com/anthropics/skills/pull/486)

### #210 — Improved Frontend-Design Skill *(Open, Created 2026-01-05)*
**Functionality:** Revises the existing frontend-design skill for clarity and actionability — ensuring every instruction is executable within a single conversation, with specific guidance to steer behavior.
**Discussion highlights:** Community flagged that the original skill was too vague. This PR reframes instructions to be Claude-executable rather than human-readable documentation.
**Link:** [PR #210](https://github.com/anthropics/skills/pull/210)

### #83 — Skill-Quality-Analyzer & Skill-Security-Analyzer *(Open, Created 2025-11-06)*
**Functionality:** Two meta-skills: (1) evaluates skills across Structure & Documentation, Examples, Resources, Trigger Precision, and Portability; (2) audits for security vulnerabilities in skill definitions.
**Discussion highlights:** A meta-skills initiative that generated substantial interest. Evaluates five quality dimensions with weighted scoring. Addresses a growing need for skill governance.
**Link:** [PR #83](https://github.com/anthropics/skills/pull/83)

### #538 — Fix Case-Sensitive File References in PDF Skill *(Open, Created 2026-03-06)*
**Functionality:** Corrects 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where uppercase file references (`REFERENCE.md`, `FORMS.md`) don't match actual lowercase filenames (`reference.md`, `forms.md`).
**Discussion highlights:** Though technically a bugfix, this PR exposed broader concerns about cross-platform compatibility, particularly on Linux filesystems where case-sensitivity breaks skill loading.
**Link:** [PR #538](https://github.com/anthropics/skills/pull/538)

### #1140 — Agent-Creator Skill + Multi-Tool Evaluation Fix *(Open, Created 2026-05-15)*
**Functionality:** Adds an 'agent-creator' meta-skill for generating task-specific agent sets, fixes `evaluation.py` to properly handle parallel tool calls, and adds Windows support via `%APPDATA%` paths.
**Discussion highlights:** Addresses a critical stability issue (#1120). The parallel tool-call evaluation fix is particularly important for skills that chain multiple tool invocations.
**Link:** [PR #1140](https://github.com/anthropics/skills/pull/1140)

---

## 2. Community Demand Trends

From Issues activity, the most-anticipated new Skill directions are:

| Demand Theme | Key Issue | Signal Strength |
|---|---|---|
| **Org-wide skill sharing** | [#228](https://github.com/anthropics/skills/issues/228) — "Skills should be shareable within an organization directly" | **Highest** (13 comments, 7 👍) |
| **Evaluation tooling fixes** | [#556](https://github.com/anthropics/skills/issues/556) — `run_eval.py` never triggers skills (0% trigger rate) | **High** (11 comments, 7 👍) |
| **Namespace & trust security** | [#492](https://github.com/anthropics/skills/issues/492) — Community skills under `anthropic/` namespace impersonate official skills | **Moderate/High** (7 comments) |
| **Duplicate skill elimination** | [#189](https://github.com/anthropics/skills/issues/189) — `document-skills` and `example-skills` plugins install identical content | **Moderate** (6 comments, 8 👍) |
| **Skill-creator best practices** | [#202](https://github.com/anthropics/skills/issues/202) — "skill-creator reads like developer documentation, not an operational skill" | **Moderate** (8 comments, closed) |
| **Agent governance patterns** | [#412](https://github.com/anthropics/skills/issues/412) — Safety patterns for AI agent systems | **Emerging** (4 comments) |
| **Multi-file preload for skills** | [#1220](https://github.com/anthropics/skills/issues/1220) — Bundle reference files inline rather than cross-referencing | **Emerging** (2 comments) |

**Key insight:** The community is demanding infrastructure and governance improvements over new domain skills — tooling stability, security boundaries, sharing mechanisms, and window management dominate the issue tracker.

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and are likely to land soon:

| PR | Skill | Status Signal | Last Update |
|---|---|---|---|
| [#190](https://github.com/anthropics/skills/pull/190) | n8n-builder, n8n-debugger, faf-expert | 4 production-tested skills bundled together; community-tested | 2026-05-18 |
| [#444](https://github.com/anthropics/skills/pull/444) | AURELION suite (kernel, advisor, agent, memory) | Structured cognitive framework with memory persistence; comprehensive | 2026-05-06 |
| [#568](https://github.com/anthropics/skills/pull/568) | ServiceNow platform skill | Covers ITSM, ITOM, ITAM, SecOps, HRSD, CSDM, IntegrationHub | 2026-04-23 |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns skill | Testing Trophy model, React Testing Library, E2E, edge cases | 2026-04-21 |
| [#335](https://github.com/anthropics/skills/pull/335) | Masonry image/video generation | Imagen 3.0 & Veo 3.1 integration with job management | 2026-03-14 |
| [#154](https://github.com/anthropics/skills/pull/154) | shodh-memory skill | Persistent context across conversations via proactive_context | 2026-03-03 |
| [#181](https://github.com/anthropics/skills/pull/181) | SAP-RPT-1-OSS predictor | Tabular foundation model for SAP business data predictive analytics | 2026-03-16 |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for infrastructure and governance tooling (skill evaluation, security auditing, org-wide sharing, and cross-platform reliability) rather than new domain-specific skills, indicating the ecosystem has reached a maturity stage where users need quality control, trust boundaries, and operational tooling to scale skill adoption safely.**

---

# Claude Code Community Digest
**2026-06-09**

## Today's Highlights

Two new capabilities shipped in v2.1.169 — a `--safe-mode` flag for troubleshooting customization issues and a `/cd` command to move sessions without breaking the prompt cache. Meanwhile, the community continues raising alarms around excessive agent spawning and token consumption, with multiple reports showing Claude deploying 50+ parallel agents for simple tasks, burning through context windows at alarming rates. A critical safety bug involving Opus 4.8 fabricating user messages has also surfaced.

## Releases

**[v2.1.169](https://github.com/anthropics/claude-code/releases/tag/v2.1.169)** — Two notable additions:
- **`--safe-mode` flag** (plus `CLAUDE_CODE_SAFE_MODE` env var): Starts Claude Code with all customizations disabled — CLAUDE.md, plugins, skills, hooks, and MCP servers — for troubleshooting configuration conflicts.
- **`/cd` command**: Moves a session to a new working directory without breaking the prompt cache, solving a long-standing friction point for developers who need to navigate between projects mid-session.

## Hot Issues

1. **[#60334](https://github.com/anthropics/claude-code/issues/60334) — Image processing failures burning API quota** (60 comments, closed)  
   A high-engagement bug where Claude repeatedly reports "an image could not be processed" on messages containing no images, wasting up to 70% of the 5-hour usage window. Community frustration is high — 14 upvotes suggest this is widespread.

2. **[#48827](https://github.com/anthropics/claude-code/issues/48827) — Cowork downloads Linux binary on Intel Mac** (18 comments, open)  
   The Cowork feature crashes on Intel macOS with exit code 132 (SIGILL) because it downloads an ELF Linux binary instead of a macOS binary. A duplicate [#66367](https://github.com/anthropics/claude-code/issues/66367) confirms others hitting the same bug.

3. **[#16550](https://github.com/anthropics/claude-code/issues/16550) — Allow Claude to write/update project files** (32 comments, open, 59 👍)  
   The most-upvoted open feature request. Users want Claude to have write access to project files beyond the current read-and-suggest paradigm. This has been open for 5 months with no official response.

4. **[#27725](https://github.com/anthropics/claude-code/issues/27725) — Detachable OS-level windows in desktop app** (13 comments, open, 54 👍)  
   Strong demand for split-screen multitasking — users want to tear chat panels into separate OS windows rather than being confined to the desktop app's tab structure.

5. **[#64349](https://github.com/anthropics/claude-code/issues/64349) — VS Code extension forces 1M context on Pro plan** (9 comments, open)  
   Windows users on the Pro plan report the VS Code extension forces 1M context windows, bypassing plan limits and potentially causing surprise billing or degraded performance.

6. **[#61044](https://github.com/anthropics/claude-code/issues/61044) — MCP tool calls in Routines fail with "requires approval"** (6 comments, open)  
   MCP tools invoked within Claude Code Routines trigger an approval prompt that cannot be dismissed — no approval UI is shown, and reconnection doesn't resolve the deadlock.

7. **[#29937](https://github.com/anthropics/claude-code/issues/29937) — Terminal rendering corruption in tmux** (10 comments, open, 22 👍)  
   Text overlaps and previous output isn't cleared correctly when running inside tmux, affecting power users who rely on terminal multiplexers. Reproduced across Alacritty and standard emulators.

8. **[#66353](https://github.com/anthropics/claude-code/issues/66353) — Sonnet 4.6 deployed 56-agent parallel for simple image upload** (1 comment, open)  
   Another alarming cost-control report: Claude spawned 56 parallel agents to handle a single image upload task. Paired with [#65920](https://github.com/anthropics/claude-code/issues/65920) (272 agents, 10M+ tokens for code analysis), this is becoming a pattern.

9. **[#66396](https://github.com/anthropics/claude-code/issues/66396) — Japanese text corruption in tool outputs on Windows** (1 comment, open)  
   Large tool outputs containing Japanese characters become corrupted and expand into fabricated lines on Windows. A localization bug that impacts international teams.

10. **[#66400](https://github.com/anthropics/claude-code/issues/66400) — Tool calls fail with "malformed and could not be parsed"** (0 comments, open)  
    A newly filed bug where tool-call markup is rendered as plain chat text and intermittently fails to parse, especially in environments with multiple concurrent sessions or git worktrees.

## Key PR Progress

1. **[#65286](https://github.com/anthropics/claude-code/pull/65286) — Fix missing plugin.json manifest for plugin-dev** (open)  
   Adds the missing `.claude-plugin/plugin.json` manifest so the `plugin-dev` plugin can be discovered and installed through normal plugin channels.

2. **[#65619](https://github.com/anthropics/claude-code/pull/65619) — Align frontend-design author with marketplace entry** (closed)  
   Fixes a malformed plugin manifest where two authors were packed into a single JSON field, fixing UI rendering in plugin marketplaces.

3. **[#66372](https://github.com/anthropics/claude-code/pull/66372) — Detect Docker daemon failures via $LASTEXITCODE** (open)  
   Fixes a PowerShell script bug where `docker info` failures weren't caught because try/catch doesn't handle native command non-zero exits — the script falsely reports Docker is running when it isn't.

4. **[#26914](https://github.com/anthropics/claude-code/pull/26914) — Add rules frontmatter syntax examples and validation hook** (closed)  
   Documents the root cause of silent failures in `paths:` frontmatter syntax and provides a PostToolUse hook for validation. A long-lived PR (4 months) finally merged.

5. **[#66171](https://github.com/anthropics/claude-code/pull/66171) — Fix symlink following in extensibility.py** (open)  
   Addresses a security issue where project-controlled GUI components could follow symlinks outside intended boundaries.

## Feature Request Trends

- **Agent spawning & cost control**: Three separate issues this week (including #66353, #65920) highlight a major pain point — Claude over-delegates to agents for trivial tasks. Users are demanding better heuristic guardrails.
- **Session mobility**: Requests for detachable windows (#27725, 54 👍), local-to-cloud session handoff (#66373), and the newly shipped `/cd` command show strong demand for flexible session management.
- **Cross-agent skill sharing**: [#66352](https://github.com/anthropics/claude-code/issues/66352) proposes user-level skill discovery directories, enabling single-source-of-truth workflows across multiple agents.
- **Startup customization**: [#65788](https://github.com/anthropics/claude-code/issues/65788) requests the ability to suppress or theme the interactive welcome banner, as it interferes with custom launcher scripts.
- **Actionable keybindings**: [#66399](https://github.com/anthropics/claude-code/issues/66399) asks for custom file-opening actions in the keybinding system, extending beyond the current predefined action set.

## Developer Pain Points

- **Runaway token consumption**: The #1 pain point this week. Multiple reports describe Claude burning through 10M+ tokens for simple tasks (code analysis, image upload) by spawning dozens to hundreds of agents. Users feel powerless to control this behavior.
- **Linux/macOS binary mismatch**: The Cowork feature (desktop companion) repeatedly downloads Linux ELF binaries for Intel macOS users, causing immediate crashes. This has been reported multiple times (#48827, #66367) over two months.
- **MCP permission deadlocks**: Tools that require approval either show no approval UI (#61044) or ignore claude.ai connector settings (#64521), leaving users in an unrecoverable state.
- **Terminal rendering issues**: tmux corruption (#29937) and cursor visibility issues in agent-view (#66398) persist, affecting the CLI's core usability for multiplexer users.
- **Internationalization bugs**: Japanese text corruption on Windows (#66396) and newline injection in code blocks (#66371) suggest insufficient testing of non-ASCII and long-form content paths.
- **Documentation gaps**: Multiple documentation issues filed today alone (#66384, #66380, #66395, #66394) highlight that features are shipping without corresponding docs, particularly around managed MCP policies and server-managed settings behavior.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-09

## Today's Highlights
A new `rust-v0.138.0` release introduces seamless CLI-to-Desktop handoff on macOS and Windows. The community is sharply focused on `gpt-5.5` availability issues — model metadata claims it's available but requests fail with 404, affecting both Desktop and CLI users. Multiple PRs land infrastructure improvements around Guardian review compaction, plugin analytics, and async hooks, signaling active investment in reliability and extensibility.

## Releases
- **rust-v0.138.0**: The `/app` command can now hand off the current CLI thread into Codex Desktop on macOS and native Windows. Windows workspace launches can open directly into Desktop instead of stopping at a manual prompt. Also includes local image attachments and standalone image generation support.
- **rust-v0.139.0-alpha.1**, **rust-v0.138.0-alpha.8**, **rust-v0.138.0-alpha.7**: Alpha releases with no additional changelog details published.

## Hot Issues

1. **[#26892 — gpt-5.5 listed as available but fails with 404](https://github.com/openai/codex/issues/26892)**  
   *76 comments, 28 👍*  
   Model metadata declares `gpt-5.5` available, but actual API requests fail with "Model not found." Only affects 5.5 — 5.4 works normally. The highest-engagement open bug; community frustration is palpable as users cannot use the advertised model.

2. **[#25144 — Option to disable automatic conversion of long prompts to .txt attachments](https://github.com/openai/codex/issues/25144)**  
   *52 comments, 65 👍*  
   Users want control over paste behavior. Long structured prompts are silently converted to `.txt` file attachments, disrupting workflows. High upvote count indicates broad desire for configuration.

3. **[#25203 — GitHub OAuth callback fails on Windows](https://github.com/openai/codex/issues/25203)**  
   *37 comments, 21 👍*  
   "Unable to find Electron app" error prevents GitHub connection from Codex Desktop on Windows. Blocks CI/CD integrations and repository browsing.

4. **[#25715 — Codex App unusably slow with WSL as agent environment](https://github.com/openai/codex/issues/25715)**  
   *36 comments, 36 👍*  
   Routine operations become non-responsive. Users report seconds-to-minutes latency for basic turns. Windows + WSL users are heavily affected.

5. **[#21671 — /compact fails with unknown service_tier parameter](https://github.com/openai/codex/issues/21671)**  
   *25 comments, 5 👍 (CLOSED)*  
   Regression in 0.129.0 where `/compact` sends an invalid `service_tier` parameter. Closed as fixed — good signal that core compaction issues are being addressed despite related open issues.

6. **[#8758 — Image generation from Codex](https://github.com/openai/codex/issues/8758)**  
   *23 comments, 55 👍 (CLOSED)*  
   Long-standing request for visual asset generation. Now realized in the latest release with standalone image generation support. Community excited about closing this gap.

7. **[#24675 — Stale app connector link after reauth-required 401](https://github.com/openai/codex/issues/24675)**  
   *21 comments, 16 👍*  
   Desktop keeps using stale connector links after authentication failures. Requires manual cache clearing to resolve. Affects Linear and other plugin connectors.

8. **[#25719 — macOS syspolicyd/trustd CPU and memory runaway](https://github.com/openai/codex/issues/25719)**  
   *20 comments, 20 👍*  
   Codex Desktop on macOS triggers system daemon resource exhaustion. High CPU/memory from `syspolicyd` and `trustd` persists until Codex is killed.

9. **[#25249 — Semi-transparent sidebar renders incorrectly on Windows](https://github.com/openai/codex/issues/25249)**  
   *15 comments, 0 👍*  
   Visual bug: maximized window with semi-transparent sidebar shows undrawn/transparent regions. Cosmetic but noticeable.

10. **[#12029 — Ability to use more than one account](https://github.com/openai/codex/issues/12029)**  
    *9 comments, 43 👍*  
    Users need personal + corporate accounts on the same machine. Current auth sharing across all Codex surfaces is a blocker. High upvote-to-comment ratio suggests strong latent demand.

## Key PR Progress

1. **[#27101 — Load user instructions through an injected provider](https://github.com/openai/codex/pull/27101)**  
   Removes implicit `$CODEX_HOME` dependency from `codex_core`. Shifts `AGENTS.md` loading responsibility to embedders. Starts loading user-level `AGENTS.md` when no primary environment is specified. Architectural improvement for decoupling.

2. **[#26953 — Add dedicated Python SDK goal operations](https://github.com/openai/codex/pull/26953)**  
   New goal API in the Python SDK that matches TUI-driven persisted goals. Callers see one logical turn even when runtime creates continuations. Enables better programmatic control.

3. **[#27107 — Add spans to run_turn](https://github.com/openai/codex/pull/27107)**  
   Granular latency tracing for turn orchestration, prompt preparation, and tool-loading costs. Helps developers identify performance bottlenecks in the app-server.

4. **[#27039 — Add detached async command hooks](https://github.com/openai/codex/pull/27039)**  
   Previously, `async: true` hooks were rejected during discovery. Now they can run outside the blocking hook lane with a deliberately narrower contract (no blocking, rewriting, or error reporting).

5. **[#27091 — Eagerly compact Guardian threads between reviews](https://github.com/openai/codex/pull/27091)**  
   Schedules compaction for reused Guardian review sessions immediately after a review completes, when context exceeds threshold. Thread-safe with owned mutex guard. Improves auto-review performance.

6. **[#25704 — Normalize Codex images for Responses strict mode](https://github.com/openai/codex/pull/25704)**  
   Feature-flagged strict-mode image processing for `/responses`. Converts local/data URLs to prepared data URIs before history recording and API sending. Foundation for stricter image handling.

7. **[#27102 — Centralize plugin telemetry metadata construction](https://github.com/openai/codex/pull/27102)**  
   Routes all plugin install/uninstall/enable/disable/use events through centralized `PluginsManager` metadata constructor. Reduces duplication and improves analytics consistency.

8. **[#27017 — Fix Windows deny-read across exec runtimes](https://github.com/openai/codex/pull/27017)**  
   Windows `deny_read` entries existed in permission profiles but `shell_command` and `exec_command` didn't resolve filesystem overrides. Fix ensures restrictions are actually enforced.

9. **[#17931 — Support encrypted local secrets for keyring auth](https://github.com/openai/codex/pull/17931)**  
   Works around Windows Credential Manager's 2,560-byte limit by encrypting large auth payloads and storing them locally. Fixes keyring failures for ChatGPT and MCP OAuth tokens.

10. **[#26880 — Preserve fsmonitor for worktree Git reads](https://github.com/openai/codex/pull/26880)**  
    Previously forced `core.fsmonitor=false` on every internal Git command, disabling built-in fsmonitor and causing full scans in large repos. Now probes effective fsmonitor setting instead.

## Feature Request Trends
- **Multi-account support** (#12029, 43 👍) — high demand for personal + corporate account coexistence on one machine
- **Image generation** (#8758, 55 👍, now implemented in v0.138.0) — users want native visual asset creation without leaving Codex
- **Paste behavior control** (#25144, 65 👍) — users want opt-out for automatic `.txt` conversion of long prompts
- **Claude Code hook parity** (#21753) — community wants full lifecycle automation surface (29+ hook types)
- **Worktree support** (#12863) — users want to use git worktrees created outside Codex without friction

## Developer Pain Points
- **Model availability confusion**: `gpt-5.5` listed as available but actually failing (#26892) — erodes trust in model metadata
- **Windows + WSL performance**: Multiple reports of extreme slowdown (#25715, #26149) — the most common performance pain point
- **Authentication and session fragility**: Stale connectors after reauth (#24675), missing sessions after restart (#19615, #27104) — reliability concerns
- **Windows-specific issues**: OAuth callback failure (#25203), semi-transparent sidebar rendering (#25249), Credential Manager limits (#17931), deny-read bypass (#27017)
- **Compact/compaction regressions**: `/compact` failures (#21671), stale service_tier issues (#22876) — essential session management is fragile
- **Guardian review instability**: Dying agent loops (#23971), high CPU on macOS (#26415) — auto-review system still maturing

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-09

## Today's Highlights
A new nightly release (v0.47.0) ships with a fix to limit Antigravity transition banner frequency and removes "experimental" labels from browser agent docs. The community remains focused on agent reliability: the generalist agent hang bug (#21409) continues to attract attention with 8 👍, and multiple issues around Auto Memory retry loops and security redaction are seeing active triage. Several important SSRF fixes are in review for the web_fetch tool.

## Releases
**v0.47.0-nightly.20260609.g0567b25a2**
- Updated the max display count for the Antigravity transition banner ([PR #27676](https://github.com/google-gemini/gemini-cli/pull/27676))
- Removed "experimental" text from browser agent documentation ([PR #27746](https://github.com/google-gemini/gemini-cli/pull/27746), now closed)

## Hot Issues (10 noteworthy)

1. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, Bug, 7 comments, 8 👍)  
   The community's most-voted issue: the CLI hangs indefinitely when deferring to the generalist agent for simple operations (e.g., folder creation). Users report waiting up to an hour before cancelling. Workaround: instructing the model not to use sub-agents. This is a top-priority agent reliability problem.

2. **[#22745 — AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (P2, Feature, 7 comments, 1 👍)  
   Epic tracking whether AST-aware tools can reduce turn counts, token noise, and misaligned reads. Could meaningfully improve code understanding quality.

3. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, Bug, 6 comments, 2 👍)  
   Critical bug where the `codebase_investigator` subagent reports "success" even after hitting the maximum turn limit, hiding interruptions from users. Misleading UX for agent orchestration.

4. **[#25166 — Shell command execution stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, Bug, 4 comments, 3 👍)  
   Simple CLI commands (that require no input) leave the shell in a "Waiting input" state after completion. High frustration due to frequency of occurrence.

5. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, Bug, 5 comments)  
   Security concern: Auto Memory reads local transcripts before the extraction prompt redacts secrets, meaning sensitive content is already in model context. Also logs existing skill data unnecessarily.

6. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, Bug, 5 comments)  
   Auto Memory only marks sessions as processed when the extraction agent successfully reads the transcript — low-signal sessions remain unprocessed and are surfaced repeatedly, creating infinite retry loops.

7. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, Bug, 6 comments)  
   Anecdotal but widely echoed: the model does not autonomously leverage custom skills or sub-agents even when the task is directly related to their descriptions. Users must explicitly instruct it.

8. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, Bug, 4 comments, 1 👍)  
   Linux Wayland users experience browser agent failures. The agent terminates with "GOAL" status despite not completing the task.

9. **[#20079 — Symlinked agent files not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** (P2, Bug, 4 comments)  
   `~/.gemini/agents/` ignores symlinked `.md` files, preventing users from organizing agent definitions with symlinks.

10. **[#24246 — 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2, Bug, 3 comments)  
    When more than ~128 tools are available, the CLI returns a 400 error. Suggests the agent lacks tool-scoping intelligence.

## Key PR Progress (10 important PRs)

1. **[#27749 — Vertex AI model mapping fix](https://github.com/google-gemini/gemini-cli/pull/27749)** (Open, size/m)  
   Refactors Vertex AI model mapping to use shared constants, improving consistency and maintainability across configuration.

2. **[#27729 — Truncate telemetry metric attributes to 1024 chars](https://github.com/google-gemini/gemini-cli/pull/27729)** (Open, P2, area/enterprise)  
   Fixes Node.js stack trace flooding in terminal when exporting telemetry to GCP Monitoring, caused by attribute length > 1024 chars.

3. **[#27505 — Prevent extra spaces on width-0 CJK continuation cells](https://github.com/google-gemini/gemini-cli/pull/27505)** (Open, P2, area/core)  
   Fixes rendering bug injecting extra spaces between CJK characters in shell output, improving cross-platform terminal display for CJK users.

4. **[#27698 — Zero-quota limits fail fast to prevent retry loop hang](https://github.com/google-gemini/gemini-cli/pull/27698)** (Open, size/s)  
   Critical fix: when hitting a hard quota limit of 0 (unbilled free-tier accounts), the CLI was stuck in a 10-attempt retry loop. Now fails fast.

5. **[#27619 — Atomic update in MCP tool discovery](https://github.com/google-gemini/gemini-cli/pull/27619)** (Open, size/s)  
   Prevents "tool not found" errors during transient network drops by ensuring the tool registry retains the last known good MCP tool set.

6. **[#27747 — Prevent infinite loop in ghost text wrapping](https://github.com/google-gemini/gemini-cli/pull/27747)** (Open, P2, help wanted)  
   Fixes CLI freeze when `@filename:line` completion is active in a terminal too narrow to display wide characters (e.g., emoji at width 2 in 1-column window).

7. **[#27744 — Fix SSRF via DNS hostnames](https://github.com/google-gemini/gemini-cli/pull/27744)** (Open, size/l)  
   Resolves DNS-based SSRF bypass: `isBlockedHost()` only checked if the hostname was an IP literal, allowing wildcard DNS services (e.g., `127.0.0.1.nip.io`) to reach private IPs.

8. **[#27739 — Prevent SSRF via DNS hostnames and redirects](https://github.com/google-gemini/gemini-cli/pull/27739)** (Open, size/l)  
   Complementary fix adding redirect-aware SSRF protection: `isBlockedHost` only inspects the entry URL, not redirect targets. Also patches timing-based scans and header-injection scans.

9. **[#27428 — Use docker inspect exit code instead of stdout parsing](https://github.com/google-gemini/gemini-cli/pull/27428)** (Open, P1, area/core)  
   Fixes sandbox `imageExists` false negatives caused by Docker outputting image names to stderr (e.g., with `DOCKER_BUILDKIT`).

10. **[#27412 — Prevent model fabrication when read_file returns binary content](https://github.com/google-gemini/gemini-cli/pull/27412)** (Closed, P2)  
    When `read_file` processes binary content (e.g., PDFs), the response is now a descriptive string rather than raw binary, preventing hallucinated analyses.

## Feature Request Trends

- **AST-aware tooling (3 open issues):** Strong interest in using abstract syntax trees for more precise file reads, search, and codebase mapping to reduce token waste and improve accuracy.
- **Agent self-awareness & orchestration (2 open issues):** Users want the agent to accurately describe its own capabilities, CLI flags, hotkeys, and to use sub-agents and skills autonomously without explicit instruction.
- **Remote & background agents (2 open issues):** Continued demand for task-level auth, 1P agent support, and background processing for remote agent execution.
- **Open Plugins & extension support (1 merged PR):** Automatically discovering sub-agents defined in Open Plugin directories, with namespacing and variable expansion.

## Developer Pain Points

- **Agent hangs and silent failures:** The generalist agent hang (#21409) and subagent MAX_TURNS misreporting (#22323) create frustrating black-hole experiences where users wait indefinitely or receive false success signals.
- **Shell execution flakiness:** Commands stuck in "Waiting input" (#25166), zero-quota infinite retry loops (#27698), and binary content triggering hallucinated model responses (#27408 / #27412) erode trust in automation.
- **Auto Memory inefficiency & security risk:** Indefinite retries of low-signal sessions (#26522) combined with secrets exposure before redaction (#26525) make the memory system both wasteful and potentially insecure.
- **Browser agent configuration gaps:** The browser agent ignores `settings.json` overrides (#22267) and fails entirely on Wayland (#21983), limiting Linux adoption.
- **Tool overload and error thresholds:** Hitting a 400 error with >128 tools (#24246) signals a lack of intelligent tool-scoping, forcing users to manually manage tool subsets.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest — 2026-06-09**

## Today's Highlights
Activity remained steady with no new releases in the last 24 hours. The community is heavily focused on input modality improvements (Vim mode, clipboard behavior, input history), alongside emerging frustrations with model switching limitations and custom registry support. Three closed PRs/Issues landed regarding streaming, cron scheduling, and hook enhancements.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#13 — CLI input should have a vi/vim input mode](https://github.com/github/copilot-cli/issues/13)** (👍 63, 7 comments)  
   Long-standing feature request with strong community resonance. Users want modal editing capabilities in interactive CLI sessions. No official response yet.

2. **[#1928 — Allow to pause copilot work](https://github.com/github/copilot-cli/issues/1928)** (👍 2, 9 comments)  
   Proposes a pause mechanism to correct mid-session misdirection without restarting. High engagement suggests workflow fragility.

3. **[#3547 — Background sub-agent hangs at total_turns=0 with gpt-5.5](https://github.com/github/copilot-cli/issues/3547)** (6 comments)  
   Spawned agents silently stall with no progress. Potentially a model-level regression or dispatch bug affecting background task reliability.

4. **[#3436 — /mcp search constructs wrong URL for custom MCP registries](https://github.com/github/copilot-cli/issues/3436)** (5 comments)  
   Missing `/v0.1/` path segment in URL construction causes 404 errors for self-hosted registries. Breaks enterprise custom MCP deployments.

5. **[#2867 — Claude Opus 4.6 returns "model not supported" after quota wait](https://github.com/github/copilot-cli/issues/2867)** (5 comments)  
   Users following retry-after instructions are met with unrecoverable errors. Indicates poor state management across quota cycles.

6. **[#2540 — Plugin-defined preToolUse hooks never fire](https://github.com/github/copilot-cli/issues/2540)** (👍 3, 4 comments)  
   `hooks.json` preToolUse hooks are completely silent, both in main sessions and sub-agents. Core plugin extensibility broken.

7. **[#2201 — sessionStart hook doesn't print or run at CLI startup](https://github.com/github/copilot-cli/issues/2201)** (3 comments)  
   Hook tutorial flow broken; `Write-Host` output never reaches terminal. New users can't validate hook setup.

8. **[#3652 — 40-80 second WSL startup delay in VS Code Chat](https://github.com/github/copilot-cli/issues/3652)** (3 comments)  
   `listSessions` call introduces major latency on WSL. Educational quota users particularly affected.

9. **[#3716 — Function call regression in 1.0.60](https://github.com/github/copilot-cli/issues/3716)** (1 comment)  
   JSON schema validation failure for tools.function.parameters suggests a Moonshot-compatibility regression in the latest release.

10. **[#3709 — /model doesn't list BYOK providers](https://github.com/github/copilot-cli/issues/3709)** (1 comment)  
    BYOK/local models excluded from in-session model switcher, forcing single-model sessions for custom providers.

## Key PR Progress
1. **[#1960 — install: use GITHUB_TOKEN for authenticated requests](https://github.com/github/copilot-cli/pull/1960)** (CLOSED)  
   Enables authenticated curl/wget downloads and git ls-remote, bypassing rate limits and supporting private repos.

2. **[#3717 — BYOK: Add an option to disable streaming](https://github.com/github/copilot-cli/issues/3717)** (CLOSED)  
   Feature proposal for `stream:false` support via env var `COPILOT_PROVIDER_DISABLE_STREAMING`. Closed as merged or accepted.

3. **[#3714 — Claude Code cron scheduled task feature](https://github.com/github/copilot-cli/issues/3714)** (CLOSED)  
   Request for scheduled/recurring task execution. Closed without resolution, indicating low priority.

4. **[#3713 — Add updatedPrompt output field to userPromptSubmitted hook](https://github.com/github/copilot-cli/issues/3713)** (CLOSED)  
   Hook enhancement enabling prompt modification before model processing. Quickly accepted.

5. **[#2948 — --available-tools silently ignored in ACP mode](https://github.com/github/copilot-cli/issues/2948)** (CLOSED)  
   Bug affecting tool filtering in autonomous mode. Now resolved.

6. **[#3701 — Runaway MCP server spawning on Windows](https://github.com/github/copilot-cli/issues/3701)** (CLOSED)  
   IDE lock-file watcher re-init loop caused infinite MCP server spawns. Critical stability fix.

7. **[#3688 — Repository agents resolved relative to git root, skills/MCP relative to cwd](https://github.com/github/copilot-cli/issues/3688)** (OPEN)  
   Inconsistency in customization source resolution. Triaged but no fix yet.

8. **[#3477 — Enterprise OTel auth: mTLS + dynamic headers](https://github.com/github/copilot-cli/issues/3477)** (OPEN)  
   Parity gap with Claude Code for production OTel deployments. Under active discussion.

9. **[#3719 — Windows: /add-dir with ~ fails due to backslash autocomplete](https://github.com/github/copilot-cli/issues/3719)** (OPEN)  
   Autocomplete override interferes with Unix-style home directory references on Windows.

10. **[#3724 — Windows Terminal copy-on-select circumvented by Copilot CLI](https://github.com/github/copilot-cli/issues/3724)** (OPEN)  
    CLI suppresses native terminal clipboard feature. Platform integration bug.

## Feature Request Trends
- **Input modality parity** — Vim/vi mode (#13), `ESC ESC` history stashing (#3720), and direct numeric input consistency (#3715) dominate input UX requests.
- **Session & multitasking management** — Pause/resume (#1928), concurrent session tooling (#2966), and background task scheduling (#3714) signal demand for production-grade session lifecycle control.
- **Model flexibility & cost control** — BYOK provider listing in `/model` (#3709), lower-cost open-weight model support (#3707), and per-session model switching indicate enterprise cost-consciousness.
- **Plugin/hook depth** — `updatedPrompt` output in hooks (#3713), reliable `preToolUse` (#2540), and startup hook execution (#2201) reflect growing reliance on extensibility.

## Developer Pain Points
- **Broken extensibility** — Plugin `preToolUse` hooks completely non-functional (#2540), session hooks don't run at startup (#2201), and agent-level tool whitelists not enforced (#2638) erode trust in the plugin system.
- **Platform inconsistencies** — WSL startup delays (#3652), Windows uninstall failures (#3662), FreeBSD install script misdetection (#3710), and ReFS sandbox limitation (#3712) create platform-specific friction.
- **Model state mismanagement** — "Model not supported" after quota wait (#2867), silent sub-agent hangs (#3547), and model switch inconsistency (#3715) suggest fragile model lifecycle handling.
- **Custom registry integration** — Wrong URL construction (#3436), missing `/v0.1/` path, and inability to discover BYOK models via `/model` (#3709) hinder self-hosted deployments.
- **Input & rendering regressions** — Multi-line input disappearance (#3722), missing copy-on-select (#3724), and backslash autocomplete corruption (#3719) degrade the interactive UX.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-06-09

## Today's Highlights
The repository remained quiet with no new releases or pull requests in the last 24 hours. Community attention has focused on a regression in the latest v0.11.0 release (broken API key authentication and file attachment support), and the ongoing migration from the Python-based CLI to the TypeScript rewrite (kimi-code) has officially been flagged for documentation deprecation.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#2436 – Installation failed. The new Kimi Code is installed ✓ Kimi can't seem to make up her mind.](https://github.com/MoonshotAI/kimi-cli/issues/2436)**  
   *User running version 1.47.0 reports an installation process that simultaneously claims success and failure. The contradictory UX is confusing and indicates a possible race condition or incomplete migration path. Low engagement (1 comment).*

2. **[#2442 – Broken Workflow: API key authentication silently removed](https://github.com/MoonshotAI/kimi-cli/issues/2442)**  
   *Regression in v0.11.0 where API key authentication was silently dropped from the "Kimi Code" subscription path. User on macOS with model 2.6 reports workflows now fail without clear error messaging. No comments yet – likely a high-severity blocker for authenticated users.*

3. **[#2441 – New version does not even support @filename now?](https://github.com/MoonshotAI/kimi-cli/issues/2441)**  
   *User on v0.11.0 reports that the @filename file attachment feature, a core workflow pattern, is no longer functional. The community may be losing basic convience features during the TypeScript migration. Bilingual issue (Chinese/English).*

4. **[#2376 – [CLOSED] Add deprecation banner on GitHub Pages](https://github.com/MoonshotAI/kimi-cli/issues/2376)**  
   *Closed enhancement requesting that all GitHub Pages documentation clearly state that python-based kimi-cli is superseded by the TypeScript rewrite. The issue was filed May 27 and closed June 8 – likely implemented or deferred. Important signal for users evaluating which codebase to adopt.*

5. **[#2298 – [Feature] Support for `.clinerules` file](https://github.com/MoonshotAI/kimi-cli/issues/2298)**  
   *Ongoing request to adopt a standard configuration file pattern (like Cursor's `.cursorrules`) for project-level agent instructions. High demand from multi-project users.*

6. **[#2320 – [Bug] Model switching in `kimi-code` broken after first context](https://github.com/MoonshotAI/kimi-cli/issues/2320)**  
   *First use of a model works, subsequent attempts silently fall back to default. Indicates context handling issues in the TypeScript rewrite. Multiple users have confirmed.*

7. **[#2341 – [Feature] Persistent chat history across sessions](https://github.com/MoonshotAI/kimi-cli/issues/2341)**  
   *Request for local chat history save/load support. Currently all context is lost on CLI restart. This feature would significantly improve daily developer usage.*

8. **[#2390 – [Bug] `kimi-code` hangs on large file input with `@file`](https://github.com/MoonshotAI/kimi-cli/issues/2390)**  
   *File input over ~500KB causes the TypeScript CLI to freeze without feedback. Community members have suggested implementing streaming or chunking.*

9. **[#2285 – [Feature] Universal `kimi.code.md` config file](https://github.com/MoonshotAI/kimi-cli/issues/2285)**  
   *Similar to #2298, developers want a single Markdown config file that controls agent behavior, model selection, and tool access. High overlap with the `.clinerules` request.*

10. **[#2401 – [Bug] Chinese characters garbled in terminal output](https://github.com/MoonshotAI/kimi-cli/issues/2401)**  
    *UTF-8 encoding issue affecting non-English users. The bilingual nature of the community (CN/EN) makes this a recurring pain point. Users report having to manually set `export LANG=zh_CN.UTF-8`.*

## Key PR Progress
No pull requests were updated in the last 24 hours.

## Feature Request Trends
- **Project-level configuration files** (#2298, #2285): The community strongly desires a single, standardized config file (e.g., `.clinerules`, `kimi.code.md`) to define agent instructions, model selection, and tool policies per project.
- **Persistent chat sessions** (#2341): Developers want to resume conversations across CLI restarts without losing context, a basic usability expectation.
- **Cross-version documentation clarity** (#2376): Users are confused about which CLI (Python vs. TypeScript) to use; better deprecation markers and migration guides are repeatedly requested.

## Developer Pain Points
- **Regression in v0.11.0** (#2442, #2441): The latest release silently broke API key authentication and the `@filename` attachment syntax. Users perceive this as a loss of core functionality during the TypeScript migration.
- **TypeScript rewrite instability** (#2320, #2390): Hanging on large files, broken model switching, and encoding issues are eroding trust in the new codebase.
- **Unclear migration path** (#2436, #2376): Users report confused installation messages and find it difficult to know whether they should use the Python or TypeScript version. The deprecation banner closure is a step forward, but documentation still lacks clear "which one should I use?" guidance.
- **Missing `@filename` support** (#2441): This is a foundational workflow for many developers. Its removal in v0.11.0 is a high-friction point that may drive users to alternative CLI tools.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-09

## Today's Highlights
A surge of regression bugs hit OpenCode today, especially around the `session_message.seq` NOT NULL constraint failure introduced by recent database migrations (v1.15.13+). Bedrock Mantle users face two distinct issues: empty successful responses from GPT-5.5 and signature mismatches against OpenAI-compatible endpoints. On the positive side, the first PR landscape for the new v2 UI layout is taking shape, with multiple contributors addressing visual regressions.

## Releases
No new versions were released in the last 24 hours.

## Hot Issues

1. **[#27167 – Add native session goals with /goal](https://github.com/anomalyco/opencode/issues/27167)**  
   *Comments: 37 · 👍 65*  
   The most upvoted open feature request. Users want persistent session lifecycle goals beyond ephemeral slash commands. Community strongly agrees this fills a gap in agentic workflows.

2. **[#5474 – `/undo` doesn't revert file changes](https://github.com/anomalyco/opencode/issues/5474)**  
   *Comments: 28*  
   Long-standing UX bug: `/undo` only rolls back chat messages but leaves file modifications intact. Creates dangerous confusion when developers think changes have been reverted.

3. **[#29548 – OpenAI provider headers timeout regression in 1.15.11](https://github.com/anomalyco/opencode/issues/29548)**  
   *Comments: 11*  
   A 10s header timeout on OpenAI provider after upgrading from 1.14.28. User found workaround by increasing `headerTimeout`; indicates a configuration default regression.

4. **[#31247 – Opus 4.8 via Copilot leaks tool-call text](https://github.com/anomalyco/opencode/issues/31247)**  
   *Comments: 6*  
   Tool-heavy sessions cause Claude Opus 4.8 to emit raw tool-call markup (e.g., `call read`, `<invoke>`) into normal assistant messages, then hitting prefill 400 errors. Serious for production agentic use.

5. **[#15535 – Support MCP Resources in addition to MCP Tools](https://github.com/anomalyco/opencode/issues/15535)**  
   *Comments: 6 · 👍 16*  
   OpenCode only exposes `tools/call` from MCP servers, not `resources/read`. Users building MCP services need this parity. Gaining strong traction.

6. **[#31204 – NOT NULL constraint failed on agent-switched sessions](https://github.com/anomalyco/opencode/issues/31204)**  
   *Comments: 4*  
   Critical crash: sessions that trigger an agent switch after the June 3-5 migrations hit `session_message.seq` constraint violation. Blocks agent switching entirely.

7. **[#31430 – Bedrock Mantle GPT-5.5 returns empty successful responses](https://github.com/anomalyco/opencode/issues/31430)**  
   *Comments: 3*  
   The new Mantle provider can return 200 OK with empty content, causing OpenCode to stop mid-task without error. Hard to debug; blocks adoption of GPT-5.5 via Bedrock.

8. **[#31349 – Bedrock Mantle OpenAI API signature mismatch](https://github.com/anomalyco/opencode/issues/31349)**  
   *Comments: 5*  
   SigV4 auth configured for Bedrock Mantle's OpenAI-compatible endpoint fails with signature mismatch. Impacts enterprise users with strict security requirements.

9. **[#16960 – Compaction loses AGENTS.md/CLAUDE.md context](https://github.com/anomalyco/opencode/issues/16960)**  
   *Comments: 5*  
   Session compaction calls LLM with empty system prompt, discarding project instructions. Long-running sessions lose behavioral consistency after compaction.

10. **[#31441 – Folder/nav buttons missing in v1.16](https://github.com/anomalyco/opencode/issues/31441)**  
    *Comments: 2*  
    UI regression: navigation buttons disappeared from top menu in v1.16. High visibility issue for daily users.

## Key PR Progress

1. **[#31434 (CLOSED) – Drain pending events before breaking on idle in JSON format](https://github.com/anomalyco/opencode/pull/31434)**  
   Fixes `opencode run --format json` emitting incomplete JSONL in CI/containerized environments. Idle event races ahead of text events. Closed and merged.

2. **[#31446 (OPEN) – Follow-up: drain pending events in JSON mode](https://github.com/anomalyco/opencode/pull/31446)**  
   Replaces #31434 with a more thorough fix. Tracks active pending parts and delays session-close until all events are flushed.

3. **[#31448 (OPEN) – Fix v2 layout chat panel rounded bottom corners](https://github.com/anomalyco/opencode/pull/31448)**  
   CSS fix: missing `overflow-hidden` on outer container causes squared bottom corners in new v2 layout. User-facing visual polish.

4. **[#31329 (OPEN) – Graceful error handling for PDF/image read failures](https://github.com/anomalyco/opencode/pull/31329)**  
   Prevents session crashes when PDF/image files are corrupted or permission-denied. Closes #21390. Important for users with large codebases containing media files.

5. **[#31442 (OPEN) – Paginate MCP catalogs](https://github.com/anomalyco/opencode/pull/31442)**  
   Follows MCP cursors when listing tools/prompts/resources, caps traversal at 1,000 pages, handles repeated cursors. Essential for large MCP servers.

6. **[#31440 (OPEN) – Retry transient network errors](https://github.com/anomalyco/opencode/pull/31440)**  
   Retries ECONNRESET/ECONNREFUSED/fetch failures instead of surfacing raw error content. Closes four related issues (#31133, #20822, #15350, #21893).

7. **[#31436 (OPEN) – Performance fixes: sameModel tautology, query limits, dedup](https://github.com/anomalyco/opencode/pull/31436)**  
   Fixes four compounding performance issues: tautological `sameModel()` comparison, missing SQL query limits, unbounded agent name lookups, and redundant DB queries.

8. **[#31444 (OPEN) – Skip spinner animation in non-TTY environments](https://github.com/anomalyco/opencode/pull/31444)**  
   `opencode plugin install` in CI/PowerShell emits raw ANSI garbage. Now detects non-TTY and skips spinner.

9. **[#31447 (OPEN) – Ensure config directory exists before writing .gitignore](https://github.com/anomalyco/opencode/pull/31447)**  
   Fixes crash on startup when `OPENCODE_CONFIG_DIR` points to a non-existent directory (e.g., after auto-update wipes install directory).

10. **[#31431 (CLOSED) – Start app without sidecar (POC)](https://github.com/anomalyco/opencode/pull/31431)**  
    Experimental proof-of-concept to open the app without the local sidecar process. Not production-ready but signals architectural exploration.

## Feature Request Trends

- **Session lifecycle management**: `/goal` command (#27167) and persistent goals—users want session-aware workflows beyond stateless slash commands.
- **MCP parity**: Resources in addition to tools (#15535) and file path linking in web UI (#13430, #31406). Developers building MCP servers need full protocol support.
- **Payment flexibility**: Crypto payments for OpenCode Go (#23153) and Chinese VAT invoicing (#30716). Growing international user base demanding local payment options.
- **Thinking mode variants**: MiniMax M3 thinking modes (#31180) and vLLM reasoning interleaved fields (#19988). Users want configurable reasoning visibility per provider.
- **Multi-platform clipboard**: Linux Wayland/X11 primary clipboard for middle-click paste (#6370). Niche but persistent demand from Linux users.

## Developer Pain Points

1. **SQLite migration regressions**: The `session_message.seq` NOT NULL constraint failure (#31204, #31413, #31412) is the single biggest blocker today—multiple closed issues flagged urgent for three different code paths. Crashes agent switching, `opencode run`, and HTTP API sessions.

2. **Bedrock Mantle instability**: Two distinct bugs (#31430, #31349) plague the new Mantle provider for GPT-5.5. Empty responses stop mid-task silently, and SigV4 auth fails against OpenAI-compatible endpoints. Blocks enterprises from adopting.

3. **Undo/rollback asymmetry**: `/undo` not reverting file changes (#5474) is a years-old papercut that erodes trust in AI-assisted editing. Each manual rollback wastes time and increases error risk.

4. **Compaction losing instruction context**: Long sessions that survive compaction lose all AGENTS.md/CLAUDE.md behavioral context (#16960). Counterintuitive for a tool designed for extended agentic sessions.

5. **Tool leakage in Copilot providers**: Raw tool-call markup appearing in assistant output (#31247) with Opus 4.8 degrades conversation quality and can cause cascading API errors. Specific to the Copilot proxy path.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-09

## Today's Highlights
v0.79.0 landed with a polarizing **Project Trust** feature that gates local project inputs behind user consent, immediately sparking a heated 14-comment discussion and a PR to add an opt-out flag. Alongside the release, the community closed **19 PRs** in 24 hours, tackling critical bugs including a high-CPU quadratic session traversal, missing binary assets for session export, and parallel compaction issues on local backends.

## Releases
**v0.79.0** — [Release Notes](https://github.com/earendil-works/pi/releases/tag/v0.79.0)
- **Project Trust**: Pi now prompts before loading project-local settings, resources, instructions, and packages. Decisions are saved; non-interactive modes support `--approve` / `--no-approve` flags.
- *Note: Release notes contain dead links (404s) per issue #5516.*

## Hot Issues (Top 10)

1. **#5514 — [OPEN] Project Trust Feature Feedback** — *markg85*  
   *Comments: 14 | 👍: 4*  
   The newly landed trust gating already annoys users who want to opt out entirely. Author feels the prompt is excessive when they know their own projects.  
   [Link](https://github.com/earendil-works/pi/issues/5514)

2. **#4180 — [CLOSED] Links not clickable anymore** — *Thinkscape*  
   *Comments: 10*  
   After an update that switched pi-codingagent to “alternate term mode”, hyperlinks in the terminal stopped being clickable. Likely a TUI rendering regression.  
   [Link](https://github.com/earendil-works/pi/issues/4180)

3. **#5464 — [CLOSED] Local models: 3-5 minute “Working” status latency** — *DuckTapeKiller*  
   *Comments: 6*  
   Running Pi with local Ollama models introduces multi-minute delays on every message mid-session, making local workflows nearly unusable.  
   [Link](https://github.com/earendil-works/pi/issues/5464)

4. **#5363 — [OPEN] Add amazon-bedrock-mantle provider** — *tasadurian*  
   *Comments: 6 | 👍: 3*  
   Requests a new provider for Bedrock Mantle models that use OpenAI-compatible API (incompatible with existing Converse-based provider). PR #5509 now implements this.  
   [Link](https://github.com/earendil-works/pi/issues/5363)

5. **#5286 — [CLOSED] Missing pricing info for GitHub Copilot models** — *markokocic*  
   *Comments: 6*  
   GitHub Copilot’s new per-token pricing isn’t reflected; Pi still shows `$0.000 (sub)` instead of actual costs.  
   [Link](https://github.com/earendil-works/pi/issues/5286)

6. **#5427 — [OPEN] OpenAI Codex transport issues** — *cperion*  
   *Comments: 3 | 👍: 4*  
   Users experience “Codex SSE response headers timed out after 10000ms” errors mid-conversation, breaking usability with Codex models.  
   [Link](https://github.com/earendil-works/pi/issues/5427)

7. **#5492 — [CLOSED] High CPU in interactive TUI on large sessions** — *somjik-api*  
   *Comments: 3*  
   A session with ~62k tokens caused ~100% CPU due to `Footer.render → getContextUsage → sessionManager.getBranch` being quadratic in session branch count. Fix landed in PR #5493.  
   [Link](https://github.com/earendil-works/pi/issues/5492)

8. **#5511 — [CLOSED] Error: context shift is disabled** — *mpetruc*  
   *Comments: 2*  
   Manual `/compact` fails with “502 status code (no body)” when context reaches ~51% of window. Suggests fragility in compaction pipeline.  
   [Link](https://github.com/earendil-works/pi/issues/5511)

9. **#5536 — [CLOSED] Split-turn compaction sends parallel summarization requests** — *mforce*  
   *Comments: 1*  
   Auto-compaction fails on single-concurrency local backends (e.g., `llama.cpp`) because split-turn mode launches two parallel summarization requests, triggering HTTP 429.  
   [Link](https://github.com/earendil-works/pi/issues/5536)

10. **#5530 — [OPEN] `azure-openai-responses` missing `store: false`** — *Jaxkr*  
    *Comments: 2*  
    Azure OpenAI runs in stateful mode by default, leading to server-side reasoning object drops. A 3-line fix PR (#5524) addresses this.  
    [Link](https://github.com/earendil-works/pi/issues/5530)

## Key PR Progress (Top 10)

1. **#5533 — [CLOSED] fix(coding-agent): add missing template.{css,js} to copy-binary-assets** — *eagafonov*  
   Fixes `pi --export` failing from the dist folder due to missing CSS/JS files.  
   [Link](https://github.com/earendil-works/pi/pull/5533)

2. **#5524 — [CLOSED] fix(ai): send `store: false` on Azure OpenAI Responses requests** — *Jaxkr*  
   Three-line fix preventing Azure OpenAI from using stateful mode, avoiding reasoning object corruption.  
   [Link](https://github.com/earendil-works/pi/pull/5524)

3. **#5521 — [CLOSED] feat(coding-agent): restore files on rewind (checkpoints)** — *sebastianbreguel*  
   Adds file checkpointing so double-Esc rewind also rolls back edited files on disk, not just conversation.  
   [Link](https://github.com/earendil-works/pi/pull/5521)

4. **#5515 — [CLOSED] feat(coding-agent): add alwaysTrust setting to skip project trust gating** — *markg85*  
   Direct response to #5514: adds a flag to completely disable the new trust gating feature.  
   [Link](https://github.com/earendil-works/pi/pull/5515)

5. **#5513 — [CLOSED] Enforce context window mid-turn via shouldStopAfterTurn** — *lukeramsden*  
   Prevents context from exceeding `contextWindow` during long tool loops by compacting mid-turn.  
   [Link](https://github.com/earendil-works/pi/pull/5513)

6. **#5509 — [OPEN] feat: Add Amazon Bedrock Mantle OpenAI Responses provider** — *unexge*  
   New provider supporting GPT 5.5/5.4 models via Bedrock Mantle’s OpenAI-compatible API. Addresses #5363.  
   [Link](https://github.com/earendil-works/pi/pull/5509)

7. **#5503 — [CLOSED] feat(minimax): use adaptive thinking for MiniMax-M3** — *kapelame*  
   Flags MiniMax-M3 as supporting adaptive thinking, matching the format Pi already uses for Claude Opus 4.6+.  
   [Link](https://github.com/earendil-works/pi/pull/5503)

8. **#5499 — [CLOSED] fix(tui): re-query autocomplete picker on cursor movement** — *Roman-Galeev*  
   Fixes stale autocomplete suggestions when cursor moves via `Editor.moveCursor()`.  
   [Link](https://github.com/earendil-works/pi/pull/5499)

9. **#5493 — [CLOSED] Avoid quadratic session branch traversal** — *somjik-api*  
   Direct fix for #5492: eliminates O(n²) behavior in session branch traversal that caused 100% CPU.  
   [Link](https://github.com/earendil-works/pi/pull/5493)

10. **#5488 — [CLOSED] question: word-wrap option labels and descriptions instead of truncating** — *IgorAlexey*  
    Replaces truncation with word-wrapping in TUI, preserving full text and ANSI styling.  
    [Link](https://github.com/earendil-works/pi/pull/5488)

## Feature Request Trends
- **Project Trust flexibility**: While trust gating launched, users immediately demand the ability to completely disable it (`alwaysTrust` setting) or make it configurable per machine.
- **Provider expansion**: Strong interest in new providers: Amazon Bedrock Mantle, Azure Cognitive Services URLs, and Claude OAuth session login (for company subscriptions without API keys).
- **File checkpointing & rewind**: Restoring files on conversation rewind is a clear priority — both a feature request issue and a PR landed today.
- **Auto-compaction robustness**: Multiple issues and PRs focus on making mid-turn context compaction reliable across local backends, parallel requests, and edge cases.

## Developer Pain Points
- **Local model latency**: Single-concurrency local backends (Ollama, llama.cpp) suffer multi-minute delays and 429 errors due to parallel compaction requests.
- **Session export fragility**: Exporting sessions from the dist folder (binary builds) breaks because `template.{css,js}` assets aren’t bundled — a regression that also affects #5240 and #5534.
- **Windows terminal flashing**: A previously fixed regression (#5113, #4699) returned: child process spawns cause terminal popup/flashing because `windowsHide:true` is missing from the central spawn wrapper.
- **Codex transport reliability**: OpenAI Codex SSE connections time out mid-session, forcing conversation restarts — a growing pain point as more users adopt Codex models.
- **CWD tracking broken**: The bash bridge captures directory changes after `cd` but never propagates them to session state, tools, or UI footer — a silent but pervasive UX issue.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-09

## Today's Highlights
The Qwen Code project continues to mature rapidly with significant progress on the **Agent Client Protocol (ACP) transport layer** and critical **memory management fixes**. A major OOM bug (#4815) has been resolved with a three-pronged fix now merged, while the team pushes forward with **ACP WebSocket transport**, **declarative agent definitions**, and **Claude config migration tools**. The community is actively contributing web-shell UX improvements and foundational infrastructure refactoring.

## Releases
*No new releases in the last 24 hours.*

## Hot Issues

1. **[#4815 — Severe OOM with `qwen --resume` and Escape key broken](https://github.com/QwenLM/qwen-code/issues/4815)** (CLOSED, P1)  
   A critical memory leak causing out-of-memory crashes within ~10 minutes of resume, with total loss of Escape key functionality. The fix (#4824) addresses three root causes: compacting API/UI history, running microcompaction on Hook messages, and triggering garbage collection under pressure. High community engagement with 9 comments.

2. **[#4514 — Daemon capability gaps & prioritized backlog](https://github.com/QwenLM/qwen-code/issues/4514)** (OPEN, needs-triage)  
   Tracks remaining gaps in the `qwen serve` HTTP/SSE surface for remote ACP-compatible clients. With 13 comments, this is the most active feature tracking issue, covering authentication, rate limiting, and session management.

3. **[#4821 — Declarative agent definitions via frontmatter](https://github.com/QwenLM/qwen-code/issues/4821)** (OPEN, P2)  
   Proposes Markdown+YAML agent definitions (à la Claude Code's `.claude/agents/`). Would enable non-TypeScript agent configuration and community sharing patterns.

4. **[#4095 — Atomic file write & transaction rollback](https://github.com/QwenLM/qwen-code/issues/4095)** (OPEN)  
   Phase 1 shipped, but DIND/shared-workspace ownership issues emerged. Mitigation PR #4431 adds ownership preservation. Demonstrates deep infrastructure thinking.

5. **[#4801 — Dedicated `web_search` tool](https://github.com/QwenLM/qwen-code/issues/4801)** (CLOSED, in-review)  
   Finally addresses Qwen Code being "the only one of 5 mainstream Code Agent CLIs without a WebSearch tool." Leverages DashScope's built-in `web_search` — a long-standing community ask (#3841).

6. **[#4782 — ACP Streamable HTTP transport tracking](https://github.com/QwenLM/qwen-code/issues/4782)** (OPEN)  
   Qwen Code Daemon now speaks native ACP at `/acp`, enabling Zed, Goose, and JetBrains connections without adapters. 3 comments, massive impact for IDE integration.

7. **[#4864 — CI: enable required status checks on main](https://github.com/QwenLM/qwen-code/issues/4864)** (OPEN, P2)  
   PR #4798 merged with all CI failing (Lint ❌, Tests ❌), introducing a TS syntax error. Root cause: no branch protection. Critical infrastructure improvement.

8. **[#4838 — Hook continuations skip tool-result microcompaction](https://github.com/QwenLM/qwen-code/issues/4838)** (OPEN, P1, welcome-PR)  
   Discovered during #4815 investigation: `/goal` mode's Hook continuations leak tool results because microcompaction only runs on UserQuery/Cron paths.

9. **[#4721 — Port Dynamic Workflows from Claude Code 2.1.160](https://github.com/QwenLM/qwen-code/issues/4721)** (OPEN)  
   A third tier of multi-agent execution — could be a game-changer for complex task decomposition.

10. **[#4675 — Vim mode Esc key leak and mode render lag](https://github.com/QwenLM/qwen-code/issues/4675)** (CLOSED)  
    Three distinct vim-mode bugs: Esc leaking to AppContainer, Enter not sending in NORMAL mode, and mode indicator lag. 3 comments from users working around the issues.

## Key PR Progress

1. **[#4874 — Web-shell mode indicator mouse-selectable](https://github.com/QwenLM/qwen-code/pull/4874)** (OPEN)  
   Converts the approval-mode indicator to a real `<button>`, making the mode picker accessible via mouse in the web-shell UI.

2. **[#4865 — Don't kill failed-spawn sleep inhibitor child](https://github.com/QwenLM/qwen-code/pull/4865)** (CLOSED)  
   Fixes sandbox abort with `Operation cancelled.` on tool use — the keep-system-awake feature was mishandling its helper process teardown.

3. **[#4161 — Add auto-improve command](https://github.com/QwenLM/qwen-code/pull/4161)** (OPEN)  
   New `/auto-improve` slash command for session-scoped improvement loops with source config, tick scheduling, and local state tracking.

4. **[#4653 — Respect configurable agent ignore files](https://github.com/QwenLM/qwen-code/pull/4653)** (OPEN)  
   Adds support for `.agentignore` and `.aiignore` alongside `.qwenignore`, plus a `context.ignoreFiles` config option.

5. **[#4564 — Expose token usage for cost visibility](https://github.com/QwenLM/qwen-code/pull/4564)** (OPEN)  
   Persists daily/monthly token usage with model/auth-type breakdowns and CSV/JSON export via `/stats`.

6. **[#4847 — Acknowledge queued Qwen Code review requests](https://github.com/QwenLM/qwen-code/pull/4847)** (OPEN)  
   Posts immediate PR comment with Actions link when `@qwen-code /review` is triggered, solving the "no feedback" problem from #4846.

7. **[#4871 — Remove GitService, migrate /restore to FileHistoryService](https://github.com/QwenLM/qwen-code/pull/4871)** (OPEN)  
   Unifies `/restore` and `/rewind` under a single `FileHistoryService`, removing the shadow-git-based `GitService` entirely.

8. **[#4773 — ACP WebSocket transport](https://github.com/QwenLM/qwen-code/pull/4773)** (OPEN)  
   Completes ACP WebSocket transport per RFD, coexisting with SSE. Depends on #4827. 110 lines of new transport code.

9. **[#4824 — Prevent OOM by compacting API/UI history](https://github.com/QwenLM/qwen-code/pull/4824)** (CLOSED)  
   Three-targeted fix for #4815: Hook microcompaction, API/UI history compaction, and memory-pressure GC triggering. Critical stability PR.

10. **[#4520 — Truncate model-facing tool output](https://github.com/QwenLM/qwen-code/pull/4520)** (OPEN)  
    Moves output truncation into `CoreToolScheduler` so any tool returning string `llmContent` is bounded before history recording.

## Feature Request Trends

- **ACP/Protocol Expansion**: Multiple PRs (#4773, #4827) and issues (#4782, #4514) pushing toward full ACP parity — WebSocket transport, REST parity, and daemon hardening.
- **Agent Definition Declarative Format**: #4821 proposes YAML-frontmatter agents, following Claude Code's lead. Community signals desire for non-code agent configuration.
- **WebSearch Integration**: #4801 (now closed) and #3841 reflect persistent demand for real web search, not just URL fetching.
- **Multi-Agent & Background Automation**: #4721 (Dynamic Workflows), #4757 (background fork agent), and #4161 (auto-improve) show interest in richer agent orchestration.
- **Observability & Monitoring**: #4564 (token usage), #4868 (memory/CPU sampling), and #2014 (structured error logging) indicate production-deployment needs.

## Developer Pain Points

- **Memory Leaks in Long Sessions**: #4815 (OOM), #4823 (Hook continuations), and #4838 (microcompaction gaps) show that long-running sessions hit memory issues — a top pain point with multiple active fixes.
- **Vim Mode Bugs**: #4675, #4815 Escape key issues — vim keybindings are fragile, with mode leaks and render lag affecting daily workflow.
- **CI Reliability**: #4864 reveals broken CI merging practices; #4846 shows queued review workflows without feedback.
- **Configuration Migration Friction**: #4845 requests `/import-config` for Claude users, highlighting cross-tool migration as a recurring need.
- **File/Path Handling**: #4568 (@ submodule access), #1388 (line numbers in copy), #4095 (atomic write ownership) — file operations have edge cases in complex projects.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-09

## Today's Highlights
CodeWhale v0.8.54 ships under the canonical project name, deprecating the legacy `deepseek-tui` npm package. Community activity is intense: 50 open issues and 30 PRs were updated in the last 24 hours, with heavy Chinese-language discussion around input cache performance, token consumption, and cross-session memory. The v0.8.55 release candidate adds Together AI and experimental OpenAI Codex providers, and a major i18n localization effort is underway with multiple PRs landing.

## Releases
- **v0.8.54** — CodeWhale v0.8.54  
  - **CodeWhale** is now the canonical project name; the legacy npm package `deepseek-tui` is deprecated and receives no further releases.  
  - Installation requires both `cargo install codewhale-cli codewhale-tui --locked`.

## Hot Issues
1. **[#1177 – Input cache hit rate too low](https://github.com/Hmbown/CodeWhale/issues/1177)**  
   *Community attention:* 24 comments. User reports that DeepSeek-Reasonix achieves 95%+ cache hit rates while CodeWhale lags far behind. This is a core efficiency concern affecting latency and cost.

2. **[#743 – Token consumption has greatly increased](https://github.com/Hmbown/CodeWhale/issues/743)**  
   13 comments. A user reports consuming 400 million tokens in half a day. The issue points to overly dense interaction patterns and requests optimization of conversation overhead.

3. **[#1969 – Session and skill migration after rename](https://github.com/Hmbown/CodeWhale/issues/1969)**  
   8 comments. Users are uncertain whether existing sessions and skills survive the rebranding to CodeWhale. The migration path is not documented in the rebranding notes.

4. **[#1579 – Default color scheme is “really ugly”](https://github.com/Hmbown/CodeWhale/issues/1579)**  
   8 comments. A subjective but vocal UI complaint about the default color scheme. Indicates a desire for theming or better defaults.

5. **[#2490 – Cannot compile Unreal Engine projects](https://github.com/Hmbown/CodeWhale/issues/2490)**  
   5 comments. A specific workflow blocker for game developers using Unreal Engine.

6. **[#1620 – Thinking process is extremely slow](https://github.com/Hmbown/CodeWhale/issues/1620)**  
   5 comments. Users report the model’s reasoning step outputs text at a crawl, suggesting streaming or backend latency issues.

7. **[#2492 – No cross-session memory](https://github.com/Hmbown/CodeWhale/issues/2492)**  
   5 comments. A critical UX gap: the assistant forgets context across restarts, and memory writes are not automatically read on startup.

8. **[#2641 – `read_file` on PDF without `pages` parameter hangs](https://github.com/Hmbown/CodeWhale/issues/2641)**  
   3 comments. A reproducible bug where reading a full PDF (no page range) causes a silent hang and `channel closed` error on ESC.

9. **[#2261 – TUI crash leaks input to PowerShell](https://github.com/Hmbown/CodeWhale/issues/2261)**  
   3 comments. On Windows, a crash during TUI dialogue causes keystrokes to be executed as PowerShell commands — a security and usability hazard.

10. **[#2904 – Feature request: persistent agent state and signed compressed KV cache capsules](https://github.com/Hmbown/CodeWhale/issues/2904)**  
    1 comment but a sophisticated proposal. User suggests persistent agent state and server-signed KV cache capsules to reduce cost and latency in long-running coding sessions.

## Key PR Progress
1. **[#2916 – v0.8.55: Together AI provider + experimental OpenAI Codex](https://github.com/Hmbown/CodeWhale/pull/2916)**  
   New release candidate adding Together AI (Qwen 3.7 Max, MiniMax 2.7, NVIDIA Nemotron) and an experimental OpenAI Codex (ChatGPT) provider with consistency fixes.

2. **[#2919 – i18n: localize ConfigEdit labels and defaults](https://github.com/Hmbown/CodeWhale/pull/2919)**  
   11 new localization strings for config edit mode labels, footer, and status messages. Part of a broader i18n push.

3. **[#2918 – i18n: localize ConfigSection and ConfigScope labels](https://github.com/Hmbown/CodeWhale/pull/2918)**  
   11 more localization strings covering all 9 config section headers and 2 scope labels. Supports 7 shipped locales.

4. **[#2902 – v0.8.54: Benchmark Runners, Community Harvests, Whaleflow Foundation](https://github.com/Hmbown/CodeWhale/pull/2902)**  
   Merged: benchmark harness runners (SWE-bench, Terminal-Bench, PinchBench), MiMo benchmark routing, Paulo’s test harnesses, and the foundational Whaleflow orchestration crate.

5. **[#2482 – feat: add WhaleFlow declarative multi-agent workflow orchestration](https://github.com/Hmbown/CodeWhale/pull/2482)**  
   Closed. New `crates/whaleflow` with JSON-driven swarm orchestration, topological scheduling, semaphore concurrency, file-scoped context. A significant architecture addition.

6. **[#2905 – fix(tui): name allow_shell blocker for shell tools](https://github.com/Hmbown/CodeWhale/pull/2905)**  
   Improves diagnostics when shell tools are unavailable due to `allow_shell = false`. Adds regression coverage.

7. **[#2903 – feat: build static linux x64 binaries with musl](https://github.com/Hmbown/CodeWhale/pull/2903)**  
   Eliminates glibc and libdbus dependencies for static Linux builds, improving portability across distributions.

8. **[#2884 – fix: client response handling and desktop tray icon safety (5 bugs)](https://github.com/Hmbown/CodeWhale/pull/2884)**  
   Closed. Fixes HTTP connection pool leaks and Tauri component lifecycle issues in the desktop app variant.

9. **[#2885 – feat(execpolicy): wire ask-only permissions into runtime](https://github.com/Hmbown/CodeWhale/pull/2885)**  
   Closed. Implements ask-only permission rules in the execution policy runtime, enabling granular tool approval workflows.

10. **[#2781 – feat(tui): ghost-text follow-up prompt suggestion](https://github.com/Hmbown/CodeWhale/pull/2781)**  
    Closed. Adds lightweight v4-flash API call to generate follow-up suggestions as dimmed ghost text in the composer, mirroring Claude Code’s UX.

## Feature Request Trends
- **Persistent agent state & memory** — Multiple issues (#2492, #2904) request reliable cross-session memory, with one proposal for KV cache capsules to reduce cost in long sessions.
- **Multi-agent orchestration** — PR #2482 (WhaleFlow) and issues around agent wait timeouts (#1425) show strong interest in declarative multi-agent workflow management.
- **Internationalization** — A coordinated i18n effort is actively landing across PRs (#2919, #2918, #2899, #2901, #2896), reflecting a global user base.
- **Provider diversity** — v0.8.54 benchmarks and v0.8.55’s Together AI / Codex providers indicate demand for multiple model backends and evaluation frameworks.
- **Ghost-text / intelligent suggestions** — PR #2781’s ghost-text feature mirrors a trend toward proactive, non-intrusive UX (Claude Code-style).

## Developer Pain Points
- **High token consumption & cost** — Issues #743 and #1818 report massive token overuse, with one user burning 400M tokens in half a day. This is a top frustration.
- **Poor input cache hit rate** — Issue #1177 highlights cache efficiency far below competing products (sub-50% vs 95%), directly impacting latency and cost.
- **Session instability & memory loss** — Issues #2492, #1425, #2739 show that agent sessions frequently hang, crash, or lose context after restart, making multi-session workflows unreliable.
- **Windows/terminal compatibility** — Issues #2261 (input leaking to PowerShell), #1338 (GUI crash on Enter), and #1556 (ghostty flicker) highlight persistent terminal and platform bugs.
- **Configuration & migration friction** — Issue #1969 reveals uncertainty about session migration after rebranding; issue #2596 and #2893 show provider aliasing and model-picker confusion.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*