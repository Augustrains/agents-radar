# AI CLI Tools Community Digest 2026-08-26

> Generated: 2026-08-26 00:32 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem Cross-Comparison Report
**2026-08-26**

---

## 1. Ecosystem Overview

The AI CLI tool landscape is entering a maturation phase marked by rapid release cadence and platform-expansion pressure. Across all seven tools surveyed, communities are increasingly focused on reliability — silent failures, incorrect success signaling, and state-management bugs dominate issue trackers. Windows remains the weakest platform across every tool, with persistent crash, packaging, and feature-parity gaps. Security hardening is accelerating, particularly around MCP (Model Context Protocol) ecosystems, with multiple tools shipping SSRF prevention, credential sanitization, and auth enforcement in the same 24-hour window. The competitive battleground is shifting from raw capability to trust — developers are demanding predictable behavior, transparent state, and configuration that actually works as displayed.

---

## 2. Activity Comparison

| Tool | Issues Active Today | PRs Active Today | Release Status | Notable Signals |
|------|---------------------|------------------|----------------|-----------------|
| **Claude Code** | 10 hot issues, 2 new | 1 | 2 patches (v2.1.245, v2.1.246) | Message queue feature (199👍); Windows crash cluster |
| **OpenAI Codex** | 10 hot issues | 10 merged | 3 Rust alphas (0.150.0-a.9→a.11) | Linux desktop request (953👍); Windows instability dominant |
| **Gemini CLI** | 10 hot issues | 10 merged | 2 stable (v0.57.0, v0.58.0-preview) | 4 security PRs (SSRF, hardcoded creds, auth); subagent misreporting |
| **Copilot CLI** | 10 hot issues, 3 new | 1 | 1 prerelease (v1.0.81-10) | Plugins dashboard GA; prerelease version-stranding bug |
| **Kimi CLI** | 2 issues, 0 new | 0 | None | Critical silent data-loss bug (Edit/Write no-op) |
| **OpenCode** | 10 hot issues | 10 merged | 1 patch (v1.18.23) | 266GB auto-updater cache leak; endpoint-unavailable cluster |
| **Pi** | 10 hot issues | 10 merged | None (0.84.3 current) | Windows megathread (49 comments); provider drift fixes |
| **Qwen Code** | 10 hot issues | 10 merged | 1 nightly | `/effort max` session-bricking (P1, closed); context mgmt pain |
| **DeepSeek TUI** | 10 hot issues | 10 merged (9 closed) | None (v0.9.12 gating) | Provider neutrality audit (2,281 lines); git index.lock conflicts |

**Summary**: Gemini CLI and OpenCode had the most active PR pipelines; OpenAI Codex shipped the most releases (3 alphas); Claude Code has the highest-engagement feature request; Kimi CLI is effectively static but facing a critical bug.

---

## 3. Shared Feature Directions

