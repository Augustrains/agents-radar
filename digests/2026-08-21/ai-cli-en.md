# AI CLI Tools Community Digest 2026-08-21

> Generated: 2026-08-21 00:32 UTC | Tools covered: 9

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

# AI CLI Developer Tools — Cross-Tool Comparison Report

**Date**: 2026-08-21  
**Scope**: Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi (pi-mono), Qwen Code, DeepSeek TUI (CodeWhale)

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape is maturing rapidly, with nine major open-source projects actively shipping releases, managing hundreds of community issues, and converging on similar architectural patterns. The ecosystem is characterized by a shared focus on MCP (Model Context Protocol) integration reliability, agent orchestration capabilities, and cross-platform parity — particularly Windows support, which remains a persistent weak point across nearly all tools. Security hardening is emerging as a first-class concern, with sandboxing improvements, credential handling, and supply-chain protections appearing across multiple projects simultaneously. The competitive landscape shows clear differentiation: Claude Code and Codex lead in feature maturity and community engagement, Gemini CLI and Qwen Code are investing heavily in agent subsystem stabilization, while smaller tools like Pi, Kimi, and CodeWhale are iterating rapidly on UX polish and niche differentiation.

---

## 2. Activity Comparison

| Tool | Releases (24h) | Hot Issues (Top 10) | Key PRs (24h) | Community Signals |
|------|---------------|--------------------|---------------|-------------------|
| **Claude Code** | 2 (v2.1.237, v2.1.238) | 10 tracked | 0 merged | Top issue at 316 👍; staged rollout breakage (#88370) |
| **OpenAI Codex** | 1 (v0.149.0) + 4 alphas | 10 tracked | 10 PRs | Auth regression cluster (21+ 👍); Windows archiving debt |
| **Gemini CLI** | 1 nightly | 10 tracked | 10 PRs | P1 subagent issues; security sandboxing focus |
| **GitHub Copilot CLI** | 1 (v1.0.81-6) | 10 tracked | 1 PR | Enterprise policy friction; MCP reliability dominant |
| **Kimi Code CLI** | 0 | 1 active | 1 PR | Emerging plugin ecosystem; memory feature request |
| **OpenCode** | 1 (v1.18.19) | 10 tracked | 10 PRs | TUI crashes; memory leak fix in PR #43733 |
| **Pi (pi-mono)** | 0 | 10 tracked | 10 PRs | Auto-compaction bug (17 👍); theme refactor open |
| **Qwen Code** | 2 (v0.21.15 + nightly) | 10 tracked | 10 PRs | /review pipeline hardening; Web Shell improvements |
| **CodeWhale (DeepSeek TUI)** | 1 (v0.9.10) | 10 tracked | 10 PRs | EPIC-005 refactor; i18n dictionary spine work |

**Key Observations**:  
- **Highest release velocity**: Claude Code (2 stable), Qwen Code (2), Codex (1 stable + 4 alphas)  
- **Most active PR pipeline**: Codex, Gemini CLI, OpenCode, Pi, Qwen, CodeWhale — each with 10+ PRs in flight  
- **Lowest activity**: Kimi Code (1 issue, 1 PR) — smallest community in this comparison  
- **Community engagement leader**: Claude Code (316 👍 on top issue) and Codex (21+ 👍 on auth regression)

---

## 3. Shared Feature Directions

The following requirements are emerging across multiple tool communities:

| Feature / Direction | Tools Citing | Specific Needs |
|---------------------|-------------|----------------|
| **Multi-line input / send key customization** | Claude Code (#keybindingFlavor), OpenCode (#shift+enter), CodeWhale (#5345), Copilot CLI (#1481) | Ctrl+Enter vs Shift+Enter confusion; proper multi-line Markdown input; Bash-style readline keybindings |
| **Session persistence & continuity** | Claude Code (#61172), Codex (#39162), Copilot CLI (#4530, #4539, #4543), Qwen Code (#9573), Gemini CLI (#28934) | Session name reset, recovery after crashes, WSL vs host anchoring, phantom errors on resume, history rollback |
| **MCP reliability & trust** | Claude Code (#88370, #61044, #86459), Copilot CLI (#3162, #4096, #4439), Gemini CLI (#28863), Pi (#8118) | Widget rendering, OAuth bridging, false policy blocking, parameter serialization, extension consent for env changes |
| **Multi-agent orchestration** | Codex (agents dashboard), Gemini CLI (#21409, #22323), Qwen Code (#8724), OpenCode (#43619), Copilot CLI (#4533) | Task lifecycle controls, subagent cost visibility, success/failure reporting accuracy, cross-session messaging |
| **Windows parity & stability** | Claude Code (#78037, #87879), Codex (#39150, #39161), Pi (#7547), Copilot CLI (#4524), Qwen Code (#9571) | OAuth re-auth loops, archiving failures, path handling (`\\?\` prefix), sandbox breaking git, input redraw |
| **Security hardening** | Gemini CLI (#28935, #28863), Qwen Code (#9527, #9577), OpenCode (#43735), Pi (#6093), Kimi (#2614) | Sandbox escapes, credential injection, PAT persistence, PTY auth, scoped API keys, digest-pinned images |
| **Context/token optimization** | Gemini CLI (#22745, #28934), Pi (#6879, #8133), DeepSeek TUI (#5518), Claude Code (#88412), Codex (#33493) | AST-aware reads, compaction profiles per model, emergency compaction thresholds, cache inheritance, unbounded payload retention |
| **Configurable sandbox / permission modes** | Copilot CLI (defaultPermissionMode), Gemini CLI (#19873), Qwen Code (#9577), OpenCode (#27875) | Per-session permission defaults, sandbox boundary flexibility, non-interactive auto-approval |
| **First-run UX / onboarding** | CodeWhale (#5522), Claude Code (Concise style), Copilot CLI (defaultMode) | Progressive onboarding, verbosity controls, default behavior configuration |
| **Localization / i18n** | Codex (#31963 zh-CN), CodeWhale (dictionary spine), Claude Code (non-Latin paths) | Reasoning label translation, CJK rendering, path encoding, locale parity enforcement |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach |
|------|--------------|-------------|-------------------|
| **Claude Code** | Production-grade stability, model behavior quality | Enterprise developers, teams with governance needs | Plugin marketplace, staged server-side rollouts, hooks-based enforcement |
| **OpenAI Codex** | Desktop/TUI parity, remote workflows | Pro users, multi-platform teams | Rust rewrite, TUI dashboard, desktop app + CLI sync, multi-agent V2 |
| **Gemini CLI** | Agent subsystem correctness, sandbox security | Google Cloud users, agent-heavy workflows | A2A server support, subagent ORCHESTRATION, macOS Seatbelt sandbox, bash-proficiency leverage |
| **GitHub Copilot CLI** | Enterprise governance, MCP ecosystem | GitHub Enterprise orgs, policy-bound teams | Managed settings, org-level model catalogues, OAuth bridging, ACP clients |
| **Kimi Code CLI** | Plugin ecosystem, persistent memory | Developers wanting lightweight, extensible CLI | stdio MCP server with explicit-memory tools, plugin subprocess model |
| **OpenCode** | Cross-provider support, UI responsiveness | Multi-provider users, TUI purists | Provider-agnostic core, built-in Cerebras/Cloudflare/Bedrock plugins, Effect/Promise plugin API |
| **Pi (pi-mono)** | Terminal UX fidelity, cross-tool muscle memory | Terminal power users, multi-model fleets | Hardware cursor support, soft-wrap copy preservation, theme refactor, per-model compaction |
| **Qwen Code** | Automated review pipelines, Web Shell | Enterprise code review teams, remote server workflows | /review orchestration, Aone Code integration, tmux-based evidence capture, provider-aware reasoning |
| **CodeWhale** | Architectural cleanliness, i18n parity | Open-source contributors, Chinese-speaking users | Crate decomposition (EPIC-005), dictionary-spine i18n, read_lints diagnostics, image content forwarding |

---

## 5. Community Momentum & Maturity

### Tier 1 — Established Leaders (high activity, large communities)
- **Claude Code**: Most mature community; 316 👍 on top issue signals strong engagement. Shipping 2 releases/day. Staged rollouts indicate enterprise-grade deployment discipline. Plugin marketplaces suggest ecosystem ambitions.
- **OpenAI Codex**: Fast-maturing with Rust rewrite; 10 PRs/day shows aggressive development. Desktop app + CLI strategy targeting prosumer market. Auth regressions are the "growth pain" of rapid iteration.

### Tier 2 — Rapid Iterators (heavy PR activity, active triage)
- **Gemini CLI**: Strong security posture, P1 subagent fixes show responsiveness. PR pipeline robust (10/day). Building evaluation infrastructure (76 tests) indicates medium-term reliability investment.
- **Qwen Code**: Aggressive feature velocity (2 releases/day), deep /review ecosystem investment. Web Shell improvements point to remote-first workflows. Community smaller but highly specialized.
- **OpenCode**: Healthiest PR variety (10/day), active contributor participation (community PRs, Amazon One Medical contribution). TUI fragility is the main community pain.
- **Pi (pi-mono)**: Unique position — Armin Ronacher contributing means high-quality TUI work. Per-model config granularity, compaction fixes, and cross-tool muscle memory alignment show deep user empathy.

### Tier 3 — Emerging / Niche
- **GitHub Copilot CLI**: Enterprise focus means fewer but higher-stakes issues. 1 PR/day seems low but parent company GitHub likely handles much internally. Community concentrated on MCP + policy.
- **CodeWhale (DeepSeek TUI)**: Impressive EPIC-005 refactor showing architectural discipline. i18n dictionary spine is a strong community-driven effort. Smaller community but very active contributor base.
- **Kimi Code CLI**: Early stage; single-issue focus on memory. Plugin ecosystem documentation suggests foundation-building rather than feature velocity.

---

## 6. Trend Signals

1. **Context Window Management is the New Battleground** — Auto-compaction failures (Pi #6879), premature compaction (CodeWhale #5518), cache inheritance loss (Claude Code #88412), and unbounded payloads (Codex #33493) all point to context-window economics as the #1 pain point for power users. Expect more investment in AST-aware reads, per-model compaction profiles, and smarter caching.

2. **MCP is Shifting from Novelty to Production Dependency** — MCP reliability issues dominate across 7 of 9 tools. False policy blocks, OAuth bridging failures, widget rendering regressions, and parameter stringification are eroding trust. Tools that solve MCP reliability will gain a competitive edge — this is the "ORM moment" for agent tooling.

3. **Agent Orchestration Needs Honest Reporting** — Subagents falsely reporting success (Gemini CLI #22323), stuck UI panels (Codex #38364), and parent-owned subagent integrity gaps (Codex PR #39792) indicate that multi-agent orchestration is moving from demo to production, and **accuracy of agent state reporting is critical for trust**.

4. **Windows Parity is a Persistent Competitive Moat** — Every major tool has Windows-specific pain points (auth loops, archiving failures, path handling, sandbox breaking git). Teams that invest in Windows QA will differentiate meaningfully — this is a consistent community complaint with no clear leader.

5. **Security Hardening is Accelerating** — Sandbox escape prevention (Gemini #28935), digest-pinned images (Qwen #9527), PTY auth (OpenCode #43735), and CI/CD credential hygiene (Qwen #9577) show security is now a feature, not an afterthought. This aligns with enterprise adoption timelines.

6. **First-Run Experience Determines Retention** — CodeWhale's #5522 (progressive onboarding), Claude Code's "Concise" style, and Copilot CLI's defaultMode all address the same signal: **users want control over verbosity and setup friction**. Tools that respect user attention will win daily-driver status.

7. **Cross-Tool Muscle Memory is a Real Cost** — Pi's community issues around `/exit`, `/quit`, `/bye` aliases and Claude Code's readline keybinding flavor show users expect consistency across tools. **Standardizing common commands is a low-effort, high-goodwill investment** for all tools.

8. **Localization is an Untapped Differentiator** — Codex's zh-CN label bug (15 comments) and CodeWhale's i18n dictionary spine (relentless `isZh` removal) show that non-English locales are underserved. Chinese-speaking developers are actively contributing; tools that prioritize i18n early will capture underserved markets.

9. **Web Shell / Remote Deployments Are Growing** — Qwen Code's Web Shell improvements, Codex's remote/mobile parity demands, and Copilot CLI's Remote-SSH issues all signal that **CLI tools are no longer local-only** — remote-first workflows are a growing requirement.

10. **Plugin Ecosystems Are Maturing with Governance** — Kimi's plugin security documentation, Claude Code's plugin marketplaces, and OpenCode's plugin API expansion show that plugins are becoming a first-class extensibility surface, **but security boundaries and data persistence need explicit formalization** (Kimi #2614 is the model to watch).

---

*Report compiled from community digest data for 2026-08-21. All metrics based on public GitHub activity and community engagement.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-08-21 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Skills have attracted the most community discussion and attention via Pull Requests:

### 1. skill-creator — Evaluation & Windows Compatibility Fixes (Multiple PRs)
**PRs:** [#1298](https://github.com/anthropics/skills/pull/1298) · [#1099](https://github.com/anthropics/skills/pull/1099) · [#1050](https://github.com/anthropics/skills/pull/1050) · [#539](https://github.com/anthropics/skills/pull/539)
**Status:** Open (all)
**Authors:** MartinCajiao, joshuawowk, gstreet-ops, Lubrsy706

Several PRs target the same core problem: `run_eval.py` (the skill-creator's evaluation harness) reports `recall=0%` for every query on Windows due to subprocess pipe reading failures. This makes the optimization loop in `run_loop.py` and `improve_description.py` optimize against noise. Additional fixes address `claude.cmd` PATHEXT resolution, encoding issues, and YAML frontmatter validation for unquoted descriptions.

**Why it's trending:** The skill-creator is the meta-tool for building all other Skills, so its reliability directly blocks the entire ecosystem's growth. This is the community's most actively-worked fix area.

---

### 2. document-typography — Typographic Quality Control
**PR:** [#514](https://github.com/anthropics/skills/pull/514)
**Status:** Open
**Author:** PGTBoos

Prevents common typographic issues in AI-generated documents: orphan word wrap (1–6 words spilling to next line), widow paragraphs (headers stranded at page bottom), and numbering misalignment. These issues affect every document Claude generates. Large, contained, and immediately applicable scope.

---

### 3. ODT Skill — OpenDocument Creation & Conversion
**PR:** [#486](https://github.com/anthropics/skills/pull/486)
**Status:** Open
**Author:** GitHubNewbie0

Adds a new `odt` skill for creating, filling, reading, and converting OpenDocument Format files (`.odt`, `.ods`). Triggers on mentions of ODT/ODS/ODF/OpenDocument/LibreOffice. Fills a gap alongside existing PDF and DOCX skills.

---

### 4. PDF Skill — Case-Sensitivity Fixes
**PR:** [#538](https://github.com/anthropics/skills/pull/538)
**Status:** Open
**Author:** Lubrsy706

Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` — `REFERENCE.md` → `reference.md` and `FORMS.md` → `forms.md`. Breaks on case-sensitive filesystems (Linux/macOS).

---

### 5. frontend-design — Clarity & Actionability Improvements
**PR:** [#210](https://github.com/anthropics/skills/pull/210)
**Status:** Open
**Author:** justinwetch

Revises the frontend-design skill so every instruction is something Claude can actually follow within a single conversation, with specific guidance to steer behavior without being overly prescriptive. Directly addresses usability of an existing skill.

---

### 6. self-audit — Mechanical Verification + Reasoning Quality Gate
**PR:** [#1367](https://github.com/anthropics/skills/pull/1367)
**Status:** Open
**Author:** YuhaoLin2005

A universal skill that audits AI output before delivery: mechanical file verification first (every claimed output file must exist), then a four-dimension reasoning audit in damage-severity priority order. Works with any project, tech stack, or model.

---

### 7. testing-patterns — Comprehensive Testing Skill
**PR:** [#723](https://github.com/anthropics/skills/pull/723)
**Status:** Open
**Author:** 4444J99

Covers the full testing stack: Testing Trophy philosophy, unit testing (AAA pattern, naming), React component testing (Testing Library), and integration/E2E patterns. An authoring-focused skill.

---

### 8. ServiceNow Platform Skill
**PR:** [#568](https://github.com/anthropics/skills/pull/568)
**Status:** Open
**Author:** Vanka07

Broad ServiceNow assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD/CSM, SPM/PPM, Vulnerability Response, and Security Incident Response. Largest-scope enterprise skill in flight.

---

## 2. Community Demand Trends

Distilled from community Issues, the most-anticipated new Skill directions are:

| Trend | Signal | Supporting Issue |
|---|---|---|
| **Security & Trust** | Community skills under `anthropic/` namespace create trust boundary abuse; users demand secure skill distribution | [#492](https://github.com/anthropics/skills/issues/492) — 43 comments |
| **Org-wide Skill Sharing** | Skills should be shareable within an organization without manual .skill file transfers | [#228](https://github.com/anthropics/skills/issues/228) — 16 comments, 8 👍 |
| **Eval Harness Reliability** | `run_eval.py` failing on Windows blocks the entire skill-creator loop | [#556](https://github.com/anthropics/skills/issues/556) — 12 comments, 7 👍 |
| **Skill Deduplication** | `document-skills` and `example-skills` plugins install identical content, wasting context window | [#189](https://github.com/anthropics/skills/issues/189) — 6 comments, 9 👍 |
| **Context Window Efficiency** | `claude-api` skill eagerly injects ~156k tokens in a single tool call | [#1487](https://github.com/anthropics/skills/issues/1487) |
| **Agent Governance** | Safety patterns for AI agent systems — policy enforcement, audit trails, trust scoring | [#412](https://github.com/anthropics/skills/issues/412) |
| **State Compression** | `compact-memory` — symbolic notation for compact agent state to reduce context bloat | [#1329](https://github.com/anthropics/skills/issues/1329) |

**Dominant themes:** reliability of the skill toolchain, security/trust boundaries, and context-window efficiency.

---

## 3. High-Potential Pending Skills

Active-comment PRs not yet merged — these may land soon:

| Skill | PR | Author | Why It May Merge |
|---|---|---|---|
| **servicepiral ServiceNow skill** | [#568](https://github.com/anthropics/skills/pull/568) | Vanka07 | Enterprise demand; updated as recently as 2026-08-12 (9 days ago) |
| **pyxel (retro game dev)** | [#525](https://github.com/anthropics/skills/pull/525) | kitao | Author maintains pyxel-mcp; niche but active |
| **skill-quality-analyzer + skill-security-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | eovidiu | Directly addresses the #492 security concern; meta-skills for the ecosystem |
| **self-audit skill** | [#1367](https://github.com/anthropics/skills/pull/1367) | YuhaoLin2005 | Strong proposal backing in Issue #1385; recently updated |
| **template/SKILL.md spec compliance** | [#1538](https://github.com/anthropics/skills/pull/1538) | bechor25 | Fixes spec violations in the repo's own templates — likely to merge for consistency |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, secure skill-development toolchain** — specifically, fixing the `skill-creator` evaluation harness (which blocks Windows users from iterating on any new Skill) and addressing the trust boundary where community skills masquerade under the `anthropic/` namespace.

---

# Claude Code Community Digest — 2026-08-21

## 1. Today's Highlights

Two releases shipped in the last 24 hours: **v2.1.238** introduces a `keybindingFlavor` setting for readline-style Ctrl+W behavior and new plugin marketplace header helpers, while **v2.1.237** fixes prompt caching for LLM gateways/custom base URLs and adds a built-in "Concise" output style. The community remains most animated about **#77136** (repetitive rhetorical tics across Claude models, 316 👍), and a new report of **MCP Apps widgets breaking** after the staged `server/discover` rollout (#88370) is drawing immediate attention.

## 2. Releases

### v2.1.238
- **New `keybindingFlavor` setting**: Set to `"readline"` for Ctrl+W to delete back to previous whitespace (Bash-style); default `"classic"` unchanged.
- **Plugin marketplaces**: `headersHelper` on URL marketplaces or catalog entries now runs a command that m... (description truncated)

### v2.1.237
- **Fixed prompt caching** for sessions using an LLM gateway or custom base URL.
- **New "Concise" output style**: Claude leads with results, skips preamble/narration, but does the same thorough work. Select via Output style in `/config`.

## 3. Hot Issues (Top 10)

1. **[#77136 — Repetitive rhetorical tics across Claude 4.7/4.8/5.0/Fable](https://github.com/anthropics/claude-code/issues/77136)** 
   *316 👍, 49 comments.* The highest-engagement open issue. Users report Claude increasingly defaults to repetitive rhetorical tics and struggles with coherent prose despite explicit style instructions. This has broad implications for code documentation and agent-generated text quality.

2. **[#84352 — CVP-approved org still receives cyber safeguard blocks](https://github.com/anthropics/claude-code/issues/84352)**
   *132 comments, 21 👍.* A Claude.ai org with prior Cyber Verification Program approval is again blocked; portal shows "Under review" despite approval email. High comment count suggests many affected users.

3. **[#88370 — MCP Apps widgets stopped rendering after server/discover rollout](https://github.com/anthropics/claude-code/issues/88370)**
   *5 comments, new today.* Widgets (`_meta.ui.resourceUri`) stopped rendering mid-evening with no client/server changes — evidence points to staged server-side `server/discover` version negotiation (v2.1.234). Breaking change in staged rollout.

4. **[#61044 — MCP tool calls in CCR Routines fail with "requires approval"](https://github.com/anthropics/claude-code/issues/61044)**
   *18 comments, 6 👍.* Routines hit approval walls with no UI shown; reconnect doesn't help. Automation workflows blocked.

5. **[#61172 — /clear inherits previous session name](https://github.com/anthropics/claude-code/issues/61172)**
   *12 comments, 15 👍.* /clear doesn't reset session name, causing duplicate-named sessions in /resume. Minor but confusing UX pain.

6. **[#78037 — OAuth refresh token rejected after ~24h on Windows](https://github.com/anthropics/claude-code/issues/78037)**
   *3 comments.* Max-sub users forced to `/login` daily. Platform-specific auth reliability issue.

7. **[#86459 — MCP array/list parameters silently stringified mid-call](https://github.com/anthropics/claude-code/issues/86459)**
   *2 comments.* Intermittent stringification breaks tools expecting `List[str]` — intermittent bugs are the worst to debug.

8. **[#88412 — Waking idle agent fork forfeits inherited prompt cache](https://github.com/anthropics/claude-code/issues/88412)**
   *New today.* Cache read pinned to fixed boundary, not TTL. Direct cost implications for agent-heavy workflows.

9. **[#88405 — Symlinked files in .claude/rules/ not auto-loaded](https://github.com/anthropics/claude-code/issues/88405)**
   *New today.* Directly contradicts docs; breaks shared-rules workflows.

10. **[#70674 — Path encoding strips non-Latin characters on Windows](https://github.com/anthropics/claude-code/issues/70674)**
    *Closed.* Directories collide, sessions cross-project visible, cleanup causes data loss. Serious bug for non-Latin users; worth confirming fix version.

## 4. Key PR Progress

*No pull requests were updated or merged in the last 24 hours.*

## 5. Feature Request Trends

- **Daemon/background mode** ([#88197](https://github.com/anthropics/claude-code/issues/88197)): Users want Codex-style remote daemon sessions with background process management and session persistence — `claude agents` dying overnight is a real workflow blocker.
- **Agent adherence to CLAUDE.md/memory** ([#88285](https://github.com/anthropics/claude-code/issues/88285)): Frustration with agents "willfully forgetting" rules; hooks are the only enforcement mechanism. Demand for reliable memory/rule persistence.
- **Cross-session messaging parity**: Linux has `agents_cross_session_inbox` working; Windows doesn't ([#87870](https://github.com/anthropics/claude-code/issues/87870)). Feature parity across platforms is a recurring theme.
- **Output style customization**: The new "Concise" style in v2.1.237 suggests Anthropic is responding to demand for more controlled verbosity — expect more style options.
- **Readline keybindings** ([v2.1.238](https://github.com/anthropics/claude-code/releases)): Bash-style editing is a niche but passionate ask; community-driven addition.

## 6. Developer Pain Points

- **Cyber safeguard false positives** ([#84352](https://github.com/anthropics/claude-code/issues/84352), [#73039](https://github.com/anthropics/claude-code/issues/73039), [#73031](https://github.com/anthropics/claude-code/issues/73031), [#73015](https://github.com/anthropics/claude-code/issues/73015)): Legitimate work gets session-halted by safety filters. Multiple reports, high engagement.
- **Data loss / session integrity**: ParentUuid chains broken after compaction ([#46603](https://github.com/anthropics/claude-code/issues/46603)), early conversation segments lost ([#88410](https://github.com/anthropics/claude-code/issues/88410)), stale resume state ([#88243](https://github.com/anthropics/claude-code/issues/88243)). Trust-eroding issues.
- **Windows-specific instability**: MSIX update silo leaks blocking launch ([#87879](https://github.com/anthropics/claude-code/issues/87879)), Cowork VM file handle leaks ([#87607](https://github.com/anthropics/claude-code/issues/87607)), daily OAuth re-auth ([#78037](https://github.com/anthropics/claude-code/issues/78037)).
- **Model behavior regression**: Repetitive rhetorical tics ([#77136](https://github.com/anthropics/claude-code/issues/77136)) and model self-fabricating user turns ([#85215](https://github.com/anthropics/claude-code/issues/85215)) point to broader model quality concerns.
- **MCP reliability**: Approval deadlocks in routines ([#61044](https://github.com/anthropics/claude-code/issues/61044)), widget rendering breaks ([#88370](https://github.com/anthropics/claude-code/issues/88370)), param stringification ([#86459](https://github.com/anthropics/claude-code/issues/86459)) — MCP remains the most fragile integration surface.
- **macOS permission fatigue**: TCC re-requests on every auto-update on macOS 27 beta ([#70094](https://github.com/anthropics/claude-code/issues/70094)) — friction for beta testers.

---

*Digest generated from GitHub data for 2026-08-21. All links point to the public anthropics/claude-code repository.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-21

## Today's Highlights

The v0.149.0 release cycle brings a major TUI upgrade with the new interactive `codex agents` dashboard for task management, alongside new working-directory commands (`/cd`, `/pwd`, `/cwd`). However, the community is buzzing about a **critical regression** affecting Windows and macOS users: opening existing conversations can trigger authentication invalidation and sign-out loops, with 21+ upvotes across duplicate reports. Additionally, a growing cluster of Windows-specific archiving failures (5+ open issues) signals an unresolved session-management debt that the team is actively patching.

---

## Releases

**rust-v0.149.0** ([Release](https://github.com/openai/codex/releases/tag/rust-v0.149.0))
- **Interactive `codex agents` dashboard**: Search, start, open, rename, and stop tasks with configurable keyboard shortcuts (#39094, #39112, #39114, #39142)
- **New TUI working-directory commands**: `/cd`, `/pwd`, and `/cwd` for session path management (#38894)

**Pre-releases**: rust-v0.150.0-alpha.1, rust-v0.149.0-alpha.7, rust-v0.149.0-alpha.4, rust-v0.149.0-alpha.3 (snapshot releases for testing; no notable changelog details published)

---

## Hot Issues

1. **[#39162 — macOS: Opening existing conversation invalidates ChatGPT auth](https://github.com/openai/codex/issues/39162)** (28 comments, 21 👍)
   Critical regression in build 26.814.41407 where opening a prior conversation redirects to sign-in. Auth handling across desktop builds is a top-priority concern; duplicate reports suggest a systemic issue.

2. **[#33493 — Local compaction v2 retains unbounded image payloads](https://github.com/openai/codex/issues/33493)** (19 comments)
   Long-running image-heavy threads enter repeated auto-compaction loops. This is a context-window management bug that causes performance degradation and extra token spend — a high-impact issue for daily users.

3. **[#39189 — Windows: Opening a thread signs out Pro account after 401](https://github.com/openai/codex/issues/39189)** (16 comments, 3 👍)
   Mirrors the macOS auth regression, but with "workspace-only settings 401" triggering sign-out for personal Pro accounts. Cross-platform auth instability is clearly a hot regression area.

4. **[#35746 — Paginated history drops rollout records and reuses ordinals](https://github.com/openai/codex/issues/35746)** (16 comments)
   Rollout history decoding inconsistency when paginating; valid records dropped, causing potential data loss in session history. This affects CLI users heavily and is unresolved across 0.146.x alphas.

5. **[#39150 — Windows: Cannot archive conversations with `\\?\` path prefix](https://github.com/openai/codex/issues/39150)** (12 comments, 2 👍)
   Extended-length Windows paths break archiving entirely. This is part of a clog of Windows archiving bugs (see also #39161, #39705, #39627) suggesting a deep-seated Windows path-handling issue.

6. **[#31963 — zh-CN renders both xhigh and ultra reasoning as “极高”](https://github.com/openai/codex/issues/31963)** (15 comments, 5 👍)
   Localization bug causing model effort confusion for Chinese users; i18n regressions signal QA gaps in the desktop app release pipeline.

7. **[#38364 — Subagents panel stuck showing "Active and Working"](https://github.com/openai/codex/issues/38364)** (11 comments)
   Completed subagents never update state in the UI panel. This erodes trust in the multi-agent orchestration UX and is generating heightened attention as agentic workflows become more popular.

8. **[#39161 — Windows: "Could not archive conversation" generic error](https://github.com/openai/codex/issues/39161)** (9 comments, 14 👍)
   High-upvote duplicate demonstrating a broad archiving failure on Windows desktop; both `\\?\` paths and legacy tasks are implicated (see #39627).

9. **[#38503 — "Too many requests" blocks access during normal web use](https://github.com/openai/codex/issues/38503)** (5 comments, 10 👍)
   Web rate limiter triggers on normal usage and blocks Work tasks. Visible modal confuses users and interrupts workflows — an incident-level concern in web/desktop parity.

10. **[#38939 — macOS: Runaway computer-use threads crash the app (V8 OOM)](https://github.com/openai/codex/issues/38939)** (4 comments)
    Spawns unbounded computer-use threads until dispatch thread exhaustion and fatal V8 OOM crash. A niche but severe crash-in-the-wild bug.

---

## Key PR Progress

1. **[#39822 — Preserve uncapped Guardian classifier instructions](https://github.com/openai/codex/pull/39822)**
   Fixes implicit truncation of policy instructions in Guardian v2 when no token limit is set. Important for policy fidelity in safety-classifier environments.

2. **[#39813 — Defer legacy filesystem policy projection](https://github.com/openai/codex/pull/39813)**
   Performance optimization — skips rebuilding legacy filesystem policy unless a cwd change can actually rebind; reduces session-setting churn.

3. **[#39811 — Restrict macOS preference reads to full-disk policies](https://github.com/openai/codex/pull/39811)**
   Security fix: prevents Seatbelt preferences and cfprefsd from exposing sandbox-adjacent data unless full-disk access is granted. Strengthens sandbox boundaries.

4. **[#39809 — Preserve WINDIR in core Windows shell environments](https://github.com/openai/codex/pull/39809)**
   Adds `WINDIR` to the allowlist for Windows core environment variables, ensuring case-variant env vars are not lost — a Linux-vs-Windows parity fix for tooling.

5. **[#39804 — Use multi-agent V1 for Amazon Bedrock models](https://github.com/openai/codex/pull/39804)**
   Bedrock lacks support for response items required by multi-agent V2; normalizes catalog to advertise V1. Compliance fix for a major cloud provider.

6. **[#39802 — Optimize case-insensitive thread history matching](https://github.com/openai/codex/pull/39802)**
   Eliminates full-span rescans by using monotonic span cursors; improves search performance for long threads.

7. **[#39798 — Update rmcp to 3.1.3](https://github.com/openai/codex/pull/39798)**
   Keeps MCP discovery robust — preserves auth-required and retryable classifications when legacy fallback is triggered.

8. **[#39795 — Add hostname to the configurable TUI status line](https://github.com/openai/codex/pull/39795)**
   Useful for teams running multi-host or remote Codex sessions; configurable status item with no DNS resolution overhead.

9. **[#39792 — Reject settings updates for parent-owned subagents](https://github.com/openai/codex/pull/39792)**
   Hardens Multi-Agent V2 by disallowing direct settings mutations on parent-owned subagents — closes a potential integrity gap in agent orchestration.

10. **[#39785 — Support turn cost telemetry for custom model providers](https://github.com/openai/codex/pull/39785)**
    Extends cost tracking beyond OpenAI endpoints; routes through provider-specific auth while excluding unsupported providers (e.g., Bedrock). Critical for multi-provider cost observability.

---

## Feature Request Trends

- **Agent/Task Management Surface**: Users are actively pushing for richer task lifecycle controls — the new `codex agents` dashboard and TUI path commands are direct responses to this demand, but issues like #22947 (remote control for general chats) show the surface area is still expanding.
- **Multi-Agent Cost Transparency**: Issue #39808 highlights a growing demand for subagent overhead visibility and cost accounting — a sign that agentic workflows are moving from experimentation to production use.
- **Better Remote/Mobile Parity**: Desktop-to-mobile remote features are maturing, and users want full feature parity (general chats, no 30s timeouts) — a sign that "remote as a first-class experience" is becoming a core expectation.
- **Localization and Accessibility**: The zh-CN reasoning-label bug (#31963) is the most-upvoted i18n complaint this week, and there are consistent requests for optional Markdown input in IDE extensions (#37972).
- **Sandbox Flexibility**: Requests to support more host filesystems (Google Drive VFS, macOS preferences) and plugin opt-outs (#39682) reflect a strong desire for configurable sandbox boundaries.

---

## Developer Pain Points

1. **Auth instability on desktop (macOS + Windows)**: The #39162 cluster — 21 upvotes and rising — indicates that auth invalidation on thread open is **the** top complaint. Duplicate reports across platforms suggest a common root cause in the desktop app’s session/credential storage, and the issue has remained open without acknowledgment of a fix.

2. **Windows archiving is a mess**: Five-plus distinct issues (#39150, #39161, #39705, #39627, #35914) all trace back to path handling, readonly file issues, or duplicate rollout scheduling. The community perceives Windows as a second-class platform in desktop release QA.

3. **Unbounded resource consumption**: Whether it’s image payloads in compaction (#33493), runaway computer-use threads (#38939), or subagent context overhead (#39808), users are hitting real costs and crashes from missing resource limits. These are high-severity for power users running long-lived sessions.

4. **Rate-limit false positives**: Multiple reports (#38503, #38763, #39771) show "Too many requests" modals appearing during normal usage, blocking access to chat history. This is a trust-damaging bug for Web/desktop workflows, and the silent 8.5-minute WebSocket "false dead-stream" (#39771) suggests underlying connectivity health checks are still immature.

5. **Plugin/skills discovery inconsistencies**: Issues #39682 (remote_plugin=false still downloads plugins) and #39805 (TUI harness not finding skills in `~/.codex`) indicate that plugin/config resolution remains flaky in TUI and desktop environments — a blocker for users adopting the new skills system.

---

*Digest generated from [openai/codex](https://github.com/openai/codex) activity on 2026-08-21.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest
**2026-08-21**

---

## 1. Today's Highlights

The Gemini CLI team is heavily focused on stabilizing the agent subsystem, with a nightly release addressing empty text turn preservation, while maintainers continue triaging a cluster of subagent-related bugs including hangs, incorrect success reporting, and configuration overrides. A notable wave of infrastructure PRs landed for PR generation, sandbox security hardening (especially macOS Seatbelt and git environment sanitization), and context optimization via history rollback and retry nudge improvements. Community-reported pain points around Auto Memory, browser agent resilience, and shell execution hangs remain active priorities with several issues in need of retesting.

---

## 2. Releases

**v0.56.0-nightly.20260820.ge90c63fa1** (published 2026-08-20)

- **fix(core):** Preserve empty text turns when tools or media are present — prevents loss of conversational context in mixed-content turns
- **Changelog update:** Added for upcoming v0.57.0-preview.0

**Full Changelog:** https://github.com/google-gemini/gemini-cli/compare/... (truncated in source data)

---

## 3. Hot Issues

The following 10 issues are generating the most community discussion and maintainer attention:

### 1. **Subagent recovery falsely reported as GOAL success** — [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)  
**Priority P1 | 12 comments | 👍 2**  
A subagent that hits MAX_TURNS before completing analysis reports `status: "success"` with `Termination Reason: "GOAL"` — misleadingly masking an interruption. This is a correctness issue that undermines trust in agent reporting.

### 2. **Generalist agent hangs indefinitely** — [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)  
**Priority P1 | 8 comments | 👍 8**  
When deferring to the generalist agent for simple tasks (e.g., folder creation), it hangs for up to an hour with no resolution. Workaround: instructing the model not to defer to subagents. High community impact.

### 3. **Zero-Dependency OS Sandboxing via bash affinity** — [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)  
**Priority P2 | 8 comments | 👍 1**  
Proposes leveraging Gemini 3's native bash proficiency with POSIX tools while enforcing security through OS-level sandboxing rather than restricting tool access. Large effort enhancement with security implications.

### 4. **Robust component-level evaluations** — [#24353](https://github.com/google-gemini/gemini-cli/issues/24353)  
**Priority P1 | 7 comments**  
Tracks expansion of the behavioral eval system (76 tests across 6 Gemini models). Critical for regression prevention as agent complexity grows.

### 5. **AST-aware file reads, search, and codebase mapping** — [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)  
**Priority P2 | 7 comments | 👍 1**  
Investigates whether AST-aware tools can reduce token consumption and improve navigation precision through single tool calls that capture exact method bounds.

### 6. **Gemini doesn't proactively use skills and sub-agents** — [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)  
**Priority P2 | 6 comments**  
Anecdotal evidence that custom skills (gradle, git) are never invoked unless explicitly instructed. Model misses opportunities to leverage user-defined agents.

### 7. **Shell command stuck at "Waiting input" after completion** — [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)  
**Priority P1 | 4 comments | 👍 3**  
Simple CLI commands complete but the CLI remains stuck showing "Awaiting user input". Particularly frustrating for automation workflows.

### 8. **Auto Memory retries low-signal sessions indefinitely** — [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)  
**Priority P2 | 5 comments**  
Sessions the extraction agent deems low-signal are never marked processed, causing infinite re-surfacing. Memory system efficiency issue.

### 9. **Browser Agent ignores settings.json overrides** — [#22267](https://github.com/google-gemini/gemini-cli/issues/22267)  
**Priority P2 | 3 comments**  
Configuration overrides (e.g., `maxTurns`) in global/project settings are merged by AgentRegistry but not applied by the Browser Agent.

### 10. **Model creates tmp scripts in random locations** — [#23571](https://github.com/google-gemini/gemini-cli/issues/23571)  
**Priority P2 | 3 comments**  
When restricted to shell execution only, the model scatters edit scripts across directories, creating cleanup overhead and dirty workspaces.

---

## 4. Key PR Progress

### 1. **History rollback and retry nudge optimizations** — [#28934](https://github.com/google-gemini/gemini-cli/pull/28934)  
Rolls back synthetic tool-cancellation text instead of appending to history, reduces API request volume, and maximizes prefix caching on retries. Prevents context window bloat.

### 2. **A2A server stale cancellation error fix** — [#28940](https://github.com/google-gemini/gemini-cli/pull/28940)  
Fixes state corruption where subsequent prompts after abort/cancel crash with `Execution aborted`. Resolves "execution stopped" in Google Cloud Assistant.

### 3. **GIT_CONFIG_* environment consistency** — [#28938](https://github.com/google-gemini/gemini-cli/pull/28938)  
`sanitizeEnvironment()` could emit malformed `GIT_CONFIG_*` triplets that git refuses to parse, breaking **every** git invocation. High-impact fix for git-heavy workflows.

### 4. **Interrupted response placeholder persistence** — [#28939](https://github.com/google-gemini/gemini-cli/pull/28939)  
Stops persisting `[The previous response was interrupted...]` as synthetic model response in session history, preventing contamination of subsequent context and prefix caching.

### 5. **macOS Seatbelt sandbox: container runtime isolation** — [#28935](https://github.com/google-gemini/gemini-cli/pull/28935)  
Blocks access to Docker/container runtime daemon sockets, binaries, Mach/XPC services, and POSIX shared memory to prevent sandbox escapes via VirtioFS mounts.

### 6. **Extension consent for environment changes** — [#28863](https://github.com/google-gemini/gemini-cli/pull/28863)  
Fixes bypass where extension updates could inject unauthorized environment variables into MCP server processes. Consent strings now cover environment configs.

### 7. **PR generator orchestrator state machine** — [#28933](https://github.com/google-gemini/gemini-cli/pull/28933)  
Implements centralized Orchestrator for iterative bug-fixing, evaluation sandbox isolation, ESLint static analysis, and trajectory logging.

### 8. **Remove unsafe `diff.external` override** — [#28930](https://github.com/google-gemini/gemini-cli/pull/28930)  
Fixes #28928: git interprets empty `diff.external` as "run no external diff" (unsafe), causing failures. Removes the override added in #28792.

### 9. **Gemini 3.7/3.6 Flash model support** — [#28910](https://github.com/google-gemini/gemini-cli/pull/28910)  
Adds full model resolution configuration for Gemini 3.7 Flash, 3.6 Flash, and 3.5 Flash-Lite across core and CLI packages.

### 10. **Preview model substitution warning** — [#28828](https://github.com/google-gemini/gemini-cli/pull/28828)  
Fixes #28825: silently rewrites preview model requests (e.g., `gemini-3.1-pro-preview`) to auto alias when no entitlement exists. Now emits a warning.

---

## 5. Feature Request Trends

Several clear directions emerge from recent GitHub activity:

1. **Smarter agent orchestration** — Deciding **when** to use subagents/skills vs. direct execution continues to be a dominant theme. Community and maintainers both want better automatic routing (issues #21968, #21409, #19873).

2. **Security as a first-class concern** — Multiple efforts focus on sandboxing, secret redaction, consent prompts, and preventing destructive git operations (PRs #28935, #28863; issues #19873, #26525, #22672).

3. **Context and token optimization** — AST-aware file reads, "tactful extraction" hierarchies, and history rollback optimizations all target reducing token bloat and improving context retention (issues #22745, #19561, PRs #28934, #28939).

4. **Memory system maturation** — Auto Memory improvements span retry behavior, deterministic redaction, invalid patch quarantine, and logging reduction (issues #26522, #26525, #26523, #26516).

5. **Enhanced visibility and evaluation infrastructure** — Subagent trajectory sharing via `/chat share`, robust component evals, and better bug reports with subagent context (issues #22598, #24353, #21763).

---

## 6. Developer Pain Points

Recurring frustrations from the community:

1. **Agent hangs are a systemic problem** — The generalist agent hanging for up to an hour on simple tasks (#21409) and shell commands staying "active" after completion (#25166) are among the most upvoted issues.

2. **Misleading success reporting** — Subagents reporting `GOAL` success when actually interrupted (#22323) erodes trust in agent status signals.

3. **Configuration not respected** — Browser Agent ignoring `settings.json` overrides (#22267) and subagents running when agents mode is disabled (#22093) point to unpredictable configuration behavior.

4. **Environmental edge cases** — Issues with Wayland browser subagents (#21983), symlinked agent files not recognized (#20079), and macOS sandbox escapes indicate cross-platform inconsistencies.

5. **Context pollution and bloat** — Interrupted responses persisted as model history, synthetic tool-cancellation text, and tmp scripts scattered across directories all contribute to dirty workspaces and inflated token usage (#28939, #23571, #28934).

6. **Silent behavior changes** — Preview model substitution without user notification (#28828) and silent skipping of invalid memory patches (#26523) highlight the need for better transparency.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest – 2026-08-21**

---

## 1. Today's Highlights

Release v1.0.81-6 shipped a long-requested improvement: `defaultMode` and `defaultPermissionMode` settings now let users control startup behavior and approval flow for new sessions, alongside `--with-token` support for non-interactive auth. Issue activity is dominated by enterprise policy and MCP integration problems — org-level model catalogues, managed settings validation, and OAuth bridging failures are top community complaints. Session continuity across environments (WSL host anchoring, Remote-SSH reconnects) is a growing cluster of fresh reports.

---

## 2. Releases

**v1.0.81-6** (released within last 24h)

- **Added:** `defaultMode` and `defaultPermissionMode` settings — enables choosing startup mode and default approval behavior for new interactive sessions.
- **Added:** `--with-token` flag for `copilot login`, allows reading an auth token directly from stdin (useful for scripting/CI).
- **Improved:** ACP clients now receive subagent IDs, raw event subscriptions, and live title updates.

🔗 [View release](https://github.com/github/copilot-cli/releases)

---

## 3. Hot Issues (Top 10 Noteworthy)

1. **#1481 – SHIFT+ENTER executes prompt instead of line break** (28 comments, 17👍)  
   Standard chat UX expected; `CTRL+ENTER` is unintuitive. Closed recently, but the 28-comment thread shows how long-standing and irritating this has been.  
   🔗 [Issue #1481](https://github.com/github/copilot-cli/issues/1481)

2. **#4390 – Org-enabled models missing from catalogue** (15 comments, 7👍)  
   Claude Sonnet 5 / Opus 5 and Kimi K3 unavailable despite being explicitly enabled by Copilot Business. Enterprise users are blocked from approved models — a serious governance gap.  
   🔗 [Issue #4390](https://github.com/github/copilot-cli/issues/4390)

3. **#3162 – MCP registry servers falsely flagged as blocked** (7 comments, 1👍)  
   v1.0.42 false-negative on registry validation. Custom servers that should be permitted are blocked — a trust-breaking bug for MCP adopters.  
   🔗 [Issue #3162](https://github.com/github/copilot-cli/issues/3162)

4. **#4096 – OAuth MCP tools never bridged to CLI sessions** (6 comments, 2👍)  
   Atlassian Remote MCP shows "Connected" in app UI but tools never appear in CLI. OAuth token handoff appears broken — core MCP workflow failure.  
   🔗 [Issue #4096](https://github.com/github/copilot-cli/issues/4096)

5. **#4503 – SDK server reports ready without auth token** (5 comments)  
   Slack-session creation fails generically because `COPILOT_SDK_AUTH_TOKEN` missing. Error message unhelpful; readiness probe misleading.  
   🔗 [Issue #4503](https://github.com/github/copilot-cli/issues/4503)

6. **#4439 – GitLab MCP OAuth rejected on RFC 8414 issuer mismatch** (5 comments, 3👍)  
   GitLab Self-Managed MCP with DCR fails. Interop with third-party MCP servers is a recurring theme — standards compliance needed.  
   🔗 [Issue #4439](https://github.com/github/copilot-cli/issues/4439)

7. **#4206 – Environment footer stuck on "Loading" forever** (4 comments, 3👍)  
   Built-in GitHub MCP handshake stalls under org policy; `/env` confirms everything is loaded, yet UI never resolves. Cosmetic but disruptive.  
   🔗 [Issue #4206](https://github.com/github/copilot-cli/issues/4206)

8. **#4038 – Non-interactive mode: late MCP injects empty user message** (3 comments)  
   With 7+ MCP tools, an empty turn replaces the real prompt; model echo/system-prompt leaks instead of answering. Non-interactive sessions unreliable with MCP.  
   🔗 [Issue #4038](https://github.com/github/copilot-cli/issues/4038)

9. **#4524 – Sandbox blocks git entirely on Windows** (3 comments)  
   Enforced sandbox too restrictive: even with working dir + `~/.copilot` enabled, git usage fails. Windows sandboxing needs serious UX rework.  
   🔗 [Issue #4524](https://github.com/github/copilot-cli/issues/4524)

10. **#4535 – `store_memory` fails: "Instance id is required"** (3 comments)  
    Regression in v1.0.81 prerelease; memory writer invoked without required instance ID. Affects long-term memory features for agents.  
    🔗 [Issue #4535](https://github.com/github/copilot-cli/issues/4535)

---

## 4. Key PR Progress

*Only 1 PR updated in last 24h — listed, plus notable context.*

1. **#4510 – Remove GitHub Copilot CLI documentation from README** (OPEN)  
   Strips installation and usage guidance from README. Community impact unclear — could signal move to dedicated docs site, or a concerning reduction in discoverability.  
   🔗 [PR #4510](https://github.com/github/copilot-cli/pull/4510)

> No other PRs received updates in the 24h window. Given the high volume of triaged issues closed recently, expect a large batch merge in the next release cycle.

---

## 5. Feature Request Trends

- **Session Persistence & Continuity** — Persistent reasoning-effort defaults ( #4530 ), multi-turn `/ask` ( #4538 ), better recent-session recovery after crashes ( #4539 ), session anchoring to WSL instead of Windows host ( #4543 ). Users want CLI state to behave like a real IDE workspace.
- **Richer Interactive Input** — Paste images into freeform question input ( #4544 ), `SHIFT+ENTER` line breaks ( #1481 ), queue editor with add-message and dequeue pause ( #4541 ). Terminal UX polish is a popular theme.
- **Configuration Persistence & Discovery** — `~/.copilot/skills/` personal skill discovery ( #4545 ), consistent workspace `.mcp.json` connectivity ( #4542 ), and persistent model/reasoning settings ( #4530 ).

---

## 6. Developer Pain Points

- **MCP Integration Reliability (dominant theme)** — False policy blocking, OAuth token bridging failures, late-connecting servers, child-process leaks, issuer mismatches — MCP support is still very rough around the edges.
- **Enterprise Policy & Governance Friction** — Managed settings enum validation failures blocking MCP servers (#4349), disabled models unavailable ( #4390 ), and non-interactive sessions bypassing `disableBypassPermissionsMode` ( #4528 ). Enterprise admins are hitting hard walls.
- **Sandbox Over-Restriction** — Breaking `git` usage ( #4524 ), blocking VS Code remote on WSL ( #4546 ), overly aggressive permission enforcement. Sandbox is crippling normal workflows.
- **Session State Fragmentation** — WSL host anchoring ( #4543 ), Remote-SSH empty transcripts ( #4529 ), local/cloud ID divergence ( #4539 ), and Ctrl+Z session loss — state management is inconsistent across environments.
- **Terminal Rendering/Stability** — Duplicate pending lines ( #4532 ), UI freezes on parallel subagents ( #4533 ), WebView2 renderer self-aborts ( #4492 ), and missing event consumption — interactive UIs feel fragile in high-load or multi-agent scenarios.

---

*Digest generated from 33 open/updated issues, 1 PR, and 1 release in the last 24h.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-08-21**

---

## 1. Today's Highlights
The community is actively exploring persistent memory capabilities for the CLI, with a new proposal (#2613) advocating for workspace-scoped long-term memory. Simultaneously, a complementary documentation PR (#2614) aims to clarify plugin security boundaries and credential handling, signaling a maturing focus on both feature extensibility and developer safety. While no new releases landed today, the issue and PR activity indicates a strong push toward formalizing plugin architecture and addressing user concerns around data persistence.

---

## 2. Releases
No new releases were published in the last 24 hours. Stay tuned for upcoming patches and feature updates.

---

## 3. Hot Issues
*Only one issue was updated in the last 24 hours.*

- **[#2613 [OPEN] [enhancement] Proposal: Kimi Memory Plus — workspace-scoped long-term memory plugin](https://github.com/MoonshotAI/kimi-cli/issues/2613)**  
  *Author: QIANLING-0831 | Created: 2026-08-20 | Comments: 0*  
  This feature request is the current focal point of community discussion. It proposes a plugin that gives the CLI persistent, project-aware memory. The author notes a critical compatibility gap: while the CLI supports registering explicit-memory tools as an stdio MCP server, it currently fails to recognize the experimental repository hooks needed for this to work seamlessly. This suggests users are hitting a hard ceiling when attempting to implement long-term context, a significant pain point for complex, multi-session workflows.

---

## 4. Key PR Progress
*Only one PR was updated in the last 24 hours.*

- **[#2614 [OPEN] docs(plugins): document security and persistent data](https://github.com/MoonshotAI/kimi-cli/pull/2614)**  
  *Author: QIANLING-0831 | Created: 2026-08-20*  
  This documentation PR is a direct response to community concerns about plugin reliability and safety. It clarifies that plugin tools run as local subprocesses with full user-level file and network access, explains credential handling for `inject` (including a warning against logging or committing injected values), and specifies that reinstalling a plugin replaces its installed directory. The PR also recommends separating persistent data from the installation directory—a crucial step for preventing data loss during updates. This lays the groundwork for safer plugin development and adoption.

---

## 5. Feature Request Trends
- **Persistent, Context-Aware Memory (Emerging):** The single new issue (#2613) highlights a strong desire for workspace-scoped memory—not just session-based chat history, but the ability to remember project decisions, user preferences, and technical context across sessions. The proposal explicitly asks for compatibility with existing MCP tooling, indicating a preference for standards-based integration over proprietary solutions.
- **Plugin Ecosystem Maturation (Implicit):** The documentation PR (#2614) suggests a broader trend: as the plugin ecosystem grows, users are demanding clear, formalized guidelines for security, data persistence, and update behavior to prevent breakage and credential leaks.

---

## 6. Developer Pain Points
- **Missing Long-Term Context:** The primary pain point expressed in #2613 is the inability to maintain long-term memory across different working sessions. Users need the CLI to "remember" project history and decisions, which is currently impossible due to a lack of recognized backend hooks for persistent storage.
- **Plugin Update Destructiveness:** The clarification in PR #2614—that reinstalling a plugin replaces its directory—points to a recurring developer fear: users may lose valuable configuration or cached data if they reinstall or update a plugin. The lack of explicit separation between code and user data is a source of potential frustration.
- **Security Ambiguity:** Developers are concerned about the security implications of plugins, particularly around credential injection (`inject`). The emphasis on warning against logging or committing injected values suggests users are worried about accidental secrets exposure in CI/CD pipelines and version history.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-21

## Today's Highlights
A new patch release (v1.18.19) shipped with Cloudflare AI Gateway passthroughs, closer Codex rate-limit alignment, and fixes for Qwen sampling defaults. The community is actively reporting TUI stability issues—multiple crash reports cite the "remove expects a renderable child object" error, and there's growing demand for multi-line prompt support in the TUI. On the performance front, a critical PR landed to eliminate per-update deep cloning of session parts, which directly addresses a major memory-leak issue.

## Releases
**v1.18.19** — Core improvements include native OpenAI and Anthropic passthroughs for Cloudflare AI Gateway models and closer alignment of Codex rate limits with ChatGPT subscription tiers. Bugfixes remove unsupported Qwen sampling defaults and address provider compatibility issues. ([Release](https://github.com/anomalyco/opencode/releases/tag/v1.18.19))

## Hot Issues
1. **[#30158 — Terminal button in web UI disappears](https://github.com/anomalyco/opencode/issues/30158)** (12 comments, 14 👍)
   Regression since v1.15.12; downgrading to v1.15.11 restores the icon. High visibility with significant community engagement, suggesting a long-standing UI regression that's still unresolved.

2. **[#27474 — TypeError: Failed to fetch](https://github.com/anomalyco/opencode/issues/27474)** (10 comments)
   Chinese-language report where Explore/Agent navigation intermittently triggers fetch errors. Affects core navigation flows and remains open after three months.

3. **[#7675 — Install script ignores OPENCODE_INSTALL_DIR](https://github.com/anomalyco/opencode/issues/7675)** (10 comments, 9 👍)
   Install script hardcodes `~/.opencode/bin`, ignoring documented env vars. Closed but still receiving comments—a recurring frustration for users needing custom install paths.

4. **[#27875 — Stuck at permission granting; Enter key broken](https://github.com/anomalyco/opencode/issues/27875)** (9 comments)
   Enter key fails to confirm permission prompts, trapping users in an endless loop of invalid tool calls. Critical for automation workflows.

5. **[#43619 — [2.0] subagent: sessionID required prevents spawning first child](https://github.com/anomalyco/opencode/issues/43619)** (9 comments)
   Schema/documentation mismatch blocks first-child agent creation in v2.0—a blocker for all delegation workflows.

6. **[#20458 — Mouse escape sequences garbled after TUI exit](https://github.com/anomalyco/opencode/issues/20458)** (8 comments, 5 👍)
   Terminal corruption after exiting the TUI. Long-standing issue (since April) with no fix yet.

7. **[#35107 — Memory keeps growing until process killed](https://github.com/anomalyco/opencode/issues/35107)** (4 comments)
   Deep profiling reveals `structuredClone` on every part update causes 488KB text parts to accumulate; 93K updates over 200 sessions creates massive heap pressure.

8. **[#42657 — TUI lag with multi-subagent sessions](https://github.com/anomalyco/opencode/issues/42657)** (3 comments)
   97% CPU on render thread with 2-4 concurrent subagents; typing delays of 1-3 seconds across all terminals.

9. **[#43054 — Models other than hy3-free / deepseek flash fail with Forbidden](https://github.com/anomalyco/opencode/issues/43054)** (4 comments, 2 👍)
   All models except two free tiers fail with `Forbidden: {"model":"big-pickle"}`. Recently reported, high-impact for providers.

10. **[#40086 — Feature: Persistent ui.sidebar.enabled config](https://github.com/anomalyco/opencode/issues/40086)** (3 comments)
    Context sidebar reappears after restart; users request persistent config to disable it.

## Key PR Progress
1. **[#43733 — fix(core): avoid deep cloning session parts](https://github.com/anomalyco/opencode/pull/43733)**
   Closes #35107. Eliminates per-update `structuredClone` on session parts—direct fix for the reported memory-leak root cause.

2. **[#43650 — fix(core): prevent shell eviction loop](https://github.com/anomalyco/opencode/pull/43650)**
   Prevents infinite retention-eviction loops on removed running shells.

3. **[#43715 — fix(opencode): preserve Cerebras completion limit](https://github.com/anomalyco/opencode/pull/43715)**
   Cerebras rejects requests with both `max_tokens` and `max_completion_tokens`; this preserves native Cerebras limits.

4. **[#43736 — [contributor] fix(opencode): preserve Cerebras completion limit](https://github.com/anomalyco/opencode/pull/43736)**
   Automated contributor's approach, adding a built-in Cerebras plugin under `packages/opencode` with auto-loading.

5. **[#43677 — [contributor] fix(core): send console anthropic api key header](https://github.com/anomalyco/opencode/pull/43677)**
   Translates OpenCode Console Bearer credentials to `x-api-key` for Anthropic Messages—fixes a cross-provider auth gap.

6. **[#43675 — [contributor] fix(opencode): answer subagent permissions in run](https://github.com/anomalyco/opencode/pull/43675)**
   Auto-approve/reject permission requests in non-interactive run sessions with proper session-tree scoping.

7. **[#43735 — [contributor] fix(client): authenticate PTY websocket connections](https://github.com/anomalyco/opencode/pull/43735)**
   Adds authenticated, single-use tickets for PTY WebSocket connections; removes unauthenticated raw-fetch path in desktop terminal.

8. **[#43681 — fix(core): resolve Bedrock AWS profile credentials for V2](https://github.com/anomalyco/opencode/pull/43681)**
   Community contribution from Amazon One Medical; resolves AWS profile credentials for Bedrock in V2.

9. **[#43734 — [contributor] fix(tui): scope prompt history by session](https://github.com/anomalyco/opencode/pull/43734)**
   Persists session ID per prompt; independent history cursors per tab; migrates legacy unscoped entries.

10. **[#43637 — refactor(app): establish session vertical slice](https://github.com/anomalyco/opencode/pull/43637)**
    Reduces 2,005-line `pages/session.tsx` into a structured vertical slice—significant architectural cleanup.

## Feature Request Trends
- **Persistent UI configuration**: Multiple requests for persistent settings (sidebar visibility, TUI layout) via `opencode.json`.
- **Multi-line prompt support**: Shift+Enter submitting is reported as a bug, but the underlying desire is proper multi-line input in the TUI.
- **Plugin API expansion**: New PRs exposing `session.switchAgent` / `session.switchModel` to Effect and Promise plugins signal a broader effort to make plugin capabilities more powerful and composable.
- **Per-MCP-server trust configuration**: Fingerprint pinning for self-signed certs (PR #40125) addresses a long-standing security/config flexibility gap.
- **Custom install locations**: Persistent requests for install scripts to respect open-standard env vars (`OPENCODE_INSTALL_DIR`, `XDG_BIN_DIR`).

## Developer Pain Points
- **TUI crashes and rendering instability**: Multiple reports of "remove expects a renderable child object" crashes (#43696, #43693, #43699) and the disappearing terminal button (#30158) show the TUI remains a fragile area.
- **Memory leaks at scale**: Both session-part cloning (#35107) and EventTarget listener leaks in `opencode web` (#34574) are driving severe memory growth in long-running deployments.
- **Provider auth and compatibility friction**: Reports of Forbidden errors for non-default models (#43054), Anthropic header issues (#43677), and Bedrock credential resolution (#43681) indicate cross-provider compatibility is a common pain point.
- **Permission flow UX**: Enter-key failures (#27875) and subagent permission handling (#43619) create deadlocks that block automation.
- **High CPU usage in multi-agent sessions**: Concurrent subagents cause render-thread saturation (#42657, #41078), making the UI unusable during heavy workloads.
- **Installation and configuration surprises**: Ignored env vars (#7675) and undocumented config paths continue to frustrate power users.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-21

## Today's Highlights

No new releases shipped in the past 24 hours, but the project saw active PR momentum with 16 pull requests touched. The most pressing community issue remains a critical auto-compaction bug (#6879) that has attracted substantial upvotes and discussion, while several quality-of-life UX improvements (command aliases, cursor handling, copy behavior) are moving through the PR pipeline. A significant TUI theming refactor from Armin Ronacher (#8398) is currently open for review.

## Releases

No new versions released in the last 24 hours.

## Hot Issues

1. **Auto-compaction never triggers until provider overflow** ([#6879](https://github.com/earendil-works/pi/issues/6879)) — Critical bug where sessions on gpt-5.6-sol exceed the context window threshold without triggering compaction, only stopping when the API rejects requests at 373k tokens. 17 upvotes and 18 comments; community is calling for compaction checks after every agentic turn.

2. **Windows usage and issue collection** ([#7547](https://github.com/earendil-works/pi/issues/7547)) — A meta-issue cataloging the various ways Pi runs on Windows and where the core team should focus energy. 36 comments from developers reporting Windows-specific pain points; effectively acting as a community knowledge base.

3. **Terminal scrolls to beginning without reason** ([#5023](https://github.com/earendil-works/pi/issues/5023)) — Random jumping to session start while the model is working. 17 comments and significant traction; closed but referenced by other issues. Likely related to terminal rendering race conditions.

4. **Windows: input redrawn on every keystroke** ([#6300](https://github.com/earendil-works/pi/issues/6300)) — Each character appears on a new line in cmd.exe and Windows Terminal on Windows 10 Pro 22H2. Developers on Windows hit this immediately; likely related to console input handling and VTE detection.

5. **Gemini 3.x fails during tool use due to missing `thought_signature`** ([#6996](https://github.com/earendil-works/pi/issues/6996)) — Gemini 3.5-flash and 3.6-flash submitters see hard failures when tool results are sent back without `thought_signature` in history. Blocks Gemini 3.x adoption for agentic workflows.

6. **Per-model compaction settings** ([#8133](https://github.com/earendil-works/pi/issues/8133)) — Request to allow compaction profiles per model instead of global settings. 3 upvotes; addresses different model context behaviors — a practical scaling need for teams using mixed model fleets.

7. **Migrate grok-mermaid → lovely-mermaid** ([#8157](https://github.com/earendil-works/pi/issues/8157)) — The community model of mermaid renderer consolidation; 7 comments with discussion about inheriting corner cases from the original port. Interesting because it reflects how community-driven forks eventually get upstreamed.

8. **Unknown slash commands silently sent to the model** ([#8081](https://github.com/earendil-works/pi/issues/8081)) — Typing `/exit` (muscle memory from Claude Code/Codex/opencode) costs tokens and lands in the transcript. Warning would prevent wasted model calls.

9. **Scoped Anthropic API keys need necessary request params** ([#6093](https://github.com/earendil-works/pi/issues/6093)) — Claude Code scoped keys (sk-ant-api03-...) need extra headers; Pi decides by prefix and misclassifies them. Closed but highlight of commonly-hit integration friction.

10. **Per-tool output expansion in the fullscreen TUI** ([#8344](https://github.com/earendil-works/pi/issues/8344)) — Proposal for mouse-driven expansion and collapse of individual tool output blocks, keeping `Ctrl+O` as the global toggle. Nice ergonomics improvement; closed with discussion.

## Key PR Progress

1. **[#8398](https://github.com/earendil-works/pi/pull/8398) — feat: add color values and theme styling** (OPEN) — Major TUI and theme refactor by mitsuhiko that exposes colors directly. Backwards-compatible; enables both adventurous style work and non-terminal UIs down the line. Big architectural addition, worth watching.

2. **[#8118](https://github.com/earendil-works/pi/pull/8118) — feat(ai): add requiresNonNullAssistantContent compat flag** (OPEN) — Fixes OpenAI-compatible gateways that reject replayed tool-call-only assistant messages (content: null) by allowing `""` instead. Solves a hard interop problem for gateway-heavy deployments.

3. **[#8302](https://github.com/earendil-works/pi/pull/8302) — feat(ai): amazon bedrock mantle** (OPEN) — Adds Amazon's Mantle API surface that hosts openai.gpt-5.x models; currently routed via Converse, which fails with validation errors. WIP waiting on e2e API keys — addresses #5363.

4. **[#8405](https://github.com/earendil-works/pi/pull/8405) — Normalize kimi-coding thinking signatures to base64url** (CLOSED) — Fixes malformed encrypted reasoning content errors on second+ turns; signature observed as invalid base64url. Hard interop bug for kimi-coding.

5. **[#8407](https://github.com/earendil-works/pi/pull/8407) — fix(tui): preserve logical lines when copying soft-wrapped text** (CLOSED) — Copying mouse selections joins visual rows; converts soft wraps into hard newlines in the clipboard — breaks URLs and paragraphs. Preserves logical boundaries.

6. **[#8395](https://github.com/earendil-works/pi/pull/8395) — fix(coding-agent): prevent TUI crash on large diffs** (CLOSED) — The `lines.push(...contentLines)` spread hits V8's max call stack size for ~14.5MB diffs; fixes the crash during tool rendering. Fixes #8036.

7. **[#8416](https://github.com/earendil-works/pi/pull/8416) — fix: hold triggerTurn-false custom messages until the tool batch ends** (CLOSED) — Custom messages sent mid-stream could land between assistant toolCall and toolResult, breaking strict providers. Hold messages until the batch ends.

8. **[#8383](https://github.com/earendil-works/pi/pull/8383) — fix(ai): send LOW to disable thinking on gemini-3.7-flash** (OPEN) — Gemini 3.7-flash rejects `thinkingLevel: MINIMAL` with 400 INVALID_ARGUMENT; switches to LOW. Prevents every call failing when disabled.

9. **[#8399](https://github.com/earendil-works/pi/pull/8399) — feat(settings-selector): show & make default searchable** (CLOSED) — Adds a default label in `/model` and `/thinking` and makes "default" searchable — aligns with `Ctrl+S` hotkey persist behavior.

10. **[#5268](https://github.com/earendil-works/pi/pull/5268) — fix(tui): render the hardware cursor by default so the prompt cursor hollows on blur** (CLOSED) — Fixes #3896: the prompt cursor stays a filled block when the terminal loses focus; hardware cursor lets the prompt hollow. Long-lived PR that finally landed.

## Feature Request Trends

The most persistent pattern across issues is **friction with cross-tool muscle memory**: `/exit`, `/quit`, and `/bye` aliases appeared in at least six separate issues (#5340, #4538, #5863, #6193, #5161). Commands from Claude Code, Codex, and opencode that are missing in Pi cost users tokens and trip them up daily. The community signal is unambiguous — implement aliases wholesale.

A second emerging direction is **per-model and per-session configuration granularity**: per-model compaction settings (#8133) and forked-session cache reuse (#8348) both point toward wanting more flexible behavior based on which model is active. Users want i different budget and caching behavior for different model families.

Third, there's a cluster of **Windows-focused TUI polish** (#7547, #6300, #6995), with the meta-issue (#7547) essentially aggregating dozens of Windows-specific reports. Expect increasing pressure on Windows-first fixes as the community grows there.

Finally, **lifecycle-aware behavior** is gaining momentum: OSC 133 busy markers should follow the agent lifecycle, not re-emit on transcript redraws (#8415), and `agent_settled` handlers should get session-control context (#8390).

## Developer Pain Points

**Context window and token management** is the top recurring frustration. Issue #6879 (auto-compaction never triggering) received the most upvotes in the last 24 hours, and the broader class of compaction, retry, and cache issues (#8133, #8348, #6879) keeps appearing. Users are hitting hard limits in high-token agentic turns.

**Unknown slash commands silently sent to the model** (#8081) is a direct token-wasting footgun that also pollutes transcripts. Combined with the "wasted 10 tokens" comments across the /exit aliases issues, token pain is pervasive.

**Windows terminal behavior remains a dominant frustration** across rendering (#6300), scrolling (#5023), and image layering (#6995) issues. The meta-issue (#7547) with 36 comments suggests the Windows story is far from solved.

**Keyboard, mouse, and clipboard fidelity issues** recur in the TUI (#8407, #8344, #8414) — copying selections breaking line semantics, focus events not driving cursor behavior, and a general desire for more discoverable interactions contribute to a sense that the TUI doesn't yet match terminal accessibility expectations.

Finally, **async and lifecycle correctness** problems appear across issues like #8396 (auto-retry leaves superseded errors in the persisted session), #8415 (OSC 133 markers re-emitted on every redraw), and #8390 (settled-safe session control) — a signal that agent-finalization and re-rendering paths need more careful state management.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-21

## Today's Highlights

The Qwen Code team shipped v0.21.15 with notable Web Shell improvements, including file attachment insertion via composer or @ selection and enhanced streaming performance. A significant cluster of `/review` pipeline hardening work continues across multiple PRs, addressing convergence advisories, Aone Code integration gaps, and security-focused audit concerns. Several critical bug fixes landed for session management, including duplicate provider tool-call handling and proper rewind projection classification.

## Releases

**[v0.21.15](https://github.com/QwenLM/qwen-code/releases)** — Latest stable release with Web Shell enhancements:
- File attachments can now be inserted via composer or @ selection
- Improved streaming performance for Web Shell interactions
- Immediate sidebar synchronization when attaching files
- Related PRs: [#9405](https://github.com/QwenLM/qwen-code/pull/9405), [#9477](https://github.com/QwenLM/qwen-code/pull/9477)

**[v0.21.11-nightly.20260820.b414f135fa](https://github.com/QwenLM/qwen-code/releases)** — Nightly build with Web Shell approval/ask-user dialogs refactored as in-flow sheets, fixing background-agent false failures.

## Hot Issues

1. **[#9278 — /review publish-time convergence advisory design](https://github.com/QwenLM/qwen-code/issues/9278)** — Open design tracking for addressing runaway review loops where fixes introduce new defects, creating ever-growing diffs. The proposal includes telemetry, diagnosis, and operator-controlled posting surfaces. Active discussion with 8 comments.

2. **[#8382 — Duplicate provider tool call id](https://github.com/QwenLM/qwen-code/issues/8382)** — Persistent error where tool calls fail with "Duplicate provider tool call id" and "not recorded" errors. Related fix #9586 closed, but this remains open awaiting retesting.

3. **[#8724 — Cross-session messaging](https://github.com/QwenLM/qwen-code/issues/8724)** — Feature request for Qwen Code sessions on the same machine to discover and message each other, with fail-closed gates on the receiving side. 7 comments showing community interest in multi-agent workflows.

4. **[#9309 — Incorrect compression behavior](https://github.com/QwenLM/qwen-code/issues/9309)** — `/compress-fast` followed by `/compress` produces anomalous context reduction (170k to 7k tokens), suggesting a possible over-compression bug. 6 comments.

5. **[#2128 — Unbounded memory growth in long sessions](https://github.com/QwenLM/qwen-code/issues/2128)** — Long-running sessions (dozens of hours) see continuous memory growth due to unbounded UI History array. P1 priority with root cause identified in code analysis.

6. **[#9556 — Review pipeline code execution security question](https://github.com/QwenLM/qwen-code/issues/9556)** — Security discussion on whether `/review` should keep granting code execution as the invoking user. Raised after 20 review rounds on #9221.

7. **[#9573 — Resumed sessions show false "Tool result missing" errors](https://github.com/QwenLM/qwen-code/issues/9573)** — Resumed sessions display placeholder errors for tool calls that completed normally, confusing users about session state.

8. **[#9485 — Web Shell clipboard failure over HTTP](https://github.com/QwenLM/qwen-code/issues/9485)** — All copy buttons fail with "Clipboard API is not available" when using non-localhost HTTP addresses. Common remote server setup affected.

9. **[#9597 — Hierarchical memory loads QWEN.md twice](https://github.com/QwenLM/qwen-code/issues/9597)** — Symlink aliases cause duplicate memory file loading, potentially causing context bloat and conflicting directives.

10. **[#9571 — Confirmation boxes steal focus while typing](https://github.com/QwenLM/qwen-code/issues/9571)** — UI bug where model confirmation boxes are selected by default, interrupting user input. Sibling issue #9611 tracks the same problem for AskUserQuestion.

## Key PR Progress

1. **[#9526 — Persistent-critical convergence advisory](https://github.com/QwenLM/qwen-code/pull/9526)** — Adds a convergence-exit advisory to review compose step, detecting when the review loop is stuck on Criticals across rounds with persistent two-round posting volume.

2. **[#9604 — Clear deferred Round-5 findings from Aone write path](https://github.com/QwenLM/qwen-code/pull/9604)** — Full cleanup of 29 suggestions the review bot raised on the Aone `--comment` posting path, implementing all deferred items.

3. **[#9607 — Demote balanced inline thinking blocks](https://github.com/QwenLM/qwen-code/pull/9607)** — Fixes OpenAI-compatible endpoint handling where hybrid-thinking models emit a second balanced `<think>` block in content, which previously caused turn failures.

4. **[#9609 — Don't steal approval focus while typing](https://github.com/QwenLM/qwen-code/pull/9609)** — Tool-approval dialog yields keyboard focus when active element is editable, preventing interruption of user typing.

5. **[#9590 — Provider-aware reasoning controls](https://github.com/QwenLM/qwen-code/pull/9590)** — Adds provider- and endpoint-aware WebShell reasoning controls for DeepSeek V4, GLM 5.2, and Kimi models, with matching documented routes.

6. **[#9466 — Anchor rewind mapping to stable prompt identity](https://github.com/QwenLM/qwen-code/pull/9466)** — Makes prompt identity the authoritative link between user turns, model history, sessions, ACP rewind, and bounded fork history.

7. **[#9527 — Bind sandbox image to pulled digest](https://github.com/QwenLM/qwen-code/pull/9527)** — Security hardening that binds exported sandbox images to the digest from the pull record, fixing two criticals from review.

8. **[#9273 — capture-tui: rendering evidence for review claims](https://github.com/QwenLM/qwen-code/pull/9273)** — Adds `qwen review capture-tui` to drive commands in private tmux servers, capturing pane text and rendering PNG evidence instead of prose arguments.

9. **[#9577 — Disable install scripts in release CI](https://github.com/QwenLM/qwen-code/pull/9577)** — Security hardening for npm release workflow: disables lifecycle scripts during installation, then explicitly runs repository-owned postinstall steps; avoids persisting write-capable PATs.

10. **[#8368 — Kimi and Xiaomi MiMo providers](https://github.com/QwenLM/qwen-code/pull/8368)** — Adds first-class preset support for Kimi (Coding Plan, API Key China/International) and Xiaomi MiMo (pay-as-you-go plus regional options) to `/auth`.

## Feature Request Trends

- **Aone Code Integration Expansion (6+ issues)**: Cross-round comment dedup, self-PR detection, incremental cache for AGit-Flow, inline anchoring for removed lines, cleanup bypass audit, AI comment merge gate, and residual small gaps — all tracked in issues #9613–#9619.

- **Multi-session/Agent Communication**: Interest in letting sessions discover and message each other (#8724), suggesting growing demand for multi-agent workflows.

- **Provider Diversity**: Continued expansion of third-party provider support (Kimi, Xiaomi MiMo in #8368; provider-aware reasoning controls in #9590).

- **Session Lifetime Management**: Bounded session rotation per channel (#8927) and manual session name persistence (#9260) show focus on session lifecycle control.

## Developer Pain Points

- **Session State Reliability**: Resumed sessions showing phantom errors (#9573) and duplicate tool-call IDs (#8382) erode trust in session persistence.

- **Context/Memory Management**: Unbounded memory growth (#2128), hierarchical memory double-loading (#9597), and compression anomalies (#9309) are recurring concerns for long sessions.

- **UI Focus Interruption**: Confirmation boxes and approval dialogs stealing focus during typing (#9571, #9611) disrupt workflow flow.

- **Review Pipeline Stability**: The `/review` command generates significant discussion around loop convergence (#9278), code execution security (#9556), and cleanup audits — suggesting the automated review system is powerful but requires careful guardrails.

- **Web Shell Connectivity**: Remote HTTP deployments face clipboard API limitations (#9485), while slow session pinning (#9465) and excessive catalog refreshes (#9562) degrade the Web Shell experience.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-21

## 1. Today's Highlights

CodeWhale (formerly DeepSeek-TUI) shipped **v0.9.10** — the "retention, identity, first-run, and release-hardening" train (76 commits) — while the community converged on a major architectural push: **EPIC-005 crate decomposition** with a flurry of refactoring PRs extracting turn-loop, stream-processing, and tool-call stages. The i18n dictionary spine work (removing `isZh` branches) advanced steadily across multiple docs pages, and a notable bug surfaced where the header status indicator has been broken since v0.9.7.

## 2. Releases

**v0.9.10** — "Codewhale" is now the official product name. The legacy `deepseek-tui` npm package is **deprecated** (no further releases). Key themes: retention, identity, first-run UX, and release hardening. PR #5513 describes the full 76-commit release lane. The `codewhale` command, npm package, and release-asset names remain lowercase technical identifiers.

## 3. Hot Issues

1. **[#5518 — Emergency compaction at ~85K–105K tokens on DeepSeek V4 despite 327K context**](https://github.com/Hmbown/CodeWhale/issues/5518) *(CLOSED)* — vLLM-hosted DeepSeek-V4-Flash sessions hit early compaction despite `auto_compact = false`. Suspected excessive output-headroom budgeting and handoff state contamination. Closed quickly, suggesting a fix landed.

2. **[#5522 — First run too front-loaded**](https://github.com/Hmbown/CodeWhale/issues/5522) *(OPEN, 0 comments)* — Direct feedback: first launch burdens users with telemetry disclosure + wall of settings before useful work. Non-English users feel the "psychological cost" most. Acceptance criteria demand progressive onboarding.

3. **[#5316 — EPIC-005: Crate Decomposition Umbrella**](https://github.com/Hmbown/CodeWhale/issues/5316) *(OPEN, 10 comments)* — The umbrella EPIC tracking the major TUI crate decomposition. All sub-EPICs and FEATs report here; nearly every PR this week traces back to it.

4. **[#5526 — Shell completion is deprecated/outdated**](https://github.com/Hmbown/CodeWhale/issues/5526) *(OPEN)* — `codew completions powershell` produces scripts that still trigger `codewhale-tui` instead of `codew`. No docs or config path found — completion is effectively stale.

5. **[#5516 — HTTP 400 max_tokens=384000 after v0.9.9 upgrade**](https://github.com/Hmbown/CodeWhale/issues/5516) *(CLOSED)* — Every request failed after upgrade with `max_tokens` exceeding `max_model_len=262144`. User never configured this. Regression from release changes; closed with 1 comment.

6. **[#5512 — Header status indicator never renders since 0.9.7**](https://github.com/Hmbown/CodeWhale/issues/5512) *(CLOSED)* — `status_indicator` setting (cw/whale/dots) broken on Windows 11. Worked in 0.8.64 era. A visible regression spanning multiple releases.

7. **[#5442 — Discoverability debt: advanced commands hidden at palette root**](https://github.com/Hmbown/CodeWhale/issues/5442) *(CLOSED)* — ~34 high-value commands demoted from discovery root; capability upgrades are "shipped-but-invisible." Community signals the TUI has depth but users can't find it.

8. **[#5345 — Multi-line input mode or custom "send" shortcut**](https://github.com/Hmbown/CodeWhale/issues/5345) *(CLOSED)* — Users compare against Grok Build/Codex which support `multi-line` mode. Most inputs are multi-line Markdown; current single-line send is friction.

9. **[#5508 — Continuous loop / infinite turn option**](https://github.com/Hmbown/CodeWhale/issues/5508) *(CLOSED)* — AI-as-coordinator use case needs an infinite-turn mode where the model keeps running until interrupted, rather than one-shot turns.

10. **[#998 — Text display truncation (zh)**](https://github.com/Hmbown/CodeWhale/issues/998) *(CLOSED)* — Chinese users want hover tooltips for truncated content. Representative of broader CJK/render fidelity concerns.

## 4. Key PR Progress

1. **[#5524 — Multi-file `read_lints` operation (OPEN)**](https://github.com/Hmbown/CodeWhale/pull/5524) — Implements #4070: model-visible `lsp` tool gains `read_lints` for multiple existing files, reusing the `LspManager` transport pool instead of spawning new servers.

2. **[#5525 — FEAT-018: utility command group shapes (OPEN)**](https://github.com/Hmbown/CodeWhale/pull/5525) — Converts all 7 TUI utility commands (`/about`, etc.) to external command shapes from FEAT-014/015. Commands stay in `codewhale-tui` but change execution boundary.

3. **[#5523 — Extract tool call stages from turn loop (OPEN)**](https://github.com/Hmbown/CodeWhale/pull/5523) — Pure refactor: `plan_tool_calls`, `execute_planned_tools`, `process_tool_results` extracted. Preserves control order, cancellation, and indexed outcomes.

4. **[#5520 — docs/sandbox + docs/web on dictionary spine (CLOSED)**](https://github.com/Hmbown/CodeWhale/pull/5520) — 14 + 15 `isZh` branches eliminated to zero. `check-locales.mjs` `OPTIONAL_FILES` extended for key/token parity enforcement.

5. **[#5521 — Drop single-argument concat! (CLOSED)**](https://github.com/Hmbown/CodeWhale/pull/5521) — Trivial lint fix (`clippy::useless-concat`) blocking CI on `main`. Quick hygiene, keeps release train moving.

6. **[#5515 — Forward MCP image results as typed content (CLOSED)**](https://github.com/Hmbown/CodeWhale/pull/5515) — Standard MCP `image` content now becomes provider-neutral rich tool-result blocks. Inline base64 removed from text receipt while preserving `structuredContent`/`isError`; reuses 5 MiB/one-image validation.

7. **[#5513 — v0.9.10 release train (CLOSED)**](https://github.com/Hmbown/CodeWhale/pull/5513) — Retention, identity, first-run, and release-hardening. 76 commits rebased over community-accepted changes. Carries fixes for the parallel-load and config-fixture flakes.

8. **[#5509 — Restore /title as independent terminal window title (CLOSED)**](https://github.com/Hmbown/CodeWhale/pull/5509) — Fixes #5430: `/title` and `/rename` had been wrongly merged; `/title` now restores the standalone terminal-window-title behavior.

9. **[#5514 — Extract stream processing from turn loop (CLOSED)**](https://github.com/Hmbown/CodeWhale/pull/5514) — Companion to #5523: response-stream state machine moved into `process_stream`, returning `StreamOutcome`. Timing and retry semantics preserved.

10. **[#5517 — docs/constitution + docs/runtime-api on dictionary spine (CLOSED)**](https://github.com/Hmbown/CodeWhale/pull/5517) — Phase 2 of #5337: 14 `isZh` branches each, now zero. Same pattern as #5504; zh held to key/token parity while other locales stay free-form.

## 5. Feature Request Trends

- **Crate decomposition / architecture refactor (EPIC-005)** — The dominant effort: turning the monolithic TUI crate into modular command shapes, extracting turn-loop stages, and decomposing execution boundaries. The community is systematically paying down complexity.
- **i18n completion (dictionary spine)** — Relentless progress eliminating `isZh` branches page-by-page, with parity checks for zh while other locales remain flexible. Strong Chinese-speaking contributor base.
- **Multi-line input / custom send keys** — Repeated requests (Grok Build / Codex parity) for multi-line mode and remappable send shortcuts.
- **On-demand diagnostics (`read_lints`)** — Model should be able to read lints for files it *hasn't* just edited, not just post-edit.
- **Continuous / infinite turn mode** — For AI-coordinator patterns where one-shot turns are insufficient.
- **First-run progressive onboarding** — Reduce cognitive load on launch; surface settings gradually instead of all at once.

## 6. Developer Pain Points

- **Silent regressions** — The header status indicator (#5512) and `max_tokens` over-provisioning (#5516) both shipped unnoticed across releases, suggesting weak release-gate regression coverage.
- **Name/identity churn** — `deepseek-tui` → `CodeWhale` / `codew` / `codewhale-tui` leaves completion scripts, docs, and user muscle memory stale (#5526).
- **Configuration surprise** — Users report HTTP 400 errors from config they never set (#5516); compaction fires despite explicit `auto_compact = false` (#5518). "It works until it doesn't" at scale.
- **CJK / locale rendering** — Truncated text without hover (#998), IME candidate window instability (#5023) — Windows/Chinese input paths remain a fragile area.
- **First-run friction** — English telemetry disclosure + wall of settings before any useful work pushes away non-English users (#5522). The product's depth is hidden behind setup cost.
- **Parallel-load flakes** — Known issues carried from v0.9.7 close-out (#5355) around `exec_persistent_service` and `exact_turn_snapshot` — nondeterministic test failures erode trust in CI.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*