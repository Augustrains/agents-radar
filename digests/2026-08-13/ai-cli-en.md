# AI CLI Tools Community Digest 2026-08-13

> Generated: 2026-08-13 00:54 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Comparison Report — 2026-08-13

## 1. Ecosystem Overview

The AI CLI tool ecosystem is entering a consolidation-and-stability phase: while new features continue to ship across all major tools, community attention has shifted overwhelmingly toward reliability, and the most heavily-discussed issues cluster around Windows platform instability, session-state corruption, cost-observability gaps, and misleading agent completion signals. The delta between "demo-ready" and "production-safe" is widening as users deploy these tools in multi-agent, long-running, and CI-embedded workflows. Concurrently, security hardening is accelerating — SSRF patches, variable-expansion bypass closures, and MCP config fail-open prevention landed across Gemini CLI, Copilot CLI, and Codex this week — indicating that the ecosystem is being tested under broader enterprise attack surfaces. The growing divergence between OSS tools (Pi, DeepSeek TUI) and vendor-backed products (Claude Code, Codex) highlights a market structuring around enterprise reliability vs. hacker-led innovation.

## 2. Activity Comparison

| Tool | Hot Issues | PRs Active | Release(s) Today | Noteworthy with |
|---|---|---|---|---|
| **Claude Code** | 10+ | 5 | v2.1.229 (patch) | Windows desktop crashes; cyber-safeguard blocks |
| **OpenAI Codex** | 10 | 10+ | rust-v0.148.0-alpha.9 (silent) | IDE context regression; Windows sandbox EPERM |
| **Gemini CLI** | 10+ | 10+ | v0.56.0-nightly.20260812 (fix-flagged) | Subagent success misreporting; security patches |
| **GitHub Copilot CLI** | 10 | 3 (none merged) | None | MCP OAuth and retry failures; model override silence |
| **Kimi Code CLI** | 1 | 2 (open, updated) | None — stabilization phase | Persistent memory (#1283) remains top ask |
| **OpenCode** | 10 | 10+ | v1.18.17 (bugfix) | Billing/free-tier confusion; Mermaid PRs |
| **Pi** | 10 | 10+ (closures) | None | Auto-compaction failure; mouse event hooks (2 PRs) |
| **Qwen Code** | 10+ | 10+ | 3 (preview, nightly, desktop v0.2.1) | Image-load regression; provider wire parity |
| **DeepSeek TUI / CodeWhale** | 10 | 10+ | v0.9.6 (rebrand) | Auto-Review regression; TUI decomposition epic |

## 3. Shared Feature Directions

| Direction | Tools Demanding | Specific Needs |
|---|---|---|
| **Session durability & cross-machine continuity** | Claude Code, Codex, Pi, Qwen, DeepSeek, Kimi | Cross-session state relays, resume without corruption, durable transcripts (non-JSONL-safe), project-scoped memory |
| **Per-thread/per-session cost transparency** | Codex, OpenCode, Claude Code | Per-thread credits in TUI, per-session budgets, spend-stop guardrails |
| **Model selection control** | Copilot CLI, Claude Code, Gemini CLI | Explicit per-subagent overrides, org-catalog awareness, no silent downgrades, reasoning-level-aware auto-pick |
| **Autonomous tool adoption** | Gemini CLI, DeepSeek TUI | Proactive skill/subagent use without explicit prompts, "blind accept" for long-running commands, AST-aware codebase tools |
| **Windows/WSL parity** | Claude Code, Codex, Copilot CLI, Qwen Code | GPU-crash isolation, sandbox ACL handling, keybinding fix (Ctrl+H), Computer Use reliability (not blocked on EPREM) |
| **MCP robustness** | Copilot CLI, Claude Code, OpenCode, Gemini | CIMD OAuth discovery, retry/backoff on transient 5xx, refresh-token lifecycle, no fail-open on corrupt config |
| **Terminal UX polish** | Pi, OpenCode, Claude Code, DeepSeek | Mouse events, rebindable keys, Mermaid rendering (TUI+HTML parity), clickable file paths, autoscroll control, wide-terminal fill |
| **Memory reliability** | Kimi, Qwen, Gemini | Layered auto+manual memory, deterministic recall, low-signal skip, redaction-before-transmission guarantees |
| **Multi-agent coordination safety** | Claude Code, Qwen, Gemini | Subagent done-state accuracy (GOAL ≠ success), no message hijack, background sends in non-interactive mode, agent-to-agent delegation |

## 4. Differentiation Analysis

The three vendor-backed tools are converging on the same battlefield: all have Windows instability, session-durability, model-selection, and MCP robustness on their list — but their accents differ. Claude Code is the enterprise-compliance battleground (cyber-safeguard approvals, EULA/portals, "80-comment thread"); Codex is pushing deepest into cost-governance (per-thread credits, thread-use TUI)—and is also the platform with the most hostile Windows sandbox story. Gemini CLI is running a distinctly security-forward posture (SSRF, variable-expansion bypass, fail-closed MCP) while its agent-runtime behavior (false GOAL reports, hangs) is the least trustworthy of the three. Copilot CLI sits on top of the Copilot Enterprise billing & model-catalogue stack and suffers every oracle-grade enterprise dependency (Entra/AD refresh loops, org-enabled model catalogues not propagating), making it the most visibly "enterprise-coupled" rather than standalone-shipped.

Of the open-source tools, OpenCode has pivoted fastest toward managed service/billing (Zen, Go subscriptions) and is paying the price — its #1 issue cluster is "paid users hitting free-tier caps." Pi (formerly badlogic/pi) is the only one shipping TUI-composition features (mouse hooks, scroll indicators) and local-model bridges, positioning it closest to a hacker-led, Ratatui-native experience. Qwen Code is differentiating on multi-agent lifecycle features (workspace-scoped memory defaults, workflow-agent directory pinning, adaptive journal caps) while remaining uniquely cheap-and-chatty for long-running jobs (accepting "blind accept" requests). DeepSeek TUI/CodeWhale is the smallest and most operator-driven: it is formalizing its rebrand to CodeWhale, decomposing its TUI into crates, and accepting community-PR harvests—a nice sign of maintainability-by-design, but it also carries the oldest regressions (Auto-Review mode silently blocks writes).

Kimi Code is the quietest, in stabilization: its only active issue is the Memory System RFC and its two open PRs are race-condition fixes—not features. That suggests a mature, stable core that is now waiting on the community to design its next big feature.

## 5. Community Momentum & Maturity

- **Claude Code** has the largest and loudest community (12–498 upvotes, 80-comment threads), and the most enterprise-grade reporting quality. Its maintainers run a fast patch cadence (v2.1.229 in 24h) but the backlog of Windows and cyber-safeguard issues is visibly stressing the platform.
- **Codex** ships quickly (11 backend PRs in 24h) but its community is less engaged with bug triage — many issues sit at 1–17 comments and tend to linger (e.g., #25178, 2.5 months). It is the most telemetry-forward but also the most silent on Windows blockers.
- **Gemini CLI** is iterating fastest on *security* and *core-agent* behavior (10 PRs active in 24h) and has an unusually health-conscious community signal (low upvotes but high P1/P2 classification). Its top frustration — false success signals — is one of the most dangerous failure modes a tool can have when automation relies on trust.
- **OpenCode** has the most engaged PR-to-issue-closure coupling (Mermaid feature and subagent-deny PRs are immediate), but the billing issues are revealing a gap between the product managing money and the product managing code.
- **Pi**, **Qwen**, and **DeepSeek** are all in "quality-hardening" mode. Pi and DeepSeek are the most community-adaptive (harvesting PRs from contributors), while Qwen Code is the most feature-rich of the smaller OSS group but shows regression-prone core paths (image load, provider wire).

**Rapid iterators:** Codex, Gemini CLI, OpenCode, Pi (a.k.a. the ones shipping code daily). **Slower, more deliberate:** Kimi Code, DeepSeek TUI/CodeWhale (one release every few days), Qwen Code (multi-channel releases but small deltas).

## 6. Trend Signals

- **"False success" is the new silent killer.** Gemini's GOAL-on-max-turns, Copilot's model overrides, DeepSeek's fake edit success, and Pi's tool-parse failures all hide failures behind a green light. Tool selection is moving from "does it do the job?" to "does it report whether it actually did?" — expect an ecosystem-wide push on verified tool calls (checksums, post-conditions, echo-after-exec).
- **Windows is the new Linux.** The majority of platform-specific pain (GPU crashes, sandbox ACLs, WSL keybinding leaks, 10013 socket errors) is on Windows, not macOS. Enterprises running Windows desktops are the loudest unserved segment right now.
- **MCP is hitting its "great refractor" moment.** After the gold-rush of adding MCP servers, tools are now scrambling to fix lifecycle, OAuth-discovery, retry/backoff, fail-closed defaults, and credential-refresh semantics. Expect a standards push around CIMD and per-server trust boundaries.
- **Cost governance is becoming a feature, not an add-on.** Codex's per-thread credits, OpenCode's budget PR, and Claude Code's silent-upgrade complaints all point to the same reality: users will stop using tools that bill them blind. Per-session limits, spend dashboards, and model-picker controls are table stakes within 12 months.
- **CRLF of session durability is the new CRLF of state.** Cross-machine relays (MEP), project-scoped memory, and durable transcripts are top asks across Claude Code, Kimi, Qwen, and Pi. The tools that master "sleep, resume, transfer, verify" will win the long-running-agents workload.
- **Security events are accelerating.** SSRF fixes in web-fetch, variable-expansion bypass patches, fail-open config prevention, and token-scoped GitHub Actions PATs are all landing within the same week — a signal that AI CLIs are being probed with injection and exfiltration techniques and must now be treated as network-exposed production agents.

---

**Bottom line for technical decision-makers:** The tools are converging on a shared, production-grade baseline (durable sessions, cost observability, MCP reliability, Windows parity, verified completion). Choose your tool based on where they diverge: Claude Code if enterprise compliance is a gating factor; Codex if cost-governance is your #1 constraint; Gemini CLI if security-hardening is non-negotiable (but expect subagent-signal issues); OpenCode if you need a fast-moving, MIT-licensed tool with desktop/CI support; Pi or Qwen if you want to build high-customization local workflows; and Kimi or DeepSeek only if your workloads are already small and simple.

---

**Source:** Community digest summaries (2026-08-13) for Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi (pi-mono), Qwen Code, DeepSeek TUI/CodeWhale.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on the provided data.

---

### 1. Top Skills Ranking

The most-discussed Pull Requests reveal a community focused on tooling reliability, document fidelity, and developer experience.

- **#1298** – `fix(skill-creator): run_eval.py always reports 0% recall...` ([PR #1298](https://github.com/anthropics/skills/pull/1298))
    - **Functionality:** A critical bugfix for the `skill-creator` tooling, addressing a systemic failure where the evaluation script consistently reported `0%` recall, rendering the description-optimization loop useless.
    - **Discussion Highlights:** This PR is the culmination of multiple community reports (Issues #556, #1169). The discussion centers on the root cause: the eval artifact not being installed properly, alongside Windows-specific stream reading issues.
    - **Status:** Open. This is the primary fix for the most prominent tooling bug in the repo.

- **#514** – `Add document-typography skill...` ([PR #514](https://github.com/anthropics/skills/pull/514))
    - **Functionality:** A quality-control skill that prevents common AI-generated document issues, such as orphan words, stranded headers (widows), and numbering misalignment.
    - **Discussion Highlights:** The high level of engagement suggests a strong, universal demand for polish and professional output in document generation. Users are likely focused on the specific rules and heuristics used to fix these typographic errors.
    - **Status:** Open.

- **#486** – `Add ODT skill — OpenDocument text creation and template filling...` ([PR #486](https://github.com/anthropics/skills/pull/486))
    - **Functionality:** Provides comprehensive support for OpenDocument Format files (.odt, .ods), including creation, template filling, reading, and conversion to HTML.
    - **Discussion Highlights:** Addresses a clear gap for open-source and ISO-standard document formats beyond the existing Microsoft Office (docx/xlsx) skills. The conversation likely focuses on the complexity of ODF XML and template parsing for a Skill.
    - **Status:** Open.

- **#210** – `Improve frontend-design skill clarity and actionability` ([PR #210](https://github.com/anthropics/skills/pull/210))
    - **Functionality:** This is a meta-PR that revises the existing `frontend-design` skill to make its instructions more concrete and executable for Claude within a single conversation.
    - **Discussion Highlights:** The engagement indicates community concern over *how Skills are written*. The discussion centers on ensuring instructions are actionable and steering behavior effectively, rather than just adding more features.
    - **Status:** Open.

- **#568** – `feat: add ServiceNow platform skill...` ([PR #568](https://github.com/anthropics/skills/pull/568))
    - **Functionality:** A broad, ambitious platform skill covering the entire ServiceNow ecosystem, from ITSM/ITOM to SecOps, HR, and IntegrationHub.
    - **Discussion Highlights:** As a large and complex skill, the discussion is likely focused on the scope, structure, and how to break down such a vast platform into effective, triggerable sub-tasks. The long update history (Aug 12) suggests active iteration.
    - **Status:** Open.

- **#1367** – `feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate` ([PR #1367](https://github.com/anthropics/skills/pull/1367))
    - **Functionality:** A "meta-skill" for auditing AI output before delivery. It focuses on mechanical file verification and a four-dimension reasoning audit.
    - **Discussion Highlights:** This taps into a strong desire for agent self-correction and quality assurance. The discussion likely revolves around the architecture of the quality gate, moving beyond simple linting into reasoning validation.
    - **Status:** Open.

- **#723** – `feat: add testing-patterns skill` ([PR #723](https://github.com/anthropics/skills/pull/723))
    - **Functionality:** A comprehensive skill covering the full testing stack, from philosophy (Testing Trophy model) to React component testing and unit testing patterns.
    - **Discussion Highlights:** This addresses a high-demand area for code generation: producing robust, well-structured tests. The discussion likely focuses on the breadth of examples, best practices (AAA pattern), and edge cases.
    - **Status:** Open.

- **#525** – `Add pyxel skill for retro game development` ([PR #525](https://github.com/anthropics/skills/pull/525))
    - **Functionality:** Integrates the Pyxel retro game engine and its MCP server, enabling Claude to write, run, and visually inspect Python-based 8-bit games.
    - **Discussion Highlights:** A popular creative-coding niche. The discussion likely focuses on the tight `write → run → inspect` iteration loop, which is a powerful demonstration of the Skills + MCP combination.
    - **Status:** Open.

---

### 2. Community Demand Trends

The Issues section reveals several strong, distinct demands from the community:

- **Security and Trust:** The top-voted issue, **#492 (Security: Community skills distributed under anthropic/ namespace)**, highlights a severe concern about trust boundaries. Users are actively worried about malicious skills impersonating official Anthropic skills and the security implications of executing arbitrary code. This is a top priority for ecosystem safety.
- **Tooling Reliability:** The cluster of issues around the `skill-creator` (e.g., #556, #202) shows immediate demand for stable, functional development tools. Users are blocked from contributing high-quality skills and optimizing descriptions because of the `run_eval.py` bug and the tool’s educational tone, which is less efficient for operational use.
- **Collaboration and Discovery:** Issue **#228 (Enable org-wide skill sharing)** with 8 👍 highlights a strong desire for enterprise features. Users need a scalable way to share .skills within organizations rather than manual file transfers. There is also a concern about duplicate skills when installing multiple plugins (#189).
- **Context Window Management:** Issues like **#1487 (`claude-api` skill eagerly injects ~156k tokens)** show that as the library grows, there is acute pain around Skills that are too large or greedily consume context, making them unusable for normal workflows.

---

### 3. High-Potential Pending Skills

These are actively-discussed PRs that are not yet merged but appear close to being landed due to their high relevance and recent activity.

- **#1367 – Self-Audit Skill** ([PR #1367](https://github.com/anthropics/skills/pull/1367)): The "four-dimension reasoning quality gate" is a novel and ambitious contribution that could significantly improve the reliability of Claude's output. A direct response to the proposal in Issue #1385.
- **#568 – ServiceNow Skill** ([PR #568](https://github.com/anthropics/skills/pull/568)): With very recent updates (2026-08-12), the author is still actively working on this. It is a high-value target for large enterprises looking to integrate Claude Code with their ServiceNow instances.
- **#1538 – Spec Compliance Fix** ([PR #1538](https://github.com/anthropics/skills/pull/1538)): This is a crucial "hygiene" PR that fixes two skills that do not conform to the Agent Skills spec. Merging this is essential to maintaining the integrity of the repository and ensuring all example skills validate correctly.
- **#1479 – Plan-File-Hygiene Skill** ([PR #1479](https://github.com/anthropics/skills/pull/1479)): Addresses the real-world problem of accumulating planning artifacts. This skill would provide a lifecycle for planning documents, filling a gap between execution and project management.

---

### 4. Skills Ecosystem Insight

The community's most concentrated demand at the Skills level is for **robust, trustworthy tooling and meta-skills that ensure quality, security, and reliability, rather than just a proliferation of new domain-specific features.**

---

# Claude Code Community Digest — 2026-08-13

## Today's Highlights
A new patch release (v2.1.229) lands with Remote Control session resume and server-supplied hook support for self-hosted runners, while community attention remains locked on unresolved enterprise-grade concerns: the 80-comment cyber-safeguard block controversy (#84352) and the 498-upvote Linux desktop feature request (#65697). Windows desktop stability remains the top pain point, with multiple GPU-process crashes and repair-loop reports surfacing this week.

## Releases
**v2.1.229** — Patch release with three notable improvements:
- Documented `claude remote-control --continue` for resuming the most recent Remote Control session
- Added server-supplied Claude Code hook support for self-hosted runner sessions, matching managed-environment behavior
- Added SSE keepalive pings to gateway streaming responses

🔗 [View release](https://github.com/anthropics/claude-code/releases)

---

## Hot Issues

### 1. CVP-Approved Org Still Receiving Cyber-Safeguard Blocks
[#84352](https://github.com/anthropics/claude-code/issues/84352) — 80 comments, 12 👍
A previously Cyber Verification Program-approved organization is still receiving cyber-safeguard blocks, and the Verification Portal now shows the application as "Under review" despite prior approval emails. The 80-comment thread signals significant enterprise pain and potential compliance workflow disruptions.

### 2. Official Claude Desktop for Linux (Closed)
[#65697](https://github.com/anthropics/claude-code/issues/65697) — 52 comments, 498 👍, CLOSED
The most-upvoted open feature request has been closed, which typically indicates either delivery or internal acceptance. At 498 upvotes, this was the single most-demanded platform gap. Community should verify whether the close means shipment or a deferral decision.

### 3. Multi-Agent Coordination Post-Mortem
[#54393](https://github.com/anthropics/claude-code/issues/54393) — 27 comments
A detailed post-mortem cataloging 12 multi-agent coordination bugs surfaced in a single autonomous overnight cycle. Serves as a canonical reference for concurrent-agent stability issues and remains actively discussed three months after filing.

### 4. Windows GPU Process Crash Kills All Sessions
[#81698](https://github.com/anthropics/claude-code/issues/81698) — 25 comments
Desktop app GPU process crash (exit code 101457950) on Windows 11 takes down all running sessions. The "one crash kills everything" failure mode is critical for production use.

### 5. Plugin Cache Not Invalidated on Update
[#14061](https://github.com/anthropics/claude-code/issues/14061) — 25 comments, 31 👍
`/plugin update` fails to invalidate the plugin cache, forcing users into stale-version limbo. Despite being filed in December 2025, it remains open — a notable long-standing issue.

### 6. Left Arrow Hijacks Chat Navigation (macOS)
[#75899](https://github.com/anthropics/claude-code/issues/75899) — 14 comments, 19 👍
Left arrow in chat input (empty box, manual mode) navigates to the agents screen and isn't rebindable. Returning from there breaks the main session view. A usability regression that disrupts a core interaction.

### 7. Claude Desktop Repeatedly Crashes, Requires Repair
[#85199](https://github.com/anthropics/claude-code/issues/85199) — 13 comments
New report of persistent Windows desktop crashes requiring "Advanced Options → Repair" each time. Continues the platform's recent pattern of Windows desktop instability.

### 8. Opus 5 Hallucination Regression
[#82326](https://github.com/anthropics/claude-code/issues/82326) — 9 comments
User reports Opus 5 "again started inventing answers which 4.8 did not do" with **no error output captured**. The sparse error data makes diagnosis difficult, but the pattern (new model intro, hallucination reports) is familiar.

### 9. Browser Automation Blocked on Financial Sites
[#40173](https://github.com/anthropics/claude-code/issues/40173) — 12 comments, CLOSED
Claude-in-Chrome blocks browser automation on banking/brokerage domains. Server-side domain blocking limits legitimate business automation. Now closed — presumably resolved or consciously scoped.

### 10. Cross-Session Messages Never Reach Runtime Queue (Regression)
[#86237](https://github.com/anthropics/claude-code/issues/86237) — 1 comment, filed today
Cross-session messages render in the target session's UI but never reach the runtime input queue. Confirmed regression between 2.1.222 and 2.1.227 — a serious interleaving agent bug.

---

## Key PR Progress

### 1. **MEP: Multi-Machine Async State Relay**
[#42996](https://github.com/anthropics/claude-code/pull/42996) — OPEN
"Meat Puppet Elimination Protocol" — a zero-infrastructure pattern for eliminating context loss when switching machines or resuming sessions. Three files; directly addresses a top community concern about session portability.

### 2. **Stale Doc Links Cleanup**
[#85822](https://github.com/anthropics/claude-code/pull/85822) — CLOSED
Converts outdated `docs.anthropic.com` links to canonical `code.claude.com` targets across plugins, README, and examples. Verified against live redirects. Small but high-velocity maintenance.

### 3. **Remaining Stale Docs Sweep**
[#85925](https://github.com/anthropics/claude-code/pull/85925) — CLOSED
Follow-up cleanup swapping old-domain doc links for canonical targets in plugins, skills, agents, commands, and issue-template contacts. Coordinate-paired with #85822; zero file overlap.

### 4. **Scope `child_process_exec` to JS/TS (Fix Python False-Positive)**
[#57888](https://github.com/anthropics/claude-code/pull/57888) — CLOSED
Rewrites the `child_process_exec` rule in `security_reminder_hook.py` so the substring `"exec("` no longer matches Python's `asyncio.create_subprocess_exec(`. A targeted fix for a nagging false-positive.

### 5. **Add Missing Source to Claude Code**
[#41611](https://github.com/anthropics/claude-code/pull/41611) — OPEN
A long-lived PR (April 2026) with minimal description. Community interest appears limited, but the age and persistence suggest niche value.

---

## Feature Request Trends

1. **Linux Desktop is the Biggest Open Gap** — Repeated calls for an official Linux desktop build (Ubuntu LTS/Debian), now closed after reaching 498 👍. Watch for release notes.

2. **Session Management & Continuity** — Multiple requests for: marking agent sessions complete (#66202), surfacing on-disk transcripts for cross-machine continuity (#81835), and MEP-style state relay (#42996). Users want Claude Code to behave like a durable workspace, not a stateless terminal.

3. **Terminal Accessibility & Keybinding Freedom** — Requests for rebindable arrow navigation (#75899), Kitty keyboard protocol detection via `CSI ? u` capability instead of terminal-name allow-lists (#71700), and better MCP annotation audience handling (#72239).

4. **Cost Transparency & Model Control** — Silent default model upgrades that trigger unexpected API charges (#71481) and missing model-picker options (#68287, #69109) point to a trend: users demand explicit control over which model runs and what it costs.

5. **Agent Visibility & Lifecycle** — Users want richer agent state indicators ("needs input, sleeping" vs. "done", #86082), completion/ dismissal actions (#66202), and fewer agent-view navigation surprises.

---

## Developer Pain Points

1. **Windows Desktop Instability is Acute** — The cluster of reports (#81698, #85199, #85905) describes a catastrophic failure pattern: GPU process crash → entire app dies → MSIX self-repair fails → app uninstalls itself and wipes data. This is the most damaging and repeatable theme this week.

2. **Cross-Session Messaging Is Broken on Two Fronts** — The receiving session gets interrupted with no message knowledge (#86059), and cross-session messages sometimes render but never reach the runtime queue (#86237). For anyone running multi-agent workflows, this is a showstopper.

3. **Plugin & Extension Cache Staleness** — `installed_plugins.json` not updating on marketplace fetch (#76882) and `/plugin update` not invalidating the cache (#14061) both trap users on outdated plugin versions.

4. **Model Migration Surprises** — From silent default model flips billing users $500+ (#71481) to capability regressions in WebSearch at high effort (#83364) and hallucination relapses (#82326), model updates are a recurring source of trust-breaking surprises.

5. **MCP & Connector Reliability** — Managed connectors that can never be re-attached (#71649), Meta MCP timeouts in CLI while fine in web (#86023), and 4-minute server-complete-but-client-never-gets-it timeouts (#86235) — MCP integration quality remains uneven.

6. **Persistent Linux Gaps** — Capable terminals denied features due to allow-lists (#71700), plus the closed-but-unconfirmed Linux desktop status (#65697), keep Linux as the platform where the community feels least served.

---

*Digest generated from public GitHub data for anthropics/claude-code, 2026-08-13.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-13

## Today's Highlights

A quiet but productive day for Codex: the team shipped `rust-v0.148.0-alpha.9` and merged a substantial batch of backend PRs focused on thread-usage telemetry, per-thread cost tracking in the TUI, and plugin metrics collection across unified exec. Community attention remains firmly centered on the **Windows Computer Use sandbox EPERM failures** (two new reports this week) and a **long-running regression where IDE context silently disables** across recent VS Code extension builds. Notably, the macOS crash-loop issue from earlier this week appears resolved.

## Releases

- **rust-v0.148.0-alpha.9** — 📦 [openai/codex releases](https://github.com/openai/codex/releases)
  A patch-level alpha release (0.148.0-alpha.9). No detailed changelog published in the release body.

## Hot Issues

1. **[#25178 — Windows Computer Use screenshot fails on Win10 22H2](https://github.com/openai/codex/issues/25178)** (25 comments, 13 👍)  
   The longest-running Windows CU issue: `get_window_state` fails with `0x80004002` when `SetIsBorderRequired` is called, blocking screenshots entirely even though window listing and keyboard input work. High engagement suggests a wide install base affected.

2. **[#31553 — VS Code extension stopped auto-including IDE context after update](https://github.com/openai/codex/issues/31553)** (17 comments, 12 👍)  
   Community's most-upvoted current bug: IDE context silently stops being attached in `.vscode-server` remote/container setups after extension update 26.623.141536. This is part of a broader regression cluster (see also #34696, #35333).

3. **[#37398 — Desktop: ~5s delay on unloaded local chats](https://github.com/openai/codex/issues/37398)** (14 comments, 9 👍)  
   Opening any unloaded chat incurs a fixed owner-discovery timeout (~5s) even when the actual thread read completes in <200ms. Users report feeling this as a universal sluggishness in the Desktop app.

4. **[#37415 — Windows Computer Use spawn EPERM; WindowsApps ACL blocks elevated sandbox](https://github.com/openai/codex/issues/37415)** (13 comments, 4 👍)  
   Fresh report (Aug 7) showing the **sandbox setup itself fails** with `spawn EPERM` on Windows, tying the Computer Use failures to a deeper elevated-sandbox setup problem on WindowsApps ACLs.

5. **[#33967 — ChatGPT for Windows stuck on "Complete Windows setup" screen](https://github.com/openai/codex/issues/33967)** (12 comments)  
   Setup cannot proceed at all for some users on x64 Windows; app is stuck pre-onboarding with no workaround, making the app entirely unusable for those affected.

6. **[#34920 — IDE Context RPC serialization error in extension 26.715.x](https://github.com/openai/codex/issues/34920)** (10 comments, 5 👍)  
   Confirmed across three successive versions (26.707.x, 26.715.x) and two IDEs (VS Code, Devin). Important because it narrows the regression window and offers a rollback path.

7. **[#35419 — IDE context auto-disables in WSL2 with VS Code](https://github.com/openai/codex/issues/35419)** (6 comments, 10 👍)  
   Second most-upvoted issue on the board. IDE context auto-disables and selected text is never attached when using WSL2 remote. Highly relevant given the volume of WSL-based Windows developers.

8. **[#24280 — Remote-created Desktop threads miss automation events](https://github.com/openai/codex/issues/24280)** (5 comments, 6 👍)  
   A long-running (since May) architectural issue: threads created via remote control / app-server do not receive `automation_update` or `load_workspace_dependencies`, breaking dynamic tool provisioning for remote workflows.

9. **[#23517 — Request: disable autoscroll setting](https://github.com/openai/codex/issues/23517)** (5 comments, 8 👍)  
   Simple UX ask, strong support: users find forced autoscroll during responses visually uncomfortable, especially for long messages. Requesting a setting to control it.

10. **[#37493 — macOS crash-loop on 16 GB Apple Silicon (CLOSED)](https://github.com/openai/codex/issues/37493)** (3 comments)  
   V8 "heap out of memory" crashes ~6s after launch on 16 GB machines, while identical builds work on 48 GB machines. **Likely fixed/resolved** — worth verifying the closure reason for affected users.

## Key PR Progress

1. **[#38275 — Unify turn input submission and routing](https://github.com/openai/codex/pull/38275)**  
   Adds `TurnInputRequest` with typed results for start / steer / decline. Exposes `start_or_steer_turn`, `start_turn_if_idle`, `steer_turn` on `CodexThread`. This centralizes one of the most complex parts of the app-server.

2. **[#38282 — Add thread usage to TUI status surfaces](https://github.com/openai/codex/pull/38282)**  
   Adds `thread-credits` and `estimated-thread-cost` items to the configurable status line and terminal title for Enterprise workspaces. Fetch-only-when-selected to avoid overhead; omits unavailable values gracefully.

3. **[#38281 — Show estimated thread usage in `/status`](https://github.com/openai/codex/pull/38281)**  
   Extends `account/usage/read` with `threadId` and returns `threadUsage` with estimated credits, optional USD cost, and a token/breakdown breakdown. Likely the enterprise cost-governance feature the community has been asking for.

4. **[#38283 — Collect plugin metrics from remote executors](https://github.com/openai/codex/pull/38283)**  
   Resolves manifest-declared metric operations against the executor filesystem for remote plugin commands; creates a sidecar in an executor-native, owner-private temp dir and streams bounded output back.

5. **[#38276 — Track plugin metrics for background unified exec commands](https://github.com/openai/codex/pull/38276)**  
   Fixes a race where unified exec yields while the command is still running; measurement collection now stays active until the background exit, even when the item completes after the turn.

6. **[#38257 — Reconnect gRPC code-mode sessions after host restarts](https://github.com/openai/codex/pull/38257)**  
   Reopens cached code-mode sessions when the gRPC host stops; serializes concurrent reconnection attempts and scopes cell IDs to new host generations to keep callbacks consistent.

7. **[#38265 — Bounded fallback ports for Windows managed proxies](https://github.com/openai/codex/pull/38265)**  
   Tries the configured Windows HTTP/SOCKS5 proxy port first, then scans the protocol's preferred port range; reserves HTTP and SOCKS5 listeners independently so collisions don't cascade.

8. **[#38274 — Represent persisted world state as JSON objects](https://github.com/openai/codex/pull/38274)**  
   Tightens `WorldState` typing so snapshots and merge patches are keyed collections of sections, preventing replay code from handling shapes that can't represent world state.

9. **[#38268 — Expose executor skill roots from `skills.read`](https://github.com/openai/codex/pull/38268)**  
   Adds `skill_root` to `skills.read` responses for executor-backed skills, so readers can locate bundled scripts relative to the executor filesystem.

10. **[#38258 — Unify external authentication provider handling](https://github.com/openai/codex/pull/38258)**  
    Standardizes error classification across resolve/refresh/validation for all `ExternalAuth` providers; also allows runtime replacement, clearing recorded permanent refresh failures after successful replacement.

## Feature Request Trends

- **Enterprise cost observability**: Requests for per-thread credits/cost surfaced repeatedly; PRs #38270, #38281, #38282 suggest this is actively being addressed.
- **Better Windows sandbox/Computer Use reliability**: Multiple new issues (#37415, #37743) indicate sandbox EPERM failures are now blocking not just CU but the whole app on Windows.
- **UX control over conversation display**: Autoscroll disabling (#23517) and audible pending-permission alerts in CLI (#11604) reflect demand for better long-running task ergonomics.
- **Remote workflow parity**: Users expect dynamic tooling, automation events, and context to work as well remote as local (#24280).

## Developer Pain Points

- **IDE context regression with no clear trigger**: Multiple issues (#31553, #34696, #34920, #35333, #35419) describe variants of IDE context silently failing. All share a common thread: **context requests constructed without required fields** (e.g., `workspaceRoot`). Developers are frustrated by the silent failure mode and want a robust error surfaced in-IDE.
- **Windows sandbox and Computer Use instability**: EPERM errors on WindowsApps ACLs (#37415) and blocked screenshots (#25178) make Computer Use unusable for a meaningful Windows cohort. One open issue remains unfixed for ~2.5 months.
- **Desktop app startup/loading latency**: Owners discovery timeouts (#37398), sqlite backfill stalls (#28087), and stale subagents leaving the app blank (#38250) all contribute to "app feels slow or broken" on launch.
- **Session state corruption bugs**: Repeated reports of thread.archived resets (#23851), archived conversations reappearing (#25541), and `/fork` breaking parent resumes (#38144) point to underlying session-state management debt.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-13

## 1. Today's Highlights

The Gemini CLI team shipped a nightly release containing a critical fix for false model capacity exhaustion errors and core quota lookup mapping issues, alongside new developer documentation for local evaluation reports. Several security-focused pull requests are moving through the pipeline, including variable expansion bypass hardening, SSRF remediation in web-fetch, and fail-open prevention for corrupt MCP enablement configs. Community-reported agent reliability issues remain the top concern, particularly around subagent success misreporting, hangs, and the generalist agent's behavior.

## 2. Releases

**v0.56.0-nightly.20260812.g5024443c7** — [Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260812.g5024443c7)
- `fix(core,cli)`: Resolve false model capacity exhaustion and fix core quota lookup model mapping ([PR #28730](https://github.com/google-gemini/gemini-cli/pull/28730))
- `feat(evals)`: Add local report command and developer documentation ([PR](https://github.com/google-gemini/gemini-cli/pull/28730))

Also in the pipeline: auto-generated changelogs for **v0.55.1** ([PR #28779](https://github.com/google-gemini/gemini-cli/pull/28779)) and **v0.56.0-preview.1** ([PR #28776](https://github.com/google-gemini/gemini-cli/pull/28776)).

## 3. Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1)
   The `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` even when it hit max turn limits before any analysis. This is particularly dangerous because it hides interruptions, leading users to trust incomplete results. 12 comments, 2 👍.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1)
   Simple delegations to the generalist agent (e.g., folder creation) hang indefinitely — one user waited an hour. The workaround is instructing the model not to defer to subagents. 8 comments, 8 👍 (highest community reaction score this week).

3. **[#21968 — Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2)
   Users report that custom skills and subagents are only invoked when explicitly instructed, despite being highly relevant. The community wants autonomous adoption of configured skills. 6 comments.

4. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1)
   Simple CLI commands hang after finishing, showing a phantom "awaiting user input" state. This blocks automation and multi-step workflows. 4 comments, 3 👍.

5. **[#22093 — Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** (P2)
   A regression where subagents (e.g., generalist) execute despite agents being disabled in all configurations. Users expect disabled to mean disabled. 3 comments.

6. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1)
   Browser agent reports `Termination Reason: GOAL` but produces no output on Wayland sessions. Platform-specific reliability issue affecting Linux users. 4 comments, 1 👍.

7. **[#24246 — 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2)
   Users with many MCP tools or skills hit 400 errors. The expectation is intelligent tool-scoping rather than requiring manual pruning. 3 comments.

8. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2)
   Sessions flagged as low-signal are never marked processed, causing repeated re-attempts and wasted quota. Part of the broader Auto Memory quality push. 5 comments.

9. **[#26525 — Deterministic redaction and reduced Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2)
   Security concern: transcript content is sent to models *before* redaction, and the service can log existing skill data. Privacy-conscious users want guarantees. 4 comments.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2)
    Models occasionally use `git reset --force` or other destructive commands when safer options exist. Community requests built-in safety guardrails for git and database operations. 3 comments, 1 👍.

## 4. Key PR Progress

1. **[#28691 — Block $VAR and ${VAR} variable expansion bypass (GHSA-wpqr-6v78-jr5g)](https://github.com/google-gemini/gemini-cli/pull/28691)** (P1, security)
   Closes an incomplete check in `detectBashSubstitution()` and `detectPowerShellSubstitution()`, adding defense-in-depth hardening for a security advisory. Fixes #28418.

2. **[#28790 — Context-aware silent retries for capacity errors](https://github.com/google-gemini/gemini-cli/pull/28790)** (P1, core)
   Implements silent retry policies for capacity exhaustion with availability TTL, enabling unattended runs to back off without terminating. Closes #28761.

3. **[#28787 — Don't treat corrupt MCP enablement config as empty](https://github.com/google-gemini/gemini-cli/pull/28787)** (P1, core)
   Fixes the fail-open vulnerability where JSON parse failures resulted in all MCP servers being enabled by default.

4. **[#28794 — Prevent fail-open and data loss on corrupt MCP enablement config](https://github.com/google-gemini/gemini-cli/pull/28794)** (P1, core)
   Complements #28787 with a comprehensive fix, preventing both security fail-open and data-loss scenarios. Fixes #28786.

5. **[#28557 — SSRF vulnerability fix via async DNS resolution](https://github.com/google-gemini/gemini-cli/pull/28557)** (P1, security)
   `isPrivateIp()` was synchronous and could only catch literal IPs — hostnames resolving to internal ranges slipped through. Uses async resolution to close the hole. Fixes #28555.

6. **[#28789 — Resolve vscode-ide-companion stop() hang](https://github.com/google-gemini/gemini-cli/pull/28789)** (core)
   Fixes an indefinite hang when active streaming MCP sessions are open during shutdown, plus a keep-alive failure threshold leak. Fixes #28785.

7. **[#28738 — Allow agents to call agents](https://github.com/google-gemini/gemini-cli/pull/28738)** (P2, agent)
   Lets subagents delegate to other subagents or recurse into themselves via `tools:` frontmatter. Fixes #22092" — highly anticipated for complex multi-step workflows.

8. **[#28673 — Add Gemini 3.6 Flash and 3.5 Flash-Lite model configurations](https://github.com/google-gemini/gemini-cli/pull/28673)** (P2, core)
   Adds base model definitions, capabilities matching, aliases, and Code Execution support for the next generation of Flash models.

9. **[#28792 — Normalize git environment and resolve workspace state mismatch](https://github.com/google-gemini/gemini-cli/pull/28792)** (core)
   Standardizes environment configuration for Git subprocesses to ensure predictable, non-interactive execution across repositories.

10. **[#28405 — Prevent scroll position jump during content updates](https://github.com/google-gemini/gemini-cli/pull/28405)** (P1, core)
    Fixes #5009 — scroll position jumps when users scroll up to review changes and new content arrives. Community-requested UX fix. 

## 5. Feature Request Trends

- **Autonomous skill/subagent usage** — Users repeatedly request that the model proactively utilizes configured skills and subagents without explicit prompting ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968), [#21432](https://github.com/google-gemini/gemini-cli/issues/21432)).
- **AST-aware codebase tools** — Multiple EPICs tracking the value of AST-aware file reads, method-bound extraction, and codebase mapping to reduce token noise and turnaround ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)).
- **Subagent trajectory visibility** — Community wants subagent execution paths visible and shareable via `/chat share` for debugging and evaluation ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598), [#21763](https://github.com/google-gemini/gemini-cli/issues/21763)).
- **Browser agent resilience** — Automatic session takeover, lock recovery, and settings override support are recurring asks ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232), [#22267](https://github.com/google-gemini/gemini-cli/issues/22267)).
- **Safety guardrails** — Users want destructive git and database commands blocked or gated behind explicit confirmation ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672), [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)).

## 6. Developer Pain Points

- **Misleading subagent success signals** — The most concerning recurring issue: subagents report `GOAL` success when they actually hit interruptions, errors, or turn limits ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)). This erodes trust in automation.
- **Hangs and stuck states** — The generalist agent hanging indefinitely ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell commands stuck at "Waiting input" ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and interactive-prompt deadlocks ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)) are top frustration drivers.
- **Config not respected** — Issues with subagents running despite being disabled ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)), and settings overrides being ignored by browser agents ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)) suggest configuration trust issues.
- **Tool bloat and limit errors** — 400 errors with >128 tools ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)) and the model creating scattered tmp scripts ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)) reflect growing pains as users scale tool counts.
- **Privacy and security transparency** — Auto Memory sending content to models before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)) and silent config fail-open ([#28787](https://github.com/google-gemini/gemini-cli/pull/28787)) show the community cares deeply about deterministic security behavior.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-13

## Today's Highlights
The majority of today's activity centers on **MCP (Model Context Protocol) reliability**, with three new issues reporting OAuth, retry, and process-lifecycle failures. Model selection and subagent model overrides continue to be a top community frustration, with new reports that explicit `model` configuration is silently ignored. No new releases were published in the last 24 hours.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#4390 — Enabled organization models missing from catalogue](https://github.com/github/copilot-cli/issues/4390)** — Models explicitly enabled by a Copilot Business org (Claude Sonnet 5/Opus 5, Kimi K3) are unavailable in CLI. This is a continuation of widespread enterprise model availability complaints, receiving 4 👍. Related: [#4422](https://github.com/github/copilot-cli/issues/4422), which reports all Claude models disabled for personal Enterprise accounts.

2. **[#1305 — Support CIMD for Remote OAuth MCP Servers](https://github.com/github/copilot-cli/issues/1305)** — Long-standing feature request (35 👍) from February still open. Standard DCR OAuth isn't enough; the community wants CIMD (Credential Issuer Metadata Discovery) for better remote MCP auth flows.

3. **[#4328 — Ctrl+H misread as Ctrl+Backspace under WSL2](https://github.com/github/copilot-cli/issues/4328)** — Input handling regression where `WT_SESSION` leaks from Windows Terminal cause keybinding misbehavior. Broke basic editing for WSL2 users on Windows.

4. **[#4432 — Rubber-duck subagent model override breaks complementary strategy](https://github.com/github/copilot-cli/issues/4432)** — The `rubber-duck` subagent is designed to give cross-family second opinions, but a model-emitted `model` argument silently overrides the `complementary` strategy, defeating its purpose.

5. **[#4346 — MCP registry policy fetch returns 403 for GITHUB_TOKEN](https://github.com/github/copilot-cli/issues/4346)** — In GitHub Actions, non-default MCP servers are completely blocked because the MCP registry policy endpoint rejects the built-in `GITHUB_TOKEN`. Breaks the documented PAT-less setup for anyone using third-party MCP servers in CI.

6. **[#3976 — tgrep indexer OOM-kills host on large monorepos](https://github.com/github/copilot-cli/issues/3976)** — The native Rust `tgrep` trigram indexer has no memory cap and can OOM the host on large repositories. Experiment flag users report it's dangerous to enable.

7. **[#4466 — Remote MCP 5xx on initialize marks server dead for entire session](https://github.com/github/copilot-cli/issues/4466)** — Transient 502s at startup are treated as permanent failures with no retry/backoff. New report, zero comments yet.

8. **[#4464 — MCP OAuth silent refresh always fails with Entra/AD](https://github.com/github/copilot-cli/issues/4464)** — Scope mixing in refresh requests forces interactive sign-in every 60–75 min for Microsoft Entra-protected MCP servers. Severe usability issue for enterprise MCP users.

9. **[#4469 — Orphaned `permission.requested` event replays on every resume](https://github.com/github/copilot-cli/issues/4469)** — A stale directory-access prompt from 10 days prior keeps reappearing, cannot be permanently dismissed. Session-resume state is corrupted.

10. **[#4459 — Auto model selection fails due to reasoning level](https://github.com/github/copilot-cli/issues/4459)** — A reopened variant of the long-standing #2870: `auto` mode mischooses models that cannot handle the required reasoning level, causing plan/execution failures.

## Key PR Progress
Only 3 PRs were active in the last 24 hours, none yet merged:

1. **[#4449 — Migrate pull request automation away from pull_request_target](https://github.com/github/copilot-cli/pull/4449)** — Security hardening: moves invalid-label automation to issue-scoped write tokens and a no-permission `pull_request` signal. Reduces the attack surface of the `pull_request_target` event.

2. **[#4453 — "ship it patch 1" (bot PR, open)](https://github.com/github/copilot-cli/pull/4453)** — An automated "ship it" patching PR; low signal.

3. **[#4452 — Revert 5 copilot/fix with copilot (bot PR, open)](https://github.com/github/copilot-cli/pull/4452)** — A revert PR generated by a bot; low signal.

## Feature Request Trends
- **Model control and transparency** (highest demand): Users want per-subagent model overrides to actually work, `/models` pickers to respect org-enabled catalogues, BYOK providers to list available models dynamically, and complementary-strategy subagents to respect the user's `/subagents` config. Multiple issues (#4432, #4458, #4462, #4358, #4390) point to this.
- **MCP/ACP robustness**: DCR is not sufficient for OAuth flows (CIMD request, #1305). Users want graceful retry/backoff on transient failures, support for `ask_user`-style extension methods (#2109), and graceful handling of refresh-token failures.
- **Resource lifecycle management**: Fix orphaned processes — extension-host processes leaking under `--server --stdio` (#4468), Docker MCP containers not terminating (#4460), and runtime memory caps for native indexers (#3976).
- **Session-state durability**: Preserve durable context across repeated compactions (#4441), fix orphaned event replays (#4469), and fix unstoppable queued-message state (#4373).

## Developer Pain Points
- **Silent model selection overrides**: The community is repeatedly hitting cases where explicitly configured models (frontmatter, env var, or inline `model` args) are silently ignored, downgraded by cost multipliers, or replaced with a session-default model. This is the single loudest frustration right now — model misbehavior is hard to debug because there's no diagnostic signal.
- **MCP in CI and enterprise is fragile**: 403 token errors, transient 5xx permanently disabling servers, and OAuth refresh loops are reported in quick succession, indicating the MCP stack is not yet production-ready for automated pipelines.
- **Windows/WSL2 and input misbehavior**: From keybinding leaks to socket errors (10013) in OAuth flows, Windows-specific experiences continue to be a recurring source of issues.
- **Long-running sessions degrade**: Event store exhaustion, orphaned processes, and corrupted resume states make long-lived agent sessions unreliable. This was the theme of half of today's new triage issues.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-08-13**

---

## 1. Today's Highlights

Activity remains focused on robustness and long‑term usability. Two open PRs addressing edge‑case crashes—a `BrokenPipeError` in the web session runner and a newline‑handling bug in string shortening—received updates, while the long‑running Memory System feature request (#1283) continues to attract community discussion as the top engagement driver. No new releases were published in the last 24 hours.

---

## 2. Releases

No new releases in the last 24 hours. The project appears to be in a stabilization phase with pending fixes not yet bundled into a release.

---

## 3. Hot Issues

Only one issue was updated in the last 24 hours, but it is a significant one:

- **[#1283 — Feature Request: Memory System - Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)**  
  *Author: CatKang | Updated: 2026-08-12 | Comments: 35*  
  This remains the single most‑discussed issue in the project. The request is for a layered memory system: automatic (AI‑managed notes) plus manual (user‑defined persistent instructions). The 35 comments suggest active community design debate on how memory should be scoped (global vs. per‑project) and how conflicts with user‑explicit instructions are resolved. Momentum here indicates this is the next major feature the community expects.

---

## 4. Key PR Progress

Two open pull requests received updates in the last 24 hours, both aimed at hardening existing functionality:

- **[#2449 — fix(string): strip newlines in shorten_middle before the length check](https://github.com/MoonshotAI/kimi-cli/pull/2449)**  
  *Author: Ricardo-M-L | Updated: 2026-08-12*  
  Fixes a subtle bug where `shorten_middle` returns early on short input *before* collapsing newlines, breaking the single‑line summary contract used by `extract_key_argument`. The fix corrects the order of operations ensuring consistent single‑line tool‑call summaries. This matters for log quality and downstream parsing.

- **[#2324 — fix(web): handle BrokenPipeError in SessionProcess.send_message](https://github.com/MoonshotAI/kimi-cli/pull/2324)**  
  *Author: Ricardo-M-L | Updated: 2026-08-12*  
  Addresses a race condition in the web runner where the subprocess may exit between `start()` and the first `stdin.write()` + `drain()`, triggering an unhandled `BrokenPipeError`. The fix adds proper guard handling to prevent a crash in a common shutdown sequence. Relevant for anyone embedding Kimi CLI in a web backend.

---

## 5. Feature Request Trends

While only one issue was active today, its long‑term presence highlights the dominant direction:

- **Persistent Memory** is the clear priority (#1283). The community wants the CLI to remember project conventions, user preferences, and past context without manual re‑prompting. Expect future minor features (session tags, explicit `--forget` commands, memory export/import) to orbit this core request.

- Secondary themes in the broader backlog (from prior activity) include: improved multi‑turn context truncation strategies, better terminal UI rendering for large diffs, and first‑class support for non‑English prompts/ergonomics.

---

## 6. Developer Pain Points

The recent PR activity reveals two recurring frustrations in the developer community:

- **Race‑condition crashes with subprocess I/O** (PR #2324): In web‑embedded deployments, users consistently hit unhandled `BrokenPipeError` when the underlying process exits during message send. This indicates that process‑lifecycle management is fragile in real‑world usage and needs more defensive coding.

- **String‑handling inconsistencies in tool‑call summaries** (PR #2449): The fact that trivial string mutations (removing newlines) are only applied *after* a length check creates surprising output differences for short vs. long inputs. This points to a broader theme of the codebase lacking uniform invariants for text processing utilities—a recurring headache for developers building on top of these helpers.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-13

## Today's Highlights
OpenCode v1.18.17 ships with session compaction improvements for smaller models and MERGE Gateway reasoning support. The community is actively reporting billing/free-tier confusion around OpenCode Zen and Go subscriptions, while PR momentum focuses heavily on the TUI (Mermaid rendering, monochrome fixes) and managed-service lifecycle hardening. Desktop WSL integration is being migrated to the v2 CLI.

## Releases

### v1.18.17
**Core Bugfixes:**
- Session compaction now keeps complete recent turns and produces clearer summaries for smaller models
- Added MERGE Gateway reasoning variants so those model options work correctly (@MatthewFeroz)
- Capped automatic session retries with added jitter to reduce repeated retry storms

## Hot Issues

1. **[#14273: Free usage exceeded when using Zen free models](https://github.com/anomalyco/opencode/issues/14273)** (Closed, 40 comments) — Users with a $3 Zen balance still hit "Free usage exceeded" errors on Kimi K2.5/MiniMax2.5. Matters because billing logic appears to ignore existing balances when free-tier limits are hit.

2. **[#4832: Gemini 3 Pro function calling fails — missing `thoughtSignature`](https://github.com/anomalyco/opencode/issues/4832)** (Closed, 35 comments, 👍14) — Long-running issue where Gemini 3 Pro rejects function calls without `thoughtSignature` support. High community demand for Gemini compatibility.

3. **[#41470: "Copied to clipboard" doesn't work in VSCode Server/Docker](https://github.com/anomalyco/opencode/issues/41470)** (Open, 11 comments) — Copying from OpenCode sessions inside Docker environments shows success but doesn't write to the system clipboard. Frustrating for container-based workflows.

4. **[#3366: Mermaid rendering in chat](https://github.com/anomalyco/opencode/issues/3366)** (Closed, 10 comments, 👍26) — Long-standing feature request now seeing PRs land (#42179, #42130). The community wants diagram rendering natively in the TUI.

5. **[#33027: MCP tools connected but not exposed to agent](https://github.com/anomalyco/opencode/issues/33027)** (Open, 7 comments) — MCP servers connect and report tools via `tools/list`, but the agent never sees them. Core agent-tool integration gap.

6. **[#19005: Make local file paths clickable in terminal output](https://github.com/anomalyco/opencode/issues/19005)** (Open, 7 comments, 👍5) — Generated file paths are plain text; users must manually copy them. Small UX win that keeps getting requested.

7. **[#42128: Free usage limit exceeded on first request (DeepSeek V4 Flash)](https://github.com/anomalyco/opencode/issues/42128)** (Closed, 7 comments, 👍5) — New users hit free-tier limits immediately with zero prior usage. Billing logic appears to default incorrectly for first-time users.

8. **[#41848: LLM retry has no max attempts — infinite retry loop](https://github.com/anomalyco/opencode/issues/41848)** (Open, 3 comments) — RETRY_MAX_DELAY set to ~24 days; stream errors cause infinite retry loops with UI stuck on "Thinking...". System reliability issue.

9. **[#33495: Zen balance doesn't remove free usage cap](https://github.com/anomalyco/opencode/issues/33495)** (Open, 6 comments) — Paid $20+ Zen balance users still hit the 200-request free-tier cap with 429s. Recurring billing confusion across multiple issues.

10. **[#41806: Instance bootstrap hangs forever on Linux — zombie git process](https://github.com/anomalyco/opencode/issues/41806)** (Open, 3 comments) — Git child exits but is never reaped; TUI renders but Enter can't start a session. Intermittent and hard to debug.

## Key PR Progress

1. **[#42202: Add per-session budget limit](https://github.com/anomalyco/opencode/pull/42202)** (Open) — New optional per-session cost budget that stops the assistant when hit, with a TUI sidebar widget to view/set it. Addresses billing concern momentum.

2. **[#42179: Render Mermaid GitGraph diagrams](https://github.com/anomalyco/opencode/pull/42179)** (Closed) — Terminal-native vertical commit graph rendering for `gitGraph` fences. Directly satisfies the long-requested #3366 feature.

3. **[#42130: Render Mermaid timelines](https://github.com/anomalyco/opencode/pull/42130)** (Closed) — Companion to GitGraph: renders `timeline` fences as vertical layouts instead of source code fallback.

4. **[#42174: Subagent sessions inherit ancestor deny rules](https://github.com/anomalyco/opencode/pull/42174)** (Open) — Critical security fix: denies are now fences across session ancestry; previously subagents escaped all configured denies.

5. **[#42185: Prevent stale service replacement](https://github.com/anomalyco/opencode/pull/42185)** (Open) — Older clients no longer replace newer managed background services after updates. Prevents a version-skew class of bugs.

6. **[#42186: Require authenticated service stop](https://github.com/anomalyco/opencode/pull/42186)** (Open) — Managed service must authenticate before client can SIGTERM/SIGKILL. Hardens the lifecycle against misidentified PIDs.

7. **[#42187: Validate promise service discovery](https://github.com/anomalyco/opencode/pull/42187)** (Open) — Trust-boundary fix: validates `JSON.parse` and health bodies before lifecycle logic consumes them.

8. **[#42199: Desktop WSL: use matching v2 CLI](https://github.com/anomalyco/opencode/pull/42199)** (Open) — Migrates Desktop WSL servers to `opencode2` with exact version matching; uses official V2 installer for releases.

9. **[#42198: Preserve monochrome code output](https://github.com/anomalyco/opencode/pull/42198)** (Open) — Fixes Unicode rendering in monochrome mode for fenced code blocks after OpenTUI 0.5.2 regression.

10. **[#42188: Retry migration status transport errors](https://github.com/anomalyco/opencode/pull/42188)** (Open) — Migration overlay keeps polling through transient disconnects instead of showing false failure toasts.

## Feature Request Trends

- **Mermaid diagram rendering** (#3366) — Strongest signal with 26 👍; now being actively delivered through GitGraph and timeline PRs.
- **Clickable file paths** (#19005) — Terminal UX polish; recurring request for generated artifact paths.
- **Per-MCP-server trust configuration** (#40111) — Enterprise users need TLS trust overrides for private-network MCP servers.
- **Per-session budget limits** (#42202) — Cost-control feature now in PR; users want spend guardrails.
- **Protect `.env` files in grep/glob results** (#17073) — Security-conscious users want permission rules applied to search patterns, not just direct reads.

## Developer Pain Points

- **Billing/entitlement confusion is the #1 issue cluster** — At least 7 active issues involve "Free usage exceeded" despite paid balances, Go subscription not recognized, or free-tier caps applying to paying users. The billing system needs a clear triage pass.
- **Session compaction reliability** — Multiple reports (#41268, #41801) of `/compact` producing garbage output or losing context with DeepSeek V4 Flash, including repetition loops and context loss.
- **Retry loops with no escape hatch** — #41848 shows unbounded retries with ~24-day max delay leave users stuck on "Thinking..." with no feedback; needs a max-attempt cap and user-visible error surfacing.
- **Zombie processes on Linux** — #41806 (unreaped git child during bootstrap) and related disk I/O errors (#32571) point to lifecycle management issues on Linux.
- **V2/2.0 transition friction** — Zsh completions broken (#41966), Copilot HTTP 400s restarting sessions (#42089), and Desktop DB schema mismatches ("no such column: project_id") all indicate rough edges in the ongoing v2 migration.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-13

## Today's Highlights
A substantial wave of issue triage and PR closures landed in the last 24 hours, with key fixes addressing long-standing bugs around auto-compaction, the `triggerTurn: false` extension handling, and usage reporting on wire protocols. Two competing PRs implement the long-requested `Component.onMouse` TUI hook, indicating strong community interest in richer extension interactivity. The project remains highly active with 50 open issues and 25 PRs updated, spanning provider compatibility (Ollama, Grok 4.6, MiniMax) and TUI/HTML rendering parity.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#6879 — Auto-compaction never triggers after context grows past 100% until provider overflow](https://github.com/earendil-works/pi/issues/6879)**  
   *17 comments, 17 👍*  
   A critical bug where a 2-hour agentic turn on GPT-5.6-sol blew past the compaction threshold to 373k tokens before the API rejected the request. The community strongly agrees (17 upvotes) that compaction checks should run after every agent step, not just at request boundaries.

2. **[#7730 — High CPU usage on Mac OS with long sessions](https://github.com/earendil-works/pi/issues/7730)**  
   *11 comments, 8 👍*  
   Users report 50–110% CPU usage and 600–800MB memory on macOS during long sessions, seemingly correlated with context size. A performance regression that affects daily driving for Mac users.

3. **[#7683 — Let components receive mouse events on their own rows](https://github.com/earendil-works/pi/issues/7683)**  
   *9 comments*  
   Feature proposal for an optional `Component.onMouse(event)` hook (now closed, with two implementing PRs). This directly addresses extension UI limitations in the fullscreen TUI.

4. **[#7836 — Edit fuzzy match misses lines with differences in whitespace length](https://github.com/earendil-works/pi/issues/7836)**  
   *9 comments*  
   `normalizeForFuzzyMatch` fails to collapse whitespace runs, causing Edit tool failures on semantically identical content — particularly problematic for smaller models, per the reporter.

5. **[#7835 — Edit tool rejects a single-object edits argument](https://github.com/earendil-works/pi/issues/7835)**  
   *4 comments*  
   Some models wrap `edits` as a single object `{oldText, newText}` instead of an array; the tool throws. A robustness issue in tool-input parsing that breaks model compatibility.

6. **[#8000 — "At" file autocomplete ranks deep nested matches above direct children](https://github.com/earendil-works/pi/issues/8000)**  
   *3 comments*  
   Scoped directory autocomplete surfaces improbable deep paths over direct children on basename ties — a UX regression for a common workflow.

7. **[#7783 — agent_end handler sendMessage({triggerTurn:false}) still starts a turn](https://github.com/earendil-works/pi/issues/7783)**  
   *3 comments*  
   Display-only custom messages from `agent_end` still trigger an assistant turn; `isStreaming` stays true until `_emitAgentSettled()`. Fixed by PR #8022.

8. **[#7805 — Root .md docs in skill directories loaded as skills](https://github.com/earendil-works/pi/issues/7805)**  
   *2 comments*  
   `README.md` / `AGENTS.md` / `CLAUDE.md` inside settings-configured skill directories generate spurious validation warnings. Being fixed in PR #8012.

9. **[#8041 — Render Mermaid and LaTeX in HTML exports to match TUI](https://github.com/earendil-works/pi/issues/8041)**  
   *1 comment, 1 👍*  
   Follow-up to #7956: HTML exports still render math and diagrams as raw text. Community seeks parity between TUI and HTML output fidelity.

10. **[#8029 — Very slow performance when moving in prompt editor](https://github.com/earendil-works/pi/issues/8029)**  
    *1 comment*  
    7,000 lines in the prompt buffer makes a single arrow press take 1,650ms — a linear-growth performance regression in the TUI prompt editor.

## Key PR Progress

1. **[#8052 — fix(coding-agent): make session persistence transactional](https://github.com/earendil-works/pi/pull/8052)** *(closed)*  
   Fixes a race where in-memory session graph advances before JSONL append succeeds, preventing corrupted session graphs on `ENOSPC`.

2. **[#7982 — fix(coding-agent): preserve usage in streaming events](https://github.com/earendil-works/pi/pull/7982)** *(closed)*  
   Closes #7911 by re-adding cumulative provider usage to `message_update` wire/RPC events while keeping stream size linear.

3. **[#8049 — feat: use local Ollama models via a local model proxy](https://github.com/earendil-works/pi/pull/8049)** *(closed)*  
   Two dependency-free Node.js scripts to bridge Ollama models into Pi on Ubuntu, macOS, and Windows. Community-driven local-model support.

4. **[#8037 — feat(tui): dispatch mouse events to components via onMouse](https://github.com/earendil-works/pi/pull/8037)** *(closed)*  
   One of two competing implementations of the `Component.onMouse` hook (#7683). `TuiAltScreen` previously swallowed all mouse events.

5. **[#8032 — feat(tui): let components receive mouse events on their own rows](https://github.com/earendil-works/pi/pull/8032)** *(open)*  
   The original #7683 implementation with hit-testing over the `LayoutBox` tree, innermost-first dispatch, and relative coordinates.

6. **[#8042 — feat(ai): add Grok 4.6](https://github.com/earendil-works/pi/pull/8042)** *(closed)*  
   Adds Grok 4.6 to the xAI Responses model set, preserving reasoning levels from `low` to `xhigh`.

7. **[#8030 — feat(ai): add MiniMax image-to-image generation](https://github.com/earendil-works/pi/pull/8030)** *(closed)*  
   Registers global/CN image generation providers with image-input metadata and `subject_reference` URL/base64 parsing.

8. **[#8022 — fix: triggerTurn: false should not start turn](https://github.com/earendil-works/pi/pull/8022)** *(closed)*  
   Fixes #7783: `sendCustomMessage()` was routing all messages through `agent.steer()`; now display-only messages bypass the turn path.

9. **[#7970 — feat(coding-agent): show fullscreen transcript scrolled-up indicator](https://github.com/earendil-works/pi/pull/7970)** *(open)*  
   Adds a `↓` indicator in the status row when the transcript is not following the end of the stream.

10. **[#8012 — fix: dont load root mds as skills in settings](https://github.com/earendil-works/pi/pull/8012)** *(open)*  
    Prevents root `README.md`, `AGENTS.md`, etc. in skill directories from being parsed as broken skills; requires frontmatter to qualify.

## Feature Request Trends

- **Local model integration**: Multiple requests for Ollama/llama.cpp integration (show all models in `/models`, auto load/unload, local proxy scripts) — a clear demand for first-class local-model ergonomics.
- **TUI interactivity extensions**: Mouse events on components (#7683), mid-line slash commands (#8015), and scrolled-up indicators (#7970) reflect a push for a more editor-like TUI.
- **Extension API expansion**: Durable message publication acknowledgments (#8023), display-only message withholding (#8035), and richer hooks signal a maturing extension surface.
- **Output fidelity parity**: Mermaid/LaTeX rendering in HTML exports (#8041) and `cases` environment alignment (#7929) show a strong community desire for consistent rendering across TUI/HTML.

## Developer Pain Points

- **Resource usage grows with session length**: CPU, memory, and prompt-editor latency scale linearly with context/buffer size (#7730, #8029).
- **Whitespace/formatting fragility in Edit tool**: Fuzzy matching misses on whitespace differences and rejects single-object `edits` — particularly painful for smaller models (#7836, #7835).
- **Context management at extremes**: Auto-compaction fails to trigger proactively, only reacting to hard provider limits (#6879).
- **Provider compatibility drift**: OpenAI-compatible proxies (9router), DeepSeek (`max_completion_tokens` vs `max_tokens`), and custom endpoint headers keep breaking silently (#3207, #8018).
- **Environment-specific path bugs**: WSL file URIs break Windows Terminal links (#8054), and `PI_CODING_AGENT_DIR` overrides are lost in resume messages (#8048).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-13

## Today's Highlights

The Qwen Code team shipped multiple releases today, headlined by `desktop-v0.2.1` which refactors default project memory to workspace scope and improves telemetry around session lifecycle. A critical bug fix `#8931` lands in the web-shell to enforce prompt-safe session navigation — preventing unintended prompt cancellation or replay — and was included across both the preview and nightly releases. The community is actively reporting on stability concerns: a regression in image handling since v0.21.2, long-running task execution issues in the shell, and significant gaps in the Anthropic provider wire as compared to OpenAI.

---

## Releases

| Version | Highlights |
|---|---|
| **[v0.21.11-preview.0](https://github.com/QwenLM/qwen-code/releases)** | Fix: Web-shell prompt-safe session navigation (#8931); chore: session continuation admission logging |
| **[v0.21.10-nightly.20260812](https://github.com/QwenLM/qwen-code/releases)** | Same web-shell navigation fix and logging improvements |
| **[desktop-v0.2.1](https://github.com/QwenLM/qwen-code/releases)** | Refactor: default project memory defaults to workspace scope (#8856); telemetry: session lifecycle alignment |
| **[desktop-v0.2.0](https://github.com/QwenLM/qwen-code/releases)** | Fix: stabilize transcript history pagination (#8914); feature: share session catalog across workspaces |
| **dsw-eas-smoke-20260812** | Non-production infrastructure smoke build; no SWE score published (baseline: v0.21.2) |

---

## Hot Issues (10 Noteworthy)

1. **[#7040 — RFC: Reliable auto-memory recall](https://github.com/QwenLM/qwen-code/issues/7040)**  
   *P2, Feature Request, Core/Memory*  
   The most-discussed open item (10 comments) with active implementation status. Two of three PRs are in review; recall delivery telemetry is merged. Community is watching this closely for quality of recall precision and multilingual evaluation.

2. **[#8963 — Shell can't run long tasks ("不能自动运行")](https://github.com/QwenLM/qwen-code/issues/8963)**  
   *P2, Bug, Shell*  
   Users report that Python scripts or long commands simply hang in both `yolo` and `auto` modes. The author compares unfavorably to Kimi Code and requests a "blind accept" mode for long-running jobs. Strong sentiment in the comments — a usability blocker for automation workflows.

3. **[#8957 — Qwen Code crashes on image load since v0.21.2](https://github.com/QwenLM/qwen-code/issues/8957)**  
   *P2, Regression, Core*  
   A clear regression: v0.21.1 works, v0.21.2+ instantly crashes when reading images. 8 comments, need-retesting status. Likely related to recent content-generation refactors.

4. **[#8678 — Session restore timeout drops current session](https://github.com/QwenLM/qwen-code/issues/8678)**  
   *P1, Bug, Session Management*  
   Large session restores that time out can lose the active session. PR1 is merged (timeout contract + observability); the remaining work is still in review. High priority due to data-loss implications.

5. **[#8562 — tmux screen flicker via SSH](https://github.com/QwenLM/qwen-code/issues/8562)**  
   *P2, UI/Rendering (Linux via tmux)*  
   Multiple reports of screen flicker inside tmux when interacting with the CLI over SSH from macOS iTerm2. User attempted self-diagnosis with Qwen 3.8 Max and narrowed it to a Qwen Code version regression.

6. **[#8097 — Background agent coordination gap](https://github.com/QwenLM/qwen-code/issues/8097)**  
   *P2, Multi-Agent Core*  
   Running multiple Explore subagents in background leads to duplicate work, premature completion, and broken `send_message` mid-flight. A design-level issue that hints at deeper architectural constraints in the multi-agent runtime.

7. **[#8897 — `--approval-mode` and `--auth-type` missing from `--help`](https://github.com/QwenLM/qwen-code/issues/8897)**  
   *P2, CLI Bug*  
   Both flags are functional but undocumented in help output. Minor but symptomatic of CLI documentation drift.

8. **[#9016 — Vertex AI ADC auth broken](https://github.com/QwenLM/qwen-code/issues/9016)**  
   *P2, Auth*  
   Application Default Credentials cannot be used with Vertex AI — an API key is required and any provided key breaks ADC. A hard blocker for GCP users with service-account-only environments.

9. **[#9005 — Anthropic wire lacks stream-safety protections present in OpenAI wire](https://github.com/QwenLM/qwen-code/issues/9005)**  
   *P1, Content Generation*  
   Companion issue to the Anthropic SDK being pinned to an outdated `^0.36.1` (Jan 2025). Community concerns center on robustness parity between the two provider paths.

10. **[#8979 — MAX_TOKENS recovery corrupts transcript on `--resume`](https://github.com/QwenLM/qwen-code/issues/8979)**  
    *P2, Session Management*  
    After a MAX_TOKENS output recovery, the durable JSONL transcript diverges from in-memory history; `--resume` rehydrates duplicated turns. Data-integrity issue for long sessions.

---

## Key PR Progress (10 Important)

1. **[#8931 — fix(web-shell): Prompt-safe session navigation](https://github.com/QwenLM/qwen-code/pull/8931)**  
   Merged. Prevents session switching from canceling or replaying the active prompt — shipped in both v0.21.11-preview.0 and nightly.

2. **[#8874 — feat(web-shell): Workspace file uploads](https://github.com/QwenLM/qwen-code/pull/8874)**  
   Open. Drag-and-drop file uploads in the composer with progress, cancellation, and automatic conflict renaming.

3. **[#8856 — refactor(serve): Default project memory to workspace scope](https://github.com/QwenLM/qwen-code/pull/8856)**  
   Merged in desktop-v0.2.1. Aligns memory defaults to workspace boundaries — a safer default for multi-project environments.

4. **[#8905 — feat(serve): Adaptive live-journal cap growth](https://github.com/QwenLM/qwen-code/pull/8905)**  
   Open. In-flight turns that outgrow per-session journal caps now trigger cap doubling before truncating replay — reduces session history loss on long turns.

5. **[#8914 — fix(web-shell): Stabilize transcript pagination](https://github.com/QwenLM/qwen-code/pull/8914)**  
   Merged in desktop-v0.2.0. Fixes flaky transcript history loading in long sessions.

6. **[#8978 — feat(serve): No-op on empty channel set](https://github.com/QwenLM/qwen-code/pull/8978)**  
   Open. `qwen serve --channel all` now gracefully no-ops instead of exiting(1) and taking down the daemon; restores only previously-active channels.

7. **[#8972 — feat(core): Workflow agent directory pinning + extended bounds](https://github.com/QwenLM/qwen-code/pull/8972)**  
   Open. Allows workflow subagents to pin a working directory and outlive default run bounds — a meaningful step for long-running workflow agents.

8. **[#8971 — fix(web-shell): Retain manual session names after /clear](https://github.com/QwenLM/qwen-code/pull/8971)** (issue #8977)  
   Open. Manual session labels in Web Shell survive `/clear` instead of being replaced by auto-titles.

9. **[#9003 — fix(sdk): Support "auto" permission mode](https://github.com/QwenLM/qwen-code/pull/9003)**  
   Open. Python and Java SDKs now accept `auto`, aligning with CLI and TypeScript SDK.

10. **[#9007 — fix(serve): Bound ACP HTTP pre-attach buffers by bytes](https://github.com/QwenLM/qwen-code/pull/9007)**  
    Open. Replaces entry-count bounds with byte-based caps for pre-attach buffering — addresses memory-spike risk on large ACP payloads.

---

## Feature Request Trends

1. **Memory reliability & auto-recall (#7040, #8357)** — The community is pushing hard for deterministic, high-quality memory recall with telemetry. Manual `/dream` guard ships in #8357; RFC #7040 is the umbrella.

2. **Long-running / unattended task execution (#8963, #8972)** — Users want the shell to handle multi-hour or multi-day jobs without hanging — including a "blind accept" mode and workflow agents that can outlive default bounds.

3. **Channel and session lifecycle control (#8978, #8927)** — Operators want graceful no-op behavior on empty channels and per-channel `sessionRotation` to bound session reuse.

4. **Desktop app consolidation (#8596)** — Deprecate the Electron desktop app; make Tauri shell the single desktop client. Community-aligned with the recent desktop releases.

5. **Multi-agent coordination hardening (#8097)** — Subagent communication via `send_message` needs to be non-interactive-safe and avoid duplicate work.

---

## Developer Pain Points

- **Provider wire parity**: The Anthropic path repeatedly lags behind OpenAI — missing stream-safety protections (#9005), outdated SDK pin, and model-ID parsing gaps (#8584). For proxy users, this is a daily friction point.
- **Regression sensitivity in core paths**: Image-load crashes (#8957), MAX_TOKENS transcript divergence (#8979), and tmux flicker (#8562) all regressed recently, suggesting test gaps in the v0.21.x series.
- **Long task execution fragility**: Shell hangs on long-running commands, no blind-accept mode, and session-restore timeouts that drop sessions (#8678) — all point to reliability issues at the edges of session lifecycle management.
- **CLI & SDK inconsistency**: Flags accepted but undocumented (#8897); SDK rejects `permission_mode="auto"` while the CLI supports it (#9002) — a class of "surface drift" bugs between CLI, SDKs, and docs.
- **Authentication friction**: Vertex AI ADC incompatibility (#9016) reveals that auth backends are not uniformly tested across provider-specific credential flows.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-13

## Today's Highlights
The project continues its transition from the legacy `deepseek-tui` npm package to the **CodeWhale** product identity (v0.9.6), with maintainers harvesting several community PRs that were blocked only by CI base drift. Notable activity includes a significant **v0.9.5 regression** where Auto-Review mode silently blocks all Bash/write operations, plus an active community discussion on the correct Chinese translation of "Constitution" in project documentation, reflecting the project's i18n maturity.

## Releases
**[v0.9.6](https://github.com/Hmbown/CodeWhale/releases)** — The release formalizes **Codewhale** as the public product name from Shannon Labs. The `codewhale` command, npm package, and release-asset names remain lowercase technical identifiers. The legacy npm package `deepseek-tui` is deprecated and receives no further releases, with migration guidance for users coming from v0.8.x legacy `deepseek`/`d` commands.

## Hot Issues
1. **[#4949 — Chinese Translation of "Constitution"](https://github.com/Hmbown/CodeWhale/issues/4949)** — 9 comments. Community debate on whether "宪法", "协作准则", or another term best translates "Constitution" in Chinese docs. The PR author argues "宪法" conveys foundational authority but others worry about political sensitivity. Active bilingual discussion.

2. **[#4959 — Proposed 'stop' Command](https://github.com/Hmbown/CodeWhale/issues/4959)** — 8 comments. In YOLO/autonomous mode, text commands like `+ stop` are ignored. Request for a mechanical `/stop` command and runtime STOP-word intercept for reliable tool-call blocking.

3. **[#5316 — EPIC-005: TUI Crate Decomposition](https://github.com/Hmbown/CodeWhale/issues/5316)** — 5 comments. Umbrella epic tracking the staged decomposition of the TUI into separate crates. All sub-epics and FEATs report here; part of a larger architectural cleanup.

4. **[#5323 — Auto-Review Mode Regression](https://github.com/Hmbown/CodeWhale/issues/5323)** — 3 comments. **Critical regression in v0.9.5:** Auto-Review mode now silently blocks every Bash call and write operation with "destructive action requires explicit review," instead of auto-approving as in v0.8.x/v0.9.x earlier. High community impact.

5. **[#5209 — File Edit Tool Fake Success](https://github.com/Hmbown/CodeWhale/issues/5209)** — 4 comments. The `File` tool's `action=edit` accepts wrong parameter names (e.g., `new_str` instead of `replace`), returns fake success, and requires 3–5x re-edits per location. Reliability issue affecting agent workflows.

6. **[#5034 — Provider Switch Retains Unrelated Default Model](https://github.com/Hmbown/CodeWhale/issues/5034)** — 5 comments. Switching to OpenAI can leave `gpt-5.5` inherited from a different route. Provider/model resolution not updated coherently. Closed as fixed.

7. **[#5097 — CodeWhale Not "Official" DeepSeek Agent](https://github.com/Hmbown/CodeWhale/issues/5097)** — 5 comments. A YouTuber claims Reasonix is DeepSeek's official coding agent, sparking community discussion about official status. Closed.

8. **[#4650 — v0.9.1 Completion Board & Release Gate](https://github.com/Hmbown/CodeWhale/issues/4650)** — 4 comments. Long-running release-blocker epic covering final integration evidence, local dogfood, and non-publishing fan-in board. Still open with multiple labels.

9. **[#5322 — Wide Terminal Output Regression](https://github.com/Hmbown/CodeWhale/issues/5322)** — 2 comments. In v0.9, transcript/output area is capped at max width instead of filling wide terminals (worked in v0.8.65). Cosmetic but noticeable UX regression.

10. **[#5000 — Interrupted Assistant Output Not Durable](https://github.com/Hmbown/CodeWhale/issues/5000)** — 3 comments. Interrupted assistant text is displayed locally but absent from authoritative session state, causing inconsistency for subsequent model turns. Closed.

## Key PR Progress
1. **[#5328 — Command Contract Crate Boundary](https://github.com/Hmbown/CodeWhale/pull/5328)** — Part of EPIC-005/006 staged TUI command decomposition. Prototypes command migration shapes with facets and shared types, no production rewiring yet.

2. **[#5339 — Suppress Child-Owned Shell Completions](https://github.com/Hmbown/CodeWhale/pull/5339)** — Filters child-owned background shell completion events from parent model stream; preserves unowned completions and task visibility. Closes #5325.

3. **[#5333 — Pin Host Terminal as Always-On-Top Mini Window](https://github.com/Hmbown/CodeWhale/pull/5333)** — Maintainer harvest of community PR #5318 (SparkofSpike). Adds PiP capability: shrink terminal to 640x400 and pin on top via `/pin` or context menu. First v0.9.7 contributor integration.

4. **[#5330 — Separate Snapshot Reads from Crash Recovery](https://github.com/Hmbown/CodeWhale/pull/5330)** — Maintainer harvest of #5320 (h3c-hexin). Adds `load_session_snapshot` for side-effect-free reads and `recover_session_for_resume` returning repair statistics.

5. **[#5336 — MCP: Omit nextCursor When No More Pages](https://github.com/Hmbown/CodeWhale/pull/5336)** — Fixes #5335. `serve --mcp` returned `"nextCursor": null`, which is invalid per MCP spec (must be string or absent). Strict clients like Claude Code reject the shape.

6. **[#5334 — Retire Stale zh-Hant Partial-Pack Declaration](https://github.com/Hmbown/CodeWhale/pull/5334)** — PR #5143 brought zh-Hant to full parity, but five surfaces still describe it as partial — including two user-facing strings in `/config` help and settings schema.

7. **[#5332 — Register OrcaRouter as Named Provider](https://github.com/Hmbown/CodeWhale/pull/5332)** — Maintainer harvest of #5321 (XiaoHuo888-hue). Wires OrcaRouter (OpenAI-compatible gateway, `sk-orca-` keys, 150+ models) like the existing OpenRouter provider.

8. **[#5329 — Move lru to 0.18, Unpin ratatui-core](https://github.com/Hmbown/CodeWhale/pull/5329)** — Fixes RUSTSEC-2026-0253: `lru` 0.16.4's `LruCache::pop()` is panic-unsafe with dangling list pointers. Restores green main gate for cargo-deny.

9. **[#5327 — Interactive Extensions Manager](https://github.com/Hmbown/CodeWhale/pull/5327)** — Adds localized interactive `/plugin` and `/plugins` manager with digest-bound bundle lifecycle controller. Legacy executable tools remain as read-only inventory.

10. **[#5331 — Copy Messages Without Visual Rails](https://github.com/Hmbown/CodeWhale/pull/5331)** — Maintainer harvest of #5319 (XhesicaFrost, closes #5314). Copies canonical source content instead of rendered Ratatui lines, removing `●` glyph and `▏` rail decorations from context-menu copies.

## Feature Request Trends
- **Reliable interruption/control**: Multiple requests for a mechanical `/stop` command and STOP-word intercept in autonomous/YOLO modes (#4959, #5267).
- **Multi-provider key management**: Users want per-provider API keys saved separately rather than a single overwriting key slot (#5250), plus custom provider configuration modeled after Kimi Code (#4660).
- **Persistent agent state**: Long-running sessions need durable state and signed compressed KV cache capsules for cost/latency continuity (#2904).
- **Unified task surface**: One operator-facing list of all running background work — shells, subagents, Fleet workers, workflows (#5270).
- **Comprehensive i18n**: Community-driven localization including dictionary spine for all routed locales, zh-Hant parity, and Chinese terminology debates (#5337, #5334, #4949).
- **Session recovery/restore**: Prompt-scoped file restoration from prior turns and durable interrupted-output representation (#5272, #5000).

## Developer Pain Points
- **CI base-drift friction**: Multiple community PRs fail CI only due to stale base (old runtime-contract measurements, stale `release-credits.ts` parity), requiring maintainer harvests since fork pushes are declined — a process bottleneck for contributors.
- **Silent tool misbehavior**: The `File` edit tool accepting wrong parameter names and returning fake success (#5209) erodes trust and wastes agent cycles.
- **v0.9.5 regressions**: Auto-Review silently blocking all Bash/writes (#5323) and output area not filling wide terminals (#5322) frustrate users upgrading from v0.8.x.
- **Configuration discoverability**: Provider/model resolution not updated coherently on switch (#5034), API keys persisting only in repo-local plaintext (#5047), and Windows flag-parsing bugs (#4564) create setup friction.
- **Copy/UX polish**: Context-menu copy including rail decorations (#5314) and stale "Space to expand" hints (#5291) are small but frequent papercuts.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*