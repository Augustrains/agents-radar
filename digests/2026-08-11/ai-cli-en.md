# AI CLI Tools Community Digest 2026-08-11

> Generated: 2026-08-11 00:45 UTC | Tools covered: 9

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
**Date:** 2026-08-11

---

## 1. Ecosystem Overview

The AI CLI tool landscape is rapidly maturing, with major players (Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI) and niche contenders (OpenCode, Pi, Qwen Code, DeepSeek TUI) all shipping frequent releases while grappling with similar reliability challenges. Windows stability and session management remain the dominant cross-cutting pain points, with nearly every tool reporting platform-specific regressions or fragility in long-running workflows. Enterprise policy enforcement and model availability are emerging as key differentiators, particularly for GitHub Copilot CLI and Claude Code. The ecosystem is also witnessing architectural convergence—multi-agent coordination, context compaction, and persistent memory are being pursued independently across multiple projects. Security hardening (SSRF, prompt injection, sandboxing) is rising in priority as these tools gain access to increasingly sensitive operations.

---

## 2. Activity Comparison

| Tool | Hot Issues | PRs (Active/Merged) | Releases Today | Release Velocity (Recent) |
|------|-----------|-------------------|----------------|--------------------------|
| **Claude Code** | 10 highlighted (120👍 top issue) | 4 key PRs (2 open, 2 closed) | v2.1.227 (bugfix) | High (multiple per week) |
| **OpenAI Codex** | 10 highlighted (81👍 top issue) | 10 key PRs (all merged) | 2 alphas (0.148.0-a.6, 0.147.0-a.6.6) | Very High (~20 PRs/24hr) |
| **Gemini CLI** | 10 highlighted (8 reactions top) | 10 key PRs (mixed status) | v0.56.0-nightly | Medium-High (nightly) |
| **GitHub Copilot CLI** | 10 highlighted (11👍 top issue) | 0 PRs updated | v1.0.79 | Medium (feature releases) |
| **Kimi Code CLI** | 1 active issue | 0 PRs | None | Low (quiet phase) |
| **OpenCode** | 10 highlighted (22👍 top issue) | 10 key PRs (all open/merged) | v1.18.16 (bugfix) | High |
| **Pi** | 10 highlighted (21 comments top) | 8 key PRs (3 open, 5 closed) | None | Medium |
| **Qwen Code** | 10 highlighted (10 comments top) | 10 key PRs (mixed status) | v0.21.9 (stable) + nightly | High |
| **DeepSeek TUI** | 7 noteworthy | 3 key PRs (1 open, 2 merged) | None (v0.9.6 shipped yesterday) | Low-Medium |

**Notable observations:**
- **OpenAI Codex** is iterating fastest with ~20 infrastructure PRs merged in 24 hours
- **Kimi Code CLI** is in a quiet phase with zero activity—community patience wearing thin
- **Claude Code** and **OpenCode** ship frequent bugfix releases but face regression backlash
- **DeepSeek TUI** shows a deliberate "subtractive" release philosophy (v0.9.6 removes guards)

---

## 3. Shared Feature Directions

### 3.1 Windows Stability & Platform Parity
| Tool | Specific Need |
|------|--------------|
| **Claude Code** | GPU process crashes, install failures, fullscreen TUI corruption |
| **OpenAI Codex** | Freezes, DWM composition leaks, Computer Use broken on Windows |
| **GitHub Copilot CLI** | Plugin update file locks, `/cwd` quoting bugs, render-loop regression |
| **Qwen Code** | Startup banner rendering issues on Windows |
| **OpenCode** | Focus loss in desktop app, RTL layout glitches |

### 3.2 Session/Context Management
| Tool | Specific Need |
|------|--------------|
| **Claude Code** | Unified session history across CLI+desktop (120👍), transcript fragility |
| **OpenAI Codex** | GPT-5.6 Sol 372K context restoration (18👍), stuck tasks after disconnect |
| **GitHub Copilot CLI** | 5MB limit breaks `/compact`, oversized events.jsonl unloadable |
| **DeepSeek TUI** | Compaction transparency, configurable thresholds (3 concurrent issues) |
| **OpenCode** | Edit snapshots cause unbounded growth, infinite loops after tool calls |
| **Gemini CLI** | Auto-memory retrying low-signal sessions, redaction timing |

### 3.3 Multi-Agent Coordination
| Tool | Specific Need |
|------|--------------|
| **Qwen Code** | Fleet architecture (4 staged issues for native multi-session coordination) |
| **Gemini CLI** | Subagent reliability (hangs, MAX_TURNS misreporting, adoption gaps) |
| **DeepSeek TUI** | Unified task surface (shells + subagents + workers) |
| **Claude Code** | Budget-aware context management for subagents |
| **GitHub Copilot CLI** | Parallel explore fan-out hitting per-model rate limits |

### 3.4 MCP & Tool Integration Reliability
| Tool | Specific Need |
|------|--------------|
| **OpenAI Codex** | OAuth credential contention, MCP form input support |
| **Gemini CLI** | OAuth token refresh with stored client ID, SSRF via DNS rebinding |
| **Claude Code** | claude-in-chrome file_upload failures, socket leaks |
| **GitHub Copilot CLI** | 60-second init budget kills sessions, fail-closed policy drops servers |
| **OpenCode** | Provider config leaks into API requests, Copilot multi-turn 404s |

### 3.5 Enterprise Policy & Compliance
| Tool | Specific Need |
|------|--------------|
| **GitHub Copilot CLI** | Model availability unreliable, org-enabled models missing (3 related issues) |
| **Claude Code** | CVP-approved orgs still blocked, usage-limit transparency |
| **OpenAI Codex** | Configurable goal token budgets, request metadata for traceability |

### 3.6 Context Compaction & Token Efficiency
| Tool | Specific Need |
|------|--------------|
| **DeepSeek TUI** | Survival contract, visible token drops, 1M-context models forced to 128K |
| **Claude Code** | Compaction over Opus 4.6/1M context, skill frontmatter opt-out |
| **OpenAI Codex** | Context window restoration demand |
| **Gemini CLI** | AST-aware tooling to reduce token noise |

---

## 4. Differentiation Analysis

### Target User & Positioning

| Tool | Target User | Positioning |
|------|------------|-------------|
| **Claude Code** | Professional developers at scale | Enterprise-grade agent with desktop companion, focus on safety (cyber-safeguards, compliance) |
| **OpenAI Codex** | Power users & early adopters | Cutting-edge alpha velocity, deep sandbox/security posture, Computer Use | 
| **Gemini CLI** | Google ecosystem developers | Deep IDE integration (VS Code companion), strong eval infrastructure (76 tests) |
| **GitHub Copilot CLI** | GitHub-centric enterprises | Tightest GitHub integration, enterprise policy enforcement, agent framework |
| **OpenCode** | Open-source tinkerers | Runtime-neutral architecture (Cloudflare workerd), TUI-first with desktop polish |
| **Pi** | Terminal purists | Lean, philosophical (subtractive design), fullscreen TUI focus; honest about weaknesses |
| **Qwen Code** | Qwen/AliCloud ecosystem | Multi-agent "fleet" vision, WebShell/daemon architecture, browser control |
| **DeepSeek TUI** | Rust-conscious OSS users | "Subtractive" philosophy—fewer guards, one stable prompt; rebranding to CodeWhale |
| **Kimi Code CLI** | Moonshot AI users | Quiet; memory system is the sole focus of community interest |

### Technical Approach

| Tool | Architecture | Notable Tech |
|------|-------------|--------------|
| **Claude Code** | Closed-source core, plugin ecosystem | Fable, Cowork, skill frontmatter |
| **OpenAI Codex** | Rust-based, alpha-channels | Hermetic Windows SDK, MCP OAuth hardening |
| **Gemini CLI** | TypeScript, nightly releases | Behavioral evals, AST-aware exploration |
| **GitHub Copilot CLI** | TypeScript/React (Ink) | Custom agent YAML, enterprise policies |
| **OpenCode** | TypeScript (Bun/Node) | Runtime-neutral refactoring, Web UI embedding |
| **Qwen Code** | TypeScript multi-process | ACP protocol, daemon architecture, WebShell |
| **Pi** | Rust | Zero-dependency philosophy, TUI-first |
| **DeepSeek TUI** | Rust | Crate decomposition (EPIC-005), provider-agnostic core |

