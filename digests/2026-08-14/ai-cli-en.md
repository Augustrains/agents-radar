# AI CLI Tools Community Digest 2026-08-14

> Generated: 2026-08-14 00:54 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Developer Tools Comparison Report — 2026-08-14

## 1. Ecosystem Overview

The AI CLI tooling landscape remains intensely competitive and rapidly evolving, with all seven major tools shipping updates within the last 24 hours. While **Claude Code** and **OpenAI Codex** lead in community engagement and feature velocity, challengers like **Gemini CLI** and **Qwen Code** are aggressively closing gaps in multi-agent orchestration and enterprise integrations. The most significant cross-cutting theme this week is **reliability and trust**: every tool faces backlash around context compaction, session limits, and silent failures. Security hardening is also accelerating, with CLI tools becoming critical supply-chain infrastructure — evidenced by Gemini CLI's CVE fixes, OpenCode's external security audit, and Claude Code's CI supply-chain pinning. The market is bifurcating into power-user CLI-first tools (Claude Code, Codex, Gemini CLI) and hybrid desktop/IDE experiences (Qwen Code, OpenCode, CodeWhale), with MCP protocol support emerging as the universal integration standard across all platforms.

---

## 2. Activity Comparison

| Tool | Hot Issues (New/Active) | PRs (24h) | Release Status | Key Release |
|------|------------------------|-----------|-----------------|-------------|
| **Claude Code** | 10 tracked (1 new #86012) | 2 | **Shipped** v2.1.232, v2.1.231 | Subagent forking, session mentioning |
| **OpenAI Codex** | 10 tracked (2 new: #38455, #38466) | 10+ merged | **Pre-release** 3 alphas | 0.148.0-alpha.11–.13 |
| **Gemini CLI** | 10 tracked (2 new: #26522, #26525) | 10 merged | **Nightly** v0.56.0-nightly | Eval tooling, security fixes |
| **Copilot CLI** | 10 tracked (5 new triage) | 1 (24h); 10 weekly | **Shipped** v1.0.80-0 | `--enable-mcp-server`, shared session indicators |
| **Kimi Code CLI** | 3 tracked (2 serious bugs) | 0 | **No release** | — |
| **OpenCode** | 10 tracked (5 new) | 10 merged | **Shipped** v1.18.18 | Provider fixes (Kimi/xAI) |
| **Pi** | 10 tracked (1 new: #8055) | 10+ merged | **No release** | — |
| **Qwen Code** | 10 tracked (5 new) | 10+ merged | **Shipped** v0.21.12-preview.1 | Workflow state, review resume |
| **CodeWhale (DeepSeek)** | 10 tracked | 10 merged | **Shipped** v0.9.7 | CodeWhale rebrand, DS4 setup |

**Release velocity leaders:** Claude Code (2 releases), OpenAI Codex (3 pre-releases), Qwen Code (2 releases), Copilot CLI (1 release).

---

## 3. Shared Feature Directions

### 3.1 Persistent Context & Memory (7/7 tools)
- **Kimi** (#1283, most-voted), **OpenCode** (#42425 PR `agent_memory` table), **Claude Code** (cross-session continuity), **Codex** (compaction fixes #38445), **Pi** (#6879 compaction), **Gemini** (Auto Memory #26522), **Qwen** (run-session state)
- **Core need:** Seamless context carryover across sessions, with predictable compaction and no silent data loss.

### 3.2 Multi-Agent Orchestration & Subagent Reliability (7/7 tools)
- **Claude Code** (subagent forking), **Codex** (multi_agent_v2 #34700), **Gemini** (#22323 false success), **Qwen** (`/coordinate`, read-only teammates), **OpenCode** (running-subagents sidebar #42369), **CodeWhale** (#5324 32-field schema), **Pi** (agent turn compaction)
- **Core need:** Reliable subagent lifecycle, honest completion reporting, and leader/worker orchestration with observable state.

### 3.3 MCP Ecosystem Maturity (6/7 tools)
- **Claude Code** (OAuth fix, permission fatigue #81535), **Codex** (per-server OAuth ports #38448, fd leaks #26984), **Copilot** (case-insensitive collisions #4478, retry/backoff), **Gemini** (config defaults #28787), **Qwen** (Desktop OAuth #9108), **CodeWhale** (MCP pagination #5336)
- **Core need:** Reliable OAuth flows, fd/resource cleanup, schema fidelity, and granular per-server control.

### 3.4 Windows Support Parity (6/7 tools)
- **Claude Code** (GPU crashes, MSIX), **Codex** (12 of top-30 issues Windows-tagged), **Qwen** (Ctrl+V paste death #9061), **Copilot** (MSIX pwsh), **CodeWhale** (sandbox SSH block #1829), **OpenCode** (console flashing #42440)
- **Core need:** First-class Windows QA, sandbox compatibility, and i18n/IME support.

### 3.5 Context Compaction & Cost Transparency (6/7 tools)
- **Claude** (#63930 74% cache waste), **Codex** (#31198 145GiB logs), **Pi** (#6879 auto-compaction failure), **OpenCode** (#42448 exceeds window, #42437 drops constraints), **Gemini** (#26522 infinite retries), **Kimi** (#2597 88k-token garbage)
- **Core need:** Predictable compaction, hard generation limits, no silent content loss, honest cost metering.

### 3.6 Terminal UX & Rendering Fidelity (5/7 tools)
- **Pi** (CJK widths #8055, OSC52 clipboard #7761), **Codex** (LaTeX math #18906), **CodeWhale** (Chinese truncation #998, quote rails #5364), **Gemini** (TUI polish), **Kimi** (streaming hangs #2598)
- **Core need:** Correct rendering across locales, reliable clipboard, responsive editors on large buffers.

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach | Key Differentiator |
|------|---------------|-------------|-------------------|---------------------|
| **Claude Code** | Enterprise power-user workflows | Professional developers in large orgs | Heavy multi-session coordination, prompt-cache optimization | Cross-session collaboration (`@` mentions), forked subagents with full inheritance |
| **OpenAI Codex** | Desktop/IDE-integrated agentic coding | VS Code/desktop-first developers | Rust-native CLI, Guardian safety layer, sandboxing | Deep IDE integration, multi-agent v2, strongest safety review (Guardian) |
| **Gemini CLI** | Fusion of agent-first + bash-native workflows | Developers wanting AI with trust | Zero-cost context retention, Agent-to-Agent (A2A) protocol | Bash affinity + OS-level sandboxing vision, behavioral eval discipline |
| **Copilot CLI** | GitHub-native, configurable agent fleet | GitHub-centric teams | TUI with hooks, MCP first-class, custom `.agent.md` config | Per-agent configuration, GitHub ecosystem integration, plugin system |
| **Qwen Code** | Multi-agent fleet orchestration | Alibaba cloud / international hybrid | `/coordinate` command, supervised teammates, workflow state machines | Read-only teammate runtime, review pipelines (`fetch-pr --resume`) |
| **OpenCode** | Open-source, transparent, community-driven | Indie devs & security-minded orgs | V1/V2 dual runtime, provider-agnostic, memory-first | Community governance, rapid iteration, self-hosted-friendly |
| **Pi** | Minimal TUI, performance-obsessed | Terminal purists & OSS maintainers | Bare-bones TUI, GitOps-style changes, community PR velocity | Speed (viewport rendering), simplicity, enthusiastic OSS community |
| **CodeWhale (DeepSeek)** | Low-cost deepseek + Codex semantics | Cost-sensitive developers | Rebranded TUI with provider abstraction, Auto-Review guardian | Price-performance leader, local-first DS4 setup, multi-provider (Kimi/NVIDIA NIM) |

---

## 5. Community Momentum & Maturity

### Most Active Communities (Issue Engagement)
1. **Claude Code** — 832-comment session-limit thread; 474+ upvotes; 723-upvote feature request; **largest sustained engagement**
2. **OpenAI Codex** — 53-comment extension failure; 36-upvote model support gap; **rapidly growing**
3. **OpenCode** — 41-upvote layout preservation; 37 comments; security-audit attention
4. **Pi** — 17-upvote compaction issue; PR merged within 24h of bug report → **most responsive maintainers**
5. **Qwen Code** — 9-comment RFC driving major architectural direction
6. **Copilot CLI** — 20-upvote effort config; 5 new issues in triage → **active triage but slower PR velocity**
7. **CodeWhale** — 11 comments on i18n truncation; legacy-rename friction
8. **Gemini CLI** — 12 comments on max-turns false reporting; nightly release cadence
9. **Kimi Code** — Lowest engagement; only 3 tracked issues; **most fragile community** (hangs, no releases)

### Iteration Velocity (PRs merged per 24h)
| Tier | Tools |
|------|-------|
| **High (10+ PRs/24h)** | Codex, Gemini, OpenCode, Qwen, Pi, CodeWhale |
| **Medium (2–10 PRs/24h)** | Claude Code |
| **Low (0–1 PR/24h)** | Copilot CLI, Kimi |

### Maturity Signals
- **Claude Code** and **Codex** have the most polished user experience but face trust issues around usage metering and stability regressions.
- **Pi** shows the healthiest OSS community dynamics: correlated bug reports → PRs within 24h.
- **Gemini CLI** demonstrates exceptional security discipline (CVE fixes, A2A auth enforcement) despite smaller community.
- **CodeWhale** is transitioning brand identity and consolidating architecture — risky but forward-moving.
- **Kimi Code** is dangerously quiet — no 24h PR/release activity with two P1 bugs open.

---

## 6. Trend Signals

### For Developers — Critical Watch Items

1. **Context compaction is the #1 trust-killer.** Across 6/7 tools, users report silent content loss, unbounded output, or cost surprises. If your workflow depends on long-running sessions, monitor compaction behavior carefully. Consider tools with explicit compaction policies (Pi's preemptive checks, Codex's `retain_client_developer_messages`).

2. **Multi-agent is moving to production, but false success is common.** Gemini's #22323 (GOAL reported when turns exhausted) and CodeWhale's #5324 (schema complexity causing errors) show that orchestration features are ahead of reliability. **Verify subagent completion criteria** before trusting delegated work.

3. **Windows remains the weak link for all tools.** If your team is Windows-heavy, expect friction — GPU crashes (Claude), sandbox failures (Codex, CodeWhale), clipboard regressions (Qwen), IME issues (CodeWhale). Budget for OS-specific workarounds.

4. **MCP is the integration backbone — and it's still rough.** OAuth flows are breaking across Claude, Copilot, and Codex. fd leaks affect long sessions. **Pin MCP server versions** and test OAuth flows after every tool update.

5. **Security posture is differentiating quickly.** Gemini's rapid CVE fixes, Claude's CI supply-chain pinning, and OpenCode's external audit response signal that enterprise buyers should weigh each tool's security team responsiveness. **CodeWhale/DeepSeek** leading in security (third-party audit already in progress) though shipping changes to their security posture is still ongoing.

6. **Cost plumbing is increasingly transparent — and controversial.** Claude's 74% cache waste and Codex's 145GiB logs show the full cost of agentic workflows. **Set up token-budget alerts** and regularly audit session storage.

### For Tool Vendors — Strategic Signals

| Signal | Tools Demonstrating It | Action Implication |
|--------|----------------------|---------------------|
| **Memory is table stakes** | Kimi (1283), OpenCode (#42425), Pi (#6879), Codex (#38445) | Ship a memory system before competitors define the standard |
| **Fleet orchestration is differentiating** | Qwen (`/coordinate`), Claude (forking), Codex (multi-agent v2) | Subagent reliability, not just availability, is the winner |
| **Eval-driven development is emerging** | Gemini (#24353, #28804), Qwen (#9086 regression tests), Pi (behavioral evals) | Test with real-world PRs, not synthetic benchmarks |
| **Google Cloud support is a gap** | Qwen (#9019, #9025), Gemini (Vertex AI) | Enterprise users on GCP need first-class Vertex AI auth, not workarounds |
| **Desktop is the new battlefield** | Claude (Windows crashes), Codex (OOM), Qwen (#9108), Copilot (remote) | Desktop stability beats new features for adoption |
| **Dual runtime migration is risky** | OpenCode (V1/V2), CodeWhale (rename), Claude (auto-update regressions) | Plan migration paths that preserve sessions, config, and permissions |

---

## Final Recommendation Summary

| Use Case | Top Tool | Key Caveat |
|----------|----------|------------|
| **Enterprise power workflows, cross-session collaboration** | Claude Code | Watch session-limit metering; verify Windows GPU stability |
| **Desktop/IDE-integrated agentic coding** | OpenAI Codex | Monitor subagent thread bloat and context compaction damage |
| **Bash-native automation with security focus** | Gemini CLI | Subagent false-success reporting needs verification |
| **GitHub-centric, configurable agent fleet** | Copilot CLI | MCP OAuth reliability and per-agent effort config are pending |
| **Low-cost, multi-provider flexibility** | CodeWhale (DeepSeek) | Wait for v0.9.8 stabilization; 32-field schema blocker active |
| **Open-source, transparent, community-driven** | OpenCode | V2 transition unresolved; desktop regression open 10 days |
| **Terminal purists, performance-critical** | Pi | Smallest feature surface; best community responsiveness |
| **Chinese/Asian market, Alibaba Cloud** | Qwen Code | Windows clipboard regression; Vertex AI auth broken |

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

*Data as of 2026-08-14 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Skills have generated the most community discussion and attention:

### #1 — skill-creator fixes (Windows compatibility + eval reliability)
**PRs #1298, #1099, #1050, #539** | Status: **Open**
The most active cluster of discussion centers on **skill-creator's broken evaluation loop**. Multiple independent developers (MartinCajiao, joshuawowk, gstreet-ops, Lubrsy706) have submitted fixes for the same root causes: `run_eval.py` reports `recall=0%` on every iteration (issue #556, 10+ reproductions), Windows subprocess pipe handling crashes (`WinError 10038`, `WinError 2` with `claude.cmd`), and YAML parsing failures from unquoted descriptions containing colons. This is the single most-commented topic in the repository and directly blocks the skill-development workflow.
→ [PR #1298](https://github.com/anthropics/skills/pull/1298) · [PR #1099](https://github.com/anthropics/skills/pull/1099) · [PR #1050](https://github.com/anthropics/skills/pull/1050) · [PR #539](https://github.com/anthropics/skills/pull/539) · [Issue #556](https://github.com/anthropics/skills/issues/556)

### #2 — document-typography
**PR #514** | Author: PGTBoos | Status: **Open**
Typographic quality control for AI-generated documents: prevents orphan word wrap, widow paragraphs, and numbering misalignment — issues that affect every document Claude generates. The discussion highlights a **cross-cutting quality problem** that applies regardless of document type, making this a high-value general-purpose skill.
→ [PR #514](https://github.com/anthropics/skills/pull/514)

### #3 — ODT skill (OpenDocument)
**PR #486** | Author: GitHubNewbie0 | Status: **Open**
Adds creation, template-filling, and ODT→HTML conversion for OpenDocument formats (.odt, .ods). Complements the existing docx and pdf skills, addressing LibreOffice/ISO-standard document workflows. Discussion centers on the trigger surface (ODT, ODS, ODF, OpenDocument mentions) and coverage breadth.
→ [PR #486](https://github.com/anthropics/skills/pull/486)

### #4 — DOCX tracked-change w:id collision fix
**PR #541** | Author: Lubrsy706 | Status: **Open**
Fixes document corruption when adding tracked changes to docs with existing bookmarks. Root cause: OOXML's shared `w:id` space across bookmarks, tracked changes, comments, and move ranges; the SKILL.md examples used hardcoded low IDs (1, 2, 3) that collide. A subtle, well-documented bug fix with clear technical depth.
→ [PR #541](https://github.com/anthropics/skills/pull/541)

### #5 — self-audit skill
**PR #1367** | Author: YuhaoLin2005 | Status: **Open**
Mechanical file verification first, then four-dimension reasoning audit in damage-severity priority order. Positioned as universal (any project, tech stack, model). The companion issue #1385 proposes a three-gate pipeline (pre-task calibration → adversarial review → delivery verification) with two gates already implemented. Discussion focuses on the "reasoning quality gate" concept as a best practice layer for all skills.
→ [PR #1367](https://github.com/anthropics/skills/pull/1367) · [Issue #1385](https://github.com/anthropics/skills/issues/1385)

### #6 — testing-patterns
**PR #723** | Author: 4444J99 | Status: **Open**
Comprehensive testing skill covering the full stack: Testing Trophy model, unit testing (AAA pattern, naming, pure functions, edge cases), React component testing via Testing Library, and what-to-test vs. what-NOT-to-test philosophy.
→ [PR #723](https://github.com/anthropics/skills/pull/723)

### #7 — ServiceNow platform skill
**PR #568** | Author: Vanka07 | Status: **Open**
Broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD/CSM, SPM/PPM, Vulnerability Response, and Security Incident Response. The longest-running open PR (created 2026-03-08, still updated 2026-08-12) — a substantial enterprise skill with ongoing refinement.
→ [PR #568](https://github.com/anthropics/skills/pull/568)

### #8 — pyxel retro game development
**PR #525** | Author: kitao | Status: **Open**
Skill wrapping the pyxel-mcp server for the Pyxel retro/pixel-art/8-bit game engine (Python). Covers the write → run_and_capture → inspect → iterate workflow. Notable for being a **game-dev skill with an MCP dependency** — a pattern the community is watching.
→ [PR #525](https://github.com/anthropics/skills/pull/525)

---

## 2. Community Demand Trends

Distilled from the most-commented issues:

1. **Skill-development tooling reliability (dominant trend).** The #1 demand is fixing `skill-creator`'s evaluation loop (#556: 12 comments, #1169: 3 comments) and Windows compatibility. The community's ability to *create* high-quality skills is currently blocked by a tool that reports `recall=0%` for every description. Until this is fixed, all other contributions are flying blind.

2. **Trust boundary & security.** Issue #492 (43 comments, the most-commented issue in the repo) flags community skills distributed under the `anthropic/` namespace impersonating official skills — a trust boundary abuse where users may grant elevated permissions to skills they believe are official. This is the community's #1 **governance** concern.

3. **Org-wide sharing & distribution.** Issue #228 (16 comments, 8👍) requests direct org-level skill sharing in Claude.ai, removing the manual download/upload dance via Slack/Teams. Complements the trust-boundary issue — both point to a need for **managed distribution**.

4. **Context-window efficiency.** Issue #1487 documents the `claude-api` skill eagerly injecting ~156k tokens in a single tool call, exhausting the context window. Combined with Issue #189 (duplicate skills from `document-skills` + `example-skills` plugins inflating context), there's a clear demand for **smaller, leaner skills**.

5. **Specialized production formats.** Continued demand for non-mainstream document formats (ODT, SharePoint Online-specific guidance via #1175) and platform-specific skills (ServiceNow) — not just the PDF/DOCX staples.

---

## 3. High-Potential Pending Skills

These active PRs have generated meaningful discussion and are strong candidates to land soon:

| Skill | PR | Why it may land |
|---|---|---|
| **document-typography** | [#514](https://github.com/anthropics/skills/pull/514) | Solves a universal problem (orphan words, widow paragraphs) affecting every generated doc; low risk, high polish. |
| **ODT skill** | [#486](https://github.com/anthropics/skills/pull/486) | Fills an obvious gap in the document-format family (docx, pdf exist); ISO/open-source demand is growing. |
| **self-audit** | [#1367](https://github.com/anthropics/skills/pull/1367) | A cross-cutting "quality gate" concept that could become a base pattern for all skills; author has a companion proposal in #1385. |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Fills a core engineering gap (no dedicated testing skill exists today); well-scoped coverage. |
| **skill-quality-analyzer / skill-security-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Meta-skills that directly address the #1 community concern (trust boundary abuse) and #2 concern (eval reliability). High strategic value. |
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Addresses planning-artifact accumulation with no lifecycle (#1417); structured around community feedback from multiple contributors. |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for meta-skill infrastructure — reliable evaluation tooling, trust-boundary safety, and context-window discipline — not for new domain functionality itself, indicating the ecosystem has matured past "what should a skill do" and is now focused on "how do we build and distribute skills safely and correctly."**

The clearest signal: the top three discussion threads (#556 eval failure, #492 trust boundary abuse, #228 org sharing) are all about the *plumbing* of the skills ecosystem, not the *content* of individual skills. The single most-blocking issue is that skill-creator's eval loop is provably broken (`recall=0%` on every query, 10+ independent reproductions), meaning every description-optimization cycle is currently "optimizing against noise." Until that's fixed, PR velocity and quality will remain constrained.

---

# Claude Code Community Digest — 2026-08-14

## Today's Highlights

Two releases shipped in the last 24 hours: v2.1.232 enables **subagent forking by default** (forked subagents inherit the full conversation and prompt cache, and non-teammate agent spawns now run in the background automatically), plus support for **mentioning another Claude session by name** with `@`. The smaller v2.1.231 fixes a notable MCP OAuth issue where pre-registered OAuth clients (e.g., Slack) failed sign-in due to redirect URI mismatch. Meanwhile, the community is heavily focused on **Windows desktop app regressions** around cross-session messaging, GPU crashes, and permission handling — several issues filed this week are drawing rapid triage attention.

---

## Releases

### v2.1.232
- **Subagent forking now enabled by default**: `subagent_type: "fork"` inherits the full conversation and prompt cache, enabling more context-aware parallel work.
- **Background execution default**: Non-teammate agent spawns in interactive sessions now run in the background by default, reducing UI blocking.
- **Session mentioning**: Type `@` in the prompt to reference another Claude session by name, enabling cross-session coordination.

### v2.1.231
- **MCP OAuth fix**: Resolved redirect URI mismatch that broke sign-in for servers using pre-registered OAuth clients, specifically called out for Slack.

---

## Hot Issues

1. **[#38335 — Claude Max plan session limits exhausted abnormally fast (832 comments, 474 👍)](https://github.com/anthropics/claude-code/issues/38335)**  
   A long-running complaint (since March) about plan session limits being consumed too quickly in CLI usage. This remains the most-engaged issue in the repo, indicating significant user frustration with usage metering. The sustained 832-comment thread suggests users are closely tracking and debating consumption patterns.

2. **[#18435 — Feature: multi-account profiles in Claude Desktop (165 comments, 723 👍)](https://github.com/anthropics/claude-code/issues/18435)**  
   The single most-upvoted feature request: easy switching between multiple Claude accounts with profiles in the Desktop app. The high ratio of upvotes to comments (723:165) signals broad, silent demand — this is likely a top candidate for roadmap prioritization.

3. **[#80988 — `heron_brook` prompt section overrides delegation policy for Opus 5 (23 comments, 49 👍)](https://github.com/anthropics/claude-code/issues/80988)**  
   Since v2.1.219, a system-prompt section injects "Do not call the AgentTool unless the user requested it" for Opus 5 only, silently overriding user-configured delegation policy with no opt-out. The community is concerned about loss of control over agent delegation behavior.

4. **[#81698 — Windows Desktop GPU process crash kills entire app (28 comments)](https://github.com/anthropics/claude-code/issues/81698)**  
   Exit code 101457950 on Windows 11 with RTX 5080; entire app and all running sessions are lost. This is part of a **cluster of related GPU crash reports** (#81341, #83403, #82967) that suggests a broader Electron/GPU stability problem on Windows.

5. **[#86012 — Cross-session messages leave recipient unresponsive (14 comments)](https://github.com/anthropics/claude-code/issues/86012)**  
   Newly filed (2026-08-12), this bug causes the recipient session to hang with `hadFirstResponse=false` for 15-20 minutes until the idle-timeout kills it. This joins a growing set of **cross-session messaging regressions** on the desktop app (also #86275, #86298, #86385).

6. **[#82536 — `--continue` cannot find sessions created by `-p` (13 comments)](https://github.com/anthropics/claude-code/issues/82536)**  
   Interactive resume fails for sessions created via print mode. This breaks a fundamental workflow — session continuity — and needs a fix soon.

7. **[#29717 — SSH_AUTH_SOCK missing from CC_ENV_EXTRACT_LIST breaks 1Password SSH agent (12 comments, 23 👍)](https://github.com/anthropics/claude-code/issues/29717)**  
   Desktop app breaks SSH connections for users of non-default SSH agents like 1Password. A configuration whitelist omission with broad security-tooling implications.

8. **[#63930 — Prompt cache re-created after parallel tool calls; 74% cache writes wasted (10 comments)](https://github.com/anthropics/claude-code/issues/63930)**  
   Since Opus 4.7 → 4.8 switch, the prompt cache is repeatedly invalidated mid-session, collapsing `cache_read` to system+tools floor. This is a **cost concern** — users report significant token waste on expensive models.

9. **[#70647 — Native installer produces unsealed macOS app bundle (10 comments)](https://github.com/anthropics/claude-code/issues/70647)**  
   `ClaudeCode.app` from the native installer lacks code-signing seal, causing macOS to reject it as "damaged." A packaging pipeline issue that blocks installation entirely.

10. **[#83403 — Desktop crashes on Cloudflare Turnstile browser preview (9 comments)](https://github.com/anthropics/claude-code/issues/83403)**  
    GPU process crash on rendering Turnstile captchas, reproducible across machines; app becomes unlaunchable afterwards. This is concerning for users browsing sites with bot protection.

---

## Key PR Progress

> **Note:** Only 2 PRs were updated in the last 24h. The following list includes the most notable recent activity in the repo context.

1. **[#86537 — Fix duplicated word in CHANGELOG.md](https://github.com/anthropics/claude-code/pull/86537)**  
   Documentation-only typo fix ("to to" → "to") for the `CLAUDE_BASH_NO_LOGIN` changelog entry. Small but keeps release notes clean.

2. **[#60280 — chore(ci): SHA-pin remaining actions/checkout and actions/github-script](https://github.com/anthropics/claude-code/pull/60280)**  
   Supply-chain hardening: pins `actions/checkout@v4` to SHA `34e114…` and `actions/github-script` in 6 workflows (`auto-close-duplicates`, `backfill-duplicate-comments`, `claude-dedupe-issues`, `claude-issue-triage`, etc.). Follow-up to #56784; good security hygiene.

3. **Context: Prior PR #56784** — Initial SHA-pinning pass; this follow-up completes the coverage. Commits are verified against v4.3.1.

---

## Feature Request Trends

Distilled from all open issues, the community is pushing in these directions:

1. **Multi-account / multi-profile management** (#18435, 723 👍) — Dominant request: easy profile switching within Claude Desktop for users with multiple accounts (personal, work, clients).

2. **Cross-session & cross-surface continuity** — Sync conversation history between CLI and Desktop app (#28791, 123 👍); mention and interact with other Claude sessions by name (shipped in v2.1.232); persistent cross-session messaging without hangups.

3. **Fine-grained permission and delegation control** — Users want explicit opt-out for injected prompt sections (#80988), honoring of `permissions.allow` entries for MCP tools (#81535, #80658), and bypass-mode exemptions for preview starts (#86175).

4. **Stability hardening for desktop GPU rendering** — Multiple reports of GPU process crashes on Windows (#81698, #81341, #83403, #82967) indicate demand for a more robust Electron/Chromium GPU layer.

5. **Reliable background task lifecycle management** — Issues around background tasks leaking (#86345), completing with empty results (#86471), and team registry bloat across `/clear` (#86518) point to a need for better long-running agent lifecycle management.

---

## Developer Pain Points

Recurring frustrations from this week's activity:

1. **Session limits and cost surprises** (#38335, #63930) — Users feel their paid plans are consumed unfairly fast, and prompt-cache invalidation is wasting money on expensive models. The 832-comment thread on session limits shows this is a top-tier trust issue.

2. **Windows desktop instability** — GPU process crashes (#81698), MSIX + vendor-signed DLL failures (#81341), and Turnstile-triggered crashes (#83403) are making the Windows desktop app feel fragile, especially for users with modern NVIDIA GPUs.

3. **Cross-session messaging is broken after auto-updates** — Four separate issues (#86012, #86275, #86298, #86385) describe the same regression: after desktop 1.28929.0 auto-update, cross-session messages either silently fail, get held for invisible approvals, or never trigger a responding turn. This is a critical workflow break for power users.

4. **Silent policy overrides with no opt-out** (#80988) — The `heron_brook` prompt injection overriding user delegation policy without an escape hatch is a governance concern. Developers want to control how their agents delegate.

5. **MCP permission fatigue** — `permissions.allow` entries not honored for MCP tools (#81535, #80658) forces repeated prompts on every call, disrupting automation. Also, MCP OAuth issues (#86502, fixed in v2.1.231) and 30s timeouts on fast endpoints are slowing integration work.

6. **Installation and packaging defects** — Unsealed macOS bundle (#70647) and SSH agent breakage (#29717) are blocking basic usage for segments of the user base. Packaging quality deserves more attention.

---

*Digest generated from github.com/anthropics/claude-code activity on 2026-08-14.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-14

## Today's Highlights

Three rapid-fire Rust release candidates (`0.148.0-alpha.11` through `.13`) landed within 24 hours, signaling active stabilization work on the CLI. Meanwhile, the community's attention remains laser-focused on a wave of Windows-specific issues — the extension resource-loading failure (#37458, 53 comments) is now closed, but a cluster of sandbox and subagent bugs on Windows continues to dominate the tracker. Internally, the team merged over a dozen PRs addressing sandbox manifests, MCP OAuth improvements, and context-compaction correctness.

---

## Releases

Three pre-release versions published in the last 24 hours:
- **rust-v0.148.0-alpha.11** — Release build
- **rust-v0.148.0-alpha.12** — Release build
- **rust-v0.148.0-alpha.13** — Release build

All three are Rust-native CLI builds; no detailed changelogs were published with these tags.

---

## Hot Issues

**1. [#37458 — Codex extension fails to start: "The extension couldn't load its resources"](https://github.com/openai/codex/issues/37458)** *(CLOSED, 53 comments, 👍 11)*  
The most active issue this week. Windows users on VS Code 1.132.0 hit a complete extension failure on startup. Now closed — presumably fixed or mitigated — but the high engagement suggests the fix will need verification across the many affected environments.

**2. [#26984 — MCP stdio servers leak pipe fds + orphan child processes → cumulative EMFILE](https://github.com/openai/codex/issues/26984)** *(OPEN, 21 comments, 👍 4)*  
Long-running CLI sessions eventually exhaust file descriptors (`os error 24`) because MCP stdio servers aren't being cleaned up. This is a silent reliability killer for power users running multi-hour agent sessions.

**3. [#34700 — spawn_agent rejects gpt-5.6-luna with multi_agent_v2 enabled](https://github.com/openai/codex/issues/34700)** *(OPEN, 15 comments, 👍 36)*  
The most-upvoted open issue. Windows users on Codex App 26.715.9868.0 can't use the latest model with subagents. The high reaction count signals broad demand for multi-agent support with newer GPT models.

**4. [#31553 — VS Code extension stopped auto-including IDE context after update](https://github.com/openai/codex/issues/31553)** *(CLOSED, 17 comments, 👍 12)*  
Another IDE-context regression, this time in remote/container environments. Closed, but part of a pattern (see #34920, #34696, #35333) where recent builds regressed on context attachment — a core feature for agentic coding.

**5. [#18906 — TUI: support Markdown math rendering for inline and block LaTeX](https://github.com/openai/codex/issues/18906)** *(OPEN, 15 comments, 👍 22)*  
Long-standing (since April) and still open. Researchers and academics want proper `$...$` and `$$...$$` rendering in the terminal UI. High upvote count with no movement — worth watching.

**6. [#35871 — Windows sandbox fails when resolved shell is MSIX (Store) build of pwsh](https://github.com/openai/codex/issues/35871)** *(OPEN, 13 comments, 👍 3)*  
`CreateProcessAsUserW` fails with access denied when PowerShell 7 is installed via the Microsoft Store. Windows sandboxing is clearly a rough edge.

**7. [#33551 — Multi-Agent V2 sends OpenAI-specific agent_message items to external providers](https://github.com/openai/codex/issues/33551)** *(OPEN, 8 comments, 👍 6)*  
Interop bug: external Responses-compatible providers (e.g., Ollama) can't parse `agent_message` item types. This matters for the community's growing interest in custom/self-hosted model routing.

**8. [#31198 — Desktop subagent session logs grow to 145GiB from repeated compacted replacement_history](https://github.com/openai/codex/issues/31198)** *(OPEN, 6 comments)*  
A pathological disk-space leak. Long parent threads with many subagents balloon to absurd sizes because full snapshots are persisted repeatedly. Related to the broader theme of compaction-related bloat (see #38466).

**9. [#35210 — [Windows][Desktop] `browser.tabs.finalize()` silently terminates the entire app](https://github.com/openai/codex/issues/35210)** *(OPEN, 12 comments)*  
A single API call in the desktop app's browser-use component kills the whole process instead of just closing a tab. Severity is high: data loss on an interactive feature.

**10. [#38455 — ChatGPT desktop repeatedly spawns Computer Use workers and crashes with V8 OOM on macOS](https://github.com/openai/codex/issues/38455)** *(OPEN, 3 comments, new)*  
Freshly filed: 187 worker threads named `computer-use` spawn while idle, then SIGABRT via node OOM. The previous version (26.730.61639) worked. Likely to attract attention fast.

---

## Key PR Progress

**1. [#38463 — Preserve thread subscriptions across revert reloads](https://github.com/openai/codex/pull/38463)** *(CLOSED)*  
Fixes a race where clients that requested `thread/revert` lose their active subscriptions when the replacement thread reloads. Correctness fix for the app server.

**2. [#38450 — Embed the Windows sandbox setup manifest in Bazel builds](https://github.com/openai/codex/pull/38450)** *(CLOSED)*  
Directly addresses the Windows sandbox pain: Bazel builds were dropping the `asInvoker` manifest that the sandbox helper needs. Should help with #30829 and #28457.

**3. [#38448 — Support per-server MCP OAuth callback ports](https://github.com/openai/codex/pull/38448)** *(CLOSED)*  
Adds `oauth.callback_port` to MCP server config, with support from plugin and skill declarations. Improves MCP interoperability for servers with conflicting callback requirements.

**4. [#38447 — Add running-task exit choices to local daemon sessions](https://github.com/openai/codex/pull/38447)** *(CLOSED)*  
`Ctrl-C` in a daemon session now presents a menu: cancel the task, exit and leave the task running, or stop the daemon. Quality-of-life improvement for long-running background work.

**5. [#38445 — Retain client developer messages across context compaction](https://github.com/openai/codex/pull/38445)** *(CLOSED)*  
Client-authored developer instructions were being lost when the context window compacted. Preserved when `retain_client_developer_messages` is enabled. Directly relevant to the compaction complaints in #31198 and #38466.

**6. [#38441 — Give Guardian V2 full tool action context](https://github.com/openai/codex/pull/38441)** *(CLOSED)*  
Guardian risk assessments now see the original `ToolPayload` (requested action + conversation context) instead of just a name and call ID. Meaningful improvement for safety review accuracy.

**7. [#38440 — Add app-server support for reverting paginated threads](https://github.com/openai/codex/pull/38440)** *(CLOSED)*  
Adds `thread/revert` for paginated threads: replaces durable history with the prefix before a given turn, interrupts active turns, and preserves the thread ID.

**8. [#31453 — exec-server: start managed network proxy on executor](https://github.com/openai/codex/pull/31453)** *(CLOSED)*  
Lays groundwork for managed-network policy enforcement on remote executors: sanitized policy propagation, HTTP/SOCKS proxy startup, and fail-closed behavior for MITM/credential injection until the boundary is established.

**9. [#38436 — Add rustls fallback for local MCP HTTP requests](https://github.com/openai/codex/pull/38436)** *(CLOSED)*  
When the platform TLS backend fails to negotiate a protocol version with an HTTPS MCP endpoint, retries once with rustls. Pragmatic robustness fix for local MCP integrations.

**10. [#31901 — Resolve local MCP refs in Code Mode tool schemas](https://github.com/openai/codex/pull/31901)** *(OPEN)*  
Resolves JSON Pointer `$ref` values (`#/$defs/...` and `#/definitions/...`) when Code Mode renders TypeScript tool declarations. Improves fidelity for complex MCP-exported schemas.

---

## Feature Request Trends

- **TUI polish**: Continued demand for better terminal UX — notably LaTeX/math rendering (#18906, 22 👍) and `/copy` targeting specific messages by ID (#24073).
- **Subagent lifecycle management**: Multiple requests (and bugs) around subagent thread limits (#22779), stuck "running" states after restart (#38408), and subagent session bloat (#31198). Users want finer control and better introspection.
- **MCP interoperability**: Both bug reports (#26984 fd leaks) and features (per-server OAuth ports in #38448, schema `$ref` resolution in #31901) show MCP remains a high-investment integration surface.
- **IDE context reliability**: The recurring theme of IDE context silently disabling or not attaching (#34920, #34696, #35333, #35419) suggests users strongly depend on automatic context and treat regressions as critical.

---

## Developer Pain Points

- **Windows support is the biggest source of friction.** Of the top-30 active issues, at least 12 are `windows-os` tagged. Sandbox helper resolution (#28457, #30829), MSIX pwsh failures (#35871), and IDE-context regressions in remote/container setups all point to Windows as the platform where codex breaks most often.
- **Context compaction causes user-visible damage.** Recurring complaints about bloat (145 GiB logs, #31198), truncated reads (#38466), and lost client messages (fixed in #38445) show that compaction is not yet transparent to users.
- **MCP reliability for long-running sessions remains unresolved.** The EMFILE leak (#26984, open since June) is the clearest example: a systemic fd leak that degrades sessions over time.
- **Model/API incompatibilities for power users.** Multi-agent with newer models (#34700, 36 👍) and external provider interop (#33551) indicate that bleeding-edge model features are landing faster than compatibility fixes.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-14

## Today's Highlights

The Gemini CLI ecosystem saw a substantial influx of security-focused work this week, with multiple PRs addressing supply chain vulnerabilities, OAuth resource leaks, and A2A server authentication gaps. Meanwhile, the community continues to surface recurring stability issues around subagent reliability—particularly false success reporting on turn limits and hanging generalist agents—which remain the top friction points for users. A new nightly release (v0.56.0-nightly) lands with expanded behavioral eval tooling.

## Releases

**v0.56.0-nightly.20260813.g1ac337739** — [Release Notes](https://github.com/google-gemini/gemini-cli/releases)
- Feat: eval validation improvements
- Feat(evals): tool call formatter and failure summary integration
- Changelog for v0.55.1 included

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   🔥 P1 · 12 comments · High severity bug: a `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` even when it maxed out turns before doing any work. This masks critical failures and undermines agent reliability. Community reaction underscores the need for honest termination reporting.

2. **[#21409 — Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   🔥 P1 · 8 comments · 8 👍 — Users report the generalist agent hangs for up to an hour on trivial tasks (e.g., folder creation). Workaround: instructing the model to avoid subagents. A top community pain point.

3. **[#19873 — Leverage bash affinity via zero-dependency OS sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)**  
   P2 · 8 comments — Enhancement proposing OS-level sandboxing so Gemini 3 models can use native POSIX tools safely without compromising security.

4. **[#24353 — Robust component-level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   P1 · 7 comments — Epic tracking expansion of behavioral evals beyond the current 76 tests across 6 Gemini models. Critical for systematic quality improvement.

5. **[#22745 — AST-aware file reads/search/codebase mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   P2 · 7 comments — Investigation epic for using AST-aware tools to reduce token noise, improve read precision, and enable smarter navigation.

6. **[#21968 — Gemini doesn't use skills and subagents proactively](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   P2 · 6 comments — Anecdotal but echoed widely: the model rarely activates custom skills/subagents on its own, even for clearly relevant tasks.

7. **[#25166 — Shell commands get stuck as "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   🔥 P1 · 4 comments · 3 👍 — Geminihangs while showing a finished command as "Awaiting user input." Affects simple commands and disrupts automation flows.

8. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
   P2 · 5 comments — Memory extraction agent never marks low-signal sessions as processed, causing repeated reprocessing of worthless sessions.

9. **[#26525 — Deterministic redaction and reduced Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   P2 · 4 comments — Privacy concern: transcript content is sent to model context before redaction, and logging may expose skill content.

10. **[#22672 — Agent should discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
    P2 · 3 comments · 1 👍 — Requests safer alternatives to `git reset`/`--force` and warnings for destructive DB operations.

## Key PR Progress

1. **[#28740 — Prevent supply chain RCE in eval-pr workflows](https://github.com/google-gemini/gemini-cli/pull/28740)**  
   Security fix (size/L) splitting eval workflow into a secure `pull_request` build and a trusted `workflow_run` step, mitigating untrusted fork code execution (#28336).

2. **[#28778 — Upgrade simple-git to 3.32.3 (CVE-2026-28292)](https://github.com/google-gemini/gemini-cli/pull/28778)**  
   Critical severity CVE fix identified by Trivy; bumps `simple-git` to a patched release.

3. **[#28801 — Rollback entire multi-turn request on cancellation/abort](https://github.com/google-gemini/gemini-cli/pull/28801)**  
   Fixes incomplete chat history after aborting a multi-turn prompt with tool calls, preventing corrupted session state.

4. **[#28803 — Add Claude Sonnet 4.5 and Opus 4.8 model definitions](https://github.com/google-gemini/gemini-cli/pull/28803)**  
   Adds constants, alias resolution, and policy chain fallbacks for both Claude models (size/XL, closed).

5. **[#28790 — Context-aware silent retries for capacity errors](https://github.com/google-gemini/gemini-cli/pull/28790)**  
   P1 fix that fully addresses #28761: unattended runs now auto-back-off and retry, with 2 silent retries in interactive mode.

6. **[#28789 — Fix vscode-ide-companion stop() hang & keep-alive threshold](https://github.com/google-gemini/gemini-cli/pull/28789)**  
   Resolves indefinite hang with active streaming MCP sessions plus keep-alive resource leak (#28785).

7. **[#28787 — Don't treat corrupt MCP enablement config as empty](https://github.com/google-gemini/gemini-cli/pull/28787)**  
   P1 fix preventing JSON parse failures from silently enabling all MCP servers—critical for security defaults.

8. **[#28699 — Enforce A2A server authentication & checkpoint path traversal fix](https://github.com/google-gemini/gemini-cli/pull/28699)**  
   Custom REST routes bypassed `UserBuilder` auth entirely; also fixes checkpoint path traversal. Significant security hardening.

9. **[#28804 — Behavioral evals for read_many_files, internal docs, MCP resources](https://github.com/google-gemini/gemini-cli/pull/28804)**  
   Expands eval coverage for multi-file batch reads, internal CLI documentation, and MCP resource discovery.

10. **[#28788 — Behavioral evals for skills activation & web fetch; EDK report fixes](https://github.com/google-gemini/gemini-cli/pull/28788)**  
   Adds evals for `activate_skill` and `web_fetch`, Windows compatibility, and filters skipped tests from EDK aggregator.

## Feature Request Trends

**1. AST-aware tooling** (#22745, #22746) — Growing demand for precise code structure understanding to cut token waste and improve navigation.

**2. OS-level sandboxing for native tool chains** (#19873) — Unlocking the model's bash-first training while maintaining security.

**3. Expanded behavioral evaluation coverage** (#24353) — Community and maintainers alike want systematic quality gates with more tests and model coverage.

**4. Subagent transparency & control** (#22598, #21763) — Users want subagent trajectories included in `/chat share` and bug reports for better debugging and evaluation.

**5. Proactive skill/subagent utilization** (#21968, #21432) — Models should autonomously activate relevant skills without explicit prompting.

## Developer Pain Points

**Agent reliability remains the #1 concern** — False "GOAL success" reporting (#22323) and indefinite generalist hangs (#21409) erode trust; workarounds like disabling subagents are common.

**Interactive hang bugs are recurring** — Stuck "Waiting input" states (#25166) and interactive prompt deadlocks (#22465) break real-world workflows, especially in scripts.

**Configuration defaults undermine security expectations** — Corrupt MCP configs silently enabling servers (#28787) and subagents running without permission since v0.33.0 (#22093) highlight trust boundary issues.

**Memory system needs guardrails** — Infinite retries on low-signal sessions (#26522) and pre-redaction context leaks (#26525) show the need for deterministic, privacy-respecting memory pipeline.

**Destructive command prevention lacks safeguards** — Users want the agent to prefer safe alternatives over `git reset`/`--force` and to warn before destructive DB operations (#22672).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-14

## Today's Highlights

The latest release (v1.0.80-0) introduces `--enable-mcp-server` flag to selectively re-enable MCP servers and adds multi-client visibility indicators for shared sessions. A cluster of new issues flags recurring problems around model routing (particularly `claude-haiku-4.5` with unsupported reasoning efforts), remote MCP OAuth reliability, and session state management — signaling continued focus on MCP ecosystem maturity and agent configuration flexibility. The community shows strong demand (20 👍) for per-agent reasoning effort configuration, currently only possible globally.

## Releases

**v1.0.80-0** — Most recent release added:
- `--enable-mcp-server` flag to re-enable MCP servers disabled in settings for the current run
- Shared session indicators: in `--ahp` mode, a session row you've joined leads with `2 clients` (or more) when others are attached, visible in both the Sessions tab and other UI views

## Hot Issues

**1. Custom Agent YAML Frontmatter Should Support Reasoning Effort** ([#2904](https://github.com/github/copilot-cli/issues/2904))
*Open | 👍 20 | 6 comments*
Custom agents (`.agent.md`) support model pinning but lack per-agent reasoning effort configuration — only available globally via `--effort=LEVEL`. High community demand; strongest signal this week for an agent-config feature.

**2. Reasoning effort 'medium' not supported for 'claude-haiku-4.5'** ([#4345](https://github.com/github/copilot-cli/issues/4345))
*Closed | 👍 4 | 5 comments*
When specific feature flags are active, sub-agent execution fails with "Reasoning effort 'medium' is not supported for model 'claude-haiku-4.5'". Likely feature-flag interaction bug; could be resolved in recent release.

**3. Custom agent `model` frontmatter rejects array syntax** ([#2133](https://github.com/github/copilot-cli/issues/2133))
*Open | 👍 7 | 4 comments*
Incompatibility between Copilot CLI and VS Code Copilot Chat: arrays in `model` field (supported in VS Code) cause CLI parse errors. Cross-tool inconsistency blocking workflow portability.

**4. `explore` tool hardcodes `gpt-5.4-mini`, ignoring custom configuration** ([#3954](https://github.com/github/copilot-cli/issues/3954))
*Open | 👍 3 | 3 comments*
The `explore` tool ignores custom model endpoints (e.g., DeepSeek) and attempts to use `gpt-5.4-mini` instead. Breaks custom API configurations; affects users with alternative model providers.

**5. Steered message in `preToolUse` "ask" denial is silently dropped** ([#4237](https://github.com/github/copilot-cli/issues/4237))
*Open | 1 comment*
Custom text from `preToolUse` hook denials isn't presented in the permission prompt. Undermines hook authoring flexibility; expected to be addressed in a future patch.

**6. `allowed_directories` in permissions-config doesn't suppress prompts** ([#4482](https://github.com/github/copilot-cli/issues/4482))
*Open, triage | New*
Directories in `~/.copilot/permissions-config.json` don't suppress "path outside allowed directory" prompts for shell commands, though `/add-dir` works. Configuration inconsistency causing workflow friction.

**7. Atlassian MCP OAuth fails with RFC 8414 error** ([#4480](https://github.com/github/copilot-cli/issues/4480))
*Open, triage | New*
OAuth discovery fails since 1.0.79: "authorization server advertised an issuer that does not match the URL its metadata was discovered at." Isolated possibly to Atlassian's MCP server specifics; regression from 1.0.71.

**8. Code debugging incorrectly flagged as cybersecurity risk** ([#4479](https://github.com/github/copilot-cli/issues/4479))
*Open, triage | New*
CAPI 422 errors during routine work (creating branches, reverting Build Insights changes) — misclassified as security risk. False-positive rate concerns in safety filters.

**9. MCP server collision detection is case-sensitive** ([#4478](https://github.com/github/copilot-cli/issues/4478))
*Open, triage | New*
Collisions like `MCPBrowser` vs `mcpbrowser` across config scopes treated as separate servers; both get processed. Logical names should be case-insensitive.

**10. Sessions lost when stopping an action** ([#4477](https://github.com/github/copilot-cli/issues/4477))
*Open, triage | New*
Hitting stop during agent execution deletes the entire session, including original prompt and edits. Data-loss bug impacting iterative workflows.

## Key PR Progress

_Note: Only 1 PR was updated in the last 24 hours. The following is a broader selection from the last week._

**1. docs: document proposed custom-agent effort frontmatter** ([#4476](https://github.com/github/copilot-cli/pull/4476))
*Closed*
Documents Option A (dedicated `effort` field parallel to `model`) for #2904. Adds "Custom Agents" reference section to README covering existing fields and the proposed addition.

**2. fix(agents): validate reasoning effort against model capabilities** 
*Merged (last week)*
Adds validation to reject unsupported reasoning-effort values during configuration, not at execution time.

**3. fix(mcp): case-insensitive server name collision detection**
*Open*
Normalizes MCP server names for collision detection across configuration scopes.

**4. fix(sessions): preserve session on stop**
*Open*
Prevents session deletion when user stops an in-progress action.

**5. fix(oAuth): align issuer validation with RFC 8414**
*Open*
Fixes issuer-mismatch errors for MCP servers that advertise a different issuer than the metadata URL.

**6. fix(permissions): honor allowed_directories from permissions-config.json**
*Open*
Ensures configured allowed directories suppress path-outside prompts as expected.

**7. fix(plugins): persist disabled state in /plugins TUI**
*Open*
Fixes UI so disabled skills show distinct state and persist across refreshes.

**8. docs(agents): document model array support**
*Open*
Adds documentation confirming array syntax for the `model` frontmatter field, matching VS Code Copilot Chat compatibility.

**9. fix(sessions): list running sessions with status**
*Open*
Adds `copilot sessions --json` command to list running sessions with id, name, cwd, and status.

**10. fix(remote-mcp): retry transient 5xx with backoff**
*Open*
Implements retry/backoff for transient 5xx errors on MCP `initialize` instead of marking the server failed for the whole session.

## Feature Request Trends

- **Per-agent reasoning effort configuration** ([#2904](https://github.com/github/copilot-cli/issues/2904), [#4476](https://github.com/github/copilot-cli/pull/4476)) — top-requested feature; users want model + effort control per `.agent.md` agent.
- **More granular MCP server control** — `--enable-mcp-server` flag (shipped in 1.0.80-0); case-insensitive collision detection, retry/backoff.
- **Better session lifecycle management** — listing running sessions ([#4470](https://github.com/github/copilot-cli/issues/4470)), preventing session loss on stop, restoring archived sessions.
- **Plugin/skill state persistence and clarity** ([#4471](https://github.com/github/copilot-cli/issues/4471)) — TUI should distinguish disabled vs enabled skills and persist changes.
- **Agent model field parity with VS Code Copilot Chat** ([#2133](https://github.com/github/copilot-cli/issues/2133)) — support for array syntax in `model` frontmatter.

## Developer Pain Points

- **Model routing bugs** — hardcoded sub-agent models ([#3954](https://github.com/github/copilot-cli/issues/3954), [#4462](https://github.com/github/copilot-cli/issues/4462)) and unsupported reasoning-effort values ([#4345](https://github.com/github/copilot-cli/issues/4345), [#4473](https://github.com/github/copilot-cli/issues/4473)) are recurring sources of friction, especially around "explore" and "code-review" sub-agents.
- **OAuth/remote MCP unreliability** — token refresh scope bugs (AADSTS70011), RFC 8414 issuer failures, Windows socket errors, concurrent refresh race conditions — impact users of remote MCP servers (Atlassian, Microsoft Entra).
- **Session state fragility** — lost sessions on stop, orphaned permission events replaying on resume, long-running sessions exhausting event storage. Multiple reports of sessions disappearing or appearing cancelled while processes remain active.
- **Permission-prompt configuration gaps** — `allowed_directories` not honored as expected, and hook-driven "ask" denials losing custom messages; permission-first users hit repeated interactive interruptions.
- **Cross-tool compatibility** — differences between CLI and VS Code Copilot Chat custom-agent behavior (model arrays, effort settings) complicate migrations.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-08-14**

---

### 1. Today's Highlights

No new releases or pull requests landed in the last 24 hours, but the community is actively flagging two serious stability defects: a silent hang in ACP streaming mode (#2598) and a runaway generation event that produced 88k tokens of garbage in a single step (#2597). The long-standing Memory System feature request (#1283) continues to accumulate traction and remains the most-voted enhancement direction, signaling strong demand for persistent context in the CLI.

---

### 2. Releases

No new releases were published in the last 24 hours.

---

### 3. Hot Issues

**#1283 — Feature Request: Memory System – Persistent context across sessions**  
[GitHub](https://github.com/MoonshotAI/kimi-cli/issues/1283)  
The highest-activity issue in the repo (38 comments). Community is asking for both automatic (AI-managed) and manual (user-defined) memory to carry context across sessions. This is the clearest signal of where the product roadmap should head next — persistent context is becoming table stakes for AI developer tools.

**#2598 — ACP/print streaming hang: no idle timeout, replaced wheel partial not written to wire (0.31.1 only covers Esc)**  
[GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2598)  
A critical reliability bug in ACP mode (`kimi acp`). The stream finishes delivering deltas but the terminal `[DONE]` frame never arrives, leaving the CLI hanging indefinitely. There is no idle timeout configuration available. A subsequent message silently replaces the stuck wheel, and the partial response never lands in `wire.jsonl`. This breaks automation pipelines that depend on ACP protocol guarantees.

**#2597 — Runaway garbled generation: 88k tokens of gibberish in one LLM step**  
[GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2597)  
A single LLM step ran for ~53 minutes and emitted 88,114 tokens of incoherent repetitive content (multilingual fragments, broken Markdown). This points to a missing generation-termination safeguard — likely a missing stop condition or a degenerate sampling state. For a CLI integrated into day-to-day workflows, this can waste significant token budget and stall interactive sessions.

---

### 4. Key PR Progress

No pull request activity in the last 24 hours.

---

### 5. Feature Request Trends

- **Persistent Memory & Context** (#1283): The dominant ask — users want the CLI to remember project patterns, preferences, and prior decisions across sessions. This is the single most-commented issue and represents a clear roadmap priority.
- **Streaming Reliability & Timeout Controls** (#2598): Implicit demand for configurable idle/wait timeouts on streaming responses, plus guarantees that partial responses are recorded durably even if interrupted.
- **Generation Guardrails** (#2597): Growing need for hard limits on output length and detection of runaway/degenerate generation loops to protect token budgets.

---

### 6. Developer Pain Points

- **Silent Hangs with No Escape Hatch**: ACP mode can hang indefinitely with no timeout and no way to recover the partial response. The 0.31.1 fix only covered the Esc-key path, leaving the replacement-wheel scenario broken.
- **Unbounded Generation Bursts**: A single step consuming 88k tokens of garbage over 53 minutes is a severe operational risk — users cannot predict or cap model output, and there is no built-in abort-and-resume mechanism.
- **No Durable Partial Logging**: When a streaming wheel is replaced, the partial content is lost entirely (not written to `wire.jsonl`). Developers lose traceability and cannot replay or audit interrupted exchanges.

---

*Digest generated from GitHub activity for MoonshotAI/kimi-cli as of 2026-08-14.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-14

## Today's Highlights

The project shipped v1.18.18 with targeted provider fixes, but the broader community conversation is centered on stability and security. A notable cluster of duplicate issues reports the CLI "deleting itself," alongside new security reports flagging a `curl|bash` upgrade pattern and SSRF risks in the `webfetch` tool. The V2 runtime continues to generate friction, with reports of missing TODO tools, database incompatibility with V1, and Windows console flashing.

## Releases

**v1.18.18** ([Release](https://github.com/anomalyco/opencode/releases/tag/v1.18.18))
- Fixes Kimi system prompt selection for official Moonshot and Kimi providers
- Corrects `xhigh` reasoning effort for xAI models

## Hot Issues

1. **[#37012 — Keep legacy layout option](https://github.com/anomalyco/opencode/issues/37012)** (37 comments, 41 👍) — The most-discussed issue this cycle. Users argue the old layout provides faster access to features without navigation overhead, and request workspace support in the new UI. Community sentiment suggests the redesign, while welcome, should not remove a familiar power-user workflow.

2. **[#42434 — `opencode upgrade` fetches remote script with no integrity verification](https://github.com/anomalyco/opencode/issues/42434)** (3 comments) — New security report on the `curl|bash` install/upgrade pattern. Medium severity supply-chain/TOCTOU risk. This is the second of four security reports filed by the same researcher this week (see also #42437, #42435), suggesting a focused security audit is underway.

3. **[#42441 / #42411 — "opencode deletes itself"](https://github.com/anomalyco/opencode/issues/42441)** (2 comments each) — Two duplicate reports (filed ~a day apart) that the installed binary literally disappears after `pnpm i -g opencode-ai`. If reproducible, this is a serious packaging bug affecting the pnpm install path. No maintainer response yet.

4. **[#41470 — "Copied to clipboard" doesn't work in VSCode Server](https://github.com/anomalyco/opencode/issues/41470)** (15 comments) — Clipboard operations fail silently inside Docker/VSCode Server environments. Persistent issue across versions (reported on 1.18.14), likely a clipboard backend detection problem in remote/headless environments.

5. **[#42083 — GitHub Copilot provider shows zero models](https://github.com/anomalyco/opencode/issues/42083)** (5 comments) — Auth succeeds but no models appear in the picker. All models report `model_picker_enabled: false`. Breaks a major provider integration for Arch Linux users on 1.18.15.

6. **[#40516 — Desktop app fails to load providers/models/MCP on startup](https://github.com/anomalyco/opencode/issues/40516)** (4 comments) — 80% of startups fail for multiple users in an enterprise org. Explicitly a version regression: v1.18.4 works, v1.18.5–v1.18.13 broken. This had enough signal to warrant a regression test, but it remains open.

7. **[#42435 — `webfetch` SSRF to local services](https://github.com/anomalyco/opencode/issues/42435)** (2 comments) — Security report that `webfetch` can reach loopback/private addresses; a guard PR was closed unmerged. Notable because it compounds with models that guess URLs. Plausible local SSRF vector for server-mode deployments.

8. **[#42074 — DeepSeek v4 Flash Free 429s on every request](https://github.com/anomalyco/opencode/issues/42074)** (2 comments) — `deepseek-v4-flash-free` via `opencode.ai/zen` returns `FreeUsageLimitError` on every request from 3 distinct IPs — including via plain `curl`, not just the official client. Suggests a server-side misconfiguration rather than client misuse.

9. **[#42437 — Context pruning silently drops instruction-bearing content](https://github.com/anomalyco/opencode/issues/42437)** (2 comments) — Security/integrity report that compaction may silently discard constraint-bearing content, not just reduce cost. Described as "Medium-High" severity; tied to `session/compact` behaviors.

10. **[#42448 — V2 Compaction exceeds context window on high-output models](https://github.com/anomalyco/opencode/issues/42448)** (2 comments) — At 79% context usage auto-compaction didn't run, and `/compact` failed because the provider blocked the oversized prompt+output. Model advertises 299,964-token window; compaction request itself exceeded it.

## Key PR Progress

1. **[#42444 — Preserve v1 database compatibility](https://github.com/anomalyco/opencode/pull/42444)** — Stops V1 `move`/`revert` projections from resetting the removed session context epoch table; keeps experimental workspace paths from querying V2 schema. Directly addresses the V1/V2 coexistence breakage reported in #42260.

2. **[#42446 — Defer update check until service resolves](https://github.com/anomalyco/opencode/pull/42446)** — Prevents an old running client from repeatedly rejecting newly installed server versions as mismatches. Extracted from closed PR #42025 into a focused fix.

3. **[#42433 — Preserve response model metadata](https://github.com/anomalyco/opencode/pull/42433)** — Keeps the AI SDK's structured `modelId` from response rather than discarding it. Closes #42420; intentionally narrower than #26091 (does not attempt arbitrary header passthrough).

4. **[#42419 — Preserve toast hover state](https://github.com/anomalyco/opencode/pull/42419)** — Fixes two edges in the actionable toast behavior: queued toasts stay paused under a stationary pointer, and selecting text no longer activates/dismisses the card.

5. **[#42453 — Correct tab context menu behavior](https://github.com/anomalyco/opencode/pull/42453)** — Pointer-only dismiss semantics: clicks outside dismiss without activating underlying UI; right-click on open menu dismisses without selecting; Rename opens reliably.

6. **[#42455 — Recover sessions from missing locations](https://github.com/anomalyco/opencode/pull/42455)** — Recover sessions whose working directory was deleted without requiring the broken location runner. Also keeps new sessions out of unavailable inherited locations.

7. **[#42456 — Isolate tab scroll state](https://github.com/anomalyco/opencode/pull/42456)** — Each session tab keeps its own transcript reading position under the `tab_scroll` experiment. Fixes a race where tab A's cleanup saved its position under tab B.

8. **[#38790 — Add workspace flows to new layout](https://github.com/anomalyco/opencode/pull/38790)** — Adds workspace selection for new sessions (local repo, isolated new workspace, existing workspaces) with a context-aware composer pill showing branch context. This is likely the response to #37012's demand for workspace support in the new layout.

9. **[#42450 — Use file times for tool output cleanup](https://github.com/anomalyco/opencode/pull/42450)** — Managed tool-output retention now uses filesystem mtimes instead of encoded identifier timestamps; preserves files when metadata can't be read. Covers cleanup across timestamp wrap boundaries.

10. **[#42425 — Add `agent_memory` table and memory-tools plugin](https://github.com/anomalyco/opencode/pull/42425)** — Cloud backup/restore of OpenCode AgentMemory via Supabase. New feature; closes #41998. Represents a persistent-memory direction for the agent runtime.

## Feature Request Trends

- **UI/UX preservation over redesign** — The top-voted issue (#37012, 41 👍) is a direct appeal to keep the legacy layout. The community values density and direct access over navigation-heavy designs. PR #38790 (workspace flows) appears to be the maintainers' answer.
- **Local/LAN model discovery** — Two open PRs (#19959, #27554) add auto-discovery of local OpenAI-compatible servers via mDNS/LAN and `/v1/models` probing. There is sustained community interest in first-class local-model support.
- **Hebrew locale** — New request (#42447) for full `he` translation. Localization requests continue to arrive steadily (Indonesian README PR #38033 also active).
- **Background activity visibility** — Feature request (#42369) for a right sidebar showing running subagents with live status and model info.
- **Persistent memory** — PR #42425 adds an `agent_memory` table with cloud sync, suggesting a broader direction toward long-term agent state.

## Developer Pain Points

- **Free-tier rate limits are broken or confusing** — At least three issues this cycle (#42029, #42074, #42452, #42449) involve `FreeUsageLimitError` 429s: hitting limits on unused accounts, limits applying instantly on new versions, and new sessions going into cooldown immediately after reset. Some reports appear server-side (curl against the Zen API fails from any IP), which erodes trust in the free tier.
- **Security audit has uncovered real issues** — The researcher (shafqatevo) has filed four reports in one day covering supply-chain (`curl|bash`), SSRF (`webfetch`), and context-pruning integrity. The sheer volume suggests an external audit is ongoing; the "guard PR closed unmerged" detail will likely need follow-up.
- **V2 transition is destabilizing for V1 users** — Reports of the V2 runtime mutating the shared V1 database (#42260), missing TODO tools (#42421), and Windows console flashing on every subprocess spawn (#42440). The coexistence story is not yet clean.
- **Desktop app regression persists** — #40516 has been open for 10 days affecting an entire organization (80% startup failure). It remains the highest-severity reliability issue in the tracker with no fix shipped.
- **CLI binary vanishing** — Two duplicate reports that `pnpm i -g opencode-ai` results in the binary disappearing after a day of use. If confirmed, this is a jarring packaging bug for Node-based installs.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-14

## Today's Highlights
The community continues to rally around terminal hygiene and performance issues, with significant progress on the long-standing `/resume` flashback problem and prompt-editor lag. A cluster of closed issues signals maintainers are actively triaging and closing out older feature requests, while several new PRs target TUI rendering optimizations and cross-platform compatibility fixes.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues
1. **[#6879 — Auto-compaction never triggers after context grows past 100%](https://github.com/earendil-works/pi/issues/6879)**  
   High engagement (19 comments, 17 👍) — the top issue this week. A 2-hour agentic turn on gpt-5.6-sol pushed past the compaction threshold until the API rejected at 373k tokens. Suggests verifying compaction after every agentic turn.

2. **[#7836 — Edit fuzzy match fails on whitespace-length differences](https://github.com/earendil-works/pi/issues/7836)**  
   `normalizeForFuzzyMatch` doesn't collapse whitespace runs, so `Edit`'s `oldText` fails on otherwise identical content. Impacts small models with whitespace noise.

3. **[#8029 — Very slow prompt editor movement with large buffers](https://github.com/earendil-works/pi/issues/8029)**  
   A single arrow press on a ~7000-line buffer took **1650ms**. The community jumped on this with a caching PR (#8066) within 24 hours.

4. **[#7791 — Global Undici dispatcher inherits 16 KiB maxHeaderSize](https://github.com/earendil-works/pi/issues/7791)**  
   `UND_ERR_HEADERS_OVERFLOW` for valid responses with large headers. CLOSED — root cause identified in `EnvHttpProxyAgent` default configuration.

5. **[#7779 — Trusted Unix users can't share PI_CODING_AGENT_DIR](https://github.com/earendil-works/pi/issues/7779)**  
   `0600` file permissions on `auth.json` / `models-store.json` lock out subsequent users. Multi-user Unix deployments affected.

6. **[#7829 — Invalid settings.json silently ignored → misleading bash error on Windows](https://github.com/earendil-works/pi/issues/7829)**  
   A typo of unsanitized backslashes clearly surfaces visible, but only confusing errors. Highlights validation gaps for user config.

7. **[#7689 — Handle `end_turn: false` for Codex backend](https://github.com/earendil-works/pi/issues/7689)**  
   Authored by mitsuhiko — the Codex backend can emit `end_turn: false` on `response.completed`, and current handling doesn't account for this.

8. **[#7761 — TUI copy shows "Copied!" but clipboard stays empty on GNOME Terminal](https://github.com/earendil-works/pi/issues/7761)**  
   `copySelectionToClipboard()` writes only an **OSC52** sequence, which VTE terminals ignore. User-visible UX bug.

9. **[#8055 — Ambiguous-width chars break table alignment on CJK terminals](https://github.com/earendil-works/pi/issues/8055)**  
   Characters like `① ± … €` are counted as 1 column but render 2 wide in CJK terminals. Break tables/lists in TUI markdown.

10. **[#8017 — Support Anthropic refusal server-side fallback](https://github.com/earendil-works/pi/issues/8017)**  
    Badlogic's own issue: compaction can fail if Anthropic's classifier deems pi's activity illegal; suggests server-side fallback support.

---

## Key PR Progress
1. **[#8082 — Render only visible viewport; restore terminal on SIGINT](https://github.com/earendil-works/pi/pulls/8082)**  
   Fixes the `/resume` flood (759 KB session → 844 KB streamed) and SIGINT leaving raw mode. Closed with real pty-harness verification.

2. **[#8086 — Fall back to legacy Gemini tool schema on unknown-field rejection](https://github.com/earendil-works/pi/pulls/8086)**  
   Fixes `400 INVALID_ARGUMENT` for endpoints that reject `parametersJsonSchema`. Important for Gemini provider reliability.

3. **[#8066 — Visual lines caching for prompt editor](https://github.com/earendil-works/pi/pulls/8066)**  
   Direct fix for #8029. Caches visual-line results; cache invalidated on width/text change. Likely eliminates the multi-second arrow-press lag.

4. **[#8084 — Don't swallow prompt after boolean extension flags](https://github.com/earendil-works/pi/pulls/8084)**  
   Fixes a wickedly silent bug: `pi -p --plan "prompt"` consumed the prompt as the flag's value and exited 0 with no messages.

5. **[#8070 — Validate extension flag defaults](https://github.com/earendil-works/pi/pulls/8070)**  
   Models `registerFlag()` as a discriminated union; rejects mismatched type/default pairs (e.g., boolean with `"false"`).

6. **[#8076 — DRAFT: dev branch with new harness](https://github.com/earendil-works/pi/pulls/8076)**  
   By davidbrai. Draft PR hinting at a new harness direction — watch this space.

7. **[#8067 — Use APP_NAME in user-facing messages](https://github.com/earendil-works/pi/pulls/8067)**  
   Replaces hardcoded strings with `APP_NAME` config — harmless for pi, needed for rebranded builds.

8. **[#8085 — Cancel active mouse selection with escape](https://github.com/earendil-works/pi/pulls/8085)**  
   Pressing `Escape` mid-drag clears selection without copying. Small but ergonomic standard behavior.

9. **[#8057 — Todo renderResult returns undefined on validation errors](https://github.com/earendil-works/pi/pulls/8057)**  
   Fixes a TUI crash when `details` is `{}` (truthy) but missing `error` and an unmatched `action`.

10. **[#7993 — Compact between tool turns (CLOSED — agent gone wild)](https://github.com/earendil-works/pi/pulls/7993)**  
    Author apologized: "This was an agent gone wild. Please ignore this." A fun lesson in agent-driven PR hygiene.

---

## Feature Request Trends
- **Compaction & context management** — automation, thresholds, preemptive checks; #6879, #8017.
- **TUI terminal hygiene** — clipboard, SIGINT restore, viewport rendering; #7761, #8080, #8082.
- **HTML export fidelity** — mermaid/LaTeX parity with TUI (#8041).
- **Performance budgets** — startup-time/memory targets comparable to jcode (#7739).
- **Host-tool flexibility** — per-tool opt-out of strict schema validation (#7607).
- **Model catalog freshness** — Grok 4.6 routing, Kimi cached_tokens (#8046, #8075).
- **Session lifecycle** — resume UX, scrollback pollution, /resume counts diverge (#8079, #7960).

---

## Developer Pain Points
- **Context-window overflow & compaction** — auto-compaction races the provider limit, causing LLM failures mid-session.
- **Terminal untidiness** — raw mode after SIGINT, OSC52 clipboard failures, history replay floods — recurring hygiene gripes.
- **Configuration footguns** — invalid JSON silently ignored, `0600` permissions exclude teammates, misleading error messages.
- **Performance on large buffers** — prompt editor and resume are O(n²)-feeling; both got targeted PRs this week.
- **Agent-generated churn** — a "gone wild" PR (#7993) and silent flag-swallowing (#8084) highlight trust and validation issues in agent-driven development loops.
- **Windows/multi-user gaps** — Unix socket test failures, shared state permissions, and Bash path assumptions keep surfacing.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-14

## Today's Highlights

This week's digest centers on the **native multi-agent fleet architecture** — the `/coordinate` command, supervised teammate runtimes, and fleet persistence are now landing across CLI, core, and web-shell. The **SWE-bench Verified benchmark is quarantined** due to non-production E2E validation issues, signaling a hard stop on release certification until results are clean. Additionally, a wave of **Windows-specific regressions** (paste in CLI, Desktop terminal spawning) and **headless/Vertex AI auth failures** are drawing active community attention and rapid fix PRs.

## Releases

**v0.21.12-preview.1** — Includes two web-shell fixes:
- Preserve standalone session target ([#9038](https://github.com/QwenLM/qwen-code/pull/9038))
- Support workspace file uploads

**v0.21.11** — Highlights:
- Added support for Agent Plugins v1 to extend agent capabilities ([#8834](https://github.com/QwenLM/qwen-code/pull/8834))
- Enabled native multi-agent workflows with read-only teammates via the `/coordinate` command ([#8804](https://github.com/QwenLM/qwen-code/pull/8804))

## Hot Issues

1. **[#8718 — RFC: Native coordination for independent Qwen sessions](https://github.com/QwenLM/qwen-code/issues/8718)** *(9 comments, P2, feature-request)* — The umbrella RFC behind the entire multi-agent fleet effort. Proposes leader dispatch of self-contained workers with correlated runtime/task state. Community engagement is high as this shapes the roadmap for agent orchestration.

2. **[#8678 — fix(serve): Preserve current session when large restore times out](https://github.com/QwenLM/qwen-code/issues/8678)** *(8 comments, P1, bug)* — Drives PR #8691 (merged) implementing timeout contracts and late-request safety. Directly impacts daemon reliability for long-running sessions.

3. **[#7118 — Windows standalone installer fails when powershell.exe cannot resolve Get-FileHash](https://github.com/QwenLM/qwen-code/issues/7118)** *(7 comments, P2, bug, 3 👍)* — Long-standing Windows install friction with community upvotes. Still open with `welcome-pr` label — good candidate for contributor onboarding.

4. **[#9019 — Gemini 2.5 unusable on Vertex AI: thinkingLevel always sent including UNSPECIFIED](https://github.com/QwenLM/qwen-code/issues/9019)** *(5 comments, P2, bug)* — Every Vertex AI request to Gemini 2.5 fails with a 400 on `thinking_level`. Blocks all Gemini 2.5 users on Google Cloud; urgent integration fix needed.

5. **[#9025 — Keyless Vertex AI not inferred from environment; headless ADC exits with no auth type](https://github.com/QwenLM/qwen-code/issues/9025)** *(5 comments, P2, bug)* — Companion to #9019. `getAuthTypeFromEnv` fails to infer keyless ADC, killing headless runs at startup. Two related Vertex AI issues in one digest signals a systemic gap in Google Cloud auth handling.

6. **[#9061 — Ctrl+V paste completely unresponsive in CLI on Windows; regression since 0.21.x](https://github.com/QwenLM/qwen-code/issues/9061)** *(3 comments, P1, bug)* — Clipboard paste regression between 0.21.0 and 0.21.11. Downgrading restores behavior. High-impact for Windows CLI daily users.

7. **[#9088 — read_file sends non-image to model API based only on .png extension — raw 400 aborts turn](https://github.com/QwenLM/qwen-code/issues/9088)** *(3 comments, P2, bug)* — `screenshot.png` containing JSON bytes gets sent to the model as an image based purely on extension. Demonstrates a lack of content-type sniffing in file tooling.

8. **[#9108 — Desktop: remaining external links fail to open; MCP OAuth cannot complete](https://github.com/QwenLM/qwen-code/issues/9108)** *(3 comments, P2, bug, UI/MCP)* — Follow-up to #9069. Four link surfaces still use the unreliable implicit new-window path in the webview, blocking MCP OAuth flows. Desktop users face silent dead links.

9. **[#9026 — NO_TOOL_RESULT_PROGRESS hard-fails headless runs when model ends quietly after tool result](https://github.com/QwenLM/qwen-code/issues/9026)** *(3 comments, P2, bug)* — Headless runs abort with `InvalidStreamError` when a model ends a turn without visible progress after a tool result. Breaks non-interactive pipelines.

10. **[#9083 — record_artifact succeeds without verifying workspacePath; store/mount path mismatch](https://github.com/QwenLM/qwen-code/issues/9083)** *(3 comments, P2, bug)* — Artifact reported as `missing` despite being on disk, due to mismatched cwd vs workspace root semantics. Models mislead users about downloadable artifacts.

## Key PR Progress

1. **[#9034 — feat(core): expose workflow execution state](https://github.com/QwenLM/qwen-code/pull/9034)** — Adds structured, observable runtime model for Workflow execution: run/step lifecycle events, journal persistence, snapshot reconstruction, cancellation and retention primitives. Foundation for workflow observability.

2. **[#8971 — feat(core): write per-agent transcripts for workflow dispatches](https://github.com/QwenLM/qwen-code/pull/8971)** — Every workflow `agent()` dispatch now writes the same per-agent JSONL transcript as sub-agent tool launches, seeded with the dispatch prompt. Removes a debugging blind spot.

3. **[#9098 — feat(cli): enable dynamic workflows from a settings key](https://github.com/QwenLM/qwen-code/pull/9098)** — `tools.workflowsEnabled` setting exposes dynamic workflows without undocumented environment variables.

4. **[#9091 + #9092 + #9093 — Review resume series](https://github.com/QwenLM/qwen-code/pull/9091)** — Ledger-based run-session tracking, on-disk state resume for `fetch-pr --resume`, and wiring through `/review` and CI retry. Turns interrupted reviews into resumable state machines.

5. **[#9086 — fix(review): harden the pipeline against four live-run failures](https://github.com/QwenLM/qwen-code/pull/9086)** — Four defects caught by running against real PRs with qwen3.8-max, each pinned with regression tests. Evidence-driven quality improvement.

6. **[#8996 — feat(autofix): judge review-feedback validity by content, not author](https://github.com/QwenLM/qwen-code/pull/8996)** — Mechanically checks whether feedback claims are true, replacing prose-gated validity. Injection defense beyond author trust.

7. **[#9095 — feat(review): close unbounded finding classes prospectively](https://github.com/QwenLM/qwen-code/pull/9095)** — Adds an enumeration-trap check to Agent 3b so review catches the class of defect, not just the current entrance.

8. **[#9100 — feat(review): validate and scope incremental anchor inside fetch-pr](https://github.com/QwenLM/qwen-code/pull/9100)** — `--since <sha>` anchor validation moves incremental-review scoping into the CLI.

9. **[#9106 — feat: consolidate Local Control into one daemon-owned implementation](https://github.com/QwenLM/qwen-code/pull/9106)** — Two separate phone-pairing implementations (two languages, two security models) merge into one daemon-owned mechanism. Security posture consolidation.

10. **[#9104 — feat(autofix): escalate non-converging diff to maintainer handoff](https://github.com/QwenLM/qwen-code/pull/9104)** — Non-convergence detection feeds growth trajectory to the agent; escalating instead of patching indefinitely.

## Feature Request Trends

- **Multi-agent fleet orchestration** is the dominant theme: RFC #8718, `/coordinate` command, supervised teammate runtimes, fleet persistence/stages 1A–3, and terminal attach all target "leader + workers" workflows with read-only teammates.
- **Workspace/artifact path consistency** across tools (`record_artifact`, `read_file`, MCP, web-shell) — recurring correctness gaps when session cwd, workspace root, and artifact store disagree.
- **Daemon health and recovery** beyond surface metrics: `activeWork` facts, deep health reporting, background agent recovery, and restore timeout contracts.
- **Web-shell parity with desktop/CLI**: workspace uploads, external-link routing via Tauri opener, channel policy redesign.

## Developer Pain Points

1. **Google Cloud/Vertex AI friction** — Two distinct auth bugs (#9019, #9025) block Gemini 2.5 users entirely; keyless ADC inference is missing.
2. **Windows-specific regressions** — Ctrl+V paste death (#9061), visible Terminal spawning in Desktop (#9043), and lingering installer SHA-256 issues (#7118) show Windows is a second-class platform for release QA.
3. **Headless reliability gaps** — `NO_TOOL_RESULT_PROGRESS` aborts (#9026) and upstream placeholder response handling (PR #8938) break CI-style runs.
4. **Artifact verification debt** — Files validated by extension not content (#9088), artifact stores reporting missing files that exist (#9083): model outputs mislead users about file operations.
5. **Desktop webview silent failure modes** — External links drop silently (no error, no fallback), with at least two rounds of fixes (#9069 → #9108/#9111) across multiple link surfaces.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-14

## Today's Highlights

The project continues its transition from `deepseek-tui` to **CodeWhale** (v0.9.7+), with the legacy npm package officially deprecated. This week's activity centers on **v0.9.8 development**, featuring a two-layer Auto-Review model-guardian tier, first-class local DS4 (DwarfStar) provider setup, and an umbrella EPIC for TUI crate decomposition. A notable cluster of issues addresses **shell sandbox restrictions** (SSH/outbound blocking), **Chinese IME input problems**, and **long-context agent hangs**, while PRs land Markdown quote-rail rendering, MCP pagination fixes, and test isolation for machine-state-dependent tests.

---

## Releases

### v0.9.7
- **Codewhale** is now the official public product name (from Shannon Labs). The `codewhale` command, npm package, and release-asset names are lowercase technical identifiers.
- The legacy `deepseek-tui` npm package is **deprecated** and will receive no further releases.
- Users upgrading from v0.8.x legacy `deepseek` / `d*` commands should migrate to the `codewhale` binary.

> Note: No v0.9.8 release yet — but PRs targeting it are actively merging (see below).

---

## Hot Issues (Top 10)

1. **[#5324 — agent tool: simplify the 32-field schema](https://github.com/Hmbown/CodeWhale/issues/5324)**  
   The model-facing `agent` tool has a 32-property JSON schema with zero required fields, serving 8 actions plus alias baggage. Models are erroring on it — a direct blocker for agent reliability. Community and maintainers agree on simplification. *(7 comments)*

2. **[#998 — 文案展示不全 (truncated text display)](https://github.com/Hmbown/CodeWhale/issues/998)**  
   Chinese UI text is cut off; user requests hover tooltips for full content. Long-running i18n/rendering concern. *(11 comments, 👍1)*

3. **[#1004 — /dryrun command proposal](https://github.com/Hmbown/CodeWhale/issues/1004)**  
   Preview the next chat completion request (system prompt, tool defs, @mentions, cached files) **without sending** it — critical for V4 Pro users iterating on long, expensive turns. *(9 comments)*

4. **[#2369 — Config paths fragmented across OS/Cygwin](https://github.com/Hmbown/CodeWhale/issues/2369)**  
   Windows/Cygwin resolve config and secret paths differently, and a legacy migration can silently corrupt state. Reliability + migration risk. *(7 comments)*

5. **[#1425 — Session hangs after large-text agent spawn](https://github.com/Hmbown/CodeWhale/issues/1425)**  
   Analyzing a 3M+ character novel spawns 10 sub-agents, then `agent_wait` times out and the session deadlocks. Sub-agents show `Running` but never complete. *(6 comments)*

6. **[#1482 — NVIDIA NIM not working](https://github.com/Hmbown/CodeWhale/issues/1482)**  
   API calls return `404 page not found`. Environment dump shows v0.8.29 — version skew may be a factor. *(6 comments)*

7. **[#894 — Image rendering confusion during execution](https://github.com/Hmbown/CodeWhale/issues/894)**  
   Images displayed out of order / mixed during long TUI runs. *(6 comments)*

8. **[#1651 — VS Code crashes when YOLO Agent runs tests](https://github.com/Hmbown/CodeWhale/issues/1651)**  
   VS Code exits unexpectedly while the YOLO agent executes test scripts in the integrated terminal (v4-pro/v4-flash). *(5 comments)*

9. **[#1829 — SSH exit code 255 (outbound TCP 22 blocked)](https://github.com/Hmbown/CodeWhale/issues/1829)**  
   The TUI shell sandbox appears to block outbound SSH on Windows. `ssh` and `scp` fail silently with exit 255. *(5 comments)*

10. **[#1732 — Merging analysis reports is extremely slow](https://github.com/Hmbown/CodeWhale/issues/1732)**  
    Cache-hit ratio drops sharply when merging large reports to local files; process crawls. *(6 comments)*

---

## Key PR Progress

1. **[#5369 — fix(tools): degrade Moonshot schemas instead of refusing conditionals](https://github.com/Hmbown/CodeWhale/pull/5369)**  
   Prerequisite slice for #5324: schema degradation for Moonshot to avoid hard refusals. *(open)*

2. **[#5364 — feat(tui): render markdown blockquotes with a quote rail](https://github.com/Hmbown/CodeWhale/pull/5364)** *(closed)*  
   Proper quote-rail rendering for `>` lines — supports nesting, inline formatting, wrapping, and selection-copy.

3. **[#5358 — feat(engine): auto-review denial rationale + turn circuit breaker](https://github.com/Hmbown/CodeWhale/pull/5358)** *(closed)*  
   First P0 slice of #5352: sends a rationale with `permission_denied` blocks and a circuit breaker to stop the model re-phrasing the same denied action until budget exhaustion.

4. **[#5353 — feat(tui): model guardian tier for Auto-Review (v0.9.8)](https://github.com/Hmbown/CodeWhale/pull/5353)** *(open)*  
   Two-layer Auto-Review: deterministic floor (non-bypassable) + one-shot model guardian fallback. Adopts Codex `auto_review` semantics + Kimi vocabulary + fail-closed defaults.

5. **[#5365 — feat(provider): add first-class local DS4 setup](https://github.com/Hmbown/CodeWhale/pull/5365)** *(open)*  
   `/setup provider ds4` and provider-picker `D` shortcut → prefilled keyless loopback preset reusing the OpenAI-compatible transport.

6. **[#5368 — fix(tui): confine unguarded tests to the isolated state root](https://github.com/Hmbown/CodeWhale/pull/5368)** *(open)*  
   Fixes the 4 machine-state-dependent tests from #5359 (lock-holder trust hole, settings path routing, display-probe flakiness).

7. **[#5339 — fix(engine): suppress child-owned shell completions](https://github.com/Hmbown/CodeWhale/pull/5339)** *(open)*  
   Filters child-owned background shell completion events out of the parent model stream. Closes #5325. *(open)*

8. **[#5336 — fix(mcp): omit nextCursor when there are no further pages](https://github.com/Hmbown/CodeWhale/pull/5336)** *(closed)*  
   Fixes invalid `"nextCursor": null` in `tools/list` and `resources/list` responses — strict MCP clients (Claude Code) were rejecting the shape.

9. **[#5333 — feat(tui): pin host terminal window as an always-on-top mini window](https://github.com/Hmbown/CodeWhale/pull/5333)** *(closed)*  
   Harvest of community PR #5318 (SparkofSpike): `shrink-and-pin-on-top` (PiP) via context menu or `/pin` command; restores on toggle.

10. **[#5338 — feat(web): move the docs guide page onto the dictionary spine](https://github.com/Hmbown/CodeWhale/pull/5338)** *(closed)*  
    Retires `isZh` ternaries in the docs guide page by introducing a per-page dictionary pattern (en/zh, verbatim copy).

---

## Feature Request Trends

1. **Provider flexibility & local-first routing** — DS4 (DwarfStar) first-class support (#5363, #5365), NVIDIA NIM fixes (#1482), FreeBSD binaries (#1097), and automatic profile switching on rate limits (#855).

2. **Input & editor ergonomics** — Multi-line input mode / configurable send shortcuts (#5345), Chinese IME compatibility (#2323), and AI selecting the correct shell/language per environment (#1754).

3. **Transparency & dry-run tooling** — `/dryrun` to preview the next completion request (#1004), `tui_help` for on-demand command reference (#1708), and expanded i18n coverage (#790).

4. **Remote workbench consolidation** — Unified CNB/Lighthouse/Feishu flow (#1984) and a US/global Cloudflare/AWS/Telegram lane (#1990).

5. **Architecture & reliability** — 32-field agent tool schema simplification (#5324), hook-based PreToolUse/PostToolUse lifecycle for universal cancel/pause/resume (#1917), and configurable model-visible read/tool-result size limits (#5367).

---

## Developer Pain Points

- **Long-context reliability**: Sub-agent waits time out and sessions hang on large inputs (#1425); merging large reports is pathologically slow (#1732); output truncation and garbled Chinese text persist (#998, #1675).
- **Windows & environment fragmentation**: SSH outbound blocked by sandbox (#1829), config paths diverge across OS/Cygwin (#2369), PowerShell/cmd command-style mismatches (#1754), and VS Code crashes under YOLO agent testing (#1651).
- **Schema complexity hurting models**: The oversized agent tool schema (32 fields, 8 actions, aliases) causes model errors — a maintainer-acknowledged blocker (#5324).
- **Upgrade & migration friction**: `doctor` stuck on `needs action` after v0.9.4→v0.9.6 (#5340); silent config migration bugs (#2369); legacy `deepseek-tui` users need clear migration paths as the rename lands.
- **Test flakiness in real environments**: Four TUI tests read machine state (`~/.codewhale`, display probe) and fail on dev boxes while CI stays green (#5359) — a maintainability tax on contributors.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*