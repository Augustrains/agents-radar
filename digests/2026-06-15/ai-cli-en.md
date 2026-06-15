# AI CLI Tools Community Digest 2026-06-15

> Generated: 2026-06-15 02:29 UTC | Tools covered: 9

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

# AI CLI Developer Tools Ecosystem — Cross-Tool Comparison Report
**Date:** 2026-06-15 | **Period:** Last 24 hours

---

## 1. Ecosystem Overview

The AI CLI tools landscape is experiencing a maturation phase where reliability, security, and resource management have overtaken feature velocity as the dominant community concerns. Across all seven tools surveyed, developers are reporting systemic issues with agent lifecycle management—subagent hangs, infinite recursion, zombie processes, and false success reporting—indicating that autonomous agent orchestration remains the hardest unsolved problem. Community activity is bifurcated between mature tools (Claude Code, Codex) where users demand stability and cost transparency, and rapidly iterating newcomers (Pi, CodeWhale, Qwen Code) where breaking changes and platform gaps create friction. A notable cross-cutting theme is the demand for standardized project context files (`.cursorrules`, `AGENTS.md`, `CLAUDE.md` equivalents), suggesting the ecosystem is converging on shared conventions for developer-agent interaction patterns.

---

## 2. Activity Comparison

| Tool | Open Issues (Hot) | Active PRs (Last 24h) | Release Status | Community Engagement Signal |
|------|------------------|----------------------|----------------|---------------------------|
| **Claude Code** | 10 hot issues | 5 key PRs | No release | High: #50246 (92 👍), #53940 (31 comments) |
| **OpenAI Codex** | 10 hot issues | 10 key PRs | No release | Very High: #14593 (607 comments, 268 👍) |
| **Gemini CLI** | 10 hot issues | 10 key PRs (5 merged) | No release | Moderate: 3 P1 bugs active |
| **GitHub Copilot CLI** | 8 issues | 0 PRs | No release | Low: #3558 (7 👍), mostly triage-level |
| **Kimi Code CLI** | 3+ issues | 4 PRs (3 closed) | No release | Low-Moderate: #2123 (rate limiting complaint) |
| **OpenCode** | 10 hot issues | 10 key PRs (3 closed) | **v1.17.7 released** | High: #28846 (77 comments, 79 👍) |
| **Pi (pi-mono)** | 10 hot issues | 10 PRs (6 merged) | No release | High: #5103 (18 comments), #5671 structural debate |
| **CodeWhale** | 10 hot issues | 10 PRs (9 closed) | **v0.8.60 (rebrand)** | Moderate: #2487 (12 comments on freezes) |
| **Qwen Code** | 10 hot issues | 10 PRs (mixed status) | No release (nightly failing) | Moderate: #3203 (135 comments on free tier) |

**Key insight:** Only *two* tools shipped a release today (OpenCode v1.17.7, CodeWhale v0.8.60). Claude Code and Codex—the most mature tools—had zero releases but high community engagement, indicating a community in "demanding mode" rather than "discovering mode."

---

## 3. Shared Feature Directions

The following feature requirements appear across **three or more** tool communities, indicating genuine ecosystem-wide demand:

