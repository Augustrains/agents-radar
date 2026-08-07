# AI CLI Tools Community Digest 2026-08-07

> Generated: 2026-08-07 01:58 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date:** 2026-08-07

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem is experiencing rapid maturation with **security and reliability** emerging as the dominant cross-cutting concerns. All major tools are shipping weekly releases with active bug-fix cycles, while communities demonstrate high sensitivity to regressions—particularly on Windows platforms. The competitive landscape shows **convergence on core features** (MCP integration, permission systems, session management) while tools differentiate through specialized strengths (Claude Code's plugin ecosystem, Codex's cloud integration, Gemini CLI's subagent architecture). The most pressing shared challenges include Windows stability, permission system friction for automation workflows, session/context management reliability, and growing demands for context-window transparency. This is a market transitioning from feature-race to reliability-and-trust phase.

---

## 2. Activity Comparison

| Tool | Issues (24h) | PRs (24h) | Releases (24h) | Notable Release | Community Engagement |
|------|-------------|-----------|----------------|-----------------|---------------------|
| **Claude Code** | 50 | 5 | 0 | — (stable period) | High; 10 hot issues, 2 with 30+👍 |
| **OpenAI Codex** | ~10 tracked | 10 | 1 | rust-v0.147.0 (Agent Plugins) | Very high; 3 issues with 20-30+ comments |
| **Gemini CLI** | ~10 tracked | 11 | 0 | v0.54.2 (prior) | High; 2 P1 bugs, active PR review |
| **GitHub Copilot CLI** | ~12 tracked | 0 | 1 | v1.0.79-6 (stability fixes) | Moderate; stable issue flow |
| **Kimi Code CLI** | 8 tracked | 2 | 0 | — | Moderate; 2 competing PRs for 1 bug |
| **OpenCode** | ~10 tracked | 10 | 0 | — (v1.18.14 referenced) | High; 401 outage dominates (10+ dupes) |
| **Pi** | ~10 tracked | 31 | 1 | v0.84.0 (Fullscreen TUI) | High; 31 PRs/day, active iteration |
| **Qwen Code** | ~10 tracked | 10 | 3 | v0.21.7 (Goal turn-limit removal) | Moderate-high; 150-comment OAuth thread |
| **DeepSeek TUI** | ~10 tracked | 10 | 0 | — (v0.9.4 train pending) | Moderate; 77-commit release train |

---

## 3. Shared Feature Directions

### 3.1 Cross-Tool Requirements Matrix

| Feature Need | Tools | Specific Requirements |
|---|---|---|
| **Context/Session Transparency** | OpenCode, Pi, DeepSeek, Claude Code | Token-by-token context breakdown (#6152 OpenCode, 129👍), compaction trigger visibility (#6879 Pi), fallback disclosure for unknown models (#5244 DeepSeek), session limit accuracy (#54750 Claude) |
| **MCP Lifecycle Management** | Codex, Kimi, OpenCode, Copilot | Lazy schema loading (#2147 Kimi), project-scoped process pools (#20883 Codex), orphan process cleanup (#4392 Copilot), server recovery after reauth (#37337 Codex) |
| **Permission System Rethink** | Claude Code, Copilot, Qwen, OpenCode | Compound-command allowlist bypass (#76718 Claude), sticky auto-mode after toggle (#4388/4389 Copilot), classifier bypass via line continuation (#8582 Qwen), path-matching failures for deny rules (#40945 OpenCode) |
| **Windows First-Class Support** | Claude Code, Codex, Qwen, Pi | ECONNRESET streaming (#84194 Claude), process leaks (#33776 Codex), startup EISDIR crash (#8615 Qwen), terminal rendering fixes across tools |
| **System Notifications** | Claude Code, Qwen, OpenCode | OS-level attention alerts (#26581 Claude, 32👍), multi-session ambient awareness |
| **BYOM/Provider Flexibility** | Copilot, Codex, Gemini, Pi, DeepSeek | In-session model switching (#4376 Copilot), per-provider API keys (#5250 DeepSeek), Ollama Cloud support (#7742 Pi), model list accuracy (#7674 Pi) |
| **Subagent/Worker Reliability** | Gemini, Codex, Claude, DeepSeek | MAX_TURNS false-success (#22323 Gemini), quota accounting for subagents (#35463 Codex), checkpoint resume (#5242 DeepSeek), context-window lineage for forks (#37347 Codex) |
| **File Edit Safety** | Kimi, OpenCode, Claude | Byte-preservation for non-UTF-8 (#2591 Kimi, 2 PRs submitted), lexical path resolution (#40962 OpenCode), symlink handling |

---

## 4. Differentiation Analysis

### 4.1 Feature Focus by Tool

| Tool | Primary Focus | Target User | Key Differentiator |
|---|---|---|---|
| **Claude Code** | Plugin ecosystem, hooks, enterprise workflows | Professional developers in Anthropic ecosystem | Deepest plugin/hook architecture; permission granularity; Cowork/cloud sessions |
| **OpenAI Codex** | Desktop/TUI hybrid, remote delegation, MCP-rich | Power users of OpenAI ecosystem | Agent Plugins (portable catalogs); sandbox hardening; desktop app maturity |
| **Gemini CLI** | Subagent delegation, skills system, evals | Developers on Google AI stack | Advanced subagent architecture; behavioral test infrastructure (76 evals); auto-memory experiments |
| **GitHub Copilot CLI** | GitHub-native workflows, BYOM providers | GitHub-centric enterprise devs | .agents standardization; ACP protocol; tight GitHub integration (Actions, models) |
| **Kimi Code CLI** | Lightweight personal assistant, VSCode extension | Individual developers, Chinese market | Simple UX; VSCode extension primary surface; bilingual community |
| **OpenCode** | Open-source flexibility, subscription plans (Go/Zen) | OSS enthusiasts, cost-sensitive users | Transparent BYOK; community-owned roadmap; aggressive TUI feature shipping |
| **Pi** | TUI-first experience, harness architecture | Terminal purists, long-session workers | Fullscreen TUI (v0.84.0); harness v2 for resumable agents; SQLite-optimized sessions |
| **Qwen Code** | Alibaba ecosystem, multimodal ambitions | Asian market, QA teams | Live Host CI; voice/audio frontend; channel integrations (DingTalk/Feishu) |
| **DeepSeek TUI** | Workflow orchestration, ACP bridging | Advanced users, fleet deployments | ACP tool execution (#5225); dynamic workflow engine; MCP Registry discovery |

### 4.2 Technical Approach Differences

- **Sandboxing:** Codex emphasizes Bubblewrap hardening (#37349, #37350); Qwen uses classifier-based read-only detection; Claude Code uses permission rules+allowlists; Gemini has minimal sandbox but strong subagent isolation.
- **Architecture:** Pi and DeepSeek both pursue "Harness" architectures for resumable agent state; Codex uses fork-based subagents with context-window lineage; Gemini pushes decentralized subagent patterns.
- **Provider Strategy:** Copilot and OpenCode support broad BYOM; Claude Code and Codex are ecosystem-centric (Anthropic/OpenAI); Gemini and Qwen are cloud-native (Google/Alibaba).
- **Terminal vs Desktop:** Pi and DeepSeek are TUI-first; Codex and Claude Code push desktop apps; Kimi and Qwen treat VSCode extensions as primary; Copilot is CLI-first with ACP for bridges.

---

## 5. Community Momentum & Maturity

### 5.1 Momentum Ranking (by activity, PR velocity, engagement)

| Tier | Tools | Rationale |
|---|---|---|
| **Rapid Iteration** | **Pi** (31 PRs/day), **Gemini CLI** (11 PRs+11 issues), **Codex** (10 PRs+1 release) | Highest PR throughput; feature releases landing weekly; community feedback loop is tight |
| **Steady Maturity** | **Claude Code**, **Qwen Code**, **OpenCode**, **DeepSeek TUI** | Stable but active; Claude Code shows platform maturity (fewer PRs, but complex ecosystem); Qwen shipped 3 releases; OpenCode shipping TUX fixes despite outage |
| **Stabilizing** | **Copilot CLI**, **Kimi Code CLI** | Low PR velocity; focus on patch releases and issue triage; Copilot shows "merge/stable" phase |

### 5.2 Community Maturity Metrics

- **Most Engaged:** OpenCode (129👍 for context visibility; 10+ duplicate outage reports), Claude Code (high-quality issue triage with 20+👍 items), Pi (31 PRs/day, strong user bug reports with root-cause analysis).
- **Most Regression-Conscious:** Gemini CLI (regression tracking across 0.53-0.55), Claude Code (hook vulnerability fix within 24h), Copilot (A/B isolation reports from users).
- **Up-and-Coming:** DeepSeek TUI — the 77-commit release train suggests a significant feature release; FreeBSD support signals platform ambition.
- **Enterprise-Focused:** Copilot (GHE.com issues, .agents standardization), Claude Code (Cowork/cloud sessions, security-critical PRs).

---

## 6. Trend Signals

### 6.1 Industry Trends from Community Feedback

| Trend | Evidence | Implication for Developers |
|---|---|---|
| **Security Is the New Battleground** | Hook fail-closed fix (#84364 Claude), classifier bypasses (#8582 Qwen), IDOR in Kimi (#821), trust model rework (#8627 Qwen) | Expect more audit-focused features; permission systems will tighten; "fail-closed" will become default |
| **Context Transparency Is Table Stakes** | 129👍 for context breakdown (OpenCode), compaction audits (Pi), token usage in ACP (#4174 Copilot) | Tools must expose what's in the context window; users want cost/usage observability, not just model text |
| **Windows Reliability Is a Competitive Moat** | 5+ Windows-specific crash/leak reports per tool this week; Codex process leaks (#33776, 32 comments) | Tools winning the Windows experience will capture enterprise share; expect a Windows hardening sprint across all tools |
| **Session Durability Becomes Core Value** | Pi harness v2 (#7710), DeepSeek checkpoint resume (#5242), Codex context lineage (#37347), Claude session corruption (#73638) | Resumable, inspectable, crash-safe sessions are the next feature battleground |
| **MCP Ecosystem Is the New Plugin Economy** | MCP ports across 4+ tools (lazy loading, pooling, recovery), registry discovery (DeepSeek #5238), cross-provider hooks (Qwen #8646) | MCP is entering mainstream; tool-to-tool interoperability will be a differentiator |
| **Privacy & Attribution Movement** | OpenCode privacy concern (44👍), Gemini redaction (#26525), Claude Cowork transparency | Users increasingly demand to know where data goes, which provider processes prompts, and retention policies |
| **Automation-User Pain Is Mounting** | Permission prompt storms (700+/2 days Claude), quora drains (Codex), silent false-success (DeepSeek #5035) | Power users are pushing back on guardrail friction; expect "rule-aware prompts" and context-aware permissioning |
| **Model Metadata Quality Matters** | DeepSeek 128K silent degrade (#5244), Pi stale model lists (#7674), OpenCode wrong context sizes (#40958) | Tools must verify model specs against reality; metadata inaccuracy costs users real tokens and trust |
| **Platform Expansion Beyond Linux/macOS** | FreeBSD (DeepSeek), Termux (Pi), WSL-specific issues (Codex), Alacritty/ConHost (Copilot) | Terminal-agnostic and headless/remote workflow support will attract power users |
| **Voice & Multimodal Prepositioning** | Qwen voice frontend proposal (#8629), inline terminal images (Qwen v0.21.7), Omni file recognition (Qwen #8197) | AI CLI tools are prepping for multimodality — image-in-terminal and voice control will expand the interaction surface |

### 6.2 Key Takeaways for Technical Decision-Makers

1. **If you run automation-heavy workflows:** Watch Claude Code's permission issues (#6527, #76718) and Copilot's sticky auto-mode (#4388) — guardrail friction is the #1 productivity killer.
2. **If you support Windows teams:** All tools acknowledge gaps; Pi, Codex, and Qwen are actively addressing it. Choose based on your tolerance for instability.
3. **If you care about deployment scale:** DeepSeek's workflow orchestration and Claude's plugin ecosystem are the most hardened for fleet/CI scenarios.
4. **If you're evaluating for context efficiency:** Gemini's AST-aware tools (#22745) and DeepSeek's progressive disclosure (#5077) show the strongest token-optimization direction.
5. **If privacy is a hard requirement:** Gemini's memory redaction gaps (#26525) and OpenCode's telemetry ambiguity (#39875) are red flags today; evaluate per-tool data policies before adoption.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-08-07 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

| # | Skill / PR | Functionality | Discussion Highlights |
|---|-----------|---------------|----------------------|
| 1 | **[skill-creator eval fixes](https://github.com/anthropics/skills/pull/1298)** — MartinCajiao | Fixes `run_eval.py` reporting 0% recall; installs eval artifact as real skill; fixes Windows stream reading, trigger detection, parallel workers | Most-commented PR in repository. Cross-references Issue [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 7👍) — the eval loop has been "optimizing against noise." Multiple duplicate PRs (#1099, #1050, #1323, #1261) confirm systemic breakage. **Status: Open** |
| 2 | **[document-typography](https://github.com/anthropics/skills/pull/514)** — PGTBoos | Typographic quality control: orphan word wrap, widow paragraphs, numbering misalignment in generated documents | Popular because it addresses a universal pain—no one wants regex-weird documents. **Status: Open** |
| 3 | **[ODT skill](https://github.com/anthropics/skills/pull/486)** — GitHubNewbie0 | Create/fill/read/convert OpenDocument files (.odt, .ods); parse ODT to HTML | Fills a gap alongside existing docx/pdf skills. Active discussion on LibreOffice interplay. **Status: Open** |
| 4 | **[self-audit](https://github.com/anthropics/skills/pull/1367)** — YuhaoLin2005 | Mechanical file verification + four-dimension reasoning quality gate before delivery (v1.3.0) | Strong follow-up demand evidenced by Issue [#1385](https://github.com/anthropics/skills/issues/1385) proposal for a reasoning quality-gate pipeline. **Status: Open** |
| 5 | **[testing-patterns](https://github.com/anthropics/skills/pull/723)** — 4444J99 | Full testing stack: Testing Trophy model, unit testing (AAA), React Testing Library, edge cases | Broad scope, active discussion on philosophy vs. actionable guidance balance. **Status: Open** |
| 6 | **[pyxel retro game dev](https://github.com/anthropics/skills/pull/525)** — kitao | MCP server for Pyxel retro/pixel-art/8-bit game engine; write → run_and_capture → inspect → iterate | Author is the library maintainer (kitao/pyxel), lending credibility; community interest in creative coding. **Status: Open** |
| 7 | **[color-expert](https://github.com/anthropics/skills/pull/1302)** — meodai | Color naming systems (ISCC-NBS, Munsell, XKCD, RAL), color spaces decision table (OKLCH/OKLAB/CAM16) | Niche but deep; author is a known color-domain expert designing for "what to use when." **Status: Open** |
| 8 | **[plan-file-hygiene](https://github.com/anthropics/skills/pull/1479)** — tonydzi | Lifecycle management for planning artifacts (addresses Issue [#1417](https://github.com/anthropics/skills/issues/1417)) | Collaborative framing credit; community co-design. **Status: Open** |

---

## 2. Community Demand Trends

**Most-anticipated Skill directions from Issues:**

1. **Security & trust boundaries** — Issue [#492](https://github.com/anthropics/skills/issues/492) (43 comments, highest-traffic issue): community skills distributed under `anthropic/` namespace create a trust-boundary vulnerability where users grant elevated permissions believing skills are official.
2. **Org-wide skill sharing / lifecycle** — Issue [#228](https://github.com/anthropics/skills/issues/228) (16 comments, 8👍): users want shared skill libraries and direct sharing links instead of Slack/Teams manual transfers. Issue [#1329](https://github.com/anthropics/skills/issues/1329): symbolic compact-memory notation for long-running agents.
3. **Reliability of the creator/eval toolchain** — Issue [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 7👍) + [#1169](https://github.com/anthropics/skills/issues/1169): run_eval.py / run_loop.py systematically report 0% recall, making description optimization meaningless. This is the single most concentrated technical demand.
4. **Context window efficiency** — Issue [#1487](https://github.com/anthropics/skills/issues/1487): `claude-api` skill eagerly injects ~156k tokens, exhausting context in one tool call. Echoed by [#1175](https://github.com/anthropics/skills/issues/1175) re: security + context concerns with SharePoint.
5. **Dedup / plugin hygiene** — Issue [#189](https://github.com/anthropics/skills/issues/189) (6 comments, 9👍): `document-skills` and `example-skills` install identical content, causing duplicate skills in context window.

---

## 3. High-Potential Pending Skills (not yet merged, active discussion)

| Skill | PR | Why it may land soon |
|-------|----|---------------------|
| **[document-typography](https://github.com/anthropics/skills/pull/514)** | #514 | Universal problem; self-contained; clear scope. Likely one revision from merge. |
| **[ODT skill](https://github.com/anthropics/skills/pull/486)** | #486 | Completes the office-format family (docx, pdf exist); strong spec. |
| **[skill-quality-analyzer + skill-security-analyzer](https://github.com/anthropics/skills/pull/83)** — eovidiu | #83 | Directly addresses the top-voted security issue (#492); evaluates skills across structure/documentation (20%), security posture, etc. High strategic value for the repo maintainers. |
| **[self-audit](https://github.com/anthropics/skills/pull/1367)** | #1367 | Maintainer of parallel proposal #1385; v1.3.0 iteration shows maturity. |
| **[testing-patterns](https://github.com/anthropics/skills/pull/723)** | #723 | Broad but well-structured; fills an obvious gap in a developer-tool repo. |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, secure, and context-efficient skill-development toolchain** — the top discussion threads center on fixing `run_eval.py`'s false 0% recall (which invalidates description optimization), preventing trust-boundary abuse under the `anthropic/` namespace, and preventing skills from exhausting the context window — rather than on any single end-user skill domain.

---

# Claude Code Community Digest
**2026-08-07**

---

## Today's Highlights

A busy week for the Claude Code community with no new releases but a wealth of active discussion. The most significant trending topics include **security and permission system concerns** — particularly around compound-command prompting, git proxy restrictions in Cowork sessions, and a critical hook vulnerability fix. Desktop and Windows stability issues continue to generate the highest community engagement, with users reporting TUI rendering bugs, background service problems, and session limit miscalculations.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

### 1. [Bug] Ask list is ignored when "Bash" is in allow list — [#6527](https://github.com/anthropics/claude-code/issues/6527)
**23 comments | 19 👍**
Users report that the `ask` permission list is silently bypassed when `Bash` appears in the allow list. This is a **security concern** — the feature that should prompt for approval on specific commands is effectively disabled. Community members have confirmed the behavior persists on Linux with the latest CLI version.

### 2. [Enhancement] Disable bundled Cowork background service on Windows — [#57371](https://github.com/anthropics/claude-code/issues/57371)
**18 comments | 42 👍**
The **most-upvoted issue** this week. Windows users want an option to disable the CoworkVMService background service that ships with Claude Desktop. Many users don't use Cowork and find the persistent background process wasteful and invasive. High engagement indicates this is a quality-of-life priority for the Windows community.

### 3. [Bug] Session limit reaches 100% despite low visible usage — [#54750](https://github.com/anthropics/claude-code/issues/54750)
**16 comments | 9 👍**
Claude Code reports the current session limit as completely exhausted, blocking further usage, even though local usage tracking shows minimal consumption. This is **cost-critical** for users on metered plans — incorrectly enforced limits directly impact productivity and spending.

### 4. [Bug] Git proxy blocks all pushes in Cloud/Cowork sessions — [#76248](https://github.com/anthropics/claude-code/issues/76248)
**14 comments | 5 👍**
The git proxy in remote Cowork sessions now blocks pushes to repositories **not in the session's authorized set** — even when users supply their own fine-grained PATs. Users are frustrated by the regression, noting that previously-working PAT pass-through authentication no longer functions. Cloud session automation workflows are being disrupted.

### 5. [Bug] Assistant text before tool calls intermittently not rendered — [#79584](https://github.com/anthropics/claude-code/issues/79584)
**9 comments | 7 👍**
On Windows, assistant text emitted before a tool call (particularly `AskUserQuestion`) in the same turn is sometimes never displayed. This is particularly impactful for **plugin-driven workflows** where users need context before making decisions.

### 6. [Bug] Session rename mid-tool-call corrupts transcript — [#73638](https://github.com/anthropics/claude-code/issues/73638)
**9 comments | 0 👍**
Renaming a session while a server tool call is in flight injects a synthetic user turn **between the tool block and its result**, permanently corrupting the transcript. Every subsequent prompt returns a 400 error. A reproducible bug affecting session continuity.

### 7. [Feature] System notifications when Claude needs attention — [#26581](https://github.com/anthropics/claude-code/issues/26581)
**8 comments | 32 👍**
The **second most-upvoted request**. Users want system-level notifications (terminal or VSCode) when Claude completes tasks or requires attention. This is a long-standing request (since February) that continues to accumulate support from users running multi-session workflows.

### 8. [Bug] Compound-command prompting makes orchestration unusable — [#76718](https://github.com/anthropics/claude-code/issues/76718)
**7 comments | 0 👍**
Permission system prompts on **compound commands even when every segment is individually allowlisted**. One user reports approving **700+ prompts** in two days of parallel-session workflows. A critical pain point for automation-heavy users.

### 9. [Regression] Desktop time-range filter only appears with State grouping — [#78775](https://github.com/anthropics/claude-code/issues/78775)
**7 comments | 23 👍**
A regression in the desktop app where the session time-range filter no longer appears unless "Group by" is set to "State." Highly-upvoted UI regression affecting basic session management workflows.

### 10. [Bug] ECONNRESET on streaming API calls — Windows only — [#84194](https://github.com/anthropics/claude-code/issues/84194)
**5 comments | 0 👍**
The bundled Bun HTTP client fails with `ECONNRESET` on streaming API calls while Node.js and curl succeed with identical requests. The issue persists across VPN configurations and survives reinstalls — pointing to a **bundled runtime networking defect** on Windows.

---

## Key PR Progress

### 1. [Open] Enable frontend-design plugin at project scope — [#84600](https://github.com/anthropics/claude-code/pull/84600)
Registers the official anthropics/claude-code marketplace and enables the frontend-design skill via `.claude/settings.json`, loading it automatically for all users of the repo.

### 2. [Open] Fix validate-agent.sh exiting on first warning — [#84427](https://github.com/anthropics/claude-code/pull/84427)
Follow-up to #76985. The validation script uses `((error_count++))` and `((warning_count++))`, which return non-zero exit codes in Bash — causing premature termination under `set -e`. Fixes the plugin development tooling.

### 3. [Open] Handle wrapped hook schemas in validate-hook-schema.sh — [#84381](https://github.com/anthropics/claude-code/pull/84381)
Fixes the hook schema validator to support both top-level `"hooks"` object wrappers and optional matchers, making it accurately validate Claude Code hook configurations.

### 4. [Open] Allow any user thumbs down to prevent auto-close — [#84365](https://github.com/anthropics/claude-code/pull/84365)
Fixes #79146 by matching the dedupe bot's promise — any user's thumbs-down reaction now prevents automatic issue closure, not just the reporter's.

### 5. [Open] Fail closed on hook exceptions in pretooluse hook — [#84364](https://github.com/anthropics/claude-code/pull/84364)
**Security-critical fix.** An exception during rule evaluation previously caused the hook to exit with status 0, **allowing gated tool execution**. Now exceptions emit `permissionDecision: 'deny'`, ensuring unauthorized actions are always blocked.

---

## Feature Request Trends

### 1. System Notifications & Attention Management
Multiple requests (e.g., #26581) for OS-level notifications when Claude needs input or completes tasks. Users running parallel sessions need ambient awareness without constant terminal polling.

### 2. Cowork & Background Service Control
Users want finer-grained control over the Cowork feature, including the ability to disable background services and adjust git proxy behavior (#57371, #76248).

### 3. Proactive Context Compaction
Interest in allowing Claude to self-initiate context compaction rather than waiting for system thresholds (#33026) — a workflow optimization for complex multi-step tasks.

### 4. Expanded Remote Control & Session Management
Requests for improved session title persistence, richer remote control features (web UI title control, #48092 reference), and better filter/grouping options in the desktop app (#78775).

### 5. Documentation Completeness
A consistent stream of documentation gap reports (all marked stale/closed by bot, ~15 in the last day) covering undocumented aliases (/proactive, /undo), environment variables, and behaviors. The community clearly relies heavily on CLI docs and finds gaps quickly.

---

## Developer Pain Points

1. **Permission System Friction** — Compound commands triggering approval prompts despite allowlist coverage (#76718), and the `ask` list being ignored when `Bash` is in the allow list (#6527). Automation-heavy workflows are hit hardest.

2. **Windows-Specific Instability** — TUI rendering issues (#79584), bundled HTTP client failures (#84194), and desktop crashes (#81664) are recurring themes. Windows remains a second-class citizen in reliability terms.

3. **Session Management Defects** — Session limits miscalculated (#54750), rename operations corrupting transcripts (#73638), and time-range filter regressions (#78775) undermine user confidence in session persistence.

4. **Cowork/Remote Session Restrictions** — Git proxy authorization changes (#76248) breaking previously-working PAT-based pushes, with users reporting mid-session behavior changes without warning.

5. **Security & Stability in Ecosystem Tooling** — The vulnerability-class bug in hook error handling (#84364) and intermittent rendering of pre-tool-call context (#79584) highlight that guardrails and determinism issues persist in the plugin ecosystem and core rendering paths.

6. **Cloud/Cowork Transparency** — The 100% session-limits-despite-low-usage bug (#54750) has been open since April. Users monitoring costs closely are the most vocal about inaccurate accounting in cloud-mediated sessions.

---

*Generated from GitHub data for anthropics/claude-code — 50 issues, 5 PRs, 0 releases in the last 24 hours.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-07

## 1. Today's Highlights

Release **rust-v0.147.0** brings portable Agent Plugins with cross-catalog search and persistent, manually ordered conversation sections. Major community attention centers on severe Windows performance bugs—including a report of hundreds of `taskkill.exe`/`conhost.exe` processes causing WMI storms (#33776, 32 comments) and a cluster of recently filed macOS zombie-process leaks. A dozen PRs landed today focused on MCP handler reuse, subagent context tracking, and sandbox hardening, signaling continued investment in reliability and performance.

## 2. Releases

**rust-v0.147.0** — [Release](https://github.com/openai/codex/releases)
- **Portable Agent Plugins**: Install and search across local, personal, workspace, and remote plugin catalogs (#36544, #36409, #36919, #36796)
- **Persistent conversation organization**: Manually ordered sections that survive sessions; incremental browsing for long transcripts (#35722, #36007, #36380, #36948)

## 3. Hot Issues

1. **[#33776 — Windows: ChatGPT.exe spawns hundreds of taskkill.exe/conhost.exe processes](https://github.com/openai/codex/issues/33776)** — 32 comments, 27 👍. 287+ orphaned processes cause WMI failure storms and DWM degradation. Highest-engagement issue today; critical for Windows Desktop users' system stability.

2. **[#19694 — Model picker filters out models from model_catalog_json](https://github.com/openai/codex/issues/19694)** — 14 comments, 35 👍. Closed, but highest-reacted issue in this window. Custom-model users on Desktop can't see models returned via `model_catalog_json`, breaking BYO-model workflows.

3. **[#21653 — Multi-line status line support](https://github.com/openai/codex/issues/21653)** — 12 comments, 58 👍. Long status line configurations are silently truncated in the TUI. Strong community demand; the most-reacted open issue.

4. **[#28080 — Desktop thread tools intermittently lose handlers ("No handler registered")](https://github.com/openai/codex/issues/28080)** — 21 comments. Tool handlers disappear mid-session on Windows, disrupting active work. No workaround identified yet.

5. **[#20883 — Project-scoped MCP process pool instead of per-session](https://github.com/openai/codex/issues/20883)** — 17 comments. Each chat spawns its own stdio MCP servers; users want workspace-level sharing to reduce resource waste.

6. **[#35355 — Compaction promotes partial output from interrupted commands into confirmed state](https://github.com/openai/codex/issues/35355)** — 5 comments. Ephemeral observations from interrupted commands can be treated as verified task state in later turns—data-integrity concern.

7. **[#16579 — Configurable default session shell on Windows](https://github.com/openai/codex/issues/16579)** — 4 comments, 32 👍. PowerShell is hardcoded; Git Bash and other shell users want a config option.

8. **[#35463 — Subagents drain full week quota overnight](https://github.com/openai/codex/issues/35463)** — 4 comments. Usage counting is broken for subagents; Pro 20x users burn their entire weekly quota in one background run.

9. **[#33967 — Windows: cannot complete setup or enter limited-access mode](https://github.com/openai/codex/issues/33967)** — 9 comments. App stuck on "Complete Windows setup" screen; no clear remediation path for affected users.

10. **[#33531 — MCP suites persist after subagents complete (10.9 GB private memory)](https://github.com/openai/codex/issues/33531)** — 5 comments. Severe memory leak on Windows when subagents finish but MCP processes remain resident.

## 4. Key PR Progress

1. **[#37352 — Configure default code-mode exec yield timeout](https://github.com/openai/codex/pull/37352)** — New `features.code_mode.default_exec_yield_time_ms` (30s default); configurable per-call.

2. **[#37350 — ThreadManager custom thread ID generation](https://github.com/openai/codex/pull/37350)** — Pluggable ID allocator for root/child/forked threads; UUIDv7 remains default.

3. **[#37349 — Minimal /dev in full-filesystem Bubblewrap sandboxes](https://github.com/openai/codex/pull/37349)** — Overlays minimal device filesystem in network-isolated sandboxes to prevent host device-tree inheritance.

4. **[#37347 — Track context windows per agent](https://github.com/openai/codex/pull/37347)** — Forked subagents now get distinct context-window lineage; fixes inherited compacted history metadata.

5. **[#37345 — Model routing hints to Codex backend](https://github.com/openai/codex/pull/37345)** — New `x-codex-routing-hint` header on HTTP, compaction, and WebSocket requests for better backend routing.

6. **[#37344 — Fix subagent MCP startup status settling](https://github.com/openai/codex/pull/37344)** — Clears cached MCP startup expectations for active subagents; TUI no longer shows startup as perpetually running.

7. **[#37337 — Recover MCP servers after OAuth reauthentication](https://github.com/openai/codex/pull/37337)** — Failed OAuth-backed MCP servers become available post-sign-in without client restart.

8. **[#37336 — Step environments for extension turn input](https://github.com/openai/codex/pull/37336)** — Extensions now receive the same refreshed environment snapshot as the current step, not stale data.

9. **[#37341 — Content references for inline visualizations](https://github.com/openai/codex/pull/37341)** — Structured `visualize` content references supported in cached, streaming, and finalized TUI rendering.

10. **[#37273 — Reuse MCP handlers across sampling steps](https://github.com/openai/codex/pull/37273)** — Caches immutable MCP handlers per session; eliminates redundant schema construction per sampling step.

## 5. Feature Request Trends

- **MCP lifecycle management**: Process pooling per project (#20883), server recovery after reauth (#37337), and startup-status fixes (#37344)—the community wants MCP to be robust and resource-efficient.
- **Session shell configurability**: Windows users want to choose their default shell (Git Bash, etc.) rather than being locked to PowerShell (#16579).
- **Sandbox/delegation hardening**: RFCs for host-enforced authority ceilings (#36381) and minimal `/dev` mounting in sandboxes (#37349) show demand for stricter least-privilege isolation.
- **Status line and TUI ergonomics**: Multi-line status lines (#21653) and full inline viewport repaints (#37335) reflect a push for a richer terminal experience.

## 6. Developer Pain Points

- **Windows-specific instability dominates**: Process leaks (#33776), WSL sandbox failures (#24873), and firewall/UAC re-arming (#31556) make Windows the most problematic platform.
- **Zombie/orphan process leaks**: At least five separate reports on macOS (#37244, #37247, #37249, #37236, #37084) and one on Windows (#33776) describe runaway child processes exhausting system limits.
- **Memory leaks in MCP/subagent workflows**: Cached MCP servers persisting after subagent completion (#33531) and per-session MCP duplication (#20883) waste significant memory.
- **State integrity concerns**: Interrupted command output being promoted to confirmed state (#35355) and checkpoint prose overriding durable project state (#37325) undermine trust in long-running sessions.
- **Quota/usage accounting bugs**: Subagents draining weekly quotas (#35463) and incorrect usage limits after reset (#37250) directly impact paid users' ability to work.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest - 2026-08-07

## Today's Highlights

The Gemini CLI project is seeing a flurry of active bug fixes and quality-of-life improvements, with a notable push toward stabilizing subagent behavior and addressing memory system issues. Several PRs target critical bugs around tool output truncation, stream abort handling, and model fallback on capacity exhaustion, while community members continue contributing fixes for terminal rendering and error message clarity. A concerning new issue (UNKNOWN_UPSTREAM_ERROR with image attachments) has been filed against v0.53.1, indicating a potential regression in multimodal handling.

## Releases

No new releases in the last 24 hours. The most recent release was **v0.54.2** (PR #28712), with a following cherry-pick patch PR (#28719) preparing **v0.55.0-preview.2**.

## Hot Issues

1. **[#22323 - Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — Critical bug where `codebase_investigator` subagents falsely report success after hitting turn limits, masking actual failures. 12 comments, high priority (p1), still awaiting retesting.

2. **[#21409 - Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** — P1 bug where the generalist agent hangs indefinitely on simple tasks (e.g., folder creation), with 8 upvotes and 8 comments. Users report waiting up to an hour before cancelling. Workaround: explicitly disable subagent delegation.

3. **[#24353 - Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** — Epic tracking expansion of behavioral eval tests. Currently 76 tests across 6 Gemini models; aims to build more comprehensive component-level testing infrastructure.

4. **[#22745 - Assess AST-aware file reads/search/mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** — Epic investigating AST-aware tooling to reduce token usage and improve precision in method-level reads and codebase navigation.

5. **[#21968 - Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — Noted behavioral gap: model ignores available custom skills (e.g., "gradle", "git") unless explicitly instructed, reducing effectiveness of user-configured workflows.

6. **[#25166 - Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1 bug where simple completed CLI commands appear hung at "Awaiting user input" — 3 upvotes, affects core workflow reliability.

7. **[#26522 - Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — Auto Memory system keeps surfacing unprocessed sessions that extraction agents deem low-signal, causing redundant work and potential wasted tokens.

8. **[#26525 - Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — Privacy concern: memory transcripts are sent to the extraction model with only prompt-based redaction (after content enters context); needs deterministic pre-redaction.

9. **[#28714 - UNKNOWN_UPSTREAM_ERROR when attaching any image](https://github.com/google-gemini/gemini-cli/issues/28714)** — New, urgent p1: image attachment causes chat to freeze (needs new chat to recover) on v0.53.1 with Gemini 3.6 Flash High. 1 comment, likely regression.

10. **[#22093 - (Sub)agents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** — Subagents activating despite explicit configuration disabling them; user expects MCP-only behavior but generalist agent runs anyway.

## Key PR Progress

1. **[#28718 - Record usage already received when a stream is aborted](https://github.com/google-gemini/gemini-cli/pull/28718)** — Fixes token accounting loss on stream abort: usage metadata captured per-chunk was only flushed on success path; this persists it on abort as well (closes #28682).

2. **[#28716 - Reclassifying Capacity Exhaustion as Terminal Error](https://github.com/google-gemini/gemini-cli/pull/28716)** — Optimizes error classification: model capacity exhaustion and insufficient credits now trigger immediate fallback/graceful degradation rather than retry loops.

3. **[#28700 - Stop a new user message fusing into an unanswered tool response](https://github.com/google-gemini/gemini-cli/pull/28700)** — Critical UX fix: interrupted tool calls previously merged the next user message into the interrupted turn, causing the model to "finish your sentence" instead of responding. Cherry-picked to v0.54.1.

4. **[#28639 - Guard formatTruncatedToolOutput against non-positive maxChars](https://github.com/google-gemini/gemini-cli/pull/28639)** — Fixes output inflation (~2x) when maxChars ≤ 0 due to negative slice indexing; adds regression tests.

5. **[#28641 - Prevent ghost text wrapping infinite loop at narrow widths](https://github.com/google-gemini/gemini-cli/pull/28641)** — Fixes hang with CJK/emoji at narrow terminal widths; force-advances splitIndex to guarantee termination.

6. **[#28673 - Add Gemini 3.6 Flash and 3.5 Flash-Lite model configurations](https://github.com/google-gemini/gemini-cli/pull/28673)** — New model support: base definitions, capabilities (thinking, multimodalToolUse), aliases, Code Execution settings.

7. **[#28719 - Cherry-pick to v0.55.0-preview.2](https://github.com/google-gemini/gemini-cli/pull/28719)** — Automated patch release bump for the preview line; also includes prior preview changes.

8. **[#28586 - Preserve thoughtSignature in functionCall parts to fix 400 error](https://github.com/google-gemini/gemini-cli/pull/28586)** — Fixes regression (since 0.53.0) causing 400 Bad Request during parallel tool calls — thoughtSignature was being stripped.

9. **[#28679 - Improve Vertex AI 401 error message](https://github.com/google-gemini/gemini-cli/pull/28679)** — Better DX when using standard API key with vertex-ai auth type; produces clear actionable error instead of failing opaquely.

10. **[#28405 - Prevent scroll position jump during content updates](https://github.com/google-gemini/gemini-cli/pull/28405)** — Fixes #5009: scroll-to-bottom re-enables too aggressively when user scrolls up to review changes and new content arrives.

11. **[#19638 - Cap search results and clarify context overflow message](https://github.com/google-gemini/gemini-cli/pull/19638)** — Guards against context-window overflow from broad SearchText queries (thousands of matches); improves the overflow UI message to be actionable.

## Feature Request Trends

- **Component-level Evaluation Infrastructure (#24353):** Users and maintainers want more sophisticated, targeted testing — beyond current 76 behavioral evals — with per-component regression coverage and multi-model benchmarking.
- **AST-Aware Codebase Tools (#22745, #22746):** Growing interest in AST-based file reads, method-boundary detection, and codebase mapping to reduce token usage and navigation turns.
- **Better Subagent Autonomy and Visibility (#21968, #22598):** Users want agents to actively use configured skills/subagents, and to see/inspect subagent trajectories (via `/chat share`).
- **Increased Agent Self-Awareness (#21432):** Demand for Gemini CLI to accurately know its own flags, hotkeys, and configurations to guide users effectively.
- **Memory System Hardening (#26516, #26522, #26523, #26525):** Multi-issue epic around Auto Memory robust — better redaction, validation of patches, no retry storms on low-signal data, and deterministic handling.
- **Non-Interactive Mode Parity (#20536):** Requests for `/stats` and other interactive commands to work in headless/CI contexts by writing to stdout.

## Developer Pain Points

- **Hangs and False Successes:** Recurring theme — subagents hang (generalist agent, #21409), report success after MAX_TURNS (#22323), or get stuck on interactive prompts (vite app, #22465; shell "Waiting input", #25166).
- **Configuration Ignored or Silently Overridden:** Subagents run when disabled (#22093); browser_agent ignores `settings.json` `maxTurns` (#22267) — undermining user trust in configuration.
- **Privacy/Firewall Blind Spots:** Auto Memory sends transcripts to models before redaction (#26525) — serious concern for enterprise users handling sensitive codebases.
- **Tool-Output Edge Cases:** 400 errors with >128 tools (#24246); `formatTruncatedToolOutput` inflating outputs (#28639); loss of usage accounting on aborted streams (#28718).
- **Terminal Rendering Gremlins:** Ghost-text loops with CJK/emoji at narrow widths (#28641); screen corruption after exiting external editors (#24935); scroll jumps during updates (#28405).
- **Destructive Command Risk (#22672):** Model occasionally uses `git reset`, `--force`, or modifies DBs without prompting — users asking for built-in guardrails against destructive operations.
- **Regression Sensitivity:** Multiple issues (image attachments breaking, #28714; thoughtSignature stripping, #28586) show users are sensitive to regressions introduced in recent versions (0.53–0.55 range).

---

*Sources: All data from [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli), retrieved 2026-08-07.*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-07

## Today's Highlights
Yesterday's release (v1.0.79-6) quietly fixes two nagging stability issues — a spurious diagnostic warning during rare internal delays and a session-history load failure that left transcripts permanently blank. The community is actively reporting on the v1.0.78–1.0.79 line, with new issues surfacing around permission-mode switching bugs, model catalog gaps for enterprise organizations, and a concerning new report of orphaned MCP server processes. Notably, the backlog shows strong demand for cross-cutting improvements in terminal rendering, session/resume reliability, and MCP registry behavior.

## Releases
- **v1.0.79-6** — Patch release containing two bug fixes:
  - A rare internal delay no longer prints a diagnostic warning on top of the interactive UI.
  - A failed session-history load no longer leaves the timeline permanently empty; previously the failure was silently discarded, leaving the transcript blank for the rest of the session.
  
  No breaking changes or new features in this release.

## Hot Issues
1. **[#3392 — Bash tool breaks on NixOS with version >=1.0.49](https://github.com/github/copilot-cli/issues/3392)** — Long-standing (89 days) and still open: agent commands fail with `Failed to start bash process`. High community traction with 7 👍. The maintainers have the strace evidence but the issue remains unresolved, making it one of the oldest and most impactful platform-specific bugs.

2. **[#4174 — ACP server does not expose token/context usage in any protocol message (CLOSED)](https://github.com/github/copilot-cli/issues/4174)** — Closed, but a meaningful data point: users integrating Copilot CLI into other tools cannot track cost or context consumption. The closure likely signals either a fix in progress or a deliberate scope decision — worth watching for follow-up.

3. **[#4251 — Resume of a large session OOMs / grinds CPU for ~70 min in 1.0.74 (regression)](https://github.com/github/copilot-cli/issues/4251)** — A clear regression with controlled A/B isolation. Users with long-lived daily sessions are affected; memory use is 3–4× higher than 1.0.73. This is a serious quality-of-life issue for power users.

4. **[#4313 — Allow scrolling through current conversation history](https://github.com/github/copilot-cli/issues/4313)** — A highly requested interaction feature: the inability to use the mouse wheel or PageUp/PageDown to navigate long conversations. Currently users can only scroll up manually with arrow keys; this request is getting steady community support.

5. **[#4311 — Transcript renders as blank lines until children/width change](https://github.com/github/copilot-cli/issues/4311)** — The terminal-rendering cache invalidation bug causes the transcript to blank out intermittently, especially in the bottom region. `/resume` does not recover; only submitting a new message repaints. Seems related to the ScrollBox measured-line cache — a claim backed by detailed technical analysis.

6. **[#4388 & #4389 — Permissions stuck in auto mode after changing back to interactive](https://github.com/github/copilot-cli/issues/4388)** — Two separate reports (from different users) describe the same bug: after switching from auto mode back to interactive, the agent continues making code changes without permission prompts. This is a safety-relevant issue for anyone toggling permission modes.

7. **[#4384 — Terminal title changes to "Windows PowerShell" when not launched in Windows Terminal](https://github.com/github/copilot-cli/issues/4384)** — A Windows-specific cosmetic bug reported for 1.0.79-5: the CLI sets its own title (GitHub Copilot) but it gets overwritten. Small but annoying, especially for users on Alacritty/ConHost.

8. **[#4392 — Post-auth MCP client rebuild leaves orphaned stdio server processes](https://github.com/github/copilot-cli/issues/4392)** — At startup, the CLI tears down and rebuilds the entire MCP client post-authentication, but the first generation of stdio child processes is never killed. Over time this can accumulate zombie processes — a resource-leak concern for long-running dev machines.

9. **[#4390 — Enabled organization models missing from catalogue (Anthropic & Kimi K3)](https://github.com/github/copilot-cli/issues/4390)** — Models explicitly enabled by a Copilot Business organization are unavailable in the CLI. Users report two distinct failures: no Anthropic models at all and missing Kimi K3. This blocks enterprise adoption of those models.

10. **[#4373 — Queued messages are stuck forever](https://github.com/github/copilot-cli/issues/4373)** — Multiple reports of messages going into a "queued" state that the model never picks up; Ctrl+C doesn't cancel them. This is one of several interactive-queue bugs reported this week (#4372 and #4385 are related), making queue handling a hot spot in the codebase.

## Key PR Progress
No new or updated pull requests were reported in the last 24 hours. The project appears to be in a merge/stable phase, with maintainers focused on triaging the recent influx of issues rather than landing new PRs.

## Feature Request Trends
- **In-session model switching** — Requests for BYOM providers to support **model discovery and in-session switching without restart** (#4376) show that users expect flexible model experimentation now that BYOM is supported.
- **Conversation navigation** — Scrolling the transcript with mouse/page keys (#4313) remains a top ergonomic request.
- **Context/cost transparency** — Users want visibility into token usage and context consumption, especially in non-interactive/ACP modes (#4174). This reflects a broader push for observability in AI coding assistants.
- **.agents standardization** — Extending `.agents` beyond skills to instructions, agents, and hooks in any opened folder (#4204) — users want a single convention for all agent customizations.
- **Permission transparency** — When a command triggers a permission prompt, users want to see *which rule or command characteristic* triggered it (#4386), not just the command being run.

## Developer Pain Points
1. **Permission-mode flakiness** — The repeated reports of sticky auto-mode after switching back to interactive (#4388, #4389) are concerning because they involve the safety guardrail. Users expect mode switches to be immediate and honored by the model.
2. **Queue and steering message ordering** — Multiple bugs (#4372, #4373, #4385) indicate that the message queue is fragile: messages get stuck, ordering gets flipped, and background tasks hang even after shell exit. This is affecting daily flows.
3. **Session resume reliability** — The OOM / high-CPU regression on large-session resume (#4251) and the silent history-load failure (now fixed in v1.0.79-6) show that resume paths are a fragile area that heavy users feel most acutely.
4. **MCP registry friction** — `/mcp search` breaking in non-GitHub remote environments (#4374) and the Actions GITHUB_TOKEN registry 403s (#4346) are blocking CI and Azure DevOps users from using MCP at all. The orphaned-process leak (#4392) adds a system-level cost.
5. **Terminal rendering issues** — Blank transcripts (#4311), dark-on-dark in tmux (#4212), and Windows title hijacking (#4384) — rendering bugs persist across platforms and are hard to work around.

---
*Digest generated from GitHub Copilot CLI repository data on 2026-08-07.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-07

## Today's Highlights

The community has rallied around a critical data-integrity bug in `StrReplaceFile` that silently corrupts non-UTF-8 bytes outside the edited region, with two independent PRs (#2594, #2595) submitted within 24 hours. Meanwhile, the long-awaited **Memory System** feature request (#1283) continues to gain traction as the most-discussed issue, and the VSCode extension's UX gaps—such as non-clickable file paths in Plan mode—remain prominent developer frustrations.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

**1. [#1283 — Feature Request: Memory System — Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)**  
The most-discussed open issue (20 comments) remains focused on implementing session-persistent memory for AI-managed context, project patterns, and user preferences. Community members are actively proposing design approaches for automatic vs. manual memory management. *👍 0 | Updated 2026-08-06*

**2. [#2591 — StrReplaceFile corrupts undecodable bytes outside the edited region](https://github.com/MoonshotAI/kimi-cli/issues/2591)**  
Critical bug caused by decoding the entire file with `errors="replace"`, which converts any non-UTF-8 byte—even far from the edit—into `EF BF BD` on disk. This silently corrupts files containing binary data, legacy encodings, or invalid UTF-8 sequences. *👍 0 | 3 comments | Updated 2026-08-07*

**3. [#2317 — [VSCode Extension] Plan mode file path not clickable in chat webview](https://github.com/MoonshotAI/kimi-cli/issues/2317)**  
Users cannot click file paths in Plan mode output to open the referenced files directly—a significant workflow break for code review and navigation. *👍 1 | 4 comments | Updated 2026-08-06*

**4. [#2474 — CLI interface continuously flickering / re-rendering entire conversation](https://github.com/MoonshotAI/kimi-cli/issues/2474)**  
Bilingual report of persistent UI shaking where the terminal inexplicably re-renders the complete conversation from scratch, creating a unusable editing experience on Linux. *👍 2 | 2 comments | Updated 2026-08-06*

**5. [#2147 — Lazy-load MCP tool schemas into context](https://github.com/MoonshotAI/kimi-cli/issues/2147)**  
Proposal to inject MCP tool schemas on-demand rather than preloading all at session start. With multiple MCP servers, thousands of tokens are wasted on unused tool definitions before the user sends the first message. *👍 1 | 1 comment | Updated 2026-08-06*

**6. [#2593 — VSCode plugin: quick auto/yolo/manual mode switching + usage status bar](https://github.com/MoonshotAI/kimi-cli/issues/2593)**  
Request to add one-click mode toggles (auto/yolo/manual) in the VSCode extension panel and display remaining quota (e.g., 5-hour allowance) directly in the status bar for easier monitoring. *👍 0 | 0 comments | Updated 2026-08-06*

**7. [#621 — First WriteFile always errors "Invalid path", falls back to absolute path](https://github.com/MoonshotAI/kimi-cli/issues/621)**  
Recurring complaint that the first file-write operation consistently fails with a relative-path resolution error before the tool retries with an absolute path. Now closed, but the workaround pattern (always using absolute paths) is documented in comments. *👍 0 | 2 comments | Updated 2026-08-06*

**8. [#821 — Missing authorization checks + dependency updates needed](https://github.com/MoonshotAI/kimi-cli/issues/821)**  
Security review findings: 2 IDOR/missing-authorization vulnerabilities in the web API (CVSS 7.0-8.0) and 5 dependency CVEs with available fixes. Now closed; community should verify whether the fixes landed in the codebase. *👍 0 | 0 comments | Updated 2026-08-06*

---

## Key PR Progress

**1. [#2594 — fix(tools): preserve non-UTF-8 bytes in StrReplaceFile edits](https://github.com/MoonshotAI/kimi-cli/pull/2594)**  
Correctly applies `old`/`new` as UTF-8 byte substrings on the raw buffer instead of decoding the entire file. While this preserves non-edit bytes, the diff-alignment strategy needs review to ensure the correct region is matched after multi-byte misalignment. *Open | Created 2026-08-06*

**2. [#2595 — fix(StrReplaceFile): refuse to edit files that are not valid UTF-8](https://github.com/MoonshotAI/kimi-cli/pull/2595)**  
Defense-in-depth alternative: detect invalid UTF-8 upfront and hard-fail instead of corrupting data. Safer default, though it blocks editing legacy-encoded files entirely. *Open | Created 2026-08-06*

**3. [#2255 — feat(shell): support Shift+Enter for inserting newlines](https://github.com/MoonshotAI/kimi-cli/pull/2255)**  
Adds Shift+Enter as the discoverable standard shortcut for inserting newlines in interactive prompts, complementing existing Ctrl-J and Alt-Enter bindings. Aligns with muscle memory from most terminal-based chat tools; now closed. *Closed | Updated 2026-08-06*

---

## Feature Request Trends

- **Session Memory (most requested):** Persistent context across sessions—both AI-managed and user-defined—remains the top community ask, driven by the need to avoid re-explaining project patterns and preferences in every new conversation.
- **VSCode Extension UX Improvements:** Users want mode switching (auto/yolo/manual), quota visibility in status bar, and clickable file paths in Plan mode—signaling that the extension has become the primary interface for many.
- **Context Budget Optimization:** Lazy-loading MCP tool schemas to reduce token consumption at session start indicates growing concern about context efficiency with multi-server setups.
- **Data-Integrity Safeguards:** The immediate community response with two competing PRs shows a strong demand for no-data-loss guarantees in file-editing tools.

---

## Developer Pain Points

- **Silent Data Corruption:** The `StrReplaceFile` corruption issue (#2591) is a high-severity concern—attempting to edit a UTF-8 file with stray invalid bytes can permanently corrupt unrelated regions, undermining trust in automated file modifications.
- **UI Instability:** Terminal flickering/re-rendering (#2474) disrupts deep-work sessions, forcing users to watch the interface redraw instead of focusing on their code.
- **Context Overhead:** The cost of injecting all MCP tool schemas into prompt context is a measurable production issue for teams with multiple MCP servers, reducing effective context budget before conversation starts.
- **Workflow Friction:** Small UX gaps—non-clickable paths in Plan mode, missing mode-switch shortcuts in the VSCode panel, no status-bar quota display—compound into daily friction for power users.
- **Path-Resolution Reliability:** The persistent "Invalid path" first-write error (#621) forces developers to use absolute paths defensively, adding unnecessary friction to automation scripts and agent workflows.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-07

## Today's Highlights
The most critical situation is the **widespread "Request blocked by upstream provider" 401 error affecting OpenCode Go and Zen subscriptions**, with at least 10 open issues and hundreds of 👍 reactions, indicating a likely unresolved server-side outage or authentication regression. In parallel, the maintainers are merging a **significant battery of PRs focused on TUI UX (queued prompts, session-scoped model selection, permission prompt lifecycle)** and core reliability (tool output bounding, empty stream delta handling, session transfer protocol). Finally, the community continues to push for **session/context visibility features** (searchable session contents, cross-project pickers), signaling a strong demand for better session management tooling.

---

## Releases
No new releases in the last 24 hours. Latest version referenced in issues remains **v1.18.14**.

---

## Hot Issues

### 1. "Request blocked by upstream provider" (OpenCode Go/Zen) — Pervasive outage
**#38257** | [Link](https://github.com/anomalyco/opencode/issues/38257) | 44 💬 | 11 👍
The most commented issue: all Go-tier models return 401 on chat/completions while /v1/models works. The reporter suspects a server-side issue. The sheer volume of duplicate issue titles ("Request blocked by upstream provider") across multiple accounts and subscription plans (Go, Zen) suggests a platform-level incident or a provider-side block, not user misconfiguration. The maintainers have not yet provided a public root-cause.

### 2. Duplicate of the same outage — demonstrating widespread impact
**#38218** | [Link](https://github.com/anomalyco/opencode/issues/38218) | 31 💬 | 13 👍
A Chinese-language report with 13 👍, confirming the same symptom across regions. The user has tried reinstalling, multiple models, all failing. This reinforces that the issue is not tied to a single plan or geographic region.

### 3. Third independent report of the same 401 — full-stack impact
**#38195** | [Link](https://github.com/anomalyco/opencode/issues/38195) | 24 💬 | 17 👍
This issue (oldest, created 07-21) notes that the issue occurs on both desktop and Hermes apps, on Windows and macOS. User properly isolates that direct provider keys (e.g., DeepSeek, Anthropic) work fine, so the block is in the OpenCode relay/auth layer.

### 4. Feature: Session context usage breakdown (like `/context` in Claude)
**#6152** | [Link](https://github.com/anomalyco/opencode/issues/6152) | 22 💬 | 129 👍
The **most thumbed-up issue in this digest**. Users want a TUI dialog showing token/context window breakdown per session. The sheer popularity (129 👍) plus 22 comments indicates that context transparency is the single most-wanted UX feature. No official response yet.

### 5. Feature: Cross-project session list/picker
**#31932** | [Link](https://github.com/anomalyco/opencode/issues/31932) | 15 💬 | 6 👍
Requests a global session picker that works across multiple repositories. Current `/sessions` is scoped to the current project, which is painful for developers who work across monorepos or multiple repos. Complements #6152 (session context usage).

### 6. Feature: Clickable links (Ctrl+Left Click)
**#1168** | [Link](https://github.com/anomalyco/opencode/issues/1168) | 11 💬 | 119 👍
A long-standing request from 2025, still open. This is purely a UX polish issue (click URLs in TUI/desktop to open in browser). High 👍 suggests devs use OpenCode for browsing error traces and documentation links frequently. Would be trivial to implement and would close a lot of user friction.

### 7. Privacy: Go plan wording and provider attribution silently removed
**#39875** | [Link](https://github.com/anomalyco/opencode/issues/39875) | 6 💬 | 44 👍
A concerned subscriber reports that two commits removed "Go privacy wording" and provider attribution, and asks for telemetry and retention to be added to the privacy policy. The user links to 5 prior related issues that got no substantive response. Notably, **this is an escalation from a single bug report to a governance/privacy concern with high community agreement (44 👍)**.

### 8. Subscription not activated after sign-up (payment method loop)
**#40234** | [Link](https://github.com/anomalyco/opencode/issues/40234) | 13 💬 | 0 👍
New user subscribed on the website, received confirmation email, but the client still shows "please subscribe" and returns `No payment method. Add a payment method here: …` error. This is a **billing/account sync bug** in the web app, distinct from the 401 issues above, but just as business-critical for conversion.

### 9. Feature: Configurable mid-run prompt semantics (queue vs steer vs break)
**#32157** | [Link](https://github.com/anomalyco/opencode/issues/32157) | 5 💬 | 67 👍
Users want explicit control over what happens to a prompt submitted mid-generation: queue (run next), steer (interrupt and redirect), or break. High 👍 (67) indicates this is not niche. This has been partially solved by the PR #40922 (queue prompts with Option+Enter) merged this week, but users want more nuance (the "break" option and compaction-aware semantics).

### 10. Bug: Web interface not auto-refreshing conversations
**#40502** | [Link](https://github.com/anomalyco/opencode/issues/40502) | 7 💬 | 0 👍
New messages don't appear in real-time in the web UI; manual refresh is required. This is a **fresh (07-04) bug** in the web client, likely introduced by a session-management refactor. Low traction yet, but if it persists it will escalate.

---

## Key PR Progress

### 1. feat(tui): queue prompts with Option/Alt+Enter
**#40922** | [Link](https://github.com/anomalyco/opencode/pull/40922) | Open
Makes Enter explicitly steer the active response; Option+Enter queues prompts into a compact dock attached to the composer. Directly addresses the #32157 feature request (queue vs steer). Adds a subtle but powerful interaction model for parallel work.

### 2. fix(llm): treat empty tool call identity in stream deltas as absent
**#40969** | [Link](https://github.com/anomalyco/opencode/pull/40969) | Open
Fixes streaming tool calls through OpenAI-compatible endpoints that send `id` as an empty string on continuation deltas (e.g., Alibaba DashScope). Currently the client throws `missing id or name`. This is a **provider-compat fix** important for users in the Asia-Pacific region who use Chinese providers.

### 3. refactor(core): simplify file tools to lexical paths
**#40962** | [Link](https://github.com/anomalyco/opencode/pull/40962) | Closed
Aligns V2 file tools with V1 behavior: resolve mutation paths lexically (not canonicalized through symlinks), list symlinks as directory entries, decode malformed UTF-8 with U+FFFD. This reduces surprising behaviors when editing symlinked files and avoids "file not found" errors for broken symlinks. Likely to fix several edge-case file bugs.

### 4. feat(core): add workspace environment foundation
**#40967** | [Link](https://github.com/anomalyco/opencode/pull/40967) | Open
Pure addition (nothing consumes it yet). Re-frames the execution model around an Effect-based `ChildProcessSpawner`, with drivers allowed to provide native fast-paths. **This is a foundational architectural change** for how OpenCode spawns processes (security, sandboxing, performance) — worth watching.

### 5. fix(tui): dismiss stale permission prompts
**#40960** | [Link](https://github.com/anomalyco/opencode/pull/40960) | Closed
Ensures TUI permission prompts are removed from local state once the server reports the request no longer exists (`PermissionNotFoundError`). Fixes the **annoying stale prompt bug** where user gets a "permission expired" error on a prompt that never existed.

### 6. fix(ai): preserve Responses item IDs
**#40943** | [Link](https://github.com/anomalyco/opencode/pull/40943) | Open
For provider-hosted output items on OpenAI/Azure Responses API: preserve item IDs and replay complete items instead of synthesizing item references. This improves **conversation continuity** when using the Responses API as a backend, reducing duplicate or wrong-turn history.

### 7. fix(ai): support streams without finish reasons
**#40965** | [Link](https://github.com/anomalyco/opencode/pull/40965) | Open
Adds `compatibility.requireFinishReason` (default `true`). When `false` and a stream ends cleanly without finish reasons, synthesize an `unknown` terminal finish. **Fixes a permissive-endpoint compatibility bug** that currently causes aborted streams on some providers.

### 8. feat(core): bound tool output
**#40929** | [Link](https://github.com/anomalyco/opencode/pull/40929) | Open
Adds configurable line/byte limits for tool text output (truncation with retained full text in managed files for 7 days). This is **a hard cap on runaway tool output** (e.g., file reads of huge logs) that can flood the context window and blow token limits. Highly practical.

### 9. fix(session): restart the loop for queued input stranded by an interrupt
**#40956** | [Link](https://github.com/anomalyco/opencode/pull/40956) | Open
Fixes: interrupting a turn (Esc or abort) **silently drops queued user messages**. This PR restarts the session loop to pick up stranded queued input. Bug is from the new queue feature flagged in the #32157 request — good that a fix is landing fast.

### 10. fix(tui): keep model selection session-scoped
**#40913** | [Link](https://github.com/anomalyco/opencode/pull/40913) | Closed
Model choice is now per-session instead of global agent-level state. Switching tabs restores each session's durable model/variant. **This is a UX quality-of-life fix**: users switching between long-running sessions (frontend vs backend vs analysis) no longer accidentally use the wrong model.

---

## Feature Request Trends

1. **Session Context Transparency & Visibility**
   Top request (#6152, 129 👍): TUI dialog showing exactly what's in the context window (tokens, source: file contents, tool outputs, messages). Users are flying blind with long-context models (1M+ tokens) and want to understand why context is used up. Related: #38973 (search session contents from pickers), #31932 (cross-project session picker).

2. **Mid-run Prompt Semantics (Queue vs Steer vs Break)**
   #32157 (67 👍) plus the merged PR #40922. Users want deliberate control over concurrent input: queue for later, steer to redirect the active turn, or break. The current behavior is often "accidental interrupt". PR #40922 covers the queue part; users still want the break and "steer with compaction awareness" behaviors.

3. **Session Management as a First-Class Concept**
   Multiple requests: cross-project session picker (#31932), searchable session contents (#38973), session stats by directory (#37760). Users want to treat OpenCode sessions as durable artifacts (similar to tmux sessions), not ephemeral conversations.

4. **Privacy & Attribution Transparency**
   #39875 (44 👍): Users are scrutinizing what happens to their data when using hosted subscription plans (Go/Zen). They want clear provider attribution (which upstream provider is used), telemetry disclosure, and retention policies. This will only grow as OpenCode's SaaS products mature.

5. **Desktop/TUI Ergonomics**
   #1168 (119 👍, clickable links) remains the top "polish" request. Low-hanging fruit that would dramatically improve daily usability.

---

## Developer Pain Points

1. **Subscription / Auth Instability (CRITICAL)**
   The "Request blocked by upstream provider" 401 is the dominant theme: 10+ open issues, 100+ cumulative comments, ~50 👍. Users report:
   - Both Go and Zen plans affected.
   - Direct provider keys work fine — isolates the problem to OpenCode's relay.
   - No public acknowledgement from maintainers yet, despite 2+ weeks.
   This is **eroding trust in the paid plans** and will drive users to BYOK (bring-your-own-key) models unless fixed quickly.

2. **Billing / Account Sync Failures**
   #40234 (new user subscription not activated) highlights a second pain point: the web billing system and the client do not stay in sync after payment. New users get stuck in a loop (no payment method => resubscribe => still broken).

3. **Windows / Linux Terminal Rendering Issues**
   #11748 (PowerShell garble after exit) and #35494 (Debian TUI freeze requiring kill -9) remain open. Linux/Windows users face suboptimal terminal experiences. The TUI freeze on Debian (XFCE/X11) has had **no recent maintainer attention** despite it being a hard blocker for those users.

4. **Model Metadata Inaccuracies**
   #40958 (DeepSeek V4 Flash Free shows 200K context instead of 1M) suggests **model metadata is not always accurate**, leading users to pick models below their actual capabilities. This is a "data quality" issue that silently reduces user productivity.

5. **Session State Loss on Interrupt**
   #40759 (closed) + #40956 (fix PR landed) show that interrupting a turn could drop or wipe queued input. The bug caused significant churn ("wipe the chat history"), and the community reacted strongly on the PR against it.

6. **Permission System Footguns**
   #40945: `permission.edit` rules are matched against worktree-relative paths, so absolute-path or `~` patterns silently never match — **fail-open for deny rules** (a security problem, e.g., `"~/.ssh/**": "deny"` would not work). While not yet hot, this is a security-relevant bug that maintainers should prioritize before users get burned.

---

*This digest aggregates the top 30 issues by comment count and 20 PRs updated within the last 24 hours for the anomalyco/opencode repository.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-07

## 1. Today's Highlights

The release of **v0.84.0** introduces the long-awaited Fullscreen TUI mode, enabling runtime mode switching with sticky editor, independent transcript scrolling, and draggable scrollbars. Community attention is focused on two critical bugs: the **auto-compaction failure** (Issue #6879, 👍15) that causes context overflow until API rejection, and the **TUI crash on over-wide lines** (#7736, #7737) which takes down the entire process with an uncaught exception. The PR landscape is active with 31 PRs in the last 24h, including fullscreen selection fixes (#7721, #7733), Ollama Cloud provider support (#7742), and SQLite session storage optimizations (#7727).

## 2. Releases

**v0.84.0** — Fullscreen TUI mode is the headline feature:
- Switch between regular and fullscreen modes at runtime
- Sticky editor and footer
- Independently scrollable transcript
- Draggable scrollbars

*Note: Several new-day bugs have been reported against this release, particularly TUI crash on wide lines (#7736, #7737) and tool-result rendering failure (#7695).*

## 3. Hot Issues

**#6879 — auto-compaction never triggers past 100% until provider overflow** (👍15, 12 comments, OPEN)  
Most-voted issue this week. A 2-hour agentic session on gpt-5.6-sol grew past compaction threshold to 373k tokens before API rejection. Community strongly agrees compaction should be checked after **every** agentic turn, not only at conversation boundaries.  
[GitHub Link](https://github.com/earendil-works/pi/issues/6879)

**#7547 — How do you use Pi on Windows?** (22 comments, OPEN)  
Major discoverability thread on Windows usage patterns. Author asks the community to self-report run-methods (WSL, MSYS2, native build, etc.) to focus core-team attention on the highest-impact paths.  
[GitHub Link](https://github.com/earendil-works/pi/issues/7547)

**#7128 — New PI_* guideline over-encourages unnecessary bash calls** (👍5, 10 comments, OPEN)  
Default system-prompt guideline to "Inspect PI_* environment variables" biases agents toward frequent `env` shell calls even when irrelevant. Community reports measurable token waste; suggestion is to scope the guidance to model/session setup moments only.  
[GitHub Link](https://github.com/earendil-works/pi/issues/7128)

**#7736 — Uncaught exception when exceeded terminal width** (3 comments, CLOSED)  
Latest-version crash: `Rendered line 409 exceeds terminal width (76 > 74)`. This is a fatal error in production; several users hit it with long lines from streaming markdown/JSON output.  
[GitHub Link](https://github.com/earendil-works/pi/issues/7736)

**#7702 — DeepSeek 400: reasoning_content must be passed back** (4 comments, OPEN)  
Multi-turn tool-call conversations via opencode zen gateway fail because `detectCompat()` doesn't echo `reasoning_content` on follow-ups. Blocking for DeepSeek users on that gateway.  
[GitHub Link](https://github.com/earendil-works/pi/issues/7702)

**#7413 — Compaction fails on GitHub Copilot GHE.com accounts** (7 comments, CLOSED)  
Enterprise `GHE.com` users can't run `/compact` ("unknown stamp 'prod-cus-01'" on summarization). Normal chat works; only compaction breaks, affecting long-session workflows in enterprises.  
[GitHub Link](https://github.com/earendil-works/pi/issues/7413)

**#7600 — pi-coding-agent leaks X11 connections** (3 comments, OPEN)  
Long-running processes leak 182 X server connections over ~8 days, eventually hitting Xorg's 256-client limit ("Maximum number of clients reached") and blocking **all** new X clients system-wide. High severity for Linux GUI users.  
[GitHub Link](https://github.com/earendil-works/pi/issues/7600)

**#7321 — Multi-line paste broken on terminals without bracketed paste** (👍1, 3 comments, OPEN)  
Termux (Android) and similar terminals: first `\r` submits instead of inserting a block. Root-cause identified: no bracketed-paste negotiation fallback.  
[GitHub Link](https://github.com/earendil-works/pi/issues/7321)

**#7674 — Qwen Token Plan (CN) model list out of sync** (3 comments, CLOSED)  
The built-in model list shows models (e.g. `MiniMax-M2.5`, `deepseek-v3.2`) that the CN API doesn't actually serve, while `deepseek-v4-flash-0731` is real but unlisted. Causes confusing selection failures.  
[GitHub Link](https://github.com/earendil-works/pi/issues/7674)

**#7691 — Anthropic login over SSH redirects to localhost** (4 comments, CLOSED)  
On headless Linux over SSH, `/login anthropic` redirects to `localhost` on the remote box instead of offering a copyable code; the Mac browser can't reach it. A login-flow dead-end for remote-headless users.  
[GitHub Link](https://github.com/earendil-works/pi/issues/7691)

## 4. Key PR Progress

**#7742 — feat(ai): Ollama Cloud support** (OPEN)  
Adds Ollama Cloud as first-class provider using `OLLAMA_API_KEY`, with manual login fallback and hybrid local/cloud via `ollama launch pi`. Follows existing provider patterns; uses models.dev model list.  
[GitHub Link](https://github.com/earendil-works/pi/pull/7742)

**#7721 — fix(tui): avoid unwanted newlines when copying in fullscreen** (CLOSED)  
Fixes wrapped-line copying: previously each visual row became a separate line on paste. Now tracks row boundaries so wrapped text pastes as the original unwrapped content.  
[GitHub Link](https://github.com/earendil-works/pi/pull/7721)

**#7717 — fix(agent): reject reset during active runs** (CLOSED)  
Directly addresses Issue #7703: `Agent.reset()` during an active run cleared the transcript but left the run unsettled, producing assistant-only transcripts. Now reset is rejected until the in-flight response settles; regression tests added.  
[GitHub Link](https://github.com/earendil-works/pi/pull/7717)

**#7710 — feat(agent): restore suspended harness operations** (OPEN)  
Implements R3 of harness v2: creates AgentHarness from existing sessions with the saved local state, restoring suspended/recoverable operations — the foundation for long-lived agent sessions.  
[GitHub Link](https://github.com/earendil-works/pi/pull/7710)

**#7727 — fix: sqlite queries optimizations** (OPEN)  
Improves remaining SQLite session-storage hot paths: branch queries push type/cursor/limit into SQL, `stopAtType` uses cached branch types, and a covering index for branch membership lookups. Meaningful latency wins for large sessions.  
[GitHub Link](https://github.com/earendil-works/pi/pull/7727)

**#7715 — feat(agent): allow blocked tool calls to terminate** (CLOSED)  
Implements Issue #5998: extensions that block a tool call via `beforeToolCall` can now hint `terminate: true` to end the agent's turn. Preserves batch rule that all blocked results must agree; regression coverage added.  
[GitHub Link](https://github.com/earendil-works/pi/pull/7715)

**#7686 — feat(coding-agent): add configurable Harness factory** (CLOSED)  
Internal factory for constructing the experimental Harness: preserves caller-provided tools, activation, prompt policy, and options; attaches prompt metadata to built-in tools and rebuilds prompts from current active tools; keeps bash session environment.  
[GitHub Link](https://github.com/earendil-works/pi/pull/7686)

**#7685 — fix(coding-agent): disable bunfig autoload in compiled binaries** (CLOSED)  
Bun-compiled standalone binaries were autoloading cwd `bunfig.toml` (running `preload`) before any Pi code — a broken preload could crash even `pi --version`. Release binaries now compile with `--no-compile-autoload`.  
[GitHub Link](https://github.com/earendil-works/pi/pull/7685)

**#7718 — fix(tui): preserve scrollback on content-driven full redraws** (CLOSED)  
Fixes scrollback loss when a rendered line above the viewport changes (e.g. streaming markdown reflow), which previously wiped the user's scroll position and pushed them back to the bottom.  
[GitHub Link](https://github.com/earendil-works/pi/pull/7718)

**#7681 — Support AGENTS.override.md as a per-directory context override** (CLOSED)  
Adds `AGENTS.override.md` as the highest-priority per-directory context file; when both `AGENTS.override.md` and `AGENTS.md`/`CLAUDE.md` exist, only the override loads. Enables project-specific context without editing shared files.  
[GitHub Link](https://github.com/earendil-works/pi/pull/7681)

## 5. Feature Request Trends

- **Provider breadth & parity** — Consistent theme across issues/PRs: Ollama Cloud (#7742), Amazon Bedrock Mantle (#6216, OPEN since July), LLM Gateway and DevPass (#7610), Qwen Token Plan Individual (#7659). Community actively needs more enterprise/cloud gateway options with proper auth flows (SSO, GCP metadata, GHE.com).

- **Fullscreen TUI customization** — New fullscreen mode in v0.84.0 spawns follow-ups: disable select-to-copy on highlight (#7720), double-click word selection (#7725), half-page scroll keybindings (#7735), theme overrides (#7722), and selection-aware pageUp/pageDown (#7680). Expect the next several releases to harden this new UI surface.

- **Agent lifecycle control** — PRs on reset-during-run rejection (#7717), blocked-tool termination hints (#7715), and harness v2 restore-from-session (#7710) point toward a future where Pi agents are resumable, controllable mid-run, and safe from state corruption — the "harness v2" plan is the north star here.

- **Session/context observability** — The compaction bug (#6879) and SQLite query optimizations (#7727) share a root goal: make large sessions predictable and fast. Users want transparent context accounting (when compaction triggers, why) and performant storage at scale.

## 6. Developer Pain Points

- **Context overflow & compaction unreliability** — The single most-voted topic (#6879). Compaction only fires at the API boundary, not when the context crosses the threshold mid-agent-turn. Costs users real tokens and failed runs. Related: compaction itself breaks on Copilot GHE.com (#7413).

- **TUI instability in the new release** — Multiple distinct crashes on v0.84.0: fatal `uncaughtException` on over-wide lines (#7736, #7737), tool-result rendering crash on undefined content (#7695), infinite recursion from the interactive TUI reference Proxy (#7743). For a TUI-first tool, process-killing rendering errors are severe; several already closed as regressions.

- **Headless/remote workflow gaps** — SSH users hit broken OAuth (localhost redirect, #7691) and missing bracketed-paste fallback (#7321). X11 session leaks (#7600) penalize long-running Linux GUI sessions. These collectively hurt the "Pi everywhere" story.

- **Config drift between environments** — Issues around stale model lists (#7674), cross-instance model leakage (#7677), and `bunfig.toml` autoload crashing binaries (#7685) all trace to one theme: Pi behaves differently depending on environment/my-machine state, and users want deterministic, inspectable configuration.

- **Provider-specific quirks accumulating** — DeepSeek `reasoning_content` passthrough (#7702), GLM prompt-cache 400s on Fireworks (#7676), and the PI_* env guideline over-triggering bash (#7128) show a pattern: each provider has corner cases that Pi adapters either miss or overfit, and users are catching them in production.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest - 2026-08-07

## Today's Highlights

Qwen Code v0.21.7 shipped with the removal of the 50-turn limit for Goals and inline terminal image rendering in the interactive CLI. The community is actively reporting and fixing critical regressions, including hook dispatch failures in 0.21.6 and multiple security issues around folder trust evaluation and shell command classifier bypasses. The team is also expanding ecosystem integrations with voice frontends and new documentation languages.

## Releases

**v0.21.7** ([Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.7))
- Removed the 50-turn limit for Goals, allowing tasks to resume beyond previous boundaries ([#8421](https://github.com/QwenLM/qwen-code/pull/8421))
- Enabled inline terminal image rendering from model outputs in the interactive CLI for kitty/iTerm2/WezTerm/Ghostty/Warp terminals ([#8090](https://github.com/QwenLM/qwen-code/issues/8090))

**v0.21.7-nightly.20260807.fca8f3c1f** ([Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.7-nightly.20260807.fca8f3c1f))
- CI fix: surface blocked autofix takeover admission ([#8410](https://github.com/QwenLM/qwen-code/pull/8410))

**live-host-v0.1.0** ([Release](https://github.com/QwenLM/qwen-code/releases/tag/live-host-v0.1.0))
- Qwen Live Host v0.1.0 with Windows merge queue CI tests and evidence-image tooling for GitHub review

**live-host-latest** - Stable Qwen Live Host installer feed

## Hot Issues

1. **[#3203](https://github.com/QwenLM/qwen-code/issues/3203) — Qwen OAuth Free Tier Policy Adjustment** (CLOSED, 150 comments)  
   Community pushback on proposed reduction of daily free quota from 1,000 to 100 requests. The high engagement indicates strong reliance on the free tier.

2. **[#8622](https://github.com/QwenLM/qwen-code/issues/8622) — Hooks regression in 0.21.6** (OPEN, 5 comments)  
   PreToolUse/PostToolUse/PreCompact/SessionStart hooks never dispatched in 0.21.6—critical regression for automation-users. Gated tool execution is silently skipped.

3. **[#8615](https://github.com/QwenLM/qwen-code/issues/8615) — Desktop 0.1.0 Windows crash: EISDIR on workspace open** (OPEN, P1, 5 comments)  
   Bundled runtime crashes on Windows with `EISDIR lstat 'C:'`—blocks all Windows desktop users.

4. **[#8582](https://github.com/QwenLM/qwen-code/issues/8582) — Read-only shell classifier bypass** (OPEN, P1, 5 comments)  
   Command substitution hidden by line continuation or `\${var@P}` auto-approved. Security-critical issue for sandboxed environments.

5. **[#8627](https://github.com/QwenLM/qwen-code/issues/8627) — DO_NOT_TRUST loses to ancestor TRUST_FOLDER** (OPEN, P2, 3 comments)  
   Untrusted workspaces can inject bearer tokens via ancestor trust rules. Trust model needs rework for explicit distrust precedence.

6. **[#8316](https://github.com/QwenLM/qwen-code/issues/8316) — Prompt lost after Ctrl+C** (OPEN, 8 comments)  
   Cancelled prompts are not restored to input box—frustrating for iterative prompt refinement workflows.

7. **[#8557](https://github.com/QwenLM/qwen-code/issues/8557) — Terminal shrink duplicates transcript** (OPEN, P3, 6 comments)  
   macOS/Warp: shrinking terminal re-prints blocks into scrollback. Rendering bug affects long-session usability.

8. **[#6565](https://github.com/QwenLM/qwen-code/issues/6565) — "Internal Error" connecting to Qwen Coder** (CLOSED, 10 comments)  
   Authentication issue persisting for multi-language users; closed but with user impact across locales.

9. **[#8644](https://github.com/QwenLM/qwen-code/issues/8644) — Windows file links broken due to URL-encoded colon** (OPEN, P2, 3 comments)  
   VS Code fails to open `file:///d%3A/...` links. Windows-specific path handling needed.

10. **[#8643](https://github.com/QwenLM/qwen-code/issues/8643) — Trust evaluated once for start directory in fast path** (OPEN, 3 comments)  
    `.env` loading from untrusted ancestors exposes credential security risk in daemon mode.

## Key PR Progress

1. **[#8388](https://github.com/QwenLM/qwen-code/pull/8388) — capture-tui: pixel-based rendering claims (Phase 2)**  
   Verification via private tmux server screenshots for rendering claims in code reviews.

2. **[#8645](https://github.com/QwenLM/qwen-code/pull/8645) — Confirm read-only git commands executing repo config**  
   Whitelisted git sub-commands could execute repository-local config programs—security hardening.

3. **[#8631](https://github.com/QwenLM/qwen-code/pull/8631) — ACP agent fan-outs concurrent and past tool-call cap**  
   Fixes serialization and early termination of `/review` agent fan-outs—critical for CI review performance.

4. **[#8425](https://github.com/QwenLM/qwen-code/pull/8425) — Share compression cache with Gemini/Vertex AI**  
   Efficient provider-managed implicit caching for same-model compression requests.

5. **[#8320](https://github.com/QwenLM/qwen-code/pull/8320) — Cooperative pause/resume for Dynamic Workflows**  
   Scheduler gates dispatches during pause, holds results, and resumes cleanly.

6. **[#8646](https://github.com/QwenLM/qwen-code/pull/8646) — Load extension hooks from Claude/Gemini manifests**  
   Cross-provider hook compatibility—extends hook ecosystem beyond Anthropic format.

7. **[#8619](https://github.com/QwenLM/qwen-code/pull/8619) — Strip Windows verbatim prefix from workspace paths**  
   Replaces `std::fs::canonicalize` with `dunce::canonicalize` for Windows path safety.

8. **[#8578](https://github.com/QwenLM/qwen-code/pull/8578) — Feishu ask-user question cards**  
   Native Card V2 presentation with callback correlation—improves Feishu channel UX.

9. **[#8525](https://github.com/QwenLM/qwen-code/pull/8525) — Resolve Qwen 3.8 reasoning budget conflicts**  
   Prevents dual `reasoning_effort` + `thinking_budget` conflicts from different config layers.

10. **[#8654](https://github.com/QwenLM/qwen-code/pull/8654) — Repository context manifest for /review**  
    Declares bounded review domains and related-path scopes—improves automated review precision.

## Feature Request Trends

- **Channel integrations**: DingTalk interactive cards ([#8517](https://github.com/QwenLM/qwen-code/pull/8517)), Feishu ask-user cards ([#8578](https://github.com/QwenLM/qwen-code/pull/8578)), both actively developed
- **Voice/audio support**: qwen-audio-agent voice frontend proposal ([#8629](https://github.com/QwenLM/qwen-code/issues/8629)) signals multimodal interaction direction
- **Multimodal (Omni)**: S3 delivery reliability ([#8185](https://github.com/QwenLM/qwen-code/issues/8185)) and experimental roadmap ([#8197](https://github.com/QwenLM/qwen-code/issues/8197)) for file recognition
- **Documentation i18n**: Korean docs/README requested ([#8551](https://github.com/QwenLM/qwen-code/issues/8551))

## Developer Pain Points

- **Hook reliability**: 0.21.6 breakage of PreToolUse/PostToolUse/PreCompact hooks ([#8622](https://github.com/QwenLM/qwen-code/issues/8622)) undermines automation trust
- **Terminal rendering issues**: Recurring on Windows/WSL/tmux—duplicate output on resize ([#8557](https://github.com/QwenLM/qwen-code/issues/8557)), Chinese IME display ([#8625](https://github.com/QwenLM/qwen-code/issues/8625)), tmux flicker ([#8562](https://github.com/QwenLM/qwen-code/issues/8562))
- **Security/trust edge cases**: Multiple reports of trust folder bypasses and credential leakage ([#8627](https://github.com/QwenLM/qwen-code/issues/8627), [#8643](https://github.com/QwenLM/qwen-code/issues/8643))
- **Windows desktop stability**: Crash on startup ([#8615](https://github.com/QwenLM/qwen-code/issues/8615)) and file-link URL encoding ([#8644](https://github.com/QwenLM/qwen-code/issues/8644)) block daily Windows workflows
- **CI infra reliability**: `/review` timeouts ([#8597](https://github.com/QwenLM/qwen-code/issues/8597)) and E2E test failures ([#8647](https://github.com/QwenLM/qwen-code/issues/8647)) indicate test infrastructure needs investment

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-07

## 1. Today's Highlights

The command-boundary refactor reaches its final verification layer (Layer 5.3) with PR #5255, consolidating palette and slash-completion integration. Meanwhile, the v0.9.4 release train (#5135) continues to mature, with several UX bug fixes shipping — most notably the mouse-scroll fix for long content (#5234) and the subagent checkpoint resume feature (#5242). FreeBSD build support is also in progress (#5254), widening the platform reach.

---

## 2. Releases

No new releases in the last 24 hours. The v0.9.4 release train (#5135) is currently 77 commits ahead of `main` and remains in active integration — expected to land soon.

---

## 3. Hot Issues (10 Notable)

### #5244 — Unknown model IDs silently degrade to 128K legacy context
**Author:** Hmbown | **Status:** OPEN
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5244)
Residual class bug from #5239: models with 1M context windows are silently compacted to 128K when the ID isn't recognized, with no surfaced warning. The community is pushing for explicit fallback disclosure — a correctness issue that affects prompt quality across providers.

### #5253 — Nested subagent max_depth can widen root session depth budget
**Author:** cacdcaecawae | **Status:** OPEN
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5253)
A descendant subagent can escalate the global recursion budget beyond the operator's configured ceiling (MAX_SPAWN_DEPTH_CEILING = 8) by passing explicit `max_depth` on nested spawns. PR #3931 patched the ceiling but missed the escalation vector — a security/correctness concern for fleet deployments.

### #5250 — Only one API key saved across providers
**Author:** ffyuhf | **Status:** OPEN
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5250)
Users switching between DeepSeek and GLM must re-enter keys each time — a clear multi-provider workflow gap. The request: per-provider key storage instead of single-key overwrite.

### #5223 — Mouse wheel routed to input history, not content area
**Author:** wangdsen | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5223)
Long conversations could only be scrolled via terminal-native shortcuts; the wheel toggled composer history instead. Fixed by PR #5234 — but the issue highlights broader TUI scroll UX concerns.

### #4978 — Anthropic API error: `'type' must be in ["enabled", "disabled", "auto"]`
**Author:** w1w218 | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/issues/4978)
Frequent HTTP 400 errors when using OpenModel (Anthropic-compatible Messages API) — intermittent and non-deterministic, suggesting a race or stale config. Closed as resolved, but the pattern of provider-compatibility flakiness is concerning.

### #5178 — Admin digest "post" returns ok:true while posting nothing
**Author:** Hmbown | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5178)
A **false success** bug: the web admin digest endpoint acknowledged posting but the draft never published — a silent data-loss pattern that is severely damaging to trust. Worth auditing for similar "optimistic ack" patterns across the routing layer.

### #4681 — `<turn_meta>` blocks displayed when reopening session
**Author:** e792a8 | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/issues/4681)
Reopened sessions surface internal `<turn_meta>` blocks to the user, leaking agent-internal state. The fix must ensure metadata stays hidden on serialization round-trips.

### #5040 — Move persistent Workflow status to top status bar
**Author:** Hmbown | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5040)
Durable workflow state sat near the composer, consuming input space and reading like a lingering prompt. Moved to the top status bar — a UX clarity win for orchestration visibility.

### #5035 — Workflow authoring failures inconsistent and hidden by parallel fan-out
**Author:** Hmbown | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/issues/5035)
A dogfood run failed because `task(...)` rejected option names accepted by direct Agent dispatch — then the retry treated failed parallel slots as `null` and "completed successfully" with no children. Silent success masking failure is a **critical reliability bug** for workflow orchestration.

### #4828 — macOS: underwater shell breaks open/osascript/launchctl (exit code -54)
**Author:** zhiyuchen1101 | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/issues/4828)
The new "underwater" terminal shell causes macOS system commands to fail with operation-not-permitted errors. Downgrading to v0.8.67 resolved it — a regression that impacted shell interop on macOS.

---

## 4. Key PR Progress (10 Important)

### #5255 — Layer 5.3: Palette, completion, and discovery filtering
**Author:** aboimpinto | **Status:** OPEN
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5255)
The final verification layer of the staged command-boundary refactor — proving each acceptance criterion of the user-command integration in the palette and slash-completion surfaces that shipped in Layer 5.1.

### #5254 — FreeBSD build fix
**Author:** mky | **Status:** OPEN
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5254)
No rquickjs bindings exist for FreeBSD, breaking compilation. This PR adds a fallback path — a low-risk change that unblocks a new platform.

### #5234 — Fix: keep alternate scroll off while mouse capture active (#5223)
**Author:** SparkofSpike | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5234)
Root cause: `recover_terminal_modes()` armed both mouse capture and xterm alternate-scroll (DECSET), so wheel input toggled composer history instead of scrolling the transcript. Fix disables alternate scroll while mouse capture is active.

### #5242 — Resume interrupted children from checkpoint via followup
**Author:** SparkofSpike | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5242)
Previously, `followup` on an `interrupted_continuable` child queued a dead-letter — the checkpoint was preserved but unreusable. Long tasks (document review, multi-step search) could not resume mid-run. This PR wires the continuation path.

### #5240 — Surface real wait elapsed time in tool content
**Author:** SparkofSpike | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5240)
`duration_ms` was only in tool metadata — invisible to the model. Every wait looked identical, biasing the model into busy-polling short waits and misjudging long stalls. Exposing real elapsed time in tool output improves agent decision-making.

### #5238 — MCP Registry discovery with Registry-first tool selection
**Author:** bistack | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5238)
Before reaching for `exec_shell`, custom code, or manual implementation, the model now consults the public MCP Registry for a matching zero-environment stdio server. `registry_sync` fetches eligible servers — a step toward self-sufficient tooling.

### #5252 — Allow embedders to isolate runtime state roots
**Author:** cacdcaecawae | **Status:** OPEN
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5252)
Adds optional `EngineConfig::subagent_state_root` for embedding hosts that need session-owned delegated-agent state, while keeping child execution cwd, file authority, receipts, and the legacy state default unchanged.

### #5225 — Expose file/search/git/patch/shell tools over ACP session/prompt
**Author:** rafaelcavalheri | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5225)
Before: ACP `session/prompt` only streamed model text — tool calls were never executed, so editor bridges (Zed, `acp-deepseek-adapter`) got a chat-only agent. Now tool requests execute with real code-editing capability.

### #5077 — Progressively disclose fresh context (perf/prompt)
**Author:** Hmbown | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5077)
Keeps `AGENTS.md` / `CLAUDE.md` eager, caps the ambient skills block at 2,400 chars (with lazy skill bodies via `load_skill name="list"`), and moves session context to progressive disclosure — reducing token pressure.

### #5135 — v0.9.4 release train
**Author:** Hmbown | **Status:** CLOSED
[GitHub](https://github.com/Hmbown/CodeWhale/pull/5135)
The 77-commit integration train containing all 2026-08-01 source candidates plus 18 train commits. Supersedes #5044; anchors the v0.9.4 feature set.

---

## 5. Feature Request Trends

- **Multi-provider support (highest signal):** #5250 — per-provider API key storage. Directly impacts users juggling DeepSeek + GLM + others.
- **Better fallback transparency:** #5244 — when model capabilities are unknown, say so instead of silently degrading.
- **Workflow/agent observability:** #5040, #5035, #5240 — surfacing real runtime state (duration, status placement, failure visibility) so orchestration is auditable and trustworthy.
- **Platform reach:** #5254 — FreeBSD support (low-cost expansion).
- **Resilience and recovery:** #5242 — resuming interrupted long-running child tasks from checkpoints (repeated pain point).

---

## 6. Developer Pain Points

- **Silent failure / false success patterns:** Two separate issues surfaced endpoints or workflows that report `ok:true` while doing nothing (#5178 admin digest, #5035 workflow fan-out) — the highest-trust-damaging class of bug.
- **Context-window surprises:** #5244 — unknown models silently falling back to 128K instead of declaring the limit is a repeated tripwire.
- **Scroll and TUI input routing:** #5223 — wheel events fighting between content and composer history; resolved via #5234, but the underlying "mode capture" design remains fragile.
- **Rebuild costs on trivial commits:** #5245, #5246 — fat LTO on every pre-push build and a `git commit` forcing full rebuilds of 682K-line crates are actively harming contributor velocity. Both are closed, but the build-split and SHA-stamp decoupling changes deserve attention.
- **macOS shell interop regressions:** #4828 — the "underwater" shell breaking system commands is a sharp reminder that TUI shell abstraction can't break host OS tooling.
- **Anthropic-compatible API flakiness:** #4978 — intermittent HTTP 400 errors with `invalid_request_error` are hard to reproduce and debug; suggests shared validation state or timing-dependent config handling.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*