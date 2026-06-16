# AI CLI Tools Community Digest 2026-06-16

> Generated: 2026-06-16 02:32 UTC | Tools covered: 9

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
**Date: 2026-06-16 | Prepared for Technical Decision-Makers**

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem continues to mature rapidly across six major competitors—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI—each serving distinct developer segments. Today's analysis reveals a market split between **platform-backed tools** (Claude Code, Codex, Gemini CLI, Copilot CLI) with deep ecosystem integration and **community-driven tools** (OpenCode, Pi, DeepSeek TUI, Qwen Code) that prioritize extensibility and multi-provider flexibility. A dominant theme across all tools is the tension between **agent autonomy** (auto-execution, sub-agents, background loops) and **user control** (permission systems, sandboxing, interrupt mechanisms). Windows and WSL compatibility remains the single largest cross-cutting pain point, with every tool reporting platform-specific bugs that degrade the developer experience. The community is increasingly vocal about **silent failures**—data truncation, false success reporting, and unkillable agent loops—demanding better observability and fail-fast semantics.

---

## 2. Activity Comparison

| Tool | Open Issues | Open PRs | Release Status (24h) | Key Community Signal |
|------|------------|---------|---------------------|---------------------|
| **Claude Code** | ~50+ active (10 hot) | 10 key PRs | v2.1.178 shipped | ENOSPC bug cluster (6 issues), VS Code auto-attach #1 request (163👍) |
| **OpenAI Codex** | ~10 hot issues | 10 key PRs | v0.140.0 stable + v0.141.0 alpha | Linux desktop app (583👍), 6 Windows/WSL bugs in 24h |
| **Gemini CLI** | 10 hot issues | 10 key PRs | No release | Agent hangs (#21409) and false success reporting (#22323) top P1s |
| **Copilot CLI** | 10 hot issues | 1 PR (test) | v1.0.63 shipped | 5 terminal rendering bugs, MCP looping regression |
| **Kimi Code CLI** | 4 active issues | 2 PRs | No release | Smallest community; proxy gap (#2455) and hook emptiness (#2303) |
| **OpenCode** | 10 hot issues | 10 key PRs | No release | Memory megathread (#20695, 96 comments), MCP client modernization |
| **Pi** | 10 hot issues | 10 key PRs | v0.79.4 shipped | Codex connection hang (#4945, 57 comments), Shrinkwrap debt (#5653) |
| **Qwen Code** | 10 hot issues | 10 key PRs | v0.18.1 + desktop-v0.0.4 | `/loop` ecosystem expansion, virtualized history bug (#5142) |
| **DeepSeek TUI** | 50 total (10 hot) | 50 PRs in motion | No release (v0.8.62 pending) | Sub-agent refactor, provider ecosystem expansion (5 new providers) |

**Observations:**
- **Top velocity:** Qwen Code (2 releases in 24h), DeepSeek TUI (50 active PRs), Claude Code (19 PRs from single contributor)
- **Most community engagement:** OpenAI Codex (583👍 on single issue), Claude Code (163👍 on auto-attach), OpenCode (84👍 on /goal)
- **Most fragmented:** DeepSeek TUI (massive PR volume, but no release) vs. Kimi Code CLI (minimal activity, 2 PRs)

---

## 3. Shared Feature Directions

| Feature Theme | Tools Involved | Specific Community Needs |
|---------------|----------------|------------------------|
| **Persistent Session Goals** | OpenCode (#27167, 84👍), Claude Code (#24726, 163👍), Kimi Code CLI (#2222) | Cross-turn `/goal` directives, persistent session IDs, archive/unarchive, searchable history |
| **Windows/WSL Path Compatibility** | ALL tools | Backslash normalization (Claude Code #68700, Codex #28094, Qwen Code #5173), UTF-8 corruption (Copilot CLI #3776, #3813), drive letter mangling |
| **Silent Failure Elimination** | Claude Code (#53940, #63909), Gemini CLI (#22323), Qwen Code (#3153) | Data truncation warnings, false success reporting, unkillable agent loops, fail-fast semantics |
| **Multi-Model & Provider Flexibility** | OpenAI Codex (#3282), Copilot CLI (#3282), Pi (#5363, #5509), DeepSeek TUI (#2574, #3005) | BYOK multi-model switching, automatic provider fallback chains, per-message model routing |
| **MCP/Plugin Ecosystem Maturity** | Claude Code (#68677, #68671), Copilot CLI (#3756), OpenCode (#28567), Qwen Code (#4966) | Full spec adherence, schema validation, server-sourced instructions, scope-based permissions |
| **Sandboxing & Permission Systems** | Claude Code (v2.1.178 `Tool(param:value)`), OpenCode (#2242, 53👍), Copilot CLI (#953), DeepSeek TUI (#1186) | File system isolation, command whitelisting, persistent allow/deny/ask rules, granular repo scoping |
| **Memory & Context Management** | Claude Code (#63358), OpenCode (#20695), Qwen Code (#4941), Pi (#5463) | Auto-compaction loops, token budget visibility, OOM after quit, context-window-aware warnings |
| **Background / Loop Automation** | Qwen Code (#5094, #5148), Claude Code (#68707 `/bug`), Codex (#28429 `sleep` tool) | Daemon-mode agents, `/loop` scheduling, interruptible sleep, background sub-agents |

---

## 4. Differentiation Analysis

| Dimension | Platform-Backed Tools | Community-Driven Tools |
|-----------|----------------------|----------------------|
| **Primary Advantage** | Ecosystem integration (VS Code, GitHub, Google Cloud) | Multi-provider flexibility, rapid community innovation |
| **Target Users** | Enterprise teams, IDE-first developers | Power users, polyglot AI developers, cost optimizers |
| **Technical Approach** | Monolithic: bundled models, proprietary agents | Modular: provider-agnostic, plugin/extensibility-first |
| **Release Cadence** | Stable + nightly (Codex: v0.140.0 stable) | Fast iteration (DeepSeek TUI: 50 PRs open) |
| **Windows Support** | Improving but inconsistent (Codex: 6 new bugs/24h) | Worse (Kimi: session resume broken, Pi: git-bash undetected) |

**Key Differentiators by Tool:**
- **Claude Code:** Most mature permission system (`Tool(param:value)` syntax), richest plugin metadata infrastructure, but ENOSPC bug cluster undermines macOS reliability
- **OpenAI Codex:** Strongest enterprise feature set (local credential broker #28034, sandbox path handling), but Linux desktop gap (583👍) and false-positive safety checks erode trust
- **Gemini CLI:** Most methodical quality approach (component-level evals #24353, SSRF hardening), but agent hangs (#21409) and sub-agent undersue (#21968) frustrate users
- **Copilot CLI:** Best GitHub integration, but slowest innovation velocity (1 PR in 24h), MCP looping regression (#3782) and terminal rendering bugs pervasive
- **Qwen Code:** Most ambitious feature roadmap (`/loop` ecosystem, dynamic workflows Phase 4), fastest release cycle (2 releases/24h), but OOM and flickering issues
- **DeepSeek TUI:** Highest community contribution velocity (50 PRs), widest provider support (DeepInfra, Atlas Cloud, WeChat bridge), but stalled turns (#2487) remain critical
- **OpenCode:** Strongest MCP modernization effort (#32490), but memory leaks (#20695) and billing activation failures (#32420) hinder adoption
- **Pi:** Cleanest architecture (data-driven model registry #5743), but smallest community, Codex connection reliability (#4945) is existential UX risk
- **Kimi Code CLI:** Most focused (smallest scope), but also most fragile—only 4 active issues cover core functionality gaps (proxy, hooks, session resume)

---

## 5. Community Momentum & Maturity

| Tool | Community Maturity | Velocity Signal | Risk Factors |
|------|-------------------|-----------------|--------------|
| **Claude Code** | **High** — Diverse contributor base, structured triage, plugin ecosystem | 19 PRs from single contributor (AZERDSQ131), 6 ENOSPC issues | Silent data corruption (#53940), VM overhead (#29045) |
| **OpenAI Codex** | **Very High** — Largest community (583👍 issues), enterprise focus | v0.140.0 stable, alpha v0.141.0, 10 architectural PRs | Linux desktop gap, false-positive safety blocks, Windows regression wave |
| **Gemini CLI** | **Medium-High** — Google-backed, methodical eval culture | P1/P2 issue discipline, 10 PRs with security focus | Agent hangs, sub-agent undersue, slow feature velocity |
| **Copilot CLI** | **Medium** — GitHub ecosystem captive audience, low external contribution | 1 PR/24h (inactive), v1.0.63 shipped | Terminal rendering regressions, MCP instability, no PR velocity |
| **Kimi Code CLI** | **Low** — Smallest community, limited language support | 2 community PRs/24h, no maintainer response | Minimal activity, proxy gap blocks enterprise adoption |
| **OpenCode** | **Medium-High** — Passionate power-user community, clear governance | 10 PRs/24h, MCP modernization focus | Memory leaks, billing failures, desktop UI freezes |
| **Pi** | **Medium** — Niche but engaged, rapid bug-fix response | v0.79.4 shipped, 10 PRs/24h, strong maintainer presence | Smallest model ecosystem, Codex dependency risk |
| **Qwen Code** | **High** — Fastest-growing feature surface, Chinese + global community | 2 releases/24h, Phase 4 workflows, 10 PRs | OOM regressions, terminal compatibility issues |
| **DeepSeek TUI** | **Very High (Velocity)** — Most active PRs (50), diverse provider ecosystem | 50 PRs in motion, no release = bottleneck risk | Stalled turns (#2487), no release discipline, fragmentation |

**Maturity Rankings (Overall):**
1. **OpenAI Codex** — Largest community, strongest architecture, but Windows gap undermines platform claim
2. **Claude Code** — Most mature ecosystem (plugins, permissions), but silent data bugs critical
3. **Qwen Code** — Fastest iteration, broadest feature ambition, but stability lags
4. **DeepSeek TUI** — Highest community contribution, but release discipline needed
5. **Gemini CLI** — Most methodical quality culture, slowest feature velocity
6. **OpenCode** — Strong niche for power users, memory issues holding it back
7. **Copilot CLI** — Best GitHub integration, but stagnating innovation
8. **Pi** — Clean architecture, smallest ecosystem
9. **Kimi Code CLI** — Minimal activity, highest fragility

---

## 6. Trend Signals

### Industry Trends from Community Feedback

1. **Agent Autonomy vs. Control is the Defining Tension**
   - Every tool is grappling with the same trade-off: how much to let agents execute autonomously vs. require user permission.
   - Claude Code's `Tool(param:value)` syntax, OpenCode's sandboxing requests, and DeepSeek TUI's persistent permission rules all point toward **structured, scoped autonomy** — not binary allow/deny.

2. **Windows/WSL is the Undisputed #1 Platform Pain Point**
   - No tool delivers a first-class Windows experience. Path mangling, UTF-8 corruption, terminal rendering bugs, and process lifecycle issues are universal.
   - Community signals demand **cross-platform as a first-class requirement**, not an afterthought.

3. **Silent Failures Are Eroding Trust Faster Than Functional Gaps**
   - File truncation (Claude Code #53940), false success reporting (Gemini CLI #22323), and unkillable agent loops (Qwen Code #3153) generate disproportionately high community outrage compared to feature gaps.
   - **Observability (token usage, resource telemetry, agent state) is becoming a core UX requirement**, not a nice-to-have.

4. **MCP/Plugin Ecosystem is the New "App Store" Battlefield**
   - Every major tool is investing in extensibility: Claude Code (`.claude/plugins`), Codex (credential broker), Gemini CLI (SSRF hardening for MCP), OpenCode (server-sourced instructions).
   - The winner will be the tool with **the lowest friction for third-party developers** — schema validation, spec adherence, and debugging tools.

5. **Multi-Provider Flexibility is Becoming Table Stakes**
   - Users want to route between models by cost, capability, or latency — not be locked into a single provider.
   - DeepSeek TUI (5+ providers), Pi (Bedrock Mantle), and Qwen Code (multi-provider disambiguation) are leading; Claude Code and Codex risk being seen as "walled gardens."

6. **Background Automation is the Next Frontier**
   - Qwen Code's `/loop`, Codex's `sleep` tool, and Claude Code's daemon features signal a shift from interactive sessions to **persistent, scheduled agents** for monitoring, maintenance, and CI-like workflows.

### Reference Value for Developers

| If You Care About... | Consider... |
|---------------------|------------|
| **Maximum ecosystem integration** | Claude Code (Anthropic ecosystem) or Copilot CLI (GitHub) |
| **Enterprise reliability** | OpenAI Codex (strongest architecture, but Windows gap) |
| **Multi-provider flexibility** | DeepSeek TUI (widest provider support) or OpenCode (MCP-first) |
| **Fastest innovation** | Qwen Code (2 releases/24h, `/loop` ecosystem) |
| **Windows cross-platform** | None are excellent; avoid Claude Code (ENOSPC) and Copilot CLI (MCP regression) |
| **Community-driven extensibility** | DeepSeek TUI (50 PRs) or Claude Code (mature plugin system) |
| **Security & auditability** | Gemini CLI (SSRF hardening, deterministic redaction) |
| **Lightweight / minimal footprint** | Pi (data-driven architecture, smallest dependency tree) |

**Bottom Line:** The AI CLI tool market is converging on a common set of requirements—Windows compatibility, multi-provider support, observable agent behavior, and structured permission systems. The tools that solve the **silent failure problem** and deliver **cross-platform parity** will win the next wave of adoption. Platform-backed tools have ecosystem depth; community tools have flexibility and velocity. The winning approach may be a hybrid: platform-level infrastructure with community-driven extensibility standards.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-16 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following Skills received the highest community engagement based on discussion volume and cross-referencing across PRs and Issues.

### 1.1 document-typography (#514) — *Open*
**Functionality:** Prevents common typographic defects in AI-generated documents: orphan word wrap (1–6 words stranded on a new line), widow paragraphs (section headers isolated at page bottom), and numbering misalignment.
**Discussion highlights:** Recognized as affecting *every* document Claude generates—users rarely request good typography explicitly, making this a high-value defensive skill. The PR has accumulated significant supporting commentary around edge cases for multi-column layouts.
**Status:** Open since 2026-03-04 | [View PR](https://github.com/anthropics/skills/pull/514)

### 1.2 run_eval.py fix suite (#556 / #1298 / #1169) — *Open / Multiple PRs*
**Functionality:** A cluster of PRs and issues addresses systemic failure in `run_eval.py`: the evaluation loop reports **recall=0% for every skill description**, meaning the skill-creator optimization pipeline optimizes against noise. PR #1298 provides the most comprehensive fix, including Windows stream reading, trigger detection, and parallel worker fixes.
**Discussion highlights:** Issue #556 (12 comments) and #1169 (3 comments) document independent reproductions across multiple environments. This is the community's most-reported blocker for skill development.
**Status:** PR #1298 open since 2026-06-10 | [View Issue #556](https://github.com/anthropics/skills/issues/556) | [View PR #1298](https://github.com/anthropics/skills/pull/1298)

### 1.3 ODT skill — OpenDocument text creation (#486) — *Open*
**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on mentions of "ODT", "ODS", "ODF", "LibreOffice", or requests for open-source/ISO standard documents.
**Discussion highlights:** The skill addresses a clear gap—Claude can generate DOCX but not the open-standard ODF equivalent. Community discussion centers on interoperability with LibreOffice and template rendering fidelity.
**Status:** Open since 2026-03-01 | [View PR](https://github.com/anthropics/skills/pull/486)

### 1.4 Testing patterns skill (#723) — *Open*
**Functionality:** Comprehensive testing stack coverage: Testing Trophy model, AAA pattern, React component testing with Testing Library, integration testing, E2E patterns, and TDD workflows.
**Discussion highlights:** One of the few skills targeting developer workflow directly. Community interest signals demand for Claude-guided test generation beyond simple unit tests.
**Status:** Open since 2026-03-22 | [View PR](https://github.com/anthropics/skills/pull/723)

### 1.5 Agent governance / safety (#412) — *Closed (as Issue)*
**Functionality:** Proposed skill for governance patterns in AI agent systems—policy enforcement, threat detection, trust scoring, and audit trails.
**Discussion highlights:** 6 comments noting a critical gap: the skills collection covers creative, technical, and enterprise workflows, but nothing focused on agent safety and governance. Closed as a proposal, but the demand persists.
**Status:** Issue closed 2026-06-13 | [View Issue](https://github.com/anthropics/skills/issues/412)

### 1.6 Shodh-memory — persistent context (#154) — *Open*
**Functionality:** Persistent memory system for AI agents that maintains context across conversations. Teaches Claude when to surface relevant memories and how to structure them.
**Discussion highlights:** 2 months of active iteration. The skill addresses a fundamental limitation—sessionless AI agents—and aligns with the broader community interest in stateful agent behavior.
**Status:** Open since 2025-12-19 | [View PR](https://github.com/anthropics/skills/pull/154)

### 1.7 AURELION skill suite (#444) — *Open*
**Functionality:** Four complementary skills: aurelion-kernel (structured thinking templates with a 5-floor cognitive framework), aurelion-advisor, aurelion-agent, and aurelion-memory.
**Discussion highlights:** The most ambitious multi-skill submission. Combines knowledge management, cognitive scaffolding, and persistent memory into a single ecosystem submission.
**Status:** Open since 2026-02-21 | [View PR](https://github.com/anthropics/skills/pull/444)

---

## 2. Community Demand Trends

Analysis of Issues (sorted by comments) reveals four clear demand vectors:

### 2.1 Skill-sharing infrastructure (#228 — 14 comments, 7 👍)
Organizations need native skill sharing without manual file transfer. Currently users must download `.skill` files, send them via Slack/Teams, and have colleagues manually upload. A shared skill library or direct sharing link is the top-requested feature.

### 2.2 Skill-creator pipeline reliability (#556, #1169, #1061 — cumulative 18 comments)
The `run_eval.py` recall=0% bug is the single most impactful blocker. Multiple independent reproductions confirm the description-optimization loop produces meaningless results. Windows compatibility issues (PATHEXT, cp1252 encoding, `select` on pipes) compound the problem.

### 2.3 Namespace security (#492 — 7 comments, 2 👍)
Community skills distributed under `anthropic/` namespace create a trust boundary vulnerability. Users may grant elevated permissions to community skills they mistake for official Anthropic releases.

### 2.4 Duplicate skill prevention (#189 — 6 comments, 9 👍)
Installing `document-skills` and `example-skills` plugins simultaneously produces identical skills, consuming context window space. The community expects deduplication logic in the installation pipeline.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and address clear pain points; they are likely to merge soon:

| PR | Skill | Key Fix | Status |
|----|-------|---------|--------|
| #1298 | run_eval.py fix | Recall=0% across all queries; Windows stream reading | Open since Jun 10 |
| #541 | DOCX tracked changes | `w:id` collision with existing bookmarks | Open since Mar 6 |
| #539 | YAML unquoted description | Silent parsing failures from unquoted `:` chars | Open since Mar 6 |
| #538 | PDF case-sensitive refs | 8 case mismatches in SKILL.md file references | Open since Mar 6 |
| #1140 | Agent-creator meta-skill | Task-specific agent sets; Windows support | Open since May 15 |

[View PR #1298](https://github.com/anthropics/skills/pull/1298) | [View PR #541](https://github.com/anthropics/skills/pull/541) | [View PR #539](https://github.com/anthropics/skills/pull/539) | [View PR #538](https://github.com/anthropics/skills/pull/538) | [View PR #1140](https://github.com/anthropics/skills/pull/1140)

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for tooling reliability and developer experience—fixing `run_eval.py`'s systemic recall failure, enabling Windows compatibility, and providing organizational skill-sharing infrastructure—before the ecosystem can absorb new domain-specific Skills.**

---

# Claude Code Community Digest — 2026-06-16

## Today's Highlights

A strong community maintenance day: v2.1.178 shipped with `Tool(param:value)` permission syntax and nested skill loading fixes. The bug tracker shows a troubling cluster of spurious ENOSPC errors on macOS (at least 6 open issues), alongside continued friction with the VS Code extension's auto-attach behavior and Windows cowork tool truncation. A wave of 19 PRs from contributor AZERDSQ131 landed, fixing pagination bugs, Windows path handling, and plugin author metadata across the `.claude/plugins` ecosystem.

## Releases

**v2.1.178** — [Release Link](https://github.com/anthropics/claude-code/releases/tag/v2.1.178)
- New `Tool(param:value)` syntax for permission rules, enabling parameter-level matching with `*` wildcards (e.g., `Agent(model:opus)` to block Opus subagents)
- Skills in nested `.claude/skills` directories now load when working on files in those directories
- On name clash, the nested skill takes precedence

## Hot Issues

1. **[#24726] VS Code: Disable auto-attach of open file/selection** — [Issue](https://github.com/anthropics/claude-code/issues/24726)  
   *53 comments, 163 👍* — The most-upvoted open feature request. Users want a toggle to stop Claude from automatically reading the active editor tab or selection. Community frustration is high; many report it pollutes context with irrelevant code.

2. **[#53940] Cowork Edit/Write silently truncates files via byte-conservation buffer cap** — [Issue](https://github.com/anthropics/claude-code/issues/53940)  
   *33 comments, 12 👍* — A deterministic Windows bug: the buffer cap truncates file content silently. No error, no warning. A "data corruption"–level bug by any standard. The community is actively requesting an immediate fix.

3. **[#29045] Claude Desktop spawns 1.8 GB Hyper-V VM on every launch** — [Issue](https://github.com/anthropics/claude-code/issues/29045)  
   *27 comments, 56 👍* — Even for chat-only use (no code, no agents). The VM is mandatory, not lazy-started. Heavy criticism around resource waste. Users want an opt-out or lazy-init for the VM.

4. **[#29017] Conversation history lost in VS Code extension** — [Issue](https://github.com/anthropics/claude-code/issues/29017)  
   *22 comments, 18 👍* — A long-standing macOS bug (filed Feb 2026). History disappears after closing/reopening VS Code. No workaround documented. High severity for daily users.

5. **[#12953] Mousewheel scrolls input history instead of chat history** — [Issue](https://github.com/anthropics/claude-code/issues/12953)  
   *16 comments, 14 👍* — Windows TUI: the input box steals scroll events. Very old issue (Dec 2025). Community is frustrated it keeps getting deprioritized.

6. **[#63909] Task runner reports ENOSPC on subprocess output despite free disk** — [Issue](https://github.com/anthropics/claude-code/issues/63909)  
   *12 comments, 19 👍* — One of at least 6 open ENOSPC-related bugs on macOS. The `statfs().bsize=0` root cause (see #65166) is known. Community notes that arbitrary command output is silently lost—extremely disruptive for CI-like workflows.

7. **[#63358] Opus 4.8 returns empty thinking blocks** — [Issue](https://github.com/anthropics/claude-code/issues/63358)  
   *10 comments, 10 👍* — Regression from Opus 4.7 (#49268). Extended thinking fields are empty in the API response, so the UI shows nothing. Community suspects a model-side issue but is frustrated by the lack of a workaround.

8. **[#62016] Claude passes `rg -rn` as `--replace=n`, corrupting search output** — [Issue](https://github.com/anthropics/claude-code/issues/62016)  
   *10 comments, 10 👍* — Claude's muscle memory for `rg -r` (recursive grep) conflicts with ripgrep's `-r` = `--replace`. Every match is silently rewritten to "n". Exit code 0, no error. Claude then misattributes its own corrupted output. A sharp edge for ripgrep users.

9. **[#67865] Desktop silently hangs installing .mcpb with entries >16KB** — [Issue](https://github.com/anthropics/claude-code/issues/67865)  
   *4 comments, 5 👍* — New: local `.mcpb` bundles with files larger than ~16KB cause a silent hang on Windows. No error, no timeout, just a frozen installer. For MCP developers distributing tools, this blocks deployment entirely.

10. **[#68677] Skill description frontmatter not surfaced for ~50% of user-defined skills** — [Issue](https://github.com/anthropics/claude-code/issues/68677)  
    *3 comments* — Brand new bug (filed 2026-06-15). When Claude loads skills into the system reminder, roughly half of user-defined skills have their `description` frontmatter dropped. The selection appears non-deterministic. For anyone relying on skill descriptions for routing, this breaks discoverability.

## Key PR Progress

1. **[#68678] Fix: Don't mark Claude Desktop issues as invalid** — [PR](https://github.com/anthropics/claude-code/pull/68678)  
   *Closed.* The triage bot was incorrectly labeling Claude Desktop bug reports as "invalid." The `.claude/commands/triage-issue.md` rule explicitly listed "Claude Desktop/Mobile apps" as non-Claude-Code, which was wrong given the unified repository.

2. **[#68707] Feat: Add /bug command to file GitHub issues from terminal** — [PR](https://github.com/anthropics/claude-code/pull/68707)  
   *Open.* Proposes a `bug-reporter` plugin with a `/bug` slash command that keeps the entire filing flow inside Claude Code—auto-collects system info, captures the current session log, and submits via API. Could dramatically lower the barrier for high-quality bug reports.

3. **[#68672] Fix: Load only event:all rules for unknown tools in hookify** — [PR](https://github.com/anthropics/claude-code/pull/68672)  
   *Closed.* The hookify plugin's pretooluse/posttooluse hooks left the `event` variable as `None` for any tool other than Bash or Edit/Write/MultiEdit, causing rules for other tools to silently load zero rules.

4. **[#68671] Fix: PostToolUse hooks cannot return permissionDecision: deny** — [PR](https://github.com/anthropics/claude-code/pull/68671)  
   *Closed.* Both PreToolUse and PostToolUse hooks were returning `permissionDecision: "deny"`, but only PreToolUse supports it. PostToolUse now correctly returns `skip` and `allow` only, aligning with the MCP spec.

5. **[#68681] Fix: Correct pagination break condition and HTTP 2xx status check** — [PR](https://github.com/anthropics/claude-code/pull/68681)  
   *Closed.* Two bugs: pagination stopped at `length === 0` instead of `length < page_size` (missing items on exact page boundaries), and a `201` status code from `gh` was treated as a failure.

6. **[#68700] Fix: Add bash prefix and normalize plugin root path for Windows** — [PR](https://github.com/anthropics/claude-code/pull/68700)  
   *Closed.* The `CLAUDE_PLUGIN_ROOT` variable contains backslashes on Windows, breaking bash scripts. Adds a path normalization step in `sg-python.sh` and all hookify hooks.

7. **[#68702] Fix: Guard PROMPT_PARTS expansion against set -u on bash 3.x (macOS)** — [PR](https://github.com/anthropics/claude-code/pull/68702)  
   *Open.* macOS ships bash 3.2. Expanding an empty array with `${array[*]}` under `set -u` triggers `unbound variable` and aborts the ralph-loop setup. This PR adds a guard.

8. **[#68689] Fix: Block symlink escape in extensibility config reads** — [PR](https://github.com/anthropics/claude-code/pull/68689)  
   *Open.* The `security-guidance` plugin read user-controlled config files with bare `open(path)`—no symlink resolution validation. If a user's `.claude/claude-security-guidance.md` is a symlink to `/etc/passwd`, it would be read and included in the LLM prompt. Adds `os.path.realpath` checks.

9. **[#68686] Fix: Rename shadowed 'field' variable and fix inline dict comma parsing** — [PR](https://github.com/anthropics/claude-code/pull/68686)  
   *Open.* Two bugs in `config_loader.py`: the variable `field` shadows the `dataclasses.field` import, and inline dicts like `{"key1": 0 "key2": 0}` (missing comma) were silently accepted instead of raising a parse error.

10. **[#60427] Docs: Use standard GitHub capitalization in README** — [PR](https://github.com/anthropics/claude-code/pull/60427)  
    *Open.* A trivial but long-standing docs PR fixing "Github" → "GitHub" in the README. Still unmerged after 28 days.

## Feature Request Trends

- **VS Code extension controls** (see #24726): Strong demand for granular auto-attach settings (disable open-file reading, disable selection monitoring). The 163 👍 on #24726 makes it the single most-requested enhancement.
- **Per-message model selection** (#68165): Users want to route trivial vs. complex messages to different models inline, without switching sessions. "Use Sonnet for `ls` and Opus for architecture decisions."
- **Conversation lifecycle management** (#65615, #29017): Multiple requests for archive/delete conversation features. Users report ballooning session lists with no cleanup mechanism.
- **Model-level controls**: Recurring requests for thinking toggle fixes (#49739), usage credit error recovery (#68561), and capability-aware tool selection (#66488).

## Developer Pain Points

1. **ENOSPC / disk-full false positives (macOS)** — At least 6 open issues (#63909, #65166, #65915, #65067, #68383, #65577) with the same root cause: `statfs().bsize=0` on tmpfs, or racing cleanup deletes. Commands are silently killed, output is lost. This is the most pervasive high-severity bug cluster.

2. **Silent data loss in Cowork mode (Windows)** — #53940: Edit/Write tools truncate files without warning. The byte-conservation buffer cap fires deterministically at all file sizes. Community reactions suggest this is actively breaking workflows.

3. **Desktop VM resource overhead** — #29045: The 1.8 GB Hyper-V VM is non-optional. #65577: The VM's rootfs.img grows unboundedly and is never reclaimed. Combined, these make the desktop app a resource hog even for chat-only use.

4. **Model regression whack-a-mole** — #63358 (Opus 4.8 empty thinking, a repeat of #49268 from Opus 4.7) and #62016 (`rg -rn` corruption) suggest that model behavior regressions are being caught by the community faster than they're being tested internally.

5. **Plugin/extension ecosystem fragility on Windows** — A major theme of today's PRs: backslash paths in bash scripts (#68700, #68694, #68699), CRLF line endings breaking version probes (#68701), Microsoft Store Python stub (#68699). The community is patching these one-by-one, but the core issue is that the plugin runtime assumes a Unix filesystem.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-16

## Today's Highlights
Codex ships **v0.140.0** with long-awaited token usage tracking (`/usage`), oversized text and image preservation in `/goal`, and permanent session deletion. The community remains deeply engaged on the **Linux desktop app request** (583 👍, 112 comments), while a new wave of **Windows/WSL path integrity bugs** and **false-positive cybersecurity flags** on routine DevOps tasks are generating urgent discussion. Internally, OpenAI engineers are advancing multi-platform credential brokering, cross-OS sandbox path handling, and a user message queue system for app-server.

---

## Releases
- **rust-v0.140.0** — Major stable release. New features:
  - `/usage` views for daily, weekly, and cumulative account token activity.
  - `/goal` now preserves oversized text, large pasted blocks, and image attachments (including in remote app-server sessions).
  - Permanent session deletion support added.
- **rust-v0.141.0-alpha.1 / alpha.2** — Two pre-release alphas published in the last 24 hours; changelogs not yet detailed.

---

## Hot Issues (Top 10 by Community Impact)

1. **#11023 — Linux Desktop App Request**  
   *[enhancement, app]* | 583 👍 | 112 comments  
   The top-voted open request. Users report macOS power issues (#10432) and urgently need a native Linux Codex Desktop.  
   [GitHub](https://github.com/openai/codex/issues/11023)

2. **#12661 — Windows: Markdown `file://` links open in Edge instead of VS Code**  
   *[bug, windows-os, extension]* | 43 👍 | 47 comments  
   Persistent editor integration issue breaking local documentation workflows. Community frustrated by lack of progress.  
   [GitHub](https://github.com/openai/codex/issues/12661)

3. **#18960 — Frequent reconnect loop: WebSocket closed before response completes**  
   *[bug, connectivity]* | 33 👍 | 42 comments  
   MacOS Codex App users hitting streaming failures that stall ongoing work sessions.  
   [GitHub](https://github.com/openai/codex/issues/18960)

4. **#3355 — Error after MacBook sleep: backend-api/codex/responses**  
   *[bug, connectivity]* | 19 👍 | 37 comments  
   Long-running tasks interrupted by lid close; no graceful resume mechanism after system sleep.  
   [GitHub](https://github.com/openai/codex/issues/3355)

5. **#21527 — "Codex is really too slow"**  
   *[bug, app, performance]* | 17 👍 | 32 comments  
   Performance regression affecting both VS Code extension and Codex App on Windows, with slow model response times.  
   [GitHub](https://github.com/openai/codex/issues/21527)

6. **#25719 — macOS: `syspolicyd`/`trustd` CPU/memory runaway triggered by Codex Desktop**  
   *[bug, app, computer-use, performance]* | 33 👍 | 26 comments  
   System process explosion causes machine slowdown; requires reboot to recover.  
   [GitHub](https://github.com/openai/codex/issues/25719)

7. **#27817 — False positive cybersecurity flag on tax filing work**  
   *[bug, safety-check]* | 0 👍 | 18 comments  
   Legitimate personal finance workflows incorrectly blocked by safety systems, eroding trust in automated guardrails.  
   [GitHub](https://github.com/openai/codex/issues/27817)

8. **#28015 — False positive cybersecurity flag blocks local repo maintenance in CLI**  
   *[bug, CLI, safety-check]* | 0 👍 | 18 comments  
   Routine `git` hygiene tasks flagged as security risks; paid sessions interrupted with extra prompts.  
   [GitHub](https://github.com/openai/codex/issues/28015)

9. **#28094 — Windows/WSL: Home project paths rewritten as `C:\home`, losing chat associations**  
   *[bug, windows-os, app, session]* | 1 👍 | 13 comments  
   After update, WSL paths are mangled, breaking project-chat context and showing "valid working directories as missing."  
   [GitHub](https://github.com/openai/codex/issues/28094)

10. **#27331 — multi_agent_v2 config breaks every turn with `spawn_agent` 400 error**  
    *[bug, exec, CLI, regression]* | 5 👍 | 4 comments  
    Feature-flag enabled causes API validation failure on every turn, even without sub-agent usage. Severity flagged as SEV3.  
    [GitHub](https://github.com/openai/codex/issues/27331)

---

## Key PR Progress (Top 10 by Architectural Significance)

1. **PR #26334 — fix: retry transient Guardian reviewer failures**  
   *CLOSED* — Treats rate-limit/timeout/transport failures as retryable, not policy denials. Prevents false safety blocks.  
   [GitHub](https://github.com/openai/codex/pull/26334)

2. **PR #28034 — Add local credential broker**  
   *OPEN* — Virtualizes GitHub/OpenAI credentials inside a MITM proxy, avoiding token leaks to child processes. Foundation for secure multi-agent tool access.  
   [GitHub](https://github.com/openai/codex/pull/28034)

3. **PR #28421 — Bind shell snapshots to retained thread environments**  
   *OPEN* — Moves shell snapshot lifetime from session-scoped to turn-environment-scoped, fixing stale environment state.  
   [GitHub](https://github.com/openai/codex/pull/28421)

4. **PR #28367 — Use ApiPathString for cross-OS sandbox config in app-server**  
   *CLOSED* — Enables Windows→Linux and Linux→Windows sandbox path passing without mangling.  
   [GitHub](https://github.com/openai/codex/pull/28367)

5. **PR #28429 — Add interruptible sleep tool**  
   *OPEN* — New built-in `sleep` tool allows the model to pause without blocking; resumes naturally when new input arrives.  
   [GitHub](https://github.com/openai/codex/pull/28429)

6. **PR #28307 — Queue TUI follow-ups through app-server**  
   *OPEN* — First proof-of-concept for durable user message queue in the CLI TUI, moving follow-ups from client memory to server.  
   [GitHub](https://github.com/openai/codex/pull/28307)

7. **PR #28425 — Carry fork lineage in initial history**  
   *OPEN* — Fixes fork ancestry metadata loss across session start, resume, and rollout boundaries.  
   [GitHub](https://github.com/openai/codex/pull/28425)

8. **PR #28260 — Add internal auto-compaction opt-out**  
   *OPEN* — Escape hatch for context-window compaction; preserves manual `/compact` behavior while allowing providers to disable auto-compaction.  
   [GitHub](https://github.com/openai/codex/pull/28260)

9. **PR #27945 — Seed session pickers from the State DB**  
   *OPEN* — Faster resume/fork picker by using indexed state DB as first-page source instead of waiting for filesystem scan.  
   [GitHub](https://github.com/openai/codex/pull/27945)

10. **PR #28146 / #28152 — Preserve remote environment cwd across OS boundaries**  
    *OPEN* — Fixes cross-OS (Linux app-server → Windows exec-server) working directory rendering for models and commands.  
    [GitHub](https://github.com/openai/codex/pull/28146) | [GitHub](https://github.com/openai/codex/pull/28152)

---

## Feature Request Trends

1. **Native Linux Desktop App** (#11023, 583 👍) — Long-unfulfilled demand, driven by macOS power/compatibility issues.
2. **VS Code inline diff & reliable undo** (#15367) — Parity with GitHub Copilot's editor UX: exact change locations and reliable revert.
3. **Multi-OS WSL path handling** (#28094, #26985, #28086) — Users need transparent cross-filesystem support for Windows/WSL workflows.
4. **Persistent session/thread reliability** (#21743, #28263, #28423) — Thread lists not refreshing across clients; goal-first sessions hidden from resume.
5. **Safety system transparency** (#27817, #28015) — Users want clear false-positive resolution paths and fewer unnecessary blocks on legitimate work.

---

## Developer Pain Points

- **Windows & WSL remain second-class citizens** — Six new Windows-specific bugs in 24 hours: path mangling, non-standard drive detection failures, sandbox helper not found, Korean characters in user profile paths crash the app, and `access denied` on bundled executables.
- **False-positive safety checks erode trust** — Routine finance tasks and DevOps maintenance flagged as "cybersecurity risk," requiring manual override loops. Developers report being blocked on authorized work.
- **Reconnect loops after sleep/network blips** (#3355, #18960, #28295) — MacOS and China-based users hit persistent streaming failures with no automatic recovery.
- **Multi-agent v2 feature flag regression** (#27331) — Enabling the flag breaks *every* turn, not just agent-spawning ones, suggesting insufficient validation on config-backed features.
- **Performance regressions on Windows** (#21527, #27603) — 15-second inter-turn delays on Codex CLI for Windows; general slowness reported on both CLI and app.

---

*Data snapshot: 2026-06-16 UTC. For real-time updates, monitor the [OpenAI Codex GitHub repository](https://github.com/openai/codex).*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-16

## Today's Highlights
No new releases today, but the community is actively tracking long-running issues around agent reliability, memory system hygiene, and security hardening. Several PRs landed around SSRF protection, terminal compatibility, and dependency pinning. The team is also prioritizing component-level evaluations and AST-aware codebase tooling as part of a broader quality push.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   *Priority P1, 7 comments, 11 weeks open.* This EPIC tracks building on behavioral eval infrastructure. With 76 tests across 6 Gemini models, the team is standardizing evaluation robustness. High signal for quality assurance investment.

2. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   *Priority P1, 7 comments, 8 👍.* A critical bug where `gemini-cli` hangs indefinitely when deferring to the generalist agent for simple tasks like folder creation. Users are pinning issues to instructing the model not to use sub-agents. Top community frustration.

3. **[#22323 — Subagent recovery after MAX_TURNS falsely reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *Priority P1, 6 comments.* `codebase_investigator` subagent reports success even after hitting turn limits without any analysis. This masks real failures and misleads users about task completion.

4. **[#22745 — Assess AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   *Priority P2, 7 comments.* A forward-looking EPIC investigating whether AST-aware tools can reduce turns, improve token efficiency, and enable precise method-bound reads. Could dramatically improve agent code understanding.

5. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   *Priority P2, 5 comments.* Auto Memory sends transcripts to extraction models before redacting secrets. Also logs existing skill content. Security-sensitive issue with privacy implications.

6. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
   *Priority P2, 5 comments.* Sessions remain unprocessed if the extraction agent skips them as low-signal, causing infinite re-surfacing. Inefficient memory management that wastes compute.

7. **[#25166 — Shell command execution stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *Priority P1, 4 comments, 3 👍.* A frequent blocker: simple CLI commands hang after finishing, showing "Waiting input." Reported for trivial commands that never prompt. High impact on daily workflow.

8. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *Priority P2, 6 comments.* Users with custom skills (gradle, git) report the model ignores them unless explicitly instructed. Core user experience issue limiting customization value.

9. **[#27938 — High memory usage detected](https://github.com/google-gemini/gemini-cli/issues/27938)**  
   *Priority P2, 2 comments, opened yesterday.* Crash report showing 24GB+ heap before Mark-Compact failures. Memory leak suspicion, effort/large.

10. **[#27935 — Gemini CLI with gemini-2.5-pro lied about reading screenshots](https://github.com/google-gemini/gemini-cli/issues/27935)**  
    *Priority P2, 2 comments, opened yesterday.* Model claims to read iOS screenshots and confirm changes, but actually did not. Hallucination issue with visual capabilities in CLI context.

## Key PR Progress

1. **[#27572 — fix(cli): handle tmux false positive background detection](https://github.com/google-gemini/gemini-cli/pull/27572)** — *Closed.* Fixes regression where Gemini CLI misdetects light backgrounds inside tmux (especially with mosh), causing incorrect theme switching. User-reported regression resolved.

2. **[#27603 — fix(core): add platform-aware shell guidance](https://github.com/google-gemini/gemini-cli/pull/27603)** — *Closed.* Adds Windows-specific shell commands to the operational prompt, fixing `#27751`. Important for cross-platform parity.

3. **[#27626 — fix(core): block private OAuth metadata URLs](https://github.com/google-gemini/gemini-cli/pull/27626)** — *Closed.* SSRF protection for MCP OAuth metadata discovery. Prevents attackers from using OAuth flows to probe internal networks.

4. **[#27744 — fix(web-fetch): resolve DNS before SSRF guard](https://github.com/google-gemini/gemini-cli/pull/27744)** — *Open.* Blocks hostname-to-private-IP bypass using wildcard DNS services (e.g., `127.0.0.1.nip.io`). Critical security hardening.

5. **[#27739 — fix(web-fetch): prevent SSRF via DNS hostnames and redirects](https://github.com/google-gemini/gemini-cli/pull/27739)** — *Open.* Companion to #27744, adds redirect-chain validation and synchronous DNS resolution. Effort/large security fix.

6. **[#24478 — feat(cli): add top-level /reload command](https://github.com/google-gemini/gemini-cli/pull/24478)** — *Closed (Stale).* Adds `/reload` (alias `/refresh`) to resync all agent state—skills, agents, MCP servers, memory, settings—in one command. Valuable UX improvement.

7. **[#27948 — chore(deps): pin dependencies and enforce 14-day update cooldown](https://github.com/google-gemini/gemini-cli/pull/27948)** — *Open.* Strips all range specifiers from dependencies, pins exact versions, and enforces a cooldown for automated updates. Supply-chain security hardening.

8. **[#27943 — fix(core-tools): resolve defensive path resolution for @-reference files](https://github.com/google-gemini/gemini-cli/pull/27943)** — *Open.* Fixes "File not found" when the model uses `@filename` mentions with filesystem tools. Prevents silent failures on CLI-referenced files.

9. **[#27854 — Fix/pending tools and trust overrides](https://github.com/google-gemini/gemini-cli/pull/27854)** — *Closed.* Prevents premature state progression during user tool approvals, serializes file writes to eliminate races, and fixes config trust override bugs. Improves execution stability.

10. **[#27947 — fix(config): migrate coreTools setting to tools.core](https://github.com/google-gemini/gemini-cli/pull/27947)** — *Open.* Migrates deprecated `coreTools` array to nested `tools.core` schema across workflows and A2A server config. Cleanup for config consistency.

## Feature Request Trends

- **Agent self-awareness and configuration alignment** — Multiple issues request the model to understand its own CLI flags, hotkeys, and settings overrides (e.g., `settings.json` ignored by browser agent). Users want the agent to act as its own expert guide.
- **AST-aware codebase tooling** — Continued interest in using Abstract Syntax Trees for file reads, searches, and codebase mapping to reduce token waste and improve navigational precision.
- **Backgroundable sub-agents** — Users want to send non-blocking sub-agents (builds, linting, exploration) to the background with `Ctrl+B` while maintaining the main interaction.
- **Destructive behavior safeguards** — Community is pushing for the agent to prefer safer alternatives over `--force`, `git reset`, or database modifications, and to warn before destructive operations.
- **Auto Memory improvements** — Feature requests center on deterministic secret redaction, banning low-signal retry loops, and quarantining invalid patches.

## Developer Pain Points

- **Agent hangs and false success reporting** — The generalist agent hang (#21409) and MAX_TURNS false success (#22323) are top frustrations. Users cannot trust completion signals and must work around sub-agent delegation.
- **Sub-agent undersue** — The model rarely activates custom skills or sub-agents unless explicitly prompted, undermining the value of configuration investments (#21968).
- **Terminal and input quirks** — Frequent issues with shell command hangs after completion, `Cmd+Backspace` deleting entire input without undo, terminal corruption after external editors, and tmux false background detection.
- **Memory system inefficiency** — Auto Memory's indefinite retries, logging of unredacted secrets, and silent skipping of invalid patches create both performance and security pain points.
- **SSRF and security gaps** — Two web-fetch SSRF PRs highlight recurring concerns about DNS-based bypasses and private IP access. The team is actively closing these gaps, but user trust in web-fetch safety remains a concern.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date: 2026-06-16**

## Today's Highlights
Version 1.0.63 ships with two quality-of-life improvements: blocked image attachments now provide actionable guidance instead of cryptic errors, and `--help` output is alphabetically sorted. However, the community is grappling with a wave of terminal rendering bugs, MCP server looping regressions, and session recovery issues that dominated the issue tracker this week.

---

## Releases
**v1.0.63** (2026-06-15) — [Release](https://github.com/github/copilot-cli/releases/tag/v1.0.63)
- Image attachment failures now explain how to resolve (enable vision policy, switch models)
- `--help` options are now alphabetically sorted for easier navigation

**v1.0.63-0** (2026-06-15) — [Release](https://github.com/github/copilot-cli/releases/tag/v1.0.63-0)
- **Added:** `w` key in `/diff` to hide whitespace-only changes
- **Added:** `deferTools` option in MCP server config to keep tools always available
- **Improved:** Reliability of OpenAI, Anthropic, and Azure OpenAI requests
- **Fixed:** Experimental `/rewind` no longer crashes

---

## Hot Issues (Top 10)

1. **[#953 — Over excessive permissions request](https://github.com/github/copilot-cli/issues/953)**  
   *Opened Jan 2026, 7 comments, 3 👍*  
   Users want granular scoping of AI access to specific repos/areas rather than blanket read/write to the entire GitHub account. The lack of progress on this enterprise-critical feature after 5 months is a growing concern.

2. **[#3727 — Regression: `userPromptSubmitted` hook context lost in v1.0.60](https://github.com/github/copilot-cli/issues/3727)**  
   *4 comments*  
   Plugin developers are blocked: the `additionalContext` from hooks is no longer injected into the planner. Affects all users relying on custom context injection via plugins.

3. **[#3282 — Add multiple BYOK model support](https://github.com/github/copilot-cli/issues/3282)**  
   *3 comments, 8 👍*  
   Users with bring-your-own-key setups currently must terminate and restart to switch models. The TUI lacks multi-model switching, making BYOK impractical for teams.

4. **[#3781 — Unrecoverable 400 error when pasting image with non-multimodal model](https://github.com/github/copilot-cli/issues/3781)** (#3781, CLOSED)  
   *3 comments*  
   Once an image is attached, every subsequent prompt fails with HTTP 400. Users must manually edit `events.jsonl` to recover — a terrible UX that v1.0.63's new guidance partially addresses.

5. **[#3756 — Third-party MCP servers disabled by organization policy](https://github.com/github/copilot-cli/issues/3756)**  
   *3 comments*  
   Enterprise users report their organization policies block third-party MCP servers entirely, with no clear path to request exceptions or configure allowed servers.

6. **[#2966 — Built-in multi-session management](https://github.com/github/copilot-cli/issues/2966)**  
   *3 comments, 1 👍*  
   Power users juggling multiple repos/tasks want first-class session management (naming, listing, parallel sessions) instead of relying on manual terminal multiplexing.

7. **[#3776 — UTF-8 mojibake when pasting from WSL to Windows](https://github.com/github/copilot-cli/issues/3776)**  
   *2 comments, 1 👍*  
   Slovak/Czech characters displayed correctly in terminal become garbled after copy-paste to Windows apps. A cross-platform localization blocker.

8. **[#3784 — Tokio reactor panic on Linux ARM64](https://github.com/github/copilot-cli/issues/3784)** (#3784, CLOSED)  
   *2 comments*  
   v1.0.62-1 crashes immediately after first prompt on ARM64. The WebSocket send triggers a panic — critical for ARM (Apple Silicon / Raspberry Pi) users.

9. **[#3769 — Threaded output mangling in Agency mode](https://github.com/github/copilot-cli/issues/3769)**  
   *2 comments, 3 👍*  
   Streaming output interleaves thinking and response text, producing jumbled display until completion. A significant usability regression in the Agency UI.

10. **[#3813 — Japanese text garbled in VS Code Terminal](https://github.com/github/copilot-cli/issues/3813)**  
    *1 comment*  
    Copy-paste works fine in iTerm2 but fails in VS Code's integrated terminal. Another internationalization issue joining the growing list.

---

## Key PR Progress
Only **1 PR** was updated in the last 24 hours (all others had 0 activity):

1. **[#3817 — `kCreate "#"`](https://github.com/github/copilot-cli/pull/3817)** (OPEN)  
   *Author: edge500*  
   Minimal PR titled with placeholder content — appears to be a test or accidental submission, not production-relevant.

*No other PRs were active in the review period.*

---

## Feature Request Trends
The most frequently requested directions from community issues include:

- **Granular permission scoping** — Users want to restrict Copilot's GitHub API access to specific repos and operations, not grant blanket read/write to their entire account.
- **Multi-model BYOK management** — Teams want to switch between multiple custom models without restarting sessions or reconfiguring environment variables.
- **Session content search** — The `--resume` feature should search inside session messages, not just names/IDs, to help users find past work.
- **Unified chronicle across VS Code** — Users want `/chronicle` to index VS Code Copilot Chat sessions alongside CLI sessions for a single searchable history.
- **Concurrent session management** — Power users need built-in support for running and switching between multiple parallel sessions across different repos/tasks.

---

## Developer Pain Points
Several recurring frustrations emerged from this week's issue activity:

- **Terminal rendering regressions** — Multiple issues ([#3769](https://github.com/github/copilot-cli/issues/3769), [#3776](https://github.com/github/copilot-cli/issues/3776), [#3780](https://github.com/github/copilot-cli/issues/3780), [#3797](https://github.com/github/copilot-cli/issues/3797), [#3813](https://github.com/github/copilot-cli/issues/3813)) report output mangling, UTF-8 corruption, and character repetition. These are degrading the core user experience.
- **MCP server instability** — Unbounded respawning loops ([#3782](https://github.com/github/copilot-cli/issues/3782)), OAuth fan-out ([#3706](https://github.com/github/copilot-cli/issues/3706)), and enterprise policy blocks ([#3756](https://github.com/github/copilot-cli/issues/3756)) make the MCP integration unreliable for production use.
- **Session corruption without recovery** — Oversized attachments ([#3767](https://github.com/github/copilot-cli/issues/3767)) and non-multimodal image paste ([#3781](https://github.com/github/copilot-cli/issues/3781)) permanently wedge sessions with no built-in recovery mechanism — users must manually edit JSON files.
- **Windows-specific breakage** — The standalone EXE fails to extract ([#3810](https://github.com/github/copilot-cli/issues/3810)), debug log paths have missing backslashes ([#3815](https://github.com/github/copilot-cli/issues/3815)), and UTF-8 paste is broken from WSL — multiple platform issues with no recent fixes.
- **Resource consumption during failures** — One user reported AIC tokens continuing to drain while all requests were failing with transient errors ([#3814](https://github.com/github/copilot-cli/issues/3814)), highlighting a lack of fail-fast logic.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-16

---

## Today's Highlights

No new releases landed in the last 24 hours, but two important pull requests from community contributor `logicwu0` are now open, directly addressing long-standing hook and session resume bugs. A new issue (#2455) reports that `FetchURL` ignores system proxy settings, which could block users in restricted networks — a significant usability gap.

---

## Releases

**No new releases in the last 24 hours.**

---

## Hot Issues

**#2455** — [FetchURL does not read system proxy, fails in blocked environments](https://github.com/MoonshotAI/kimi-cli/issues/2455)  
*Author: KuangYin-Z | Updated: 2026-06-15 | Comments: 0*  
The `FetchURL` tool ignores system proxy configuration (e.g., `HTTP_PROXY`, `HTTPS_PROXY`), causing network requests to fail in censored environments while `curl` and `shell` work fine. **Why it matters:** This blocks adoption in enterprise and certain geographic regions where proxy access is mandatory. No comments yet — community may pick up once awareness grows.

**#2402** — [[bug] Error: [compaction.failed] APIStatusError: 400 — request rejected as high risk](https://github.com/MoonshotAI/kimi-cli/issues/2402)  
*Author: thoughtworld | Updated: 2026-06-16 | Comments: 2*  
User on Windows receives `compaction.failed` + 400 error during compaction, likely triggered by backend risk-detection logic. **Why it matters:** Compaction is critical for long sessions; a hard rejection with no retry mechanism undermines reliability. Two comments suggest the user is probing workarounds but no official response yet.

**#2303** — [UserPromptSubmit hook receives empty prompt from shell UI](https://github.com/MoonshotAI/kimi-cli/issues/2303)  
*Author: AkaCoder404 | Updated: 2026-06-15 | Comments: 1*  
When typing in the interactive shell, `UserPromptSubmit` hook fires with an empty `"prompt"` field, making regex-based hook matching impossible. **Why it matters:** Breaks all custom prompt transformation hooks. A fix PR (#2454) is now open — likely to be merged soon.

**#2222** — [`kimi --continue` reports "No previous session found" despite visible history](https://github.com/MoonshotAI/kimi-cli/issues/2222)  
*Author: LiPingFeel | Updated: 2026-06-15 | Comments: 1*  
On Windows, `kimi --continue` fails even though `kimi` without flags restores the previous session. Root cause: session ID mismatch in `work_directory` lookup. **Why it matters:** Session resumption is a core workflow for iterative coding. PR #2453 addresses this directly.

**#2455** — (listed above) — proxy issue.

**#2402** — (listed above) — compaction rejection.

**#2303** — (listed above) — hook emptiness.

**#2222** — (listed above) — session resume.

*Note: Only 4 issues were active in the last 24h, so selections are limited. No feature requests appeared today.*

---

## Key PR Progress

**#2454** — [fix(hooks): pass prompt text to UserPromptSubmit from structured input](https://github.com/MoonshotAI/kimi-cli/pull/2454)  
*Author: logicwu0 | Updated: 2026-06-15 | Status: Open*  
Fixes #2303. Root cause: `KimiSoul._turn` was deriving hook input incorrectly, yielding empty `prompt`. The patch changes hook text extraction to use the actual user input string. **Impact:** Restores regex-based hook functionality. No comments from maintainers yet — looks ready for review.

**#2453** — [fix(session): resume latest session when last_session_id is missing](https://github.com/MoonshotAI/kimi-cli/pull/2453)  
*Author: logicwu0 | Updated: 2026-06-15 | Status: Open*  
Fixes #2222. Root cause: `Session.continue_` relied entirely on a `work_directory`-scoped session ID, which could be `None` even when sessions exist. The fix falls back to the most recent session for the directory. **Impact:** Restores `--continue` reliability. Another clean, focused fix.

*Note: No other PRs were updated in the last 24h. Both are community-contributed, reflecting strong engagement around core UX bugs.*

---

## Feature Request Trends

No feature requests were active in the last 24 hours. Based on historical patterns (e.g., #2402, #2222), the community is currently focused on **stability and correctness** rather than new capabilities. Common ongoing themes observed from broader issue history include:
- **Better session management** (resumption, multi-session support)
- **Hook extensibility** (ability to intercept all prompt variants)
- **Network resilience** (proxy support, retry on backend rejections)

---

## Developer Pain Points

1. **Backend risk rejection with no fallback** (#2402) — A `400` during compaction kills the session with no recovery. Users on Windows and certain API tiers hit this unpredictably.
2. **Proxy configuration gap** (#2455) — `FetchURL` ignores system environment variables, forcing developers in restricted networks to work around the tool.
3. **Hook data inconsistency** (#2303) — Hooks receiving empty prompts break automation workflows; developers must now wait for the PR merge.
4. **Session resume fragility** (#2222) — `--continue` failing in directories with visible history undermines trust in state persistence.

**Recurring pattern:** Many pain points stem from **environment-specific behaviors** (Windows paths, proxy settings, API risk detection) that lack clear error messages or workarounds — developers want better diagnostics and fallback mechanisms.

---

*Data source: github.com/MoonshotAI/kimi-cli | Generated 2026-06-16*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-16

## Today's Highlights

A major effort to modernize MCP client support is underway, with a key PR merging server-sourced instructions into agent context. The community is rallying around persistent session goals (`/goal`), token-per-second metrics, and sandboxing for terminal agents. Meanwhile, billing activation issues and antivirus false positives are causing friction for new users on OpenCode Go.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **#27167 — [FEATURE]: Add native session goals with /goal**  
   *Author: jorgitin02 | Comments: 49 | 👍: 84*  
   The most upvoted open feature request. Proposes a persistent `/goal` command to set cross-turn session objectives, addressing a gap in OpenCode's otherwise flexible slash command system.  
   [Issue #27167](https://github.com/anomalyco/opencode/issues/27167)

2. **#20695 — Memory Megathread**  
   *Author: thdxr | Comments: 96 | 👍: 65*  
   The highest-traffic open issue. Maintainers are collecting heap snapshots to debug memory leaks across configurations. Strong caution against LLM-suggested fixes.  
   [Issue #20695](https://github.com/anomalyco/opencode/issues/20695)

3. **#2242 — Is there a way to sandbox the agent?**  
   *Author: edmBernard | Comments: 69 | 👍: 53*  
   Persistent demand for restricting agent file access and command scope. Users cite macOS seatbelt equivalents (Gemini CLI, Codex CLI) and want similar protection.  
   [Issue #2242](https://github.com/anomalyco/opencode/issues/2242)

4. **#5374 — [FEATURE]: show tokens / second**  
   *Author: IceWreck | Comments: 17 | 👍: 81*  
   High interest in real-time throughput metrics to compare providers. Perceived as essential for cost and performance optimization.  
   [Issue #5374](https://github.com/anomalyco/opencode/issues/5374)

5. **#6930 — Using OpenCode with Anthropic OAuth violates ToS & Results in Ban**  
   *Author: johnellison | Comments: 22 | 👍: 14*  
   Closed but widely discussed. User reports account ban after OpenCode-initiated Anthropic OAuth flow, raising compliance concerns.  
   [Issue #6930](https://github.com/anomalyco/opencode/issues/6930)

6. **#28567 — [FEATURE]: Full MCP client capabilities**  
   *Author: Arcadi4 | Comments: 14 | 👍: 22*  
   OpenCode's MCP client is flagged as lagging behind the latest spec. This issue tracks gaps in resource handling, instructions, and streaming.  
   [Issue #28567](https://github.com/anomalyco/opencode/issues/28567)

7. **#28957 & #31456 — "Upstream idle timeout exceeded"**  
   *Authors: VENAXIS, gitpilotco | Comments: 14, 4 | 👍: 0, 0*  
   Repeated reports of session timeouts during model inference, particularly with free-tier and slower models. Infrastructure-level concern.  
   [Issue #28957](https://github.com/anomalyco/opencode/issues/28957) | [Issue #31456](https://github.com/anomalyco/opencode/issues/31456)

8. **#19252 — Build command freezes despite completion**  
   *Author: bchstring-glitch | Comments: 10 | 👍: 7*  
   Build execution finishes but the agent stalls, unable to proceed. Common pattern with multi-step workflows.  
   [Issue #19252](https://github.com/anomalyco/opencode/issues/19252)

9. **#21345 — Move git/PR instructions out of bash tool description**  
   *Author: DrDexter6000 | Comments: 3 | 👍: 9*  
   Detailing ~1.7K tokens of boilerplate per request. Signals growing awareness of token budget waste in default tool descriptions.  
   [Issue #21345](https://github.com/anomalyco/opencode/issues/21345)

10. **#32420 — Paid Go subscription charged but not activated**  
    *Author: JN-ANC | Comments: 3*  
    Multiple identical reports. Billing system may be missing activation hooks for OpenCode Go subscriptions.  
    [Issue #32420](https://github.com/anomalyco/opencode/issues/32420)

## Key PR Progress

1. **#32490 — feat(mcp): append server instructions to context**  
   *Author: Arcadi4*  
   Implements MCP `InitializeResult.instructions` injection into agent context. Part of the larger MCP revision, refs #28567.  
   [PR #32490](https://github.com/anomalyco/opencode/pull/32490)

2. **#32499 — fix(opencode): allow clearing session archive time**  
   *Author: doctorbruce*  
   Adds ability to un-archive sessions (closes #24153). Addresses pain point for long-lived projects.  
   [PR #32499](https://github.com/anomalyco/opencode/pull/32499)

3. **#32494 — fix(opencode): include pr identity in github context**  
   *Author: wgu9*  
   Adds PR number and URL to `opencode github run` contexts, enabling PR-comment runs to reference themselves. Fixes #32233.  
   [PR #32494](https://github.com/anomalyco/opencode/pull/32494)

4. **#29150 — fix(opencode): break auto-compact loop when compaction makes no progress**  
   *Author: ZehuaWang*  
   Prevents infinite auto-compaction when provider context limits exceed model.dev specs. Closes #28543.  
   [PR #29150](https://github.com/anomalyco/opencode/pull/29150)

5. **#32489 — fix(opencode): sanitize OpenAI MCP tool schemas**  
   *Author: jquense*  
   Strips JSON Schema keywords unsupported by OpenAI tool schemas, preventing crashes when MCP servers expose non-standard schemas. Closes #32488.  
   [PR #32489](https://github.com/anomalyco/opencode/pull/32489)

6. **#31645 — feat(cli): add progress feedback to upgrade command**  
   *Author: szzhoujiarui-sketch*  
   Real-time progress messages during `opencode upgrade` download/install. Addresses UX gap where the command appeared to hang. Closes #31623.  
   [PR #31645](https://github.com/anomalyco/opencode/pull/31645)

7. **#31644 — fix(acp): register compact and summarize commands for visibility**  
   *Author: szzhoujiarui-sketch*  
   `/compact` and `/summarize` now appear in autocomplete and `/help`. Previously hidden despite being functional. Closes #31636.  
   [PR #31644](https://github.com/anomalyco/opencode/pull/31644)

8. **#28466 — fix(opencode): ignore MCP resource file downloads**  
   *Author: Arcadi4* (closed)  
   Prevents unwanted file downloads when MCP resources are mentioned. Closes three linked issues (#14753, #8920, #29245).  
   [PR #28466](https://github.com/anomalyco/opencode/pull/28466)

9. **#32487 — feat: configure cost display currency**  
   *Author: dingskyhi*  
   Adds `display.currency`, `display.cost_currency`, and `display.currency_rate` config keys. Lets users see usage costs in their local currency. Closes #32485.  
   [PR #32487](https://github.com/anomalyco/opencode/pull/32487)

10. **#29006 — docs(ecosystem): add opencode-datarobot-skills plugin**  
    *Author: carsongee*  
    Ecosystem listing for DataRobot's opencode skill pack. Signals growing third-party skill ecosystem.  
    [PR #29006](https://github.com/anomalyco/opencode/pull/29006)

## Feature Request Trends

- **Session lifecycle management**: `/goal` for persistent objectives (highly upvoted), un-archive support, pending-review status icons.
- **MCP parity**: Full spec adherence (resources, instructions, streaming)—a top integration concern.
- **Observability**: Tokens/second, cost display in local currency, token budget analysis.
- **Sandboxing & permissions**: File system restrictions, command whitelisting, session-level isolation (recurring theme across many issues).
- **Provider flexibility**: Missing model variants (Kimi models), better custom provider token handling.

## Developer Pain Points

- **Memory leaks & compaction loops**: Long-standing memory megathread (#20695) and PR #29150 highlight core stability issues that affect all users.
- **Billing & activation failures**: Multiple reports of OpenCode Go subscription charges without activation (#32420, #32482, #32466), plus confirmed billing after tab close (#32471).
- **Build execution stalls**: The agent frequently freezes after command completion (#19252, #22154, #22767), especially with Gradle and Playwright.
- **Idle timeout errors**: Upstream connection timeouts when using slower/free models (#28957, #31456) degrade user experience.
- **Encoding issues on non-UTF-8 systems**: Hardcoded UTF-8 decoding in bash.ts causes garbled output on Windows CJK locales (#30869).
- **Desktop UI freezes**: Markdown AST traversal blocks UI thread on startup (#32452), and missing scrollbar in chat (#32467).

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-16

## Today's Highlights
Pi's v0.79.4 release ships automatic first-run theme detection, a quality-of-life win for new users. Meanwhile, the community is converging around reliability: a high-profile OpenAI Codex connection hang (57 comments, 30 👍) dominates discussion, and multiple closed PRs today address crash fixes in process handling, TUI rendering, and extension API promises. The long-running Shrinkwrap deduplication issue (#5653) remains in progress, signaling architectural work still underway.

## Releases
**v0.79.4** — [Release Link](https://github.com/earendil-works/pi/releases/tag/v0.79.4)
- **Automatic first-run theme selection**: pi now detects terminal background on first launch and defaults to `dark` or `light` theme. See [theme docs](https://github.com/earendil-works/pi/blob/v0.79.4/packages/coding-agent/docs/themes.md).
- **Standalone binary improvements** (details in release notes).

---

## Hot Issues (Top 10 Notable)

1. **[#4945] OpenAI Codex Connection Reliability** (OPEN, 57 comments, 30 👍)  
   *`gpt-5.5` leaves TUI stuck on `Working...` with no stream, tool call, or error; only Escape recovers.*  
   Most-voted issue. Signals systemic LLM streaming reliability concerns.  
   [Link](https://github.com/earendil-works/pi/issues/4945)

2. **[#5103] Windows: git-bash not detected from PATH in zip build** (OPEN, 21 comments)  
   *`pi.exe` from GitHub release can't find Git Bash even when on PATH.*  
   Ongoing Windows onboarding friction. Community is actively diagnosing PATH discovery logic.  
   [Link](https://github.com/earendil-works/pi/issues/5103)

3. **[#4877] Session folder collision** (OPEN, 15 comments, 2 👍)  
   *Paths like `/a/b/c/d` and `/a-b/c-d` collide into identical session folder names.*  
   Subtle but impactful design defect; could cause silent data confusion.  
   [Link](https://github.com/earendil-works/pi/issues/4877)

4. **[#5363] Add Amazon Bedrock Mantle provider** (OPEN, 13 comments, 3 👍)  
   *Request for new provider using OpenAI-compatible Bedrock Mantle API.*  
   Community-driven provider expansion continues.  
   [Link](https://github.com/earendil-works/pi/issues/5363)

5. **[#5653] Move off Shrinkwrap** (OPEN, 10 comments)  
   *Duplicate `pi-ai` copies on disk due to npm hoisting; module-level `Map` registry breaks.*  
   Architectural debt — key maintainability issue with dependency deduplication.  
   [Link](https://github.com/earendil-works/pi/issues/5653)

6. **[#5728] Support provider-specific config in auth.json** (OPEN, 6 comments)  
   *Providers like Cloudflare AI Gateway need `accountId`/`gatewayId` beyond API keys.*  
   Multi-provider config management is becoming a pain point.  
   [Link](https://github.com/earendil-works/pi/issues/5728)

7. **[#5785] `--min-release-age=0` npm flag during updates** (CLOSED, 2 comments)  
   *Flag overrides npm's supply-chain protection; community called it "a very VERY bad idea."*  
   Triggered immediate pushback; quickly closed but signals security sensitivity.  
   [Link](https://github.com/earendil-works/pi/issues/5785)

8. **[#5687] `pi list` / `pi update` hang when extension runs MCP server** (CLOSED, 7 comments)  
   *Commands never exit because long-lived MCP server keeps process alive.*  
   Package management UX bug with extension lifecycle implications.  
   [Link](https://github.com/earendil-works/pi/issues/5687)

9. **[#5736] Escape no longer interrupts active task** (CLOSED, 7 comments)  
   *UI advertises Escape as cancel, but keybind doesn't reliably stop agent execution.*  
   Core UX regression caught and fixed quickly.  
   [Link](https://github.com/earendil-works/pi/issues/5736)

10. **[#5463] Auto-compaction after final turn throws error** (OPEN, 2 comments, 5 👍)  
    *`agent.continue()` crashes when last message is assistant role.*  
    High signal-to-noise ratio; compaction logic still fragile.  
    [Link](https://github.com/earendil-works/pi/issues/5463)

---

## Key PR Progress (Top 10)

1. **[#5789] fix(tui): restore cursorUp start-of-line jump** (OPEN)  
   *Regressed fix for #5494; pressing Up on first non-empty line now re-opens history instead of jumping to start-of-line.*  
   [Link](https://github.com/earendil-works/pi/pull/5789)

2. **[#5675] fix: stabilize compaction after reload** (CLOSED)  
   *Preserves token boundaries across repeated compactions; fixes queued message delivery after reload.*  
   [Link](https://github.com/earendil-works/pi/pull/5675)

3. **[#5784] fix(coding-agent): sort threaded sessions by latest subtree activity** (OPEN)  
   *Sessions in Threaded mode now sort by latest descendant activity, not root modification date.*  
   [Link](https://github.com/earendil-works/pi/pull/5784)

4. **[#5779] feat(coding-agent): XML-structured /review prompt responses** (CLOSED)  
   *Converts `/review` to XML instruction envelopes with coverage-aware workflows.*  
   [Link](https://github.com/earendil-works/pi/pull/5779)

5. **[#5776] Fix: agent wedge on unresponsive streams & tool executions** (CLOSED)  
   *Addresses indefinite hangs when LLM stream stops without closing or tool `execute()` never resolves.*  
   [Link](https://github.com/earendil-works/pi/pull/5776)

6. **[#5758] feat(coding-agent): diagnose when child holds stdio open past exit** (CLOSED)  
   *Follow-up to #5753; detects detached descendants keeping stdout open after shell exits.*  
   [Link](https://github.com/earendil-works/pi/pull/5758)

7. **[#5753] fix: drain stdout before resolving when child holds pipe past exit** (CLOSED)  
   *Fixes #5303; ensures data written >100ms after exit isn't lost.*  
   [Link](https://github.com/earendil-works/pi/pull/5753)

8. **[#5509] feat: Add Amazon Bedrock Mantle OpenAI Responses provider** (OPEN)  
   *New provider supporting GPT 5.5/5.4 via Bedrock Mantle's OpenAI-compatible API.*  
   [Link](https://github.com/earendil-works/pi/pull/5509)

9. **[#5765] feat(d-pi): split createDPiExtension into remote-executor and multi-agent extensions** (CLOSED)  
   *Decomposes monolithic extension into two focused, independently registrable extensions.*  
   [Link](https://github.com/earendil-works/pi/pull/5765)

10. **[#5743] refactor(ai): decompose generate-models.ts into data-driven generator** (CLOSED)  
    *Follows #5702; replaces sprawling `if/else` with data-driven model registry.*  
    [Link](https://github.com/earendil-works/pi/pull/5743)

---

## Feature Request Trends

- **Provider expansion**: Repeated requests for new AI providers (Amazon Bedrock Mantle, Z.AI CN, Gemini 3.5 Flash on Vertex) — community wants pi to support any OpenAI-compatible endpoint.
- **Extension API maturity**: Requests to expose internal tools (`generateDiffString`, `generateUnifiedPatch`) and fix async behavior (`sendUserMessage`/`sendMessage` returning non-awaited Promises).
- **Config flexibility**: Demand for provider-specific config in `auth.json` (beyond API keys) and environment-variable overrides for truncation limits.
- **Security & supply chain**: Strong sensitivity to npm flags that bypass release-age protections; requests for SHA256SUMS and provenance attestations on binary releases.
- **OAuth customization**: Users want custom callback page rendering for OAuth flows.

---

## Developer Pain Points

- **LLM streaming reliability** (#4945, #5776): Silent hangs with `Working...` spinner and no error output remain the most-upvoted frustration. Community is actively patching timeout and drain logic.
- **Windows support gaps** (#5103): Git Bash detection from PATH remains broken in standalone zip builds — a blocker for Windows adoption.
- **Process lifecycle edge cases** (#5687, #5736, #5753, #5758): Extensions with long-lived MCP servers cause commands to hang; Escape keybind doesn't reliably interrupt; child processes with delayed stdout output trigger crashes or data loss.
- **Dependency deduplication** (#5653, #5782): Shrinkwrap causes duplicate package copies and broken module-level registries; floating AWS SDK ranges cause enterprise installation failures.
- **Session management fragility** (#4877, #5463, #5675): Folder collisions, auto-compaction crashes, and post-reload failures erode trust in session persistence.
- **Security posture** (#5785, #5739): Community immediately flags insecure defaults (`--min-release-age=0`); demand for verifiable binary integrity.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**Date:** 2026-06-16

## Today's Highlights
The Qwen Code team shipped **v0.18.1** with a critical fix for oversized context warnings, while the CLI saw a flurry of activity around the new **`/loop` command ecosystem** for background automation. On the bug front, two significant UI issues—a virtualized history mode rendering problem and trackpad scrolling conflicts in tmux—garnered community attention. The desktop app also reached **v0.0.4**, fixing MCP server persistence and model defaults refresh.

## Releases

- **[v0.18.1-nightly.20260616.a68b2e1e7](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.1-nightly.20260616.a68b2e1e7)**: Nightly build with a fix for oversized context instructions ([#5073](https://github.com/QwenLM/qwen-code/pull/5073)) and documentation updates for stale defaults and CLI syntax.
- **[v0.18.1](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.1)**: Stable release including a new daemon feature that gates direct session shell behind explicit opt-in ([@doudouOUC](https://github.com/doudouOUC)), enhancing security by preventing unintended shell access.
- **[desktop-v0.0.4](https://github.com/QwenLM/qwen-code/releases/tag/desktop-v0.0.4)**: Desktop app update fixing MCP server removal persistence ([#4535](https://github.com/QwenLM/qwen-code/pull/4535)) and refreshing raw model-derived defaults ([@Jerry2003826](https://github.com/Jerry2003826)).

## Hot Issues

1. **[#5142 – bug(cli): Virtualized History Mode where history is not visible](https://github.com/QwenLM/qwen-code/issues/5142)** — Users report that CLI history only appears when pressing the slash key, otherwise the interface appears empty. High community engagement (4 comments) with implications for basic usability.

2. **[#5160 – bug(cli): /model lists discontinued qwen-oauth coder-model even when OAuth is not configured](https://github.com/QwenLM/qwen-code/issues/5160)** — A confusing UX issue where discontinued models appear in the model picker despite the user having no OAuth setup. Community suggests it misleads new users about available models.

3. **[#5173 – Model provider disambiguation fails when multiple providers share the same model id](https://github.com/QwenLM/qwen-code/issues/5173)** — When multiple providers (e.g., Token Plan, IdeaLab) register models with the same `id` like `qwen3.7-max`, the selection does not persist across sessions. This is a critical configuration bug for users chaining multiple API providers.

4. **[#5147 – OOM after /quit when managed auto-memory builds transcript from large text-only history](https://github.com/QwenLM/qwen-code/issues/5147)** — Even with previous OOM fixes in place, short sessions can crash after `/quit` due to managed auto-memory background tasks. The issue points to persistent memory management challenges.

5. **[#5177 – exit_plan_mode fails with empty plan parameter, causing wasted retry turns](https://github.com/QwenLM/qwen-code/issues/5177)** — A plan-mode workflow bug where the model calls `exit_plan_mode` without parameters, causing wasted LLM retry turns. This is a productivity drain for users relying on planning features.

6. **[#3979 – plan mode causes continuous screen flickering in Ghostty terminal](https://github.com/QwenLM/qwen-code/issues/3979)** — Long-standing UI bug persisting across versions, particularly affecting macOS terminal emulators. User frustration is evident with 2 comments and no resolution yet.

7. **[#5159 – Trackpad scroll in tmux session triggers prompt history navigation instead of viewport scrolling](https://github.com/QwenLM/qwen-code/issues/5159)** — macOS users running Qwen Code inside tmux cannot scroll conversation history with trackpad gestures, making long conversations difficult to navigate.

8. **[#4966 – SchemaValidator missing numeric string coercion causes MCP tool failures](https://github.com/QwenLM/qwen-code/issues/4966)** — MCP tool calls fail because LLMs emit numeric parameters as strings (e.g., `"depth": "3"` instead of `3`), causing strict MCP servers to reject valid actions. A significant blocker for tool-heavy workflows.

9. **[#5119 – When the agent wants to run a sudo command there is no way to allow it](https://github.com/QwenLM/qwen-code/issues/5119)** — Agents cannot handle `sudo` commands gracefully, failing and forcing users to copy-paste. This is a frequent frustration for developers managing system-level operations.

10. **[#3153 – Cannot stop Qwen after you reject a command](https://github.com/QwenLM/qwen-code/issues/3153)** — After rejecting a command, the agent repeatedly attempts the same action without allowing termination, creating an infinite loop. This has been open since April with persistent user impact.

## Key PR Progress

1. **[#5094 – feat(core+cli): Workflow P4 — meta + /workflows + phase-tree](https://github.com/QwenLM/qwen-code/pull/5094)** — Landmark PR completing Phase 4 of the Dynamic Workflows port. Adds meta extraction, `/workflows` command, and phase-tree visualization for complex automated pipelines.

2. **[#5148 – feat(loop): align /loop command surface and add task-file reader](https://github.com/QwenLM/qwen-code/pull/5148)** — First slice of the `/loop` alignment work, adding a task-file reader and `proactive` alias. Foundation for background automation without cron dependencies.

3. **[#5175 – feat(daemon): deliver web-shell mid-turn messages into the running turn](https://github.com/QwenLM/qwen-code/pull/5175)** — Enables real-time mid-turn interaction in web-shell, allowing users to inject messages while a model turn is still executing—reducing latency in interactive workflows.

4. **[#4850 – feat(extensions): interactive multi-tab /extensions manager](https://github.com/QwenLM/qwen-code/pull/4850)** — Major UX improvement replacing the flat read-only extension list with interactive tabs for Installed, Discover, and Sources, covering the full extension lifecycle.

5. **[#5171 – fix(core): auto-retry transport stream errors before the first chunk](https://github.com/QwenLM/qwen-code/pull/5171)** — Adds bounded automatic retry for transient stream drops before any data is received, reducing silent failures in poor network conditions.

6. **[#5155 – fix(agent): make forking explicit; keep omitted subagent_type awaitable](https://github.com/QwenLM/qwen-code/pull/5155)** — Fixes agent behavior where models were forking instead of awaiting results. Now `subagent_type: "fork"` is required for forking, preventing accidental parallel execution.

7. **[#5145 – feat(cli): show follow-up suggestion in input placeholder](https://github.com/QwenLM/qwen-code/pull/5145)** — Uses the fast model to generate follow-up suggestions shown in the input placeholder after each response, improving prompt engineering flow.

8. **[#5174 – feat(cli): Add daemon status API](https://github.com/QwenLM/qwen-code/pull/5174)** — Implements a read-only `GET /daemon/status` endpoint exposing runtime metrics (session counts, rate-limit rejects, transport counts) for monitoring and debugging.

9. **[#4918 – feat(hooks): pass original API call ID (toolCallId) to hook system](https://github.com/QwenLM/qwen-code/pull/4918)** — Threads the LLM provider's `tool_call_id` through all hook interfaces, enabling correlation between tool calls and their outcomes—critical for debugging and observability.

10. **[#5141 – fix(core): Track supported sed edits in file history](https://github.com/QwenLM/qwen-code/pull/5141)** — Treats a safe subset of single-file `sed -i` commands as normal edit confirmations instead of opaque shell executions, enabling file history tracking for these common operations.

## Feature Request Trends

The dominant theme is **background automation and loop capabilities**. Multiple feature requests ([#5124](https://github.com/QwenLM/qwen-code/issues/5124), [#5129](https://github.com/QwenLM/qwen-code/issues/5129), [#5130](https://github.com/QwenLM/qwen-code/issues/5130), [#5131](https://github.com/QwenLM/qwen-code/issues/5131)) focus on building a comprehensive `/loop` framework with self-paced scheduling, task-file support, cancellation, and status feedback—enabling agents to run continuous monitoring or maintenance tasks without cron.

A secondary trend is **token and memory optimization** ([#4941](https://github.com/QwenLM/qwen-code/issues/4941), [#5132](https://github.com/QwenLM/qwen-code/issues/5132)), with users requesting context-window-aware file warnings and token-efficient loop templates to avoid repeatedly resending unchanged content.

There is rising interest in **sub-agent parallel execution controls** ([#5176](https://github.com/QwenLM/qwen-code/issues/5176)) and **persistent model provider disambiguation** ([#5173](https://github.com/QwenLM/qwen-code/issues/5173)), suggesting users are running increasingly complex multi-provider setups.

## Developer Pain Points

1. **Terminal/UI flickering issues** — Multiple reports ([#3979](https://github.com/QwenLM/qwen-code/issues/3979), [#3949](https://github.com/QwenLM/qwen-code/issues/3949)) describe continuous screen flickering in Ghostty and Tabby terminals, particularly in plan mode. The issue spans versions and has no clear resolution timeline.

2. **Memory management failures** — Despite fixes for `/quit`-related OOM ([#4644](https://github.com/QwenLM/qwen-code/issues/4644), [#4717](https://github.com/QwenLM/qwen-code/issues/4717)), new cases emerge ([#5147](https://github.com/QwenLM/qwen-code/issues/5147)) where managed auto-memory background tasks cause heap overflow even on short sessions.

3. **Unkillable agent loops** — Issues [#3153](https://github.com/QwenLM/qwen-code/issues/3153) and [#5119](https://github.com/QwenLM/qwen-code/issues/5119) highlight a class of problems where rejected commands or failed actions cause the agent to repeat the same action endlessly without termination options.

4. **Model provider configuration confusion** — The combination of OAuth-related stale model listings ([#5160](https://github.com/QwenLM/qwen-code/issues/5160)) and provider disambiguation failures ([#5173](https://github.com/QwenLM/qwen-code/issues/5173)) creates a frustrating user experience for anyone managing multiple API providers.

5. **Terminal emulator compatibility** — Mac-specific issues with trackpad scrolling in tmux ([#5159](https://github.com/QwenLM/qwen-code/issues/5159)), Tabby flickering, and Ghostty rendering problems suggest the CLI's terminal handling lacks robust cross-emulator compatibility.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-16

## Today's Highlights
No new releases were cut in the last 24 hours, but the community remains highly active with 50 open issues and 50 PRs in motion. Key developments center on **sub-agent reliability** (stalled turns, timeout fixes, and worker runtime refactoring) and **provider ecosystem expansion** (DeepInfra, Atlas Cloud, and Agent Client Protocol registry integration). The maintainer is actively closing out release-blocker issues while addressing long-standing Windows TUI freeze bugs and configuration persistence improvements.

## Releases
*No new releases in the last 24 hours.*  
Latest stable version remains **v0.8.62** (previous release v0.8.61). Several high-priority issues are tagged `v0.8.61` and `v0.8.62`, suggesting a patch release may be imminent.

---

## Hot Issues — Top 10 Noteworthy

### 1. [Stalled Turn — No Completion Signal](https://github.com/Hmbown/CodeWhale/issues/2487) (#2487) 🔥
**Why it matters:** A critical bug in `yolo` mode where operations freeze with no recovery path. Even sending `continue` fails. This is the **most commented issue** (13 comments) and affects the core user experience for power users relying on autonomous mode. The community is actively debugging the completion signal mechanism.

### 2. [TUI Mouse-Report Leak & Runtime Safety (Release Tracker)](https://github.com/Hmbown/CodeWhale/issues/3063) (#3063)
**Why it matters:** This closed release-blocker for v0.8.59 documents a macOS TUI input leak (mouse-report) and the maintainer's triage process. The fix is already shipped, but the issue serves as a reference for similar input-layer bugs.

### 3. [Typed Persistent Permission Rules](https://github.com/Hmbown/CodeWhale/issues/1186) (#1186)
**Why it matters:** A high-impact enhancement (9 comments) adding persistent permission rules scoped by tool name, command prefix, and path pattern. This is essential for production deployment where users need `allow`/`deny`/`ask` policies that survive restarts. Tagged for both v0.9.0 and v0.8.61.

### 4. [v0.8.61: Split Sub-Agents into Headless Worker Runtime](https://github.com/Hmbown/CodeWhale/issues/3096) (#3096)
**Why it matters:** A major architectural refactor to decouple sub-agents from the TUI, making them leaner async tasks instead of UI-shaped processes. The community (8 comments) recognizes this as foundational for scaling multi-agent workflows without terminal bloat.

### 5. [Agent Client Protocol / Registry Listing](https://github.com/Hmbown/CodeWhale/issues/3192) (#3192)
**Why it matters:** Community members want DeepSeek TUI listed on the Agent Client Protocol registry to enable seamless installation from editors like Zed. This reflects growing demand for **editor-agnostic AI tooling integration**.

### 6. [TUI Freeze on Windows (crossterm poll)](https://github.com/Hmbown/CodeWhale/issues/1812) (#1812)
**Why it matters:** A **persistent Windows 11 bug** (6 comments, long-running since v0.8.39) where the terminal UI becomes completely unresponsive while the process stays alive. The maintainer has confirmed with thread-state analysis, making this a priority for cross-platform parity.

### 7. [Provider Fallback Chain](https://github.com/Hmbown/CodeWhale/issues/2574) (#2574)
**Why it matters:** Users want automatic failover between providers (e.g., DeepSeek → OpenRouter) when API quota is exhausted or errors occur. Currently requires manual `/provider` switching. This is the **most popular enhancement request** for reliability in multi-provider setups.

### 8. [Clarification Question Requests for Agents](https://github.com/Hmbown/CodeWhale/issues/3102) (#3102)
**Why it matters:** Proposes giving agents a first-class UI mechanism to ask users clarifying questions instead of burying them in chat. This would fundamentally improve agent-user interaction for ambiguous tasks. Part of a larger UX reliability push.

### 9. [Telemetry — Token/Resource Usage Visibility](https://github.com/Hmbown/CodeWhale/issues/2666) (#2666)
**Why it matters:** During long-running tasks, agents lack visibility into token budgets, context window pressure, and API costs. This is crucial for power users running expensive multi-agent orchestrations who need real-time feedback to avoid silent failures.

### 10. [SiliconFlow & Tencent TokenHub 401 Auth Error](https://github.com/Hmbown/CodeWhale/issues/2629) (#2629)
**Why it matters:** A Chinese user base blocker — deep-tui fails with `401 invalid api key` against SiliconFlow and Tencent TokenHub despite correct OpenAI-compatible configuration. Highlights the need for broader provider compatibility testing.

---

## Key PR Progress — Top 10 Important

### 1. [Provider Metadata Registry Refactor](https://github.com/Hmbown/CodeWhale/pull/3005) (#3005)
**Summary (CLOSED):** Extracts provider metadata into a static `PROVIDER_REGISTRY`, eliminating ~100 hand-maintained match arms. This is a **foundational refactor** that makes adding new providers trivial (`provider!()` macro).

### 2. [Retry Release Lookups & Downloads](https://github.com/Hmbown/CodeWhale/pull/3244) (#3244)
**Summary (CLOSED):** Adds retry logic for transient GitHub release metadata and asset-download failures. Includes fallback from REST API to public redirect URLs — critical for automated CI/CD and user upgrade reliability.

### 3. [DeepInfra Provider Support](https://github.com/Hmbown/CodeWhale/pull/3235) (#3235)
**Summary (CLOSED):** Adds DeepInfra as a supported provider (100+ open-source models including DeepSeek V4). OpenAI-compatible API. This expands the provider ecosystem significantly for cost-sensitive users.

### 4. [Atomically Persist Ask-Only Permission Rules](https://github.com/Hmbown/CodeWhale/pull/3233) (#3233)
**Summary (CLOSED):** Adds `ConfigStore::append_ask_rules` for persisting typed permission rules without changing approval semantics. Foundation work for the larger persistent permissions feature (#1186).

### 5. [App-Server as Canonical Runtime API Entrypoint](https://github.com/Hmbown/CodeWhale/pull/3257) (#3257)
**Summary (CLOSED):** Makes `codewhale app-server --http` the canonical entrypoint, delegating to the existing `serve` path. Adds smoke tests and fixes some control surface issues. This paves the way for headless/mobile operation.

### 6. [Workspace Follow Symlinks Setting](https://github.com/Hmbown/CodeWhale/pull/3242) (#3242)
**Summary (OPEN):** Adds `workspace_follow_symlinks` configuration so walk-based tools follow symlinks during directory traversal. Important for monorepo and NixOS environments.

### 7. [WeChat Bridge via Feishu + Tencent OpenClaw](https://github.com/Hmbown/CodeWhale/pull/3206) (#3206)
**Summary (CLOSED):** Leverages the existing Feishu bridge to add a WeChat bridge, allowing users to interact with CodeWhale from their messaging infrastructure. Demonstrates strong community interest in **chat-based AI tooling**.

### 8. [Atlas Cloud Provider Documentation](https://github.com/Hmbown/CodeWhale/pull/3239) (#3239)
**Summary (OPEN):** Docs-only PR adding Atlas Cloud (59 models) as an OpenAI-compatible backend. Quick-start configuration and logo. Another sign of **rapid provider ecosystem growth**.

### 9. [i18n Phase 1-4b Wiring](https://github.com/Hmbown/CodeWhale/pull/2239) (#2239)
**Summary (OPEN):** Large PR (47 files, 1059 lines) wiring MessageId translations into the UI layer. Fixes 109 compile errors from upstream rebase. This is **critical for non-English user adoption**, especially the growing Chinese user base.

### 10. [Harvest-Credit Close Template + Stewardship Docs](https://github.com/Hmbown/CodeWhale/pull/2986) (#2986)
**Summary (CLOSED):** Process improvement — formalizes a harvest-credit close template that credits contributors even when PRs are merged piecemeal. Important for **community health and contributor retention**.

---

## Feature Request Trends

The following **feature directions** emerge from cross-cutting analysis of all 50+ open issues:

1. **Provider Ecosystem Expansion** (most active)
   - Automatic fallback chains across providers (#2574)
   - Dynamic API key resolution via scripts (#3004)
   - Agent Client Protocol registry integration (#3192)
   - New provider support: DeepInfra (#3235), Atlas Cloud (#3239), Moonshot/Kimi (#3265)

2. **Sub-Agent & Multi-Agent Reliability** (highest pain)
   - Headless worker runtime to avoid TUI bloat (#3096)
   - Checkpoint/restart for mid-turn child work (#2029)
   - Visible token/resource telemetry (#2666)
   - Permission inheritance for sub-agents (#414)

3. **Configuration & Persistence Improvements**
   - Typed persistent permission rules (#1186)
   - Symlink-aware file operations (#3242)
   - Scoped skill scanning (#3264)

4. **Internationalization & Accessibility**
   - Full i18n Phase 1-4b (#2239)
   - Chinese user support for local providers (#2629)

5. **Agent-User Interaction**
   - Clarification question UI (#3102)
   - Mid-turn intervention in Agent mode (#874)

---

## Developer Pain Points

| Pain Point | Frequency | Affected Versions | Key Issue |
|---|---|---|---|
| **Stalled turns / frozen TUI** | Very High (20% of bug reports) | v0.8.39–v0.8.61 | #2487, #2739, #1812 |
| **Sub-agent timeout (120s ceiling)** | High (10% of bug reports) | v0.8.39–v0.8.61 | #1806, #1679 |
| **Provider authentication failures** | Medium (non-standard providers) | v0.8.50–v0.8.60 | #2629, #3265 |
| **Blocked tool cancellation** | Medium (long-running sync ops) | v0.8.61 | #1791 |
| **Configuration security** | Medium (plaintext API keys) | All | #3004 |
| **CLI/scripting integration gaps** | Low but growing | v0.8.60+ | #3192, #3242 |
| **No mid-turn intervention** | Low (specific to Agent mode) | v0.8.61 | #874 |
| **glibc compatibility** | Low (Linux server deployment) | v0.8.61 | #1067 |

**Recurring theme:** The most frustrating bugs are **silent failures** — stalls with no error messages, timeouts without retries, and UI freezes without crash logs. The community strongly desires **observability improvements** (token usage, resource telemetry, visible agent state) to diagnose these issues rather than blind workarounds.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*