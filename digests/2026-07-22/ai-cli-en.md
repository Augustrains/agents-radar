# AI CLI Tools Community Digest 2026-07-22

> Generated: 2026-07-22 01:18 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date: 2026-07-22**

---

## 1. Ecosystem Overview

The AI CLI tools landscape on July 22, 2026 shows a market approaching maturity, with seven major tools each stabilizing around specific developer workflows. The ecosystem is dominated by **reliability concerns**—every tool reported at least one critical regression or bug affecting core functionality, from tool-calling failures (Kimi Code, Qwen Code) to authentication regressions (OpenCode, Pi) and UI freezes (Codex, Gemini CLI). **MCP (Model Context Protocol) support** has become a cross-cutting battleground, with multiple tools racing to support remote OAuth, resource primitives, and dynamic tool discovery. **Sub-agent orchestration** remains the most fragile capability across the board, with agent hangs, false success reports, and session-mutation bugs appearing in every codebase. The community signal is clear: developers value **deterministic behavior and session persistence** over new flashy features.

---

## 2. Activity Comparison

| Tool | Issues (24h) | PRs (24h) | Latest Release | Release Velocity |
|------|-------------|-----------|----------------|------------------|
| **Claude Code** | 10 hot issues | 10 PRs | v2.1.217 (recent) | High — continuous rolling releases |
| **OpenAI Codex** | 10 hot issues | 10 PRs | v0.145.0 | High — weekly major releases + alphas |
| **Gemini CLI** | 10 hot issues | 10 PRs | v0.52.0-nightly | Medium — nightly + ad-hoc patches |
| **GitHub Copilot CLI** | 10 hot issues | 1 PR | v1.0.74-0 | Medium — point releases |
| **Kimi Code CLI** | 4 hot issues | 1 PR | v0.28.1 | Low — slower cadence |
| **OpenCode** | 10 hot issues | 10 PRs | (none today) | Medium — irregular but active |
| **Pi** | 10 hot issues | 10 PRs | v0.81.1 (same day) | Very High — two releases in 24h |
| **Qwen Code** | 10 hot issues | 10 PRs | v0.20.1 | High — previews + stable releases |
| **DeepSeek TUI (CodeWhale)** | 10 hot issues | 10 PRs | (v0.9.1 frozen) | Very High — integration sprint |

**Key observations:**
- **Pi** and **DeepSeek TUI** show the highest release velocity, with Pi shipping two versions in 24 hours.
- **Kimi Code CLI** is the quietest, with only 4 active issues and 1 PR.
- **GitHub Copilot CLI** has the lowest PR-to-Issue ratio (1:10), suggesting a maintenance-focused cycle or CI bottlenecks.
- **All tools** except Kimi Code CLI sustained 10+ tracked issues, indicating the ecosystem is broadly active.

---

## 3. Shared Feature Directions

The following requirements appear across **multiple tool communities**, indicating strong market demand:

