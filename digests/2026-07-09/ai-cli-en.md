# AI CLI Tools Community Digest 2026-07-09

> Generated: 2026-07-09 01:29 UTC | Tools covered: 9

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
**Date:** 2026-07-09

## 1. Ecosystem Overview

The AI CLI tool landscape is experiencing a turbulent growth phase marked by rapid iteration, platform parity challenges, and escalating cost concerns. Seven major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI—are competing for developer mindshare, each advancing distinct architectural philosophies from agent-first designs to TUI-centric workflows. A consistent theme across all ecosystems is the tension between powerful autonomous agent capabilities and the lack of guardrails for cost, safety, and resource consumption. The community is increasingly vocal about token consumption transparency, sub-agent reliability, and enterprise deployment friction, signaling a maturation from novelty-seeking to production-readiness demands.

## 2. Activity Comparison

| Tool | Hot Issues (24h) | PR Activity (24h) | Releases (24h) | Overall Velocity |
|------|-----------------|-------------------|----------------|------------------|
| **Claude Code** | 10 active (3 critical) | 6 open | ✅ v2.1.205 | Moderate; patch cycle |
| **OpenAI Codex** | 10 active (2 critical) | 10 reviewed | ✅ rust-v0.143.0 | High; major release + alpha |
| **Gemini CLI** | 10 active (2 security) | 10 open | ✅ v0.50.0 + preview | High; dual-track releases |
| **GitHub Copilot CLI** | 10 active | 0 meaningful | ❌ None | Low; maintenance mode |
| **Kimi Code CLI** | 1 active | 0 | ❌ None | Very low; stalled |
| **OpenCode** | 10 active (2 closed) | 10 open | ❌ None | High; V2 stabilization |
| **Pi** | 10 active (7 closed) | 6 (all closed) | ❌ None | Moderate; bug-fix focused |
| **Qwen Code** | 10 active | 10 open | ✅ v0.19.8 | High; steady feature delivery |
| **DeepSeek TUI** | 10 active (7 closed) | 10 active | ❌ None | Very high; 10+ PRs/day |

**Key insight:** DeepSeek TUI leads in raw velocity, OpenAI Codex and Gemini CLI in release sophistication. GitHub Copilot CLI and Kimi Code CLI show minimal development activity.

## 3. Shared Feature Directions

| Theme | Tools Demanding | Specific Needs |
|-------|----------------|----------------|
| **Cost Controls & Token Transparency** | Claude Code, OpenAI Codex, Gemini CLI, Pi, OpenCode | Per-agent budgets, token usage dashboards, runaway detection, pricing transparency |
| **Sub-Agent Reliability** | Claude Code, Gemini CLI, OpenCode, Qwen Code, DeepSeek TUI | Hanging/freezing agents, infinite loops, recovery logic masking failures, lack of kill switches |
| **Windows Platform Parity** | Claude Code, OpenAI Codex, OpenCode, Qwen Code, Kimi Code CLI | Auth failures, sandbox setup issues, IME/CJK problems, Cowork missing, extension install failures |
| **Enterprise/Proxy Support** | OpenAI Codex, Kimi Code CLI, Gemini CLI, GitHub Copilot CLI, Qwen Code | SSL interception bypass, system proxy routing, corporate network compatibility, BYOK support |
| **Session Lifecycle Management** | Claude Code, GitHub Copilot CLI, OpenCode, Pi, Qwen Code | Stuck background agents, context compression transparency, undo/cancel controls, session resumption |
| **Memory/Context Persistence** | OpenAI Codex, Qwen Code, Gemini CLI, Pi | Memory index staleness, compaction data loss, topic-based memory directories, configurable retention |
| **Plugin/Extension Ecosystem** | Claude Code, OpenAI Codex, GitHub Copilot CLI, DeepSeek TUI | Custom slash commands, distributable workflows, marketplace discovery, sandboxed sub-agent tools |
| **Multi-Session Concurrency** | Pi, DeepSeek TUI, Qwen Code | Background agent switching without teardown, parallel workspaces, concurrent agent sessions |

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Kimi Code CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|-------------------|---------------|----------|-----|-----------|--------------|
| **Primary UX** | TUI + Cowork | CLI + Desktop App | CLI + Agent | TUI | Basic CLI | Full Desktop App | TUI | WebShell + CLI | TUI-only |
| **Agent Philosophy** | Hierarchical (Opus Advisor) | Managed sub-agents | Generalist + Specialists | Skills-based | Basic | Sub-agent tasks | Agent sessions | Daemon + channels | Fleet profiles |
| **Cost Model** | Token-based, opaque | Rate-limit, opaque | Free-tier + Pro | Subscription | Unknown | Zen (free) + Pro | Token-based | Token-based | Token-based |
| **Key Differentiator** | Agent orchestration | Remote plugins + proxy | Security/CI focus | GitHub integration | Simplicity | Desktop V2 + MCP | TUI polish | Channel platform | Velocity & scale |
| **Platform Maturity** | macOS > Windows | macOS > Windows | Cross-platform | macOS > Windows | Unknown | macOS + Windows | macOS + Linux | Cross-platform | Linux/macOS |
| **Community Culture** | Feature-rich but vocal | Enterprise push | Security-conscious | Stable, low-velocity | Stalled | Active V2 rebuild | Bug-fix cycle | Steady delivery | Hyperactive |

**Strategic note:** OpenAI Codex differentiates on enterprise networking (proxy routing), Claude Code on agent hierarchy (Opus Advisor), Gemini CLI on security practices (A2A RCE fix, CI verification), and DeepSeek TUI on raw iteration velocity. GitHub Copilot CLI relies on inertia and GitHub integration.

## 5. Community Momentum & Maturity

### High Momentum (Rapid Iteration)
- **DeepSeek TUI** — 10+ PRs/day, v0.8.68 with 10+ closed PRs, community contributor JayBeest landing major feature. Highest raw velocity but potential for burnout ("CodeWhale tsunami").
- **OpenCode** — V2 stabilization surge, high community engagement (96 👍 on usage API request), actively closing major feature requests (MCP capabilities).
- **OpenAI Codex** — Major release v0.143.0 with enterprise features, dual alpha tracks, but GPT-5.5 regression threatens user trust.
- **Gemini CLI** — Dual stable/preview release track, critical security fixes, robust evaluation infrastructure (76 tests across 6 models).

