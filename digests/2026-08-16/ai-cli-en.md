# AI CLI Tools Community Digest 2026-08-16

> Generated: 2026-08-16 00:31 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Comparison Report — 2026-08-16

## 1. Ecosystem Overview

The AI CLI developer tools landscape is maturing rapidly, with seven major tools (Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI) showing distinct trajectories and community priorities. The ecosystem is characterized by two dominant themes: **reliability engineering** (session continuity, compaction, data integrity, and cross-platform stability) and **workflow integration** (MCP servers, persistent memory, workspace scoping, and headless/CI automation). Windows desktop stability remains the single largest cross-tool pain point, affecting Claude Code, Codex, and Pi users with crashes, stutters, and GPU-process failures. Meanwhile, feature demand is converging on session management (continuation, queuing, resumption) and context persistence (memory systems, cross-device sync), indicating that the core agentic loop is now expected to be reliable and stateful by default. Managed providers (OpenCode Go/Zen, Gemini) are under scrutiny for billing transparency and service reliability, while self-hosted users increasingly demand configurable budgets, sandboxing, and provider parity.

---

## 2. Activity Comparison

| Tool | Issues (Hot/Active) | PRs (Notable) | Releases (24h) | Distinct Signals |
|---|---|---|---|---|
| **Claude Code** | 50+ updated; 10 hot (top: 197👍 session continuation, 197👍 message queue) | 3 notable (1 merged/closed) | None | Windows GPU crashes dominant; session/queue requests lead |
| **OpenAI Codex** | 10 hot (top: 85👍 Windows stutter; 79👍 workspace scope) | 10+ merged (storage diagnostics, MCP hooks, pagination fixes) | 2 alphas (rust-v0.148.0-alpha.19/20) | Active engineering; Windows perf and disk bloat top issues |
| **Gemini CLI** | 10 hot (P1: subagent false success, generalist hangs) | 10 active (SSRF fix, subagent recovery, sandbox upgrade) | 1 nightly (v0.56.0) | Subagent reliability and security hardening focus |
| **GitHub Copilot CLI** | 10 hot (NixOS bash break, Atlassian OAuth regressions) | 2 (1 open, 1 closed) | None | Auth/MCP integration recurring regressions; NixOS blocked |
| **Kimi Code CLI** | 5 hot (memory system, token allowance drop) | 2 (1 open, 1 closed) | None | Memory system unmet; billing transparency concern |
| **OpenCode** | 10 hot (billing sync, grok-4.5 outage, Plan→Build auto-switch 31👍) | 10 notable (session budget, Docker/Incus workspaces) | None | Managed provider instability; workspace isolation push |
| **Pi** | 10 hot (compaction never triggers, Windows taskkill self-kill) | 10 active (compaction boundaries, Mermaid upgrade, token accounting) | None | Compaction and token accounting dominate; Windows safety gap |
| **Qwen Code** | 10 hot (review infrastructure, IME broken, CI flakiness) | 10 active (worktree leases, flakiness gate, content-anchored reviews) | 1 nightly (v0.21.11) | Self-healing CI and review pipeline hardening |
| **DeepSeek TUI** | 10 hot (SSE UTF-8 garbling, CI red, web UI broken) | 10 active (provider templates, budgets, security fixes) | None | CI stabilization wave; macOS-specific bugs; i18n care |

---

## 3. Shared Feature Directions

The following requirements appear across multiple tools, indicating strong cross-community demand:

### 3.1 Session Continuation and Message Queuing
- **Claude Code**: #13354 (197👍) explicit "continue" at session limit; #50246 (197👍) queue follow-up messages.
- **Gemini CLI**: #22323 false "success" on MAX_TURNS — subagent recovery needs honest status.
- **Pi**: #6879 auto-compaction failing to trigger until provider overflow; #8168 role corruption after restore.
- **Qwen Code**: #9153 resume support for `/review`; #9190 content-anchored incremental rounds.
- **Signal**: Users expect long-running tasks to survive session boundaries, queue messages safely, and resume without data loss or misleading status. This is the ecosystem's #1 reliability gap.

