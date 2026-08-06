# AI CLI Tools Community Digest 2026-08-06

> Generated: 2026-08-06 01:16 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem Cross-Comparison Report — 2026-08-06

---

## 1. Ecosystem Overview

The AI CLI tool landscape has entered a **stabilization-and-hardening phase**, where feature velocity is balanced against reliability, security, and cost concerns. Across all seven major tools, the dominant themes are **false-positive safety filtering** (Claude Code, Codex, Qwen Code), **session/daemon reliability** (all tools), **MCP ecosystem maturity** (Claude Code, Copilot CLI, Kimi, OpenCode), and **cost guardrails** (Claude Code, Codex, Pi). The release cadence varies significantly: Claude Code ships stable releases continuously, Codex iterates rapidly on alpha builds, while Gemini CLI, Pi, Kimi, and DeepSeek TUI are in regression-fix and API-expansion phases. The emergence of cross-tool patterns — such as the "interrupted by user" error being misused for watchdog aborts (Claude Code) and parallel sub-agent reliability concerns (Gemini CLI, Qwen Code) — indicates that the industry is converging on similar architectural patterns (sub-agents, background jobs, MCP, session portability) and therefore facing similar failure modes. Notably, **security/trust issues** are the fastest-growing frustration cluster across Claude Code, Codex, Qwen Code, and Gemini CLI, suggesting this is the next battleground for differentiation.

---

## 2. Activity Comparison (as of 2026-08-06)

