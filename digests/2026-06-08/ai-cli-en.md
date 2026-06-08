# AI CLI Tools Community Digest 2026-06-08

> Generated: 2026-06-08 02:15 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Ecosystem Comparison Report
**Date:** 2026-06-08

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is experiencing a bifurcation between **mature platforms** (Claude Code, OpenAI Codex) grappling with scale-related billing and stability issues, and **rapidly iterating challengers** (Gemini CLI, Qwen Code, CodeWhale) aggressively closing feature gaps while addressing foundational reliability. A unifying theme across all platforms is the **urgent demand for session reliability, billing transparency, and cross-platform parity**, with Windows and Linux users consistently reporting worse experiences than macOS. The ecosystem is also converging on **protocol standardization** (ACP, MCP) and **agent lifecycle management** as core infrastructure concerns, signaling maturation beyond the "feature velocity at all costs" phase.

---

## 2. Activity Comparison

| Tool | Active Issues (24h) | Active PRs (24h) | New Release (24h) | Community Engagement Level |
|------|--------------------|-----------------|--------------------|---------------------------|
| **Claude Code** | ~30 updated | 2 | None | **High** — #16157 alone has 1,476 comments |
| **OpenAI Codex** | ~25 updated | 10 merged/active | None | **High** — 510 👍 on Linux desktop request |
| **Gemini CLI** | 50 open updated | 14 updated | None | **Medium** — focused, security-aware community |
| **GitHub Copilot CLI** | 10 updated | 1 (trivial) | None | **Low-Medium** — quieter, enterprise-focused |
| **Kimi Code CLI** | 9 updated | 1 (closed) | None | **Low** — migration confusion suppressing engagement |
| **OpenCode** | ~20 updated | 10 active | None (v1.16.0 recently out) | **High** — rapid iteration, vocal community |
| **Pi** | ~15 updated | 10 merged | None | **Medium** — strong contributor presence |
| **Qwen Code** | 7 updated | 15+ active | Yes (nightly) | **High** — 42 PRs in 24h, ambitious roadmap |
| **CodeWhale (DeepSeek)** | ~15 updated | 21 updated | None | **Medium-High** — community-driven stabilization |

**Key observations:**
- **Qwen Code** leads raw development velocity (42 PRs, nightly releases)
- **Claude Code** has the most engaged but most frustrated user base (billing crisis)
- **CodeWhale** shows strong community contributor activity (21 PRs from multiple authors)
- **GitHub Copilot CLI** has notably lower community activity despite large user base

---

## 3. Shared Feature Directions

