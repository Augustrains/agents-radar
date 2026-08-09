# AI CLI Tools Community Digest 2026-08-09

> Generated: 2026-08-09 00:43 UTC | Tools covered: 9

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

**Date:** 2026-08-09

---

## 1. Ecosystem Overview

The AI CLI tool landscape is maturing from single-purpose chat interfaces into full agentic development platforms, with communities now scrutinizing reliability, session state management, and multi-agent orchestration as core concerns rather than nice-to-haves. Across all seven tools examined, the dominant themes are: **silent failures** (configuration ignored, subagent status misreported, model fallbacks undisclosed), **session persistence gaps** (memory loss between sessions, unreliable resume semantics), and **Windows platform parity** (a disproportionately high share of filed bugs). The competitive frontier is shifting from raw model capability to operational robustness—how well tools handle long-running sessions, subagent hierarchies, and cross-platform reliability—while feature requests converge on non-interrupting interaction patterns, AST-aware code navigation, and agent-to-agent delegation. Notably, all tools are actively shipping (multiple alpha/beta releases this week), but community trust is being eroded by entitlement confusion, silent config failures, and unreliable agent status reporting.

---

## 2. Activity Comparison

| Tool | Open Issues (active) | PRs (last 24h) | Releases (last 24h) | Notable Signals |
|---|---|---|---|---|
| **Claude Code** | ~10 hot, 1 PR active | 1 (open) | 2 patch (v2.1.225, v2.1.226) | Highest issue engagement (71+ comments); low PR throughput relative to issues |
| **OpenAI Codex** | ~10 hot | 10 (substantive) | 2 alpha (rust-v0.148.0-alpha.4/5) | Highest PR velocity; active feature development on hooks & security |
| **Gemini CLI** | ~10 hot | 10 (4 closed, 6 open) | 1 nightly (v0.56.0) | Strong epic-based planning (AST navigation, evals); key "agent-to-agent" PR open |
| **GitHub Copilot CLI** | ~10 hot (15 of 24 closed) | 0 | None | Massive triage sweep; silent-state bugs dominate; Windows regressions cluster |
| **Kimi CLI** | 2 active threads | 0 | None | Quietest tool; single critical runaway-generation bug; Memory System is sole focus |
| **OpenCode** | ~10 hot | 10 (5 closed, 5 open) | None | Community-driven (all PRs from contributors); gateway bug cluster; long-standing copy/paste regression |
| **Pi** | ~10 hot | 10 (7 closed, 3 open) | None (v0.84.1 current) | Provider reliability is #1 issue (76 comments); specific compaction fixes shipped |
| **Qwen Code** | ~10 hot | 10 (mixed) | 1 (v0.21.8) | Multi-agent orchestration RFCs; autofix pipeline hardening |
| **DeepSeek TUI (CodeWhale)** | ~10 hot | 10 (8 closed, 2 open) | 1 (v0.9.5) | Major refactor (crates/core extraction); runtime API expansion; community provider additions |

---

## 3. Shared Feature Directions