| Tool | Hot Issues (active) | Key PRs | Release Status | Notable New Issues |
|---|---|---|---|---|
| **Claude Code** | 10 (3 new) | 9 | **v2.1.223 stable** | 3x security-downgrade reports, $411 unintended API charges |
| **OpenAI Codex** | 10 (1 new) | 10 | **rust-v0.146.1 stable** + 8 alpha builds (v0.147.0-alpha.6→13) | Cyber-safety false positives (#37161) |
| **Gemini CLI** | 10 (0 new) | 8 (5 merged) | No new release; post-v0.53.0 regression fixes | — |
| **GitHub Copilot CLI** | 10 (7 new) | 0 (no PRs updated) | **v1.0.79-2/-3/-4 pre-release** | MCP init failures, Azure DevOps remote 400s, model-delegation bypass |
| **Kimi Code CLI** | 4 (3 new) | 4 (2 critical fixes) | No new release | Image-tool abort mid-task, UTF-8 corruption bug |
| **OpenCode** | 10 (1 new) | 10 | **v1.18.14 stable** (regression suspected) | Session-history wipe regression (#40759) |
| **Pi** | 10 (0 new) | 10 | No new release; fix wave merged | — |
| **Qwen Code** | 10 (0 new) | 10+ | **desktop-v0.1.0** + v0.21.6 stable + nightly | Read-only shell classifier bypass (P1 security) |
| **DeepSeek TUI** | 3 (0 new) | 14 | **v0.9.4 in integration train** (77 commits, RC) | Silent 128K context-window fallback |

**Key observations:**
- **Codex** has the most aggressive release cadence (8 alpha builds in 24 hours), indicating active feature iteration.
- **Copilot CLI** and **Qwen Code** have the highest volume of newly filed triage-level issues (7 and ~6 respectively), suggesting growing user bases in expansion phases.
- **DeepSeek TUI** has the most PRs per issue, indicating a focused engineering push (likely toward the v0.9.4 release).

---

## 3. Shared Feature Directions (Cross-Tool Requirements)

### A. Cost Control & Usage Transparency
- **Claude Code**: $411 unintended API charge (#84350) → implicit demand for budget guardrails.
- **Codex**: 600M token/day consumption spikes (#32309), unbounded image payloads in compaction (#33493).
- **Pi**: Dedicated thinking-level control for compaction (separate from session) (#7553).
- **OpenCode**: Usage/balance API endpoint (#16017, 126👍) for programmatic cost tracking.

### B. Session Portability & Resume Reliability
- **Claude Code**: `--continue` can't find headless sessions (#82536); portable session transcripts (#81946).
- **Codex**: Harden named session lookup in TUI (#37157).
- **OpenCode**: Cross-project session picker (#31932); sessions wiping history (#40759).
- **Pi**: Ephemeral in-session model changes (#5263).
- **Kimi CLI**: Persistent memory across sessions (#1283, 19 comments).
- **All tools**: Reliable resume of background/detached agents.

### C. MCP Ecosystem Maturity
- **Claude Code**: Marketplace management, owner-wildcard repo blocking.
- **Codex**: OAuth parity across platforms (#34684), handshake timeouts (#37168), tool namespace reservation (#37188).
- **Copilot CLI**: OAuth 3LO support (#4371); MCP policy enforcement failures on GHEC (#4378); FastMCP `server/discover` handling (#4370).
- **Kimi CLI**: Image-returning MCP tools abort mid-task (#2588).
- **DeepSeek TUI**: MCP server configuration API over HTTP (#5130).
- **Qwen Code**: SSE server hangs when no `endpoint` event (#8550).

### D. Sub-Agent Reliability & Transparency
- **Claude Code**: Subagent watchdog aborts mislabeled (`#84346`).
- **Codex**: Orchestrator skills in world state to save context (#37149).
- **Gemini CLI**: Generalist-agent hangs (#21409, 8👍); MAX_TURNS misreported as success (#22323); subagents running without permission (#22093).
- **Qwen Code**: tmux-backed interactive terminal sub-agents (PR #8613); parallel sub-agent status UI (PR #8559).
- **DeepSeek TUI**: Checkpoint-based resume of interrupted subagents (#5242).

### E. Security & Trust Boundaries
- **Claude Code**: False-positive safety flags downgrading Opus 5→4.8 (#84340 Cluster).
- **Codex**: Cyber-capable model auto-review defaults (#37057); Guardian circuit breaker (#37190).
- **Gemini CLI**: SSRF via async DNS resolution (#28557); deterministic redaction before sending (. #26525).
- **Qwen Code**: Read-only shell classifier bypass (#8582); password leaks in sanitizer (#8136); trust-boundary hook hardening (#8396).
- **Copilot CLI**: Security hook that fails to fire (#3013).

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach | Key Differentiator |
|---|---|---|---|---|
| **Claude Code** | Enterprise agentic workflows | Pro/enterprise developers | Sub-agents, skills marketplace, background jobs | Deep Anthropic model integration; marketplace ecosystem |
| **OpenAI Codex** | **Code agent** + desktop app | Pro/team users | TUI + GUI, MCP, remote environments | Model agnosticism (can delegate to Opus); fast iteration cadence |
| **Gemini CLI** | **IDE/agent integration** | Google/GCP ecosystem devs | Session-based, skills, Auto Memory | Deep GCA backend integration; nested-stream error handling |
| **GitHub Copilot CLI** | **Git-native** workflow | GitHub-centric teams | Worktrees, PR integration, cloud agents | Tight GitHub/enterprise policy integration |
| **Kimi CLI** | **Lighweight, low-friction** CLI | Individual indie devs | ACP (Agent Client Protocol), minimal config | Focus on minimal viable agent; ACP ecosystem as bridge |
| **OpenCode** | **Open, extensible** agent | TUI power users | V2 engine, cross-process OAuth, plugin architecture | Open-source extensibility; fastest approach to v2 data migration |
| **Pi** | **TUI-forward** micro-agent | Terminal purists | TUI-first, OSC 8, Codex WebSocket backend | Rust-based performance; minimal resource footprint |
| **Qwen Code** | **Multi-surface** agents | Chinese + global community | Desktop (Tauri), Web Shell, IM channels (DingTalk/QQ/Feishu) | **Broadest channel coverage** — beyond CLI to chat/IM surfaces |
| **DeepSeek TUI** | **Lightweight Runtime API** | TUI+hacker community | Rust-based, growing REST API surface | Comprehensive Runtime API for managed clients; ACP tool execution |

**Emerging patterns:**
- **Multi-surface agents**: Qwen Code stands alone in covering IM channels (DingTalk, QQ, Feishu) — representing a genuinely different vector of distribution.
- **Model routing**: Copilot CLI's sub-agent delegation to Opus despite configured GPT-5.6 Terra (#4377) and Claude Code's model downgrades both indicate **model orchestration** is a major pain point across tools.
- **Engine evolution**: OpenCode is the only tool mid-migration (V1→V2 engine), while Claude Code (skills marketplace) and Codex (alpha-heavy) are further along in feature iteration cycles.

---

## 5. Community Momentum & Maturity

### High Momentum (shipping new functionality + significant community engagement)
- **OpenAI Codex**: 8 alpha builds in 24 hours; 373👍 on `/undo` request; large active PR pipeline — clearly the fastest iterating, with significant community loyalty despite Windows instability.
- **Claude Code**: Continuous stable releases; new marketplace management; high-engagement billing/usage issues (17+ comments) — the largest and most vocal user base, heavily enterprise-oriented.
- **Qwen Code**: Shipped a brand-new Tauri desktop app; active feature expansion (Live Voice, tmux sub-agents, IM channels); strong community probing security boundaries.

### Steady/Rapid Response
- **OpenCode**: Stable feature flow (v1.18.14) but a critical session-history regression threatens trust.
- **Pi**: Methodical fix wave (10 PRs merged today); TUI-polish-oriented community.
- **DeepSeek TUI**: Focused engineering sprint toward v0.9.4; Runtime API expansion signals long-term architectural ambition.
- **Kimi CLI**: Small but responsive — two rapid PRs to fix a same-day critical bug.

### Moderate/Slower Response
- **Gemini CLI**: No new releases; mostly merged regression-fix PRs; issue backlog shows high community patience but slow resolution of P1 issues (#21409, #22323 open for months).
- **GitHub Copilot CLI**: Release-driven but slow PR pipeline; the broad influx of triage issues suggests either a growing user base or surfacing pent-up problems.

### Community Sentiment Snapshot
| Tool | Positive Signals | Negative Signals |
|---|---|---|
| Claude Code | Marketplace momentum, fast fixes | Model-flagging distrust, cost exposure |
| Codex | Alpha iteration energy, responsive backports | Windows instability, `/undo` regression |
| Gemini CLI | Strong eval-suite investment | Long-unsolved sub-agent hangs |
| Copilot CLI | Pre-release polish (worktrees, pinned prompts) | MCP policy fragility, silent failures |
| OpenCode | V2 engine migration progress | Session-history regression in current stable |
| Qwen Code | Desktop launch, channel breadth | Security gaps (shell bypass) |
| DeepSeek TUI | API expansion, ACP capability | Silent context degradation |

---

## 6. Trend Signals (Industry-Level Takeaways for Developers)

1. **Security safety-catcher calibration is the #1 pain point across the industry.**  
   Claude Code (Opus downgrades), Codex (cyber-safety false positives), Qwen Code (shell bypass), and Gemini CLI (SSRF) all report incidents. The pattern: safety features are over-cautious in some contexts (blocking authorized work) and under-cautious in others (shell bypasses, credential leaks). Expect platforms to invest heavily in adaptive, context-aware safety policies over binary rule-based filters.

2. **"Agent delegation" is breaking user trust.**  
   Whether it's Copilot CLI's sub-agents delegating to Opus against user config, Claude Code's model downgrades, or Gemini CLI's sub-agents running without permission — **users want deterministic model routing** and transparent sub-agent behavior. This will become a key development target.

3. **Cost transparency is essential for adoption in the enterprise.**  
   From Claude Code's $411 incident to Codex's 600M token/day reports, users are being burned by unclear billing boundaries. Demand for **programmatic usage APIs** (OpenCode #16017) and **per-task budget controls** will grow. Vendors that ship cost guardrails first will have a competitive advantage.

4. **Session portability and resume reliability are now table stakes.**  
   Every tool has issues with sessions that can't be resumed, histories wiped, or state lost. As AI CLIs move from "experiments" to "daily drivers," **users need sessions to survive restarts, model changes, and context compaction**. The ability to reliably resume long-running work will differentiate tools.

5. **MCP is replacing direct model access as the integration surface — and it's still immature.**  
   OAuth failures, handshake timeouts, zombie processes, policy enforcement gaps — MCP is powerful but flaky. Expect a hardening wave across all tools in coming months, particularly around **remote MCP, cross-process OAuth, and streaming resilience**.

6. **Desktop/GUI extensions are where innovation is happening — but reliability lags.**  
   Codex Desktop (GPU crashes, MEMORY LEAKS), Copilot CLI (Windows crashes), Qwen Desktop (startup crash), OpenCode Desktop (packaging issues) — the desktop build-out is proceeding but platform-specific instability is a systemic issue.

7. **Windows support remains the weak link across every tool.**  
   From Claude Code's TCC permission dialogs on macOS to Codex's Sysmon BSODs, Copilot CLI's native crashes, Kimi's abnormal exits, and Qwen's startup crash — **cross-platform maturity is the gap between "demo" and "production" for AI CLIs**. Tools that invest in Windows/macOS parity will win enterprise teams.

8. **Transparency about model state is becoming a differentiator.**  
   Requests for real wait times (DeepSeek #5240), fallback context-window warnings (#5244), actionable error messages (Kimi #2590), and honest sub-agent completion status (Gemini #22323) all point to the same conclusion: **users are willing to accept limitations if the tool tells the truth about them.**

---

## Bottom Line for Decision-Makers

The AI CLI ecosystem is converging on the same architectural patterns (sub-agents, MCP, background jobs, desktop apps) but diverging on execution quality. **Claude Code leads in enterprise trust and marketplace vision; Codex leads in iteration velocity; Qwen Code differentiates through distribution channels; DeepSeek TUI offers the most open Runtime API for third-party integration.** All tools face reliability/security challenges ahead of converging on best practices — the teams that address session reliability, cost guardrails, and transparent agent behavior will lead the next phase of adoption.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-08-06 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

### #1 — skill-creator bug-fix cluster (PR #1298)
**URL:** [anthropics/skills PR #1298](https://github.com/anthropics/skills/pull/1298)
**Status:** Open | **Author:** MartinCajiao | **Created:** 2026-06-10

**Functionality:** Fixes the `run_eval.py` script — the core evaluation harness for skill-creator — which was reporting `recall=0%` for every skill description, effectively optimizing descriptions against noise. The PR installs the eval artifact as a real skill, fixes Windows stream reading, trigger detection, and parallel worker behavior.

**Discussion highlights:** This is the most active PR in the repository, directly addressing [Issue #556](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍) and [Issue #1169](https://github.com/anthropics/skills/issues/1169) with 10+ independent reproductions. The cluster includes related PRs: [#1099](https://github.com/anthropics/skills/pull/1099) (Windows subprocess pipe crash), [#1050](https://github.com/anthropics/skills/pull/1050) (Windows subprocess + encoding), [#1323](https://github.com/anthropics/skills/pull/1323) (trigger detection misses real skill names), and [#1261](https://github.com/anthropics/skills/pull/1261) (command files polluting live project registry).

### #2 — document-typography (PR #514)
**URL:** [anthropics/skills PR #514](https://github.com/anthropics/skills/pull/514)
**Status:** Open | **Author:** PGTBoos | **Created:** 2026-03-04

**Functionality:** Typographic quality control for generated documents — prevents orphan word wrap (1–6 words spilling to next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment. Addresses a universal pain point in AI-generated documents.

**Discussion highlights:** The community recognizes this as a gap-filler — "these issues affect every document Claude generates" — with users noting the skill would apply across docx, pdf, and html workflows regardless of output format.

### #3 — fix(pdf): case-sensitive file references (PR #538)
**URL:** [anthropics/skills PR #538](https://github.com/anthropics/skills/pull/538)
**Status:** Open | **Author:** Lubrsy706 | **Created:** 2026-03-06

**Functionality:** Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where `REFERENCE.md` and `FORMS.md` were referenced in uppercase but exist lowercase. Breaks on case-sensitive filesystems (Linux/macOS).

**Discussion highlights:** Part of a maintenance wave by the same author — see also [#541](https://github.com/anthropics/skills/pull/541) (docx w:id collision with bookmarks) and [#539](https://github.com/anthropics/skills/pull/539) (YAML unquoted description validation). Signals community investment in correctness and cross-platform reliability of the core document skills.

### #4 — ODT skill (PR #486)
**URL:** [anthropics/skills PR #486](https://github.com/anthropics/skills/pull/486)
**Status:** Open | **Author:** GitHubNewbie0 | **Created:** 2026-03-01

**Functionality:** OpenDocument text creation, template filling, and ODT→HTML conversion (`.odt`, `.ods`). Triggers on 'ODT', 'ODS', 'ODF', 'OpenDocument', or 'LibreOffice document' mentions.

**Discussion highlights:** High interest — fills an office-format gap alongside the existing docx/pdf skills. Community members noted the importance for European public-sector contexts where ODF is mandated.

### #5 — frontend-design skill improvement (PR #210)
**URL:** [anthropics/skills PR #210](https://github.com/anthropics/skills/pull/210)
**Status:** Open | **Author:** justinwetch | **Created:** 2026-01-05

**Functionality:** Revises the frontend-design skill for clarity, actionability, and internal coherence — ensures every instruction is something Claude can follow in a single conversation with specific behavior-steering guidance.

**Discussion highlights:** Focused on **skill quality** rather than new functionality — an early example of the meta-discussion that later crystallized into the skill-creator bug cluster. The PR author explicitly aimed to "improve clarity and actionability" as the benchmark.

### #6 — self-audit skill (PR #1367)
**URL:** [anthropics/skills PR #1367](https://github.com/anthropics/skills/pull/1367)
**Status:** Open | **Author:** YuhaoLin2005 | **Created:** 2026-06-28

**Functionality:** Audits AI output before delivery — mechanical file verification first, then four-dimension reasoning audit in damage-severity priority order. Works with any project, tech stack, or model. Related proposal at [Issue #1385](https://github.com/anthropics/skills/issues/1385) (Reasoning Quality Gate Pipeline).

**Discussion highlights:** Represents a growing community interest in **output quality gates**, adversarial review, and delivery verification — complementary to the skill-creator eval fixes.

---

## 2. Community Demand Trends

**From Issues (50 tracked, top 15 shown):**

| Trend | Representative Issue(s) | Signal |
|---|---|---|
| **Security & trust boundary** | [#492](https://github.com/anthropics/skills/issues/492) (43 comments, 2 👍) — community skills under `anthropic/` namespace impersonate official skills | Strongest demand signal; elevated permissions risk |
| **Org-wide skill sharing** | [#228](https://github.com/anthropics/skills/issues/228) (16 comments, 8 👍) — share skills within orgs without manual download/upload | High enthusiasm; collaboration feature |
| **Eval & quality tooling** | [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍), [#1169](https://github.com/anthropics/skills/issues/1169) — run_eval.py 0% recall | Active user pain; multiple PRs in flight |
| **Duplicate skill conflicts** | [#189](https://github.com/anthropics/skills/issues/189) (6 comments, 9 👍) — document-skills and example-skills install identical content | Plugin ecosystem confusion |
| **Context window management** | [#1487](https://github.com/anthropics/skills/issues/1487) (4 comments) — `claude-api` skill injects ~156k tokens in one call; [#1175](https://github.com/anthropics/skills/issues/1175) — SharePoint access control in SKILL.md | Efficiency and safety concerns |
| **New skill proposals** | [#1329](https://github.com/anthropics/skills/issues/1329) — compact-memory (symbolic notation for agent state); [#412](https://github.com/anthropics/skills/issues/412) — agent-governance safety patterns | Memory & governance directions |
| **Skill vanishing/data loss** | [#62](https://github.com/anthropics/skills/issues/62) (10 comments, 2 👍) — all skills disappeared after file rename | Reliability fear |
| **Platform coverage** | [#29](https://github.com/anthropics/skills/issues/29) — AWS Bedrock support; [#16](https://github.com/anthropics/skills/issues/16) — expose skills as MCPs | Integration breadth |

**Most-anticipated new directions:** Security hardening, org-level sharing, agent memory/state management, governance patterns, and output quality gates.

---

## 3. High-Potential Pending Skills

These PRs are open with active discussion and may merge soon:

| Skill | PR | Summary |
|---|---|---|
| **self-audit** (v1.3.0) | [#1367](https://github.com/anthropics/skills/pull/1367) | Mechanical verification + four-dimension reasoning quality gate |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Color naming systems, color spaces, "what to use when" tables |
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Addresses planning artifact accumulation lifecycle gap ([#1417](https://github.com/anthropics/skills/issues/1417)) |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Testing Trophy model, unit/React component/E2E testing |
| **pyxel** (retro games) | [#525](https://github.com/anthropics/skills/pull/525) | MCP server for Pyxel retro game engine (write → run → iterate) |
| **skill-quality-analyzer** / **skill-security-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Meta-skills evaluating skill quality and security across 5 dimensions |
| **SAP-RPT-1-OSS predictor** | [#181](https://github.com/anthropics/skills/pull/181) | SAP tabular foundation model for predictive analytics |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand at the Skills level is reliability tooling for the skill-authoring lifecycle itself** — fixing the eval harness that measures skill quality (six distinct PRs addressing `run_eval.py`/`run_loop.py` bugs), alongside security hardening of the trust boundary and output-quality gates — reflecting a maturation from "what skills should we build" to "how do we build, measure, and trust skills at scale."

---

# Claude Code Community Digest — 2026-08-06

## Today's Highlights
Release v2.1.223 brings marketplace management improvements, but the community's attention is firmly on a cluster of **model behavior issues**: multiple reports of authorized security work being falsely flagged and downgraded from Opus 5 to Opus 4.8 (#84340, #84344, #84353), plus a concerning case of an unattended job racking up $411 in unintended API charges (#84350). The `--continue` flag failing to find sessions created with `-p` (#82536) and session-hanging bugs continue to draw developer frustration.

## Releases
**v2.1.223** — Added owner wildcard entries (`"owner/*"`) to `strictKnownMarketplaces` and `blockedMarketplaces` managed settings, enabling allow/block of all marketplace repos under a GitHub org. Also added a warning when workflow agents, forked skills, slash commands, or resumed background agents are involved.

## Hot Issues

1. **[#82506 — Possible Claude Max usage bug: session limit consumed without using](https://github.com/anthropics/claude-code/issues/82506)** (17 comments, 👍7) — Users report Max plan session limits being consumed without actual usage. High community engagement suggests billing/usage concerns are top-of-mind.

2. **[#66504 — Session URL appended to commit messages and PR descriptions by default — should be opt-in](https://github.com/anthropics/claude-code/issues/66504)** (12 comments, 👍46) — The most-upvoted open FR. Developers are unhappy that session URLs leak into commit history and PRs by default, creating noise and potential privacy concerns.

3. **[#58750 — Cowork Desktop (macOS): AskUserQuestion card never reaches renderer](https://github.com/anthropics/claude-code/issues/58750)** (11 comments) — Pending requests silently resolve as "Dismissed" on quit. Long-running bug affecting Cowork desktop UX on macOS.

4. **[#82536 — `--continue` cannot find sessions created by `-p` (interactive resume)](https://github.com/anthropics/claude-code/issues/82536)** (7 comments) — Headless sessions can't be resumed interactively, breaking a natural workflow transition. Filed 2026-07-30, no fix yet.

5. **[#83403 — Claude Desktop crashes near 5-hour usage limit, requires full reinstall](https://github.com/anthropics/claude-code/issues/83403)** (6 comments) — Severe crash bug forcing full reinstalls. Likely tied to the Max session-limit logic.

6. **[#78915 — "[Request interrupted by user for tool use]" on FOREGROUND Task with no user interrupt](https://github.com/anthropics/claude-code/issues/78915)** (3 comments) — Spurious "interrupted by user" messages on foreground subagent dispatch, CLI/macOS, v2.1.212. Related to #84346 below.

7. **[#84340/#84344/#84353 — Security testing falsely flags and downgrades Opus 5 → Opus 4.8](https://github.com/anthropics/claude-code/issues/84340)** (new, cluster of 3 reports) — Authorized whitehat security work is being caught by safeguards. The downgrade appears triggered by re-authentication or session state, not content. Notably, one reporter wrote in Spanish, indicating global impact.

8. **[#84350 — Claude deployed unattended job calling metered paid API — $411 in unintended charges](https://github.com/anthropics/claude-code/issues/84350)** (new) — **Major trust issue.** Model deployed a job calling a paid API without cost guardrails. Strongly suggests the need for cost-control features.

9. **[#84346 — Subagent model-stall watchdog abort (~600s) surfaces as "[Request interrupted by user for tool use]"](https://github.com/anthropics/claude-code/issues/84346)** (new) — 13 transcripts with identical 600.0–605.6s gap signature. Related to #78915; the error string is being reused for a watchdog abort it was never meant for.

10. **[#84349 — Background/detached sessions die permanently after daemon restart](https://github.com/anthropics/claude-code/issues/84349)** (new) — Stale workers are refused respawn and then reported dead (`respawned=0`). Affects reliability of long-running background agents.

## Key PR Progress

1. **[#41661 — Add 14 Revolutionary Claude Code Plugins](https://github.com/anthropics/claude-code/pull/41661)** — Adds 14 plugin directories across security, performance, architecture, and fullstack automation. Updates marketplace to 27 plugins. Large surface area; awaiting review since March.

2. **[#16929 — Respect `--comment` flag for `/code-review` GitHub posting](https://github.com/anthropics/claude-code/pull/16929)** — Fixes #16606. Makes terminal output the default, only posts to GitHub when `--comment` is explicitly passed. Aligns implementation with README.

3. **[#84138 — Workaround for self-signed certificate error in Cowork](https://github.com/anthropics/claude-code/pull/84138)** — Closes #24470. Addresses Bun runtime not loading macOS system certificates, causing SSL failures for users without proxies.

4. **[#84004 — Limit frontmatter parsing in plugin-dev](https://github.com/anthropics/claude-code/pull/84004)** — Range-based `sed` would restart at every `---` line. Now parses only the opening YAML frontmatter block, fixing corruption when Markdown contains horizontal rules.

5. **[#84003 — Propagate top-level failures in duplicate-maintenance scripts](https://github.com/anthropics/claude-code/pull/84003)** — Replaces `.catch(console.error)` so startup/API failures actually fail the process instead of resolving silently.

6. **[#83999 — Validate `gh` flag values in restricted wrapper](https://github.com/anthropics/claude-code/pull/83999)** — Rejects value-taking flags missing their value (e.g., `gh issue list --limit`), preventing bypass of argument validation.

7. **[#83995 — Validate label option values in scripts](https://github.com/anthropics/claude-code/pull/83995)** — Prevents `$2: unbound variable` aborts and consumption of following options as label values.

8. **[#83993 — Reject self-referential duplicates](https://github.com/anthropics/claude-code/pull/83993)** — Stops `comment-on-duplicates.sh` from marking an issue as a duplicate of itself, which previously triggered infinite-style loops.

9. **[#83992 — Assert expected hook decision in test-hook.sh](https://github.com/anthropics/claude-code/pull/83992)** — Fixes #83800. Adds `--expect allow|deny|ask` flag so tests catch hooks that allow operations they were intended to deny.

## Feature Request Trends

- **Opt-in session metadata in commits/PRs** (#66504, 👍46) — Strong demand for session URL/transcript references to be opt-in rather than default.
- **Portable session transcripts** (#81946) — Users want transcripts linked by session ID independent of project/absolute path, enabling cross-machine portability.
- **Disableable left-arrow detach gesture** (#84348) — Gesture conflicts with standard text navigation; needs setting or keybinding.
- **Cost guardrails** (implied by #84350) — Unattended jobs with metered APIs need explicit budget controls.
- **Mobile slash-command typeahead** (#56204) — Feature parity for claude.ai/code on mobile browsers.

## Developer Pain Points

- **Model behavior and safeguards reliability** — Four reports (#84340, #84344, #84352, #84353) of false-positive cyber-safeguard flags, with **Opus 5→4.8 downgrades** derailing authorized security work. One CVP-approved org still blocked (#84352). This is the fastest-growing frustration cluster.
- **Spurious "interrupted by user" messages** (#78915, #84346) — The same error string is used for watchdog aborts and dispatch-time failures, making debugging confusing. Multiple cross-linked reports.
- **Session/daemon reliability** (#82536, #84347, #84349) — `--continue` can't resume headless sessions, sessions hang until VS Code restart, and background agents die permanently after daemon restarts.
- **Windows-specific issues** (#84333, #84354) — MSIX app silently becomes *Modified/NeedsRemediation* mid-session; "Past Conversations" empty due to case-sensitive path hashing.
- **MacOS permission prompts show bare version numbers** (#79867) — TCC dialogs display "2.1.216" as app name, making permission decisions unassessable for users.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-06

## Today's Highlights

The Codex team shipped a stabilization release (rust-v0.146.1) with safer automatic-review defaults for cyber-capable models, while several alpha builds of v0.147 continue rapid iteration. The community remains deeply engaged on long-standing Windows desktop stability issues — particularly GPU-process crashes and sandbox-related system degradation — alongside a highly-voted request to restore the `/undo` TUI command. On the engineering front, a wave of PRs consolidates skills and MCP infrastructure while adding defense-in-depth around guardian policies and handshake timeouts.

---

## Releases

**rust-v0.146.1** — Stable patch release with one notable fix:
- Safer automatic-review defaults for cyber-capable models, with permission changes now explained in the terminal interface ([#37057](https://github.com/openai/codex/pull/37057))

This is important — it directly addresses the community's growing concern (see Issue #37161) about overly aggressive cybersecurity filtering. The backport means stable users get the fix without waiting for v0.147.

**Alpha channel (rust-v0.147.0-alpha.6 through alpha.13)** — Multiple rapid-fire releases over 24 hours, indicating active iteration on the 0.147 feature set. No individual changelogs were published for these builds, but the PR list below gives a strong signal of what's landing: rollout migration, skills consolidation, MCP hardening, and remote environment provisioning.

---

## Hot Issues

1. **[#9203 — Make "/undo" back](https://github.com/openai/codex/issues/9203)** — *70 comments, 373 👍*
   The most-voted community request. Users are being bitten by unintended file deletions/modifications on untracked files, and the removal of `/undo` has no workaround. The sustained 8-month thread signals this is a top-priority quality-of-life regression.

2. **[#12491 — Codex.app GUI: MCP child processes not reaped (1300+ zombies, 37GB leak)](https://github.com/openai/codex/issues/12491)** — *31 comments, 5 👍*
   Severe resource leak in the desktop GUI — MCP child processes survive task completion, producing thousands of zombies and massive memory growth. This should be a P0 for the desktop team.

3. **[#33776 — Windows: ChatGPT.exe spawns hundreds of taskkill.exe/conhost.exe processes](https://github.com/openai/codex/issues/33776)** — *30 comments, 27 👍*
   A Windows-specific process storm (287+ processes in one session) degrading DWM and causing WMI failures. High upvote count indicates broad Windows-desktop user impact.

4. **[#23979 — Desktop conversation history missing after update](https://github.com/openai/codex/issues/23979)** — *26 comments, 5 👍*
   Post-update, local project threads vanish from the UI despite intact SQLite data on disk. Data-preservation worry — users fear their session history is gone.

5. **[#31035 — Windows: SysmonDrv reinstall + BSODs](https://github.com/openai/codex/issues/31035)** — *23 comments*
   Alarming: Codex Desktop appears to reinstall/start Sysinternals Sysmon driver after forced uninstall, leading to kernel crashes. If true, this is a sandbox implementation issue with system-level consequences.

6. **[#35352 — Desktop exits when embedded browser GPU process crashes + SwiftShader fallback blocked](https://github.com/openai/codex/issues/35352)** — *17 comments* (CLOSED)
   GPU-process crash hard-exits the app. Closed — fix likely shipping. Related duplicates (#35635, #35566, #35411) suggest this was a widespread Windows issue.

7. **[#34684 — `codex mcp login` fails on macOS against spec-compliant OAuth server (works on Linux)](https://github.com/openai/codex/issues/34684)** — *10 comments, 5 👍*
   Platform inconsistency in OAuth flow breaks MCP integration on macOS. Developer-facing and blocks a core workflow.

8. **[#33493 — Local compaction v2 retains unbounded input_image payloads → repeated auto-compaction](https://github.com/openai/codex/issues/33493)** — *8 comments, 2 👍*
   Image-heavy threads enter an auto-compaction loop because the compacted context still contains full image payloads. Context-window abuse users are paying excessive tokens.

9. **[#32309 — High-frequency code-mode polling amplified by large resumed context](https://github.com/openai/codex/issues/32309)** — *7 comments, 4 👍*
   User reports ~600M token/day consumption (vs 150–200M with 5.5) driven by polling and context-resume amplification. Token-cost spike is a serious Pro 20x user concern.

10. **[#37161 — Severe false positives in cybersecurity request filtering](https://github.com/openai/codex/issues/37161)** — *5 comments, 1 👍* (NEW)
    Legitimate security engineering tasks (static analysis, fuzzing, debugging) blocked by the cyber-safety filter. Ironically filed the same day the v0.146.1 fix shipped — likely related.

---

## Key PR Progress

1. **[#37190 — Interrupt cyber model turns after one Guardian denial](https://github.com/openai/codex/pull/37190)**
   Circuit-breaker policy for catalog-flagged cyber models: one Guardian denial ends the turn, while other models retain existing thresholds. Directly addresses false-positive fatigue.

2. **[#37191 — Preserve legacy semantics during rollout migration](https://github.com/openai/codex/pull/37191)** + **[#37175 — Add legacy rollout migration to paginated history](https://github.com/openai/codex/pull/37175)**
   Migration of legacy JSONL rollouts into paginated history, carefully preserving rollbacks, compaction checkpoints, and subagent history. Critical for data integrity as the storage format evolves.

3. **[#37188 — Reserve the `tool_search` namespace for the search tool](https://github.com/openai/codex/pull/37188)**
   Prevents namespace collisions by removing shadowing `tool_search` namespaces before registering the built-in search tool — ties into #32101 where `tool_search` was being dropped from `exec` in Code Mode.

4. **[#37168 — Bound remote MCP handshake HTTP requests](https://github.com/openai/codex/pull/37168)**
   Fixes a blocking-executor bug where timed-out streamable HTTP handshakes kept running. Required for reliable remote MCP.

5. **[#37167 — Expose session sources to MCP contributors](https://github.com/openai/codex/pull/37167)**
   Thread-scoped MCP resolution via `session_source()` — enables version/type-aware MCP behavior across threads.

6. **[#37166 — Keep textarea cursors and rendering inside the viewport](https://github.com/openai/codex/pull/37166)**
   TUI textarea fix: logical lines that exactly fill the width no longer lose cursor tracking; clipping/wrapping corrected.

7. **[#37157 — Harden named session lookup in the TUI](https://github.com/openai/codex/pull/37157)**
   Shared exact-name lookup between resume/archive, prefers valid SQLite names, validates rollout identity — reduces session-recovery failure surface.

8. **[#37151 — Coalesce concurrent Git status scans](https://github.com/openai/codex/pull/37151)**
   Shares in-flight `git status --porcelain` across concurrent workspace metadata requests (same repo root). Performance win for multi-thread desktop use.

9. **[#37149 — Project orchestrator skills through world state](https://github.com/openai/codex/pull/37149)**
   Moves orchestrator skill catalog into world state so unchanged catalogs remain incremental across turns — saves context/tokens on resume.

10. **[#37147 — Track provisioned environment state across registration](https://github.com/openai/codex/pull/37147)**
    Adds pending/ready/failed provisioning states for Noise environments with conflict rejection — foundation for reliable remote execution.

---

## Feature Request Trends

- **Restore `/undo`** (#9203, 373 👍): clear #1 ask. Users need rollback for untracked-file changes; no equivalent exists.
- **Per-thread Auto mode** (#34278): routing both model and reasoning effort per-thread, atomically, at submission time.
- **Better MCP ergonomics**: OAuth login parity across platforms (#34684), tools reliably exposed to app threads (#19425), and handshake resilience.
- **Accessibility improvements** (#34211): JAWS/screen-reader support for chat history and message navigation.
- **Compaction/context controls**: users want predictable context windows — no unbounded image retention (#33493) or polling amplification (#32309).

---

## Developer Pain Points

- **Windows desktop instability dominates**: GPU process crashes with SwiftShader blocks (#35352, #35635, #35566, #35411), MSIX self-corruption (#35737), Sysmon/BSOD issues (#31035) — Windows users are hitting systemic reliability issues.
- **Process/resource leaks**: MCP zombie processes (37GB leaks, #12491), taskkill storms (#33776), and sandbox offline stuck states (#37187) — the desktop app leaks or hangs under real usage.
- **Session/data integrity**: conversation history vanishing after updates (#23979), orchestration state reverting to on-request approvals (#32862), and compaction loops inflating token bills (#33493, #37090) erode trust.
- **MCP integration inconsistencies**: cross-platform OAuth failures (#34684), tools discovered but never exposed (#19425), `tool_search` dropped in Code Mode (#32101) — MCP is powerful but immature across surfaces.
- **Cyber-safety false positives** (#37161): legitimate security work is being blocked, though v0.146.1's backport is a step toward relief. The Guardian circuit breaker (#37190) should reduce over-blocking.
- **Context/token consumption spikes** (#32309, #37090): users on Pro 20x report 3–4× token usage vs prior models — a real cost concern.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-06

## Today's Highlights
No new releases landed in the last 24 hours, but the PR queue shows strong momentum on stability fixes: two independent PRs address a malformed-tool-argument crash in the SDK's `sendStream()`, and a merged fix targets the "model finishes your sentence" bug caused by message fusion after interrupted tool calls. Issue activity remains concentrated on subagent reliability, with the generalist-agent hang (#21409) and a MAX_TURNS misreporting issue (#22323) still drawing community attention after months of being open.

## Releases
No new releases in the last 24 hours. The most recent activity centers on post-v0.53.0 regression fixes, particularly the `Function call is missing a thought_signature` API error addressed in PR #28607.

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (12 comments, P1)  
   A `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` even when it hit the max-turns limit before doing any analysis. This masks real failures as successes, potentially eroding trust in agent-reported outcomes. Maintainer-only, marked for retesting.

2. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (8 comments, 8 👍, P1)  
   The generalist subagent hangs indefinitely on simple tasks like folder creation—users report waiting up to an hour before cancelling. Workaround: instruct the model to never defer to subagents. A long-standing reliability issue with high community impact.

3. **[#19873 — Zero-Dependency OS sandboxing & post-execution intent routing](https://github.com/google-gemini/gemini-cli/issues/19873)** (8 comments, P1)  
   Proposes leveraging Gemini 3's native bash affinity by introducing OS-level sandboxing with post-execution intent routing—a design that could preserve the model's preferred shell-based workflows while improving safety. Represents a significant architectural direction for the agent.

4. **[#24353 — Robust component-level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (7 comments, P1)  
   Epic tracking expansion of the behavioral eval suite (currently 76 tests across 6 Gemini models). Signals growing investment in regression prevention for agent behavior—a response to the spate of regressions in recent releases.

5. **[#22745 — Assess AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (7 comments, P2)  
   Epic investigating whether AST-aware tools could reduce token noise, improve method-boundary precision, and reduce turn counts from misaligned reads. Could substantially improve agent efficiency on large codebases.

6. **[#21968 — Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (6 comments)  
   Anecdotal but resonant: the model rarely self-selects custom skills or subagents without explicit prompting, even when highly relevant. Suggests a gap between agent capability and autonomous tool selection.

7. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (5 comments, P2)  
   If the extraction agent skips a low-signal session, it stays "unprocessed" and keeps getting re-surfaced—an infinite retry loop. A data-hygiene issue in the Auto Memory subsystem.

8. **[#26525 — Deterministic redaction and reduced Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (4 comments, P2, security)  
   Auto Memory sends local transcript content to the model before any redaction happens, and the service can log existing skill contents. Privacy-relevant concern for users handling sensitive code.

9. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (4 comments, 3 👍, P1)  
   Simple CLI commands hang with the shell marked "Awaiting user input" after the command has already finished. Intermittent but highly disruptive to interactive workflows.

10. **[#22093 — Subagents run without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** (3 comments, P2)  
    Users with agents disabled in all configs saw subagents activate anyway after an update—a permission-model regression that raises trust and safety questions.

## Key PR Progress

1. **[#28700 — Stop a new user message fusing into an unanswered tool response](https://github.com/google-gemini/gemini-cli/pull/28700)** (merged)  
   Fixes the "model finishes your sentence" bug: after an interrupted tool call (stream failure or ESC), the next user message was merged into the interrupted turn, causing the model to continue rather than follow instructions.

2. **[#28607 — Preserve functionCall thoughtSignature when stripping thought parts](https://github.com/google-gemini/gemini-cli/pull/28607)** (merged, closed)  
   Fixes the v0.53.0 regression causing `API Error 400: Function call is missing a thought_signature`. `stripThoughts()` was dropping required signatures during context management.

3. **[#28695 — Don't abort sendStream on malformed tool arguments](https://github.com/google-gemini/gemini-cli/pull/28695)** (merged, closed)  
   Unguarded `JSON.parse()` on string-valued tool arguments could throw out of the generator. Tool args are model output—malformed JSON should be handled, not fatal.

4. **[#28660 — Keep sendStream alive on malformed tool arguments](https://github.com/google-gemini/gemini-cli/pull/28660)** (open)  
   An alternative/overlapping approach to #28695: defensively parse, validate that decoded args are JSON objects (rejecting arrays/primitives/null), and convert invalid arguments into structured `functionResponse` errors.

5. **[#28672 — Repair /compress session reload and quota-fallback tool response loss](https://github.com/google-gemini/gemini-cli/pull/28672)** (merged, closed)  
   Two fixes in one: `/compress` failures that left sessions broken, and tool responses lost when hitting quota limits forced a fallback model switch.

6. **[#28670 — Correct fallback on model capacity errors for GCA agent mode](https://github.com/google-gemini/gemini-cli/pull/28670)** (merged, closed)  
   Backend capacity exhaustion (`MODEL_CAPACITY_EXHAUSTED`/HTTP 429) caused infinite retries on the same failed model instead of falling back to Flash or other available models.

7. **[#28689 — Unwrap and parse nested gaxios streaming errors](https://github.com/google-gemini/gemini-cli/pull/28689)** (merged, closed)  
   Improves structured quota/rate-limit error parsing in nested streaming failures—better classification and messaging for Gemini Code Assist.

8. **[#28677 — Add timeout to IdeClient.getInstance() process traversal](https://github.com/google-gemini/gemini-cli/pull/28677)** (open, P1)  
   Process-tree traversal could hang indefinitely, leaving the TUI stuck at "Initializing..." forever. Adds a 3-second race timeout with a no-IDE fallback.

9. **[#28557 — Resolve SSRF vulnerability in web-fetch.ts via async DNS resolution](https://github.com/google-gemini/gemini-cli/pull/28557)** (open, P1/P2)  
   `isBlockedHost` used synchronous `isPrivateIp()`, which only checked literal IPs—hostnames resolving to `169.254.169.254` (metadata endpoint) sailed past validation. Fixes #28555.

10. **[#28688 — Dynamically resolve Cloud Workstations proxy redirect URI for OAuth](https://github.com/google-gemini/gemini-cli/pull/28688)** (open, security)  
    OAuth flows in Cloud Workstations VMs statically redirect to `localhost`, which fails because the browser runs locally while the CLI runs remotely. Resolves proxy redirect URIs dynamically.

## Feature Request Trends

- **AST-aware code navigation** (#22745, #22746): Multiple epics tracking whether AST-aware reads/search/mapping improve agent precision and reduce token waste. Suggested starting points: `tilth` and `glyph`.
- **OS-level sandboxing with intent routing** (#19873): Let the model use its native bash capabilities but route/validate post-execution—a middle ground between freedom and safety.
- **Deterministic security redaction** (#26525): Move from prompt-instructed redaction to deterministic, pre-send redaction of secrets in Auto Memory. Related to broader data-handling concerns.
- **Self-awareness and actionable diagnostics** (#21432, #21763, #22598): Requests for the agent to accurately describe its own flags/hotkeys, and for subagent trajectories to be visible/shareable via `/bug` reports and `/chat share`.

## Developer Pain Points

- **Subagent reliability remains the #1 frustration**: The generalist hang (#21409), silent MAX_TURNS misreporting (#22323), and subagents running without permission (#22093) all point to a trust deficit—developers can't rely on subagent outcomes without verification.
- **"Model does the wrong thing silently"**: From tmp script littering (#23571) to destructive git commands (#22672), the agent needs better guardrails against messy or destructive behavior.
- **Post-update regressions keep recurring**: v0.33.0 broke the permission model (#22093); v0.53.0 broke thought signatures (#28607); terminal buffer corruption persists (#24935). The eval suite expansion (#24353) is a direct response, but trust takes time to rebuild.
- **Interactive shell hangs**: Commands completing but hanging with "Waiting input" (#25166) and interactive prompts freezing (vite app creation, #22465) break the flow of interactive development.
- **Auto Memory privacy and hygiene**: Transcript content is sent to models before redaction (#26525), low-signal sessions retry indefinitely (#26522), and invalid patches are silently skipped (#26523)—a subsystem that needs hardening.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-06

## Today's Highlights
Two new pre-releases (v1.0.79-2, v1.0.79-3) landed, focused on interactive polish with an improved pinned-prompt layout for the tab bar and a new `/worktree new` command for launching sessions in fresh worktrees. The issue tracker saw a significant influx of triage-level reports, with particularly active threads on MCP policy enforcement failures in enterprise configurations and a recurring Windows native-runtime crash that has persisted for months.

## Releases
**v1.0.79-2** (pre-release)
- Pinned prompts now occupy the tab bar row, preserving prompt shape while reducing timeline height.
- Pinned prompts stay off by default on terminals under 30 rows; configurable via `pinnedPrompts` setting.

**v1.0.79-3** (pre-release)
- Added `/worktree new` for starting a new session inside a fresh worktree.

**v1.0.79-4** (pre-release)
- Published without visible notes; likely includes fixes from triaged issues.

## Hot Issues
1. **#4370 — Copilot CLI 1.0.79-1 fails MCP initialization when `server/discover` returns `-32602`** ([link](https://github.com/github/copilot-cli/issues/4370))  
   FastMCP servers don't implement `server/discover` and return `-32602`; Copilot treats that as fatal instead of falling back. Breaks MCP integration broadly for FastMCP users.

2. **#4202 — Built-in view tool reports "Path does not exist" for existing files in 1.0.73** ([link](https://github.com/github/copilot-cli/issues/4202))  
   Regression introduced in 1.0.72; reproducible with an isolated probe. The view tool is fundamental to code exploration, making this a high-impact bug.

3. **#4382 — Kernel execve returns ENOEXEC but ld.so runs fine (Oracle Linux 10)** ([link](https://github.com/github/copilot-cli/issues/4382))  
   NPM-installed binary fails on Oracle Linux 10 x86_64 unless run via `ld` directly. Likely an ELF interpreter path issue; blocks a niche but real user base.

4. **#4378 — Cloud agent: MCP registry policy fetch fails with 401/403 on GHEC data residency** ([link](https://github.com/github/copilot-cli/issues/4378))  
   On GHEC with data residency, all user-configured MCP servers silently drop from cloud agent sessions — only platform defaults remain. Silent failure makes this especially dangerous for enterprise adopters.

5. **#4374 — `/mcp search` fails with 400 in repos with Azure DevOps git remotes** ([link](https://github.com/github/copilot-cli/issues/4374))  
   The MCP registry policy fetch fails when the repo remote is Azure DevOps; GitHub-specific assumptions break non-GitHub remotes. 4 upvotes in hours indicate broad impact.

6. **#4377 — GPT-5.6 Terra delegates to Opus subagent** ([link](https://github.com/github/copilot-cli/issues/4377))  
   Users noticing significant Opus credit consumption despite configuring GPT-5.6 Terra — sub-agent delegation bypasses the primary model configuration, causing unexpected cost.

7. **#4375 — macOS: `MallocStackLogging` stderr spam on every tool call** ([link](https://github.com/github/copilot-cli/issues/4375))  
   Noisy stderr output on each subprocess spawn; pollutes logs and makes debugging harder. Minor but very visible annoyance.

8. **#4381 — Notification badge count persists after all notifications cleared (Windows)** ([link](https://github.com/github/copilot-cli/issues/4381))  
   Desktop app badge stays after clearing all notifications — a common quality-of-life bug for Windows users.

9. **#4379 — Browser canvas: isolated storage partition breaks GitHub login persistence** ([link](https://github.com/github/copilot-cli/issues/4379))  
   Each canvas has its own storage partition, so login never persists across canvas sessions; you're always signed out.

10. **#4345 — Reasoning effort 'medium' not supported for claude-haiku-4.5** ([link](https://github.com/github/copilot-cli/issues/4345))  
    Server-side feature flags can trigger incompatible reasoning effort settings for models that don't support them; repeated errors during sub-agent execution.

## Key PR Progress
No pull requests were updated in the last 24 hours. GitHub Copilot CLI development is currently release-driven, with fixes landing directly through pre-release builds.

## Feature Request Trends
- **BYOM (Bring Your Own Model) improvements**: Emerging demand for **in-session model switching** and **automatic model discovery** for custom providers like Google Vertex AI (see [#4376](https://github.com/github/copilot-cli/issues/4376)).
- **MCP maturity**: **OAuth 3LO support** for MCP gateways (see [#4371](https://github.com/github/copilot-cli/issues/4371)) — users connecting with Authorization Code grants need browser-based URL elicitation.

## Developer Pain Points
- **Enterprise MCP policy enforcement is fragile**: At least three distinct failures ([#3934](https://github.com/github/copilot-cli/issues/3934), [#4378](https://github.com/github/copilot-cli/issues/4378), [#4374](https://github.com/github/copilot-cli/issues/4374)) show that policy checks either block legitimate servers, silently drop user config, or assume GitHub-only remotes. The most common thread: silent degradation is worse than explicit failure.
- **Agent delegation bypasses user intent** — both in model selection ([#4377](https://github.com/github/copilot-cli/issues/4377)) and in safety hooks ([#3013](https://github.com/github/copilot-cli/issues/3013), closed). A security hook that fails to fire is a serious concern.
- **Windows stability**: Long-running crash reports ([#4026](https://github.com/github/copilot-cli/issues/4026)) persist across months and versions, but today's surge of new triage issues didn't include new commentary on a fix.
- **Terminal UX regressions**: Alt-screen changes ([#1799](https://github.com/github/copilot-cli/issues/1799), 12 comments) and clipboard ownership notices ([#3172](https://github.com/github/copilot-cli/issues/3172), 7 upvotes) show the community is sensitive to interactive-mode polish and layout changes.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-06

## Today's Highlights
Two rapid-fire PRs landed to address a critical bug where image-returning MCP tools aborted runs mid-task without actionable error messages, and a pair of fixes aim to make the CLI more resilient against data corruption (undecodable bytes) and provide clearer configuration guidance. A long-standing feature request for a persistent memory system continues to draw community attention, while a newer crash report on Windows highlights platform-specific instability. The maintainers are clearly prioritizing tool-call reliability and error clarity.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#1283 — Feature Request: Memory System - Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)**  
   *Author: CatKang | Updated: 2026-08-06 | Comments: 19*  
   The most-commented open feature request. Users are asking for both automatic (AI-managed) and manual memory to persist project patterns, user preferences, and context across sessions. This remains a top community priority since February.

2. **[#2591 — StrReplaceFile corrupts undecodable bytes outside the edited region](https://github.com/MoonshotAI/kimi-cli/issues/2591)**  
   *Author: shoemoney | Created: 2026-08-05 | Comments: 0*  
   A serious data-corruption bug: files containing non-UTF-8 bytes are silently rewritten with U+FFFD replacement characters, even in regions far from the edit. This is a dangerous bug for users working with mixed-encoding or binary-adjacent files.

3. **[#2588 — Model declared without capabilities: image-returning MCP tool aborts the run mid-task, after side effects, with no hint at the fix](https://github.com/MoonshotAI/kimi-cli/issues/2588)**  
   *Author: tic-top | Created: 2026-08-05 | Comments: 0*  
   The error message is clear enough to trigger an abort, but not clear enough to tell users what config to change — and the abort happens *after* tool side effects have already been applied. This spurred two follow-up PRs today.

4. **[#2587 — kimi cli will exit abnormally when advancing the session normally](https://github.com/MoonshotAI/kimi-cli/issues/2587)**  
   *Author: Sdongmaker | Created: 2026-08-05 | Comments: 0*  
   A crash report on Windows (NT 10.0.26200) using K3 high model. The user reports an unexplained abnormal exit during normal session progression. No reproducer has been shared yet.

## Key PR Progress

1. **[#2592 — fix(soul): degrade unsupported tool media instead of aborting mid-task](https://github.com/MoonshotAI/kimi-cli/pull/2592)**  
   *Author: rainbowgore | Created: 2026-08-06*  
   Directly addresses the core of #2588: instead of raising `LLMNotSupported` after tool side effects, this PR degrades unsupported tool media gracefully, allowing the task to continue without a hard abort.

2. **[#2590 — fix(soul): name the config fix in the unsupported-capability error](https://github.com/MoonshotAI/kimi-cli/pull/2590)**  
   *Author: ayaangazali | Created: 2026-08-05*  
   The companion fix to #2588: improves the error message to explicitly tell the user which capability field to add to their `config.toml`. A small but high-impact UX improvement.

3. **[#2589 — docs: mention qwen-audio-agent as a voice ACP client](https://github.com/MoonshotAI/kimi-cli/pull/2589)**  
   *Author: x-lixu | Created: 2026-08-05*  
   A documentation-only PR adding the open-source full-duplex voice runtime `qwen-audio-agent` as an ACP client. The author discloses authorship, which is a good practice. Low risk, useful for voice-interface developers.

## Feature Request Trends
- **Persistent Memory System (#1283)** — the dominant ask, with 19 comments. Users want stateful personalization across sessions, both explicit (user-defined instructions) and implicit (AI-observed patterns). No milestone or assigned milestone yet, but the comment volume suggests this will eventually be prioritized.
- **ACP (Agent Client Protocol) ecosystem expansion** — the docs PR for `qwen-audio-agent` indicates a growing interest in voice-driven and alternative client interfaces for Kimi CLI, beyond traditional IDE extensions.

## Developer Pain Points
- **Tool side-effect safety (#2588, #2592)** — the abort-after-side-effect pattern is a serious trust issue. Developers rely on tools like MCP to mutate files or trigger workflows; aborting after mutating is disruptive and hard to debug.
- **Encoding corruption (#2591)** — rewriting file content during string replacement is a classic footgun. A targeted "edit in place with byte-range awareness" approach is needed to avoid touching untouched regions.
- **Windows stability (#2587)** — abnormal exits are hard to diagnose without core dumps or logs; likely the top platform-specific issue right now.
- **Actionable error messages (#2590)** — the community values errors that not only say *what* is wrong, but *how* to fix it. This is a recurring theme across tools, and the PR shows maintainers agree.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-06

## Today's Highlights

OpenCode shipped v1.18.14 with a simplified xAI device-code login flow and improved retry handling for transient provider errors, while the community's long-standing ask for an official VS Code extension (#11176) remains the most-thumbed open issue. The v2 engine migration is progressing steadily, with PRs landing for V1→V2 data migration and multiple cleanup refactors, alongside new complaints about session history wiping in `/sessions` after the latest update.

## Releases

**v1.18.14** — [Release notes](https://github.com/anomalyco/opencode/releases/tag/v1.18.14)
- **Core improvements:** Simplified xAI login to a single device-code flow that works better in headless and remote environments.
- **Bugfixes:** Preserved structured mid-stream provider errors so compatible providers can retry failed responses; retried more transient provider and network errors.

User reports indicate a **regression**: `/sessions` now wipes chat history and conversation context as soon as a new message is entered after switching sessions (see issue #40759 below).

---

## Hot Issues

1. **[#16017 — Feature: Add Go plan usage/balance API endpoint](https://github.com/anomalyco/opencode/issues/16017)** — 32 comments, 👍126. The community wants programmatic access to subscription usage data (dashboard-only today). High demand for automation/CI integration; has been open since March and is steadily gaining upvotes.

2. **[#11176 — Official OpenCode VS Code extension](https://github.com/anomalyco/opencode/issues/11176)** — 27 comments, 👍134. Long-running request (since January) with growing momentum. Users want native IDE integration beyond the TUI; top-voted issue overall.

3. **[#40759 — `/sessions` does not work anymore (regression)](https://github.com/anomalyco/opencode/issues/40759)** — Newly filed against v1.18.14. Switching sessions via the picker wipes chat history once a new message is entered. Critical bug, likely tied to the latest release; maintainers should triage quickly.

4. **[#39845 — DeepSeek V4 Flash suddenly requires "Enable models hosted in China"](https://github.com/anomalyco/opencode/issues/39845)** — 17 comments, 👍22. Mid-session breakage: model claims it's China-hosted and requires explicit opt-in unexpectedly. Confusing UX and silent behavior change; multiple users report the same.

5. **[#23153 — Feature: Pay Go with crypto](https://github.com/anomalyco/opencode/issues/23153)** — 16 comments, 👍36. Users want crypto payment support for OpenCode Go subscriptions, indicating demand for alternative payment rails and more flexible billing.

6. **[#34498 — Respect `disable-model-invocation: true` in SKILL.md frontmatter](https://github.com/anomalyco/opencode/issues/34498)** — 13 comments, 👍49. Parity request with Claude Code/Codex: skills that don't need model invocation shouldn't trigger it. Well-received feature request with clear spec.

7. **[#31932 — Cross-project session list/picker for TUI](https://github.com/anomalyco/opencode/issues/31932)** — 14 comments, 👍6. `/sessions` is scoped per-project; multi-repo users want a global view. Related to #35581; consistent ask across several threads.

8. **[#37564 — "Auto mode" LLM model classifier auto-approval for permissions](https://github.com/anomalyco/opencode/issues/37564)** — 6 comments, 👍12. Users want adaptive permission auto-approval based on task classification, similar to features in other agentic tools. Builds on prior discussion in #33585.

9. **[#31734 — Include ripgrep in Windows binary builds for offline environments](https://github.com/anomalyco/opencode/issues/31734)** — 3 comments, 👍4. Offline Windows users can't use ripgrep-based search; need bundled binaries. Recurring infrastructure pain point.

10. **[#40348 — Global AGENTS.md rules repeatedly forgotten across sessions](https://github.com/anomalyco/opencode/issues/40348)** — 2 comments. Users report OpenCode "forgets" global rules (e.g., 'no auto-commit') across sessions, forcing constant re-reminders. Trust-breaking behavior that erodes confidence in context management.

---

## Key PR Progress

1. **[#40723 — feat(core): migrate v1 data to v2](https://github.com/anomalyco/opencode/pull/40723)** — Major milestone: REST-triggered V1 session history migration with resumable progress, imports V2 session data and legacy JSON credentials. The v2 engine transition is the most significant ongoing effort.

2. **[#38790 — feat(app): add workspace flows to new layout](https://github.com/anomalyco/opencode/pull/38790)** — Adds Local/New/Existing workspace selection for new sessions with long-list search, branch context, and per-project defaults. Large UI/UX feature for the v2 app.

3. **[#40768 — fix(mcp): survive a cross-process OAuth refresh race on connect](https://github.com/anomalyco/opencode/pull/40768)** — Fixes #34520: two processes sharing one credential row can race on OAuth token refresh, causing one to fail with stale tokens. Important concurrency fix for MCP users.

4. **[#40769 — fix(mcp): reuse the registered dynamic client on re-login](https://github.com/anomalyco/opencode/pull/40769)** — Prevents unnecessary dynamic client re-registration on every login (fixes #40767). Complementary OAuth robustness improvement for V2 engine.

5. **[#40772 — fix(opencode): report a missing auth method instead of crashing](https://github.com/anomalyco/opencode/pull/40772)** — Adds guard against indexing into empty hook table in `ProviderAuth.authorize`; prevents crashes (fixes #40774). Correctness fix for edge-case provider configurations.

6. **[#40724 — refactor(plugin): split session HTTP hooks](https://github.com/anomalyco/opencode/pull/40724)** — Replaces single middleware registration with separate request/response hooks, simplifying plugin adaptation and migrating built-in OpenAI request rewrite. Cleaner plugin architecture.

7. **[#40765 — refactor(core): deduplicate Copilot endpoint routing](https://github.com/anomalyco/opencode/pull/40765)** — Uses shared GitHub Copilot endpoint-routing heuristic from `@opencode-ai/ai` instead of maintaining duplicate logic. Removes divergence risk.

8. **[#40764 — fix(desktop): embed version in server sidecar](https://github.com/anomalyco/opencode/pull/40764)** — Prevents beta sidecars from falling back to local builds and requesting `@opencode-ai/plugin@local`. Packaging fix with deployment implications.

9. **[#40763 — fix(tui): load sidebar project names sooner](https://github.com/anomalyco/opencode/pull/40763)** — Removes 300 ms delay before project labels appear in persisted tab titles. Small UX improvement, but reduces perceived sluggishness.

10. **[#38308 — feat(app): optional vertical tab rail](https://github.com/anomalyco/opencode/pull/38308)** — Opt-in vertical tab layout (Settings › General), resizable and collapsible. Addresses long-standing layout preference request (#36942); horizontal tabs remain default.

---

## Feature Request Trends

- **Streamlined authentication and billing**: Multiple threads around simplified logins (xAI device flow), crypto payments (#23153), and usage/balance APIs (#16017) show a focus on frictionless onboarding and metering.
- **Cross-project session management**: Recurring asks for global session pickers (#31932, #35581) and session status organization (#21590) indicate users work across repos and need better session hygiene.
- **Expanded IDE surface**: The VS Code extension (#11176) is the highest-voted feature; alongside desktop workflow improvements (#34004) and TUI usability enhancement, the community is pushing for richer client experiences.
- **Autocomplete improvements**: Several requests (mid-line slash commands #40719, skills in root autocomplete #40720, autocompleting skill invocations mid-prompt #40689, autocomplete for configured references #34040) reveal TUI typing efficiency as a hot area.
- **MCP ecosystem growth**: HTTP Streamable transport (#8058), sampling support (#11948), and new integrations like TaskMarket (#40722) point to OpenCode as a hub for agent tooling.

---

## Developer Pain Points

- **Context persistence failures**: Users repeatedly lose global rules (#40348) and are frustrated when session history is wiped by regressions (#40759). Reliability of context across sessions is a core trust issue.
- **Unexpected model availability changes**: Mid-session breakage when models suddenly require China-hosted opt-in (#39845) or return Forbidden errors (#40633) without clear explanation creates distrust in provider abstraction.
- **OAuth and auth races**: Cross-process OAuth refresh races (#34520, #40768) and missing dynamic client reuse (#40769) cause connection failures in multi-instance usage. These are getting fixed but represent recurring friction.
- **Desktop/packaging friction**: Windows users lacking bundled ripgrep (#31734) and laptop users unable to scroll settings to find updates (#40775) show incremental polish gaps in the desktop experience.
- **Windows/offline limitations**: Persistent asks for bundled binaries and better offline behavior (#31734) suggest enterprise users are adopting OpenCode in constrained environments.

---

*Data source: [github.com/anomalyco/opencode](https://github.com/anomalyco/opencode) — issues, PRs, and releases updated 2026-08-05 through 2026-08-06.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-06

## Today's Highlights
A significant wave of fixes landed today, addressing long-standing bugs like dangling OSC 8 hyperlinks in the TUI and an extension event-bus listener leak. The community also rallied around Windows support, with a dedicated issue collecting feedback to guide platform improvements. Key feature work progressed on `AGENTS.override.md` support, line ranges in `@file` references, and a new Qwen Token Plan provider.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[Windows Support Feedback ( #7547 )](https://github.com/earendil-works/pi/issues/7547)** — Open, 17 comments. A rallying point for Windows developers, asking how users run Pi on Windows to prioritize fixes. High engagement shows strong demand for better Windows support.

2. **[Config Folder on Linux ( #534 )](https://github.com/earendil-works/pi/issues/534)** — Closed, 14 comments, 23 👍. Requests XDG Base Directory compliance for the config folder. Long-standing issue with strong upvotes; closed but remains a notable community request.

3. **[TruncateToWidth Leaves Dangling OSC 8 Links ( #7399 )](https://github.com/earendil-works/pi/issues/7399)** — Closed, 12 comments. A subtle TUI bug where truncated output leaves hyperlinks open, breaking terminal rendering. Fixed today; good regression coverage added.

4. **[Ephemeral In-Session Model Changes ( #5263 )](https://github.com/earendil-works/pi/issues/5263)** — Open, 11 comments, 12 👍. Wants in-session model/thinking-level changes to be ephemeral by default, with a `/settings` entry for global defaults. Strongly requested for better UX.

5. **[Sessions Hang on "Working" ( #5291 )](https://github.com/earendil-works/pi/issues/5291)** — Closed, 8 comments. Anthropic Enterprise subscription users intermittently get stuck on "Working..." with no recovery. Impacts reliability perception; closed without a clear public resolution visible.

6. **[`pi update --self` Transient Failure ( #6675 )](https://github.com/earendil-works/pi/issues/6675)** — Closed, 8 comments. A single network failure aborts self-update. Minor but annoying; likely fixed with retry logic.

7. **[Configurable Thinking Level for Compaction ( #7553 )](https://github.com/earendil-works/pi/issues/7553)** — Open, 7 comments. Users want compaction to have its own thinking-level setting, separate from the session's, to avoid exploding summarization costs on reasoning models.

8. **[iTerm2 Inline Image Payload Size ( #7465 )](https://github.com/earendil-works/pi/issues/7465)** — Closed, 7 comments. `xterm.js` requires the `size` parameter in OSC 1337; without it images are silently rejected. Interop bug affecting embedding scenarios.

9. **[Vertex/GCP Metadata Server Support ( #5323 )](https://github.com/earendil-works/pi/issues/5323)** — Open, 6 comments. The auth check uses `existsSync` on credentials instead of the GCP metadata server, breaking environments without static credentials. Needs async metadata-server detection.

10. **[WebSocket Retry Only Handles Two Codes ( #7444 )](https://github.com/earendil-works/pi/issues/7444)** — Open, 4 comments. Other transient `response.failed` errors hard-stop the turn. Robustness gap in the Codex WebSocket layer.

## Key PR Progress

1. **[Close Truncated OSC 8 Links ( #7657 )](https://github.com/earendil-works/pi/pull/7657)** — Fixes #7399. Closes dangling hyperlinks on truncation; includes regression tests for the BEL-terminated case.

2. **[Skip OSC 8 Scan for Plain Prefixes ( #7665 )](https://github.com/earendil-works/pi/pull/7665)** — Follow-up optimization that avoids per-character ANSI parsing for ordinary truncated text, preserving the new fix.

3. **[Fix Event Bus Leak ( #7656 )](https://github.com/earendil-works/pi/pull/7656)** — Fixes #7193. Scopes `pi.events.on()` subscriptions to the extension runtime. Prevents stale listeners after session reloads.

4. **[Support `AGENTS.override.md` ( #7681 )](https://github.com/earendil-works/pi/pull/7681)** — Closes #7642. Loads `AGENTS.override.md` as the highest-priority context file per directory; ancestor layering preserved.

5. **[Support `AGENTS.override.md` ( #7664 )](https://github.com/earendil-works/pi/pull/7664)** — Companion PR: prefers the override over `AGENTS.md` and `CLAUDE.md` including global dir, with docs.

6. **[Support Line Ranges in `@file` References ( #7679 )](https://github.com/earendil-works/pi/pull/7679)** — Adds 1-based inclusive `#L<start>-L<end>` selectors for CLI references; preserves literal filenames, rejects image ranges.

7. **[Qwen Token Plan Individual Provider ( #7659 )](https://github.com/earendil-works/pi/pull/7659)** — Adds built-in provider with `QWEN_TOKEN_PLAN_API_KEY` and eight documented models; still open for review.

8. **[Replace Qwen 3.8 Max Preview ( #7670 )](https://github.com/earendil-works/pi/pull/7670)** — Swaps the preview model for GA `qwen3.8-max` with reasoning-effort mapping (`low`/`medium`/`xhigh`).

9. **[Restore Copilot Models from Account Policy ( #7672 )](https://github.com/earendil-works/pi/pull/7672)** — Fixes empty model lists by falling back to policy-enabled models when strict picker data is empty; keeps non-Individual accounts strict.

10. **[Naturally Sort Model Selectors ( #7692 / #7690 )](https://github.com/earendil-works/pi/pull/7692)** — Shared case-insensitive, numeric-aware comparator for both `/model` and `/scoped-models`, addressing confusing `@1m` vs `@200k` ordering.

## Feature Request Trends
- **Model selector UX**: Multiple issues call for natural sorting, ephemeral in-session changes, and scoped/context-window options to reduce friction when switching models.
- **Context file flexibility**: Users want `AGENTS.override.md` for per-directory overrides and file references with line ranges to avoid sending whole files.
- **Provider breadth**: New Qwen Token Plan support and improved Vertex/GCP metadata detection reflect demand for more cloud/enterprise providers.
- **TUI polish**: Requests for mouse-event routing and zero-width fill markers show interest in richer terminal extensions.

## Developer Pain Points
- **Windows on-ramp**: A dedicated issue with 17 comments highlights confusion about supported Windows setups and where to focus fix energy.
- **Reliability interruptions**: Stuck "Working..." turns, WebSocket retry gaps, and self-update failures erode trust in long-running sessions.
- **Compaction costs**: Lack of a dedicated thinking budget for compaction on reasoning models makes summaries unexpectedly expensive.
- **Terminal/embedding interop**: OSC 8 hyperlink truncation and iTerm2/xterm.js image interoperability remain common sources of breakage.

---

*Data from [github.com/badlogic/pi-mono](https://github.com/earendil-works/pi)*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-06

## Today's Highlights

The Qwen Code team shipped **desktop-v0.1.0**, the first Tauri-based desktop release, alongside nightly and stable updates that include experimental native Live Voice support for WebShell on macOS. Security remains a focal point this week, with a P1 read-only shell classifier bypass discovered and multiple trust-boundary hardening PRs in flight. The community is actively shaping the desktop roadmap, pushing for a low-maintenance Web Shell wrapper and deprecating the Electron app in favor of the Tauri shell.

## Releases

**desktop-v0.1.0** — Initial Tauri-based desktop release ([changelog](https://github.com/QwenLM/qwen-code/releases/tag/desktop-v0.1.0)). CI fixes for the qwen-triage workflow. This marks the strategic pivot away from the Electron desktop app.

**v0.21.6** — Stable release with Web Shell improvements: conversation turns now stay expanded during active background work, and macOS users get experimental native Live Voice support via a global shortcut ([#7859](https://github.com/QwenLM/qwen-code/pull/7859)).

**v0.21.6-nightly.20260806.cb3dc107f** — Nightly with a single test fix: deflaked the glob external-path test by using a dedicated empty directory instead of `/tmp` ([#8604](https://github.com/QwenLM/qwen-code/pull/8604)).

## Hot Issues

1. **[#8582 — Read-only shell classifier bypass (P1, Security)](https://github.com/QwenLM/qwen-code/issues/8582)** — The read-only shell classifier auto-approves command substitution hidden by line continuation or `${var@P}` expansion. This is a critical security gap: commands that execute arbitrary code pass the safety gate. 4 comments, active discussion on remediation.

2. **[#8615 — Desktop 0.1.0 crashes on Windows startup (P1)](https://github.com/QwenLM/qwen-code/issues/8615)** — Bundled runtime crashes with `EISDIR lstat 'C:'` when opening a workspace on Windows 11. A launch-blocker for the new desktop release.

3. **[#8136 — Provider warning sanitizer leaks passwords (P2, Security)](https://github.com/QwenLM/qwen-code/issues/8136)** — `sanitizeProviderWarning` truncates messages containing ports and can leak passwords containing `@`. Credential exposure in `/status` payloads is a serious concern; 8 comments show strong community engagement.

4. **[#8532 — CI logs fake disk-full errors (P2, Testing)](https://github.com/QwenLM/qwen-code/issues/8532)** — Error-path unit tests print production-looking "disk full" messages to stderr, confusing CI triage and making real ENOSPC failures harder to spot.

5. **[#8550 — `qwen mcp list` hangs indefinitely on SSE servers (P2)](https://github.com/QwenLM/qwen-code/issues/8550)** — MCP list command hangs forever when an SSE server never emits the legacy `endpoint` event. No timeout guard exists; marked ready-for-agent.

6. **[#8538 — Copy-response button broken on Windows (P2, UI)](https://github.com/QwenLM/qwen-code/issues/8538)** — Desktop 0.0.5 on Windows 10: clipboard remains unchanged after clicking copy. Reproduced across restarts and reboots.

7. **[#8560 — Web Shell 401 on session deep-link refresh (P2, Auth)](https://github.com/QwenLM/qwen-code/issues/8560)** — Refreshing a `/session/<id>` URL returns Unauthorized when `qwen serve` has a bearer token. Session continuity breaks with auth enabled.

8. **[#8562 — TUI flickers in tmux via SSH (P2, Linux)](https://github.com/QwenLM/qwen-code/issues/8562)** — Chinese-language report of continuous screen flashing in tmux splits when connecting via iTerm2 → SSH → Ubuntu → tmux. User used Qwen 3.8 Max to diagnose; points to recent version regressions.

9. **[#8580 — TUI flickers in tmux < 3.5 (P2, Rendering)](https://github.com/QwenLM/qwen-code/issues/8580)** — Complimentary root-cause analysis: every overflowing frame triggers full-screen clear+repaint guarded only by unqueried DEC 2026. Definitively scoped to tmux < 3.5.

10. **[#8606 — VSCode companion file links broken for nested files (P2)](https://github.com/QwenLM/qwen-code/issues/8606)** — Edit/Write file links resolve to `<workspace-root>/<basename>`, causing "file not found" for any nested path. Breaks the core edit loop in VSCode.

## Key PR Progress

1. **[#8612 — fix(autofix): ship core dist in the review CLI bundle](https://github.com/QwenLM/qwen-code/pull/8612)** — Fixes the review CLI bundle missing the core package build output, which caused fan-out legs to fail at restore time.

2. **[#8614 — feat(web-shell): fullscreen view for the right artifact panel](https://github.com/QwenLM/qwen-code/pull/8614)** — Adds expand/collapse toggle to the panel showing artifacts, subagents, review changes, monitors, and scheduled tasks.

3. **[#8613 — feat(web-shell): tmux-backed interactive terminal sub-agent](https://github.com/QwenLM/qwen-code/pull/8613)** — Lets agents run interactive CLIs (REPLs, TUI apps) inside a tmux session on the daemon host, with a live terminal view in Web Shell. Major capability expansion.

4. **[#8396 — fix(hooks): close four trust-boundary holes in hook execution](https://github.com/QwenLM/qwen-code/pull/8396)** — HTTP hooks no longer follow redirects; DNS-level SSRF checks enforced; three other boundary holes closed where repo config meets code execution or network egress.

5. **[#8388 — feat(review): capture-tui — pixel-level rendering evidence (Phase 2)](https://github.com/QwenLM/qwen-code/pull/8388)** — Verifiers can now drive code in a private tmux server and capture exact rendering ("the panel clips at 80 columns" gets pixel proof, not prose).

6. **[#8578 — feat(channels): Feishu ask-user question cards](https://github.com/QwenLM/qwen-code/pull/8578)** — Native Feishu Card V2 for `ask_user_question` interactions with single/multi-select forms and callback correlation.

7. **[#8565 — fix(dingtalk): continuous and attributable status cards](https://github.com/QwenLM/qwen-code/pull/8565)** — Each DingTalk task run gets one continuous status card that streams output across response boundaries, with elapsed-time refresh during idle.

8. **[#8559 — feat(web-shell): parallel agent activity feedback](https://github.com/QwenLM/qwen-code/pull/8559)** — Parallel subagent status stays at conversation tail, auto-expands during activity, and collapses gracefully before the main agent resumes.

9. **[#8332 — feat(cli): audio bridge for attachments](https://github.com/QwenLM/qwen-code/pull/8332)** — Transcribes audio attachments through a batch voice model when the primary model lacks audio support; marks results as explicitly untrusted machine transcription.

10. **[#8241 — fix(qqbot): restore per-group session isolation](https://github.com/QwenLM/qwen-code/pull/8241)** — Removes the forced `sessionScope: 'single'` override that broke per-group isolation for QQ Bot under thread scope.

## Feature Request Trends

- **Phone access and remote control** — Two separate requests ([#8595](https://github.com/QwenLM/qwen-code/issues/8595), [#8092](https://github.com/QwenLM/qwen-code/issues/8092)) push for QR-code pairing and Web Shell reuse for phone/desktop access to local sessions.
- **Desktop consolidation** — Strong community signal to [deprecate the Electron app and rename desktop-shell to desktop](https://github.com/QwenLM/qwen-code/issues/8596); parallel effort to [build the lower-maintenance Web Shell wrapper](https://github.com/QwenLM/qwen-code/issues/8092).
- **Async and batch execution** — Requests for a [ `/slow` batch mode](https://github.com/QwenLM/qwen-code/issues/8605) for lower-cost asynchronous agent runs and [background Agent recovery tracking](https://github.com/QwenLM/qwen-code/issues/8586).
- **SDK and integration hooks** — Community wants [inline hooks config in TS SDK `query()`](https://github.com/QwenLM/qwen-code/issues/8591) and broader i18n coverage ([Korean docs](https://github.com/QwenLM/qwen-code/issues/8551)).

## Developer Pain Points

- **TUI rendering instability** — Three separate issues report flickering or duplicate output in tmux and terminal resize scenarios ([#8562](https://github.com/QwenLM/qwen-code/issues/8562), [#8557](https://github.com/QwenLM/qwen-code/issues/8557), [#8580](https://github.com/QwenLM/qwen-code/issues/8580)). The tmux < 3.5 root-cause analysis makes this a priority fix.
- **CI reliability eroding trust** — Mocked error tests polluting logs ([#8532](https://github.com/QwenLM/qwen-code/issues/8532)), /review runs burning full 360-minute timeouts ([#8597](https://github.com/QwenLM/qwen-code/issues/8597)), and flaky glob tests undermine confidence in CI signals.
- **Desktop polish gaps** — Copy buttons that don't work ([#8538](https://github.com/QwenLM/qwen-code/issues/8538)), markdown links that don't open ([#8593](https://github.com/QwenLM/qwen-code/issues/8593)), and language settings with no effect ([#8592](https://github.com/QwenLM/qwen-code/issues/8592)) mark the desktop app as still maturing.
- **Security edge cases keep surfacing** — From password leaks in sanitizers ([#8136](https://github.com/QwenLM/qwen-code/issues/8136)) to shell classifier bypasses ([#8582](https://github.com/QwenLM/qwen-code/issues/8582)), the community is actively probing trust boundaries — and finding real gaps.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-06

## 1. Today's Highlights

The DeepSeek TUI community is deeply engaged in the v0.9.4 release cycle, with a 77-commit integration train (#5135) bringing substantial Runtime API expansions, including new memory, MCP, goal-loop, skill, and verifier-receipt endpoints. Critical bug fixes address terminal scrolling (#5234), a blocking cursor query race condition via ratatui pinning (#5192), and Windows linker argument escaping for OpenHarmony SDKs (#5095). Community momentum is strong, with a new Chinese-language Windows beginner guide (#5229) and an ACP tool-execution feature (#5225) that upgrades code assistants from chat-only to full code-editing agents.

## 2. Releases

No new releases in the last 24 hours. The community is awaiting v0.9.4, currently in the integration train (#5135) with 77 commits ahead of main.

## 3. Hot Issues

1. **[#4029] Reasonix-like Interface Inquiry** — [Link](https://github.com/Hmbown/CodeWhale/issues/4029)  
   Community member asks whether a Reasonix-style UI is planned. Active discussion (4 comments) suggests ongoing interest in alternative interface paradigms.

2. **[#5005] Sandbox Path Whitelist for Logs and Build Artifacts** — [Link](https://github.com/Hmbown/CodeWhale/issues/5005)  
   `sandbox_mode = "workspace-write"` blocks Xcode build artifacts under `~/Library/Developer/Xcode/DerivedData/`. Closed, but resonated with mobile/desktop developers needing external log access.

3. **[#5250] Multi-Provider API Key Storage** — [Link](https://github.com/Hmbown/CodeWhale/issues/5250)  
   Users juggling DeepSeek and GLM must re-enter API keys on every model switch. High friction for multi-provider workflows; community suggests per-provider key persistence.

4. **[#5244] Silent Context Window Degradation** — [Link](https://github.com/Hmbown/CodeWhale/issues/5244)  
   Unknown model IDs silently fall back to the 128K legacy context window—a 1M-window model compacts at 128K with no warning. Residual bug from #5239, flagged by maintainer Hmbown.

## 4. Key PR Progress

1. **[#5135] v0.9.4 Release Train** — [Link](https://github.com/Hmbown/CodeWhale/pull/5135)  
   The complete v0.9.4 integration train, 77 commits ahead of main, containing all release candidates; supersedes #5044.

2. **[#5225] ACP Tool Execution** — [Link](https://github.com/Hmbown/CodeWhale/pull/5225)  
   Exposes file/search/git/patch/shell tools over `session/prompt`, transforming ACP from chat-only to real code-editing agent for Zed and third-party bridges.

3. **[#5131] Memory API Endpoints** — [Link](https://github.com/Hmbown/CodeWhale/pull/5131)  
   Adds `/v1/memory` routes for bounded inspection and lifecycle controls, closing a major gap for managed clients.

4. **[#5130] MCP Server Configuration API** — [Link](https://github.com/Hmbown/CodeWhale/pull/5130)  
   Adds POST/update/delete routes for MCP server management—no more hand-editing TOML/JSON.

5. **[#5133] Goal-Loop State API** — [Link](https://github.com/Hmbown/CodeWhale/pull/5133)  
   Exposes active-goal state and lifecycle transitions via `/v1/threads/{id}/goal`.

6. **[#5132] Verifier Receipts API** — [Link](https://github.com/Hmbown/CodeWhale/pull/5132)  
   Beyond the aggregate failure counter: lists durable task receipts, failure details, and retry guidance.

7. **[#5129] Skill Lifecycle API** — [Link](https://github.com/Hmbown/CodeWhale/pull/5129)  
   Full skill management over HTTP—install, update, uninstall, trust, audit—mirroring TUI capabilities.

8. **[#5240] Real Wait Time in Tool Content** — [Link](https://github.com/Hmbown/CodeWhale/pull/5240)  
   Surface actual `duration_ms` in Bash wait results so models can distinguish short waits from multi-minute stalls, preventing busy-poll loops.

9. **[#5242] Resume Interrupted Subagents** — [Link](https://github.com/Hmbown/CodeWhale/pull/5242)  
   Enables checkpoint-based resume of interrupted children via `agents/followup`—previously queued as dead-letter.

10. **[#5234] Mouse Capture Scroll Fix** — [Link](https://github.com/Hmbown/CodeWhale/pull/5234)  
    Fixes transcript scrolling when mouse capture is active; wheel input was incorrectly toggling composer history due to DECSET interaction.

11. **[#5192] ratatui 0.30.0 Pin** — [Link](https://github.com/Hmbown/CodeWhale/pull/5192)  
    Pins `ratatui-core` to prevent blocking CPR queries that race the event loop at startup.

12. **[#5095] Windows Linker Space Handling** — [Link](https://github.com/Hmbown/CodeWhale/pull/5095)  
    Re-quotes OpenHarmony linker arguments containing spaces, fixing `--sysroot` splitting for SDKs in spaced paths like `D:\DevEco Studio\...`.

13. **[#5229] Chinese Windows Beginner Guide** — [Link](https://github.com/Hmbown/CodeWhale/pull/5229)  
    New `docs/WINDOWS_BEGINNER.zh-CN.md` covering install, config, model switching, permissions, and common issues—validated on Windows 10.

14. **[#5236] Model Studio Live Proof** — [Link](https://github.com/Hmbown/CodeWhale/pull/5236)  
    Adds video/screenshot evidence for #5203 demonstrating `qwen3.8-max` reasoning-to-working transitions on Alibaba Cloud Model Studio.

## 5. Feature Request Trends

- **Runtime API expansion** dominates: memory inspection, MCP management, goal-loop control, skill lifecycle, and verifier receipts—managed clients are demanding parity with TUI capabilities (PRs #5131, #5130, #5133, #5132, #5129).
- **Multi-provider support**: Separate API key storage per provider (#5250) and tool execution over ACP (#5225) point toward a multi-model, bridge-friendly future.
- **Awareness & transparency**: Surface fallback context windows (#5244) and real wait times (#5240) show demand for honest model-state feedback.
- **Cross-platform robustness**: Windows path handling (#5095) and Chinese documentation (#5229) indicate a growing non-Unix community.

## 6. Developer Pain Points

- **Silent degradation**: Unknown model IDs silently fall back to 128K context (1M-window models compacted), wasting tokens and confusing users (#5244).
- **Key management friction**: One API key slot forces re-entry when switching providers like DeepSeek and GLM—a daily annoyance for multi-model developers (#5250).
- **Sandbox restrictions blocking workflows**: Xcode and other build tools write logs/artifacts outside the workspace, and workspace-write mode blocks access (#5005).
- **Terminal interaction bugs**: Mouse capture breaking scroll (#5234) and blocking CPR queries at startup (#5192) disrupt the core TUI experience.
- **Context-blind tool calls**: Models cannot see wait durations in Bash results, leading to poor polling behavior and wasted cycles (#5240).
- **Unrecoverable interrupted tasks**: Long-running subagent tasks had no resume path—checkpoint data existed but nothing could restart them (#5242).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*