### Moderate Momentum (Steady Maintenance)
- **Claude Code** — Patch cycle continues but token consumption crisis (#42249, 38 comments) unresolved after 3 months. Community patience wearing thin.
- **Pi** — Targeted bug-fix focus, 7 closed issues in 24h, but low feature velocity. Model compatibility problems accumulating.
- **Qwen Code** — Consistent releases (v0.19.8), strong channel platform expansion, but Windows issues and CI fragility persist.

### Low Momentum (Stalled/Declining)
- **GitHub Copilot CLI** — No releases, zero meaningful PRs, active issues like Gatekeeper (#970, 21 👍) and infinite loops (#3158) unresolved. Ecosystem coasting on inertia.
- **Kimi Code CLI** — Single active issue, zero PR activity, no releases. Effectively dormant for enterprise users.

## 6. Trend Signals

### Critical Industry Trends

1. **Cost Crisis is the #1 Pain Point:** Three Claude Code top-10 issues and OpenAI Codex's rate-limit regression signal that token-based pricing without transparency and guardrails is unsustainable for production use. Expect tools to add per-agent budgets, real-time TPS tracking (OpenCode #6096, 60 👍), and automated cost alerts.

2. **Sub-Agent Safety is Underserved:** Every multi-agent tool reports hanging, infinite loops, or recovery masking failures. The industry needs standardized sub-agent lifecycle management — kill switches, timeout policies, and failure transparency. DeepSeek TUI's tool sandboxing (#4042) is a promising direction.

3. **Enterprise Compliance is the Adoption Gate:** OpenAI Codex's proxy routing, Gemini CLI's security fixes, and Kimi Code CLI's SSL interception issue all point to enterprise IT requirements as the rate-limiting step for widespread adoption. Tools without SOC2, proxy support, and certificate flexibility will stall at scale.

4. **Windows Remains Second-Class:** Six of nine tools have active Windows-specific issues. This is a known gap but persists — likely because most AI CLI developers target macOS/Linux. Expect Windows parity to become a competitive differentiator once enterprise adoption accelerates.

5. **Memory & Context Management is the Next Frontier:** Multiple tools (Qwen Code, OpenAI Codex, Gemini CLI) face memory index staleness, compaction data loss, and unbounded retention. As sessions grow longer and agent workflows more complex, intelligent memory pruning and transparent compression will become table stakes.

6. **Platform Economics are Shifting:** The rise of "free" tiers (OpenCode Zen, Gemini free model) and Bring-Your-Own-Key models suggests the market is moving away from proprietary pricing lock-in. Users increasingly demand cost flexibility — pay-per-token, subscription, or self-hosted.

### Developer Recommendations

- **If you prioritize cost control:** Monitor Claude Code's #42249 and OpenAI Codex's #31668. Consider Gemini CLI's budget-friendly track.
- **If you deploy on Windows:** Evaluate OpenCode's PowerShell UTF-8 fix (#31985) and Qwen Code's Windows extension fixes (#6545). Avoid Claude Code and GitHub Copilot CLI for Windows teams.
- **If you need enterprise compliance:** OpenAI Codex v0.143.0's proxy support is market-leading. Gemini CLI's security culture is strong. Kimi Code CLI is not enterprise-ready.
- **If you build agent-heavy workflows:** DeepSeek TUI's velocity and DeepSeek TUI's sub-agent sandboxing are cutting-edge, but expect instability. Claude Code's hierarchical agent model is more mature.
- **If you want stability:** GitHub Copilot CLI is dormant but stable. OpenCode V2 is stabilizing but still in transition.

**Bottom line:** The AI CLI tool ecosystem is entering a consolidation phase where cost transparency, enterprise compliance, and sub-agent reliability will separate winners from also-rans. DeepSeek TUI leads on innovation velocity; OpenAI Codex leads on enterprise readiness; Claude Code leads on agent sophistication but risks user trust if cost issues remain unaddressed.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-09 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The most-discussed Skill submissions by community attention:

### #1 — Skill-Creator Fix: Run_eval 0% Recall Bug
**PR #1298** ([link](https://github.com/anthropics/skills/pull/1298)) | *Open* | MartinCajiao
Fixes the core evaluation pipeline where `run_eval.py` consistently reports `recall=0%` for every skill description, rendering the description-optimization loop ineffective. The fix installs the eval artifact as a real skill, corrects Windows stream-reading, improves trigger detection, and fixes parallel worker behavior. **Discussion impact:** Addresses the single most-cited blocker (Issues #556, #1169, #1061) affecting the skill-creator meta-skill—10+ independent reproductions reported. Merging this would unblock the entire skill optimization workflow.

### #2 — Document Typography Skill
**PR #514** ([link](https://github.com/anthropics/skills/pull/514)) | *Open* | PGTBoos
Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Targets universal document-quality issues that affect every Claude-generated output. **Discussion highlights:** Community strongly supports as a "must-have" baseline skill—users note these typographic issues are pervasive but rarely requested explicitly. High practical value for professional document generation.

### #3 — Testing-Patterns Skill
**PR #723** ([link](https://github.com/anthropics/skills/pull/723)) | *Open* | 4444J99
A comprehensive testing skill covering the Testing Trophy model, unit testing (AAA pattern, edge cases), React component testing with Testing Library, and E2E patterns. **Discussion highlights:** Fills a clear gap in the Skills ecosystem—no existing skill covers the full testing stack. Community sees this as essential for production code quality.

### #4 — ODT Skill (OpenDocument Format)
**PR #486** ([link](https://github.com/anthropics/skills/pull/486)) | *Open* | GitHubNewbie0
Enables creation, filling, reading, and conversion of `.odt` and `.ods` files—the native format for LibreOffice and many open-source workflows. **Discussion highlights:** Addresses demand from enterprise users and open-source advocates who cannot use proprietary formats. Multiple commenters noted interoperability gaps with existing document skills.

### #5 — Self-Audit Skill (v1.3.0)
**PR #1367** ([link](https://github.com/anthropics/skills/pull/1367)) | *Open* | YuhaoLin2005
A two-stage output verification skill: mechanical file existence checks followed by a four-dimension reasoning audit (damage-severity prioritized). Universal across projects and tech stacks. **Discussion highlights:** Newest high-engagement PR; community interested in the proactive quality-gate approach. Some discussion around whether this overlaps with built-in verification.

### #6 — Color-Expert Skill
**PR #1302** ([link](https://github.com/anthropics/skills/pull/1302)) | *Open* | meodai
Comprehensive color knowledge skill covering naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway, CSS named), color spaces with "what to use when" guidance, accessibility contrast rules, and cultural color associations. **Discussion highlights:** Niche but highly specialized; received attention for its depth of color science expertise.

### #7 — Frontend-Design Skill Improvement
**PR #210** ([link](https://github.com/anthropics/skills/pull/210)) | *Open* | justinwetch
Revises the frontend-design skill for clarity and actionability—ensuring every instruction is executable within a single conversation. **Discussion highlights:** Community feedback centered on the challenge of making design guidance specific enough to steer Claude's behavior without being overly prescriptive.

---

## 2. Community Demand Trends

From the most-commented Issues, the community's most-anticipated Skill directions are:

| Trend | Evidence | Key Issue |
|-------|----------|-----------|
| **Security & Trust Boundaries** | #492 (34 comments)—community demands clear security boundaries for community-contributed skills distributed under the `anthropic/` namespace. Users want official vs. community skill labeling and permission gating. | [#492](https://github.com/anthropics/skills/issues/492) |
| **Org-Wide Skill Sharing** | #228 (14 comments)—enterprise users need centralized skill distribution without manual file transfers. Currently no mechanism for team-wide skill libraries. | [#228](https://github.com/anthropics/skills/issues/228) |
| **Skill-Creator Reliability** | #556 (12 comments), #1061 (3 comments), #1169 (3 comments)—the skill optimization pipeline (`run_eval.py`) is effectively broken. This is the #1 infrastructure blocker for Skill authors. | [#556](https://github.com/anthropics/skills/issues/556) |
| **Agent Governance / Safety** | #412 (6 comments)—proposal for governance patterns: policy enforcement, threat detection, trust scoring, audit trails. Growing concern as agents become more autonomous. | [#412](https://github.com/anthropics/skills/issues/412) |
| **Compact Agent Memory** | #1329 (9 comments)—proposal for symbolic notation to reduce context overhead from long-running agent memory/notes. Addresses the practical cost of verbose agent state. | [#1329](https://github.com/anthropics/skills/issues/1329) |
| **Duplicate Skills / Plugin Conflicts** | #189 (6 comments)—identical skills installed via different plugins waste context window. Community wants deduplication and clearer role boundaries between skill collections. | [#189](https://github.com/anthropics/skills/issues/189) |

---

## 3. High-Potential Pending Skills

These active-comment PRs are not yet merged but show strong momentum toward landing:

| PR | Skill | Last Activity | Probability Assessment |
|----|-------|---------------|-----------------------|
| [#1298](https://github.com/anthropics/skills/pull/1298) | Skill-Creator `run_eval.py` fix | 2026-06-23 | **High**—critical infrastructure fix, multiple maintainer comments |
| [#1367](https://github.com/anthropics/skills/pull/1367) | Self-audit (mechanical + reasoning) | 2026-07-02 | **Medium-High**—recent activity, universal applicability |
| [#1323](https://github.com/anthropics/skills/pull/1323) | Skill-Creator trigger detection fix | 2026-06-25 | **High**—solves same root cause as #1298, complementary |
| [#1261](https://github.com/anthropics/skills/pull/1261) | Skill-Creator command file isolation | 2026-07-08 | **High**—fixes parallel eval corruption, most recently updated |
| [#1099](https://github.com/anthropics/skills/pull/1099) | Skill-Creator Windows crash fix | 2026-05-24 | **Medium**—Windows-specific, part of a fix cluster |
| [#723](https://github.com/anthropics/skills/pull/723) | Testing-patterns skill | 2026-04-21 | **Medium**—no recent activity, but high community demand |
| [#514](https://github.com/anthropics/skills/pull/514) | Document typography | 2026-03-13 | **Medium-Low**—stale but no objections raised |

**Key insight:** Four of the seven high-potential PRs are `skill-creator` fixes, reflecting that the community's immediate priority is making the Skill authoring pipeline functional before adding new Skills.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is fixing the skill-creator meta-skill's evaluation pipeline—specifically the `run_eval.py` 0% recall bug—which currently blocks all Skill description optimization and has become the ecosystem's critical bottleneck, with 5+ interdependent PRs and 3+ dedicated Issues (total 18+ comments) all converging on the same root causes: subprocess handling, trigger detection, and parallel worker isolation on both Unix and Windows.**

---

# Claude Code Community Digest — 2026-07-09

## Today's Highlights
A minor patch (v2.1.205) shipped fixing JSON schema handling and session transcript tampering. The community continues to report severe token consumption issues as the dominant friction point, with multiple open threads on runaway agent costs and opaque billing. A new cluster of Windows-specific Cowork and desktop bugs surfaced this week, signaling ongoing platform parity gaps.

---

## Releases
**v2.1.205** — [Release link](https://github.com/anthropics/claude-code/releases/tag/v2.1.205)
- Added auto-mode rule blocking tampering with session transcript files
- Fixed `--json-schema` silently producing unstructured output when the schema was invalid; schemas using the `format` keyword are no longer rejected
- Fixed a message sent while Claude was working being silently dropped

---

## Hot Issues (10 selected)

1. **[#69238 — No response from API error when Advisor is triggered](https://github.com/anthropics/claude-code/issues/69238)**  
   **44 comments · 70 👍**  
   Sonnet users hit "No response from API" errors whenever the Advisor (Opus 4.8) is invoked. High engagement suggests this blocks a core workflow. *Platform: macOS, area: TUI/API*

2. **[#42249 — Extreme token consumption — quota depleted in minutes](https://github.com/anthropics/claude-code/issues/42249)**  
   **38 comments · 17 👍**  
   Routine reads/edits burn through daily limits in ~1 hour. No resolution after three months; the issue remains the #1 cost complaint.

3. **[#55053 — Sudden 5-hour session window squeeze starting Apr 29](https://github.com/anthropics/claude-code/issues/55053)**  
   **37 comments · 12 👍**  
   A ~5–10× faster session-window depletion after an unannounced server-side change. Users report Sonnet sub-agents consuming disproportionate budget.

4. **[#74649 — Missing HCS services: vfpext — Cowork not working on Windows 11 Pro](https://github.com/anthropics/claude-code/issues/74649)**  
   **23 comments · 0 👍**  
   Cowork feature fails on Windows due to missing Hyper-V services. Freshly filed but gathering traction.

5. **[#69706 — API Error: 401 Invalid authentication credentials](https://github.com/anthropics/claude-code/issues/69706)**  
   **22 comments · 10 👍**  
   Persistent Windows auth failures. Users report valid API keys being rejected mid-session.

6. **[#65620 — Pre-tool-call assistant text never emitted (regression ~June 4)](https://github.com/anthropics/claude-code/issues/65620)**  
   **18 comments · 7 👍**  
   Thinking blocks silently swallow prose blocks in session transcripts. Has reproducer, designated regression. Blocks debugging workflows.

7. **[#67506 — Token consumption with Fable 5 not matching its description](https://github.com/anthropics/claude-code/issues/67506)**  
   **16 comments · 1 👍**  
   Fable 5 users report actual spend exceeding advertised rates. Undermines trust in pricing transparency.

8. **[#67636 — Parallel agent spawning causes excessive token consumption before crashing](https://github.com/anthropics/claude-code/issues/67636)**  
   **5 comments · 0 👍**  
   Claude spawns 10–15 agents for simple tasks, burning millions of tokens before hitting limits. Community calls for agent orchestration safeguards.

9. **[#75314 — 10 background Agent tasks stuck running for 34+ hours, no way to cancel](https://github.com/anthropics/claude-code/issues/75314)**  
   **3 comments · 0 👍**  
   Background agents hang indefinitely with no kill switch. ~1M tokens wasted. Highlights missing session lifecycle controls.

10. **[#75924 — Session history visible in UI but inaccessible after context compression](https://github.com/anthropics/claude-code/issues/75924)**  
    **1 comment · 0 👍**  
    Context compression silently drops history from the model while showing it in the UI. No user warning or opt-out. UX anti-pattern.

---

## Key PR Progress (6 open; top 6 selected)

1. **[#41447 — feat: open source claude code ✨](https://github.com/anthropics/claude-code/pull/41447)**  
   A long-standing community PR to open-source the codebase. Closed issues referenced (#59, #456, etc.). Still open after 3 months; sentiment is mixed (0 👍 likely from bots).

2. **[#72014 — Add protect-mcp plugin: fail-closed Cedar policy gate + signed receipts](https://github.com/anthropics/claude-code/pull/72014)**  
   A plugin that **blocks** policy-violating tool calls before execution and issues offline-verifiable signed receipts. Significant for enterprise compliance.

3. **[#75541 — fix(sweep): paginate issue events and honor unlabeled when closing expired issues](https://github.com/anthropics/claude-code/pull/75541)**  
   Fixes auto-close logic in the issue sweep script. Previously could mislabel issues when event pages overflowed 100.

4. **[#75537 — fix(hook-development): recognize all five hook handler types](https://github.com/anthropics/claude-code/pull/75537)**  
   The plugin-dev skill only knew 2 of 5 hook types. This PR fixes the validator and documentation. Important for plugin ecosystem health.

5. **[#75529 — docs(code-review plugin): clarify relationship to bundled /code-review skill](https://github.com/anthropics/claude-code/pull/75529)**  
   Resolves naming collision between the `code-review` plugin and the built-in `/code-review` slash command. Purely docs but prevents user confusion.

6. **[#68673 — fix(scripts): break pagination when page is not full, not only when empty](https://github.com/anthropics/claude-code/pull/68673)**  
   Pagination edge-case fix in scripts. Low-impact but correctness-critical for automation.

---

## Feature Request Trends

- **Plugin system expansion**: Multiple requests (e.g., #66032) ask for `.claude/workflows/*.js` to be distributable as plugin components, enabling reusable, shareable workflow scripts.
- **Desktop status indicators**: #60097 (9 👍) requests a `statusLine` equivalent in the desktop app to show current worktree/cwd, mirroring CLI functionality.
- **Agent cost controls**: A cross-cutting demand for agent-spawning limits, per-agent token budgets, and explicit user confirmation before parallel agent launches.
- **Context compression transparency**: Users want opt-out, warnings, and a summary of what was compressed before it happens.
- **Background session lifecycle management**: Stuck/cancellable agent processes and better visibility into running background tasks.

---

## Developer Pain Points

- **Runaway token consumption** dominates the issue tracker (3 of top 10 issues). Users report multi-million-token burn from misconfigured agent spawning, silent context retention, and opaque pricing for new models (Fable 5).
- **Windows platform gaps**: Cowork (HCS/vfpext), auth failures (401 errors), and input method (IME/CJK) issues show Windows remains a second-class citizen.
- **Session history invisibility**: Text blocks dropped silently during thinking (#65620) and history inaccessible after compression (#75924) erode trust in session fidelity.
- **No kill switch for background agents**: Users have no UI or API to terminate runaway background tasks (#75314).
- **JSON/UTF-8 serialization bugs**: Multiple issues (#64777, #69781) report "surrogates not allowed" errors mid-conversation, suggesting improper encoding handling in the API client.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-09

## Today's Highlights

A significant `rust-v0.143.0` release shipped with remote plugins enabled by default and system proxy support for macOS and Windows, signaling a major push toward enterprise networking compliance. However, the community is sounding alarms over a severe GPT-5.5 tool-calling regression affecting CLI users across Linux, macOS, and Windows, with multiple reports of `unsupported call: exec_command` errors. Additionally, a systemic rate-limit/usage-accounting bug is draining paid accounts' credits abnormally fast, triggering billing concerns among Pro subscribers.

## Releases

**rust-v0.143.0** — Major release with two headline features:
- Remote plugins now enabled by default, featuring richer catalog rows, npm marketplace sources, and visible remote/local version indicators (#30297, #26705, #29375, #30981)
- Codex can now route authentication and Responses API traffic through macOS and Windows system proxies, including PAC file support

Two alpha releases for the next minor version also landed:
- `rust-v0.144.0-alpha.1` and `rust-v0.144.0-alpha.2` — No changelog details provided

## Hot Issues

1. **[#29072 — Windows Codex App: apply_patch fails](https://github.com/openai/codex/issues/29072)**  
   *40 comments, 23 👍* — Persistent Windows bug where `apply_patch` fails because `codex-windows-sandbox-setup.exe` cannot launch from its installed package path. This has been open since June 19 and remains unresolved, blocking basic file-patching workflows for Windows users.

2. **[#2153 — ChatGPT integration](https://github.com/openai/codex/issues/2153)**  
   *38 comments, 150 👍* — Long-running request (since August 2025) for seamless session transfer between Codex and ChatGPT. The community strongly desires the ability to move work-in-progress code sessions to ChatGPT for research/UI-based brainstorming and bring results back to Codex CLI.

3. **[#31520 — Update command fails: "Could not find Codex package or platform npm release assets"](https://github.com/openai/codex/issues/31520)**  
   *11 comments, 24 👍* — A fresh regression where `curl | sh` update fails across platforms. The rapid upvote count suggests many users are encountering this immediately after the v0.143.0 release.

4. **[#31611 — CLI 0.143.0 on Amazon Linux 2023: `unsupported call: exec_command`](https://github.com/openai/codex/issues/31611)**  
   *6 comments, 4 👍* — Basic shell commands fail entirely on Amazon Linux. Downgrading to v0.140.0 fixes it, confirming this is a regression introduced in 0.143.0.

5. **[#31609 — gpt-5.5 tool calling regression](https://github.com/openai/codex/issues/31609)**  
   *5 comments, 2 👍* — Reports that GPT-5.5 tool calling is broken in CLI v0.143.0. Users describe it as "completely broken," with tool calls failing immediately.

6. **[#31665 — GPT-5.5 sends self-referential `namespace` on built-in tool calls](https://github.com/openai/codex/issues/31665)**  
   *4 comments, 1 👍* — Narrows the regression: the model sends `exec_commandexec_command` as a concatenated namespace, causing `unsupported call` errors. Known-working models (e.g., older GPT versions) do not exhibit this behavior.

7. **[#31668 — Multiple paid accounts: limits drain after one prompt, company credits burned in a day](https://github.com/openai/codex/issues/31668)**  
   *3 comments* — A systemic, billing-impacting rate-limit regression. Users report that paid accounts drain their entire monthly quota in a single session, with multiple related reports linked.

8. **[#19758 — Topic-based memory directory with agent-initiated writes](https://github.com/openai/codex/issues/19758)**  
   *8 comments* — A feature request for `memdir`-style topic-based memory, inspired by Claude Code's layout. Proposes a `/memory` slash command and agent-initiated memory writes. The community is actively discussing memory architecture improvements.

9. **[#20851 — First-class Computer Use support from CLI](https://github.com/openai/codex/issues/20851)**  
   *8 comments, 12 👍* — Computer Use (desktop automation) is currently app-only. Users want CLI parity, noting the feature is already partially implemented as a bundled MCP helper.

10. **[#31676 — Windows Desktop UI freezes after typing a prompt](https://github.com/openai/codex/issues/31676)**  
    *2 comments* — New report of application hangs on Windows after prompt submission. Combined with #31444 (IME/Explorer hangs), Windows desktop stability is a growing concern.

## Key PR Progress

1. **[#31361 — model-provider: route model discovery through HTTP client factory](https://github.com/openai/codex/pull/31361)**  
   Code-reviewed. Ensures model catalog refreshes respect system proxy settings, aligning with the v0.143.0 proxy feature.

2. **[#31637 — login: route raw auth flows through HTTP client](https://github.com/openai/codex/pull/31637)**  
   Code-reviewed. Completes proxy coverage for authentication flows, moving login off raw `reqwest::Client` usage.

3. **[#31363 — codex-api: route file uploads through HTTP client factory](https://github.com/openai/codex/pull/31363)**  
   Code-reviewed. Ensures the three-step file upload flow respects system proxy settings, closing a gap for enterprise users.

4. **[#31362 — core: route realtime and memories through HTTP client factory](https://github.com/openai/codex/pull/31362)**  
   Code-reviewed. Fixes proxy bypass for Realtime API and memory summarization requests.

5. **[#31431 — build: ratchet direct reqwest dependencies](https://github.com/openai/codex/pull/31431)**  
   Code-reviewed. Adds build-enforced guardrails to prevent new crates from bypassing the shared HTTP client abstraction.

6. **[#31683 — trace remote shell starts across core and exec server](https://github.com/openai/codex/pull/31683)**  
   Fresh PR adding OTEL tracing boundaries for remote shell commands, aiming to improve debugging of the exec-server pipeline.

7. **[#29869 — Preserve source chronology for imported sessions](https://github.com/openai/codex/pull/29869)**  
   Preserves original creation/last-activity timestamps when importing sessions, ensuring state-database rebuilds retain accurate chronology.

8. **[#31672 — Import enabled plugins from known marketplaces](https://github.com/openai/codex/pull/31672)**  
   Implements plugin discovery from user-level marketplace registries with fallback resolution for file, URL, npm, and inline sources.

9. **[#31681 — core: move reasoning effort to step context](https://github.com/openai/codex/pull/31681)**  
   Refactors `reasoning_effort` from turn-scoped to step-scoped state, aligning with the individual model sampling request model.

10. **[#31326 — feat: add managed Amazon Bedrock login](https://github.com/openai/codex/pull/31326)**  
    Server-side implementation for Codex-managed Bedrock API keys, enabling users to onboard without manual `auth.json` manipulation.

## Feature Request Trends

The most active feature request themes this week are:

- **Memory persistence improvements** (#19758): Users want topic-based, directory-structured memory with agent-initiated writes and slash-command access, moving beyond monolithic `memory_summary.md` files.
- **CLI parity with desktop** (#20851, #23324, #31640): Computer Use, sub-agent auto-approval, and mutation support in Plan Mode are all desktop-only features that CLI users are actively requesting.
- **ChatGPT bidirectional integration** (#2153): Sustained demand (150 👍) for session migration between Codex and ChatGPT for research/UI workflows.
- **Plugin ecosystem expansion** (#31672, #31677): The new remote plugin system is generating requests for larger archive limits, better marketplace discovery, and richer installation options.
- **Slash command extensibility** (#31666): Users want `/aliases` for reusable prompt shortcuts, inspired by the Interbase CLI.

## Developer Pain Points

**GPT-5.5 tool calling regression (Critical)** — Multiple reports (#31609, #31665, #31639, #31635) confirm that GPT-5.5 in CLI v0.143.0 is essentially unusable. The model sends corrupted `namespace` values on built-in tools (e.g., `exec_commandexec_command`), causing all shell commands to fail. This affects Linux, macOS, and Windows users equally.

**Windows-specific stability crisis** — At least 5 distinct Windows issues (#29072, #31511, #31676, #31444, #31564) report hangs, freezes, explorer/IME interference, and sandbox setup failures. The Windows desktop experience appears severely degraded.

**Rate-limit billing regression** — Issue #31668 and related reports (#31682, #31647) describe a systemic problem where paid accounts exhaust monthly quotas in a single session. Multiple accounts are affected, suggesting a server-side usage-accounting regression rather than client-side issues.

**Update infrastructure failure** — PR #31520 documents that the `curl | sh` update for v0.143.0 fails for many users with "Could not find Codex package or platform npm release assets," leaving users stuck on older versions or unable to install.

**Sub-agent/sandbox UX friction** — Multiple reports (#23664, #23324, #23515) describe inconsistent approval prompt display, lack of auto-approval inheritance from parent agents, and worktree session conflicts when running multiple concurrent Codex sessions.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-09

## Today's Highlights
Two releases shipped today: a stable **v0.50.0** with CI and security fixes, and a **v0.51.0-preview.0** cutting-edge build. Critical security work landed on the A2A server, fixing a zero-click RCE vulnerability, while the community continues to flag agent reliability issues—including subagent recovery masking failures and generalist agent hangs. The Auto Memory system also drew attention for indefinite retries and insufficient pre-model redaction.

## Releases

- **v0.50.0** (stable) — [View Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.50.0)  
  Focused on CI release verification (npm ci script fixes, workspace binary shadowing prevention) and the new Tool Registry feature (`Feat/tool registry`).  
- **v0.51.0-preview.0** (preview) — [View Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.51.0-preview.0)  
  Includes proxy test fixes and nightly version bump. Intended for early adopters.

## Hot Issues (10 selected)

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)** — Subagent recovery after MAX_TURNS reports "GOAL" success, masking interruption.  
   *Why it matters:* Critical bug—users get false confidence that analysis completed. Community engagement is high (10 comments, 2 👍). P1 priority, pending retesting.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)** — Generalist agent hangs indefinitely when deferred to.  
   *Why it matters:* Blocks all agent-based workflows. Workaround exists (disable agent delegation), but this is a top-voted issue (8 👍) with 7 comments. P1.

3. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353)** — Epic: Robust component-level evaluations.  
   *Why it matters:* 76 behavioral eval tests running across 6 model versions—foundational for quality assurance. P1, with 7 comments.

4. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)** — Epic: Assess AST-aware file reads, search, and codebase mapping.  
   *Why it matters:* Could dramatically reduce token consumption and improve navigation accuracy. 7 comments, 1 👍.

5. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522)** — Auto Memory retries low-signal sessions indefinitely.  
   *Why it matters:* Resource waste and potential infinite loops in background extraction. 5 comments.

6. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)** — Shell command execution stuck on "Waiting input" after command completes.  
   *Why it matters:* High-frequency frustration (3 👍), P1. Blocks all shell-driven tasks. 4 comments.

7. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672)** — Agent should stop/discourage destructive behavior (e.g., `git reset --force`).  
   *Why it matters:* Safety concern for production workspaces. Customer-issue tagged, 3 comments.

8. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983)** — Browser subagent fails on Wayland.  
   *Why it matters:* Linux desktop users blocked. P1, 4 comments.

9. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246)** — 400 error with >128 tools enabled.  
   *Why it matters:* Scalability ceiling for power users with many skills/tools. 3 comments.

10. **[#22465](https://github.com/google-gemini/gemini-cli/issues/22465)** — Gemini CLI gets stuck at interactive prompt creating a Vite app.  
    *Why it matters:* Common onboarding task broken. P2, 2 comments.

## Key PR Progress (10 selected)

1. **[#28319](https://github.com/google-gemini/gemini-cli/pull/28319)** — **Critical security: fix A2A server RCE via environment poisoning.** Refactors startup to enforce workspace trust. Size/m, open.

2. **[#28164](https://github.com/google-gemini/gemini-cli/pull/28164)** — Limit recursive reasoning to 15 turns per request, preventing infinite loops and excessive API usage. Size/m, open.

3. **[#28316](https://github.com/google-gemini/gemini-cli/pull/28316)** — Fix A2A task cancellation aborting execution loop (ghost executions). Also addresses race conditions and memory leaks. Size/l, open.

4. **[#28223](https://github.com/google-gemini/gemini-cli/pull/28223)** — Bypass LLM correction for JSON/IPYNB files in `write_file` and `replace` tools—prevents corruption of notebooks and configs. Size/m, open.

5. **[#28310](https://github.com/google-gemini/gemini-cli/pull/28310)** — Remove trailing period from Antigravity URL in sign-in error messages. Small fix improving DX. Size/s, open.

6. **[#28309](https://github.com/google-gemini/gemini-cli/pull/28309)** — Improve Markdown rendering for CJK text wrapping and `__bold__` syntax—addresses internationalization issues. Size/m, open.

7. **[#28103](https://github.com/google-gemini/gemini-cli/pull/28103)** — Avoid keep-alive socket reuse during OAuth token exchange, fixing "Premature close" errors on Node.js 24.17.0+. Size/m, closed.

8. **[#28224](https://github.com/google-gemini/gemini-cli/pull/28224)** — Fix emoji truncation in display strings by avoiding surrogate pair splitting. Size/s, open.

9. **[#28219](https://github.com/google-gemini/gemini-cli/pull/28219)** — Parse commented `settings.json` in memory bootstrap—prevents silent fallback to defaults. Size/s, open.

10. **[#28306](https://github.com/google-gemini/gemini-cli/pull/28306)** — Implement Caretaker Triage Worker main loop and Pub/Sub egress publisher. New infrastructure for automated issue triage. Size/m, open.

## Feature Request Trends

- **AST-aware tooling** (#22745, #22746): Community strongly desires syntax-aware navigation and editing to reduce token waste and improve precision.
- **Agent self-awareness** (#21432, #22598): Users want the agent to understand its own capabilities, flags, and share subagent trajectories for debugging.
- **Evaluation infrastructure** (#24353): Growing demand for robust, automated component-level evaluations—76 tests across 6 models already exist.
- **Non-destructive behavior** (#22672): Users consistently request safety rails for git and database operations.

## Developer Pain Points

- **Agent reliability and hangs** (#21409, #25166, #22465): High-frequency complaints about agents freezing on interactive prompts or hanging indefinitely—especially the generalist agent.
- **Subagent behavior opacity** (#22323, #21763): Recovery logic hides failures behind "GOAL" status, and bug reports lack subagent context. Makes debugging extremely difficult.
- **Configuration and permission surprises** (#22093, #22267): Agents running with disabled permissions, or ignoring settings.json overrides—erodes trust.
- **Scalability limits** (#24246): Hard cap at 128 tools triggers 400 errors—power users hit this frequently.
- **Auto Memory issues** (#26522, #26525): Indefinite retries, insufficient pre-model redaction of secrets, and silent patch rejection create both reliability and security concerns.
- **Terminal rendering regressions** (#21924, #24935, #28309): High-performance resizing, CJK text, emoji splitting, and editor exit corruption—many small papercuts affecting daily use.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-07-09

## Today's Highlights
No new releases were published in the last 24 hours, and the repository shows a quiet day in terms of new activity. The most notable event is the closure of Issue #4039 regarding enterprise-managed plugins not syncing to disk, which was resolved today. The community continues to experience friction around macOS Gatekeeper issues, stale keychain entries causing repeated OAuth popups, and a newly reported problem with `/resume` breaking for all non-git sessions.

## Releases
No new releases were published in the last 24 hours.

## Hot Issues

1. **[#970 — Copilot app blocked by macOS Gatekeeper under corporate security policy](https://github.com/github/copilot-cli/issues/970)** (OPEN, 6 comments, 21 👍)  
   *Why it matters:* Every Homebrew upgrade triggers a macOS security warning requiring manual approval. For enterprise users under strict security policies, this is a showstopper that wastes time and creates support tickets. The community is clearly frustrated, and a fix would benefit a large segment of Mac-based developers.

2. **[#2792 — Automatic switching between model for planning and execution](https://github.com/github/copilot-cli/issues/2792)** (OPEN, 4 comments, 14 👍)  
   *Why it matters:* Users want to assign cheaper/faster models for planning and more capable models for execution. This would reduce token costs and latency while maintaining output quality for complex tasks—a highly requested power-user feature.

3. **[#4053 — TUI hangs at 'Loading: N skills' on NFS/GPFS: SIGCHLD race](https://github.com/github/copilot-cli/issues/4053)** (OPEN, 1 comment)  
   *Why it matters:* A serious concurrency bug affecting Linux users with network file systems. The TUI becomes completely unresponsive due to a race condition when spawning subprocesses. This blocks adoption in many enterprise environments relying on NFS/GPFS.

4. **[#4016 — BYOK (COPILOT_PROVIDER_*) still rejected in --acp mode](https://github.com/github/copilot-cli/issues/4016)** (OPEN, 1 comment, 2 👍)  
   *Why it matters:* A regression (1.0.61–1.0.68) that breaks bring-your-own-key configurations for non-interactive/ACP mode. Enterprise customers relying on custom providers are blocked, and this is the third time this class of bug has resurfaced.

5. **[#2112 — Stale keytar entries cause repeated browser OAuth popups for HTTP MCP servers](https://github.com/github/copilot-cli/issues/2112)** (OPEN, 1 comment, 1 👍)  
   *Why it matters:* Every launch triggers unwanted OAuth popups because expired tokens in the OS keychain override valid file-cache tokens. A frustrating UX that breaks automated and headless workflows.

6. **[#618 — Feature Request: Support custom slash commands from .github/prompts directory](https://github.com/github/copilot-cli/issues/618)** (CLOSED, 32 comments, 99 👍)  
   *Why it matters:* The most upvoted issue in the list (99 👍). Users want parity with the VS Code extension’s ability to load custom prompts from `.github/prompts/`. This would enable team-shared command libraries and more customizable workflows.

7. **[#3158 — Plan→Compact→Re-Plan infinite loop (217 cycles, zero execution)](https://github.com/github/copilot-cli/issues/3158)** (CLOSED, 4 comments)  
   *Why it matters:* A severe bug where auto-compaction puts the agent into a permanent planning loop, burning through entire sessions without writing any code. Multiple duplicate reports (10+ issues filed by the same user) suggest this is a systemic design flaw in context management.

8. **[#4054 — /resume broken for all non-git sessions](https://github.com/github/copilot-cli/issues/4054)** (OPEN, 1 comment)  
   *Why it matters:* Newly reported. The `/resume` command is completely unusable for sessions started outside a git repository due to a catch-22 in the picker's git gate. This breaks session continuity for a significant use case.

9. **[#1624 — Previous installed CLI versions not cleaned up](https://github.com/github/copilot-cli/issues/1624)** (OPEN, 1 comment, 1 👍)  
   *Why it matters:* Old versions accumulate, consuming up to 2GB of disk space per user. A straightforward housekeeping issue that creates unnecessary storage pressure, especially on corporate-managed machines.

10. **[#4065 — Copilot exfiltration protection is too aggressive and blocks legitimate spec content](https://github.com/github/copilot-cli/issues/4065)** (OPEN, 0 comments)  
    *Why it matters:* A false-positive exfiltration alert triggered by a legitimate configuration file containing the string `${env.AUTH_TOKEN}`. Overtuned security heuristics that block valid workflows need immediate tuning.

## Key PR Progress
No meaningful pull requests were active in the last 24 hours. Both open PRs (#4057 and #3708) appear to be non-functional (empty or trivial file uploads) and do not represent active development progress.

## Feature Request Trends
The most prominent feature requests center on **agent customization and control**:
- **Custom slash commands** (Issue #618, 99 👍): Reading prompts from `.github/prompts/` for team-shared workflows.
- **Automatic model switching** (Issue #2792, 14 👍): Using different models for planning vs. execution to optimize cost and quality.
- **Configurable exit resume hint** (Issue #4066): Preference to show renamed session names instead of opaque IDs.

A secondary theme is **enterprise and policy management**:
- Enterprise plugin sync (Issue #4039, fixed) and managed-settings compliance.
- Better support for headless/non-interactive modes with custom providers.

## Developer Pain Points
The following recurring frustrations emerge from the issue tracker:

- **Session management fragility:** The "plan-compact-re-plan" infinite loop (10+ duplicates from one user) and the newly broken `/resume` for non-git sessions point to deep issues in session state and context compaction.
- **Enterprise deployment friction:** macOS Gatekeeper warnings, stale keychain entries causing OAuth popups, and NFS/GPFS hangs all create friction for corporate rollouts.
- **Authentication churn:** Repeated OAuth popups (Issue #2112) and BYOK regressions (Issue #4016) erode trust in authentication reliability.
- **Disk bloat:** Lack of automatic cleanup for old CLI versions (Issue #1624) wastes space on developer machines.
- **Overtuned security heuristics:** Exfiltration protection flagging legitimate configuration files (Issue #4065) is a classic case of security UX that penalizes real work.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date:** 2026-07-09  
**Source:** [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## Today's Highlights
No new releases or merged pull requests landed in the last 24 hours, marking a quiet day on the development front. The community's attention remains fixed on a persistent SSL certificate interception issue (Issue #2458) caused by corporate antivirus software, which has been open since mid-June and continues to block users behind managed networks. With zero PR activity, the maintainer signal is currently low, but the single hot issue suggests that enterprise and corporate users are becoming a louder voice in the ecosystem.

---

## Releases
**None.** No new versions were published in the last 24 hours.

---

## Hot Issues
*Only 1 issue was updated in the last 24h. The full pick is listed below.*

1. **#2458 – Add option to ignore ssl certificate**  
   *Author:* dmorsin | *Updated:* 2026-07-08 | *Comments:* 2 | 👍: 0  
   *Why it matters:* A corporate user reports that their organization's antivirus performs man-in-the-middle (MiTM) SSL interception, injecting its own certificate and breaking `kimi login`. This is a blocker for any developer behind a corporate firewall or managed endpoint. With only 2 comments and 0 upvotes, the issue hasn't gained broad traction yet, but the use case is critical for enterprise adoption.  
   **Link:** [Issue #2458](https://github.com/MoonshotAI/kimi-cli/issues/2458)

---

## Key PR Progress
**None.** No pull requests were updated in the last 24 hours.

---

## Feature Request Trends
Based on the single active issue in this window, the most prominent feature request direction is:

- **SSL/TLS Bypass & Certificate Flexibility** – Users behind corporate proxies, antivirus, or self-signed certificate infrastructures are requesting official support for `--insecure` or `--ignore-ssl` flags. This trend signals an increasing need for the CLI to operate in locked-down enterprise environments where standard CA chains are disrupted.

*Note: With only one issue surfaced in the last 24h, broader trend analysis is limited. A full history of all open issues would be required for a comprehensive view.*

---

## Developer Pain Points
Recurring frustrations observed from the active issue (and implied from its context):

- **Corporate Network Incompatibility:** The inability to trust custom certificates or skip SSL verification makes Kimi CLI unusable for developers in large organizations using endpoint security tools. This is a high-friction point for enterprise rollout.
- **Delayed Response to SSL Warnings:** Despite the issue being open since June 17, there is no evidence of a fix or workaround being prioritized. Developers are left with no clear migration path.
- **Lack of Configurable HTTP Client Options:** There is no evident v flag, proxy config, or CA bundle override, forcing users to either modify system-wide certificate stores or abandon the tool.

*[Note: No other issues were updated in the last 24h, so pain points are inferred from the single active issue and common patterns in CLI tools.]*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest
**2026-07-09**

---

## Today's Highlights

The OpenCode community saw a surge of activity focused on **V2 stabilization**, **provider compatibility**, and **subagent reliability**. Key developments include the closure of the "Full MCP client capabilities" feature request after a long discussion, a significant fix for PowerShell UTF-8 encoding on Windows now open for review, and ongoing critical conversations around Gemma 4 tool calling failures and subagent hang issues. The team also merged several V2 fixes for session state persistence and review pane behavior.

---

## Releases

*No new releases in the last 24 hours.*

---

## Hot Issues

1. **[#20995 - Gemma 4 (e4b) tool calling fails via Ollama OpenAI-compatible API](https://github.com/anomalyco/opencode/issues/20995)**
   - **Why it matters**: 30 comments, 47 thumbs up. The top-voted open issue. Gemma 4's streaming `tool_calls` are not recognized by OpenCode, breaking a critical workflow for many users leveraging local models via Ollama. Community interest is high, but progress has been slow since April.

2. **[#16017 - [FEATURE]: Add Go plan usage/balance API endpoint](https://github.com/anomalyco/opencode/issues/16017)**
   - **Why it matters**: 23 comments, **96 thumbs up** — the most upvoted open issue. Users want programmatic access to their subscription usage data (rolling/weekly/monthly). The dashboard already shows this, but an API would enable billing automation and custom dashboards.

3. **[#28567 - [CLOSED] [FEATURE]: Full MCP client capabilities](https://github.com/anomalyco/opencode/issues/28567)**
   - **Why it matters**: Closed after 22 comments and 25 👍. The community successfully pushed for alignment with the latest MCP standard. This marks a significant milestone for OpenCode's extensibility story.

4. **[#6096 - [FEATURE]: Adding Experimental Calculation and Display of Tokens per second](https://github.com/anomalyco/opencode/issues/6096)**
   - **Why it matters**: 19 comments, 60 👍. One of the longest-running feature requests (Dec 2025). Users consistently want real-time TPS metrics to compare provider performance and debug latency issues.

5. **[#30086 - High CPU usage in newer versions of OpenCode](https://github.com/anomalyco/opencode/issues/30086)**
   - **Why it matters**: 17 comments, 11 👍. A regression where CPU usage spiked dramatically — users report going from 10 concurrent sessions to struggling with 3. Performance regression is a high-priority concern.

6. **[#35556 - [CLOSED] V2: first Location can expose an empty plugin generation](https://github.com/anomalyco/opencode/issues/35556)**
   - **Why it matters**: Closed with a clear root cause identified (PluginSupervisor races during initial reload). The fix (#35755) resolves a subtle V2 startup race condition.

7. **[#33028 - Subagents hang indefinitely after quick bash tool call](https://github.com/anomalyco/opencode/issues/33028)**
   - **Why it matters**: 5 comments but a critical reliability bug. Subagents hang on streaming calls after a bash tool, requiring manual kill. Reproduced across two different models — suggests a systemic issue with stream timeout handling.

8. **[#33490 - GLM-5.2 via OpenCode Go rejects `instructions` field](https://github.com/anomalyco/opencode/issues/33490)**
   - **Why it matters**: An incompatibility between OpenCode Go's provider chain and GLM-5.2. Extra `instructions` field is not permitted by the downstream API, blocking users on this model.

9. **[#35952 - Tasks (subagents) are not resumable on ANY failure or freeze](https://github.com/anomalyco/opencode/issues/35952)**
   - **Why it matters**: Fresh issue (yesterday) highlighting a pain point for batch job users. When agents stall mid-job (often due to high demand), there is no restart mechanism, leading to wasted quota costs.

10. **[#30310 - opencode-go qwen3.7-max intermittently returns 500 Internal server error](https://github.com/anomalyco/opencode/issues/30310)**
    - **Why it matters**: Intermittent HTTP 500 on text requests via OpenCode Go endpoint. Affects reliability of a popular model, with no root cause resolution yet.

---

## Key PR Progress

1. **[#35995 - fix(project): bound icon discovery scan](https://github.com/anomalyco/opencode/pull/35995) [OPEN]**
   - **What**: Limits `**/favicon.*` scanning to avoid freezes on large projects. Closes #29953. A direct fix for a performance regression.

2. **[#35994 - fix(core): avoid per-file directory list rebuild](https://github.com/anomalyco/opencode/pull/35994) [OPEN]**
   - **What**: Optimizes `ripgrepLayer` startup by avoiding repeated `Array.from(directories)` rebuilds, improving file indexing performance.

3. **[#31985 - fix(shell): add PowerShell UTF-8 command wrapper on Windows](https://github.com/anomalyco/opencode/pull/31985) [OPEN]**
   - **What**: **Key fix for Windows users**. Adds UTF-8 support for PowerShell command execution, closing 5 related issues (#23636, #31187, #30205, #31830, #26882). A significant quality-of-life improvement for the Windows ecosystem.

4. **[#35985 - fix(provider): derive reasoning variants from models.dev](https://github.com/anomalyco/opencode/pull/35985) [OPEN]**
   - **What**: Moves reasoning variant detection from hardcoded model ID tables to the `models.dev` API's `reasoning_options` field. More maintainable and future-proof provider support.

5. **[#35982 - fix(provider): improve prompt caching](https://github.com/anomalyco/opencode/pull/35982) [OPEN]**
   - **What**: Addresses prompt caching inconsistencies across AI SDK providers — some use camelCase, some snake_case, some cache silently. Makes caching portable and reliable.

6. **[#34794 - feat(provider): add --model free](https://github.com/anomalyco/opencode/pull/34794) [OPEN]**
   - **What**: New `--model free` flag that randomly selects a zero-cost OpenCode Zen model. Closes #21863. Makes free-tier model selection effortless.

7. **[#31798 - [CLOSED] fix(snapshot): reuse source git objects to avoid re-hashing huge repos](https://github.com/anomalyco/opencode/pull/31798)**
   - **What**: Merged fix for massive repos (e.g., Chromium with 500k files). Avoids `git add --all` re-hashing by reusing existing git objects, solving a hang-on-open issue.

8. **[#35078 - [CLOSED] fix(app): reserve review pane minimum instead of capping chat width](https://github.com/anomalyco/opencode/pull/35078)**
   - **What**: Fixes a UI regression where the review pane was forced to ~55% of window width on wide monitors. Now the chat has a minimum width, making the review pane properly resizable.

9. **[#35628 - [CLOSED] fix(app): unmount hidden session panes](https://github.com/anomalyco/opencode/pull/35628)**
   - **What**: Performance fix — unmounts closed side panels instead of retaining zero-size instances, reducing memory and render overhead.

10. **[#35488 - [CLOSED] feat(app): persist review state per session](https://github.com/anomalyco/opencode/pull/35488)**
    - **What**: Persists review panel state (file selection, mode) per server/workspace/session. Files that become unavailable fall back gracefully, improving UX for multi-session workflows.

---

## Feature Request Trends

- **Usage Analytics & Monitoring** (#6096, #16017): Strong demand for TPS display, token tracking, and API access to subscription usage data. Users want to audit costs and compare provider performance.
- **Model Router / Auto-Selection** (#35937): Users want OpenCode to automatically pick the best model for a task (e.g., a lightweight model for simple queries, a powerful model for code generation). Hot-switching without restart is a key ask.
- **Data Lifecycle Management** (#34875): Configurable session data retention and automated cleanup of the SQLite database. Users report unbounded growth of `opencode.db`.
- **MCP Elicitation / Human-in-the-Loop** (#23066, closed): The community continues to push for MCP tools that can request human input mid-workflow, enabling interactive tool pipelines.
- **Clipboard / TUI Polish** (#35977, #35978): Linux TUI users face recurring clipboard pain — `xclip`/`xsel`/`wl-clipboard` must be manually installed. Requests to bundle these or auto-install them.

---

## Developer Pain Points

- **Subagent Reliability** (#33028, #35952): Subagents hang indefinitely after tool calls and are not resumable on failure. For users running batch jobs, a single stalled agent means wasted quota and manual restarts.
- **CPU/Performance Regressions** (#30086, #35994, #35995): Recent versions introduced CPU spikes and UI lag. Users report being unable to run multiple sessions. The team is actively addressing this with icon scan bounding and directory list optimization.
- **Provider Compatibility Fragmentation** (#20995, #33490, #30310): Inconsistencies between providers (Ollama, OpenCode Go, Z.AI) cause hard-to-debug failures. Tool calling, field validation, and intermittent 500 errors are recurring themes.
- **Context Window Errors** (#35991): Deepseek V4 Flash Free users report that even fresh sessions start with 500K+ tokens in context, immediately exceeding the model's 262K limit — suggesting a bug in context management or conversation history retention.
- **Data Loss / Recovery** (#35939, #17953): AI-deleted files cannot be recovered from the UI even though the changes are visible. Destructive file operations lack guardrails and undo capabilities remain incomplete in V2.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-09

## Today's Highlights
A flurry of targeted bug fixes and UX improvements landed today, with significant attention on session lifecycle: fixing fork double-selection, stabilizing clipboard paste on X11, and supporting custom metadata in JSONL headers for the new harness module. The community also rallied around model-compatibility issues, with a critical ghost-model bug on Xiaomi’s MiMo Token Plan providers and DeepSeek V4 crashes making the hot list. A new prompt cache miss tracking feature in the coding agent signals growing operational maturity.

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 selected from 42 total)

**#6204 — [CLOSED] mimo-v2-omni is a ghost model on the three MiMo Token Plan providers**
A bundled model catalog lists `mimo-v2-omni` for all Xiaomi regional providers, but the endpoints return `400 Not supported model`. This instantly breaks user trust in the provider list. 7 comments, low community reaction (0 👍).  
👉 [View Issue](https://github.com/earendil-works/pi/issues/6204)

**#5700 — [CLOSED] Support multiple live agent sessions with TUI switching**
A long-running feature request (since June 13) asking for concurrent agent sessions where a user can background one agent while interacting with another. Currently `switchSession` tears down the old session. 9 comments, 0 👍.  
👉 [View Issue](https://github.com/earendil-works/pi/issues/5700)

**#5263 — [OPEN] Make in-session model and thinking-level changes ephemeral by default**
High community demand (6 👍) to make runtime model switches affect only the active session, not global defaults. Proposes a “Default model” entry in `/settings` as the sole global surface. 5 comments.  
👉 [View Issue](https://github.com/earendil-works/pi/issues/5263)

**#5886 — [OPEN] AgentSession settlement/continuation and assistant-tail lifecycle bugs**
A meta-issue summarizing a class of bugs where post-run logic tries to continue an agent from a transcript that is no longer coherent. Filed by mitsuhiko. 4 comments, 2 👍.  
👉 [View Issue](https://github.com/earendil-works/pi/issues/5886)

**#6434 — [CLOSED] Fix empty reasoning content TUI render for OpenAI models**
OpenAI Responses replay leaks empty thinking blocks into the TUI. Fix strips them while preserving the raw reasoning item. 3 comments, 1 👍.  
👉 [View Issue](https://github.com/earendil-works/pi/issues/6434)

**#6431 — [CLOSED] Retryable error: bun fetch socket drop not classified**
A transient network socket drop (`socket connection was closed`) terminates a running agent without any retry because the retry classifier does not recognize this Bun fetch error. Critical for reliability on Bun runtime. 1 comment.  
👉 [View Issue](https://github.com/earendil-works/pi/issues/6431)

**#6429 — [CLOSED] OpenAI Responses sends max_output_tokens=1 after compaction**
After session auto-compaction, Pi sends `max_output_tokens: 1` (below minimum of 16), causing repeated 400 errors. A severe regression for long-running `openai/gpt-5.5` sessions. 1 comment.  
👉 [View Issue](https://github.com/earendil-works/pi/issues/6429)

**#6433 — [CLOSED] DeepSeek V4 + thinking mode crashes session in v0.80.3**
DeepSeek V4 Pro/V4 Flash with thinking mode crashes silently (returns to terminal) due to `reasoning_content` not being preserved during tool-call history replay. Regression from 0.79.x. 1 comment.  
👉 [View Issue](https://github.com/earendil-works/pi/issues/6433)

**#6378 — [OPEN] Error: maximum context length exceeded**
A user reports being unable to work around the 262000 token context limit, requesting the context-compression plugin. 2 comments, 0 👍.  
👉 [View Issue](https://github.com/earendil-works/pi/issues/6378)

**#6303 — [OPEN] Exponential retry backoff has no cap**
`_prepareRetry()` runs unbounded exponential backoff (base 2000ms * 2^attempt). At attempt 7, delay is ~4 minutes. Config `retry.provider.maxRetryDelayMs` exists but is never read. 2 comments, 1 👍.  
👉 [View Issue](https://github.com/earendil-works/pi/issues/6303)

## Key PR Progress (10 selected from 6 total)

**#6436 — [CLOSED] fix(ai): hide responses reasoning comment markers**
Strips provider-inserted HTML comment markers from visible OpenAI Responses reasoning summaries while preserving raw signed reasoning items. Adds regression tests.  
👉 [View PR](https://github.com/earendil-works/pi/pull/6436)

**#6427 — [OPEN] feat(coding-agent): add prompt cache miss tracking**
Detects prompt cache misses per turn by comparing cache reads against previous request prompt tokens. Emits warning-colored transcript notices for idle gaps past TTL or model switches. `/session` view integration.  
👉 [View PR](https://github.com/earendil-works/pi/pull/6427)

**#6430 — [CLOSED] fix fork menu allowing user to double select an entry**
Closes the forking menu before the fork process starts, preventing double-selection when extensions slow down teardown and create multiple session forks.  
👉 [View PR](https://github.com/earendil-works/pi/pull/6430)

**#6418 — [CLOSED] Fix native clipboard in bun release**
Copies native `.node` files into the clipboard package for Bun release compatibility, and adds `xclip` fallback on X11 when native clipboard fails. Fixes #6250.  
👉 [View PR](https://github.com/earendil-works/pi/pull/6418)

**#6417 — [CLOSED] feat(agent): support custom metadata in jsonl session headers**
Adds optional opaque `metadata?: Record<string, unknown>` to the v3 JSONL session header, accepted by `JsonlSessionStorage.create()` and returned in metadata.  
👉 [View PR](https://github.com/earendil-works/pi/pull/6417)

**#6413 — [CLOSED] feat(coding-agent): show git info in local version**
Displays git commit/branch/tag when running Pi directly from the repo. Closes #6412.  
👉 [View PR](https://github.com/earendil-works/pi/pull/6413)

*Note: Only 6 PRs were updated in the last 24h; all are listed above.*

## Feature Request Trends
- **Multi-session concurrency:** Strong interest (Issue #5700, 9 comments) in running multiple agent sessions simultaneously with TUI switching, rather than tearing down the current session.
- **In-session ephemeral model changes:** High demand (Issue #5263, 6 👍) for runtime model/thinking-level changes to be session-scoped only, with a dedicated `/settings` entry for global defaults.
- **Extension hooks at startup:** Users want `session_before_load` or equivalent hooks fired before the session file is read at startup (Issue #6428).
- **Pre-compaction on model switch:** A new edge case request (Issue #6426) to auto-compact the session when switching to a smaller-context model, preventing overflow on the next request.
- **Built-in provider additions:** Novita AI (Issue #6420) and better support for image-model generation formatting (Issue #6419).

## Developer Pain Points
- **Model compatibility & provider bugs:** Ghost models (e.g., `mimo-v2-omni` on Xiaomi endpoints — #6204), broken DeepSeek V4 with thinking mode (#6433), and missing Anthropic OAuth billing markers (#6421) erode user confidence in bundled provider configurations.
- **Session lifecycle fragility:** Settlement/continuation bugs (#5886) and the fork double-selection issue (#6321) cause session corruption and lost work.
- **Retry & error handling gaps:** Unbounded exponential backoff (#6303), unclassified socket drops (#6431), and post-compaction `max_output_tokens` overflow (#6429) cause silent failures or prolonged wait times.
- **Clipboard & image paste breaks:** Native clipboard bindings fail in Bun release binaries on Linux/X11 (#6250), and pasted images are often ignored by models (#6373).
- **Read-only config paths break credential reads:** Pi creates lock files even for read operations, preventing use of read-only `~/.pi/agent` directories (#6406).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-09

## Today's Highlights

The team shipped **v0.19.8** with server isolation improvements and WeCom channel documentation. The community is actively debating a **multi-workspace daemon RFC** (#6378) and addressing a critical **Anthropic Claude 4.8+ compatibility break** where deprecated `temperature` parameters cause 400 errors. CI reliability remains a pain point, with two release workflow failures this week.

## Releases

### v0.19.8 ([Release Notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.8))
- **feat(cli):** Added `serve env isolation` and `total admission` controls for improved daemon security and resource management  
- **docs(channels):** Added WeCom to the channels overview documentation

## Hot Issues (Top 10)

1. **[#6378](https://github.com/QwenLM/qwen-code/issues/6378) RFC: Multiple workspaces in one daemon**  
   *Priority: P2 | Comments: 19*  
   The most-discussed open issue proposes extending the `1 daemon = 1 workspace × N sessions` model to support multiple isolated workspaces per daemon. The community is actively discussing migration paths and backward compatibility.

2. **[#6384](https://github.com/QwenLM/qwen-code/issues/6384) Hard limit: 0 when env-configured model reserves full context for output**  
   *Priority: P2 | Comments: 5*  
   A critical bug causes session startup failures when environment-configured models reserve their full default context window for output, resulting in an effective `hard limit: 0`. Affects users with custom model configurations.

3. **[#6334](https://github.com/QwenLM/qwen-code/issues/6334) Extension install fails on Windows**  
   *Comments: 5 | 👍: 1*  
   Users report `extensions install` failures from Git downloads on Windows (v0.19.6). A related fix PR (#6545) is now addressing the root cause — stale temp directories causing clone failures.

4. **[#6505](https://github.com/QwenLM/qwen-code/issues/6505) Subagent infinite tool-call loops**  
   *Priority: P2 | Comments: 4*  
   A critical multi-agent bug where subagents can repeat identical tool calls indefinitely because the main agent's `LoopDetectionService` doesn't cover subagent scope. Closed as fixed.

5. **[#6414](https://github.com/QwenLM/qwen-code/issues/6414) VS Code: Failed to connect to Qwen agent**  
   *Comments: 4*  
   VS Code extension users are experiencing connection failures to the Qwen agent. Marked as `need-information` — the core team is awaiting repro details.

6. **[#6487](https://github.com/QwenLM/qwen-code/issues/6487) Memory index stale after `/remember`; content lost on compaction**  
   *Priority: P2 | Comments: 2*  
   Two independent memory degradation mechanisms: the MEMORY.md index doesn't refresh the system instruction after `/remember`, and compaction silently drops memory content. Impacts long-running sessions.

7. **[#6554](https://github.com/QwenLM/qwen-code/issues/6554) Nightly release workflow failed**  
   *Comments: 1*  
   The `v0.19.8-nightly` release failed due to a failing `quality` job. A hotfix PR (#6555) applies Prettier formatting across 74 files to restore CI green.

8. **[#6519](https://github.com/QwenLM/qwen-code/issues/6519) Anthropic Claude 4.8+ `temperature` parameter deprecated**  
   *Priority: P1 | Comments: 1*  
   A high-priority compatibility bug: Qwen Code sends a deprecated `temperature` parameter to Claude Opus 4.8+ models, resulting in 400 errors. Root cause identified in the Anthropic content generator.

9. **[#6536](https://github.com/QwenLM/qwen-code/issues/6536) WebShell @ references serialize instead of showing chips**  
   *Priority: P2 | Comments: 1*  
   UX regression: built-in composer @ references render as compact chips before sending but appear as raw text (e.g., `@.qwen/`) in sent messages.

10. **[#3845](https://github.com/QwenLM/qwen-code/issues/3845) Installation fails: Cannot find module**  
    *Comments: 2 | 👍: 2*  
    A long-standing installation issue on Windows where the installer script fails with `Cannot find module` errors. High community upvote ratio suggests it affects multiple users.

## Key PR Progress (Top 10)

1. **[#6525](https://github.com/QwenLM/qwen-code/pull/6525) feat(serve): Cursor-paged transcript replay endpoint**  
   Adds `GET /session/:id/transcript` with cursor-paged JSONL transcript snapshots, active parent chain reconstruction, and lightweight metadata. Enables efficient session replay for daemon clients.

2. **[#6259](https://github.com/QwenLM/qwen-code/pull/6259) feat(daemon): Persist session artifacts across restarts**  
   Implements V2 daemon artifact metadata persistence — restores restorable artifacts across daemon restart/session replay with durable tombstones and snapshot recording in JSONL.

3. **[#6526](https://github.com/QwenLM/qwen-code/pull/6526) Fix: Long session timeline scrolling**  
   Fixes Web Shell session timeline for conversations with many turns: centered viewport, hidden native scrollbars, auto-visibility for current marker.

4. **[#6555](https://github.com/QwenLM/qwen-code/pull/6555) fix: Prettier formatting to restore CI quality job**  
   Emergency hotfix applying `npm run format` across 74 files to fix the nightly release workflow. Whitespace-only changes — no logic or behavior altered.

5. **[#6495](https://github.com/QwenLM/qwen-code/pull/6495) feat(channels): Webhook-triggered channel tasks**  
   Enables external webhooks to POST events to `qwen serve`, with channel workers proactively delivering AI-generated responses to configured chat targets.

6. **[#6535](https://github.com/QwenLM/qwen-code/pull/6535) feat(scheduled-tasks): Isolated run mode via `create_sub_session`**  
   Introduces a daemon-only `create_sub_session` tool with clean context/transcript, wiring it into the cron scheduler for isolated execution — preventing accumulated context pollution.

7. **[#6545](https://github.com/QwenLM/qwen-code/pull/6545) fix(extension): Clean temp dir before fallback git clone on Windows**  
   Fixes the Windows extension install failure (#6334) by cleaning the temp directory before retrying with `git clone` after a failed GitHub release download.

8. **[#6547](https://github.com/QwenLM/qwen-code/pull/6547) ci(autofix): Single-target scheduler**  
   Updates the Qwen Autofix CI to a 10-minute single-target scheduler: prioritizes existing bot PRs over the approved issue backlog, reducing duplicate work.

9. **[#6457](https://github.com/QwenLM/qwen-code/pull/6457) feat(qqbot): Group message handling and cron-msg-experimental**  
   Final piece of QQ Bot channel support: adds group message handling with keyword triggers, @-mention detection, and experimental cron messaging.

10. **[#6551](https://github.com/QwenLM/qwen-code/pull/6551) perf(core): Pure-ASCII fast path for token estimation**  
    Speeds up character-based token estimation by 1.61× (51.9ms → 32.2ms median) using a single regex scan for the common code/ASCII prose case.

## Feature Request Trends

- **Multi-tenant daemon architecture**: The community is pushing for multiple workspaces per daemon process (#6378), isolated sub-sessions (#6535), and better session artifact persistence (#6259)
- **Channel platform expansion**: Active development on QQ Bot support (#6457) and webhook-triggered tasks (#6495), plus diagnostics and policy controls for existing channels (WeCom, DingTalk, Feishu)
- **Observability & hooks**: Demand for mid-turn streaming hooks (`MessageDisplay` — #6489), background task status in hook payloads (#6529), and read-only Advisor feedback loops for complex tasks (#6542)
- **Memory system improvements**: Requests for configurable AutoMemory timeouts (#6308), worktree memory isolation (#6449), and solutions for memory index staleness (#6487)
- **Configuration flexibility**: Users want configurable vision bridge timeouts (#6524), DM policy controls (#6392), and NO_PROXY support in the ProxyAgent (#6401)

## Developer Pain Points

1. **Release workflow fragility**: Two release failures this week (nightly and stable) due to CI quality checks and formatting drift — the community is experiencing friction with release reliability

2. **Windows-specific bugs**: Persistent installation failures (#3845) and extension install problems (#6334) continue to plague Windows users despite multiple fix attempts

3. **Session/memory degradation**: Multiple issues report silent truncation of session history (#6501), memory loss on compaction (#6487), and stale memory indexes — degrading the quality of long-running sessions

4. **Model compatibility breaks**: The Anthropic Claude 4.8+ `temperature` deprecation (#6519) highlights the challenge of keeping pace with rapidly evolving model APIs

5. **Agent safety and loop detection**: The subagent infinite tool-call loop bug (#6505) and self-kill process recognition (#6246) reveal gaps in agent safety mechanisms, particularly in multi-agent and shell-execution contexts

6. **UI/UX regressions**: WebShell @-reference serialization (#6536), processing duration display flicker (#6402), and status line model misattribution (#6512) indicate ongoing polish needs in the interactive interface

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-09

**Project:** [Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale) (previously DeepSeek TUI)

---

## 1. Today's Highlights

The v0.8.68 milestone accelerates toward completion with a burst of 10+ closed PRs across fleet routing, model catalog, and performance lanes. A major architecture shift is underway: `AgentProfile` becomes the canonical contract for Fleet rosters, replacing the parallel loadout system. Community contributor **JayBeest** lands the sub-agent tool sandboxing plan, while **yekern** flags an unbounded `subagents.v1.json` growth issue affecting long-running sessions.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Hot Issues (10 selected)

1. **[#4092 — v0.8.68 execution board: lane order, dependencies, and agent protocol](https://github.com/Hmbown/CodeWhale/issues/4092)** *(49 comments)*  
   The canonical v0.8.68 coordination issue. Every open milestone issue carries a single `lane-*` label. This is the single entry point for understanding the release's scope and lane structure. High signal for contributors wanting to pick work.

2. **[#4042 — Environment-level tool sandboxing for sub-agents](https://github.com/Hmbown/CodeWhale/issues/4042)** *(12 comments, CLOSED)*  
   JayBeest's thorough analysis of `--disallowed-tools`, per-tool `enabled/disabled` flags, and runtime enforcement gaps. Led directly to PR #4096. Community praised the evidence-driven approach.

3. **[#3965 — Per-sub-agent provider assignment + LM Studio support](https://github.com/Hmbown/CodeWhale/issues/3965)** *(7 comments, CLOSED)*  
   User request that evolved into the Fleet profile routing redesign. LM Studio users have been waiting for this—now addressed by PR #4262.

4. **[#4227 — Help JayBeest keep up with the CodeWhale tsunami 🌊](https://github.com/Hmbown/CodeWhale/issues/4227)** *(2 comments, OPEN)*  
   A meta-issue from JayBeest requesting a skill/workflow to automate pulling, rebuilding, and testing against latest `main`. Reflects community sentiment that project velocity is overwhelming for contributors.

5. **[#4217 — subagents.v1.json grows unbounded](https://github.com/Hmbown/CodeWhale/issues/4217)** *(1 comment, OPEN)*  
   yekern reports `~300,000 lines` in state file after days-long sessions. Root cause identified at `subagent/mod.rs:1992`. Critical for anyone running CodeWhale as a long-lived terminal tool.

6. **[#4236 — Epic: official Termux / Android arm64 support](https://github.com/Hmbown/CodeWhale/issues/4236)** *(0 comments, OPEN)*  
   Epic tracking Android-native TUI support. Multiple child issues (#4237, #4238, #4241, #4242) already filed. Community signal from #1135 shows strong demand.

7. **[#3757 — Launch is slow; profile and remove startup inefficiency](https://github.com/Hmbown/CodeWhale/issues/3757)** *(3 comments, CLOSED)*  
   Startup latency finally addressed via PR #3761 (deferred maintenance cleanup). A win for day-to-day UX.

8. **[#3990 — Slash autocomplete repeats aliases already shown](https://github.com/Hmbown/CodeWhale/issues/3990)** *(1 comment, CLOSED)*  
   Dogfood bug: `/clear or /qingping` appears twice. Fixed in PR #4254. Small but impactful for daily TUI users.

9. **[#4097 — Parent model burns turns with peek+sleep polling loop](https://github.com/Hmbown/CodeWhale/issues/4097)** *(1 comment, CLOSED)*  
   Mr-Moon121 flags a #3183 regression: wasteful polling instead of passive waiting. Affects sub-agent workflows at scale.

10. **[#3986 — API-key onboarding shows wrong config path](https://github.com/Hmbown/CodeWhale/issues/3986)** *(1 comment, CLOSED)*  
    Misleading UI when `CODEWHALE_HOME` is set. Fixed in PR #4254. Important for managed/isolated installs.

---

## 4. Key PR Progress (10 selected)

1. **[#4264 — Cache command and regex hot paths](https://github.com/Hmbown/CodeWhale/pull/4264)** *(OPEN)*  
   Introduces process-lifetime static storage for command groups and a bounded LRU regex cache for tool search. Targets #4155 and #4154.

2. **[#4263 — v0.8.68 batch: Android updater, Termux docs, perf consts, tool sandbox](https://github.com/Hmbown/CodeWhale/pull/4263)** *(CLOSED)*  
   Coherent multi-lane batch: Android asset selection in updater, `LANDLOCK` removal docs, string literal constants, and sub-agent `Arg0` tool sandboxing.

3. **[#4262 — Route AgentProfile pins through custom providers](https://github.com/Hmbown/CodeWhale/pull/4262)** *(CLOSED)*  
   Fixes #3965 by making AgentProfile the canonical surface for per-child provider routing, including user-named custom providers like `lm-studio`. Deliberately supersedes stale PR #3969.

4. **[#4255 — Models.dev refresh/snapshot automation](https://github.com/Hmbown/CodeWhale/pull/4255)** *(CLOSED)*  
   Implements #4117: a validate/dry-run-only Python script that fetches the public Models.dev catalog. Safety-first approach—no disk writes in refresh mode.

5. **[#4252 — Six-view model picker catalog browsing](https://github.com/Hmbown/CodeWhale/pull/4252)** *(CLOSED)*  
   Implements #4115: expands `/model` from two views to six (Configured, Catalog, Recent, Coding, Cheap, Long context). Major UX improvement for provider/model selection.

6. **[#4251 — Make work_update the canonical progress tool](https://github.com/Hmbown/CodeWhale/pull/4251)** *(CLOSED)*  
   Introduces `work_update` as the sole model-facing progress tool. Keeps `checklist_*` and `todo_*` as hidden compat aliases for legacy replay.

7. **[#4243 — Migrate runtime_threads maps to parking_lot::Mutex](https://github.com/Hmbown/CodeWhale/pull/4243)** *(CLOSED)*  
   Community contribution from wuisabel-gif. Migrates four `std::sync::Mutex` sites in `RuntimeThreadManager` to `parking_lot`. Named per issue claim protocol.

8. **[#4254 — Stopship dogfood UX fixes: slash aliases + API-key path](https://github.com/Hmbown/CodeWhale/pull/4254)** *(CLOSED)*  
   Fixes #3990 and #3986. Removes duplicate alias display and shows correct `CODEWHALE_HOME`-aware config path in onboarding.

9. **[#4096 — Sub-agent tool scoping plan and Phase 1 implementation](https://github.com/Hmbown/CodeWhale/pull/4096)** *(CLOSED)*  
   JayBeest's first contribution: three documentation files + Phase 1 implementation for #4042. Includes `SUBAGENT_TOOL_SCOPING_PLAN.md` and codebase guide.

10. **[#3902 — Fix five render/input hot paths](https://github.com/Hmbown/CodeWhale/pull/3902)** *(OPEN, 5 days old)*  
    Still open but critical: fixes double computation in task sidebar, input handler redraw, prompt rendering, autocomplete, and file tree. Includes multi-agent adversarial review.

---

## 5. Feature Request Trends

- **Fleet/AgentProfile unification**: Strong push to make `AgentProfile` the canonical contract for all agent roles, replacing parallel Fleet-only loadout systems (#4111, #4136, #4137, #4138).
- **Live model catalog**: Users want real-time provider/model metadata from Models.dev, not hand-curated bundled data (#4184, #4187, #4188, #4114, #4255).
- **Android/Termux support**: Growing demand for official Android arm64 builds beyond Linux arm64 workarounds (#4236 epic, #4237, #4238, #4241, #4242).
- **Sub-agent tool sandboxing**: Runtime enforcement of tool restrictions per sub-agent context (#4042, #4096). JayBeest's plan is community-driven and phased.
- **Per-sub-agent provider routing**: Independent model/provider selection for each sub-agent, especially for LM Studio users (#3965, #4262).

---

## 6. Developer Pain Points

- **High project velocity**: Contributors report difficulty keeping up with 10+ PRs/day. JayBeest filed a meta-issue (#4227) requesting onboarding automation. Community sentiment: "CodeWhale tsunami 🌊."
- **Unbounded state file growth**: `subagents.v1.json` reaches ~300k lines with no cleanup mechanism (#4217). Affects long-running sessions. Manual workaround: empty file and restart.
- **Wasteful polling loop regression**: Parent agents burn tokens on `peek → sleep → peek` loops while sub-agents run (#4097). Regression from #3183, still unresolved.
- **Overlapping provider/model truth**: Multiple sources of provider data (bundled JSON, hardcoded config, live catalog) create maintenance burden and user confusion (#4188).
- **Startup latency**: Despite fixes (#3757, #3761), launch performance still flagged as a concern for repeated TUI use.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*