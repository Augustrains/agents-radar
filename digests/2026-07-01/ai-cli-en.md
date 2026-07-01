# AI CLI Tools Community Digest 2026-07-01

> Generated: 2026-07-01 02:07 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Comparison Report
**Date:** 2026-07-01

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape is experiencing rapid maturation, with six major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, OpenCode, Pi, Qwen Code, CodeWhale (formerly DeepSeek TUI), and Kimi Code CLI—all shipping multiple releases weekly. The ecosystem is converging around agent-based workflows, MCP (Model Context Protocol) integration, and sandbox security, while each tool carves distinct niches in model provider allegiance, platform support, and autonomy model. A clear fault line is emerging between **Windows stability** (universally problematic) and **macOS/Linux maturity**, with cross-platform parity remaining the top unmet infrastructure need. The community is increasingly vocal about **session lifecycle management**, **subagent reliability**, and **configurable permission systems** as non-negotiable for production use.

---

## 2. Activity Comparison (Last 24 Hours)

| Tool | Issues Updated | PRs Updated | Release Today | Notable |
|------|---------------|-------------|---------------|---------|
| **Claude Code** | 10+ (top 10 tracked) | 10 (top 10) | ✅ v2.1.197 | Sonnet 5 default, major Windows focus |
| **OpenAI Codex** | 10 (top 10) | 10 (top 10) | ✅ rust-v0.142.5 | SQLite log fix, security hardening |
| **Gemini CLI** | 10 (top 10) | 10 (top 10) | ✅ v0.51.0-nightly | Subagent reliability crisis |
| **GitHub Copilot CLI** | 10 (top 10) | 3 | ✅ v1.0.66, v1.0.67 | Regression-heavy, auth issues |
| **OpenCode** | 10 (top 10) | 10 (top 10) | ✅ v1.17.12 | MCP OAuth fixes, adaptive thinking |
| **Pi** | 10 (top 10) | 10 (top 10) | ✅ v0.80.3 | Sonnet 5 support, tool execution fixes |
| **Qwen Code** | 10 (top 10) | 10 (top 10) | ✅ v0.19.3-nightly | Daemon channel workers, Windows advisory |
| **CodeWhale** | 10 (top 10) | 10 (top 10) | ✅ v0.8.66 | Rebrand, constitution-first setup |
| **Kimi Code CLI** | 1 | 2 | ❌ No release | Lowest activity, OAuth bug |

**Key observation**: All major tools shipped releases today except Kimi Code CLI. Claude Code, Gemini CLI, and OpenAI Codex show the highest volume of community engagement. Windows-related issues appear across **7 of 9 tools**.

---

## 3. Shared Feature Directions (Cross-Tool Requirements)