### Key Differentiators
- **Claude Code** leads in desktop integration ambition (unified history request = #1 signal)
- **OpenAI Codex** is most aggressive in alpha iteration velocity but worst at changelog transparency
- **Gemini CLI** has strongest eval/test culture (model capability regression catching)
- **GitHub Copilot CLI** leads enterprise policy features but suffers most from server-side opacity
- **Qwen Code** is betting big on multi-agent fleets—unique in the space
- **DeepSeek TUI/Pi** differentiate through aesthetic purity: fewer features, more polish
- **Kimi** is dormant but the memory-system demand (31 comments on 5-month-old issue) shows latent growth potential

---

## 5. Community Momentum & Maturity

### Rapidly Iterating (High momentum, high risk of regressions)
- **OpenAI Codex** — 20 PRs/day; alpha releases; Windows stability pushing back
- **Claude Code** — Frequent bugfix releases; regressions measured by community bisecting
- **Qwen Code** — Stable release + nightly; fleet architecture ramping to P1 issues

### Steady Progress (Medium momentum)
- **Gemini CLI** — Nightly cadence; strong security fixes; eval culture
- **OpenCode** — v1.18.x iterations; performance regression is top concern
- **GitHub Copilot CLI** — Feature releases; enterprise model issues accumulating
- **Pi** — Quiet but deliberate: merges targeted fixes weekly

### Slower / Consolidating
- **DeepSeek TUI** — v0.9.6 is subtractive; EPIC-005 signals refactoring phase
- **Kimi Code CLI** — No activity; community waiting for roadmap signal

### Community Engagement Signals

| Tool | Engagement Proxy | Sentiment Signal |
|------|-----------------|------------------|
| **Claude Code** | 120👍 on session history | High desired, frequent regression complaints |
| **OpenAI Codex** | 81👍 on Windows freezes | High engagement, urgent stability demand |
| **GitHub Copilot CLI** | 11👍 on policy issues | Enterprise frustration, trust erosion |
| **OpenCode** | 46 comments on CPU bug | Active debugging culture |
| **Gemini CLI** | P1 tags + reactions | Maintainer-responsive, security-aware |
| **Pi** | 21 comments on WSL login | Niche but engaged |
| **Qwen Code** | P1/P2 tagging with autofix | Maintainer-driven, automated remediation |
| **DeepSeek TUI** | 3 compaction issues | Small but vocal; maintainer engages |

---

## 6. Trend Signals

### 6.1 The "Trust Gap" in Metering & Billing
Rapid unexplained usage consumption (Claude Code #85446), Max-plan gating without subscription context (#80749), and Copilot model availability denials (#1595, #4422) all point to **metering/billing transparency as a critical trust surface**. Developers are actively bisecting regressions and measuring behavior changes—tools that obscure metering logic will suffer reputation damage.

### 6.2 Session Fragility is the New Reliability Frontier
With 5MB CAPI limits breaking `/compact` (Copilot), oversized JSONL making sessions unloadable (#4325), interactive sessions not writing transcripts (Claude #85665), and rewind index misalignment (Qwen #8885), **long-running session management is the weakest link in agentic workflows**. This is where enterprise adoption will stall first.

### 6.3 Windows as the Hardest Problem
Every single tool reports Windows-specific bugs—from GPU crashes to install failures to DWM leaks. The signal is unambiguous: **cross-platform parity is not being achieved; Windows remains a second-class citizen**. Teams that invest here first will gain competitive advantage.

### 6.4 Multi-Agent Architectures are the Next Battleground
Qwen's fleet architecture, Gemini's subagent reliability work, DeepSeek's unified task surface, and OpenCode's runtime-neutral refactoring all point to **multi-agent coordination as the defining architectural trend**. The winners will solve observability (what is every agent doing?) and reliability (why do agents hang?).

### 6.5 Security is Shifting from Sandboxing to Session Security
From SSRF via DNS rebinding (Gemini #28557) to spoofed system-reminders (Claude #74636) to session poisoning via invalid tool calls (Pi #7782), **security is now about session state integrity**—not just what the model can execute, but what traces persist and how they can mislead.

### 6.6 Subtractive Engineering is Emerging as a Valid Alternative
DeepSeek TUI's v0.9.6 ("fewer runtime guards," "one stable base prompt") and Pi's zero-dependency philosophy represent a counter-trend to feature bloat. **As complexity accumulates, tools that consciously subtract will win on reliability and user trust.**

### 6.7 AI-Assisted Development is Becoming Self-Hosting
Tools like Qwen's `qwen review capture-tui` (driving code under review in tmux to capture rendered pixels) and GitHub Copilot's `/code-review` show **AI tools are now being used to test AI tools—a flywheel that accelerates development but also introduces model-bias into QA processes.**

### 6.8 Developer Expectations are Converging on "It Should Just Work"
Across all communities, the most common frustration patterns are: "It says done but isn't," "It worked yesterday," and "Why is this configuration required?" **The bar is rising: developers are not tolerating regressions, configuration complexity, or opaque failure modes.** Tools that communicate honestly (e.g., explicit "survival contracts" for compaction) will build more loyal communities.

---

*Report generated from community digest data, 2026-08-11.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-08-11 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking (Most-Discussed PRs)

**1. document-typography** — [PR #514](https://github.com/anthropics/skills/pull/514) (OPEN)
- **Functionality**: Typographic quality control for AI-generated documents — prevents orphan word wraps, widow paragraphs, and numbering misalignment.
- **Discussion Highlights**: Addresses a universal pain point in AI-generated documents. The community recognized this as a "quietly essential" skill that affects every document Claude produces.
- **Status**: Open. Author PGTBoos has engaged with maintainers; no merge yet.

**2. ODT skill (OpenDocument)** — [PR #486](https://github.com/anthropics/skills/pull/486) (OPEN)
- **Functionality**: Create, fill, read, and convert OpenDocument Format files (.odt, .ods), including ODT-to-HTML conversion.
- **Discussion Highlights**: Fills a significant gap in document-format coverage. Multiple users noted the need for ISO-standard open-source document support alongside existing DOCX/PDF skills.
- **Status**: Open; substantial discussion on scope and template-filling behavior.

**3. self-audit (reasoning quality gate)** — [PR #1367](https://github.com/anthropics/skills/pull/1367) (OPEN)
- **Functionality**: Mechanical file verification plus four-dimension reasoning audit in damage-severity priority order. Universal for any project/stack/model.
- **Discussion Highlights**: Generated strong interest in verification workflows. The "Step 0 mechanical check" approach was praised as practical and model-agnostic. Connected to Issue #1385 proposing a broader three-gate pipeline.
- **Status**: Open; author actively updating (v1.3.0).

**4. skill-creator: run_eval.py fixes** — [PR #1298](https://github.com/anthropics/skills/pull/1298) (OPEN)
- **Functionality**: Fixes the eval harness's 0% recall bug (Issue #556, 10+ independent reproductions) — installs the eval artifact properly, fixes Windows stream reading, trigger detection, and parallel workers.
- **Discussion Highlights**: The most critical infrastructure PR. The skill-creator's optimization loop has been "optimizing against noise." Broke into sub-PRs (#1099, #1050, #1323, #1261), showing community investment in the tooling itself.
- **Status**: Open; a cluster of related fixes converging.

**5. frontend-design skill improvements** — [PR #210](https://github.com/anthropics/skills/pull/210) (OPEN)
- **Functionality**: Revises the frontend-design skill for clarity, actionability, and internal coherence — every instruction must be actionable within a single conversation.
- **Discussion Highlights**: Community feedback centered on making design skills more executable rather than descriptive. A model for iterative skill-quality improvement.
- **Status**: Open since January; long-running refinement.

**6. SAP-RPT-1-OSS predictor** — [PR #181](https://github.com/anthropics/skills/pull/181) (OPEN)
- **Functionality**: Wraps SAP's open-source tabular foundation model for predictive analytics on SAP business data.
- **Discussion Highlights**: Notable for being a domain-specific vertical integration — signals demand for enterprise data-model skills beyond generic document handling.
- **Status**: Open; awaiting maintainer review of the MCP/server dependency.

**7. testing-patterns** — [PR #723](https://github.com/anthropics/skills/pull/723) (OPEN)
- **Functionality**: Comprehensive testing skill covering Testing Trophy model, unit testing (AAA pattern), React component testing with Testing Library, and what NOT to test.
- **Discussion Highlights**: Addresses a clearly stated community need for structured test-generation guidance. Well-received for its philosophy-to-practice arc.
- **Status**: Open; awaiting merge.

**8. color-expert** — [PR #1302](https://github.com/anthropics/skills/pull/1302) (OPEN)
- **Functionality**: Self-contained color expertise: naming systems (ISCC-NBS, Munsell, XKCD, RAL), color spaces with a "what to use when" table, CAM16, etc.
- **Discussion Highlights**: Appreciated for its density and specificity. A reference-style skill that demonstrates how deep domain knowledge can be packaged.
- **Status**: Open; author responsive. Note: Issue #1329 mentions the broader question of whether external contributions are welcome.

---

## 2. Community Demand Trends (From Issues)

**1. Security & Trust Boundary** — [Issue #492](https://github.com/anthropics/skills/issues/492) (43 comments, 👍 2)
The single most-discussed issue. Community skills distributed under the `anthropic/` namespace impersonate official skills, enabling trust-boundary abuse. Risk: users grant elevated permissions to non-official skills. This is the top concern for the ecosystem's future.

**2. Skill-Creator Tooling Reliability** — [Issue #556](https://github.com/anthropics/skills/issues/556) (12 comments, 👍 7) + [Issue #1169](https://github.com/anthropics/skills/issues/1169) (3 comments, 👍 1)
The eval harness's 0% recall bug has been independently reproduced 10+ times. The description-optimization loop is broken on Windows and in trigger detection. The community wants a working authoring pipeline before submitting more skills.

**3. Org-Wide Skill Sharing** — [Issue #228](https://github.com/anthropics/skills/issues/228) (16 comments, 👍 8)
Direct demand for enterprise distribution: shared skill libraries, sharing links, and org-level management. Current manual download/Slack/upload workflow is untenable for teams.

**4. Duplicate Skill Content Across Plugins** — [Issue #189](https://github.com/anthropics/skills/issues/189) (6 comments, 👍 9)
`document-skills` and `example-skills` plugins install identical skills, wasting context window. Signals need for package-level curation and deduplication.

**5. Context-Window Efficiency** — [Issue #1487](https://github.com/anthropics/skills/issues/1487) (4 comments)
The `claude-api` skill eagerly injects ~156k tokens in one call, exhausting the context window. A new class of failure: skills that are technically correct but operationally unusable due to size.

**6. Skills as MCPs** — [Issue #16](https://github.com/anthropics/skills/issues/16) (4 comments)
Persistent demand for exposing Skills as standardized MCP interfaces — treating skills as API-addressable software rather than prompt-injected instructions.

---

## 3. High-Potential Pending Skills (Likely to Land Soon)

- **[document-typography](https://github.com/anthropics/skills/pull/514)** (PR #514) — Widespread consensus this is needed; small, focused scope with clear acceptance criteria. The author has been responsive. **High likelihood of merge.**

- **[testing-patterns](https://github.com/anthropics/skills/pull/723)** (PR #723) — Well-structured, addresses explicit demand for test-generation guidance, and the Testing Trophy model is uncontroversial. **Strong candidate.**

- **[ODT skill](https://github.com/anthropics/skills/pull/486)** (PR #486) — Completes the document-format matrix (DOCX/PDF/ODT). The main open question is template-filling scope. **Likely with revisions.**

- **[self-audit](https://github.com/anthropics/skills/pull/1367)** (PR #1367) — Connected to a broader proposal (Issue #1385), actively maintained, addresses verification gaps no other skill covers. **Potentially lands as a v1 with iteration.**

- **[skill-creator run_eval fix cluster](https://github.com/anthropics/skills/pull/1298)** (PR #1298, plus #1099, #1050, #1323, #1261) — These are blocking the entire skill-authoring workflow. Maintainers are likely to prioritize consolidation here. **High priority for ecosystem health.**

- **[color-expert](https://github.com/anthropics/skills/pull/1302)** (PR #1302) — Deep, well-specified reference skill. Low controversy; adds unique value. **Likely merge.**

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is for **trustworthy skill-authoring infrastructure** — a reliable evaluation loop that verifies skills actually trigger correctly — followed by **verification and quality-gate skills** that ensure AI output is mechanically sound before delivery.

---

# Claude Code Community Digest — 2026-08-11

## Today's Highlights

Release v2.1.227 shipped with a critical fix for subscription-tier flag evaluation and a regression affecting Bash commands under `claude-code-action`, but it has already drawn three fresh bug reports — including a transcript-logging regression and a Windows install failure. Community discussion remains dominated by the hundred-plus-upvote request for unified session history across CLI and desktop surfaces.

## Releases

**v2.1.227** — Two fixes:
- Feature flags were evaluated without the user's subscription tier when a session began with an expired login token, wrongly prompting Max plan users to enable usage credits for Fable.
- Every Bash command failed under `claude-code-action` with an `allowed_no` error; this is now fixed.

## Hot Issues

1. [**CVP-approved org still receives cyber-safeguard blocks in Claude Code**](https://github.com/anthropics/claude-code/issues/84352) — #84352, 32 comments. A previously approved Claude.ai org shows "Under review" again in the Verification Portal and is blocked despite an approval email. High engagement from users with similar compliance-approval friction.

2. [**Sync conversation history between CLI and Claude Code desktop app**](https://github.com/anthropics/claude-code/issues/28791) — #28791, 31 comments, 120 👍. The most-upvoted open feature request: users want one seamless history across CLI and desktop. The companion request for [session sharing with Claude Desktop](https://github.com/anthropics/claude-code/issues/15881) sits at 60 👍.

3. [**Fable 5 gated behind "requires usage credits" in interactive TUI on Max plan**](https://github.com/anthropics/claude-code/issues/80749) — #80749, closed. The original report was partially walked back in a correction comment: not a clean regression in 2.1.216, and 2.1.215 also gates. The v2.1.227 release directly targets this class of bug.

4. [**Cowork stale-cache corruption under Fable 5 — sandbox read view truncates**](https://github.com/anthropics/claude-code/issues/67585) — #67585, 7 comments. Host writes are clean on disk but the sandbox read view truncates; includes a full diagnosis and proposed fix. Data-loss severity tags make this a priority watch.

5. [**`claude-in-chrome` file_upload fails: paths expected array, received undefined**](https://github.com/anthropics/claude-code/issues/84627) — #84627, 7 comments. The MCP tool fails on every call against valid file inputs across three different element refs. Blocks browser-automation workflows.

6. [**Claude Desktop Windows GPU process crash takes down the app**](https://github.com/anthropics/claude-code/issues/83744) — #83744, 6 comments. Exit code 101457950 kills the whole application — desktop stability concern for Windows users.

7. [**Frequent premature compaction + infinite loop + prompt freezing on Opus 4.6 / 1M context**](https://github.com/anthropics/claude-code/issues/41984) — #41984, closed. A long-running complaint about context management; worth monitoring for whether the fix lands in a release.

8. [**Spoofed "file was modified... don't tell the user" system-reminder after Write/Edit**](https://github.com/anthropics/claude-code/issues/74636) — #74636, 5 comments. A security-adjacent report: a system-reminder-style note appears after Claude's own tool calls, instructing it not to surface file changes to the user.

9. [**Rapid, unexplained usage-limit consumption during normal usage**](https://github.com/anthropics/claude-code/issues/85446) — #85446, 2 comments. 5-hour and weekly limits jumped from ~20% to critical within 20 minutes of normal work. Usage-billing transparency is a recurring trust issue.

10. [**2.1.227: interactive sessions never write transcript JSONL**](https://github.com/anthropics/claude-code/issues/85665) — #85665, fresh. A regression measured from 2.1.226; headless `-p` is unaffected. Newest critical release-regression report. Related: [**Windows install fails on all methods with "defines.json" syntax error**](https://github.com/anthropics/claude-code/issues/85663).

## Key PR Progress

1. [**feat: automatic GitHub/GitLab detection and GitLab support for /code-review**](https://github.com/anthropics/claude-code/pull/34951) — #34951, open. Multi-platform support for `/code-review` with auto-detection. Addresses issue #26932. Community has waited five months on this — a clear priority signal.

2. [**plugins: add entroly-context for budget-aware context management**](https://github.com/anthropics/claude-code/pull/85464) — #85464, closed. New community plugin for budget-aware context selection when codebases exceed the context window — directly addresses the context-limit pain point.

3. [**docs: enforce task tool and model metadata**](https://github.com/anthropics/claude-code/pull/9262) — #9262, closed. Documents `claude-3-5-haiku-latest` for commit commands and requires the Task tool in commit workflows. Docs-only, but signals an enforcement direction.

4. [**security-guidance: update default model refs from Opus 4.7/Sonnet 4.6 to Opus 5/Sonnet 5**](https://github.com/anthropics/claude-code/pull/85409) — #85409, open. The `security-guidance` plugin's README and hook code reference outdated models; this updates the `llm.py` `SECURITY_REVIEW_MODEL` default.

## Feature Request Trends

- **Unified session history across CLI and desktop** — the top-voted request (120 👍) plus a companion at 60 👍. Users want one conversation record everywhere.
- **Opt-in, state-independent submit key** — Enter = newline, Mod+Enter = submit, consolidating the "Enter-to-send" cluster across desktop and CLI.
- **Budget-aware context management** — community plugin work and the compaction over Opus 4.6/1M context both point at the same need: more control over context windows. Enter — newline vs submit — is a recurring configuration-complexity complaint.
- **Skill frontmatter opt-out from post-compaction replay** — skills need a way to decline being re-attached after compaction, since stale `$ARGUMENTS` can trigger real side effects (one reported accidental git push).
- **Seamless session sharing with Claude Desktop** — export/import or direct context handoff without manual file juggling.

## Developer Pain Points

- **Usage-limit visibility and billing transparency** — rapid unexplained consumption (issue #85446) and Max-plan users gated for Fable credits (issue #80749) erode trust in metering. The 2.1.227 fix addresses the subscription-tier evaluation path.
- **Session and transcript fragility** — interactive sessions not writing JSONL in 2.1.227; background sessions that `--resume` lists but `--continue` refuses; pasted-text and collapsed-slash-command dispatch bugs (issues #85665, #85657, #85654).
- **Windows desktop and install instability** — GPU process crashes, install failures across npm/ps1/cmd/winget, fullscreen-TUI screen corruption, and binary-upload ENOENT on SSH remotes (issues #83744, #85663, #85651, #78493).
- **System-reminder injection and spoofing concerns** — false "don't tell the user" notes after Write/Edit calls (issue #74636) raise security flags about prompt-injection surface.
- **Tool and MCP reliability** — `claude-in-chrome` file_upload failing on valid inputs (issue #84627); socket leaks from killed sandboxed commands spinning at 100% CPU (issue #85666).
- **Regression cadence** — the community measured the 2.1.227 transcript regression to 2.1.226 and the Fable-gating behavior across 2.1.215–2.1.218, indicating active bisecting and a low tolerance for rapid regressions after releases.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-11

## 1. Today's Highlights

Windows stability remains the dominant community concern, with two long-running performance issues (#20214, #33192) continuing to accumulate engagement alongside a cluster of Computer Use failures and a `Broken pipe` WebSocket regression that leaves tasks stuck in "Thinking" after the latest desktop update. On the development side, the team merged a rapid series of ~20 infrastructure PRs in 24 hours focused on Windows SDK hermeticity, MCP OAuth robustness, and internal refactoring, while two new Rust releases (`0.148.0-alpha.6` and `0.147.0-alpha.6.6`) shipped for early testing.

## 2. Releases

- **rust-v0.148.0-alpha.6** — Alpha release with no public changelog details yet; likely internal iteration toward 0.148 stable.
- **rust-v0.147.0-alpha.6.6** — Patch alpha on the 0.147 track; no public changelog provided.

Both releases are tagged as alpha-quality and aimed at early adopters testing the next development cycle.

## 3. Hot Issues

1. **[#20214 — Codex App freezes on Windows 11](https://github.com/openai/codex/issues/20214)** — 81👍, 93 comments. The most-engaged issue in the backlog by a wide margin. Users on Windows 11 Pro with ample resources (32GB RAM, Ryzen 5) report persistent freezes/stutters. High engagement suggests broad reproducibility across configurations.

2. **[#37458 — Extension fails to load on Windows VSCode](https://github.com/openai/codex/issues/37458)** — 31 comments, rapidly climbing. The Codex panel fails with "The extension couldn't load its resources" on VSCode 1.132.0 Windows x64. Recent report (Aug 7) with 31 comments in 3 days indicates a widespread regression.

3. **[#37013 — Stale node_repl exec context in Computer Use](https://github.com/openai/codex/issues/37013)** — Windows Computer Use only works within a single JS execution. Cross-call reuse fails with transport errors. Core Computer Use functionality is broken for multi-step workflows.

4. **[#37383 — Computer Use app/window discovery fails (0x80070003)](https://github.com/openai/codex/issues/37383)** — Pro x5 subscribers on Windows 11 25H2 cannot discover apps/windows during Computer Use sessions. Complements #37013; together they indicate systematic Windows Computer Use breakage.

5. **[#20930 — Remote connection notifications broken](https://github.com/openai/codex/issues/20930)** — 16👍. No notifications on turn completion when connecting remotely. Long-running issue (since May 4) still unresolved after 3 months.

6. **[#34619 — GPT-5.6 Sol 372k context window regression](https://github.com/openai/codex/issues/34619)** — 18👍. Users demand restoration of the 372k context window or an opt-in setting. High-value feature request from power users that directly impacts agent capability.

7. **[#37403 — macOS Remote Control/CLI thread regression](https://github.com/openai/codex/issues/37403)** — `already has an active writer` after the Aug 7 update. Breaks a common workflow: starting a CLI thread on desktop, continuing it remotely, then resuming locally. Recent regression with developer-level detail.

8. **[#36645 — App exits after Browser Use teardown](https://github.com/openai/codex/issues/36645)** — Complete application exit after task completion when Browser Use session tears down. Severity is high; users lose all state.

9. **[#33192 — DWM Composition handles accumulate](https://github.com/openai/codex/issues/33192)** — Memory/desktop composition leak on Windows 10 22H2 reproducible with terminal tool calls; 22-handle growth per 5 calls. Points to a systematic resource leak in tool-call paths.

10. **[#37894 — WebSocket Broken pipe leaves tasks stuck](https://github.com/openai/codex/issues/37894)** — Regression immediately after 26.803.61601 update. Tasks stuck after `Broken pipe` disconnect, echoing the older #32555. Two separate reports indicate a systemic WebSocket reconnection gap.

## 4. Key PR Progress

1. **[#37875 — Honor configured Windows sandbox level for managed networking](https://github.com/openai/codex/pull/37875)** — Fixes managed networking implicitly forcing elevated sandbox backend even when restricted token was configured. Directly addresses Windows security/least-privilege concerns.

2. **[#37896 — Hermetic Windows SDK and MSVC runtime repositories](https://github.com/openai/codex/pull/37896)** — Pins Windows SDK and MSVC runtime for x64/arm64 with explicit EULA acceptance flag. Improves build reproducibility for Windows contributors.

3. **[#37866 — MCP OAuth credential contention regression tests](https://github.com/openai/codex/pull/37866)** — Tests for non-blocking credential probes under file/secrets store locks. Addresses the class of MCP auth flakiness users reported in #37219 and #37549.

4. **[#37864 — Support MCP form input in full-access user threads](https://github.com/openai/codex/pull/37864)** — Recognizes `openai/standard-form-input` client extension, enabling forms even when tool permissions are auto-approved. Unblocks fully automated workflows that still need user-entered values.

5. **[#37867 — Reject duplicate resolved paths in apply_patch](https://github.com/openai/codex/pull/37867)** — Prevents patches with operations resolving to the same file (`duplicate.txt` vs `./duplicate.txt`). Security hardening against ambiguous patch targets.

6. **[#37889 — Ignore Unix socket proxy settings on Windows](https://github.com/openai/codex/pull/37889)** — Stops macOS-only Unix socket permissions from clamping Windows proxy listeners to loopback. Addresses a Windows-specific configuration leak.

7. **[#37902 — Defer `view_image` processing to history insertion](https://github.com/openai/codex/pull/37902)** — Passes image bytes unchanged, deferring decode/resize to the shared history-insertion path. Simplifies image handling and reduces duplicated logic.

8. **[#37878 — Configurable goal token budget limits](https://github.com/openai/codex/pull/37878)** — Adds `goals.max_goal_token_budget` positive-integer config; rejected goal creation/updates exceeding the budget. Gives users control over token consumption in goal-driven workflows.

9. **[#37895 — Configurable Responses API request metadata](https://github.com/openai/codex/pull/37895)** — Product-owned key/value metadata for every turn payload (16-entry limit, ASCII identifier keys). Enables traceability for enterprise/API users.

10. **[#31901 — Resolve local MCP refs in Code Mode tool schemas](https://github.com/openai/codex/pull/31901)** — Resolves JSON Pointer `$ref` values against schema root in TypeScript tool declarations (`#/$defs/...` and `#/definitions/...` with RFC 6901 escaping). Makes Code Mode schemas more robust for complex MCP servers.

## 5. Feature Request Trends

- **Windows stability is the #1 request theme.** Users across 10+ issues ask for fixes to freezes, crashes, and resource leaks on Windows 10/11. The volume of Windows-specific bug reports in the top 30 is disproportionate to platform share, suggesting significant hardening is needed.
- **Context window control (GPT-5.6 Sol 372k).** Multiple issues request restoration of the larger context window or an explicit opt-in setting. Power users see reduced context as a capability regression.
- **Better remote/headless workflows.** Remote connection notification issues, Remote Control/CLI thread resume, and Android pairing failures all point to demand for first-class remote operation.
- **Sandbox and permission granularity.** Windows sandbox level selection, global permission mode persistence, and MCP form input support indicate demand for more fine-grained control over execution environments.
- **Sidebar/UI ergonomics.** Hover-triggered sidebar disable option, sidebar ordering after pin/unpin, and scrolling issues suggest UX polish is needed, particularly for Windows.

## 6. Developer Pain Points

- **Windows reliability is the biggest recurring frustration.** Issues #20214, #33192, #35606, and #30906 describe freezing, crashing, and resource leaks on Windows 10/11. Users report full-application crashes consuming weekly Pro usage allotments, which has cost implications beyond annoyance.
- **WebSocket disconnect handling is fragile.** Two separate issues (#37894, #32555) document tasks stuck in "Thinking" or with no recovery after `Broken pipe` disconnects. The most recent regression happened immediately after a desktop update, suggesting inadequate reconnection logic.
- **MCP re-authentication loops.** Linear connector repeatedly requests OAuth despite granted access (#37219, #37549 closed as duplicate). MCP auth token contention appears to be a systemic problem the team is actively addressing in PR #37866.
- **Computer Use is broken on Windows.** Issues #37013 and #37383 independently report Computer Use failures on Windows. The feature appears partially functional — working within a single execution context but failing across contexts.
- **No public changelog for alpha releases.** Both rust releases today shipped without release notes. Developers tracking regressions (e.g., #37403 after the Aug 7 update) cannot correlate behavior changes to specific versions without binary searching.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-11

## Today's Highlights
The Gemini CLI community continues to focus heavily on agent reliability and security. Key issues this week center on subagent recovery failing to report turn limits, generalist agent hangs, and security concerns around auto-memory logging and SSRF vulnerabilities. Several high-priority PRs addressing OAuth token refresh, DNS resolution for SSRF protection, and sandbox crash handling are in active review.

## Releases
**v0.56.0-nightly.20260810.gcf22ac7e8** — Nightly release with no new features announced. [Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260809.gcf22ac7e8...v0.56.0-nightly.20260810.gcf22ac7e8)

## Hot Issues

1. **[Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption**](https://github.com/google-gemini/gemini-cli/issues/22323) — P1 bug, 12 comments, 2 reactions. The `codebase_investigator` subagent reports success even when it hits turn limits before doing any analysis. This makes it impossible to distinguish legitimate completion from premature interruption—a critical observability gap.

2. **[Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** — P1 bug, 8 comments, 8 reactions (most-liked this week). Delegation to the generalist agent causes indefinite hangs (up to an hour), making even trivial tasks like folder creation unreliable. Users are working around it by disabling subagent delegation entirely.

3. **[Zerо-Dependency OS Sandboxing & Post-Execution Intent Routing](https://github.com/google-gemini/gemini-cli/issues/19873)** — P2 enhancement, 8 comments. Proposes leveraging Gemini 3 models' native bash affinity with zero-dependency sandboxing—aiming to give the model safe access to POSIX tools for codebase exploration without security trade-offs.

4. **[Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** — P1 epic, 7 comments. Follow-up on behavioral eval infrastructure; 76 eval tests now exist across 6 Gemini models. Community is pushing for more comprehensive component-level testing to catch regressions earlier.

5. **[AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** — P2 epic/follow-up, 7 comments, 1 reaction. Investigates whether AST-aware tools can reduce token noise and improve navigation precision. References `tilth` and `glyph` as potential starting points. Some users are skeptical: the model already handles code structure well, and AST tooling may not justify added complexity.

6. **[Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — P2 bug, 6 comments. Users with custom skills (gradle, git) report the model doesn't proactively leverage them, only using them when explicitly instructed. Persistent gap between feature availability and model adoption.

7. **[Auto Memory retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — P2 bug, 5 comments. Auto Memory re-processes sessions the extraction agent deemed low-signal, wasting tokens. Part of a broader set of memory-system issues filed by SandyTao520 (also: #26525, #26523, #26516).

8. **[Shell command execution gets stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1 bug, 4 comments, 3 reactions. Simple CLI commands that finish still show as active, hanging the session. A recurring pattern of subprocess lifecycle bugs.

9. **[Deterministic redaction and reduced Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — P2 security bug, 4 comments. Auto Memory sends transcript content to models *before* redaction, and can log existing skill content—a privacy/security concern for sensitive codebases.

10. **[Browser Agent ignores settings.json overrides (maxTurns)](https://github.com/google-gemini/gemini-cli/issues/22267)** — P2 bug, 3 comments. Configuration overrides are read correctly during initialization but not applied at runtime—an expectations-vs-reality mismatch for users relying on browser agent customizations.

## Key PR Progress

1. **[Track all activate() Disposables in vscode-ide-companion](https://github.com/google-gemini/gemini-cli/pull/28764)** — Fixes a subtle comma-expression bug where `gemini.diff.accept` command had the wrong scope. Small but important for IDE extension correctness.

2. **[Dynamically resolve Cloud Workstations proxy redirect URI for OAuth](https://github.com/google-gemini/gemini-cli/pull/28688)** — Fixes OAuth failures in Google Cloud Workstations VMs where browser runs locally but environment redirects to `localhost`.

3. **[Resolve swallowed directory mismatch in IDE connections](https://github.com/google-gemini/gemini-cli/pull/28729)** — Fixes IDE companion connection failures under Cider/VS Code forks with virtual FUSE or different directory paths.

4. **[Add tool call formatter and failure summaries to evals](https://github.com/google-gemini/gemini-cli/pull/28305)** — Adds numbered tool-call timelines and failure diagnostics to behavioral eval output—a significant debugging UX improvement.

5. **[Add `eval:validate` static analysis CLI](https://github.com/google-gemini/gemini-cli/pull/28344)** — Validates eval source files against 9 rules with CI-gating exit codes. Could standardize eval maintenance and prevent silent regressions.

6. **[Resolve false model capacity exhaustion and fix core quota lookup mapping](https://github.com/google-gemini/gemini-cli/pull/28730)** — Corrects error messaging around capacity surges, preserves "Keep trying" in UI, and fixes client-side quota lookup mapping.

7. **[Refresh MCP OAuth tokens with the stored client ID](https://github.com/google-gemini/gemini-cli/pull/28481)** — Fixes MCP OAuth refresh for dynamic client registration; local refresh failure previously deleted stored credentials, forcing re-auth every cycle. High-impact for MCP users; closed but merged.

8. **[Fix SSRF vulnerability in web-fetch.ts with async DNS resolution](https://github.com/google-gemini/gemini-cli/pull/28557)** — Addresses `isBlockedHost` bypass via domain names resolving to private IPs; prevents access to `169.254.169.254` and internal ranges. Directly addresses a security vulnerability.

9. **[Handle EACCES in resolveToRealPath to prevent sandbox crash](https://github.com/google-gemini/gemini-cli/pull/28734)** — Fixes CLI crash on startup when macOS Seatbelt sandboxing is enabled; previously only recovered from `ENOENT`/`EISDIR`/etc.

10. **[Prevent boolean thought parts leaking as `[Thought: true]` text](https://github.com/google-gemini/gemini-cli/pull/28624)** — Fixes internal thought part leakage into visible text—a quality-of-life bug affecting prompt readability.

## Feature Request Trends
- **AST-aware tooling (read, search, codebase mapping)** — Multiple, related requests (issues #22745, #22746) for AST-based tools to reduce token noise and improve navigation precision.
- **Better memory system hygiene** — Three related issues from SandyTao520 (#26516, #26522, #26523) focus on auto-memory: quarantining invalid patches, avoiding infinite retries, and deterministic redaction.
- **Improved subagent observability** — Visible subagent trajectories via `/chat share` (#22598) and richer `/bug` reports (#21763) for better debugging context.
- **Zero-dependency OS sandboxing** (#19873) — Safe model access to native POSIX tools, with post-execution intent routing.
- **Subagent adoption push** (#21968) — Better model behavior around proactively using custom skills and sub-agents.

## Developer Pain Points
- **Subprocess/agent lifecycle bugs are a top frustration** — Hangs (#21409), stuck "Waiting input" states (#25166), and MAX_TURNS misreporting (#22323) are breaking basic workflows.
- **Model ignores user configuration** — Subagents running despite being disabled (#22093) and browser agent ignoring `settings.json` overrides (#22267) undermine trust in configuration.
- **Security-hardening needs are evident** — Auto Memory redaction timing (#26525) and web fetch SSRF (#28557) highlight the challenge of secure-by-design agent behavior.
- **Interaction with interactive prompts are flaky** — Getting stuck at interactive prompts like `create vite app` (#22465) breaks scripted workflows.
- **Bash cleanup overhead** — Model-created temp scripts across directories (#23571) create workspace-clutter pain for clean commits.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-08-11

## Today's Highlights

Release v1.0.79 introduces sandbox configuration visibility and new enterprise policy support for allow-all and proxy enforcement. The issue tracker shows a surge in enterprise-related model availability problems, with multiple reports of Anthropic models being incorrectly disabled under Copilot Business/Enterprise accounts. Several critical session-recovery bugs—including the 5 MB payload limit breaking `/compact` and oversized `events.jsonl` files making sessions permanently unloadable—are drawing attention as they effectively kill long-running workflows.

**Release:** [v1.0.79](https://github.com/github/copilot-cli/releases/tag/v1.0.79)

---

## Releases

### v1.0.79 (2026-08-10)

- The `/sandbox` configuration dialog now shows where sandbox settings are stored in `settings.json`.
- Added support for the enterprise `allow-auto-only` policy so `/allow-all auto` works while full allow-all remains blocked.
- Enterprise-managed sandbox policy can now enforce a proxy URL while credentials are handled.

---

## Hot Issues

1. **[#1595 – Sporadic policy blocking issue retrieving models](https://github.com/github/copilot-cli/issues/1595)**  
   Enterprise users with valid subscriptions and remaining quota intermittently get "access denied by Copilot policy" when running `/models`. 29 comments and 11 👍 indicate this is a widespread, long-standing frustration (open since February).

2. **[#2904 – Custom Agent YAML Frontmatter Should Support Reasoning Effort](https://github.com/github/copilot-cli/issues/2904)**  
   Custom `.agent.md` files can pin a model but not a reasoning-effort level. The only workaround is a global CLI flag, which is impractical when mixing lightweight and deep-reasoning agents. 19 👍 — the top feature request in this batch.

3. **[#4345 – Reasoning effort 'medium' not supported for `claude-haiku-4.5`](https://github.com/github/copilot-cli/issues/4345)**  
   When server-side feature flags are active, the CLI repeatedly fails during sub-agent execution because `claude-haiku-4.5` doesn't support `medium` reasoning effort. A model-capability mismatch that should arguably be handled gracefully, not crash the run.

4. **[#4422 – All Claude models disabled under CLI model selection](https://github.com/github/copilot-cli/issues/4422)**  
   A personal Enterprise account that could use Claude models yesterday now gets "This model is disabled" for all of them today, even though they appear enabled in Copilot settings. Rolling back the CLI version did not help, suggesting a server-side policy issue.

5. **[#4390 – Enabled organization models missing from catalogue](https://github.com/github/copilot-cli/issues/4390)**  
   Models explicitly enabled by a Copilot Business org (Claude Sonnet 5, Opus 5, Kimi K3) are missing from the effective catalogue. The CLI reports "disabled by your organization" for models the org actually enabled.

6. **[#4424 – `/compact` cannot recover a session after the 5 MB CAPI payload limit](https://github.com/github/copilot-cli/issues/4424)**  
   Once a session reaches the 5 MB CAPI Responses limit, normal prompts fail *and* `/compact` also fails — there's no way to reduce context and preserve the session. Effectively kills long-running work.

7. **[#4325 – Session permanently unloadable once `events.jsonl` exceeds V8's max string length](https://github.com/github/copilot-cli/issues/4325)**  
   Long-lived sessions become impossible to resume when the session file exceeds V8's max string length. The session still lists in `/resume`, but loading throws — a core session-management fragility.

8. **[#4416 – Parallel explore subagent fan-out dies to per-model 429s](https://github.com/github/copilot-cli/issues/4416)**  
   Parallel task-tool fan-out concentrates all `explore` calls on a single model bucket (`claude-haiku-4.5`), which hits strict burst limits. No backoff and no auto-switch despite `eligibleForAutoSwitch` being set.

9. **[#4095 – Windows plugin update fails with "Access is denied (os error 5)"](https://github.com/github/copilot-cli/issues/4095)**  
   `copilot plugin update` fails on Windows while VS Code is running because the Copilot extension holds watcher handles on installed plugins. 13 👍 — a high-friction Windows-specific workflow blocker.

10. **[#4426 – `/cwd` does not strip surrounding quotes from pasted Windows paths](https://github.com/github/copilot-cli/issues/4426)**  
    Pasting a path from Explorer's "Copy as path" (which includes double quotes) makes `/cwd` treat the quotes as literal characters and append the result as a relative path. Small but annoying daily-driver bug.

---

## Key PR Progress

No pull requests were updated in the last 24 hours.

---

## Feature Request Trends

- **Per-agent reasoning effort (configurable):** The top-voted request ([#2904](https://github.com/github/copilot-cli/issues/2904)) asks for `reasoning_effort` in custom agent frontmatter, alongside the existing `model` field. The community sees the current global `--effort` flag as too coarse.
- **Configurable/hud-style status display:** [#4418](https://github.com/github/copilot-cli/issues/4418) requests a built-in configurable HUD (linking to a community project). Users want visible session state, branch, and context without running `/context`.
- **Prompt caching for Anthropic models:** [#3808](https://github.com/github/copilot-cli/issues/3808) asks for explicit Anthropic prompt-caching optimizations to cut latency and token cost on long system prompts and large codebases.
- **Floating GUI prompt composer:** [#4417](https://github.com/github/copilot-cli/issues/4417) proposes a built-in accessible prompt editor (large text, word wrap, dark theme) — a UX/a11y direction rather than a core-engine one.
- **Constrain `run_factory` to registered names:** [#4425](https://github.com/github/copilot-cli/issues/4425) asks the model not to invent factory names and retry them serially, reducing wasted calls on nonexistent tools.

---

## Developer Pain Points

- **Enterprise model availability is unreliable and opaque.** Multiple reports ([#1595](https://github.com/github/copilot-cli/issues/1595), [#4390](https://github.com/github/copilot-cli/issues/4390), [#4422](https://github.com/github/copilot-cli/issues/4422)) show models being blocked, missing from catalogues, or intermittently denied despite correct org settings. The CLI gives no clear diagnostic path — a major trust issue for enterprise adopters.
- **Sessions are fragile at scale.** Both the 5 MB CAPI limit breaking `/compact` ([#4424](https://github.com/github/copilot-cli/issues/4424)) and `events.jsonl` overrunning V8's string limit ([#4325](https://github.com/github/copilot-cli/issues/4325)) remove the only recovery paths for long-lived sessions. This is a critical reliability gap for agentic workflows.
- **Parallel tool use breaks the model.** Non-deterministic response ordering ([#4420](https://github.com/github/copilot-cli/issues/4420)), per-model 429s on explore fan-out ([#4416](https://github.com/github/copilot-cli/issues/4416)), and subtasks freezing ([#4306](https://github.com/github/copilot-cli/issues/4306)) all point to concurrency handling as a systemic weak spot.
- **MCP handshake and policy edge cases erode trust.** The fixed 60-second MCP init budget with no retry ([#4421](https://github.com/github/copilot-cli/issues/4421)) and the interim fail-closed policy that permanently drops user MCP servers ([#4419](https://github.com/github/copilot-cli/issues/4419)) both cause permanent session damage from transient conditions.
- **Windows remains a second-class platform.** File-lock issues on plugin updates ([#4095](https://github.com/github/copilot-cli/issues/4095)), quoting problems in `/cwd` ([#4426](https://github.com/github/copilot-cli/issues/4426)), and the React/Ink render-loop regression in the integrated terminal ([#4222](https://github.com/github/copilot-cli/issues/4222)) consistently surface.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest**
**Date: 2026-08-11**

### 1. Today's Highlights
The project is currently in a quiet phase with no new releases or merged pull requests in the last 24 hours. Community attention is heavily focused on the long-running **Memory System** feature request (#1283), which remains the single most active discussion thread despite being opened months ago. This sustained interest indicates a strong demand for persistent context as the next major capability for the tool.

### 2. Releases
No new versions were published in the last 24 hours. Stay tuned for future updates.

### 3. Hot Issues
No new issues were opened in the last 24 hours. However, the following issue remains a critical point of discussion:

- **#1283 [Feature Request] Memory System - Persistent context across sessions**
  - **Author:** CatKang | **Created:** 2026-02-27 | **Updated:** 2026-08-10 | **Comments:** 31
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/1283)
  - **Why it matters:** This is the community’s top-voted demand. Users want the CLI to automatically learn project patterns and user preferences, plus support manual persistent instructions. The 5-month timeline and 31 comments show it’s a complex feature requiring careful design around AI-managed vs. user-defined memory, and likely a storage schema. The lack of maintainer updates here is a growing concern.

### 4. Key PR Progress
There are no new or updated Pull Requests in the last 24 hours. The maintainers appear to be focusing on internal development or addressing feedback on existing PRs.

### 5. Feature Request Trends
- **Persistent Context/Memory:** The dominant trend is a push for the CLI to "remember" (project-specific patterns, user preferences, and historical commands). This goes beyond simple history and implies a need for a structured knowledge base within the tool.
- **Long-Running Initiative:** The fact that the Memory System issue remains open without a maintainer response suggests users are waiting for a roadmap update. Interest remains high but patience may be wearing thin.

### 6. Developer Pain Points
- **Lack of Statefulness:** Developers frequently have to re-state context, preferences, or project constraints in every new session. The Memory System request is a direct response to this friction.
- **Feedback Loop on Backlog:** The single active issue being a 5-month-old feature request signals a communication gap. The community is eager for a maintainer's perspective on whether and how this feature will be implemented, indicating frustration with the roadmap visibility.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-11

## Today's Highlights
Release v1.18.16 lands with config-parsing resilience and desktop UX polish, while the community's attention is dominated by a long-running CPU performance regression (#30086) with 46 comments. A wave of `[contributor]` PRs from kitlangton signals a focused refactoring effort to make the core runtime-neutral and filesystem-free for Cloudflare workerd compatibility. Several desktop-specific issues around focus management, session state, and menu accelerators are actively being addressed.

## Releases
**v1.18.16** — Bugfix release focused on stability: config parsing no longer fails on unknown top-level fields, and projects opened from the Home screen are now registered system-wide. Desktop improvements include right-click to open the project menu in Home, plus better fallback handling in file listings.

## Hot Issues
1. **[#30086 — High CPU usage in newer versions](https://github.com/anomalyco/opencode/issues/30086)** — 46 comments, 22 👍. Users report severe CPU spikes with as few as 3 concurrent sessions (previously 10+ were fine), causing system-wide lag. This is the single most-discussed issue and likely a top regression priority.

2. **[#14041 — Copy message as raw markdown](https://github.com/anomalyco/opencode/issues/14041)** — 10 comments. Repeated request (also filed as #41609) for copying LLM responses as raw markdown rather than rich text. Long-standing gap that continues to resurface.

3. **[#26220 — Infinite loop after tool calls (Zen/big-pickle)](https://github.com/anomalyco/opencode/issues/26220)** — 8 comments. Process hangs and ignores input after completing tool calls; affects the "Big Pickle" (GLM 4.6) variant. Includes a community question (#41573) asking what "big pickle" even is, suggesting confusion around model naming.

4. **[#10517 — VS Code extension install ambiguous](https://github.com/anomalyco/opencode/issues/10517)** — 8 comments, 24 👍. Users struggle with auto-install failing; marketplace search yields multiple unrelated "opencode" extensions. High 👍 count signals broad frustration with IDE onboarding.

5. **[#37389 — GitHub Copilot multi-turn 404 with item_reference (v2)](https://github.com/anomalyco/opencode/issues/37389)** — 7 comments. `github-copilot/gpt-5.5` intermittently errors when sending `item_reference`; reopened after a prior close, indicating active v2 work.

6. **[#40958 — DeepSeek V4 Flash Free context capped at 200K](https://github.com/anomalyco/opencode/issues/40958)** — 4 comments. models.dev metadata limits the Zen model to 200K context despite native 1M support. A metadata config fix (see PR #41620) is already in flight.

7. **[#35432 — `tool_call: false` does not disable tools](https://github.com/anomalyco/opencode/issues/35432)** — 3 comments. Config flag is ignored; tools are always resolved and sent, breaking providers without tool-call support. A provider-compatibility blocker.

8. **[#40816 — Edit tool snapshots cause unbounded growth](https://github.com/anomalyco/opencode/issues/40816)** — 2 comments. Full-file before/after snapshots persist per edit call; large sessions get slower at every prompt. Performance architecture concern.

9. **[#40866 — Desktop input fields lose focus](https://github.com/anomalyco/opencode/issues/40866)** — 2 comments. Windows Desktop v1.18.14: clicking or Tab-ing between fields is broken — "basically unusable." Desktop stability is a recurring theme.

10. **[#41593 — Agent config fields forwarded to provider API](https://github.com/anomalyco/opencode/issues/41593)** — 2 comments. `fallbacks` and `persona` agent config keys leak into provider API request bodies, causing validation errors. Config isolation bug.

## Key PR Progress

1. **[#41624 — fix(tui): collapse execute child details](https://github.com/anomalyco/opencode/pull/41624)** — Code Mode `execute` children constrained to one line by default; click to expand/collapse inline. A TUI readability improvement.

2. **[#41622 — refactor(core): skill service stores values, config plugin owns filesystem](https://github.com/anomalyco/opencode/pull/41622)** — Moves filesystem scanning/parsing out of the skill service into the config plugin. Part of the runtime-neutral core direction.

3. **[#41619 — fix(util): no filesystem side effects at global module load](https://github.com/anomalyco/opencode/pull/41619)** — Removes top-level await filesystem writes when importing `@opencode-ai/util/global`. Required for Cloudflare workerd startup.

4. **[#41625 — fix(app): wire desktop menu accelerators](https://github.com/anomalyco/opencode/pull/41625)** — Fixes non-functional accelerators on Windows/Linux where menus are rendered in-app rather than native. Closes #41592.

5. **[#41618 — refactor(core): move plugin discovery and watching to config side](https://github.com/anomalyco/opencode/pull/41618)** — PluginSupervisor now only handles lifecycle; directory discovery and source classification move to config.

6. **[#41525 — feat(cli): embed web UI](https://github.com/anomalyco/opencode/pull/41525)** — Embeds the web application into Bun/Node CLI distributions; adds `opencode web` and TUI `/web` command with authenticated browser launch.

7. **[#41620 — fix(provider): scope DeepSeek V4 Flash sampling defaults](https://github.com/anomalyco/opencode/pull/41620)** — Defaults `top_p` to 0.95 for versioned V4 Flash 0731 and aliases; preserves provider defaults for third-party/self-hosted models.

8. **[#41621 — feat(session): persist previous agent on switch](https://github.com/anomalyco/opencode/pull/41621)** — Adds `previous` field to `agent-switched` messages, mirroring `model-switched`. Improves session auditability.

9. **[#41616 — fix(core): restore parcel watch for git HEAD](https://github.com/anomalyco/opencode/pull/41616)** — Fixes branch label staleness after `git checkout` caused by Bun's `fs.watch` missing rename-based HEAD updates.

10. **[#41615 — fix(core): resolve Cloudflare account endpoints](https://github.com/anomalyco/opencode/pull/41615)** — Routes Workers AI catalog models through the native Cloudflare provider; cleans up models.dev URL templates and passes account ID per model resolution.

## Feature Request Trends
- **Copy as raw markdown** (#14041, #41609): A recurring simple-but-missed feature that keeps getting re-filed, indicating it has broad appeal.
- **Worktree-based workspace switching** (#36048): Developers want CLI-level worktree management (`opencode worktree create|list|remove|switch`) with stash-based context warp.
- **Local LAN provider discovery** (#27554 PR): mDNS-based auto-discovery for local OpenAI-compatible servers, closing the loop on self-hosted workflows.
- **Opt-out exit splash** (#38010): Demand for a cleaner embedded/white-label experience; the issue notes earlier related requests were auto-closed.
- **Subagent sessions prompting** (#40804 PR): Enabling direct prompting of subagent sessions from the web UI composer.

## Developer Pain Points
- **Performance regression** (#30086): A major, recent CPU regression that has cut usable concurrent sessions from 10+ to ~3 — the most commented issue by far.
- **VS Code extension onboarding** (#10517, #31500, #16217): Auto-install consistently fails, and the marketplace search is ambiguous. High 👍 counts show this is widespread.
- **Desktop UX bugs** (#40866, #41560, #41588, #41614): Focus loss, cross-session state leaks, tab state not preserved, and RTL layout glitches — multiple Windows-specific issues suggest QA gaps on Windows.
- **Provider compatibility** (#37389, #35432, #40797): v2 Copilot 404s, `tool_call: false` being ignored, and proxy failures with `anthropic` provider keys show friction with non-standard provider setups.
- **Config/state leakage** (#41593, #41616): Agent fields and stale git HEAD labels surprise users; config isolation and watch fidelity remain rough edges.

---

*Digest generated from GitHub data for anomalyco/opencode on 2026-08-11.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-11

## Today's Highlights

A quiet day on the release front, but the community is actively churning through a backlog of bug reports and PRs. The hottest topics are **WSL login hangs** (#6187), **TUI input handling races** (#7876, #7899), and **provider-specific incompatibilities** (Bedrock, Cloudflare, AI21). Two significant PRs — fullscreen transcript search and fix for Bedrock tool argument sanitization — were merged or closed, signaling steady progress on developer-experience improvements.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#6187 — Pi login hangs in WSL after GitHub Copilot device authorization](https://earendil-works/pi/issues/6187)** (OPEN, 21 comments)  
   The most-discussed issue: device authorization completes in the browser, but the WSL client never detects it. High signal for Linux/WSL users — this is likely a polling or local-server binding issue.

2. **[#7855 — "Response was truncated before completion"](https://earendil-works/pi/issues/7855)** (CLOSED, 4 comments)  
   Intermittent truncation errors with any OpenAI-compatible API (reproduced with local VLLM). Closed with no action — likely a client-side timeout config issue, but unclear if fixed or just triaged out.

3. **[#7850 — GitHub Copilot login fails with 429 rate limiting for large orgs](https://earendil-works/pi/issues/7850)** (CLOSED, 4 comments, 2 👍)  
   Organizations with 20+ available models hit `429 Too Many Requests` during Copilot login. Community upvoting suggests this affects enterprise users.

4. **[#7782 — Invalid Bedrock tool call poisons session](https://earendil-works/pi/issues/7782)** (CLOSED, 4 comments)  
   Bedrock generated a tool call with an empty key `""`, which Pi persisted and replayed on every turn, permanently bricking the session. Critical robustness bug — fixed by PR #7882.

5. **[#7836 — Edit fuzzy match misses whitespace differences](https://earendil-works/pi/issues/7836)** (OPEN, 3 comments, 1 👍)  
   `normalizeForFuzzyMatch` doesn't collapse or strip whitespace, so small models fail edit operations on near-identical content. A quality-of-life issue for weaker models, but no fix yet.

6. **[#7846 — Unable to start 0.84.0/0.84.1 with Bun runtime](https://earendil-works/pi/issues/7846)** (OPEN, 2 comments, 1 👍)  
   Crash at startup: `zlib.createZstdDecompress is not a function` — a Bun/undici incompatibility. Blocks Bun users from upgrading.

7. **[#7791 — Global Undici dispatcher inherits 16 KiB maxHeaderSize](https://earendil-works/pi/issues/7791)** (OPEN, 2 comments)  
   `EnvHttpProxyAgent` is installed without explicit `maxHeaderSize`, causing `UND_ERR_HEADERS_OVERFLOW` on valid responses with large headers. Edge-case but real-world API pain.

8. **[#7876 — Alt+Enter intermittently aborts running task](https://earendil-works/pi/issues/7876)** (CLOSED, 4 comments)  
   In tmux/SSH (no Kitty protocol), `ESC`+`CR` can split across the 10ms StdinBuffer timeout, aborting the active turn. Tightly analyzed, with a fix landed in PR #7899.

9. **[#7794 — APPEND_SYSTEM.md auto-discovery broken](https://earendil-works/pi/issues/7794)** (CLOSED, 3 comments)  
   Two bugs: empty-array truthy check and a discovery function issue. Auto-loading of `~/.pi/agent/APPEND_SYSTEM.md` was silently broken.

10. **[#7869 — AI21 API broken](https://earendil-works/pi/issues/7869)** (CLOSED, 2 comments)  
    AI21 deprecated the old endpoint; Pi returns HTTP 410. Provider-side change requiring a transport update.

## Key PR Progress

1. **[#7913 — Fullscreen transcript search](https://earendil-works/pi/pulls/7913)** (OPEN)  
   Adds `Ctrl+Shift+f` search over the transcript in fullscreen TUI. Highly requested UX feature for long sessions.

2. **[#7882 — Sanitize empty Bedrock tool argument keys](https://earendil-works/pi/pulls/7882)** (CLOSED)  
   Recursively removes empty property names when replaying tool arguments to Bedrock, without mutating persisted data. Directly fixes the session-poisoning bug (#7782).

3. **[#7899 — Prevent split Alt+Enter from interrupting](https://earendil-works/pi/pulls/7899)** (OPEN)  
   Increases the escape-sequence timeout from 10ms to 100ms to prevent aborts when `ESC`+`CR` split across byte reads. Fixes #7876.

4. **[#7901 — Cloudflare Workers AI Gateway transport](https://earendil-works/pi/pulls/7901)** (OPEN)  
   Adds AI Gateway transport over the Cloudflare AI binding, enabling Pi inside Cloudflare Workers. Feature request #7838.

5. **[#7897 — Inherit subagent session config](https://earendil-works/pi/pulls/7897)** (OPEN)  
   Subagents now follow the current session's model/thinking level instead of the last arbitrary session's. Simplifies multi-session workflows.

6. **[#7906 — Fullscreen fixed top bar](https://earendil-works/pi/pulls/7906)** (CLOSED)  
   Adds a fixed top bar showing cwd, git branch, context usage, and auto-compaction state in fullscreen mode. Improves at-a-glance situational awareness.

7. **[#7904 — Normalize single-object edits argument to array](https://earendil-works/pi/pulls/7904)** (CLOSED)  
   Accepts `{oldText, newText}` as a single object (or JSON string) for the edit tool, handling models that don't wrap edits in an array. Lowers friction for weak models.

8. **[#7887 — Add trailing newline after cwd in system prompt](https://earendil-works/pi/pulls/7887)** (CLOSED)  
   Fixes a subtle prompt-formatting bug where the first user message could appear directly after the working directory.

9. **[#7873 — Skip global aliases in bash tool calls](https://earendil-works/pi/pulls/7873)** (CLOSED)  
   Filters out unsupported global aliases (e.g., `alias -g G='| grep'`) that break bash tool execution. Common on zsh-heavy setups.

10. **[#7881 — Reject item_* IDs in message-level input fields](https://earendil-works/pi/pulls/7881)** (CLOSED)  
    Prevents Responses API ID namespace confusion (`item_*` vs `msg_*`) during streaming. Fixes subtle state corruption in tool-call streaming.

## Feature Request Trends

- **Cloudflare AI Gateway support** (#7838, PR #7901): Multiple requests to run Pi inside Cloudflare Workers via the AI binding.
- **TUI fullscreen enhancements**: Search (#7913), fixed top bar (#7906), narrow-width footer (#7884) — a clear push to make fullscreen mode production-ready.
- **Sticky prompt header** (#7802): Keep the last sent prompt visible at the top of the chat, with truncation and a toggle.
- **Three-state tool-output toggle in /export** (#7907): Show/hide/preview tool output in exported HTML — a documentation and sharing workflow improvement.

## Developer Pain Points

- **WSL/SSH input and auth issues**: Login hangs (#6187) and split-key abort races (#7876) continue to plague terminal-based workflows outside macOS.
- **Provider-specific footguns**: Bedrock session poisoning (#7782), AI21 endpoint retirement (#7869), 429 rate limits for Copilot orgs (#7850), and Cloudflare `strict:false` omission (#7896) — providers are the top source of friction this week.
- **Runtime incompatibilities**: Bun startup crash (#7846) and Undici header-size limits (#7791) suggest the Node/Bun runtime layer needs hardening.
- **Model quality workarounds**: Whitespace-insensitive fuzzy matching (#7836) and single-object edit normalization (PR #7904) indicate small models struggle with strict tool-call schemas — a recurring theme as Pi targets weaker backends.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-11

## Today's Highlights

The v0.21.9 stable release shipped with native Qoder plugin installation from multiple sources and QR-code Local Control pairing, while development momentum centers on the multi-agent "fleet" architecture — with four staged implementation PRs now open. The community is actively reporting terminal rendering regressions on macOS and WebShell session-management bugs, with several P1 issues already attracting maintainer attention.

## Releases

### v0.21.9 (stable)
- **Qoder plugin extensions**: Native support for installing plugins from directories, archives, Git repos, URLs, and npm packages, with automatic system-prompt loading ([#8661](https://github.com/QwenLM/qwen-code/pull/8661))
- **Local Control pairing** via QR code for desktop clients

### v0.21.9-nightly.20260811.8c90697ace
- Memory context refresh marker carry-over tests ([#8809](https://github.com/QwenLM/qwen-code/pull/8809))

## Hot Issues

1. **[#8718 — RFC: Native coordination for independent Qwen sessions](https://github.com/QwenLM/qwen-code/issues/8718)** — The umbrella issue for the multi-agent "fleet" roadmap. Proposes a leader dispatching self-contained workers with correlated runtime/task state visibility. Eight comments; actively designed via staged implementation issues (#8840–#8843).

2. **[#8124 — Startup banner missing top lines on first paint](https://github.com/QwenLM/qwen-code/issues/8124)** — Intermittent TUI rendering bug on Windows; the banner's top ~3 lines are omitted on the very first stdout write. Ten comments; correlates with pending provider updates; tagged `welcome-pr`.

3. **[#8557 — Shrinking terminal reprints transcript blocks in scrollback](https://github.com/QwenLM/qwen-code/issues/8557)** — macOS/Warp-specific duplicate output when narrowing the terminal. Eight comments; spawned the fix in PR #8831 and a follow-up (#8849) about input-box jitter during resize.

4. **[#8871 — ACP child process fails with "Unknown argument: acp"](https://github.com/QwenLM/qwen-code/issues/8871)** — `qwen serve` spawns ACP child with `--acp` flag that the child can't parse, causing auth failures. P2, four comments; a CLI argument-parsing regression.

5. **[#8847 and #8870 — E2E test failures on main](https://github.com/QwenLM/qwen-code/issues/8847)** — Two CI failures in interactive provenance tests and ACP integration. Both are tagged `ready-for-agent`, indicating the project's automated remediation loop is active.

6. **[#8888 — Autofix cancels in-progress review-pr, self-reinforcing loop](https://github.com/QwenLM/qwen-code/issues/8888)** — On bot-authored PRs, autofix pushes trigger `pull_request_target` events that cancel review workflows, creating an infinite feedback loop. Three comments; a CI orchestration bug worth fixing soon.

7. **[#8885 — Rewind indexes misaligned with automatic user-role history entries](https://github.com/QwenLM/qwen-code/issues/8885)** — P1 session-management bug exposed by PR #8838: model-facing history can contain automatic entries (cron prompts, notifications) that ChatRecordingService doesn't track, breaking rewind. Three comments.

8. **[#8678 — Preserve current session when large restore times out](https://github.com/QwenLM/qwen-code/issues/8678)** — P1 daemon issue; PR1 merged ([#8691](https://github.com/QwenLM/qwen-code/pull/8691)) implements timeout contracts and observability. Still open for the remaining work.

9. **[#8860 — OpenAI API logs grow unbounded: ~95 GB / 340k files in two months](https://github.com/QwenLM/qwen-code/issues/8860)** — `logs/openai` has no rotation/retention when `enableOpenAILogging` is on. P2 performance/storage issue; a `status/in-progress` fix is being worked.

10. **[#8898 — "Repetitive tool calls detected" API error](https://github.com/QwenLM/qwen-code/issues/8898)** — Users hit constant blocking errors when the model repeats identical tool calls across rounds. Closed as `need-information`; three comments. This pattern suggests a model-level guardrail that may frustrate legitimate workflows.

## Key PR Progress

1. **[#8687 — Guard cross-worktree Git mutations in daemon](https://github.com/QwenLM/qwen-code/pull/8687)** — Adds host-side guard for model-issued shell commands that use `-C`/`--work-tree`/`--git-dir` to escape the session's workspace. Important security hardening for `qwen serve`.

2. **[#8675 — Model-specific reasoning controls across the stack](https://github.com/QwenLM/qwen-code/pull/8675)** — End-to-end reasoning-controls registry (Thinking/Effort) touching Core, ACP, daemon, SDK, and WebShell. First registration: `qwen3`. Currently under `autofix/takeover`.

3. **[#8831 — Fix banner duplication and drag flicker on resize/wake](https://github.com/QwenLM/qwen-code/pull/8831)** — Root cause: the renderer cleared with row count computed at old width, stranding the reflowed banner. Fixes both #8557 and the resize artifacts.

4. **[#8838 — Persist scheduled cron prompts in transcripts](https://github.com/QwenLM/qwen-code/pull/8838)** — Automatic scheduled prompts are now recorded via the cron-message contract before the model turn runs, fixing their disappearance in restored sessions. `review/self-reported`; related issues #8837, #8885.

5. **[#8707 — Qwen WebBridge: direct browser control](https://github.com/QwenLM/qwen-code/pull/8707)** — Exposes Kimi WebBridge-compatible `/command` and `/status` endpoints from `qwen serve` to the Qwen Chrome extension, implementing a 17-action surface with task-scoped ownership.

6. **[#8848 — Redesign Channel policy and workspace management in WebShell](https://github.com/QwenLM/qwen-code/pull/8848)** — Adds direct-message, group-access, session-routing, and workspace-ownership controls for every manageable adapter. Corresponds to issue #8845.

7. **[#8576 — Arrow keys switch @ completion category tabs](https://github.com/QwenLM/qwen-code/pull/8576)** — Replaces Ctrl+arrow/Ctrl+Tab with bare Left/Right when the tab bar is visible; Vim mode follows the same contract. UX simplification for completions.

8. **[#8894 — `qwen review capture-tui`: rendering claims get pixels, not prose](https://github.com/QwenLM/qwen-code/pull/8894)** — Phase 2 of evidence images: the verifier drives code under review in a private tmux server and captures the pane exactly as rendered. A novel approach to UI regression testing.

9. **[#8368 — Add Kimi and Xiaomi MiMo providers](https://github.com/QwenLM/qwen-code/pull/8368)** — First-class presets for Kimi (three access tiers) and Xiaomi MiMo (pay-as-you-go, multiple regions) in `/auth`. Under `autofix/takeover`.

10. **[#8732 — Adopt Goal v3 in ACP sessions](https://github.com/QwenLM/qwen-code/pull/8732)** — Replaces the legacy Stop-hook `/goal` with the canonical Goal v3 state machine: create, status, edit, pause, resume, replace, clear — with canonical notifications in WebShell.

## Feature Request Trends

- **Multi-agent fleet architecture** (#8718, #8840–#8843): The dominant roadmap direction — native coordination for independent sessions, a supervised teammate runtime, persistence/recovery, and terminal attach. Four staged issues with explicit dependencies.
- **WebShell/daemon management** (#8845, #8848, #8891): Channel policy redesign, session-catalog scheduling, and workspace ownership — driving WebShell toward multi-tenant, enterprise-grade session management.
- **Reasoning controls** (#8675): Model-specific Thinking/Effort toggles across all clients — a response to the Qwen3 reasoning line.
- **Terminal UX** (#8576, #8741): Arrow-key navigation for completions, better `/clear` diagnostics when blocked by background tasks.

## Developer Pain Points

1. **Terminal rendering regressions on macOS**: Three related issues (#8557, #8849, #8124) around resize/wake rendering artifacts — banner duplication, input-box jitter, and missing top lines. The fixes in #8831 are promising but the problem space is clearly finicky.

2. **Session management in daemon mode**: Rewind index misalignment (#8885), missing cron prompts in restored transcripts (#8837), and timeout handling for large restores (#8678) — persistent state bugs in `qwen serve`.

3. **Provider update side effects**: The built-in provider updater silently overwrites `model.name`/`model.baseUrl` when the current model belongs to another provider (#8863, closed), and the update prompt repeats indefinitely when custom models are preserved (#8504).

4. **CI orchestration friction**: The autofix/review-pr cancellation loop (#8888) and repeated E2E failures (#8847, #8870) show the project's automated remediation pipeline is still stabilizing.

5. **Unbounded log growth**: 95 GB of OpenAI API logs in two months with no rotation (#8860) — a real storage hazard for long-running users.

6. **Integration gaps**: Help text missing documented flags (#8897), ACP child process argument mismatch (#8871), and false microphone permission warnings on macOS (#8877) — polish issues that erode trust in a stable release.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-11

## 1. Today's Highlights
The project (now visibly rebranded as **CodeWhale** in issue/PR titles, though DeepSeek-TUI remains the repo name) is consolidating around **v0.9.6**, a "subtractive release" focused on **removing runtime guards**, **stabilizing the base prompt**, and **making provider handling more truthful**. A new **EPIC-005: TUI Crate Decomposition** (#5316) was opened to track a major structural refactor of the codebase, while a reliability fix for **subagent depth budgeting** (#5317) landed as the only new open PR. The community continues to push hardest on **context compaction behavior**, with three concurrent issues (#5096, #4394, #5239) highlighting that the feature remains opaque and under-configured.

## 2. Releases
No new releases were published in the last 24 hours. The most recent release, **v0.9.6**, was shipped via PR #5315 (merged/closed on 2026-08-10). Per the PR description, v0.9.6 is a **subtractive release** with the following themes:
- **Fewer runtime guards** — reducing defensive checks that may have caused false positives
- **One stable base prompt** — consolidating prompt variants into a single canonical version
- **Truthful provider endings** — fixing issues where the TUI reported provider/model states that did not match reality
- **Smaller compaction path** — trimming the compaction code while preserving the core provider-agnostic guarantees

## 3. Hot Issues (10 Noteworthy)
1. **[#5316 — EPIC-005: CodeWhale TUI Crate Decomposition (Umbrella)](https://github.com/Hmbown/CodeWhale/issues/5316)**
   Newly opened umbrella EPIC tracking sub-EPICs and FEATs for decomposing the TUI crate. Currently zero comments, but this signals a major architectural shift that will affect all contributors.
2. **[#2870 — EPIC: staged command-boundary refactor (CLOSED)](https://github.com/Hmbown/CodeWhale/issues/2870)**
   Closed after a ~2-month lifecycle with 20 comments. This EPIC tracked the mergeable layers for the command-boundary refactor; its closure suggests the work is fully landed in v0.9.6.
3. **[#5034 — Switching providers can retain an unrelated default model](https://github.com/Hmbown/CodeWhale/issues/5034)**
   Maintainer-reported bug: switching to OpenAI can leave `gpt-5.5` as the default even when it was inherited from a different route. Community has engaged (4 comments); this is a correctness issue that erodes trust in provider switching.
4. **[#5096 — Compaction gain not visible](https://github.com/Hmbown/CodeWhale/issues/5096)**
   User reports `/compact` says "triggered/complete" but the token counter does not drop (e.g., stays at 37K/128K). Several other users on local endpoints (Qwen3.6, DeepSeek v4 Flash). Points to a gap between UI feedback and actual context state.
5. **[#5270 — v0.9.5: unified tasks surface (shell + subagents + durable workers)](https://github.com/Hmbown/CodeWhale/issues/5270)**
   Enhancement request for a single operator-facing list of "things still running": background shells, subagents, Fleet/lane workers, workflow runs. Community wants idle chrome to admit background work is still alive.
6. **[#4394 — Compaction: publish and enforce a structured survival contract](https://github.com/Hmbown/CodeWhale/issues/4394)**
   Maintainer-driven: asks for an explicit contract defining what survives compaction (plan, to-do, subagent state, tool results). Even though implementation exists, users need a documented guarantee.
7. **[#5239 — Model supports 1M context, why trigger compression at 128K?](https://github.com/Hmbown/CodeWhale/issues/5239)**
   User with a 1M-context model finds the TUI compresses at 128K, causing **frequent, unnecessary compaction**. Requests configurability to match model capability.
8. **[#5317 — fix(subagents): cap nested max_depth by inherited budget](https://github.com/Hmbown/CodeWhale/issues/5317)**
   PR linked to issue #5253; fixes a bug where `child_max_spawn_depth_for_spawn` dropped the inherited budget, allowing nested spawns to exceed the session's chosen recursion depth. Important for subagent reliability.
9. **[#5300 — refactor(core): own primary request preparation (CLOSED)](https://github.com/Hmbown/CodeWhale/issues/5300)**
   Merged refactor replacing the unused `ChatRequest` scaffold with the production `MessageRequest` DTO family, moving request preparation into `codewhale-core`. Lays groundwork for EPIC-005.
10. **[#5315 — chore(release): ship v0.9.6 (CLOSED)](https://github.com/Hmbown/CodeWhale/issues/5315)**
    Release-prep PR with no public issue; confirms v0.9.6 shipped and describes its subtractive philosophy.

## 4. Key PR Progress (10 Important PRs)
1. **[#5317 — fix(subagents): cap nested max_depth by inherited budget](https://github.com/Hmbown/CodeWhale/pull/5317)**
   *Open.* Fixes a recursion-depth escalation bug in nested subagent spawning by applying `inherited.min(..)` in the explicit-`max_depth` arm.
2. **[#5300 — refactor(core): own primary request preparation](https://github.com/Hmbown/CodeWhale/pull/5300)**
   *Merged.* Removes the synthetic `ChatRequest` scaffold; introduces `prepare_primary_turn_request` for provider-neutral defaults. A structural step toward crate decomposition.
3. **[#5315 — chore(release): ship v0.9.6](https://github.com/Hmbown/CodeWhale/pull/5315)**
   *Merged.* Release PR for v0.9.6: subtractive changes across runtime guards, base prompt, provider endings, and compaction path.
4. **[#2851 — Reference / proof PR for command-boundary refactor (from #2870)](https://github.com/Hmbown/CodeWhale/issues/2851)**
   *Referenced in EPIC #2870.* The proof-of-concept PR that validated the staged command-boundary refactor approach.
5. **[#5253 — Issue referenced by #5317 (subagent depth budget)](https://github.com/Hmbown/CodeWhale/pull/5317)**
   *Referenced.* The original bug report that #5317 fixes.
6. **[#5316 — EPIC-005: Crate Decomposition (tracked work)](https://github.com/Hmbown/CodeWhale/issues/5316)**
   *Tracking umbrella.* All decomposition sub-EPICs and FEATs will report here; PRs logged under this path will shape the crate structure.
7. **[#5300-related — DTO family migration](https://github.com/Hmbown/CodeWhale/pull/5300)**
   *Merged.* Part of the larger effort to move production `MessageRequest` DTOs from TUI crate into `codewhale-core`.
8. **[#5270-tracked — Tasks panel consolidation](https://github.com/Hmbown/CodeWhale/issues/5270)**
   *Open.* While not a PR itself, this issue will drive PRs consolidating the tasks surface (shell, subagents, Fleet, workflow).
9. **[#4394-tracked — Compaction survival contract](https://github.com/Hmbown/CodeWhale/issues/4394)**
   *Open.* Expected to result in a documentation PR + possibly a config schema change for compaction guarantees.
10. **[#5239-tracked — Configurable compaction threshold](https://github.com/Hmbown/CodeWhale/issues/5239)**
    *Open.* Community request; likely to produce a configuration PR allowing users to set context thresholds per model.

## 5. Feature Request Trends
Across the 7 active issues, three clear feature directions emerge:

1. **Compaction transparency and control** (3 of 7 issues: #5096, #4394, #5239) — Users want:
   - Visible token-count reductions after `/compact` claims success
   - A documented "survival contract" explaining exactly what survives compaction
   - Configurable compaction thresholds matching model context windows (e.g., 1M instead of hard-coded 128K)
2. **Unified session visibility** (#5270) — A single view of all background work (shells, subagents, workers, workflows) rather than scattered panels. Include "idle chrome" cues so the UI admits when work is still alive.
3. **Provider-model coherence** (#5034) — When switching providers, model defaults should be recalculated atomically; no stale model inheritance from prior routes.

## 6. Developer Pain Points
- **"Says done, isn't done" syndrome:** The `/compact` command reports completion but the token counter does not drop. This erodes trust in a core reliability feature and is the single loudest complaint in the digest.
- **Configurability gaps:** Users with large-context models (1M) are forced into compaction at 128K, causing unnecessary churn and potential data loss. Hard-coded thresholds frustrate advanced users on modern hardware.
- **Provider switch residue:** Stale model defaults after switching providers indicate a coherence bug between two state systems (provider and model) that should be updated as one unit.
- **Observability of background work:** Operators have no single mental model of "what is still running," leading to uncertainty about whether it is safe to quit or expect output.
- **Documentation debt around compaction:** Maintainers themselves acknowledge (in #4394) that even though compaction implementation is mature, the *contract* is unpublished — leaving users to guess what survived.

---

*Digest generated from GitHub data for Hmbown/DeepSeek-TUI (CodeWhale), 2026-08-11.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*