**a. Non-Interruptive / Queueable Workflows**
- Claude Code: Message queue mode (#50246, 199👍)
- Qwen Code: Background agent coordination (#8097), loop-detection false positives (#9733)
- DeepSeek TUI: Supervised operation (control socket, lifecycle outbox, /relaunch)
- Copilot CLI: Shareable/resumable sessions

These cluster around one need: **let agents do multi-step work without derailing state**.

**b. Context Window Transparency & Compression Control**
- Qwen Code: Skill lifecycle management (#6762), incorrect compression (#9309), context telemetry (#10015)
- Claude Code: Context-edge autocompact never fires (#77509)
- Pi: Compaction fixes across 5 PRs (reserve scaling, stop-reason handling, tool_choice)
- DeepSeek TUI: Compaction survival contract (#4394)
- Kimi CLI: Context compaction reopens deleted tasks (#2523)

**Shared pain**: Models and tools don't behave well at scale. Users want explicit, verifiable control over what stays in context.

**c. Rule/Hook Enforcement That Respects Boundaries**
- Claude Code: Prompt-topic rules (#87804), drift-based rule violations (#89464)
- OpenAI Codex: Hooks bypassed by `exec`/Code Mode (#23411, #32491)
- Gemini CLI: Skill-scoped hooks, session-persistent vs. scoped
- Copilot CLI: MCP dashboards that look enabled but aren't connected

**Theme**: Static path-based or one-shot rule application is insufficient. Users want stateful, scope-aware enforcement.

**d. Provider Neutrality & BYO-Model Support**
- OpenCode: Cloudflare AI Gateway fixes, new providers (Cerebras, Together)
- Gemini CLI: Provider-neutral gating audit (#5588)
- Pi: Opper provider, DeepSeek vision, Bedrock compatibility
- Copilot CLI: BYOK/local providers in `/model` picker (#3709)
- OpenAI Codex: Subagent orchestration with custom models (#17598)

**e. MCP Reliability and Security**
- Copilot CLI: Token injection regression (#4604), workspace MCP not connecting (#4542)
- Gemini CLI: SSRF prevention, consent enforcement, env injection hardening
- Claude Code: draft-07 outputSchema rejection (#86142)
- OpenAI Codex: Enterprise OAuth identity for MCP (3 PRs)

---

## 4. Differentiation Analysis

| Tool | Core Focus | Target User | Technical Approach |
|------|-----------|-------------|--------------------|
| **Claude Code** | Enterprise safety + permissions | Enterprise orgs, compliance-minded | Path-based rules, `/permissions`, cyber-safeguard verification |
| **OpenAI Codex** | Infrastructure + enterprise identity | Large orgs with bespoke IT | Rust rewrite (alpha line), MCP OAuth enterprise integration |
| **Gemini CLI** | Agent orchestration refactoring | OSS/Google-ecosystem devs | A2A server, subagent redesign, security patches |
| **Copilot CLI** | GitHub-centric UX | Existing GitHub users | Plugins dashboard, desktop app, GitHub MCP interop |
| **Kimi CLI** | Minimal, focused CLI | Cost-sensitive individuals | Slow iteration; 2-issue tracker; no new features |
| **OpenCode** | Performance + gateway flexibility | Power/OSS users | Rust core, provider gateway fixes, auto-updater hardening |
| **Pi** | Streaming quality + provider compat | Stream-focused heavy users | Provider adapters, response schema handling, eager execution, Windows crowd-funding |
| **Qwen Code** | Long-session stability | Enterprise + automation | Session rotation, review pipeline, WebShell as IDE, loop detection |
| **DeepSeek TUI** | Cross-provider neutral Rust TUI | External-image pipeline users | Provider-neutral auditing, sandbox customization, external supervision |

**Key architectural divergence**: **Pi** and **OpenCode** implement heavier client-side provider adapters (tool-call rewrites, image hoisting, deep-link recovery) while **OpenAI Codex** and **Gemini CLI** focus on server/permission-layer abstraction. This reflects a strategic split between "make the tool fly with any model" vs. "define a canonical server contract".

---

## 5. Community Momentum & Maturity

**High Momentum (Rapid Iteration)**
- **OpenCode**: 10 PRs merged in 24h across testing, TUI, session, and provider logic. Release in 2 days (v1.18.x). High contributor activity on patches.
- **Gemini CLI**: 10 merged PRs, 4 security-focused. Reliable 2-release day cadence. Open contributor pipeline.
- **Pi**: 10 PRs merged/closed in 24h. Strong contributors (extensions, providers, eager exec). Active issue triaging.
- **Qwen Code**: 10 PRs merged/closed (WebShell, review pipeline, session management). Nightly builds.
- **DeepSeek TUI**: 9 PRs closed, 1 gated integration branch (72 commits). Contributor-series pipeline, hatching a full crate refactor.

**Moderate Momentum (Stable but Less Deliverables)**
- **Claude Code**: 2 patch releases, 1 PR. High issue volume but slower code turn.
- **OpenAI Codex**: 3 alpha releases but minimal notes; 10 PRs merged (infrastructure-heavy, lower user-visible impact).
- **Copilot CLI**: 1 prerelease, 1 PR active. Plugins dashboard GA is notable but the tracker is comparatively sparse.

**Stagnation / Risk**
- **Kimi CLI**: 0 releases, 0 PRs, only 2 issues (one a critical silent data-loss). Low community engagement and minimal maintainer visibility. **High risk** for current users.

---

## 6. Trend Signals

**Signal 1: Status-fatigue — "The agent says done when it isn't"**
Subagent success misreporting (Gemini #22323), Kimi's false write-success (#2617), Qwen's loop-detection false-positive kills (#9733), and Claude's drift-based rule violations (#89464) all point toward a single, deep problem: **the agent's own self-reporting of state and success is not to be trusted.** Expect a wave of tooling around outcome/observability contracts — LLM-generated completion signals will need verification layers (filesystem checks, event-based confirmations, cross-validation).

**Signal 2: Context real-estate is the new bottleneck — and users want it governed**
Compaction fixes across 5 tools in one day, context telemetry requests, skill-body lifecycle controls, and drift-based enforcement all read as the same underlying pain: **model context is finite, opaque, and unmanaged.** The next battleground is unlikely to be raw context-window size (100k→1M is already cheap); the differentiator will be "what you can afford to keep" — compression, scoping, budgeting, and eviction policies.

**Signal 3: Windows is the credibility test no one is passing**
Windows issues dominate every major tool's tracker — Crash on startup, MSIX packaging, PATH breakage, sandbox misbehavior, GPU process crashes, file-lock errors, PowerShell version mismatch, worktree archiving failures. No tool has cracked it. For AI coding tools to become the default for enterprise (where Windows is still the standard desktop), this must be fixed — **expect a "Windows excellence" sprint from at least one vendor in the next 2-3 quarters.**

**Signal 4: MCP is moving to production — and the sharp edges are showing**
Across Copilot CLI (token injection regression), Gemini CLI (SSRF, consent bypass), Claude Code (draft-07 schema rejection), and OpenAI Codex (enterprise OAuth), the MCP ecosystem is clearly hitting the "trying to wire it into corporate infrastructure" phase. The tools that invest in enterprise-grade MCP security and reliability (rather than developer-facing convenience) will win the procurement-driven deals.

**Signal 5: Provider-neutrality is going from nice-to-have to table-stakes**
With tools increasingly supporting BYO-model, custom gateways, and local providers, vendor lock-in is being actively dismantled at the CLI layer. DeepSeek's audit, Pi's adapter work, and Copilot's BYOK picker demand signal a future where **the CLI is the stable abstraction layer and models are fungible** — which will pressure OpenAI and Anthropic to keep their infrastructure rails (or tooling-specific features) compelling.

**Signal 6: Governance is the missing middle layer**
Sandbox deny-lists (DeepSeek), fleet cost ceilings (#5567), approval receipt persistence (#5584), cyber-safeguard verification (Claude), enterprise MCP OAuth (Codex) — these aren't developer-specific. Something is emerging called **"agent compliance"** — configurable, auditable guardrails that survive long-running, multi-platform, multi-operator workflows. This will likely be an adoption-blocker for regulated industries if not solved.

---

*Data synthesized from public GitHub issue and PR activity across claude-code, openai/codex, gemini-cli, copilot-cli, kimi-cli, opencode, pi, qwen-code, and deepseek-tui repositories for 2026-08-26.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-08-26 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Skills have generated the most community discussion and engagement:

### 1. Skill-Creator Evaluation Fixes (PR #1298, #1099, #1050)
Multiple PRs targeting `run_eval.py` — the evaluation harness for skill descriptions — have dominated discussion. The core issue: the script reports 0% recall across all queries, making the optimization loop "optimize against noise." PR #1298 by MartinCajiao addresses artifact installation, Windows stream reading, and parallel workers. PR #1099 and #1050 fix Windows-specific subprocess crashes. **Status:** All open; this is the most active fix area in the repository.

### 2. Self-Audit Skill (PR #1367)
A mechanical verification plus four-dimension reasoning quality gate that audits AI output before delivery. Performs file existence verification first, then reasoning quality audits in damage-severity priority order. Universal across tech stacks and models. **Status:** Open, active discussion.

### 3. Hivemind: Zero-Cost Multi-Agent Orchestration (PR #1628)
Delegates mechanical work to headless opencode workers running on free models while Claude Code remains the sole planner, reviewer, and merger. Positioned around the insight that "the expensive model's context is the scarce resource, not its intelligence." **Status:** Open, recent activity.

### 4. Document-Typography Skill (PR #514)
Typographic quality control for generated documents — prevents orphan word wrap, widow paragraphs, and numbering misalignment. Addresses quality issues that affect every AI-generated document. **Status:** Open.

### 5. ServiceNow Platform Skill (PR #568)
Broad ServiceNow assistant covering ITSM, ITOM, ITAM/SAM, FSM, HRSD, SPM/PPM, vulnerability response, and IntegrationHub. Designed as a platform-level skill rather than a narrow scripting helper. **Status:** Open, extended discussion window (March–August).

### 6. Testing-Patterns Skill (PR #723)
Comprehensive testing stack coverage: Testing Trophy model, AAA pattern, unit testing best practices, React component testing with Testing Library, and what-to-test vs. what-not-to-test guidance. **Status:** Open.

### 7. Pyxel Retro Game Development (PR #525)
Skill for pyxel-mcp, an MCP server for the Pyxel retro game engine. Covers write → run_and_capture → inspect → iterate workflow for pixel-art/8-bit Python games. **Status:** Open, long-lived discussion (March–July).

---

## 2. Community Demand Trends

From the Issues tracker, the most anticipated Skill directions are:

| Demand Area | Evidence | Signal Strength |
|---|---|---|
| **Security & Trust Boundaries** | Issue #492 (43 comments): community skills under `anthropic/` namespace enabling trust abuse | 🔴 Critical — highest-commented issue |
| **Org-wide Skill Sharing** | Issue #228 (16 comments): direct sharing within organizations, no manual file transfers | 🟠 High |
| **Reliable Evaluation Tooling** | Issue #556 (12 comments): `run_eval.py` never triggers skills; 0% trigger rate | 🟠 High |
| **Context Window Efficiency** | Issue #1487: `claude-api` skill injects ~156k tokens in a single call | 🟡 Medium |
| **Duplicate Skills Management** | Issue #189: document-skills and example-skills install identical content | 🟡 Medium |
| **Eval Harness Reliability** | Issue #1390: mcp-builder evaluation scores 0/N against real servers | 🟡 Medium |

**Cross-cutting theme:** The community is not primarily demanding *more* Skills — they are demanding *reliable infrastructure* around Skills: security guarantees, evaluation correctness, sharing mechanisms, and context efficiency.

---

## 3. High-Potential Pending Skills

These open PRs show active discussion and may land soon:

| PR | Skill | Description | Created | Comments |
|---|---|---|---|---|
| [#1628](https://github.com/anthropics/skills/pull/1628) | Hivemind | Multi-agent orchestration with free-model workers | 2026-08-21 | Active |
| [#1367](https://github.com/anthropics/skills/pull/1367) | Self-Audit | Mechanical verification + reasoning quality gate (v1.3.0) | 2026-06-28 | Active (updated Jul) |
| [#1615](https://github.com/anthropics/skills/pull/1615) | scnet-hpc | HPC cluster operations via SSH + Slurm workflows | 2026-08-20 | Recent |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | Comprehensive testing stack coverage | 2026-03-22 | Sustained (Mar–Apr) |
| [#568](https://github.com/anthropics/skills/pull/568) | servicenow | Broad ServiceNow platform assistant | 2026-03-08 | Sustained (Mar–Aug) |
| [#525](https://github.com/anthropics/skills/pull/525) | pyxel | Retro game development via MCP | 2026-03-05 | Sustained (Mar–Jul) |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for tooling that makes Skills trustworthy and measurable — security boundaries, reliable evaluation harnesses, context-window discipline, and sharing infrastructure — rather than for additional domain-specific Skills themselves.**

---

# Claude Code Community Digest — 2026-08-26

## Today's Highlights

Two patch releases shipped in the last 24 hours: v2.1.246 adds a safety warning for overly-broad Bash allow rules and introduces a new Auto mode tab in `/permissions`, while v2.1.245 fixes a startup crash on Linux distributions bundling glibc 2.44. The community's attention remains split between a long-running cyber-safeguard false-positive saga (#84352, 155 comments) and a highly-upvoted feature request for message queuing (#50246, 199 👍). The Windows desktop app continues to generate a steady stream of crash and packaging-related reports.

## Releases

**v2.1.246** — Adds a startup warning for Bash allow rules with wildcards before the subcommand (e.g. `Bash(git * main)`), which can unintentionally match options inserted before the subcommand. Also adds an Auto mode tab to `/permissions` for viewing and editing auto mode classifier rules.

**v2.1.245** — Fixes a startup crash on Linux distributions shipping glibc 2.44 (e.g. Arch Linux, CachyOS, Fedora Rawhide).

---

## Hot Issues

1. **[#84352 — CVP-approved org still receives cyber safeguard blocks](https://github.com/anthropics/claude-code/issues/84352)** — *155 comments, 24 👍* · A Claude.ai org previously granted Cyber Verification Program approval is again being blocked, with the Verification Portal showing the application as "Under review" despite prior approval. The high comment count suggests many affected users are piling on, making this the most active thread today.

2. **[#50246 — Message queue mode](https://github.com/anthropics/claude-code/issues/50246)** — *68 comments, 199 👍* · Closed, but still the most-upvoted feature request on the board. Users want to queue follow-up messages while Claude is mid-task instead of being forced to interrupt and risk derailing the current work. The volume of 👍 signals strong pent-up demand.

3. **[#80444 — Windows desktop GPU-process crash (0x060C201E)](https://github.com/anthropics/claude-code/issues/80444)** — *56 comments* · A fatal crash when opening the in-app Browser tab, leaving the MSIX package unlaunchable until a Repair. Users have reproduced across two NVIDIA driver versions. The severity (bricked app) explains the high engagement.

4. **[#65833 — Scroll wheel broken in TUI on WSL since v2.1.150](https://github.com/anthropics/claude-code/issues/65833)** — *41 comments, 99 👍* · The scroll wheel now sends arrow keys (cycling input history) instead of scrolling the conversation. A long-standing regression with widespread impact on WSL users.

5. **[#86142 — draft-07 outputSchema MCP servers rejected](https://github.com/anthropics/claude-code/issues/86142)** — *29 comments* · MCP servers declaring draft-07 outputSchema are rejected client-side with "unsupported dialect" and never dispatched. Notable because the MCP ecosystem is actively migrating to draft-07.

6. **[#85891 — Windows: window always-on-top with no toggle](https://github.com/anthropics/claude-code/issues/85891)** — *24 comments, 36 👍* · The Claude Desktop window stays above all other apps with no setting to disable it. A Windows counterpart to the previously-reported macOS issue.

7. **[#87804 — Prompt-topic triggers for `.claude/rules/`](https://github.com/anthropics/claude-code/issues/87804)** — *13 comments* · Users want rules to load based on the *subject matter* of a prompt, not just `paths:`. The request specifically calls out that neither existing rule-scoping nor skill-level semantic triggers cover this case.

8. **[#61012 — Usage limit reached repeatedly without active use (Pro)](https://github.com/anthropics/claude-code/issues/61012)** — *18 comments* · Pro users reporting usage-limit blocks despite little or no active usage. Recurring cost/billing frustration that hasn't been resolved since May.

9. **[#89663 — ECONNRESET on streaming with bundled Node v26.3.0](https://github.com/anthropics/claude-code/issues/89663)** — *New today* · Windows 11 users hitting ECONNRESET on nearly every streaming request while the browser UI works fine on the same network. Filed today, 0 comments yet.

10. **[#89464 — Standing CLAUDE.md prohibitions don't fire against incremental drift](https://github.com/anthropics/claude-code/issues/89464)** — *New today* · A "never do X yourself, always delegate" rule is acknowledged but never triggers because the model drifts toward the prohibited behavior one small step at a time. A subtle but important compliance gap.

---

## Key PR Progress

*Only 1 PR updated in the last 24h.*

1. **[#89404 — validate-agent.sh: stop aborting at first warning, stop false-flagging valid agents](https://github.com/anthropics/claude-code/pull/89404)** — by @bcherny · Fixes three `set -euo pipefail` interactions in the plugin-dev skill's `validate-agent.sh`: `((warning_count++))` / `((error_count++))` abort the script on the first warning (since the arithmetic expression evaluates to 0), and legitimate agents are incorrectly rejected. Addresses public issue #83803.

---

## Feature Request Trends

- **Non-interruptive workflows.** The most-upvoted request (#50246, message queue mode) and the "incremental drift" complaint (#89464) both reflect a desire for Claude to handle multi-step, parallel work without losing state or violating standing rules. Users want *less* interruption and *more* adherence to long-lived constraints.

- **Context-aware rule loading.** A cluster of requests — prompt-topic triggers for `.claude/rules/` (#87804), skill-scoped hook lifecycle (#89669), and semantic triggers on skills — points toward wanting rules and hooks to activate based on *what the model is doing*, not just static file paths. The current tooling is felt as too coarse.

- **Hooks that respect boundaries.** Two issues (#89669, follow-up to #82801) ask for hook scope limited to a skill's active execution rather than persisting for the whole session. The maintainer's "working as documented" response has not satisfied users.

- **Per-OS desktop polish.** Always-on-top windows (#85891), off-screen dialog restoration (#89668), and plugin UI state confusion (#89667) show the desktop apps (especially Windows) lagging behind the CLI in maturity.

---

## Developer Pain Points

- **Windows packaging is fragile.** The MSIX package continues to generate crashes (#80444, #85901), update-lock failures (#73694), and silent background-agent kills (#82277). Users are repeatedly forced to "Repair" or reinstall to recover.

- **Context-window edge behavior is broken.** Autocompact never fires proactively at the context edge (#77509), leaving autonomous sessions parked indefinitely. Combined with the scroll-wheel regression (#65833) and mouse-mode exit bug (#79015), the TUI/agent experience in long sessions is a consistent source of complaints.

- **Safety and permission systems are either too broad or too blind.** The new wildcard warning in v2.1.246 is a direct response to Bash allow rules matching unintended patterns, while #84352 shows that overly-aggressive cyber safeguards are still blocking legitimate approved orgs. Balance remains elusive.

- **Silent partial failures.** Things that "look" enabled but aren't: Slack connector invisible to routines (#89665), plugins shown as Disabled while working (#89667), Cowork sessions reporting zero connected folders (#86647). These are harder to debug than outright crashes and erode trust.

- **Standing instructions degrade over time.** The "incremental drift" report (#89464) captures a subtle but real problem: CLAUDE.md prohibitions are read once, then the model crosses the line one small step at a time without any single action large enough to trigger the rule. This suggests a need for stateful, cross-turn rule enforcement rather than per-message checks.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-26

## Today's Highlights

The Codex team shipped three rapid-fire Rust alpha releases (0.150.0-alpha.9 through alpha.11) while merging a wave of infrastructure PRs focused on MCP OAuth enterprise identity, exec-server test hardening under Bazel, and credential sanitization. The community's attention remains heavily concentrated on Windows desktop stability, with multiple new reports of startup failures, thread disappearance, and sandbox recovery errors — a trend that has persisted for weeks and now spans 10+ open Windows-specific issues.

---

## Releases

Three new alpha releases were published in the last 24 hours, all part of the Rust 0.150.0 line:

- **rust-v0.150.0-alpha.9** — [Release](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.9)
- **rust-v0.150.0-alpha.10** — [Release](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.10)
- **rust-v0.150.0-alpha.11** — [Release](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.11)

Release notes are minimal; the rapid cadence suggests a hotfix cycle. No changelog details were published in the release metadata.

---

## Hot Issues

1. **[#11023 — Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)** — *CLOSED; 209 comments, 953 👍*
   The most-upvoted open feature request in repo history. Users want a Linux desktop app due to macOS power consumption issues (referenced issue #10432). The closure suggests a resolution or roadmap commitment, but the community demand signal is massive.

2. **[#38350 — Recurring scheduled tasks auto-disable](https://github.com/openai/codex/issues/38350)** — *40 comments*
   Scheduled tasks silently flip from enabled to paused after successful runs without user action. Four unrelated tasks disabled simultaneously in one occurrence — points to a server-side state bug, not user error.

3. **[#28919 — Windows missing "control other devices" tab](https://github.com/openai/codex/issues/28919)** — *44 comments, 42 👍*
   Windows desktop app lacks the remote device control settings tab present on macOS. Windows users are increasingly vocal about feature parity gaps.

4. **[#40715 — Windows MCP config "invalid transport" failure](https://github.com/openai/codex/issues/40715)** — *17 comments*
   Stable 26.820.60940 fails parsing `mcp_servers.codex_app` while Beta 26.727.40816 works. This is a regression in the stable channel — notable because MCP configuration is becoming business-critical for enterprise users.

5. **[#17598 — Native subagent orchestration broken with custom providers](https://github.com/openai/codex/issues/17598)** — *14 comments*
   Subagent orchestration doesn't respect non-OpenAI custom model providers. As enterprises increasingly BYO-model, this limitation blocks adoption.

6. **[#23411 — Code Mode `exec` doesn't fire PreToolUse hooks](https://github.com/openai/codex/issues/23411)** — *9 comments*
   The freeform `exec` tool in Code Mode bypasses `PreToolUse` hooks — same bug class previously fixed for `apply_patch` (#18391). Security-relevant: hook-based guardrails silently don't apply.

7. **[#31868 — Support 1M context for GPT-5.6](https://github.com/openai/codex/issues/31868)** — *8 comments, 22 👍*
   Follow-up to #19464 requesting the 1M context window in Codex clients. Strong demand signal for long-context workflows, especially for repo-scale tasks.

8. **[#35555 — CLI hard-fails on telemetry DB lock](https://github.com/openai/codex/issues/35555)** — *7 comments*
   The CLI aborts at startup when any process holds a write lock on `logs_2.sqlite` — a 5-second busy timeout with no retry gates the entire boot. Maddening for users running multiple Codex instances or long-lived sessions.

9. **[#39819 — Tool Call Visibility as config option](https://github.com/openai/codex/issues/39819)** — *CLOSED; 3 comments, 10 👍*
   Community pushback on the collapsed tool-call view in TUI v149. Users want a `config.toml` opt-out to restore detailed per-call visibility. Closed — likely addressed or deferred; worth watching what ships.

10. **[#38076 — macOS data loss: rollout JSONLs repeatedly deleted](https://github.com/openai/codex/issues/38076)** — *3 comments*
    Active session rollout files are deleted while thread metadata remains. A SHA-256-sealed snapshot proves continued loss across app restarts. This is the most severe data-integrity report in the current queue.

---

## Key PR Progress

1. **[#40739 — Enterprise IdP identity resolution for MCP OAuth](https://github.com/openai/codex/pull/40739)** — Resolves stored enterprise IdP sessions against discovered authorization metadata, requiring configured issuer and public-client authentication. Directly enables enterprise MCP deployments.

2. **[#40722 — Enterprise ID-JAG exchange for MCP OAuth](https://github.com/openai/codex/pull/40722)** — Companion to #40739; adds a non-interactive two-step exchange that trades an enterprise ID-JAG for a resource-bound MCP bearer token with URL/claim validation.

3. **[#40728 — Attachment-owned permissions for MCP servers](https://github.com/openai/codex/pull/40728)** — MCP servers attached to executor environments now retain their owner's permission profile instead of inheriting thread-wide sandbox authority. A meaningful security boundary fix.

4. **[#40737 — Preserve MCP tool output as content items](https://github.com/openai/codex/pull/40737)** — Converts unstructured MCP results into typed function-call output items, preserving media and encrypted content. Improves structured tool-result handling in the protocol layer.

5. **[#40713 — Sanitize credentials from Git remote metadata](https://github.com/openai/codex/pull/40713)** — Introduces `SanitizedGitUrl` to strip embedded credentials before remotes enter turn/thread metadata. Important security hardening for shared session logs.

6. **[#40716 — Thread ownership metadata for managed worktrees](https://github.com/openai/codex/pull/40716)** — Binds managed linked worktrees to threads via versioned `codex-thread.json` in Git metadata, with atomic no-clobber writes. Useful for multi-user worktree isolation.

7. **[#40736 — Exec-server compatibility tests under Bazel](https://github.com/openai/codex/pull/40736)** — Adds Bazel test rules running the shared Noise relay compatibility suite across current, release 0.149.1, and minimum supported binaries. Better regression coverage for the exec-server protocol.

8. **[#40717 — Sandboxed exec-server test environments](https://github.com/openai/codex/pull/40717)** — Test fixtures can now dispatch filesystem-helper invocations and accept a Linux sandbox executable via `CODEX_TE…`, enabling sandboxed CI exec-server tests.

9. **[#40710 — Explicit remote executor connection refresh](https://github.com/openai/codex/pull/40710)** — Adds `Environment::refresh_connection` for remote Noise registry-backed environments, enabling planned executor replacement without waiting on transient-disconnect recovery.

10. **[#40726 — Telemetry for SQLite log persistence](https://github.com/openai/codex/pull/40726)** — Adds visibility into batch size, write latency, failures, and dropped entries for SQLite log persistence, with safeguards preventing exporter diagnostics from feeding back into the log sink.

---

## Feature Request Trends

- **Linux desktop app**: #11023's 953 👍 makes this the single most-requested feature. The closure suggests progress, but the intensity of demand signals a major unmet need.
- **1M context support**: #31868 builds on prior demand for GPT-5.6-class long-context in all Codex clients. Expect this to recur until shipped.
- **Tool-call visibility controls**: #39819 shows users want configurable TUI verbosity — the collapse of tool-call details in v149 drew quick backlash.
- **Managed worktree/thread association**: PR #40716 aligns with earlier requests for structured multi-thread worktree lifecycle management.
- **Hook trust for wrappers**: #21615 asks for a supported path for IDE/wrapper installers to request trust for installed hooks — a growing integration surface.

---

## Developer Pain Points

- **Windows desktop instability is the dominant theme**: 10+ open Windows-specific bugs this week, including startup failures (#40700, #28392), chat disappearance (#40674, #34026), MCP transport regressions (#40715), sandbox recovery crashes (#39251), and thread-store ordinal errors (#40630). Windows users are experiencing the worst reliability of any platform.
- **Session/data integrity issues**: #38076 (rollout JSONL deletion on macOS) and #40219 (deleted conversations repopulating) suggest persistence-layer problems that erode user trust.
- **Hook contract gaps**: Both #23411 (exec bypassing PreToolUse) and #32491 (exec skipping trusted hooks without bypass flag) reveal that hook semantics are inconsistent across Code Mode, `exec`, and app-server paths — a security-relevant reliability gap.
- **Lock and concurrency failures**: #35555 (telemetry DB gate) and #39823 (active writer on resume) indicate the CLI's SQLite/session layer struggles under concurrent use.
- **Stale subagents and rehydration bugs**: #25179 and #37041 both report phantom subagents that can't be closed — a UX and resource-management problem in long-running sessions.
- **Update fatigue**: #30122 (4 comments) captures user frustration with near-continuous app updates, a meta-signal about release cadence vs. quality.

---

*Digest generated from openai/codex GitHub activity, 2026-08-26.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-26

---

## 1. Today's Highlights

**Two stable releases shipped this cycle** — v0.57.0 (with Cloud Workstations OAuth fixes and IDE connection reliability improvements) and v0.58.0-preview.0 (with symlink handling and ignore-path consistency fixes). Activity is heavily concentrated on **agent reliability** — the top issues are about subagents incorrectly reporting success on interruptions, generalist agent hangs, and the model under-utilizing custom skills. From a security posture perspective, this is a notably active day: four separate PRs address hardcoded credentials, SSRF in MCP OAuth flows, unauthenticated A2A server routes, and environment variable injection via extensions — teams relying on MCP or A2A for production workflows should be aware that hardening is in progress.

---

## 2. Releases

### v0.58.0-preview.0
- **Changelog**: [google-gemini/gemini-cli/releases/v0.58.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.58.0-preview.0)
- **Fixes**:
  - `fix(core)`: consistent symlink evaluation in ignore path handling — symlinked paths are now resolved consistently when determining exclusion rules
  - `refactor(core)`: internal cleanup related to ignore path processing

### v0.57.0 (stable)
- **Changelog**: [google-gemini/gemini-cli/releases/tag/v0.57.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.57.0)
- **Fixes**:
  - `fix(core)`: dynamically resolve Cloud Workstations proxy redirect URI for OAuth flows — fixes authentication in proxied/Cloud Workstation environments
  - `fix(core)`: resolve swallowed directory mismatch in IDE connections — IDE integration now correctly detects and surfaces directory mismatches

### v0.56.0-nightly.20260825.g812f7a2bc
- `fix(a2a-server)`: clear stale cancellation error on new message turns
- `fix(core)`: declare top-level safety checkers in write policy configuration

---

## 3. Hot Issues

1. **Subagent recovery after MAX_TURNS reported as GOAL success** — [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)  
   `codebase_investigator` subagent returns `status: "success"` / `Termination Reason: "GOAL"` even when it hit max turns before doing any analysis. This silently hides interruptions from users and breaks downstream decision-making. High-priority, 13 comments, active for several months — a correctness issue in agent termination semantics.

2. **Generalist agent hangs indefinitely** — [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)  
   The generalist agent hangs forever (up to an hour+) on trivial tasks like folder creation when deferred to. Users report that instructing the model not to defer to subagents resolves the issue — a workaround, not a fix. High community engagement (8 👍, 8 comments).

3. **Shell command gets stuck with "Waiting input" after completion** — [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)  
   After simple CLI commands finish, the agent hangs while showing "Awaiting user input." P1 with effort/medium label — this is a "shell never returns" class of bug that erodes developer trust in the agent.

4. **Auto Memory retries low-signal sessions indefinitely** — [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)  
   Sessions that the extraction agent decided not to read (low signal) remain unprocessed forever and get re-surfaced repeatedly — infinite retry loop behavior in background memory system. Part of the broader Auto Memory stability track.

5. **Auto Memory lacks deterministic redaction** — [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)  
   Redaction of secrets happens *after* transcript content is already in model context, and the service can log sensitive information. Security-relevant gap for anyone using Auto Memory in sensitive repositories.

6. **Browser agent fails on Wayland** — [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)  
   Browser subagent fails on Wayland sessions with a generic GOAL termination. Linux/Wayland users are impacted; still open after ~5 months.

7. **Gemini doesn't use skills and sub-agents enough** — [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)  
   Anecdotal but widely felt: the model doesn't proactively use custom skills or sub-agents without explicit instructions, even for highly relevant tasks. Suggests gaps in tool-selection and agent-routing heuristics.

8. **> 128 tools causes 400 error** — [#24246](https://github.com/google-gemini/gemini-cli/issues/24246)  
   Breaking API error when the environment has more than ~128 tools available. The agent doesn't prioritize or limit tools in scope — a scalability ceiling for power users with many extensions/skills.

9. **`get-shit-done` output hook crashes CLI** — [#22186](https://github.com/google-gemini/gemini-cli/issues/22186)  
   Repeated crash when the get-shit-done output is nearly finished (during user summary printing). P1, with maintenance interest. Crash-on-exit behaviors are frustrating for long-running sessions.

10. **PandaDoc extension not appearing in gallery despite matching requirements** — [#28208](https://github.com/google-gemini/gemini-cli/issues/28208)  
    Extension discovery appears broken or at least opaque — a developer-facing frustration for third-party extension authors. The issue links to a previous closed-as-stale one (#27838).

---

## 4. Key PR Progress

1. **Security: enforce auth and stop checkpoint path traversal in A2A server** — [#28699](https://github.com/google-gemini/gemini-cli/pull/28699)  
   A2A custom REST routes were registered without going through `UserBuilder`, so they accepted requests with zero credentials. This PR enforces authentication and prevents path traversal via checkpoints. Closes a serious unauthenticated-access vector for developers running A2A servers.

2. **Security: prevent SSRF in MCP OAuth metadata discovery and authentication** — [#29081](https://github.com/google-gemini/gemini-cli/pull/29081)  
   Enforces RFC 9728/8414 constraints: HTTPS for remote OAuth endpoints (HTTP only for loopback), origin validation for resource indicators, and fetch restrictions during discovery. Critical for anyone using MCP servers over networked OAuth flows.

3. **Security: consent on environment changes in extensions; sanitize runtime-altering variables** — [#28863](https://github.com/google-gemini/gemini-cli/pull/28863)  
   Extension updates could bypass consent and inject unauthorized environment variables into MCP server processes. The PR incorporates MCP env configs into consent strings and sanitizes custom environments. Directly addresses a "supply chain / silent config change" attack surface.

4. **Security: remove misleading security schemes and hardcoded credentials** — [#29067](https://github.com/google-gemini/gemini-cli/pull/29067)  
   Removes hardcoded credentials from the A2A server's `customUserBuilder` and corrects agent card metadata. Note: the previous version of this PR (#29018) was closed — superseded.

5. **Reliability: prevent concurrent extension install races** — [#29087](https://github.com/google-gemini/gemini-cli/pull/29087)  
   Two concurrent Gemini CLI processes could install/update the same extension with interleaved file copies — now guarded via `proper-lockfile`. Prevents corrupted extension state for those running parallel agents.

6. **Core fix: drop unsafe `diff.external` override** — [#28930](https://github.com/google-gemini/gemini-cli/pull/28930)  
   A previous PR added `['diff.external', '']` to `defaultGitOverrides`, but Git doesn't treat empty values as "unset" — it tries to execute an empty path. This is a real bug that broke Git operations inside the shell sandbox when external diff tools were present on the system. Fixes #28928.

7. **Reliability: fix `IdeServer.stop()` hang with open MCP stream** — [#29088](https://github.com/google-gemini/gemini-cli/pull/29088)  
   `IdeServer.stop()` never resolves because long-lived streaming responses on `GET /mcp` prevent connection drain. Fixes an extension deactivation hang in the VSCode IDE companion. Supersedes earlier attempt #28789.

8. **Correctness: detect mixed line endings instead of flagging CRLF on a single match** — [#28983](https://github.com/google-gemini/gemini-cli/pull/28983)  
   `detectLineEnding()` incorrectly classifies files as CRLF if *any* `\r\n` appears, even in predominantly LF files. Now only flags consistent CRLF files. Prevents spurious rewrites for mixed-line-ending codebases (common on Windows-touched repos).

9. **Fix: TRUST_PARENT rule precedence in folder-trust resolution** — [#28701](https://github.com/google-gemini/gemini-cli/pull/28701)  
   "Longest match wins" logic was producing wrong results when TRUST_PARENT rules appeared alongside more specific rules — fixes incorrect trust decisions for nested folder structures.

10. **Testing/CI: skip environment-dependent tests with reason instead of failing** — [#28832](https://github.com/google-gemini/gemini-cli/pull/28832)  
    On a clean Windows checkout, `npx vitest run` in `packages/core` reports 13 failures that aren't product defects (8 need privileges Windows doesn't grant by default, 4 need PowerShell 7). This PR makes them skip with a reason. Improves contributor experience on Windows.

---

## 5. Feature Request Trends

1. **Zero-dependency OS sandboxing with post-execution intent routing** — [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)  
   The theme: let the model use its native `bash` affinity freely, but safely — sandbox execution without heavyweight wrappers and route intent (read vs. write) after execution. Strong signal that developers want both capability and safety, without a "security tax."

2. **AST-aware file reading, search, and codebase mapping** — [#22745](https://github.com/google-gemini/gemini-cli/issues/22745) and [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)  
   Epic-level interest in using AST-aware tools to slice method bounds precisely, reduce token noise from misaligned reads, and map codebases more efficiently. Recommended starting points: `tilth` or `glyph` tools.

3. **Subagent self-awareness and observability** — several issues in this cluster:
   - Visualize and share subagent trajectories via `/chat share` — [#22598](https://github.com/google-gemini/gemini-cli/issues/22598)
   - Include subagent context in `/bug` reports — [#21763](https://github.com/google-gemini/gemini-cli/issues/21763)
   - Make the agent self-aware of CLI flags/hotkeys/self-execution mechanics — [#21432](https://github.com/google-gemini/gemini-cli/issues/21432)
   
   The pattern: developers want to *see, debug, and reproduce* what's happening inside subagents.

4. **Tactful Extraction for token-frugal surgical reads** — [#19561](https://github.com/google-gemini/gemini-cli/issues/19561)  
   A disciplined search hierarchy (grep → read targeted sections → expand only as needed) to avoid 15k+ token context blowups from "firehose" file reads. Cost-optimization remains a top community priority.

5. **Proactive skill and subagent adoption** — [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)  
   The community consistently asks: *"Why doesn't the model use the tools and skills we configured, unless we explicit command it?"* The "learned helplessness" pattern is a recurring complaint.

---

## 6. Developer Pain Points

1. **Silent failures and misreported agent state** — The #1 cluster is *incorrect success signaling*: subagents reporting GOAL success when interrupted (#22323), hangs treated as completion (#21409), and shell commands stuck in "Waiting input" (#25166). The broader theme: **the agent says "done" when it isn't, and says "waiting" when it's actually stuck.** This erodes trust faster than almost anything.

2. **The model doesn't use its own configured tools enough** — Despite skills, subagents, and sandboxing being configured in `~/.gemini/agents/` and `settings.json`, the model repeatedly misses relevant opportunities to use them (#21968). The model still writes tmp scripts everywhere when asked not to use shell (#23571), and can engage in destructive git behavior when safer alternatives exist (#22672).

3. **Memory system reliability and security** — Memory/auto-memory issues cluster around: sessions being silently skipped or retried forever (#26522), invalid patches hard-dismissed (with a stale inbox summary) (#26523), and secrets entering model context before redaction (#26525). The surrounding theme: *memory is the missing "personalized context" feature, but it's still too fragile and opaque.*

4. **Configuration and discovery are still rough edges** — Symlinks in `~/.gemini/agents/` aren't recognized (#20079), browser agent ignores `settings.json` overrides like `maxTurns` (#22267), and >128 tools triggers a 400 error (#24246). A suite of environment and setup quirks that slow down startup workflow — a consistent source of "I set this up and it just doesn't adhere" friction.

5. **Out-of-the-box terminal UX gaps** — Resize flicker (#21924), high-noise output on large file reads (#19561), subagent context missing from bug reports (#21763), and no easy way to share subagent trajectories (#22598). Impact of these are less severe but still materially affect the long-session developer experience.

6. **Security defaults and documented behavior inconsistency** — The day's PR/issue pairing (SSRF, hardcoded creds, extension env injection, unauthenticated A2A routes) suggests the A2A + MCP server stack is a **high-risk, under-hardened area** for teams running agents in networked setups. The [security-related issue #26525](#) and [PandaDoc extension discovery failure](#28208) point to both *practical insecurity* and *opacity in how extensions are reviewed/published*.

---

*Digest generated from GitHub data for 2026-08-26 in a single pass. For full context, refer to the [issue tracker](https://github.com/google-gemini/gemini-cli/issues) and [release history](https://github.com/google-gemini/gemini-cli/releases).*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-26

## Today's Highlights

A new prerelease (v1.0.81-10) opens the plugins dashboard to everyone, unifying `/plugin`, `/mcp`, and `/skills` under a single management surface, with `x` now deleting entries across all dialogs. Meanwhile, the issue tracker reveals deepening concerns around MCP server reliability, BYOK model routing, and a prerelease update bug that strands users on stale builds.

---

## Releases

### v1.0.81-10
- **New:** Plugins dashboard is now Generally Available — run `/plugin`, `/mcp`, or `/skills`, or the `copilot plugins` command. Opt out with `PLUGINS_DASHBOARD=false`.
- **Improved:** `x` now acts as the delete key in sandbox config, settings, the MCP dashboard, the sessions dialog, and the diff view.
- View all releases: [github.com/github/copilot-cli/releases](https://github.com/github/copilot-cli/releases)

---

## Hot Issues

1. **[#13 — vi/vim input mode for the CLI](https://github.com/github/copilot-cli/issues/13)** (👍 74, 8 💬)
   The most upvoted open request. Users deeply miss modal editing (vim keys) while writing prompts. Long-running request (since Sep 2025); has not been addressed in any release, and community patience is thinning.

2. **[#3709 — `/model` should include BYOK/local providers in the picker](https://github.com/github/copilot-cli/issues/3709)** (👍 28, 6 💬)
   Currently, BYOK pins a session to one model via `COPILOT_MODEL`, and the `/model` picker only lists GitHub-hosted models. Users want to switch among local providers mid-session.

3. **[#4605 — Prerelease update checker strands users on 1.0.81-9](https://github.com/github/copilot-cli/issues/4605)** (new, 0 💬)
   Freshly filed: `copilot update prerelease` thinks 1.0.81-9 is newer than 1.0.81-10 because both releases share `created_at`, and the ranking logic picks the wrong one. Verified, concrete release bug.

4. **[#4560 — Model "auto" always runs with reasoning effort disabled](https://github.com/github/copilot-cli/issues/4560)** (1 💬)
   When model is `auto`, `reasoningEffort` is pinned to `null` and attempts to configure one are rejected. Users silently lose reasoning on auto-selected models.

5. **[#4492 — Desktop app WebView2 renderer self-aborts (STATUS_BREAKPOINT)](https://github.com/github/copilot-cli/issues/4492)** (2 💬)
   Closed as moved to the desktop app repo, but the underlying crash — a renderer abort leaving a blank window — remains relevant for desktop-app users of the CLI.

6. **[#4035 — Voice installer hits private Azure Artifacts feed (HTTP 401)](https://github.com/github/copilot-cli/issues/4035)** (4 💬)
   The voice runtime installer tries to pull `Microsoft.AI.Foundry.Local.Core` from a private Azure feed instead of nuget.org, breaking voice mode for users without Azure DevOps access.

7. **[#4542 — Workspace `.mcp.json` detected but not connected in sessions](https://github.com/github/copilot-cli/issues/4542)** (2 💬)
   `mcp list` and `mcp get` show workspace MCP servers as enabled, but they are never actually connected in interactive or `-i` / `-p` sessions. Misleading diagnostics for an invisible failure.

8. **[#4272 — New models greyed out by organization policy — no way to enable](https://github.com/github/copilot-cli/issues/4272)** (👍 3, 1 💬)
   Enterprise users see "disabled by your organization's policy" for many new models, but the referenced settings link offers no way to actually enable them. Unclear for admins and users alike.

9. **[#4604 — User-configured `api.githubcopilot.com/mcp/` loses injected token on 1.0.81-10](https://github.com/github/copilot-cli/issues/4604)** (new)
   Regressed in today's release: user-configured Copilot MCP servers no longer get the injected token, hit 401, and OAuth cannot rescue them because github.com has no dynamic client registration.

10. **[#4593 — Archiving a worktree session fails on Windows (os error 32)](https://github.com/github/copilot-cli/issues/4593)** (1 💬)
    On Windows, archiving a worktree-backed session fails because the session process tree is still running from inside the worktree. Windows-specific reliability gap.

---

## Key PR Progress

Only 1 PR was active in the last 24 hours:

- **[#4607 — Prepare public prerelease v1.0.81-11](https://github.com/github/copilot-cli/pull/4607)** (closed by dereklegenzoff)
  Advances the public repository commit timestamp before publishing v1.0.81-11. Notably, issue #4605 (prerelease ranking bug) may be addressed by this timestamp fix, but there is no explicit confirmation in the PR description.

---

## Feature Request Trends

- **Vim/vi keybindings for all interactive input** (`#13`) — long-standing, high-community support, still missing. The most requested single capability.
- **Shareable/resumable sessions** across machines and teammates (`#3537`, `#1153`) — a clear desire among teams and multi-device users.
- **More flexible model routing** (`#3709`, `#4560`) — include BYOK/local models in the `/model` picker, and make `auto` respect reasoning-effort configuration.
- **Escape-hatch for `ask_user` enum fields** (`#3323`) — suggested answers should not prevent free-form custom input.
- **Better MCP control** (`#3380`) — a `--disable-repo-mcps` flag to skip repository-shipped MCP configs entirely.

---

## Developer Pain Points

- **MCP reliability is the top recurring theme**: several new issues (`#4604`, `#4602`, `#4542`, `#4606`) reflect silent failures across MCP token injection, workspace MCP not connecting, and fragile fail-closed behavior stripping MCP servers from sessions.
- **Release/update issues erode trust**: the `latest-prerelease` stranding bug (`#4605`) plus the regression that dropped exit summaries (`#4268`) highlight workflows that depend on dependable versioning.
- **Configuration that looks right but behaves wrong**: `mcp list` showing enabled servers that never connect (`#4542`), models greyed out with no path to enable (`#4272`), and `auto` models silently running without reasoning (`#4560`) — configurations appear valid but silently degrade behavior.
- **Windows-specific rough edges**: worktree archiving fails with file-lock errors (`#4593`), an ongoing pattern of Windows quality gaps.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-08-26**

---

### 1. Today's Highlights

The community is currently focused on a **critical data-loss regression** in v0.38.0 (Issue #2617), where Edit/Write tools report success without actually writing files on macOS. Additionally, an older **context compaction bug** (Issue #2523) has resurfaced with new activity, involving the CLI reopening completed and deleted tasks. No new releases or pull requests were published in the last 24 hours, indicating a quiet development cycle amid active bug reporting.

---

### 2. Releases

No new releases were published in the last 24 hours. The most recent version remains **v0.38.0**.

---

### 3. Hot Issues

*Only two issues were updated in the last 24 hours; both are listed below.*

- **[#2617 — Edit/Write tools report success but never write to disk (0.38.0, macOS)](https://github.com/MoonshotAI/kimi-cli/issues/2617)**
  - **Author:** tizerluo | **Created:** 2026-08-25 | **Comments:** 2
  - **Why it matters:** This is a **silent data-loss bug**. Both Edit and Write tools return success messages ("The file has been updated...") while writing nothing to disk, 100% reproducible since 2026-08-25. This is the most severe type of issue for developer trust, as it can lead to unnoticed loss of work. The community has not yet indicated a workaround.
  - **Community reaction:** Low engagement (2 comments) but high severity. This is likely the immediate priority for maintainers.

- **[#2523 — Context compaction bug: Kimi Code reopens an already completed and deleted task](https://github.com/MoonshotAI/kimi-cli/issues/2523)**
  - **Author:** Frogzter | **Created:** 2026-07-20 | **Updated:** 2026-08-25 | **Comments:** 1
  - **Why it matters:** After context compaction, the CLI attempts to resume a task that has already been completed and deleted, causing workflow disruption. This is a **state-management defect** in the session/task tracking system, affecting users who rely on long-running sessions. The issue is on older v0.6.3 but was updated yesterday, suggesting continued relevance.
  - **Community reaction:** Still open with minimal traffic, indicating the fix may be lower priority or difficult to reproduce across versions.

---

### 4. Key PR Progress

*No pull requests were updated or created in the last 24 hours. No active PRs to report at this time.*

---

### 5. Feature Request Trends

With only two issues active in the last 24 hours, actionable feature-request signals are limited. However, based on the current open issues and their context, the following trends are observable:

- **Reliability of file operations:** Users are demanding atomic write verification. The top issue (#2617) shows a need for tools to verify write success at the filesystem level rather than assuming success based on API calls.
- **Robust session state management:** The compaction bug (#2523) suggests a need for more resilient task-locking and state persistence, preventing resurrection of completed tasks.
- **Cross-platform parity:** The Write/Edit bug appears macOS-specific, but patterns across platforms (Windows in #2523) indicate users expect consistent behavior regardless of OS.

---

### 6. Developer Pain Points

- **Silent failures:** The most acute pain point is the **lack of error propagation** in file operations. Developers cannot detect when writes fail, making automated workflows risky. This is the #1 actionable item.
- **Session integrity after compaction:** Developers running long automated sessions are frustrated by **zombie tasks** resurfacing after compaction, forcing manual cleanup or workflow interruption.
- **Delayed bug resolution on legacy versions:** Issue #2523 has been open for over a month, signaling pain points around version-to-version consistency and slower fixes for older releases.

---

*Digest generated from MoonshotAI/kimi-cli GitHub activity as of 2026-08-26.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-26

## Today's Highlights
The v1.18.23 patch release addresses critical Cloudflare AI Gateway routing issues for third-party and Anthropic models, while the community reports a significant uptick in "Endpoint is unavailable" errors affecting free-tier models using tools. A new PR set targets the 2.0 auto-updater's 266 GB cache leak, and core test suite isolation work makes running `bun run test` hermetic — no longer loading personal configs or MCP servers.

## Releases
**v1.18.23** — Patch release with two targeted bugfixes:
- Fixed Cloudflare AI Gateway routing for third-party providers so non-Workers models work through the gateway's REST API. ([@superhighfives](https://github.com/superhighfives))
- Fixed Anthropic models through Cloudflare AI Gateway by converting dotted model IDs like `claude-haiku-4.5` to the dashed slug format the gateway expects.

## Hot Issues

1. **[#44300](https://github.com/anomalyco/opencode/issues/44300) — Zen API free models fail with "Endpoint is unavailable" for any request containing tools** (13 comments, 5 👍)  
   The Ox Alpha free model consistently errors on chat completions with a `tools` array, affecting both Zen Console and Go routes. Related reports [#44850](https://github.com/anomalyco/opencode/issues/44850) and [#45073](https://github.com/anomalyco/opencode/issues/45073) confirm this is not an isolated incident — free-tier users frequently hit this wall exactly when agentic tool use kicks in.

2. **[#33618](https://github.com/anomalyco/opencode/issues/33618) — Qwen 3.7 Plus/Max (via OpenRouter) produce unknown/invalid tool calls** (10 comments, 4 👍)  
   Tool calls sporadically fail with empty names (`✗ "" failed`) followed by `Tool execution aborted`, causing repeated retries and aborted sessions. Long-running issue since June; community suspects OpenRouter response formatting drift.

3. **[#19143](https://github.com/anomalyco/opencode/issues/19143) — [FEATURE] Implement message search (Cmd+F / Ctrl+F) in the Desktop App** (9 comments, 8 👍)  
   No way to quickly locate information within long sessions in the desktop app. Persistent demand — this March-opened issue keeps gathering upvotes and activity.

4. **[#35434](https://github.com/anomalyco/opencode/issues/35434) — Multi-question tool calls fail silently in TUI since v1.17.13 (regression from #34116)** (7 comments)  
   The `question` tool with 2+ questions renders the form but pressing Enter sends nothing to the backend — no `reply` or `reject` event. Regression confirmed; single-question calls still work.

5. **[#17846](https://github.com/anomalyco/opencode/issues/17846) — `--log-level DEBUG` fails to log anything** (6 comments, 2 👍)  
   On macOS, once `~/.local/share/opencode/log` hits 10 files, DEBUG logging silently stops. Appears to be a log rotation edge case. Open since March against v1.2.27, still unfixed in current builds.

6. **[#14524](https://github.com/anomalyco/opencode/issues/14524) — [FEATURE] Display model cost in the model picker** (5 comments, 11 👍)  
   No cost indicator when selecting models in the TUI. High upvote count (11) relative to comment count signals strong demand — users want to avoid accidental cost spikes with frontier models.

7. **[#43277](https://github.com/anomalyco/opencode/issues/43277) — Sessions permanently stuck during normal use — survive reboots, cannot be recovered** (5 comments)  
   Sessions become permanently "stuck" (refusing new messages), persisting across full system reboots. Restarting the opencode server does not clear the state — suggests on-disk session corruption.

8. **[#45087](https://github.com/anomalyco/opencode/issues/45087) — [2.0] Auto-updater ate 266 GB by reinstalling OpenCode every 10 minutes** (4 comments)  
   Long-running `opencode2 serve --service` processes reinstall beta packages endlessly into `~/.npm/_cacache`. The running server keeps its old compiled version in memory, so its ten-minute update loop never detects the update it already performed. PR [#45091](https://github.com/anomalyco/opencode/pull/45091) targets this.

9. **[#35494](https://github.com/anomalyco/opencode/issues/35494) — TUI freezes on Debian 13 x86_64 / XFCE / X11 — blank screen, only `kill -9` works** (3 comments)  
   Hard freeze on Linux with X11. No crash logs, no recovery — only force-kill. Open since July, still reproducible.

10. **[#45053](https://github.com/anomalyco/opencode/issues/45053) — `opencode-go/muse-spark-1.2-contributor` hangs indefinitely** (3 comments)  
    Model accepts requests but never responds — no stream, no error, no completion. Other models on the same subscription work fine, suggesting server-side serving issues for this specific model rather than client-side auth problems.

## Key PR Progress

1. **[#45102](https://github.com/anomalyco/opencode/pull/45102) — fix(tui): preserve interrupted Mermaid diagrams**  
   Keeps partially-streamed Mermaid flowcharts rendered when interrupted mid-node, persisting them across session reopens — previously discarded.

2. **[#45103](https://github.com/anomalyco/opencode/pull/45103) — feat(desktop): open existing sessions from deep links**  
   Adds `opencode://open-session?server=...&session=...` links for the Desktop app. "Copy Link" now emits deep links that reopen existing sessions — closes #44167.

3. **[#44845](https://github.com/anomalyco/opencode/pull/44845) — test(core): isolate host configuration and credentials**  
   Makes the Core test suite hermetic with respect to home directories, OpenCode config, credentials, provider settings, npm config, and temp files. `bun run test` no longer loads personal plugins, skills, or MCP servers.

4. **[#45098](https://github.com/anomalyco/opencode/pull/45098) — feat(ai): add native Cerebras and Together AI providers**  
   First-class support for both providers backed by the existing OpenAI Chat protocol. Core resolves both catalog SDK identifiers automatically.

5. **[#45100](https://github.com/anomalyco/opencode/pull/45100) — fix(tui): detect clipped transcript bottom**  
   Fixes false "at bottom" reporting when the final user message is clipped by one terminal row; scroll state now correctly accounts for visible padding.

6. **[#45094](https://github.com/anomalyco/opencode/pull/45094) — fix(ai): preserve provider-defined responses item IDs**  
   Replaces item-type-specific Response ID allowlists with the exact Codex outbound rule: first underscore must have nonempty prefix and suffix. Preserves provider-issued message, reasoning, function-call, and hosted-tool IDs regardless of prefix, length, or characters.

7. **[#44705](https://github.com/anomalyco/opencode/pull/44705) — fix(session): coerce legacy string tool-part input**  
   Fixes `GET /session/:id` crashes by coercing legacy 1.14 string `state.input` values to the `Schema.Record` format that 1.18 expects. Closes #44688.

8. **[#45097](https://github.com/anomalyco/opencode/pull/45097) — fix(tui): avoid false model availability warnings**  
   Stops labeling a selected model `(unavailable)` merely because its display metadata is missing from a stale or still-loading location-scoped client catalog.

9. **[#45002](https://github.com/anomalyco/opencode/pull/45002) — feat(core): repair malformed tool arguments before validation**  
   Adds an internal plugin that repairs common malformed tool arguments before the original Effect/Zod/Standard Schema/JSON Schema validator runs — applies to direct tools and inner CodeMode tool calls, using only unambiguous schema info.

10. **[#45091](https://github.com/anomalyco/opencode/pull/45091) — fix(cli): prevent repeated updates and npm cache growth**  
    Remembers the last successfully installed version to stop long-running services from reinstalling the same release every ten minutes; installs npm updates with a scoped temporary cache that is removed afterward (matching Bun behavior). Directly addresses #45087's 266 GB leak.

## Feature Request Trends
- **Deep linking & session portability**: Desktop deep links ([#45103](https://github.com/anomalyco/opencode/pull/45103)) and session recovery ([#43277](https://github.com/anomalyco/opencode/issues/43277)) suggest a growing need to treat sessions as first-class, shareable, recoverable artifacts.
- **Cost transparency**: The model-picker cost column ([#14524](https://github.com/anomalyco/opencode/issues/14524)) remains in high demand (11 👍) — users increasingly need pricing visibility with the proliferation of cheap and expensive gateway models.
- **Desktop app parity**: Users want Desktop to match CLI capabilities: message search ([#19143](https://github.com/anomalyco/opencode/issues/19143)), MCP server setup UI ([#40335](https://github.com/anomalyco/opencode/issues/40335)), and deep-link session opening.
- **Locale expansion**: New request for Hebrew locale ([#42447](https://github.com/anomalyco/opencode/issues/42447)) alongside existing i18n efforts.
- **Context editing**: Editing/deleting messages in context to recover from dead-end conversations ([#7712](https://github.com/anomalyco/opencode/issues/7712), 12 👍) — long-running request from January still open.

## Developer Pain Points
- **"Endpoint is unavailable" cascade**: A major cluster of issues ([#44300](https://github.com/anomalyco/opencode/issues/44300), [#44850](https://github.com/anomalyco/opencode/issues/44850), [#45073](https://github.com/anomalyco/opencode/issues/45073), [#45020](https://github.com/anomalyco/opencode/issues/45020)) where free/Go gateway models fail exactly when tools are attached — the core agentic workflow breaks for free-tier users.
- **Endless auto-update loops**: The 266 GB npm cache leak ([#45087](https://github.com/anomalyco/opencode/issues/45087)) and repeated reinstall behavior signal lifecycle management gaps in long-running processes.
- **Silent failures**: A recurring theme — hangs without output (muse-spark, #45053), refusals hidden from history ([#44958](https://github.com/anomalyco/opencode/issues/44958)), and stuck sessions that survive reboots ([#43277](https://github.com/anomalyco/opencode/issues/43277)) — making debugging particularly painful when there's no error to chase.
- **Tool-call reliability**: From Qwen's empty names ([#33618](https://github.com/anomalyco/opencode/issues/33618)) to multi-question form submission dead-ends ([#35434](https://github.com/anomalyco/opencode/issues/35434)), the community continues to feel the sharp edges of tool orchestration.
- **Terminal/UI stability on Linux**: X11 TUI freezes ([#35494](https://github.com/anomalyco/opencode/issues/35494)) and console window flashes on Windows ([#42440](https://github.com/anomalyco/opencode/issues/42440)) remain open quality-of-life issues affecting workflow fluidity.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-26

## Today's Highlights

A dense day of upstream fixes lands across the Pi codebase: Bedrock OpenAI models reject images nested in tool results, Grok fails compaction when `tool_choice` is sent without tools, and a language-model verbosity bug caused reasoning text to render one word per line. Community contributors have been busy — the image-handling and provider-compat fixes in particular are landing swiftly, though the Windows experience remains the most active and contested topic in the issue tracker.

## Releases

No new releases in the last 24 hours. (Current public track: 0.84.3.)

## Hot Issues

1. **[#7547 — [Windows] [sink-thread] How do you use Pi on windows?](https://github.com/earendil-works/pi/issues/7547)**  
   The most active thread in the repo (49 comments). Maintainers are explicitly crowdsourcing Windows usage patterns to prioritize fixes. Community reports a wide split between WSL, native, and Docker approaches; no consensus yet. This will likely drive Windows investment decisions for weeks.

2. **[#8584 — TUI row corruption during streaming](https://github.com/earendil-works/pi/issues/8584)**  
   Assistant text rendered one word per line after long tool output. Caused by a model verbosity quirk pushing output near line-width boundaries. Closed today, with the root cause pinned to the verbosity issue below (#8619).

3. **[#5886 — AgentSession settlement/continuation and assistant-tail lifecycle bugs](https://github.com/earendil-works/pi/issues/5886)**  
   Long-standing meta-issue (since June) collecting post-run transcript logic failures. Mirrors several closed issues today about stop-reason handling. A maintainer described it as "a larger fix" without a cohesive explanation yet.

4. **[#7855 — "Response was truncated before completion."](https://github.com/earendil-works/pi/issues/7855)**  
   Intermittent truncation errors on OpenAI-compatible endpoints (VLLM local confirmed). Closed as fixed; likely tied to the compaction/summarization fixes landing today.

5. **[#8582 — Built-in PowerShell tool uses Windows PowerShell 5.1](https://github.com/earendil-works/pi/issues/8582)**  
   Interactive mode falls back to legacy PS 5.1 despite PowerShell 7 on PATH. Print mode correctly uses `pwsh`; the inconsistency is confusing and closed as fixed.

6. **[#8468 — GitHub Copilot fails with timeout](https://github.com/earendil-works/pi/issues/8468)**  
   `Error: Failed to login to GitHub Copilot: The operation was aborted due to timeout`. Closed; required a pre-release checkout to verify, suggesting the fix is in an unreleased commit.

7. **[#6596 — spawn(taskkill) ENOENT on Node.js 24](https://github.com/earendil-works/pi/issues/6596)**  
   Windows process-tree kill fails on Node 24 due to PATH resolution. Open, with an in-progress fix proposing absolute System32 paths. Intersects with the wider Windows thread.

8. **[#8456 — Gemini 3.7 Flash rejects /tree branch summarization](https://github.com/earendil-works/pi/issues/8456)**  
   Built-in summarization sends `MINIMAL` thinking level; Gemini rejects it. User-side adapter gap; workaround exists but root-cause fix not yet merged.

9. **[#6444 — thinkingTokenBudgetField is being ignored](https://github.com/earendil-works/pi/issues/8444)**  
   `supportsThinkingTokenBudget: true` works but the field name remap is ignored, breaking llama.cpp compatibility. Open; affects users running local models with custom budget field names.

10. **[#8636 — Accumulated tool-result images brick sessions on vision models](https://github.com/earendil-works/pi/issues/8636)**  
    Long sessions with image tool results eventually hit `media_budget_exceeded` 400s on providers with per-request patch budgets. Closed as fixed; see PR #8642 for the Bedrock hoisting change.

## Key PR Progress

1. **[#8650 — Omit Responses tool_choice when no tools are sent](https://github.com/earendil-works/pi/pull/8650)**  
   Companion to #8633; fixes Grok compaction failure (`400 A tool_choice was set...`) by omitting the field entirely.

2. **[#8642 — Hoist Bedrock tool result images for OpenAI models](https://github.com/earendil-works/pi/pull/8642)**  
   Moves images out of `toolResult.content` into sibling user content blocks for OpenAI model IDs on Bedrock. Regression-tested; fixes a hard session-killing bug.

3. **[#8641 — Load skills when bash is available](https://github.com/earendil-works/pi/pull/8641)**  
   Skills section now loads when `read` is disabled but `bash` is available. Adds system-prompt regression tests; addresses a capability gap for restricted environments.

4. **[#8639 — Add Opper provider](https://github.com/earendil-works/pi/pull/8639)**  
   New built-in OpenAI-compatible provider (api.opper.ai/v3/compat). Full integration: provider module, catalog generation, docs, and test-matrix coverage.

5. **[#8635 — Preserve aborted stop reason during lazy setup](https://github.com/earendil-works/pi/pull/8635)**  
   Fixes abort handling when a request is cancelled during a lazy auth/tool setup phase. Includes regression test for aborting during tool execution.

6. **[#8633 — Omit Responses tool_choice without tools](https://github.com/earendil-works/pi/pull/8633)**  
   Same as #8650 but for OpenAI Responses and Azure OpenAI Responses paths. Providers reject `tool_choice` when no tools are present.

7. **[#8629 — Add eager tool execution](https://github.com/earendil-works/pi/pull/8629)**  
   Opt-in eager execution for discard-safe tools (V1: `read`). Starts eligible calls at `toolcall_end`, reuses the outcome at dispatch, and otherwise discards without lifecycle events.

8. **[#8627 — Use ctx.cwd for cwd-sensitive tools](https://github.com/earendil-works/pi/pull/8627)**  
   Extensions-registered tools now resolve paths against the real session cwd via ExtensionContext instead of creation-time cwd. Touches read/write/edit/grep and more.

9. **[#8629 — Eager tool execution](https://github.com/earendil-works/pi/pull/8629)**  
   Also noteworthy for its safety design: only finalized, explicitly discard-safe tool calls are eligible. Signals a performance-focused direction for long agent runs.

10. **[#8616 & #8613 — Image/EXIF parsing and share isolation](https://github.com/earendil-works/pi/pull/8616)**  
    Two targeted fixes from the same contributor: `convertToPng()` now scans past non-EXIF APP1 segments (XMP-before-EXIF JPEGs), and concurrent `/share` invocations get unique temp dirs instead of clobbering each other.

## Feature Request Trends

- **Provider expansion is the dominant theme**: Opper joins via PR #8639; DeepSeek's new vision model requested in #8483; SiliconFlow support in #4742 (China + international endpoints). The community clearly wants broad model catalog coverage.
- **Windows-first-class tooling**: The megathread #7547 is a call to action. Between taskkill ENOENT, PowerShell version mismatch, and provider-specific quirks, Windows users are self-organizing to define a coherent experience.
- **Image handling and vision-model robustness**: At least six issues/PRs today touch images — tool-result hoisting, patch-budget enforcement, EXIF parsing, image-only queue delivery. Vision workflows are clearly mainstream now, and edge cases are surfacing.
- **Eager/prefetch execution**: PR #8629 introduces speculative tool execution for `read`. If this proves stable, expect follow-ups for other read-only tools.

## Developer Pain Points

- **Streaming quality**: Garbled output (#8584, #8619), buffer re-parsing (O(n²), #7698), and truncation (#7855) remain recurring themes. Streaming is the most fragile surface in the codebase.
- **Compaction and context management**: A whole cluster of fixes today — reserve token scaling, degenerate stop-reason summaries, `tool_choice`-without-tools, abort-stop-reason preservation. Compaction is executing in production environments with real models that don't behave like the happy path.
- **Windows-specific friction**: PATH issues for `taskkill`, legacy PowerShell fallback, and a general feeling that Windows is "second-class" pervades multiple threads. The community is asking for maintainers to pick a canonical Windows workflow or document the support matrix.
- **Provider-specific API drift**: Anthropic-compatible, OpenAI-compatible, Responses, Bedrock, Codex — each provider has undocumented quirks (tool_choice, thread-id headers, reasoning_details format). Contributors are doing detective work adapter-by-adapter.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**2026-08-26**

---

## 1. Today's Highlights

The Qwen Code team shipped nightly build `v0.22.0-nightly.20260825` with a WebShell workspace directory fix. Meanwhile, the issue tracker paints a busy picture: the `/effort max` provider-compatibility bug (P1) was closed after breaking sessions across OpenAI-compatible providers, and multiple multi-agent coordination gaps (duplicate subagent work, loop-detection false positives) are drawing sustained community attention. The PR queue is dominated by WebShell UX work and a systematic `/review` pipeline hardening effort.

---

## 2. Releases

**v0.22.0-nightly.20260825.22bb5e8b9f** — [Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.22.0-nightly.20260825.22bb5e8b9f)

- `fix(web-shell)`: pass session workspace cwd when opening from overview panel ([PR #9730](https://github.com/QwenLM/qwen-code/pull/9730))

---

## 3. Hot Issues

1. **[#9459](https://github.com/QwenLM/qwen-code/issues/9459) — `/effort max` bricks sessions on OpenAI-compatible providers** *(CLOSED, P1)*
   `clampReasoningEffort()` fails to clamp `'max'`, and every subsequent request 400s until the tier is changed. The UI offers a value that no provider accepts—a sharp edge that burned users mid-session. Closed in 6 days; the community responded strongly with 10 comments.

2. **[#8097](https://github.com/QwenLM/qwen-code/issues/8097) — Background agent coordination gap** *(OPEN, P2)*
   Running multiple Explore subagents leads to duplicate work, premature completion, and non-interactive `send_message`. This is a systemic multi-agent orchestration issue and likely a gateway problem for power users. 8 comments.

3. **[#6762](https://github.com/QwenLM/qwen-code/issues/6762) — Skill Context Lifecycle Management** *(OPEN, P2, feature-request)*
   SKILL.md bodies are loaded into context forever — no unload/compress mechanism. The community wants lifecycle control over skill context to reduce token pressure and improve long-session stability.

4. **[#9198](https://github.com/QwenLM/qwen-code/issues/9198) — OOM on 1TB servers** *(OPEN, P2, need-information)*
   A week-long session eventually OOMs; terminal rendering degenerates into garbage escape codes. Unusual because hardware is not the constraint — points to unbounded memory growth.

5. **[#9309](https://github.com/QwenLM/qwen-code/issues/9309) — Compression is incorrect somewhere** *(CLOSED, P3)*
   `/compress-fast` then `/compress` mishandles context (170k → 7k with an unexpected result). Context management is clearly a top pain point.

6. **[#5823](https://github.com/QwenLM/qwen-code/issues/5823) — `/loop` cron tasks fire silently, with no visibility** *(OPEN, P2)*
   Scheduled tasks continue firing across new chat sessions with zero prompting. Model cannot list or stop its own scheduled tasks — serious autonomy/control gap.

7. **[#9733](https://github.com/QwenLM/qwen-code/issues/9733) — Loop detection false-positives kill unattended turns** *(OPEN, P2, need-retesting)*
   Legitimate verification cycles (write → run → edit → re-run) trip loop detection and terminate turns unrecoverably. Fatal for scripted automation.

8. **[#10000](https://github.com/QwenLM/qwen-code/issues/10000) — `/find-simplifications` candidate ledger** *(OPEN, duplicate)*
   A long-lived ledger for dead-code surveys. The 5 comments are largely meta-discussion; signals growing community interest in repo-maintenance automation.

9. **[#10051](https://github.com/QwenLM/qwen-code/issues/10051) — Native DAP Integration for debugging** *(OPEN, P3, feature-request)*
   Request for first-class Debug Adapter Protocol support so the agent can interact with debuggers programmatically. Fresh request with early traction (4 comments in one day).

10. **[#10057](https://github.com/QwenLM/qwen-code/issues/10057) — Review cleanup deletes concurrent review artifacts** *(OPEN, P2)*
    `qwen review cleanup` uses prefix matching; one target token can be a dash-prefix of another, sweeping away a concurrent review's files. A classic footgun in the review pipeline.

---

## 4. Key PR Progress

1. **[#9260](https://github.com/QwenLM/qwen-code/pull/9260) — WebShell: manual session name survives `/clear`**
   User-chosen session names now persist across `/clear`, live updates, and page reloads. Small UX fix, high daily-impact.

2. **[#9980](https://github.com/QwenLM/qwen-code/pull/9980) — Load model recommendations before editing**
   Replaces #9389 with a bounded, snapshot-before-editing design for the setup wizard. Avoids mounting the editor before recommendations arrive.

3. **[#8927](https://github.com/QwenLM/qwen-code/pull/8927) — `sessionRotation`: bound session lifetime per channel**
   Adds `maxTurns` and a time bound — when a route's session is past its bound, the next message starts a fresh session. Important for long-running channel integrations.

4. **[#9940](https://github.com/QwenLM/qwen-code/pull/9940) — Review: reply carried findings into their thread, resolve fixed ones**
   Multi-round reviews now re-post surviving findings as replies inside the original thread and resolve threads when findings are fixed. Clear improvement to PR review hygiene.

5. **[#9984](https://github.com/QwenLM/qwen-code/pull/9984) — WebShell: opt-in interactive browser terminal**
   Adds a terminal to the WebShell right panel, gated on daemon capability `web_terminal`. Version-safe feature gating done right.

6. **[#9988](https://github.com/QwenLM/qwen-code/pull/9988) — WebShell: session token usage panel**
   Opt-in panel showing total usage, per-model breakdowns, subagent invocations, and tool stats — with graceful reconnect handling. Direct answer to #10015.

7. **[#10010](https://github.com/QwenLM/qwen-code/pull/10010) — Review: warn when a subsystem's Criticals keep regrowing**
   A successor-chain sentinel detects when the same file keeps re-opening Criticals across rounds and leads with a ⚠️ Divergence note.

8. **[#9983](https://github.com/QwenLM/qwen-code/pull/9983) — Keep host-trusted state out of review sandbox writable surface**
   Moves worktree lease files out of the bind-mounted directory the container can write to. Hardening identified from #9723's review.

9. **[#9969](https://github.com/QwenLM/qwen-code/pull/9969) — Accept contained symlinks in older-Git archive fallback**
   The public GitHub extension fallback now accepts symlinks that resolve inside the archive, instead of rejecting all tar link entries. Security-preserving compatibility fix.

10. **[#10055](https://github.com/QwenLM/qwen-code/pull/10055) — Run autofix scan lane on persistent runner pool**
    Moves the autonomous-fix routing and scan off GitHub-hosted runners to the self-hosted pool, with fork-trust and kill-switch controls.

---

## 5. Feature Request Trends

1. **Context/Session Lifecycle Management** — The dominant theme across issues (#6762, #9309, #9198, #10015). Users want: skill-body unload/compression, correct compression semantics, bounded memory growth, and telemetry on context usage.
2. **Multi-Agent Orchestration Visibility** — Background agents, cron jobs, and subagent coordination need better supervision (#8097, #5823, #4055). Users want to see, pause, and kill what the model spawns.
3. **Review Pipeline Automation** — A wave of PRs and issues around `/review` (anchors, deduplication, cleanup safety, divergence detection) indicates the community is pushing for fully-automated, trustworthy code review.
4. **Debugger Integration** — Native DAP support (#10051) is a new, fast-moving request that would extend Qwen Code from static analysis into runtime debugging.
5. **WebShell as a First-Class Surface** — Interactive terminal, token usage panel, compact mode, session workflow cockpit — the WebShell is becoming a full IDE alternative.

---

## 6. Developer Pain Points

- **Context management is the #1 recurring frustration.** Incorrect compression (#9309), unmanaged skill bodies (#6762), unbounded growth (#9198), and unusable telemetry (no context breakdown on spans, #10015) all point to the same root: developers do not trust or understand what is in the context window.
- **Autonomy without guardrails is dangerous.** Silent cron tasks (#5823), loop-detection false positives killing legitimate runs (#9733), and background agent duplicate work (#8097) all erode trust in unattended operation.
- **Provider compatibility is still a sharp edge.** `/effort max` bricking sessions (#9459) and vision models silently dropping image parts (#10027) show that third-party provider quirks can break core flows.
- **Windows remains a second-class citizen.** `O_NOFOLLOW` issues (#8227), a red Windows test lane (#9481), and MCP SSE hangs on Windows (#10056) are recurring themes.
- **CI and infrastructure churn.** ENOSPC on self-hosted runners (#10035), review cleanup deleting concurrent artifacts (#10057), and the constant need to harden sandboxing (#9983) show the cost of a complex build and review pipeline.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest - 2026-08-26

## 1. Today's Highlights

The v0.9.12 integration branch (#5576) is code-complete with 72 commits, gated on release blockers including provider neutrality (#5588), sandbox security hardening (#5568), and fleet cost controls (#5567). A significant three-part feature series from contributor M-Maciej landed: control socket support (#5594), `/relaunch` command (#5593), and lifecycle outbox (#5592) — all merged and closed. The community continues to push on operational reliability, with active discussions around the EPIC-005 crate decomposition umbrella (#5316) and a critical git index.lock issue affecting development workflows (#5617).

## 2. Releases

No new releases in the last 24 hours. The integration branch for v0.9.12 is gated and pending version bump + changelog/RC verification (#5576).

## 3. Hot Issues

1. **EPIC-005: CodeWhale TUI Crate Decomposition** (16 comments, OPEN) — [#5316](https://github.com/Hmbown/CodeWhale/issues/5316) - Umbrella epic tracking the crate structure overhaul. 16 comments indicate active community participation across sub-epics. Author: aboimpinto.

2. **Provider neutrality: 18 DeepSeek-exclusive gates** (5 comments, OPEN) — [#5588](https://github.com/Hmbown/CodeWhale/issues/5588) - Audit found 2,281 lines across 279 files containing 'deepseek' occurrences; 18 suspect gates where behavior is DeepSeek-gated but conceptually provider-neutral. One fix already landed (NVIDIA NIM env leak). Author: Hmbown.

3. **Stale write-claims lock sub-agents out** (3 comments, CLOSED) — [#5562](https://github.com/Hmbown/CodeWhale/issues/5562) - Critical bug: stale write-claims persist forever and cascade-lock other agents from command execution. Verifier role contradicts its own description. Reproducible on Windows 10. Author: slowly247.

4. **MiniMax/Xiaomi 404 on fresh install** (3 comments, CLOSED) — [#5601](https://github.com/Hmbown/CodeWhale/issues/5601) - Chinese-language report: first-time configuration of MiniMax and Xiaomi models returns 404, likely hardcoded URL errors. Workaround: use v0.6 for CLI configuration. Author: Brook-WZ.

5. **Git index.lock prevents commits** (2 comments, OPEN) — [#5617](https://github.com/Hmbown/CodeWhale/issues/5617) - Read-only git probes hold `.git/index.lock`, causing user `git commit` failures. Root cause: `git status` in workspace conflicts. Author: LmeSzinc.

6. **Compaction: publish structured survival contract** (4 comments, OPEN) — [#4394](https://github.com/Hmbown/CodeWhale/issues/4394) - Compaction has substantial implementation but lacks explicit survival contract; needs published, enforceable guarantees about what persists. Author: Hmbown.

7. **Workflow responseSchema failures need bounded repair** (4 comments, CLOSED) — [#5583](https://github.com/Hmbown/CodeWhale/issues/5583) - Schema failures correctly surface but discard opportunity for bounded repair and lack raw-output receipts. Community expressed interest in graceful degradation. Author: jbovard2016.

8. **Workflow owner snapshots collapse Degraded into Completed** (4 comments, CLOSED) — [#5582](https://github.com/Hmbown/CodeWhale/issues/5582) - Degraded workflow owners misreported as Completed in snapshots; needs distinct state representation. Author: jbovard2016.

9. **Replace internal git CLI reads with gix** (1 comment, OPEN) — [#5618](https://github.com/Hmbown/CodeWhale/issues/5618) - Follow-up to #5617: process spawn overhead from git CLI probes (~5+ processes per render in large repos). Proposal: use gitoxide for internal reads. Author: LmeSzinc.

10. **Event-granularity audit: surfaces that stall** (2 comments, OPEN) — [#5581](https://github.com/Hmbown/CodeWhale/issues/5581) - Surfaces only updating at TurnComplete read as frozen during long turns. Cost already fixed (#5578); other surfaces need per-step updates. Author: Hmbown.

## 4. Key PR Progress

1. **0.9.12 integration: must-fix + UX fixes** (OPEN) — [#5576](https://github.com/Hmbown/CodeWhale/pull/5576) - The main v0.9.12 integration branch: 72 commits covering release blockers, UX fixes, provider neutrality, and security hardening. Gated and code-complete for release blockers. Author: Hmbown.

2. **Control socket — part d (final)** (CLOSED) — [#5594](https://github.com/Hmbown/CodeWhale/pull/5594) - Completes supervised operation support: opt-in, Unix-only, newline-framed JSON-RPC socket per session. Default OFF. Closes #5533. Author: M-Maciej.

3. **/relaunch command — part c** (CLOSED) — [#5593](https://github.com/Hmbown/CodeWhale/pull/5593) - Adds missing self-relaunch after `/update`, switching session to current binary in one step. Handles persistence, terminal restore, telemetry flush. Closes #5532. Author: M-Maciej.

4. **Lifecycle outbox — part b** (CLOSED) — [#5592](https://github.com/Hmbown/CodeWhale/pull/5592) - Opt-in `[lifecycle_outbox]` config appending JSONL lines per lifecycle event. Works for interactive TUI and headless exec. Closes #5531. Author: M-Maciej.

5. **Persist child approval receipts** (CLOSED) — [#5584](https://github.com/Hmbown/CodeWhale/pull/5584) - Fixes missing durable evidence for child approval prompts; commits Asked/terminal outcomes to receipt store inherited from session. Author: cyq1017.

6. **Move git_status/git_diff off async executor** (CLOSED) — [#5616](https://github.com/Hmbown/CodeWhale/pull/5616) - Fixes blocking `std::process::Command::output()` in async `execute()` that can stall tokio worker pool and hang entire session. Author: rafaelcavalheri.

7. **Preserve Windows verbatim-path operands** (CLOSED) — [#5610](https://github.com/Hmbown/CodeWhale/pull/5610) - Fixes two Windows CI failures blocking FEAT-019: `enforce_readonly_workspace_operands` mishandled verbatim paths through POSIX word split. Author: aboimpinto.

8. **Adopt command shapes in memory group (FEAT-019)** (CLOSED) — [#5609](https://github.com/Hmbown/CodeWhale/pull/5609) - Converts `/note`, `/memory` to external command shapes from FEAT-014/015, following FEAT-018 pattern. Author: aboimpinto.

9. **Show tool and MCP schema costs (#5603)** (CLOSED) — [#5611](https://github.com/Hmbown/CodeWhale/pull/5611) - Rebase of wuisabel-gif's work: context inspector shows bounded schema-cost estimates per built-in tool and MCP server, sorted by token cost. Author: Hmbown (original: wuisabel-gif).

10. **Add focused transcript actions** (CLOSED) — [#5608](https://github.com/Hmbown/CodeWhale/pull/5608) - `y` copy, `Y` copy metadata, `Enter` fullscreen, `r` raw markdown for focused transcript block when composer empty. Addresses focused slice of #5551. Author: wuisabel-gif.

## 5. Feature Request Trends

- **Supervised/headless operation**: Strong demand for control sockets, lifecycle event outbox, and external supervision support (#5531, #5533) — suggests maturing use in automation/CI contexts.
- **Operational reliability**: Compaction survival contracts (#4394), event-granularity updates (#5581), and bounded repair for schema failures (#5583) all target predictable, auditable behavior under failure.
- **Provider neutrality**: Strong push to reduce DeepSeek-specific gating (#5588), with friction around model configuration for non-DeepSeek providers (#5601).
- **TUI usability**: Focused-block actions (#5551), line-range mentions and hidden-file picker (#5550), and onboarding tutorial (#5556) target power-user workflows.
- **Performance**: Git operations optimization (#5617, #5618) and executor offload (#5616) address latency issues in large repositories.
- **Security hardening**: Sandbox deny-lists (#5568), fleet cost ceilings (#5567), and approval receipt persistence (#5584) — governance and control features for enterprise adoption.

## 6. Developer Pain Points

- **Git CLI interference**: Codewhale's internal git probes holding `.git/index.lock` breaks user's own commits (#5617); also heavy process spawn overhead in large repos (#5618). High-frequency pain with multiple workarounds proposed.
- **Configuration friction**: First-time model setup failures (404s) for non-DeepSeek providers (#5601), and model list not auto-updating (#5607) — onboarding is a recurring weak spot.
- **Sub-agent reliability**: Stale write-claims cascade-locking agents (#5562), approval receipts not persisted (#5543), child approval IDs reused across restarts (#5615) — agent management correctness is fragile.
- **Sandbox over-permissiveness**: Full-disk read access in every posture, including ReadOnly children (#5568), creates secret exfiltration risk; need opt-in deny-lists.
- **Provider-specific assumptions**: DeepSeek-exclusive logic gates leaking into provider-neutral features (#5588); docs still reference deprecated `api.deepseeki.com` host (#5564).
- **Windows-specific breakage**: Verbatim path handling through POSIX word split (#5610), Windows CI failures, and platform-specific behavior in git tools — a recurring theme in the past week's fixes.

---

*Digest generated from github.com/Hmbown/DeepSeek-TUI data as of 2026-08-26. All linked items point to the Hmbown/CodeWhale repository.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*