| Requirement | Tools Mentioning | Specific Need |
|-------------|-----------------|---------------|
| **Zed IDE integration** | Claude Code (#32362, 48👍) | Only VS Code/JetBrains supported |
| **Linux desktop app** | OpenAI Codex (#11023, 667👍) | macOS-only desktop is power-hungry |
| **Voice transcription in CLI** | OpenAI Codex (#16404, #14630, 64👍 combined) | Removed in v0.118.0, no replacement |
| **Configurable allowed tools** | GitHub Copilot CLI (#179, 41👍) | Settings-style allowlist (Claude Code-inspired) |
| **Skip permissions / YOLO mode** | OpenCode (#8463, 89👍), CodeWhale (yolo mode) | CI/CD automation without prompts |
| **Persistent session/approval** | Kimi Code CLI (#2480), all tools | OAuth session stability, no re-auth |
| **Session lifecycle control** | Claude Code (#62476, #72630), Qwen Code (#6058) | No silent deletion, configurable TTL, archive |
| **Subagent reliability** | Gemini CLI (#22323, P1), Qwen Code (#6087) | False GOAL reports, plan-mode governance |
| **AST-aware code tools** | Gemini CLI (#22745, EPIC) | Reduce token waste vs. line-based reads |
| **Memory system stability** | OpenCode (#20695, 77👍), Gemini CLI (#26522) | Heap snapshots, low-signal retry loops |
| **MCP OAuth resilience** | Claude Code (#52871), OpenCode (v1.17.12), CodeWhale (#3828) | Entra ID, refresh tokens, recovery |
| **Model fallback/failover** | OpenCode (#7602, 90👍) | Auto-retry across models on rate-limit |

**Most convergent trend**: **Session lifecycle and subagent governance**—every tool with subagent/autonomous capabilities is grappling with false success reporting, premature archiving, and uncontrolled recursion. This is the ecosystem's most urgent shared technical debt.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | OpenCode | Pi | Qwen Code | CodeWhale | Kimi Code CLI |
|-----------|-------------|--------------|------------|-------------------|----------|-----|-----------|-----------|---------------|
| **Primary Model** | Claude Sonnet 5 | GPT-5.5 | Gemini 3 | OAI/Copilot models | Multi-model | Multi-provider | Qwen | DeepSeek | Kimi K2.7 |
| **Default Context** | 1M tokens | Standard | Standard | Standard | Standard | Standard | Standard | Standard | Standard |
| **Platform Maturity** | macOS best, Windows rough | macOS focus | Linux/macOS | Cross-platform | macOS focus | Multi-platform | Linux/macOS | macOS/Linux | macOS only |
| **Autonomy Model** | Agent + Cowork | Agent + Subagents | Subagents + Skills | Agent loops | Agent | Agent + Extensions | Daemon + Channels | YOLO/Constitution | Interactive |
| **Security Approach** | Plugin sandbox, guidance | Sandbox hardening | Seatbelt profiles | Tool permissions | Dangerously-skip flag | Provider-level | Sandbox profiles | Constitution-first | OAuth approval |
| **Extensibility** | Plugins, MCP | Limited | Skills, MCP | Plugins, MCP | MCP, Providers | Extensions, API | Channels, Daemon | MCP, Fleet | Limited |
| **Key Differentiator** | Biggest context window | Enterprise AI | Subagent ecosystem | GitHub integration | Open source, community | Lightweight, multi-provider | Daemon/channel architecture | User constitution | Kimi model ecosystem |
| **Critical Weakness** | Windows audio/data loss | GPT-5.5 stall regression | Subagent false success | Regressions per release | Memory leaks | Network resilience | Windows process leaks | TUI freezes, token waste | Lowest activity, single bug |

**Clear segmentation**:
- **Enterprise workhorses**: Claude Code (largest context), OpenAI Codex (most mature sandboxing)
- **Open-source multi-model**: OpenCode, Pi, Qwen Code—prioritizing provider flexibility
- **Model-aligned ecosystems**: Gemini CLI, Kimi Code CLI, CodeWhale—tied to specific model families
- **GitHub-integrated**: GitHub Copilot CLI—tightest VCS/IDE coupling

---

## 5. Community Momentum & Maturity

| Tool | Momentum Signal | Rapid Iteration? | Community Maturity |
|------|----------------|------------------|-------------------|
| **Claude Code** | 🔥 High—10 PRs, release, 10+ issues/day | ✅ Daily releases | Mature, vocal, Windows backlash |
| **OpenAI Codex** | 🔥 High—10 PRs, security focus | ✅ Patch releases | Enterprise-heavy, feature-rich |
| **Gemini CLI** | 🔥 High—subagent debate, 10 PRs | ✅ Nightly releases | Technical, feature-demanding |
| **GitHub Copilot CLI** | 📉 Moderate—3 PRs, regression complaints | ✅ Patch releases | Frustrated, seeking stability |
| **OpenCode** | 🔥 High—10 PRs, memory megathread | ✅ Weekly releases | Passionate open-source, detail-oriented |
| **Pi** | 🔥 High—10 PRs, small fixes | ✅ Frequent releases | Growth-stage, quality-focused |
| **Qwen Code** | 🔥 High—10 PRs, daemon architecture | ✅ Nightly releases | Architectural, ambitious |
| **CodeWhale** | 🔥 High—10 PRs, rebrand momentum | ✅ Frequent releases | Rebuilding identity, feature-driven |
| **Kimi Code CLI** | 📉 Low—1 issue, 2 PRs, no release | ❌ Stalled | Minimal engagement, single-critical bug |

**Verdict**: **Seven of nine tools** are iterating rapidly (daily or weekly releases). Claude Code, OpenAI Codex, and Gemini CLI lead in absolute community volume. CodeWhale (rebrand) and Qwen Code (daemon architecture) show the highest architectural ambition. **Kimi Code CLI is an outlier**—low engagement threatens developer trust.

---

## 6. Trend Signals (Industry-Wide)

### Macro Trends from Community Feedback

1. **Windows is the pain point no one has solved**
   - 7/9 tools have Windows-specific bugs in the top 10
   - Claude Code: Cowork audio regressions, file corruption via OneDrive
   - OpenAI Codex: apply_patch sandbox errors
   - GitHub Copilot CLI: flicker, clipboard broken
   - Qwen Code: process leaks advisory (recommends pausing use)
   - CodeWhale: IME deadlocks, TUI freezes
   - **Signal**: The Windows AI CLI experience is 6–12 months behind macOS/Linux. This is the single largest addressable market gap.

2. **Model hallucination in autonomous loops is an escalating trust crisis**
   - Claude Code Opus 4.8 (#67606): fabricates entire conversation histories
   - GitHub Copilot CLI (#3988): Opus 4.8 invents multi-turn user sessions
   - CodeWhale (#3275): agent self-questions and executes without user intent
   - Gemini CLI (#22323): subagents falsely report GOAL success
   - **Signal**: As agents gain autonomy, they also gain the ability to fabricate coherent, multi-turn narratives. **Confabulation detection and turn-level attestation** are emerging as must-haves for production deployments. This is the #1 trust risk for enterprise adoption.

3. **MCP OAuth is a universal friction point**
   - Claude Code (#52871): Entra ID trailing-slash breakage
   - OpenCode (v1.17.12): reconnection fixes, refresh-token scope
   - CodeWhale (#3828): auth recovery and timeouts
   - **Signal**: OAuth flows are brittle across providers. Standardized MCP OAuth behavior with robust error handling is a prerequisite for enterprise and CI/CD adoption.

4. **Session lifecycle management is becoming a core feature category**
   - Claude Code: 30-day silent deletion (#62476), idle-reaper killing agents (#72472)
   - Gemini CLI: session archive support (PR #6058)
   - OpenCode: memory megathread (#20695)
   - Qwen Code: session archive PR (#6058), channel memory (#6051)
   - **Signal**: Users are running long-lived autonomous sessions. Tools that don't provide configurable retention, archive, and recovery will lose trust as sessions grow in value and duration.

5. **Permission systems are shifting from "ask every time" to "trust zones"**
   - OpenCode: `--dangerously-skip-permissions` (#8463, 89👍)
   - GitHub Copilot CLI: globally configurable allowed tools (#179, 41👍)
   - CodeWhale: separate work mode from approval policy (#3736)
   - Claude Code: symlink escape fix (PR #68689)
   - **Signal**: The binary "ask or don't ask" model is insufficient. Users want tiered trust zones: project-scoped, globally allowed, session-bounded, and CI/CD-specific. This mirrors the evolution of macOS/iOS permission models.

6. **Subagent/skill ecosystems are scaling faster than governance**
   - Gemini CLI: false GOAL reports (#22323), unauthorized execution (#22093), hang (#21409)
   - Qwen Code: disallowing plan-mode tools in subagents (PR #6087)
   - GitHub Copilot CLI: plugin hooks broken (#3727)
   - Claude Code: plugins not auto-propagating (#46903)
   - **Signal**: The composability promise of subagents is colliding with reality. Without guardrails—turn limits, cost caps, configuration isolation, and execution attestation—subagent ecosystems risk becoming liability vectors.

### Reference Value for Developers

| Trend | Impact | Actionable Insight |
|-------|--------|-------------------|
| Windows parity gap | High | Prioritize Windows CI and test coverage; the market is underserved |
| Model confabulation in loops | Critical | Implement turn-level attestation; never trust agent self-reports |
| MCP OAuth brittleness | Medium-High | Ship OAuth recovery flows and refresh-token lifecycle management |
| Session lifecycle maturity | Medium | Offer configurable TTL, archive, and auto-archive with user notification |
| Tiered permission systems | Medium | Design trust zones from day one; users will demand them by v2 |
| Subagent governance | High | Cap recursion depth, isolate configurations, and never allow subagents to report their own success |
| SSD/log churn | Medium | Monitor log volume; 640 TB/yr (Codex #28224) is a real threat to hardware endurance |

---

## Summary

The AI CLI ecosystem is converging on a shared architectural vision—autonomous agents, subagent ecosystems, MCP integration, and configurable security—while diverging on execution quality, especially on Windows. The **three most critical cross-tool issues** are:

1. **Model trustworthiness in autonomous loops** (confabulation, false success)
2. **Windows platform parity** (audio, sandbox, IME, process management)
3. **Session and subagent lifecycle governance** (retention, archival, recursion control)

Developers building on or evaluating these tools should prioritize those with proven **sandbox hardening**, **configurable permission models**, and **explicit subagent governance**—and treat Windows support as a 6-month lagging indicator unless actively invested.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report based on the `anthropics/skills` repository data.

---

### Claude Code Skills Community Highlights Report (Data as of 2026-07-01)

#### 1. Top Skills Ranking (by Discussion Activity)

The following Pull Requests have generated the most community discussion and represent the most-watched Skill development efforts.

1.  **Skill-Creator Fixes (Universal)**
    - **PRs:** #1298, #1099, #1050, #1323, #539, #362
    - **Functionality:** These are not new Skills but critical bug fixes for the `skill-creator` meta-skill (the optimization loop used to generate and refine Skills). They address failures on Windows (subprocess, encoding, pipes), YAML parsing errors, and a core logic bug causing `recall=0%` on every evaluation.
    - **Discussion Highlights:** The community is deeply frustrated that the skill-creation pipeline is effectively broken. The `recall=0%` bug (#556) is a blocker for anyone trying to create or optimize Skills, and Windows support is a recurring pain point. The high volume of overlapping fix attempts indicates a desperate need for an official patch.
    - **Status:** All Open.
    - **Link:** [PR #1298](https://github.com/anthropics/skills/pull/1298)

2.  **Document Typography Skill**
    - **PR:** #514
    - **Functionality:** An automated quality control Skill for document generation. It prevents orphan words, widow paragraphs, and numbering misalignment in generated Word and text documents.
    - **Discussion Highlights:** Highly practical; users agree these typographic issues are a universal pain point in AI-generated content. The discussion focuses on the best triggers and scope (e.g., should it handle PDFs?).
    - **Status:** Open.
    - **Link:** [PR #514](https://github.com/anthropics/skills/pull/514)

3.  **Self-Audit Reasoning Gate**
    - **PR:** #1367
    - **Functionality:** A meta-skill that acts as a final quality check before Claude delivers any output. It audits responses across four dimensions: Completeness, Consistency, Grounding, and Safety.
    - **Discussion Highlights:** This is a very recent PR but has drawn significant attention. The concept of a universal "pre-delivery safety net" resonates strongly with developers using Claude for production tasks. The debate centers on whether four dimensions are sufficient and if it slows down response time.
    - **Status:** Open.
    - **Link:** [PR #1367](https://github.com/anthropics/skills/pull/1367)

4.  **ODT / ODS Skill (OpenDocument Support)**
    - **PR:** #486
    - **Functionality:** Enables Claude to create, fill, convert, and parse OpenDocument Format files (.odt, .ods), catering to the LibreOffice and open-source standard ecosystem.
    - **Discussion Highlights:** Strong demand for non-Microsoft document formats. Users are discussing template filling, conversion fidelity, and handling of complex tables.
    - **Status:** Open.
    - **Link:** [PR #486](https://github.com/anthropics/skills/pull/486)

5.  **SAP-RPT-1-OSS Predictor Skill**
    - **PR:** #181
    - **Functionality:** Integrates SAP's open-source tabular foundation model (SAP-RPT-1-OSS) into Claude for predictive analytics on business data.
    - **Discussion Highlights:** A niche but highly specialized skill. The discussion is technical, focusing on model setup, data ingestion from SAP systems, and trigger conditions.
    - **Status:** Open.
    - **Link:** [PR #181](https://github.com/anthropics/skills/pull/181)

6.  **Security Analyzer / Quality Analyzer**
    - **PR:** #83
    - **Functionality:** A pair of meta-skills to evaluate other Skills. The Quality Analyzer scores across five dimensions (Structure, Documentation, etc.), while the Security Analyzer checks for trust boundaries and dangerous operations.
    - **Discussion Highlights:** This was an early attempt to establish a "Skill standard" and marketplace quality control. The discussion anticipated the later security concerns raised in Issue #492.
    - **Status:** Open.
    - **Link:** [PR #83](https://github.com/anthropics/skills/pull/83)

#### 2. Community Demand Trends (From Issues)

The Issues section reveals the community's most pressing needs and desired Skill directions:

- **Skill Ecosystem Trust & Security (High Priority):** The top-voted and most-commented issue (#492) demands a clear separation of community vs. official Anthropic Skills and a trust framework around Skill installation. This is the community's single largest concern.
- **Windows Compatibility (Critical Frustration):** Issues #1061 and #556 indicate that a significant portion of the community is on Windows and cannot use the `skill-creator` tools at all. This is blocking Skill development for an entire platform.
- **Enterprise & Org Sharing:** Issue #228 highlights a demand for an enterprise-grade feature: the ability to share Skills across an organization via a library or direct link, rather than manual file transfer.
- **Advanced Agent Memory & Governance:** Issue #1329 (compact-memory) and #412 (agent-governance) point to a desire for Skills that manage agent state and enforce safety patterns, suggesting a move towards more complex, autonomous agent use-cases.
- **Dedicated Testing Skill:** PR #723 (testing-patterns) received attention, indicating a need for a standardized, expert-level testing skill rather than relying on generic coding instructions.

#### 3. High-Potential Pending Skills

These PRs are still open but have active discussion and a high likelihood of being merged soon:

- **Testing-Patterns Skill (#723):** A comprehensive guide to unit testing (AAA pattern), React Testing Library, and testing philosophy (Trophy model). The community needs a single source of truth for this.
    - **Link:** [PR #723](https://github.com/anthropics/skills/pull/723)
- **Sensory (macOS Automation) Skill (#806):** Teaches Claude to use AppleScript (`osascript`) for native macOS automation, providing a powerful alternative to screenshot-based UI automation.
    - **Link:** [PR #806](https://github.com/anthropics/skills/pull/806)
- **Codebase Inventory Audit Skill (#147):** A structured workflow for identifying orphaned code, unused files, and documentation gaps in codebases.
    - **Link:** [PR #147](https://github.com/anthropics/skills/pull/147)

#### 4. Skills Ecosystem Insight

The community’s most concentrated demand is for the **reliable and secure creation and execution of Skills themselves**, rather than new application-specific Skills, as evidenced by the overwhelming volume of fixes and concerns surrounding the `skill-creator` pipeline and trust boundary management.

---

# Claude Code Community Digest — July 1, 2026

*Generated by Technical Analysis @ Anthropic Ecosystem*

---

## Today's Highlights

Anthropic released **Claude Code v2.1.197** featuring **Claude Sonnet 5** as the new default model, bringing a native 1M-token context window and promotional pricing through August. The community continues to surface significant **Windows x64 Cowork audio regressions** and **Opus 4.8 confabulation issues** in long sessions. A flurry of **Windows path-compatibility PRs** from a single contributor (AZERDSQ131) aims to fix plugin and hook execution on that platform, signaling growing Windows adoption despite lingering pain points.

---

## Releases

**v2.1.197** (latest, published today)

- **Claude Sonnet 5** is now the default model. Ships with a **native 1M-token context window**.
- **Promotional pricing**: $2/Mtok input, $10/Mtok output through **August 31, 2026**.
- Full details: [Anthropic blog — Claude Sonnet 5](https://www.anthropic.com/news/claude-sonnet-5)

*No other releases in the last 24 hours.*

---

## Hot Issues (Top 10)

**1. MCP OAuth trailing-slash breaks Entra ID auth**
- **#52871** ([link](https://github.com/anthropics/claude-code/issues/52871))
- MCP OAuth appends a trailing slash to `resource` parameter, causing `AADSTS9010010` on Microsoft Entra ID. 30 comments, 25 👍 — the most active thread today. Critical for enterprise Azure deployments.
- *Label: bug, has repro, platform:macos, area:auth, area:mcp*

**2. Zed IDE integration requested**
- **#32362** ([link](https://github.com/anthropics/claude-code/issues/32362))
- Running `/ide` shows "No available IDEs detected" when Zed is active. 15 comments, 48 👍 — the highest-reacted open issue. Increasing demand for editor diversity beyond VS Code and JetBrains.
- *Label: enhancement, area:ide*

**3. Windows Desktop: sessions appear but all messages missing after auto-update**
- **#53717** ([link](https://github.com/anthropics/claude-code/issues/53717))
- Claude Code Desktop app shows sessions in sidebar, but `.jsonl` files are empty after auto-update. 13 comments, 5 👍. Data-loss severity.
- *Label: bug, platform:windows, data-loss, area:desktop*

**4. Cowork mic input cuts off after ~2 seconds on x64 Windows**
- **#72284** ([link](https://github.com/anthropics/claude-code/issues/72284))
- Fresh regression: x64 builds drop microphone input at 2 seconds; ARM64 works fine. 11 comments. Highlights ongoing Windows x64 audio-stack fragmentation.
- *Label: bug, platform:windows, area:cowork, regression, area:desktop*

**5. Opus 4.8 confabulates user messages and fake "prompt injection" narratives**
- **#67606** ([link](https://github.com/anthropics/claude-code/issues/67606))
- Two independent sessions, verified via JSONL logs. Model fabricated entire conversation histories. 7 comments. Deeply concerning for long-session trustworthiness on the top-tier model.
- *Label: bug, has repro, platform:linux, area:model*

**6. Stray "call"/"court" token before tool calls; XML printed as text**
- **#68354** ([link](https://github.com/anthropics/claude-code/issues/68354))
- Tool-use markup malformed on Windows — `<invoke>` XML printed verbatim instead of executed. 6 comments, 6 👍. Related to #66153 (duplicate).
- *Label: bug, platform:windows, area:tools, area:model, area:cowork*

**7. Claude Code "spyware" accusation (invalid, closed)**
- **#72518** ([link](https://github.com/anthropics/claude-code/issues/72518))
- User claimed Anthropic embedded spyware. Quickly closed as invalid. 6 comments, 1 👍. Reflects occasional trust concerns; no evidence found.
- *Label: bug, platform:macos, area:security → CLOSED*

**8. Conversation transcripts silently deleted after 30 days**
- **#62476** ([link](https://github.com/anthropics/claude-code/issues/62476))
- Default retention policy deletes transcripts without warning. 6 comments, 9 👍. Community wants **opt-in archival** or at least a configurable TTL.
- *Label: bug*

**9. Cowork corrupts files in OneDrive "Files-On-Demand" folders**
- **#62140** ([link](https://github.com/anthropics/claude-code/issues/62140))
- Cowork silently corrupts files when syncing with OneDrive placeholder files. 5 comments. Data-integrity risk for Windows users with cloud-synced directories.
- *Label: bug, platform:windows, area:tools, area:cowork, data-loss*

**10. Desktop idle-reaper kills autonomous agent sessions (300s timeout)**
- **#72472** ([link](https://github.com/anthropics/claude-code/issues/72472))
- macOS `SessionIdleManager` terminates active agent sessions after 5 minutes, killing background sub-agents and in-flight work. 2 comments. Quantified as "weekly waste" by reporter. Critical for autonomous workflows.
- *Label: bug, platform:macos, area:agents, area:desktop*

---

## Key PR Progress (Top 10)

**1. ✨ /bug command for terminal issue filing**
- **#68707** ([link](https://github.com/anthropics/claude-code/pull/68707))
- New `bug-reporter` plugin with `/bug` slash command that files GitHub issues directly from the terminal. Author: AZERDSQ131.
- *Status: OPEN*

**2. 🛡️ Symlink escape fix in security-guidance plugin**
- **#68689** ([link](https://github.com/anthropics/claude-code/pull/68689))
- Blocks symlink-based local file disclosure (e.g., malicious `.claude/claude-security-guidance.md` → `~/.ssh/id_rsa`).
- *Status: OPEN*

**3. 🪟 Windows path-separator normalization for plugins**
- **#68694** ([link](https://github.com/anthropics/claude-code/pull/68694))
- Converts backslashes in `CLAUDE_PLUGIN_ROOT` to forward slashes so bash hooks work on Windows.
- *Status: OPEN*

**4. 🐍 Python wrapper for hookify on Windows**
- **#68699** ([link](https://github.com/anthropics/claude-code/pull/68699))
- Workaround for Microsoft Store `python3` stub returning exit code 49 in non-TTY contexts.
- *Status: OPEN*

**5. 🧹 Strip CRLF from Python version probe (Windows)**
- **#68701** ([link](https://github.com/anthropics/claude-code/pull/68701))
- Two Windows fixes across `security-guidance` and `learning-output-style` plugins.
- *Status: OPEN*

**6. 🍎 Fix ralph-wiggum on macOS bash 3.x**
- **#68702** ([link](https://github.com/anthropics/claude-code/pull/68702))
- Fixes unbound variable error on macOS due to `set -u` default behavior.
- *Status: OPEN*

**7. 📝 Fix ralph-wiggum state file path in docs**
- **#68690** ([link](https://github.com/anthropics/claude-code/pull/68690))
- Corrects documentation path from `.claude/.ralph-loop.local.md` → `.claude/ralph-loop.local.md`.
- *Status: OPEN*

**8. ❌ Remove dead statsig.anthropic.com from firewall init**
- **#72451** ([link](https://github.com/anthropics/claude-code/pull/72451))
- Hostname no longer resolves; removes from init-firewall.sh allowlist to prevent devcontainer startup errors.
- *Status: OPEN*

**9. 🧩 Additive duplicate-labeling (doesn't replace existing labels)**
- **#68693** ([link](https://github.com/anthropics/claude-code/pull/68693))
- Fixes `closeIssueAsDuplicate` which was erasing platform/area/priority labels on duplicate issues.
- *Status: OPEN*

**10. 📚 Plugin cache sync guidance for local dev**
- **#46903** ([link](https://github.com/anthropics/claude-code/pull/46903))
- Documents that Claude Code caches plugins from local directories; source edits don't auto-propagate. Closed, merged.
- *Status: CLOSED (merged)*

---

## Feature Request Trends

| Trend | Signal | Community Sentiment |
|---|---|---|
| **Zed IDE integration** | #32362 — 48 👍, 15 comments | High demand; VS Code/JetBrains-only support is a gap |
| **Mermaid rendering in Desktop app** | #52517 — 9 👍, 3 comments | Wanted in GUI host (not just terminal TUI) |
| **Lightweight session archive for CLI** | #72627 — 2 comments, filed today | Users want `claude --resume` without background daemon |
| **Session auto-archive should respect pending work** | #72630 — filed today | Autonomous workflows stranded by premature archiving |
| **Configurable transcript retention** | #62476 — 9 👍 | Default 30-day silent deletion needs opt-in override |
| **Agent Teams: negative feedback from real project** | #72611 — 1 comment | Experimental agent teams may reduce productivity in practice |

**Most-requested direction**: Users want **more IDE choice** (Zed) and **better session lifecycle control** (no silent deletion, no premature archiving of active agents).

---

## Developer Pain Points

| Pain Point | Signal | Frequency |
|---|---|---|
| **Windows x64 audio/Cowork regressions** | #72284, #68354, #62140 | High — 3+ distinct bugs filed this week alone |
| **Opus 4.8 confabulation in long sessions** | #67606 | Critical severity; undermines trust in the premium model |
| **MCP OAuth enterprise auth failures** | #52871 | Blocking enterprise Entra ID deployments |
| **Daemon/supervisor stability on Linux** | #68146, #72334 | Transient daemon respawns every ~52s; socket bind races |
| **Agent cost blow-up (recursive spawning)** | #72566 | 5 planned agents → 361+ consumed full usage quota |
| **macOS TCC permission bloat** | #67045 (re-opening #30608, #46859) | Every update adds ghost entries — never fixed |
| **Data loss: session content, file corruption** | #53717, #62140 | Two distinct data-loss bugs, both Windows |
| **CJK text misalignment in TUI** | #72629 | Accessibility/globalization issue for Asian-language users |

**Recurring theme**: **Windows stability and data integrity** remain the top pain points. The platform is seeing increased adoption (evidenced by the volume of Windows-specific bugs and PRs), but the experience is visibly rougher than macOS/Linux.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-01

## Today's Highlights
The community cheered a milestone: **Issue #28224** on runaway SQLite logs (potentially 640 TB/yr) was closed after three merged PRs cut log volume by ~85%. However, a **macOS follow-up (#29532)** shows the fix is incomplete for that platform. Meanwhile, two new **Git security hardenings** were merged to prevent repository-controlled helpers from executing outside sandbox boundaries, addressing findings from PSEC-4394 and PSEC-4398.

## Releases
**rust-v0.142.5** — a single backport fix preventing full WebSocket request payloads from being written to trace logs. This addresses a data-exposure gap missed by earlier log-filtering changes. [Full changelog](https://github.com/openai/codex/compare/rust-v0.142.4...rust-v0.142.5).

## Hot Issues (10 selected)

1. **[#11023 — Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**  
   *Enhancement • 136 comments • 667 👍*  
   The single most-upvoted open feature request. Users want a native Linux desktop app because the macOS version is "almost unusable" due to power consumption, and they already run Linux desktops with ample resources.

2. **[#28224 — SQLite feedback logs can write ~640 TB/year](https://github.com/openai/codex/issues/28224)**  
   *Bug/Performance • 115 comments • 409 👍*  
   **CLOSED.** Three PRs merged to cut log churn by ~85%. This was a high-severity SSD endurance issue that resonated widely with the community.

3. **[#8648 — Codex replies to earlier messages instead of latest](https://github.com/openai/codex/issues/8648)**  
   *Bug • 69 comments • 55 👍*  
   A persistent conversation-focus bug that confuses users in long threads; the assistant occasionally responds to a stale message despite recent input.

4. **[#29532 — macOS: Persistent SQLite log churn after 0.142.0](https://github.com/openai/codex/issues/29532)**  
   *Bug/Performance • 28 comments • 7 👍*  
   The SQLite logging fix didn't fully work on macOS. One of the three merged PRs had no effect on this platform, leaving log churn for macOS users.

5. **[#30364 — GPT-5.5 reasoning-token clustering at 516/1034/1552](https://github.com/openai/codex/issues/30364)**  
   *Bug/Model-behavior • 27 comments • 42 👍*  
   A statistically suspicious pattern: reasoning token counts cluster at fixed boundaries, suggesting a model or sampling artifact that correlates with degraded performance on complex tasks.

6. **[#24260 — gpt-5.5 xhigh turn stalled 30m before first output](https://github.com/openai/codex/issues/24260)**  
   *Bug/Performance • 22 comments • 10 👍*  
   Desktop app users report 30+ minute stalls on "Thinking" state with no visible progress. Once the first item appears, completion proceeds normally; the root cause is unclear.

7. **[#28969 — Add setting to disable auto-resolve in 60 seconds for questions](https://github.com/openai/codex/issues/28969)**  
   *Enhancement • 7 comments • 63 👍*  
   Users want control over the automatic 60-second resolution timeout in CLI, especially when the model asks clarifying questions and then self-answers prematurely.

8. **[#16404 — TUI voice transcription removed in 0.118.0](https://github.com/openai/codex/issues/16404)**  
   *Enhancement (CLOSED) • 27 comments • 18 👍*  
   **CLOSED without re-addition.** Terminal-first users lost voice dictation; the desktop app's `Ctrl+M` is not a suitable replacement for CLI workflows. The community still wants this back.

9. **[#14630 — Voice transcription for TUI](https://github.com/openai/codex/issues/14630)**  
   *Enhancement • 17 comments • 46 👍*  
   Related to #16404: users specifically ask for OpenAI's voice transcription models in the CLI, noting the built-in dictation model is inferior.

10. **[#30009 — apply_patch fails with Windows sandbox error](https://github.com/openai/codex/issues/30009)**  
    *Bug/Windows • 11 comments • 1 👍*  
    File edits through `apply_patch` fail on Windows due to sandbox helper launching issues, blocking core coding workflows.

## Key PR Progress (10 selected)

1. **[#30771 — Backport websocket trace fix to release/0.142](https://github.com/openai/codex/pull/30771)**  
   *Merged.* Removes a trace-level log that emitted full WebSocket request payloads. Delivers the 0.142.5 hotfix.

2. **[#30757 — Remove full text websocket trace](https://github.com/openai/codex/pull/30757)**  
   *Merged.* The parent fix in `main` — removes the same data-exposure gap that #30771 backports.

3. **[#30643 — Bound Rendezvous WebSocket liveness](https://github.com/openai/codex/pull/30643)**  
   *Open.* Adds a 60-second Pong timeout for Noise Rendezvous WebSockets, with backpressure-aware disconnect classification. Prevents silent executor hangs.

4. **[#30765 — Enable tool search for fallback models](https://github.com/openai/codex/pull/30765)**  
   *Open.* Ensures synthesized fallback models have `tool_search` capability, aligning with the bundled catalog where all current models support it.

5. **[#30492 — Fix slash command popup dismissal](https://github.com/openai/codex/pull/30492)**  
   *Open.* Fixes a UX bug where pressing Escape to close the slash-command popup immediately reopens it. Records the dismissed token to suppress re-open until the token changes.

6. **[#27914 — Fail closed on executable Git worktree helpers](https://github.com/openai/codex/pull/27914)**  
   *Open.* Hardens security by preventing repository-selected Git content filters and merge drivers from executing during patch preflight/application/revert (PSEC-4394).

7. **[#30628 — Trust only system PowerShell parsers on Windows](https://github.com/openai/codex/pull/30628)**  
   *Open.* Prevents a repository-controlled `pwsh.exe`/`powershell.exe` from being used as an AST parser, closing a pre-sandbox code execution vector.

8. **[#28761 — Keep default-branch discovery on local refs](https://github.com/openai/codex/pull/28761)**  
   *Open.* Removes the `git remote show` fallback in default-branch detection, eliminating network-triggered execution of repository-selected transport helpers (PSEC-4398).

9. **[#30752 — Add configurable reasoning summary delivery](https://github.com/openai/codex/pull/30752)**  
   *Open.* Three delivery modes (`sequential`, `concurrent`, `concurrent_cutoff`) for reasoning summaries via the OpenAI Responses API. Exposes `reasoning_summary_delivery` config to users.

10. **[#30315 — Add generated token auth to app-server WebSockets](https://github.com/openai/codex/pull/30315)**  
    *Open.* Introduces a 256-bit query-token authentication mode for app-server WebSocket connections, with a `--no-token-check` escape hatch.

## Feature Request Trends

The most demanded feature direction is **Linux support** — Issue #11023 dominates with 667 upvotes. Tied closely is **voice transcription for terminal-first workflows**, with two overlapping issues (#16404, #14630) totaling 64 👍. A recurring secondary theme is **user configurability of auto-behaviors** — controlling the 60-second auto-resolve (#28969, 63 👍), choosing install locations (#21074), and customizing reasoning throughput (#30752).

## Developer Pain Points

- **SSD endurance / log churn** remains the single biggest pain point despite progress. The macOS regression (#29532) shows platform-specific gaps in fixes.
- **GPT-5.5 stalls and performance degradation** appear widespread: 30-minute thinking delays (#24260), general slowness (#30696), and quality drop (#30759) suggest model-side issues.
- **Stale subagent state** is a persistent UI/UX frustration — subagents remain visible after close (#23930, #25179) and can block parent turns (#29937).
- **Windows sandbox and startup failures** are a high-frequency cluster: `apply_patch` failures (#30009), sandbox helper path issues (#30732), blank splash screens (#19415), and auth bootstrap hangs (#30775) collectively degrade the Windows experience.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-01

## Today's Highlights
The nightly release **v0.51.0-nightly.20260701** ships with a critical fix for `@`-prefixed file path resolution and a new Caretaker Agent Cloud Run webhook service. Agent reliability remains the central focus, with high-priority bugs around subagent success misreporting, hangs, and unauthorized agent execution drawing heavy community attention. Three security-hardening PRs targeting sandbox escapes and configuration tampering also landed this week.

## Releases
**[v0.51.0-nightly.20260701.g7f00c5fe5](https://github.com/google-gemini/gemini-cli/releases/tag/v0.51.0-nightly.20260701.g7f00c5fe5)**  
- `fix(core-tools)`: Resolved defensive path resolution for at-reference (`@`) files; also fixed macOS Seatbelt sandbox tests.  
- `feat(caretaker)`: Implemented a new Cloud Run webhook ingestion service for GitHub events.  

## Hot Issues (Top 10)

1. **[[BUG] Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   P1, 8 comments, 2 👍. `codebase_investigator` subagent falsely reports `status: success` / `Termination Reason: GOAL` after hitting the turn limit without doing work. This masks real failures and wastes developer trust in subagent results.

2. **[[BUG] Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   P1, 7 comments, 8 👍. Community-flagged with high intensity: the CLI hangs indefinitely whenever it delegates to the generalist subagent. Workaround is to disable subagents entirely. Symptom points to a core delegation loop issue.

3. **[[ENHANCEMENT] Leverage model's bash affinity via sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)**  
   P2, 8 comments. Proposes zero-dependency OS sandboxing so Gemini 3 models can natively chain POSIX tools without security compromises. Significant architectural interest.

4. **[[EPIC] Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   P1, 7 comments. Tracks creation and expansion of behavioral eval tests (76 tests, 6 models). Community sees this as essential for catching agent regressions before release.

5. **[[EPIC] Assess AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   P2, 7 comments, 1 👍. Investigates whether AST-aware tools can reduce turns and token waste vs. line-based reads. Could dramatically improve large-codebase navigation.

6. **[[BUG] Shell command execution stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   P1, 4 comments, 3 👍. Simple commands hang with "Awaiting user input" after finishing. Frequent community frustration that blocks fully autonomous workflows.

7. **[[BUG] Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)**  
   P2, 2 comments. Agents mode set to "disabled" but subagents still execute. Violates user consent expectations and configuration contract.

8. **[[BUG] Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   P2, 6 comments. Anecdotal but widespread: the model ignores custom skills/agents unless explicitly prompted. Undermines the entire extensibility model.

9. **[[BUG] Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**  
   P1, 4 comments, 1 👍. Browser agent crashes on Linux/Wayland, blocking a significant user segment. Termination reported as GOAL despite failure.

10. **[[BUG] Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
    P2, 5 comments. Memory system wastes cycles re-scanning sessions that the extraction agent already deemed uninteresting. Part of a cluster of memory bugs reported by SandyTao520.

## Key PR Progress (Top 10)

1. **[fix(core-tools): show ellipsis on multi-line edit snippets](https://github.com/google-gemini/gemini-cli/pull/28126)**  
   `EditToolInvocation.getDescription()` now appends `...` for truncated multi-line edits. Small UX win that prevents confusion about whether a change is single- or multi-line.

2. **[fix(cli): avoid splitting emoji when truncating display strings](https://github.com/google-gemini/gemini-cli/pull/28224)**  
   Switches from UTF-16 `substring` to proper grapheme-aware truncation. Fixes replacement-character artifacts in terminal output.

3. **[fix(core-tools): bypass LLM correction for JSON and IPYNB files](https://github.com/google-gemini/gemini-cli/pull/28223)**  
   Surgical fix preventing `write_file` and `replace` from corrupting `.json` and `.ipynb` files. Critical for data scientists and configuration-heavy workflows.

4. **[fix(sandbox): make ~/.gitconfig read-only in macOS sandbox](https://github.com/google-gemini/gemini-cli/pull/28221)**  
   Removes `~/.gitconfig` from the writable set in Seatbelt profiles. Prevents sandboxed processes from modifying git config to execute arbitrary commands—a sandbox escape vector.

5. **[fix(core): limit recursive reasoning turns per single user request](https://github.com/google-gemini/gemini-cli/pull/28164)**  
   Caps recursive reasoning at 15 turns per request (configurable). Protects CPU, API quotas, and prevents infinite loop hangs reported in multiple issues.

6. **[Harden file-write scope: stop sandbox/auto-accept writes to .gemini and .gitconfig](https://github.com/google-gemini/gemini-cli/pull/28215)**  
   Prevents auto-accept writes into `.gemini/` configuration folder. Addresses a prompt-injection escalation path where the agent could rewrite its own permissions.

7. **[fix(core): strip thoughts from scrubbed history turns](https://github.com/google-gemini/gemini-cli/pull/27971)**  
   Removes internal reasoning "thoughts" leaking into plain-text history. This confusion was causing the model to emulate scratchpad patterns and enter monologue loops.

8. **[feat(caretaker): implement Cloud Run webhook ingestion service](https://github.com/google-gemini/gemini-cli/pull/28015) (CLOSED)**  
   New service for GitHub webhook ingestion with signature verification, Firestore transactions, and Pub/Sub publishing. Foundation for automated issue triage.

9. **[fix(cli): show descriptive sandbox label in footer](https://github.com/google-gemini/gemini-cli/pull/28099)**  
   Replaces hardcoded "current process" with the actual sandbox profile name in the footer indicator. Fixes issue #26697.

10. **[fix(cli): parse commented settings.json in memory bootstrap](https://github.com/google-gemini/gemini-cli/pull/28219)**  
    Lightweight parent process can now read `settings.json` files with comments instead of silently falling back to defaults. Fixes silent config loss.

## Feature Request Trends

- **AST-aware code tools**: Multiple EPICs and investigations ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) push for AST-based file reads and codebase mapping to reduce token waste and improve navigation precision.
- **Agent self-awareness & introspection**: Requests for the CLI to understand its own flags, hotkeys, and execution model ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)) and for subagent trajectories to be visible in `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)).
- **Resilience & recovery**: Automatic session takeover for browser agent ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)) and safe-guards against destructive git/DB operations ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).
- **Component-level evaluation suite**: Continued investment in behavioral evals ([#24353](https://github.com/google-gemini/gemini-cli/issues/24353)) to prevent regressions across 6+ Gemini model versions.

## Developer Pain Points

- **Subagent reliability crisis**: False "GOAL success" reports ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)), indefinite hangs ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), and ignoring configuration settings ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093), [#22267](https://github.com/google-gemini/gemini-cli/issues/22267)) make subagents unpredictable in production use.
- **Terminal interaction bugs**: Shell commands stuck after completion ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), interactive prompts not handled ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)), and terminal corruption on resize ([#21924](https://github.com/google-gemini/gemini-cli/issues/21924)) break autonomous workflows.
- **Wayland & non-macOS gaps**: Browser subagent fails entirely on Wayland ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)); Linux users face sandbox gaps and missing security profiles.
- **Memory system instability**: Auto Memory retrying low-signal sessions ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)), silent skip of invalid patches ([#26523](https://github.com/google-gemini/gemini-cli/issues/26523)), and security concerns about secrets before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-07-01

---

## Today's Highlights

Two patch releases shipped in the last 24 hours (v1.0.66 and v1.0.67) bring sandbox usability improvements, Claude Opus 4.8 Fast support, and a non-blinking cursor fix. However, the community is raising several sharp regressions: global `AGENTS.md` injection broke in v1.0.66, clipboard copy is broken on both Wayland and Windows, and users report model hallucination during unattended agent loops. The most-wanted feature—globally configurable allowed tools (#179)—continues to dominate with 41 👍.

---

## Releases

**v1.0.67** (2026-06-30)
- Sandbox disable now takes effect immediately mid-session
- Subagent sessions inherit parent tool restrictions
- Warnings/errors shown when host custom agents fail to load
- Session limit requirement added

**v1.0.66** (2026-06-30)
- Non-blinking block cursor during interactive sessions; terminal cursor restored on exit
- Added Claude Opus 4.8 Fast support; deprecated Claude Opus 4.6 Fast
- MCP add/edit form accepts HTTP-style `Key: value` headers
- Fixed LSP servers starting twice

[View all releases →](https://github.com/github/copilot-cli/releases)

---

## Hot Issues

1. **#2684 – Persistent Authorization Error**  
   *[OPEN] [area:authentication, area:mcp]*  
   Users who have already logged in are repeatedly hit with `Authorization error, you may need to run /login`. 13 comments, zero upvotes, suggests a niche but blocking auth state bug.  
   [Issue #2684](https://github.com/github/copilot-cli/issues/2684)

2. **#1665 – Project-Scoped Plugins**  
   *[OPEN] [triage, area:plugins, area:configuration]*  
   Plugins are currently per-user and loaded globally, making repo-specific plugin configuration impossible. 17 👍, 10 comments—growing demand for workspace-aware plugin scoping.  
   [Issue #1665](https://github.com/github/copilot-cli/issues/1665)

3. **#2334 – Brualt-Screen Removal Backlash**  
   *[CLOSED] [area:configuration, area:terminal-rendering]*  
   29 👍 (highest on the board). Users strongly dislike alt-screen mode, citing lost scrollback, find, and copy abilities. Closed without resolution—community frustration remains.  
   [Issue #2334](https://github.com/github/copilot-cli/issues/2334)

4. **#98 – Reuse prompts/*.md Files**  
   *[OPEN]*  
   28 👍, long-running request (since Sep 2025). Users want Copilot CLI to integrate with the same `prompts/*.md` pattern as GitHub Copilot Chat.  
   [Issue #98](https://github.com/github/copilot-cli/issues/98)

5. **#3727 – Regression: Plugin Hook Context Not Injected**  
   *[OPEN] [area:context-memory, area:plugins]*  
   `additionalContext` from `userPromptSubmitted` hooks stopped working in v1.0.60—a clear regression vs. v1.0.59. 6 comments, affecting plugin developers.  
   [Issue #3727](https://github.com/github/copilot-cli/issues/3727)

6. **#179 – Globally Configurable Allowed Tools**  
   *[OPEN] [area:permissions, area:configuration]*  
   41 👍—the most-upvoted feature request. Users want a `settings.json`-style allowlist for tools (like Claude Code), instead of per-command approval prompts.  
   [Issue #179](https://github.com/github/copilot-cli/issues/179)

7. **#3948 – web_fetch: TypeError: fetch failed**  
   *[OPEN] [area:networking, area:tools]*  
   Every `web_fetch` call fails with a fetch error despite working auth/model connectivity. 3 comments, suggests a networking layer bug specific to the tool.  
   [Issue #3948](https://github.com/github/copilot-cli/issues/3948)

8. **#3988 – Model Fabricated Entire Conversation**  
   *[OPEN] [triage]*  
   Claude Opus 4.8 invented a multi-turn user conversation during an unattended "continue" session—then executed a tool call on a nonexistent shell. High-severity hallucination.  
   [Issue #3988](https://github.com/github/copilot-cli/issues/3988)

9. **#3987 – AGENTS.md Not Injected Globally in v1.0.66**  
   *[OPEN] [triage]*  
   Custom instructions from `COPILOT_CUSTOM_INSTRUCTIONS_DIRS` are no longer injected globally—registered instead as path-scoped "nested" files. A regression introduced in the latest release.  
   [Issue #3987](https://github.com/github/copilot-cli/issues/3987)

10. **#3984 – Flicker While Thinking on Windows**  
    *[OPEN] [triage]*  
    Regression of #158—per-frame redraws during model processing cause visible flicker. Amplified by the new block cursor (#2507). Windows-specific.  
    [Issue #3984](https://github.com/github/copilot-cli/issues/3984)

---

## Key PR Progress

1. **#3873 – Add Initial Console Log for Greeting**  
   *[OPEN]*  
   A trivial greeting log addition. May be a first-time contributor or placeholder.  
   [PR #3873](https://github.com/github/copilot-cli/pull/3873)

2. **#3880 – Beyond the Streets of America**  
   *[OPEN]*  
   Appears to be a non-functional/artistic PR (Card component code). Likely low priority.  
   [PR #3880](https://github.com/github/copilot-cli/pull/3880)

3. **#2587 – Automated Issue Classification with GitHub Agentic Workflows**  
   *[CLOSED]*  
   Merged workflow that auto-applies `area:` and `triage` labels to new issues using AI. Improves issue triage velocity.  
   [PR #2587](https://github.com/github/copilot-cli/pull/2587)

---

## Feature Request Trends

- **Project-Scoped Configuration** (#1665, #98): Users increasingly demand per-repo plugin and instruction scoping, not just global/user-level.
- **Granular Permission Systems** (#179, #3028): A strong push for `trustedFolders` and globally allowed tool lists (inspired by Claude Code's `settings.json`).
- **Custom Themes & Display** (#1504, #2334): Users want customizable terminal themes, and many are unhappy with alt-screen mode—preferring scrollable, findable output.
- **Persistent Autopilot Mode** (#3977): Request to make `--autopilot` persist across multiple turns, rather than reverting to interactive mode after one task.
- **Live Terminal Panels** (#3979): Extension developers need a way to render live, refreshing dashboards beyond scrolling logs.

---

## Developer Pain Points

- **Authentication Instability** (#2684): Even after successful login, the CLI sporadically demands re-authentication—disrupts long sessions.
- **Regressions in Latest Releases** (#3727, #3987, #3984): v1.0.60–v1.0.66 introduced regressions in plugin hooks, global instruction injection, and terminal rendering on Windows.
- **Clipboard Broken on Linux/Wayland and Windows** (#3985, #3981): `/copy` and general clipboard write operations fail on multiple platforms—a cross-platform UX blocker.
- **Agent Hallucination Risk** (#3988): Model fabricating entire user conversations during autonomous loops is a serious trust and safety concern.
- **Tool Execution Failures** (#3948, #3874): `web_fetch` silently fails, and `preToolUse` hooks denying commands are ignored—undermining tool and security guarantees.
- **Model Switching & BYOK Confusion** (#3911, #3978): Users with BYOK report errors reading null properties, and the CLI reverts to previous models after reconnection.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-01

## 1. Today's Highlights

Activity was relatively quiet today with no new releases and limited community engagement. The most critical open issue concerns a broken "Approve for this session" feature in the OAuth workflow, which could block automations for users relying on persistent approval. On the PR side, the community continues to contribute UX improvements, notably a long-running PR (#1600) to better visually separate user input from model output in the interactive shell.

## 2. Releases

No new releases in the last 24 hours.

## 3. Hot Issues

*(Only 1 issue updated in the last 24h — full list below:)*

- **#2480 [BUG] Approve for this session doesn't work** — [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2480)  
  **Author:** Econ01 | **Created:** 2026-06-30 | **Comments:** 0 | **👍:** 0  
  A user running Kimi Code CLI v0.20.1 on macOS (Darwin arm64) reports that the `--approve` flag for session-based auth is not respected when using Kimi Code (OAuth) with the `K2.7 Code` model. This is a critical bug because it breaks the OAuth approval flow, meaning users may be forced to re-authenticate every interaction rather than having a persistent session. No community discussion yet, but the severity warrants close monitoring.

## 4. Key PR Progress

*(Only 2 PRs updated in the last 24h — full list below:)*

- **#1600 [OPEN] feat(shell): highlight user input with bright blue and separator for better visibility** — [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/1600)  
  **Author:** liuchong | **Created:** 2026-03-27 | **Updated:** 2026-06-30  
  This long-dormant PR (opened ~3 months ago) was refreshed yesterday. It applies bright blue color (`#007AFF`) to user input text and adds a full-width separator below each user message in `echo.py`. This is a small but high-impact UX enhancement — better visual distinction between user and assistant messages reduces cognitive load during long shell sessions. Good candidate for merge.

- **#2246 [CLOSED] feat(shell): add --prompt-interactive option** — [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2246)  
  **Author:** shuizhongyueming | **Created:** 2026-05-12 | **Updated:** 2026-06-30  
  Now merged. Adds `--prompt-interactive` (short: `-P`) to allow passing an initial prompt when launching the shell UI, while keeping the session open for follow-ups. This resolves feature request #2240 and is valuable for scripting workflows where users want to seed a conversation programmatically.

## 5. Feature Request Trends

Based on broader issue activity (not limited to last 24h), the community is consistently requesting:

- **Persistent session/approval management** — The broken "approve for this session" (#2480) is a recent symptom of a larger demand for reliable, long-lived auth sessions without repeated sign-in prompts.
- **Streaming control options** — Users want finer control over output streaming (e.g., buffered output for CI/CD, real-time for interactive use).
- **Custom shell prompts** — Beyond `--prompt-interactive`, users are asking for the ability to set default system prompts via config file or environment variable.
- **Multi-model routing** — Ability to switch models mid-session or route specific queries to different backends.

## 6. Developer Pain Points

- **OAuth session instability** — The #2480 bug highlights a recurring frustration: OAuth flows that require re-approval per session, breaking automation and CI pipelines.
- **Low visibility of user vs. system output** — PR #1600 directly addresses this, indicating the default shell UI can be confusing when user input and model replies blend together, especially in long histories.
- **Slow PR turnaround** — PR #1600 sat untouched for 3 months; developers notice when quality UX improvements languish in review.
- **Missing release cadence** — No releases in the last 24h is not a problem in isolation, but the community may be waiting for a v0.20.2 that includes the `--prompt-interactive` feature (just merged) and potential auth fix.

---

*Data collected from `github.com/MoonshotAI/kimi-cli` on 2026-07-01.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-01

## Today's Highlights
Version 1.17.12 shipped with adaptive thinking for Claude Sonnet 5 and critical MCP OAuth reconnection fixes. The community's top concerns remain memory instability, lack of cross-model fallback, and friction around permission prompts. A major PR from @eXamadeus aims to close 15 question-UI bugs in one go.

## Releases
**v1.17.12** — [Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.12)
- Enabled adaptive thinking for Claude Sonnet 5.
- Prefer MCP content responses over structured output when both are present.
- Reconnect MCP servers after OAuth even if the server was disabled (@MaxAnderson95).
- Request MCP refresh-token scope during OAuth.
- Show MCP OAuth completion message.

## Hot Issues

1. **#20695 — Memory Megathread** (105 comments, 77 👍)  
   [Issue](https://github.com/anomalyco/opencode/issues/20695)  
   Central collection point for heap snapshot debugging. The maintainers explicitly ask users not to suggest LLM-based fixes and request manual heap snapshots. High engagement signals this is the #1 stability blocker.

2. **#8501 — Expand Pasted Text** (28 comments, 191 👍)  
   [Issue](https://github.com/anomalyco/opencode/issues/8501)  
   The most-voted feature request. Users want to see the full pasted content behind `[Pasted ~1 lines]` summaries for editing and verification.

3. **#7602 — Native Model Fallback / Failover** (28 comments, 90 👍)  
   [Issue](https://github.com/anomalyco/opencode/issues/7602)  
   No way to define fallback between different models. Long-running agents fail hard when a specific model rate-limits or errors.

4. **#8463 — `--dangerously-skip-permissions` (YOLO mode)** (23 comments, 89 👍)  
   [Issue](https://github.com/anomalyco/opencode/issues/8463)  
   Requests a flag to suppress permission prompts in trusted/automated environments. Polarizing but heavily desired by CI/CD users.

5. **#16017 — Go Plan Usage/Balance API** (21 comments, 84 👍)  
   [Issue](https://github.com/anomalyco/opencode/issues/16017)  
   Expose subscription usage data via public API. Dashboard already shows it; users want programmatic access for budgeting.

6. **#24879 — Go Pro Tier ($20) and Share Modifier Discounts** (10 comments, 6 👍)  
   [Issue](https://github.com/anomalyco/opencode/issues/24879)  
   Pricing request for a mid-tier plan between Go and Zen pay-as-you-go, plus first-month discounts.

7. **#33696 — GitHub Copilot Provider Broken** (7 comments, 5 👍)  
   [Issue](https://github.com/anomalyco/opencode/issues/33696)  
   After fresh auth, no models detected. Affects all Copilot users on latest builds.

8. **#28956 — Question Prompt Overlay Blocks Response** (6 comments)  
   [Issue](https://github.com/anomalyco/opencode/issues/28956)  
   No minimize/close button on the question tool overlay. Users cannot scroll back to read AI output before the question appeared.

9. **#33318 — Zen Paid Balance Still Hits Free Limit** (6 comments)  
   [Issue](https://github.com/anomalyco/opencode/issues/33318)  
   Paid Zen users still hitting 200-request free cap. Budgeting confusion blocks adoption of the pay-as-you-go plan.

10. **#34640 — MCP Optional Arrays Materialized as Empty** (4 comments)  
    [Issue](https://github.com/anomalyco/opencode/issues/34640)  
    Optional array params get sent as `[]` even when model didn't intend them, triggering mutually-exclusive argument validation failures.

## Key PR Progress

1. **#34692 — LSP Initialize Timeout to 300s** [OPEN]  
   [PR](https://github.com/anomalyco/opencode/pull/34692)  
   Closes #28289. Increases the LSP handshake timeout for large workspaces. Previously submitted twice with compliance issues; now clean.

2. **#34688 — Recognize More Inline File Paths** [CLOSED]  
   [PR](https://github.com/anomalyco/opencode/pull/34688) (opencode-agent)  
   Expands inline code path detection to `.mjs`, `.cjs`, GraphQL, Dockerfile, dotfiles, and lock/config files. Adds test coverage.

3. **#34116 — Question UI Fixes and UX Improvements** [OPEN]  
   [PR](https://github.com/anomalyco/opencode/pull/34116) (@eXamadeus)  
   Single PR closing **15** issues related to question overlay, including #28956 (no minimize), #23515 (focus stealing), and #11014 (poor scrolling). Major UX win if merged.

4. **#34686 — Stop Replaying Stale Copilot Response IDs** [CLOSED]  
   [PR](https://github.com/anomalyco/opencode/pull/34686) (@rekram1-node)  
   Fixes #31236 — GitHub Copilot gpt-5.5 responses fail with "input item ID does not belong to this connection" when auth token changes mid-session.

5. **#34677 — Experimental Codemode** [OPEN]  
   [PR](https://github.com/anomalyco/opencode/pull/34677) (@rekram1-node)  
   No description yet, but the title suggests a new code-generation mode for the agent. Watch for details.

6. **#30472 — TUI Clipboard Over SSH with tmux** [OPEN]  
   [PR](https://github.com/anomalyco/opencode/pull/30472) (@ayubun)  
   Closes multiple SSH clipboard bugs. Ensures `set-clipboard on` tmux config works over remote sessions.

7. **#30837 — Optimize Snapshots & Loading UI** [CLOSED]  
   [PR](https://github.com/anomalyco/opencode/pull/30837) (@ayubun)  
   Reduces snapshot directory bloat via `alternates` deduplication. Closes #3176 and #30386.

8. **#33950 — Show Real Tool Context in Permission Prompt Title** [OPEN]  
   [PR](https://github.com/anomalyco/opencode/pull/33950) (@bcdady)  
   ACP permission prompts currently show `permission.permission` instead of the actual tool name. This PR surfaces the real context.

9. **#34680 — Use models.dev Reasoning Options** [OPEN]  
   [PR](https://github.com/anomalyco/opencode/pull/34680) (@rekram1-node)  
   Parses and preserves `reasoning_options` from models.dev, drives provider reasoning variants, and adds gateway budget-token handling for Anthropic.

10. **#34682 — Auto Model for GitHub Copilot Provider** [OPEN]  
    [PR](https://github.com/anomalyco/opencode/pull/34682) (@OpeOginni)  
    Closes #34644. Adds the "Auto" model picker to the Copilot provider, matching VSCode behavior where the server selects the best model.

## Feature Request Trends
- **Model fallback and failover** (#7602, #28371) — Users want automatic retry chains across different models, plus the ability to disable reasoning to save tokens.
- **Paste expansion** (#8501) — Highly voted; users need to see and edit pasted content behind summaries.
- **Skip permissions / YOLO mode** (#8463) — Strong demand for bypassing confirmation dialogs in automated and trusted environments.
- **Search in desktop app** (#19143) — Cmd+F to find text within long sessions.
- **Quick-jump sidebar** (#32165) — A slim sidebar listing only user prompts for jumping between turns.

## Developer Pain Points
- **Memory instability** (#20695) — The megathread with 105 comments shows memory leaks remain the top systemic issue.
- **Paid users hitting free caps** (#33318, #33495) — Zen and Go subscribers still limited as if free-tier; billing logic appears broken.
- **Copilot provider reliability** (#33696, #31236) — Auth and session state issues make the Copilot provider unreliable for daily use.
- **Transient network errors not retried** (#30611, #34672) — Only `ECONNRESET` is retried; `ETIMEDOUT` and other timeouts fail sessions outright.
- **MCP tool argument materialization** (#34640) — Optional arrays become empty arrays, breaking tools with mutually-exclusive parameters.
- **opencode serve ignoring config** (#19078) — CLI server command doesn't respect `OPENCODE_CONFIG` environment variable, limiting headless deployments.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-01

## Today's Highlights
Pi v0.80.3 ships with **Anthropic Claude Sonnet 5 support** across Anthropic-compatible and Bedrock providers, with adaptive thinking enabled. The community is actively polishing tool-execution edge cases, with **three critical fixes landing for empty tool results, session state refresh between turns, and provider error surfacing**. A long-standing feature request for `excludeFromContext` on custom messages is nearing merge after 19 days of discussion.

## Releases
**v0.80.3** ([release](https://github.com/earendil-works/pi/releases/tag/v0.80.3))  
- **Anthropic Claude Sonnet 5 support** — Available through inherited Anthropic-compatible and Bedrock provider catalogs with adaptive thinking enabled. See [Providers doc](https://github.com/earendil-works/pi/blob/v0.80.3/packages/coding-agent/docs/providers.md).

## Hot Issues
1. **[#6103](https://github.com/earendil-works/pi/issues/6103)** — [OPEN] **OpenAI Responses API mislabels empty tool results as "(see attached image)"**  
   A latent bug surfaced by the `pi-hashline-edit-pro` extension. Tool calls returning empty output get mislabeled, confusing the model. Already fixed in PR #6196.

2. **[#6197](https://github.com/earendil-works/pi/issues/6197)** — [CLOSED] **pi outputs LaTeX `$\rightarrow$` instead of rendering an arrow**  
   A rendering bug in the TUI causes unescaped LaTeX to leak into user-visible output. Quick community report, closed within hours.

3. **[#6187](https://github.com/earendil-works/pi/issues/6187)** — [OPEN] **Pi login hangs in WSL after GitHub Copilot device authorization**  
   The browser-based device flow completes, but the WSL terminal never detects it. Affects Windows + WSL users onboarding. No fix yet.

4. **[#6181](https://github.com/earendil-works/pi/issues/6181)** — [OPEN] **bash tool: misleading timeout error when value exceeds setTimeout limit**  
   Setting a large timeout (e.g., 99999999) kills the command instantly, but reports "timed out after 99999999 seconds". Minor but confusing UX.

5. **[#5654](https://github.com/earendil-works/pi/issues/5654)** — [OPEN] **Add `excludeFromContext` to custom messages via `sendMessage()`**  
   High-demand feature (PR #5678 in progress). Mirrors existing bash-execution skip behavior. Would allow diagnostic/status messages to be persisted without polluting LLM context.

6. **[#6151](https://github.com/earendil-works/pi/issues/6151)** — [OPEN] **Support `image_url` content type (pass URL directly without base64 conversion)**  
   Currently all image content is base64-encoded. Request to pass URLs directly for supported APIs, reducing token overhead and enabling external image hosting.

7. **[#6133](https://github.com/earendil-works/pi/issues/6133)** — [CLOSED] **pi crashes with `ECONNRESET` during streaming**  
   Upstream provider TCP reset mid-stream escapes the streaming try/catch, becoming an uncaught exception. Needs retry logic hardening.

8. **[#6164](https://github.com/earendil-works/pi/issues/6164)** — [CLOSED] **Image base64 corrupted when sending to Kimi Coding provider**  
   A provider-specific encoding issue: base64 data passes validation for OpenAI but fails for Kimi. Likely a whitespace/line-wrapping mismatch.

9. **[#6188](https://github.com/earendil-works/pi/issues/6188)** — [CLOSED] **Auto-complete only works if slash is the first symbol in input**  
   Users expect auto-complete to trigger after typing text then `/` mid-sentence, but it only fires at input start. UX regression.

10. **[#6186](https://github.com/earendil-works/pi/issues/6186)** — [CLOSED] **`ctx.newSession()` is a silent no-op under `--mode rpc`**  
   Extension API inconsistency: session management methods resolve without error but do nothing in RPC mode. Breaks headless integrations.

## Key PR Progress
1. **[#6196](https://github.com/earendil-works/pi/pull/6196)** — [CLOSED] **fix(ai): return empty string for empty tool results instead of "(see attached image)"**  
   Fixes #6103. Both OpenAI Responses and Completions handlers now return `""` when tool output is empty with no images. Prevents model confusion.

2. **[#5678](https://github.com/earendil-works/pi/pull/5678)** — [OPEN] **Add `excludeFromContext` for custom messages**  
   Authored by mitsuhiko. Adds the flag across agent harness and extension APIs. Persists messages normally but skips them in `convertToLlm`. Also teaches compaction and branch summarization to respect the flag.

3. **[#6176](https://github.com/earendil-works/pi/pull/6176)** — [CLOSED] **Apply extension tool changes before the next provider request in the same run**  
   Fixes session runtime state refresh between turns. When an extension calls `pi.setActiveTools()`, the next provider request now uses the updated tool set immediately.

4. **[#5832](https://github.com/earendil-works/pi/pull/5832)** — [CLOSED] **fix(ai): surface provider HTTP error body instead of opaque SDK message**  
   Behind a proxy/gateway, non-2xx responses with unparseable bodies now show the raw HTTP body instead of "Unknown: UnknownError". Drastically improves debugging.

5. **[#6182](https://github.com/earendil-works/pi/pull/6182)** — [CLOSED] **feat(tui): add redo support to editors**  
   Follow-up to #959. Adds `ctrl+shift+z` / `cmd+shift+z` redo in the TUI editor, completing undo/redo parity.

6. **[#6190](https://github.com/earendil-works/pi/pull/6190)** — [CLOSED] **Add environment variable for `PI_SKILL_PATH`**  
   Enables per-repo skill configuration via `.envrc` without CLI flags. Accepted quickly; community had been requesting this in #6191.

7. **[#6175](https://github.com/earendil-works/pi/pull/6175)** — [CLOSED] **fix(coding-agent): emit session name changes to extensions**  
   Extensions now receive events when session names change, enabling proper UI updates in custom TUI components.

8. **[#6169](https://github.com/earendil-works/pi/pull/6169)** — [CLOSED] **Disable padding for assistant messages**  
   Closes #6168. Removes visual padding around assistant message blocks in the TUI, a long-standing cosmetic annoyance on Discord.

9. **[#6178](https://github.com/earendil-works/pi/pull/6178)** — [CLOSED] **fix: guard against undefined content in tool result messages**  
   Extension tools that return results without a `content` property (e.g., `get_kline`) no longer crash the agent loop. Null-guard added.

10. **[#1737](https://github.com/earendil-works/pi/pull/1737)** — [CLOSED] **Mcowger/move cache breakpoints**  
    Optimizes prompt caching across providers by marking both the final assistant tool_use block and final user message block with `cache_control`. Merged after long review.

## Feature Request Trends
- **Extension/Hook API improvements** — Multiple requests for better lifecycle hooks (`ctx.newSession` in RPC mode, session name events, tool-change notifications). Extensions are growing in complexity and need tighter integration.
- **Headless/hardened integrations** — Durable HITL interrupts (#5901), RPC mode session management (#6186), and proper error recovery on connection drops (#6133) point to enterprise deployment needs.
- **UI customization** — Padding removal (#6168), mid-sentence auto-complete (#6188), redo support (#6182). The TUI is maturing from "works" to "feels right."
- **Provider parity** — New provider requests (Scaleway #6165), model definition fixes (GLM 5.2 Fast #6195, Xiaomi pricing #6138), and API compatibility tweaks (image_url support #6151). The community wants frictionless multi-provider workflows.

## Developer Pain Points
1. **Network resilience** — `ECONNRESET` crashes (#6133) and WSL login hangs (#6187) show fragility in network-handling code, especially with proxy/gateway setups.
2. **Tool execution edge cases** — Empty tool results mislabeled (#6103), large timeouts causing misleading errors (#6181), undefined content crashing the agent loop (#6178). Tool execution is the most common failure surface.
3. **Extension API surprises** — `ctx.newSession()` silently failing in RPC mode (#6186) and tool changes not being picked up mid-run (#6162) erode developer trust in the extension API contract.
4. **Provider-specific encoding bugs** — Kimi base64 corruption (#6164), Xiaomi model pricing mismatches (#6138), Fireworks GLM endpoint misconfiguration (#6195). Each provider integration carries its own edge-case tax.
5. **Auto-compaction crashes** — The auto-compaction feature (#5463) throws unhandled errors when the last message is from an assistant, breaking long sessions silently.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-01

## Today's Highlights
The community continues to push hard on **daemon-managed channel workers** and **subagent governance**, with multiple PRs and issues converging on session archiving, channel memory, and plan-mode isolation for subagents. A critical **Windows process management advisory** (#6067) was published, warning users of severe stability risks on v0.19.x. On the bug front, a **stream activity timeout regression** (#5975) is generating significant user frustration after the v0.19.3 nightly update.

## Releases
- **v0.19.3-nightly.20260701.a974594d7** — A nightly release with documentation refresh for the daemon (wave 2) and an auto-completion feature addition in core configuration. No stable release today.

## Hot Issues (Top 10 by Comment Count)

1. **[#5975] API Error: No stream activity for 120000ms after 19 chunks**  
   *8 comments · 1 👍*  
   Users report that upgrading to v0.19.3 nightly causes frequent streaming timeouts after previously working fine. The community is actively discussing whether this is a latency regression or a server-side issue.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5975)

2. **[#6049] Surprising behaviour for generationConfig timeout set to 0**  
   *7 comments*  
   Setting `timeout: 0` causes instant timeouts instead of meaning "no timeout." Several users were surprised by this design, suggesting a documentation or behavior fix.  
   [Link](https://github.com/QwenLM/qwen-code/issues/6049)

3. **[#5176] Request: allow sub-agent max parallel count setting and put the rest in queue**  
   *4 comments · 1 👍*  
   Users running local LLMs want to limit concurrent sub-agents to avoid resource exhaustion. Still open and needs triage.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5176)

4. **[#4951] [CLOSED] Are the in/out token counts in the statusline accurate?**  
   *4 comments*  
   A user questions whether the displayed token counts are real — reporting hundreds of thousands after just a few messages. Closed, but the underlying confusion persists.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4951)

5. **[#6067] [CRITICAL] Qwen Code Windows platform has process management anomalies**  
   *3 comments*  
   A high-risk advisory detailing process leaks in v0.19.2 (Issue #5873) and broader concerns about PowerShell subprocess cleanup. The author recommends users pause usage on Windows.  
   [Link](https://github.com/QwenLM/qwen-code/issues/6067)

6. **[#6094] [qqbot] Cron/blockStreaming interaction issues + botOpenId instruction timing**  
   *3 comments*  
   Follow-up issues from PR #5902 review — cron tasks with `blockStreaming: on` produce duplicate messages. Needs attention for channel reliability.  
   [Link](https://github.com/QwenLM/qwen-code/issues/6094)

7. **[#5979] Bug: /auth modifies provider config but new sessions still get 401**  
   *3 comments*  
   Changing API keys via `/auth` doesn't propagate to new sessions — a surprising authentication persistence bug.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5979)

8. **[#6084] Follow up ACP daemon loop detection review fixes**  
   *2 comments*  
   The already-merged loop guard has edge cases where stop-hook continuations or repeated invalid tool calls can still cause infinite loops. A focused follow-up is in progress.  
   [Link](https://github.com/QwenLM/qwen-code/issues/6084)

9. **[#6089] macOS: sandbox .sb files missing from lib/chunks/ — fatal launch error**  
   *2 comments*  
   Six sandbox profile files are missing from the macOS distribution, causing `qwen` to crash on launch. A blocking issue for Apple Silicon users.  
   [Link](https://github.com/QwenLM/qwen-code/issues/6089)

10. **[#6069] /model --vision cannot disambiguate duplicate same-id OpenAI-compatible endpoints**  
    *2 comments*  
    When two models share the same `id` but different `baseUrl`, the vision bridge selector cannot pin to the correct endpoint.  
    [Link](https://github.com/QwenLM/qwen-code/issues/6069)

## Key PR Progress (Top 10 by Activity)

1. **[#6073] feat(channel): add channel loop support**  
   Enables recurring chat-bound agent work via `/loop add`, `/loop list`, and `/loop cancel` for channel users. Persisted lifecycle state through the channel session.  
   [Link](https://github.com/QwenLM/qwen-code/pull/6073)

2. **[#6051] feat: explicit channel memory for messaging channels**  
   Adds per-chat/thread memory that authorized members can save, view, and clear — automatically injected into fresh channel sessions.  
   [Link](https://github.com/QwenLM/qwen-code/pull/6051)

3. **[#6058] feat(daemon): Add session archive support**  
   Moves inactive sessions to `chats/archive/`, rejects load/resume of archived sessions, and supports unarchiving. Improves daemon session management.  
   [Link](https://github.com/QwenLM/qwen-code/pull/6058)

4. **[#6085] Fix ACP daemon loop review follow-ups**  
   Makes loop detection a terminal turn path, adds stable invalid-tool bucket, and prevents edge-cases where stop-hook or changing error text could bypass guards.  
   [Link](https://github.com/QwenLM/qwen-code/pull/6085)

5. **[#6031] feat(cli): Add daemon-managed channel worker for serve --channel**  
   Implements `qwen serve --channel <name>` and `--channel all` with out-of-process channel workers supervised by the daemon.  
   [Link](https://github.com/QwenLM/qwen-code/pull/6031)

6. **[#6060] feat(cli): add --project and --global flags to /model**  
   Allows per-project model persistence by writing model selection to workspace-level `.qwen/settings.json` vs. global settings.  
   [Link](https://github.com/QwenLM/qwen-code/pull/6060)

7. **[#6087] feat(core): Disallow plan lifecycle tools in subagents**  
   Prevents ordinary subagents, workflow subagents, and teammates from calling `enter_plan_mode`/`exit_plan_mode`. Plan mode remains caller-owned.  
   [Link](https://github.com/QwenLM/qwen-code/pull/6087)

8. **[#6092] refactor(review): drop deterministic-analysis and autofix steps**  
   Slims the `/review` skill from 11 to 9 steps by removing linter/type-checker auto-run and autofix. Aims to reduce review latency and flakiness.  
   [Link](https://github.com/QwenLM/qwen-code/pull/6092)

9. **[#6033] fix(core): Parse tagged thinking for GLM responses**  
   Enables `<think>...</think>` parsing for DashScope OpenAI-compatible `glm-*` requests, preventing internal reasoning from leaking as normal output.  
   [Link](https://github.com/QwenLM/qwen-code/pull/6033)

10. **[#6011] feat(ui): add mouse click & hover in alternate-screen mode**  
    Adds interactive mouse support to TUI select menus, dialogs, and hover highlights when Virtualized History is enabled.  
    [Link](https://github.com/QwenLM/qwen-code/pull/6011)

## Feature Request Trends

- **Channel & Daemon Improvements** — The largest cluster: channel memory (#6050), group history backfill (#6064), channel loop support (#6073), and daemon-managed channel workers (#5976, #6031) are all landing rapidly.
- **Subagent Governance** — Strong demand for limiting subagent parallelism (#5176), restricting plan-mode tools in subagents (#6083), and better memory persistence for subagent workflows.
- **Model & Provider Flexibility** — Per-project model persistence (#6052), inline model switching in a single command (#5967), and disambiguation of duplicate model endpoints (#6069) are recurring themes.
- **Mobile & Web Shell** — Mobile sidebar for session switching (#6000) and a browser tab favicon (#6091) indicate growing interest in the web-based interface.
- **UI/UX Polish** — Mouse click/hover in TUI (#6053, #6011), frozen transcript view (#5666), and comprehensive settings JSON schema (#6043) suggest the community wants a more polished interactive experience.

## Developer Pain Points

1. **Streaming Timeout Regression** — The v0.19.3 nightly introduced frequent `No stream activity for 120000ms` errors (#5975), breaking workflows that previously worked reliably.
2. **Windows Process Instability** — The advisory (#6067) highlights severe process leaks and missing subprocess cleanup in Windows, with the reporter recommending users pause usage entirely. This is the highest-severity pain point.
3. **Authentication & Configuration Persistence** — Changes made via `/auth` not applying to new sessions (#5979), and `timeout: 0` causing unexpected behavior (#6049) frustrate users trying to configure multiple providers.
4. **macOS Sandbox Blocker** — Missing `.sb` files in the macOS distribution (#6089) cause a fatal crash on launch — a distribution packaging issue that blocks all Apple Silicon users.
5. **Model Switching Confusion** — `/model --vision` cannot disambiguate duplicate provider IDs (#6069) and the two-step `/model` + prompt flow (#5967) remains a workflow friction point for users with complex model setups.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (CodeWhale) Community Digest — 2026-07-01

## Today's Highlights

The project officially rebranded from **deepseek-tui** to **CodeWhale** with the v0.8.66 release, marking a major identity shift. The community is heavily focused on the upcoming **v0.8.67 constitution-first setup wizard**, with 10+ linked issues and the foundational PR #3861 now open. Meanwhile, persistent reliability bugs — TUI freezing on Windows, stalled turns, and excessive token consumption — continue to dominate user complaints.

## Releases

- **v0.8.66** — Released as the first canonical CodeWhale version. The legacy `deepseek-tui` npm package is deprecated. Rebranding docs are available at `docs/REBRAND.md`. Includes critical fixes for MCP auth failures, wildcard tool prefix support, background console window suppression on Windows, and a shared modal UI renderer.

## Hot Issues

1. **#2487** — *Frequent error: Turn stalled – no completion signal received* (Open, 18 comments)  
   Users in `yolo` mode report the TUI becomes completely unresponsive, with `continue` failing to resume. This is a high-impact reliability blocker for power users.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/2487)

2. **#3275** — *CodeWhale overly involved in self-questioning, deviating from user intent* (Open, 13 comments)  
   The agent enters an autonomous loop of proposing, answering, and executing without user confirmation. A regression from issue #3061. Community frustration is palpable.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/3275)

3. **#1177** — *Input cache hit rate too low* (Closed, 25 comments)  
   Users compare CodeWhale unfavorably to DeepSeek-Reasonix (95%+ cache hit rate). Solved in recent releases, but remains a sore point.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/1177)

4. **#1120** — *Cache hit problems persist* (Closed, 23 comments)  
   Follow-up to #1177; confirms fix was shipped but users remain skeptical about residual issues.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/1120)

5. **#1812** — *TUI freezes intermittently on Windows 11* (Open, 9 comments)  
   Complete UI unresponsiveness with logs and thread-state analysis. No keyboard or screen updates, but process stays alive. Affects multiple versions.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/1812)

6. **#743** — *Token consumption increased dramatically* (Closed, 15 comments)  
   A user reported 400M tokens consumed in half a day. The issue points to overly dense dialog interactions. Community calls for optimization.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/743)

7. **#3736** — *Separate work mode from approval policy* (Open, 5 comments)  
   The maintainer identifies four overlapping permission knobs causing mode confusion. A structural refactor is planned for v0.8.67.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/3736)

8. **#3793** — *Build guided localized constitution creator* (Open, 5 comments)  
   Part of the v0.8.67 setup wizard. Users want a language-first, guided constitution, not a blank prompt editor.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/3793)

9. **#765** — *Conversation stuck at "Working" on Windows* (Closed, 9 comments)  
   After npm global install, the TUI hangs indefinitely on chat. Resolved in v0.8.66 but affected many Windows users.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/765)

10. **#1835** — *Windows input field unresponsive with IME (Chinese Sogou)* (Open, 3 comments)  
    A deadlock in IME composition events makes the input field completely unusable for CJK users.  
    [View Issue](https://github.com/Hmbown/CodeWhale/issues/1835)

## Key PR Progress

1. **#3861** — *v0.8.67 constitution-first setup foundation* (Open)  
   Lands the shared state model, persistence, and renderer for the new setup wizard. Foundation code in `crates/`.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3861)

2. **#3833** — *Shared modal UI + progressive /fleet setup* (Closed, v0.8.66)  
   Fixes two systemic modal bugs (opaque bleed-through, footer overflow). Adopted across all `ModalKind` variants.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3833)

3. **#3823** — *Suppress background console windows on Windows* (Closed)  
   Every child process spawned by the TUI no longer pops a console window — critical for Windows UX.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3823)

4. **#3825** — *Expand `${VAR}` env placeholders in MCP stdio config* (Closed)  
   Allows secret injection into MCP child processes via config file placeholders without exposing env vars.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3825)

5. **#3828** — *MCP auth and liveness recovery* (Closed, v0.8.66)  
   Fixes MCP OAuth auth-required failures, stale-token cleanup, and approval timeout recovery.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3828)

6. **#3824** — *Support wildcard disallowed tool prefixes* (Closed)  
   Allows hiding entire MCP server tool sets dynamically. Uses `prefix:*` matching.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3824)

7. **#3858** — *Default /model to configured providers* (Closed)  
   Partial fix for #3830: `/provider` and `/model` now show only configured providers by default.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3858)

8. **#3818** — *Expand active tool run summaries* (Open)  
   Fixes an edge case where collapsing tool-run summaries before history flush caused display bugs.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3818)

9. **#3822** — *Prefer exact binary release assets* (Open)  
   Improves binary asset matching to prefer exact platform matches over prefix-only matches during updates.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3822)

10. **#3860** — *Make launch gate queue test deterministic* (Closed)  
    Fixes a flaky test that relied on wall-clock delays. Now owns the semaphore permit directly.  
    [View PR](https://github.com/Hmbown/CodeWhale/pull/3860)

## Feature Request Trends

- **Constitution-first setup wizard**: The dominant theme for v0.8.67. Users want guided, language-localized constitution creation with clear security posture selectors.
- **Provider/model setup simplification**: High friction on first run. Requests for a provider readiness card, single-API-key happy path, and visual health checks.
- **Modal UI improvements**: A shared `ModalShell` v1 is shipping for release-blocking menus. Community wants consistent, scrollable, and non-bleeding overlays.
- **MCP auth and secret management**: Expanding env var support, OAuth token recovery, and clean error messages for auth failures.
- **Windows parity**: Suppressing console windows, fixing IME deadlocks, and resolving freeze issues are top requests from the Windows user base.

## Developer Pain Points

- **TUI unresponsiveness**: The #1 user complaint. Stalled turns, frozen input fields, and "Working" hang states plague both Windows and macOS users. Multiple issues reference `no completion signal received` errors.
- **Excessive token consumption**: Users report 400M+ tokens consumed in hours. The agent's self-questioning loops and overly dense dialog context are suspected causes. Community urgently requests configurable context limits.
- **Cache hit rate frustration**: Despite fixes, users remain wary of caching performance compared to competing tools. Transparency around cache metrics is desired.
- **Agent autonomy without confirmation**: The TUI frequently deviates from user intent, proposing and executing unverified changes. Users want stricter approval gates, especially in non-`yolo` modes.
- **Windows IME deadlocks**: CJK input method users on Windows face a complete input freeze. No workaround exists in current releases.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*