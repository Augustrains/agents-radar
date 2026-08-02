# AI CLI Tools Community Digest 2026-08-02

> Generated: 2026-08-02 01:25 UTC | Tools covered: 9

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
**Date:** 2026-08-02

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem is entering a "reliability plateau" phase—feature velocity remains high, but community attention has shifted sharply toward session integrity, cost transparency, and predictable behavior. Across all major tools, the dominant complaint pattern is **silent failures**: models substituting without notice (Claude Code, Copilot CLI), destructive actions taken on false error messages (OpenAI Codex), and false "success" reports (Gemini CLI). A second systemic theme is **session state fragility**: compaction errors, corruption bugs, and unrecoverable sessions plague every tool, undermining trust in long-running autonomous work. Third, **provider flexibility** has become table stakes—users demand BYOK/multi-provider support, and each tool's responsiveness to this demand is becoming a key differentiator. Finally, **Windows and non-UTF-8 locale support** remain the weakest surfaces across all major tools, with recurring installation, path-handling, and encoding failures.

---

## 2. Activity Comparison

| Tool | Issues Filed Today | Active PRs | Release Status | Notable Release |
|------|-------------------|------------|----------------|-----------------|
| **Claude Code** | 18+ | 3 (all closed) | No release; **v2.1.220** | — |
| **OpenAI Codex** | 2 urgent | 8-10 active | No release | — |
| **Gemini CLI** | ~5 | 9 open | **v0.55.0-nightly** | Capacity-exhaustion terminal fix |
| **Copilot CLI** | ~8 | 0 updated | **v1.0.78-2** | Split-view UX fix |
| **Kimi CLI** | 5 | 5 active | **v1.48.0** | — |
| **OpenCode** | ~10 | 10 active | **v1.18.11** | MCP SSE loop fix |
| **Pi** | ~8 | 7 active | No release | — |
| **Qwen Code** | ~7 | 10 active | **v0.21.3** | Enhanced `/review` |
| **DeepSeek TUI** | 4 | 10 active | **v0.9.4 RC** (PR #5044) | xAI login fix |

**Key observations:**
- **OpenCode** and **Qwen Code** are iterating fastest, shipping releases and maintaining steady PR momentum.
- **Claude Code** and **OpenAI Codex** are in "consumption mode"—issues are accumulating faster than fixes are merged.
- **DeepSeek TUI** is in an active release cycle with a burn-down batch covering 8 user-facing fixes.
- **Copilot CLI** is in a between-release lull with zero PR activity in the last 24 hours.

---

## 3. Shared Feature Directions

The following requirements appear across multiple tool communities, indicating strong cross-cutting demand:

1. **Persistent Memory / Cross-Session Context**
   - *Kimi CLI* (#1283 — Memory System, top-voted)
   - *OpenCode* (#20322 — native auto-memory; #40109 — plugin)
   - *Qwen Code* (#8277 — prompt-cache optimization as a proxy)
   - *Gemini CLI* (#26522 — Auto Memory reliability)
   
   **Need:** Native, configurable memory that persists project conventions and user preferences without manual context injection.

2. **Provider Flexibility & BYOK Parity**
   - *Copilot CLI* (#3282 — multi-BYK model; 19 👍)
   - *OpenAI Codex* (#29156 — custom provider parity between CLI/Desktop)
   - *Pi* (#7010 — OpenAI-compatible schema normalization; #7161 — x-client-request-id)
   - *Gemini CLI* (#28600 — new model 404s)
   - *Kimi CLI* (#2576 — provider setup docs)
   
   **Need:** Seamless multi-provider support with consistent behavior regardless of the underlying model or gateway.

3. **Context Compaction, Not Just Clearing**
   - *Claude Code* (#83225 — partial compaction UI mismatch)
   - *OpenAI Codex* (#18490 — compact-and-implement in Plan Mode)
   - *Pi* (#6879 — auto-compaction never triggers; #7048 — truncated summaries)
   - *Qwen Code* (#8279/#8339 — reuse prompt cache during compression)
   
   **Need:** Smart compaction that preserves working memory, isn't destructive, and triggers reliably before token caps are hit.

4. **Voice / Accessibility Control**
   - *Claude Code* (#42700 — TTS + voice mode, 22 👍, top feature request)
   - *Qwen Code* (#3110, #8286 — voice input, private ASR)
   
   **Need:** Hands-free operation for mobile/accessibility workflows.

5. **Cost Visibility & Guardrails**
   - *Claude Code* (#83231 — avoidable GCP spend; #83205 — quota draining fast)
   - *OpenAI Codex* (#36528 — allowance burn; #35816, #31033 — unexplained limit drops)
   
   **Need:** Pre-execution cost warnings, spend telemetry, and attribution for usage.

6. **Model Behavior Transparency**
   - *Claude Code* (#83224 — silent Fable→Opus substitution; #82466 — model config ignored)
   - *OpenCode* (#39875 — privacy/attribution removal)
   
   **Need:** Explicit logging of model selection and substitution; no silent fallbacks.

---

## 4. Differentiation Analysis

| Tool | Primary Target | Technical Approach | Key Distinguisher |
|------|---------------|-------------------|-------------------|
| **Claude Code** | Enterprise/Pro developers | Desktop app + CLI, session-rich | Deep session model, but now facing trust issues from silent behavior changes |
| **OpenAI Codex** | Desktop-first, ChatGPT ecosystem | Full IDE-like experience | Model-agnostic but Desktop app is the weakest surface (Windows + Diff view broken) |
| **Gemini CLI** | Developer workflow automation | Subagent-centric architecture | Strong subagent/skill model, but false "GOAL" success reports erode trust |
| **Copilot CLI** | GitHub-centric, VS Code users | Shell-native, autopilot modes | Tight GitHub integration; BYOK and custom agents are main differentiators |
| **Kimi CLI** | Moonshot API users, Chinese devs | Python-based, hooks system | Web UI tech preview; hooks and locale support are expanding |
| **OpenCode** | Cross-platform, gateway users | TUI + Desktop + Web | Unified marketplace, plugin API (V2); fastest iteration in ecosystem |
| **Pi** | Power users, proxy/gateway operators | Terminal-native, provider-agnostic | Best provider flexibility story (Cline, MiniMax, Fireworks); strong OSS/community health |
| **Qwen Code** | Alibaba/Qwen stack, local model users | CLI + `/review` verification | Verification-first approach (`/review`, `review drive`); strong test/CI maturity |
| **DeepSeek TUI** | DeepSeek/local model users | Rust-based TUI, sandboxed tools | Sandbox posture and permission system; Windows and locale support lagging |

**Key differentiators:**
- **Verification-first (Qwen Code)** vs. **autonomy-first (Claude Code, Copilot CLI)**
- **Provider-agnostic (Pi, OpenCode)** vs. **vendor-locked (Gemini CLI, Claude Code)**
- **Session-rich (Claude Code)** vs. **transcript-light (Pi, DeepSeek TUI)**
- **Desktop-heavy (Codex)** vs. **TUI-native (Pi, DeepSeek TUI, Gemini CLI)**

---

## 5. Community Momentum & Maturity

### Rapid Iteration (High momentum)
- **OpenCode** — Shipping releases (v1.18.11) with 10 active PRs; community responds with new issues within hours; strong bug-fix turnaround (24h for some)
- **Qwen Code** — v0.21.3 in last 24h; 10 active PRs including intelligent review routing and deterministic testing; mature CI culture with bot-filed issues
- **Pi** — Consistent PR velocity (~10 significant PRs); deep root-cause analysis culture; community contributors are filing and fixing issues directly

### Steady but Reactive
- **Claude Code** — Large, vocal community (19+ comments on top issues) but few merged PRs (3, all maintenance); issue backlog growing
- **Gemini CLI** — Nightly releases with targeted fixes; strong maintainer response on regressions (thought_signature fix in <24h)
- **Kimi CLI** — Maintainer-active (ayaangazali filing multiple fixes); smaller community but high signal quality

### Stalling / At-Risk
- **OpenAI Codex** — Issues accumulate without fix (Diff view open 1+ week, Windows setup unfixed since July 10); community engagement rising but trust in resolution is low
- **Copilot CLI** — Quiet period; between releases; zero PR activity in 24h despite new issues

### Maturity Signals
- **Qwen Code** leads on engineering discipline: deterministic E2E tests, autofix pipelines, CI gates, fake-server migrations
- **Pi** leads on provider flexibility and OSS health: active contributor base, multiple provider integrations, high-quality PR reviews
- **Claude Code** and **OpenAI Codex** lead on community size but are at risk of losing trust due to unresolved reliability issues

---

## 6. Trend Signals

1. **Silent behavior = trust killer.** Across every tool, users are demanding explicit opt-in for consequential actions (model substitution, metadata injection, telemetry). The industry is moving from "autonomous by default" to "autonomous with consent."

2. **Session as artifact is the next battleground.** Corruption bugs, unrecoverable sessions, and false status reports are the top reliability complaints. Tools that can guarantee session integrity (Pi's durability barriers, Copilot CLI's V8 limits) will win power users.

3. **Enterprises are hitting cost walls.** The GCP spend incident (#83231) and weekly allowance burns (#36528) signal that unlimited autonomous action is not enterprise-safe. Expect quota management, pre-flight cost warnings, and budget-aware agents to become table stakes.

4. **Validation and verification are emerging as core features.** Qwen Code's `/review drive` and verifier asymmetry work point to a future where agents don't just "do" but "prove." This will be a major differentiator for CI/CD integration.

5. **Provider diversity is the anti-lock-in hedge.** Pi and OpenCode are benefitting most from user demand for BYOK/multi-provider support. Vendors that gate features behind their own models will face increasing pressure.

6. **Windows is still the neglected platform.** Every major tool has Windows- specific blockers: Codex install failures, Claude Code OAuth loops, DeepSeek TUI flag parsing, Copilot CLI WSL issues. Developers on Windows remain underserved.

7. **Terminal ecosystem compatibility is fragmenting.** Warp conflicts (Qwen Code), Terminal.app exits (DeepSeek TUI), WT_SESSION confusion (Copilot CLI), and GBK encoding crashes (Kimi CLI) indicate that TUI tools cannot assume a standard terminal environment.

8. **Memory is converging as a first-class primitive.** From Kimi's Memory System to OpenCode's plugin to Qwen Code's prompt-cache work, cross-session learning is the next major feature frontier—currently all tools are at "manual memory" stage, and the first tool to nail "automatic, non-bloating memory" will have a decisive edge.

---

*Report generated from community digests dated 2026-08-02. All metrics extracted from GitHub issue/PR activity within the last 24 hours unless otherwise noted.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data current as of 2026-08-02 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

### #1 — skill-creator Fixes (Multiple PRs: #1298, #1099, #1050, #1323, #1261)
**Status:** Open (all) | **Activity:** 5 PRs, cross-referenced by Issues #556, #1061, #1169

The most sustained community effort targets `skill-creator`'s `run_eval.py`, which reports `recall=0%` on every skill description—making the description-optimization loop optimize against noise. **#1298** (MartinCajiao) addresses eval artifact installation, Windows stream reading, trigger detection, and parallel workers. **#1099** (joshuawowk) and **#1050** (gstreet-ops) fix Windows subprocess `PATHEXT` and encoding bugs. **#1323** (Polluelo978) fixes trigger detection that misses real skill names. **#1261** (alvingarcia) isolates eval command files from live project registries.

**Discussion highlights:** Windows compatibility is the single largest recurring theme—multiple independent reproductions of the same failure, all blocked on Unix-first assumptions in shared scripts.

---

### #2 — document-typography (#514) by PGTBoos
**Status:** Open | **Created:** 2026-03-04 | **Updated:** 2026-03-13

Typographic quality control for AI-generated documents: orphan word wrap (1–6 words spilling to next line), widow paragraphs (headers stranded at page bottom), and numbering misalignment.

**Discussion highlights:** Broad applicability—these issues affect every generated document, not just niche use cases. Users rarely request typography fixes explicitly, making this a "silent quality" skill.

---

### #3 — pdf case-sensitivity fix (#538) by Lubrsy706
**Status:** Open | **Created:** 2026-03-06 | **Updated:** 2026-04-29

Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` (`REFERENCE.md` → `reference.md`, `FORMS.md` → `forms.md`), which break on case-sensitive filesystems (Linux/macOS).

**Discussion highlights:** Small but critical fix; the same author (#541, #539) is active on DOCX tracked-change ID collisions and YAML description validation—indicating a pattern of deep OOXML/SKILL.md robustness work.

---

### #4 — ODT Skill (#486) by GitHubNewbie0
**Status:** Open | **Created:** 2026-03-01 | **Updated:** 2026-04-14

OpenDocument text creation, template filling, and ODT→HTML conversion. Triggers on 'ODT', 'ODS', 'ODF', 'OpenDocument', 'LibreOffice document'.

**Discussion highlights:** Fills a gap in document-format coverage (the ecosystem has pdf, docx, pptx, xlsx—but not ODF). Complements the existing document-skills plugin.

---

### #5 — frontend-design clarity revision (#210) by justinwetch
**Status:** Open | **Created:** 2026-01-05 | **Updated:** 2026-03-07

Revises the frontend-design skill for clarity, actionability, and internal coherence. Focus: ensuring every instruction is executable in a single conversation, with specificity to steer behavior without over-constraining.

**Discussion highlights:** Represents a class of "education-to-operation" refactors—converting human-oriented documentation into machine-executable instructions (also see Issue #202).

---

## 2. Community Demand Trends

### 🔴 Critical: skill-creator Reliability (Issues #556, #1061, #1169, #1329)
The **single highest-urgency demand** is fixing `run_eval.py` / `run_loop.py` so the description-optimization loop works at all—and works on Windows natively. 10+ independent reproductions of `recall=0%`; multiple 1-line Unix-first assumptions blocking adoption.

### 🟠 High: Security & Trust Boundaries (Issue #492, 43 comments, 2👍)
Community skills distributed under the `anthropic/` namespace impersonate official Anthropic skills, creating a trust-boundary vulnerability. Users may grant elevated permissions to skills they believe are official. Mitigation controls (signing, namespace verification, marketplace moderation) are the most-requested governance feature.

### 🟠 High: Org-Wide Skill Sharing (Issue #228, 16 comments, 8👍)
Skills should be shareable within organizations directly—no `.skill` file downloads via Slack/Teams or manual Settings > Capabilities uploads. A shared skill library or direct sharing link is the top platform feature request.

### 🟡 Medium: Context Window Efficiency (Issue #1487, 4 comments)
The `claude-api` skill eagerly injects ~156k tokens in a single tool call, exhausting context. Demand: skills must be lazy-loaded or size-bounded; eager injection is a design anti-pattern.

### 🟡 Medium: Deduplication & Plugin Hygiene (Issue #189, 6 comments, 9👍)
`document-skills` and `example-skills` plugins install identical content, causing duplicate skills in context. Demand: manifest-level dedup and clearer plugin boundaries.

---

## 3. High-Potential Pending Skills

| Skill | PR | Author | Last Updated | Notes |
|---|---|---|---|---|
| **self-audit** | [#1367](https://github.com/anthropics/skills/pull/1367) | YuhaoLin2005 | 2026-07-02 | Mechanical file verification + four-dimension reasoning audit (v1.3.0); pairs with Issue #1385 proposal |
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Palo-Alto-AI-Research-Lab | 2026-07-27 | Addresses planning-artifact lifecycle gap (#1417); credits community for naming/ framing |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | meodai | 2026-07-21 | Comprehensive color naming systems (ISCC-NBS, Munsell, XKCD, RAL) + color-space selection table |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | 4444J99 | 2026-04-21 | Testing Trophy model, AAA pattern, React Testing Library, edge cases, naming conventions |
| **pyxel** | [#525](https://github.com/anthropics/skills/pull/525) | kitao | 2026-07-15 | Retro/pixel-art/8-bit game development via pyxel-mcp; write→run→capture→iterate loop |
| **skill-quality-analyzer + skill-security-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | eovidiu | 2026-01-07 | Meta-skills evaluating structure/documentation (20%), security posture, and quality across five dimensions |

*All are open PRs with active commentary; none have been merged as of the data snapshot.*

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is a reliable, secure skill-creation feedback loop** — fixing `run_eval.py`/`run_loop.py` so description optimization actually works (cross-platform), while simultaneously demanding trust-boundary controls (namespace impersonation) and context-window discipline (eager injection caps), before expanding into new skill categories.

---

# Claude Code Community Digest — 2026-08-02

## Today's Highlights
A wave of new bug reports (18+ filed today) suggests the recent 2.1.220 release introduced regressions in session management, model selection, and hook execution. Notably, users are reporting **silent model substitution** (Fable → Opus), **injected session links in git history**, and **several context-window/compaction issues** — all pointing to growing friction around session control and transparency. The long-standing **OAuth login loop** (#77966) remains the most active thread with 19 comments, while a new **cost-transparency complaint** (~$19 in unexpected Google Cloud spend) signals mounting concern over agent autonomy.

## Releases
No new releases in the last 24 hours. Latest known version remains **2.1.220**.

## Hot Issues

1. **[#77966 — OAuth login loop: state parameter dropped after "sign in again" redirect](https://github.com/anthropics/claude-code/issues/77966)** — 19 comments, 13 👍
   The most active thread. Users on Linux/IntelliJ hit an infinite login redirect when the OAuth state parameter is dropped mid-flow. Blocking all authentication and extremely frustrating for multi-platform teams. Community has confirmed it's a server-side redirect issue, not local config.

2. **[#42700 — TTS readback + voice mode for Remote Control sessions](https://github.com/anthropics/claude-code/issues/42700)** — 13 comments, 22 👍
   The highest-reacted open feature request. Users want hands-free operation of Remote Control sessions via text-to-speech and voice commands. Strong demand signal for mobile/accessibility workflows.

3. **[#80279 — Regression in 2.1.217: "Last Activity" filter missing when grouping by Project](https://github.com/anthropics/claude-code/issues/80279)** — 10 comments, 13 👍
   The desktop app's sidebar lost the "Last Activity" date filter after the auto-update to 2.1.217. A clear regression with high user impact — session triage is significantly harder without it.

4. **[#73638 — Renaming a session mid-tool-call corrupts transcript permanently](https://github.com/anthropics/claude-code/issues/73638)** — 8 comments
   Renaming a session while a `server_tool_use` call is in-flight injects a system-reminder as a user turn, causing a permanent 400 error on all future prompts. Data-corrupting bug with a repro — severe for long-running projects.

5. **[#74113 — Background agents idle without delivering final SendMessage report](https://github.com/anthropics/claude-code/issues/74113)** — 6 comments, 5 👍
   Windows users report background agents going silent — the final report never arrives unless manually re-pinged. Breaks the trust model for async agent workflows.

6. **[#82466 — Default model in settings.json not honored at session start](https://github.com/anthropics/claude-code/issues/82466)** — 4 comments
   Even with `"model": "claude-fable-5[1m]"` set in global settings, sessions launch on a different model and `/model` doesn't reliably fix it. Configuration not being respected is a fundamental trust-breaker.

7. **[#83011 — iOS Simulator helper crash-loops on macOS 27 beta (Metal/CoreImage NSException)](https://github.com/anthropics/claude-code/issues/83011)** — 3 comments
   `claude-ios-sim` crashes in `recordBinaryArchiveUsage` on macOS 27 beta. Early-adopter platforms are breaking; no workaround available yet.

8. **[#82230 — Embedded ugrep allocates ~29 GB on bounded-quantifier regex, OOM-kills host](https://github.com/anthropics/claude-code/issues/82230)** — 1 comment
   A single grep pattern like `.{0,N}(a|b|c).{0,M}` triggers catastrophic memory use (29 GB RSS) inside the embedded ugrep shim. A DoS-class bug from normal user input.

9. **[#83226 — Session link written into git history by default with no opt-out](https://github.com/anthropics/claude-code/issues/83226)** — 0 comments, filed today
   Claude Code appends `Claude-Session:` URLs to git commit messages and PR descriptions by default. Users never requested it, there's no documented opt-out, and it forces vendor-controlled links into permanent history. Privacy/control concern with broad blast radius.

10. **[#83224 — Subagents silently served different model than requested (Fable → Opus)](https://github.com/anthropics/claude-code/issues/83224)** — 0 comments, filed today
    Even with explicit `model: "fable"`, subagents ran Opus after the first request. No error, warning, or log of the substitution. Silent fallback to a more expensive model raises cost and transparency concerns.

## Key PR Progress
Only 3 PRs updated in the last 24 hours, all closed and authored by **Yigtwxx** (v1.0.0:

- **[#77442 — fix: repair issue-automation telemetry and dead days_back input](https://github.com/anthropics/claude-code/pull/77442)** — Fixes Statsig events timestamped in 1970 (epoched 0) from the dedupe workflow, and restores the `days_back` input that was no longer being read.

- **[#77439 — docs(plugins): sync security-guidance listing with v2.0.0 plugin manifest](https://github.com/anthropics/claude-code/pull/77439)** — The marketplace listing still described the old v1.0.0 security-guidance plugin; this aligns the manifest with the v2.0.0 rewrite from #62586/#62592.

- **[#77443 — fix(ralph-wiggum): make stop hook's jq error handling reachable under set -e](https://github.com/anthropics/claude-code/pull/77443)** — Under `set -euo pipefail`, the jq failure branch was unreachable, masking parse errors and preventing the friendly recovery path in the stop hook.

**Note:** No active feature PRs are in flight — the repository is currently consuming more than contributing.

## Feature Request Trends
1. **Voice/Accessibility (TTS + voice mode)** — #42700 is the top-reacted request; users want hands-free control of Remote Control sessions. Expect this theme to grow on mobile.
2. **Session interoperability between CLI and desktop** — #83225 highlights that partial compaction works in CLI but has no desktop UI, and desktop ignores CLI-created summaries. Users want one session model across surfaces.
3. **Fine-grained session control** — Multiple asks converge: respecting default model (#82466), honoring opt-in vs. opt-out for metadata (session links in git, #83226), and explicit model-substitution warnings (#83224).
4. **Cost visibility and guardrails** — #83231 (avoidable GCP spend) and #83205 (quota draining fast) both demand better spend telemetry and pre-execution cost warnings.

## Developer Pain Points
- **Silent behavior changes**: The cluster of issues around unannounced model substitution, injected git trailers, and filters disappearing (regressions) points to a systemic problem: Claude Code is making consequential decisions without notifying users. The community wants opt-in defaults and visible logs.
- **Session integrity risk**: #73638 (corrupt transcript), #83229 (blocking Stop hook reprints full answer), and #74113 (agents going silent) each break the "session as a reliable artifact" model — devs can't trust long-running sessions or post-hoc review.
- **Context-window management remains painful**: Compaction/summarization is one of the most-complained-about areas — partial summaries are UI-inconsistent (#83225), filtering by activity is broken (#80279), and context-limit diagnostics are misleading with custom base URLs (#82931).
- **Cost and performance anxiety**: Both quota draining abnormally fast (#83205) and avoidable cloud spend (#83231) suggest Claude Code is acting without sufficient user insight, eroding trust in autonomous operation.
- **Tool-system reliability**: The ugrep OOM bug (#82230) and AskUserQuestion permission-request failures (#81607) show that low-level tooling still has sharp edges that can wedge the entire session.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest
**2026-08-02**

---

## Today's Highlights

A quiet 24-hour cycle with no new releases, but a pair of urgent bug reports surfaced on August 1st: a Windows user reports a near-total weekly usage allowance burn in a single day (#36528), and another user reports the Sol model deleting production directories after a misleading "local server not responding" message (#36522). On the engineering side, a batch of `copyberry[bot]` PRs landed that improve TUI performance, raise MCP catalog limits, and increase remote plugin bundle size caps.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#35058 — Codex Diff crashes with "Oops, an error has occurred" in VS Code on macOS](https://github.com/openai/codex/issues/35058)**
   The most-reacted issue this week (👍 111, 44 comments). The Codex Diff tab is completely broken for macOS users across all repositories—even fresh workspaces. This has been open for over a week with no fix in sight, and the high engagement suggests an ecosystem-wide blocker for VS Code users.

2. **[#32149 — Windows setup fails before UAC prompt; both setup options non-functional](https://github.com/openai/codex/issues/32149)**
   Windows users cannot even install the Codex app. The issue has been open since July 10 with 29 comments but no resolution, making this a serious on-ramp problem for new Windows users.

3. **[#33776 — ChatGPT.exe spawns hundreds of taskkill.exe/conhost.exe processes on Windows](https://github.com/openai/codex/issues/33776)**
   A performance nightmare (287+ orphaned processes) that triggers WMI storms and degrades the desktop window manager. 26 👍 shows this is not an edge case.

4. **[#36528 — URGENT: Prolite account weekly Codex usage went 0% → 97% in one day with unstable reset windows](https://github.com/openai/codex/issues/36528)**
   Newly filed (Aug 1) and already drawing attention. A near-total weekly allowance burn in a single day is a metering/rate-limit bug with real operational consequences for paying users.

5. **[#36522 — Sol deleted production server directories after reporting "local server not responding"](https://github.com/openai/codex/issues/36522)**
   A critical safety failure: the model misinterpreted a connectivity error and executed destructive commands. The community reaction is understandably alarmed; this speaks to the need for stronger sandbox guardrails.

6. **[#28103 — Codex desktop MSIX missing Linux codex binary in app/resources — breaks "Run agent in WSL"](https://github.com/openai/codex/issues/28103)**
   With 23 👍 and 7 comments, Windows users on the Microsoft Store build cannot use WSL integration at all. An older issue (June 13) still unfixed.

7. **[#32297 — Built-in image generation repeatedly fails with network error after July 9 desktop update](https://github.com/openai/codex/issues/32297)**
   Another regression introduced by a desktop update that has persisted for nearly a month with no resolved state.

8. **[#20864 — Desktop App laggy: scans all `~/.codex/sessions` rollout files instead of session index/state](https://github.com/openai/codex/issues/20864)**
   Performance scalability issue that grows worse over time as the session directory accumulates. Relevant to heavy users of the Desktop app.

9. **[#29156 — Desktop custom providers are unusable with existing chats and the model picker](https://github.com/openai/codex/issues/29156)**
   Custom model provider support works in the CLI but is broken in the Desktop app, including the model picker and chat history. 17 👍—users clearly want parity between TUI and Desktop.

10. **[#35420 — Work/Codex stream repeatedly disconnects when workspace is OneDrive-backed and OneDrive is degraded](https://github.com/openai/codex/issues/35420)**
    A niche but real integration issue: cloud-backed file sync services break Codex streaming reliability. Highlights the expanding surface area of file-sync interactions.

---

## Key PR Progress

1. **[#31817 — Update models.json](https://github.com/openai/codex/pull/31817)** *(open)*
   Automated model catalog refresh—routine housekeeping, but keeps the CLI/desktop in sync with new model offerings.

2. **[#36534 — Raise the MCP catalog item limit to 2,048](https://github.com/openai/codex/pull/36534)** *(closed)*
   Doubles the paginated MCP tool/resource discovery limit from 1,024 to 2,048. Useful for users with many tools exposed via MCP servers.

3. **[#30977 — Drop parent MCP lifecycle events from forked agent history](https://github.com/openai/codex/pull/30977)** *(closed)*
   Fixes agent-history contamination when forking: parent tool execution events no longer leak into child rollouts, improving subagent isolation.

4. **[#36511 — Support two-stroke TUI key chords](https://github.com/openai/codex/pull/36511)** *(closed)*
   Accepts two-stroke keybindings (e.g., `ctrl-x ctrl-s`) in TUI keymap configs with pending-chord hints. Nice power-user ergonomics improvement.

5. **[#36507 — Retain attempted tool metadata across prompts](https://github.com/openai/codex/pull/36507)** *(closed)*
   Re-attaches `executed_tool_calls` metadata to subsequent prompts (bounded to 32 KiB, prioritizing recent calls). Improves situational continuity without unbounded memory growth.

6. **[#36485 — Increase remote plugin bundle size limits](https://github.com/openai/codex/pull/36485)** *(closed)*
   Remote plugin download cap raised 50 MiB→100 MiB; extracted bundle cap 250 MiB→512 MiB. Accommodates larger plugins without breaking existing deployments.

7. **[#31471 — Extract apps cache logic into ConnectorRuntimeManager](https://github.com/openai/codex/pull/31471)** *(open)*
   Part 1 of 4 for faster connectors. Refactors the Codex Apps tools cache into a scoped, immutable snapshot; discards stale contexts on context switches. A solid architecture cleanup.

8. **[#36482 — Avoid querying terminal size on every TUI redraw](https://github.com/openai/codex/pull/36482)** *(closed)*
   Caches terminal dimensions across redraws (refreshing only on resize events, process resume, etc.). Small but measurable performance win for TUI responsiveness.

9. **[#15261 — Store guardian transcript boundary on review session](https://github.com/openai/codex/pull/15261)** *(open)*
   Long-running PR (since March) that persists the parent transcript checkpoint on the guardian review session, so follow-up reviews only include transcript data since the last review. Improves review efficiency on long sessions.

10. **[#36440 — Extract exec-server request dispatching](https://github.com/openai/codex/pull/36440)** *(closed)*
    Moves JSON-RPC message handling into a dedicated `RequestDispatcher`; connection loop stays focused on I/O and lifecycle. Clean separation of concerns.

---

## Feature Request Trends

1. **Context compaction (not just clearing) in Plan Mode** — [#18490](https://github.com/openai/codex/issues/18490) asks for `Yes, compact context and implement plan` to preserve memory of prior work instead of a full wipe. A recurring theme across issues: users want smarter context lifecycle management.

2. **Custom model provider parity between CLI and Desktop** — [#29156](https://github.com/openai/codex/issues/29156) and related issues highlight a persistent gap: the Desktop app cannot reliably use custom providers, model pickers, or existing chats. Users want the same flexibility they get in the TUI.

3. **Customizable model picker presets** — [#32665](https://github.com/openai/codex/issues/32665) requests user-defined presets in the power slider. A small but clear expression of desire for more user control over model selection.

4. **TUI composer polish** — [#13466](https://github.com/openai/codex/issues/13466) asks for the placeholder text to be disabled via config and for task-aware suggestions. Quality-of-life improvements that reduce friction for daily CLI users.

---

## Developer Pain Points

1. **Windows remains the weakest platform** — Issues range from install failures ([#32149](https://github.com/openai/codex/issues/32149)), native crashes with `0xc0000409` ([#31989](https://github.com/openai/codex/issues/31989)), process storms ([#33776](https://github.com/openai/codex/issues/33776)), missing WSL support binaries ([#28103](https://github.com/openai/codex/issues/28103)), and PS 5.1 installer crashes ([#19559](https://github.com/openai/codex/issues/19559)). The pattern is unmistakable: Windows users are having a materially worse experience than macOS/Linux users.

2. **Rate-limit and usage metering confusion is causing real pain** — [#36528](https://github.com/openai/codex/issues/36528), [#35816](https://github.com/openai/codex/issues/35816), and [#31033](https://github.com/openai/codex/issues/31033) all describe sudden, unexplained drops in weekly usage limits. Users on paid plans are hitting 0% remaining without clear attribution—this undermines trust in the product for power users.

3. **Model-driven safety failures in production contexts** — [#36522](https://github.com/openai/codex/issues/36522) (deleted production directories) and [#34898](https://github.com/openai/codex/issues/34898) (governance loops exhausting usage) are concerning: the model is making irreversible, destructive decisions while reporting false negative status messages. This is the number one risk for enterprise adoption.

4. **Session/context bloat is a recurring performance problem** — [#34268](https://github.com/openai/codex/issues/34268) (110+ GiB of session data from forked history duplication), [#20864](https://github.com/openai/codex/issues/20864) (full session scan on startup), and [#29007](https://github.com/openai/codex/issues/29007) (unbounded thread metadata crashing desktop startup) all point to a systemic issue: session state management does not scale to long-running, multi-agent conversations.

5. **Diff view reliability in the VS Code extension** — [#35058](https://github.com/openai/codex/issues/35058) and [#36016](https://github.com/openai/codex/issues/36016) show the Diff tab is broken for macOS users across multiple extension versions. Given how central diff review is to an agentic coding workflow, this is a core UX gap.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

**Date:** 2026-08-02

---

## 1. Today's Highlights

The Gemini CLI community is actively surfacing reliability concerns around subagent lifecycle management, particularly around false "success" reports when agents hit turn limits and persistent hanging issues. A critical new fix addresses capacity exhaustion being treated as terminal to prevent retry hangs, while a P1 regression fix for the `thought_signature` API error in v0.53.0 is moving through review. A notable load-order race condition fix for environment variables in settings resolution is also pending, which could impact configuration reliability for many users.

---

## 2. Releases

**v0.55.0-nightly.20260801.gf47d6c6f7** (Nightly)

- [`fix(core): classify capacity exhaustion as terminal`](https://github.com/google-gemini/gemini-cli/pull/28599) — Prevents retry hangs when the model's context capacity is exhausted, treating it as a terminal state instead of triggering endless retry loops.
- [`fix(core,cli): propagate InvalidStreamError details to UI`](https://github.com/google-gemini/gemini-cli/pull/28599) — Provides clearer guidance in the UI when an empty response is detected, offering specific next steps instead of a generic error.

---

## 3. Hot Issues

1. [**#22323: Subagent recovery after MAX_TURNS reported as GOAL success**](https://github.com/google-gemini/gemini-cli/issues/22323) ⭐ 12 comments • 2 👍
   `codebase_investigator` reports `status: "success"` with `Termination Reason: "GOAL"` even when it hits MAX_TURNS before doing any work. This masks real failures and misleads users about actual completion — a significant trust issue for autonomous workflows.

2. [**#21409: Generalist agent hangs**](https://github.com/google-gemini/gemini-cli/issues/21409) ⭐ 8 comments • 8 👍
   CLI hangs indefinitely (up to an hour) when deferring to the generalist agent for simple tasks like folder creation. Users found a workaround by instructing the model not to use subagents. High community interest given the 8 upvotes.

3. [**#28600: 404 errors for gemini-3.1pro-preview**](https://github.com/google-gemini/gemini-cli/issues/28600) ⭐ 8 comments • 0 👍
   Users are getting 404 errors when accessing Gemini 3.1 Pro Preview. This is urgent for anyone testing the newest model. No maintainer response yet, beyond bot triage.

4. [**#24353: Robust component-level evaluations**](https://github.com/google-gemini/gemini-cli/issues/24353) ⭐ 7 comments • 0 👍
   Epic tracking expansion from 76 behavioral eval tests across 6 Gemini models. This is foundational for preventing regressions like the recent `thought_signature` bug from shipping in the future.

5. [**#22745: AST-aware file reads, search, and mapping**](https://github.com/google-gemini/gemini-cli/issues/22745) ⭐ 7 comments • 1 👍
   Epic investigating whether AST-aware tooling can reduce token usage and misaligned reads. Could be a major efficiency win for large codebase navigation.

6. [**#21968: Gemini does not use skills and sub-agents enough**](https://github.com/google-gemini/gemini-cli/issues/21968) ⭐ 6 comments • 0 👍
   Anecdotal but consistent: Gemini CLI doesn't proactively leverage custom skills and subagents, even when relevant. Users must manually instruct it, reducing the value of these features.

7. [**#26522: Auto Memory retries low-signal sessions indefinitely**](https://github.com/google-gemini/gemini-cli/issues/26522) ⭐ 5 comments • 0 👍
   Auto Memory can't mark low-signal sessions as processed, causing them to be surfaced repeatedly. Resource waste and noisy memory extraction.

8. [**#25166: Shell command execution gets stuck at "Waiting input"**](https://github.com/google-gemini/gemini-cli/issues/25166) ⭐ 4 comments • 3 👍
   Simple commands that have already completed leave the CLI hanging at a prompt. High frustration — 3 upvotes — because it blocks subsequent work and forces manual interruption.

9. [**#20079: Symlinked agent files not recognized**](https://github.com/google-gemini/gemini-cli/issues/20079) ⭐ 4 comments • 0 👍
   Files in `~/.gemini/agents/` that are symlinks are ignored. This breaks common dotfile management workflows (e.g., synced configs via symlinks).

10. [**#21983: Browser subagent fails on Wayland**](https://github.com/google-gemini/gemini-cli/issues/21983) ⭐ 4 comments • 1 👍
    Browser automation fails on Wayland display servers. A platform-specific blocker for Linux users, with a working `Termination Reason: GOAL` but an actual failure.

---

## 4. Key PR Progress

1. [**#28597 (OPEN): fix(cli): load environment variables before resolving settings placeholders**](https://github.com/google-gemini/gemini-cli/pull/28597)
   Fixes a load-order race condition where `.env` files were ignored during settings placeholder expansion. `size/l` PR with `status/need-issue` — likely fixes a real configuration pain for many.

2. [**#28607 (OPEN): fix(core): preserve functionCall thoughtSignature when stripping thought parts**](https://github.com/google-gemini/gemini-cli/pull/28607)
   Addresses the v0.53.0 regression causing `API Error 400: Function call is missing a thought_signature`. Fixes #28604. High severity (API-blocking for affected users) and `area/agent`.

3. [**#28526 (OPEN): fix(vscode-ide-companion): stop leaking gemini.diff.accept and onDidChangeWorkspaceFolders disposables**](https://github.com/google-gemini/gemini-cli/pull/28526)
   Fixes a parenthesis bug that collapsed two registrations into a no-op comma expression, leaking disposables. Fixes #27790.

4. [**#21307 (OPEN): feat: add support for daemon mode**](https://github.com/google-gemini/gemini-cli/pull/21307)
   Long-running PR (since March) proposing a daemon mode + lightweight client for shell-centric workflows and context-preserving integrations with Unix tools. `help wanted` tag suggests maintainer interest.

5. [**#28613 (OPEN): fix: replace console.error with debugLogger in sdk session**](https://github.com/google-gemini/gemini-cli/pull/28613)
   Small hygiene fix removing an ESLint disable directive for more consistent logging.

6. [**#28612 (OPEN): chore/release: bump version to 0.55.0-nightly.20260801.gf47d6c6f7**](https://github.com/google-gemini/gemini-cli/pull/28612)
   Automated nightly version bump.

7. [**#28619 (OPEN): Update .gitignore to ignore .env and .ai files; add unit tests**](https://github.com/google-gemini/gemini-cli/pull/28619) — Part of a larger PR series; adds proper env files to `.gitignore` to prevent accidental secret leakage.

8. [**#28616 (OPEN): Pending changes exported from your codespace**](https://github.com/google-gemini/gemini-cli/pull/28616) — Auto-generated PR from a codespace export; `size/xs`, likely low value.

9. [**#28617 (OPEN): Add script to connect GitHub repo to GCP project**](https://github.com/google-gemini/gemini-cli/pull/28617) — Adds a DevTools API script for GCP connectivity, part of the same contributor's PR series.

10. [**#28618 (OPEN): Add documentation for approving workflows from forked repositories**](https://github.com/google-gemini/gemini-cli/pull/28618) — Documents fork PR workflow approval process for maintainers.

---

## 5. Feature Request Trends

- **AST-aware tooling** (#22745, #22746): Persistent interest in AST-aware file reads, search, and codebase mapping to reduce token consumption and improve navigation precision. Multiple issues track this as an epic, with `tilth` or `glyph` recommended as starting points.
- **Autonomous agent reliability**: Requests for better agent "self-awareness" (#21432 — accurate flags, hotkeys, self-execution), visibility into subagent trajectories via `/chat share` (#22598), and discouraging destructive behavior (#22672).
- **Browser agent resilience**: Session takeover and lock recovery (#22232) and respecting `settings.json` overrides (#22267) — users want the browser agent to be more robust against crashes and orphaned processes.
- **Daemon mode**: A long-running PR (#21307) pushes for a headless daemon for Unix tool integration — likely to gain traction as more users seek to use Gemini CLI as a backend engine.

---

## 6. Developer Pain Points

- **False success & silent failures**: Subagents reporting "GOAL" when they actually crashed or hit MAX_TURNS (#22323, #21983) erodes user trust in autonomous completion status. This is the top recurring frustration this week.
- **Hangs are pervasive**: Generalist agent hangs (#21409), shell command "Waiting input" after completion (#25166), and interactive prompt hangs (#22465) — users are repeatedly stuck waiting for CLI to return control.
- **Manual override of agent behavior**: Users must explicitly instruct Gemini CLI to use (or not use) skills/subagents (#21968, #22093). The agent's autonomous decision-making doesn't reliably align with user expectations.
- **Memory system noise**: Auto Memory loop issues (#26522) and security concerns about deterministic redaction (#26525) suggest the memory feature needs hardening before wide adoption.
- **Configuration friction**: Symlinked agents not recognized (#20079), settings.json overrides ignored for browser agent (#22267), and environment placeholder races (#28597) — all point to configuration handling that's not yet robust for advanced users.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-02

## Today's Highlights

A steady stream of issue reports continues around session stability, with new bugs around resumed autopilot sessions not retaining mode, session file size limits causing unrecoverable states, and post-fork plan/todo corruption. On the feature side, multi-BYK model support and custom agent reasoning-effort configuration remain top community requests. A new patch release (v1.0.78-2) addresses a UX nit around split-view close confirmation.

---

## Releases

**v1.0.78-2** — [Release Link](https://github.com/github/copilot-cli/releases)

- **Improved** — Split-view sidebar close confirmation now reads `x again to close` (or `x again to exit CLI` on the final session) instead of `x close`, making the second-press action explicit.
- **Fixed** — Extension slash commands run their handler exactly once per invocation when several extensions are present.

---

## Hot Issues

1. **[#3282 — Add multiple BYOK model capability](https://github.com/github/copilot-cli/issues/3282)** *(open, 👍19, 6 comments)*
   Users can currently only configure a single BYOK model via environment variable. Switching models requires terminating the session and restarting. Highly requested.

2. **[#2904 — Custom Agent YAML frontmatter should support reasoning effort](https://github.com/github/copilot-cli/issues/2904)** *(open, 👍16, 3 comments)*
   `.agent.md` files support pinning a model but not a per-agent reasoning effort. Users want `--effort` configurable per custom agent, not just globally.

3. **[#2901 — Lazy-load MCP servers on first tool invocation](https://github.com/github/copilot-cli/issues/2901)** *(open, 👍14, 2 comments)*
   All MCP servers connect at startup, slowing boot times as server counts grow. Community wants on-demand connection.

4. **[#4305 — "Failed to convert JavaScript value 'Undefined' into rust type 'String'"](https://github.com/github/copilot-cli/issues/4305)** *(closed, 👍5)*
   Regression seen after upgrading to v1.0.76 — errors appear on nearly every command. Closed in the last 24h; likely fixed in the 1.0.78.x line.

5. **[#4325 — Session permanently unloadable once events.jsonl exceeds V8 max string length](https://github.com/github/copilot-cli/issues/4325)** *(open, 👍1)*
   Long-lived sessions that grow `events.jsonl` beyond V8 limits become permanently unresumable. Session appears in `/resume` but cannot load. Serious data-loss risk.

6. **[#4327 — BYOK responses streaming drops apply_patch input before execution](https://github.com/github/copilot-cli/issues/4327)** *(open)*
   With OpenAI-compatible `wireApi: "responses"` providers, the model emits complete `apply_patch` input but the CLI invokes the tool with an empty string — breaking an entire provider path.

7. **[#4299 — Increasing typing latency over long copilot sessions](https://github.com/github/copilot-cli/issues/4299)** *(open)*
   Long sessions with background agents become unusably laggy. Community reports it as a top workflow blocker.

8. **[#4306 — Subtasks freeze and stop responding](https://github.com/github/copilot-cli/issues/4306)** *(open)*
   Autopilot workflows that loop between custom agents (e.g., `speckit-implement` ↔ `speckit-converge`) eventually freeze mid-session, requiring full restarts.

9. **[#4318 — Autopilot task-completion enforcement can override explicit user instructions](https://github.com/github/copilot-cli/issues/4318)** *(open)*
   When a user narrows a task to research-only, autopilot's completion enforcement can keep the agent acting anyway. Trust and control concern for autonomous mode.

10. **[#4329 — Autopilot not actually enabled when resuming a session](https://github.com/github/copilot-cli/issues/4329)** *(open, triage)*
    Statusline claims autopilot is on after resume, but approval-gated actions still fail. Misleading UI + broken behavior combo.

---

## Key PR Progress

No pull requests were updated in the last 24 hours. The repository is currently in an issue-heavy phase between release cycles.

---

## Feature Request Trends

- **Multi-model BYOK support** — One key per session; users want multiple BYOK models switchable inside the TUI.
- **Custom agent reasoning-effort control** — Fine-grained per-agent configuration of `--effort`, not just global.
- **Lazy MCP server loading** — Reduce startup latency by connecting MCP servers only when first invoked.
- **Session pinning improvements** — Pinned sessions should appear in a dedicated section at the top when grouping by status.
- **Trusted Access for Cyber program linkage** — Some users need a way to authorize security-related workflows (Claude Opus 5 flagged content).

---

## Developer Pain Points

- **Session corruption / unrecoverable states** — `events.jsonl` size limits and post-fork plan/todo loss are making long-lived sessions risky.
- **Autopilot trust issues** — Resumed sessions lie about autopilot state; completion-enforcement overrides explicit user narrowing; subtasks freeze mid-loop.
- **Provider-specific breakage** — BYOK responses-streaming drops tool input; `.mcp.json` comments silently disable all MCP servers.
- **Input latency degradation** — Long sessions degrade to unusable typing lag, especially with background agents.
- **Installer version pinning broken** — Requesting a specific version still installs latest, blocking downgrade paths for regression testing.
- **Input keybinding bugs** — `Ctrl+H` misread as `Ctrl+Backspace` under WSL2 due to `WT_SESSION` leakage; root-cause confusion between Windows Terminal and the CLI.
- **Nested agent MCP inheritance** — Custom agents two levels deep don't receive declared MCP tools unless an intermediate agent also declares them. Isolate behavior vs. documentation.

---

*Digest generated 2026-08-02 from [github.com/github/copilot-cli](https://github.com/github/copilot-cli)*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-02

## Today's Highlights

The community's long-standing request for a persistent **Memory System** (#1283) continues to gain traction with renewed discussion, signaling strong demand for cross-session context. Meanwhile, maintainer **ayaangazali** has been highly active, submitting multiple high-quality fixes, including a resolution for the `StrReplaceFile` replacement-count bug (#2526) and a critical shell timeout deadlock fix (#2530). Notably, a batch of **Web UI** bugs (#2573, #2574) surfaced in the last 24 hours, pointing to growing adoption of the technical preview but also revealing stability gaps in session management.

## Releases

No new releases in the last 24 hours. Latest known version: **kimi-cli 1.48.0**.

## Hot Issues

1. **[#1283 — Memory System: Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)** — Long-standing, most-discussed enhancement with 10 comments. Request spans automatic and manual memory (project patterns, user prefs). Updated on Aug 1; remains top community priority.

2. **[#2526 — StrReplaceFile reports too few total replacements for chained edits](https://github.com/MoonshotAI/kimi-cli/issues/2526)** — Real correctness bug: sequential edits count against original content instead of running content. PR #2554 proposes a fix; expect merger after review.

3. **[#2573 — Web UI "Connecting to session..." infinite spinner](https://github.com/MoonshotAI/kimi-cli/issues/2573)** — New crash affecting `kimi web` session switching (v1.48.0, macOS arm64, Chrome 150). Indicates Web UI (Technical Preview) stability gap.

4. **[#2574 — Kimi Code Stuck on "Processing" and Doesn't Respond](https://github.com/MoonshotAI/kimi-cli/issues/2574)** — Unity MCP integration halts mid-session; no "Processing" termination. Suggests MCP or event-loop deadlock on prolonged use. Requires maintainer reproduction.

5. **[#2576 — docs: document OmniRoute OpenAI-compatible provider setup](https://github.com/MoonshotAI/kimi-cli/issues/2576)** — Pure docs request for reproducible gateway config (base URL, model, env-var mapping) to prevent misconfiguration. Low friction; likely a quick win.

*Remaining issues (total 5) covered above; no other community activity in window.*

## Key PR Progress

1. **[#2577 — fix(web,vis): do not crash printing startup banner on legacy console codecs](https://github.com/MoonshotAI/kimi-cli/pull/2577)** — Resolves #2532; `print()` with U+279C crashes on GBK (Chinese Windows). Switches to safe printing; critical for non-UTF-8 locales.

2. **[#2575 — fix(hooks): fire PostToolUse hooks through fire_and_forget_trigger](https://github.com/MoonshotAI/kimi-cli/pull/2575)** — Resolves #2564; fixes `asyncio.create_task()` handle-dropping that could terminate pending hook tasks. Reliability fix for asynchronous hooks.

3. **[#2554 — fix(tools): count StrReplaceFile replacements against running content](https://github.com/MoonshotAI/kimi-cli/pull/2554)** — Addresses #2526; corrects replacement counting for chained edits. Small (<100 LOC); likely merged this week.

4. **[#2572 — fix(kosong): recursively unwrap double-encoded JSON in tool-call arguments](https://github.com/MoonshotAI/kimi-cli/pull/2572)** — Handles Moonshot API double-encoding of nested arrays/objects in `function.arguments`; fixes Pydantic validation errors for `StrReplaceFile`, `SetTodoList`, etc.

5. **[#2530 — fix(shell): stop blocking until timeout when a detached child holds the pipes](https://github.com/MoonshotAI/kimi-cli/pull/2530)** — Resolves #2468; `_run_shell_command` now allows early exit despite detached child (e.g., `some_daemon & echo done`) holding stdout/stderr.

*Remaining 5 PRs not updated in window; above represent active work from maintainers and community contributors.*

## Feature Request Trends

- **Persistent Memory System** (#1283): Highest-signal request; desire for both AI-managed and user-defined context persistence across sessions (project patterns, preferences).
- **Provider documentation**: Growing ecosystem of OpenAI-compatible gateways (e.g., OmniRoute) requires clearer setup docs and reproducible configs.
- **Web UI maturity**: Increased usage of `kimi web` Technical Preview — session switching and stability improvements are emerging as themes.

## Developer Pain Points

- **Cross-session context loss**: Repeated requests for memory; developers want CLI to "remember" project conventions and user prefs.
- **Proxy/gateway misconfiguration**: OpenAI-compatible provider setup remains error-prone (base URL, model mapping); better docs are urgent.
- **MCP integration stability**: Unity MCP case (#2574) shows CI/CD tooling integrations can stall silently — more graceful error handling needed.
- **Encoding/locale compatibility**: Non-UTF-8 consoles (GBK) break CLI startup; a sign that international developer base is active and testing on varied platforms.
- **Shell command latency**: Detached children causing premature timeout blocks (#2530); developers expect shell behavior similar to native terminals.

---
*Data source: [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) | Generated: 2026-08-02*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-02

## Today's Highlights

OpenCode shipped v1.18.11 with two targeted bugfixes addressing MCP SSE reconnect loops and interleaved reasoning field configs, while community attention pivoted to policy questions — a hot thread on Go plan wording/attribution removal (35 👍) and new questions about model hosting locations surfaced. Desktop reliability remains the sharpest pain point, with users reporting silent send failures, premature success sounds, and empty-input Enter interrupts, several already receiving fix PRs within 24 hours.

## Releases

**v1.18.11** (latest, last 24h)
- **Core bugfixes**: Stopped MCP SSE connections from getting stuck in reconnect loops after server error responses; fixed provider model configs using interleaved reasoning fields like `reasoning_text` or custom field names.
- **Desktop bugfix**: External links now open in the system browser.

## Hot Issues

1. **[#37012 — Keep legacy layout option](https://github.com/anomalyco/opencode/issues/37012)**
   - 34 comments, 37 👍. Strong community pushback on the new UI; old layout praised for main-window access and workspace ergonomics.

2. **[#39875 — Revert silent removal of Go privacy wording and provider attribution](https://github.com/anomalyco/opencode/issues/39875)**
   - 5 comments, 35 👍. A Go subscriber demands transparency on two recent commits changing what "OpenCode" product branding is shown, plus telemetry/retention additions to the privacy policy. Builds on four earlier no-response issues.

3. **[#32149 — Stops processing requests without response](https://github.com/anomalyco/opencode/issues/32149)**
   - 9 comments. "Thinking" state shows, then nothing — no output, no error. A core reliability complaint with high visibility.

4. **[#20322 — Native auto-memory for cross-session learning](https://github.com/anomalyco/opencode/issues/20322)**
   - 8 comments, 5 👍. Long-standing (since March) request for persisted learnings across sessions; references three related proposals.

5. **[#33028 — Subagents hang indefinitely after quick bash tool call](https://github.com/anomalyco/opencode/issues/33028)**
   - 8 comments. Stream never times out after a quick bash call, affecting two different models (`glm-5.2`, `minimax-m3`). Only manual Esc unblocks.

6. **[#23595 — `<system-reminder>` keeps moving, breaking llama.cpp cache](https://github.com/anomalyco/opencode/issues/23595)**
   - 6 comments, 11 👍. Prompt-history churn forces unnecessary reprocessing; users want a stable system-reminder position.

7. **[#39847 — Information on where the models are hosted](https://github.com/anomalyco/opencode/issues/39847)**
   - 5 comments, 17 👍. DeepSeek V4 stopped working; user signed up on "EU hosted" claims and demands hosting transparency.

8. **[#27837 — Web UI: session list empty on left panel in web server mode](https://github.com/anomalyco/opencode/issues/27837)**
   - 5 comments. `/api/session` returns data but frontend stays empty; root cause traced to SSE event-driven loading logic.

9. **[#17340 — Session compaction fails with "context exceeds model limit"](https://github.com/anomalyco/opencode/issues/17340)**
   - 4 comments. A 128k model hit 145,882 tokens; compaction refuses to strip media, stranding the session.

10. **[#40038 — Desktop makes success notification sound immediately on send](https://github.com/anomalyco/opencode/issues/40038)**
    - 3 comments. Zero feedback after the sound — user has no idea what happened. On v1.18.11.

## Key PR Progress

1. **[#40108 — Add unified marketplace](https://github.com/anomalyco/opencode/pull/40108)**
   - Closes #28696; broad package model with shared runtime for desktop, TUI, CLI, and API clients.

2. **[#40110 — Prevent Enter from sending/interrupting on empty input](https://github.com/anomalyco/opencode/pull/40110)**
   - Fixes #40106 (desktop/web). Empty-input Enter is now a no-op; targets both V1 submission pipeline and V2 interrupt path.

3. **[#39905 — Add system prompt debug command](https://github.com/anomalyco/opencode/pull/39905)**
   - New `opencode debug prompt` CLI command to print the effective system prompt. Addresses three related issues (#24990, #39033, #33333).

4. **[#40109 — Add oc-supermemory-redux plugin to ecosystem docs](https://github.com/anomalyco/opencode/pull/40109)**
   - Documentation-only; new community plugin for persistent memory.

5. **[#26861 — Fix old messages disappearing during long sessions](https://github.com/anomalyco/opencode/pull/26861)**
   - Lazy-scroll loading: loads 50 older messages when near top; fixes #7380.

6. **[#37889 — Fix GitHub OIDC format and error handling](https://github.com/anomalyco/opencode/pull/37889)**
   - Handles GitHub's OIDC token format change and improves error reporting. Closes #37823.

7. **[#34785 — Add RFC 8628 device-flow OAuth for custom gateways](https://github.com/anomalyco/opencode/pull/34785)**
   - Generic device-flow OAuth provider type for custom gateways.

8. **[#34698 — Suppress lone `</think>` chunk at reasoning→tool boundary](https://github.com/anomalyco/opencode/pull/34698)**
   - Emitted `text-delta` for lone closing reasoning markers; now suppressed. Closes #34126.

9. **[#34709 — Add tool result content API (V2 plugins)](https://github.com/anomalyco/opencode/pull/34709)**
   - `Tool.result({ output, content })` + `context.progress(...)`; migrates built-ins and wires replayable progress events.

10. **[#34763 — Support prompt-only new session deeplinks (Desktop)](https://github.com/anomalyco/opencode/pull/34763)**
    - Handles `opencode://new-session?prompt=...` deeplinks. Closes #34762.

## Feature Request Trends

- **Persistent memory / cross-session learning** is the clearest cluster: multiple issues (#20322, #32658) plus a plugin PR (#40109) — the community wants native memory, not manual context injections.
- **Trust & transparency**: Go-plan users are pushing back on privacy wording removal and model hosting opacity (#39875, #39847, #39872) — a trust deficit is forming.
- **UI configurability**: Users want legacy layout opt-out (#37012), collapsible tool output (#40096), and better search/model-grouping controls (PR #34764).
- **MCP flexibility**: Per-server TLS trust config and cert-skip options (#40111, #23506) signal friction with custom/on-prem MCP servers.

## Developer Pain Points

- **Silent failures and dead-end sessions**: Requests stop with no response (#32149), success sound plays with no output (#40038), and desktop sends on empty Enter mid-task (#40106) — a systemic feedback-loop problem.
- **Hangs and infinite retries**: Subagent hangs after bash calls (#33028), `SessionRetry.policy()` retries forever with no cap (#21960, #40090), and compaction can hit "context exceeds model limit" with no recovery path (#17340).
- **Prompt/cache instability**: Moving `<system-reminder>` breaks llama.cpp prefix caching (#23595) and causes unnecessary prompt reprocessing.
- **Web/server mode gaps**: Empty session lists in web UI (#27837) suggest the web server path is under-tested relative to the TUI.
- **Subscription/plan friction**: Free-tier users hit "Free usage exceeded" with unclear terms (#40078); Go subscribers report plan-switching and invite failures (#40107, #40088) — these are trust-eroding at the account level.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-02

## Today's Highlights

The Pi project saw heavy activity around session reliability, with a major PR series addressing stale promise hangs in model catalog refreshes, OAuth token caching with short-lived credentials, and pre-dispatch session persistence barriers. The community is also pushing for better performance on long sessions — keystroke lag scaling with conversation length and session bloating from subagent transcripts are both attracting attention. Multiple provider integrations landed, including Cline, MiniMax video, and a fix for Fireworks connection timeouts.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#6879 — Auto-compaction never triggers after context grows past 100% until provider overflow](https://github.com/earendil-works/pi/issues/6879)** (6 👍, 8 comments) — A 2-hour agentic turn climbed past the compaction threshold and only stopped at the API's 373k token rejection. This is a critical reliability gap for long-running sessions; the author suggests checking after every agent turn. High community agreement.

2. **[#7161 — Anthropic-messages never sends x-client-request-id](https://github.com/earendil-works/pi/issues/7161)** (8 comments) — OpenAI paths send this header for session affinity, but Anthropic doesn't. Proxy operators with multiple Claude accounts can't group conversations into sessions, breaking round-robin setups. A contribution proposal (#7438) already implements the fix.

3. **[#7010 — Normalize optional object tool schemas for OpenAI-compatible providers](https://github.com/earendil-works/pi/issues/7010)** (1 👍, 6 comments) — Tool JSON schemas for optional object parameters aren't normalizing `required`, which breaks OpenAI-compatible gateways expecting stricter schema validation. Important for anyone using custom tooling with alternate providers.

4. **[#7315 — Fireworks requests fail instantly with "Request timed out"](https://github.com/earendil-works/pi/issues/7315)** (4 comments) — Turns fail with zero token usage and empty content before any provider work happens. Auto-retry masks the issue but wastes time. Related PR #7435 addresses the likely cause (Node's 250ms address-family timeout).

5. **[#7048 — Compaction summary persists truncated mid-word when hitting token cap](https://github.com/earendil-works/pi/issues/7048)** (4 comments) — `generateSummary` caps output but only throws on `stopReason === "error"`, not `"length"`. The result is corrupted, mid-word compaction summaries persisted into the session.

6. **[#7385 — Keystroke input lag scales with conversation length](https://github.com/earendil-works/pi/issues/7385)** (3 comments) — 350-520ms per-character latency on sessions with ~160 tool calls. The tool-result-renderer bypasses the Text component render cache, forcing full re-processing of all tool results on every keystroke. Performance-critical for long agentic sessions.

7. **[#7321 — Multi-line paste broken on terminals without bracketed paste (Termux)](https://github.com/earendil-works/pi/issues/7321)** (1 👍, 2 comments) — Every newline in a paste triggers submit instead of inserting the content. Mobile and minimal terminal users are blocked from standard paste workflows.

8. **[#7402 — Bengali text paste + Space key desyncs differential renderer](https://github.com/earendil-works/pi/issues/7402)** (6 comments) — Width overcounting with wide characters causes visual line duplication. The editor state is correct; rendering drifts from the physical cursor. Important for Unicode correctness.

9. **[#7301 — Stalled availability refresh is permanently unrecoverable](https://github.com/earendil-works/pi/issues/7301)** (3 comments) — `forceRefreshAvailability()` chains onto a stuck promise, so the entire model runtime never settles again even after the cause clears. A single transient failure becomes a permanent outage. Fixed by PR #7451.

10. **[#6600 — Pi update --extensions blocks npm scripts with npm 11.16.0](https://github.com/earendil-works/pi/issues/6600)** (4 comments) — npm's new default script-blocking breaks Pi's extension update flow. Ecosystem drift is forcing tooling adjustments.

## Key PR Progress

1. **[#7451 — Bound model catalog refreshes](https://github.com/earendil-works/pi/pull/7451) (OPEN)** — Fixes five issues (#7027, #7113, #7153, #7418, #7443) around hangs when pi.dev is unreachable, including the `/model` command freeze and post-login catalog refresh stalls. Cancellation and queuing added for stale promise handling.

2. **[#7466 — Opt-in pre-dispatch durability barrier](https://github.com/earendil-works/pi/pull/7466) (CLOSED)** — Sessions persist nothing until the first assistant message completes, leaving an ambiguous window where a crash makes it impossible to tell "provider never invoked" from "invoked, billed, output lost." This adds at-most-once guarantees for embedders.

3. **[#7456 — Support short-lived OAuth tokens](https://github.com/earendil-works/pi/pull/7456) (CLOSED)** — Fixes the five-minute lifetime refresh loop (#7457). Refreshes only when less than one minute remains, preventing refresh-on-every-request behavior for providers with short expiry windows.

4. **[#7453 — Add Cline API and ClinePass providers](https://github.com/earendil-works/pi/pull/7453) (CLOSED)** — New usage-billing and flat-rate provider integrations for the Cline gateway via a single `CLINE_API_KEY`. Broadens the provider ecosystem.

5. **[#7441 — Tolerate missing finish_reason on non-empty openai-completions streams](https://github.com/earendil-works/pi/pull/7441) (CLOSED)** — Gateways violating the SSE spec (omitting terminal finish_reason) were killing sessions with `Stream ended without finish_reason`. Now tolerated for non-empty streams.

6. **[#7440 — Add switchable terminal renderers](https://github.com/earendil-works/pi/pull/7440) (OPEN)** — Allows coding-agent UI modes to switch at runtime while preserving terminal, focus, input, and renderer state. From mitsuhiko; relevant for plugin and multi-mode workflows.

7. **[#7435 — Increase connection attempt timeout](https://github.com/earendil-works/pi/pull/7435) (OPEN)** — Raises Undici's address-family timeout from 250ms to 2s for Pi's connector, preventing false failures on high-latency routes to Fireworks. Regression-tested.

8. **[#7467 — Add MiniMax video generation](https://github.com/earendil-works/pi/pull/7467) (CLOSED)** — New video-generation API registry with MiniMax global and CN providers, including create/query/download handling. Expands beyond text/image modalities.

9. **[#7448 — Add bounded branch entry queries](https://github.com/earendil-works/pi/pull/7448) (CLOSED)** — Consistent traversal bounds and limits across array, JSONL, and SQLite stores, with SQLite branch cache repair. Part of the session storage scalability push.

10. **[#7426 — Make path utilities cross-platform on Windows](https://github.com/earendil-works/pi/pull/7426) (CLOSED)** — POSIX-only path separator assumptions in harness utilities caused `loadSkills` crashes on Windows. Important for Windows adoption.

## Feature Request Trends

- **Session reloadability**: Pre-dispatch durability, bounded branch queries, and post-crash session reconstruction are all active areas — the community wants robust crash recovery and auditability.
- **Provider flexibility**: Requests for per-provider concurrency limits (#7460), compaction on a different model (#7447), and more gateway integrations (Cline, MiniMax) indicate users are running heterogeneous model stacks.
- **Performance at scale**: Keystroke lag on long sessions (#7385), session bloat from subagent transcripts (#7452), and SQLite caching scalability are pushing the project toward larger, longer-lived sessions.
- **Rendering robustness**: Unicode width handling (#7402), scroll lock (#4679), and iTerm2/xterm image compatibility (#7465) show polish is important as the TUI matures.

## Developer Pain Points

- **Hangs and stale promises**: The recurring theme this week — model catalog refresh hangs (#7443, #7418), availability refresh unrecoverability (#7301), and hard-coded 30s RPC timeouts (#7446) — points to systemic resilience gaps around network failures.
- **Provider-specific workarounds**: The Fireworks timeout (#7315), missing x-client-request-id on Anthropic (#7161), and OAuth expiry refresh loops (#7457) reflect pain from real-world provider quirks.
- **Compaction reliability**: Both #6879 (never triggers early enough) and #7048 (truncates mid-word) highlight that compaction — critical for long sessions — is fragile.
- **Context bloat**: Subagent transcripts saved into parent sessions (#7452) cause JSONL files to balloon and can hang sessions entirely. Storage hygiene is becoming a real concern.
- **Ecosystem breakage**: npm 11.16.0 breaking extension updates (#6600) shows downstream dependency changes are a recurring operational headache.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-02

## Today's Highlights

Qwen Code shipped **v0.21.3** with significant upgrades to the `/review` command, adding test plan validation, measured failure attribution, and new verification lenses. On the CI front, the team introduced an intelligent core review router to replace blanket CODEOWNERS assignments, and a new `qwen review drive` subcommand promises to make build-and-drive verification a first-class workflow. Several high-impact PRs target prompt-cache reuse during chat compression, deterministic E2E testing via fake servers, and GitHub channel restart-safety for inbound tasks.

## Releases

- **v0.21.3** — Enhanced `/review` command with test plan validation, measured failure attribution, and new verification lenses. ([#8215](https://github.com/QwenLM/qwen-code/pull/8215), [#8218](https://github.com/QwenLM/qwen-code/pull/8218))
- **v0.21.3-nightly.20260802.184365390** — Complete TUI keyboard shortcut reference docs; fix for history pagination on `o`.

## Hot Issues

1. [#176 — Tool calling does not work with local model qwen3-30b-a3b (23 comments, 7 👍, CLOSED)](https://github.com/QwenLM/qwen-code/issues/176) — A long-running pain point: local models respond with tool calls that never execute, with no visible errors. High community engagement suggests this is a top adoption blocker for local-model users.

2. [#8286 — Support explicitly trusted private ASR base URLs (OPEN)](https://github.com/QwenLM/qwen-code/issues/8286) — Voice feature request for enterprise/managed deployments needing HTTP/internal ASR endpoints. A companion PR is already up (#8350), showing active maintainer interest.

3. [#8131 — Statusline text cannot be selected in Virtualized History mode (OPEN)](https://github.com/QwenLM/qwen-code/issues/8131) — UI/UX regression on macOS where statusline text selection breaks in Virtualized History mode, disrupting copy-paste workflows.

4. [#8279 — Could chat compression reuse the main prompt-cache prefix via a fork? (OPEN)](https://github.com/QwenLM/qwen-code/issues/8279) — A design discussion (no implementation requested) to validate whether compression could leverage the session's existing prompt cache. Directly addressed by PR #8339 today.

5. [#8330 — `@` completion tab switching inaccessible in Warp (OPEN)](https://github.com/QwenLM/qwen-code/issues/8330) — Terminal-specific conflict where Ctrl+Tab is hijacked by Warp, making the tabbed completion picker unusable. Highlights growing terminal-ecosystem compatibility concerns.

6. [#4777 — Deferred-tools listing in system prompt busts prompt cache on MCP discovery (OPEN)](https://github.com/QwenLM/qwen-code/issues/4777) — The deferred MCP tools listing is baked into the cached system prompt; every MCP tool reveal invalidates the cache. This is a core performance issue affecting cache hit rates on long sessions.

7. [#8277 — Better Prompt Caching (OPEN)](https://github.com/QwenLM/qwen-code/issues/8277) — A master tracking issue consolidating prompt-cache work across provider adapters, tool discovery, local KV-cache reuse, and telemetry—signaling a roadmap-wide push on context performance.

8. [#8284 — Expose prompt cache hit rate as telemetry (OPEN, 2 comments)](https://github.com/QwenLM/qwen-code/issues/8284) — Feature request to surface cache hit rate as a first-class telemetry signal, aiding cost and latency optimization for heavy users.

9. [#8333 — Main CI failed: E2E cron test (OPEN, autofix/in-progress)](https://github.com/QwenLM/qwen-code/issues/8333) — Bot-reported CI failure on `cli/acp-cron.test.ts`; the autofix pipeline is actively addressing it, demonstrating the project's growing automation maturity.

10. [#8299 — Finish deterministic fake-server migration and add stable merge gate (OPEN)](https://github.com/QwenLM/qwen-code/issues/8299) — Continuation of test-pyramid work to eliminate flaky post-merge E2E failures by using `fake-openai-server` for SDK/CLI behaviors.

## Key PR Progress

1. [#8346 — Teach the verifier the falsify-not-verify asymmetry](https://github.com/QwenLM/qwen-code/pull/8346) — Adds a rule block so the `/review` verifier stops rejecting findings on "I could not verify it" grounds, distinguishing absence of evidence from evidence of absence.

2. [#8349 — `qwen review drive`: readiness polled, completion proven, cleanup guaranteed](https://github.com/QwenLM/qwen-code/pull/8349) — New subcommand that waits for services to be truly ready, drives them, and captures outcomes as facts—replacing sleep-based guesses for build-and-drive verification.

3. [#8347 — Intelligent core review router + expand code owner pool](https://github.com/QwenLM/qwen-code/pull/8347) — Replaces blanket CODEOWNERS auto-assign with a workflow that routes review requests to 0–2 maintainers based on diff size and round-robin rotation.

4. [#8339 — Reuse prompt cache during chat compression](https://github.com/QwenLM/qwen-code/pull/8339) — Chat compression now reuses the main conversation's prompt-cache prefix when the compression model matches the main model, preserving system instructions and tool definitions.

5. [#8302 — Make permission-control E2E deterministic with fake OpenAI responses](https://github.com/QwenLM/qwen-code/pull/8302) — Replaces model-selected tool behavior with scripted fake responses while keeping SDK, CLI, and permission controller in the test path—reducing flakiness.

6. [#8306 — Recover interrupted inbound tasks on the GitHub channel](https://github.com/QwenLM/qwen-code/pull/8306) — Makes GitHub channel inbound work restart-safe: persisted before dispatch, recovered before next poll, and completed responses retried without re-running the agent.

7. [#8344 — Redact sibling directives from forked subagent history](https://github.com/QwenLM/qwen-code/pull/8344) — Stops a forked subagent from seeing other forks' directives launched in the same turn, fixing a cross-contamination privacy bug.

8. [#8305 — Render inline terminal images in interactive CLI](https://github.com/QwenLM/qwen-code/pull/8305) — Extends terminal-image infrastructure from file previews to model/tool `inlineData`, preserving ordered text/image parts.

9. [#8341 — Make sub-session concurrency caps configurable](https://github.com/QwenLM/qwen-code/pull/8341) — Adds `serve.maxConcurrentSubSessionsPerCaller` and `...Total` settings, raising defaults from 5→16 and 20→24 respectively.

10. [#8343 — Auto-update ECS runners on stable publish](https://github.com/QwenLM/qwen-code/pull/8343) — Emits a `repository_dispatch` after stable publish so self-hosted CI runners stay current and avoid silent downgrades.

## Feature Request Trends

- **Prompt-Cache Optimization**: A clear cluster of requests (#8277, #8279, #8284, #8339) around improving cache hit rates, reusing prefixes, and exposing hit-rate telemetry—indicating user focus on latency and token cost.
- **Voice Input & Private ASR**: Continued demand for CLI voice input (#3110) plus a new request for trusted private ASR base URLs (#8286), driven by enterprise and managed-deployment needs.
- **Deterministic Testing & CI Stability**: Multiple issues and PRs (#8299, #8302, #8333) push toward fake-server migrations and stable merge gates—reflecting community frustration with flaky E2E tests.
- **Extension Ecosystem**: Support for installing extensions directly from the qwen-code repository (#2635) remains an open ask, with community interest in a richer skill/extension marketplace.

## Developer Pain Points

- **Local Model Tool Calling**: Issue #176 (23 comments, 7 👍) captures a major blocker—local models produce tool calls that silently fail to execute, with no diagnostics. This is the highest-traffic open topic.
- **Session & File Visibility**: Users struggle to understand which files were created by which session (#7966), and want clearer sub-agent visibility into reasoning and tool calls (#3758).
- **Terminal & UI Friction**: Recurring complaints include TUI scroll flicker on Linux (#5971), statusline text-selection issues (#8131), and keybinding conflicts with terminal emulators like Warp (#8330).
- **Model Behavior Unpredictability**: Reports of models "getting dumber" over time (#5029) or producing empty responses (`[API Error: Model stream ended with empty response text.]`, #3804) persist, eroding user confidence in long sessions.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-02

*Data sources: Hmbown/DeepSeek-TUI (mirror of Hmbown/CodeWhale)*

---

## Today's Highlights

The project is in the final stretch of the **v0.9.4 release cycle**, with a source candidate PR (#5044) on the release lane carrying release-blocker fixes including an xAI device-login recovery. Maintainers are also burning down a backlog of user-facing fixes across Anthropic wire compatibility, sandbox posture, and session-layer issues in a single batch PR (#5063) — while fresh architectural epics were filed today around multi-worktree ergonomics (#5061) and KV-cache prefix stability (#5059), signaling a focus on reliability and developer efficiency ahead of the next minor.

---

## Releases

No new release tags in the last 24 hours. The **v0.9.4 source candidate** is open as PR #5044 (release lane, reconciled with `main`), with these documented blocker fixes:

- **#5032** — xAI device login: recover from dangling `oauth_credential_generation` pointer (3/3 dogfood fixes passing)
- Additional release-blocker items per the PR description (full changelog expected at ship)

---

## Hot Issues

1. **[#5034 — v0.9.4: switching providers can retain an unrelated default model](https://github.com/Hmbown/CodeWhale/issues/5034)** *(OPEN, release-blocker)*  
   Switching to OpenAI leaves `gpt-5.5` as the default model even when inherited from a different route. Flagged as a release blocker for v0.9.4; provider/model resolution is not updating as one coherent unit.

2. **[#4683 — Wrong deepseek completions URL](https://github.com/Hmbown/CodeWhale/issues/4683)** *(OPEN)*  
   Flaky network failures hitting `https://api.deepseek.com/v1/chat/completions` after long-running asks. Community reports it's intermittent — points to connection handling or timeout issues rather than a hardcoded URL bug.

3. **[#4564 — `codewhale exec --auto`: flags consumed as single arg on Windows](https://github.com/Hmbown/CodeWhale/issues/4564)** *(OPEN)*  
   `--model` and `--toolsets` flags placed before `exec` are concatenated into one argument on Windows with npm global installs. Reporter proposes env-var fallbacks (`CODWHALE_MODEL` / `CODWHALE_TOOLSETS`).

4. **[#4716 — TUI exits immediately on launch (`[Process completed]`)](https://github.com/Hmbown/CodeWhale/issues/4716)** *(OPEN, stop-ship)*  
   Fresh Terminal.app tab on macOS returns immediately to `[Process completed]` when running `codew`. Maintainer-filed; marked stop-ship for the affected candidate version.

5. **[#4682 — Custom provider causes launch failure](https://github.com/Hmbown/CodeWhale/issues/4682)** *(CLOSED)*  
   Setting a custom provider name via `/provider` leads to launch failure on fresh installs. Closed within the burn-down batch, implying the root cause was fixed in #5063.

6. **[#4684 — `danger-full-access` does not disable tools-layer workspace boundary check](https://github.com/Hmbown/CodeWhale/issues/4684)** *(CLOSED)*  
   OS-level sandbox is disabled, but the tools layer (`read_file`, `grep_files`) still enforces workspace boundaries — breaking global skill access. Fixed by the sandbox work in PR #5063.

7. **[#5007 — Youtuber uses Codex instead of CodeWhale as DeepSeek TUI](https://github.com/Hmbown/CodeWhale/issues/5007)** *(CLOSED)*  
   Community visibility discussion: a popular YouTuber demoed DeepSeek-v4-flash using Codex as the TUI. Mild community attention (6 comments) around positioning as the go-to DeepSeek TUI.

8. **[#4085 — Cannot read/write under `~/Library/CloudStorage/Dropbox/` (macOS File Provider)](https://github.com/Hmbown/CodeWhale/issues/4085)** *(CLOSED)*  
   File operations fail in Dropbox-managed directories. Deep-dived: not a sandbox issue (ad-hoc signed, zero entitlements); likely macOS File Provider path resolution. Closed with the v0.9.3 reliability work.

9. **[#5060 — Workflow search hardcodes 16-worker ceiling](https://github.com/Hmbown/CodeWhale/issues/5060)** *(OPEN, filed today)*  
   `WORKFLOW_SEARCH_MAX_CONCURRENT: u16 = 16` is hardcoded instead of reading the Fleet concurrency seam. Asks for the resolved limit in run receipts for operator observability.

10. **[#5062 — Managed sign-in: real device-flow dogfood against CWC staging](https://github.com/Hmbown/CodeWhale/issues/5062)** *(OPEN, filed today)*  
    The xAI login dogfood exposed #5032; maintainers want a recorded PASS/FAIL device-flow login against staging before v0.9.4 ships. Process quality signal.

---

## Key PR Progress

1. **[#5063 — Issue burn-down batch: eight user-facing fixes](https://github.com/Hmbown/CodeWhale/pull/5063)** *(OPEN)*  
   Seven commits, one per fix area: Anthropic wire strictness, sandbox posture, workflow config scoping, session layer, input handling, TUI fixes. Each with regression tests, diagnozed at root-cause level.

2. **[#5044 — Codewhale v0.9.4 source candidate](https://github.com/Hmbown/CodeWhale/pull/5044)** *(OPEN)*  
   Release lane reconciling with `main`. Carries #5032 xAI login recovery and other release blockers; the lane PR all other fixes are stacking onto.

3. **[#5051 — Turn-scoped tool restriction and env-gated sampling overrides](https://github.com/Hmbown/CodeWhale/pull/5051)** *(OPEN)*  
   `StartTurnRequest.allowed_tools` / `disallowed_tools` threaded into the per-turn engine tool gate (deny wins). Makes external benchmark drivers first-class without overlay patches.

4. **[#5025 — Make permission posture live](https://github.com/Hmbown/CodeWhale/pull/5025)** *(CLOSED)*  
   Normalizes runtime compatibility inputs into one `permission_posture` with canonical thread defaults. Auto-Review becomes deterministic; approvals don't open modals.

5. **[#5030 — Correct File edit validation and release clippy gate](https://github.com/Hmbown/CodeWhale/pull/5030)** *(CLOSED)*  
   Validates C/C++ preprocessor conditionals against the complete file before/after `edit_file`; orphaned `#if`/`#endif` fail closed, balanced blocks allowed.

6. **[#5029 — Restore only persisted composer drafts](https://github.com/Hmbown/CodeWhale/pull/5029)** *(CLOSED)*  
   Stops inferring drafts from the final transcript message; restores only from `OfflineQueueState.draft`. Fixes session-resume hallucinating user input.

7. **[#5024 — Trim drifting turn metadata](https://github.com/Hmbown/CodeWhale/pull/5024)** *(CLOSED)*  
   Keeps actionable facts (dates, workspace, permission posture, working set, goals) while removing noisy drift (version, model, mode, cache, rates) from persisted turn metadata.

8. **[#5006 — Preserve long Windows user PATH (installer)](https://github.com/Hmbown/CodeWhale/pull/5006)** *(CLOSED, community)*  
   NSIS `ReadRegStr` returns empty for long registry values; installer replaced the user PATH with only CodeWhale's bin dir. Fixed via proper registry read handling.

9. **[#5008 — Actionable File edit diagnostics and stale-line-number tolerance](https://github.com/Hmbown/CodeWhale/pull/5008)** *(CLOSED, community)*  
   Fixes #5003: model repeatedly failing 100+ line replacements on C files with Chinese comments and CRLF endings — 15+ failed `File` attempts, 3 rollbacks. Improves diagnostics and line-number tolerance.

10. **[#5027 — Make SQLite startup lock-safe](https://github.com/Hmbown/CodeWhale/pull/5027)** *(CLOSED)*  
    Installs the 5-second busy timeout before any schema work, treats WAL as the persistent mode it is (reads current mode, transitions only when necessary). Prevents startup contention failures.

---

## Feature Request Trends

1. **Localization expansion (v0.9.2 wave, largely landed)** — Large push for Korean/Spanish/Brazilian Portuguese (closed), plus new asks for **Hindi (Devanagari shaping)** (#4790), **Ukrainian alongside Russian** (#4791), **French/German/Catalan** (#4788), and **Catalan + Galician/Basque assessment** (#4749). The project treats locales as a first-class matrix with raw-key-parity contracts.

2. **Multi-worktree / parallel-lane ergonomics (new epic, #5061)** — Cross-worktree file-claim visibility, shared build caches, branch-to-PR promotion helpers. Signals mainline developers running multiple lanes who don't want to pay cold-build costs per worktree.

3. **Tool-budget enforcement (continued)** — #4415 (per-turn tool budgets, write-first constraints) closed after evidence of runaway `read_file` calls on GLM-5.2. Expect continued tightening of tool-call governance.

4. **Architecture / code-health debt reduction** — Large refactor wave (#4077 web_search split, #3958 shell split, #3953 runtime_api split, #4083 MCP split, #4174 ToolRegistry reconciliation) is largely closed, indicating a completed v0.9.3 cleanup push.

5. **Cross-provider auto-routing consent flow (#4411, closed)** — `/model auto` can select any provider; shipped design adds a consent flow. Expect providers to gain explicit consent UX.

---

## Developer Pain Points

1. **Provider/model coherence (recurring, release-blocker)** — #5034 shows default model retention across provider switches; #4682 (custom provider launch failure) and #4683 (DeepSeek URL flakiness) are adjacent. Provider-switching state is the #1 correctness complaint right now.

2. **Windows-specific quirks (recurring)** — Flag concatenation with npm global installs (#4564), long PATH overwrite by the installer (#5006), plus the ongoing `danger-full-access` Windows sandbox caveat (#4684) paint a picture of Windows as a second-class citizen on flag parsing and installer paths.

3. **macOS File Provider / cloud storage paths** — #4085 (Dropbox via File Provider) is the second cloud-storage path issue pattern this cycle; users expect TUI file tools to transparently handle virtualized filesystems.

4. **Large-file edit failures (community-verified)** — #5008 documents 15+ failed `File` attempts on a 100+ line C file with Chinese comments and CRLF endings. Editing large, mixed-encoding, CRLF files is a real-world reliability gap being addressed with better diagnostics and stale-line tolerance.

5. **Startup reliability on fresh environments** — Both #4716 (immediate TUI exit on macOS) and #5027 (SQLite startup lock contention) target the same class: "install → run → instant failure with no actionable message." Priority given via stop-ship and release-blocker tags.

6. **Clear CLI/flag semantics** — Windows flag parsing (#4564) plus the `/rc` command that doesn't exist in the runtime (#4936) show recurring friction at the CLI boundary: flags consumed incorrectly, and product copy instructing commands the runtime lacks.

---

*Generated from GitHub data pipeline. All links point to the canonical Hmbown/CodeWhale repository.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*