| Feature / Need | Affected Tools | Description |
|----------------|----------------|-------------|
| **Local/Offline Model Support** | Gemini CLI (#5938, 37👍), Pi (#3357, 43👍), DeepSeek TUI (#4655) | Enterprise users demand on-premises LLM execution. Pi shipped v0.81.0 with llama.cpp integration; Gemini CLI has 11+ months of pent-up demand. |
| **Full MCP Protocol Support** | Copilot CLI (#1518/#1803, 22👍), Claude Code (#79986), Codex (implicit) | Tools need `resources/read`, `prompts`, and resource subscriptions—not just tools. Remote OAuth with DCR/CIMD is the next frontier. |
| **Sub-Agent Reliability** | Claude Code (implicit), Codex (#28058, 99👍), Gemini CLI (#22323, #21409), OpenCode (#33028), Qwen Code (#7156) | Agent hangs, false success reports, session-mutation bugs, and audit-trail loss are the #1 reliability category across the ecosystem. |
| **Project Management / Task Tracking** | Claude Code (#79948, #79982), DeepSeek TUI (#2889, #4636) | Users want agents to self-manage tasks, track completion, and provide verification—raw agent sprawl needs structure. |
| **Session & Transcript Persistence** | Claude Code (#62476, 13👍), Codex (paginated threads), Pi (#6917/#6914), OpenCode (#38163) | Configurable retention, cross-machine continuity, and searchable history are universal demands. |
| **Cost & Usage Transparency** | Copilot CLI (#4207), OpenCode (#4925), Pi (#6877/#6881), DeepSeek TUI (implicit) | Per-agent credit breakdowns, session cost display, and deterministic rate-limit resets. |
| **Custom Editor Integration** | Codex (#10428, 33👍), Pi (external editor #6774) | Users want to configure their own editors (Alacritty, Zed, etc.) with custom icons. |
| **Windows Stability** | Codex (#20214, #34327, #34260), Claude Code (#61021, #79986), OpenCode (#37481), Qwen Code (#7056, #7139) | Windows continues to be the weakest platform for all tools—UI freezes, process leaks, broken sandbox paths, and numpad input gaps. |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|------------|-------------|------------|-------------|-----------|----------|-----|-----------|--------------|
| **Primary Model** | Anthropic Claude | OpenAI GPT-4o | Gemini 2.5 | Copilot (GPT-4) | Moonshot k2.5 | Multi-provider | Multi-model | Qwen 3.8 | Multi-provider |
| **Target User** | Power devs, CI/CD | General devs | Enterprise GCP | GitHub ecosystem | Chinese devs | Open-source devs | TUI enthusiasts | Alibaba ecosystem | Self-hosters |
| **Key Strength** | Extensibility (hooks, plugins) | Sub-agent orchestration | Security architecture | GitHub integration | Simplicity | Web & desktop | TUI speed | Model diversity | Performance focus |
| **Weakest Point** | Fable 5 entitlement bugs | Windows stability | Agent infinite loops | MCP gaps | Tool-calling fragility | Memory leaks | Dependency duplication | Model-switching bugs | Platform maturity |
| **Release Philosophy** | Continuous rolling | Weekly major + alphas | Nightly + security patches | Point releases | Slow, stable | Irregular | Very fast iterating | Preview + stable | Sprint-driven |
| **Platform Support** | macOS/Linux/Windows | macOS (best), Windows (weak) | Linux/macOS (VS Code) | Linux/macOS/Windows | Linux/macOS | Web + desktop | Linux (best) | Cross-platform | Cross-platform |
| **Unique Feature** | Plugin/hook system | Multi-agent encryption | A2A server protocol | GitHub Actions native | Shell mode simplicity | Generators in codemode | Local llama.cpp | Autofix CI | Sub-agent worktree |

**Strategic positioning:**
- **Claude Code** leads on **extensibility architecture** but is bleeding trust with Fable 5 entitlement confusion.
- **OpenAI Codex** has the strongest **sub-agent orchestration** but the worst **Windows stability**—its Windows users are effectively beta testers.
- **Gemini CLI** differentiates on **enterprise security** (variable expansion blocking, workspace trust enforcement) but suffers from **agent reliability** issues.
- **GitHub Copilot CLI** owns **GitHub-native workflows** but is weakest on **MCP protocol completeness** despite high community demand.
- **Pi** and **DeepSeek TUI** are racing on **performance and local-first** approaches, with Pi's dual release in 24h signaling aggressive iteration.
- **OpenCode** and **Qwen Code** serve **ecosystem-specific users** (open-source multi-provider and Alibaba, respectively) with unique features like codemode generators and autofix CI.

---

## 5. Community Momentum & Maturity

| Tier | Tool | Maturity Indicators |
|------|------|-------------------|
| **Tier 1: High Momentum** | **Pi** | 2 releases in 24h, 10 hot issues + 10 PRs, strong local-model push. Community highly engaged with detailed feedback. Fastest iteration pace. |
| | **DeepSeek TUI (CodeWhale)** | 24 closed issues + 5 merged PRs in 24h, v0.9.1 integration sprint. High engagement on agent reliability and TUI UX. |
| | **Claude Code** | Largest community by absolute numbers (41 comments on single issue), but maturity is uneven—Fable 5 entitlement bugs indicate scaling pains. |
| | **OpenAI Codex** | 99👍 on audit-trail regression (#28058) signals the most community-validated pain point in the ecosystem. High engagement despite Windows issues. |
| **Tier 2: Stable Growth** | **Qwen Code** | Steady preview+stable cadence, closing P1 bugs rapidly (#7156). Community focused on Chinese ecosystem integration (Feishu, DingTalk). |
| | **GitHub Copilot CLI** | Lower PR velocity (1 PR/24h) suggests maintenance mode, but issues show active feature requests (MCP resources, 26👍 for OAuth). |
| | **OpenCode** | Diverse community (119 comments on memory megathread). Memory issues and layout migration friction indicate growing pains with scale. |
| **Tier 3: Niche / Quiet** | **Gemini CLI** | Strong security work (GHSA patches) but lower community engagement (max 37👍 on top issue). Enterprise focus may limit public momentum. |
| | **Kimi Code CLI** | Lowest activity (4 issues, 1 PR). Tool-calling regression (#2527) could be a trust-breaking event if unresolved. |

**Community maturity pattern:** The ecosystem is splitting into **fast-iterating challengers** (Pi, DeepSeek TUI) and **established platforms facing scaling pains** (Claude Code, Codex). The fast-iterators have fewer users but higher per-capita engagement. The platforms have large user bases but are drowning in regressions.

---

## 6. Trend Signals

1. **MCP is the new API standard.** Every tool is racing to support remote OAuth, resources, prompts, and tool subscriptions. Tools that lag (Copilot CLI) face growing community pressure. Expect **MCP certification** or standardized compliance testing within 6 months.

2. **Local-first LLM orchestration is inevitable.** Pi shipped it; Gemini CLI users demand it (37👍, 11 months). Regulatory pressure and enterprise data policies will force every tool to support Ollama/litellm/llama.cpp within 2026-2027.

3. **Sub-agent reliability is the critical bottleneck.** Every tool has agent hangs, false success reports, or audit-trail loss. The community is screaming for **deterministic agent behavior** over new features. The tool that solves this first will win trust.

4. **Windows is the platform debt.** Every tool's weakest platform. Users report UI freezes, process storms, sandbox path failures, and broken input. This is a **systemic architectural issue**—terminal-based CLIs will struggle on Windows until proper ConPTY/CLI infrastructure matures.

5. **Session persistence is a universal unmet need.** Users want configurable retention, cross-machine continuity, searchable history, and session naming. This is basic UX hygiene that no tool has fully solved.

6. **Cost transparency is becoming table stakes.** As developers scale usage, they demand per-agent credit breakdowns, session cost displays, and predictable rate-limit resets. Tools that hide costs will lose power users.

7. **The extensibility promise vs. reality gap.** Claude Code's hook system has 6+ community PRs fixing path quoting, encoding, and import resolution. Gemini CLI's custom skills are rarely invoked. The ecosystem sells extensibility but the implementation is brittle.

8. **Enterprise security hardening is accelerating.** Gemini CLI is leading on security PRs (variable expansion blocking, workspace trust enforcement, session ID rotation). This trend will accelerate as tools move from dev playgrounds to production CI/CD pipelines.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot:** github.com/anthropics/skills | **Date:** 2026-07-22

---

## 1. Top Skills Ranking

The most-discussed Pull Requests by community engagement reveal several critical skill-development themes:

**#1298 — `fix(skill-creator): run_eval.py always reports 0% recall`** ([PR #1298](https://github.com/anthropics/skills/pull/1298))
*Function:* Fixes the core skill evaluation pipeline — `run_eval.py` was returning `recall=0%` for every tested description, rendering the entire description-optimization loop (`run_loop.py`, `improve_description.py`) non-functional.
*Discussion highlights:* Reproduces 10+ independent confirmations of the bug. Fix spans four interdependent issues: eval artifact installation, Windows stream reading, trigger detection logic, and parallel worker behavior.
*Status:* **Open** — one of the most critical infrastructure fixes under active review.

**#514 — `Add document-typography skill`** ([PR #514](https://github.com/anthropics/skills/pull/514))
*Function:* Typographic quality control for AI-generated documents — prevents orphan word wrap, widow paragraphs, and numbering misalignment.
*Discussion highlights:* Community agrees these issues affect nearly every long-form Claude output. Minimal debate on approach; high signal-to-noise.
*Status:* **Open**

**#1367 — `feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate`** ([PR #1367](https://github.com/anthropics/skills/pull/1367))
*Function:* A universal output audit skill: verifies claimed files exist mechanically, then runs a four-dimension reasoning audit (damage-severity order) across any project and model.
*Discussion highlights:* Proposes a proactive alternative to reactive debugging. Interest in cross-model applicability.
*Status:* **Open**

**#538 — `fix(pdf): correct case-sensitive file references in SKILL.md`** ([PR #538](https://github.com/anthropics/skills/pull/538))
*Function:* Fixes 8 case-sensitivity mismatches between SKILL.md references and actual filenames (`REFERENCE.md` → `reference.md`), which broke on case-sensitive filesystems.
*Discussion highlights:* Illustrates a systemic documentation-quality issue in the repository.
*Status:* **Open**

**#541 — `fix(docx): prevent tracked change w:id collision with existing bookmarks`** ([PR #541](https://github.com/anthropics/skills/pull/541))
*Function:* Fixes DOCX corruption when tracked changes are added to documents with existing bookmarks — the shared `w:id` namespace caused collisions with hardcoded IDs.
*Discussion highlights:* Technical deep dive into OOXML internals. Demonstrates the complexity of maintaining document-format skills.
*Status:* **Open**

**#486 — `Add ODT skill — OpenDocument text creation and template filling`** ([PR #486](https://github.com/anthropics/skills/pull/486))
*Function:* Full OpenDocument format support (.odt, .ods) including creation, template filling, and ODT-to-HTML conversion.
*Discussion highlights:* Demand for LibreOffice/ISO-standard document support. Broader than any single format fix.
*Status:* **Open**

**#525 — `Add pyxel skill for retro game development`** ([PR #525](https://github.com/anthropics/skills/pull/525))
*Function:* Integrates with [pyxel-mcp](https://github.com/kitao/pyxel-mcp) for retro/pixel-art game development with Claude.
*Discussion highlights:* Author is the Pyxel engine creator — high trust signal. Interest in MCP-skill hybrid patterns.
*Status:* **Open** — last updated 2026-07-15.

**#210 — `Improve frontend-design skill clarity and actionability`** ([PR #210](https://github.com/anthropics/skills/pull/210))
*Function:* Revises the existing frontend-design skill for clearer, more actionable instructions that Claude can execute within a single conversation.
*Discussion highlights:* Focus on token efficiency and instruction specificity. Representative of the broader "skill quality" movement.
*Status:* **Open**

---

## 2. Community Demand Trends

From the top Issues by engagement:

| Demand Direction | Evidence | Signal Strength |
|---|---|---|
| **Trust & security boundaries** | Issue #492 (43 comments) — community skills under `anthropic/` namespace enable trust abuse. Users want official/official distinction. | **Highest** — 43 comments, 2 👍 |
| **Org-wide skill sharing** | Issue #228 (14 comments, 7 👍) — no native sharing mechanism; manual `.skill` file distribution via Slack/Teams. | **High** — highest 👍 count |
| **Skill-creator reliability** | Issue #556 (12 comments, 7 👍) — `run_eval.py` 0% trigger rate renders optimization loop useless. | **High** — directly blocks skill authoring |
| **Duplicate skill installations** | Issue #189 (6 comments, 9 👍) — overlapping plugins install identical skills. | **Moderate/High** — top 👍/comment ratio |
| **Windows compatibility** | Issue #1061 (3 comments, 2 👍) — subprocess, encoding, and pipe-select failures on Windows. | **Moderate** — affects platform equity |
| **Agent governance patterns** | Issue #412 (6 comments) — safety patterns for AI agent systems: policy enforcement, threat detection, audit trails. | **Growing** — no PR yet |
| **Reasoning quality pipeline** | Issue #1385 (3 comments) — pre-task calibration → adversarial review → delivery verification. | **Emerging** — proposer has active PR #1367 |

**Key takeaway:** The community's most vocal demand is _trust infrastructure_ — namespace security (Issue #492), validation tooling (Issue #556), and sharing mechanisms (Issue #228) — rather than new domain-specific skills.

---

## 3. High-Potential Pending Skills

Active PRs with sustained community traction that are likely to land soon:

| PR | Skill | Last Activity | Why It Matters |
|---|---|---|---|
| [#1302](https://github.com/anthropics/skills/pull/1302) | `color-expert` — comprehensive color naming, spaces, and harmonies | 2026-07-21 | Deep domain coverage (ISCC-NBS, Munsell, OKLCH, CAM16). Self-contained, well-researched. |
| [#1367](https://github.com/anthropics/skills/pull/1367) | `self-audit` — mechanical verification + reasoning quality gate | 2026-07-02 | Addresses the "trust but verify" gap no existing skill covers. Universal applicability. |
| [#723](https://github.com/anthropics/skills/pull/723) | `testing-patterns` — full-stack testing (unit, React, API, E2E) | 2026-04-21 | Covers Testing Trophy model, a widely-adopted but underspecified pattern in AI-assisted testing. |
| [#525](https://github.com/anthropics/skills/pull/525) | `pyxel` — retro game development via MCP | 2026-07-15 | Author is Pyxel creator; demonstrates skill+MCP hybrid pattern. |
| [#83](https://github.com/anthropics/skills/pull/83) | `skill-quality-analyzer` + `skill-security-analyzer` (meta-skills) | 2026-01-07 | Self-referential — evaluates skills themselves. High alignment with Issue #492 trust concerns. |

**Watch for:** PRs from `Lubrsy706` (#538, #539, #541) — a prolific bug-fixer addressing systemic quality issues in document-format skills and validation tooling.

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is **skill-development infrastructure** (reliable evaluation tooling, namespace security, sharing mechanisms, and cross-platform compatibility) — the "scaffolding" that makes creating and distributing high-quality skills viable — rather than any single domain-specific Skill.

---

# Claude Code Community Digest — 2026-07-22

## Today's Highlights
Fable 5 rollout continues to cause friction for Max plan users, with multiple reports of the model being gated behind usage credits despite proper entitlements. A major regression (#71542) where the GitHub connector links repositories but cannot access any content remains the most active open issue with 41 comments. On the PR front, six community-contributed fixes from `rahulrshetty45` targeting hookify and plugin documentation issues were submitted en masse, signaling a strong community push on developer experience polish.

## Releases
**v2.1.217** (latest):
- Added emoji shortcode autocomplete in the prompt input: `:heart:` inserts ❤️, `:hea` gives suggestions — disable via `emojiCompletionEnabled`
- Added warnings for transcript write failures (e.g. disk full) and when session saving is off due to inheritance

## Hot Issues (10 notable items)

### Critical / High Activity
1. **[#71542 — GitHub connector links but cannot access ANY content (regression)](https://github.com/anthropics/claude-code/issues/71542)**  
   *41 comments, 36 👍* — Account-wide regression affecting public and private repos. Community reaction is strong, with users confirming the issue after recent updates. Still open for 26 days; this is the highest-signal bug currently.

2. **[#79337 — Fable 5 requires "usage credits" on Max plan (day it became standard)](https://github.com/anthropics/claude-code/issues/79337)**  
   *26 comments, 9 👍* — On 2026-07-20, Claude Code silently downgrades Max sessions from Fable 5 to Opus 4.8, claiming usage credits required. Timestamped issue suggests a provisioning/billing mismatch during rollout.

3. **[#79360 — Fable 5 gated via claude setup-token (inference-only scope)](https://github.com/anthropics/claude-code/issues/79360)**  
   *5 comments, 30 👍* — Related to #79337 but distinct: users authenticated via `claude setup-token` with inference-only scopes cannot read entitlements. High reaction count indicates this affects many CI/CD/headless setups.

### Recurring / Architectural
4. **[#45810 — Marketplace update button disabled even when outdated](https://github.com/anthropics/claude-code/issues/45810)**  
   *15 comments, 6 👍* — Long-standing UI bug (since April) where the update button in the plugin marketplace is greyed out/non-interactive. Still open with no fix merged.

5. **[#61021 — Can't easily select text in VSCode terminal with Claude Code](https://github.com/anthropics/claude-code/issues/61021)**  
   *14 comments, 8 👍* — Recent change broke terminal text selection behavior in VSCode. Users must now use alternative copy methods. Windows and TUI platform.

6. **[#62476 — Claude Code silently deletes transcripts after 30 days](https://github.com/anthropics/claude-code/issues/62476)**  
   *11 comments, 13 👍* — Default retention policy deletes conversations without clear notification. Community wants opt-in/configured retention.

7. **[#79986 — Desktop 1.24012.1: tools/call never sent to MCP servers (Windows)](https://github.com/anthropics/claude-code/issues/79986)**  
   *0 comments, 1 👍* — Fresh regression in latest Desktop release. All Filesystem tools fail despite correct handshake. Reported today.

### Community Creations
8. **[#79818 — Auto-documenting with self-hosted Plane + knowledge system](https://github.com/anthropics/claude-code/issues/79818)**  
   *2 comments* — Show & tell: user teaches Claude Code to auto-record and retrieve its own work across machines. Demonstrates the continuity problem and a practical hack.

9. **[#79948 — "I double-dog-dare you: build the PM layer Claude Code is missing"](https://github.com/anthropics/claude-code/issues/79948)**  
   *1 comment* — Passionate feature request for project management: force agent completion, verify against reality, multi-tier workflow. Raw community frustration with agent sprawl.

10. **[#79968 — Message flagged as security risk during normal game dev](https://github.com/anthropics/claude-code/issues/79968)**  
    *1 comment* — False positive security flag. User reports normal development messages blocked. Possibly a language/context detection issue.

## Key PR Progress (10 important pull requests)

### Community Bugfixes (rahulrshetty45 batch)
1. **[#79644 — Quote ${CLAUDE_PLUGIN_ROOT} in plugin hook commands](https://github.com/anthropics/claude-code/pull/79644)**  
   Fixes #78490 — macOS plugin root contains spaces under `~/Library/Application Support/…`, causing shell word-splitting and silent hook failures.

2. **[#79645 — Read rule and transcript files as UTF-8](https://github.com/anthropics/claude-code/pull/79645)**  
   Fixes #77270 — On Windows, file reads defaulted to cp1252, breaking arrow/emoji/em-dash characters in rule files.

3. **[#79647 — Resolve imports independent of plugin directory name](https://github.com/anthropics/claude-code/pull/79647)**  
   Fixes #69665 — Hook entry scripts broke if the plugin directory wasn't literally named `hookify`. Package-relative imports now work regardless.

4. **[#79636 — Add hookify. prefix to example rule filenames](https://github.com/anthropics/claude-code/pull/79636)**  
   Fixes #79143 — Shipped examples lacked required `hookify.` prefix, causing loading failures for users following documentation.

5. **[#79640 — Use disable-model-invocation for Ralph commands](https://github.com/anthropics/claude-code/pull/79640)**  
   Fixes #79138 — Ralph-loop commands used unrecognized `hide-from-slash-command-tool` instead of documented `disable-model-invocation`.

6. **[#79642 — Fix marketplace name to claude-code-plugins](https://github.com/anthropics/claude-code/pull/79642)**  
   Fixes #70064 — `README.md` told users to install from `claude-code-marketplace`, but the actual name is `claude-code-plugins`.

7. **[#79635 — Point PR Review Toolkit Contributing to in-repo agents](https://github.com/anthropics/claude-code/pull/79635)**  
   Fixes #79137 — Documentation pointed to a private repo. Agents actually live in `plugins/pr-review-toolkit/agents/`.

8. **[#79643 — Align /commit-push-pr docs with actual behavior](https://github.com/anthropics/claude-code/pull/79643)**  
   Fixes #79144 — Docs implied branch history analysis; actual command only uses `git status`, `git diff HEAD`, and `git branch --show-current`.

### Platform / Infrastructure
9. **[#78532 — GCP gateway: optional internal ALB + PG16 Cloud SQL fix](https://github.com/anthropics/claude-code/pull/78532)**  
   PG16 instances now default to ENTERPRISE_PLUS edition, rejecting shared-core tiers. Adds internal ALB option for GCP Terraform example.

10. **[#79620 — Add text-to-speech read-aloud hook for accessibility](https://github.com/anthropics/claude-code/pull/79620)**  
    Multi-platform TTS hook: Piper (Linux), `say` (macOS), PowerShell (Windows). Includes markdown-aware extraction and code-skip heuristic.

## Feature Request Trends

1. **Project Management / Task Tracking** — Multiple requests (e.g. #79948, #79982) for built-in task creation, update, listing, and status tracking. Users want Claude Code to manage its own work and verify completion. Tools like `TaskCreate` are reported unavailable (#79982).

2. **Transcript & Session Persistence** — Users want configurable transcript retention (#62476), ability to resume sessions from the Claude app (#79975), and continuity across machines (#79818). The auto-deletion after 30 days frustrates power users.

3. **UI/UX Clipboard & Copy Improvements** — Copy chat as markdown source (#54670), fix whitespace stripping when copying (#79960), and text selection in terminal (#61021) are persistently requested.

4. **Accessibility & Automation** — Screen reader improvements (#69996), screenshot hotkey automation (#79987), and TTS read-aloud (#79620) show growing demand for non-visual and hands-free workflows.

5. **MCP Tool Reliability** — Multiple reports (#79986, #79983, #79992) of MCP tool calls silently failing, tools/call never dispatched, or approval loops. Community wants deterministic MCP behavior.

## Developer Pain Points

- **Fable 5 Entitlement Confusion** — Max plan users hit "usage credits required" despite proper subscriptions (#79337, #79360). Two distinct bugs: one for interactive, one for token-authenticated sessions. High community reaction (30+ 👍 on #79360).
- **GitHub Connector Regression** — #71542 has been open 26 days with 41 comments. Repos link fine but content is inaccessible. Affects account-wide, both public and private repos.
- **Plugin/Hook System Fragility** — Six PRs from a single community member (rahulrshetty45) in one day fixing bugs in the hookify system: path quoting, encoding, import resolution, documentation. The system works but edge cases around cross-platform support and plugin naming are brittle.
- **Context Compaction Threshold** — #79665 reports auto-compact warnings fire at ~177k tokens in 1M-context sessions — calibrated for 200k default window rather than the actual 1M. Wastes context prematurely.
- **Silent Data Loss** — #62476 (transcript deletion) and #79986 (Desktop MCP tools/call silent failure) share a common theme: failures that don't surface obvious errors, making debugging time-consuming for developers.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest — 2026-07-22

## Today's Highlights

OpenAI shipped **Codex 0.145.0** with experimental paginated thread history, multi-tool import from Cursor/Claude Code, and sub-agent memory support. Meanwhile, **Windows stability remains the top pain point**, with three separate issues surfacing unbounded process-cleanup storms, HID module-related UI freezes, and Crashpad dump leaks that can consume 5GB+ per day. A high-impact regression in encrypted MultiAgentV2 messages (99 👍) is stripping audit trails from task logs, drawing significant community concern.

---

## Releases

**rust-v0.145.0** — New Features:
- **Experimental paginated thread history** with efficient resume, search, persisted names, sub-agent support, and memories (#33364, #33907, #34085, #34229, #34386)
- Expanded `/import` to migrate settings from Cursor and Claude Code — including MCP servers, plugins, sessions, commands, and project configurations

Pre-release alphas (0.145.0-alpha.27 through alpha.30) were also cut but contain no public changelog details.

---

## Hot Issues (10 Noteworthy)

1. **[#20214 — Codex App frequently freezes/stutters on Windows 11 Pro](https://github.com/openai/codex/issues/20214)**  
   *63 comments, 70 👍*  
   The highest-traffic Windows bug on the board. Users report stuttering despite 32 GB RAM and AMD Ryzen 5 hardware. No fix has been confirmed since April; community frustration is mounting.

2. **[#28058 — Regression: encrypted MultiAgentV2 messages remove readable task audit trail](https://github.com/openai/codex/issues/28058)**  
   *26 comments, 99 👍*  
   Post-0.137.0 encryption of multi-agent payloads (`#26210`) has made task logs unreadable for debugging. This is the **most upvoted open issue**, signaling a major reliability regression for sub-agent workflows.

3. **[#34260 — Windows Desktop: unbounded taskkill.exe/conhost.exe cleanup storm exhausts WMI](https://github.com/openai/codex/issues/34260)**  
   *14 comments, 8 👍*  
   A newly filed bug (July 20) describing hundreds of concurrent `taskkill.exe` processes that exhaust WMI provider quotas and freeze the system. Critical for Windows power users.

4. **[#25921 — Codex Desktop generates Crashpad pending dumps without limit: +5GB/day](https://github.com/openai/codex/issues/25921)**  
   *15 comments, 5 👍*  
   Crashpad dumps pile up in `~/Library/Application Support/com.openai.codex/web/Crashpad/pending`, reaching 54,504 files and 4.9 GB in a single day. Affects macOS stability and disk hygiene.

5. **[#34327 — Severe UI freezes correlate with Codex Micro HID/serial module](https://github.com/openai/codex/issues/34327)**  
   *4 comments, 3 👍*  
   Disabling the HID/serial module resolves the hangs entirely. Suggests a polling or interrupt-handling defect in the Windows app's hardware interaction layer.

6. **[#9508 — Make Weekly Limit Reset Deterministic](https://github.com/openai/codex/issues/9508)**  
   *46 comments, 31 👍*  
   Users continue to demand predictable rate-limit resets. The current behavior is described as "arbitrary," disrupting planned usage cycles. Over 6 months old and still unresolved.

7. **[#32149 — Windows setup fails before UAC prompt; both setup options non-functional](https://github.com/openai/codex/issues/32149)**  
   *24 comments, 5 👍*  
   New users on Windows 11 cannot complete installation. The MSIX and installer path both fail before even reaching the UAC elevation prompt.

8. **[#26478 — Windows spellcheck detects misspellings but shows "No Guesses Found"](https://github.com/openai/codex/issues/26478)**  
   *11 comments, 23 👍*  
   Native Windows spellcheck works in Notepad but always returns empty suggestions inside Codex Desktop. A quality-of-life bug affecting writing workflows.

9. **[#18629 — Desktop threads poisoned by inline base64 tool images → "Bad Request" on resume](https://github.com/openai/codex/issues/18629)**  
   *11 comments, 1 👍*  
   Image-producing tool output is persisted inline in thread history, causing `{"detail":"Bad Request"}` errors when the thread grows large. Likely also inflates token usage.

10. **[#10989 — Xcode Codex sign-in fails in Safari when HTTPS-only blocks http://localhost callback](https://github.com/openai/codex/issues/10989)**  
    *8 comments, 6 👍*  
    Safari's HTTPS-only mode blocks the `http://localhost:1455/auth/callback` redirect. A platform-specific auth blocker for Xcode users on macOS Tahoe.

---

## Key PR Progress (10 Important Merges)

1. **[#34643 — Migrate login HTTP construction to `HttpClient`](https://github.com/openai/codex/pull/34643)**  
   Centralizes all `reqwest` usage into `codex-http-client`, covering API, model discovery, auth, remote control, and skill routes. A major architectural cleanup.

2. **[#34641 — Harden managed proxy setup for sandboxed executions](https://github.com/openai/codex/pull/34641)**  
   Makes the Linux proxy socket directory readable inside `bubblewrap` sandboxes and routes WS_PROXY/WSS_PROXY through the managed proxy bridge. Removes inherited proxy env vars for isolation.

3. **[#34630 — Add a policy-aware HTTP client builder](https://github.com/openai/codex/pull/34630)**  
   Introduces `HttpClientBuilder` for configuring headers, redirects, Cloudflare cookies, and diagnostics without exposing the underlying transport. Factory-backed construction respects rollout policies.

4. **[#34629 — Harden Windows elevated sandbox startup](https://github.com/openai/codex/pull/34629)**  
   Checks writable-root permissions via DACL snapshots and refreshes ACLs when SIDs are missing required access. Starts the command runner only after validation.

5. **[#34624 — Terminate Windows process trees with job objects](https://github.com/openai/codex/pull/34624)**  
   Assigns Windows pipe, ConPTY, and sandbox processes to job objects, enabling clean termination of entire process trees while allowing background children to survive root-process exit.

6. **[#34626 — Scale skill metadata budgets with model context windows](https://github.com/openai/codex/pull/34626)**  
   Replaces a fixed character limit with a dynamic budget of 2% of the model context window (capped at 4,000 tokens). Better supports varying model context sizes.

7. **[#34621 — Load paginated model context across rollout lineages](https://github.com/openai/codex/pull/34621)**  
   Supports the new paginated thread history feature by resolving full rollout lineages when loading model context, reverse-scanning each segment up to its byte boundary.

8. **[#34625 — Fix Windows TUI navigation key handling](https://github.com/openai/codex/pull/34625)**  
   Keeps the Windows console in cooked input mode to prevent Crossterm from receiving literal escape bytes instead of Win32 input records. Fixes arrow key navigation in the TUI.

9. **[#34613 — Route Windows sandbox proxy traffic by restricting SID](https://github.com/openai/codex/pull/34613)**  
   Keeps shared HTTP/SOCKS5 loopback listeners alive across sandbox restarts by using SID-based restriction for stable port assignment.

10. **[#34605 — Allow naming sessions with `/new` and `/clear`](https://github.com/openai/codex/pull/34605)**  
    Accepts an optional session name after `/new` or `/clear`, pushing it through the app server to name the new thread. Reports failures in chat while still creating the session.

---

## Feature Request Trends

- **Deterministic rate-limit resets** (#9508, #16423): Two issues with 77 combined 👍 demand predictable weekly cycles. Users plan work around limits and current behavior is described as "arbitrary."
- **Custom editor integration** (#10428, 33 👍): The "Open In" menu is limited to defaults; users want to add Alacritty, Zed, and other editors with custom icons and commands.
- **Background terminal sessions** (#3968, 33 👍): Similar to Claude Code's capability — long-running processes should persist after the CLI window is closed, with reattachment support.
- **Pinned prompt/composer input** (#26311, 8 👍): In long TUI sessions, the input box scrolls out of view. Users want a sticky bottom-pinned input bar.

---

## Developer Pain Points

- **Windows stability crisis**: Four high-severity bugs plague Windows 11 — UI freezes (HID module, #34327), unbounded process cleanup storms (#34260), Crashpad dump leaks (macOS cross-reference, #25921), and setup failures (#32149). Windows users are effectively beta testers.
- **Audit-trail regression in sub-agents**: Encryption of MultiAgentV2 messages (#28058) has broken task log readability, directly impacting debugging for multi-agent workflows. The 99 👍 reaction signals this is the community's #1 reliability concern.
- **Thread poisoning by inline media**: Base64 image payloads persisted in thread history (#18629) cause unrecoverable "Bad Request" errors on large threads. No solution has been proposed since April.
- **Cross-platform auth friction**: Xcode sign-in fails due to Safari HTTPS-only blocks (#10989, #34639). This blocks a growing macOS developer segment from using the Xcode Codex extension.
- **Remote-SSH extension fragility**: The VS Code extension fails to load over Remote-SSH (#26951, #27597) while the CLI works fine — a split that undermines trust in the extension's reliability for remote development.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-07-22

## Today's Highlights
The caretaker bot automation pipeline is maturing rapidly, with new triage worker workflows and PR-generator infrastructure landing this week. The most active community discussion remains the long-standing request for local/offline model support (37 reactions), while a critical security fix for shell variable expansion bypass (GHSA-wpqr-6v78-jr5g) is under review. Several agent reliability issues—including subagent hang, infinite token loops, and false GOAL-success reports—continue to dominate the bug tracker.

## Releases
- **v0.52.0-nightly.20260721.gacae7124b** (nightly): No release notes beyond changelog link. [Full diff →](https://github.com/google-gemini/gemini-cli/compare/v0.52.0-nightly.20260720.gacae7124b...v0.52.0-nightly.20260721.gacae7124b)

## Hot Issues

1. **[#5938 – Local/offline language model support (Ollama, LM Studio, etc.)](https://github.com/google-gemini/gemini-cli/issues/5938)**  
   *priority/p3, kind/enhancement* | 12 comments | 37 👍  
   Enterprise users with strict data privacy requirements have been asking for on-premises model support for 11+ months. The high reaction count signals strong demand.

2. **[#22323 – Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *priority/p1, kind/bug* | 12 comments  
   A deceptive bug: subagents that hit their turn limit report `status: "success"` with `Termination Reason: "GOAL"`, masking failures from users and downstream automation.

3. **[#21409 – Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   *priority/p1, kind/bug* | 8 comments | 8 👍  
   Users report that deferring to the generalist agent—even for simple tasks like folder creation—causes indefinite hangs. Workaround: explicit instruction to avoid subagents.

4. **[#28362 – Token drain loop with missing template.py](https://github.com/google-gemini/gemini-cli/issues/28362)**  
   *priority/p1, kind/bug* | 3 comments  
   A suspected infinite loop triggered by a shipped template.py file that was absent from distributions, burning tokens and requiring manual cancellation.

5. **[#25166 – Shell command gets stuck "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *priority/p1, kind/bug* | 4 comments | 3 👍  
   After simple CLI commands finish, the shell tool remains in a "Waiting input" state, blocking the agent from proceeding. Recurring frustration for power users.

6. **[#26522 – Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
   *priority/p2, kind/bug* | 5 comments  
   Background extraction agent only marks sessions as processed after a successful `read_file`. Low-signal sessions are skipped, resurfacing forever—a CPU/token waste.

7. **[#22745 – AST-aware file reads and codebase mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   *priority/p2, kind/feature* | 7 comments  
   Epic tracking whether AST-based tools (method-bound reads, search, mapping) reduce token waste and turn count. A performance-focused feature with low community engagement.

8. **[#21968 – Gemini does not use custom skills and sub-agents](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *priority/p2, kind/bug* | 6 comments  
   Users create custom skills with clear descriptions, but the model rarely invokes them autonomously—even for highly relevant tasks. Undermines the extensibility promise.

9. **[#24246 – 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**  
   *priority/p2, kind/bug* | 3 comments  
   Gateway error when too many tools are enabled. Suggests need for smarter tool selection or batching as the tool ecosystem grows.

10. **[#22672 – Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
    *priority/p2, kind/customer-issue* | 3 comments | 1 👍  
    Users report the agent issuing `git reset`, `--force` flags, or risky DB commands when safer alternatives exist. A safety/guardrail request.

## Key PR Progress

1. **[#28403 – Block $VAR and ${VAR} variable expansion bypass](https://github.com/google-gemini/gemini-cli/pull/28403)**  
   *priority/p1, area/security* | Fixes GHSA-wpqr-6v78-jr5g  
   Hardens shell substitution detection against bypasses. Critical security fix under active review.

2. **[#28470 – Enforce workspace trust and task isolation for a2a-server](https://github.com/google-gemini/gemini-cli/pull/28470)**  
   *area/security* | Closed (merged)  
   Prevents zero-click RCE in untrusted workspaces. Major security refactor of the A2A server backend.

3. **[#28469 – Rotate session ID on model fallback](https://github.com/google-gemini/gemini-cli/pull/28469)**  
   *fix(core)* | Opens  
   Fixes a blocking API error when fallback to `gemini-2.5-flash` occurs under the same stale session ID.

4. **[#28472 – Sequentially verify cached credentials](https://github.com/google-gemini/gemini-cli/pull/28472)**  
   *fix(core)* | Opens  
   Resolves GCA Agent Mode fatal auth error (exit code 41) in VS Code caused by a credential fallback regression.

5. **[#28389 – Real-world time budget to prevent infinite-loop state transitions](https://github.com/google-gemini/gemini-cli/pull/28389)**  
   *priority/p1, area/agent* | Opens  
   Adds a wall-clock deadline to `sendMessageStream` and `processTurn` to break infinite event-driven loops.

6. **[#28397 – Remove synchronous I/O from shell tool critical path](https://github.com/google-gemini/gemini-cli/pull/28397)**  
   *area/core* | Opens  
   Replaces `fs.mkdtempSync`/`existsSync`/`statSync` with async `node:fs/promises`. Aims to stop UI stuttering in the Ink terminal.

7. **[#28394 – Remove temp files on background process exit](https://github.com/google-gemini/gemini-cli/pull/28394)**  
   *area/core* | Opens  
   Fixes a temporary directory leak for `is_background: true` shell commands.

8. **[#28386 – Track VS Code activation disposables](https://github.com/google-gemini/gemini-cli/pull/28386)**  
   *priority/p2, area/core* | Opens  
   Fixes a subtle bug where comma expressions caused only the last `Disposable` to be tracked, leaking subscriptions.

9. **[#28305 – Tool call formatter & failure summaries for evals](https://github.com/google-gemini/gemini-cli/pull/28305)**  
   *area/evals* | Opens  
   Prints a compact numbered timeline of tool calls (with status/errors) when a behavioral eval fails. Improves debugging UX.

10. **[#28474 – Add skill name dimension to tool call telemetry](https://github.com/google-gemini/gemini-cli/pull/28474)**  
    *priority/p3, area/enterprise* | Opens  
    Adds `skill_name` to telemetry labels for enterprise observability. Author notes it was "vibe coded."

## Feature Request Trends
- **Local/offline AI models** (37 👍): The #1 community request. Enterprise data privacy is the driving use case.
- **AST-aware code understanding** (#22745, #22746): Internal initiative to reduce token usage and improve precision via abstract syntax tree analysis.
- **Subagent trajectory visibility** (#22598): Users want subagent traces in `/chat share` for debugging and evaluation.
- **Agent self-awareness** (#21432): Users want the CLI to accurately describe its own flags, hotkeys, and capabilities as a reliable fallback guide.

## Developer Pain Points
- **Agent hangs and infinite loops**: Multiple priority-p1 bugs (#21409, #28362, #25166) where the agent gets stuck indefinitely on simple operations or token drains. This is the top reliability concern.
- **Subagent reliability and false success reports**: Subagents frequently lie about completion status (#22323) or ignore configuration overrides (#22267), undermining trust in autonomous execution.
- **Broken extensibility**: Custom skills and sub-agents are largely ignored by the core agent (#21968), making the platform's extensibility promise hollow in practice.
- **SPoF authentication failures**: The VS Code integration is brittle to credential changes (#28472), causing fatal agent crashes.
- **Shell tool leakiness**: Temp files remain after background execution (#28394), and synchronous I/O causes UI jank (#28397).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-22

## Today's Highlights
The v1.0.74-0 release introduces `/model plan` for per-session model selection in plan mode, but the community is grappling with a concerning regression where plan-mode blocks shell commands previously used to enrich planning. Meanwhile, MCP-related issues dominate the conversation, with support for CIMD remote OAuth, resources/prompts, and resource subscriptions all seeing sustained engagement.

## Releases
**v1.0.74-0** — [Release Notes](https://github.com/github/copilot-cli/releases/tag/v1.0.74-0)
- **Added:** `/model plan` (alias `/model --plan`) to set a specific model while in plan mode. Provide a model ID, `off` to clear, or no ID to open an interactive picker. The CLI reverts to the session model when exiting plan mode.
- **Improved:** Resume search now matches session titles even when whitespace differs, making session recovery more robust.

## Hot Issues (10 Noteworthy)
1. **[#1305 — Support CIMD for Remote OAuth MCP Servers](https://github.com/github/copilot-cli/issues/1305)** (4 comments, 👍26)  
   *Why it matters:* The push for Dynamic Client Registration (DCR) in MCP has high community demand. With 26 upvotes, this is the most-wanted MCP auth improvement. Enables "just-in-time" OAuth client registration—critical for enterprise MCP deployments.

2. **[#4188 — Regression on plan-mode: shell commands blocked](https://github.com/github/copilot-cli/issues/4188)** (3 comments, 👍2)  
   *Why it matters:* A core workflow regression. Plan mode previously used shell commands (e.g., `gh` CLI) to enrich plans, but they are now blocked. This breaks established user workflows and has high urgency.

3. **[#2193 — Default model configuration for /fleet subagents](https://github.com/github/copilot-cli/issues/2193)** (3 comments, 👍14)  
   *Why it matters:* Fleet users must repeat model preferences in every prompt. 14 upvotes underscore the need for global/project-level default model config for subagents.

4. **[#4012 — BYOK: reasoning effort not supported for model "glm-5.2:cloud"](https://github.com/github/copilot-cli/issues/4012)** (2 comments, 👍16)  
   *Why it matters:* BYOK (Bring Your Own Key) users hitting model-specific feature gaps. 16 upvotes reflect broad demand for better BYOK model compatibility and error messages.

5. **[#1518 — Support MCP resources and prompts](https://github.com/github/copilot-cli/issues/1518)** (2 comments, 👍14)  
   *Why it matters:* Copilot CLI only supports MCP tools, but servers offer three primitives. 14 upvotes show strong desire for full MCP protocol support.

6. **[#4163 — Zombie child processes accumulate under copilot PID](https://github.com/github/copilot-cli/issues/4163)** (2 comments, 👍0)  
   *Why it matters:* A system-level reliability bug—zombie processes leak at ~2/minute, degrading performance over long sessions. Under-reported but serious.

7. **[#4183 — Auto-compaction doesn't prevent CAPI 5 MB body limit failure](https://github.com/github/copilot-cli/issues/4183)** (1 comment, 👍5)  
   *Why it matters:* Long, tool-heavy sessions hit a hard 5 MB serialization limit even with auto-compaction. A silent blocker for power users running complex agents.

8. **[#4206 — Environment footer stuck on "Loading:" forever](https://github.com/github/copilot-cli/issues/4206)** (1 comment, 👍1)  
   *Why it matters:* MCP handshake stalls under org MCP policies leave users in a permanently "loading" state. A UX dead-end that makes the CLI unusable until fixed.

9. **[#1803 — Support MCP resources/read primitive](https://github.com/github/copilot-cli/issues/1803)** (1 comment, 👍8)  
   *Why it matters:* Building block for full MCP resource support. 8 upvotes, referenced by #1518 and #3073—a key dependency for autonomous agent workflows.

10. **[#4208 — Support explicit inline custom agent invocation and chaining](https://github.com/github/copilot-cli/issues/4208)** (0 comments, 👍3)  
    *Why it matters:* Users want to compose agents within a single prompt—invoking specific `.github/agents` mid-conversation. A sign of maturing agent ecosystems.

## Key PR Progress
- **[#3163 — ViewSonic monitor](https://github.com/github/copilot-cli/pull/3163)**  
  A monorepo-focused PR initiating GitHub Actions runners for #2591, #3561, and #3559. Still open after two months; likely stalled on CI configuration.

*Note: Only 1 PR was updated in the last 24 hours. The repository shows a lower PR velocity compared to Issue volume.*

## Feature Request Trends
1. **Full MCP Protocol Support** — The #1 theme. Requests for `resources/read`, resource subscriptions (`notifications/resources/updated`), and `prompts` primitives (#1518, #1803, #3073) collectively draw >30 upvotes. Remote OAuth MCP with CIMD/DCR (#1305, #4203) is the secondary MCP push.

2. **Agent Composition & Configuration** — Users want default model config for `/fleet` subagents (#2193), inline agent chaining (#4208), custom agent access to `skill` tools (#4209), and `.agents` discovery for instructions/hooks (#4204). The ecosystem is demanding better agent orchestration.

3. **Model Configuration & Switching** — Rapid model switching presets (#4190), per-plan model selection (now shipped in v1.0.74-0), and BYOK reasoning-effort compatibility (#4012) show users want finer-grained model control without disrupting workflow.

4. **Credit & Usage Transparency** — Per-subagent AI credit breakdown in `/usage` (#4207) and configurable retry counts (#4210) reveal demand for operational observability.

## Developer Pain Points
- **Plan-mode regression (#4188)** is the most immediate frustration—a feature regression that strips power from established workflows.
- **Zombie processes (#4163)** and **5 MB body limit failures (#4183)** indicate systemic reliability issues for heavy session users.
- **MCP handshake stalls under org policies (#4206)** and **OAuth refresh failure (#4203)** create hard blocks for enterprise adopters.
- **Terminal rendering bugs** — dark-on-dark in tmux (#4212), clipboard failures in WSL/tmux nesting (#4191), and BigInt serialization crashes (#4211) degrade the daily experience.
- **Regression churn** — the `view` tool broke in v1.0.72/73 for existing files (#4202), and BYOK streaming delta issues (#4196) suggest quality assurance gaps in recent releases.
- **MCP tool list staleness (#3125)** — mid-turn tool changes aren’t visible until the next user turn, a subtle but impactful limitation for dynamic tool ecosystems.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest**
*Date: 2026-07-22*

---

### 1. Today's Highlights

Three new bugs were opened within the last 24 hours, all impacting core functionality on the latest v0.28.1 release: a critical regression where **k2.5 tool calling is completely broken** (Issue #2527), a Windows-specific **numpad input not being captured** (Issue #2529), and a **shell mode output flooding** issue when using `!` prefix commands (Issue #2528). These overshadow the day's lone Pull Request, which targets a long-standing **shell hang issue** (#2468) caused by detached child processes holding pipes open.

---

### 2. Releases

**No new releases in the last 24 hours.** The latest published version remains **v0.28.1**.

---

### 3. Hot Issues

*(Picking from the 4 items updated in the last 24h, as that is the full set)*

| # | Issue | Title | Why It Matters | Community Reaction |
|---|-------|-------|----------------|-------------------|
| 1 | [#2527](https://github.com/MoonshotAI/kimi-cli/issues/2527) | **k2.5 model tool calling completely invalid + goal mode infinite loop** | A **critical functional regression** for the K2.5 model. The tool execution layer returns "Tool not found" for all formats (Bash, JSON, etc.), and Goal Mode enters an infinite loop. This blocks any automated workflow using the latest model. | Opened today, 0 comments yet, but the description is thorough with exact failure modes. High severity. |
| 2 | [#2529](https://github.com/MoonshotAI/kimi-cli/issues/2529) | **Right-side numpad input not captured** | **Windows-specific UI bug** — users relying on a numeric keypad for efficiency cannot interact with the input box. Suggests a missing key event listener for Numpad keys. | Freshly opened, no comments. Minor impact severity but clear and reproducible. |
| 3 | [#2528](https://github.com/MoonshotAI/kimi-cli/issues/2528) | **Shell mode output too long** | Typing `!` in shell mode triggers an unexpectedly long text output, likely a formatting or streaming glitch in the Shell interpreter. Could clutter terminal history. | Opened today, no comments. Moderately annoying for heavy shell-mode users. |
| 4 | [#2474](https://github.com/MoonshotAI/kimi-cli/issues/2474) | **CLI interface constantly shaking / re-rendering from scratch** | **Persistent UI jitter on Linux (v0.19.2).** The entire conversation terminal re-renders, causing visual shaking. Similar to an uncontrolled `useEffect` loop in the TUI layer. Reported 27 days ago; still open. | 2 upvotes, 1 comment. Affects users on older LS kernel environments. Low activity suggests a tricky root cause. |

---

### 4. Key PR Progress

*(Only 1 PR was updated in the last 24 hours)*

| # | PR | Description | Status | Significance |
|---|----|-------------|--------|--------------|
| 1 | [#2530](https://github.com/MoonshotAI/kimi-cli/pull/2530) | **fix(shell): stop blocking until timeout when a detached child holds pipes** | **Open** (Created today by ayaangazali) | Addresses [#2468](https://github.com/MoonshotAI/kimi-cli/issues/2468) — a classic **background-process hang**. In shell mode, commands like `some_daemon & echo done` leave a detached child holding stdout/stderr, causing `_run_shell_command` to block forever waiting for EOF. The fix adds an exit-code check before waiting on pipes. **High-value fix for shell reliability.** |

---

### 5. Feature Request Trends

Based on the open issues in this 24-hour window, the implicit feature request from the community is:

- **Robustness of Tool Calling across model versions**: The complete failure of tool calling in k2.5 (Issue #2527) and the general pattern of "Tool not found" errors suggests users need **better abstraction between model-specific tool formats and the execution layer**. A unified tool dispatch mechanism would prevent model upgrades from breaking workflows.

---

### 6. Developer Pain Points

Recurring frustrations visible in the latest data:

| Pain Point | Evidence | Frequency |
|------------|----------|-----------|
| **Tool execution fragility** | #2527 — tool calling fails entirely for k2.5; formats not recognized | Critical (1 new report today) |
| **Terminal UI instability** | #2474 — continuous shaking/re-rendering on Linux (still unresolved after 27 days) | Persistent (low activity, hard to fix) |
| **Input method gaps** | #2529 — Windows numpad not captured | Low severity but clear gap in keybinding coverage |
| **Shell mode blocking / flooding** | #2528 (output too long), #2530 (hang on detached child) | Two distinct issues affecting shell-mode interactivity today |

The dominant pattern: **regression in model integration** (tool calling) and **shell-mode reliability** are the most acute developer pain points this week.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-22

## Today's Highlights

Memory management and layout transitions dominate today's digest, with the **Memory Megathread** (#20695) continuing as the most-engaged community issue at 119 comments. A wave of **layout-related bugs** (#37012, #37546, #38124) is emerging as users migrate to the new tabbed UI, while the team merges critical fixes for **WSL boot-order crashes** (#37481) and **Copilot API endpoint discovery** (#38184). No new releases in the last 24 hours.

## Releases

*No new releases in the last 24 hours.*

## Hot Issues

1. **[#20695 — Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)** (119 comments, 90 👍)
   The central tracking issue for all memory-related bugs. The author explicitly discourages LLM-suggested solutions and requests manual heap snapshots. Highest engagement issue by a wide margin, indicating systemic memory pressure across the application.

2. **[#37012 — Keep legacy layout option](https://github.com/anomalyco/opencode/issues/37012)** (26 comments, 27 👍)
   Strong community pushback against the new layout, citing loss of easy access to tools and workspace functionality. Users want a toggle to stay on the old layout permanently.

3. **[#38190 — Request blocked by upstream provider](https://github.com/anomalyco/opencode/issues/38190)** (7 comments, 3 👍)
   A generic upstream blocking error with no clear provider—affects chat message sending. Quickly closed, suggesting a transient or config issue.

4. **[#33028 — Subagents hang indefinitely after bash tool call](https://github.com/anomalyco/opencode/issues/33028)** (7 comments, 3 👍)
   Subagents freeze after fast shell commands; only manual kill unblocks. Reproduced with two different models and providers. Critical for workflow reliability.

5. **[#37790 — Go subscription paid but "Insufficient balance"](https://github.com/anomalyco/opencode/issues/37790)** (10 comments, 0 👍)
   Stripe payment processed but workspace shows insufficient balance. Billing state mismatch that blocks paid users from using the service.

6. **[#34652 — SchemaError on nested array arguments with Anthropic provider](https://github.com/anomalyco/opencode/issues/34652)** (5 comments, 0 👍)
   Anthropic native provider returns JSON-encoded strings for array params (e.g., `todowrite`), triggering hard `SchemaError`. Does not affect OpenAI provider—provider-specific serialization mismatch.

7. **[#37546 — Web: no way to revert new layout, workspaces missing](https://github.com/anomalyco/opencode/issues/37546)** (4 comments, 5 👍)
   Web users past v1.17.19 cannot revert to legacy layout, and the new layout lacks git worktrees entirely. A blocker for users depending on workspace management.

8. **[#38124 — Existing profiles not eligible for layout transition toggle](https://github.com/anomalyco/opencode/issues/38124)** (3 comments, 1 👍)
   The layout rollback UI is gated on an eligibility flag that only initializes during desktop onboarding. Existing web profiles are locked into the new layout.

9. **[#38201 — TUI input frozen with large binary files](https://github.com/anomalyco/opencode/issues/38201)** (1 comment, 0 👍)
   Project copy refresh hangs when the directory contains large binaries (MP3, ROM, PNG). TUI renders but input is dead—likely an async I/O bottleneck.

10. **[#31119 — Error: no such column: name](https://github.com/anomalyco/opencode/issues/31119)** (14 comments, 15 👍)
    App becomes completely unusable after update due to a database schema mismatch. High engagement for a core data-layer regression.

## Key PR Progress

1. **[#38206 — Cache all system messages instead of only first 2](https://github.com/anomalyco/opencode/pull/38206)** (opened today)
   Fixes a subtle provider optimization bug where `applyCaching()` sliced system messages to only the first 2, discarding plugin and MCP instructions. Important for prompt fidelity in complex setups.

2. **[#38186 — Fix unavailable notification state for WSL sidecar](https://github.com/anomalyco/opencode/pull/38186)** (closed)
   Defers permission and notification reads until the matching server sync is available—follow-up to the WSL boot-order crash fix. Reactive approach avoids the fatal error on launch.

3. **[#38080 — Show running shell command in UI](https://github.com/anomalyco/opencode/pull/38080)** (opened)
   Displays the shell command as soon as tool input is available, including while running. Allows expanding collapsed running shell tools to watch live output. UX improvement for long-running commands.

4. **[#38172 — Support generator functions in codemode](https://github.com/anomalyco/opencode/pull/38172)** (opened)
   Adds lazy `yield`/`yield*`, `next`/`return`/`throw`, and finally completion for sync and async generators. Enables streaming and resource management patterns in code generation.

5. **[#38204 — Await initial Copilot model sync](https://github.com/anomalyco/opencode/pull/38204)** (opened today)
   Loads account-specific Copilot models before installing the initial catalog transform. Prevents exposing bundled model list before remote data arrives. Adds deterministic regression test.

6. **[#38184 — Discover Copilot API endpoint after OAuth](https://github.com/anomalyco/opencode/pull/38184)** (closed)
   Persists the account-specific Copilot API endpoint on V2 device OAuth completion. Removes the need for a separate startup request, improving provider initialization speed.

7. **[#38162 — Reduce snapshot repository setup subprocesses](https://github.com/anomalyco/opencode/pull/38162)** (opened)
   Replaces eight `git config` calls with one atomic rewrite. Reduces focused snapshot test execution time. Performance optimization for snapshot operations.

8. **[#37833 — NVIDIA NIM DeepSeek request compatibility](https://github.com/anomalyco/opencode/pull/37833)** (opened)
   Fixes DeepSeek V4 models on NVIDIA NIM hanging during streaming. Closes a provider-specific integration gap for users running on NVIDIA infrastructure.

9. **[#38200 — Add Solidity file type and highlighting](https://github.com/anomalyco/opencode/pull/38200)** (opened)
   Adds Solidity syntax highlighting support. A straightforward feature addition for the Web3/crypto developer audience.

10. **[#37973 — Make mini resize replay opt-in](https://github.com/anomalyco/opencode/pull/37973)** (opened)
    Stops `--mini` mode from wiping the screen and refetching the session on every terminal resize. Now only replays on explicit user action, preventing scrollback loss and performance hits.

## Feature Request Trends

Three major directions are emerging from recent issues:

1. **Layout persistence and migration**: Users want a toggle to keep the legacy layout (#37012, #37546, #38124). The transition to the new tabbed UI is causing friction, especially on Web where rollback is impossible.

2. **First-party external connectors**: A clear demand for managed OAuth connectors to common SaaS tools—Google Calendar, Gmail, Slack, Notion, Sheets (#38095). Users want the agent to act across external systems without manual MCP configuration.

3. **Session and cost metadata**: Users want auto-naming from first message content (#38163) rather than "New Session" defaults. Also, a longstanding request for total session cost display (#4925) that includes sub-agent token costs is still open.

## Developer Pain Points

- **Memory instability**: The Memory Megathread (#20695) at 119 comments indicates ongoing, hard-to-diagnose memory leaks. LLM-suggested fixes are explicitly discouraged—requires manual heap snapshot collection.
- **Upstream provider errors**: Generic "Request blocked by upstream provider" (#38190) and "Internal Server Error" across all models (#38131) suggest provider integration fragility, especially for non-OpenAI endpoints.
- **Provider-specific schema mismatches**: Anthropic returns JSON-encoded nested arrays (#34652); Google sends numeric enum values (#33041). Each provider requires separate serialization handling.
- **WSL ecosystem reliability**: The desktop app fatally errors when persisted tabs reference WSL servers before the sidecar is ready (#37481). Multi-platform users are directly affected.
- **Subscription billing state bugs**: Paid subscriptions not reflecting in workspace balance (#37790) blocks paying users from using the service—a critical trust issue.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-22

## Today's Highlights

Pi shipped **v0.81.0** and **v0.81.1** within 24 hours, introducing local llama.cpp model management and verifiable release source archives. A critical crash bug in `streamFunction` affected users upgrading to 0.81.0 (issues #6915 and #6918) and was addressed in follow-up PRs. The community also saw strong progress on compaction retry logic, external editor speedups, and a new agent harness execution abstraction.

## Releases

- **[v0.81.1](https://github.com/earendil-works/pi/releases/tag/v0.81.1)** — Verifiable release source archives: deterministic, checksummed source archives with instructions for rebuilding standalone binaries. Includes documentation for the rebuild process.
- **[v0.81.0](https://github.com/earendil-works/pi/releases/tag/v0.81.0)** — **Local llama.cpp model management**: connect to a llama.cpp router, search and download Hugging Face models, and load/unload models with live progress. Full documentation at [llama-cpp.md](https://github.com/earendil-works/pi/blob/v0.81.0/packages/coding-agent/docs/llama-cpp.md).

## Hot Issues

1. **[#3357](https://github.com/earendil-works/pi/issues/3357) — Official local LLM provider extension (CLOSED)**  
   **30 comments, 43 👍**  
   A long-running, heavily-upvoted issue to dynamically fetch model lists from `{baseUrl}/models` for llama.cpp/ollama/LM Studio integration. Community consensus suggests this is a highly desired capability for offline-first workflows. Closing signals that the 0.81.0 local model management features may address this.

2. **[#6278](https://github.com/earendil-works/pi/issues/6278) — New Claude models fail ~20% of edits (CLOSED)**  
   **23 comments**  
   Claude 4.5+ injects extra keys into edit tool calls (`new_text_x`, `type`, `in_file`), causing validation failures. A significant reliability blocker for Claude users — community frustration is evident from the high comment count and rapid closure.

3. **[#5653](https://github.com/earendil-works/pi/issues/5653) — Move off Shrinkwrap (OPEN, inprogress)**  
   **19 comments**  
   Dual-install of `pi-ai` and `pi-coding-agent` results in two copies of `pi-ai` on disk due to npm shrinkwrap. The module-level `Map` for the provider registry breaks, causing duplicate provider registrations. A fundamental packaging problem affecting all npm-installed users.

4. **[#6915](https://github.com/earendil-works/pi/issues/6915) — Pi crashes with uncaught exception after v0.81.0 update (CLOSED)**  
   **14 comments**  
   `TypeError: streamFunction is not a function` on session resume. Triggered by upgrading to 0.81.0. High severity — immediate community reports and follow-up fixes landed same day.

5. **[#6747](https://github.com/earendil-works/pi/issues/6747) — API for enhancing agent message markdown (OPEN, inprogress)**  
   **7 comments**  
   Extensions need to mutate agent message display without affecting LLM payload. Use case: best-effort formula rendering. Signals demand for richer rendering in the TUI.

6. **[#6774](https://github.com/earendil-works/pi/issues/6774) — Ctrl+G external editor slow on crowded `os.tmpdir()` (OPEN)**  
   **7 comments**  
   Direct tmpfile write causes performance issues when `os.tmpdir()` is cluttered. Proposal: use `mkdtemp` subdirectory. Affects daily editing UX.

7. **[#6918](https://github.com/earendil-works/pi/issues/6918) — Constant crashing — Pi 0.81.0 (CLOSED)**  
   **3 comments**  
   Second report of the same `streamFunction` crash from v0.81.0. Duplicate of #6915, both resolved by subsequent patches.

8. **[#6911](https://github.com/earendil-works/pi/issues/6911) — OpenAI SDK sleeps full Retry-After (days) and Escape can't abort (CLOSED)**  
   **3 comments**  
   SDK `maxRetries` respects unbounded `Retry-After` headers, freezing Pi for hours/days. Escape key does not abort. Critical UX issue for production users hitting rate limits.

9. **[#6920](https://github.com/earendil-works/pi/issues/6920) — Autocomplete crash on `/` input with non-string values (CLOSED)**  
   **3 comments**  
   `TypeError: value.startsWith is not a function` when provider returns non-strings. Interrupts the autocomplete pipeline entirely. Impacts all interactive users.

10. **[#6879](https://github.com/earendil-works/pi/issues/6879) — Auto-compaction never triggers until provider overflow (OPEN)**  
    **2 comments**  
    A 2-hour agentic turn on GPT-5.6 exceeded 100% context window before compaction kicked in at 373k tokens. Proposal: check compaction after every agent turn, not only at request boundaries.

## Key PR Progress

1. **[#6654](https://github.com/earendil-works/pi/pull/6654) — Override prompt cache key (OPEN)**  
   Adds `promptCacheKey` to `StreamOptions` for OpenAI and OpenAI-compatible providers. Enables custom caching strategies beyond session-scoped keys. Useful for shareable prompt caches.

2. **[#6928](https://github.com/earendil-works/pi/pull/6928) — Generate models with reasoning options from models.dev (OPEN)**  
   Syncs thinking/reasoning metadata from a central model catalog. Ensures Pi accurately reflects model capabilities for reasoning levels.

3. **[#6216](https://github.com/earendil-works/pi/pull/6216) — Amazon Bedrock Mantle OpenAI Responses provider (OPEN)**  
   New provider for Bedrock Mantle's OpenAI-compatible API. Unlocks AWS-backend OAI model access for enterprise users.

4. **[#6927](https://github.com/earendil-works/pi/pull/6927) — Native OpenRouter OAuth support (OPEN)**  
   PKCE-based OAuth flow with localhost callback, timeout, and cancellation. Simplifies OpenRouter API key management.

5. **[#6903](https://github.com/earendil-works/pi/pull/6903) — Speed up external editor launch (OPEN)**  
   Moves prompt files into `mkdtemp` subdirectories to avoid `os.tmpdir()` congestion. Direct fix for issue #6774.

6. **[#6913](https://github.com/earendil-works/pi/pull/6913) — Release source archives (CLOSED)**  
   Implements v0.81.1's deterministic source archives with checksums and binary rebuild instructions. Foundation for supply-chain security.

7. **[#6901](https://github.com/earendil-works/pi/pull/6901) — Compaction & branch summarization follow retry policy (CLOSED)**  
   Fixes #6647: compaction and summarization now retry on transient failures using the same retry policy as normal turns. Includes TUI event emission for retry indication.

8. **[#6916](https://github.com/earendil-works/pi/pull/6916) — AgentHarness execution tools (OPEN)**  
   New `AgentHarnessTool` abstraction carrying app-specific context (execution environment, session ID). Enables reusable tool execution across different hosting frameworks.

9. **[#6912](https://github.com/earendil-works/pi/pull/6912) — Never enable SDK Retry-After sleeps (CLOSED)**  
   Forces OpenAI/Anthropic SDK `maxRetries` to 0, replacing SDK-level retries with Pi's agent-level abortable retry logic. Fixes #6911.

10. **[#6572](https://github.com/earendil-works/pi/pull/6572) — Render image blocks in interactive messages (OPEN)**  
    Displays clipboard images in TUI using existing image component, attaches clipboard images to next message, shows pending attachments in footer. Major UX improvement for visual workflows.

## Feature Request Trends

- **Local-first LLM orchestration**: Heavy demand for native llama.cpp, ollama, and LM Studio integration (issues #3357, closed; v0.81.0 release). Community wants Pi as a unified local/remote model router.
- **Extension system expansion**: Multiple requests for markdown rendering hooks (#6747), deferred reload support (#6552), and session replay anchors (#6909). Extensions are becoming a core investment area.
- **Agent execution portability**: The AgentHarness abstraction (#6916) and execution environment tooling signal a push toward reusable, framework-agnostic agent tools.
- **Session management UX**: Archive shortcuts (#6917/#6914), inline image rendering (#6572), and external editor improvements (#6774) show demand for polished day-to-day interaction patterns.
- **Cost transparency**: Requests to use provider-reported costs (#6877, #6881) and model catalog syncing (#6928) indicate growing operational concerns as users scale usage.

## Developer Pain Points

- **Crash trio in 0.81.0**: The `streamFunction` crash (#6915, #6918) affected multiple users upgrading to the latest release. Combined with `Retry-After` freezes (#6911), this eroded confidence in the upgrade path.
- **Duplicate dependency syndrome**: Shrinkwrap-based double-install (#5653) causes silent failures in the provider registry. A structural npm packaging issue that impacts any use of multiple Pi packages.
- **Compaction reliability**: Poor compaction triggering (#6879) led to unchecked context growth, and single transient failures collapsed entire compaction runs (#6647, now fixed). Production users needing long-running sessions are most affected.
- **Windows path handling**: The `find` tool fails on Windows for any pattern with path separators (`src/**/*.ts`) while plain filenames work (#6817). A platform-specific regression affecting substantial user segment.
- **Autocomplete fragility**: Non-string provider returns crash the entire autocomplete pipeline (#6920), and slash-command tab completion prevents argument autocomplete (#5593). Both create friction in the primary interaction mode.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**2026-07-22**

## Today's Highlights
The team shipped **v0.20.1** today with a major fix for the `agent` tool schema that was blocking OpenAI-compatible users. A critical **P1 session model mutation bug** (#7156) was finally closed, and the autofix system gained two important capabilities: keeping failing checks visible until resolution and normalizing empty parameters for worktree-isolated subagent launches. Performance work continues with lazy-loading `undici` from the startup path.

## Releases
**v0.20.1** – Full release with no breaking changes. Key feature: `feat(autofix): label-driven takeover and release; fix forced-dispatch green no-op` (#7165). The autofix system can now take over labeled issues and release fixes when checks pass.

**v0.20.0-preview.0** / **v0.20.0-nightly.20260722** – Both include `test(telemetry): Cover daemon metrics init ordering and document metricReader asymmetry` (#7456).

**cua-driver-rs-v0.7.3** – New prebuilt binaries for macOS (codesigned + notarized), Linux (glibc 2.31+), and Windows, now supporting relative coordinates.

## Hot Issues

1. **#7156 – [CLOSED] Subagent mutates main session model — context overflow recurrence** [P1/bug](https://github.com/QwenLM/qwen-code/issues/7156)
   *The most critical fix of the week.* PR #7119 partially fixed model-override clearing, but a second code path still caused main session context overflow when subagents ran. Community had 11 comments tracking the regression.

2. **#7316 – [CLOSED] OpenAI toolCall breaks subAgent completely** [P2/bug](https://github.com/QwenLM/qwen-code/issues/7316)
   OpenAI-compatible models returned empty strings for optional `working_dir` parameter, causing schema validation failures in worktree-isolated subagents. A blocker for multi-provider setups.

3. **#7056 – [OPEN] VS Code companion fails to connect** [P2/bug](https://github.com/QwenLM/qwen-code/issues/7056)
   Persistent Windows issue: `Qwen ACP process exited unexpectedly (exit code: 0)`. Still awaiting triage after 5 comments and 6 days open.

4. **#7306 – [OPEN] Harden tool-output budgeting, observability, and artifact lifecycle** [P2/enhancement](https://github.com/QwenLM/qwen-code/issues/7306)
   Phase 1 merged (#7323), reducing model-facing characters by ~14k. Community requesting better lifecycle management for long-running sessions.

5. **#7427 – [OPEN] Web shell artifact panel spams fetch errors** [P2/bug](https://github.com/QwenLM/qwen-code/issues/7427)
   Auto-refresh on panel mount triggers repeated `Load artifacts failed: Failed to fetch` toasts. Welcome PR label applied.

6. **#7332 – [CLOSED] enable_thinking=false sent to thinking-only models** [P1/bug](https://github.com/QwenLM/qwen-code/issues/7332)
   Internal operations (context compaction, goal judge) broke `qwen3.8-max-preview` users by forcing thinking off. Quick closure within 24 hours.

7. **#7287 – [OPEN] Auto-memory MEMORY.md not registered in FileReadCache** [P2/bug](https://github.com/QwenLM/qwen-code/issues/7287)
   Memory system loads MEMORY.md into system prompt but rejects `write_file` updates on first attempt because `checkPriorRead()` fails. Blocks reliable persistent memory workflows.

8. **#7301 – [CLOSED] Web Shell loses bearer token on page refresh** [P2/bug](https://github.com/QwenLM/qwen-code/issues/7301)
   `qwen serve --token` only works on initial auto-open; refreshing or copying the URL loses auth. Duplicate #7398 also closed.

9. **#7139 – [CLOSED] Windows Docker sandbox passes invalid workspace cwd** [P1/bug](https://github.com/QwenLM/qwen-code/issues/7139)
   Every shell tool call on Windows fails with `chdir(2) failed` due to path mismatch between Docker bind mount and ACP shell tools.

10. **#5540 – [OPEN] Allow resuming completed background sub-agents** [feature-request](https://github.com/QwenLM/qwen-code/issues/5540)
    Background sub-agents are single-shot; `send_message` to completed agents hard-fails. One-month-old request with steady community interest (4 comments).

## Key PR Progress

1. **#7456 – [MERGED] Test daemon metrics init ordering** ([PR](https://github.com/QwenLM/qwen-code/pull/7456))
   Closed the loop on lazy telemetry SDK work from #7276. Adds assertions for daemon initialization ordering and documents asymmetric metricReader behavior.

2. **#7455 – [MERGED] Lazy-load undici for faster startup** ([PR](https://github.com/QwenLM/qwen-code/pull/7455))
   Moves ~2 MiB of HTTP client parse/compile out of the eager ACP child startup closure. Part of ongoing cold-start optimization (see #7264).

3. **#7403 – [MERGED] Normalize empty working_dir for isolation:worktree** ([PR](https://github.com/QwenLM/qwen-code/pull/7403))
   Direct fix for #7316: treats `working_dir: ""` as unset when `isolation: "worktree"` is requested, unblocking OpenAI users.

4. **#7393 – [OPEN] Memory recall delivery telemetry** ([PR](https://github.com/QwenLM/qwen-code/pull/7393))
   Adds terminal delivery tracking for auto-memory recall — distinguishes "selected" from "actually delivered" to the model.

5. **#7390 – [MERGED] Workspace selector in Web Shell composer** ([PR](https://github.com/QwenLM/qwen-code/pull/7390))
   Fulfills #6700: users can switch workspaces, register directories, or create trusted workspaces directly from the toolbar.

6. **#7438 – [MERGED] Keep failing autofix checks visible** ([PR](https://github.com/QwenLM/qwen-code/pull/7438))
   Prevents the autofix scan from ignoring a still-red check until its commit is positively judged. Critical for CI reliability.

7. **#7465 – [OPEN] Fix Feishu media download stream cancels** ([PR](https://github.com/QwenLM/qwen-code/pull/7465))
   Two unawaited stream cancels in Feishu downloader. Mirrors the #7361 fix for DingTalk.

8. **#7268 – [OPEN] Hot-reload workspace trust changes** ([PR](https://github.com/QwenLM/qwen-code/pull/7268))
   Enables trust-policy changes without daemon restart using snapshot generations. Semantic monitoring closes previous generation before reconciliation.

9. **#7459 – [OPEN] Restore background agent roster on session reopen** ([PR](https://github.com/QwenLM/qwen-code/pull/7459))
   Interrupted agents return as paused, completed agents retain task IDs. `list_agents` read-only endpoint added for visibility.

10. **#7463 – [OPEN] Java SDK daemon transport** ([PR](https://github.com/QwenLM/qwen-code/pull/7463))
    Adds Java 11 daemon transport to `qwencode-sdk` (v0.1.0-alpha). Thread-scoped sessions with streaming completion and structured errors.

## Feature Request Trends
- **Sub-agent lifecycle persistence** (#5540, #7426, #7459): Multiple PRs and issues target keeping background agents resident after completion, with resume capability and improved roster management.
- **Web Shell UX improvements** (#6700, #6701, #7390, #7380, #7430): Workspace selectors, "Start In" context pickers, subagent detail panels, and session rendering optimization dominate UI requests.
- **Cold-start performance** (#7264, #7455): Systematic audit of ACP child process startup, with lazy-loading of undici and telemetry SDK yielding measurable improvements.

## Developer Pain Points
- **Model-switching mutations** (#7156, #7315, #7433): Subagent execution silently overwriting main session model settings remains the most dangerous recurring bug, causing context overflow and 400 errors.
- **OpenAI compatibility gaps** (#7316, #7403): Empty string coercion for optional fields and mandatory parameter handling continue to frustrate users with non-Qwen providers.
- **Windows sandbox tool execution** (#7056, #7139): Path mapping between Docker containers and Windows filesystem consistently breaks shell tools during E2E and sandbox operations.
- **Token/auth persistence** (#7301, #7398): Web Shell token loss on refresh and token usage deletion on conversation cleanup degrade the user experience for serve-mode users.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-22

## Today's Highlights
CodeWhale v0.9.1 entered its final integration sprint, with 24 closed issues and 5 merged PRs in the last 24 hours targeting release-blocker bugs. Key fixes landed for sub-agent worktree isolation, TUI scrolling for long outputs, and Enter-key send latency that had plagued users across multiple versions. The project also saw its first HarmonyOS build succeed, expanding platform reach.

## Releases
No new releases in the last 24 hours. The v0.9.1 freeze is active with a completion board issue ([#4650](https://github.com/Hmbown/CodeWhale/issues/4650)) tracking final dogfood and release gate.

## Hot Issues

1. **[#4032](https://github.com/Hmbown/CodeWhale/issues/4032) — Codewhale not following the constitution** (CLOSED, 41 comments)  
   *Why it matters:* User reports Codewhale consistently ignores user-provided scripts to write its own temporary scripts, then justifies the behavior when challenged. This is a fundamental reliability and trust issue in the agent runtime. Community discussion is intense but no resolution details visible.

2. **[#2870](https://github.com/Hmbown/CodeWhale/issues/2870) — EPIC: staged command-boundary refactor** (OPEN, 15 comments)  
   *Why it matters:* This master EPIC tracks the v0.9.1 command execution refactor into mergeable layers. Critical for understanding how all tool/sub-agent orchestration changes connect.

3. **[#4227](https://github.com/Hmbown/CodeWhale/issues/4227) — Help map the CodeWhale tsunami** (OPEN, 11 comments)  
   *Why it matters:* A meta-tooling proposal for a workflow that auto-syncs dev environments with main (10+ PRs/day velocity). Addresses contributor onboarding friction.

4. **[#2766](https://github.com/Hmbown/CodeWhale/issues/2766) — UI refactor needed** (OPEN, 9 comments)  
   *Why it matters:* Core usability complaint: output hard to copy, confirmation pop-ups hide main interface with useless info. Long-running UX debt.

5. **[#2889](https://github.com/Hmbown/CodeWhale/issues/2889) — Work Agent rows: real sub-agent details** (OPEN, 7 comments)  
   *Why it matters:* Restored from deleted issue. Community demands structured agent activity instead of raw tool noise in the sidebar. Central to TUI information architecture.

6. **[#4410](https://github.com/Hmbown/CodeWhale/issues/4410) — Restore xAI device-code OAuth login** (CLOSED, 7 comments)  
   *Why it matters:* xAI auth broken due to hardcoded endpoint path mismatch with official Grok CLI. Blocking anyone using xAI providers.

7. **[#2886](https://github.com/Hmbown/CodeWhale/issues/2886) — Add Gherkin acceptance E2E for tool lifecycle** (OPEN, 6 comments)  
   *Why it matters:* Before moving command ownership, maintainers want behavioral test coverage to prevent regressions. Indicates maturity push.

8. **[#4605](https://github.com/Hmbown/CodeWhale/issues/4605) — Enter key send lag** (CLOSED, 3 comments)  
   *Why it matters:* 200–1200ms freeze on message send, unfixed across 3+ minor versions (0.6.x–0.9.0). High-frequency touchpoint regression. Fixed today by separating UI ack from send prep.

9. **[#4603](https://github.com/Hmbown/CodeWhale/issues/4603) — Long output content cannot scroll** (CLOSED, 3 comments)  
   *Why it matters:* Content truncated beyond viewport with no way to review large diffs/logs. Significant UX gap for power users. Fixed today with PTY scenario lock.

10. **[#4655](https://github.com/Hmbown/CodeWhale/issues/4655) — Self-hosted route limits capped by 4K fallback** (CLOSED, 1 comment)  
    *Why it matters:* Unknown self-hosted models silently capped at 4096 tokens. Fixed today by letting explicit route limits override the compatibility fallback.

## Key PR Progress

1. **[#4675](https://github.com/Hmbown/CodeWhale/pull/4675) — Integrate v0.9.1 runtime and release surface** (OPEN)  
   *V0.9.1 runtime simplification, empty-Work fix, and final TUI color grammar (cool mode colors + warm permission colors).*

2. **[#4673](https://github.com/Hmbown/CodeWhale/pull/4673) — fix(shell): default no-cwd commands to context.workspace** (CLOSED)  
   *Fixes [#4674](https://github.com/Hmbown/CodeWhale/issues/4674): sub-agent worktrees were running commands in the parent checkout. Now defaults to `context.workspace` for sub-agent isolation.*

3. **[#4678](https://github.com/Hmbown/CodeWhale/pull/4678) — fix(credit): preserve v0.9.1 integration authorship** (CLOSED)  
   *Maps maintainers to canonical GitHub identities without rewriting commit ancestry. Negative tests for unmodified identities.*

4. **[#4654](https://github.com/Hmbown/CodeWhale/pull/4654) — fix(tui): acknowledge Enter before slow send prep** (CLOSED)  
   *Fixes [#4605](https://github.com/Hmbown/CodeWhale/issues/4605): immediate UI ack ("Preparing") prevents perceived freeze during 200–1200ms send prep. Contributor: @SamhandsomeLee.*

5. **[#4653](https://github.com/Hmbown/CodeWhale/pull/4653) — test(tui): lock long-output transcript scrolling** (CLOSED)  
   *Fixes [#4603](https://github.com/Hmbown/CodeWhale/issues/4603): end-to-end PTY scenario with 3+ viewports of output, verifying retain-beyond-viewport behavior.*

6. **[#4652](https://github.com/Hmbown/CodeWhale/pull/4652) — feat(cli): add --no-project-config for reproducible exec** (CLOSED)  
   *Enables headless reproducible config surface, supporting Verifiers v0.2.1 harness integration.*

7. **[#4658](https://github.com/Hmbown/CodeWhale/pull/4658) — feat(runtime-api): add provider registry + switch endpoints** (CLOSED)  
   *Three new API endpoints enabling dynamic provider/model picker without fragile multi-step config clobbering. Contributor: @gaord.*

8. **[#4656](https://github.com/Hmbown/CodeWhale/pull/4656) — fix(route): honor explicit limits for unknown local models** (CLOSED)  
   *Fixes [#4655](https://github.com/Hmbown/CodeWhale/issues/4655): unknown self-hosted wire aliases now respect configured output limits instead of 4K fallback. Contributor: @h3c-hexin.*

9. **[#4657](https://github.com/Hmbown/CodeWhale/pull/4657) — fix(streaming): report progress on idle timeouts** (CLOSED)  
   *Includes byte/timing telemetry in SSE idle-timeout errors. Distinguishes prefill stalls from mid-stream stalls. Contributor: @h3c-hexin.*

10. **[#4613](https://github.com/Hmbown/CodeWhale/pull/4613) — fix(tui): sanitize Moonshot tool parameters per MFJS spec** (CLOSED)  
    *Moonshot/Kimi tool validation fixes: `apply_patch`, `financial_report` tools previously broke due to unsupported root-level `anyOf`/`oneOf`. Contributor: @bistack.*

## Feature Request Trends

- **Unified provider/model configuration**: Multiple requests for a single-screen provider setup with full catalog visibility ([#4651](https://github.com/Hmbown/CodeWhale/issues/4651), [#4639](https://github.com/Hmbown/CodeWhale/issues/4639), [#4660](https://github.com/Hmbown/CodeWhale/issues/4660)). Users want progressive disclosure instead of provider-specific global residue.
- **Skill management consolidation**: Strong sentiment to make `/skills` the single command family for skill lifecycle, rejecting new parallel command families ([#4651](https://github.com/Hmbown/CodeWhale/issues/4651)).
- **Permission model clarity**: Community wants one typed permission decision (Ask/Auto-Review/Full Access) before every tool call, with durable state across restarts ([#4628](https://github.com/Hmbown/CodeWhale/issues/4628), [#4412](https://github.com/Hmbown/CodeWhale/issues/4412)).
- **Work/agent visualization**: Persistent requests for structured agent activity display instead of raw tool noise, with one truthful queue and clear mode/permission indicators ([#2889](https://github.com/Hmbown/CodeWhale/issues/2889), [#4636](https://github.com/Hmbown/CodeWhale/issues/4636), [#2766](https://github.com/Hmbown/CodeWhale/issues/2766)).

## Developer Pain Points

- **Multi-version performance regression**: Enter-key send lag affecting 0.6.x–0.9.0 with no fix until today ([#4605](https://github.com/Hmbown/CodeWhale/issues/4605)). Indicates inadequate performance testing across versions.
- **Content truncation and reviewability**: Long outputs (diffs, logs, multi-turn conversations) silently truncated with no scroll mechanism ([#4603](https://github.com/Hmbown/CodeWhale/issues/4603)). Core UX gap for power users on all platforms.
- **Sub-agent worktree isolation failure**: Bash tools defaulting to parent workspace when sub-agent spawned with `worktree: true`, causing cross-contamination ([#4674](https://github.com/Hmbown/CodeWhale/issues/4674)). Root cause: `cwd: None` fallthrough.
- **Self-hosted model cap confusion**: Unknown wire aliases silently restricted to 4096 tokens with no user-facing warning ([#4655](https://github.com/Hmbown/CodeWhale/issues/4655)). Affects anyone using custom/local model endpoints.
- **OAuth provider fragmentation**: xAI device-code auth broken by hardcoded endpoint, needing per-provider path discovery ([#4410](https://github.com/Hmbown/CodeWhale/issues/4410)). Pattern could affect other providers.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*