| Feature | Tools Requesting | Specific Need |
|---------|-----------------|---------------|
| **Project context auto-loading** | Claude Code (CLAUDE.md), Kimi Code (#850: AGENTS.md/.cursorrules), CodeWhale (#2771: LLM-guided init), Qwen Code (#4845: /import-config from Claude) | Standardized conventions for injecting project-level instructions at session start |
| **Message queuing / non-interrupting input** | Claude Code (#50246, 92 👍), Gemini CLI (agent hang workarounds), CodeWhale (#2739: freeze on continue) | Queue prompts for sequential execution without disrupting active tasks |
| **Automatic provider fallback** | CodeWhale (#2574), Pi (#5702: provider rejection), OpenCode (#28846: pricing-driven model switching) | Auto-switch provider on quota/rate-limit/error without manual intervention |
| **Agent working directory control** | Claude Code (#12748, subagent cwd), GitHub Copilot CLI (#956: scripts wrong folder), OpenCode (#30355: subagent directory inheritance) | `cwd` parameter for subagents, especially for monorepo/git-worktree workflows |
| **Subagent lifecycle governance** | Claude Code (#68430: infinite recursion), Gemini CLI (#21409, #22323: hangs & false success), CodeWhale (#1806: 120s timeout), Qwen Code (#5083: zombie processes) | Timeouts, kill switches, checkpoint/resume, escape-propagation to subagents |
| **Context/token budget controls** | Claude Code (#65585: auto-compact broken for 3rd party), Codex (#10823: compact fails), Qwen Code (#5101: unbounded tool results), Pi (#5654: excludeFromContext) | User-controllable context management, tool result budgeting, per-model compaction |
| **MCP protocol completeness** | OpenCode (#28567: full MCP client), Pi (#5687: MCP server hangs CLI), CodeWhale (#2475: Burp MCP breaks tasks), Qwen Code (#5083: MCP shell zombie) | Streaming, notifications, proper error handling, tool result schema compliance |
| **Cross-platform parity (Windows/Linux)** | Claude Code (pty exhaustion macOS), Codex (#11023: Linux desktop, 568 👍), Gemini CLI (#21983: Wayland browser), CodeWhale (#1812: Windows freeze), Qwen Code (#5055: VSIX false trojan) | Native Linux desktop apps, Windows TUI stability, Wayland support, glibc compatibility |
| **Billing/rate-limit transparency** | Claude Code (#32544: false rate limits), Codex (#14593: token burn, 268 👍), Kimi Code (#2123: misleading quotas), OpenCode (#28846: DeepSeek price cut pass-through), Qwen Code (#3203: free tier reduction) | Clear consumption reporting, accurate quota enforcement, pricing pass-through |

**Emerging pattern:** The community is converging on a *three-layer configuration model*—global, project, and session-level—with standardized file names (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`, `.pi`, `.qwenignore`). This is the closest the ecosystem has come to an interop standard.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | CodeWhale | Qwen Code |
|-----------|------------|--------------|------------|-------------|-----------|----------|----|-----------|-----------|
| **Primary user base** | Power devs, heavy automation | Enterprise web/desktop | GCP-native devs | GitHub ecosystem | Asian market, cost-sensitive | Plugin devs, MCP users | Extension authors, tinkerers | Cost-conscious, multi-provider | Open-source, Alibaba cloud |
| **Architecture** | Monolithic agent | Desktop+CLI+plugin | CLI+ subagents | CLI+ GitHub API | Plugin-based | Plugin+SDK | Extension-based | Agent orchestration | Daemon+web CLI |
| **Key strength** | Cowork, subagent orchestration | Rate-limit reset credits | AST-aware code tools | GitHub integration, BYOK | Project context auto-loading | MCP client, terminal stability | Extension API, provider flexibility | Provider fallback, YOLO mode | Dynamic workflows, safe mode |
| **Key weakness** | Subagent recursion, silent truncation | Token burn, Windows stability | Agent hangs, shell brittleness | Small community, few PRs | Severe rate limiting, Windows gaps | TUI debt, edit tool fragility | Escape-key broken, local LLM gaps | TUI freezes, glibc lockout | CI failures, free tier controversy |
| **Community maturity** | **Mature** (high expectations, vocal) | **Mature** (largest base, most comments) | **Growth** (3 P1 bugs active) | **Early** (8 issues, 0 PRs) | **Early** (small but engaged) | **Growth** (active releases) | **Growth** (fast PR cycle, structural debates) | **Early** (rebranding friction) | **Growth** (high issue volume, CI instability) |
| **Innovation signal** | Session management regression | Async hooks, MITM CA | Memory system, evaluation infra | Custom provider discovery | Shell configuration for Windows | Edit pipeline hardening | Prompt guideline API, tool profiling | WhaleFlow orchestration, voice commands | Safe-mode, import-config migration |

**Distinctive technical approaches:**

- **Pi** is architecturally unique with its extension-first design and the `pi sendMessage()` API, positioning it as a platform for building AI tools rather than a standalone CLI. The Shrinkwrap double-copy issue (#5653) is a direct consequence of this modular ambition.
- **OpenCode** is the only tool shipping a `--discoverable` serve mode for multi-window/server workflows (#27805), indicating a vision of daemon-driven, multi-session usage.
- **CodeWhale** is the only tool explicitly building a *fleet* orchestration layer (WhaleFlow), with heterogeneous-model workers and shared task ledgers—a differentiator from the single-agent-plus-subagent pattern of others.
- **Gemini CLI** is investing in AST-aware code understanding (#22745-22747), a unique approach to reducing token noise that no other tool is pursuing at the same depth.

---

## 5. Community Momentum & Maturity

### High Activity / High Maturity
- **Claude Code**: Most mature, but community sentiment is shifting from enthusiasm to frustration. The 92-upvote message queue request (#50246) and data-loss regression (#41458) suggest users feel the tool has plateaued. Key metric: 10 hot issues, all with substantive technical analysis.
- **OpenAI Codex**: Largest community (607 comments on #14593), but the dominant conversation is *cost anxiety*, not features. The rate-limit reset credit PR stack (#28143, #28154) is a direct response. Codex is iterating on infrastructure (async hooks, MCP timeouts) rather than new capabilities.

### High Activity / Growth Phase
- **Pi**: Highest PR velocity (6 merged today). The structural debate on `.pi` directory design (#5671) is a sign of a community that cares about architecture. The extension API is becoming a differentiator. Risk: two Escape-key bugs (#5736, #5685) suggest core UX fragility.
- **OpenCode**: v1.17.7 shipped today, and the MCP parity push (#28567) aligns with ecosystem trends. The edit tool hardening cluster (#32348, #30907) shows attention to quality. The DeepSeek pricing issue (#28846, 79 👍) indicates a price-sensitive, pragmatic user base.

### Moderate Activity / Early Growth
- **Gemini CLI**: Three P1 bugs are blocking, but the evaluation infrastructure (#24353) and memory system (#26516 epic) suggest a team investing in foundations. The 53-dependency bump PR is a signal of maintenance health.
- **Qwen Code**: High issue volume, but the nightly CI failures (#5117, #5068) and Trojan false-positive (#5055) create a perception of instability. The `--safe-mode` (#4943) and `/import-config` (#4845) features show empathy for users struggling with complexity.
- **CodeWhale**: Rebranding has created migration friction, but the v0.8.61 draft PR (#3225) targeting freezes and orchestration is ambitious. The voice command PR (#3051) suggests creative differentiation.

### Low Activity / Nascent
- **GitHub Copilot CLI**: Eight issues, zero PRs, lowest engagement. The duplicate item error (#3558, 7 👍) is the highest-voted issue, but the community is too small to create pressure. The BYOK model discovery request (#3795) shows potential, but the project feels under-resourced.
- **Kimi Code CLI**: Few issues, but the rate limiting complaint (#2123) is a retention risk. The Windows shell config closure (#839) and paste support (#2018) show platform catch-up. Smallest community of the seven.

---

## 6. Trend Signals

The following industry trends emerge from cross-tool community feedback, with reference value for developers deciding where to invest:

### 1. The "Agent Reliability Wall"
Every tool except Copilot CLI has active issues about subagents hanging, lying about completion, or entering infinite loops. **This is the defining technical challenge of Q3 2026.** Tools that solve checkpoint-resume, timeout propagation, and truthful status reporting will win loyalty. The field is converging on a model where the primary agent is a *supervisor* of limited-life subagents with explicit budgets (turns, tokens, time).

### 2. Cost Transparency Becomes a Feature
Token consumption anxiety (#14593, 268 👍 on Codex) and pricing pass-through demands (#28846, 79 👍 on OpenCode) signal that the "tokens are infinite" era is over. Tools exposing per-task cost breakdowns (Qwen Code #5118), rate-limit reset credits (Codex #28143), and provider-specific pricing (Pi #5738) will gain trust. **Billing UX is the new API UX.**

### 3. Project-Level Configuration Standardization
The convergence on `CLAUDE.md`, `AGENTS.md`, `.cursorrules`, `.pi`, and `.qwenignore` suggests an emerging informal standard: a project file that the AI reads at session start to understand conventions, safety rules, and environment. Cross-tool migration tools like Qwen Code's `/import-config` (#4845) will become essential. **This is the `Dockerfile` of AI CLI tools.**

### 4. Platform Fragmentation Is the Next Battleground
Windows users face TUI freezes (CodeWhale #1812, Claude Code pty exhaustion), broken paste (OpenCode #13984), and false trojan flags (Qwen Code #5055). Linux users need glibc compatibility (CodeWhale #1067) and Wayland support (Gemini CLI #21983). The tool with the best cross-platform investing will capture the enterprise market. Currently, none have solved this.

### 5. MCP Protocol Maturity Is Becoming a Gatekeeper
OpenCode (#28567), Pi (#5687), CodeWhale (#2475), and Qwen Code (#5083) all have open issues tied to MCP client/server correctness. As the MCP ecosystem grows (Hugging Face MCP, Burp, custom providers), tools that implement the full spec correctly (streaming, notifications, error handling) will have a competitive advantage. **MCP compliance is table stakes by Q4 2026.**

### 6. The Free Tier Tension
Qwen Code's proposed free tier cut from 1,000 to 100 req/day (#3203, 135 comments) and Kimi Code's misleading quotas (#2123) highlight a universal tension: tools need revenue, but developers rely on free access for evaluation and CI. The community reaction is strongly negative. **Tools that communicate pricing honestly will build more trust than those with generous but opaque quotas.**

---

## Summary Recommendation for Technical Decision-Makers

| If you prioritize... | Strongest candidate | Why |
|---------------------|---------------------|-----|
| **Highest maturity & community support** | Claude Code (but monitor cost regressions) | Largest community, most documentation, but approaching reliability plateau |
| **Cross-platform stability** | None currently excel | OpenCode has best Linux/macOS story; Windows is problematic everywhere |
| **Extension/plugin flexibility** | Pi | Architecture is designed for extension authors; fast PR cycle, growing API surface |
| **Cost control & provider flexibility** | OpenCode or CodeWhale | Both respond to pricing sentiment; CodeWhale has fallback chains planned |
| **Enterprise compliance** | Gemini CLI (GCP-native) or Codex (rate-limit credits) | Gemini has evaluation infrastructure; Codex has enterprise policy controls |
| **Open-source & rapid iteration** | Qwen Code (but watch CI stability) | Most open development model; high issue volume suggests active maintenance |

**Cross-tool consensus weakest area:** *Reliable long-running agent sessions.* No tool has solved multi-hour autonomous workflows with checkpoint/resume, truthful error reporting, and predictable cost. This remains the largest market opportunity.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot**: 2026-06-15 | **Source**: github.com/anthropics/skills

---

## 1. Top Skills Ranking

The most-discussed Skill PRs by overall community engagement (comments + cross-referencing activity):

### #514 — `document-typography` *(Open)*
**Functionality**: Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents — three pervasive typographic defects that affect every document Claude produces.  
**Discussion highlights**: Resonates strongly because it addresses a universal pain point; commenters noted the skill could be extended for multi-language typography rules.  
**Status**: Open since March 2026 | [View PR](https://github.com/anthropics/skills/pull/514)

### #486 — `odt` — OpenDocument skill *(Open)*
**Functionality**: Create, fill, read, and convert .odt/.ods files using LibreOffice-compatible formats, including template filling and ODT-to-HTML parsing.  
**Discussion highlights**: Community interest reflects demand for open-source document formats as an alternative to proprietary DOCX workflows.  
**Status**: Open since March 2026 | [View PR](https://github.com/anthropics/skills/pull/486)

### #210 — Improve `frontend-design` clarity *(Open)*
**Functionality**: Revises the existing frontend-design skill for actionable, single-conversation instructions — ensuring Claude can consistently follow guidance on layout, spacing, and responsive design.  
**Discussion highlights**: Debate around whether "design" skills should instruct Claude on aesthetic principles vs. structural HTML/CSS decisions.  
**Status**: Open since January 2026 | [View PR](https://github.com/anthropics/skills/pull/210)

### #83 — `skill-quality-analyzer` + `skill-security-analyzer` *(Open)*
**Functionality**: Two meta-skills: one evaluates skill quality across five dimensions (structure, documentation, performance); the other audits skills for security vulnerabilities and trust-boundary risks.  
**Discussion highlights**: Meta-skills are a novel category; reviewers questioned whether quality analysis should be a separate skill or built into the CLI tooling.  
**Status**: Open since November 2025 | [View PR](https://github.com/anthropics/skills/pull/83)

### #1140 — `agent-creator` meta-skill *(Open)*
**Functionality**: Generates task-specific agent sets (composable Claude Code agents), fixes multi-tool evaluation parallelism, and adds Windows APPDATA path support.  
**Discussion highlights**: Addresses issue #1120; tight integration with the skill-creator evaluation pipeline.  
**Status**: Open since May 2026 | [View PR](https://github.com/anthropics/skills/pull/1140)

### #181 — `SAP-RPT-1-OSS` predictor *(Open)*
**Functionality**: Skill for using SAP's open-source tabular foundation model (Apache 2.0) for predictive analytics on business data.  
**Discussion highlights**: Enterprise analytics use case; community interest in integrating external ML models as Skills rather than standalone MCP tools.  
**Status**: Open since December 2025 | [View PR](https://github.com/anthropics/skills/pull/181)

### #444 — `AURELION` skill suite *(Open)*
**Functionality**: Four interrelated skills — kernel (structured thinking templates), advisor (decision support), agent (autonomous workflow), memory (persistent context) — forming a cognitive framework for knowledge management.  
**Discussion highlights**: Largest single PR in scope; discussion focused on whether the suite should be one skill or four independently installable ones.  
**Status**: Open since February 2026 | [View PR](https://github.com/anthropics/skills/pull/444)

---

## 2. Community Demand Trends

The top Issues reveal five concentrated demand vectors:

| Demand Area | Key Issue(s) | Signal |
|---|---|---|
| **Org-wide skill sharing & distribution** | #228 (14 comments, 7 👍) | Most-commented issue: users want direct sharing links and shared skill libraries instead of manual .skill file transfer |
| **Evaluation pipeline reliability** | #556 (12 comments, 7 👍), #1169, #1061 | 0% recall bug in `run_eval.py` is the community's most urgent technical blocker; multiple independent reproductions |
| **Duplicate/conflicting skill plugins** | #189 (6 comments, 8 👍) | High upvote count: `document-skills` and `example-skills` install identical content, wasting context window space |
| **Security & trust boundaries** | #492 (7 comments, 2 👍) | Community-made skills under `anthropic/` namespace impersonate official skills — a trust boundary vulnerability |
| **Windows compatibility** | #1061, plus PRs #1099, #1050, #1298 | Sustained pressure: subprocess, encoding, and pipe-handling failures block Windows users from the entire skill-creator toolchain |

**Most-anticipated new Skill directions** (from Issues and feature requests):
- **Agent governance & safety patterns** (Issue #412) — policy enforcement, threat detection, audit trails
- **Multi-file skill bundling** (Issue #1220) — preloading reference files alongside SKILL.md
- **MCP integration** (Issue #16) — exposing Skills as MCP tools for cross-platform use

---

## 3. High-Potential Pending Skills

These PRs have active discussion, are not yet merged, and address clear community pain points:

| PR | Skill | Why It Could Land Soon |
|---|---|---|
| [#538](https://github.com/anthropics/skills/pull/538) | **PDF case-sensitive fix** | Simple 8-line fix for file reference mismatches that break on case-sensitive filesystems; low risk, high impact |
| [#539](https://github.com/anthropics/skills/pull/539) | **Unquoted YAML detection** | Prevents silent parsing failures in description fields; partial overlap with #361 but both active |
| [#541](https://github.com/anthropics/skills/pull/541) | **DOCX w:id collision fix** | Prevents document corruption when tracked changes conflict with existing bookmarks; targeted fix |
| [#509](https://github.com/anthropics/skills/pull/509) | **CONTRIBUTING.md** | Addresses a community health gap (25% GitHub health score); low-effort documentation PR |
| [#1298](https://github.com/anthropics/skills/pull/1298) | **run_eval.py 0% recall fix** | Most comprehensive fix for the #556 bug family; merges multiple earlier partial fixes into one complete solution |
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | Full-stack testing skill (unit, React, integration, e2e); fills an obvious gap in the collection |
| [#147](https://github.com/anthropics/skills/pull/147) | **codebase-inventory-audit** | 10-step orphan code/documentation audit workflow; directly useful for repo maintenance |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable, portable evaluation infrastructure** — the `run_eval.py` 0% recall bug (#556) and its associated Windows/platform compatibility issues span at least 6 PRs and 4 separate Issues, consuming more community attention than any single new Skill proposal, and signaling that the meta-tooling layer (skill validation, evaluation, installation) is the critical bottleneck to Skill ecosystem growth.

---

# Claude Code Community Digest — 2026-06-15

## Today's Highlights

A critical cluster of bugs around **subagent spawning** and **recursive token burn** emerged this week (`#68430`), with reports of agents spawning 50+ levels deep and ignoring `FORK_SUBAGENT=0`. Meanwhile, the long-running **message queue** feature request (`#50246`) continues to attract strong community support (92 👍), and multiple reports of **pty exhaustion on macOS** (`#65995`, `#66434`) suggest a systemic resource leak in the Desktop app that can render terminals unusable.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#53940 — Cowork Edit/Write tools silently truncate files](https://github.com/anthropics/claude-code/issues/53940)**  
   *31 comments, 12 👍*  
   A byte-conservation buffer cap silently truncates files during Cowork operations. High engagement suggests this is a daily pain point for anyone using Cowork on Windows.

2. **[#50246 — Message queue mode](https://github.com/anthropics/claude-code/issues/50246)**  
   *28 comments, 92 👍*  
   The most-upvoted open feature request. Users want to queue messages instead of interrupting active tasks — a workflow essential for complex, multi-step sessions.

3. **[#41458 — cleanupPeriodDays: 99999 ignored](https://github.com/anthropics/claude-code/issues/41458)**  
   *16 comments, 1 👍*  
   490 sessions silently deleted despite explicit retention config. A data-loss regression that undermines trust in session management.

4. **[#32544 — Extra usage charged despite available plan capacity](https://github.com/anthropics/claude-code/issues/32544)**  
   *15 comments, 14 👍*  
   Billing and false rate-limit errors on Linux. Community concern about cost transparency and API reliability.

5. **[#51143 — Claude Desktop blank/white screen on Windows](https://github.com/anthropics/claude-code/issues/51143)**  
   *13 comments, 12 👍*  
   Cowork unusable on Windows due to persistent rendering failure. Multiple reinstalls have no effect.

6. **[#63870 — Bash tool calls emitted as raw text](https://github.com/anthropics/claude-code/issues/63870)**  
   *11 comments, 13 👍*  
   `<invoke>` XML printed verbatim instead of executed. User provided JSONL evidence of 23 malformed calls in one session.

7. **[#68430 — Subagent infinite recursion and token burn](https://github.com/anthropics/claude-code/issues/68430)**  
   *7 comments*  
   CRITICAL: Subagents recursively spawn 50+ levels deep, ignoring safeguards. Catastrophic token burn scenario flagged as urgent.

8. **[#66020 — macOS kernel zone leak from Claude Code CLI](https://github.com/anthropics/claude-code/issues/66020)**  
   *7 comments*  
   `data.kalloc.1024` zone leak causes panics at ~20GB. Leak rate scales 21→1027/sec with agent load — a performance fire.

9. **[#65585 — Auto-compact stopped working for third-party providers](https://github.com/anthropics/claude-code/issues/65585)**  
   *4 comments, 3 👍*  
   Regression since v2.1.161. Third-party API users lose context management, increasing costs and degrading quality.

10. **[#68461 — iTerm2 screen corruption in long sessions](https://github.com/anthropics/claude-code/issues/68461)**  
    *3 comments*  
    Renderer emits cursor-up sequences larger than viewport. Regression present since 2.1.162, still unfixed in 2.1.177.

## Key PR Progress

1. **[#68423 — Don't auto-close assigned issues in sweep](https://github.com/anthropics/claude-code/pull/68423)**  
   Fixes `sweep.ts` to skip assigned issues during stale/close automation. Prevents active issues from being incorrectly closed.

2. **[#67699 — Fix Claude autonomously running background scripts](https://github.com/anthropics/claude-code/pull/67699)**  
   `/bounty $29` — Addresses unauthorized external API calls by Claude during background operations.

3. **[#67409 — Fix account downgraded due to billing error](https://github.com/anthropics/claude-code/pull/67409)**  
   `/bounty $200` — Resolves a billing error that incorrectly downgraded user accounts.

4. **[#67722 — Fix autonomous external script execution (CLOSED)](https://github.com/anthropics/claude-code/pull/67722)**  
   Closed PR addressing the same vulnerability as #67699. Duplicate efforts suggest this is a high-priority security concern.

5. **[#1 — Create SECURITY.md](https://github.com/anthropics/claude-code/pull/1)**  
   Still receiving updates after 16 months — possibly a recurring merge target or CI trigger.

## Feature Request Trends

**Three dominant themes** emerge from open feature requests:

- **Message Queuing & Non-Interrupting Input** (`#50246`, `#64204`): Users consistently request the ability to queue prompts for sequential execution without interrupting active tasks. This is the #1 most-upvoted feature across all open issues.

- **Subagent Working Directory Control** (`#12748`, 23 👍): Developers working with Git worktrees, monorepos, or polyglot projects need the `Task` tool to accept a `cwd` parameter so subagents operate in the correct directory.

- **Window Capture / Appshots** (`#68498`): Users want macOS accessibility-based full-window text capture (including scrolled content), inspired by OpenAI Codex's Appshots feature. High-priority request for improved context gathering.

## Developer Pain Points

1. **Silent data loss**: Files truncated by Cowork tools (`#53940`), sessions deleted despite retention settings (`#41458`), and output files written as 0 bytes (`#68496`) — all without user-facing warnings.

2. **Resource exhaustion under load**: macOS kernel zone leaks (`#66020`), pty exhaustion (`#65995`, `#66434`), and infinite subagent spawning (`#68430`) compound into system-level failures when using Claude Code intensively.

3. **Billing and rate-limit confusion**: Users charged despite available plan capacity (`#32544`), HTTP 529 errors mislabeled as rate limits (`#68502`), and account downgrades from billing errors (`#67409`) — eroding trust in the service's cost management.

4. **Model reliability regressions**: Bash tool calls rendered as raw text (`#63870`), malformed tool calls in extended sessions (`#68472`), and failure to verify artifacts against top-level goals (`#66130`) signal degradation in long-running agent interactions.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-15

## Today's Highlights
No new releases shipped in the last 24 hours, but the community remains vocal about token consumption and platform support. The top issue by far—burning tokens very fast (#14593)—continues to accumulate comments (607 total, +268 upvotes) without a fix, while feature demand for a native Linux desktop app (#11023) stays strong at 568 upvotes. On the PR side, OpenAI engineers are landing important infrastructure work around rate-limit reset credits, async hooks, and MCP tool timeouts.

## Releases
*(No new releases in the last 24 hours)*

## Hot Issues (Top 10 by community impact)

1. **[#14593 – Burning tokens very fast](https://github.com/openai/codex/issues/14593)**  
   *Open for 3+ months, 607 comments, 268 👍*  
   A Business-tier user on VS Code reports excessively fast token consumption. This is the most-commented open issue in the repo and a top community frustration. No official resolution has been posted.

2. **[#11023 – Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**  
   *568 👍, 107 comments*  
   Request for a native Linux desktop app. Users cite macOS power consumption issues as a reason to move to Linux. High demand but no official acknowledgment of a roadmap.

3. **[#21527 – Codex is really too slow](https://github.com/openai/codex/issues/21527)**  
   *29 comments, 17 👍*  
   Performance complaints span both VS Code plugin and the desktop app. Response times are the core issue.

4. **[#10823 – Unable to compact context in long sessions](https://github.com/openai/codex/issues/10823)**  
   *29 comments*  
   Long-running sessions hit "high demand" errors when attempting context compaction. Blocks productivity for power users with persistent workspaces.

5. **[#27817 / #28015 – False positive cybersecurity flags](https://github.com/openai/codex/issues/27817)**  
   *16 comments each*  
   Two separate reports (app and CLI) flagging normal finance/tax work and routine DevOps as cybersecurity risks. Safety system is over-aggressive for non-security tasks.

6. **[#25500 – "No chats" in Desktop Projects sidebar](https://github.com/openai/codex/issues/25500)**  
   *18 comments*  
   UI bug where older non-archived conversations don't appear in the sidebar on Windows.

7. **[#27367 / #25807 – Windows app opens then exits immediately](https://github.com/openai/codex/issues/27367)**  
   *9 + 8 comments*  
   Two reports of the Codex desktop app crashing on launch after recent updates (Windows 10/11). CLI still works, pointing to an Electron packaging issue.

8. **[#28074 – WSL integration broken on fresh installs](https://github.com/openai/codex/issues/28074)**  
   *6 comments, 3 👍*  
   WSL-mode connectivity fails even on completely fresh installs. Critical for Windows developers relying on Linux toolchains.

9. **[#9252 – Remove 2 leading spaces from cmd suggestion](https://github.com/openai/codex/issues/9252)**  
   *14 comments, 54 👍*  
   Aesthetic but highly-upvoted CLI TUI request. Persistent formatting issue in command suggestions.

10. **[#28212 – Request for safe workaround for WSL-mode startup failure](https://github.com/openai/codex/issues/28212)**  
    *4 comments (CLOSED)*  
    User asked for recovery steps after WSL-mode crash. Closed—likely resolved or workaround provided.

## Key PR Progress (Top 10 by technical significance)

1. **[#28143 – Expose rate-limit reset credits](https://github.com/openai/codex/pull/28143)**  
   Backend API to read/redeem personal rate-limit reset credits. Enables the `/usage` TUI flow (#27925). Directly addresses token consumption frustration.

2. **[#28154 – Rate-limit reset redemption in /usage](https://github.com/openai/codex/pull/28154)**  
   Companion to #28143—adds CLI-side redemption UI. Lets users view and spend earned resets without leaving the terminal.

3. **[#28235 – Add request user input auto-resolution timer](https://github.com/openai/codex/pull/28235)**  
   TUI auto-responds to `request_user_input` prompts after a 60s hidden + 60s visible countdown. Improves headless/automated workflows.

4. **[#27452 / #27771 / #27772 – Async hooks stack](https://github.com/openai/codex/pull/27452)**  
   Three-PR stack: bounded runtime → async hook execution → visibility of hook mode. Enables hooks to run independently of their launching operation, with UI inspection.

5. **[#28234 – Increase default MCP tool timeout to 300s](https://github.com/openai/codex/pull/28234)**  
   Raises MCP timeout from 120s to 300s. Addresses timeouts for long-running external tool calls without per-tool configuration.

6. **[#25888 – Prepare managed child MITM CA env](https://github.com/openai/codex/pull/25888)**  
   Multi-PR stack for preserving platform CA roots and materializing child MITM CA bundles. Security infrastructure for sandbox/managed environments.

7. **[#28008 / #28009 – External agent import accounting & telemetry](https://github.com/openai/codex/pull/28008)**  
   Import progress notifications and fine-grained telemetry for external agent imports. Helps diagnose partial failures in async imports.

8. **[#27963 – Reference writable roots from environment context](https://github.com/openai/codex/pull/27963)**  
   Deduplicates writable-root paths by referencing the structured `<filesystem>` context instead of repeating in permission messages. Cleaner developer experience.

9. **[#28232 – Add workspace headline statusline item](https://github.com/openai/codex/pull/28232)**  
   New TUI statusline item showing workspace messages for Enterprise users. Fetches every 10 seconds.

10. **[#27666 – Add managed field support to requirements.toml](https://github.com/openai/codex/pull/27666)**  
    Extends `requirements.toml` to enforce managed auth, storage, telemetry, shell, and Windows settings. Infrastructure for enterprise policy control.

## Feature Request Trends

- **Linux desktop app** (#11023, 568 👍) remains the single most-requested feature. Community cites macOS power issues and preference for Linux dev environments.
- **Spellcheck toggle** (#25431, 14 👍) – Windows desktop users want an on/off switch in settings.
- **Persistent terminal title** (#21958, 3 👍) – Users managing multiple AI CLIs want clear window identification.
- **MCP & custom model improvements** – Requests for better local OAuth keyring persistence (#28201) and localhost connectivity (#21773) indicate growing use of custom/local models via MCP.

## Developer Pain Points

1. **Token consumption anxiety** – #14593 (607 comments) is the dominant concern. Users on paid plans feel tokens are burning too fast without transparency.
2. **Windows stability** – Multiple reports of app crashing on launch (#27367, #25807), WSL integration broken (#28074), and paste failures (#28226). Windows users face a fractured experience.
3. **Over-aggressive safety checks** – #27817, #28015, #28230: routine finance, DevOps, and tax work flagged as cybersecurity risks. Safety system needs better signal/noise.
4. **Performance regression** – #21527 ("codex is really too slow") and #20840 (high GPU usage, battery drain) suggest optimization effort has lagged behind feature work.
5. **Context management in long sessions** – #10823: inability to compact context forces users to restart sessions, losing history and continuity. Critical for power users running multi-hour sessions.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-15

## Today's Highlights
A major dependency refresh dropped today with 53 updated packages (PR #27925), signaling a significant maintenance push. Meanwhile, three P1 bugs remain active on the agent hang and evaluation fronts, and the community continues to surface memory system reliability issues through SandyTao520's focused cleanup tracker (#26516). No new releases landed in the last 24 hours.

## Releases
No new releases in the last 24 hours. The last recorded action is a flurry of dependency bumps merged today (see Key PR Progress).

## Hot Issues
1. **[#24353 — Robust component level evaluations (P1, 7 comments)**](https://github.com/google-gemini/gemini-cli/issues/24353)
   Follow-up on the behavioral evals system; 76 tests now exist across 6 Gemini models. High-priority EPIC for eval infrastructure maturity.

2. **[#21409 — Generalist agent hangs (P1, 7 comments, 8 👍)**](https://github.com/google-gemini/gemini-cli/issues/21409)
   CLI hangs indefinitely when deferring to the generalist agent. Workaround exists (disable sub-agents), but this is blocking simple tasks like folder creation. Strong community upvote signal.

3. **[#22745 — AST-aware file reads, search, and mapping (P2, 7 comments, 1 👍)**](https://github.com/google-gemini/gemini-cli/issues/22745)
   Long-running investigation into whether AST-aware tools improve code understanding. Could reduce token noise and hallucinations on method boundary detection.

4. **[#22323 — Subagent recovery after MAX_TURNS falsely reports success (P1, 6 comments, 2 👍)**](https://github.com/google-gemini/gemini-cli/issues/22323)
   `codebase_investigator` subagent lies about goal completion after hitting turn limits. Critical reliability bug that undermines trust in agent reporting.

5. **[#25166 — Shell hang after command completion (P1, 4 comments, 3 👍)**](https://github.com/google-gemini/gemini-cli/issues/25166)
   CLI shows "Waiting input" after simple shell commands have finished. Intermittent but highly disruptive for script execution workflows.

6. **[#26525 — Add deterministic redaction and reduce Auto Memory logging (P2, 5 comments)](https://github.com/google-gemini/gemini-cli/issues/26525)**
   Auto Memory sends transcript content to model context before redacting secrets. Security concern flagged for enterprise users.

7. **[#26522 — Stop Auto Memory retrying low-signal sessions indefinitely (P2, 5 comments)](https://github.com/google-gemini/gemini-cli/issues/26522)**
   Sessions that the extraction agent skips remain unprocessed forever, causing infinite re-processing loops. Inefficiency at scale.

8. **[#22672 — Agent should stop/discourage destructive behavior (P2, 3 comments, 1 👍)](https://github.com/google-gemini/gemini-cli/issues/22672)**
   Model occasionally uses `git reset --force` or destructive DB commands when safer alternatives exist. Governance concern for production environments.

9. **[#21983 — Browser subagent fails on Wayland (P1, 4 comments, 1 👍)](https://github.com/google-gemini/gemini-cli/issues/21983)**
   Browser agent crashes on Linux/Wayland with a "GOAL" termination but no usable output. Linux desktop users affected.

10. **[#24246 — 400 error with >128 tools (P2, 3 comments)](https://github.com/google-gemini/gemini-cli/issues/24246)**
    Agent hits API 400 error when too many tools are enabled. Needs smarter tool scoping — relevant for MCP-heavy setups.

## Key PR Progress
1. **[#27925 — chore(deps): bump the npm-dependencies group with 53 updates (CLOSED, merged)](https://github.com/google-gemini/gemini-cli/pull/27925)**
   Massive dependency refresh spanning `@agentclientprotocol/sdk`, `octokit`, `eslint`, and many more. Clean merge today.

2. **[#27929 — chore(deps): bump @google/genai from 1.30.0 to 2.8.0 (CLOSED, merged)](https://github.com/google-gemini/gemini-cli/pull/27929)**
   Major version bump to the core GenAI SDK. Likely brings new model capabilities and API changes.

3. **[#27931 — chore(deps): bump puppeteer-core from 24.39.0 to 25.1.0 (CLOSED, merged)](https://github.com/google-gemini/gemini-cli/pull/27931)**
   Puppeteer major version bump — critical for browser subagent stability and Wayland support.

4. **[#27730 — fix: keep array tool results out of structuredContent (OPEN, P1)](https://github.com/google-gemini/gemini-cli/pull/27730)**
   Fixes MCP compliance issue where JSON array tool results were incorrectly copied into structured content. Hotfix for calendar-style payloads.

5. **[#27729 — Fix telemetry metric truncation to 1024 chars (OPEN, P2)](https://github.com/google-gemini/gemini-cli/pull/27729)**
   Prevents Node.js stack traces flooding terminal when GCP metric export fails on long attribute values. Enterprise telemetry fix.

6. **[#27718 — fix(core): keep auto visible without preview access (OPEN, P2)](https://github.com/google-gemini/gemini-cli/pull/27718)**
   Ensures the `auto` model alias remains visible in `/model` for users without preview access. UX fix for model selection.

7. **[#23030 — feat(cli): implement non-invasive UX Journey testing framework (CLOSED, merged)](https://github.com/google-gemini/gemini-cli/pull/23030)**
   Introduces a "white box" terminal UI testing framework without manual instrumentation. Long-term quality enabler.

8. **[#22456 — feat(ui): add new interactive policies dialog (CLOSED, merged)](https://github.com/google-gemini/gemini-cli/pull/22456)**
   Replaces text-based `/policies` output with a searchable, tabbed UI — major UX improvement for policy management.

9. **[#27934 — chore(deps): bump marked from 15.0.12 to 18.0.5 (CLOSED, merged)](https://github.com/google-gemini/gemini-cli/pull/27934)**
   Markdown parser bump with breaking changes — may affect rendering of agent output.

10. **[#27926 — chore(deps): bump google-auth-library from 9.15.1 to 10.7.0 (CLOSED, merged)](https://github.com/google-gemini/gemini-cli/pull/27926)**
    Auth library major version bump. Impacts all GCP-integrated authentication flows.

## Feature Request Trends
- **AST-aware code understanding** (#22745, #22746, #22747): A three-issue investigation into AST-grep, AST-based file reading, and codebase mapping to reduce hallucinations and improve agent precision.
- **Sub-agent governance and safety** (#22672, #20303): Demand for guardrails against destructive commands and for remote agent auth/background operations.
- **Memory system reliability** (#26516 epic, #26522, #26523, #26525): Collective push to make Auto Memory deterministic, secure, and non-looping.
- **Evaluation infrastructure maturity** (#24353, #23166, #23313): Requests for stable, reliable, always-passing evaluation tests to prevent regressions in agent behavior.
- **Browser agent resilience** (#22232, #22267): Persistent lock recovery, Wayland support, and settings.json override compliance.

## Developer Pain Points
- **Agent hangs and false success reporting** (#21409, #22323, #25166): The most frequently upvoted issues involve subagents hanging indefinitely or reporting success when they hit turn limits. Erodes developer trust in autonomous workflows.
- **Shell execution brittleness** (#25166, #23571): Commands that hang after completion or scatter temp scripts across the filesystem frustrate users expecting clean, reproducible execution.
- **Configuration and permission leaks** (#22093, #22267): Subagents running despite being disabled in settings, and browser agents ignoring `settings.json` overrides — indicating a core configuration merge gap.
- **Tool overload and content structure bugs** (#24246, #27730): Hitting API limits with too many tools, and MCP array payloads leaking into wrong fields. Pain points for power users with many integrations.
- **Auto Memory inefficiency** (#26522, #26523): Low-signal sessions that never get marked as processed, and invalid patches accumulating silently. Creates background noise and wasted tokens.
- **Terminal and UI glitches** (#21924, #24935): Flickering on resize, corruption after external editor exit — ongoing polish issues for a terminal-native tool.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-06-15

## Today's Highlights
No new releases or pull requests landed in the last 24 hours. The community is actively discussing **eight open issues**, with a notable cluster of triage-level reports surfacing around session poisoning from malformed attachments, BYOK model discovery gaps, and cross-platform (Azure DevOps) integration requests. The most significant ongoing thread—duplicate item errors in agent workflows—continues to draw developer attention with 7 upvotes.

## Releases
No new releases in the last 24 hours.

## Hot Issues

### 1. Agent skills scripts executed in wrong folder
- **Issue:** [#956](https://github.com/github/copilot-cli/issues/956)
- **Author:** msundman78 | **Updated:** 2026-06-14 | **Comments:** 6 | 👍: 2
- **Why it matters:** This is a long-standing (since January) bug in the agents subsystem. Skills referencing scripts via relative paths (`scripts/myscript.sh`) execute from an unexpected working directory, breaking the official agentskills.io spec. Community has been discussing workarounds for 6 months without resolution.

### 2. Duplicate Item Errors
- **Issue:** [#3558](https://github.com/github/copilot-cli/issues/3558)
- **Author:** psulightning | **Updated:** 2026-06-14 | **Comments:** 4 | 👍: 7
- **Why it matters:** **Highest-voted open issue.** Users consistently hit `CAPIError: 400` with `Duplicate item found with id fc_call_...` after initial prompt processing. This blocks multi-turn agent sessions. The 7 reactions suggest this is a widespread blocker for power users.

### 3. Different prompt input box layout in two cmd tabs
- **Issue:** [#3797](https://github.com/github/copilot-cli/issues/3797)
- **Author:** kunalk16 | **Created:** 2026-06-15 | **Comments:** 1 | 👍: 0
- **Why it matters:** Freshly filed UI inconsistency bug. Within the same terminal window, two cmd tabs render different prompt box layouts—one appears broken or misaligned. Suggests a rendering state leak across tabs.

### 4. Feature request: opt-in model discovery for BYOK / custom providers
- **Issue:** [#3795](https://github.com/github/copilot-cli/issues/3795)
- **Author:** aosama | **Updated:** 2026-06-14 | **Comments:** 0 | 👍: 0
- **Why it matters:** BYOK users must manually set `COPILOT_MODEL` or `--model` with provider-specific identifiers. The request asks the CLI to proactively query custom provider endpoints for available models, streamlining setup.

### 5. Add Azure DevOps work items to Up next
- **Issue:** [#3794](https://github.com/github/copilot-cli/issues/3794)
- **Author:** OmerMicro | **Updated:** 2026-06-14 | **Comments:** 0 | 👍: 0
- **Why it matters:** The "Up next" inbox currently only surfaces GitHub items. For teams using Azure DevOps repos (already supported as projects), this creates a blind spot. A clear signal for broader DevOps ecosystem integration.

### 6. Malformed attachment poisons session; all subsequent turns fail with 400
- **Issue:** [#3791](https://github.com/github/copilot-cli/issues/3791)
- **Author:** jay-tau | **Updated:** 2026-06-14 | **Comments:** 0 | 👍: 0
- **Why it matters:** A critical session-state corruption bug. A single password-protected `.xlsx` causes a CAPI 400 that persists across all later turns—even when the attachment is removed. Users must restart the session entirely. High severity for any file-heavy workflow.

### 7. 590A:31190E:55961D:614135:6A2E7EBC … (spam/garbage issue)
- **Issue:** [#3793](https://github.com/github/copilot-cli/issues/3793)
- **Author:** ja552588 | **Updated:** 2026-06-14 | **Comments:** 0 | 👍: 0
- **Why it matters:** No description, only hex dumps in the title. Likely a mis-filed or spam report. Worth noting for maintainers as it may indicate broken report template validation or automated abuse.

### 8. hhhhhhh (closed as invalid)
- **Issue:** [#3796](https://github.com/github/copilot-cli/issues/3796)
- **Author:** TAREQ097H | **Created:** 2026-06-14 | **Comments:** 1 | 👍: 0
- **Why it matters:** Closed as invalid—likely test or spam. Reflects ongoing noise in issue tracker, possibly from new users unfamiliar with the reporting process.

## Key PR Progress
No pull requests were updated in the last 24 hours.

## Feature Request Trends
Based on recent issue activity, the most requested feature directions include:
- **BYOK / Custom Provider Model Discovery** – Users want the CLI to automatically enumerate models from custom endpoints rather than requiring manual `COPILOT_MODEL` configuration.
- **Cross-Platform Inbox Integration** – The "Up next" panel is being asked to surface work items from Azure DevOps in addition to GitHub, reflecting growing enterprise adoption of mixed DevOps toolchains.

## Developer Pain Points
- **Session poisoning fragility** – A single malformed attachment (e.g., encrypted `.xlsx`) can permanently corrupt a CLI session, requiring a full restart (#3791). This is a high-friction issue for developers working with native document attachments.
- **Duplicate item errors blocking multi-turn workflows** – The `Duplicate item found with id` error (#3558) remains the highest-voted problem, indicating that agent sessions frequently fail after the first turn when state management breaks.
- **Agent skill execution context confusion** – The long-open bug #956 shows that skill scripts do not execute from the expected directory, breaking the official spec and frustrating power users building custom agent skills.
- **UI rendering inconsistencies** – The newly reported cmd tab layout bug (#3797) suggests cross-tab state pollution, which can confuse developers managing multiple terminal sessions.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-15

## Today's Highlights
Kimi Code CLI saw no new releases in the last 24 hours, but community activity remains high with 3 new issues and 4 pull requests. A long-standing feature request (#850) for auto-loading project context files like `AGENTS.md` and `.cursorrules` was finally closed, signaling potential implementation. Meanwhile, user frustration over severe rate limiting (#2123) and a system prompt conflict bug (#2451) are the most pressing concerns.

## Releases
No new releases in the last 24 hours. The latest stable version is **Kimi Code v0.12.0** (as referenced in Issue #2451).

## Hot Issues

### 1. [#850 – Auto-load project context/rules (e.g., AGENTS.md, .cursorrules) at session start](https://github.com/MoonshotAI/kimi-cli/issues/850)
- **Status:** CLOSED (enhancement)  
- **Why it matters:** A highly requested feature inspired by Claude Code’s `CLAUDE.md` support. Users want the CLI to automatically detect and load project-level conventions and steering instructions. The closure suggests this may be shipped soon.  
- **Community reaction:** Moderate interest (3 comments, 1 👍). Users from adjacent tools are eager for parity.

### 2. [#2123 – 限速，限额严重 (Severe rate limiting & quota)](https://github.com/MoonshotAI/kimi-cli/issues/2123)
- **Status:** OPEN (enhancement)  
- **Why it matters:** User reports that actual API call limits are far below advertised “300–1200 requests per 5 hours” — often only 60+ calls. The user has requested a refund, citing insufficient disclosure.  
- **Community reaction:** 2 comments, 0 👍 — but a critical complaint for paid subscribers.

### 3. [#2451 – System prompt conflicting with my desired workflow](https://github.com/MoonshotAI/kimi-cli/issues/2451)
- **Status:** OPEN (bug)  
- **Why it matters:** A user on Debian with an API key subscription reports that the CLI’s built-in system prompt overrides their strict project guidelines, breaking their workflow.  
- **Community reaction:** No comments yet; early-stage report.

### 4. (Additional noteworthy issues are limited this week. The digest focuses on the most impactful ones above.)

## Key PR Progress

### 1. [#2452 – fix(tools): fail StrReplaceFile when a multi-edit hunk is unmatched](https://github.com/MoonshotAI/kimi-cli/pull/2452)
- **Status:** OPEN  
- **What it does:** Fixes a bug where `StrReplaceFile` would silently apply partial edits and only error if the **entire** document was unchanged. Now errors correctly when any individual hunk fails to match.  
- **Why it matters:** Prevents silent, incorrect file modifications during multi-edit operations — a critical reliability fix.

### 2. [#2018 – feat: add Alt+V paste support for Windows Terminal](https://github.com/MoonshotAI/kimi-cli/pull/2018)
- **Status:** CLOSED  
- **What it does:** Adds `Alt+V` as a fallback paste key binding because Windows Terminal intercepts `Ctrl+V`.  
- **Why it matters:** Resolves a long-standing usability issue for Windows users.

### 3. [#2020 – fix: use per-process log filenames to prevent rotation lock on Windows](https://github.com/MoonshotAI/kimi-cli/pull/2020)
- **Status:** CLOSED  
- **What it does:** Changes log file naming from `kimi.log` to `kimi.{pid}.log` to avoid `PermissionError` when multiple processes run concurrently.  
- **Why it matters:** Eliminates a frequent crash scenario on Windows.

### 4. [#839 – feat(shell): add configurable shell support for Windows](https://github.com/MoonshotAI/kimi-cli/pull/839)
- **Status:** CLOSED  
- **What it does:** Enables users to configure which shell (e.g., PowerShell, CMD, WSL) Kimi Code uses for command execution on Windows.  
- **Why it matters:** Expands cross-platform usability, especially for developer environments.

## Feature Request Trends
- **Project-context auto-loading:** Users strongly desire automatic detection and injection of project rules files (`.cursorrules`, `AGENTS.md`, etc.) at session start — a pattern popularized by Claude Code.
- **Better rate limit transparency:** Paid subscribers are demanding clear, upfront disclosure of API call limits and quotas, along with more generous limits for the “Code Plan.”
- **System prompt overrides:** A growing request for user-controlled system prompts that can take precedence over built-in instructions for custom workflows.

## Developer Pain Points
- **Unreliable rate limiting:** The "Code Plan" quota is perceived as misleading, with actual usage far below advertised limits, causing workflow interruptions and refund disputes.
- **System prompt inflexibility:** Built-in prompts can conflict with user-defined guidelines, forcing developers to workaround or abandon the CLI for certain tasks.
- **Windows compatibility gaps:** Despite recent fixes (paste, shell config, log rotation), Windows users still encounter friction — the OS remains a secondary citizen compared to Unix-like platforms.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest
**Date: 2026-06-15**

---

## Today's Highlights

OpenCode v1.17.7 ships with critical fixes for plugin connectivity and terminal integration, while the community rallies around DeepSeek V4 Pro's dramatic price cut with a high-engagement feature request. The TUI stability front sees multiple PRs landing to fix terminal teardown issues, and MCP client capabilities remain a top priority for power users.

---

## Releases

**v1.17.7** — [View Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.7)

**Bugfixes:**
- Plugin client requests now reuse the active server instead of assuming the default local port
- ACP shell tool calls now display the command and working directory from invocation time
- Plugin-provided shell environment variables properly apply to PTY sessions

**Improvements:**
- MCP infrastructure improvements (details in linked PRs)

---

## Hot Issues

1. **[#28846 — Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction](https://github.com/anomalyco/opencode/issues/28846)** 🏆 77 comments, 79 👍
   *Status: CLOSED* — The community is eagerly demanding that OpenCode Go subscription tiers reflect DeepSeek's massive price drop. High engagement signals this is a top business-viability concern for paid users.

2. **[#13984 — Cannot copy and paste in OpenCode CLI](https://github.com/anomalyco/opencode/issues/13984)** 🏆 48 comments, 20 👍
   *Status: OPEN (since Feb 2026)* — A long-standing clipboard pain point. Users report "copied to clipboard" feedback but actual paste fails. Multiple OS/terminal reports suggest a cross-platform issue.

3. **[#15585 — "Free usage exceed" with free models](https://github.com/anomalyco/opencode/issues/15585)** 🏆 48 comments, 13 👍
   *Status: CLOSED* — Users discovered free models have undocumented usage limits even after short sessions. Created confusion about what "free" actually means.

4. **[#28567 — Full MCP client capabilities](https://github.com/anomalyco/opencode/issues/28567)** 11 comments, 21 👍
   *Status: OPEN* — OpenCode's MCP client is lagging behind the protocol spec. Users want streaming, notifications, and proper tool result error handling. Tied to multiple open MCP-related bugs.

5. **[#5305 — Plugin Hook for Instant TUI Commands](https://github.com/anomalyco/opencode/issues/5305)** 18 comments, 13 👍
   *Status: OPEN* — Request for plugins to register commands that execute without the agent loop. Would enable quick actions and custom workflows without model overhead.

6. **[#32172 — Add GLM-5.2 model support for Z.AI provider](https://github.com/anomalyco/opencode/issues/32172)** 7 comments
   *Status: OPEN* — Z.AI's newest reasoning model is out but not yet available in OpenCode. Fresh request with immediate demand from Z.AI Coding Plan users.

7. **[#28957 — "Upstream idle timeout exceeded"](https://github.com/anomalyco/opencode/issues/28957)** 13 comments
   *Status: OPEN* — Sessions using the "writing-plans" skill time out on macOS Tahoe. Infrastructure-level error suggesting model service idle disconnection.

8. **[#25832 — OpenCode cannot read images anymore](https://github.com/anomalyco/opencode/issues/25832)** 12 comments, 4 👍
   *Status: OPEN* — Vision capability regression. Users who relied on image-based HTML editing report "Bad request" errors since late April.

9. **[#11829 — Recursive Language Model Context Management](https://github.com/anomalyco/opencode/issues/11829)** 6 comments, 11 👍
   *Status: OPEN* — Proposes treating context as an external queryable environment (RLM paradigm from MIT paper). Forward-thinking but complex.

10. **[#32348 — EditBuffer Destroyed after upgrading to 1.17.7](https://github.com/anomalyco/opencode/issues/32348)** 3 comments
    *Status: OPEN* — Fresh regression in latest release. Users on macOS Tahoe + Ghostty terminal hitting consistent `EditBuffer is destroyed` errors during normal editing.

---

## Key PR Progress

1. **[#32245 — fix(mcp): stop idle OAuth callback server](https://github.com/anomalyco/opencode/pull/32245)**
   *Status: OPEN* — Prevents port leaks by properly shutting down the MCP OAuth listener after callbacks complete. Critical for long-running MCP sessions.

2. **[#32367 — fix: create worktrees from empty git repos](https://github.com/anomalyco/opencode/pull/32367)**
   *Status: OPEN* — Fixes `git worktree add` failure on repos with no commits. Blocks users starting fresh projects with OpenCode worktrees.

3. **[#32302 — fix(opencode): forward parent attachments to subagents](https://github.com/anomalyco/opencode/pull/32302)**
   *Status: OPEN* — Fixes attachment handoff for `@mention` subagents in task flows. Closes #25553 — important for multi-agent workflows.

4. **[#32241 — fix(tui): render move errors inline](https://github.com/anomalyco/opencode/pull/32241)**
   *Status: OPEN* — Improves error UX for file/directory move operations by keeping errors inside the selection dialog instead of crashing the UI.

5. **[#32244 — fix(mcp): handle tool result errors](https://github.com/anomalyco/opencode/pull/32244)**
   *Status: CLOSED* — Routes MCP `CallToolResult.isError` through standard tool-error path. Closes #16969, related to MCP capabilities push (#28567).

6. **[#32364 — fix: reset terminal modes on TUI shutdown](https://github.com/anomalyco/opencode/pull/32364)**
   *Status: OPEN* — Addresses #32336 by ensuring mouse tracking, alt-screen, and bracketed paste are properly disabled on exit. Direct fix for terminal corruption.

7. **[#32362 — fix: include file content preview in oldString not found error](https://github.com/anomalyco/opencode/pull/32362)**
   *Status: OPEN* — Improves edit error messages by showing actual file content when `oldString` search fails. Closes #30863 — helps users debug failed edits.

8. **[#28152 — fix(server): share global memoMap in TCP listener](https://github.com/anomalyco/opencode/pull/28152)**
   *Status: CLOSED* — Fixes #28037 where plugin permission replies were silently dropped. TCP listener now uses a shared memoMap to deduplicate singleton services.

9. **[#27805 — [beta] Discover running serve instances from TUI](https://github.com/anomalyco/opencode/pull/27805)**
   *Status: OPEN* — Adds `opencode serve --discoverable` to let TUI auto-connect to running server instances. Beta feature for multi-window/server workflows.

10. **[#30907 — fix: expose all errors in edit tool instead of squashing to first](https://github.com/anomalyco/opencode/issues/30907)**
    *Status: CLOSED* — `Cause.squash()` was silently discarding all but the first error. Now surfaces full error chain for debugging multi-edit failures.

---

## Feature Request Trends

**1. MCP Protocol Parity** — Multiple issues (#28567, #31002) demand full MCP client support: streaming, notifications, proper error handling, and schema compliance. The ecosystem is outpacing OpenCode's implementation.

**2. AI Provider & Model Agility** — #28846 (DeepSeek pricing), #32172 (GLM-5.2), and #31475 (Composer 2.5) show users want rapid adaptation to model landscape changes, including pricing pass-through and new model discovery.

**3. Plugin System Expansion** — #5305 (instant TUI commands) and #28202 (async prompt handling) indicate plugin developers are pushing the boundaries of what hooks should support — especially for non-blocking operations and custom UI commands.

**4. Session & Context Management** — #11829 (RLM context), #24017 (prompt bookmarks), and #30763 (session flags) reflect growing demand for persistent session organization, especially as users run longer, more complex workflows.

**5. Remote & Server Workflows** — #31901 (SSH directories), #27805 (serve discovery), and #30355 (subagent directory inheritance) point toward multi-machine, daemon-driven usage patterns becoming mainstream.

---

## Developer Pain Points

**Terminal & TUI Stability** — The cluster of issues around terminal teardown (#32336, #20458), clipboard (#13984, #15604, #16521), and crashes on exit (#32334, #32330) suggests OpenCode's TUI layer has accumulated technical debt in state transitions. The fix in #32364 is welcome but the breadth of terminal pain points suggests deeper architectural review needed.

**Plugin Server & SDK Fragility** — #28037 (silently dropped permission replies), #29894 (silent abort no-ops in server mode), and #28202 (async prompt overlap) reveal that the plugin system's reliability degrades significantly when OpenCode runs in server/SDK-driven mode. Developers building on top of the SDK are hitting a wall of silent failures.

**Edit Tool Reliability** — #32348 (EditBuffer destroyed), #30907 (error squashing), and #30863 (missing error context) suggest the edit pipeline has fragility under concurrent or rapid-fire edit operations. The fix in #30907 is critical but more hardening needed.

**Vision Model Support** — #25832 (images broken) and #22469 (image input support) affect users who rely on visual understanding for web development. The regression from April suggests testing gaps for vision-specific model integration.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-06-15

## Today's Highlights
Activity is surging as the community pushes the agent framework toward multi-session and extension-level control. The most critical open issue is that **global and project `.pi` directories can overlap in `$HOME`**, a design ambiguity flagged by Armin Ronacher that affects every user. At the same time, a **cache-write pricing fix for Anthropic 1h writes** is already in PR, and an **xAI Grok OAuth login** has landed as a new built-in provider. The Escape-key interrupt feature is broken in two separate ways, drawing the most urgent attention.

## Releases
No new releases in the last 24 hours.

[↑ Back to top](#pi-community-digest--2026-06-15)

---

## Hot Issues

### 1. [#5671 – ~/.pi and cwd/.pi overlap](https://github.com/earendil-works/pi/issues/5671) (👍3)
> **What:** The folder `.pi` is used for both global settings and project-local settings, causing ambiguity when `$HOME` overlaps with a project directory.
> **Why it matters:** This is a structural design issue that Armin Ronacher raised in the context of #5619. While today the conflict is mitigated by storing global data under `.pi/agent`, the namespace collision creates confusion for new users and blocks cleaner project-scoped configuration.
> **Community sentiment:** High engagement; the 5 comments and 3 reactions indicate broad interest in a fix, likely splitting into `~/.config/pi` vs `.pi`.

### 2. [#5103 – Windows bash detector fails when Git Bash is on non-default drive](https://github.com/earendil-works/pi/issues/5103) (18 comments)
> **What:** The bash detector only searches `C:\Program Files\Git\bin\bash.exe`, missing installations on drives like `D:\`.
> **Why it matters:** This is the highest-comment issue on the board, affecting all Windows users with non-standard Git Bash installations. The root cause is a hardcoded path string instead of PATH resolution.
> **Community sentiment:** Frustrated but constructive; the reporter provided clear reproduction steps and debug output.

### 3. [#5653 – Move off Shrinkwrap (duplicate pi-ai on disk)](https://github.com/earendil-works/pi/issues/5653) (9 comments)
> **What:** Installing both `@earendil-works/pi-ai` and `@earendil-works/pi-coding-agent` as direct deps produces two copies of `pi-ai` on disk, breaking the API provider registry because it's a module-level `Map`.
> **Why it matters:** This is a dependency-management blocker for extension authors who need both packages. The duplicate copy means provider registrations from one copy are invisible to the other.
> **Community sentiment:** Marked `inprogress`; the community is waiting on a migration off Shrinkwrap to a deduplication-aware solution.

### 4. [#5736 – Escape no longer interrupts active interactive task](https://github.com/earendil-works/pi/issues/5736) (6 comments)
> **What:** Pressing Escape during an active interactive run no longer reliably cancels the current task, despite the UI advertising it as the cancel/abort key.
> **Why it matters:** This is a core UX regression. Users rely on Escape as the primary kill switch for runaway agents.
> **Community sentiment:** Co-authored with gpt-5.5, indicating the reporter used AI assistance to write the bug report. The team is actively investigating—marked `inprogress`.

### 5. [#5702 – prompt_cache_retention sent to providers that reject it](https://github.com/earendil-works/pi/issues/5702) (6 comments)
> **What:** A 400 error from OpenCode/Zen because `prompt_cache_retention` is sent to providers that don't support it. The reporter also flagged that `generate-models.ts` is hard to maintain.
> **Why it matters:** This is a cross-provider compatibility issue that blocks building on top of pi-ai. The model-registry build system is described as a "rabbit hole."
> **Community sentiment:** The reporter wrote a detailed "one discussion" rather than drip-feeding. The maintainability concern resonated—closed with a fix merged.

### 6. [#5654 – Add `excludeFromContext` to custom messages](https://github.com/earendil-works/pi/issues/5654) (👍1)
> **What:** A request to add `excludeFromContext?: boolean` to `CustomMessage` / `pi.sendMessage()`, mirroring the flag that bash-execution messages already have.
> **Why it matters:** This is a precise feature request for developers who inject status updates (e.g., `/status` slash command) that should not pollute LLM context. Multiple comments endorse it.
> **Community sentiment:** Positive; one reaction, and a PR (#5678) by mitsuhiko is already open.

### 7. [#5687 – pi list and pi update never exit when extension runs MCP server](https://github.com/earendil-works/pi/issues/5687) (6 comments)
> **What:** Package subcommands (`pi list`, `pi update`) finish their work but hang forever because `handlePackageCommand` loads extensions, and an MCP server keeps the process alive.
> **Why it matters:** This makes CLI automation impossible when extensions with MCP servers are installed. The command prints output but never exits to the shell.
> **Community sentiment:** Closed quickly; the team acknowledged the issue and merged a fix.

### 8. [#5706 – Task hangs indefinitely at waiting for summary approval with local LLM](https://github.com/earendil-works/pi/issues/5706) (5 comments)
> **What:** Pi gets stuck at the "waiting for summary approval" step when using a local OpenAI-compatible LLM backend. Cloud providers (DeepSeek, OpenAI) work fine.
> **Why it matters:** Local LLM users—a growing segment—are blocked from using the summary-approval workflow entirely.
> **Community sentiment:** The reporter provided exact reproduction steps. Closed, suggesting a fix was deployed.

### 9. [#5685 – Pressing Escape does not stop subagent/background agent](https://github.com/earendil-works/pi/issues/5685) (5 comments)
> **What:** Pressing Escape cancels the main task but the subagent keeps running.
> **Why it matters:** This is the second Escape-related bug today (#5736 is the other). Together they represent a systemic interrupt-propagation failure.
> **Community sentiment:** Closed as a duplicate of #5736 or related fix.

### 10. [#5208 – pi crashes when background process exits late output](https://github.com/earendil-works/pi/issues/5208) (4 comments)
> **What:** `uncaughtException: Cannot append to a finished output accumulator` when a background process's stdout/stderr pipes emit data after the `exit` event but before `close`.
> **Why it matters:** This is a crash, not a hang. Affects any background process with late-flushing output. The race condition is subtle and hard to reproduce.
> **Community sentiment:** Marked `inprogress`; the reporter provided a detailed analysis of the `ProcessRegistry` event ordering.

[↑ Back to top](#pi-community-digest--2026-06-15)

---

## Key PR Progress

### 1. [#5738 – fix(ai): price anthropic 1h cache writes at 2x input](https://github.com/earendil-works/pi/pull/5738)
> **What:** The Anthropic provider reads `ephemeral_1h_input_tokens` and charges 1h cache-write slices at 2× base input, fixing a 1.6× undercount.
> **Why important:** Accurate cost tracking is essential for users with high cache-hit rates. This is a direct fix to #5737.
> **Status:** Open, awaiting review.

### 2. [#5678 – Add excludeFromContext for custom messages](https://github.com/earendil-works/pi/pull/5678)
> **What:** Adds `excludeFromContext` to custom messages across the agent harness and extension APIs. Skips them in `convertToLlm` while persisting them for display.
> **Why important:** Enables status-only custom messages that don't bloat model context. Also teaches compaction and branch summarization to respect the flag.
> **Status:** Open, authored by mitsuhiko.

### 3. [#5735 – fix(coding-agent): defer extension reload requests safely](https://github.com/earendil-works/pi/pull/5735)
> **What:** Makes extension reload requests safe from all contexts (not just slash commands) by adding a deferral mechanism in `AgentSession`.
> **Why important:** Fixes a crash when extensions call `ctx.reload()` during active agent work.
> **Status:** Open, authored by mitsuhiko.

### 4. [#5732 – feat(extensions): support allowCommands option in sendUserMessage](https://github.com/earendil-works/pi/pull/5732)
> **What:** Adds `allowCommands?: boolean` to `sendUserMessage()`. When enabled, extension-injected prompts can execute slash commands.
> **Why important:** Enables session resets and custom control commands from external bridges. A precise extension API enhancement.
> **Status:** Closed, merged.

### 5. [#5731 – feat(coding-agent): Add tool instrumentation for execution profiling](https://github.com/earendil-works/pi/pull/5731)
> **What:** Adds tool-level instrumentation to profile execution time and success rates for each tool call.
> **Why important:** Provides visibility into slow or failing tools, critical for debugging agent workflows.
> **Status:** Closed, merged.

### 6. [#5714 – [codex] add xAI Grok account OAuth login](https://github.com/earendil-works/pi/pull/5714)
> **What:** Adds a built-in `xai-grok` OAuth provider with OIDC discovery, device-code login, and refresh tokens. Grok subscription models are surfaced in `/login`.
> **Why important:** New provider support directly expands the model ecosystem. Grok's CLI proxy is integrated as the backend.
> **Status:** Closed, merged.

### 7. [#5711 – feat(coding-agent): add extension prompt guideline API](https://github.com/earendil-works/pi/pull/5711)
> **What:** Implements `pi.setPromptGuidelines()` as a new ExtensionAPI method to inject guidelines into the system prompt.
> **Why important:** Solves #5710—extensions can now influence model behavior without hacking the system prompt. Marked "verified, works for me."
> **Status:** Open.

### 8. [#5385 – feat: detect first-run terminal theme](https://github.com/earendil-works/pi/pull/5385)
> **What:** Queries the terminal with OSC to detect light/dark theme on first run and persists it to settings.
> **Why important:** Removes friction for new users who previously had to manually set the theme. A quality-of-life improvement.
> **Status:** Closed, merged.

### 9. [#5708 – Wrap question extension text instead of truncating](https://github.com/earendil-works/pi/pull/5708)
> **What:** Fixes text truncation in question extensions; now wraps properly.
> **Why important:** Closes #5707, improving readability of long extension prompts.
> **Status:** Closed, merged.

### 10. [#5726/5725 – Fix test model IDs for checks](https://github.com/earendil-works/pi/pull/5726)
> **What:** Updates test model IDs to valid entries across providers and aligns compaction test model ID with current Anthropic naming.
> **Why important:** CI was failing due to stale model IDs. Both PRs are identical; #5725 was closed in favor of #5726.
> **Status:** Closed, merged.

[↑ Back to top](#pi-community-digest--2026-06-15)

---

## Feature Request Trends

The most-requested feature directions from this week's issues are:

1. **Multi-agent session management:** Multiple concurrent agent sessions with TUI switching (e.g., #5700). Users want to run background agents while working in the foreground, without tearing down sessions.

2. **Extension-level prompt control:** APIs for extensions to inject prompt guidelines (#5710), set `excludeFromContext` on custom messages (#5654), and configure `allowCommands` (#5733). The trend is toward richer extension APIs that give plugin authors more control over context and model behavior.

3. **Provider-specific auth config:** Support for per-provider configuration in `auth.json` beyond just API keys (#5728). Users with Cloudflare AI Gateway, OpenAI proxies, and custom deployments need fields like `accountId`, `gatewayId`, and base URLs in the config file.

4. **Model-specific compaction settings:** Different models have different context windows, so a single compaction config is suboptimal (#5722). Small models need lower reserve tokens, large long-context models need higher keepRecentTokens.

5. **Core extension marketplace curation:** The community is asking for official core extensions and a marketplace with categorization and rating (#5686). This signals that the extension ecosystem is maturing beyond experimental usage.

[↑ Back to top](#pi-community-digest--2026-06-15)

---

## Developer Pain Points

Recurring frustrations and high-frequency requests from this week's data:

1. **Escape-key interrupt is broken (systemic):** Two separate issues (#5736, #5685) report that Escape fails to stop main tasks and subagents. This is a core UX failure that erodes trust in the cancel mechanism.

2. **Local LLM compatibility gaps:** Local OpenAI-compatible backends hang at summary approval (#5706) and may have image rendering issues (#5618). The community using local models feels like second-class citizens.

3. **CLI hangs due to background processes:** Package commands (`list`, `update`) hang when MCP servers are active (#5687). This makes scripting and CI integration unreliable.

4. **Windows path handling is fragile:** The bash detector hardcodes paths (#5103), and the CJK-wide-character rendering issue (#5297) shows TUI is tested primarily on Unix with ASCII terminals.

5. **Deduplication gaps in dependency management:** The Shrinkwrap double-copy issue (#5653) creates module-level state corruption. Extension authors cannot safely nest dependencies without reinitializing the provider registry.

6. **Process lifecycle races:** Background processes can crash pi entirely (#5208) when stdout pipes fire after the `exit` event. Output truncation in bash tool (#5303) due to `waitForChildProcess` timing is a related pain point.

[↑ Back to top](#pi-community-digest--2026-06-15)

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-15

## Today's Highlights
A significant cluster of security and reliability bugs has surfaced, including a Trojan detection in the VSIX Windows package (Issue #5055) and a critical daemon segfault on Ubuntu 24.04 (#5114). The community shows strong demand for a `/import-config` migration tool from Claude (#4845) and a `--safe-mode` troubleshooting flag (#4943). The nightly release workflow continues to fail (#5117, #5068), adding pressure on the team's CI pipeline.

## Releases
**No new releases in the last 24 hours.** The nightly build workflow for `v0.18.0-nightly.20260615.91476134a` failed (#5117), following a similar failure on 2026-06-13 (#5068). Users awaiting the next stable release should monitor the [actions run](https://github.com/QwenLM/qwen-code/actions/runs/27516870586).

---

## Hot Issues (10 noteworthy)

1. **#5055 — Trojan:JS/ShaiWorm.DBA!MTB detection in VSIX**  
   [🔗 Issue](https://github.com/QwenLM/qwen-code/issues/5055)  
   *Status: Open | Priority: P1 | Category: Security*  
   A Windows user reports Windows Defender flags `qwenlm.qwen-code-vscode-ide-companion-0.18.0-win32-x64.vsix` as a trojan. This is a P1 security concern; the community expects an immediate investigation and a signed/clean re-release.

2. **#5080 — API key confusion between Standard and Token Plan endpoints**  
   [🔗 Issue](https://github.com/QwenLM/qwen-code/issues/5080)  
   *Status: Open | Priority: P2 | Category: Authentication*  
   Switching between `sk-xxx` (Standard) and Token Plan providers yields 401 errors, indicating a routing bug. Affects users on Alibaba Cloud Bailian who need seamless provider switching.

3. **#5083 — TUI freezes due to zombie child processes**  
   [🔗 Issue](https://github.com/QwenLM/qwen-code/issues/5083)  
   *Status: Open | Priority: P2 | Category: Performance*  
   A zombie `bash` subprocess (PID 255709) under the main process (PID 2920) was not reaped, causing the TUI to freeze. The root cause is likely improper child-process lifecycle management in the MCP/shell integration layer.

4. **#5102 — Side-effect execution despite permission-contract probe**  
   [🔗 Issue](https://github.com/QwenLM/qwen-code/issues/5102)  
   *Status: Open | Priority: P2 | Category: Security*  
   A provider-requested side effect (writing `modelock_denied_side_effect.txt`) was executed even during the permission probe. This breaks the fundamental security contract of the tool-use model.

5. **#5101 — Repeated large tool results inflate provider history**  
   [🔗 Issue](https://github.com/QwenLM/qwen-code/issues/5101)  
   *Status: Open | Priority: P1 | Category: Core/Performance*  
   A deterministic repro shows that repeated large tool outputs are sent back verbatim to the provider, causing unbounded context growth and eventual OOM. This is a critical memory-management gap.

6. **#5119 — No way to allow sudo commands interactively**  
   [🔗 Issue](https://github.com/QwenLM/qwen-code/issues/5119)  
   *Status: Open | Priority: P2 | Category: Security/UX*  
   Sudo commands fail ungracefully; the user must manually copy-paste each time. The permission dialogue lacks a "run with sudo" affordance, a blocker for system-administration workflows.

7. **#3203 — Proposed OAuth free tier cut from 1000 to 100 req/day**  
   [🔗 Issue](https://github.com/QwenLM/qwen-code/issues/3203)  
   *Status: Open | Type: Feature-Request*  
   A 135-comment, month-old debate on reducing the free tier from 1,000 to 100 daily requests and phasing it out by June 20. Community sentiment is strongly negative; many rely on free access for evaluation.

8. **#3267 — Free plan request limits not matching docs**  
   [🔗 Issue](https://github.com/QwenLM/qwen-code/issues/3267)  
   *Status: Closed*  
   A user hit the daily limit without completing a single task, pointing to a discrepancy between documented 1,000 requests/day and actual enforced limits. The closed status without a public resolution is concerning.

9. **#5114 — Daemon segfault on Ubuntu 24.04**  
   [🔗 Issue](https://github.com/QwenLM/qwen-code/issues/5114)  
   *Status: Closed | Tagged: FAQ*  
   A fresh `pip install qwen-code` followed by `python -m qwen_code.daemon` segfaults on Ubuntu 24.04. Closed quickly, but the FAQ tag suggests a known issue — users should check the daemon docs for workarounds.

10. **#5117/#5068 — Nightly release workflow failures**  
    [🔗 Issue #5117](https://github.com/QwenLM/qwen-code/issues/5117) | [Issue #5068](https://github.com/QwenLM/qwen-code/issues/5068)  
    *Status: Open*  
    Two consecutive nightly releases failed. Combined with previous CI issues, this signals a potential packaging or test regression in the release pipeline.

---

## Key PR Progress (10 important)

1. **#5120 — Skip auto-title when history has no user message**  
   [🔗 PR](https://github.com/QwenLM/qwen-code/pull/5120)  
   Prevents title generation for empty daemon sessions. A small but important guard against spurious API calls.

2. **#5094 — Workflow P4a: extractAndStripMeta + RunOutcome metadata**  
   [🔗 PR](https://github.com/QwenLM/qwen-code/pull/5094)  
   First half of Phase 4 of the Dynamic Workflows port (tracked in #4721). Extracts meta-information from tool outputs, enabling structured workflow orchestration.

3. **#5118 — Per-task token/time details in web-shell todos**  
   [🔗 PR](https://github.com/QwenLM/qwen-code/pull/5118)  
   Adds expandable cost/timing info for completed tasks in the web UI. Excellent for debugging token consumption.

4. **#4943 — `--safe-mode` flag for troubleshooting**  
   [🔗 PR](https://github.com/QwenLM/qwen-code/pull/4943)  
   Disables all customizations (hooks, MCP, extensions, skills) to isolate user-config issues. Highly requested by the community for debugging.

5. **#4850 — Interactive multi-tab `/extensions` manager**  
   [🔗 PR](https://github.com/QwenLM/qwen-code/pull/4850)  
   Turns the flat extensions list into a Discover/Installed/Sources tabbed UI. A major UX improvement for extension management.

6. **#4845 — `/import-config` for Claude config migration**  
   [🔗 PR](https://github.com/QwenLM/qwen-code/issues/4845)  
   *(Note: still an open feature request, but PR is linked)*  
   One-click import of MCP servers, instructions, permissions from Claude Code/Desktop. Critical for lowering switching friction.

7. **#5111 — Bound active tool result history**  
   [🔗 PR](https://github.com/QwenLM/qwen-code/pull/5111)  
   Adds a char-based budget for compactable tool results, clearing old ones via microcompaction. Directly addresses the memory issues in #5101.

8. **#5097 — Heartbeat fallback to prevent memory monitor starvation**  
   [🔗 PR](https://github.com/QwenLM/qwen-code/pull/5097)  
   Under autonomous loops, `queueMicrotask` and `setInterval` were starving, causing OOM. Heartbeat fallback ensures memory checks still fire.

9. **#4653 — Configurable agent ignore files**  
   [🔗 PR](https://github.com/QwenLM/qwen-code/pull/4653)  
   Adds support for `.agentignore` and `.aiignore` alongside `.qwenignore`. Uses existing ignore-filtering infrastructure; a clean extension.

10. **#5073 — Warn on oversized context instructions**  
    [🔗 PR](https://github.com/QwenLM/qwen-code/pull/5073)  
    Warns at startup if QWEN.md or context instructions exceed 15% of the model's context window. Prevents silent truncation surprises.

---

## Feature Request Trends

| Theme | Count | Key Issues |
|-------|-------|------------|
| **Claude migration tools** | 3+ | #4845 (`/import-config`), #4723 (rule system comparison) |
| **MCP server improvements** | 4+ | #4218 (Windows filesystem MCP broken), #5083 (zombie processes), #5100 (agent name breaks skills) |
| **Context/token management** | 5+ | #5101 (large results), #4369 (RAM leak via AI code), #4349 (estimatePromptTokens fix) |
| **UI/UX polish** | 3+ | #5104 (show active model in footer), #5064 (status line wrapping), #5118 (task details) |
| **Security & permission** | 4+ | #5119 (sudo support), #5102 (side-effect bypass), #5055 (trojan detection), #5114 (segfault) |

---

## Developer Pain Points

1. **Free tier instability** — The proposed reduction to 100 req/day (#3203) and undocumented throttling (#3267) erode trust. Many developers were relying on free access for CI and evaluation.

2. **Memory and process management** — Zombie processes (#5083), unbounded tool-result history (#5101), and memory monitor starvation (#5097) point to systemic weaknesses in the autonomous-loop runtime.

3. **Windows support gaps** — Trojan false positives in VSIX (#5055), MCP filesystem tools not working (#4218), and API key confusion (#5080) disproportionately affect Windows users.

4. **CI/CD reliability** — Back-to-back nightly release failures (#5117, #5068) and the PR triage pipeline refactor (#4866) signal growing pains as the project scales.

5. **Missing safe mode** — The need for `--safe-mode` (#4943) and `import-config` (#4845) highlights that configuration complexity is a pain point for both troubleshooting and onboarding.

6. **Language/regional feedback** — Several issues are filed in Chinese (#4727 TUI freeze, #5083, #5080), suggesting active adoption in China but also a need for bilingual maintainers.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-15

## Today's Highlights
The project has officially rebranded to **CodeWhale** (v0.8.60), with the legacy `deepseek-tui` npm package deprecated. However, the community is grappling with persistent TUI freezes and sub-agent timeouts across platforms, with Windows `crossterm` freezes and 120s API ceilings being the most disruptive issues. A major v0.8.61 patch PR is in draft review, targeting these launch-blocker bugs alongside new WhaleFlow foundation code.

## Releases
- **v0.8.60 (`CodeWhale` branding rollout)**: The canonical project name is now `CodeWhale` for all releases, commands, npm packages, and assets. The legacy `deepseek-tui` npm package is deprecated with no further releases. A migration guide is available at `docs/REBRAND.md`. Users on `v0.8.x` legacy names should plan migration accordingly.

## Hot Issues (Top 10)

1. **[#2487 – Turn stalled - no completion signal received](https://github.com/Hmbown/CodeWhale/issues/2487)** (*12 comments*)
   - **What**: YOLO mode freezes with "Turn stalled" error; `continue` fails to resume. The agent simply stops responding.
   - **Impact**: Critical usability blocker for agent mode users. Persistent across versions.
   - **Community**: Users report this happens frequently; workarounds nonexistent.

2. **[#3147 – MSBuild FileTracker Fails on Windows](https://github.com/Hmbown/CodeWhale/issues/3147)** (*7 comments*)
   - **What**: `cmake --build` is completely broken on Windows 10/11 when invoked from CodeWhale's managed shell (MSBuild FileTracker cannot initialize).
   - **Impact**: Blocks C++ developers using CodeWhale for build automation on Windows.
   - **Status**: CLOSED — likely fixed in a patched shell environment.

3. **[#1812 – TUI Freezes on Windows (crossterm poll)](https://github.com/Hmbown/CodeWhale/issues/1812)** (*5 comments*)
   - **What**: Intermittent TUI freezes on Windows 11 — UI completely unresponsive, but process stays alive. Two confirmed events with logs and thread-state analysis.
   - **Impact**: Core reliability issue affecting all Windows users.
   - **Community**: Multiple users confirming the behavior; high priority for maintainers.

4. **[#2475 – YOLO mode + Burp MCP interrupts tasks](https://github.com/Hmbown/CodeWhale/issues/2475)** (*4 comments*)
   - **What**: In YOLO mode, connecting to Burp proxy triggers MCP prompts that interrupt and break running tasks.
   - **Impact**: Security analysts relying on YOLO mode cannot use Burp integration reliably.

5. **[#1806 – Sub-agent 120s API timeout renders agent_open unusable](https://github.com/Hmbown/CodeWhale/issues/1806)** (*4 comments*)
   - **What**: Sub-agents fail identically after 120s timeout — exactly the kind of parallel task they're advertised for.
   - **Impact**: Parallel agent offloading is effectively broken for non-trivial tasks.
   - **Community**: Users reporting this as a "critical missing feature" for realistic workloads.

6. **[#2629 – 401 auth errors with SiliconFlow and Tencent TokenHub](https://github.com/Hmbown/CodeWhale/issues/2629)** (*3 comments*)
   - **What**: CodeWhale returns `401 invalid api key` for OpenAI-compatible providers like SiliconFlow and Tencent Cloud TokenHub, despite correct credentials.
   - **Impact**: Blocks Chinese-cloud users entirely.
   - **Community**: Multiple users confirming on Windows 11 with correct setup.

7. **[#1067 – glibc 2.39 requirement blocks Ubuntu 22.04](https://github.com/Hmbown/CodeWhale/issues/1067)** (*3 comments*)
   - **What**: Prebuilt binaries require glibc 2.39, which is only in Ubuntu 24.04+. Ubuntu 22.04 (glibc 2.35) users cannot run the binary.
   - **Impact**: Major Linux distribution blocker for server/Docker deployments.
   - **Community**: Requests for multi-glibc builds or static linking.

8. **[#2574 – Provider fallback chain (auto-switch on API failure)](https://github.com/Hmbown/CodeWhale/issues/2574)** (*3 comments*)
   - **What**: Currently, switching providers requires manual `/provider` command. Users want automatic fallback on quota exhaustion, 401, 429, or 5xx errors.
   - **Impact**: Workflow disruption when primary provider fails mid-task.
   - **Community**: Strong support; many users running multiple providers.

9. **[#2739 – Task execution freezes, infinite wait on continue](https://github.com/Hmbown/CodeWhale/issues/2739)** (*2 comments*)
   - **What**: Long-running bug-fix tasks freeze; `Esc` shows timeout; `continue` fails; session content lost on restart.
   - **Impact**: Users frustrated enough to abandon the tool entirely.
   - **Community**: User explicitly says they "can't tolerate it anymore."

10. **[#2924 – Can't update via npm](https://github.com/Hmbown/CodeWhale/issues/2924)** (*1 comment, 1 thumbs-up*)
    - **What**: `npm update` fails silently or errors on the rebranded `codewhale` package. Suggests packaging/registry issues.
    - **Impact**: Blocks users from receiving security fixes and features.

## Key PR Progress (Top 10)

1. **[#3225 – v0.8.61: community harvest + freeze fix + WhaleFlow foundation](https://github.com/Hmbown/CodeWhale/pull/3225)** ([Draft])
   - **What**: 28-commit assembly targeting the Windows freeze bug, community-contributed fixes, and WhaleFlow orchestration foundation. Not yet merge-ready — version bump is local.
   - **Importance**: The primary vehicle for addressing the most severe open bugs. Key PR for the whole community.

2. **[#3051 – Add /voice slash command for speech-to-text](https://github.com/Hmbown/CodeWhale/pull/3051)** ([CLOSED])
   - **What**: Three new slash commands (`/voice`, `/voice rec`, `/voice stop`) for one-shot speech recording via active provider's API.
   - **Importance**: Accessibility and UX improvement inspired by MiMo Code. Reuses existing API infrastructure.

3. **[#3197 – Rename DeepSeek blue consumers to whale accent](https://github.com/Hmbown/CodeWhale/pull/3197)** ([CLOSED])
   - **What**: Adds `WHALE_ACCENT_PRIMARY` color semantics, keeps `DEEPSEEK_BLUE` as deprecated alias. Visual identity migration.
   - **Importance**: Part of the rebranding effort; low risk but PR is actually good.

4. **[#2779 – Dormant provider fallback chain config](https://github.com/Hmbown/CodeWhale/pull/2779)** ([CLOSED])
   - **What**: Parses `fallback_providers = [...]` config with empty-list serialization skipped. Runtime still uses primary provider, but data model is ready.
   - **Importance**: Addresses #2574's config layer. A foundation for the runtime auto-switch logic.

5. **[#2811 – VS Code local runtime extension scaffold](https://github.com/Hmbown/CodeWhale/pull/2811)** ([CLOSED])
   - **What**: Official VS Code extension scaffold with commands to open CodeWhale, start `codewhale serve --http`, status bar state, and VSIX packaging metadata.
   - **Importance**: Brings CodeWhale into the mainstream editor ecosystem.

6. **[#2802 – Hugging Face MCP helpers](https://github.com/Hmbown/CodeWhale/pull/2802)** ([CLOSED])
   - **What**: Adds `/hf mcp status`, `/hf mcp setup`, `/hf concepts`, and `/huggingface` alias. Documents HF-generated MCP configuration.
   - **Importance**: Simplifies Hugging Face MCP integration for ML/AI developers.

7. **[#2771 – LLM-guided AGENTS.md init](https://github.com/Hmbown/CodeWhale/pull/2771)** ([CLOSED])
   - **What**: `/init` now gathers project context and delegates AGENTS.md generation to the LLM, instead of writing a static template.
   - **Importance**: Makes agent initialization adaptive and context-aware, reducing manual editing.

8. **[#2796 – Sidebar slash command](https://github.com/Hmbown/CodeWhale/pull/2796)** ([CLOSED])
   - **What**: Adds `/sidebar` command to toggle/show/hide the sidebar, with optional `--save` persistence.
   - **Importance**: UX tweak requested by users doing copy-heavy transcript work.

9. **[#2803 – Pausable custom command MVP](https://github.com/Hmbown/CodeWhale/pull/2803)** ([CLOSED])
   - **What**: Harvests pausable custom slash-command support — parse `pausable: true` frontmatter, engine pause state, pause gate before tool execution.
   - **Importance**: Enables interactive debugging of custom commands.

10. **[#2102 – Defer low-value native tools by default](https://github.com/Hmbown/CodeWhale/pull/2102)** ([CLOSED])
    - **What**: Native tools outside the core catalog are now deferred (lazy-loaded). Configurable via `[tools] always_load = [...]`.
    - **Importance**: Performance optimization — reduces startup time and memory for users who don't need niche tools.

## Feature Request Trends
- **Agent reliability & resumability**: Multiple issues ask for checkpoint/resume for sub-agents, longer timeouts, and visible progress. Users want agents that survive long tasks.
- **Provider flexibility**: Strong demand for automatic provider fallback chains, expanded provider support (DeepInfra, HuggingFace, Azure), and OpenAI-compatible API compatibility fixes (SiliconFlow, Tencent).
- **Orchestration & parallelism**: WhaleFlow swarm synthesis (reduce pass), fleet ledger as shared task list, and multi-agent coordination are recurring themes. Users want "ultracode-style" heterogeneous-model workers.
- **TUI polish**: Clarification question modals, cost tracking for non-DeepSeek models, token/context visibility during long tasks, and auth error diagnostics.
- **Ecosystem integration**: VS Code extension, Zed/AgentClientProtocol registry listing, and Hugging Face MCP integration signals a need for CodeWhale to live inside other IDEs.

## Developer Pain Points
- **Windows TUI freezes** (#1812, #2739): Cross-term poll freezes are the #1 platform-specific complaint. Multiple confirmed events, session loss on restart.
- **Sub-agent timeout / stall** (#1806, #2487, #2475): The 120s API ceiling and "Turn stalled" errors make parallel agent workflows unreliable. Users are abandoning the tool over this.
- **Authentication & API compatibility** (#2629, #2574): OpenAI-compatible providers return 401 errors for correctly configured credentials. No automatic fallback — manual `/provider` switch needed on failure.
- **Linux glibc version lockout** (#1067, #3207): Prebuilt binaries require glibc 2.39, excluding Ubuntu 22.04 (2.35) and many server/Docker environments. No static build option.
- **Rebranding migration pain** (#2917, #2924): The `deepseek-tui` → `codewhale` rename has broken update paths (`npm update`, `cargo install`). Users stuck on old versions cannot update.
- **Context clipping** (#2652): Sub-agent and tool outputs are clipped in live transcript, but the model treats them as full evidence. Leads to incorrect orchestration decisions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*