### 3.1 Linux Desktop Clients (5 of 9 tools)
| Tool | Request | Community Signal |
|------|---------|-----------------|
| **Claude Code** | #65697 — 310 👍, 22 comments | Strongest demand |
| **OpenAI Codex** | #11023 — 510 👍, 100 comments | **Highest upvoted request across all tools** |
| **Gemini CLI** | (Built-in CLI, Wayland issues #21983) | Less vocal but affected |
| **OpenCode** | (Desktop exists, quality issues) | Implicit demand |
| **Pi** | Terminal-native, less pressure | Lower priority |

### 3.2 Billing & Usage Transparency (4 of 9 tools)
- **Claude Code**: #16157 (1,476 comments) — "Max subscribers burning through allowance instantly"
- **OpenAI Codex**: #12299 — "Hit usage limit despite 10% remaining"
- **OpenCode**: #14273, #15585 — "Free model usage exceeded" with ambiguous limits
- **GitHub Copilot CLI**: #2828 — "Rate limit messages need actionable suggestions"

**Pattern**: Users across platforms demand **real-time quota visibility**, **granular billing breakdowns**, and **protection against charges for failed API calls**.

### 3.3 Multi-Provider / BYOK Model Support (5 of 9 tools)
- **Claude Code**: Third-party provider context detection (#46416)
- **GitHub Copilot CLI**: BYOK/local provider session switching (#3709)
- **OpenCode**: Azure Foundry, multiple provider support (#31239)
- **Pi**: Requesty integration (#5472), DeepSeek persistence fix (#5431)
- **Qwen Code**: Dynamic multi-model fetching (#1206)

### 3.4 Session Persistence & Cross-Device Handoff (4 of 9 tools)
- **Claude Code**: Remote Control session disconnection (#32982)
- **Kimi Code CLI**: Multi-device session handoff (#2269)
- **CodeWhale**: No cross-session memory (#2492)
- **Gemini CLI**: Global cross-folder resume (#23490)

### 3.5 Memory System Reliability (3 of 9 tools)
- **Claude Code**: Facts forgotten across sessions (#66143, #59529)
- **Gemini CLI**: Auto Memory retry loops (#26522), pre-redaction leaks (#26525)
- **CodeWhale**: Cross-session memory gap (#2492)

### 3.6 Image/Clipboard Input Support (3 of 9 tools)
- **Claude Code**: Image paste broken on Windows (#66119)
- **GitHub Copilot CLI**: Clipboard image pasting (#1276)
- **Pi**: Image paste submits path only, not bytes (#5438)

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Qwen Code | Pi | CodeWhale |
|-----------|-------------|--------------|------------|-------------------|------------|-----|-----------|
| **Primary use case** | Full-stack dev, agentic coding | General AI coding assistant | Multi-agent workflows | Quick inline coding | Daemon-mode IDE integration | Extensible coding agent | DeepSeek-optimized TUI |
| **Target user** | Pro developers (Max subscribers) | Plus/Pro subscribers | Google ecosystem devs | GitHub ecosystem | Open-source/enterprise | Power users, extension devs | Cost-sensitive, DeepSeek users |
| **Key differentiator** | Most mature agent features | Broadest model access | Component-level eval framework | GitHub integration | ACP protocol, daemon mode | Composable architecture | Aggressive token efficiency |
| **Top pain point** | Billing opacity, compact bugs | macOS perf, WSL instability | Sub-agent reliability | Proxy auth, session stability | Network dependency, OOM | Provider fragility, cold start | Token waste, session freezes |
| **Community dynamic** | Frustrated but engaged | Turbulent, model trust eroding | Security-focused, maturing | Quiet, enterprise-oriented | Rapidly expanding, ambitious | Contributor-driven, active | Rebranding transition |
| **Release cadence** | Moderate | Moderate | Fast | Slow | **Very fast** (nightly) | Fast | Moderate |
| **Internationalization** | No evidence | No evidence | No evidence | No evidence | No evidence | No evidence | **Active** (7 locales in #2891) |

---

## 5. Community Momentum & Maturity

### Rapidly Maturing (High velocity, growing adoption)
- **Qwen Code**: **Fastest development cadence** (42 PRs/24h, nightly releases). Moving aggressively toward production-grade daemon architecture with ACP protocol, session management, and enterprise features. The most ambitious roadmap of any tool.
- **OpenCode**: Strong community engagement, v1.16.0 regression awareness, but rapid feature delivery. MCP ecosystem integration shows maturity.
- **Pi**: **Healthiest contributor dynamics** — multiple PRs from external developers, clean architectural improvements. Still smaller user base but solid foundations.

### Established but Struggling (High adoption, growing pains)
- **Claude Code**: **Most engaged user base** (#16157 at 1,400+ comments) but billing crisis eroding trust. Feature-rich but core reliability issues (compaction, memory) remain unresolved for months.
- **OpenAI Codex**: High visibility (510 👍 on Linux request) but facing **model trust issues** (gpt-5.5 404) and platform instability. WSL performance regression is a top blocker.

### Emerging / Stabilizing
- **Gemini CLI**: Security-aware development (command injection fixes, telemetry hardening). Component-level eval framework (#24353) signals QA maturity. Still establishing community.
- **CodeWhale (DeepSeek)**: Active community stabilization with 21 PRs in 24h, but **rebranding uncertainty** (#1969) creates risk of user churn. Strong Rust-based architecture.
- **Kimi Code CLI**: **Lowest momentum** — migration confusion (#2381, #2437) suppressing engagement. Strategic pivot from `kimi-cli` to `kimi-code` has fragmented the community.

### Quiet But Stable
- **GitHub Copilot CLI**: Lowest community activity, but likely large silent install base. Enterprise-focused features (BYOK, proxy support) suggest different engagement model.

---

## 6. Trend Signals

### ✅ Strong Signals (Validated by multiple tools)

1. **Protocol Standardization is Accelerating**
   - Qwen Code's ACP WebSocket + SSE transport parity (#4773)
   - OpenCode's MCP capability-aware connections (#31271)
   - Claude Code and Codex both exploring MCP plugin ecosystems
   - **Implication**: Cross-tool interoperability may become a competitive differentiator

2. **Agent Lifecycle Management is the New Battleground**
   - Background agents (Qwen #4780), sub-agent orchestration (Gemini #21409), session reapers (Qwen #4833)
   - Users want persistent, self-managing agents — not session-bound conversations
   - **Implication**: Tools that solve "set and forget" agent reliability will win power users

3. **Billing Transparency is a Trust Crisis**
   - 4 tools have active, high-engagement billing complaints
   - Failed API calls still costing users (#62466 in Claude Code)
   - Ambiguous free-tier limits (#15585 in OpenCode)
   - **Implication**: First tool to ship real-time usage dashboards with per-call cost breakdowns gains significant market advantage

4. **Cross-Platform Parity is Non-Negotiable**
   - Linux desktop is the #1 feature request across the ecosystem (820+ combined 👍)
   - Windows/WSL users face more bugs and limitations than macOS users
   - **Implication**: Tools that fail to prioritize Linux will alienate the developer core

### ⚠️ Warning Signals (Requires monitoring)

5. **Release Velocity Fatigue**
   - OpenCode user feedback: "You guys are coding too fast and it hurts" (#31267)
   - Kimi Code's rebuild-from-scratch eroding user trust
   - **Risk**: Rapid iteration without stability guarantees creates churn for production users

6. **Memory System Immaturity**
   - 3 tools report memory systems that forget, leak data, or loop infinitely
   - No tool has demonstrated reliable cross-session memory
   - **Risk**: Memory is a high-stakes feature — broken implementations cause more frustration than absence

7. **Enterprise Requirements Growing Faster Than Support**
   - Air-gapped initialization (Qwen #4550), SSL inspection (Copilot #333), Azure integration (OpenCode #31239)
   - BYOK, SSO, and compliance features are increasingly table stakes
   - **Risk**: Enterprise adoption will stall without dedicated investments in these areas

### 🧭 Strategic Recommendations for Developers

| If you care about... | Consider... |
|----------------------|-------------|
| **Feature velocity & bleeding-edge** | **Qwen Code** — fastest development, ambitious ACP/daemon roadmap |
| **Mature agent capabilities** | **Claude Code** — most sophisticated but prepare for billing frustrations |
| **Security & compliance** | **Gemini CLI** — security-first PRs, eval framework, active patching |
| **Enterprise / GitHub integration** | **Copilot CLI** + **OpenCode** — both targeting enterprise use cases |
| **Multi-provider flexibility** | **Pi** or **OpenCode** — best BYOK/Ollama support |
| **Cost efficiency** | **CodeWhale** — DeepSeek-optimized, but token waste issues need monitoring |
| **Cross-platform parity** | **Gemini CLI** or **Pi** — strongest Linux/Windows support currently |

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-06-08 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Skills have attracted the most community discussion and attention based on pull request activity:

### 1. document-typography (#514) — *Open*
**Functionality**: Prevents common typographic defects in AI-generated documents—orphan word wrap (1–6 words on a new line), widow paragraphs (section headers stranded at page bottoms), and numbering misalignment. Addresses pervasive formatting issues across all Claude-generated documents.
**Discussion**: Community members noted the skill solves a universal pain point; the author demonstrated the issues affect "every document Claude generates." Low controversy, high perceived value.
**Status**: Open | [View PR](https://github.com/anthropics/skills/pull/514)

### 2. ODT Skill — OpenDocument Text Creation (#486) — *Open*
**Functionality**: Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on mentions of ODT, ODS, ODF, OpenDocument, or LibreOffice.
**Discussion**: The primary discussion centered on ISO standard compliance and interoperability with LibreOffice workflows. Community interest was strong from enterprise users requiring ODF support.
**Status**: Open | [View PR](https://github.com/anthropics/skills/pull/486)

### 3. skill-quality-analyzer & skill-security-analyzer (#83) — *Open*
**Functionality**: Meta-skills that evaluate other skills across five dimensions: Structure & Documentation (20%), plus security analysis for vulnerability detection in skill definitions.
**Discussion**: Significant interest in skill governance and quality assurance. The meta-skill approach sparked debate about whether skills should self-evaluate or rely on external tooling.
**Status**: Open | [View PR](https://github.com/anthropics/skills/pull/83)

### 4. agent-creator Skill (#1140) — *Open*
**Functionality**: Meta-skill for generating task-specific agent sets. Includes fixes for multi-tool evaluation and Windows support for recalc.py via %APPDATA% paths.
**Discussion**: Addressed Issue #1120 regarding agent composition. The Windows compatibility fixes were particularly well-received by the community.
**Status**: Open | [View PR](https://github.com/anthropics/skills/pull/1140)

### 5. feature-dev Workflow Fix (#363) — *Open*
**Functionality**: Fixes the TodoWrite overwrite bug that caused Phase 6 (Quality Review) and Phase 7 (Summary) to be skipped during the `/feature-dev` workflow. Phase 5 creates task-level todos without incrementing the phase counter, causing subsequent phases to be missed.
**Discussion**: This became a high-traffic issue as multiple users reported incomplete workflow execution. The fix demonstrates a nuanced understanding of Claude Code's internal state management.
**Status**: Open | [View PR](https://github.com/anthropics/skills/pull/363)

### 6. n8n-builder & n8n-debugger (#190) — *Open*
**Functionality**: Four production-tested skills: **faf-expert** (Foundational AI-context Format files, CLAUDE.md bi-sync, MCP server configuration), **n8n-builder** (building n8n workflows from scratch), **n8n-debugger** (troubleshooting n8n workflows), and additional automation tooling.
**Discussion**: The n8n skills received strong engagement from automation-focused users. The faf-expert skill introduced novel concepts around persistent project context synchronization.
**Status**: Open | [View PR](https://github.com/anthropics/skills/pull/190)

### 7. testing-patterns Skill (#723) — *Open*
**Functionality**: Comprehensive testing coverage: Testing Trophy model, AAA pattern for unit tests, React component testing with Testing Library, edge case identification, and testing philosophy guidance.
**Discussion**: Community members debated the Testing Trophy vs. Testing Pyramid approaches. The skill's comprehensive scope was both praised (for completeness) and critiqued (for token efficiency).
**Status**: Open | [View PR](https://github.com/anthropics/skills/pull/723)

---

## 2. Community Demand Trends

Analysis of the most-discussed Issues reveals five clear demand directions:

### 🔴 Highest Urgency: Windows Compatibility
Multiple concurrent issues (#556, #1099, #1050, #1169) document that `run_eval.py` and `run_loop.py` are **unusable on Windows**—every query returns "not triggered," producing `precision=100%, recall=0%` on every iteration. This is the single largest blocker for Windows users.

### 🏢 Enterprise & Org Features
Issue #228 (13 comments, 7 👍) calls for **org-wide skill sharing** in Claude.ai. Users currently must download .skill files and manually distribute them via Slack/Teams. A shared skill library or direct sharing link is the top feature request.

### 🔒 Security & Trust Boundaries
Issue #492 (7 comments) raised a critical vulnerability: **community skills distributed under the `anthropic/` namespace** impersonate official skills. This trust boundary issue could lead to users granting elevated permissions to malicious skills. The community has high interest in namespace verification and skill provenance.

### 📄 Document & Office Format Support
Multiple PRs (#514, #486, #538, #541) and issues target document generation quality. Demand is concentrated on: typographic quality control, ODF/ODT format support, and fixing document corruption bugs (tracked change ID collisions in DOCX).

### 🧪 Meta-Skills & Tooling
Demand for skills that improve the skill ecosystem itself—quality analysis (#83), creator tooling (#539, #202), and evaluation pipeline fixes (#556, #1169). The community increasingly wants tooling to author, validate, and test skills reliably.

---

## 3. High-Potential Pending Skills

These PRs have active discussions and appear close to landing:

| PR | Skill | Key Discussion Point | Likelihood |
|----|-------|---------------------|------------|
| #514 | document-typography | Addresses universal AI document quality issue | **High** — minimal controversy, clear value |
| #509 | CONTRIBUTING.md | Closes #452 community health gap (25% score) | **High** — low complexity, high impact |
| #723 | testing-patterns | Comprehensive but long; token efficiency concern | **Medium-High** — needs scope trimming |
| #568 | ServiceNow platform | Broad enterprise scope; reviewers want narrower focus | **Medium** — may split into sub-skills |
| #1140 | agent-creator | Fixes critical evaluation bugs; Windows support | **Medium** — depends on #1120 resolution |
| #444 | AURELION skill suite | Four skills; cognitive framework concept is novel | **Medium** — needs integration testing |
| #154 | shodh-memory | Persistent cross-conversation memory | **Medium** — complexity concerns |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *infrastructure and quality tooling*—skills that fix bugs (Windows compatibility, document corruption, workflow state management), improve skill authoring (quality analysis, evaluation pipelines), and enable enterprise deployment (org-wide sharing, security boundaries)—rather than domain-specific functional skills.**

This signals a maturing ecosystem: early adopters have built functional skills; now they need the tooling to make those skills reliable, portable, and safe across platforms and organizations.

---

# Claude Code Community Digest — 2026-06-08

## Today's Highlights

The community remains heavily focused on usage-limits, billing, and compaction issues, with the top-voted bug (#16157) now exceeding 1,400 comments and 691 reactions. A new surge of Windows and Linux platform bugs—particularly around Cowork (desktop VM service), sandbox failures on merged-usr systems, and auth inconsistencies—dominate the 24-hour update window. No new releases were published today, but two long-standing PRs saw renewed activity.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#16157 — Instantly hitting usage limits with Max subscription](https://github.com/anthropics/claude-code/issues/16157)**  
   *Labels: bug, platform:macos, area:cost, area:api, oncall*  
   **1,476 comments | 691 👍**  
   The single most-discussed issue in the repository. Max subscribers report burning through their usage allowance within minutes of starting a session. Despite being filed in January, it continues to attract daily engagement with no resolution in sight. **Community sentiment: frustrated and demanding urgent billing transparency.**

2. **[#60366 — Saying "hi" returns "API Error: violates Usage Policy"](https://github.com/anthropics/claude-code/issues/60366)**  
   *Labels: bug, area:model*  
   **81 comments | 20 👍**  
   A simple greeting triggers a usage policy violation error. This suggests an overly aggressive content filter or a context poisoning bug. **Community sentiment: bewildered and concerned about false positives.**

3. **[#63896 — "Usage credits required for 1M context" compaction error on Windows](https://github.com/anthropics/claude-code/issues/63896)**  
   *Labels: bug, platform:windows, area:cost, area:core, api:anthropic*  
   **36 comments | 21 👍**  
   Users on Max subscriptions hitting a billing gate during automatic context compaction. Highlights a cross-billing-and-compaction failure path. **Community sentiment: annoyed that premium subscribers still see credit walls.**

4. **[#63015 — Auto-compact never triggers despite "100% context used"](https://github.com/anthropics/claude-code/issues/63015)**  
   *Labels: bug, has repro, platform:macos, area:core, regression*  
   **25 comments | 17 👍**  
   A clear regression: the statusline reports full context, but compact never fires, causing sessions to grow unbounded and eventually fail. **Community sentiment: confused by a broken core UX loop.**

5. **[#65697 — Official Claude Desktop build for Linux](https://github.com/anthropics/claude-code/issues/65697)**  
   *Labels: enhancement, platform:linux, area:desktop*  
   **22 comments | 310 👍**  
   The most upvoted **open** feature request. Linux users (Ubuntu/Debian) are asking for a native desktop client, not just the terminal CLI. **Community sentiment: strong demand; many feel left out of the desktop ecosystem.**

6. **[#13024 — Add hook for when Claude is waiting for user input](https://github.com/anthropics/claude-code/issues/13024)**  
   *Labels: enhancement, has repro, area:core*  
   **21 comments | 67 👍**  
   Developers want programmable hooks to know when the model pauses for input, enabling better automation and IDE integration. **Community sentiment: a clean API design request from power users.**

7. **[#25128 — Drag and drop not working in VS Code extension](https://github.com/anthropics/claude-code/issues/25128)**  
   *Labels: bug, has repro, platform:macos, area:ide*  
   **19 comments | 39 👍**  
   A regression since v2.1.6 that breaks file drag-and-drop in the VS Code chat panel; works fine in the terminal. **Community sentiment: annoyed at a long-standing regression in a core workflow.**

8. **[#62466 — Repeated "Image couldn't be processed" API errors consuming usage limit](https://github.com/anthropics/claude-code/issues/62466)**  
   *Labels: bug*  
   **18 comments | 16 👍**  
   Failed image processing calls still bill users, draining quotas silently. **Community sentiment: frustrated by non-retryable errors that still cost money.**

9. **[#32982 — Remote Control sessions die after ~20 min idle](https://github.com/anthropics/claude-code/issues/32982)**  
   *Labels: bug, has repro, platform:macos, platform:linux, area:networking*  
   **12 comments | 59 👍**  
   Remote Control (SSH) sessions silently disconnect after short idle periods despite keepalives. High upvote count suggests broad impact. **Community sentiment: blocking for remote-work workflows.**

10. **[#51041 — Request for 100x plan](https://github.com/anthropics/claude-code/issues/51041)**  
    *Labels: enhancement, area:cost (CLOSED)*  
    **12 comments | 4 👍**  
    A user offering to pay ~$600/month for a highest-tier plan. Closed, but reflects unmet demand for higher usage caps for power developers.

## Key PR Progress

_(Only 2 PRs had updates in the last 24h; all listed below.)_

1. **[#58673 — "s"](https://github.com/anthropics/claude-code/pull/58673)** (OPEN)  
   *Trivial PR with no real description.* Minimal community engagement. Likely spam or test submission.

2. **[#39370 — feat(plugins): add frontend-design-system plugin](https://github.com/anthropics/claude-code/pull/39370)** (CLOSED)  
   Adds a design-system plugin that generates wireframes, OKLCH color tokens, and design specs before writing code. Complements the existing `frontend-design` plugin. Interesting architectural direction for multi-phase code generation.

## Feature Request Trends

- **Linux Desktop Client (#65697, 310 👍)** — The strongest single ask. Linux developers want a native GUI app, not just the terminal CLI.
- **Higher-tier billing plans (#51041, #51141)** — Power users are hitting subscription caps and explicitly requesting 100x / ultra tiers at higher price points ($400–$600/month).
- **Programmatic hooks (#13024, 67 👍)** — Developers want fine-grained event hooks (waiting for input, permission approval override) for automation.
- **TTS / Voice mode for Remote Control (#42700, 12 👍)** — Accessibility and hands-free operation requests are emerging as a niche but organized ask.
- **Third-party provider context detection (#46416)** — Request to auto-detect context windows for non-Anthropic API providers (e.g., MiniMax), currently blocked by hardcoded 200K fallback.

## Developer Pain Points

- **Billing & Usage Transparency (dominant theme)** — Issue #16157 alone has 1,476 comments. Users report hitting limits instantly, being charged for failed API calls (#62466), and seeing credit walls during compaction (#63896). **This is the #1 community frustration.**
- **Auto-Compact Reliability (#63015, #65340)** — The compact feature is broken or never triggers for many users, causing sessions to grow until failure.
- **Cross-Platform Parity Gaps** — Windows users face unique failures: no image paste (#66119), Cowork VM service doesn't start (#64592), concurrent config file corruption (#64600). Linux users want a native desktop (#65697) and face sandbox issues on merged-usr systems (#64799).
- **Memory System Unreliability (#66143, #59529)** — Users report Claude Code forgetting saved facts across sessions despite the memory system, creating a loop of repeated corrections that drain context and tokens.
- **Content Filter False Positives (#60366)** — Saying "hello" or similar benign inputs triggering usage policy violations erodes trust in the model's safety system.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest
**Date:** 2026-06-08

---

## 1. Today's Highlights

The Codex community is experiencing significant turbulence this week, with a cluster of severe performance and stability issues dominating the issue tracker. A critical failure mode has emerged where `gpt-5.5` is listed as available in local metadata but returns 404 errors on actual requests, affecting both Desktop and CLI users globally. Additionally, macOS users are reporting a serious CPU/memory runaway caused by `syspolicyd`/`trustd` processes triggered by the Codex Desktop app, while several Windows users face entirely missing "Computer Use" and Chrome plugins after app restarts. On the development side, the team is actively merging PRs for persistent plugin catalog caching, stable item IDs for the Responses API, and a new Python SDK goal-turns feature.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Hot Issues

1. **[#11023: Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)** — *Enhancement, App* — The most-upvoted open feature request (510 👍, 100 comments). Users on Mac are experiencing severe power/latency issues linked to another bug, and the Linux community is asking for a native desktop client. This issue has been open since February but remains highly active.

2. **[#25715: Codex App Unusably Slow with WSL as Agent Environment](https://github.com/openai/codex/issues/25715)** — *Bug, Windows, Performance* — 36 comments in one week. Users with WSL2-backed sessions report "routine turns" taking minutes. The high comment velocity suggests this is a top regression for Windows developers using the agent mode.

3. **[#25719: Codex Desktop macOS triggers `syspolicyd`/`trustd` CPU and memory runaway](https://github.com/openai/codex/issues/25719)** — *Bug, macOS, Performance* — 19 comments. The app causes macOS system policy daemons to consume runaway CPU and RAM. Combined with issue #25243 (file descriptor exhaustion from locked files), macOS stability is a recurring pain point.

4. **[#26892: `gpt-5.5` listed as available but returns 404 "Model not found"](https://github.com/openai/codex/issues/26892)** — *Bug, Windows, CLI, App* — Opened just yesterday and already 12 comments. Users in multiple regions (Brazil, US) report that `gpt-5.5` appears in model listings but every request fails with a 404. A related closed issue (#18793) for `gpt-5.4` suggests this is a recurring pattern with new model rollouts.

5. **[#12299: "You've hit your usage limit" despite 10% rate limit remaining](https://github.com/openai/codex/issues/12299)** — *Bug, Rate Limits, Extension* — 19 comments. Users on Plus plans report false-positive rate limit errors. The community is frustrated by unclear quota accounting and weekly limit "rationing."

6. **[#4003: Patched files have mixed line endings on Windows](https://github.com/openai/codex/issues/4003)** — *Bug, Windows, Tool Calls* — Open since September 2025 with 48 👍 and 20 comments. This long-standing issue where Codex does not respect native line endings during file edits continues to affect Windows users.

7. **[#11881: GitHub PR review fails with "create a Codex account and connect to github"](https://github.com/openai/codex/issues/11881)** — *Bug, Auth, GitHub Action* — 16 comments. Users who have already connected their GitHub accounts are being asked to re-authenticate. This blocks CI/CD workflows.

8. **[#17265: MCP OAuth tokens not auto-refreshed even with stored refresh token](https://github.com/openai/codex/issues/17265)** — *Bug, Auth, MCP* — 13 comments. Once access tokens expire, all MCP tool calls fail with auth errors. The stored refresh tokens are not used automatically, forcing manual re-authentication.

9. **[#21232: Codex App freezes when opening image-heavy projects](https://github.com/openai/codex/issues/21232)** — *Bug, Windows, Performance* — 11 comments. Users with many generated images (e.g., via Imagen) see the app become "Not Responding." This impacts creative workflows.

10. **[#26929: Windows Codex Desktop: Computer Use / Chrome tools missing after intermittent helper-path failures](https://github.com/openai/codex/issues/26929)** — *Bug, Windows, Computer Use* — Filed today. The "Computer Use" plugins and Chrome integration are unstable or missing entirely on Windows, even when the underlying native pipe later initializes correctly. This is a fresh issue with high potential impact.

---

## 4. Key PR Progress

1. **[#26932: Use cached remote plugin catalog for plugin list](https://github.com/openai/codex/pull/26932)** — Reduces latency of `plugin/list` by serving from a local disk cache when the global catalog is already present. This addresses the sluggish plugin loading experience reported by many users.

2. **[#26920: Add Python SDK goal turns](https://github.com/openai/codex/pull/26920)** — Exposes `goal=True` on synchronous and asynchronous Python `run` and `turn` methods. Goals can now be started atomically and surfaced as logical SDK turns with stable IDs and rollover-aware control. Significant for programmatic Codex users.

3. **[#25976: Use stable item IDs for Responses API calls](https://github.com/openai/codex/pull/25976)** — Enables stable item IDs for items round-tripping between Codex and the Responses API. This improves traceability and debugging for both client- and server-originated items.

4. **[#26831: Add global instructions contributor API](https://github.com/openai/codex/pull/26831)** — Introduces a small extension point for hosts to supply global instructions outside of `Config`. This decouples instructions from core configuration loading, enabling more flexible plugin-based setup.

5. **[#26830: Characterize global instruction lifecycle](https://github.com/openai/codex/pull/26830)** — Adds end-to-end coverage for global instruction behavior across thread creation, turns, compaction, resume, forks, and subagents. Necessary groundwork before moving global instructions out of `Config`.

6. **[#25232: Derive window generation from effective rollout lineage](https://github.com/openai/codex/pull/25232)** — Fixes `x-codex-window-id` generation after rollbacks, resumes, and retained-history forks. Prevents incorrect window lineage reconstruction, which could corrupt compaction behavior.

7. **[#26852: Avoid blocking connection cleanup in app-server](https://github.com/openai/codex/pull/26852)** — Fixes a bug where remote-control sessions reconnect every 5-7 seconds because the transport-event queue's `ConnectionClosed` handler blocks on stuck RPCs, preventing cleanup of replacement connections.

8. **[#26859: Auto-recover from corrupted SQLite databases](https://github.com/openai/codex/pull/26859)** — Addresses corruption incidents caused by a recent SQLite upgrade. The fix acknowledges data loss is inevitable in corrupted databases but adds automatic recovery pathways, since data can be reconstructed from other sources.

9. **[#26917: Support marketplace metadata for git plugins](https://github.com/openai/codex/pull/26917)** — Git-sourced marketplace entries now show `displayName`, `description`, and `keywords` in `plugin/list` before installation. Previously, these were invisible until the plugin was installed locally.

10. **[#26287: Refine Guardian prompt for indirect exfiltration](https://github.com/openai/codex/pull/26287)** — Strengthens the Guardian security policy against indirect data exfiltration, focusing on sensitive data, authorization, and egress. Preserves user approvals for personal data while tightening rules for credentials and private organization data.

---

## 5. Feature Request Trends

- **Linux Desktop App (#11023):** The #1 most-requested feature with 510 👍. Users on Mac are fleeing due to power/performance bugs, and Linux users want a native experience.
- **General User / Non-Developer Mode (#26556):** A new suggestion for "Claim Gates" that would simplify the Codex interface for domain experts who are not software engineers. Highlights the tension between Codex's developer-optimized diff/log UX and its growing non-technical user base.
- **Persistent Plugins & State:** Multiple issues request that Computer Use, Chrome integration, and MCP OAuth sessions survive app restarts without requiring manual reinstall or re-login.
- **Better Rate Limit Transparency (#12299, #26512):** Users are demanding real-time, accurate quota usage displays and investigation into passive quota drain when not actively using Codex.

---

## 6. Developer Pain Points

- **Windows & WSL Instability:** The most recurring theme. From app slowness (#25715) to missing plugins (#25962, #26929), mixed line endings (#4003), and file path resolution bugs (#24268), Windows/WSL users face the highest friction.
- **Model Availability vs. Reality:** The `gpt-5.5` 404 bug (#26892) is a systemic trust issue: users cannot rely on the model listing UI. The same pattern occurred with `gpt-5.4` (#18793). This erodes confidence during critical workflow moments.
- **macOS System Resource Abuse:** Two distinct bugs (#25719, #25243) show the macOS Desktop app triggering kernel daemon CPU runaway and file descriptor exhaustion. The "locked use" pattern suggests internal file handle management issues.
- **Session & Thread Loss (#25500, #25463, #15122):** Conversations silently disappear from the UI while remaining on disk, forcing users to manually recover JSONL files. Combined with MCP OAuth persistence failures (#17265), session reliability is severely compromised.
- **MCP & Plugin Lifecycle:** Plugins that vanish after restart (#25809), auth tokens that don't refresh (#17265), and OAuth logins that don't persist (#15122) create a repeating cycle of setup frustration for power users.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-08

## Today's Highlights
No new releases were published in the last 24 hours, but the development pipeline remains active with 14 pull requests and 50 open issues receiving updates. Today's activity leans heavily toward security hardening (command injection fixes, telemetry truncation), terminal stability (MIME type sniffing, render flicker), and the ongoing effort to mature the Auto Memory and sub-agent systems. A new changelog automation guide was also introduced to improve release note hygiene.

## Releases
*No new releases in the last 24 hours.*

---

## Hot Issues

### 1. Agent Hangs on Sub-agent Deferral
**#21409** — Users report that `gemini-cli` hangs indefinitely when it defers to the generalist agent. Simple operations like folder creation become stuck for up to an hour. Workaround: explicitly instruct the model not to use sub-agents. High community impact (8 👍).  
🔗 [Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)

### 2. Sub-agent MAX_TURNS Misreported as Success
**#22323** — The `codebase_investigator` sub-agent hits its turn limit but reports `status: "success"` with `Termination Reason: "GOAL"`, masking the interruption from downstream logic. A reliability regression that undermines trust in agent completion signals.  
🔗 [Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)

### 3. Shell Commands Get Stuck in "Waiting Input" After Completion
**#25166** — After executing simple CLI commands (e.g., `ls`), the shell command remains marked as active and "Awaiting user input" even though the process has finished. Causes the agent to hang and prevents further steps. 3 👍.  
🔗 [Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)

### 4. 400 Error with >128 Tools
**#24246** — When more than ~128 tools are enabled, Gemini CLI receives a 400 error from the API. Users expect the agent to be smarter about limiting tool scope rather than sending everything at once.  
🔗 [Issue #24246](https://github.com/google-gemini/gemini-cli/issues/24246)

### 5. Auto Memory Indefinitely Retries Low-Signal Sessions
**#26522** — Auto Memory only marks a session as "processed" when the extraction agent successfully reads it. If the agent decides a session is low-signal and skips it, that session reappears indefinitely, creating noisy repeated processing cycles.  
🔗 [Issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522)

### 6. Auto Memory Logging Leaks Secrets Before Redaction
**#26525** — Auto Memory reads local transcripts and sends content to the extraction model before the redaction prompt is applied. The service can also log existing skill results. A security concern regarding secret exposure in model context and logs.  
🔗 [Issue #26525](https://github.com/google-gemini/gemini-cli/issues/26525)

### 7. Browser Agent Fails on Wayland
**#21983** — The browser sub-agent crashes under Wayland display servers. Termination reason shows "GOAL" but the agent outputs no useful result. A compatibility gap for Linux users on modern display stacks.  
🔗 [Issue #21983](https://github.com/google-gemini/gemini-cli/issues/21983)

### 8. Temp Scripts Litter File System
**#23571** — When restricted from direct shell execution, the model creates numerous temporary edit scripts in random directories. Users report significant cleanup overhead before committing.  
🔗 [Issue #23571](https://github.com/google-gemini/gemini-cli/issues/23571)

### 9. Corrupted Terminal After External Editor Exit
**#24935** — Exiting an external editor in `terminalBuffer` mode leaves the terminal display corrupted. A full Ink-side screen refresh is missing. Affects users who rely on external editors for multi-line input.  
🔗 [Issue #24935](https://github.com/google-gemini/gemini-cli/issues/24935)

### 10. Component-Level Evaluation Framework (Epic)
**#24353** — The epic tracking the evolution from 76 behavioral eval tests toward robust, component-level evaluations across 6 supported Gemini variants. Foundational for quality assurance as the agent ecosystem grows.  
🔗 [Issue #24353](https://github.com/google-gemini/gemini-cli/issues/24353)

---

## Key PR Progress

### 1. MCP Image MIME Type Sniffing (Closed)
**#27733** — Sniffs magic bytes before sending MCP image/resource inline data to the model, correcting misreported WebP/PNG/JPEG/GIF MIME types. Adds regression coverage for image blocks.  
🔗 [PR #27733](https://github.com/google-gemini/gemini-cli/pull/27733)

### 2. Telemetry Attribute Truncation for GCP Export
**#27729** — Truncates telemetry metric attributes to 1024 characters to prevent GCP Monitoring export errors that flood the terminal with Node.js stack traces.  
🔗 [PR #27729](https://github.com/google-gemini/gemini-cli/pull/27729)

### 3. Keep Array Tool Results Out of structuredContent
**#27730** — Fixes `McpComplianceTransport` inadvertently copying JSON arrays into `structuredContent`, which broke calendar-style payloads. Fixes #27725.  
🔗 [PR #27730](https://github.com/google-gemini/gemini-cli/pull/27730)

### 4. Prevent Stack Overflow from Regex Backtracking
**#27580** — Replaces a complex regex-based `@` command parser with an iterative scanner to avoid catastrophic backtracking on large pasted inputs. Fixes #27539.  
🔗 [PR #27580](https://github.com/google-gemini/gemini-cli/pull/27580)

### 5. Command Injection Prevention in findCommand
**#27575** — Replaces shell-interpolated `execSync` calls with safe `spawnSync`/`spawn` in two files (`ide-installer.ts` and `editor.ts`), preventing command injection via shell metacharacters.  
🔗 [PR #27575](https://github.com/google-gemini/gemini-cli/pull/27575)

### 6. Oversized Bug Report URL Fallback
**#27591** — Fixes `/bug` command crash on Android/Termux by splitting oversized GitHub issue URLs that exceed deep-link/intent limits.  
🔗 [PR #27591](https://github.com/google-gemini/gemini-cli/pull/27591)

### 7. Changelog Automation Guide
**#27735** — Adds a maintenance guide for the automated release notes system, including troubleshooting steps for common failures. Aids handoff and reviewer efficiency.  
🔗 [PR #27735](https://github.com/google-gemini/gemini-cli/pull/27735)

### 8. Keep Auto Alias Visible Without Preview Access
**#27718** — Marks the top-level `auto` alias as non-preview so it remains visible in `/model` when dynamic model configuration is enabled, without leaking preview-only models.  
🔗 [PR #27718](https://github.com/google-gemini/gemini-cli/pull/27718)

### 9. Global Cross-Folder Session Resume (Closed)
**#23490** — Makes `gemini --resume <session-id>` work across folders instead of only within the original project. Also improves interactive startup UX around mismatched-folder resume.  
🔗 [PR #23490](https://github.com/google-gemini/gemini-cli/pull/23490)

### 10. Node 20 Compatibility & Windows Symlink Fix (Closed)
**#27385** — Fixes a `URL.parse` crash on Node 20.x and resolves platform-specific symlink test failures on Windows.  
🔗 [PR #27385](https://github.com/google-gemini/gemini-cli/pull/27385)

---

## Feature Request Trends

- **AST-Aware Code Analysis** — Multiple issues (#22745, #22746, #22747) advocate for AST-aware file reads, search, and codebase mapping to reduce token usage and improve method-level precision compared to line-based tools.
- **Sub-agent & Skill Self-Discovery** — Users want agents to autonomously determine when to use custom skills and sub-agents (#21968, #21432) without explicit instruction, improving the "set and forget" experience.
- **Remote & Background Agents** — The Remote Agents sprint (#20303) and detached task execution in A2A (#15674) signal a shift toward persistent, cloud-connected agent workflows with task-level auth.
- **Memory System Maturation** — Auto Memory improvements dominate feature requests: deterministic redaction (#26525), low-signal session quarantine (#26522), and invalid patch handling (#26523) point toward making memory persistent, safe, and non-noisy.
- **Browser Agent Resilience** — Automatic session takeover and lock recovery (#22232) is a recurring ask, especially for users relying on persistent browser profiles.

---

## Developer Pain Points

- **Agent Reliability** — Hangs (#21409), false success reports (#22323), and sub-agents running without permission (#22093) erode trust in autonomous operation. These are the most-upvoted and most-discussed issues.
- **Security & Data Leakage** — Two distinct security concerns emerged: Auto Memory sending pre-redaction content to models (#26525) and command injection vectors in shell execution (#27575). Both are being actively patched.
- **Terminal & UI Stability** — Corruption after external editor exit (#24935), flicker on resize (#21924), and stuck "Waiting input" states (#25166) suggest the Ink-based terminal rendering layer needs hardening.
- **Tool & Configuration Management** — The 400 error with >128 tools (#24246), settings.json overrides being ignored by the browser agent (#22267), and destructive git operations (#22672) highlight gaps in tool-scoping and configuration enforcement.
- **Workspace Cleanliness** — The model's tendency to scatter temporary scripts across the filesystem (#23571) creates friction for users who want clean commits and minimal side effects.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — June 8, 2026

## Today's Highlights

The community is actively requesting deeper model flexibility, with a notable new feature request to allow switching between **BYOK/local providers and GitHub-hosted models within a single session**. Additionally, a bug affecting ongoing long-running sessions—where the agent enters an infinite compaction/directory-listing loop—has drawn attention and a refund request. On the platform side, a newly surfaced issue reveals the installation script misidentifies FreeBSD as Windows, blocking adoption on that platform.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **Pasting images from clipboard into prompts** — [#1276](https://github.com/github/copilot-cli/issues/1276)  
   Highly upvoted (👍 8) feature request to support pasting screenshots or UI bug images directly into CLI prompts. Community discussion (11 comments) reflects strong demand for richer multi-modal input.

2. **SSL inspection issue in corporate environments** — [#333](https://github.com/github/copilot-cli/issues/333)  
   Long-standing bug (open since Oct 2025) causing “fetch failed” errors behind MITM proxies. Affects enterprise users with macOS and properly installed certificates. Reopened discussion suggests this remains a blocker for corporate adoption.

3. **Weekly rate limiting feedback** — [#2828](https://github.com/github/copilot-cli/issues/2828) (CLOSED)  
   User requested that rate-limit messages include suggestions on how to proceed. Closed but the community sentiment shows frustration over opaque rate-limiting UX.

4. **Infinite session loop / compaction bug** — [#3216](https://github.com/github/copilot-cli/issues/3216)  
   A 136-turn session entered an infinite loop of directory-tree listing and context compaction. Author requested a refund. Highlights reliability risks for long or complex exploratory sessions, especially with model Claude Sonnet 4.6.

5. **Linux distribution packaging license clarification** — [#2294](https://github.com/github/copilot-cli/issues/2294)  
   Arch Linux maintainer seeks clarification on Section 2 of the license to enable packaging in distro repos. Community signals desire for broader open-source distribution.

6. **`/model` command not listing BYOK providers** — [#3709](https://github.com/github/copilot-cli/issues/3709)  
   Newly opened feature request (June 7) where the model picker only shows GitHub-hosted models even when a local BYOK provider is configured. Author wants seamless switching in one session.

7. **ReFS / Dev Drive local-sandbox limitation on Windows** — [#3712](https://github.com/github/copilot-cli/issues/3712)  
   A documentation request about local-sandbox incompatibility with ReFS/Dev Drive on Windows. Not yet confirmed as a Copilot CLI bug, but important for Windows developers using modern filesystems.

8. **Windows Registry version not updated after `/update`** — [#3711](https://github.com/github/copilot-cli/issues/3711)  
   Bug report that after updating to v1.0.60, the Registry entry still shows the old version. Minor but causes confusion during deployment or version tracking.

9. **Install script misidentifies FreeBSD as Windows** — [#3710](https://github.com/github/copilot-cli/issues/3710)  
   The installation script at `gh.io/copilot-install` incorrectly falls through to a Windows-check after excluding Linux, Android, and Darwin, leading to errors on FreeBSD. Blocks FreeBSD users from installing.

10. **Confusing error with GITHUB_TOKEN in GitHub Actions** — [#3396](https://github.com/github/copilot-cli/issues/3396) (CLOSED)  
    When `GITHUB_TOKEN` (or `GH_TOKEN`) is set in Actions, the CLI forwards it to the Copilot backend, which rejects it with a 400 error. Closed but underscores the need for better environment variable detection.

## Key PR Progress

Only **one PR** was updated in the last 24 hours:

- **Add files via upload** — [#3708](https://github.com/github/copilot-cli/pull/3708)  
  Opened by a new contributor with no description or comments. Likely a documentation or configuration file update requiring review.

## Feature Request Trends

The most requested feature directions, distilled from recent issues:

- **Multi-model switching within a single session**, spanning GitHub-hosted and BYOK/local providers — driven by #3709 and #1276.
- **Image/multimodal clipboard support** in prompts (screenshots, UI bugs, logs) — #1276 is a top-voted request.
- **Improved rate-limiting UX** with clear suggestions on how to proceed — #2828 is closed but sentiment persists.
- **License updates** to permit Linux distribution packaging (Arch Linux, others) — #2294.
- **Better enterprise networking support**, particularly for SSL-inspected proxies — #333 remains open.

## Developer Pain Points

Recurring frustrations and high-frequency requests emerging from the community:

- **Corporate proxy/SSL inspection blocks** — enterprise users remain unable to connect even with properly installed certificates (#333).
- **Session stability** — long-running sessions (136+ turns) can trigger infinite loops or resource exhaustion (#3216).
- **Script installation platform detection** — the curl installer fails on FreeBSD and potentially other uncommon OSes (#3710).
- **Environment variable collision in CI/CD** — `GITHUB_TOKEN` being silently forwarded causes opaque errors in Actions (#3396).
- **Windows-specific issues** — Registry versioning (#3711) and ReFS/Dev Drive sandbox limitations (#3712) suggest uneven Windows QA coverage.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-08

## Today's Highlights
Migration confusion and community frustration dominate today's digest as MoonshotAI pushes users from `kimi-cli` to `kimi-code`. A surge of bug reports around agentic session handling, installation ambiguity, and local model compatibility suggests the transition is causing real friction. Meanwhile, feature requests for cross-device session handoff and clickable symbol navigation highlight growing expectations for a more mature IDE-like CLI experience.

## Releases
No new releases in the last 24 hours. The latest tagged version remains **kimi-code v0.11.0**.

## Hot Issues

1. **[#2381 — Why abandon kimi-cli and redo kimi code? The old one didn't do a good job and still divides the community?](https://github.com/MoonshotAI/kimi-cli/issues/2381)** [CLOSED]  
   A heated discussion questioning MoonshotAI's strategic pivot. The author argues that splitting the community and rebuilding from scratch erodes trust in the tool as a long-term productivity investment. Closed without a public resolution.

2. **[#2437 — Migration Feedback: unclear state migration, quota attribution confusion, and possible agent quality regression](https://github.com/MoonshotAI/kimi-cli/issues/2437)** [OPEN]  
   A detailed Fedora Linux user report documenting how `kimi-cli v1.47.0` was replaced by `kimi-code v0.11.0`. The user notes unclear migration state, lost quota attribution, and potential degradation in agent output quality.

3. **[#2436 — Installation failed. The new Kimi Code is installed ✓ Kimi can't seem to make up her mind.](https://github.com/MoonshotAI/kimi-cli/issues/2436)** [OPEN]  
   A confusing install experience where the CLI reports success and failure simultaneously. The user notes `kimi-cli -V` still shows the old version (1.47.0) after the new installer ran.

4. **[#2438 — Status of agent unknown. It is not possible to dive in agentic session to overview.](https://github.com/MoonshotAI/kimi-cli/issues/2438)** [OPEN]  
   On Fedora 42, after starting a dialogue, the agent session becomes opaque — users cannot inspect or navigate within an ongoing agentic workflow, making debugging near impossible.

5. **[#2269 — Remote Control / Multi-Device Session Handoff](https://github.com/MoonshotAI/kimi-cli/issues/2269)** [OPEN]  
   A highly requested feature (5 comments) for seamless session migration across laptop, web, and mobile. No upvotes yet, but the use case resonates with multi-environment power users.

6. **[#2439 — compaction.unable error when reviewing project with local Ollama model](https://github.com/MoonshotAI/kimi-cli/issues/2439)** [OPEN]  
   Using a local Ollama model triggers a cryptic `compaction.unable` error during project review. This indicates incomplete support for custom/local model backends.

7. **[#2440 — Clickable symbol / line references in Kimi Code chat panel](https://github.com/MoonshotAI/kimi-cli/issues/2440)** [OPEN]  
   While file paths are clickable, function/method names are not. Users want IDE-style "jump to definition" from chat output — a significant ergonomic gap for code exploration.

8. **[#2381 (continued reaction)]** — Several users across threads express concern that MoonshotAI is rewriting rather than iterating, suggesting a lack of confidence in the existing codebase.

9. **Quota attribution confusion (from #2437)** — Migration silently reassigns or loses quota visibility, making users unsure whether they are being double-billed or losing unused credits.

10. **Agent quality regression suspicion (from #2437)** — The same user reports that after migration, agent responses feel less capable, hinting at either a model switch or degraded context handling.

## Key PR Progress

1. **[#774 — fix: correct module-name type in pyproject.toml](https://github.com/MoonshotAI/kimi-cli/pull/774)** [CLOSED, updated 2026-06-07]  
   Fixes a TOML parsing error where `module-name` was incorrectly declared as a sequence instead of a string, breaking `make prepare`. Merged.

## Feature Request Trends
- **Multi-device session portability** (#2269) is the most ambitious request — users want true cloud-backed session persistence and remote control.
- **IDE-level navigation** (#2440) — clickable symbol references in chat output reflect a demand for deep codebase integration beyond simple file opening.
- **Local model compatibility** (#2439) — users expect first-class support for Ollama and other local inference engines, especially for offline or privacy-sensitive workflows.

## Developer Pain Points
- **Migration confusion** dominates: users are unclear whether they should stay on `kimi-cli` or move to `kimi-code`, with conflicting status messages and no clear rollback path.
- **Agent session opacity** (#2438) — once in an agentic loop, users lose visibility into what the model is doing, making fault diagnosis impossible.
- **Regression fears** (#2381, #2437) — the community suspects quality degradation in the new codebase, undermining trust in the product's reliability as a daily driver.
- **Installation ambiguity** (#2436) — the installer claims success while the old binary remains active, creating silent inconsistency that will confuse less experienced users.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-08

## Today's Highlights

Development velocity remains extremely high, with v1.16.0 introducing a significant regression for AWS Bedrock SSO users and a broken MCP toggle in Desktop. Community attention is concentrated on two long-unresolved issues: sandboxing agent terminal access (63 comments, 51 upvotes) and free model usage limits. The team is actively merging fixes across Desktop WSL support, MCP server capability handling, and plugin auto-update cleanup.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#2242 – Sandbox agent terminal access](https://github.com/anomalyco/opencode/issues/2242)** (OPEN, 63 comments, 51 👍)  
   *Long-running request to restrict agent file-system access.* Users compare with gemini-cli and codex-cli seatbelt implementations. High engagement suggests this is a blocking concern for security-conscious teams.

2. **[#15585 – Free model "usage exceeded" errors](https://github.com/anomalyco/opencode/issues/15585)** (CLOSED, 47 comments, 12 👍)  
   *All three free models fail with ambiguous limits.* Community confusion persists despite closure — related issue [#14273](https://github.com/anomalyco/opencode/issues/14273) remains open with Zen balance not being respected.

3. **[#3472 – Context awareness not working](https://github.com/anomalyco/opencode/issues/3472)** (CLOSED, 37 comments, 25 👍)  
   *VS Code selection not passed to the agent.* High upvote count indicates this is a core UX expectation. Documentation gap also flagged.

4. **[#10221 – Black screen on fresh install](https://github.com/anomalyco/opencode/issues/10221)** (CLOSED, 29 comments, 16 👍)  
   *Terminal rendering failure.* Affects both macOS and Windows. Re-emerges across versions — see also [#14334](https://github.com/anomalyco/opencode/issues/14334) (21 comments, 28 👍).

5. **[#29059 – Dynamic workflows feature request](https://github.com/anomalyco/opencode/issues/29059)** (OPEN, 10 comments, 12 👍)  
   *Equivalent to Claude Code's multi-step automation.* Duplicate [#30308](https://github.com/anomalyco/opencode/issues/30308) confirms strong demand for project-local repeatable workflows.

6. **[#31239 – Azure Foundry connectivity confusion](https://github.com/anomalyco/opencode/issues/31239)** (CLOSED, 11 comments)  
   *No clear docs for Azure OpenAI endpoint setup.* Related [#13999](https://github.com/anomalyco/opencode/issues/13999) (OPEN, 9 comments) adds the specific Responses API versioning bug.

7. **[#11829 – RLM context management](https://github.com/anomalyco/opencode/issues/11829)** (OPEN, 5 comments, 11 👍)  
   *Treat context as external environment per MIT's RLM paper.* Forward-looking proposal with strong signal-to-noise ratio.

8. **[#25848 – Session renaming](https://github.com/anomalyco/opencode/issues/25848)** (OPEN, 7 comments)  
   *Manual session rename via /rename or CLI.* Small but persistent quality-of-life request.

9. **[#31217 – TUI Enter key swallowing input](https://github.com/anomalyco/opencode/issues/31217)** (OPEN, 4 comments)  
   *Pressing Enter clears input without submitting.* Affects both Chinese and English text. Slash commands work fine — suggests focus-related bug.

10. **[#31203 – MCP toggle unresponsive in Desktop](https://github.com/anomalyco/opencode/issues/31203)** (OPEN, 4 comments)  
    *v1.16.0 regression — MCP toggle visible but does nothing.* Related to earlier v1.15.x fix for MCP not showing at all.

## Key PR Progress

1. **[#31095 – Desktop WSL bug fixes](https://github.com/anomalyco/opencode/pull/31095)** (CLOSED)  
   *Fixes `can't access distroReady before initialization`, stale sidebar, and version reporting.* Addresses the most common WSL regression pattern.

2. **[#31283 – Snapshot sidecar lifecycle stabilization](https://github.com/anomalyco/opencode/pull/31283)** (OPEN)  
   *Prevents Git index lock blocking snapshots and terminates stale Desktop server references.* Solves a silent failure class in snapshot capture.

3. **[#31211 – Replace solid-primitives/scheduled with manual debounce](https://github.com/anomalyco/opencode/pull/31211)** (OPEN)  
   *Critical Node.js compat fix — `@solid-primitives/scheduled` returns no-op under `isServer=true`.* Blocks server-side rendering scenarios.

4. **[#31271 – Respect MCP server capabilities](https://github.com/anomalyco/opencode/pull/31271)** (OPEN)  
   *Only connect tool/prompt/resource handlers when server advertises them.* Prevents unnecessary `tools/list` calls on resource-only servers.

5. **[#26167 – Retry empty stream truncations](https://github.com/anomalyco/opencode/pull/26167)** (OPEN)  
   *Discards partial parts from upstream providers that end without `stop_reason`.* Mitigates silent session truncation.

6. **[#28301 – Cache unsupported MCP prompt lists](https://github.com/anomalyco/opencode/pull/28301)** (OPEN)  
   *Prevents repeated `-32601` failures for servers without `prompts/list`.* Reduces latency in MCP-heavy sessions.

7. **[#28308 – Strip reasoning from OpenAI-compatible history](https://github.com/anomalyco/opencode/pull/28308)** (OPEN)  
   *Removes non-standard fields rejected by strict providers.* Unblocks compatibility with Gemini, Mistral, and others.

8. **[#30849 – Strip MiniMax trailing tool_call leak](https://github.com/anomalyco/opencode/pull/30849)** (OPEN)  
   *Sanitizer for MiniMax response artifact where assistant text ends with leaked tool-call marker.* Model-specific fix for a common annoyance.

9. **[#27231 – Edit button for connected providers](https://github.com/anomalyco/opencode/pull/27231)** (OPEN)  
   *Allows modifying provider configuration post-setup.* Long-requested feature (#20598) — simplifies credential rotation.

10. **[#26239 – /menu slash command](https://github.com/anomalyco/opencode/pull/26239)** (CLOSED)  
    *Opens TUI command menu via `/menu`, equivalent to Ctrl+P.* Accessibility win for users who prefer keyboard-driven navigation.

## Feature Request Trends

- **Dynamic Workflows**: Two separate issues ([#29059](https://github.com/anomalyco/opencode/issues/29059), [#30308](https://github.com/anomalyco/opencode/issues/30308)) request Claude Code-style multi-step project-local automation. High overlap suggests this should be consolidated.
- **Context-Aware Agents**: Persistent demand for VS Code selection integration ([#3472](https://github.com/anomalyco/opencode/issues/3472), [#3095](https://github.com/anomalyco/opencode/issues/3095)) and neovim/TUI context polling ([#26234](https://github.com/anomalyco/opencode/pull/26234)). Users expect the agent to "see" what they're working on.
- **Advanced Context Management**: The RLM paradigm proposal ([#11829](https://github.com/anomalyco/opencode/issues/11829)) with 11 👍 in 5 comments indicates developer appetite for architectural improvements beyond simple compaction.
- **Desktop Quality-of-Life**: Session renaming ([#25848](https://github.com/anomalyco/opencode/issues/25848)), minimize-to-tray ([#18134](https://github.com/anomalyco/opencode/issues/18134)), and LaTeX rendering ([#24426](https://github.com/anomalyco/opencode/issues/24426)) reflect maturing expectations for the Desktop client.
- **MCP Ecosystem**: Requests for MCP toggle fixes, capability-aware connections, and prompt-list caching signal growing reliance on external servers.

## Developer Pain Points

1. **Free Model Limitations**: Ambiguous "free usage exceeded" errors ([#15585](https://github.com/anomalyco/opencode/issues/15585), [#14273](https://github.com/anomalyco/opencode/issues/14273)) with no clear documentation on limits. Zen balance not being respected adds confusion.
2. **AWS Bedrock SSO Regression**: v1.16.0 broke SSO entirely ([#31147](https://github.com/anomalyco/opencode/issues/31147)) with a Symbol-related credential provider crash blocker for enterprise AWS users.
3. **MCP Reliability**: Toggle not working in Desktop v1.16.0 ([#31203](https://github.com/anomalyco/opencode/issues/31203)), empty MCP lists in web UI ([#30487](https://github.com/anomalyco/opencode/issues/30487)), and servers not registering capabilities.
4. **Context Compaction Bugs**: Pruning clears read results causing instruction re-attachment ([#30807](https://github.com/anomalyco/opencode/issues/30807)), and orchestration leakage during compaction ([#28355](https://github.com/anomalyco/opencode/issues/28355)) erodes confidence in long sessions.
5. **Azure OpenAI Integration**: Missing `?api-version=` on Responses API ([#13999](https://github.com/anomalyco/opencode/issues/13999)) plus unclear docs ([#31239](https://github.com/anomalyco/opencode/issues/31239)) — Azure remains a second-class provider despite high enterprise demand.
6. **Release Velocity Overwhelm**: User feedback in [#31267](https://github.com/anomalyco/opencode/issues/31267) ("You guys are coding too fast and it hurts") captures frustration with churn between versions breaking workflows.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-08

## Today's Highlights
The Pi ecosystem saw a burst of activity focused on **developer experience refinements** and **coding-agent API surface improvements**. Multiple PRs from contributor `dyyz1993` landed improvements to context usage estimation and bash tool safety. A key bug-fix landed to prevent unconditional `agent.continue()` after compaction, which had been causing errors in plan-mode workflows. The community also rallied around quality-of-life features like day-of-week injection and configurable image storage paths.

## Releases
No new releases were published in the last 24 hours.

## Hot Issues

1. **#5223 — Anthropic provider modifies thinking blocks (Opus 4.8)**  
   *15 comments, 6 👍*  
   Multi-turn conversations with Claude Opus 4.8 adaptive thinking fail with 400 errors because the provider modifies `thinking` blocks in the latest assistant message. A high-impact bug for users relying on extended reasoning models.  
   [GitHub](https://github.com/earendil-works/pi/issues/5223)

2. **#5188 — shift+enter submits instead of creating new line**  
   *8 comments, 2 👍*  
   Despite keybinding config specifying `shift+enter` for new line, the TUI submits instead. `ctrl+j` works correctly. A frustrating inconsistency for power users.  
   [GitHub](https://github.com/earendil-works/pi/issues/5188)

3. **#5464 — Local models: 3-5 minute "Working" latency mid-session**  
   *3 comments*  
   Even simple messages like "Hi" incur a multi-minute `Working` status when using Ollama-backed local models. Points to a fundamental performance issue in the local model loop.  
   [GitHub](https://github.com/earendil-works/pi/issues/5464)

4. **#5431 — API key for DeepSeek not found after save**  
   *4 comments*  
   A user reports that saved DeepSeek credentials are not recognized after a restart — the auth flow appears to have a persistence bug.  
   [GitHub](https://github.com/earendil-works/pi/issues/5431)

5. **#5402 — Slow cold start: eager provider SDK loading adds ~2.4s**  
   *2 comments*  
   Even with `--no-extensions`, Pi takes ~2.4 seconds just to load 138MB of provider SDKs. A significant anti-pattern for quick-start users.  
   [GitHub](https://github.com/earendil-works/pi/issues/5402)

6. **#5428 — Refining a plan leads to error in plan mode**  
   *3 comments, 1 👍*  
   Using the example plan mode, refining a plan triggers `Agent is already processing` — related to the `continue()` post-compaction bug (fixed today in #5471).  
   [GitHub](https://github.com/earendil-works/pi/issues/5428)

7. **#5456 — openai-responses provider ignores `compat.supportsDeveloperRole`**  
   *3 comments*  
   The `openai-responses` API style always sends system prompt as `role: "developer"` when reasoning is enabled — even when the model explicitly says it doesn't support it.  
   [GitHub](https://github.com/earendil-works/pi/issues/5456)

8. **#5438 — Clipboard image paste only submits temp file path**  
   *2 comments*  
   In interactive mode, pasting an image inserts the file path but never attaches the actual image bytes to the model request. Completely breaks vision workflows.  
   [GitHub](https://github.com/earendil-works/pi/issues/5438)

9. **#5469 — Feature request: Collapse MCP tool results by default**  
   *3 comments*  
   Heavy MCP users are drowning in large expanded blocks for fetch/search results. A `settings.json` opt-out is requested.  
   [GitHub](https://github.com/earendil-works/pi/issues/5469)

10. **#5478 — cwd bridge captures shell directory changes but never propagates them**  
    *2 comments*  
    `cd` inside bash tool silently succeeds but the new directory is never propagated to tools, footer, or session state — making the capture entirely useless.  
    [GitHub](https://github.com/earendil-works/pi/issues/5478)

## Key PR Progress

1. **#5486 — fix: include day of week in Current date system prompt**  
   *Merged*  
   Adds day-of-week to the date string (e.g., "2026-06-08 (Monday)") to stop smaller models from hallucinating weekdays.  
   [GitHub](https://github.com/earendil-works/pi/pull/5486)

2. **#5479 — perf: reuse services on same-cwd session switch**  
   *Merged*  
   Skips recreating cwd-bound services when switching sessions in the same directory. Reduces overhead for session-heavy workflows.  
   [GitHub](https://github.com/earendil-works/pi/pull/5479)

3. **#5481 — feat: require bash descriptions and default timeout**  
   *Merged*  
   Adds a required `description` field to the bash tool schema and a default timeout to prevent zombie processes. Improves auditability and safety.  
   [GitHub](https://github.com/earendil-works/pi/pull/5481)

4. **#5480 — fix: estimate context usage after compaction**  
   *Merged*  
   After compaction, now estimates context usage by summing non-compacted tokens, rather than showing `?/200k` in the footer.  
   [GitHub](https://github.com/earendil-works/pi/pull/5480)

5. **#5472 — feat: add Requesty as native provider**  
   *Merged*  
   Adds Requesty.ai as a first-class provider, so `requesty/...` models work OOTB without needing generic OpenAI-compatible configuration.  
   [GitHub](https://github.com/earendil-works/pi/pull/5472)

6. **#5471 — fix: don't unconditionally continue after compaction**  
   *Merged*  
   Fixes #5463: after auto-compaction, only calls `agent.continue()` if there are actually queued messages — prevents errors in plan mode and other workflows.  
   [GitHub](https://github.com/earendil-works/pi/pull/5471)

7. **#5467 — Include models.json path in migration parse errors**  
   *Merged*  
   Reports malformed `models.json` migration errors with the absolute file path, making debugging much easier.  
   [GitHub](https://github.com/earendil-works/pi/pull/5467)

8. **#5465 — feat: add mineru document-parsing skill**  
   *Merged*  
   Adds a new `mineru` skill under `.pi/skills/mineru/` for document parsing (URL and local-file upload with polling).  
   [GitHub](https://github.com/earendil-works/pi/pull/5465)

9. **#5455 — Export RpcExtensionUIRequest / RpcExtensionUIResponse from public API**  
   *Merged*  
   Makes the RPC protocol's extension-UI types reachable from `@earendil-works/pi-coding-agent`. Completes the public surface for extension authors.  
   [GitHub](https://github.com/earendil-works/pi/issues/5455)

10. **#5444 — Extract composable `runAgentSession` from `main.ts` monolith**  
    *Merged*  
    Extracts a testable `runAgentSession` function from the 860-line `main.ts`, improving testability and separation of concerns.  
    [GitHub](https://github.com/earendil-works/pi/issues/5444)

## Feature Request Trends
- **Configurable UI behavior**: Multiple requests for collapsing MCP tool results (#5469), configurable image storage paths (#5414), and auto-horizontal-scroll for session tree (#4956) show a desire for more customizable TUI.
- **Extensibility API improvements**: Requests to export more types (#5455, #5443), allow excluding built-in tools (#5447), and extract composable functions (#5444) signal a maturing ecosystem of extension developers.
- **Provider and model support**: Adding Requesty (#5472) and fixing developer role detection (#5456) indicate ongoing demand for broader model compatibility.
- **Safety and auditability**: The bash description + timeout PR (#5481) and context usage estimation (#5480) reflect growing interest in operational guardrails.

## Developer Pain Points
- **Provider integration fragility**: Anthropic thinking block modification (#5223), DeepSeek API key persistence (#5431), and OpenRouter model version gaps (#3931) continue to plague multi-provider setups.
- **Performance regressions**: The 2.4s cold start from eager SDK loading (#5402) and 3-5 minute local model latency (#5464) are significant blockers for daily use.
- **TUI interaction inconsistencies**: `shift+enter` submission vs. newline (#5188), navigation in multiline prompts (#5454), and raw markdown fence rendering (#5462) degrade the terminal UX.
- **cwd tracking broken**: The cwd bridge captures but never propagates directory changes (#5478), and the long-standing request to allow session CWD changes (#2992) remains unresolved.
- **Package manager friction**: Bun users still face issues with extension installation (#4160), and tmux version requirements lag behind actual needs (#5432).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-08

## Today's Highlights

The Qwen Code ecosystem continues to mature rapidly, with **ACP (Agent Client Protocol) transport parity** reaching a major milestone — the daemon now supports both SSE and WebSocket transports, enabling native connections from Zed, Goose, and JetBrains without adapter code. The team also shipped session lifecycle improvements including an **idle reaper for automatic cleanup** and a **background-agent `/fork` command**, while fixing a long-standing submodule file completion bug. Community activity remains high with 42 PRs and 7 issues updated in the last 24 hours.

## Releases

- **v0.17.1-nightly.20260608.aea34fa2c** — Nightly release. Contains chore release automation and a fix from @he-yufeng that skips "thought" parts in CLI copy output (likely related to model reasoning traces).

## Hot Issues

1. **[#4514 — Daemon capability gaps & prioritized backlog](https://github.com/QwenLM/qwen-code/issues/4514)** (OPEN/12 comments)  
   A comprehensive tracking issue for remaining gaps in the `qwen serve` HTTP/SSE surface after slash-command passthrough. The community has been actively discussing extensions, diagnostics, and workspace settings. This is the blueprint for v0.16-alpha polish.

2. **[#4782 — ACP Streamable HTTP transport implementation status](https://github.com/QwenLM/qwen-code/issues/4782)** (OPEN/2 comments)  
   Tracks the ongoing ACP transport implementation. The thread confirms that ACP-native editors (Zed, Goose, JetBrains) now work without adapters. Phase 2 (WebSocket) is in flight via PR #4773.

3. **[#4830 — Fallback model support for resilient sessions](https://github.com/QwenLM/qwen-code/issues/4830)** (CLOSED as duplicate)  
   Proposes automatic fallback to alternative models when the primary provider is rate-limited or unavailable. Closed as duplicate, suggesting this is already tracked elsewhere — a strong sign the team is prioritizing session resilience.

4. **[#4550 — LAN initialization stuck without internet](https://github.com/QwenLM/qwen-code/issues/4550)** (OPEN/2 comments)  
   A critical bug for enterprise users: Qwen Code hangs during initialization when running in isolated/air-gapped networks. The user requests a configuration option to skip the initialization step. No resolution yet.

5. **[#1206 — Dynamic multi-model support for OpenAI-compatible APIs](https://github.com/QwenLM/qwen-code/issues/1206)** (OPEN/2 comments, 1 👍)  
   Long-standing feature request (Dec 2025) to dynamically fetch and switch models from OpenAI-compatible endpoints via `/auth`. Still open with only 2 comments — perhaps awaiting the broader daemon-mode model-switching infrastructure.

6. **[#4568 — `@` file completion shows submodule folder but no files](https://github.com/QwenLM/qwen-code/issues/4568)** (CLOSED)  
   Bug where `@` autocomplete only shows submodule directories, not their contents. Marked as scope/git, scope/ide. Fixed in PR #4596 by adding `--recurse-submodules` to git file listing.

7. **[#4744 — Support `/copy N` to copy Nth-last message](https://github.com/QwenLM/qwen-code/issues/4744)** (CLOSED)  
   Feature request to extend `/copy` with a numeric argument (matching Claude Code behavior). Implemented in PR #4761 and closed. Quick turnaround on a UX polish item.

8. **[#4514 subtopic: Extensions diagnostic surface](https://github.com/QwenLM/qwen-code/issues/4514)** — Referenced in PR #4832 which adds `GET /workspace/extensions`. The community is keen on visibility into installed extensions, their capabilities, and health status.

9. **[#4514 subtopic: Settings management](https://github.com/QwenLM/qwen-code/issues/4514)** — Referenced in PR #4816 (`/settings` slash command). Demonstrates community demand for runtime configuration without restarting the daemon.

10. **Submodule handling consistency** — Multiple issues touch on submodule support (e.g., #4568 fixed, but #4830 mentions fallback model resilience). The community expects robust mono-repo and multi-repo support.

## Key PR Progress

1. **[#4833 — Session idle reaper](https://github.com/QwenLM/qwen-code/pull/4833)** (OPEN/New)  
   Adds automatic cleanup of idle sessions (configurable TTL, default 30 min). Essential for preventing resource leaks in long-running daemon deployments. Uses existing `closeSession` infrastructure. **This is a production-hardening PR.**

2. **[#4773 — ACP WebSocket transport](https://github.com/QwenLM/qwen-code/pull/4773)** (OPEN)  
   Completes ACP WebSocket transport per RFD, co-existing with SSE. Introduces transport-agnostic interfaces (`transportStream.ts`) and a connection registry. Depends on #4827. **This is the key enabler for real-time bidirectional ACP communication.**

3. **[#4827 — ACP/REST parity: 29 new `_qwen/*` methods](https://github.com/QwenLM/qwen-code/pull/4827)** (OPEN/+935 lines)  
   Massive PR achieving full ACP REST parity. Adds session extensions (recap, btw, shell, detach, context_usage) and hardening. Replaces auto-closed #4736. **This is the largest single ACP deliverable in recent history.**

4. **[#4613 — Keep model & approval-mode consistent across clients](https://github.com/QwenLM/qwen-code/pull/4613)** (OPEN)  
   Fixes stale state when multiple clients share a daemon session. Addresses duplicate/dropped broadcasts. Critical for IDE + terminal + web-shell coexistence.

5. **[#4780 — `/fork` background-agent command](https://github.com/QwenLM/qwen-code/pull/4780)** (OPEN)  
   Adds ability to spawn a background agent that inherits full conversation context, works asynchronously, and reports back through existing notification channels. **This enables sophisticated multi-agent workflows.**

6. **[#4596 — Recurse into submodule files](https://github.com/QwenLM/qwen-code/pull/4596)** (CLOSED)  
   Fixes submodule file crawling by adding `--recurse-submodules` to `git ls-files`. Direct fix for #4568. Merged quickly.

7. **[#4816 — `/settings` slash command for web-shell](https://github.com/QwenLM/qwen-code/pull/4816)** (CLOSED)  
   Full-stack implementation: daemon routes, SDK methods, React hooks, keyboard-navigable UI. Enables runtime settings changes without daemon restart.

8. **[#4832 — Extensions diagnostic HTTP/ACP surface](https://github.com/QwenLM/qwen-code/pull/4832)** (CLOSED)  
   Adds `GET /workspace/extensions` with capability summaries (MCP servers, skills, agents, hooks, commands). Addresses issue #4514 T3.9. **This is essential for cluster monitoring and troubleshooting.**

9. **[#4490 — Daemon-mode feature batch merge into main](https://github.com/QwenLM/qwen-code/pull/4490)** (OPEN)  
   Periodic integration merge of `daemon_mode_b_main` → `main`. Rolls up 46 commits across 386 files (+115k/−12k LOC). The batch includes core daemon-mode features for v0.16-alpha.

10. **[#4824 — Prevent OOM by compacting history under memory pressure](https://github.com/QwenLM/qwen-code/pull/4824)** (OPEN)  
    Three targeted fixes: microcompact on Hook messages, enforce API history limit, trigger UI history compactions under memory pressure. **Addresses long-running session stability for production workloads.**

## Feature Request Trends

1. **ACP/AI Protocol Evolution** — Dominant theme. Full transport parity (SSE + WebSocket), 29 new methods, and native editor support. The community is converging on ACP as the standard protocol.

2. **Session Lifecycle Management** — Idle reapers, fallback models, automatic cleanup, background agents. Users want long-running sessions that are resilient and resource-efficient.

3. **Multi-Client Consistency** — Model switching, approval modes, and settings must stay in sync across IDE, terminal, and web-shell clients sharing a daemon session.

4. **Enterprise/Offline Readiness** — Air-gapped initialization, submodule support, rate-limit handling. The user base increasingly includes enterprise teams with strict network policies.

5. **UX Polish** — `/copy N`, `/settings`, file completion improvements. Community expects Claude Code parity in slash commands and autocomplete behavior.

## Developer Pain Points

1. **No network initialization blocking** — Issue #4550 highlights that Qwen Code currently requires internet access for initialization. Enterprise users in air-gapped environments are blocked entirely. This is a high-priority fix for enterprise adoption.

2. **Submodule handling inconsistencies** — While #4568 is fixed, the conversation around submodule support suggests deeper issues with mono-repo projects and git submodule tool integration.

3. **OOM in long-running sessions** — PR #4824 directly addresses memory pressure in extended sessions. This suggests production users are hitting old-space exhaustion during goal-mode loops or deep agent workflows.

4. **Background auto-update breaking model switching** — PR #4760 fixes a subtle bug where `npm install -g` in the background invalidates lazy-loaded content generators, causing auth-type switching to fail. Indicates that the update mechanism lacks transactional safety.

5. **Stale temporal context** — PR #4798 injects current date/time on every user query to prevent stale temporal awareness. This is a fundamental issue for long-running agent loops that can span days.

6. **Static mode screen flash** — PR #4795 fixes a full-screen flash in compact mode during tool-call completion. While not critical, it degrades the user experience during heavy tool-use workflows.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-08

## 1. Today's Highlights
The project, now rebranded to **CodeWhale**, saw a surge in PR activity with **21 pull requests** updated in the last 24 hours, many from new contributors fixing concurrency, security, and error-handling bugs. On the issue side, community frustration continues to mount around **excessive token consumption** and **session instability**, with three high-comment-count issues (#1177, #743, #1969) still unresolved concerning cache hit rates, token usage, and rebranding migration. The project remains in an active, community-driven stabilization phase as the maintainer works toward the v0.9.0 milestone.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Hot Issues (10 noteworthy items)

**#1177 — [OPEN] Input cache hit rate too low**  
[Link](Hmbown/CodeWhale Issue #1177)  
Why it matters: A direct performance comparison with the sibling project DeepSeek-Reasonix reveals a **>95% vs. sub-par** cache hit rate gap. The 24 comments show strong developer consensus that this is a blocking efficiency issue.

**#743 — [OPEN] Token consumption has greatly increased**  
[Link](Hmbown/CodeWhale Issue #743)  
Why it matters: A user reports consuming **400 million tokens in half a day**, with 13 comments confirming similar experiences. This points to a systemic inefficiency in how context is managed per-turn.

**#1969 — [OPEN] Will existing sessions and skills survive rebranding to CodeWhale?**  
[Link](Hmbown/CodeWhale Issue #1969)  
Why it matters: With 8 comments and no clear migration path documented, this is a high-impact **blocker for long-term users** concerned about data loss after the rename.

**#1579 — [OPEN] The color scheme is really ugly**  
[Link](Hmbown/CodeWhale Issue #1579)  
Why it matters: 8 comments of mostly negative sentiment about visual design. While aesthetic, such feedback can affect **adoption rates** among new users.

**#1620 — [OPEN] Thought process extremely slow**  
[Link](Hmbown/CodeWhale Issue #1620)  
Why it matters: A user reports "one word per half-day" rendering, with 5 comments suggesting this may be a **rendering or streaming bottleneck**, not a model issue.

**#2492 — [OPEN] No cross-session memory**  
[Link](Hmbown/CodeWhale Issue #2492)  
Why it matters: 5 comments highlight that the tool **forgets earlier session context on restart**, and even when memory is forced, it is not read automatically on startup. This is a core UX gap for professional users.

**#2328 — [OPEN] exec_shell mode availability inconsistent**  
[Link](Hmbown/CodeWhale Issue #2328)  
Why it matters: The `exec_shell` tool works in YOLO mode but fails in Agent mode, contradicting documentation. 4 comments reflect confusion and **workflow disruption**.

**#1556 — [OPEN] Ghostty terminal flashing on macOS**  
[Link](Hmbown/CodeWhale Issue #1556)  
Why it matters: 3 comments report persistent screen flickering in the Ghostty terminal, indicating a **rendering engine incompatibility**.

**#2620 — [OPEN] Task execution freeze with text overflow**  
[Link](Hmbown/CodeWhale Issue #2620)  
Why it matters: 3 comments describe a **hard freeze** during refactoring tasks, with text spilling outside the TUI panel. This is a critical reliability bug.

**#1357 — [OPEN] Input box overlap with runtime prompt**  
[Link](Hmbown/CodeWhale Issue #1357)  
Why it matters: 3 comments show runtime placeholder text **covering user input**, making part of the dialog invisible — a basic UI layout bug.

## 4. Key PR Progress (10 noteworthy items)

**#2891 — feat(i18n): localize approval dialog surface across 7 locales**  
[Link](Hmbown/CodeWhale PR #2891)  
Adds 23 new `MessageId` variants covering 7 locales for the `ApprovalWidget` takeover card. A significant **internationalization milestone**.

**#2888 — refactor(commands): extract registry and parser helpers**  
[Link](Hmbown/CodeWhale PR #2888)  
Layer 3 of the staged command-boundary refactor (#2791). Moves shared command helper ownership out of `commands/mod.rs` without altering dispatch behavior.

**#2873 — feat(config): add hotbar slot persistence (CLOSED)**  
[Link](Hmbown/CodeWhale PR #2873)  
Adds `[[hotbar]]` schema for slots 1-8, allowing user-configured hotbar actions to persist. Closed quickly — a solid, focused config contribution.

**#2874 — feat(cache): slim runtime_prompt to minimal tag, move policy descriptions to system prompt (CLOSED)**  
[Link](Hmbown/CodeWhale PR #2874)  
Builds on #2801 to fix prefix-cache invalidation by moving per-turn policy descriptions back to system prompt, reducing token overhead.

**#2885 — feat(execpolicy): wire ask-only permissions into runtime**  
[Link](Hmbown/CodeWhale PR #2885)  
Hooks `ask-only` permission records from `permissions.toml` into runtime execution policy — an important **security and compliance enhancement**.

**#2883 — fix: concurrency bugs (5 bugs)**  
[Link](Hmbown/CodeWhale PR #2883)  
Fixes mutex poisoning, thread spawning exhaustion, and Windows compilation failures. A **stability-critical** PR.

**#2882 — fix: security bugs in execution policy, approval mapping, and tool input validation**  
[Link](Hmbown/CodeWhale PR #2882)  
Addresses 5 security vulnerabilities including **execution policy bypass via whitespace normalization** and HTTP API approval mapping gaps.

**#2881 — fix: error handling (11 bugs)**  
[Link](Hmbown/CodeWhale PR #2881)  
Closes 11 instances of silent error discards (`.ok()`, `Err(_)`, `let _ =`) that were masking failures and potential data loss.

**#2865 — Modernize toward latest Claude Code**  
[Link](Hmbown/CodeWhale PR #2865)  
A broad modernization across prompts, hooks, skills, agents, and UI — based on a grounded gap analysis against the latest Claude Code.

**#2869 — fix(tui): list saved models from all providers in /model picker**  
[Link](Hmbown/CodeWhale PR #2869)  
Fixes a usability bug where custom models saved under non-active providers were invisible in the `/model` picker.

## 5. Feature Request Trends
Distilled from the issue set:
- **Cross-session memory/context persistence** (#2492, #2739, #1830, #1425) – The #1 requested feature: the ability to resume conversations without losing progress, and to have persistent memory across sessions.
- **Mode-aware agent behavior** (#2346, #2328) – Users want the AI agent to automatically adjust its tool selection and escalation behavior when the user switches between Plan, Agent, or YOLO modes.
- **Internationalization / locale support** (#2891, #1922) – Growing demand for multi-language support, especially for approval dialogs and error messages.
- **Hotbar / shortcut customization** (#2873, #2064) – Configurable key bindings for frequently-used commands to reduce manual typing.
- **Input cache efficiency** (#1177) – A strong desire to match or exceed the cache hit rates of competing tools like DeepSeek-Reasonix.

## 6. Developer Pain Points
- **Token waste** (Issues #743, #1177, #1818, #2346) – The single most-voiced pain point. Users report token consumption in the hundreds of millions, driven by redundant context, overly verbose per-turn messages, and agents that do not respect mode changes.
- **Session reliability / freezing** (Issues #2620, #2739, #1830, #1425) – Recurring reports of complete TUI freezes, text overflow, and loss of in-progress work on restart or timeout. This erodes trust in the tool for long-running tasks.
- **UI rendering glitches** (Issues #1556, #1357, #2261, #2374, #2244) – A cluster of reports about screen flickering, input overlap, terminal leakage on crash, and content overflow — all suggesting the TUI rendering layer needs deeper stabilization.
- **Rebranding migration uncertainty** (Issue #1969) – Existing users are anxious about whether their sessions, skills, and custom configurations will survive the rename to CodeWhale. Clear migration documentation is an urgent need.
- **Documentation gaps** (Issues #2328, #2244, #2879) – Several issues highlight mismatches between documented behavior and actual runtime behavior, especially around mode restrictions and expected scroll behavior.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*