**1. Non-Interrupting / Queue-Based Interaction**
- **Claude Code** (#50246, 184👍): Queue messages during active tasks.
- **DeepSeek TUI** (#5268): Mid-turn control (queue/send-now/Esc-keep-draft).
- **Pi** (#7810): Concurrent compaction rejection (related—prevents double-trigger).
- *Need:* Users want to interact with agent sessions without derailing in-flight work.

**2. Session State Persistence & Resume Fidelity**
- **Claude Code** (#62903 Session Bridge, #81092 memorized commands).
- **Copilot CLI** (#4397 model selection lost on resume, #4329 autopilot state desync).
- **Kimi CLI** (#1283 Memory System, 25 comments).
- **OpenCode** (#31307 concurrent sessions share SQLite state).
- **DeepSeek TUI** (#4416 stale agent state between sessions).
- *Need:* Resume must be a faithful snapshot; memories must persist and be retrievable.

**3. AST-Aware / Precise Code Navigation**
- **Gemini CLI** (#22745, #22746): Epic investigating AST-aware file reads and mapping.
- **DeepSeek TUI** (#5272): Prompt-scoped file recovery from session snapshots.
- **Claude Code**: 1M context misreporting (#81693) hints at context-management pain.
- *Need:* Reduce token noise, precise method-level reads, accurate context accounting.

**4. Agent-to-Agent Delegation**
- **Gemini CLI** (#28738): Subagents calling subagents (open, help-wanted).
- **Qwen Code** (#8718, #8724, #8769): Session-to-session messaging, leader/worker dispatch.
- **DeepSeek TUI** (#4022): Subagent control surfaces outside TUI.
- **OpenCode** (#31307): Session isolation vs. sharing—correctness of concurrency.
- *Need:* Hierarchical agent models with transparent status and permission boundaries.

**5. Windows Platform Parity**
- **Claude Code**: GPU crashes (#81698), .mcpb install failures (#84199), Defender EBUSY.
- **Codex**: Computer Use failures (#37180, #37383), TUI repaint bugs, mouse stutter (#33074).
- **Copilot CLI**: 5 of 10 hot issues are Windows-specific (#4285, #4222, #4299, #4401, #4399).
- **Gemini CLI**: Wayland browser subagent failures (#21983), macOS Seatbelt EACCES (#28734).
- *Need:* Non-Linux platforms must not be second-class.

**6. Security & Guardrail Transparency**
- **Claude Code**: Cyber-safeguard false positives (#83436), model switches without consent (#60093).
- **Codex**: Step environments for Guardian approvals (#37618), cyber-model prefix filtering (#37516).
- **Gemini CLI**: Deterministic redaction before model context (#26525), destructive-command prevention (#22672).
- **Copilot CLI**: `allowed_directories` silently ignored (#4398).
- **DeepSeek TUI**: Unknown model ID silent context fallback (#5244).
- *Need:* Explicit, predictable guardrail behavior; no silent config ignoring.

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach | Differentiator |
|---|---|---|---|---|
| **Claude Code** | Production-grade agentic coding with enterprise trust | Professional devs in large orgs | Tight Anthropic model integration, gateway support, MCP ecosystem | Model routing transparency is a liability; strongest community engagement per issue |
| **OpenAI Codex** | Secure, sandboxed agent execution with hooks | Enterprise & security-conscious devs | Rust-based; extensive hook lifecycle; step environments; workload identity | Best PR velocity; security posture is mature (env stripping, process-tree termination) |
| **Gemini CLI** | Google ecosystem integration + agent hierarchies | Developers in Google Cloud / Vertex environments | Nightly releases; epic-driven roadmap (evals, AST tools); OpenAI-compatible auth being explored | Most structured roadmap; agent-to-agent delegation PR is architecturally significant |
| **Copilot CLI** | GitHub-native workflows with AGENTS.md interop | GitHub-centric developers | Close GitHub integration, skills system, permissions.config | Silent state-desync bugs are eroding trust; triage velocity is high but regressions persist |
| **Kimi CLI** | Minimal, focused CLI with Moonshot models | Developers wanting simple, fast assistant | Lightweight; no releases this week | Quietest community; Memory System is sole roadmap driver; runaway generation is critical |
| **OpenCode** | Plugin-extensible, community-driven TUI | Power users, plugin authors | Bun-based; plugin SDK v2; TUI-first | Most community-contributed code; SDK v2 and region-based slots are strong architecture moves |
| **Pi** | Multi-provider TUI with extension system | Developers wanting provider freedom | Provider API diversity, extension SDK, telemetry-aware streaming | Broadest provider support (Bedrock, DeepSeek, openai-codex); community votes on issues are meaningful |
| **Qwen Code** | Multi-agent orchestration + CI/CD autofix | DevOps / CI-centric teams | Web Shell convergence, workflow engine, autofix pipeline | Most operational (autofix, spam blocklist, replay journals); browser control via WebBridge |
| **DeepSeek TUI (CodeWhale)** | Single-binary, multi-provider agentic TUI | Performance-conscious devs | Rust monolith → crates/core extraction; runtime HTTP API | 682K-line crate being modularized; runtime API (goal/memory/skill endpoints) is unique; community provider contributions |

**Key Differentiation Observations:**

- **OpenAI Codex** is the most *engineering-focused* (hooks, environments, security); **Google Gemini** is the most *strategic* (epics, evals); **Qwen** is the most *operational* (CI/CD, autofix); **Claude Code** is the most *community-driven* (highest issue engagement, but low PR throughput).
- **Windows parity is a universal weakness** except in **Qwen Code** which shows no Windows-specific bugs—likely due to Linux/CI-centric users.
- **Kimi CLI** and **Copilot CLI** are the least differentiated on roadmap; **Pi** and **DeepSeek TUI** are most similar in architecture (TUI + provider diversity + extension systems).

---

## 5. Community Momentum & Maturity

| Tool | Community Energy | Release Cadence | Backlog Health | Maturity Signal |
|---|---|---|---|---|
| **Claude Code** | ★★★★★ (184👍 queue mode; 71-comment Fable issue) | Stable patches | Low PR throughput; high issue volume | Longest-running; feature requests are sophisticated (queue mode, remote control) |
| **OpenAI Codex** | ★★★★☆ (substantive PRs from copyberry[bot]; focused issues) | Rapid alpha cadence | Healthy; PRs outpace issues | Maturing fast on architecture (workload identity, gRPC services); needs Windows work |
| **Gemini CLI** | ★★★★☆ (epic-based community input; help-wanted PR) | Nightly + planned | Structured; P1/P2 labels; evals framework | Most *planned* roadmap; agent-to-agent is the frontier |
| **Copilot CLI** | ★★★☆☆ (triage sweep shows activity but few deep threads) | None this week | Mixed; many closed, but regressions ("was fixed") erode confidence | Community frustration is highest relative to activity |
| **Kimi CLI** | ★★☆☆☆ (only 2 active threads) | None | Quiet; no contributor momentum | Least mature; critical reliability bug (#2597) may be a trust crisis |
| **OpenCode** | ★★★★☆ (contributors landed 10 PRs) | None this week | High contributor velocity; long-standing bugs persist | Most community-driven; SDK v2 and plugin slots will compound momentum |
| **Pi** | ★★★★☆ (76-comment issue; community votes matter) | Steady patches (0.84.x) | Active maintainer response (compaction fixes landed) | Mature ecosystem; provider breadth is community-supported |
| **Qwen Code** | ★★★☆☆ (feature requests are operational, not glamorous) | Weekly stable + nightly | Mixed; CI flakiness noted | Operationally mature (autofix, spam control); multi-agent RFCs signal ambition |
| **DeepSeek TUI** | ★★★★☆ (first-time contributors adding providers) | Monthly-ish stable + nightly | Healthy; refactor planned; 464 dead-code attributes need sweep | Rebranding to CodeWhale; monolith split will unlock velocity |

**Top-Line:**

- **Most active:** OpenAI Codex (PRs), Claude Code (issues), DeepSeek TUI (contributor PRs).
- **Most strategically guided:** Gemini CLI (epics/evals).
- **Most at-risk for community churn:** Copilot CLI (regressions), Kimi CLI (quiet + critical bug).
- **Most architecturally ambitious:** DeepSeek TUI (crates/core + runtime API), Gemini (agent-to-agent), OpenCode (SDK v2 + regions).

---

## 6. Trend Signals

**1. Operational Reliability > Model Capability.** Across all tools, the top complaints are about *how* the tool behaves (silent failures, hangs, stale state, false status), not *which* model is under the hood. Developers are past "wow" and into "I need to trust this in CI." **Watch for:** deterministic replay journals (Qwen #8735), step-context correctness (Codex #37641), and termination guarantees (Codex #37527).

**2. Multi-Agent Is the Next Battleground.** Gemini's agent-to-agent PR, Qwen's session messaging RFC, and Claude Code's queue-mode all point to the same direction: agents coordinating with other agents (and users) in a structured way. Subagent status transparency (Gemini #22323, Codex #37563, DeepSeek #4416) is the #1 trust problem in this space.

**3. Security Is Moving from "Guardrail" to "Predicate."** Codex's workload-identity token exchange (#37610) and env-stripping (#37607), Gemini's redaction-before-context (#26525), and Qwen's read-only classifier bypass fixes (#8590) all signal security is becoming *enforced*, not advisory. Misconfigurations (Copilot's `allowed_directories`) are security bugs, not UX issues.

**4. Configuration Must Be Honest.** The single most-repeated complaint across tools: *silent no-ops*. `allowed_directories` ignored, `dynamicCommandTranslation` non-functional, `.env` not ignored, model IDs silently falling back. Developers want explicit errors, not implicit behavior. **Signal:** Tools that add config validation warnings (Pi #7829, DeepSeek #5244) will build more trust.

**5. Context Is Becoming a First-Class Resource.** Whether 1M-token Claude Opus 5 misreporting (Claude Code #81693), Pi's compaction late-triggering (#6879), or Gemini's AST-aware reads, the industry is converging on: **context windows are finite, expensive, and need explicit management**. Expect more features around compaction triggers, token accounting, and context-preserving resume.

**6. Windows Parity Is Now a Competitive Moat.** Five of ten hot issues on Copilot CLI, four on Claude Code, three on Codex—Windows is where users churn. Tools that ship Windows-stable builds (Qwen appears immune, possibly due to user base) will capture developer mindshare from teams that standardize on Windows workstations.

**7. The "Extractor" Pattern Is Emerging.** DeepSeek TUI's 682K-line monolith split, OpenCode's SDK v2, and Gemini's `crates/core` extraction all reflect the same realization: **the engine must be UI-independent**. Cloud apps, remote workspaces, desktop companions, and CI runners all need the same core, exposed via APIs (DeepSeek's runtime endpoints and Codex's gRPC host service are the clearest examples).

---

**Bottom Line for Decision-Makers:**

- If you need **enterprise trust + model transparency**: Watch Claude Code's billing/entitlement fixes and Windows stability before committing.
- If you need **security-hardened automation**: OpenAI Codex is the most advanced (hooks, environments, token exchange).
- If you want **community-driven innovation**: OpenCode and DeepSeek TUI are where contributors are landing the most substantive code.
- If you want **a strategic roadmap**: Gemini CLI's epic-based planning (AST, evals) is the clearest vision.
- If you're on **Windows or macOS**: Expect friction everywhere except Qwen Code; budget for workarounds.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-08-09 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The most-discussed Skills in the repository, ranked by community attention:

**#1 — Skill-Creator Fixes (Multiple PRs: #1298, #1099, #1050, #1323, #1261)**
- **Functionality:** A suite of critical bug fixes targeting `run_eval.py`, `run_loop.py`, and `improve_description.py` — the scripts that auto-optimize Skill descriptions. The core issue (#556, 10+ independent reproductions) is that the evaluation loop reports *recall=0%* on every query, making the entire description-optimization pipeline optimize against noise.
- **Discussion Highlights:** The trigger-detection logic misses real skill names; Windows subprocess handling crashes (`WinError 10038`, `WinError 2`); synthetic command files leak into the user's live project `.claude/commands/` during parallel evals.
- **Status:** All OPEN. See [PR #1298](https://github.com/anthropics/skills/pull/1298), [PR #1099](https://github.com/anthropics/skills/pull/1099), [PR #1050](https://github.com/anthropics/skills/pull/1050), [PR #1323](https://github.com/anthropics/skills/pull/1323), [PR #1261](https://github.com/anthropics/skills/pull/1261)

**#2 — document-typography** ([PR #514](https://github.com/anthropics/skills/pull/514))
- **Functionality:** Typographic quality control for generated documents — prevents orphan word wrap (1–6 words spilling to next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment.
- **Discussion Highlights:** Addresses pervasive quality issues in AI-generated documents; users rarely request good typography explicitly, making this a silent quality differentiator.
- **Status:** OPEN, created 2026-03-04.

**#3 — PDF Case-Sensitivity Fix** ([PR #538](https://github.com/anthropics/skills/pull/538))
- **Functionality:** Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` (`REFERENCE.md` → `reference.md`, `FORMS.md` → `forms.md`). Breaks on case-sensitive filesystems (Linux/macOS).
- **Discussion Highlights:** Highlights the broader problem of cross-platform consistency in shipped Skills.
- **Status:** OPEN, created 2026-03-06.

**#4 — ODT Skill** ([PR #486](https://github.com/anthropics/skills/pull/486))
- **Functionality:** OpenDocument Text creation, template filling, and ODT→HTML parsing. Triggers on any mention of ODT, ODS, ODF, OpenDocument, or LibreOffice.
- **Discussion Highlights:** Extends the document-format coverage beyond DOCX/PDF; demand for open-source/ISO-standard formats.
- **Status:** OPEN, created 2026-03-01.

**#5 — Frontend-Design Clarity** ([PR #210](https://github.com/anthropics/skills/pull/210))
- **Functionality:** Revision of the frontend-design Skill to improve clarity, actionability, and internal coherence — ensuring every instruction is executable within a single conversation.
- **Discussion Highlights:** Reflects community demand for Skills that are operational directives, not educational prose (echoes Issue #202, which criticizes `skill-creator` for being "developer documentation").
- **Status:** OPEN, created 2026-01-05.

**#6 — Skill-Quality/Security Analyzers** ([PR #83](https://github.com/anthropics/skills/pull/83))
- **Functionality:** Two meta-skills: `skill-quality-analyzer` (evaluates across 5 dimensions: structure, documentation, examples, resources) and `skill-security-analyzer` (trust-boundary auditing).
- **Discussion Highlights:** Directly responds to the #1 community concern — security of community-submitted Skills (see Issue #492 below).
- **Status:** OPEN, created 2025-11-06.

---

## 2. Community Demand Trends

**Highest-signal demands from Issues:**

| Trend | Signal | Representative Issues |
|---|---|---|
| **Security & Trust Boundary** | Critical | [#492](https://github.com/anthropics/skills/issues/492) — 43 comments: community skills under `anthropic/` namespace impersonate official skills, enabling privilege escalation. |
| **Org-Wide Skill Sharing** | Strong | [#228](https://github.com/anthropics/skills/issues/228) — 16 comments, 8 👍: direct sharing/libraries instead of manual `.skill` file downloads and Slack handoffs. |
| **Tooling Reliability** | Strong | [#556](https://github.com/anthropics/skills/issues/556) — 12 comments, 7 👍: `run_eval.py` never triggers skills in headless mode. [#1169](https://github.com/anthropics/skills/issues/1169) — recall=0% even on literal slash-command queries. |
| **Context-Window Efficiency** | Emerging | [#1487](https://github.com/anthropics/skills/issues/1487) — `claude-api` skill injects ~156k tokens in one call. [#202](https://github.com/anthropics/skills/issues/202) — `skill-creator` reads like docs, not an operational skill. |
| **Format Coverage Expansion** | Steady | ODT ([#486](https://github.com/anthropics/skills/pull/486)), typography ([#514](https://github.com/anthropics/skills/pull/514)), pyxel/retro games ([#525](https://github.com/anthropics/skills/pull/525)) — community pushes beyond core DOCX/PDF. |
| **Duplicate Skill Collisions** | Moderate | [#189](https://github.com/anthropics/skills/issues/189) — 6 comments, 9 👍: `document-skills` and `example-skills` plugins install identical content. |

---

## 3. High-Potential Pending Skills

Active PRs not yet merged — likely to land soon:

- **[self-audit](https://github.com/anthropics/skills/pull/1367)** — Mechanical file verification + four-dimension reasoning quality gate before delivery. Universal, model-agnostic. Active comments through 2026-07-02.
- **[color-expert](https://github.com/anthropics/skills/pull/1302)** — Color naming systems (ISCC-NBS, Munsell, RAL, Ridgway), color spaces, and "what to use when" tables. Updated 2026-07-21.
- **[plan-file-hygiene](https://github.com/anthropics/skills/pull/1479)** — Addresses #1417: planning artifacts accumulate with no lifecycle. Active comments through 2026-07-27.
- **[testing-patterns](https://github.com/anthropics/skills/pull/723)** — Full-stack testing: Testing Trophy model, AAA pattern, React Testing Library, edge cases. Active through 2026-04-21.
- **[pyxel (retro games)](https://github.com/anthropics/skills/pull/525)** — MCP server integration for the Pyxel retro game engine; write → run_and_capture → inspect → iterate workflow. Active through 2026-07-15.
- **[SAP-RPT-1-OSS predictor](https://github.com/anthropics/skills/pull/181)** — Tabular foundation model for predictive analytics on SAP business data. Active through 2026-03-16.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, secure, and efficient Skill-authoring toolchain itself** — the top recurring theme is not new Skill functionality but fixing `run_eval.py`/`run_loop.py` so the description-optimization loop produces trustworthy results, coupled with trust-boundary protection against impersonation under the `anthropic/` namespace and context-window discipline to prevent Skills from exhausting Claude's context in a single tool call.

---

# Claude Code Community Digest — 2026-08-09

---

## Today's Highlights

Two patch releases (v2.1.225, v2.1.226) landed this week with gateway spend-limit support and reliability fixes. The community is sharply focused on three fronts: Fable 5 model access issues on Max plans (#79337, 71 comments), the long-running request for a message queue mode (#50246, 184 👍), and recurring Windows desktop app crashes (#81698). Notably, Fable 5 — which became standard on Max plans on July 20 — is being silently downgraded to Opus 4.8 for some users, and this remains the single most active issue in the tracker.

---

## Releases

**v2.1.226** — Bug fixes and reliability improvements. No breaking changes.

**v2.1.225** — Two notable changes:
- **Gateway spend-limit support**: Claude Code's usage warning now recognizes gateway-enforced spend limits. When the limit is reached, the message names the cap, its reset time, and the operator's custom message. Requires gateway on v2.1.225.
- **Workspace trust prompt**: `claude agents` now shows a trust prompt for untrusted directories, matching the behavior of the main CLI.

Release notes: https://github.com/anthropics/claude-code/releases

---

## Hot Issues (10 Notable)

1. **[BUG] Fable 5 prompts 'usage credits required' on Max plan — silently downgrades to Opus 4.8** (#79337)  
   Since Fable 5 became standard on Max plans (2026-07-20), some users are blocked from using it, with an automatic fallback to Opus 4.8. 71 comments, 23 👍. The top issue by engagement — model entitlement logic remains an active pain point.  
   https://github.com/anthropics/claude-code/issues/79337

2. **[Feature] Message queue mode — queue messages instead of interrupting active tasks** (#50246)  
   184 👍 across 50 comments. One of the most upvoted requests in the tracker: users want to queue follow-ups while Claude is mid-task rather than derailing the current work with an interrupt. No maintainer response yet.  
   https://github.com/anthropics/claude-code/issues/50246

3. **[Feature] Remote control for Claude Code sessions in the Claude Desktop App** (#29006)  
   119 👍. Users want to monitor and steer CLI sessions from the desktop app. Trending again after 5 months with no official update.  
   https://github.com/anthropics/claude-code/issues/29006

4. **[BUG] VS Code extension does not use MCP servers at all** (#19054)  
   24 comments. A 7-month-old bug on macOS: MCP servers configured for the CLI are ignored by the VS Code extension. Still open — a notable gap in the editor-integration story.  
   https://github.com/anthropics/claude-code/issues/19054

5. **[BUG] Windows desktop app: GPU process crash kills entire app and all sessions** (#81698)  
   Exit code 101457950 on Windows 11, RTX 5080. A single GPU process failure wipes all running sessions. 15 comments.  
   https://github.com/anthropics/claude-code/issues/81698

6. **[BUG] Claude Opus 5 context window reported as 200k instead of 1M tokens** (#81693)  
   The statusline context gauge saturates and `/compact` appears to do nothing because `context_window_size` is reported as 200,000 for a 1M-context model. Affects usability of the 1M window for users who rely on the gauge.  
   https://github.com/anthropics/claude-code/issues/81693

7. **[BUG] Cyber-safeguard false positives on scientific computing session** (#83436)  
   IR spectrometer calibration is blocked by cyber-safeguards, firing on accumulated context and blocking on both Opus 5 and Opus 4.8. False-positive safety triggers continue to frustrate legitimate workloads.  
   https://github.com/anthropics/claude-code/issues/83436

8. **[BUG] Crash leaves terminal in mouse-tracking mode** (#84029)  
   The restore handler is only registered for graceful exit, so a crash leaves raw escape sequences injected into every mouse movement. A clean diagnostic of a real TUI reliability gap.  
   https://github.com/anthropics/claude-code/issues/84029

9. **[BUG] Local `.mcpb` extension install fails on MSIX build** (#84199)  
   "Private dir leaf redirects (junction/substitute-name plant)" error with no actual reparse point present. Windows packaging issues continue to surface across extensions and plugins.  
   https://github.com/anthropics/claude-code/issues/84199

10. **[Bug] Claude forgets memorized commands and generates incorrect guesses** (#81092)  
    Claude routinely ignores memorized commands (e.g., how to re-request a copilot PR review) and guesses instead of reading memories. Memory retrieval reliability is a recurring theme.  
    https://github.com/anthropics/claude-code/issues/81092

---

## Key PR Progress

Note: Only 1 PR was active in the last 24h, but it's a meaningful one.

1. **[PR #77492] fix(hookify): match Write and prompt rules** (OPEN, updated 2026-08-08)  
   Makes file rules inspect content passed to Write as new text, maps simple prompt rules to the current UserPromptSubmit payload, retains the legacy configured field, and adds regression coverage for Write, Edit, and prompt rules. Root cause: simple rules were inferred as fields absent from the payload. Authored by ShiroKSH; has been open since 2026-07-14.  
   https://github.com/anthropics/claude-code/pull/77492

*No other PRs were updated in the last 24 hours. The repository has a very low PR throughput relative to its issue volume — worth noting for maintainer-activity expectations.*

---

## Feature Request Trends

1. **Non-interrupting interaction** — The message queue mode (#50246, 184 👍) is the single most-requested feature. Users repeatedly ask for ways to interact with Claude without derailing in-flight work.

2. **Desktop ↔ CLI bridge** — Remote control of CLI sessions from the desktop app (#29006, 119 👍). Users want a persistent, visual surface for long-running sessions.

3. **Session continuity** — Session Bridge / structured context preservation for long-running agent sessions (#62903) and memorized-command reliability (#81092) both point at the same need: agents should persist context and behavior reliably across sessions.

4. **Cleaner code hygiene** — New request to keep development history out of code comments/docstrings by default — put it in git, not the file (#85130). Suggests users want Claude to write "final" code, not annotated code.

5. **Per-session plugin/MCP allowlists** — For remote/Cowork runners, users want per-session MCP plugin allowlists to avoid OOM on multi-session machines (#70564).

**Takeaway:** The community is converging on two big themes — *non-blocking interaction* and *session/determinism control*. These are the areas where Anthropic can most differentiate Claude Code from other agentic tools.

---

## Developer Pain Points

1. **Billing/entitlement confusion** — Recurring reports of correct plans being ignored (Fable on Max #79337), paid invoices showing Free plan (#66558, closed), and model switches without disclosure (#60093, closed). These erode trust more than any feature gap.

2. **Windows-specific instability** — GPU process crashes killing all sessions (#81698), kernel BSODs (#80912), EBUSY rename errors from Defender scanning (#67595), and `.mcpb` install failures (#84199). Windows remains the least-polished platform.

3. **Safety false positives on legitimate work** — Cyber-safeguard blocks on scientific computing (#83436) and post-CVP-approval blocks (#84352). High-visibility, low-utility guardrails are actively harming legitimate users.

4. **Terminal/TUI fragility** — Crashes leaving terminals in mouse-tracking mode (#84029), mouse reporting interfering with copy-paste (#68602), and context-window misreporting breaking `/compact` (#81693). These are small but daily-quality-of-life issues.

5. **Memory unreliability** — Claude forgetting memorized commands and guessing instead of reading memory (#81092). For a tool marketed on personalization, unreliability here is disproportionately damaging.

6. **Context/disclosure concerns** — Model switches without consent (#60093) and `usage credits required` on plans that should include the model (#79337) — both closed or trending, but both point to a need for better transparency in the model-routing layer.

---

*Digest generated from public GitHub data for anthropics/claude-code. All links point to the official repository.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-09

## Today's Highlights

Two alpha releases (`rust-v0.148.0-alpha.4` and `rust-v0.148.0-alpha.5`) shipped today with no published changelog details. Meanwhile, the community is actively reporting Windows-specific issues across the board—Computer Use failures, TUI repaint bugs, and SMB workspace problems—while a cluster of PRs from copyberry[bot] landed substantive improvements to hook lifecycle management, async command support, and workload identity token exchange.

---

## Releases

| Version | Notes |
|---|---|
| **rust-v0.148.0-alpha.5** | Alpha release; no detailed changelog published |
| **rust-v0.148.0-alpha.4** | Alpha release; no detailed changelog published |

*Both released within the last 24 hours. Details are sparse; expect more information in subsequent updates.*

---

## Hot Issues

1. **[#32177 — text-log attachment poisons session](https://github.com/openai/codex/issues/32177)** — Attaching a plain-text log in the Codex App triggers "Request blocked" and corrupts subsequent turns. 15 comments, 17 👍. This is a serious UX bug that degrades the entire session rather than just failing the request.

2. **[#21653 — Multi-line status line support](https://github.com/openai/codex/issues/21653)** — Status line truncates when too many items are configured. 13 comments, 59 👍. The highest-voted enhancement request right now; the community clearly wants configurable statusline layout.

3. **[#27284 — SSH remote shows "No chats" despite existing remote threads](https://github.com/openai/codex/issues/27284)** — Inconsistency between the state DB and UI rendering for SSH remote projects. 12 comments, 5 👍. Affects anyone using the app against remote hosts.

4. **[#37180 — Windows Computer Use approval prompt never appears](https://github.com/openai/codex/issues/37180)** — `launch_app` fails with `node_repl exec context not found`. 8 comments, 2 👍. Blocks core functionality on Windows.

5. **[#37383 — Windows Computer Use fails with 0x80070003](https://github.com/openai/codex/issues/37383)** — App/window discovery fails during Computer Use. 8 comments, 4 👍. Second Windows Computer Use issue in a day—reliability here is clearly a pain point.

6. **[#33463 — DeviceCheck token generation unavailable (macOS)](https://github.com/openai/codex/issues/33463)** — New Chat fails after updating to ChatGPT 26.707.72221. 8 comments. Closed and presumably fixed, but notable for the churn it caused.

7. **[#33074 — Windows app causes mouse stutter](https://github.com/openai/codex/issues/33074)** — Launching the desktop app stutters the mouse system-wide without CPU/Disk saturation. 6 comments, 9 👍. High visibility performance issue on Windows.

8. **[#35463 — Subagents drain full week quota overnight](https://github.com/openai/codex/issues/35463)** — Usage counting is broken; subagents burn through quota. 5 comments. Critical for cost control; users watching weekly limits disappear.

9. **[#37563 — Desktop rehydrates closed subagents as "Working"](https://github.com/openai/codex/issues/37563)** — After restart, dead subagents show as live. 4 comments, 2 👍. Confusing UX and potentially misleading state indicators.

10. **[#37418 — "MCP startup interrupted" false positive](https://github.com/openai/codex/issues/37418)** — CLI 0.147.0 reports failures even when all MCP servers initialize fine. 4 comments. Misleading diagnostics damage user trust.

---

## Key PR Progress

1. **[#37641 — Step context for command approval prefix rules](https://github.com/openai/codex/pull/37641)** — Reads `allow_prefix_rules` from the active step context when constructing exec approval requests. Fixes a correctness bug in command approvals.

2. **[#37622 — Include buffered turns when editing prompts](https://github.com/openai/codex/pull/37622)** — Reconstructs buffered turns from notifications so prompt edits find the right message even when it's not yet in the thread's turns.

3. **[#37618 — Step environments for Guardian approval reviews](https://github.com/openai/codex/pull/37618)** — Uses the current step's environment (not the stale turn snapshot) so working directory and permissions are correct.

4. **[#37610 — Workload identity token exchange support](https://github.com/openai/codex/pull/37610)** — New crate for exchanging file-backed JWT assertions for short-lived ChatGPT credentials. Token caching and refresh logic included.

5. **[#37607 — Prevent launch context from reaching child processes](https://github.com/openai/codex/pull/37607)** — Strips `OPENAI_FEDERATION_RULE_ID` and `OPENAI_IDENTITY_TOKEN_FILE` from inheritable env vars for model-reachable children. Good security hygiene.

6. **[#37538 — Expose execution mode in hook listings](https://github.com/openai/codex/pull/37538)** — Adds `executionMode` to `HookMetadata` and propagates sync/async mode through the app-server protocol.

7. **[#37533 — Support asynchronous command hooks](https://github.com/openai/codex/pull/37533)** — Async hooks now run in the background with per-session concurrency limits, instead of being skipped outside `SessionEnd`.

8. **[#37530 — gRPC code-mode host service](https://github.com/openai/codex/pull/37530)** — Exportable, transport-independent implementation of the code-mode gRPC API with leased sessions, execution lifecycle, and tool-call subscriptions.

9. **[#37527 — Terminate timed-out hook process trees](https://github.com/openai/codex/pull/37527)** — Hooks run in process groups (Unix) or job objects (Windows) so timeouts kill the whole tree, not just the parent.

10. **[#37516 — Ignore reusable command approvals for cyber models](https://github.com/openai/codex/pull/37516)** — Filters saved `allow` prefix rules for cyber-specialized models while preserving prompt, forbidden, network, and host-executable policies.

---

## Feature Request Trends

- **Statusline flexibility** ([#21653](https://github.com/openai/codex/issues/21653)): Multi-line support and more layout control for the TUI statusline.
- **Project/sidebar management** ([#26026](https://github.com/openai/codex/issues/26026), [#30230](https://github.com/openai/codex/issues/30230)): Users want to delete or archive sidebar projects explicitly, with clear undo paths and archive/delete differentiation.
- **Strict subagent authority ceilings** ([#36381](https://github.com/openai/codex/issues/36381)): An RFC proposing host-enforced least-privilege preflight checks before subagent delegation.
- **Symmetric text paste in TUI** ([#17103](https://github.com/openai/codex/issues/17103)): Ctrl+V is currently image-only in some contexts; users want text paste support.

---

## Developer Pain Points

- **Windows ecosystem reliability**: Multiple issues for Computer Use (approval prompts, window discovery), SMB/UNC workspaces failing in sandbox modes, app-wide mouse stutter, and extension loading failures. Windows parity remains the most frequently filed complaint cluster.
- **Subagent/turn state inconsistency**: Rehydrated "Working" subagents after restart ([#37563](https://github.com/openai/codex/issues/37563)), simultaneously active turns via remote control ([#34767](https://github.com/openai/codex/issues/34767)), delegation delivered but reported as failed ([#29886](https://github.com/openai/codex/issues/29886)).
- **Quota/usage accounting**: Subagents draining weekly quotas ([#35463](https://github.com/openai/codex/issues/35463)) and unexplained usage drops ([#37532](https://github.com/openai/codex/issues/37532)) create budgeting anxiety.
- **Sandbox/recursion edge cases**: Relative write rules recursively expanding across turns until process spawn fails with E2BIG ([#33479](https://github.com/openai/codex/issues/33479)).
- **Misleading diagnostics**: False MCP startup interruption ([#37418](https://github.com/openai/codex/issues/37418)) and the text-log "poisoned session" issue ([#32177](https://github.com/openai/codex/issues/32177)) erode trust in the tool's self-reporting.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-09

## Today's Highlights

The Gemini CLI team shipped nightly v0.56.0 with a critical fix reclassifying capacity exhaustion as a terminal error, resolving a class of hangs that have plagued users. Community interest remains heavily concentrated on agent reliability—particularly subagent recovery semantics, generalist agent hangs, and shell command execution deadlocks—alongside a substantial push for AST-aware code navigation and self-orchestrating agents. The standout PR this week enables agents to call other agents, a long-requested capability that could dramatically expand the platform's composability.

## Releases

**v0.56.0-nightly.20260808.gcf22ac7e8** — [Release notes](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260808.gcf22ac7e8)

Key changes:
- **Reclassified capacity exhaustion as a terminal error** ([#28716](https://github.com/google-gemini/gemini-cli/pull/28716)) — prevents infinite retry loops when the API is overloaded, addressing a major source of stuck sessions
- **Updated Firestore schema** for caretaker infrastructure with `error` and `pr_number` fields ([#28467](https://github.com/google-gemini/gemini-cli/pull/28467))

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — *P1, Bug, 12 comments*
   A `codebase_investigator` subagent reports `status: "success"` even when it hit the turn limit before doing any work. This misrepresents failure as success, misleading both users and downstream automation. High community engagement (12 comments) reflects frustration with opaque agent outcomes.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** — *P1, Bug, 8 comments, 8 👍*
   Simple tasks like folder creation hang indefinitely when deferred to the generalist agent. Users report waiting up to an hour before cancelling. The workaround—instructing the model to never use subagents—is a poor mitigation for a headline feature. High 👍 count indicates widespread impact.

3. **[#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** — *P2, Enhancement, 8 comments*
   Proposes letting Gemini 3 models operate as native bash users with POSIX tool chaining while maintaining security through sandboxing and post-execution intent routing. This would align tool design with the model's native strengths; ambitious scope (effort/large) suggests this is a strategic direction rather than a quick fix.

4. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** — *P1, Epic, 7 comments*
   An epic tracking the evolution from 76 behavioral eval tests to a comprehensive component-level evaluation framework across 6 Gemini models. Signals a maturing quality assurance strategy that should reduce regressions like the ones seen in recent releases.

5. **[#22745 — Assess AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** — *P2, Epic, 7 comments*
   Investigates whether AST-aware tools can precisely read method bounds in a single call, reducing token noise from misaligned reads. Paired with [#22746](https://github.com/google-gemini/gemini-cli/issues/22746) which recommends `tilth`/`glyph` as starting points. A promising direction for both cost reduction and accuracy.

6. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — *P2, Bug, 6 comments*
   Anecdotal but persistent: the CLI rarely invokes custom skills or subagents autonomously, even when clearly relevant (e.g., gradle/git skills for build tasks). Users must explicitly force it. This undermines the value proposition of custom agent definitions.

7. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — *P2, Bug, 5 comments*
   Sessions are only marked processed when successfully read; low-signal sessions are repeatedly surfaced to the extraction agent, wasting tokens and compute. A bookkeeping flaw in the memory pipeline that should be a straightforward fix.

8. **[#25166 — Shell command hangs with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — *P1, Bug, 4 comments, 3 👍*
   Simple CLI commands that cannot possibly wait for input hang indefinitely, showing "Awaiting user input" after the command has finished. High severity (P1) with a clear repro path; 3 👍 suggests meaningful user impact.

9. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — *P2, Security, 4 comments*
   Auto Memory sends transcript content to the model before the prompt-based redaction occurs, meaning secrets are already in model context. Also flags excessive logging. A privacy concern for a feature that processes local files; security-focused users will want this tracked closely.

10. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — *P1, Bug, 4 comments*
    Browser subagent completes with "GOAL" termination but fails to actually function on Wayland sessions. Composite with [#22267](https://github.com/google-gemini/gemini-cli/issues/22267) (browser agent ignores settings.json overrides), browser agent reliability is a clear weakness area.

## Key PR Progress

1. **[#28738 — Allow agents to call agents](https://github.com/google-gemini/gemini-cli/pull/28738)** — *Open, size/l, help wanted*
   Lets subagents delegate to other subagents or recurse into themselves via `tools:` frontmatter. Fixes [#22092](https://github.com/google-gemini/gemini-cli/issues/22092). This is the most architecturally significant open PR—it would transform the agent model from a fixed hierarchy to a flexible graph. Large scope and "help wanted" label suggest the maintainers are actively seeking collaboration.

2. **[#28735 — Fix formatTruncatedToolOutput non-positive maxChars](https://github.com/google-gemini/gemini-cli/pull/28735)** — *Open, size/xs*
   Guards against output inflation when `maxChars` is non-positive. Fixes [#28620](https://github.com/google-gemini/gemini-cli/issues/28620). Small but sensible defensive fix for tool output truncation.

3. **[#28736 — Clear OAuth callback timeout on flow completion](https://github.com/google-gemini/gemini-cli/pull/28736)** — *Open, size/s*
   Wraps `resolve`/`reject` in `startCallbackServer` to clear timeouts and close the server gracefully. Fixes [#28652](https://github.com/google-gemini/gemini-cli/issues/28652). Prevents dangling timers after auth, which can keep the process alive unexpectedly.

4. **[#28734 — Handle EACCES in resolveToRealPath](https://github.com/google-gemini/gemini-cli/pull/28734)** — *Open, size/s*
   Prevents a startup crash when macOS Seatbelt sandboxing denies realpath access inside a Git repo. Only handled `ENOENT`, `EISDIR`, `ENAMETOOLONG`, `ENOTDIR` previously. A targeted fix that improves macOS compatibility.

5. **[#28679 — Improve Vertex AI 401 error when using standard API key](https://github.com/google-gemini/gemini-cli/pull/28679)** — *Open, size/s*
   Provides a clear error message when users configure `vertex-ai` auth but only have a standard Gemini API key. Focuses on developer experience for a confusing misconfiguration.

6. **[#28608 — Fall back to stable models when preview 404s](https://github.com/google-gemini/gemini-cli/pull/28608)** — *Open, size/m*
   Fixes [#28600](https://github.com/google-gemini/gemini-cli/issues/28600): with Gemini API key auth, `gemini-3.1-pro-preview` can 404 if the key lacks preview access. Adds a fallback chain to stable models. Prevents auth failures from blocking model selection.

7. **[#28737 — Feat/OpenAI compatible auth](https://github.com/google-gemini/gemini-cli/pull/28737)** — *Closed, size/xl*
   Attempted to add OpenAI-compatible authentication but was closed. Large scope may have been withdrawn for redesign; worth watching for a future iteration given community demand for broader provider compatibility.

8. **[#28526 — Fix IDE companion disposables leak](https://github.com/google-gemini/gemini-cli/pull/28526)** — *Closed, size/s*
   Fixes [#27790](https://github.com/google-gemini/gemini-cli/issues/27790): a stray parenthesis collapsed `context.subscriptions.push(...)` calls into a comma expression, leaking `gemini.diff.accept` and `onDidChangeWorkspaceFolders` disposables. Subtle but real resource leak in the VS Code extension.

9. **[#28619 — Update .gitignore; add .env and .ai files; add unit tests](https://github.com/google-gemini/gemini-cli/pull/28619)** — *Open, size/m*
   Ignores `.env` and `.ai` files. The `.env` addition is critical for preventing accidental secret commits; `.ai` files may be a domain-specific artifact. Adds unit tests to lock in behavior.

10. **[#28732 — Version bump to 0.56.0-nightly](https://github.com/google-gemini/gemini-cli/pull/28732)** — *Open, size/s*
    Automated nightly release bump. Routine but indicates the release pipeline is healthy.

## Feature Request Trends

1. **AST-aware code navigation** — Multiple tracked issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) investigate using AST tools for precise codebase mapping and file reads. The goal is fewer turns, less token noise, and better accuracy. This appears to be an official investigation epic with named tool candidates.

2. **Agent self-architecting** — From "agents calling agents" ([#28738](https://github.com/google-gemini/gemini-cli/pull/28738)) to "self-awareness" issues ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)) asking the CLI to know its own flags and mechanics, there is a clear push toward more autonomous, self-orchestrating agent hierarchies.

3. **Subagent transparency** — Multiple requests for subagent trajectory visibility ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)) and bug reporting that includes subagent context ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763)). Users want to see what subagents are doing, both for debugging and for trust.

4. **Destructive behavior prevention** — Issues asking the agent to discourage or prevent destructive git operations and forced commands ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)). Users want safer defaults when the model handles complex operations.

5. **Zero-dependency OS sandboxing** — The proposal in [#19873](https://github.com/google-gemini/gemini-cli/issues/19873) to let models use native POSIX tools with sandboxing instead of abstracted tools. This is a bold architectural proposal with security implications.

## Developer Pain Points

1. **Silent failures in subagents** — Subagents reporting "GOAL" success when they actually hit turn limits ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) undermines trust in the entire agent system. Developers cannot tell if their work was done correctly.

2. **Hanging sessions** — The generalist agent hang ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)) and shell command "Waiting input" deadlock ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)) are major productivity killers. Users routinely wait 30–60 minutes before cancelling.

3. **Unpredictable model behavior** — Creating temp scripts in random directories ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)) and ignoring configured skills ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)) make cleanup and reproducibility difficult. The agent's autonomous choices don't always align with user expectations.

4. **Security and privacy concerns** — Auto Memory's prompt-based redaction happening after content is already in model context ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)) is a legitimate concern for privacy-sensitive users. Similarly, the `.env` ignore gap ([#28619](https://github.com/google-gemini/gemini-cli/pull/28619)) suggests secret management needs more attention.

5. **Subagent permission leaks** — The report that subagents run without permission since v0.33.0 ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)) raises serious questions about the permission model. Users expect their configuration to be the source of truth for what agents can do.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest - 2026-08-09

## Today's Highlights
A wave of triage closures cleared out stale and invalid issues, while a cluster of Windows-specific regressions (rendering freezes, toast crashes, silent exits) remain front and center. Notably, **15 of 24 issues were closed in the last 24 hours**, indicating maintainers are actively sweeping the backlog — but several open bugs around **model selection persistence**, **permissions config loading**, and **Windows terminal rendering** continue to draw developer attention.

## Releases
No new releases in the last 24 hours. The latest tracked version remains **1.0.78** (referenced in open issues #4397, #4401).

## Hot Issues

1. **[#4285 – Silent exit 1 on Windows when log level is set to any canonical value](https://github.com/github/copilot-cli/issues/4285)**  
   *CLOSED* | 👍 2 | *area: platform-windows, configuration*  
   On 1.0.76-1, setting log level to `none`, `error`, `warning`, `info`, or `debug` causes immediate exit with code 1 and zero output — no stderr, no log file. Only `all` and `default` work. High-impact Windows blocker that was closed, presumably fixed in 1.0.77/1.0.78.

2. **[#4222 – Regression: Infinite React/Ink render loop returns on Windows (v1.0.72+)](https://github.com/github/copilot-cli/issues/4222)**  
   *CLOSED* | *area: platform-windows, terminal-rendering*  
   The infamous "Maximum update depth exceeded" freeze from #2802 has regressed. Main pane intermittently freezes on VS Code integrated terminal (native Windows), swallowing output until the process is killed. Community disappointment is palpable given this was previously fixed.

3. **[#4299 – Increasing typing latency over long sessions with background agents](https://github.com/github/copilot-cli/issues/4299)**  
   *CLOSED* | 👍 1 | *area: sessions, input-keyboard*  
   Long-running sessions (especially with background agents) degrade to unusable typing latency. The single most impactful UX complaint in this batch — no workaround identified in-thread.

4. **[#4256 – Add `cache_control` breakpoints to Anthropic requests](https://github.com/github/copilot-cli/issues/4256)**  
   *CLOSED* | 👍 3 | *area: models*  
   Requests to Claude/Anthropic don't set `cache_control` breakpoints, forcing full reprocessing of system prompt and tool definitions on every turn. High-cost inefficiency for heavy users; the 3 👍s signal real demand for prompt-caching parity.

5. **[#4329 – Autopilot not actually enabled when resuming a session](https://github.com/github/copilot-cli/issues/4329)**  
   *CLOSED* | *area: permissions, sessions*  
   Statusline shows autopilot enabled after `/resume`, but approval-gated actions still fail. A silent state-desync bug — the worst kind, since users believe they're in auto-approve mode when they aren't.

6. **[#4397 – Resume session silently switches back to default model](https://github.com/github/copilot-cli/issues/4397)**  
   *OPEN* | *area: sessions, models*  
   Starting with `--model=gpt-5.6-terr...` and then resuming loses the model selection. Related to #4329: session state restoration is clearly fragile. No comments yet, but this affects anyone using model-specific workflows.

7. **[#4398 – `allowed_directories` in permissions.config is never loaded](https://github.com/github/copilot-cli/issues/4398)**  
   *OPEN* | *area: permissions, configuration*  
   Directories listed in `permissions.config` are silently ignored — `/list-dirs` never shows them. Security-relevant config that's dead on arrival; silent failure here is particularly dangerous.

8. **[#4410 – `/agent` pop-up treats `.github\agents\AGENTS.md` as a custom agent](https://github.com/github/copilot-cli/issues/4410)**  
   *OPEN* | *area: tools*  
   Repository guidance file gets misparsed as a custom agent definition, producing malformed-frontmatter errors. Confusing false positive that breaks a documented feature.

9. **[#4401 – Regression: skill tool cannot find valid skills in `~/.agents/skills`](https://github.com/github/copilot-cli/issues/4401)**  
   *OPEN* | *area: platform-windows, tools*  
   Valid `SKILL.md` directories under `~/.agents/skills` are invisible to the `skill` tool. Appears related to #2230 (closed) — possibly an incomplete fix. Affects the skills ecosystem on Windows.

10. **[#4402 – npm shim is a loader, not a version pin — silent version drift](https://github.com/github/copilot-cli/issues/4402)**  
    *OPEN* | *area: installation*  
    Two invocations 101 seconds apart ran **different CLI versions** (1.0.77 then 1.0.78) with zero changes. `--prefer-version` works but is undocumented. Nondeterministic tooling is a reproducibility nightmare for CI and scripting.

## Key PR Progress
No pull requests were updated in the last 24 hours. (0 items in data source)

## Feature Request Trends

1. **Model/session state persistence** — Three issues (#4397, #4329, #4395) orbit the same problem: session resume drops model selection, autopilot state, and quick-delete actions. Users expect `resume` to be a faithful snapshot, not a best-effort approximation.

2. **Config discoverability and honesty** — #4398 (silently ignored `allowed_directories`), #4409 (inert `cli_remote_control_enabled`), and #4402 (undocumented `--prefer-version`) share a theme: **configuration that fails silently or is undocumented**. The community is asking for explicit errors over implicit no-ops.

3. **Windows parity** — #4299 (latency), #4222 (render freeze), #4285 (silent exit), #4399 (PowerShell hook operators), #4401 (skills on Windows) — five of the ten hottest issues are Windows-specific. The Windows experience is clearly the rough edge.

4. **Cross-tool compatibility** — #4399 (`.claude/settings.local.json` hooks on PowerShell) and #4410 (AGENTS.md misparse) show users expect Copilot CLI to interoperate cleanly with the broader agent ecosystem (Claude Code, AGENTS.md spec).

5. **Anthropic cost optimization** — #4256 (`cache_control` breakpoints) is the only performance/cost feature request, but its 3 👍 in a quiet thread suggests real appetite for prompt-caching.

## Developer Pain Points

- **Silent state desync is the #1 frustration.** Whether it's autopilot showing enabled but not working (#4329), `allowed_directories` silently ignored (#4398), or npm serving different versions without warning (#4402), the recurring complaint is: *the tool lies to me until I hit the failure*.

- **Windows is a second-class citizen.** Five of ten hot issues are Windows-specific, and two (#4222, #4285) are regressions of previously-fixed bugs. The community reaction on #4222 is noticeably sharp — "this was fixed in 1.0.31 and it's back" erodes trust in the release process.

- **Session resume is unreliable.** Two separate state-restoration bugs (#4329 autopilot, #4397 model selection) plus a missing feature (#4395 quick delete) paint a picture of sessions as a fragile, half-finished feature.

- **Config failures are invisible.** Whether it's permissions (`allowed_directories`), entitlements (`cli_remote_control_enabled`), or install paths (`--prefer-version`), developers are repeatedly discovering that what they configured isn't what runs — often after wasting significant time.

- **Ecosystem interop is patchy.** The AGENTS.md misparse (#4410) and Claude Code hook breakage on PowerShell (#4399) suggest the team is adopting cross-tool standards without fully testing them on all platforms.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-09

## Today's Highlights
No new releases or pull requests landed in the last 24 hours, but the issue tracker saw active discussion on two fronts: a long-running feature request for a persistent Memory System (#1283) continues to gather community input, while a newly filed critical bug report (#2597) describes a severe runaway generation incident that produced 88k tokens of gibberish in a single LLM step. The contrast highlights the community's dual focus on expanding capability (memory persistence) and hardening reliability (output guards).

## Releases
No new releases published in the last 24 hours.

## Hot Issues

1. **[#2597 — Runaway garbled generation — 88k tokens of gibberish in one LLM step](https://github.com/MoonshotAI/kimi-cli/issues/2597)**
   - *New, critical.* The model ran for ~53 minutes and emitted 88,114 incoherent tokens in a single step. No comments yet, but this is a severe reliability concern that likely deserves immediate maintainer attention — it suggests missing output-length caps or loop-detection guards.

2. **[#1283 — Feature Request: Memory System — Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)**
   - *Open, 25 comments.* The most-discussed open feature. Users want automatic (AI-managed notes) and manual (user-defined instructions) memory to preserve project patterns and preferences across sessions. Community participation indicates strong demand; likely a top roadmap candidate.

3. **[#1283 follow-up — Memory scope and privacy concerns](https://github.com/MoonshotAI/kimi-cli/issues/1283)**
   - Commenters are debating storage location (local vs. cloud), opt-in/opt-out defaults, and how to avoid memory bloat. This sub-discussion is shaping the design direction for the feature.

4. **[#2597 follow-up — Reproducibility questions](https://github.com/MoonshotAI/kimi-cli/issues/2597)**
   - Commenters (if any arrive) will likely ask whether the issue is deterministic, which model/config was used, and whether a `--max-tokens` flag or `interrupt` hotkey was available. Maintainers should pin for a fast response.

5. **[Memory System — Multi-project support](https://github.com/MoonshotAI/kimi-cli/issues/1283)**
   - A sub-thread requesting per-project memory namespaces so context doesn't leak between repositories. Community consensus leans toward directory-scoped memory files.

6. **[Memory System — Conflict resolution](https://github.com/MoonshotAI/kimi-cli/issues/1283)**
   - Discussion on how to handle conflicting memories (e.g., user manually overrides an AI-generated note). Suggestions include explicit "forget" commands and memory versioning.

7. **[Memory System — Manual override priority](https://github.com/MoonshotAI/kimi-cli/issues/1283)**
   - Users want manual memories to take precedence over automatic ones, with clear visual indicators in the CLI showing which memory type is active.

8. **[Memory System — Prompt injection risk assessment](https://github.com/MoonshotAI/kimi-cli/issues/1283)**
   - A commenter raises concern that persistent memory could be poisoned by malicious content in project files. Community calls for sanitization/validation steps before memory is written.

9. **[Memory System — Performance impact on large repos](https://github.com/MoonshotAI/kimi-cli/issues/1283)**
   - Users ask whether memory retrieval will scale on large codebases. Suggestions include embedding-based retrieval or keyword-based indexing to avoid re-reading entire repos.

10. **[Memory System — Integration with IDE extensions](https://github.com/MoonshotAI/kimi-cli/issues/1283)**
    - A request that memory files follow a standard format (e.g., Markdown/YAML) so IDE plugins (VS Code, JetBrains) can render/edit them directly, making memory inspectable and shareable.

## Key PR Progress
No pull requests were updated or merged in the last 24 hours. The only signal is the absence of activity — a quiet day on the development front. However, it is worth noting that the Memory System feature (#1283) has enough community traction that a PR addressing it would likely draw immediate attention and should be prioritized by the maintainers or external contributors.

## Feature Request Trends
The dominant direction is **persistent memory and context management**. The community is asking for:
- Automatic capture of project patterns, user preferences, and decisions across sessions.
- Manual memory via user-defined instruction files.
- Per-project scoping to avoid cross-repo leakage.
- Conflict resolution and manual-override semantics.
- Security hardening against prompt injection via memory poisoning.
- Performance-conscious retrieval for large codebases.

A secondary, emerging concern is **reliability guards** — specifically, capping output token limits and adding loop-detection / early-abort mechanisms to prevent runaway generations like the one in #2597.

## Developer Pain Points
- **Lost context between sessions** (high frequency): Developers repeatedly re-explain project conventions and preferences to Kimi. The Memory System request is the direct symptom.
- **Unbounded generation risk** (new, high severity): The #2597 report describes a catastrophic single-step generation with no apparent kill switch or token cap. Users are likely to expect a `--max-tokens` equivalent and a predictable interrupt path.
- **Lack of transparency in memory behavior** (emerging): Commenters in #1283 want to inspect what the CLI "remembers" and override it; without that visibility, trust in any future memory feature will be low.

---
*Sources: [MoonshotAI/kimi-cli Issues](https://github.com/MoonshotAI/kimi-cli/issues) and [Pull Requests](https://github.com/MoonshotAI/kimi-cli/pulls)*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-09

## 1. Today's Highlights

A cluster of related bugs emerged this week around the **OpenCode Go gateway injecting a leading space into the `deepseek-v4-flash` model name**, causing HTTP 400 errors across multiple clients (Issues #41300, #41306, #41314, #41322). Separately, the community continues to push for **native session goals** (Issue #27167, 128 👍) and a long-standing **copy/paste regression** in the CLI (Issue #13984) remains unresolved after nearly six months. On the code side, contributor `kitlangton` landed a series of TUI and core stability fixes, including **plugin slot regions** and **file mutation permission ordering**.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Hot Issues

**1. [#27167 — [FEATURE]: Add native session goals with /goal](https://github.com/anomalyco/opencode/issues/27167)** — 128 👍, 69 comments
The most-upvoted open feature request. Users want a persistent, first-class session goal/lifecycle mechanism beyond custom slash commands. The long comment thread suggests active design discussion and high community demand.

**2. [#13984 — Can not copy and paste in opencode CLI](https://github.com/anomalyco/opencode/issues/13984)** — 27 👍, 55 comments
A long-standing usability regression (open since February) where the CLI reports "copied to clipboard" but paste yields nothing. The 55-comment thread indicates widespread impact and frustration.

**3. [#33356 — [2.0] Unbounded growth of the `event` table: opencode.db reaches 13GB+](https://github.com/anomalyco/opencode/issues/33356)** — 4 👍, 15 comments
Critical data-integrity issue: the SQLite event-sourcing table is never pruned or compacted, filling disks on long-lived instances. Users report 13 GB databases and 97–99% volume usage. This is a production-blocker for heavy users.

**4. [#14965 — Slow startup](https://github.com/anomalyco/opencode/issues/14965)** — 13 👍, 19 comments
Startup latency regression, notably in Ghostty. The terminal-specific nature suggests a rendering or TTY-detection issue rather than a general performance problem.

**5. [#41300 — Leading space in model name when using opencode-go/deepseek-v4-flash](https://github.com/anomalyco/opencode/issues/41300)** — 1 👍, 4 comments
New bug: the Console Go relay rejects the documented model ID because a leading space is prepended. First of four related reports today (see below).

**6. [#41306 — deepseek-v4-flash still broken on Console Go after #41211](https://github.com/anomalyco/opencode/issues/41306)** — 0 👍, 3 comments
Verification that a previously "closed" fix did not resolve the problem. Root-cause evidence points to the gateway forwarding model names with a leading space.

**7. [#41314 — OpenCode Go relay injects leading space into model string](https://github.com/anomalyco/opencode/issues/41314)** — 0 👍, 2 comments
Independent reproduction of the same gateway bug via direct API call. The upstream relay validator rejects `"model": " deepseek-v4-flash"`.

**8. [#41322 — OpenCode Go rejects documented deepseek-v4-flash ID via direct API call](https://github.com/anomalyco/opencode/issues/41322)** — 1 👍, 2 comments
Fourth report of the same issue, reproduced with plain `curl`. Confirms the bug is server-side in the gateway, not client-side.

**9. [#38993 — [FEATURE]: Add and Remove MCP servers from the TUI dialog](https://github.com/anomalyco/opencode/issues/38993)** — 0 👍, 5 comments
Community wants TUI-native MCP server management. HTTP controls exist (#37712) but the TUI surface is still missing — a UX gap for users who don't want to edit config files.

**10. [#31307 — Multiple opencode instances share the same session via SQLite](https://github.com/anomalyco/opencode/issues/31307)** — 3 👍, 4 comments
Concurrent instances in the same project unexpectedly share sessions, causing cross-talk. A data-isolation bug that can corrupt user intent when running parallel agents.

## 4. Key PR Progress

**1. [#41342 — [contributor] feat(tui): show session branches in vertical tabs](https://github.com/anomalyco/opencode/pull/41342)** — Open
Displays the VCS branch name on each session tab, keeping default branches hidden and using contrasting colors for feature branches. Improves multi-branch workflow visibility.

**2. [#12042 — [contributor] feat(plugin): provide SDK v2](https://github.com/anomalyco/opencode/pull/12042)** — Closed
Long-awaited SDK v2 with a dual-client approach (v1 and v2) for backwards compatibility. Plugin authors can migrate incrementally. Closes #7641.

**3. [#41189 — [contributor] feat(tui): region structure for plugin slot placement](https://github.com/anomalyco/opencode/pull/41189)** — Open
Replaces positional slot names (`prompt.footer.end`) with structured regions that publish a tree of named host parts. Plugins can claim relative placements — a significant architecture improvement for plugin authors.

**4. [#41202 — [contributor] fix(core): authorize file mutations before locking](https://github.com/anomalyco/opencode/pull/41202)** — Open
Fixes a deadlock/ordering issue: permission requests now happen *before* acquiring file-mutation locks. Critical correctness fix for `write`, `edit`, and `patch` flows.

**5. [#41308 — [contributor] fix(tui): align session tab shortcut labels](https://github.com/anomalyco/opencode/pull/41308)** — Closed
Session tab markers now render as real keyboard shortcut labels (1–9, `0` for tab 10, `·` for later tabs) with consistent two-cell gutters.

**6. [#41309 — [contributor] fix(core): flush plugin reload generations](https://github.com/anomalyco/opencode/pull/41309)** — Closed
Fixes `PluginSupervisor.flush` to wait for the current activation generation, including hot reloads, and repairs a regression test deadlock.

**7. [#41310 — [contributor] fix(tui): isolate lifecycle and theme tests](https://github.com/anomalyco/opencode/pull/41310)** — Closed
Stabilizes seven flaky TUI tests (four lifecycle, three theme fallback) that failed on Linux and Windows CI by isolating process-global Bun module mocks.

**8. [#41335 — fix(core): escape literal wildcards and anchor patch insertions](https://github.com/anomalyco/opencode/pull/41335)** — Open
Fixes two bugs from #41333: literal wildcard escaping in the matcher and anchored patch insertion. A correctness fix for file-editing tools.

**9. [#41336 — [needs:issue, needs:compliance] fix(cli): add fish shell completion support](https://github.com/anomalyco/opencode/pull/41336)** — Closed
Proper fish shell completion scripts. Previously `opencode completion fish` emitted bash/zsh syntax — a clear bug for fish users.

**10. [#41307 — [contributor] fix(core): update recorded prompt cache key](https://github.com/anomalyco/opencode/pull/41307)** — Closed
Updates the recorded `SessionRunnerLLM` test cassette to match the new `prompt_cache_key` field being forwarded in requests. Test-infrastructure alignment with the runner change.

## 5. Feature Request Trends

- **Native session goals (🗳️ 128 👍)** — The dominant feature request. Users want persistent session lifecycle management (`/goal`) rather than ad-hoc slash commands. High engagement suggests this could become a flagship 2.0 feature.
- **MCP management in the TUI** — Multiple requests for graphical server add/remove/connect workflows. HTTP endpoints exist; the TUI surface is the gap.
- **Drag-and-drop Office files** — Users want `.docx`/`.xlsx` handling in the chat interface for document-driven workflows.
- **Terminal/desktop parity** — Repeated reports (plugin commands, copy/paste, theme behavior) where Desktop and CLI behave differently. Requests consistently ask for feature equivalence.
- **Session isolation** — Users running parallel instances expect independent sessions; shared SQLite state is seen as a correctness violation.

## 6. Developer Pain Points

- **Gateway/relay validation bugs (today's theme)** — Four separate reports of the same leading-space model-name bug. The root cause is server-side, but the lack of clear error messaging, repeated "fixed" issues (#41211) that aren't, and impact across Hermes, OpenCode Go, and direct curl calls compound the frustration.
- **Data growth and retention** — The 13 GB `event` table issue is a silent production risk. Developers with long-running sessions are discovering disk exhaustion — no warnings, no compaction, no retention policy.
- **Copy/paste regression** — Unresolved for ~6 months. This is a basic workflow blocker that erodes trust in the CLI.
- **Network resilience** — Sessions fail on transient errors (not just `ECONNRESET`); step-cap assistant messages can cause 400s on Claude with thinking enabled — a brittle retry/permission model.
- **Process/resource leaks** — Duplicate MCP server processes, post-hibernation CPU spikes in Bun, and gibberish terminal output on exit all point to lifecycle-management gaps.
- **Cost tracking gaps** — Chinese providers (GLM, DeepSeek, Qwen) show $0.00 spent, breaking budget visibility for a significant user segment.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-09

## Today's Highlights

The community is focused on stability and reliability issues this week: connection drops with `openai-codex` are generating the most discussion (76 comments), and a critical bug where auto-compaction fails to trigger during long agentic turns until the provider overflows has multiple reports. The team is actively addressing the compaction gap — two PRs improving compaction concurrency and trigger timing landed today — alongside a wave of UX polish for the TUI.

## Releases

No new releases in the last 24 hours. Current version: **0.84.1**, with earlier patch fixes (`0.83.0`) still referenced in several open issues.

## Hot Issues

1. **[#4945 — openai-codex Connection Reliability Issues](https://earendil-works/pi/issues/4945)** [inprogress]  
   The most-discussed issue: `openai-codex`/`gpt-5.5` sometimes leaves the TUI stuck on "Working..." with no output, no error, no tool call — only Escape recovers (recording an aborted turn). 76 comments, 31 👍. Maintainers have marked it in-progress; this has been a persistent pain point for nearly three months.

2. **[#6879 — auto-compaction never triggers until provider overflow](https://earendil-works/pi/issues/6879)** [bug]  
   A 2+ hour agentic turn on `gpt-5.6-sol` never triggered compaction; the footer surpassed 100% context and the API rejected at 373k tokens. Compaction only runs after `agent_end`, which never fires during tool loops. 15 comments, 15 👍 — clearly resonating with heavy agent users. Related follow-up: [#7821](https://earendil-works/pi/issues/7821), also closed as untriaged.

3. **[#7836 — Edit fuzzy match misses whitespace-length differences](https://earendil-works/pi/issues/7836)** [untriaged]  
   `normalizeForFuzzyMatch` doesn't collapse whitespace runs or strip leading whitespace, so `oldText` fails even when content is semantically identical. Small models struggle with exact whitespace; this makes the edit tool fragile in practice.

4. **[#7837 — Fullscreen TUI: mouse selection overwrites system clipboard](https://earendil-works/pi/issues/7837)** [untriaged]  
   Dragging to select in fullscreen mode immediately writes to the system clipboard via OSC 52 (target `c`) and flashes "Copied!" — every time, with no opt-out or modifier key. Privacy and accidental-clipboard-clobbering concerns raised.

5. **[#7734 — print mode hangs at exit with subagents](https://earendil-works/pi/issues/7734)** [bug]  
   With 14 extensions loaded, print mode finishes, prints the final answer, then never exits (0% CPU, no open sockets). Reproduced on 0.83.0 and 0.84.0. Non-print mode exits fine.

6. **[#7782 — Invalid Bedrock tool call poisons session](https://earendil-works/pi/issues/7782)** [bug]  
   Pi accepted a Bedrock tool call with an empty key (`""`), persisted it, and replayed it on every turn — permanently bricking the session once Bedrock rejected it. Highlights a missing validation/sanitization layer.

7. **[#7820 — openai-codex stream requests lack retry wrapper](https://earendil-works/pi/issues/7820)** [untriaged]  
   ~30% of long-thinking turns (3–25 min) died from mid-stream transport errors (`WebSocket closed 1006`) with no retry. Non-streaming requests have `retryProviderRequest` wrappers; streaming doesn't.

8. **[#7835 — Edit tool rejects single-object edits argument](https://earendil-works/pi/issues/7835)** [untriaged]  
   Some models wrap arguments as a single object `{oldText, newText}` instead of an array; the edit tool throws when `edits` isn't an array. Arrays recover gracefully; objects hard-fail.

9. **[#7829 — Invalid settings.json silently ignored; misleading 'bash not found'](https://earendil-works/pi/issues/7829)** [untriaged]  
   Unescaped backslashes in a Windows path (`C:\Users\...`) make invalid JSON, which is silently ignored — leading to a confusing "bash not found" error. No warning about the settings parse failure.

10. **[#7816 — Reload reports stale context from in-flight commands](https://earendil-works/pi/issues/7816)** [untriaged]  
    Reloading Pi while an extension command is still running surfaces a stale-context error when that command resumes. Affects extension developers.

## Key PR Progress

1. **[#7610 — Add LLM Gateway and LLM Gateway DevPass providers](https://earendil-works/pi/pulls/7610)** [OPEN]  
   Adds LLM Gateway (OpenRouter-style router) as a built-in `openai-completions` provider, contributed by the LLM Gateway team. Replaces #7480, which auto-closed before its diff was visible.

2. **[#7713 — Stream assistant and config with telemetry](https://earendil-works/pi/pulls/7713)** [OPEN, inprogress]  
   Implements `StreamAssistant` and `StreamAssistantConfig` with `telemetryContext` for harness v2. Foundation work for telemetry-aware streaming.

3. **[#7801 — Lazily load uncommon syntax grammars](https://earendil-works/pi/pulls/7801)** [OPEN]  
   Experimental refactoring of syntax highlighting. Cuts startup time and memory by not loading uncommon grammars eagerly. Notes a minor UI invalidation trade-off. Public API impact is being managed carefully.

4. **[#7810 — Reject concurrent compaction calls](https://earendil-works/pi/pulls/7810)** [CLOSED]  
   Fixes a crash (`Cannot read properties of undefined (reading 'signal')`) triggered by pressing `/compact` twice in quick succession — the shared `AbortController` instance field was being clobbered.

5. **[#7811 — Send max_tokens to native DeepSeek](https://earendil-works/pi/pulls/7811)** [CLOSED]  
   DeepSeek documents `max_tokens`, but Pi was sending `max_completion_tokens` — which DeepSeek silently ignores. Direct API testing confirmed the fix. Sets `maxTokensField` specifically for native DeepSeek.

6. **[#7817 — Treat incomplete reason 'length' as a length stop](https://earendil-works/pi/pulls/7817)** [CLOSED]  
   OpenAI-compatible providers (Doubao/Volcengine Ark) return `incomplete_details.reason = 'length'`; `mapStopReason()` only recognized `'max_output_tokens'`. This normalizes the handling so a length stop isn't misclassified as an error.

7. **[#7807 — Expose low reasoning effort for native DeepSeek V4 Flash](https://earendil-works/pi/pulls/7807)** [OPEN]  
   V4 Flash supports `low` reasoning effort; V4 Pro maps it to `high`. Pi was applying one shared map, silently promoting Flash's `low` to `high`. Adds a Flash-specific map.

8. **[#7834 — Annotate --version with runtime (bun/node/deno)](https://earendil-works/pi/pulls/7834)** [CLOSED]  
   `pi --version` now outputs `0.84.1 (bun)`, etc., so issue reporters and diagnostics can immediately distinguish runtime-specific bugs. Closes #7244.

9. **[#7833 — Change notify extension from agent_end to agent_settled](https://earendil-works/pi/pulls/7833)** [CLOSED]  
   `agent_end` fires after each low-level run — before retries, compacted retries, and queued continuations. Switches the example to `agent_settled` so "Ready for input" notifications don't fire while Pi is still working.

10. **[#7721 — Avoid unwanted newlines when copying in fullscreen](https://earendil-works/pi/pulls/7721)** [CLOSED]  
    In fullscreen TUI, selecting a wrapped line copies each visual row as a separate line, inserting phantom newlines. PR tracks row boundaries so pasted text matches the original content exactly.

## Feature Request Trends

1. **Multiple logins per provider** — [#7814](https://earendil-works/pi/issues/7814) is the most-upvoted feature request in this window: users with two ChatGPT Plus subscriptions (or similar) want concurrent sessions without duplicating the OAuth flow in a custom provider extension.

2. **Configurable TUI scrolling** — Two requests touch the same theme: [#7765](https://earendil-works/pi/issues/7765) (mouse wheel scroll step, hardcoded to 1 line) and [#7830](https://earendil-works/pi/issues/7830) (line-by-line keyboard scroll, `tui.altScreen.lineUp`/`lineDown`). Users want finer-grained reading control in fullscreen mode.

3. **Settings profiles** — [#7813](https://earendil-works/pi/issues/7813) asks for multiple profiles (per-project or via CLI/env) since settings are hardcoded to `~/.pi/agent/settings.json` and `<cwd>/.pi/settings.json`.

4. **Provider breadth** — New providers keep coming: [Meta Model API / Muse Spark](https://earendil-works/pi/issues/7543) and [Cloudflare Workers AI Gateway](https://earendil-works/pi/issues/7838) over the AI binding. The `add-llm-provider` skill makes these "pretty trivial," per one reporter.

5. **Session lifecycle improvements** — [#7818](https://earendil-works/pi/issues/7818) requests deleting the *active* session (currently blocked; only deletable from `/resume` with a different session active).

## Developer Pain Points

- **Provider reliability dominates** — The single most-commented issue of the week is connection reliability with `openai-codex`. Two separate failure modes (stuck TUI on "Working...", 30% mid-stream transport deaths with no retry) make gpt-5.6-sol turns genuinely hard to trust.

- **Compaction is still too late** — Auto-compaction only fires after `agent_end`; long tool loops blow past the threshold and only stop at the provider's hard token limit (373k in one case). The community has filed multiple reports; the maintainers are clearly aware (two related fixes landed today).

- **Tool-call validation is missing** — The Bedrock empty-key issue is a concrete security/correctness gap: invalid tool arguments are persisted and replayed, permanently bricking sessions. Developers want validation/sanitization before execution.

- **Edit tool fragility** — Two distinct issues this week (fuzzy-match whitespace, single-object rejection) show the edit tool remains the weak point for smaller models. Whether it's whitespace normalization or argument shape flexibility, model-generated edits are failing more than they should.

- **Windows and settings ergonomics** — Silently ignored invalid JSON leading to a misleading "bash not found" error is a rough diagnostic path. Users want settings parse failures surfaced clearly rather than swallowed, and they'd like profiles to manage per-project provider/model combinations.

- **Extension lifecycle bugs** — Double-binding on session replacement ([#7831](https://earendil-works/pi/issues/7831)), stale-context errors after reload ([#7816](https://earendil-works/pi/issues/7816)), and print mode hanging with subagents ([#7734](https://earendil-works/pi/issues/7734)) continue to dent the extension ecosystem's polish.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-09

## Today's Highlights
This week's development cycle centers on multi-agent coordination, CI reliability, and expanding the Web Shell into a full desktop experience. A significant security fix restores real-time autofix for fork PRs by bridging review events to credentialed workflows, while the community pushes forward on native session-to-session messaging and workflow-engine orchestration for `/review`. The autofix pipeline continues to mature with deterministic rejection gates and spam blocklist enforcement, signaling a strong operational focus alongside feature growth.

## Releases
**v0.21.8** — Restored real-time autofix support for pull requests opened from forks by bridging review events to credentialed workflows ([#8676](https://github.com/QwenLM/qwen-code/pull/8676)). Enabled compression cache sharing for OpenAI, Gemini, and Vertex AI providers.

**v0.21.7-nightly.20260808.4ec0371e6** — Fixed CI surface for blocked autofix takeover admission ([#8410](https://github.com/QwenLM/qwen-code/pull/8410)) and documented serve sub-session concurrency.

## Hot Issues
1. **[#8092: Build a lower-maintenance desktop app around Web Shell](https://github.com/QwenLM/qwen-code/issues/8092)** — Community desires a desktop experience reusing Web Shell instead of maintaining separate UI. Six comments in a week show strong interest in consolidating the product surface.

2. **[#8724: Cross-session messaging on same machine](https://github.com/QwenLM/qwen-code/issues/8724)** — Proposes `list_agents`/`send_message` primitives with fail-closed gates. Directly complements the RFC for native session coordination.

3. **[#8718: RFC: Native coordination for independent Qwen sessions](https://github.com/QwenLM/qwen-code/issues/8718)** — Leader/worker dispatch pattern with structured result collection. Signals a roadmap shift toward multi-agent orchestration.

4. **[#8737: Chrome 'Allow remote debugging?' consent re-appears every session](https://github.com/QwenLM/qwen-code/issues/8737)** — P2 macOS MCP annoyance with `chrome-devtools` auto-connect; users expect one-time consent persistence.

5. **[#8697: OTEL_METRICS_EXPORTER=otlp silently disables metrics](https://github.com/QwenLM/qwen-code/issues/8697)** — Shared OTel collector environments break native metrics while traces continue. Closed but highlights telemetry config fragility.

6. **[#8758: Auto session titles dominated by UserPromptSubmit hook context](https://github.com/QwenLM/qwen-code/issues/8758)** — Hooks returning large `additionalContext` pollute session titles, degrading searchability.

7. **[#8752: VS Code settings schema rejects supported prompt hooks](https://github.com/QwenLM/qwen-code/issues/8752)** — Schema validation conflicts with runtime capabilities; IDE users cannot configure documented hooks.

8. **[#8750: bare-URL hyperlink swallows CJK punctuation](https://github.com/QwenLM/qwen-code/issues/8750)** — Terminal hyperlinks include trailing full-width punctuation, breaking click targets—common in CJK output.

9. **[#8721: npm test fails due to unknown flag](https://github.com/QwenLM/qwen-code/issues/8721)** — Local development blocked by `npm run test` failure (EUNKNOWN flag), slowing contributor onboarding.

10. **[#8769: Proposal: rebuild /review Step 3–5 on workflow engine](https://github.com/QwenLM/qwen-code/issues/8769)** — Move fan-out, verification, and reverse audit to deterministic workflow code, replacing model-driven orchestration.

## Key PR Progress
1. **[#8762: Stop usage_update frames flooding demo event log](https://github.com/QwenLM/qwen-code/pull/8762)** — Renders live context meter instead of raw JSON; improves `/demo` debuggability.

2. **[#8767: Make spam blocklist enforcement actually work](https://github.com/QwenLM/qwen-code/pull/8767)** — Deletes blocklisted comments and closes PRs outright; replaces ineffective auto-minimize.

3. **[#8735: Make replay journal durable](https://github.com/QwenLM/qwen-code/pull/8735)** — Versioned checkpoint contract with serialized writes; recovery validates committed journal prefix.

4. **[#8590: Close read-only classifier bypasses via line continuation and `${var@P}`](https://github.com/QwenLM/qwen-code/pull/8590)** — Security hardening for shell command classification (#8582).

5. **[#8770: Surface posted review link from /review submit](https://github.com/QwenLM/qwen-code/pull/8770)** — Deterministic `html_url` extraction from Create Review response.

6. **[#8739: Word-wise drag and line-wise extension in VP text selection](https://github.com/QwenLM/qwen-code/pull/8739)** — Implements common editor behaviors for double/triple-click drag in terminal UI.

7. **[#8761: Route workflow label mutations through REST](https://github.com/QwenLM/qwen-code/pull/8761)** — Replaces `gh pr edit` for label changes with `issues/labels` endpoints; adds guard test.

8. **[#8475: Restore deferred MCP tools on resumed sessions](https://github.com/QwenLM/qwen-code/pull/8475)** — Re-reveals deferred tools when declarations refresh; fix for progressive background discovery.

9. **[#8764: Read response body with reader, not for-await](https://github.com/QwenLM/qwen-code/pull/8764)** — Explicit `getReader()` loop with behavioral tests; avoids `Symbol.asyncIterator` pitfalls.

10. **[#8675: Add model-specific reasoning controls](https://github.com/QwenLM/qwen-code/pull/8675)** — Registry for Thinking/Effort controls across Core, ACP, daemon, SDK, WebShell; first registration for `qwen3` models.

## Feature Request Trends
- **Multi-agent coordination** (#8718, #8724, #8769): Session-to-session messaging, leader/worker dispatch, and workflow-engine orchestration are the dominant roadmap direction.
- **Web Shell convergence** (#8092, #8699): Users want Web Shell as the unified UI surface for both desktop apps and browser automation, reducing MCP dependency.
- **Terminal UX refinement** (#8738, #8741, #8750): Text selection gestures, blocked-command clarity, and CJK-aware hyperlink handling show polish focus.
- **Browser integration** (#8699, #8737): Direct browser control via WebBridge and persistent Chrome consent are recurring asks.

## Developer Pain Points
- **CI flakiness**: E2E test failures (#8756, #8766, #8768) stem from unawaited setup and race conditions; autofix pipeline is iterating on deterministic gates (#8765).
- **Configuration validation gaps**: Settings exposed but non-functional (`dynamicCommandTranslation`, #8748) or rejected by schema (#8752) frustrate users.
- **macOS-specific breakage**: Workspace mocks break permission tests (#8753) and Chrome MCP consent re-prompts (#8737) point to platform-sensitive handling.
- **Security edge cases**: Trust folder overrides (#8627) and git config program execution (#8575) are closed but reveal attack surface depth.
- **Test infrastructure neglect**: `integration-tests/` never type-checked (#8692) and vendored source drift (#8722) signal maintenance debt.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-09

## 1. Today's Highlights
The v0.9.5 milestone tracker (#5266) is now active, outlining a substantial refactor agenda that moves the engine into `crates/core` and introduces a series of agent-ready workflow features. A notable new release snapshot (v0.9.5) has been published, consolidating the terminal app into a single compiled runtime with the `codewhale`/`codew` commands. Community contributions are arriving steadily, including a first-class Mistral provider route (#5295) and an automatic prompt-based model selector (#5257), signaling growing community engagement around provider flexibility.

## 2. Releases
- **v0.9.5** — Codewhale 0.9.5 consolidates the terminal app into one compiled runtime while keeping both `codewhale` and `codew` commands. Removes default turn ceilings that interrupted long-work sessions, and aligns updater, installers, release assets, website, and package surfaces around the unified contract. Release assets verified 34/34.
- **v0.9.4** — Updated release notes confirm Codewhale is the public product from Shannon Labs; the legacy npm package `deepseek-tui` is deprecated with no further releases. Users on the v0.8.x legacy `deepseek`/`d` commands should migrate to `codewhale`.

## 3. Hot Issues
1. **[#4022 — CLI/TUI parity for subagent control surfaces](https://github.com/Hmbown/CodeWhale/issues/4022)** — The TUI sidebar became the primary interactive surface for subagent status and cancellation, but these controls must not be trapped inside the TUI if a cloud app or remote workspace is introduced. Fundamentally an architecture question about where control surfaces live.

2. **[#4785 — 464 `#[allow(dead_code)]` attributes hiding drift](https://github.com/Hmbown/CodeWhale/issues/4785)** — A structural code-quality issue: 464 allow attributes across 143 files make the compiler unable to report dead-code drift. Community reaction underscores the need for a systematic sweep to restore compile-time safety.

3. **[#4326 — RSS after cancelling a 32-worker storm](https://github.com/Hmbown/CodeWhale/issues/4326)** — Post-cancellation RSS increased instead of settling in the 32-worker PTY benchmark. The team needs to distinguish allocator high-water retention from a real worker/runtime leak.

4. **[#4416 — Stale failed-agent state between sessions](https://github.com/Hmbown/CodeWhale/issues/4416)** — A second CodeWhale instance in the same workspace renders stale red failed-agent rows from an earlier session, even though the status bar shows zero activity. A data-isolation bug that undermines trust in multi-session workflows.

5. **[#5272 — Prompt-scoped file recovery](https://github.com/Hmbown/CodeWhale/issues/5272)** — Restore workspace files from a prior user prompt's session snapshots, not just transcript scrollback. Must cooperate with git to avoid discarding user commits. Part of the v0.9.5 agent-ready agenda.

6. **[#5270 — Unified tasks surface](https://github.com/Hmbown/CodeWhale/issues/5270)** — One operator-facing list of running background shells, subagents, Fleet/lane workers, and workflow runs. Currently these are fragmented across separate systems; unification is a top v0.9.5 priority.

7. **[#5267 — Turn-stop honesty](https://github.com/Hmbown/CodeWhale/issues/5267)** — Users lose trust when the footer says "ending"/"stopping" but the model keeps talking. Four resume paths need investigation, with a preference for deleting false guards over adding status prose.

8. **[#5244 — Unknown model ids silently degrade to 128K context](https://github.com/Hmbown/CodeWhale/issues/5244)** — When `context_window_for_model` doesn't know a model id, it falls back silently to the legacy 128K default, causing 1M-window models to compact prematurely. Requires explicit surfacing of fallback behavior.

9. **[#5268 — Mid-turn control (queue / send-now / Esc-keep-draft) + named waits](https://github.com/Hmbown/CodeWhale/issues/5268)** — Steering feels like fighting a locked chat bubble. The composer should remain useful while a turn runs, with a crisp contract for queue vs send-now vs cancel-keep-draft.

10. **[#5291 — Clear stale reasoning hints](https://github.com/Hmbown/CodeWhale/issues/5291)** — Reasoning blocks show "Space to expand" after the model has completed its response; a cosmetic but user-visible truthfulness issue in the release candidate.

## 4. Key PR Progress
1. **[#5295 — Mistral AI as first-class provider route](https://github.com/Hmbown/CodeWhale/pull/5295)** — First-time contributor @xavierpestel-ai adds Mistral AI (la Plateforme) with `mistral-code-latest` default, `CODEWHALE_PROVIDER=mistral`, and `--provider mistral` support. Open; a strong sign of community enthusiasm for multi-provider support.

2. **[#5300 — Core owns primary request preparation](https://github.com/Hmbown/CodeWhale/pull/5300)** — Replaces the unused synthetic `ChatRequest` scaffold in `codewhale-core` with production `MessageRequest` DTOs previously owned by the TUI crate, with a pure `prepare_primary_turn_request` constructor. Open; a structural step toward the `crates/core` extraction.

3. **[#5292 — chore(release): prepare v0.9.5](https://github.com/Hmbown/CodeWhale/pull/5292)** — Consolidated the terminal app into one compiled runtime keeping `codewhale`/`codew` commands, removed default turn ceilings, and aligned the updater/installers/assets/website. Merged.

4. **[#5133 — Runtime API: persistent goal-loop state/completion controls](https://github.com/Hmbown/CodeWhale/pull/5133)** — Adds goal resource endpoints: `GET/POST/DELETE /v1/threads/{id}/goal` for reading active-goal state and driving lifecycle transitions. Closed.

5. **[#5132 — Runtime API: verifier receipts and evidence](https://github.com/Hmbown/CodeWhale/pull/5132)** — Exposes durable task receipts, per-task verifier details, and retry metadata beyond the aggregate counter. Three new read-only endpoints under `/v1/fleet/runs/{run_id}/`. Closed.

6. **[#5131 — Runtime API: bounded memory inspection/lifecycle](https://github.com/Hmbown/CodeWhale/pull/5131)** — Memory resource routes: list active memory, view scope/provenance, and apply lifecycle controls, gated behind `require_runtime_token`. Closed.

7. **[#5130 — Runtime API: bounded MCP lifecycle management](https://github.com/Hmbown/CodeWhale/pull/5130)** — Post/put/delete routes for `/v1/apps/mcp/servers` so clients no longer need to edit TOML/JSON directly. Closed.

8. **[#5129 — Runtime API: skill lifecycle endpoints](https://github.com/Hmbown/CodeWhale/pull/5129)** — Install, update, uninstall, trust, and audit routes for skills, all token-protected. Closed.

9. **[#5205 — Stabilize IME candidate positioning in Tabby](https://github.com/Hmbown/CodeWhale/pull/5205)** — Detects `TERM_PROGRAM=Tabby`, enables low-motion rendering and bounded redraw cadence to prevent Chinese IME candidate window drift in rapid TUI redraws. Closed.

10. **[#5257 — Add `model = auto` for prompt-based tier selection](https://github.com/Hmbown/CodeWhale/pull/5257)** — Automatically selects `deepseek-v4-pro` (complex) or `deepseek-v4-flash` (simple) based on the user's prompt. Merged; a community contribution addressing cost/performance trade-offs.

## 5. Feature Request Trends
- **Engine extraction to `crates/core`**: Multiple issues (#5261, #5263, #5300) push for moving the turn loop, session/thread management, and prompt assembly out of the TUI into a shared core crate to enable CLI/TUI/cloud parity.
- **Agent-ready workflow controls**: The v0.9.5 milestone (#5266) bundles prompt-scoped file recovery (#5272), unified tasks surface (#5270), session peek (#5271), durable plan artifacts (#5269), mid-turn control (#5268), and turn-stop honesty (#5267).
- **Provider neutrality and expansion**: Community actively requests new providers (Mistral in #5295), Responses-API dialect profiling (#5092, #5093), and renaming legacy `DeepSeekClient` internals to provider-neutral types (#5103).
- **Runtime API expansion**: Closed PRs demonstrate a strong push for exposing full lifecycle controls (goal, memory, MCP, skills, verifier receipts) via HTTP for managed desktop/web clients.
- **Build-time and monolith reduction**: The 682,959-line `codewhale-tui` crate taxes every edit, commit, and test loop; a dedicated epic (#5249) proposes splitting the monolith.

## 6. Developer Pain Points
- **Turn-stop dishonesty**: The model keeps talking after UI declares "ending"/"stopping" across four resume paths (#5267) — erodes user trust.
- **Stale state across sessions**: Failed-agent rows from prior sessions bleed into fresh workspace instances (#4416), creating confusing noise.
- **Silent context-window degradation**: Unknown model ids quietly fall back to 128K legacy defaults, causing premature compaction of 1M-window models (#5244).
- **Monolith build tax**: The 620-file `codewhale-tui` crate recompiles as one unit; SHA-stamping invalidates tui+cli on every commit; 25 integration-test binaries each require rebuilds (#5249).
- **Dead-code drift**: 464 `#[allow(dead_code)]` attributes hide structural decay; the compiler can't report what's genuinely unused (#4785).
- **Heavy sub-agent ceremony**: Small child agents must produce a rigid "SUMMARY/EVIDENCE/CHANGES/RISKS/BLOCKERS" contract with sentinel tags — more ceremony than value for small tasks (#5189).
- **Unpredictable RSS after cancellation**: Post-cancel memory doesn't settle in high-fanout scenarios, requiring investigation into whether it's allocator retention or a real leak (#4326).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*