### 3.2 Persistent Memory and Cross-Device State Sync
- **Kimi Code CLI**: #1283 (40 comments) persistent memory layer; #1478 memory optimization.
- **Claude Code**: #87027 account-level sync for config/auto-memory; #87028 context path between claude.ai and CLI.
- **Gemini CLI**: Memory retries and redaction concerns (#26522, #26525).
- **Signal**: Memory is the next frontier — users want their setup and context to "follow the login" across machines and sessions, not live only in local files.

### 3.3 Workspace/Project-Scoped Sessions
- **OpenAI Codex**: #3550 (79👍) scope chats to VS Code projects.
- **Pi**: #8177 exclusive writers for resumed JSONL sessions.
- **OpenCode**: #42831/#42829 Docker/Incus workspace isolation for subagents.
- **Signal**: Developers want per-project isolation, reproducible environments, and clear boundaries between concurrent workstreams.

### 3.4 Configurable Budgets and Timeouts
- **Pi**: #8146 output caps; #8174 length-stop messaging; #8165 token accounting.
- **OpenCode**: #42823 per-session budget limit.
- **Copilot CLI**: #4421 configurable MCP handshake timeout with retry.
- **Claude Code**: #74567 scoped-write permission mode for CI.
- **Signal**: Users demand fine-grained control over token spend, resource limits, and timeout behavior — especially for headless and CI workloads.

### 3.5 Headless/Automation Reliability
- **Claude Code**: #86986 `setup-token` 400 rejection; #74567 `dontAsk` denies Write.
- **Copilot CLI**: #4346 MCP registry 403 in CI; #4499 OOM in autopilot.
- **OpenAI Codex**: #38774 paginated history for `exec` persistent threads.
- **Signal**: Unattended agents and CI pipelines are growing use cases, but permission modes, token auth, and session persistence are not yet battle-tested.

### 3.6 Provider Interop and Transparency
- **Kimi Code CLI**: #1155 `openai_legacy` reasoning content drop.
- **Pi**: #8105 optional tool params materialized as required; #8181 model-specific thinking levels.
- **Gemini CLI**: #28828 silent preview-model substitution.
- **OpenCode**: #37790 "Insufficient balance" despite successful payment.
- **Signal**: Tool-makers must validate provider integrations beyond the documented API — users are hitting subtle, costly interop bugs and want clear indication of what model/provider actually ran.

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target Users | Technical Approach |
|---|---|---|---|
| **Claude Code** | Session continuity, Windows stability, hooks | Enterprise teams, long-running complex tasks | TUI-first; hooks/plugins system; permission modes; desktop app (Electron) |
| **OpenAI Codex** | Reliability under load, storage hygiene, MCP integration | Heavy automation users, API-heavy workflows | Rust core; `exec` headless mode; Guardian permission approvals; storage diagnostics |
| **Gemini CLI** | Subagent orchestration, security (SSRF), sandboxing | Developers using Gemini 3 models; security-conscious | JS/Node; nightly releases; A2A subagent protocol; Docker sandbox upgrades |
| **GitHub Copilot CLI** | MCP integration, CI/CD workflows, GitHub ecosystem | GitHub-centric developers, Codespaces users | Node; ACP support; MCP registry governance; model catalog management |
| **Kimi Code CLI** | Persistent memory, subscription transparency | Moonshot Kimi users; long-session heavy users | Go; openai-compatible providers; K3 1M-token window; memory roadmap |
| **OpenCode** | Managed provider (Go/Zen) reliability, billing UX | Users of managed AI services; TUI/desktop users | TypeScript; Go/Zen providers; per-session budgets; Docker/Incus isolation |
| **Pi** | Compaction correctness, provider parity, TUI polish | Self-hosters; multi-provider power users | Rust; multi-provider support (xAI, DeepSeek, etc.); Mermaid rendering; extension system |
| **Qwen Code** | Automated review pipeline, CI self-healing | Qwen/self-hosted users; CI-heavy teams | Node; `/review` infrastructure; worktree leases; flakiness gates |
| **DeepSeek TUI** | i18n (Chinese), macOS/Windows parity, web/TUI parity | DeepSeek users; Chinese-speaking developers | Rust TUI + web companion; provider templates; cross-platform CI hardening |

**Key Distinctions**:
- **Claude Code** and **OpenCode** lean heavier on managed/desktop experiences; **Pi**, **Qwen Code**, and **DeepSeek TUI** are more self-hosted/community-driven.
- **Gemini CLI** and **OpenAI Codex** are iterating fastest on security and infrastructure (SSRF fixes, sandboxing, storage diagnostics), reflecting Google/OpenAI engineering velocity.
- **Kimi Code** and **DeepSeek TUI** show strong localization dynamics (Chinese IME, i18n debates), indicating geographic community splits.
- **Pi** is the most "power-user utility" — multi-provider, extension-heavy, TUI-focused — while **Qwen Code** is narrowing on review automation as a flagship feature.

---

## 5. Community Momentum & Maturity

| Tool | Momentum | Maturity | Signal |
|---|---|---|---|
| **OpenAI Codex** | ⬆️⬆️⬆️ | High — 20+ PRs merged in 24h, active release train | Most rapidly iterating; engineering velocity high; community engaged on reliability |
| **Claude Code** | ⬆️⬆️ | High — mature feature set, but issues dominate | Slow release cadence (none in 24h) but high community expectation; two 197👍 feature requests indicate strong latent demand |
| **Gemini CLI** | ⬆️⬆️ | Medium-high — nightly releases, security focus | Actively fixing subagent reliability; security (SSRF) and sandbox upgrade show responsible engineering |
| **Copilot CLI** | ⬆️ | Medium — regression-prone releases | Community vocal on auth/MCP regressions; NixOS and Codespaces staleness point to update-path fragility |
| **Pi** | ⬆️⬆️ | Medium-high — compaction and TUI polish | Steady PR flow; long-running issues (#6879 17👍) indicate trust in the project but unresolved pain |
| **OpenCode** | ⬆️ | Medium — billing/provider issues top-heavy | Managed-provider instability is hurting trust; feature work (budgets, isolation) is positive but overshadowed |
| **Kimi Code CLI** | ⬆️ | Low-medium — small community but engaged | Memory system is the #1 ask; token-allowance drop report is a red flag for transparency |
| **Qwen Code** | ⬆️ | Medium — self-hosted/CI hardening | Active self-healing CI investment; review infrastructure is becoming a differentiator |
| **DeepSeek TUI** | ⬆️ | Medium — CI stabilization wave | Active but small community; i18n care and macOS parity are unique strengths |

**Maturity Ranking (rough)**: Claude Code ≈ OpenAI Codex > Pi > Copilot CLI ≈ Gemini CLI > OpenCode > Qwen Code > DeepSeek TUI > Kimi Code CLI

---

## 6. Trend Signals

What the community is telling the industry:

### 6.1 Reliability Is the New Feature
The #1 cross-tool signal: users want the agentic loop to be **dependable**. Session continuation, honest subagent status, compaction that actually triggers, data-integrity on resume, and cross-platform stability are not "nice-to-haves" — they are the gating factors for production adoption. Tools that fail silently (Claude Code's truncation, Codex's disk bloat, Pi's role corruption) are eroding trust fastest.

### 6.2 Windows Desktop Is a First-Class Platform, Not an Afterthought
Four of nine tools report Windows-specific failures (Claude Code GPU crashes, Codex stutter, Pi taskkill self-kill, DeepSeek TUI CI failures). As AI CLIs move from terminals to desktop apps, Windows users are a large and vocal cohort. Tools that ignore Windows parity will lose share in enterprises where Windows is the standard.

### 6.3 Managed Providers Must Be Transparent and Predictable
Billing surprises (OpenCode "Insufficient balance", Kimi token-allowance drop), silent model substitution (Gemini), and provider-API outages (grok-4.5) are trust-killers. Users want clear entitlement sync, explicit cache pricing (Bedrock), and honest error messages. "Free" claims without model-level qualification generate more friction than goodwill.

### 6.4 Memory and Context Are the Next Battleground
Kimi's memory request, Claude Code's account-level sync, and Pi's compaction efforts all point in one direction: **stateful agents**. The user's setup, project patterns, and preferences should persist across sessions and machines. The tool that cracks persistent, privacy-aware, cross-device memory will have a durable advantage.

### 6.5 Automation and CI Are Accelerating Demand for Headless Mode
`dontAsk` permission bugs, `setup-token` 400s, MCP handshake timeouts, and autopilot OOMs all signal that **headless/CI is a growing, underserved use case**. As AI CLI tools move into pipelines and unattended agents, permission modes, long-lived tokens, and session replay must be first-class citizens — not afterthoughts.

### 6.6 Security Is Moving from "Nice-to-Have" to "Table Stakes"
SSRF fixes (Gemini), sandbox upgrades (Gemini), GHSA preparation (DeepSeek TUI), and false-positive safety-block corrections (Claude Code) show that both tools and users are taking security seriously. The next wave of adoption will require provable isolation, redaction before model transmission, and deterministic permission enforcement.

### 6.7 Self-Hosters Want Configurability, Not Just Features
Long-context self-hosted users (Pi, Qwen, DeepSeek) are demanding configurable read/tool-result budgets, provider-specific caps, and honest token accounting. These users are sensitive to cost and correctness; tools that give them control will retain them as advocates.

---

**Bottom Line for Decision-Makers**:
- **Invest in reliability** (session continuity, compaction, data integrity) before adding features.
- **Treat Windows desktop as a top-tier platform**, not a secondary target.
- **Provide transparent billing, explicit model selection, and honest failure states.**
- **Build memory and context persistence as core architecture**, not optional plugins.
- **Design for headless/CI from day one** with tested permission modes and long-lived tokens.
- **Watch OpenAI Codex and Gemini CLI** — they are iterating fastest on exactly the dimensions (storage hygiene, security, subagent honesty) that will define the next generation of developer trust.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

**Data as of 2026-08-16 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following PRs have attracted the most community attention and discussion. Note that all currently remain **open** — none have been merged as of this data snapshot.

### #1 — Bug Fix: `run_eval.py` Reports 0% Recall ([PR #1298](https://github.com/anthropics/skills/pull/1298))
**Author:** MartinCajiao | **Created:** 2026-06-10 | **Status:** Open
**Functionality:** Fixes the `skill-creator` evaluation pipeline — the core issue (also tracked in [Issue #556](https://github.com/anthropics/skills/issues/556), with 10+ independent reproductions) is that `run_eval.py` always reports `recall=0%` for every skill description, meaning the description-optimization loop is "optimizing against noise." The fix installs the eval artifact as a real skill, and addresses Windows stream reading, trigger detection, and parallel workers.
**Discussion highlight:** This is the single most impactful bug in the skill-creator workflow — it renders the auto-optimization loop effectively useless. Multiple contributors (gstreet-ops, joshuawowk, dthau120391) have submitted complementary fixes ([PR #1050](https://github.com/anthropics/skills/pull/1050), [PR #1099](https://github.com/anthropics/skills/pull/1099)), making this a coordinated community effort.

### #2 — Document Typography Skill ([PR #514](https://github.com/anthropics/skills/pull/514))
**Author:** PGTBoos | **Created:** 2026-03-04 | **Status:** Open
**Functionality:** A skill for typographic quality control in AI-generated documents — prevents orphan word wrap, widow paragraph headers, and numbering misalignment.
**Discussion highlight:** Addresses a universal pain point: these formatting issues affect every document Claude generates, yet users rarely request fixes explicitly. Direct complement to the existing `docx` and `pdf` skills.

### #3 — ODT Skill (OpenDocument Text) ([PR #486](https://github.com/anthropics/skills/pull/486))
**Author:** GitHubNewbie0 | **Created:** 2026-03-01 | **Status:** Open
**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods) — filling a major gap in the document-format coverage (DOCX, PDF exist; ODT does not). Includes template filling and ODT-to-HTML conversion.
**Discussion highlight:** Fills an obvious ecosystem gap for LibreOffice/open-source users; complements the existing `docx` and `pdf` skills.

### #4 — Frontend-Design Skill Clarity Overhaul ([PR #210](https://github.com/anthropics/skills/pull/210))
**Author:** justinwetch | **Created:** 2026-01-05 | **Status:** Open
**Functionality:** Revises the frontend-design skill for clarity, actionability, and internal coherence — ensuring every instruction is executable within a single conversation.
**Discussion highlight:** Reflects a broader community trend: existing skills are too verbose/educational and need to be rewritten as operational, action-oriented instructions (see also [Issue #202](https://github.com/anthropics/skills/issues/202), which criticizes `skill-creator` for the same problem).

### #5 — Self-Audit Skill (Mechanical + Reasoning Quality Gate) ([PR #1367](https://github.com/anthropics/skills/pull/1367))
**Author:** YuhaoLin2005 | **Created:** 2026-06-28 | **Status:** Open
**Functionality:** A universal skill that audits AI output before delivery — first mechanical file verification (every claimed output exists), then a four-dimension reasoning audit in damage-severity priority order. Works with any project, stack, or model.
**Discussion highlight:** Companion proposal in [Issue #1385](https://github.com/anthropics/skills/issues/1385) outlines a three-gate pipeline: Pre-task Calibration → Adversarial Review → Delivery Verification. Novel meta-skill category.

### #6 — Testing-Patterns Skill ([PR #723](https://github.com/anthropics/skills/pull/723))
**Author:** 4444J99 | **Created:** 2026-03-22 | **Status:** Open
**Functionality:** Comprehensive testing skill covering the Testing Trophy philosophy, unit testing (AAA pattern, naming, edge cases), React component testing, and what *not* to test.
**Discussion highlight:** Fills the most-requested functional gap — see Community Demand Trends below. Well-structured, single-focus, uses the official skill template.

---

## 2. Community Demand Trends

From Issues (organized by engagement):

### 🔥 Trust & Security (highest urgency — [Issue #492](https://github.com/anthropics/skills/issues/492), 43 comments, 2👍)
Community skills distributed under the `anthropic/` namespace impersonate official Anthropic skills, creating a trust boundary vulnerability. Users may grant elevated permissions believing they are official. **This is the most-discussed issue in the repository.**

### 🔥 Skill Sharing & Distribution ([Issue #228](https://github.com/anthropics/skills/issues/228), 16 comments, 8👍)
Org-wide skill sharing is broken — users must manually download `.skill` files, send via Slack/Teams, and have colleagues navigate UI menus. Demand for a shared skill library or direct sharing link.

### 🔥 Skill-Creator Toolchain Reliability ([Issue #556](https://github.com/anthropics/skills/issues/556), 12 comments, 7👍; [Issue #1169](https://github.com/anthropics/skills/issues/1169), 3 comments)
`run_eval.py`/`run_loop.py` report `recall=0%` on every iteration — the skill-description optimization loop is broken. Multiple independent reproductions; multiple contributors submitting fixes.

### 📈 Document Formats
ODT ([PR #486](https://github.com/anthropics/skills/pull/486)) and typography ([PR #514](https://github.com/anthropics/skills/pull/514)) — the community wants complete, high-quality document output coverage.

### 📈 Meta-Skills for Quality Assurance
Self-audit/skill-quality-analyzer ([PR #1367](https://github.com/anthropics/skills/pull/1367), [PR #83](https://github.com/anthropics/skills/pull/83)) — skills that audit and verify AI output quality.

### 📈 Testing Skills
Testing-patterns ([PR #723](https://github.com/anthropics/skills/pull/723)) — a comprehensive, focused skill. **Still the most-requested functional skill direction.**

### ⚠️ Known Broken Skills
- [Issue #189](https://github.com/anthropics/skills/issues/189) — `document-skills` and `example-skills` plugins install identical content, causing duplicate skills in context window (9👍).
- [Issue #1487](https://github.com/anthropics/skills/issues/1487) — `claude-api` skill eagerly injects ~156k tokens, exhausting the context window in a single tool call.
- [Issue #12](https://github.com/anthropics/skills/issues/12) — `docx` skill whitespace reformatting corrupts documents.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and may land soon:

### ServiceNow Platform Skill ([PR #568](https://github.com/anthropics/skills/pull/568))
**Author:** Vanka07 | Updated: 2026-08-12 (most recent update among top PRs)
Broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM, FSM, HRSD, CSM, SPM/PPM, Vulnerability Response, Security Incident Response, and IntegrationHub. Enterprise-grade scope, recently active.

### Pyxel Retro Game Development ([PR #525](https://github.com/anthropics/skills/pull/525))
**Author:** kitao | Updated: 2026-07-15
Skill for `pyxel-mcp`, an MCP server for the Pyxel retro game engine. Covers the write → run_and_capture → inspect → iterate workflow. Niche but well-defined; author is also the MCP server maintainer.

### `skill-creator` Fix: Unquoted YAML Description Warning ([PR #539](https://github.com/anthropics/skills/pull/539))
**Author:** Lubrsy706 | Updated: 2026-04-16
Adds pre-parse validation to detect unquoted `description` fields containing `:` — prevents silent YAML parsing failures where descriptions get truncated. Small, focused, clearly correct.

### `docx` Tracked Change `w:id` Collision Fix ([PR #541](https://github.com/anthropics/skills/pull/541))
**Author:** Lubrsy706 | Updated: 2026-04-16
Fixes document corruption when the DOCX skill adds tracked changes alongside existing bookmarks (shared `w:id` ID space in OOXML). Directly addresses a document-corruption bug class.

### Skills Spec Compliance Fix ([PR #1538](https://github.com/anthropics/skills/pull/1538))
**Author:** bechor25 | Updated: 2026-08-12
Brings two skills back under the Agent Skills spec — `template/SKILL.md` name mismatch with its directory, plus a second skill failing `skills-ref validate`. Critical for maintaining the reference implementation's integrity.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliability infrastructure — fixing the skill-creator evaluation pipeline (0% recall bug), the trust boundary vulnerability from namespace impersonation, and duplicate/corrupting skills — before any new functional skills can be trusted in production.**

---

# Claude Code Community Digest — 2026-08-16

## Today's Highlights
No new releases landed in the last 24 hours, but the issue tracker remains highly active with 50 items updated. The community is heavily focused on session management (continuation and message queueing), prompting two of the most-upvoted feature requests. A cluster of Windows stability reports continues to dominate bug reports, with recurring GPU crashes and authentication/setup friction on that platform.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

**1. [Feature] Continue when the session limit reached** — [#13354](https://github.com/anthropics/claude-code/issues/13354)  
*197 👍 · 78 comments*  
The most active and upvoted open request. Users want an explicit "continue" flow when hitting the session limit rather than being forced to start over or manually manage resumption. Community discussion indicates this is a daily frustration for long-running tasks.

**2. [Feature] Message queue mode** — [#50246](https://github.com/anthropics/claude-code/issues/50246)  
*197 👍 · 56 comments*  
Tied with the top issue on upvotes. Users want to queue follow-up messages while Claude is mid-task instead of being forced to interrupt and risk derailing current work. Several commenters describe workarounds (external note-taking, separate sessions) indicating real workflow impact.

**3. [Bug] Windows: fatal GPU-process crash in desktop app** — [#80444](https://github.com/anthropics/claude-code/issues/80444)  
*5 👍 · 34 comments*  
Electron-based desktop app crashes via the in-app Browser tab on two different GPU driver versions, leaving the MSIX package unlaunchable (appxState=2) until Repair. High comment volume suggests broad impact on Windows users.

**4. [Bug] Claude Desktop repeated crashes, requires Repair** — [#85199](https://github.com/anthropics/claude-code/issues/85199)  
*4 👍 · 23 comments*  
Related to the above: recurring crashes on Windows requiring "Advanced Options → Repair." Likely same root-cause family; community is awaiting a fix.

**5. [Bug] tools/list_changed doesn't refresh deferred-tool index** — [#66084](https://github.com/anthropics/claude-code/issues/66084)  
*3 👍 · 8 comments · Labeled reproduced*  
Confirmed bug on macOS: the deferred-tool/ToolSearch index doesn't update in interactive sessions after `tools/list_changed`. Affects MCP-heavy workflows and tool discovery reliability.

**6. [Bug] `--permission-mode dontAsk` denies Write/Edit unconditionally** — [#74567](https://github.com/anthropics/claude-code/issues/74567)  
*0 👍 · 3 comments · Labeled reproduced*  
Headless agents using `dontAsk` can't write files even with `--allowedTools` scoping. Community highlights lack of a working scoped-write option for unattended/CI workflows — a blocker for automation.

**7. [Bug] Cross-session messages displayed but never enqueued** — [#86671](https://github.com/anthropics/claude-code/issues/86671)  
*1 👍 · 3 comments · Labeled regression*  
Windows regression: messages sent across sessions appear in the UI but the model never sees them. Silent data loss in multi-session workflows.

**8. [Bug] `claude setup-token` tokens rejected with 400** — [#86986](https://github.com/anthropics/claude-code/issues/86986)  
*0 👍 · 1 comment*  
Freshly minted long-lived tokens from `setup-token` are rejected on first request (`API Error: 400`), while interactive auth works. Reproducible locally and in CI — a blocker for automation pipelines.

**9. [Bug] External editor input truncated and replaced** — [#87017](https://github.com/anthropics/claude-code/issues/87017)  
*0 👍 · 1 comment*  
Linux: text typed via external editor (Ctrl+G) is silently truncated and replaced with a `[Pasted text #N +N lines]` stub on return. Potential data loss for users relying on external editors.

**10. [Feature] Account-level sync for config and auto memory** — [#87027](https://github.com/anthropics/claude-code/issues/87027)  
*0 👍 · 1 comment*  
Request to sync user config, settings, and auto-memory across multiple machines via login. Related: [#87028](https://github.com/anthropics/claude-code/issues/87028) asks for a context path between claude.ai and Claude Code.

---

## Key PR Progress
No significant PRs were merged in the last 24 hours. The most notable open PRs are:

**1. [#86870](https://github.com/anthropics/claude-code/pull/86870) — fix: prevent false-positive CVP status changes during authorized security research**  
Open. Adds context checking to `security-guidance/hooks/review_api.py` to avoid triggering security alerts during authorized lab/educational sessions. Directly addresses the false-positive safety blocks raised in issues like [#72074](https://github.com/anthropics/claude-code/issues/72074) and [#72088](https://github.com/anthropics/claude-code/issues/72088).

**2. [#84600](https://github.com/anthropics/claude-code/pull/84600) — Enable frontend-design plugin at project scope** *(closed)*  
Registers the official marketplace and enables the `frontend-design` skill via `.claude/settings.json`. Merged/closed — low-risk DX improvement.

**3. [#82981](https://github.com/anthropics/claude-code/pull/82981) — Claude/automatizar inventario insumos w4n98s** *(open)*  
Non-code change; appears to be a test or accidental PR. Low relevance.

---

## Feature Request Trends

**1. Session Continuation & Queueing (dominant trend)**  
Two top issues ([#13354](https://github.com/anthropics/claude-code/issues/13354), [#50246](https://github.com/anthropics/claude-code/issues/50246)) share ~400 combined upvotes. The community wants: (a) graceful handling of session limits, and (b) the ability to queue follow-up messages without interrupting active work. This signals deep workflows where session boundaries are a real bottleneck.

**2. Cross-Device / Cross-Product State Sync**  
Multiple requests ([#87027](https://github.com/anthropics/claude-code/issues/87027), [#87028](https://github.com/anthropics/claude-code/issues/87028)) ask for account-level sync of config, auto-memory, and context between machines and between claude.ai and Claude Code. Users want their setup and memory to "follow the login," not live only in local files.

**3. TUI and UX Polish**  
Visible scrollbar ([#62929](https://github.com/anthropics/claude-code/issues/62929)) and fullscreen statusLine fixes ([#76411](https://github.com/anthropics/claude-code/issues/76411)) reflect growing demand for richer terminal UX as the TUI becomes a primary surface.

**4. Headless/Agent-Oriented Permissions**  
The `dontAsk` bug ([#74567](https://github.com/anthropics/claude-code/issues/74567)) and `setup-token` failures ([#86986](https://github.com/anthropics/claude-code/issues/86986)) point to a broader need: reliable, well-documented permission modes and long-lived token support for unattended agents.

---

## Developer Pain Points

**1. Windows Desktop Stability**  
A cluster of issues ([#80444](https://github.com/anthropics/claude-code/issues/80444), [#85199](https://github.com/anthropics/claude-code/issues/85199), [#87013](https://github.com/anthropics/claude-code/issues/87013)) describes repeated GPU-process crashes in the Electron desktop app, with some requiring manual MSIX repair. This is the loudest single platform pain point.

**2. Silent Data Corruption / Loss**  
Multiple reports describe silent failures: memory-file frontmatter gets wiped on YAML parse errors ([#76868](https://github.com/anthropics/claude-code/issues/76868)), cross-session messages never reach the model ([#86671](https://github.com/anthropics/claude-code/issues/86671)), and external editor text is truncated ([#87017](https://github.com/anthropics/claude-code/issues/87017)). Silent failures are the most damaging class of bug for trust.

**3. False-Positive Safety/AUP Blocks**  
A series of reports ([#72074](https://github.com/anthropics/claude-code/issues/72074), [#72088](https://github.com/anthropics/claude-code/issues/72088), [#72093](https://github.com/anthropics/claude-code/issues/72093)) documents security/AUP filters halting legitimate security research and reverse-engineering work. PR [#86870](https://github.com/anthropics/claude-code/pull/86870) is a community attempt to address this.

**4. Auth & Onboarding Friction on Windows**  
Issues around PATH setup ([#86999](https://github.com/anthropics/claude-code/issues/86999)), `setup-token` rejection ([#86986](https://github.com/anthropics/claude-code/issues/86986)), and login-loop bugs ([#84331](https://github.com/anthropics/claude-code/issues/84331), [#79808](https://github.com/anthropics/claude-code/issues/79808)) show Windows onboarding is rougher than macOS/Linux.

**5. Deferred-Tool / MCP Index Staleness**  
`tools/list_changed` not refreshing the deferred-tool index ([#66084](https://github.com/anthropics/claude-code/issues/66084)) and unusable filesystem MCP on macOS ([#80094](https://github.com/anthropics/claude-code/issues/80094)) indicate MCP integration still has rough edges.

**6. Hooks Configuration Fragility**  
Two distinct bugs: one schema-invalid matcher silently disables *all* hooks ([#75081](https://github.com/anthropics/claude-code/issues/75081)), and identical hooks from settings and plugins run concurrently without deduplication ([#76297](https://github.com/anthropics/claude-code/issues/76297)). Hooks are powerful but fragile — users want validation and deterministic behavior.

---

*Digest generated from GitHub data for anthropics/claude-code, 2026-08-16.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-16

## Today's Highlights

The Codex community remains heavily focused on desktop app performance regressions, with a surge of Windows-specific stuttering reports following the Aug 14-15 releases (builds 26.810.x) — including multiple reports of system-wide cursor freezes even when Codex is idle. On the engineering side, a substantial batch of 20+ merged PRs landed today covering TUI improvements, MCP hooks integration, storage diagnostics, and session pagination fixes, signaling active work on both reliability and developer experience. Two alpha releases (`rust-v0.148.0-alpha.19` and `.20`) were published with no visible changelog details.

---

## Releases

### rust-v0.148.0-alpha.20 & rust-v0.148.0-alpha.19
- **Published:** 2026-08-15/16
- **Changelog:** Minimal — both releases are tagged with no detailed notes beyond version identifiers.
- **Context:** These rapid-fire alpha iterations follow the 0.148.0-alpha series trend observed over the past weeks, likely containing incremental fixes related to session handling, MCP connectivity, and the Windows stutter issues dominating recent issue reports.

🔗 [View releases](https://github.com/openai/codex/releases)

---

## Hot Issues (Top 10)

### 1. 🔥 [Codex App frequently freezes/stutters on Windows 11 Pro despite sufficient system resources](https://github.com/openai/codex/issues/20214)
- **State:** OPEN | **Comments:** 104 | **👍:** 85
- **Why it matters:** The longest-running and most-upvoted performance issue. AMD Ryzen 5 + 32GB RAM systems still experience freezes, ruling out resource constraints as the cause.
- **Community sentiment:** High frustration; users report the issue persists across multiple app versions and Windows builds.

### 2. 🔥 [[Windows] ChatGPT/Codex desktop app causes system-wide mouse stutter when running without elevation](https://github.com/openai/codex/issues/38546)
- **State:** OPEN | **Comments:** 25 | **👍:** 11
- **Why it matters:** Filed Aug 14, this issue is gaining traction rapidly. Non-elevated Codex causes whole-OS mouse stutter, suggesting a polling or low-level input hook pattern.
- **Community sentiment:** Users confirm the stutter disappears immediately when the app is run as admin or exited.

### 3. [Codex Desktop continuously generates Crashpad pending dumps, growing without any limit: +5GB per day](https://github.com/openai/codex/issues/25921)
- **State:** OPEN | **Comments:** 17 | **👍:** 8
- **Why it matters:** Silent 5GB/day disk consumption via Crashpad dump accumulation is a severe operational issue for long-running users.
- **Community sentiment:** Users report hundreds of thousands of files; some hit disk-full conditions on smaller SSDs.

### 4. [Scope Codex chats to VS Code projects/workspaces](https://github.com/openai/codex/issues/3550)
- **State:** CLOSED | **Comments:** 34 | **👍:** 79
- **Why it matters:** Second-most-upvoted issue overall. The "worktrees" feature likely addressed this, but community demand for workspace-scoped conversations remains a strong signal.
- **Community sentiment:** Developers want per-project session isolation to reduce context confusion.

### 5. [[Windows] System-wide stutter while Codex is idle; fully exiting app immediately restores OS responsiveness](https://github.com/openai/codex/issues/38750)
- **State:** OPEN | **Comments:** 9 | **👍:** 0
- **Why it matters:** Filed 2026-08-15. Confirms the stutter occurs even with zero active tasks — the app's background/UI loop is the culprit.
- **Community sentiment:** Users are reverting to older builds (26.616.x) as a workaround.

### 6. [Paginated history drops valid flattened rollout records and reuses ordinals](https://github.com/openai/codex/issues/35746)
- **State:** OPEN | **Comments:** 13 | **👍:** 0
- **Why it matters:** Data-integrity bug in rollout history pagination — lost records and ordinal reuse can corrupt session replay fidelity.
- **Community sentiment:** Low visibility but high severity for developers relying on `--resume` and session history.

### 7. [Desktop threads can be poisoned by inline base64 tool images, leading to Bad Request on resume](https://github.com/openai/codex/issues/18629)
- **State:** OPEN | **Comments:** 12 | **👍:** 2
- **Why it matters:** Persisted `input_image` payloads with base64 data corrupt thread replay, causing `{"detail":"Bad Request"}` errors and likely inflated token usage.
- **Community sentiment:** Users report unusable threads after moderate image-tool usage; workaround is manual session deletion.

### 8. [Subagent fork sessions persist large JSONL histories indefinitely, causing severe ~/.codex disk bloat](https://github.com/openai/codex/issues/30779)
- **State:** OPEN | **Comments:** 5
- **Why it matters:** Forked subagent sessions never get cleaned up, consuming gigabytes of disk. Related to the broader session-growth problem (#34337).
- **Community sentiment:** Users on API plans with heavy subagent use report 10s of GBs within days.

### 9. [Native Bedrock Codex GPT-5.6 Sol lacks explicit cache controls, producing high cache-write spend](https://github.com/openai/codex/issues/37674)
- **State:** OPEN | **Comments:** 4 | **👍:** 5
- **Why it matters:** AWS Bedrock deployments cannot opt into explicit prompt caching, leading to material cost increases on agentic workloads.
- **Community sentiment:** Enterprise users flag this as a blocker for production adoption on Bedrock.

### 10. [Codex copied the image file 150,000 times, consuming 400 GiB of disk space](https://github.com/openai/codex/issues/35470)
- **State:** OPEN | **Comments:** 5
- **Why it matters:** Extreme edge case of file-copy amplification on Windows. Likely related to image context handling and loop detection failures.
- **Community sentiment:** Shocked reactions; users are checking their own `~/.codex` directories for similar bloat.

---

## Key PR Progress (Top 10)

### 1. [Add storage diagnostics to `codex doctor`](https://github.com/openai/codex/pull/38795) ✅ Merged
- Warns when `CODEX_HOME` drops below 5 GiB, fails below 1 GiB; reports Windows Dev Drive status with remediation guidance.
- **Significance:** Directly addresses the disk-bloat issue cluster (#25921, #30779, #34337).

### 2. [Use paginated history for persistent exec threads](https://github.com/openai/codex/pull/38774) ✅ Merged
- Requests paginated history for `codex exec` persistent threads; falls back to legacy history for stores without pagination support.
- **Significance:** Targets the pagination data-loss bug in #35746.

### 3. [Add MCP tool handler support to the hooks engine](https://github.com/openai/codex/pull/38705) ✅ Merged
- Discovers synchronous `mcp_tool` hook handlers, expands nested placeholders in tool inputs, preserves JSON types.
- **Significance:** Extends the hooks engine to MCP — major step for plugin/MCP workflow integration.

### 4. [Refresh hook runtimes after plugin changes](https://github.com/openai/codex/pull/38703) ✅ Merged
- Rebuilds hook runtimes on effective plugin changes or marketplace upgrades; refreshes plugin/MCP caches.
- **Significance:** Eliminates stale runtime issues when plugins are updated mid-session.

### 5. [Route permission requests through shared Guardian approvals](https://github.com/openai/codex/pull/38701) ✅ Merged
- Unifies `request_permissions` into the shared Guardian approval path; preserves turn cancellation during pending reviews.
- **Significance:** Simplifies permission UX across TUI, exec, and desktop contexts.

### 6. [Keep active-turn model settings stable across updates](https://github.com/openai/codex/pull/38785) ✅ Merged
- Prevents model changes mid-turn; setting updates apply to the next turn instead of altering in-flight sampling.
- **Significance:** Fixes nondeterministic behavior when users change models during long runs.

### 7. [Scope TUI app directory state to the active context](https://github.com/openai/codex/pull/38743) ✅ Merged
- Invalidates stale app data, pickers, and in-flight requests when account/workspace/thread context changes.
- **Significance:** Fixes cross-account app contamination in the TUI.

### 8. [Normalize CRLF line endings in pasted text](https://github.com/openai/codex/pull/38704) ✅ Merged
- Converts CRLF pairs correctly so pasted Windows text doesn't create double line breaks in the TUI composer.
- **Significance:** Quality-of-life fix for Windows users.

### 9. [Propagate request trace context through exec-server relays](https://github.com/openai/codex/pull/38690) ✅ Merged
- Adds W3C `traceparent`/`tracestate` to relay frames, even across fragmented Noise-record encrypted requests.
- **Significance:** Improves distributed tracing reliability for debugging and observability.

### 10. [Add a health endpoint to the code-mode gRPC listener](https://github.com/openai/codex/pull/38806) ✅ Merged
- Serves `GET /healthz` over HTTP/1.1 while continuing to require HTTP/2 for gRPC methods.
- **Significance:** Enables standard load-balancer health checks for code-mode deployments.

---

## Feature Request Trends

1. **Workspace/Project-Scoped Sessions** — Persistent demand to scope chats to VS Code projects (👍 79 on #3550). Users want per-project session isolation and recent-task filtering.
2. **Explicit Prompt Cache Controls (Bedrock)** — Request for opt-in cache controls in AWS Bedrock deployment path to manage costs (#37674).
3. **MCP Elicitation Over Remote Streamable HTTP** — Users want interactive MCP forms to work over remote HTTP, not just stdio (#38707).
4. **Session Storage Limits & Cleanup** — Repeated requests for built-in session pruning policies, size caps, and garbage collection for rollout files (#34337, #30779).
5. **Health/Diagnostics Tooling** — `codex doctor` expansion is welcomed; community wants deeper storage checks, crash-dump cleanup tooling, and Dev Drive guidance.

---

## Developer Pain Points

1. **Windows Desktop Performance Is the #1 Pain Point** — The dominant theme across issues. System-wide stutter, freezes, idle CPU spikes (90-102%), and mouse jank persist across multiple versions and are worsening with the 26.810.x line. Users are actively reverting versions.
2. **Silent Disk Bloat Across the Board** — Crashpad dumps (+5GB/day), subagent fork histories, image-file copy loops (400 GiB), and unbounded rollout storage are draining developer SSDs silently. No built-in cleanup mechanism exists.
3. **Session/History Data Integrity** — Pagination dropping rollout records (#35746), ordinals being reused, and base64 images poisoning replayable threads (#18629) add distrust to `--resume` workflows.
4. **MCP/Remote Connectivity Gaps** — Remote streamable HTTP elicitation doesn't deliver user Accept responses; desktop MCP suites accumulate per-session on Windows with missed process-tree termination (#34614).
5. **macOS Computer-Use Spawn Storms** — `SkyComputerUseService` respawn loops (5-8 processes/second) that exhaust launchservicesd and trigger kernel panics, even when Computer Use is disabled (#38760, #38769, #38771).

---

*Digest compiled from public GitHub data for openai/codex on 2026-08-16. All links point to official repository resources.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-16

## Today's Highlights
A new nightly release (v0.56.0-nightly.20260815) landed with a fix for SSR agent test infrastructure. The community continues to surface critical concerns around subagent reliability — particularly false "success" reports after hitting turn limits and generalist agent hangs — with active PRs now addressing both issues. Security is also in focus, with SSRF protections and sandbox runtime upgrades moving through the pipeline.

## Releases
**v0.56.0-nightly.20260815.g2a87e7be1** — Patch release migrating `process.env` to `vi.stubEnv` in a2a-server tests to fix an SSR agent test issue. ([Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260814.gc0d192452...v0.56.0))

## Hot Issues
1. **[#22323: Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — Critical P1 bug where `codebase_investigator` reports `status: "success"` and `Termination Reason: "GOAL"` despite hitting turn limits before analysis. Misleading signals can corrupt downstream decision-making. 12 comments, actively being fixed in PR #28815.

2. **[#21409: Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** — P1 issue with 8 👍 reactions. Simple operations like folder creation hang for up to an hour when the CLI defers to the generalist agent. Community workaround: explicitly instructing the model to avoid subagent delegation.

3. **[#19873: Zero-dependency OS sandboxing & post-execution intent routing](https://github.com/google-gemini/gemini-cli/issues/19873)** — Enhancement leveraging Gemini 3 models' native bash affinity. Proposes OS-level sandboxing with selective command approval rather than restrictively excluding shell execution. Large effort, ongoing discussion.

4. **[#24353: Robust component-level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** — Epic tracking expansion of behavioral evals beyond the current 76 tests across 6 Gemini models. Signals maturing focus on systematic quality assurance.

5. **[#22745: AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** — Epic investigating AST-aware tools for precise method-bound reads, reduced token noise, and improved codebase navigation. Paired with #22746 for implementation research.

6. **[#21968: Gemini doesn't use skills and sub-agents proactively](https://github.com/google-gemini/gemini-cli/issues/21968)** — Community-observed behavior: custom skills and sub-agents are ignored unless explicitly instructed. Users with well-described `gradle` and `git` skills report the model rarely invokes them autonomously.

7. **[#25166: Shell commands stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1 bug causing hangs after simple CLI command execution. 3 👍 reactions; impacts day-to-day workflow reliability.

8. **[#26522: Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — P2 bug in the memory system: low-signal sessions never get marked as processed, causing repeated re-extraction attempts and wasted tokens.

9. **[#26525: Deterministic redaction and reduced Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — Security-adjacent concern: transcript content is sent to the extraction model before redaction occurs. Also flags potential logging of skills referenced in candidate patches.

10. **[#21983: Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — P1 compatibility bug affecting Linux Wayland users. Browser agent terminates with `GOAL` status without explaining the root cause.

## Key PR Progress
1. **[#28815: Preserve original termination reason during subagent recovery](https://github.com/google-gemini/gemini-cli/pull/28815)** — Direct fix for #22323. Ensures `MAX_TURNS`/`TIMEOUT` are reported accurately even when recovery succeeds. P1, maintainer-only.

2. **[#28828: Warn when a preview model is silently substituted](https://github.com/google-gemini/gemini-cli/pull/28828)** — Fixes #28825. Currently, requesting a preview model without entitlement silently rewrites to `auto-gemini-2.5` with zero indication. Adds explicit warning.

3. **[#28725: Prevent SSRF via DNS resolution bypass in web-fetch](https://github.com/google-gemini/gemini-cli/pull/28725)** — Critical security fix (CVSS 8.6) for #28555. Blocks malicious DNS rebinding that could reach private/loopback IPs like `169.254.169.254`.

4. **[#28726: Upgrade sandbox Dockerfile to node:22-slim](https://github.com/google-gemini/gemini-cli/pull/28726)** — Fixes #28584 by migrating all sandbox Dockerfiles from node:20 to node:22, addressing EOL security concerns.

5. **[#28827: Avoid false authentication errors for 401 substrings](https://github.com/google-gemini/gemini-cli/pull/28827)** — Fixes #28203. Prevents unrelated values containing "401" from being treated as auth failures. Adds regression coverage for ports and exit codes.

6. **[#28679: Improve Vertex AI 401 error message when using standard API key](https://github.com/google-gemini/gemini-cli/pull/28679)** — Better DX: provides clear guidance when users configure vertex-ai auth but only provide a standard Gemini API key.

7. **[#28823: Evals for task graph dependencies and error recovery](https://github.com/google-gemini/gemini-cli/pull/28823)** — Adds behavioral evals for `tracker_add_dependency`, `tracker_visualize`, file-path 404 recovery, and shell failure diagnosis/retry.

8. **[#28824: Multi-tool chain, context safety, and security boundary evals](https://github.com/google-gemini/gemini-cli/pull/28824)** — New evals for multi-tool workflows, safe handling of large files, and enforcement of sensitive-file boundaries.

9. **[#28822: Evals for todos and task tracker](https://github.com/google-gemini/gemini-cli/pull/28822)** — Behavioral evals for `write_todos`, `complete_task`, `tracker_list_tasks`, and `tracker_get_task` — strengthening core planning/tracking reliability.

10. **[#28608: Fall back to stable models when preview model 404s with API key auth](https://github.com/google-gemini/gemini-cli/pull/28608)** — Fixes #28600. Resume fallback chain when `gemini-3.1-pro-preview` gets 404 with Gemini API key auth lacking preview access.

## Feature Request Trends
- **Zero-dependency OS sandboxing** (#19873): Tap into models' native bash capabilities while preserving security via sandboxing and post-execution intent routing.
- **AST-aware code intelligence** (#22745, #22746): Precise method-bound reads, search, and codebase mapping to reduce turns and token noise.
- **Improved agent self-awareness** (#21432): Accurate CLI flags, hotkeys, and self-execution knowledge.
- **Subagent trajectory visibility** (#22598): Expose subagent behavior via `/chat share` for review and evaluation.
- **Browser agent resilience** (#22232): Automatic session takeover and lock recovery instead of fail-fast behavior.
- **Component-level evaluations** (#24353): Systematic behavioral evals scaled across models.

## Developer Pain Points
- **Subagent reliability**: False success reports (#22323), indefinite hangs (#21409), and unpermissioned agent activation (#22093) erode trust in delegation.
- **Silent model substitution**: Preview models quietly replaced without notification (#28828, #28608) confuse users about which model actually ran.
- **Shell hang and stuck states**: Commands showing "Waiting input" after completion (#25166) and interactive prompts hanging (#22465) break automation flows.
- **Tool sprawl and cleanup overhead**: Models creating temp scripts across directories (#23571) and exceeding the 128-tool limit causing 400 errors (#24246).
- **Configuration ignored**: Browser agent and subagents ignoring `settings.json` overrides (#22267, #22093) and symlinked agent files not recognized (#20079).
- **Memory system inefficiencies**: Infinite low-signal retries (#26522), pre-redaction transcript exposure (#26525), and silent patch skipping (#26523).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-16

## Today's Highlights

The Copilot CLI community is actively surfacing reliability concerns around authentication and MCP server integration, with two separate reports of Atlassian MCP OAuth regressions across recent releases. A significant deployment issue affects NixOS users where the Bash tool has been broken since v1.0.49, and Codespaces users are stuck on an ancient v1.0.3 due to update path failures. On the positive side, maintainers are closing out infrastructure improvements around MCP registry policy handling in CI and migrating pull request automation away from `pull_request_target`.

## Releases

No new releases in the last 24 hours. The community is currently tracking issues against v1.0.79 and v1.0.80.

## Hot Issues

1. **[#3392 — Bash tool breaks on NixOS with version >=1.0.49](https://github.com/github/copilot-cli/issues/3392)**  
   **Labels:** platform-linux, tools | **Reactions:** 👍 9 | **Comments:** 4  
   Long-standing issue (May 2026) with high community engagement. The Bash tool fails to start on NixOS, throwing "Failed to start bash process" errors. NixOS users remain blocked on recent versions, and the issue has persisted across multiple releases (1.0.49 through 1.0.50+).

2. **[#4480 — Atlassian MCP OAuth fails with "Incompatible authorization server" on 1.0.79](https://github.com/github/copilot-cli/issues/4480)**  
   **Status:** CLOSED | **Reactions:** 👍 6 | **Comments:** 4  
   A regression from 1.0.71 where OAuth discovery for the Atlassian MCP server fails due to an RFC 8414 §3.3 issuer mismatch. Closed, but a follow-up issue (#4490) suggests the fix may not have fully landed.

3. **[#4490 — Atlassian MCP OAuth authentication broken in 1.0.80](https://github.com/github/copilot-cli/issues/4490)**  
   **Status:** OPEN | **Comments:** 0  
   The same RFC 8414 §3.3 regression appears to persist in v1.0.80, despite working in v1.0.78. This suggests an incomplete fix or a recurring regression pattern in the OAuth discovery logic.

4. **[#4421 — MCP initialize handshake has a fixed 60s budget with no retry](https://github.com/github/copilot-cli/issues/4421)**  
   **Status:** OPEN | **Comments:** 1  
   Hard-coded 60-second timeout with no retry for MCP `initialize` handshakes. npx-launched stdio servers fail ~29% of sessions and never recover for the session's lifetime. Significant reliability concern for MCP-heavy workflows.

5. **[#4499 — v1.0.79 fatal "Committing semi space failed" OOM in autopilot](https://github.com/github/copilot-cli/issues/4499)**  
   **Status:** OPEN | **Comments:** 0  
   Windows crash where V8 heap is only 607 MB of 4.30 GB at crash time — this is a host-RAM commit failure, not a heap limit issue. Points to potential memory management problems in long-running autopilot sessions on Windows.

6. **[#4491 — /spawn command template contradicts its own contract](https://github.com/github/copilot-cli/issues/4491)**  
   **Status:** OPEN | **Comments:** 1  
   The `/spawn` template can silently turn "create a child session" into "inject context into an unrelated running session" — with no approval gate on cross-session writes. A potentially destructive behavior worth urgent attention.

7. **[#4346 — MCP registry policy fetch returns 403 for Actions GITHUB_TOKEN](https://github.com/github/copilot-cli/issues/4346)**  
   **Status:** CLOSED | **Reactions:** 👍 3 | **Comments:** 2  
   Blocked all non-default MCP servers in CI when using the documented PAT-less Actions setup. Now closed, which is good news for CI/CD workflows relying on MCP servers.

8. **[#4494 — Newly enabled model remains unavailable until cache is cleared](https://github.com/github/copilot-cli/issues/4494)**  
   **Status:** OPEN | **Comments:** 0  
   Model catalog doesn't refresh after enabling new models in GitHub settings. Users must manually clear local Copilot state/cache — affects both CLI and Visual Studio.

9. **[#4493 — /restart fails in sessions created with -w](https://github.com/github/copilot-cli/issues/4493)**  
   **Status:** OPEN | **Comments:** 0  
   Sessions started with `copilot -w` cannot recover via `/restart` due to an option conflict between the worktree option and existing session ID.

10. **[#4501 — Codespaces ships Copilot CLI 1.0.3 and update only installs with sudo](https://github.com/github/copilot-cli/issues/4501)**  
    **Status:** OPEN | **Comments:** 0  
    Fresh Codespaces ship an ancient v1.0.3, and `copilot update` doesn't replace the binary without sudo. This leaves many users on a severely outdated version.

## Key PR Progress

Only 2 PRs were updated in the last 24 hours. While the digest format calls for 10, only these are available:

1. **[#4497 — Handle fork PR associations in invalid-label writer](https://github.com/github/copilot-cli/pull/4497)**  
   **Status:** OPEN  
   Updates the trusted invalid-label writer to handle fork PR workflow runs where GitHub doesn't populate the PR association. Falls back to trusted workflow-run metadata, requiring exactly one open PR match — a security-conscious approach to a fragile area.

2. **[#4449 — Migrate pull request automation away from pull_request_target](https://github.com/github/copilot-cli/pull/4449)**  
   **Status:** CLOSED  
   Migrates invalid-label automation off `pull_request_target` (a known supply-chain risk vector). Uses issue-scoped write tokens for closing invalid issues and a no-permission `pull_request` signal for mergeable PR handling. Good security hygiene.

## Feature Request Trends

- **Model flexibility**: [#4495](https://github.com/github/copilot-cli/issues/4495) requests support for GPT-5.6's `reasoning.mode` parameter ("standard"/"pro"), joining ongoing demand for finer-grained model control.
- **Session management UX**: [#4502](https://github.com/github/copilot-cli/issues/4502) requests the ability to un-archive sessions marked as Done. Users want reversible session lifecycle actions.
- **Better MCP configuration**: [#4275](https://github.com/github/copilot-cli/issues/4275) asks for `contextTier` to be exposed as a session config option in ACP, matching the interactive CLI's `/model` picker. Demand for parity between interactive and non-interactive modes is a recurring theme.
- **Configurable timeouts**: [#4421](https://github.com/github/copilot-cli/issues/4421) highlights demand for configurable MCP handshake timeouts with retry logic.

## Developer Pain Points

- **Repeated authentication regressions**: The Atlassian MCP OAuth issue appeared in 1.0.79, was reported closed, then resurfaced in 1.0.80 (#4480, #4490). This pattern of recurring regressions in OAuth/MCP discovery is eroding trust in release stability.
- **Stale environments**: Codespaces shipping v1.0.3 (#4501) and NixOS breakage (#3392) leaving users unable to update or run recent versions. Update mechanism fragility is a real blocker for adoption.
- **Non-interactive mode gaps**: BYOK prompt caching breaks in autopilot nudge turns (#4500), OOM crashes in Windows autopilot (#4499), and MCP server failures in CI (#4346) suggest the non-interactive/A CP surface is less battle-tested than the interactive CLI.
- **Irreversible actions**: `/spawn` potentially writing to unrelated sessions (#4491) and no way to un-archive Done sessions (#4502) point to missing safety rails and undo capability.
- **Model availability friction**: Newly enabled models not appearing until cache reset (#4494) creates confusion and wasted debugging time when users expect their newly authorized models to just work.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest – 2026-08-16**

---

### 1. Today's Highlights
The community is actively pushing for a robust, persistent **memory system** in Kimi Code CLI, with two long-standing issues (#1283, #1478) receiving recent updates. Additionally, a new report (#2604) flags a potential **~3–5× reduction in effective weekly token allowance** without prior announcement, sparking concerns about subscription terms or metering regressions. A closed issue (#1155) confirms a past bug fix for the `openai_legacy` provider, while new discussions focus on **quota-aware context compaction** to better manage token usage on subscription plans.

---

### 2. Releases
No new releases were published in the last 24 hours.

---

### 3. Hot Issues

1. **[#1283 – Feature Request: Memory System – Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)**  
   *Open | Updated 2026-08-15 | 40 comments*  
   The most-discussed feature request: a memory layer for persisting context, project patterns, and user preferences across sessions. Users stress the need for both AI-managed and manual memory. Community reaction remains positive and engaged, though no implementation has been announced.

2. **[#1478 – Can the memory layer be optimized?](https://github.com/MoonshotAI/kimi-cli/issues/1478)**  
   *Open | Updated 2026-08-15 | 3 comments*  
   Follow-up to #1283, highlighting that no memory-related documentation exists (beyond `agent.md`) and that managing large projects without persistent context is painful. References a similar implementation in another tool as inspiration.

3. **[#2604 – Effective weekly allowance appears reduced ~3–5×](https://github.com/MoonshotAI/kimi-cli/issues/2604)**  
   *Open | Updated 2026-08-15 | 2 comments*  
   A user with client-side instrumentation reports a dramatic drop in token allowance without warning. Flags a possible silent Terms change or metering regression. This is a **high-priority trust issue** for paying users.

4. **[#2603 – Quota-aware compaction on subscription plans](https://github.com/MoonshotAI/kimi-cli/issues/2603)**  
   *Open | Updated 2026-08-15 | 0 comments*  
   Suggests triggering context compaction based on **token budget** rather than only the model’s max context window. With K3's 1M-token window, compaction rarely triggers, wasting subscription quotas. A pragmatic proposal for cost-conscious users.

5. **[#1155 – openai_legacy provider drops reasoning content](https://github.com/MoonshotAI/kimi-cli/issues/1155)**  
   *Closed | Updated 2026-08-15 | 0 comments*  
   Resolved bug: the `openai_legacy` provider discarded reasoning content from OpenAI-compatible servers (sglang, vllm) because `reasoning_key` was not forwarded. Important for users of third-party inference engines.

---

### 4. Key PR Progress

1. **[#2524 – fix(tools): count StrReplaceFile replacements against the running content](https://github.com/MoonshotAI/kimi-cli/pull/2524)**  
   *Open | Updated 2026-08-15*  
   Fixes a bug where chained `StrReplaceFile` edits reported replacement counts based on original content, causing false errors. Improves correctness for sequential multi-edit workflows.

2. **[#2506 – fix(kosong): raise a clear error on circular $ref in deref_json_schema](https://github.com/MoonshotAI/kimi-cli/pull/2506)**  
   *Closed | Updated 2026-08-15*  
   Addressed infinite loops on circular `$ref` in JSON schema dereferencing. Small, self-contained fix that improves robustness for users interacting with complex schemas.

---

### 5. Feature Request Trends

- **Persistent Memory System (High Demand):** The dominant request across open issues. Users want Kimi to store and recall project-specific information across sessions, including both automatic (AI-managed) and manual notes. The project is expected to follow patterns seen in other agent tools (e.g., `SOUL.md`, `USER.md`, `MEMORY.md`).
- **Token Budget Awareness on Subscriptions:** A growing concern as users hit plan limits. Requests include quota-based context compaction and clearer metering/billing transparency.
- **Custom Provider Compatibility:** Users expect reliable integration with OpenAI-compatible backends, including handling of reasoning/thinking fields.

---

### 6. Developer Pain Points

- **Memory & Context Loss on Large Projects:** Frequent complaints about losing state between sessions, making work on large codebases inefficient and frustrating. Users strongly desire a built-in memory layer.
- **Silent Quota Reductions:** The reported ~3–5× drop in weekly allowance without notice has eroded user trust. Developers expect predictable and transparent usage limits.
- **Context Compaction Ignoring Subscription Budgets:** With a 1M-token window, users rarely benefit from compaction, leading to wasted paid tokens and unexpected cap hits.
- **Schema/Provider Edge Cases:** Historical issues with `openai_legacy` dropping reasoning content and crashes on circular `$ref` in schemas indicate ongoing friction with non-default setups.

---

This digest reflects a community that values deep, long-running coding sessions, and is actively pressing for smarter memory management and more transparent resource usage.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-16

---

## 1. Today's Highlights

OpenCode's trending discussions center around a cluster of service-side outages and provider reliability issues, particularly with the OpenCode Go/Zen managed provider — grok-4.5 has been failing with HTTP 500/503 errors for two weeks across multiple user reports and issue threads, and paid subscribers are still getting "Insufficient balance" errors. The maintainers have been shipping backend improvements this week, including session state tracking, budget limits, and event subscription refinements, while 18 pull requests from mid-July were batch-closed in the last 24 hours — a sign of active triage and cleanup. A long-running, heavily upvoted feature request around Plan Mode auto-switching to Build mode when using the Question tool remains a community favorite with 31 👍.

---

## 2. Releases

No new versions were published in the last 24 hours.

---

## 3. Hot Issues

**1. [Go subscription paid but workspace shows "Insufficient balance"](https://github.com/anomalyco/opencode/issues/37790)**
14 comments | 0 👍 | Created 2026-07-19 — The all-time top issue in this digest. The Stripe payment succeeded but the workspace never updated the entitlement, making the service unusable. The long tail and no resolution after nearly a month suggests a systemic billing-sync problem that needs urgent internal attention.

**2. [Go Pro tier ($20) with first-month discounts](https://github.com/anomalyco/opencode/issues/24879)**
11 comments | 11 👍 | Created 2026-04-29 — Users hit the Go monthly cap and are forced to Zen pay-as-you-go, which is hard to budget. The community wants a predictable Pro tier with usage discounts — a clear monetization product gap that keeps resurfacing.

**3. [Why does Opencode require a subscription when the site says 100% free?](https://github.com/anomalyco/opencode/issues/42143)**
10 comments | 1 👍 | Created 2026-08-12 — New users are confused by the marketing vs. actual model access. The "free" claim apparently only covers certain models/providers, generating friction and support load.

**4. [Plan Mode + Question tool can auto switch to Build mode](https://github.com/anomalyco/opencode/issues/7801)**
10 comments | 31 👍 | Created 2026-01-11 — The highest-upvoted feature request in this digest. Users want the Question tool to automatically switch from Plan to Build mode — a UX flow that would reduce manual mode juggling during interactive planning.

**5. [grok-4.5 on OpenCode Go not working since Aug 2](https://github.com/anomalyco/opencode/issues/40206)**
9 comments | 1 👍 | Created 2026-08-03 — Provider-API regression affecting a flagship model for two weeks. Response is always HTTP 500, making the paid Go tier unusable for this model. Related reports in #40886 (HTTP 503) and #42802 confirm it spans both Zen and Go providers.

**6. [Infinite compaction loop when compression fails to reduce context](https://github.com/anomalyco/opencode/issues/27924)**
8 comments | 0 👍 | Created 2026-05-16 — A core session-loop bug: when compaction doesn't reduce tokens, the session loops infinitely between overflow→compact, effectively hanging. This is a correctness issue that frustrates long-session users.

**7. [Links wrapped across lines not clickable in Kitty terminal](https://github.com/anomalyco/opencode/issues/35649)**
5 comments | 2 👍 | Created 2026-07-07 — Long URLs with line wrapping break OSC 8 hyperlink handling, making links unclickable. A duplicate was filed today (#42805) with a `needs:compliance` label — the issue likely spans multiple terminal emulators and markdown rendering.

**8. [Upstream request failed: Endpoint is unavailable](https://github.com/anomalyco/opencode/issues/42750)**
4 comments | 0 👍 | Created 2026-08-15 — Repeated retries (up to 8+ attempts) with no success. Likely a service-degradation symptom from OpenCode Go/Zen infrastructure. Same-day reports #42757 and #42799 show broad service instability.

**9. [Fetch Failed after prompts in recent update](https://github.com/anomalyco/opencode/issues/42329)**
4 comments | 0 👍 | Created 2026-08-13 — After the most recent update, prompts fail with "Failed to fetch" — works 0-1 times after restart. A regression report that pairs with the endpoint-unavailable cluster.

**10. [Project path not updated after moving project directory](https://github.com/anomalyco/opencode/issues/34737)**
4 comments | 0 👍 | Created 2026-07-01 — OpenCode stores the original project path, and after a move it reopens the deleted location. A basic state-migration bug that affects users reorganizing their filesystem — low severity but frequent enough to be noisy.

---

## 4. Key PR Progress

**1. [feat(session): add viewed state](https://github.com/anomalyco/opencode/pull/42811)** — New server-owned session attention state (still open). Adds `time.viewed` alongside `time.idle` so clients can distinguish unread sessions, with a durable `session.viewed` event. Useful for TUI/desktop unread-badge indicators.

**2. [feat(opencode): add per-session budget limit](https://github.com/anomalyco/opencode/pull/42823)** — Adds `budget` per session: stops the assistant when spend reaches the limit. Includes schema migration and API support. Directly addresses cost-control pain points from #24879 and #32911.

**3. [feat(app): add voice input and session budget UI](https://github.com/anomalyco/opencode/pull/42824)** — Companion to #42823: mic button for continuous speech-to-text and a session-budget panel. Voice input enables hands-free interaction; budget UI makes cost controls visible.

**4. [fix(desktop): reveal scrollbar in settings dialog panels](https://github.com/anomalyco/opencode/pull/35555)** — Closed after automated cleanup. Settings panels hid their scrollbars, so keyboard-only or scroll-wheel-less users couldn't tell content continued below the fold. Applies to General/Keybinds/Providers/Models panels in both layouts.

**5. [fix(plugin): scope Promise event iterators](https://github.com/anomalyco/opencode/pull/42832)** — Replaces the unowned stream bridge with one child Effect scope and scoped queue per async iterator. Prevents buffered events escaping and makes pending `next()` calls resolve terminally — a robustness fix for plugin event subscribers.

**6. [feat(core): add Docker blueprint workspaces](https://github.com/anomalyco/opencode/pull/42831)** — New local Docker workspace provider built around immutable blueprint snapshots; keeps coordinator and model loop outside containers; supports subagent forking into child containers; auto-stops idle containers. Targets isolated, reproducible dev environments.

**7. [feat(core): add Incus workspace forks](https://github.com/anomalyco/opencode/pull/42829)** — Incus-backed workspace provider for container/VM blueprints with snapshot-based forking, subagent isolation into child instances, and idle auto-stop. Pairs with the Docker PR as part of an isolation/workspace push.

**8. [refactor(core): use numeric event timestamps](https://github.com/anomalyco/opencode/pull/42828)** — Switches V2 events from `DateTime.Utc` to finite epoch-millisecond numbers. Simplifies persistence/replay and eliminates round-trip conversion — a clean internal simplification for event handling.

**9. [fix(app): release virtualized timeline elements](https://github.com/anomalyco/opencode/pull/42825)** — Fixes a renderer memory leak: TanStack Virtual retained ~37,500 detached DOM nodes in long sessions. Releasing rows after Solid removal should visibly reduce memory growth.

**10. [fix(core): batch streamed session deltas](https://github.com/anomalyco/opencode/pull/42826)** — Performance fix: the server now batches small delta events instead of publishing every text/reasoning/tool fragment separately. Expected to reduce event overhead and client churn under streaming.

---

## 5. Feature Request Trends

Across recent issues, five clear directions stand out:

1. **Pricing and billing transparency** — The #1 conversation driver this week. Users want predictable Pro tiers (#24879), budget limits per session (#42823/#42824), and clarification of the "100% free" claim vs. paid Go/Zen (#42143). Expect continued pressure on monetization UX.

2. **Autonomous mode transitions** — Plan Mode + Question tool auto-switching to Build is the single most-upvoted request (#7801, 31 👍). There is a broader desire for smarter, context-aware mode changes to reduce manual toggling.

3. **Managed-provider reliability** — grok-4.5 failures and endpoint-unavailable errors (#40206, #40886, #42802, #42750) are the loudest symptom — but the underlying ask is stability and better status communication for the Go/Zen managed providers.

4. **Workspace isolation and reproducibility** — Docker blueprint workspaces (#42831) and Incus forks (#42829) point to a user base increasingly running OpenCode in containers/VMs for security and reproducibility, especially for concurrent subagents.

5. **Permission enforcement for agents** — Agent permission rules (`permission.ask`) not being enforced at runtime (#32787) sits alongside Plan-mode discussions — users want fine-grained, reliable control over what agents can execute without prompt.

---

## 6. Developer Pain Points

- **Managed-provider instability is the #1 recurring frustration.** Multiple issues across Go/Zen providers indicate HTTP 500/503s on `grok-4.5`, endpoint-unavailable errors, and "Insufficient balance" — even after successful payment — are ongoing, and some have persisted for weeks. The service appears to be having capacity/entitlement sync failures across the fleet.

- **The recent updates broke things that previously worked.** Reports of "Failed to fetch" after launch (#42329), the Poe provider tool regression (#42818: "Unknown Bedrock client tool"), and the running-subagent row not being clickable in V2 TUI (#42754) all suggest the last one or two releases introduced regressions.

- **Paid users are stuck without a self-service workaround.** Subscription payment succeeded but workspace still says "Insufficient balance" (#37790) with no resolution for nearly a month. Users can't proceed at all.

- **Memory and performance concerns in long sessions.** The compaction loop hang (#27924) and the renderer retaining ~37,500 detached DOM nodes (PR #42825) both indicate long-running sessions degrade — either hanging or eating memory without need.

- **OSC 8 hyperlinks break on wrapped lines.** The Kitty-terminal issue (#35649) plus a duplicate today (#42805) suggests this is a general terminal-compliance problem across many emulators — a small but persistent annoyance for anyone copying long URLs out of the TUI.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-16

## Today's Highlights

Compaction and token accounting dominate today's issue tracker: the long-running #6879 highlights that auto-compaction can fail to trigger until providers hard-reject requests, while multiple PRs land fixes for compaction boundaries, token statistics, and role corruption after session restore. The TUI also gets attention with cursor-flicker fixes and a scroll-step configuration request, and the Mermaid rendering migration from `grok-mermaid` to the more capable `lovely-mermaid` moves forward. A significant Windows-specific issue reveals a `bash` tool vulnerability that can self-terminate the Pi host process.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **#6879 — Auto-compaction never triggers until provider overflow**  
   [github.com/earendil-works/pi/issues/6879](https://github.com/earendil-works/pi/issues/6879)  
   A 2-hour agentic turn on `gpt-5.6-sol` grew past the compaction threshold and only stopped at 373k tokens when the API rejected the request. The community clearly cares (17 👍); the fix likely requires checking after every agentic turn, not just before provider calls.

2. **#6187 — Pi login hangs in WSL after GitHub Copilot device authorization**  
   [github.com/earendil-works/pi/issues/6187](https://github.com/earendil-works/pi/issues/6187)  
   Device authorization completes in the browser, but the WSL client never detects it and hangs. Closed, but with 27 comments this remains a painful onboarding issue for WSL users.

3. **#7855 — "Response was truncated before completion"**  
   [github.com/earendil-works/pi/issues/7855](https://github.com/earendil-works/pi/issues/7855)  
   Random truncation with any OpenAI-compatible API, reproduced with local VLLM. The user must manually prompt continuation; the root cause is still unclear.

4. **#8105 — Codex materializes optional tool parameters as required**  
   [github.com/earendil-works/pi/issues/8105](https://github.com/earendil-works/pi/issues/8105)  
   With `gpt-5.6-sol`, `strict: null` serialization forces callers to submit every tool property. A subtle interop bug that breaks real-world tool schemas.

5. **#8170 — Windows `bash` tool can kill its own host via `taskkill`**  
   [github.com/earendil-works/pi/issues/8170](https://github.com/earendil-works/pi/issues/8170)  
   A model-generated `taskkill /F /IM node.exe` killed the Pi/pi-web host itself. No confirmation prompt was shown. This is a serious safety gap for Windows users.

6. **#8028 — TUI `fullRender` crashes with `RangeError` on large outputs**  
   [github.com/earendil-works/pi/issues/8028](https://github.com/earendil-works/pi/issues/8028)  
   A video-production agent reading many frames exceeds the V8 string length limit. Crashes the whole process instead of degrading gracefully.

7. **#7765 — Mouse wheel scroll step hardcoded to 1 line**  
   [github.com/earendil-works/pi/issues/7765](https://github.com/earendil-works/pi/issues/7765)  
   Fullscreen TUI mode hardcodes `wheelScrollLines = 1` with no configuration. Closed as no-action, but the request pattern (configurable scroll speed) recurs.

8. **#8003 — Cursor flickers aggressively while streaming**  
   [github.com/earendil-works/pi/issues/8003](https://github.com/earendil-works/pi/issues/8003)  
   The input editor cursor blinks faster and more noticeably during assistant output. A UX annoyance that got worse when typing while generating. Open, but a PR (#8155) may target it.

9. **#8168 — Compaction + session restore corrupts tool-result role**  
   [github.com/earendil-works/pi/issues/8168](https://github.com/earendil-works/pi/issues/8168)  
   After auto-compaction during a tool-heavy turn, the next request fails with a 422 `"Input should be <ChatMessageRole.TOOL: 'tool'>"` — role corruption on restore. Data-integrity issue for long-running sessions.

10. **#4776 — Add shell completion script generator**  
    [github.com/earendil-works/pi/issues/4776](https://github.com/earendil-works/pi/issues/4776)  
    Request for `pi completion <bash|zsh|fish>` subcommands. Closed, but with 5 👍 it reflects a common quality-of-life gap for CLI tooling.

---

## Key PR Progress

1. **#8153 — Compact at safe turn boundaries**  
   [github.com/earendil-works/pi/pull/8153](https://github.com/earendil-works/pi/pull/8153)  
   Adds a run-scoped boundary-compaction API consumed between completed turns. Rebuilds live context in the same run, preserves the native recent tail, and keeps overflow recovery bounded. Directly addresses the compaction pain from #6879.

2. **#8164 — Never continue from trailing assistant message**  
   [github.com/earendil-works/pi/pull/8164](https://github.com/earendil-works/pi/pull/8164)  
   Silent-overflow compaction on a completed turn (`stopReason: 'stop'`) crashed with `"Cannot continue from message role: assistant"`. Fix: only retry mid-flight rejections (`stopReason: 'error'`).

3. **#8165 — tokens.total = billable only (exclude cache tokens)**  
   [github.com/earendil-works/pi/pull/8165](https://github.com/earendil-works/pi/pull/8165)  
   Cache tokens (billed at 1/120th rate) skewed compaction budgets and status stats. Now `total` = input + output only; cache reported separately. Mirrors an earlier `miss-minutes` fix.

4. **#8158 — Upgrade Mermaid terminal rendering**  
   [github.com/earendil-works/pi/pull/8158](https://github.com/earendil-works/pi/pull/8158)  
   Migrates from `grok-mermaid` to `lovely-mermaid`, which has far better parsers and fewer inherited corner cases. Closes #8157 and #7832. Open.

5. **#8155 — Avoid resetting cursor blink during renders**  
   [github.com/earendil-works/pi/pull/8155](https://github.com/earendil-works/pi/pull/8155)  
   Tracks terminal cursor visibility in `TuiBase` and only emits visibility commands on state transitions. Applies to regular and fullscreen renderers; likely fixes the flicker from #8003.

6. **#8151 — Contain widget render failures on extension invalidation**  
   [github.com/earendil-works/pi/pull/8151](https://github.com/earendil-works/pi/pull/8151)  
   A third-party extension (`@marckrenn/pi-sub-bar`) captured extension ctx in a widget closure. On `/reload`, widget registration survived invalidation. Fix tears down ctx-owned widgets properly.

7. **#8181 — Expose low thinking level for DeepSeek V4 Flash**  
   [github.com/earendil-works/pi/pull/8181](https://github.com/earendil-works/pi/pull/8181)  
   Fixes `DEEPSEEK_V4_FLASH_THINKING_LEVEL_MAP` only applying to the `deepseek` provider; opencode and opencode-go now get `low` reasoning effort too.

8. **#8146 — Cap Baseten DeepSeek V4 Flash output at 384k tokens**  
   [github.com/earendil-works/pi/pull/8146](https://github.com/earendil-works/pi/pull/8146)  
   models.dev reports 1,048,576, but Baseten serves 384k max. Requests above fail. Capped `maxTokens` at 384,000.

9. **#8174 — Neutral wording for repeated ambiguous length stops**  
   [github.com/earendil-works/pi/pull/8174](https://github.com/earendil-works/pi/pull/8174)  
   Fixes misleading "Context overflow recovery failed" when the real cause was a second recoverable `length` stop, not context overflow.

10. **#8124 — Route xAI models through Responses, default to Grok 4.6**  
    [github.com/earendil-works/pi/pull/8124](https://github.com/earendil-works/pi/pull/8124)  
    Switches xAI default from Grok 4.5 to 4.6, sends a Pi user agent, and uses the Responses API instead of Completions. Open.

---

## Feature Request Trends

- **Configurable TUI behavior**: recurring requests for scroll-step configuration (#7765), thinking-block max height (#8171), and cursor behavior (#8003). Users want fine-grained control over terminal UX.
- **Extension lifecycle hardening**: multiple issues ask for more extension hooks (`model_select_before`, `ui_dialog_start/end`, compaction error exposure) and safer widget teardown (#7147, #8169, #8175, #8151).
- **Compaction transparency**: users want visible, debuggable compaction decisions — exposed failure events (#8175), boundary-safe compaction (#8153), and better error messages (#8176).
- **Provider parity**: model-specific thinking levels (#8182), provider-specific output caps (#8146), and new built-in providers (LLMTR, #8178) show a demand for uniform multi-provider behavior.
- **Session safety**: exclusive writers for resumed JSONL sessions (#8177) and file restore on `/tree` navigation (#8152) point to reliability concerns for long-lived sessions.

---

## Developer Pain Points

1. **Compaction is unpredictable**: #6879 (auto-compaction not triggering), #8168 (role corruption after restore), #8176 (misleading error messages), and #8175 (silent failures) paint a picture of a subsystem that behaves inconsistently under real workloads.

2. **WSL and Windows are second-class**: #6187 (login hang) and #8170 (`taskkill` self-kill) show platform-specific gaps, with the Windows issue being a genuine safety hazard.

3. **Terminal rendering and streaming UX**: cursor flicker (#8003), scroll-step rigidity (#7765), blank lines from hidden thinking blocks (#8154), and V8 string-limit crashes (#8028) disrupt the core interactive loop.

4. **Provider interop surprises**: `strict` tool-parameter serialization (#8105), inflated output limits (#8146), and model-specific thinking-level maps (#8181) mean every provider integration needs careful validation beyond the documented API.

5. **Session restore fragility**: role corruption (#8168), the trailing-assistant-message crash (#8164), and exclusive-writer ambiguity (#8177) make resuming long sessions a risk rather than a convenience.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-16

## Today's Highlights

The Qwen Code team shipped a new nightly release featuring an autofix footprint gate, while the DSW EAS smoke test chain validated SWE-bench and Terminal-Bench integration end-to-end across five successive runs. A major focus this week continues to be hardening the `/review` command infrastructure, with a wave of issues and PRs addressing concurrency races, worktree leases, and deterministic incremental review plans.

## Releases

**v0.21.11-nightly.20260815.c396fe3d12** — The headline feature is `feat(autofix): deny-by-default footprint gate and positional window censuses`, tightening how autofix findings are scoped. The release also includes a web-shell fix. Multiple DSW EAS SWE + Terminal-Bench smoke runs (r1–r5) all completed successfully, validating the full release pipeline: Release → Action → DSW SWE-bench Verified → Publisher → Terminal-Bench 2.0 → same Release. SWE-bench Verified results were consistently 1/1 resolved with zero errors.

## Hot Issues

1. **[#92.50](https://github.com/QwenLM/qwen-code/issues/9250) — `qwen serve` host writer hard-codes new-file mode 0600** (P3). The built-in text-write tools ignore umask and offer no configuration. Community pushback around Unix permission conventions; 4 comments.

2. **[#7427](https://github.com/QwenLM/qwen-code/issues/7427) — Web-shell artifact panel spams 'Load artifacts failed: Failed to fetch'** (P2, open ~4 weeks). Automatic refresh triggers error toasts repeatedly. Long-standing UI annoyance with 5 comments, still awaiting a fix.

3. **[#9219](https://github.com/QwenLM/qwen-code/issues/9219) — `/review` presubmit overlap detection is exact-line only** (P2). Multi-line ranges and semantic duplicates bypass the noConflict check, allowing redundant review comments. Part of the ongoing review-infrastructure hardening wave.

4. **[#9218](https://github.com/QwenLM/qwen-code/issues/9218) — `/review` presubmit rejects the Step 6 findings artifact** (P2). Path collision between the findings artifact and the skill's example file. Pipeline friction that forces manual rework after hours of analysis.

5. **[#9089](https://github.com/QwenLM/qwen-code/issues/9089) — PAT-bearing autofix jobs share a host with untrusted branch code** (P1, security). Runner-level isolation needed — cannot be fixed from inside a GitHub Actions step. High-priority security concern for the project's own CI.

6. **[#9200](https://github.com/QwenLM/qwen-code/issues/9200) — Inconsistent execution process for identical tasks** (P2). User reports high variance in tracing despite identical inputs; community sentiment is critical of reliability. Needs more info.

7. **[#9230](https://github.com/QwenLM/qwen-code/issues/9230) — Side query defeats server-side prefix caching; `enableCacheSharing` off by default** (P2, performance). Main session gets ~0% prompt-cache reuse on prefix-caching servers. Significant token-cost implication for users running local inference.

8. **[#9205](https://github.com/QwenLM/qwen-code/issues/9205) — Concurrent same-PR reviews race on the fixed worktree path** (P2). Worktree is deleted mid-run by a second session reviewing the same PR. Likely resolved by PR #9211 (worktree lease lock).

9. **[#5966](https://github.com/QwenLM/qwen-code/issues/5966) — Chinese IME completely broken in UI intermittently** (P2, open ~7 weeks). Long-standing input-method bug; user can only type pinyin. High severity for Chinese-speaking users.

10. **[#9219](https://github.com/QwenLM/qwen-code/issues/9219) — CI flakiness wave**: issues #9237, #9239, #9241, #9248 all report main-branch E2E test failures with `autofix/approved` status, suggesting a systematic CI reliability problem under active automated repair.

## Key PR Progress

1. **[#9183](https://github.com/QwenLM/qwen-code/pull/9183) — Scale reverse-audit round cap to diff topology**. Round caps adapt to diff size (10 small, 5 chunked, 3 huge), tuning cost to risk.

2. **[#9247](https://github.com/QwenLM/qwen-code/pull/9247) — Budget composed review body against GitHub's 65,536-char limit**. Deterministic trimming order when overflow occurs. Prevents review-post failures.

3. **[#9211](https://github.com/QwenLM/qwen-code/pull/9211) — Lock PR review worktree lease against concurrent sessions**. Directly addresses issue #9205; lease doubles as a lock consulted before destructive operations.

4. **[#9235](https://github.com/QwenLM/qwen-code/pull/9235) — Redact skill bodies from Web Shell event surface**. Stops leaking full SKILL.md contents to browser clients that don't need them. Security-hardening win.

5. **[#9220](https://github.com/QwenLM/qwen-code/pull/9220) — Self-heal failed checkouts on reused review runners**. Terminal checkout failures now trigger automatic workspace repair on the self-hosted pool.

6. **[#9130](https://github.com/QwenLM/qwen-code/pull/9130) — Deterministic flakiness gate for sandboxed verification**. Re-runs modified unit tests up to 5× (configurable 2–10) after clean install; hardened over 7 review rounds.

7. **[#9191](https://github.com/QwenLM/qwen-code/pull/9191) — Transfer per-file content verdicts across rebases**. Keeps incremental review savings when history is rewritten (rebase/force-push), anchoring on content not commit SHA.

8. **[#9190](https://github.com/QwenLM/qwen-code/pull/9190) — Content-anchored incremental rounds for the local review-fix loop**. Extends incremental review to local dirty-tree rounds, where token costs are highest.

9. **[#9228](https://github.com/QwenLM/qwen-code/pull/9228) — Narrow serve-ab's self-hosted wipe to A/B checkout dirs**. Prevents full workspace deletion (including ~900MB `.git`); prior behavior forced full re-downloads per job.

10. **[#9189](https://github.com/QwenLM/qwen-code/pull/9189) — Defer verified out-of-footprint findings to a follow-up queue**. Adds a fourth disposition to address-review: verified findings outside PR scope are recorded in a machine-readable queue instead of being dropped.

## Feature Request Trends

The dominant theme is **resilient automated review**: resume support (#9153), content-anchored incremental rounds (#9190), deterministic incremental plans (#9188), and per-file verdict transfer across rebases (#9191). Systemically, the project is moving toward a self-healing CI pipeline — flakiness gates, self-repairing checkouts, and lease-based concurrency control. Smaller request directions include `--resume` propagation across all review entry points (#9153), export-path refactoring using WebShellTranscript (#9186), and per-file verdict persistence for long-lived PRs.

## Developer Pain Points

- **Worktree races**: Multiple sessions reviewing the same PR collide on fixed paths; worktrees deleted mid-run destroy hours of analysis. Pressure for lock-based leases is high.
- **CI flakiness**: A burst of main-branch E2E failures this week (4+ issues) is being addressed by the flakiness gate (#9130) and self-healing checkouts (#9220), but the problem isn't fully contained.
- **Presubmit schema friction**: `/review`'s last-gate validation rejects its own pipeline output (issues #9218, #9209), forcing manual rework after multi-hour runs.
- **Token waste**: Prefix-cache defeats (#9230) and non-incremental local review loops (#9190) both burn tokens unnecessarily — a cost-sensitive pain point for self-hosters.
- **User-facing stability**: Chinese IME failures (#5966) persist for 7+ weeks, and OOM with terminal corruption (#9198) indicates mid-session reliability gaps remain.
- **Pipe-owner friction**: `/statusline` dialog clipping in short terminals (#9037) and manual session names being lost after `/clear` (#8977) are small but irksome UX regressions.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-16

## Today's Highlights
The v0.9.8 stabilization wave dominates today's activity, with maintainers landing a dense cluster of fixes for red CI across platforms (macOS symlink failures, provider-count assertion drift, and cancel-in-progress killing concurrent builds). The web UI is under active repair (#5370), and a three-week translation debate over "Constitution" resolved with "宪章" (charter) as the settled term, already merged into the TUI localization. Several large feature PRs — provider templates (#5406), configurable read/tool-result budgets (#5405), and SSE UTF-8 splitting fixes (#5404) — are open and awaiting review.

## Releases
No new releases in the last 24 hours. The v0.9.8 cut is being finalized through PR #5407.

## Hot Issues

**1. [#5316 — EPIC-005: CodeWhale TUI Crate Decomposition (Umbrella)](https://github.com/Hmbown/CodeWhale/issues/5316)**  
The architectural tracking issue for decomposing the TUI crate. 7 comments, still open. This is the structural roadmap the community should monitor for long-term codebase direction.

**2. [#5374 — [bug] The writing its weird (the agent)](https://github.com/Hmbown/CodeWhale/issues/5374)**  
Critical rendering bug on macOS: streaming agent text shows corrupted characters (U+FFFD/CJK garbling). 5 comments, open. PR #5404 targets this directly — SSE UTF-8 split across HTTP/2 DATA frames. High-impact for macOS users.

**3. [#5322 — [bug] Regression: output area doesn't fill wide terminals](https://github.com/Hmbown/CodeWhale/issues/5322)**  
Closed by PR #5400. v0.9 introduced a max-width cap that broke v0.8.65 behavior on wide displays. Community reported cramped text with unused white space; fix restores identity `session_shell_area`.

**4. [#5370 — [bug] P0: web UI looks broken — audit and rebuild](https://github.com/Hmbown/CodeWhale/issues/5370)**  
Maintainer-reported P0: the public web UI is "totally broken" in look and features. Scoped to both the public Next.js app and the managed CWC app. 2 comments, open. This funnels into PR #5411's model-settings rebuild.

**5. [#5350 — [enhancement] Simplify third-party model config with pre-built templates](https://github.com/Hmbown/CodeWhale/issues/5350)**  
Chinese-language request: manual Base URL/model/key setup for OpenCode Zen, OpenCode Go, Agnes, Sensenova is painful; states stuck at `not checked`/`cache failed`. 3 comments, open. PR #5406 implements it.

**6. [#5241 — Pricing endpoint returns 503 - all sessions show unverified_live_pricing](https://github.com/Hmbown/CodeWhale/issues/5241)**  
Cost display broken after 0.8.67→0.9.3 upgrade: every session shows `unverified_live_pricing`. 2 comments, open. PR #5402 restores honest session costs when live pricing verification fails.

**7. [#5367 — Feature Request: Configurable model-visible read/tool-result size limits](https://github.com/Hmbown/CodeWhale/issues/5367)**  
Self-hosted long-context DeepSeek V4 users hit conservative ceilings (read 50 KiB, tool-result 12K chars) causing ~20 extra reads on a 64 KiB file. 3 comments, open. PR #5405 implements configurable budgets.

**8. [#4949 — Discussion: Chinese Translation of "Constitution" — "宪法", "协作准则", or Something Else?](https://github.com/Hmbown/CodeWhale/issues/4949)**  
CLOSED after 17 comments. Three-week translation debate settled on "宪章" (charter). TUI merged it in `cf08cb6af`; PR #5397 applies it to the web. Notable for showing the community's care for i18n precision and political sensitivity.

**9. [#5392 — agy_credentials tests fail on every macOS run: symlink refusal](https://github.com/Hmbown/CodeWhale/issues/5392)**  
Closed by PR #5396. `open_secure_regular_file` refuses symlinks at any path component; macOS temp dirs live under `/var` which is one. Not a flake — every macOS CI run failed deterministically.

**10. [#5403 — main is red on both platforms across all four completed runs](https://github.com/Hmbown/CodeWhale/issues/5403)**  
After #5395 stopped runs from cancelling each other, four completed runs turned red on both macOS (plugin_e2e_acceptance) and Windows (NSIS provisioning). Signals CI health debt from the v0.9.8 window.

## Key PR Progress

**1. [#5395 — fix(ci): stop cancel-in-progress from killing concurrent main pushes](https://github.com/Hmbown/CodeWhale/pull/5395)** — CLOSED.  
Critical CI fix: main-branch runs shared one concurrency group, so later pushes cancelled earlier runs mid-flight. Failing assertions never turned red. This was masking all subsequent breakage.

**2. [#5399 — fix(tui): v0.9.8 stabilization — turn-owned agents, compaction quality, Blue Stage web](https://github.com/Hmbown/CodeWhale/pull/5399)** — CLOSED.  
Large stabilization landing on current main: turn-owned default direct subagents, compaction quality fixes, Blue Stage web. No version bump or tag — reconstruction of the missing Rust stabilization.

**3. [#5400 — fix(tui): fill transcript to full terminal width (#5322)](https://github.com/Hmbown/CodeWhale/pull/5400)** — CLOSED.  
Restores v0.8.65 behavior: transcript and composer fill host width on wide terminals. `session_shell_area` is an identity again.

**4. [#5404 — fix(client): fail closed on SSE UTF-8 split across HTTP/2 DATA (#5374)](https://github.com/Hmbown/CodeWhale/pull/5404)** — OPEN.  
Fixes garbled streaming text on macOS/DeepSeek Flash. HTTP/2 DATA can split multi-byte characters; the fix decodes safely rather than using `String::from_utf8_lossy`.

**5. [#5406 — feat(tui): prefab provider templates and test-connection (#5350)](https://github.com/Hmbown/CodeWhale/pull/5406)** — OPEN.  
Implements built-in templates for OpenCode Zen, OpenCode Go, Agnes, SenseNova — users only enter an API key. Includes a test-connection button to break stuck `not checked` states.

**6. [#5405 — feat(tui): configurable model-visible read/tool-result budgets (#5367)](https://github.com/Hmbown/CodeWhale/pull/5405)** — OPEN.  
For self-hosted long-context models: optional larger per-result budgets (read, read_file, tool-result wire size). Directly reduces token waste on large files.

**7. [#5402 — fix(tui): restore session cost when live pricing is unverifiable (#5241)](https://github.com/Hmbown/CodeWhale/pull/5402)** — OPEN.  
Honest-path fix: session costs no longer stay `unverified_live_pricing` forever when the pricing endpoint 503s (including `control_plane_not_attached`).

**8. [#5401 — fix: CodeQL Highs (#107, #88–#106) and prepare GHSA-8hp3 / GHSA-3mgh](https://github.com/Hmbown/CodeWhale/pull/5401)** — OPEN.  
Security slice only: fixes clear-text logging (CodeQL #107) and prepares two GHSA advisories. Explicitly does NOT tag a release — security hygiene decoupled from release cadence.

**9. [#5396 — fix(tui): canonicalize agy_credentials fixtures for macOS (#5392)](https://github.com/Hmbown/CodeWhale/pull/5396)** — CLOSED.  
Test fixture fix: canonicalize temp paths so `/var/folders/...` is resolved through the symlink before asserting secure-open behavior. Production code untouched.

**10. [#5397 + #5398 — fix(web): charter terminology + regenerate facts for v0.9.8 providers](https://github.com/Hmbown/CodeWhale/pull/5397)** — CLOSED (both).  
Together: apply the "宪章/charter" term to the website (following #4949's outcome) and regenerate `facts.generated.ts` to unblock the required `check:facts` lint gate.

## Feature Request Trends
- **Simplified third-party provider onboarding** (#5350, #5406): Users consistently struggle with manual Base URL/model/API key configuration. The community wants prefab templates, embedded docs, and test-connection buttons — one-minute setup, not research projects.
- **Configurable limits for self-hosted models** (#5367, #5405): Long-context self-hosters are hitting conservative, hardcoded ceilings on `read`/`read_file`/tool result sizes. Clear demand for model- or profile-level tunable budgets.
- **Web UI parity maintenance** (#5370, #5411): The public web UI has drifted from the TUI's feature surface. Requested direction: rebuild against harness references and expose read-only settings previews with real configuration actions.
- **i18n precision** (#4949, #5397): The community cares about non-political, accurate translations. The three-week constitution/charter debate signals a standard for culturally-safe terminology.

## Developer Pain Points
- **CI red through the v0.9.8 window**: Provider-count assertions (#5383), macOS symlink TempDir failures (#5392), and cancel-in-progress masking failures (#5395) — a cascade of CI debt that blocked merges and hid breakage.
- **macOS-specific bugs are recurring**: SSE UTF-8 splitting (#5374), symlink refusals in secure-open (#5392), plugin PTY keep-alive hangs (#5408). Each requires a platform-specific fix, hinting at a need for a dedicated macOS CI matrix improvement.
- **Web/TUI feature drift**: The web app lags the TUI in features and is currently "totally broken" per maintainers (#5370). Developers inheriting the headless web work face an audit-and-rebuild effort.
- **Self-hosted configuration friction**: Manual provider setup and opaque `not checked`/`cache failed` states (#5350) cost users significant debugging time; the pricing endpoint 503 (#5241) doubles the pain by hiding cost data entirely.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*