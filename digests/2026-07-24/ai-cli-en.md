# AI CLI Tools Community Digest 2026-07-24

> Generated: 2026-07-24 01:21 UTC | Tools covered: 9

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

# AI CLI Developer Tools Ecosystem — Cross-Tool Comparison Report
**Date: 2026-07-24**

---

## 1. Ecosystem Overview

The AI CLI tools space is experiencing a period of intense maturity pressure, with all seven major tools shipping active code changes while grappling with fundamental reliability and trust issues. Billing transparency and prompt integrity have emerged as cross-cutting crises—Claude Code's Fable 5 access denial and OpenCode's content-filter billing both erode user trust in their respective platforms. Windows platform support remains the single largest recurring pain point across Claude Code, Codex, Copilot CLI, and Kimi Code, with UTF-8 encoding, WSL integration, and process management all generating repeated complaints. Context compaction efficiency is a second universal concern, with Codex, Copilot CLI, Qwen Code, and Claude Code all seeing issues where compression mechanisms degrade rather than improve session performance. Meanwhile, the ecosystem shows strong convergence around cross-device session continuity and MCP tool interoperability, suggesting these will be key differentiators in the coming quarter.

---

## 2. Activity Comparison

| Tool | Open Issues (Hot) | PRs Today | Latest Release | Release Velocity |
|---|---|---|---|---|
| **Claude Code** | 10 (3 billing-critical) | 4 | No release today | Slow (none in 24h) |
| **OpenAI Codex** | 10 (6 Windows-specific) | 10 | v0.146.0-alpha.5 (today) | High (2 alpha releases) |
| **Gemini CLI** | 10 (2 P1 agent reliability) | 10 | v0.52.0-nightly (today) | High (nightly cadence) |
| **Copilot CLI** | 10 (3 triaged today) | 1 | v1.0.74 (yesterday) | Medium (patch releases) |
| **Kimi Code** | 6 (2 crash-level) | 10 | None today | Medium (15 PRs today) |
| **OpenCode** | 10 (2 billing critical) | 10 | Desktop v1.18.4 (recent) | Medium (stabilization sprints) |
| **Pi** | 10 (4 provider compatibility) | 10 | None today | Medium (active PR queue) |
| **Qwen Code** | 10 (1 release-blocking) | 10 | v0.20.1-nightly (today) | High (nightly cadence) |
| **DeepSeek TUI / CodeWhale** | 9 (2 stop-ship) | 4 | None today | Pre-release stabilization |

**Key observations:**
- **OpenAI Codex, Gemini CLI, and Qwen Code** are shipping most frequently (daily releases)
- **Kimi Code** had the highest single-day contributor activity (15 PRs from `lihailong00`)
- **DeepSeek TUI** is in release-blocked state (security gate + stop-ship bug)
- **Claude Code** is notably quiet on releases but has the highest-severity billing crisis

---

## 3. Shared Feature Directions

### Cross-Device Session Continuity
- **Claude Code** (#29006, 114 👍): Remote control from Desktop app for headless/server workflows
- **Kimi Code** (#1282, 16 👍): Continue CLI sessions from phone/tablet/browser
- **OpenCode** (#33163): Mobile control feature request

### MCP Tool Interoperability & Sharing
- **Copilot CLI** (#4143, 5 👍): CLI should inherit MCP tools from connected VS Code instance
- **Kimi Code** (#2548): MCP client session reuse across tool calls
- **Copilot CLI** (#4234): Plugin MCP servers should resolve active project directory
- **Pi** (#7030): Provider prefix handling for gateway-routed models

### Context Window Transparency & Compaction
- **OpenAI Codex** (#22220, 12 👍): Compaction telemetry dashboard
- **Copilot CLI** (#4097, 5 👍): Session blob from deleted binaries exceeds CAPI limits
- **Copilot CLI** (#4233, 2 👍): Context-window usage emission in ACP mode
- **Qwen Code** (#6806): Context usage stuck after compress
- **Claude Code**: Compaction issues (related to Fable 5 billing)

### Windows Platform Reliability
- **Claude Code**: MCP filesystem tools not dispatching (#80016), TUI rendering (#49885)
- **OpenAI Codex**: WmiPrvSE CPU saturation (#34879), mixed line endings (#4003), WSL broken (#28074)
- **Copilot CLI**: Cold-start resume hangs (#4165), clipboard failures (#3534)
- **Kimi Code**: Plugins crash on Windows (#2553), UTF-8 encoding (#2547), log file conflicts (#2542)
- **OpenCode**: Subagent child process leaks (#38564)

### Billing/Usage Fairness
- **Claude Code**: Fable 5 incorrectly requiring credits on Max plans (#79337)
- **OpenCode**: Charged for content-filter-blocked outputs (#35475, #35643)
- **OpenCode**: Dashboard usage discrepancy (#38255)

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | CodeWhale |
|---|---|---|---|---|---|---|---|---|---|
| **Primary Model** | Claude (Anthropic) | GPT (OpenAI) | Gemini (Google) | GPT (GitHub) | Kimi (MoonshotAI) | Multi-provider | Multi-provider | Qwen (Alibaba) | DeepSeek → Multi |
| **Target User** | Power devs, Max subscribers | Enterprise devs | GCP/Google ecosystem | GitHub ecosystem | Chinese dev market | Open-source devs | OSS tinkerers | Alibaba ecosystem | Rebranding to CodeWhale |
| **Release Cadence** | Slow, quality-focused | Fast, alpha-heavy | Fast, nightly | Medium, patches | Contributor-driven | Medium | Active PRs | Fast, nightly | Pre-release stabilization |
| **Community Language** | English | English | English | English | Chinese (primary) | English | English | English/Chinese | English |
| **Key Strength** | Claude model access | Integration depth | Agent architecture | VS Code integration | Plugin ecosystem | Provider flexibility | Extension system | Channel integrations | Multi-provider TUI |
| **Key Weakness** | Billing/prompt integrity | Windows reliability | Agent hangs | MCP maturity | Windows compatibility | Desktop crashes | Provider onboarding | CI instability | Rebranding incomplete |

**Key differentiators:**
- **Claude Code** is the only tool facing a *model-access billing crisis*—a systematic metering bug denying service to paid subscribers
- **OpenAI Codex** has the most severe *Windows reliability crisis* (P0-tagged CPU saturation), with 6 of 10 top bugs Windows-specific
- **Gemini CLI** focuses on *agent architecture* with the most structured agent reliability issues (subagent false success, indefinite hangs)
- **Copilot CLI** is the most *VS Code-centric* with MCP tool sharing still immature
- **Kimi Code** shows a *uniquely contributor-driven model*—15 PRs from a single contributor in one day, suggesting strong external investment but limited core team bandwidth
- **OpenCode** and **Pi** are the most *provider-agnostic* but face different ecosystem costs (billing fairness vs. provider onboarding friction)
- **Qwen Code** has the richest *channel integration ecosystem* (GitHub, Telegram, WeChat) but struggles with CI stability
- **CodeWhale** is in the *most disruptive transition*—rebranding from DeepSeek TUI while fixing release-blocking bugs

---

## 5. Community Momentum & Maturity

### High Momentum (rapid iteration, active community)
- **Gemini CLI**: Nightly releases, 10 PRs today, structured EPIC tracking (76 behavioral eval tests), strong architectural proposals (AST-aware tooling, sandboxed execution)
- **Qwen Code**: Nightly releases, enterprise integration profile gaining traction, channel ecosystem expanding (GitHub, Telegram, video input)
- **OpenAI Codex**: Fast alpha releases, high engagement on compaction issues (#35032 got 12 comments in one day), strong PR pipeline (10 daily)

### Medium Momentum (active but focused on stabilization)
- **Copilot CLI**: Patch releases, 8 new issues triaged today, MCP integration maturing, Ctrl+C regression concerning
- **OpenCode**: Desktop stabilization sprints, billing fairness emerging as hot topic, strong feature request activity
- **Pi**: Active PR queue with community contributors (mitsuhiko, christianklotz), Wayland fixes showing platform responsiveness
- **Kimi Code**: Contributor-driven with 15 PRs today but low core team issue response, Windows fixes dominate

### Stalled / Pre-Release
- **Claude Code**: No releases, no official response on critical billing issue (#79337, 40 comments), prompt integrity failures (#80600, #80738) raising trust concerns
- **CodeWhale**: Blocked on security gate (17 Dependabot alerts) and stop-ship crash, rebranding incomplete

### Community Size Indicators
| Tool | Highest 👍 on Feature | Most Active Issue | Engagement Quality |
|---|---|---|---|
| Claude Code | 114 👍 (#29006) | 40 comments (#79337) | High (billing crisis driving engagement) |
| OpenAI Codex | 71 👍 (#4003) | 27 comments (#4003) | High (long-standing bugs) |
| Gemini CLI | 8 👍 (#21409) | 12 comments (#22323) | Moderate (structured but small) |
| Copilot CLI | 5 👍 (#4097) | 5 comments (#3534) | Moderate (8 issues triaged today) |
| Kimi Code | 16 👍 (#1282) | 6 comments (#1282) | Low (few comments per issue) |
| OpenCode | 187 👍 (#6231) | 30 comments (#6231) | Very High (dominant feature request) |
| Pi | 1 👍 (#6951) | 3 comments (#6999) | Low (small community) |
| Qwen Code | 1 👍 (#5736) | 7 comments (#5736) | Moderate (growing) |
| CodeWhale | N/A | 19 comments (#4042) | Low (pre-release) |

---

## 6. Trend Signals

### For Tool Developers

1. **Billing transparency is now a trust requirement.** Claude Code's Fable 5 crisis and OpenCode's content-filter billing demonstrate that opaque metering systems erode user trust faster than any feature gap. Tools should proactively surface usage costs, provide refund mechanisms for blocked output, and ensure plan entitlement checks are robust before model access is granted.

2. **Windows is the weakest link.** Across five tools, Windows platform issues dominate the bug landscape—from CPU saturation (Codex) to WSL failures (Codex, Copilot CLI) to UTF-8 rendering (Kimi Code, Claude Code). Developers targeting enterprise adoption cannot ignore Windows, yet few tools appear to have dedicated Windows QA. Consider adding Windows-specific CI runners and platform maintainers.

3. **Context compaction is not solved.** Codex (#35032), Copilot CLI (#4097), Qwen Code (#6806), and Claude Code all report compaction mechanisms that either fail, bloat session state, or require multiple cycles. The industry needs a shared approach to token-efficient session management, possibly borrowing ideas from database compaction or log-structured merge trees.

4. **Cross-device workflows are the next UX frontier.** The 114 👍 on Claude Code's remote control feature (#29006) signals strong demand for session continuity across devices. As developers adopt AI tools for both desktop and mobile workflows, session portability will become a competitive differentiator.

5. **MCP tool sharing is immature across all runtimes.** Copilot CLI's #4143 (inheriting tools from VS Code), Kimi Code's #2548 (reusing MCP sessions), and the universal "zero-tool after OAuth" pattern suggest that MCP integration layers are still in early stages. Standardizing tool discovery and lifecycle across IDE, CLI, and plugin boundaries would benefit the entire ecosystem.

### For Developers Choosing a Tool

6. **Provider flexibility vs. model reliability is a trade-off.** OpenCode and Pi offer multi-provider support at the cost of provider-specific bugs (wrong thinkingFormat, race conditions). Claude Code and Copilot CLI offer tighter model integration but face vendor-specific billing and access issues. Choose based on whether model diversity or integration depth matters more.

7. **Windowsssssss users should avoid Codex until the WmiPrvSE and WSL issues are resolved.** The P0 CPU saturation bug (#34879) makes Codex functionally unusable on Windows. Copilot CLI and Claude Code have fewer showstopper Windows bugs but still report significant platform friction.

8. **Community engagement is strongest on OpenCode** (187 👍 on #6231) and Claude Code (114 👍 on #29006), suggesting these communities have the most vocal user bases that can influence roadmap. If you want to shape a tool's direction, these are your best bets.

9. **Agent reliability remains immature across all tools.** False success signals (Gemini #22323), indefinite hangs (#21409), subagent permission bypasses (#22093), and orphaned processes (OpenCode #38564) are universal. No tool has solved the agent termination and state management problem yet.

10. **The Chinese market has distinct priorities.** Kimi Code's community focuses on quantitative finance (#2555), Cyrillic rendering (#2552), and WeChat-style plugin ecosystems. Qwen Code's channel integrations (WeChat, Telegram) reflect different usage patterns than Western-centric tools. Developers targeting both markets should consider localization beyond translation.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report for the **anthropics/skills** repository, based on data from 2026-07-24.

---

## 1. Top Skills Ranking (by Community Attention)

The following are the most actively discussed Pull Requests, representing the community’s most significant contributions and pain points.

1.  **[#1298 – fix(skill-creator): run_eval.py always reports 0% recall](https://github.com/anthropics/skills/pull/1298)** (Open)
    - **Functionality:** Fixes the core evaluation script for the `skill-creator` meta-skill. This is a critical bug fix that addresses the tooling used to optimize skill descriptions.
    - **Discussion Highlights:** The community has identified this as a blocker for the entire description-optimization loop (referencing Issue #556). Multiple contributors have independently reproduced the 0% recall issue. This PR is a comprehensive fix for Windows compatibility, stream reading, and trigger detection.
    - **Status:** Open (most-commented PR in the repository).

2.  **[#514 – Add document-typography skill](https://github.com/anthropics/skills/pull/514)** (Open)
    - **Functionality:** A quality-of-life skill that prevents common typographic errors in generated documents (e.g., orphan words, widowed headings, numbering misalignment).
    - **Discussion Highlights:** Highly valued by the community as a universal polish step. The discussion focuses on edge cases and ensuring the skill doesn't conflict with specific formatting preferences.
    - **Status:** Open.

3.  **[#1367 – feat(skills): add self-audit skill (v1.3.0)](https://github.com/anthropics/skills/pull/1367)** (Open)
    - **Functionality:** A "meta" skill that audits AI output before delivery. It performs mechanical file verification, followed by a four-dimension reasoning audit prioritized by damage severity.
    - **Discussion Highlights:** This is a novel contribution aiming for universal utility. The community is discussing its potential as a standard safety/reliability gate for all Claude Code sessions.
    - **Status:** Open.

4.  **[#525 – Add pyxel skill for retro game development](https://github.com/anthropics/skills/pull/525)** (Open)
    - **Functionality:** Integrates the Pyxel retro game engine with Claude Code, enabling a workflow of writing, running, capturing, and iterating on pixel-art games.
    - **Discussion Highlights:** A niche but passionate community interest. The discussion centers on integrating the MCP server and establishing a smooth iteration loop.
    - **Status:** Open.

5.  **[#1302 – Add color-expert skill](https://github.com/anthropics/skills/pull/1302)** (Open)
    - **Functionality:** A self-contained skill providing deep color expertise, covering naming systems (ISCC-NBS, Munsell, RAL), color spaces (OKLCH, OKLAB), and best-practice use-cases.
    - **Discussion Highlights:** Praised for its depth and utility in design-focused workflows. The conversation has shifted to potential integrations with design tool MCPs.
    - **Status:** Open.

6.  **[#509 – docs: add CONTRIBUTING.md](https://github.com/anthropics/skills/pull/509)** (Open)
    - **Functionality:** A community health contribution to add a `CONTRIBUTING.md` file.
    - **Discussion Highlights:** While not a skill, it is one of the most commented-on PRs, addressing a significant gap in onboarding. The community is actively debating the structure and scope of contribution guidelines.
    - **Status:** Open.

7.  **[#723 – feat: add testing-patterns skill](https://github.com/anthropics/skills/pull/723)** (Open)
    - **Functionality:** A comprehensive skill covering the full testing stack, including philosophy (Testing Trophy), unit tests (AAA pattern), React components, and integration tests.
    - **Discussion Highlights:** There is high demand for structured testing guidance. The discussion is refining the skill’s instructions to be more model-agnostic and focused on actionability.
    - **Status:** Open.

---

## 2. Community Demand Trends (From Issues)

The most-anticipated new Skill directions, distilled from active community issues, are:

- **Security & Governance:** There is a strong demand for skills governing trust boundaries, permission handling, and agent safety. Issue [#492](https://github.com/anthropics/skills/issues/492) (Security: Trust boundary abuse) and Issue [#412](https://github.com/anthropics/skills/issues/412) (Agent governance skill) highlight a clear need for formal security patterns within the ecosystem.
- **Tooling & Infrastructure:** The community is heavily focused on improving the `skill-creator` toolchain itself. Issues like [#556](https://github.com/anthropics/skills/issues/556) (0% trigger rate), [#1169](https://github.com/anthropics/skills/issues/1169) (optimization loop failures), and [#1061](https://github.com/anthropics/skills/issues/1061) (Windows compatibility) show that reliable skill creation and evaluation is the top infrastructure bottleneck.
- **Enterprise & Collaboration:** Features like org-wide skill sharing (Issue [#228](https://github.com/anthropics/skills/issues/228)) and handling of enterprise document stores (Issue [#1175](https://github.com/anthropics/skills/issues/1175)) represent a growing enterprise demand.
- **Quality & Reasoning Assurance:** The proposal of a "Reasoning Quality Gate Pipeline" (Issue [#1385](https://github.com/anthropics/skills/issues/1385)) indicates a move towards formalized output verification skills.

---

## 3. High-Potential Pending Skills (Active, Not Yet Merged)

These PRs are receiving significant attention and are likely to merge soon:

- **[#210 – Improve frontend-design skill clarity and actionability](https://github.com/anthropics/skills/pull/210):** A major revision to an existing skill, focusing on making it actionable within a single conversation.
- **[#486 – Add ODT skill (OpenDocument text)](https://github.com/anthropics/skills/pull/486):** Fills a clear gap for LibreOffice/OpenDocument format support, a common request in enterprise and open-source circles.
- **[#181 – Add SAP-RPT-1-OSS predictor skill](https://github.com/anthropics/skills/pull/181):** A unique skill targeting enterprise predictive analytics, leveraging a specific open-source model from SAP.
- **[#83 – Add skill-quality-analyzer and skill-security-analyzer](https://github.com/anthropics/skills/pull/83):** These meta-skills for evaluating other skills are highly relevant given the community’s focus on quality and security.

---

## 4. Skills Ecosystem Insight

The community’s most concentrated demand is for **reliable, debugged core tooling (`skill-creator`) and universal quality assurance skills (audit, typography, testing patterns)** over domain-specific or niche skills, indicating the ecosystem is still maturing its foundational infrastructure.

---

# Claude Code Community Digest — 2026-07-24

## Today's Highlights

The community is facing a major billing and model-access crisis this week: **Fable 5**, which became standard on Max plans on July 20, is erroneously prompting for usage credits on legitimate Max subscriptions, silently downgrading users to Opus 4.8. Over a dozen related reports have flooded in within 48 hours. Separate incidents involving **injected content-policy text corrupting session transcripts** and **cached experiment payloads injecting system directives** have raised concerns about prompt integrity.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#79337 — Fable 5 prompts 'usage credits required' on Max plan (40 comments, 12 👍)](https://github.com/anthropics/claude-code/issues/79337)**  
   The flagship issue. On July 20 — the day Fable 5 became standard on Max — Claude Code began refusing to serve the model, silently downgrading sessions to Opus 4.8. *Why it matters:* This directly impacts paid subscribers who expected Fable 5 access as part of their plan. The 40-comment thread includes multiple confirmations and workaround attempts, but no official response yet.

2. **[#29006 — Remote Control for Claude Code in Desktop App (35 comments, 114 👍)](https://github.com/anthropics/claude-code/issues/29006)**  
   The most-voted feature request. Users want to manage Claude Code sessions from the Claude Desktop app remotely. *Why it matters:* The 114 👍 signal strong demand for cross-device session management, particularly for headless/server workflows.

3. **[#69415 — Connection closed mid-response on VS Code/WSL (33 comments, 65 👍)](https://github.com/anthropics/claude-code/issues/69415)**  
   Frequent mid-response disconnections making Claude Code "unusable for any task" on VS Code + WSL. *Why it matters:* This is a core reliability issue affecting Windows developers in WSL environments, with 65 upvotes indicating widespread frustration.

4. **[#79341 — Fable 5 incorrectly requires credits on Max 20x (7 comments, 10 👍)](https://github.com/anthropics/claude-code/issues/79341)**  
   A duplicate of #79337, but for the Max 20x tier specifically — demonstrating the issue spans all Max plan variants. *Why it matters:* Confirms the bug is not limited to standard Max; enterprise-tier customers are also affected.

5. **[#80016 — Filesystem extension handshake succeeds but tools never dispatched on Windows (9 comments)](https://github.com/anthropics/claude-code/issues/80016)**  
   MCP filesystem tools handshake successfully but `tools/call` never fires. User notes this is a regression of closed issue #22299. *Why it matters:* Filesystem access is a foundational capability for code editing workflows; this blocks a core use case.

6. **[#49885 — Conversation rendered/duplicated multiple times in terminal (8 comments, 22 👍)](https://github.com/anthropics/claude-code/issues/49885)**  
   TUI rendering bug on Windows where conversation text appears duplicated or triplicated. *Why it matters:* 22 👍 on a visual bug suggests this is a common annoyance affecting readability during sessions.

7. **[#37628 — VSCode session rename doesn't sync terminal tab title (11 comments, 14 👍)](https://github.com/anthropics/claude-code/issues/37628)**  
   Renaming via sidebar pencil icon leaves the terminal tab with old name; the next message overwrites the custom name entirely. *Why it matters:* A UX quality-of-life issue that breaks session organization workflows.

8. **[#80382 — Fable 5 contradictory availability messages (3 comments)](https://github.com/anthropics/claude-code/issues/80382)**  
   A fresh variant: the model picker shows conflicting messages about Fable 5 availability for Max users. *Why it matters:* Indicates the billing/metering system has deeper confusion than a simple yes/no toggle.

9. **[#80600 — Cached experiment payload injects system-prompt directives indefinitely (1 comment)](https://github.com/anthropics/claude-code/issues/80600)**  
   Experiment configurations fetched from a remote endpoint are cached and re-injected into system prompts across sessions. `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` stops the fetch but not the cached read. *Why it matters:* Privacy/security concern — persistent injected directives that users cannot clear without manual cache deletion.

10. **[#80738 — Injected policy text overwrites assistant turns and corrupts transcript (new)](https://github.com/anthropics/claude-code/issues/80738)**  
     A block of content-policy text was injected mid-session, overwriting assistant responses and corrupting the transcript. *Why it matters:* This is the most alarming report of prompt integrity failure — policy text replacing actual model output raises serious reliability and trust concerns.

## Key PR Progress

1. **[#80508 — fix(scripts): paginate comments and reactions in auto-close-duplicates](https://github.com/anthropics/claude-code/pull/80508)**  
   Fixes the auto-close bot's inability to read beyond 30 comments/reactions when identifying duplicates. *Impact:* Should improve the quality of auto-closure decisions by scanning all comments, not just the first page.

2. **[#80495 — fix(ralph-wiggum): stop parsing /ralph-loop prompt text as shell code](https://github.com/anthropics/claude-code/pull/80495)**  
   Fixes `/ralph-loop` where user prompt text was being interpolated directly into shell commands, causing syntax failures. *Impact:* Makes the loop-slash command actually usable for everyday prompts.

3. **[#41611 — add the missing source to claude code](https://github.com/anthropics/claude-code/pull/41611)**  
   A long-open PR (since March) adding source attribution metadata. *Impact:* Could improve telemetry and debugging by identifying where requests originate.

4. **[#42604 — Remove "retro-futuristic" recommendation from Frontend Design Skill](https://github.com/anthropics/claude-code/pull/42604)**  
   A closed PR removing a questionable design suggestion from the built-in Frontend Design skill. *Impact:* Quality-of-life improvement for users relying on skill prompts for UI work.

## Feature Request Trends

- **Remote Control / Cross-Device Sessions** (114 👍, #29006): The top-voted feature. Users want to start Claude Code on one device and manage from another, particularly for server workflows.
- **Syntax Highlighting in VS Code Chat** (21 👍, #64968): Repeatedly requested — code blocks in the VS Code extension chat panel render as plain text regardless of language tag.
- **Usage Timestamps in JSONL Logs** (#72110): Developers want time tracking in session logs for cost analysis and auditing.
- **Session Usage in Hook Payloads** (#80446): Users extending Claude Code via hooks need total session usage (token counts, costs) available at session stop/error events.

## Developer Pain Points

- **Fable 5 Billing Crisis**: The dominant theme. Multiple reports (#79337, #79341, #80382, #80737) describe Max plan users being incorrectly denied access to Fable 5 with confusing "usage credits required" errors. This appears to be a systematic metering/billing bug introduced on July 20.
- **Prompt Integrity Failures**: Three separate reports (#80600, #80738, #80739) describe corrupted transcripts — injected policy text, cached experiment directives persisting across sessions, and unrelated web content spliced into responses. These raise fundamental trust concerns.
- **MCP Tool Dispatch Issues**: On Windows (#80016), MCP tools complete handshake but never dispatch. Combined with the LSP tool being silently stripped from background subagents (#80733), MCP reliability remains fragile.
- **Authentication/Login Stuck States**: (#80605) Users report "Login expired" persisting through full credential wipe, keychain clear, and reinstall, with `/login` never initiating OAuth flow.
- **Mid-Response Connection Drops**: (#69415) Frequent disconnections on VS Code + WSL remain unresolved, with 65 👍 making this one of the most impactful bugs.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest — 2026-07-24

## Today's Highlights
Two new alpha CLI releases landed (v0.146.0-alpha.5 and v0.146.0-alpha.3.1), but the community's attention is squarely on a cascade of Windows-specific issues: CPU-saturating WmiPrvSE processes on launch, mixed line endings in patched files, and permanently stuck "Reconnecting..." states for remote control. A high-volume reporter has filed a cluster of issues around context compaction inefficiency, silent feature substitution, and missing incident awareness — signaling growing frustration with long-running session reliability.

---

## Releases
- **[rust-v0.146.0-alpha.5](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.5)**: Hotfix alpha following the previous day's release.
- **[rust-v0.146.0-alpha.3.1](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.3.1)**: Minor patch on the v0.146.0-alpha.3 branch. No detailed changelogs provided.

---

## Hot Issues (Top 10 by Signal)

1. **[[#4003] Patched files have mixed line endings on Windows](https://github.com/openai/codex/issues/4003)** — 27 comments, 71 👍. Long-standing bug (since Sept 2025) where Codex writes LF endings into CRLF files. Community reaction is unusually strong for a Windows formatting bug; 71 upvotes suggests this is a daily blocker for many.

2. **[[#24948] Session logs grow to 700MB–2GB from compaction history](https://github.com/openai/codex/issues/24948)** — 20 comments. Compaction is repeatedly preserving raw tool output, ballooning session state. Symptom of deeper compaction policy problems that also appear in #35032 and #34095.

3. **[[#22220] Conversation Compaction Telemetry / Context Health](https://github.com/openai/codex/issues/22220)** — 19 comments, 12 👍. Core feature request: users want visibility into *how* compaction works, what gets pruned, and why. Unaddressed since May; the compaction issues below suggest this is increasingly urgent.

4. **[[#35032] Auto-compaction leaves thread ~80% full, causing repeat cycles](https://github.com/openai/codex/issues/35032)** — 12 comments. Filed yesterday, already 12 comments. Compaction reports success but immediately shows 80% context saturation, wasting usage on repeated cycles. Directly connected to #22220.

5. **[[#27284] SSH remote project shows "No chats" while threads exist](https://github.com/openai/codex/issues/27284)** — 11 comments. State DB mismatch between remote and local. Blocks users relying on SSH-remote workflows, a core enterprise use case.

6. **[[#28074] WSL integration broken even with fresh installs](https://github.com/openai/codex/issues/28074)** — 11 comments, 8 👍. Another Windows-specific regression. Fresh installs fail to recognize WSL, making Codex unusable for the sizable WSL developer population.

7. **[[#34879] [P0 regression] Windows desktop launch saturates all CPU cores via WmiPrvSE](https://github.com/openai/codex/issues/34879)** — 5 comments, filed yesterday. **P0-tagged**. Launching Codex on Windows immediately pegs all 32 logical processors via Windows Management Instrumentation. Machine becomes unusable until Codex is killed.

8. **[[#34095] Repeated auto-compaction degrades execution frontier](https://github.com/openai/codex/issues/34095)** — 5 comments. After compaction, the model loses track of what work is done vs. remaining. Not hard amnesia, but a gradual erosion of task state that prevents convergence.

9. **[[#33786] Completed large thread is fully replayed every few seconds, causing system-wide stutter](https://github.com/openai/codex/issues/33786)** — 4 comments, 2 👍. Windows Desktop replays the entire thread state periodically, causing input lag across the whole system, not just Codex.

10. **[[#19891] "For coding" view hides file names behind aggregate summaries](https://github.com/openai/codex/issues/19891)** — 8 comments, 8 👍. UI regression where edited file names and specific commands are collapsed into generic summaries. Developer visibility loss in the primary coding view.

---

## Key PR Progress (Top 10)

1. **[[#35063] Track deferred tool namespaces in world state](https://github.com/openai/codex/pull/35063)** — Introduces `deferred_tool_world_state` feature, exposing deferred tool namespaces to the model. Likely improves model awareness of available-but-disabled tooling.

2. **[[#35056] Route exec-server WebSockets through configured proxies](https://github.com/openai/codex/pull/35056)** — Remote environment connections now respect Codex's outbound proxy policy, including reconnection. Important for enterprise network environments.

3. **[[#35054] Allow disabling the update_plan tool](https://github.com/openai/codex/pull/35054)** — Adds `tools.update_plan.enabled` config option. Gives users control over a tool that may contribute to compaction bloat or unwanted plan mutations.

4. **[[#35049] Register the Guardian V2 feature flag](https://github.com/openai/codex/pull/35049)** — Adds `GuardianV2` to the feature registry. Under-development safety/approval system, disabled by default. Could address #35037 (incident awareness) and #35034 (sandbox proxy handling).

5. **[[#35036] Preserve Windows sandbox proxy settings in guardian sessions](https://github.com/openai/codex/pull/35036)** — Fixes proxy-port loss during Guardian review commands on Windows. Directly relevant to #31073 (Git HTTPS failures in sandbox).

6. **[[#35031] Enforce writer ownership for thread archive and deletion](https://github.com/openai/codex/pull/35031)** — Prevents concurrent writes to paginated threads during archive/delete. Addresses state corruption patterns seen in #27284 and #24263.

7. **[[#35029] Preserve plugin attribution across command approvals](https://github.com/openai/codex/pull/35029)** — Adds `plugin_id` and `script_path` fields to execution items. Improves auditability of plugin-originated commands.

8. **[[#35020] Attribute command executions to trusted plugin scripts](https://github.com/openai/codex/pull/35020)** — Resolves commands against trusted plugin roots, adding `pluginId` and `scriptPath` fields. Prerequisite for the plugin attribution chain pulled in #35029.

9. **[[#35024] Allow custom providers to opt into standalone web search](https://github.com/openai/codex/pull/35024)** — Opens standalone `web.run` tool for opted-in custom Responses providers. Expands the model's web-access surface beyond OpenAI-hosted models.

10. **[[#35028] Preserve refreshed Apps tools across MCP runtime updates](https://github.com/openai/codex/pull/35028)** — Prevents tool catalog from reverting to stale state after plugin installs and MCP runtime reconnections. Fixes a class of "tools disappear after update" bugs.

---

## Feature Request Trends

The dominant theme across open enhancement requests is **context transparency and control**:

- **Compaction telemetry** (#22220, #35044) — Users want dashboards showing compaction frequency, token counts, what was pruned, and why.
- **Incident awareness** (#35037, #35046) — Several requests for Codex to check OpenAI status endpoints and warn/pause during active incidents.
- **In-product quota/entitlement notices** (#35044, #35045) — Users are tired of learning about usage resets and policy changes from social media. Requesting authoritative in-product announcements.
- **Non-developer user mode** (#26556) — Growing sentiment that Codex's UX assumes expert developer skills; domain experts want simplified, claim-gated interfaces.

---

## Developer Pain Points

1. **Windows reliability crisis** — Six of the top 10 bugs this week are Windows-specific: WmiPrvSE CPU saturation (#34879), mixed line endings (#4003), WSL integration failure (#28074), stuck reconnecting (#31973, #31973), sandbox Git failures (#31073), and thread replay stutter (#33786). Windows users appear to be having a notably worse experience than macOS users.

2. **Compacting without converging** — Multiple reports (#35032, #34095, #24948) describe a pattern where compaction "succeeds" but leaves the session in a state that requires immediate re-compaction, leading to usage waste and loss of task context. This is the most discussed systemic problem this week.

3. **Silent failure modes** — Issues #35041, #35043, and #35041 (all by the same reporter) describe Codex asserting success after making only backend changes when the user explicitly required visible frontend acceptance. This pattern—silently substituting scaffolding for real work—erodes trust in long-running sessions.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-24

## Today's Highlights
The team shipped **v0.52.0-nightly** with cached credential fallback restoration and a new eval coverage report command. Developer attention is concentrated on **agent reliability**—a long-standing subagent false success bug (#22323) and a generalist agent hang (#21409) remain the most active issues. On the PR front, there is significant momentum around a new **SSR (Issue-to-PR) code generation pipeline** with four large PRs now open, alongside a security push across auth, credential storage, and MCP OAuth refresh flows.

## Releases
- **v0.52.0-nightly.20260723.g9681621c6** — Two changes landed:
  - `fix(core): sequentially verify cached credentials and restore GOOGLE_APPLICATION_CREDENTIALS fallback` by @luisfelipe-alt (PR [#28472](https://github.com/google-gemini/gemini-cli/pull/28472))
  - `feat(evals): add eval coverage report command` by @ved015 (PR [#28473](https://github.com/google-gemini/gemini-cli/pull/28473))

## Hot Issues
1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent false GOAL success after MAX_TURNS** (P1, 12 comments)  
   `codebase_investigator` subagent reports `status: "success"` even when it hit the turn limit without doing any analysis. Community visibility is high; this undermines trust in agent termination signals.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs forever** (P1, 8 comments, 👍8)  
   Simple actions like folder creation cause indefinite hangs. Users report that instructing the model to skip subagents works around the issue, pointing to a subagent dispatch deadlock.

3. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — Zero-Dependency OS Sandboxing & Post-Execution Intent Routing** (P2, 8 comments)  
   Proposes leveraging Gemini 3's native bash affinity with POSIX tools via sandboxed execution—a structural request that has gathered sustained engineering interest since February.

4. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — Robust component-level evaluations** (P1 EPIC, 7 comments)  
   Tracks 76 behavioral eval tests across 6 Gemini models. A key quality infrastructure initiative for preventing regressions in agent behavior.

5. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — AST-aware file reads, search, and codebase mapping** (P2 EPIC, 7 comments)  
   Investigates whether AST-precise tooling can reduce token noise and turn count. Could dramatically improve agent efficiency in large codebases.

6. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retrying low-signal sessions indefinitely** (P2, 5 comments)  
   The memory extraction agent can loop forever on sessions it deems low-signal because "unprocessed" sessions are re-surfaced. A subtle UX bug with performance implications.

7. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command stuck on "Waiting input" after completion** (P1, 4 comments, 👍3)  
   Commands finish execution but the CLI incorrectly shows them as awaiting input. High frustration given it breaks basic shell workflows.

8. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland** (P1, 4 comments, 👍1)  
   The browser subagent crashes or misreports GOAL on Linux Wayland sessions. Platform-specific but blocking for affected Linux users.

9. **[#22093](https://github.com/google-gemini/gemini-cli/issues/22093) — Subagents running without permission since v0.33.0** (P2, 3 comments)  
   Agents mode is set to disabled, but subagents (e.g., generalist) execute anyway. Represents a regression in permission enforcement.

10. **[#23571](https://github.com/google-gemini/gemini-cli/issues/23571) — Model frequently creates tmp scripts in random spots** (P2, 3 comments)  
    The shell-execution-only model scatters temporary edit scripts across the filesystem, creating cleanup overhead before commits.

## Key PR Progress
1. **[#28524](https://github.com/google-gemini/gemini-cli/pull/28524) — Caretaker Triage prompt hill-climbing & orchestrator updates**  
   3 weeks of prompt optimization integrated; introduces a dedicated `code_explorer` skill for the triage worker. Directly improves issue triage quality.

2. **[#28433](https://github.com/google-gemini/gemini-cli/pull/28433) — PR Generator orchestrator: iterative bug-fixing state machine** (size/l, size/xl)  
   Core of the new SSR pipeline: coordinates Firestore locking, AI coding loops, ESLint analysis, and automatic PR generation from issues.

3. **[#28432](https://github.com/google-gemini/gemini-cli/pull/28432) — PR Generator Firestore dual-locking & test ingestion**  
   Database layer for the SSR pipeline with transactional locking, lifecycle state enums, and test harnesses for concurrent access scenarios.

4. **[#28431](https://github.com/google-gemini/gemini-cli/pull/28431) — PR Generator Cloud Run/Workflows/Docker configuration**  
   Infrastructure-as-code for the SSR pipeline: Cloud Run Jobs, Eventarc triggers, and Docker images for production deployment.

5. **[#28509](https://github.com/google-gemini/gemini-cli/pull/28509) — Filter thought parts from history when context management is disabled**  
   Prevents leakage of internal model monologue (`thought: true` parts) into history, which could cause duplicate reasoning blocks and confuse subsequent turns.

6. **[#28519](https://github.com/google-gemini/gemini-cli/pull/28519) — Prevent infinite auth loop by awaiting credential save**  
   Fixes a class of crash loops where asynchronous credential writes were not awaited, causing repeated re-authentication prompts.

7. **[#28481](https://github.com/google-gemini/gemini-cli/pull/28481) — Refresh MCP OAuth tokens with stored client ID** (P1, area/security)  
   Fixes a bug where OAuth token refresh for dynamically registered MCP servers would fail locally and silently delete stored credentials, forcing re-auth on every session.

8. **[#28485](https://github.com/google-gemini/gemini-cli/pull/28485) — Add gemini-3.5-flash to model selector** (P2)  
   Users were unable to select flash model variants because the model dialog only surfaces a hardcoded default. Opens access to newer model tiers.

9. **[#28446](https://github.com/google-gemini/gemini-cli/pull/28446) — Use native fetch for OAuth token exchange** (P1, area/security)  
   Fixes "Premature close" errors on headless VPSes during login by switching from undici/HTTP agents to native `fetch`, which has better underlying transport handling.

10. **[#28517](https://github.com/google-gemini/gemini-cli/pull/28517) — Enforce HTTPS for GoogleCredentialsAuthProvider**  
    Prevents ADC tokens from being transmitted over cleartext HTTP. A defense-in-depth security layer for credential transmission.

## Feature Request Trends
- **AST-aware tooling** — Multiple EPICs (e.g., [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)) push for AST-precise file reads and codebase mapping to reduce token waste and turn counts.
- **Agent self-awareness** — Developers want agents that understand their own CLI flags, hotkeys, capabilities, and limits (e.g., [#21432](https://github.com/google-gemini/gemini-cli/issues/21432)).
- **Subagent transparency** — Strong demand for subagent trajectory visibility in `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)) and bug reports ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763)) to facilitate debugging and evaluation.
- **Sandboxed execution** — The zero-dependency OS sandboxing proposal ([#19873](https://github.com/google-gemini/gemini-cli/issues/19873)) remains a top architectural ask for safely leveraging Gemini's bash affinity.

## Developer Pain Points
- **Agent hangs and false completions** — The #1 source of frustration. Subagents reporting `GOAL` success when they actually timed out ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)), and generalist agents hanging indefinitely ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)).
- **Permission & control issues** — Subagents executing despite being disabled in configuration ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)) and performing destructive operations (git reset --force, etc.) without guardrails ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).
- **Terminal/UI glitches** — Shell commands stuck on "Waiting input" after finishing ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), terminal corruption after exiting editors ([#24935](https://github.com/google-gemini/gemini-cli/issues/24935)), and flicker on resize ([#21924](https://github.com/google-gemini/gemini-cli/issues/21924)).
- **Tool count limits** — A 400 error surfaces when the agent has >128 tools available ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)), suggesting a need for smarter tool scoping.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-24

## Today's Highlights
Two patch releases (v1.0.74 and v1.0.74-4) landed yesterday with improved MCP support, including Open Plugin Spec v1 manifests and reliable IDE reconnection after MCP server reloads. The community saw a surge of new issues around MCP tool integration quirks and session recovery failures, with eight new triage-labeled issues filed today alone.

## Releases
- **v1.0.74** (2026-07-23)
  - Fix: Typing `?` while the `/search` bar is open no longer enters it as text instead of opening quick help
  - Added: Support for Open Plugin Spec v1 plugin manifests and `mcp.json` configuration
  - Fix: IDE integration reconnects reliably when the CLI reloads MCP servers or changes directory
  - Improvement: Multi-turn subagent handling

- **v1.0.74-4** (2026-07-23)
  - Added: Subagent timelines now identify whether prompts came from the main agent or another subagent
  - Fix: IDE integration reconnects reliably when the CLI reloads MCP servers or changes directory

## Hot Issues
1. **#[4097](https://github.com/github/copilot-cli/issues/4097) — `apply_patch` stores deleted binary in session history, permanently exceeding CAPI 5 MB limit**  
   *Open, 4 comments, 5 👍*  
   When `apply_patch` deletes a large binary file, its `tool.execution_complete` event stores the entire deleted binary as a textual diff. This permanently bloats conversation history past CAPI Responses' 5 MB limit, and `/compact` cannot recover. A critical UX blocker for projects with binary assets.

2. **#[3534](https://github.com/github/copilot-cli/issues/3534) — WSL2 (ARM64): `/copy` fails with `clip.exe exited with code 1`**  
   *Open, 5 comments, 4 👍*  
   Clipboard writes on WSL2 ARM64 fail due to a quoting bug in the `cmd.exe` wrapper. Affects all clipboard operations on this platform. Community upvoted as a high-priority platform gap.

3. **#[4165](https://github.com/github/copilot-cli/issues/4165) — `copilot --resume` hangs at "Resuming session" on cold start in Windows**  
   *Open, 3 comments, 1 👍*  
   Resuming sessions from PowerShell on Windows gets stuck indefinitely. Sessions resume successfully when launched interactively first, suggesting a cold-boot initialization race condition.

4. **#[4206](https://github.com/github/copilot-cli/issues/4206) — Environment footer stuck on "Loading:" forever when built-in GitHub MCP handshake stalls under org MCP policy**  
   *Open (triaged), 3 comments, 2 👍*  
   Under enterprise MCP policies, the status footer permanently shows a loading state even though all items are actually loaded. Cosmetic but confusing, and may mask real loading failures.

5. **#[4143](https://github.com/github/copilot-cli/issues/4143) — CLI should inherit MCP tools from connected VS Code instance**  
   *Open (triaged), 2 comments, 5 👍*  
   Users want MCP tools available in VS Code (e.g., MSSQL Agent, Anthropic Tools) to be accessible in the CLI session when IDE-connected. Currently, they remain siloed. Highest upvotes today.

6. **#[4214](https://github.com/github/copilot-cli/issues/4214) — Eternal blinking loading circle on new sessions**  
   *Open, 1 comment, 1 👍*  
   New CLI sessions get stuck at "Loading:" or "Loading: 1 skill" indefinitely. User reports Copilot identifies the source but cannot fix it, raising concerns about billing for unresponsive sessions.

7. **#[4235](https://github.com/github/copilot-cli/issues/4235) — Ctrl+C no longer cancels/interrupts an active agent run (regression)**  
   *Open (triage), new today*  
   Critical regression: Ctrl+C during an active agent run now appears to be ignored. Previously it aborted the in-progress turn. This breaks a fundamental user expectation for terminal tools.

8. **#[4238](https://github.com/github/copilot-cli/issues/4238) — Failed GitHub MCP tool details render the server label one character per line**  
   *Open (triage), new today*  
   Expanded error details for failed MCP tool calls produce an extremely tall, unreadable display because the server label wraps to one character per line. Pure rendering bug, but severely impacts debugging.

9. **#[4234](https://github.com/github/copilot-cli/issues/4234) — Plugin MCP servers cannot resolve the active project directory**  
   *Open (triage), new today*  
   MCP servers loaded from plugins launch with their working directory set to the plugin installation root, not the user's project. Project-scoped MCP servers read and write the wrong location.

10. **#[4233](https://github.com/github/copilot-cli/issues/4233) — Emit `usage_update` in `--acp` mode for parity with interactive statusline**  
    *Open (triage), 1 comment, 2 👍*  
    The `--acp` mode never emits context-window or AI-credit usage updates, leaving ACP clients (Zed, etc.) blind to usage metrics that the CLI already computes internally.

## Key PR Progress
1. **#[4228](https://github.com/github/copilot-cli/pull/4228) — Withdrawn: incorrect scope for #3534**  
   *Closed, new today*  
   Withdrawn quickly because the fix addressed documentation rather than the private clipboard runtime implementation. Source branch deleted.

## Feature Request Trends
- **MCP tool sharing across runtimes**: Users increasingly expect MCP tools configured in VS Code or plugins to be automatically available in CLI sessions ([#4143](https://github.com/github/copilot-cli/issues/4143), [#4234](https://github.com/github/copilot-cli/issues/4234)).
- **Session state management & recovery**: Multiple requests for better session recovery mechanisms, including automatic compaction of oversized histories ([#4097](https://github.com/github/copilot-cli/issues/4097)) and graceful handling of CAPI limits.
- **Enterprise & policy controls**: Growing demand for enterprise-grade authentication in ACP mode ([#3161](https://github.com/github/copilot-cli/issues/3161)) and better visibility into policy-stalled loading states ([#4206](https://github.com/github/copilot-cli/issues/4206)).
- **Hook extensibility**: Requests to make hook outputs actionable, not just observational — particularly for prompt modification ([#3713](https://github.com/github/copilot-cli/issues/3713)) and custom permission handling ([#4237](https://github.com/github/copilot-cli/issues/4237)).
- **Context window transparency**: Strong interest in surfacing real (deferred) MCP tool costs in `/context` and ACP usage updates ([#4189](https://github.com/github/copilot-cli/issues/4189), [#4233](https://github.com/github/copilot-cli/issues/4233)).

## Developer Pain Points
- **Session memory bloat is a recurring crisis**: Multiple issues ([#3767](https://github.com/github/copilot-cli/issues/3767), [#4097](https://github.com/github/copilot-cli/issues/4097)) describe sessions becoming permanently wedged after exceeding the 5 MB CAPI limit, with no recovery path. `/compact` is reported as ineffective for binary-based bloat.
- **Windows and WSL2 platform instability**: Persistent clipboard failures on WSL2 ARM64 ([#3534](https://github.com/github/copilot-cli/issues/3534)), cold-start resume hangs ([#4165](https://github.com/github/copilot-cli/issues/4165)), and stale binary issues ([#4199](https://github.com/github/copilot-cli/issues/4199)) make Windows the most painful platform.
- **MCP integration inconsistencies**: JSON serialization failures with `BigInt` ([#4211](https://github.com/github/copilot-cli/issues/4211)), tool visibility delays after `tools/list_changed` ([#3125](https://github.com/github/copilot-cli/issues/3125)), and zero-tool exposure after successful OAuth ([#4089](https://github.com/github/copilot-cli/issues/4089)) suggest the MCP integration layer is still maturing.
- **Interrupt and input handling regressions**: Ctrl+C not working ([#4235](https://github.com/github/copilot-cli/issues/4235)) and `Ctrl+G` (edit in `$EDITOR`) breaking during question prompts ([#4230](https://github.com/github/copilot-cli/issues/4230)) are regressions that disrupt core terminal workflows.
- **Loading/initialization feedback gaps**: Multiple reports of eternal loading states with no error feedback ([#4214](https://github.com/github/copilot-cli/issues/4214), [#4206](https://github.com/github/copilot-cli/issues/4206)) leave users unsure if something is broken or just slow.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date:** 2026-07-24

---

## Today's Highlights

The community saw a major surge in fix activity, with 15 pull requests opened in a single day, primarily from contributor `lihailong00` addressing Windows compatibility, MCP stability, and shell completion bugs. A significant new discussion (#2555) explores using Kimi's Agent architecture for quantitative finance, while long-standing feature requests like Remote Control (#1282) continue to gather community support. No new releases were published in the last 24 hours.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **#2555 – A-share quantification + AI Agent practice** (New, 0 comments, 0 👍)
   *Author: yupeng012*
   A deep-dive discussion on applying Kimi's Agent patterns to financial trading agents, using real PnL as the only evolution metric instead of benchmark scores. Important for the quantitative finance community exploring agentic workflows.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2555)

2. **#1282 – Feature Request: Remote Control** (6 comments, 16 👍)
   *Author: CatKang*
   Proposes continuing local CLI sessions from any device (phone, tablet, browser). The most upvoted open feature request, indicating strong demand for cross-device workflow continuity.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/1282)

3. **#2553 – /plugins crashes with TypeError (Windows, v0.29.0)** (0 comments, 0 👍)
   *Author: tovipy-png*
   The plugin management screen crashes entirely when 2+ plugins are installed on Windows. A critical usability blocker for power users.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2553)

4. **#2552 – Poor Cyrillic font kerning in Kimi Desktop** (0 comments, 0 👍)
   *Author: Serg2000Mr*
   Broken letter spacing in markdown rendering for Cyrillic text on Windows. Affects readability for Russian-speaking users.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2552)

5. **#2545 – Sync queued prompts to backend for phone users** (0 comments, 0 👍)
   *Author: vilicvane*
   When the browser goes to background on mobile, queued prompts aren't sent. A UX pain point for mobile Kimi Web users.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2545)

6. **#2538 – kimi-datasource plugin worker pool blocks all sessions** (0 comments, 0 👍)
   *Author: cloxichjc*
   Worker pool timeout in the `kimi-datasource` plugin causes cascading session freezes across concurrent sessions. A reliability issue for multi-session users.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2538)

---

## Key PR Progress

1. **#2554 – Fix StrReplaceFile replacement count** (0 comments)
   *Author: ayaangazali*
   Corrects the success message to count replacements against running content rather than original content. Small but important for accurate tool feedback.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2554)

2. **#2548 – Reuse initialized MCP client sessions** (0 comments)
   *Author: lihailong00*
   Keeps MCP client sessions open across tool calls, preventing a second `initialize` handshake that some servers reject. Improves reliability for custom MCP servers.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2548)

3. **#2551 – Fix file completion search limit** (0 comments)
   *Author: lihailong00*
   Allows searching beyond the first 1000 filesystem entries for `@` file completion queries. Important for users in large repositories.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2551)

4. **#2549 – Index tracked vendor files for completion** (0 comments)
   *Author: lihailong00*
   Includes Git-tracked `vendor/` files in `@` completion while still excluding `node_modules`. Balances discoverability with performance.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2549)

5. **#2547 – Configure Windows stdio as UTF-8** (0 comments)
   *Author: lihailong00*
   Sets stdout/stderr to UTF-8 on Windows at startup, fixing rendering issues with cp936/cp1252 streams. Critical for non-English Windows users.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2547)

6. **#2546 – Escape markup in echoed stdin prompts** (0 comments)
   *Author: lihailong00*
   Prevents user input containing Rich markup characters (e.g., `[/login]`) from breaking the terminal display. Important for security and UX.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2546)

7. **#2543 – Notify hooks on permission prompts** (0 comments)
   *Author: lihailong00*
   Emits `permission_prompt` notification hook when manual approval is required. Enhances observability for tool execution workflows.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2543)

8. **#2541 – Continue after MCP deferred startup failure** (0 comments)
   *Author: lihailong00*
   Prevents optional/background MCP startup failures from aborting the interactive session. Improves resilience in complex setups.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2541)

9. **#2542 – Isolate Windows process log files** (0 comments)
   *Author: lihailong00*
   Uses `kimi.<pid>.log` on Windows to prevent concurrent processes from corrupting the same log file. Essential for multi-process Windows workflows.
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2542)

10. **#2537 – Support numeric keypad input** (0 comments)
    *Author: lihailong00*
    Recognizes DEC application-keypad sequences from Windows Terminal. Addresses a common annoyance for users relying on numeric keypads.
    [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2537)

---

## Feature Request Trends

- **Remote Control / Cross-Device Continuity (#1282, #2545):** Users strongly desire the ability to resume sessions across devices, especially from mobile. The 16 👍 on #1282 (created months ago) shows sustained interest.
- **Financial/Quantitative Agent Workflows (#2555):** A new emerging theme—community members are exploring how Kimi's agent architecture can be adapted for real-time trading, with emphasis on PnL-driven learning rather than benchmark scores.
- **Plugin System Stability (#2553, #2538):** As plugin adoption grows, users are hitting boundaries in concurrent usage and multi-plugin management. Expect more demand for robust plugin isolation.

---

## Developer Pain Points

- **Windows Compatibility (#2553, #2552, #2547, #2542, #2537):** The single largest pain point. Issues with UTF-8 encoding, font rendering, plugin crashes, log file conflicts, and numeric keypad support all hit Windows users. The 15 PRs opened today include 8 Windows-specific fixes.
- **Plugin Reliability at Scale (#2538):** Worker pool timeouts in plugins causing cascading session freezes is a critical reliability concern for power users running multiple concurrent sessions.
- **MCP Server Compatibility (#2548, #2541):** Developers running custom MCP servers are hitting initialization handshake failures and crash-on-startup bugs, indicating the MCP integration layer still needs hardening.
- **Terminal Rendering Edge Cases (#2546, #2552):** Rich markup in plain text input and broken font kerning for non-Latin scripts point to rendering fragility when handling diverse user input and locale settings.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-24

## Today's Highlights

The community remains highly engaged around two converging themes: **provider model discovery** and **billing fairness**. The long-running Issue #6231 on auto-discovering OpenAI-compatible models (30 comments, 187 👍) continues as the top-voted feature, while a new cluster of reports around the content filter charging users for blocked outputs (Issues #35475, #35643) has escalated billing transparency concerns. On the stability front, today saw a flurry of crash reports (closed in the Desktop 1.18.4 release) and two focused stabilization PRs from kitlangton targeting tool definition ordering for prompt-cache improvements.

## Releases

**No new releases in the last 24 hours.**

## Hot Issues

1. **[#6231 — Auto-discover models from OpenAI-compatible provider endpoints](https://github.com/anomalyco/opencode/issues/6231)** (30 comments, 187 👍) — *Open*  
   The community's top request by a wide margin. Users of LM Studio, Ollama, and llama.cpp must manually list models in config; frequent model changes make this painful. This issue has been open since December 2025 and remains a blocker for many local-first users.

2. **[#37012 — [FEATURE]: keep legacy layout option](https://github.com/anomalyco/opencode/issues/37012)** (29 comments, 30 👍) — *Open*  
   A loud call to preserve the old layout, citing easy access to all features from the main window. The new UI requires more navigation, and workspace functionality is reportedly missing.

3. **[#37716 — Internal Server Error](https://github.com/anomalyco/opencode/issues/37716)** (26 comments, 5 👍) — *Closed*  
   A Desktop v1.18.3 bug causing server errors across multiple models. Closed quickly, likely patched in 1.18.4.

4. **[#35475 — False positive content-filter on claude-fable-5, charged ~$20 for blocked output](https://github.com/anomalyco/opencode/issues/35475)** (10 comments, 0 👍) — *Open*  
   A serious billing issue: benign queries are flagged by the content filter, yet cache writes are billed (~$6.69 each) despite zero output to the user. Total loss: ~$20. Community is watching closely.

5. **[#25848 — [FEATURE]: add session renaming](https://github.com/anomalyco/opencode/issues/25848)** (11 comments, 0 👍) — *Open*  
   Users want `/rename` or `opencode session rename` commands. A simple UX gap that makes session organization difficult.

6. **[#37326 — math equations not rendered](https://github.com/anomalyco/opencode/issues/37326)** (7 comments, 1 👍) — *Open*  
   Models outputting LaTeX equations don't render properly in the UI. A quality-of-life issue for technical users.

7. **[#35643 — Content filter blocks output but user is still billed for full generation cost](https://github.com/anomalyco/opencode/issues/35643)** (3 comments, 0 👍) — *Open*  
   Companion to #35475. Confirms the billing system charges for blocked responses. Users argue charges should be refunded or never applied.

8. **[#38255 — Discrepancy between different opencode go usage dashboard](https://github.com/anomalyco/opencode/issues/38255)** (5 comments, 0 👍) — *Open*  
   Monthly limit says 100% usage, but granular dashboard shows only ~$10 spent. Models stopped working at midnight. A confusing billing dashboard bug.

9. **[#38591 — npm error unsupported platform for opencode-ai@1.18.4 on FreeBSD](https://github.com/anomalyco/opencode/issues/38591)** (2 comments, 0 👍) — *Open*  
   FreeBSD users cannot install the npm package. The issue raises broader questions about platform support strategy.

10. **[#38564 — Subagent termination does not kill spawned child processes (disk abuse risk)](https://github.com/anomalyco/opencode/issues/38564)** (2 comments, 0 👍) — *Open*  
    Killing a subagent leaves PowerShell child processes running at 100% I/O. A resource abuse and security risk that needs urgent attention.

## Key PR Progress

1. **[#38590 — fix(core): stabilize tool definition ordering](https://github.com/anomalyco/opencode/pull/38590)** — *Open*  
   kitlangton ensures tool definitions are emitted in canonical name order, producing byte-identical arrays regardless of plugin order. This stabilizes the first provider prompt-cache prefix component.

2. **[#38584 — fix(opencode): recover projects moved to a new path](https://github.com/anomalyco/opencode/pull/38584)** — *Open*  
   Fixes a bug where moved Git repos kept the old path as primary worktree, preventing project recovery. Closes #38578.

3. **[#38588 — fix(codemode): stabilize catalog ordering](https://github.com/anomalyco/opencode/pull/38588)** — *Closed*  
   Renders Code Mode catalogs in canonical dotted-path order, preventing false `core/codemode` instruction updates on unchanged tool reloads.

4. **[#38581 — fix(opencode): preserve grep symlink paths](https://github.com/anomalyco/opencode/pull/38581)** — *Open*  
   Grep was canonicalizing symlinked paths and returning real targets; subsequent tool calls would fail on the non-existent symlink. Closes #38582.

5. **[#38183 — feat(core): render CodeMode catalog deltas from structured snapshots](https://github.com/anomalyco/opencode/pull/38183)** — *Open*  
   Moves Code Mode catalog prompting into core, upgrading from whole-string replacement to skill-style semantic diffing. Follow-up to #38003.

6. **[#38369 — fix(core): improve patch errors](https://github.com/anomalyco/opencode/pull/38369)** — *Closed*  
   Identifies malformed hunks with operation paths, reports matching failures without redundant error prefixes, and includes stable filesystem causes.

7. **[#38579 — feat(mcp): forward plugin request metadata](https://github.com/anomalyco/opencode/pull/38579)** — *Open*  
   Allows plugins to set optional `_meta` fields forwarded to MCP tool calls. Closes #17084, building on #21539 and #21624.

8. **[#38423 — feat(ai): preserve raw finish reasons](https://github.com/anomalyco/opencode/pull/38423)** — *Closed*  
   Models terminal reasons as `{ normalized, raw }` on finish events. Preserves raw reasons from OpenAI, Anthropic, Gemini, and Bedrock.

9. **[#38198 — fix(acp): stage file edits for native review instead of writing twice](https://github.com/anomalyco/opencode/pull/38198)** — *Open*  
   Prevents double writes during ACP review. Closes #38196, related to the long-standing #4240.

10. **[#38539 — fix(tui): preview written file content](https://github.com/anomalyco/opencode/pull/38539)** — *Open*  
    Renders completed writes as block cards with real before/after diffs. Distinguishes new files from overwrites using red/green rendering.

## Feature Request Trends

- **Auto Model Discovery** (#6231) remains the dominant request, with 187 upvotes and a continuous stream of activity from local-provider users.
- **UI/UX improvements** are the second-largest cluster: legacy layout preservation (#37012), session renaming (#25848), mobile control (#33163), and sub-agent output views (#37267) indicate users feel the new UI sacrifices workflow efficiency.
- **Platform and accessibility**: RTL language support (#6284) and FreeBSD compatibility (#38591) show growing diversity in user environments.
- **Billing transparency** has emerged as a new hot topic, driven by content-filter billing bugs (#35475, #35643). Users want clear charging policies for blocked outputs.

## Developer Pain Points

- **Billing and content filter friction** is the most urgent recurring frustration. Users are charged for blocked outputs, and the dashboard shows inconsistent usage data (#38255). Trust in the billing system is eroding.
- **Sub-process and resource management** is a critical stability concern. Subagent termination leaves orphaned child processes (#38564), and tool calls can enter infinite loops (#26220). Developers are losing work to hung or runaway processes.
- **Platform fragmentation** bites users on FreeBSD (#38591) and via the VS Code extension installation process (#36028). The expectation of cross-platform reliability is not fully met.
- **Model compatibility issues** hit early adopters hard: DeepSeek V4 on the Go subscription (#38554) and kimi-k2.6 thinking/reasoning parameter conflicts (#38329) show that the model integration layer has gaps.
- **Crash frequency** on the Desktop app (1.18.3/1.18.4) has generated multiple crash reports (TUI, renderer, sidebar loss). While some were closed quickly, the volume suggests a regression in release quality.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-24

## Today's Highlights

The community is showing intense focus on provider compatibility, with high activity around Anthropic tool-call normalization and OpenAI-compatible provider fixes. A strong cluster of clipboard-related bugs on Wayland systems highlights ongoing sandboxing challenges, while several PRs advance extension API stability and model configuration hot-reload capabilities. The volume of closed issues (25 of top 30) suggests maintainers are actively clearing the queue.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **#6951 — [OPEN] Qwen3.8-max-preview reasoning effort misconfiguration**  
   The built-in `thinkingLevelMap` uses `minimal/low/medium/high` but Qwen's API requires `low/medium/xhigh`. This mismatch silently degrades reasoning quality for Qwen users. Community visibility: 1 👍.  
   [Link](https://github.com/earendil-works/pi/issues/6951)

2. **#6999 — [OPEN] models.json hot-reload broken after 0.80.8**  
   Users who dynamically edit `~/.pi/agent/models.json` mid-session can no longer see changes when opening `/model`. This breaks a common workflow for testing custom provider configs. 3 comments, no 👍.  
   [Link](https://github.com/earendil-works/pi/issues/6999)

3. **#6994 — [CLOSED] Llama provider hardcoded 16k maxTokens**  
   `packages/coding-agent/src/extensions/llama/provider.ts` artificially caps output at 16,384 tokens regardless of the actual model's context window. Community response: merged via PR #7034.  
   [Link](https://github.com/earendil-works/pi/issues/6994)

4. **#6948 — [OPEN] llama.cpp defaultProvider race condition at startup**  
   Setting `defaultProvider: "llama.cpp"` in `settings.json` works for model display but the session never starts with the correct model due to async refresh timing. 3 comments.  
   [Link](https://github.com/earendil-works/pi/issues/6948)

5. **#6872 — [OPEN] `/copy` falsely reports success when wl-copy fails**  
   A critical UX bug for users in sandboxed or headless environments: `wl-copy` exit code is never checked, so fallback `xclip` never runs. Duplicate with #7012 (now closed). Community remains engaged with 3 comments.  
   [Link](https://github.com/earendil-works/pi/issues/6872)

6. **#7002 — [CLOSED] Anthropic tool-call ID normalization collision risk**  
   Foreign IDs longer than Anthropic's 40-char limit are truncated with a hash, which can collide for sufficiently similar IDs. A correctness concern for cross-provider sessions. 3 comments.  
   [Link](https://github.com/earendil-works/pi/issues/7002)

7. **#7033 — [CLOSED] Malformed package manifest crash-loops sessions**  
   A non-array `pi.skills` field (e.g., `"./skills"` instead of `["./skills"]`) causes an uncaught TypeError every session start, with no recovery path. 2 comments.  
   [Link](https://github.com/earendil-works/pi/issues/7033)

8. **#6970 — [OPEN] GitHub Copilot plugin auth vs OAuth confusion**  
   Pi's use of `GitHub Copilot Plugin` integration instead of proper OAuth causes token invalidation when used alongside other Copilot clients (neovim, copilot-lsp). 2 comments, 1 👍.  
   [Link](https://github.com/earendil-works/pi/issues/6970)

9. **#7030 — [CLOSED] Provider prefix dropped for OpenAI models via Cloudflare**  
   `compat.js` streamSimple falls back to raw API provider when `getBuiltinProviderForModel` returns undefined, dropping the Cloudflare prefix. Affects all gateway-routed OpenAI models. 2 comments.  
   [Link](https://github.com/earendil-works/pi/issues/7030)

10. **#6998 — [OPEN] DeepSeek on Aliyun needs qwen thinkingFormat**  
    Models provided via the Qwen Token Plan use wrong `thinkingFormat` (DeepSeek defaults instead of `"qwen"`). Additional issues with `thinkingLevelMap` override. 2 comments.  
    [Link](https://github.com/earendil-works/pi/issues/6998)

## Key PR Progress

1. **#7036 — [OPEN] Reload model config in picker (by mitsuhiko)**  
   Directly addresses #6999, but the author notes a design tension: `reloadConfig` vs. a flag on `refresh`. A clean architectural decision is needed.  
   [Link](https://github.com/earendil-works/pi/pull/7036)

2. **#7034 — [CLOSED] Derive llama output limits from context window (by christianklotz)**  
   Fixes #6994 by removing the hardcoded 16k cap and deriving limits from each model's context. Includes test coverage for windows above 16k.  
   [Link](https://github.com/earendil-works/pi/pull/7034)

3. **#7032 — [OPEN] Expose unavailable scoped models with diagnostics (by christianklotz)**  
   Model resolution now surfaces typed `no-match` diagnostics for models that are configured but no longer available. Users can remove them via `/scoped-models`.  
   [Link](https://github.com/earendil-works/pi/pull/7032)

4. **#7017 — [CLOSED] Experimental limited repainting for long sessions (by mitsuhiko)**  
   Adds a setting to avoid fully repainting transcripts on very long sessions. A pragmatic performance optimization for heavy users.  
   [Link](https://github.com/earendil-works/pi/pull/7017)

5. **#7028 — [CLOSED] Keep /resume unfiltered after nested resume (by simonckemper)**  
   Running `/resume` inside a resumed session collapsed picker to a single self-reference. Now idempotent and correctly shows all sessions.  
   [Link](https://github.com/earendil-works/pi/pull/7028)

6. **#7011 — [OPEN] Share host modules with native ESM extensions (by haoqixu)**  
   Fixes module state divergence where Jiti's native imports cause extensions to load private copies of Pi packages instead of sharing the host's instances.  
   [Link](https://github.com/earendil-works/pi/pull/7011)

7. **#7009 — [CLOSED] Await wl-copy exit code with fallback to xclip (by rkfshakti)**  
   Fixes the Wayland clipboard false-success bug. Now properly awaits exit code and falls through to `xclip`/OSC 52 on failure.  
   [Link](https://github.com/earendil-works/pi/pull/7009)

8. **#6980 — [CLOSED] Make provider retries abortable (by petrroll)**  
   Replaces Anthropic/OpenAI SDK inner retries with a common helper that respects `maxRetryDelayMS` and is interruptible via `AbortSignal`. Fixes #6911.  
   [Link](https://github.com/earendil-works/pi/pull/6980)

9. **#6971 — [CLOSED] Emit bash_execution_update events (by ananthakumaran)**  
   Adds event-level `id` for parallel bash execution tracking on the client side. Tested against pimacs.el.  
   [Link](https://github.com/earendil-works/pi/pull/6971)

10. **#6341 — [CLOSED] Support constrained sampling for tools (by mitsuhiko)**  
    Adds opt-in `constrainedSampling` config enabling provider-side JSON-schema constrained tool input generation (a.k.a. "strict" tools). A major feature for deterministic tool interactions.  
    [Link](https://github.com/earendil-works/pi/pull/6341)

## Feature Request Trends

The strongest signal this week is **provider expansion and compatibility**. Three separate issues (#4742, #7013, and discussion around SiliconFlow) request built-in support for the SiliconFlow model aggregator. Another thread (#6886) requests server-side Fable-to-Opus fallback from Anthropic. These indicate a community actively seeking to reduce manual `models.json` configuration.

A secondary trend is **constrained/strict tool generation**. Issue #6306 (closed) and PR #6341 together form a cohesive effort to add grammar-aware tool probing with provider-side JSON-schema enforcement. This is among the more architecturally significant features being discussed.

On the UX side, **standard keyboard text selection** (#7038, just filed) and **exportable transcript renderers** for extensions (#7037) signal growing demand for accessibility and extensibility in the TUI.

## Developer Pain Points

1. **Wayland clipboard failures** — Two issues (#6872, #7012) and one PR (#7009) all revolve around `wl-copy` exit codes not being checked, causing false-success reports and skipped fallbacks. The sandboxed/bwrap use case is particularly affected.

2. **Provider onboarding friction** — Model configuration continues to be a pain point: hardcoded limits (llama.cpp), wrong default thinking maps (Qwen, DeepSeek on Aliyun), race conditions at startup (llama.cpp defaultProvider), and broken hot-reload of model config (#6999) all impede smooth setup.

3. **Cross-provider edge cases** — Token invalidation when Copilot clients coexist (#6970), tool-call ID collisions (#7002), and gateway-routed model prefix dropping (#7030) show that the multi-provider architecture still has rough edges in production.

4. **Extension reliability** — A malformed package manifest can crash-loop every session (#7033), and installing an extension with `resources_discover` handlers collapses all skill scopes (#6968). Both are correctness bugs that erode trust in the extension system.

5. **TUI display bugs** — CJK cursor positioning (#7021) and home-path corruption outside the footer (#7006) are cross-cutting issues that affect non-English users and those with unusual filesystem layouts.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**Date: 2026-07-24**

## Today's Highlights
The project shipped a new nightly release (v0.20.1-nightly) with telemetry and performance improvements, while the community continues to grapple with full prompt reprocessing regressions and a broken update check system across multiple npm versions. A major architectural proposal for an enterprise external-memory integration profile is gaining traction, and CI stability emerges as a growing concern with multiple E2E test failures on main.

## Releases
**v0.20.1-nightly.20260724.7d17c44a3** ([Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.20.1-nightly.20260724.7d17c44a3))
- Test coverage for daemon metrics initialization ordering (PR [#7456](https://github.com/QwenLM/qwen-code/pull/7456))
- Performance improvements (scope unspecified)

## Hot Issues
1. **[#5736] Full prompt reprocessing regression** ([Issue](https://github.com/QwenLM/qwen-code/issues/5736))  
   *Status: CLOSED | 7 comments*  
   User reports increased full prompt re-processing after recent update when continuing conversations. Llama.cpp logs confirm forced re-processing. Community upvote count: 1. This remains a critical performance concern for local LLM users.

2. **[#7599] Workspace artifacts missing managedId** ([Issue](https://github.com/QwenLM/qwen-code/issues/7599))  
   *Status: CLOSED | 5 comments*  
   Artifacts created via `record_artifact` with `workspacePath` are emitted without `managedId`, breaking managed-artifact coordination in SSE events.

3. **[#7449] Enterprise external-memory integration profile proposal** ([Issue](https://github.com/QwenLM/qwen-code/issues/7449))  
   *Status: OPEN | 5 comments*  
   A provider-neutral enterprise memory integration profile. Triage feedback suggests documentation-first approach with incremental compatibility tests.

4. **[#7585] Direct External Context Provider Profile** ([Issue](https://github.com/QwenLM/qwen-code/issues/7585))  
   *Status: OPEN | 4 comments*  
   Proposes an extension enabling one Qwen CLI process to retrieve repository-shared context from an external memory service.

5. **[#7485] TUI large blank area after session resume** ([Issue](https://github.com/QwenLM/qwen-code/issues/7485))  
   *Status: OPEN | 4 comments*  
   After `qwen resume`, a large blank gap appears between the last message and the input prompt. UI regression affecting terminal users.

6. **[#7264] Cold-start lazy-loading audit follow-ups** ([Issue](https://github.com/QwenLM/qwen-code/issues/7264))  
   *Status: OPEN | 4 comments*  
   Eager static import closure of **17.24 MiB / 2420 modules** measured in ACP child process — all parsed on every cold start. Performance-critical optimization target.

7. **[#6014] Agent file reading no longer shows filenames** ([Issue](https://github.com/QwenLM/qwen-code/issues/6014))  
   *Status: OPEN | 4 comments*  
   Recent UI change downgraded from showing actual filenames to just "read 1 file". User frustration evident.

8. **[#6806] Context usage percentage stuck after /compress** ([Issue](https://github.com/QwenLM/qwen-code/issues/6806))  
   *Status: OPEN | 4 comments*  
   Status line doesn't reflect reduced token count after compression commands until next model request.

9. **[#7616] Too many flaky E2E tests?** ([Issue](https://github.com/QwenLM/qwen-code/issues/7616))  
   *Status: OPEN | 2 comments*  
   Developer questions whether 30 E2E failures in 12 days are real regressions or test design issues. Tests verify deterministic logic through non-deterministic model APIs.

10. **[#7568] Extension installation failure** ([Issue](https://github.com/QwenLM/qwen-code/issues/7568))  
    *Status: OPEN | 2 comments*  
    Installing extensions fails with misleading error "Extension id belongs to 'dotnet', not 'dotnet-test'" when the actual issue is a version mismatch.

## Key PR Progress
1. **[#7632] GitHub polling channel adapter** ([PR](https://github.com/QwenLM/qwen-code/pull/7632))  
   Adds GitHub notification polling with notification-as-wakeup architecture for responding to @mentions on issues/PRs.

2. **[#7497] Native video input in /learn** ([PR](https://github.com/QwenLM/qwen-code/pull/7497))  
   Adds support for local MP4/WebM/MOV/M4V files and video URLs as input to the `/learn` command.

3. **[#7302] Prior session references via @mention** ([PR](https://github.com/QwenLM/qwen-code/pull/7302))  
   Adds project-scoped session completion in `@` mentions, inserting `@session:<id>` with read-only transcript summary.

4. **[#7594] Compile cache propagation to ACP children** ([PR](https://github.com/QwenLM/qwen-code/pull/7594))  
   Performance improvement: publishes compile-cache directory to environment, letting ACP children reuse Node's module compilation cache.

5. **[#7607] Configurable image generation models** ([PR](https://github.com/QwenLM/qwen-code/pull/7607))  
   Adds user-configurable image generation model with `/model --image` and approval-gated generation tool.

6. **[#7603] Java SDK daemon transport hardening** ([PR](https://github.com/QwenLM/qwen-code/pull/7603))  
   Adapts Java daemon SDK to restart-safe event cursor contract, sending `X-Qwen-Event-Epoch` header.

7. **[#7268] Hot-reload workspace trust changes** ([PR](https://github.com/QwenLM/qwen-code/pull/7268))  
   Enables runtime trust-policy changes without daemon restart using semantic trust-policy snapshots.

8. **[#7195] Dedicated undici fetch for MCP Streamable HTTP** ([PR](https://github.com/QwenLM/qwen-code/pull/7195))  
   Routes MCP Streamable HTTP through undici's own fetch with disabled timeouts, fixing long-lived SSE streams.

9. **[#6506] Large paste performance optimization** ([PR](https://github.com/QwenLM/qwen-code/pull/6506))  
   Intercepts bracketed paste markers to bypass per-character event processing, reducing 260K char paste from ~1.7s to near-instant.

10. **[#7539] Clean orphaned managed npm update artifacts** ([PR](https://github.com/QwenLM/qwen-code/pull/7539))  
    Adds cleanup pass before updates to remove stale staging directories from dead processes.

## Feature Request Trends
Three major directionals are emerging from recent issues and PRs:

1. **Enterprise integration profiles** — multiple proposals ([#7449](https://github.com/QwenLM/qwen-code/issues/7449), [#7585](https://github.com/QwenLM/qwen-code/issues/7585)) for standardized external memory and context provider integrations, indicating growing enterprise adoption.

2. **Channel/notification ecosystem expansion** — new adapters for GitHub notifications ([#7632](https://github.com/QwenLM/qwen-code/pull/7632)), Telegram topic support ([#7609](https://github.com/QwenLM/qwen-code/issues/7609)), and WebSocket improvements.

3. **UI/UX polish for power users** — session references via @mention ([#7302](https://github.com/QwenLM/qwen-code/pull/7302)), version upgrade notices ([#7542](https://github.com/QwenLM/qwen-code/pull/7542)), and git mode selection in Web Shell ([#7471](https://github.com/QwenLM/qwen-code/pull/7471)).

## Developer Pain Points
Several recurring friction points are evident:

1. **Update check failures** — Multiple reports ([#7543](https://github.com/QwenLM/qwen-code/issues/7543), [#7515](https://github.com/QwenLM/qwen-code/issues/7515), [#7520](https://github.com/QwenLM/qwen-code/issues/7520)) across npm 10 and 12, with `getNpmCliPath` returning incorrect paths and npm 12's global mode array response breaking parsing.

2. **CI instability** — 5 E2E test failures on main in 24 hours alone ([#7516](https://github.com/QwenLM/qwen-code/issues/7516), [#7559](https://github.com/QwenLM/qwen-code/issues/7559), [#7605](https://github.com/QwenLM/qwen-code/issues/7605), [#7549](https://github.com/QwenLM/qwen-code/issues/7549)). Developer questions whether tests are testing deterministic logic through non-deterministic model APIs ([#7616](https://github.com/QwenLM/qwen-code/issues/7616)).

3. **Channel integration regressions** — WeChat ([#7590](https://github.com/QwenLM/qwen-code/issues/7590)), Telegram ([#7609](https://github.com/QwenLM/qwen-code/issues/7609)), user-level skills not loaded in channel mode ([#7575](https://github.com/QwenLM/qwen-code/issues/7575)), and monitor stop triggering automatic model turns ([#7566](https://github.com/QwenLM/qwen-code/issues/7566)).

4. **Full prompt reprocessing** — Recurring complaint ([#5736](https://github.com/QwenLM/qwen-code/issues/5736)) about forced full re-processing during conversation continuation, especially painful for local LLM users.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-24

## Today's Highlights
The CodeWhale project (formerly DeepSeek TUI) is in active pre-release stabilization for v0.9.1, with a security gate issue (#4713) tracking 17 open Dependabot alerts. A **stop-ship** bug (#4716) causing the TUI to exit immediately on macOS fresh terminals was reported, while the community contributed fixes for background shell output archiving (#4724) and full edit previews in the details pager (#4722). Several issues highlight lingering DeepSeek-era branding in settings menus (#4717) and under-baked provider auto-switching (#4720).

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#4713] v0.9.1 security gate: deep scan and dependency alert disposition**  
   *Author: Hmbown | Open*  
   Release-blocking: 17 open Dependabot alerts (7 high, 10 moderate) in axios, body-parser, braces, etc. Must be dispositioned before tagging v0.9.1.  
   *Why it matters:* This gates the entire v0.9.1 release. Community should expect delays until resolved.  
   👉 https://github.com/Hmbown/CodeWhale/issues/4713

2. **[#4716] TUI exits immediately on launch in fresh terminal — [stop-ship]**  
   *Author: Hmbown | Open*  
   `codew` / `codewhale` returns `[Process completed]` immediately on macOS fresh Terminal.app tabs. v0.9.1 candidate affected.  
   *Why it matters:* Stop-ship designation means no release until fixed. Critical for macOS users.  
   👉 https://github.com/Hmbown/CodeWhale/issues/4716

3. **[#4719] Composer: large pasted prompts get byte-corrupted before submission**  
   *Author: Hmbown | Open*  
   Path truncation and character dropping when pasting multi-line prompts. A downstream agent concluded "path doesn't exist" from corrupted input.  
   *Why it matters:* Core editing workflow broken for power users. Likely encoding issue in TUI input handling.  
   👉 https://github.com/Hmbown/CodeWhale/issues/4719

4. **[#4720] Provider/model setup and auto-switching feel under-baked**  
   *Author: Hmbown | Open*  
   Runtime auto-switched `deepseek → zai` (model `deepseek-v4-pro → GLM-5.2`) without clear user notification. Switches feel unintentional.  
   *Why it matters:* Provider routing is a fundamental UX concern. Users need transparency and control.  
   👉 https://github.com/Hmbown/CodeWhale/issues/4720

5. **[#4717] Settings: legacy "DeepSeek fallback model" shown prominently on non-DeepSeek providers**  
   *Author: Hmbown | Open*  
   Active provider `zai / GLM-5.2` still shows "DeepSeek fallback model" row. UI remains tied to DeepSeek branding.  
   *Why it matters:* Confusing UX for multi-provider users; suggests incomplete rebranding/cleanup.  
   👉 https://github.com/Hmbown/CodeWhale/issues/4717

6. **[#4723] Windows: AltGr+Q on ABNT2 layout opens help overlay instead of typing "/"**  
   *Author: nicolassmotta | Open*  
   Windows reports AltGr+Q as Ctrl+Alt+Q, conflicting with TUI keybindings. Brazilian ABNT2 users cannot type "/".  
   *Why it matters:* International keyboard support gap. Low-complexity fix but blocks users on common layout.  
   👉 https://github.com/Hmbown/CodeWhale/issues/4723

7. **[#4718] TUI transcript: information density too high (repeated hints, stacked reasoning states)**  
   *Author: Hmbown | Open*  
   Every tool card repeats "Option+V to inspect"; reasoning status shows stacked redundant labels.  
   *Why it matters:* Cognitive load reduction needed for professional workflows. UI polish issue.  
   👉 https://github.com/Hmbown/CodeWhale/issues/4718

8. **[#4721] Settings menu audit: catalog remaining legacy/density/labeling issues**  
   *Author: Hmbown | Open*  
   Tracking issue for systematic cleanup of DeepSeek-era assumptions in settings UI. Non-blocking but important for v0.9.1 polish.  
   *Why it matters:* Identifies scope of rebranding work; community contributions welcome.  
   👉 https://github.com/Hmbown/CodeWhale/issues/4721

9. **[#4042] feat: Environment-level tool sandboxing for sub-agents**  
   *Author: JayBeest | Closed*  
   Runtime enforcement of `--disallowed-tools` across sessions, sub-agents, Fleet workers, and MCP servers. 19 comments.  
   *Why it matters:* Security infrastructure for multi-agent execution. High community engagement.  
   👉 https://github.com/Hmbown/CodeWhale/issues/4042

10. **[#4722] TUI transcript: information density (backreference from PR)**  
    *Author: nightt5879 | Open*  
    (Referenced in PR #4722 for details pager improvements.)  
    👉 https://github.com/Hmbown/CodeWhale/issues/4722

## Key PR Progress

1. **[#4724] fix(tui): archive completed background shell output**  
   *Author: qinlinwang | Open*  
   Archives final stdout/stderr into originating ExecCell on job completion. Clears live output, freezes duration.  
   *Why it matters:* Solves output persistence for background jobs — a common workflow blocker.  
   👉 https://github.com/Hmbown/CodeWhale/pull/4724

2. **[#4722] fix(tui): show complete edit previews in details**  
   *Author: nightt5879 | Open*  
   Keeps compact `edit_file` card bounded, renders full `-/+` diff lazily in Alt+V details pager. Includes regression tests.  
   *Why it matters:* Balances compact UI with full edit transparency. Addresses #4718 density concerns.  
   👉 https://github.com/Hmbown/CodeWhale/pull/4722

3. **[#4346] fix: sanitize tool input_schema for Anthropic adapter**  
   *Author: qinlinwang | Closed*  
   Removes top-level `oneOf`/`anyOf`/`allOf` that cause Anthropic API 400 errors.  
   *Why it matters:* Unblocks Anthropic provider for tool-using agents. Critical multi-provider fix.  
   👉 https://github.com/Hmbown/CodeWhale/pull/4346

4. **[#4610] [v0.9.2] feat(tui): add configurable session token header**  
   *Author: XhesicaFrost | Open*  
   Opt-in `header_items = ["tokens"]` showing cumulative input, cache-hit, output token counts.  
   *Why it matters:* Adds transparency for token usage tracking. Planned for v0.9.2.  
   👉 https://github.com/Hmbown/CodeWhale/pull/4610

## Feature Request Trends

- **Multi-provider transparency**: Users want clear labeling when providers/models switch at runtime (#4720), and no stale DeepSeek-specific UI elements when other providers are active (#4717).
- **International keyboard support**: Windows AltGr handling for non-US layouts (ABNT2, likely others) is blocking for international users (#4723).
- **Token usage visibility**: Growing demand for in-header token counters (#4610), likely driven by cost-conscious users.
- **Tool sandboxing at environment level**: Completed work on `--disallowed-tools` enforcement (#4042) reflects need for security isolation in multi-agent/fleet deployments.
- **UI density control**: Repeated hints and stacked status labels (#4718, #4722) indicate users want configurable verbosity in transcript views.

## Developer Pain Points

- **Blocking v0.9.1 release**: Two stop-ship items — security gate (#4713, 17 Dependabot alerts) and fresh-terminal crash (#4716) — are delaying the release.
- **Input corruption**: Large paste operations corrupt prompts with character dropping and path truncation (#4719), breaking core editing workflows.
- **Provider switching opacity**: Auto-switching between providers (e.g., DeepSeek → Zhipu AI) happens without deliberate user intent or clear notification (#4720), causing trust issues.
- **Incomplete rebranding**: Settings UI still prominently displays DeepSeek-specific options (#4717) even when the active provider is not DeepSeek, suggesting missed cleanup items.
- **High-frequency issues**: The density of open issues (9 total, most from past 24h) suggests the project is under heavy active development but may benefit from stabilization sprints.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*